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

コミュニティエクスペリエンスから期待される機能の種類はよく知られています。 コミュニティ機能は、コミュニティ機能として使用できます。 基本的に、オーサーモードでページにコンポーネントを追加するだけで済むコミュニティ機能を実装するように事前に配線された 1 つ以上のページです。 は、の構造を定義するための構成要素です。 [コミュニティサイトテンプレート](/help/communities/sites.md) コミュニティサイトの送信元 [作成日](/help/communities/sites-console.md).

コミュニティサイトを作成したら、標準を使用して、結果のページにコンテンツを追加できます [AEM オーサリングモード](/help/sites-authoring/editing-content.md). コミュニティ機能コンソールに表示されるように、様々なコミュニティ機能を使用できます。

>[!NOTE]
>
>の作成のためのコンソール [コミュニティサイト](/help/communities/sites-console.md), [コミュニティサイトテンプレート](/help/communities/sites.md), [コミュニティグループテンプレート](/help/communities/tools-groups.md)、および [コミュニティ機能](/help/communities/functions.md) は、オーサー環境でのみ使用します。

## コミュニティ機能コンソール {#community-functions-console}

オーサー環境でコミュニティ機能コンソールにアクセスするには：

* に移動します。 **[!UICONTROL ツール]** > **[!UICONTROL コミュニティ]** > **[!UICONTROL コミュニティ機能]**.

![コミュニティ機能](assets/community-functions.png)

## 事前定義済み関数 {#pre-built-functions}

次に、AEM Communitiesで提供される機能について簡単に説明します。 各機能には、Communities コンポーネントがワイヤリングされ、に簡単に組み込むことができる機能が含まれている 1 つ以上のAEM ページが含まれています。 [コミュニティサイトテンプレート](/help/communities/sites.md).

コミュニティサイトテンプレートは、ログイン、ユーザープロファイル、通知、メッセージング、サイトメニュー、検索、テーマ設定、ブランディング機能などの、コミュニティサイトの構造を提供します。

### タイトルと URL の設定 {#title-and-url-settings}

**タイトル** および **URL** は、すべてのコミュニティ機能に共通のプロパティです。

