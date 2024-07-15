---
title: モデレートコンソール
description: 管理者とコミュニティモデレーターがモデレートコンソールを使用して、モデレート権限を持つすべての UGC にアクセスする方法を説明します。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: 829da16a-4083-43c1-857d-f2666b363bfc
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '2028'
ht-degree: 2%

---

# モデレートコンソール {#moderation-console}

AEM Communitiesでは、管理者とコミュニティモデレーター [ モデレーターとして割り当てられた信頼できるコミュニティメンバー）が、オーサー環境とPublish環境の両方から一括 ](/help/communities/moderate-ugc.md) コミュニティコンテンツのモデレート）を実行できます。

管理者とコミュニティモデレーターは、Publish環境で [ コンテキスト内モデレート ](/help/communities/in-context.md) を実行することもできます。

すべての [ コミュニティサイト ](/help/communities/sites-console.md) の機能は、管理者権限でログインしたユーザーが使用できる `Administration` メニュー項目です。 `Administration` リンクをクリックすると、モデレートコンソールにアクセスできます。

管理者およびコミュニティモデレーターはモデレートコンソールから、モデレートする権限を持つすべてのユーザー生成コンテンツ（UGC）にアクセスできます。 複数のサイトのモデレートが許可されている場合は、すべてのサイトにわたる投稿を表示したり、選択したコミュニティサイトでフィルタリングしたりできます。

詳しくは、[ ユーザーとユーザーグループの管理 ](/help/communities/users.md) を参照してください。

モデレートコンソールは以下をサポートします。

* モデレートタスクを一括で実行する。
* UGC を検索中。
* UGC の詳細の表示。
* UGC オーサーの詳細の表示。

管理者または ` [moderator permissions](/help/communities/in-context.md#identifyingtrustedmembers)` を持つメンバーとしてログインした場合にのみ、モデレートタスクを実行できます。

## Publish環境へのアクセス {#publish-environment-access}

公開されたコミュニティサイトからモデレートコンソールにアクセスするには、コミュニティモデレーターがログインしたときに表示される管理リンクを使用します。

![publishweretail](assets/publishweretail.png)

管理リンクを選択すると、モデレートコンソールが次のように表示されます。

![moderation-console-publish](assets/moderation-console-publish.png)

## オーサー環境へのアクセス {#author-environment-access}

オーサー環境で、モデレートコンソールにアクセスします。

