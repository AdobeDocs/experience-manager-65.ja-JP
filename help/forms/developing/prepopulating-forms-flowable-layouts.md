---
title: 編集可能なレイアウトをFormsに自動埋め込み
seo-title: 編集可能なレイアウトをFormsに自動埋め込み
description: Java APIとWeb Service APIを使用してレンダリングされたフォーム内のユーザーにデータを表示するための、編集可能なレイアウトでフォームを事前入力します。
seo-description: Java APIとWeb Service APIを使用してレンダリングされたフォーム内のユーザーにデータを表示するための、編集可能なレイアウトでフォームを事前入力します。
uuid: 93ccb496-e1c2-4b79-8e89-7a2abfce1537
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 30a12fc6-07b8-4c7c-b9e2-caa2bec0ac48
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '3533'
ht-degree: 4%

---


# 編集可能なレイアウトをFormsに自動埋め込み{#prepopulating-forms-with-flowable-layouts1}

## 編集可能なレイアウトをFormsに自動埋め込み{#prepopulating-forms-with-flowable-layouts2}

フォームの自動埋め込みは、レンダリングされたフォーム内のユーザーにデータを表示します。 例えば、あるユーザーがユーザー名とパスワードを使用してWebサイトにログインしたとします。 認証に成功した場合、クライアントアプリケーションはユーザ情報のデータベースをクエリします。 データがフォームにマージされた後、フォームがユーザーにレンダリングされます。 その結果、ユーザーはフォーム内でパーソナライズされたデータを表示できます。

フォームの自動埋め込みには、次の利点があります。

* ユーザーがフォーム内にカスタムデータを表示できる.
* ユーザーがフォームに入力する手間を軽減します。
* データを配置する場所を制御できるため、データの整合性を維持できる.

次の2つのXMLデータソースで、フォームの自動埋め込みを行うことができます。

* XDPデータソース。XFA構文(Acrobatを使用して作成されたフォームの自動埋め込みに使用するXFDFデータ)に準拠するXMLです。
* フォームのフィールド名と一致する名前と値のペアを含む、任意のXMLデータソース（この節の例では、任意のXMLデータソースを使用します）。

自動埋め込みを行うすべてのフォームフィールドに、XML要素が存在する必要があります。 XML要素名は、フィールド名と一致する必要があります。 XML要素がフォームフィールドに対応していない場合、またはXML要素名がフィールド名と一致しない場合、XML要素は無視されます。 すべてのXML要素が指定されている限り、XML要素が表示される順序と一致させる必要はありません。

既にデータを含むフォームを事前入力する場合は、XMLデータソース内に既に表示されているデータを指定する必要があります。 10個のフィールドを含むフォームが4つのフィールドにデータを含むとします。 次に、残りの6つのフィールドに事前入力するとします。 この場合、フォームの自動埋め込みに使用する10個のXML要素をXMLデータソースに指定する必要があります。 6つの要素のみを指定した場合、元の4つのフィールドは空になります。

例えば、サンプルの確認フォームなどのフォームを自動埋め込むことができます。 ([インタラクティブPDF formsのレンダリング](/help/forms/developing/rendering-interactive-pdf-forms.md)の「確認フォーム」を参照)。

サンプルの確認フォームを自動埋め込むには、フォーム内の3つのフィールドに一致する3つのXML要素を含むXMLデータソースを作成する必要があります。 このフォームには次の3つのフィールドが含まれています。`FirstName`、`LastName`、`Amount`。 最初の手順は、フォームデザイン内のフィールドと一致するXML要素を含むXMLデータソースを作成することです。 次の手順は、次のXMLコードに示すように、XML要素にデータ値を割り当てることです。

```xml
     <Untitled>
         <FirstName>Jerry</FirstName>
         <LastName>Johnson</LastName>
         <Amount>250000</Amount>
     </Untitled>
```

