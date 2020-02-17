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
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# メッセージング機能{#messaging-feature}

フォーラムやコメントで行われる一般に公開されるインタラクションに加えて、** **AEM Communitiesのメッセージング機能を使用すると、コミュニティメンバーは互いに非公開でやり取りできます。

This feature can be included when a [community site](/help/communities/overview.md#communitiessites) is created.

メッセージング機能を使用すると、次のことができます。

**A** - 1人以上のコミュニティメンバーB **— 直接メッセージをコミュニティメンバーグループに送る** - [C](/help/communities/messaging.md#group-messaging)C -************ C — メッセージを送るD — メッセージを送るD — メッセージを送るE - Bulk * Delete * Message * Delete * Message * F -

![messaging-section](assets/messaging-section.png) ![restore-message](assets/restore-message.png)

メッセージング機能を有効にして変更するには、次を参照してください。

* [管理者へのメッセージ](/help/communities/messaging.md) の設定
* [Messaging Essentials](/help/communities/essentials-messaging.md) for developers

>[!NOTE]
>
>作成者編集モードでページに(コ `Compose Message, Message, or Message List` ンポーネントグループにあ `Communities`る)コンポーネントを追加することはサポートされていません。

## メッセージングコンポーネントの設定 {#configure-messaging-components}

コミュニティサイトでメッセージングを有効にする場合、設定は不要です。 この情報は、デフォルト設定を変更する必要がある場合に表示されます。

### メッセージリストの設定（メッセージボックス） {#configure-message-list-message-box}

To modify the configuration of the list of messages for **Inbox**, **Sent Items**, and **Trash **pages of the messaging feature, open the site in [author edit mode](/help/communities/sites-console.md#authoring-site-content).

1. In `Preview`mode, select the **Messages **link to open the main messaging page. Then select either **Inbox**, **Sent Items **or **Trash **to configure the component for that message list.

1. In `Edit` mode, select the component on the page.
1. 設定ダイアログにアクセスするには、アイコンを選択して継承をキャンセル `link`します。
継承がキャンセルされると、設定アイコンを選択して設定ダイアログを開くことができます。

1. Once the configuration is complete, it is necessary to restore inheritance by selecting the `broken link` icon.

![configure-message-list](assets/configure-message-list.png)

#### 「基本」タブ{#basic-tab}

![basic-tab-messagelist](assets/basic-tab-messagelist.png)

* **サービスセレク**&#x200B;ター&#x200B;*(必須*)`serviceSelector.name`AEM Communities Messaging Operations Serviceのプロパティ****の値に設定します [](/help/communities/messaging.md#messaging-operations-service)。

* **構成ページ**(必&#x200B;*須*)：メンバーが**`Reply`**ボタンをクリックしたときに開くページ。 ターゲットページには、**メッセージを作成**&#x200B;フォームを含める必要があります。

* **リソースとして返信／表示**&#x200B;オンにすると、返信 URL と表示 URL がリソースを参照します。オフにすると、データは URL 内でクエリパラメーターとして渡されます。

* **プロファイルの表示フォーム**&#x200B;送信者のプロファイルの表示に使用するプロファイルフォームです。

* **ごみ箱フォルダー**&#x200B;オンにすると、このメッセージリストコンポーネントには、「削除済み」（ごみ箱）のフラグが設定されているメッセージのみが表示されます。

* **Folder Paths**(*必須*) **AEM Communities Messaging Operations Serviceでinbox.path.name** と**sentitems.path.name **に設定された値を参照します [](/help/communities/messaging.md#messaging-operations-service)。 When configuring for an `Inbox`, add one entry using the value of **inbox.path.name**. When configuring for an `Outbox`, add one entry using the value of **sentitems.path.name**. When configuring for `Trash`, add two entries with both values.

#### 「表示」タブ{#display-tab}

![display-tab-message-list](assets/display-tab-message-list.png)

* **既読ボタンをマーク**：オンの場合、メッセ `Read`ージを既読としてマークするボタンを表示します。

* **[未読にする]ボ**&#x200B;タンこのチェックボックスをオンにすると、メ `Mark Unread` ッセージを既読としてマークするボタンが表示されます。

* **削除ボタン**：オンにすると、既読とマ `Delete`ークするメッセージのボタンが表示されます。 Will duplicate the delete functionality if **`Message Options`** is also checked.

* **メッセージ**&#x200B;オプション：オンにす **`Reply`**&#x200B;ると、 **`Reply All`**、、、**`Forward`**および**`Delete`**ボタンが表示され、メッセージを再送または削除できます。 Will duplicate the delete functionality if **`Delete Button`** is also checked.

* **1 ページのメッセージ数**&#x200B;指定した数字がページネーションスキームで 1 ページに表示されるメッセージの最大数になります。数字を指定しない（空白のまま）場合、すべてのメッセージが表示され、ページネーションはありません。

* **タイムスタンプのパターン** 1 つ以上の言語に対してタイムスタンプのパターンを指定します。初期設定は en、de、fr、it、es、ja、zh_CN、ko_KR です。

* **ユーザーを表**&#x200B;示「**`Sender`**」または「**`Recipients`***」を選択して、送信者と受信者のどちらを表示するかを指定します。

### 構成メッセージの設定 {#configure-compose-message}

To modify the configuration of the compose message page, open the site in [author edit mode](/help/communities/sites-console.md#authoring-site-content).

* In `Preview`mode, select the **Messages **link to open the main messaging page. Then select the New Message button to open the `Compose Message` page.

* In `Edit` mode, select the main component on the page containing the Message body.
* 設定ダイアログにアクセスするには、アイコンを選択して継承をキャンセル `link`します。
継承がキャンセルされると、設定アイコンを選択して設定ダイアログを開くことができます。

* Once the configuration is complete, it is necessary to restore inheritance by selecting the `broken link`icon.

![config-compose-message](assets/config-compose-message.png)

#### 「基本」タブ{#basic-tab-1}

![basic-tab-compose](assets/basic-tab-compose.png)

* **リダイレクト URL**&#x200B;メッセージの送信後に表示されるページの URL を入力します。For example, `../messaging.html`.

* **キャンセル URL**&#x200B;送信者がメッセージをキャンセルした場合に表示されるページの URL を入力します。For example, `../messaging.html`.

* **メッセージ件名の最大の長さ**「件名」フィールドに許可される最大文字数です。例えば、500。 初期設定は無制限です。

* **メッセージ本文の最大の長さ**「コンテンツ」フィールドに許可される最大文字数です。例：10000 初期設定は無制限です。

* **サービスセレク**&#x200B;ター&#x200B;*(必須*)`serviceSelector.name`AEM Communities Messaging Operations Serviceのプロパティ****の値に設定します [](/help/communities/messaging.md#messaging-operations-service)。

#### 「表示」タブ{#display-tab-1}

![display-tab-compose](assets/display-tab-compose.png)

* **[件名フィールドを表示**]チェックボックスをオンにした場合は `Subject` 、フィールドを表示し、メッセージに件名を追加できます。 初期設定はオフです。

* **件名ラベル**&#x200B;フィールドの横に表示するテキストを入力 `Subject` します。 デフォルトは `Subject` です。

* **「添付ファイルフィールドを表示**」をオンにした場合 `Attachment` 、フィールドを表示し、メッセージに添付ファイルを追加できるようにします。 初期設定はオフです。

* **ファイルラベルを添**&#x200B;付フィールドの横に表示するテキストを入力 `Attachment` します。 デフォルトは **`Attach File`** です。

* **コンテンツフィールドを表示**：オンにした場合、フィールドを表 `Content` 示し、メッセージ本文の追加を有効にします。 初期設定はオフです。

* **コンテンツラ**&#x200B;ベルフィールドの横に表示するテキストを入力 `Content` します。 デフォルトは **`Body`** です。

* **リッチテキストエディターを使用**&#x200B;オンにすると、独自のリッチテキストエディターを使用するカスタムのコンテンツテキストボックスを使用することを意味します。初期設定はオフです。

* **タイムスタンプのパターン** 1 つ以上の言語に対してタイムスタンプのパターンを指定します。初期設定は en、de、fr、it、es、ja、zh_CN、ko_KR です。

