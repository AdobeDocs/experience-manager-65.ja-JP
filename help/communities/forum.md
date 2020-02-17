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
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# フォーラム機能{#forum-feature}

## 概要 {#introduction}

フォーラム機能は、パブリッシュ環境にサインインしているサイト訪問者（コミュニティメンバー）が以下を実行できる領域を提供します。

* 新しいトピックを作成する
* トピックを表示および返信する
* トピックをフォローする
* フォーラムを検索する
* フォーラムのコンテンツをモデレートできるようにする
* フォーラムのトピックをページ間で移動する

ドキュメントのこのセクションでは、以下の内容について説明します。

* フォーラム機能を AEM サイトに追加
* configuration settings for the `Forum`component

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

「**設定**」タブで、トピックと返信の設定を指定します。

* **添付ファイルのサムネールを許可**オンの場合、添付画像のサムネールが作成されます。
* **添付サムネールの最大サイズ** 添付サムネール画像の最大サイズ（ピクセル単位）です。デフォルト値は、800 x 800 です。

* **サムネールの最小画像サイズ**
* **Max Thumbnail Sizeインラ**&#x200B;イン画像のサムネール画像の最大サイズ（ピクセル単位）。 デフォルト値は、800 x 800 です。

* **ページごとのトピック**各ページに表示するトピック数/投稿数を定義します。 初期設定は 10 です。
* **モデレート**&#x200B;オンにすると、トピックおよびコメントの投稿を公開サイトに表示する前に承認が必要になります。初期設定はオフです。

* **閉じる**&#x200B;オンにすると、フォーラムは新しいトピックやコメントを受け付けなくなります。初期設定はオフです。

* **リッチテキストエディター**&#x200B;オンにすると、マークアップを使用してトピックおよびコメントを入力できます。初期設定はオフです。

* **タグ付けを許可**&#x200B;オンにすると、メンバーは自分の投稿にタグラベルを付加できます（「**タグフィールド**」タブを参照）。初期設定はオフです。

* **ファイルのアップロードを許可**&#x200B;オンにすると、トピックまたはコメントに添付ファイルを付加できます。初期設定はオフです。

* **フォローを許可**&#x200B;オンにすると、フォーラム投稿のフォロー機能が追加され、新しい投稿をメンバーに[通知](/help/communities/notifications.md)できます。初期設定はオフです。

* **ピン留めを許可**&#x200B;オンにすると、フォーラムトピックをトピックリストの上部にピン留めできます。初期設定はオフです。

* **おすすめコンテンツを許可**&#x200B;オンにすると、アイデアを[おすすめコンテンツ](/help/communities/featured.md)として指定できます。初期設定はオフです。

* **電子メール購読を許可**&#x200B;オンにすると、新しい投稿があった場合にメンバーに電子メールで通知できるようになります（[購読](/help/communities/subscriptions.md)）。Requires `Allow Following` to be checked and [email configured](/help/communities/email.md). 初期設定はオフです。

* **「Max File Size** Relevant only if `Allow File Uploads` is」をオンにした場合。 このフィールドは、アップロードするファイルのサイズ（バイト単位）を制限します。 初期設定は104857600(10 Mb)です。

* **「Allowed File Types** Relevant only if `Allow File Uploads` 」がオンの場合。 ドット付きのファイル拡張子をコンマ区切りで指定します（例：.jpg, .jpeg, .png, .doc, .docx, .pdf）。ファイルタイプを指定した場合、指定しなかったファイルはアップロードできません。 初期設定は、** **すべてのファイルタイプを許可するように指定されていない。

* **「ファイルのアップロードを許可」がオン**&#x200B;になっている場合にのみ、「添付画像ファイルの最大サイズ」が関連します。 アップロードされた画像ファイルの最大バイト数。 初期設定は2097152** **(2 Mb)です。

* **スレッド化された返信を許可**&#x200B;オンにすると、トピックに投稿されたコメントへの返信を許可します。初期設定はオフです。

* **投票を許可**&#x200B;オンにすると、トピックに投票機能が組み込まれます。初期設定はオフです。

* **ユーザーによるコメントおよびトピックの削除を許可**&#x200B;オンにすると、メンバーは自分が投稿したコメントおよびトピックを削除できます。初期設定はオフです。

* **パンくずリストを表示**&#x200B;オンにすると、トピックページにナビゲーション用のパンくずリストが表示されます。初期設定はオンです。

* **バッジを表示**&#x200B;オンにすると、獲得した[バッジ](/help/communities/implementing-scoring.md)と割り当てられたバッジがメンバーのブログエントリに表示されます。初期設定はオフです。

* **「Allow Privileged Members**」を選択すると、「Privileged Members」のみがコンテンツの作成を許可されます。

* **許可されている特権メンバー**コンテンツの作成が許可されている特権メンバーを追加します。
* **作成者編集モードでのユーザー生成コンテンツのブロック**&#x200B;有効な場合、作成者モードでの編集中にユーザー生成コンテンツがブロックされます。

