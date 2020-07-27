---
title: インタラクティブ通信内でグラフを使用する
seo-title: インタラクティブ通信内のグラフコンポーネント
description: 対話型通信でグラフを使用すると、大量の情報を簡単に視覚的な形式を分析できるように要約できます
seo-description: AEM Forms には、インタラクティブ通信内でグラフを作成するためのグラフコンポーネントが用意されています。ここでは、グラフコンポーネントの基本的な設定とエージェント設定について説明します。
uuid: 978aa431-9a5b-4964-b37c-7bfa8c3f49b9
content-type: reference
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e21714ad-d445-4aff-b0db-d577061e0907
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '2646'
ht-degree: 24%

---


# インタラクティブ通信内でグラフを使用する{#using-charts-in-interactive-communications}

表やグラフはデータを視覚的に表現します。インタラクティブ通信で大量の情報を分かりやすい視覚的な形式で表現することにより、複雑なデータを視覚的に理解して分析することができます。

インタラクティブ通信を作成する際にグラフを追加することにより、インタラクティブ通信のフォームデータモデルから取得した 2 次元のデータを視覚的に表現することができます。グラフコンポーネントでは、次のタイプのグラフを追加および設定できます。 円グラフ、列グラフ、ドーナツグラフ、棒グラフ、線グラフ、線とポイントグラフ、点グラフ、面グラフ、四半円グラフ、四半円グラフなどがあります。

## Add and configure chart in an Interactive Communication {#add-and-configure-chart-in-an-interactive-communication}

次の手順を実行して、対話型通信でグラフを追加および設定します。

1. 対話型通信のサイドキックから **「コンポーネント** 」をタップします。
1. 「 **グラフ** 」コンポーネントを次のいずれかのコンポーネントにドラッグ&amp;ドロップします。

   * 印刷チャネル: Target領域または画像フィールド
   * Webチャネル: パネルまたはTarget領域

1. Interactive Communicationエディターでグラフコンポーネントをタップし、コンポーネントツールバーから **[!UICONTROL 設定(]**![configure_icon](assets/configure_icon.png))を選択します。

   左ペインにグラフのプロパティが表示されます。

   ![印刷チャネルの線グラフの基本プロパティ](assets/chart_properties_print_new.png)

   印刷チャネルの線グラフの基本プロパティ

   ![Web チャネルの線グラフの基本プロパティ](assets/chart_properties_web_new.png)

   Web チャネルの線グラフの基本プロパティ

