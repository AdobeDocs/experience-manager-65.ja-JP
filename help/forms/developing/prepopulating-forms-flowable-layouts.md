---
title: 編集可能なレイアウトを使用したFormsの事前入力
seo-title: 編集可能なレイアウトを使用したFormsの事前入力
description: Java APIとWebサービスAPIを使用して、レンダリングされたフォーム内のユーザーにデータを表示するための、編集可能なレイアウトをフォームに事前入力します。
seo-description: Java APIとWebサービスAPIを使用して、レンダリングされたフォーム内のユーザーにデータを表示するための、編集可能なレイアウトをフォームに事前入力します。
uuid: 93ccb496-e1c2-4b79-8e89-7a2abfce1537
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 30a12fc6-07b8-4c7c-b9e2-caa2bec0ac48
role: Developer
exl-id: ff087084-fb1c-43a4-ae54-cc77eb862493
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '3533'
ht-degree: 4%

---

# Formsへの編集可能なレイアウトの事前入力{#prepopulating-forms-with-flowable-layouts1}

## Formsへの編集可能なレイアウトの事前入力{#prepopulating-forms-with-flowable-layouts2}

フォームの自動埋め込みは、レンダリングされたフォーム内のユーザーにデータを表示します。 例えば、ユーザーがユーザー名とパスワードを使用してWebサイトにログインしたとします。 認証が成功した場合、クライアントアプリケーションはデータベースに対してユーザー情報を照会します。 データがフォームにマージされ、フォームがユーザーにレンダリングされます。 その結果、ユーザーはフォーム内のパーソナライズされたデータを表示できます。

フォームの自動埋め込みには次の利点があります。

* ユーザーがフォーム内にカスタムデータを表示できる.
* ユーザーがフォームに入力する際に入力する時間を減らします。
* データを配置する場所を制御できるため、データの整合性を維持できる.

次の2つのXMLデータソースを使用して、フォームを事前入力できます。

* XDPデータソース。XFA構文に準拠するXMLです(または、Acrobatを使用して作成されたフォームの事前入力用のXFDFデータ)。
* フォームのフィールド名に一致する名前と値のペアを含む、任意のXMLデータソース（この節の例では、任意のXMLデータソースを使用します）。

事前入力するフォームフィールドごとに、XML要素が存在する必要があります。 XML要素名は、フィールド名と一致する必要があります。 XML要素がフォームフィールドに対応していない場合や、XML要素名がフィールド名と一致しない場合は無視されます。 すべてのXML要素が指定されている限り、XML要素の表示順を一致させる必要はありません。

既にデータを含むフォームを事前入力する場合は、XMLデータソース内に既に表示されているデータを指定する必要があります。 10個のフィールドを含むフォームに4つのフィールドのデータがあるとします。 次に、残りの6つのフィールドに事前入力するとします。 この場合、フォームの事前入力に使用するXMLデータソースに10個のXML要素を指定する必要があります。 6つの要素のみを指定した場合、元の4つのフィールドは空になります。

例えば、サンプルの確認フォームなどのフォームを事前入力できます。 ([インタラクティブPDF formsのレンダリング](/help/forms/developing/rendering-interactive-pdf-forms.md)の「確認フォーム」を参照)。

サンプルの確認フォームを事前入力するには、フォーム内の3つのフィールドに一致する3つのXML要素を含むXMLデータソースを作成する必要があります。 このフォームには、次の3つのフィールドが含まれています。`FirstName`、`LastName`、および`Amount`。 最初の手順は、フォームデザイン内のフィールドと一致するXML要素を含むXMLデータソースを作成することです。 次の手順では、次のXMLコードに示すように、XML要素にデータ値を割り当てます。

```xml
     <Untitled>
         <FirstName>Jerry</FirstName>
         <LastName>Johnson</LastName>
         <Amount>250000</Amount>
     </Untitled>
```

