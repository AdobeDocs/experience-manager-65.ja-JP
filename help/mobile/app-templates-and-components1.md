---
title: アプリのテンプレートとコンポーネント
seo-title: アプリのテンプレートとコンポーネント
description: このページでは、アプリのテンプレートとコンポーネントについて説明します。テンプレートの構造について詳しく説明します。
seo-description: このページでは、アプリのテンプレートとコンポーネントについて説明します。テンプレートの構造について詳しく説明します。
uuid: ba2fd91b-de5a-4f39-a976-5455f9983669
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: 7f31c6a7-92d5-4a87-a9f0-68a82b834d5a
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 90%

---


# アプリのテンプレートとコンポーネント{#app-templates-and-components}

>[!NOTE]
>
>単一ページアプリケーションフレームワークを基にしたクライアント側レンダリング（React など）が必要なプロジェクトでは、SPA エディターを使用することをお勧めします。[詳細情報](/help/sites-developing/spa-overview.md)

テンプレートはページを作成するための雛形として使用され、選択した範囲内で使用できるコンポーネントを定義します。テンプレートは、そこから作成されるページと同じ構造を持つノードの階層ですが、実際のコンテンツは含みません。

テンプレートごとに、使用可能なコンポーネントが提示されます。

* テンプレートは[コンポーネント](/help/sites-developing/components.md)で構成されています。
* コンポーネントによって使用され、アクセスが許可されるウィジェットを使用して、コンテンツがレンダリングされます。

>[!NOTE]
>
>To learn how to develop your AEM application using CRXDE Lite, see [Developing with CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md).

テンプレートはページの基礎です。

ページを作成するには、テンプレート（ノードツリーの **/apps/&lt;myapp>/templates/&lt;mytemplate>**）をサイトツリーの対応する位置にコピーする必要があります。「**Web サイト**」タブを使用してページを作成する場合も、この処理が行われます。

このコピー処理により、ページには、初期コンテンツ（通常はトップレベルコンテンツのみ）と sling:resourceType プロパティ、ページのレンダリングに使用するページコンポーネントのパス（子ノード jcr:content に含まれるすべてのもの）ができます。

## テンプレートの構造 {#structure-of-a-template}

以下の 2 つの側面について考慮する必要があります。

* テンプレート自体の構造
* テンプレート使用時に作成されるコンテンツの構造

テンプレートは **cq:Template** タイプのノードの下に作成されます。

様々なプロパティを設定できます。具体例は以下のとおりです。

* **jcr:title** - テンプレートのタイトル。ページ作成時にダイアログに表示されます。
* **jcr:description** - テンプレートの説明。ページ作成時にダイアログに表示されます。

このノードには、*jcr:content（cq:PageContent）*&#x200B;ノードが含まれます。jcr:content ノードは、生成されるページのコンテンツノードの基礎として使用されます。このノードは、*sling:resourceType* を使用して、新しいページの実際のコンテンツのレンダリングに使用されるコンポーネントを参照します。

>[!NOTE]
>
>AEM におけるテンプレートとコンポーネントの基礎については、以下のリソースを参照してください。
>
>* [テンプレート](/help/sites-developing/templates.md)
>* [コンポーネント](/help/sites-developing/components.md)

>



テンプレートとコンポーネントの基本的な理解ができたら、次のリソースを参照してください。

* [テンプレートとコンポーネントの作成および追加](/help/mobile/mobile-ondemand-app-templates.md)
* [コンテンツのプロパティを使用したコンテンツの書き出し](/help/mobile/on-demand-content-properties-exporting.md)
* [ベストプラクティス](/help/mobile/best-practices-aem-mobile.md)
* [AEM Mobile コンテンツサービスの開発](//help/mobile/developing-content-services.md)

### その他のリソース {#additional-resources}

モバイルアプリに関するその他のトピックについては、以下のリンクを参照してください。

* [モバイルとコンテンツ同期](/help/mobile/mobile-ondemand-contentsync.md)
* [モバイルアプリのテスト](/help/mobile/develop-mobile-apps-testing.md)

