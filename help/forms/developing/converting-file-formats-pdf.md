---
title: ファイル形式とPDFの変換
seo-title: ファイル形式とPDFの変換
description: Generate PDFサービスを使用して、ネイティブファイル形式をPDFに変換します。 Generate PDFサービスは、PDFを他のファイル形式に変換し、PDFドキュメントのサイズを最適化します。
seo-description: Generate PDFサービスを使用して、ネイティブファイル形式をPDFに変換します。 Generate PDFサービスは、PDFを他のファイル形式に変換し、PDFドキュメントのサイズを最適化します。
uuid: f72ad603-c996-4d48-9bfc-bed7bf776af6
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 180cac3f-6378-42bc-9a47-60f9f08a7103
role: Developer
exl-id: 10535740-e3c2-4347-a88f-86706ad699b4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '7912'
ht-degree: 4%

---

# ファイル形式とPDF {#converting-between-file-formatsand-pdf}の変換

**このドキュメントのサンプルと例は、JEE上のAEM Forms環境に限られています。**

**Generate PDFサービスについて**

Generate PDF サービスは、ネイティブファイル形式を PDF に変換します。また、PDF を他のファイル形式に変換し、PDF ドキュメントのサイズを最適化します。

Generate PDF サービスは、以下のファイル形式を PDF に変換する際にネイティブアプリケーションを使用します。特に説明がない限り、これらのアプリケーションはドイツ語版、フランス語版、英語版および日本語版のみサポートされています。*Windows* は、Windows Server® 2003およびWindows Server 2008のみをサポートしていることを示しています。

* Microsoft Office 2003および2007:DOC、DOCX、RTF、TXT、XLS、XLSX、PPT、PPTX、VSD、MPP、MPPX、XPS、PUBの変換（Windowsのみ）

>[!NOTE]
>
>Acrobat® 9.2以降は、Microsoft XPS形式をPDFに変換する場合に必要です。

* DWF、DWG、DXWを変換するAutodesk AutoCAD 2005、2006、2007、2008、2009（英語のみ）
* WPD、QPW、SHWを変換するCorel WordPerfect 12およびX4（英語のみ）
* ODT、ODS、ODP、ODF、ODF、SXW、SXI、SXC、SXD、DOC、DOCX、RTF、TXT、TXT、XLS、XLSX、PPT、PPTX、VSD、MPP、MPPX、PUB

>[!NOTE]
>
>Generate PDFサービスは、64ビットバージョンのOpenOfficeをサポートしていません。

* Adobe Photoshop® CS2によるPSDの変換（Windowsのみ）

>[!NOTE]
>
>Photoshop CS3とCS4は、Windows Server 2003またはWindows Server 2008をサポートしていないので、サポートされていません。

* FMの変換：Adobe FrameMaker® 7.2および8（Windowsのみ）
* PMD、PM6、P65、PM の変換：Adobe PageMaker® 7.0（Windows のみ）
* サードパーティのアプリケーションによってサポートされているネイティブ形式（アプリケーションに固有のセットアップファイルの開発が必要）（Windows のみ）

Generate PDF サービスでは、次の標準ベースのファイル形式を PDF に変換します。

* ビデオファイル形式：SWF、FLV（Windows のみ）
* 画像ファイル形式：JPEG、JPG、JP2、J2Kí、JPC、J2C、GIF、BMP、TIFF、TIF、PNG、JPF
* HTML (Windows、Sun™ Solaris™およびLinux®)

Generate PDF サービスでは、PDF を次のファイル形式に変換します（Windows のみ）：

* EPS（Encapsulated PostScript）
* HTML3.2
* CSS 1.0 を使用した HTML 4.01
* DOC（Microsoft Word format）
* RTF
* テキスト（アクセス可能およびプレーンの両方）
* XML
* PDF/A-1a（DeviceRGBカラースペースのみを使用）
* PDF/A-1b（DeviceRGBカラースペースのみを使用）

Generate PDF サービスを使用するには、以下の管理タスクを実行する必要があります。

* 必要なネイティブアプリケーションを、AEM Forms をホストするコンピューター上にインストールする
* AEM FormsをホストするコンピューターにAdobe Acrobat ProfessionalまたはAcrobat Pro Extended 9.2をインストールする
* インストール後のセットアップタスクを実行する

これらのタスクについては、「 AEM formsの自動インストールおよびデプロイ（JBoss版） 」を参照してください。

Generate PDFサービスを使用して、次のタスクを実行できます。

* ネイティブファイル形式からPDFに変換します。
* HTMLドキュメントをPDFドキュメントに変換します。
* PDFドキュメントをファイル形式に変換します。

>[!NOTE]
>
>Generate PDFサービスについて詳しくは、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

## Word文書のPDF文書への変換{#converting-word-documents-to-pdf-documents}

この節では、Generate PDF APIを使用して、Microsoft Word文書をプログラムでPDF文書に変換する方法について説明します。

