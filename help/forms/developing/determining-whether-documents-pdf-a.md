---
title: ドキュメントがPDF/Aに準拠しているかどうかを確認する
seo-title: ドキュメントがPDF/Aに準拠しているかどうかを確認する
description: 'null'
seo-description: 'null'
uuid: 4e9d8c8f-2153-411b-9c4b-2d14b3c8f4bb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: c429d6e1-7847-43c8-bf75-cb0078dbb9d5
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '2069'
ht-degree: 5%

---


# Determining Whether Documents Are PDF/A-Compliant {#determining-whether-documents-are-pdf-a-compliant}

Assemblerサービスを使用すると、PDFドキュメントがPDF/Aに準拠しているかどうかを確認できます。 PDF/Aドキュメントは、ドキュメントのコンテンツを長期間保存するためのアーカイブ形式として存在します。 フォントはドキュメント内に埋め込まれ、ファイルは圧縮されません。その結果、通常、PDF/A ドキュメントは標準の PDF ドキュメントよりも大きくなります。また、PDF/A ドキュメントには、オーディオおよびビデオコンテンツは含まれません。

PDF/A-1仕様は、AとBの2つの準拠レベルで構成されています。2つのレベルの主な違いは、論理構造（アクセシビリティ）のサポートです。これは、準拠レベルBには必要ありません。準拠レベルにかかわらず、PDF/A-1は、生成されたPDF/Aドキュメントにすべてのフォントを埋め込むことを指示します。 現時点では、検証（および変換）ではPDF/A-1bのみがサポートされています。

この説明の目的で、次のDDXドキュメントが使用されているとします。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
         <DocumentInformation source="Loan.pdf" result="Loan_result.xml">
         <PDFAValidation compliance="PDF/A-1b" resultLevel="Detailed"                       ignoreUnusedResources="true" allowCertificationSignatures="true" />
     </DocumentInformation>
 </DDX>
