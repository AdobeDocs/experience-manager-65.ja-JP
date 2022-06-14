---
title: 電子メール通知の設定
seo-title: Configuring Email Notification
description: AEM で電子メール通知を設定する方法について説明します。
seo-description: Learn how to configure Email Notification in AEM.
uuid: 6cbdc312-860b-4a69-8bbe-2feb32204a27
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 6466d7b8-e308-43c5-acdc-dec15f796f64
exl-id: 918fcbbc-a78a-4fab-a933-f183ce6a907f
source-git-commit: ea5abbbe8f928a63b7d3d6f96f3007a3c82706e0
workflow-type: tm+mt
source-wordcount: '2116'
ht-degree: 100%

---

# 電子メール通知の設定{#configuring-email-notification}

AEM は、次のようなユーザーに電子メール通知を送信します。

* 変更やレプリケーションなど、ページイベントを購読したことがある。[通知インボックス](/help/sites-classic-ui-authoring/author-env-inbox.md#subscribing-to-notifications)では、このようなイベントを購読する方法について説明します。

* フォーラムイベントを購読したことがある
* ワークフローで手順を実行する必要がある。[参加者ステップ](/help/sites-developing/workflows-step-ref.md#participant-step)では、ワークフローで電子メール通知を実行する方法について説明します。

前提条件：

* ユーザーのプロファイルで有効な電子メールアドレスが定義されている必要があります。
* **Day CQ Mail Service** が適切に設定されている必要があります。

ユーザーへの通知は、各自がプロファイルで定義している言語の電子メールで送信されます。言語ごとに、独自のカスタマイズ可能なテンプレートがあります。新しい言語用には新しい電子メールテンプレートを追加できます。

>[!NOTE]
>
>AEM を操作しているときは、このようなサービスの設定を管理する方法がいくつかあります。詳細および推奨事項については、[OSGi の設定](/help/sites-deploying/configuring-osgi.md)を参照してください。

## メールサービスの設定 {#configuring-the-mail-service}

AEM で電子メールを送信できるようにするために、**Day CQ Mail Service** を適切に設定する必要があります。設定は、Web コンソールで表示できます。AEM を操作しているときは、このようなサービスの設定を管理する方法がいくつかあります。詳細および推奨事項については、[OSGi の設定](/help/sites-deploying/configuring-osgi.md)を参照してください。

以下の制約が適用されます。

* **SMTP サーバーポート**&#x200B;は 25 以上にする必要があります。

* **SMTP サーバーホスト名**&#x200B;は空白にできません。
* **「送信元」アドレス**&#x200B;は空白にしてはなりません。

**Day CQ Mail Service** の問題をデバッグしやすくするために、サービスのログを監視できます。

`com.day.cq.mailer.DefaultMailService`

設定は、Web コンソールに次のように表示されます。

![chlimage_1-276](assets/chlimage_1-276.png)

## 電子メール通知チャネルの設定 {#configuring-the-email-notification-channel}

ページまたはフォーラムのイベント通知を購読するとき、送信元の電子メールアドレスは、デフォルトで `no-reply@acme.com` に設定されます。この値は、Web コンソールで **Notification Email Channel** サービスを設定することで変更できます。

送信元のメールアドレスを設定するには、`sling:OsgiConfig` ノードをリポジトリに追加します。以下の手順で、CRXDE Lite を使用してノードを直接追加します。

1. CRXDE Lite で、`config` という名前のノードを、アプリケーションフォルダーの下に追加します。
1. config フォルダーに、以下の名前のノードを追加します。

   `com.day.cq.wcm.notification.email.impl.EmailChannel`リソースのタイプは次のとおりとします。`sling:OsgiConfig`

1.  `String` プロパティを `email.from` という名前のノードに追加します。値には、使用するメールアドレスを指定します。

1. 「**すべて保存**」をクリックします。

次の手順を使用して、コンテンツパッケージソースフォルダーでノードを定義します。

1.  `jcr_root/apps/*app_name*/config folder` に、`com.day.cq.wcm.notification.email.impl.EmailChannel.xml` という名前のファイルを作成します。

1. このノードを表現する次の XML を追加します。

   `<?xml version="1.0" encoding="UTF-8"?> <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0" jcr:primaryType="sling:OsgiConfig" email.from="name@server.com"/>`
1. `email.from` 属性の値（`name@server.com`）を、実際の電子メールアドレスに置き換えます。

1.  ファイルを保存します。

## ワークフロー電子メール通知サービスの設定 {#configuring-the-workflow-email-notification-service}

ワークフロー電子メール通知を受信したとき、送信元電子メールアドレスとホスト URL プレフィックスはいずれもデフォルトに設定されています。これらの値は、Web コンソールで **Day CQ Workflow Email Notification Service** を設定することによって変更できます。その場合は、変更をリポジトリに保持することをお勧めします。

デフォルト設定は、Web コンソールに次のように表示されます。

![chlimage_1-277](assets/chlimage_1-277.png)

### ページ通知用の電子メールテンプレート {#email-templates-for-page-notification}

ページ通知用の電子メールテンプレートは次の場所にあります。

`/libs/settings/notification-templates/com.day.cq.wcm.core.page`

デフォルトの英語のテンプレート（`en.txt`）は次のように定義されています。

```xml
subject=[CQ Page Event Notification]: Page Event

header=-------------------------------------------------------------------------------------\n \
Time: ${time}\n \
User: ${userFullName} (${userId})\n \
-------------------------------------------------------------------------------------\n\n

message=The following pages were affected by the event: \n \
 \n \
${modifications} \n \
 \n\n
footer=\n \
-------------------------------------------------------------------------------------\n \
This is an automatically generated message. Please do not reply.
```

#### ページ通知用の電子メールテンプレートのカスタマイズ {#customizing-email-templates-for-page-notification}

ページ通知用の英語の電子メールテンプレートをカスタマイズするには：

1. CRXDE で、次のファイルを開きます。

   `/libs/settings/notification-templates/com.day.cq.wcm.core.page/en.txt`

1. ニーズに合わせてファイルを変更します。
1. 変更内容を保存します。

テンプレートには以下の書式が必要です。

```
 subject=<text_1>
 header=<text_2>
 message=<text_3>
 footer=<text_4>
```

&lt;text_x> には、静的テキストと動的文字列変数を混在させることができます。ページ通知用の電子メールテンプレート内では次の変数を使用できます。

* `${time}`、イベントの日時。

* `${userFullName}`、イベントを実行したユーザーのフルネーム。

* `${userId}`、イベントを実行したユーザーの ID。
* `${modifications}`、ページイベントのタイプとページパスを次の形式で表します。

   &lt;page event type> => &lt;page path>

   次に例を示します。

   PageModified => /content/geometrixx/ja/products

### フォーラム通知用の電子メールテンプレート {#email-templates-for-forum-notification}

フォーラム通知用の電子メールテンプレートは次の場所にあります。

`/etc/notification/email/default/com.day.cq.collab.forum`

デフォルトの英語のテンプレート（`en.txt`）は次のように定義されています。

```xml
subject=[CQ Forum Notification]

header=-------------------------------------------------------------------------------------\n \
Time: Time: ${time}\n \
Forum Page Path: ${forum.path}\n \
-------------------------------------------------------------------------------------\n\n

message=Page: ${host.prefix}${forum.path}.html\n

footer=\n \
-------------------------------------------------------------------------------------\n \
This is an automatically generated message. Please do not reply.
```

#### フォーラム通知用の電子メールテンプレートのカスタマイズ {#customizing-email-templates-for-forum-notification}

フォーラム通知用の英語の電子メールテンプレートをカスタマイズするには：

1. CRXDE で、次のファイルを開きます。

   `/etc/notification/email/default/com.day.cq.collab.forum/en.txt`

1. ニーズに合わせてファイルを変更します。
1. 変更内容を保存します。

テンプレートには以下の書式が必要です。

```
 subject=<text_1>
 header=<text_2>
 message=<text_3>
 footer=<text_4>
```

`<text_x>` には、静的なテキストと動的な文字列変数を混在させることができます。

フォーラム通知用の電子メールテンプレート内では次の変数を使用できます。

* `${time}`、イベントの日時。

* `${forum.path}`、フォーラムページのパス。

### ワークフロー通知用の電子メールテンプレート {#email-templates-for-workflow-notification}

ワークフロー通知用の電子メールテンプレート（英語）は次の場所にあります。

`/libs/settings/workflow/notification/email/default/en.txt`

次のように定義されています。

```xml
subject=Workflow notification: ${event.EventType}

header=-------------------------------------------------------------------------------------\n \
Time: ${event.TimeStamp}\n \
Step: ${item.node.title}\n \
User: ${participant.name} (${participant.id})\n \
Workflow: ${model.title}\n \
-------------------------------------------------------------------------------------\n\n

message=Content: ${host.prefix}${payload.path.open}\n

footer=\n \
-------------------------------------------------------------------------------------\n \
View the overview in your ${host.prefix}/aem/inbox\n \
-------------------------------------------------------------------------------------\n \
This is an automatically generated message. Please do not reply.
```

#### ワークフロー通知用の電子メールテンプレートのカスタマイズ {#customizing-email-templates-for-workflow-notification}

ワークフローイベント通知用の英語の電子メールテンプレートをカスタマイズするには：

1. CRXDE で、次のファイルを開きます。

   `/libs/settings/workflow/notification/email/default/en.txt`

1. ニーズに合わせてファイルを変更します。
1. 変更内容を保存します。

テンプレートには以下の書式が必要です。

```
subject=<text_1>
 header=<text_2>
 message=<text_3>
 footer=<text_4>
```

>[!NOTE]
>
>`<text_x>` には、静的なテキストと動的な文字列変数を混在させることができます。`<text_x>` 項目の各行の末尾には、最後のインスタンスを除き、バックスラッシュ（`\`）を付加する必要があります。バックスラッシュがないと、`<text_x>` 文字列変数の終了と見なされます。
>
>テンプレート形式について詳しくは、[Properties.load() メソッドの javadocs](https://docs.oracle.com/javase/8/docs/api/java/util/Properties.html#load-java.io.InputStream-) を参照してください。

メソッド `${payload.path.open}` を使用すると、作業項目のペイロードのパスが表示されます。例えば、Sites のページの場合、`payload.path.open` は `/bin/wcmcommand?cmd=open&path=…` と同じようなものです。これにサーバー名が抜けているのは、テンプレートによってプレフィックスとして `${host.prefix}` が付加されるためです。

電子メールテンプレート内では以下の変数を使用できます。

* `${event.EventType}`、イベントのタイプ。
* `${event.TimeStamp}`、イベントの日時。
* `${event.User}`、イベントをトリガーしたユーザー。
* `${initiator.home}`、イニシエーターノードのパス。

* `${initiator.name}`、イニシエーター名。

* `${initiator.email}`、イニシエーターのメールアドレス。
* `${item.id}`、作業項目の ID。
* `${item.node.id}`、この作業項目に関連付けられているワークフローモデル内のノードの ID。
* `${item.node.title}`、作業項目のタイトル
* `${participant.email}`、参加者のメールアドレス
* `${participant.name}`、参加者の名前。
* `${participant.familyName}`、参加者の姓
* `${participant.id}`、参加者の ID
* `${participant.language}`、参加者の言語
* `${instance.id}`、ワークフローの ID
* `${instance.state}`、ワークフローの状態
* `${model.title}`、ワークフローモデルのタイトル
* `${model.id}`、ワークフローモデルの ID

* `${model.version}`、ワークフローモデルのバージョン
* `${payload.data}`、ペイロード

* `${payload.type}`、ペイロードのタイプ
* `${payload.path}`、ペイロードのパス
* `${host.prefix}`、ホストのプレフィックス（例：http://localhost:4502）

### 新しい言語用の電子メールテンプレートの追加 {#adding-an-email-template-for-a-new-language}

新しい言語用のテンプレートを追加するには：

1. CRXDE で、ファイル `<language-code>.txt` を以下に追加します。

   * `/libs/settings/notification-templates/com.day.cq.wcm.core.page`：ページ通知用
   * `/etc/notification/email/default/com.day.cq.collab.forum`：フォーラム通知用
   * `/libs/settings/workflow/notification/email/default`：ワークフロー通知用

1. 言語に合わせてファイルを調整します。
1. 変更内容を保存します。

>[!NOTE]
>
>メールテンプレートのファイル名として使用される `<language-code>` は、AEM で認識できる小文字 2 文字の言語コードにする必要があります。言語コードについては、AEM は ISO-639-1 に依存しています。

## AEM Assets の電子メール通知の設定 {#assetsconfig}

AEM Assets のコレクションが共有されている場合も共有されていない場合も、AEM から電子メール通知を受信できます。電子メール通知を設定するには、次の手順に従います。

1. [メールサービスの設定](/help/sites-administering/notification.md#configuring-the-mail-service)で説明したように、電子メールサービスを設定します。
1. AEM に管理者としてログインします。**ツール**／**操作**／**Web コンソール**&#x200B;をクリックして、Web コンソール設定を開きます。
1. **Day CQ DAM Resource Collection Servlet** を編集します。「**send email**」を選択します。「**保存**」をクリックします。

## OAuth の設定 {#setting-up-oauth}

AEM は、組織が安全なメール要件に準拠できるように、Oauth2 の統合メーラーサービスをサポートしています。

以下に示すように、複数のメールプロバイダーに対して OAuth を設定できます。

>[!NOTE]
>
>この手順は、公開インスタンスの例です。オーサーインスタンスでメール通知を有効にするには、オーサー上で同じ手順を実行する必要があります。

### Gmail {#gmail}

1. `https://console.developers.google.com/projectcreate` でプロジェクトを作成 
1. プロジェクトを選択し、**API とサービス**／**ダッシュボード - 資格情報**&#x200B;に移動します。
1. 必要に応じて OAuth 同意画面を設定する
1. 次の更新画面で、これらの 2 つの範囲を追加します。
   * `https://mail.google.com/`
   * `https://www.googleapis.com//auth/gmail.send`
1. 範囲を追加したら、左側のメニューで&#x200B;**資格情報**&#x200B;に戻り、 **資格情報を作成**／**OAuth クライアント ID**／**デスクトップアプリ**&#x200B;に移動します。
1. 新しいウィンドウが開き、クライアント ID とクライアント秘密鍵が表示されます。
1. これらの資格情報を保存します。

**AEM 側の設定**

>[!NOTE]
>
>Adobe Managed Service をご利用のお客様は、顧客サービスエンジニアと協力して、これらの変更を本番環境に加えることができます。

まず、メールサービスを設定します。

1. `http://serveraddress:serverport/system/console/configMgr` に移動して、AEM web コンソールを開きます
1. **Day CQ Mail Service** を探して、クリックします。
1. 次の設定を追加します。
   * SMTP サーバーのホスト名: `smtp.gmail.com`
   * SMTP サーバーポート：`25` または `587`（要件に応じて）
   * 「**SMPT で StarTLS を使用**」および「**SMTP には StarTLS が必要**」のチェックボックスをオンにします。
   * **OAuth フロー** をチェックし、「**保存**」をクリックします。

次に、以下の手順に従って、SMTP OAuth プロバイダーを設定します。

1. `http://serveraddress:serverport/system/console/configMgr` に移動して、AEM web コンソールを開きます。
1. **CQ Mailer SMTP OAuth2 Provider** を探して、クリックします。
1. 必要な情報を以下のとおり入力します。
   * 認証 URL：`https://accounts.google.com/o/oauth2/auth`
   * トークン URL：`https://accounts.google.com/o/oauth2/token`
   * 範囲：`https://www.googleapis.com/auth/gmail.send` および `https://mail.google.com/`。複数の範囲を追加するには、設定された各範囲の右側にある「**+**」ボタンをクリックします。
   * クライアント ID とクライアント秘密鍵：上記の段落で取得した値を使用して、これらのフィールドを設定します。
   * 更新トークン URL: `https://accounts.google.com/o/oauth2/token`
   * 更新トークンの有効期限：なし
1. 「**保存**」をクリックします。

<!-- clarify refresh token expiry, currrently not present in the UI -->

設定が完了すると、設定は次のようになります。

![OAuth SMTP プロバイダー](assets/oauth-smtpprov2.png)

次に、OAuth コンポーネントをアクティベートします。手順は次のとおりです。

1. URL：`http://serveraddress:serverport/system/console/components` にアクセスして、コンポーネントコンソールに移動します。
1. 以下のコンポーネントを探します
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeGenerateServlet`
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeAccessTokenGenerator`
1. コンポーネントの左側にある「再生」アイコンを押します。

   ![components](assets/oauth-components-play.png)

最後に、以下により設定を確認します。

1. 公開インスタンスのアドレスに移動し、管理者としてログインします。
1. ブラウザーで新しいタブを開き、`http://serveraddress:serverport/services/mailer/oauth2/authorize` に移動します。これにより、ご利用の SMTP プロバイダー（この場合は Gmail）のページにリダイレクトされます。
1. ログインして、必要な権限を与えることに同意する
1. 同意すると、トークンがリポジトリに格納されます。公開インスタンス：`http://serveraddress:serverport/crx/de/index.jsp#/conf/global/settings/mailer/oauth` でこの URL に直接アクセスすると、`accessToken` でトークンにアクセスできます。
1. 公開インスタンスごとに上記の手順を繰り返します。

<!-- clarify if the ip/server address in the last procedure is that of the publish instance -->

### Microsoft Outlook {#microsoft-outlook}

1. [https://portal.azure.com/](https://portal.azure.com/)に移動し、ログインします。
1. 検索バーで **Azure Active Directory** を検索し、結果をクリックします。または、[https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) を直接参照することもできます。
1. **アプリの登録**／**新しい登録**&#x200B;をクリックします。

   ![](assets/oauth-outlook1.png)

1. 必要に応じて情報を入力し、**登録**&#x200B;をクリックします。
1. 新しく作成されたアプリに移動し、**API 権限**&#x200B;を選択します。
1. **権限を追加**／**グラフ権限**／**委任権限**&#x200B;に移動します。
1. アプリに対して以下の権限を選択し、「**権限を追加**」をクリックします。
   * `SMTP.Send`
   * `Mail.Read`
   * `Mail.Send`
   * `openid`
   * `offline_access`
1. **認証**／**プラットフォームの追加**／**web** に移動し、「**リダイレクト URL**」セクションで、OAuth コードをリダイレクトする URL を次のように追加してから「**設定**」を押します。
   * `http://localhost:4503/services/mailer/oauth2/token`
1. 公開インスタンスごとに上記の手順を繰り返します。
1. 要件に応じて設定を指定します
1. 次に、「**証明書とシークレット**」に移動し、「**新しいクライアントシークレット**」をクリックし、画面の手順に従ってシークレットを作成します。このシークレットは後で使用するため、必ずメモしてください
1. 左側のウィンドウで「**概要**」を押し、後で使用するために、「**アプリケーション（クライアント）ID**」および「**ディレクトリ（テナント）ID**」の値をコピーします。

まとめると、以下の情報を使用して、AEM 側の Mailer サービスの Oauth2 を設定する必要があります。

* 認証 URLはテナント ID を使用して構築されます。次の形式になります。`https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/authorize`
* トークン URL はテナント ID を使用して構築されます。次の形式になります。`https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* 更新 URL はテナント ID を使用して構築されます。次の形式になります。`https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* クライアント ID
* クライアント秘密鍵

**AEM 側の設定**

次に、OAuth2 の設定を AEM と統合します。

1. `http://serveraddress:serverport/system/console/configMgr` をブラウジングすることで、ローカルインスタンスの web コンソールに移動します。
1.  **Day CQ Mail Service** を探してクリックします。
1. 次の設定を追加します。
   * SMTP サーバーのホスト名: `smtp.office365.com`
   * SMTP ユーザー：電子メール形式のユーザ名
   * 「From」アドレス：メーラーが送信するメッセージの「From」フィールドで使用するメールアドレス
   * SMTP サーバーポート：要件に応じて `25` または `587`
   * 「**SMPT は StarTLS を使用**」と「**SMTP には StarTLS が必要**」のチェックボックスをオンにします。
   * **OAuth フロー**&#x200B;を確認して「**保存**」をクリックします。
1.  **CQ メーラー SMTP OAuth2 プロバイダー** を探して、それをクリックします。
1. 必要な情報を以下のとおり入力します。
   * 「認証 URL」、「トークン URL」、「更新トークン URL」を、[この手順の最後](#microsoft-outlook)に説明した方法で作成し、入力します。
   * クライアント ID とクライアント秘密鍵：これらのフィールドに、前述のように取得した値を設定します。
   * 次のスコープを設定に追加します。
      * openid
      * offline_access
      * `https://outlook.office365.com/Mail.Send`
      * `https://outlook.office365.com/Mail.Read`
      * `https://outlook.office365.com/SMTP.Send`
   * AuthCode リダイレクト URL：`http://localhost:4503/services/mailer/oauth2/token`
   * 更新トークン URL：これは、上記のトークン URL と同じ値である必要があります
1. 「**保存**」をクリックします。

設定が完了すると、設定は次のようになります。

![](assets/oauth-outlook-smptconfig.png)

次に、OAuth コンポーネントをアクティベートします。手順は次のとおりです。

1. URL：`http://serveraddress:serverport/system/console/components` にアクセスして、コンポーネントコンソールに移動します。
1. 以下のコンポーネントを探します
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeGenerateServlet`
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeAccessTokenGenerator`
1. コンポーネントの左側にある「再生」アイコンを押します。

![components2](assets/oauth-components-play.png)

最後に、以下により設定を確認します。

1. 公開インスタンスのアドレスに移動し、管理者としてログインします。
1. ブラウザーで新しいタブを開き、`http://serveraddress:serverport/services/mailer/oauth2/authorize` に移動します。これにより、ご利用の SMTP プロバイダー（この場合は Gmail）のページにリダイレクトされます。
1. ログインして、必要な権限を与えることに同意する
1. 同意すると、トークンがリポジトリに格納されます。ご利用の公開インスタンスで次の URL に直接アクセスすることで、`accessToken` のトークンにアクセスできます。`http://serveraddress:serverport/crx/de/index.jsp#/conf/global/settings/mailer/oauth`