---
title: DDXドキュメントの動的な作成
seo-title: DDXドキュメントの動的な作成
description: 'null'
seo-description: 'null'
uuid: b73e8069-6c9f-4517-a0ae-f3d503191d2d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 2ad227de-68a8-446f-8c4f-a33a6f95bec8
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '2123'
ht-degree: 4%

---


# DDXドキュメントの動的な作成{#dynamically-creating-ddx-documents}

Assembler操作の実行に使用できるDDXドキュメントを動的に作成できます。 DDXドキュメントを動的に作成すると、実行時に取得したDDXドキュメントの値を使用できます。 DDXドキュメントを動的に作成するには、使用しているプログラミング言語に属するクラスを使用します。 例えば、Javaを使用してクライアントアプリケーションを開発する場合は、`org.w3c.dom.*`パッケージに属するクラスを使用します。 同様に、Microsoft .NETを使用している場合は、`System.Xml`名前空間に属するクラスを使用します。

DDXドキュメントをAssemblerサービスに渡す前に、XMLを`org.w3c.dom.Document`インスタンスから`com.adobe.idp.Document`インスタンスに変換します。 Webサービスを使用している場合は、XMLの作成に使用したデータ型（例えば、`XmlDocument`）のXMLを`BLOB`インスタンスに変換します。

この説明では、次のDDXドキュメントが動的に作成されると仮定します。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

このDDXドキュメントは、PDFドキュメントをディスアセンブリします。 PDFドキュメントのディスアセンブリについて詳しいことをお勧めします。

>[!NOTE]
>
>Assemblerサービスについて詳しくは、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

>[!NOTE]
>
>DDXドキュメントについて詳しくは、「[Assembler Service and DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63)」を参照してください。

## 手順{#summary-of-steps}の概要

動的に作成されたDDXドキュメントを使用してPDFドキュメントをディスアセンブリするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. PDFアセンブラクライアントを作成します。
1. DDXドキュメントを作成します
1. DDXドキュメントを変換します。
1. 実行時オプションを設定します。
1. PDFドキュメントのディスアセンブリ
1. アセンブル解除されたPDFドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(AEM FormsがJBossにデプロイされている場合に必要)
* jbossall-client.jar(AEM FormsがJBossにデプロイされている場合に必要)

**PDFアセンブラクライアントの作成**

プログラムによってAssembler操作を実行する前に、Assemblerサービスクライアントを作成します。

**DDXドキュメントの作成**

使用しているプログラミング言語を使用して、DDXドキュメントを作成します。 PDFドキュメントをディスアセンブリするDDXドキュメントを作成するには、`PDFsFromBookmarks`要素が含まれていることを確認します。 Java APIを使用している場合、DDXドキュメントの作成に使用するデータタイプを`com.adobe.idp.Document`インスタンスに変換します。 Webサービスを使用している場合は、データ型を`BLOB`インスタンスに変換します。

**DDXドキュメントの変換**

`org.w3c.dom`クラスを使用して作成されたDDXドキュメントは、`com.adobe.idp.Document`オブジェクトに変換する必要があります。 Java APIを使用する場合にこのタスクを実行するには、Java XML変換クラスを使用します。 Webサービスを使用している場合は、DDXドキュメントを`BLOB`オブジェクトに変換します。

**PDFドキュメントの参照によるディスアセンブリ**

PDFドキュメントをディスアセンブリするには、ディスアセンブリするPDFドキュメントを表すPDFファイルを参照します。 Assemblerサービスに渡されると、ドキュメント内のレベル1のブックマークごとに個別のPDFドキュメントが返されます。

**実行時オプションの設定**

ジョブの実行中にAssemblerサービスの動作を制御する実行時オプションを設定できます。 例えば、エラーが発生した場合にジョブの処理を続行するようAssemblerサービスに指示するオプションを設定できます。 実行時オプションを設定するには、`AssemblerOptionSpec`オブジェクトを使用します。

