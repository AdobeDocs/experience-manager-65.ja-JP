---
title: Bulk Editor の開発
seo-title: Developing the Bulk Editor
description: タグ付けにより、コンテンツを分類および整理できます
seo-description: Tagging allows content to be categorized and organized
uuid: 3cd04c52-5bdb-47f6-9fa3-d7a4937e8e20
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e9a1ff95-e88e-41f0-9731-9a59159b4653
exl-id: 8753aaab-959f-459b-bdb6-057cbe05d480
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1837'
ht-degree: 100%

---

# Bulk Editor の開発{#developing-the-bulk-editor}

ここでは、Bulk Editor ツールを開発する方法と、Bulk Editor に基づく製品リストコンポーネントを拡張する方法について説明します。

## Bulk Editor のクエリパラメーター {#bulk-editor-query-parameters}

Bulk Editor を操作するときに、特定の設定で Bulk Editor を呼び出すために URL に追加できるクエリパラメーターがいくつかあります。製品リストコンポーネントなどで、Bulk Editor を常に特定の設定で使用するには、  （/libs/wcm/core/components/bulkeditor にある）bulkeditor.jsp を変更するか、特定の設定でコンポーネントを作成する必要があります。クエリパラメーターを使用した変更は、永続的ではありません。

例えば、ブラウザーの URL に次のように入力するとします。

`https://<servername><port_number>/etc/importers/bulkeditor.html?rootPath=/content/geometrixx/en&queryParams=geometrixx&initialSearch=true&hrp=true`

「hrp=true」によってフィールドが非表示になるので、Bulk Editor は「**ルートパス**」フィールドなしで表示されます。パラメーター「hrp=false」を使用すると、フィールドが表示されます（デフォルト値）。

以下に Bulk Editor のクエリパラメーターリストを示します。

>[!NOTE]
>
>各パラメーターには、長い名前と短い名前を指定できます。例えば、検索ルートパスの長い名前は `rootPath`、短い名前は `rp` のようになります。長い名前が定義されていない場合、短い名前がリクエストから読み取られます。