```

このDDXドキュメント内で、 `DocumentInformation` 要素はAssemblerサービスに対して、入力PDFドキュメントに関する情報を返すように指示します。 要素内で `DocumentInformation` は、 `PDFAValidation` 要素が入力PDFドキュメントがPDF/Aに準拠しているかどうかを示すようにAssemblerサービスに指示します。

Assemblerサービスは、要素を含むXMLドキュメント内で入力PDFドキュメントがPDF/Aに準拠しているかどうかを指定する情報を返し `PDFAConformance` ます。 入力PDFドキュメントがPDF/Aに準拠している場合、 `PDFAConformance` 要素の `isCompliant` 属性の値は `true`です。 PDFドキュメントがPDF/Aに準拠していない場合、 `PDFAConformance` 要素の `isCompliant` 属性の値は `false`です。

>[!NOTE]
>
>この節で指定するDDXドキュメントには `DocumentInformation` 要素が含まれているので、AssemblerサービスはPDFドキュメントではなくXMLデータを返します。 つまり、Assemblerサービスは、PDFドキュメントをアセンブリまたはディスアセンブリしません。 xmlドキュメント内の入力PDFドキュメントに関する情報を返します。

>[!NOTE]
>
>For more information about the Assembler service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>DDXドキュメントについて詳しくは、『 [Assembler Service and DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63)』を参照してください。

## 手順の概要 {#summary-of-steps}

PDFドキュメントがPDF/Aに準拠しているかどうかを確認するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. PDFアセンブラクライアントを作成します。
1. 既存のDDXドキュメントの参照。
1. PDF/Aの準拠性の判定に使用されるPDFドキュメントを参照します。
1. 実行時オプションを設定します。
1. PDFドキュメントに関する情報を取得します。
1. 返されたXMLドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(AEM FormsがJBossにデプロイされている場合に必要)
* jbossall-client.jar(AEM FormsがJBossにデプロイされている場合に必要)

AEM FormsがJBoss以外のサポート対象のJ2EEアプリケーションサーバーにデプロイされている場合は、adobe-utilities.jarファイルとjbossall-client.jarファイルを、AEM FormsがデプロイされているJ2EEアプリケーションサーバーに固有のJARファイルに置き換える必要があります。 For information about the location of all AEM Forms JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**PDFアセンブラクライアントの作成**

プログラムによってAssembler操作を実行する前に、Assemblerサービスクライアントを作成する必要があります。

**既存のDDXドキュメントの参照**

Assemblerサービス操作を実行するには、DDXドキュメントを参照する必要があります。 入力PDFドキュメントがPDF/Aに準拠しているかどうかを確認するには、DDXドキュメントに要素内の `PDFAValidation` 要素が含まれていることを確認し `DocumentInformation` ます。 この `PDFAValidation` 要素は、入力PDFドキュメントがPDF/Aに準拠しているかどうかを指定するXMLドキュメントを返すようAssemblerサービスに指示します。

**PDF/Aの準拠性の判定に使用されるPDFドキュメントの参照**

PDFドキュメントがPDF/Aに準拠しているかどうかを確認するには、PDFドキュメントを参照してAssemblerサービスに渡す必要があります。

**実行時オプションの設定**

ジョブの実行中にAssemblerサービスの動作を制御する実行時オプションを設定できます。 例えば、エラーが発生した場合にジョブの処理を続行するようAssemblerサービスに指示するオプションを設定できます。 設定できる実行時オプションについて詳しくは、『 `AssemblerOptionSpec` AEM FormsAPIリファレンス』の [クラス参照を参照してください](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

**PDFドキュメントに関する情報の取得**

Assemblerサービスクライアントの作成後、DDXドキュメントの参照、インタラクティブPDFドキュメントの参照、および実行時オプションの設定を行った後、この `invokeDDX` 操作を呼び出すことができます。 DDXドキュメントには `DocumentInformation` 要素が含まれているので、AssemblerサービスはPDFドキュメントではなくXMLデータを返します。

**返されたXMLドキュメントを保存します**

Assemblerサービスが返すXMLドキュメントは、入力PDFドキュメントがPDF/Aに準拠しているかどうかを指定します。 例えば、入力PDFドキュメントがPDF/Aに準拠していない場合、Assemblerサービスは次の要素を含むXMLドキュメントを返します。

```xml
 <PDFAConformance isCompliant="false" compliance="PDF/A-1b" resultLevel="Detailed" ignoreUnusedResources="true" allowCertificationSignatures="true">
