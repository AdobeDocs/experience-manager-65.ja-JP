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


# DDXドキュメントの動的な作成 {#dynamically-creating-ddx-documents}

Assembler操作の実行に使用できるDDXドキュメントを動的に作成できます。 DDXドキュメントを動的に作成すると、実行時に取得したDDXドキュメントの値を使用できます。 DDXドキュメントを動的に作成するには、使用しているプログラミング言語に属するクラスを使用します。 例えば、Javaを使用してクライアントアプリケーションを開発する場合は、 `org.w3c.dom.*`パッケージに属するクラスを使用します。 同様に、Microsoft .NETを使用している場合は、 `System.Xml` 名前空間に属するクラスを使用します。

DDXドキュメントをAssemblerサービスに渡す前に、XMLをインスタンスからイ `org.w3c.dom.Document` ンスタンスに変換し `com.adobe.idp.Document` ます。 Webサービスを使用している場合は、XMLの作成に使用したデータ型(例えば、 `XmlDocument`)のXMLを `BLOB` インスタンスに変換します。

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
>For more information about the Assembler service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>DDXドキュメントについて詳しくは、『 [Assembler Service and DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63)』を参照してください。

## 手順の概要 {#summary-of-steps}

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

使用しているプログラミング言語を使用して、DDXドキュメントを作成します。 PDF要素をディスアセンブリするDDXドキュメントを作成するには、ドキュメントに `PDFsFromBookmarks` 要素が含まれていることを確認します。 Java APIを使用している場合、DDXドキュメントの作成に使用するデータタイプを `com.adobe.idp.Document` インスタンスに変換します。 Webサービスを使用している場合は、データ型を `BLOB` インスタンスに変換します。

**DDXドキュメントの変換**

クラスを使用して作成されたDDXドキュメントは、 `org.w3c.dom` オブジェクトに変換する必要があり `com.adobe.idp.Document` ます。 Java APIを使用する場合にこのタスクを実行するには、Java XML変換クラスを使用します。 Webサービスを使用している場合は、DDXドキュメントを `BLOB` オブジェクトに変換します。

**PDFドキュメントの参照によるディスアセンブリ**

PDFドキュメントをディスアセンブリするには、ディスアセンブリするPDFドキュメントを表すPDFファイルを参照します。 Assemblerサービスに渡されると、ドキュメント内のレベル1のブックマークごとに個別のPDFドキュメントが返されます。

**実行時オプションの設定**

ジョブの実行中にAssemblerサービスの動作を制御する実行時オプションを設定できます。 例えば、エラーが発生した場合にジョブの処理を続行するようAssemblerサービスに指示するオプションを設定できます。 実行時オプションを設定するには、 `AssemblerOptionSpec` オブジェクトを使用します。

**PDFドキュメントのディスアセンブリ**

操作を呼び出して、PDFドキュメントをディスアセンブリ `invokeDDX` します。 動的に作成されたDDXドキュメントを渡します。 Assemblerサービスは、コレクションオブジェクト内で分解されたPDFドキュメントを返します。

**アセンブル解除されたPDFドキュメントの保存**

分解されたすべてのPDFドキュメントは、コレクションオブジェクト内で返されます。 コレクションオブジェクトを繰り返し処理し、各PDFドキュメントをPDFファイルとして保存します。

**関連トピック**

[Java APIを使用したDDXドキュメントの動的な作成](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-java-api)

