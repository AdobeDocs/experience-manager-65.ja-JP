---
title: ページテンプレート - 静的
description: テンプレートは、ページの作成に使用され、選択した範囲内で使用できるコンポーネントを定義します
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
docset: aem65
exl-id: b934ac41-78b9-497f-ba95-b05ef1e5660e
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1601'
ht-degree: 43%

---

# ページテンプレート - 静的{#page-templates-static}

テンプレートは、ページの作成に使用され、選択した範囲内で使用できるコンポーネントを定義します。 テンプレートは、そこから作成されるページと同じ構造を持つノードの階層ですが、実際のコンテンツは含みません。

各テンプレートには、使用可能なコンポーネントの選択が表示されます。

* テンプレートは、次の要素で構成されています [Components](/help/sites-developing/components.md);
* コンポーネントでは、ウィジェットを使用し、ウィジェットへのアクセスを許可します。このウィジェットはコンテンツのレンダリングに使用されます。

>[!NOTE]
>
>[編集可能なテンプレート](/help/sites-developing/page-templates-editable.md) も使用できますが、これは最も柔軟性が高く、最新の機能を実現するために推奨されるタイプのテンプレートです。

## テンプレートのプロパティと子ノード {#properties-and-child-nodes-of-a-template}

テンプレートは cq:Template タイプのノードで、次のプロパティと子ノードを持っています。

<table>
 <tbody>
  <tr>
   <td><strong>名前 <br /> </strong></td>
   <td><strong>種類 <br /> </strong></td>
   <td><strong>説明 <br /> </strong></td>
  </tr>
  <tr>
   <td>. <br /> </td>
   <td> cq:Template</td>
   <td>現在のテンプレートです。 テンプレートのノードタイプは cq:Template です。<br /> </td>
  </tr>
  <tr>
   <td> allowedChildren </td>
   <td> String[]</td>
   <td>このテンプレートの子となることが許可されているテンプレートのパス。<br /> </td>
  </tr>
  <tr>
   <td> allowedParents</td>
   <td> String[]</td>
   <td>このテンプレートの親となることが許可されているテンプレートのパス。<br /> </td>
  </tr>
  <tr>
   <td> allowedPaths</td>
   <td> String[]</td>
   <td>このテンプレートをベースとすることが許可されているページのパス。<br /> </td>
  </tr>
  <tr>
   <td> jcr:created</td>
   <td> 日付</td>
   <td>テンプレートの作成日。<br /> </td>
  </tr>
  <tr>
   <td> jcr:description</td>
   <td> 文字列</td>
   <td>テンプレートの説明。<br /> </td>
  </tr>
  <tr>
   <td> jcr:title</td>
   <td> 文字列</td>
   <td>テンプレートのタイトル。<br /> </td>
  </tr>
  <tr>
   <td> ranking</td>
   <td> Long</td>
   <td>テンプレートのランクです。ユーザーインターフェイスにテンプレートを表示する際に使用します。<br /> </td>
  </tr>
  <tr>
   <td> jcr:content</td>
   <td> cq:PageContent</td>
   <td>テンプレートのコンテンツを含むノード。<br /> </td>
  </tr>
  <tr>
   <td> thumbnail.png</td>
   <td> nt:file</td>
   <td>テンプレートのサムネール。<br /> </td>
  </tr>
  <tr>
   <td> icon.png</td>
   <td> nt:file</td>
   <td>テンプレートのアイコン。<br /> </td>
  </tr>
 </tbody>
</table>

テンプレートはページの基礎です。

ページを作成するには、テンプレート（ノードツリー `/apps/<myapp>/template/<mytemplate>`）をサイトツリーの対応する位置にコピーする必要があります。「**Web サイト**」タブを使用してページを作成する場合も、この処理がおこなわれています。

また、このコピーアクションは、ページの初期コンテンツ（通常はトップレベルコンテンツのみ）と、ページのレンダリングに使用されるページコンポーネントへのパスである sling:resourceType プロパティ（子ノード jcr:content 内のすべて）も提供します。

## テンプレートの構造 {#how-templates-are-structured}