>[!NOTE]
>
>追加のファイル形式について詳しくは、[追加のネイティブファイル形式](converting-file-formats-pdf.md#adding-support-for-additional-native-file-formats)のサポートの追加を参照してください。

>[!NOTE]
>
>Generate PDFサービスについて詳しくは、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順の概要{#summary-of-steps}

Microsoft Word文書をPDF文書に変換するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Generate PDFクライアントを作成します。
1. PDFドキュメントに変換するファイルを取得します。
1. ファイルをPDFドキュメントに変換します。
1. 結果を取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用する場合は、プロキシファイルを必ず含めてください。

**Generate PDFクライアントの作成**

プログラムによって「Generate PDF」操作を実行する前に、Generate PDFサービスクライアントを作成します。 Java APIを使用している場合は、`GeneratePdfServiceClient`オブジェクトを作成します。 WebサービスAPIを使用している場合は、`GeneratePDFServiceService`オブジェクトを作成します。

**PDFドキュメントに変換するファイルの取得**

PDFドキュメントに変換するMicrosoft Wordドキュメントを取得します。

**ファイルをPDFドキュメントに変換する**

Generate PDFサービスクライアントを作成した後、 `createPDF2`メソッドを呼び出すことができます。 このメソッドでは、変換するドキュメントに関する情報（ファイル拡張子を含む）が必要です。

**結果の取得**

ファイルをPDFドキュメントに変換した後、結果を取得できます。 例えば、WordファイルをPDFドキュメントに変換した後に、そのPDFドキュメントを取得して保存することができます。

**関連トピック**

[Java APIを使用したWord文書のPDF文書への変換](converting-file-formats-pdf.md#convert-word-documents-to-pdf-documents-using-the-java-api)

[WebサービスAPIを使用したWordドキュメントのPDFドキュメントへの変換](converting-file-formats-pdf.md#convert-word-documents-to-pdf-documents-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Generate PDFサービスAPIのクイックスタート](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### Java APIを使用してWord文書をPDF文書に変換する{#convert-word-documents-to-pdf-documents-using-the-java-api}

Generate PDF API(Java)を使用して、Microsoft WordドキュメントをPDFドキュメントに変換します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-generatepdf-client.jarなどのクライアントJARファイルを含めます。

1. Generate PDFクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `GeneratePdfServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. PDFドキュメントに変換するファイルを取得します。

   * 変換するWordファイルを表す`java.io.FileInputStream`オブジェクトを、コンストラクターを使用して作成します。 ファイルの場所を指定するstring値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. ファイルをPDFドキュメントに変換します。

   `GeneratePdfServiceClient`オブジェクトの`createPDF2`メソッドを呼び出し、次の値を渡して、ファイルをPDFドキュメントに変換します。

   * 変換するファイルを表す`com.adobe.idp.Document`オブジェクト。
   * ファイル拡張子を含む`java.lang.String`オブジェクト。
   * 変換処理で使用されるファイルタイプ設定を含む`java.lang.String`オブジェクト。 ファイルタイプ設定は、.docや.xlsなど、様々なファイルタイプの変換設定を提供します。
   * 使用するPDF設定の名前を格納する`java.lang.String`オブジェクト。 例えば、`Standard`を指定できます。
   * 使用するセキュリティ設定の名前を含む`java.lang.String`オブジェクト。
   * PDFドキュメントの生成中に適用される設定を含む、オプションの`com.adobe.idp.Document`オブジェクトです。
   * PDFドキュメントに適用するメタデータ情報を含む、オプションの`com.adobe.idp.Document`オブジェクトです。

   `createPDF2`メソッドは、新しいPDFドキュメントとログ情報を含む`CreatePDFResult`オブジェクトを返します。 通常、ログファイルには、変換リクエストによって生成されたエラーメッセージや警告メッセージが含まれます。

1. 結果を取得します。

   PDFドキュメントを取得するには、次の操作を実行します。

   * `CreatePDFResult`オブジェクトの`getCreatedDocument`メソッドを呼び出し、`com.adobe.idp.Document`オブジェクトを返します。
   * `com.adobe.idp.Document`オブジェクトの`copyToFile`メソッドを呼び出して、前の手順で作成したオブジェクトからPDFドキュメントを抽出します。

   `createPDF2`メソッドを使用してログドキュメントを取得した場合（HTML変換には適用されません）、次の操作を実行します。

   * `CreatePDFResult`オブジェクトの`getLogDocument`メソッドを呼び出します。 `com.adobe.idp.Document`オブジェクトを返します。
   * `com.adobe.idp.Document`オブジェクトの`copyToFile`メソッドを呼び出して、ログドキュメントを抽出します。


**関連トピック**

[手順の概要](converting-file-formats-pdf.md#summary-of-steps)

[クイックスタート（SOAPモード）:Java APIを使用したMicrosoft Word文書のPDF文書への変換](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-a-microsoft-word-document-to-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用してWordドキュメントをPDFドキュメントに変換します。 {#convert-word-documents-to-pdf-documents-using-the-web-service-api}

Generate PDF API（Webサービス）を使用して、Microsoft WordドキュメントをPDFドキュメントに変換します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. Generate PDFクライアントを作成します。

   * デフォルトのコンストラクターを使用して`GeneratePDFServiceClient`オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`GeneratePDFServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに渡す文字列値（例：`http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`）を渡します。 `lc_version`属性を使用する必要はありません。 ただし、`?blob=mtom`と指定します。
   * `GeneratePDFServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値は、MTOMが使用されるようにします。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールド`GeneratePDFServiceClient.ClientCredentials.UserName.UserName`にAEM formsユーザー名を割り当てます。
      * 対応するパスワード値をフィールド`GeneratePDFServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * フィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に定数値`HttpClientCredentialType.Basic`を割り当てます。
      * フィールド`BasicHttpBindingSecurity.Security.Mode`に定数値`BasicHttpSecurityMode.TransportCredentialOnly`を割り当てます。

1. PDFドキュメントに変換するファイルを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、PDFドキュメントに変換するファイルを保存するために使用します。
   * コンストラクターを呼び出して、`System.IO.FileStream`オブジェクトを作成します。 変換するファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得することで、バイト配列のサイズを判断できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことによって、バイト配列にストリームデータを入力します。
   * `BLOB`オブジェクトの`MTOM`プロパティにバイト配列の内容を割り当てて、オブジェクトを設定します。

1. ファイルをPDFドキュメントに変換します。

   `GeneratePDFServiceService`オブジェクトの`CreatePDF2`メソッドを呼び出し、次の値を渡して、ファイルをPDFドキュメントに変換します。

   * 変換するファイルを表す`BLOB`オブジェクト。
   * ファイル拡張子を含む文字列。
   * 変換処理で使用されるファイルタイプ設定を含む`java.lang.String`オブジェクト。 ファイルタイプ設定は、.docや.xlsなど、様々なファイルタイプの変換設定を提供します。
   * 使用するPDF設定を含むstringオブジェクト。 `Standard`を指定できます。
   * 使用するセキュリティ設定を含む文字列オブジェクト。 `No Security`を指定できます。
   * PDFドキュメントの生成中に適用される設定を含む、オプションの`BLOB`オブジェクトです。
   * PDFドキュメントに適用するメタデータ情報を含む、オプションの`BLOB`オブジェクトです。
   * `CreatePDF2`メソッドによって設定される、タイプ`BLOB`の出力パラメーター。 `CreatePDF2`メソッドは、このオブジェクトに変換後のドキュメントを入力します。 （このパラメーター値は、Webサービスの呼び出しにのみ必要です）。
   * `CreatePDF2`メソッドによって設定される、タイプ`BLOB`の出力パラメーター。 `CreatePDF2`メソッドは、このオブジェクトにログドキュメントを入力します。 （このパラメーター値は、Webサービスの呼び出しにのみ必要です）。

1. 結果を取得します。

   * `BLOB`オブジェクトの`MTOM`フィールドをバイト配列に割り当てて、変換後のPDFドキュメントを取得します。 byte配列は変換されたPDFドキュメントを表します。 `createPDF2`メソッドの出力パラメーターとして使用する`BLOB`オブジェクトを使用してください。
   * コンストラクターを呼び出し、変換後のPDFドキュメントのファイルの場所を表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * コンストラクターを呼び出し、`System.IO.FileStream`オブジェクトを渡して、`System.IO.BinaryWriter`オブジェクトを作成します。
   * `System.IO.BinaryWriter`オブジェクトの`Write`メソッドを呼び出し、バイト配列を渡すことにより、バイト配列の内容をPDFファイルに書き込みます。

**関連トピック**

[手順の概要](converting-file-formats-pdf.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## HTMLドキュメントからPDFドキュメントへの変換{#converting-html-documents-to-pdf-documents}

この節では、Generate PDF APIを使用してHTMLドキュメントをPDFドキュメントにプログラムで変換する方法について説明します。

>[!NOTE]
>
>Generate PDFサービスについて詳しくは、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順の概要{#summary_of_steps-1}

HTMLドキュメントをPDFドキュメントに変換するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Generate PDFクライアントを作成します。
1. PDFドキュメントに変換するHTMLコンテンツを取得します。
1. HTMLコンテンツをPDFドキュメントに変換します。
1. 結果を取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用する場合は、プロキシファイルを必ず含めてください。

**Generate PDFクライアントの作成**

プログラムによって「Generate PDF」操作を実行する前に、Generate PDFサービスクライアントを作成する必要があります。 Java APIを使用している場合は、`GeneratePdfServiceClient`オブジェクトを作成します。 WebサービスAPIを使用している場合は、`GeneratePDFServiceService`を作成します。

**PDFドキュメントに変換するHTMLコンテンツの取得**

PDFドキュメントに変換するHTMLコンテンツを参照します。 HTMLファイルや、URLを使用してアクセス可能なHTMLコンテンツなどのHTMLコンテンツを参照できます。

**HTMLコンテンツをPDFドキュメントに変換する**

サービスクライアントを作成した後で、適切なPDF作成操作を呼び出すことができます。 この操作では、変換対象のドキュメントのパスを含む、変換対象のドキュメントに関する情報が必要です。

**結果の取得**

HTMLコンテンツをPDFドキュメントに変換した後、結果を取得してPDFドキュメントを保存できます。

**関連トピック**

[Java APIを使用したHTMLコンテンツのPDFドキュメントへの変換](converting-file-formats-pdf.md#convert-html-content-to-a-pdf-document-using-the-java-api)

[WebサービスAPIを使用したHTMLコンテンツのPDFドキュメントへの変換](converting-file-formats-pdf.md#convert-html-content-to-a-pdf-document-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Generate PDFサービスAPIのクイックスタート](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### Java API {#convert-html-content-to-a-pdf-document-using-the-java-api}を使用してHTMLコンテンツをPDFドキュメントに変換します

Generate PDF API(Java)を使用してHTMLドキュメントをPDFドキュメントに変換します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-generatepdf-client.jarなどのクライアントJARファイルを含めます。

1. Generate PDFクライアントを作成します。

   コンストラクターを使用し、接続プロパティを含む`ServiceClientFactory`オブジェクトを渡して、`GeneratePdfServiceClient`オブジェクトを作成します。

1. PDFドキュメントに変換するHTMLコンテンツを取得します。

   文字列変数を作成し、HTMLコンテンツを指すURLを割り当てて、HTMLコンテンツを取得します。

1. HTMLコンテンツをPDFドキュメントに変換します。

   `GeneratePdfServiceClient`オブジェクトの`htmlToPDF2`メソッドを呼び出し、次の値を渡します。

   * 変換するHTMLファイルのURLを含む`java.lang.String`オブジェクト。
   * 変換処理で使用されるファイルタイプ設定を含む`java.lang.String`オブジェクト。 ファイルタイプの設定には、スパイダリングレベルを含めることができます。
   * 使用するセキュリティ設定の名前を含む`java.lang.String`オブジェクト。
   * PDFドキュメントの生成中に適用される設定を含む、オプションの`com.adobe.idp.Document`オブジェクトです。 この情報を指定しない場合、設定は前の3つのパラメーターに基づいて自動的に選択されます。
   * PDFドキュメントに適用するメタデータ情報を含む、オプションの`com.adobe.idp.Document`オブジェクトです。

1. 結果を取得します。

   `htmlToPDF2`メソッドは、生成された新しいPDFドキュメントを含む`HtmlToPdfResult`オブジェクトを返します。 新しく作成したPDFドキュメントを取得するには、次の操作を実行します。

   * `HtmlToPdfResult`オブジェクトの`getCreatedDocument`メソッドを呼び出します。 `com.adobe.idp.Document`オブジェクトを返します。
   * `com.adobe.idp.Document`オブジェクトの`copyToFile`メソッドを呼び出して、前の手順で作成したオブジェクトからPDFドキュメントを抽出します。

**関連トピック**

[HTMLドキュメントからPDFドキュメントへの変換](converting-file-formats-pdf.md#converting-html-documents-to-pdf-documents)

[クイックスタート（SOAPモード）:Java APIを使用したHTMLコンテンツからPDFドキュメントへの変換](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[クイックスタート（SOAPモード）:Java APIを使用したHTMLコンテンツからPDFドキュメントへの変換](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#convert-html-content-to-a-pdf-document-using-the-web-service-api}を使用してHTMLコンテンツをPDFドキュメントに変換します

Generate PDF API（Webサービス）を使用して、HTMLコンテンツをPDFドキュメントに変換します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. Generate PDFクライアントを作成します。

   * デフォルトのコンストラクターを使用して`GeneratePDFServiceClient`オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`GeneratePDFServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに渡す文字列値（例：`http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`）を渡します。 `lc_version`属性を使用する必要はありません。 ただし、`?blob=mtom`と指定します。
   * `GeneratePDFServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値は、MTOMが使用されるようにします。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールド`GeneratePDFServiceClient.ClientCredentials.UserName.UserName`にAEM formsユーザー名を割り当てます。
      * 対応するパスワード値をフィールド`GeneratePDFServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * フィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に定数値`HttpClientCredentialType.Basic`を割り当てます。
      * フィールド`BasicHttpBindingSecurity.Security.Mode`に定数値`BasicHttpSecurityMode.TransportCredentialOnly`を割り当てます。

1. PDFドキュメントに変換するHTMLコンテンツを取得します。

   文字列変数を作成し、HTMLコンテンツを指すURLを割り当てて、HTMLコンテンツを取得します。

1. HTMLコンテンツをPDFドキュメントに変換します。

   `GeneratePDFServiceService`オブジェクトの`HtmlToPDF2`メソッドを呼び出し、次の値を渡して、HTMLコンテンツをPDFドキュメントに変換します。

   * 変換するHTMLコンテンツを含む文字列。
   * 変換処理で使用されるファイルタイプ設定を含む`java.lang.String`オブジェクト。
   * 使用するセキュリティ設定を含む文字列オブジェクト。
   * PDFドキュメントの生成中に適用される設定を含む、オプションの`BLOB`オブジェクトです。
   * PDFドキュメントに適用するメタデータ情報を含む、オプションの`BLOB`オブジェクトです。
   * `CreatePDF2`メソッドによって設定される、タイプ`BLOB`の出力パラメーター。 `CreatePDF2`メソッドは、このオブジェクトに変換後のドキュメントを入力します。 （このパラメーター値は、Webサービスの呼び出しにのみ必要です）。

1. 結果を取得します。

   * `BLOB`オブジェクトの`MTOM`フィールドをバイト配列に割り当てて、変換後のPDFドキュメントを取得します。 byte配列は変換されたPDFドキュメントを表します。 `HtmlToPDF2`メソッドの出力パラメーターとして使用する`BLOB`オブジェクトを使用してください。
   * コンストラクターを呼び出し、変換後のPDFドキュメントのファイルの場所を表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * コンストラクターを呼び出し、`System.IO.FileStream`オブジェクトを渡して、`System.IO.BinaryWriter`オブジェクトを作成します。
   * `System.IO.BinaryWriter`オブジェクトの`Write`メソッドを呼び出し、バイト配列を渡すことにより、バイト配列の内容をPDFファイルに書き込みます。

**関連トピック**

[HTMLドキュメントからPDFドキュメントへの変換](converting-file-formats-pdf.md#converting-html-documents-to-pdf-documents)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## PDFドキュメントを非画像形式に変換する{#converting-pdf-documents-to-non-image-formats}

この節では、Generate PDF Java APIとWebサービスAPIを使用して、PDFドキュメントを画像以外の形式の例であるRTFファイルにプログラムで変換する方法について説明します。 その他の画像以外の形式には、HTML、テキスト、DOC、EPSなどがあります。 PDFドキュメントをRTFに変換する場合は、送信ボタンなどのフォーム要素がPDFドキュメントに含まれていないことを確認してください。 フォーム要素は変換されません。

>[!NOTE]
>
>Generate PDFサービスについて詳しくは、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順の概要{#summary_of_steps-2}

PDFドキュメントをサポートされているいずれかのタイプに変換するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Generate PDFクライアントを作成します。
1. 変換するPDFドキュメントを取得します。
1. PDFドキュメントを変換します。
1. 変換したファイルを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用する場合は、プロキシファイルを必ず含めてください。

**Generate PDFクライアントの作成**

プログラムによって「Generate PDF」操作を実行する前に、Generate PDFサービスクライアントを作成する必要があります。 Java APIを使用している場合は、`GeneratePdfServiceClient`オブジェクトを作成します。 WebサービスAPIを使用している場合は、`GeneratePDFServiceService`オブジェクトを作成します。

**変換するPDFドキュメントを取得する**

画像以外の形式に変換するPDFドキュメントを取得します。

**PDFドキュメントの変換**

サービスクライアントを作成した後で、PDF書き出し操作を呼び出すことができます。 この操作では、変換対象のドキュメントのパスを含む、変換対象のドキュメントに関する情報が必要です。

**変換したファイルを保存します。**

変換したファイルを保存します。 例えば、PDFドキュメントをRTFファイルに変換する場合、変換後のドキュメントをRTFファイルに保存します。

**関連トピック**

[Java APIを使用したPDFドキュメントのRTFファイルへの変換](converting-file-formats-pdf.md#convert-a-pdf-document-to-a-rtf-file-using-the-java-api)

[WebサービスAPIを使用したPDFドキュメントのRTFファイルへの変換](converting-file-formats-pdf.md#convert-a-pdf-document-to-a-rtf-file-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Generate PDFサービスAPIのクイックスタート](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### Java API {#convert-a-pdf-document-to-a-rtf-file-using-the-java-api}を使用してPDFドキュメントをRTFファイルに変換します

Generate PDF API(Java)を使用してPDFドキュメントをRTFファイルに変換します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-generatepdf-client.jarなどのクライアントJARファイルを含めます。

1. Generate PDFクライアントを作成します。

   コンストラクターを使用し、接続プロパティを含む`ServiceClientFactory`オブジェクトを渡して、`GeneratePdfServiceClient`オブジェクトを作成します。

1. 変換するPDFドキュメントを取得します。

   * 変換するPDFドキュメントを表す`java.io.FileInputStream`オブジェクトを、コンストラクタを使用して作成します。 PDFドキュメントの場所を指定するstring値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PDFドキュメントを変換します。

   `GeneratePdfServiceClient`オブジェクトの`exportPDF2`メソッドを呼び出し、次の値を渡します。

   * 変換するPDFファイルを表す`com.adobe.idp.Document`オブジェクト。
   * 変換するファイルの名前を格納する`java.lang.String`オブジェクト。
   * Adobe PDF設定の名前を格納する`java.lang.String`オブジェクト。
   * 変換対象のファイルの種類を指定する`ConvertPDFFormatType`オブジェクト。
   * PDFドキュメントの生成中に適用される設定を含む、オプションの`com.adobe.idp.Document`オブジェクトです。

   `exportPDF2`メソッドは、変換されたファイルを含む`ExportPDFResult`オブジェクトを返します。

1. PDFドキュメントを変換します。

   新しく作成されたファイルを取得するには、次の操作を実行します。

   * `ExportPDFResult`オブジェクトの`getConvertedDocument`メソッドを呼び出します。 `com.adobe.idp.Document`オブジェクトを返します。
   * `com.adobe.idp.Document`オブジェクトの`copyToFile`メソッドを呼び出して、新しいドキュメントを抽出します。

**関連トピック**

[手順の概要](converting-file-formats-pdf.md#summary-of-steps)

[クイックスタート（SOAPモード）:Java APIを使用したHTMLコンテンツからPDFドキュメントへの変換](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#convert-a-pdf-document-to-a-rtf-file-using-the-web-service-api}を使用してPDFドキュメントをRTFファイルに変換します

Generate PDF API（Webサービス）を使用してPDFドキュメントをRTFファイルに変換します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. Generate PDfクライアントを作成します。

   * デフォルトのコンストラクターを使用して`GeneratePDFServiceClient`オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`GeneratePDFServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに渡す文字列値（例：`http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`）を渡します。 `lc_version`属性を使用する必要はありません。 ただし、`?blob=mtom`と指定します。
   * `GeneratePDFServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値は、MTOMが使用されるようにします。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールド`GeneratePDFServiceClient.ClientCredentials.UserName.UserName`にAEM formsユーザー名を割り当てます。
      * 対応するパスワード値をフィールド`GeneratePDFServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * フィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に定数値`HttpClientCredentialType.Basic`を割り当てます。
      * フィールド`BasicHttpBindingSecurity.Security.Mode`に定数値`BasicHttpSecurityMode.TransportCredentialOnly`を割り当てます。

1. 変換するPDFドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、変換されたPDFドキュメントを保存するために使用されます。
   * コンストラクターを呼び出し、PDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得することで、バイト配列のサイズを判断できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことによって、バイト配列にストリームデータを入力します。
   * `BLOB`オブジェクトの`MTOM`プロパティにバイト配列の内容を割り当てて、オブジェクトを設定します。

1. PDFドキュメントを変換します。

   `GeneratePDFServiceServiceWse`オブジェクトの`ExportPDF2`メソッドを呼び出し、次の値を渡します。

   * 変換するPDFファイルを表す`BLOB`オブジェクト。
   * 変換するファイルのパス名を含む文字列。
   * ファイルの場所を指定する`java.lang.String`オブジェクト。
   * 変換対象のファイルの種類を指定するstringオブジェクト。 以下のように `RTF`.
   * PDFドキュメントの生成中に適用される設定を含む、オプションの`BLOB`オブジェクトです。
   * `ExportPDF2`メソッドによって設定される、タイプ`BLOB`の出力パラメーター。 `ExportPDF2`メソッドは、このオブジェクトに変換後のドキュメントを入力します。 （このパラメーター値は、Webサービスの呼び出しにのみ必要です）。

1. 変換したファイルを保存します。

   * `BLOB`オブジェクトの`MTOM`フィールドをバイト配列に割り当てて、変換したRTFドキュメントを取得します。 バイト配列は、変換されたRTFドキュメントを表します。 `ExportPDF2`メソッドの出力パラメーターとして使用する`BLOB`オブジェクトを使用してください。
   * コンストラクターを呼び出して、`System.IO.FileStream`オブジェクトを作成します。 RTFファイルの場所を表すstring値を渡します。
   * コンストラクターを呼び出し、`System.IO.FileStream`オブジェクトを渡して、`System.IO.BinaryWriter`オブジェクトを作成します。
   * `System.IO.BinaryWriter`オブジェクトの`Write`メソッドを呼び出し、バイト配列を渡すことで、バイト配列の内容をRTFファイルに書き込みます。

**関連トピック**

[手順の概要](converting-file-formats-pdf.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 追加のネイティブファイル形式{#adding-support-for-additional-native-file-formats}のサポートの追加

この節では、追加のネイティブファイル形式のサポートを追加する方法について説明します。 Generate PDFサービスと、このサービスでネイティブファイル形式をPDFに変換する際に使用されるネイティブアプリケーションとの間のインタラクションの概要を示します。

この節では、以下についても説明します。

* この製品でネイティブファイル形式をPDFに変換する際に既に使用されているネイティブアプリケーションに対するGenerate PDFサービスの応答を変更する方法
* Generate PDFサービス、Generate PDFサービスのApplication Monitor(AppMon)コンポーネント、およびMicrosoft Wordなどのネイティブアプリケーション間のインタラクション
* XMLグラマーがこれらの操作で果たす役割

### コンポーネントの操作{#component-interactions}

Generate PDFサービスは、ネイティブファイル形式を変換します。そのためには、ファイル形式に関連付けられたアプリケーションを呼び出し、アプリケーションとやり取りして、デフォルトのプリンターを使用してドキュメントを印刷します。 デフォルトのプリンターをAdobe PDFプリンターとして設定する必要があります。

この図は、ネイティブアプリケーションサポートに関連するコンポーネントとドライバを示しています。 また、インタラクションに影響を与えるXML文法についても言及しています。

ネイティブファイル変換のコンポーネントのインタラクション

このドキュメントでは、*ネイティブアプリケーション*&#x200B;という用語を使用して、Microsoft Wordなどのネイティブファイル形式の作成に使用するアプリケーションを示します。

** AppMonisは、ユーザーがそのアプリケーションで表示されるダイアログボックス内を移動するのと同じ方法でネイティブアプリケーションとやり取りするエンタープライズコンポーネントです。AppMonがMicrosoft Wordなどのアプリケーションに対して、次の順次タスクを含むファイルを開いて印刷するように指示する際に使用するXMLグラマー。

1. ファイル/開くを選択してファイルを開く
1. [開く]ダイアログボックスが表示されていることを確認します。そうでない場合は、エラーの処理
1. 「ファイル名」フィールドにファイル名を入力し、「開く」ボタンをクリックします
1. ファイルが実際に開かれることを確認する
1. ファイル/印刷を選択して、印刷ダイアログボックスを開きます。
1. [印刷]ダイアログボックスが表示されることを確認する

AppMonは、標準のWin32 APIを使用して、キーストロークやマウスクリックなどのUIイベントを転送するためにサードパーティのアプリケーションとやり取りし、これらのアプリケーションを制御してPDFファイルを生成するのに役立ちます。

これらのWin32 APIの制限により、AppMonは、フローティングメニューバー（TextPadなどの一部のアプリケーションで見つかる）や、Win32 APIを使用してコンテンツを取得できない特定の種類のダイアログなど、特定の種類のウィンドウにこれらのUIイベントをディスパッチできません。

フローティングメニューバーを視覚的に識別するのは簡単です。ただし、特別な種類のダイアログは、視覚的な検査だけでは特定できない可能性があります。 AppMonが標準のWin32 APIを使用してAppMonとやり取りできるかどうかを確認するダイアログを調べるには、Microsoft Spy++ (Microsoft Visual C++開発環境の一部)または同等のWinID ([https://www.dennisbabkin.com/php/download.php?what=WinID](https://www.dennisbabkin.com/php/download.php?what=WinID)から無料でダウンロードできる)などのサードパーティアプリケーションが必要です。

WinIDがテキスト、サブウィンドウ、ウィンドウクラスIDなどのダイアログコンテンツを抽出できる場合は、AppMonも同じ処理を行うことができます。

次の表に、ネイティブファイル形式の印刷に使用する情報の種類を示します。

<table>
 <thead>
  <tr>
   <th><p>情報タイプ</p></th>
   <th><p>説明</p></th>
   <th><p>ネイティブファイルに関連するエントリの変更/作成 </p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>管理設定 </p></td>
   <td><p>PDF設定、セキュリティ設定、ファイルタイプ設定が含まれます。 </p><p>ファイルタイプ設定は、ファイル名拡張子を対応するネイティブアプリケーションに関連付けます。 ファイルタイプの設定では、ネイティブファイルの印刷に使用するネイティブアプリケーション設定も指定します。 </p></td>
   <td><p>既にサポートされているネイティブアプリケーションの設定を変更するには、システム管理者が管理コンソールで「ファイルタイプ設定」を設定します。 </p><p>新しいネイティブファイル形式のサポートを追加するには、ファイルを手動で編集する必要があります。 （<a href="converting-file-formats-pdf.md#adding-or-modifying-support-for-a-native-file-format">ネイティブファイル形式</a>のサポートの追加または変更を参照）。 </p></td>
  </tr>
  <tr>
   <td><p>スクリプト </p></td>
   <td><p>Generate PDFサービスとネイティブアプリケーションの間のインタラクションを指定します。 このようなやり取りは、通常、アプリケーションに対して、Adobe PDFドライバーにファイルを印刷するよう指示します。 </p><p>このスクリプトには、ネイティブアプリケーションに特定のダイアログボックスを開くよう指示し、それらのダイアログボックスのフィールドやボタンに対して特定の応答を提供する指示が含まれています。 </p></td>
   <td><p>Generate PDFサービスには、サポートされるすべてのネイティブアプリケーション用のスクリプトファイルが含まれます。 これらのファイルは、XML編集アプリケーションを使用して変更できます。</p><p>新しいネイティブアプリケーションのサポートを追加するには、新しいスクリプトファイルを作成する必要があります。 （<a href="converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application">ネイティブアプリケーション用の追加のダイアログXMLファイルの作成または変更</a>を参照）。 </p></td>
  </tr>
  <tr>
   <td><p>[汎用]ダイアログボックスの手順 </p></td>
   <td><p>複数のアプリケーションに共通のダイアログボックスに対する応答方法を指定します。 このようなダイアログボックスは、オペレーティングシステム、ヘルパーアプリケーション（PDFMakerなど）、ドライバによって生成されます。 </p><p>この情報を格納するファイルは、appmon.global.en_US.xmlです。</p></td>
   <td><p>このファイルは変更しないでください。 </p></td>
  </tr>
  <tr>
   <td><p>アプリケーション固有のダイアログボックスの手順</p></td>
   <td><p>アプリケーション固有のダイアログボックスに対する応答方法を指定します。 </p><p>この情報を含むファイルはappmonです。<i>'[appname]'</i>.dialog.<i>'[locale]'</i>.xml （例：appmon.word.en_US.xml）</p></td>
   <td><p>このファイルは変更しないでください。 </p><p>新しいネイティブアプリケーション用のダイアログボックスの手順を追加するには、<a href="converting-file-formats-pdf.md#creating_or_modifying_an_additional_dialog_xml_file_for_a_native_application">ネイティブアプリケーション用の追加のダイアログXMLファイルの作成または変更</a>を参照してください。</p></td>
  </tr>
  <tr>
   <td><p>その他のアプリケーション固有のダイアログボックスの手順 </p></td>
   <td><p>アプリケーション固有のダイアログボックスの手順に対する上書きと追加を指定します。 この節では、このような情報の例を示します。 </p><p>この情報を含むファイルはappmonです。<i>'[appname]'</i>.addition.<i>'[locale]'</i>.xml.例えば、 appmon.addition.en_US.xmlなどです。</p></td>
   <td><p>このタイプのファイルは、XML編集アプリケーションを使用して作成および変更できます。 （<a href="converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application">ネイティブアプリケーション用の追加のダイアログXMLファイルの作成または変更</a>を参照）。 </p><p><strong>重要</strong>:サーバーがサポートするネイティブアプリケーションごとに、追加のアプリケーション固有のダイアログボックスの手順を作成する必要があります。 </p></td>
  </tr>
 </tbody>
</table>

### スクリプトとダイアログのXMLファイルについて{#about-the-script-and-dialog-xml-files}

スクリプトXMLファイルは、ユーザーがアプリケーションダイアログボックス内を移動するのと同じ方法で、Generate PDFサービスにアプリケーションダイアログボックス内を移動するよう指示します。 スクリプトXMLファイルは、ボタンの押し方、チェックボックスの選択/選択解除、メニュー項目の選択などの操作を実行して、ダイアログボックスに応答するようGenerate PDFサービスに指示します。

これに対し、ダイアログXMLファイルは、スクリプトXMLファイルと同じタイプのアクションを持つダイアログボックスに対応します。

#### ダイアログボックスとウィンドウ要素の用語{#dialog-box-and-window-element-terminology}

この節と次の節では、説明するパースペクティブに応じて、ダイアログボックスと含まれるコンポーネントに対して異なる用語を使用します。 ダイアログボックスのコンポーネントは、ボタン、フィールド、コンボボックスなどの項目です。

この節と次の節では、ユーザーの観点からダイアログボックスとそのコンポーネントを説明する際に、*ダイアログボックス*、*ボタン*、*フィールド*、*コンボボックス*&#x200B;などの用語を使用します。

この節と次の節では、ダイアログボックスとそのコンポーネントを内部表現の観点から説明する際に、*window要素*&#x200B;という用語が使用されます。 窓要素の内部表現は階層で、各窓要素のインスタンスはラベルで識別されます。 ウィンドウ要素インスタンスは、その物理的な特性と動作も記述します。

ユーザーの視点から見ると、ダイアログボックスとそのコンポーネントは異なる動作を示し、一部のダイアログボックス要素は、アクティブになるまで非表示になります。 内部表現の観点からは、そのような動作の問題は存在しません。 例えば、ダイアログボックスの内部表現は、ダイアログボックス内にネストされている点を除いて、ダイアログボックスに含まれるコンポーネントの内部表現と似ています。

この節では、AppMonに手順を提供するXML要素について説明します。 これらの要素には、`dialog`要素や`window`要素などの名前が付けられます。 このドキュメントでは、XML要素を区別するために等幅フォントを使用します。 `dialog`要素は、XMLスクリプトファイルが意図的に、または意図せずに表示される原因となる可能性があるダイアログボックスを識別します。 `window`要素は、ウィンドウ要素（ダイアログボックスまたはダイアログボックスのコンポーネント）を識別します。

#### 階層 {#hierarchy}

次の図は、スクリプトとダイアログのXMLの階層を示しています。 スクリプトXMLファイルは、script.xsdスキーマに準拠し、 window.xsdスキーマが（XMLの意味で）含まれます。 同様に、ダイアログXMLファイルはdialogs.xsdスキーマに準拠し、dialogs.xsdスキーマも含まれます。

![as_as_xml_hierarchy](assets/as_as_xml_hierarchy.png)

スクリプトおよびダイアログXMLの階層

#### スクリプトXMLファイル{#script-xml-files}

*スクリプトXMLファイル*&#x200B;は、ネイティブアプリケーションに特定のウィンドウ要素に移動し、それらの要素に応答を提供するよう指示する一連の手順を指定します。 ほとんどの応答は、対応するダイアログボックスのフィールド、コンボボックス、またはボタンにユーザーが入力する入力に対応するテキストまたはキーストロークです。

Generate PDFサービスでスクリプトXMLファイルをサポートする目的は、ネイティブアプリケーションにネイティブファイルの印刷を指示することです。 ただし、スクリプトXMLファイルを使用して、ネイティブアプリケーションのダイアログボックスとの対話時にユーザーが実行できるタスクを実行できます。

スクリプトXMLファイル内の手順は、分岐の機会を得ずに、順番に実行されます。 サポートされる唯一の条件付きテストは、タイムアウト/再試行用です。これにより、特定の期間内および特定の回数の再試行の後に手順が正常に完了しなかった場合にスクリプトが終了します。

順次的なステップに加えて、ステップ内の命令も順に実行されます。 手順と手順が、ユーザーが同じ手順を実行する順序を反映していることを確認する必要があります。

スクリプトXMLファイルの各ステップは、ステップの指示が正常に実行された場合に表示される予定のウィンドウ要素を識別します。 スクリプトステップの実行中に予期しないダイアログボックスが表示された場合は、次の節で説明するように、Generate PDFサービスはダイアログXMLファイルを検索します。

#### ダイアログXMLファイル{#dialog-xml-files}

ネイティブアプリケーションを実行すると、異なるダイアログボックスが表示されます。これは、ネイティブアプリケーションが表示モードか非表示モードかに関係なく表示されます。 ダイアログボックスは、オペレーティングシステムによって、またはアプリケーション自体によって生成できます。 ネイティブアプリケーションがGenerate PDFサービスの制御下で実行されている場合、システムおよびネイティブアプリケーションのダイアログボックスが非表示のウィンドウに表示されます。

*ダイアログXMLファイル*&#x200B;は、Generate PDFサービスがシステムまたはネイティブアプリケーションのダイアログボックスにどのように応答するかを指定します。 ダイアログXMLファイルを使用すると、Generate PDFサービスは、変換プロセスを容易にする方法で、プロンプトのないダイアログボックスに応答できます。

現在実行中のスクリプトXMLファイルで処理されないダイアログボックスがシステムまたはネイティブアプリケーションに表示された場合、Generate PDFサービスは、一致が見つかると停止し、次の順序でダイアログXMLファイルを検索します。

* アプリモン`[appname]`.追加の.`[locale]`.xml
* アプリモン`[appname]``[locale]`.xml （このファイルは変更しないでください。）
* appmon.global.`[locale]`.xml （このファイルは変更しないでください。）

Generate PDFサービスは、ダイアログボックスに一致するものを見つけた場合、ダイアログボックスに対して指定されたキーストロークまたはその他の操作を送信することで、ダイアログボックスを閉じます。 ダイアログボックスの指示で中止メッセージを指定した場合、Generate PDFサービスは現在実行中のジョブを終了し、エラーメッセージを生成します。 このような中止メッセージは、スクリプトXML文法の`abortMessage`要素で指定されます。

Generate PDFサービスで、前にリストされたファイルに記述されていないダイアログボックスが表示された場合、そのダイアログボックスのキャプションがログファイルエントリに組み込まれます。 現在実行中のジョブは、最終的にタイムアウトになります。 その後、ログファイルの情報を使用して、ネイティブアプリケーション用の追加のダイアログXMLファイルで新しい手順を作成できます。

### ネイティブファイル形式{#adding-or-modifying-support-for-a-native-file-format}のサポートを追加または変更する

この節では、他のネイティブファイル形式をサポートするため、または既にサポートされているネイティブファイル形式のサポートを変更するために実行する必要があるタスクについて説明します。

サポートを追加または変更する前に、次の作業を実行する必要があります。

#### ウィンドウ要素を識別するツールの選択{#choosing-a-tool-for-identifying-window-elements}

ダイアログおよびスクリプトXMLファイルでは、ダイアログまたはスクリプト要素が応答するウィンドウ要素（ダイアログボックス、フィールド、またはその他のダイアログコンポーネント）を指定する必要があります。 例えば、スクリプトがネイティブ・アプリケーション用のメニューを起動した後、スクリプトは、キー操作またはアクションを適用するメニューのウィンドウ要素を特定する必要があります。

ダイアログボックスは、タイトルバーに表示されるキャプションによって簡単に識別できます。 ただし、Microsoft Spy++などのツールを使用して、下位レベルのウィンドウ要素を特定する必要があります。 下位レベルのウィンドウ要素は、明らかではない様々な属性を使用して識別できます。 さらに、各ネイティブアプリケーションは、ウィンドウ要素を異なる方法で識別できます。 その結果、ウィンドウ要素を識別する方法は複数あります。 ウィンドウ要素の識別を考慮するための推奨順序を次に示します。

1. 一意の場合はキャプション自体
1. コントロールID（特定のダイアログボックスに対して一意である場合とそうでない場合があります）
1. 一意であるかどうかにかかわらず、クラス名

これら3つの属性のいずれかまたは組み合わせを使用して、ウィンドウを識別できます。

属性でキャプションを識別できない場合は、親に対するインデックスを使用して、ウィンドウ要素を識別できます。 *index*&#x200B;は、兄弟のウィンドウ要素を基準としたウィンドウ要素の位置を指定します。 多くの場合、コンボボックスを識別するには、インデックスしか使用できません。

次の問題に注意してください。

* Microsoft Spy++は、キャプションのホットキーを識別するためにアンパサンド(&amp;)を使用してキャプションを表示します。 例えば、Spy++は、1つの印刷ダイアログボックスのキャプションを`Pri&nt`と表示します。これは、ホットキーが&#x200B;*n*&#x200B;であることを示します。 スクリプトおよびダイアログXMLファイルのキャプションタイトルは、アンパサンドを省略する必要があります。
* 一部のキャプションには改行が含まれています。 Generate PDFサービスは改行を識別できません。 キャプションに改行が含まれている場合は、キャプションを他のメニュー項目と区別するのに十分な量含め、省略された部分に正規表現を使用します。 例えば、(`^Long caption title$`)などです。 （[キャプション属性での正規表現の使用](converting-file-formats-pdf.md#using-regular-expressions-in-caption-attributes)を参照）。
* 予約XML文字には文字エンティティ（エスケープシーケンスとも呼ばれます）を使用します。 例えば、アンパサンドには`&`、記号より小さいか大きい場合は`<`と`>`、アポストロフィには`&apos;`、引用符には`&quot;`を使用します。

ダイアログまたはスクリプトXMLファイルを使用する予定がある場合は、Microsoft Spy++アプリケーションをインストールする必要があります。

#### ダイアログとスクリプトファイルのパッケージ化を解除します。 {#unpackaging-the-dialog-and-script-files}

ダイアログファイルとスクリプトファイルは、 appmondata.jarファイルにあります。 これらのファイルのいずれかを変更したり、新しいスクリプトまたはダイアログファイルを追加したりする前に、このJARファイルのパッケージを解除する必要があります。 例えば、EditPlusアプリケーションのサポートを追加するとします。 appmon.editplus.script.en_US.xmlとappmon.editplus.script.addition.en_US.xmlという2つのXMLファイルを作成します。 次に示すように、これらのXMLスクリプトをadobe-appmondata.jarファイルの2つの場所に追加する必要があります。

* adobe-livecycle-native-jboss-x86_win32.ear > adobe-Native2PDFSvc.war\WEB-INF\lib > adobe-native.jar > Native2PDFSvc-native.jar\bin > adobe-appmondata.jar\com\adobe\appmon adobe-livecycle-native-jboss-x86_win32.earファイルは、`[AEM forms install directory]\configurationManager`にあるexportフォルダーにあります。 (AEM Formsが別のJ2EEアプリケーションサーバーにデプロイされている場合は、adobe-livecycle-native-jboss-x86_win32.earファイルを、ご使用のJ2EEアプリケーションサーバーに対応するEARファイルに置き換えます)。
* adobe-generatepdf-dsc.jar / adobe-appmondata.jar\com\adobe\appmon （adobe-appmondata.jarファイルはadobe-generatepdf-dsc.jarファイル内にあります）。 adobe-generatepdf-dsc.jarファイルは`[AEM forms install directory]\deploy`フォルダーにあります。

これらのXMLファイルをadobe-appmondata.jarファイルに追加した後、GeneratePDFコンポーネントを再デプロイする必要があります。 adobe-appmondata.jarファイルにダイアログおよびスクリプトXMLファイルを追加するには、次のタスクを実行します。

1. WinZipやWinRARなどのツールを使用して、adobe-livecycle-native-jboss-x86_win32.earfile / adobe-Native2PDFSvc.war\WEB-INF\lib / adobe-native.jar / Native2PDFSvc-native.jar\bin / adobe-appmondata.jarファイルを開きます。
1. ダイアログおよびスクリプトXMLファイルをappmondata.jarファイルに追加するか、このファイル内の既存のXMLファイルを変更します。 （[ネイティブアプリケーション用のスクリプトXMLファイルの作成または変更](converting-file-formats-pdf.md#creating-or-modifying-a-script-xml-file-for-a-native-application)および[ネイティブアプリケーション用の追加のダイアログXMLファイルの作成または変更](converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application)を参照）。
1. WinZipやWinRARなどのツールを使用して、 adobe-generatepdf-dsc.jar / adobe-appmondata.jarを開きます。
1. ダイアログおよびスクリプトXMLファイルをappmondata.jarファイルに追加するか、このファイル内の既存のXMLファイルを変更します。 （[ネイティブアプリケーション用のスクリプトXMLファイルの作成または変更](converting-file-formats-pdf.md#creating-or-modifying-a-script-xml-file-for-a-native-application)および[ネイティブアプリケーション用の追加のダイアログXMLファイルの作成または変更](converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application)を参照）。 XMLファイルをadobe-appmondata.jarファイルに追加した後、新しいadobe-appmondata.jarファイルをadobe-generatepdf-dsc.jarファイルに配置します。
1. 追加のネイティブファイル形式のサポートを追加した場合は、アプリケーションのパスを提供するシステム環境変数を作成します（[ネイティブアプリケーションを見つけるための環境変数の作成](converting-file-formats-pdf.md#creating-an-environment-variable-to-locate-the-native-application)を参照）。

**GeneratePDFコンポーネントを再デプロイするには**

1. Workbenchにログインします。
1. **Window** > **Show Views** > **Components**&#x200B;を選択します。 この操作により、コンポーネントビューがWorkbenchに追加されます。
1. GeneratePDFコンポーネントを右クリックし、「**コンポーネントを停止**」を選択します。
1. コンポーネントが停止したら、右クリックし、「コンポーネントのアンインストール」を選択して削除します。
1. **コンポーネント**&#x200B;アイコンを右クリックし、「**コンポーネントをインストール**」を選択します。
1. 変更されたadobe-generatepdf-dsc.jarファイルを参照して選択し、「開く」をクリックします。 GeneratePDFコンポーネントの横に赤い四角形が表示されます。
1. GeneratePDFコンポーネントを展開し、「サービス記述子」を選択し、「GeneratePDFService」を右クリックして「サービスをアクティブ化」を選択します。
1. 表示される設定ダイアログボックスで、適切な設定値を入力します。 これらの値を空白のままにすると、デフォルトの設定値が使用されます。
1. 「PDFを生成」を右クリックし、「コンポーネントを開始」を選択します。
1. [アクティブなサービス]を展開します。 サービス名が実行中の場合は、その横に緑色の矢印が表示されます。 それ以外の場合、サービスは停止状態になります。
1. サービスが停止状態の場合は、サービス名を右クリックし、「Start Service」を選択します。

### ネイティブアプリケーション{#creating-or-modifying-a-script-xml-file-for-a-native-application}のスクリプトXMLファイルの作成または変更

ファイルを新しいネイティブアプリケーションにダイレクトする場合は、そのアプリケーション用のスクリプトXMLファイルを作成する必要があります。 Generate PDFサービスと、既にサポートされているネイティブアプリケーションとのやり取りを変更する場合は、そのアプリケーションのスクリプトを変更する必要があります。

スクリプトには、ネイティブアプリケーションのウィンドウ要素間を移動し、それらの要素に対して特定の応答を提供する手順が含まれています。 この情報を格納するファイルは、`appmon.`[appname]&quot; `.script.`[locale]`.xml`です。 例えば、 appmon.notepad.script.en_US.xmlなどがあります。

#### スクリプトが実行する必要があるステップを識別します。{#identifying-steps-the-script-must-execute}

ネイティブアプリケーションを使用して、ナビゲートする必要があるウィンドウ要素と、ドキュメントを印刷するために実行する必要がある各応答を決定します。 任意の応答から生成されるダイアログボックスに注意してください。 手順は次の手順に似ています。

1. ファイル／開くを選択します。
1. パスを指定し、「開く」をクリックします。
1. メニューバーでファイル/印刷を選択します。
1. プリンタに必要なプロパティを指定します。
1. 「印刷」を選択し、名前を付けて保存ダイアログボックスが表示されるのを待ちます。 Generate PDFサービスでPDFファイルの保存先を指定するには、Save Asダイアログボックスが必要です。

#### キャプション属性{#identifying-the-dialogs-specified-in-caption-attributes}で指定されたダイアログの識別

Microsoft Spy++を使用して、ネイティブアプリケーションのウィンドウ要素プロパティのIDを取得します。 スクリプトを記述するには、これらのIDが必要です。

#### キャプション属性{#using-regular-expressions-in-caption-attributes}での正規表現の使用

キャプションの仕様では、正規表現を使用できます。 Generate PDFサービスは、`java.util.regex.Matcher`クラスを使用して正規表現をサポートします。 `java.util.regex.Pattern`で説明されている正規表現をサポートしています。 (JavaのWebサイト([https://java.sun.com/j2se/1.4.2/docs/api/java/util/regex/Pattern.html](https://java.sun.com/j2se/1.4.2/docs/api/java/util/regex/Pattern.html))にアクセスします。

**メモ帳のバナーでメモ帳の前に付加されるファイル名を格納する正規表現**

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

#### window要素とwindowList要素の順序{#ordering-the-window-and-windowlist-elements}

`window`要素と`windowList`要素の順序は次のようにする必要があります。

* 複数の`window`要素が`windowList`要素または`dialog`要素で子として表示される場合、`caption`名前の長さが順序内の位置を示す降順で、それらの`window`要素を並べ替えます。
* 複数の`windowList`要素が`window`要素に現れる場合、最初の`indexes/`要素の`caption`属性の長さで、順序の位置を示す`windowList`要素を降順に並べ替えます。

**ダイアログファイル内のウィンドウ要素の並べ替え**

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

**windowList要素内のウィンドウ要素の順序付け**

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

### ネイティブアプリケーション{#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application}用の追加のダイアログXMLファイルの作成または変更

以前サポートされていなかったネイティブアプリケーション用のスクリプトを作成する場合は、そのアプリケーション用の追加のダイアログXMLファイルも作成する必要があります。 AppMonが使用するすべてのネイティブアプリケーションには、ダイアログXMLファイルを1つだけ追加する必要があります。 追加のダイアログXMLファイルは、未承諾のダイアログボックスが必要な場合でも必要です。 追加のダイアログボックスには、その`window`要素がプレースホルダーにすぎない場合でも、少なくとも1つの`window`要素が必要です。

>[!NOTE]
>
>このコンテキストでは、「追加」とは、`appmon.[applicationname].addition.[locale]`.xml&#39;ファイルの内容を意味します。 このようなファイルは、ダイアログXMLファイルの上書きと追加を指定します。

次の目的で、ネイティブアプリケーション用の追加のダイアログXMLファイルを変更することもできます。

* 別の応答を持つアプリケーションのダイアログXMLファイルを上書きするには
* そのアプリケーションのダイアログXMLファイルで指定されていないダイアログボックスに応答を追加するには

追加のdialogXMLファイルを識別するファイル名は`appmon.[appname].addition.[locale].xml`です。 例えば、 appmon.excel.addition.en_US.xmlなどがあります。

追加のダイアログXMLファイルの名前は、`appmon.[applicationname].addition.[locale].xml`という形式を使用する必要があります。ここで、*applicationname*&#x200B;は、XML設定ファイルおよびスクリプトで使用されるアプリケーション名と完全に一致する必要があります。

>[!NOTE]
>
>native2pdfconfig.xml設定ファイルで指定された汎用アプリケーションに、プライマリダイアログXMLファイルがない。 [ネイティブファイル形式](converting-file-formats-pdf.md#adding-or-modifying-support-for-a-native-file-format)のサポートの追加や変更の節では、このような仕様について説明します。

`window`要素内に子として表示される`windowList`要素を並べ替える必要があります。 （[window要素とwindowList要素の並べ替え](converting-file-formats-pdf.md#ordering-the-window-and-windowlist-elements)を参照）。

### 一般ダイアログXMLファイル{#modifying-the-general-dialog-xml-file}の変更

一般的なダイアログXMLファイルを変更して、システムによって生成されたダイアログボックスに応答したり、複数のアプリケーションに共通するダイアログボックスに応答したりできます。

#### XML設定ファイル{#adding-a-filetype-entry-in-the-xml-configuration-file}にファイルタイプエントリを追加する

この手順では、Generate PDFサービス設定ファイルを更新して、ファイルタイプをネイティブアプリケーションに関連付ける方法を説明します。 この設定ファイルを更新するには、管理コンソールを使用して設定データをファイルに書き出す必要があります。 設定データのデフォルトのファイル名は、 native2pdfconfig.xmlです。

**Generate PDFサービス設定ファイルの更新**

1. **ホーム** / **サービス** / **Adobe PDF Generator** / **設定ファイル**&#x200B;を選択し、「**設定を書き出し**」を選択します。
1. 必要に応じて、native2pdfconfig.xmlファイルの`filetype-settings`要素を変更します。
1. **ホーム** / **サービス** / **Adobe PDF Generator** /**設定ファイル**&#x200B;を選択し、「**設定を読み込み**」を選択します。 設定データがGenerate PDFサービスに読み込まれ、以前の設定に置き換えられます。

>[!NOTE]
>
>アプリケーションの名前は、`GenericApp`要素の`name`属性の値として指定します。 この値は、そのアプリケーション用に開発するスクリプトで指定された対応する名前と完全に一致する必要があります。 同様に、`GenericApp`要素の`displayName`属性は、対応するスクリプトの`expectedWindow`ウィンドウキャプションと完全に一致する必要があります。 このような等価性は、`displayName`属性または`caption`属性に含まれる正規表現を解決した後に評価されます。

この例では、Generate PDFサービスで提供されるデフォルトの設定データが変更され、（Microsoft Wordではなく）メモ帳を使用して、ファイル名拡張子が.txtのファイルを処理するように指定されています。 この変更を行う前に、Microsoft Wordは、このようなファイルを処理するネイティブアプリケーションとして指定されていました。

**テキストファイルをメモ帳に転送するための変更(native2pdfconfig.xml)**

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

#### ネイティブアプリケーションを見つけるための環境変数{#creating-an-environment-variable-to-locate-the-native-application}の作成

ネイティブアプリケーション実行可能ファイルの場所を指定する環境変数を作成します。 変数は、`[applicationname]_PATH`という形式を使用する必要があります。ここで、*applicationname*&#x200B;は、XML設定ファイルおよびスクリプトで使用されるアプリケーション名と完全に一致する必要があり、パスには、実行可能ファイルのパスが二重引用符で囲まれます。 このような環境変数の例は`Photoshop_PATH`です。

新しい環境変数を作成した後、Generate PDFサービスがデプロイされているサーバーを再起動する必要があります。

**Windows XP環境でのシステム変数の作成**

1. **Campaign コントロールパネル/システム**&#x200B;を選択します。
1. [システムのプロパティ]ダイアログボックスで、[**詳細**]タブをクリックし、[**環境変数**]をクリックします。
1. [環境変数]ダイアログボックスの[システム変数]で、[**新規**]をクリックします。
1. [新しいシステム変数]ダイアログボックスの[**変数名**]ボックスに、`[applicationname]_PATH`という形式の名前を入力します。
1. 「**変数値**」ボックスに、アプリケーションの実行可能ファイルのフルパスとファイル名を入力し、「**OK**」をクリックします。 例えば、次のように入力します。`c:\windows\Notepad.exe`
1. [環境変数]ダイアログボックスで、[**OK**]をクリックします。

**コマンドラインからシステム変数を作成する**

1. コマンドラインウィンドウで、次の形式で変数定義を入力します。

   ```shell
            [applicationname]_PATH=[Full path name]
   ```

   例えば、次のように入力します。`NotePad_PATH=C:\WINDOWS\NOTEPAD.EXE`

1. システム変数を有効にするための新しいコマンドラインプロンプトを起動します。

#### XMLファイル{#xml-files}

AEM Formsには、Generate PDFサービスでメモ帳を使用してファイル名拡張子が.txtのファイルを処理するためのサンプルXMLファイルが含まれています。 このコードはこの節に含まれています。 さらに、この節で説明するその他の変更を行う必要があります。

#### 追加のダイアログXMLファイル{#additional-dialog-xml-file}

この例では、メモ帳アプリケーション用の追加のダイアログボックスが含まれています。 これらのダイアログボックスは、Generate PDFサービスで指定されたダイアログボックスに加えて使用できます。

**メモ帳ダイアログボックス(appmon.notepad.addition.en_US.xml)**

```xml
 <dialogs app="Notepad" locale="en_US" version="7.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="dialogs.xsd">
     <window caption="Caption Title">
         <windowList>
             <window className="Button" caption="OK" action="press"/>
         </windowList>
     </window>
 </dialogs>
```

#### スクリプトXMLファイル{#script-xml-file}

次の例では、Generate PDFサービスがメモ帳とやり取りし、Adobe PDFプリンターを使用してファイルを印刷する方法を指定します。

**メモ帳スクリプトXMLファイル(appmon.notepad.script.en_US.xml)**

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
