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
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 58%

---

# アプリのテンプレートとコンポーネント{#app-templates-and-components}

{{ue-over-mobile}}

テンプレートはページを作成するための雛形として使用され、選択した範囲内でどのコンポーネントを使用できるかを定義します。テンプレートは、そこから作成されるページと同じ構造を持つノード階層ですが、実際のコンテンツは含みません。

テンプレートごとに、使用可能なコンポーネントが提示されます。

* テンプレートは[コンポーネント](/help/sites-developing/components.md)で構成されています。
* コンポーネントはウィジェットを使用し、ウィジェットへのアクセスを許可します。コンテンツをレンダリングするにはウィジェットが使用されます。

>[!NOTE]
>
>CRXDE Liteを使用してAdobe Experience Manager（AEM）アプリケーションを開発する方法については、[CRXDE Liteを使用した開発 ](/help/sites-developing/developing-with-crxde-lite.md) を参照してください。

テンプレートはページの基礎です。

ページを作成するには、テンプレート（ノードツリー **/apps/&lt;myapp>/templates/&lt;mytemplate>**）をサイトツリーの対応する位置にコピーする必要があります。「**web サイト**」タブを使用してページを作成する場合も、この処理がおこなわれています。

このコピー処理により、ページには、初期コンテンツ（通常はトップレベルコンテンツのみ）と sling:resourceType プロパティ、ページのレンダリングに使用するページコンポーネントのパス（子ノード jcr:content に含まれるすべてのもの）が与えられます。

## テンプレートの構造 {#structure-of-a-template}

考慮すべき側面が 2 つあります。

* テンプレート自体の構造
* テンプレートの使用時に生成されるコンテンツの構造

テンプレートは **cq:Template** タイプのノードの下に作成されます。

様々なプロパティを設定できます。主なものを以下に示します。

* **jcr:title** - テンプレートのタイトル。ページの作成時にダイアログに表示されます。
* **jcr:description** - テンプレートの説明。ページの作成時にダイアログに表示されます。

このノードには、結果ページのコンテンツノードの基礎として使用される *a jcr:content （cq:PageContent）* ノードが含まれます。 これは、*sling:resourceType* を使用して、新しいページの実際のコンテンツのレンダリングに使用するコンポーネントを参照します。

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
