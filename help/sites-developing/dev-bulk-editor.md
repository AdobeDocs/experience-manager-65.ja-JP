---
title: Bulk Editor の開発
description: タグ付けを使用すると、コンテンツを分類および整理できます
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 8753aaab-959f-459b-bdb6-057cbe05d480
source-git-commit: fc2f26a69c208947c14e8c6036825bb217901481
workflow-type: tm+mt
source-wordcount: '1833'
ht-degree: 37%

---

# Bulk Editor の開発{#developing-the-bulk-editor}

この節では、バルクエディターツールの開発方法と、バルクエディターに基づく製品リストコンポーネントの拡張方法について説明します。

## バルクエディタークエリパラメーター {#bulk-editor-query-parameters}

Bulk Editor を操作する際には、URL に追加して、特定の設定で Bulk Editor を呼び出すためのクエリパラメーターがいくつかあります。 Bulk Editor を製品リストコンポーネントなどの特定の設定で常に使用したい場合は、 `bulkeditor.jsp` （/libs/wcm/core/components/bulkeditor 内）または特定の設定でコンポーネントを作成します。 クエリパラメーターを使用して行った変更は、永続的ではありません。

例えば、ブラウザーの URL に次のように入力するとします。

`https://<servername><port_number>/etc/importers/bulkeditor.html?rootPath=/content/geometrixx/en&queryParams=geometrixx&initialSearch=true&hrp=true`

Bulk Editor は、 **ルートパス** 「hrp=true」のフィールドは、フィールドを非表示にします。 パラメーター hrp=false の場合、フィールドが表示されます（デフォルト値）。

次に、Bulk Editor クエリパラメーターのリストを示します。

>[!NOTE]
>
>各パラメーターには、長い名前と短い名前を指定できます。例えば、検索ルートパスの長い名前は次のようになります。 `rootPath`短いのは `rp`. 長い名前が定義されていない場合、短い名前がリクエストから読み取られます。

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

### バルクエディターベースのコンポーネントの開発：製品リストコンポーネント {#developing-a-bulk-editor-based-component-the-product-list-component}

この節では、バルクエディターの使用方法の概要と、バルクエディター（製品リストコンポーネント）に基づく既存のGeometrixxコンポーネントの説明を示します。

製品リストコンポーネントを使用すると、ユーザーはデータのテーブルを表示および編集できます。 例えば、製品リストコンポーネントを使用して、カタログ内の製品を表すことができます。 情報は標準のHTMLテーブルに表示され、編集は **編集** ダイアログボックスに BulkEditor ウィジェットが表示されます。 ( この Bulk Editor は、 /etc/importers/bulkeditor.htmlまたはツールメニューからアクセスできるものと同じです )。 製品リストコンポーネントは、特定の限られたバルクエディター機能用に設定されています。 Bulk Editor のすべての部分（または Bulk Editor から派生したコンポーネント）を設定できます。

Bulk Editor を使用すると、行の追加、変更、削除、フィルタリングおよびエクスポート、変更の保存、一連の行のインポートをおこなうことができます。 すべての行は、製品リストコンポーネントインスタンス自体の下にノードとして保存されます。 すべてのセルは、各ノードのプロパティです。これは設計の選択肢で、簡単に変更できます。例えば、リポジトリ内の別の場所にノードを保存できます。 クエリサーブレットの役割は、表示するノードのリストを返すことです。検索パスは、製品リストインスタンスとして定義されます。

製品リストコンポーネントのソースコードは、   /apps/geometrixx/components/productlist は、すべてのAdobe Experience Manager(AEM) コンポーネントのような、いくつかの部分で構成されます。

