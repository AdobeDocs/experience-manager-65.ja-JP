---
title: セキュリティチェックリスト
seo-title: Security Checklist
description: AEM を設定およびデプロイする際の様々なセキュリティに関する考慮事項について説明します。
seo-description: Learn about the various security considerations when configuring and deploying AEM.
uuid: 8e293316-4177-4271-87c6-9dc1a2e85a07
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: de7d7209-c194-4d19-853b-468ebf3fa4b2
docset: aem65
exl-id: 314a6409-398c-470b-8799-0c4e6f745141
feature: Security
source-git-commit: f60d3049b10a8ec500dd0cd4b1b5d4efbe415d84
workflow-type: tm+mt
source-wordcount: '2859'
ht-degree: 100%

---

# セキュリティチェックリスト {#security-checklist}

ここでは、デプロイの際に AEM インストールのセキュリティを確保するために必要となる様々な手順について説明します。このチェックリストは、上から順に適用するように設計されています。

>[!NOTE]
>
>[Open Web Application Security Project（OWASP）](https://owasp.org/www-project-top-ten/)で公開されている、最も危険性の高いセキュリティ上の脅威についても確認できます。

>[!NOTE]
>
>開発段階に適用されるその他の[セキュリティに関する考慮事項](/help/sites-developing/dev-guidelines-bestpractices.md#security-considerations)も参照してください。

## 主なセキュリティ対策 {#main-security-measures}

### 実稼動準備モードでの AEM の実行 {#run-aem-in-production-ready-mode}

詳しくは、[実稼動準備モードでの AEM の実行](/help/sites-administering/production-ready.md)を参照してください。

### トランスポート層のセキュリティのための HTTPS の有効化 {#enable-https-for-transport-layer-security}

インスタンスの安全を確保するには、オーサーインスタンスとパブリッシュインスタンスの両方の HTTPS トランスポート層を有効にする必要があります。

>[!NOTE]
>
>詳しくは、[HTTP over SSL の有効化](/help/sites-administering/ssl-by-default.md)を参照してください。

### セキュリティホットフィックスのインストール {#install-security-hotfixes}

[アドビが提供する最新のセキュリティホットフィックス](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=ja)がインストールされていることを確認してください。

### AEM および OSGi コンソールの admin アカウントのデフォルトパスワードの変更 {#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts}

インストール後に、（すべてのインスタンスに対する）権限のある [**AEM** `admin`アカウント](#changing-the-aem-admin-password)のパスワードを変更することを強くお勧めします。

以下のアカウントが該当します。

* AEM `admin` アカウント

   AEM 管理者アカウントのパスワードを変更すると、CRX へのアクセス時には新しいパスワードを使用する必要があります。

* OSGi Web コンソールの `admin` パスワード

   この変更は、web コンソールへのアクセスに使用する admin アカウントにも適用されます。そのため、web コンソールへのアクセスの際にも同じパスワードを使用する必要があります。

これらの 2 つのアカウントは、個別の資格情報を使用する異なるアカウントです。デプロイメントをセキュリティで保護するには、それぞれに強力なパスワードを設定することが不可欠です。

#### AEM admin パスワードの変更 {#changing-the-aem-admin-password}

AEM の admin アカウントのパスワードは、[Granite の操作 - ユーザー](/help/sites-administering/granite-user-group-admin.md)コンソールで変更できます。

このコンソールでは、`admin` アカウントの編集と[パスワードの変更](/help/sites-administering/granite-user-group-admin.md#changing-the-password-for-an-existing-user)を行うことができます。

>[!NOTE]
>
>admin アカウントを変更すると、OSGi Web コンソールのアカウントも変更されます。admin アカウントの変更後は、OSGi アカウントを変更してください。

#### OSGi web コンソールのパスワード変更の重要性 {#importance-of-changing-the-osgi-web-console-password}

AEM `admin` アカウントとは別に、OSGi web コンソールのデフォルトのパスワードを変更しない場合は、次の問題が発生する可能性があります。

* 起動／シャットダウン（大規模なサーバーでは数分かかる場合があります）時にデフォルトのパスワードを使用するサーバーのリスク
* リポジトリの停止／バンドルの再起動時（OSGi は実行されている場合）のサーバーのリスク

Web コンソールのパスワードの変更について詳しくは、以下の [OSGi Web コンソールの admin パスワードの変更](/help/sites-administering/security-checklist.md#changing-the-osgi-web-console-admin-password)を参照してください。

#### OSGi Web コンソールの admin パスワードの変更 {#changing-the-osgi-web-console-admin-password}

Web コンソールへのアクセスに使用するパスワードの変更も必要です。そのためには、[Apache Felix OSGi Management Console](/help/sites-deploying/osgi-configuration-settings.md) の以下のプロパティを設定します。

**User Name** および **Password**：Apache Felix Web Management Console 自体にアクセスするための認証情報です。
インスタンスのセキュリティを確保するために、初期インストール後にパスワードを変更する必要があります。

次の手順を実行します。

1. Web コンソール（`<server>:<port>/system/console/configMgr`）にアクセスします。
1. **Apache Felix OSGi Management Console** に移動して、**ユーザー名**&#x200B;と&#x200B;**パスワード**&#x200B;を変更します。

   ![chlimage_1-3](assets/chlimage_1-3.png)

1. 「**保存**」をクリックします。

### カスタムエラーハンドラーの実装 {#implement-custom-error-handler}

情報が開示されないようにするには、（404 および 500 HTTP 応答コード専用の）カスタムエラーハンドラーページを定義することをお勧めします。

>[!NOTE]
>
>詳しくは、[カスタムスクリプトまたはエラーハンドラーの作成方法](https://helpx.adobe.com/experience-manager/kb/CustomErrorHandling.html)に関するナレッジベースの記事を参照してください。

### ディスパッチャーのセキュリティチェックリストの確認 {#complete-dispatcher-security-checklist}

AEM Dispatcher はインフラストラクチャの重要な部分です。[ Dispatcher のセキュリティチェックリスト](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/security-checklist.html?lang=ja#getting-started)を確認することを強くお勧めします。

>[!CAUTION]
>
>Dispatcher を使用して「.form」セレクターを無効にする必要があります。

## 検証手順 {#verification-steps}

### レプリケーションおよびトランスポートユーザーの設定 {#configure-replication-and-transport-users}

AEM の標準インストールでは、`admin` をデフォルトの[レプリケーションエージェント](/help/sites-deploying/replication.md)内のトランスポート認証情報のユーザーとして指定します。また、admin ユーザーはオーサーシステムでレプリケーションのソースを特定する場合にも使用されます。

セキュリティを考慮して、特定の使用事例に対応するように両方のユーザーを変更してください。その際の注意事項を次に示します。

* **トランスポートユーザー**&#x200B;は管理者ユーザーにしないでください。代わりに、公開システムの関連部分へのアクセス権のみを持つユーザーを公開システムに設定し、そのユーザーの認証情報をトランスポートに使用します。

   バンドルされたレプリケーション受信者ユーザーから開始し、状況に合わせてそのユーザーのアクセス権限を設定できます。

* **レプリケーションユーザー**&#x200B;または&#x200B;**エージェントユーザー ID** も admin 以外のユーザー（ただし、レプリケーションされるコンテンツの確認のみ可能なユーザー）にする必要があります。レプリケーションユーザーは、レプリケーション対象のコンテンツを、発行者に送信する前に作成者システムで収集するために使用します。

### 操作ダッシュボードのセキュリティヘルスチェックの確認 {#check-the-operations-dashboard-security-health-checks}

AEM 6 には新しく操作ダッシュボードが導入されています。このダッシュボードは、システムオペレーターが問題のトラブルシューティングやインスタンスのヘルスの監視をおこなうためのものです。

また、このダッシュボードには一連のセキュリティヘルスチェック機能が用意されています。実稼動インスタンスの運用を開始する前に、すべてのセキュリティヘルスチェックのステータスを確認しておくことをお勧めします。詳しくは、[操作ダッシュボードのドキュメント](/help/sites-administering/operations-dashboard.md)を参照してください。

### サンプルコンテンツが存在するかどうかの確認 {#check-if-example-content-is-present}

実稼動システムを公開する前に、そのシステム上のすべてのサンプルコンテンツ／ユーザー（Geometrixx プロジェクトやそのコンポーネントなど）を完全にアンインストールして削除しておく必要があります。

>[!NOTE]
>
>このインスタンスが[実稼動準備モード](/help/sites-administering/production-ready.md)で実行されている場合、サンプルの We.Retail アプリケーションは削除されます。何らかの理由でこれが当てはまらない場合は、パッケージマネージャーに移動して、すべての We.Retail パッケージを検索してアンインストールすることで、サンプルコンテンツをアンインストールできます。詳しくは、[パッケージの操作](package-manager.md)を参照してください。

### CRX 開発バンドルが存在するかどうかの確認 {#check-if-the-crx-development-bundles-are-present}

実稼動のオーサーシステムとパブリッシュシステムへのアクセスを可能にする前に、それらの両方のシステムで、以下の開発用 OSGi バンドルをアンインストールしておく必要があります。

* Adobe CRXDE サポート（com.adobe.granite.crxde-support）
* Adobe Granite CRX Explorer（com.adobe.granite.crx-explorer）
* Adobe Granite CRXDE Lite（com.adobe.granite.crxde-lite）

### Sling 開発バンドルが存在するかどうかの確認 {#check-if-the-sling-development-bundle-is-present}

[AEM Developer Tools for Eclipse](/help/sites-developing/aem-eclipse.md) は Apache Sling Tooling Support Install（org.apache.sling.tooling.support.install）をデプロイします。

実稼動のオーサーシステムとパブリッシュシステムへのアクセスを可能にする前に、それらの両方のシステムで、この OSGi バンドルをアンインストールしておく必要があります。

### クロスサイトリクエストフォージェリからの保護 {#protect-against-cross-site-request-forgery}

#### CSRF 対策フレームワーク {#the-csrf-protection-framework}

AEM 6.1 には、クロスサイトリクエストフォージェリーから保護する **CSRF 対策フレームワーク**&#x200B;と呼ばれるメカニズムが搭載されています。使用方法について詳しくは、[ドキュメント](/help/sites-developing/csrf-protection.md)を参照してください。

#### Sling Referrer Filter {#the-sling-referrer-filter}

CRX WebDAV および Apache Sling のクロスサイトリクエストフォージェリ（CSRF）に関する既存のセキュリティ問題に対応するには、リファラーフィルターを使用するために設定を追加する必要があります。

リファラーフィルターサービスは OSGi のサービスの 1 つであり、次の設定が可能です。

* フィルター処理する HTTP メソッド
* 空のリファラーヘッダーを使用できるかどうか
* サーバーホスト以外に許可されるサーバーのリスト

   デフォルトでは、localhost のすべてのバリエーションおよびサーバーのバインド先の現在のホストの名前がリストに含まれます。

リファラーフィルターサービスを設定するには：

1. 次の場所で Apache Felix コンソール（**設定**）を開きます。

   `https://<server>:<port_number>/system/console/configMgr`

1. `admin` としてログインします。
1. **設定**&#x200B;メニューで、次の項目を選択します。

   `Apache Sling Referrer Filter`

1. 「`Allow Hosts`」フィールドに、リファラーとして許可するすべてのホストを入力します。各エントリは、

   &lt;protocol>://&lt;server>:&lt;port> の形式である必要があります。

   例：

   * `https://allowed.server:80` の場合、このサーバーからの指定ポートでの要求がすべて許可されます。
   * https 要求も許可する場合は、2 行目を入力する必要があります。
   * このサーバーからすべてのポートを許可する場合は、ポート番号として `0` を使用できます。

1. リファラーヘッダーが空の場合やない場合を許可するには、「`Allow Empty`」フィールドを選択します。

   >[!CAUTION]
   >
   >ご利用のシステムが CSRF 攻撃を受ける可能性があるため、`cURL` などのコマンドラインツールを使用する場合は、空の値を許可するのではなく、リファラーを指定することをお勧めします。

1. このフィルターが「`Filter Methods`」フィールドを使用してチェックする方法を編集します。

1. 「**保存**」をクリックして変更を保存します。

### OSGi 設定 {#osgi-settings}

一部の OSGi 設定は、アプリケーションのデバッグを容易におこなえるようにデフォルトで設定されます。実稼動のパブリッシュインスタンスとオーサーインスタンスでは、これらの設定を変更して、内部情報が公開されないようにする必要があります。

>[!NOTE]
>
>**Day CQ WCM Debug Filter** を除く以下のすべての設定は、自動的に[実稼動準備モード](/help/sites-administering/production-ready.md)の対象になります。このため、インスタンスを実稼動環境にデプロイする前にすべての設定を見直すことをお勧めします。

以下に示す各サービスについて、記載されている設定を変更してください。

* [Adobe Granite HTML Library Manager](/help/sites-deploying/osgi-configuration-settings.md#day-cq-html-library-manager)：

   * 「**Minify**」を有効化（CRLF および空白文字を削除）
   * 「**Gzip**」を有効化（1 回の要求でファイルを gzip してアクセスするため）
   * 「**Debug**」を無効化
   * 「**Timing**」を無効化

* [Day CQ WCM デバッグフィルター](/help/sites-deploying/osgi-configuration-settings.md#day-cq-wcm-debug-filter)：

   * 「**有効**」の選択を解除

* [Day CQ WCM フィルター](/help/sites-deploying/osgi-configuration-settings.md)：

   * （パブリッシュインスタンスのみ）「**WCM モード**」を「無効」に設定

* [Apache Sling Java Script Handler](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-javascript-handler):

   * 「**デバッグ情報の生成**」を無効化

* [Apache Sling JSP スクリプトハンドラー](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-jsp-script-handler)：

   * 「**デバッグ情報の生成**」を無効化
   * 「**マッピングされたコンテンツ**」を無効化

詳しくは、[OSGi 設定](/help/sites-deploying/osgi-configuration-settings.md)を参照してください。

AEM を操作しているときは、このようなサービスの設定を管理する方法がいくつかあります。詳細および推奨事項については、[OSGi の設定](/help/sites-deploying/configuring-osgi.md)を参照してください。

## 追加情報 {#further-readings}

### サービス拒否（DoS）攻撃の軽減 {#mitigate-denial-of-service-dos-attacks}

サービス拒否（DoS）攻撃は、対象となるユーザーがコンピューターリソースを使用できない状態にするものです。多くの場合、この攻撃ではリソースを過負荷状態にします。次に例を示します。

* 外部のソースから大量の要求を送信する。
* システムが正常に提供できないような大量の情報を要求される。

   例えば、リポジトリ全体の JSON 表現を要求されます。

* 無制限の個数の URL を含むコンテンツページを要求される。URL にはハンドル、何らかのセレクター、拡張子、サフィックスを含める場合があり、そのいずれかを変わる可能性があります。

   例えば、`.../en.html` は次のようにリクエストされる可能性があります。

   * `.../en.ExtensionDosAttack`
   * `.../en.SelectorDosAttack.html`
   * `.../en.html/SuffixDosAttack`

   有効なすべてのバリエーションがディスパッチャーによってキャッシュされ（例えば、`200` 応答を返し、キャッシュするように設定されている場合）、最終的にはファイルシステムがいっぱいになり、以降の要求に対してサービスを提供できなくなります。

このような攻撃を防ぐための設定のポイントは多数ありますが、ここでは AEM に直接関連する設定についてのみ説明します。

**DoS を防ぐための Sling の設定**

Sling はコンテンツ中心型です&#x200B;*。*&#x200B;つまり、（HTTP）要求がそれぞれ JCR リソース（リポジトリーノード）の形式でコンテンツにマップされるので、コンテンツに焦点を当てた処理が行われるということです。

* 最初のターゲットは、コンテンツを保持しているリソース（JCR ノード）です。。
* 次に、リソースのプロパティを要求の特定の部分（例：セレクター、拡張子など）と組み合わせてレンダラー（スクリプト）が特定されます。

>[!NOTE]
>
>詳しくは、[Sling の要求処理](/help/sites-developing/the-basics.md#sling-request-processing)を参照してください。

このアプローチにより Sling が強化され、柔軟性も向上しますが、これまでどおり柔軟性の管理には注意が必要です。

DoS の悪用を防ぐ方法は次のとおりです。

1. アプリケーションレベルで制御を組み込みます。バリエーションの数が原因で、デフォルト設定が適していない可能性があります。

   アプリケーションで必要な処理は次のとおりです。

   * アプリケーションのセレクターを制御して、必要とされる明示的なセレクター&#x200B;*のみ*&#x200B;提供し、他のすべてに対しては `404` を返します。
   * コンテンツノードの出力が無制限に大量におこなわれないようにします。

1. 問題点となっている可能性のあるデフォルトのレンダラーの設定を確認します。

   * 特に、ツリー構造が複数のレベルに及ぶ JSON レンダラーです。

      例えば、次のようなリクエストの場合、

      `http://localhost:4502/.json`

      リポジトリ全体を JSON 表現でダンプできてしまいます。これにより、サーバーで重大な問題が発生します。そのため、Sling では最大の結果数に制限を設定します。JSON レンダリングの深度を制限するには、次の値を設定できます。

      **JSON の最大結果数**（`json.maximumresults`）

      [Apache Sling GET サーブレット](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet)の設定で指定します。この制限を超えると、レンダリングが止まります。AEM 内での Sling 用のデフォルト値は `1000` です。

   * 予防策として、デフォルトの他のレンダラー（HTML、プレーンテキスト、XML）を無効にします。この場合も [Apache Sling GET Servlet](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet) を設定します。
   >[!CAUTION]
   >
   >JSON レンダラーを無効にしないでください。これは AEM の通常処理に必要なレンダラーです。

1. ファイアウォールを使用してインスタンスへのアクセスをフィルタリングします。

   * 保護のない状態ではサービス拒否攻撃を受ける恐れがあるので、オペレーティングシステムレベルのファイアウォールを使用してインスタンスへのアクセスをフィルタリングする必要があります。

**フォームセレクターを使用することで生じる DoS に対する軽減策**

>[!NOTE]
>
>この軽減策は、Forms を使用していない AEM 環境でのみ実行してください。

AEM は `FormChooserServlet` 用の標準インデックスを提供していないため、クエリでフォームセレクターを使用すると、高コストのリポジトリトラバーサルが発生し、大抵の場合 AEM インスタンスが停止します。フォームセレクターは、クエリに文字列 **&amp;ast;.form.&amp;ast;** が含まれていれば検出されてしまいます。

これを軽減するには、次の手順に従ってください。

1. ブラウザーで *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr* を参照して、web コンソールに移動します

1. **Day CQ WCM Form Chooser Servlet** を検索します。
1. エントリをクリックした後、次のウィンドウで「**Advanced Search Require**」を無効にします。

1. 「**保存**」をクリックします。

**アセットダウンロードサーブレット使用することで生じる DoS を軽減**

デフォルトのアセットダウンロードサーブレットを使用すると、認証済みユーザーは、アセットの ZIP ファイルを作成するよう、任意の大きさの同時ダウンロード要求を発行できます。大きな ZIP アーカイブを作成すると、サーバーとネットワークが過負荷になる可能性があります。この動作に起因する潜在的なサービス拒否（DoS）のリスクを軽減するために、[!DNL Experience Manager] パブリッシュインスタンスでは `AssetDownloadServlet` OSGi コンポーネントがデフォルトで無効になっています。これは、[!DNL Experience Manager] オーサーインスタンスでデフォルトで有効になっています。

ダウンロード機能が必要ない場合は、オーサーデプロイメントとパブリッシュデプロイメントでサーブレットを無効にします。セットアップでアセットダウンロードサーブレットを有効にする必要がある場合、詳細については[この記事](/help/assets/download-assets-from-aem.md)を参照してください。また、デプロイメントでサポートできるダウンロードの最大制限を定義できます。

### WebDAV の無効化 {#disable-webdav}

WebDAV は、オーサリングとパブリッシュの両方の環境で無効にする必要があります。そのためには、適切な OSGi バンドルを停止します。

1. **Felix Management Console** に接続します。

   `https://<*host*>:<*port*>/system/console`

   例えば、`http://localhost:4503/system/console/bundles` です。

1. バンドルのリストで、次の名前のバンドルを探します。

   `Apache Sling Simple WebDAV Access to repositories (org.apache.sling.jcr.webdav)`

1. （「アクション」列にある）停止ボタンをクリックして、このバンドルを停止します。

1. 再び、バンドルのリストで、次の名前のバンドルを探します。

   `Apache Sling DavEx Access to repositories (org.apache.sling.jcr.davex)`

1. 停止ボタンをクリックして、このバンドルを停止します。

   >[!NOTE]
   >
   >AEM の再起動は不要です。

### ユーザーのホームパスに個人を特定できる情報を公開していないことの確認 {#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path}

ユーザーの保護に重要なのは、リポジトリユーザーのホームパスに個人を特定できる情報を公開しないことです。

AEM 6.1 以降では、新しく実装された `AuthorizableNodeName` インターフェイスにより、ユーザー ID（または認証可能な ID）のノード名を保存する方法が変わりました。新しいインターフェイスでは、ノード名にユーザー ID を表示する代わりに、ランダムな名前を生成します。

これは現在は AEM で許可可能 ID を生成するデフォルトの方法なので、これを有効にするために設定を変更する必要はありません。

既存のアプリケーションとの後方互換性を確保するために以前の実装が必要な場合、非推奨ではありますが、この機能を無効にすることもできます。これを行うには、次の手順を実行する必要があります。

1. Web コンソールに移動して、**Apache Jackrabbit Oak SecurityProvider** のプロパティ **requiredServicePids** から org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName エントリを削除します。

   また、OSGi 設定の **org.apache.jackrabbit.oak.security.internal.SecurityProviderRegistration** PID を探すことで、Oak Security Provider を見つけることもできます。

1. Web コンソールから **Apache Jackrabbit Oak Random Authorizable Node Name** OSGi 設定を削除します。

   この設定の PID である **org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName** を検索すると、簡単に該当箇所が見つかります。

>[!NOTE]
>
>詳しくは、「Oak Documentation」の[Authorizable Node Name Generation（英語）](https://jackrabbit.apache.org/oak/docs/security/user/authorizablenodename.html)を参照してください。

### クリックジャッキングの防止 {#prevent-clickjacking}

クリックジャッキングを防ぐには、`SAMEORIGIN` に設定した HTTP ヘッダー `X-FRAME-OPTIONS` を指定するように web サーバーを設定することをお勧めします。

クリックジャッキングについて詳しくは、[OWASP のサイト](https://www.owasp.org/index.php/Clickjacking)を参照してください。

### 必要な場合は暗号鍵を適切にレプリケーションする {#make-sure-you-properly-replicate-encryption-keys-when-needed}

特定の AEM 機能および認証スキームでは、すべての AEM インスタンスに暗号鍵をレプリケーションする必要があります。

これをおこなう前に、6.3 とそれ以前のバージョンでは鍵を保存する方法が異なるので、鍵のレプリケーションはバージョン間で異なることに注意してください。

詳しくは、以下を参照してください。

#### AEM 6.3 での鍵のレプリケーション {#replicating-keys-for-aem}

以前のバージョンではレプリケーション鍵はリポジトリに保存されましたが、AEM 6.3 からはファイルシステム上に保存されます。

したがって、インスタンス間で鍵をレプリケーションするには、ソースインスタンスからターゲットインスタンスのファイルシステム上の場所に鍵をコピーする必要があります。

具体的には、以下をおこなう必要があります。

1. コピーする鍵要素を含む AEM インスタンス（通常はオーサーインスタンス）にアクセスします。
1. ローカルファイルシステム内で、com.adobe.granite.crypto.file を見つけます。例えば、次のパスにあります。

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`

   各フォルダー内の `bundle.info` ファイルは、バンドル名を示します。 

1. データフォルダーに移動します。次に例を示します。

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. HMAC とマスターファイルをコピーします。
1. 次に、HMAC 鍵の複製先となるターゲットインスタンスにアクセスし、データフォルダーに移動します。次に例を示します。

   * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. 前の手順でコピーした 2 つのファイルを貼り付けます。
1. ターゲットインスタンスが既に実行されている場合は、[Crypto バンドルを更新](/help/communities/deploy-communities.md#refresh-the-granite-crypto-bundle)します。
1. 鍵のレプリケーション先のすべてのインスタンスに対して上記の手順を繰り返します。

>[!NOTE]
>
>最初に AEM をインストールするときに次のパラメーターを追加することによって、6.3 よりも前の鍵の保存方法に戻すことができます。
>
>`-Dcom.adobe.granite.crypto.file.disable=true`

#### AEM 6.2 以前のバージョンでの鍵のレプリケーション {#replicating-keys-for-aem-and-older-versions}

AEM 6.2 以前のバージョンでは、鍵は `/etc/key` ノードの下のリポジトリに保存されます。

インスタンス全体で鍵を安全にレプリケーションするために推奨される方法は、このノードのみをレプリケーションすることです。CRXDE Lite によって、ノードを選択してレプリケーションできます。

1. *https://&lt;serrveraddress>:4502/crx/de/index.jsp* に移動して CRXDE Lite を開きます。
1. `/etc/key` ノードを選択します。
1. 「**レプリケーション**」タブに移動します。
1. 「**レプリケーション**」ボタンを押します。

### 侵入テストの実施 {#perform-a-penetration-test}

実稼動に移行する前に、AEM インフラストラクチャの侵入テストを実施することを強くお勧めします。

### 開発のベストプラクティス {#development-best-practices}

AEM 環境の安全を確保するには、新規開発において[セキュリティのベストプラクティス](/help/sites-developing/security.md)に従うことが重要です。
