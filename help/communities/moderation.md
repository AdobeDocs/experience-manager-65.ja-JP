---
title: モデレートコンソール
seo-title: モデレートコンソール
description: モデレートコンソールへのアクセス方法
seo-description: モデレートコンソールへのアクセス方法
uuid: d3b8a160-85b2-43f4-9891-5fafa8c48c5f
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 404582ab-bb4c-4775-9ae3-17356d376dca
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '2110'
ht-degree: 51%

---


# モデレートコンソール  {#moderation-console}

AEM Communitiesでは、コミュニティコンテンツ[の一括モデレートは、管理者とコミュニティモデレーター（モデレーターとして割り当てられた信頼できるコミュニティメンバー）による作成者と投稿の両方の環境から実行できます。](/help/communities/moderate-ugc.md)

管理者およびコミュニティのモデレーターは、公開環境で[コンテキスト内モデレート](/help/communities/in-context.md)を実行することもできます。

すべての[コミュニティサイト](/help/communities/sites-console.md)の機能は、管理者権限を持つユーザーが使用できる`Administration`メニュー項目です。 `Administration`リンクをクリックすると、モデレートコンソールにアクセスできます。

モデレートコンソールでは、管理者とコミュニティモデレーターが、モデレート権限を持っているすべてのユーザー生成コンテンツ（UGC）にアクセスできます。複数のサイトのモデレートを許可すると、すべてのサイトにわたる投稿の表示や、選択したコミュニティのサイトによるフィルターが可能です。

詳細については、[ユーザーとユーザーグループの管理](/help/communities/users.md)を参照してください。

モデレートコンソールでは以下の操作を実行できます。

* モデレートタスクの一括実行を参照してください。
* UGCの検索を参照してください。
* UGCの詳細の表示を参照してください。
* UGC作成者の詳細の表示。

管理者としてログインした場合、または` [moderator permissions](/help/communities/in-context.md#identifyingtrustedmembers)`を持つメンバーの場合にのみ、モデレートタスクを実行できます。

## パブリッシュ環境からのアクセス {#publish-environment-access}

公開済みのコミュニティサイトからモデレートコンソールにアクセスするには、コミュニティモデレーターがサインインしたときに表示される管理リンクからアクセスします。

![publishewertel](assets/publishweretail.png)

管理リンクを選択すると、以下のモデレートコンソールが表示されます。

![moderation-console-publish](assets/moderation-console-publish.png)

## オーサー環境からのアクセス {#author-environment-access}

オーサー環境でモデレートコンソールに移動するには、