次の図に示すように、確認フォームにこのXMLデータソースを事前入力し、フォームをレンダリングすると、XML要素に割り当てたデータ値が表示されます。

![pf_pf_confirmxml3](assets/pf_pf_confirmxml3.png)

### 編集可能なレイアウトを使用したフォームの事前入力{#prepopulating_forms_with_flowable_layouts-1}

編集可能なレイアウトのFormsは、ユーザーに不明な量のデータを表示する場合に役立ちます。 フォームのレイアウトはマージされるデータ量に合わせて自動的に調整されるので、固定レイアウトのフォームと同様に、フォームの固定レイアウトやページ数を事前に決定する必要はありません。

通常、フォームには実行時に取得されるデータが入力されます。 その結果、メモリ内XMLデータソースを作成し、そのデータをメモリ内XMLデータソースに直接配置することで、フォームの事前入力を行うことができます。

オンラインストアなどのWebベースのアプリケーションを検討します。 オンライン買い物客が品目の購入を終了すると、購入したすべての品目が、フォームの事前入力に使用されるメモリ内XMLデータソースに配置されます。 次の図に、このプロセスを示します。このプロセスについて、図の後の表で説明します。

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
   <td><p>ユーザーが品目の購入を完了し、「送信」ボタンをクリックすると、メモリ内XMLデータソースが作成されます。 購入した品目とユーザー情報は、メモリ内XMLデータソースに配置されます。 </p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>XMLデータソースは、発注書フォームの事前入力に使用されます（このフォームの例を次の表に示します）。 </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>発注書フォームがクライアントのWebブラウザーにレンダリングされます。 </p></td>
  </tr>
 </tbody>
</table>

次の図に、発注書フォームの例を示します。 テーブル内の情報は、XMLデータ内のレコード数に合わせて調整できます。

![pf_pf_poform](assets/pf_pf_poform.png)

>[!NOTE]
>
>フォームには、エンタープライズデータベースや外部アプリケーションなど、他のソースのデータを事前入力することができます。

### フォームデザインに関する考慮事項{#form-design-considerations}

