---
title: セキュリティチェックリスト
seo-title: Security Checklist
description: AEMを設定およびデプロイする際の様々なセキュリティに関する考慮事項について説明します。
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
source-git-commit: f23adcf200b625e2ab2a766460c41fd7e38fae83
workflow-type: tm+mt
source-wordcount: '2986'
ht-degree: 28%

---

# セキュリティチェックリスト {#security-checklist}

この節では、デプロイ時にAEMのインストールが安全になるようにするために必要な様々な手順について説明します。 このチェックリストは、上から順に適用するように設計されています。

>[!NOTE]
>
>[Open Web Application Security Project（OWASP）](https://owasp.org/www-project-top-ten/)で公開されている、最も危険性の高いセキュリティ上の脅威についても確認できます。

>[!NOTE]
>
>開発段階に適用されるその他の[セキュリティに関する考慮事項](/help/sites-developing/dev-guidelines-bestpractices.md#security-considerations)も参照してください。

## 主なセキュリティ対策 {#main-security-measures}

### 実稼動準備モードでAEMを実行 {#run-aem-in-production-ready-mode}

詳しくは、 [実稼動準備モードでのAEMの実行](/help/sites-administering/production-ready.md).

### トランスポート層のセキュリティのための HTTPS の有効化 {#enable-https-for-transport-layer-security}

インスタンスの安全を確保するには、オーサーインスタンスとパブリッシュインスタンスの両方の HTTPS トランスポート層を有効にする必要があります。

>[!NOTE]
>
>詳しくは、[HTTP over SSL の有効化](/help/sites-administering/ssl-by-default.md)を参照してください。

### セキュリティホットフィックスのインストール {#install-security-hotfixes}

最新の [Adobeが提供するセキュリティホットフィックス](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=ja).

### AEMおよび OSGi コンソールの Admin アカウントのデフォルトパスワードの変更 {#change-default-passwords-for-the-aem-and-osgi-console-admin-accounts}

Adobeでは、インストール後に、権限を持つ [**AEM** `admin` アカウント](#changing-the-aem-admin-password) （すべてのインスタンス）。

以下のアカウントが該当します。

* AEM `admin` アカウント

   AEM admin アカウントのパスワードを変更した後、CRX にアクセスする際に新しいパスワードを使用します。

* OSGi Web コンソールの `admin` パスワード

   この変更は、Web コンソールへのアクセスに使用する管理者アカウントにも適用されるので、アクセス時には同じパスワードを使用します。

これらの 2 つのアカウントは、個別の資格情報を使用する異なるアカウントです。デプロイメントをセキュリティで保護するには、それぞれに強力なパスワードを設定することが不可欠です。

#### AEM admin パスワードの変更 {#changing-the-aem-admin-password}

AEM admin アカウントのパスワードは、 [Granite の操作 — ユーザー](/help/sites-administering/granite-user-group-admin.md) コンソール。

このコンソールでは、`admin` アカウントの編集と[パスワードの変更](/help/sites-administering/granite-user-group-admin.md#changing-the-password-for-an-existing-user)を行うことができます。

>[!NOTE]
>
>admin アカウントを変更すると、OSGi Web コンソールのアカウントも変更されます。 admin アカウントを変更した後、OSGi アカウントを別のアカウントに変更する必要があります。

#### OSGi web コンソールのパスワード変更の重要性 {#importance-of-changing-the-osgi-web-console-password}

AEM `admin` アカウントとは別に、OSGi web コンソールのデフォルトのパスワードを変更しない場合は、次の問題が発生する可能性があります。

* 起動時およびシャットダウン時にデフォルトのパスワードでサーバーを公開（大規模なサーバーの場合は数分かかる場合があります）
* リポジトリがダウン/再起動中のバンドルで、OSGI が実行中の場合のサーバーの公開。

Web コンソールのパスワードの変更について詳しくは、 [OSGi Web コンソールの管理者パスワードの変更](/help/sites-administering/security-checklist.md#changing-the-osgi-web-console-admin-password) 下

#### OSGi Web コンソールの管理者パスワードの変更 {#changing-the-osgi-web-console-admin-password}

Web コンソールへのアクセスに使用するパスワードを変更します。 を使用します。 [OSGi 設定](/help/sites-deploying/configuring-osgi.md) 次のプロパティを更新するには、 **Apache Felix OSGi Management Console**:

* **ユーザー名**&#x200B;と&#x200B;**パスワード**：Apache Felix web 管理コンソールにアクセスするための資格情報です。パスワードを変更する必要があります *後* インスタンスのセキュリティを確保するための最初のインストール。

>[!NOTE]
>
>詳しくは、 [OSGi 設定](/help/sites-deploying/configuring-osgi.md) OSGi 設定の詳細は、を参照してください。

**OSGi Web コンソールの管理者パスワードを変更するには**:

1. の使用 **ツール**, **運用** メニュー、を開きます。 **Web コンソール** をクリックし、 **設定** 」セクションに入力します。
例： `<server>:<port>/system/console/configMgr`.
1. のエントリに移動して開きます。 **Apache Felix OSGi Management Console**.
1. を **ユーザー名** および **パスワード**.

   ![chlimage_1-3](assets/chlimage_1-3.png)

1. 「**保存**」を選択します。

### カスタムエラーハンドラーの実装 {#implement-custom-error-handler}

Adobeでは、情報開示を防ぐために、特に 404 および 500 HTTP 応答コード用に、カスタムエラーハンドラーページを定義することをお勧めします。

>[!NOTE]
>
>詳しくは、 [カスタムスクリプトやエラーハンドラーを作成する方法](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/full-stack/custom-error-page.html?lang=en) を参照してください。

### Dispatcher のセキュリティチェックリストを完了する {#complete-dispatcher-security-checklist}

AEM Dispatcher は、インフラストラクチャの重要な部分です。 Adobeでは、 [Dispatcher のセキュリティチェックリスト](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/security-checklist.html?lang=en).

>[!CAUTION]
>
>Dispatcher を使用する場合は、「.form」セレクターを無効にする必要があります。

## 検証手順 {#verification-steps}

### レプリケーションユーザーとトランスポートユーザーの設定 {#configure-replication-and-transport-users}

AEM の標準インストールでは、`admin` をデフォルトの[レプリケーションエージェント](/help/sites-deploying/replication.md)内のトランスポート認証情報のユーザーとして指定します。また、管理者ユーザーは、オーサーシステムでレプリケーションのソースを設定する際に使用します。

セキュリティに関する考慮事項については、次の 2 つの点を考慮して、特定の使用例をすぐに反映するように変更する必要があります。

* この **輸送利用者** は管理者ユーザーではない必要があります。 代わりに、パブリッシュシステムの関連する部分に対するアクセス権のみを持つユーザーをパブリッシュシステム上に設定し、そのユーザーの資格情報をトランスポートに使用します。

   バンドルされたレプリケーション受信者ユーザーから開始し、状況に合わせてそのユーザーのアクセス権限を設定できます。

* この **レプリケーションユーザー** または **エージェントユーザー ID** また、管理者ユーザーではなく、レプリケートされたコンテンツのみを表示できるユーザーでもある必要があります。 レプリケーションユーザーは、パブリッシュ元に送信される前に、オーサーシステムでレプリケートされるコンテンツを収集するために使用されます。

### 操作ダッシュボードのセキュリティヘルスチェックを確認します。 {#check-the-operations-dashboard-security-health-checks}

AEM 6 には、システムオペレーターが問題のトラブルシューティングやインスタンスの正常性の監視をおこなえるよう支援する、新しい操作ダッシュボードが導入されました。

また、このダッシュボードには、セキュリティヘルスチェックのコレクションが付属しています。 実稼動インスタンスでの運用を開始する前に、すべてのセキュリティヘルスチェックのステータスを確認することをお勧めします。 詳しくは、[操作ダッシュボードのドキュメント](/help/sites-administering/operations-dashboard.md)を参照してください。

### サンプルコンテンツが存在するかどうかを確認 {#check-if-example-content-is-present}

すべてのサンプルコンテンツとユーザー (Geometrixxプロジェクトとそのコンポーネントなど ) は、非公開でアクセスできるようにする前に、生産的なシステム上で完全にアンインストールおよび削除する必要があります。

>[!NOTE]
>
>サンプル `We.Retail` このインスタンスがで実行されている場合、アプリケーションは削除されます [実稼動準備モード](/help/sites-administering/production-ready.md). このシナリオが該当しない場合は、パッケージマネージャーに移動し、検索とアンインストールを行って、サンプルコンテンツをアンインストールできます。 `We.Retail` パッケージ。

詳しくは、 [パッケージの操作](package-manager.md).

### CRX 開発バンドルが存在するかどうかを確認します {#check-if-the-crx-development-bundles-are-present}

これらの開発用 OSGi バンドルは、アクセス可能にする前に、オーサーとパブリッシュの両方の生産システムでアンインストールする必要があります。

* AdobeCRXDE サポート (com.adobe.granite.crxde-support)
* AdobeGranite CRX Explorer (com.adobe.granite.crx-explorer)
* AdobeGraniteCRXDE Lite(com.adobe.granite.crxde-lite)

### Sling 開発バンドルが存在するかどうかを確認します。 {#check-if-the-sling-development-bundle-is-present}

この [AEM Developer Tools](/help/sites-developing/aem-eclipse.md) Apache Sling Tooling Support Install(org.apache.sling.tooling.support.install) をデプロイします。

この OSGi バンドルは、オーサーとパブリッシュの両方の生産システムでアクセス可能にする前にアンインストールする必要があります。

### クロスサイトリクエストフォージェリに対するProtect {#protect-against-cross-site-request-forgery}

#### CSRF 対策フレームワーク {#the-csrf-protection-framework}

AEM 6.1 には、クロスサイトリクエストフォージェリーから保護する **CSRF 対策フレームワーク**&#x200B;と呼ばれるメカニズムが搭載されています。使用方法について詳しくは、[ドキュメント](/help/sites-developing/csrf-protection.md)を参照してください。

#### Sling Referrer Filter {#the-sling-referrer-filter}

CRX WebDAV および Apache Sling のクロスサイトリクエストフォージェリ (CSRF) に関する既知のセキュリティ問題に対処するには、リファラーフィルターの設定を追加して、それを使用します。

リファラーフィルターサービスは、以下を設定できる OSGi サービスです。

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

1. 「`Allow Hosts`」フィールドに、リファラーとして許可するすべてのホストを入力します。各エントリは、フォームである必要があります

   &lt;protocol>://&lt;server>:&lt;port> の形式である必要があります。

   例：

   * `https://allowed.server:80` の場合、このサーバーからの指定ポートでの要求がすべて許可されます。
   * https 要求も許可する場合は、2 行目を入力する必要があります。
   * そのサーバのすべてのポートを許可する場合は、 `0` をポート番号として設定します。

1. リファラーヘッダーが空の場合やない場合を許可するには、「`Allow Empty`」フィールドを選択します。

   >[!CAUTION]
   >
   >Adobeでは、リファラーは、 `cURL` 空の値を許可する代わりに、システムが CSRF 攻撃にさらされる可能性があります。

1. このフィルターが `Filter Methods` フィールドに入力します。

1. 「**保存**」をクリックして変更を保存します。

### OSGi 設定 {#osgi-settings}

一部の OSGi 設定は、アプリケーションのデバッグを容易にするために、デフォルトで設定されています。 パブリッシュインスタンスとオーサーの実稼動インスタンスでこのような設定を変更して、内部情報が公開されないようにします。

>[!NOTE]
>
>以下のすべての設定（を除く） **Day CQ WCM Debug Filter**&#x200B;は、 [実稼動準備モード](/help/sites-administering/production-ready.md). そのため、Adobeでは、実稼動環境にインスタンスをデプロイする前に、すべての設定を確認することをお勧めします。

次の各サービスについて、指定した設定を変更する必要があります。

* [AdobeGraniteHTMLライブラリマネージャー](/help/sites-deploying/osgi-configuration-settings.md#day-cq-html-library-manager):

   * 有効 **縮小** （CRLF 文字と空白文字を削除）。
   * 有効 **Gzip** （1 回の要求でファイルを gzip で圧縮してアクセスできるようにする）。
   * 無効 **デバッグ**
   * 無効 **タイミング**

* [Day CQ WCM デバッグフィルター](/help/sites-deploying/osgi-configuration-settings.md#day-cq-wcm-debug-filter)：

   * 「**有効**」の選択を解除

* [Day CQ WCM フィルター](/help/sites-deploying/osgi-configuration-settings.md)：

   * （パブリッシュインスタンスのみ）「**WCM モード**」を「無効」に設定

* [Apache Sling JavaScript Handler](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-javascript-handler):

   * 「**デバッグ情報の生成**」を無効化

* [Apache Sling JSP スクリプトハンドラー](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-jsp-script-handler)：

   * 「**デバッグ情報の生成**」を無効化
   * 「**マッピングされたコンテンツ**」を無効化

詳しくは、 [OSGi 設定](/help/sites-deploying/osgi-configuration-settings.md).

AEMを操作する場合、このようなサービスの設定を管理する方法はいくつかあります。参照 [OSGi の設定](/help/sites-deploying/configuring-osgi.md) を参照してください。

## その他の読み取り値 {#further-readings}

### サービス拒否 (DoS) 攻撃の軽減 {#mitigate-denial-of-service-dos-attacks}

サービス拒否 (DoS) 攻撃とは、意図したユーザーがコンピュータリソースを利用できない状態にする試みです。 この攻撃は、多くの場合、リソースをオーバーロードすることで行われます。例：

* 外部ソースからの大量のリクエスト。
* システムが正常に配信できる以上の詳細情報のリクエスト。

   例えば、リポジトリ全体の JSON 表現を要求されます。

* 無制限の個数の URL を含むコンテンツページを要求される。URL にはハンドル、何らかのセレクター、拡張子、サフィックスを含める場合があり、そのいずれかを変わる可能性があります。

   例えば、`.../en.html` は次のようにリクエストされる可能性があります。

   * `.../en.ExtensionDosAttack`
   * `.../en.SelectorDosAttack.html`
   * `.../en.html/SuffixDosAttack`

   すべての有効なバリエーション ( 例えば、 `200` 応答とをキャッシュするように設定 )Dispatcher によってキャッシュされ、最終的にファイルシステムがフルになり、以降の要求に対するサービスが不要になります。

このような攻撃を防ぐための設定には多くのポイントがありますが、ここでは、AEMに関連するポイントのみについて説明します。

**DoS を防ぐための Sling の設定**

Sling は *コンテンツ中心の*.(HTTP) 要求が JCR リソース（リポジトリノード）の形式でコンテンツにマッピングされるので、処理はコンテンツに焦点を当てます。

* 最初のターゲットは、コンテンツを保持するリソース（JCR ノード）です。
* 次に、レンダラー（スクリプト）は、リソースプロパティから、要求の特定の部分（セレクターや拡張子など）と共に配置されます。

詳しくは、 [Sling リクエストの処理](/help/sites-developing/the-basics.md#sling-request-processing) を参照してください。

このアプローチにより、Sling は強力で柔軟性が高くなりますが、常に柔軟性が高く、慎重に管理する必要があります。

DoS の誤用を防ぐには、次の操作を行います。

1. アプリケーションレベルでコントロールを組み込みます。 可能なバリエーションの数により、デフォルトの設定は実行できません。

   アプリケーションでは、次の操作を実行する必要があります。

   * アプリケーションのセレクターを制御して、必要とされる明示的なセレクター&#x200B;*のみ*&#x200B;提供し、他のすべてに対しては `404` を返します。
   * コンテンツノードの数に制限がない場合に出力を防ぎます。

1. 問題のある領域になる可能性のある、デフォルトのレンダラーの設定を確認します。

   * 特に、JSON レンダラーは複数のレベルでツリー構造を横断します。

      例えば、次のようなリクエストの場合、

      `http://localhost:4502/.json`

      は、サーバーで重大な問題を引き起こす可能性のある JSON 表現でリポジトリ全体をダンプできました。 このため、Sling は最大結果数に制限を設定しています。 JSON レンダリングの深さを制限するには、次の値を設定します。

      **JSON の最大結果数**（`json.maximumresults`）

      [Apache Sling GET サーブレット](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet)の設定で指定します。この制限を超えると、レンダリングは折りたたまれます。 AEM 内での Sling 用のデフォルト値は `1000` です。

   * 予防策として、他のデフォルトのレンダラー (HTML、プレーンテキスト、XML) を無効にする必要があります。 この操作を繰り返すには、 [Apache SlingGETサーブレット](/help/sites-deploying/osgi-configuration-settings.md#apache-sling-get-servlet).
   >[!CAUTION]
   >
   >AEMの通常の操作に必要なので、JSON レンダラーを無効にしないでください。

1. ファイアウォールを使用して、インスタンスへのアクセスをフィルタリングします。

   * オペレーティングシステムレベルのファイアウォールを使用して、インスタンスのポイントへのアクセスをフィルタリングする必要があります。これにより、保護されていない状態のままにした場合に、サービス拒否攻撃が発生する可能性があります。

**フォームセレクターを使用することで生じる DoS に対する軽減策**

>[!NOTE]
>
>この軽減策は、Forms を使用していない AEM 環境でのみ実行してください。

これは、AEMでは標準で用意されている `FormChooserServlet`を使用すると、クエリでフォームセレクターを使用すると、コストのかかるリポジトリトラバーサルがトリガーになり、通常はAEMインスタンスが停止します。 フォームセレクターは、クエリに文字列 **&amp;ast;.form.&amp;ast;** が含まれていれば検出されてしまいます。

この問題を軽減するには、次の手順を実行します。

1. ブラウザーで *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr* を参照して、web コンソールに移動します

1. を検索 **Day CQ WCM Form Chooser Servlet**
1. エントリをクリックした後、 **詳細検索が必要** を次のウィンドウに表示します。

1. 「**保存**」をクリックします。

**アセットダウンロードサーブレットによって発生する DoS を軽減**

デフォルトのアセットダウンロードサーブレットを使用すると、認証済みユーザーは、任意の大きさの同時ダウンロードリクエストを発行して、アセットの ZIP ファイルを作成できます。 大きな ZIP アーカイブを作成すると、サーバーとネットワークが過負荷になる可能性があります。この動作に起因する潜在的なサービス拒否（DoS）のリスクを軽減するために、[!DNL Experience Manager] パブリッシュインスタンスでは `AssetDownloadServlet` OSGi コンポーネントがデフォルトで無効になっています。これは、[!DNL Experience Manager] オーサーインスタンスでデフォルトで有効になっています。

ダウンロード機能が必要ない場合は、オーサーデプロイメントとパブリッシュデプロイメントでサーブレットを無効にします。 セットアップでアセットダウンロードサーブレットを有効にする必要がある場合、詳細については[この記事](/help/assets/download-assets-from-aem.md)を参照してください。また、デプロイメントでサポートできるダウンロードの最大制限を定義できます。

### WebDAV を無効にする {#disable-webdav}

適切な OSGi バンドルを停止して、オーサー環境とパブリッシュ環境の両方で WebDAV を無効にします。

1. に接続 **Felix 管理コンソール** 実行日：

   `https://<*host*>:<*port*>/system/console`

   例：`http://localhost:4503/system/console/bundles`

1. バンドルのリストで、次の名前のバンドルを探します。

   `Apache Sling Simple WebDAV Access to repositories (org.apache.sling.jcr.webdav)`

1. このバンドルを停止するには、「Actions」列で停止ボタンをクリックします。

1. 再度、バンドルのリストで、次の名前のバンドルを探します。

   `Apache Sling DavEx Access to repositories (org.apache.sling.jcr.davex)`

1. このバンドルを停止するには、停止ボタンをクリックします。

   >[!NOTE]
   >
   >AEM の再起動は不要です。

### ユーザーのホームパスに個人を特定できる情報を公開していないことの確認 {#verify-that-you-are-not-disclosing-personally-identifiable-information-in-the-users-home-path}

リポジトリユーザーのホームパスに個人を特定できる情報を公開しないようにすることで、ユーザーを保護することが重要です。

AEM 6.1 以降では、新しく実装された `AuthorizableNodeName` インターフェイスにより、ユーザー ID（または認証可能な ID）のノード名を保存する方法が変わりました。新しいインターフェイスでは、ノード名にユーザー ID が表示されなくなり、代わりにランダムな名前が生成されます。

有効にする設定は実行しないでください。AEMで許可可能 ID を生成するデフォルトの方法になったからです。

非推奨ですが、既存のアプリケーションとの下位互換性を確保するために古い実装が必要な場合に備えて、無効にすることができます。 これをおこなうには、次の手順を実行する必要があります。

1. Web コンソールに移動して、**Apache Jackrabbit Oak SecurityProvider** のプロパティ **requiredServicePids** から org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName エントリを削除します。

   また、OSGi 設定の **org.apache.jackrabbit.oak.security.internal.SecurityProviderRegistration** PID を探すことで、Oak Security Provider を見つけることもできます。

1. Web コンソールから **Apache Jackrabbit Oak Random Authorizable Node Name** OSGi 設定を削除します。

   検索を容易にするために、この設定の PID は次のようになります。 **org.apache.jackrabbit.oak.security.user.RandomAuthorizableNodeName**.

>[!NOTE]
>
>詳しくは、 [許可可能なノード名の生成](https://jackrabbit.apache.org/oak/docs/security/user/authorizablenodename.html).

### 匿名権限堅牢化パッケージ {#anonymous-permission-hardening-package}

デフォルトでは、AEMには次のようなシステムメタデータが格納されます。 `jcr:createdBy` または `jcr:lastModifiedBy` ノードのプロパティとして、通常のコンテンツの横にあるリポジトリで。 設定とアクセス制御の設定に応じて、場合によっては、これによって、例えば、生の JSON または XML としてレンダリングされる場合などに、個人識別情報 (PII) が公開される可能性があります。

すべてのリポジトリデータと同様に、これらのプロパティは Oak 認証スタックによって仲介されます。 権限の最小化の原則に従って、アクセスを制限する必要があります。

これをサポートするため、Adobeは、お客様が構築する基盤として、許可堅牢化パッケージを提供します。 これは、リポジトリのルートに「拒否」アクセス制御エントリをインストールし、一般的に使用されるシステムプロパティに匿名アクセスを制限することで機能します。 パッケージをダウンロードできます [ここ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/helper/anonymous-permissions-pkg-0.1.2.zip) とは、サポートされているすべてのバージョンのAEMにインストールできます。 詳しくは、リリースノートを参照してください。

### クリックジャッキングの防止 {#prevent-clickjacking}

クリックジャックを防ぐため、Adobeでは、Web サーバーで `X-FRAME-OPTIONS` HTTP ヘッダーをに設定 `SAMEORIGIN`.

クリックジャッキングについて詳しくは、 [OWASP サイト](https://www.owasp.org/index.php/Clickjacking).

### 必要に応じて、暗号化キーを適切にレプリケートする {#make-sure-you-properly-replicate-encryption-keys-when-needed}

特定のAEM機能および認証スキームでは、すべてのAEMインスタンスに暗号化キーをレプリケートする必要があります。

キーの保存方法は 6.3 以前のバージョンとは異なるので、事前にキーのレプリケーションはバージョン間で異なる方法でおこなわれます。

詳しくは、以下を参照してください。

#### AEM 6.3 のキーのレプリケート {#replicating-keys-for-aem}

以前のバージョンでは、レプリケーションキーはAEM 6.3 以降、ファイルシステムに保存されていました。

したがって、インスタンス間で鍵をレプリケートするには、ソースインスタンスからファイルシステム上のターゲットインスタンスの場所に鍵をコピーします。

具体的には、次の操作を行う必要があります。

1. コピーする主要な素材を含むAEMインスタンス（通常はオーサーインスタンス）にアクセスします。
1. ローカルファイルシステム内で、com.adobe.granite.crypto.file を見つけます。例えば、次のパスにあります。

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`

   この `bundle.info` 各フォルダー内のファイルは、バンドル名を識別します。

1. データフォルダーに移動します。次に例を示します。

   * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. HMAC ファイルとマスターファイルをコピーします。
1. 次に、HMAC キーの複製先のターゲットインスタンスに移動し、データフォルダーに移動します。 次に例を示します。

   * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

1. 前の手順でコピーした 2 つのファイルを貼り付けます。
1. ターゲットインスタンスが既に実行されている場合は、[Crypto バンドルを更新](/help/communities/deploy-communities.md#refresh-the-granite-crypto-bundle)します。
1. キーのレプリケート先となるすべてのインスタンスに対して、上記の手順を繰り返します。

>[!NOTE]
>
>AEMを初めてインストールする際に、以下のパラメーターを追加することで、6.3 より前のキーの保存方法に戻すことができます。
>
>`-Dcom.adobe.granite.crypto.file.disable=true`

#### AEM 6.2 以前のバージョンでの鍵のレプリケーション {#replicating-keys-for-aem-and-older-versions}

AEM 6.2 以前のバージョンでは、鍵は `/etc/key` ノードの下のリポジトリに保存されます。

インスタンス間で鍵を安全にレプリケートするには、このノードのみをレプリケートすることをお勧めします。 ノードを選択してレプリケートするには、次のCRXDE Liteを使用します。

1. *`https://&lt;serveraddress&gt;:4502/crx/de/index.jsp`* に移動して CRXDE Lite を開きます
1. `/etc/key` ノードを選択します。
1. 次に移動： **レプリケーション** タブをクリックします。
1. を押します。 **レプリケーション** 」ボタンをクリックします。

### 侵入テストの実施 {#perform-a-penetration-test}

Adobeでは、実稼動環境に移行する前に、AEMインフラストラクチャの侵入テストを実行することをお勧めします。

### 開発のベストプラクティス {#development-best-practices}

新しい開発が [セキュリティのベストプラクティス](/help/sites-developing/security.md) AEM環境を安全に保つため。
