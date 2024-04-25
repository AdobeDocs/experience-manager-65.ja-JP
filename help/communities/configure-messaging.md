---
title: メッセージング機能
description: AEM Communitiesのメッセージング機能を設定して、コミュニティメンバーが互いにより個人的にやり取りできるようにする方法を説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: d121dc05-7d15-44ba-8d2d-b59d6c6480c8
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '952'
ht-degree: 1%

---

# メッセージング機能 {#messaging-feature}

フォーラムやコメントで発生する公の場でのインタラクションに加えて、AEM Communitiesのメッセージング機能を使用すると、コミュニティメンバーはより個人的にやり取りできるようになります。

この機能は、 [コミュニティサイト](/help/communities/overview.md#communitiessites) が作成されました。

メッセージ機能を使用すると、次の操作を実行できます。

**A** - 1 人以上のコミュニティメンバーにメッセージを送信

**B** - ダイレクトメッセージの送信： [コミュニティメンバーグループに一括](/help/communities/messaging.md#group-messaging)

**C**  – 添付ファイル付きメッセージの送信

**日** - メッセージの転送

**E** - メッセージへの返信

**金** - メッセージを削除します

**G**  – 削除されたメッセージの復元

![messaging-section](assets/messaging-section.png)

![restore-message](assets/restore-message.png)

メッセージ機能を有効にして変更するには、以下を参照してください。

* [メッセージングの設定](/help/communities/messaging.md) 管理者向け
* [メッセージングの基本事項](/help/communities/essentials-messaging.md) 開発者向け

>[!NOTE]
>
>の追加はサポートされていません `Compose Message, Message, or Message List` コンポーネント （内を検索） `Communities`コンポーネントグループ）を使用して、オーサー編集モードのページに移動します。

## メッセージコンポーネントの設定 {#configure-messaging-components}

コミュニティサイトに対してメッセージングが有効になっている場合、それ以上の設定は必要なく設定されます。 デフォルトの設定を変更する必要がある場合、この情報が表示されます。

### メッセージリストの設定（メッセージボックス） {#configure-message-list-message-box}

のメッセージリストの設定を変更する手順は次のとおりです **受信トレイ**, **送信済みアイテム**、および **ごみ箱** メッセージング機能のページで、次の場所のサイトを開きます： [オーサー編集モード](/help/communities/sites-console.md#authoring-site-content).

1. 対象： `Preview` モードで、 **メッセージ** メインのメッセージページを開くためのリンクです。 次に、次のいずれかを選択します **受信トレイ**, **送信済みアイテム** または **ごみ箱** そのメッセージリスト用のコンポーネントを設定します。

1. 対象： `Edit` モードで、ページ上のコンポーネントを選択します。
1. 設定ダイアログにアクセスするには、を選択して継承をキャンセルします `link` アイコン。
継承がキャンセルされると、「設定」アイコンを選択して、設定ダイアログを開くことができます。

1. 設定が完了したら、を選択して継承を復元する必要があります。 `broken link` アイコン。

![configure-message-list](assets/configure-message-list.png)

#### 「基本」タブ {#basic-tab}

![basic-tab-messagelist](assets/basic-tab-messagelist.png)

* **サービスセレクター**

  （*必須*）これをプロパティの値に設定します **`serviceSelector.name`** から [AEM Communities Messaging Operations サービス](/help/communities/messaging.md#messaging-operations-service).

* **ページを作成**

  （*必須*） メンバーがクリックしたときに開くページ **`Reply`** ボタン。 ターゲットページには、次が含まれている必要があります **メッセージを作成** フォーム。

* **返信/リソースとして表示**

  オンにした場合、返信 URL とビュー URL がリソースを参照します。オフにした場合、データが URL のクエリパラメーターとして渡されます。

* **プロファイル表示フォーム**

  送信者プロファイルの表示に使用するプロファイルフォーム。

* **ごみ箱フォルダー**

  オンにすると、このメッセージリストコンポーネントは、削除済み（ごみ箱）としてフラグ付けされたメッセージのみを表示します。

* **フォルダーパス**

  （*必須*）に設定された値を参照します **inbox.path.name** および **sentitems.path.name** が含まれる [AEM Communities Messaging Operations サービス](/help/communities/messaging.md#messaging-operations-service). に対応するようにを設定する場合 `Inbox`、の値を使用してエントリを 1 つ追加します。 **inbox.path.name**. に対応するようにを設定する場合 `Outbox`、の値を使用してエントリを 1 つ追加します。 **sentitems.path.name**. 用に設定する場合 `Trash`は、両方の値を持つ 2 つのエントリを追加します。

#### 「表示」タブ {#display-tab}

![display-tab-message-list](assets/display-tab-message-list.png)

* **「読み取り」ボタンをマーク**

  オンにすると、が表示されます `Read`メッセージを既読としてマークするボタン。

* **未読にするボタン**

  オンにすると、が表示されます `Mark Unread` メッセージを既読としてマークするボタン。

* **「削除」ボタン**

  オンにすると、が表示されます `Delete` メッセージを既読としてマークするボタン。 次の場合は、削除機能を複製します **`Message Options`** もチェックされます。

* **メッセージオプション**

  オンにすると、と表示されます **`Reply`**, **`Reply All`**, **`Forward`**、および **`Delete`** メッセージの再送信または削除を許可するボタン。 次の場合は、削除機能を複製します **`Delete Button`** もチェックされます。

* **ページあたりのメッセージ数**

  指定された数は、ページネーションスキームでページごとに表示されるメッセージの最大数です。 番号が指定されていない場合（空白の場合）、すべてのメッセージが表示され、ページネーションは行われません。

* **タイムスタンプパターン**

  1 つ以上の言語のタイムスタンプパターンを指定します。 デフォルトは、en、de、fr、it、es、ja、zh_CN、ko_KR です。

* **ユーザーを表示**

  次のいずれかを選択します **`Sender`** または **`Recipients`** そのため、送信者と受信者のどちらを表示するかを決定できます。

### メッセージを作成の設定 {#configure-compose-message}

メッセージを作成ページの設定を変更するには、でサイトを開きます。 [オーサー編集モード](/help/communities/sites-console.md#authoring-site-content).

* 対象： `Preview` モードで、 **メッセージ** メインのメッセージページを開くためのリンクです。 次に、「新規メッセージ」ボタンを選択し、 `Compose Message` ページ。

* 対象： `Edit` モードで、メッセージ本文を含むページ上のメインコンポーネントを選択します。
* 設定ダイアログにアクセスするには、を選択して継承をキャンセルします `link` アイコン。
継承がキャンセルされると、「設定」アイコンを選択して、設定ダイアログを開くことができます。

* 設定が完了したら、を選択して継承を復元する必要があります。 `broken link` アイコン。

![config-compose-message](assets/config-compose-message.png)

#### 「基本」タブ {#basic-tab-1}

![basic-tab-compose](assets/basic-tab-compose.png)

* **リダイレクト URL**

  メッセージの送信後に表示されるページの URL を入力します。 例えば、`../messaging.html` のように指定します。

* **URL をキャンセル**

  送信者がメッセージをキャンセルした場合に表示されるページの URL を入力します。 例えば、`../messaging.html` のように指定します。

* **メッセージ件名の最大長**

  「件名」フィールドで許可される最大文字数。 例：500。 デフォルトは無制限です。

* **メッセージ本文の最大長**

  「コンテンツ」フィールドで許可される最大文字数。 例：10000。 デフォルトは無制限です。

* **サービスセレクター**

  （*必須*）これをプロパティの値に設定します **`serviceSelector.name`** から [AEM Communities Messaging Operations サービス](/help/communities/messaging.md#messaging-operations-service).

#### 「表示」タブ {#display-tab-1}

![display-tab-compose](assets/display-tab-compose.png)

* **件名フィールドを表示**

  オンにした場合は、を表示 `Subject` フィールドに入力し、メッセージへの件名の追加を有効にします。 デフォルトはオフです。

* **件名ラベル**

  の横に表示するテキストを入力します `Subject` フィールド。 デフォルトは `Subject` です。

* **添付ファイル フィールドを表示**

  オンにした場合は、を表示 `Attachment` フィールドに入力し、メッセージへの添付ファイルの追加を有効にします。 デフォルトはオフです。

* **ファイル ラベルを添付**

  の横に表示するテキストを入力します `Attachment` フィールド。 デフォルトは **`Attach File`** です。

* **コンテンツフィールドを表示**

  オンにした場合は、を表示 `Content` フィールドに入力し、メッセージ本文の追加を有効にします。 デフォルトはオフです。

* **コンテンツラベル**

  の横に表示するテキストを入力します `Content` フィールド。 デフォルトは **`Body`** です。

* **リッチテキストエディターの使用**

  オンにした場合、独自のリッチテキストエディターでカスタムコンテンツテキストボックスが使用されることを示します。 デフォルトはオフです。

* **タイムスタンプパターン**

  1 つ以上の言語のタイムスタンプパターンを指定します。 デフォルトは、en、de、fr、it、es、ja、zh_CN、ko_KR です。