```

XMLドキュメントをXMLファイルとして保存し、ファイルを開いて結果を表示できるようにします。

**関連トピック**

[Java APIを使用した、ドキュメントがPDF/Aに準拠しているかどうかの確認](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api)

[WebサービスAPIを使用した、ドキュメントがPDF/Aに準拠しているかどうかを確認する](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[プログラムによるPDFドキュメントのアセンブリ](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java APIを使用した、ドキュメントがPDF/Aに準拠しているかどうかの確認 {#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api}

Assembler Service API(Java)を使用して、PDFドキュメントがPDF/Aに準拠しているかどうかを確認します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-assembler-client.jarなどのクライアントJARファイルを含めます。

1. PDFアセンブラクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `AssemblerServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. 既存のDDXドキュメントの参照。

   * コンストラクターを使用し、DDXファイルの場所を指定する文字列値を渡して、DDXドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。 PDFドキュメントがPDF/Aに準拠しているかどうかを確認するには、DDXドキュメントに、要素内に含まれる `PDFAValidation` 要素が含まれていることを確認し `DocumentInformation` ます。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PDF/Aの準拠性の判定に使用されるPDFドキュメントを参照します。

   * コンストラクターを使用し、PDF/Aの準拠性を決定するために使用するPDFドキュメントの場所を渡して、 `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクターを使用し、PDF `com.adobe.idp.Document` ドキュメントを含む `java.io.FileInputStream` オブジェクトを渡して、オブジェクトを作成します。
   * コンストラクターを使用して、入力PDFドキュメントの保存に使用する `java.util.Map` オブジェクトを作成し `HashMap` ます。
   * メソッド追加を呼び出し、次の引数を渡すことによって、オブジェクトに対するエントリを作成します。 `java.util.Map``put`

      * キー名を表すstring値です。 この値は、DDXドキュメントで指定されたソース要素の値と一致する必要があります。 例えば、この節で紹介するDDXドキュメントにあるsource要素の値はLoan.pdfです。
      * 入力PDFドキュメントを含む `com.adobe.idp.Document` オブジェクトです。

1. 実行時オプションを設定します。

   * コンストラクターを使用して、実行時のオプションを格納する `AssemblerOptionSpec` オブジェクトを作成します。
   * オブジェクトに属するメソッドを呼び出して、ビジネス要件に合うように実行時オプションを設定し `AssemblerOptionSpec` ます。 例えば、エラーが発生した場合にジョブの処理を続行するようにAssemblerサービスに指示するには、 `AssemblerOptionSpec` オブジェクトの `setFailOnError` メソッドを呼び出して渡し `false`ます。

1. PDFドキュメントに関する情報を取得します。

   オブジェクトの `AssemblerServiceClient``invokeDDX` メソッドを呼び出し、次の必須値を渡します。

   * 使用するDDXドキュメントを表す `com.adobe.idp.Document` オブジェクトです
   * PDF/Aの準拠性を判定するために使用される入力PDFファイルを含む `java.util.Map` オブジェクトです
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` object that specifies the run-time options

   この `invokeDDX` メソッドは、入力PDFドキュメントがPDF/Aに準拠しているかどうかを指定するXMLデータを含む `com.adobe.livecycle.assembler.client.AssemblerResult` オブジェクトを返します。

1. 返されたXMLドキュメントを保存します。

   入力PDFドキュメントがPDF/Aドキュメントであるかどうかを指定するXMLデータを取得するには、次の操作を実行します。

   * オブジェクトの `AssemblerResult` メソッドを呼び出し `getDocuments` ます。 これは、 `java.util.Map` オブジェクトを返します。
   * オブジェクトを繰り返し処理して、結果のオブジ `java.util.Map``com.adobe.idp.Document` ェクトを見つけます。
   * オブジェクトの `com.adobe.idp.Document``copyToFile` メソッドを呼び出してXMLドキュメントを抽出します。 XMLデータはXMLファイルとして保存してください。

**関連トピック**

[クイック開始（SOAPモード）: Java API](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-determining-whether-a-document-is-pdf-a-compliant-using-the-java-api) （SOAPモード）を使用したPDF/A準拠ドキュメントかどうかの判定

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## WebサービスAPIを使用した、ドキュメントがPDF/Aに準拠しているかどうかを確認する {#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api}

Assembler Service API（Webサービス）を使用して、PDFドキュメントがPDF/Aに準拠しているかどうかを確認します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >サーバーホスト `localhost` AEM FormsのIPアドレスに置き換えます。

1. PDFアセンブラクライアントを作成します。

   * デフォルトのコンストラクターを使用して `AssemblerServiceClient` オブジェクトを作成します。
   * コンストラクターを使用して `AssemblerServiceClient.Endpoint.Address` オブジェクトを作成し `System.ServiceModel.EndpointAddress` ます。 WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/AssemblerService?blob=mtom`)に渡すstring値を渡します。 属性を使用する必要はありません `lc_version` 。 この属性は、サービス参照を作成する場合に使用されます)。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `AssemblerServiceClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールドにAEM formsのユーザー名を割り当て `AssemblerServiceClient.ClientCredentials.UserName.UserName`ます。
      * 対応するパスワード値をフィールドに割り当て `AssemblerServiceClient.ClientCredentials.UserName.Password`ます。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当て `BasicHttpBindingSecurity.Security.Mode`ます。

