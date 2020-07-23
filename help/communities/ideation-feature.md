---
title: アイディエーション機能
seo-title: アイディエーション機能
description: アイディエーション機能の追加と設定
seo-description: アイディエーション機能の追加と設定
uuid: 38468290-6d00-4ee4-91d8-7c2e8ae32712
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: a3f5a21d-2df6-4663-a1ea-3a067c46f860
docset: aem65
translation-type: tm+mt
source-git-commit: f62fb1eb760ddd7baee9ba5a631ff4b921e2d08b
workflow-type: tm+mt
source-wordcount: '1124'
ht-degree: 36%

---


# アイディエーション機能 {#ideation-feature}

## 概要 {#introduction}

アイディエーション機能は、パブリッシュ環境にサインインしているサイト訪問者（コミュニティメンバー）が以下を実行できる領域を提供します。

* コミュニティと共有するアイデアを作成します。
* アイデアに対する表示とコメント。
* 考えに従って。
* アイデアに投票する。

ドキュメントのこの節では、以下について説明します。

* AEMサイトへのアイデア作成機能の追加
* Ideationコンポーネントの設定です。

### ページへのアイディエーションの追加 {#adding-a-ideation-to-a-page}

To add a `Ideation` component to a page in author mode, use the component browser to locate

* `Communities / Ideation`

を探し、ページ上のアイデアを表示する位置にドラッグします。

For necessary information, visit [Communities Components Basics](/help/communities/basics.md).

