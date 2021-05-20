---
title: DDXドキュメントの動的作成
seo-title: DDXドキュメントの動的作成
description: Java APIとWebサービスAPIを使用してDDXドキュメントを動的に作成します。 DDXドキュメントを動的に作成すると、実行時に取得されたDDXドキュメント内の値を使用できます。
seo-description: Java APIとWebサービスAPIを使用してDDXドキュメントを動的に作成します。 DDXドキュメントを動的に作成すると、実行時に取得されたDDXドキュメント内の値を使用できます。
uuid: b73e8069-6c9f-4517-a0ae-f3d503191d2d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 2ad227de-68a8-446f-8c4f-a33a6f95bec8
role: Developer
exl-id: b3c19c82-e26f-4dc8-b846-6aec705cee08
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2199'
ht-degree: 4%

---

# DDXドキュメントの動的な作成{#dynamically-creating-ddx-documents}

**このドキュメントのサンプルと例は、JEE上のAEM Forms環境に限られています。**

Assembler操作の実行に使用できるDDXドキュメントを動的に作成できます。 DDXドキュメントを動的に作成すると、実行時に取得されたDDXドキュメント内の値を使用できます。 DDXドキュメントを動的に作成するには、使用しているプログラミング言語に属するクラスを使用します。 例えば、Javaを使用してクライアントアプリケーションを開発する場合は、`org.w3c.dom.*`パッケージに属するクラスを使用します。 同様に、Microsoft .NETを使用している場合は、`System.Xml`名前空間に属するクラスを使用します。

DDXドキュメントをAssemblerサービスに渡す前に、XMLを`org.w3c.dom.Document`インスタンスから`com.adobe.idp.Document`インスタンスに変換します。 Webサービスを使用している場合は、XMLの作成に使用するデータ型（例えば、`XmlDocument`）から`BLOB`インスタンスにXMLを変換します。

この説明では、次のDDXドキュメントが動的に作成されたとします。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

このDDXドキュメントは、PDFドキュメントを分解します。 PDFドキュメントのディスアセンブリについて詳しく理解しておくことをお勧めします。

