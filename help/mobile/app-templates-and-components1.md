---
title: アプリのテンプレートとコンポーネント
description: このページでは、アプリのテンプレートとコンポーネントについて説明します。 テンプレートの構造に関する詳細情報が提供されます。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 58d95325-7cb1-4204-842d-17add70e1fbf
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 18%

---

# アプリのテンプレートとコンポーネント{#app-templates-and-components}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアントサイドレンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)。

テンプレートは、ページの作成に使用され、選択した範囲内で使用できるコンポーネントを定義します。 テンプレートは、そこから作成されるページと同じ構造を持つノードの階層ですが、実際のコンテンツは含みません。

各テンプレートには、使用可能なコンポーネントの選択が表示されます。

* テンプレートは、次の要素で構成されています [Components](/help/sites-developing/components.md);
* コンポーネントでは、ウィジェットを使用し、ウィジェットへのアクセスを許可します。このウィジェットはコンテンツのレンダリングに使用されます。

>[!NOTE]
>
>CRXDE Liteを使用してAdobe Experience Manager（AEM）アプリケーションを開発する方法については、次を参照してください。 [CRXDE Liteを使用した開発](/help/sites-developing/developing-with-crxde-lite.md).

テンプレートはページの基礎です。

ページを作成するには、テンプレートをコピーする必要があります（ノードツリー） **/apps/&lt;myapp>/templates/&lt;mytemplate>**）を選択し、サイトツリー内の対応する位置に移動します。 **Web サイト** タブ。

また、このコピーアクションは、ページの初期コンテンツ（通常はトップレベルコンテンツのみ）と、ページのレンダリングに使用されるページコンポーネントへのパスである sling:resourceType プロパティ（子ノード jcr:content 内のすべて）も提供します。

## テンプレートの構造 {#structure-of-a-template}

考慮すべき 2 つの側面があります。

* テンプレート自体の構造
* テンプレートが使用される際に生成されるコンテンツの構造

テンプレートは、タイプのノードの下に作成されます **cq:Template**.

特に、次のような様々なプロパティを設定できます。

* **jcr:title** - テンプレートのタイトル。ページの作成時にダイアログに表示されます。
* **jcr:description** - テンプレートの説明。ページの作成時にダイアログに表示されます。

このノードには *jcr:content （cq:PageContent）* 結果ページのコンテンツノードの基礎として使用されるノード。 これは、を使用して参照します *sling:resourceType*：新しいページの実際のコンテンツのレンダリングに使用されるコンポーネント。

>[!NOTE]
>
>AEMのテンプレートおよびコンポーネントの基本については、以下のリソースを参照してください。
>
>* [テンプレート](/help/sites-developing/templates.md)
>* [コンポーネント](/help/sites-developing/components.md)
>

テンプレートとコンポーネントについて基本的に理解したら、次のリソースを参照してください。

* [テンプレートとコンポーネントの作成および追加](/help/mobile/mobile-ondemand-app-templates.md)
* [コンテンツのプロパティを使用したコンテンツのエクスポート](/help/mobile/on-demand-content-properties-exporting.md)
* [ベストプラクティス](/help/mobile/best-practices-aem-mobile.md)
* [AEM Mobile コンテンツサービスの開発](/help/mobile/developing-content-services.md)

### その他のリソース {#additional-resources}

モバイルアプリに関するその他のトピックについて詳しくは、以下のリンクを参照してください。

* [モバイルとコンテンツ同期](/help/mobile/mobile-ondemand-contentsync.md)
* [モバイルアプリのテスト](/help/mobile/develop-mobile-apps-testing.md)
