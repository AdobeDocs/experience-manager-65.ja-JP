---
title: フォーラム機能
seo-title: フォーラム機能
description: フォーラム機能を追加および設定する方法
seo-description: フォーラム機能を追加および設定する方法
uuid: e69be4e1-c9d5-4d51-8e7e-609e5460e378
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: d936cef5-ad76-482d-97bf-c40137185812
docset: aem65
translation-type: tm+mt
source-git-commit: 58a06c1a16c62bffad2893fbec0b32d2ce7267a7

---


# フォーラム機能{#forum-feature}

## 概要 {#introduction}

フォーラム機能は、パブリッシュ環境にサインインしているサイト訪問者（コミュニティメンバー）が以下を実行できる領域を提供します。

* 新しいトピックの作成
* 表示とトピックへの返信
* トピックのフォロー
* フォーラムの検索
* フォーラムのコンテンツのモデレートの支援
* フォーラムトピックを別のページに移動する

ドキュメントのこの節では、以下の内容について説明します。

* AEMサイトへのフォーラム機能の追加
* Configuration settings for the `Forum`component.

### フォーラムをページに追加 {#adding-a-forum-to-a-page}

To add a `Forum` component to a page in author mode, use the component browser to locate

* `Communities / Forum`

コンポーネントを探し、ページ上のフォーラムを表示する位置にドラッグします。

For necessary information, visit [Communities Components Basics](/help/communities/basics.md).

