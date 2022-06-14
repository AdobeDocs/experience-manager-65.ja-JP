---
title: モデレートコンソール
seo-title: Moderation Console
description: モデレートコンソールへのアクセス方法
seo-description: How to access the Moderation console
uuid: d3b8a160-85b2-43f4-9891-5fafa8c48c5f
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 404582ab-bb4c-4775-9ae3-17356d376dca
docset: aem65
role: Admin
exl-id: 829da16a-4083-43c1-857d-f2666b363bfc
source-git-commit: 1d334c42088342954feb34f6179dc5b134f81bb8
workflow-type: tm+mt
source-wordcount: '2042'
ht-degree: 53%

---

# モデレートコンソール {#moderation-console}

AEM Communitiesで一括 [コミュニティコンテンツのモデレート](/help/communities/moderate-ugc.md) は、管理者とコミュニティモデレーター（モデレーターとして割り当てられた信頼できるコミュニティメンバー）によって、オーサー環境とパブリッシュ環境の両方から実行できます。

管理者とコミュニティモデレーターも、 [コンテキスト内モデレート](/help/communities/in-context.md) （パブリッシュ環境で）

すべての [コミュニティサイト](/help/communities/sites-console.md) は `Administration` 管理者権限を持つログインユーザーが使用できるメニュー項目です。 この `Administration` リンクをクリックすると、モデレートコンソールにアクセスできます。

モデレートコンソールでは、管理者とコミュニティモデレーターが、モデレート権限を持っているすべてのユーザー生成コンテンツ（UGC）にアクセスできます。複数のサイトのモデレートを許可されている場合は、すべてのサイトにわたる投稿を表示したり、選択したコミュニティサイトでフィルターしたりできます。

詳しくは、 [ユーザーとユーザーグループの管理](/help/communities/users.md).

モデレートコンソールでは以下の操作を実行できます。

* モデレートタスクを一括して実行します。
* UGC を検索しています。
* UGC の詳細を表示します。
* UGC 作成者の詳細を表示します。

管理者または ` [moderator permissions](/help/communities/in-context.md#identifyingtrustedmembers)`（モデレートタスクを実行できます）

## パブリッシュ環境からのアクセス {#publish-environment-access}

公開済みのコミュニティサイトからモデレートコンソールにアクセスするには、コミュニティモデレーターがサインインしたときに表示される管理リンクからアクセスします。

![publishweretail](assets/publishweretail.png)

管理リンクを選択すると、以下のモデレートコンソールが表示されます。

![moderation-console-publish](assets/moderation-console-publish.png)

## オーサー環境からのアクセス {#author-environment-access}

オーサー環境でモデレートコンソールに移動するには、

* グローバルナビゲーションから、 **[!UICONTROL コミュニティ]** > **[!UICONTROL モデレート]**.

