---
title: プッシュ通知
description: ここでは、Adobe Experience Manager Mobile アプリでプッシュ通知を使用する方法について説明します。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 375f2f40-1b98-4e21-adee-cbea274e6a2a
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '3156'
ht-degree: 1%

---

# プッシュ通知{#push-notifications}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアントサイドレンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)。

Adobe Experience Manager（AEM）モバイルアプリのユーザーに対して、重要な通知を即座に通知できることが、モバイルアプリとそのマーケティングキャンペーンの価値にとって重要です。 ここでは、アプリにプッシュ通知を受信させるために実行する必要がある手順を説明します。 また、AEM Mobileから携帯電話にインストールされているアプリにプッシュを設定して送信する方法についても説明します。 また、このセクションでは、 [ディープリンク](#deeplinking) プッシュ通知に機能を追加します。

>[!NOTE]
>
>*プッシュ通知は配信を保証するものではありません。お知らせに似ています。 全員が確実に受け取れるように最善の努力をしますが、それらは保証された配信メカニズムではありません。 また、プッシュの配信時間は、1 秒未満から 30 分まで変動する場合があります。*

AEMでプッシュ通知を使用するには、異なるテクノロジーが必要です。 まず、プッシュ通知サービスプロバイダーを使用して、通知とデバイスを管理する必要があります（AEMでは、まだこれを行いません）。 AEMでは、次の 2 つのプロバイダーが標準で設定されています。 [Amazon Simple Notification Service](https://aws.amazon.com/sns/) （または SNS）、 [プッシュウーシュ](https://www.pushwoosh.com/). 次に、特定のモバイル OS のプッシュテクノロジーは、iOS デバイス用のApple Push Notification Service （APNS）と、Android™ デバイス用のGoogle Cloud Messaging （GCM）のうち、適切なサービスを経由する必要があります。 AEMは、これらのプラットフォーム固有のサービスと直接通信しませんが、関連する設定情報の一部をAEMが提供し、これらのサービスがプッシュを実行するための通知を行う必要があります。

インストールと設定が完了すると（後述のとおり）、次のように動作します。

1. プッシュ通知がAEMで作成され、サービスプロバイダー（Amazon SNS または Pushwoosh）に送信されます。
1. サービスプロバイダーが受信し、コアプロバイダー（APNS または GCM）に送信します。
1. コアプロバイダーは、そのプッシュに登録されているすべてのデバイスに通知をプッシュします。 デバイスごとに、携帯データネットワークまたは WiFi （デバイスで使用可能な方）を使用します。
1. デバイスが登録されているアプリが実行されていない場合、通知はデバイスに表示されます。 通知をタップしたユーザーがアプリを起動し、アプリ内に通知を表示します。 アプリケーションが既に実行されている場合は、アプリ内通知のみが表示されます。

このリリースのAEMでは、iOSおよび Android™ モバイルデバイスをサポートしています。

## 概要と手順 {#overview-and-procedure}

AEM Mobile アプリでプッシュ通知を使用するには、次の大まかな手順を実行する必要があります。

通常、Experience Manager開発者は次の操作を行います。

1. AppleおよびGoogleのメッセージサービスへの登録
1. プッシュメッセージサービスへの登録と設定
1. アプリへのプッシュサポートの追加
1. テスト用の電話の準備

Experience Manager管理者は次の操作を行います。

1. AEM アプリでのプッシュの設定
1. アプリのビルドとデプロイ
1. プッシュ通知の送信
1. ディープリンクの設定 *（オプション）*

### 手順 1:AppleおよびGoogleのメッセージサービスへの登録 {#step-register-with-apple-and-google-messaging-services}

#### Apple Push Notification Service （APNS）の使用 {#using-the-apple-push-notification-service-apns}

Appleページに移動 [こちら](https://developer.apple.com/documentation/usernotifications#//apple_ref/doc/uid/TP40008194-CH8-SW1) Appleのプッシュ通知サービスを理解するには：

APN を使用するには、 **証明書** ファイル（.cer ファイル）、プッシュ **秘密鍵** （.p12 ファイル）、および **秘密鍵のパスワード** Appleから その方法については、こちらを参照してください [こちら](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/).

#### Google Cloud Messaging （GCM）サービスの使用 {#using-the-google-cloud-messaging-gcm-service}

>[!NOTE]
>
>Googleは、GCM を Firebase Cloud Messaging （FCM）と呼ばれる同様のサービスに置き換えます。 FCM について詳しくは、 [こちら](https://firebase.google.com/docs/cloud-messaging/).

Googleページに移動 [こちら](https://developer.android.com/google/gcm/index.html) Google Cloud Messaging for Android™ の詳細

[次の手順に従います](https://developer.android.com/google/gcm/gs.html) 対象： **Google API プロジェクトの作成**, **GCM サービスの有効化**、および **API キーの取得**. 必要なのは、 **API キー** Android™ デバイスにプッシュ通知を送信する。 また、を記録します **プロジェクト番号**（別名） **GCM 送信者 Id**.

以下の手順は、GCM API キーを作成する別の方法を示しています。

1. Google にログインし、 [Googleの開発者向けページ](https://developers.google.com/mobile/add?platform=android&amp;cntapi=gcm).
1. リストからアプリを選択します（または作成します）。
1. 「Android™ パッケージ名」の下で、アプリ ID （）を入力します。 `com.adobe.cq.mobile.weretail.outdoorsapp`. （それでもうまくいかない場合は、「test.test」で再試行してください。）
1. クリック **サービスの選択と設定を続行する**
1. 「Cloud Messaging」を選択し、 **Google Cloud Messaging の有効化**.
1. 新しい Server API キーと（新規または既存の）送信者 ID が表示されます。

>[!NOTE]
>
>サーバー API キーを記録します。 この値は、プッシュプロバイダーのサイトに入力されます。

### 手順 2：プッシュメッセージサービスの登録と設定 {#step-register-and-configure-a-push-messaging-service}

AEMは、次の 3 つのサービスのいずれかをプッシュ通知に使用するように設定されています。

* Amazon SNS
* Pushwoosh
* Adobe Mobile Services

*AMAZONSNS* および *プッシュウーシュ* 設定では、AEM screens 内からプッシュしたメールを送信できます。

*Mobile Services のAdobe* configuration を使用すると、Adobe Analytics アカウントを使用してAdobeMobile Services 内からプッシュ通知を設定して送信できます（ただし、AMS プッシュ通知を有効にするには、この設定を使用してアプリをビルドする必要があります）。

#### Amazon SNS メッセージサービスの使用 {#using-the-amazon-sns-messaging-service}

>[!NOTE]
>
>*Amazon SNS に関する情報およびAWS アカウントを作成するためのリンクが表示されます [こちら](https://aws.amazon.com/sns/). 1 年間無料でアカウントを取得できます。*

Amazon SNS を使用しない場合は、以下の手順をスキップできます。

プッシュ通知用のAmazon SNS をセットアップするには、次の手順に従います。

1. **Amazon SNS への登録**

   1. アカウント Id を記録します。 形式は、スペースやダッシュを含まない 12 桁（つまり「123456789012」）にする必要があります。
   1. 後の手順（ID プールの作成）では「us-east」または「eu」地域にいることを確認します。
   1. 登録後、管理コンソールにログインし、 [SNS](https://console.aws.amazon.com/sns/) （プッシュ通知サービス）。 表示された場合は、「Get Started」をクリックします。

1. **アクセスキーと ID の作成**

   1. 画面右上のログイン名をクリックし、メニューから「セキュリティ資格情報」を選択します。
   1. 「アクセスキー」をクリックし、下のスペースで **新しいアクセスキーの作成**.
   1. クリック **アクセスキーを表示**&#x200B;を作成し、表示されているアクセスキー ID と秘密アクセスキーをコピーして保存します。 キーをダウンロードするオプションを選択すると、これらの同じ値を含む CSV ファイルが得られます。
   1. このページでは、その他のセキュリティ関連の証明書や、その他の証明書を管理できます。

   >[!NOTE]
   >
   >1 つのアクセスキーを複数のアプリで使用できます。

   「AWS Sandbox」アカウントを使用する組織の場合、手順は似ており、こちらで概要を説明します。

   1. 画面右上のログイン名をクリックし、メニューから「マイセキュリティ資格情報」を選択します。
   1. アクションの左リストで「ユーザー」をクリックし、ユーザー名を選択します。
   1. 「セキュリティ資格情報」タブをクリックします。
   1. ここから、キーを表示し、新しいキーを作成します。 後で使用するためにキーを保存します。

1. **トピックの作成**

   1. クリック **トピックを作成** トピック名を選択します。 トピック ARN、トピック所有者、地域、表示名などのすべてのフィールドを記録します。
   1. クリック **その他のトピック アクション** > **トピック ポリシーの編集**. 次の下 **これらのユーザーに、このトピックへのサブスクライブを許可します**&#x200B;を選択 **皆さん。**
   1. クリック **ポリシーの更新**.

   >[!NOTE]
   >
   >開発、テスト、デモなど、様々なシナリオに対して複数のトピックを作成できます。 残りの SNS 設定は同じままです。 別のトピックを使用してアプリをビルドします。そのトピックに送信されたプッシュ通知は、そのトピックでビルドされたアプリでのみ受信されます。

1. **Platform アプリケーションの作成**

   1. 「アプリケーション」をクリックし、「Platform アプリケーションの作成」をクリックします。 名前を選択し、プラットフォーム（iOSの場合は APNS、Android™ の場合は GCM）を選択します。 プラットフォームによって異なります。 その他のフィールドには、以下のように入力する必要があります。

      1. APNS の場合、P12 ファイル、パスワード、証明書、および秘密鍵をすべて入力する必要があります。 これらは、手順で取得する必要があります *Apple Push Notification Service （APNS）の使用* 上。
      1. GCM の場合は、API キーを入力する必要があります。 これは、手順で取得する必要があります *Google Cloud Messaging （GCM）サービスの使用* 上。

   1. サポートしているプラットフォームごとに、上記の手順を 1 回繰り返します。 iOSと Android™ の両方にプッシュできるようにするには、2 つの Platform アプリケーションを作成する必要があります。

1. **ID プールの作成**

   1. 使用方法 [匿名](https://console.aws.amazon.com/cognito) 未認証ユーザーの基本データを保存する ID プールを作成します。 現在、Amazon Cognito では「us-east」リージョンと「eu」リージョンのみがサポートされています。
   1. 名前を付け、「未認証の ID へのアクセスを有効にする」チェックボックスをオンにします。
   1. 次のページ（「*Cognito ID では、リソースへのアクセスが必要です*&quot;）を許可をクリックします。
   1. ページの右上にあるリンク「」をクリックします&#x200B;*ID プールを編集」*. ID プール Id が表示されます。 後で使用するために、このテキストを保存します。
   1. 同じページで、「Unauthenticated role」の隣のドロップダウンを選択し、Cognito_という役割があることを確認します&lt;pool name=&quot;&quot;>UnauthRole が選択されました。 変更を保存します。

1. **アクセスを設定**

   1. へのログイン [ID とアクセスの管理](https://console.aws.amazon.com/iam/home) （IAM）。
   1. 「役割」を選択します。
   1. 前の手順で作成した Cognito_というロールをクリックします&lt;youridentitypoolname>Unauth_Role. 表示された「Role ARN」を記録します。
   1. 「インラインポリシー」をまだ開いていない場合は開きます。 oneClick_Cognito_のような名前のポリシーが表示されます。&lt;youridentitypoolname>Unauth_Role_1234567890123。
   1. 「ポリシーを編集」をクリックします。 ポリシードキュメントのコンテンツを次の JSON スニペットに置き換えます。

   <table>
    <tbody>
     <tr>
     <td><p> </p> <p>{</p> <p> 「バージョン」: 「2012-10-17」、</p> <p> "ステートメント": [</p> <p> {</p> <p> "アクション": [</p> <p> 「mobileanalytics:PutEvents」</p> <p> "cognito-sync:*",</p> <p> "SNS:CreatePlatformEndpoint",</p> <p> "SNS:Subscribe"</p> <p> ],</p> <p> "Effect": "Allow",</p> <p> "Resource": [</p> <p> "*"</p> <p> ]</p> <p> }</p> <p> ]</p> <p>}</p> <p> </p> </td>
     </tr>
    </tbody>
    </table>

   1. クリック **ポリシーの適用**.

#### Pushwoosh メッセージサービスの使用 {#using-the-pushwoosh-messaging-service}

Pushwoosh を使用しない場合は、この手順をスキップできます。

Pushwoosh を使用するには：

1. **Pushwoosh に登録**

   1. pushwoosh.comに移動して、アカウントを作成します。

1. **API アクセストークンの作成**

   1. Pushwoosh サイトで、API Access メニュー項目に移動して、API アクセストークンを生成します。 このトークンを安全に記録します。

1. **アプリの作成**

   1. Android™ のサポートでは、GCM API キーを指定する必要があります。
   1. アプリケーションを設定する際に、フレームワークとして「Cordova」を選択します。
   1. iOSをサポートするには、証明書ファイル（.cer）、プッシュ証明書（.p12）、秘密鍵のパスワードを指定する必要があります。これらは、Appleの APNS サイトから入手する必要があります。 「フレームワーク」で、「Cordova」を選択します。
   1. Pushwoosh は、「XXXXX-XXXXX」という形式でそのアプリのアプリ ID を生成します。各 X は 16 進数値（0 ～ F）です。

>[!NOTE]
>
>*AEMで、同じアプリ ID （および他の関連する値：API アクセストークンと GCM ID）で 2 番目のアプリが設定されている場合、AEMの 2 番目のアプリを介して送信されたプッシュ通知は、そのアプリ ID を持つ他のアプリに送信されます。*

### 手順 3：アプリにプッシュサポートを追加する {#step-add-push-support-to-the-app}

#### ContentSync 設定の追加 {#add-contentsync-configuration}

notificationsConfig という名前の 2 つのコンテンツノード（app-config 内に 1 つ、app-config-dev 内に 1 つ）を作成します。

* /content/`<your app>`/shell/jcr:content/page-app/app-config-dev/notificationsConfig
* /content/`<your app>`/shell/jcr:content/page-app/app-config/notificationsConfig

次のプロパティ（.content.xml ファイル）を使用します。
&lt;jcr:root xmlns:jcr=&quot; &lt;span id=&quot; translate=&quot;no&quot; />https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/1.0/index.html](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/1.0/index.html)&quot; xmlns:nt=&quot; [https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/1.0/index.html](https://developer.adobe.com/experience-manager/reference-materials/spec/jcr/1.0/index.html)&quot; jcr:primaryType=&quot;nt:unstructured&quot; excludeProperties=&quot;[appAPIAccessToken]&quot; path=&quot;../../../...&quot;
[targetRootDirectory=&quot;www&quot; type=&quot;notificationsconfig&quot;/>

>[!NOTE]
>
>コンテンツ同期ハンドラーは、これらのノードを探します。ノードがない場合は、page-notifications-config.json ファイルを書き出しません。

#### クライアントライブラリの追加 {#add-client-libraries}

次の手順に従って、プッシュ通知のクライアントライブラリをアプリに追加する必要があります。

CRXDE Liteで：

1. に移動します。 */etc/designs/phonegap/&lt;app name=&quot;&quot;>/clientlibsall に設定します。*
1. プロパティペインで、「埋め込み」セクションをダブルクリックします。
1. 表示されるダイアログボックスで、「+」ボタンをクリックしてクライアントライブラリを追加します。
1. 新しいテキストフィールドに「cq.mobile.push」と追加し、「OK」をクリックします。
1. cq.mobile.push.amazon という名前をもう 1 つ追加し、「OK」をクリックします。
1. 変更内容を保存します。

>[!NOTE]
>
>プッシュ通知を削除するか使用しない場合は、アプリの容量を考慮し、コンソールエラーメッセージを避けるために、アプリからこれらの clientlib を削除します。

### 手順 4：電話をテスト用に準備 {#step-prepare-a-phone-for-testing}

>[!NOTE]
>
>*プッシュ通知の場合、エミュレーターはプッシュ通知を受信できないので、実際のデバイスでテストする必要があります。*

#### IOS {#ios}

iOSの場合は、macOS コンピューターを使用してに参加します [iOS開発者プログラム](https://developer.apple.com/programs/ios/). 一部の企業は、すべての開発者が利用できる企業ライセンスを持っています。

XCode 8.1 では、プッシュ通知を使用する前に、プロジェクトの「機能」タブに移動して、「プッシュ通知」切り替えをオンにする必要があります。

#### Android™ {#android}

CLI を使用してアプリを Android™ 電話にインストールするには（以下を参照） **手順 6 - アプリのビルドとデプロイ**）、最初に電話を「開発者モード」にする必要があります。 参照： [オンデバイス開発者オプションの有効化](https://developer.android.com/tools/device.html#developer-device-options) 詳細を参照してください。

### 手順 5:AEM アプリでのプッシュの設定 {#step-configure-push-on-aem-apps}

設定済みのモバイルデバイスにビルドおよびデプロイする前に、使用するメッセージングサービスの通知設定を指定する必要があります。

1. プッシュ通知に適した認証グループを作成します。
1. 適切なユーザーとしてAEMにログインし、「アプリ」タブをクリックします。
1. アプリをクリックします。
1. Cloud Serviceを管理タイルを見つけ、鉛筆をクリックして、クラウド設定を変更します。
1. 通知設定として、「Amazon SNS 接続」、「Pushwoosh 接続」または「Adobeモバイルサービス」を選択します。
1. プロバイダープロパティを入力し、「送信」をクリックして保存して「完了」をクリックします。 AMS がある場合を除き、この段階ではリモートで検証されません。
1. 設定を管理タイルに入力したCloud Serviceが表示されます。

### 手順 6：アプリのビルドとデプロイ {#step-build-and-deploy-the-app}

**注意：** 手順を参照 [こちら](/help/mobile/building-app-mobile-phonegap.md) PhoneGap アプリケーションの構築時に使用します。

PhoneGap を使用してアプリをビルドおよびデプロイする方法は 2 つあります。

**注意：** プッシュ通知のテストでは、プッシュ通知がプッシュプロバイダー（AppleまたはGoogle）とデバイスの間で個別のプロトコルを使用するので、エミュレーターでは十分ではありません。 現在のMac/PC ハードウェアおよびエミュレーターは、これをサポートしていません。

1. *PhoneGap Build* は、PhoneGap が提供するサービスで、サーバー上でアプリを構築し、デバイスに直接ダウンロードできるようにします。 でPhoneGap Buildドキュメントを参照してください `https://build.phonegap.com/` を参照して、PhoneGap Buildの設定と使用の方法を確認してください。

1. *PhoneGap コマンドラインインターフェイス* （CLI）を使用すると、コマンドラインで豊富な PhoneGap コマンドのセットを使用して、アプリを作成、デバッグ、デプロイできます。 PhoneGap 開発者向けドキュメント （`https://docs.phonegap.com/en/edge/guide_cli_index.md.html#The%20Command-Line%20Interface`）を参照して、PhoneGap CLI の設定方法と使用方法を確認してください。

### 手順 7：プッシュ通知を送信する {#step-send-a-push-notification}

通知を作成して送信するには、次の手順に従います。

1. 通知の作成

   * AEM Mobile アプリのダッシュボードで、プッシュ通知タイルを見つけます。
   * 右上のメニューで、「作成」を選択します。 このボタンは、クラウド設定が最初に設定されるまで使用できません。
   * 通知の作成ウィザードで、タイトルとメッセージを入力し、「作成」ボタンをクリックします。 これで、通知を即時または後で送信する準備が整いました。 編集したり、メッセージやタイトルを変更して保存したりできます。

1. 通知の送信

   * アプリダッシュボードで、プッシュ通知タイルを見つけます。
   * 通知を選択するか、右下の「詳細」ボタン（..）、通知のリストを表示します。 このリストは、通知の送信準備ができているか、既に送信されているか、送信中にエラーが発生したかどうかも示します。
   * 1 つの通知のチェックボックス（のみ）を選択し、リストの上の「通知を送信」ボタンをクリックします。 表示されるダイアログで、通知を「キャンセル」または「送信」する機会が 1 つ与えられます。

1. 結果への対処

   * プッシュ通知サービス（Amazon SNS または Pushwoosh）が Send リクエストを受け取り、有効であることを確認し、ネイティブプロバイダー（APNS および GCM）に正常に送信した場合、ダイアログボックスが閉じてメッセージが表示されません。 通知リストに、その通知のステータスが送信済みとして表示されます。
   * プッシュ送信が失敗した場合、ダイアログボックスに問題を示すメッセージが表示されます。 通知リストには、その通知のステータスがエラーと表示されますが、問題が修正された場合は、通知を再度送信できます。 エラーが発生した場合は、追加のエラー情報がサーバーエラーログに表示されます。
   * iOSと Android™ のプッシュ通知には、プラットフォームの違いがいくつかあることに注意してください。 その中には、

      * CLI を使用してビルドすると、Android™ にデプロイされた後にアプリが起動します。 iOSでは、手動で開始する必要があります。 プッシュ登録ステップは起動時に行われるので、Android™ アプリは（既に開始されて登録されているので）プッシュ通知をすぐに受け取ることができますが、iOS アプリは受け取ることができません。
      * Android™ では、「OK」ボタンのテキストがすべて大文字（およびアプリ内通知に追加されたその他のボタン）で表示されますが、iOSでは表示されません。

AMS プッシュ通知の場合、通知を構成し、AMS サーバーから送信する必要があります。 AMS には、AWSおよび Pushwoosh を使用するAEM通知で提供される機能よりも高度なプッシュ通知機能が用意されています。

>[!NOTE]
>
>*プッシュ通知は配信を保証するものではありません。お知らせに似ています。 誰もが聞こえるように最善の努力をしますが、それらは保証された配信メカニズムではありません。 また、プッシュの配信時間は、1 秒未満から 30 分まで変動する場合があります。*

### プッシュ通知を使用したディープリンクの設定 {#configuring-deep-linking-with-push-notifications}

ディープリンクとは プッシュ通知のコンテキストでは、アプリを開いたり、（開いている場合は）アプリ内の指定された場所にリダイレクトしたりできるようにする手段です。

仕組み プッシュ通知の作成者は、オプションでボタンラベル（「表示」など）を追加できます。 通知にリンクし、視覚的なパスブラウザーを使用して、通知でリンクするページを選択します。 送信された場合、プッシュは通常どおり行われます。ただし、アプリ内メッセージの場合、「OK」ボタンは「解除」ボタンに置き換えられ、新しいボタン（「表示」）が指定されます も表示されます。 「新規」ボタンをクリックすると、アプリ内の指定したページに移動します。 「閉じる」をクリックすると、メッセージが閉じます。

アプリが開いていない場合、シェードは通常どおりに表示されます。 シェードで通知に対してアクションを実行すると、アプリが開き、プッシュ通知で設定された内容に基づいてディープリンクボタンがユーザーに表示されます。

通知を作成し、ボタンのテキストとオプションのディープリンクのリンクパスを追加します。

>[!CAUTION]
>
>ダッシュボードのプッシュ通知タイルにアクセスするには、次の手順に従います。

1. 右上の「編集」をクリックします **Cloud Serviceの管理** タイル。

   ![chlimage_1-108](assets/chlimage_1-108.png)

1. 「」を選択します **Pushwoosh 接続**. 「**次へ**」をクリックします。

   ![chlimage_1-109](assets/chlimage_1-109.png)

1. プロパティの詳細を入力し、 **Submit**.

   ![chlimage_1-110](assets/chlimage_1-110.png)

   設定を送信すると、 **プッシュ通知** タイルがダッシュボードに表示されます。

   ![chlimage_1-111](assets/chlimage_1-111.png)

### 通知を作成ウィザード {#create-notification-wizard}

に達したら、 **プッシュ通知** タイルがダッシュボードに表示されます。通知を作成ウィザードを使用してコンテンツを追加します。

1. の右上隅にある追加記号をクリックします **プッシュ通知** を開くためのタイル **通知の作成ウィザード**.

   ![chlimage_1-112](assets/chlimage_1-112.png)

1. リンクパスの参照アイコンをクリックすると、アプリのコンテンツ構造がユーザーに表示されます。

   パスを選択したら、チェックアイコンをクリックします。

   ![chlimage_1-113](assets/chlimage_1-113.png)

   >[!NOTE]
   >
   >リンクボタンのテキストは、20 文字に制限されています。
   >
   >エンドユーザーがアプリケーションの最新バージョンを持っていない場合、リンクされたパスが使用できない場合、ディープリンクのアクションを確認すると、アプリのメインページに移動します。

1. を入力 **テキストの詳細** が含まれる **通知の作成ウィザード** をクリックして、 **作成**.

   ![chlimage_1-114](assets/chlimage_1-114.png)

   から作成したプッシュ通知をクリックして詳細を開きます **プッシュ通知** タイル。

   プロパティの編集、通知の送信、通知の削除を行うことができます。

   ![chlimage_1-115](assets/chlimage_1-115.png)

>[!NOTE]
>
>**追加情報**:
>
>Pushwoosh およびAmazon SNS は、6.4 リリース以降はサポートされなくなり、Package Share からアドオンとして使用できるようになります。

### 次の手順 {#the-next-steps}

アプリのプッシュ通知の詳細については、次を参照してください。 [AEM Mobile コンテンツのパーソナライゼーション](/help/mobile/phonegap-aem-mobile-content-personalization.md).