[WebサービスAPIを使用したDDXドキュメントの動的な作成](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[プログラムによるPDFドキュメントのディスアセンブリ](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## Java APIを使用したDDXドキュメントの動的な作成 {#dynamically-create-a-ddx-document-using-the-java-api}

DDXドキュメントを動的に作成し、Assembler Service API(Java)を使用してPDFドキュメントをディスアセンブリします。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-assembler-client.jarなどのクライアントJARファイルを含めます。

1. PDFアセンブラクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `AssemblerServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. DDXドキュメントを作成します

   * クラスのメソッドを呼び出して、Java `DocumentBuilderFactory` オブジェクトを作成し `DocumentBuilderFactory` ま `newInstance` す。
   * オブジェクトの `DocumentBuilder` メソッドを呼び出して、Java `DocumentBuilderFactory``newDocumentBuilder` オブジェクトを作成します。
   * オブジェクトの `DocumentBuilder` メソッドを呼び出して、オブジ `newDocument``org.w3c.dom.Document` ェクトをインスタンス化します。
   * オブジェクトのメソッドを呼び出して、DDXドキュメントのル `org.w3c.dom.Document` ートエレメントを作成し `createElement` ます。 このメソッドは、ルート要素を表す `Element` オブジェクトを作成します。 要素の名前を表すstring値を `createElement` メソッドに渡します。 戻り値を `Element` にキャストします。次に、子要素の `setAttribute` メソッドを呼び出して、子要素の値を設定します。 最後に、ヘッダー要素の `appendChild` メソッドを呼び出して要素をヘッダー要素に追加し、子要素オブジェクトを引数として渡します。 次のコード行に、このアプリケーションロジックを示します。
      ` Element root = (Element)document.createElement("DDX");  root.setAttribute("xmlns","https://ns.adobe.com/DDX/1.0/");  document.appendChild(root);`

   * オブジェクトの `PDFsFromBookmarks` メソッドを呼び出して、 `Document` 要素を作成し `createElement` ます。 要素の名前を表すstring値を `createElement` メソッドに渡します。 戻り値を `Element` にキャストします。要素の `PDFsFromBookmarks``setAttribute` メソッドを呼び出して、要素の値を設定します。 DDX要素の `PDFsFromBookmarks` メソッドを呼び出して、 `DDX``appendChild` 要素に要素を追加します。 要素オブジェクトを引数として渡し `PDFsFromBookmarks` ます。 次のコード行に、このアプリケーションロジックを示します。

      ` Element PDFsFromBookmarks = (Element)document.createElement("PDFsFromBookmarks");  PDFsFromBookmarks.setAttribute("prefix","stmt");  root.appendChild(PDFsFromBookmarks);`

   * オブジェクトの `PDF` メソッドを呼び出して、 `Document` 要素を作成し `createElement` ます。 要素名を表すstring値を渡します。 戻り値を `Element` にキャストします。要素の `PDF``setAttribute` メソッドを呼び出して、要素の値を設定します。 要素の `PDF` メソッドを呼び出して、要素 `PDFsFromBookmarks` を `PDFsFromBookmarks``appendChild` 要素に追加します。 要素オブジェクトを引数として渡し `PDF` ます。 次のコード行に、このアプリケーションロジックを示します。

      ` Element PDF = (Element)document.createElement("PDF");  PDF.setAttribute("source","AssemblerResultPDF.pdf");  PDFsFromBookmarks.appendChild(PDF);`

1. DDXドキュメントを変換します。

   * オブジェクトのスタティック `javax.xml.transform.Transformer` メソッドを呼び出して、 `javax.xml.transform.Transformer``newInstance` オブジェクトを作成します。
   * オブジェクトの `Transformer` メソッドを呼び出して、 `TransformerFactory` オブジェクトを作成 `newTransformer` します。
   * コンストラクタを使用して `ByteArrayOutputStream` オブジェクトを作成します。
   * コンストラクタを使用して `javax.xml.transform.dom.DOMSource` オブジェクトを作成します。DDXドキュメントを表す `org.w3c.dom.Document` オブジェクトを渡します。
   * コンストラクタを使用して `javax.xml.transform.dom.DOMSource` オブジェクトを渡すことによって、`ByteArrayOutputStream` オブジェクトを作成します。
   * オブジェクトの `ByteArrayOutputStream` メソッドを呼び出して、Java `javax.xml.transform.Transformer``transform` オブジェクトを入力します。 お `javax.xml.transform.dom.DOMSource` よびオブジェクトを渡 `javax.xml.transform.stream.StreamResult` します。
   * バイト配列を作成し、 `ByteArrayOutputStream` オブジェクトのサイズをバイト配列に割り当てます。
   * オブジェクトのメソッドを呼び出して、 `ByteArrayOutputStream` バイト配列を設定し `toByteArray` ます。
   * Create a `com.adobe.idp.Document` object by using its constructor and passing the byte array.

1. ディスアセンブリするPDFドキュメントの参照

   * コンストラクターを使用して、入力PDFドキュメントの格納に使用する `java.util.Map` オブジェクトを作成し `HashMap` ます。
   * コンストラクターを使用し、ディスアセンブリするPDFドキュメントの場所を渡して、 `java.io.FileInputStream` オブジェクトを作成します。
   * Create a `com.adobe.idp.Document` object. ディスアセンブリするPDFドキュメントを含む `java.io.FileInputStream` オブジェクトを渡します。
   * メソッド追加を呼び出し、次の引数を渡すことによって、オブジェクトに対するエントリを作成します。 `java.util.Map``put`

      * キー名を表すstring値です。 この値は、DDXドキュメントで指定されたPDFソース要素の値と一致する必要があります。 (動的に作成されるDDXドキュメントでは、値はです `AssemblerResultPDF.pdf`)。
      * ディスアセンブリするPDFドキュメントを含む `com.adobe.idp.Document` オブジェクトです。

1. 実行時オプションを設定します。

   * コンストラクターを使用して、実行時のオプションを格納する `AssemblerOptionSpec` オブジェクトを作成します。
   * オブジェクトに属するメソッドを呼び出して、ビジネス要件に合うように実行時オプションを設定し `AssemblerOptionSpec` ます。 例えば、エラーが発生した場合にジョブの処理を続行するようにAssemblerサービスに指示するには、 `AssemblerOptionSpec` オブジェクトの `setFailOnError` メソッドを呼び出して渡し `false`ます。

1. PDFドキュメントのディスアセンブリ

   オブジェクトの `AssemblerServiceClient``invokeDDX` メソッドを呼び出し、次の値を渡します。

   * 動的に作成されるDDXドキュメントを表す `com.adobe.idp.Document` オブジェクトです
   * ディスアセンブリするPDFドキュメントを含む `java.util.Map` オブジェクト
   * デフォルトフォントやジョブログレベルなど、実行時のオプションを指定する `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` オブジェクト。

   この `invokeDDX` メソッドは、分解されたPDFドキュメントと発生した例外が含まれる `com.adobe.livecycle.assembler.client.AssemblerResult` オブジェクトを返します。

1. アセンブル解除されたPDFドキュメントを保存します。

   ディスアセンブリされたPDFドキュメントを取得するには、次の操作を実行します。

   * オブジェクトの `AssemblerResult` メソッドを呼び出し `getDocuments` ます。 このメソッドは、 `java.util.Map` オブジェクトを返します。
   * オブジェクトを繰り返し処理して、結果のオブジ `java.util.Map``com.adobe.idp.Document` ェクトを見つけます。
   * オブジェクトの `com.adobe.idp.Document``copyToFile` メソッドを呼び出してPDFドキュメントを抽出します。

**関連トピック**

[クイック開始（SOAPモード）: Java APIを使用したDDXドキュメントの動的な作成](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-dynamically-creating-a-ddx-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## WebサービスAPIを使用したDDXドキュメントの動的な作成 {#dynamically-create-a-ddx-document-using-the-web-service-api}

DDXドキュメントを動的に作成し、Assembler Service API（Webサービス）を使用してPDFドキュメントをディスアセンブリします。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 サービス参照を設定する際は、次のWSDL定義を使用してください。 `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >サーバーホスト `localhost` AEM FormsのIPアドレスに置き換えます。

1. PDFアセンブラクライアントを作成します。

   * デフォルトのコンストラクターを使用して `AssemblerServiceClient` オブジェクトを作成します。
   * コンストラクターを使用して `AssemblerServiceClient.Endpoint.Address` オブジェクトを作成し `System.ServiceModel.EndpointAddress` ます。 WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/AssemblerService?blob=mtom`)に渡すstring値を渡します。 属性を使用する必要はありません `lc_version` 。 この属性は、サービス参照を作成する際に使用されます。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `AssemblerServiceClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールドにAEM formsのユーザー名を割り当て `AssemblerServiceClient.ClientCredentials.UserName.UserName`ます。
      * 対応するパスワード値をフィールドに割り当て `AssemblerServiceClient.ClientCredentials.UserName.Password`ます。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当て `BasicHttpBindingSecurity.Security.Mode`ます。

1. DDXドキュメントを作成します

   * コンストラクタを使用して `System.Xml.XmlElement` オブジェクトを作成します。
   * オブジェクトのメソッドを呼び出して、DDXドキュメントのル `XmlElement` ートエレメントを作成し `CreateElement` ます。 このメソッドは、ルート要素を表す `Element` オブジェクトを作成します。 要素の名前を表すstring値を `CreateElement` メソッドに渡します。 DDX要素の `SetAttribute` メソッドを呼び出して、その値を設定します。 最後に、 `XmlElement` オブジェクトのメソッドを呼び出して、DDXドキュメントに要素を追加し `AppendChild` ます。 DDXオブジェクトを引数として渡します。 次のコード行に、このアプリケーションロジックを示します。

      ` System.Xml.XmlElement root = ddx.CreateElement("DDX");  root.SetAttribute("xmlns", "https://ns.adobe.com/DDX/1.0/");  ddx.AppendChild(root);`

   * オブジェクトの `PDFsFromBookmarks` メソッドを呼び出して、DDXドキュメントの `XmlElement``CreateElement` 要素を作成します。 要素の名前を表すstring値を `CreateElement` メソッドに渡します。 次に、その `SetAttribute` メソッドを呼び出して、要素の値を設定します。 要素の `PDFsFromBookmarks` メソッドを呼び出して、ルート要素に `DDX` 要素を追加し `AppendChild` ます。 要素オブジェクトを引数として渡し `PDFsFromBookmarks` ます。 次のコード行に、このアプリケーションロジックを示します。

      ` XmlElement PDFsFromBookmarks = ddx.CreateElement("PDFsFromBookmarks");  PDFsFromBookmarks.SetAttribute("prefix", "stmt");  root.AppendChild(PDFsFromBookmarks);`

   * オブジェクトの `PDF` メソッドを呼び出して、DDXドキュメントの `XmlElement``CreateElement` 要素を作成します。 要素の名前を表すstring値を `CreateElement` メソッドに渡します。 次に、子要素の `SetAttribute` メソッドを呼び出して、子要素の値を設定します。 要素の `PDF` メソッドを呼び出して、要素 `PDFsFromBookmarks` を `PDFsFromBookmarks``AppendChild` 要素に追加します。 要素オブジェクトを引数として渡し `PDF` ます。 次のコード行に、このアプリケーションロジックを示します。

      ` XmlElement PDF = ddx.CreateElement("PDF");  PDF.SetAttribute("source", "AssemblerResultPDF.pdf");  PDFsFromBookmarks.AppendChild(PDF);`

1. DDXドキュメントを変換します。

   * コンストラクタを使用して `System.IO.MemoryStream` オブジェクトを作成します。
   * DDXドキュメントを表す `MemoryStream` オブジェクトを使用して、DDXドキュメントで `XmlElement` オブジェクトを設定します Invoke the `XmlElement` object’s `Save` method and pass the `MemoryStream` object.
   * バイト配列を作成し、 `MemoryStream` オブジェクト内のデータを入力します。 次のコードは、このアプリケーションロジックを示しています。

      ` int bufLen = Convert.ToInt32(stream.Length);  byte[] byteArray = new byte[bufLen];  stream.Position = 0;  int count = stream.Read(byteArray, 0, bufLen);`

   * Create a `BLOB` object. バイト配列を `BLOB` オブジェクトの `MTOM` フィールドに割り当てます。

1. ディスアセンブリするPDFドキュメントの参照

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、入力PDFドキュメントの保存に使用されます。 この `BLOB` オブジェクトは、引数としてに渡 `invokeOneDocument` されます。
   * Create a `System.IO.FileStream` object by invoking its constructor. 入力PDFドキュメントーのファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
   * オブジェクトの `System.IO.FileStream``Read` メソッドを呼び出し、読み取るバイト配列、開始位置およびストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * オブジェクトのプロパティにバイト配列の内容を割り当てて、 `BLOB``MTOM` オブジェクトを入力します。

1. 実行時オプションを設定します。

   * コンストラクターを使用して、実行時のオプションを格納する `AssemblerOptionSpec` オブジェクトを作成します。
   * オブジェクトに属するデータメンバに値を割り当てることで、ビジネス要件に合った実行時オプションを設定し `AssemblerOptionSpec` ます。 例えば、エラーが発生した場合にジョブの処理を続行するようにAssemblerサービスに指示するには、 `false` オブジェクトの `AssemblerOptionSpec``failOnError` データメンバーに割り当てます。

1. PDFドキュメントのディスアセンブリ

   オブジェクトの `AssemblerServiceClient``invokeDDX` メソッドを呼び出し、次の値を渡します。

   * 動的に作成されるDDXドキュメントを表す `BLOB` オブジェクトです
   * 入力PDFドキュメントを含む `mapItem` 配列
   * 実行時オプションを指定する `AssemblerOptionSpec` オブジェクトです。

   この `invokeDDX` メソッドは、ジョブの結果と発生した例外を含む `AssemblerResult` オブジェクトを返します。

1. アセンブル解除されたPDFドキュメントを保存します。

   新しく作成されたPDFドキュメントを取得するには、次の操作を実行します。

   * オブジェクトの `AssemblerResult` フィールドにアクセスします。この `documents` フィールドは、分解されたPDFドキュメントを含む `Map` オブジェクトです。
   * オブジェクトを繰り返し処理して、 `Map` 各結果ドキュメントを取得します。 次に、その配列メンバーをにキャスト `value` し `BLOB`ます。
   * PDFドキュメントを表すバイナリデータを抽出するには、その `BLOB` オブジェクトの `MTOM` プロパティにアクセスします。 PDFファイルに書き出すことができるバイトの配列を返します。

**関連トピック**

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
