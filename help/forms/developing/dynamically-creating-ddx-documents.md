---
title: DDX ドキュメントの動的な作成
seo-title: Dynamically Creating DDX Documents
description: Java API と web サービス API を使用して DDX ドキュメントを動的に作成します。 DDX ドキュメントを動的に作成すると、実行時に取得された DDX ドキュメント内の値を使用できます。
seo-description: Create a DDX document dynamically using the Java API and Web Service API. Dynamically creating a DDX document enables you to use values in the DDX document that are obtained during run-time.
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
source-wordcount: '2163'
ht-degree: 100%

---

# DDX ドキュメントの動的な作成 {#dynamically-creating-ddx-documents}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

Assembler 操作の実行に使用できる DDX ドキュメントを動的に作成できます。 DDX ドキュメントを動的に作成すると、実行時に取得された DDX ドキュメント内の値を使用できます。 DDX ドキュメントを動的に作成するには、使用しているプログラミング言語に属するクラスを使用します。 例えば、Java を使用してクライアントアプリケーションを開発する場合は、 `org.w3c.dom.*`パッケージに属するクラスを使用します。同様に、Microsoft .NET を使用している場合は、 `System.Xml` 名前空間に属するクラスを使用します。

DDX ドキュメントを Assembler サービスに渡す前に、XML を `org.w3c.dom.Document` インスタンスから `com.adobe.idp.Document` インスタンスに変換します。Web サービスを使用している場合は、XML を作成するために使用されたデータタイプから XML を `BLOB` インスタンスに変換します（例： `XmlDocument`）

このディスカッションでは、次の DDX ドキュメントが動的に作成されると仮定します。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

この DDX ドキュメントは、PDF ドキュメントをディスアセンブリします。 PDF ドキュメントのディスアセンブリに関する知識を身に付けることをお勧めします。

