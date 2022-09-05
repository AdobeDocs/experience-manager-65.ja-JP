---
title: メールサービスの OAuth2 サポート
description: 'メールサービスの Oauth2 サポート  '
source-git-commit: 081b0c70ceca0502cb84d7e1b68b0b12dc45a4e7
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 47%

---

# メールサービスの OAuth2 サポート {#oauth2-support-for-the-mail-service}

AEM as a Cloud Service は、組織が安全な電子メール要件に準拠できるように、Oauth2 の統合メールサービスをサポートしています。

Oauth は複数のメールプロバイダーに対して設定できます。Microsoft Office 365 Outlook で Oauth2 による認証を行うように AEM メールサービスを設定する手順を以下に示します。他のベンダーも同様の方法で設定できます。

## Microsoft Outlook {#microsoft-outlook}

1. [https://portal.azure.com/](https://portal.azure.com/)に移動し、ログインします。
1. 検索バーで **Azure Active Directory** を検索し、結果をクリックします。または、[https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) を直接参照することもできます。
1. **アプリの登録**／**新しい登録**&#x200B;をクリックします。

   ![](/help/forms/using/assets/outh_outlook.PNG)

1. 必要に応じて情報を入力し、**登録**&#x200B;をクリックします。
1. 新しく作成されたアプリに移動し、**API 権限**&#x200B;を選択します。
1. **権限を追加**／**グラフ権限**／**委任権限**&#x200B;に移動します。
1. アプリに対して以下の権限を選択し、「**権限を追加**」をクリックします。
   * `SMTP.Send`
   * `Mail.Read`
   * `Mail.Send`
   * `openid`
   * `offline_access`
1. **認証**／**プラットフォームを追加** ／**Web**&#x200B;に移動し、**リダイレクト URL**&#x200B;セクションで、次の URL を追加します（スラッシュありで 1 つとスラッシュなしで 1 つ）。
   * `http://localhost/`
   * `http://localhost`
1. 各 URL を追加した後で「**設定**」を押し、必要に応じて設定を指定します
1. 次へ、に移動します。 **証明書と秘密鍵**&#x200B;をクリックし、 **新しいクライアント秘密鍵** をクリックし、画面に表示される手順に従って秘密鍵を作成します。 このシークレットは後で使用するため、必ずメモしてください
1. 押す **概要** をクリックし、 **アプリケーション（クライアント） ID** 後で使用する場合。

まとめると、AEM側で Mail サービスの OAuth2 を設定するには、次の情報が必要です。

* 次の形式の認証 URL: `https://login.microsoftonline.com/<ID>/oauth2/v2.0/authorize`
* フォームのトークン URL: `https://login.microsoftonline.com/<ID>/oauth2/v2.0/token`
* フォームの更新 URL: `https://login.microsoftonline.com/<ID>/oauth2/v2.0/token`
* クライアント ID
* クライアント秘密鍵

### 更新トークンの生成 {#generating-the-refresh-token}

次に、次の手順で示すように、更新トークンを生成する必要があります。

これは、次の手順で行います。

1. 置き換えた後、ブラウザーで次の URL を開きます `clientID` アカウントに固有の値を使用：

   ```https://login.microsoftonline.com/common/oauth2/v2/authorize?client_id=<client_id>&scope=IMAP.AccessAsUser.A;;%20POP.AccessAsUser.All%20SMTP.Send%20User.Read&response_type=code&redirect-uri=http://loginmicrosoftonline.com/common/outh2/nativeclient&prompt=login```

1. 必要な場合は、許可を許可します。
1. URL は、新しい場所にリダイレクトされます。この場所は次の形式で構成されます。`http://localhost/?code=<code>&state=12345&session_state=4f984c6b-cc1f-47b9-81b2-66522ea83f81#`
1. 上記の例の `<code>` の値をコピーします
1. 次の cURL コマンドを使用して、 refreshToken を取得します。clientID、clientSecret をアカウントの値との値に置き換えます。 `<code>`:

   ```
   curl -H “ContentType application/x-www-form-urlencoded” -d 
   "client_id=<client-id>
   &scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All&code=M.R3_BAY.1bf609bf-25b3-2fcd-d910-02e02c53bc
   &grant_type=authorization_code
   &redirect_uri= https://login.microsoftonline.com/common/oauth2/nativeclient
   &client_secret=~1E8Q~cz-m6vgOb9m~SI.eF9jSVTbFUiP5f0” -X POST https://login.microsoftonline.com/common/oauth2/v2.0/token
   ```

1. refreshToken と accessToken をメモしておきます。

### トークンの検証 {#validating-the-tokens}

AEM 側で Oauth を設定する前に、次の手順で accessToken と refreshToken の両方を検証してください。

1. 前の手順で生成した refreshToken を使用して accessToken を生成します。次の curl を使用してこれを実現し、 `<client_id>`,`<client_secret>` と `<refreshToken>`:

   ```
   curl -H “ContentType application/x-www-form-urlencoded” -d 
   "client_id=<client_id>
   &scope=https%3A%2F%2Foutlook.office.com%2FIMAP.AccessAsUser.All&code=<code>
   &grant_type=authorization_code
   &redirect_uri= https://login.microsoftonline.com/common/oauth2/nativeclient
   &client_secret=<client_secret>
   &refresh_token=<refresh_token” 
   -X POST https://login.microsoftonline.com/common/oauth2/v2.0/token
   ```

1. accessToken を使用してメールを送信し、正しく機能しているかどうかを確認します。

>[!NOTE]
>
> [この場所](https://docs.microsoft.com/ja-jp/azure/active-directory/develop/v2-oauth2-auth-code-flow)から Postman API コレクションを取得できます。

### Auth2.0 サポートを使用した電子メールサービスの設定 {#configureemailservice}

次に、Admin UI でログインして、最新の JEE サーバーで電子メールサービスを設定する必要があります。

1. に移動します。 **ホーム** - **サービス** - **アプリケーションとサービス** - **サービス管理** - **電子メールサービス**
1. **設定 Email サービス** ウィンドウが表示され、設定 **SMPT** および **IMP** 基本認証用のサーバー。
1. Outlook メール認証サービスを有効にするには、[ ] をクリックします。 **oAuth 2.0 認証設定** チェックボックス。
1. 次の値をコピー： **クライアント ID** および **クライアント秘密鍵** Azure Portal から。
1. 生成されたの値をコピー **更新トークン**.
1. クリック **保存** 詳細を保存します。
1. Workbench にログインして検索 **Email 1.0** から **アクティビティピッカー**.
1. Email 1.0 では、次の 3 つのオプションを使用できます。
   * **ドキュメントと共に送信**:添付ファイルが 1 つだけの電子メールを送信します。
   * **添付ファイルのマップと共に送信**:複数の添付ファイルを含む電子メールを送信します。
   * **受信**:POP3 または IMAP から電子メールを受信します。
1. 「 」を選択してアプリケーションをテストする **ドキュメントと共に送信**
1. 提供 **宛先** および **送信者** アドレス。
1. アプリケーションを呼び出し、oAuth2.0 認証を使用して電子メールを送信します。

>[!NOTE]
>
> Auth 2.0 認証設定を、ワークベンチの特定のプロセスに対する基本認証に変更する場合は、 **oAuth2.0 認証** 下のチェックボックス **グローバル設定を使用** 内 **接続設定** タブをクリックします。

### トラブルシューティング {#troubleshooting}

メールサービスが正しく動作していない場合は、 `refreshToken` 上記のように。 新しい値がデプロイされるまで数分かかります。


