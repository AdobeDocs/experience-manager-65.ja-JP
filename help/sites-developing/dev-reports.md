---
title: レポートの開発
description: Adobe Experience Manager(AEM) は、レポートフレームワークに基づいて標準レポートを選択します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 3891150e-9972-4bbc-ad61-7f46a1f9bbb4
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '5182'
ht-degree: 56%

---


# レポートの開発 {#developing-reports}

Adobe Experience Manager(AEM) では、 [標準レポート](/help/sites-administering/reporting.md) そのほとんどはレポートフレームワークに基づいています。

フレームワークを使用して、これらの標準レポートを拡張するか、独自の新しいレポートを作成できます。 レポートフレームワークは、既存の CQ5 の概念や原則と緊密に統合されているので、開発者は CQ5 に関する既存の知識を、レポート開発の出発点として活用できます。

AEM に用意されている標準レポートの特徴：

* 以下のレポートは、レポートフレームワークに基づいています。

   * [コンポーネントレポート](/help/sites-administering/reporting.md#component-report)
   * [ページアクティビティレポート](/help/sites-administering/reporting.md#page-activity-report)
   * [ユーザーレポート](/help/sites-administering/reporting.md#user-report)
   * [ワークフローインスタンスレポート](/help/sites-administering/reporting.md#workflow-instance-report)

* 以下のレポートは、個別の原則に基づいているので、拡張できません。

   * [ディスク使用量](/help/sites-administering/reporting.md#disk-usage)
   * [ヘルスチェック](/help/sites-administering/reporting.md#health-check)
   * [ワークフローレポート](/help/sites-administering/reporting.md#workflow-report)

>[!NOTE]
>
>[独自のレポートの作成 - 例](#creating-your-own-report-an-example)のチュートリアルでも、以下で説明している使用可能な原則の種類を示しています。
>
>標準レポートを参照し、他の実装例を確認することもできます。

>[!NOTE]
>
>以下の例と定義で使用している表記は次のとおりです。
>
>* 各行では、次のようにノードまたはプロパティを定義しています。
>  `N:<name> [<nodeType>]` ：名前が `<*name*>` でノードタイプが `<*nodeType*>`*のノードを表します。*
>  `P:<name> [<propertyType]` ：名前が `<*name*>` でプロパティタイプが `<*propertyType*>` のプロパティを表します。
>  `P:<name> = <value>` ：プロパティ `<name>` に値 `<value>` を設定する必要があることを表します。
>
>* インデントは、ノード間の階層的依存関係を示します。
>* 次で区切られた項目： |は可能な項目のリストを示します。例えば、型や名前などです。 `String|String[]` は、プロパティが String または String のいずれかであることを示します。[].
>
>* `[]` は配列を示します。例えば String[] や、[クエリ定義](#query-definition)で説明しているノードの配列などがあります。
>
>特に指定のない限り、デフォルトのタイプは次のようになります。
>
>* ノード - `nt:unstructured`
>* プロパティ - `String`

## レポートフレームワーク {#reporting-framework}

レポートフレームワークは、次のような原則に従って動作します。

* 完全に、CQ5 QueryBuilder で実行されるクエリによって返される結果セットに基づいています。
* 結果セットは、レポートに表示するデータを定義します。結果セットの各行は、レポートの表形式表示の行に対応しています。
* 結果セットに対して実行できる操作は RDBMS の概念に似ており、主に *グループ化*&#x200B;と&#x200B;*集約*&#x200B;です。

* ほとんどのデータの取得と処理は、サーバーサイドでおこなわれます。
* クライアント側では、事前に処理されたデータの表示のみが行われます。小規模な処理タスク（セルコンテンツ内のリンクの作成など）のみがクライアント側で実行されます。

レポートフレームワーク（標準レポートの構造で示される）は、処理キューによって提供される次の構築ブロックを使用します。

![chlimage_1-248](assets/chlimage_1-248.png)

### レポートページ {#report-page}

レポートページは次のとおりです。

* 標準の CQ5 ページ。
* に基づく [標準の CQ5 テンプレート。レポート用に設定されます。](#report-template).

### レポートベース {#report-base}

The [`reportbase` コンポーネント](#report-base-component) は、次の理由により、レポートの基礎となります。

* の定義を保持 [クエリ](#the-query-and-data-retrieval) は、基になるデータの結果セットを配信します。

* これは、すべての列を含む、適応した段落システムです ( `columnbase`) がレポートに追加されました。
* 使用可能なグラフの種類と、現在アクティブなグラフの種類を定義します。
* 編集ダイアログボックスを定義します。このダイアログボックスでは、レポートの特定の側面を設定できます。

### 列ベース {#column-base}

各列は、[`columnbase`  コンポーネント](#column-base-component)のインスタンスであり、次のような特徴があります。

* 各レポートの parsys（`reportbase`）で使用される段落です。
* リンク先の [基になる結果セット](#the-query-and-data-retrieval). つまり、この結果セット内で参照される特定のデータと、その処理方法を定義します。
* 使用可能な集計やフィルターなどの追加の定義をデフォルト値と共に保持します。

### クエリとデータの取得 {#the-query-and-data-retrieval}

クエリ：

* [`reportbase`](#report-base)  コンポーネントの一部として定義されます。
* 次に基づく [CQ QueryBuilder](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/search/QueryBuilder.html).
* レポートの基本要素として使用するデータを取得します。結果セット（テーブル）の各行は、クエリが返すノードに結び付けられます。 [それぞれの列](#column-base-component)の具体的な情報はこのデータセットから抽出されます。

* 通常、次で構成されます。

   * ルートパス。

     検索するリポジトリのサブツリーを指定します。

     パフォーマンスへの影響を最小限に抑えるには、クエリをリポジトリの特定のサブツリーに制限（試行）することをお勧めします。 このルートパスは、[レポートテンプレート](#report-template)で事前定義するか、[設定（編集）ダイアログ](#configuration-dialog)でユーザーが設定することができます。

   * [1 つまたは複数の条件](#query-definition)。

     （最初の）結果セットを生成するために適用されます。ノードタイプの制限や、プロパティの制約などが含まれます。

**ここで重要な点は、クエリの結果セットで返される各単一のノードを使用して、レポート上に単一の行を生成する（1 対 1 の関係）ことです。**

開発者は、レポートに対して定義したクエリが、そのレポートに適したノードセットを返すようにする必要があります。 ただし、ノード自体が必要な情報をすべて保持する必要はありません。親ノードや子ノードから導き出すこともできます。例えば、[ユーザーレポート](/help/sites-administering/reporting.md#user-report)で使用するクエリでは、ノードタイプ（この場合は `rep:user`）に基づいてノードを選択します。ただし、このレポートのほとんどの列は、これらのノードから直接データを取り出すのではなく、子ノードの `profile` からデータを取り出します。

### 処理キュー {#processing-queue}

The [クエリ](#the-query-and-data-retrieval) レポートに行として表示するデータの結果セットを返します。 結果セットの各行が（サーバー側で）処理され、 [いくつかの段階](#phases-of-the-processing-queue)、レポートに表示するためにクライアントに転送される前。

次のような操作が可能です。

* 基になる結果セットから値を抽出したり導き出したりします。

  例えば、2 つのプロパティ値の差を計算することで、2 つのプロパティ値を 1 つの値として処理できます。

* 抽出された値の解決。様々な方法で実行できます。

  例えば、パスをタイトル（対応する *jcr:title* プロパティにある、人間が読み取れるコンテンツ）にマッピングできます。

* 様々なポイントでフィルターを適用します。
* 必要に応じて、複合値を作成します。

  例えば、ユーザーに表示するテキスト、ソートに使用する値、リンクの作成（クライアントサイドで）に使用する追加の URL で構成されます。

#### 処理キューのワークフロー {#workflow-of-the-processing-queue}

処理キューのワークフローを次に示します。

![chlimage_1-249](assets/chlimage_1-249.png)

#### 処理キューのフェーズ {#phases-of-the-processing-queue}

具体的な手順と要素は次の通りです。

1. 値抽出を使用して、[初期クエリ（reportbase）](#query-definition)から返された結果を、基になる結果セットに変換します。

   値抽出は、[列のタイプ](#column-specific-definitions)に基づいて自動的に選択されます。値抽出を使用して、基になる JCR クエリから値を読み取り、その値から結果セットを作成し、その後の処理で適用できるようにします。例えば `diff` タイプの場合、値抽出では 2 つのプロパティを読み取り、単一の値を計算して結果セットに追加します。値抽出は設定できません。

1. 生データを含む最初の結果セットに対して [初期フィルタリング](#column-specific-definitions) (*raw* フェーズ ) が適用されます。

1. 値は [前処理済み](#processing-queue); （定義済み） *適用* フェーズ。

1. [フィルター](#column-specific-definitions) ( 割り当て先 *前処理済み* フェーズ ) は、前処理された値に対して実行されます。

1. 値は、 [定義済みリゾルバー](#processing-queue).
1. [フィルター](#column-specific-definitions) ( 割り当て先 *解決済み* フェーズ ) は、解決された値に対して実行されます。

1. データは[グループ化および集計済](#column-specific-definitions)です。
1. 配列データは、リスト（文字列ベース）に変換することで解決されます。

   これは、複数の値を持つ結果をリストに変換して表示できるようにする暗黙の手順です。複数の値を持つ JCR プロパティに基づいたセル値（未集計）が必要です。

1. *afterApply* フェーズの定義に従い、値が再度[前処理](#processing-queue)されます。

1. データが並べ替えられます。
1. 処理されたデータはクライアントに転送されます。

>[!NOTE]
>
>基になるデータの結果セットを返す初期クエリは、`reportbase` コンポーネントで定義されます。
>
>処理キューの他の要素は、`columnbase` コンポーネントで定義されます。

## レポートの構築と設定 {#report-construction-and-configuration}

レポートを作成して設定するには、次の手順を実行する必要があります。

* a [レポートコンポーネントの定義場所](#location-of-report-components)
* [`reportbase`  コンポーネント](#report-base-component)
* 1 つ以上 [`columnbase` コンポーネント](#column-base-component)
* a [ページコンポーネント](#page-component)
* a [レポートデザイン](#report-design)
* a [レポートテンプレート](#report-template)

### レポートコンポーネントの場所 {#location-of-report-components}

デフォルトのレポートコンポーネントは、`/libs/cq/reporting/components` の下に保持されます。

ただし、これらのノードは更新せず、以下に独自のコンポーネントノードを作成することをお勧めします。 `/apps/cq/reporting/components` またはより適切な場合は `/apps/<yourProject>/reports/components`.

場所（一例として）：

```
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:components [sling:Folder]
```

この下に、レポートのルートを作成し、その下に、レポートベースコンポーネントと列ベースコンポーネントを作成します。

```
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:components [sling:Folder]
                N:<reportname> [sling:Folder]
                        N:<reportname> [cq:Component]  // report base component
                        N:<columnname> [cq:Component]  // column base component
```

### ページコンポーネント  {#page-component}

レポートページには、`/libs/cq/reporting/components/reportpage` の `sling:resourceType` を使用する必要があります。

カスタマイズしたページコンポーネントは必要ありません（通常は）。

## レポートの基本コンポーネント {#report-base-component}

レポートタイプごとに、`/libs/cq/reporting/components/reportbase` からコンテナコンポーネントを取得する必要があります。

このコンポーネントは、レポート全体のコンテナとして使用され、以下の情報が含まれます。

* The [クエリ定義](#query-definition).
* An [（オプション）dialog](#configuration-dialog) レポートを設定するために使用します。
* 任意 [グラフ](#chart-definitions) と統合されています。

```
N:<reportname> [cq:Component]
    P:sling:resourceSuperType = "cq/reporting/components/reportbase"
    N:charting
    N:dialog [cq:Dialog]
    N:queryBuilder
```

### クエリ定義 {#query-definition}

```xml
N:queryBuilder
    N:propertyConstraints
    [
        N:<name> // array of nodes (name irrelevant), each with the following properties:
            P:name
            P:value
    ]
    P:nodeTypes [String|String[]]
    P:mandatoryProperties [String|String[]
  ]
```

* `propertyConstraints`

  結果セットを、特定の値を持つ特定のプロパティを持つノードに制限します。 複数の制限が指定された場合、ノードはこれらすべてを満たす（AND 演算による）必要があります。

  次に例を示します。

  ```
  N:propertyConstraints
   [
   N:0
   P:sling:resourceType
   P:foundation/components/textimage
   N:1
   P:jcr:modifiedBy
   P:admin
   ]
  ```

  `admin` ユーザーによって最終的な変更が加えられた、すべての `textimage` コンポーネント を返します。

* `nodeTypes`

  指定したノードタイプのみを結果セットに含める場合に使用します。複数のノードタイプを指定できます。

* `mandatoryProperties`

  結果セットを、 *すべて* 指定したプロパティ。 プロパティの値が考慮されません。

すべてはオプションであり、必要に応じて組み合わせることができますが、少なくともそのうちの 1 つを定義する必要があります。

### チャート定義 {#chart-definitions}

```xml
N:charting
    N:settings
        N:active [cq:WidgetCollection]
        [
            N:<name> // array of nodes, each with the following property
                P:id   // must match the id of a child node of definitions
        ]
    N:definitions [cq:WidgetCollection]
    [
        N:<name> // array of nodes, each with the following properties
            P:id
            P:type
            // additional, chart type specific configurations
    ]
```

* `settings`

  アクティブなチャートについての定義を保持します。

   * `active`

     複数の設定を定義できるので、これを使用してどれが現在アクティブなものかを定義できます。これらはノードの配列によって定義されます（これらのノードには強制的な命名規則はありませんが、標準レポートでは通常、`0`、`1`.. `x` が使用されます）。各ノードは次のプロパティを持ちます。

      * `id`

        アクティブなチャートの ID。チャート（`definitions`）のいずれかの ID に一致する必要があります。

* `definitions`

  レポートでの使用が可能なチャートタイプを定義します。The `definitions` 使用する項目は、 `active` 設定。

  この定義はノードの配列（通常は `0`、`1`.. `x` と命名）を使用して指定され、各ノードには次のプロパティが含まれています。

   * `id`

     チャートの ID。

   * `type`

     使用できるグラフのタイプ。次から選択します。

      * `pie` 円グラフ。現在のデータのみから生成されます。

      * `lineseries`
折れ線グラフ（実際のスナップショットを表す点をつないだもの）履歴データからのみ生成されます。

   * グラフのタイプに応じて、追加のプロパティを使用できます。

      * グラフタイプが `pie` の場合：

         * `maxRadius`（`Double/Long`）

           円グラフで許容される最大半径。グラフで許容される最大サイズ（凡例を使用しない場合）。`fixedRadius` が指定されている場合、この値は無視されます。

         * `minRadius`（`Double/Long`）

           円グラフで許容される最小半径。`fixedRadius` が指定されている場合、この値は無視されます。

         * `fixedRadius`（`Double/Long`）
円グラフの半径の固定値を指定します。

      * グラフタイプが [`lineseries`](/help/sites-administering/reporting.md#display-limits) の場合：

         * `totals`（`Boolean`）

           **合計**を示す線を追加表示する場合は、true を指定します。
デフォルト：`false`

         * `series`（`Long`）

           表示する線（系列）の数。
デフォルト：`9`（この値も許容される最大値です）

         * `hoverLimit`（`Long`）

           ポップアップを表示する集計スナップショットの最大数（各水平線に表示され、個別の値を表すドット）。 つまり、ユーザーがグラフの凡例内の個別の値または対応するラベルにマウスポインターを置いたとき。

           デフォルト： `35` （つまり、現在のグラフ設定に 35 個を超える異なる値が適用できる場合は、ポップアップはまったく表示されません）。

           同時に表示できるポップアップは 10 個までに制限されています（凡例テキストにマウスを合わせると、複数のポップアップを表示できます）。

### 設定ダイアログ {#configuration-dialog}

各レポートには設定ダイアログを設定でき、ユーザーはレポートの様々なパラメーターを指定できます。このダイアログには、レポートページを開いているときに、「**編集**」ボタンでアクセスできます。

このダイアログは、標準の CQ [ダイアログ](/help/sites-developing/components-basics.md#dialogs)であり、そのように設定することができます（詳しくは [CQ.Dialog](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Dialog) を参照してください）。

ダイアログの例を次に示します。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<jcr:root xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
    jcr:primaryType="cq:Dialog"
    height="{Long}424">
    <items jcr:primaryType="cq:WidgetCollection">
        <props jcr:primaryType="cq:Panel">
            <items jcr:primaryType="cq:WidgetCollection">
                <title
                    jcr:primaryType="cq:Widget"
                    path="/libs/cq/reporting/components/commons/title.infinity.json"
                    xtype="cqinclude"/>
                <description
                    jcr:primaryType="cq:Widget"
                    path="/libs/cq/reporting/components/commons/description.infinity.json"
                    xtype="cqinclude"/>
                <rootPath
                    jcr:primaryType="cq:Widget"
                    fieldLabel="Root path"
                    name="./report/rootPath"
                    rootPath=""
                    rootTitle="Repository root"
                    xtype="pathfield"/>
                <processing
                    jcr:primaryType="cq:Widget"
                    path="/libs/cq/reporting/components/commons/processing.infinity.json"
                    xtype="cqinclude"/>
                <scheduling
                    jcr:primaryType="cq:Widget"
                    path="/libs/cq/reporting/components/commons/scheduling.infinity.json"
                    xtype="cqinclude"/>
            </items>
        </props>
    </items>
</jcr:root>
```

いくつかの事前設定されたコンポーネントを使用できます。`xtype` プロパティに値 `cqinclude` を指定して、これらのコンポーネントをダイアログで参照できます。

* **`title`**

  `/libs/cq/reporting/components/commons/title`

  レポートタイトルを定義するテキストフィールド。

* **`description`**

  `/libs/cq/reporting/components/commons/description`

  レポートの説明を定義するテキスト領域。

* **`processing`**

  `/libs/cq/reporting/components/commons/processing`

  レポート処理モード（手動／自動でのデータの読み込み）のセレクター。

* **`scheduling`**

  `/libs/cq/reporting/components/commons/scheduling`

  履歴グラフのスナップショットをスケジュールするためのセレクター。

>[!NOTE]
>
>`.infinity.json` サフィックスを使用して、参照されるコンポーネントを含める必要があります（上記の例を参照）。

### ルートパス {#root-path}

また、レポートのルートパスを定義できます。

* **`rootPath`**

  レポートの対象を、リポジトリの特定のセクション（ツリーまたはサブツリー）に限定できます。パフォーマンスの最適化のために、限定することをお勧めします。このルートパスは、各レポートページの `report` ノードの `rootPath` プロパティで指定します（ページを作成するときにテンプレートから取得されます）。

  次の方法で指定できます。

   * [レポートテンプレート](#report-template)（固定値または設定ダイアログのデフォルト値として）。
   * ユーザー（このパラメーターを使用）

## 列の基本コンポーネント {#column-base-component}

各列タイプには、`/libs/cq/reporting/components/columnbase` から派生したコンポーネントが必要です。

列コンポーネントは、次の組み合わせを定義します。

* The [列固有のクエリ](#column-specific-query) 設定。
* The [リゾルバーと前処理](#resolvers-and-preprocessing).
* [列固有の定義](#column-specific-definitions)（フィルターや集計など。`definitions` の子ノード）。
* [列のデフォルト値](#column-default-values).
* The [クライアントフィルター](#client-filter) サーバから返されたデータから表示する情報を抽出する。
* また、列コンポーネントは、 `cq:editConfig`. を定義するには、 [イベントとアクション](#events-and-actions) 必須。
* [汎用列](#generic-columns)の設定。

```
N:<columnname> [cq:Component]
    P:componentGroup
    P:jcr:title
    P:sling:resourceSuperType = "cq/reporting/components/columnbase"
    N:cq:editConfig [cq:EditConfig] // <a href="#events-and-actions">Events and Actions</a>
    N:defaults // <a href="#column-default-values">Column Default Values</a>
    N:definitions
      N:queryBuilder // <a href="#column-specific-query">Column Specific Query</a>
        P:property [String|String[]] // Column Specific Query
        P:subPath // Column Specific Query
        P:secondaryProperty [String|String[]] // Column Specific Query
        P:secondarySubPath // Column Specific Query
      N:data
        P:clientFilter [String] // <a href="#client-filter">Client Filter</a>
        P:resolver // <a href="#resolvers-and-preprocessing">Resolvers and Preprocessing</a>
        N:resolverConfig // Resolvers and Preprocessing
        N:preprocessing // Resolvers and Preprocessing
      P:type // <a href="#column-specific-definitions">Column Specific Definitions</a>
      P:groupable [Boolean] // Column Specific Definitions
      N:filters [cq:WidgetCollection] // Column Specific Definitions
      N:aggregates [cq:WidgetCollection] // Column Specific Definitions
```

[新規レポートの定義](#defining-your-new-report)も参照してください。

### 列固有のクエリ {#column-specific-query}

個々の列で使用するための（[レポートデータ結果セット](#the-query-and-data-retrieval)からの）特定のデータ抽出を定義します。

```xml
N:definitions
    N:queryBuilder
        P:property [String|String[]]
        P:subPath
        P:secondaryProperty [String|String[]]
        P:secondarySubPath
```

* `property`

  セルの実際の値を計算するために使用するプロパティを定義します。

  プロパティが String として定義されている場合[]に設定すると、複数のプロパティが（順に）スキャンされ、実際の値が見つかります。

  例えば、次のような場合、

  `property = [ "jcr:lastModified", "jcr:created" ]`

  対応する値抽出（ここで制御）:

   * 使用可能な jcr:lastModified プロパティがあるかどうかを確認し、ある場合はそれを使用します。
   * 使用可能な jcr:lastModified プロパティがない場合は、代わりに jcr:created の内容が使用されます。

* `subPath`

  クエリが返すノードに結果がない場合、 `subPath` は、プロパティの場所を定義します。

* `secondaryProperty`

  実際のセル値の計算に使用する必要がある 2 番目のプロパティです。 この定義は、特定の列タイプ（差分および並べ替え可能）に対してのみ使用されます。

  例えば、ワークフローインスタンスレポートがある場合、指定されたプロパティは、開始時刻と終了時刻の時間差（ミリ秒）の実際の値を保存するために使用されます。

* `secondarySubPath`

  subPath と同様、`secondaryProperty` が使用された場合。

通常は、 `property` が使用されます。

### クライアントフィルター {#client-filter}

クライアントフィルタは、サーバから返されたデータから、表示する情報を抽出する。

>[!NOTE]
>
>このフィルターは、サーバーサイドの処理全体が適用された後に、クライアントサイドで実行されます。

```xml
N:definitions
    N:data
        P:clientFilter [String]
```

The `clientFilter` は、次の JavaScript 関数です。

* 入力として、パラメーターを 1 つ受け取ります。サーバーから返されたデータ（完全に前処理済み）です。
* 出力として、フィルターを適用した（処理後の）値を返します。入力データから抽出または派生したデータです。

次の例では、コンポーネントパスから対応するページパスを抽出します。

```
function(v) {
    var sepPos = v.lastIndexOf('/jcr:content');
    if (sepPos < 0) {
        return v;
    }
    return v.substring(sepPos + '/jcr:content'.length, v.length);
}
```

### リゾルバーと前処理 {#resolvers-and-preprocessing}

[処理キュー](#processing-queue)で様々なリゾルバーを定義し、前処理を設定します。

```xml
N:definitions
    N:data
        P:resolver
        N:resolverConfig
        N:preprocessing
            N:apply
            N:applyAfter
```

* `resolver`

  使用するリゾルバーを定義します。次のリゾルバーを利用できます。

   * `const`

     値を他の値にマッピングします。例えば、`en` などの定数を、等価な値 `English` に解決するために使用します。

   * `default`

     デフォルトのリゾルバー。これは、実際には何も解決しないダミーのリゾルバーです。

   * `page`

     パスの値を、適切なページのパス（正確には、対応する `jcr:content` ノード）に解決します。例えば、`/content/.../page/jcr:content/par/xyz` は `/content/.../page/jcr:content` に解決されます。

   * `path`

     パスの値を解決します。その際、オプションでサブパスを追加し、ノードのプロパティから実際の値を取得します ( `resolverConfig`) を解決されたパスに置き換えます。 例えば、`/content/.../page/jcr:content` の `path` は `jcr:title` プロパティのコンテンツに解決でき、これはページパスがページタイトルに解決されることを意味します。

   * `pathextension`

     パスを先頭に追加し、解決されたパスのノードのプロパティから実際の値を取得することで、値を解決します。例えば、値 `de` の先頭に、プロパティ `language` から値を取得して `/libs/wcm/core/resources/languages` のようなパスを追加すると、国コード `de` を言語の説明 `German` に解決できます。

* `resolverConfig`

  リゾルバーの定義を提供します。 使用できるオプションは、 `resolver` 選択済み：

   * `const`

     プロパティを使用して、解決する定数を指定します。プロパティの名前で、解決する定数を定義します。プロパティの値で、解決後の値を定義します。

     例えば、 **名前**= `1` および **値** `=One` 1 を 1 に解決します。

   * `default`

     使用できる設定がありません。

   * `page`

      * `propertyName`（オプション）

        値の解決に使用するプロパティの名前を定義します。指定しない場合、デフォルト値の *jcr:title*（ページタイトル）が使用されます。`page` リゾルバーの場合、最初にパスがページパスに解決され、次にページタイトルに解決されることを意味します。

   * `path`

      * `propertyName`（オプション）

        値の解決に使用するプロパティの名前を指定します。指定しない場合、`jcr:title` のデフォルト値が使用されます。

      * `subPath`（任意）

        このプロパティは、値を解決する前にパスに付加する接尾辞を指定するときに使用します。

   * `pathextension`

      * `path`（必須）

        先頭に付加するパスを定義します。

      * `propertyName`（必須）

        実際の値が配置されている、解決されたパスのプロパティを定義します。

      * `i18n`（任意、ブール演算タイプ）

        解決された値が *国際化した* ( つまり、 [CQ5 の国際化サービス](/help/sites-administering/tc-manage.md)) をクリックします。

* `preprocessing`

  前処理は任意で、*apply* または *applyAfter* の処理フェーズに（別々に）バインドできます。

   * `apply`

     初期の前処理フェーズ（[処理キューの説明での手順 3](#processing-queue)）に適用。

   * `applyAfter`

     前処理（[処理キューの説明での手順 9](#processing-queue)）後に適用。

#### リゾルバー {#resolvers}

リゾルバーを使用して、必要な情報を抽出します。様々なリゾルバーの例を以下に示します。

**Const**

次に、の定数値を解決します。 `VersionCreated` 文字列に `New version created`.

`/libs/cq/reporting/components/auditreport/typecol/definitions/data` を参照してください。

```xml
N:data
    P:resolver=const
    N:resolverConfig
        P:VersionCreated="New version created"
```

**ページ**

対応するページの jcr:content（子）ノードの jcr:description プロパティに、パス値を解決します。

`/libs/cq/reporting/components/compreport/pagecol/definitions/data` を参照してください。

```xml
N:data
    P:resolver=page
    N:resolverConfig
        P:propertyName="jcr:description"
```

**パス**

以下は、`jcr:title` プロパティのコンテンツへの `/content/.../page` パスを解決します。これは、ページパスがページタイトルに解決されることを意味します。

`/libs/cq/reporting/components/auditreport/pagecol/definitions/data` を参照してください。

```xml
N:data
    P:resolver=path
    N:resolverConfig
        P:propertyName="jcr:title"
        P:subPath="/jcr:content"
```

**パスの拡張子**

以下のコードでは、値 `de` の前にパスの拡張子 `/libs/wcm/core/resources/languages` を付けて、プロパティ `language` から値を取得し、言語の説明 `German` に対して国名コード `de` を解決します。

`/libs/cq/reporting/components/userreport/languagecol/definitions/data` を参照してください。

```xml
N:data
    P:resolver=pathextension
    N:resolverConfig
        P:path="/libs/wcm/core/resources/languages"
        P:propertyName="language"
```

#### 前処理 {#preprocessing}

`preprocessing` の定義は、以下のどちらかに適用できます。

* 元の値：

  元の値に対する前処理の定義は、`apply` や `applyAfter` に直接指定します。

* 値の集計状態：

  必要に応じて、集計ごとに個別の定義を指定できます。

  集計値の明示的な前処理を指定するには、前処理定義がそれぞれの `aggregated` 子ノード（`apply/aggregated`、`applyAfter/aggregated`）に存在している必要があります。個別の集計に対する明示的な前処理が必要な場合、前処理の定義は、それぞれの集計の名前を持つ子ノードに対して行われます ( 例えば、 `apply/aggregated/min/max` または他の集計 )。

以下のいずれかを指定して、前処理中に使用できます。

* [パターンの検索と置換](#preprocessing-find-and-replace-patterns)
検索後、（正規表現として定義される）指定したパターンを別のパターンに置き換えます。例えば、元の値からサブ文字列を抽出するときに使用できます。

* [データタイプフォーマッター](#preprocessing-data-type-formatters)

  数値を相対文字列に変換します。例えば、「1 時間の時差を表す値」は、次のような文字列に解決されます。 `1:24PM (1 hour ago)`.

以下に例を示します。

```xml
N:definitions
    N:data
        N:preprocessing
            N:apply|applyAfter
                P:pattern         // regex
                P:replace         // replacement for regex
                // and/or
                P:format          // data type formatter
```

#### 前処理 — パターンの検索と置換 {#preprocessing-find-and-replace-patterns}

前処理の場合は、[正規表現](https://ja.wikipedia.org/wiki/%E6%AD%A3%E8%A6%8F%E8%A1%A8%E7%8F%BE) または Regex と定義される `pattern` を指定しますが、これは検索後に `replace` パターンによって置換されます。

* `pattern`

  サブ文字列を検索するために使用される正規表現。

* `replace`

  元の文字列の置き換えとして使用される文字列、または文字列の表現です。 多くの場合、`pattern` の正規表現によって検索される文字列のサブ文字列を示します。

置換の例は、以下のように分類できます。

* `definitions/data/preprocessing/apply` ノードを以下の 2 つのプロパティと共に使用します。

   * `pattern`：`(.*)(/jcr:content)(/|$)(.*)`
   * `replace`：`$1`

* 以下の文字列が検索されます。

   * `/content/geometrixx/en/services/jcr:content/par/text`

* 次の 4 つのセクションに分類されます。

   * `$1` - `(.*)` - `/content/geometrixx/en/services`
   * `$2` - `(/jcr:content)` - `/jcr:content`
   * `$3` - `(/|$)` - `/`
   * `$4` - `(.*)` - `par/text`

* `$1` で表される文字列に置き換えます。

   * `/content/geometrixx/en/services`

#### 前処理 — データタイプフォーマッター {#preprocessing-data-type-formatters}

これらのフォーマッターは、数値を対応する文字列に変換します。

例えば、`min`、`avg`、`max` の集計を許可する時間列に使用できます。As `min`/ `avg`/ `max` 集計は、 *時間差* ( 例： `10 days ago`) の場合は、データフォーマッターが必要です。 したがって、`min`／`avg`／`max` の集計値に対して `datedelta` フォーマッターが適用されます。次の場合、 `count` 集計も使用できます。この場合、フォーマッタは不要で、元の値も不要です。

現在使用可能なデータタイプフォーマッターは、以下のとおりです。

* `format`

  データタイプフォーマッター：

   * `duration`

     指定された 2 つの日時の間のタイムスパンです。例えば、1 時間かかったワークフローアクションの開始と終了 (2/13/11 11:23h から 1 時間後の2/13/11 12:23h まで )。

     数値（ミリ秒として解釈）が期間を表す文字列に変換されます。例えば、`30000` は *`30s`* にフォーマットされます。

   * `datedelta`

     データデルタは、過去の日付から「今」までの期間です（レポートが後で表示される場合は、結果が異なります）。

     数値（日単位の時間差として解釈）が、対応する日付の文字列に変換されます。例えば、「1」は 1 日前の形式で設定されます。

以下の例では、`min` および `max` の集計に対して `datedelta` フォーマットが指定されています。

```xml
N:definitions
    N:data
        N:preprocessing
            N:apply
                N:aggregated
                    N:min
                        P:format = "datedelta"
                    N:max
                        P:format = "datedelta"
```

### 列固有の定義 {#column-specific-definitions}

列固有の定義は、その列で使用できるフィルターと集計を定義します。

```xml
N:definitions
    P:type
    P:groupable [Boolean]
    N:filters [cq:WidgetCollection]
    [
        N:<name> // array of nodes (names irrelevant) with the following properties:
            P:filterType
            P:id
            P:phase
    ]
    N:aggregates [cq:WidgetCollection]
    [
        N:<name> // array of nodes (names irrelevant) with the following properties:
            P:text
            P:type
    ]
```

* `type`

  標準オプションとして使用できるものは以下のとおりです。

   * `string`
   * `number`
   * `int`
   * `date`
   * `diff`
   * `timeslot`

     集計に必要な日付の一部を抽出するために使用します（例えば、年ごとにグループ化して、年ごとに集計したデータを取得します）。

   * `sortable`

     並べ替えと表示に異なる値（異なるプロパティから取得）を使用する値に使用されます。

  また、上記のいずれかを複数の値として定義できます。例： `string[]` 文字列の配列を定義します。

  値抽出は、列のタイプによって選択されます。値抽出が列のタイプに対して使用可能な場合は、この抽出が使用されます。それ以外の場合は、デフォルトの値抽出が使用されます。

  タイプには、（任意で）パラメーターを指定できます。例えば、`timeslot:year` は日付フィールドから年を抽出します。タイプとそのパラメーター：

   * `timeslot`  — 値は、 `java.utils.Calendar`.

      * `timeslot:year` - `Calendar.YEAR`
      * `timeslot:month-of-year` - `Calendar.MONTH`
      * `timeslot:week-of-year` - `Calendar.WEEK_OF_YEAR`
      * `timeslot:day-of-month` - `Calendar.DAY_OF_MONTH`
      * `timeslot:day-of-week` - `Calendar.DAY_OF_WEEK`
      * `timeslot:day-of-year` - `Calendar.DAY_OF_YEAR`
      * `timeslot:hour-of-day` - `Calendar.HOUR_OF_DAY`
      * `timeslot:minute-of-hour` - `Calendar.MINUTE`

* `groupable`

  レポートをこの列でグループ化できるかどうかを指定します。

* `filters`

  フィルターの定義。

   * `filterType`

     使用可能なフィルターは以下のとおりです。

      * `string`

        文字列ベースのフィルター。

   * `id`

     フィルター識別子。

   * `phase`

     利用可能なフェーズ：

      * `raw`

        フィルターは生データに適用されます。

      * `preprocessed`

        フィルターは、前処理済みのデータに適用されます。

      * `resolved`

        フィルターは、解決されたデータに適用されます。

* `aggregates`

  集計の定義。

   * `text`

     集計のテキスト名。次の場合 `text` が指定されていない場合、集計のデフォルトの説明が取得されます。 例： `minimum` が `min` 集計。

   * `type`

     集計タイプ。使用可能な集計は次のとおりです。

      * `count`

        行数を数えます。

      * `count-nonempty`

        空でない行の数を数えます。

      * `min`

        最小値が提供されます。

      * `max`

        最大値を提供します。

      * `average`

        平均値が提供されます。

      * `sum`

        すべての値の合計を提供します。

      * `median`

        中央値を示します。

      * `percentile95`

        すべての値の 95 番目のパーセンタイル値を使用します。

### 列のデフォルト値 {#column-default-values}

列のデフォルト値を定義します。

```xml
N:defaults
    P:aggregate
```

* `aggregate`

  有効な `aggregate` の値は、`aggregates` の `type` と同じです（[列固有の定義（定義 - フィルター／集計）](#column-specific-definitions)を参照）。

### イベントおよびアクション {#events-and-actions}

「設定を編集」では、リスナーが検出する必要なイベントと、それらのイベントの発生後に適用されるアクションを定義します。 背景の情報について詳しくは、[コンポーネント開発の概要](/help/sites-developing/components.md)を参照してください。

必要なアクションがすべて実行されるようにするには、次の値を定義します。

```xml
N:cq:editConfig [cq:EditConfig]
    P:cq:actions [String[]] = "insert", "delete"
    P:cq:dialogMode = "floating"
    P:cq:layout = "auto"
    N:cq:listeners [cq:EditListenersConfig]
        P:aftercreate = "REFRESH_INSERTED"
        P:afterdelete = "REFRESH_SELF"
        P:afteredit = "REFRESH_SELF"
        P:afterinsert = "REFRESH_INSERTED"
        P:aftermove = "REFRESH_SELF"
        P:afterremove = "REFRESH_SELF"
```

### 汎用列 {#generic-columns}

汎用列は、列定義（の大部分）を（コンポーネントノードではなく）列ノードのインスタンスに格納する拡張機能です。

個々の汎用コンポーネント用にカスタマイズできる（標準）ダイアログボックスを使用します。 このダイアログボックスでは、レポートページ上の汎用列の列プロパティを（メニューオプションを使用して）定義できます **列のプロパティ…**) をクリックします。

例えば、 **汎用** 列 **ユーザーレポート**.詳しくは、 `/libs/cq/reporting/components/userreport/genericcol`.

列を汎用にするには：

* `generic` に列の `definition` ノードの `type` プロパティを設定します。

  `/libs/cq/reporting/components/userreport/genericcol/definitions` を参照してください。

* 列の `definition` ノードで、（標準）ダイアログの定義を指定します。

  `/libs/cq/reporting/components/userreport/genericcol/definitions/dialog` を参照してください。

   * ダイアログボックスのフィールドは、対応するコンポーネントプロパティと同じ名前を参照する必要があります（パスも含む）。

     例えば、汎用列のタイプをダイアログで設定できるようにする場合、名前が `./definitions/type` のフィールドを使用します。

   * UI やダイアログを使用して定義するプロパティは、`columnbase` コンポーネントで定義するプロパティより優先されます。

* 編集設定を定義します。

  `/libs/cq/reporting/components/userreport/genericcol/cq:editConfig` を参照してください。

* 標準の AEM の手法を使用して、（その他の）列のプロパティを定義します。

  コンポーネントインスタンスと列インスタンスの両方で定義されたプロパティの場合は、列インスタンスの値が優先されます。

  汎用列で使用できるプロパティは次のとおりです。

   * `jcr:title` - 列名
   * `definitions/aggregates` - 集計
   * `definitions/filters` - フィルター
   * `definitions/type` - 列のタイプ（セレクターかコンボボックス、または非表示のフィールドを使用して、ダイアログで定義する必要があります）
   * `definitions/data/resolver` および `definitions/data/resolverConfig`（ただし `definitions/data/preprocessing` と `.../clientFilter` は除く）- リゾルバーと設定
   * `definitions/queryBuilder` - クエリビルダーの設定
   * `defaults/aggregate` - デフォルトの集計

  汎用列の新しいインスタンスが **ユーザーレポート**&#x200B;の場合、ダイアログで定義されたプロパティは次の場所に保持されます。

  `/etc/reports/userreport/jcr:content/report/columns/genericcol/settings/generic`

## レポートデザイン {#report-design}

レポートの作成に使用できる列のタイプはデザインで定義します。列を追加する段落システムも定義します。

Adobeでは、各レポートに個別のデザインを作成することをお勧めします。 これにより、完全な柔軟性が確保されます。 詳しくは、 [新しいレポートの定義](#defining-your-new-report).

デフォルトのレポートコンポーネントは、`/etc/designs/reports` の下に保持されます。

レポートの場所は、コンポーネントの場所によって異なります。

* `/etc/designs/reports/<yourReport>` は、レポートが以下に含まれる場合に適しています `/apps/cq/reporting`

* `/apps/<yourProject>/reports` パターンを使用したレポートの場合は `/etc/designs/<yourProject>/reports/<*yourReport*>`

必要なデザインプロパティは、`jcr:content/reportpage/report/columns` に登録されます（例：`/etc/designs/reports/<reportName>/jcr:content/reportpage/report/columns`）。

* `components`

  レポートで使用できるコンポーネントやコンポーネントグループ。

* `sling:resourceType`

  値が `cq/reporting/components/repparsys` のプロパティ。

（コンポーネントレポートのデザインから取得した）デザインスニペットの例を次に示します。

```xml
<!-- ... -->
    <jcr:content
        jcr:primaryType="nt:unstructured"
        jcr:title="Component Report"
        sling:resourceType="wcm/core/components/designer">
        <reportpage jcr:primaryType="nt:unstructured">
            <report jcr:primaryType="nt:unstructured">
                <columns
                    jcr:primaryType="nt:unstructured"
                    sling:resourceType="cq/reporting/components/repparsys"
                    components="group:Component Report"/>
            </report>
        </reportpage>
    </jcr:content>
<!-- ... -->
```

個々の列に対してデザインを指定する必要はありません。使用可能な列は、デザインモードで定義できます。

>[!NOTE]
>
>Adobeでは、標準のレポートデザインを変更しないことをお勧めします。 これは、ホットフィックスのアップグレード時やインストール時に変更内容が失われないようにするためです。
>
>標準レポートをカスタマイズする場合は、レポートとそのデザインをコピーします。

>[!NOTE]
>
>レポートの作成時に、デフォルトの列を自動的に作成できます。これらはテンプレートで指定されます。

## レポートテンプレート {#report-template}

各レポートタイプは、テンプレートを提供する必要があります。これらは標準的な [CQ テンプレート](/help/sites-developing/templates.md)であり、そのように設定できます。

テンプレートは次の条件を満たす必要があります。

* `cq/reporting/components/reportpage` に `sling:resourceType` を設定

* 使用するデザインを示す
* を作成する `report` コンテナを参照する子ノード ( `reportbase`) コンポーネントを `sling:resourceType` プロパティ

（コンポーネントレポートテンプレートから取得される）テンプレートスニペットの例を次に示します。

```xml
<!-- ... -->
    <jcr:content
        cq:designPath="/etc/designs/reports/compreport"
        jcr:primaryType="cq:PageContent"
        sling:resourceType="cq/reporting/components/reportpage">
        <report
            jcr:primaryType="nt:unstructured"
            sling:resourceType="cq/reporting/components/compreport/compreport"/>
    </jcr:content>
<!-- .. -->
```

（ユーザーレポートテンプレートから取得した）ルートパスの定義を示すテンプレートスニペットの例を次に示します。

```xml
<!-- ... -->
    <jcr:content
        cq:designPath="/etc/designs/reports/userreport"
        jcr:primaryType="cq:PageContent"
        sling:resourceType="cq/reporting/components/reportpage">
        <report
            jcr:primaryType="nt:unstructured"
            rootPath="/home/users"
            sling:resourceType="cq/reporting/components/compreport/compreport"/>
    </jcr:content>
<!-- .. -->
```

デフォルトのレポートテンプレートは、`/libs/cq/reporting/templates` の下に保持されます。

ただし、Adobeでは、これらのノードを更新しないことをお勧めします。 代わりに、以下に独自のコンポーネントノードを作成します。 `/apps/cq/reporting/templates` またはより適切な場合は `/apps/<yourProject>/reports/templates`.

定義例は次のとおりです（[レポートコンポーネントの場所](#location-of-report-components)も参照）。

```xml
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:templates [sling:Folder]
```

この下に、テンプレートのルートを作成します。

```xml
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:templates [sling:Folder]
                N:<reportname> [sling:Folder]
```

## 独自レポートの作成 — 例 {#creating-your-own-report-an-example}

### 新しいレポートの定義 {#defining-your-new-report}

レポートを定義するには、次の項目を作成して設定します。

1. レポートコンポーネントのルート。
1. レポートのベースコンポーネント。
1. 1 つ以上の列ベースコンポーネント。
1. レポートのデザイン。
1. レポートテンプレートのルート。
1. レポートテンプレート。

これらの手順を説明するために、次の例では、リポジトリ内のすべての OSGi 設定をリストするレポートを定義します。 つまり、 `sling:OsgiConfig` ノード。

>[!NOTE]
>
>既存のレポートをコピーして新しいバージョンにカスタマイズするという方法もあります。

1. 新しいレポートのルートノードを作成します。

   例えば、`/apps/cq/reporting/components/osgireport` の下です。

   ```xml
   N:cq [nt:folder]
       N:reporting [sling:Folder]
           N:components [sling:Folder]
               N:osgireport [sling:Folder]
   ```

1. レポートベースを定義します。例： `osgireport[cq:Component]` under `/apps/cq/reporting/components/osgireport`.

   ```xml
   N:osgireport [sling:Folder]
       N:osgireport [cq:Component]
           P:sling:resourceSuperType [String] = "cq/reporting/components/reportbase"
           N:charting [nt:unstructured]
               N:settings [nt:unstructured]
                   N:active [cq:WidgetCollection]
                       N:0 [nt:unstructured]
                           P:id [String] = "pie"
                       N:1 [nt:unstructured]
                           P:id [String] = "lineseries"
               N:definitions [cq:WidgetCollections]
                   N:0 [nt:unstructured]
                       P:id [String] = "pie"
                       P:maxRadius [Long] = 180
                       P:type [String] = "pie"
                   N:1 [nt:unstructured]
                       P:id [String] = "lineseries"
                       P:type [String] = "lineseries"
           N:dialog [cq:Dialog]
               P:height [Long] = 424
               N:items [cq:WidgetCollection]
                   N:props [cq:Panel]
                       N:items [cq:WidgetCollection]
                           N:title [cq:Widget]
                               P:path [String] = "/libs/cq/reporting/components/commons/title.infinity.json"
                               P:xtype [String] = "cqinclude"
                           N:description [cq:Widget]
                               P:path [String] = "/libs/cq/reporting/components/commons/description.infinity.json"
                               P:xtype [String] = "cqinclude"
                           N:rootPath [cq:Widget]
                               P:fieldLabel [String] = "Root path"
                               P:name [String] = "./report/rootPath"
                               P:xtype [String] = "pathfield"
                           N:processing [cq:Widget]
                               P:path [String] = "/libs/cq/reporting/components/commons/processing.infinity.json"
                               P:xtype [String] = "cqinclude"
                           N:scheduling [cq:Widget]
                               P:path [String] = "/libs/cq/reporting/components/commons/scheduling.infinity.json"
                               P:xtype [String] = "cqinclude"
           N:queryBuilder [nt:unstructured]
               P:nodeTypes [String[]] = "sling:OsgiConfig"
   ```

   これは、次のようなレポートベースコンポーネントを定義します。

   * タイプが `sling:OsgiConfig` のすべてのノードを検索
   * `pie` と `lineseries` の両方のグラフを表示
   * ユーザーがレポートを設定するためのダイアログを提供します

1. 最初の列 (columnbase) コンポーネントを定義します。 例： `bundlecol[cq:Component]` under `/apps/cq/reporting/components/osgireport`.

   ```xml
   N:osgireport [sling:Folder]
       N:bundlecol [cq:Component]
           P:componentGroup [String] = "OSGi Report"
           P:jcr:title = "Bundle"
           P:sling:resourceSuperType [String] = "cq/reporting/components/columnbase"
           N:cq:editConfig [cq:EditConfig]
               P:cq:actions [String[]] = "insert", "delete"
               P:cq:dialogMode [String] = "floating"
               P:cq:layout [String] = "auto"
               N:cq:listeners [cq:EditListenersConfig]
                   P:aftercreate [String] "REFRESH_INSERTED"
                   P:afterdelete [String] "REFRESH_SELF"
                   P:afteredit [String] "REFRESH_SELF"
                   P:afterinsert [String] "REFRESH_INSERTED"
                   P:aftermove [String] "REFRESH_SELF"
                   P:afterremove [String] "REFRESH_SELF"
           N:defaults [nt:unstructured]
               P:aggregate [String] = "count"
           N:definitions [nt:unstructured]
               P:groupable [Boolean] = false
               P:type [String] = "string"
               N:queryBuilder [nt:unstructured]
                   P:property [String] = "jcr:path"
   ```

   これは、次のような columnbase コンポーネントを定義します。

   * サーバーから受信する値（この場合、`sling:OsgiConfig` の各ノードの `jcr:path` プロパティ）を検索し、その値を返す
   * `count` 集計を提供
   * グループ化はできない
   * タイトル（テーブル内の列タイトル）は `Bundle`
   * サイドキックグループ `OSGi Report` に含まれる
   * 指定されたイベントで更新

   >[!NOTE]
   >
   >この例では、 `N:data` および `P:clientFilter`. これは、サーバーから受け取った値が 1 対 1 で返されるためで、これがデフォルトの動作です。
   >
   >これは、定義と同じです。
   >
   >```
   >N:data [nt:unstructured]
   >   P:clientFilter [String] = "function(v) { return v; }"
   >```
   >
   >この関数は、受け取った値を返します。

1. レポートデザインを定義します。例： `osgireport[cq:Page]` under `/etc/designs/reports`.

   ```xml
   N:osgireport [cq:Page]
       N:jcr:content [nt:unstructured]
           P:jcr:title [String] = "OSGi report"
           P:sling:resourceType [String] = "wcm/core/components/designer"
           N:reportpage [nt:unstructured]
               N:report [nt:unstructured]
                   N:columns [nt:unstructured]
                       P:components [String] = "group:OSGi Report"
                       P:sling:resourceType [String] = "cq/reporting/components/repparsys"
   ```

1. 新しいレポートテンプレートのルートノードを作成します。

   例えば、`/apps/cq/reporting/templates/osgireport` の下です。

   ```xml
   N:cq [nt:folder]
       N:reporting [sling:Folder]
           N:templates [sling:Folder]
               N:osgireport [cq:Template]
   ```

1. レポートテンプレートを定義します。例： `osgireport[cq:Template]` under `/apps/cq/reporting/templates`.

   ```xml
   N:osgireport [cq:Template]
       P:allowedPaths [String[]] = "/etc/reports(/.*)?"
       P:jcr:description [String] = "Use this report generator to create an OSGi report."
       P:jcr:title [String] = "OSGi Report Template"
       P:ranking [Long] = 100
       P:shortTitle [String] = "OSGi Report"
       N:jcr:content [cq:PageContent]
           P:cq:designPath [String] = "/etc/designs/reports/osgireport"
           P:sling:resourceType [String] = "cq/reporting/components/reportpage"
           N:report [nt:unstructured]
               P:rootPath [String] = "/"
               P:sling:resourceType [String] = "cq/reporting/components/osgireport/osgireport"
       N:thumbnail.png [nt:file]
   ```

   これは、次のようなテンプレートを定義します。

   * 結果のレポートの `allowedPaths` を定義します。上記の場合、`/etc/reports` 下の任意の場所となります。
   * テンプレートのタイトルと説明を提供します。
   * テンプレートリストで使用するサムネール画像を提供します（このノードの完全な定義は上記ではありません。既存のレポートから thumbnail.png のインスタンスをコピーするのが最も簡単です）。

### 新しいレポートのインスタンスの作成 {#creating-an-instance-of-your-new-report}

これで、新しいレポートのインスタンスを作成できます。

1. **ツール**&#x200B;コンソールを開きます。

1. 選択 **レポート** をクリックします。
1. 次に、ツールバーから「**新規…**」を選択します。「**タイトル**」 および 「**名前**」を定義して、テンプレートのリストから新しいレポートタイプ（**OSGi レポートテンプレート**）を選択し、「**作成**」をクリックします。
1. 新しいレポートインスタンスがリストに表示されます。 ダブルクリックして開きます。
1. サイドキックからコンポーネント（この例では、「**OSGi レポート**」グループの「**バンドル**」）をドラッグして最初の列を作成し、[レポートの定義を開始](/help/sites-administering/reporting.md#the-basics-of-report-customization)します。

   >[!NOTE]
   >
   >この例では、グループ化可能な列がないので、グラフは使用できません。 グラフを表示するには、`groupable` を `true` に設定します。
   >
   >```
   >N:osgireport [sling:Folder]
   > N:bundlecol [cq:Component]
   > N:definitions [nt:unstructured]
   > P:groupable [Boolean] = true
   >```
   >

## レポートフレームワークサービスの設定 {#configuring-the-report-framework-services}

この節では、レポートフレームワークを実装する OSGi サービスの高度な設定オプションについて説明します。

これらは、Web コンソールの設定メニュー（次の場所で利用可能）を使用して表示できます。 `http://localhost:4502/system/console/configMgr`（例： ）。 AEM を操作しているときは、このようなサービスの設定を管理する方法がいくつかあります。詳細および推奨事項については、[OSGi の設定](/help/sites-deploying/configuring-osgi.md)を参照してください。

### 基本サービス（Day CQ レポート設定） {#basic-service-day-cq-reporting-configuration}

* **タイムゾーン**&#x200B;は、履歴データが作成されるタイムゾーンを定義します。これは、履歴グラフで世界中の各ユーザーに対して、確実に同じデータを表示するためです。
* **ロケール** 使用するロケールを定義します。 **タイムゾーン** 履歴データに対して。 ロケールは、ロケール固有のカレンダー設定（例えば、週の最初の曜日が日曜日か月曜日か）を決定するために使用されます。

* **スナップショットパス**&#x200B;は、履歴グラフのスナップショットを保存するルートパスを定義します。
* **レポートへのパス**&#x200B;は、レポートのあるパスを定義します。これは、スナップショットサービスで、実際にスナップショットを作成するレポートを決定するために使用されます。
* **日別スナップショット**&#x200B;は、日別のスナップショットを取得する時間を定義します。指定された時間は、サーバーのローカルタイムゾーンになります。
* **時間別スナップショット**&#x200B;は、時間別のスナップショットを取得する各時刻の分を定義します。
* **行（最大）**&#x200B;は、各スナップショットに対して保存される最大行数を定義します。この値は合理的に選択する必要があります。 値が大きすぎる場合は、リポジトリのサイズに影響します。値が小さすぎる場合は、履歴データの処理方法が原因で、データが正確でない可能性があります。
* **フェイクデータ**&#x200B;を有効にした場合、 `fakedata` セレクター。無効の場合は、 `fakedata` セレクターは例外をスローします。

  データは偽物なので、必ず設定する必要があります *のみ* をテストおよびデバッグ目的で使用します。

  の使用 `fakedata` セレクターはレポートを暗黙的に終了するので、既存のデータはすべて失われます。 データは手動で復元できますが、時間のかかるプロセスになる場合があります。

* **スナップショットユーザー**&#x200B;で、スナップショットの取得に使用できるオプションのユーザーを定義します。

  基本的には、レポートを終了したユーザーに対してスナップショットが取得されます。代わりに使用するフォールバックユーザーを指定する場合があります（例えば、パブリッシュシステムでは、アカウントがレプリケートされていないので、このユーザーが存在しない場合）。

  また、ユーザーを指定すると、セキュリティ上のリスクが生じる場合があります。

* **スナップショットユーザーを適用**&#x200B;有効にした場合、すべてのスナップショットが、以下で指定されたユーザーで取得されます。 *スナップショットユーザ*. 正しく処理されない場合は、セキュリティに重大な影響が及ぶ可能性があります。

### キャッシュ設定 (Day CQ Reporting Cache) {#cache-settings-day-cq-reporting-cache}

* **有効にする** レポートデータのキャッシュを有効または無効にできます。 レポートのキャッシュを有効にすると、複数のリクエストを実行する際にレポートデータがメモリに保持されます。 これにより、パフォーマンスが向上しますが、メモリ消費が増加し、極端な状況ではメモリ不足に陥る場合があります。
* **TTL** は、レポートデータがキャッシュされる時間（秒単位）を定義します。数値を大きくするとパフォーマンスが向上しますが、期間内にデータが変更された場合は不正確なデータが返される場合もあります。
* **最大エントリ数**&#x200B;は、一度にキャッシュできるレポートの最大数を定義します。

>[!NOTE]
>
>レポートデータは、ユーザーと言語ごとに異なる場合があります。したがって、レポートデータは、レポート、ユーザーおよび言語ごとにキャッシュされます。 これは、`2` の&#x200B;**最大エントリ数**&#x200B;の値が、実際には次のいずれかのデータをキャッシュすることを意味します。
>
>* 言語設定が異なる 2 人のユーザー向けの 1 つのレポート
>* 1 人のユーザーと 2 つのレポート
>
