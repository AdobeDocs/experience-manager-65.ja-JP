---
title: 編集可能なレイアウトを使用した Forms の事前入力
seo-title: Prepopulating Forms with Flowable Layouts
description: Java API と web サービス API を使用して、レンダリングされたフォーム内のユーザーにデータを表示するための、フォームに編集可能なレイアウトを事前入力してください。
seo-description: Prepopulate forms with flowable layout to display data to users within a rendered form using the Java API and the Web Service API.
uuid: 93ccb496-e1c2-4b79-8e89-7a2abfce1537
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 30a12fc6-07b8-4c7c-b9e2-caa2bec0ac48
role: Developer
exl-id: ff087084-fb1c-43a4-ae54-cc77eb862493
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: tm+mt
source-wordcount: '3505'
ht-degree: 99%

---

# 編集可能なレイアウトを使用した Forms の事前入力 {#prepopulating-forms-with-flowable-layouts1}

## 編集可能なレイアウトを使用した Forms の事前入力 {#prepopulating-forms-with-flowable-layouts2}

フォームに事前入力すると、レンダリングされたフォーム内でユーザーにデータが表示されます。例えば、あるユーザーが、ユーザー名とパスワードを使用して web サイトにログインしたとします。認証に成功した場合、クライアントアプリケーションはデータベースに対してユーザー情報を問い合わせます。データがフォームに結合され、フォームがユーザーにレンダリングされます。その結果、ユーザーはフォーム内でパーソナライズされたデータを表示できます。

フォームの事前入力には次の利点があります。

* ユーザーがフォーム内にカスタムデータを表示できる。
* ユーザーがフォームに入力する作業を削減できる。
* データを配置する場所を制御できるため、データの整合性を確保できる。

次の 2 つの XML データソースから、 フォームの自動埋め込み行うことができます。

* XDP データソース。XFA 構文に準拠する XML です ( または、Acrobat を使用して作成されたフォームに事前入力する XFDF データ )。
* フォームのフィールド名に一致する名前と値のペアを含む任意の XML データソース（この節の例では、任意の XML データソースを使用します）。

事前入力するフォームフィールドごとに、XML 要素が存在する必要があります。XML 要素名は、フィールド名と一致する必要があります。XML 要素がフォームフィールドに対応していない場合や、XML 要素名がフィールド名と一致しない場合、XML 要素は無視されます。すべての XML 要素が指定されている場合、XML 要素の表示順序を一致させる必要はありません。

既にデータを含むフォームに事前入力する場合は、XML データソース内に既に表示されているデータを指定する必要があります。10 個のフィールドを含むフォームの 4 個のフィールドにデータが含まれているとします。次に、残り 6 個のフィールドに事前入力するとします。この場合、フォームの事前入力に使用する 10 個の XML 要素を XML データソースに指定する必要があります。6 個の要素のみを指定した場合、元の 4 個のフィールドは空になります。

例えば、サンプルの確認フォームなどのフォームを事前入力することができます。( [インタラクティブPDF formsのレンダリング](/help/forms/developing/rendering-interactive-pdf-forms.md).)

サンプルの確認フォームを事前入力するには、フォーム内の 3 個のフィールドに一致する 3 個の XML 要素を含む XML データソースを作成する必要があります。このフォームには、 `FirstName`、`LastName`、`Amount` の 3 個のフィールドが含まれています。最初のステップでは、フォームデザイン内のフィールドと一致する XML 要素を含む XML データソースを作成します。次のステップでは、次の XML コードに示すように、XML 要素にデータ値を割り当てます。

```xml
     <Untitled>
         <FirstName>Jerry</FirstName>
         <LastName>Johnson</LastName>
         <Amount>250000</Amount>
     </Untitled>
```

次の図に示すように、この XML データソースを確認フォームに事前入力し、フォームをレンダリングすると、XML 要素に割り当てたデータ値が表示されます。

![pf_pf_confirmxml3](assets/pf_pf_confirmxml3.png)

