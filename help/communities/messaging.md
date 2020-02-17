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
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# メッセージの設定{#configure-messaging}

## 概要 {#overview}

AEM Communities のメッセージング機能を使用すると、サインイン済みのサイト訪問者（メンバー）が互いにメッセージを送信できます。このメッセージには、サイトにサインインしているときにアクセス可能です。

コミュニティサイトのメッセージングを有効にするには、[コミュニティサイトの作成](/help/communities/sites-console.md)中にチェックボックスをオンにします。

このページには、デフォルト設定と可能な調整に関する情報が含まれています。

For additional information for developers, see [Messaging Essentials](/help/communities/essentials-messaging.md).

## メッセージング操作サービス {#messaging-operations-service}

The configuration [AEM Communities Messaging Operations Service](https://localhost:4502/system/console/configMgr/com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl) identifies the endpoint which handles messaging related requests, the folders the service should use for storing messages, and if messages may include file attachments, what file types are allowed.

For community sites created using the `Communities Sites console`, an instance of the service already exists, with the inbox set to `/mail/inbox`.

### コミュニティのメッセージング操作サービス {#community-messaging-operations-service}

以下に示すとおり、[サイト作成ウィザード](/help/communities/sites-console.md)で作成されたサイトには、サービスの設定があります。設定の横にある鉛筆アイコンを選択して、設定を表示または編集できます。

![メッセージ操作](assets/messaging-operations.png)

### 新しい設定を追加 {#add-new-configuration}

To add a new configuration, select the plus &#39;**+**&#39; icon next to the service&#39;s name :

* **Message Fields Whitelist**&#x200B;ユーザーが編集および保持できる、メッセージを作成コンポーネントのプロパティを指定します。新しいフォーム要素を追加する場合、SRPに保存する必要がある場合は、要素IDを追加する必要があります。 Default is two entries: *subject* and *content*.

* **Message box size limit**&#x200B;各ユーザーのメッセージボックスの最大バイト数。 初期設定は*1073741824 *(1 GB)です。

* **Message count limit**：ユーザーごとに許可されるメッセージの合計数です。 値を —1に設定した場合、許可されるメッセージの数に制限はなく、メッセージボックスのサイズ制限に従います。 Default is *10000* (10k).

* **配信失敗を通知する**：オンにすると、メッセージ配信が一部の受信者に失敗した場合に送信者に通知します。 初期設定は&#x200B;*オン*&#x200B;です。

* **配信失敗メッセージに表**&#x200B;示される送信者の名前。 Default is *failureNotifier*.

* **失敗メッセージテンプレート**&#x200B;パス配信に失敗したメッセージテンプレートルートの絶対パス。 Default is */etc/notification/messaging/default*.

* **[再試行回数**]配信に失敗したメッセージの再送を試みる回数。 デフォルトは *3* です。

* **再試行間隔**：送信に失敗した場合にメッセージを再送信する間隔を秒数で指定します。 初期設定は*100 *（秒）です。

* **カウント更新プールサイズ**&#x200B;カウント更新に使用される同時スレッドの数。 デフォルトは *10* です。

* **「Inbox path**(*Required*)」：フォルダーに使用する、ユーザーのノード(/home/users/*username*)を基準とするパスで **`inbox`** す。 パスの末尾にスラッシュ「/」を付けることはできません。 Default is */mail/inbox.*

* **送信済みアイテムのパス**(必須&#x200B;*)：フォルダーに使用する、ユーザーのノードを基準とするパス(/home/users/* username *)***`send items`** 。 パスの末尾にスラッシュ「/」を付けることはできません。 Default is */mail/sentitems* .

* **添付ファイルのサ**&#x200B;ポートこのチェックボックスをオンにすると、ユーザーはメッセージに添付ファイルを追加できます。 初期設定は&#x200B;*オン*&#x200B;です。

* **グループメッセージを有効**&#x200B;にする：選択すると、登録ユーザーはメンバーのグループにバルクメッセージを送信できます。 Default is *deselected*.

* **最大数 合計受信者数**&#x200B;グループメッセージが有効な場合は、一度に送信できる受信者の最大数を指定します。 デフォルトは *100* です。

* **バッチサ**&#x200B;イズ大きな受信者グループに送信する際に、送信用に一括して送信するメッセージの数です。 デフォルトは *100* です。

* **Total attachment size** supportAttachmentsがチェックされている場合、この値はすべての添付ファイルの許容される最大合計サイズ（バイト単位）を指定します。 Default is *104857600* (100 MB).

* **添付ファイルタイプ黒** listファイル拡張子のブラックリスト。先頭に「**.**」というプレフィックス付き）のブラックリストです。ブラックリストに記載されていない場合は、拡張が許可されます。 Extensions may be added or removed using the &#39;**+**&#39; and &#39;**-**&#39; icons.

* **許可されている添付ファイルの種類**
   **(アク&#x200B;*ションが必要*)** 、ファイル拡張子のホワイトリスト（ブラックリストの逆）。 To allow all filename extensions, except for those blacklisted, use the &#39;**-**&#39; icon to remove the single empty entry.

* **サービスセレク**&#x200B;ター&#x200B;*(必須*)サービスが呼び出される絶対パス（エンドポイント）（仮想リソース）。 The root of the path chosen must be one included in the *Execution Paths* configuration setting of OSGi config [ `Apache Sling Servlet/Script Resolver and Error Handler`](https://localhost:4502/system/console/configMgr/org.apache.sling.servlets.resolver.SlingServletResolver), such as `/bin/`, `/apps/`, and `/services/`. サイトのメッセージング機能に対してこの設定を選択するには、このエンドポイントをの値とし **`Service selector`** て指定します( `Message List and Compose Message components` 「メッセージ [機能](/help/communities/configure-messaging.md)」を参照)。
初期設定は */bin/messaging* です。

* **フィールドホワイトリスト**&#x200B;メッセージ **フィールドのホワイトリストを使用**。

>[!CAUTION]
>
>Each time a `Messaging Operations Service` configuration is opened for edit, if `allowedAttachmentTypes.name` had been removed, an empty entry is re-added to make the property configurable. 1つの空のエントリを指定すると、添付ファイルが事実上無効になります。
>
>To allow all filename extensions, except for those blacklisted, use the &#39;**-**&#39; icon to (again) remove the single empty entry before clicking **Save**.

## Group Messaging {#group-messaging}

登録ユーザーがダイレクトメッセージを一括してユーザーグループに送信できるようにするには、次の **Messaging Operation Services設定の2つのインスタンスで、**Enable group messaging **を必ず有効にし** てください。

* com.adobe.cq.sosical.messaging.client.endpoints.impl.MessagingOperationsServiceImpl～social-console
* com.adobe.cq.sosical.messaging.client.endpoints.impl.MessagingOperationsServiceImpl～social-messaging

**Messaging Operationsサービス：ソーシャルコンソール**

![social-console-op-service](assets/social-console-op-service.png)

**Messaging Operationsサービス：社会的メッセージング**

![social-message-op-service](assets/social-message-op-service.png)

## トラブルシューティング {#troubleshooting}

One way to troubleshoot problems is to enable [debugging messages in the log.](/help/sites-administering/troubleshooting.md)

[個々のサービス用のロガーとライター](/help/sites-deploying/configure-logging.md#loggers-and-writers-for-individual-services)も参照してください。

The package to monitor is `com.adobe.cq.social.messaging`.
