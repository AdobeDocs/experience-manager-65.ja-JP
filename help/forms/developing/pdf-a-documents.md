---
title: PDF/A ドキュメントの操作
seo-title: Working with PDF/A Documents
description: DocConverter サービスを使用して、PDF ドキュメントが PDF/A ドキュメントかどうかを判断し、PDF ドキュメントであればこれを PDF/A ドキュメントに変換します。
seo-description: Use the  DocConverter service to determine if a PDF document is a PDF/A document and convert PDF documents to PDF/A documents.
uuid: c258d253-068a-4412-955a-21d8a4792d6f
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 1e6cc554-aef1-463c-906b-634b80a27917
role: Developer
exl-id: 966c3554-25df-4467-866e-11c43cc15b58
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2358'
ht-degree: 100%

---

# PDF/A ドキュメントの操作 {#working-with-pdf-a-documents}

**DocConverter サービスについて**

DocConverter サービスは、PDF ドキュメントを PDA/A ドキュメントに変換できます。このサービスを使用して、次のタスクを実行できます。

* PDF ドキュメントを PDF/A ドキュメントに変換する（[ドキュメントを PDF/A ドキュメントに変換する](pdf-a-documents.md#converting-documents-to-pdf-a-documents)を参照。）
* PDF ドキュメントが PDF/A ドキュメントかどうかを判断する（[プログラムによる PDF/A の適合性の判断](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)を参照。）

>[!NOTE]
>
>DocConverter サービスについて詳しくは、[AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

## ドキュメントを PDF/A ドキュメントに変換する {#converting-documents-to-pdf-a-documents}

DocConverter サービスを使用して、PDF ドキュメントを PDF/A ドキュメントに変換できます。PDF/A はドキュメントの内容を長期保存するためのアーカイブ形式なので、すべてのフォントが埋め込まれ、ファイルが非圧縮になります。変換の結果、PDF/A ドキュメントのサイズは通常、標準の PDF ドキュメントより大きくなります。なお、PDF/A ドキュメントには、オーディオおよびビデオのコンテンツは含まれません。PDF ドキュメントを PDF/A ドキュメントに変換する前に、PDF ドキュメントが PDF/A ドキュメントでないことを確認してください。

PDF/A-1 仕様は、A と B という 2 つの適合レベルで構成されます。2 つの主な違いは、論理構造（アクセシビリティ）のサポートに関するもので、適合レベル B には必要ありません。いずれの適合レベルであれ、PDF/A-1 では、生成された PDF/A ドキュメントにすべてのフォントが埋め込まれます。現時点では、検証（および変換）では PDF/A-1b のみがサポートされています。

PDF/A は PDFドキュメントをアーカイブするときの標準ですが、標準の PDF ドキュメントが会社の要件に適合している場合は、アーカイブに PDF/A を使用する必要はありません。PDF/A 規格の目的は、長期的なアーカイブやドキュメントの保存のニーズに対応できる PDF ファイルを構築することです。

>[!NOTE]
>
>DocConverter サービスについて詳しくは、[AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary-of-steps}

PDF ドキュメントを PDF/A ドキュメントに変換するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. DocConvert クライアントの作成
1. PDF ドキュメントを参照して、PDF/A ドキュメントに変換します。
1. トラッキング情報を設定します。
1. ドキュメントを変換します。
1. PDF/A ドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、必ずプロキシファイルを含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-utilities.jar（AEM Forms が JBoss Application Server にデプロイされている場合に必要）
* jbossall-client.jar（AEM Forms が JBoss Application Server にデプロイされている場合に必要）

これらの JAR ファイルの場所については、[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。

**DocConvert クライアントの作成**

DocConverter の操作をプログラム的に実行する前に、DocConverter クライアントを作成する必要があります。Java API を使用する場合は、`DocConverterServiceClient` オブジェクトを作成します。DocConverter web サービス API を使用している場合は、 `DocConverterServiceService` オブジェクトを作成してください。

**PDF ドキュメントを参照して PDF/A ドキュメントに変換**

PDF ドキュメントを取得して PDF/A ドキュメントに変換します。Acrobat フォームなどの PDF ドキュメントを PDF/A ドキュメントに変換しようとすると、例外が発生します。

**トラッキング情報を設定**

変換処理中に追跡する情報の量を指定する実行時オプションを設定できます。つまり、PDF ドキュメントを PDF/A ドキュメントに変換する際に DocConverter サービスが追跡する情報の量を 9 つの異なるレベルで設定できます。

**ドキュメントを変換**

DocConverter サービスクライアントを作成して、変換する PDF ドキュメントを参照しながら、追跡すべき情報の量を指定する実行時オプションを設定した後、PDF ドキュメントをPDF/A ドキュメントに変換できます。

**PDF/A ドキュメントを保存**

PDF/A ドキュメントは、PDF ファイルとして保存できます。

**関連トピック**

[Java API を使用して、PDF/A ドキュメントにドキュメントを変換する](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-java-api)

[Web サービス API を使用してドキュメントを PDF/A ドキュメントに変換](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[プログラムによる PDF/A の適合性の判断](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)

### Java API を使用して、PDF/A ドキュメントにドキュメントを変換する {#convert-documents-to-pdf-a-documents-using-the-java-api}

Java API を使用して、PDF ドキュメントを PDF/A ドキュメントに変換します。

1. プロジェクトファイルを含める

   adobe-docconverter-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. DocConvert クライアントの作成

   * 接続プロパティが格納された `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用し、`DocConverterServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. PDF ドキュメントを参照して PDF/A ドキュメントに変換

   * コンストラクターを使用して、変換ファイルの場所を指定する文字列値を渡すことによって、変換する PDF ドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクターを使用し、`java.io.FileInputStream` オブジェクトを渡すことによって、`com.adobe.idp.Document` オブジェクトを作成します。

1. トラッキング情報を設定

   * コンストラクターを使用して `PDFAConversionOptionSpec` オブジェクトを作成します。
   * `PDFAConversionOptionSpec` オブジェクトの `setLogLevel` メソッドを呼び出し、トラッキングレベルを指定する文字列値を渡すことにより、情報のトラッキングレベルを設定します。 例えば、値 `FINE` を渡します。様々な値について詳しくは、[AEM Forms API リファレンス](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ja)の `setLogLevel` メソッドを参照してください。

1. ドキュメントを変換

   `DocConverterServiceClient` オブジェクトの `toPDFA` メソッドを呼び出して次の値を渡すことによって、PDF ドキュメントを PDF/A ドキュメントに変換します。

   * 変換する PDF ドキュメントを含む `com.adobe.idp.Document` オブジェクト
   * トラッキング情報を指定する `PDFAConversionOptionSpec` オブジェクト

   `toPDFA` メソッドは、PDF/A ドキュメントを含む `PDFAConversionResult` オブジェクトを返します。

1. PDF/A ドキュメントを保存

   * `PDFAConversionResult` オブジェクトの `getPDFA` メソッドを呼び出して PDF/A ドキュメントを取得します。 このメソッドは、PDF/A ドキュメントを表す `com.adobe.idp.Document` オブジェクトを返します。
   * PDF/A ファイルを表す `java.io.File` オブジェクトを作成します。ファイル名の拡張子が .pdf であることを確認します。
   *  `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを呼び出して `java.io.File` オブジェクトを渡すことによって、PDF/A データをファイルに入力します。

**関連トピック**

[PDF/A ドキュメントの操作](pdf-a-documents.md#working-with-pdf-a-documents)

[クイックスタート（SOAP モード）：Java API を使用した PDF/A ドキュメントへのドキュメントの変換](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-converting-a-document-to-a-pdf-a-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用してドキュメントを PDF/A ドキュメントに変換 {#convert-documents-to-pdf-a-documents-using-the-web-service-api}

DocConverter API（web サービス）を使用して、PDF ドキュメントを PDF/A ドキュメントに変換します。

1. プロジェクトファイルを含める

   * DocConverter WSDL を使用する Microsoft .NET クライアントアセンブリを作成します。
   * Microsoft .NET クライアントアセンブリを参照します。

1. DocConvert クライアントの作成

   * Microsoft .NET クライアントアセンブリを使用して、デフォルトのコンストラクターを呼び出すことによって `DocConverterServiceService` オブジェクトを作成します。
   * `DocConverterServiceService` オブジェクトの `Credentials` データメンバーを、ユーザー名とパスワードの値を指定する `System.Net.NetworkCredential` 値で設定します。

1. PDF ドキュメントを参照して PDF/A ドキュメントに変換

   * コンストラクターを使用して `BLOB` オブジェクトを作成します。`BLOB` オブジェクトは、PDF/A ドキュメントに変換される PDF ドキュメントを格納するために使用されます。
   * コンストラクターを呼び出し、暗号化する PDF ドキュメントのファイルの場所とファイルを開くモードを表す文字列値を渡して、`System.IO.FileStream` オブジェクトを作成します。
   * `System.IO.FileStream` オブジェクトの内容を格納するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することで、バイト配列のサイズを決定できます。
   * バイト配列にストリームデータを入力するには、`System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出し、バイト配列、開始位置、読み取るストリーム長を渡します。
   * `binaryData` プロパティにバイト配列のコンテンツを割り当てることによって `BLOB` オブジェクトを設定します。

1. トラッキング情報を設定

   * コンストラクターを使用して `PDFAConversionOptionSpec` オブジェクトを作成します。
   * トラッキングレベルを指定する値を `PDFAConversionOptionSpec` オブジェクトの `logLevel` データメンバーに割り当てることによって、情報トラッキングレベルを設定します。例えば、`FINE` の値をこのデータメンバーに割り当てます。

1. ドキュメントを変換

   `DocConverterServiceService` オブジェクトの `toPDFA` メソッドを呼び出して次の値を渡すことによって、PDF ドキュメントを PDF/A ドキュメントに変換します。

   * 変換する PDF ドキュメントを含む `BLOB` オブジェクト
   * トラッキング情報を指定する `PDFAConversionOptionSpec` オブジェクト

   `toPDFA` メソッドは、PDF/A ドキュメントを含む `PDFAConversionResult` オブジェクトを返します。

1. PDF/A ドキュメントを保存

   * PDF/A ドキュメントを格納する `BLOB` オブジェクトを作成するには、`PDFAConversionResult` オブジェクトの `PDFADocument` データメンバーの値を取得します。
   * `PDFAConversionResult` オブジェクトを使用して、返された `BLOB` オブジェクトの内容を格納するバイト配列を作成します。 `BLOB` オブジェクトの `binaryData` データメンバーの値を取得して、バイト配列に入力します。
   * `System.IO.FileStream` オブジェクトを作成するには、そのコンストラクターを呼び出し、PDF/A ドキュメントのファイルの場所を表す文字列の値を渡します。
   * コンストラクターを使用して `System.IO.FileStream` オブジェクトを渡すことにより、`System.IO.BinaryWriter` オブジェクトを作成します。
   * `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを呼び出して、バイト配列を渡すことによって、バイト配列の内容を PDF ファイルに書き込みます。

**関連トピック**

[PDF/A ドキュメントの操作](pdf-a-documents.md#working-with-pdf-a-documents)

[Base64 エンコーディングを使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64 エンコーディングを使用する .NET クライアントアセンブリの作成](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## プログラムによる PDF/A 準拠の判別 {#programmatically-determining-pdf-a-compliancy}

DocConverter サービスを使用すると、PDF ドキュメントが PDF/A に準拠しているかどうかを検証できます。PDF/A ドキュメントの詳細と、PDF ドキュメントを PDF/A ドキュメントに変換する方法について詳しくは、[ドキュメントを PDF/A ドキュメントに変換](pdf-a-documents.md#converting-documents-to-pdf-a-documents)を参照してください。

>[!NOTE]
>
>DocConverter サービスについて詳しくは、[AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary_of_steps-1}

PDF/A 準拠を判断するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. DocConvert クライアントの作成
1. PDF/A の準拠を判断するために使用される PDF ドキュメントを参照してください。
1. 実行時オプションを設定します。
1. PDF ドキュメントに関する情報を取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、必ずプロキシファイルを含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-utilities.jar（AEM Forms が JBoss Application Server にデプロイされている場合に必要）
* jbossall-client.jar（AEM Forms が JBoss Application Server にデプロイされている場合に必要）

これらの JAR ファイルの場所については、[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。

**DocConvert クライアントの作成**

DocConverter の操作をプログラム的に実行する前に、DocConverter クライアントを作成する必要があります。Java API を使用する場合は、`DocConverterServiceClient` オブジェクトを作成します。DocConverter web サービス API を使用する場合は、`DocConverterServiceService` オブジェクトを作成してください。

**PDF/A 準拠の判断に使用する PDFドキュメントを参照**

PDFドキュメントが PDF/ A に準拠しているかどうかを判断するには、PDFドキュメントを参照し、DocConverter サービスに渡す必要があります。

**実行時オプションの設定**

変換処理中に追跡する情報の量を指定する実行時オプションを設定できます。つまり、PDF ドキュメントを PDF/A ドキュメントに変換する際に DocConverter サービスが追跡する情報の量を 9 つの異なるレベルで設定できます。

**PDF ドキュメントに関する情報を取得**

DocConverter サービスクライアントを作成し、PDFドキュメントを参照し、実行時オプションを設定した後、PDFドキュメントが PDF/A 準拠のドキュメントであるかどうかを判断できます。

**関連トピック**

[Java API を使用して PDF/A の準拠を判断](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-java-api)

[Web サービス API を使用した PDF/A の準拠の判断](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API を使用して PDF/A の準拠を判断 {#determine-pdf-a-compliancy-using-the-java-api}

Java API を使用して PDF/A の準拠を判断します。

1. プロジェクトファイルを含める

   adobe-docconverter-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. DocConvert クライアントの作成

   * 接続プロパティが格納された `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して `ServiceClientFactory` オブジェクトを渡し、`DocConverterServiceClient` オブジェクトを作成します。

1. PDF/A 準拠の判断に使用する PDF ドキュメントを参照

   * コンストラクターを使用して、PDF ファイルの場所を指定する文字列値を渡すことにより、変換するインタラクティブ PDF ドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクターを使用して `java.io.FileInputStream` オブジェクトを渡すことにより、`com.adobe.idp.Document` オブジェクトを作成します。

1. 実行時オプションを設定

   * コンストラクターを使用して `PDFAValidationOptionSpec` オブジェクトを作成します。
   * `PDFAValidationOptionSpec` オブジェクトの `setCompliance` メソッドを呼び出し、`PDFAValidationOptionSpec.Compliance.PDFA_1B` を渡して、準拠レベルを設定します。
   * `PDFAValidationOptionSpec` オブジェクトの `setLogLevel` メソッドを呼び出し、トラッキングレベルを指定する文字列値を渡して、情報トラッキングレベルを指定します。例えば、値 `FINE` を渡します。様々な値について詳しくは、 [AEM Forms API リファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)の `setLogLevel` メソッドを参照してください。

1. PDF ドキュメントに関する情報を取得

   `DocConverterServiceClient` オブジェクトの `isPDFA` メソッドを呼び出し、次の値を渡して、PDF/A 準拠を判断します。

   * PDF ドキュメントが含まれる `com.adobe.idp.Document` オブジェクト。
   * 実行時オプションを指定する `PDFAValidationOptionSpec` オブジェクト。

   この `isPDFA` メソッドは、この操作の結果を格納する `PDFAValidationResult` オブジェクトを返します。

**関連トピック**

[PDF/A ドキュメントの操作](pdf-a-documents.md#working-with-pdf-a-documents)

[クイックスタート（SOAP モード）：Java API を使用した PDF/A の適合性の判断](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-determining-pdf-a-compliancy-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用した PDF/A の準拠の判断 {#determine-pdf-a-compliancy-using-the-web-service-api}

Web サービス API を使用して、PDF/A の準拠を判断します。

1. プロジェクトファイルを含める

   * DocConverter WSDL を使用する Microsoft .NET クライアントアセンブリを作成します。
   * Microsoft .NET クライアントアセンブリを参照します。

1. DocConvert クライアントの作成

   * Microsoft .NET クライアントアセンブリを使用して、デフォルトのコンストラクターを呼び出すことによって `DocConverterServiceService` オブジェクトを作成します。
   * `DocConverterServiceService` オブジェクトの `Credentials` データメンバーを、`System.Net.NetworkCredential` ユーザー名とパスワードの値を指定する値を使用して設定します。

1. PDF/A 準拠の判断に使用する PDF ドキュメントを参照

   * `BLOB` オブジェクトのコンストラクタを使用して、このオブジェクトを作成します。`BLOB` オブジェクトは、PDF/A ドキュメントに変換される PDF ドキュメントを格納するために使用されます。
   * コンストラクターを呼び出し、暗号化する PDF ドキュメントのファイルの場所とファイルを開くモードを表す文字列値を渡して、`System.IO.FileStream` オブジェクトを作成します。
   * `System.IO.FileStream` オブジェクトの内容を格納するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することで、バイト配列のサイズを決定できます。
   * バイト配列にストリームデータを入力するには、`System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出し、バイト配列、開始位置、読み取るストリーム長を渡します。
   * `BLOB` オブジェクトに入力するには、オブジェクトの `binaryData` プロパティに、バイト配列の内容を入力します。

1. 実行時オプションを設定

   * `PDFAValidationOptionSpec` オブジェクトを作成するには、このオブジェクトのコンストラクタを使用します。
   * コンプライアンスレベルを設定するには、 `PDFAValidationOptionSpec` オブジェクトの、`PDFAConversionOptionSpec_Compliance.PDFA_1B` の値を持つ `compliance` データメンバーを渡します。
   * 情報トラッキングレベルを設定するには、 `PDFAValidationOptionSpec` オブジェクトの、`PDFAValidationOptionSpec_ResultLevel.DETAILED` の値を持つ `resultLevel` データメンバーを渡します。

1. PDF ドキュメントに関する情報を取得

   `DocConverterServiceService` オブジェクトの `isPDFA` メソッドを呼び出し、次の値を渡して、PDF/A 準拠を判断します。

   * PDF ドキュメントを含む `BLOB` オブジェクト。
   * 実行時オプションを含む `PDFAValidationOptionSpec` オブジェクト。

   この `isPDFA` メソッドは、この操作の結果を格納する `PDFAValidationResult` オブジェクトを返します。

**関連トピック**

[PDF/A ドキュメントの操作](pdf-a-documents.md#working-with-pdf-a-documents)

[Base64 エンコーディングを使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64 エンコーディングを使用する .NET クライアントアセンブリの作成](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
