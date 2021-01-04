---
title: PDF/Aドキュメントの操作
seo-title: PDF/Aドキュメントの操作
description: DocConverterサービスを使用して、PDFドキュメントがPDF/Aドキュメントであるかどうかを確認し、PDFドキュメントをPDF/Aドキュメントに変換します。
seo-description: DocConverterサービスを使用して、PDFドキュメントがPDF/Aドキュメントであるかどうかを確認し、PDFドキュメントをPDF/Aドキュメントに変換します。
uuid: c258d253-068a-4412-955a-21d8a4792d6f
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 1e6cc554-aef1-463c-906b-634b80a27917
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '2386'
ht-degree: 7%

---


# PDF/Aドキュメントの操作{#working-with-pdf-a-documents}

**DocConverterサービスについて**

DocConverterサービスは、PDFドキュメントをPDA/Aドキュメントに変換できます。 このサービスを使用して、次のタスクを実行できます。

* PDFドキュメントをPDF/Aドキュメントに変換します。 ([ドキュメントをPDF/Aドキュメントに変換する](pdf-a-documents.md#converting-documents-to-pdf-a-documents)を参照)。
* PDFドキュメントがPDF/Aドキュメントかどうかを確認します。 （「[PDF/Aへの準拠をプログラムで判断する](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)」を参照）。

>[!NOTE]
>
>DocConverterサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

## ドキュメントをPDF/Aドキュメントに変換{#converting-documents-to-pdf-a-documents}

DocConverterサービスを使用すると、PDFドキュメントをPDF/Aドキュメントに変換できます。 PDF/Aはドキュメントのコンテンツを長期間保存するためのアーカイブ形式なので、すべてのフォントが埋め込まれ、ファイルは圧縮されません。 その結果、通常、PDF/A ドキュメントは標準の PDF ドキュメントよりも大きくなります。また、PDF/A ドキュメントには、オーディオおよびビデオコンテンツは含まれません。PDFドキュメントをPDF/Aドキュメントに変換する前に、PDFドキュメントがPDF/Aドキュメントでないことを確認してください。

PDF/A-1仕様は、AとBの2つの準拠レベルで構成されています。主な違いは、論理構造（アクセシビリティ）のサポートですが、準拠レベルBには必要ありません。準拠レベルにかかわらず、PDF/A-1では、生成されたPDF/Aドキュメントにすべてのフォントが埋め込まれます。 現時点では、検証（および変換）ではPDF/A-1bのみがサポートされています。

PDF/AはPDFドキュメントのアーカイブの標準ですが、標準のPDFドキュメントが会社の要件を満たしている場合、PDF/Aをアーカイブに使用する必要はありません。 PDF/A標準の目的は、長期にわたるアーカイブやドキュメントの保存のニーズに対応したPDFファイルを作成することです。

>[!NOTE]
>
>DocConverterサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順{#summary-of-steps}の概要

PDFドキュメントをPDF/Aドキュメントに変換するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. DocConvertクライアントの作成
1. PDFドキュメントを参照してPDF/Aドキュメントに変換します。
1. トラッキング情報を設定します。
1. ドキュメントを変換します。
1. PDF/Aドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めます。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-utilities.jar(AEM FormsがJBoss Application Serverにデプロイされている場合に必要)
* jbossall-client.jar(AEM FormsがJBoss Application Serverにデプロイされている場合に必要)

これらのJARファイルの場所について詳しくは、「[AEM FormsJavaライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)」を参照してください。

**DocConvertクライアントの作成**

プログラムによってDocConverter操作を実行する前に、DocConverterクライアントを作成する必要があります。 Java APIを使用している場合は、`DocConverterServiceClient`オブジェクトを作成します。 DocConverter WebサービスAPIを使用している場合は、`DocConverterServiceService`オブジェクトを作成します。

**PDFドキュメントを参照してPDF/Aドキュメントに変換**

PDF/Aドキュメントに変換するPDFドキュメントを取得します。 AcrobatフォームなどのPDFドキュメントをPDF/Aドキュメントに変換しようとすると、例外が発生します。

**トラッキング情報の設定**

変換プロセス中に追跡する情報の量を決定する実行時オプションを設定できます。 つまり、9つの異なるレベルを設定して、PDFドキュメントをPDF/Aドキュメントに変換するときに、DocConverterサービスで追跡される情報の量を指定できます。

**ドキュメントの変換**

DocConverterサービスクライアントを作成した後、変換するPDFドキュメントを参照し、追跡する情報の量を指定する実行時オプションを設定します。PDFドキュメントをPDF/Aドキュメントに変換できます。

**PDF/Aドキュメントの保存**

PDF/AドキュメントをPDFファイルとして保存できます。

**関連トピック**

[Java APIを使用したPDF/Aドキュメントへのドキュメントの変換](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-java-api)

[WebサービスAPIを使用してドキュメントをPDF/Aドキュメントに変換する](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDF/Aへの準拠をプログラムで判断する](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)

### Java API {#convert-documents-to-pdf-a-documents-using-the-java-api}を使用してドキュメントをPDF/Aドキュメントに変換

Java APIを使用してPDFドキュメントをPDF/Aドキュメントに変換します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-docconverter-client.jarなどのクライアントJARファイルを含めます。

1. DocConvertクライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `DocConverterServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. PDFドキュメントを参照してPDF/Aドキュメントに変換

   * コンストラクターを使用し、PDFファイルの場所を指定するstring値を渡して、変換するPDFドキュメントを表す`java.io.FileInputStream`オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. トラッキング情報の設定

   * コンストラクタを使用して `PDFAConversionOptionSpec` オブジェクトを作成します。
   * `PDFAConversionOptionSpec`オブジェクトの`setLogLevel`メソッドを呼び出し、追跡レベルを指定する文字列値を渡して、情報追跡レベルを設定します。 例えば、値`FINE`を渡します。 異なる値について詳しくは、『[AEM FormsAPIリファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)』の`setLogLevel`メソッドを参照してください。

1. ドキュメントの変換

   `DocConverterServiceClient`オブジェクトの`toPDFA`メソッドを呼び出し、次の値を渡して、PDFドキュメントをPDF/Aドキュメントに変換します。

   * 変換するPDFドキュメントが含まれる`com.adobe.idp.Document`オブジェクトです
   * 追跡情報を指定する`PDFAConversionOptionSpec`オブジェクト

   `toPDFA`メソッドは、PDF/Aドキュメントを含む`PDFAConversionResult`オブジェクトを返します。

1. PDF/Aドキュメントの保存

   * `PDFAConversionResult`オブジェクトの`getPDFA`メソッドを呼び出して、PDF/Aドキュメントを取得します。 このメソッドは、PDF/Aドキュメントを表す`com.adobe.idp.Document`オブジェクトを返します。
   * PDF/Aファイルを表す`java.io.File`オブジェクトを作成します。 ファイル名の拡張子が.pdfであることを確認します。
   * `com.adobe.idp.Document`オブジェクトの`copyToFile`メソッドを呼び出し、`java.io.File`オブジェクトを渡すことで、PDF/Aデータをファイルに入力します。

**関連トピック**

[PDF/Aドキュメントの操作](pdf-a-documents.md#working-with-pdf-a-documents)

[クイック開始（SOAPモード）:Java APIを使用したドキュメントのPDF/Aドキュメントへの変換](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-converting-a-document-to-a-pdf-a-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#convert-documents-to-pdf-a-documents-using-the-web-service-api}を使用してドキュメントをPDF/Aドキュメントに変換する

DocConverter API（Webサービス）を使用してPDFドキュメントをPDF/Aドキュメントに変換します。

1. プロジェクトファイルを含める

   * DocConverter WSDLを使用するMicrosoft .NETクライアントアセンブリを作成します。
   * Microsoft .NETクライアントアセンブリを参照します。

1. DocConvertクライアントの作成

   * Microsoft .NETクライアントアセンブリを使用して、`DocConverterServiceService`オブジェクトを作成します。その場合は、デフォルトのコンストラクタを呼び出します。
   * `DocConverterServiceService`オブジェクトの`Credentials`データメンバーに、ユーザー名とパスワードの値を指定する`System.Net.NetworkCredential`値を設定します。

1. PDFドキュメントを参照してPDF/Aドキュメントに変換

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、PDF/Aドキュメントに変換されたPDFドキュメントを保存するために使用します。
   * コンストラクターを呼び出し、PDFドキュメントーのファイルの場所と、ファイルを開くモードを表す文字列値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得して、バイト配列のサイズを決定できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * `BLOB`オブジェクトに`binaryData`プロパティを割り当て、バイト配列の内容を指定します。

1. トラッキング情報の設定

   * コンストラクタを使用して `PDFAConversionOptionSpec` オブジェクトを作成します。
   * 追跡レベルを指定する値を`PDFAConversionOptionSpec`オブジェクトの`logLevel`データメンバに割り当てて、情報追跡レベルを設定します。 例えば、値`FINE`をこのデータメンバーに割り当てます。

1. ドキュメントの変換

   `DocConverterServiceService`オブジェクトの`toPDFA`メソッドを呼び出し、次の値を渡して、PDFドキュメントをPDF/Aドキュメントに変換します。

   * 変換するPDFドキュメントが含まれる`BLOB`オブジェクトです
   * 追跡情報を指定する`PDFAConversionOptionSpec`オブジェクト

   `toPDFA`メソッドは、PDF/Aドキュメントを含む`PDFAConversionResult`オブジェクトを返します。

1. PDF/Aドキュメントの保存

   * `PDFAConversionResult`オブジェクトの`PDFADocument`データメンバーの値を取得して、PDF/Aドキュメントを格納する`BLOB`オブジェクトを作成します。
   * `PDFAConversionResult`オブジェクトを使用して返された`BLOB`オブジェクトの内容を格納するバイト配列を作成します。 `BLOB`オブジェクトの`binaryData`データメンバの値を取得して、バイト配列を入力します。
   * コンストラクターを呼び出し、PDF/Aドキュメントーのファイルの場所を表す文字列値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * コンストラクターを呼び出して`System.IO.FileStream`オブジェクトを渡し、`System.IO.BinaryWriter`オブジェクトを作成します。
   * `System.IO.BinaryWriter`オブジェクトの`Write`メソッドを呼び出し、バイト配列を渡すことで、バイト配列の内容をPDFファイルに書き込みます。

**関連トピック**

[PDF/Aドキュメントの操作](pdf-a-documents.md#working-with-pdf-a-documents)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64エンコーディングを使用する.NETクライアントアセンブリの作成](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## PDF/Aへの準拠をプログラムで判断する{#programmatically-determining-pdf-a-compliancy}

DocConverterサービスを使用すると、PDFドキュメントがPDF/Aに準拠しているかどうかを確認できます。 PDF/AドキュメントおよびPDFドキュメントをPDF/Aドキュメントに変換する方法について詳しくは、[ドキュメントをPDF/Aドキュメントに変換する](pdf-a-documents.md#converting-documents-to-pdf-a-documents)を参照してください。

>[!NOTE]
>
>DocConverterサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順{#summary_of_steps-1}の概要

PDF/Aの互換性を判断するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. DocConvertクライアントの作成
1. PDF/Aの準拠性の判定に使用されるPDFドキュメントを参照します。
1. 実行時オプションを設定します。
1. PDFドキュメントに関する情報を取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めます。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-utilities.jar(AEM FormsがJBoss Application Serverにデプロイされている場合に必要)
* jbossall-client.jar(AEM FormsがJBoss Application Serverにデプロイされている場合に必要)

これらのJARファイルの場所について詳しくは、「[AEM FormsJavaライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)」を参照してください。

**DocConvertクライアントの作成**

プログラムによってDocConverter操作を実行する前に、DocConverterクライアントを作成する必要があります。 Java APIを使用している場合は、`DocConverterServiceClient`オブジェクトを作成します。 DocConverter WebサービスAPIを使用している場合は、`DocConverterServiceService`オブジェクトを作成します。

**PDF/Aの準拠性の判定に使用されるPDFドキュメントの参照**

PDFドキュメントがPDF/Aに準拠しているかどうかを確認するには、PDFドキュメントを参照して、DocConverterサービスに渡す必要があります。

**実行時オプションの設定**

変換プロセス中に追跡する情報の量を決定する実行時オプションを設定できます。 つまり、9種類の異なるレベルを設定して、PDFドキュメントをPDF/Aドキュメントに変換する場合に、DocConverterサービスで追跡される情報の量を指定できます。

**PDFドキュメントに関する情報の取得**

DocConverterサービスクライアントを作成し、PDFドキュメントを参照し、実行時オプションを設定した後、PDFドキュメントがPDF/A準拠のドキュメントであるかどうかを確認できます。

**関連トピック**

[Java APIを使用したPDF/Aへの準拠の確認](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-java-api)

[WebサービスAPIを使用したPDF/Aの準拠の確認](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API {#determine-pdf-a-compliancy-using-the-java-api}を使用したPDF/Aの準拠性の判定

Java APIを使用してPDF/Aへの準拠を確認します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-docconverter-client.jarなどのクライアントJARファイルを含めます。

1. DocConvertクライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `DocConverterServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. PDF/Aの準拠性の判定に使用されるPDFドキュメントの参照

   * コンストラクターを使用し、PDFファイルの場所を指定するstring値を渡して、変換するPDFドキュメントを表す`java.io.FileInputStream`オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 実行時オプションの設定

   * コンストラクタを使用して `PDFAValidationOptionSpec` オブジェクトを作成します。
   * `PDFAValidationOptionSpec`オブジェクトの`setCompliance`メソッドを呼び出し、`PDFAValidationOptionSpec.Compliance.PDFA_1B`を渡して、準拠レベルを設定します。
   * `PDFAValidationOptionSpec`オブジェクトの`setLogLevel`メソッドを呼び出し、追跡レベルを指定する文字列値を渡して、情報追跡レベルを設定します。 例えば、値`FINE`を渡します。 異なる値について詳しくは、『[AEM FormsAPIリファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)』の`setLogLevel`メソッドを参照してください。

1. PDFドキュメントに関する情報の取得

   `DocConverterServiceClient`オブジェクトの`isPDFA`メソッドを呼び出し、次の値を渡して、PDF/Aの準拠性を判断します。

   * PDFドキュメントを含む`com.adobe.idp.Document`オブジェクトです。
   * 実行時オプションを指定する`PDFAValidationOptionSpec`オブジェクト。

   `isPDFA`メソッドは、この操作の結果を含む`PDFAValidationResult`オブジェクトを返します。

**関連トピック**

[PDF/Aドキュメントの操作](pdf-a-documents.md#working-with-pdf-a-documents)

[クイック開始（SOAPモード）:Java APIを使用したPDF/Aへの準拠の判断](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-determining-pdf-a-compliancy-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#determine-pdf-a-compliancy-using-the-web-service-api}を使用したPDF/Aの準拠性の判定

WebサービスAPIを使用して、PDF/Aへの準拠を確認します。

1. プロジェクトファイルを含める

   * DocConverter WSDLを使用するMicrosoft .NETクライアントアセンブリを作成します。
   * Microsoft .NETクライアントアセンブリを参照します。

1. DocConvertクライアントの作成

   * Microsoft .NETクライアントアセンブリを使用して、`DocConverterServiceService`オブジェクトを作成します。その場合は、デフォルトのコンストラクタを呼び出します。
   * `DocConverterServiceService`オブジェクトの`Credentials`データメンバーに、ユーザー名とパスワードの値を指定する`System.Net.NetworkCredential`値を設定します。

1. PDF/Aの準拠性の判定に使用されるPDFドキュメントの参照

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、PDF/Aドキュメントに変換されたPDFドキュメントを保存するために使用します。
   * コンストラクターを呼び出し、PDFドキュメントーのファイルの場所と、ファイルを開くモードを表す文字列値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得して、バイト配列のサイズを決定できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * `BLOB`オブジェクトに`binaryData`プロパティを割り当て、バイト配列の内容を指定します。

1. 実行時オプションの設定

   * コンストラクタを使用して `PDFAValidationOptionSpec` オブジェクトを作成します。
   * `PDFAValidationOptionSpec`オブジェクトの`compliance`データメンバに値`PDFAConversionOptionSpec_Compliance.PDFA_1B`を割り当てて、準拠レベルを設定します。
   * `PDFAValidationOptionSpec`オブジェクトの`resultLevel`データメンバに値`PDFAValidationOptionSpec_ResultLevel.DETAILED`を割り当てて、情報追跡レベルを設定します。

1. PDFドキュメントに関する情報の取得

   `DocConverterServiceService`オブジェクトの`isPDFA`メソッドを呼び出し、次の値を渡して、PDF/Aの準拠性を判断します。

   * PDFドキュメントを含む`BLOB`オブジェクトです。
   * 実行時オプションを含む`PDFAValidationOptionSpec`オブジェクトです。

   `isPDFA`メソッドは、この操作の結果を含む`PDFAValidationResult`オブジェクトを返します。

**関連トピック**

[PDF/Aドキュメントの操作](pdf-a-documents.md#working-with-pdf-a-documents)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64エンコーディングを使用する.NETクライアントアセンブリの作成](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