編集可能なレイアウトを含むFormsは、Designerで作成されたフォームデザインに基づいています。 フォームデザインでは、ユーザーの入力に基づく値の計算を含む、レイアウト、プレゼンテーション、データ取得ルールのセットを指定します。 ルールは、データがフォームに入力されると適用されます。 フォームに追加されるフィールドは、フォームデザイン内のサブフォームです。 例えば、前の図に示す発注書フォームでは、各行がサブフォームです。 サブフォームを含むフォームデザインの作成について詳しくは、[編集可能なレイアウトの発注書フォームの作成](https://www.adobe.com/go/learn_aemforms_qs_poformflowable_9)を参照してください。

### データのサブグループ{#understanding-data-subgroups}について

固定レイアウトと編集可能なレイアウトを使用してフォームに事前入力するには、XMLデータソースを使用します。 ただし、フォームに編集可能なレイアウトを自動埋め込むXMLデータソースには、フォーム内で繰り返されるサブフォームの自動埋め込みに使用される繰り返しXML要素が含まれている点が異なります。 これらの繰り返しXML要素は、データサブグループと呼ばれます。

前の図に示す発注書フォームの事前入力に使用するXMLデータソースには、4つの繰り返しデータサブグループが含まれています。 各データサブグループは、購入した品目に対応します。 購入した商品は、モニター、卓上ランプ、電話、アドレス帳です。

次のXMLデータソースは、発注書フォームの事前入力に使用されます。

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

各データサブグループには、この情報に対応する4つのXML要素が含まれています。

* 品目の部品番号
* 項目の説明
* 品目数
* 単価

データサブグループの親XML要素の名前は、フォームデザイン内のサブフォームの名前と一致する必要があります。 例えば、前の図では、データサブグループの親XML要素の名前が`detail`であることに注意してください。 これは、発注書フォームの基となるフォームデザインにあるサブフォームの名前に対応します。 データサブグループの親XML要素の名前とサブフォームの名前が一致しない場合、サーバー側のフォームは事前入力されません。

各データサブグループには、サブフォーム内のフィールド名に一致するXML要素が含まれている必要があります。 フォームデザイン内の`detail`サブフォームには、次のフィールドが含まれます。

* txtPartNum
* txtDescription
* numQty
* numUnitPrice

>[!NOTE]
>
>繰り返しXML要素を含むデータソースを使用してフォームに事前入力しようとし、`RenderAtClient`オプションを`No`に設定した場合、最初のデータレコードのみがフォームにマージされます。 すべてのデータレコードが確実にフォームにマージされるようにするには、`RenderAtClient`を`Yes`に設定します。 `RenderAtClient`オプションについて詳しくは、[クライアントでのFormsのレンダリング](/help/forms/developing/rendering-forms-client.md)を参照してください。

>[!NOTE]
>
>Formsサービスについて詳しくは、『 AEM Formsのサービスリファレンス[ 』を参照してください。](https://www.adobe.com/go/learn_aemforms_services_63)

### 手順の概要{#summary-of-steps}

編集可能なレイアウトをフォームに事前入力するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. メモリ内XMLデータソースを作成します。
1. XMLデータソースを変換します。
1. 事前入力されたフォームをレンダリングする。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用する場合は、プロキシファイルを必ず含めてください。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用する場合は、プロキシファイルを必ず含めてください。

**メモリ内XMLデータソースの作成**

`org.w3c.dom`クラスを使用して、メモリ内XMLデータソースを作成し、編集可能なレイアウトでフォームに事前入力することができます。 フォームに準拠するXMLデータソースにデータを配置する必要があります。 編集可能なレイアウトを含むフォームとXMLデータソースとの関係については、[データのサブグループ](#understanding-data-subgroups)についてを参照してください。

**XMLデータソースの変換**

`org.w3c.dom`クラスを使用して作成されたメモリ内XMLデータソースは、フォームの事前入力に使用する前に、 `com.adobe.idp.Document`オブジェクトに変換できます。 Java XML変換クラスを使用して、メモリ内XMLデータソースを変換できます。

>[!NOTE]
>
>FormsサービスのWSDLを使用してフォームの事前入力を行う場合は、`org.w3c.dom.Document`オブジェクトを`BLOB`オブジェクトに変換する必要があります。

**事前入力されたフォームのレンダリング**

事前入力されたフォームは、他のフォームと同様にレンダリングします。 唯一の違いは、XMLデータソースを含む`com.adobe.idp.Document`オブジェクトを使用してフォームに事前入力する点です。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[FormsサービスAPIのクイックスタート](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[インタラクティブPDF formsのレンダリング](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Java API {#prepopulating-forms-using-the-java-api}を使用したフォームの事前入力

Forms API(Java)を使用してフォームに編集可能なレイアウトを事前入力するには、次の手順を実行します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-forms-client.jarなどのクライアントJARファイルを含めます。 これらのファイルの場所については、[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。

1. メモリ内XMLデータソースの作成

   * `DocumentBuilderFactory`クラス` `newInstance`メソッドを呼び出して、Java `DocumentBuilderFactory`オブジェクトを作成します。
   * `DocumentBuilderFactory`オブジェクトの`newDocumentBuilder`メソッドを呼び出して、Java `DocumentBuilder`オブジェクトを作成します。
   * `DocumentBuilder`オブジェクトの`newDocument`メソッドを呼び出して、`org.w3c.dom.Document`オブジェクトをインスタンス化します。
   * `org.w3c.dom.Document`オブジェクトの`createElement`メソッドを呼び出して、XMLデータソースのルート要素を作成します。 これにより、ルート要素を表す`Element`オブジェクトが作成されます。 要素の名前を表す文字列値を`createElement`メソッドに渡します。 戻り値を `Element` にキャストします。次に、`Document`オブジェクトの`appendChild`メソッドを呼び出してルート要素をドキュメントに追加し、ルート要素オブジェクトを引数として渡します。 次のコード行に、このアプリケーションロジックを示します。

      ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * `Document`オブジェクトの`createElement`メソッドを呼び出して、XMLデータソースのヘッダー要素を作成します。 要素の名前を表す文字列値を`createElement`メソッドに渡します。 戻り値を `Element` にキャストします。次に、`root`オブジェクトの`appendChild`メソッドを呼び出してヘッダー要素をルート要素に追加し、ヘッダー要素オブジェクトを引数として渡します。 ヘッダー要素に追加されるXML要素は、フォームの静的な部分に対応します。 次のコード行に、このアプリケーションロジックを示します。

      ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * `Document`オブジェクトの`createElement`メソッドを呼び出してヘッダー要素に属する子要素を作成し、要素の名前を表す文字列値を渡します。 戻り値を `Element` にキャストします。次に、 `appendChild`メソッドを呼び出して子要素の値を設定し、 `Document`オブジェクトの`createTextNode`メソッドを引数として渡します。 子要素の値として表示される文字列値を指定します。 最後に、ヘッダー要素の`appendChild`メソッドを呼び出して子要素をヘッダー要素に追加し、子要素オブジェクトを引数として渡します。 次のコード行に、このアプリケーションロジックを示します。

      ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`


   * フォームの静的部分に表示される各フィールドの最後のサブステップを繰り返して、残りの要素をヘッダー要素に追加します(XMLデータソース図では、これらのフィールドがAの節に表示されます（[データのサブグループ](#understanding-data-subgroups)の理解を参照）。
   * `Document`オブジェクトの`createElement`メソッドを呼び出して、XMLデータソースの詳細要素を作成します。 要素の名前を表す文字列値を`createElement`メソッドに渡します。 戻り値を `Element` にキャストします。次に、`root`オブジェクトの`appendChild`メソッドを呼び出してルート要素にdetail要素を追加し、引数としてdetail要素オブジェクトを渡します。 詳細要素に追加されるXML要素は、フォームの動的な部分に対応します。 次のコード行に、このアプリケーションロジックを示します。

      ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * `Document`オブジェクトの`createElement`メソッドを呼び出して詳細要素に属する子要素を作成し、要素の名前を表す文字列値を渡します。 戻り値を `Element` にキャストします。次に、 `appendChild`メソッドを呼び出して子要素の値を設定し、 `Document`オブジェクトの`createTextNode`メソッドを引数として渡します。 子要素の値として表示される文字列値を指定します。 最後に、detail要素の`appendChild`メソッドを呼び出して子要素をdetail要素に追加し、子要素オブジェクトを引数として渡します。 次のコード行に、このアプリケーションロジックを示します。

      ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * 詳細要素に追加するすべてのXML要素に対して、最後のサブ手順を繰り返します。 発注書フォームへの入力に使用するXMLデータソースを適切に作成するには、次のXML要素を詳細要素に追加する必要があります。`txtDescription`、`numQty`、および`numUnitPrice`。
   * フォームの事前入力に使用されるすべてのデータ項目に対して、最後の2つのサブ手順を繰り返します。

1. XMLデータソースの変換

   * `javax.xml.transform.Transformer`オブジェクトの静的な`newInstance`メソッドを呼び出して、`javax.xml.transform.Transformer`オブジェクトを作成します。
   * `TransformerFactory`オブジェクトの`newTransformer`メソッドを呼び出して、`Transformer`オブジェクトを作成します。
   * コンストラクタを使用して `ByteArrayOutputStream` オブジェクトを作成します。
   * コンストラクターを使用し、手順1で作成した`org.w3c.dom.Document`オブジェクトを渡して、`javax.xml.transform.dom.DOMSource`オブジェクトを作成します。
   * コンストラクタを使用して `javax.xml.transform.dom.DOMSource` オブジェクトを渡すことによって、`ByteArrayOutputStream` オブジェクトを作成します。
   * `javax.xml.transform.Transformer`オブジェクトの`transform`メソッドを呼び出し、`javax.xml.transform.dom.DOMSource`および`javax.xml.transform.stream.StreamResult`オブジェクトを渡すことで、Java `ByteArrayOutputStream`オブジェクトを設定します。
   * バイト配列を作成し、`ByteArrayOutputStream`オブジェクトのサイズをバイト配列に割り当てます。
   * `ByteArrayOutputStream`オブジェクトの`toByteArray`メソッドを呼び出して、バイト配列を設定します。
   * コンストラクターを使用してバイト配列を渡し、`com.adobe.idp.Document`オブジェクトを作成します。

1. 事前入力されたフォームのレンダリング

   `FormsServiceClient`オブジェクトの`renderPDFForm`メソッドを呼び出し、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定するstring値。
   * フォームとマージするデータを含む`com.adobe.idp.Document`オブジェクト。 必ず、手順1と2で作成した`com.adobe.idp.Document`オブジェクトを使用します。
   * 実行時オプションを格納する`PDFFormRenderSpec`オブジェクト。
   * Formsサービスに必要なURI値を含む`URLSpec`オブジェクト。
   * 添付ファイルを格納する`java.util.HashMap`オブジェクト。 これはオプションのパラメーターで、フォームにファイルを添付しない場合は`null`を指定できます。

   `renderPDFForm`メソッドは、クライアントのWebブラウザーに書き込む必要があるフォームデータストリームを含む`FormsResult`オブジェクトを返します。

   * フォームデータストリームをクライアントのWebブラウザーに送信するために使用する`javax.servlet.ServletOutputStream`オブジェクトを作成します。
   * `FormsResult`オブジェクトの`getOutputContent`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトを作成します。
   * `com.adobe.idp.Document`オブジェクトの`getInputStream`メソッドを呼び出して、`java.io.InputStream`オブジェクトを作成します。
   * `InputStream`オブジェクトの`read`メソッドを呼び出し、バイト配列を引数として渡すことで、バイト配列にフォームデータストリームを入力します。
   * `javax.servlet.ServletOutputStream`オブジェクトの`write`メソッドを呼び出して、フォームデータストリームをクライアントWebブラウザーに送信します。 `write`メソッドにバイト配列を渡します。


**関連トピック**

[クイックスタート（SOAPモード）:Java APIを使用した、Formsへの編集可能なレイアウトの事前入力](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#prepopulating-forms-using-the-web-service-api}を使用したフォームの事前入力

Forms API（Webサービス）を使用してフォームに編集可能なレイアウトを事前入力するには、次の手順を実行します。

1. プロジェクトファイルを含める

   * FormsサービスのWSDLを使用するJavaプロキシクラスを作成します。 （[Apache Axis](/help/forms/developing/invoking-aem-forms-using-web.md#creating-java-proxy-classes-using-apache-axis)を使用したJavaプロキシクラスの作成を参照）。
   * Javaプロキシクラスをクラスパスに含めます。

1. メモリ内XMLデータソースの作成

   * `DocumentBuilderFactory`クラス` `newInstance`メソッドを呼び出して、Java `DocumentBuilderFactory`オブジェクトを作成します。
   * `DocumentBuilderFactory`オブジェクトの`newDocumentBuilder`メソッドを呼び出して、Java `DocumentBuilder`オブジェクトを作成します。
   * `DocumentBuilder`オブジェクトの`newDocument`メソッドを呼び出して、`org.w3c.dom.Document`オブジェクトをインスタンス化します。
   * `org.w3c.dom.Document`オブジェクトの`createElement`メソッドを呼び出して、XMLデータソースのルート要素を作成します。 これにより、ルート要素を表す`Element`オブジェクトが作成されます。 要素の名前を表す文字列値を`createElement`メソッドに渡します。 戻り値を `Element` にキャストします。次に、`Document`オブジェクトの`appendChild`メソッドを呼び出してルート要素をドキュメントに追加し、ルート要素オブジェクトを引数として渡します。 次のコード行に、このアプリケーションロジックを示します。

      ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * `Document`オブジェクトの`createElement`メソッドを呼び出して、XMLデータソースのヘッダー要素を作成します。 要素の名前を表す文字列値を`createElement`メソッドに渡します。 戻り値を `Element` にキャストします。次に、`root`オブジェクトの`appendChild`メソッドを呼び出してヘッダー要素をルート要素に追加し、ヘッダー要素オブジェクトを引数として渡します。 ヘッダー要素に追加されるXML要素は、フォームの静的な部分に対応します。 次のコード行に、このアプリケーションロジックを示します。

      ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * `Document`オブジェクトの`createElement`メソッドを呼び出してヘッダー要素に属する子要素を作成し、要素の名前を表す文字列値を渡します。 戻り値を `Element` にキャストします。次に、 `appendChild`メソッドを呼び出して子要素の値を設定し、 `Document`オブジェクトの`createTextNode`メソッドを引数として渡します。 子要素の値として表示される文字列値を指定します。 最後に、ヘッダー要素の`appendChild`メソッドを呼び出して子要素をヘッダー要素に追加し、子要素オブジェクトを引数として渡します。 次のコード行に、このアプリケーションロジックを示します。

      ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`

   * フォームの静的部分に表示される各フィールドの最後のサブステップを繰り返して、残りの要素をヘッダー要素に追加します(XMLデータソース図では、これらのフィールドがAの節に表示されます（[データのサブグループ](#understanding-data-subgroups)の理解を参照）。
   * `Document`オブジェクトの`createElement`メソッドを呼び出して、XMLデータソースの詳細要素を作成します。 要素の名前を表す文字列値を`createElement`メソッドに渡します。 戻り値を `Element` にキャストします。次に、`root`オブジェクトの`appendChild`メソッドを呼び出してルート要素にdetail要素を追加し、引数としてdetail要素オブジェクトを渡します。 詳細要素に追加されるXML要素は、フォームの動的な部分に対応します。 次のコード行に、このアプリケーションロジックを示します。

      ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * `Document`オブジェクトの`createElement`メソッドを呼び出して詳細要素に属する子要素を作成し、要素の名前を表す文字列値を渡します。 戻り値を `Element` にキャストします。次に、 `appendChild`メソッドを呼び出して子要素の値を設定し、 `Document`オブジェクトの`createTextNode`メソッドを引数として渡します。 子要素の値として表示される文字列値を指定します。 最後に、detail要素の`appendChild`メソッドを呼び出して子要素をdetail要素に追加し、子要素オブジェクトを引数として渡します。 次のコード行に、このアプリケーションロジックを示します。

      ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * 詳細要素に追加するすべてのXML要素に対して、最後のサブ手順を繰り返します。 発注書フォームへの入力に使用するXMLデータソースを適切に作成するには、次のXML要素を詳細要素に追加する必要があります。`txtDescription`、`numQty`、および`numUnitPrice`。
   * フォームの事前入力に使用されるすべてのデータ項目に対して、最後の2つのサブ手順を繰り返します。

1. XMLデータソースの変換

   * `javax.xml.transform.Transformer`オブジェクトの静的な`newInstance`メソッドを呼び出して、`javax.xml.transform.Transformer`オブジェクトを作成します。
   * `TransformerFactory`オブジェクトの`newTransformer`メソッドを呼び出して、`Transformer`オブジェクトを作成します。
   * コンストラクタを使用して `ByteArrayOutputStream` オブジェクトを作成します。
   * コンストラクターを使用し、手順1で作成した`org.w3c.dom.Document`オブジェクトを渡して、`javax.xml.transform.dom.DOMSource`オブジェクトを作成します。
   * コンストラクタを使用して `javax.xml.transform.dom.DOMSource` オブジェクトを渡すことによって、`ByteArrayOutputStream` オブジェクトを作成します。
   * `javax.xml.transform.Transformer`オブジェクトの`transform`メソッドを呼び出し、`javax.xml.transform.dom.DOMSource`および`javax.xml.transform.stream.StreamResult`オブジェクトを渡すことで、Java `ByteArrayOutputStream`オブジェクトを設定します。
   * バイト配列を作成し、`ByteArrayOutputStream`オブジェクトのサイズをバイト配列に割り当てます。
   * `ByteArrayOutputStream`オブジェクトの`toByteArray`メソッドを呼び出して、バイト配列を設定します。
   * コンストラクターを使用して`BLOB`オブジェクトを作成し、`setBinaryData`メソッドを呼び出してバイト配列を渡します。

1. 事前入力されたフォームのレンダリング

   `FormsService`オブジェクトの`renderPDFForm`メソッドを呼び出し、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定するstring値。
   * フォームとマージするデータを含む`BLOB`オブジェクト。 必ず、手順1と2で作成した`BLOB`オブジェクトを使用します。
   * 実行時オプションを格納する`PDFFormRenderSpecc`オブジェクト。 詳しくは、「[AEM Forms APIリファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)」を参照してください。
   * Formsサービスに必要なURI値を含む`URLSpec`オブジェクト。
   * 添付ファイルを格納する`java.util.HashMap`オブジェクト。 これはオプションのパラメーターで、フォームにファイルを添付しない場合は`null`を指定できます。
   * メソッドで設定される空の`com.adobe.idp.services.holders.BLOBHolder`オブジェクト。 これは、レンダリングされたPDFフォームを保存するために使用されます。
   * メソッドで設定される空の`javax.xml.rpc.holders.LongHolder`オブジェクト。 （この引数は、フォームのページ数を保存します）。
   * メソッドで設定される空の`javax.xml.rpc.holders.StringHolder`オブジェクト。 （この引数はロケール値を格納します）。
   * この操作の結果を格納する空の`com.adobe.idp.services.holders.FormsResultHolder`オブジェクト。

   `renderPDFForm`メソッドは、最後の引数値として渡される`com.adobe.idp.services.holders.FormsResultHolder`オブジェクトに、クライアントWebブラウザーに書き込む必要のあるフォームデータストリームを設定します。

   * `com.adobe.idp.services.holders.FormsResultHolder`オブジェクトの`value`データメンバーの値を取得して、`FormResult`オブジェクトを作成します。
   * `FormsResult`オブジェクトの`getOutputContent`メソッドを呼び出して、フォームデータを含む`BLOB`オブジェクトを作成します。
   * `getContentType`メソッドを呼び出して、`BLOB`オブジェクトのコンテンツタイプを取得します。
   * `setContentType`メソッドを呼び出し、`BLOB`オブジェクトのコンテンツタイプを渡すことで、`javax.servlet.http.HttpServletResponse`オブジェクトのコンテンツタイプを設定します。
   * `javax.servlet.http.HttpServletResponse`オブジェクトの`getOutputStream`メソッドを呼び出して、フォームデータストリームをクライアントWebブラウザーに書き込むための`javax.servlet.ServletOutputStream`オブジェクトを作成します。
   * バイト配列を作成し、`BLOB`オブジェクトの`getBinaryData`メソッドを呼び出してそれを設定します。 このタスクは、`FormsResult`オブジェクトの内容をバイト配列に割り当てます。
   * `javax.servlet.http.HttpServletResponse`オブジェクトの`write`メソッドを呼び出して、フォームデータストリームをクライアントWebブラウザーに送信します。 `write`メソッドにバイト配列を渡します。

   >[!NOTE]
   >
   >`renderPDFForm`メソッドは、最後の引数値として渡される`com.adobe.idp.services.holders.FormsResultHolder`オブジェクトに、クライアントWebブラウザーに書き込む必要のあるフォームデータストリームを設定します。

**関連トピック**

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
