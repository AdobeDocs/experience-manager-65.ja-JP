---
title: コミュニティ機能
description: コミュニティ関数コンソールにアクセスする方法を学ぶ
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 2395c895-c611-43ac-abb6-c2bc4b4a41f4
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '2215'
ht-degree: 2%

---

# コミュニティ機能{#community-functions}

コミュニティエクスペリエンスから期待される機能の種類はよく知られています。 コミュニティ機能は、コミュニティ機能として使用できます。 基本的に、オーサーモードでページにコンポーネントを追加するだけで済むコミュニティ機能を実装するように事前に配線された 1 つ以上のページです。 これらは、[&#x200B; コミュニティサイトテンプレート &#x200B;](/help/communities/sites.md) の構造を定義するために使用される構築ブロックで、ここからコミュニティサイトが [&#x200B; 作成 &#x200B;](/help/communities/sites-console.md) されます。

コミュニティサイトを作成したら、標準の [AEM オーサリングモード &#x200B;](/help/sites-authoring/editing-content.md) を使用して、結果ページにコンテンツを追加できます。 コミュニティ機能コンソールに表示されるように、様々なコミュニティ機能を使用できます。

>[!NOTE]
>
>[&#x200B; コミュニティサイト &#x200B;](/help/communities/sites-console.md)、[&#x200B; コミュニティサイトテンプレート &#x200B;](/help/communities/sites.md)、[&#x200B; コミュニティグループテンプレート &#x200B;](/help/communities/tools-groups.md)、および [&#x200B; コミュニティ機能 &#x200B;](/help/communities/functions.md) の作成用のコンソールは、オーサー環境でのみ使用されます。

## コミュニティ機能コンソール {#community-functions-console}

オーサー環境でコミュニティ機能コンソールにアクセスするには：

* **[!UICONTROL ツール]**/**[!UICONTROL コミュニティ]**/**[!UICONTROL コミュニティ機能]** に移動します。

![&#x200B; コミュニティ関数 &#x200B;](assets/community-functions.png)

## 事前定義済み関数 {#pre-built-functions}

次に、AEM Communitiesで提供される機能について簡単に説明します。 各機能には、1 つ以上のAEM ページが含まれています。このページには、コミュニティコンポーネントがワイヤリングされ、[&#x200B; コミュニティサイトテンプレート &#x200B;](/help/communities/sites.md) に簡単に組み込むことができる機能が含まれています。

コミュニティサイトテンプレートは、ログイン、ユーザープロファイル、通知、メッセージング、サイトメニュー、検索、テーマ設定、ブランディング機能などの、コミュニティサイトの構造を提供します。

### タイトルと URL の設定 {#title-and-url-settings}

**タイトル** と **URL** は、すべてのコミュニティ機能に共通のプロパティです。

コミュニティ機能をコミュニティサイトテンプレートに追加したり、コミュニティサイトの構造を [&#x200B; 変更 &#x200B;](/help/communities/sites-console.md#modifying-site-properties) するときに追加すると、機能のダイアログが開き、タイトルと URL を設定できます。

#### 設定機能の詳細 {#configuration-function-details}

![title-url-details](assets/title-url-details.png)

* **タイトル**

  （*必須*）サイトの機能のメニューに表示されるテキスト

* **URL**

  （*必須*） URI の生成に使用する名前。 名前は、AEMおよび JCR によって課された [&#x200B; 命名規則 &#x200B;](/help/sites-developing/naming-conventions.md) に従う必要があります。

例えば、次の場合に、[&#x200B; はじめに &#x200B;](/help/communities/getting-started.md) チュートリアルに従って作成したサイトを使用します

* タイトル = Web ページ
* URL = ページ

次に、ページの URL はhttps://localhost:4503/content/sites/engage/en/page.htmlです。

ページのメニューリンクは次のように表示されます。

![engage-page](assets/engage-page.png)

### アクティビティストリーム機能 {#activity-stream-function}

アクティビティストリーム関数は、[&#x200B; アクティビティストリーム コンポーネント &#x200B;](/help/communities/activities.md) を含むページで、すべての表示（すべてのアクティビティ、ユーザーアクティビティ、以下）が選択されています。 開発者向けの [&#x200B; アクティビティストリームの初期設定 &#x200B;](/help/communities/essentials-activities.md) も参照してください。

テンプレートに追加すると、次のダイアログが開きます。

#### 設定機能の詳細 {#configuration-function-details-1}

![function-details](assets/function-details.png)

* [タイトルと URL の設定](#title-and-url-settings)

* **「マイアクティビティ」ビューを表示**

  選択すると、アクティビティ ページにはタブが含まれ、現在のメンバーによってコミュニティ内で生成されたアクティビティに基づいてアクティビティがフィルタリングされます。 デフォルトが選択されています。

* **「すべてのアクティビティ」ビューを表示**

  選択すると、アクティビティ ページにはタブが含まれます。このタブには、現在のメンバーがアクセス権を持つ、コミュニティ内で生成されたすべてのアクティビティが含まれます。 デフォルトが選択されています。

* **「ニュースフィード」ビューを表示**

  選択すると、アクティビティ ページには、現在のメンバーがフォローしているものに基づいてアクティビティをフィルタリングするタブが含まれます。 デフォルトが選択されています。

### ブログ機能 {#blog-function}

ブログ機能は、タグ付け、ファイルのアップロード、フォロー、メンバーの自己編集、投票、モデレート用に設定された [&#x200B; ブログコンポーネント &#x200B;](/help/communities/blog-feature.md) を含むページです。 開発者向けの [&#x200B; ブログの基本事項 &#x200B;](/help/communities/blog-developer-basics.md) も参照してください。

テンプレートに追加すると、次のダイアログが開きます。

![blog-component](assets/blog-component.png)

* [タイトルと URL の設定](#title-and-url-settings)

* **権限のあるメンバーを許可**

  選択した場合、ブログでは、[&#x200B; 権限のあるメンバーグループ &#x200B;](/help/communities/users.md#privileged-members-group) の選択を許可することにより、権限のあるメンバーのみが記事を作成できます。 選択しない場合、すべてのコミュニティメンバーが作成できます。 デフォルトでは選択されていません。

* **ファイルのアップロードを許可**

  選択した場合、ブログにはメンバーがファイルをアップロードする機能が含まれます。 デフォルトが選択されています。

* **スレッド返信を許可**

  選択しない場合、ブログでは記事への返信（コメント）が許可されますが、コメントへの返信は許可されません。 デフォルトが選択されています。

* **おすすめコンテンツを許可**

  選択すると、ブログが [&#x200B; 注目のコンテンツ &#x200B;](/help/communities/featured.md) として識別されます。 デフォルトが選択されています。

### カレンダー機能 {#calendar-function}

カレンダー関数は、タグ付けを許可するように設定された [&#x200B; カレンダーコンポーネント &#x200B;](/help/communities/calendar.md) を含むページです。 開発者向けの [&#x200B; カレンダーの基本事項 &#x200B;](/help/communities/calendar-basics-for-developers.md) も参照してください。

テンプレートに追加すると、次のダイアログが開きます。

![calendar-details](assets/calendar-details.png)

* [タイトルと URL の設定](#title-and-url-settings)

* **ピン留めを許可**

  選択した場合、フォーラムでは、トピックへの返信をコメントのリストの先頭にピン留めできます。 デフォルトが選択されています。

* **権限のあるメンバーを許可**

  選択した場合、ブログでは、[&#x200B; 権限のあるメンバーグループ &#x200B;](/help/communities/users.md#privileged-members-group) の選択を許可することにより、権限のあるメンバーのみが記事を作成できます。 選択しない場合、すべてのコミュニティメンバーが作成できます。 デフォルトでは選択されていません。

* **ファイルのアップロードを許可**

  選択した場合、ブログにはメンバーがファイルをアップロードする機能が含まれます。 デフォルトが選択されています。

* **スレッド返信を許可**

  選択しない場合、ブログでは記事への返信（コメント）が許可されますが、コメントへの返信は許可されません。 デフォルトが選択されています。

* **おすすめコンテンツを許可**

  選択した場合、そのコンテンツは [&#x200B; おすすめコンテンツ &#x200B;](/help/communities/featured.md) と識別されます。 デフォルトが選択されています。

### おすすめコンテンツ機能 {#featured-content-function}

おすすめコンテンツ機能は、コメントを追加および削除できるように設定された [&#x200B; おすすめコンテンツ コンポーネント &#x200B;](/help/communities/featured.md) を含むページです。

コンテンツを機能させる機能は、コンポーネントごとに許可または禁止できます（[&#x200B; ブログ関数 &#x200B;](#blog-function)、[&#x200B; カレンダー関数 &#x200B;](#calendar-function)、[&#x200B; フォーラム関数 &#x200B;](#forum-function)、[&#x200B; アイディエーション関数 &#x200B;](#ideation-function)、[QnA 関数 &#x200B;](#qna-function) を参照）。

テンプレートに追加した場合、唯一の設定は [&#x200B; タイトルと URL の設定 &#x200B;](#title-and-url-settings) です。

### ファイルライブラリ機能 {#file-library-function}

ファイルライブラリ機能は、コメントを追加および削除できるように設定された [&#x200B; ファイルライブラリコンポーネント &#x200B;](/help/communities/file-library.md) を含むページです。

テンプレートに追加した場合、唯一の設定は [&#x200B; タイトルと URL の設定 &#x200B;](#title-and-url-settings) です。

### フォーラム機能 {#forum-function}

フォーラム機能は、タグ付け、ファイルのアップロード、フォロー、メンバーの自己編集、投票、モデレート用に設定された [&#x200B; フォーラムコンポーネント &#x200B;](/help/communities/forum.md) を含むページです。

テンプレートに追加すると、次のダイアログが開きます。

#### 設定機能の詳細 {#configuration-function-details-2}

![forum-component1](assets/forum-component1.png)

* [タイトルと URL の設定](#title-and-url-settings)

* **ピン留めを許可**

  選択した場合、フォーラムでは、トピックへの返信をコメントのリストの先頭にピン留めできます。 デフォルトが選択されています。

* **権限のあるメンバーを許可**

  選択した場合、フォーラムでは、[&#x200B; 権限を持つメンバーグループ &#x200B;](/help/communities/users.md#privileged-members-group) の選択を許可することにより、権限を持つメンバーのみがトピックを投稿できます。 選択しない場合、すべてのコミュニティメンバーが投稿できます。 デフォルトでは選択されていません。

* **ファイルのアップロードを許可**

  選択した場合、フォーラムにはメンバーがファイルをアップロードする機能が含まれます。 デフォルトが選択されています。

* **スレッド返信を許可**

  選択しない場合、フォーラムではトピックに関するコメントが許可されますが、それらのコメントに対する返信は許可されません。 デフォルトが選択されています。

* **おすすめコンテンツを許可**

  選択した場合、コンポーネントのコンテンツは [&#x200B; おすすめコンテンツ &#x200B;](/help/communities/featured.md) と識別されます。 デフォルトが選択されています。

### Groups 関数 {#groups-function}

>[!CAUTION]
>
>サイトの構造またはコミュニティサイトテンプレートでは、groups 関数を *最初でも唯一でも* 機能にする *必要はありません*。
>
>[page 関数 &#x200B;](#page-function) など、その他の関数を最初に含めてリストする必要があります。

グループ機能は、コミュニティメンバーがパブリッシュ環境のコミュニティサイト内にサブコミュニティを作成する機能を提供します。

[&#x200B; 設定 &#x200B;](/help/communities/sites-console.md#groupmanagement) に応じて、グループ機能が [&#x200B; コミュニティサイトテンプレート &#x200B;](/help/communities/sites.md) に含まれている場合、グループはパブリックまたはプライベートにすることができます。また、1 つ以上のコミュニティグループテンプレートを設定して、コミュニティグループが実際に作成されるときにテンプレートを選択できます（パブリッシュ環境など）。 [&#x200B; コミュニティグループテンプレート &#x200B;](/help/communities/tools-groups.md) は、フォーラムやカレンダーなど、グループページ用に作成するコミュニティ機能を指定します。

コミュニティグループを作成すると、新しいグループ用にメンバーグループが動的に作成され、メンバーを割り当てたり、結合したりできます。 詳しくは、[&#x200B; ユーザーとユーザーグループの管理 &#x200B;](/help/communities/users.md) を参照してください。

Communities [&#x200B; 機能パック 1](/help/communities/deploy-communities.md#latestfeaturepack) の場合、コミュニティグループは、[Communities サイトのグループコンソール &#x200B;](/help/communities/groups.md) を使用してオーサー環境で作成されますが、有効な場合はパブリッシュ環境で作成できます。

テンプレートに追加すると、次のダイアログが開きます。

![group-template-config](assets/group-template-config.png)

* [タイトルと URL の設定](#title-and-url-settings)

* **グループテンプレートの選択**

  1 つ以上の有効なグループテンプレートを選択できるドロップダウン。今後（パブリッシュ環境で）新しいコミュニティグループを作成する際に、このドロップダウンから選択できます。

* **権限のあるメンバーを許可**

  選択した場合、フォーラムでは、[&#x200B; 特権メンバーのセキュリティ グループ &#x200B;](/help/communities/users.md#privileged-members-group) の選択を許可することにより、特権メンバーのみがトピックを投稿できます。 選択しない場合、すべてのコミュニティメンバーが投稿できます。 デフォルトでは選択されていません。

* **Publishの作成を許可**

  これを選択すると、承認済みのコミュニティメンバーは、パブリッシュ環境でグループを作成できます。 選択を解除すると、新しいグループ（サブコミュニティ）は、オーサー環境でコミュニティサイトのグループコンソールからのみ作成できます。
デフォルトが選択されています。

### アイディエーション機能 {#ideation-function}

アイディエーション関数は、1 つの [&#x200B; アイディエーションコンポーネント &#x200B;](/help/communities/ideation-feature.md) を持つページです。

テンプレートに追加すると、次のダイアログが開き、デフォルトのタイトルと URL 名、およびテンプレートのデフォルトの表示設定を指定します。

![ideation-function](assets/ideation-function.png)

* [タイトルと URL の設定](#title-and-url-settings)

* **権限のあるメンバーを許可**

  選択した場合、フォーラムでは、[&#x200B; 特権メンバーのセキュリティ グループ &#x200B;](/help/communities/users.md#privileged-members-group) の選択を許可することにより、特権メンバーのみがトピックを投稿できます。 選択しない場合、すべてのコミュニティメンバーが投稿できます。 デフォルトでは選択されていません。

* **ファイルのアップロードを許可**

  選択した場合、アイデアにはメンバーがファイルをアップロードする機能が含まれます。 デフォルトが選択されています。

* **スレッド返信を許可**

  選択しない場合、トピックへの返信（コメント）は許可されますが、コメントへの返信は許可されません。 デフォルトが選択されています。

* **おすすめコンテンツを許可**

  選択した場合、そのコンテンツは [&#x200B; おすすめコンテンツ &#x200B;](/help/communities/featured.md) と識別されます。 デフォルトが選択されています。

### リーダーボード機能 {#leaderboard-function}

リーダーボード関数は、1 つの [&#x200B; リーダーボードコンポーネント &#x200B;](/help/communities/enabling-leaderboard.md) を持つページです。

**メモ**：リーダーボードコンポーネントを *after* 追加で設定する必要がある場合、リーダーボード機能を含むコミュニティテンプレートからコミュニティサイトを作成します。 コミュニティサイトの [&#x200B; スコアとバッジ &#x200B;](/help/communities/enabling-leaderboard.md#rules-tab) の設定に依存する、リーダーボードコンポーネントの [&#x200B; ルール &#x200B;](/help/communities/implementing-scoring.md) を指定します。

テンプレートに追加すると、次のダイアログが開き、デフォルトのタイトルと URL 名、およびテンプレートのデフォルトの表示設定を指定します。

![leaderboard-dialog](assets/leaderboard-dialog.png)

* [タイトルと URL の設定](#title-and-url-settings)

* **バッジを表示**

  選択すると、バッジアイコンの列がリーダーボードに含まれます。
デフォルトでは選択されていません。

* **バッジ名を表示**

  選択すると、バッジ名の列がリーダーボードに含まれます。
デフォルトでは選択されていません。

* **アバターを表示**

  これを選択すると、メンバーのアバター画像がリーダーボードのメンバープロファイルへの名前リンクの横に表示されます。
デフォルトでは選択されていません。

### ページ機能 {#page-function}

ページ機能は、コミュニティサイトの機能（ログイン、メニュー、通知、メッセージング、テーマ設定およびブランディング）に接続されている空白のページをコミュニティサイトに追加します。 コンテンツは、[&#x200B; 標準のAEM オーサリングモード &#x200B;](/help/sites-authoring/editing-content.md) を使用してページに追加されます。

テンプレートに追加した場合、唯一の設定は [&#x200B; タイトルと URL の設定 &#x200B;](#title-and-url-settings) です。

### Q&amp;A 機能 {#qna-function}

QnA 関数は、タグ付け、ファイルのアップロード、フォロー、自己編集 [&#128279;](/help/communities/working-with-qna.md) 投票、モデレート用に設定された QnA コンポーネントを含むページです。

設定をテンプレートに追加すると、権限のあるメンバーに対する制限が許可されます。

![qna-dialog](assets/qna-dialog.png)

* [タイトルと URL の設定](#title-and-url-settings)

* **ピン留めを許可**

  選択した場合、フォーラムでは、トピックへの返信をコメントのリストの先頭にピン留めできます。 デフォルトが選択されています。

* **権限のあるメンバーを許可**

  QnA フォーラムでは、選択を許可することで、権限を持つメンバーのみが質問を投稿できる [&#x200B; 権限を持つメンバーグループ &#x200B;](/help/communities/users.md#privileged-members-group)。 選択しない場合、すべてのコミュニティメンバーが投稿できます。 デフォルトでは選択されていません。

* **ファイルのアップロードを許可**

  選択した場合、QnA フォーラムには、メンバーがファイルをアップロードする機能が含まれます。 デフォルトが選択されています。

* **スレッド返信を許可**

  これを選択しない場合、QnA フォーラムでは投稿された質問に対するコメント（回答）は許可されますが、回答に対する返信は許可されません。 デフォルトが選択されています。

* **おすすめコンテンツを許可**

  選択した場合、そのコンテンツは [&#x200B; おすすめコンテンツ &#x200B;](/help/communities/featured.md) と識別されます。 デフォルトが選択されています。

## コミュニティ機能を作成 {#create-community-function}

コミュニティ機能を作成するには、コミュニティ機能コンソールの上部にある「`Create Community Function`」アイコンを選択します。 同じAEM ブループリントに基づく複数の関数を作成し、オーサーエディットモードで開いて一意にカスタマイズできます。

![create-community-function](assets/create-community-function.png)

### コミュニティ機能名 {#community-function-name}

![function-name](assets/function-name.png)

コミュニティ機能名パネルで、名前、説明、およびその機能が有効か無効かが設定されます。

* **コミュニティ関数名**

  表示および保存に使用する関数名。

* **コミュニティ機能の説明**

  表示する関数の説明。

* **無効/有効**

  関数が参照可能かどうかを制御するトグルスイッチ。

### AEM ブループリント {#aem-blueprint}

![aem ブループリント &#x200B;](assets/aem-blueprint.png)

`AEM Blueprint` のパネルでは、コミュニティ機能の基盤となる実装であるブループリントを選択できます。

コミュニティ機能は、1 つ以上のページを含むミニサイトで、ログイン、ユーザープロファイル、通知、メッセージング、サイトメニュー、検索、テーマ設定、ブランディング機能など、コミュニティサイトに組み込むために事前に配線されています。 関数を作成したら、オーサー編集モードで [&#x200B; 関数を開く &#x200B;](#open-community-function) ことで、ページまたはコンポーネントの設定をカスタマイズできます。

コミュニティ機能は [&#x200B; ブループリント &#x200B;](/help/sites-administering/msm-livecopy.md#creatingablueprint) の [&#x200B; ライブコピー &#x200B;](/help/sites-administering/msm.md#live-copies) として実装されているので、機能を含む [&#x200B; コミュニティサイトテンプレート &#x200B;](/help/communities/sites.md) または [&#x200B; コミュニティグループテンプレート &#x200B;](/help/communities/tools-groups.md) から作成されたすべてのコミュニティサイトページに影響を与える機能への変更をロールアウトできる場合があります。 親ブループリントからのページの関連付けを解除して、ページレベルの変更を行うこともできます。

[&#x200B; マルチサイトマネージャー &#x200B;](/help/sites-administering/msm.md) も参照してください。

### サムネール {#thumbnail}

![funtion-thumbnail](assets/funtion-thumbnail.png)

サムネールパネルで画像をアップロードして、[&#x200B; コミュニティ機能コンソール &#x200B;](#community-functions-console) に表示することができます。

## コミュニティ機能を開く {#open-community-function}

![open-function](assets/open-function.png)

`Open Community Function` アイコンを選択してオーサー編集モードに入り、ページコンテンツのオーサリングや機能コンポーネントの設定の変更を行います。

### コンポーネントの設定 {#configuring-components}

コミュニティ機能はAEM ブループリントのライブコピーとして実装されます。詳細については、[Multi Site Manager](/help/sites-administering/msm.md) を参照してください。

ページコンテンツのオーサリングだけでなく、コンポーネントの設定も可能です。

作成したコミュニティサイトのページでコンポーネントを設定する場合、コンポーネントを設定するには、[&#x200B; 継承 &#x200B;](/help/sites-administering/msm-livecopy.md#changing-live-copy-content) をキャンセルする必要が生じる場合があります。 設定が完了したら、継承を再確立する必要があります。

設定について詳しくは、作成者の [&#x200B; コミュニティコンポーネント &#x200B;](/help/communities/author-communities.md) を参照してください。

## コミュニティ機能を編集 {#edit-community-function}

![edit-function](assets/edit-function.png)

「`Edit Community Function`」アイコンを選択し、[&#x200B; コミュニティ関数の作成 &#x200B;](#create-community-function) と同じパネルを使用して、関数の有効化や無効化を含む関数のプロパティを編集します。
