---
title: コンテンツフラグメント用コンポーネント
seo-title: コンテンツフラグメント用コンポーネント
description: AEM のコンテンツフラグメントは、ページから独立したアセットとして作成および管理されます
seo-description: AEM のコンテンツフラグメントは、ページから独立したアセットとして作成および管理されます
uuid: 81a9e0fe-ed45-4880-b36c-4f49e2598389
contentOwner: Alison Heimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: b7777dc5-a867-4799-9e2c-a1f4bb5dd96a
docset: aem65
pagetitle: Components for Content Fragments
translation-type: tm+mt
source-git-commit: afed13a2f832b91d0df825d1075852cc84443646
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 78%

---


# コンテンツフラグメント用コンポーネント{#components-for-content-fragments}

## フラグメントオーサリング用コンポーネント {#components-for-fragment-authoring}

>[!CAUTION]
>
>フラグメントエディターで使用する実際のコンポーネントは、変更される可能性があるので、拡張または変更しないことをお勧めします。

See the [Content Fragment Management API - Client-Side](/help/sites-developing/customizing-content-fragments.md#the-content-fragment-management-api-client-side).

## ページオーサリング用コンポーネント {#components-for-page-authoring}

>[!CAUTION]
>
>[コンテンツフラグメントコアコンポーネント](https://helpx.adobe.com/experience-manager/core-components/using/content-fragment-component.html)が推奨されます。詳しくは、[コアコンポーネントの開発](https://helpx.adobe.com/experience-manager/core-components/using/developing.html)を参照してください。
>
>この節では、コンテンツフラグメント用に提供されるオリジナル コンテンツについて説明します（**一般**&#x200B;グループの&#x200B;**コンテンツフラグメント**）。

>[!NOTE]
>
>詳しくは、「 [コンテンツフラグメントレンダリング用のコンポーネントの設定](/help/sites-developing/content-fragments-config-components-rendering.md) 」も参照してください。

Adobe Experience Manager（AEM）のコンテンツフラグメントは、[ページに依存しないアセット](/help/assets/content-fragments/content-fragments.md)として作成および管理されます。コンテンツフラグメントを使用すると、チャネルに特化しないコンテンツをチャネル固有のバリエーションと共に作成できます。[その後、コンテンツページを作成する際に、これらのフラグメントとそのバリエーションを使用できます](/help/sites-authoring/content-fragments.md)。 また、既存のコンテンツフラグメントアセットを使用するには、アセットブラウザーからページに [ドラッグします](/help/sites-authoring/content-fragments.md#adding-a-content-fragment-to-your-page) （基礎コンポーネントの画像など、他のアセットベースのコンポーネントに対しても使用できます）。 既製のコンテンツフラグメントコンポーネントには、参照されているコンテンツフラグメントの[要素](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment)が 1 つだけ表示されます。Using the component dialog you can define the [element, variation and range of fragment paragraphs](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment) that you want to display on the page.

>[!NOTE]
>
>このコンテンツフラグメントコンポーネントは、廃止された記事コンポーネントの強化版として AEM 6.2 で導入されました。

>[!NOTE]
>
>コンテンツフラグメントは、クラシック UI ではサポートされません。

### 定義 {#definition}

**コンテンツフラグメント**&#x200B;コンポーネントは、コンテンツフラグメントアセット（効果的に拡張されたテキストアセット）への参照を保持するために使用されます。コンテンツフラグメントのリソースタイプは次のとおりです。

`dam/cfm/components/contentfragment/contentfragment`

参照を定義するには、次のプロパティを使用します。

`fileReference`

タッチ操作対応 UI のエディター のみ、コンテンツフラグメントコンポーネントを完全にサポートします。これには、次のクライアントライブラリが含まれます。

`cq.authoring.editor.plugin.cfm`

このライブラリは、コンテンツフラグメント専用の機能をエディターに追加します。例えば、ページ上のコンテンツフラグメントの追加および設定機能のサポート、アセットブラウザーでのコンテンツフラグメントアセットの検索機能およびサイドパネルでの関連コンテンツの検索機能を使用できます。

### 中間コンテンツ {#in-between-content}

**コンテンツフラグメント**&#x200B;コンポーネントを使用すると、表示される[要素](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment)のさまざまな段落の間に追加コンポーネントを挿入できます。基本的に、表示される要素は様々な段落で構成されます（各段落はキャリッジリターンによってマークされます）。これらの段落の間に、他のコンポーネントを使用してコンテンツを挿入できます。

技術的な観点から、表示された要素の各段落*はそれぞれ独自のparsysに存在し、段落間に追加する各コンポーネントはparsysに挿入されます（フードの下）。

言い換えると、コンテンツフラグメントコンポーネントのインスタンスが 3 つの段落で構成されている場合、コンポーネントはリポジトリ内に 3 つの異なる parsys を持ちます。コンテンツフラグメントに追加される中間コンテンツはすべて、実際にはこれらの parsys の内部に配置されます。

リポジトリ内では、中間コンテンツは全体の段落構造内での自身の位置を基準として格納されます。実際の段落コンテンツに付加されるわけではありません。

この仕組みを理解するために、次のような状況を考えてみましょう。

* コンテンツフラグメントのインスタンスが 3 つの段落で構成されている
* 2 番目の段落の後に、既にいくつかのコンテンツが挿入されている

   * この場合、コンテンツは 2 番目の parsys に格納されます。

基本的に、このインスタンスの段落構造を変更した場合は（表示される段落のバリエーション、要素または範囲を変更するなど）、表示される中間コンテンツに影響が及びます。例えば次の場合が考えられます。

* コンテンツフラグメントコンポーネントが編集され、2 番目の段落の前に別の段落が追加される：

   * 中間コンテンツは、新規作成された段落の後に表示されます（2 番目の parsys が新規作成された段落を保持するようになります）。

* コンテンツフラグメントコンポーネントが編集され、2 番目の段落が削除される：

   * 中間コンテンツは、以前は 3 番目だった段落の後に表示されます（2 番目の parsys が、以前は 3 番目だった段落を保持するようになります）。

* 最初の段落だけを表示するようにコンテンツフラグメントコンポーネントが設定される：

   * 中間コンテンツは表示されなくなります（新しい設定によって、2 番目の parsys はレンダリングされなくなります）。

### コンテンツフラグメントコンポーネントのカスタマイズ {#customizing-the-content-fragment-component}

既製のコンテンツフラグメントコンポーネントを拡張のブループリントとして使用するときは、次のルールを守ってください。

* HTL レンダリングスクリプトと関連 POJO を再利用して、中間コンテンツ機能の実装方法を確認します。
* Reuse the content fragment node: `cq:editConfig`

   * The `afterinsert`/ `afteredit`/ `afterdelete` listeners are used to trigger JS events. これらのイベントを `cq.authoring.editor.plugin.cfm` クライアントライブラリで処理して、関連コンテンツをサイドパネルに表示します。
   * コンテンツフラグメントアセットのドラッグをサポートするように `cq:dropTargets` を設定します。
   * ページエディターでコンテンツフラグメントのオーサリングをサポートするように `cq:inplaceEditing` を設定します。フラグメントのインプレースエディターは `cq.authoring.editor.plugin.cfm` クライアントライブラリで定義され、クイックリンクによって現在の[要素／バリエーション](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment)を[フラグメントエディター](/help/assets/content-fragments/content-fragments-variations.md)で開けるようにします。

### レンダリング前のアセットの書き直し {#asset-rewriting-before-rendering}

コンテンツフラグメント管理では、初期レンダリング処理を使用してページの最終的な HTML 出力を生成します。これは、コンテンツフラグメントコンポーネントによって内部で使用されますが、参照ページ上の参照フラグメントを更新するバックグラウンド処理でも使用されます。

内部では、このレンダリングに Sling Rewriter を使用します。The respective configuration is found at `/libs/dam/config/rewriter/cfm` and can be adjusted if required. See the [Apache Sling Rewriter](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) for more information.

既成の設定は、次の変換サービスを使用します。

* `transformer-cfm-payloadfilter`  — フラグメントのHTMLの `body` 一部( `<body>...</body>`)のみを取得する場合

* `transformer-cfm-parfilter` - 段落範囲が指定されている場合に、不要な段落を除外します（コンテンツフラグメントコンポーネントで実行可能）
* `transformer-cfm-assetprocessor` - フラグメントに埋め込まれたアセットのリストを取得するために内部で使用されます

レンダリング処理は [`com.adobe.cq.dam.cfm.content.FragmentRenderService`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html) を通じて公開され、必要に応じて、（例えば）カスタムコンポーネントによって活用されます。
