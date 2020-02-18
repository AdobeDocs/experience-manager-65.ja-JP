---
title: PDF/Aドキュメントの操作
seo-title: PDF/Aドキュメントの操作
description: 'null'
seo-description: 'null'
uuid: c258d253-068a-4412-955a-21d8a4792d6f
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 1e6cc554-aef1-463c-906b-634b80a27917
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# PDF/Aドキュメントの操作 {#working-with-pdf-a-documents}

**DocConverterサービスについて**

DocConverterサービスは、PDFドキュメントをPDA/Aドキュメントに変換できます。 このサービスを使用して、次のタスクを実行できます。

* PDFドキュメントをPDF/Aドキュメントに変換します。 (Converting Documents [to PDF/A Documentsを参照](pdf-a-documents.md#converting-documents-to-pdf-a-documents))。
* PDFドキュメントがPDF/Aドキュメントかどうかを確認します。 (「プログラ [ムによるPDF/Aの準拠の判定](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)」を参照)。

>[!NOTE]
>
>For more information about the DocConverter service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## ドキュメントのPDF/Aドキュメントへの変換 {#converting-documents-to-pdf-a-documents}

DocConverterサービスを使用して、PDFドキュメントをPDF/Aドキュメントに変換できます。 PDF/Aはドキュメントのコンテンツを長期保存するためのアーカイブ形式なので、すべてのフォントが埋め込まれ、ファイルは圧縮されません。 その結果、通常、PDF/A ドキュメントは標準の PDF ドキュメントよりも大きくなります。また、PDF/A ドキュメントには、オーディオおよびビデオコンテンツは含まれません。PDFドキュメントをPDF/Aドキュメントに変換する前に、PDFドキュメントがPDF/Aドキュメントでないことを確認してください。

PDF/A-1仕様は、2つのレベルの準拠（AとB）で構成されています。この2つの主な違いは、準拠レベルBには必要ない論理構造（アクセシビリティ）のサポートに関するものです。準拠レベルに関係なく、PDF/A-1では、生成されたPDF/Aドキュメント内にすべてのフォントが埋め込まれます。 現時点では、検証（および変換）ではPDF/A-1bのみがサポートされています。

PDF/AはPDFドキュメントのアーカイブの標準ですが、標準PDFドキュメントが会社の要件を満たしている場合にPDF/Aをアーカイブに使用する必要はありません。 PDF/A標準の目的は、長期にわたるアーカイブおよびドキュメント保存のニーズを満たすPDFファイルを作成することです。

>[!NOTE]
>
>For more information about the DocConverter service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary-of-steps}

PDFドキュメントをPDF/Aドキュメントに変換するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. DocConvertクライアントの作成
1. PDF/Aドキュメントに変換するPDFドキュメントを参照します。
1. トラッキング情報を設定します。
1. ドキュメントを変換します。
1. PDF/Aドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-utilities.jar（AEM FormsがJBoss Application serverにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsがJBoss Application Serverにデプロイされている場合に必要）

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**DocConvertクライアントの作成**

プログラムでDocConverter操作を実行する前に、DocConverterクライアントを作成する必要があります。 Java APIを使用している場合は、オブジェクトを作成し `DocConverterServiceClient` ます。 DocConverter webサービスAPIを使用している場合は、オブジェクトを作成し `DocConverterServiceService` ます。

**PDF/Aドキュメントに変換するPDFドキュメントの参照**

PDF/Aドキュメントに変換するPDFドキュメントを取得します。 AcrobatフォームなどのPDFドキュメントをPDF/Aドキュメントに変換しようとすると、例外が発生します。

**トラッキング情報の設定**

変換プロセス中に追跡する情報の量を決定する実行時オプションを設定できます。 つまり、PDFドキュメントをPDF/Aドキュメントに変換する際にDocConverterサービスが追跡する情報の量を指定する9つの異なるレベルを設定できます。

**ドキュメントの変換**

DocConverterサービスクライアントを作成した後、変換するPDFドキュメントを参照し、追跡する情報の量を指定する実行時オプションを設定し、PDFドキュメントをPDF/Aドキュメントに変換できます。

**PDF/Aドキュメントの保存**

PDF/AドキュメントをPDFファイルとして保存できます。

**関連トピック**

[Java APIを使用したドキュメントのPDF/Aドキュメントへの変換](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-java-api)

[WebサービスAPIを使用したドキュメントのPDF/Aドキュメントへの変換](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDF/A準拠のプログラムによる判断](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)

### Java APIを使用したドキュメントのPDF/Aドキュメントへの変換 {#convert-documents-to-pdf-a-documents-using-the-java-api}

Java APIを使用してPDFドキュメントをPDF/Aドキュメントに変換します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-docconverter-client.jarなどのクライアントJARファイルを含めます。

1. DocConvertクライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `DocConverterServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. PDF/Aドキュメントに変換するPDFドキュメントの参照

   * コンストラ `java.io.FileInputStream` クターを使用し、PDFファイルの場所を指定するstring値を渡して、変換するPDFドキュメントを表すオブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. トラッキング情報の設定

   * コンストラクタを使用して `PDFAConversionOptionSpec` オブジェクトを作成します。
   * オブジェクトのメソッドを呼び出し、トラッキ `PDFAConversionOptionSpec` ングレベルを指 `setLogLevel` 定する文字列値を渡して、情報トラッキングレベルを設定します。 For example, pass the value `FINE`. 各値について詳しくは、『 `setLogLevel` AEM Forms APIリファレンス』の [メソッドを参](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)照してください。

1. ドキュメントの変換

   オブジェクトのメソッドを呼び出し、次の値を渡して、PDFドキュ `DocConverterServiceClient` メントをPDF/A `toPDFA` ドキュメントに変換します。

   * 変換す `com.adobe.idp.Document` るPDFドキュメントを含むオブジェクトです
   * 追跡情 `PDFAConversionOptionSpec` 報を指定するオブジェクト
   このメ `toPDFA` ソッドは、PDF/A `PDFAConversionResult` ドキュメントを含むオブジェクトを返します。

1. PDF/Aドキュメントの保存

   * オブジェクトのメソッドを呼び出して、PDF/Aドキュ `PDFAConversionResult` メントを取得 `getPDFA` します。 このメソッドは、PDF/A `com.adobe.idp.Document` ドキュメントを表すオブジェクトを返します。
   * PDF/Aフ `java.io.File` ァイルを表すオブジェクトを作成します。 ファイル名の拡張子が.pdfであることを確認します。
   * オブジェクトのメソッドを呼び出し、オブジェクトを渡すこ `com.adobe.idp.Document` とで、ファイルにPDF/A `copyToFile` データを入力 `java.io.File` します。

**関連トピック**

[PDF/Aドキュメントの操作](pdf-a-documents.md#working-with-pdf-a-documents)

[クイックスタート（SOAPモード）:Java APIを使用したドキュメントからPDF/Aドキュメントへの変換](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-converting-a-document-to-a-pdf-a-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したドキュメントのPDF/Aドキュメントへの変換 {#convert-documents-to-pdf-a-documents-using-the-web-service-api}

DocConverter API（Webサービス）を使用してPDFドキュメントをPDF/Aドキュメントに変換します。

1. プロジェクトファイルを含める

   * DocConverter WSDLを使用するMicrosoft .NETクライアントアセンブリを作成します。
   * Microsoft .NETクライアントアセンブリを参照します。

1. DocConvertクライアントの作成

   * Microsoft .NETクライアントアセンブリを使用して、デフォルトのコンストラクタ `DocConverterServiceService` ーを呼び出してオブジェクトを作成します。
   * オブジェクト `DocConverterServiceService` のデータメ `Credentials` ンバーに、ユーザー `System.Net.NetworkCredential` 名とパスワードの値を指定する値を設定します。

1. PDF/Aドキュメントに変換するPDFドキュメントの参照

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、PDF/Aドキュメントに変換されたPDFドキュメントを保存するために使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、PDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイト配列、開 `System.IO.FileStream` 始位置、ストリ `Read` ーム長を渡すことによって、バイト配列にストリームデータを設定します。
   * オブジェクト `BLOB` にバイト配列の内容をプロ `binaryData` パティに割り当てて、オブジェクトを設定します。

1. トラッキング情報の設定

   * コンストラクタを使用して `PDFAConversionOptionSpec` オブジェクトを作成します。
   * 情報追跡レベルを設定するには、追跡レベルを指定する値をオブジェクトのデータメ `PDFAConversionOptionSpec` ンバに割り `logLevel` 当てます。 例えば、このデータメンバーに `FINE` 値を割り当てます。

1. ドキュメントの変換

   オブジェクトのメソッドを呼び出し、次の値を渡して、PDFドキュ `DocConverterServiceService` メントをPDF/A `toPDFA` ドキュメントに変換します。

   * 変換す `BLOB` るPDFドキュメントを含むオブジェクトです
   * 追跡情 `PDFAConversionOptionSpec` 報を指定するオブジェクト
   このメ `toPDFA` ソッドは、PDF/A `PDFAConversionResult` ドキュメントを含むオブジェクトを返します。

1. PDF/Aドキュメントの保存

   * オブジェクト `BLOB` のデータメンバーの値を取得して、PDF/Aドキュメントを保存するオブ `PDFAConversionResult` ジェクトを `PDFADocument` 作成します。
   * オブジェクトを使用して返されたオブジェクトの内容を `BLOB` 格納するバイト配列を作成し `PDFAConversionResult` ます。 オブジェクトのデータメンバーの値を取得して、バ `BLOB` イト配列を `binaryData` 設定します。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、PDF/Aドキュメントのファイルの場所を表すstring値を渡します。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡すことで、バ `System.IO.BinaryWriter` イト配列の内 `Write` 容をPDFファイルに書き込みます。

**関連トピック**

[PDF/Aドキュメントの操作](pdf-a-documents.md#working-with-pdf-a-documents)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64エンコーディングを使用する.NETクライアントアセンブリの作成](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## PDF/A準拠のプログラムによる判断 {#programmatically-determining-pdf-a-compliancy}

DocConverterサービスを使用して、PDFドキュメントがPDF/Aに準拠しているかどうかを確認できます。 PDF/AドキュメントおよびPDFドキュメントをPDF/Aドキュメントに変換する方法について詳しくは、「ドキュメントからPDF/Aドキュメ [ントへの変換」を参照してください](pdf-a-documents.md#converting-documents-to-pdf-a-documents)。

>[!NOTE]
>
>For more information about the DocConverter service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-1}

PDF/Aの準拠を判断するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. DocConvertクライアントの作成
1. PDF/Aの準拠性の判定に使用されるPDFドキュメントを参照します。
1. 実行時オプションを設定します。
1. PDFドキュメントに関する情報を取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-utilities.jar（AEM FormsがJBoss Application serverにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsがJBoss Application Serverにデプロイされている場合に必要）

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**DocConvertクライアントの作成**

プログラムでDocConverter操作を実行する前に、DocConverterクライアントを作成する必要があります。 Java APIを使用している場合は、オブジェクトを作成し `DocConverterServiceClient` ます。 DocConverter webサービスAPIを使用している場合は、オブジェクトを作成し `DocConverterServiceService` ます。

**PDF/Aの準拠性の判定に使用するPDFドキュメントの参照**

PDFドキュメントがPDF/Aに準拠しているかどうかを判断するには、PDFドキュメントを参照し、DocConverterサービスに渡す必要があります。

**実行時オプションの設定**

変換プロセス中に追跡する情報の量を決定する実行時オプションを設定できます。 つまり、PDFドキュメントをPDF/Aドキュメントに変換する際にDocConverterサービスが追跡する情報の量を指定する9種類のレベルを設定できます。

**PDFドキュメントに関する情報の取得**

DocConverterサービスクライアントを作成し、PDFドキュメントを参照し、実行時のオプションを設定した後、PDFドキュメントがPDF/A準拠のドキュメントであるかどうかを判断できます。

**関連トピック**

[Java APIを使用したPDF/Aの準拠の判定](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-java-api)

[WebサービスAPIを使用したPDF/Aの準拠の確認](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java APIを使用したPDF/Aの準拠の判定 {#determine-pdf-a-compliancy-using-the-java-api}

Java APIを使用してPDF/Aの準拠性を判断します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-docconverter-client.jarなどのクライアントJARファイルを含めます。

1. DocConvertクライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `DocConverterServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. PDF/Aの準拠性の判定に使用するPDFドキュメントの参照

   * コンストラ `java.io.FileInputStream` クターを使用し、PDFファイルの場所を指定するstring値を渡して、変換するPDFドキュメントを表すオブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 実行時オプションの設定

   * コンストラクタを使用して `PDFAValidationOptionSpec` オブジェクトを作成します。
   * オブジェクトのメソッドを呼び出して渡すこ `PDFAValidationOptionSpec` とで、準拠レベル `setCompliance` を設定しま `PDFAValidationOptionSpec.Compliance.PDFA_1B`す。
   * オブジェクトのメソッドを呼び出し、トラッキ `PDFAValidationOptionSpec` ングレベルを指 `setLogLevel` 定する文字列値を渡して、情報トラッキングレベルを設定します。 For example, pass the value `FINE`. 各値について詳しくは、『 `setLogLevel` AEM Forms APIリファレンス』の [メソッドを参](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)照してください。

1. PDFドキュメントに関する情報の取得

   オブジェクトのメソッドを呼び出し、次 `DocConverterServiceClient` の値を渡して、PDF/A `isPDFA` の準拠性を判断します。

   * PDFドキ `com.adobe.idp.Document` ュメントを含むオブジェクトです。
   * 実行時 `PDFAValidationOptionSpec` のオプションを指定するオブジェクトです。
   このメ `isPDFA` ソッドは、この操 `PDFAValidationResult` 作の結果を含むオブジェクトを返します。

**関連トピック**

[PDF/Aドキュメントの操作](pdf-a-documents.md#working-with-pdf-a-documents)

[クイックスタート（SOAPモード）:Java APIを使用したPDF/Aの準拠の判定](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-determining-pdf-a-compliancy-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したPDF/Aの準拠の確認 {#determine-pdf-a-compliancy-using-the-web-service-api}

WebサービスAPIを使用してPDF/Aの準拠性を判断します。

1. プロジェクトファイルを含める

   * DocConverter WSDLを使用するMicrosoft .NETクライアントアセンブリを作成します。
   * Microsoft .NETクライアントアセンブリを参照します。

1. DocConvertクライアントの作成

   * Microsoft .NETクライアントアセンブリを使用して、デフォルトのコンストラクタ `DocConverterServiceService` ーを呼び出してオブジェクトを作成します。
   * オブジェクト `DocConverterServiceService` のデータメ `Credentials` ンバーに、ユーザー `System.Net.NetworkCredential` 名とパスワードの値を指定する値を設定します。

1. PDF/Aの準拠性の判定に使用するPDFドキュメントの参照

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、PDF/Aドキュメントに変換されたPDFドキュメントを保存するために使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、PDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイト配列、開 `System.IO.FileStream` 始位置、ストリ `Read` ーム長を渡すことによって、バイト配列にストリームデータを設定します。
   * オブジェクト `BLOB` にバイト配列の内容をプロ `binaryData` パティに割り当てて、オブジェクトを設定します。

1. 実行時オプションの設定

   * コンストラクタを使用して `PDFAValidationOptionSpec` オブジェクトを作成します。
   * 準拠レベルを設定するには、オブジェクトの `PDFAValidationOptionSpec` データメンバ `compliance` ーに値を割り当てま `PDFAConversionOptionSpec_Compliance.PDFA_1B`す。
   * オブジェクトのデータメンバーに値を割り当て `PDFAValidationOptionSpec` て、情報の追 `resultLevel` 跡レベルを設定しま `PDFAValidationOptionSpec_ResultLevel.DETAILED`す。

1. PDFドキュメントに関する情報の取得

   オブジェクトのメソッドを呼び出し、次 `DocConverterServiceService` の値を渡して、PDF/A `isPDFA` の準拠性を判断します。

   * PDFドキ `BLOB` ュメントを含むオブジェクトです。
   * 実行時 `PDFAValidationOptionSpec` のオプションを含むオブジェクトです。
   このメ `isPDFA` ソッドは、この操 `PDFAValidationResult` 作の結果を含むオブジェクトを返します。

**関連トピック**

[PDF/Aドキュメントの操作](pdf-a-documents.md#working-with-pdf-a-documents)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64エンコーディングを使用する.NETクライアントアセンブリの作成](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