### 編集可能なレイアウトを使用したフォームの事前入力 {#prepopulating_forms_with_flowable_layouts-1}

レイアウトが編集可能な Forms は、未定量のデータをユーザーに表示する場合に役立ちます。フォームのレイアウトは結合されるデータ量に合わせて自動的に調整されるので、固定レイアウトのフォームの場合とは異なり、フォームの固定レイアウトやページ数を事前に決定する必要はありません。

通常、フォームには、実行時に取得されるデータが入力されます。その結果、メモリ内 XML データソースを作成し、そのデータをメモリ内 XML データソースに直接配置することで、フォームに事前入力することができます。

Web ベースのアプリケーション（オンラインストアなど）を考えてみましょう。オンライン買い物客が品目の購入を完了すると、購入したすべての品目は、フォームの事前入力に使用されるメモリ内 XML データソースに配置されます。次の図に、このプロセスを示します。このプロセスについて、図の後の表で説明します。

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
   <td><p>ユーザーは、web ベースのオンラインストアから品目を購入します。 </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>ユーザーが品目の購入を完了し、「送信」ボタンをクリックすると、メモリ内 XML データソースが作成されます。購入した品目とユーザー情報は、メモリ内 XML データソースに配置されます。 </p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>XML データソースが、発注書フォームの事前入力に使用されます（このフォームの例を次の表に示します）。 </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>発注書フォームがクライアントの web ブラウザーにレンダリングされます。 </p></td>
  </tr>
 </tbody>
</table>

次の図に、発注書フォームの例を示します。テーブル内の情報は、XML データ内のレコード数に合わせて調整できます。

![pf_pf_poform](assets/pf_pf_poform.png)

>[!NOTE]
>
>フォームには、エンタープライズデータベースや外部アプリケーションなど、他のソースからのデータを事前入力することができます。

### フォームデザインの考慮事項 {#form-design-considerations}

