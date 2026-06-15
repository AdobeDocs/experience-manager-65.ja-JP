---
title: ドキュメントのセキュリティのために外部ブラウザーからの拡張認証を設定する
description: システムのデフォルトのweb ブラウザーを使用して、AcrobatまたはReaderでポリシーで保護されたPDF ドキュメントを認証できるように、外部ブラウザー認証を設定する方法について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_document_security
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: Document Security
exl-id: a452674c-aea0-45d6-88cd-438af539d355
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: 98a772829d3568a5826ea9e3ae65760f1587040f
workflow-type: tm+mt
source-wordcount: '986'
ht-degree: 4%

---

# ドキュメントのセキュリティのために外部ブラウザーからの拡張認証を設定する {#configure-external-browser-authentication-document-security}

>[!NOTE]
>
> AEM Forms管理コンソールにアクセスするための管理者権限があることを確認します。

外部ブラウザーからの拡張認証を使用すると、AcrobatまたはReaderに組み込まれたブラウザー制御の代わりに、システムのデフォルトのweb ブラウザー（Microsoft EdgeやGoogle Chromeなど）を使用して、ポリシーで保護されたPDF ドキュメントの認証を行うことができます。 これにより、PassKey、生体認証、最新のブラウザーを必要とするその他のID プロバイダー（IDP）機能などの最新の認証方法が可能になります。

有効にすると、AcrobatまたはReaderでポリシーで保護されたドキュメントを開くと、ユーザーのデフォルトブラウザーでIDP ログインページが起動します。 認証後、ユーザーは自動的にAcrobatまたはReaderにリダイレクトされ、ドキュメントのロックが解除されます。

## 前提条件 {#prerequisites}

外部ブラウザー認証を設定する前に、次の要件が満たされていることを確認します。