1. チャネルタイプに基づいて [グラフのプロパティ](../../forms/using/chart-component-interactive-communications.md#configure-chart-properties) を設定します。
1. (Print channel only) In the **[!UICONTROL Agent Settings]**, specify if it is mandatory for the agent to use this chart. If i **[!UICONTROL t Is Mandatory For the Agent To Use This Chart]** option is not selected, the agent can tap the eye icon for the chart in the **[!UICONTROL Content]** tab of Agent UI to show or hide the chart.

   ![chart_agentproperties](assets/chart_agentproperties.png)

1. Tap ![done_icon](assets/done_icon.png) to save the chart properties.

   「 **[!UICONTROL プレビュー]** 」をタップして、グラフに関連付けられた外観とデータを表示します。 「 **[!UICONTROL 編集]** 」をタップして、グラフのプロパティを再設定します。

## グラフのプロパティの設定 {#configure-chart-properties}

印刷およびWebチャネル用のグラフを作成する際に、次のプロパティを設定します。

<table>
 <tbody>
  <tr>
   <td>フィールド</td>
   <td>説明</td>
   <td>チャネルタイプ</td>
  </tr>
  <tr>
   <td>名前</td>
   <td>グラフ要素の識別子。 このフィールドで指定したグラフの名前は、グラフに表示されません。 他のコンポーネント、スクリプト、SOM式の要素を参照する場合に使用されます。</td>
   <td>印刷出力と Web 出力</td>
  </tr>
  <tr>
   <td>グラフのタイプ</td>
   <td>生成するグラフのタイプ。 円グラフ、列グラフ、ドーナツグラフ、棒グラフ、線グラフ、線とポイントグラフ、点グラフ、領域グラフのオプションを使用できます。</td>
   <td>印刷出力と Web 出力</td>
  </tr>
  <tr>
   <td>系列/複数系列</td>
   <td>X軸とY軸にプロットされたフォームデータモデルのコレクション項目に対して複数のシリーズを追加する場合に選択します。</td>
   <td>印刷出力と Web 出力</td>
  </tr>
  <tr>
   <td>系列/データモデルオブジェクト</td>
   <td>グラフに複数のシリーズを追加するフォームデータモデルのコレクション項目の名前。<br /> X軸とY軸にプロットされたプロパティに対して親フォームデータモデルオブジェクトプロパティを選択し、意味のある系列を作成します。 連結するデータモデルオブジェクトは、数値、文字列、または日付型である必要があります。</td>
   <td>印刷出力と Web 出力</td>
  </tr>
  <tr>
   <td>積み上げを表示</td>
   <td>各系列の値を互いの上に積み上げるように選択します。</td>
   <td>印刷出力と Web 出力</td>
  </tr>
  <tr>
   <td>X 軸／タイトル</td>
   <td>X軸のタイトル。</td>
   <td>印刷出力と Web 出力</td>
  </tr>
  <tr>
   <td>X軸/データモデルオブジェクト</td>
   <td><p>X軸にプロットするフォームデータモデルのコレクション項目の名前。</p> <p>グラフのX軸とY軸にプロットするために、互いに関連して意味のある、同じ親データモデルオブジェクトの2つのコレクション型/配列型プロパティを選択します。 連結するデータモデルオブジェクトは、数値、文字列、または日付型である必要があります。</p> </td>
   <td>印刷出力と Web 出力</td>
  </tr>
  <tr>
   <td>Y 軸／タイトル</td>
   <td>Y軸のタイトル。 </td>
   <td>印刷出力と Web 出力</td>
  </tr>
  <tr>
   <td>Y軸/データモデルオブジェクト</td>
   <td><p>Y軸にプロットするフォームデータモデルのコレクション項目 印刷チャネルでは、Y軸のデータモデルオブジェクトは数値型にする必要があります。</p> <p>グラフのX軸とY軸にプロットするために、互いに関連して意味のある、同じ親データモデルオブジェクトの2つのコレクション型/配列型プロパティを選択します。 </p> </td>
   <td>印刷出力と Web 出力</td>
  </tr>
  <tr>
   <td>Y 軸／関数</td>
   <td>y軸の値の計算に使用する統計/カスタム関数。</td>
   <td>印刷出力と Web 出力</td>
  </tr>
  <tr>
   <td>オブジェクトを非表示</td>
   <td>最終出力でグラフを非表示にする場合に選択します。</td>
   <td>印刷出力と Web 出力</td>
  </tr>
  <tr>
   <td>タイトル</td>
   <td>グラフのタイトル。 </td>
   <td>印刷出力</td>
  </tr>
  <tr>
   <td>高さ</td>
   <td>グラフの高さ（ピクセル単位）。</td>
   <td>印刷出力</td>
  </tr>
  <tr>
   <td>幅</td>
   <td>グラフの幅（ピクセル単位）。Web チャネルのグラフの幅については、スタイルレイヤーを使用するかテーマを適用して調整することができます。</td>
   <td>印刷出力</td>
  </tr>
  <tr>
   <td>前の必須改ページ</td>
   <td>新しいページの先頭にグラフが表示されるようにグラフの前に改ページを追加する場合は、このプロパティを選択します。 </td>
   <td>印刷出力</td>
  </tr>
  <tr>
   <td>後に必須の改ページ</td>
   <td>新しいページの先頭にグラフのコンテンツが表示されるようにグラフの後ろに改ページを追加する場合は、このプロパティを選択します。 </td>
   <td>印刷出力</td>
  </tr>
  <tr>
   <td>インデント</td>
   <td>ページの左側からのグラフのインデント。 </td>
   <td>印刷出力</td>
  </tr>
  <tr>
   <td>ツールヒント</td>
   <td><p>Webチャネルーのグラフ内のデータポイントにマウスを置くと表示されるツールチップの形式。 デフォルト値は${x}(${y})です。 グラフのタイプに応じて、グラフのポイント、棒、スライスにマウスを置くと、変数${x}と${y}がX軸とY軸の対応する値に動的に置き換えられ、ツールチップに表示されます。</p> <p>To disable tool tip, leave the <span class="uicontrol">Tooltip</code> field blank. このオプションは線グラフと領域グラフには適用できません。For example, see <a href="#chartoutputprintweb">Example 1: Chart output in print and web</a>.</code></p> </td>
   <td>Web</td>
  </tr>
  <tr>
   <td>グラフ固有の設定</td>
   <td><p>共通の設定に加えて、次のようなグラフ固有の設定を使用できます。</p>
    <ul>
     <li><strong>凡例を表示： </strong>有効な場合、円グラフまたはドーナツグラフの凡例を表示します。</li>
     <li><strong>凡例の位置： </strong>グラフを基準にした凡例の位置を指定します。 使用できるオプションは、右端、左端、上、下です。印刷チャネルでは、右側の凡例を使用することをお勧めします。</li>
     <li><strong>内側の半径</strong>: ドーナツグラフで使用でき、グラフ内の内側の円の半径をピクセル単位で指定できます。</li>
     <li><strong>線の色</strong>: 線グラフ、線と点グラフ、領域グラフで使用でき、グラフ内の線の色を指定できます。</li>
     <li><strong>点の色</strong>: 点グラフ、線グラフ、点グラフで使用でき、グラフ内の点の色を指定できます。<br /> </li>
     <li><strong>領域の色</strong>: 面グラフで使用でき、グラフ内の線の下の領域の色を指定できます。</li>
     <li><strong>基準点/連結の種類： </strong>四半円点グラフで使用して<strong> 、基準点の連結タイプを </strong>指定できます。 参照点の値を定義するには、スタティックテキストまたはデータモデルオブジェクトプロパティを使用します。</li>
     <li><strong>基準点/X軸： </strong>[バインディングタイプ]ドロップダウンリストから[ <span class="uicontrol">静的</code> ]を選択して基準点のX軸の値を指定した場合は、四半円円グラフで使用できます。</code></li>
     <li><strong>基準点/Y軸： </strong>[バインディングタイプ]ドロップダウンリストから[ <span class="uicontrol">静的</code> ]を選択して基準点のY軸値を指定した場合は、象限グラフに使用できます。</code></li>
     <li><strong>基準点/シリーズのデータモデルオブジェクト： </strong>[連結タイプ]ドロップダウンリストで[ <span class="uicontrol">データモデルオブジェクト</code> ]を選択した場合は、複数のシリーズ象限グラフで使用できます。 基準点の系列を特定するためのフォームデータモデルオブジェクトのプロパティを定義してください. </code></li>
     <li><strong>「基準点」(Reference Point) &gt; 「データモデルオブジェクトのシリーズ値」(Data Model Object Value for Series): </strong>[連結タイプ]ドロップダウンリストで[ <span class="uicontrol">データモデルオブジェクト</code> ]を選択した場合は、複数のシリーズ象限グラフで使用できます。 系列のフォームデータモデルオブジェクトプロパティと、このフィールドで定義された値を使用して、参照点の系列を識別します。</code></li>
     <li><strong>基準点/基準点のデータモデルオブジェクト： </strong>[連結タイプ]ドロップダウンリストから[ <span class="uicontrol">データモデルオブジェクト</code> ]を選択した場合は、象限グラフで使用できます。 X軸とY軸にプロットされるプロパティの兄弟であるフォームデータモデルオブジェクトプロパティを定義します。 さらに、複数のシリーズに対して、シリーズに対して定義されたデータモデルオブジェクトプロパティの子エンティティであるデータモデルオブジェクトプロパティを定義します。</code></li>
     <li><strong>基準点/基準点のデータモデルオブジェクト値： </strong>[連結タイプ]ドロップダウンリストから[ <span class="uicontrol">データモデルオブジェクト</code> ]を選択した場合は、象限グラフで使用できます。 グラフの基準点を指定するには、参照点のフォームデータモデルオブジェクトプロパティと、このフィールドで定義された値を使用します。<br /> <strong>象限ラベル/左上：</strong> 左上の象限の名前を指定するには、象限グラフで使用できます。</code></li>
     <li><strong>象限ラベル/右上：</strong> 右上の象限の名前を指定するには、象限グラフで使用できます。</li>
     <li><strong>象限ラベル/右下： </strong>右下の象限の名前を指定するには、象限グラフで使用できます。</li>
     <li><strong>象限ラベル/左下： </strong>左下の象限の名前を指定するには、象限グラフで使用できます。</li>
    </ul> </td>
   <td>印刷出力と Web 出力</td>
  </tr>
 </tbody>
</table>

## グラフでの関数の使用 {#use-functions-in-chart}

統計関数を使用するようにグラフを設定し、ソースデータの値を計算して、グラフにプロットできます。グラフ内で関数を適用すると、フォームデータモデルでは直接指定できないデータを描画することができます。

![グラフの機能](assets/functions_charts_new.png)

While the Chart component come with some in-built functions, you can write [custom functions](#customfunctionsweb) and make them available for use in the chart configuration in the web channel.

デフォルトでは、以下の関数をグラフコンポーネントに使用できます。

**平均（平均）** ：一方の軸にある特定の値のX軸またはY軸の値の平均を返します。

**[合計** ]一方の軸にある特定の値のX軸またはY軸のすべての値の合計を返します。

**[最大値** ]一方の軸にある特定の値のX軸またはY軸の最大値を返します。

**[頻度** ]一方の軸にある特定の値のX軸またはY軸の値の数を返します。

**[範囲** ]一方の軸にある特定の値のX軸またはY軸の最大値と最小値の差を返します。

**[中央値** ]一方の軸にある特定の値のX軸またはY軸の値を上半分と下半分に分ける値を返します。

**[最小** ]一方の軸にある特定の値のX軸またはY軸の最小値を返します。

**[モード** ]一方の軸にある特定の値のX軸またはY軸で最も多く出現する値を返します。

詳しくは、 [例2を参照してください。 折れ線グラフでの和関数と頻度関数の適用](#applicationsumfrequency)。

### Custom functions in web channel {#customfunctionsweb}

グラフでデフォルトの関数を使用するだけでなく、JavaScript™ でカスタム関数を作成し、Web チャネル用のグラフコンポーネントの関数リストにその関数を追加することもできます。

関数は入力された配列または値、カテゴリ名を使用して、値を返します。次に例を示します。

```javascript
Multiply(valueArray, category) {
 var val = 1;
 _.each(valueArray, function(value) {
 val = val * value;
 });
 return val;
}
```

カスタム関数を作成したら、以下を実行してグラフの設定で使用できるようにします。

1. 該当するインタラクティブ通信に関連付けられているクライアントライブラリにカスタム関数を追加します。For more information, see [Configuring the Submit action](/help/forms/using/configuring-submit-actions.md) and [Using Client-Side Libraries](/help/sites-developing/clientlibs.md).

1. To display the custom function in Function drop-down, in CRXDe Lite, create an `nt:unstructured` node in the apps folder with the following properties:

   * Add property `guideComponentType` with value as `fd/af/reducer`. (mandatory)

   * Add property `value` to a fully qualified name of the custom JavaScript™ function. （必須）に設定し、その値をMultiplyなどのカスタム関数の名前に設定します。
   * Add property `jcr:description` with the value you want to display as the name of the custom function that appears in the Function drop-down. 例えば、**Multiply** と表示されます。

   * Add property `qtip` with value that will be short description of the custom function. 「**関数**」ドロップダウンリスト内の関数名にポインターを置くと、ここで指定した説明がツールヒントとして表示されます。

1. 「**すべて保存**」をクリックして設定を保存します。

これで関数をグラフで使用できるようになります。

## 例 1：印刷チャネルと Web チャネルのグラフ出力 {#chartoutputprintweb}

「基本」タブで、グラフのタイプ、データを含むソースフォームデータモデルのプロパティ、グラフのX軸とY軸にプロットするラベル、およびオプションでグラフにプロットする値を計算する統計関数を定義します。

Interactive Communicationを使用して生成されたカード文を使用して、基本的なプロパティで必要となる最小限の情報について詳しく説明します。 具体的な例として、取引明細に記載されている様々な支払額を描画するグラフを生成する場合を考えてみます。この例では、インタラクティブ通信の印刷出力と Web 出力で、異なるタイプのグラフを使用します。

### 印刷用の列グラフ {#columnchartprint}

これを行うには、次のプロパティを指定します。

* **[!UICONTROL 名前]** — グラフの名前を指定します。
* **[!UICONTROL グラフのタイプ]** — ドロップダウンリストから「 **列** 」を選択します。
* **[!UICONTROL タイトル]** - X軸の費用タイプとY軸の取引金額を指定します。
* **[!UICONTROL データ・モデル・オブジェクト]** — データ・モデル・オブジェクトのプロパティを選択し、X軸（経費タイプ）とY軸（取引金額）のデータ連結を作成します。

![対話型通信の印刷チャネルの列グラフ](assets/sample_chart_print_column_new.png)

対話型通信の印刷チャネルの列グラフ

### Web用ドーナツグラフ {#donutchartweb}

これを行うには、次のプロパティを指定します。

* **[!UICONTROL 名前]** — グラフの名前を指定します。
* **[!UICONTROL グラフのタイプ]** — ドロップダウンリストから「 **[!UICONTROL ドーナツ]** 」を選択します。
* **[!UICONTROL データ・モデル・オブジェクト]** — データ・モデル・オブジェクトのプロパティを選択し、X軸（経費タイプ）とY軸（取引金額）のデータ連結を作成します。
* **[!UICONTROL 内側の半径]** — 内側の半径の値を150に指定して、グラフ内の内側の円の半径をピクセル単位で指定します。
* **[!UICONTROL ツールチップ]** - ${x}(${y})のデフォルトの形式を使用して、ツールチップを表示します。 ツールチップは次のように表示されます。 経費タイプ（取引金額）。 例： ビットコインの借方(10000)。

![対話型コミュニケーションのウェブチャネルにおけるドーナツグラフ](assets/sample_chart_web_new.png)

対話型コミュニケーションのウェブチャネルにおけるドーナツグラフ

## 例 2: 線グラフ内で Sum 関数と Frequency 関数を適用する {#applicationsumfrequency}

グラフ内で関数を適用すると、フォームデータモデルでは直接指定できないデータを描画することができます。この例では、クレジットカード明細の例を使用して、合計と頻度の関数をグラフに適用する方法を理解します。

![2つの「AirBnBの借方」トランザクションを含む関数のない折れ線グラフ](assets/line_chart_web_new.png)

2つの「AirBnBの借方」トランザクションを含む関数のない折れ線グラフ

### Sum 関数 {#sum-function}

Sum 関数を適用することにより、同じデータプロパティの複数のインスタンスの値を合計し、グラフ上で 1 つの項目として表示することができます。例えば、次のグラフでは、Sum関数がY軸に適用され、AirBnBトランザクションの2つの借方（2050と1050）の金額が合計され、1つのトランザクション(3100)のみが表示されます。

同じデータプロパティで複数のインスタンスが存在する場合は、Sum 関数を適用して合計値を表示すると、グラフが見やすくなります。

![折れ線グラフの合計](assets/line_chart_web_sum_new.png)

### Frequency 関数 {#frequency-function}

一方の軸にある特定の値のY軸の値の数を返します。 Y軸（取引金額）の頻度関数を適用すると、AirBnB取引の借方の2回の値と、残りの取引タイプの1回の値がグラフに表示されます。

![折れ線グラフの頻度](assets/line_chart_web_functions_frequency_new.png)

## 例3: Webの複数シリーズの象限グラフ {#example-multi-series-quadrant-chart-in-web}

グラフには、特定の日付範囲で実行された取引の金額が表示されます。 象限グラフでは、グラフ領域を4つのラベル付きのセクションに分割できます。 文字は、X軸とY軸に静的基準点を使用します。 複数シリーズ機能を使用して、銀行名に基づいてデータを分類します。

これを行うには、次のプロパティを指定します。

* **名前：** グラフの名前を指定します。
* **グラフの種類：** ドロップダウン **リストから** [四分円]を選択します。

* 「 **複数シリーズ** 」チェックボックスを選択します。
* **Data Model Object**: シリーズのデータモデルオブジェクトプロパティを指定します。 バンク名のデータモデルオブジェクトプロパティは、X軸とY軸にプロットされたデータモデルオブジェクトプロパティの親です。
* **データモデルオブジェクト：** X軸（取引日）とY軸（取引金額）のデータ連結を作成するには、データモデルオブジェクトプロパティを選択します。
* 「 **基準点** 」セクションで、「連結の種類」として「 **静的** 」を選択します。

* X軸とY軸の基準点の値を指定します。
* [左上]、[右上]、[右下]、[左下]の各象限ラベルを指定します。
* 「凡例を **表示** 」チェックボックスを選択して、銀行名の色コードを表示します。

![象限グラフ](assets/charts_quadrant_example_new.png)

