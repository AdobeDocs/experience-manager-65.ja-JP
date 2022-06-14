---
title: ファイル形式と PDF の変換
seo-title: Converting Between File Formats and PDF
description: Generate PDF サービスを使用して、ネイティブファイル形式を PDF に変換します。また、PDF を他のファイル形式に変換し、PDF ドキュメントのサイズを最適化します。
seo-description: Use the Generate PDF service to convert native file formats to PDF. Generate PDF service also converts PDF to other file formats and optimizes the size of PDF documents.
uuid: f72ad603-c996-4d48-9bfc-bed7bf776af6
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 180cac3f-6378-42bc-9a47-60f9f08a7103
role: Developer
exl-id: 10535740-e3c2-4347-a88f-86706ad699b4
source-git-commit: 0c7dba43dad8608b4a5de271e1e44942c950fb16
workflow-type: tm+mt
source-wordcount: '7850'
ht-degree: 100%

---

# ファイル形式と PDF の変換 {#converting-between-file-formatsand-pdf}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

**Generate PDF サービスについて**

Generate PDF サービスは、ネイティブファイル形式を PDF に変換します。また、PDF を他のファイル形式に変換し、PDF ドキュメントのサイズを最適化します。

Generate PDF サービスは、以下のファイル形式を PDF に変換する際にネイティブアプリケーションを使用します。特に説明がない限り、これらのアプリケーションはドイツ語版、フランス語版、英語版および日本語版のみサポートされています。*Windows のみ*&#x200B;は、Windows Server® 2003 および Windows Server 2008 のみをサポートしています。

* Microsoft Office 2003 および 2007：DOC、DOCX、RTF、TXT、XLS、XLSX、PPT、PPTX、VSD、MPP、XPS および PUB を変換（Windows のみ）

>[!NOTE]
>
>Acrobat® 9.2 以降は、Microsoft XPS 形式を PDF に変換する場合に必要です。

* DWF、DWG、DXW を変換する Autodesk AutoCAD 2005、2006、2007、2008、2009（英語のみ）
* WPD、QPW、SHW を変換する Corel WordPerfect 12 および X4（英語のみ）
* ODT、ODS、ODP、ODF、SXW、SXI、SXC、SXD、DOC、DOCX、RTF、TXT、XLS、XLSX、PPT、PPTX、VSD、MPP、MPPX および PUB を変換する OpenOffice 2.0、2.4、3.0.1、および 3.1

>[!NOTE]
>
>Generate PDF サービスは、64 ビットバージョンの OpenOffice をサポートしていません。

* PSD を変換する Adobe Photoshop® CS2（Windows のみ）

>[!NOTE]
>
>Windows Server 2003 または Windows Server 2008 がサポートされていないので、Photoshop CS3 および CS4 はサポートされていません。

* FM を変換する Adobe FrameMaker® 7.2 および 8（Windows のみ）
* PMD、PM6、P65、PM を変換する Adobe PageMaker® 7.0（Windows のみ）
* サードパーティのアプリケーションによってサポートされているネイティブ形式（アプリケーションに固有のセットアップファイルの開発が必要）（Windows のみ）

Generate PDF サービスでは、次の標準ベースのファイル形式を PDF に変換します。

* ビデオファイル形式：SWF、FLV（Windows のみ）
* 画像ファイル形式：JPEG、JPG、JP2、J2Kí、JPC、J2C、GIF、BMP、TIFF、TIF、PNG、JPF
* HTML（Windows、Sun™ Solaris™ および Linux®）

Generate PDF サービスでは、PDF を次のファイル形式に変換します（Windows のみ）：

* EPS（Encapsulated PostScript）
* HTML 3.2
* CSS 1.0 を使用した HTML 4.01
* DOC（Microsoft Word format）
* RTF
* テキスト（アクセス可能およびプレーンの両方）
* XML
* DeviceRGB カラースペースのみを使用する PDF/A-1a
* DeviceRGB カラースペースのみを使用する PDF/A-1b

Generate PDF サービスを使用するには、以下の管理タスクを実行する必要があります。

* 必要なネイティブアプリケーションを、AEM Forms をホストするコンピューター上にインストールする
* AEM Forms をホストするコンピューターに Adobe Acrobat Professional または Acrobat Pro Extended 9.2 をインストールします
* インストール後のセットアップタスクを実行します

これらのタスクに関する説明は『自動オプションの JBoss を使用した AEM Forms のインストールとデプロイ』に記載されています。

Generate PDF サービスを使用して、次のタスクを実行できます。

* ネイティブファイル形式から PDF への変換。
* HTML ドキュメントから PDF ドキュメントへの変換。
* PDF ドキュメントからファイル形式への変換。