管理者として、または [モデレーター権限](/help/communities/in-context.md#identifyingtrustedmembers)を使用すると、モデレートタスクを実行できます。 表示されるコミュニティコンテンツは、サインインしたメンバーによるモデレートが許可されているものだけです。

>[!NOTE]
>
>パブリッシュ環境の UGC をオーサー環境で表示できるのは、選択した SRP で共通ストアが実装されている場合のみです。例えば、デフォルトではストレージは JSRP です。JSRP は、オーサーとパブリッシュに共通するストアではありません。 [コミュニティコンテンツのストレージ](/help/communities/working-with-srp.md)を参照してください。

![moderationconsoleauthor](assets/moderationconsoleauthor.png)

## モデレートコンソールの UI {#moderation-console-ui}

左側のナビゲーションレール（オーサー環境では表示されますが、パブリッシュ環境では表示されません）の他に、モデレートコンソールの UI には次の主な領域があります。

* **[トップナビゲーションバー](#top-navigation-bar)**
* **[ツールバー](#toolbar)**
* **[コンテンツ領域](#content-area)**

### 上部ナビゲーションバー {#top-navigation-bar}

上部ナビゲーションバーはすべてのコンソールで共通です。詳しくは、 [基本操作](/help/sites-authoring/basic-handling.md).

### ツールバー {#toolbar}

上部ナビゲーションバーの下にツールバーがあり、その左側に次の切り替えスイッチがあります。

* [フィルターレール](/help/communities/moderation.md#filterrail)コンテンツのフィルター条件のプロパティを選択できるレールが開きます。

上部ナビゲーションバーの下にツールバーがあり、その左側に次の切り替えスイッチがあります。

![toggleswitch](assets/toggleswitch.png)

[フィルターレール](/help/communities/moderation.md#filterrail)「検索」を選択すると、コンテンツのフィルター条件のプロパティを選択できるレールが開きます。

![filterrail](assets/filterrail.png)

### コンテンツ領域 {#content-area}

コンテンツ領域には、投稿された UGC に関する以下の情報が表示されます。

* UGC が投稿されました
* メンバー名
* メンバーアバター
* 投稿の場所。
* 投稿された日時。
* 投稿への返信数。
* [好感度](/help/communities/moderate-ugc.md#sentiment) 投稿に関連付けられている
* 承認されている場合は、チェックマークが表示されます。
* 添付ファイルがある場合は、クリップが表示されます。

>[!NOTE]
> 
>コンテンツ領域には、 *無限スクロール*&#x200B;を使用すると、コンテンツの最後に達するまでスクロールを続行できます。 ツールバーは、スクロール時もコンテンツ領域の上の位置に固定されて表示されます。

### フィルターレール {#ootbfilters}

![open-filterrail](assets/open-filterrail.png)

サイドパネルアイコンをクリックすると、フィルターレールが開きます。 コンテンツ領域の左側に表示されるフィルターレールには、異なるフィルターが用意されており、それぞれのフィルターは、コンテンツ領域に表示される参照 UGC に直ちに影響を与えます。

各カテゴリ内のフィルターは次のとおりです **または**&#x200B;を一緒に追加し、異なるカテゴリのフィルターを **および**&#x200B;一緒に。

例えば、 **質問** および **回答**&#x200B;を選択すると、次のいずれかの **質問** *または* an **回答**.

ただし、 **質問** および **保留中**&#x200B;に含まれている場合、 **質問** および **保留中**.

>[!NOTE]
>
>コミュニティモデレーターは、モデレートコンソール UI で事前定義されたフィルターをブックマークできます。これらのフィルターは、URL の末尾に（クエリ文字列パラメーターとして）追加されるので、モデレーターはブックマークしたフィルターに戻ったり、これらのリンクを共有することもできます。

![searchicon](assets/searchicon.png)

フィルターレールが開いているときに「検索」アイコンを選択すると、サイドパネルが閉じます。ただし、フィルターレールを閉じて、ユーザー生成コンテンツのみを表示するには、「検索」アイコンをクリックし、「コンテンツのみ」オプションを選択します。

#### コンテンツのパス {#content-path}

コンテンツのパスは、表示される UGC 参照を、指定したコンテンツリポジトリに配置されている投稿のみに限定します。

![content-path](assets/content-path.png)

#### テキスト検索 {#text-search}

テキスト検索は、表示される UGC 参照を、入力したテキストを含む投稿のみに限定します。

![text-search](assets/text-search.png)

#### サイト {#site}

サイトは、表示される UGC 参照を、選択したコミュニティサイトへの投稿のみに限定します。サイトがチェックされていない場合は、UGC への参照がすべて表示されます。

![site-panel](assets/site-panel.png)

>[!NOTE]
>
>管理者が一括モデレートコンソールにアクセスしたときは、[サイト作成ウィザード](/help/communities/sites-console.md)を使わずに作成したサイト（Geometrixx サンプルサイトなど）も含め、すべての UGC 参照が表示されます。
>
>信頼されているコミュニティメンバーが一括モデレートコンソールにアクセスしたときは、そのメンバーがモデレート権限を持つコミュニティサイト用に作成された UGC 参照のみが表示されます。これらの UGC 参照はサイトフィルターでフィルタリングできます。

#### コンテンツタイプ {#content-type}

コンテンツタイプは、表示される UGC 参照を、選択したリソースタイプの投稿のみに限定します。次に示すタイプの中から 1 つ以上選択できます。何も選択しない場合は、すべてのタイプが表示されます。

* **コメント**
* **フォーラムトピック**
* **フォーラム返信**
* **Q&amp;A 質問**
* **Q&amp;A 回答**
* **ブログ記事**
* **ブログコメント**
* **カレンダーイベント**
* **カレンダーコメント**
* **ファイルライブラリフォルダー**
* **ファイルライブラリ文書**
* **アイデア**
* **アイディエーションのコメント**

![content-types](assets/content-types.png)

#### 追加のコンテンツタイプ {#additional-content-types}

フィルター条件のリソースをさらに追加するには：

* オーサーインスタンスに管理者としてログインします。
* 開く [Web コンソール](https://localhost:4502/system/console/configMgr).
* 場所 `AEM Communities Moderation Dashboard Filters`.
* 編集モードで開く設定を選択します。
* フィルターするコンポーネントの ResourceType を入力します。

   * 例えば、含まれる投票コンポーネントに対してフィルタを適用するには、次のように入力します。

      `Voting=social/tally/components/hbs/voting`
   ![additional-contenttype](assets/additional-contenttype.png)

* 「保存」を選択します。
* コミュニティ — モデレートコンソールを更新します。

その結果、次の項目の選択可能な新しいフィルターが作成されます。 `Voting` の下に `Content Type` フィルターグループを使用します。

このフィルターを選択すると、ダッシュボードのコンテンツに、入力した ResourceType に一致する UGC が表示されます。

#### ステータス {#status}

ステータスは、表示される UGC 参照を、選択したステータスの投稿のみに限定します。「保留中」、「承認」、「拒否」、「終了」のステータス（ブログ記事の場合は「ドラフト」と「スケジュール済み」、Q&amp;A 質問の場合は「回答済み」と「未回答」もあります）のうち、1 つ以上を選択できます。何も選択しなかった場合は、すべてのものが表示されます。

>[!NOTE]
>
>「未回答」ステータスのみを選択すると、回答済みの質問を除く（すべてのコンテンツタイプの）すべてのコンテンツが表示されます。これは、未回答の質問とフォーラムトピックやブログ記事、コメントなどのコンテンツには、回答済みの質問に関係するプロパティが存在しないからです。

![ステータス](assets/statuses.png)

#### フラグ設定 {#flagging}

フラグ設定は、表示される UGC 参照を、フラグが付いている投稿または非表示の投稿のみに限定します。

コンテンツにフラグが設定されると、 **フラグ** ボタンをもう一度クリックします。 フラグには重要やフォローアップなどのレベルがないことに注意してください。

![フラグ](assets/flagging.png)

#### メンバー {#members}

メンバーは、表示される UGC 参照を、特定のメンバー（メンバー名を入力して指定）が投稿した UGC のみに限定します。

![members](assets/members.png)

#### 過去に投稿済み {#posted-in-the-last}

過去に投稿済みは、表示される UGC 参照を、1 時間、1 日以内、1 週間、1 ヶ月または 1 年以内に投稿されたものに限定します。

![posted-last](assets/posted-last.png)

#### 好感度 {#sentiment}

[好感度](/help/communities/moderate-ugc.md#sentiment) 表示される UGC 参照を、好感度の値が肯定的、否定的、中立の投稿に限定します。

![sentiment](assets/sentiment.png)

## カスタムフィルター {#custom-filters}

の標準フィルターとは別に [フィルターレール](/help/communities/moderation.md#ootbfilters)を使用すると、メタデータに対する追加のカスタムフィルターをモデレート UI に追加できます。 開発者は、GitHub のサンプルコードを使用して、既存のモデレート UI フィルターを拡張できます。

![custom-tag-filter](assets/custom-tag-filter.png)

この [サンプルプロジェクト](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/main/aem-communities-moderation-filter) Github にタグフィルターを実装して、ユーザー生成コンテンツに特定のタグが適用されているかどうかに基づいて UGC リストをフィルタリングします。 サンプルコードに従って、他の類似の UGC メタデータフィールドに類似のフィルターを作成できます。

タグフィルターのサンプルをインストールするには：

1. AEM オーサーでパッケージマネージャーを開きます (`https://[aem-author]:4502/crx/packmgr/index.jsp`) インスタンスと AEM パブリッシュ (`https://[aem-publish]:4503/crx/packmgr/index.jsp`) インスタンスを使用します。
1. パッケージをビルドします。 `com.adobe.social.sample.moderation.filter.ui.apps-1.0-SNAPSHOT.zip` を GitHub コードからインストールし、同じ設定を有効にします。
1. AEM オーサーでバンドルコンソールを開きます ( `https://[aem-author]:4502/system/console/bundles`) インスタンスと AEM パブリッシュ ( `https://[aem-publish]:4503/system/console/bundles`) インスタンスを使用します。
1. パッケージ (`[com](https://sample-moderation-filter.com/).adobe.social.sample.moderation.filter.core-1.0-SNAPSHOT.jar`) を GitHub からインストールし、同じ設定を有効にします。
1. に移動します。 **/apps/social/moderation/facets** AEM オーサーのノード (`https://[aem-author]:4502/crx/de/index.jsp#/apps/social/moderation/facets`) と AEM パブリッシュ (`https://[aem-publish]:4502/crx/de/index.jsp#/apps/social/moderation/facets`) インスタンスを使用します。
1. 技術ユーザーの追加 **communities-utility-reader** と `jcr:read` 権限。

既存のコミュニティサイトにカスタムフィルターを公開するには：

1. 編集 `Clientlibs` 既存のモデレートページの `/content/we-retail/us/en/community/moderation/shell3/jcr:content/head/clientlibs.`

   * 新しいカテゴリを追加 `cq.social.hbs.moderation.v2.`

1. `/content/we-retail/us/en/community/moderation/shell3/jcr:content/rails/searchWell/items/filters.` に移動します。

   * 新しいコンポーネントに設定 `sling:resourceType = social/moderation/v2/filters.`

1. `/content/we-retail/us/en/community/moderation/shell3/jcr:content/views/content/items/modcontainer` にアクセスします。

   * 新しいコンポーネントに設定 `sling:resourceType = social/moderation/v2/modcontainer`.

## モデレートアクション {#moderation-actions}

[モデレートアクション](/help/communities/moderate-ugc.md#moderation-actions)は、コンテンツ領域で選択された 1 つ以上のコンテンツに対して実行したり、コンテンツの詳細表示時に実行したりできます。

投稿を一括モデレートするには、コンテンツ領域で、選択 (![selecticon](assets/selecticon.png)) アイコンを投稿に表示します。投稿の上にマウスを置く（デスクトップ）か、投稿の上に指を押しながら（モバイル）表示します。 この操作をおこなうと、複数選択モードに入ります。複数選択モードでは、一括でモデレートする投稿をクリックするだけで選択できます。ツールバーに表示されるボタンを使用して、選択した投稿に対してモデレートアクションを実行します。どのアクションをおこなうときも、必ず確認メッセージが表示されます。

コンテンツ領域内の 1 つの投稿のみをモデレートする場合は、その投稿の上にマウスポインターを置く（デスクトップの場合）か、その投稿を指で長押しして（モバイルの場合）ボタンを表示します。1 つのコンテンツを操作するときは、削除アクションの場合に限り確認メッセージが表示されます。

### 複数の投稿のモデレート {#moderating-multiple-posts}

一括選択モードに入るには、 `Select` 投稿のアイコン：

![select-icon](assets/select-icon.png)

一括選択モードを終了するには、ツールバーのキャンセル（x）アイコンを選択します。

複数の投稿に対して実行できるモデレートアクションは次のとおりです。

* 拒否
* 削除
* 投稿を閉じる／再度開く

これらのアクションを実行できるアイコンは、複数の投稿を選択したときにのみツールバーに表示されます。

![隔壁モデレート](assets/bulkmoderate.png)

### 1 つの投稿のモデレート {#moderating-a-single-post}

単一選択モードでは、次の操作が可能です。

* ユーザー名を選択して、ユーザーの詳細を表示します。
* 投稿へのリンクを選択して、コンテキスト内の投稿を表示します。
* [返信](#reply)
* [アクセス設定](#allow)
* [拒否](#deny)
* [削除](#delete)
* [閉じる](#close)
* 表示 [モデレート履歴](#moderation-history)
* [詳細を表示](#viewdetails)

モデレートアクションアイコンの上のカード表示には、投稿のテキストが表示され、下のデータは次の内容を示します。

* 返信がある場合は、返信の数が前に付きます。
* フラグが設定されている場合。
* 承認されている場合。
* UGC が投稿されたとき。

![singleselectmode](assets/singleselectmode.png)

#### 返信 {#reply}

![返信](assets/reply.png)

1 つの投稿を操作する場合、UGC タイプが返信をサポートし、返信を許可するように設定されている場合は、返信アイコンが表示されます。

#### アクセス設定 {#allow}

![許可](assets/allow.png)

1 つの投稿を操作するときに、その投稿がフラグ付きか、拒否されている場合は、許可アイコンが表示されます。フラグが設定されている場合、「許可」を選択するとすべてのフラグがクリアされます。

#### 拒否 {#deny}

![拒否](assets/deny.png)

この **拒否** モデレート操作は、モデレートされているコンテンツに対してのみ使用でき、モデレートされていないコンテンツには表示されません（複数選択モードの場合を除く）。

モデレート対象でないコンテンツは、必ず承認された状態になります。

モデレート対象のコンテンツは、最初は保留中のステータスになり、後で承認または拒否に変更できます。

保留中から別のステータスに変更されたコンテンツが、保留中に戻ることはありません。承認または拒否のステータスに設定されたコンテンツは、いつでも別のステータスに変更できます。

#### 削除 {#delete}

![delete](assets/delete.png)

単一選択モードまたは一括モードで、アイテムを選択して削除できます。削除のアクションを実行すると、確認ダイアログが表示されます。削除すると、それらの項目は直ちにコンテンツ領域から消えます。 **UGC を削除すると、リポジトリから完全に削除され、後で取り出すことはできません**.

#### 閉じる {#close}

![close](assets/close.png)

1 つの投稿を操作する場合、UGC タイプがそのリソースのそれ以上の投稿を防ぐ機能をサポートしている場合は、閉じるアイコンが表示されます。

#### モデレート履歴 {#moderation-history}

![モデレート](assets/moderation.png)

1 つの投稿を操作するときに、投稿にカーソルを合わせると、モデレート履歴アイコンが表示されます。このアイコンを選択すると、UGC 投稿に関して実行されたアクションの履歴を含むパネルが表示されます。

複数の UGC 投稿のコンテンツ領域に戻るには、表示詳細ウィンドウの右上隅の X を選択します。

次に例を示します。

![moderation-history](assets/moderation-history.png)

#### 詳細を表示 {#view-detail}

![表示](assets/view.png)

1 つの投稿を操作するときに、その UGC を詳細モードで開くと、より詳しい情報を表示できます。

これをおこなうには、投稿の上にマウスポインターを置いて、 `View Detail` アイコンをクリックして選択し、投稿の詳細を含むパネルを表示します。

複数の UGC 投稿のコンテンツ領域に戻るには、表示詳細ウィンドウの右上隅の X を選択します。

次に例を示します。

![view1](assets/view1.png)
