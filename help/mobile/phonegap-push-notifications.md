---
title: プッシュ通知
seo-title: プッシュ通知
description: このページでは、AEM Mobile アプリでプッシュ通知を使用する方法について説明します。
seo-description: このページでは、AEM Mobile アプリでプッシュ通知を使用する方法について説明します。
uuid: 0ed8b183-ef81-487f-8f35-934d74ec82af
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: ed8c51d2-5aac-4fe8-89e8-c175d4ea1374
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d
workflow-type: tm+mt
source-wordcount: '3291'
ht-degree: 59%

---


# プッシュ通知{#push-notifications}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアント側レンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)を参照してください。

重要な通知を AEM Mobile アプリユーザーに即座に警告できることは、モバイルアプリとそのマーケティングキャンペーンの価値にとって重要です。ここでは、アプリがプッシュ通知を受信できるようにするために必要な手順と、AEM Mobileから電話にインストールされているアプリにプッシュを設定して送信する方法について説明します。 また、プッシュ通知に[ディープリンク](#deeplinking)機能を設定する方法についても説明します。

>[!NOTE]
>
>プッシュ通知は保証型配信ではありません。むしろお知らせに近いものです。全ユーザーがプッシュ通知を受信するように最大限の努力が払われていますが、保証型配信メカニズムではありません。*Also, the time to deliver a push can vary from less than a second to up to half an hour.*

AEM でプッシュ通知を使用するには、さまざまなテクノロジーがいくつか必要になります。まず、プッシュ通知サービスプロバイダーを使用して、通知とデバイスを管理する必要があります(AEMはまだこれを行いません)。 Two providers are configured out-of-the-box with AEM: [Amazon Simple Notification Service](https://aws.amazon.com/sns/) (or SNS), and [Pushwoosh](https://www.pushwoosh.com/). 次に、指定したモバイル OS 向けのプッシュテクノロジーは、適切なサービスである Apple のプッシュ通知サービス（APNS。iOS デバイス用）、Google Cloud Messaging（GCM。Android デバイス用）を経由する必要があります。AEMは、これらのプラットフォーム固有のサービスと直接通信しませんが、プッシュを実行するには、AEMから、通知と共に一部の関連する設定情報を提供する必要があります。

インストールおよび設定（下記）が完了すると、次のように機能します。

1. プッシュ通知が AEM に作成されて、サービスプロバイダー（Amazon SNS または Pushwoosh）に送信されます。
1. サービスプロバイダーが、プッシュ通知を受信してコアプロバイダー（APNS または GCM）に送信します。
1. コアプロバイダーが、プッシュ通知を受け取るように登録されているすべてのデバイスに通知をプッシュします。各デバイスに対して、携帯電話データネットワークまたはWiFi （デバイスで現在使用可能な方）を使用します。
1. 通知用に登録されているアプリが実行中でない場合、通知はデバイスに表示されます。ユーザーが通知をタップすると、アプリが開始され、アプリ内に通知が表示されます。 アプリケーションが既に実行されている場合は、アプリケーション内通知のみが表示されます。

AEM のこのリリースでは、iOS と Android のモバイルデバイスをサポートしています。

## 概要および手順 {#overview-and-procedure}

AEM Mobile アプリでプッシュ通知を使用するには、次のおおまかな手順を実行する必要があります。

通常、AEM開発者は次の操作を行います。

1. Apple および Google メッセージングサービスに登録します。
1. プッシュメッセージングサービスに登録して設定します。
1. アプリにプッシュサポートを追加します。
1. テスト用に電話を準備します。

AEM管理者は次の操作を実行できます。

1. AEM アプリでのプッシュの設定
1. アプリのビルドおよびデプロイ
1. プッシュ通知の送信
1. ディープリンクの設定（オプション）**

### 手順 1：Apple および Google メッセージングサービスへの登録 {#step-register-with-apple-and-google-messaging-services}

#### Using the Apple Push Notification Service (APNS) {#using-the-apple-push-notification-service-apns}

Go to the Apple page [here](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html) to become familiar with the Apple Push Notification Service.

To use APNS you will need a **Certificate** file (a .cer file), a push **Private Key** (a .p12 file) and a **Private Key Password** from Apple. Instructions on how to do that can be found [here](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ProvisioningDevelopment.html).

#### Google Cloud Messaging（GCM）サービスの使用 {#using-the-google-cloud-messaging-gcm-service}

>[!NOTE]
>
>Google は、GCM を Firebase Cloud Messaging（FCM）という類似のサービスに置き換えます。FCM について詳しくは、[こちら](https://developers.google.com/cloud-messaging/faq)を参照してください。

Go to the Google page [here](https://developer.android.com/google/gcm/index.html) to become familiar with Google Cloud Messaging for Android.

You will need to follow the steps [here](https://developer.android.com/google/gcm/gs.html) to **Create a Google API project**, **Enable the GCM Service**, and **Obtain an API Key**. Android デバイスにプッシュ通知を送信するには、**API キー**&#x200B;が必要になります。Also, record your **Project Number**, which is also sometimes called a **GCM Sender Id**.

以下に、GCM API キーを作成する別の方法を示します。

1. Log into google and go to the [Google&#39;s Developer page](https://developers.google.com/mobile/add?platform=android&amp;cntapi=gcm).
1. リストからアプリを選択します（または新しいアプリを作成します）。
1. Under Android Package Name, enter your app id, i.e. `com.adobe.cq.mobile.weretail.outdoorsapp`. （問題が解決しない場合は、「test.test」を使用して再試行します）。
1. 「**Continue To Choose and configure services**」をクリックします。
1. 「Cloud Messaging」を選択し、「**Enable Google Cloud Messaging**」をクリックします。
1. 新しいサーバー API キー（「Server API Key」）と（新規または既存の）送信者 ID（「Sender ID」）が表示されます。

>[!NOTE]
>
>サーバー API キーを記録します。この値は、プッシュプロバイダーのサイトで入力します。

### 手順 2：プッシュメッセージングサービスの登録および設定 {#step-register-and-configure-a-push-messaging-service}

AEM は、プッシュ通知に 3 つのサービスのうちいずれかを使用するように設定されています。

* Amazon SNS
* Pushwoosh
* Adobe Mobile Services

Amazon SNS ** および Pushwoosh ** の設定を使用すると、AEM 画面内からプッシュ通知を送信できます。

Adobe Mobile Services ** の設定を使用すると、Adobe Analytics アカウントを使用して Adobe Mobile Services 内からプッシュ通知を設定および送信できます（ただし、AMS プッシュ通知を有効にするには、この設定をおこなってアプリをビルドする必要があります）。

#### Amazon SNS メッセージングサービスの使用 {#using-the-amazon-sns-messaging-service}

>[!NOTE]
>
>*AmazonSNSの情報と、新しいAWSアカウントを作成するためのリンクは [こちら](https://aws.amazon.com/sns/)。 1 年間無料のアカウントを入手できます。*

Amazon SNS を使用しない場合には、この手順をスキップできます。

次の手順に従って、プッシュ通知用に Amazon SNS を設定します。

1. **Amazon SNS への登録**

   1. アカウント ID を記録します。形式は12桁で、スペースやダッシュは使用できません。&quot;123456789012&quot;と表示されます。
   1. 現在の地域が「us-east」または「eu」であることを確認します。後の手順（ID プールの作成）でそのどちらかが必要になるからです。
   1. After registering, log into the management console and select [SNS](https://console.aws.amazon.com/sns/) (Push Notification Service). 「Get Started」（はじめに）が表示されたらクリックします。

1. **アクセスキーおよび ID の作成**

   1. 画面右上のログイン名をクリックし、メニューから「Security Credentials」を選択します。
   1. Click on Access Keys, and in the space below, click **Create New Access Key**.
   1. Click **Show Access Key**, and copy and save the Access Key ID and Secret Access Key shown. キーをダウンロードするオプションを選択した場合には、ダウンロードした csv ファイルにそれらと同じ値が記載されています。
   1. このページでは、他のセキュリティ関連の証明書などを管理できます。

   >[!NOTE]
   >
   >アクセスキーは、複数のアプリで使用できます。

   「AWS サンドボックス」アカウントを使用する組織でも、同様に以下の手順に従います。

   1. 画面右上のログイン名をクリックし、メニューから「My Security Credentials」を選択します。
   1. 左側のアクションのリストから「Users」をクリックして、ユーザー名を選択します。
   1. 「Security credentials」タブをクリックします。
   1. ここからキーを表示し、新規のキーを作成します。後で使用するためにキーを保存します。


1. **トピックの作成**

   1. 「**Create Topic**」をクリックし、トピック名を選択します。「Topic ARN」、「Topic Owner」、「Region」、「Display name」などすべてのフィールドを記録します。
   1. Click **Other Topic Actions** > **Edit Topic Policy**. Under **Allow these users to subscribe to this topic**, select **Everyone.**
   1. 「**Update Policy**」をクリックします。

   >[!NOTE]
   >
   >開発、テスト、デモなどの、様々なシナリオに合わせて複数のトピックを作成できます。残りのSNS構成は同じままにできます。 別のトピックでアプリを作成します。そのトピックに送信されるプッシュ通知は、そのトピックで作成されたアプリでのみ受信されます。

1. **プラットフォームアプリケーションの作成**

   1. Applications／Create Platform Application をクリックします。名前を選択し、プラットフォーム（iOS の場合は APNS、Android の場合は GCM）を選択します。プラットフォームに応じて、他のフィールドにも入力する必要があります。

      1. APNS の場合、P12 ファイル、パスワード、証明書および秘密鍵をすべて入力する必要があります。These should have been obtained in the step *Using the Apple Push Notification Service (APNS)* above.
      1. GCM の場合、API キーを入力する必要があります。This should have been obtained in the step *Using the Google Cloud Messaging (GCM) service* above.
   1. サポート対象のプラットフォームごとに 1 回、上述の手順を繰り返します。iOS と Android の両方にプッシュできるようにするには、2 つのプラットフォームアプリケーションを作成する必要があります。


1. **ID プールの作成**

   1. Use [Cognito](https://console.aws.amazon.com/cognito) to create an Identity Pool, which will store basic data of unauthenticated users. ただし、現在、Amazon・コグニトがサポートしている地域は「米国東部」と「eu」のみです。
   1. ID プールに名前を付け、「Enable access to unauthenticated identities」ボックスをオンにします。
   1. 次のページ（Your Cognito identities require access to your resources **）で、「Allow」をクリックします。
   1. ページの右上で、「Edit identity pool」リンクをクリックします。** IDプールIDが表示されます。 後で使用するために、このテキストを保存します。
   1. 同じページで、「Unauthenticated role」の隣にあるドロップダウンを選択し、「Cognito_&lt;プール名>UnauthRole」という役割が選択されていることを確認します。変更を保存します。

1. **アクセスの設定**

   1. Login to [Identity and Access Management](https://console.aws.amazon.com/iam/home) (IAM)
   1. 「Roles」を選択します。
   1. 前の手順で作成した役割（Cognito_&lt;ID プール名>Unauth_Role という名前）をクリックします。表示された「ロールARN」を記録します。
   1. 「Inline Policies」をまだ開いていない場合は開きます。1Click_Cognito_&lt;yourIdentityPoolName>Unauth_Role_1234567890123のような名前のポリシーが表示されます。
   1. 「Edit Policy」をクリックします。ポリシードキュメントの内容を次のJSONスニペットに置き換えます。

   <table>
    <tbody>
     <tr>
     <td><p> </p> <p>{</p> <p> "Version":"2012-10-17",</p> <p> "Statement": [</p> <p> {</p> <p> "アクション": [</p> <p> "mobileanalytics:PutEvents",</p> <p> "cognito-sync:*",</p> <p> "SNS:CreatePlatformEndpoint",</p> <p> "SNS:Subscribe"</p> <p> ],</p> <p> "効果":「許可」、</p> <p> "Resource": [</p> <p> "*"</p> <p> ]</p> <p> }</p> <p> ]</p> <p>}</p> <p> </p> </td>
     </tr>
    </tbody>
    </table>

   1. 「**Apply Policy**」をクリックします。


#### Pushwoosh メッセージングサービスの使用 {#using-the-pushwoosh-messaging-service}

Pushwoosh を使用しない場合には、この手順をスキップできます。

Pushwoosh を使用するには：

1. **Pushwoosh への登録**

   1. pushwoosh.com に移動し、新しいアカウントを作成します。

1. **API アクセストークンの作成**

   1. Pushwooshサイトで、APIアクセスメニュー項目に移動してAPIアクセストークンを生成します。 これは、安全に記録する必要があります。

1. **新しいアプリを作成**

   1. Android をサポートする場合には、GCM API キーを指定する必要があります。
   1. アプリを設定するときには、フレームワークとして Cordova を選択します。
   1. iOS をサポートする場合には、証明書ファイル（.cer）、プッシュ証明書（.p12）および秘密鍵のパスワードを指定する必要があります。これらは、Apple の APNS サイトから入手済みです。フレームワークには、Cordovaを選択します。
   1. Pushwoosh が、そのアプリのアプリ ID を「XXXXX-XXXXX」という形式で生成します。各 X は 16 進数値（0 ～ F）です。

>[!NOTE]
>
>*2つ目のアプリが同じアプリID（およびその他の関連値）を持つAEMで設定されている場合：APIアクセストークンとGCM Id(GCM Id)を参照)、AEM上の2番目のアプリを介して送信されるプッシュ通知は、そのアプリIDを持つ他のアプリに送信されます。*

### 手順 3：アプリへのプッシュサポートの追加 {#step-add-push-support-to-the-app}

#### コンテンツ同期設定の追加 {#add-contentsync-configuration}

notificationsConfig という 2 つのコンテンツノードを（1 つは app-config に、もう 1 つは app-config-dev に）作成します。

* /content/`<your app>`/shell/jcr:content/pge-app/app-config-dev/notificationsConfig
* /content/`<your app>`/shell/jcr:content/pge-app/app-config/notificationsConfig

With these properties (.content.xml files) :
&lt;jcr:root xmlns:jcr=&quot; [https://www.jcp.org/jcr/1.0](https://www.jcp.org/jcr/1.0)&quot; xmlns:nt=&quot; [https://www.jcp.org/jcr/nt/1.0](https://www.jcp.org/jcr/nt/1.0)&quot;
jcr:primaryType=&quot;nt:unstructured&quot;
excludeProperties=&quot;[appAPIAccessToken]&quot;
path=&quot;../../../..&quot;
targetRootDirectory=&quot;www&quot;type=&quot;notificationsconfig&quot;/>

>[!NOTE]
>
>コンテンツ同期ハンドラーは、これらのノードを検索し、ノードがなければ pge-notifications-config.json ファイルを書き出しません。

#### クライアントライブラリの追加 {#add-client-libraries}

次の手順に従って、プッシュ通知クライアントライブラリをアプリに追加する必要があります。

CRXDE Lite で以下の手順に従います。

1. Navigate to */etc/designs/phonegap/&lt;app name>/clientlibsall.*
1. プロパティペインで「埋め込み」セクションをダブルクリックします。
1. 表示されるダイアログで、+ ボタンをクリックして新規クライアントライブラリを追加します。
1. 新規テキストフィールドで、「cq.mobile.push」を追加し、「OK」をクリックします。
1. もう 1 つ「cq.mobile.push.amazon」というエントリを追加し、「OK」をクリックします。
1. 変更内容を保存します。

>[!NOTE]
>
>アプリのスペースの都合で、プッシュ通知を削除したか、使用していない場合は、コンソールのエラーメッセージを避けるために、これらのクライアントライブラリをアプリから削除します。

### 手順 4：テスト用の電話の準備 {#step-prepare-a-phone-for-testing}

>[!NOTE]
>
>*プッシュ通知の場合、エミュレーターはプッシュ通知を受信できないので、実際のデバイスでテストする必要があります。*

#### iOS {#ios}

For iOS you will need to use a Mac OS computer and you need to join the [iOS Developer Program](https://developer.apple.com/programs/ios/). 一部の企業は、すべての開発者が利用できる会社ライセンスを持っています。

XCode 8.1 では、プッシュ通知を使用する前に、プロジェクトの「Capabilities」タブに移動し、「Push Notifications」のトグルをオンに切り替える必要があります。

#### Android {#android}

To install the app on an Android phone using CLI (see below: **Step 6 - Build and deploy the app**), you first must put the phone in &quot;developer mode.&quot; See [Enabling On-device Developer Options](https://developer.android.com/tools/device.html#developer-device-options) for details on doing this.

### 手順 5：AEM アプリでのプッシュの設定 {#step-configure-push-on-aem-apps}

ビルドして設定済みのモバイルデバイスにデプロイする前に、使用するメッセージングサービス用に通知設定をおこなう必要があります。

1. プッシュ通知に適切な認証グループを作成します。
1. 適切なユーザーとして AEM にログインし、「アプリ」タブをクリックします。
1. 「アプリケーション」をクリックします。
1. クラウドサービスを管理タイルを検索し、鉛筆をクリックして、クラウド設定を変更します。
1. 通知設定として、「Amazon SNS 接続」、「Pushwoosh 接続」または「Adobe Mobile Services」を選択します。
1. プロバイダーのプロパティを入力し、「送信」をクリックして保存し、「完了」をクリックします。AMSの場合を除き、この段階ではリモートでの検証は行われません。
1. クラウドサービスを管理タイルに、入力した設定が表示されます。

### 手順 6：アプリのビルドおよびデプロイ {#step-build-and-deploy-the-app}

**注意：** PhoneGapアプリケーションの構築に関する説明は [](/help/mobile/building-app-mobile-phonegap.md) 、こちらも参照してください。

PhoneGap を使用してアプリをビルドしてデプロイするには、2 つの方法があります。

**注意：** プッシュ通知はプッシュプロバイダー（AppleまたはGoogle）とデバイスの間で異なるプロトコルを使用するので、プッシュ通知テストではエミュレーターは十分ではありません。 現在の Mac／PC ハードウェアおよびエミュレーターは、これをサポートしていません。

1. *PhoneGap Build* は、PhoneGapが提供するサービスです。PhoneGapは、アプリを自社のサーバー上で作成し、デバイスに直接ダウンロードできるようにするサービスです。 Refer to the [PhoneGap Build documentation](https://build.phonegap.com/) to learn how to set up and use PhoneGap Build.

1. *PhoneGap Command Line Interface* (CLI)を使用すると、コマンドラインで豊富なPhoneGapコマンドを使用して、アプリの作成、デバッグ、デプロイを行うことができます。 Refer to the [PhoneGap developer documentation](https://docs.phonegap.com/en/edge/guide_cli_index.md.html#The%20Command-Line%20Interface) to learn how to set up and use PhoneGap CLI.

### 手順 7：プッシュ通知の送信 {#step-send-a-push-notification}

新規通知を作成して送信するには、次の手順に従います。

1. 新規通知の作成

   * AEM Mobile アプリのダッシュボードで、プッシュ通知タイルを探します。
   * 右上のメニューで、「作成」を選択します。このボタンは、クラウド設定が最初に設定されるまで使用できません。
   * 通知を作成ウィザードで、タイトルおよびメッセージに入力し、「作成」ボタンをクリックします。これで、通知をすぐに送信するか、後で送信する準備ができました。 編集したり、メッセージやタイトルを変更して保存したりできます。

1. 通知の送信

   * アプリダッシュボードで、プッシュ通知タイルを探します。
   * 通知を選択するか、右下の「詳細」ボタン(..)をクリックして、通知のリストを表示します。 また、このリストは、通知の送信準備ができているか、既に送信されているか、送信中にエラーが発生したかを示します。
   * 1 つの通知（のみ）のチェックボックスを選択し、リストの上方にある「通知を送信」ボタンをクリックします。表示されるダイアログで、「キャンセル」または「送信」を行うことができます。

1. 結果の処理

   * プッシュ通知サービス（Amazon SNS または Pushwoosh）が送信要求を受信し、要求が有効であることを確認してネイティブのプロバイダー（APNS および GCM）に正常に送信した場合には、送信ダイアログがメッセージなしで閉じます。通知リストで、その通知のステータスが「送信済み」と表示されます。
   * プッシュ送信が失敗した場合、ダイアログには問題の発生を示すメッセージが表示されます。通知リストでは、その通知のステータスが「エラー」と表示されますが、問題が修正された場合は、通知を再度送信できます。 エラーのイベント時に、サーバーエラーログに追加のエラー情報が表示されます。
   * iOS と Android のプッシュ通知には、プラットフォームの違いがいくつかあります。その中には

      * CLI によるビルドでアプリが起動するのは、アプリを Android にデプロイした後です。iOSでは、手動で開始する必要があります。 起動時にプッシュ登録手順が行われるので、Androidアプリはすぐにプッシュ通知を受け取ることができます（Androidアプリは起動および登録されるため）が、iOSアプリは受け取りません。
      * Android では「OK」ボタンのテキストはすべて大文字です（アプリ内通知で追加されたその他のボタンも大文字です）が、iOS ではそうではありません。

AMS プッシュ通知では、AMS サーバーから通知を作成し、送信する必要があります。AMSは、AWSおよびPushwooshでAEM通知が提供する機能を超える追加のプッシュ通知機能を提供します。

>[!NOTE]
>
>プッシュ通知は保証型配信ではありません。むしろお知らせに近いものです。全ユーザーがプッシュ通知を受信するように最大限の努力が払われていますが、保証型配信メカニズムではありません。*Also, the time to deliver a push can vary from less than a second to up to half an hour.*

### プッシュ通知でのディープリンクの設定 {#configuring-deep-linking-with-push-notifications}

ディープリンクとはプッシュ通知のコンテキストでは、これは、アプリを開くか、アプリ内の指定した場所に（開いている場合に）転送するかを許可する手段です。

では、これはどのように機能するでしょうか。プッシュ通知の作成者は、視覚的なパスブラウザーを利用して、オプションで通知にボタンラベル（「Show me!」など）を追加したり、通知内にリンクを記載するページを選択したりできます。送信すると、プッシュが通常どおりに発生しますが、アプリ内メッセージでは「OK」ボタンが「解除」ボタンに置き換えられ、指定した新しいボタン（「Show me!」）も表示される点が異なります。「新規」ボタンをクリックすると、アプリ内の指定されたページに移動します。 「解除」をクリックすると、単にメッセージが消去されます。

アプリが開かれていない場合は、シェードが通常どおりに表示されます。シェードで通知に対してアクションを実行すると、アプリが開き、プッシュ通知で設定された内容に基づいてユーザーにディープリンクボタンが表示されます。

通知を作成し、オプションのディープリンクのボタンテキストおよびリンクパスを追加します。

>[!CAUTION]
>
>ダッシュボードのプッシュ通知タイルにアクセスするには、以下の手順に従います。

1. **クラウドサービスを管理**&#x200B;タイルの右上隅の編集アイコンをクリックします。

   ![chlimage_1-108](assets/chlimage_1-108.png)

1. 「**Pushwoosh 接続**」を選択します。「**次へ**」をクリックします。

   ![chlimage_1-109](assets/chlimage_1-109.png)

1. プロパティの詳細を入力して、「**送信**」をクリックします。

   ![chlimage_1-110](assets/chlimage_1-110.png)

   設定を送信すると、ダッシュボードに&#x200B;**プッシュ通知**&#x200B;タイルが表示されます。

   ![chlimage_1-111](assets/chlimage_1-111.png)

### 通知を作成ウィザード {#create-notification-wizard}

ダッシュボードに&#x200B;**プッシュ通知**&#x200B;タイルが表示されたら、通知を作成ウィザードを使用してコンテンツを追加します。

1. **プッシュ通知**&#x200B;タイルの右上隅にある追加記号をクリックし、**通知を作成ウィザード**&#x200B;を表示します。

   ![chlimage_1-112](assets/chlimage_1-112.png)

1. リンクパス内の参照アイコンをクリックすると、ユーザーにアプリのコンテンツ構造が表示されます。

   パスを選択したら、チェックアイコンをクリックします。

   ![chlimage_1-113](assets/chlimage_1-113.png)

   >[!NOTE]
   >
   >リンクボタンのテキストは20文字までに制限されています。
   >
   >エンドユーザーが最新バージョンのアプリケーションを持っておらず、リンクされたパスを利用できない場合、ディープリンクのアクションを確認すると、ユーザーがアプリのメインページに移動します。

1. **通知を作成ウィザード**&#x200B;の「**テキスト詳細**」に入力し、「**作成**」をクリックします。

   ![chlimage_1-114](assets/chlimage_1-114.png)

   **プッシュ通知**&#x200B;タイルから、作成したプッシュ通知をクリックして、詳細を表示します。

   プロパティの編集、通知の送信、通知の削除をおこなえます。

   ![chlimage_1-115](assets/chlimage_1-115.png)

>[!NOTE]
>
>**追加情報**:
>
>PushwooshおよびAmazonSNSは、6.4リリース以降はサポートされなくなり、パッケージ共有のアドオンとして使用できるようになります。

### 次の手順 {#the-next-steps}

Once you understand the details on push notifications for your app, see [AEM Mobile Content Personalization](/help/mobile/phonegap-aem-mobile-content-personalization.md).

