---
title: メッセージの設定
seo-title: メッセージングの設定
description: Communities のメッセージング
seo-description: Communities のメッセージング
uuid: 159dcf9d-7948-4a3d-9f51-a5b4d03e172b
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 232a0ec1-8dfc-41ec-84cc-69f9db494ea0
docset: aem65
role: Administrator
exl-id: ee94f093-fd14-49f2-9990-fbe853d924b1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 22%

---

# メッセージの設定{#configure-messaging}

## 概要 {#overview}

AEM Communities のメッセージング機能を使用すると、サインイン済みのサイト訪問者（メンバー）が互いにメッセージを送信できます。このメッセージには、サイトにサインインしているときにアクセス可能です。

コミュニティサイトのメッセージングを有効にするには、[コミュニティサイトの作成](/help/communities/sites-console.md)中にチェックボックスをオンにします。

このページには、デフォルト設定と可能な調整に関する情報が含まれています。

開発者向けの追加情報については、[メッセージングの基本事項](/help/communities/essentials-messaging.md)を参照してください。

## メッセージング操作サービス {#messaging-operations-service}

設定[AEM Communities Messaging Operations Service](https://localhost:4502/system/console/configMgr/com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl)は、メッセージ関連の要求を処理するエンドポイント、メッセージの保存に使用するフォルダー、メッセージに添付ファイルが含まれる場合は許可されるファイルタイプを識別します。

`Communities Sites console`を使用して作成されたコミュニティサイトでは、サービスのインスタンスが既に存在し、インボックスが`/mail/inbox`に設定されています。

### コミュニティのメッセージング操作サービス {#community-messaging-operations-service}

以下に示すとおり、[サイト作成ウィザード](/help/communities/sites-console.md)で作成されたサイトには、サービスの設定があります。設定の横にある鉛筆アイコンを選択すると、設定を表示または編集できます。

![messaging-operations](assets/messaging-operations.png)

### 新しい設定を追加 {#add-new-configuration}

新しい設定を追加するには、サービス名の横にあるプラス「**+**」アイコンを選択します。

* **メッセージフィールドの許可リスト**

   ユーザーが編集および保持できるメッセージを作成コンポーネントのプロパティを指定します。 新しいフォーム要素を追加する場合、SRPに格納するには、要素IDを追加する必要があります。 デフォルトは2つのエントリです。*subject*&#x200B;と&#x200B;*content*。

* **メッセージボックスのサイズ制限**

   各ユーザーのメッセージボックスの最大バイト数。 初期設定は&#x200B;*1073741824*(1 GB)です。

* **メッセージ数の制限**

   ユーザーごとに許可されるメッセージの合計数です。 値を —1に設定した場合、許可されるメッセージ数は無制限で、メッセージボックスのサイズ制限に従います。 初期設定は&#x200B;*10000* (10k)です。

* **配信エラーの通知**

   オンにすると、メッセージの配信が一部の受信者に失敗した場合に送信者に通知します。 初期設定は&#x200B;*オン*&#x200B;です。

* **配信失敗の送信者ID**

   配信に失敗したメッセージに表示される送信者の名前。 初期設定は&#x200B;*failureNotifier*&#x200B;です。

* **失敗メッセージテンプレートのパス**

   配信に失敗したメッセージテンプレートのルートへの絶対パス。 初期設定は&#x200B;*/etc/notification/messaging/default*&#x200B;です。

* **再試行の回数**

   配信に失敗したメッセージの再送を試行する回数です。デフォルトは *3* です。

* **再試行の間隔**

   送信に失敗したメッセージの再送を試行するまでの間隔（秒数）です。初期設定は&#x200B;*100*（秒）です。

* **更新プールのサイズのカウント**

   カウントの更新に使用する同時スレッドの数。 デフォルトは *10* です。

* **インボックスパス**

   （*必須*）`inbox`フォルダーに使用する、ユーザーのノード(/home/users/*username*)を基準としたパス。 パスの末尾にフォワードスラッシュ「/」を付けることはできません。 初期設定は&#x200B;*/mail/inbox*&#x200B;です。

* **送信済みアイテムのパス**

   （*必須*）`sent items`フォルダーに使用する、ユーザーのノード(/home/users/*username*)を基準としたパス。 パスの末尾にフォワードスラッシュ「/」を付けることはできません。 初期設定は&#x200B;*/mail/sentitems*&#x200B;です。

* **サポートの添付ファイル**

   オンにすると、ユーザーがメッセージに添付ファイルを追加できるようになります。初期設定は&#x200B;*オン*&#x200B;です。

* **グループメッセージの有効化**

   選択すると、登録ユーザーはメンバーグループに一括メッセージを送信できます。 初期設定は&#x200B;*選択解除*&#x200B;です。

* **最大数受信者の合計**

   グループメッセージが有効な場合は、一度に送信できるグループメッセージの受信者の最大数を指定します。 デフォルトは *100* です。

* **バッチサイズ**

   大規模な受信者グループへの送信時に一括送信処理するメッセージの数です。デフォルトは *100* です。

* **合計添付ファイルサイズ**

   「supportAttachments」をオンにすると、この値によりすべての添付ファイルの最大許容合計サイズ（バイト単位）が指定されます。初期設定は&#x200B;*104857600*(100 MB)です。

* **添付ファイルの種類のブロックリスト**

   ファブロックリストイル名拡張子の。先頭に「**」が付きます。**」というプレフィックス付き）のブラックリストです。選択しなブロックリストに加えるい場合、拡張機能は許可されます。 拡張は、「**+**」および「**-**」アイコンを使用して追加または削除できます。

* **許可されている添付ファイルの種類**

   **(*アクションが必要*)** フ許可リストァイル拡張子の(拡張子の逆ブロックリスト)。ファイル名の拡張子をすべて許可するにブロックリストに加えるは、「**-**」アイコンを使用して、1つの空のエントリを削除します。

* **サービスセレクター**

   （*必須*）サービスの呼び出しに使用する絶対パス（エンドポイント）（仮想リソース）。 選択するパスのルートは、*OSGi設定[ `Apache Sling Servlet/Script Resolver and Error Handler`](https://localhost:4502/system/console/configMgr/org.apache.sling.servlets.resolver.SlingServletResolver)の設定（`/bin/`、`/apps/`、`/services/`など）に含まれているパスである必要があります。*&#x200B;サイトのメッセージング機能に対してこの設定を選択するには、このエンドポイントを`Message List and Compose Message components`の&#x200B;**`Service selector`**&#x200B;値として提供します（[メッセージ機能](/help/communities/configure-messaging.md)を参照）。

   初期設定は */bin/messaging* です。

* **フィールドの許可リスト**

   **メッセージフィールド許可リスト**&#x200B;を使用します。

>[!CAUTION]
>
>`Messaging Operations Service`設定を編集用に開くたびに、`allowedAttachmentTypes.name`が削除された場合は、空のエントリが再追加され、プロパティを設定できるようになります。 1つの空のエントリを指定すると、添付ファイルが無効になります。
>
>ファイル名の拡張子をすべて許可するにブロックリストに加えるは、「**-**」アイコンを使用して（もう一度）1つの空のエントリを削除してから、「**保存**」をクリックします。

## グループメッセージ{#group-messaging}

登録ユーザーがダイレクトメッセージを一括でユーザーグループに送信できるようにするには、次の2つの&#x200B;**Messaging Operation Services**&#x200B;設定で、**グループメッセージング**&#x200B;を有効にします。

* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-console`
* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-messaging`

**メッセージング操作サービス：ソーシャルコンソール**

![social-console-op-service](assets/social-console-op-service.png)

**メッセージング操作サービス：ソーシャルメッセージ**

![social-message-op-service](assets/social-message-op-service.png)

## トラブルシューティング {#troubleshooting}

問題をトラブルシューティングする1つの方法は、ログで[メッセージのデバッグを有効にすることです。](/help/sites-administering/troubleshooting.md)

[個々のサービス用のロガーとライター](/help/sites-deploying/configure-logging.md#loggers-and-writers-for-individual-services)も参照してください。

監視するパッケージは`com.adobe.cq.social.messaging`です。