* グローバルナビゲーションから **[!UICONTROL コミュニティ]**/**[!UICONTROL モデレート]** を選択します。

管理者として、または [ モデレーター権限 ](/help/communities/in-context.md#identifyingtrustedmembers) を持つメンバーとしてログインした場合にのみ、モデレートタスクを実行できます。 表示される唯一のコミュニティコンテンツは、ログインしたメンバーがモデレートを許可されているものです。

>[!NOTE]
>
>Publish環境からの UGC は、選択した SRP が共通ストアを実装している場合にのみ、オーサー環境に表示されます。 例えば、デフォルトではストレージは JSRP ですが、これはオーサーとPublishの共通ストアではありません。 [コミュニティコンテンツのストレージ](/help/communities/working-with-srp.md)を参照してください。

![moderationconsoleauthor](assets/moderationconsoleauthor.png)

## モデレートコンソール UI {#moderation-console-ui}

左側のナビゲーションレール（作成者には表示されますが、Publishには表示されません）の脇に、モデレート UI の主な領域は次のとおりです。

* **[上部ナビゲーションバー](#top-navigation-bar)**
* **[ツールバー](#toolbar)**
* **[コンテンツ領域](#content-area)**

### 上部ナビゲーションバー {#top-navigation-bar}

上部のナビゲーションバーは、すべてのコンソールで一定です。 詳しくは、「基本操作 [ を参照してください ](/help/sites-authoring/basic-handling.md)。

### ツールバー {#toolbar}

上部のナビゲーションバーの下にあるツールバーには、左側に次の切り替えスイッチが用意されています。

* [ フィルターパネル ](/help/communities/moderation.md#filterrail)
コンテンツをフィルタリングするプロパティを選択できるパネルを開きます。

上部のナビゲーションバーの下にあるツールバーには、左側に次の切り替えスイッチが用意されています。

![ トッグレススイッチ ](assets/toggleswitch.png)

[ フィルターパネル ](/help/communities/moderation.md#filterrail)
「検索」を選択するとパネルが開き、コンテンツをフィルタリングするプロパティを選択できます。

![filterrail](assets/filterrail.png)

### コンテンツ領域 {#content-area}

コンテンツ領域には、投稿された UGC の情報が含まれます。

* UGC が投稿されました
* メンバー名
* メンバーアバター
* 投稿の場所
* 投稿時
* 投稿への返信数
* 投稿に関連付けられた [ センチメント ](/help/communities/moderate-ugc.md#sentiment)
* 承認されると、チェックマークが表示されます
* 添付ファイルがある場合、クリップが表示されます

>[!NOTE]
> 
>コンテンツ領域には *無限スクロール* が備わっています。つまり、コンテンツの最後に達するまでスクロールを続けることができます。 スクロール中も、ツールバーはコンテンツ領域の上に固定された表示可能な位置のままになります。

### フィルターパネル {#ootbfilters}

![open-filterrail](assets/open-filterrail.png)

サイドパネルアイコンをクリックすると、フィルターパネルが開きます。 コンテンツ領域の左側に表示されるフィルターレールには、様々なフィルターが用意されており、それぞれがコンテンツ領域に表示される参照元の UGC にすぐに影響を与えます。

各カテゴリ内のフィルターは **OR** 結合され、異なるカテゴリ内のフィルターは **AND** 結合されます。

例えば、**Question** と **Answer** の両方をオンにすると、**Question** *または***Answer** のコンテンツが表示されます。

ただし、「**質問** および **保留中** をチェックすると、**質問** および **保留中** のコンテンツのみが表示されます。

>[!NOTE]
>
>コミュニティモデレーターは、モデレートコンソール UI で事前定義済みフィルターをブックマークできます。 これらのフィルターが URL の末尾に（クエリ文字列パラメーターとして）追加されるので、モデレーターはブックマークされたフィルターに後で戻ることができ、また、これらのリンクを共有できます。

![searchicon](assets/searchicon.png)

フィルターパネルが開くと、検索アイコンがサイドパネルの表示/非表示を切り替えます。 ただし、フィルターパネルを閉じてユーザー生成コンテンツのみを表示するには、検索アイコンをクリックし、「コンテンツのみ」オプションを選択します。

#### コンテンツのパス {#content-path}

コンテンツパスは、表示される参照 UGC を、指定されたコンテンツリポジトリに配置された投稿に制限します。

![content-path](assets/content-path.png)

#### テキスト検索 {#text-search}

テキスト検索では、表示される参照 UGC が、入力されたテキストを含む投稿に制限されます。

![ テキスト検索 ](assets/text-search.png)

#### サイト {#site}

サイトは、表示される参照 UGC を、選択したコミュニティサイトへの投稿に制限します。 サイトのチェックがオフになっている場合、UGC へのすべての参照が表示されます。

![site-panel](assets/site-panel.png)

>[!NOTE]
>
>管理者が一括モデレートコンソールにアクセスすると、Geometrixxサンプルなど、[site creation wizard](/help/communities/sites-console.md) で作成されていないサイトを含む、UGC へのすべての参照が表示されます。
>
>信頼できるコミュニティメンバーがPublishで一括モデレートコンソールにアクセスすると、そのメンバーがモデレートを許可されているコミュニティサイト用に作成された UGC への参照のみが表示されます。 また、サイトフィルターでフィルタリングすることもできます。

#### コンテンツタイプ {#content-type}

コンテンツタイプは、表示される参照 UGC を、選択したリソースタイプの投稿に制限します。 次のタイプの中から 1 つ以上を選択できます。 何も選択されていない場合、すべてのタイプが表示されます。

* **コメント**
* **フォーラムトピック**
* **フォーラム返信**
* **QnA 質問**
* **QnA 回答**
* **ブログ記事**
* **ブログコメント**
* **カレンダーイベント**
* **カレンダーコメント**
* **ファイルライブラリフォルダー**
* **ファイルライブラリドキュメント**
* **アイデア**
* **アイディエーション コメント**

![content-types](assets/content-types.png)

#### 追加のコンテンツタイプ {#additional-content-types}

フィルタリング対象の追加リソースを追加するには：

* オーサーインスタンスに管理者としてログインします。
* [Web コンソール ](https://localhost:4502/system/console/configMgr) を開きます。
* `AEM Communities Moderation Dashboard Filters` を見つけます。
* 設定を選択すると、編集モードで開くことができます。
* フィルターするコンポーネントの ResourceType を入力してください：

   * 例えば、含まれている投票コンポーネントをフィルタリングするには、次のように入力します。

     `Voting=social/tally/components/hbs/voting`

  ![additional-contenttype](assets/additional-contenttype.png)

* 「保存」を選択します。
* Communities - モデレートコンソールを更新します。

その結果、`Content Type` しいフィルターグループの下にある `Voting` の新しい選択可能なフィルターになります。

そのフィルターを選択すると、ダッシュボードのコンテンツに、入力されたいずれかのリソースタイプに一致する UGC が表示されます。

#### ステータス {#status}

ステータスは、表示される参照 UGC を、選択したステータスの投稿に制限します。投稿には、保留、承認済み、拒否、クローズド、ブログ記事のドラフトまたはスケジュール、QnA 質問の回答または未回答が 1 つ以上の場合があります。 何も選択されていない場合、すべてが表示されます。

>[!NOTE]
>
>「未回答」ステータスのみが選択されている場合、モデレーターには、回答された質問を除くすべてのコンテンツ（すべてのコンテンツタイプ）が表示されます。 これは、回答されていない質問や、フォーラムのトピック、ブログの記事、コメントなどの他のコンテンツがある場合、回答された質問の責任があるプロパティが存在しないためです。

![ ステータス ](assets/statuses.png)

#### フラグ設定 {#flagging}

フラグを設定すると、表示される参照 UGC が、フラグが設定された投稿や非表示の投稿に制限されます。

コンテンツの一部にフラグが設定されると、そのコンテンツにフラグが設定されたままになります。その後、「**フラグ**」ボタンをもう一度選択して、そのコンテンツの一部のフラグを解除します。 重要なフラグやフォローアップなどのフラグ設定レベルはありません。

![ フラグ設定 ](assets/flagging.png)

#### メンバー {#members}

メンバーは、表示される参照 UGC を、入力されたメンバー名によって投稿された UGC に制限します。

![ 社員 ](assets/members.png)

#### 過去に投稿済み {#posted-in-the-last}

最終回に投稿される制限：参照される UGC が、過去 1 時間、1 日、1 週間、1 か月、1 年間に行われた投稿に表示されます。

![posted-last](assets/posted-last.png)

#### 好感度 {#sentiment}

[ センチメント ](/help/communities/moderate-ugc.md#sentiment) は、表示される参照 UGC を、センチメント値がプラス、マイナス、ニュートラルの投稿に制限します。

![ センチメント ](assets/sentiment.png)

## カスタムフィルター {#custom-filters}

[ フィルターパネル ](/help/communities/moderation.md#ootbfilters) の標準フィルター以外に、メタデータに対するカスタムフィルターをモデレート UI に追加できます。 開発者は、GitHub のサンプルコードを使用して、既存のモデレート UI フィルターを拡張できます。

![custom-tag-filter](assets/custom-tag-filter.png)

GitHub の [ サンプルプロジェクト ](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/main/aem-communities-moderation-filter) にはタグフィルターが実装されており、特定のタグがユーザー生成コンテンツに適用されているかどうかに基づいて UGC リストをフィルタリングできます。 サンプルコードに従って、他の類似した UGC メタデータフィールドと同様のフィルターを作成できます。

タグフィルターのサンプルをインストールするには：

1. AEM オーサー（`https://[aem-author]:4502/crx/packmgr/index.jsp`）インスタンスとAEM Publish（`https://[aem-publish]:4503/crx/packmgr/index.jsp`）インスタンスで、パッケージマネージャーを開きます。
1. GitHub コードからパッケージ `com.adobe.social.sample.moderation.filter.ui.apps-1.0-SNAPSHOT.zip` をビルドし、それをインストールして有効にします。
1. AEM オーサー（`https://[aem-author]:4502/system/console/bundles`）インスタンスとAEM Publish（`https://[aem-publish]:4503/system/console/bundles`）インスタンスでバンドルコンソールを開きます。
1. GitHub からパッケージ（`[com](https://sample-moderation-filter.com/).adobe.social.sample.moderation.filter.core-1.0-SNAPSHOT.jar`）をビルドし、それをインストールして有効にします。
1. AEM オーサー（`https://[aem-author]:4502/crx/de/index.jsp#/apps/social/moderation/facets`）およびAEM Publish（`https://[aem-publish]:4502/crx/de/index.jsp#/apps/social/moderation/facets`）インスタンスの **/apps/social/moderation/facets** ノードに移動します。
1. `jcr:read` の権限を持つテクニカルユーザー **communities-utility-reader** を追加します。