[必要なクライアント側ライブラリが含まれる場合](/help/communities/ideation.md#essentials-for-client-side) 、次のようにコンポー `Ideation` ネントが表示されます。

![アイディエーション](assets/ideation.png)

### アイディエーションの設定 {#configuring-an-ideation}

Select the placed `Ideation` component to access and select the `Configure` icon which opens the edit dialog.

![configure-new](assets/configure-new.png)

![ideation-settings](assets/ideation-settings.png)

#### 「設定」タブ{#settings-tab}

「**[!UICONTROL 設定]**」タブでは、アイデアとコメントの基本機能を設定します。

* **添付サムネールを許可**
* **添付サムネールの最大サイズ**
* **サムネールの最小画像サイズ**
* **サムネールの最大サイズ**
* **権限を持つメンバーを許可**
* **許可された権限を持つメンバー**
* **作成者編集モードでユーザーが生成したコンテンツをブロックする**
* **アイディエーションのタイトル**

* アイデアの表示タイトル。 デフォルトは `Ideation` です。
* **アイディエーション説明**

   アイデアのサブタイトルとして表示する説明。 初期設定では、説明はありません。

* **1 ページのトピック数**

   ページあたりに表示するアイデア/投稿の数を定義します。 初期設定は 10 です。

* **モデレート**

   オンにした場合、アイデアやコメントの投稿は、投稿サイトに表示される前に承認される必要があります。 初期設定はオフです。

* **閉じる**

   このオプションを選択すると、新しいアイデアやコメントに対するイデエーションフォーラムが閉じられます。 初期設定はオフです。

* **リッチテキストエディター**

   オンにすると、アイデアやコメントはマークアップと共に入力される場合があります。 初期設定はオフです。

* **タグ付けを許可**

   If checked, allow members to add tag labels to their post (see **[!UICONTROL Tag field]** tab). 初期設定はオフです。

* **ファイルのアップロードを許可**

   オンにした場合、添付ファイルをアイデアまたはコメントに追加できるようにします。 初期設定はオフです。

* **最大ファイルサイズ**

   チェックされている場合にのみ関連 `Allow File Uploads` します。 このフィールドは、アップロードされるファイルのサイズ（バイト単位）を制限します。 初期設定は104857600(10 Mb)です。

* **許可されるファイルタイプ**

   チェックされている場合にのみ関連 `Allow File Uploads` します。 ドット付きのファイル拡張子をコンマ区切りで指定します（例：.jpg, .jpeg, .png, .doc, .docx, .pdf）。ファイルの種類が指定されている場合、指定されていないファイルはアップロードできません。 初期設定は、すべてのファイルタイプを許可するように指定されません。

* **添付する画像ファイルの最大サイズ**

   「ファイルのアップロードを許可」がオンになっている場合にのみ関連します。 アップロードされた画像ファイルの最大バイト数。 初期設定は2097152(2 Mb)です。

* **応答を許可**

   オンの場合、アイデアに投稿されたコメントへの返信を許可します。 初期設定はオフです。

* **投票を許可**

   オンにした場合、アイデアのコメントに対する投票を許可します。 初期設定はオフです。

* **ユーザーによるコメントおよびトピックの削除を許可**

   オンの場合、メンバーが投稿したコメントやアイデアを削除できるようにします。 初期設定はオフです。

* **フォローを許可**

   If checked, include the following feature for idea posts, which allows members to be [notified](/help/communities/notifications.md) of new posts. 初期設定はオフです。

* **電子メール購読を許可**

   If checked, allow members to be notified of new posts by email ([subscription](/help/communities/subscriptions.md)). Requires `Allow Following` to be checked and [email configured](/help/communities/email.md). 初期設定はオフです。

* **投票を許可**

   オンにした場合、アイデアのコメントに対する投票を許可します。 初期設定はオフです。

* **バッジを表示**

   If checked, display earned and assigned [badges](/help/communities/implementing-scoring.md) with a member&#39;s idea. 初期設定はオフです。

* **リストページで返信を受け取らない**

* **おすすめコンテンツを許可**

   If checked, the idea is able to be identified as [featured content](/help/communities/featured.md). 初期設定はオフです。

* **メンションを有効化**
* **最大メンション数**
* **UI メンションパターン**

#### 「ユーザーモデレート」タブ{#user-moderation-tab}

Under the **[!UICONTROL User Moderation]** tab, specify how the posted ideas and comments (user generated content) are managed. For more information, see [Moderating User Generated Content](/help/communities/moderate-ugc.md).

* **投稿を拒否**

   オンにすると、信頼されたメンバーのモデレーターは、投稿を拒否し、投稿がパブリックフォーラムに表示されないように許可されます。 初期設定はオフです。

* **トピックを閉じる / 再度開く**

   オンにすると、信頼されたメンバーのモデレーターがトピックを閉じて、さらに編集やコメントを行ったり、トピックを再度開いたりすることができます。 初期設定はオフです。

* **投稿にフラグを設定**

   このオプションを選択すると、他のユーザーのトピックやコメントに不適切なフラグを付けることができます。 初期設定はオフです。

* **フラグ設定理由リスト**

   オンにした場合、メンバーは、トピックまたはコメントに不適切なフラグを付ける理由をドロップダウンリストから選択できます。 初期設定はオフです。

* **カスタムフラグ設定理由**

   このオプションを選択すると、トピックやコメントに不適切なフラグを付ける理由をメンバーが自分で入力できます。 初期設定はオフです。

* **モデレートのしきい値**

   モデレーターに通知する前に、トピックまたはコメントにメンバーがフラグを付ける必要がある回数を入力します。 初期設定は1（1回）です。

* **フラグ付けの制限**

   トピックまたはコメントが公開表示に表示されなくなる前にフラグを付ける必要がある回数を入力します。 -1に設定した場合、フラグ付けされたトピックまたはコメントはパブリック表示に表示されません。 それ以外の場合は、この数値をモデレートしきい値以上にする必要があります。 初期設定は 5 です。

#### 「タグフィールド」タブ{#tag-field-tab}

「**[!UICONTROL タグフィールド]**」タブでは、「**[!UICONTROL 設定]**」タブでタグ付けが許可されている場合に、適用できるタグを名前空間に従って制限します。

* **許可された名前空間**

   「 `Allow Tagging` 設定 **** 」タブでチェックされている場合に関連します。 適用できるタグは、チェック対象の名前空間カテゴリ内のタグに限定されます。 名前空間のリストには、「標準タグ」(デフォルトの名前空間)と「すべてのタグを含む」があります。 初期設定はオフで、すべての名前空間が許可されます。

* **推奨の制限**

   フォーラムに投稿するメンバーに対して提案として表示するタグの数を入力します。 A value of **-1** means no limit. 初期設定は 0 です。

#### 「並べ替え設定」タブ{#sort-settings-tab}

Under the **[!UICONTROL Sort Settings]** tab, specify how the posted comments are sorted when displayed.

* **並べ替え**

   許可されている並べ替えの選択項目をすべて選択： `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. デフォルトは `Newest, Oldest, Last Updated` です。

* **デフォルトとして設定**

   デフォルトとして表示する、チェック済みの並べ替えオプションの1つをプルダウンして選択します。 デフォルトは `Newest` です。

* **Analytics 並べ替えのタイムオプションを選択**

   プルダウンしていずれかを選択し `All, Last 24 Hours, Last 7 Days, Last 30 Days`ます。 デフォルトは `All` です。

## サイト訪問者のエクスペリエンス {#site-visitor-experience}

### アイデアの作成 {#creating-idea}

Communities のすべての機能と同様に、サインインしていない場合、サイト訪問者はアイデアを読むことと、他のユーザーの（コメントや投票／「いいね!」を通じた）意見を見ることしかできません。

メンバーはサインインすると、新しいアイデアを作成できます。

![新しいアイデアを生み出す](assets/create-new-idea.png)

アイデアを送信する前に、ドラフトとして保存できます。

この `Save as Draft` ボタンを選択すると、ドラフトが保存されます。

![節約案](assets/save-idea.png)

保存したドラフトを `My Drafts` タブで表示する場合、編集モード `Read More` を再開する場合に選択します。

![編集アイデア](assets/edit-idea.png)

#### フィードバックの提供 {#providing-feedback}

Once the idea is published, other members can sign in, open the idea ( `Read More`) and like the idea, thus adding to the vote count, and make comments.

![feedback](assets/feedback-idea.png)

### 追加情報 {#additional-information}

開発者向けの詳細情報は、[アイディエーションの基本事項](/help/communities/ideation.md)ページを参照してください。

投稿されたトピックとコメントのモデレートについては、[ユーザー生成コンテンツのモデレート](/help/communities/moderate-ugc.md)を参照してください。

投稿されたトピックとコメントのタグ付けについては、[ユーザー生成コンテンツのタグ付け](/help/communities/tag-ugc.md)を参照してください。
