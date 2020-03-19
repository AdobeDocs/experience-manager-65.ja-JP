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
source-git-commit: e8d8bf89971d3d9d5ec150308dda247aa53c77bb

---


# メッセージング機能 {#messaging-feature}

AEM Communitiesのメッセージ機能を使用すると、フォーラムやコメントで公開されるインタラクションに加え、コミュニティメンバー同士でもっとプライベートにやり取りを行うことができます。

This feature can be included when a [community site](/help/communities/overview.md#communitiessites) is created.

メッセージ機能を使用すると、次のことができます。

**A** - 1つ以上のコミュニティメンバー&#x200B;**B** - [B](/help/communities/messaging.md#group-messaging)-**B** -**B** -**M** B -**C D****** C C C D C D MESSAGED Dest [D]Es ]EssEEEEEEEEEEEPEssEEEsEEBBB DBBBB SB B S

![messaging-section](assets/messaging-section.png) ![restore-message](assets/restore-message.png)

メッセージ機能を有効にして変更するには、次を参照してください。

* [管理者へのメッセージの設定](/help/communities/messaging.md) （英語のみ）
* [Messaging Essentials](/help/communities/essentials-messaging.md) for developers

>[!NOTE]
>
>作成者編集モードでページに(コ `Compose Message, Message, or Message List` ンポーネントグルー `Communities`プ内の)コンポーネントを追加することはサポートされていません。

## メッセージングコンポーネントの設定 {#configure-messaging-components}

コミュニティサイトでメッセージングが有効になっている場合、設定は不要です。 デフォルトの設定を変更する必要がある場合は、この情報が表示されます。

### メッセージリストの設定（メッセージボックス） {#configure-message-list-message-box}

To modify the configuration of the list of messages for **Inbox**, **Sent Items**, and **Trash** pages of the messaging feature, open the site in [author edit mode](/help/communities/sites-console.md#authoring-site-content).

1. In `Preview`mode, select the **Messages** link to open the main messaging page. Then select either **Inbox**, **Sent Items** or **Trash** to configure the component for that message list.

1. In `Edit` mode, select the component on the page.
1. 設定ダイアログにアクセスするには、アイコンを選択して継承をキャンセル `link`します。
継承がキャンセルされると、設定アイコンを選択して設定ダイアログを開くことができます。

1. Once the configuration is complete, it is necessary to restore inheritance by selecting the `broken link` icon.

![configure-message-list](assets/configure-message-list.png)

#### 「基本」タブ{#basic-tab}

![basic-tab-messagelist](assets/basic-tab-messagelist.png)

* **サービスセレクター**

   (*Required*) Set this to the value of the property **`serviceSelector.name`** from the [AEM Communities Messaging Operations Service](/help/communities/messaging.md#messaging-operations-service).

* **ページを作成**

   (必&#x200B;*須*)メンバーがボタンをクリックしたときに開くペ **`Reply`** ージ。 ターゲットページには、**メッセージを作成**&#x200B;フォームを含める必要があります。

* **リソースとして返信/表示**

   オンにすると、返信URLと表示URLがリソースを参照し、オフにすると、URL内のクエリパラメーターとしてデータが渡されます。

* **縦断表示フォーム**

   送信者プロファイルの表示に使用するプロファイルフォーム。

* **ごみ箱フォルダ**

   このチェックボックスをオンにすると、削除済み（ごみ箱）としてフラグ付けされたメッセージのみが表示されます。

* **フォルダパス**

   (*Required*) Referencing the values set for **inbox.path.name** and **sentitems.path.name** in the [AEM Communities Messaging Operations Service](/help/communities/messaging.md#messaging-operations-service). When configuring for an `Inbox`, add one entry using the value of **inbox.path.name**. When configuring for an `Outbox`, add one entry using the value of **sentitems.path.name**. When configuring for `Trash`, add two entries with both values.

#### 「表示」タブ{#display-tab}

![display-tab-message-list](assets/display-tab-message-list.png)

* **既読をマークボタン**

   If checked, displays a `Read`button allowing a message to be marked as read.

* **未読にするボタン**

   If checked, displays a `Mark Unread` button allowing a message to be marked as read.

* **削除ボタン**

   If checked, displays a `Delete`button allowing a message to be marked as read. Will duplicate the delete functionality if **`Message Options`** is also checked.

* **メッセージオプション**

   オンにすると、メッセージ **`Reply`**&#x200B;を再送 **`Reply All`**&#x200B;信または削 **`Forward`** 除できるボ **`Delete`** タン、ボタン、およびボタンが表示されます。 Will duplicate the delete functionality if **`Delete Button`** is also checked.

* **1 ページのメッセージ数**

   指定する数は、ページネーションスキームで1ページに表示されるメッセージの最大数です。 数字を指定しない（空白のまま）場合、すべてのメッセージが表示され、ページネーションはありません。

* **タイムスタンプのパターン**

   1つ以上の言語のタイムスタンプパターンを指定します。 初期設定は en、de、fr、it、es、ja、zh_CN、ko_KR です。

* **ユーザーを表示**

   またはを選択し **`Sender`** て、送 **`Recipients`** 信者と受信者のどちらを表示するかを指定します。

### メッセージを作成の設定 {#configure-compose-message}

To modify the configuration of the compose message page, open the site in [author edit mode](/help/communities/sites-console.md#authoring-site-content).

* In `Preview` mode, select the **Messages** link to open the main messaging page. Then select the New Message button to open the `Compose Message` page.

* In `Edit` mode, select the main component on the page containing the Message body.
* 設定ダイアログにアクセスするには、アイコンを選択して継承をキャンセル `link` します。
継承がキャンセルされると、設定アイコンを選択して設定ダイアログを開くことができます。

* Once the configuration is complete, it is necessary to restore inheritance by selecting the `broken link` icon.

![config-compose-message](assets/config-compose-message.png)

#### 「基本」タブ{#basic-tab-1}

![basic-tab-compose](assets/basic-tab-compose.png)

* **リダイレクトURL**

   メッセージの送信後に表示されるページのURLを入力します。 For example, `../messaging.html`.

* **キャンセル URL**

   送信者がメッセージをキャンセルした場合に表示されるページのURLを入力します。 For example, `../messaging.html`.

* **メッセージの件名の最大長**

   「件名」フィールドで許可される最大文字数。 例えば、500と入力します。 初期設定はno limitです。

* **メッセージ本文の最大長**

   「コンテンツ」フィールドで許可される最大文字数。 例：10000 初期設定はno limitです。

* **サービスセレクター**

   (*Required*) Set this to the value of the property **`serviceSelector.name`** from the [AEM Communities Messaging Operations Service](/help/communities/messaging.md#messaging-operations-service).

#### 「表示」タブ{#display-tab-1}

![display-tab-compose](assets/display-tab-compose.png)

* **件名フィールドを表示**

   チェックすると、フィールドを表示 `Subject` し、メッセージに件名を追加できるようになります。 デフォルトはチェックされていません。

* **件名ラベル**

   フィールドの横に表示するテキストを入力 `Subject` します。 デフォルトは `Subject` です。

* **ファイルの添付フィールドを表示**

   チェックすると、フィールドを表示し `Attachment` 、メッセージへの添付ファイルの追加を有効にします。 デフォルトはチェックされていません。

* **添付ファイルのラベル**

   フィールドの横に表示するテキストを入力 `Attachment` します。 デフォルトは **`Attach File`** です。

* **コンテンツフィールドを表示**

   チェックすると、フィールドを表示し `Content` 、メッセージ本文の追加を有効にします。 デフォルトはチェックされていません。

* **コンテンツラベル**

   フィールドの横に表示するテキストを入力 `Content` します。 デフォルトは **`Body`** です。

* **リッチテキストエディターを使用**

   オンの場合、独自のリッチテキストエディターでカスタムのコンテンツテキストボックスが使用されることを示します。 デフォルトはチェックされていません。

* **タイムスタンプのパターン**

   1つ以上の言語のタイムスタンプパターンを指定します。 初期設定は en、de、fr、it、es、ja、zh_CN、ko_KR です。