* HTMLレンダリング：レンダリングは JSP ファイル (/apps/geometrixx/components/productlist/productlist.jsp) で行われます。 JSP は、現在の製品リストコンポーネントのサブノードを読み取り、それぞれをHTMLテーブルの行として表示します。
* 編集ダイアログは、バルクエディター設定を定義する場所です。コンポーネントのニーズに合わせてダイアログを設定します。使用可能な列およびグリッドまたは検索で実行できるアクション。詳しくは、 [バルクエディターの設定プロパティ](#bulk-editor-configuration-properties) を参照してください。

次に、ダイアログサブノードの XML 表現を示します。

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

### バルクエディターの設定プロパティ {#bulk-editor-configuration-properties}

Bulk Editor のすべての部分を設定できます。 次の表に、Bulk Editor のすべての設定プロパティを示します。

<table>
 <tbody>
  <tr>
   <td>プロパティ名</td>
   <td>定義</td>
  </tr>
  <tr>
   <td>rootPath</td>
   <td>検索ルートパス</td>
  </tr>
  <tr>
   <td>queryParams</td>
   <td>検索クエリー</td>
  </tr>
  <tr>
   <td>contentMode</td>
   <td>コンテンツモードを有効にする場合に True を指定します。プロパティは、検索結果ノードではなく、jcr:content ノードで読み取られます。</td>
  </tr>
  <tr>
   <td>colsValue</td>
   <td>検索されたプロパティ（チェックボックスとして表示される colsSelection の値がチェックされます）</td>
  </tr>
  <tr>
   <td>extraCols</td>
   <td>追加の検索済みプロパティ（コンマ区切りのテキストフィールドで表示）</td>
  </tr>
  <tr>
   <td>initialSearch</td>
   <td>True を指定して、ページの読み込み時にクエリを実行</td>
  </tr>
  <tr>
   <td>colsSelection</td>
   <td>検索されたプロパティの選択（チェックボックスとして表示）</td>
  </tr>
  <tr>
   <td>showGridOnly</td>
   <td>True を指定すると、グリッドのみが表示され、検索パネルは表示されません（必ず initialSearch を true に設定してください）。</td>
  </tr>
  <tr>
   <td>searchPanelCollapsed</td>
   <td>デフォルトで検索パネルを折りたたむ場合は True を指定します</td>
  </tr>
  <tr>
   <td>hideRootPath</td>
   <td>ルートパスフィールドを非表示</td>
  </tr>
  <tr>
   <td>hideQueryParams</td>
   <td>クエリフィールドを非表示</td>
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
   <td>余分な列フィールドを非表示にする</td>
  </tr>
  <tr>
   <td>hideSearchButton</td>
   <td>検索ボタンを非表示にする</td>
  </tr>
  <tr>
   <td>hideSaveButton</td>
   <td>保存ボタンを非表示にする</td>
  </tr>
  <tr>
   <td>hideExportButton</td>
   <td>書き出しボタンを非表示にする</td>
  </tr>
  <tr>
   <td>hideImportButton</td>
   <td>「読み込み」ボタンを非表示にする</td>
  </tr>
  <tr>
   <td>hideResultNumber</td>
   <td>グリッドの検索結果番号のテキストを非表示にする</td>
  </tr>
  <tr>
   <td>hideInsertButton</td>
   <td>グリッドの挿入ボタンを非表示にする</td>
  </tr>
  <tr>
   <td>hideDeleteButton</td>
   <td>グリッドの削除ボタンを非表示にする</td>
  </tr>
  <tr>
   <td>hidePathCol</td>
   <td>グリッドの「パス」列を非表示にする</td>
  </tr>
  <tr>
   <td>queryURL</td>
   <td>クエリサーブレットへのパス</td>
  </tr>
  <tr>
   <td>exportURL</td>
   <td>書き出しサーブレットのパス</td>
  </tr>
  <tr>
   <td>importURL</td>
   <td>サーブレットを読み込むパス</td>
  </tr>
  <tr>
   <td>insertedResourceType</td>
   <td>行の挿入時にノードに追加されるリソースタイプ</td>
  </tr>
  <tr>
   <td>saveButton</td>
   <td>ボタンウィジェット設定を保存</td>
  </tr>
  <tr>
   <td>searchButton</td>
   <td>検索ボタンウィジェット設定</td>
  </tr>
  <tr>
   <td>exportButton</td>
   <td>書き出しボタンのウィジェット設定</td>
  </tr>
  <tr>
   <td>importButton</td>
   <td>読み込みボタンウィジェットの設定</td>
  </tr>
  <tr>
   <td>searchPanel</td>
   <td>検索パネルのウィジェット設定</td>
  </tr>
  <tr>
   <td>grid</td>
   <td>グリッドウィジェット設定</td>
  </tr>
  <tr>
   <td>store</td>
   <td>設定を保存</td>
  </tr>
  <tr>
   <td>colModel</td>
   <td>グリッド列モデルの設定</td>
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
   <td>列のメタデータ設定。 可能なプロパティは次のとおりです（列のすべてのセルに適用されます）。 <br />
    <ul>
     <li>cellStyle: html style </li>
     <li>cellCls: css クラス </li>
     <li>readOnly：値を変更できない場合は true </li>
     <li>checkbox: true を指定すると、列のすべてのセルがチェックボックスとして定義されます（true/false 値）。 </li>
     <li>forcedPosition：グリッド内の列の配置先を指定する整数値（0 ～列数 —1）<p><br /> </p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### 列のメタデータ設定 {#columns-metadata-configuration}

各列に対して、次のようにを設定できます。

* 表示プロパティ：html スタイル、CSS クラスおよび読み取り専用

* チェックボックス
* 強制的な位置

CSS 列と読み取り専用列

Bulk Editor には次の 3 つの列設定があります。

* セル CSS クラス名 (cellCls)：設定した列の各セルに追加される CSS クラス名。
* セルのスタイル (cellStyle)：設定した列の各HTMLに追加されるセルスタイル。
* 読み取り専用 (readOnly)：設定された列の各セルに対して読み取り専用が設定されます。

設定は、次のように定義する必要があります。

```
"colsMetadata": {
"Column name": {
     "cellStyle": "html style",
     "cellCls": "CSS class",
     "readOnly": true/false
}
}
```

次の例は、productlist コンポーネント (/apps/geometrixx/components/productlist/dialog/items/editor/colsMetadata) にあります。

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

checkbox configuration プロパティが true に設定されている場合、列のすべてのセルがチェックボックスとしてレンダリングされます。 ボックスがオンの場合は **true** がサーバーの Save サーブレットに送信され、オフの場合は **false** が送信されます。ヘッダーメニューで、**すべてを選択**&#x200B;または **なしを選択**&#x200B;することもできます。これらのオプションは、選択したヘッダーがチェックボックス列のヘッダーの場合に有効になります。

前の例では、選択列には、checkbox=&quot;true&quot;のチェックボックスのみが含まれています。

**強制位置**

強制位置メタデータ forcedPosition を使用すると、グリッド内で列を配置する場所を指定できます。0 が最初の位置で、 &lt;number of=&quot;&quot; columns=&quot;&quot;>-1 が最後の位置です。 その他の値は無視されます。

前の例では、選択列は forcedPosition=&quot;0&quot;の最初の列です。

### クエリサーブレット {#query-servlet}

デフォルトでは、クエリサーブレットは `/libs/wcm/core/components/bulkeditor/json.java` にあります。別のパスを設定するとデータを取得できます。

クエリサーブレットは、GQL クエリと返す列を受け取り、結果を計算し、結果を JSON ストリームとして Bulk Editor に返します。

製品リストコンポーネントの場合、クエリサーブレットに送信される 2 つのパラメーターは次のようになります。

* クエリ：「path:/content/geometrixx/en/customers/jcr:content/par/productlist Cube」
* cols：「Selection,ProductId,ProductName,Color,CatalogCode,SellingSku」

また、JSON ストリームは次のように返されます。

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

### サーブレットを保存 {#save-servlet}

Bulk Editor のデフォルト設定では、各行がノードで、このノードのパスが行レコードに保存されます。 Bulk Editor は、行とノード間のリンクを jcr パスを介して保持します。 ユーザーがグリッドを編集すると、すべての変更のリストが作成されます。 ユーザーが **保存**&#x200B;に設定すると、POSTクエリが、更新されたプロパティ値と共に各パスに送信されます。 これは Sling の基本的な概念であり、各セルがノードのプロパティである限り適切に機能します。ただし、クエリサーブレットで継承を計算するように実装している場合は、クエリサーブレットが返すプロパティは別のノードから継承される可能性があるので、このモデルは機能しません。

変更は、各ノードに直接反映されるのではなく、保存ジョブを行う 1 つのサーブレットに反映される、というのが保存サーブレットの概念です。これにより、そのサーブレットで変更を分析することができ、そのプロパティを適切なノードに保存できます。

更新された各プロパティは、次の形式でサーブレットに送信されます。

* パラメーター名：&lt;jcr path>/&lt;property name>

  例：/content/geometrixx/en/products/jcr:content/par/productlist/1258674859000/SellingSku

* 値：&lt;value>

  値：12123

サーブレットは、catalogCode プロパティが格納されている場所を認識している必要があります。

保存サーブレットのデフォルトの実装は /libs/wcm/bulkeditor/save/POST.jsp にあり、製品リストのコンポーネントで使用されます。（&lt;jcr path>/&lt;property name> 形式の）リクエストからすべてのパラメーターを取得し、JCR API を使用してノードにプロパティを書き込みます。また、存在しない場合は、ノードも作成されます（グリッド挿入行）。

デフォルトのコードは、サーバーがネイティブに実装する ( &lt;jcr path=&quot;&quot;>/&lt;property name=&quot;&quot;>) を参照し、プロパティの継承モデルを管理できる Save サーブレットを構築するには、まず最初に使用する必要があります。
