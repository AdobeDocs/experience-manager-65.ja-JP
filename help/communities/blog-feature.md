---
title: ブログ機能
description: ブログ機能がジャーナル形式のコミュニティ情報の提供をどのようにサポートするかについて説明します。 エントリは、権限のあるユーザーによってPublish環境で作成されます。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 4650ac36-5506-4efc-be35-fac9e5a58f3d
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1696'
ht-degree: 1%

---

# ブログ機能 {#blog-feature}

## はじめに {#introduction}

AEM Communitiesのブログ機能は、オーサリングアクティビティから、Publish環境で行われる真のコミュニティアクティビティに変わりました。

ブログ機能は、ジャーナル形式でコミュニティ情報を提供することをサポートしています。 ブログエントリは、許可されたメンバー（登録され、ログインしたユーザー）がPublish環境で作成します。

のブログ機能には、次のものが用意されています。

* Publish側でのブログ記事およびコメントの作成
* リッチテキスト編集
* インライン画像（ドラッグ&amp;ドロップをサポート）
* 埋め込みソーシャルネットワーキングコンテンツ（[oEmbed サポート ](/help/communities/blog-developer-basics.md#allowing-rich-media)）
* ドラフトモード
* スケジュールされた公開
* 代理人として作成（[ 特権メンバー ](/help/communities/users.md#privileged-members-group) は、別のコミュニティメンバーに代わってコンテンツを作成できます）
* ブログ記事およびコメントの [ コンテキスト内および一括モデレート ](/help/communities/moderate-ugc.md)

ドキュメントのこの節では、以下について説明します。

* AEM サイトへのブログ機能の追加
* ブログコンポーネントの設定

>[!NOTE]
>
>コンポーネント `Journal` および `Journal Sidebar` のタイトルは、`Blog` および `Blog Sidebar` です。
>
>AEM 6.0 以前のリリースにあるブログ機能は削除されました。 テンプレートをベースにしており、オーサー環境でコンテンツを作成できるのは作成者のみでした。

## ページへのブログコンポーネントの追加 {#adding-blog-components-to-a-page}

オーサーモードでブログをページに追加する場合は、コンポーネントブラウザーを使用して以下を見つけます

* `Communities / Blog`
* `Communities / Blog Sidebar`

そして、ブログが表示されるページの場所にドラッグします。

必要な情報については、[Communities コンポーネントの基本 ](/help/communities/basics.md) を参照してください。

[ 必須のクライアントサイドライブラリ ](/help/communities/blog-developer-basics.md#essentials-for-client-side) が含まれている場合、`Blog` のコンポーネントが表示されます。

![add-blog-component](assets/add-blog-component.png)

### ブログの設定 {#configuring-blog}

配置された `Blog` コンポーネントを選択して、編集ダイアログボックスを開く `Configure` アイコンにアクセスして選択できるようにします。

![ 設定 ](assets/configure-new.png)

![ ブログ設定 ](assets/blog-configure.png)

#### 「設定」タブ {#settings-tab}

「**設定**」タブで、ブログの基本機能を指定します。

* **添付ファイルのサムネールを許可**

  オンにすると、添付された画像のサムネールが作成されます。

* **添付サムネールの最大サイズ**

  添付ファイルのサムネール画像の最大サイズ （ピクセル単位）。 デフォルト値は 800 x 800 です。

* **サムネールの最小イメージサイズ**

  インライン画像のサムネールを生成するための画像の最小サイズ（バイト単位）。 デフォルト値は 100000 バイト（100 kb）です。

* **最大サムネールサイズ**

  インライン画像のサムネール画像の最大サイズ（ピクセル単位）。 デフォルト値は 800 x 800 です。

* **権限のあるメンバーを許可**

  オンにすると、権限を持つメンバーのみがコンテンツを作成できます。

* **許可された特権メンバー**

  コンテンツの作成を許可する権限のあるメンバーを追加します。

* **オーサー編集モードでのユーザー生成コンテンツのブロック**

  これを有効にすると、オーサーモードでの編集中に、ユーザーが生成したコンテンツがブロックされます。

* **ジャーナルのタイトル**

  ページに表示するブログタイトル。

>[!NOTE]
>
>ジャーナルタイトルは、ブログの URL を自動的に作成するために使用されます。
>
>ここで指定したジャーナル タイトルから最大 50 文字（一意性を追加する 5 文字）が使用され、ブログの URL が作成されます。

* **ジャーナルの説明**

  ブログの説明。

* **1 ページあたりのトピック数**

  ページごとに表示されるブログエントリ/コメントの数を定義します。 デフォルトは 10 です。

* **モデレート**

  オンにした場合、ブログのエントリとコメントが公開サイトに表示される前に投稿を承認する必要があります。 デフォルトではオフになっています。

* **終了**

  オンにすると、新しいブログエントリとコメントに対してブログがクローズされます。 デフォルトではオフになっています。

* **リッチテキストエディター**

  オンにすると、ブログのエントリとコメントがマークアップ付きで入力される場合があります。 デフォルトではオンになっています。

* **タグ付けを許可**

  オンにした場合、メンバーが投稿にタグラベルを追加できるようになります（「**タグフィールド** タブを参照）。 デフォルトではオフになっています。

* **ファイルのアップロードを許可**

  オンにすると、ブログエントリまたはコメントに添付ファイルを追加できるようになります。 デフォルトではオフになっています。

* **最大ファイルサイズ**

  「`Allow File Uploads`」がオンの場合にのみ関連します。 このフィールドでは、アップロードするファイルのサイズ（バイト単位）を制限します。 デフォルトは 104857600 （10 Mb）です。

* **許可されるファイルタイプ**

  「`Allow File Uploads`」がオンの場合にのみ関連します。 「ドット」区切り文字を使用したファイル拡張子のコンマ区切りリスト。 例：.jpg、.jpeg、.png、.doc、.docx、.pdf いずれかのファイルタイプを指定した場合、指定されていないファイルタイプはアップロードできません。 デフォルトは、すべてのファイルタイプが許可されるように、何も指定されていません。

* **アタッチ イメージ ファイルの最大サイズ**

  「ファイルのアップロードを許可」がオンの場合にのみ関連します。 アップロードされた画像ファイルの最大バイト数。 デフォルトは 2097152 （2 Mb）です。

* **返信を許可**

  オンにした場合、ブログエントリに投稿されたコメントへの返信を許可します。 デフォルトではオフになっています。

* **投票の許可**

  オンにした場合は、投票機能をブログエントリと共に追加します。 デフォルトではオフになっています。

* **ユーザーがコメントおよびトピックを削除できるようにする**

  オンにした場合、メンバーが投稿したコメントおよびブログエントリを削除できます。 デフォルトではオフになっています。

* **次の操作を許可**

  オンにした場合、メンバーが新しい投稿を [ 通知 ](/help/communities/notifications.md) できるようにするブログ記事の次の機能を含めます。 デフォルトではオフになっています。

* **メール購読の許可**

  オンにすると、メンバーが新しい投稿をメールで通知できるようになります（[ 購読 ](/help/communities/subscriptions.md)）。 `Allow Following` を確認し、[ メールを設定済み ](/help/communities/email.md) にする必要があります。 デフォルトではオフになっています。

* **バッジを表示**

  オンにすると、獲得および割り当てられた [ バッジ ](/help/communities/implementing-scoring.md) がメンバーのブログエントリと共に表示されます。 デフォルトではオフになっています。

* **リストページで返信を受け取らない**

* **おすすめコンテンツを許可**

  オンにした場合、アイデアは [ おすすめコンテンツ ](/help/communities/featured.md) と識別されます。 デフォルトではオフになっています。

* **メンションの有効化**

  これを有効にすると、登録済みのコミュニティユーザーは、他の登録済みメンバー（名、姓、ユーザー名を使用）を識別し、共通の@user-name 構文を使用してタグ付けできるようになります。 タグ付けされたユーザーは、自分のメンションに関する通知を受け取ります。

* **最大メンション数**

  投稿で許可されるメンションの最大数を制限します。 初期設定は 10 です。

* **UI 注釈パターン**

  POST で登録ユーザーにタグ付け（@mention）するための、許可されているパターン文字列を指定します。 例えば、`~{{familyName}}{{givenName}}` のように指定します。

#### ユーザーモデレートタブ {#user-moderation-tab}

**ユーザーモデレート** タブで、「モデレート設定」を指定します。

* **投稿を拒否**

  オンにすると、信頼されたメンバーモデレーターは投稿を拒否し、その投稿が公開フォーラムに表示されるのを防ぐことができます。 デフォルトではオフになっています。

* **トピックを閉じる/再度開く**

  オンにすると、信頼されたメンバーモデレーターがトピックを閉じて編集やコメントを追加したり、トピックを再度開いたりすることがあります。 デフォルトではオフになっています。

* **旗の掲示**

  オンにした場合、他のメンバーが不適切なトピックやコメントを含むフラグを立てることができます。 デフォルトではオフになっています。

* **フラグ理由リスト**

  オンにすると、メンバーは、トピックまたはコメントに不適切なフラグを設定した理由をドロップダウンリストから選択できます。 デフォルトではオフになっています。

* **カスタムフラグの理由**

  オンにした場合、トピックまたはコメントに不適切なフラグを設定する独自の理由をメンバーが入力できるようにします。 デフォルトではオフになっています。

* **モデレートしきい値**

  モデレータに通知を送信する前に、トピックまたはコメントがメンバによってフラグ付けされる回数を入力します。 デフォルトは 1 （1 回）です。

* **フラグの上限**

  トピックまたはコメントをパブリック ビューで非表示にする前に、そのトピックまたはコメントにフラグを付ける回数を入力します。 -1 に設定すると、フラグが設定されたトピックまたはコメントがパブリック ビューから隠されることはありません。 それ以外の場合は、この数はモデレートしきい値以上にする必要があります。 デフォルトは 5 です。

#### 「タグフィールド」タブ {#tag-field-tab}

「**タグフィールド**」タブで、「**設定**」タブの **タグ付けを許可** がオンの場合に適用できるタグを指定します。

* **許可された名前空間**

  **設定** タブで「`Allow Tagging`」がオンの場合に関連します。 適用できるタグは、オンになっている名前空間カテゴリ内のタグに制限されます。 名前空間のリストには、「標準タグ」（デフォルトの名前空間）と「すべてのタグを含める」が含まれています。 デフォルトでは、チェックされていないが、すべての名前空間が許可されていることを意味します。

* **提案の制限**

  フォーラムに投稿するメンバーに提案として表示するタグの数を入力します。 値が–1 の場合は、制限なしという意味です。 初期設定は 0 です。

### ブログサイドバーの設定 {#configuring-blog-sidebar}

`Blog Sidebar` コンポーネントをダブルクリックすると、編集ダイアログが開きます。

「**Journal サイドバー設定**」タブで、アーカイブの日付形式と、サイドバーに表示するエントリのタイプを指定します。

![blog-component-sidebar](assets/blog-component-sidebar.png)

* **日付形式**

  ブログエントリのアーカイブに表示するために使用する形式。 この形式では、Java™ 規則に従ったプレースホルダーを使用します。

   * yyyy :2015 年のように通年
   * yy：短い年（「15」など）
   * MMMMM :1 か月（6 月など）
   * MMM：月が短い（6 月など）
   * MM：月の数値（06 など）

  デフォルトは「yyyy MMMMM」です。これは「2015 June」などのように表示されます

* **ビュータイプ**

  サイドバーに表示するブログエントリのタイトルとタイプ。 次の中から選択します

   * 作成者
   * カテゴリ
   * アーカイブ

* **ブログコンポーネントのパス**

  *（任意）* ブログ記事を一覧表示するブログリソースの場所。 空白の場合は、同じページに表示される resourceType `social/journal/components/hbs/journal` のコンポーネントが使用されます。

   * 例えば、`/content/sites/engage/en/blog/jcr:content/content/primary/blog` のように指定します。

* **提案の制限**

  表示されるブログ記事の数です。 値が–1 の場合は、制限なしという意味です。 初期設定は -1 です。

## サイト訪問者エクスペリエンス {#site-visitor-experience}

パブリッシュ環境では、ブログ機能によって最新のブログ記事が表示され、その後に古いブログ記事が作成順に表示されます。 ブログサイドバーを使用すると、サイト訪問者はフィルターを適用して、表示するブログ記事の選択を制限できます。

ブログ記事の後に、コメントを投稿または表示するためのリンクが表示されます。

ブログ記事を選択すると、ブログ記事とコメントが表示されます（有効な場合）。

その他の権限は、サイト訪問者がモデレーター、管理者、コミュニティメンバー、権限のあるメンバー、匿名のどれであるかによって異なります。

### 記事の操作 {#working-with-articles}

ブログ記事を作成する場合は、次の方法を選択します。

1. 直ちにPublish
1. ドラフトのPublish
1. スケジュールされた日時にPublishする

ブログ記事は、適切なタブ（公開済み、ドラフト、またはスケジュール済み）の下に表示され、公開時に作成できるメンバーに表示されます。

#### モデレーターと管理者 {#moderators-and-administrators}

サインインしたユーザーがモデレーターまたは管理者権限を持っている場合、ブログに投稿されたすべてのブログ記事とコメントで（コンポーネントの設定で許可された） [ モデレートタスク ](/help/communities/moderate-ugc.md) を実行できます。

![moderator-homepage](assets/moderator-homepage.png)

#### メンバー {#members}

ログインしたユーザーがコミュニティメンバーまたは [ 権限のあるメンバー ](/help/communities/users.md#privileged-members-group) （設定に応じて異なる）の場合、ユーザーは `New Article` を選択して新しいブログ記事を作成および投稿できます。

具体的には、次のような場合があります。

* ブログ記事の作成
* 他のメンバーの代わりに新しいブログ記事をPost
* ブログ記事へのコメントのPost
* 自分のブログ記事またはコメントを編集する
* 自分のブログ記事またはコメントを削除する
* 他のユーザーのブログ記事またはコメントにフラグを付ける

![member-homepage](assets/member-homepage.png)

![create-blog](assets/create-blog.png)

#### 匿名 {#anonymous}

ログインしていないサイト訪問者は、投稿されたブログ記事やコメントを読んだり、サポートされている場合はそれらを翻訳したりすることはできますが、ブログ記事やコメントを追加したり、他のユーザーの記事やコメントにフラグを立てたりすることはできません。

![anonymous-user-view](assets/anonymous-user-view.png)

## 追加情報 {#additional-information}

詳しくは、開発者向けの [ ブログの初期設定 ](/help/communities/blog-developer-basics.md) ページを参照してください。

ブログエントリとコメントのモデレートについては、「[ ユーザー作成コンテンツのモデレート ](/help/communities/moderate-ugc.md)」を参照してください。

ブログエントリとコメントのタグ付けについては、[ ユーザー生成コンテンツのタグ付け ](/help/communities/tag-ugc.md) を参照してください。

ブログエントリとコメントの翻訳については、[ ユーザー生成コンテンツの翻訳 ](/help/communities/translate-ugc.md) を参照してください。
