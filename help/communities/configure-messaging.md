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
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 11%

---


# メッセージング機能 {#messaging-feature}

AEM Communitiesのメッセージ機能は、フォーラムやコメントで公開されたインタラクションに加え、コミュニティメンバー同士がもう一度個人的に交流できるようにします。

この機能は、[コミュニティサイト](/help/communities/overview.md#communitiessites)が作成されたときに含めることができます。

メッセージ機能を使用すると、次のことができます。

**A** -1人以上のコミュニティメンバーにメッセージを送信します。

**B**  — ダイレクトメッセージを [一括してコミュニティのメンバーグループに送信](/help/communities/messaging.md#group-messaging)

**C**  — メッセージに添付ファイルを送信

**D**  — メッセージを転送します。

**E**  — メッセージに返信

**F**  — メッセージを削除

**G**  — 削除したメッセージを復元します

![messaging-section](assets/messaging-section.png)

![restore-message](assets/restore-message.png)

メッセージ機能を有効にして変更するには、次を参照してください。

* [管理者向けの](/help/communities/messaging.md) メッセージの設定
* [開発者へのメッセージ](/help/communities/essentials-messaging.md) の基本

>[!NOTE]
>
>`Compose Message, Message, or Message List`コンポーネント（`Communities`コンポーネントグループにあります）をページに追加する場合は、作成者編集モードではサポートされません。

## メッセージングコンポーネントの設定{#configure-messaging-components}

コミュニティサイトでメッセージングを有効にすると、それ以上の設定は不要に設定されます。 この情報は、デフォルトの設定を変更する必要がある場合に表示されます。

### メッセージリストの構成（メッセージボックス） {#configure-message-list-message-box}

メッセージング機能の&#x200B;**インボックス**、**送信済みアイテム**、**ごみ箱**&#x200B;ページのメッセージリストの設定を変更するには、[作成者編集モード](/help/communities/sites-console.md#authoring-site-content)でサイトを開きます。

1. `Preview`モードで、**メッセージ**&#x200B;リンクを選択して、メインメッセージングページを開きます。 次に、「インボックス&#x200B;**」、「**&#x200B;送信済みアイテム&#x200B;**」、「**&#x200B;ごみ箱&#x200B;**」のいずれかを選択し、そのメッセージリストのコンポーネントを設定します。**

1. `Edit`モードで、ページ上のコンポーネントを選択します。
1. 設定ダイアログにアクセスするには、`link`アイコンを選択して継承をキャンセルします。
継承がキャンセルされると、設定アイコンを選択して設定ダイアログを開くことができます。

1. 設定が完了したら、`broken link`アイコンを選択して継承を復元する必要があります。

![configure-message-リスト](assets/configure-message-list.png)

#### 「基本」タブ{#basic-tab}

![basic-tab-messagelist](assets/basic-tab-messagelist.png)

* **サービスセレクター**

   （*必須*）[AEM Communitiesメッセージング操作サービス](/help/communities/messaging.md#messaging-operations-service)のプロパティ&#x200B;**`serviceSelector.name`**&#x200B;の値に設定します。

* **構成ページ**

   （*必須*）メンバーが「**`Reply`**」ボタンをクリックしたときに開くページ。 ターゲットページには、**メッセージを作成**&#x200B;フォームを含める必要があります。

* **リソースとしての返信/表示**

   オンの場合、返信URLと表示URLはリソースを参照し、それ以外の場合、データはURLのクエリパラメーターとして渡されます。

* **プロファイル表示フォーム**

   送信者のプロファイルの表示に使用するプロファイルフォーム。

* **ごみ箱フォルダ**

   このチェックボックスをオンにすると、このメッセージリストコンポーネントは、削除済み（ごみ箱）としてフラグ付けされたメッセージのみを表示します。

* **Folder Paths**

   （*必須*）[AEM Communitiesメッセージング操作サービス](/help/communities/messaging.md#messaging-operations-service)の&#x200B;**inbox.path.name**&#x200B;および&#x200B;**sentitems.path.name**&#x200B;に設定された値を参照します。 `Inbox`の設定時に、**inbox.path.name**&#x200B;の値を使用してエントリを1つ追加します。 `Outbox`の設定時に、**sentitems.path.name**&#x200B;の値を使用してエントリを1つ追加します。 `Trash`の設定時に、両方の値を持つ2つのエントリを追加します。

#### 「表示」タブ{#display-tab}

![display-tab-message-リスト](assets/display-tab-message-list.png)

* **既読をマークボタン**

   オンにすると、`Read`ボタンが表示され、メッセージを既読としてマークできます。

* **未読にするボタン**

   オンにすると、`Mark Unread`ボタンが表示され、メッセージを既読としてマークできます。

* **削除ボタン**

   オンにすると、`Delete`ボタンが表示され、メッセージを既読としてマークできます。 **`Message Options`**&#x200B;もチェックされている場合は、削除機能を重複します。

* **メッセージオプション**

   オンにすると、**`Reply`**、**`Reply All`**、**`Forward`**、**`Delete`**&#x200B;の各ボタンが表示され、メッセージを再送または削除できます。 **`Delete Button`**&#x200B;もチェックされている場合は、削除機能を重複します。

* **1 ページのメッセージ数**

   指定する数値は、ページネーションスキームで1ページに表示されるメッセージの最大数です。 数字を指定しない（空白のまま）場合、すべてのメッセージが表示され、ページネーションはありません。

* **タイムスタンプのパターン**

   1つ以上の言語のタイムスタンプパターンを指定します。 初期設定は en、de、fr、it、es、ja、zh_CN、ko_KR です。

* **ユーザーを表示**

   **`Sender`**&#x200B;または&#x200B;**`Recipients`**&#x200B;を選択して、送信者と受信者のどちらを表示するかを決定します。

### 構成メッセージの構成{#configure-compose-message}

構成メッセージページの設定を変更するには、[作成者編集モード](/help/communities/sites-console.md#authoring-site-content)でサイトを開きます。

* `Preview`モードで、**メッセージ**&#x200B;リンクを選択して、メインメッセージングページを開きます。 次に、「新しいメッセージ」ボタンを選択して`Compose Message`ページを開きます。

* `Edit`モードで、メッセージの本文を含むページのメインコンポーネントを選択します。
* 設定ダイアログにアクセスするには、`link`アイコンを選択して継承をキャンセルします。
継承がキャンセルされると、設定アイコンを選択して設定ダイアログを開くことができます。

* 設定が完了したら、`broken link`アイコンを選択して継承を復元する必要があります。

![config-compose-message](assets/config-compose-message.png)

#### 「基本」タブ{#basic-tab-1}

![basic-tab-compose](assets/basic-tab-compose.png)

* **リダイレクトURL**

   メッセージの送信後に表示されるページのURLを入力します。 例： `../messaging.html`

* **キャンセル URL**

   送信者がメッセージをキャンセルした場合に表示されるページのURLを入力します。 例： `../messaging.html`

* **メッセージの件名の最大長**

   件名フィールドに入力できる最大文字数。 例えば、500のように指定します。 初期設定はno limitです。

* **メッセージ本文の最大長**

   「コンテンツ」フィールドで許可される最大文字数。 例えば、10000のように指定します。 初期設定はno limitです。

* **サービスセレクター**

   （*必須*）[AEM Communitiesメッセージング操作サービス](/help/communities/messaging.md#messaging-operations-service)のプロパティ&#x200B;**`serviceSelector.name`**&#x200B;の値に設定します。

#### 「表示」タブ{#display-tab-1}

![display-tab-compose](assets/display-tab-compose.png)

* **件名フィールドを表示**

   オンにした場合、`Subject`フィールドを表示し、メッセージに件名を追加できるようにします。 デフォルトはチェックされていません。

* **件名ラベル**

   `Subject`フィールドの横に表示するテキストを入力します。 デフォルトは `Subject` です。

* **ファイルの添付フィールドを表示**

   オンにした場合、`Attachment`フィールドを表示し、添付ファイルをメッセージに追加できるようにします。 デフォルトはチェックされていません。

* **添付ファイルのラベル**

   `Attachment`フィールドの横に表示するテキストを入力します。 デフォルトは **`Attach File`** です。

* **コンテンツフィールドを表示**

   オンの場合、`Content`フィールドを表示し、メッセージ本文の追加を有効にします。 デフォルトはチェックされていません。

* **コンテンツラベル**

   `Content`フィールドの横に表示するテキストを入力します。 デフォルトは **`Body`** です。

* **リッチテキストエディターを使用**

   オンの場合、独自のリッチテキストエディターでカスタムのコンテンツテキストボックスが使用されることを示します。 デフォルトはチェックされていません。

* **タイムスタンプのパターン**

   1つ以上の言語のタイムスタンプパターンを指定します。 初期設定は en、de、fr、it、es、ja、zh_CN、ko_KR です。

