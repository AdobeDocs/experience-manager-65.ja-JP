---
title: コミュニティ機能
seo-title: Community Functions
description: コミュニティ機能コンソールへのアクセス方法を説明します。
seo-description: Learn how to access the Community Functions console
uuid: d3d70134-f318-4709-a673-b01a3467d980
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 91833914-b811-4355-a97d-e1a9cb7441f1
docset: aem65
role: Admin
exl-id: 2395c895-c611-43ac-abb6-c2bc4b4a41f4
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2220'
ht-degree: 6%

---

# コミュニティ機能{#community-functions}

コミュニティエクスペリエンスで期待される機能のタイプは、よく知られています。 コミュニティ機能は、コミュニティ機能として使用できます。 基本的に、コミュニティ機能を実装するために事前に配線された 1 つ以上のページです。この場合、オーサリングモードでページにコンポーネントを追加するだけではなく、単にコミュニティ機能を実装する必要があります。 これらは、 [コミュニティサイトテンプレート](/help/communities/sites.md) どのコミュニティサイトから [作成済み](/help/communities/sites-console.md).

コミュニティサイトを作成した後は、標準の [AEMオーサリングモード](/help/sites-authoring/editing-content.md). 様々なコミュニティ機能がコミュニティ機能コンソールに表示されます。

>[!NOTE]
>
>作成用のコンソール [コミュニティサイト](/help/communities/sites-console.md), [コミュニティサイトテンプレート](/help/communities/sites.md), [コミュニティグループテンプレート](/help/communities/tools-groups.md)、および [コミュニティ機能](/help/communities/functions.md) は、オーサー環境でのみ使用されます。

## コミュニティ機能コンソール {#community-functions-console}

オーサー環境でコミュニティ機能コンソールにアクセスするには：

* に移動します。 **[!UICONTROL ツール]** > **[!UICONTROL Communities]** > **[!UICONTROL コミュニティ機能]**.

![community-functions](assets/community-functions.png)

## 事前定義済み関数 {#pre-built-functions}

以下に、AEM Communitiesで提供される機能について簡単に説明します。 各機能には、コミュニティコンポーネントを含む 1 つ以上のAEMページが含まれます。このページは、 [コミュニティサイトテンプレート](/help/communities/sites.md).

コミュニティサイトテンプレートは、ログイン、ユーザープロファイル、通知、メッセージング、サイトメニュー、検索、テーマ設定、ブランディング機能など、コミュニティサイトの構造を提供します。

### タイトルと URL の設定 {#title-and-url-settings}

**タイトル** および **URL** は、すべてのコミュニティ機能に共通のプロパティです。

