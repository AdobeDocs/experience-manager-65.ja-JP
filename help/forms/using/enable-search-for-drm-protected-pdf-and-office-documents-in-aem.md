---
title: Document Security によって保護された PDF ドキュメントと Microsoft Office ドキュメントを AEM で検索可能にする
description: DRM 保護されたドキュメントでネイティブAEM検索を有効にして全文検索を実行する方法をPDFします。
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
noindex: true
feature: Document Security
exl-id: 91cbd1f1-d53d-455b-8d2c-6918b521db81
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 57%

---

# Document Security によって保護された PDF ドキュメントと Microsoft Office ドキュメントを AEM で検索可能にする{#enable-aem-to-search-document-security-protected-pdf-and-microsoft-office-documents}

Adobe Experience Managerは、AEMに保存されている様々なアセットを検索して検索するためのユーザーインターフェイスを提供します。 ネイティブ検索では、AEMアセットを検索および検索し、プレーンテキストファイル、Microsoft Office ドキュメント、PDFドキュメントなど、一般的に使用される様々なドキュメント形式でテキスト検索を実行できます。 ネイティブ検索を拡張して有効にし、DRM 保護された PDF ドキュメントと Microsoft Office ドキュメントで全テキストの検索を実行できるようにすることも可能です。

AEMが Document Security で保護されたPDFとMicrosoft Office ドキュメントを検索できるようにするには、次の手順を実行します。

## 事前準備 {#before-you-start}

* AEM Forms Document Security をインストールして設定します。
* sun.util.calendar パッケージを&#x200B;**デシリアライゼーションファイアウォール設定の許可リストに追加します。**&#x200B;設定は `https://'[server]:[port]'/system/console/configMgr` にリストされます。
* すべての AEM バンドルが正常に実行していることを確認します。バンドルは `https://'[server]:[port]'/system/console/bundles` にリストされます。アクティブ状態になっていないバンドルが存在する場合、数分間待ってからバンドルの状態を確認してください。

## AEM Formsワークフロー (JEE 上のAEM Forms) 内での安全な接続の確立 {#establish-a-secure-connection-within-aem-forms-workflow-aem-forms-on-jee}

安全な接続により、同じサーバー上で実行されている JEE 上のAEM Formsと OSGi サービスとの間で、情報をシームレスにやり取りできます。 次のいずれかの方法を使用して安全な接続を確立します。

* JEE 上の AEM Forms の管理者資格情報を使用した AEM Forms Client SDK Bundle の設定
* 相互認証を使用した AEM Forms Client SDK Bundle の設定

### JEE 上の AEM Forms の管理者資格情報を使用した AEM Forms Client SDK Bundle の設定 {#configure-aem-forms-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. AEM Configuration Manager を開き、管理者としてログインします。 デフォルトの URL は https://&lt;serverName>:&lt;port>/lc/system/console/configMgr です。
1. AEM Forms Client SDK バンドルを検索して開きます。 次のプロパティの値を指定します。

   * **サーバー URL**：JEE サーバー上の AEM Forms の HTTP URL を指定します。HTTPS 経由の通信を可能にするには、-Djavax.net.ssl.trustStore=&lt;JEE キーストアファイル上の AEM Forms のパス> のパラメーターを使用して、JEE サーバー上の AEM Forms を再起動します。
   * **サービス名**：指定されたサービスの一覧に RightsManagementService を追加します。
   * **ユーザー名：** JEE サーバー上の AEM Forms からの呼び出しの開始に使用される JEE アカウントの AEM Forms のユーザー名を指定します。指定したアカウントには、JEE サーバー上のAEM Formsで Document Services を呼び出す権限が必要です。
   * **パスワード**:「ユーザー名」フィールドで説明した JEE 上のAEM Formsアカウントのパスワードを指定します。

   「**保存**」をクリックします。AEMでは、Document Security で保護されたPDFとMicrosoft Office ドキュメントを検索できます。

### 相互認証を使用した AEM Forms Client SDK Bundle の設定 {#configure-aem-forms-client-sdk-bundle-using-mutual-authentication}

1. JEE 上のAEM Formsの相互認証を有効にします。 詳しくは、 [CAC と相互認証](https://helpx.adobe.com/jp/livecycle/kb/cac-mutual-authentication.html).
1. AEM Configuration Manager を開き、管理者としてログインします。 デフォルトの URL は https://&lt;serverName>:&lt;port>/lc/system/console/configMgr です。
1. AEM Forms Client SDK バンドルを検索して開きます。 次のプロパティの値を指定します。

   * **サーバー URL**：JEE サーバー上の AEM Forms の HTTPS URL を指定します。HTTPS 経由の通信を可能にするには、-Djavax.net.ssl.trustStore=&lt;JEE キーストアファイル上の AEM Forms のパス> のパラメーターを使用して、JEE サーバー上の AEM Forms を再起動します。
   * **2way SSL の有効化**：「2way SSL の有効化」オプションを有効にします。
   * **キーストアファイル URL**：キーストアファイルの URL を指定します。
   * **TrustStore ファイル URL**：Truststore ファイルの URL を指定します。
   * **キーストアパスワード**：キーストアファイルのパスワードを指定します。
   * **TrustStore パスワード**：Truststore ファイルのパスワードを指定します。
   * **サービス名**：指定されたサービスの一覧に RightsManagementService を追加します。

   「**保存**」をクリックします。AEMは、Document Security で保護されたPDFとMicrosoft Office ドキュメントを検索できます

## ポリシーで保護されたサンプルPDFまたはMicrosoft Office ドキュメントのインデックスを作成する {#index-a-sample-policy-protected-pdf-or-microsoft-office-document}

1. 管理者として AEM Assets にログインします。
1. AEM Digital Asset Manager でフォルダーを作成し、新しく作成したフォルダーにポリシーで保護されたPDFーまたはMicrosoft Office ドキュメントをアップロードします。 これで AEM 検索を使用してポリシーで保護されたドキュメントのコンテンツを検索できます。検索したテキストを含むドキュメントが返されます。
