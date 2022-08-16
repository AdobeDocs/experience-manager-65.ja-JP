---
title: プログラムによる PDF ドキュメントの分割
seo-title: Programmatically Disassembling PDF Documents
description: Assembler サービスを使用すると、Java API と web サービス API を使用して、1 つの PDF ドキュメントを複数の PDF ドキュメントに分割できます。
seo-description: Use the Assembler service to disassemble a single PDF document into multiple PDF documents using the Java API and the Web Service API.
uuid: d71cc044-e948-4b7a-b598-b041723b69e9
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8e38a597-5d22-4d83-95fe-4494fb04e4a3
role: Developer
exl-id: c5e712e0-5c3f-48cd-91cf-fd347222a6b2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1761'
ht-degree: 100%

---

# プログラムによる PDF ドキュメントの分割 {#programmatically-disassembling-pdf-documents}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

Assembler サービスに PDF ドキュメントを渡すことで、ドキュメントを分割できます。このタスクは、一般的に、PDF ドキュメントが最初に多数の個別ドキュメント（明細書一式など）から作成された場合に役立ちます。以下のイラストでは、DocA が複数の結果ドキュメントに分割されています。ページの初めの レベル 1 のブックマークで、新しい結果ドキュメントの開始が示されています。

![pd_pd_pdfsfrombookmarks](assets/pd_pd_pdfsfrombookmarks.png)

PDF ドキュメントを分割するには、`PDFsFromBookmarks` 要素が DDX ドキュメント内にある必要があります。`PDFsFromBookmarks` 要素は結果の要素であり、`DDX` 要素の子要素のみとすることができます。複数のドキュメントが生成される可能性があるため、`result` 属性はありません。

`PDFsFromBookmarks` 要素を使用すると、ソースドキュメントのレベル 1 のブックマークごとに 1 つのドキュメントが生成されます。

ここでは、以下の DDX ドキュメントが使用されていると仮定します。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

>[!NOTE]
>
>この節を読む前に、Assembler サービスを使用した PDF ドキュメントの組み立てを理解しておくことをお勧めします（[プログラムによる PDF ドキュメントの組み立て](/help/forms/developing/programmatically-assembling-pdf-documents.md)を参照してください）。

>[!NOTE]
>
>1 つの PDF ドキュメントを Assembler サービスに渡し、1 つのドキュメントを取得する場合、`invokeOneDocument` 操作を呼び出すことができます。ただし、PDF ドキュメントを分割するには、`invokeDDX` 操作を使用します。理由は、1 つの入力 PDF ドキュメントが Assembler サービスに渡されるのに対し、Assembler サービスは 1 つ以上のドキュメントを含むコレクションオブジェクトを返すからです。