編集可能なレイアウトの Forms は、Designer で作成されたフォームデザインに基づいています。フォームデザインでは、ユーザー入力に基づく値の計算を含む、レイアウト、プレゼンテーション、データ取得のルールのセットを指定してください。ルールは、データがフォームに入力される際に適用されます。フォームに追加されるフィールドは、フォームデザイン内のサブフォームです。例えば、前の図で示した発注書フォームでは、各行がサブフォームになっています。サブフォームを含むフォームデザインの作成について詳しくは、 [編集可能なレイアウトを含む発注書フォームの作成](https://www.adobe.com/go/learn_aemforms_qs_poformflowable_9_jp)を参照してください。

### データのサブグループについて {#understanding-data-subgroups}

固定レイアウトと編集可能なレイアウトを使用したフォームの事前入力には、XML データソースが使用されます。ただし、編集可能なレイアウトのフォームの事前入力に使用される XML データソースには、フォーム内で繰り返されるサブフォームの事前入力に使用される「繰り返し XML 要素」が含まれているという相違点があります。これらの繰り返し XML 要素は、データサブグループと呼ばれます。

前の図に示す発注書フォームの事前入力に使用する XML データソースには、4 つの繰り返しデータのサブグループが含まれています。各データサブグループは、購入した品目に対応します。購入した品目は、モニター、デスクランプ、電話、アドレス帳です。

発注書フォームの事前入力には、次の XML データソースが使用されます。

```xml
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

各データサブグループには、この情報に対応する 4 つの XML 要素が含まれています。

* 品目のパーツ番号
* 品目の説明
* 品目の数量
* 単価

データサブグループの親 XML 要素の名前は、フォームデザイン内のサブフォームの名前と一致する必要があります。例えば、前の図では、データサブグループの親 XML 要素の名前が `detail` になっています。これは、発注書フォームの基になるフォームデザインにあるサブフォームの名前に対応します。データサブグループの親 XML 要素の名前とサブフォームが一致しない場合、サーバー側のフォームは事前入力されません。

各データサブグループには、サブフォーム内のフィールド名に一致する XML 要素が含まれている必要があります。フォームデザインにある `detail` サブフォームには、次のフィールドが含まれます。

* txtPartNum
* txtDescription
* numQty
* numUnitPrice

>[!NOTE]
>
>繰り返し XML 要素を含むデータソースをフォームに事前入力しようとして、`RenderAtClient` 選択肢を `No` に設定すると、最初のデータレコードのみがフォームに結合されます。すべてのデータレコードが確実にフォームに結合されるようにするには、`RenderAtClient` を `Yes` に設定してください。`RenderAtClient` オプションについて詳しくは、[クライアントでの Forms のレンダリング](/help/forms/developing/rendering-forms-client.md)を参照してください。

>[!NOTE]
>
>Forms サービスについて詳しくは、[AEM Forms サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary-of-steps}

フォームに編集可能なレイアウトを事前入力するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. メモリ内 XML データソースを作成します。
1. XML データソースを変換します。
1. 事前入力されたフォームをレンダリングします。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**メモリ内 XML データソースの作成**

`org.w3c.dom` クラスを使用して、メモリ内の XML データソースを作成し、編集可能なレイアウトでフォームを事前入力できます。フォームに準拠する XML データソースにデータを配置する必要があります。編集可能なレイアウトを含むフォームと XML データソースとの関係について詳しくは、[データのサブグループについて](#understanding-data-subgroups)を参照してください。

 **XML データソースを変換**

`org.w3c.dom` クラスを使用して作成されたメモリ内 XML データソースは、フォームの事前入力に使用する前に、`com.adobe.idp.Document` オブジェクトに変換できます。メモリ内 XML データソースは、Java XML 変換クラスを使用して変換できます。

>[!NOTE]
>
>Forms サービスの WSDL を使用してフォームを事前入力する場合は、 `org.w3c.dom.Document` オブジェクトを `BLOB` オブジェクトに変換する必要があります。

**事前入力されたフォームをレンダリング**

事前入力されたフォームは、他のフォームと同様にレンダリングされます。唯一の違いは、XML データソースを含む `com.adobe.idp.Document` オブジェクトを使用してフォームに事前入力するということです。

**関連トピック**

[AEM Forms Java ライブラリファイルの組み込み](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms サービス API のクイックスタート](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[インタラクティブ PDF Forms のレンダリング](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Forms をレンダリングする web アプリケーションの作成](/help/forms/developing/creating-web-applications-renders-forms.md)

### Java API を使用したフォームの事前入力 {#prepopulating-forms-using-the-java-api}

Forms API（Java）を使用して、編集可能なレイアウトでフォームに事前入力するには、次の手順を実行します。

1. プロジェクトファイルを含める

   adobe-livecycle-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。これらのファイルの場所については、[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。

1. メモリ内 XML データソースの作成

   * `DocumentBuilderFactory` クラスの `newInstance` メソッドを呼び出して Java の `DocumentBuilderFactory` オブジェクトを作成します。
   * `DocumentBuilderFactory` オブジェクトの `newDocumentBuilder` メソッドを呼び出して、Java の `DocumentBuilder` オブジェクトを作成します。 
   * `DocumentBuilder` オブジェクトの `newDocument` メソッドを呼び出して、`org.w3c.dom.Document` オブジェクトをインスタンス化します。
   * `org.w3c.dom.Document` オブジェクトの `createElement` メソッドを呼び出して、XML データソースのルート要素を作成します。これにより、ルート要素を表す `Element` オブジェクトが作成されます。要素名を表す文字列値を `createElement` メソッドに渡します。戻り値を `Element` にキャストします。次に、`Document` オブジェクトの `appendChild` メソッドを呼び出してルート要素オブジェクトを引数として渡すことによって、ルート要素をドキュメントに追加します。次のコード行に、このアプリケーションロジックを示します。

      ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * `Document` オブジェクトの `createElement` メソッドを呼び出して、XML データソースのヘッダー要素を作成します。要素名を表す文字列値を `createElement` メソッドに渡します。戻り値を `Element` にキャストします。次に、 `root` オブジェクトの `appendChild` メソッドを呼び出してヘッダー要素オブジェクトを引数として渡し、ヘッダー要素をドキュメントに追加します。ヘッダー要素に追加される XML 要素は、フォームの静的な部分に対応します。次のコード行は、このアプリケーションロジックを示しています。

      ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * `Document` オブジェクトの `createElement` メソッドを呼び出して要素名を表す文字列値を渡すことによって、ヘッダー要素に属する子要素を作成します。戻り値を `Element` にキャストします。次に、`appendChild` メソッドを呼び出して、`Document` オブジェクトの `createTextNode` メソッドを引数として渡すことによって、子要素の値を設定します。子要素の値として表示される文字列値を指定します。最後に、ヘッダー要素の `appendChild` メソッドを呼び出して、子要素オブジェクトを引数として渡すことによって、子要素をヘッダー要素に追加します。次のコード行は、このアプリケーションロジックを示しています。

      ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`


   * フォームの静的部分に表示される各フィールドに対して最後のサブ手順を繰り返して、残りのすべての要素をヘッダー要素に追加します（XML データソース図では、これらのフィールドがセクション A に表示されます（[データのサブグループについて](#understanding-data-subgroups)を参照）。
   * `Document` オブジェクトの `createElement` メソッドを呼び出して、XML データソースの詳細要素を作成します。要素の名前を表す文字列値を `createElement` メソッドに渡します。戻り値を `Element` にキャストします。次に、`root` オブジェクトの `appendChild` メソッドを呼び出して、詳細要素オブジェクトを引数として渡すことによって、詳細要素をルート要素に追加します。詳細要素に追加される XML 要素は、フォームの動的な部分に対応します。次のコード行は、このアプリケーションロジックを示しています。

      ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * `Document` オブジェクトの `createElement` メソッドを使用して、要素の名前を表す文字列値を渡すことによって、詳細要素に属する子要素を作成します。戻り値を `Element` にキャストします。次に、`appendChild` メソッドを呼び出して、`Document` オブジェクトの `createTextNode` メソッドを引数として渡すことによって、子要素の値を設定します。子要素の値として表示される文字列値を指定します。最後に、詳細要素の `appendChild` メソッドを呼び出して、子要素オブジェクトを引数として渡すことによって、子要素を詳細要素に追加します。次のコード行は、このアプリケーションロジックを示しています。

      ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * 詳細要素に追加するすべての XML 要素に対して、最後のサブ手順を繰り返します。発注書フォームの入力に使用される XML データソースを適切に作成するには、詳細要素に XML 要素 `txtDescription`、`numQty`、`numUnitPrice` を追加する必要があります。
   * フォームの事前入力に使用されるすべてのデータ項目に対して、最後の 2 つのサブ手順を繰り返します。

1. XML データソースの変換

   * `javax.xml.transform.Transformer` オブジェクトの静的 `newInstance` メソッドを呼び出すことによって、`javax.xml.transform.Transformer` オブジェクトを作成します。
   * `TransformerFactory` オブジェクトの `newTransformer` メソッドを呼び出すことによって、`Transformer` オブジェクトを作成します。
   * コンストラクターを使用して、`ByteArrayOutputStream` オブジェクトを作成します。
   * コンストラクターを使用して手順 1 で作成した `org.w3c.dom.Document` オブジェクトを渡すことによって、`javax.xml.transform.dom.DOMSource` オブジェクトを作成します。
   * コンストラクターを使用して `ByteArrayOutputStream` オブジェクトを渡すことによって、`javax.xml.transform.dom.DOMSource` オブジェクトを作成します。
   * `javax.xml.transform.Transformer` オブジェクトの `transform` メソッドを呼び出して `javax.xml.transform.dom.DOMSource` および `javax.xml.transform.stream.StreamResult` オブジェクトを渡すことによって、Java の `ByteArrayOutputStream` オブジェクトを設定します。
   * バイト配列を作成して、`ByteArrayOutputStream` オブジェクトのサイズをバイト配列に割り当てます。
   * `ByteArrayOutputStream` オブジェクトの `toByteArray` メソッドを呼び出して、バイト配列を設定します。
   * コンストラクターを使用してバイト配列を渡すことによって、`com.adobe.idp.Document` オブジェクトを作成します。

1. 事前入力されたフォームをレンダリング

   `FormsServiceClient` オブジェクトの `renderPDFForm` メソッドを呼び出して、次の値を渡します。

   * ファイル名拡張子を含んだフォームデザイン名を指定する文字列値。
   * フォームに結合するデータを含む `com.adobe.idp.Document` オブジェクト。手順 1 と 2 で作成した `com.adobe.idp.Document` オブジェクトを使用するようにしてください。
   * 実行時オプションを保存する `PDFFormRenderSpec` オブジェクト。
   * Forms サービスで必要な URI 値を格納する `URLSpec` オブジェクト。
   * 添付ファイルを保存する `java.util.HashMap` オブジェクト。オプションのパラメーターです。フォームにファイルを添付しない場合は `null` を指定できます。

   `renderPDFForm` メソッドは、 `FormsResult` クライアントの web ブラウザーに書き込む必要があるフォームデータストリームを含むオブジェクトを返します。

   * フォームデータストリームをクライアントの web ブラウザーに送信するために使用する `javax.servlet.ServletOutputStream` オブジェクトを作成します。
   * `FormsResult` オブジェクトの `getOutputContent` メソッドを呼び出すことによって、`com.adobe.idp.Document` オブジェクトを作成します。
   * `com.adobe.idp.Document` オブジェクトの `getInputStream` メソッドを呼び出すことによって `java.io.InputStream` オブジェクトを作成します。
   * `InputStream` オブジェクトの `read` メソッドを呼び出してバイト配列を引数として渡すことによって、バイト配列を作成し、フォームデータストリームを設定します。
   * `javax.servlet.ServletOutputStream` オブジェクトの `write` メソッドを呼び出して、フォームデータストリームをクライアントの web ブラウザーに送信します。バイト配列を `write` メソッドに渡します。


**関連トピック**

[クイックスタート（SOAP モード）：Java API を使用した、編集可能なレイアウトを含む Forms の事前入力](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用したフォームの事前入力 {#prepopulating-forms-using-the-web-service-api}

Forms API（web サービス）を使用してフォームに編集可能なレイアウトを事前入力するには、次の手順を実行します。

1. プロジェクトファイルを含める

   * Forms サービス WSDL を使用する Java プロキシクラスを作成します。（[Apache Axis を使用した Java プロキシクラスの作成](/help/forms/developing/invoking-aem-forms-using-web.md#creating-java-proxy-classes-using-apache-axis)を参照。）
   * Java プロキシクラスをクラスパスに含めます。

1. メモリ内 XML データソースの作成

   * `DocumentBuilderFactory` クラスの `newInstance` メソッドを呼び出して Java の `DocumentBuilderFactory` オブジェクトを作成します。
   * `DocumentBuilderFactory` オブジェクトの `newDocumentBuilder` メソッドを呼び出して、Java の `DocumentBuilder` オブジェクトを作成します。 
   * `DocumentBuilder` オブジェクトの `newDocument` メソッドを呼び出して、`org.w3c.dom.Document` オブジェクトをインスタンス化します。
   * `org.w3c.dom.Document` オブジェクトの `createElement` メソッドを呼び出して、XML データソースのルート要素を作成します。これにより、ルート要素を表す `Element` オブジェクトが作成されます。要素名を表す文字列値を `createElement` メソッドに渡します。戻り値を `Element` にキャストします。次に、 `Document` オブジェクトの `appendChild` メソッドを呼び出してルート要素オブジェクトを引数として渡し、ルート要素をドキュメントに追加します。次のコード行は、このアプリケーションロジックを示しています。

      ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * `Document` オブジェクトの `createElement` メソッドを呼び出して、XML データソースのヘッダー要素を作成します。要素名を表す文字列値を `createElement` メソッドに渡します。戻り値を `Element` にキャストします。次に、 `root` オブジェクトの `appendChild` メソッドを呼び出してヘッダー要素オブジェクトを引数として渡し、ヘッダー要素をドキュメントに追加します。ヘッダー要素に追加される XML 要素は、フォームの静的な部分に対応します。次のコード行は、このアプリケーションロジックを示しています。

      ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * `Document` オブジェクトの `createElement` メソッドを呼び出して要素名を表す文字列値を渡すことによって、ヘッダー要素に属する子要素を作成します。戻り値を `Element` にキャストします。次に、`appendChild` メソッドを呼び出して、`Document` オブジェクトの `createTextNode` メソッドを引数として渡すことによって、子要素の値を設定します。子要素の値として表示される文字列値を指定します。最後に、子要素をヘッダー要素に追加するには、ヘッダー要素の `appendChild` メソッドを呼び出し、子要素オブジェクトを引数として渡します。次のコード行に、このアプリケーションロジックを示します。

      ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`

   * フォームの静的部分に表示される各フィールドに対して最後のサブステップを繰り返し、残りのすべての要素をヘッダー要素に追加します。（XML データソース図では、これらのフィールドが A のセクションに表示されます。詳しくは、[データのサブグループについて](#understanding-data-subgroups)を参照してください。）
   * `Document` オブジェクトの `createElement` メソッドを呼び出して、XML データソースの詳細要素を作成します。要素の名前を表す文字列値を `createElement` メソッドに渡します。戻り値を `Element` にキャストします。次に、`root` オブジェクトの `appendChild` メソッドを呼び出して、詳細要素オブジェクトを引数として渡すことによって、詳細要素をルート要素に追加します。詳細要素に追加される XML 要素は、フォームの動的な部分に対応します。次のコード行に、このアプリケーションロジックを示します。

      ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * 詳細要素に属する子要素を作成するには、 `Document` オブジェクトの `createElement` メソッドを呼び出して、要素の名前を表す文字列値を渡します。戻り値を `Element` にキャストします。次に、`appendChild` メソッドを呼び出して、`Document` オブジェクトの `createTextNode` メソッドを引数として渡すことによって、子要素の値を設定します。子要素の値として表示される文字列値を指定します。最後に、詳細要素の `appendChild` メソッドを呼び出して子要素を詳細要素に追加することで、子要素オブジェクトを引数として渡します。次のコード行に、このアプリケーションロジックを示します。

      ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * 詳細要素に追加するすべての XML 要素に対して、最後のサブ手順を繰り返します。発注書フォームの入力に使用される XML データソースを適切に作成するには、詳細要素に XML 要素 `txtDescription`、`numQty`、`numUnitPrice` を追加する必要があります。
   * フォームの事前入力に使用されるすべてのデータ項目に対して、最後の 2 つのサブ手順を繰り返します。

1. XML データソースの変換

   * `javax.xml.transform.Transformer` オブジェクトの静的 `newInstance` メソッドを呼び出すことによって、`javax.xml.transform.Transformer` オブジェクトを作成します。
   * `TransformerFactory` オブジェクトの `newTransformer` メソッドを呼び出すことによって、`Transformer` オブジェクトを作成します。
   * コンストラクターを使用して、`ByteArrayOutputStream` オブジェクトを作成します。
   * コンストラクターを使用して手順 1 で作成した `org.w3c.dom.Document` オブジェクトを渡すことによって、`javax.xml.transform.dom.DOMSource` オブジェクトを作成します。
   * コンストラクターを使用して `ByteArrayOutputStream` オブジェクトを渡すことによって、`javax.xml.transform.dom.DOMSource` オブジェクトを作成します。
   * `javax.xml.transform.Transformer` オブジェクトの `transform` メソッドを呼び出して `javax.xml.transform.dom.DOMSource` および `javax.xml.transform.stream.StreamResult` オブジェクトを渡すことによって、Java の `ByteArrayOutputStream` オブジェクトを設定します。
   * バイト配列を作成して、`ByteArrayOutputStream` オブジェクトのサイズをバイト配列に割り当てます。
   * `ByteArrayOutputStream` オブジェクトの `toByteArray` メソッドを呼び出して、バイト配列に入力します。
   * コンストラクターを使用して `BLOB` オブジェクトを作成し、`setBinaryData` メソッドを呼び出して、バイト配列を渡します。

1. 事前入力されたフォームをレンダリング

   `FormsService` オブジェクトの `renderPDFForm` メソッドを呼び出して、次の値を渡します。

   * ファイル名拡張子を含んだフォームデザイン名を指定する文字列値。
   * フォームに結合するデータを含む `BLOB` オブジェクト。手順 1 と 2 で作成した `BLOB` オブジェクトを使用していることを必ず確認してください。
   * 実行時オプションを保存する `PDFFormRenderSpecc` オブジェクト。詳しくは、「[AEM Forms のデータ統合](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ja)」を参照してください。
   * Forms サービスで必要な URI 値を格納する `URLSpec` オブジェクト。
   * 添付ファイルを保存する `java.util.HashMap` オブジェクト。これはオプションのパラメーターで、 フォームにファイルを添付しない場合に、`null`を指定します。
   * メソッドによって設定される空の `com.adobe.idp.services.holders.BLOBHolder` オブジェクト。これは、レンダリングされた PDF フォームを保存するために使用されます。
   * メソッドによって設定される空の `javax.xml.rpc.holders.LongHolder` オブジェクト。（この引数は、フォームのページ数を保存します）。
   * メソッドによって設定される空の `javax.xml.rpc.holders.StringHolder` オブジェクト。（この引数はロケール値を格納します）。
   * この操作の結果を格納する空の `com.adobe.idp.services.holders.FormsResultHolder` オブジェクト。

   `renderPDFForm` メソッドは、最後の引数値で渡される `com.adobe.idp.services.holders.FormsResultHolder` オブジェクトに、クライアント Web ブラウザーに書き込む必要のあるフォームデータストリームを設定します。

   *  `com.adobe.idp.services.holders.FormsResultHolder` オブジェクトの `value` データメンバーの値を取得して `FormResult` オブジェクトを作成します。
   * `FormsResult` オブジェクトの `getOutputContent` メソッドを呼び出して、フォームデータを含む `BLOB` オブジェクトを作成します。
   * `getContentType` メソッドを呼び出して、`BLOB` オブジェクトのコンテンツタイプを取得します。
   * `javax.servlet.http.HttpServletResponse` オブジェクトのコンテンツタイプを設定するには、`setContentType` メソッドを呼び出して、`BLOB` オブジェクトのコンテンツタイプを渡します。
   * `javax.servlet.http.HttpServletResponse` オブジェクトの `getOutputStream` メソッドを呼び出して、フォームデータストリームをクライアント web ブラウザーに書き込むために使用される `javax.servlet.ServletOutputStream` オブジェクトを作成します。
   * バイト配列を作成し、`BLOB` オブジェクトの `getBinaryData` メソッドを呼び出して入力します。このタスクは、`FormsResult` オブジェクトのコンテンツをバイト配列に割り当てます。
   * `javax.servlet.http.HttpServletResponse` オブジェクトの `write` メソッドを呼び出して、フォームデータストリームをクライアント web ブラウザーに送信します。バイト配列を `write` メソッドに渡します。

   >[!NOTE]
   >
   >`renderPDFForm` メソッドによって、最後の引数値として渡される `com.adobe.idp.services.holders.FormsResultHolder` オブジェクトに、クライアント web ブラウザーに書き込む必要があるフォームデータストリームが入力されます。

**関連トピック**

[Base64 エンコーディングを使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