* グローバルナビゲーションから、**[!UICONTROL コミュニティ]**/**[!UICONTROL モデレート]**&#x200B;を選択します。

管理者として、または[モデレーター権限](/help/communities/in-context.md#identifyingtrustedmembers)を持つメンバーとしてサインインした場合にのみ、モデレートタスクを実行できます。 表示されるコミュニティコンテンツは、サインインしたメンバーがモデレートを許可されるものだけです。

>[!NOTE]
>
>パブリッシュ環境の UGC をオーサー環境で表示できるのは、選択した SRP で共通ストアが実装されている場合のみです。例えば、デフォルトでは、ストレージはJSRPです。JSRPは、作成者および発行用の一般的なストアではありません。 [コミュニティコンテンツのストレージ](/help/communities/working-with-srp.md)を参照してください。

![moderationconsoleauthor](assets/moderationconsoleauthor.png)

## モデレートコンソールの UI {#moderation-console-ui}

左側のナビゲーションレール（オーサー環境では表示されますが、パブリッシュ環境では表示されません）の他に、モデレートコンソールの UI には次の主な領域があります。

* **[トップナビゲーションバー](#top-navigation-bar)**
* **[ツールバー](#toolbar)**
* **[コンテンツ領域](#content-area)**

### 上部ナビゲーションバー {#top-navigation-bar}

上部ナビゲーションバーはすべてのコンソールで共通です。詳しくは、[基本操作](/help/sites-authoring/basic-handling.md)を参照してください。

### ツールバー {#toolbar}

上部ナビゲーションバーの下にツールバーがあり、その左側に次の切り替えスイッチがあります。

* [フィルターレール](/help/communities/moderation.md#filterrail)コンテンツのフィルター条件のプロパティを選択できるレールが開きます。

上部ナビゲーションバーの下にツールバーがあり、その左側に次の切り替えスイッチがあります。

![toggleswitch](assets/toggleswitch.png)

[フィルターレール](/help/communities/moderation.md#filterrail)「検索」を選択すると、コンテンツのフィルター条件のプロパティを選択できるレールが開きます。

![filterrail](assets/filterrail.png)

### コンテンツ領域 {#content-area}

コンテンツ領域には、投稿された UGC に関する以下の情報が表示されます。

* UGCが投稿されました
* メンバー名
* 会員アバター
* 投稿の場所。
* 投稿された日時。
* 投稿への返信数。
* [投稿に関連付けら](/help/communities/moderate-ugc.md#sentiment) れたセンチメント
* 承認済みの場合は、チェックマークが表示されます。
* 添付ファイルがある場合は、クリップが表示されます。

>[!NOTE]
> 
>コンテンツ領域には&#x200B;*無限スクロール*&#x200B;があります。つまり、コンテンツの最後に到達するまでスクロールを続行できます。 ツールバーは、スクロール時もコンテンツ領域の上の位置に固定されて表示されます。

### フィルターレール  {#ootbfilters}

![open-filterrail](assets/open-filterrail.png)

サイドパネルアイコンにより、フィルターレールが開きます。 コンテンツ領域の左側に表示されるフィルターレールは、様々なフィルターを提供し、それぞれがコンテンツ領域に表示される参照先のUGCに直接影響します。

各カテゴリ内のフィルターは&#x200B;**OR**&#39;dで、異なるカテゴリ内のフィルターは&#x200B;**AND**&#39;dです。

例えば、**質問**&#x200B;と&#x200B;**回答**&#x200B;の両方を確認すると、**質問** *または*&#x200B;回答&#x200B;**のコンテンツが表示されます。**

ただし、**質問**&#x200B;と&#x200B;**保留中**&#x200B;を確認すると、**質問**&#x200B;で、**保留中**&#x200B;の内容だけが表示されます。

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

サイトは、表示される UGC 参照を、選択したコミュニティサイトへの投稿のみに限定します。サイトがチェックされていない場合は、UGCへのすべての参照が表示されます。

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

* 作成者インスタンスに管理者としてログインします。
* [Webコンソール](https://localhost:4502/system/console/configMgr)を開きます。
* `AEM Communities Moderation Dashboard Filters`を探します。
* 編集モードで開く設定を選択します。
* フィルタするコンポーネントのResourceTypeを入力します。

   * 例えば、含まれる投票コンポーネントをフィルタするには、次のように入力します。

      `Voting=social/tally/components/hbs/voting`
   ![additional-contenttype](assets/additional-contenttype.png)

* 「保存」を選択します。
* コミュニティ — モデレートコンソールを更新します。

結果は、`Content Type`フィルターグループの下の`Voting`に対して選択可能な新しいフィルターになります。

このフィルターを選択すると、ダッシュボードのコンテンツに、入力した ResourceType に一致する UGC が表示されます。

#### ステータス {#status}

ステータスは、表示される UGC 参照を、選択したステータスの投稿のみに限定します。「保留中」、「承認」、「拒否」、「終了」のステータス（ブログ記事の場合は「ドラフト」と「スケジュール済み」、Q&amp;A 質問の場合は「回答済み」と「未回答」もあります）のうち、1 つ以上を選択できます。何も選択しなかった場合は、すべてのものが表示されます。

>[!NOTE]
>
>「未回答」ステータスのみを選択すると、回答済みの質問を除く（すべてのコンテンツタイプの）すべてのコンテンツが表示されます。これは、未回答の質問とフォーラムトピックやブログ記事、コメントなどのコンテンツには、回答済みの質問に関係するプロパティが存在しないからです。

![ステータス](assets/statuses.png)

#### フラグ設定 {#flagging}

フラグ設定は、表示される UGC 参照を、フラグが付いている投稿または非表示の投稿のみに限定します。

一度フラグが付けられると、「**フラグ**」ボタンをもう一度選択して、その1つのコンテンツのフラグを解除するまで、フラグ付けされたままになります。 フラグには重要やフォローアップなどのレベルがないことに注意してください。

![落下](assets/flagging.png)

#### メンバー {#members}

メンバーは、表示される UGC 参照を、特定のメンバー（メンバー名を入力して指定）が投稿した UGC のみに限定します。

![members](assets/members.png)

#### 過去に投稿済み {#posted-in-the-last}

過去に投稿済みは、表示される UGC 参照を、1 時間、1 日以内、1 週間、1 ヶ月または 1 年以内に投稿されたものに限定します。

![最後に投稿された](assets/posted-last.png)

#### 好感度 {#sentiment}

[センチメン](/help/communities/moderate-ugc.md#sentiment) トでは、参照先のUGCの表示が、センチメント値がポジティブ、ネガティブ、中立の投稿に限定されます。

![sentiment](assets/sentiment.png)

## カスタムフィルター{#custom-filters}

[フィルターパネル](/help/communities/moderation.md#ootbfilters)の初期設定されたフィルター以外に、メタデータに関する追加のカスタムフィルターをモデレートUIに追加できます。 開発者は、Githubのサンプルコードを使用して、既存のモデレートUIフィルターを拡張できます。

![custom-tag-filter](assets/custom-tag-filter.png)

Githubの[サンプルプロジェクト](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/main/aem-communities-moderation-filter)は、タグフィルターを実装し、特定のタグがユーザー生成コンテンツに適用されるかどうかに基づいてUGCリストをフィルターします。 サンプルコードに従って、他の類似したUGCメタデータフィールドに類似したフィルターを作成できます。

タグフィルターのサンプルをインストールするには：

1. AEM作成者([https://[aem-author]:4502/crx/packmgr/index.jsp](https://aem65-communities-demo.corp.adobe.com:4502/crx/packmgr/index.jsp))インスタンスとAEM発行([https://[aem-publish]:4503/crx/packmgr/index.jsp](https://aem65-communities-demo.corp.adobe.com:4502/crx/packmgr/index.jsp))インスタンスでパッケージマネージャーを開きます。
1. Githubコードからパッケージ`com.adobe.social.sample.moderation.filter.ui.apps-1.0-SNAPSHOT.zip`を構築し、同じパッケージをインストールして有効にします。
1. AEM作成者(`https://[aem-author]:4502/system/console/bundles`)インスタンスとAEM発行(`https://[aem-publish]:4503/system/console/bundles`)インスタンスのバンドルコンソールを開きます。
1. Githubからパッケージ` [com](https://sample-moderation-filter.com/).adobe.social.sample.moderation.filter.core-1.0-SNAPSHOT.jar`を構築し、同じパッケージをインストールして有効にします。
1. AEM Authorの&#x200B;**/apps/social/moderation/facets**&#x200B;ノード([https://[aem-author]:4502/crx/de/index.jsp#/apps/social/moderation/facets](https://aem65-communities-demo.corp.adobe.com:4502/crx/de/index.jsp#/apps/social/moderation/facets))とAEM Publish ([https://[aem-publish]:4502/crx/de/index.jsp/>[aem-publi/]/>/apps/s/s/s/s/s/s/s/s/s/s/s/s/s/socococococococ/s/s/.](https://aem65-communities-demo.corp.adobe.com:4502/crx/de/index.jsp#/apps/social/moderation/facets)
1. &lt;a2/追加>権限を持つ技術ユーザー&#x200B;**communities-utility-reader**。`jcr:read`

