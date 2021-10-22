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
ht-degree: 36%

---

# 電子メール通知の設定{#configuring-email-notification}

AEM は、次のようなユーザーに電子メール通知を送信します。

* 変更やレプリケーションなど、ページイベントを購読したことがある。[通知インボックス](/help/sites-classic-ui-authoring/author-env-inbox.md#subscribing-to-notifications)では、このようなイベントを購読する方法について説明します。

* フォーラムイベントを購読したことがある
* ワークフローで手順を実行する必要がある。[参加者ステップ](/help/sites-developing/workflows-step-ref.md#participant-step)では、ワークフローで電子メール通知を実行する方法について説明します。

前提条件：

* ユーザーのプロファイルで有効な電子メールアドレスが定義されている必要があります。
* 10. **Day CQ Mail Service** を適切に設定する必要があります。

ユーザーへの通知は、各自がプロファイルで定義している言語の電子メールで送信されます。言語ごとに、独自のカスタマイズ可能なテンプレートがあります。新しい言語用には新しい電子メールテンプレートを追加できます。

>[!NOTE]
>
>AEM を操作しているときは、このようなサービスの設定を管理する方法がいくつかあります。詳細および推奨事項については、[OSGi の設定](/help/sites-deploying/configuring-osgi.md)を参照してください。

## メールサービスの設定 {#configuring-the-mail-service}

AEM で電子メールを送信できるようにするために、**Day CQ Mail Service** を適切に設定する必要があります。設定は、Web コンソールで表示できます。AEM を操作しているときは、このようなサービスの設定を管理する方法がいくつかあります。詳細および推奨事項については、[OSGi の設定](/help/sites-deploying/configuring-osgi.md)を参照してください。

以下の制約が適用されます。

* **SMTP サーバーポート**&#x200B;は 25 以上にする必要があります。

* 10. **SMTP サーバーのホスト名** を空白にすることはできません。
* **「送信元」アドレス**&#x200B;は空白にしてはなりません。

**Day CQ Mail Service** の問題をデバッグしやすくするために、サービスのログを監視できます。

`com.day.cq.mailer.DefaultMailService`

設定は、Web コンソールに次のように表示されます。

![chlimage_1-276](assets/chlimage_1-276.png)

## 電子メール通知チャネルの設定 {#configuring-the-email-notification-channel}

ページまたはフォーラムのイベント通知を購読するとき、送信元の電子メールアドレスは、デフォルトで `no-reply@acme.com` に設定されます。この値は、Web コンソールで **Notification Email Channel** サービスを設定することで変更できます。

差出人の電子メールアドレスを設定するには、 `sling:OsgiConfig` ノードをリポジトリに追加します。 次の手順を実行して、ノードを直接追加します。CRXDE Lite:

1. CRXDE Lite で、`config` という名前のノードを、アプリケーションフォルダーの下に追加します。
1. config フォルダーに、次の名前のノードを追加します。

   `com.day.cq.wcm.notification.email.impl.EmailChannel`リソースのタイプは次のとおりとします。`sling:OsgiConfig`

1. の `String` プロパティを `email.from`. 値には、使用する電子メールアドレスを指定します。

1. 「**すべて保存**」をクリックします。

次の手順を使用して、コンテンツパッケージソースフォルダーでノードを定義します。

1. を `jcr_root/apps/*app_name*/config folder`、という名前のファイルを作成します。 `com.day.cq.wcm.notification.email.impl.EmailChannel.xml`

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

* `${userFullName}`：イベントをトリガーしたユーザーの完全名。

* `${userId}`：イベントをトリガーしたユーザーの ID。
* `${modifications}`は、ページイベントのタイプとページパスを次の形式で示します。

   &lt;page event=&quot;&quot; type=&quot;&quot;> => &lt;page path=&quot;&quot;>

   例えば、次の操作が可能です。

   PageModified => /content/geometrixx/en/products

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

ここで、 `<text_x>` には、静的テキストと動的文字列変数を組み合わせることができます。

フォーラム通知用の電子メールテンプレート内では次の変数を使用できます。

* `${time}`、イベントの日時。

* `${forum.path}`：フォーラムページへのパス。

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
>ここで、 `<text_x>` には、静的テキストと動的文字列変数を組み合わせることができます。 各行の `<text_x>` 項目はバックスラッシュ ( `\`) を使用します。ただし、最後のインスタンスを除き、バックスラッシュがない場合は `<text_x>` 文字列変数。
>
>テンプレート形式について詳しくは、[Properties.load() メソッドの javadocs](https://docs.oracle.com/javase/8/docs/api/java/util/Properties.html#load-java.io.InputStream-) を参照してください。

メソッド `${payload.path.open}` 作業項目のペイロードへのパスを表示します。 例えば、 Sites のページの場合は、 `payload.path.open` 次のようになります。 `/bin/wcmcommand?cmd=open&path=…`.;サーバー名が付いていないので、テンプレートの先頭には `${host.prefix}`.

電子メールテンプレート内では以下の変数を使用できます。

* `${event.EventType}`、イベントのタイプ
* `${event.TimeStamp}`、イベントの日時
* `${event.User}`：イベントをトリガーしたユーザー
* `${initiator.home}`、イニシエータ・ノード・パス

* `${initiator.name}`、イニシエータ名

* `${initiator.email}`（イニシエーターの E メールアドレス）
* `${item.id}`（作業項目の id）
* `${item.node.id}`（この作業項目に関連付けられたワークフローモデル内のノードの id）
* `${item.node.title}`（作業項目のタイトル）
* `${participant.email}`、参加者の電子メールアドレス
* `${participant.name}`、参加者の名前
* `${participant.familyName}`（参加者の姓）
* `${participant.id}`，参加者の id
* `${participant.language}`、参加者の言語
* `${instance.id}`、ワークフロー id
* `${instance.state}`、ワークフローの状態
* `${model.title}`（ワークフローモデルのタイトル）
* `${model.id}`（ワークフローモデルの id）

* `${model.version}`（ワークフローモデルのバージョン）
* `${payload.data}`、ペイロード

* `${payload.type}`、ペイロードタイプ
* `${payload.path}`、ペイロードのパス
* `${host.prefix}`、ホストプレフィックス。例：http://localhost:4502

### 新しい言語用の電子メールテンプレートの追加 {#adding-an-email-template-for-a-new-language}

新しい言語用のテンプレートを追加するには：

1. CRXDE で、ファイルを追加します。 `<language-code>.txt` 以下：

   * `/libs/settings/notification-templates/com.day.cq.wcm.core.page` :ページ通知の場合
   * `/etc/notification/email/default/com.day.cq.collab.forum` :フォーラム通知の場合
   * `/libs/settings/workflow/notification/email/default` :ワークフロー通知の場合

1. 言語に合わせてファイルを調整します。
1. 変更内容を保存します。

>[!NOTE]
>
>10. `<language-code>` 電子メールテンプレートのファイル名として使用する場合は、AEMで認識される 2 文字の小文字の言語コードを使用する必要があります。 言語コードについては、AEM は ISO-639-1 に依存しています。

## AEM Assets の電子メール通知の設定 {#assetsconfig}

AEM Assets のコレクションが共有されている場合も共有されていない場合も、AEM から電子メール通知を受信できます。電子メール通知を設定するには、次の手順に従います。

1. [メールサービスの設定](/help/sites-administering/notification.md#configuring-the-mail-service)で説明したように、電子メールサービスを設定します。
1. AEM に管理者としてログインします。**ツール**／**操作**／**Web コンソール**&#x200B;をクリックして、Web コンソール設定を開きます。
1. **Day CQ DAM Resource Collection Servlet** を編集します。「**send email**」を選択します。「**保存**」をクリックします。

## OAuth の設定 {#setting-up-oauth}

AEMは、組織が安全な電子メール要件に準拠できるように、OAuth2 の統合メーラーサービスをサポートしています。

以下に示すように、複数の E メールプロバイダーに対して OAuth を設定できます。

>[!NOTE]
>
>この手順は、パブリッシュインスタンスの例です。 オーサーインスタンスで電子メール通知を有効にする場合は、オーサーインスタンスで同じ手順を実行する必要があります。

### Gmail {#gmail}

1. でプロジェクトを作成する `https://console.developers.google.com/projectcreate`
1. プロジェクトを選択し、に移動します。 **API とサービス** - **ダッシュボード — 資格情報**
1. 必要に応じて OAuth 同意画面を設定する
1. 次の [ 更新 ] 画面で、次の 2 つのスコープを追加します。
   * `https://mail.google.com/`
   * `https://www.googleapis.com//auth/gmail.send`
1. スコープを追加したら、に戻ります。 **資格情報** 左側のメニューで、 **資格情報の作成** - **OAuth Client ID** - **デスクトップアプリ**
1. 新しいウィンドウが開き、クライアント ID とクライアントの秘密鍵が表示されます。
1. これらの資格情報を保存します。

**AEM側の設定**

>[!NOTE]
>
>Adobe管理サービスのお客様は、カスタマーサービスエンジニアと協力して、これらの変更を実稼動環境に加えることができます。

まず、メールサービスを設定します。

1. に移動して、AEM Web コンソールを開きます。 `http://serveraddress:serverport/system/console/configMgr`
1. を探して、「 **Day CQ Mail Service**
1. 次の設定を追加します。
   * SMTP サーバーのホスト名: `smtp.gmail.com`
   * SMTP サーバーポート： `25` または `587`（要件に応じて）
   * 次のチェックボックスをオンにします。 **SMPT で StarTLS を使用** および **SMTP には StarTLS が必要**
   * チェック **OAuth フロー** をクリックします。 **保存**.

次に、以下の手順に従って SMTP OAuth プロバイダーを設定します。

1. に移動して、AEM Web コンソールを開きます。 `http://serveraddress:serverport/system/console/configMgr`
1. を探して、「 **CQ Mailer SMTP OAuth2 Provider**
1. 必要な情報を次のように入力します。
   * 認証 URL: `https://accounts.google.com/o/oauth2/auth`
   * トークン URL: `https://accounts.google.com/o/oauth2/token`
   * スコープ： `https://www.googleapis.com/auth/gmail.send` および `https://mail.google.com/`. 複数の範囲を追加するには、 **+** ボタンをクリックします。
   * クライアント ID とクライアントの秘密鍵：上記の段落で説明したように取得した値を使用して、これらのフィールドを設定します。
   * 更新トークン URL: `https://accounts.google.com/o/oauth2/token`
   * 更新トークンの有効期限：never
1. 「**保存**」をクリックします。

<!-- clarify refresh token expiry, currrently not present in the UI -->

設定が完了すると、設定は次のようになります。

![oauth smtp プロバイダー](assets/oauth-smtpprov2.png)

次に、OAuth コンポーネントをアクティブ化します。 手順は次のとおりです。

1. 次の URL にアクセスして、コンポーネントコンソールに移動します。 `http://serveraddress:serverport/system/console/components`
1. 次のコンポーネントを探します。
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeGenerateServlet`
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeAccessTokenGenerator`
1. コンポーネントの左側にある再生アイコンを押します。

   ![コンポーネント](assets/oauth-components-play.png)

最後に、次の手順で設定を確認します。

1. パブリッシュインスタンスのアドレスに移動し、管理者としてログインします。
1. ブラウザーで新しいタブを開き、に移動します。 `http://serveraddress:serverport/services/mailer/oauth2/authorize`. これにより、SMTP プロバイダー（この場合は Gmail）のページにリダイレクトされます。
1. ログインと、必要な権限の付与に対する同意
1. 同意すると、トークンはリポジトリに保存されます。 これには、以下でアクセスできます。 `accessToken` パブリッシュインスタンスでこの URL に直接アクセスして、次の操作をおこないます。 `http://serveraddress:serverport/crx/de/index.jsp#/conf/global/settings/mailer/oauth`
1. 各パブリッシュインスタンスに対して上記を繰り返します。

<!-- clarify if the ip/server address in the last procedure is that of the publish instance -->

### Microsoft Outlook {#microsoft-outlook}

1. に移動します。 [https://portal.azure.com/](https://portal.azure.com/) をクリックし、ログインします。
1. を検索 **Azure Active Directory** 検索バーで、結果をクリックします。 または、 [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)
1. をクリックします。 **アプリの登録** - **新規登録**

   ![](assets/oauth-outlook1.png)

1. 必要に応じて情報を入力し、「 **登録**
1. 新しく作成したアプリに移動し、「 」を選択します。 **API 権限**
1. に移動します。 **権限を追加** - **グラフ権限** - **委任された権限**
1. アプリに対する以下の権限を選択し、「 **権限を追加**:
   * `SMTP.Send`
   * `Mail.Read`
   * `Mail.Send`
   * `openid`
   * `offline_access`
1. に移動します。 **認証** - **プラットフォームの追加** - **Web**、および **リダイレクト Url** 「 」セクションで、OAuth コードをリダイレクトするための次の URL を追加し、 **設定**:
   * `http://localhost:4503/services/mailer/oauth2/token`
1. 各パブリッシュインスタンスに対して上記を繰り返します。
1. 要件に従って設定を行います
1. 次に、に移動します。 **証明書と秘密**&#x200B;をクリックし、 **新しいクライアント秘密鍵** および画面の手順に従って、秘密鍵を作成します。 後で使用するために、この秘密を必ずメモしておきます
1. 押す **概要** 左側のウィンドウで、 **アプリケーション（クライアント） ID** および **ディレクトリ（テナント） ID** 後で使用する

要約すると、AEM側で Mailer サービスの OAuth2 を設定するには、次の情報が必要です。

* 認証 URL。テナント ID を使用して構築されます。 次の形式になります。 `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/authorize`
* トークン URL。テナント ID を使用して構築されます。 次の形式になります。 `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* 更新 URL。テナント ID を使用して構築されます。 次の形式になります。 `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* クライアント ID
* クライアント秘密鍵

**AEM側の設定**

次に、OAuth2 設定をAEMと統合します。

1. を参照して、ローカルインスタンスの Web コンソールに移動します。 `http://serveraddress:serverport/system/console/configMgr`
1. を探してクリックします。 **Day CQ Mail Service**
1. 次の設定を追加します。
   * SMTP サーバーのホスト名: `smtp.office365.com`
   * SMTP ユーザー：電子メール形式のユーザー名
   * &quot;差出人&quot;のアドレス：メーラーから送信されるメッセージの「送信者：」フィールドで使用する電子メールアドレス
   * SMTP サーバーポート： `25` または `587` 要件に応じて
   * 次のチェックボックスをオンにします。 **SMPT で StarTLS を使用** および **SMTP には StarTLS が必要**
   * チェック **OAuth フロー** をクリックします。 **保存**.
1. を探して、「 **CQ Mailer SMTP OAuth2 Provider**
1. 必要な情報を次のように入力します。
   * 「認証 URL」、「トークン URL」および「更新トークン URL」を入力します。それらの URL は、 [この手順の終わり](#microsoft-outlook)
   * クライアント ID とクライアントの秘密鍵：これらのフィールドに、前述のように取得した値を設定します。
   * 次のスコープを構成に追加します。
      * openid
      * offline_access
      * `https://outlook.office365.com/Mail.Send`
      * `https://outlook.office365.com/Mail.Read`
      * `https://outlook.office365.com/SMTP.Send`
   * AuthCode リダイレクト Url: `http://localhost:4503/services/mailer/oauth2/token`
   * 更新トークン URL:これは、上記のトークン URL と同じ値にする必要があります
1. 「**保存**」をクリックします。

設定が完了すると、設定は次のようになります。

![](assets/oauth-outlook-smptconfig.png)

次に、OAuth コンポーネントをアクティブ化します。 手順は次のとおりです。

1. 次の URL にアクセスして、コンポーネントコンソールに移動します。 `http://serveraddress:serverport/system/console/components`
1. 次のコンポーネントを探します。
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeGenerateServlet`
   * `com.day.cq.mailer.oauth.servlets.handler.OAuthCodeAccessTokenGenerator`
1. コンポーネントの左側にある再生アイコンを押します。

![components2](assets/oauth-components-play.png)

最後に、次の手順で設定を確認します。

1. パブリッシュインスタンスのアドレスに移動し、管理者としてログインします。
1. ブラウザーで新しいタブを開き、に移動します。 `http://serveraddress:serverport/services/mailer/oauth2/authorize`. これにより、SMTP プロバイダー（この場合は Gmail）のページにリダイレクトされます。
1. ログインと、必要な権限の付与に対する同意
1. 同意すると、トークンはリポジトリに保存されます。 これには、以下でアクセスできます。 `accessToken` パブリッシュインスタンスでこの URL に直接アクセスして、次の操作をおこないます。 `http://serveraddress:serverport/crx/de/index.jsp#/conf/global/settings/mailer/oauth`