* サービスパック 6.5.25.0がデプロイされたJEE上のAEM Forms 6.5、またはサポートされているアプリケーションサーバー（JBoss、WebLogic、またはWebSphere）にインストールされた該当するJEE ホットフィックスパッチを含むサービスパック 6.5.24.0。 AEM Forms JEE Hotfix2 6.5.24.0[&#128279;](#software-distribution-links)の ソフトウェア配布リンクを参照してください。
* 拡張認証（サードパーティ認証）は既に有効になっており、IDPで機能します。 [&#x200B; サーバー設定](/help/forms/using/admin-help/configuring-client-server-options.md#server-configuration-settings)および[拡張認証プロバイダーの追加](/help/forms/using/admin-help/configuring-client-server-options.md#add-the-extended-authentication-provider)を参照してください。
* クライアントにインストールされたAdobe Acrobat ProまたはAdobe Acrobat Reader（64 ビット）最新のアップデートが適用されたWindows PC

### AEM Forms JEE ホットフィックス 2 6.5.24.0のソフトウェア配布リンク {#software-distribution-links}

外部ブラウザー認証は、JEE サービスパック 6.5.25.0以降のAEM Formsで利用できます。

JEE サービスパック 6.5.24.0以前のAEM Formsを使用している場合は、次のいずれかの操作を行います。

* JEE サービスパック 6.5.25.0[&#128279;](https://experience.adobe.com/#/downloads/content/software-distribution/jp/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/servicepack/aem-service-pkg-6.5.25.0.zip)のAEM Formsにアップグレードします。
* 以下のリンクを使用して、アプリケーションサーバーとプラットフォーム用のAEM Forms JEE ホットフィックス 6.5.24.0 パッチをインストールします。

お使いのプラットフォームのAEM Forms JEE ホットフィックス 6.5.24.0 パッチを[Adobe ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/ja/aem.html)からダウンロードしてインストールします。

**JBoss**

* Windows: [Windows for JBoss JEE サーバー](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-02/jboss/adobe-aem-forms-jee-hotfix2-6.5.24.0-win-jboss.zip)のAEM Service Pack 6.5.24.0のホットフィックス
* Linux: [JBoss JEE サーバー用Linux上のAEM サービスパック 6.5.24.0のホットフィックス &#x200B;](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-02/jboss/adobe-aem-forms-jee-hotfix2-6.5.24.0-linux-jboss.tar.gz)

**WebSphere**

* Windows: WebSphere JEE サーバー[&#128279;](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-02/websphere/adobe-aem-forms-jee-hotfix2-6.5.24.0-win-websphere.zip)のWindows上のAEM Service Pack 6.5.24.0のホットフィックス
* Linux: [WebSphere JEE サーバー用Linux上のAEM Service Pack 6.5.24.0のホットフィックス &#x200B;](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-02/websphere/adobe-aem-forms-jee-hotfix2-6.5.24.0-linux-websphere.tar.gz)

**WebLogic**

* Windows: WebLogic JEE サーバー[&#128279;](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-02/weblogic/adobe-aem-forms-jee-hotfix2-6.5.24.0-win-weblogic.zip)のWindows上のAEM Service Pack 6.5.24.0のホットフィックス
* Linux: [WebLogic JEE サーバー用Linux上のAEM サービスパック 6.5.24.0のホットフィックス &#x200B;](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-24-0-hotfix-02/weblogic/adobe-aem-forms-jee-hotfix2-6.5.24.0-linux-weblogic.tar.gz)

インストール手順については、[JEE パッチのインストール &#x200B;](/help/release-notes/jee-patch-installer-65.md)を参照してください。

## 外部ブラウザー認証を有効にする {#enable-external-browser-authentication}

このビデオでは、AEM Forms Document Security サーバーで外部ブラウザー認証を有効にする方法を説明します。

>[!VIDEO](https://video.tv.adobe.com/v/3492357/)

1. 管理コンソールで、**サービス** > **Document Security** > **Configuration** > **Server Configuration**&#x200B;をクリックします。
1. 「**Adobe クライアントアプリケーションの外部ブラウザーからの拡張認証を許可する**」セクションを見つけます。
1. 有効にする各Adobe クライアントプラットフォームのチェックボックスをオンにします。
   * **Adobe AcrobatとReader （64 ビット） – デスクトップ**
   * **Adobe Acrobat Reader （32 ビット） – デスクトップ**
1. 「**OK**」をクリックします。

サーバー設定の説明については、[&#x200B; サーバー設定](/help/forms/using/admin-help/configuring-client-server-options.md#server-configuration-settings)を参照してください。

<!--
## Client configuration (Acrobat / Reader) {#client-configuration}

External browser authentication is enabled by default in Acrobat and Reader. No client-side configuration is needed for most deployments. When the server is configured to allow external browser authentication, the client uses it automatically.

To disable external browser authentication on specific client machines (forcing the embedded browser fallback), set the following registry value:

`HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Adobe\Adobe Acrobat\<product_branch>\FeatureLockDown\EDC`

| Setting | Value |
| ------- | ----- |
| Value name | `TPExternalBrowserAuthAdmin` |
| Value type | `REG_DWORD` |
| Value data | `0` (to disable) |

>[!NOTE]
>
> Both the server-side setting and the client-side preference must be enabled for external browser authentication to work. If either is disabled, the client falls back to the embedded browser.
-->

## 検証 {#verification}

このビデオでは、外部ブラウザー認証を検証する方法を説明します。Acrobatでポリシーで保護されたPDFを開き、デフォルトのブラウザーからログインし、認証後にドキュメントのロック解除を確認します。

>[!VIDEO](https://video.tv.adobe.com/v/3492356/)

1. Document Security サーバーを使用して、ポリシーで保護されたPDF ドキュメントを作成します。
1. Windows クライアントコンピューターで、保護されたPDFをAcrobat ProまたはAcrobat Readerで開きます。
1. Acrobatに同意ダイアログが表示されます。 「**ログイン**」をクリックします。
1. システムのデフォルトブラウザーがIDP ログインページで開くことを確認します。
1. 完全認証：
1. 保護されたドキュメントが正常に開くことを確認します。

## トラブルシューティング {#troubleshooting}

### システムブラウザーではなく、埋め込まれたブラウザーが開きます {#embedded-browser-opens-instead-of-system-browser}

* サーバーで外部ブラウザー認証が有効になっていることを確認します。 [外部ブラウザー認証を有効にする](#enable-external-browser-authentication)を参照してください。
* AcrobatまたはReaderのバージョンがこの機能をサポートしていることを確認します。

### 認証はブラウザーで成功しますが、ドキュメントのロックが解除されません {#authentication-succeeds-but-document-does-not-unlock}

* AcrobatまたはReaderが動作しており、ファイアウォールまたはセキュリティソフトウェアによってブロックされていないことを確認します。
* 問題が解決しない場合は、AcrobatまたはReaderのインストールを再インストールまたは修復して、プロトコルハンドラーの登録を復元します。

### 「ログインできませんでした」というメッセージがAcrobatに表示される {#we-couldnt-sign-you-in-message}

* ユーザーが認証を完了するのに時間がかかりすぎている可能性があります。 もう一度やり直してください。
* ブラウザーとAEM Forms サーバー間のネットワーク接続を確認します。

### 認証オプションがログインページに表示されない {#authentication-option-does-not-appear}

* 認証方法とオプションは、AEM FormsやAcrobatではなく、IDPによって設定されます。 IDPが、使用する認証方法をサポートしていることを確認します。
* ログインページがシステムブラウザー（埋め込みブラウザーではなく）に読み込まれていることを確認します。
