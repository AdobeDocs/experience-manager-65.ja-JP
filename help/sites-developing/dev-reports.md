---
title: レポートの開発
seo-title: レポートの開発
description: AEM には、レポートフレームワークに基づく様々な標準レポートが用意されています。
seo-description: AEM には、レポートフレームワークに基づく様々な標準レポートが用意されています。
uuid: 1b406d15-bd77-4531-84c0-377dbff5cab2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 50fafc64-d462-4386-93af-ce360588d294
translation-type: tm+mt
source-git-commit: ea6da2b75cce4052211fb8f0793f1f380eb85a20
workflow-type: tm+mt
source-wordcount: '5252'
ht-degree: 48%

---


# レポートの開発{#developing-reports}

AEMは、[標準レポート](/help/sites-administering/reporting.md)を選択し、そのほとんどがレポートフレームワークに基づいています。

このフレームワークを使用して、これらの標準レポートを拡張することも、まったく新規のレポートを独自に開発することもできます。このレポートフレームワークは、既存のCQ5の概念や原則と密接に統合されているので、開発者は、CQ5に関する既存の知識をレポート作成の基盤として利用できます。

AEMで配信される標準レポートの場合：

* これらのレポートは、レポートのフレームワークに基づいて構築されています。

   * [コンポーネントのレポート](/help/sites-administering/reporting.md#component-report)
   * [ページアクティビティレポート](/help/sites-administering/reporting.md#page-activity-report)
   * [ユーザーレポート](/help/sites-administering/reporting.md#user-report)
   * [ワークフローインスタンスレポート](/help/sites-administering/reporting.md#workflow-instance-report)

* 以下のレポートは、個々の原則に基づいているため、拡張できません。

   * [ディスク使用量](/help/sites-administering/reporting.md#disk-usage)
   * [ヘルスチェック](/help/sites-administering/reporting.md#health-check)
   * [ワークフローレポート](/help/sites-administering/reporting.md#workflow-report)

>[!NOTE]
>
>[独自のレポートの作成 - 例](#creating-your-own-report-an-example)のチュートリアルでも、以下で説明する原理のうち使用できるものを示しています。
>
>標準レポートを参照し、他の実装例を確認することもできます。

>[!NOTE]
>
>以下の例と定義では、次の表記が使用されます。
>
>* 各行は、次のようなノードまたはプロパティを定義します。
   >
   >  
* `N:<name> [<nodeType>]`
   >
   >     
   `<*name*>`の名前と&#x200B;`<*nodeType*>`*のノードタイプを持つノードを記述します。*
   >
   >  
* `P:<name> [<propertyType]`
   >
   >     
   `<*name*>`という名前と`<*propertyType*>`というプロパティタイプを持つプロパティについて説明します。
   >
   >  
* `P:<name> = <value>`
   >
   >     
   `<value>`の値に設定する必要があるプロパティ`<name>`を説明します。
   >
   >
* インデントは、ノード間の階層的依存関係を示します。
>* 次で区切られた項目 |は、可能な項目のリストを表します。例えば、タイプまたは名前は次のとおりです。

>
>  
例えば`String|String[]`は、プロパティがStringまたはString[]のいずれかであることを意味します。
>
>* `[]` 配列を表す例えば、[] Stringや、 [クエリ定義のようなノードの配列](#query-definition)。
>
>
特に説明がない限り、デフォルトのタイプは次のとおりです。
>
>* ノード数 - `nt:unstructured`
>* プロパティ - `String`


## レポートフレームワーク {#reporting-framework}

レポートフレームワークは、次のような原理で使用されます。

* CQ5 QueryBuilder が実行するクエリによって返される結果セットに、完全に基づいています。
* 結果セットは、レポートに表示するデータを定義します。 結果セットの各行は、レポートの表形式表示の行に対応しています。
* 結果セットに対して実行できる操作は、RDBMSの概念に似ています。主に&#x200B;*グループ化*&#x200B;と&#x200B;*集計*&#x200B;です。

* データの取得と処理は、ほとんどサーバー側でおこなわれます。
* クライアントは、事前に処理されたデータの表示のみを担当します。 小さな処理タスク（例えば、セルのコンテンツ内にリンクを作成する場合など）のみがクライアント側で実行されます。

レポートフレームワーク（標準レポートの構造で示される）では、次の構成要素を使用して処理キューが供給します。

![chlimage_1-248](assets/chlimage_1-248.png)

### レポートページ {#report-page}

レポートページ：

* は標準のCQ5ページです。
* [レポート用に設定された CQ5 の標準テンプレート](#report-template)に基づいています。

### レポートベース  {#report-base}

[`reportbase` コンポーネント](#report-base-component)は、次のようにすべてのレポートの基礎となるものです。

* 基になる結果セットのデータを提供する[クエリ](#the-query-and-data-retrieval)の定義を保持します。

* は、レポートに追加されるすべての列(`columnbase`)を含む、適応した段落システムです。
* 使用可能なチャートタイプおよび現在アクティブなチャートタイプを定義します。
* ユーザーがレポートの特定の側面を設定できる[編集]ダイアログを定義します。

### 列ベース {#column-base}

各列は、[ `columnbase`コンポーネント](#column-base-component)のインスタンスです。

* は、各レポートのparsys ( `reportbase` )で使用される段落です。
* [基になる結果セット](#the-query-and-data-retrieval)へのリンクを定義します。例：この結果セット内で参照される特定のデータと、その処理方法を定義します。
* 追加の定義を保持します。集計やフィルター、およびデフォルト値など。

### クエリとデータの取得  {#the-query-and-data-retrieval}

クエリの概要は次のとおりです。

* [`reportbase`](#report-base) コンポーネントの一部として定義されます。
* [CQ QueryBuilder](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/search/QueryBuilder.html) に基づいています。
* レポートの基準として使用するデータを取得します。 結果セット（テーブル）の各行が、ノードに 1 つずつ関連付けられ、クエリから返されます。次に、[個々の列](#column-base-component)に対する固有情報をこのデータセットから抽出する。

* 通常、次のデータから構成されます。

   * ルートパス。

      これにより、検索対象とするリポジトリのサブツリーが指定されます。

      パフォーマンスの低下を最小限にするため、クエリの対象をリポジトリの特定のサブツリーになるべく制限することをお勧めします。このルートパスは、[レポートテンプレート](#report-template)で事前定義するか、または[設定（編集）ダイアログ](#configuration-dialog)でユーザーが設定することができます。

   * [1 つ以上の条件](#query-definition)。

      これらは、（最初の）結果セットの生成時に適用されます。ノードタイプの制限や、プロパティの制限などがあります。

**重要な点は、クエリの結果セットに返されるノードを 1 つ使用して、レポートの行が 1 つ生成される（ノードと行は 1 対 1 の関係にある）ことです。**

開発者は、レポートに対して定義したクエリによって、そのレポートに適切なノードセットが返されることを確認する必要があります。ただし、ノード自体に必要なすべての情報を保持する必要はなく、親ノードや子ノードから派生させることもできます。 例えば、[ユーザーレポート](/help/sites-administering/reporting.md#user-report)で使用されるクエリでは、ノードタイプ（この場合は `rep:user`）に基づいてノードが選択されます。ただし、このレポートのほとんどの列は、これらのノードから直接データを受け取るのではなく、子ノード`profile`からデータを受け取ります。

### Processing Queue {#processing-queue}

[クエリ](#the-query-and-data-retrieval)によって返される結果セットのデータが、レポート上で行として表示されます。結果セットの各行は、（サーバー側の）[いくつかのフェーズ](#phases-of-the-processing-queue)で処理をおこなってから、クライアントに転送され、レポートに表示されます。

次のような操作が可能です。

* 基になる結果セットからの複数の値の抽出や取得。

   例えば、2 つのプロパティ値の差を計算することで、その 2 つの値を 1 つの値として処理できます。

* 抽出した値の解決。様々な方法でおこなうことができます。

   例えば、パスをタイトル（対応する *jcr:title* プロパティの、わかりやすいコンテンツ）にマップできます。

* 様々なポイントでのフィルターの適用
* 必要に応じて、複合値を作成します。

   例えば、ユーザーに表示されるテキストから、値を作成してソートに使用したり、追加の URL を作成して（クライアント側で）リンクの作成に使用したりできます。

#### 処理キューのワークフロー {#workflow-of-the-processing-queue}

処理キューのワークフローを以下に示します。

![chlimage_1-249](assets/chlimage_1-249.png)

#### 処理キューのフェーズ {#phases-of-the-processing-queue}

具体的な手順と要素は次のとおりです。

1. [初期クエリ(reportbase)](#query-definition)から返された結果を、値抽出を使用して基本的な結果セットに変換します。

   値抽出は、[列のタイプ](#column-specific-definitions)によって自動的に選択されます。値抽出を使用して、基になる JCR クエリから値を読み取り、その値から結果セットを作成し、その後の処理で適用できるようにします。例えば、`diff`型の場合、値抽出器は2つのプロパティを読み取り、1つの値を計算して結果セットに追加します。 値抽出機能を構成できません。

1. 生データを含むこの初期結果セットに、[初期フィルター](#column-specific-definitions)（*raw* フェーズ）が適用されます。

1. *apply* フェーズの定義に従い、値が[前処理](#processing-queue)されます。

1. 前処理された値に対して、[フィルタリング](#column-specific-definitions)（*preprocessed* フェーズに割り当てられています）が実行されます。

1. [指定されたリゾルバー](#processing-queue)によって、値が解決されます。
1. 解決された値に対して、[フィルタリング](#column-specific-definitions)（*resolved* フェーズに割り当てられています）が実行されます。

1. データは[グループ化され、集計](#column-specific-definitions)です。
1. 配列データは、（文字列ベースの）リストに変換することで解決されます。

   この手順は、複数の値を持つ結果をリストに変換して表示できるようにする暗黙の手順です。複数の値を持つ JCR プロパティに基づいた（集計されていない）セル値が必要です。

1. 値は再び[前処理済み](#processing-queue)です。を設定します。**

1. データは並べ替えられます。
1. 処理済みデータはクライアントに転送される。

>[!NOTE]
>
>基になるデータの結果セットを返す初期クエリは、`reportbase` コンポーネントで定義されます。
>
>処理キューの他の要素は、`columnbase`コンポーネントに定義されます。

## レポートの構成と設定 {#report-construction-and-configuration}

レポートの構成および設定には、次の要素が必要です。

* [独自のレポートコンポーネントの定義で使用する場所](#location-of-report-components)
* [ `reportbase`コンポーネント](#report-base-component)
* 1 つ以上の [`columnbase` コンポーネント](#column-base-component)
* [ページコンポーネント](#page-component)
* [レポートデザイン](#report-design)
* [レポートテンプレート](#report-template)

### レポートコンポーネントの場所  {#location-of-report-components}

デフォルトのレポートコンポーネントは`/libs/cq/reporting/components`の下に保持されます。

ただし、これらのノードは更新しないで、`/apps/cq/reporting/components`以下に独自のコンポーネントノードを作成するか、それ以上の適切な`/apps/<yourProject>/reports/components`を作成することを強くお勧めします。

定義（例）は次のとおりです。

```
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:components [sling:Folder]
```

この下にレポートのルートを作成し、このルート下にレポートベースコンポーネントおよび列ベースコンポーネントを作成します。

```
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:components [sling:Folder]
                N:<reportname> [sling:Folder]
                        N:<reportname> [cq:Component]  // report base component
                        N:<columnname> [cq:Component]  // column base component
```

### ページコンポーネント {#page-component}

レポートページは`/libs/cq/reporting/components/reportpage`の`sling:resourceType`を使用する必要があります。

ページコンポーネントのカスタマイズは、（ほとんどの場合）必要ありません。

## レポートベースコンポーネント  {#report-base-component}

各レポートタイプには、`/libs/cq/reporting/components/reportbase`から派生したコンテナコンポーネントが必要です。

このコンポーネントは、レポート全体のコンテナとして使用され、次の情報が含まれます。

* [クエリ定義](#query-definition)。
* レポート設定用の[（オプションの）ダイアログ](#configuration-dialog)。
* レポートに組み込まれる[チャート](#chart-definitions)。

```
N:<reportname> [cq:Component]
    P:sling:resourceSuperType = "cq/reporting/components/reportbase"
    N:charting
    N:dialog [cq:Dialog]
    N:queryBuilder
```

### クエリ定義  {#query-definition}

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

   特定のプロパティと値を持つノードのみを結果セットに含める場合に使用できます。複数の制限が指定された場合、含まれるノードはこれらすべての制限を満たす（AND 演算による）必要があります。

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

   `admin`ユーザーが最後に変更した`textimage`コンポーネントをすべて返します。

* `nodeTypes`

   指定したノードタイプのみを結果セットに含める場合に使用します。複数のノードタイプを指定できます。

* `mandatoryProperties`

   指定したプロパティをすべて持つノードのみを結果セットに含める場合に使用できます。**&#x200B;プロパティの値は考慮されません。

すべてはオプションで、必要に応じて組み合わせることができますが、少なくとも1つは定義する必要があります。

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

   アクティブなグラフの定義を保持します。

   * `active`

      複数の設定を定義できるので、これを使用して現在アクティブなノードを定義できます。これらはノードの配列によって定義されます（これらのノードに必須の命名規則はありませんが、標準のレポートでは通常`0`, `1`.. `x`が使用されます）。それぞれに次のプロパティがあります。

      * `id`

         アクティブなグラフのID。 チャート定義（`definitions`）のいずれかのチャートの ID に一致する必要があります。

* `definitions`

   レポートでの使用が可能なチャートタイプを定義します。`definitions` のうち使用されるタイプが、`active` で指定されます。

   定義はノードの配列（再び`0`、`1`... `x`という名前）を使用して指定され、それぞれ次のプロパティを持ちます。

   * `id`

      グラフID。

   * `type`

      使用できるグラフの種類です。 次から選択：

      * `pie`円グラフ。現在のデータからのみ生成されます。

      * `lineseries`線系列（実際のスナップショットを表す点をつないだもの）履歴データからのみ生成されます。
   * グラフのタイプに応じて、次の追加のプロパティを使用できます。

      * グラフのタイプ`pie`:

         * `maxRadius`（`Double/Long`）

            この円グラフで許容される半径の最大値、つまりこのチャートで許容される最大サイズ（凡例を使用しない場合）。`fixedRadius`が定義されている場合は無視されます。

         * `minRadius`（`Double/Long`）

            円グラフに許可する最小半径です。 `fixedRadius`が定義されている場合は無視されます。

         * `fixedRadius` (  `Double/Long`)円グラフの固定半径を定義します。
      * グラフのタイプ[`lineseries`](/help/sites-administering/reporting.md#display-limits):

         * `totals`（`Boolean`）

            **Total**を示す追加の行を表示する場合はtrueです。
デフォルト値: `false`

         * `series`（`Long`）

            表示する行/系列の数。
デフォルト：`9`（この値は許容される最大値です）

         * `hoverLimit`（`Long`）

            ポップアップが表示される集計スナップショット（各横線に表示されるドット。それぞれの値は異なる値を表す）の最大数。例えば、グラフの凡例内の別の値や対応するラベルにマウスを移動したときに表示されます。

            デフォルト：`35`（現在のチャート設定で適用される個別の値が 35 個を超える場合は、ポップアップが表示されません）。

            このほかに、同時表示できるポップアップ数（凡例のテキストにマウスオーバーしたときに表示できる複数のポップアップ）を 10 個までに制限できます。



### 設定ダイアログ {#configuration-dialog}

各レポートには設定ダイアログを設定でき、ユーザーはレポートの様々なパラメーターを指定できます。 このダイアログには、レポートページが開いているときに「**編集**」ボタンを使用してアクセスできます。

このダイアログは標準のCQ [ダイアログ](/help/sites-developing/components-basics.md#dialogs)であり、このように設定できます（詳しくは[CQ.Dialog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Dialog)を参照）。

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

   レポートタイトルを定義するテキストフィールド

* **`description`**

   `/libs/cq/reporting/components/commons/description`

   レポートの説明を定義するテキスト領域。

* **`processing`**

   `/libs/cq/reporting/components/commons/processing`

   レポートの処理モード（データを手動または自動で読み込む）のセレクター。

* **`scheduling`**

   `/libs/cq/reporting/components/commons/scheduling`

   履歴グラフのスナップショットをスケジュールするためのセレクターです。

>[!NOTE]
>
>参照されるコンポーネントは、`.infinity.json`サフィックスを使用して含める必要があります（上の例を参照）。

### ルートパス {#root-path}

このほか、レポートのルートパスを指定することもできます。

* **`rootPath`**

   レポートの対象を、リポジトリの特定のセクション（ツリーまたはサブツリー）に限定できます。パフォーマンスの最適化のために、限定することをお勧めします。このルートパスは、各レポートページの `rootPath` ノードの `report` プロパティで指定します（ページの作成時、テンプレートから取得されます）。

   次の方法で指定できます。

   * [レポートテンプレート](#report-template)（固定値または設定ダイアログのデフォルト値）。
   * ユーザー（このパラメーターを使用）

## 列ベースコンポーネント  {#column-base-component}

各列タイプには、`/libs/cq/reporting/components/columnbase`から派生するコンポーネントが必要です。

列コンポーネントは、次の組み合わせを定義します。

* [列固有のクエリ](#column-specific-query)の設定。
* [リゾルバーと前処理](#resolvers-and-preprocessing)。
* [列固有の定義](#column-specific-definitions)（フィルターや集計など。`definitions` の子ノード）。
* [列のデフォルト値](#column-default-values)。
* サーバーによって返されるデータから、表示する情報を抽出するための[クライアントフィルター](#client-filter)。
* 以上のほか、列コンポーネントの `cq:editConfig` で適切なインスタンスを指定し、必要な[イベントとアクション](#events-and-actions)を指定する必要があります。
* [一般列](#generic-columns)の設定。

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

### 列固有のクエリ  {#column-specific-query}

個別の列で使用する特定のデータを（[レポートデータの結果セット](#the-query-and-data-retrieval)から）抽出する方法を定義します。

```xml
N:definitions
    N:queryBuilder
        P:property [String|String[]]
        P:subPath
        P:secondaryProperty [String|String[]]
        P:secondarySubPath
```

* `property`

   セルの実値の計算に使用するプロパティを指定します。

   プロパティがString[]として定義されている場合、実際の値を見つけるために複数のプロパティが（順に）スキャンされます。

   例えば、次の場合：

   `property = [ "jcr:lastModified", "jcr:created" ]`

   対応する値抽出器（ここでは制御可能）は、次の処理を行います。

   * 有効な jcr:lastModified プロパティが存在するかどうかを確認し、存在する場合はそのプロパティを使用します。
   * jcr:lastModifiedプロパティを使用できない場合は、jcr:createdのコンテンツが代わりに使用されます。

* `subPath`

   クエリによって返されるノードに結果を配置しない場合、このプロパティを実際に配置する場所を `subPath` で指定します。

* `secondaryProperty`

   セルの実値の計算に必要な、2 つ目のプロパティを定義します。このプロパティは、特定の列のタイプ（diff および sortable）でのみ使用されます。

   例えばワークフローインスタンスレポートの場合、開始時間と終了時間の時間差（ミリ秒単位）の実値を格納するときに使用するプロパティを指定できます。

* `secondarySubPath`

   subPathと同様、`secondaryProperty`が使用される場合。

ほとんどの場合、`property` のみを使用します。

### クライアントフィルター {#client-filter}

クライアントフィルタは、サーバから返されたデータから表示する情報を抽出する。

>[!NOTE]
>
>このフィルタは、サーバー側処理全体が適用された後に、clientsideで実行されます。

```xml
N:definitions
    N:data
        P:clientFilter [String]
```

`clientFilter` は、JavaScript 関数として、次のように定義されます。

* を入力として受け取る場合、1つのパラメータが受け取られます。サーバーから返されるデータ（処理が完全に行われている）
* 出力時、フィルターを適用した後の（処理後の）値を返します。返すデータは、入力時のデータから抽出または取得したものです。

次の例では、コンポーネントのパスから対応するページパスが抽出されます。

```
function(v) {
    var sepPos = v.lastIndexOf('/jcr:content');
    if (sepPos < 0) {
        return v;
    }
    return v.substring(sepPos + '/jcr:content'.length, v.length);
}
```

### リゾルバーと前処理  {#resolvers-and-preprocessing}

[処理キュー](#processing-queue)で様々なリゾルバーを指定し、前処理を設定します。

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

   使用するリゾルバーを定義します。 次のリゾルバーを使用できます。

   * `const`

      値を他の値にマップします。例えば `en` などの定数を、対応する値 `English` に解決できます。

   * `default`

      デフォルトのリゾルバーです。 これは実際に何も解決しないダミーリゾルバーです。

   * `page`

      パスの値を、対応するページのパス（正確には、対応する `jcr:content` ノード）に解決します。例えば、`/content/.../page/jcr:content/par/xyz`は`/content/.../page/jcr:content`に解決されます。

   * `path`

      パスの値にオプションとしてサブパスを付加し、解決されたパスにあるノードのプロパティ（`resolverConfig` で指定）から実値を取得することで、パスの値を解決します。例えば、`/content/.../page/jcr:content`の`path`を`jcr:title`プロパティの内容に解決できる場合、これはページパスがページタイトルに解決されることを意味します。

   * `pathextension`

      パスを先頭に付加し、解決されたパスのノードのプロパティから実値を取得することで、値を解決します。例えば、国コード`language`を言語の説明`de`に解決するために、`de`のようなパスの前に`/libs/wcm/core/resources/languages`の値を付加し、プロパティ&lt;a2/>から値を取り出すことができます。`German`

* `resolverConfig`

   リゾルバーの定義をおこないます。以下のうち使用できるオプションは、`resolver` の選択によって決まります。

   * `const`

      プロパティを使用して、解決する定数を指定します。プロパティの名前で、解決する定数を指定します。プロパティの値で、解決後の値を指定します。

      例えば、**Name**= `1`および&#x200B;**Value** `=One`のプロパティは、1を1に解決します。

   * `default`

      設定が利用できません。

   * `page`

      * `propertyName` (オプション)

         値の解決に使用するプロパティの名前を指定します。指定しなかった場合、デフォルト値&#x200B;*jcr:title*（ページタイトル）が使用されます。`page`リゾルバーの場合、これは、最初にパスがページパスに解決され、次にページタイトルに解決されることを意味します。
   * `path`

      * `propertyName` (オプション)

         値の解決に使用するプロパティの名前を指定します。指定しなかった場合は、デフォルト値の`jcr:title`が使用されます。

      * `subPath` (オプション)

         このプロパティは、値を解決する前にパスに付加する接尾辞を指定するときに使用します。
   * `pathextension`

      * `path` (mandatory)

         先頭に付加するパスを指定します。

      * `propertyName` （必須）

         実際の値が存在する解決済みパスのプロパティを定義します。

      * `i18n` （オプション）type Boolean)

         解決された値を&#x200B;*国際化*&#x200B;にするかどうかを決定します（例：[CQ5の国際化サービス](/help/sites-administering/tc-manage.md)を使用します）。



* `preprocessing`

   前処理はオプションであり、処理フェーズ&#x200B;*apply*&#x200B;または&#x200B;*applyAfter*&#x200B;に（個別に）バインドできます。

   * `apply`

      初期の前処理フェーズ（[処理キューの説明での手順 3](#processing-queue)）に適用。

   * `applyAfter`

      前処理後（[処理キューの説明での手順 9](#processing-queue)）に適用。

#### リゾルバー {#resolvers}

リゾルバーは、必要な情報の抽出に使用されます。 様々なリゾルバーの例を以下に示します。

**定数**

次の例では、`VersionCreated`の定数値を文字列`New version created`に解決します。

参照先 `/libs/cq/reporting/components/auditreport/typecol/definitions/data`.

```xml
N:data
    P:resolver=const
    N:resolverConfig
        P:VersionCreated="New version created"
```

**ページ**

パス値を、対応するページのjcr:content（子）ノードのjcr:descriptionプロパティに解決します。

参照先 `/libs/cq/reporting/components/compreport/pagecol/definitions/data`.

```xml
N:data
    P:resolver=page
    N:resolverConfig
        P:propertyName="jcr:description"
```

**パス**

次の例では、`/content/.../page`のパスを`jcr:title`プロパティの内容に解決します。これは、ページパスがページタイトルに解決されることを意味します。

参照先 `/libs/cq/reporting/components/auditreport/pagecol/definitions/data`.

```xml
N:data
    P:resolver=path
    N:resolverConfig
        P:propertyName="jcr:title"
        P:subPath="/jcr:content"
```

**パスの拡張子**

次の例では、パス拡張子`/libs/wcm/core/resources/languages`の付いた値`de`の前に値&lt;a1/>を付け、プロパティ`language`から値を取り、国コード`de`を言語の説明`German`に解決します。

参照先 `/libs/cq/reporting/components/userreport/languagecol/definitions/data`.

```xml
N:data
    P:resolver=pathextension
    N:resolverConfig
        P:path="/libs/wcm/core/resources/languages"
        P:propertyName="language"
```

#### 前処理 {#preprocessing}

`preprocessing` の定義は、次のどちらかに適用できます。

* 元の値：

   元の値の前処理定義は、`apply`および/または`applyAfter`に直接指定されます。

* の値を集計した状態で表示します。

   必要に応じて、集計ごとに別々の定義を指定できます。

   集計値の明示的な前処理を指定するには、前処理定義はそれぞれの`aggregated`子ノード( `apply/aggregated`, `applyAfter/aggregated`)に存在する必要があります。 個別の集計に対して、前処理を明示的に指定する必要がある場合は、各集計の名前が付いた子ノード（例えば `apply/aggregated/min/max` などの集計）で前処理の定義をおこなう必要があります。

前処理中に使用する次のいずれかを指定できます。

* [パターンの検索と置換](#preprocessing-find-and-replace-patterns)検索後、指定したパターン（正規表現として指定）を他のパターンに置き換えます。例えば、元の値からサブ文字列を抽出するときに使用できます。

* [データ型フォーマッタ](#preprocessing-data-type-formatters)

   数値を相対文字列に変換します。例えば、1時間の時差を表す値「」は、`1:24PM (1 hour ago)`のような文字列に解決されます。

次に例を示します。

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

#### 前処理 - パターンの検索と置換  {#preprocessing-find-and-replace-patterns}

前処理の場合は、`pattern`([正規式](https://en.wikipedia.org/wiki/Regular_expression)またはregexとして定義)を指定して配置し、`replace`パターンで置き換えます。

* `pattern`

   サブ文字列の検索に使用する正規表現。

* `replace`

   元の文字列の置き換えに使用する文字列、または文字列の表現。通常、`pattern` の正規表現によって検索される文字列のサブ文字列を示します。

置換の例は、次のように分類できます。

* 次の2つのプロパティを持つノード`definitions/data/preprocessing/apply`の場合：

   * `pattern`: `(.*)(/jcr:content)(/|$)(.*)`
   * `replace`:  `$1`

* 次のような文字列が検索されます。

   * `/content/geometrixx/en/services/jcr:content/par/text`

* 次の4つのセクションに分類されます。

   * `$1` -  `(.*)` -  `/content/geometrixx/en/services`
   * `$2` -  `(/jcr:content)` -  `/jcr:content`
   * `$3` -  `(/|$)` -  `/`
   * `$4` -  `(.*)` -  `par/text`

* `$1`で表される文字列に置き換えます。

   * `/content/geometrixx/en/services`

#### 前処理 - データタイプフォーマッター {#preprocessing-data-type-formatters}

これらのフォーマッタは、数値を相対文字列に変換します。

例えば、`min`、`avg`、`max`集計を許可する時間列に使用できます。 `min`/ `avg`/ `max`集計は&#x200B;*時間差*&#x200B;として表示されます(例：`10 days ago`)の場合は、データフォーマッタが必要です。 この場合、`datedelta`フォーマッタが`min`/ `avg`/ `max`集計された値に適用されます。 `count`集計も利用できる場合は、フォーマッタは不要で、元の値も必要ありません。

現在、使用できるデータ型フォーマッタは次のとおりです。

* `format`

   データタイプフォーマッター：

   * `duration`

      期間は、2つの定義された日付の間の時間です。 例えば、ワークフローアクションの開始から終了までの時間を 1 時間とした場合、開始を 2011 年 2 月 13 日 11 時 23 分とすると、終了は 1 時間後の 2011 年 2 月 13 日 12 時 23 分となります。

      数値（ミリ秒として解釈）を期間文字列に変換します。例えば、`30000`の形式は* `30s`です。*

   * `datedelta`

      過去の日付から「現在」までのタイムスパンです（したがって、レポートを後の時点で表示すると、結果が異なります）。

      数値（日単位の時間差として解釈）が、対応する日付の文字列に変換されます。例えば、1 という値は 1 日前にフォーマットされます。

次の例は、`min`と`max`集計の`datedelta`フォーマットを定義しています。

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

列固有の定義は、その列で使用できるフィルターや集計を指定するものです。

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

   標準オプションとして使用できるものは次のとおりです。

   * `string`
   * `number`
   * `int`
   * `date`
   * `diff`
   * `timeslot`

      日付から、集計に必要な部分を抽出する場合（例えば年でグループ化し、年ごとに集計したデータを取得する場合）に使用します。

   * `sortable`

      異なる値（異なるプロパティの値）を使用してソートし、表示できる値に適用します。
   それに加えて. 上記のいずれかを複数の値として定義できます。例えば、`string[]`は文字列の配列を定義します。

   値抽出は、列のタイプによって選択されます。値抽出器が列タイプで使用可能な場合は、この抽出器が使用されます。 それ以外の場合は、デフォルト値抽出が使用されます。

   タイプには、（オプションとして）パラメーターを指定できます。例えば、`timeslot:year`は日付フィールドから年を抽出します。 パラメータを含むタイプ：

   * `timeslot`  — 値は、の対応する定数と比較でき `java.utils.Calendar`ます。

      * `timeslot:year` - `Calendar.YEAR`
      * `timeslot:month-of-year` -  `Calendar.MONTH`
      * `timeslot:week-of-year` -  `Calendar.WEEK_OF_YEAR`
      * `timeslot:day-of-month` -  `Calendar.DAY_OF_MONTH`
      * `timeslot:day-of-week` -  `Calendar.DAY_OF_WEEK`
      * `timeslot:day-of-year` -  `Calendar.DAY_OF_YEAR`
      * `timeslot:hour-of-day` -  `Calendar.HOUR_OF_DAY`
      * `timeslot:minute-of-hour` -  `Calendar.MINUTE`


* `groupable`

   レポートをこの列でグループ化できるかどうかを指定します。

* `filters`

   フィルターの定義。

   * `filterType`

      次のフィルターを使用できます。

      * `string`

         文字列ベースのフィルター。
   * `id`

      フィルター識別子。

   * `phase`

      利用可能なフェーズ：

      * `raw`

         フィルターは生データに適用されます。

      * `preprocessed`

         フィルターは、事前に処理されたデータに適用されます。

      * `resolved`

         フィルターは解決されたデータに適用されます。


* `aggregates`

   集計の定義。

   * `text`

      集計のテキスト名。 `text` の指定がない場合、集計のデフォルトの説明が使用されます。例えば `minimum` 集計の場合、`min` が使用されます。

   * `type`

      集計タイプ。 次の集計を使用できます。

      * `count`

         行数を数えます。

      * `count-nonempty`

         空でない行の数を数えます。

      * `min`

         最小値を指定します。

      * `max`

         最大値を指定します。

      * `average`

         平均値を示します。

      * `sum`

         すべての値の合計を示します。

      * `median`

         中央値を示します。

      * `percentile95`

         各値の 95 パーセンタイル値を求めます。

### 列のデフォルト値 {#column-default-values}

列のデフォルト値の定義を次に示します。

```xml
N:defaults
    P:aggregate
```

* `aggregate`

   有効な`aggregate`値は、`aggregates`の下の`type`と同じです([列固有の定義(定義 —フィルター/集計)](#column-specific-definitions)を参照)。

### イベントおよびアクション {#events-and-actions}

編集設定を使用して、リスナーが検出する必要のあるイベントおよびそのイベント発生後に適用するアクションを定義できます。背景情報については、[コンポーネント開発の概要](/help/sites-developing/components.md)を参照してください。

必要なアクションがすべて実行されるようにするには、次の値を指定します。

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

### 一般列 {#generic-columns}

汎用列は、列定義の（ほとんどの）が、（コンポーネントノードではなく）列ノードのインスタンスに格納される拡張です。

各汎用コンポーネントには、カスタマイズした（標準）ダイアログが使用されます。 このダイアログを使用して、レポートのユーザーがレポートページ上の一般列のプロパティを指定できます（「**列のプロパティ...**」のメニューオプションを使用）。

例えば、**ユーザーレポート**&#x200B;の&#x200B;**汎用**&#x200B;列です。`/libs/cq/reporting/components/userreport/genericcol`を参照してください。

列を汎用にするには：

* 列の`definition`ノードの`type`プロパティを`generic`に設定します。

   参照先 `/libs/cq/reporting/components/userreport/genericcol/definitions`

* 列の `definition` ノードで、（標準）ダイアログの定義をおこないます。

   参照先 `/libs/cq/reporting/components/userreport/genericcol/definitions/dialog`

   * ダイアログのフィールドが、対応するコンポーネントプロパティと同じ名前（パスを含む）を参照する必要があります。

      例えば、ダイアログで汎用列のタイプを設定可能にする場合は、`./definitions/type`という名前のフィールドを使用します。

   * UI（ダイアログ）を使用して指定されるプロパティは、`columnbase` コンポーネントで指定されるプロパティより優先されます。

* 編集設定を定義します。

   参照先 `/libs/cq/reporting/components/userreport/genericcol/cq:editConfig`

* 標準的なAEM手法を使用して、列のプロパティを定義します（追加）。

   プロパティがコンポーネントインスタンスと列インスタンスの両方で指定されている場合、列インスタンスの値が優先されることに注意してください。

   一般列で使用できるプロパティは次のとおりです。

   * `jcr:title`  — 列名
   * `definitions/aggregates` -集計
   * `definitions/filters` - filters
   * `definitions/type` — 列のタイプ（セレクター/コンボボックスまたは非表示フィールドを使用して、ダイアログで定義する必要があります）
   * `definitions/data/resolver` および `definitions/data/resolverConfig` (でも `definitions/data/preprocessing` または `.../clientFilter`) — リゾルバと設定
   * `definitions/queryBuilder` -クエリビルダーの設定
   * `defaults/aggregate`  — デフォルトの集計

   「**ユーザーレポート**」の一般列に新しいインスタンスを作成した場合、ダイアログで指定されるプロパティは次の場所に保持されます。

   `/etc/reports/userreport/jcr:content/report/columns/genericcol/settings/generic`

## レポートデザイン {#report-design}

デザインによって、レポートの作成に使用できる列のタイプが定義されます。 列を追加する段落システムも定義します。

各レポートに個別のデザインを作成することを強くお勧めします。 これにより、最大限の柔軟性が確保されます。 [新規レポートの定義](#defining-your-new-report)も参照してください。

デフォルトのレポートコンポーネントは`/etc/designs/reports`の下に保持されます。

レポートの格納場所は、独自のコンポーネントを配置した場所によって次のいずれかになります。

* `/etc/designs/reports/<yourReport>` が  `/apps/cq/reporting`

* `/etc/designs/<yourProject>/reports/<*yourReport*>` ( `/apps/<yourProject>/reports` パターンを使用したレポート用)

必要なデザインプロパティは`jcr:content/reportpage/report/columns`に登録されます（例：`/etc/designs/reports/<reportName>/jcr:content/reportpage/report/columns`）:

* `components`

   レポートで使用できるコンポーネントやコンポーネントグループ。

* `sling:resourceType`

   値`cq/reporting/components/repparsys`のプロパティ。

デザインスニペットの例を次に示します（コンポーネントレポートのデザインから取得）。

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

個々の列に対してデザインを指定する必要はありません。 使用可能な列はデザインモードで定義できます。

>[!NOTE]
>
>標準のレポートデザインは変更しないことをお勧めします。 これは、ホットフィックスのアップグレードやインストール時に変更が失われないようにするためです。
>
>標準レポートをカスタマイズする場合は、レポートとそのデザインをコピーしてください。

>[!NOTE]
>
>デフォルトの列は、レポートの作成時に自動的に作成できます。 これらはテンプレートで指定されます。

## レポートテンプレート  {#report-template}

各レポートタイプは、テンプレートを提供する必要があります。 これらは標準の[CQテンプレート](/help/sites-developing/templates.md)で、そのように設定できます。

テンプレートは次の条件を満たす必要があります。

* `sling:resourceType`を`cq/reporting/components/reportpage`に設定

* 使用する設計を示す
* `sling:resourceType`プロパティを使用してコンテナ(`reportbase`)コンポーネントを参照する`report`子ノードを作成します

テンプレートスニペットの例を以下に示します（コンポーネントレポートテンプレートから取得）。

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

（ユーザーレポートテンプレートから取得された）ルートパスの定義を示すテンプレートスニペットの例を以下に示します。

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

デフォルトのレポートテンプレートは`/libs/cq/reporting/templates`の下に保持されます。

ただし、これらのノードは更新しないで、`/apps/cq/reporting/templates`以下に独自のコンポーネントノードを作成するか、それ以上の適切な`/apps/<yourProject>/reports/templates`を作成することを強くお勧めします。

定義例は次のとおりです（[レポートコンポーネントの場所](#location-of-report-components)も参照）。

```xml
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:templates [sling:Folder]
```

この場所に、テンプレートのルートを作成します。

```xml
N:apps
    N:cq [nt:folder]
        N:reporting|reports [sling:Folder]
            N:templates [sling:Folder]
                N:<reportname> [sling:Folder]
```

## 独自のレポートの作成 - 例 {#creating-your-own-report-an-example}

### 新しいレポートの定義 {#defining-your-new-report}

新しいレポートを定義するには、以下を作成して設定する必要があります。

1. レポートコンポーネントのルート
1. レポートベースコンポーネント
1. 1 つ以上の列ベースコンポーネント
1. レポートデザイン
1. レポートテンプレートのルート
1. レポートテンプレート

これらの手順を説明するために、次の例では、リポジトリ内のすべてのOSGi設定をリストするレポートを定義します。例えば、`sling:OsgiConfig`ノードのすべてのインスタンスです。

>[!NOTE]
>
>既存のレポートをコピーして新しいバージョンにカスタマイズすることもできます。

1. 新しいレポートのルートノードを作成します。

   例えば、`/apps/cq/reporting/components/osgireport`の下にあります。

   ```xml
   N:cq [nt:folder]
       N:reporting [sling:Folder]
           N:components [sling:Folder]
               N:osgireport [sling:Folder]
   ```

1. レポートベースを定義します。例えば、`/apps/cq/reporting/components/osgireport`の下に`osgireport[cq:Component]`があります。

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

   これは、次のようなレポートベースのコンポーネントを定義します。

   * タイプ`sling:OsgiConfig`のすべてのノードを検索
   * `pie`グラフと`lineseries`グラフの両方を表示
   * ユーザーがレポート設定できるダイアログを提供する

1. 最初の列（columnbase）コンポーネントを定義します。例えば、`/apps/cq/reporting/components/osgireport`の下に`bundlecol[cq:Component]`があります。

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

   これは、次のような列の基本コンポーネントを定義します。

   * サーバーから受信する値（この場合、`jcr:path` の各ノードの `sling:OsgiConfig` プロパティ）を検索し、その値を返す
   * `count`集計を提供
   * グループ化はできない
   * タイトル（テーブル内の列タイトル）は `Bundle`
   * はサイドキックグループ`OSGi Report`にあります
   * 指定のイベントで更新される

   >[!NOTE]
   >
   >この例では、`N:data`と`P:clientFilter`の定義はありません。 これは、サーバーから受け取った値が1:1単位で返されるためです（デフォルトの動作）。
   >
   >これは定義と同じです。
   >
   >
   ```
   >N:data [nt:unstructured]
   >   P:clientFilter [String] = "function(v) { return v; }"
   >```
   >
   >関数は受け取った値を返すだけです。

1. レポートデザインを定義します。例えば、`/etc/designs/reports`の下に`osgireport[cq:Page]`があります。

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

   例えば、`/apps/cq/reporting/templates/osgireport`の下にあります。

   ```xml
   N:cq [nt:folder]
       N:reporting [sling:Folder]
           N:templates [sling:Folder]
               N:osgireport [cq:Template]
   ```

1. レポートテンプレートを定義します。例えば、`/apps/cq/reporting/templates`の下に`osgireport[cq:Template]`があります。

   ```xml
   N:osgireport [cq:Template]
       P:allowedPaths [String[]] = "/etc/reports(/.*)?"
       P:jcr:description [String] = "Use this report generator to create a new OSGi report."
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

   * 結果のレポートの`allowedPaths`を定義します。上記の場合は`/etc/reports`以下の任意の場所です。
   * テンプレートのタイトルと説明を指定する
   * テンプレートリストで使用するサムネール画像を指定する（このノードの詳細な定義は表示していません。既存のレポートから thumbnail.png のインスタンスをコピーするのが最も簡単な方法です）。

### 新規レポートのインスタンスの作成 {#creating-an-instance-of-your-new-report}

新しいレポートのインスタンスを、次のように作成できます。

1. **ツール**&#x200B;コンソールを開きます。

1. 左側のウィンドウで、「**レポート**」を選択します。
1. **新しい…**&#x200B;をツールバーから削除します。 **タイトル**&#x200B;と&#x200B;**名前**&#x200B;を定義し、テンプレートのリストから新しいレポートタイプ（**OSGiレポートテンプレート**）を選択し、**作成**&#x200B;をクリックします。
1. 新しいレポートインスタンスがリストに表示されます。 重複をクリックして開きます。
1. サイドキックからコンポーネント（この例では、「**OSGi Report**」グループの「**バンドル**」）をドラッグして最初の列を作成し、[レポートの定義を開始](/help/sites-administering/reporting.md#the-basics-of-report-customization)します。

   >[!NOTE]
   >
   >この例ではグループ化可能な列がないので、グラフは使用できません。 グラフを表示するには、`groupable`を`true`に設定します。
   >
   >
   ```
   >N:osgireport [sling:Folder]
   > N:bundlecol [cq:Component]
   > N:definitions [nt:unstructured]
   > P:groupable [Boolean] = true
   >```

## レポートフレームワークサービスの設定 {#configuring-the-report-framework-services}

この節では、レポートフレームワークの実装に使用する OSGi サービスの高度な設定オプションについて説明します。

これらはWebコンソールのConfigurationメニューを使用して表示できます（`http://localhost:4502/system/console/configMgr`など）。 AEM を操作しているときは、このようなサービスの設定を管理する方法がいくつかあります。詳細および推奨事項については、[OSGi の設定](/help/sites-deploying/configuring-osgi.md)を参照してください。

### 基本サービス（Day CQ レポート設定）  {#basic-service-day-cq-reporting-configuration}

* **** Timezoneは、に対して作成されるタイムゾーン履歴データを定義します。これは、履歴グラフに、世界中の各ユーザーの同じデータが表示されるようにするためです。
* **** Localeは、履歴データに対して **** Timezoneと組み合わせて使用するロケールを定義します。ロケールは、ロケールに固有のカレンダー設定（週の最初の日が日曜日か月曜日かなど）を決定するために使用されます。

* **スナップショット** パスは、履歴グラフのスナップショットが保存されるルートパスを定義します。
* **レポートへのパスは、レポ** ートの配置先のパスを定義します。これは、スナップショットを実際に作成するレポートを決定するために、スナップショットサービスによって使用されます。
* **日別** スナップショットは、日別スナップショットが作成される1日の時間を定義します。指定した時間は、サーバーのローカルタイムゾーンで表します。
* **時間別** スナップショットは、時間別スナップショットが作成される1時間の分を定義します。
* **Rows (max)** は、各スナップショットに格納される最大行数を定義します。この値は適切に選択されるべきです。値が大きすぎると、リポジトリのサイズに影響します。値が小さすぎると、履歴データの処理方法が原因で、データが正確でない場合があります。
* **フェイクデータ**（有効な場合）は、 `fakedata` セレクターを使用して、フェイク履歴データを作成できます。無効にすると、 `fakedata` セレクターを使用した場合、例外がスローされます。

   フェイクデータは、必ずテストおよびデバッグの用途でのみ使用してください。**

   `fakedata` セレクターを使用すると、レポートが暗黙的に終了するので、既存のデータがすべて失われます。データは手動で復元できますが、非常に時間のかかる作業となります。

* 「**Snapshot user**」で、スナップショットの取得に使用できるオプションのユーザーを指定します。

   通常、レポートを終了したユーザーに対してスナップショットが取得されます。例えばパブリッシュシステムで、ユーザーアカウントが複製されていないのでこのユーザーが存在しない場合など、このユーザーの代わりに使用する代替ユーザーの指定が必要な場合があります。

   ただし、ユーザーを指定するとセキュリティリスクが高まる可能性もあります。

* 「**Enforce snapshot user**」を有効にすると、すべてのスナップショットが、「Snapshot user **」で指定したユーザーを使用して取得されます。正しく処理しないと、セキュリティに重大な影響が出る可能性があります。

### キャッシュ設定(Day CQレポートキャッシュ) {#cache-settings-day-cq-reporting-cache}

* **[** 有効]を選択すると、レポートデータのキャッシュを有効または無効にできます。レポートのキャッシュを有効にすると、複数の要求がおこなわれる間、レポートデータがメモリに保持されます。これにより、パフォーマンスが向上しますが、メモリ消費量が増え、極端な状況ではメモリ不足になる可能性があります。
* **** TTLは、レポートデータをキャッシュする時間（秒）を定義します。数値を大きくするとパフォーマンスが向上しますが、期間内にデータが変更された場合は、不正確なデータが返される場合もあります。
* **最大** エントリ数は、一度にキャッシュするレポートの最大数を定義します。

>[!NOTE]
>
>レポートデータは、ユーザーと言語ごとに異なる場合があります。 したがって、レポートデータは、レポート、ユーザー、言語ごとにキャッシュされます。 つまり、**Max entries**&#x200B;値`2`は、次のいずれかのデータを実際にキャッシュします。
>
>* 言語設定が異なる2人のユーザーに対して1つのレポート
>* 1 人のユーザーに対し、2 つのレポート

>



