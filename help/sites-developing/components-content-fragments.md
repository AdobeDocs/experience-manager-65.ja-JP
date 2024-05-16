---
title: コンテンツフラグメント用コンポーネント
description: Adobe Experience Manager（AEM）のコンテンツフラグメントは、ページに依存しないアセットとして作成および管理されます。
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
docset: aem65
pagetitle: Components for Content Fragments
exl-id: f2edd9b2-f231-42f3-a25e-428cd1d96c2a
solution: Experience Manager, Experience Manager Sites
feature: Developing,Content Fragments
role: Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: ht
source-wordcount: '932'
ht-degree: 100%

---

# コンテンツフラグメント用コンポーネント{#components-for-content-fragments}

## フラグメントオーサリング用コンポーネント {#components-for-fragment-authoring}

>[!CAUTION]
>
>実際のコンポーネントはまだ変更される可能性があるので、拡張または変更は推奨されません。

[コンテンツフラグメント管理 API - クライアントサイド](/help/sites-developing/customizing-content-fragments.md#the-content-fragment-management-api-client-side)を参照してください。

## ページオーサリング用コンポーネント {#components-for-page-authoring}

>[!CAUTION]
>
>[コンテンツフラグメントのコアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=ja)が推奨されます。詳しくは、[コアコンポーネントの開発](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html?lang=ja)を参照してください。
>
>この節では、コンテンツフラグメントと併用するために配信される元のコンポーネント（**一般**&#x200B;グループ&#x200B;**コンテンツフラグメント**）について説明します。

>[!NOTE]
>
>詳しくは、[レンダリングコンポーネントのコンテンツフラグメントの設定](/help/sites-developing/content-fragments-config-components-rendering.md)も参照してください。

Adobe Experience Manager（AEM）のコンテンツフラグメントは、[ページに依存しないアセットとして作成および管理](/help/assets/content-fragments/content-fragments.md)されます。これにより、チャネルに依存しないコンテンツを様々なバリエーション（チャネル固有）で作成できます。[その後、コンテンツページの作成時に、これらのフラグメントおよびバリエーションを使用できます](/help/sites-authoring/content-fragments.md)。また、[アセットブラウザーからページにドラッグする](/help/sites-authoring/content-fragments.md#adding-a-content-fragment-to-your-page)ことで、既存のコンテンツフラグメントアセットを使用できます（基盤コンポーネントの画像など、他のアセットベースのコンポーネントと同様）。既製のコンテンツフラグメントコンポーネントには、参照されているコンテンツフラグメントの[要素](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment)が 1 つだけ表示されます。ページ上に表示する[要素、バリエーションおよびフラグメント段落の範囲](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment)は、コンポーネントダイアログで定義できます。

>[!NOTE]
>
>このコンテンツフラグメントコンポーネントは、廃止された記事コンポーネントの拡張バージョンとして AEM 6.2 で導入されました。

>[!NOTE]
>
>コンテンツフラグメントは、クラシック UI ではサポートされていません。

### 定義 {#definition}

**コンテンツフラグメント**&#x200B;コンポーネントは、コンテンツフラグメントアセット（効果的に拡張されたテキストアセット）への参照を保持するために使用されます。コンテンツフラグメントのリソースタイプは次のとおりです。

`dam/cfm/components/contentfragment/contentfragment`

参照を定義するには、次のプロパティを使用します。

`fileReference`

コンテンツフラグメントコンポーネントを完全にサポートするのは、タッチ操作対応 UI のエディターのみです。これには、クライアントライブラリが含まれます。

`cq.authoring.editor.plugin.cfm`

このライブラリは、コンテンツフラグメント専用の機能をエディターに追加します。例えば、ページ上でコンテンツフラグメントを追加および設定する機能、アセットブラウザーでコンテンツフラグメントアセットを検索する機能、およびサイドパネルで関連コンテンツを検索する機能を使用できます。

### 中間コンテンツ {#in-between-content}

**コンテンツフラグメント**&#x200B;コンポーネントを使用すると、表示される[要素](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment)の異なる段落の間に追加のコンポーネントをドロップできます。基本的に、表示される要素は異なる段落で構成されます（各段落はキャリッジリターンでマークされます）。これらの各段落の間に、他のコンポーネントを使用してコンテンツを挿入できます。

技術的には、表示される要素の各段落は個別の parsys 内に存在しており、段落間に追加される各コンポーネントは（内部的な処理で）その parsys に挿入されます。

つまり、コンテンツフラグメントコンポーネントのインスタンスが 3 つの段落で構成されている場合、そのコンポーネントはリポジトリ内に 3 つの異なる parsys が存在することになります。コンテンツフラグメントに追加される中間コンテンツは、実際にはこれらの parsys 内に配置されます。

リポジトリ内では、中間コンテンツは、段落構造全体内の位置を基準に格納されます。つまり、中間コンテンツは実際の段落コンテンツには添付されません。

これを説明するために、次の点に注意してください。

* コンテンツフラグメントのインスタンスが 3 つの段落で構成されている
* また、2 番目の段落の後に既に一部のコンテンツが挿入されている

   * これは、コンテンツは 2 番目の parsys に格納されることを意味します。

基本的に、このインスタンスの段落構造を変更した場合は（表示される段落のバリエーション、要素または範囲を変更するなど）、表示される中間コンテンツに影響が及びます。例えば次の場合が考えられます。

* コンテンツフラグメントコンポーネントが編集され、2 番目の段落の前に別の段落が追加される：

   * 中間コンテンツは、新規作成された段落の後に表示されます（2 番目の parsys が新規作成された段落を保持）。

* コンテンツフラグメントコンポーネントが編集され、2 番目の段落が削除された場合。

   * 中間コンテンツは、以前は 3 番目だった段落の後に表示されます（2 番目の parsys が以前は 3 番目だった段落を保持）。

* 最初の段落だけを表示するようにコンテンツフラグメントコンポーネントが設定された場合。

   * 中間コンテンツは表示されません（新しい設定により、2 番目の parsys はレンダリングされなくなります）。

### コンテンツフラグメントコンポーネントのカスタマイズ {#customizing-the-content-fragment-component}

既製のコンテンツフラグメントコンポーネントを拡張のブループリントとして使用するには、次の契約に従う必要があります。

* HTL レンダリングスクリプトとそれに関連する POJO を再利用すると、中間コンテンツ機能の実装方法を確認できます。
* コンテンツフラグメントノード `cq:editConfig` を再利用します。

   *  `afterinsert`／`afteredit`／`afterdelete` リスナーを使用して JS イベントを呼び出します。このイベントは `cq.authoring.editor.plugin.cfm` クライアントライブラリで処理されて、関連コンテンツがサイドパネルに表示されます。
   * コンテンツフラグメントアセットのドラッグをサポートするように `cq:dropTargets` を設定します。
   * ページエディターでコンテンツフラグメントのオーサリングをサポートするように `cq:inplaceEditing` を設定します。フラグメントのインプレースエディターは `cq.authoring.editor.plugin.cfm` クライアントライブラリで定義され、クイックリンクによって現在の[要素／バリエーション](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment)を[フラグメントエディター](/help/assets/content-fragments/content-fragments-variations.md)で開けるようにします。

### レンダリング前のアセットの書き換え {#asset-rewriting-before-rendering}

コンテンツフラグメント管理では、内部レンダリングプロセスを使用して、ページの最終 HTML 出力を生成します。これは、コンテンツフラグメントコンポーネントによって内部的に使用されますが、参照ページ上の参照フラグメントを更新するバックグラウンドプロセスによっても使用されます。

内部では、このレンダリングに Sling Rewriter を使用します。各設定は `/libs/dam/config/rewriter/cfm` にあり、必要に応じて調整できます。詳しくは、[Apache Sling Rewriter](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) を参照してください。

>[!CAUTION]
>
>リライターの設定を調整／オーバーレイする場合：
>
>* `/libs/dam/config/rewriter/cfm`
>
>`serializerType` を次のように更新する&#x200B;**必要があります**。
>
>* `serializerType="html5-serializer"`

既製の設定は、次の変換サービスを使用します。

* `transformer-cfm-payloadfilter` - フラグメントの HTML の `body` 部分（`<body>...</body>`）の取得用のみ

* `transformer-cfm-parfilter` - 段落範囲が指定されている場合に、不要な段落を除外します（コンテンツフラグメントコンポーネントで実行可能）
* `transformer-cfm-assetprocessor` - フラグメントに埋め込まれたアセットのリストを取得するために内部で使用されます

レンダリング処理は [`com.adobe.cq.dam.cfm.content.FragmentRenderService`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html) を通じて行われ、必要に応じて、（例えば）カスタムコンポーネントによって使用されます。
