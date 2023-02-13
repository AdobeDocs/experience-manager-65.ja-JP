---
title: Microsoft® Office 365 メールサーバープロトコルの OAuth2 ベース認証の設定
description: Microsoft® Office 365 メールサーバープロトコルの OAuth2 ベース認証の設定
exl-id: cd3da71f-892c-4fde-905f-71a64fb5d4e4
source-git-commit: 4df6be3206cd4b64dbaf14607bfdcec549117091
workflow-type: ht
source-wordcount: '938'
ht-degree: 100%

---

# Microsoft® Office 365 メールサーバープロトコルとの統合 {#oauth2-support-for-the-microsoft-mail-server-protocols}

組織が安全なメールの要件に準拠できるように、AEM Forms では、Microsoft® Office 365 メールサーバープロトコルとの統合のために OAuth 2.0 をサポートしています。Azure Active Directory（Azure AD）OAuth 2.0 認証サービスを使用して、IMAP、POP、SMTP などの様々なプロトコルと接続し、Office 365 ユーザーのメールデータにアクセスできます。OAuth 2.0 サービスを介して認証するように Microsoft® Office 365 メールサーバープロトコルを設定する手順を以下に示します。

1. [https://portal.azure.com/](https://portal.azure.com/) にログインし、検索バーで **Azure Active Directory** を検索して、結果をクリックします。または、[https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) を直接参照することもできます。
1. **追加**／**アプリの登録**／**新しい登録**&#x200B;をクリックします。

   ![アプリの登録](/help/forms/using/assets/outh_outlook_microsoft_azure.png)

1. 必要に応じて情報を入力し、「**登録**」をクリックします。
   ![サポートされているアカウント](/help/forms/using/assets/azure_suuportedaccountype.png)
上記の場合、 
「**任意の組織ディレクトリ（任意の Azure AD ディレクトリ - マルチテナント）内のアカウントおよび個人用の Microsoft® アカウント（Skype、Xbox など）**」オプションが選択されています。

   >[!NOTE]
   >
   > * **任意の組織ディレクトリ（任意の Azure AD ディレクトリ - マルチテナント）内のアカウント**&#x200B;の場合、個人用のメールアカウントではなく、職場アカウントを使用することをお勧めします。
   > * **個人用の Microsoft® アカウントのみ**&#x200B;および&#x200B;**シングルテナント**&#x200B;アプリケーションはサポートされていません。
   > * **マルチテナントおよび個人用の Microsoft® アカウント**&#x200B;アプリケーションを使用することをお勧めします。


1. 次に、**証明書とシークレット**&#x200B;に移動し、「**新しいクライアントシークレット**」をクリックし、画面上の手順に従ってシークレットを作成します。このシークレットは後で使用するので、必ずメモしてください。

   ![秘密鍵](/help/forms/using/assets/azure_secretkey.png)

1. 権限を追加するには、新しく作成したアプリに移動し、**API 権限**／ **権限を追加**／**Microsoft® Graph**／**デリゲートされた権限**&#x200B;を選択します。
1. アプリの以下の権限のチェックボックスをオンにして、「**権限を追加**」をクリックします。

   * `IMAP.AccessUser.All`
   * `Mail.Read`
   * `offline_access`
   * `POP.AccessAsUser.All`
   * `SMTP.Send`
   * `User.Read`

   ![API 権限](/help/forms/using/assets/azure_apipermission.png)

1. **認証**／**プラットフォームを追加**／**Web** を選択し、「**リダイレクト URL**」セクションで、以下の URI（Universal Resource Identifier）のいずれかを次のように追加します。
   * `https://login.microsoftonline.com/common/oauth2/nativeclient`
   * `http://localhost`

   この場合、`https://login.microsoftonline.com/common/oauth2/nativeclient` はリダイレクト URI として使用されます。

1. 各 URL を追加した後で「**設定**」をクリックし、要件に従って設定を指定します。
   ![リダイレクト URI](/help/forms/using/assets/azure_redirecturi.png)

   >[!NOTE]
   >
   > 「**アクセストークン**」チェックボックスと「**ID トークン**」チェックボックスを選択する必要があります。

1. 左側のパネルで「**概要**」をクリックし、後で使用するために、**アプリケーション (クライアント) ID**、**ディレクトリ (テナント) ID** および&#x200B;**クライアントシークレット**&#x200B;の値をコピーします。

   ![概要](/help/forms/using/assets/azure_overview.png)

## 認可コードの生成 {#generating-the-authorization-code}

次に、以下の手順で説明する認可コードを生成する必要があります。

1. `clientID` を `<client_id>` に、`redirect_uri` をアプリケーションのリダイレクト URI に置き換えた後、次の URL をブラウザーで開きます。

   ```https://login.microsoftonline.com/common/oauth2/v2.0/authorize?client_id=[clientid]&scope=IMAP.AccessAsUser.All%20POP.AccessAsUser.All%20SMTP.Send%20User.Read%20Mail.Read%20offline_access&response_type=code&redirect_uri=[redirect_uri]&prompt=login```

1. 上記の URL を入力すると、ログイン画面にリダイレクトされます。
   ![ログイン画面](/help/forms/using/assets/azure_loginscreen.png)

1. メールアドレスを入力し、「**次へ**」をクリックすると、アプリの権限画面が表示されます。

   ![権限の許可](/help/forms/using/assets/azure_permission.png)

1. 権限を許可すると、`https://login.microsoftonline.com/common/oauth2/nativeclient?code=<code>&session_state=[session_id]` のような新しい URL にリダイレクトされます。

1. 上記 URL の `<code>` の値を上記 URL の `0.ASY...` から `&session_state` にコピーします。

## 更新トークンの生成 {#generating-the-refresh-token}

次に、次の手順で説明する更新トークンを生成する必要があります。

1. コマンドプロンプトを開き、次の cURL コマンドを使用して refreshToken を取得します。

1. `clientID`、`client_secret` および `redirect_uri` をアプリケーションの値と `<code>` の値に置き換えます。

   `curl -H “ContentType application/x-www-form-urlencoded” -d “client_id=[client-id]&scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FPOP.AccessAsUser.All%20https%3A%2F%2Foutlook.office.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office.com%2FUser.Read%20https%3A%2F%2Foutlook.office.com%2FMail.Read%20offline_access&code=[code]&grant_type=authorization_code&redirect_uri=[redirect_uri]&client_secret=[secretkey_value]” -X POST https://login.microsoftonline.com/common/oauth2/v2.0/token`

1. 更新トークンをメモしておきます。

## OAuth 2.0 をサポートするメールサービスの設定 {#configureemailservice}

ここで、管理 UI にログインして、最新の JEE サーバーでメールサービスを設定する必要があります。

1. **ホーム**／**サービス**／**アプリケーションとサービス**／**サービス管理**／**メールサービス**&#x200B;に移動すると、基本認証用に設定された&#x200B;**メールサービス設定**&#x200B;ウィンドウが表示されます。

   >[!NOTE]
   >
   > OAuth 2.0 認証サービスを有効にするには、「**SMTP サーバーが認証を必要とするかどうか (SMTP 認証)**」チェックボックスをオンにする必要があります。

1. 「**OAuth 2.0 認証設定**」を `True` に設定します。
1. **クライアント ID** と&#x200B;**クライアントシークレット**&#x200B;の値を Azure Portal からコピーします。
1. 生成された&#x200B;**更新トークン**&#x200B;の値をコピーします。
1. **Workbench** にログインし、**アクティビティピッカー**&#x200B;から **Email 1.0** を検索します。
1. Email 1.0 では、次の 3 つのオプションを使用できます。
   * **ドキュメントと共に送信**：1 つの添付ファイルを含むメールを送信します。
   * **添付ファイルのマップと共に送信**：複数の添付ファイルを含むメールを送信します。
   * **受信**：IMAP からメールを受信します。

   >[!NOTE]
   >
   >* Transport Security プロトコルの有効な値は「blank」、「SSL」または「TLS」です。oAuth 認証サービスを有効にするには、**SMTP Transport Security** と **Receive Transport Security** の値を **TLS** に設定する必要があります。
   >* **POP3 プロトコル**&#x200B;は、OAuth 用にはサポートされていません。


   ![接続設定](/help/forms/using/assets/oauth_connectionsettings.png)

1. 「**ドキュメントと共に送信**」を選択してアプリケーションをテストします。
1. **TO** および **From** アドレスを提供します。
1. アプリケーションを呼び出し、OAuth 2.0 認証を使用してメールを送信します。

   >[!NOTE]
   >
   >Auth 2.0 認証設定をワークベンチの特定のプロセスに対する基本認証に変更する場合は、「**接続設定**」タブの&#x200B;**グローバル設定を使用**&#x200B;の下で、**OAuth 2.0認証**&#x200B;値を「False」に設定できます。

## OAuth タスク通知を有効にする手順は次のとおりです。 {#enable_oauth_task}

1. **ホーム**／**サービス**／**フォームワークフロー**／**サーバー設定**／**メール設定**&#x200B;に移動します。
1. OAuth タスクの通知を有効にするには、「**OAuth を有効にする**」チェックボックスを選択します。
1. Azure Portal から&#x200B;**クライアント ID** および&#x200B;**クライアント秘密鍵**&#x200B;の値をコピーします。
1. 生成された&#x200B;**更新トークン**&#x200B;の値をコピーします。
1. 「**保存**」をクリックして、詳細を保存します。

   ![タスク通知](/help/forms/using/assets/task_notification.png)

   >[!NOTE]
   >
   > タスク通知に関して詳しくは、 [ここをクリック](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/manage-endpoints/configuring-email-endpoints.html?lang=ja#create-an-email-endpoint-for-the-complete-task-service)します。

## メールのエンドポイントを設定する手順は次のとおりです。 {#configure_email_endpoint}

1. **ホーム**／**サービス**／**アプリケーションとサービス**／**エンドポイント管理**&#x200B;に移動します。
1. メールエンドポイントを設定するには、**oAuth 2.0 認証設定**&#x200B;を `True` に設定します。
1. Azure Portal から&#x200B;**クライアント ID** および&#x200B;**クライアント秘密鍵**&#x200B;の値をコピーします。
1. 生成された&#x200B;**更新トークン**&#x200B;の値をコピーします。
1. 「**保存**」をクリックして、詳細を保存します。

   ![接続設定](/help/forms/using/assets/oauth_emailendpoint.png)

   >[!NOTE]
   >
   > メールエンドポイントの設定に関する詳細は、[メールエンドポイントの設定](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/manage-endpoints/configuring-email-endpoints.html?lang=ja)をクリックします。

## トラブルシューティング {#troubleshooting}

* メールサービスが正しく動作していない場合。上記のように `Refresh Token` を再生成してください。 新しい値がデプロイされるまで数分かかります。

* ワークベンチを使用してメールエンドポイントでメールサーバーの詳細を設定中に、エラーが発生しました。ワークベンチの代わりに管理 UI を使用してエンドポイントを設定してみてください。
