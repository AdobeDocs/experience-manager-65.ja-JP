---
title: Document Security によって保護された PDF ドキュメントを AEM で検索可能にする
seo-title: Document Security によって保護された PDF ドキュメントを AEM で検索可能にする
description: 'ネイティブ AEM 検索を有効にし、DRM 保護された PDF ドキュメントで全テキストの検索を実行する方法について説明します。  '
seo-description: 'ネイティブ AEM 検索を有効にし、DRM 保護された PDF ドキュメントで全テキストの検索を実行する方法について説明します。  '
uuid: ec6e5d53-a74c-4958-a389-7937d073c083
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/working_with_document_security
discoiquuid: b79c147c-f846-4e48-bec0-8b658502bb6f
docset: aem65
translation-type: tm+mt
source-git-commit: b703c59d7d913fc890c713c6e49e7d89211fd998
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 86%

---


# Document Security によって保護された PDF ドキュメントを AEM で検索可能にする{#enable-aem-to-search-document-security-protected-pdf-documents}

AEM 検索では、AEM アセットの検索と場所の特定をすることができます。また、プレーンテキストファイル、Microsoft Office ドキュメント、PDF ドキュメントなど、広く使用されているさまざまなドキュメント形式において、テキスト検索を実行することができます。ネイティブ検索を拡張し、[AEM Document Security で保護された PDF ドキュメント](../../forms/using/admin-help/document-security.md)で全テキストの検索を実行することも可能です。このようなドキュメントで全テキストの検索を AEM で実行できるようにするには、次の手順を実行します。

1. 安全な接続の確立
1. サンプルポリシーで保護された PDF ドキュメントのインデックス作成

## 前提条件 {#prerequisites}

* OSGi 上で AEM Forms を使用している場合：

   * [AEM Forms Document Security Indexer パッケージ](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html)を AEM Forms サーバーにインストールします。

   * JEE サーバー上で AEM Forms が起動して実行されていること、および Document Security が JEE サーバー上の対応する AEM Forms にインストールされていることを確認します。保護されたドキュメントのインデックスを作成するには、JEE サーバー上の AEM Form が必要です。

* JEE サーバー上で AEM Forms のみを使用している場合、Indexer パッケージはすでにインストールされています。
* すべてのバンドルが正常に実行していることを確認します。アクティブ状態になっていないバンドルが存在する場合は、すべてのバンドルが起動して実行されるまで待ちます。

   * For AEM Forms on OSGi, the bundles are listed at https://&#39;[server]:[port]&#39;/system/console/bundles.
   * For AEM Forms on JEE, the bundles are listed at https://&#39;[server]:[port]&#39;/[context-path]/system/console/bundles. 例：https://localhost:8080/lc/system/console/bundles

* 許可リスト追加に対する *sun.util.calendar* パッケージ。 パッケージを許可リストに追加するには、次の手順を実行します。

   1. AEM Web コンソールを開きます。The URL is https://&#39;[server]:[port]&#39;/system/console/configMgr.
   1. **デシリアライゼーションファイアウォール設定**&#x200B;を探して開きます。

   1. Add the sun.util.calendar package to the Allowlisted classes or package prefixes field and click **Save**.

### AEM Forms JEE と OSGi スタック間の安全な接続の確立 {#establish-a-secure-connection-between-aem-forms-jee-and-osgi-stacks}

次のいずれかの方法を使用して安全な接続を確立します。

* JEE 上の AEM Forms の管理者資格情報を使用して Adobe LiveCycle Client SDK Bundle を設定します
* 相互認証を使用した Adobe LiveCycle Client SDK Bundle の設定

#### JEE 上の AEM Forms の管理者資格情報を使用して Adobe LiveCycle Client SDK Bundle を設定します {#configure-adobe-livecycle-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. AEM Web コンソールを開きます。The URL is https://&#39;[server]:[port]&#39;/system/console/configMgr.
1. **Adobe LiveCycle Client SDK Bundle** を探して開きます。次の各フィールドの値を指定します。

   * **サーバー URL**：JEE サーバー上の AEM Forms の HTTPS URL を指定します。HTTPS 経由の通信を可能にするには、-Djavax.net.ssl.trustStore=&lt;JEE キーストアファイル上の Forms のパス> のパラメータで AEM サーバーを再起動します。
   * **サービス名**：指定されたサービスの一覧に RightsManagementService を追加します。
   * **ユーザー名**：AEM サーバーからの呼び出しの開始に使用される JEE 上の AEM Forms アカウントのユーザー名を指定します。指定したアカウントは、JEE サーバー上の AEM Forms で Document Services を開始することができる権限が付与されている必要があります。
   * **パスワード**：Username フィールドに表示される JEE 上の AEM Forms アカウントのパスワードを指定します。
   「**保存**」をクリックします。AEM は Document Security によって保護された PDF ドキュメントの検索が有効になっています。

#### 相互認証を使用した Adobe LiveCycle Client SDK Bundle の設定 {#configure-adobe-livecycle-client-sdk-bundle-using-mutual-authentication}

1. JEE 上の AEM Forms の相互認証を有効にします。詳しくは、「[CAC および相互認証](https://helpx.adobe.com/jp/livecycle/kb/cac-mutual-authentication.html)」を参照してください。
1. AEM Web コンソールを開きます。The URL is https://&#39;[server]:[port]&#39;/system/console/configMgr.
1. **Adobe LiveCycle Client SDK** Bundle を探して開きます。次の各プロパティの値を指定します。

   * **サーバー URL**：JEE サーバー上の AEM Forms の HTTPS URL を指定します。HTTPS 経由の通信を可能にするには、-Djavax.net.ssl.trustStore=&lt;JEE キーストアファイル上の AEM Forms のパス> のパラメータで AEM サーバーを再起動します。
   * **2way SSL の有効化**：「2way SSL の有効化」を有効にします。
   * **キーストアファイル URL**：キーストアファイルの URL を指定します。
   * **TrustStore ファイル URL**：Truststore ファイルの URL を指定します.
   * **キーストアパスワード**：キーストアファイルのパスワードを指定します。
   * **TrustStore パスワード**：Truststore ファイルのパスワードを指定します。
   * **サービス名**：指定されたサービスの一覧に RightsManagementService を追加します。
   「**保存**」をクリックします。AEM は Document Security によって保護された PDF ドキュメントの検索が有効になっています。

### サンプルポリシーで保護された PDF ドキュメントのインデックス作成 {#index-a-sample-policy-protected-pdf-document}

1. 管理者として AEM Assets にログインします。
1. AEM Digital Asset Manager でフォルダーを作成し、新しく作成したフォルダーにポリシーで保護された PDF ドキュメントをアップロードします。

   これで AEM 検索を使用してポリシーで保護されたドキュメントを検索できるようになりました。