コミュニティ機能がコミュニティサイトテンプレートに追加されたとき、または追加されたとき [修正中](/help/communities/sites-console.md#modifying-site-properties) コミュニティサイトの構造では、機能のダイアログが開き、タイトルと URL を設定できます。

#### 設定機能の詳細 {#configuration-function-details}

![title-url-details](assets/title-url-details.png)

* **タイトル**

  (*必須*) サイトの機能のメニューに表示されるテキスト

* **URL**

  (*必須*) URI の生成に使用される名前。 名前は [命名規則](/help/sites-developing/naming-conventions.md) AEMと JCR によって課せられます。

例えば、 [はじめに](/help/communities/getting-started.md) チュートリアル、場合は

* タイトル= Web ページ
* URL = page

次に、ページの URL はhttps://localhost:4503/content/sites/engage/en/page.htmlです。

ページのメニューリンクは次のように表示されます。

![engage-page](assets/engage-page.png)

### アクティビティストリーム機能 {#activity-stream-function}

アクティビティストリーム機能は、 [アクティビティストリームコンポーネント](/help/communities/activities.md) すべてのビューを選択した状態（すべてのアクティビティ、ユーザーアクティビティ、フォロー）。 関連トピック [Activity Stream Essentials](/help/communities/essentials-activities.md) 開発者向け。

テンプレートに追加すると、次のダイアログが開きます。

#### 設定機能の詳細 {#configuration-function-details-1}

![function-details](assets/function-details.png)

* [タイトルと URL の設定](#title-and-url-settings)

* **「マイアクティビティ」ビューを表示**

  選択した場合、アクティビティページにタブが表示され、現在のメンバーがコミュニティ内で生成したアクティビティに基づいてアクティビティをフィルタリングできます。 初期設定ではオンになっています。

* **「すべてのアクティビティ」ビューを表示**

  選択した場合、アクティビティページにタブが表示され、現在のメンバーがアクセスできるコミュニティ内で生成されたすべてのアクティビティが含まれます。 初期設定ではオンになっています。

* **「ニュースフィード」ビューを表示**

  選択した場合、アクティビティページには、現在のメンバーがフォローしているアクティビティに基づいてアクティビティをフィルタリングするタブが含まれます。 初期設定ではオンになっています。

### ブログ機能 {#blog-function}

ブログ機能は、 [ブログコンポーネント](/help/communities/blog-feature.md) タグ付け、ファイルのアップロード、フォロー、メンバーが自己編集、投票、モデレートをおこなえるように設定されます。 関連トピック [ブログの基本事項](/help/communities/blog-developer-basics.md) 開発者向け。

テンプレートに追加すると、次のダイアログが開きます。

![blog-component](assets/blog-component.png)

* [タイトルと URL の設定](#title-and-url-settings)

* **権限を持つメンバーを許可**

  選択した場合、ブログでは、権限を持つメンバーのみが記事を作成できます。この場合、記事の選択は許可されます [権限を持つメンバーグループ](/help/communities/users.md#privileged-members-group). 選択しない場合、すべてのコミュニティメンバーが作成できます。 初期設定はオフです。

* **ファイルのアップロードを許可**

  選択した場合、メンバーがファイルをアップロードする機能がブログに含まれます。 初期設定ではオンになっています。

* **スレッド化された返信を許可**

  選択しない場合、ブログは記事に対する返信（コメント）を許可しますが、コメントに対する返信は許可されません。 初期設定ではオンになっています。

* **おすすめコンテンツを許可**

  選択すると、ブログは次のように識別されます。 [おすすめコンテンツ](/help/communities/featured.md). 初期設定ではオンになっています。

### カレンダー機能 {#calendar-function}

カレンダー関数は、 [カレンダーコンポーネント](/help/communities/calendar.md) タグ付けを許可するように設定されています。 関連トピック [カレンダーの基本事項](/help/communities/calendar-basics-for-developers.md) 開発者向け。

テンプレートに追加すると、次のダイアログが開きます。

![calendar-details](assets/calendar-details.png)

* [タイトルと URL の設定](#title-and-url-settings)

* **ピン留めを許可**

  選択した場合、フォーラムでは、トピックの返信をコメントのリストの先頭にピン留めできます。 初期設定ではオンになっています。

* **権限を持つメンバーを許可**

  選択した場合、ブログでは、権限を持つメンバーのみが記事を作成できます。この場合、記事の選択は許可されます [権限を持つメンバーグループ](/help/communities/users.md#privileged-members-group). 選択しない場合、すべてのコミュニティメンバーが作成できます。 初期設定はオフです。

* **ファイルのアップロードを許可**

  選択した場合、メンバーがファイルをアップロードする機能がブログに含まれます。 初期設定ではオンになっています。

* **スレッド化された返信を許可**

  選択しない場合、ブログは記事に対する返信（コメント）を許可しますが、コメントに対する返信は許可されません。 初期設定ではオンになっています。

* **おすすめコンテンツを許可**

  選択すると、そのコンテンツは次のように識別されます。 [おすすめコンテンツ](/help/communities/featured.md). 初期設定ではオンになっています。

### おすすめコンテンツ機能 {#featured-content-function}

おすすめコンテンツ機能は、 [おすすめコンテンツコンポーネント](/help/communities/featured.md) コメントの追加や削除を許可するように設定されました。

コンテンツを特集する機能は、コンポーネントごとに許可または禁止できます ( [ブログ機能](#blog-function), [カレンダー機能](#calendar-function), [フォーラム機能](#forum-function), [アイディエーション関数](#ideation-function)、および [Q&amp;A 機能](#qna-function)) をクリックします。

テンプレートに追加した場合の設定は、 [タイトルと URL の設定](#title-and-url-settings).

### ファイルライブラリ機能 {#file-library-function}

ファイルライブラリ関数は、 [ファイルライブラリコンポーネント](/help/communities/file-library.md) コメントの追加や削除を許可するように設定されました。

テンプレートに追加した場合の設定は、 [タイトルと URL の設定](#title-and-url-settings).

### フォーラム機能 {#forum-function}

フォーラム機能は、 [フォーラムコンポーネント](/help/communities/forum.md) タグ付け、ファイルのアップロード、フォロー、メンバーが自己編集、投票、モデレートをおこなえるように設定されます。

テンプレートに追加すると、次のダイアログが開きます。

#### 設定機能の詳細 {#configuration-function-details-2}

![forum-component1](assets/forum-component1.png)

* [タイトルと URL の設定](#title-and-url-settings)

* **ピン留めを許可**

  選択した場合、フォーラムでは、トピックの返信をコメントのリストの先頭にピン留めできます。 初期設定ではオンになっています。

* **権限を持つメンバーを許可**

  選択すると、権限を持つメンバーのみがトピックを投稿できるようになります。 [権限を持つメンバーグループ](/help/communities/users.md#privileged-members-group). 選択しない場合、すべてのコミュニティメンバーが投稿できます。 初期設定はオフです。

* **ファイルのアップロードを許可**

  選択すると、メンバーがファイルをアップロードする機能もフォーラムに含まれます。 初期設定ではオンになっています。

* **スレッド化された返信を許可**

  選択しない場合、フォーラムはトピックに対するコメントを許可しますが、それらのコメントに対する返信は許可されません。 初期設定ではオンになっています。

* **おすすめコンテンツを許可**

  選択すると、コンポーネントのコンテンツは [おすすめコンテンツ](/help/communities/featured.md). 初期設定ではオンになっています。

### グループ機能 {#groups-function}

>[!CAUTION]
>
>グループ機能は、 *not* は *最初でも唯一でも* 機能をサイトの構造内、またはコミュニティサイトテンプレート内に組み込むことができます。
>
>その他の関数 ( [ページ関数](#page-function)、を含め、最初にリストする必要があります。

グループ機能を使用すると、コミュニティメンバーは、パブリッシュ環境のコミュニティサイト内にサブコミュニティを作成できます。

基準 [設定](/help/communities/sites-console.md#groupmanagement) (Groups 関数が [コミュニティサイトテンプレート](/help/communities/sites.md)の場合、グループはパブリックまたはプライベートに設定でき、1 つ以上のコミュニティグループテンプレートを設定して、コミュニティグループが実際に作成される際に（パブリッシュ環境からなど）テンプレートを選択できます。 A [コミュニティグループテンプレート](/help/communities/tools-groups.md) フォーラムやカレンダーなど、グループページに対して作成するコミュニティ機能を指定します。

コミュニティグループを作成すると、新しいグループに対してメンバーグループが動的に作成され、メンバーの割り当てや参加が可能になります。 詳しくは、 [ユーザーとユーザーグループの管理](/help/communities/users.md).

コミュニティの時点 [機能パック 1](/help/communities/deploy-communities.md#latestfeaturepack)の場合、コミュニティグループは、オーサー環境で [コミュニティサイトのグループコンソール](/help/communities/groups.md)を有効にすると、パブリッシュ環境で作成される場合があります。

テンプレートに追加すると、次のダイアログが開きます。

![group-template-config](assets/group-template-config.png)

* [タイトルと URL の設定](#title-and-url-settings)

* **グループテンプレートを選択**

  （パブリッシュ環境で）新しいコミュニティグループの作成者が将来選択できる、1 つ以上の有効なグループテンプレートを選択できるドロップダウン。

* **権限を持つメンバーを許可**

  選択すると、権限を持つメンバーのみがトピックを投稿できるようになります。 [権限を持つメンバーのセキュリティグループ](/help/communities/users.md#privileged-members-group). 選択しない場合、すべてのコミュニティメンバーが投稿できます。 初期設定はオフです。

* **公開作成を許可**

  選択すると、権限を持つコミュニティメンバーは、パブリッシュ環境でグループを作成できます。 選択を解除すると、新しいグループ（サブコミュニティ）は、コミュニティサイトのグループコンソールからオーサー環境でのみ作成できます。
初期設定ではオンになっています。

### アイディエーション機能 {#ideation-function}

アイディエーション関数は、 [アイディエーションコンポーネント](/help/communities/ideation-feature.md).

テンプレートに追加すると、次のダイアログが開きます。このダイアログでは、テンプレートのデフォルトのタイトルと URL 名と、デフォルトの表示設定を指定しています。

![アイディエーション機能](assets/ideation-function.png)

* [タイトルと URL の設定](#title-and-url-settings)

* **権限を持つメンバーを許可**

  選択すると、権限を持つメンバーのみがトピックを投稿できるようになります。 [権限を持つメンバーのセキュリティグループ](/help/communities/users.md#privileged-members-group). 選択しない場合、すべてのコミュニティメンバーが投稿できます。 初期設定はオフです。

* **ファイルのアップロードを許可**

  選択した場合、メンバーがファイルをアップロードする機能もアイデアに含まれます。 初期設定ではオンになっています。

* **スレッド化された返信を許可**

  選択しない場合、アイデアはトピックに対する返信（コメント）を許可しますが、コメントに対する返信は許可されません。 初期設定ではオンになっています。

* **おすすめコンテンツを許可**

  選択すると、そのコンテンツは次のように識別されます。 [おすすめコンテンツ](/help/communities/featured.md). 初期設定ではオンになっています。

### リーダーボード機能 {#leaderboard-function}

リーダーボード機能は、 [リーダーボードコンポーネント](/help/communities/enabling-leaderboard.md).

**注意**：リーダーボードコンポーネントには、さらに設定が必要です *次より後* コミュニティサイトは、リーダーボード機能を含むコミュニティテンプレートから作成されます。 リーダーボードコンポーネントの [ルール](/help/communities/enabling-leaderboard.md#rules-tab)（の設定に依存） [スコアとバッジ](/help/communities/implementing-scoring.md) コミュニティサイト用。

テンプレートに追加すると、次のダイアログが開きます。このダイアログでは、テンプレートのデフォルトのタイトルと URL 名と、デフォルトの表示設定を指定しています。

![leaderboard-dialog](assets/leaderboard-dialog.png)

* [タイトルと URL の設定](#title-and-url-settings)

* **バッジを表示**

  選択すると、リーダーボードにバッジアイコンの列が表示されます。
初期設定はオフです。

* **バッジ名を表示**

  選択すると、リーダーボードにバッジ名の列が表示されます。
初期設定はオフです。

* **アバターを表示**

  選択した場合、メンバーのアバター画像がリーダーボードに含まれ、メンバーのプロファイルへの名前リンクの横に表示されます。
初期設定はオフです。

### ページ機能 {#page-function}

ページ機能により、コミュニティサイトに空白のページが追加され、ログイン、メニュー、通知、メッセージ、テーマ設定、ブランディングなどのコミュニティサイトの機能に結び付けられます。 コンテンツをページに追加するには、 [標準AEMオーサリングモード](/help/sites-authoring/editing-content.md).

テンプレートに追加した場合の設定は、 [タイトルと URL の設定](#title-and-url-settings).

### Q&amp;A 機能 {#qna-function}

Q&amp;A 機能は、 [Q&amp;A コンポーネント](/help/communities/working-with-qna.md) タグ付け、ファイルのアップロード、フォロー、メンバーが自己編集、投票、モデレートをおこなえるように設定されます。

テンプレートに追加すると、権限を持つメンバーに対する制限が許可されます。

![qna-dialog](assets/qna-dialog.png)

* [タイトルと URL の設定](#title-and-url-settings)

* **ピン留めを許可**

  選択した場合、フォーラムでは、トピックの返信をコメントのリストの先頭にピン留めできます。 初期設定ではオンになっています。

* **権限を持つメンバーを許可**

  選択した場合、Q&amp;A フォーラムでは、権限を持つメンバーに対してのみ質問の投稿を許可し、 [権限を持つメンバーグループ](/help/communities/users.md#privileged-members-group). 選択しない場合、すべてのコミュニティメンバーが投稿できます。 初期設定はオフです。

* **ファイルのアップロードを許可**

  選択した場合、Q&amp;A フォーラムにはメンバーがファイルをアップロードする機能が含まれます。 初期設定ではオンになっています。

* **スレッド化された返信を許可**

  選択しない場合、Q&amp;A フォーラムでは投稿された質問に対するコメント（回答）が許可されますが、回答に対する返信は許可されません。 初期設定ではオンになっています。

* **おすすめコンテンツを許可**

  選択すると、そのコンテンツは次のように識別されます。 [おすすめコンテンツ](/help/communities/featured.md). 初期設定ではオンになっています。

## コミュニティ機能を作成 {#create-community-function}

コミュニティ機能を作成する機能には、 `Create Community Function` コミュニティ機能コンソールの上部にあるアイコン。 同じAEMブループリントに基づく複数の関数を作成し、オーサー編集モードで開いて一意にカスタマイズできます。

![create-community-function](assets/create-community-function.png)

### コミュニティ機能名 {#community-function-name}

![function-name](assets/function-name.png)

コミュニティ機能名パネルで、名前と説明、および機能を有効にするか無効にするかを設定します。

* **コミュニティ機能名**

  表示と保存に使用される関数名。

* **コミュニティ機能の説明**

  表示する関数の説明。

* **無効/有効**

  関数が参照可能かどうかを制御するトグルスイッチ。

### AEM ブループリント {#aem-blueprint}

![aem-blueprint](assets/aem-blueprint.png)

次の日： `AEM Blueprint` パネルの場合は、コミュニティ機能の基盤となるブループリントを選択できます。

コミュニティ機能は、1 つ以上のページを含むミニサイトで、ログイン、ユーザープロファイル、通知、メッセージング、サイトメニュー、検索、テーマ設定、ブランディング機能など、コミュニティサイトに組み込むために事前に設定されています。 関数を作成した後は、次の操作を実行できます。 [関数を開く](#open-community-function) オーサー編集モードで、ページやコンポーネントの設定をカスタマイズします。

コミュニティ機能は [ライブコピー](/help/sites-administering/msm.md#live-copies) の [ブループリント](/help/sites-administering/msm-livecopy.md#creatingablueprint)を使用すると、関数に対して行われた変更をロールアウトできます。この変更は、 [コミュニティサイトテンプレート](/help/communities/sites.md) または [コミュニティグループテンプレート](/help/communities/tools-groups.md) 関数を含む ページを親ブループリントと関連付け解除して、ページレベルで変更することもできます。

関連トピック [マルチサイトマネージャ](/help/sites-administering/msm.md).

### サムネール {#thumbnail}

![funtion-thumbnail](assets/funtion-thumbnail.png)

サムネールパネルでは、画像をアップロードして [コミュニティ機能コンソール](#community-functions-console).

## コミュニティ機能を開く {#open-community-function}

![open-function](assets/open-function.png)

を選択します。 `Open Community Function` ページコンテンツをオーサリングし、機能コンポーネントの設定を変更するためのオーサー編集モードに入るアイコン。

### コンポーネントの設定 {#configuring-components}

コミュニティ機能は、AEMブループリントのライブコピーとして実装されます。詳しくは、以下に記載されています。 [マルチサイトマネージャ](/help/sites-administering/msm.md).

ページコンテンツの作成だけでなく、コンポーネントの設定も可能です。

作成したコミュニティサイトのページでコンポーネントを設定する場合は、キャンセルが必要になる場合があります [継承](/help/sites-administering/msm-livecopy.md#changing-live-copy-content) コンポーネントを設定する場合。 設定が完了したら、継承を再確立する必要があります。

設定の詳細については、 [コミュニティコンポーネント](/help/communities/author-communities.md) 作成者向け

## コミュニティ機能を編集 {#edit-community-function}

![edit-function](assets/edit-function.png)

を選択します。 `Edit Community Function` アイコンをクリックし、 [コミュニティ機能の作成](#create-community-function)（関数の有効/無効を含む）を切り替えます。
