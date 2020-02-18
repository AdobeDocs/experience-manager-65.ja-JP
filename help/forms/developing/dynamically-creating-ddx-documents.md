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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# DDXドキュメントの動的な作成 {#dynamically-creating-ddx-documents}

Assembler操作の実行に使用できるDDXドキュメントを動的に作成できます。 DDXドキュメントを動的に作成すると、実行時に取得したDDXドキュメントの値を使用できます。 DDXドキュメントを動的に作成するには、使用しているプログラミング言語に属するクラスを使用します。 例えば、Javaを使用してクライアントアプリケーションを開発する場合は、パッケージに属するクラスを使用 `org.w3c.dom.*`します。 同様に、Microsoft .NETを使用している場合は、名前空間に属するクラスを使用し `System.Xml` ます。

DDXドキュメントをAssemblerサービスに渡す前に、XMLをインスタンスからインスタンスに変 `org.w3c.dom.Document` 換してくだ `com.adobe.idp.Document` さい。 Webサービスを使用している場合は、XMLの作成に使用したデータ型(例えば、 `XmlDocument`)からインスタンスにXMLを変換し `BLOB` ます。

この説明では、次のDDXドキュメントが動的に作成されると仮定します。

```as3
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

このDDXドキュメントは、PDFドキュメントを分解します。 PDFドキュメントのディスアセンブリについて詳しくあることをお勧めします。

>[!NOTE]
>
>For more information about the Assembler service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>DDXドキュメントについて詳しくは、 [Assembler Service and DDX Referenceを参照してください](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 手順の概要 {#summary-of-steps}

動的に作成されたDDXドキュメントを使用してPDFドキュメントをディスアセンブリするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. PDFアセンブラクライアントを作成します。
1. DDXドキュメントを作成します。
1. DDXドキュメントを変換します。
1. 実行時オプションを設定します。
1. PDFドキュメントのディスアセンブリ
1. 分解されたPDFドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar（AEM FormsがJBossにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsをJBossにデプロイする場合に必要）

**PDFアセンブラクライアントの作成**

プログラムによってAssembler操作を実行する前に、Assemblerサービスクライアントを作成します。

**DDXドキュメントの作成**

使用しているプログラミング言語を使用してDDXドキュメントを作成します。 PDFドキュメントをディスアセンブリするDDXドキュメントを作成するには、そのドキュメントに要素が含まれていることを確認 `PDFsFromBookmarks` します。 Java APIを使用している場合は、DDXドキュメントの作成に使用する `com.adobe.idp.Document` データ型をインスタンスに変換します。 Webサービスを使用している場合は、データ型をインスタンスに変換し `BLOB` ます。

**DDXドキュメントの変換**

クラスを使用して作成されたDDXドキュメントは、 `org.w3c.dom` オブジェクトに変換する必要があ `com.adobe.idp.Document` ります。 Java APIを使用する場合にこのタスクを実行するには、Java XML変換クラスを使用します。 Webサービスを使用している場合は、DDXドキュメントをオブジェクトに変換 `BLOB` します。

**ディスアセンブリするPDFドキュメントの参照**

PDFドキュメントをディスアセンブリするには、ディスアセンブリ対象のPDFドキュメントを表すPDFファイルを参照します。 Assemblerサービスに渡されると、ドキュメント内のレベル1のブックマークごとに別々のPDFドキュメントが返されます。

**実行時オプションの設定**

ジョブの実行中にAssemblerサービスの動作を制御する実行時オプションを設定できます。 例えば、エラーが発生した場合にジョブの処理を続行するようAssemblerサービスに指示するオプションを設定できます。 実行時オプションを設定するには、オブジェクトを使用 `AssemblerOptionSpec` します。

**PDFドキュメントのディスアセンブリ**

操作を呼び出して、PDFドキュメントをディスアセンブリ `invokeDDX` します。 動的に作成されたDDXドキュメントを渡します。 Assemblerサービスは、コレクションオブジェクト内で分解されたPDFドキュメントを返します。

**分解されたPDFドキュメントの保存**

分解されたすべてのPDFドキュメントは、コレクションオブジェクト内で返されます。 コレクションオブジェクトを繰り返し処理し、各PDFドキュメントをPDFファイルとして保存します。

**関連トピック**

[Java APIを使用したDDXドキュメントの動的な作成](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-java-api)

[WebサービスAPIを使用したDDXドキュメントの動的な作成](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDFドキュメントのプログラムによるディスアセンブリ](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## Java APIを使用したDDXドキュメントの動的な作成 {#dynamically-create-a-ddx-document-using-the-java-api}

Assembler Service API(Java)を使用して、DDXドキュメントを動的に作成し、PDFドキュメントをディスアセンブリします。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-assembler-client.jarなどのクライアントJARファイルを含めます。

1. PDFアセンブラクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `AssemblerServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. DDXドキュメントを作成します。

   * クラスのメソッド `DocumentBuilderFactory` を呼び出して、Javaオブジ `DocumentBuilderFactory` ェクトを作成 `newInstance` します。
   * オブジェクトのメ `DocumentBuilder` ソッドを呼び出して、Java `DocumentBuilderFactory` オブジェクトを作成 `newDocumentBuilder` します。
   * オブジェクトのメ `DocumentBuilder` ソッドを呼び出し `newDocument` て、オブジェクトをインスタンス化 `org.w3c.dom.Document` します。
   * オブジェクトのメソッドを呼び出して、DDXドキュメントのル `org.w3c.dom.Document` ート要素を作成 `createElement` します。 このメソッドは、ルート `Element` 要素を表すオブジェクトを作成します。 要素の名前を表すstring値をメソッドに渡し `createElement` ます。 戻り値を `Element` にキャストします。次に、そのメソッドを呼び出して、子要素の値を設定し `setAttribute` ます。 最後に、ヘッダー要素のメソッドを呼び出して要素をヘッダー要素に追加し、子要 `appendChild` 素オブジェクトを引数として渡します。 次のコード行に、このアプリケーションロジックを示します。
      ` Element root = (Element)document.createElement("DDX");  root.setAttribute("xmlns","https://ns.adobe.com/DDX/1.0/");  document.appendChild(root);`

   * オブジェクト `PDFsFromBookmarks` のメソッドを呼び出して、 `Document` 要素を作成 `createElement` します。 要素の名前を表すstring値をメソッドに渡し `createElement` ます。 戻り値を `Element` にキャストします。要素のメソッドを呼び出し `PDFsFromBookmarks` て、要素の値を設定し `setAttribute` ます。 DDX要素の `PDFsFromBookmarks` メソッドを呼 `DDX` び出して、要素を要素に追加し `appendChild` ます。 要素オブジェクト `PDFsFromBookmarks` を引数として渡します。 次のコード行に、このアプリケーションロジックを示します。

      ` Element PDFsFromBookmarks = (Element)document.createElement("PDFsFromBookmarks");  PDFsFromBookmarks.setAttribute("prefix","stmt");  root.appendChild(PDFsFromBookmarks);`

   * オブジェクト `PDF` のメソッドを呼び出して、 `Document` 要素を作成 `createElement` します。 要素名を表すstring値を渡します。 戻り値を `Element` にキャストします。要素のメソッドを呼び出し `PDF` て、要素の値を設定し `setAttribute` ます。 要素のメ `PDF` ソッドを呼び `PDFsFromBookmarks` 出して、要素 `PDFsFromBookmarks` を要素に追加し `appendChild` ます。 要素オブジェクト `PDF` を引数として渡します。 次のコード行に、このアプリケーションロジックを示します。

      ` Element PDF = (Element)document.createElement("PDF");  PDF.setAttribute("source","AssemblerResultPDF.pdf");  PDFsFromBookmarks.appendChild(PDF);`

