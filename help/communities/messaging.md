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
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 22%

---


# メッセージの設定 {#configure-messaging}

## 概要 {#overview}

AEM Communities のメッセージング機能を使用すると、サインイン済みのサイト訪問者（メンバー）が互いにメッセージを送信できます。このメッセージには、サイトにサインインしているときにアクセス可能です。

コミュニティサイトのメッセージングを有効にするには、[コミュニティサイトの作成](/help/communities/sites-console.md)中にチェックボックスをオンにします。

このページには、デフォルトの設定と可能な調整に関する情報が含まれています。

For additional information for developers, see [Messaging Essentials](/help/communities/essentials-messaging.md).

## メッセージング操作サービス {#messaging-operations-service}

The configuration [AEM Communities Messaging Operations Service](https://localhost:4502/system/console/configMgr/com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl) identifies the endpoint which handles messaging related requests, the folders the service should use for storing messages, and if messages may include file attachments, what file types are allowed.

For community sites created using the `Communities Sites console`, an instance of the service already exists, with the inbox set to `/mail/inbox`.

### コミュニティのメッセージング操作サービス {#community-messaging-operations-service}

以下に示すとおり、[サイト作成ウィザード](/help/communities/sites-console.md)で作成されたサイトには、サービスの設定があります。設定の横にある鉛筆アイコンを選択して、設定を表示または編集できます。

![メッセージング操作](assets/messaging-operations.png)

### 新しい設定を追加 {#add-new-configuration}

To add a new configuration, select the plus &#39;**+**&#39; icon next to the service&#39;s name :

* **Message Fields許可リスト**

   構成メッセージコンポーネントのユーザーが編集および保持できるプロパティを指定します。 新しいフォーム要素を追加する場合は、SRPに保存する必要がある場合は、要素IDを追加する必要があります。 Default is two entries: *subject* and *content*.

* **メッセージボックスのサイズ制限**

   各ユーザーのメッセージボックスの最大バイト数です。 Default is *1073741824* (1 GB).

* **メッセージ数の制限**

   1人のユーザーに許可されるメッセージの合計数です。 値を —1に設定した場合、許可されるメッセージの数に制限はなく、メッセージボックスのサイズ制限に従います。 Default is *10000* (10k).

* **配信エラーの通知**

   オンの場合、メッセージ配信が一部の受信者に失敗した場合に送信者に通知します。 初期設定は&#x200B;*オン*&#x200B;です。

* **失敗配信の送信者ID**

   配信失敗メッセージに表示される送信者の名前。 Default is *failureNotifier*.

* **失敗メッセージテンプレートのパス**

   失敗した配信のメッセージテンプレートルートの絶対パス Default is */etc/notification/messaging/default*.

* **再試行数**

   配信に失敗したメッセージの再送を試行する回数です。デフォルトは *3* です。

* **再試行間の待機**

   送信に失敗したメッセージの再送を試行するまでの間隔（秒数）です。Default is *100* (seconds).

* **更新プールのサイズをカウント**

   カウントの更新に使用される同時スレッドの数。 デフォルトは *10* です。

* **インボックスのパス**

   (*Required*) The path, relative to the user&#39;s node (/home/users/*username*), to use for the `inbox` folder. パスの末尾にスラッシュ「/」を付けることはできません。 Default is */mail/inbox*.

* **送信済みアイテムのパス**

   (*Required*) The path, relative to the user&#39;s node (/home/users/*username*), to use for the `sent items` folder. パスの末尾にスラッシュ「/」を付けることはできません。 Default is */mail/sentitems* .

* **サポートの添付ファイル**

   オンにすると、ユーザーがメッセージに添付ファイルを追加できるようになります。初期設定は&#x200B;*オン*&#x200B;です。

* **グループメッセージを有効にする**

   選択すると、登録済みユーザーは、メンバーのグループに一括メッセージを送信できます。 Default is *deselected*.

* **最大数 全受信者**

   グループメッセージが有効な場合、グループメッセージを一度に送信できる受信者の最大数を指定します。 デフォルトは *100* です。

* **バッチサイズ**

   大規模な受信者グループへの送信時に一括送信処理するメッセージの数です。デフォルトは *100* です。

* **合計添付ファイルサイズ**

   「supportAttachments」をオンにすると、この値によりすべての添付ファイルの最大許容合計サイズ（バイト単位）が指定されます。Default is *104857600* (100 MB).

* **添付ファイルブロックリストタイプの**

   ファイル名拡張子のブロックリスト。先頭に「**.**」というプレフィックス付き）のブラックリストです。そうでないブロックリストに加える場合は、拡張が許可されます。 Extensions may be added or removed using the &#39;**+**&#39; and &#39;**-**&#39; icons.

* **許可されている添付ファイルの種類**

   **(*操作が必要*)** ファイル名拡張子の許可リスト(の逆)。 To allow all filename extensions, except for those blocklisted, use the &#39;**-**&#39; icon to remove the single empty entry.

* **サービスセレクター**

   (*Required*) An absolute path (endpoint) through which the service is called (a virtual resource). The root of the path chosen must be one included in the *Execution Paths* configuration setting of OSGi config [ `Apache Sling Servlet/Script Resolver and Error Handler`](https://localhost:4502/system/console/configMgr/org.apache.sling.servlets.resolver.SlingServletResolver), such as `/bin/`, `/apps/`, and `/services/`. サイトのメッセージング機能に対してこの設定を選択するには、このエンドポイントをの **`Service selector`** 値として指定します `Message List and Compose Message components` ( [メッセージ機能](/help/communities/configure-messaging.md))。

   初期設定は */bin/messaging* です。

* **フィールド許可リスト**

   「 **メッセージフィールド」許可リストを使用します**。

>[!CAUTION]
>
>Each time a `Messaging Operations Service` configuration is opened for edit, if `allowedAttachmentTypes.name` had been removed, an empty entry is re-added to make the property configurable. 1つの空のエントリを指定すると、添付ファイルが有効に無効になります。
>
>To allow all filename extensions, except for those blocklisted, use the &#39;**-**&#39; icon to (again) remove the single empty entry before clicking **Save**.

## Group Messaging {#group-messaging}

登録済みユーザーがダイレクトメッセージを一括してユーザーグループに送信できるようにするには、次の2つの **Messaging Operation Services** 設定のインスタンスで **、「グループメッセージを** 有効にする」を必ず有効にしてください。

* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-console`
* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-messaging`

**Messaging Operationsサービス：ソーシャルコンソール**

![social-console-op-service](assets/social-console-op-service.png)

**Messaging Operationsサービス：社会的メッセージ**

![social-message-op-service](assets/social-message-op-service.png)

## トラブルシューティング {#troubleshooting}

One way to troubleshoot problems is to enable [debugging messages in the log.](/help/sites-administering/troubleshooting.md)

[個々のサービス用のロガーとライター](/help/sites-deploying/configure-logging.md#loggers-and-writers-for-individual-services)も参照してください。

The package to monitor is `com.adobe.cq.social.messaging`.