When the [required client-side libraries](/help/communities/essentials-forum.md#essentials-for-client-side) are included, this is how the `Forum`component will appear :

![chlimage_1-104](assets/chlimage_1-104.png)

### フォーラムの設定 {#configuring-a-forum}

Select the placed `Forum` component to access and select the `Configure` icon which opens the edit dialog.

![chlimage_1-105](assets/chlimage_1-105.png) ![forum-config](assets/forum-config.png)

#### 「設定」タブ{#settings-tab}

「**設定**」タブでは、トピックと返信の基本機能を設定します。

* **添付サムネールを許可**

   オンにすると、添付された画像のサムネールが作成されます。

* **添付サムネールの最大サイズ**

   添付ファイルのサムネール画像の最大サイズ（ピクセル単位）。 デフォルト値は、800 x 800 です。

* **サムネールの最小画像サイズ**
* **サムネールの最大サイズ**

   インライン画像のサムネール画像の最大サイズ（ピクセル単位）。 デフォルト値は、800 x 800 です。

* **1 ページのトピック数**

   1 ページあたりに表示されるトピック / 投稿の数を定義します。デフォルト値は 10 です。

* **モデレート**

   オンにした場合、トピックとコメントの投稿は、公開サイトに表示される前に承認する必要があります。 初期設定はオフです。

* **閉じる**

   オンにすると、フォーラムは新しいトピックとコメントに対して閉じられます。 初期設定はオフです。

* **リッチテキストエディター**

   チェックすると、トピックとコメントがマークアップと共に入力される場合があります。 初期設定はオフです。

* **タグ付けを許可**

   If checked, allow members to add tag labels to their post (see **Tag field** tab). 初期設定はオフです。

* **ファイルのアップロードを許可**

   オンにした場合、添付ファイルをトピックまたはコメントに追加できます。 初期設定はオフです。

* **フォローを許可**

   If checked, include the following feature for forum posts, which allows members to be [notified](/help/communities/notifications.md) of new posts. 初期設定はオフです。

* **ピン留めを許可**

   オンにすると、フォーラムトピックがトピックのリストの上部に固定されます。 初期設定はオフです。

* **おすすめコンテンツを許可**

   If checked, the idea is able to be identified as [featured content](/help/communities/featured.md). 初期設定はオフです。

* **電子メール購読を許可**

   If checked, allow members to be notified of new posts by email ([subscription](/help/communities/subscriptions.md)). Requires `Allow Following` to be checked and [email configured](/help/communities/email.md). 初期設定はオフです。

* **最大ファイルサイズ**

   がオンの場合のみ `Allow File Uploads` 関連します。 このフィールドは、アップロードされるファイルのサイズ（バイト単位）を制限します。 初期設定は104857600(10 Mb)です。

* **許可されるファイルタイプ**

   がオンの場合のみ `Allow File Uploads` 関連します。 ドット付きのファイル拡張子をコンマ区切りで指定します（例：.jpg, .jpeg, .png, .doc, .docx, .pdf）。ファイルの種類が指定されている場合、指定されていないファイルはアップロードできません。 初期設定は、すべてのファイルタイプが許可されるように指定されない。

* **Max Attach Image File Size** Relevant only if Allow File Uploadsがチェックされている場合のみ。 アップロードされた画像ファイルの最大バイト数。 初期設定は2097152(2 Mb)です。

* **スレッド化された返信を許可**

   オンにすると、トピックに投稿されたコメントへの返信を許可します。 初期設定はオフです。

* **投票を許可**

   オンの場合、トピックに投票機能を含めます。 初期設定はオフです。

* **ユーザーによるコメントおよびトピックの削除を許可**

   オンにすると、投稿したコメントやトピックの削除をメンバーに許可します。 初期設定はオフです。

* **パンくずリストを表示**

   オンにすると、トピックページのナビゲーション階層を表示します。 初期設定はオンです。

* **バッジを表示**

   If checked, display earned and assigned [badges](/help/communities/implementing-scoring.md) with a member&#39;s blog entry. 初期設定はオフです。

* **権限を持つメンバーを許可**

   オンにすると、特権を持つメンバーのみがコンテンツの作成を許可されます。

* **許可された権限を持つメンバー**

   特権追加を持つメンバーは、コンテンツの作成を許可されます。

* **作成者編集モードでユーザーが生成したコンテンツをブロックする**

   有効にすると、作成者モードでの編集中にユーザー生成コンテンツがブロックされます。

* **メンションを有効化**

   有効にすると、登録済みコミュニティユーザーは、他の登録済みメンバー（名、姓、ユーザー名を使用）を識別し、共通の@user-name構文を使用してタグ付けできます。 タグ付きユーザーは、メンションに関する通知を受信します。

* **最大メンション数**

   投稿で許可するメンションの最大数を制限します。 初期設定は 10 です。

* **UI メンションパターン**

   投稿内の登録ユーザーにタグ(@mention)を付けるために許可されたパターン文字列を指定します。 例えば、`~{{familyName}}{{givenName}}` のように指定します。

>[!NOTE]
>
>トピックに対するコメントを有効にするには、との両方 `AllowThreaded Replies` を確認す `Allow users to Delete Comments and Topics` る必要がある場合があります。


#### 「ユーザーモデレート」タブ{#user-moderation-tab}

Under the **User Moderation** tab, specify how the posted topics and replies (user generated content) are managed. For more information, see [Moderating User Generated Content](/help/communities/moderate-ugc.md).

* **投稿を拒否**

   このオプションを選択すると、信頼できるメンバーのモデレーターは、投稿を拒否し、投稿が公開フォーラムに表示されないようにします。 初期設定はオフです。

* **トピックを閉じる / 再度開く**

   このオプションを選択すると、信頼できるメンバーのモデレーターがトピックを閉じて、さらに編集やコメントを行ったり、トピックを再度開いたりすることができます。 初期設定はオフです。

* **トピックを移動**

   オンにした場合、投稿側のモデレーターがトピックを移動できるようにします。 初期設定はオンです。

* **投稿にフラグを設定**

   このオプションを選択すると、他のユーザーのトピックやコメントに不適切なフラグを付けることができます。 初期設定はオフです。

* **フラグ設定理由リスト**

   このオプションを選択すると、メンバーは、トピックまたはコメントに不適切なフラグを付ける理由を、ドロップダウンリストから選択できます。 初期設定はオフです。

* **カスタムフラグ設定理由**

   このオプションを選択すると、トピックやコメントに不適切なフラグを付ける理由をメンバーが自分で入力できるようになります。 初期設定はオフです。

* **モデレートのしきい値**

   モデレーターに通知する前に、トピックまたはコメントにメンバーがフラグを付ける必要がある回数を入力します。 初期設定は1（1回）です。

* **フラグ付けの制限**

   トピックまたはコメントが公開表示に表示されなくなる前にフラグを付ける必要がある回数を入力します。 -1に設定すると、フラグ付けされたトピックまたはコメントがパブリック表示に表示されません。 そうでない場合、この数値はモデレートしきい値以上にする必要があります。 初期設定は 5 です。

#### 「タグフィールド」タブ{#tag-field-tab}

「**タグフィールド**」タブでは、「**設定**」タブでタグ付けが許可されている場合に、適用できるタグを名前空間に従って制限します。

* **許可された名前空間**

   「設定」タブで `Allow Tagging` チェックされている場 **合は** 、該当します。 適用できるタグは、チェックされた名前空間内のタグに限定されます。 名前空間のリストには、「標準タグ」(デフォルトの名前空間)と「すべてのタグを含む」が含まれます。 初期設定は「なし」で、すべての名前空間が許可されます。

* **推奨の制限**

   フォーラムへの投稿に対して提案として表示するタグの数を入力します。 初期設定は**-**1 （制限なし）です。

#### 「翻訳」タブ{#translation-tab}

「**翻訳**」タブでは、コミュニティサイトの翻訳が有効になっている場合に、選択された投稿だけでなくトピック全体を翻訳するかどうかを設定できます。

* **すべてを翻訳**

   オンにすると、フォーラムスレッドがユーザーの好みの言語に変換されます。 初期設定はオフです。

#### 「並べ替え設定」タブ{#sort-settings-tab}

Under the **Sort Settings** tab, specify how the posted comments are sorted when displayed.

* **並べ替え**

   許可されている並べ替えの選択をすべてオンにします： `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. デフォルトは `Newest, Oldest, Last Updated` です。

* **デフォルトとして設定**

   プルダウンして、デフォルトとして表示するチェック済みの並べ替えオプションの1つを選択します。 デフォルトは `Newest` です。

* **Analytics 並べ替えのタイムオプションを選択**

   プルダウンして1つを選択しま `All, Last 24 Hours, Last 7 Days, Last 30 Days`す。 デフォルトは `All` です。

### 追加情報 {#additional-information}

詳しくは、開発者向けの[フォーラムの基本事項](/help/communities/essentials-forum.md)ページを参照してください。

投稿されたトピックとコメントのモデレートについては、[ユーザー生成コンテンツのモデレート](/help/communities/moderate-ugc.md)を参照してください。

投稿されたトピックとコメントのタグ付けについては、[ユーザー生成コンテンツのタグ付け](/help/communities/tag-ugc.md)を参照してください。

投稿されたトピックとコメントの翻訳については、[ユーザー生成コンテンツの翻訳](/help/communities/translate-ugc.md)を参照してください。
