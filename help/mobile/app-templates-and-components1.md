---
title: アプリのテンプレートとコンポーネント
description: このページでは、アプリテンプレートとコンポーネントについて説明します。 テンプレートの構造に関する詳細な情報を提供します。
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: 58d95325-7cb1-4204-842d-17add70e1fbf
solution: Experience Manager
feature: Mobile
role: User
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 38%
---
# アプリのテンプレートとコンポーネント{#app-templates-and-components}

{{ue-over-mobile}}

テンプレートはページを作成するための雛形として使用され、選択した範囲内でどのコンポーネントを使用できるかを定義します。 テンプレートは、そこから作成されるページと同じ構造を持つノード階層ですが、実際のコンテンツは含みません。

テンプレートごとに、使用可能なコンポーネントが提示されます。

* テンプレートは[コンポーネント](/help/sites-developing/components.md)で構成されています。
* コンポーネントはウィジェットを使用し、ウィジェットへのアクセスを許可します。コンテンツをレンダリングするにはウィジェットが使用されます。

>[!NOTE]
>
>CRXDE Liteを使用してAdobe Experience Manager （AEM） アプリケーションを開発する方法については、[CRXDE Liteを使用した開発](/help/sites-developing/developing-with-crxde-lite.md)を参照してください。

テンプレートはページの基礎です。

ページを作成するには、テンプレートをサイトツリーの対応する位置にコピーする必要があります（node-tree **/apps/&lt;myapp>/templates/&lt;mytemplate>**）。これは、**Web サイト** タブを使用してページを作成した場合に発生します。

このコピーアクションは、ページに最初のコンテンツ（通常はトップレベルのコンテンツのみ）と、ページのレンダリングに使用されるページコンポーネント（子ノード jcr:content内のすべての）へのパスであるプロパティ sling:resourceTypeも与えます。

## テンプレートの構造 {#structure-of-a-template}

考慮すべき側面が 2 つあります。

* テンプレート自体の構造
* テンプレートの使用時に生成されるコンテンツの構造

テンプレートは、**cq:Template**&#x200B;型のノードの下に作成されます。

様々なプロパティを設定できます。主なものを以下に示します。

* **jcr:title** - テンプレートのタイトル。ページ作成時にダイアログに表示されます。
* **jcr:description** - テンプレートの説明。ページの作成時にダイアログに表示されます。

このノードには、結果ページのコンテンツノードのベースとして使用される&#x200B;*a jcr:content （cq:PageContent）* ノードが含まれています。 これは、*sling:resourceType*&#x200B;を使用して、新しいページの実際のコンテンツのレンダリングに使用するコンポーネントを参照します。

>[!NOTE]
>
>AEMのテンプレートとコンポーネントの基本については、次のリソースを参照してください。
>
>* [テンプレート](/help/sites-developing/templates.md)
>* [コンポーネント](/help/sites-developing/components.md)
>

テンプレートとコンポーネントの基本を理解したら、次のリソースを参照してください。

* [テンプレートとコンポーネントの作成および追加](/help/mobile/mobile-ondemand-app-templates.md)
* [コンテンツのプロパティを使用したコンテンツのエクスポート](/help/mobile/on-demand-content-properties-exporting.md)
* [ベストプラクティス](/help/mobile/best-practices-aem-mobile.md)
* [AEM Mobileコンテンツサービスの開発](/help/mobile/developing-content-services.md)

### その他のリソース {#additional-resources}

モバイルアプリに関するその他のトピックについては、以下のリンクを参照してください。

* [モバイルとコンテンツ同期](/help/mobile/mobile-ondemand-contentsync.md)
* [モバイルアプリのテスト](/help/mobile/develop-mobile-apps-testing.md)