<table>
 <tbody>
  <tr>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p> パラメーター</p> <p>（長い名前 / 短い名前）<br /> </p> </td>
   <td> 型 <br /> </td>
   <td> 説明 <br /> </td>
  </tr>
  <tr>
   <td> rootPath / rp<br /> </td>
   <td> 文字列 </td>
   <td> 検索ルートパス</td>
  </tr>
  <tr>
   <td> queryParams / qp<br /> </td>
   <td> 文字列</td>
   <td> 検索クエリ</td>
  </tr>
  <tr>
   <td> contentMode / cm<br /> </td>
   <td> ブール値</td>
   <td> true の場合、コンテンツモードが有効になります <br /> </td>
  </tr>
  <tr>
   <td> colsValue / cv<br /> </td>
   <td> String[]</td>
   <td> 検索対象プロパティ（チェックボックスとして表示される colsSelection で選択した値）</td>
  </tr>
  <tr>
   <td> extraCols / ec<br /> </td>
   <td> String[]</td>
   <td> 任意選択の検索対象プロパティ（コンマ区切りのテキストフィールドで表示）</td>
  </tr>
  <tr>
   <td> initialSearch / is<br /> </td>
   <td> ブール値</td>
   <td> true の場合、ページの読み込み時にクエリを実行します <br /> </td>
  </tr>
  <tr>
   <td> colsSelection / cs<br /> </td>
   <td> String[]</td>
   <td> 検索対象プロパティの選択（チェックボックスとして表示）</td>
  </tr>
  <tr>
   <td> showGridOnly / sgo<br /> </td>
   <td> ブール値</td>
   <td> true の場合、グリッドのみを表示し、検索パネルは非表示になります <br /> </td>
  </tr>
  <tr>
   <td> searchPanelCollapsed / spc</td>
   <td> ブール値</td>
   <td> true の場合、読み込み時に検索パネルは折りたたまれます</td>
  </tr>
  <tr>
   <td> hideRootPath / hrp</td>
   <td> ブール値</td>
   <td> true の場合、ルートパスフィールドを非表示</td>
  </tr>
  <tr>
   <td> hideQueryParams／hqp</td>
   <td> ブール値</td>
   <td> true の場合は、クエリフィールドは非表示になります</td>
  </tr>
  <tr>
   <td> hideContentMode／hcm</td>
   <td> ブール値</td>
   <td> true の場合は、コンテンツモードフィールドは非表示になります</td>
  </tr>
  <tr>
   <td> hideColsSelection／hcs</td>
   <td> ブール値</td>
   <td> true の場合は、列選択フィールドは非表示になります</td>
  </tr>
  <tr>
   <td> hideExtraCols／hec</td>
   <td> ブール値</td>
   <td> true の場合は、列選択フィールドは非表示になります</td>
  </tr>
  <tr>
   <td> hideSearchButton</td>
   <td> ブール値</td>
   <td> true の場合は、検索ボタンは非表示になります</td>
  </tr>
  <tr>
   <td> hideSaveButton／hsavep</td>
   <td> ブール値</td>
   <td> true の場合は、保存ボタンは非表示になります</td>
  </tr>
  <tr>
   <td> hideExportButton／hexpb</td>
   <td> ブール値</td>
   <td> true の場合は、書き出しボタンは非表示になります</td>
  </tr>
  <tr>
   <td> hideImportButton／hib</td>
   <td> ブール値</td>
   <td> true の場合は、読み込みボタンは非表示になります</td>
  </tr>
  <tr>
   <td> hideResultNumber／hrn</td>
   <td> ブール値</td>
   <td> true の場合、グリッドの検索結果番号テキストは非表示になります</td>
  </tr>
  <tr>
   <td> hideInsertButton／hinsertb</td>
   <td> ブール値</td>
   <td> true の場合、グリッドの挿入ボタンがは非表示になります</td>
  </tr>
  <tr>
   <td> hideDeleteButton／hdelb</td>
   <td> ブール値</td>
   <td> true の場合、グリッドの削除ボタンは非表示になります</td>
  </tr>
  <tr>
   <td> hidePathCol／hpc</td>
   <td> ブール値</td>
   <td> true の場合、グリッドの「パス」列は非表示になります</td>
  </tr>
 </tbody>
</table>

### Bulk Editor ベースのコンポーネントの作成：製品リストコンポーネント {#developing-a-bulk-editor-based-component-the-product-list-component}

ここでは、Bulk Editor の使用方法の概要について説明します。また、Bulk Editor に基づく既存の Geometrixx コンポーネントである製品リストコンポーネントについても説明します。

製品リストコンポーネントを使用すると、ユーザーがデータのテーブルを表示および編集できます。例えば、製品リストコンポーネントを使用して、カタログの商品を表現できます。情報は標準的な HTML テーブルで表示され、編集は BulkEditor ウィジェットを含む&#x200B;**編集**&#x200B;ダイアログで実行されます。（この Bulk Editor は、  /etc/importers/bulkeditor.html またはツールメニューからアクセスできるものとまったく同じです）。製品リストコンポーネントは、特定の制限された Bulk Editor 機能を使用するように設定されています。バルクエディターのすべての部分（またはバルクエディターから派生したコンポーネント）を設定できます。

Bulk Editor を使用すると、行の追加、変更、削除、フィルターおよび書き出し、変更内容の保存および複数行の読み込みをおこなうことができます。各行は、製品リストコンポーネントインスタンス以下の 1 つのノードとして格納されます。すべてのセルは、各ノードのプロパティです。これはデザインの選択として簡単に変更できます。例えば、リポジトリの他の場所にノードを格納することもできます。クエリサーブレットの役割は、表示するノードリストを返すことです。検索パスは製品リストインスタンスとして定義されます。

製品リストコンポーネントのソースコードは、  /apps/geometrixx/components/productlist は、他のすべての AEM コンポーネントと同様に複数のパーツで構成されています。

