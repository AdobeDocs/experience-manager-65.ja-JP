---
title: ファイル形式とPDFの変換
seo-title: ファイル形式とPDFの変換
description: 'null'
seo-description: 'null'
uuid: f72ad603-c996-4d48-9bfc-bed7bf776af6
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 180cac3f-6378-42bc-9a47-60f9f08a7103
translation-type: tm+mt
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '7842'
ht-degree: 4%

---


# ファイル形式とPDF {#converting-between-file-formatsand-pdf}の変換

**Generate PDFサービスについて**

Generate PDF サービスは、ネイティブファイル形式を PDF に変換します。また、PDF を他のファイル形式に変換し、PDF ドキュメントのサイズを最適化します。

Generate PDF サービスは、以下のファイル形式を PDF に変換する際にネイティブアプリケーションを使用します。特に説明がない限り、これらのアプリケーションはドイツ語版、フランス語版、英語版および日本語版のみサポートされています。*Windows* は、Windows Server® 2003およびWindows Server 2008のみをサポートすることを示しています。

* Microsoft Office 2003および2007:DOC、DOCX、RTF、TXT、XLS、XLSX、PPT、PPTX、VSD、MPP、MPPX、XPS、PUBを変換（Windowsのみ）

>[!NOTE]
>
>Microsoft XPS形式をPDFに変換するには、Acrobat® 9.2以降が必要です。

* DWF、DWG、DXWを変換するAutodesk AutoCAD 2005、2006、2007、2008、2009（英語のみ）
* Corel WordPerfect 12およびX4によるWPD、QPW、SHWの変換（英語のみ）
* OpenOffice 2.0、2.4、3.0.1および3.1を使用して、ODT、ODS、ODP、ODG、ODF、SXW、SXI、SXD、DOC、DOCX、RTF、TXT、XLS、XLSX、PPT、pptx、VSD、MPP、MPPX、PUB

>[!NOTE]
>
>Generate PDFサービスは、64ビット版のOpenOfficeをサポートしていません。

* Adobe Photoshop® CS2からPSDへの変換（Windowsのみ）

>[!NOTE]
>
>PhotoshopCS3とCS4は、Windows Server 2003またはWindows Server 2008をサポートしていないため、サポートされていません。

* Adobe FrameMaker® 7.2および8でFMを変換（Windowsのみ）
* PMD、PM6、P65、PM の変換：Adobe PageMaker® 7.0（Windows のみ）
* サードパーティのアプリケーションによってサポートされているネイティブ形式（アプリケーションに固有のセットアップファイルの開発が必要）（Windows のみ）

Generate PDF サービスでは、次の標準ベースのファイル形式を PDF に変換します。

* ビデオファイル形式：SWF、FLV（Windows のみ）
* 画像ファイル形式：JPEG、JPG、JP2、J2Kí、JPC、J2C、GIF、BMP、TIFF、TIF、PNG、JPF
* HTML （Windows、Sun™ Solaris™、およびLinux®）

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
* AEM Formsをホストするコンピューターに、Adobe AcrobatプロフェッショナルまたはAcrobat Proエクステンデッド9.2をインストールする
* インストール後のセットアップタスクを実行する

これらのタスクは、『AEM formsの自動インストールおよびデプロイ（JBoss版）』に説明されています。

Generate PDFサービスを使用して、次のタスクを実行できます。

* ネイティブファイル形式からPDFに変換します。
* HTMLドキュメントをPDFドキュメントに変換します。
* PDFドキュメントをファイル形式に変換します。

>[!NOTE]
>
>Generate PDFサービスについて詳しくは、「[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)」を参照してください。

## WordドキュメントからPDFドキュメントへの変換{#converting-word-documents-to-pdf-documents}

この節では、Generate PDF APIを使用して、Microsoft WordドキュメントをPDFドキュメントにプログラム的に変換する方法について説明します。

