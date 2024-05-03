---
title: Document Security によって保護された PDF ドキュメントと Microsoft Office ドキュメントを AEM で検索可能にする
description: ネイティブ AEM 検索を有効にし、DRM 保護された PDF ドキュメントで全テキストの検索を実行する方法について説明します。
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
noindex: true
feature: Document Security
exl-id: 91cbd1f1-d53d-455b-8d2c-6918b521db81
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 100%

---

# Document Security によって保護された PDF ドキュメントと Microsoft Office ドキュメントを AEM で検索可能にする{#enable-aem-to-search-document-security-protected-pdf-and-microsoft-office-documents}

Adobe Experience Manager には、AEM に保存された様々なアセットを検索し、その場所を特定するためのユーザーインターフェイスが用意されています。ネイティブ検索では、AEM アセットの検索と場所の特定を行うことができます。また、プレーンテキストファイル、Microsoft Office ドキュメント、PDF ドキュメントなど、広く使用されている様々なドキュメント形式において、テキスト検索を実行することができます。ネイティブ検索を拡張して有効にし、DRM 保護された PDF ドキュメントと Microsoft Office ドキュメントで全テキストの検索を実行できるようにすることも可能です。

次の手順を実行し、ドキュメントセキュリティによって保護された PDF ドキュメントと Microsoft Office ドキュメントを AEM で検索可能にします。

## 事前準備 {#before-you-start}

* AEM Forms ドキュメントセキュリティをインストールして設定します。
* sun.util.calendar パッケージを&#x200B;**デシリアライゼーションファイアウォール設定の許可リストに追加します。**&#x200B;設定は `https://'[server]:[port]'/system/console/configMgr` にリストされます。
* すべての AEM バンドルが正常に実行していることを確認します。バンドルは `https://'[server]:[port]'/system/console/bundles` にリストされます。アクティブ状態になっていないバンドルが存在する場合、数分間待ってからバンドルの状態を確認してください。

## AEM Forms Workflow（AEM Forms on JEE）内での安全な接続の確立 {#establish-a-secure-connection-within-aem-forms-workflow-aem-forms-on-jee}

安全な接続は、AEM Forms on JEE と、同じサーバー上で実行している OSGi サービスとの間の情報の流れをシームレスにします。次のいずれかの方法を使用して安全な接続を確立します。

* JEE 上の AEM Forms の管理者資格情報を使用した AEM Forms Client SDK Bundle の設定
* 相互認証を使用した AEM Forms Client SDK Bundle の設定

### JEE 上の AEM Forms の管理者資格情報を使用した AEM Forms Client SDK Bundle の設定 {#configure-aem-forms-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. AEM Configuration Manager を開き、管理者としてログインします。デフォルトの URL は https://&lt;serverName>:&lt;port>/lc/system/console/configMgr です。
1. AEM Forms クライアント SDK バンドルを探して開きます。次の各プロパティの値を指定します。

   * **サーバー URL**：JEE サーバー上の AEM Forms の HTTP URL を指定します。HTTPS 経由の通信を可能にするには、-Djavax.net.ssl.trustStore=&lt;JEE キーストアファイル上の AEM Forms のパス> のパラメーターを使用して、JEE サーバー上の AEM Forms を再起動します。
   * **サービス名**：指定されたサービスの一覧に RightsManagementService を追加します。
   * **ユーザー名：** JEE サーバー上の AEM Forms からの呼び出しの開始に使用される JEE アカウントの AEM Forms のユーザー名を指定します。指定したアカウントには、AEM Forms on JEE サーバーでドキュメントサービスを呼び出すことができる権限が付与されている必要があります。
   * **パスワード**：ユーザー名フィールドに表示される AEM Forms on JEE アカウントのパスワードを指定します。

   「**保存**」をクリックします。AEM では、ドキュメントセキュリティによって保護された PDF ドキュメントと、Microsoft Office ドキュメントの検索が有効になっています。

### 相互認証を使用した AEM Forms Client SDK Bundle の設定 {#configure-aem-forms-client-sdk-bundle-using-mutual-authentication}

1. AEM Forms on JEE の相互認証を有効にします。詳しくは、[CAC および相互認証](https://helpx.adobe.com/jp/livecycle/kb/cac-mutual-authentication.html)を参照してください。
1. AEM Configuration Manager を開き、管理者としてログインします。デフォルトの URL は https://&lt;serverName>:&lt;port>/lc/system/console/configMgr です。
1. AEM Forms クライアント SDK バンドルを探して開きます。次の各プロパティの値を指定します。

   * **サーバー URL**：JEE サーバー上の AEM Forms の HTTPS URL を指定します。HTTPS 経由の通信を可能にするには、-Djavax.net.ssl.trustStore=&lt;JEE キーストアファイル上の AEM Forms のパス> のパラメーターを使用して、JEE サーバー上の AEM Forms を再起動します。
   * **2way SSL の有効化**：「2way SSL の有効化」オプションを有効にします。
   * **キーストアファイル URL**：キーストアファイルの URL を指定します。
   * **TrustStore ファイル URL**：Truststore ファイルの URL を指定します。
   * **キーストアパスワード**：キーストアファイルのパスワードを指定します。
   * **TrustStore パスワード**：Truststore ファイルのパスワードを指定します。
   * **サービス名**：指定されたサービスの一覧に RightsManagementService を追加します。

   「**保存**」をクリックします。AEM では、ドキュメントセキュリティによって保護された PDF ドキュメントと、Microsoft Office ドキュメントの検索が有効になっています。

   >[!NOTE]
   >
   > SDK を再起動するには、「Ctrl + C」コマンドを使用することをお勧めします。Java プロセスの停止など、別の方法を使用して AEM SDK を再起動すると、AEM 開発環境で不整合が生じる場合があります。

## サンプルポリシーで保護された PDF ドキュメントまたは Microsoft Office ドキュメントのインデックス作成 {#index-a-sample-policy-protected-pdf-or-microsoft-office-document}

1. 管理者として AEM Assets にログインします。
1. AEM Digital Asset Manager でフォルダーを作成し、新しく作成したフォルダーにポリシーで保護された PDF ドキュメントまたは Microsoft Office ドキュメントをアップロードします。これで AEM 検索を使用してポリシーで保護されたドキュメントのコンテンツを検索できます。検索したテキストを含むドキュメントが返されます。