次の図に示すように、このXMLデータソースを使用して確認フォームに事前入力し、フォームをレンダリングすると、XML要素に割り当てたデータ値が表示されます。

![pf_pf_confirmxml3](assets/pf_pf_confirmxml3.png)

### 編集可能なレイアウトでフォームに自動埋め込み{#prepopulating_forms_with_flowable_layouts-1}

編集可能なレイアウトを含むFormsは、不明な量のデータをユーザーに表示する場合に便利です。 フォームのレイアウトはマージされるデータ量に合わせて自動的に調整されるので、固定レイアウトのフォームとは異なり、固定レイアウトやフォームのページ数を事前に決める必要はありません。

通常、フォームには実行時に取得されるデータが入力されます。 その結果、メモリ内XMLデータソースを作成し、そのデータをメモリ内XMLデータソースに直接配置することで、フォームの自動埋め込みを行うことができます。

オンラインストアなど、Webベースのアプリケーションを考えてみます。 オンライン買い物客が購入アイテムの購入を終了すると、購入したすべてのアイテムが、フォームの自動埋め込みに使用されるメモリ内XMLデータソースに配置されます。 次の図に、このプロセスを示します。このプロセスについて、次の図の下の表で説明します。

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
   <td><p>ユーザは、ウェブベースのオンラインストアから商品を購入する。 </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>ユーザーが購入アイテムの購入を完了し、「Submit」ボタンをクリックすると、メモリ内XMLデータソースが作成されます。 購入したアイテムとユーザー情報は、メモリ内XMLデータソースに配置されます。 </p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>XMLデータソースは、発注書フォームの自動埋め込みに使用されます（次の表にこのフォームの例を示します）。 </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>発注書フォームがクライアントのWebブラウザーにレンダリングされます。 </p></td>
  </tr>
 </tbody>
</table>

次の図に、発注書フォームの例を示します。 表の情報は、XMLデータのレコード数に合わせて調整できます。

![pf_pf_poform](assets/pf_pf_poform.png)

>[!NOTE]
>
>フォームには、エンタープライズデータベースや外部アプリケーションなど、他のソースのデータを事前入力することができます。

### フォームデザインの考慮事項{#form-design-considerations}

