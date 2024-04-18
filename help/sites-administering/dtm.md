---
title: Adobe Dynamic Tag Management との統合
description: Adobe Dynamic Tag Management との統合について説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: 1e0821f5-627f-4262-ba76-62303890e112
solution: Experience Manager, Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '2146'
ht-degree: 90%

---

# Adobe Dynamic Tag Management との統合 {#integrating-with-adobe-dynamic-tag-management}

[Adobe Dynamic Tag Management](https://business.adobe.com/products/experience-platform/adobe-experience-platform.html?lang=ja) と AEM を統合すると、Dynamic Tag Management Web プロパティを使用して AEM Sites を追跡できます。マーケターは、Dynamic Tag Management を使用して、データ収集のためのタグを管理し、複数のデジタルマーケティングシステムにデータを配信できます。例えば、Dynamic Tag Management を使用して、AEM web サイトの使用状況データを収集し、そのデータを Adobe Analytics または Adobe Target に配信して分析します。

統合する前に、Dynamic Tag Managementを作成します [web プロパティ](https://microsite.omniture.com/t2/help/ja_JP/dtm/#Web_Properties) これは、AEM サイトのドメインを追跡します。 AEM が Dynamic Tag Management ライブラリにアクセスできるように、web プロパティの[ホスティングオプション](https://microsite.omniture.com/t2/help/ja_JP/dtm/#Hosting__Embed_Tab)を設定する必要があります。

統合を設定した後は、Dynamic Tag Management デプロイメントツールおよびルールを変更しても、AEM の Dynamic Tag Management 設定を変更する必要はありません。変更内容は AEM で自動的に有効になります。

>[!NOTE]
>
>カスタムプロキシ設定で DTM を使用している場合、AEMの一部の機能で 3.x API と 4.x API が使用されているので、両方の HTTP クライアントプロキシ設定を行います。
>
>* 3.x は [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient) のように設定します。
>* 4.x は [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator) のように設定します。
>

## デプロイメントオプション {#deployment-options}

次のデプロイメントオプションは、Dynamic Tag Management との統合の設定に影響を与えます。

### Dynamic Tag Management のホスティング {#dynamic-tag-management-hosting}

AEM は、クラウドまたは AEM でホストされている Dynamic Tag Management をサポートします。

* クラウドホスト型：ダイナミック Tag Management JavaScript ライブラリはクラウドに保存され、AEM ページでそれらを直接参照します。
* AEMでホスト：Dynamic Tag Managementは JavaScript ライブラリを生成します。 AEM はワークフローモデルを使用してライブラリを取得し、インストールします。

実装で使用するホスティングのタイプによって、実行する設定タスクおよび実装タスクの一部が決定されます。ホスティングオプションについて詳しくは、Dynamic Tag Management ヘルプの[ホスティング - 「埋め込み」タブ](https://microsite.omniture.com/t2/help/ja_JP/dtm/#Hosting__Embed_Tab)を参照してください。

### ステージングおよび実稼動ライブラリ {#staging-and-production-library}

AEM オーサーインスタンスで Dynamic Tag Management のステージング用コードを使用するか実稼動用コードを使用するかを決定します。

一般的に、オーサーインスタンスでは Dynamic Tag Management のステージングライブラリを使用し、実稼動インスタンスでは実稼動ライブラリを使用します。このシナリオでは、オーサーインスタンスを使用して、未承認の Dynamic Tag Management 設定をテストできます。

必要に応じて、オーサーインスタンスで実稼動ライブラリを使用できます。ライブラリがクラウドホスト型の場合は、テスト目的でステージングライブラリを使用するよう切り替えられる web ブラウザープラグインを利用できます。

### Dynamic Tag Management デプロイメントフックの使用 {#using-the-dynamic-tag-management-deployment-hook}

AEM が Dynamic Tag Management ライブラリをホストしている場合は、Dynamic Tag Management デプロイメントフックサービスを使用して、ライブラリの更新を AEM に自動的にプッシュできます。Dynamic Tag Management web プロパティのプロパティが編集されるなど、ライブラリに変更が加えられると、ライブラリの更新がプッシュされます。

デプロイメントフックを使用するには、Dynamic Tag ManagementがライブラリをホストするAEM インスタンスに接続できる必要があります。 Dynamic Tag Management サーバーが [AEM にアクセスできるようにしてください](/help/sites-administering/dtm.md#enabling-access-for-the-deployment-hook-service)。

AEM がファイアウォールの背後にある場合など、環境によっては AEM に到達できないことがあります。そのような場合には、AEM のポーリングインポーターオプションを使用して、ライブラリを定期的に取得できます。cron ジョブ式でライブラリダウンロードのスケジュールを決定します。

## デプロイメントフックサービスへのアクセスの有効化 {#enabling-access-for-the-deployment-hook-service}

Dynamic Tag Management デプロイメントフックサービスによる AEM へのアクセスを有効にして、このサービスが AEM ホスト型ライブラリを更新できるようにします。必要に応じて、ステージングライブラリと実稼動ライブラリを更新する Dynamic Tag Management サーバーの IP アドレスを指定します。

* ステージング：`107.21.99.31`
* 実稼動：`23.23.225.112` および `204.236.240.48`

[Web コンソール](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)または [`sling:OsgiConfig`](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) ノードを使用して、設定を実行します。

* Web コンソールでは、設定ページの Adobe DTM デプロイフック設定項目を使用します。
* OSGi 設定の場合、サービス PID は `com.adobe.cq.dtm.impl.servlets.DTMDeployHookServlet` です。

次の表に、設定するプロパティを示します。

| Web コンソールのプロパティ | OSGi のプロパティ | 説明 |
|---|---|---|
| ステージング DTM IP のホワイトリスト | `dtm.staging.ip.whitelist` | ステージングライブラリを更新する Dynamic Tag Management サーバーの IP アドレス。 |
| 実稼動 DTM IP のホワイトリスト | `dtm.production.ip.whitelist` | 実稼動ライブラリを更新する Dynamic Tag Management サーバーの IP アドレス。 |

## Dynamic Tag Management 設定の作成 {#creating-the-dynamic-tag-management-configuration}

AEM インスタンスが Dynamic Tag Management で認証され、web プロパティとやり取りできるようにするクラウド設定を作成します。

>[!NOTE]
>
>DTM Web プロパティに Adobe Analytics ツールが含まれていて、[コンテンツインサイト](/help/sites-authoring/content-insights.md)も使用している場合は、ページに 2 つの Adobe Analytics トラッキングコードを含めないようにしてください。あなたの [Adobe Analytics Cloud設定](/help/sites-administering/adobeanalytics-connect.md#configuring-the-connection-to-adobe-analytics)を選択し、「トラッキングコードを含めない」オプションを選択します。

### 一般設定 {#general-settings}

<table>
 <tbody>
  <tr>
   <th>プロパティ</th>
   <th>説明</th>
  </tr>
  <tr>
   <td>API トークン</td>
   <td>Dynamic Tag Management ユーザーアカウントの API トークンプロパティの値。AEM は、Dynamic Tag Management での認証にこのプロパティを使用します。</td>
  </tr>
  <tr>
   <td>Company（会社）</td>
   <td>ログイン ID が関連付けられている会社。</td>
  </tr>
  <tr>
   <td>プロパティ</td>
   <td>AEM サイト用のタグを管理するために作成した web プロパティの名前。</td>
  </tr>
  <tr>
   <td>作成者に対して実稼動用のコードを含める</td>
   <td><p>このオプションを選択すると、AEMのオーサーインスタンスとパブリッシュインスタンスで Dynamic Tag Management ライブラリの実稼動版が使用されます。 </p> <p>このオプションが選択されていない場合は、オーサーインスタンスにはステージング設定が適用され、パブリッシュインスタンスには実稼動設定が適用されます。</p> </td>
  </tr>
 </tbody>
</table>

### セルフホスティングプロパティ - ステージングと実稼動 {#self-hosting-properties-staging-and-production}

Dynamic Tag Management 設定の次のプロパティによって、AEM は Dynamic Tag Management ライブラリをホストできます。AEM は、これらのプロパティを使用してライブラリをダウンロードし、インストールできます。オプションで、ライブラリを自動的に更新し、Dynamic Tag Management 管理アプリケーションで行われたすべての変更を反映させることができます。

一部のプロパティは、Dynamic Tag Management web プロパティの「埋め込み」タブの「ライブラリのダウンロード」セクションから取得した値を使用します。詳しくは、Dynamic Tag Management ヘルプの[ライブラリダウンロード](https://microsite.omniture.com/t2/help/ja_JP/dtm/#Library_Download)を参照してください。

>[!NOTE]
>
>Dynamic Tag Management バンドルを AEM にホスティングしている場合は、Dynamic Tag Management でライブラリダウンロードを有効にしてから設定を作成する必要がありますまた、ダウンロードするライブラリを提供する Akamai も有効にする必要があります。

Dynamic Tag Management ライブラリを AEM にホスティングしている場合は、設定に従って、AEM が web プロパティの一部のプロパティを自動的に設定します。次の表の説明を参照してください。

<table>
 <tbody>
  <tr>
   <th>プロパティ</th>
   <th>説明</th>
  </tr>
  <tr>
   <td>セルフホスティングを使用</td>
   <td>Dynamic Tag Management ライブラリファイルを AEM にホスティングする場合に選択します。このオプションを選択すると、この表のその他のプロパティが表示されます。</td>
  </tr>
  <tr>
   <td>DTM バンドル URL</td>
   <td>Dynamic Tag Management ライブラリのダウンロードに使用する URL。この値は、Dynamic Tag Management のライブラリダウンロードページの「ダウンロード URL」セクションから取得します。安全上の理由から、この値は手動で設定する必要があります。</td>
  </tr>
  <tr>
   <td>ダウンロードワークフロー</td>
   <td><p>Dynamic Tag Management ライブラリのダウンロードおよびインストールに使用するワークフローモデル。デフォルトのモデルは「デフォルトの DTM バンドルのダウンロード」です。カスタムモデルを作成した場合を除き、このモデルを使用します。</p> <p>デフォルトのダウンロードワークフローは、ライブラリがダウンロードされると自動的にアクティベートします。</p> </td>
  </tr>
  <tr>
   <td>ドメインのヒント</td>
   <td><p>（オプション）Dynamic Tag Management ライブラリをホスティングしている AEM サーバーのドメイン。に設定されたデフォルトドメインを上書きできるように値を指定します <a href="/help/sites-developing/externalizer.md">Day CQ Link Externalizer サービス</a>.</p> <p>Dynamic Tag Management に接続すると、AEM はこの値を使用して、Dynamic Tag Management web プロパティのライブラリダウンロードプロパティのステージング HTTP パスまたは実稼動 HTTP パスを設定します。</p> </td>
  </tr>
  <tr>
   <td>ドメインのヒントを保護</td>
   <td><p>（オプション）HTTPS 経由で Dynamic Tag Management ライブラリをホスティングしている AEM サーバーのドメイン。に設定されたデフォルトドメインを上書きできるように値を指定します <a href="/help/sites-developing/externalizer.md">Day CQ Link Externalizer サービス</a>.</p> <p>Dynamic Tag Management に接続すると、AEM はこの値を使用して、Dynamic Tag Management web プロパティのライブラリダウンロードプロパティのステージング HTTP パスまたは実稼動 HTTP パスを設定します。</p> </td>
  </tr>
  <tr>
   <td>共有暗号鍵</td>
   <td><p>（オプション）ダウンロードの解読に使用する共有暗号鍵。この値は、Dynamic Tag Management のライブラリダウンロードページの「共有暗号鍵」フィールドから取得します。</p> <p><strong>注意：</strong> AEMがインストールされているコンピューターに OpenSSL ライブラリをインストールし、ダウンロードしたライブラリをAEMで復号化できるようにする必要があります。</p> </td>
  </tr>
  <tr>
   <td>ポーリングインポーターを有効にする</td>
   <td><p>（オプション）更新されたバージョンを確実に使用するよう、Dynamic Tag Management ライブラリを定期的にダウンロードおよびインストールするために選択します。選択した場合、Dynamic Tag Management は HTTP POST リクエストをデプロイフック URL に送信しません。</p> <p>AEM は、Dynamic Tag Management web プロパティのライブラリダウンロードプロパティのデプロイフック URL プロパティを自動的に設定します。選択した場合、このプロパティは値なしで設定されます。選択しない場合、このプロパティには Dynamic Tag Management 設定の URL が設定されます。</p> <p>例えば、AEM がファイアウォールの背後にある場合など、Dynamic Tag Management デプロイフックが AEM に接続できない場合に、ポーリングインポーターを有効にします。</p> </td>
  </tr>
  <tr>
   <td>スケジュール式</td>
   <td>（「ポーリングインポーターを有効にする」を選択した場合に表示され、必須になります。）Dynamic Tag management ライブラリをいつダウンロードするかを制御する cron 式。</td>
  </tr>
 </tbody>
</table>

![chlimage_1-352](assets/chlimage_1-352.png)

### クラウドホスティングプロパティ - ステージングと実稼動 {#cloud-hosting-properties-staging-and-production}

Dynamic Tag Configuration がクラウドホスト型の場合は、Dynamic Tag Management 設定の次のプロパティを設定します。

<table>
 <tbody>
  <tr>
   <th>プロパティ</th>
   <th>説明</th>
  </tr>
  <tr>
   <td>セルフホスティングを使用</td>
   <td>Dynamic Tag Management ライブラリファイルがクラウド内にホストされている場合は、このオプションをオフにします。</td>
  </tr>
  <tr>
   <td>ヘッダーコード</td>
   <td><p>ホスト用 Dynamic Tag Management から取得されるステージング用ヘッダーコード。Dynamic Tag Management に接続すると、この値が自動的に設定されます。</p> <p> Dynamic Tag Management でこのコードを確認するには、「埋め込み」タブをクリックし、ホスト名をクリックします。「ヘッダーコード」セクションを展開し、必要に応じて「ステージング埋め込みコード」領域または「実稼動埋め込みコード」領域の「埋め込みコードをコピー」をクリックします。</p> </td>
  </tr>
  <tr>
   <td>フッターコード</td>
   <td><p>ホスト用 Dynamic Tag Management から取得されるステージング用フッターコード。Dynamic Tag Management に接続すると、この値が自動的に設定されます。</p> <p>Dynamic Tag Management でこのコードを確認するには、「埋め込み」タブをクリックし、ホスト名をクリックします。「フッターコード」セクションを拡張し、必要に応じて「ステージング埋め込みコード」領域または「実稼動埋め込みコード」領域の「埋め込みコードをコピー」をクリックします。</p> </td>
  </tr>
 </tbody>
</table>

![chlimage_1-353](assets/chlimage_1-353.png)

以下の手順では、タッチ操作向け UI を使用して、Dynamic Tag Management との統合を設定します。

1. パネルで、ツール／操作／クラウド／クラウドサービスをクリックします。
1. 動的Tag Management領域に、設定を追加するために次のいずれかのリンクが表示されます。

   * 初めて設定を追加する場合は「今すぐ設定」をクリックします。
   * ひとつ以上の設定が作成されている場合は、「設定を表示」をクリックし、「利用可能な設定」の横の「+」リンクをクリックします。

   ![chlimage_1-354](assets/chlimage_1-354.png)

1. 設定のタイトルを入力して、「作成」をクリックします。
1. 「API トークン」フィールドに、Dynamic Tag Management ユーザーアカウントの API トークンプロパティの値を入力します。

   API トークンの値については、DTM のクライアントケアにお問い合わせください。

   >[!NOTE]
   >
   >API トークンは、Dynamic Tag Management ユーザーが明示的にリクエストするまで有効期限切れになりません。

   ![chlimage_1-355](assets/chlimage_1-355.png)

1. 「DTM に接続」をクリックします。AEM が Dynamic Tag Management で認証され、アカウントが関連付けられている会社のリストを取得します。
1. 会社を選択し、AEM サイトの追跡に使用するプロパティを選択します。
1. オーサーインスタンスでステージング用コードを使用する場合は、「作成者に対して実稼動用のコードを含める」の選択を解除します。
1. 必要に応じて「ステージング設定」タブおよび「実稼動設定」タブのプロパティに値を設定し、「OK」をクリックします。

## Dynamic Tag Management ライブラリの手動ダウンロード {#manually-downloading-the-dynamic-tag-management-library}

Dynamic Tag Management ライブラリを手動でダウンロードして、AEM 上でただちに更新します。例えば、ライブラリを自動ダウンロードするようにポーリングインポーターをスケジュール設定する前に更新されたライブラリをテストする場合は、手動でダウンロードします。

1. パネルで、ツール／操作／クラウド／クラウドサービスをクリックします。
1. 「Dynamic Tag Management」領域で、「設定を表示」をクリックし、設定をクリックします。
1. 「ステージング設定」領域または「実稼動設定」領域で、「ダウンロードワークフローをトリガー」ボタンをクリックして、ライブラリバンドルをダウンロードおよびデプロイします。

   ![chlimage_1-356](assets/chlimage_1-356.png)

>[!NOTE]
>
>ダウンロードしたファイルは、`/etc/clientlibs/dtm/my config/companyID/propertyID/servertype`に保存されます。
>
>次の設定は、[DTM 設定](#creating-the-dynamic-tag-management-configuration)から直接取得しました。
>
>* `myconfig`
>* `companyID`
>* `propertyID`
>* `servertype`
>

## Dynamic Tag Management 設定とサイトの関連付け {#associating-a-dynamic-tag-management-configuration-with-your-site}

AEM が必要なスクリプトをページに追加できるよう、Dynamic Tag Management 設定と web サイトのページを関連付けます。サイトのルートページと設定を関連付けます。そのページのすべての子ページが関連付けを継承します。必要に応じて、子ページの関連付けを上書きできます。

次の手順を実行して、ページとその子ページを Dynamic Tag Management 設定に関連付けます。

1. サイトのルートページをクラシック UI で開きます。
1. サイドキックを使用して、ページのプロパティを開きます。
1. 「クラウドサービス」タブで、「サービスを追加」をクリックし、「Dynamic Tag Management」を選択して、「OK」をクリックします。

   ![chlimage_1-357](assets/chlimage_1-357.png)

1. Dynamic Tag Management ドロップダウンメニューを使用して設定を選択し、「OK」をクリックします。

次の手順を実行して、ページに対する継承された設定の関連付けを上書きします。上書きは、ページとすべての子ページに影響を与えます。

1. クラシック UI でページを開きます。
1. サイドキックを使用して、ページのプロパティを開きます。
1. 「クラウドサービス」タブで、「継承元」プロパティの横の鍵アイコンをクリックし、確認ダイアログボックスで「はい」をクリックします。

   ![chlimage_1-358](assets/chlimage_1-358.png)

1. Dynamic Tag Management 設定を削除するか、別の Dynamic Tag Management 設定を選択して、「OK」をクリックします。