>[!NOTE]
>
>Assemblerサービスについて詳しくは、『AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)向けサービスリファレンス』を参照してください。[

>[!NOTE]
>
>DDXドキュメントについて詳しくは、『[AssemblerサービスとDDXリファレンス](https://www.adobe.com/go/learn_aemforms_ddx_63)』を参照してください。

## 手順の概要{#summary-of-steps}

動的に作成されたDDXドキュメントを使用してPDFドキュメントをディスアセンブリするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. PDFアセンブラークライアントを作成します。
1. DDXドキュメントを作成します。
1. DDXドキュメントを変換します。
1. 実行時オプションを設定します。
1. PDFドキュメントのディスアセンブリ。
1. アセンブリ解除したPDFドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用する場合は、プロキシファイルを必ず含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(AEM FormsをJBossにデプロイする場合に必要)
* jbossall-client.jar(AEM FormsをJBossにデプロイする場合に必要)

**PDFアセンブラークライアントの作成**

プログラムでAssembler操作を実行する前に、Assemblerサービスクライアントを作成します。

**DDXドキュメントの作成**

使用しているプログラミング言語を使用してDDXドキュメントを作成します。 PDFドキュメントをディスアセンブリするDDXドキュメントを作成するには、`PDFsFromBookmarks`要素が含まれていることを確認します。 Java APIを使用している場合、DDXドキュメントの作成に使用するデータ型を`com.adobe.idp.Document`インスタンスに変換します。 Webサービスを使用している場合は、データ型を`BLOB`インスタンスに変換します。

**DDXドキュメントの変換**

`org.w3c.dom`クラスを使用して作成されたDDXドキュメントは、`com.adobe.idp.Document`オブジェクトに変換する必要があります。 Java APIを使用する際にこのタスクを実行するには、Java XML変換クラスを使用します。 Webサービスを使用している場合は、DDXドキュメントを`BLOB`オブジェクトに変換します。

**ディスアセンブリするPDFドキュメントの参照**

PDFドキュメントをディスアセンブリするには、ディスアセンブリするPDFドキュメントを表すPDFファイルを参照します。 Assemblerサービスに渡されると、ドキュメント内のレベル1のブックマークごとに個別のPDFドキュメントが返されます。

**実行時オプションの設定**

ジョブの実行中にAssemblerサービスの動作を制御する実行時オプションを設定できます。 例えば、エラーが発生した場合にジョブの処理を続行するようAssemblerサービスに指示するオプションを設定できます。 実行時オプションを設定するには、`AssemblerOptionSpec`オブジェクトを使用します。

**PDFドキュメントのディスアセンブリ**

`invokeDDX`操作を呼び出して、PDFドキュメントをディスアセンブリします。 動的に作成されたDDXドキュメントを渡します。 Assemblerサービスは、コレクションオブジェクト内で分解されたPDFドキュメントを返します。

**分解したPDFドキュメントの保存**

アセンブリが解除されたPDFドキュメントはすべて、コレクションオブジェクト内で返されます。 コレクションオブジェクトを繰り返し処理し、各PDFドキュメントをPDFファイルとして保存します。

**関連トピック**

[Java APIを使用したDDXドキュメントの動的な作成](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-java-api)

[WebサービスAPIを使用したDDXドキュメントの動的な作成](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDFドキュメントのプログラムによる分解](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## Java API {#dynamically-create-a-ddx-document-using-the-java-api}を使用したDDXドキュメントの動的な作成

AssemblerサービスAPI(Java)を使用して、DDXドキュメントを動的に作成し、PDFドキュメントをディスアセンブリします。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-assembler-client.jarなどのクライアントJARファイルを含めます。

1. PDFアセンブラークライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して`AssemblerServiceClient`オブジェクトを渡し、`ServiceClientFactory`オブジェクトを作成します。

1. DDXドキュメントを作成します。

   * `DocumentBuilderFactory`クラス` `newInstance`メソッドを呼び出して、Java `DocumentBuilderFactory`オブジェクトを作成します。
   * `DocumentBuilderFactory`オブジェクトの`newDocumentBuilder`メソッドを呼び出して、Java `DocumentBuilder`オブジェクトを作成します。
   * `DocumentBuilder`オブジェクトの`newDocument`メソッドを呼び出して、`org.w3c.dom.Document`オブジェクトをインスタンス化します。
   * `org.w3c.dom.Document`オブジェクトの`createElement`メソッドを呼び出して、DDXドキュメントのルートエレメントを作成します。 このメソッドは、ルート要素を表す`Element`オブジェクトを作成します。 要素の名前を表す文字列値を`createElement`メソッドに渡します。 戻り値を `Element` にキャストします。次に、子要素の`setAttribute`メソッドを呼び出して値を設定します。 最後に、ヘッダー要素の`appendChild`メソッドを呼び出してヘッダー要素に要素を追加し、子要素オブジェクトを引数として渡します。 次のコード行に、このアプリケーションロジックを示します。
      ` Element root = (Element)document.createElement("DDX");  root.setAttribute("xmlns","https://ns.adobe.com/DDX/1.0/");  document.appendChild(root);`

   * `Document`オブジェクトの`createElement`メソッドを呼び出して、`PDFsFromBookmarks`要素を作成します。 要素の名前を表す文字列値を`createElement`メソッドに渡します。 戻り値を `Element` にキャストします。`setAttribute`メソッドを呼び出して、`PDFsFromBookmarks`要素の値を設定します。 DDX要素の`appendChild`メソッドを呼び出して、 `PDFsFromBookmarks`要素を`DDX`要素に追加します。 `PDFsFromBookmarks`要素オブジェクトを引数として渡します。 次のコード行に、このアプリケーションロジックを示します。

      ` Element PDFsFromBookmarks = (Element)document.createElement("PDFsFromBookmarks");  PDFsFromBookmarks.setAttribute("prefix","stmt");  root.appendChild(PDFsFromBookmarks);`

   * `Document`オブジェクトの`createElement`メソッドを呼び出して、`PDF`要素を作成します。 要素名を表すstring値を渡します。 戻り値を `Element` にキャストします。`setAttribute`メソッドを呼び出して、`PDF`要素の値を設定します。 `PDFsFromBookmarks`要素の`appendChild`メソッドを呼び出して、`PDF`要素を`PDFsFromBookmarks`要素に追加します。 `PDF`要素オブジェクトを引数として渡します。 次のコード行に、このアプリケーションロジックを示します。

      ` Element PDF = (Element)document.createElement("PDF");  PDF.setAttribute("source","AssemblerResultPDF.pdf");  PDFsFromBookmarks.appendChild(PDF);`

1. DDXドキュメントを変換します。

   * `javax.xml.transform.Transformer`オブジェクトの静的な`newInstance`メソッドを呼び出して、`javax.xml.transform.Transformer`オブジェクトを作成します。
   * `TransformerFactory`オブジェクトの`newTransformer`メソッドを呼び出して、`Transformer`オブジェクトを作成します。
   * コンストラクタを使用して `ByteArrayOutputStream` オブジェクトを作成します。
   * コンストラクタを使用して `javax.xml.transform.dom.DOMSource` オブジェクトを作成します。DDXドキュメントを表す`org.w3c.dom.Document`オブジェクトを渡します。
   * コンストラクタを使用して `javax.xml.transform.dom.DOMSource` オブジェクトを渡すことによって、`ByteArrayOutputStream` オブジェクトを作成します。
   * `javax.xml.transform.Transformer`オブジェクトの`transform`メソッドを呼び出して、Java `ByteArrayOutputStream`オブジェクトを設定します。 `javax.xml.transform.dom.DOMSource`と`javax.xml.transform.stream.StreamResult`オブジェクトを渡します。
   * バイト配列を作成し、`ByteArrayOutputStream`オブジェクトのサイズをバイト配列に割り当てます。
   * `ByteArrayOutputStream`オブジェクトの`toByteArray`メソッドを呼び出して、バイト配列を設定します。
   * コンストラクターを使用してバイト配列を渡し、`com.adobe.idp.Document`オブジェクトを作成します。

1. ディスアセンブリするPDFドキュメントの参照。

   * `HashMap`コンストラクターを使用して、入力PDFドキュメントの格納に使用する`java.util.Map`オブジェクトを作成します。
   * コンストラクターを使用し、ディスアセンブリするPDFドキュメントの場所を渡すことで、`java.io.FileInputStream`オブジェクトを作成します。
   * `com.adobe.idp.Document`オブジェクトを作成します。 ディスアセンブリするPDFドキュメントを含む`java.io.FileInputStream`オブジェクトを渡します。
   * `put`メソッドを呼び出し、次の引数を渡して、`java.util.Map`オブジェクトにエントリを追加します。

      * キー名を表すstring値です。 この値は、DDXドキュメントで指定されたPDFソース要素の値と一致する必要があります。 （動的に作成されるDDXドキュメントでは、値は`AssemblerResultPDF.pdf`です）。
      * ディスアセンブリするPDFドキュメントを含む`com.adobe.idp.Document`オブジェクト。

1. 実行時オプションを設定します。

   * コンストラクターを使用して、実行時オプションを格納する`AssemblerOptionSpec`オブジェクトを作成します。
   * `AssemblerOptionSpec`オブジェクトに属するメソッドを呼び出して、ビジネス要件に合った実行時オプションを設定します。 例えば、エラーが発生したときにジョブの処理を続行するようにAssemblerサービスに指示するには、`AssemblerOptionSpec`オブジェクトの`setFailOnError`メソッドを呼び出し、`false`を渡します。

1. PDFドキュメントのディスアセンブリ。

   `AssemblerServiceClient`オブジェクトの`invokeDDX`メソッドを呼び出し、次の値を渡します。

   * 動的に作成されたDDXドキュメントを表す`com.adobe.idp.Document`オブジェクト
   * ディスアセンブリするPDFドキュメントを含む`java.util.Map`オブジェクト
   * デフォルトのフォントやジョブのログレベルを含む、実行時のオプションを指定する`com.adobe.livecycle.assembler.client.AssemblerOptionSpec`オブジェクト

   `invokeDDX`メソッドは、分解されたPDFドキュメントと発生した例外を含む`com.adobe.livecycle.assembler.client.AssemblerResult`オブジェクトを返します。

1. アセンブリ解除したPDFドキュメントを保存します。

   分解されたPDFドキュメントを取得するには、次の操作を実行します。

   * `AssemblerResult`オブジェクトの`getDocuments`メソッドを呼び出します。 このメソッドは`java.util.Map`オブジェクトを返します。
   * `java.util.Map`オブジェクトを繰り返し処理して、結果の`com.adobe.idp.Document`オブジェクトを見つけます。
   * `com.adobe.idp.Document`オブジェクトの`copyToFile`メソッドを呼び出して、PDFドキュメントを抽出します。

**関連トピック**

[クイックスタート（SOAPモード）:Java APIを使用したDDXドキュメントの動的な作成](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-dynamically-creating-a-ddx-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## WebサービスAPI {#dynamically-create-a-ddx-document-using-the-web-service-api}を使用してDDXドキュメントを動的に作成する

Assembler Service API（Webサービス）を使用して、DDXドキュメントを動的に作成し、PDFドキュメントをディスアセンブリします。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 サービス参照を設定する際は、次のWSDL定義を使用してください。`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. PDFアセンブラークライアントを作成します。

   * デフォルトのコンストラクターを使用して`AssemblerServiceClient`オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`AssemblerServiceClient.Endpoint.Address`オブジェクトを作成します。 AEM FormsサービスにWSDLを指定するstring値を渡します（例：`http://localhost:8080/soap/services/AssemblerService?blob=mtom`）。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する際に使用されます。
   * `AssemblerServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値は、MTOMが使用されるようにします。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールド`AssemblerServiceClient.ClientCredentials.UserName.UserName`にAEM formsユーザー名を割り当てます。
      * 対応するパスワード値をフィールド`AssemblerServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * フィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に定数値`HttpClientCredentialType.Basic`を割り当てます。
      * フィールド`BasicHttpBindingSecurity.Security.Mode`に定数値`BasicHttpSecurityMode.TransportCredentialOnly`を割り当てます。

1. DDXドキュメントを作成します。

   * コンストラクタを使用して `System.Xml.XmlElement` オブジェクトを作成します。
   * `XmlElement`オブジェクトの`CreateElement`メソッドを呼び出して、DDXドキュメントのルートエレメントを作成します。 このメソッドは、ルート要素を表す`Element`オブジェクトを作成します。 要素の名前を表す文字列値を`CreateElement`メソッドに渡します。 `SetAttribute`メソッドを呼び出して、DDX要素の値を設定します。 最後に、 `XmlElement`オブジェクトの`AppendChild`メソッドを呼び出して、DDXドキュメントに要素を追加します。 DDXオブジェクトを引数として渡します。 次のコード行に、このアプリケーションロジックを示します。

      ` System.Xml.XmlElement root = ddx.CreateElement("DDX");  root.SetAttribute("xmlns", "https://ns.adobe.com/DDX/1.0/");  ddx.AppendChild(root);`

   * `XmlElement`オブジェクトの`CreateElement`メソッドを呼び出して、DDXドキュメントの`PDFsFromBookmarks`要素を作成します。 要素の名前を表す文字列値を`CreateElement`メソッドに渡します。 次に、 `SetAttribute`メソッドを呼び出して、要素の値を設定します。 `DDX`要素の`AppendChild`メソッドを呼び出して、`PDFsFromBookmarks`要素をルート要素に追加します。 `PDFsFromBookmarks`要素オブジェクトを引数として渡します。 次のコード行に、このアプリケーションロジックを示します。

      ` XmlElement PDFsFromBookmarks = ddx.CreateElement("PDFsFromBookmarks");  PDFsFromBookmarks.SetAttribute("prefix", "stmt");  root.AppendChild(PDFsFromBookmarks);`

   * `XmlElement`オブジェクトの`CreateElement`メソッドを呼び出して、DDXドキュメントの`PDF`要素を作成します。 要素の名前を表す文字列値を`CreateElement`メソッドに渡します。 次に、子要素の`SetAttribute`メソッドを呼び出して値を設定します。 `PDFsFromBookmarks`要素の`AppendChild`メソッドを呼び出して、`PDF`要素を`PDFsFromBookmarks`要素に追加します。 `PDF`要素オブジェクトを引数として渡します。 次のコード行に、このアプリケーションロジックを示します。

      ` XmlElement PDF = ddx.CreateElement("PDF");  PDF.SetAttribute("source", "AssemblerResultPDF.pdf");  PDFsFromBookmarks.AppendChild(PDF);`

1. DDXドキュメントを変換します。

   * コンストラクタを使用して `System.IO.MemoryStream` オブジェクトを作成します。
   * DDXドキュメントを表す`XmlElement`オブジェクトを使用して、DDXドキュメントで`MemoryStream`オブジェクトを設定します。 `XmlElement`オブジェクトの`Save`メソッドを呼び出して、`MemoryStream`オブジェクトを渡します。
   * バイト配列を作成し、`MemoryStream`オブジェクト内のデータを設定します。 次のコードは、このアプリケーションロジックを示しています。

      ` int bufLen = Convert.ToInt32(stream.Length);  byte[] byteArray = new byte[bufLen];  stream.Position = 0;  int count = stream.Read(byteArray, 0, bufLen);`

   * `BLOB`オブジェクトを作成します。 `BLOB`オブジェクトの`MTOM`フィールドにバイト配列を割り当てます。

1. ディスアセンブリするPDFドキュメントの参照。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、入力PDFドキュメントの保存に使用されます。 この`BLOB`オブジェクトは、引数として`invokeOneDocument`に渡されます。
   * コンストラクターを呼び出して、`System.IO.FileStream`オブジェクトを作成します。 入力PDFドキュメントのファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得することで、バイト配列のサイズを判断できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことによって、バイト配列にストリームデータを入力します。
   * `BLOB`オブジェクトの`MTOM`プロパティにバイト配列の内容を割り当てて、オブジェクトを設定します。

1. 実行時オプションを設定します。

   * コンストラクターを使用して、実行時オプションを格納する`AssemblerOptionSpec`オブジェクトを作成します。
   * `AssemblerOptionSpec`オブジェクトに属するデータメンバーに値を割り当てて、ビジネス要件に合った実行時オプションを設定します。 例えば、エラーが発生したときにジョブの処理を続行するようにAssemblerサービスに指示するには、`false`を`AssemblerOptionSpec`オブジェクトの`failOnError`データメンバーに割り当てます。

1. PDFドキュメントのディスアセンブリ。

   `AssemblerServiceClient`オブジェクトの`invokeDDX`メソッドを呼び出し、次の値を渡します。

   * 動的に作成されたDDXドキュメントを表す`BLOB`オブジェクト
   * 入力PDFドキュメントが含まれる`mapItem`配列
   * 実行時オプションを指定する`AssemblerOptionSpec`オブジェクト

   `invokeDDX`メソッドは、ジョブの結果と発生した例外を含む`AssemblerResult`オブジェクトを返します。

1. アセンブリ解除したPDFドキュメントを保存します。

   新しく作成したPDFドキュメントを取得するには、次の操作を実行します。

   * `AssemblerResult`オブジェクトの`documents`フィールドにアクセスします。これは、分解されたPDFドキュメントを含む`Map`オブジェクトです。
   * `Map`オブジェクトを繰り返し処理して、各結果ドキュメントを取得します。 次に、配列メンバの`value`を`BLOB`にキャストします。
   * `BLOB`オブジェクトの`MTOM`プロパティにアクセスして、PDFドキュメントを表すバイナリデータを抽出します。 PDFファイルに書き出すことができるバイトの配列を返します。

**関連トピック**

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
