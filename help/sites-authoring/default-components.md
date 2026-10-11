---
title: デフォルトコンポーネント
description: Adobe Experience Manager には、すぐに使用できる様々なコンポーネントが付随しており、web サイト作成者に包括的な機能を提供します。
exl-id: 85463610-8461-4c1f-bfe7-72229a31ea40
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: e2c1b6d3-bb7e-4fe8-8c72-f7b403298e91
    internal-label: Authoring
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 97%
---
# コンポーネント{#components}

Adobe Experience Manager（AEM）には、すぐに使用できる様々なコンポーネントが付随しており、web サイト作成者に包括的な機能を提供します。 これらの機能は、[ページの編集](/help/sites-authoring/editing-content.md)時に使用でき、フィルタリングのために主な機能領域（コンポーネントグループと呼ばれます）でグループ化されています。

コンポーネントは、[ページの編集](/help/sites-authoring/editing-content.md)時に使用できます。 フィルタリングを容易にするために、コンポーネントは主要な機能領域（コンポーネントグループ）でグループ化されています。

>[!NOTE]
>
>ここでは、標準の AEM インストールでそのまま使用できるコンポーネントについてのみ説明します。
>
>インスタンスによっては、要件に合わせて明示的に開発されたカスタムコンポーネントが存在する場合があります。 これらは、ここで説明するいくつかのコンポーネントと同じ名前の場合があります。

## 一般的な使用方法 {#general-usage}

コンポーネントは、[ページの編集](/help/sites-authoring/editing-content.md)時に、ページエディターのサイドパネルにある「**コンポーネント**」タブで使用できます。

コンポーネントを選択し、ページ上の必要な場所にドラッグできます。 その後、次の機能を使用して編集できます。

* [プロパティの設定](/help/sites-authoring/editing-page-properties.md)
* [コンテンツの編集](/help/sites-authoring/editing-content.md)

* [コンテンツの編集 - 全画面表示モード](/help/sites-authoring/editing-content.md#edit-content-full-screen-mode)

ページへのコンポーネントの追加について詳しくは、[ページコンテンツの編集](/help/sites-authoring/editing-content.md)を参照してください。
コンポーネントは、コンポーネントグループと呼ばれる様々なカテゴリーに従って並べ替えられます。 このようなコンポーネントグループの例を次に示します。

* **We.Retail**：[We.Retail 参照実装](/help/sites-developing/we-retail.md)で使用するためにプロキシ設定されたコアコンポーネントが含まれています。

* **We.Retail コマース**：買い物かごや商品グリッドなどのコマースコンポーネントが含まれています。

* **一般**：レイアウトコンテナやエクスペリエンスフラグメントが含まれています。

## 全コンポーネントの概要 {#overview-of-all-components}

[コンポーネントコンソール](/help/sites-authoring/default-components-console.md)では、インストールした AEM から提供されるコンポーネントグループとコンポーネントの概要を確認できます。 個々のコンポーネントとその使用方法に関する主な情報を確認できます。

## コンポーネント - 主な領域 {#components-major-areas}

次のページには、コンポーネントに関する重要な追加情報へのリンクが記載されています。

* [コアコンポーネント](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ja) - コアコンポーネントは柔軟かつ機能豊富なオーサリング機能を提供します。ページを作成するうえで不可欠なコンテンツタイプが用意されています。

* [コミュニティ](/help/communities/author-communities.md) - コンポーネントには、web サイトのインタラクティブな機能（フォーラムやコメントなど）が用意されています。 このコンポーネントの多くは[コミュニティサイト](/help/communities/overview.md)の作成時に追加されます。

* [e コマース &#x200B;](/help/commerce/cif-classic/administering/ecommerce.md) - AEMのe コマース機能には、さまざまなコンポーネントも含まれています。 実際の使用方法は、使用しているコマースエンジンによって異なります。

### コンポーネントの設定 {#configuring-components}

作成者が標準インストールからアクセスできるコンポーネントに加えて、他の様々なコンポーネントも使用できます。

* ページが最新の編集可能な推奨テンプレートに基づいている場合は、[テンプレートを編集](/help/sites-authoring/templates.md)して、コンポーネントを有効／無効にしたり、特定のコンポーネントのパラメーターを編集したりできます。
* ページが静的テンプレートに基づいている場合は、[デザインモード](/help/sites-authoring/default-components-designmode.md#enable-disable-components)を使用して、コンポーネントを有効／無効にしたり、特定のコンポーネントのパラメーターを編集したりできます。
