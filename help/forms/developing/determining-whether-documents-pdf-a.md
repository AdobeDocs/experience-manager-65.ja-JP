---
title: ドキュメントが PDF/A に準拠しているかどうかの検証
seo-title: Determining Whether Documents Are PDF/A-Compliant
description: Assembler サービスでは、Java API と web サービス API を使用して、PDF ドキュメントが PDF/A に準拠しているかどうかを判断できます。
seo-description: Use the Assembler service to determine if a PDF document is PDF/A-compliant using the Java API and Web Service API.
uuid: 4e9d8c8f-2153-411b-9c4b-2d14b3c8f4bb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: c429d6e1-7847-43c8-bf75-cb0078dbb9d5
role: Developer
exl-id: 096fd2ac-616f-484a-b093-9d98b2f87093
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '2082'
ht-degree: 100%

---

# ドキュメントが PDF/A に準拠しているかどうかの検証 {#determining-whether-documents-are-pdf-a-compliant}

Assembler サービスを使用して、PDF ドキュメントが PDF/A に準拠しているかどうかを判断できます。PDF/A ドキュメントは、ドキュメントのコンテンツを長期間保存するためのアーカイブ形式として存在します。フォントはドキュメント内に埋め込まれ、ファイルは圧縮されません。その結果、通常、PDF/A ドキュメントは標準の PDF ドキュメントよりも大きくなります。また、PDF/A ドキュメントには、オーディオおよびビデオコンテンツは含まれません。

PDF/A-1 仕様は、A と B という 2 つの適合レベルで構成されます。2 つのレベルの主な違いは、適合レベル B には必要ない論理構造（アクセシビリティ）のサポートです。適合レベルに関係なく、PDF/A-1 では、生成されたPDF/A ドキュメント内にすべてのフォントが埋め込まれていることを示します。現時点では、検証（および変換）では PDF/A-1b のみがサポートされています。

この説明では、次の DDX ドキュメントが使用されていると仮定します。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
         <DocumentInformation source="Loan.pdf" result="Loan_result.xml">
         <PDFAValidation compliance="PDF/A-1b" resultLevel="Detailed"                       ignoreUnusedResources="true" allowCertificationSignatures="true" />
     </DocumentInformation>
 </DDX>