>[!NOTE]
>
>Assembler サービスについて詳しくは、[AEM Forms サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

>[!NOTE]
>
>DDX ドキュメントについて詳しくは、[Assembler サービスと DDX リファレンス](https://www.adobe.com/go/learn_aemforms_ddx_63)を参照してください。

## 手順の概要 {#summary-of-steps}

PDF ドキュメントを分割するには、以下のタスクを実行します。

1. プロジェクトファイルを含めます。
1. PDF Assembler クライアントを作成します。
1. 既存の DDX ドキュメントを参照します。
1. 分割する PDF ドキュメントを参照します。
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

AEM Forms が JBoss 以外のサポート対象の J2EE アプリケーションサーバーにデプロイされている場合は、adobe-utilities.jar ファイルと jbossall-client.jar ファイルを、AEM Forms がデプロイされている J2EE アプリケーションサーバーに固有の JAR ファイルに置き換える必要があります。

**PDF Assembler クライアントを作成する**

Assembler 操作をプログラムで実行する前に、Assembler サービスクライアントを作成する必要があります。

**既存の DDX ドキュメントの参照**

PDF ドキュメントを分割するには、DDX ドキュメントを参照する必要があります。この DDX ドキュメントに `PDFsFromBookmarks` 要素を含める必要があります。

**分割する PDF ドキュメントの参照**

PDF ドキュメントを分割するには、分割する PDF ドキュメントを表す PDF ファイルを参照します。Assembler サービスに渡されると、その PDF ドキュメント内のレベル 1 のブックマークごとに別の PDF ドキュメントが返されます。

**実行時オプションの設定**

ジョブの実行中に Assembler サービスの動作を制御する実行時オプションを設定できます。例えば、エラーが発生した場合にジョブの処理を続行するよう Assembler サービスに指示するオプションを設定できます。

**PDF ドキュメントの分割**

Assembler サービスクライアントを作成し、DDX ドキュメントと分割する PDF ドキュメントを参照して、実行時オプションを設定すると、`invokeDDX` メソッドを呼び出して PDF ドキュメントを分割できます。DDX ドキュメントに PDF ドキュメントの分割手順が記載されている場合、Assembler サービスはコレクションオブジェクト内の分割された PDF ドキュメントを返します。

**分割した PDF ドキュメントを保存**

分割されたすべての PDF ドキュメントは、コレクションオブジェクト内で返されます。コレクションオブジェクトを反復処理し、各 PDF ドキュメントを PDF ファイルとして保存します。

**関連トピック**

[AEM Forms Java ライブラリファイルの組み込み](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDF ドキュメントをプログラムで組み立てる](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java API を使用した PDF ドキュメントの分割 {#disassemble-a-pdf-document-using-the-java-api}

Assembler サービス API（Java）を使用して PDF ドキュメントを分割します。

1. プロジェクトファイルを含めます。

   adobe-livecycle-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. PDF Assembler クライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して `ServiceClientFactory` オブジェクトを渡すことにより、`AssemblerServiceClient` オブジェクトを作成します。

1. 既存の DDX ドキュメントを参照します。

   * コンストラクタを使用し、DDX ファイルの場所を指定する文字列値を渡すことによって、その DDX ドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクターを使用して `java.io.FileInputStream` オブジェクトを渡し、`com.adobe.idp.Document` オブジェクトを作成します。

1. 分割する PDF ドキュメントを参照します。

   * `HashMap` コンストラクターを使って、入力 PDF ドキュメントを保存するために使用する `java.util.Map` オブジェクトを作成します。
   * コンストラクターを使用して、分割する PDF ドキュメントの場所を渡し、`java.io.FileInputStream` オブジェクトを作成します。
   * `com.adobe.idp.Document` オブジェクトを作成し、分割する PDF ドキュメントを含む `java.io.FileInputStream` オブジェクトを渡します。
   * エントリを `java.util.Map` オブジェクトに追加するには、`put` メソッドを呼び出して以下の引数を使用します。

      * キー名を表す文字列値。この値は、DDX ドキュメントで指定された PDF ソース要素の値と一致している必要があります。
      * 分割する PDF ドキュメントを含む `com.adobe.idp.Document` オブジェクト。

1. 実行時オプションを設定します。

   * コンストラクタを使用して、実行時オプションを格納する `AssemblerOptionSpec` オブジェクトを作成します。
   * `AssemblerOptionSpec` オブジェクトに属するメソッドを呼び出して、ビジネス要件を満たすよう実行時オプションを設定します。例えば、エラーが発生時にジョブの処理を続行するように Assembler サービスに指示するには、 `AssemblerOptionSpec` オブジェクトの `setFailOnError` メソッドとパス `false`を呼び出します。

1. PDF ドキュメントを分割します。

   `AssemblerServiceClient` オブジェクトの `invokeDDX` メソッドを呼び出して、以下の必須値を渡します。

   * 使用する DDX ドキュメントを表す `com.adobe.idp.Document` オブジェクト
   * 分割する PDF ドキュメントを含む `java.util.Map` オブジェクト
   * デフォルトのフォントやジョブログレベルを含む、実行時のオプションを指定する `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` オブジェクト

   `invokeDDX` メソッドは、 ディスアセンブリされた PDF ドキュメントと発生した例外を含む `com.adobe.livecycle.assembler.client.AssemblerResult` オブジェクトを返します。

1. 分割した PDF ドキュメントを保存します。

   分割された PDF ドキュメントを取得するには、以下のアクションを実行します。

   * `AssemblerResult` オブジェクトの `getDocuments` メソッドを呼び出します。これにより、`java.util.Map` オブジェクトが返されます。
   * 結果の `com.adobe.idp.Document` オブジェクトが見つかるまで `java.util.Map` オブジェクトを反復処理します。
   * `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを呼び出して、PDF ドキュメントを抽出します。

**関連トピック**

[プログラムによる PDF ドキュメントの分割](#programmatically-disassembling-pdf-documents)

[クイックスタート（SOAP モード）：Java API を使用した PDF ドキュメントの分割](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-disassembling-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Web サービス API を使用した PDF ドキュメントの分割 {#disassemble-a-pdf-document-using-the-web-service-api}

Assembler サービス API（web サービス）を使用して PDF ドキュメントを分割します。

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

1. 既存の DDX ドキュメントを参照します。

   * コンストラクターを使用して `BLOB` オブジェクトを作成します。`BLOB` オブジェクトは、DDX ドキュメントを保存するために使用されます。
   * コンストラクタを呼び出して `System.IO.FileStream` オブジェクトを作成します。DDX ドキュメントのファイルの場所を表す文字列値と、ファイルを開くモードを表す文字列値を渡します。
   * `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することで、バイト配列のサイズを決定できます。
   * バイト配列にストリームデータを入力するには、`System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出し、バイト配列、開始位置、読み取るストリーム長を渡します。
   * `MTOM` プロパティにバイト配列の内容を割り当てることによって、`BLOB` オブジェクトにデータを入力します。

1. 分割する PDF ドキュメントを参照します。

   * コンストラクターを使用して `BLOB` オブジェクトを作成します。`BLOB` オブジェクトは、入力 PDF ドキュメントを格納するために使用します。この `BLOB` オブジェクトは引数として `invokeOneDocument` に渡されます。
   * コンストラクタを呼び出し、入力 PDF ドキュメントのファイルの場所とファイルを開くモードを表す文字列値を渡すことによって、`System.IO.FileStream` オブジェクトを作成します。
   * `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することで、バイト配列のサイズを決定できます。
   * `System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出し、バイト配列、開始位置、読み取るストリーム長を渡すことによって、バイト配列にストリームデータを入力します。
   * バイト配列の内容を `MTOM` フィールドに割り当てることで、`BLOB` オブジェクトにデータを入力します。
   * `MyMapOf_xsd_string_To_xsd_anyType` オブジェクトを作成します。このコレクションオブジェクトは、ディスアセンブルする PDF を保存するために使用されます。
   * `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトを作成します。
   * キー名を表す文字列値を `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトの `key` フィールドに割り当てます。この値は、DDX ドキュメントで指定された PDF ソース要素の値と一致している必要があります。
   * PDF ドキュメントを格納する `BLOB` オブジェクトを、`MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトの `value` フィールドに割り当てます。
   * `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトを `MyMapOf_xsd_string_To_xsd_anyType` オブジェクトに追加します。`MyMapOf_xsd_string_To_xsd_anyType` オブジェクトの `Add` メソッドを呼び出して、`MyMapOf_xsd_string_To_xsd_anyType` オブジェクトを渡します。

1. 実行時オプションを設定します。

   * ランタイムオプションを格納する `AssemblerOptionSpec` オブジェクトをコンストラクタで作成します。
   * `AssemblerOptionSpec` オブジェクトに属するデータメンバーに値を割り当てることで、ビジネス要件を満たす実行時オプションを設定します。例えば、エラーが発生してもジョブの処理を続行するよう Assembler サービスに指示するには、`AssemblerOptionSpec` オブジェクトの `failOnError` フィールドに `false` を割り当てます。

1. PDF ドキュメントを分割します。

   `AssemblerServiceClient` オブジェクトの `invokeDDX` メソッドを呼び出して、次の値を渡します。

   * PDF ドキュメントをディスアセンブルする DDX ドキュメントを表す `BLOB` オブジェクト
   * ディスアセンブルする PDF ドキュメントを含む `MyMapOf_xsd_string_To_xsd_anyType` オブジェクト
   * 実行時オプションを指定する `AssemblerOptionSpec` オブジェクト

   `invokeDDX` メソッドは、ジョブの結果および発生した例外を含む `AssemblerResult` オブジェクトを返します。

1. 分割した PDF ドキュメントを保存します。

   新しく作成した PDF ドキュメントを取得するには、次の操作を実行します。

   * `AssemblerResult` オブジェクトの `documents` フィールド（ディスアセンブリされた PDF ドキュメントを含む `Map` オブジェクト）にアクセスします。
   * `Map`オブジェクトを反復処理して、各結果ドキュメントを取得します。次に、その配列メンバーの`value`を`BLOB`にキャストします。
   * `BLOB`オブジェクトの`MTOM`プロパティにアクセスして、PDF ドキュメントを表すバイナリデータを抽出します。これにより、PDF ファイルに書き出すことができるバイト配列が返されます。

**関連トピック**

[プログラムによる PDF ドキュメントの分割](#programmatically-disassembling-pdf-documents)

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
