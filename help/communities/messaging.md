---
title: メッセージングの設定
description: ログインしているサイト訪問者（メンバー）が互いにメッセージを送信する機能を提供するAEM Communitiesのメッセージ機能について説明します。
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
source-wordcount: '864'
ht-degree: 0%

---

# メッセージングの設定 {#configure-messaging}

## 概要 {#overview}

AEM Communitiesのメッセージ機能では、ログインしているサイト訪問者（メンバー）が、サイトにログインしたときにアクセスできるメッセージを相互に送信できます。

[&#x200B; コミュニティサイト作成中](/help/communities/sites-console.md)にチェックボックスをオンにすると、コミュニティサイトに対するメッセージが有効になります。

このページには、デフォルト設定と可能な調整に関する情報が表示されます。

開発者向けの追加情報については、[Messaging Essentials](/help/communities/essentials-messaging.md)を参照してください。

## Messaging Operations Service {#messaging-operations-service}

設定[AEM Communities Messaging Operations Service](https://localhost:4502/system/console/configMgr/com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl)は、メッセージに関連するリクエストを処理するエンドポイント、メッセージの保存にサービスが使用するフォルダー、メッセージに添付ファイルが含まれる可能性がある場合に許可されるファイルの種類を特定します。

`Communities Sites console`を使用して作成されたコミュニティサイトの場合、サービスのインスタンスが存在し、受信トレイは`/mail/inbox`に設定されています。

### コミュニティメッセージングオペレーションサービス {#community-messaging-operations-service}

以下に示すように、[&#x200B; サイト作成ウィザード &#x200B;](/help/communities/sites-console.md)で作成されたサイトに対するサービスの設定が存在します。 設定は、設定の横にある鉛筆アイコンを選択して表示または編集できます。

![messaging-operations](assets/messaging-operations.png)

### 新しい設定を追加 {#add-new-configuration}

設定を追加するには、サービス名の横にあるプラス &#39;**+**&#39; アイコンを選択します。

* **メッセージフィールドが許可リストに加える**

  ユーザーが編集および保持できるメッセージ作成コンポーネントのプロパティを指定します。 新しいフォーム要素が追加された場合、SRPに保存する場合は、要素IDを追加する必要があります。 デフォルトは2つのエントリです：*subject*&#x200B;と&#x200B;*content*。

* **メッセージボックスのサイズ制限**

  各ユーザーのメッセージボックス内の最大バイト数。 デフォルトは&#x200B;*1073741824* （1 GB）です。

* **メッセージ数の制限**

  ユーザーごとに許可されるメッセージの合計数です。 値–1は、メッセージボックスのサイズ制限に従って、メッセージの数に制限がないことを示します。 デフォルトは&#x200B;*10000* （10k）です。

* **配信エラーの通知**

  チェックを入れた場合、メッセージの配信が一部の受信者に失敗した場合は、送信者に通知します。 デフォルトは&#x200B;*checked*&#x200B;です。

* **配信失敗の送信者ID**

  配信に失敗したメッセージに表示される送信者の名前。 デフォルトは&#x200B;*failureNotifier*&#x200B;です。

* **エラーメッセージテンプレートのパス**

  配信に失敗したメッセージテンプレートのルートへの絶対パス。 デフォルトは&#x200B;*/etc/notification/messaging/default*&#x200B;です。

* **再試行の回数**

  配信に失敗したメッセージの再送信を試みる回数。 デフォルトは&#x200B;*3*&#x200B;です。

* **再試行の間に待機**

  送信に失敗した場合に、メッセージを再送信するまでの待機時間（秒）。 デフォルトは&#x200B;*100* （秒）です。

* **プールサイズの更新をカウント**

  カウント更新に使用される同時スレッドの数。 デフォルトは&#x200B;*10*&#x200B;です。

* **受信トレイのパス**

  （*必須*） ユーザーのノード （/home/users/*username*）に対する相対パスで、`inbox` フォルダーに使用します。 パスの末尾にスラッシュ「/」を付けることはできません。 デフォルトは&#x200B;*/mail/inbox*&#x200B;です。

* **送信済みアイテムのパス**

  （*必須*） ユーザーのノード （/home/users/*username*）に対する相対パスで、`sent items` フォルダーに使用します。 パスの末尾にスラッシュ「/」を付けることはできません。 デフォルトは&#x200B;*/mail/sentitems*&#x200B;です。

* **添付ファイルのサポート**

  オンにすると、ユーザーはメッセージに添付ファイルを追加できます。 デフォルトは&#x200B;*checked*&#x200B;です。

* **グループメッセージを有効にする**

  選択した場合、登録ユーザーはメンバーのグループにバルクメッセージを送信できます。 デフォルトは&#x200B;*選択解除*&#x200B;です。

* **最大数 合計受信者数**

  グループメッセージが有効になっている場合は、一度にグループメッセージを送信できる最大受信者数を指定します。 デフォルトは&#x200B;*100*&#x200B;です。

* **バッチサイズ**

  多数の受信者グループに送信する際に、1回の送信で一括して送信するメッセージの数。 デフォルトは&#x200B;*100*&#x200B;です。

* **添付ファイルの合計サイズ**

  supportAttachmentsがチェックされている場合、この値はすべての添付ファイルの許可される最大合計サイズ（バイト単位）を指定します。 デフォルトは&#x200B;*104857600* （100 MB）です。

* **添付ファイルの種類とブロックリストに加える**

  システムによって拒否される、ファイル名拡張子のブロックリスト（&#39;**.**&#39;が先頭に付きます）。 ブロックリストに加えるしない場合は、拡張機能が許可されます。 拡張機能は、&#39;**+**&#39;および&#39;**-**&#39; アイコンを使用して追加または削除できます。

* **許可された添付ファイルの種類**

  **（*アクションが必要*）** ファイル名の拡張子で構成されるファイル名の許可リストで、ファイル名の拡張子とは反対です。 ファイル名の拡張子をすべて許可するには、ファイル名の拡張子が削除されている場合を除き、&#39;**-**&#39; アイコンを使用して1つの空のエントリを削除します。

* **サービスセレクター**

  （*必須*） サービスが呼び出される絶対パス （エンドポイント） （仮想リソース）。 選択したパスのルートは、OSGi設定[`Apache Sling Servlet/Script Resolver and Error Handler`](https://localhost:4502/system/console/configMgr/org.apache.sling.servlets.resolver.SlingServletResolver)の&#x200B;*実行パス*&#x200B;構成設定（`/bin/`、`/apps/`、および`/services/`など）に含まれている必要があります。 サイトのメッセージ機能にこの設定を選択するには、このエンドポイントを`Message List and Compose Message components`の&#x200B;**`Service selector`**&#x200B;値として指定します（[&#x200B; メッセージ機能](/help/communities/configure-messaging.md)を参照）。

  デフォルトは&#x200B;*/bin/messaging*&#x200B;です。

* **フィールド許可リスト**

  **メッセージフィールドを使用**&#x200B;します。

>[!CAUTION]
>
>`Messaging Operations Service`設定を編集用に開くたびに、`allowedAttachmentTypes.name`が削除された場合、空のエントリが読み込まれ、プロパティが設定可能になります。 1つの空のエントリを使用すると、ファイルの添付ファイルが無効になります。
>
>ファイル名の拡張子をすべて許可するには、ファイル名の拡張子を除くファイル名の拡張子を許可するには、「**-**」アイコンを使用して、空のエントリを（再び）削除してから&#x200B;**保存**&#x200B;をクリックします。

## グループメッセージ {#group-messaging}

登録ユーザーがユーザーグループにダイレクトメッセージを一括で送信できるようにするには、**メッセージングオペレーションサービス**&#x200B;設定の次の2つのインスタンスで&#x200B;**グループメッセージ**&#x200B;を有効にしてください。

* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-console`
* `com.adobe.cq.social.messaging.client.endpoints.impl.MessagingOperationsServiceImpl~social-messaging`

**メッセージング操作サービス：ソーシャルコンソール**

![social-console-op-service](assets/social-console-op-service.png)

**メッセージング操作サービス：ソーシャルメッセージ**

![social-message-op-service](assets/social-message-op-service.png)

## トラブルシューティング {#troubleshooting}

問題をトラブルシューティングする方法の1つは、[&#x200B; ログ内のメッセージのデバッグを有効にすることです。](/help/sites-administering/troubleshooting.md)

[個別サービスのロガーとライター](/help/sites-deploying/configure-logging.md#loggers-and-writers-for-individual-services)も参照してください。

監視するパッケージは`com.adobe.cq.social.messaging`です。