>[!NOTE]
>
>その他のファイル形式について詳しくは、[追加のネイティブファイル形式に対するサポートの追加](converting-file-formats-pdf.md#adding-support-for-additional-native-file-formats)を参照してください。

>[!NOTE]
>
>Generate PDFサービスについて詳しくは、「[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)」を参照してください。

### 手順{#summary-of-steps}の概要

Microsoft WordドキュメントをPDFドキュメントに変換するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Generate PDFクライアントを作成します。
1. PDFドキュメントに変換するファイルを取得します。
1. ファイルをPDFドキュメントに変換します。
1. 結果を取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めてください。

**Generate PDFクライアントの作成**

プログラムを使用してGenerate PDF操作を実行する前に、Generate PDFサービスクライアントを作成します。 Java APIを使用している場合は、`GeneratePdfServiceClient`オブジェクトを作成します。 WebサービスAPIを使用している場合は、`GeneratePDFServiceService`オブジェクトを作成します。

**PDFドキュメントに変換するファイルを取得します**

Microsoft Wordドキュメントを取得してPDFドキュメントに変換します。

**ファイルをPDFドキュメントに変換**

Generate PDFサービスクライアントの作成後、`createPDF2`メソッドを呼び出すことができます。 このメソッドには、変換するドキュメント（ファイル拡張子など）に関する情報が必要です。

**結果を取得する**

ファイルがPDFドキュメントに変換された後、結果を取得できます。 例えば、WordファイルをPDFドキュメントに変換した後、PDFドキュメントを取得して保存できます。

**関連トピック**

[Java APIを使用したWordドキュメントのPDFドキュメントへの変換](converting-file-formats-pdf.md#convert-word-documents-to-pdf-documents-using-the-java-api)

[WebサービスAPIを使用してWordドキュメントをPDFドキュメントに変換する](converting-file-formats-pdf.md#convert-word-documents-to-pdf-documents-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Generate PDF Service APIのクイック開始](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### Java API {#convert-word-documents-to-pdf-documents-using-the-java-api}を使用してWordドキュメントをPDFドキュメントに変換する

Generate PDF API(Java)を使用してMicrosoft WordドキュメントをPDFドキュメントに変換します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-generatepdf-client.jarなどのクライアントJARファイルを含めます。

1. Generate PDFクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `GeneratePdfServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. PDFドキュメントに変換するファイルを取得します。

   * コンストラクタを使用して、変換するWordファイルを表す`java.io.FileInputStream`オブジェクトを作成します。 ファイルの場所を指定するstring値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. ファイルをPDFドキュメントに変換します。

   `GeneratePdfServiceClient`オブジェクトの`createPDF2`メソッドを呼び出し、次の値を渡して、ファイルをPDFドキュメントに変換します。

   * 変換するファイルを表す`com.adobe.idp.Document`オブジェクト。
   * ファイル拡張子を含む`java.lang.String`オブジェクト。
   * 変換に使用されるファイルタイプ設定が含まれる`java.lang.String`オブジェクト。 ファイルタイプの設定では、.docや.xlsなど、異なるファイルタイプの変換設定を指定します。
   * 使用するPDF設定の名前が含まれる`java.lang.String`オブジェクトです。 例えば、`Standard`を指定できます。
   * 使用するセキュリティ設定の名前を含む`java.lang.String`オブジェクト。
   * PDFドキュメントの生成中に適用される設定を含む、オプションの`com.adobe.idp.Document`オブジェクトです。
   * PDFドキュメントに適用するメタデータ情報を含む、オプションの`com.adobe.idp.Document`オブジェクトです。

   `createPDF2`メソッドは、新しいPDFドキュメントとログ情報を含む`CreatePDFResult`オブジェクトを返します。 通常、ログファイルには、変換要求によって生成されるエラーメッセージや警告メッセージが含まれます。

1. 結果を取得します。

   PDFドキュメントを取得するには、次の操作を実行します。

   * `CreatePDFResult`オブジェクトの`getCreatedDocument`メソッドを呼び出します。このメソッドは、`com.adobe.idp.Document`オブジェクトを返します。
   * `com.adobe.idp.Document`オブジェクトの`copyToFile`メソッドを呼び出して、前の手順で作成したオブジェクトからPDFドキュメントを抽出します。

   `createPDF2`メソッドを使用してログドキュメントを取得した場合（HTML変換には適用されません）、次の操作を実行します。

   * `CreatePDFResult`オブジェクトの`getLogDocument`メソッドを呼び出します。 `com.adobe.idp.Document`オブジェクトを返します。
   * `com.adobe.idp.Document`オブジェクトの`copyToFile`メソッドを呼び出して、ログドキュメントを抽出します。


**関連トピック**

[手順の概要](converting-file-formats-pdf.md#summary-of-steps)

[クイック開始（SOAPモード）:Java APIを使用したMicrosoft WordドキュメントのPDFドキュメントへの変換](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-a-microsoft-word-document-to-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#convert-word-documents-to-pdf-documents-using-the-web-service-api}を使用してWordドキュメントをPDFドキュメントに変換する

Generate PDF API（Webサービス）を使用して、Microsoft WordドキュメントをPDFドキュメントに変換します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. Generate PDFクライアントを作成します。

   * `GeneratePDFServiceClient`オブジェクトを作成するには、そのデフォルトのコンストラクタを使用します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`GeneratePDFServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに指定するstring値を渡します（例：`http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`）。 `lc_version`属性を使用する必要はありません。 ただし、`?blob=mtom`を指定します。
   * `GeneratePDFServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * AEM formsユーザー名をフィールド`GeneratePDFServiceClient.ClientCredentials.UserName.UserName`に割り当てます。
      * 対応するパスワード値をフィールド`GeneratePDFServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * 定数値`HttpClientCredentialType.Basic`をフィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に割り当てます。
      * 定数値`BasicHttpSecurityMode.TransportCredentialOnly`をフィールド`BasicHttpBindingSecurity.Security.Mode`に割り当てます。

1. PDFドキュメントに変換するファイルを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、PDFドキュメントに変換するファイルを保存するために使用します。
   * コンストラクターを呼び出して、`System.IO.FileStream`オブジェクトを作成します。 変換するファイルの場所とファイルを開くモードを表すstring値を渡します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得して、バイト配列のサイズを決定できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * `BLOB`オブジェクトを設定するには、`MTOM`プロパティにバイト配列の内容を割り当てます。

1. ファイルをPDFドキュメントに変換します。

   `GeneratePDFServiceService`オブジェクトの`CreatePDF2`メソッドを呼び出し、次の値を渡して、ファイルをPDFドキュメントに変換します。

   * 変換するファイルを表す`BLOB`オブジェクト。
   * ファイル拡張子を含む文字列です。
   * 変換に使用されるファイルタイプ設定が含まれる`java.lang.String`オブジェクト。 ファイルタイプの設定では、.docや.xlsなど、異なるファイルタイプの変換設定を指定します。
   * 使用するPDF設定を含むstringオブジェクトです。 `Standard`を指定できます。
   * 使用するセキュリティ設定を含むstringオブジェクトです。 `No Security`を指定できます。
   * PDFドキュメントの生成中に適用される設定を含む、オプションの`BLOB`オブジェクトです。
   * PDFドキュメントに適用するメタデータ情報を含む、オプションの`BLOB`オブジェクトです。
   * `CreatePDF2`メソッドによって入力される、タイプ`BLOB`の出力パラメーター。 `CreatePDF2`メソッドは、変換されたドキュメントをこのオブジェクトに入力します。 （このパラメーター値は、Webサービスの呼び出しの場合にのみ必要です）。
   * `CreatePDF2`メソッドによって入力される、タイプ`BLOB`の出力パラメーター。 `CreatePDF2`メソッドは、このオブジェクトにログドキュメントを入力します。 （このパラメーター値は、Webサービスの呼び出しの場合にのみ必要です）。

1. 結果を取得します。

   * `BLOB`オブジェクトの`MTOM`フィールドをバイト配列に割り当てて、変換されたPDFドキュメントを取得します。 byte配列は、変換されたPDFドキュメントを表します。 `createPDF2`メソッドの出力パラメーターとして使用する`BLOB`オブジェクトを使用してください。
   * コンストラクターを呼び出し、変換されたPDFドキュメントーのファイルの場所を表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * コンストラクターを呼び出して`System.IO.FileStream`オブジェクトを渡し、`System.IO.BinaryWriter`オブジェクトを作成します。
   * `System.IO.BinaryWriter`オブジェクトの`Write`メソッドを呼び出し、バイト配列を渡すことで、バイト配列の内容をPDFファイルに書き込みます。

**関連トピック**

[手順の概要](converting-file-formats-pdf.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## HTMLドキュメントからPDFドキュメントへの変換{#converting-html-documents-to-pdf-documents}

この節では、Generate PDF APIを使用して、HTMLドキュメントをPDFドキュメントにプログラム的に変換する方法について説明します。

>[!NOTE]
>
>Generate PDFサービスについて詳しくは、「[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)」を参照してください。

### 手順{#summary_of_steps-1}の概要

HTMLドキュメントをPDFドキュメントに変換するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Generate PDFクライアントを作成します。
1. PDFドキュメントに変換するHTMLコンテンツを取得します。
1. HTMLコンテンツをPDFドキュメントに変換します。
1. 結果を取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めてください。

**Generate PDFクライアントの作成**

プログラムを使用してGenerate PDF操作を実行する前に、Generate PDFサービスクライアントを作成する必要があります。 Java APIを使用している場合は、`GeneratePdfServiceClient`オブジェクトを作成します。 WebサービスAPIを使用している場合は、`GeneratePDFServiceService`を作成します。

**PDFドキュメントに変換するHTMLコンテンツを取得する**

PDFドキュメントに変換するHTMLコンテンツを参照します。 HTMLファイルなどのHTMLコンテンツや、URLを使用してアクセスできるHTMLコンテンツを参照できます。

**HTMLコンテンツのPDFドキュメントへの変換**

サービスクライアントを作成したら、適切なPDF作成操作を呼び出すことができます。 この操作には、ターゲットドキュメントへのパスなど、変換するドキュメントに関する情報が必要です。

**結果を取得する**

HTMLコンテンツがPDFドキュメントに変換されたら、結果を取得してPDFドキュメントを保存できます。

**関連トピック**

[Java APIを使用したHTMLコンテンツのPDFドキュメントへの変換](converting-file-formats-pdf.md#convert-html-content-to-a-pdf-document-using-the-java-api)

[WebサービスAPIを使用したHTMLコンテンツのPDFドキュメントへの変換](converting-file-formats-pdf.md#convert-html-content-to-a-pdf-document-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Generate PDF Service APIのクイック開始](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### Java API {#convert-html-content-to-a-pdf-document-using-the-java-api}を使用したHTMLコンテンツのPDFドキュメントへの変換

Generate PDF API(Java)を使用してHTMLドキュメントをPDFドキュメントに変換します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-generatepdf-client.jarなどのクライアントJARファイルを含めます。

1. Generate PDFクライアントを作成します。

   コンストラクターを使用し、接続プロパティを含む`ServiceClientFactory`オブジェクトを渡して、`GeneratePdfServiceClient`オブジェクトを作成します。

1. PDFドキュメントに変換するHTMLコンテンツを取得します。

   文字列変数を作成し、HTMLコンテンツを指すURLを割り当てることで、HTMLコンテンツを取得します。

1. HTMLコンテンツをPDFドキュメントに変換します。

   `GeneratePdfServiceClient`オブジェクトの`htmlToPDF2`メソッドを呼び出し、次の値を渡します。

   * 変換するHTMLファイルのURLを含む`java.lang.String`オブジェクト。
   * 変換に使用されるファイルタイプ設定が含まれる`java.lang.String`オブジェクト。 ファイルタイプ設定には、スパイダリングレベルを含めることができます。
   * 使用するセキュリティ設定の名前を含む`java.lang.String`オブジェクト。
   * PDFドキュメントの生成中に適用される設定を含む、オプションの`com.adobe.idp.Document`オブジェクトです。 この情報を指定しない場合、設定は前の3つのパラメーターに基づいて自動的に選択されます。
   * PDFドキュメントに適用するメタデータ情報を含む、オプションの`com.adobe.idp.Document`オブジェクトです。

1. 結果を取得します。

   `htmlToPDF2`メソッドは、生成された新しいPDFドキュメントを含む`HtmlToPdfResult`オブジェクトを返します。 新しく作成されたPDFドキュメントを取得するには、次の操作を実行します。

   * `HtmlToPdfResult`オブジェクトの`getCreatedDocument`メソッドを呼び出します。 `com.adobe.idp.Document`オブジェクトを返します。
   * `com.adobe.idp.Document`オブジェクトの`copyToFile`メソッドを呼び出して、前の手順で作成したオブジェクトからPDFドキュメントを抽出します。

**関連トピック**

[HTMLドキュメントのPDFドキュメントへの変換](converting-file-formats-pdf.md#converting-html-documents-to-pdf-documents)

[クイック開始（SOAPモード）:Java APIを使用したHTMLコンテンツのPDFドキュメントへの変換](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[クイック開始（SOAPモード）:Java APIを使用したHTMLコンテンツのPDFドキュメントへの変換](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#convert-html-content-to-a-pdf-document-using-the-web-service-api}を使用してHTMLコンテンツをPDFドキュメントに変換する

Generate PDF API（Webサービス）を使用してHTMLコンテンツをPDFドキュメントに変換します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. Generate PDFクライアントを作成します。

   * `GeneratePDFServiceClient`オブジェクトを作成するには、そのデフォルトのコンストラクタを使用します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`GeneratePDFServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに指定するstring値を渡します（例：`http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`）。 `lc_version`属性を使用する必要はありません。 ただし、`?blob=mtom`を指定します。
   * `GeneratePDFServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * AEM formsユーザー名をフィールド`GeneratePDFServiceClient.ClientCredentials.UserName.UserName`に割り当てます。
      * 対応するパスワード値をフィールド`GeneratePDFServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * 定数値`HttpClientCredentialType.Basic`をフィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に割り当てます。
      * 定数値`BasicHttpSecurityMode.TransportCredentialOnly`をフィールド`BasicHttpBindingSecurity.Security.Mode`に割り当てます。

1. PDFドキュメントに変換するHTMLコンテンツを取得します。

   文字列変数を作成し、HTMLコンテンツを指すURLを割り当てることで、HTMLコンテンツを取得します。

1. HTMLコンテンツをPDFドキュメントに変換します。

   `GeneratePDFServiceService`オブジェクトの`HtmlToPDF2`メソッドを呼び出し、次の値を渡して、HTMLコンテンツをPDFドキュメントに変換します。

   * 変換するHTMLコンテンツを含む文字列です。
   * 変換に使用されるファイルタイプ設定が含まれる`java.lang.String`オブジェクト。
   * 使用するセキュリティ設定を含むstringオブジェクトです。
   * PDFドキュメントの生成中に適用される設定を含む、オプションの`BLOB`オブジェクトです。
   * PDFドキュメントに適用するメタデータ情報を含む、オプションの`BLOB`オブジェクトです。
   * `CreatePDF2`メソッドによって入力される、タイプ`BLOB`の出力パラメーター。 `CreatePDF2`メソッドは、変換されたドキュメントをこのオブジェクトに入力します。 （このパラメーター値は、Webサービスの呼び出しの場合にのみ必要です）。

1. 結果を取得します。

   * `BLOB`オブジェクトの`MTOM`フィールドをバイト配列に割り当てて、変換されたPDFドキュメントを取得します。 byte配列は、変換されたPDFドキュメントを表します。 `HtmlToPDF2`メソッドの出力パラメーターとして使用する`BLOB`オブジェクトを使用してください。
   * コンストラクターを呼び出し、変換されたPDFドキュメントーのファイルの場所を表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * コンストラクターを呼び出して`System.IO.FileStream`オブジェクトを渡し、`System.IO.BinaryWriter`オブジェクトを作成します。
   * `System.IO.BinaryWriter`オブジェクトの`Write`メソッドを呼び出し、バイト配列を渡すことで、バイト配列の内容をPDFファイルに書き込みます。

**関連トピック**

[HTMLドキュメントのPDFドキュメントへの変換](converting-file-formats-pdf.md#converting-html-documents-to-pdf-documents)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## PDFドキュメントから非画像形式への変換{#converting-pdf-documents-to-non-image-formats}

この節では、Generate PDF Java APIとWebサービスAPIを使用して、PDFドキュメントをプログラムでRTFファイルに変換する方法について説明します。このファイルは画像以外の形式の例です。 その他の画像以外の形式には、HTML、テキスト、DOC、EPSがあります。 PDFドキュメントをRTFに変換する場合は、PDFドキュメントに送信ボタンなどのフォーム要素が含まれていないことを確認します。 フォーム要素は変換されません。

>[!NOTE]
>
>Generate PDFサービスについて詳しくは、「[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)」を参照してください。

### 手順{#summary_of_steps-2}の概要

PDFドキュメントをサポートされている任意の種類に変換するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Generate PDFクライアントを作成します。
1. 変換するPDFドキュメントを取得します。
1. PDFドキュメントを変換します。
1. 変換したファイルを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めてください。

**Generate PDFクライアントの作成**

プログラムを使用してGenerate PDF操作を実行する前に、Generate PDFサービスクライアントを作成する必要があります。 Java APIを使用している場合は、`GeneratePdfServiceClient`オブジェクトを作成します。 WebサービスAPIを使用している場合は、`GeneratePDFServiceService`オブジェクトを作成します。

**変換するPDFドキュメントを取得します**

画像以外の形式に変換するPDFドキュメントを取得します。

**「Convert the PDF」ドキュメント**

サービスクライアントを作成したら、PDF書き出し操作を呼び出すことができます。 この操作には、ターゲットドキュメントへのパスなど、変換するドキュメントに関する情報が必要です。

**変換したファイルを保存**

変換したファイルを保存します。 例えば、PDFドキュメントをRTFファイルに変換する場合は、変換後のドキュメントをRTFファイルに保存します。

**関連トピック**

[Java APIを使用したPDFドキュメントのRTFファイルへの変換](converting-file-formats-pdf.md#convert-a-pdf-document-to-a-rtf-file-using-the-java-api)

[WebサービスAPIを使用したPDFドキュメントのRTFファイルへの変換](converting-file-formats-pdf.md#convert-a-pdf-document-to-a-rtf-file-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Generate PDF Service APIのクイック開始](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### Java API {#convert-a-pdf-document-to-a-rtf-file-using-the-java-api}を使用してPDFドキュメントをRTFファイルに変換します。

Generate PDF API(Java)を使用してPDFドキュメントをRTFファイルに変換します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-generatepdf-client.jarなどのクライアントJARファイルを含めます。

1. Generate PDFクライアントを作成します。

   コンストラクターを使用し、接続プロパティを含む`ServiceClientFactory`オブジェクトを渡して、`GeneratePdfServiceClient`オブジェクトを作成します。

1. 変換するPDFドキュメントを取得します。

   * コンストラクターを使用して、変換するPDFドキュメントを表す`java.io.FileInputStream`オブジェクトを作成します。 PDFドキュメントの場所を指定するstring値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PDFドキュメントを変換します。

   `GeneratePdfServiceClient`オブジェクトの`exportPDF2`メソッドを呼び出し、次の値を渡します。

   * 変換するPDFファイルを表す`com.adobe.idp.Document`オブジェクトです。
   * 変換するファイルの名前を含む`java.lang.String`オブジェクト。
   * Adobe PDF設定の名前を含む`java.lang.String`オブジェクト。
   * 変換のターゲットファイルの種類を指定する`ConvertPDFFormatType`オブジェクト。
   * PDFドキュメントの生成中に適用される設定を含む、オプションの`com.adobe.idp.Document`オブジェクトです。

   `exportPDF2`メソッドは、変換されたファイルを含む`ExportPDFResult`オブジェクトを返します。

1. PDFドキュメントを変換します。

   新しく作成したファイルを取得するには、次の操作を実行します。

   * `ExportPDFResult`オブジェクトの`getConvertedDocument`メソッドを呼び出します。 `com.adobe.idp.Document`オブジェクトを返します。
   * `com.adobe.idp.Document`オブジェクトの`copyToFile`メソッドを呼び出して、新しいドキュメントを抽出します。

**関連トピック**

[手順の概要](converting-file-formats-pdf.md#summary-of-steps)

[クイック開始（SOAPモード）:Java APIを使用したHTMLコンテンツのPDFドキュメントへの変換](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#convert-a-pdf-document-to-a-rtf-file-using-the-web-service-api}を使用してPDFドキュメントをRTFファイルに変換します。

Generate PDF API（Webサービス）を使用してPDFドキュメントをRTFファイルに変換します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. Generate PDFクライアントを作成します。

   * `GeneratePDFServiceClient`オブジェクトを作成するには、そのデフォルトのコンストラクタを使用します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`GeneratePDFServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに指定するstring値を渡します（例：`http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`）。 `lc_version`属性を使用する必要はありません。 ただし、`?blob=mtom`を指定します。
   * `GeneratePDFServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * AEM formsユーザー名をフィールド`GeneratePDFServiceClient.ClientCredentials.UserName.UserName`に割り当てます。
      * 対応するパスワード値をフィールド`GeneratePDFServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * 定数値`HttpClientCredentialType.Basic`をフィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に割り当てます。
      * 定数値`BasicHttpSecurityMode.TransportCredentialOnly`をフィールド`BasicHttpBindingSecurity.Security.Mode`に割り当てます。

1. 変換するPDFドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、変換されたPDFドキュメントの保存に使用されます。
   * コンストラクターを呼び出し、PDFドキュメントーのファイルの場所とファイルを開くモードを表す文字列値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得して、バイト配列のサイズを決定できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * `BLOB`オブジェクトを設定するには、`MTOM`プロパティにバイト配列の内容を割り当てます。

1. PDFドキュメントを変換します。

   `GeneratePDFServiceServiceWse`オブジェクトの`ExportPDF2`メソッドを呼び出し、次の値を渡します。

   * 変換するPDFファイルを表す`BLOB`オブジェクトです。
   * 変換するファイルのパス名を含む文字列です。
   * ファイルの場所を指定する`java.lang.String`オブジェクト。
   * 変換のターゲットファイルの種類を指定するstringオブジェクト。 `RTF`を指定します。
   * PDFドキュメントの生成中に適用される設定を含む、オプションの`BLOB`オブジェクトです。
   * `ExportPDF2`メソッドによって入力される、タイプ`BLOB`の出力パラメーター。 `ExportPDF2`メソッドは、変換されたドキュメントをこのオブジェクトに入力します。 （このパラメーター値は、Webサービスの呼び出しの場合にのみ必要です）。

1. 変換したファイルを保存します。

   * `BLOB`オブジェクトの`MTOM`フィールドをバイト配列に割り当てて、変換されたRTFドキュメントを取得します。 バイト配列は、変換されたRTFドキュメントを表します。 `ExportPDF2`メソッドの出力パラメーターとして使用する`BLOB`オブジェクトを使用してください。
   * コンストラクターを呼び出して、`System.IO.FileStream`オブジェクトを作成します。 RTFファイルの場所を表すstring値を渡します。
   * コンストラクターを呼び出して`System.IO.FileStream`オブジェクトを渡し、`System.IO.BinaryWriter`オブジェクトを作成します。
   * `System.IO.BinaryWriter`オブジェクトの`Write`メソッドを呼び出し、バイト配列を渡すことで、バイト配列の内容をRTFファイルに書き込みます。

**関連トピック**

[手順の概要](converting-file-formats-pdf.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 追加のネイティブファイル形式のサポートの追加{#adding-support-for-additional-native-file-formats}

この節では、その他のネイティブファイル形式に対するサポートを追加する方法について説明します。 このサービスでは、Generate PDFサービスと、このサービスでネイティブファイル形式をPDFに変換する際に使用されるネイティブアプリケーションとの間のやり取りの概要を提供します。

この節では、以下についても説明します。

* Generate PDFサービスが、この製品でネイティブファイル形式のPDFへの変換に既に使用されているネイティブアプリケーションに対して提供する応答を変更する方法
* Generate PDFサービス、Generate PDFサービスのApplication Monitor(AppMon)コンポーネント、およびMicrosoft Wordなどのネイティブアプリケーション間でのやり取り
* XMLグラマーがこれらのインタラクションで果たす役割

### コンポーネントの操作{#component-interactions}

Generate PDFサービスは、ファイル形式に関連付けられたアプリケーションを呼び出してネイティブファイル形式を変換し、アプリケーションとやり取りして、デフォルトのプリンターを使用してドキュメントを印刷します。 デフォルトのプリンターは、Adobe PDFプリンターとして設定する必要があります。

次の図に、ネイティブアプリケーションのサポートに関連するコンポーネントとドライバを示します。 また、インタラクションに影響を与えるXMLグラマーについても説明します。

ネイティブファイル変換のコンポーネントの操作

このドキュメントでは、「*ネイティブアプリケーション*」という用語を使用して、Microsoft Wordなどのネイティブファイル形式の生成に使用するアプリケーションを示します。

*AppMonisは、ユーザーがそのアプリケーションによって表示されるダイアログボックス内を移動するのと同じ方法で、ネイティブアプリケーションと対話するエンタープライズコンポーネントです。* AppMonで、Microsoft Wordなどのアプリケーションに対して、ファイルを開いて印刷するよう指示するために使用されるXMLグラマーでは、次の順次タスクが含まれます。

1. ファイル/開くを選択してファイルを開く
1. [開く]ダイアログボックスが表示されていることを確認します。そうでない場合は、エラーを処理します
1. 「ファイル名」フィールドにファイル名を入力し、「開く」ボタンをクリックする
1. ファイルが実際に開かれていることの確認
1. ファイル/印刷を選択して、印刷ダイアログボックスを開く
1. 印刷ダイアログボックスが表示されることを確認する

AppMonは、標準のWin32 APIを使用して、キーストロークやマウスクリックなどのUIイベントを転送するために、サードパーティアプリケーションとやり取りします。これは、これらのアプリケーションを制御してPDFファイルを生成するのに役立ちます。

これらのWin32 APIの制限により、AppMonは、フローティングメニューバー（TextPadなどのアプリケーションで見つかる）や、Win32 APIを使用してコンテンツを取得できない特定の種類のダイアログなど、特定の種類のウィンドウにこれらのUIイベントをディスパッチできません。

フローティングメニューバーを見分けるのは簡単です。ただし、特別な種類のダイアログは、視覚検査だけでは特定できない場合があります。 AppMonが標準のWin32 APIを使用してAppMonとやり取りできるかどうかを調べるためのダイアログを調べるには、Microsoft Spy++ (Microsoft Visual C++開発環境の一部)やそれに相当するWinID ([https://www.dennisbabkin.com/php/download.php?what=WinID](https://www.dennisbabkin.com/php/download.php?what=WinID)から無料でダウンロードできます)などのサードパーティ製品が必要です。

WinIDがテキスト、サブウィンドウ、ウィンドウクラスIDなどのダイアログコンテンツを抽出できる場合、AppMonも同様に機能します。

次の表に、ネイティブファイル形式で印刷する際に使用する情報の種類を示します。

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
   <td><p>PDF設定、セキュリティ設定、ファイルタイプ設定などが含まれます。 </p><p>ファイルタイプ設定により、ファイル名拡張子が対応するネイティブアプリケーションに関連付けられます。 ファイルタイプ設定では、ネイティブファイルの印刷に使用するネイティブアプリケーション設定も指定します。 </p></td>
   <td><p>既にサポートされているネイティブアプリケーションの設定を変更するには、システム管理者が管理コンソールで「ファイルタイプ設定」を設定します。 </p><p>新しいネイティブファイル形式のサポートを追加するには、ファイルを手動で編集する必要があります。 （<a href="converting-file-formats-pdf.md#adding-or-modifying-support-for-a-native-file-format">ネイティブファイル形式のサポートの追加または変更</a>を参照）。 </p></td>
  </tr>
  <tr>
   <td><p>スクリプト </p></td>
   <td><p>Generate PDFサービスとネイティブアプリケーションとの間のやり取りを指定します。 このような操作を行うと、通常、アプリケーションはAdobe PDFドライバにファイルを印刷するよう指示します。 </p><p>このスクリプトには、ネイティブアプリケーションに特定のダイアログボックスを開かせ、それらのダイアログボックスのフィールドとボタンに対して特定の応答を提供する命令が含まれています。 </p></td>
   <td><p>Generate PDFサービスには、サポートされるすべてのネイティブアプリケーション用のスクリプトファイルが含まれます。 これらのファイルは、XML編集アプリケーションを使用して変更できます。</p><p>新しいネイティブアプリケーションのサポートを追加するには、新しいスクリプトファイルを作成する必要があります。 （<a href="converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application">ネイティブアプリケーション用の追加のダイアログXMLファイルの作成または変更</a>を参照）。 </p></td>
  </tr>
  <tr>
   <td><p>一般的なダイアログボックスの説明 </p></td>
   <td><p>複数のアプリケーションに共通のダイアログボックスに対する対応方法を指定します。 このようなダイアログボックスは、オペレーティングシステム、ヘルパーアプリケーション（PDFMakerなど）、およびドライバーによって生成されます。 </p><p>この情報を含むファイルは、appmon.global.en_US.xmlです。</p></td>
   <td><p>このファイルは変更しないでください。 </p></td>
  </tr>
  <tr>
   <td><p>アプリケーション固有のダイアログボックスの説明</p></td>
   <td><p>アプリケーション固有のダイアログボックスに対する応答方法を指定します。 </p><p>この情報を含むファイルはappmonです。<i>`[appname]`</i>.dialog.<i>`[ロケール]`</i>.xml （appmon.word.en_US.xmlなど）</p></td>
   <td><p>このファイルは変更しないでください。 </p><p>新しいネイティブアプリケーション用のダイアログボックスの手順を追加するには、<a href="converting-file-formats-pdf.md#creating_or_modifying_an_additional_dialog_xml_file_for_a_native_application">ネイティブアプリケーション用の追加のダイアログXMLファイルの作成または変更</a>を参照してください。</p></td>
  </tr>
  <tr>
   <td><p>その他のアプリケーション固有のダイアログボックスの手順 </p></td>
   <td><p>アプリケーション固有のダイアログボックスの説明に対する上書きと追加を指定します。 この節では、このような情報の例を示します。 </p><p>この情報を含むファイルはappmonです。<i>`[appname]`</i>.addition.<i>`[ロケール]`</i>.xml.appmon.addition.en_US.xmlなどがあります。</p></td>
   <td><p>この種類のファイルは、XML編集アプリケーションを使用して作成および変更できます。 （<a href="converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application">ネイティブアプリケーション用の追加のダイアログXMLファイルの作成または変更</a>を参照）。 </p><p><strong>重要</strong>:サーバーがサポートするネイティブアプリケーションごとに、アプリケーション固有のダイアログボックスに関する追加の手順を作成する必要があります。 </p></td>
  </tr>
 </tbody>
</table>

### スクリプトおよびダイアログXMLファイルについて{#about-the-script-and-dialog-xml-files}

スクリプトXMLファイルは、ユーザーがアプリケーションのダイアログボックスを移動するのと同じように、Generate PDFサービスにアプリケーションのダイアログボックス間を移動するよう指示します。 また、スクリプトXMLファイルは、ボタンの押し下げ、チェックボックスの選択/選択解除、メニュー項目の選択などの操作を実行して、Generate PDFサービスにダイアログボックスへの応答を指示します。

対照的に、ダイアログXMLファイルは、スクリプトXMLファイルで使用されるのと同じタイプのアクションを持つダイアログボックスに応答します。

#### ダイアログボックスとウィンドウ要素の用語{#dialog-box-and-window-element-terminology}

この節と次の節では、説明するパースペクティブに応じて、ダイアログボックスやダイアログボックスに含まれるコンポーネントに対して異なる用語を使用します。 ダイアログボックスのコンポーネントは、ボタン、フィールド、コンボボックスなどの項目です。

この節と次の節では、ユーザーの観点からダイアログボックスとその構成要素について説明する際に、*ダイアログボックス*、*ボタン*、*フィールド*、*コンボボックス*&#x200B;などの用語が使用されます。

この節と次の節では、内部表現の観点から、ダイアログボックスとそのコンポーネントについて説明する場合、*window要素*&#x200B;という用語が使用されます。 ウィンドウ要素の内部表現は階層で、各ウィンドウ要素のインスタンスはラベルで識別されます。 ウィンドウ要素インスタンスは、その物理的な特性と動作も記述します。

ユーザーの観点から見ると、ダイアログボックスとそのコンポーネントには異なる動作が表示されます。この場合、一部のダイアログボックス要素はアクティブ化されるまで非表示になります。 内部表現の観点からは、そのような行動の問題は存在しません。 例えば、ダイアログボックスの内部表現は、ダイアログボックス内でコンポーネントがネストされる点を除いて、ダイアログボックスの内部表現とそのコンポーネントの内部表現は似ています。

ここでは、AppMonに手順を提供するXML要素について説明します。 これらの要素には、`dialog`要素や`window`要素などの名前が付けられます。 このドキュメントでは、XML要素を区別するために等幅フォントを使用します。 `dialog`要素は、XMLスクリプトファイルが意図的にまたは意図せずに表示される原因となる可能性のあるダイアログボックスを識別します。 `window`要素は、ウィンドウ要素（ダイアログボックスまたはダイアログボックスのコンポーネント）を識別します。

#### 階層 {#hierarchy}

次の図に、スクリプトとダイアログのXMLの階層を示します。 スクリプトXMLファイルは、script.xsdスキーマに準拠しています。このには、（XMLの意味で）window.xsdスキーマが含まれます。 同様に、ダイアログXMLファイルはdialogs.xsdスキーマに準拠しています。この中にはwindow.xsdスキーマも含まれています。

![as_as_xml_hierarchy](assets/as_as_xml_hierarchy.png)

スクリプトとダイアログのXMLの階層

#### スクリプトXMLファイル{#script-xml-files}

*スクリプトXMLファイル*&#x200B;は、ネイティブアプリケーションに特定のウィンドウ要素に移動させ、それらの要素に応答を提供する一連の手順を指定します。 ほとんどの応答は、対応するダイアログボックスのフィールド、コンボボックス、またはボタンに対してユーザーが入力するテキストまたはキーストロークです。

Generate PDFサービスでスクリプトXMLファイルがサポートされる目的は、ネイティブアプリケーションにネイティブファイルを印刷させることです。 ただし、スクリプトXMLファイルは、ネイティブアプリケーションのダイアログボックスを操作する際にユーザーが実行できるあらゆるタスクを実行するために使用できます。

スクリプトXMLファイル内の手順は、分岐の必要がなく順番に実行されます。 サポートされる唯一の条件付きテストは、タイムアウト/再試行に対するテストです。これにより、特定の再試行内および特定の数の期間が経過した後にステップが正常に完了しなかった場合に、スクリプトが終了します。

順次的なステップに加えて、ステップ内の命令も順に実行される。 手順と手順が、ユーザーが同じ手順を実行する順序を反映していることを確認する必要があります。

スクリプトXMLファイル内の各手順は、手順が正常に実行された場合に表示される予定のウィンドウ要素を識別します。 スクリプトの手順の実行中に予期しないダイアログボックスが表示された場合は、次の節の説明に従って、Generate PDFサービスでダイアログXMLファイルを検索します。

#### ダイアログXMLファイル{#dialog-xml-files}

ネイティブアプリケーションを実行すると、表示モードと非表示モードのどちらに関係なく、異なるダイアログボックスが表示されます。 ダイアログボックスは、オペレーティングシステムまたはアプリケーション自体で生成できます。 ネイティブアプリケーションがGenerate PDFサービスの制御下で実行されている場合、システムおよびネイティブアプリケーションのダイアログボックスが非表示ウィンドウに表示されます。

*ダイアログXMLファイル*&#x200B;は、Generate PDFサービスがシステムまたはネイティブアプリケーションのダイアログボックスに対してどのように応答するかを指定します。 ダイアログXMLファイルを使用すると、Generate PDFサービスは、変換プロセスを容易にする方法で、指示に従わないダイアログボックスに応答できます。

現在実行中のスクリプトXMLファイルで処理されないダイアログボックスがシステムまたはネイティブアプリケーションに表示された場合、Generate PDFサービスは、次の順序でダイアログXMLファイルを検索し、一致が見つかった場合は停止します。

* appmon`[appname]`.追加の.`[locale]`.xml
* appmon`[appname]``[locale]`.xml （このファイルは変更しないでください。）
* appmon.global.`[locale]`.xml （このファイルは変更しないでください。）

Generate PDFサービスは、ダイアログボックスに一致するものを見つけた場合、ダイアログボックスに対して指定されたキーストロークまたは他の操作を送信して、ダイアログボックスを閉じます。 ダイアログボックスの手順で中止メッセージを指定した場合、Generate PDFサービスは、現在実行中のジョブを終了し、エラーメッセージを生成します。 このような中止メッセージは、スクリプトXML文法の`abortMessage`要素で指定されます。

Generate PDFサービスで、前述のファイルのいずれにも記述されていないダイアログボックスが検出された場合、Generate PDFサービスは、このダイアログボックスのキャプションをログファイルエントリに組み込みます。 現在実行中のジョブは、最終的にタイムアウトになります。 その後、ログファイル内の情報を使用して、ネイティブアプリケーション用の追加のダイアログXMLファイル内の新しい手順を作成できます。

### ネイティブファイル形式{#adding-or-modifying-support-for-a-native-file-format}のサポートを追加または変更する

この節では、他のネイティブファイル形式をサポートするため、または既にサポートされているネイティブファイル形式のサポートを変更するために実行する必要があるタスクについて説明します。

サポートを追加または変更する前に、次のタスクを実行する必要があります。

#### ウィンドウ要素を識別するツールの選択{#choosing-a-tool-for-identifying-window-elements}

ダイアログおよびスクリプトのXMLファイルでは、ダイアログまたはスクリプト要素が応答するウィンドウ要素（ダイアログボックス、フィールド、または他のダイアログコンポーネント）を指定する必要があります。 例えば、スクリプトがネイティブ・アプリケーションのメニューを呼び出した後、スクリプトはキー操作またはアクションを適用するメニューのウィンドウ要素を識別する必要があります。

ダイアログボックスは、タイトルバーに表示されるキャプションで簡単に識別できます。 ただし、Microsoft Spy++などのツールを使用して、下位レベルのウィンドウ要素を識別する必要があります。 下位レベルのウィンドウ要素は、明らかでない様々な属性を使用して識別できます。 また、各ネイティブアプリケーションは、ウィンドウ要素を異なる方法で識別できます。 その結果、ウィンドウ要素を識別する複数の方法があります。 ウィンドウ要素の識別を考慮するための推奨順序を次に示します。

1. 一意の場合のキャプション自体
1. コントロールID（特定のダイアログボックスに対して一意である場合とそうでない場合があります）
1. クラス名。一意のクラス名の場合とそうでない場合があります。

これら3つの属性のいずれかまたは組み合わせを使用して、ウィンドウを識別できます。

属性がキャプションを識別できない場合、親に対するインデックスを使用してウィンドウ要素を識別できます。 *index*&#x200B;は、兄弟のwindow要素を基準にした、window要素の位置を指定します。 多くの場合、コンボボックスを識別する唯一の方法はインデックスです。

次の問題に注意してください。

* Microsoft Spy++では、キャプションにアンパサンド(&amp;)を使用してキャプションのホットキーを識別して表示します。 例えば、Spy++では、1つの印刷ダイアログボックスのキャプションが`Pri&nt`と表示されます。これは、ホットキーが&#x200B;*n*&#x200B;であることを示します。 スクリプトおよびダイアログXMLファイルのキャプションタイトルでは、アンパサンドを省略する必要があります。
* 一部のキャプションには改行が含まれます。 Generate PDFサービスは改行を識別できません。 キャプションに改行が含まれる場合は、キャプションを他のメニュー項目と区別するのに十分な量含め、省略された部分には正規式を使用します。 例えば、(`^Long caption title$`)のように指定します。 ([キャプション属性での正規式の使用](converting-file-formats-pdf.md#using-regular-expressions-in-caption-attributes)を参照)。
* 予約済みのXML文字には、文字エンティティ（エスケープシーケンスとも呼ばれます）を使用します。 例えば、アンパサンドには`&`、次の値より小さい記号および次の値には`<`および`>`を、アポストロフィには`&apos;`を、引用符には`&quot;`を使用します。

ダイアログまたはスクリプトXMLファイルを操作する場合は、Microsoft Spy++アプリケーションをインストールする必要があります。

#### ダイアログとスクリプトファイルのパッケージ化を解除{#unpackaging-the-dialog-and-script-files}

ダイアログファイルとスクリプトファイルは、appmondata.jarファイルに存在します。 これらのファイルのいずれかを変更したり、新しいスクリプトやダイアログファイルを追加したりする前に、このJARファイルを展開する必要があります。 例えば、EditPlusアプリケーションのサポートを追加するとします。 appmon.editplus.script.en_US.xmlという名前の2つのXMLファイルとappmon.editplus.script.addition.en_US.xmlを作成します。 これらのXMLスクリプトは、次に示すように、adobe-appmondata.jarファイルの2か所に追加する必要があります。

* adobe-livecycle-native-jboss-x86_win32.ear > adobe-Native2PDFSvc.war\WEB-INF\lib > adobe-native.jar > Native2PDFSvc-native.jar\bin > adobe-appmondata.jar\com\adobe\appmon。 adobe-livecycle-native-jboss-x86_win32.earファイルは、`[AEM forms install directory]\configurationManager`のexportフォルダーにあります。 (AEM Formsを別のJ2EEアプリケーションサーバーにデプロイする場合は、adobe-livecycle-native-jboss-x86_win32.earファイルを、ご使用のJ2EEアプリケーションサーバーに対応するEARファイルに置き換えます)。
* adobe-generatepdf-dsc.jar/adobe-appmondata.jar\com\adobe\appmon （adobe-appmondata.jarファイルはadobe-generatepdf-dsc.jarファイル内にあります）。 adobe-generatepdf-dsc.jarファイルは`[AEM forms install directory]\deploy`フォルダーにあります。

これらのXMLファイルをadobe-appmondata.jarファイルに追加した後、GeneratePDFコンポーネントを再デプロイする必要があります。 adobe-appmondata.jarファイルにダイアログおよびスクリプトXMLファイルを追加するには、次のタスクを実行します。

1. WinZipやWinRARなどのツールを使用して、adobe-livecycle-native-jboss-x86_win32.earfile > adobe-Native2PDFSvc.war\WEB-INF\lib > adobe-native.jar > Native2PDFSvc-native.jar\bin > adobe-appmondata.jarファイルを開きます。
1. ダイアログ追加とスクリプトXMLファイルをappmondata.jarファイルに追加するか、このファイル内の既存のXMLファイルを変更します。 （「[ネイティブアプリケーション用のスクリプトXMLファイルの作成または変更](converting-file-formats-pdf.md#creating-or-modifying-a-script-xml-file-for-a-native-application)」および「[ネイティブアプリケーション用の追加のダイアログXMLファイルの作成または変更](converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application)」を参照）。
1. WinZipやWinRARなどのツールを使用して、adobe-generatepdf-dsc.jar/adobe-appmondata.jarを開きます。
1. ダイアログ追加とスクリプトXMLファイルをappmondata.jarファイルに追加するか、このファイル内の既存のXMLファイルを変更します。 （「[ネイティブアプリケーション用のスクリプトXMLファイルの作成または変更](converting-file-formats-pdf.md#creating-or-modifying-a-script-xml-file-for-a-native-application)」および「[ネイティブアプリケーション用の追加のダイアログXMLファイルの作成または変更](converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application)」を参照）。 XMLファイルをadobe-appmondata.jarファイルに追加した後、新しいadobe-appmondata.jarファイルをadobe-generatepdf-dsc.jarファイルに配置します。
1. 追加のネイティブファイル形式のサポートを追加した場合は、アプリケーションのパスを提供するシステム環境変数を作成します(「[ネイティブ環境を検索するためのアプリケーション変数の作成](converting-file-formats-pdf.md#creating-an-environment-variable-to-locate-the-native-application)」を参照)。

**GeneratePDFコンポーネントを再デプロイするには**

1. Workbenchにログインします。
1. **ウィンドウ**/**表示を表示**/**コンポーネント**&#x200B;を選択します。 この操作により、WorkbenchにComponents表示ーが追加されます。
1. GeneratePDFコンポーネントを右クリックし、「**Stop Component**」を選択します。
1. コンポーネントが停止したら、右クリックし、「Uninstall Component」を選択して削除します。
1. 「**コンポーネント**」アイコンを右クリックし、「**コンポーネントをインストール**」を選択します。
1. 変更されたadobe-generatepdf-dsc.jarファイルを参照して選択し、「開く」をクリックします。 GeneratePDFコンポーネントの横に赤い四角形が表示されます。
1. GeneratePDFコンポーネントを展開し、「Service Descriptors」を選択して、「GeneratePDFService」を右クリックし、「Activate Service」を選択します。
1. 表示される設定ダイアログボックスで、適切な設定値を入力します。 これらの値を空白のままにすると、デフォルトの設定値が使用されます。
1. 「GeneratePDF」を右クリックし、「開始コンポーネント」を選択します。
1. 「Active Services」を展開します。 サービス名が実行されている場合は、その横に緑色の矢印が表示されます。 それ以外の場合は、サービスは停止状態です。
1. サービスが停止状態の場合は、サービス名を右クリックし、「開始サービス」を選択します。

### ネイティブアプリケーション{#creating-or-modifying-a-script-xml-file-for-a-native-application}のスクリプトXMLファイルの作成または変更

ファイルを新しいネイティブアプリケーションに転送する場合は、そのアプリケーションのスクリプトXMLファイルを作成する必要があります。 既にサポートされているネイティブアプリケーションとGenerate PDFサービスがやり取りする方法を変更する場合は、そのアプリケーションのスクリプトを変更する必要があります。

スクリプトには、ネイティブアプリケーションのウィンドウ要素間を移動し、それらの要素に対して特定の応答を提供する手順が含まれています。 この情報を含むファイルは、`appmon.`[appname]&quot;`.script.`[locale]`.xml`です。 appmon.notepad.script.en_US.xmlなどがあります。

#### スクリプトが{#identifying-steps-the-script-must-execute}を実行する必要があるステップを識別します

ネイティブのドキュメントを使用して、ナビゲートする必要のあるウィンドウ要素と、アプリを印刷するために実行する必要のある各応答を決定します。 任意の応答から生成されるダイアログボックスに注目してください。 手順は次の手順と似ています。

1. ファイル／開くを選択します。
1. パスを指定し、「開く」をクリックします。
1. メニューバーでファイル/印刷を選択します。
1. プリンターに必要なプロパティを指定します。
1. 「印刷」を選択し、名前を付けて保存ダイアログボックスが表示されるまで待ちます。 Generate PDFサービスでPDFファイルの保存先を指定するには、Save Asダイアログボックスが必要です。

#### キャプション属性{#identifying-the-dialogs-specified-in-caption-attributes}で指定されているダイアログを特定する

Microsoft Spy++を使用して、ネイティブアプリケーションのウィンドウ要素プロパティのIDを取得します。 スクリプトを作成するには、これらのIDが必要です。

#### キャプション属性での正規式の使用{#using-regular-expressions-in-caption-attributes}

キャプションの仕様では、正規式を使用できます。 Generate PDFサービスは、`java.util.regex.Matcher`クラスを使用して正規式をサポートします。 `java.util.regex.Pattern`で説明されている正規式をサポートしています。 (JavaのWebサイト([https://java.sun.com/j2se/1.4.2/docs/api/java/util/regex/Pattern.html](https://java.sun.com/j2se/1.4.2/docs/api/java/util/regex/Pattern.html))にアクセスします)。

**メモ帳バナーの前に付加されるファイル名を格納する正規式**

```xml
 <!-- The regular expression ".*Notepad" means any number of non-terminating characters followed by Notepad. -->
 <step>
     <expectedWindow>
         <window caption=".*Notepad"/>
     </expectedWindow>
 </step>
```

**印刷と印刷設定を区別する正規式**

```xml
 <!-- This regular expression differentiates the Print dialog box from the Print Setup dialog box. The "^" specifies the beginning of the line, and the "$" specifies the end of the line. -->
 <windowList>
     <window controlID="0x01" caption="^Print$" action="press"/>
 </windowList>
```

#### window要素とwindowList要素の順序{#ordering-the-window-and-windowlist-elements}

`window`要素と`windowList`要素は、次のように並べる必要があります。

* 複数の`window`要素が`windowList`または`dialog`要素内の子として表示される場合、それらの`window`要素を降順に並べ、`caption`名前の長さで順序内の位置を示します。
* 複数の`windowList`要素が`window`要素に出現する場合、それらの`windowList`要素を降順に並べます。最初の`indexes/`要素の`caption`属性の長さは、順序内の位置を示します。

**ダイアログファイル内のウィンドウ要素の順序付け**

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

以前サポートされていなかったネイティブアプリケーションのスクリプトを作成する場合は、そのアプリケーション用に追加のダイアログXMLファイルも作成する必要があります。 AppMonで使用されるすべてのネイティブアプリケーションには、ダイアログXMLファイルが1つだけ必要です。 未承諾のダイアログボックスが想定されない場合でも、追加のダイアログXMLファイルが必要です。 追加のダイアログボックスには、その`window`要素が単なるプレースホルダーであっても、少なくとも1つの`window`要素が必要です。

>[!NOTE]
>
>このコンテキストで、additionalは`appmon.[applicationname].addition.[locale]`.xml`ファイルの内容を表します。 このようなファイルは、ダイアログXMLファイルへの上書きと追加を指定します。

ネイティブアプリケーション用の追加のダイアログXMLファイルは、次の目的で変更することもできます。

* 別の応答を持つアプリケーションのダイアログXMLファイルを上書きするには
* そのアプリケーションのダイアログXMLファイル内で指定されていないダイアログボックスに応答を追加するには

追加のdialogXMLファイルを識別するファイル名は`appmon.[appname].addition.[locale].xml`です。 appmon.excel.addition.en_US.xmlなどがあります。

追加のダイアログXMLファイルの名前は、`appmon.[applicationname].addition.[locale].xml`の形式を使用する必要があります。*applicationname*&#x200B;は、XML設定ファイルおよびスクリプトで使用されるアプリケーション名と完全に一致する必要があります。

>[!NOTE]
>
>native2pdfconfig.xml設定ファイルで指定された汎用アプリケーションには、プライマリダイアログXMLファイルがありません。 [ネイティブファイル形式](converting-file-formats-pdf.md#adding-or-modifying-support-for-a-native-file-format)のサポートの追加または変更の節で、このような仕様を説明します。

`window`要素に子として表示する`windowList`要素を順に並べる必要があります。 （[ウィンドウ要素とwindowList要素の順序](converting-file-formats-pdf.md#ordering-the-window-and-windowlist-elements)を参照）。

### 一般的なダイアログXMLファイルの変更{#modifying-the-general-dialog-xml-file}

一般的なダイアログXMLファイルを変更して、システムによって生成されたダイアログボックスに応答したり、複数のアプリケーションに共通するダイアログボックスに応答したりできます。

#### XML構成ファイル{#adding-a-filetype-entry-in-the-xml-configuration-file}にファイルタイプエントリを追加する

この手順では、Generate PDFサービス設定ファイルを更新して、ファイルの種類をネイティブアプリケーションに関連付ける方法を説明します。 この設定ファイルを更新するには、管理コンソールを使用して設定データをファイルに書き出す必要があります。 設定データのデフォルトのファイル名は、native2pdfconfig.xmlです。

**Generate PDFサービス設定ファイルの更新**

1. **ホーム**/**サービス**/**Adobe PDFジェネレーター**/**構成ファイル**&#x200B;を選択し、「**構成を書き出し**」を選択します。
1. 必要に応じて、native2pdfconfig.xmlファイルの`filetype-settings`要素を変更します。
1. **ホーム**/**サービス**/**Adobe PDFジェネレーター**/**構成ファイル**&#x200B;を選択し、「**構成を読み込み**」を選択します。 設定データがGenerate PDFサービスに読み込まれ、以前の設定は置き換えられます。

>[!NOTE]
>
>アプリケーションの名前は、`GenericApp`要素の`name`属性の値として指定されます。 この値は、そのアプリケーション用に開発するスクリプトで指定された、対応する名前と完全に一致する必要があります。 同様に、`GenericApp`要素の`displayName`属性は、対応するスクリプトの`expectedWindow`ウィンドウのキャプションと完全に一致する必要があります。 このような等価性は、`displayName`属性または`caption`属性に出現する正規式を解決した後で評価されます。

この例では、Generate PDFサービスに付属のデフォルトの設定データを変更し、（Microsoft Wordではなく）メモ帳を使用してファイル名拡張子.txtのファイルを処理するように指定しています。 この変更前は、Microsoft Wordは、このようなファイルを処理するネイティブアプリケーションとして指定されていました。

**テキストファイルをメモ帳に向けるための変更(native2pdfconfig.xml)**

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

#### ネイティブ環境を特定するアプリケーション変数の作成{#creating-an-environment-variable-to-locate-the-native-application}

ネイティブ環境の実行可能ファイルの場所を指定するアプリケーション変数を作成します。 変数は`[applicationname]_PATH`の形式を使用する必要があります。*applicationname*&#x200B;は、XML設定ファイルおよびスクリプトで使用されるアプリケーション名と完全に一致し、パスには重複引用符で囲まれた実行可能ファイルのパスが含まれます。 このような環境変数の例は`Photoshop_PATH`です。

新しい環境変数を作成したら、Generate PDFサービスをデプロイしているサーバーを再起動する必要があります。

**Windows XP環境でシステム変数を作成する**

1. **Campaign コントロールパネル/システム**&#x200B;を選択します。
1. 「System Properties」ダイアログ・ボックスで、「**Advanced**」タブをクリックし、「**環境変数**」をクリックします。
1. [環境変数]ダイアログボックスの[システム変数]で、[**新規**]をクリックします。
1. 「New System Variable」ダイアログ・ボックスの「**Variable name**」ボックスに、`[applicationname]_PATH`という形式を使用する名前を入力します。
1. 「**Variable value**」ボックスに、アプリケーションの実行可能ファイルのフルパスとファイル名を入力し、「**OK**」をクリックします。 例えば、次のように入力します。`c:\windows\Notepad.exe`
1. [環境変数]ダイアログボックスで、[**OK**]をクリックします。

**コマンドラインからシステム変数を作成する**

1. コマンドラインウィンドウで、次の形式を使用して変数定義を入力します。

   ```shell
            [applicationname]_PATH=[Full path name]
   ```

   例えば、次のように入力します。`NotePad_PATH=C:\WINDOWS\NOTEPAD.EXE`

1. システム変数を有効にするための新しいコマンドラインプロンプトを開始します。

#### XMLファイル{#xml-files}

AEM Formsには、Generate PDFサービスでメモ帳を使用してファイル名拡張子.txtのファイルを処理するためのサンプルXMLファイルが含まれています。 このコードは、この節に含まれています。 さらに、この節で説明するその他の変更を行う必要があります。

#### 追加のダイアログXMLファイル{#additional-dialog-xml-file}

次の使用例は、メモ帳アプリケーション用の追加のダイアログボックスを含みます。 これらのダイアログボックスは、Generate PDFサービスで指定されているダイアログボックスに加えて使用できます。

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

**NotepadスクリプトXMLファイル(appmon.notepad.script.en_US.xml)**

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

