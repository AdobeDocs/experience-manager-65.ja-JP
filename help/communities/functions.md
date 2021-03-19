---
title: コミュニティ機能
seo-title: コミュニティ機能
description: コミュニティ機能コンソールにアクセスする方法を説明します
seo-description: コミュニティ機能コンソールにアクセスする方法を説明します
uuid: d3d70134-f318-4709-a673-b01a3467d980
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 91833914-b811-4355-a97d-e1a9cb7441f1
docset: aem65
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2459'
ht-degree: 43%

---


# コミュニティ機能{#community-functions}

コミュニティに必要とされる機能の種類はだいたい決まっています。コミュニティ機能はコミュニティ機能として利用できます。 基本的に、これらは、コミュニティ機能を実装するために事前に配線された1つ以上のページです。コミュニティ機能を実装するには、作成者モードでページにコンポーネントを追加する以外にも必要です。 これらは、[作成](/help/communities/sites-console.md)されたコミュニティサイトの[コミュニティサイトテンプレート](/help/communities/sites.md)の構造を定義するために使用される構成要素です。

コミュニティサイトが作成されると、標準の[AEMオーサリングモード](/help/sites-authoring/editing-content.md)を使用して、結果のページにコンテンツを追加できます。 コミュニティ機能コンソールには、様々なコミュニティ機能が表示されます。

>[!NOTE]
>
>[コミュニティサイト](/help/communities/sites-console.md)、[コミュニティサイトテンプレート](/help/communities/sites.md)、[コミュニティグループテンプレート](/help/communities/tools-groups.md)、[コミュニティ機能](/help/communities/functions.md)の作成用コンソールは、作成者環境でのみ使用できます。

## Community Functions Console {#community-functions-console}

作成者環境のコミュニティ機能コンソールにアクセスするには：

* **[!UICONTROL ツール]** > **[!UICONTROL コミュニティ]** > **[!UICONTROL コミュニティ機能]**&#x200B;に移動します。

![コミュニティ機能](assets/community-functions.png)

## 標準で提供される機能 {#pre-built-functions}

AEM Communities で提供される機能を以下で簡単に説明します。各機能は、[コミュニティサイトテンプレート](/help/communities/sites.md)に容易に組み込むことができる機能に結合されたCommunitiesコンポーネントを含む1つ以上のAEMページを含む。

コミュニティサイトテンプレートは、ログイン、ユーザープロファイル、通知、メッセージング、サイトメニュー、検索、テーマ、ブランディング機能など、コミュニティサイトの構造を定義します。

### タイトルと URL の設定  {#title-and-url-settings}

**タイトル**&#x200B;と **URL** は、すべてのコミュニティ機能に共通するプロパティです。

