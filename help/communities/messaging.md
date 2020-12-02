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


# メッセージの構成{#configure-messaging}

## 概要 {#overview}

AEM Communities のメッセージング機能を使用すると、サインイン済みのサイト訪問者（メンバー）が互いにメッセージを送信できます。このメッセージには、サイトにサインインしているときにアクセス可能です。

コミュニティサイトのメッセージングを有効にするには、[コミュニティサイトの作成](/help/communities/sites-console.md)中にチェックボックスをオンにします。

このページには、デフォルトの設定と可能な調整に関する情報が含まれています。

開発者向けの追加情報については、[Messaging Essentials](/help/communities/essentials-messaging.md)を参照してください。

## メッセージング操作サービス {#messaging-operations-service}

構成[AEM Communitiesメッセージング操作サービス](https://localhost:4502/system/console/configMgr/com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl)は、メッセージング関連の要求を処理するエンドポイント、サービスがメッセージの格納に使用するフォルダー、およびメッセージに添付ファイルが含まれる場合は、許可されるファイルの種類を識別します。

`Communities Sites console`を使用して作成されたコミュニティサイトでは、サービスのインスタンスが既に存在し、インボックスが`/mail/inbox`に設定されています。

### コミュニティのメッセージング操作サービス {#community-messaging-operations-service}

以下に示すとおり、[サイト作成ウィザード](/help/communities/sites-console.md)で作成されたサイトには、サービスの設定があります。設定の横にある鉛筆アイコンを選択して、設定を表示または編集できます。

![メッセージング操作](assets/messaging-operations.png)

### 新しい設定を追加 {#add-new-configuration}

新しい設定を追加するには、サービス名の横にあるプラス「**+**」アイコンを選択します。

* **Message Fields許可リスト**

   構成メッセージコンポーネントのユーザーが編集および保持できるプロパティを指定します。 新しいフォーム要素を追加する場合は、SRPに保存する必要がある場合は、要素IDを追加する必要があります。 初期設定は2つのエントリです。*subject* and *content*.

* **メッセージボックスのサイズ制限**

   各ユーザーのメッセージボックスの最大バイト数です。 デフォルトは&#x200B;*1073741824* (1 GB)です。

* **メッセージ数の制限**

   1人のユーザーに許可されるメッセージの合計数です。 値を —1に設定した場合、許可されるメッセージの数に制限はなく、メッセージボックスのサイズ制限に従います。 初期設定は&#x200B;*10000* (10k)です。

* **配信エラーの通知**

   オンの場合、メッセージ配信が一部の受信者に失敗した場合に送信者に通知します。 初期設定は&#x200B;*オン*&#x200B;です。

* **失敗配信の送信者ID**

   配信失敗メッセージに表示される送信者の名前。 初期設定は&#x200B;*failureNotifier*&#x200B;です。

* **失敗メッセージテンプレートのパス**

   失敗した配信のメッセージテンプレートルートの絶対パス デフォルトは&#x200B;*/etc/notification/messaging/default*&#x200B;です。

* **再試行数**

   配信に失敗したメッセージの再送を試行する回数です。デフォルトは *3* です。

* **再試行間の待機**

   送信に失敗したメッセージの再送を試行するまでの間隔（秒数）です。初期設定は&#x200B;*100* （秒）です。

* **更新プールのサイズをカウント**

   カウントの更新に使用される同時スレッドの数。 デフォルトは *10* です。

* **インボックスのパス**

   （*必須*）`inbox`フォルダーに使用する、ユーザーのノードを基準とした相対パス(/home/users/*username*)。 パスの末尾にスラッシュ「/」を付けることはできません。 初期設定は&#x200B;*/mail/inbox*&#x200B;です。

* **送信済みアイテムのパス**

   （*必須*）`sent items`フォルダーに使用する、ユーザーのノードを基準とした相対パス(/home/users/*username*)。 パスの末尾にスラッシュ「/」を付けることはできません。 初期設定は&#x200B;*/mail/sentitems*&#x200B;です。

* **サポートの添付ファイル**

   オンにすると、ユーザーがメッセージに添付ファイルを追加できるようになります。初期設定は&#x200B;*オン*&#x200B;です。

* **グループメッセージを有効にする**

   選択すると、登録済みユーザーは、メンバーのグループに一括メッセージを送信できます。 初期設定は&#x200B;*未選択*&#x200B;です。

* **最大数全受信者**

   グループメッセージが有効な場合、グループメッセージを一度に送信できる受信者の最大数を指定します。 デフォルトは *100* です。

* **バッチサイズ**

   大規模な受信者グループへの送信時に一括送信処理するメッセージの数です。デフォルトは *100* です。

* **合計添付ファイルサイズ**

   「supportAttachments」をオンにすると、この値によりすべての添付ファイルの最大許容合計サイズ（バイト単位）が指定されます。初期設定は&#x200B;*104857600*(100 MB)です。

* **添付ファイルブロックリストタイプの**

   ファイル名拡張子のブロックリスト。先頭に「**」が付きます。**」というプレフィックス付き）のブラックリストです。そうでないブロックリストに加える場合は、拡張が許可されます。 拡張子は、「**+**」アイコンと「**-**」アイコンを使用して追加または削除できます。

* **許可されている添付ファイルの種類**

   **(*操作が必要*** )ファイル名拡張子の許可リスト(の逆)。これらを除くすべてのファイル名拡張子を許可するには、ブロックリストに加える&#39;**-**&#39;アイコンを使用して、空のエントリを1つ削除します。

* **サービスセレクター**

   （*必須*）サービスが呼び出される絶対パス（エンドポイント）です（仮想リソース）。 選択するパスのルートは、*OSGi config [ `Apache Sling Servlet/Script Resolver and Error Handler`](https://localhost:4502/system/console/configMgr/org.apache.sling.servlets.resolver.SlingServletResolver)の&lt;a0/>Execution Paths*&#x200B;構成設定（`/bin/`、`/apps/`、`/services/`など）に含まれている必要があります。 サイトのメッセージング機能に対してこの設定を選択するには、このエンドポイントを`Message List and Compose Message components`の&#x200B;**`Service selector`**&#x200B;値として指定します（[メッセージ機能](/help/communities/configure-messaging.md)を参照）。

   初期設定は */bin/messaging* です。

* **フィールド許可リスト**

   **メッセージフィールド許可リスト**&#x200B;を使用します。

>[!CAUTION]
>
>編集用に`Messaging Operations Service`設定が開かれるたびに、`allowedAttachmentTypes.name`が削除されると、空のエントリが再度追加され、プロパティを設定可能にします。 1つの空のエントリを指定すると、添付ファイルが有効に無効になります。
>
>これらを除くすべてのファイル名拡張子を許可するには、ブロックリストに加える&#39;**-**&#39;アイコンを使用して（もう一度）空のエントリを1つ削除してから、**「保存**」をクリックします。

## グループメッセージ{#group-messaging}

登録ユーザーがダイレクトメッセージを一括してユーザーグループに送信できるようにするには、次の2つの&#x200B;**メッセージング操作サービス**&#x200B;構成の&#x200B;**Enable group messaging**&#x200B;に必ず従ってください。

* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-console`
* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-messaging`

**Messaging Operationsサービス：ソーシャルコンソール**

![social-console-op-service](assets/social-console-op-service.png)

**Messaging Operationsサービス：社会的メッセージ**

![social-message-op-service](assets/social-message-op-service.png)

## トラブルシューティング {#troubleshooting}

問題のトラブルシューティングの1つの方法は、ログで[デバッグメッセージを有効にすることです。](/help/sites-administering/troubleshooting.md)

[個々のサービス用のロガーとライター](/help/sites-deploying/configure-logging.md#loggers-and-writers-for-individual-services)も参照してください。

監視するパッケージは`com.adobe.cq.social.messaging`です。
