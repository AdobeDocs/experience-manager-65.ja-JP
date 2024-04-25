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

コミュニティサイトでメッセージングを有効にするには、 [コミュニティサイトの作成](/help/communities/sites-console.md).

このページには、デフォルトの設定と可能な調整に関する情報が含まれています。

開発者向けの追加情報については、以下を参照してください [メッセージングの基本事項](/help/communities/essentials-messaging.md).

## メッセージング操作サービス {#messaging-operations-service}

設定 [AEM Communities Messaging Operations サービス](https://localhost:4502/system/console/configMgr/com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl) は、メッセージング関連の要求を処理するエンドポイント、メッセージの保存にサービスが使用する必要のあるフォルダー、およびメッセージに添付ファイルが含まれる場合は、許可されるファイル タイプを識別します。

を使用して作成されたコミュニティサイトの場合 `Communities Sites console`：サービスのインスタンスが存在し、インボックスがに設定されています `/mail/inbox`.

### コミュニティメッセージング運用サービス {#community-messaging-operations-service}

以下に示すように、サービスの設定は、で作成されたサイトに対して存在します [サイト作成ウィザード](/help/communities/sites-console.md). 設定は、設定の横にある鉛筆アイコンを選択して表示または編集できます。

![メッセージング操作](assets/messaging-operations.png)

### 新しい設定を追加 {#add-new-configuration}

設定を追加するには、プラス「」を選択します&#x200B;**+**「」アイコン（サービス名の横）が表示されます。

* **メッセージフィールドの許可リスト**

  ユーザーが編集および保持できるメッセージの作成コンポーネントのプロパティを指定します。 新しいフォーム要素を追加する場合、SRP に保存するには要素 ID を追加する必要があります。 デフォルトは 2 つのエントリです。 *件名* および *コンテンツ*.

* **メッセージボックスのサイズ制限**

  各ユーザーのメッセージ ボックスの最大バイト数です。 デフォルトは *1073741824* （1 GB）。

* **メッセージ数の制限**

  ユーザーごとに許可されるメッセージの合計数。 値が–1 の場合は、メッセージ ボックスのサイズ制限に従って、メッセージの数に制限がないことを示します。 デフォルトは *10000* （10k）。

* **配信エラーを通知**

  オンにすると、一部の受信者にメッセージ配信が失敗した場合に送信者に通知します。 デフォルトは *確認済み*.

* **エラー配信送信者 ID**

  配信の失敗メッセージに表示される送信者の名前。 デフォルトは *failureNotifier*.

* **失敗メッセージテンプレートパス**

  配信失敗メッセージテンプレートルートの絶対パス。 デフォルトは */etc/notification/messaging/default*.

* **再試行の数**

  配信に失敗したメッセージの再送信を試行する回数。 デフォルトは *3*.

* **再試行の間待機**

  送信に失敗したときにメッセージを再送信する間隔を秒単位で指定します。 デフォルトは *100* （秒）。

* **カウント更新プールのサイズ**

  カウントの更新に使用される同時スレッドの数。 デフォルトは *10*.

* **インボックスパス**

  （*必須*） ユーザーのノードを基準とした相対パス （/home/users/*ユーザー名*）、に使用します。 `inbox` フォルダー。 パスの末尾にスラッシュ「/」を付けることはできません。 デフォルトは */mail/inbox*.

* **送信済み項目のパス**

  （*必須*） ユーザーのノードを基準とした相対パス （/home/users/*ユーザー名*）、に使用します。 `sent items` フォルダー。 パスの末尾にスラッシュ「/」を付けることはできません。 デフォルトは */mail/sentitems* .

* **サポートの添付ファイル**

  オンにすると、ユーザーは、メッセージに添付ファイルを追加できます。 デフォルトは *確認済み*.

* **グループメッセージングの有効化**

  選択した場合、登録ユーザーはメンバーのグループに一括メッセージを送信できます。 デフォルトは *選択解除*.

* **最大数 合計受信者数のうち**

  グループメッセージが有効な場合、グループメッセージを一度に送信できる最大受信者数を指定します。 デフォルトは *100*.

* **バッチサイズ**

  多数の受信者に送信する際に送信のために一括で処理するメッセージの数。 デフォルトは *100*.

* **添付ファイルの合計サイズ**

  supportAttachments がオンの場合、この値は、すべての添付ファイルの最大許容トータルサイズ（バイト単位）を指定します。 デフォルトは *104857600* （100 MB）。

* **添付ファイルの種類^ブロックリスト**

  ファイル名拡張子のブロックリスト。先頭に「**.**&#39;、これはシステムによって拒否されています。 ブロックリストに加えるされていない場合は、拡張子が許可されます。 拡張機能は、「」を使用して追加または削除できます&#x200B;**+**「および」**-**&#x200B;アイコン。

* **許可される添付ファイルタイプ**

  **（*必要なアクション*）** ファイル名の拡張子の許可リスト。ブロックリストの逆。 ブロックリストに加えるされているファイル名以外のすべてのファイル拡張子を許可するには、「**-**「」アイコンをクリックして、単一の空のエントリを削除します。

* **サービスセレクター**

  （*必須*）サービスが呼び出される絶対パス（エンドポイント）（仮想リソース）。 選択したパスのルートは、 *実行パス* osgi 設定の設定 [`Apache Sling Servlet/Script Resolver and Error Handler`](https://localhost:4502/system/console/configMgr/org.apache.sling.servlets.resolver.SlingServletResolver)（例：） `/bin/`, `/apps/`、および `/services/`. サイトのメッセージ機能に対してこの設定を選択するために、このエンドポイントは次のように指定します **`Service selector`** の値 `Message List and Compose Message components` （を参照） [メッセージ機能](/help/communities/configure-messaging.md)）に設定します。

  デフォルトはです */bin/messaging* .

* **フィールド^許可リスト**

  使用方法 **メッセージフィールドの許可リスト**.

>[!CAUTION]
>
>Every time a `Messaging Operations Service` 次の場合、設定が編集用に開かれます `allowedAttachmentTypes.name` が削除されている場合は、プロパティを設定可能にするために、空のエントリが追加されます。 空のエントリを 1 つ指定すると、添付ファイルが無効になります。
>
>ブロックリストに加えるされているファイル名以外のすべてのファイル拡張子を許可するには、「**-**「」アイコンをクリックして、空のエントリを 1 つ削除してから（再び）クリックします **保存**.

## グループメッセージング {#group-messaging}

登録ユーザーがダイレクトメッセージをユーザーグループに一括で送信できるようにするには、次の点を確認します **グループメッセージングの有効化** 以下の 2 つの場合 **メッセージング操作サービス** 設定：

* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-console`
* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-messaging`

**メッセージング オペレーション サービス：ソーシャル コンソール**

![social-console-op-service](assets/social-console-op-service.png)

**メッセージング操作サービス：ソーシャルメッセージング**

![social-message-op-service](assets/social-message-op-service.png)

## トラブルシューティング {#troubleshooting}

問題のトラブルシューティングを行う方法の 1 つに、を有効にすることがあります [ログでのメッセージのデバッグ。](/help/sites-administering/troubleshooting.md)

関連トピック [個々のサービス用のロガーとライター](/help/sites-deploying/configure-logging.md#loggers-and-writers-for-individual-services).

監視するパッケージはです。 `com.adobe.cq.social.messaging`.
