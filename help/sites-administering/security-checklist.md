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
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '3004'
ht-degree: 98%

---

# セキュリティチェックリスト {#security-checklist}

このセクションでは、デプロイ時に AEM のインストールが安全になるようにするために必要な様々な手順について説明します。このチェックリストは、上から順に適用するように設計されています。

>[!NOTE]
>
>[Open Web Application Security Project（OWASP）](https://owasp.org/www-project-top-ten/)で公開されている、最も危険性の高いセキュリティ上の脅威についても確認できます。

>[!NOTE]
>
>開発段階に適用されるその他の[セキュリティに関する考慮事項](/help/sites-developing/dev-guidelines-bestpractices.md#security-considerations)も参照してください。

## 主なセキュリティ対策 {#main-security-measures}

### 実稼動準備モードでの AEM の実行 {#run-aem-in-production-ready-mode}

詳しくは、「[実稼動準備モードでの AEM の実行](/help/sites-administering/production-ready.md)」を参照してください。

### トランスポート層のセキュリティのための HTTPS の有効化 {#enable-https-for-transport-layer-security}

インスタンスの安全を確保するには、オーサーインスタンスとパブリッシュインスタンスの両方の HTTPS トランスポート層を有効にする必要があります。

>[!NOTE]
>
>詳しくは、[HTTP over SSL の有効化](/help/sites-administering/ssl-by-default.md)を参照してください。

### セキュリティホットフィックスのインストール {#install-security-hotfixes}

最新の[アドビ提供のセキュリティホットフィックス](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=ja)がインストールされていることを確認してください。

### AEM および OSGi コンソールの管理者アカウントのデフォルトパスワードの変更 {#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts}

インストール後に、（すべてのインスタンスに対する）権限のある [**AEM** `admin`アカウント](#changing-the-aem-admin-password)のパスワードを変更することをお勧めします。

以下のアカウントが該当します。

* AEM `admin` アカウント

  AEM 管理者アカウントのパスワードを変更した後、CRX へのアクセス時には新しいパスワードを使用します。

* OSGi web コンソールの `admin` パスワード

  この変更は、web コンソールへのアクセスに使用する admin アカウントにも適用されます。そのため、web コンソールへのアクセスの際にも同じパスワードを使用します。

これらの 2 つのアカウントは、個別の資格情報を使用する異なるアカウントです。デプロイメントをセキュリティで保護するには、それぞれに強力なパスワードを設定することが不可欠です。

#### AEM admin パスワードの変更 {#changing-the-aem-admin-password}

AEM 管理者アカウントのパスワードは、[Granite の操作 - ユーザー](/help/sites-administering/granite-user-group-admin.md)コンソールで変更できます。

このコンソールでは、`admin` アカウントの編集と[パスワードの変更](/help/sites-administering/granite-user-group-admin.md#changing-the-password-for-an-existing-user)を行うことができます。

>[!NOTE]
>
>管理者アカウントを変更すると、OSGi web コンソールのアカウントも変更されます。管理者アカウントを変更したら、OSGi アカウントを別のアカウントに変更する必要があります。

#### OSGi web コンソールのパスワード変更の重要性 {#importance-of-changing-the-osgi-web-console-password}

AEM `admin` アカウントとは別に、OSGi web コンソールのデフォルトのパスワードを変更しない場合は、次の問題が発生する可能性があります。

* 起動時およびシャットダウン時にデフォルトのパスワードでサーバーが公開される（大規模なサーバーの場合は数分かかる場合があります）
* リポジトリがダウンまたはバンドルを再起動中で、OSGI を実行中に、サーバーが公開される

Web コンソールのパスワードの変更について詳しくは、「[OSGi web コンソールの管理者パスワードの変更](/help/sites-administering/security-checklist.md#changing-the-osgi-web-console-admin-password)」を参照してください。

#### OSGi web コンソールの管理者パスワードの変更 {#changing-the-osgi-web-console-admin-password}

Web コンソールへのアクセスに使用するパスワードを変更します。[OSGi 設定](/help/sites-deploying/configuring-osgi.md)を使用して、**Apache Felix OSGi 管理コンソール**&#x200B;の以下のプロパティを更新します。

* **ユーザー名**&#x200B;と&#x200B;**パスワード**：Apache Felix web 管理コンソールにアクセスするための資格情報です。
インスタンスのセキュリティを確保するには、最初のインストールの*後に*&#x200B;パスワードを変更する必要があります。

>[!NOTE]
>
>OSGi 設定について詳しくは、「[OSGi 設定](/help/sites-deploying/configuring-osgi.md)」を参照してください。

**OSGi web コンソールの admin パスワードの変更**：

1. **ツール**／**操作**&#x200B;メニューから、**Web コンソール**&#x200B;を開き、「**設定**」セクションに移動力します。
例：`<server>:<port>/system/console/configMgr`
1. **Apache Felix OSGi 管理コンソール**&#x200B;に移動してエントリを開きます。
1. **ユーザー名**&#x200B;および **パスワード**&#x200B;を変更します。

   ![chlimage_1-3](assets/chlimage_1-3.png)

1. 「**保存**」を選択します。

### カスタムエラーハンドラーの実装 {#implement-custom-error-handler}

情報が開示されないようにするには、（404 および 500 HTTP 応答コード専用の）カスタムエラーハンドラーページを定義することをお勧めします。

>[!NOTE]
>
>詳しくは、[カスタムスクリプトまたはエラーハンドラーの作成方法](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/full-stack/custom-error-page.html?lang=ja)を参照してください。

### Dispatcher のセキュリティチェックリストの完了 {#complete-dispatcher-security-checklist}

AEM Dispatcher はインフラストラクチャの重要な部分です。[Dispatcher のセキュリティチェックリスト](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/security-checklist.html?lang=ja)を確認することをお勧めします。

>[!CAUTION]
>
>Dispatcher を使用する場合は、「.form」セレクターを無効にする必要があります。

## 検証手順 {#verification-steps}

### レプリケーションの設定とユーザーのトランスポート {#configure-replication-and-transport-users}

AEM の標準インストールでは、`admin` をデフォルトの[レプリケーションエージェント](/help/sites-deploying/replication.md)内のトランスポート資格情報のユーザーとして指定します。また、管理者ユーザーは、オーサーシステムでレプリケーションを展開する際に使用します。

セキュリティに関する考慮事項については、次の 2 つの点を考慮して、特定の使用例がすぐに反映されるように両方を変更する必要があります。

* **トランスポートユーザー**&#x200B;は admin 以外のユーザーにする必要があります。正確には、パブリッシュシステムの関連部分へのアクセス権限のみを持つユーザーをパブリッシュシステムで設定し、そのユーザーの資格情報をトランスポートに使用してください。

  バンドルされたレプリケーション受信者ユーザーから開始し、状況に合わせてそのユーザーのアクセス権限を設定できます。

* **レプリケーションユーザー**&#x200B;または&#x200B;**エージェントユーザー ID** も admin 以外のユーザー（ただし、レプリケーションされるコンテンツの確認のみ可能なユーザー）にする必要があります。レプリケーションユーザーは、レプリケーション対象のコンテンツを、パブリッシュに送信する前にオーサーシステムで収集するために使用します。

### 操作ダッシュボードのセキュリティヘルスチェックの確認 {#check-the-operations-dashboard-security-health-checks}

AEM 6 には、システムオペレーターが問題のトラブルシューティングやインスタンスの正常性の監視を行うための新しい操作ダッシュボードが導入されました。

このダッシュボードには、セキュリティヘルスチェックのコレクションも付属しています。実稼動インスタンスでの運用を開始する前に、すべてのセキュリティヘルスチェックのステータスを確認することをお勧めします。詳しくは、[操作ダッシュボードのドキュメント](/help/sites-administering/operations-dashboard.md)を参照してください。

### サンプルコンテンツが存在するかどうかを確認 {#check-if-example-content-is-present}

実稼動システムを公開する前に、そのシステム上のすべてのサンプルコンテンツ／ユーザー（Geometrixx プロジェクトやそのコンポーネントなど）を完全にアンインストールして削除しておく必要があります。

>[!NOTE]
>
>このインスタンスが[実稼動準備モード](/help/sites-administering/production-ready.md)で実行されている場合、サンプルの `We.Retail` アプリケーションは削除されます。このシナリオが当てはまらない場合は、パッケージマネージャーに移動して、すべての `We.Retail` パッケージを検索してアンインストールすることで、サンプルコンテンツをアンインストールできます。

[パッケージの操作](package-manager.md)を参照してください。

### CRX 開発バンドルが存在するかどうかの確認 {#check-if-the-crx-development-bundles-are-present}

これらの開発用 OSGi バンドルは、アクセスできるようにする前に、オーサーとパブリッシュの両方の実稼働システムからアンインストールする必要があります。

* Adobe CRXDE サポート（com.adobe.granite.crxde-support）
* Adobe Granite CRX Explorer（com.adobe.granite.crx-explorer）
* Adobe Granite CRXDE Lite（com.adobe.granite.crxde-lite）

### Sling 開発バンドルが存在するかどうかの確認 {#check-if-the-sling-development-bundle-is-present}

[AEM Developer Tools](/help/sites-developing/aem-eclipse.md) は Apache Sling Tooling Support Install（org.apache.sling.tooling.support.install）をデプロイします。

この OSGi バンドルは、アクセスできるようにする前に、オーサーとパブリッシュの両方の実稼働システムからアンインストールする必要があります。

### クロスサイトリクエストフォージェリーからの保護 {#protect-against-cross-site-request-forgery}

#### CSRF 対策フレームワーク {#the-csrf-protection-framework}

AEM 6.1 には、クロスサイトリクエストフォージェリーから保護する **CSRF 対策フレームワーク**&#x200B;と呼ばれるメカニズムが搭載されています。使用方法について詳しくは、[ドキュメント](/help/sites-developing/csrf-protection.md)を参照してください。

#### Sling リファラーフィルター {#the-sling-referrer-filter}

CRX WebDAV および Apache Sling のクロスサイトリクエストフォージェリ（CSRF）に関する既存のセキュリティ問題に対応するには、リファラーフィルターを使用するために設定を追加します。

リファラーフィルターサービスは OSGi のサービスの 1 つであり、次の設定が可能です。

* どの http メソッドをフィルターするか
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

アプリケーションのデバッグを容易にするために、一部の OSGi 設定はデフォルトで指定されています。実稼動のパブリッシュインスタンスとオーサーインスタンスでは、これらの設定を変更して、内部情報が公開されないようにします。

>[!NOTE]
>
>以下の設定はすべて（**Day CQ WCM デバッグフィルター**&#x200B;は除く）、[実稼動準備モード](/help/sites-administering/production-ready.md)で自動的にカバーされます。このため、インスタンスを実稼働環境にデプロイする前にすべての設定を見直すことをお勧めします。

以下に示す各サービスについて、記載されている設定を変更してください。

* [Adobe Granite HTML Library Manager](/help/sites-deploying/osgi-configuration-settings.md#day-cq-html-library-manager):

   * 「**縮小**」を有効にして CRLF 文字と空白文字を削除する
   * 「**Gzip**」を有効にして、1 回のリクエストでファイルを gzip で圧縮してアクセスできるようにする。
   * 「**デバッグ**」を無効にする
   * 「**タイミング**」を無効にする

* [Day CQ WCM デバッグフィルター](/help/sites-deploying/osgi-configuration-settings.md#day-cq-wcm-debug-filter)：

   * 「**有効**」の選択を解除

* [Day CQ WCM フィルター](/help/sites-deploying/osgi-configuration-settings.md)：

   * （パブリッシュインスタンスのみ）「**WCM モード**」を「無効」に設定

* [Apache Sling JavaScript ハンドラー](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-javascript-handler)：

   * 「**デバッグ情報の生成**」を無効化

* [Apache Sling JSP スクリプトハンドラー](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-jsp-script-handler)：

   * 「**デバッグ情報の生成**」を無効化
   * 「**マッピングされたコンテンツ**」を無効化

[OSGi 設定](/help/sites-deploying/osgi-configuration-settings.md)を参照してください。

AEM を操作しているときは、このようなサービスの設定を管理する方法がいくつかあります。詳細および推奨事項については、[OSGi の設定](/help/sites-deploying/configuring-osgi.md)を参照してください。

## 参考情報 {#further-readings}

### サービス拒否（DoS）攻撃の軽減 {#mitigate-denial-of-service-dos-attacks}

サービス拒否（DoS）攻撃とは、意図したユーザーがコンピュータリソースを利用できない状態にする試みです。多くの場合、この攻撃ではリソースを過負荷状態にします。次に例を示します。

* 外部のソースから大量のリクエストを送信する。
* システムが正常に提供できないような大量の情報をリクエストされる。

  例えば、リポジトリ全体の JSON 表現を要求されます。

* 無制限の個数の URL を含むコンテンツページを要求される。URL にはハンドル、何らかのセレクター、拡張子、サフィックスを含める場合があり、そのいずれかを変わる可能性があります。

  例えば、`.../en.html` は次のようにリクエストされる可能性があります。

   * `.../en.ExtensionDosAttack`
   * `.../en.SelectorDosAttack.html`
   * `.../en.html/SuffixDosAttack`

  有効なすべてのバリエーションが Dispatcher によってキャッシュされ（例えば、`200` 応答を返し、キャッシュするように設定されている場合）、最終的にはファイルシステムがいっぱいになり、以降のリクエストに対してサービスを提供できなくなります。

このような攻撃を防ぐための設定のポイントは多数ありますが、ここでは AEM に関連するポイントについてのみ説明します。

**DoS を防ぐための Sling の設定**

Sling は&#x200B;*コンテンツ中心型*&#x200B;です。（HTTP）リクエストがそれぞれ JCR リソース（リポジトリノード）の形式でコンテンツにマッピングされるので、コンテンツに焦点を当てた処理が行われます。

* 最初のターゲットは、コンテンツを保持しているリソース（JCR ノード）です。
* 次に、レンダラーまたはスクリプトが、リクエストの特定の部分（セレクターや拡張子など）と共にリソースプロパティから配置されます。

詳しくは、[Sling のリクエスト処理](/help/sites-developing/the-basics.md#sling-request-processing)を参照してください。

このアプローチにより Sling が強化され、柔軟性も向上しますが、これまでどおり柔軟性の管理には注意が必要です。

DoS の誤用を防ぐには、以下を行います。

1. アプリケーションレベルで制御を組み込みます。可能なバリエーションの数が原因で、デフォルト設定が実現可能でない場合があります。

   アプリケーションでは、次の操作を実行する必要があります。

   * アプリケーションのセレクターを制御して、必要とされる明示的なセレクター&#x200B;*のみ*&#x200B;提供し、他のすべてに対しては `404` を返します。
   * コンテンツノードを無制限に出力できないようにします。

1. 問題となる可能性のある、デフォルトのレンダラー設定を確認します。

   * 特に、JSON レンダラーでは、ツリー構造が複数のレベルに及びます。

     例えば、次のようなリクエストの場合、

     `http://localhost:4502/.json`

     リポジトリ全体を JSON 表現でダンプできてしまうので、サーバーの重大な問題を引き起こすおそれがあります。そのため、Sling では結果の数に上限を設定しています。JSON レンダリングの深度を制限するには、次の値を設定します。

     **JSON の最大結果数**（`json.maximumresults`）

     [Apache Sling GET サーブレット](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet)の設定で指定します。この制限を超えると、レンダリングが停止します。AEM 内での Sling 用のデフォルト値は `1000` です。

   * 予防策として、他のデフォルトレンダラー（HTML、プレーンテキスト、XML）を無効にしてください。ここでも、[Apache Sling GET サーブレット](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet)を設定します。

   >[!CAUTION]
   >
   >JSON レンダラーは AEM の通常操作に必要なので、無効にしないでください。

1. ファイアウォールを使用して、インスタンスへのアクセスをフィルタリングします。

   * 保護されていない状態ではサービス拒否攻撃につながるおそれがあるインスタンスポイントへのアクセスをフィルタリングするには、オペレーティングシステムレベルのファイアウォールを使用する必要があります。

**フォームセレクターを使用することで生じる DoS に対する軽減策**

>[!NOTE]
>
>この軽減策は、Forms を使用していない AEM 環境でのみ実行してください。

AEM は `FormChooserServlet` 用の標準インデックスを提供していないので、クエリでフォームセレクターを使用すると、コストの高いリポジトリトラバーサルが発生する可能性があり、通常は AEM インスタンスが過負荷になって最終的に停止します。フォームセレクターは、クエリに文字列 **&amp;ast;.form.&amp;ast;** が含まれていれば検出されてしまいます。

この問題を軽減するには、次の手順を実行することができます。

1. ブラウザーで *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr* を参照して、web コンソールに移動します

1. **Day CQ WCM Form 選択サーブレット**&#x200B;を検索します
1. エントリをクリックした後、次のウィンドウで「**詳細検索が必要**」を無効にします。

1. 「**保存**」をクリックします。

**アセットダウンロードサーブレットによって発生する DoS を軽減**

デフォルトのアセットダウンロードサーブレットを使用すると、認証済みユーザーは、任意の大きさの同時ダウンロードリクエストを発行してアセットの ZIP ファイルを作成することができます。大きな ZIP アーカイブを作成すると、サーバーとネットワークが過負荷になる可能性があります。この動作に起因する潜在的なサービス拒否（DoS）のリスクを軽減するために、[!DNL Experience Manager] パブリッシュインスタンスでは `AssetDownloadServlet` OSGi コンポーネントがデフォルトで無効になっています。これは、[!DNL Experience Manager] オーサーインスタンスでデフォルトで有効になっています。

ダウンロード機能が必要ない場合は、オーサーデプロイメントとパブリッシュデプロイメントでこのサーブレットを無効にします。セットアップでアセットダウンロードサーブレットを有効にする必要がある場合、詳細については[この記事](/help/assets/download-assets-from-aem.md)を参照してください。また、デプロイメントでサポートできるダウンロードの最大制限を定義できます。

### WebDAV の無効化 {#disable-webdav}

該当する OSGi バンドルを停止して、オーサー環境とパブリッシュ環境の両方で WebDAV を無効にします。

1. 以下で動作している **Felix 管理コンソール**&#x200B;に接続します。

   `https://<*host*>:<*port*>/system/console`

   例：`http://localhost:4503/system/console/bundles`

1. バンドルのリストで、次の名前のバンドルを探します。

   `Apache Sling Simple WebDAV Access to repositories (org.apache.sling.jcr.webdav)`

1. このバンドルを停止するには、「アクション」列で停止ボタンをクリックします。

1. 再び、バンドルのリストで、次の名前のバンドルを探します。

   `Apache Sling DavEx Access to repositories (org.apache.sling.jcr.davex)`

1. このバンドルを停止するには、停止ボタンをクリックします。

   >[!NOTE]
   >
   >AEM の再起動は不要です。

### ユーザーのホームパスに個人を特定できる情報を公開していないことの確認 {#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path}

個人を特定できる情報をリポジトリユーザーのホームパスで公開しないようにして、ユーザーを保護することが重要です。

AEM 6.1 以降、`AuthorizableNodeName` インターフェイスの新しい実装により、ユーザー ID（認証可能な ID）のノード名の保存方法が変わりました。新しいインターフェイスでは、ノード名にユーザー ID を表示しなくなり、代わりにランダムな名前を生成します。

これは現在、AEM で認証可能な ID を生成するデフォルトの方法となっているので、これを有効にするための設定は必要ありません。

お勧めはしませんが、既存のアプリケーションとの下位互換性を確保するために古い実装が必要な場合には、この方法を無効にすることができます。それには、以下を行う必要があります。

1. Web コンソールに移動して、**Apache Jackrabbit Oak SecurityProvider** のプロパティ **requiredServicePids** から org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName エントリを削除します。

   また、OSGi 設定の **org.apache.jackrabbit.oak.security.internal.SecurityProviderRegistration** PID を探すことで、Oak Security Provider を見つけることもできます。

1. Web コンソールから **Apache Jackrabbit Oak Random Authorizable Node Name** OSGi 設定を削除します。

   ちなみに、この設定の PID は **org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName** です。該当する設定を見つける際の参考にしてください。

>[!NOTE]
>
>詳しくは、Oak ドキュメントの [Authorizable Node Name Generation](https://jackrabbit.apache.org/oak/docs/security/user/authorizablenodename.html)（英語）を参照してください。

### 匿名権限堅牢化パッケージ {#anonymous-permission-hardening-package}

デフォルトでは、AEM は、`jcr:createdBy` や `jcr:lastModifiedBy` などのシステムメタデータをノードプロパティとして、リポジトリ内の通常のコンテンツの隣に保存します。設定とアクセス制御の設定に応じて、場合によっては、これによって、例えば、生の JSON または XML としてレンダリングされる場合などに、個人識別情報 (PII) が公開される可能性があります。

すべてのリポジトリデータと同様に、これらのプロパティは Oak 認証スタックによって仲介されます。権限の最小化の原則に従って、これらのプロパティへのアクセスを制限する必要があります。

これをサポートするため、アドビでは、お客様の構築基盤として権限堅牢化パッケージを提供しています。これは、リポジトリルートに「拒否」アクセス制御エントリをインストールし、一般的に使用されるシステムプロパティへの匿名アクセスを制限することで機能します。このパッケージは[こちら](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/jp/details.html/content/dam/aem/public/adobe/packages/helper/anonymous-permissions-pkg-0.1.2.zip)からダウンロードでき、サポートされているすべてのバージョンの AEM にインストールできます。

変更点を説明するために、パッケージをインストールする前に匿名で表示できる次のノードプロパティと、

![パッケージのインストール前](/help/sites-administering/assets/before_resized.png)

パッケージのインストール後に表示可能な次のノードプロパティを比較できます。ここでは、`jcr:createdBy` と `jcr:lastModifiedBy` は表示されません。

![パッケージのインストール後](/help/sites-administering/assets/after_resized.png)

詳しくは、パッケージのリリースノートを参照してください。

### クリックジャッキングの防止 {#prevent-clickjacking}

クリックジャッキングを防ぐには、`X-FRAME-OPTIONS` に設定した HTTP ヘッダー `SAMEORIGIN` を指定するように web サーバーを設定することをお勧めします。

クリックジャッキングについて詳しくは、[OWASP のサイト](https://www.owasp.org/index.php/Clickjacking)を参照してください。

### 必要に応じて暗号化キーの適切なレプリケートを確認 {#make-sure-you-properly-replicate-encryption-keys-when-needed}

特定の AEM 機能および認証スキームでは、すべての AEM インスタンスに暗号化キーをレプリケートする必要があります。

これを行う前に、6.3 とそれ以前のバージョンでは鍵を保存する方法が異なるので、鍵のレプリケーションはバージョン間で異なる方法で行われます。

詳しくは以下を参照してください。

#### AEM 6.3 用のキーのレプリケート {#replicating-keys-for-aem}

以前のバージョンではレプリケーションキーがリポジトリに保存されていましたが、AEM 6.3 以降はファイルシステムに保存されます。

したがって、インスタンス間で鍵をレプリケーションするには、ソースインスタンスからターゲットインスタンスのファイルシステム上の場所に鍵をコピーします。

具体的には、次の手順を実行する必要があります。

1. コピーする鍵データが含まれている AEM インスタンス（通常はオーサーインスタンス）にアクセスします。
1. ローカルファイルシステム内で、com.adobe.granite.crypto.file を見つけます。例えば、次のパスにあります。

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`

   各フォルダー内の `bundle.info` ファイルは、バンドル名を示します。

1. データフォルダーに移動します。例：

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. HMAC ファイルとマスターファイルをコピーします。
1. 次に、HMAC キーの複製先のターゲットインスタンスに移動し、データフォルダーにアクセスします。例：

   * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. 前の手順でコピーした 2 つのファイルを貼り付けます。
1. ターゲットインスタンスが既に実行されている場合は、[Crypto バンドルを更新](/help/communities/deploy-communities.md#refresh-the-granite-crypto-bundle)します。
1. 鍵のレプリケーション先のすべてのインスタンスに対して上記の手順を繰り返します。

#### AEM 6.2 以前のバージョンでの鍵のレプリケーション {#replicating-keys-for-aem-and-older-versions}

AEM 6.2 以前のバージョンでは、鍵は `/etc/key` ノードの下のリポジトリに保存されます。

インスタンス間でキーを安全にレプリケートするには、このノードのみをレプリケートすることをお勧めします。ノードを選択してレプリケートするには、次の CRXDE Lite を使用します。

1. *`https://&lt;serveraddress&gt;:4502/crx/de/index.jsp`* に移動して CRXDE Lite を開きます
1. `/etc/key` ノードを選択します。
1. 「**レプリケーション**」タブに移動します。
1. 「**レプリケーション**」ボタンをクリックします。

### 侵入テストの実施 {#perform-a-penetration-test}

実稼動に移行する前に、AEM インフラストラクチャの侵入テストを実施することをお勧めします。

### 開発のベストプラクティス {#development-best-practices}

AEM 環境の安全を確保するには、新規開発において[セキュリティのベストプラクティス](/help/sites-developing/security.md)に従うことが重要です。
