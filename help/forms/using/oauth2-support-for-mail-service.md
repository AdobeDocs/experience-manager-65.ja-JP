---
title: Microsoft® Office 365 メールサーバープロトコルの OAuth2 サポート
description: Microsoft® Office 365 メールサーバープロトコルの OAuth2 サポート
source-git-commit: 85189a4c35d1409690cbb93946369244e8848340
workflow-type: tm+mt
source-wordcount: '940'
ht-degree: 3%

---

# Microsoft® Office 365 メールサーバープロトコルの OAuth 2.0 サポート {#oauth2-support-for-the-microsoft-mail-server-protocols}

AEM Formsでは、組織が安全な電子メール要件に準拠できるように、Microsoft® Office 365 メールサーバープロトコルとの統合に対して OAuth 2.0 のサポートを提供しています。 Azure Active Directory (Azure AD) は、OAuth 2.0 認証サービスを提供します。このサービスを使用すると、IMAP、POP、SMTP などの様々なプロトコルとの接続や、Office 365 ユーザーの電子メールデータへのアクセスが可能になります。

OAuth 2.0 サービスを介して認証するMicrosoft® Office 365 メールサーバープロトコルを設定する手順を以下に示します。

1. ログイン [https://portal.azure.com/](https://portal.azure.com/) およびを検索します。 **Azure Active Directory** 検索バーで、結果をクリックします。
または、[https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) を直接参照することもできます。
1. クリック **追加** > **アプリの登録** > **新規登録**

   ![アプリ登録](/help/forms/using/assets/outh_outlook_microsoft_azure.png)

1. 必要に応じて情報を入力し、「 **登録**.
   ![サポートされているアカウント](/help/forms/using/assets/azure_suuportedaccountype.png)


   上記の場合、 **任意の組織ディレクトリ（任意の Azure AD ディレクトリ — マルチテナント）および個人用のMicrosoft®アカウント（Skype、Xbox など）のアカウント** 」オプションが選択されている。

   >[!NOTE]
   >
   > * の場合 **任意の組織ディレクトリ（任意の Azure AD ディレクトリ — マルチテナント）のアカウント** アプリケーションの場合は、個人の電子メールアカウントではなく、勤務先アカウントを使用することをお勧めします。
   > * **個人用Microsoft®アカウントのみ** および **シングルテナント** アプリケーションはサポートされていません。
   > * 次を使用することをお勧めします。 **マルチテナントおよび個人用Microsoft®アカウント** アプリケーション。


1. 次へ、に移動します。 **証明書と秘密鍵**&#x200B;をクリックし、 **新しいクライアント秘密鍵** をクリックし、画面に表示される手順に従って秘密鍵を作成します。 後で使用するために、このシークレットの値を必ずメモしておきます。

   ![秘密鍵](/help/forms/using/assets/azure_secretkey.png)

1. 権限を追加するには、新しく作成されたアプリに移動し、を選択します。 **API 権限** > **権限を追加** > **Microsoft® Graph** > **委任された権限**
1. アプリの以下の権限のチェックボックスをオンにして、「 」をクリックします。 **権限を追加**:

   * `IMAP.AccessUser.All`
   * `Mail.Read`
   * `offline_access`
   * `POP.AccessAsUser.All`
   * `SMTP.Send`
   * `User.Read`

   ![API 権限](/help/forms/using/assets/azure_apipermission.png)

1. 選択 **認証** > **プラットフォームの追加** > **Web**、および **リダイレクト URL** セクションで、以下の URI(Universal Resource Identifier) のいずれかを次のように追加します。
   * `https://login.microsoftonline.com/common/oauth2/nativeclient`
   * `http://localhost`

   この場合、 `https://login.microsoftonline.com/common/oauth2/nativeclient` はリダイレクト URI として使用されます。

1. クリック **設定** 各 URL を追加し、必要に応じて設定をおこなった後で、
   ![リダイレクト URI](/help/forms/using/assets/azure_redirecturi.png)

   >[!NOTE]
   >
   > 選択が必須です。 **アクセストークン** および **ID トークン** チェックボックス。

1. クリック **概要** をクリックし、 **アプリケーション（クライアント） ID**, **ディレクトリ（テナント） ID**、および **クライアント秘密鍵** 後で使用する場合。

   ![概要](/help/forms/using/assets/azure_overview.png)

## 認証コードの生成 {#generating-the-authorization-code}

次に、次の手順で説明する認証コードを生成する必要があります。

1. 置き換えた後、ブラウザーで次の URL を開きます `clientID` と `<client_id>` および `redirect_uri` アプリケーションのリダイレクト URI を使用して、以下の設定をおこないます。

   ```https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=[clientid]&scope=IMAP.AccessAsUser.All%20POP.AccessAsUser.All%20SMTP.Send%20User.Read%20Mail.Read%20offline_access&response_type=code&redirect_uri=[redirect_uri]&prompt=login```

1. 上記の URL を入力すると、ログイン画面にリダイレクトされます。
   ![ログイン画面](/help/forms/using/assets/azure_loginscreen.png)

1. E メールを入力し、「 **次へ** アプリの権限画面が表示されます。

   ![許可権限](/help/forms/using/assets/azure_permission.png)

1. 権限を許可すると、次のような新しい URL にリダイレクトされます。 `https://login.microsoftonline.com/common/oauth2/nativeclient?code=<code>&session_state=[session_id]`

1. 次の値をコピー： `<code>` 上記の URL から `0.ASY...` から `&session_state` 上記の URL 内に入力します。

## 更新トークンの生成 {#generating-the-refresh-token}

次に、次の手順で説明する更新トークンを生成する必要があります。
1. コマンドプロンプトを開き、次の cURL コマンドを使用して refreshToken を取得します。
1. を `clientID`, `client_secret` および `redirect_uri` と、 `<code>`:

   `curl -H “ContentType application/x-www-form-urlencoded” -d “client_id=[client-id]&scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FPOP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office.com%2FUser.Read%20https%3A%2F%2Foutlook.office.com%2FMail.Read%20offline_access&code=[code]&grant_type=authorization_code&redirect_uri=[redirect_uri]&client_secret=[secretkey_value]” -X POST https://login.microsoftonline.com/common/oauth2/v2.0/token`

1. 更新トークンをメモしておきます。

## OAuth 2.0 サポートを使用した電子メールサービスの設定 {#configureemailservice}

次に、Admin UI でログインして、最新の JEE サーバーで電子メールサービスを設定する必要があります。

1. に移動します。 **ホーム** > **サービス** > **アプリケーションとサービス** > **サービス管理** > **電子メールサービス**、 **設定 Email サービス** ウィンドウが表示され、基本認証用に設定されます。

   >[!NOTE]
   >
   > oAuth 2.0 認証サービスを有効にするには、 **SMTP サーバーが認証（SMTP 認証）を必要とするかどうか** チェックボックス。

1. 設定 **oAuth 2.0 認証設定** as `True`.
1. 次の値をコピー： **クライアント ID** および **クライアント秘密鍵** Azure Portal から。
1. 生成されたの値をコピー **更新トークン**.
1. にログイン **Workbench** および検索 **Email 1.0** から **アクティビティピッカー**.
1. Email 1.0 では、次の 3 つのオプションを使用できます。
   * **ドキュメントと共に送信**:添付ファイルが 1 つだけの電子メールを送信します。
   * **添付ファイルのマップと共に送信**:複数の添付ファイルを含む電子メールを送信します。
   * **受信**:IMAP から電子メールを受信します。

   >[!NOTE]
   >
   >* Transport Security プロトコルの有効な値は次のとおりです。&#39;blank&#39;、&#39;SSL&#39;または&#39;TLS&#39;。 値を **SMTP Transport Security** および **トランスポートセキュリティを受信** から **TLS** oAuth 認証サービスを有効にする場合。
   >* **POP3 プロトコル** は、OAuth ではサポートされていません。


   ![接続設定](/help/forms/using/assets/oauth_connectionsettings.png)

1. 「 」を選択してアプリケーションをテストする **ドキュメントと共に送信**.
1. 提供 **宛先** および **送信者** アドレス。
1. アプリケーションを呼び出し、0Auth 2.0 認証を使用して電子メールを送信します。

   >[!NOTE]
   >
   >Auth 2.0 認証設定を、Workbench の特定のプロセスに対する基本認証に変更する場合は、 **OAuth 2.0 認証** の下の値が「False」 **グローバル設定を使用** 内 **接続設定** タブをクリックします。

## OAuth タスク通知を有効にするには {#enable_oauth_task}

1. に移動します。 **ホーム** > **サービス** > **フォームワークフロー** > **サーバー設定** > **メール設定**
1. OAuth タスクの通知を有効にするには、 **OAuth を有効にする** チェックボックス。
1. 次の値をコピー： **クライアント ID** および **クライアント秘密鍵** Azure Portal から。
1. 生成されたの値をコピー **更新トークン**.
1. クリック **保存** 詳細を保存します。

   ![タスク通知](/help/forms/using/assets/task_notification.png)

   >[!NOTE]
   >
   > タスク通知に関する詳細を知るには、 [ここをクリック](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/manage-endpoints/configuring-email-endpoints.html#create-an-email-endpoint-for-the-complete-task-service).

## 電子メールエンドポイントを設定するには {#configure_email_endpoint}

1. に移動します。 **ホーム** > **サービス** > **アプリケーションとサービス** > **エンドポイント管理**
1. 電子メールエンドポイントを設定するには、 **oAuth 2.0 認証設定** as `True`.
1. 次の値をコピー： **クライアント ID** および **クライアント秘密鍵** Azure Portal から。
1. 生成されたの値をコピー **更新トークン**.
1. クリック **保存** 詳細を保存します。

   ![接続設定](/help/forms/using/assets/oauth_emailendpoint.png)

   >[!NOTE]
   >
   > 電子メールエンドポイントの設定に関する詳細は、 [電子メールエンドポイントの設定](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/manage-endpoints/configuring-email-endpoints.html).

## トラブルシューティング {#troubleshooting}

* 電子メールサービスが正しく動作していない場合。 を再生成してください `Refresh Token` 上記のように。 新しい値がデプロイされるまで数分かかります。

* Workbench を使用して電子メールエンドポイントで電子メールサーバーの詳細を設定中にエラーが発生しました。Workbench の代わりに Admin UI を使用してエンドポイントを設定してみてください。