考慮すべき 2 つの側面があります。

* テンプレート自体の構造
* テンプレートが使用される際に生成されるコンテンツの構造

### テンプレートの構造 {#the-structure-of-a-template}

テンプレートは、タイプのノードの下に作成されます **cq:Template**.

![screen_shot_2012-02-13at63646pm](assets/screen_shot_2012-02-13at63646pm.png)

特に、次のような様々なプロパティを設定できます。

* **jcr:title** - テンプレートのタイトル。ページの作成時にダイアログに表示されます。
* **jcr:description** - テンプレートの説明。ページの作成時にダイアログに表示されます。

このノードには、結果ページのコンテンツノードの基礎として使用される jcr:content （cq:PageContent）ノードが含まれます。これは、sling:resourceType を使用して、新しいページの実際のコンテンツのレンダリングに使用されるコンポーネントを参照します。

![screen_shot_2012-02-13at64010pm](assets/screen_shot_2012-02-13at64010pm.png)

このコンポーネントは、新しいページを作成する際に、コンテンツの構造およびデザインを定義するために使用します。

![screen_shot_2012-02-13at64137pm](assets/screen_shot_2012-02-13at64137pm.png)

### テンプレートによって作成されるコンテンツ {#the-content-produced-by-a-template}

テンプレートは、`cq:Page` タイプのページを作成するのに使用します（前述のように、ページは特別なタイプのコンポーネントです）。各 AEM ページには構造化ノード `jcr:content` があります。この特徴は次のとおりです。

* cq:PageContent タイプです
* 定義済みのコンテンツ定義を保持する構造化ノードタイプ
* コンテンツのレンダリングに使用する Sling スクリプトを保持するコンポーネントを参照するための `sling:resourceType` プロパティを持つ。

### デフォルトのテンプレート {#default-templates}

AEMには、すぐに使用できる様々なデフォルトテンプレートが付属しています。 場合によっては、テンプレートをそのまま使用する必要があります。 その場合、テンプレートを web サイトで使用できるようにする必要があります。

例えば、AEMには、コンテンツページとホームページを含む、複数のテンプレートが付属しています。

| **タイトル** | **コンポーネント** | **場所** | **目的** |
|---|---|---|---|
| ホームページ | homepage | geometrixx | Geometrixxのホームページテンプレート。 |
| コンテンツページ | contentpage | geometrixx | Geometrixxコンテンツページテンプレート。 |

#### デフォルトのテンプレートの表示 {#displaying-default-templates}

リポジトリ内のすべてのテンプレートのリストを表示するには、次の手順を実行します。

1. CRXDE Liteーで、 **ツール** メニューとクリック **クエリ**.

1. 「クエリ」タブで、次の手順を実行します
1. As **タイプ**&#x200B;を選択 **XPath**.

1. が含まれる **クエリ** 入力フィールドに次の文字列を入力：//element （&#42;, cq:Template）

1. クリック **実行**. リストが結果ボックスに表示されます。

