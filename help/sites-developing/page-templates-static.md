---
title: ページテンプレート - 静的
description: テンプレートはページの作成に使用され、選択した範囲内でどのコンポーネントが使用可能かを定義します
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
ht-degree: 100%

---

# ページテンプレート - 静的{#page-templates-static}

テンプレートはページを作成するための雛形として使用され、選択した範囲内でどのコンポーネントを使用できるかを定義します。テンプレートは、そこから作成されるページと同じ構造を持つノード階層ですが、実際のコンテンツは含みません。

テンプレートごとに、使用可能なコンポーネントが提示されます。

* テンプレートは[コンポーネント](/help/sites-developing/components.md)で構成されています。
* コンポーネントはウィジェットを使用し、ウィジェットへのアクセスを許可します。コンテンツをレンダリングするにはウィジェットが使用されます。

>[!NOTE]
>
>[編集可能なテンプレート](/help/sites-developing/page-templates-editable.md) も使用できますが、これは最も柔軟性が高く、最新の機能を実現するために推奨されるタイプのテンプレートです。

## テンプレートのプロパティと子ノード {#properties-and-child-nodes-of-a-template}

テンプレートは、cq:Template タイプのノードで、以下のプロパティと子ノードを含んでいます。

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

このコピー処理により、ページには、初期コンテンツ（通常はトップレベルコンテンツのみ）と sling:resourceType プロパティ、ページのレンダリングに使用するページコンポーネントのパス（子ノード jcr:content に含まれるすべてのもの）が与えられます。

## テンプレートの構造 {#how-templates-are-structured}

考慮すべき側面が 2 つあります。

* テンプレート自体の構造
* テンプレートの使用時に生成されるコンテンツの構造

### テンプレートの構造 {#the-structure-of-a-template}

テンプレートは **cq:Template** タイプのノードの下に作成されます。

![screen_shot_2012-02-13at63646pm](assets/screen_shot_2012-02-13at63646pm.png)

様々なプロパティを設定できます。主なものを以下に示します。

* **jcr:title** - テンプレートのタイトル。ページの作成時にダイアログに表示されます。
* **jcr:description** - テンプレートの説明。ページの作成時にダイアログに表示されます。

このノードには jcr:content（cq:PageContent）ノードが含まれており、結果ページのコンテンツノードの基礎として使用できます。これが、sling:resourceType を使用して、新しいページの実際のコンテンツをレンダリングする際に使用するコンポーネントを参照します。

![screen_shot_2012-02-13at64010pm](assets/screen_shot_2012-02-13at64010pm.png)

このコンポーネントは、新しいページを作成する際に、コンテンツの構造およびデザインを定義するために使用します。

![screen_shot_2012-02-13at64137pm](assets/screen_shot_2012-02-13at64137pm.png)

### テンプレートによって作成されるコンテンツ {#the-content-produced-by-a-template}

テンプレートは、`cq:Page` タイプのページを作成するのに使用します（前述のように、ページは特別なタイプのコンポーネントです）。各 AEM ページには構造化ノード `jcr:content` があります。この特徴は次のとおりです。

* タイプが cq:PageContent である。
* 定義済みのコンテンツ定義を保持する構造化ノードタイプである。
* コンテンツのレンダリングに使用する Sling スクリプトを保持するコンポーネントを参照するための `sling:resourceType` プロパティを持つ。

### デフォルトのテンプレート {#default-templates}

AEM には、様々なデフォルトテンプレートが標準提供されています。場合によっては、テンプレートをそのまま使用することもできます。その場合は、テンプレートが目的の web サイトで使用できることを確認する必要があります。

例えば、AEM には、コンテンツページやホームページを含む、いくつかのテンプレートが付属しています。

| **タイトル** | **コンポーネント** | **場所** | **目的** |
|---|---|---|---|
| ホームページ | homepage | geometrixx | Geometrixx ホームページテンプレート。 |
| コンテンツページ | contentpage | geometrixx | Geometrixx コンテンツページテンプレート。 |

#### デフォルトテンプレートの表示 {#displaying-default-templates}

リポジトリ内のすべてのテンプレートのリストを確認するには、以下の手順を実行します。

1. CRXDE Lite で、**ツール**&#x200B;メニューを開いて、「**クエリ**」をクリックします。

1. 「クエリ」タブで、
1. 「**タイプ**」として「**XPath**」を選択します。

1. 「**クエリ**」入力フィールドに次の文字列を入力します。
//element(&#42;, cq:Template)

1. 「**実行**」をクリックします。結果ボックスにリストが表示されます。

