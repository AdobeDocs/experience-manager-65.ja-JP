---
title: ドキュメントがPDF/Aに準拠しているかどうかの確認
seo-title: ドキュメントがPDF/Aに準拠しているかどうかの確認
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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Determining Whether Documents Are PDF/A-Compliant {#determining-whether-documents-are-pdf-a-compliant}

Assemblerサービスを使用して、PDFドキュメントがPDF/Aに準拠しているかどうかを確認できます。 PDF/Aドキュメントは、ドキュメントのコンテンツを長期保存するためのアーカイブ形式として存在します。 フォントはドキュメント内に埋め込まれ、ファイルは圧縮されません。その結果、通常、PDF/A ドキュメントは標準の PDF ドキュメントよりも大きくなります。また、PDF/A ドキュメントには、オーディオおよびビデオコンテンツは含まれません。

PDF/A-1仕様は、2つのレベルの準拠（AとB）で構成されています。この2つのレベルの主な違いは、論理構造（アクセシビリティ）のサポートです。これは準拠レベルBには必要ありません。準拠レベルに関係なく、PDF/A-1では、生成されたPDF/Aドキュメント内にすべてのフォントが埋め込まれます。 現時点では、検証（および変換）ではPDF/A-1bのみがサポートされています。

この説明の目的で、次のDDXドキュメントが使用されているとします。

```as3
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
         <DocumentInformation source="Loan.pdf" result="Loan_result.xml">
         <PDFAValidation compliance="PDF/A-1b" resultLevel="Detailed"                       ignoreUnusedResources="true" allowCertificationSignatures="true" />
     </DocumentInformation>
 </DDX>
```

このDDXドキュメント内で、要素は `DocumentInformation` 入力PDFドキュメントに関する情報を返すようAssemblerサービスに指示します。 要素内で `DocumentInformation` は、要素が入 `PDFAValidation` 力PDFドキュメントがPDF/Aに準拠しているかどうかを示すようにAssemblerサービスに指示します。

Assemblerサービスは、要素を含むXMLドキュメント内で入力PDFドキュメントがPDF/Aに準拠しているかどうかを指定する情報を返し `PDFAConformance` ます。 入力PDFドキュメントがPDF/Aに準拠している場合、要素の属性 `PDFAConformance` の値はにな `isCompliant` ります `true`。 PDFドキュメントがPDF/Aに準拠していない場合、要素の属性 `PDFAConformance` の値はにな `isCompliant` ります `false`。

>[!NOTE]
>
>この節で指定したDDXドキュメントに要素が含まれているので、Assemblerサ `DocumentInformation` ービスはPDFドキュメントではなくXMLデータを返します。 つまり、AssemblerサービスはPDFドキュメントをアセンブルまたはディスアセンブリしません。xmlドキュメント内の入力PDFドキュメントに関する情報を返します。

>[!NOTE]
>
>For more information about the Assembler service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>DDXドキュメントについて詳しくは、 [Assembler Service and DDX Referenceを参照してください](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 手順の概要 {#summary-of-steps}

PDFドキュメントがPDF/Aに準拠しているかどうかを確認するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. PDFアセンブラクライアントを作成します。
1. 既存のDDXドキュメントを参照します。
1. PDF/Aの準拠性の判定に使用されるPDFドキュメントを参照します。
1. 実行時オプションを設定します。
1. PDFドキュメントに関する情報を取得します。
1. 返されたXMLドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar（AEM FormsがJBossにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsをJBossにデプロイする場合に必要）

aem formsがJBoss以外のサポート対象のJ2EEアプリケーションサーバーにデプロイされている場合は、adobe-utilities.jarファイルとjbossall-client.jarファイルを、AEM formsのデプロイ先のJ2EEアプリケーションサーバーに固有のJARファイルに置き換える必要があります。 For information about the location of all AEM Forms JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**PDFアセンブラクライアントの作成**

プログラムでAssembler操作を実行する前に、Assemblerサービスクライアントを作成する必要があります。

**既存のDDXドキュメントの参照**

Assemblerサービス操作を実行するには、DDXドキュメントを参照する必要があります。 入力PDFドキュメントがPDF/Aに準拠しているかどうかを確認するには、DDXドキュメントに要素内の要素が含まれてい `PDFAValidation` ることを確認 `DocumentInformation` します。 この要 `PDFAValidation` 素は、入力PDFドキュメントがPDF/Aに準拠しているかどうかを指定するXMLドキュメントを返すようAssemblerサービスに指示します。

**PDF/Aの準拠性の判定に使用するPDFドキュメントの参照**

PDFドキュメントがPDF/Aに準拠しているかどうかを確認するには、PDFドキュメントを参照し、Assemblerサービスに渡す必要があります。

**実行時オプションの設定**

ジョブの実行中にAssemblerサービスの動作を制御する実行時オプションを設定できます。 例えば、エラーが発生した場合にジョブの処理を続行するようAssemblerサービスに指示するオプションを設定できます。 設定可能なランタイムオプションについて詳しくは、『 `AssemblerOptionSpec` AEM Forms APIリファレンス』のクラス [リファレンスを参照し](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)てください。

**PDFドキュメントに関する情報の取得**

Assemblerサービスクライアントを作成し、DDXドキュメントを参照し、インタラクティブPDFドキュメントを参照し、実行時オプションを設定した後で、操作を呼び出すことがで `invokeDDX` きます。 DDXドキュメントには要素が含まれて `DocumentInformation` いるので、AssemblerサービスはPDFドキュメントではなくXMLデータを返します。

**返されたXMLドキュメントを保存します**

Assemblerサービスが返すXMLドキュメントは、入力PDFドキュメントがPDF/Aに準拠しているかどうかを指定します。 例えば、入力PDFドキュメントがPDF/Aに準拠していない場合、Assemblerサービスは次の要素を含むXMLドキュメントを返します。

```as3
 <PDFAConformance isCompliant="false" compliance="PDF/A-1b" resultLevel="Detailed" ignoreUnusedResources="true" allowCertificationSignatures="true">
```

XMLドキュメントをXMLファイルとして保存し、ファイルを開いて結果を表示できるようにします。

**関連トピック**

[Java APIを使用したドキュメントがPDF/Aに準拠しているかどうかを確認する](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api)

[WebサービスAPIを使用したドキュメントがPDF/Aに準拠しているかどうかの確認](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDFドキュメントのプログラムによるアセンブリ](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java APIを使用したドキュメントがPDF/Aに準拠しているかどうかを確認する {#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api}

Assembler Service API(Java)を使用して、PDFドキュメントがPDF/Aに準拠しているかどうかを確認します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-assembler-client.jarなどのクライアントJARファイルを含めます。

1. PDFアセンブラクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `AssemblerServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. 既存のDDXドキュメントを参照します。

   * コンストラ `java.io.FileInputStream` クターを使用し、DDXファイルの場所を指定するstring値を渡して、DDXドキュメントを表すオブジェクトを作成します。 PDFドキュメントがPDF/Aに準拠しているかどうかを確認するには、DDXドキュメントに、要素内に含まれる要 `PDFAValidation` 素が含まれていることを確認し `DocumentInformation` ます。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PDF/Aの準拠性の判定に使用されるPDFドキュメントを参照します。

   * コンストラ `java.io.FileInputStream` クターを使用し、PDF/Aの準拠性を判定するために使用するPDFドキュメントの場所を渡して、オブジェクトを作成します。
   * コンストラク `com.adobe.idp.Document` ターを使用し、PDFドキュメントを含むオブジェクトを `java.io.FileInputStream` 渡して、オブジェクトを作成します。
   * コンストラク `java.util.Map` ターを使用して、入力PDFドキュメントの保存に使用するオブジェクトを作成 `HashMap` します。
   * メソッドを呼び出し、次 `java.util.Map` の引数を渡して、オ `put` ブジェクトにエントリを追加します。

      * キー名を表すstring値です。 この値は、DDXドキュメントで指定されたソース要素の値と一致する必要があります。 例えば、この節で紹介するDDXドキュメント内のsource要素の値はLoan.pdfです。
      * 入力PDF `com.adobe.idp.Document` ドキュメントを含むオブジェクトです。

1. 実行時オプションを設定します。

   * コンストラクタ `AssemblerOptionSpec` ーを使用して、実行時のオプションを格納するオブジェクトを作成します。
   * オブジェクトに属するメソッドを呼び出して、ビジネス要件に合わせて実行時のオプションを設定 `AssemblerOptionSpec` します。 例えば、エラーが発生した場合にジョブの処理を続行するようにAssemblerサービスに指示するには、オブジェクトのメソッド `AssemblerOptionSpec` を呼び出して `setFailOnError` 渡してくださ `false`い。

1. PDFドキュメントに関する情報を取得します。

   オブジェクト `AssemblerServiceClient` のメソッドを呼 `invokeDDX` び出し、次の必要な値を渡します。

   * 使用す `com.adobe.idp.Document` るDDXドキュメントを表すオブジェクトです
   * PDF/A `java.util.Map` の準拠性を判定するために使用される入力PDFファイルを含むオブジェクト
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` object that specifies the run-time options
   このメ `invokeDDX` ソッドは、入力PDF `com.adobe.livecycle.assembler.client.AssemblerResult` ドキュメントがPDF/Aに準拠しているかどうかを指定するXMLデータを含むオブジェクトを返します。

1. 返されたXMLドキュメントを保存します。

   入力PDFドキュメントがPDF/Aドキュメントであるかどうかを指定するXMLデータを取得するには、次の操作を実行します。

   * オブジェクト `AssemblerResult` のメソッドを呼び出 `getDocuments` します。 オブジェクトを返 `java.util.Map` します。
   * 結果のオブジェクト `java.util.Map` が見つかるまで、オブジェクトを繰り返 `com.adobe.idp.Document` します。
   * オブジェクト `com.adobe.idp.Document` のメソッドを呼 `copyToFile` び出して、XMLドキュメントを抽出します。 XMLデータはXMLファイルとして保存します。

**関連トピック**

[クイックスタート（SOAPモード）:Java API](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-determining-whether-a-document-is-pdf-a-compliant-using-the-java-api) （SOAPモード）を使用したドキュメントがPDF/Aに準拠しているかどうかの判定

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## WebサービスAPIを使用したドキュメントがPDF/Aに準拠しているかどうかの確認 {#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api}

Assembler Service API（Webサービス）を使用して、PDFドキュメントがPDF/Aに準拠しているかどうかを確認します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. PDFアセンブラクライアントを作成します。

   * デフォルトのコンス `AssemblerServiceClient` トラクターを使用して、オブジェクトを作成します。
   * コンストラクタ `AssemblerServiceClient.Endpoint.Address` ーを使用してオブジェクトを作 `System.ServiceModel.EndpointAddress` 成します。 WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/AssemblerService?blob=mtom`)に渡すstring値。 属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。)
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `AssemblerServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `AssemblerServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `AssemblerServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. 既存のDDXドキュメントを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオブ `BLOB` ジェクトは、DDXドキュメントの保存に使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、DDXドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイト配列、開 `System.IO.FileStream` 始位置、ストリ `Read` ーム長を渡すことによって、バイト配列にストリームデータを設定します。
   * オブジェクト `BLOB` にバイト配列の内容を `MTOM` フィールドに割り当てて、オブジェクトを入力します。

1. PDF/Aの準拠性の判定に使用されるPDFドキュメントを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、入力PDFドキュメントの保存に使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、入力PDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイト配列、開 `System.IO.FileStream` 始位置、ストリ `Read` ーム長を渡すことによって、バイト配列にストリームデータを設定します。
   * オブジェクト `BLOB` にバイト配列の内容をプロ `MTOM` パティに割り当てて、オブジェクトを設定します。
   * Create a `MyMapOf_xsd_string_To_xsd_anyType` object. このコレクションオブジェクトは、PDFドキュメントの保存に使用されます。
   * Create a `MyMapOf_xsd_string_To_xsd_anyType_Item` object.
   * キー名を表すstring値をオブジェクトのフィールド `MyMapOf_xsd_string_To_xsd_anyType_Item` に割り当て `key` ます。 この値は、DDXドキュメントで指定されたPDFソース要素の値と一致する必要があります。
   * PDFドキュメント `BLOB` を保存するオブジェクトをオブジェクトのフィー `MyMapOf_xsd_string_To_xsd_anyType_Item` ルドに割り当 `value` てます。
   * オブジェクト `MyMapOf_xsd_string_To_xsd_anyType_Item` をオブジェクトに追加 `MyMapOf_xsd_string_To_xsd_anyType` します。 オブジェクトの `MyMapOf_xsd_string_To_xsd_anyType` メソッドを呼 `Add` び出し、オブジェクトを渡 `MyMapOf_xsd_string_To_xsd_anyType` します。

1. 実行時オプションを設定します。

   * コンストラクタ `AssemblerOptionSpec` ーを使用して、実行時のオプションを格納するオブジェクトを作成します。
   * オブジェクトに属するデータメンバーに値を割り当てて、ビジネス要件に合わせて実行時オプションを設定 `AssemblerOptionSpec` します。 例えば、エラーが発生した場合にジョブの処理を続行するようAssemblerサービスに指示するには、オブジェクトの `false` データメ `AssemblerOptionSpec` ンバーに割り `failOnError` 当てます。

1. PDFドキュメントに関する情報を取得します。

   オブジェクト `AssemblerServiceService` のメソッドを `invoke` 呼び出し、次の値を渡します。

   * DDXドキ `BLOB` ュメントを表すオブジェクトです。
   * 入力PDF `MyMapOf_xsd_string_To_xsd_anyType` ドキュメントを含むオブジェクトです。 そのキーはPDFソースファイルの名前と一致し、その値は入力PDFファイルに対応するオ `BLOB` ブジェクトである必要があります。
   * 実行時 `AssemblerOptionSpec` のオプションを指定するオブジェクトです。
   このメ `invoke` ソッドは、入力PDF `AssemblerResult` ドキュメントがPDF/Aドキュメントであるかどうかを指定するXMLデータを含むオブジェクトを返します。

1. 返されたXMLドキュメントを保存します。

   入力PDFドキュメントがPDF/Aドキュメントであるかどうかを指定するXMLデータを取得するには、次の操作を実行します。

   * オブジェクト `AssemblerResult` のフィー `documents` ルドにアクセスします。このフィールドは、 `Map` 入力PDFドキュメントがPDF/Aドキュメントであるかどうかを指定するXMLデータを含むオブジェクトです。
   * オブジェクトを繰り返し `Map` 処理し、各結果ドキュメントを取得します。 次に、その配列メンバーの値をにキャストします `BLOB`。
   * オブジェクトのフィールドにアクセスして、XMLデータを表すバイナリデ `BLOB` ータを抽出 `MTOM` します。 このフィールドには、XMLファイルとして書き出すことのできるバイトの配列が格納されます。

**関連トピック**

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
