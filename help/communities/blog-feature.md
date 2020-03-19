---
title: ブログ機能
seo-title: ブログ機能
description: ジャーナル形式のコミュニティ情報
seo-description: ジャーナル形式のコミュニティ情報
uuid: 7323063f-81e8-45c3-9035-bf7df6124830
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: cf8b3d72-30ba-40ca-ae48-b61abbb28802
docset: aem65
translation-type: tm+mt
source-git-commit: 272eedc1585dbdea315b49d010e4b1d78cedc360

---


# ブログ機能 {#blog-feature}

## 概要 {#introduction}

AEM Communities のブログ機能は、オーサリングアクティビティから、パブリッシュ環境でおこなわれるコミュニティアクティビティへと変わりました。

ブログ機能は、ジャーナル形式でのコミュニティ情報の提供をサポートします。ブログエントリは、公開環境で、許可されたメンバー（登録されたログインユーザー）によって作成されます。

ブログ機能では以下のことが可能です。

* パブリッシュ側でのブログ記事とコメントの作成
* リッチテキスト編集
* インライン画像（ドラッグアンドドロップのサポートあり）
* 埋め込みソーシャルネットワーキングコンテンツ（[oEmbed のサポート](/help/communities/blog-developer-basics.md#allowing-rich-media)）
* ドラフトモード
* 日時指定公開
* 代理作成（[権限を持つメンバー](/help/communities/users.md#privileged-members-group)が他のコミュニティメンバーの代わりにコンテンツを作成できる）
* ブログ記事やコメントの[コンテキスト内モデレートと一括モデレート](/help/communities/moderate-ugc.md)

ドキュメントのこのセクションでは、以下の内容について説明します。：

* AEMサイトへのブログ機能の追加
* ブログコンポーネントの設定

>[!NOTE]
>
>コンポーネン `Journal`トと `Journal Sidebar` には、およびのタイ `Blog` トルが付きま `Blog Sidebar`す。
>
>AEM 6.0 以前のリリースのブログ機能は、現在は削除されています。テンプレートに基づいており、作成者のみが作成者環境でコンテンツを作成できるようになりました。

## ブログコンポーネントをページに追加 {#adding-blog-components-to-a-page}

作成者モードでページにブログを追加する場合は、コンポーネントブラウザを使用して、

* `Communities / Blog`
* `Communities / Blog Sidebar`

ページ上のブログを表示したい位置にドラッグします。

For necessary information, visit [Communities Components Basics](/help/communities/basics.md).

When the [required client-side libraries](/help/communities/blog-developer-basics.md#essentials-for-client-side) are included, this is how the `Blog`component will appear :

![chlimage_1-229](assets/chlimage_1-229.png)

そして、どのよう `Blog Sidebar` に表示されるか：

![chlimage_1-230](assets/chlimage_1-230.png)

### ブログの設定 {#configuring-blog}

Select the placed `Blog` component to access and select the `Configure` icon which opens the edit dialog.

![chlimage_1-231](assets/chlimage_1-231.png) ![Blog settings](assets/blog-configure.png)

#### 「設定」タブ{#settings-tab}

「**設定**」タブでは、以下に示すブログの基本機能を指定します。

* **添付サムネールを許可**

   オンにすると、添付された画像のサムネールが作成されます。

* **添付サムネールの最大サイズ**

   添付ファイルのサムネール画像の最大サイズ（ピクセル単位）。 デフォルト値は、800 x 800 です。

* **サムネールの最小画像サイズ**

   インライン画像のサムネールを生成するための画像の最小サイズ（バイト）。 デフォルト値は100000バイト(100 KB)です。

* **サムネールの最大サイズ**

   インライン画像のサムネール画像の最大サイズ（ピクセル単位）。 デフォルト値は、800 x 800 です。

* **権限を持つメンバーを許可**

   オンにすると、特権を持つメンバーのみがコンテンツの作成を許可されます。

* **許可された権限を持つメンバー**

   コンテンツの作成を許可する権限を持つメンバーを追加します。

* **作成者編集モードでユーザーが生成したコンテンツをブロックする**

   有効にすると、作成者モードでの編集中にユーザー生成コンテンツがブロックされます。

* **ジャーナルタイトル**

   ページに表示するブログのタイトル。

>[!NOTE]
>
>ジャーナルタイトルは、ブログ用の URL を自動的に作成するために使用されます。
>ここで指定するジャーナルタイトルから、ブログのURLを作成する際に使用される最大50文字（一意性を確保するために5文字を含む）。

* **ジャーナルの説明**

   ブログの説明。

* **1 ページのトピック数**

   1ページに表示するブログエントリ/コメントの数を定義します。 デフォルトは、10 です。

* **モデレート**

   オンにした場合、公開されたサイトに表示されるブログエントリとコメントの投稿は、承認される必要があります。 デフォルトはオフです。

* **閉じる**

   オンにすると、ブログは新しいブログエントリとコメントに閉じられます。 初期設定はオフです。

* **リッチテキストエディター**

   オンにすると、ブログエントリとコメントがマークアップと共に入力される場合があります。 初期設定はオンです。

* **タグ付けを許可**

   If checked, allow members to add tag labels to their post (see **Tag field** tab). 初期設定はオフです。

* **ファイルのアップロードを許可**

   オンにすると、添付ファイルをブログエントリまたはコメントに追加できます。 初期設定はオフです。

* **最大ファイルサイズ**

   がオンの場合のみ `Allow File Uploads` 関連します。 このフィールドは、アップロードされるファイルのサイズ（バイト単位）を制限します。 初期設定は104857600(10 Mb)です。

* **許可されるファイルタイプ**

   がオンの場合のみ `Allow File Uploads` 関連します。 ドット付きのファイル拡張子をコンマ区切りで指定します（例：.jpg, .jpeg, .png, .doc, .docx, .pdf）。ファイルの種類が指定されている場合、指定されていないファイルはアップロードできません。 初期設定は、すべてのファイルタイプが許可されるように指定されない。

* **添付する画像ファイルの最大サイズ**

   「ファイルのアップロードを許可」がオンの場合にのみ関連します。 アップロードされた画像ファイルの最大バイト数。 初期設定は2097152(2 Mb)です。

* **応答を許可**

   オンの場合、ブログエントリに投稿されたコメントへの返信を許可します。 初期設定はオフです。

* **投票を許可**

   オンの場合、ブログエントリに投票機能を含めます。 初期設定はオフです。

* **ユーザーによるコメントおよびトピックの削除を許可**

   オンにすると、投稿したコメントやブログエントリの削除をメンバーに許可します。 初期設定は** **オフです。

* **フォローを許可**

   If checked, include the following feature for blog articles, which allows members to be [notified](/help/communities/notifications.md) of new posts. 初期設定はオフです。

* **電子メール購読を許可**

   If checked, allow members to be notified of new posts by email ([subscription](/help/communities/subscriptions.md)). Requires `Allow Following` to be checked and [email configured](/help/communities/email.md). 初期設定はオフです。

* **バッジを表示**

   If checked, display earned and assigned [badges](/help/communities/implementing-scoring.md) with a member&#39;s blog entry. 初期設定はオフです。

* **リストページで返信を取得しない**

* **おすすめコンテンツを許可**

   If checked, the idea is able to be identified as [featured content](/help/communities/featured.md). 初期設定はオフです。

* **メンションを有効化**

   有効にすると、登録済みコミュニティユーザーは、他の登録済みメンバー（名、姓、ユーザー名を使用）を識別し、共通の@user-name構文を使用してタグ付けできます。 タグ付きユーザーは、メンションに関する通知を受信します。

* **最大メンション数**

   投稿で許可するメンションの最大数を制限します。 初期設定は 10 です。

* **UI メンションパターン**

   投稿内の登録ユーザーにタグ(@mention)を付けるために許可されたパターン文字列を指定します。 例：～{{familyName}}{{givenName}}

#### 「ユーザーモデレート」タブ{#user-moderation-tab}

「**ユーザーモデレート**」タブでは、以下のモデレート設定を指定します。

* **投稿を拒否**

   このオプションを選択すると、信頼できるメンバーのモデレーターは、投稿を拒否し、投稿が公開フォーラムに表示されないようにします。 初期設定はオフです。

* **トピックを閉じる / 再度開く**

   このオプションを選択すると、信頼できるメンバーのモデレーターがトピックを閉じて、さらに編集やコメントを行ったり、トピックを再度開いたりすることができます。 初期設定はオフです。

* **投稿にフラグを設定**

   このオプションを選択すると、他のユーザーのトピックやコメントに不適切なフラグを付けることができます。 初期設定はオフです**。**

* **フラグ設定理由リスト**

   このオプションを選択すると、メンバーは、トピックまたはコメントに不適切なフラグを付ける理由をドロップダウンリストから選択できます。 初期設定はオフです。

* **カスタムフラグ設定理由**

   このオプションを選択すると、トピックやコメントに不適切なフラグを付ける理由をメンバーが自分で入力できるようになります。 初期設定はオフです**。**

* **モデレートのしきい値**

   モデレーターに通知する前に、トピックまたはコメントにメンバーがフラグを付ける必要がある回数を入力します。 初期設定は1（1回）です。

* **フラグ付けの制限**

   トピックまたはコメントが公開ビューに表示されなくなる前にフラグ付けされる必要がある回数を入力します。 -1に設定した場合、フラグ付けされたトピックまたはコメントは公開ビューで非表示になりません。 そうでない場合、この数値はモデレートしきい値以上にする必要があります。 初期設定は 5 です。

#### 「タグフィールド」タブ{#tag-field-tab}

「**タグフィールド**」タブでは、「**設定**」タブで「**タグ付けを許可**」がオンの場合に適用できるタグを指定します。

* **許可された名前空間**

   「**設定**」 `Allow Tagging` タブでチェックされている場合に関連します。 適用できるタグは、チェックされた名前空間カテゴリ内のタグに制限されます。 名前空間のリストには、「Standard Tags」（デフォルトの名前空間）と「Include All Tags」が含まれます。 初期設定はオフで、すべての名前空間が許可されます。

* **推奨の制限**

   フォーラムへの投稿に対して提案として表示するタグの数を入力します。 -1 は無制限を意味します。初期設定は 0 です。

### ブログのサイドバーの設定 {#configuring-blog-sidebar}

When you double-click the `Blog Sidebar` component, an edit dialog opens up.

「**ジャーナルサイドバー設定**」タブでは、アーカイブの日付の形式と、サイドバーに表示するエントリのタイプを指定します。

![blog-component-sidebar](assets/blog-component-sidebar.png)

* **日付の形式**

   ブログエントリのアーカイブに表示する形式。 Java 表記法に従って、プレースホルダーを使用します。

   * yyyy：4 桁の西暦（例：2015）
   * yy：西暦の下 2 桁（例：15）
   * MMMMM：月の正式名（例：June）
   * MMM：月の短縮名（例：Jun）
   * MM：月の数字（例：06）
   初期設定は「yyyy MMMMM」です。これは「2015 June」のように表示されます。

* **表示タイプ**

   サイドバーに表示するブログエントリのタイトルとタイプ。 選択肢は次のとおりです。

   * 作成者
   * カテゴリ
   * アーカイブ

* **ブロッグコンポーネントのパス**

   *（オプション）* 、ブログ記事の一覧表示元のブログリソースの場所。 If left blank, will use the component of resourceType `social/journal/components/hbs/journal` that appears on the same page.

   * 例：`/content/sites/engage/en/blog/jcr:content/content/primary/blog`

* **推奨の制限**

   表示するブログ記事の数。 -1 は無制限を意味します。初期設定は -1 です。

## サイト訪問者のエクスペリエンス {#site-visitor-experience}

パブリッシュ環境では、ブログ記事は作成の降順に表示されます（最新のブログ記事の後に、古いブログ記事が表示されます）。ブログのサイドバーを使用すると、サイトの訪問者はフィルタを適用して、表示するブログ記事の選択を制限できます。

ブログ記事の下には、コメントを投稿または表示するためのリンクが表示されます。

ブログ記事を選択すると、そのブログ記事とコメントが表示されます（有効な場合）。

その他の機能は、サイト訪問者がモデレーターか、管理者か、コミュニティメンバーか、権限を持つメンバーか、匿名かによって異なります。

### 記事の操作 {#working-with-articles}

新しいブログ記事を作成する場合は、次の選択肢があります。

1. 即時公開する
1. ドラフトを公開する
1. 指定された日時に公開する

ブログ記事は、それぞれ適切なタブ（公開済み、ドラフト、スケジュール済み）で、パブリッシュ環境でオーサリングできるメンバー向けに表示されます。

#### モデレーターおよび管理者 {#moderators-and-administrators}

サインインしているユーザーがモデレーター権限または管理者権限を持っている場合、そのユーザーは、すべてのブログ記事およびブログに投稿されたコメントに対して[モデレートタスク](/help/communities/moderate-ugc.md)を実行できます（実行可能な操作はコンポーネントの設定に従います）。

![chlimage_1-232](assets/chlimage_1-232.png)

#### メンバー {#members}

When the signed in user is a community member or [privileged member](/help/communities/users.md#privileged-members-group) (depending on configuration), they are able to select `New Article` to create and post a new blog article.

具体的には、次のことが考えられます。

* 新しいブログ記事の作成
* 別のメンバーに代わって新しいブログ記事を投稿する
* ブログ記事へのコメントの投稿
* 自分のブログ記事またはコメントの編集
* 自分のブログ記事またはコメントを削除する
* 他のユーザーのブログ記事またはコメントにフラグを付ける

![chlimage_1-233](assets/chlimage_1-233.png) ![chlimage_1-234](assets/chlimage_1-234.png)

#### 匿名 {#anonymous}

サインインしていないサイト訪問者は、投稿されたブログ記事やコメントを閲覧することしかできず（サポートされている場合は翻訳も可）、ブログ記事やコメントを追加したり、他人の記事やコメントにフラグを設定することはできません。

![chlimage_1-235](assets/chlimage_1-235.png)

## 追加情報 {#additional-information}

開発者向けの詳細情報は、[ブログの基本事項](/help/communities/blog-developer-basics.md)ページを参照してください。

ブログエントリとコメントのモデレートについては、[ユーザー生成コンテンツのモデレート](/help/communities/moderate-ugc.md)を参照してください。

ブログエントリとコメントのタグ付けについては、[ユーザー生成コンテンツのタグ付け](/help/communities/tag-ugc.md)を参照してください。

ブログエントリとコメントの翻訳については、[ユーザー生成コンテンツの翻訳](/help/communities/translate-ugc.md)を参照してください。