通常は、既存のテンプレートを使用して、各自の用途に合わせて新しいテンプレートを開発します。 参照： [ページテンプレートの開発](#developing-page-templates) を参照してください。

既存のテンプレートを各自の web サイト用に有効にし、**web サイト**&#x200B;コンソールから「**Web サイト**」のすぐ下にページを作成するときに&#x200B;**ページを作成**&#x200B;ダイアログにそのテンプレートを表示する場合は、テンプレートノードの allowedPaths プロパティを次のように設定します。**/content(/.&#42;）?**

## テンプレートデザインの適用方法 {#how-template-designs-are-applied}

UI でスタイルが[デザインモード](/help/sites-authoring/default-components-designmode.md)を使用して定義されている場合、デザインは、スタイルが定義されているコンテンツノードの正確なパスに保持されます。

>[!CAUTION]
>
>Adobeでは、[デザインモード](/help/sites-authoring/default-components-designmode.md) を介してのみデザインを適用することをお勧めします。
>
>例えば、CRXDE Liteでデザインを変更することはベストプラクティスではなく、そのようなデザインの適用は、意図したビヘイビアーとは異なることがあります。

デザインがデザインモードを使用してのみ適用される場合、次のセクションは、 [デザインパスの解像度](/help/sites-developing/page-templates-static.md#design-path-resolution)、[デシジョンツリー](/help/sites-developing/page-templates-static.md#decision-tree)、および[例](/help/sites-developing/page-templates-static.md#example)は適用されません。

### デザインパスの解像度 {#design-path-resolution}

静的テンプレートに基づいてコンテンツをレンダリングする場合、AEMはコンテンツ階層のトラバーサルに基づいて、最も関連性の高いデザインとスタイルをコンテンツに適用しようとします。

AEM は次の順序で、コンテンツノードに最も関連性の高いスタイルを決定します。

* （デザインモードでデザインが定義されている場合と同様に）コンテンツノードのフルパスと正確なパスのデザインがある場合には、そのデザインを使用します。
* 親のコンテンツノードにデザインがある場合は、そのデザインを使用します。
* コンテンツノードのパス上に任意のノードのデザインがある場合は、そのデザインを使用します。

最後の 2 つのケースで、適用可能なデザインが複数ある場合は、コンテンツノードに最も近いものを使用します。

### デシジョンツリー {#decision-tree}

これは[デザインパスの解像度](/help/sites-developing/page-templates-static.md#design-path-resolution)を図で表現したものです。

![design_path_resolution](assets/design_path_resolution.png)

### 例 {#example}

デザインを任意のノードに適用できる場合、シンプルなコンテンツ構造を次のように考えてみます。

`/root/branch/leaf`

次の表に、AEMでのデザインの選択方法を示します。

<table>
 <tbody>
  <tr>
   <td><strong>デザインの検索<br /> </strong></td>
   <td><strong>存在するデザイン<br /> </strong></td>
   <td><strong>選択したデザイン<br /> </strong></td>
   <td><strong>コメント</strong></td>
  </tr>
  <tr>
   <td><code class="code">leaf
      </code></td>
   <td><p><code>root</code></p> <p><code>branch</code></p> <p><code>leaf</code></p> </td>
   <td><code>leaf</code></td>
   <td>最も正確に一致するものが常に取得されます。<br /> </td>
  </tr>
  <tr>
   <td><code>leaf</code></td>
   <td><p><code>root</code></p> <p><code>branch</code></p> </td>
   <td><code>branch</code></td>
   <td>ツリー下部の最も近いマッチにフォールバックします。</td>
  </tr>
  <tr>
   <td><code>leaf</code></td>
   <td><code>root</code></td>
   <td><code>root</code></td>
   <td>他のすべてが失敗した場合は、残りのものを取得します。<br /> </td>
  </tr>
  <tr>
   <td><code>branch</code></td>
   <td><code>branch</code></td>
   <td><code>branch</code></td>
   <td> </td>
  </tr>
  <tr>
   <td><code>branch</code></td>
   <td><p><code>branch</code></p> <p><code class="code">leaf
       </code></p> </td>
   <td><code>branch</code></td>
   <td> </td>
  </tr>
  <tr>
   <td><code>branch</code></td>
   <td><p><code>root</code></p> <p><code class="code">branch
       </code></p> </td>
   <td><code>branch</code></td>
   <td> </td>
  </tr>
  <tr>
   <td><code>branch</code></td>
   <td><p><code>root</code></p> <p><code class="code">leaf
       </code></p> </td>
   <td><code>root</code></td>
   <td><p>完全に一致しない場合は、ツリーの 1 つ下のものを選択します。</p> <p>これは常に適用できるが、ツリーの上の方は具体的すぎる可能性があると仮定します。<br /> </p> </td>
  </tr>
 </tbody>
</table>

## ページテンプレートの開発 {#developing-page-templates}

AEM ページテンプレートは、ページの作成に使用する単純なモデルです。 必要に応じて初期コンテンツをいくつでも含めることができます。役割は、正しい初期ノード構造を作成し、必要なプロパティ（主に sling:resourceType）を設定して編集とレンダリングを可能にすることです。

### テンプレートの作成（既存のテンプレートに基づく） {#creating-a-new-template-based-on-an-existing-template}

新しいテンプレートは最初から完全に作成できますが、多くの場合、代わりに既存のテンプレートがコピーされ、更新されて時間と労力が節約されます。 例えば、Geometrixx内のテンプレートを使用して作業を開始できます。

既存のテンプレートに基づいてテンプレートを作成するには：

1. 既存のテンプレート（できれば、目的の定義にできるだけ近い定義で）を新しいノードにコピーします。

   テンプレートは次の場所に保存されます。 **/apps/&lt;website-name>/templates/&lt;template-name>**.

   >[!NOTE]
   >
   >使用可能なテンプレートのリストは、新しいページの場所と、各テンプレートで指定されている配置制限によって異なります。 参照： [テンプレートの可用性](#templateavailibility).

1. 変更： **jcr:title** （新しい役割を反映する新しいテンプレートノード）。 を更新することもできます **jcr:description** （該当する場合）。 ページのテンプレートの使用可否を適宜変更してください。

   >[!NOTE]
   >
   >**Web サイト** コンソールから **Web サイト** のすぐ下にページを作成するときに **ページを作成** ダイアログにテンプレートを表示する場合は、 `allowedPaths`テンプレートノードのプロパティを、`/content(/.*)?`に設定します。

   ![chlimage_1-88](assets/chlimage_1-88.png)

1. テンプレートのベースとなるコンポーネントをコピーします（コンポーネントは **sling:resourceType** のプロパティ **jcr:content** ノードを含む）を選択して、インスタンスを作成します。

   コンポーネントは次の場所に保存されています。 **/apps/&lt;website-name>/components/&lt;component-name>**.

1. を更新 **jcr:title** および **jcr:description** 新しいコンポーネント
1. 新しいサムネール画像をテンプレート選択リスト（サイズ 128 x 98 ピクセル）に表示する場合は、thumbnail.png を置き換えます。
1. を更新 **sling:resourceType** （テンプレートの） **jcr:content** 新しいコンポーネントを参照するノード。
1. テンプレートの機能やデザイン、基盤となるコンポーネントまたはその両方に追加の変更を加えます。

   >[!NOTE]
   >
   >に加えた変更 **/apps/&lt;website>/templates/&lt;template-name>** ノードが（選択リスト内のように）テンプレートインスタンスに影響を与える。
   >
   >
   に加えた変更 **/apps/&lt;website>/components/&lt;component-name>** ノードは、テンプレートの使用時に作成されるコンテンツページに影響します。

   これで、新しいテンプレートを使用して web サイト内にページを作成できます。

>[!NOTE]
>
エディタークライアントライブラリは、 `cq.shared` コンテンツページの名前空間、ない場合は JavaScript エラー `Uncaught TypeError: Cannot read property 'shared' of undefined` 件の結果。
>
すべてのサンプルコンテンツページには `cq.shared` が含まれているので、それらをベースとするコンテンツには自動的に `cq.shared` が含められます。ただし、サンプルコンテンツをベースとせず、ゼロから独自のコンテンツページを作成する場合は、`cq.shared` 名前空間を含める必要があります。
>
詳しくは、[クライアントサイドライブラリの使用](/help/sites-developing/clientlibs.md)を参照してください。

## 既存のテンプレートを使用可能にする {#making-an-existing-template-available}

この例では、特定のコンテンツパスに対してテンプレートを使用できるようにする方法を示します。 ページ作成者がページの作成時に使用できるテンプレートは、で定義されたロジックによって決まります。 [テンプレートの可用性](/help/sites-developing/templates.md#template-availability).

1. CRXDE Lite で、ページに使用するテンプレート（ニュースレターテンプレートなど）に移動します。
1. 変更： `allowedPaths` に使用されるプロパティとその他のプロパティ [テンプレートの可用性](/help/sites-developing/templates.md#template-availability). 例えば `allowedPaths`: `/content/geometrixx-outdoors/[^/]+(/.*)?` は、このテンプレートが `/content/geometrixx-outdoors` 以下の任意のパスで許可されることを意味します。

   ![chlimage_1-89](assets/chlimage_1-89.png)
