---
title: メッセージングの設定
description: ログインしたサイト訪問者（メンバー）がメッセージを相互に送信する機能を提供する、AEM Communitiesのメッセージング機能について説明します。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: ee94f093-fd14-49f2-9990-fbe853d924b1
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 0%

---

# メッセージングの設定 {#configure-messaging}

## 概要 {#overview}

AEM Communitiesのメッセージング機能は、ログインしたサイト訪問者（メンバー）が、サイトへのログイン時にアクセス可能なメッセージを相互に送信する機能を提供します。

[&#x200B; コミュニティサイトの作成 &#x200B;](/help/communities/sites-console.md) 中にボックスをオンにすることで、コミュニティサイトでメッセージングが有効になります。

このページには、デフォルトの設定と可能な調整に関する情報が含まれています。

開発者向けの追加情報については、[&#x200B; メッセージングの基本事項 &#x200B;](/help/communities/essentials-messaging.md) を参照してください。

## メッセージング操作サービス {#messaging-operations-service}

設定 [AEM Communities Messaging Operations Service](https://localhost:4502/system/console/configMgr/com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl) は、メッセージング関連の要求を処理するエンドポイント、メッセージの保存にサービスが使用するフォルダー、およびメッセージに添付ファイルが含まれる場合は、許可されるファイルの種類を特定します。

`Communities Sites console` を使用して作成されたコミュニティサイトの場合は、サービスのインスタンスが存在し、インボックスが `/mail/inbox` に設定されています。

### コミュニティメッセージング運用サービス {#community-messaging-operations-service}

次に示すように、[&#x200B; サイト作成ウィザード &#x200B;](/help/communities/sites-console.md) で作成されたサイトには、サービスの設定が存在します。 設定は、設定の横にある鉛筆アイコンを選択して表示または編集できます。

![messaging-operations](assets/messaging-operations.png)

### 新しい設定を追加 {#add-new-configuration}

設定を追加するには、サービス名の横にあるプラス「**+**」アイコンを選択します。

* 許可リストに加える **メッセージフィールド**

  ユーザーが編集および保持できるメッセージの作成コンポーネントのプロパティを指定します。 新しいフォーム要素を追加する場合、SRP に保存するには要素 ID を追加する必要があります。 デフォルトでは、*subject* と *content* の 2 つのエントリが指定されています。

* **メッセージボックスのサイズ制限**

  各ユーザーのメッセージ ボックスの最大バイト数です。 デフォルトは *1073741824* （1 GB）です。

* **メッセージ数の制限**

  ユーザーごとに許可されるメッセージの合計数。 値が–1 の場合は、メッセージ ボックスのサイズ制限に従って、メッセージの数に制限がないことを示します。 デフォルトは *10000* （10k）です。

* **配信エラーを通知**

  オンにすると、一部の受信者にメッセージ配信が失敗した場合に送信者に通知します。 デフォルトは *オン* です。

* **配信送信者 ID のエラー**

  配信の失敗メッセージに表示される送信者の名前。 デフォルトは *failureNotifier* です。

* **失敗メッセージテンプレートパス**

  配信失敗メッセージテンプレートルートの絶対パス。 デフォルトは、*/etc/notification/messaging/default* です。

* **再試行の数**

  配信に失敗したメッセージの再送信を試行する回数。 デフォルトは *3* です。

* **再試行間の待機**

  送信に失敗したときにメッセージを再送信する間隔を秒単位で指定します。 デフォルト値は *100* （秒）です。

* **カウント更新プールのサイズ**

  カウントの更新に使用される同時スレッドの数。 デフォルトは *10* です。

* **インボックスパス**

  （*必須*） `inbox` フォルダーに使用するユーザーのノードに対する相対パス（/home/users/*username*）。 パスの末尾にスラッシュ「/」を付けることはできません。 デフォルトは */mail/inbox* です。

* **送信済み項目のパス**

  （*必須*） `sent items` フォルダーに使用するユーザーのノードに対する相対パス（/home/users/*username*）。 パスの末尾にスラッシュ「/」を付けることはできません。 デフォルトは */mail/sentitems* です。

* **サポートの添付ファイル**

  オンにすると、ユーザーは、メッセージに添付ファイルを追加できます。 デフォルトは *オン* です。

* **グループメッセージングの有効化**

  選択した場合、登録ユーザーはメンバーのグループに一括メッセージを送信できます。 デフォルトは *選択解除* です。

* **最大数 合計受信者数のうち**

  グループメッセージが有効な場合、グループメッセージを一度に送信できる最大受信者数を指定します。 デフォルトは *100* です。

* **バッチサイズ**

  多数の受信者に送信する際に送信のために一括で処理するメッセージの数。 デフォルトは *100* です。

* **添付ファイルの合計サイズ**

  supportAttachments がオンの場合、この値は、すべての添付ファイルの最大許容トータルサイズ（バイト単位）を指定します。 デフォルトは *104857600* （100 MB）です。

* ブロックリストに加える **添付ファイルの種類**

  ファイル名拡張子のブロックリスト。「**」で始まります。**」、これはシステムによって拒否されています。 ブロックリストに加えるされていない場合は、拡張子が許可されます。 拡張機能は、「**+**」アイコンと「**-**」アイコンを使用して追加または削除できます。

* **許可される添付ファイルタイプ**

  **（*Action Required*）** ファイル名の拡張子の許可リスト ブロックリストに加える。 ブロックリストに加えるされたファイル名以外のすべてのファイル拡張子を許可するには、「**-**」アイコンを使用して空のエントリを 1 つ削除します。

* **サービスセレクター**

  （*必須*） サービスが呼び出される絶対パス （エンドポイント） （仮想リソース）。 選択するパスのルートは、OSGi 設定 [`Apache Sling Servlet/Script Resolver and Error Handler`](https://localhost:4502/system/console/configMgr/org.apache.sling.servlets.resolver.SlingServletResolver) の *実行パス* 設定に含まれているルート（`/bin/`、`/apps/`、`/services/` など）にする必要があります。 サイトのメッセージ機能用にこの設定を選択するには、このエンドポイントを `Message List and Compose Message components` の **`Service selector`** 値として指定します（[&#x200B; メッセージ機能 &#x200B;](/help/communities/configure-messaging.md) を参照）。

  デフォルトは、*/bin/messaging* です。

* 許可リストに加える **フィールド**

  許可リストに加える **メッセージフィールド** を使用します。

>[!CAUTION]
>
>`Messaging Operations Service` 設定を編集用に開くたびに、設定が削除されてい `allowedAttachmentTypes.name` 場合は、空のエントリが読み取られ、プロパティを設定可能になります。 空のエントリを 1 つ指定すると、添付ファイルが無効になります。
>
>ブロックリストに加えるすべてのファイル名拡張子を許可するには、「**-**」アイコンを使用して（再び）空のファイル名拡張子を 1 つ削除してから、「保存 **をクリックし** す。

## グループメッセージング {#group-messaging}

登録ユーザーがユーザーグループにダイレクトメッセージの一括送信を許可するには、「Messaging Operation Services **設定の次の 2 つのインスタンスで** グループメッセージングを有効にする **を確認し** す。

* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-console`
* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-messaging`

**Messaging Operations サービス：ソーシャルコンソール**

![social-console-op-service](assets/social-console-op-service.png)

**メッセージング操作サービス：ソーシャルメッセージング**

![social-message-op-service](assets/social-message-op-service.png)

## トラブルシューティング {#troubleshooting}

問題のトラブルシューティングを行う方法の 1 つは、[&#x200B; ログ内のメッセージのデバッグ &#x200B;](/help/sites-administering/troubleshooting.md) を有効にすることです。

[&#x200B; 個々のサービスのロガーとライター &#x200B;](/help/sites-deploying/configure-logging.md#loggers-and-writers-for-individual-services) も参照してください。

監視するパッケージは `com.adobe.cq.social.messaging` です。