1. DDXドキュメントを変換します。

   * オブジェクト `javax.xml.transform.Transformer` の静的メソッドを呼び出し `javax.xml.transform.Transformer` て、オブジェクトを作成 `newInstance` します。
   * オブジェクト `Transformer` のメソッドを呼び出して、オ `TransformerFactory` ブジェクトを作成 `newTransformer` します。
   * コンストラクタを使用して `ByteArrayOutputStream` オブジェクトを作成します。
   * コンストラクタを使用して `javax.xml.transform.dom.DOMSource` オブジェクトを作成します。DDXドキュメント `org.w3c.dom.Document` を表すオブジェクトを渡します。
   * コンストラクタを使用して `javax.xml.transform.dom.DOMSource` オブジェクトを渡すことによって、`ByteArrayOutputStream` オブジェクトを作成します。
   * オブジェクトのメ `ByteArrayOutputStream` ソッドを呼び出して、Java `javax.xml.transform.Transformer` オブジェクトを設定 `transform` します。 オブジェクトとオ `javax.xml.transform.dom.DOMSource` ブジェクトを渡 `javax.xml.transform.stream.StreamResult` します。
   * バイト配列を作成し、オブジェクトのサイズをバ `ByteArrayOutputStream` イト配列に割り当てます。
   * オブジェクトのメソッドを呼び出して、バ `ByteArrayOutputStream` イト配列を設定 `toByteArray` します。
   * Create a `com.adobe.idp.Document` object by using its constructor and passing the byte array.