```

この DDX ドキュメント内で、`DocumentInformation` 要素は、入力 PDF ドキュメントに関する情報を返すように Assembler サービスに指示します。`DocumentInformation` 要素内で、`PDFAValidation` 要素は、入力 PDF ドキュメントが PDF/A に準拠しているかどうかを示すように Assembler サービスに指示します。

Assembler サービスは、入力 PDF ドキュメントが `PDFAConformance` 要素を含む XML ドキュメント内で PDF/A 準拠であるかどうかを指定する情報を返します。入力 PDF ドキュメントが PDF/A に準拠している場合、`PDFAConformance` 要素の `isCompliant` 属性の値は `true` です。PDF ドキュメントが PDF/A に準拠していない場合、`PDFAConformance` 要素の `isCompliant` 属性の値は `false` です。

>[!NOTE]
>
>この節で指定した DDX ドキュメントには `DocumentInformation` 要素が含まれているため、Assembler サービスは PDF ドキュメントではなく、XML データを返します。つまり、Assembler サービスは、PDF ドキュメントをアセンブルやディスアセンブルしません。XML ドキュメント内の入力 PDF ドキュメントに関する情報を返します。

>[!NOTE]
>
>Assembler サービスについて詳しくは、[AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

>[!NOTE]
>
>DDX ドキュメントについて詳しくは、[Assembler サービスと DDX リファレンス](https://www.adobe.com/go/learn_aemforms_ddx_63)を参照してください。

## 手順の概要 {#summary-of-steps}

PDF ドキュメントが PDF/A に準拠しているかどうかを判断するには、以下のタスクを実行します。

1. プロジェクトファイルを含めます。
1. PDF Assembler クライアントを作成します。
1. 既存の DDX ドキュメントを参照します。
1. PDF/A の準拠を判断するために使用される PDF ドキュメントを参照してください。
1. 実行時オプションを設定します。
1. PDF ドキュメントに関する情報を取得します。
1. 返された XML ドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar（AEM Forms が JBoss にデプロイされている場合に必要）
* jbossall-client.jar（AEM Formsが JBoss にデプロイされている場合に必要）

AEM Forms が JBoss 以外のサポート対象の J2EE アプリケーションサーバーにデプロイされている場合は、adobe-utilities.jar ファイルと jbossall-client.jar ファイルを、AEM Forms がデプロイされている J2EE アプリケーションサーバーに固有の JAR ファイルに置き換える必要があります。 すべての AEM Forms JAR ファイルの場所について、詳しくは [AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。

**PDF Assembler クライアントを作成する**

Assembler 操作をプログラムで実行する前に、Assembler サービスクライアントを作成する必要があります。

**既存の DDX ドキュメントの参照**

Assembler サービス操作を実行するには、DDX ドキュメントを参照する必要があります。入力 PDF ドキュメントが PDF/A に準拠しているかどうかを判断するには、DDX ドキュメントに `DocumentInformation` 要素内の `PDFAValidation` 要素が含まれていることを確認してください。この `PDFAValidation` 要素は、入力 PDF ドキュメントが PDF/A に準拠しているかどうかを指定する XML ドキュメントを返すように Assembler サービスに指示します。

**PDF/A 準拠の判断に使用される PDF ドキュメントの参照**

PDFドキュメントが PDF/A に準拠しているかどうかを判断するには、PDF ドキュメントを参照して Assembler サービスに渡す必要があります。

**実行時オプションを設定**

ジョブの実行中に Assembler サービスの動作を制御する実行時オプションを設定できます。例えば、エラーが発生した場合にジョブの処理を続行するよう Assembler サービスに指示するオプションを設定できます。 設定できる実行時オプションについて詳しくは、[AEM Forms API リファレンス](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ja)の `AssemblerOptionSpec` クラスリファレンスを参照してください。

**PDF ドキュメントに関する情報の取得**

Assembler サービスクライアントの作成、DDX ドキュメントの参照、インタラクティブ PDF ドキュメントの参照、実行時オプションの設定を行うと、`invokeDDX` 操作を呼び出すことができます。DDX ドキュメントには `DocumentInformation` 要素が含まれているため、Assembler サービスは PDF ドキュメントではなく、XML データを返します。

**返された XML ドキュメントの保存**

Assembler サービスが返す XML ドキュメントは、入力 PDF ドキュメントが PDF/A に準拠しているかどうかを指定します。例えば、入力 PDF ドキュメントが PDF/A に準拠していない場合、Assembler サービスは以下の要素を含む XML ドキュメントを返します。

```xml
 <PDFAConformance isCompliant="false" compliance="PDF/A-1b" resultLevel="Detailed" ignoreUnusedResources="true" allowCertificationSignatures="true">