コミュニティ機能をコミュニティサイトテンプレートに追加したり、次の場合に追加したりする [変更中](/help/communities/sites-console.md#modifying-site-properties) コミュニティサイトの構造。関数のダイアログが開き、タイトルと URL を設定できます。

#### 設定機能の詳細 {#configuration-function-details}

![title-url-details](assets/title-url-details.png)

* **タイトル**

  （*必須*） サイトの機能のメニューに表示されるテキスト

* **URL**

  （*必須*） URI の生成に使用される名前。 名前は、に従う必要があります。 [命名規則](/help/sites-developing/naming-conventions.md) AEMおよび JCR による適用

例えば、次のように作成したサイトを使用します [はじめに](/help/communities/getting-started.md) チュートリアル（場合）

* タイトル = Web ページ
* URL = ページ

次に、ページの URL はhttps://localhost:4503/content/sites/engage/en/page.htmlです。

ページのメニューリンクは次のように表示されます。

![engage-page](assets/engage-page.png)

### アクティビティストリーム機能 {#activity-stream-function}

アクティビティストリーム関数は、を持つページです。 [アクティビティストリームのコンポーネント](/help/communities/activities.md) すべての表示を選択した状態（すべてのアクティビティ、ユーザーアクティビティ、後続のアクティビティ）。 関連トピック [アクティビティストリームの初期設定](/help/communities/essentials-activities.md) 開発者向け。

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

ブログ関数は、を含むページです。 [ブログコンポーネント](/help/communities/blog-feature.md) タグ付け、ファイルのアップロード、フォロー、メンバーの自己編集、投票、モデレート用に設定されます。 関連トピック [ブログの基本事項](/help/communities/blog-developer-basics.md) 開発者向け。

テンプレートに追加すると、次のダイアログが開きます。

![blog-component](assets/blog-component.png)

* [タイトルと URL の設定](#title-and-url-settings)

* **特権のあるメンバーを許可する**

  選択した場合、ブログでは、権限のあるメンバーのみが選択を許可して記事を作成できます。 [特権メンバーグループ](/help/communities/users.md#privileged-members-group). 選択しない場合、すべてのコミュニティメンバーが作成できます。 デフォルトでは選択されていません。

* **ファイルのアップロードを許可**

  選択した場合、ブログにはメンバーがファイルをアップロードする機能が含まれます。 デフォルトが選択されています。

* **スレッド返信を許可する**

  選択しない場合、ブログでは記事への返信（コメント）が許可されますが、コメントへの返信は許可されません。 デフォルトが選択されています。

* **おすすめコンテンツを許可**

  選択すると、ブログは次のように識別されます [おすすめコンテンツ](/help/communities/featured.md). デフォルトが選択されています。

### カレンダー機能 {#calendar-function}

カレンダー関数は、を含むページです [カレンダーコンポーネント](/help/communities/calendar.md) タグ付けを許可するように設定されました。 関連トピック [カレンダーの基本事項](/help/communities/calendar-basics-for-developers.md) 開発者向け。

テンプレートに追加すると、次のダイアログが開きます。

![calendar-details](assets/calendar-details.png)

* [タイトルと URL の設定](#title-and-url-settings)

* **ピン留めを許可**

  選択した場合、フォーラムでは、トピックへの返信をコメントのリストの先頭にピン留めできます。 デフォルトが選択されています。

* **特権のあるメンバーを許可する**

  選択した場合、ブログでは、権限のあるメンバーのみが選択を許可して記事を作成できます。 [特権メンバーグループ](/help/communities/users.md#privileged-members-group). 選択しない場合、すべてのコミュニティメンバーが作成できます。 デフォルトでは選択されていません。

* **ファイルのアップロードを許可**

  選択した場合、ブログにはメンバーがファイルをアップロードする機能が含まれます。 デフォルトが選択されています。

* **スレッド返信を許可する**

  選択しない場合、ブログでは記事への返信（コメント）が許可されますが、コメントへの返信は許可されません。 デフォルトが選択されています。

* **おすすめコンテンツを許可**

  選択した場合、そのコンテンツは次のように識別されます [おすすめコンテンツ](/help/communities/featured.md). デフォルトが選択されています。

### おすすめコンテンツ機能 {#featured-content-function}

おすすめコンテンツ関数は、が含まれるページです [おすすめコンテンツコンポーネント](/help/communities/featured.md) コメントを追加および削除できるように設定します。

コンテンツを機能させる機能は、コンポーネントごとに許可または禁止できます（ [ブログ関数](#blog-function), [カレンダー関数](#calendar-function), [フォーラム機能](#forum-function), [Ideation 関数](#ideation-function)、および [QnA 関数](#qna-function)）に設定します。

テンプレートに追加した場合、唯一の設定は、 [タイトルと URL の設定](#title-and-url-settings).

### ファイルライブラリ機能 {#file-library-function}

ファイルライブラリ関数は、を持つページです。 [ファイルライブラリコンポーネント](/help/communities/file-library.md) コメントを追加および削除できるように設定します。

テンプレートに追加した場合、唯一の設定は、 [タイトルと URL の設定](#title-and-url-settings).

### フォーラム機能 {#forum-function}

フォーラム機能は、が含まれるページです。 [フォーラムコンポーネント](/help/communities/forum.md) タグ付け、ファイルのアップロード、フォロー、メンバーの自己編集、投票、モデレート用に設定されます。

テンプレートに追加すると、次のダイアログが開きます。

#### 設定機能の詳細 {#configuration-function-details-2}

![forum-component1](assets/forum-component1.png)

* [タイトルと URL の設定](#title-and-url-settings)

* **ピン留めを許可**

  選択した場合、フォーラムでは、トピックへの返信をコメントのリストの先頭にピン留めできます。 デフォルトが選択されています。

* **特権のあるメンバーを許可する**

  選択した場合、フォーラムでは、権限のあるメンバーのみがトピックを投稿できます（トピックの選択が許可されます） [特権メンバーグループ](/help/communities/users.md#privileged-members-group). 選択しない場合、すべてのコミュニティメンバーが投稿できます。 デフォルトでは選択されていません。

* **ファイルのアップロードを許可**

  選択した場合、フォーラムにはメンバーがファイルをアップロードする機能が含まれます。 デフォルトが選択されています。

* **スレッド返信を許可する**

  選択しない場合、フォーラムではトピックに関するコメントが許可されますが、それらのコメントに対する返信は許可されません。 デフォルトが選択されています。

* **おすすめコンテンツを許可**

  選択した場合、コンポーネントのコンテンツは次のように識別されます [おすすめコンテンツ](/help/communities/featured.md). デフォルトが選択されています。

### Groups 関数 {#groups-function}

>[!CAUTION]
>
>groups 関数には次の条件があります *ではない* 次になる *最初でも唯一でも* サイトの構造またはコミュニティサイトテンプレートで機能します。
>
>その他の関数（など） [ページ関数](#page-function)、を含め、最初にリストする必要があります。

グループ機能は、コミュニティメンバーがパブリッシュ環境のコミュニティサイト内にサブコミュニティを作成する機能を提供します。

基準 [設定](/help/communities/sites-console.md#groupmanagement) groups 関数がに含まれている場合 [コミュニティサイトテンプレート](/help/communities/sites.md)グループは、パブリックまたはプライベートに設定できます。1 つ以上のコミュニティグループテンプレートを設定して、コミュニティグループが実際に作成される際のテンプレートの選択肢を提供することができます（パブリッシュ環境からなど）。 A [コミュニティグループテンプレート](/help/communities/tools-groups.md) フォーラムやカレンダーなど、グループページ用に作成するコミュニティ機能を指定します。

コミュニティグループを作成すると、新しいグループ用にメンバーグループが動的に作成され、メンバーを割り当てたり、結合したりできます。 詳しくは、を参照してください [ユーザーとユーザーグループの管理](/help/communities/users.md).

コミュニティの場合 [機能パック 1](/help/communities/deploy-communities.md#latestfeaturepack)、コミュニティグループは、オーサー環境で次を使用して作成されます [コミュニティサイトのグループコンソール](/help/communities/groups.md)、およびは、有効な場合、パブリッシュ環境で作成できます。

テンプレートに追加すると、次のダイアログが開きます。

![group-template-config](assets/group-template-config.png)

* [タイトルと URL の設定](#title-and-url-settings)

* **グループテンプレートの選択**

  1 つ以上の有効なグループテンプレートを選択できるドロップダウン。今後（パブリッシュ環境で）新しいコミュニティグループを作成する際に、このドロップダウンから選択できます。

* **特権のあるメンバーを許可する**

  選択した場合、フォーラムでは、権限のあるメンバーのみがトピックを投稿できます（トピックの選択が許可されます） [特権メンバーのセキュリティ グループ](/help/communities/users.md#privileged-members-group). 選択しない場合、すべてのコミュニティメンバーが投稿できます。 デフォルトでは選択されていません。

* **パブリッシュの作成を許可**

  これを選択すると、承認済みのコミュニティメンバーは、パブリッシュ環境でグループを作成できます。 選択を解除すると、新しいグループ（サブコミュニティ）は、オーサー環境でコミュニティサイトのグループコンソールからのみ作成できます。
デフォルトが選択されています。

### アイディエーション機能 {#ideation-function}

アイディエーション関数は、1 つを含むページです [アイディエーション成分](/help/communities/ideation-feature.md).

テンプレートに追加すると、次のダイアログが開き、デフォルトのタイトルと URL 名、およびテンプレートのデフォルトの表示設定を指定します。

![観念関数](assets/ideation-function.png)

* [タイトルと URL の設定](#title-and-url-settings)

* **特権のあるメンバーを許可する**

  選択した場合、フォーラムでは、権限のあるメンバーのみがトピックを投稿できます（トピックの選択が許可されます） [特権メンバーのセキュリティ グループ](/help/communities/users.md#privileged-members-group). 選択しない場合、すべてのコミュニティメンバーが投稿できます。 デフォルトでは選択されていません。

* **ファイルのアップロードを許可**

  選択した場合、アイデアにはメンバーがファイルをアップロードする機能が含まれます。 デフォルトが選択されています。

* **スレッド返信を許可する**

  選択しない場合、トピックへの返信（コメント）は許可されますが、コメントへの返信は許可されません。 デフォルトが選択されています。

* **おすすめコンテンツを許可**

  選択した場合、そのコンテンツは次のように識別されます [おすすめコンテンツ](/help/communities/featured.md). デフォルトが選択されています。

### リーダーボード機能 {#leaderboard-function}

リーダーボード関数は、1 つを含むページです [リーダーボードコンポーネント](/help/communities/enabling-leaderboard.md).

**メモ**：リーダーボードコンポーネントには、さらに設定が必要です *後* コミュニティサイトは、リーダーボード機能を含むコミュニティテンプレートから作成されます。 リーダーボードコンポーネントの [個のルール](/help/communities/enabling-leaderboard.md#rules-tab)（の設定に依存） [スコアおよびバッジ](/help/communities/implementing-scoring.md) コミュニティサイト用。

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

ページ機能は、コミュニティサイトの機能（ログイン、メニュー、通知、メッセージング、テーマ設定およびブランディング）に接続されている空白のページをコミュニティサイトに追加します。 コンテンツは、 [標準AEM オーサリングモード](/help/sites-authoring/editing-content.md).

テンプレートに追加した場合、唯一の設定は、 [タイトルと URL の設定](#title-and-url-settings).

### Q&amp;A 機能 {#qna-function}

QnA 関数は、 [QnA コンポーネント](/help/communities/working-with-qna.md) タグ付け、ファイルのアップロード、フォロー、メンバーの自己編集、投票、モデレート用に設定されます。

設定をテンプレートに追加すると、権限のあるメンバーに対する制限が許可されます。

![qna-dialog](assets/qna-dialog.png)

* [タイトルと URL の設定](#title-and-url-settings)

* **ピン留めを許可**

  選択した場合、フォーラムでは、トピックへの返信をコメントのリストの先頭にピン留めできます。 デフォルトが選択されています。

* **特権のあるメンバーを許可する**

  これを選択すると、QnA フォーラムでは、権限を持つメンバーのみが質問を投稿できます。その際、選択を許可します。 [特権メンバーグループ](/help/communities/users.md#privileged-members-group). 選択しない場合、すべてのコミュニティメンバーが投稿できます。 デフォルトでは選択されていません。

* **ファイルのアップロードを許可**

  選択した場合、QnA フォーラムには、メンバーがファイルをアップロードする機能が含まれます。 デフォルトが選択されています。

* **スレッド返信を許可する**

  これを選択しない場合、QnA フォーラムでは投稿された質問に対するコメント（回答）は許可されますが、回答に対する返信は許可されません。 デフォルトが選択されています。

* **おすすめコンテンツを許可**

  選択した場合、そのコンテンツは次のように識別されます [おすすめコンテンツ](/help/communities/featured.md). デフォルトが選択されています。

## コミュニティ機能を作成 {#create-community-function}

コミュニティ機能を作成するには、 `Create Community Function` アイコンはコミュニティ機能コンソールの上部にあります。 同じAEM ブループリントに基づく複数の関数を作成し、オーサーエディットモードで開いて一意にカスタマイズできます。

![create-community-function](assets/create-community-function.png)

### コミュニティ機能名 {#community-function-name}

![function-name](assets/function-name.png)

コミュニティ機能名パネルで、名前、説明、およびその機能が有効か無効かが設定されます。

* **コミュニティ機能名**

  表示および保存に使用する関数名。

* **コミュニティ機能の説明**

  表示する関数の説明。

* **無効/有効**

  関数が参照可能かどうかを制御するトグルスイッチ。

### AEM ブループリント {#aem-blueprint}

![aem-blueprint](assets/aem-blueprint.png)

日 `AEM Blueprint` パネルを使用すると、コミュニティ機能の基盤となる実装であるブループリントを選択できます。

コミュニティ機能は、1 つ以上のページを含むミニサイトで、ログイン、ユーザープロファイル、通知、メッセージング、サイトメニュー、検索、テーマ設定、ブランディング機能など、コミュニティサイトに組み込むために事前に配線されています。 関数を作成すると、次の操作を行うことができます [関数を開きます。](#open-community-function) オーサー編集モードで、ページまたはコンポーネントの設定をカスタマイズします。

コミュニティ機能はとして実装されているので、 [ライブコピー](/help/sites-administering/msm.md#live-copies) の [設計図](/help/sites-administering/msm-livecopy.md#creatingablueprint)から作成されたすべてのコミュニティサイトページに影響を与える関数に対して行われた変更をロールアウトできます。 [コミュニティサイトテンプレート](/help/communities/sites.md) または [コミュニティグループテンプレート](/help/communities/tools-groups.md) これには関数が含まれています。 親ブループリントからのページの関連付けを解除して、ページレベルの変更を行うこともできます。

関連トピック [Multi Site Manager](/help/sites-administering/msm.md).

### サムネール {#thumbnail}

![function-thumbnail](assets/funtion-thumbnail.png)

サムネールパネルで画像をアップロードして、に表示することができます。 [コミュニティ機能コンソール](#community-functions-console).

## コミュニティ機能を開く {#open-community-function}

![open-function](assets/open-function.png)

「」を選択します `Open Community Function` アイコンをクリックしてオーサー編集モードに入り、ページコンテンツのオーサリングと機能コンポーネントの設定の変更を行います。

### コンポーネントの設定 {#configuring-components}

コミュニティ関数は、AEM ブループリントのライブコピーとして実装されます。詳細は、次の場所に記載されています [Multi Site Manager](/help/sites-administering/msm.md).

ページコンテンツのオーサリングだけでなく、コンポーネントの設定も可能です。

作成したコミュニティサイトのページでコンポーネントを設定する場合は、キャンセルする必要がある場合があります [継承](/help/sites-administering/msm-livecopy.md#changing-live-copy-content) コンポーネントを設定します。 設定が完了したら、継承を再確立する必要があります。

設定について詳しくは、次を参照してください： [Communities コンポーネント](/help/communities/author-communities.md) （作成者向け）。

## コミュニティ機能を編集 {#edit-community-function}

![edit-function](assets/edit-function.png)

「」を選択します `Edit Community Function` と同じパネルを使用して関数のプロパティを編集するアイコン [コミュニティ関数の作成](#create-community-function)関数の有効化または無効化を含みます。
