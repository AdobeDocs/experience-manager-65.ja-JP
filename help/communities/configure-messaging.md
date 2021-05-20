---
title: メッセージング機能
seo-title: メッセージング機能
description: メッセージングコンポーネントの設定
seo-description: メッセージングコンポーネントの設定
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
source-wordcount: '932'
ht-degree: 12%

---

# メッセージング機能 {#messaging-feature}

AEM Communitiesのメッセージング機能を使用すると、フォーラムやコメントで公に表示されるインタラクションに加えて、コミュニティメンバーが互いに非公開でやり取りできます。

この機能は、[コミュニティサイト](/help/communities/overview.md#communitiessites)を作成する際に含めることができます。

メッセージング機能では、次の機能を利用できます。

**A**  - 1人または複数のコミュニティメンバーにメッセージを送信します

**B**  — ダイレクトメッセージを一括でコミュニティメ [ンバーグループに送信します](/help/communities/messaging.md#group-messaging)

**C**  — 添付ファイル付きのメッセージを送信

**D**  — メッセージを転送する

**E**  — メッセージに返信します

**F**  — メッセージを削除する

**G**  — 削除されたメッセージを復元

![messaging-section](assets/messaging-section.png)

![restore-message](assets/restore-message.png)

メッセージング機能を有効にして変更するには、以下を参照してください。

* [管理者向](/help/communities/messaging.md) けメッセージの設定
* [開発者向け](/help/communities/essentials-messaging.md) のメッセージ

>[!NOTE]
>
>`Compose Message, Message, or Message List`コンポーネント（`Communities`コンポーネントグループ内）を作成者編集モードでページに追加することはサポートされていません。

## メッセージングコンポーネントの設定{#configure-messaging-components}

コミュニティサイトのメッセージを有効にすると、追加の設定は不要になります。 デフォルトの設定を変更する必要がある場合は、情報が表示されます。

### メッセージ・リスト（メッセージ・ボックス）の構成{#configure-message-list-message-box}

メッセージング機能の&#x200B;**インボックス**、**送信済みアイテム**、**ごみ箱**&#x200B;ページのメッセージリストの設定を変更するには、[作成者編集モード](/help/communities/sites-console.md#authoring-site-content)でサイトを開きます。

1. `Preview`モードで、**メッセージ**&#x200B;リンクを選択して、メインメッセージページを開きます。 次に、「**インボックス**」、「**送信済みアイテム**」または「**ごみ箱**」を選択して、そのメッセージリスト用のコンポーネントを設定します。

1. `Edit`モードで、ページ上のコンポーネントを選択します。
1. 設定ダイアログにアクセスするには、`link`アイコンを選択して継承をキャンセルします。
継承がキャンセルされると、設定アイコンを選択して設定ダイアログを開くことができます。

1. 設定が完了したら、`broken link`アイコンを選択して継承を復元する必要があります。

![configure-message-list](assets/configure-message-list.png)

#### 「基本」タブ{#basic-tab}

![basic-tab-messagelist](assets/basic-tab-messagelist.png)

* **サービスセレクター**

   （*必須*）これを[AEM Communities Messaging Operations Service](/help/communities/messaging.md#messaging-operations-service)のプロパティ&#x200B;**`serviceSelector.name`**&#x200B;の値に設定します。

* **ページを作成**

   （*必須*）メンバーが&#x200B;**`Reply`**&#x200B;ボタンをクリックすると開くページ。 ターゲットページには、**メッセージを作成**&#x200B;フォームを含める必要があります。

* **リソースとして返信/表示**

   オンにすると、返信URLと表示URLでリソースが参照されます。オフにすると、データがURLでクエリパラメーターとして渡されます。

* **プロファイル表示フォーム**

   送信者のプロファイルの表示に使用するプロファイルフォーム。

* **ごみ箱フォルダ**

   オンにすると、このメッセージリストコンポーネントには、削除済み（ごみ箱）とフラグ付けされたメッセージのみが表示されます。

* **フォルダーパス**

   （*必須*） [AEM Communities Messaging Operations Service](/help/communities/messaging.md#messaging-operations-service)の&#x200B;**inbox.path.name**&#x200B;および&#x200B;**sentitems.path.name**&#x200B;に設定された値を参照します。 `Inbox`に対して設定する場合、**inbox.path.name**&#x200B;の値を使用して1つのエントリを追加します。 `Outbox`に対して設定する場合、**sentitems.path.name**&#x200B;の値を使用して1つのエントリを追加します。 `Trash`に対して設定する場合、両方の値を持つ2つのエントリを追加します。

#### 「表示」タブ{#display-tab}

![display-tab-message-list](assets/display-tab-message-list.png)

* **既読をマークボタン**

   オンにすると、メッセージを既読としてマークできる`Read`ボタンが表示されます。

* **未読のマークボタン**

   オンにすると、メッセージを既読としてマークできる`Mark Unread`ボタンが表示されます。

* **「削除」ボタン**

   オンにすると、メッセージを既読としてマークできる`Delete`ボタンが表示されます。 **`Message Options`**&#x200B;もオンにすると、削除機能が複製されます。

* **メッセージオプション**

   オンにすると、**`Reply`**、**`Reply All`**、**`Forward`**&#x200B;および&#x200B;**`Delete`**&#x200B;ボタンが表示され、メッセージを再送信または削除できます。 **`Delete Button`**&#x200B;もオンにすると、削除機能が複製されます。

* **1 ページのメッセージ数**

   指定された数は、ページネーションスキームで1ページに表示されるメッセージの最大数です。 数字を指定しない（空白のまま）場合、すべてのメッセージが表示され、ページネーションはありません。

* **タイムスタンプのパターン**

   1つ以上の言語のタイムスタンプパターンを指定します。 初期設定は en、de、fr、it、es、ja、zh_CN、ko_KR です。

* **ユーザーを表示**

   「**`Sender`**」または「**`Recipients`**」を選択して、「送信者」と「受信者」のどちらを表示するかを決定します。

### メッセージの構成{#configure-compose-message}を設定

メッセージを作成ページの設定を変更するには、[オーサー編集モード](/help/communities/sites-console.md#authoring-site-content)でサイトを開きます。

* `Preview`モードで、**メッセージ**&#x200B;リンクを選択して、メインメッセージページを開きます。 次に、「新しいメッセージ」ボタンを選択して`Compose Message`ページを開きます。

* `Edit`モードで、メッセージ本文を含むページ上のメインコンポーネントを選択します。
* 設定ダイアログにアクセスするには、`link`アイコンを選択して継承をキャンセルします。
継承がキャンセルされると、設定アイコンを選択して設定ダイアログを開くことができます。

* 設定が完了したら、`broken link`アイコンを選択して継承を復元する必要があります。

![config-compose-message](assets/config-compose-message.png)

#### 「基本」タブ{#basic-tab-1}

![basic-tab-compose](assets/basic-tab-compose.png)

* **リダイレクトURL**

   メッセージの送信後に表示されるページのURLを入力します。 （例：`../messaging.html`）。

* **キャンセル URL**

   送信者がメッセージをキャンセルした場合に表示されるページのURLを入力します。 （例：`../messaging.html`）。

* **メッセージの件名の最大長**

   「件名」フィールドに入力できる最大文字数です。 例：500 初期設定は無制限です。

* **メッセージ本文の最大長**

   「コンテンツ」フィールドに入力できる最大文字数です。 例：10000 初期設定は無制限です。

* **サービスセレクター**

   （*必須*）これを[AEM Communities Messaging Operations Service](/help/communities/messaging.md#messaging-operations-service)のプロパティ&#x200B;**`serviceSelector.name`**&#x200B;の値に設定します。

#### 「表示」タブ{#display-tab-1}

![display-tab-compose](assets/display-tab-compose.png)

* **件名フィールドの表示**

   オンにした場合、`Subject`フィールドを表示し、メッセージへの件名の追加を有効にします。 初期設定はオンになっていません。

* **件名ラベル**

   `Subject`フィールドの横に表示するテキストを入力します。 デフォルトは `Subject` です。

* **ファイルの添付フィールドを表示**

   オンにすると、`Attachment`フィールドを表示し、メッセージへの添付ファイルの追加を有効にします。 初期設定はオンになっていません。

* **添付ファイルのラベル**

   `Attachment`フィールドの横に表示するテキストを入力します。 デフォルトは **`Attach File`** です。

* **コンテンツフィールドを表示**

   オンにした場合、`Content`フィールドを表示し、メッセージ本文の追加を有効にします。 初期設定はオンになっていません。

* **コンテンツラベル**

   `Content`フィールドの横に表示するテキストを入力します。 デフォルトは **`Body`** です。

* **リッチテキストエディターを使用**

   オンにすると、独自のリッチテキストエディターを備えたカスタムコンテンツテキストボックスが使用されます。 初期設定はオンになっていません。

* **タイムスタンプのパターン**

   1つ以上の言語のタイムスタンプパターンを指定します。 初期設定は en、de、fr、it、es、ja、zh_CN、ko_KR です。