```

XML ドキュメントを XML ファイルとして保存し、ファイルを開いて結果を表示できるようにします。

**関連トピック**

[Java API を使用したドキュメントが PDF/A に準拠しているかどうかの確認](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api)

[web サービス API を使用したドキュメントが PDF/A に準拠しているかどうかの確認](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDF ドキュメントをプログラムで組み立てる](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java API を使用したドキュメントが PDF/A に準拠しているかどうかの確認 {#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api}

Assembler サービス API（Java）を使用して、PDF ドキュメントが PDF/A に準拠しているかどうかを判断します。

1. プロジェクトファイルを含めます。

   adobe-livecycle-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. PDF Assembler クライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用し、`ServiceClientFactory` オブジェクトを渡して、`AssemblerServiceClient` オブジェクトを作成します。

1. 既存の DDX ドキュメントを参照します。

   * DDX ドキュメントを表す `java.io.FileInputStream` オブジェクトを作成するには、コンストラクターを使用して、DDX ファイルの場所を指定する文字列値を渡します。PDF ドキュメントが PDF/A に準拠しているかどうかを判断するには、DDX ドキュメントの `DocumentInformation` 要素内に含まれる `PDFAValidation` 要素が含まれていることを確認してください。
   * コンストラクターを使用して `java.io.FileInputStream` オブジェクトを渡し、`com.adobe.idp.Document` オブジェクトを作成します。

1. PDF/A の準拠を判断するために使用される PDF ドキュメントを参照してください。

   * `java.io.FileInputStream` オブジェクトを作成するには、コンストラクターを使用して、PDF/A の準拠を判断するために使用される PDF ドキュメントの場所を渡します。
   * `com.adobe.idp.Document` オブジェクトを作成するには、コンストラクターを使用して、PDF ドキュメントを含む `java.io.FileInputStream` オブジェクトを渡します。
   * `HashMap` コンストラクターを使用して、入力 PDF ドキュメントを格納するために使用される`java.util.Map` オブジェクトを作成します。
   * `java.util.Map` オブジェクトにエントリを追加するには、`put` メソッドを呼び出して、以下の引数を渡します。

      * キー名を表す文字列値。この値は、DDX ドキュメントで指定されたソース要素の値と一致する必要があります。 例えば、この節で紹介する DDX ドキュメント内のソース要素の値は Loan.pdf です。
      * 入力 PDF ドキュメントを含む `com.adobe.idp.Document` オブジェクト。

1. 実行時オプションを設定します。

   * コンストラクターを使用して、実行時オプションを格納する `AssemblerOptionSpec` オブジェクトを作成します。
   * `AssemblerOptionSpec` オブジェクトに属するメソッドを呼び出して、ビジネス要件を満たすように実行時オプションを設定します。例えば、エラーが発生したときにジョブの処理を続行するように Assembler サービスに指示するには、`AssemblerOptionSpec` オブジェクトの `setFailOnError` メソッドを呼び出して、`false` を渡します。

1. PDF ドキュメントに関する情報を取得します。

   `AssemblerServiceClient` オブジェクトの `invokeDDX` メソッドを呼び出して、以下の必要な値を渡します。

   * 使用する DDX ドキュメントを表す `com.adobe.idp.Document` オブジェクト
   * PDF/A 準拠の判断に使用される入力 PDF ファイルを含む `java.util.Map` オブジェクト
   * 実行時のオプションを指定する `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` オブジェクト

   この `invokeDDX` メソッドは、入力 PDF ドキュメントが PDF/A に準拠しているかどうかを指定する XML データを含む `com.adobe.livecycle.assembler.client.AssemblerResult` オブジェクトを返します。

1. 返された XML ドキュメントを保存します。

   入力 PDF ドキュメントが PDF/A ドキュメントであるかどうかを指定する XML データを取得するには、次のアクションを実行します。

   * `AssemblerResult` オブジェクトの `getDocuments` メソッドを呼び出します。これにより、`java.util.Map` オブジェクトが返されます。
   * 結果の `com.adobe.idp.Document` オブジェクトが見つかるまで、`java.util.Map` オブジェクトを繰り返し処理します。
   * `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを呼び出して、XML ドキュメントを抽出します。XML データは XML ファイルとして保存してください。

**関連トピック**

[クイックスタート（SOAP モード）：Java API を使用したドキュメントの PDF/A 準拠の確認](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-determining-whether-a-document-is-pdf-a-compliant-using-the-java-api)（SOAP モード）

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## web サービス API を使用したドキュメントが PDF/A に準拠しているかどうかの確認 {#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api}

Assembler Service API（web サービス）を使用して、PDF ドキュメントが PDF/A に準拠しているかどうかを判断します。

1. プロジェクトファイルを含めます。

   MTOM を使用する Microsoft .NET プロジェクトを作成します。以下の WSDL 定義を必ず使用してください。`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`

   >[!NOTE]
   >
   >`localhost` を、AEM Forms をホストするサーバーの IP アドレスに置き換えます。