1. ディスアセンブリするPDFドキュメントを参照します。

   * コンストラク `java.util.Map` ターを使用して、入力PDFドキュメントの保存に使用するオブジェクトを作成 `HashMap` します。
   * コンストラク `java.io.FileInputStream` ターを使用し、ディスアセンブリするPDFドキュメントの場所を渡して、オブジェクトを作成します。
   * Create a `com.adobe.idp.Document` object. ディスアセンブリ `java.io.FileInputStream` するPDFドキュメントを含むオブジェクトを渡します。
   * メソッドを呼び出し、次 `java.util.Map` の引数を渡して、オ `put` ブジェクトにエントリを追加します。

      * キー名を表すstring値です。 この値は、DDXドキュメントで指定されたPDFソース要素の値と一致する必要があります。 (動的に作成されるDDXドキュメントでは、値は `AssemblerResultPDF.pdf`です。)
      * ディスア `com.adobe.idp.Document` センブルするPDFドキュメントを含むオブジェクトです。

1. 実行時オプションを設定します。

   * コンストラクタ `AssemblerOptionSpec` ーを使用して、実行時のオプションを格納するオブジェクトを作成します。
   * オブジェクトに属するメソッドを呼び出して、ビジネス要件に合わせて実行時のオプションを設定 `AssemblerOptionSpec` します。 例えば、エラーが発生した場合にジョブの処理を続行するようにAssemblerサービスに指示するには、オブジェクトのメソッド `AssemblerOptionSpec` を呼び出して `setFailOnError` 渡してくださ `false`い。

1. PDFドキュメントのディスアセンブリ

   オブジェクト `AssemblerServiceClient` のメソッドを `invokeDDX` 呼び出し、次の値を渡します。

   * 動的に `com.adobe.idp.Document` 作成されたDDXドキュメントを表すオブジェクト
   * ディスア `java.util.Map` センブルするPDFドキュメントを含むオブジェクト
   * デフォ `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` ルトフォントやジョブログレベルなど、実行時のオプションを指定するオブジェクトです
   このメソ `invokeDDX` ッドは、分解さ `com.adobe.livecycle.assembler.client.AssemblerResult` れたPDFドキュメントと発生した例外を含むオブジェクトを返します。

1. 分解されたPDFドキュメントを保存します。

   分解されたPDFドキュメントを取得するには、次の操作を実行します。

   * オブジェクト `AssemblerResult` のメソッドを呼び出 `getDocuments` します。 このメソッドは、オブジェクトを `java.util.Map` 返します。
   * 結果のオブジェクト `java.util.Map` が見つかるまで、オブジェクトを繰り返 `com.adobe.idp.Document` します。
   * オブジェクト `com.adobe.idp.Document` のメソッドを呼 `copyToFile` び出してPDFドキュメントを抽出します。

**関連トピック**

