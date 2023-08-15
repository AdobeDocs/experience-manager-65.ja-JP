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
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '2041'
ht-degree: 4%

---

# モデレートコンソール {#moderation-console}

AEM Communitiesで一括 [コミュニティコンテンツのモデレート](/help/communities/moderate-ugc.md) は、管理者とコミュニティモデレーター（モデレーターとして割り当てられた信頼できるコミュニティメンバー）によって、オーサー環境とパブリッシュ環境の両方から実行できます。

管理者とコミュニティのモデレーターも、 [コンテキスト内モデレート](/help/communities/in-context.md) （パブリッシュ環境で使用）

すべての [コミュニティサイト](/help/communities/sites-console.md) は `Administration` 管理者権限を持つログインユーザーが使用できるメニュー項目です。 The `Administration` リンクをクリックすると、モデレートコンソールにアクセスできます。

モデレートコンソールから、管理者とコミュニティモデレーターは、モデレート権限を持つすべてのユーザー生成コンテンツ (UGC) にアクセスできます。 複数のサイトのモデレートを許可されている場合は、すべてのサイトにわたる投稿を表示したり、選択したコミュニティサイトでフィルターしたりできます。

詳しくは、以下を参照してください。 [ユーザーとユーザーグループの管理](/help/communities/users.md).

モデレートコンソールでは、次の機能をサポートしています。

* モデレートタスクを一括して実行します。
* UGC を検索しています。
* UGC の詳細を表示します。
* UGC 作成者の詳細を表示します。

管理者または ` [moderator permissions](/help/communities/in-context.md#identifyingtrustedmembers)`（モデレートタスクを実行できます）

## パブリッシュ環境へのアクセス {#publish-environment-access}

公開済みのコミュニティサイトからモデレートコンソールにアクセスするには、コミュニティモデレーターがサインインすると表示される「管理」リンクを使用します。

![publishweretail](assets/publishweretail.png)

「管理」リンクを選択すると、モデレートコンソールが表示されます。

![moderation-console-publish](assets/moderation-console-publish.png)

## オーサー環境へのアクセス {#author-environment-access}

オーサー環境で、モデレートコンソールに移動するには、次の手順を実行します。

* グローバルナビゲーションから、「 」を選択します。 **[!UICONTROL Communities]** > **[!UICONTROL モデレート]**.

