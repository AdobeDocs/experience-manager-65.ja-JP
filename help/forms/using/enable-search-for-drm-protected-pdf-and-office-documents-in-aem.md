---
title: Document Security によって保護された PDF ドキュメントと Microsoft Office ドキュメントを AEM で検索可能にする
seo-title: Document Security によって保護された PDF ドキュメントと Microsoft Office ドキュメントを AEM で検索可能にする
description: ネイティブ AEM 検索を有効にし、DRM 保護された PDF ドキュメントで全テキストの検索を実行する方法について説明します。
seo-description: ネイティブ AEM 検索を有効にし、DRM 保護された PDF ドキュメントで全テキストの検索を実行する方法について説明します。
uuid: dba882f8-bad4-4122-a0df-03cf087afb23
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7eebef08-83b9-4b56-90ec-35ab3b0c27e8
noindex: true
translation-type: tm+mt
source-git-commit: b703c59d7d913fc890c713c6e49e7d89211fd998
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 77%

---


# Document Security によって保護された PDF ドキュメントと Microsoft Office ドキュメントを AEM で検索可能にする{#enable-aem-to-search-document-security-protected-pdf-and-microsoft-office-documents}

Adobe Experience Manager には、AEM に保存された様々なアセットを検索し、その場所を特定するためのユーザーインターフェイスが用意されています。ネイティブ検索機能を使用して AEM アセットを検索し  テキスト検索は、プレーンテキストファイル、Microsoft Officeドキュメント、PDFドキュメントなど、一般的に使用される様々なドキュメント形式に基づいて行われます。 ネイティブ検索を拡張して有効にし、DRM保護されたPDFおよびMicrosoft Officeドキュメントでフルテキスト検索を実行することもできます。

次の手順を実行し、Document Security によって保護された PDF ドキュメントと Microsoft Office ドキュメントを AEM で検索可能にします。

## 事前準備 {#before-you-start}

* AEM Forms Document Security をインストールして設定します。
* sun.util.calendar追加を&#x200B;**デシリアル化ファイアウォール構成の許可リストにパッケージ化します。** 設定は、に一覧表示され `https://'[server]:[port]'/system/console/configMgr`ます。
* すべての AEM バンドルが正常に実行していることを確認します。バンドルは`https://'[server]:[port]'/system/console/bundles`に一覧表示されます。 アクティブ状態になっていないバンドルが存在する場合、数分間待ってからバンドルの状態を確認してください。

## AEM Formsワークフロー(JEE上のAEM Forms){#establish-a-secure-connection-within-aem-forms-workflow-aem-forms-on-jee}内での安全な接続の確立

安全な接続は、JEE 上の AEM Forms と、同じサーバー上で実行している OSGi サービスとの間の情報の流れをシームレスにします。次のいずれかの方法を使用して安全な接続を確立します。

* JEE 上の AEM Forms の管理者資格情報を使用して AEM Forms Client SDK Bundle を設定します
* 相互認証を使用して AEM Forms Client SDK Bundle を設定します

### JEE 上の AEM Forms の管理者資格情報を使用して AEM Forms Client SDK Bundle を設定します {#configure-aem-forms-client-sdk-bundle-with-aem-forms-on-jee-admin-credentials}

1. AEM Configuration Manager を開き、管理者としてログインします。デフォルトのURLはhttps://&lt;serverName>:&lt;port>/lc/system/console/configMgrです。
1. AEM Forms Client SDK Bundle を探して開きます。次の各プロパティの値を指定します。

   * **サーバー URL**：JEE サーバー上の AEM Forms の HTTP URL を指定します。HTTPS経由の通信を可能にするには、-Djavax.net.ssl.trustStore=&lt;JEEキーストアファイルのAEM Formsのパス>パラメーターを使用して、JEEサーバー上のAEM Formsを再起動します。
   * **サービス名**：指定されたサービスの一覧に RightsManagementService を追加します。
   * **ユーザー名：** JEE サーバー上の AEM Forms からの呼び出しの開始に使用される JEE アカウントの AEM Forms のユーザー名を指定します。指定したアカウントは、JEE サーバー上の AEM Forms で Document Services を呼び出すことができる権限が付与されている必要があります。
   * **パスワード**：「ユーザー名」フィールドに表示される JEE 上の AEM Forms アカウントのパスワードを指定します。

   「**保存**」をクリックします。AEM は、Document Security によって保護された PDF ドキュメントと Microsoft Office ドキュメントの検索が有効になっています。

### 相互認証を使用して AEM Forms Client SDK Bundle を設定します  {#configure-aem-forms-client-sdk-bundle-using-mutual-authentication}

1. JEE 上の AEM Forms の相互認証を有効にします。詳しくは、「[CAC および相互認証](https://helpx.adobe.com/jp/livecycle/kb/cac-mutual-authentication.html)」を参照してください。
1. AEM Configuration Manager を開き、管理者としてログインします。デフォルトのURLはhttps://&lt;serverName>:&lt;port>/lc/system/console/configMgrです。
1. AEM Forms Client SDK Bundle を探して開きます。次の各プロパティの値を指定します。

   * **サーバー URL**：JEE サーバー上の AEM Forms の HTTPS URL を指定します。HTTPS経由の通信を可能にするには、-Djavax.net.ssl.trustStore=&lt;JEEキーストアファイルのAEM Formsのパス>パラメーターを使用して、JEEサーバー上のAEM Formsを再起動します。
   * **2way SSL の有効化**：「2way SSL の有効化」を有効にします。
   * **キーストアファイル URL**：キーストアファイルの URL を指定します。
   * **TrustStore ファイル URL**：Truststore ファイルの URL を指定します.
   * **キーストアパスワード**：キーストアファイルのパスワードを指定します。
   * **TrustStore パスワード**：Truststore ファイルのパスワードを指定します。
   * **サービス名**：指定されたサービスの一覧に RightsManagementService を追加します。

   「**保存**」をクリックします。AEM は、Document Security によって保護された PDF ドキュメントと Microsoft Office ドキュメントの検索が有効になっています。

## サンプルポリシーで保護された PDF ドキュメントまたは Microsoft Office ドキュメントのインデックス作成  {#index-a-sample-policy-protected-pdf-or-microsoft-office-document}

1. 管理者として AEM Assets にログインします。
1. AEM Digital Asset Manager でフォルダーを作成し、新しく作成したフォルダーにポリシーで保護された PDF ドキュメントまたは Microsoft Office ドキュメントをアップロードします。これで AEM 検索を使用してポリシーで保護されたドキュメントのコンテンツを検索できます。検索したテキストを含むドキュメントを返す必要があります。

