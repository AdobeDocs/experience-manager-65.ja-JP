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

この機能は、[ コミュニティサイト ](/help/communities/overview.md#communitiessites) の作成時に含めることができます。

メッセージ機能を使用すると、次の操作を実行できます。

**A** - 1 人以上のコミュニティメンバーにメッセージを送信する

**B** - ダイレクトメッセージの [ 一括でのコミュニティメンバーグループへの送信 ](/help/communities/messaging.md#group-messaging)

**C** – 添付ファイル付きメッセージの送信

**D** - メッセージの転送

**E** - メッセージへの返信

**F** - メッセージを削除する

**G** – 削除されたメッセージの復元

![messaging-section](assets/messaging-section.png)

![restore-message](assets/restore-message.png)

メッセージ機能を有効にして変更するには、以下を参照してください。

* 管理者向けの [ メッセージングの設定 ](/help/communities/messaging.md)
* 開発者向けの [ メッセージングの基本事項 ](/help/communities/essentials-messaging.md)

>[!NOTE]
>
>`Communities` コンポーネントグループ）にある `Compose Message, Message, or Message List` コンポーネントをオーサー編集モードでページに追加することはサポートされていません。

## メッセージコンポーネントの設定 {#configure-messaging-components}

コミュニティサイトに対してメッセージングが有効になっている場合、それ以上の設定は必要なく設定されます。 デフォルトの設定を変更する必要がある場合、この情報が表示されます。

### メッセージリストの設定（メッセージボックス） {#configure-message-list-message-box}

メッセージ機能の **インボックス**、**送信済み項目**、および **ごみ箱** ページのメッセージリストの設定を変更するには、サイトを [ オーサー編集モード ](/help/communities/sites-console.md#authoring-site-content) で開きます。

1. `Preview` モードで、「**メッセージ**」リンクを選択して、メインメッセージページを開きます。 次に、**インボックス**、**送信済み項目** または **ごみ箱** を選択して、そのメッセージリストのコンポーネントを設定します。

1. `Edit` モードで、ページ上のコンポーネントを選択します。
1. 設定ダイアログにアクセスするには、`link` アイコンを選択して継承をキャンセルします。
継承がキャンセルされると、「設定」アイコンを選択して、設定ダイアログを開くことができます。

1. 設定が完了したら、`broken link` アイコンを選択して継承を復元する必要があります。

![configure-message-list](assets/configure-message-list.png)

#### 「基本」タブ {#basic-tab}

![basic-tab-messagelist](assets/basic-tab-messagelist.png)

* **サービスセレクター**

  （*必須*）これを [AEM Communities Messaging Operations Service](/help/communities/messaging.md#messaging-operations-service) のプロパティ **`serviceSelector.name`** の値に設定します。

* **ページを作成**

  （*必須*）メンバーが「**`Reply`**」ボタンをクリックしたときに開くページ。 ターゲットページには **メッセージを作成** フォームが含まれている必要があります。

* **返信/リソースとして表示**

  オンにした場合、返信 URL とビュー URL がリソースを参照します。オフにした場合、データが URL のクエリパラメーターとして渡されます。

* **プロファイル表示フォーム**

  送信者プロファイルの表示に使用するプロファイルフォーム。

* **ごみ箱フォルダー**

  オンにすると、このメッセージリストコンポーネントは、削除済み（ごみ箱）としてフラグ付けされたメッセージのみを表示します。

* **フォルダーパス**

  （*必須*） **6}AEM Communities Messaging Operations Service](/help/communities/messaging.md#messaging-operations-service) の** inbox.path.name **および** sentitems.path.name} に設定された値を参照しています。 [`Inbox` 用にを設定する場合は、**inbox.path.name** の値を使用して 1 つのエントリを追加します。 `Outbox` 用にを設定する場合は、**sentitems.path.name** の値を使用して 1 つのエントリを追加します。 `Trash` 用にを設定する場合、両方の値を持つ 2 つのエントリを追加します。

#### 「表示」タブ {#display-tab}

![display-tab-message-list](assets/display-tab-message-list.png)

* **読み取りボタンをマーク**

  オンにすると、メッセージを既読としてマークできる `Read` ボタンが表示されます。

* **未読にするボタン**

  オンにすると、メッセージを既読としてマークできる「`Mark Unread`」ボタンが表示されます。

* **削除ボタン**

  オンにすると、メッセージを既読としてマークできる「`Delete`」ボタンが表示されます。 **`Message Options`** もオンになっている場合、削除機能を複製します。

* **メッセージオプション**

  オンにすると、**`Reply`**、**`Reply All`**、**`Forward`**、**`Delete`** のボタンが表示され、メッセージの再送信や削除が可能になります。 **`Delete Button`** もオンになっている場合、削除機能を複製します。

* **ページあたりのメッセージ数**

  指定された数は、ページネーションスキームでページごとに表示されるメッセージの最大数です。 番号が指定されていない場合（空白の場合）、すべてのメッセージが表示され、ページネーションは行われません。

* **タイムスタンプパターン**

  1 つ以上の言語のタイムスタンプパターンを指定します。 デフォルトは、en、de、fr、it、es、ja、zh_CN、ko_KR です。

* **ユーザーを表示**

  **`Sender`** または **`Recipients`** を選択すると、送信者と受信者のどちらを表示するかを指定できます。

### メッセージを作成の設定 {#configure-compose-message}

メッセージを作成ページの設定を変更するには、サイトを [ オーサー編集モード ](/help/communities/sites-console.md#authoring-site-content) で開きます。

* `Preview` モードで、「**メッセージ**」リンクを選択して、メインメッセージページを開きます。 次に、「新規メッセージ」ボタンを選択して、`Compose Message` のページを開きます。

* `Edit` モードで、メッセージ本文を含むページ上のメインコンポーネントを選択します。
* 設定ダイアログにアクセスするには、`link` アイコンを選択して継承をキャンセルします。
継承がキャンセルされると、「設定」アイコンを選択して、設定ダイアログを開くことができます。

* 設定が完了したら、`broken link` アイコンを選択して継承を復元する必要があります。

![config-compose-message](assets/config-compose-message.png)

#### 「基本」タブ {#basic-tab-1}

![basic-tab-compose](assets/basic-tab-compose.png)

* **リダイレクト URL**

  メッセージの送信後に表示されるページの URL を入力します。 例えば、`../messaging.html` のように指定します。

* **キャンセル URL**

  送信者がメッセージをキャンセルした場合に表示されるページの URL を入力します。 例えば、`../messaging.html` のように指定します。

* **メッセージ件名の最大長**

  「件名」フィールドで許可される最大文字数。 例：500。 デフォルトは無制限です。

* **メッセージ本文の最大長**

  「コンテンツ」フィールドで許可される最大文字数。 例：10000。 デフォルトは無制限です。

* **サービスセレクター**

  （*必須*）これを [AEM Communities Messaging Operations Service](/help/communities/messaging.md#messaging-operations-service) のプロパティ **`serviceSelector.name`** の値に設定します。

#### 「表示」タブ {#display-tab-1}

![display-tab-compose](assets/display-tab-compose.png)

* **件名フィールドを表示**

  オンにした場合は、`Subject` フィールドを表示し、メッセージへの件名の追加を有効にします。 デフォルトはオフです。

* **件名ラベル**

  `Subject` フィールドの横に表示するテキストを入力します。 デフォルトは `Subject` です。

* **[ 添付ファイルを表示 ] フィールド**

  オンにした場合は、`Attachment` フィールドを表示し、メッセージへの添付ファイルの追加を有効にします。 デフォルトはオフです。

* **ファイル ラベルを添付**

  `Attachment` フィールドの横に表示するテキストを入力します。 デフォルトは **`Attach File`** です。

* **コンテンツフィールドを表示**

  オンにした場合は、`Content` フィールドを表示し、メッセージ本文の追加を有効にします。 デフォルトはオフです。

* **コンテンツラベル**

  `Content` フィールドの横に表示するテキストを入力します。 デフォルトは **`Body`** です。

* **リッチテキストエディター**

  オンにした場合、独自のリッチテキストエディターでカスタムコンテンツテキストボックスが使用されることを示します。 デフォルトはオフです。

* **タイムスタンプパターン**

  1 つ以上の言語のタイムスタンプパターンを指定します。 デフォルトは、en、de、fr、it、es、ja、zh_CN、ko_KR です。