編集可能なレイアウトを含むFormsは、Designerで作成されたフォームデザインに基づいています。 フォームデザインでは、ユーザー入力に基づく値の計算を含む、レイアウト、プレゼンテーションおよびデータ取得ルールのセットを指定します。 ルールは、データがフォームに入力されるときに適用されます。 フォームに追加されるフィールドは、フォームデザイン内のサブフォームです。 例えば、前の図に示す発注書フォームでは、各行がサブフォームです。 サブフォームを含むフォームデザインの作成について詳しくは、[編集可能なレイアウトを含む発注書フォームの作成](https://www.adobe.com/go/learn_aemforms_qs_poformflowable_9)を参照してください。

### データサブグループ{#understanding-data-subgroups}について

XMLデータソースは、フォームに固定レイアウトと編集可能なレイアウトを事前入力するために使用します。 ただし、編集可能なレイアウトでフォームを自動埋め込むXMLデータソースには、フォーム内で繰り返されるサブフォームの自動埋め込みに使用される繰り返しXML要素が含まれています。 これらの繰り返しXML要素は、データサブグループと呼ばれます。

前の図に示す発注書フォームの自動埋め込みに使用されるXMLデータソースには、4つの繰り返しデータサブグループが含まれています。 各データサブグループは購入した品目に対応しています。 購入したアイテムは、モニタ、卓上ランプ、電話、アドレス帳です。

次のXMLデータソースを使用して、発注書フォームの自動埋め込みを行います。

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

各データサブグループには、次の情報に対応する4つのXML要素が含まれています。

* 項目のパーツ番号
* 項目の説明
* 品目数量
* 単価

データサブグループの親XML要素の名前は、フォームデザイン内のサブフォームの名前と一致する必要があります。 例えば、前の図では、データサブグループの親XML要素の名前が`detail`であることに注意してください。 これは、発注書フォームの基となるフォームデザイン内のサブフォームの名前に対応します。 データサブグループの親XML要素の名前とサブフォームが一致しない場合、サーバー側のフォームは事前入力されません。

各データサブグループには、サブフォーム内のフィールド名と一致するXML要素が含まれている必要があります。 フォームデザイン内の`detail`サブフォームには、次のフィールドが含まれています。

* txtPartNum
* txtDescription
* numQty
* numUnitPrice

>[!NOTE]
>
>繰り返しXML要素を含むデータソースを使用してフォームに自動埋め込みを試み、`RenderAtClient`オプションを`No`に設定した場合、最初のデータレコードだけがフォームにマージされます。 すべてのデータレコードを確実にフォームに結合するには、`RenderAtClient`を`Yes`に設定します。 `RenderAtClient`オプションについて詳しくは、[クライアントでのFormsのレンダリング](/help/forms/developing/rendering-forms-client.md)を参照してください。

>[!NOTE]
>
>Formsサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順{#summary-of-steps}の概要

編集可能なレイアウトをフォームに自動埋め込むには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. メモリ内XMLデータソースを作成します。
1. XMLデータソースを変換します。
1. 事前入力されたフォームをレンダリングします。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めてください。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めてください。

**メモリ内XMLデータソースの作成**

`org.w3c.dom`クラスを使用してメモリ内XMLデータソースを作成し、編集可能なレイアウトでフォームに自動埋め込みを行うことができます。 フォームに適合するXMLデータソースにデータを配置する必要があります。 編集可能なレイアウトを含むフォームとXMLデータソースとの関係について詳しくは、[データサブグループ](#understanding-data-subgroups)についてを参照してください。

**XMLデータソースの変換**

`org.w3c.dom`クラスを使用して作成されたメモリ内XMLデータソースは、フォームの自動埋め込みに使用する前に、`com.adobe.idp.Document`オブジェクトに変換できます。 メモリ内XMLデータソースは、Java XML変換クラスを使用して変換できます。

>[!NOTE]
>
>FormsサービスのWSDLを使用してフォームの自動埋め込みを行う場合は、`org.w3c.dom.Document`オブジェクトを`BLOB`オブジェクトに変換する必要があります。

**事前入力されたフォームのレンダリング**

他のフォームと同様に、事前入力されたフォームをレンダリングします。 唯一の違いは、XMLデータソースを含む`com.adobe.idp.Document`オブジェクトを使用してフォームの自動埋め込みを行う点です。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[FormsサービスAPIクイック開始](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[インタラクティブPDF formsのレンダリング](/help/forms/developing/rendering-interactive-pdf-forms.md)

[FormsをレンダリングするWeb アプリケーションの作成](/help/forms/developing/creating-web-applications-renders-forms.md)

### Java APIを使用したフォームの自動埋め込み{#prepopulating-forms-using-the-java-api}

FormsAPI(Java)を使用して編集可能なレイアウトを含むフォームを事前入力するには、次の手順を実行します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-forms-client.jarなどのクライアントJARファイルを含めます。 これらのファイルの場所については、[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。

1. メモリ内XMLデータソースの作成

   * `DocumentBuilderFactory`クラス’ `newInstance`メソッドを呼び出して、Java `DocumentBuilderFactory`オブジェクトを作成します。
   * `DocumentBuilderFactory`オブジェクトの`newDocumentBuilder`メソッドを呼び出して、Java `DocumentBuilder`オブジェクトを作成します。
   * `DocumentBuilder`オブジェクトの`newDocument`メソッドを呼び出して、`org.w3c.dom.Document`オブジェクトをインスタンス化します。
   * `org.w3c.dom.Document`オブジェクトの`createElement`メソッドを呼び出して、XMLデータソースのルート要素を作成します。 これにより、ルート要素を表す`Element`オブジェクトが作成されます。 要素名を表す文字列値を`createElement`メソッドに渡します。 戻り値を `Element` にキャストします。次に、`Document`オブジェクトの`appendChild`メソッドを呼び出してルートドキュメントを要素に追加し、ルート要素オブジェクトを引数として渡します。 次のコード行に、このアプリケーションロジックを示します。

      ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * `Document`オブジェクトの`createElement`メソッドを呼び出して、XMLデータソースのヘッダー要素を作成します。 要素名を表す文字列値を`createElement`メソッドに渡します。 戻り値を `Element` にキャストします。次に、`root`オブジェクトの`appendChild`メソッドを呼び出して、ルート要素にヘッダー要素を追加し、ヘッダー要素オブジェクトを引数として渡します。 ヘッダー要素に追加されるXML要素は、フォームの静的な部分に対応します。 次のコード行に、このアプリケーションロジックを示します。

      ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * `Document`オブジェクトの`createElement`メソッドを呼び出して、ヘッダー要素に属する子要素を作成し、要素名を表す文字列値を渡します。 戻り値を `Element` にキャストします。次に、子要素の`appendChild`メソッドを呼び出して値を設定し、`Document`オブジェクトの`createTextNode`メソッドを引数として渡します。 子要素の値として表示する文字列値を指定します。 最後に、ヘッダー要素の`appendChild`メソッドを呼び出して子要素をヘッダー要素に追加し、子要素オブジェクトを引数として渡します。 次のコード行に、このアプリケーションロジックを示します。

      ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`


   * フォームの静的部分に表示される各フィールドに対して最後のサブ手順を繰り返すことで、ヘッダー要素に残るす追加べての要素(XMLデータソース図では、これらのフィールドをAの節に示します（「データサブグループ[について」を参照）。](#understanding-data-subgroups)
   * `Document`オブジェクトの`createElement`メソッドを呼び出して、XMLデータソースの詳細要素を作成します。 要素名を表す文字列値を`createElement`メソッドに渡します。 戻り値を `Element` にキャストします。次に、`root`オブジェクトの`appendChild`メソッドを呼び出してルート要素に詳細要素を追加し、引数としてdetail要素オブジェクトを渡します。 detail要素に追加されるXML要素は、フォームの動的な部分に対応しています。 次のコード行に、このアプリケーションロジックを示します。

      ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * `Document`オブジェクトの`createElement`メソッドを呼び出して、detail要素に属する子要素を作成し、要素名を表す文字列値を渡します。 戻り値を `Element` にキャストします。次に、子要素の`appendChild`メソッドを呼び出して値を設定し、`Document`オブジェクトの`createTextNode`メソッドを引数として渡します。 子要素の値として表示する文字列値を指定します。 最後に、detail要素の`appendChild`メソッドを呼び出して子要素をdetail要素に追加し、子要素オブジェクトを引数として渡します。 次のコード行に、このアプリケーションロジックを示します。

      ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * すべてのXML要素に対して、最後のサブ手順を繰り返し、詳細要素に追加します。 発注書フォームへの入力に使用するXMLデータソースを適切に作成するには、次のXML要素を詳細要素に追加する必要があります。`txtDescription`、`numQty`、`numUnitPrice`。
   * フォームの自動埋め込みに使用されるすべてのデータ項目に対して、最後の2つのサブ手順を繰り返します。

1. XMLデータソースの変換

   * `javax.xml.transform.Transformer`オブジェクトの静的`newInstance`メソッドを呼び出して、`javax.xml.transform.Transformer`オブジェクトを作成します。
   * `TransformerFactory`オブジェクトの`newTransformer`メソッドを呼び出して、`Transformer`オブジェクトを作成します。
   * コンストラクタを使用して `ByteArrayOutputStream` オブジェクトを作成します。
   * コンストラクターを使用し、手順1で作成した`org.w3c.dom.Document`オブジェクトを渡して、`javax.xml.transform.dom.DOMSource`オブジェクトを作成します。
   * コンストラクタを使用して `javax.xml.transform.dom.DOMSource` オブジェクトを渡すことによって、`ByteArrayOutputStream` オブジェクトを作成します。
   * `javax.xml.transform.Transformer`オブジェクトの`transform`メソッドを呼び出し、`javax.xml.transform.dom.DOMSource`および`javax.xml.transform.stream.StreamResult`オブジェクトを渡して、Java `ByteArrayOutputStream`オブジェクトを入力します。
   * バイト配列を作成し、`ByteArrayOutputStream`オブジェクトのサイズをバイト配列に割り当てます。
   * `ByteArrayOutputStream`オブジェクトの`toByteArray`メソッドを呼び出して、バイト配列を入力します。
   * コンストラクタを使用し、バイト配列を渡して`com.adobe.idp.Document`オブジェクトを作成します。

1. 事前入力されたフォームのレンダリング

   `FormsServiceClient`オブジェクトの`renderPDFForm`メソッドを呼び出し、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定するstring値。
   * フォームとマージするデータを含む`com.adobe.idp.Document`オブジェクト。 手順1と2で作成した`com.adobe.idp.Document`オブジェクトを使用していることを確認します。
   * 実行時オプションを格納する`PDFFormRenderSpec`オブジェクト。
   * Formsサービスに必要なURI値を含む`URLSpec`オブジェクト。
   * 添付ファイルを格納する`java.util.HashMap`オブジェクト。 これはオプションのパラメーターです。フォームにファイルを添付しない場合は、`null`を指定できます。

   `renderPDFForm`メソッドは、クライアントのWebブラウザーに書き込む必要があるフォームデータストリームを含む`FormsResult`オブジェクトを返します。

   * フォームデータストリームをクライアントのWebブラウザーに送信するために使用する`javax.servlet.ServletOutputStream`オブジェクトを作成します。
   * `FormsResult`オブジェクト&#39;s `getOutputContent`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトを作成します。
   * `com.adobe.idp.Document`オブジェクトの`getInputStream`メソッドを呼び出して、`java.io.InputStream`オブジェクトを作成します。
   * `InputStream`オブジェクトの`read`メソッドを呼び出し、バイト配列を引数として渡すことで、バイト配列を作成し、フォームデータストリームを入力します。
   * `javax.servlet.ServletOutputStream`オブジェクトの`write`メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに送信します。 バイト配列を`write`メソッドに渡します。


**関連トピック**

[クイック開始（SOAPモード）:Java APIを使用した編集可能なレイアウトでのFormsの自動埋め込み](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したフォームの自動埋め込み{#prepopulating-forms-using-the-web-service-api}

FormsAPI（Webサービス）を使用して編集可能なレイアウトをフォームに自動埋め込むには、次の手順を実行します。

1. プロジェクトファイルを含める

   * FormsサービスのWSDLを使用するJavaプロキシクラスを作成します。 （「[Apache Axisを使用したJavaプロキシクラスの作成](/help/forms/developing/invoking-aem-forms-using-web.md#creating-java-proxy-classes-using-apache-axis)」を参照）。
   * クラスパスにJavaプロキシクラスを含めます。

1. メモリ内XMLデータソースの作成

   * `DocumentBuilderFactory`クラス’ `newInstance`メソッドを呼び出して、Java `DocumentBuilderFactory`オブジェクトを作成します。
   * `DocumentBuilderFactory`オブジェクトの`newDocumentBuilder`メソッドを呼び出して、Java `DocumentBuilder`オブジェクトを作成します。
   * `DocumentBuilder`オブジェクトの`newDocument`メソッドを呼び出して、`org.w3c.dom.Document`オブジェクトをインスタンス化します。
   * `org.w3c.dom.Document`オブジェクトの`createElement`メソッドを呼び出して、XMLデータソースのルート要素を作成します。 これにより、ルート要素を表す`Element`オブジェクトが作成されます。 要素名を表す文字列値を`createElement`メソッドに渡します。 戻り値を `Element` にキャストします。次に、`Document`オブジェクトの`appendChild`メソッドを呼び出してルートドキュメントを要素に追加し、ルート要素オブジェクトを引数として渡します。 次のコード行に、このアプリケーションロジックを示します。

      ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * `Document`オブジェクトの`createElement`メソッドを呼び出して、XMLデータソースのヘッダー要素を作成します。 要素名を表す文字列値を`createElement`メソッドに渡します。 戻り値を `Element` にキャストします。次に、`root`オブジェクトの`appendChild`メソッドを呼び出して、ルート要素にヘッダー要素を追加し、ヘッダー要素オブジェクトを引数として渡します。 ヘッダー要素に追加されるXML要素は、フォームの静的な部分に対応します。 次のコード行に、このアプリケーションロジックを示します。

      ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * `Document`オブジェクトの`createElement`メソッドを呼び出して、ヘッダー要素に属する子要素を作成し、要素名を表す文字列値を渡します。 戻り値を `Element` にキャストします。次に、子要素の`appendChild`メソッドを呼び出して値を設定し、`Document`オブジェクトの`createTextNode`メソッドを引数として渡します。 子要素の値として表示する文字列値を指定します。 最後に、ヘッダー要素の`appendChild`メソッドを呼び出して子要素をヘッダー要素に追加し、子要素オブジェクトを引数として渡します。 次のコード行に、このアプリケーションロジックを示します。

      ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`

   * フォームの静的部分に表示される各フィールドに対して最後のサブ手順を繰り返すことで、ヘッダー要素に残るす追加べての要素(XMLデータソース図では、これらのフィールドをAの節に示します（「データサブグループ[について」を参照）。](#understanding-data-subgroups)
   * `Document`オブジェクトの`createElement`メソッドを呼び出して、XMLデータソースの詳細要素を作成します。 要素名を表す文字列値を`createElement`メソッドに渡します。 戻り値を `Element` にキャストします。次に、`root`オブジェクトの`appendChild`メソッドを呼び出してルート要素に詳細要素を追加し、引数としてdetail要素オブジェクトを渡します。 detail要素に追加されるXML要素は、フォームの動的な部分に対応しています。 次のコード行に、このアプリケーションロジックを示します。

      ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * `Document`オブジェクトの`createElement`メソッドを呼び出して、detail要素に属する子要素を作成し、要素名を表す文字列値を渡します。 戻り値を `Element` にキャストします。次に、子要素の`appendChild`メソッドを呼び出して値を設定し、`Document`オブジェクトの`createTextNode`メソッドを引数として渡します。 子要素の値として表示する文字列値を指定します。 最後に、detail要素の`appendChild`メソッドを呼び出して子要素をdetail要素に追加し、子要素オブジェクトを引数として渡します。 次のコード行に、このアプリケーションロジックを示します。

      ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * すべてのXML要素に対して、最後のサブ手順を繰り返し、詳細要素に追加します。 発注書フォームへの入力に使用するXMLデータソースを適切に作成するには、次のXML要素を詳細要素に追加する必要があります。`txtDescription`、`numQty`、`numUnitPrice`。
   * フォームの自動埋め込みに使用されるすべてのデータ項目に対して、最後の2つのサブ手順を繰り返します。

1. XMLデータソースの変換

   * `javax.xml.transform.Transformer`オブジェクトの静的`newInstance`メソッドを呼び出して、`javax.xml.transform.Transformer`オブジェクトを作成します。
   * `TransformerFactory`オブジェクトの`newTransformer`メソッドを呼び出して、`Transformer`オブジェクトを作成します。
   * コンストラクタを使用して `ByteArrayOutputStream` オブジェクトを作成します。
   * コンストラクターを使用し、手順1で作成した`org.w3c.dom.Document`オブジェクトを渡して、`javax.xml.transform.dom.DOMSource`オブジェクトを作成します。
   * コンストラクタを使用して `javax.xml.transform.dom.DOMSource` オブジェクトを渡すことによって、`ByteArrayOutputStream` オブジェクトを作成します。
   * `javax.xml.transform.Transformer`オブジェクトの`transform`メソッドを呼び出し、`javax.xml.transform.dom.DOMSource`および`javax.xml.transform.stream.StreamResult`オブジェクトを渡して、Java `ByteArrayOutputStream`オブジェクトを入力します。
   * バイト配列を作成し、`ByteArrayOutputStream`オブジェクトのサイズをバイト配列に割り当てます。
   * `ByteArrayOutputStream`オブジェクトの`toByteArray`メソッドを呼び出して、バイト配列を入力します。
   * コンストラクターを使用して`BLOB`オブジェクトを作成し、`setBinaryData`メソッドを呼び出して、バイト配列を渡します。

1. 事前入力されたフォームのレンダリング

   `FormsService`オブジェクトの`renderPDFForm`メソッドを呼び出し、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定するstring値。
   * フォームとマージするデータを含む`BLOB`オブジェクト。 手順1と2で作成した`BLOB`オブジェクトを使用していることを確認します。
   * 実行時オプションを格納する`PDFFormRenderSpecc`オブジェクト。 詳しくは、[AEM FormsAPIリファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)を参照してください。
   * Formsサービスに必要なURI値を含む`URLSpec`オブジェクト。
   * 添付ファイルを格納する`java.util.HashMap`オブジェクト。 これはオプションのパラメーターです。フォームにファイルを添付しない場合は、`null`を指定できます。
   * メソッドによって入力される空の`com.adobe.idp.services.holders.BLOBHolder`オブジェクト。 これは、レンダリングされたPDFフォームを保存するために使用します。
   * メソッドによって入力される空の`javax.xml.rpc.holders.LongHolder`オブジェクト。 （この引数は、フォームのページ数を格納します）。
   * メソッドによって入力される空の`javax.xml.rpc.holders.StringHolder`オブジェクト。 （この引数はロケールの値を格納します）。
   * この操作の結果を含む空の`com.adobe.idp.services.holders.FormsResultHolder`オブジェクトです。

   `renderPDFForm`メソッドは、最後の引数値として渡される`com.adobe.idp.services.holders.FormsResultHolder`オブジェクトに、クライアントWebブラウザーに書き込む必要のあるフォームデータストリームを入力します。

   * `com.adobe.idp.services.holders.FormsResultHolder`オブジェクトの`value`データメンバの値を取得して、`FormResult`オブジェクトを作成します。
   * `FormsResult`オブジェクトの`getOutputContent`メソッドを呼び出して、フォームデータを含む`BLOB`オブジェクトを作成します。
   * `getContentType`メソッドを呼び出して、`BLOB`オブジェクトのコンテンツタイプを取得します。
   * `javax.servlet.http.HttpServletResponse`オブジェクトのコンテンツタイプを設定するには、`setContentType`メソッドを呼び出し、`BLOB`オブジェクトのコンテンツタイプを渡します。
   * `javax.servlet.http.HttpServletResponse`オブジェクトの`getOutputStream`メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに書き込むために使用する`javax.servlet.ServletOutputStream`オブジェクトを作成します。
   * バイト配列を作成し、`BLOB`オブジェクトの`getBinaryData`メソッドを呼び出して値を設定します。 このタスクは、`FormsResult`オブジェクトの内容をバイト配列に割り当てます。
   * `javax.servlet.http.HttpServletResponse`オブジェクトの`write`メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに送信します。 バイト配列を`write`メソッドに渡します。

   >[!NOTE]
   >
   >`renderPDFForm`メソッドは、最後の引数値として渡される`com.adobe.idp.services.holders.FormsResultHolder`オブジェクトに、クライアントWebブラウザーに書き込む必要のあるフォームデータストリームを入力します。

**関連トピック**

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