* HTML レンダリング。このレンダリングは JSP ファイル（/apps/geometrixx/components/productlist/productlist.jsp）で実行されます。JSP は現在の製品リストコンポーネントのサブノードを読み取り、HTML テーブルの行として各サブノードを表示します。
* 編集ダイアログは、バルクエディター設定を定義する場所です。コンポーネントのニーズに合わせてダイアログを設定します。使用可能な列およびグリッドまたは検索で実行できるアクション。すべての設定プロパティについて詳しくは、[Bulk Editor の設定プロパティ](#bulk-editor-configuration-properties)を参照してください。

以下はダイアログのサブノードの XML 表現です。

```xml
        <editor
            jcr:primaryType="cq:Widget"
            colsSelection="[ProductId,ProductName,Color,CatalogCode,SellingSku]"
            colsValue="[ProductId,ProductName,Color,CatalogCode,SellingSku]"
            contentMode="false"
            exportURL="/etc/importers/bulkeditor/export.tsv"
            extraCols="Selection"
            hideColsSelection="false"
            hideContentMode="true"
            hideDeleteButton="false"
            hideExportButton="false"
            hideExtraCols="true"
            hideImportButton="false"
            hideInsertButton="false"
            hideMoveButtons="false"
            hidePathCol="true"
            hideRootPath="true"
            hideSaveButton="false"
            hideSearchButton="false"
            importURL="/etc/importers/bulkeditor/import"
            initialSearch="true"
            insertedResourceType="geometrixx/components/productlist/sku"
            queryParams=""
            queryURL="/etc/importers/bulkeditor/query.json"
            saveURL="/etc/importers/bulkeditor/save"
            xtype="bulkeditor">
            <saveButton
                jcr:primaryType="nt:unstructured"
                text="Save modifications"/>
            <searchButton
                jcr:primaryType="nt:unstructured"
                text="Apply filter"/>
            <queryParamsInput
                jcr:primaryType="nt:unstructured"
                fieldDescription="Enter here your filters"
                fieldLabel="Filters"/>
            <searchPanel
                jcr:primaryType="nt:unstructured"
                height="200">
                <defaults
                    jcr:primaryType="nt:unstructured"
                    labelWidth="150"/>
            </searchPanel>
            <grid
                jcr:primaryType="nt:unstructured"
                height="275"/>
            <store jcr:primaryType="nt:unstructured">
                <sortInfo
                    jcr:primaryType="nt:unstructured"
                    direction="ASC"
                    field="CatalogCode"/>
            </store>
            <colModel
                jcr:primaryType="nt:unstructured"
                width="150"/>
            <colsMetadata jcr:primaryType="nt:unstructured">
                <Selection
                    jcr:primaryType="nt:unstructured"
                    checkbox="true"
                    forcedPosition="0"
                    headerText=""/>
                <ProductId
                    jcr:primaryType="nt:unstructured"
                    cellCls="productlist-cell-productid"
                    headerText="Product Id"/>
                <ProductName
                    jcr:primaryType="nt:unstructured"
                    cellStyle="background-color: #FFCC99;"
                    headerText="Product Name"/>
                <CatalogCode
                    jcr:primaryType="nt:unstructured"
                    cellStyle="background-color: #EDEDED;"
                    headerText="Catalog Code"/>
                <Color jcr:primaryType="nt:unstructured">
                    <editor
                        jcr:primaryType="nt:unstructured"
                        store="[Blue,Red,Yellow]"
                        triggerAction="all"
                        typeAhead="true"
                        xtype="combo"/>
                </Color>
                <SellingSku
                    jcr:primaryType="nt:unstructured"
                    headerText="Sku Id"/>
            </colsMetadata>
        </editor>
```

### Bulk Editor の設定プロパティ {#bulk-editor-configuration-properties}

バルクエディターのすべての部分が設定可能です。次の表に、バルクエディターのすべての設定プロパティを示します。

<table>
 <tbody>
  <tr>
   <td>プロパティ名</td>
   <td>定義</td>
  </tr>
  <tr>
   <td>rootPath</td>
   <td>検索のルートパス</td>
  </tr>
  <tr>
   <td>queryParams</td>
   <td>検索クエリー</td>
  </tr>
  <tr>
   <td>contentMode</td>
   <td>true の場合は、コンテンツモードが有効（プロパティを検索結果ノードではなく jcr:content ノードで読み取り）</td>
  </tr>
  <tr>
   <td>colsValue</td>
   <td>検索対象プロパティ（チェックボックスとして表示される colsSelection で選択した値）</td>
  </tr>
  <tr>
   <td>extraCols</td>
   <td>追加の検索対象プロパティ（コンマ区切りでテキストフィールドに表示）</td>
  </tr>
  <tr>
   <td>initialSearch</td>
   <td>true の場合は、ページの読み込み時にクエリーを実行</td>
  </tr>
  <tr>
   <td>colsSelection</td>
   <td>検索対象プロパティの選択（チェックボックスとして表示）</td>
  </tr>
  <tr>
   <td>showGridOnly</td>
   <td>true の場合は、グリッドのみを表示し、検索パネルは非表示（必ず initialSearch を true に設定）</td>
  </tr>
  <tr>
   <td>searchPanelCollapsed</td>
   <td>true の場合は、デフォルトで検索パネルを折りたたみ</td>
  </tr>
  <tr>
   <td>hideRootPath</td>
   <td>ルートパスフィールドを非表示</td>
  </tr>
  <tr>
   <td>hideQueryParams</td>
   <td>クエリーフィールドを非表示</td>
  </tr>
  <tr>
   <td>hideContentMode</td>
   <td>コンテンツモードフィールドを非表示</td>
  </tr>
  <tr>
   <td>hideColsSelection</td>
   <td>列選択フィールドを非表示</td>
  </tr>
  <tr>
   <td>hideExtraCols</td>
   <td>任意選択の列フィールドを非表示</td>
  </tr>
  <tr>
   <td>hideSearchButton</td>
   <td>検索ボタンを非表示</td>
  </tr>
  <tr>
   <td>hideSaveButton</td>
   <td>保存ボタンを非表示</td>
  </tr>
  <tr>
   <td>hideExportButton</td>
   <td>書き出しボタンを非表示</td>
  </tr>
  <tr>
   <td>hideImportButton</td>
   <td>読み込みボタンを非表示</td>
  </tr>
  <tr>
   <td>hideResultNumber</td>
   <td>グリッドの検索結果番号テキストを非表示</td>
  </tr>
  <tr>
   <td>hideInsertButton</td>
   <td>グリッドの挿入ボタンを非表示</td>
  </tr>
  <tr>
   <td>hideDeleteButton</td>
   <td>グリッドの削除ボタンを非表示</td>
  </tr>
  <tr>
   <td>hidePathCol</td>
   <td>グリッドの「パス」列を非表示</td>
  </tr>
  <tr>
   <td>queryURL</td>
   <td>クエリーサーブレットへのパス</td>
  </tr>
  <tr>
   <td>exportURL</td>
   <td>書き出しサーブレットへのパス</td>
  </tr>
  <tr>
   <td>importURL</td>
   <td>読み込みサーブレットへのパス</td>
  </tr>
  <tr>
   <td>insertedResourceType</td>
   <td>行が挿入されるとノードに追加されるリソースタイプ</td>
  </tr>
  <tr>
   <td>saveButton</td>
   <td>保存ボタンウィジェット設定</td>
  </tr>
  <tr>
   <td>searchButton</td>
   <td>検索ボタンウィジェット設定</td>
  </tr>
  <tr>
   <td>exportButton</td>
   <td>書き出しボタンウィジェット設定</td>
  </tr>
  <tr>
   <td>importButton</td>
   <td>読み込みボタンウィジェット設定</td>
  </tr>
  <tr>
   <td>searchPanel</td>
   <td>検索パネルウィジェット設定</td>
  </tr>
  <tr>
   <td>grid</td>
   <td>グリッドウィジェット設定</td>
  </tr>
  <tr>
   <td>store</td>
   <td>ストア設定</td>
  </tr>
  <tr>
   <td>colModel</td>
   <td>グリッドの列モデル設定</td>
  </tr>
  <tr>
   <td>rootPathInput</td>
   <td>rootPath ウィジェット設定</td>
  </tr>
  <tr>
   <td>queryParamsInput</td>
   <td>queryParams ウィジェット設定</td>
  </tr>
  <tr>
   <td>contentModeInput</td>
   <td>contentMode ウィジェット設定</td>
  </tr>
  <tr>
   <td>colsSelectionInput</td>
   <td>colsSelection ウィジェット設定</td>
  </tr>
  <tr>
   <td>extraColsInput</td>
   <td>extraCols ウィジェット設定</td>
  </tr>
  <tr>
   <td>colsMetadata</td>
   <td>列のメタデータ設定です。以下のプロパティを設定できます（列のすべてのセルに適用されます）。<br />
    <ul>
     <li>cellStyle：HTML スタイル </li>
     <li>cellCls：CSS クラス </li>
     <li>readOnly：true の場合は、値を変更できません。 </li>
     <li>checkbox：true の場合は、列のすべてのセルをチェックボックス（true／false 値）として定義します。 </li>
     <li>forcedPosition：グリッド内での列の位置を指定する整数値（0 ～列 -1 の数）<p><br /> </p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### 列メタデータ設定 {#columns-metadata-configuration}

列ごとに以下を設定できます。

* 表示プロパティ：html スタイル、CSS クラスおよび読み取り専用

* チェックボックス
* 強制位置

CSS および読み取り専用の列

Bulk Editor には以下の 3 つの列の設定があります。

* セル CSS クラス名（cellCls）：設定する列の各セルに追加される CSS クラス名。
* セルスタイル（cellStyle）：設定する列の各セルに追加される HTML スタイル。
* 読み取り専用（readOnly）：設定する列の各セルに読み取り専用が設定されます。

設定は以下のように定義する必要があります。

```
"colsMetadata": {
"Column name": {
     "cellStyle": "html style",
     "cellCls": "CSS class",
     "readOnly": true/false
}
}
```

次の例は、productlist コンポーネント（/apps/geometrixx/components/productlist/dialog/items/editor/colsMetadata）にあります。

```xml
            <colsMetadata jcr:primaryType="nt:unstructured">
                <Selection
                    jcr:primaryType="nt:unstructured"
                    checkbox="true"
                    forcedPosition="0"
                    headerText=""/>
                <ProductId
                    jcr:primaryType="nt:unstructured"
                    cellCls="productlist-cell-productid"
                    headerText="Product Id"/>
                <ProductName
                    jcr:primaryType="nt:unstructured"
                    cellStyle="background-color: #FFCC99;"
                    headerText="Product Name"/>
                <CatalogCode
                    jcr:primaryType="nt:unstructured"
                    cellStyle="background-color: #EDEDED;"
                    headerText="Catalog Code"/>
                <Color jcr:primaryType="nt:unstructured">
                    <editor
                        jcr:primaryType="nt:unstructured"
                        store="[Blue,Red,Yellow]"
                        triggerAction="all"
                        typeAhead="true"
                        xtype="combo"/>
                </Color>
                <SellingSku
                    jcr:primaryType="nt:unstructured"
                    headerText="Sku Id"/>
            </colsMetadata>
```

**チェックボックス**

checkbox 設定プロパティを true に設定すると、その列のすべてのセルがチェックボックスとしてレンダリングされます。ボックスがオンの場合は **true** がサーバーの Save サーブレットに送信され、オフの場合は **false** が送信されます。ヘッダーメニューで、**すべてを選択**&#x200B;または **なしを選択**&#x200B;することもできます。これらのオプションは、選択したヘッダーがチェックボックス列のヘッダーの場合に有効になります。

前の例で、selection 列には、checkbox=&quot;true&quot; のチェックボックスのみが含まれます。

**強制された位置**

強制された位置メタデータ forcedPosition を使用すると、グリッド内での列の位置を指定できます。0 が先頭位置で、&lt;列の数>-1 が最終位置です。その他の値は無視されます。

前の例で、selection 列は forcedPosition=&quot;0&quot; の最初の列です。

### クエリサーブレット {#query-servlet}

デフォルトでは、クエリサーブレットは `/libs/wcm/core/components/bulkeditor/json.java` にあります。別のパスを設定するとデータを取得できます。

Query サーブレットには、GQL クエリおよび返す列を受信し、結果を計算し、結果を JSON ストリームとして Bulk Editor に送信するという機能があります。

製品リストコンポーネントの場合、Query サーブレットに送信される 2 つのパラメーターは以下のとおりです。

* クエリ：「path:/content/geometrixx/en/customers/jcr:content/par/productlist Cube」
* cols：「Selection,ProductId,ProductName,Color,CatalogCode,SellingSku」

返される JSON ストリームは次のようになります。

```
{
  "hits": [{
      "jcr:path": "/content/geometrixx/en/products/jcr:content/par/productlist/1258674828905",
      "ProductId": "21",
      "ProductName": "Cube",
      "Color": "Blue",
      "CatalogCode": "43244",
      "SellingSku": "32131"
    }
  ],
  "results": 1
}
```

各ヒットは 1 つのノードとそのプロパティに対応し、グリッドに行として表示されます。

クエリサーブレットを拡張すると、複雑な継承モデルを返したり、特定の論理場所に保存されたノードを返したりすることができます。クエリサーブレットを使用すると、あらゆる種類の複雑な計算を実行できます。リポジトリ内の複数ノードの集計がグリッドに行で表示されます。この場合、これらの行の変更と保存は、Save サーブレットで管理する必要があります。

### 保存サーブレット {#save-servlet}

バルクエディターのデフォルト設定では、各行が 1 つのノードであり、各行のレコードにそのノードのパスが格納されます。バルクエディターは、行とノードの間のリンクを jcr パスを介して保持します。ユーザーがグリッドを編集すると、すべての変更のリストが作成されます。ユーザーが「**保存**」をクリックすると、更新されたプロパティ値と共に POST クエリが各パスに送信されます。これは Sling の基本的な概念であり、各セルがノードのプロパティである限り適切に機能します。ただし、クエリサーブレットで継承を計算するように実装している場合は、クエリサーブレットが返すプロパティは別のノードから継承される可能性があるので、このモデルは機能しません。

変更は、各ノードに直接反映されるのではなく、保存ジョブを行う 1 つのサーブレットに反映される、というのが保存サーブレットの概念です。これにより、そのサーブレットで変更を分析することができ、そのプロパティを適切なノードに保存できます。

更新された各プロパティは、次の形式でサーブレットに送信されます。

* パラメーター名：&lt;jcr path>/&lt;property name>

   例：/content/geometrixx/en/products/jcr:content/par/productlist/1258674859000/SellingSku

* 値：&lt;value>

   値：12123

サーブレットは、catalogCode プロパティが格納されている場所を認識している必要があります。

保存サーブレットのデフォルトの実装は /libs/wcm/bulkeditor/save/POST.jsp にあり、製品リストのコンポーネントで使用されます。（&lt;jcr path>/&lt;property name> 形式の）リクエストからすべてのパラメーターを取得し、JCR API を使用してノードにプロパティを書き込みます。また、存在しない場合は、ノードも作成されます（グリッド挿入行）。

デフォルトのコードをそのまま使用しないでください。サーバーがネイティブに実行する機能（&lt;jcr path>/&lt;property name> での POST）を再実装したコードなので、プロパティの継承モデルを管理する保存サーブレットを作成する際の出発点として使用するのに適しています。