**PDFドキュメントのディスアセンブリ**

`invokeDDX`操作を呼び出して、PDFドキュメントをディスアセンブリします。 動的に作成されたDDXドキュメントを渡します。 Assemblerサービスは、コレクションオブジェクト内で分解されたPDFドキュメントを返します。

**アセンブル解除されたPDFドキュメントの保存**

分解されたすべてのPDFドキュメントは、コレクションオブジェクト内で返されます。 コレクションオブジェクトを繰り返し処理し、各PDFドキュメントをPDFファイルとして保存します。

**関連トピック**

[Java APIを使用したDDXドキュメントの動的な作成](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-java-api)

[WebサービスAPIを使用したDDXドキュメントの動的な作成](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[プログラムによるPDFドキュメントのディスアセンブリ](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## Java API {#dynamically-create-a-ddx-document-using-the-java-api}を使用したDDXドキュメントの動的な作成

DDXドキュメントを動的に作成し、Assembler Service API(Java)を使用してPDFドキュメントをディスアセンブリします。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-assembler-client.jarなどのクライアントJARファイルを含めます。

1. PDFアセンブラクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用し、`AssemblerServiceClient`オブジェクトを渡して、`ServiceClientFactory`オブジェクトを作成します。

1. DDXドキュメントを作成します

   * `DocumentBuilderFactory`クラス’ `newInstance`メソッドを呼び出して、Java `DocumentBuilderFactory`オブジェクトを作成します。
   * `DocumentBuilderFactory`オブジェクトの`newDocumentBuilder`メソッドを呼び出して、Java `DocumentBuilder`オブジェクトを作成します。
   * `DocumentBuilder`オブジェクトの`newDocument`メソッドを呼び出して、`org.w3c.dom.Document`オブジェクトをインスタンス化します。
   * `org.w3c.dom.Document`オブジェクトの`createElement`メソッドを呼び出して、DDXドキュメントのルートエレメントを作成します。 このメソッドは、ルート要素を表す`Element`オブジェクトを作成します。 要素名を表す文字列値を`createElement`メソッドに渡します。 戻り値を `Element` にキャストします。次に、子要素の`setAttribute`メソッドを呼び出して、値を設定します。 最後に、ヘッダー要素の`appendChild`メソッドを呼び出して要素をヘッダー要素に追加し、子要素オブジェクトを引数として渡します。 次のコード行に、このアプリケーションロジックを示します。
      ` Element root = (Element)document.createElement("DDX");  root.setAttribute("xmlns","https://ns.adobe.com/DDX/1.0/");  document.appendChild(root);`

   * `Document`オブジェクトの`createElement`メソッドを呼び出して、`PDFsFromBookmarks`要素を作成します。 要素名を表す文字列値を`createElement`メソッドに渡します。 戻り値を `Element` にキャストします。`PDFsFromBookmarks`要素の値を設定するには、`setAttribute`メソッドを呼び出します。 DDX要素の`appendChild`メソッドを呼び出して、`PDFsFromBookmarks`要素を`DDX`要素に追加します。 `PDFsFromBookmarks`要素オブジェクトを引数として渡します。 次のコード行に、このアプリケーションロジックを示します。

      ` Element PDFsFromBookmarks = (Element)document.createElement("PDFsFromBookmarks");  PDFsFromBookmarks.setAttribute("prefix","stmt");  root.appendChild(PDFsFromBookmarks);`

   * `Document`オブジェクトの`createElement`メソッドを呼び出して、`PDF`要素を作成します。 要素名を表すstring値を渡します。 戻り値を `Element` にキャストします。`PDF`要素の値を設定するには、`setAttribute`メソッドを呼び出します。 `PDFsFromBookmarks`要素の`appendChild`メソッドを呼び出して、`PDF`要素を`PDFsFromBookmarks`要素に追加します。 `PDF`要素オブジェクトを引数として渡します。 次のコード行に、このアプリケーションロジックを示します。

      ` Element PDF = (Element)document.createElement("PDF");  PDF.setAttribute("source","AssemblerResultPDF.pdf");  PDFsFromBookmarks.appendChild(PDF);`

1. DDXドキュメントを変換します。

   * `javax.xml.transform.Transformer`オブジェクトの静的`newInstance`メソッドを呼び出して、`javax.xml.transform.Transformer`オブジェクトを作成します。
   * `TransformerFactory`オブジェクトの`newTransformer`メソッドを呼び出して、`Transformer`オブジェクトを作成します。
   * コンストラクタを使用して `ByteArrayOutputStream` オブジェクトを作成します。
   * コンストラクタを使用して `javax.xml.transform.dom.DOMSource` オブジェクトを作成します。DDXドキュメントを表す`org.w3c.dom.Document`オブジェクトを渡します。
   * コンストラクタを使用して `javax.xml.transform.dom.DOMSource` オブジェクトを渡すことによって、`ByteArrayOutputStream` オブジェクトを作成します。
   * `javax.xml.transform.Transformer`オブジェクトの`transform`メソッドを呼び出して、Java `ByteArrayOutputStream`オブジェクトを入力します。 `javax.xml.transform.dom.DOMSource`および`javax.xml.transform.stream.StreamResult`オブジェクトを渡します。
   * バイト配列を作成し、`ByteArrayOutputStream`オブジェクトのサイズをバイト配列に割り当てます。
   * `ByteArrayOutputStream`オブジェクトの`toByteArray`メソッドを呼び出して、バイト配列を入力します。
   * コンストラクタを使用し、バイト配列を渡して`com.adobe.idp.Document`オブジェクトを作成します。

1. ディスアセンブリするPDFドキュメントの参照

   * `HashMap`コンストラクターを使用して、入力PDFドキュメントの格納に使用する`java.util.Map`オブジェクトを作成します。
   * コンストラクターを使用し、ディスアセンブリするPDFドキュメントの場所を渡して、`java.io.FileInputStream`オブジェクトを作成します。
   * `com.adobe.idp.Document`オブジェクトを作成します。 ディスアセンブリするPDFドキュメントを含む`java.io.FileInputStream`オブジェクトを渡します。
   * &lt;a0追加/>オブジェクトへのエントリ。その`java.util.Map`メソッドを呼び出し、次の引数を渡すことによって作成します。`put`

      * キー名を表すstring値です。 この値は、DDXドキュメントで指定されたPDFソース要素の値と一致する必要があります。 (動的に作成されるDDXドキュメントでは、値は`AssemblerResultPDF.pdf`です)。
      * ディスアセンブリするPDFドキュメントが含まれる`com.adobe.idp.Document`オブジェクトです。

1. 実行時オプションを設定します。

   * コンストラクターを使用して、実行時オプションを格納する`AssemblerOptionSpec`オブジェクトを作成します。
   * `AssemblerOptionSpec`オブジェクトに属するメソッドを呼び出して、ビジネス要件に合うように実行時オプションを設定します。 例えば、エラーが発生した場合にジョブの処理を続行するようにAssemblerサービスに指示するには、`AssemblerOptionSpec`オブジェクトの`setFailOnError`メソッドを呼び出し、`false`を渡します。

1. PDFドキュメントのディスアセンブリ

   `AssemblerServiceClient`オブジェクトの`invokeDDX`メソッドを呼び出し、次の値を渡します。

   * 動的に作成されるDDXドキュメントを表す`com.adobe.idp.Document`オブジェクト
   * ディスアセンブリするPDFドキュメントが含まれる`java.util.Map`オブジェクト
   * デフォルトフォントとジョブログレベルを含む、実行時のオプションを指定する`com.adobe.livecycle.assembler.client.AssemblerOptionSpec`オブジェクト

   `invokeDDX`メソッドは、分解されたPDFドキュメントと発生した例外を含む`com.adobe.livecycle.assembler.client.AssemblerResult`オブジェクトを返します。

1. アセンブル解除されたPDFドキュメントを保存します。

   ディスアセンブリされたPDFドキュメントを取得するには、次の操作を実行します。

   * `AssemblerResult`オブジェクトの`getDocuments`メソッドを呼び出します。 このメソッドは、`java.util.Map`オブジェクトを返します。
   * `java.util.Map`オブジェクトを繰り返し処理して、結果の`com.adobe.idp.Document`オブジェクトを見つけます。
   * `com.adobe.idp.Document`オブジェクトの`copyToFile`メソッドを呼び出してPDFドキュメントを抽出します。

**関連トピック**

[クイック開始（SOAPモード）:Java APIを使用したDDXドキュメントの動的な作成](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-dynamically-creating-a-ddx-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## WebサービスAPI {#dynamically-create-a-ddx-document-using-the-web-service-api}を使用したDDXドキュメントの動的な作成

DDXドキュメントを動的に作成し、Assembler Service API（Webサービス）を使用してPDFドキュメントをディスアセンブリします。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 サービス参照を設定する際は、次のWSDL定義を使用してください。`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. PDFアセンブラクライアントを作成します。

   * `AssemblerServiceClient`オブジェクトを作成するには、そのオブジェクトのデフォルトのコンストラクタを使用します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`AssemblerServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに指定するstring値を渡します（例：`http://localhost:8080/soap/services/AssemblerService?blob=mtom`）。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する際に使用されます。
   * `AssemblerServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * AEM formsユーザー名をフィールド`AssemblerServiceClient.ClientCredentials.UserName.UserName`に割り当てます。
      * 対応するパスワード値をフィールド`AssemblerServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * 定数値`HttpClientCredentialType.Basic`をフィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に割り当てます。
      * 定数値`BasicHttpSecurityMode.TransportCredentialOnly`をフィールド`BasicHttpBindingSecurity.Security.Mode`に割り当てます。

1. DDXドキュメントを作成します

   * コンストラクタを使用して `System.Xml.XmlElement` オブジェクトを作成します。
   * `XmlElement`オブジェクトの`CreateElement`メソッドを呼び出して、DDXドキュメントのルートエレメントを作成します。 このメソッドは、ルート要素を表す`Element`オブジェクトを作成します。 要素名を表す文字列値を`CreateElement`メソッドに渡します。 `SetAttribute`メソッドを呼び出して、DDX要素の値を設定します。 最後に、`XmlElement`オブジェクトの`AppendChild`メソッドを呼び出して、DDXドキュメントに要素を追加します。 DDXオブジェクトを引数として渡します。 次のコード行に、このアプリケーションロジックを示します。

      ` System.Xml.XmlElement root = ddx.CreateElement("DDX");  root.SetAttribute("xmlns", "https://ns.adobe.com/DDX/1.0/");  ddx.AppendChild(root);`

   * `XmlElement`オブジェクトの`CreateElement`メソッドを呼び出して、DDXドキュメントの`PDFsFromBookmarks`要素を作成します。 要素名を表す文字列値を`CreateElement`メソッドに渡します。 次に、`SetAttribute`メソッドを呼び出して、要素の値を設定します。 `DDX`要素の`AppendChild`メソッドを呼び出して、`PDFsFromBookmarks`要素をルート要素に追加します。 `PDFsFromBookmarks`要素オブジェクトを引数として渡します。 次のコード行に、このアプリケーションロジックを示します。

      ` XmlElement PDFsFromBookmarks = ddx.CreateElement("PDFsFromBookmarks");  PDFsFromBookmarks.SetAttribute("prefix", "stmt");  root.AppendChild(PDFsFromBookmarks);`

   * `XmlElement`オブジェクトの`CreateElement`メソッドを呼び出して、DDXドキュメントの`PDF`要素を作成します。 要素名を表す文字列値を`CreateElement`メソッドに渡します。 次に、子要素の`SetAttribute`メソッドを呼び出して、値を設定します。 `PDFsFromBookmarks`要素の`AppendChild`メソッドを呼び出して、`PDF`要素を`PDFsFromBookmarks`要素に追加します。 `PDF`要素オブジェクトを引数として渡します。 次のコード行に、このアプリケーションロジックを示します。

      ` XmlElement PDF = ddx.CreateElement("PDF");  PDF.SetAttribute("source", "AssemblerResultPDF.pdf");  PDFsFromBookmarks.AppendChild(PDF);`

1. DDXドキュメントを変換します。

   * コンストラクタを使用して `System.IO.MemoryStream` オブジェクトを作成します。
   * DDXドキュメントを表す`XmlElement`オブジェクトを使用して、`MemoryStream`オブジェクトにDDXドキュメントを入力します。 `XmlElement`オブジェクトの`Save`メソッドを呼び出し、`MemoryStream`オブジェクトを渡します。
   * バイト配列を作成し、`MemoryStream`オブジェクト内のデータを入力します。 次のコードは、このアプリケーションロジックを示しています。

      ` int bufLen = Convert.ToInt32(stream.Length);  byte[] byteArray = new byte[bufLen];  stream.Position = 0;  int count = stream.Read(byteArray, 0, bufLen);`

   * `BLOB`オブジェクトを作成します。 バイト配列を`BLOB`オブジェクトの`MTOM`フィールドに割り当てます。

1. ディスアセンブリするPDFドキュメントの参照

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、入力PDFドキュメントの保存に使用されます。 この`BLOB`オブジェクトは、`invokeOneDocument`に引数として渡されます。
   * コンストラクターを呼び出して、`System.IO.FileStream`オブジェクトを作成します。 入力PDFドキュメントーのファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得して、バイト配列のサイズを決定できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * `BLOB`オブジェクトに、`MTOM`プロパティにバイト配列の内容を割り当てて入力します。

1. 実行時オプションを設定します。

   * コンストラクターを使用して、実行時オプションを格納する`AssemblerOptionSpec`オブジェクトを作成します。
   * `AssemblerOptionSpec`オブジェクトに属するデータメンバに値を割り当てて、ビジネス要件に合うように実行時オプションを設定します。 例えば、エラーが発生した場合にジョブの処理を続行するようにAssemblerサービスに指示するには、`false`を`AssemblerOptionSpec`オブジェクトの`failOnError`データメンバーに割り当てます。

1. PDFドキュメントのディスアセンブリ

   `AssemblerServiceClient`オブジェクトの`invokeDDX`メソッドを呼び出し、次の値を渡します。

   * 動的に作成されるDDXドキュメントを表す`BLOB`オブジェクト
   * 入力PDFドキュメントが含まれる`mapItem`配列
   * 実行時オプションを指定する`AssemblerOptionSpec`オブジェクト

   `invokeDDX`メソッドは、ジョブの結果と発生した例外を含む`AssemblerResult`オブジェクトを返します。

1. アセンブル解除されたPDFドキュメントを保存します。

   新しく作成されたPDFドキュメントを取得するには、次の操作を実行します。

   * `AssemblerResult`オブジェクトの`documents`フィールドにアクセスします。これは、分解されたPDFドキュメントが格納されている`Map`オブジェクトです。
   * `Map`オブジェクトを繰り返し処理して、各結果ドキュメントを取得します。 次に、その配列メンバーの`value`を`BLOB`にキャストします。
   * `BLOB`オブジェクトの`MTOM`プロパティにアクセスして、PDFドキュメントを表すバイナリデータを抽出します。 PDFファイルに書き出すことができるバイトの配列を返します。

**関連トピック**

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