* **「メンション**&#x200B;を有効にする」を有効にすると、登録済みコミュニティユーザーは、他の登録済みメンバー（名、姓、ユーザー名を使用）を識別し、共通の@user-name構文を使用してタグ付けできます。 タグ付きユーザーは、メンションに関する通知を受信します。

* **最大メンション**：投稿で許可されるメンションの最大数を制限します。 初期設定は 10 です。

* **UIメンションパターン**：投稿内の登録ユーザーにタグ付け(@mention)するために許可されたパターン文字列を指定します。 For example `~{{familyName}}{{givenName}}`.

>[!NOTE]
>
>トピックに対するコメントを有効にするには、との `AllowThreaded Replies` 両方を `Allow users to Delete Comments and Topics` 確認する必要がある場合があります。

#### 「ユーザーモデレート」タブ{#user-moderation-tab}

「**ユーザーモデレート**」タブで、投稿されたトピックと返信（ユーザー生成コンテンツ）の管理方法を指定します。 For more information, see [Moderating User Generated Content](/help/communities/moderate-ugc.md).

* **投稿を拒否**&#x200B;オンにすると、信頼されているメンバーモデレーターが投稿を拒否して、公開フォーラムへの表示を止めることができます。初期設定はオフです。

* **トピックを閉じる／再度開く**&#x200B;オンにすると、信頼されているメンバーモデレーターが、トピックをそれ以上編集およびコメントできないように閉じたり、再度開いたりすることができます。初期設定はオフです。

* **トピックを移動**&#x200B;オンにすると、公開側のモデレーターはトピックを移動できます。 初期設定はオンです。

* **投稿にフラグを設定**&#x200B;オンにすると、メンバーは他のメンバーのトピックまたはコメントに「不適切」のフラグを設定できます。初期設定はオフです。

* **フラグ設定理由リスト**&#x200B;オンにすると、メンバーはトピックまたはコメントに「不適切」のフラグを設定した理由をドロップダウンリストから選択できます。初期設定はオフです。

* **カスタムフラグ設定理由**&#x200B;オンにすると、メンバーはトピックまたはコメントに「不適切」のフラグを設定した独自の理由を入力できます。初期設定はオフです。

* **モデレートのしきい値**&#x200B;メンバーがトピックまたはコメントに何回フラグを設定したらモデレーターに通知するかを指定します。初期設定は1（1回）です。

* **フラグ付けの制限**&#x200B;トピックまたはコメントに何回フラグが設定されたら、公開表示から非表示にするかを指定します。-1に設定した場合、フラグ付けされたトピックまたはコメントは公開ビューで非表示になりません。 そうでない場合、この数値はモデレートのしきい値以上にする必要があります。 初期設定は 5 です。

#### 「タグフィールド」タブ{#tag-field-tab}

Under the **Tag field** tab, the tags which may be applied, if allowed under the **Settings **tab, are limited according to namespaces chosen.

* ****Settings ****&#x200B;タブでチェ `Allow Tagging` ック済みの場合は、「Namespaces Relevant」を使用できます。 適用できるタグは、チェックされた名前空間カテゴリ内のタグに制限されます。 名前空間のリストには、「Standard Tags」（デフォルトの名前空間）と「Include All Tags」が含まれます。 初期設定はnoneで、すべての名前空間が許可されます。

* **推奨の制限**&#x200B;フォーラムに投稿するメンバーに表示する推奨タグの数を入力します。初期設定は**-**1（制限なし）です。

#### 「翻訳」タブ{#translation-tab}

「**Translation **」タブで、コミュニティサイトの翻訳が有効な場合、トピック全体または選択した投稿を翻訳するように翻訳を設定できます。

* **すべてを翻訳**&#x200B;オンにすると、フォーラムスレッドはユーザーの選択した言語に翻訳されます。初期設定はオフです。

#### 「並べ替え設定」タブ{#sort-settings-tab}

「**並べ替え設定**」タブで、投稿されたコメントの表示順を指定します。

* **Sort By** Check all allowed sort selections : `Newest, Oldest, Last Updated, Most Viewed, Most Active, Most Followed and Most Liked`. デフォルトは `Newest, Oldest, Last Updated` です。

* **デフォルトとして設定**&#x200B;プルダウンして、オンになっている並べ替えオプションのいずれかを選択し、デフォルトとして表示されるようにします。デフォルトは `Newest` です。

* **「Analyticsの並べ替えの時間オプション」のプ**&#x200B;ルダウンを選択して、いずれかを選択しま `All, Last 24 Hours, Last 7 Days, Last 30 Days`す。 デフォルトは `All` です。

### 追加情報 {#additional-information}

詳しくは、開発者向けの[フォーラムの基本事項](/help/communities/essentials-forum.md)ページを参照してください。

投稿されたトピックとコメントのモデレートについては、[ユーザー生成コンテンツのモデレート](/help/communities/moderate-ugc.md)を参照してください。

投稿されたトピックとコメントのタグ付けについては、[ユーザー生成コンテンツのタグ付け](/help/communities/tag-ugc.md)を参照してください。

投稿されたトピックとコメントの翻訳については、[ユーザー生成コンテンツの翻訳](/help/communities/translate-ugc.md)を参照してください。