管理者として、または [モデレーター権限](/help/communities/in-context.md#identifyingtrustedmembers)を使用すると、モデレートタスクを実行できます。 表示されるコミュニティコンテンツは、サインインしたメンバーによるモデレートが許可されているものだけです。

>[!NOTE]
>
>パブリッシュ環境の UGC は、選択した SRP が共通ストアを実装している場合にのみ、オーサー環境で表示されます。 例えば、デフォルトではストレージは JSRP です。JSRP は、オーサーとパブリッシュに共通するストアではありません。 [コミュニティコンテンツのストレージ](/help/communities/working-with-srp.md)を参照してください。

![moderationconsoleauthor](assets/moderationconsoleauthor.png)

## モデレートコンソール UI {#moderation-console-ui}

左側のナビゲーションレール（オーサー環境では表示され、パブリッシュ環境では表示されない）の他に、モデレート UI の主な領域は次のとおりです。

* **[上部ナビゲーションバー](#top-navigation-bar)**
* **[ツールバー](#toolbar)**
* **[コンテンツ領域](#content-area)**

### 上部ナビゲーションバー {#top-navigation-bar}

上部ナビゲーションバーは、すべてのコンソールで一定です。 詳しくは、 [基本操作](/help/sites-authoring/basic-handling.md).

### ツールバー {#toolbar}

上部ナビゲーションバーの下にあるツールバーでは、左側に次の切り替えスイッチが表示されます。

* [フィルターレール](/help/communities/moderation.md#filterrail)
パネルが開き、コンテンツのフィルタリングに使用するプロパティを選択できます。

上部ナビゲーションバーの下にあるツールバーでは、左側に次の切り替えスイッチが表示されます。

![toggleswitch](assets/toggleswitch.png)

[フィルターレール](/help/communities/moderation.md#filterrail)
「検索」を選択するとパネルが開き、コンテンツをフィルタリングするプロパティを選択できます。

![filterrail](assets/filterrail.png)

### コンテンツ領域 {#content-area}

コンテンツ領域には、投稿された UGC の情報が含まれます。

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
>コンテンツ領域には、 *無限スクロール*&#x200B;を使用すると、コンテンツの最後に達するまでスクロールを続行できます。 スクロール中でも、ツールバーはコンテンツ領域の上の固定された表示位置に保たれます。

### フィルターレール {#ootbfilters}

![open-filterrail](assets/open-filterrail.png)

サイドパネルアイコンをクリックすると、フィルターレールが開きます。 コンテンツ領域の左側に表示されるフィルターレールには、異なるフィルターが用意されており、それぞれのフィルターは、コンテンツ領域に表示される参照 UGC に直ちに影響を与えます。

各カテゴリ内のフィルターは次のとおりです。 **または**&#x200B;を一緒に追加し、異なるカテゴリのフィルターを **および**&#x200B;一緒に。

例えば、 **質問** および **回答**&#x200B;を選択すると、次のいずれかの **質問** *または* an **回答**.

ただし、 **質問** および **保留中**&#x200B;に含まれている場合、 **質問** および **保留中**.

>[!NOTE]
>
>コミュニティモデレーターは、モデレートコンソールの UI で事前定義済みのフィルターをブックマークできます。 これらのフィルターは URL の末尾に（クエリ文字列パラメーターとして）追加されるので、モデレーターは後でブックマークされたフィルターに戻り、これらのリンクを共有することができます。

![searchicon](assets/searchicon.png)

フィルターレールが開いている場合、検索アイコンはサイドパネルを閉じるかどうかを切り替えます。 ただし、フィルターレールを閉じてユーザー生成コンテンツのみを表示する場合は、検索アイコンをクリックして、「コンテンツのみ」オプションを選択します。

#### コンテンツのパス {#content-path}

コンテンツのパスは、表示される UGC 参照を、指定したコンテンツリポジトリに配置された投稿に限定します。

![content-path](assets/content-path.png)

#### テキスト検索 {#text-search}

テキスト検索では、表示される UGC 参照を、入力したテキストを含む投稿に限定します。

![text-search](assets/text-search.png)

#### サイト {#site}

サイトでは、表示される参照 UGC を、選択したコミュニティサイトへの投稿に限定します。 サイトがチェックされていない場合は、UGC への参照がすべて表示されます。

![site-panel](assets/site-panel.png)

>[!NOTE]
>
>管理者が一括モデレートコンソールにアクセスすると、UGC への参照がすべて表示されます。これには、 [サイト作成ウィザード](/help/communities/sites-console.md)例えば、Geometrixxサンプル。
>
>信頼されたコミュニティメンバーが発行時に一括モデレートコンソールにアクセスすると、そのメンバーがモデレートする権限を持つコミュニティサイト用に作成された UGC への参照のみが表示され、サイトフィルターでフィルタリングできます。

#### コンテンツタイプ {#content-type}

コンテンツタイプは、表示される参照 UGC を、選択したリソースタイプの投稿のみに制限します。 次のタイプを 1 つ以上選択できます。 何も選択しない場合は、すべてのタイプが表示されます。

* **コメント**
* **フォーラムトピック**
* **フォーラム返信**
* **Q&amp;A 質問**
* **Q&amp;A 回答**
* **ブログ記事**
* **ブログコメント**
* **カレンダー イベント**
* **カレンダーコメント**
* **ファイルライブラリフォルダー**
* **ファイルライブラリ文書**
* **アイデア**
* **アイディエーションのコメント**

![content-types](assets/content-types.png)

#### 追加のコンテンツタイプ {#additional-content-types}

フィルタリング対象のリソースを追加するには、次の手順に従います。

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

このフィルターを選択すると、ダッシュボードのコンテンツに、入力した ResourceTypes に一致する UGC が表示されます。

#### ステータス {#status}

ステータスは、表示される UGC 参照を、選択したステータスの投稿に制限します。選択できる投稿には、保留中、承認済み、拒否、クローズ済みの 1 つ以上の投稿、ブログ記事の下書きやスケジュール済み、Q&amp;A の質問に対する回答済みまたは未回答済みが含まれます。 何も選択しない場合は、すべてが表示されます。

>[!NOTE]
>
>「未回答」ステータスのみが選択されている場合、モデレーターには、回答済みの質問を除くすべてのコンテンツ（すべてのコンテンツタイプ）が表示されます。 「回答済みの質問」に対する責任者プロパティが存在しないのは、「未回答の質問」や、フォーラムトピック、ブログ記事、コメントなどのコンテンツの場合です。

![ステータス](assets/statuses.png)

#### フラグ設定 {#flagging}

フラグ設定は、表示される参照 UGC を、フラグ付けされた投稿または非表示の投稿に限定します。

コンテンツにフラグが設定されると、 **フラグ** ボタンをもう一度クリックします。 重要なレベルやフォローアップレベルなどのフラグレベルはありません。

![フラグ](assets/flagging.png)

#### メンバー {#members}

メンバーは、表示される UGC 参照を、入力したメンバー名で投稿された UGC に限定します。

![メンバー](assets/members.png)

#### 過去に投稿済み {#posted-in-the-last}

最後に投稿された UGC 参照は、1 時間、1 日、1 週間、1 か月、または 1 年に行われた投稿に限定されます。

![posted-last](assets/posted-last.png)

#### 好感度 {#sentiment}

[好感度](/help/communities/moderate-ugc.md#sentiment) 表示される UGC 参照を、好感度の値が肯定的、否定的、中立の投稿に限定します。

![好感度](assets/sentiment.png)

## カスタムフィルター {#custom-filters}

の標準フィルターとは別に [フィルターレール](/help/communities/moderation.md#ootbfilters)を使用すると、メタデータに対する追加のカスタムフィルターをモデレート UI に追加できます。 開発者は、GitHub のサンプルコードを使用して、既存のモデレート UI フィルターを拡張できます。

![custom-tag-filter](assets/custom-tag-filter.png)

The [サンプルプロジェクト](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/main/aem-communities-moderation-filter) Github にタグフィルターを実装して、ユーザー生成コンテンツに特定のタグが適用されているかどうかに基づいて UGC リストをフィルタリングします。 サンプルコードに従って、他の類似の UGC メタデータフィールドに類似のフィルターを作成できます。

タグフィルターのサンプルをインストールするには：

1. AEMオーサーでパッケージマネージャーを開きます (`https://[aem-author]:4502/crx/packmgr/index.jsp`) インスタンスとAEM Publish (`https://[aem-publish]:4503/crx/packmgr/index.jsp`) インスタンスを使用します。
1. パッケージをビルドします。 `com.adobe.social.sample.moderation.filter.ui.apps-1.0-SNAPSHOT.zip` を GitHub コードからインストールし、同じ設定を有効にします。
1. AEMオーサーでバンドルコンソールを開きます ( `https://[aem-author]:4502/system/console/bundles`) インスタンスとAEM Publish ( `https://[aem-publish]:4503/system/console/bundles`) インスタンスを使用します。
1. パッケージをビルドします (`[com](https://sample-moderation-filter.com/).adobe.social.sample.moderation.filter.core-1.0-SNAPSHOT.jar`) を GitHub からインストールし、同じ設定を有効にします。
1. に移動します。 **/apps/social/moderation/facets** AEM Author のノード (`https://[aem-author]:4502/crx/de/index.jsp#/apps/social/moderation/facets`) とAEM Publish (`https://[aem-publish]:4502/crx/de/index.jsp#/apps/social/moderation/facets`) インスタンスを使用します。
1. 技術ユーザーの追加 **communities-utility-reader** 次を使用 `jcr:read` 権限。

既存のコミュニティサイトにカスタムフィルターを公開するには：

1. 編集 `Clientlibs` 既存のモデレートページの `/content/we-retail/us/en/community/moderation/shell3/jcr:content/head/clientlibs.`

   * 新しいカテゴリを追加 `cq.social.hbs.moderation.v2.`

1. `/content/we-retail/us/en/community/moderation/shell3/jcr:content/rails/searchWell/items/filters.` に移動します。

   * 新しいコンポーネントに設定 `sling:resourceType = social/moderation/v2/filters.`

1. `/content/we-retail/us/en/community/moderation/shell3/jcr:content/views/content/items/modcontainer` にアクセスします。

   * 新しいコンポーネントに設定 `sling:resourceType = social/moderation/v2/modcontainer`.

## モデレートアクション {#moderation-actions}

[モデレートアクション](/help/communities/moderate-ugc.md#moderation-actions) は、コンテンツ領域での 1 つ以上の選択に対して、またはコンテンツの詳細の表示時に実行できます。

投稿を一括モデレートするには、コンテンツ領域で、選択 (![selecticon](assets/selecticon.png)) アイコンを投稿に表示します。投稿の上にマウスを置く（デスクトップ）か、投稿の上に指を押しながら指を置く（モバイル）と表示されます。 これにより、複数選択モードに入り、クリックするだけで、一括モデレートする後続の投稿を選択できるようになります。 ツールバーに表示されるボタンを使用して、選択した投稿に対するモデレートアクションを実行します。 すべてのアクションで確認を求められます。

コンテンツ領域で 1 つの投稿をモデレートするには、その投稿にマウスを合わせるか（デスクトップ）、投稿上で指を押しながら（モバイル）、投稿にボタンが表示されるようにします。 1 つのコンテンツの詳細で操作する場合は、削除アクションのみが確認を求めます。

### 複数の投稿のモデレート {#moderating-multiple-posts}

一括選択モードに入るには、 `Select` 投稿のアイコン：

![select-icon](assets/select-icon.png)

一括選択モードを終了するには、ツールバーのキャンセル (x) アイコンを選択します。

複数の投稿に対して実行できるモデレートアクションは次のとおりです。

* 拒否
* 削除
* 投稿を閉じる/再度開く

これらのアクションを許可するアイコンは、複数の投稿が選択されている場合にのみツールバーに表示されます。

![隔壁モデレート](assets/bulkmoderate.png)

### 単一の投稿のモデレート {#moderating-a-single-post}

単一選択モードでは、次の操作が可能です。

* ユーザー名を選択して、ユーザーの詳細を表示します。
* 投稿へのリンクを選択して、コンテキスト内の投稿を表示します。
* [返信](#reply)
* [許可](#allow)
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

#### 許可 {#allow}

![許可](assets/allow.png)

1 つの投稿を操作する場合、その投稿にフラグが設定されているか拒否されていると、許可アイコンが表示されます。 フラグが設定されている場合、「許可」を選択するとすべてのフラグがクリアされます。

#### 拒否 {#deny}

![拒否](assets/deny.png)

The **拒否** モデレート操作は、モデレートされているコンテンツに対してのみ使用でき、モデレートされていないコンテンツには表示されません（複数選択モードの場合を除く）。

モデレートされていないコンテンツは常に承認されます。

モデレートされたコンテンツは、最初は「保留」状態になり、後で承認または拒否するように変更できます。

保留中の状態から離れたコンテンツは、保留中の状態に戻すことはできません。 承認または拒否としてマークされたコンテンツは、いつでも別の状態に変更できます。

#### 削除 {#delete}

![削除](assets/delete.png)

単一選択または一括モードでは、項目を選択して削除できます。 削除アクションを実行すると、確認ダイアログが表示されます。 削除すると、それらの項目は直ちにコンテンツ領域から消えます。 **UGC を削除すると、リポジトリから完全に削除され、後で取り出すことはできません**.

#### 閉じる {#close}

![閉じる](assets/close.png)

1 つの投稿を操作する場合、UGC タイプがそのリソースのそれ以上の投稿を防ぐ機能をサポートしている場合は、閉じるアイコンが表示されます。

#### モデレート履歴 {#moderation-history}

![モデレート](assets/moderation.png)

1 つの投稿を操作する場合、その投稿にカーソルを合わせると、モデレート履歴アイコンが表示されます。 このアイコンを選択すると、UGC 投稿に関して実行されたアクションの履歴を含むパネルが表示されます。

複数の UGC 投稿のコンテンツ領域表示に戻るには、ビュー詳細ペインの右上隅にある X を選択します。

例：

![moderation-history](assets/moderation-history.png)

#### 詳細を表示 {#view-detail}

![表示](assets/view.png)

1 つの投稿を操作する場合、UGC を詳細モードで開くと、さらに詳細を表示できます。

これをおこなうには、投稿の上にマウスポインターを置いて、 `View Detail` アイコンをクリックして選択し、投稿の詳細を含むパネルを表示します。

複数の UGC 投稿のコンテンツ領域表示に戻るには、ビュー詳細ペインの右上隅にある X を選択します。

例：

![view1](assets/view1.png)