>[!NOTE]
>
>Assembler サービスについて詳しくは、[AEM Forms サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

>[!NOTE]
>
>DDX ドキュメントについて詳しくは、[Assembler サービスと DDX リファレンス](https://www.adobe.com/go/learn_aemforms_ddx_63)を参照してください。

## 手順の概要 {#summary-of-steps}

動的に作成された DDX ドキュメントを使用して PDF ドキュメントをディスアセンブリするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. PDF Assembler クライアントを作成します。
1. DDX ドキュメントを作成します。
1. DDX ドキュメントを変換します。
1. 実行時オプションを設定します。
1. PDF ドキュメントを分割します。
1. 分割した PDF ドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar（AEM Forms が JBoss にデプロイされている場合に必要）
* jbossall-client.jar（AEM Formsが JBoss にデプロイされている場合に必要）

**PDF Assembler クライアントの作成**

Assembler 操作をプログラムで実行する前に、Assembler サービスクライアントを作成します。

**DDX ドキュメントの作成**

使用しているプログラミング言語を使用して DDX ドキュメントを作成します。 PDF ドキュメントをディスアセンブリする DDX ドキュメントを作成するには、ドキュメントに `PDFsFromBookmarks` 要素が含まれていることを確認します。DDX ドキュメントの作成に使用するデータタイプを `com.adobe.idp.Document` インスタンスに変換をします（Java API を使用する場合）。 Web サービスを使用している場合は、データタイプを `BLOB` インスタンスに変換します。

**DDX ドキュメントの変換**

`org.w3c.dom` クラスを使って作成した DDX ドキュメントは、 `com.adobe.idp.Document` オブジェクトに変換する必要があります。Java API を使用する際にこのタスクを実行するには、Java XML 変換クラスを使用します。 Web サービスを使用している場合は、DDX ドキュメントを `BLOB` オブジェクトに変換します。

**ディスアセンブリする PDF ドキュメントの参照**

PDF ドキュメントを分割するには、分割する PDF ドキュメントを表す PDF ファイルを参照します。Assembler サービスに渡されると、その PDF ドキュメント内のレベル 1 のブックマークごとに別の PDF ドキュメントが返されます。

**実行時オプションを設定**

ジョブを実行する際の Assembler サービスの動作を制御する実行時オプションを設定できます。例えば、エラーが発生した場合にジョブの処理を続行するよう Assembler サービスに指示するオプションを設定できます。 実行時オプションを設定するには、 `AssemblerOptionSpec` オブジェクトを使用します。

**PDF ドキュメントのディスアセンブリ**

`invokeDDX` 操作を呼び出して、PDF ドキュメントをディスアセンブリします。動的に作成された DDX ドキュメントを渡します。 Assembler サービスは、コレクションオブジェクト内のディスアセンブリされた PDF ドキュメントを返します。

**ディスアセンブリされた PDF ドキュメントを保存**

分割されたすべての PDF ドキュメントは、コレクションオブジェクト内で返されます。コレクションオブジェクトを反復処理し、各 PDF ドキュメントを PDF ファイルとして保存します。

**関連トピック**

[Java API を使用した DDX ドキュメントの動的な作成](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-java-api)

[Web サービス API を使用した DDX ドキュメントの動的な作成](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[プログラムによる PDF ドキュメントの分割](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## Java API を使用した DDX ドキュメントの動的な作成 {#dynamically-create-a-ddx-document-using-the-java-api}

Assembler サービス API（Java）を使用して、DDX ドキュメントを動的に作成し、PDF ドキュメントをディスアセンブリします。

1. プロジェクトファイルを含めます。

   adobe-livecycle-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. PDF Assembler クライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して `ServiceClientFactory` オブジェクトを渡すことによって、`AssemblerServiceClient` オブジェクトを作成します。

1. DDX ドキュメントを作成します。

   *  `DocumentBuilderFactory` クラスの `newInstance` メソッドを呼び出して、Java `DocumentBuilderFactory` オブジェクトを作成します。
   * `DocumentBuilderFactory` オブジェクトの `newDocumentBuilder` メソッドを呼び出して、Java の `DocumentBuilder` オブジェクトを作成します。 
   * `DocumentBuilder` オブジェクトの `newDocument` メソッドを呼び出し、`org.w3c.dom.Document` オブジェクトをインスタンス化します。
   * `org.w3c.dom.Document` オブジェクトの `createElement` メソッドを呼び出して、DDX ドキュメントのルート要素を作成します。このメソッドは、 ルート要素を表す `Element` オブジェクトを作成します。 要素の名前を表す文字列値を `createElement` メソッドに渡します。戻り値を `Element` にキャストします。次に、`setAttribute` メソッド呼び出して、子要素の値を設定します。最後に、Header 要素を要素に追加するには、Header 要素の `appendChild` メソッドを呼び出して、子要素オブジェクトを引数として渡します。 次のコード行は、このアプリケーションロジックを示しています。
      ` Element root = (Element)document.createElement("DDX");  root.setAttribute("xmlns","https://ns.adobe.com/DDX/1.0/");  document.appendChild(root);`

   * `Document` オブジェクトの `createElement` メソッドを呼び出して、`PDFsFromBookmarks` 要素を作成します。 要素の名前を表す文字列値を `createElement` メソッドに渡します。 戻り値を `Element` にキャストします。`setAttribute` メソッドを呼び出して、`PDFsFromBookmarks` 要素の値を設定 します。DDX 要素の `appendChild` メソッドを呼び出して、`DDX` 要素に `PDFsFromBookmarks` 要素を追加します。`PDFsFromBookmarks` 要素オブジェクトを引数として渡します。 次のコード行は、このアプリケーションロジックを示しています。

      ` Element PDFsFromBookmarks = (Element)document.createElement("PDFsFromBookmarks");  PDFsFromBookmarks.setAttribute("prefix","stmt");  root.appendChild(PDFsFromBookmarks);`

   * `Document` オブジェクトの `createElement` メソッドを呼び出して、`PDF` 要素を作成します。要素名を表す文字列の値を渡します。戻り値を `Element` にキャストします。`setAttribute` メソッドを呼び出して、`PDF` 要素の値を設定します。`PDFsFromBookmarks` 要素の `appendChild` メソッドを呼び出して、`PDF` 要素を `PDFsFromBookmarks` 要素に追加します。`PDF` 要素オブジェクトを引数として渡します。 次のコード行に、このアプリケーションロジックを示します。

      ` Element PDF = (Element)document.createElement("PDF");  PDF.setAttribute("source","AssemblerResultPDF.pdf");  PDFsFromBookmarks.appendChild(PDF);`

1. DDX ドキュメントを変換します。

   * `javax.xml.transform.Transformer` オブジェクトを作成するには、`javax.xml.transform.Transformer` オブジェクトの静的 `newInstance` メソッドを呼び出します。
   * `TransformerFactory` オブジェクトの `newTransformer` メソッドを呼び出すことによって、`Transformer` オブジェクトを作成します。
   * コンストラクタを使用して `ByteArrayOutputStream` オブジェクトを作成します。
   * コンストラクタを使用して `javax.xml.transform.dom.DOMSource` オブジェクトを作成します。DDX ドキュメントを表す `org.w3c.dom.Document` オブジェクトを渡します。
   * `javax.xml.transform.dom.DOMSource` オブジェクトを作成するには、コンストラクタを使用して、`ByteArrayOutputStream` オブジェクトを渡します。
   * `javax.xml.transform.Transformer` オブジェクトの `transform` メソッドを呼び出して、Java `ByteArrayOutputStream` オブジェクトを入力します。`javax.xml.transform.dom.DOMSource` オブジェクトと `javax.xml.transform.stream.StreamResult` オブジェクトを渡します。
   * バイト配列を作成し、 `ByteArrayOutputStream` オブジェクトをバイト配列に割り当てます。
   * `ByteArrayOutputStream` オブジェクトの `toByteArray` メソッドを呼び出して、バイト配列を設定します。
   * コンストラクターを使用して、バイト配列を渡すことによって、`com.adobe.idp.Document` オブジェクトを作成します。

1. 分割する PDF ドキュメントを参照します。

   * `HashMap` コンストラクターを使って、入力 PDF ドキュメントを保存するために使用する `java.util.Map` オブジェクトを作成します。
   * `java.io.FileInputStream` オブジェクトを作成するには、コンストラクターを使用し、ディスアセンブリする PDF ドキュメントの場所を渡します。
   * `com.adobe.idp.Document` オブジェクトを作成します。ディスアセンブリする PDF ドキュメントを含む `java.io.FileInputStream` オブジェクトを作成します。
   * エントリを `java.util.Map` オブジェクトに追加するには、`put` メソッドを呼び出し、次の引数を渡します。

      * キー名を表す文字列値。この値は、DDX ドキュメントで指定された PDF ソース要素の値と一致する必要があります（動的に作成される DDX ドキュメントでは、値は `AssemblerResultPDF.pdf` です）。
      * ディスアセンブリする PDF ドキュメントを含む `com.adobe.idp.Document` オブジェクト。

1. 実行時オプションを設定します。

   * コンストラクタを使用して、実行時オプションを格納する `AssemblerOptionSpec` オブジェクトを作成します。
   * `AssemblerOptionSpec` オブジェクトに属するメソッドを呼び出して、ビジネス要件を満たすよう実行時オプションを設定します。例えば、エラーが発生時にジョブの処理を続行するように Assembler サービスに指示するには、 `AssemblerOptionSpec` オブジェクトの `setFailOnError` メソッドとパス `false`を呼び出します。

1. PDF ドキュメントを分割します。

   `AssemblerServiceClient` オブジェクトの `invokeDDX` メソッドを呼び出して、次の値を渡します。

   * 動的に作成された DDX ドキュメントを表す `com.adobe.idp.Document` オブジェクト
   * ディスアセンブリする PDF ドキュメントを含む `java.util.Map` オブジェクト
   * デフォルトのフォントやジョブログレベルを含む、実行時のオプションを指定する `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` オブジェクト

   `invokeDDX` メソッドは、 ディスアセンブリされた PDF ドキュメントと発生した例外を含む `com.adobe.livecycle.assembler.client.AssemblerResult` オブジェクトを返します。

1. 分割した PDF ドキュメントを保存します。

   分割された PDF ドキュメントを取得するには、以下のアクションを実行します。

   * `AssemblerResult` オブジェクトの `getDocuments` メソッドを呼び出します。このメソッドは、`java.util.Map` オブジェクトを返します。
   * 結果の `com.adobe.idp.Document` オブジェクトが見つかるまで、`java.util.Map` オブジェクトを反復処理します。
   * `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを呼び出して、PDF ドキュメントを抽出します。

**関連トピック**

[クイックスタート（SOAP モード）：Java API を使用した DDX ドキュメントの動的な作成](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-dynamically-creating-a-ddx-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Web サービス API を使用した DDX ドキュメントの動的な作成 {#dynamically-create-a-ddx-document-using-the-web-service-api}

Assembler サービス API（web サービス）を使用して、DDX ドキュメントを動的に作成し、PDF ドキュメントをディスアセンブリします。

1. プロジェクトファイルを含めます。

   MTOM を使用する Microsoft .NET プロジェクトを作成します。サービスリファレンスを設定する際は、WSDL の定義 `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1` を必ず使用してください。 

   >[!NOTE]
   >
   >`localhost` を、AEM Forms をホストするサーバーの IP アドレスに置き換えます。

1. PDF Assembler クライアントを作成します。

   * デフォルトのコンストラクターを使用して、`AssemblerServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して、`AssemblerServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/AssemblerService?blob=mtom`）。`lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。
   * `AssemblerServiceClient.Endpoint.Binding` フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` フィールドを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `AssemblerServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `AssemblerServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
      * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` をフィールド `BasicHttpBindingSecurity.Security.Mode` に割り当てます。

1. DDX ドキュメントを作成します。

   * コンストラクターを使用して `System.Xml.XmlElement` オブジェクトを作成します。
   * `XmlElement` オブジェクトの `CreateElement` メソッドを呼び出して、DDX ドキュメントのルート要素を作成します。このメソッドは、 ルート要素を表す `Element` オブジェクトを作成します。 要素の名前を表す文字列値を `CreateElement` メソッドに渡します。 `SetAttribute` メソッドを呼び出して、DDX 要素の値を設定します。最後に、 `XmlElement` オブジェクトの `AppendChild` メソッドを呼び出して、DDX ドキュメントに要素を追加します。DDX オブジェクトを引数として渡します。 次のコード行は、このアプリケーションロジックを示しています。

      ` System.Xml.XmlElement root = ddx.CreateElement("DDX");  root.SetAttribute("xmlns", "https://ns.adobe.com/DDX/1.0/");  ddx.AppendChild(root);`

   * `XmlElement` オブジェクトの `CreateElement` メソッドを呼び出して、DDX ドキュメント `PDFsFromBookmarks` 要素を作成します。 要素の名前を表す文字列値を `CreateElement` メソッドに渡します。 次に、 `SetAttribute` メソッドを呼び出して、要素の値を設定します。`DDX` 要素の `AppendChild` メソッドを呼び出して、`PDFsFromBookmarks` 要素をルート要素に追加します。`PDFsFromBookmarks` 要素オブジェクトを引数として渡します。 次のコード行は、このアプリケーションロジックを示しています。

      ` XmlElement PDFsFromBookmarks = ddx.CreateElement("PDFsFromBookmarks");  PDFsFromBookmarks.SetAttribute("prefix", "stmt");  root.AppendChild(PDFsFromBookmarks);`

   * `XmlElement` オブジェクトの `CreateElement` メソッドを呼び出して、DDX ドキュメント `PDF` 要素を作成します。 要素の名前を表す文字列値を `CreateElement` メソッドに渡します。 次に、 `SetAttribute` メソッドを呼び出して、子要素の値を設定します。`PDFsFromBookmarks` 要素の `AppendChild` メソッドを呼び出して、`PDF` 要素を `PDFsFromBookmarks` 要素に追加します。`PDF` 要素オブジェクトを引数として渡します。 次のコード行に、このアプリケーションロジックを示します。

      ` XmlElement PDF = ddx.CreateElement("PDF");  PDF.SetAttribute("source", "AssemblerResultPDF.pdf");  PDFsFromBookmarks.AppendChild(PDF);`

1. DDX ドキュメントを変換します。

   * コンストラクターを使用して `System.IO.MemoryStream` オブジェクトを作成します。
   * DDX ドキュメントを表す `XmlElement` オブジェクトを使った DDX ドキュメントで、`MemoryStream` オブジェクトを入力します。`XmlElement` オブジェクトの `Save` メソッドを呼び出し、`MemoryStream` オブジェクトを渡します。
   * バイト配列を作成し、 `MemoryStream` オブジェクトにあるデータを入力します。次のコードは、このアプリケーションロジックを示しています。

      ` int bufLen = Convert.ToInt32(stream.Length);  byte[] byteArray = new byte[bufLen];  stream.Position = 0;  int count = stream.Read(byteArray, 0, bufLen);`

   * `BLOB` オブジェクトを作成します。バイト配列を `BLOB` オブジェクトの `MTOM` フィールドに割り当てます。

1. 分割する PDF ドキュメントを参照します。

   * コンストラクターを使用して `BLOB` オブジェクトを作成します。`BLOB` オブジェクトは、入力 PDF ドキュメントを格納するために使用します。 この `BLOB` オブジェクトは引数として `invokeOneDocument` に渡されます。
   * コンストラクターを呼び出して、`System.IO.FileStream` オブジェクトを作成します。入力 PDF ドキュメントのファイルの場所と、ファイルを開くモードを表す文字列値を渡します。
   * `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することで、バイト配列のサイズを決定できます。
   * `System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出し、読み込むバイト配列、開始位置、ストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * `MTOM` プロパティを割り当てて、`BLOB` オブジェクトにバイト配列の内容を入力します。

1. 実行時オプションを設定します。

   * ランタイムオプションを格納する `AssemblerOptionSpec` オブジェクトをコンストラクタで作成します。
   * `AssemblerOptionSpec` オブジェクトに属するデータメンバーに値を割り当てることで、ビジネス要件に応じたランタイムオプションを設定します。例えば、エラーが発生時にジョブの処理を続行するように Assembler サービスに指示するには、 `false` を `AssemblerOptionSpec` オブジェクトの `failOnError` データメンバーに割り当てます。

1. PDF ドキュメントを分割します。

   `AssemblerServiceClient` オブジェクトの `invokeDDX` メソッドを呼び出して、次の値を渡します。

   * 動的に作成された DDX ドキュメントを表す `BLOB` オブジェクト
   * 入力 PDF ドキュメントを含む `mapItem` 配列
   * 実行時オプションを指定する `AssemblerOptionSpec` オブジェクト

   `invokeDDX` メソッドは、ジョブの結果と発生した例外を含む `AssemblerResult` オブジェクトを返します。

1. 分割した PDF ドキュメントを保存します。

   新しく作成した PDF ドキュメントを取得するには、次の操作を実行します。

   * `AssemblerResult` オブジェクトの `documents` フィールド（ディスアセンブリされた PDF ドキュメントを含む `Map` オブジェクト）にアクセスします。
   * `Map`オブジェクトを反復処理して、各結果ドキュメントを取得します。次に、その配列メンバーの`value`を`BLOB`にキャストします。
   * `BLOB`オブジェクトの`MTOM`プロパティにアクセスして、PDF ドキュメントを表すバイナリデータを抽出します。これにより、PDF ファイルに書き出すことができるバイト配列が返されます。

**関連トピック**

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
