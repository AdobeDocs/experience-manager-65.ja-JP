---
title: メッセージの設定
seo-title: Configuring Messaging
description: Communities のメッセージング
seo-description: Communities messaging
uuid: 159dcf9d-7948-4a3d-9f51-a5b4d03e172b
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 232a0ec1-8dfc-41ec-84cc-69f9db494ea0
docset: aem65
role: Admin
exl-id: ee94f093-fd14-49f2-9990-fbe853d924b1
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '822'
ht-degree: 22%

---

# メッセージの設定 {#configure-messaging}

## 概要 {#overview}

AEM Communities のメッセージング機能を使用すると、サインイン済みのサイト訪問者（メンバー）が互いにメッセージを送信できます。このメッセージには、サイトにサインインしているときにアクセス可能です。

コミュニティサイトのメッセージングを有効にするには、[コミュニティサイトの作成](/help/communities/sites-console.md)中にチェックボックスをオンにします。

このページには、デフォルト設定に関する情報と、可能な調整が含まれています。

開発者向けの追加情報については、 [メッセージの基本事項](/help/communities/essentials-messaging.md).

## メッセージング操作サービス {#messaging-operations-service}

設定 [AEM Communities Messaging Operations Service](https://localhost:4502/system/console/configMgr/com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl) は、メッセージング関連の要求を処理するエンドポイント、メッセージの保存に使用するフォルダー、添付ファイルが含まれる場合はどのファイルタイプを使用できるかを指定します。

を使用して作成されたコミュニティサイトの場合 `Communities Sites console`、サービスのインスタンスは既に存在し、インボックスはに設定されています `/mail/inbox`.

### コミュニティのメッセージング操作サービス {#community-messaging-operations-service}

以下に示すとおり、[サイト作成ウィザード](/help/communities/sites-console.md)で作成されたサイトには、サービスの設定があります。設定の横にある鉛筆アイコンを選択すると、設定を表示または編集できます。

![messaging-operations](assets/messaging-operations.png)

### 新しい設定を追加 {#add-new-configuration}

新しい設定を追加するには、プラス記号「**+**「 」アイコンがサービス名の横に表示されます。

* **メッセージフィールド許可リスト**

   ユーザーが編集および保持できるメッセージを作成コンポーネントのプロパティを指定します。 新しいフォーム要素を追加する場合、SRP に格納するには、要素 ID を追加する必要があります。 デフォルトでは、次の 2 つのエントリです。 *件名* および *コンテンツ*.

* **メッセージボックスのサイズ制限**

   各ユーザーのメッセージボックスの最大バイト数です。 デフォルトはです。 *1073741824* (1 GB)。

* **メッセージ数の制限**

   ユーザーごとに許可されるメッセージの合計数です。 -1 の値は、許可されるメッセージ数に制限がないことを示し、メッセージボックスのサイズ制限に従います。 デフォルトはです。 *10000* (10k)。

* **配信エラーを通知**

   オンにすると、メッセージの配信が一部の受信者に失敗した場合に送信者に通知します。 初期設定は&#x200B;*オン*&#x200B;です。

* **配信送信者 ID の失敗**

   配信に失敗したメッセージに表示される送信者の名前。 デフォルトはです。 *failureNotifier*.

* **失敗メッセージテンプレートのパス**

   配信に失敗したメッセージテンプレートのルートへの絶対パス。 デフォルトはです。 */etc/notification/messaging/default*.

* **再試行の回数**

   配信に失敗したメッセージの再送を試行する回数です。デフォルトは *3* です。

* **再試行を待つ**

   送信に失敗したメッセージの再送を試行するまでの間隔（秒数）です。デフォルトはです。 *100* （秒）。

* **更新プールのサイズをカウント**

   カウントの更新に使用する同時スレッドの数。 デフォルトは *10* です。

* **インボックスのパス**

   (*必須*) ユーザーのノードを基準としたパス (/home/users/*ユーザー名*)、 `inbox` フォルダー。 パスの末尾にスラッシュ「/」を付けることはできません。 デフォルトはです。 */mail/inbox*.

* **送信済みアイテムのパス**

   (*必須*) ユーザーのノードを基準としたパス (/home/users/*ユーザー名*)、 `sent items` フォルダー。 パスの末尾にスラッシュ「/」を付けることはできません。 デフォルトはです。 */mail/sentitems* .

* **添付ファイルのサポート**

   オンにすると、ユーザーがメッセージに添付ファイルを追加できるようになります。初期設定は&#x200B;*オン*&#x200B;です。

* **グループメッセージを有効にする**

   選択すると、登録ユーザーはメンバーのグループに一括メッセージを送信できます。 デフォルトはです。 *選択解除*.

* **最大数 （合計受信者数）**

   グループメッセージが有効な場合は、一度に送信できるグループメッセージの最大受信者数を指定します。 デフォルトは *100* です。

* **バッチサイズ**

   大規模な受信者グループへの送信時に一括送信処理するメッセージの数です。デフォルトは *100* です。

* **合計添付ファイルサイズ**

   「supportAttachments」をオンにすると、この値によりすべての添付ファイルの最大許容合計サイズ（バイト単位）が指定されます。デフォルトはです。 *104857600* (100 MB)。

* **添付ファイルタイプのブロックリスト**

   ファイルブロックリスト名拡張子の。先頭に「 」が付く&#x200B;**.**」というプレフィックス付き）のブラックリストです。選択しなブロックリストに加えるい場合、拡張機能は許可されます。 拡張機能は、「 」を使用して追加または削除できます&#x200B;**+**&#39;および&#39;**-**&#39;アイコン。

* **許可されている添付ファイルのタイプ**

   **(*アクションが必要です*)** ファイル許可リスト名の拡張子の ( ファイルの逆ブロックリスト)。 ファイル名の拡張子をすべて許可する（ファイル名を除く）にブロックリストに加えるは、「**-**「 」アイコンを使用して、1 つの空のエントリを削除します。

* **サービスセレクター**

   (*必須*) サービスの呼び出しに使用される絶対パス（エンドポイント）です（仮想リソース）。 選択したパスのルートは、 *実行パス* OSGi 設定の設定 [ `Apache Sling Servlet/Script Resolver and Error Handler`](https://localhost:4502/system/console/configMgr/org.apache.sling.servlets.resolver.SlingServletResolver)例： `/bin/`, `/apps/`、および `/services/`. サイトのメッセージング機能でこの設定を選択するには、このエンドポイントが **`Service selector`** の値 `Message List and Compose Message components` ( [メッセージ機能](/help/communities/configure-messaging.md)) をクリックします。

   初期設定は */bin/messaging* です。

* **フィールドの許可リスト**

   用途 **メッセージフィールド許可リスト**.

>[!CAUTION]
>
>毎回 a `Messaging Operations Service` 設定を開いて編集する ( `allowedAttachmentTypes.name` が削除された場合、空のエントリが再度追加され、プロパティを設定できるようになりました。 1 つの空のエントリを指定すると、添付ファイルが無効になります。
>
>ファイル名の拡張子をすべて許可する（ファイル名を除く）にブロックリストに加えるは、「**-**「 」アイコンをクリックする前に空のエントリを（再度）1 つ削除します。 **保存**.

## グループメッセージ {#group-messaging}

登録ユーザーがダイレクトメッセージを一括でユーザーグループに送信できるようにするには、 **グループメッセージを有効にする** 次の 2 つの例では **メッセージング操作サービス** 設定：

* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-console`
* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-messaging`

**メッセージング操作サービス：ソーシャルコンソール**

![social-console-op-service](assets/social-console-op-service.png)

**メッセージング操作サービス：ソーシャルメッセージ**

![social-message-op-service](assets/social-message-op-service.png)

## トラブルシューティング {#troubleshooting}

問題をトラブルシューティングする 1 つの方法は、 [ログにメッセージをデバッグする。](/help/sites-administering/troubleshooting.md)

[個々のサービス用のロガーとライター](/help/sites-deploying/configure-logging.md#loggers-and-writers-for-individual-services)も参照してください。

監視するパッケージは次のとおりです。 `com.adobe.cq.social.messaging`.
