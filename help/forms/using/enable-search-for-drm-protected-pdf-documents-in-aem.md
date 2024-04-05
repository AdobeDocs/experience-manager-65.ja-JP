---
title: Document Security によって保護された PDF ドキュメントを AEM で検索可能にする
description: ネイティブ AEM 検索を有効にし、DRM 保護された PDF ドキュメントで全テキストの検索を実行する方法について説明します。
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
geptopics: SG_AEMFORMS/categories/working_with_document_security
docset: aem65
feature: Document Security
exl-id: 7cf17fb6-021a-473e-bc3b-27c317953002
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 100%

---

# Document Security によって保護された PDF ドキュメントを AEM で検索可能にする{#enable-aem-to-search-document-security-protected-pdf-documents}

AEM 検索では、AEM アセットを検索して場所を特定することができます。また、プレーンテキストファイル、Microsoft Office ドキュメント、PDF ドキュメントなどの一般的に使用されている様々なドキュメント形式において、テキスト検索を実行することができます。ネイティブ検索を拡張し、[AEM Document Security で保護された PDF ドキュメント](../../forms/using/admin-help/document-security.md)で全文検索を実行することも可能です。このようなドキュメントに対する全文検索を AEM で実行できるようにするには、次の手順を実行します。

1. 安全な接続を確立
1. ポリシーで保護されたサンプルの PDF ドキュメントをインデックス化

## 前提条件 {#prerequisites}

* OSGi 上で AEM Forms を使用している場合：

   * [AEM Forms Document Security Indexer パッケージ](https://helpx.adobe.com/jp/aem-forms/kb/aem-forms-releases.html)を AEM Forms サーバーにインストールします。

   * JEE サーバー上で AEM Forms が起動して実行されていること、および Document Security が JEE サーバー上の対応する AEM Forms にインストールされていることを確認します。保護されたドキュメントのインデックスを作成するには、JEE サーバー上の AEM Form が必要です。

* JEE サーバー上で AEM Forms のみを使用している場合、Indexer パッケージはすでにインストールされています。
* すべてのバンドルが正常に実行していることを確認します。アクティブ状態になっていないバンドルが存在する場合は、すべてのバンドルが起動して実行されるまで待ちます。

   * OSGi 上の AEM Forms の場合、バンドルは https://&#39;[server]:[port]&#39;/system/console/bundles に一覧表示されます。
   * JEE 上の AEM Forms の場合、バンドルは https://&#39;[server]:[port]&#39;/[context-path]/system/console/bundles に一覧表示されます。例：https://localhost:8080/lc/system/console/bundles。

* *sun.util.calendar* パッケージを許可リストに追加します。パッケージを許可リストに追加するには、次の手順を実行します。

   1. AEM Web コンソールを開きます。URL は https://&#39;[server]:[port]&#39;/system/console/configMgr です。
   1. **デシリアライゼーションファイアウォール設定**&#x200B;を探して開きます。

   1. sun.util.calendar パッケージを、許可リストに登録済みのクラスまたはパッケージ接頭辞のフィールドに追加して、「**保存**」をクリックします。

### AEM Forms JEE と OSGi スタック間の安全な接続を確立 {#establish-a-secure-connection-between-aem-forms-jee-and-osgi-stacks}

次のいずれかの方法を使用して安全な接続を確立します。

* JEE 上の AEM Forms の管理者資格情報を使用して Adobe LiveCycle Client SDK バンドルを設定します
* 相互認証を使用した Adobe LiveCycle Client SDK Bundle の設定

#### JEE 上の AEM Forms の管理者資格情報を使用して Adobe LiveCycle Client SDK バンドルを設定します {#configure-adobe-livecycle-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. AEM Web コンソールを開きます。URL は https://&#39;[server]:[port]&#39;/system/console/configMgr です。
1. **Adobe LiveCycle Client SDK バンドル**&#x200B;を探して開きます。次の各フィールドの値を指定します。

   * **サーバー URL**：JEE サーバー上の AEM Forms の HTTPS URL を指定します。HTTPS 経由の通信を可能にするには、-Djavax.net.ssl.trustStore=&lt;JEE キーストアファイル上の AEM Forms のパス> のパラメータで AEM サーバーを再起動します。
   * **サービス名**：指定されたサービスの一覧に RightsManagementService を追加します。
   * **ユーザー名**：AEM サーバーからの呼び出しの開始に使用される JEE 上の AEM Forms アカウントのユーザー名を指定します。指定したアカウントには、JEE サーバー上の AEM Forms でドキュメントサービスを開始する権限が付与されている必要があります。
   * **パスワード**：「ユーザー名」フィールドに表示される JEE 上の AEM Forms アカウントのパスワードを指定します。

   「**保存**」をクリックします。AEM で、Document Security によって保護された PDF ドキュメントを検索できるようになります。

#### 相互認証を使用した Adobe LiveCycle Client SDK Bundle の設定 {#configure-adobe-livecycle-client-sdk-bundle-using-mutual-authentication}

1. AEM Forms on JEE の相互認証を有効にします。詳しくは、[CAC および相互認証](https://helpx.adobe.com/jp/livecycle/kb/cac-mutual-authentication.html)を参照してください。
1. AEM Web コンソールを開きます。URL は https://&#39;[server]:[port]&#39;/system/console/configMgr です。
1. **Adobe LiveCycle Client SDK** バンドルを探して開きます。次の各プロパティの値を指定します。

   * **サーバー URL**：JEE サーバー上の AEM Forms の HTTPS URL を指定します。HTTPS 経由の通信を有効にするには、-Djavax.net.ssl.trustStore=&lt;path of AEM Forms on JEE keystore file> のパラメーターを使用して AEM サーバーを再起動します。
   * **2way SSL の有効化**：「2way SSL の有効化」オプションを有効にします。
   * **キーストアファイル URL**：キーストアファイルの URL を指定します。
   * **TrustStore ファイル URL**：Truststore ファイルの URL を指定します.
   * **キーストアパスワード**：キーストアファイルのパスワードを指定します。
   * **TrustStore パスワード**：Truststore ファイルのパスワードを指定します。
   * **サービス名**：指定されたサービスの一覧に RightsManagementService を追加します。

   「**保存**」をクリックします。AEM で、Document Security によって保護された PDF ドキュメントを検索できるようになります。

### ポリシーで保護されたサンプルの PDF ドキュメントをインデックス化 {#index-a-sample-policy-protected-pdf-document}

1. 管理者として AEM Assets にログインします。
1. AEM Digital Asset Manager でフォルダーを作成し、新しく作成したフォルダーにポリシーで保護された PDF ドキュメントをアップロードします。

   これで、AEM 検索を使用してポリシーで保護されたドキュメントを検索できるようになりました。

   >[!NOTE]
   >
   > 「Ctrl + C」コマンドを使用して SDK を再起動することをお勧めします。 別の方法（Java プロセスの停止など）を使用してAEM SDK を再起動すると、AEM開発環境で不整合が生じる場合があります。
