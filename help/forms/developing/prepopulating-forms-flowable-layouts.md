---
title: 編集可能なレイアウトでのフォームの自動埋め込み
seo-title: 編集可能なレイアウトでのフォームの自動埋め込み
description: 'null'
seo-description: 'null'
uuid: 93ccb496-e1c2-4b79-8e89-7a2abfce1537
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 30a12fc6-07b8-4c7c-b9e2-caa2bec0ac48
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 編集可能なレイアウトでのフォームの自動埋め込み {#prepopulating-forms-with-flowable-layouts1}

## 編集可能なレイアウトでのフォームの自動埋め込み {#prepopulating-forms-with-flowable-layouts2}

フォームの自動埋め込みは、レンダリングされたフォーム内のユーザーにデータを表示します。 例えば、ユーザーがユーザー名とパスワードを使用してWebサイトにログインしたとします。 認証に成功した場合、クライアントアプリケーションはデータベースに対してユーザー情報のクエリを実行します。 データがフォームにマージされ、フォームがユーザーにレンダリングされます。 その結果、ユーザーはフォーム内でパーソナライズされたデータを表示できます。

フォームの自動埋め込みには、次の利点があります。

* ユーザーがフォーム内にカスタムデータを表示できる.
* ユーザーがフォームに入力する際の入力量を削減します。
* データを配置する場所を制御できるため、データの整合性を維持できる.

次の2つのXMLデータソースで、フォームに自動埋め込みを行うことができます。

* XDPデータソース。XFA構文（またはAcrobatを使用して作成されたフォームの自動埋め込みを行うXFDFデータ）に準拠するXMLです。
* フォームのフィールド名に一致する名前と値のペアを含む任意のXMLデータソース（この節の例では、任意のXMLデータソースを使用します）。

事前入力するすべてのフォームフィールドにXML要素が存在する必要があります。 XML要素名は、フィールド名と一致する必要があります。 XML要素がフォームフィールドに対応していない場合、またはXML要素名がフィールド名と一致しない場合、XML要素は無視されます。 すべてのXML要素が指定されている限り、XML要素が表示される順序に一致する必要はありません。

既にデータを含むフォームに事前入力する場合は、XMLデータソース内に既に表示されているデータを指定する必要があります。 10個のフィールドを含むフォームに4つのフィールドのデータが含まれているとします。 次に、残りの6つのフィールドに事前入力するとします。 この場合、フォームの自動埋め込みに使用するXMLデータソースに10個のXML要素を指定する必要があります。 6つの要素のみを指定した場合、元の4つのフィールドは空になります。

例えば、サンプル確認フォームなどのフォームを事前入力できます。 ( [Rendering Interactive PDF Forms]（/help/forms/developing/rendering-forms-rendering-forms rendering-interactive-pdf-forms-rendering.md#rendering-interactive-pdf-formsの確認フォームを参照）。

サンプルの確認フォームを事前入力するには、フォーム内の3つのフィールドに一致する3つのXML要素を含むXMLデータソースを作成する必要があります。 このフォームには、次の3つのフィールドが含まれています。 `FirstName`、 `LastName`、、 `Amount`、 最初の手順は、フォームデザイン内のフィールドに一致するXML要素を含むXMLデータソースを作成することです。 次の手順では、次のXMLコードに示すように、XML要素にデータ値を割り当てます。

```as3
     <Untitled>
         <FirstName>Jerry</FirstName>
         <LastName>Johnson</LastName>
         <Amount>250000</Amount>
     </Untitled>
```

次の図に示すように、確認フォームにこのXMLデータソースを事前入力し、フォームをレンダリングすると、XML要素に割り当てたデータ値が表示されます。

![pf_pf_confirmxml3](assets/pf_pf_confirmxml3.png)

### 編集可能なレイアウトでのフォームの自動埋め込み {#prepopulating_forms_with_flowable_layouts-1}

編集可能なレイアウトを含むフォームは、不確定な量のデータをユーザーに表示する場合に便利です。 フォームのレイアウトはマージされるデータ量に合わせて自動的に調整されるので、固定レイアウトのフォームとは異なり、固定レイアウトやフォームのページ数を事前に決定する必要はありません。

通常、フォームには実行時に取得されるデータが入力されます。 その結果、メモリ内XMLデータソースを作成し、そのデータをメモリ内XMLデータソースに直接配置することで、フォームの自動埋め込みを行うことができます。

オンラインストアなど、Webベースのアプリケーションを考えます。 オンライン買い物客がアイテムの購入を完了すると、購入したすべてのアイテムが、フォームの自動埋め込みに使用されるメモリ内XMLデータソースに配置されます。 次の図に、このプロセスを示します。このプロセスについて、図の後の表で説明します。

![pf_pf_finsrv_webapp_v1](assets/pf_pf_finsrv_webapp_v1.png)

次の表に、この図の手順を示します。

<table>
 <thead>
  <tr>
   <th><p>ステップ</p></th>
   <th><p>説明</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>ユーザは、ウェブベースのオンラインストアからアイテムを購入する。 </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>ユーザーが項目の購入を完了し、「送信」ボタンをクリックすると、メモリ内XMLデータソースが作成されます。 購入したアイテムとユーザー情報は、メモリ内XMLデータソースに配置されます。 </p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>XMLデータソースは、発注書フォームの自動埋め込みに使用されます（このフォームの例を次の表に示します）。 </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>発注書フォームがクライアントWebブラウザーにレンダリングされます。 </p></td>
  </tr>
 </tbody>
</table>

次の図に、発注書フォームの例を示します。 表の情報は、XMLデータのレコード数に合わせて調整できます。

![pf_pf_poform](assets/pf_pf_poform.png)

>[!NOTE]
>
>フォームには、エンタープライズデータベースや外部アプリケーションなど、他のソースのデータを事前入力することができます。

### フォームデザインに関する考慮事項 {#form-design-considerations}

編集可能なレイアウトを含むフォームは、Designerで作成されたフォームデザインに基づいています。 フォームデザインでは、ユーザー入力に基づく値の計算を含む、一連のレイアウト、プレゼンテーション、データ取得ルールを指定します。 ルールは、データがフォームに入力されるときに適用されます。 フォームに追加されるフィールドは、フォームデザイン内のサブフォームです。 例えば、前の図に示した発注書フォームでは、各行がサブフォームです。 サブフォームを含むフォームデザインの作成について詳しくは、編集可能なレイア [ウトを含む発注書フォームの作成を参照してください](https://www.adobe.com/go/learn_aemforms_qs_poformflowable_9)。

### データ・サブグループについて {#understanding-data-subgroups}

XMLデータソースは、フォームに固定レイアウトと編集可能なレイアウトを事前入力するために使用します。 ただし、フォームに編集可能なレイアウトを自動埋め込むXMLデータソースには、フォーム内で繰り返されるサブフォームの自動埋め込みに使用される繰り返しXML要素が含まれている点が異なります。 これらの繰り返しXML要素は、データサブグループと呼ばれます。

前の図に示した発注書フォームの自動埋め込みに使用されるXMLデータソースには、4つの繰り返しデータサブグループが含まれています。 各データサブグループは購入した品目に対応しています。 購入したアイテムは、モニター、卓上ランプ、電話、アドレス帳です。

発注書フォームの自動埋め込みには、次のXMLデータソースが使用されます。

```as3
     <header>
         <!-- XML elements used to prepopulate non-repeating fields such as address
         <!and city
         <txtPONum>8745236985</txtPONum>
         <dtmDate>2004-02-08</dtmDate>
         <txtOrderedByCompanyName>Any Company Name</txtOrderedByCompanyName>
         <txtOrderedByAddress>555, Any Blvd.</txtOrderedByAddress>
         <txtOrderedByCity>Any City</txtOrderedByCity>
         <txtOrderedByStateProv>ST</txtOrderedByStateProv>
         <txtOrderedByZipCode>12345</txtOrderedByZipCode>
         <txtOrderedByCountry>Any Country</txtOrderedByCountry>
         <txtOrderedByPhone>(123) 456-7890</txtOrderedByPhone>
         <txtOrderedByFax>(123) 456-7899</txtOrderedByFax>
         <txtOrderedByContactName>Contact Name</txtOrderedByContactName>
         <txtDeliverToCompanyName>Any Company Name</txtDeliverToCompanyName>
         <txtDeliverToAddress>7895, Any Street</txtDeliverToAddress>
         <txtDeliverToCity>Any City</txtDeliverToCity>
         <txtDeliverToStateProv>ST</txtDeliverToStateProv>
         <txtDeliverToZipCode>12346</txtDeliverToZipCode>
         <txtDeliverToCountry>Any Country</txtDeliverToCountry>
         <txtDeliverToPhone>(123) 456-7891</txtDeliverToPhone>
         <txtDeliverToFax>(123) 456-7899</txtDeliverToFax>
         <txtDeliverToContactName>Contact Name</txtDeliverToContactName>
     </header>
     <detail>
         <!-- A data subgroup that contains information about the monitor>
         <txtPartNum>00010-100</txtPartNum>
         <txtDescription>Monitor</txtDescription>
         <numQty>1</numQty>
         <numUnitPrice>350.00</numUnitPrice>
     </detail>
     <detail>
         <!-- A data subgroup that contains information about the desk lamp>
         <txtPartNum>00010-200</txtPartNum>
         <txtDescription>Desk lamps</txtDescription>
         <numQty>3</numQty>
         <numUnitPrice>55.00</numUnitPrice>
     </detail>
     <detail>
         <!-- A data subgroup that contains information about the Phone>
             <txtPartNum>00025-275</txtPartNum>
             <txtDescription>Phone</txtDescription>
             <numQty>5</numQty>
             <numUnitPrice>85.00</numUnitPrice>
     </detail>
     <detail>
         <!-- A data subgroup that contains information about the address book>
         <txtPartNum>00300-896</txtPartNum>
         <txtDescription>Address book</txtDescription>
         <numQty>2</numQty>
         <numUnitPrice>15.00</numUnitPrice>
     </detail>
```

各データサブグループには、次の情報に対応する4つのXML要素が含まれています。

* 項目の部品番号
* 項目の説明
* 品目数量
* 単価

データサブグループの親XML要素の名前は、フォームデザイン内のサブフォームの名前と一致する必要があります。 例えば、前の図では、データサブグループの親XML要素の名前がになっています `detail`。 これは、発注書フォームの基になるフォームデザイン内のサブフォームの名前に対応します。 データサブグループの親XML要素の名前とサブフォームが一致しない場合、サーバー側のフォームは事前入力されません。

各データサブグループには、サブフォーム内のフィールド名と一致するXML要素が含まれている必要があります。 フォーム `detail` デザイン内のサブフォームには、次のフィールドが含まれています。

* txtPartNum
* txtDescription
* numQty
* numUnitPrice

>[!NOTE]
>
>繰り返しXML要素を含むデータソースを使用してフォームに自動埋め込みを行う場合、このオプションを「 `RenderAtClient` 」に設定 `No`すると、最初のデータレコードのみがフォームにマージされます。 すべてのデータレコードが確実にフォームにマージされるようにするには、をに設 `RenderAtClient` 定しま `Yes`す。 このオプションについて詳しくは、「ク `RenderAtClient` ライアントでのフ [ォームのレンダリング」を参照してください](/help/forms/developing/rendering-forms-client.md)。

>[!NOTE]
>
>For more information about the Forms service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary-of-steps}

編集可能なレイアウトでフォームを自動埋め込むには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. メモリ内XMLデータソースを作成します。
1. XMLデータソースを変換します。
1. 事前入力されたフォームをレンダリングします。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

**メモリ内XMLデータソースの作成**

クラスを使用して、 `org.w3c.dom` メモリ内XMLデータソースを作成し、編集可能なレイアウトでフォームに自動埋め込みを行うことができます。 フォームに適合するXMLデータソースにデータを配置する必要があります。 編集可能なレイアウトを含むフォームとXMLデータソースとの関係について詳しくは、 [Understanding data subgropes](/help/forms/developing/rendering-forms-rendering-forms prepopulating-forms-flowable-layouts-prepopulating-forms-flowable-layouts-prepogulates.md#underd-data-subgroups)を参照してください。

**XMLデータソースの変換**

クラスを使用して作成されたメモリ内XMLデータソースは、フォ `org.w3c.dom` ームの自動埋め込みに使用する前にオ `com.adobe.idp.Document` ブジェクトに変換することができます。 メモリ内XMLデータソースは、Java XML変換クラスを使用して変換できます。

>[!NOTE]
>
>FormsサービスのWSDLを使用してフォームを自動埋め込む場合は、オブジェクトをオブジェクトに変換す `org.w3c.dom.Document` る必要があり `BLOB` ます。

**事前入力されたフォームのレンダリング**

事前入力されたフォームは、他のフォームと同様にレンダリングします。 唯一の違いは、XMLデータソースを含むオ `com.adobe.idp.Document` ブジェクトを使用してフォームに自動埋め込みを行う点です。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[FormsサービスAPIのクイックスタート](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[インタラクティブPDFフォームのレンダリング](/help/forms/developing/rendering-interactive-pdf-forms.md)

[フォームをレンダリングするWebアプリケーションの作成](/help/forms/developing/creating-web-applications-renders-forms.md)

### Java APIを使用したフォームの自動埋め込み {#prepopulating-forms-using-the-java-api}

Forms API(Java)を使用して編集可能なレイアウトでフォームを事前入力するには、次の手順を実行します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-forms-client.jarなどのクライアントJARファイルを含めます。 これらのファイルの場所については、[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。

1. メモリ内XMLデータソースの作成

   * クラスのメソッド `DocumentBuilderFactory` を呼び出して、Javaオブジ `DocumentBuilderFactory` ェクトを作成 `newInstance` します。
   * オブジェクトのメ `DocumentBuilder` ソッドを呼び出して、Java `DocumentBuilderFactory` オブジェクトを作成 `newDocumentBuilder` します。
   * オブジェクトのメ `DocumentBuilder` ソッドを呼び出し `newDocument` て、オブジェクトをインスタンス化 `org.w3c.dom.Document` します。
   * オブジェクトのメソッドを呼び出して、XMLデータソースのル `org.w3c.dom.Document` ート要素を作成 `createElement` します。 これにより、ルート `Element` 要素を表すオブジェクトが作成されます。 要素の名前を表すstring値をメソッドに渡し `createElement` ます。 戻り値を `Element` にキャストします。次に、オブジェクトのメソッドを呼び出してルート要素をドキュメ `Document` ントに追加し、ル `appendChild` ート要素オブジェクトを引数として渡します。 次のコード行に、このアプリケーションロジックを示します。

      ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * オブジェクトのメソッドを呼び出して、XMLデータソースのヘッ `Document` ダー要素を作成 `createElement` します。 要素の名前を表すstring値をメソッドに渡し `createElement` ます。 戻り値を `Element` にキャストします。次に、オブジェクトのメソッドを呼び出して、ルート要素に `root` ヘッダー要素を追 `appendChild` 加し、ヘッダー要素オブジェクトを引数として渡します。 ヘッダー要素に追加されるXML要素は、フォームの静的な部分に対応します。 次のコード行に、このアプリケーションロジックを示します。

      ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * オブジェクトのメソッドを呼び出して、header要素に属する子要素を作 `Document` 成し、要 `createElement` 素の名前を表すstring値を渡します。 戻り値を `Element` にキャストします。次に、子要素のメソッドを呼び出して値を設定 `appendChild` し、オブジェクトのメ `Document` ソッドを引 `createTextNode` 数として渡します。 子要素の値として表示するstring値を指定します。 最後に、header要素のメソッドを呼び出して、header要素に子要素を追加し、 `appendChild` 子要素オブジェクトを引数として渡します。 次のコード行に、このアプリケーションロジックを示します。

      ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`


   * フォームの静的部分に表示される各フィールドの最後のサブステップを繰り返して、残りのすべての要素をヘッダー要素に追加します（XMLデータソース図では、A節に示します）。(データサブグ [ループについてを参照](#understanding-data-subgroups))。
   * オブジェクトのメソッドを呼び出して、XMLデータソースの `Document` 詳細要素を作成 `createElement` します。 要素の名前を表すstring値をメソッドに渡し `createElement` ます。 戻り値を `Element` にキャストします。次に、オブジェクトのメソッドを呼び出してルート要素に `root` 詳細要素を追加 `appendChild` し、引数としてdetail要素オブジェクトを渡します。 detail要素に追加されるXML要素は、フォームの動的な部分に対応しています。 次のコード行に、このアプリケーションロジックを示します。

      ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * オブジェクトのメソッドを呼び出して、detail要素に属する子要素 `Document` を作成し、要 `createElement` 素の名前を表すstring値を渡します。 戻り値を `Element` にキャストします。次に、子要素のメソッドを呼び出して値を設定 `appendChild` し、オブジェクトのメ `Document` ソッドを引 `createTextNode` 数として渡します。 子要素の値として表示するstring値を指定します。 最後に、detail要素のメソッドを呼び出して子要素をdetail要素に追加し、 `appendChild` 子要素オブジェクトを引数として渡します。 次のコード行に、このアプリケーションロジックを示します。

      ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * 詳細要素に追加するすべてのXML要素に対して、最後のサブ手順を繰り返します。 発注書フォームへの入力に使用するXMLデータソースを正しく作成するには、次のXML要素を詳細要素に追加する必要があります。 `txtDescription`、 `numQty`、、 `numUnitPrice`、
   * フォームの自動埋め込みに使用するすべてのデータ項目に対して、最近の2つのサブ手順を繰り返します。

1. XMLデータソースの変換

   * オブジェクト `javax.xml.transform.Transformer` の静的メソッドを呼び出し `javax.xml.transform.Transformer` て、オブジェクトを作成 `newInstance` します。
   * オブジェクト `Transformer` のメソッドを呼び出して、オ `TransformerFactory` ブジェクトを作成 `newTransformer` します。
   * コンストラクタを使用して `ByteArrayOutputStream` オブジェクトを作成します。
   * コンストラク `javax.xml.transform.dom.DOMSource` ターを使用し、手順1で作成したオブジ `org.w3c.dom.Document` ェクトを渡して、オブジェクトを作成します。
   * コンストラクタを使用して `javax.xml.transform.dom.DOMSource` オブジェクトを渡すことによって、`ByteArrayOutputStream` オブジェクトを作成します。
   * オブジェクトのメ `ByteArrayOutputStream` ソッドを呼び出し、オブ `javax.xml.transform.Transformer` ジェクトとオ `transform` ブジェクトを渡すことで、Javaオ `javax.xml.transform.dom.DOMSource` ブジェク `javax.xml.transform.stream.StreamResult` トを設定します。
   * バイト配列を作成し、オブジェクトのサイズをバ `ByteArrayOutputStream` イト配列に割り当てます。
   * オブジェクトのメソッドを呼び出して、バ `ByteArrayOutputStream` イト配列を設定 `toByteArray` します。
   * Create a `com.adobe.idp.Document` object by using its constructor and passing the byte array.

1. 事前入力されたフォームのレンダリング

   オブジェクト `FormsServiceClient` のメソッドを `renderPDFForm` 呼び出し、次の値を渡します。

   * ファイル名の拡張子を含むフォームデザイン名を指定するstring値。
   * フォーム `com.adobe.idp.Document` とマージするデータを含むオブジェクトです。 手順1と2で作成したオブ `com.adobe.idp.Document` ジェクトを必ず使用してください。
   * 実行時 `PDFFormRenderSpec` のオプションを格納するオブジェクトです。
   * Formsサ `URLSpec` ービスに必要なURI値を含むオブジェクトです。
   * 添付フ `java.util.HashMap` ァイルを格納するオブジェクト。 これはオプションのパラメーターで、フォームにフ `null` ァイルを添付しないかどうかを指定できます。
   このメソ `renderPDFForm` ッドは、クライア `FormsResult` ントのWebブラウザーに書き込む必要があるフォームデータストリームを含むオブジェクトを返します。

   * フォームデー `javax.servlet.ServletOutputStream` タストリームをクライアントWebブラウザーに送信するために使用するオブジェクトを作成します。
   * オブジェクトの `com.adobe.idp.Document` メソッドを呼び出して、オ `FormsResult` ブジェクトを作成 `getOutputContent` します。
   * オブジェクト `java.io.InputStream` のメソッドを呼び出して、オ `com.adobe.idp.Document` ブジェクトを作成 `getInputStream` します。
   * バイト配列を作成し、オブジェクトのメソッドを呼び出し、バイト配列を引 `InputStream` 数として渡すこ `read` とによって、フォームデータストリームを設定します。
   * オブジェクト `javax.servlet.ServletOutputStream` のメソッドを呼び `write` 出して、フォームデータストリームをクライアントWebブラウザーに送信します。 バイト配列をメソッドに渡し `write` ます。


**関連トピック**

[クイックスタート（SOAPモード）:Java APIを使用した編集可能なレイアウトでのフォームの自動埋め込み](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したフォームの事前入力 {#prepopulating-forms-using-the-web-service-api}

Forms API（Webサービス）を使用して編集可能なレイアウトでフォームを事前入力するには、次の手順を実行します。

1. プロジェクトファイルを含める

   * FormsサービスWSDLを使用するJavaプロキシクラスを作成します。 (Apache Axisを使 [用したJavaプロキシクラスの作成を参照](/help/forms/developing/invoking-aem-forms-using-web.md#creating-java-proxy-classes-using-apache-axis))。
   * クラスパスにJavaプロキシクラスを含めます。

1. メモリ内XMLデータソースの作成

   * クラスのメソッド `DocumentBuilderFactory` を呼び出して、Javaオブジ `DocumentBuilderFactory` ェクトを作成 `newInstance` します。
   * オブジェクトのメ `DocumentBuilder` ソッドを呼び出して、Java `DocumentBuilderFactory` オブジェクトを作成 `newDocumentBuilder` します。
   * オブジェクトのメ `DocumentBuilder` ソッドを呼び出し `newDocument` て、オブジェクトをインスタンス化 `org.w3c.dom.Document` します。
   * オブジェクトのメソッドを呼び出して、XMLデータソースのル `org.w3c.dom.Document` ート要素を作成 `createElement` します。 これにより、ルート `Element` 要素を表すオブジェクトが作成されます。 要素の名前を表すstring値をメソッドに渡し `createElement` ます。 戻り値を `Element` にキャストします。次に、オブジェクトのメソッドを呼び出してルート要素をドキュメ `Document` ントに追加し、ル `appendChild` ート要素オブジェクトを引数として渡します。 次のコード行に、このアプリケーションロジックを示します。

      ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * オブジェクトのメソッドを呼び出して、XMLデータソースのヘッ `Document` ダー要素を作成 `createElement` します。 要素の名前を表すstring値をメソッドに渡し `createElement` ます。 戻り値を `Element` にキャストします。次に、オブジェクトのメソッドを呼び出して、ルート要素に `root` ヘッダー要素を追 `appendChild` 加し、ヘッダー要素オブジェクトを引数として渡します。 ヘッダー要素に追加されるXML要素は、フォームの静的な部分に対応します。 次のコード行に、このアプリケーションロジックを示します。

      ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * オブジェクトのメソッドを呼び出して、header要素に属する子要素を作 `Document` 成し、要 `createElement` 素の名前を表すstring値を渡します。 戻り値を `Element` にキャストします。次に、子要素のメソッドを呼び出して値を設定 `appendChild` し、オブジェクトのメ `Document` ソッドを引 `createTextNode` 数として渡します。 子要素の値として表示するstring値を指定します。 最後に、header要素のメソッドを呼び出して、header要素に子要素を追加し、 `appendChild` 子要素オブジェクトを引数として渡します。 次のコード行に、このアプリケーションロジックを示します。

      ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`

   * フォームの静的部分に表示される各フィールドの最後のサブステップを繰り返して、残りのすべての要素をヘッダー要素に追加します（XMLデータソース図では、A節に示します）。(データサブグ [ループについてを参照](#understanding-data-subgroups))。
   * オブジェクトのメソッドを呼び出して、XMLデータソースの `Document` 詳細要素を作成 `createElement` します。 要素の名前を表すstring値をメソッドに渡し `createElement` ます。 戻り値を `Element` にキャストします。次に、オブジェクトのメソッドを呼び出してルート要素に `root` 詳細要素を追加 `appendChild` し、引数としてdetail要素オブジェクトを渡します。 detail要素に追加されるXML要素は、フォームの動的な部分に対応しています。 次のコード行に、このアプリケーションロジックを示します。

      ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * オブジェクトのメソッドを呼び出して、detail要素に属する子要素 `Document` を作成し、要 `createElement` 素の名前を表すstring値を渡します。 戻り値を `Element` にキャストします。次に、子要素のメソッドを呼び出して値を設定 `appendChild` し、オブジェクトのメ `Document` ソッドを引 `createTextNode` 数として渡します。 子要素の値として表示するstring値を指定します。 最後に、detail要素のメソッドを呼び出して子要素をdetail要素に追加し、 `appendChild` 子要素オブジェクトを引数として渡します。 次のコード行に、このアプリケーションロジックを示します。

      ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * 詳細要素に追加するすべてのXML要素に対して、最後のサブ手順を繰り返します。 発注書フォームへの入力に使用するXMLデータソースを正しく作成するには、次のXML要素を詳細要素に追加する必要があります。 `txtDescription`、 `numQty`、、 `numUnitPrice`、
   * フォームの自動埋め込みに使用するすべてのデータ項目に対して、最近の2つのサブ手順を繰り返します。

1. XMLデータソースの変換

   * オブジェクト `javax.xml.transform.Transformer` の静的メソッドを呼び出し `javax.xml.transform.Transformer` て、オブジェクトを作成 `newInstance` します。
   * オブジェクト `Transformer` のメソッドを呼び出して、オ `TransformerFactory` ブジェクトを作成 `newTransformer` します。
   * コンストラクタを使用して `ByteArrayOutputStream` オブジェクトを作成します。
   * コンストラク `javax.xml.transform.dom.DOMSource` ターを使用し、手順1で作成したオブジ `org.w3c.dom.Document` ェクトを渡して、オブジェクトを作成します。
   * コンストラクタを使用して `javax.xml.transform.dom.DOMSource` オブジェクトを渡すことによって、`ByteArrayOutputStream` オブジェクトを作成します。
   * オブジェクトのメ `ByteArrayOutputStream` ソッドを呼び出し、オブ `javax.xml.transform.Transformer` ジェクトとオ `transform` ブジェクトを渡すことで、Javaオ `javax.xml.transform.dom.DOMSource` ブジェク `javax.xml.transform.stream.StreamResult` トを設定します。
   * バイト配列を作成し、オブジェクトのサイズをバ `ByteArrayOutputStream` イト配列に割り当てます。
   * オブジェクトのメソッドを呼び出して、バ `ByteArrayOutputStream` イト配列を設定 `toByteArray` します。
   * コンストラクタ `BLOB` ーを使用してオブジェクトを作成し、そのメソッドを呼び出 `setBinaryData` して、バイト配列を渡します。

1. 事前入力されたフォームのレンダリング

   オブジェクト `FormsService` のメソッドを `renderPDFForm` 呼び出し、次の値を渡します。

   * ファイル名の拡張子を含むフォームデザイン名を指定するstring値。
   * フォーム `BLOB` とマージするデータを含むオブジェクトです。 手順1と2で作成したオ `BLOB` ブジェクトを必ず使用してください。
   * 実行時 `PDFFormRenderSpecc` のオプションを格納するオブジェクトです。 For more information, see [AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Formsサ `URLSpec` ービスに必要なURI値を含むオブジェクトです。
   * 添付フ `java.util.HashMap` ァイルを格納するオブジェクト。 これはオプションのパラメーターで、フォームにフ `null` ァイルを添付しないかどうかを指定できます。
   * メソッドに `com.adobe.idp.services.holders.BLOBHolder` よって入力される空のオブジェクトです。 これは、レンダリングされたPDFフォームを保存するために使用します。
   * メソッドに `javax.xml.rpc.holders.LongHolder` よって入力される空のオブジェクトです。 （この引数には、フォーム内のページ数が格納されます）。
   * メソッドに `javax.xml.rpc.holders.StringHolder` よって入力される空のオブジェクトです。 （この引数はロケールの値を格納します）。
   * この操作 `com.adobe.idp.services.holders.FormsResultHolder` の結果を含む空のオブジェクトです。
   メソッド `renderPDFForm` は、最後の引 `com.adobe.idp.services.holders.FormsResultHolder` 数値として渡されたオブジェクトに、クライアントWebブラウザーに書き込む必要があるフォームデータストリームを入力します。

   * オブジェクト `FormResult` のデータメンバーの値を取得して、オ `com.adobe.idp.services.holders.FormsResultHolder` ブジェクトを `value` 作成します。
   * オブジェクトの `BLOB` メソッドを呼び出して、フォームデータを含むオ `FormsResult` ブジェクトを作成 `getOutputContent` します。
   * メソッドを呼び出して、オブジェ `BLOB` クトのコンテンツタイプを取得 `getContentType` します。
   * メソッドを呼 `javax.servlet.http.HttpServletResponse` び出し、オブジェクトのコンテンツタ `setContentType` イプを渡すことで、オブジェクトのコンテンツタイプを設定 `BLOB` します。
   * オブジェクトの `javax.servlet.ServletOutputStream` メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに書き込むために使用する `javax.servlet.http.HttpServletResponse` オブジェクトを作 `getOutputStream` 成します。
   * バイト配列を作成し、オブジェクトのメソッドを呼び出 `BLOB` して値を設定 `getBinaryData` します。 このタスクは、オブジェクトの内容をバ `FormsResult` イト配列に割り当てます。
   * オブジェクト `javax.servlet.http.HttpServletResponse` のメソッドを呼び `write` 出して、フォームデータストリームをクライアントWebブラウザーに送信します。 バイト配列をメソッドに渡し `write` ます。
   >[!NOTE]
   >
   >メソッド `renderPDFForm` は、最後の引 `com.adobe.idp.services.holders.FormsResultHolder` 数値として渡されたオブジェクトに、クライアントWebブラウザーに書き込む必要があるフォームデータストリームを入力します。

**関連トピック**

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