既存のコミュニティサイトにカスタムフィルターを公開するには：

1. 既存のモデレートページの`Clientlibs`を編集`/content/we-retail/us/en/community/moderation/shell3/jcr:content/head/clientlibs.`

   * 追加新しいカテゴリ`cq.social.hbs.moderation.v2.`

1. `/content/we-retail/us/en/community/moderation/shell3/jcr:content/rails/searchWell/items/filters.` に移動します。

   * 新しいコンポーネント`sling:resourceType = social/moderation/v2/filters.`に設定

1. `/content/we-retail/us/en/community/moderation/shell3/jcr:content/views/content/items/modcontainer` にアクセスします。

   * 新しいコンポーネント`sling:resourceType = social/moderation/v2/modcontainer`に設定します。

## モデレートアクション {#moderation-actions}

[モデレートアクション](/help/communities/moderate-ugc.md#moderation-actions)は、コンテンツ領域で選択された 1 つ以上のコンテンツに対して実行したり、コンテンツの詳細表示時に実行したりできます。

投稿を一括モデレートするには、コンテンツ領域で、投稿の選択(![selecticon](assets/selecticon.png))アイコンをクリックします。このアイコンの上にマウスを置くと（デスクトップ）、投稿の指を押して押し続けると（モバイル）、 この操作をおこなうと、複数選択モードに入ります。複数選択モードでは、一括でモデレートする投稿をクリックするだけで選択できます。ツールバーに表示されるボタンを使用して、選択した投稿に対してモデレートアクションを実行します。どのアクションをおこなうときも、必ず確認メッセージが表示されます。

コンテンツ領域内の 1 つの投稿のみをモデレートする場合は、その投稿の上にマウスポインターを置く（デスクトップの場合）か、その投稿を指で長押しして（モバイルの場合）ボタンを表示します。1 つのコンテンツを操作するときは、削除アクションの場合に限り確認メッセージが表示されます。

### 複数の投稿のモデレート  {#moderating-multiple-posts}

投稿の`Select`アイコンをクリックして、一括選択モードに入ります。

![select-icon](assets/select-icon.png)

一括選択モードを終了するには、ツールバーのキャンセル（x）アイコンを選択します。

複数の投稿に対して実行できるモデレートアクションは次のとおりです。

* 拒否
* 削除
* 投稿を閉じる／再度開く

これらのアクションを実行できるアイコンは、複数の投稿を選択したときにのみツールバーに表示されます。

![牛モデレート](assets/bulkmoderate.png)

### 1 つの投稿のモデレート {#moderating-a-single-post}

単一選択モードでは、次の操作が可能です。

* 表示ユーザーの詳細を表示するには、ユーザー名を選択します。
* 投稿へのリンクを選択して、投稿をコンテキスト内で表示します。
* [返信](#reply)
* [許可](#allow)
* [拒否](#deny)
* [削除](#delete)
* [閉じる](#close)
* 表示[モデレート履歴](#moderation-history)
* [詳細を表示](#viewdetails)

モデレートアクションアイコンの上にあるカード表示には、投稿のテキストが表示され、その下に次のことを示すデータが表示されます。

* 返信がある場合は、その前に返信数が付加されます。
* フラグが付いている場合。
* 承認されている場合。
* UGCが投稿された日。

![singleselectmode](assets/singleselectmode.png)

#### 返信 {#reply}

![返信](assets/reply.png)

単一の投稿で作業する場合、UGCタイプが返信をサポートし、返信を許可するように設定されている場合は、返信アイコンが表示されます。

#### アクセス設定 {#allow}

![許可](assets/allow.png)

1 つの投稿を操作するときに、その投稿がフラグ付きか、拒否されている場合は、許可アイコンが表示されます。フラグ付けされた場合、「許可」を選択すると、すべてのフラグがクリアされます。

#### 拒否 {#deny}

![拒否](assets/deny.png)

**モデレートを拒否**&#x200B;アクションは、モデレートされたコンテンツに対してのみ使用でき、複数選択モードを除き、モデレートされていないコンテンツには表示されません。

モデレート対象でないコンテンツは、必ず承認された状態になります。

モデレート対象のコンテンツは、最初は保留中のステータスになり、後で承認または拒否に変更できます。

保留中から別のステータスに変更されたコンテンツが、保留中に戻ることはありません。承認または拒否のステータスに設定されたコンテンツは、いつでも別のステータスに変更できます。

#### 削除 {#delete}

![次を削除します。](assets/delete.png)

単一選択モードまたは一括モードで、アイテムを選択して削除できます。削除のアクションを実行すると、確認ダイアログが表示されます。削除すると、それらの項目はコンテンツ領域からすぐに消えます。 **UGCを削除すると、そのUGCはリポジトリから完全に削除され、後で取得することはできません**。

#### 閉じる {#close}

![close](assets/close.png)

単一の投稿で作業する場合、UGCタイプでそのリソースのそれ以上の投稿を防ぐ機能がサポートされていると、閉じるアイコンが表示されます。

#### Moderation History {#moderation-history}

![モデレート](assets/moderation.png)

1 つの投稿を操作するときに、投稿にカーソルを合わせると、モデレート履歴アイコンが表示されます。アイコンを選択すると、UGC投稿に関して行われたアクションの履歴を含むペインが表示されます。

複数の UGC 投稿のコンテンツ領域に戻るには、表示詳細ウィンドウの右上隅の X を選択します。

次に例を示します。

![モデレート履歴](assets/moderation-history.png)

#### 詳細を表示 {#view-detail}

![表示](assets/view.png)

1 つの投稿を操作するときに、その UGC を詳細モードで開くと、より詳しい情報を表示できます。

その場合は、投稿の上にマウスポインターを置いて`View Detail`アイコンを表示し、選択すると、投稿の詳細を含むパネルが表示されます。

複数の UGC 投稿のコンテンツ領域に戻るには、表示詳細ウィンドウの右上隅の X を選択します。

次に例を示します。

![表示1](assets/view1.png)