[クイックスタート（SOAPモード）:Java APIを使用したDDXドキュメントの動的な作成](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-dynamically-creating-a-ddx-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## WebサービスAPIを使用したDDXドキュメントの動的な作成 {#dynamically-create-a-ddx-document-using-the-web-service-api}

Assembler Service API（Webサービス）を使用して、DDXドキュメントを動的に作成し、PDFドキュメントをディスアセンブリします。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 サービス参照を設定する際は、必ず次のWSDL定義を使用してください。 `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. PDFアセンブラクライアントを作成します。

   * デフォルトのコンス `AssemblerServiceClient` トラクターを使用して、オブジェクトを作成します。
   * コンストラクタ `AssemblerServiceClient.Endpoint.Address` ーを使用してオブジェクトを作 `System.ServiceModel.EndpointAddress` 成します。 WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/AssemblerService?blob=mtom`)に渡すstring値。 属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `AssemblerServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `AssemblerServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `AssemblerServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. DDXドキュメントを作成します。

   * コンストラクタを使用して `System.Xml.XmlElement` オブジェクトを作成します。
   * オブジェクトのメソッドを呼び出して、DDXドキュメントのル `XmlElement` ート要素を作成 `CreateElement` します。 このメソッドは、ルート `Element` 要素を表すオブジェクトを作成します。 要素の名前を表すstring値をメソッドに渡し `CreateElement` ます。 DDX要素のメソッドを呼び出して、その値を設定し `SetAttribute` ます。 最後に、オブジェクトのメソッドを呼び出して、DDXドキュメント `XmlElement` に要素を追加 `AppendChild` します。 DDXオブジェクトを引数として渡します。 次のコード行に、このアプリケーションロジックを示します。

      ` System.Xml.XmlElement root = ddx.CreateElement("DDX");  root.SetAttribute("xmlns", "https://ns.adobe.com/DDX/1.0/");  ddx.AppendChild(root);`

   * オブジェクトのメソッドを呼び出し `PDFsFromBookmarks` て、DDXドキュメントの `XmlElement` エレメントを作成 `CreateElement` します。 要素の名前を表すstring値をメソッドに渡し `CreateElement` ます。 次に、そのメソッドを呼び出して、要素の値を設定し `SetAttribute` ます。 要素のメ `PDFsFromBookmarks` ソッドを呼び出して、ルート要素 `DDX` に要素を追加 `AppendChild` します。 要素オブジェクト `PDFsFromBookmarks` を引数として渡します。 次のコード行に、このアプリケーションロジックを示します。

      ` XmlElement PDFsFromBookmarks = ddx.CreateElement("PDFsFromBookmarks");  PDFsFromBookmarks.SetAttribute("prefix", "stmt");  root.AppendChild(PDFsFromBookmarks);`

   * オブジェクトのメソッドを呼び出し `PDF` て、DDXドキュメントの `XmlElement` エレメントを作成 `CreateElement` します。 要素の名前を表すstring値をメソッドに渡し `CreateElement` ます。 次に、そのメソッドを呼び出して、子要素の値を設定し `SetAttribute` ます。 要素のメ `PDF` ソッドを呼び `PDFsFromBookmarks` 出して、要素 `PDFsFromBookmarks` を要素に追加し `AppendChild` ます。 要素オブジェクト `PDF` を引数として渡します。 次のコード行に、このアプリケーションロジックを示します。

      ` XmlElement PDF = ddx.CreateElement("PDF");  PDF.SetAttribute("source", "AssemblerResultPDF.pdf");  PDFsFromBookmarks.AppendChild(PDF);`

1. DDXドキュメントを変換します。

   * コンストラクタを使用して `System.IO.MemoryStream` オブジェクトを作成します。
   * DDXドキュメント `MemoryStream` を表すオブジェクトを使用して、DDXドキュメ `XmlElement` ントでオブジェクトを設定します。 Invoke the `XmlElement` object’s `Save` method and pass the `MemoryStream` object.
   * バイト配列を作成し、オブジェクト内のデータを設定し `MemoryStream` ます。 次のコードは、このアプリケーションロジックを示しています。

      ` int bufLen = Convert.ToInt32(stream.Length);  byte[] byteArray = new byte[bufLen];  stream.Position = 0;  int count = stream.Read(byteArray, 0, bufLen);`

   * Create a `BLOB` object. バイト配列をオブジェクトのフィー `BLOB` ルドに割り当 `MTOM` てます。

1. ディスアセンブリするPDFドキュメントを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、入力PDFドキュメントの保存に使用されます。 このオ `BLOB` ブジェクトは、引数として `invokeOneDocument` に渡されます。
   * Create a `System.IO.FileStream` object by invoking its constructor. 入力PDFドキュメントのファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイト配列、開 `System.IO.FileStream` 始位置、ストリ `Read` ーム長を渡すことによって、バイト配列にストリームデータを設定します。
   * オブジェクトにバ `BLOB` イト配列の内容をプロ `MTOM` パティに割り当てて、オブジェクトを設定します。

1. 実行時オプションを設定します。

   * コンストラクタ `AssemblerOptionSpec` ーを使用して、実行時のオプションを格納するオブジェクトを作成します。
   * オブジェクトに属するデータメンバーに値を割り当てて、ビジネス要件に合わせて実行時オプションを設定 `AssemblerOptionSpec` します。 例えば、エラーが発生した場合にジョブの処理を続行するようAssemblerサービスに指示するには、オブジェクトの `false` データメ `AssemblerOptionSpec` ンバーに割り `failOnError` 当てます。

1. PDFドキュメントのディスアセンブリ

   オブジェクト `AssemblerServiceClient` のメソッドを `invokeDDX` 呼び出し、次の値を渡します。

   * 動的に `BLOB` 作成されたDDXドキュメントを表すオブジェクト
   * 入力PDF `mapItem` ドキュメントを含む配列
   * 実行時 `AssemblerOptionSpec` のオプションを指定するオブジェクト
   このメ `invokeDDX` ソッドは、ジョ `AssemblerResult` ブの結果と発生した例外を含むオブジェクトを返します。

1. 分解されたPDFドキュメントを保存します。

   新しく作成されたPDFドキュメントを取得するには、次の操作を実行します。

   * オブジェクトのフ `AssemblerResult` ィールドにアク `documents` セスします。このフィールドは、ア `Map` センブル解除されたPDFドキュメントを含むオブジェクトです。
   * オブジェクトを繰り返し `Map` 処理し、各結果ドキュメントを取得します。 次に、その配列メンバーをにキャス `value` トします `BLOB`。
   * PDFドキュメントを表すバイナリデータを抽出するには、そのオブジェクトのプロパ `BLOB` ティにアクセス `MTOM` します。 PDFファイルに書き出し可能なバイト配列を返します。

**関連トピック**

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