コミュニティ機能をコミュニティサイトテンプレートに追加するか、コミュニティサイトの構造を[変更](/help/communities/sites-console.md#modifying-site-properties)すると、その機能のダイアログが開き、タイトルと URL を設定できます。

#### 設定機能の詳細  {#configuration-function-details}

![title-url-details](assets/title-url-details.png)

* **タイトル**

   （*必須*）サイトの機能のメニューに表示されるテキスト

* **URL**

   （*必須*）URIの生成に使用する名前。 この名前は、AEMおよびJCRが定める[命名規則](/help/sites-developing/naming-conventions.md)に従う必要があります。

例えば、[使用の手引き](/help/communities/getting-started.md)のチュートリアルに従って作成したサイトを使用し、

* タイトル = Web ページ
* URL = page

次に、ページのURLはhttps://localhost:4503/content/sites/engage/en/page.htmlになります。

また、このページのメニューリンクは以下のように表示されます。

![関与ページ](assets/engage-page.png)

### アクティビティストリーム機能 {#activity-stream-function}

アクティビティストリーム機能は、選択されたすべてのビュー（すべてのアクティビティ、ユーザーアクティビティおよびフォロー）を備えた[アクティビティストリームコンポーネント](/help/communities/activities.md)を含むページです。開発者向けの[アクティビティストリームの初期設定](/help/communities/essentials-activities.md)も参照してください。

テンプレートに追加すると、次のダイアログが開きます。

#### 設定機能の詳細 {#configuration-function-details-1}

![function-details](assets/function-details.png)

* [Title and URL Settings](#title-and-url-settings)

* **「マイアクティビティ」ビューを表示**

   選択した場合、アクティビティページには、現在のメンバーによってコミュニティ内で生成されたアクティビティに基づいてフィルターを行うタブが含まれます。 デフォルトで選択されています。

* **「すべてのアクティビティ」ビューを表示**

   選択した場合、アクティビティページにはタブが含まれ、このタブには現在のアクティビティがアクセス権を持つコミュニティ内で生成されたすべてのメンバーが含まれます。 デフォルトで選択されています。

* **「ニュースフィード」ビューを表示**

   選択した場合、アクティビティページには、現在のメンバーに基づくアクティビティが従うフィルターのタブが含まれます。 デフォルトで選択されています。

### 割り当て機能 {#assignments-function}

割り当て関数は、有効化](/help/communities/overview.md#enablement-community)の[コミュニティサイトを定義する基本機能です。 コミュニティのメンバーに有効化リソースを割り当てることができます。 [開発者向けのAssignments Essentials](/help/communities/essentials-assignments.md)も参照してください。

この関数は、[有効化アドオン](/help/communities/enablement.md)の機能として利用できます。 有効化アドオンは、実稼働環境で使用するために追加のライセンスが必要です。

テンプレートへの追加時には、[タイトルと URL 設定](#title-and-url-settings)のみを設定します。

### ブログ機能  {#blog-function}

ブログ機能は、タグ付け、ファイルのアップロード、フォロー、メンバー自身による編集、投票、モデレートに対応した[ブログコンポーネント](/help/communities/blog-feature.md)を含むページです。[開発者向けのブログEssentials](/help/communities/blog-developer-basics.md)も参照してください。

テンプレートに追加すると、次のダイアログが開きます。

![blog-component](assets/blog-component.png)

* [タイトルとURLの設定](#title-and-url-settings)

* **権限を持つメンバーを許可**

   選択した場合、ブログは、特権を持つメンバーの[特権を持つメンバーグループ](/help/communities/users.md#privileged-members-group)の選択を許可して、記事の作成のみを許可します。 選択しない場合、すべてのコミュニティメンバーが作成できます。 デフォルト値はオフです。

* **ファイルのアップロードを許可**

   選択すると、メンバーがファイルをアップロードする機能がブログに追加されます。 デフォルトで選択されています。

* **スレッド化された返信を許可**

   選択しなかった場合、ブログでは記事への返信（コメント）は許可されますが、コメントへの返信は許可されません。 デフォルトで選択されています。

* **おすすめコンテンツを許可**

   選択すると、ブログは[特集コンテンツ](/help/communities/featured.md)として識別されます。 デフォルトで選択されています。

### カレンダー機能 {#calendar-function}

カレンダー機能は、タグ付けに対応した[カレンダーコンポーネント](/help/communities/calendar.md)を含むページです。開発者向けの[Calendar Essentials](/help/communities/calendar-basics-for-developers.md)も参照してください。

テンプレートに追加すると、次のダイアログが開きます。

![カレンダーの詳細](assets/calendar-details.png)

* [タイトルとURLの設定](#title-and-url-settings)

* **ピン留めを許可**

   選択すると、トピックの返信をコメントのリストの先頭に固定できます。 デフォルトで選択されています。

* **権限を持つメンバーを許可**

   選択した場合、ブログは、特権を持つメンバーの[特権を持つメンバーグループ](/help/communities/users.md#privileged-members-group)の選択を許可して、記事の作成のみを許可します。 選択しない場合、すべてのコミュニティメンバーが作成できます。 デフォルト値はオフです。

* **ファイルのアップロードを許可**

   選択すると、メンバーがファイルをアップロードする機能がブログに追加されます。 デフォルトで選択されています。

* **スレッド化された返信を許可**

   選択しなかった場合、ブログでは記事への返信（コメント）は許可されますが、コメントへの返信は許可されません。 デフォルトで選択されています。

* **おすすめコンテンツを許可**

   選択すると、そのコンテンツは[特集コンテンツ](/help/communities/featured.md)として識別されます。 デフォルトで選択されています。

### カタログ機能 {#catalog-function}

カタログ機能は、[イネーブルメントコミュニティ](/help/communities/overview.md#enablement-community)のメンバーが、割り当てられていないイネーブルメントリソースを参照できるようにします。 開発者向けの[タグ付け可能なリソース](/help/communities/tag-resources.md)と[カタログの初期設定](/help/communities/catalog-developer-essentials.md)を参照してください。

コミュニティサイトの有効化リソースと学習パスは、そのプロパティ` [Show in Catalog](/help/communities/resources.md)`がtrueに設定されている場合、すべてのカタログに表示されます。 リソースと学習パスを明示的に含めるには、[プリフィルター](/help/communities/catalog-developer-essentials.md#pre-filters)をカタログに適用する必要があります。

テンプレートに追加した場合、この設定により、サイト訪問者に表示されるタグフィルターの設定に使用されるタグ名前空間を指定できます。

![カタログ関数](assets/catalog-function.png)

* [タイトルとURLの設定](#title-and-url-settings)

* **すべての名前空間を選択**

   選択したタグ名前空間は、カタログにリストされているイネーブルメントリソースのリストをフィルタリングする訪問者が選択できるタグを定義します。
選択した場合、コミュニティサイトで許可されているすべてのタグ名前空間を利用できます。
選択しない場合は、コミュニティサイトで許可される1つ以上の名前空間を選択できます。
デフォルトで選択されています。

### おすすめコンテンツ機能 {#featured-content-function}

おすすめコンテンツ機能は、コメントの追加と削除に対応した[おすすめコンテンツコンポーネント](/help/communities/featured.md)を含むページです。

おすすめコンテンツの機能は、コンポーネントごとに許可または禁止することができます（[ブログ機能](#blog-function)、[カレンダー機能](#calendar-function)、[フォーラム機能](#forum-function)、[アイディエーション機能](#ideation-function)、[Q&amp;A 機能](#qna-function)を参照してください）。

テンプレートへの追加時には、[タイトルと URL 設定](#title-and-url-settings)のみを設定します。

### ファイルライブラリ機能  {#file-library-function}

ファイルライブラリ機能は、コメントの追加と削除に対応した[ファイルライブラリコンポーネント](/help/communities/file-library.md)を含むページです。

テンプレートへの追加時には、[タイトルと URL 設定](#title-and-url-settings)のみを設定します。

### フォーラム機能  {#forum-function}

フォーラム機能は、タグ付け、ファイルのアップロード、フォロー、メンバー自身による編集、投票、モデレートに対応した[フォーラムコンポーネント](/help/communities/forum.md)を含むページです。

テンプレートに追加すると、次のダイアログが開きます。

#### 設定機能の詳細 {#configuration-function-details-2}

![forum-component1](assets/forum-component1.png)

* [タイトルとURLの設定](#title-and-url-settings)

* **ピン留めを許可**

   選択すると、トピックの返信をコメントのリストの先頭に固定できます。 デフォルトで選択されています。

* **権限を持つメンバーを許可**

   選択した場合、フォーラムは、[特権メンバーグループ](/help/communities/users.md#privileged-members-group)の選択を許可して、特権メンバーの投稿のみを許可します。 選択しない場合、すべてのコミュニティメンバーが投稿を許可されます。 デフォルト値はオフです。

* **ファイルのアップロードを許可**

   選択すると、メンバーがファイルをアップロードする機能がフォーラムに組み込まれます。 デフォルトで選択されています。

* **スレッド化された返信を許可**

   選択しなかった場合、フォーラムではトピックに対するコメントは許可されますが、これらのコメントに対する返信は許可されません。 デフォルトで選択されています。

* **おすすめコンテンツを許可**

   選択した場合、コンポーネントのコンテンツは[特集コンテンツ](/help/communities/featured.md)として識別されます。 デフォルトで選択されています。

### グループ機能 {#groups-function}

>[!CAUTION]
>
>グループ関数は、サイトの構造またはコミュニティサイトテンプレート内の&#x200B;*最初の*&#x200B;関数ではなく、*唯一の*&#x200B;関数である必要があります。
>
>他の機能（[ページ機能](#page-function)など）を含め、その機能を 1 番目にリストする必要があります。

グループ機能を使用すると、パブリッシュ環境でコミュニティメンバーがコミュニティサイト内にサブコミュニティを作成できます。

グループ機能を[コミュニティサイトテンプレート](/help/communities/sites.md)に含めるときの[設定](/help/communities/sites-console.md#groupmanagement)によって、グループを公開または非公開にしたり、1 つ以上のコミュニティグループテンプレートを設定しておいて、コミュニティグループを（パブリッシュ環境から）実際に作成するときにテンプレートを選択できるようにすることも可能です。[コミュニティグループテンプレート](/help/communities/tools-groups.md)は、フォーラムやカレンダーなど、グループページ用に作成するコミュニティ機能を指定します。

コミュニティグループを作成すると、この新しいグループに対してメンバーグループが動的に作成され、メンバーの割り当てや追加ができるようになります。詳細については、[ユーザーとユーザーグループの管理](/help/communities/users.md)を参照してください。

Communities [機能パック 1](/help/communities/deploy-communities.md#latestfeaturepack) 以降では、コミュニティグループはオーサー環境で[コミュニティサイトのグループコンソール](/help/communities/groups.md)を使用して作成します。また、有効な場合はパブリッシュ環境でも作成できます。

テンプレートに追加すると、次のダイアログが開きます。

![group-template-config](assets/group-template-config.png)

* [タイトルとURLの設定](#title-and-url-settings)

* **グループテンプレートを選択**

   (公開環境で)新しいコミュニティグループの将来の作成者が選択できる、1つ以上の有効なグループテンプレートの選択を可能にするドロップダウン。

* **権限を持つメンバーを許可**

   選択した場合、フォーラムは、[特権メンバーのセキュリティグループ](/help/communities/users.md#privileged-members-group)の選択を許可して、権限のあるメンバーの投稿のみを許可します。 選択しない場合、すべてのコミュニティメンバーが投稿を許可されます。 デフォルト値はオフです。

* **公開作成を許可**

   選択すると、許可されたコミュニティメンバーは、公開環境でグループを作成できます。 選択しない場合、新しいグループ（サブコミュニティ）は、Communitiesのサイトグループコンソールから作成者環境でのみ作成できます。
デフォルトで選択されています。

### アイディエーション機能 {#ideation-function}

アイディエーション機能とは、[アイディエーションコンポーネント](/help/communities/ideation-feature.md)を 1 つ含むページです。

テンプレートに追加すると、次のダイアログが開きます。ここで、タイトルおよび URL 名のデフォルトと、テンプレートのデフォルト表示設定を指定します。

![理想関数](assets/ideation-function.png)

* [タイトルとURLの設定](#title-and-url-settings)

* **権限を持つメンバーを許可**

   選択した場合、フォーラムは、[特権メンバーのセキュリティグループ](/help/communities/users.md#privileged-members-group)の選択を許可して、権限のあるメンバーの投稿のみを許可します。 選択しない場合、すべてのコミュニティメンバーが投稿を許可されます。 デフォルト値はオフです。

* **ファイルのアップロードを許可**

   選択すると、メンバーがファイルをアップロードする機能がアイデアに含まれます。 デフォルトで選択されています。

* **スレッド化された返信を許可**

   選択しなかった場合、アイデアではトピックへの返信（コメント）は許可されますが、コメントへの返信は許可されません。 デフォルトで選択されています。

* **おすすめコンテンツを許可**

   選択すると、そのコンテンツは[特集コンテンツ](/help/communities/featured.md)として識別されます。 デフォルトで選択されています。

### リーダーボード機能 {#leaderboard-function}

リーダーボード機能とは、[リーダーボーコンポーネント](/help/communities/enabling-leaderboard.md)を 1 つ含むページです。

**注**:リーダーボードコンポーネントは、リーダーボード機能を含むコミュニティテンプレートからコミュニティサイトを作成した ** 後に、さらに設定する必要があります。リーダーボードコンポーネントの[ルール](/help/communities/enabling-leaderboard.md#rules-tab)を指定します。これは、コミュニティサイトの[スコアおよびバッジ](/help/communities/implementing-scoring.md)の設定に依存します。

テンプレートに追加すると、次のダイアログが開きます。ここで、タイトルおよび URL 名のデフォルトと、テンプレートのデフォルト表示設定を指定します。

![リーダーボード対話](assets/leaderboard-dialog.png)

* [タイトルとURLの設定](#title-and-url-settings)

* **バッジを表示**

   選択すると、バッジアイコンの列がリーダーボードに含まれます。
デフォルト値はオフです。

* **バッジ名を表示**

   選択すると、バッジ名の列がリーダーボードに含まれます。
デフォルト値はオフです。

* **アバターを表示**

   選択すると、メンバーのアバター画像がリーダーボードに含まれ、メンバーのプロファイルへの名前リンクの隣に表示されます。
デフォルト値はオフです。

### ページ機能 {#page-function}

ページ機能を使用すると、ログイン、メニュー、通知、メッセージング、テーマ、ブランディングといったコミュニティサイトの機能が組み込まれた空白のページがコミュニティサイトに追加されます。[標準のAEMオーサリングモード](/help/sites-authoring/editing-content.md)を使用して、コンテンツをページに追加します。

テンプレートへの追加時には、[タイトルと URL 設定](#title-and-url-settings)のみを設定します。

### Q&amp;A 機能  {#qna-function}

Q&amp;A 機能は、タグ付け、ファイルのアップロード、フォロー、メンバー自身による編集、投票、モデレートに対応した [Q&amp;A コンポーネント](/help/communities/working-with-qna.md)を含むページです。

テンプレートへの追加時に、権限を持つメンバーだけが投稿できるような設定をすることができます。

![qna-dialog](assets/qna-dialog.png)

* [タイトルとURLの設定](#title-and-url-settings)

* **ピン留めを許可**

   選択すると、トピックの返信をコメントのリストの先頭に固定できます。 デフォルトで選択されています。

* **権限を持つメンバーを許可**

   選択した場合、QnAフォーラムは、[特権メンバーグループ](/help/communities/users.md#privileged-members-group)の選択を許可することで、特権メンバーに対しての質問の投稿のみを許可します。 選択しない場合、すべてのコミュニティメンバーが投稿を許可されます。 デフォルト値はオフです。

* **ファイルのアップロードを許可**

   選択した場合、QnAフォーラムには、メンバーがファイルをアップロードする機能が含まれます。 デフォルトで選択されています。

* **スレッド化された返信を許可**

   選択しなかった場合、QnAフォーラムでは投稿された質問に対するコメント（回答）は許可されますが、回答に対する返信は許可されません。 デフォルトで選択されています。

* **おすすめコンテンツを許可**

   選択すると、そのコンテンツは[特集コンテンツ](/help/communities/featured.md)として識別されます。 デフォルトで選択されています。

## Create Community Function {#create-community-function}

コミュニティ機能を作成するには、コミュニティ機能コンソールの上部にある`Create Community Function`アイコンを選択します。 同じAEM Blueprintに基づく複数の機能を作成し、作成者編集モードで開いて独自にカスタマイズできます。

![create-community-function](assets/create-community-function.png)

### コミュニティ機能名 {#community-function-name}

![function-name](assets/function-name.png)

コミュニティ機能名パネルでは、機能の名前および説明と、機能を有効にするか無効にするかを設定します。

* **コミュニティ機能名**

   表示とストレージに使用する関数名。

* **コミュニティ機能の説明**

   表示する関数の説明です。

* **無効/有効**

   関数が参照可能かどうかを制御するトグルスイッチ。

### AEM ブループリント {#aem-blueprint}

![aem-blueprint](assets/aem-blueprint.png)

`AEM Blueprint`パネルでは、コミュニティ機能の基本的な実装であるBluePrintを選択できます。

コミュニティ機能は、ログイン、ユーザープロファイル、通知、メッセージング、サイトメニュー、検索、テーマ設定、ブランディング機能など、コミュニティサイトに組み込むための1つ以上のページがあらかじめ用意されているミニサイトです。 関数が作成されたら、[関数](#open-community-function)を作成者編集モードで開き、ページやコンポーネントの設定をカスタマイズできます。

コミュニティ機能は[blueprint](/help/sites-administering/msm-livecopy.md#creatingablueprint)の[ライブコピー](/help/sites-administering/msm.md#live-copies)として実装されているので、その機能を含む[コミュニティサイトテンプレート](/help/communities/sites.md)または[コミュニティグループテンプレート](/help/communities/tools-groups.md)から作成された全てのコミュニティサイトページに対して行われた変更を展開できる。 また、親の青写真からページの関連付けを解除して、ページレベルの変更を行うこともできます。

[マルチサイトマネージャー](/help/sites-administering/msm.md)も参照してください。

### サムネール  {#thumbnail}

![機能サムネール](assets/funtion-thumbnail.png)

サムネールパネルでは、[コミュニティ機能コンソール](#community-functions-console)に表示する画像をアップロードできます。

## コミュニティ機能を開く  {#open-community-function}

![開機能](assets/open-function.png)

`Open Community Function`アイコンを選択して、ページコンテンツのオーサリングと機能コンポーネントの設定の変更を行うための作成者編集モードに入ります。

### コンポーネントの設定 {#configuring-components}

コミュニティ機能は、AEM ブループリントのライブコピーとして実装されます（ライブコピーについては[マルチサイトマネージャー](/help/sites-administering/msm.md)を参照）。

ページコンテンツのオーサリングだけでなく、コンポーネントの設定をすることもできます。

作成したコミュニティサイトのページでコンポーネントを設定する場合は、[継承](/help/sites-administering/msm-livecopy.md#changing-live-copy-content)を取り消してコンポーネントを構成する必要がある場合があります。 構成が完了したら、継承を再確立する必要があります。

設定について詳しくは、作成者向けの[コミュニティコンポーネント](/help/communities/author-communities.md)を参照してください。

## コミュニティ機能を編集  {#edit-community-function}

![編集機能](assets/edit-function.png)

`Edit Community Function`アイコンを選択し、[コミュニティ関数](#create-community-function)の作成と同じパネルを使用して、関数のプロパティを編集します。このパネルには、関数の有効/無効を含めます。
