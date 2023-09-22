---
title: コンテンツフラグメント用コンポーネント
description: Adobe Experience Manager(AEM) のコンテンツフラグメントは、ページに依存しないアセットとして作成および管理されます
contentOwner: AEM Docs
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
docset: aem65
pagetitle: Components for Content Fragments
exl-id: f2edd9b2-f231-42f3-a25e-428cd1d96c2a
source-git-commit: b66ec42c35b5b60804015d340b8194bbd6ef3e28
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 35%

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
>The [コンテンツフラグメントコアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/content-fragment-component.html?lang=ja) が推奨されました。 詳しくは、 [コアコンポーネントの開発](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/overview.html?lang=ja) を参照してください。
>
>この節では、コンテンツフラグメントで使用するために配信される元のコンポーネント (**コンテンツフラグメント** （内） **一般** グループ ) です。

>[!NOTE]
>
>詳しくは、[レンダリングコンポーネントのコンテンツフラグメントの設定](/help/sites-developing/content-fragments-config-components-rendering.md)も参照してください。

Adobe Experience Manager（AEM）のコンテンツフラグメントは、[ページに依存しないアセットとして作成および管理](/help/assets/content-fragments/content-fragments.md)されます。チャネルに特化しないコンテンツを、チャネル固有のバリエーションと共に作成できます。 [その後、コンテンツページをオーサリングする際に、これらのフラグメントとそのバリエーションを使用できます](/help/sites-authoring/content-fragments.md). また、既存のコンテンツフラグメントアセットを使用する場合は、 [アセットブラウザーからページにドラッグする](/help/sites-authoring/content-fragments.md#adding-a-content-fragment-to-your-page) （基盤コンポーネントの画像など、他のアセットベースのコンポーネントについて） 既製のコンテンツフラグメントコンポーネントには、参照されているコンテンツフラグメントの[要素](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment)が 1 つだけ表示されます。ページ上に表示する[要素、バリエーションおよびフラグメント段落の範囲](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment)は、コンポーネントダイアログで定義できます。

>[!NOTE]
>
>このコンテンツフラグメントコンポーネントは、廃止された記事コンポーネントの拡張バージョンとしてAEM 6.2 で導入されました。

>[!NOTE]
>
>コンテンツフラグメントは、クラシック UI ではサポートされていません。

### 定義 {#definition}

The **コンテンツフラグメント** コンポーネントは、コンテンツフラグメントアセット（効果的に拡張されたテキストアセット）への参照を保持するために使用されます。 コンテンツフラグメントのリソースタイプは次のとおりです。

`dam/cfm/components/contentfragment/contentfragment`

参照を定義するには、次のプロパティを使用します。

`fileReference`

次に示すクライアントライブラリを含むコンテンツフラグメントコンポーネントを完全にサポートするのは、タッチ操作対応 UI のエディターだけです。

`cq.authoring.editor.plugin.cfm`

このライブラリは、コンテンツフラグメント専用の機能をエディターに追加します。 例えば、ページ上でコンテンツフラグメントを追加および設定する機能、アセットブラウザーでコンテンツフラグメントアセットを検索する機能、サイドパネルで関連コンテンツを検索する機能をサポートできます。

### 中間コンテンツ {#in-between-content}

The **コンテンツフラグメント** t コンポーネントを使用すると、表示される異なる段落の間に追加のコンポーネントをドロップできます [要素](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment). 基本的に、表示される要素は異なる段落で構成されます（各段落はキャリッジリターンでマークされます）。 これらの各段落の間に、他のコンポーネントを使用してコンテンツを挿入できます。

技術的な観点から、表示された要素の各段落はそれぞれ独自の parsys に存在し、段落の間に追加する各コンポーネントは（内部で）parsys に挿入されます。

つまり、コンテンツフラグメントコンポーネントのインスタンスが 3 つの段落で構成されている場合、そのコンポーネントはリポジトリ内に 3 つの異なる parsys を持ちます。 コンテンツフラグメントに追加される中間コンテンツは、実際にはこれらの parsys 内に配置されます。

リポジトリ内では、中間コンテンツは、段落構造全体内の位置を基準に格納されます。つまり、中間コンテンツは実際の段落コンテンツには添付されません。

この点を説明するために、次の点に注意してください。

* コンテンツフラグメントのインスタンスが 3 つの段落で構成されている
* また、2 番目の段落の後に既に一部のコンテンツが挿入されています。

   * つまり、コンテンツは 2 番目の parsys に保存されます。

基本的に、このインスタンスの段落構造を変更した場合は（表示される段落のバリエーション、要素または範囲を変更するなど）、表示される中間コンテンツに影響が及びます。例えば次の場合が考えられます。

* コンテンツフラグメントコンポーネントが編集され、2 番目の段落の前に別の段落が追加される：

   * 中間コンテンツは、新しく作成された段落の後に表示されます（2 番目の parsys には新しく作成された段落が格納されます）。

* コンテンツフラグメントコンポーネントが編集され、2 番目の段落が削除される：

   * 中間コンテンツは、以前は 3 番目だった段落の後に表示されます（2 番目の parsys が前の 3 番目の段落を保持するようになりました）。

* 最初の段落だけを表示するようにコンテンツフラグメントコンポーネントが設定される：

   * 中間コンテンツは表示されません（新しい設定により、2 番目の parsys はレンダリングされなくなりました）。

### コンテンツフラグメントコンポーネントのカスタマイズ {#customizing-the-content-fragment-component}

標準搭載のコンテンツフラグメントコンポーネントを拡張機能のブループリントとして使用するには、次の契約に従う必要があります。

* HTL レンダリングスクリプトとそれに関連する POJO を再利用して、中間コンテンツ機能の実装方法を確認できます。
* コンテンツフラグメントノード `cq:editConfig` を再利用します。

   *  `afterinsert`／`afteredit`／`afterdelete` リスナーを使用して JS イベントを呼び出します。これらのイベントは、 `cq.authoring.editor.plugin.cfm` 関連するコンテンツをサイドパネルに表示するクライアントライブラリ。
   * コンテンツフラグメントアセットのドラッグをサポートするように `cq:dropTargets` を設定します。
   * ページエディターでコンテンツフラグメントのオーサリングをサポートするように `cq:inplaceEditing` を設定します。フラグメントのインプレースエディターは `cq.authoring.editor.plugin.cfm` クライアントライブラリで定義され、クイックリンクによって現在の[要素／バリエーション](/help/assets/content-fragments/content-fragments.md#constituent-parts-of-a-content-fragment)を[フラグメントエディター](/help/assets/content-fragments/content-fragments-variations.md)で開けるようにします。

### レンダリング前のアセットの書き換え {#asset-rewriting-before-rendering}

コンテンツフラグメント管理では、内部レンダリングプロセスを使用して、ページの最終HTML出力を生成します。 これは、コンテンツフラグメントコンポーネントによって内部的に使用されるだけでなく、参照ページ上の参照フラグメントを更新するバックグラウンドプロセスによっても使用されます。

内部では、このレンダリングに Sling Rewriter を使用します。それぞれの設定は、次の場所にあります。 `/libs/dam/config/rewriter/cfm` 必要に応じて調整できます。 詳しくは、[Apache Sling Rewriter](https://sling.apache.org/documentation/bundles/output-rewriting-pipelines-org-apache-sling-rewriter.html) を参照してください。

>[!CAUTION]
>
>リライターの設定を調整／オーバーレイする場合：
>
>* `/libs/dam/config/rewriter/cfm`
>
>次に、 `serializerType` **必須** 更新先：
>
>* `serializerType="html5-serializer"`

既製の設定は、次の変換サービスを使用します。

* `transformer-cfm-payloadfilter` - フラグメントの HTML の `body` 部分（`<body>...</body>`）の取得用のみ

* `transformer-cfm-parfilter` - 段落範囲が指定されている場合に、不要な段落を除外します（コンテンツフラグメントコンポーネントで実行可能）
* `transformer-cfm-assetprocessor` - フラグメントに埋め込まれたアセットのリストを取得するために内部で使用されます

レンダリングプロセスは、を通じて公開されます。 [`com.adobe.cq.dam.cfm.content.FragmentRenderService`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/dam/cfm/ContentFragment.html) 必要に応じて、カスタムコンポーネントで（例えば）使用できます。