1. PDF Assembler クライアントを作成します。

   * デフォルトのコンストラクターを使用して、`AssemblerServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して、`AssemblerServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/AssemblerService?blob=mtom`）。`lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。
   * `AssemblerServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` フィールドを `WSMessageEncoding.Mtom` に設定します。 この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `AssemblerServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * `AssemblerServiceClient.ClientCredentials.UserName.Password` フィールドに対応するパスワード値を割り当てます。
      * フィールド `BasicHttpBindingSecurity.Transport.ClientCredentialType` に定数値 `HttpClientCredentialType.Basic` を割り当てます。
      * フィールド `BasicHttpBindingSecurity.Security.Mode` に定数値 `BasicHttpSecurityMode.TransportCredentialOnly` を割り当てます。

1. 既存の DDX ドキュメントを参照します。

   * コンストラクターを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、DDX ドキュメントの保存に使用されます。
   * `System.IO.FileStream` オブジェクトを作成するには、そのコンストラクターを呼び出し、DDX ドキュメントのファイルの場所とファイルを開くモードを表す文字列値を渡します。
   * `System.IO.FileStream` オブジェクトのコンテンツを保存するバイト配列を作成します。バイト配列のサイズは、`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することで決定できます。
   * バイト配列にストリームデータを入力するには、`System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出し、読み込むバイト配列、開始位置、ストリーム長を渡します。
   * `MTOM` フィールドにバイト配列の内容をを割り当てて、`BLOB` オブジェクトにデータを入力します。

1. PDF/A の準拠を判断するために使用される PDF ドキュメントを参照してください。

   * コンストラクターを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、入力 PDF ドキュメントの格納に使用します。
   * `System.IO.FileStream` オブジェクトを作成するには、そのコンストラクターを呼び出し、入力 PDF ドキュメントのファイルの場所とファイルを開くモードを表す文字列値を渡します。
   * `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。バイト配列のサイズは、`System.IO.FileStream` オブジェクトの `Length` プロパティを取得して決定します。
   * バイト配列にストリームデータを入力するには、`System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出し、バイト配列、開始位置、読み取るストリーム長を渡します。
   * `MTOM` プロパティにバイト配列の内容を割り当てて、`BLOB` オブジェクトにデータを入力します。
   * `MyMapOf_xsd_string_To_xsd_anyType` オブジェクトを作成します。このコレクションオブジェクトは、PDF ドキュメントの保存に使用されます。
   * `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトを作成します。
   * キー名を表す文字列値を `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトの `key` フィールドに割り当てます。この値は、DDX ドキュメントで指定された PDF ソース要素の値と一致している必要があります。
   * PDF ドキュメントを保存する `BLOB` オブジェクトを、`MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトの `value` フィールドに割り当てます。
   * `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトを `MyMapOf_xsd_string_To_xsd_anyType` オブジェクトに追加します。`MyMapOf_xsd_string_To_xsd_anyType` オブジェクトの `Add` メソッドを呼び出して `MyMapOf_xsd_string_To_xsd_anyType` オブジェクトを渡します。

1. 実行時オプションを設定します。

   * コンストラクターを使用して実行時オプションを格納する `AssemblerOptionSpec` オブジェクトを作成します。
   * `AssemblerOptionSpec` オブジェクトに属するデータメンバーに値を割り当てることにより、ビジネス要件を満たすように実行時オプションを設定します。例えば、エラーが発生した場合にジョブの処理を続行するように Assembler サービスに指示するには、`false` を `AssemblerOptionSpec` オブジェクトの `failOnError` データメンバーに割り当てます。

1. PDF ドキュメントに関する情報を取得します。

   `AssemblerServiceService` オブジェクトの `invoke` メソッドを呼び出して、以下の値を渡します。

   * DDX ドキュメントを表す `BLOB` オブジェクト。
   * 入力 PDF ドキュメントを格納する `MyMapOf_xsd_string_To_xsd_anyType` オブジェクト。キーは PDF ソースファイルの名前と一致する必要があり、値は入力 PDF ファイルに対応する `BLOB` オブジェクトである必要があります。
   * 実行時オプションを指定する `AssemblerOptionSpec` オブジェクト。

   `invoke` メソッドは、入力 PDF ドキュメントが PDF/A ドキュメントであるかどうかを指定する XML データを含む `AssemblerResult` オブジェクトを返します。

1. 返された XML ドキュメントを保存します。

   入力 PDF ドキュメントが PDF/A ドキュメントであるかどうかを指定する XML データを取得するには、次のアクションを実行します。

   * `AssemblerResult` オブジェクトの `documents` フィールドにアクセスします。これは、入力 PDF ドキュメントが PDF/A ドキュメントであるかどうかを指定する XML データを含む `Map` オブジェクトです。
   * `Map` オブジェクトを反復処理して各結果ドキュメントを取得します。次に、その配列メンバーの値を `BLOB` にキャストします。
   * `BLOB` オブジェクトの `MTOM` フィールドにアクセスして、XML データを表すバイナリデータを抽出します。このフィールドには、XML ファイルとして書き出すことができるバイトの配列が格納されます。

**関連トピック**

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