既存のコミュニティサイトにカスタムフィルターを公開するには：

1. 既存のモデレーションページ `/content/we-retail/us/en/community/moderation/shell3/jcr:content/head/clientlibs.` の `Clientlibs` を編集

   * 新しいカテゴリ `cq.social.hbs.moderation.v2.` を追加

1. `/content/we-retail/us/en/community/moderation/shell3/jcr:content/rails/searchWell/items/filters.` に移動します。

   * 新しいコンポーネント `sling:resourceType = social/moderation/v2/filters.` に設定

1. `/content/we-retail/us/en/community/moderation/shell3/jcr:content/views/content/items/modcontainer` にアクセスします。

   * 新しいコンポーネント `sling:resourceType = social/moderation/v2/modcontainer` に設定します。

## モデレートアクション {#moderation-actions}

[ モデレートアクション ](/help/communities/moderate-ugc.md#moderation-actions) は、コンテンツ領域で選択した 1 つ以上の項目に対して、またはコンテンツの詳細を表示するときに実行できます。

投稿を一括モデレートするには、コンテンツ領域で、投稿の選択（![selecticon](assets/selecticon.png)）アイコンをクリックします。これは、マウス（デスクトップ）で投稿にカーソルを合わせたり、投稿の上で指を押し続けたり（モバイル）したときに表示されます。 これにより、複数選択モードに入り、クリックするだけで一括モデレートされる後続の投稿を選択できるようになります。 ツールバーに表示されたボタンを使用して、選択した投稿に対してモデレートアクションを実行できます。 すべてのアクションで確認を求められます。

コンテンツエリアで 1 つの投稿をモデレートするには、マウス（デスクトップ）で投稿の上にマウスポインターを置くか、投稿の上で指を押したままにします（モバイル）。すると、投稿にボタンが表示されます。 単一のコンテンツの詳細に対して操作を行う場合、削除アクションでのみ確認を求められます。

### 複数の投稿のモデレート {#moderating-multiple-posts}

投稿上の `Select` のアイコンをクリックして、一括選択モードに入ります。

![select-icon](assets/select-icon.png)

一括選択モードを終了するには、ツールバーのキャンセル（x）アイコンを選択します。

複数の投稿に対して実行できるモデレートアクションは次のとおりです。

* 拒否
* 削除
* 投稿を閉じる/再度開く

これらのアクションを許可するアイコンは、複数の投稿が選択されている場合にのみツールバーに表示されます。

![bulkmoderate](assets/bulkmoderate.png)

### 1 つの投稿のモデレート {#moderating-a-single-post}

単一選択モードでは、次の操作が可能です。

* ユーザー名を選択して、ユーザーの詳細を表示します。
* 投稿へのリンクを選択して、投稿のコンテキスト内を表示します。
* [返信](#reply)
* [許可](#allow)
* [拒否](#deny)
* [削除](#delete)
* [閉じる](#close)
* 表示 [ モデレート履歴 ](#moderation-history)
* [詳細を表示](#viewdetails)

モデレートアクションアイコンの上のカード表示には、投稿のテキストが表示され、以下には以下を示すデータが表示されます。

* 返信がある場合は、返信の数が先頭に表示されます
* フラグが設定されている場合
* 承認されている場合
* UGC が投稿された日時

![singleselectmode](assets/singleselectmode.png)

#### 返信 {#reply}

![ 返信 ](assets/reply.png)

1 つの投稿に対処する場合、UGC タイプが返信をサポートしていて、返信を許可するように設定されている場合、返信アイコンが表示されます。

#### 許可 {#allow}

![許可](assets/allow.png)

1 つの投稿で作業している場合、投稿にフラグが付いているか拒否されると、「許可」アイコンが表示されます。 フラグが設定されている場合、「許可」を選択すると、すべてのフラグがクリアされます。

#### 拒否 {#deny}

![ 拒否 ](assets/deny.png)

**拒否** モデレートアクションは、モデレートされたコンテンツでのみ使用でき、複数選択モードの場合を除き、モデレートされていないコンテンツには表示されません。

モデレートされていないコンテンツは常に承認されます。

モデレートされたコンテンツは、最初は保留状態になり、後で承認または却下のために変更できます。

保留状態を終了したコンテンツが、保留状態に戻ることはありません。 承認済みまたは拒否とマークされたコンテンツは、いつでも別の状態に変更できます。

#### 削除 {#delete}

![ 削除 ](assets/delete.png)

単一選択モードまたは一括モードでは、項目を選択して削除できます。 削除アクションを実行すると、確認ダイアログが表示されます。 削除すると、これらの項目はコンテンツ領域からすぐに消えます。 **UGC が削除されると、リポジトリから完全に削除され、後で取得することはできません**。

#### 閉じる {#close}

![ 閉じる ](assets/close.png)

1 つの投稿で作業する場合、UGC タイプがそのリソースに対するそれ以上の投稿を防ぐ機能をサポートしている場合は、閉じるアイコンが表示されます。

#### モデレート履歴 {#moderation-history}

![ モデレーション ](assets/moderation.png)

1 つの投稿にカーソルを合わせると、モデレート履歴アイコンが表示されます。 アイコンを選択すると、UGC の投稿に関して実行されたアクションの履歴を含むパネルが表示されます。

複数の UGC 投稿のコンテンツエリア表示に戻るには、ビュー詳細ペインの右上隅にある「X」を選択します。

次に例を示します。

![ モデレーション履歴 ](assets/moderation-history.png)

#### 詳細を表示 {#view-detail}

![ 表示 ](assets/view.png)

1 つの投稿で作業する場合、UGC を詳細モードで開くと、詳細を表示できます。

これを行うには、投稿にカーソルを合わせて「`View Detail`」アイコンを表示し、選択して、投稿の詳細を含むパネルを表示します。

複数の UGC 投稿のコンテンツエリア表示に戻るには、ビュー詳細ペインの右上隅にある「X」を選択します。

次に例を示します。

![view1](assets/view1.png)