>[!NOTE]
>
>Generate PDF サービスについて詳しくは、[AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

## Word ドキュメントの PDF ドキュメントへの変換 {#converting-word-documents-to-pdf-documents}

このセクションでは Generate PDF API を使用して、Microsoft Word ドキュメントをプログラムで PDF ドキュメントに変換する方法について説明します。

>[!NOTE]
>
>その他のファイル形式について詳しくは、[追加のネイティブファイル形式のサポートの追加](converting-file-formats-pdf.md#adding-support-for-additional-native-file-formats)を参照してください。

>[!NOTE]
>
>AEM Forms サービスについて詳しくは、[AEM Forms サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary-of-steps}

Microsoft Word ドキュメントを PDF ドキュメントに変換するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. PDF 生成クライアントを作成します。
1. PDF ドキュメントに変換するファイルを取得します。
1. ファイルを PDF ドキュメントに変換します。
1. 結果を取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**PDF 生成クライアントの作成**

プログラムによって「PDF を生成」操作を実行する前に、PDF 生成サービスクライアントを作成します。 Java API を使用している場合は、`GeneratePdfServiceClient` オブジェクトを作成します。Web サービス API を使用している場合は、`GeneratePDFServiceService` オブジェクトを作成します。

**PDF ドキュメントに変換するファイルを取得する**

PDF ドキュメントに変換する Microsoft Word ドキュメントを取得します。

**ファイルを PDF ドキュメントに変換**

PDF 生成サービスクライアントを作成した後、`createPDF2` メソッドを呼び出します。このメソッドでは、変換するドキュメントに関する情報（ファイル拡張子を含む）が必要です。

**結果の取得**

ファイルを PDF ドキュメントに変換した後、結果を取得できます。例えば、Word ファイルを PDF ドキュメントに変換した後に、その PDF ドキュメントを取得して保存できます。

**関連トピック**

[Java API を使用して Word ドキュメントを PDF ドキュメントに変換](converting-file-formats-pdf.md#convert-word-documents-to-pdf-documents-using-the-java-api)

[Web サービス API を使用して Word ドキュメントを PDF ドキュメントに変換](converting-file-formats-pdf.md#convert-word-documents-to-pdf-documents-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Generate PDF サービス API クイックスタート](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### Java API を使用して Word ドキュメントを PDF ドキュメントに変換 {#convert-word-documents-to-pdf-documents-using-the-java-api}

Generate PDF API（Java）を使用して、Microsoft Word ドキュメントを PDF ドキュメントに変換します。

1. プロジェクトファイルを含めます。

   adobe-generatepdf-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. PDF 生成クライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `ServiceClientFactory` オブジェクトを渡すことによって、`GeneratePdfServiceClient` オブジェクトを作成します。

1. PDF ドキュメントに変換するファイルを取得します。

   * コンストラクターを使用して、変換する Word ファイルを表す `java.io.FileInputStream` オブジェクトを作成します。ファイルの場所を指定する文字列値を渡します。
   * コンストラクターを使用して `java.io.FileInputStream` オブジェクトを渡すことによって、`com.adobe.idp.Document` オブジェクトを作成します。

1. ファイルを PDF ドキュメントに変換します。

   `GeneratePdfServiceClient` オブジェクトの `createPDF2` メソッドを呼び出して次の値を渡すことによって、ファイルを PDF ドキュメントに変換します。

   * 変換するファイルを表す `com.adobe.idp.Document` オブジェクト。
   * ファイル拡張子を含む `java.lang.String` オブジェクト。
   * 変換で使用されるファイルタイプ設定を含む `java.lang.String` オブジェクト。ファイルタイプ設定は、.doc や .xls など、様々なファイルタイプの変換設定を提供します。
   * 使用する PDF 設定の名前を含む `java.lang.String` オブジェクト。例えば、`Standard` を指定できます。
   * 使用するセキュリティ設定の名前を含む `java.lang.String` オブジェクト。
   * PDF ドキュメントの生成中に適用される設定を含むオプションの `com.adobe.idp.Document` オブジェクト。
   * PDF ドキュメントに適用されるメタデータ情報を含むオプションの `com.adobe.idp.Document` オブジェクト。

   `createPDF2` メソッドは、新しい PDF ドキュメントとログ情報を含む `CreatePDFResult` オブジェクトを返します。通常、ログファイルには、変換リクエストによって生成されるエラーまたは警告メッセージが含まれます。

1. 結果を取得します。

   PDF ドキュメントを取得するには、次のアクションを実行します。

   * `CreatePDFResult` オブジェクトの `getCreatedDocument` メソッドを呼び出します。これは `com.adobe.idp.Document` オブジェクトを返します。
   * `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを呼び出して、前の手順で作成したオブジェクトから PDF ドキュメントを抽出します。

   `createPDF2` メソッドを使用してログドキュメントを取得した場合（HTML 変換には適用されません）、次のアクションを実行します。

   * `CreatePDFResult` オブジェクトの `getLogDocument` メソッドを呼び出します。 これは `com.adobe.idp.Document` オブジェクトを返します。
   * `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを呼び出してログドキュメントを抽出します。


**関連トピック**

[手順の概要](converting-file-formats-pdf.md#summary-of-steps)

[クイックスタート（SOAP モード）：Java API を使用して Microsoft Word ドキュメントを PDF ドキュメントに変換](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-a-microsoft-word-document-to-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用して Word ドキュメントを PDF ドキュメントに変換 {#convert-word-documents-to-pdf-documents-using-the-web-service-api}

Generate PDF API（web サービス）を使用して、Microsoft Word ドキュメントを PDF ドキュメントに変換します。

1. プロジェクトファイルを含めます。

   MTOM を使用する Microsoft .NET プロジェクトを作成します。WSDL 定義 `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1` を使用するようにします。

   >[!NOTE]
   >
   >`localhost` を AEM Forms をホスティングするサーバーの IP アドレスに置換します。

1. PDF 生成クライアントを作成します。

   * デフォルトのコンストラクターを使用して `GeneratePDFServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して `GeneratePDFServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`）。`lc_version` 属性を使用する必要はありません。ただし、`?blob=mtom` を指定します。
   * `GeneratePDFServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` フィールドを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `GeneratePDFServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `GeneratePDFServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
      * フィールド `BasicHttpBindingSecurity.Security.Mode` に定数値 `BasicHttpSecurityMode.TransportCredentialOnly` を割り当てます。

1. PDF ドキュメントに変換するファイルを取得します。

   * コンストラクターを使用して `BLOB` オブジェクトを作成します。`BLOB` オブジェクトは、PDF ドキュメントに変換するファイルを格納するために使用されます。
   * コンストラクターを使用して `System.IO.FileStream` オブジェクトを作成します。変換するファイルの場所を表す文字列値とファイルを開くモードを渡します。
   * `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することで、バイト配列のサイズを決定できます。
   *  `System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出して読み込み対象のバイト配列、開始位置、ストリーム長を渡すことによって、バイト配列にストリームデータを入力します。
   * `MTOM` プロパティにバイト配列の内容を割り当て、`BLOB` オブジェクトにデータを入力します。

1. ファイルを PDF ドキュメントに変換します。

   `GeneratePDFServiceService` オブジェクトの `CreatePDF2` メソッドを呼び出して次の値を渡し、ファイルを PDF ドキュメントに変換します。

   * 変換するファイルを表す `BLOB` オブジェクト。
   * ファイル拡張子を含む文字列。
   * 変換で使用されるファイルタイプ設定を含む `java.lang.String` オブジェクト。ファイルタイプ設定は、.doc や .xls など、様々なファイルタイプの変換設定を提供します。
   * 使用する PDF 設定を含む文字列オブジェクト。`Standard` を指定できます。
   * 使用するセキュリティ設定を含む文字列オブジェクト。 `No Security` を指定できます。
   * PDF ドキュメントの生成中に適用される設定を含むオプションの `BLOB` オブジェクト。
   * PDF ドキュメントに適用されるメタデータ情報を含むオプションの `BLOB` オブジェクト。
   * `CreatePDF2` メソッドによって入力されるタイプ `BLOB` の出力パラメーター。`CreatePDF2` メソッドは、変換されたドキュメントをこのオブジェクトに入力します。（このパラメーター値は、web サービスの呼び出しにのみ必要です）。
   * `CreatePDF2` メソッドによって入力される `BLOB` 型の出力パラメーター。`CreatePDF2` メソッドは、このオブジェクトにログドキュメントを入力します。 （このパラメーター値は、web サービスの呼び出しにのみ必要です）。

1. 結果を取得します。

   * 変換後の PDF ドキュメントを取得するには、`BLOB` オブジェクトの `MTOM` フィールドをバイト配列に変換します。 バイト配列は変換後の PDF ドキュメントを表します。`createPDF2` メソッドの出力パラメーターとして使用される `BLOB` オブジェクトを使用していることを確認してください。
   * コンストラクターを呼び出して変換された PDF ドキュメントのファイルの場所を表す文字列値を渡すことにより、`System.IO.FileStream` オブジェクトを作成します。
   * コンストラクターを使用して `System.IO.FileStream` オブジェクトを渡すことによって、`System.IO.BinaryWriter` オブジェクトを作成します。
   * `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを呼び出して、バイト配列を渡すことによって、バイト配列の内容を PDF ファイルに書き込みます。

**関連トピック：**

[手順の概要](converting-file-formats-pdf.md#summary-of-steps)

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## HTML ドキュメントを PDF ドキュメントに変換 {#converting-html-documents-to-pdf-documents}

このセクションでは、PDF 生成 API を使用して、プログラムで HTML ドキュメントを PDF ドキュメントに変換する方法について説明します。

>[!NOTE]
>
>PDF 生成サービスについて詳しくは、[AEM Forms サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary_of_steps-1}

HTML ドキュメントを PDF ドキュメントに変換するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. PDF 生成クライアントを作成します。
1. HTML コンテンツを取得して PDF ドキュメントに変換します。
1. HTML のコンテンツを PDF ドキュメントに変換します。
1. 結果を取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**PDF 生成クライアントの作成**

プログラムによって「PDF を生成」操作を実行する前に、PDF 生成サービスクライアントを作成する必要があります。 Java API を使用している場合は、`GeneratePdfServiceClient` オブジェクトを作成します。Web サービス API を使用している場合は、`GeneratePDFServiceService` を作成します。

**HTML コンテンツを取得して PDF ドキュメントに変換する**

PDF ドキュメントに変換する HTML コンテンツを参照します。HTMLコンテンツ（HTML ファイルや、URL を使用してアクセス可能な HTML コンテンツなど）を参照できます。

**HTML コンテンツを PDF ドキュメントに変換**

サービスクライアントを作成した後、適切な PDF 作成操作を呼び出すことができます。 この操作では、ターゲットドキュメントへのパスを含む、変換するドキュメントに関する情報が必要です。

**結果の取得**

HTML コンテンツを PDF ドキュメントに変換した後、結果を取得して PDF ドキュメントを保存できます。

**関連トピック**

[Java API を使用して HTML コンテンツを PDF ドキュメントに変換する](converting-file-formats-pdf.md#convert-html-content-to-a-pdf-document-using-the-java-api)

[Web サービス API を使用して HTML コンテンツを PDF ドキュメントに変換する](converting-file-formats-pdf.md#convert-html-content-to-a-pdf-document-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Generate PDF サービス API クイックスタート](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### Java API を使用して HTML コンテンツを PDF ドキュメントに変換する {#convert-html-content-to-a-pdf-document-using-the-java-api}

Generate PDF API（Java）を使用して HTML ドキュメントを PDF ドキュメントに変換します。

1. プロジェクトファイルを含めます。

   adobe-generatepdf-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. PDF 生成クライアントを作成します。

   コンストラクターを使用し、接続プロパティを含む `ServiceClientFactory` オブジェクトを渡すことにより、`GeneratePdfServiceClient` オブジェクトを作成します。

1. HTML コンテンツを取得して PDF ドキュメントに変換します。

   文字列変数を作成し、HTML の内容を指す URL を割り当てて、HTML コンテンツを取得します。

1. HTML のコンテンツを PDF ドキュメントに変換します。

   `GeneratePdfServiceClient` オブジェクトの `htmlToPDF2` メソッドを呼び出して、次の値を渡します。

   * 変換する HTML ファイルの URL を含む `java.lang.String` オブジェクト。
   * 変換で使用されるファイルタイプ設定を含む `java.lang.String` オブジェクト。 ファイルタイプの設定には、スパイダリングレベルを含めることができます。
   * 使用するセキュリティ設定の名前を含む `java.lang.String` オブジェクト。
   * PDF ドキュメントの生成中に適用される設定を含むオプションの `com.adobe.idp.Document` オブジェクト。この情報が指定されていない場合、設定は前の 3 つのパラメータに基づいて自動的に選択されます。
   * PDF ドキュメントに適用されるメタデータ情報を含むオプションの `com.adobe.idp.Document` オブジェクト。

1. 結果を取得します。

   `htmlToPDF2` メソッドは、生成された新しい PDF ドキュメントを含む `HtmlToPdfResult` オブジェクトを返します。新しく作成した PDF ドキュメントを取得するには、次のアクションを実行します。

   * `HtmlToPdfResult` オブジェクトの `getCreatedDocument` メソッドを呼び出します。これは `com.adobe.idp.Document` オブジェクトを返します。
   * `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを呼び出して、前の手順で作成したオブジェクトから PDF ドキュメントを抽出します。

**関連トピック**

[HTML ドキュメントを PDF ドキュメントに変換](converting-file-formats-pdf.md#converting-html-documents-to-pdf-documents)

[クイックスタート（SOAP モード）：Java API を使用して HTML コンテンツを PDF ドキュメントに変換](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[クイックスタート（SOAP モード）：Java API を使用して HTML コンテンツを PDF ドキュメントに変換](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用して HTML コンテンツを PDF ドキュメントに変換する {#convert-html-content-to-a-pdf-document-using-the-web-service-api}

Generate PDF API（web サービス）を使用して、HTML のコンテンツを PDF ドキュメントに変換します。

1. プロジェクトファイルを含めます。

   MTOM を使用する Microsoft .NET プロジェクトを作成します。WSDL 定義 `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1` を使用するようにします。

   >[!NOTE]
   >
   >`localhost` を AEM Forms をホスティングするサーバーの IP アドレスに置換します。

1. PDF 生成クライアントを作成します。

   * デフォルトのコンストラクターを使用して `GeneratePDFServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して `GeneratePDFServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`）。`lc_version` 属性を使用する必要はありません。ただし、`?blob=mtom` を指定します。
   * `GeneratePDFServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` フィールドを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `GeneratePDFServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `GeneratePDFServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
      * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` をフィールド `BasicHttpBindingSecurity.Security.Mode` に割り当てます。

1. HTML コンテンツを取得して PDF ドキュメントに変換します。

   文字列変数を作成し、HTML の内容を指す URL を割り当てて、HTML コンテンツを取得します。

1. HTML のコンテンツを PDF ドキュメントに変換します。

   `GeneratePDFServiceService` オブジェクトの `HtmlToPDF2` メソッドを呼び出し、次の値を渡して HTML の内容を PDF ドキュメントに変換します。

   * 変換する HTML の内容を含む文字列。
   * 変換処理で使用されるファイルタイプ設定を含む `java.lang.String` オブジェクト。
   * 使用するセキュリティ設定を含む文字列オブジェクト。
   * PDF ドキュメントの生成時に適用される設定を含むオプションの `BLOB` オブジェクト。
   * PDF ドキュメントに適用されるメタデータ情報を含むオプションの `BLOB` オブジェクト。
   * `CreatePDF2` メソッドによって入力されるタイプ `BLOB` の出力パラメーター。`CreatePDF2` メソッドは、変換されたドキュメントをこのオブジェクトに入力します。（このパラメーター値は、web サービスの呼び出しにのみ必要です）。

1. 結果を取得します。

   * 変換後の PDF ドキュメントを取得するには、`BLOB` オブジェクトの `MTOM` フィールドをバイト配列に変換します。 バイト配列は変換後の PDF ドキュメントを表します。`HtmlToPDF2` メソッドの出力パラメーターとして使用される `BLOB` オブジェクトを使用していることを確認してください。
   * コンストラクターを呼び出して変換された PDF ドキュメントのファイルの場所を表す文字列値を渡すことにより、`System.IO.FileStream` オブジェクトを作成します。
   * コンストラクターを使用して `System.IO.FileStream` オブジェクトを渡すことによって、`System.IO.BinaryWriter` オブジェクトを作成します。
   * `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを呼び出して、バイト配列を渡すことによって、バイト配列の内容を PDF ファイルに書き込みます。

**関連トピック**

[HTML ドキュメントを PDF ドキュメントに変換](converting-file-formats-pdf.md#converting-html-documents-to-pdf-documents)

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## PDF ドキュメントを非画像形式に変換中 {#converting-pdf-documents-to-non-image-formats}

この節では、Generate PDF Java API と web サービス API を使用して、PDF ドキュメントをプログラムで RTF ファイルに変換する方法について説明します。RTF ファイルは、非画像形式の一例です。その他の非画像形式には、HTML、テキスト、DOC、EPS などがあります。PDF ドキュメントを RTF に変換する場合は、送信ボタンなどのフォーム要素が PDF ドキュメントに含まれていないことを確認します。フォーム要素は変換されません。

>[!NOTE]
>
>Generate PDF サービスについて詳しくは、[AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary_of_steps-2}

PDF ドキュメントをサポートされている任意のタイプに変換するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. PDF 生成クライアントを作成します。
1. 変換する PDF ドキュメントを取得します。
1. PDF ドキュメントを変換します。
1. 変換したファイルを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**PDF 生成クライアントの作成**

プログラムによって「PDF を生成」操作を実行する前に、PDF 生成サービスクライアントを作成する必要があります。 Java API を使用している場合は、`GeneratePdfServiceClient` オブジェクトを作成します。Web サービス API を使用している場合は、`GeneratePDFServiceService` オブジェクトを作成します。

**変換する PDF ドキュメントを取得**

非画像形式に変換する PDF ドキュメントを取得します。

**PDF ドキュメントを変換**

サービスクライアントを作成した後で、PDF のエクスポート操作を呼び出すことができます。この操作では、ターゲットドキュメントへのパスを含む、変換するドキュメントに関する情報が必要です。

**変換したファイルを保存**

変換されたファイルを保存します。例えば、PDF ドキュメントを RTF ファイルに変換する場合は、変換されたドキュメントを RTF ファイルに保存します。

**関連トピック**

[Java API を使用して PDF ドキュメントを RTF ファイルに変換](converting-file-formats-pdf.md#convert-a-pdf-document-to-a-rtf-file-using-the-java-api)

[Web サービス API を使用して PDF ドキュメントを RTF ファイルに変換](converting-file-formats-pdf.md#convert-a-pdf-document-to-a-rtf-file-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Generate PDF サービス API クイックスタート](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### Java API を使用して PDF ドキュメントを RTF ファイルに変換 {#convert-a-pdf-document-to-a-rtf-file-using-the-java-api}

Generate PDF API（Java）を使用して、PDF ドキュメントを RTF ファイルに変換します。

1. プロジェクトファイルを含めます。

   adobe-generatepdf-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. PDF 生成クライアントを作成します。

   コンストラクターを使用し、接続プロパティを含む `ServiceClientFactory` オブジェクトを渡すことにより、`GeneratePdfServiceClient` オブジェクトを作成します。

1. 変換する PDF ドキュメントを取得します。

   * コンストラクターを使用して、変換する PDF ドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。PDF ドキュメントの場所を指定する文字列値を渡します。
   * コンストラクターを使用し、`java.io.FileInputStream` オブジェクトを渡すことによって、`com.adobe.idp.Document` オブジェクトを作成します。

1. PDF ドキュメントを変換します。

   `GeneratePdfServiceClient` オブジェクトの `exportPDF2` メソッドを呼び出して、次の値を渡します。

   * 変換する PDF ファイルを表す `com.adobe.idp.Document` オブジェクト。
   * 変換するファイルの名前を含む `java.lang.String` オブジェクト。
   * Adobe PDF 設定の名前を含む `java.lang.String` オブジェクト。
   * 変換対象のターゲットファイルタイプを指定する `ConvertPDFFormatType` オブジェクト。
   * PDF ドキュメントの生成中に適用される設定を含むオプションの `com.adobe.idp.Document` オブジェクト。

   `exportPDF2` メソッドは、変換されたファイルを含む `ExportPDFResult` オブジェクトを返します。

1. PDF ドキュメントを変換します。

   新しく作成されたファイルを取得するには、次のアクションを実行します。

   * `ExportPDFResult` オブジェクトの `getConvertedDocument` メソッドを呼び出します。これは `com.adobe.idp.Document` オブジェクトを返します。
   * `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを呼び出して、新規ドキュメントを抽出します。

**関連トピック**

[手順の概要](converting-file-formats-pdf.md#summary-of-steps)

[クイックスタート（SOAP モード）：Java API を使用して HTML コンテンツを PDF ドキュメントに変換](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用して PDF ドキュメントを RTF ファイルに変換 {#convert-a-pdf-document-to-a-rtf-file-using-the-web-service-api}

Generate PDF API（web サービス）を使用して、PDF ドキュメントを RTF ファイルに変換します。

1. プロジェクトファイルを含めます。

   MTOM を使用する Microsoft .NET プロジェクトを作成します。WSDL 定義 `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1` を使用するようにします。

   >[!NOTE]
   >
   >`localhost` を AEM Forms をホスティングするサーバーの IP アドレスに置換します。

1. Generate PDF クライアントを作成します。

   * デフォルトのコンストラクターを使用して `GeneratePDFServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して `GeneratePDFServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`）。`lc_version` 属性を使用する必要はありません。ただし、`?blob=mtom` を指定します。
   * `GeneratePDFServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` フィールドを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `GeneratePDFServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `GeneratePDFServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
      * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` をフィールド `BasicHttpBindingSecurity.Security.Mode` に割り当てます。

1. 変換する PDF ドキュメントを取得します。

   * コンストラクターを使用して `BLOB` オブジェクトを作成します。`BLOB` オブジェクトは、変換された PDF ドキュメントの保存に使用されます。
   * `System.IO.FileStream` オブジェクトを作成するには、コンストラクターを呼び出し、PDF ドキュメントのファイルの場所とファイルを開くモードを表す文字列値を渡します。
   * `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することで、バイト配列のサイズを決定できます。
   *  `System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出して読み込み対象のバイト配列、開始位置、ストリーム長を渡すことによって、バイト配列にストリームデータを入力します。
   * `MTOM` プロパティにバイト配列の内容を割り当てて、`BLOB` オブジェクトにデータを入力します。

1. PDF ドキュメントを変換します。

   `GeneratePDFServiceServiceWse` オブジェクトの `ExportPDF2` メソッドを呼び出して、次の値を渡します。

   * 変換する PDF ファイルを表す `BLOB` オブジェクト。
   * 変換するファイルのパス名を含む文字列。
   * ファイルの場所を指定する `java.lang.String` オブジェクト。
   * 変換対象のファイルタイプを指定する文字列オブジェクト。`RTF` を指定します。
   * PDF ドキュメントの生成時に適用される設定を含むオプションの `BLOB` オブジェクト。
   * `ExportPDF2` メソッドによって入力されるタイプ `BLOB` の出力パラメーター。`ExportPDF2` メソッドは、変換されたドキュメントをこのオブジェクトに入力します。（このパラメーター値は、web サービスの呼び出しにのみ必要です）。

1. 変換したファイルを保存します。

   * 変換された RTF ドキュメントを取得するには、`BLOB` オブジェクトの `MTOM` フィールドをバイト配列に割り当てます。バイト配列は変換された RTF ドキュメントを表します。`ExportPDF2` メソッドの出力パラメーターとして使用される `BLOB` オブジェクトを使用していることを確認してください。
   * コンストラクターを呼び出して `System.IO.FileStream` オブジェクトを作成します。RTF ファイルの場所を表す文字列値を渡します。
   * コンストラクターを呼び出して、`System.IO.FileStream` オブジェクトを渡すことによって、`System.IO.BinaryWriter` オブジェクトを作成します。
   * バイト配列の内容を RTF ファイルに書き込むには、`System.IO.BinaryWriter` オブジェクトの `Write` メソッドを呼び出し、バイト配列を渡します。

**関連トピック**

[手順の概要](converting-file-formats-pdf.md#summary-of-steps)

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 追加のネイティブファイル形式のサポートの追加 {#adding-support-for-additional-native-file-formats}

この節では、追加のネイティブファイル形式のサポートを追加する方法について説明します。Generate PDF サービスと、このサービスがネイティブファイル形式を PDF に変換するために使用するネイティブアプリケーションとの間のやり取りの概要を提供します。

この節では、次の点についても説明します。

* この製品がネイティブファイル形式を PDF に変換する際に使用しているネイティブアプリケーションに対して、Generate PDF サービスが提供する応答を変更する方法
* Generate PDF サービス、Generate PDF サービスの Application Monitor（AppMon）コンポーネント、Microsoft Word などのネイティブアプリケーション間のインタラクション
* これらのインタラクションにおいて XML 文法が果たす役割

### コンポーネントのインタラクション {#component-interactions}

Generate PDF サービスがネイティブファイル形式を変換するには、そのファイル形式に関連付けられたアプリケーションを呼び出し、デフォルトのプリンターを使用してドキュメントを印刷するためにそのアプリケーションとやり取りします。デフォルトのプリンターを Adobe PDF プリンターとして設定する必要があります。

この図は、ネイティブアプリケーションのサポートに関連するコンポーネントとドライバーを示しています。また、インタラクションに影響を与える XML 文法についても説明します。

ネイティブファイル変換のためのコンポーネントのインタラクション

このドキュメントでは、*ネイティブアプリケーション*&#x200B;という用語を使用して、ネイティブファイル形式（Microsoft Word など）の生成に使用するアプリケーションを示します。

*AppMon* は、ユーザーがアプリケーションで表示されるダイアログボックス間を移動するのと同じ方法でネイティブアプリケーションとやり取りする、エンタープライズコンポーネントです。AppMon が Microsoft Word などのアプリケーションにファイルを開いて印刷するように指示する際に使用する XML 文法には、次のような連続したタスクが含まれます。

1. ファイル／開くを選択してファイルを開く
1. 開くダイアログボックスが表示されていることを確認する。表示されていない場合はエラーを処理する
1. 「ファイル名」フィールドにファイル名を入力し、「開く」ボタンをクリックする
1. ファイルが実際に開くことを確認する
1. ファイル／印刷を選択して、印刷ダイアログボックスを開く
1. 印刷ダイアログボックスが表示されることを確認する

AppMon は、標準の Win32 API を使用して、サードパーティのアプリケーションとやり取りし、キーストロークやマウスクリックなどの UI イベントを転送します。これは、これらのアプリケーションを制御して PDF ファイルを生成するのに役立ちます。

これらの Win32 API の制限により、AppMon は、TextPad などの一部のアプリケーションで見つかるフローティングメニューバーや、Win32 API を使用してコンテンツを取得できない特定の種類のダイアログなど、特定の種類のウィンドウにこれらの UI イベントをディスパッチできません。

フローティングメニューバーを視覚的に識別するのは簡単です。ただし、特別な種類のダイアログは、目視による検査だけでは特定できない場合があります。 ダイアログを調べて、AppMon が標準の Win32 API を使用してダイアログと対話できるかどうかを判断するには、Microsoft Spy ++（Microsoft Visual C ++ 開発環境の一部）または同等の WinID（[ https://www.dennisbabkin.com/php/download.php?what=WinID](https://www.dennisbabkin.com/php/download.php?what=WinID) から無料でダウンロードできます）などのサードパーティアプリケーションが必要になります。

WinID がテキスト、サブウィンドウ、ウィンドウクラス ID などのダイアログの内容を抽出できる場合は、AppMon も同じ処理を実行できます。

次のテーブルは、ネイティブファイル形式の印刷で使用される情報の種類を示しています。

<table>
 <thead>
  <tr>
   <th><p>情報タイプ</p></th>
   <th><p>説明</p></th>
   <th><p>ネイティブファイルに関連するエントリの変更／作成 </p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>管理設定 </p></td>
   <td><p>PDF 設定、セキュリティ設定、およびファイルタイプ設定が含まれます。 </p><p>ファイルタイプ設定は、ファイル名の拡張子を対応するネイティブアプリケーションに関連付けます。 ファイルタイプ設定では、ネイティブファイルの印刷に使用するネイティブアプリケーション設定も指定します。 </p></td>
   <td><p>既にサポートされているネイティブアプリケーションの設定を変更するには、システム管理者が管理コンソールで「ファイルタイプ設定」を設定します。 </p><p>新しいネイティブファイル形式のサポートを追加するには、ファイルを手動で編集する必要があります。 （<a href="converting-file-formats-pdf.md#adding-or-modifying-support-for-a-native-file-format">ネイティブファイル形式のサポートの追加または変更</a>を参照。） </p></td>
  </tr>
  <tr>
   <td><p>スクリプト </p></td>
   <td><p>PDF 生成サービスとネイティブアプリケーション間の相互作用を指定します。このようなやり取りは、通常、アプリケーションに対して、Adobe PDF ドライバーにファイルを印刷するよう指示します。 </p><p>スクリプトには、特定のダイアログボックスを開くようネイティブアプリケーションに指示し、それらのダイアログボックスのフィールドやボタンに対して特定の応答を提供する指示が含まれています。 </p></td>
   <td><p>PDF 生成サービスには、サポートされているすべてのネイティブアプリケーションのスクリプトファイルが含まれています。これらのファイルは、XML 編集アプリケーションを使用して変更できます。</p><p>新しいネイティブアプリケーションのサポートを追加するには、新しいスクリプトファイルを作成する必要があります。 （<a href="converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application">ネイティブアプリケーション用の追加のダイアログ XML ファイルの作成または変更</a>を参照。） </p></td>
  </tr>
  <tr>
   <td><p>汎用ダイアログボックスの説明 </p></td>
   <td><p>複数のアプリケーションに共通のダイアログボックスに対する応答方法を指定します。 このようなダイアログボックスは、オペレーティングシステム、ヘルパーアプリケーション（PDFMaker など）、ドライバーによって生成されます。 </p><p>この情報は、appmon.global.en_US.xml ファイルに含まれます。</p></td>
   <td><p>このファイルは変更しないでください。 </p></td>
  </tr>
  <tr>
   <td><p>アプリケーション固有のダイアログボックスの説明</p></td>
   <td><p>アプリケーション固有のダイアログボックスに対する応答方法を指定します。 </p><p>この情報は、appmon.<i>`[appname]`</i>.dialog.<i>'[locale]'</i>.xml ファイルに含まれます。（appmon.word.en_US.xml など）</p></td>
   <td><p>このファイルは変更しないでください。 </p><p>新しいネイティブアプリケーション用のダイアログボックスの手順を追加するには、<a href="converting-file-formats-pdf.md#creating_or_modifying_an_additional_dialog_xml_file_for_a_native_application">ネイティブアプリケーション用の追加のダイアログ XML ファイルの作成または変更</a>を参照してください。</p></td>
  </tr>
  <tr>
   <td><p>その他のアプリケーション固有のダイアログボックスの手順 </p></td>
   <td><p>アプリケーション固有のダイアログボックスの手順に対する上書きと追加を指定します。 この節では、このような情報の例を示します。 </p><p>この情報は、appmon.<i>`[appname]`</i>.addition.<i>`[locale]`</i>.xml ファイルに含まれます。（例：appmon.addition.en_US.xml）</p></td>
   <td><p>このタイプのファイルは、XML 編集アプリケーションを使用して作成および変更できます。 （<a href="converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application">ネイティブアプリケーション用の追加のダイアログ XML ファイルの作成または変更</a>を参照。） </p><p><strong>重要</strong>：サーバーがサポートするネイティブアプリケーションごとに、追加のアプリケーション固有のダイアログボックスの手順を作成する必要があります。 </p></td>
  </tr>
 </tbody>
</table>

### スクリプトとダイアログの XML ファイルについて {#about-the-script-and-dialog-xml-files}

スクリプト XML ファイルは、ユーザーがアプリケーションダイアログボックスをナビゲートするのと同じ方法で、PDF 生成サービスにアプリケーションダイアログボックスをナビゲートするように指示します。スクリプト XML ファイルは、ボタンの押下、チェックボックスの選択または選択解除、メニュー項目の選択などのアクションを実行することにより、ダイアログボックスに応答するように PDF 生成サービスに指示します。

これに対して、ダイアログ XML ファイルは、スクリプト XML ファイルで使用されるのと同じタイプのアクションでダイアログボックスに応答するだけです。

#### ダイアログボックスとウィンドウ要素の用語 {#dialog-box-and-window-element-terminology}

このセクションと次のセクションでは、説明されている視点に応じて、ダイアログボックスとそれに含まれるコンポーネントに対して異なる用語を使用します。ダイアログボックスのコンポーネントは、ボタン、フィールド、コンボボックスなどの項目です。

このセクションと次のセクションで、ユーザーの観点からダイアログボックスとそのコンポーネントについて説明する場合、*ダイアログボックス*、*ボタン*、*フィールド*、*コンボボックス*&#x200B;などの用語を使用します。

このセクションと次のセクションで、ダイアログボックスとそのコンポーネントを内部表現の観点から説明する場合、*ウィンドウ要素*&#x200B;という用語を使用します。ウィンドウ要素の内部表現は階層で、各ウィンドウ要素のインスタンスはラベルで識別されます。ウィンドウ要素インスタンスは、その物理的な特性と動作も記述します。

ユーザーの視点から見ると、ダイアログボックスとそのコンポーネントは異なる動作を示し、一部のダイアログボックス要素は、アクティブ化されるまで非表示になります。 内部表現の観点からは、そのような行動の問題は存在しません。 例えば、ダイアログボックスの内部表現は、そのダイアログボックスに含まれるコンポーネントの内部表現に似ていますが、コンポーネントがダイアログボックス内にネストされている点が異なります。

このセクションでは、AppMon に手順を提供する XML 要素について説明します。 これらの要素には、`dialog` 要素、`window` 要素などの名前があります。このドキュメントでは、XML 要素を区別するために等幅フォントを使用します。 `dialog` 要素は、XML スクリプトファイルが意図的または意図せずに表示される原因となる可能性のあるダイアログボックスを識別します。 `window` 要素は、ウィンドウ要素（ダイアログボックスまたはダイアログボックスのコンポーネント）を識別します。

#### 階層 {#hierarchy}

次の図は、スクリプトとダイアログ XML の階層を示しています。 スクリプト XML ファイルは、script.xsd スキーマに準拠しており、この script.xsd スキーマには、window.xsd スキーマが（XML の意味で）含まれます。 同様に、ダイアログ XML ファイルは dialogs.xsd スキーマに準拠し、dialogs.xsd スキーマにも window.xsd スキーマが含まれます。

![as_as_xml_hierarchy](assets/as_as_xml_hierarchy.png)

スクリプトとダイアログ XML の階層

#### スクリプト XML ファイル {#script-xml-files}

*スクリプト XML ファイル*&#x200B;は、特定のウィンドウ要素に移動してそれらの要素への応答を提供するように指示する一連のステップをネイティブアプリケーションに指定します。ほとんどの応答は、ユーザーが対応するダイアログボックスのフィールド、コンボボックス、ボタンへの入力に対応するテキストまたはキーストロークです。

PDF 生成サービスでスクリプト XML ファイルをサポートする目的は、ネイティブアプリケーションにネイティブファイルを印刷するよう指示することです。 ただし、スクリプト XML ファイルを使用して、ユーザーがネイティブアプリケーションのダイアログボックスを操作するときに実行できるすべてのタスクを実行できます。

スクリプト XML ファイル内の手順は、分岐の機会がなく、順番に実行されます。 サポートされている唯一の条件付きテストは、タイムアウト／再試行です。これにより、特定の期間内および特定の回数の再試行後に手順が正常に完了しなかった場合にスクリプトが終了します。

順次的な手順に加えて、手順内の命令も順に実行されます。 手順と指示が、ユーザーが同じ手順を実行する順序を反映していることを確認する必要があります。

スクリプト XML ファイルの各手順は、手順の指示を正常に実行した場合に表示されるウィンドウ要素と予想されるウィンドウ要素を識別します。スクリプトでの手順の実行中に予期しないダイアログボックスが表示された場合、PDF 生成サービスは、次のセクションで説明するようにダイアログ XML ファイルを検索します。

#### ダイアログ XML ファイル {#dialog-xml-files}

ネイティブアプリケーションを実行すると、異なるダイアログボックスが表示されます。これは、ネイティブアプリケーションが表示モードか非表示モードかに関係なく表示されます。 ダイアログボックスは、オペレーティングシステムによって生成することも、アプリケーション自体によって生成することもできます。 ネイティブアプリケーションが PDF 生成サービスの制御下で実行されている場合、システムおよびネイティブアプリケーションのダイアログボックスが非表示ウィンドウに表示されます。

*ダイアログ XML ファイル*&#x200B;は、 PDF 生成サービスのシステムまたはネイティブアプリケーションのダイアログボックスに対する応答を指定します。 ダイアログ XML ファイルを使用すると、PDF 生成サービスは、変換プロセスを容易にする方法で、プロンプトのないダイアログボックスに応答できます。

システムまたはネイティブアプリケーションが、現在実行中のスクリプト XML ファイルで処理されないダイアログボックスを表示すると、PDF 生成サービスはダイアログ XML ファイルをこの順序で検索し、一致するものが見つかると停止します。

* appmon。`[appname]`。追加。`[locale]`.xml
* appmon。`[appname]``[locale]`.xml （このファイルは変更しないでください）。
* appmon.global。`[locale]`.xml （このファイルは変更しないでください）。

Generate PDF サービスは、ダイアログボックスに一致するものを見つけると、ダイアログボックスに指定されたキーストロークまたはその他のアクションを送信して、それを閉じます。ダイアログボックスの指示で中止メッセージが指定されている場合、Generate PDF サービスは現在実行中のジョブを終了し、エラーメッセージを生成します。このような中止メッセージは、スクリプト XML 文法の `abortMessage` 要素で指定されます。

Generate PDF サービスで、以前にリストされたファイルのいずれにも記述されていないダイアログボックスが検出された場合、Generate PDF サービスは、ダイアログボックスのキャプションをログファイルエントリに組み込みます。現在実行中のジョブは最終的にタイムアウトします。その後、ログファイル内の情報を使用して、ネイティブアプリケーション用の追加のダイアログ XML ファイルで新しい手順を作成できます。

### ネイティブファイル形式のサポートの追加または変更 {#adding-or-modifying-support-for-a-native-file-format}

この節では、他のネイティブファイル形式をサポートするために必要な作業、または既にサポートされているネイティブファイル形式のサポートを変更するために必要な作業について説明します。

サポートを追加または変更する前に、次の作業を完了する必要があります。

#### ウィンドウ要素を識別するツールの選択 {#choosing-a-tool-for-identifying-window-elements}

ダイアログおよびスクリプトの XML ファイルでは、ダイアログまたはスクリプト要素が応答するウィンドウ要素（ダイアログボックス、フィールド、またはその他のダイアログコンポーネント）を識別する必要があります。 例えば、スクリプトがネイティブアプリケーションのメニューを呼び出した後、スクリプトはそのメニューでキー操作またはアクションを適用するウィンドウ要素を識別する必要があります。

ダイアログボックスは、タイトルバーに表示されるキャプションによって簡単に識別できます。 ただし、下位レベルのウィンドウ要素を識別するには、Microsoft Spy++ などのツールを使用する必要があります。 下位レベルのウィンドウ要素は各種の属性を使用して識別できますが、これらの属性は明確ではありません。 さらに、ウィンドウ要素の識別方法はネイティブアプリケーションごとに異なる場合があります。そのため、ウィンドウ要素を識別する方法は複数あります。 ウィンドウ要素の識別を考慮する場合に推奨される順序を次に示します。

1. キャプション自体（一意の場合）
1. コントロール ID（特定のダイアログボックスで一意である場合とそうでない場合がある）
1. クラス名（一意である場合とそうでない場合がある）

ウィンドウを識別するために、これら 3 つの属性のうち 1 つ、または複数の属性の組み合わせを使用できます。

属性でキャプションを識別できない場合は、代わりに親に対するインデックスを使用してウィンドウ要素を識別できます。 *インデックス*&#x200B;は、兄弟ウィンドウ要素に対するウィンドウ要素の位置を指定します。多くの場合、コンボボックスはインデックスでしか判別できません。

次のような問題があります。

* Microsoft Spy++ では、キャプションのホットキーを識別するために、アンパサンド（&amp;）を使用してキャプションを表示します。例えば、Spy++ では、ある印刷ダイアログボックスのキャプションが `Pri&nt` と表示されていますが、これはホットキーが *n* であることを示しています。スクリプトおよびダイアログの XML ファイルのキャプションタイトルでは、アンパサンドを省略する必要があります。
* 一部のキャプションには改行が含まれています。Generate PDF サービスでは改行を識別できません。キャプションに改行が含まれている場合は、他のメニュー項目と区別するのに十分なキャプションを含め、省略された部分には正規表現を使用します。例えば（`^Long caption title$`）のようになります。 （[キャプション属性での正規表現の使用](converting-file-formats-pdf.md#using-regular-expressions-in-caption-attributes)を参照。）
* 予約された XML 文字には、文字エンティティ（エスケープシーケンスとも呼ばれます）を使用します。例えば、アンパサンドには `&`、「より小さい」と「より大きい」を表す記号にはそれぞれ `<` と `>`、アポストロフィには `&apos;`、引用符には `&quot;` を使用します。

ダイアログまたはスクリプト XML ファイルで作業する場合は、Microsoft Spy++ アプリケーションをインストールする必要があります。

#### ダイアログおよびスクリプトファイルの解凍 {#unpackaging-the-dialog-and-script-files}

ダイアログファイルとスクリプトファイルは、appmondata.jar ファイルにあります。これらのファイルを変更したり、新しいスクリプトファイルやダイアログファイルを追加したりする前に、この JAR ファイルを解凍する必要があります。 例えば、EditPlus アプリケーションのサポートを追加するとします。appmon.editplus.script.en_US.xml と appmon.editplus.script.add.en_US.xml という名前の 2 つの XML ファイルを作成します。これらの XML スクリプトは、以下に指定するように、2 つの場所で adobe-appmondata.jar ファイルに追加する必要があります。

* adobe-livecycle-native-jboss-x86_win32.ear／adobe-Native2PDFSvc.war\WEB-INF\lib／adobe-native.jar／Native2PDFSvc-native.jar\bin／adobe-appmondata.jar\com\adobe\appmon. adobe-livecycle-native-jboss-x86_win32.ear ファイルは、`[AEM forms install directory]\configurationManager` のエクスポートフォルダーにあります。（AEM Forms が別の J2EE アプリケーションサーバーにデプロイされている場合は、adobe-livecycle-native-jboss-x86_win32.ear ファイルを、J2EE アプリケーションサーバーに対応する EAR ファイルに置き換えます。）
* adobe-generatepdf-dsc.jar／adobe-appmondata.jar\com\adobe\appmon（adobe-appmondata.jar ファイルは adobe-generatepdf-dsc.jar ファイル内にあります）。adobe-generatepdf-dsc.jar ファイルは、`[AEM forms install directory]\deploy` フォルダーにあります。

これらの XML ファイルを adobe-appmondata.jar ファイルに追加した後、GeneratePDF コンポーネントを再デプロイする必要があります。adobe-appmondata.jar ファイルにダイアログおよびスクリプト XML ファイルを追加するには、次のタスクを実行します。

1. WinZip や WinRAR などのツールを使用して、adobe-livecycle-native-jboss-x86_win32.earfile ／ adobe-Native2PDFSvc.war\WEB-INF\lib ／ adobe-native.jar ／ Native2PDFSvc-native.jar\bin ／ adobe-appmondata.jar ファイルを開きます。
1. appmondata.jar ファイルにダイアログおよびスクリプト XML ファイルを追加するか、このファイル内の既存の XML ファイルを変更します。（[ネイティブアプリケーション用のスクリプト XML ファイルの作成または変更](converting-file-formats-pdf.md#creating-or-modifying-a-script-xml-file-for-a-native-application)および [ネイティブアプリケーション用の追加のダイアログ XML ファイルの作成または変更](converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application)を参照してください）
1. WinZip や WinRAR などのツールを使用して、adobe-generatepdf-dsc.jar／adobe-appmondata.jar を開きます。
1. appmondata.jar ファイルにダイアログおよびスクリプト XML ファイルを追加するか、このファイル内の既存の XML ファイルを変更します。（[ネイティブアプリケーション用のスクリプト XML ファイルの作成または変更](converting-file-formats-pdf.md#creating-or-modifying-a-script-xml-file-for-a-native-application)および [ネイティブアプリケーション用の追加のダイアログ XML ファイルの作成または変更](converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application)を参照してください）XML ファイルを adobe-appmondata.jar ファイルに追加した後、新しい adobe-appmondata.jar ファイルを adobe-generatepdf-dsc.jar ファイルに配置します。
1. 追加でイティブファイル形式のサポートを加えた場合は、アプリケーションのパスを提供するシステム環境変数を作成します（[ネイティブアプリケーションを見つけるための環境変数の作成](converting-file-formats-pdf.md#creating-an-environment-variable-to-locate-the-native-application)を参照）。

**PDF 生成コンポーネントを再デプロイするには**

1. ワークベンチにログインします。
1. **ウィンドウ**／**表示**／**コンポーネント**&#x200B;を選択します。このアクションにより、コンポーネント表示が Workbench に追加されます。
1. GeneratePDF コンポーネントを右クリックし、**コンポーネントを停止**&#x200B;を選択します。
1. コンポーネントが停止したら、「コンポーネントをアンインストールする」を右クリックして 選択し、削除します。
1. **コンポーネント**&#x200B;アイコンを右クリックし、「**コンポーネントをインストールする**」を選択します。
1. 変更された adobe-generatepdf-dsc.jar ファイルを参照して選択し、「開く」をクリックします。 GeneratePDF コンポーネントの横に赤い四角形が表示されます。
1. GeneratePDF コンポーネントを展開し、「サービス記述子」を選択し、「GeneratePDF サービス」を右クリックして「サービスをアクティブ化」を選択します。
1. 表示される設定ダイアログボックスで、適切な設定値を入力します。 これらの値を空白のままにした場合、デフォルトの設定値が使用されます。
1. 「GeneratePDF」を右クリックし、「コンポーネントを開始」を選択します。
1. 「アクティブなサービス」を展開します。 サービス名の横に緑色の矢印が表示されます（実行中の場合）。 それ以外の場合、サービスは停止状態になります。
1. サービスが停止状態の場合は、サービス名を右クリックし、「サービスを開始」を選択します。

### ネイティブアプリケーション用のスクリプト XML ファイルの作成または変更 {#creating-or-modifying-a-script-xml-file-for-a-native-application}

新しいネイティブアプリケーションにファイルをダイレクトする場合は、そのアプリケーション用のスクリプト XML ファイルを作成する必要があります。PDF 生成サービスと既にサポートされているネイティブアプリケーションとのやり取りを変更する場合は、そのアプリケーションのスクリプトを変更する必要があります。

スクリプトには、ネイティブアプリケーションのウィンドウ要素間を移動し、それらの要素に対して特定の応答を提供する手順が含まれています。 この情報を含むファイルは `appmon.`[アプリ名]`` `.script.`[ロケール]`.xml`です。 例えば appmon.notepad.script.en_US.xml です。

#### スクリプトが実行する必要があるステップの識別 {#identifying-steps-the-script-must-execute}

ネイティブアプリケーションを使用して、ドキュメントを印刷するために移動する必要のあるウィンドウ要素と実行する必要がある各応答を決定します。 任意の応答によって生成されるダイアログボックスに注意してください。 手順は次の手順に似ています。

1. ファイル／開くを選択します。
1. パスを指定し、「開く」をクリックします。
1. メニューバーでファイル／印刷を選択します。
1. プリンターに必要なプロパティを指定します。
1. 「印刷」を選択し、「別名で保存」ダイアログボックスが表示されるのを待ちます。 PDF 生成サービスで「別名で保存」ダイアログボックスが必要なのは、PDF ファイルの出力先を指定するためです。

#### キャプション属性で指定されたダイアログの識別 {#identifying-the-dialogs-specified-in-caption-attributes}

Microsoft Spy++ を使用して、ネイティブアプリケーションのウィンドウ要素プロパティの ID を取得します。 スクリプトを記述するには、次の ID が必要です。

#### キャプション属性での正規表現の使用 {#using-regular-expressions-in-caption-attributes}

キャプションの仕様では、正規表現を使用できます。 PDF 生成サービスでは、正規表現をサポートする `java.util.regex.Matcher` クラスを使用します。このユーティリティは `java.util.regex.Pattern` で説明された正規表現をサポートします。

**メモ帳バナーでメモ帳の前に付けたファイル名を格納する正規表現**

```xml
 <!-- The regular expression ".*Notepad" means any number of non-terminating characters followed by Notepad. -->
 <step>
     <expectedWindow>
         <window caption=".*Notepad"/>
     </expectedWindow>
 </step>
```

**印刷と印刷設定を区別する正規表現**

```xml
 <!-- This regular expression differentiates the Print dialog box from the Print Setup dialog box. The "^" specifies the beginning of the line, and the "$" specifies the end of the line. -->
 <windowList>
     <window controlID="0x01" caption="^Print$" action="press"/>
 </windowList>
```

#### window 要素と windowList 要素の順序付け {#ordering-the-window-and-windowlist-elements}

`window` および `windowList` 要素は次の順序にする必要があります。

* 複数の `window` 要素が `windowList` または `dialog` 要素の子として表示される場合、それらの `window` 要素を降順で並べ替えます。`caption` 名の長さは順序での位置を示します。
* 複数の `windowList` 要素が `window` 要素に表示される場合は、それらの `windowList` 要素を降順で並べ替えます。最初の `indexes/` 要素の `caption` 属性の長さは順序内の位置を示します。

**ダイアログファイル内のウィンドウ要素の順序**

```xml
 <!-- The caption attribute in the following window element is 40 characters long. It is the longest caption in this example, so its parent window element appears before the others. -->
 <window caption="Unexpected Failure in DebugActiveProcess">
     <…>
 </window>

 <!-- Caption length is 33 characters. -->
 <window caption="Adobe Acrobat - License Agreement">
     <…>
 </window>

 <!-- Caption length is 33 characters. -->
 <window caption="Microsoft Visual.*Runtime Library">
     <…>
 </window>

 <!-- The caption attribute in the following window element is 28 characters long. It is the shortest caption in this example, so its parent window element appears after the others. -->
 <window caption="Adobe Acrobat - Registration">
     <…>
 </window>
```

**windowList 要素内のウィンドウ要素の順序**

```xml
 <!-- The caption attribute in the following indexes element is 56 characters long. It is the longest caption in this example, so its parent window element appears before the others. -->
 <windowList>
     <window caption="Can&apos;t exit design mode because.* cannot be created"/>
     <window className="Button" caption="OK" action="press"/>
 </windowList>
 <windowList>
     <window caption="Do you want to continue loading the project?"/>
     <window className="Button" caption="No" action="press"/>
 </windowList>
 <windowList>
     <window caption="The macros in this project are disabled"/>
     <window className="Button" caption="OK" action="press"/>
 </windowList>
```

### ネイティブアプリケーション用の追加のダイアログ XML ファイルの作成または変更 {#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application}

以前にサポートされていなかったネイティブアプリケーション用のスクリプトを作成する場合は、そのアプリケーション用の追加のダイアログ XML ファイルも作成する必要があります。 AppMon が使用する各ネイティブアプリケーションには、1 つの追加のダイアログ XML ファイルのみを含める必要があります。 未承諾のダイアログボックスが見つからない場合でも、追加のダイアログ XML ファイルが必要です。 追加のダイアログボックスには、その `window` 要素が単なるプレースホルダーである場合でも、少なくとも 1 つの `window` 要素を含める必要があります。

>[!NOTE]
>
>このコンテキストでは、「追加」という用語は、`appmon.[applicationname].addition.[locale].xml` ファイルの内容を意味します。このようなファイルは、ダイアログ XML ファイルの上書きと追加を指定します。

また、以下の目的のために、ネイティブアプリケーション用の追加のダイアログ XML ファイルを変更することもできます。

* アプリケーションのダイアログ XML ファイルを別の応答で上書きする
* そのアプリケーションのダイアログ XML ファイル内で指定されていないダイアログボックスに応答を追加する

追加の dialogXML ファイルを識別するファイル名は、`appmon.[appname].addition.[locale].xml` です。（例：appmon.excel.addition.en_US.xml）

追加のダイアログ XML ファイルの名前には、`appmon.[applicationname].addition.[locale].xml` 形式を使用する必要があります。この形式では、*applicationname* は、XML 設定ファイルおよびスクリプトで使用されるアプリケーション名と完全に一致する必要があります。

>[!NOTE]
>
>native2pdfconfig.xml 設定ファイルで指定された一般のアプリケーションには、プライマリダイアログ XML ファイルが含まれていません。 この仕様については、[ ネイティブファイル形式に対するサポートの追加または変更](converting-file-formats-pdf.md#adding-or-modifying-support-for-a-native-file-format)のセクションで説明します。

`window` 要素で子として表示される `windowList` 要素に順序を付ける必要があります。（[window 要素と windowList 要素の順序](converting-file-formats-pdf.md#ordering-the-window-and-windowlist-elements)を参照してください。）

### 一般ダイアログ XML ファイルの変更 {#modifying-the-general-dialog-xml-file}

システムで生成されるダイアログボックスに応答したり、複数のアプリケーションに共通するダイアログボックスに応答したりするように、汎用ダイアログ XML ファイルを変更できます。

#### XML 設定ファイルへの filetype エントリの追加 {#adding-a-filetype-entry-in-the-xml-configuration-file}

この手順では、Generate PDF サービスの設定ファイルを更新して、ファイル形式をネイティブアプリケーションに関連付ける方法を説明します。 この設定ファイルを更新するには、管理コンソールを使用して設定データをファイルに書き出す必要があります。 設定データのデフォルトのファイル名は native2pdfconfig.xml です。

**Generate PDF サービスの設定ファイルの更新**

1. **ホーム**／**サービス**／**Adobe PDF Generator**／**設定ファイル**&#x200B;を選択し、「**設定の書き出し**」を選択します。
1. 必要に応じて、native2pdfconfig.xml ファイルの `filetype-settings` 要素を変更します。
1. **ホーム**／**サービス**／**Adobe PDF Generator**／**設定ファイル**&#x200B;を選択し、「**設定を読み込み**」を選択します。設定データが Generate PDF サービスに読み込まれ、以前の設定と置き換えられます。

>[!NOTE]
>
>アプリケーションの名前は、`GenericApp` 要素の `name` 属性の値として指定されます。 この値は、そのアプリケーション用に開発するスクリプトで指定された、対応する名前と完全に一致する必要があります。 同様に、`GenericApp` 要素の `displayName` 属性は、対応するスクリプトの `expectedWindow` ウィンドウのキャプションと完全に一致する必要があります。このような等価性は、`displayName` または `caption` 属性に表示される正規表現を解決した後に評価されます。

この例では、Generate PDF サービスで提供されるデフォルトの設定データを変更し、ファイル名拡張子が.txt のファイルを処理するために（Microsoft Word ではなく）メモ帳を使用するように指定しました。 この変更を行う前は、このようなファイルを処理するネイティブアプリケーションとして Microsoft Word が指定されていました。

**テキストファイルをメモ帳に転送するための変更（native2pdfconfig.xml）**

```xml
 <filetype-settings>

 <!-- Some native app file types were omitted for brevity. -->
 <!-- The following GenericApp element specifies Notepad as the native application that should be used to process files that have a txt file name extension. -->
             <GenericApp
                 extensions="txt"
                 name="Notepad" displayName=".*Notepad"/>
             <GenericApp
                 extensions="wpd"
                 name="WordPerfect" displayName="Corel WordPerfect"/>
             <GenericApp extensions="pmd,pm6,p65,pm"
                 name="PageMaker" displayName="Adobe PageMaker"/>
             <GenericApp extensions="fm"
                 name="FrameMaker" displayName="Adobe FrameMaker"/>
             <GenericApp extensions="psd"
                 name="Photoshop" displayName="Adobe Photoshop"/>
         </settings>
     </filetype-settings>
```

#### ネイティブアプリケーションを探すための環境変数の作成 {#creating-an-environment-variable-to-locate-the-native-application}

ネイティブアプリケーション実行可能ファイルの場所を指定する環境変数を作成します。 変数には `[applicationname]_PATH` 形式を使用する必要があります。ここでは、 *applicationname* は、XML 設定ファイルおよびスクリプトで使用されるアプリケーション名と完全に一致し、パスには二重引用符で囲んだ実行可能ファイルへのパスを含める必要があります。例えば、`Photoshop_PATH` のような環境変数になります。

新しい環境変数を作成した後、Generate PDF サービスがデプロイされているサーバーを再起動する必要があります。

**Windows XP 環境でのシステム変数の作成**

1. **コントロールパネル／システム**&#x200B;を選択します。
1. システムプロパティダイアログボックスで、「**詳細**」タブをクリックしてから、「**環境変数**」をクリックします。
1. 環境変数ダイアログボックスの 「システム変数」で、「**新規**」をクリックします。
1. 新規システム変数ダイアログボックスで、「**変数名**」ボックスに、`[applicationname]_PATH` 形式を使用して名前を入力します。
1. 「**変数値**」ボックスに、アプリケーションの実行可能ファイルのフルパスとファイル名を入力し、「**OK**」をクリックします。入力例 : `c:\windows\Notepad.exe`
1. 環境変数ダイアログボックスで、「 **OK**」をクリックします。

**コマンドラインからのシステム変数の作成**

1. コマンドラインウィンドウで、次の形式を使用して変数定義を入力します。

   ```shell
            [applicationname]_PATH=[Full path name]
   ```

   入力例 : `NotePad_PATH=C:\WINDOWS\NOTEPAD.EXE`

1. 新しいコマンドラインプロンプトを起動して、システム変数を有効にします。

#### XML ファイル {#xml-files}

AEM Forms には、Generate PDFサービスでメモ帳を使用してファイル名拡張子が.txt のファイルを処理するためのサンプル XML が含まれています。このコードはこのセクションに組み込まれています。さらに、この節で説明している、他の変更も加える必要があります。

#### 追加のダイアログ XML ファイル {#additional-dialog-xml-file}

以下は、メモ帳アプリケーションで追加するダイアログボックスの例を示します。これらのダイアログボックスは、Generate PDF サービスで指定するダイアログボックスに追加で設定できます。

**メモ帳ダイアログボックス（appmon.notepad.addition.en_US.xml）**

```xml
 <dialogs app="Notepad" locale="en_US" version="7.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="dialogs.xsd">
     <window caption="Caption Title">
         <windowList>
             <window className="Button" caption="OK" action="press"/>
         </windowList>
     </window>
 </dialogs>
```

#### スクリプト XML ファイル {#script-xml-file}

次の例では、Generate PDF サービスが Adobe PDF プリンターを使用することにより、メモ帳と連携してファイルを印刷する方法を指定しています。

**メモ帳スクリプト XML ファイル（appmon.notepad.script.en_US.xml）**

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<!--
*
* ADOBE CONFIDENTIAL
* ___________________
* Copyright 2004 - 2005 Adobe Systems Incorporated
* All Rights Reserved.
*
* NOTICE:  All information contained herein is, and remains
* the property of Adobe Systems Incorporated and its suppliers,
* if any.  The intellectual and technical concepts contained
* herein are proprietary to Adobe Systems Incorporated and its
* suppliers and may be covered by U.S. and Foreign Patents,
* patents in process, and are protected by trade secret or copyright law.
* Dissemination of this information or reproduction of this material
* is strictly forbidden unless prior written permission is obtained
* from Adobe Systems Incorporated.
*-->

<!-- This file automates printing of text files via notepad to Adobe PDF printer. In order to see the complete hierarchy we recommend using the Microsoft Spy++ which details the properties of windows necessary to write scripts. In this sample there are total of eight steps-->

<application name="Notepad" version="9.0" locale="en_US" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="scripts.xsd">

    <!-- In this step we wait for the application window to appear -->
    <step>
        <expectedWindow>
            <window caption=".*Notepad"/>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the application window and send File->Open menu bar, menu item commands and the expectation is the windows Open dialog-->
    <step>
        <acquiredWindow>
            <window caption=".*Notepad">
                <virtualInput>
                    <menuBar>
                        <selection>
                            <name>File</name>
                        </selection>
                        <selection>
                            <name>Open...</name>
                        </selection>
                    </menuBar>
                </virtualInput>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Open"/>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the Open window and then select the 'Edit' widget and input the source path followed by clicking on the 'Open' button . The expectation of this 'action' is that the Open dialog will disappear -->
    <step>
        <acquiredWindow>
            <window caption="Open">
                <windowList>
                    <window className="ComboBoxEx32">
                        <windowList>
                            <window className="ComboBox">
                                <windowList>
                                <window className="Edit" action="inputSourcePath"/>
                                </windowList>
                            </window>
                        </windowList>
                    </window>
                </windowList>
                <windowList>
                    <window className="Button" caption="Open" action="press"/>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Open" action="disappear"/>
        </expectedWindow>
        <pause value="30"/>
    </step>

    <!-- In this step, we acquire the application window and send File->Print menu bar, menu item commands and the expectation is the windows Print dialog-->
    <step>
        <acquiredWindow>
            <window caption=".*Notepad">
                <virtualInput>
                    <menuBar>
                        <selection>
                            <name>File</name>
                        </selection>
                        <selection>
                            <name>Print...</name>
                        </selection>
                    </menuBar>
                </virtualInput>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Print">
        </window>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the Print dialog and click on the 'Preferences' button and the expected window in this case is the dialog with the caption '"Printing Preferences' -->
    <step>
        <acquiredWindow>
            <window caption="Print">
                <windowList>
                    <window caption="General">
                        <windowList>
                            <window className="Button" caption="Preferences" action="press"/>
                        </windowList>
                    </window>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Printing Preferences"/>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the dialog "Printing Preferences' and select the combo box which is the 10th child of window with caption '"Adobe PDF Settings' and select the first index. (Note: All indeces start with 0.) Besides this we uncheck the box which  has the caption '"View Adobe PDF results' and we click on the button OK. The expectation is that 'Printing Preferences' dialog disappears. -->
    <step>
        <acquiredWindow>
            <window caption="Printing Preferences">
                <windowList>
                    <window caption="Adobe PDF Settings">
                        <windowList>
                            <window className="Button" caption="View Adobe PDF results" action="uncheck"/>
                        </windowList>
                        <windowList>
                            <window className="Button" caption="Ask to Replace existing PDF file" action="uncheck"/>
                        </windowList>
                    </window>
                </windowList>
                <windowList>
                    <window className="Button" caption="OK" action="press"/>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Printing Preferences" action="disappear"/>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the 'Print' dialog and click on the Print button. The expectation is that the dialog with caption 'Print' disappears. In this case we use the regular expression '^Print$' for specifying the caption given there could be multiple dialogs with caption that includes the word Print. -->
    <step>
        <acquiredWindow>
            <window caption="Print">
                <windowList>
                    <window caption="General"/>
                    <window className="Button" caption="^Print$" action="press"/>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Print" action="disappear"/>
        </expectedWindow>
    </step>
    <step>
        <expectedWindow>
            <window caption="Save PDF File As"/>
        </expectedWindow>
    </step>
    <!-- Finally in this step, we acquire the dialog with caption "Save PDF File As" and in the Edit widget type the destination path for the output PDF file and click on the Save button. The expectation is that the dialog disappears-->
    <step>
        <acquiredWindow>
            <window caption="Save PDF File As">
                <windowList>
                    <window className="Edit" action="inputDestinationPath"/>
                </windowList>
                <windowList>
                    <window className="Button" caption="Save" action="press"/>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Save PDF File As" action="disappear"/>
        </expectedWindow>
    </step>

    <!-- We can always set a retry count or a maximum time for a step. In case we surpass these limitations, PDF Generator generates this abort message and terminates processing. -->
    <abortMessage msg="15078"/>
</application>
```
