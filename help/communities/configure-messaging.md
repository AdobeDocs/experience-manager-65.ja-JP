---
title: メッセージング機能
seo-title: Messaging Feature
description: メッセージングコンポーネントの設定
seo-description: Configuring Messaging components
uuid: 8b99ded1-aec2-40c9-82d5-e2e404f614ca
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 9d952604-f9ef-498f-937b-871817c80226
docset: aem65
exl-id: d121dc05-7d15-44ba-8d2d-b59d6c6480c8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 11%

---

# メッセージング機能 {#messaging-feature}

フォーラムやコメントでおこなわれる公開インタラクションに加えて、AEM Communitiesのメッセージ機能を使用すると、コミュニティメンバーが互いに非公開でやり取りできます。

この機能は、 [コミュニティサイト](/help/communities/overview.md#communitiessites) が作成されました。

メッセージ機能を使用すると、次のことができます。

**A** - 1 人または複数のコミュニティメンバーにメッセージを送信

**B**  — ダイレクトメッセージを送信 [コミュニティメンバーグループに一括で追加](/help/communities/messaging.md#group-messaging)

**C**  — 添付ファイル付きのメッセージを送信する

**D**  — メッセージを転送する

**E**  — メッセージに返信

**金**  — メッセージを削除

**G**  — 削除されたメッセージを復元します

![messaging-section](assets/messaging-section.png)

![restore-message](assets/restore-message.png)

メッセージング機能を有効にして変更するには、以下を参照してください。

* [メッセージの設定](/help/communities/messaging.md) 管理者向け
* [メッセージの基本事項](/help/communities/essentials-messaging.md) 開発者向け

>[!NOTE]
>
>追加はサポートされていません `Compose Message, Message, or Message List` コンポーネント ( `Communities`コンポーネントグループ ) をオーサリング編集モードでページに追加する必要があります。

## メッセージコンポーネントの設定 {#configure-messaging-components}

コミュニティサイトでメッセージを有効にすると、設定が必要なくなります。 デフォルトの設定を変更する必要がある場合は、情報が表示されます。

### メッセージリストを設定（メッセージボックス） {#configure-message-list-message-box}

次のメッセージのリストの設定を変更するには： **インボックス**, **送信済みアイテム**、および **ごみ箱** メッセージング機能のページで、 [オーサー編集モード](/help/communities/sites-console.md#authoring-site-content).

1. In `Preview` モード、 **メッセージ** メインメッセージページを開くためのリンク 次に、 **インボックス**, **送信済みアイテム** または **ごみ箱** をクリックして、そのメッセージリストのコンポーネントを設定します。

1. In `Edit` モード」で、ページ上のコンポーネントを選択します。
1. 設定ダイアログにアクセスするには、 `link` アイコン
継承がキャンセルされると、設定アイコンを選択して設定ダイアログを開くことができます。

1. 設定が完了したら、 `broken link` アイコン

![configure-message-list](assets/configure-message-list.png)

#### 「基本」タブ {#basic-tab}

![basic-tab-messagelist](assets/basic-tab-messagelist.png)

* **サービスセレクター**

   (*必須*) これをプロパティの値に設定します。 **`serviceSelector.name`** から [AEM Communities Messaging Operations Service](/help/communities/messaging.md#messaging-operations-service).

* **ページを作成**

   (*必須*) メンバーが **`Reply`** 」ボタンをクリックします。 ターゲットページには、**メッセージを作成**&#x200B;フォームを含める必要があります。

* **返信/リソースとして表示**

   オンにすると、返信 URL と表示 URL でリソースが参照されます。オンにしない場合、データは URL でクエリパラメーターとして渡されます。

* **プロファイル表示フォーム**

   送信者のプロファイルの表示に使用するプロファイルフォームです。

* **ごみ箱フォルダ**

   オンにすると、このメッセージリストコンポーネントには、削除済み（ごみ箱）としてフラグ付けされたメッセージのみが表示されます。

* **フォルダーパス**

   (*必須*) **inbox.path.name** および **sentitems.path.name** 内 [AEM Communities Messaging Operations Service](/help/communities/messaging.md#messaging-operations-service). を `Inbox`、値を使用して 1 つのエントリを追加 **inbox.path.name**. を `Outbox`、値を使用して 1 つのエントリを追加 **sentitems.path.name**. を設定する際 `Trash`、両方の値を持つ 2 つのエントリを追加します。

#### 「表示」タブ {#display-tab}

![display-tab-message-list](assets/display-tab-message-list.png)

* **既読をマークボタン**

   オンにすると、 `Read`ボタンを使用して、メッセージを既読としてマークすることができます。

* **未読のマークボタン**

   オンにすると、 `Mark Unread` ボタンを使用して、メッセージを既読としてマークすることができます。

* **「削除」ボタン**

   オンにすると、 `Delete` ボタンを使用して、メッセージを既読としてマークすることができます。 次の場合に削除機能が複製されます： **`Message Options`** がオンになっている。

* **メッセージオプション**

   オンにすると、が表示されます **`Reply`**, **`Reply All`**, **`Forward`** および **`Delete`** ボタンを使用して、メッセージを再送信または削除できます。 次の場合に削除機能が複製されます： **`Delete Button`** がオンになっている。

* **1 ページのメッセージ数**

   指定した数は、ページネーションスキームで 1 ページに表示されるメッセージの最大数です。 数字を指定しない（空白のまま）場合、すべてのメッセージが表示され、ページネーションはありません。

* **タイムスタンプのパターン**

   1 つ以上の言語のタイムスタンプパターンを指定します。 初期設定は en、de、fr、it、es、ja、zh_CN、ko_KR です。

* **ユーザーを表示**

   次のいずれかを選択 **`Sender`** または **`Recipients`** をクリックして、「送信者」と「受信者」のどちらを表示するかを決定します。

### メッセージを作成を設定 {#configure-compose-message}

メッセージを作成ページの設定を変更するには、サイトを開き、 [オーサー編集モード](/help/communities/sites-console.md#authoring-site-content).

* In `Preview` モード、 **メッセージ** メインメッセージページを開くためのリンク 次に、「新しいメッセージ」ボタンを選択して、 `Compose Message` ページ。

* In `Edit` モード：メッセージ本文を含むページ上のメインコンポーネントを選択します。
* 設定ダイアログにアクセスするには、 `link` アイコン
継承がキャンセルされると、設定アイコンを選択して設定ダイアログを開くことができます。

* 設定が完了したら、 `broken link` アイコン

![config-compose-message](assets/config-compose-message.png)

#### 「基本」タブ {#basic-tab-1}

![basic-tab-compose](assets/basic-tab-compose.png)

* **リダイレクト URL**

   メッセージの送信後に表示されるページの URL を入力します。 （例：`../messaging.html`）。

* **キャンセル URL**

   送信者がメッセージをキャンセルした場合に表示されるページの URL を入力します。 （例：`../messaging.html`）。

* **メッセージ件名の最大長**

   「件名」フィールドに入力できる最大文字数。 例：500 初期設定は無制限です。

* **メッセージ本文の最大長**

   「コンテンツ」フィールドに入力できる最大文字数です。 例：10000。 初期設定は無制限です。

* **サービスセレクター**

   (*必須*) これをプロパティの値に設定します。 **`serviceSelector.name`** から [AEM Communities Messaging Operations Service](/help/communities/messaging.md#messaging-operations-service).

#### 「表示」タブ {#display-tab-1}

![display-tab-compose](assets/display-tab-compose.png)

* **件名フィールドを表示**

   オンにすると、 `Subject` フィールドに入力し、メッセージへの件名の追加を有効にします。 初期設定はオンになっていません。

* **件名ラベル**

   横に表示するテキストを入力 `Subject` フィールドに入力します。 デフォルトは `Subject` です。

* **ファイルの添付フィールドを表示**

   オンにすると、 `Attachment` フィールドに値を入力し、メッセージへの添付ファイルの追加を有効にします。 初期設定はオンになっていません。

* **添付ファイルのラベル**

   横に表示するテキストを入力 `Attachment` フィールドに入力します。 デフォルトは **`Attach File`** です。

* **コンテンツフィールドを表示**

   オンにすると、 `Content` フィールドに値を入力し、メッセージ本文の追加を有効にします。 初期設定はオンになっていません。

* **コンテンツラベル**

   横に表示するテキストを入力 `Content` フィールドに入力します。 デフォルトは **`Body`** です。

* **リッチテキストエディターを使用**

   オンにすると、独自のリッチテキストエディターでカスタムの「コンテンツ」テキストボックスが使用されることを示します。 初期設定はオンになっていません。

* **タイムスタンプのパターン**

   1 つ以上の言語のタイムスタンプパターンを指定します。 初期設定は en、de、fr、it、es、ja、zh_CN、ko_KR です。
