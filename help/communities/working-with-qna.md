---
title: Q&A フォーラム機能
seo-title: Q&A フォーラム機能
description: Q&A フォーラム機能をページに追加
seo-description: Q&A フォーラム機能をページに追加
uuid: e0d95009-0d04-4fa7-8d05-5948c4e37f08
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 6e6ffe09-c50b-4238-8b8c-597c133d0a9e
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Q&amp;A フォーラム機能{#q-a-forum-feature}

## 概要 {#introduction}

QnA(Q&amp;A)フォーラム機能は、コミュニティメンバーが質問をし、質問に答えるための領域を提供します。 これにより、メンバーは次のことができます。

* 新しい質問の作成
* インライン画像の追加（ドラッグ&amp;ドロップのサポートあり）
* 質問の表示と回答
* 質問の検索
* QnAコンテンツのモデレートの支援
* 最適な回答の特定
* QnA質問をページ間で移動する

このドキュメントでは、以下の内容を説明しています。

* Q&amp;A フォーラム機能を AEM サイトに追加.
* configuration settings for the `QnA`component.

## Q&amp;A フォーラムをページに追加 {#adding-a-q-a-forum-to-a-page}

作成者モードでペ `QnA` ージにコンポーネントを追加するには、コンポーネントブラウザーを使用してQnAフォーラムが表示さ `Communities / QnA`れるページ上の場所にコンポーネントを配置し、ドラッグします。

For necessary information, visit [Communities Components Basics](/help/communities/basics.md).

When the [required client-side libraries](/help/communities/qna-essentials.md#essentials-for-client-side) are included, this is how the `QnA`component appears:

![chlimage_1](assets/chlimage_1.png)

### Q&amp;A の設定 {#configuring-qna}

Select the placed `QnA` component to access and select the `Configure` icon which opens the edit dialog.

![chlimage_1-1](assets/chlimage_1-1.png)![qna-config](assets/qna-config.png)

#### 「設定」タブ{#settings-tab}

「**設定**」タブでは、トピック（質問）と返信（回答）の基本機能を設定します。

* **添付サムネールを許可**

   オンにすると、添付された画像のサムネールが作成されます。

* **添付サムネールの最大サイズ**

   添付ファイルのサムネール画像の最大サイズ（ピクセル単位）。 デフォルト値は、800 x 800 です。

* **サムネールの最小画像サイズ**

   インライン画像のサムネールを生成するための画像の最小サイズ（バイト）。 デフォルト値は100000バイト(100 KB)です。

* **サムネールの最大サイズ**

   インライン画像のサムネール画像の最大サイズ（ピクセル単位）。 デフォルト値は、800 x 800 です。

* **1 ページのトピック数**

   1ページに表示する質問数/投稿数を定義します。 初期設定は 10 です。

* **モデレート**

   オンにした場合、トピックとコメントの投稿は、公開サイトに表示される前に承認する必要があります。 デフォルト値はオフです。

* **閉じる**

   選択すると、フォーラムは新しい質問とコメントに対して閉じられます。 デフォルト値はオフです。

* **リッチテキストエディター**

   オンにすると、トピックとコメントをマークアップと共に入力できます。 デフォルト値はオフです。

* **タグ付けを許可**

   If checked, allow members to add tag labels to their post (see **Tag field** tab). デフォルト値はオフです。

* **ファイルのアップロードを許可**

   選択すると、添付ファイルを質問またはコメントに追加できます。 デフォルト値はオフです。

* **フォローを許可**

   If checked, include the following feature for forum posts, which allows members to be [notified](/help/communities/notifications.md) of new posts. デフォルト値はオフです。

* **ピン留めを許可**

   オンにすると、フォーラムトピックをトピックのリストの先頭に固定できます。 デフォルト値はオフです。

* **電子メール購読を許可**

   If checked, allow members to be notified of new posts by email ([subscription](/help/communities/subscriptions.md)). 「フォローを許可」をオンにして、[電子メールを設定](/help/communities/email.md)する必要があります。デフォルト値はオフです。

* **最大ファイルサイズ**

   がオンの場合にのみ `Allow File Uploads` 関連します。 このフィールドは、アップロードするファイルのサイズ（バイト単位）を制限します。初期設定は104857600(10 Mb)です。

* **許可されるファイルタイプ**

   がオンの場合にのみ `Allow File Uploads` 関連します。 区切り文字「。」を含むファイル拡張子のコンマ区切りリスト。 例：.jpg, .jpeg, .png, .doc, .docx, .pdf）。ファイルタイプを指定した場合、指定しなかったファイルタイプはアップロードできません。 初期設定は、** **すべてのファイルタイプを許可するように指定されていない。

* **添付する画像ファイルの最大サイズ**

   「ファイルのアップロードを許可」がオンになっている場合にのみ関連します。 アップロードされた画像ファイルに含めることができる最大バイト数。 初期設定は2097152** **(2 Mb)です。

* **応答を許可**

   選択した場合、質問に投稿されたコメントへの返信を許可します。 デフォルト値はオフです。
* **投票を許可**

   選択した場合、質問に投票機能を含めます。 デフォルト値はオフです。

* **ユーザーによるコメントおよびトピックの削除を許可**

   オンにした場合、メンバーは投稿したコメントや質問を削除できます。 初期設定は** **選択解除されています。

* **権限を持つメンバーを許可**

   オンにすると、特権を持つメンバーのみがコンテンツを作成できます。

* **作成者編集モードでユーザーが生成したコンテンツをブロックする**

   有効にすると、作成者モードでの編集中にユーザー生成コンテンツがブロックされます。

* **選択した回答を上に移動**選択すると、最初に表示される回答は選択した回答になります。 デフォルト値はオフです。
* **バッジを表示**

   If checked, display earned and assigned [badges](/help/communities/implementing-scoring.md) with a member&#39;s blog entry. デフォルト値はオフです。

* **おすすめコンテンツを許可**

   if checked, the idea is able to be identified as [featured content](/help/communities/featured.md). デフォルト値はオフです。

* **メンションを有効化**

   有効にすると、登録済みコミュニティユーザーは、他の登録済みメンバー（名、姓、ユーザー名を使用）を識別し、共通の@user-name構文を使用してタグ付けできます。 タグ付きユーザーは、メンションに関する通知を受け取ります。

* **最大メンション数**

   投稿で許可されるメンションの最大数を制限します。 初期設定は 10 です。

* **UI メンションパターン**

   投稿内の登録ユーザーにタグ付け(@mention)するために許可されているパターン文字列を指定します。 例えば、～{{familyName}}{{givenName}}のように指定します。

#### 「ユーザーモデレート」タブ{#user-moderation-tab}

Under the **User Moderation** tab, specify how the posted topics (questions) and answers (user generated content) are managed. For more information, see [Moderating User Generated Content](/help/communities/moderate-ugc.md).

* **回答を拒否**

   選択すると、信頼できるメンバーのモデレーターは、投稿された回答を拒否し、公開Q&amp;Aフォーラムに回答が表示されないようにします。 デフォルト値はオフです。

* **トピックを閉じる / 再度開く**

   選択すると、信頼されたメンバーのモデレーターは、質問（トピック）を閉じて、さらに編集や回答を行ったり、質問を再度開いたりできます。 デフォルト値はオフです。

* **トークンを移動**&#x200B;オンにすると、パブリッシュ側のモデレーターが質問を移動できます。デフォルト値はオフです。

* **投稿にフラグを設定**

   選択すると、他のユーザーの質問や回答に不適切としてフラグを付けることを許可します。 デフォルト値はオフです。

* **フラグ設定理由リスト**

   選択すると、メンバーは、質問または回答に不適切としてフラグを付ける理由をドロップダウンリストから選択できます。 デフォルト値はオフです。

* **カスタムフラグ設定理由**

   選択すると、質問または回答に不適切としてフラグを付ける独自の理由をメンバーが入力できるようになります。 デフォルト値はオフです。

* **モデレートのしきい値**

   モデレーターに通知する前に、メンバーが質問または回答にフラグを付ける必要がある回数を入力します。 初期設定は1（1回）です。

* **フラグ付けの制限**

   質問または回答が公開ビューに表示されないようにするためにフラグを付ける必要がある回数を入力します。 -1に設定した場合、フラグ付けされた質問または回答は公開ビューに表示されません。 そうでない場合、この数値はモデレートのしきい値以上にする必要があります。 初期設定は 5 です。

#### 「タグフィールド」タブ{#tag-field-tab}

Under the **Tag field** tab, the tags that can be applied, if allowed under the **Settings **tab, are limited according to namespaces chosen.

* ****Settings ****&#x200B;タブでチェ `Allow Tagging` ック済みの場合は、「Namespaces Relevant」を使用できます。 適用できるタグは、チェックされた名前空間カテゴリ内のタグに制限されます。 名前空間のリストには、「Standard Tags」（デフォルトの名前空間）と「Include All Tags」が含まれます。 初期設定はnoneで、すべての名前空間が許可されます。

* **推奨の制限**&#x200B;フォーラムに投稿するメンバーに表示する推奨タグの数を入力します。値**-**1は、制限がないことを意味します。 初期設定は 0 です。

#### 「並べ替え設定」タブ{#sort-settings-tab}

Under the **Sort Settings** tab, specify how the posted comments are sorted when displayed.

* **並べ替え**

   許可されている並べ替えの選択項目をすべて選択： `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. デフォルトは `Newest, Oldest, Last Updated` です。

* **デフォルトとして設定**

   デフォルトとして表示するオンの並べ替えオプションの1つを選択するには、プルダウンします。 デフォルトは `Newest` です。

* **Analytics 並べ替えのタイムオプションを選択**

   ドロップダウンして、いずれかを選択しま `All, Last 24 Hours, Last 7 Days, Last 30 Days`す。 デフォルトは `All` です。

## サイト訪問者のエクスペリエンス {#site-visitor-experience}

### 回答の指定 {#identifying-answers}

One answer can be marked as a correct or useful answer using the `Select Answer` button. Once a Question is marked as Answered, another answer cannot be selected until the first one has been deselected using the `Unmark Chosen Answer`button.

実行可能な回答として選択した後は、ボタンを使用して選択を解除で `Unmark Chosen Answer` きます。

Once an answer is selected as the viable answer, an indication that the question has been `Answered`is displayed next to the question topic on the main QnA page.

#### モデレーターおよび管理者 {#moderators-and-administrators}

サインインしているユーザーがモデレーター権限または管理者権限を持っている場合は、誰が質問または回答を作成したかにかかわらず、コンポーネントの設定によって許可されているモデレートタスクを実行できます。

また、回答を識別することもできます。

#### メンバー {#members}

サイト訪問者がログインした場合、設定に応じて、次のことが可能です。

* 新しい質問を投稿する.
* 自分が作成した質問を編集または削除する.
* 他のメンバーの質問や回答にフラグを付けます。
* 作成した質問に対する回答を特定します。

#### 匿名 {#anonymous}

サインインしていないサイト訪問者は、投稿された質問と回答を読み、サポートされている場合は翻訳するだけで、質問を追加したり、回答を追加したり、他の人の投稿にフラグを付けたりすることはできません。

## 追加情報 {#additional-information}

More information can be found on the [QnA Essentials](/help/communities/qna-essentials.md) page for developers.

投稿されたトピックとコメントのモデレートについては、[ユーザー生成コンテンツのモデレート](/help/communities/moderate-ugc.md)を参照してください。

投稿されたトピックとコメントのタグ付けについては、[ユーザー生成コンテンツのタグ付け](/help/communities/tag-ugc.md)を参照してください。