1. 既存のDDXドキュメントの参照。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、DDXドキュメントの格納に使用されます。
   * コンストラクターを呼び出し、DDXドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
   * オブジェクトの `System.IO.FileStream``Read` メソッドを呼び出し、読み取るバイト配列、開始位置およびストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * オブジェクトにバイト配列の内容を割り当てて、 `BLOB` オブジェクト `MTOM` を入力します。

1. PDF/Aの準拠性の判定に使用されるPDFドキュメントを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、入力PDFドキュメントの保存に使用されます。
   * コンストラクターを呼び出し、入力PDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
   * オブジェクトの `System.IO.FileStream``Read` メソッドを呼び出し、読み取るバイト配列、開始位置およびストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * オブジェクトのプロパティにバイト配列の内容を割り当てて、 `BLOB``MTOM` オブジェクトを入力します。
   * Create a `MyMapOf_xsd_string_To_xsd_anyType` object. このコレクションオブジェクトは、PDFドキュメントの保存に使用されます。
   * Create a `MyMapOf_xsd_string_To_xsd_anyType_Item` object.
   * キー名を表すstring値を `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトの `key` フィールドに割り当てます。 この値は、DDXドキュメントで指定されたPDFソース要素の値と一致する必要があります。
   * PDFドキュメントを保存している `BLOB` オブジェクトをオブジェクトのフィ `MyMapOf_xsd_string_To_xsd_anyType_Item` ー `value` ルドに割り当てます。
   * オ追加ブジェクトをオブジ `MyMapOf_xsd_string_To_xsd_anyType_Item``MyMapOf_xsd_string_To_xsd_anyType` ェクトに追加します。 オブジェクトの `MyMapOf_xsd_string_To_xsd_anyType` メソッドを呼び出して、 `Add``MyMapOf_xsd_string_To_xsd_anyType` オブジェクトを渡します。

1. 実行時オプションを設定します。

   * コンストラクターを使用して、実行時のオプションを格納する `AssemblerOptionSpec` オブジェクトを作成します。
   * オブジェクトに属するデータメンバに値を割り当てることで、ビジネス要件に合った実行時オプションを設定し `AssemblerOptionSpec` ます。 例えば、エラーが発生した場合にジョブの処理を続行するようにAssemblerサービスに指示するには、 `false` オブジェクトの `AssemblerOptionSpec``failOnError` データメンバーに割り当てます。

1. PDFドキュメントに関する情報を取得します。

   オブジェクトの `AssemblerServiceService``invoke` メソッドを呼び出し、次の値を渡します。

   * DDXドキュメントを表す `BLOB` オブジェクトです。
   * 入力PDFドキュメントを含む `MyMapOf_xsd_string_To_xsd_anyType` オブジェクトです。 キーはPDFソースファイルの名前と一致する必要があり、その値は入力PDFファイルに対応する `BLOB` オブジェクトである必要があります。
   * 実行時オプションを指定する `AssemblerOptionSpec` オブジェクトです。

   この `invoke` メソッドは、入力PDFドキュメントがPDF/Aドキュメントであるかどうかを指定するXMLデータを含む `AssemblerResult` オブジェクトを返します。

1. 返されたXMLドキュメントを保存します。

   入力PDFドキュメントがPDF/Aドキュメントであるかどうかを指定するXMLデータを取得するには、次の操作を実行します。

   * オブジェクトのフ `AssemblerResult` ィールドにアクセスします。この `documents``Map` フィールドは、入力PDFドキュメントがPDF/Aドキュメントであるかどうかを指定するXMLデータが含まれるオブジェクトです。
   * オブジェクトを繰り返し処理して、 `Map` 各結果ドキュメントを取得します。 次に、その配列メンバの値をにキャストし `BLOB`ます。
   * XMLデータを表すバイナリデータを抽出するには、その `BLOB` オブジェクトの `MTOM` フィールドにアクセスします。 このフィールドには、XMLファイルとして書き出すことができるバイトの配列が格納されます。

**関連トピック**

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
