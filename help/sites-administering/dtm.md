---
title: Adobe Dynamic Tag Management との統合
description: Dynamic Tag Managementとの統合について説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: 1e0821f5-627f-4262-ba76-62303890e112
source-git-commit: 4289c68feb51842b5649f7cff73c5c4bc38add6c
workflow-type: tm+mt
source-wordcount: '2146'
ht-degree: 25%

---

# Adobe Dynamic Tag Management との統合 {#integrating-with-adobe-dynamic-tag-management}

[Adobe Dynamic Tag Management](https://business.adobe.com/products/experience-platform/adobe-experience-platform.html?lang=ja) と AEM を統合すると、Dynamic Tag Management Web プロパティを使用して AEM Sites を追跡できます。マーケターは、Dynamic Tag Management を使用して、データ収集のためのタグを管理し、複数のデジタルマーケティングシステムにデータを配信できます。例えば、Dynamic Tag Management を使用して、AEM web サイトの使用状況データを収集し、そのデータを Adobe Analytics または Adobe Target に配信して分析します。

統合する前に、Dynamic Tag Managementを作成します [web プロパティ](https://microsite.omniture.com/t2/help/en_US/dtm/#Web_Properties) AEMサイトのドメインを追跡するためのものです。 AEM が Dynamic Tag Management ライブラリにアクセスできるように、web プロパティの[ホスティングオプション](https://microsite.omniture.com/t2/help/ja_JP/dtm/#Hosting__Embed_Tab)を設定する必要があります。

統合を設定した後、Dynamic Tag Managementデプロイメントツールおよびルールを変更した場合、AEMで Dynamic Tag Managementの設定を変更する必要はありません。 変更はAEMで自動的に利用できます。

>[!NOTE]
>
>カスタムプロキシ設定で DTM を使用している場合は、AEMの一部の機能で 3.x API を使用し、他の一部の機能では 4.x API を使用するので、両方の HTTP クライアントプロキシ設定を指定します。
>
>* 3.x は [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient) のように設定します。
>* 4.x は [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator) のように設定します。
>

## デプロイメントオプション {#deployment-options}

次のデプロイメントオプションは、Dynamic Tag Managementとの統合の設定に影響します。

### Dynamic Tag Management Hosting {#dynamic-tag-management-hosting}

AEMは、クラウド内でホストされる、またはAEMでホストされる Dynamic Tag Managementをサポートします。

* クラウドでホストされる： Dynamic Tag Management JavaScript ライブラリはクラウドに保存され、AEMページはそれらを直接参照します。
* AEMでホストされる： Dynamic Tag Managementは JavaScript ライブラリを生成します。 AEMは、ワークフローモデルを使用して、ライブラリを取得してインストールします。

実装で使用されるホスティングのタイプによって、実行する設定タスクと実装タスクの一部が決まります。 ホスティングオプションについて詳しくは、 [ホスティング — 「埋め込み」タブ](https://microsite.omniture.com/t2/help/ja_JP/dtm/#Hosting__Embed_Tab) (Dynamic Tag Managementヘルプ ) を参照してください。

### ステージングおよび実稼動用ライブラリ {#staging-and-production-library}

AEMオーサーインスタンスで Dynamic Tag Managementステージング用のコードと実稼動用のコードのどちらを使用するかを決定します。

通常、オーサーインスタンスは Dynamic Tag Managementステージングライブラリを使用し、実稼動インスタンスは実稼動ライブラリを使用します。 このシナリオを使用すると、オーサーインスタンスを使用して、未承認の Dynamic Tag Management設定をテストできます。

必要に応じて、オーサーインスタンスで実稼動ライブラリを使用できます。ライブラリがクラウドホスト型の場合は、テスト目的でステージングライブラリを使用するよう切り替えられる web ブラウザープラグインを利用できます。

### Dynamic Tag Management Deployment Hook の使用 {#using-the-dynamic-tag-management-deployment-hook}

AEMが Dynamic Tag Managementライブラリをホストする場合、Dynamic Tag Managementデプロイメントフックサービスを使用して、ライブラリの更新をAEMに自動的にプッシュできます。 Dynamic Tag Management web プロパティのプロパティが編集されるなど、ライブラリに変更が加えられると、ライブラリの更新がプッシュされます。

デプロイメントフックを使用するには、Dynamic Tag Managementが、ライブラリをホストするAEMインスタンスに接続できる必要があります。 [AEMへのアクセスを有効にする](/help/sites-administering/dtm.md#enabling-access-for-the-deployment-hook-service) Dynamic Tag Managementサーバー用。

AEM がファイアウォールの背後にある場合など、環境によっては AEM に到達できないことがあります。そのような場合には、AEM のポーリングインポーターオプションを使用して、ライブラリを定期的に取得できます。cron ジョブ式は、ライブラリのダウンロードのスケジュールを示します。

## デプロイメントフックサービスへのアクセスの有効化 {#enabling-access-for-the-deployment-hook-service}

AEMにアクセスして、Dynamic Tag ManagementデプロイメントフックサービスがAEMでホストされるライブラリを更新できるようにします。 必要に応じて、ステージングライブラリと実稼動ライブラリを更新する Dynamic Tag Management サーバーの IP アドレスを指定します。

* ステージング：`107.21.99.31`
* 実稼動：`23.23.225.112` および `204.236.240.48`

[Web コンソール](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)または [`sling:OsgiConfig`](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository) ノードを使用して、設定を実行します。

* Web コンソールでは、設定ページの Adobe DTM デプロイフック設定項目を使用します。
* OSGi 設定の場合、サービス PID は `com.adobe.cq.dtm.impl.servlets.DTMDeployHookServlet` です。

次の表に、設定するプロパティを示します。

| Web コンソールのプロパティ | OSGi のプロパティ | 説明 |
|---|---|---|
| ステージング DTM IP のホワイトリスト | `dtm.staging.ip.whitelist` | ステージングライブラリを更新する Dynamic Tag Managementサーバーの IP アドレス。 |
| 実稼動 DTM IP のホワイトリスト | `dtm.production.ip.whitelist` | 実稼動用ライブラリを更新する Dynamic Tag Managementサーバーの IP アドレス。 |

## Dynamic Tag Management設定の作成 {#creating-the-dynamic-tag-management-configuration}

クラウド設定を作成して、AEMインスタンスが Dynamic Tag Managementで認証され、Web プロパティとやり取りできるようにします。

>[!NOTE]
>
>DTM Web プロパティに Adobe Analytics ツールが含まれていて、[コンテンツインサイト](/help/sites-authoring/content-insights.md)も使用している場合は、ページに 2 つの Adobe Analytics トラッキングコードを含めないようにしてください。を [Adobe Analytics Cloud設定](/help/sites-administering/adobeanalytics-connect.md#configuring-the-connection-to-adobe-analytics)「トラッキングコードを含めない」オプションを選択します。

### 一般設定 {#general-settings}

<table>
 <tbody>
  <tr>
   <th>Property</th>
   <th>説明</th>
  </tr>
  <tr>
   <td>API トークン</td>
   <td>Dynamic Tag Managementユーザーアカウントの API トークンプロパティの値。 AEMは、このプロパティを使用して Dynamic Tag Managementの認証をおこないます。</td>
  </tr>
  <tr>
   <td>Company（会社）</td>
   <td>ログイン ID が関連付けられている会社。</td>
  </tr>
  <tr>
   <td>プロパティ</td>
   <td>AEMサイトのタグを管理するために作成した Web プロパティの名前。</td>
  </tr>
  <tr>
   <td>作成者に対して実稼動用のコードを含める</td>
   <td><p>このオプションを選択すると、AEMオーサーインスタンスとパブリッシュインスタンスで、実稼動版の Dynamic Tag Managementライブラリが使用されます。 </p> <p>このオプションを選択しない場合、ステージング設定はオーサーインスタンスに適用され、実稼動設定はパブリッシュインスタンスに適用されます。</p> </td>
  </tr>
 </tbody>
</table>

### 自己ホスティングプロパティ — ステージングと実稼動 {#self-hosting-properties-staging-and-production}

次の Dynamic Tag Management設定プロパティを使用すると、AEMは Dynamic Tag Managementライブラリをホストできます。 プロパティを使用すると、AEMはライブラリをダウンロードしてインストールできます。 必要に応じて、ライブラリを自動的に更新して、Dynamic Tag Management管理アプリケーションでおこなわれた変更を反映させることができます。

一部のプロパティでは、Dynamic Tag Management Web プロパティの「埋め込み」タブの「ライブラリのダウンロード」セクションから取得した値を使用します。 詳しくは、 [ライブラリのダウンロード](https://microsite.omniture.com/t2/help/ja_JP/dtm/#Library_Download) (Dynamic Tag Managementヘルプ ) を参照してください。

>[!NOTE]
>
>AEM上に Dynamic Tag Managementバンドルをホストしている場合は、設定を作成する前に、Dynamic Tag Managementでライブラリのダウンロードを有効にする必要があります。 また、Akamai はダウンロード用のライブラリを提供するので、Akamai を有効にする必要があります。

AEM上で Dynamic Tag Managementライブラリをホストする場合、AEMは、設定に従って Web プロパティの一部のプロパティを自動的に設定します。 次の表の説明を参照してください。

<table>
 <tbody>
  <tr>
   <th>Property</th>
   <th>説明</th>
  </tr>
  <tr>
   <td>自己ホストを使用</td>
   <td>AEM上で Dynamic Tag Managementライブラリファイルをホストする場合は、「 」を選択します。 このオプションを選択すると、この表の他のプロパティが表示されます。</td>
  </tr>
  <tr>
   <td>DTM バンドル URL</td>
   <td>Dynamic Tag Managementライブラリのダウンロードに使用する URL。 この値は、Dynamic Tag Managementのライブラリダウンロードページの「ダウンロード URL 」セクションから取得します。 セキュリティ上の理由から、この値は手動で設定する必要があります。</td>
  </tr>
  <tr>
   <td>ダウンロードワークフロー</td>
   <td><p>Dynamic Tag Managementライブラリのダウンロードとインストールに使用するワークフローモデル。 デフォルトのモデルは、「Default DTM Bundle Download」です。 カスタムモデルを作成していない場合は、このモデルを使用します。</p> <p>デフォルトのダウンロードワークフローは、ライブラリがダウンロードされる際に、自動的にアクティベートします。</p> </td>
  </tr>
  <tr>
   <td>ドメインのヒント</td>
   <td><p>（オプション）Dynamic Tag ManagementライブラリをホストしているAEMサーバーのドメイン。 値を指定して、 <a href="/help/sites-developing/externalizer.md">Day CQ Link Externalizer サービス</a>.</p> <p>Dynamic Tag Managementに接続する場合、AEMはこの値を使用して、Dynamic Tag Management Web プロパティの Library Download プロパティの Staging HTTP Path または Production HTTP Path を設定します。</p> </td>
  </tr>
  <tr>
   <td>ドメインのヒントを保護</td>
   <td><p>（オプション）HTTPS 経由で Dynamic Tag ManagementライブラリをホストしているAEMサーバーのドメイン。 値を指定して、 <a href="/help/sites-developing/externalizer.md">Day CQ Link Externalizer サービス</a>.</p> <p>Dynamic Tag Managementに接続する場合、AEMはこの値を使用して、Dynamic Tag Management Web プロパティの Library Download プロパティの Staging HTTPS Path または Production HTTPS Path を設定します。</p> </td>
  </tr>
  <tr>
   <td>共有暗号鍵</td>
   <td><p>（オプション）ダウンロードの復号化に使用する共有暗号鍵。 この値は、Dynamic Tag Management のライブラリダウンロードページの「共有暗号鍵」フィールドから取得します。</p> <p><strong>注意：</strong> AEMがダウンロードしたライブラリを復号化できるよう、AEMがインストールされているコンピューターに OpenSSL ライブラリをインストールしておく必要があります。</p> </td>
  </tr>
  <tr>
   <td>ポーリングインポーターを有効にする</td>
   <td><p>（オプション）更新されたバージョンを確実に使用するよう、Dynamic Tag Management ライブラリを定期的にダウンロードおよびインストールするために選択します。選択した場合、Dynamic Tag Management は HTTP POST リクエストをデプロイフック URL に送信しません。</p> <p>AEMは、Dynamic Tag Management Web プロパティのライブラリダウンロードプロパティのデプロイフック URL プロパティを自動的に設定します。 選択すると、プロパティに値が設定されません。 選択しない場合、このプロパティには Dynamic Tag Management 設定の URL が設定されます。</p> <p>例えば、AEMがファイアウォールの背後にある場合など、Dynamic Tag ManagementのデプロイフックがAEMに接続できない場合に、ポーリングインポーターを有効にします。</p> </td>
  </tr>
  <tr>
   <td>スケジュール式</td>
   <td>（「ポーリングインポーターを有効にする」が選択されている場合に表示され、必須です）。 Dynamic Tag Management ライブラリをダウンロードするタイミングを制御する cron 式です。</td>
  </tr>
 </tbody>
</table>

![chlimage_1-352](assets/chlimage_1-352.png)

### クラウドホスティングのプロパティ — ステージング環境および実稼動環境 {#cloud-hosting-properties-staging-and-production}

Dynamic Tag 設定がクラウドホスト型の場合は、Dynamic Tag Management設定に対して次のプロパティを設定します。

<table>
 <tbody>
  <tr>
   <th>Property</th>
   <th>説明</th>
  </tr>
  <tr>
   <td>自己ホストを使用</td>
   <td>Dynamic Tag Managementライブラリファイルがクラウドでホストされている場合は、このオプションをオフにします。</td>
  </tr>
  <tr>
   <td>ヘッダーコード</td>
   <td><p>ホスト用に Dynamic Tag Managementから取得したステージング用のヘッダーコード。 この値は、Dynamic Tag Managementに接続すると自動的に設定されます。</p> <p> コードを Dynamic Tag Managementで表示するには、「埋め込み」タブをクリックし、ホスト名をクリックします。 「ヘッダーコード」セクションを展開し、必要に応じて、ステージング埋め込みコードの「埋め込みコードをコピー」領域または「実稼動埋め込みコード」領域をクリックします。</p> </td>
  </tr>
  <tr>
   <td>フッターコード</td>
   <td><p>ホスト用に Dynamic Tag Managementから取得したステージング用のフッターコード。 この値は、Dynamic Tag Managementに接続すると自動的に設定されます。</p> <p>コードを Dynamic Tag Managementで表示するには、「埋め込み」タブをクリックし、ホスト名をクリックします。 「フッターコード」セクションを拡張し、必要に応じて「ステージング埋め込みコード」領域または「実稼動埋め込みコード」領域の「埋め込みコードをコピー」をクリックします。</p> </td>
  </tr>
 </tbody>
</table>

![chlimage_1-353](assets/chlimage_1-353.png)

次の手順では、タッチ操作向け UI を使用して、Dynamic Tag Managementとの統合を設定します。

1. レールで、ツール/操作/クラウド/Cloud Serviceをクリックします。
1. Dynamic Tag Management領域に、設定を追加するための次のリンクの 1 つが表示されます。

   * 初めて設定を追加する場合は「今すぐ設定」をクリックします。
   * ひとつ以上の設定が作成されている場合は、「設定を表示」をクリックし、「利用可能な設定」の横の「+」リンクをクリックします。

   ![chlimage_1-354](assets/chlimage_1-354.png)

1. 設定のタイトルを入力し、「作成」をクリックします。
1. 「 API トークン」フィールドに、Dynamic Tag Managementユーザーアカウントの API トークンプロパティの値を入力します。

   API トークンの値については、DTM のクライアントケアにお問い合わせください。

   >[!NOTE]
   >
   >API トークンは、Dynamic Tag Management ユーザーが明示的にリクエストするまで有効期限切れになりません。

   ![chlimage_1-355](assets/chlimage_1-355.png)

1. 「 DTM に接続」をクリックします。 AEMは Dynamic Tag Managementで認証され、アカウントに関連付けられている会社のリストを取得します。
1. 「会社」を選択し、AEMサイトの追跡に使用するプロパティを選択します。
1. オーサーインスタンスでステージング用コードを使用している場合は、「オーサーに実稼動用コードを含める」をオフにします。
1. 必要に応じて、「ステージング設定」タブと「実稼動設定」タブでプロパティの値を指定し、「OK」をクリックします。

## Dynamic Tag Management Library の手動ダウンロード {#manually-downloading-the-dynamic-tag-management-library}

AEMで直ちに更新するには、Dynamic Tag Managementライブラリを手動でダウンロードします。 例えば、ポーリングインポーターがライブラリを自動的にダウンロードするようにスケジュール設定される前に、更新されたライブラリをテストする場合は、手動でダウンロードします。

1. レールで、ツール/操作/クラウド/Cloud Serviceをクリックします。
1. Dynamic Tag Management領域で、「設定を表示」をクリックし、設定をクリックします。
1. 「ステージング設定」領域または「実稼動設定」領域で、「トリガーのダウンロードワークフロー」ボタンをクリックして、ライブラリバンドルをダウンロードしてデプロイします。

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

## Dynamic Tag Management設定とサイトの関連付け {#associating-a-dynamic-tag-management-configuration-with-your-site}

Dynamic Tag Management設定を Web サイトのページに関連付け、AEMが必要なスクリプトをページに追加できるようにします。 サイトのルートページを設定に関連付けます。 そのページのすべての子ページが関連付けを継承します。必要に応じて、下位のページで関連付けを上書きできます。

次の手順を実行して、ページとその子ページを Dynamic Tag Management 設定に関連付けます。

1. クラシック UI でサイトのルートページを開きます。
1. 「Sidekick」を使用してページのプロパティを開きます。
1. 「Cloud Service」タブで、「サービスを追加」をクリックし、「動的なTag Management」を選択して、「OK」をクリックします。

   ![chlimage_1-357](assets/chlimage_1-357.png)

1. 「 Dynamic Tag Management 」ドロップダウンメニューを使用して設定を選択し、「 OK 」をクリックします。

ページの継承された設定の関連付けを上書きするには、次の手順を実行します。 上書きは、ページおよびすべてのページの子孫に影響します。

1. クラシック UI でページを開きます。
1. 「Sidekick」を使用してページのプロパティを開きます。
1. [Cloud Service] タブで、[ 継承元 ] プロパティの横にある南京錠アイコンをクリックし、確認ダイアログボックスで [ はい ] をクリックします。

   ![chlimage_1-358](assets/chlimage_1-358.png)

1. Dynamic Tag Management 設定を削除するか、別の Dynamic Tag Management 設定を選択して、「OK」をクリックします。