通常は、既存のテンプレートを使用し、独自の用途に新しいテンプレートを開発します。詳しくは、[ページテンプレートの開発](#developing-page-templates)を参照してください。

既存のテンプレートを各自の web サイト用に有効にし、**web サイト**&#x200B;コンソールから「**Web サイト**」のすぐ下にページを作成するときに&#x200B;**ページを作成**&#x200B;ダイアログにそのテンプレートを表示する場合は、テンプレートノードの allowedPaths プロパティを次のように設定します。**/content(/.&#42;)?**

## テンプレートデザインの適用方法 {#how-template-designs-are-applied}

UI でスタイルが[デザインモード](/help/sites-authoring/default-components-designmode.md)を使用して定義されている場合、デザインは、スタイルが定義されているコンテンツノードの正確なパスに保持されます。

>[!CAUTION]
>
>Adobeでは、[デザインモード](/help/sites-authoring/default-components-designmode.md) を介してのみデザインを適用することをお勧めします。
>
>例えば、CRXDE Lite でデザインを変更することはベストプラクティスではなく、そのようなデザインの適用は、意図したビヘイビアーとは異なることがあります。

デザインがデザインモードを使用してのみ適用される場合、次のセクションは、 [デザインパスの解像度](/help/sites-developing/page-templates-static.md#design-path-resolution)、[デシジョンツリー](/help/sites-developing/page-templates-static.md#decision-tree)、および[例](/help/sites-developing/page-templates-static.md#example)は適用されません。

### デザインパスの解像度 {#design-path-resolution}

静的テンプレートに基づいてコンテンツをレンダリングする場合、AEM は コンテンツ階層のトラバーサルに基づいて、最も関連性の高いデザインとスタイルをコンテンツに適用しようとします。

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

AEM がデザインを選択する方法を次の表に示します。

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

AEM のページテンプレートは、ページの作成に使用されるモデルにすぎません。初期コンテンツは必要に応じて増減できます。テンプレートの役割は、編集やレンダリングが可能なように必要なプロパティ（主に sling:resourceType）が設定された、正しい初期ノード構造を作成することです。

### テンプレートの作成（既存のテンプレートを使用） {#creating-a-new-template-based-on-an-existing-template}

新しいテンプレートは完全にゼロから作成できますが、多くの場合は、既存のテンプレートをコピーし更新して、時間と労力を節約します。例えば、Geometrixx 内のテンプレートを使用して作業を開始できます。

既存のテンプレートに基づいてテンプレートを作成するには：

1. 既存のテンプレート（作成したいテンプレートに定義が最も近いものが望ましい）を、新しいノードにコピーします。

   テンプレートは **/apps/&lt;web サイト名>/templates/&lt;テンプレート名>** に格納されています。

   >[!NOTE]
   >
   >使用可能なテンプレートのリストは、新しいページの場所と、各テンプレートで指定されている配置制限によって異なります。詳しくは、[使用可能なテンプレート](#templateavailibility)を参照してください。

1. 新しいテンプレートノードの **jcr:title** を、新しい役割を反映するものに変更します。また、必要に応じて **jcr:description** も更新します。必要に応じて、ページの使用可能なテンプレートを必ず変更してください。

   >[!NOTE]
   >
   >**Web サイト** コンソールから **Web サイト** のすぐ下にページを作成するときに **ページを作成** ダイアログにテンプレートを表示する場合は、 `allowedPaths`テンプレートノードのプロパティを、`/content(/.*)?`に設定します。

   ![chlimage_1-88](assets/chlimage_1-88.png)

1. テンプレートの基礎となっているコンポーネント（テンプレート内の **jcr:content** ノードの **sling:resourceType** プロパティで示される）をコピーして、インスタンスを作成します。

   コンポーネントは、**/apps/&lt;web サイト名>/components/&lt;コンポーネント名>** に格納されています。

1. 新しいコンポーネントの **jcr:title** と **jcr:description** を更新します。
1. テンプレート選択リストに新しいサムネール画像を表示する場合は、thumbnail.png を置き換えます（サイズは 128 x 98 px）。
1. テンプレートの **jcr:content** ノードの **sling:resourceType** を、新しいコンポーネントを参照するように更新します。
1. テンプレートとその基になるコンポーネントのいずれか一方または両方について、機能やデザインをさらに変更します。

   >[!NOTE]
   >
   >**/apps/&lt;web サイト>/templates/&lt;テンプレート名>** ノードに対する変更は、テンプレートインスタンスに影響します（選択リストの場合と同様）。
   >
   >
   **/apps/&lt;web サイト>/components/&lt;コンポーネント名>** ノードに対する変更は、テンプレート使用時に作成されるコンテンツページに影響します。

   これで、新しいテンプレートを使用して web サイト内にページを作成できます。

>[!NOTE]
>
エディタークライアントライブラリは、コンテンツページに `cq.shared` 名前空間が存在することを前提としています。名前空間が存在しない場合は、JavaScript エラー「`Uncaught TypeError: Cannot read property 'shared' of undefined`」が発生します。
>
すべてのサンプルコンテンツページには `cq.shared` が含まれているので、それらをベースとするコンテンツには自動的に `cq.shared` が含められます。ただし、サンプルコンテンツをベースとせず、ゼロから独自のコンテンツページを作成する場合は、`cq.shared` 名前空間を含める必要があります。
>
詳しくは、[クライアントサイドライブラリの使用](/help/sites-developing/clientlibs.md)を参照してください。

## 既存のテンプレートを使用可能にする {#making-an-existing-template-available}

この例では、特定のコンテンツパスにテンプレートを使用できるようにする方法を示しています。ページ作成者がページの作成時に使用できるテンプレートは、[使用可能なテンプレート](/help/sites-developing/templates.md#template-availability)で定義されたロジックによって決まります。

1. CRXDE Lite で、ページに使用するテンプレート（ニュースレターテンプレートなど）に移動します。
1. `allowedPaths` プロパティおよび[使用可能なテンプレート](/help/sites-developing/templates.md#template-availability)に使用する他のプロパティを変更します。例えば `allowedPaths`: `/content/geometrixx-outdoors/[^/]+(/.*)?` は、このテンプレートが `/content/geometrixx-outdoors` 以下の任意のパスで許可されることを意味します。

   ![chlimage_1-89](assets/chlimage_1-89.png)
