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
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# ファイル形式とPDFの変換 {#converting-between-file-formatsand-pdf}

**Generate PDFサービスについて**

Generate PDF サービスは、ネイティブファイル形式を PDF に変換します。また、PDF を他のファイル形式に変換し、PDF ドキュメントのサイズを最適化します。

Generate PDF サービスは、以下のファイル形式を PDF に変換する際にネイティブアプリケーションを使用します。特に説明がない限り、これらのアプリケーションはドイツ語版、フランス語版、英語版および日本語版のみサポートされています。*Windowsのみ* 、Windows Server® 2003およびWindows Server 2008のみがサポートされていることを示します。

* DOC、DOCX、RTF、TXT、XLS、XLSX、PPT、PPTX、VSD、MPP、MPPX、XPS、PUBの変換（Windowsのみ）

   **注意**:Microsoft XPS形式をPDFに変換するには、Acrobat® 9.2以降が必要です。*

* DWF、DWG、DXWを変換するAutodesk AutoCAD 2005、2006、2007、2008、2009（英語のみ）
* WPD、QPW、SHWを変換するCorel WordPerfect 12およびX4（英語のみ）
* OpenOffice 2.0、2.4、3.0.1および3.1:ODT、ODP、ODG、ODF、SXW、SXI、SXC、SXD、DOC、DOCX、RTF、TXT、XLS、XLSX、PPT、pptx、VSD、MPP、MPPX、PUB

   ***注意&#x200B;**:Generate PDFサービスは、64ビットバージョンのOpenOfficeをサポートしていません。*

* PSDを変換するAdobe Photoshop® CS2（Windowsのみ）

   *注&#x200B;**意**:Photoshop CS3およびCS4は、Windows Server 2003またはWindows Server 2008をサポートしていないので、サポートされていません。*

* FM変換用のAdobe FrameMaker® 7.2および8（Windowsのみ）
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
* DeviceRGBカラースペースのみを使用するPDF/A-1a
* DeviceRGBカラースペースのみを使用するPDF/A-1b

Generate PDF サービスを使用するには、以下の管理タスクを実行する必要があります。

* 必要なネイティブアプリケーションを、AEM Forms をホストするコンピューター上にインストールする
* AEM FormsをホストするコンピューターにAdobe Acrobat ProfessionalまたはAcrobat Pro Extended 9.2をインストールします。
* インストール後のセットアップタスクを実行する

これらのタスクについては、『JBoss自動インストールおよびデプロイ（AEM formsの場合）』を参照してください。

Generate PDFサービスを使用して、次のタスクを実行できます。

* ネイティブファイル形式からPDFに変換します。
* HTMLドキュメントをPDFドキュメントに変換
* PDFドキュメントをファイル形式に変換

>[!NOTE]
>
>For more information about the Generate PDF service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## WordドキュメントのPDFドキュメント {#converting-word-documents-to-pdf-documents}

ここでは、Generate PDF APIを使用して、Microsoft WordのドキュメントをPDFドキュメントに変換する方法について説明します。

>[!NOTE]
>
>その他のファイル形式について詳しくは、「追加のネイティブフ [ァイル形式に対するサポートの追加」を参照してくださ](converting-file-formats-pdf.md#adding-support-for-additional-native-file-formats)い。

>[!NOTE]
>
>For more information about the Generate PDF service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary-of-steps}

Microsoft WordドキュメントをPDFドキュメントに変換するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Generate PDFクライアントの作成を参照してください。
1. PDFに変換するファイルを取得します。ドキュメント
1. ファイルをPDFに変換します。ドキュメント
1. 結果を取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

**Generate PDFクライアントの作成**

プログラムによってGenerate PDF操作を実行する前に、Generate PDFサービスクライアントを作成します。 Java APIを使用している場合は、オブジェクトを作成し `GeneratePdfServiceClient` ます。 WebサービスAPIを使用している場合は、オブジェクトを作成 `GeneratePDFServiceService` します。

**PDFに変換するファイルの取得ドキュメント**

PDFドキュメントに変換するMicrosoft Wordドキュメントを取得します。

**ファイルをPDFに変換するドキュメント**

Generate PDFサービスクライアントを作成した後、このメソッドを呼び出すことがで `createPDF2` きます。 このメソッドには、変換するドキュメント（ファイル拡張子を含む）に関する情報が必要です。

**結果の取得**

ファイルがPDFドキュメントに変換された後、結果を取得できます。 例えば、WordファイルをPDFドキュメントに変換した後、PDFファイルを取得して保存できます。ドキュメント

**関連トピック**

[Java APIを使用してWordドキュメントをPDFドキュメントに変換する](converting-file-formats-pdf.md#convert-word-documents-to-pdf-documents-using-the-java-api)

[WebサービスAPIを使用してWordドキュメントをPDFドキュメントに変換する](converting-file-formats-pdf.md#convert-word-documents-to-pdf-documents-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Generate PDFサービスAPIのクイック開始](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### Java APIを使用してWordドキュメントをPDFドキュメントに変換する {#convert-word-documents-to-pdf-documents-using-the-java-api}

Generate PDF API(Java)を使用して、Microsoft WordドキュメントをPDFドキュメントに変換します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-generatepdf-client.jarなどのクライアントJARファイルを含めます。

1. Generate PDFクライアントの作成を参照してください。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `GeneratePdfServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. PDFに変換するファイルを取得します。ドキュメント

   * 変換するWord `java.io.FileInputStream` ファイルを表すオブジェクトを、コンストラクタを使用して作成します。 ファイルの場所を指定するstring値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. ファイルをPDFに変換します。ドキュメント

   オブジェクトのメソッドを呼び出し、次の値を `GeneratePdfServiceClient` 渡して、ファイル `createPDF2` をPDFドキュメントに変換します。

   * A `com.adobe.idp.Document` object that represents the file to convert.
   * ファイル `java.lang.String` 拡張子を含むオブジェクトです。
   * 変換に `java.lang.String` 使用するファイルタイプ設定を含むオブジェクトです。 ファイルタイプの設定は、.docや.xlsなど、異なるファイルタイプの変換設定を提供します。
   * 使用 `java.lang.String` するPDF設定の名前を含むオブジェクトです。 For example, you can specify `Standard`.
   * 使用 `java.lang.String` するセキュリティ設定の名前を含むオブジェクトです。
   * PDF生成時 `com.adobe.idp.Document` に適用される設定を含むオプションのオブジェクトです。ドキュメント
   * PDFオブジェクト `com.adobe.idp.Document` に適用されるメタデータ情報を含むオプションのドキュメントです。
   このメソ `createPDF2` ッドは、新しいPDF `CreatePDFResult` ドキュメントとログ情報を含むオブジェクトを返します。 通常、ログファイルには、変換要求によって生成されたエラーメッセージまたは警告メッセージが含まれます。

1. 結果を取得します。

   PDFアクションを取得するには、次のドキュメントを実行します。

   * オブジェクト `CreatePDFResult` のメソッドを呼 `getCreatedDocument` び出し、オブジェクトを返 `com.adobe.idp.Document` します。
   * オブジェクト `com.adobe.idp.Document` のメソッドを `copyToFile` 呼び出して、前の手順で作成したオブジェクトからPDFドキュメントを抽出します。
   このメソッドを使用し `createPDF2` てログドキュメントを取得した場合（HTML変換には適用されません）、次の操作を実行します。

   * オブジェクトの `CreatePDFResult` メソッドを呼び出 `getLogDocument` します。 オブジェクトを返 `com.adobe.idp.Document` します。
   * オブジェクト `com.adobe.idp.Document` のメソッドを呼 `copyToFile` び出して、ログドキュメントを抽出します。


**関連トピック**

[手順の概要](converting-file-formats-pdf.md#summary-of-steps)

[クイック開始（SOAPモード）:Java APIを使用したMicrosoft WordドキュメントのPDFドキュメントへの変換](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-a-microsoft-word-document-to-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用してWordドキュメントをPDFドキュメントに変換する {#convert-word-documents-to-pdf-documents-using-the-web-service-api}

Generate PDF API（Webサービス）を使用して、Microsoft WordドキュメントをPDFドキュメントに変換します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. Generate PDFクライアントの作成を参照してください。

   * Create a `GeneratePDFServiceClient` object by using its default constructor.
   * Create a `GeneratePDFServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLを指定するstring値をAEM Formsサービス(例： `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`.)に渡します。属性を使用する必要はありま `lc_version` せん。 ただし、を指定しま `?blob=mtom`す。
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得して、オブジェクトを作成 `GeneratePDFServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のオプションを実行して、基本的なHTTP認証を有効にします。タスク

      * AEM formsのユーザー名をフィールドに割り当てま `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `GeneratePDFServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールドに `HttpClientCredentialType.Basic` 割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールドに `BasicHttpSecurityMode.TransportCredentialOnly` 割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. PDFに変換するファイルを取得します。ドキュメント

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、PDFドキュメントに変換するファイルの保存に使用されます。
   * Create a `System.IO.FileStream` object by invoking its constructor. 変換するファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * オブジェクトの内容を格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得す `System.IO.FileStream` ることで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイ `System.IO.FileStream` ト配列、開始位 `Read` 置およびストリームの長さを渡すことで、バイト配列にストリームデータを入力します。
   * オブジェクト `BLOB` にバイト配列の内容をプロパティ `MTOM` に割り当てて、オブジェクトを設定します。

1. ファイルをPDFに変換します。ドキュメント

   オブジェクトのメソッドを呼び出し、次の値を `GeneratePDFServiceService` 渡して、ファイル `CreatePDF2` をPDFドキュメントに変換します。

   * 変換す `BLOB` るファイルを表すオブジェクトです。
   * ファイル拡張子を含む文字列。
   * 変換に `java.lang.String` 使用するファイルタイプ設定を含むオブジェクトです。 ファイルタイプの設定は、.docや.xlsなど、異なるファイルタイプの変換設定を提供します。
   * 使用するPDF設定を含むstringオブジェクトです。 You can specify `Standard`.
   * 使用するセキュリティ設定を含むstringオブジェクトです。 You can specify `No Security`.
   * PDF生成時 `BLOB` に適用される設定を含むオプションのオブジェクトです。ドキュメント
   * PDFオブジェクト `BLOB` に適用されるメタデータ情報を含むオプションのドキュメントです。
   * メソッドによって設定さ `BLOB` れるタイプの出力パラメー `CreatePDF2` ター。 このメソッ `CreatePDF2` ドは、変換後のオブジェクトをこのオブジェクトにドキュメントします。 （このパラメーター値は、Webサービスの呼び出しにのみ必要です）。
   * メソッドによって設定さ `BLOB` れるタイプの出力パラメー `CreatePDF2` ター。 メソッド `CreatePDF2` は、このオブジェクトにログドキュメントを設定します。 （このパラメーター値は、Webサービスの呼び出しにのみ必要です）。

1. 結果を取得します。

   * 変換されたPDFドキュメントを取得するには、オブジェクトの `BLOB` フィールドをバ `MTOM` イト配列に割り当てます。 バイト配列は、変換されたPDFドキュメントを表します。 メソッドの出力パラメ `BLOB` ーターとして使用するオブジェクトを使用してく `createPDF2` ださい。
   * コンストラクタ `System.IO.FileStream` ーを呼び出し、変換されたPDFフォルダーのファイルの場所を表すstring値を渡して、オブジェクトを作成します。ドキュメント
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡すことによって、バ `System.IO.BinaryWriter` イト配列の内 `Write` 容をPDFファイルに書き込みます。

**関連トピック**

[手順の概要](converting-file-formats-pdf.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## HTMLドキュメントのPDFへの変換ドキュメント {#converting-html-documents-to-pdf-documents}

この節では、Generate PDF APIを使用して、HTMLドキュメントをPDF画像にプログラム変換する方法を説明します。

>[!NOTE]
>
>For more information about the Generate PDF service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-1}

HTMLドキュメントをPDFドキュメントに変換するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Generate PDFクライアントの作成を参照してください。
1. PDFに変換するHTMLコンテンツを取得します。ドキュメント
1. HTMLコンテンツをPDFに変換しますドキュメント。
1. 結果を取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

**Generate PDFクライアントの作成**

プログラムによってGenerate PDF操作を実行する前に、Generate PDFサービスクライアントを作成する必要があります。 Java APIを使用している場合は、オブジェクトを作成し `GeneratePdfServiceClient` ます。 WebサービスAPIを使用している場合は、を作成しま `GeneratePDFServiceService`す。

**PDFに変換するHTMLコンテンツの取得ドキュメント**

PDFコンテンツに変換するHTMLコンテンツを参照します。ドキュメント HTMLファイルやURLを使用してアクセス可能なHTMLコンテンツなどのHTMLコンテンツを参照できます。

**HTMLコンテンツのPDFへの変換ドキュメント**

サービスクライアントの作成後、適切なPDF作成操作を呼び出すことができます。 この操作には、変換するドキュメントに関する情報(ターゲットドキュメントのパスなど)が必要です。

**結果の取得**

HTMLコンテンツがPDFドキュメントに変換されたら、結果を取得してPDFドキュメントを保存できます。

**関連トピック**

[Java APIを使用したHTMLコンテンツのPDFドキュメントへの変換](converting-file-formats-pdf.md#convert-html-content-to-a-pdf-document-using-the-java-api)

[WebサービスAPIを使用したHTMLコンテンツのPDFドキュメントへの変換](converting-file-formats-pdf.md#convert-html-content-to-a-pdf-document-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Generate PDFサービスAPIのクイック開始](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### Java APIを使用したHTMLコンテンツのPDFドキュメントへの変換 {#convert-html-content-to-a-pdf-document-using-the-java-api}

Generate PDF API(Java)を使用してHTMLドキュメントをPDFドキュメントに変換します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-generatepdf-client.jarなどのクライアントJARファイルを含めます。

1. Generate PDFクライアントの作成を参照してください。

   コンストラクタ `GeneratePdfServiceClient` ーを使用し、接続プロパティを含むオブジェクトを渡 `ServiceClientFactory` して、オブジェクトを作成します。

1. PDFに変換するHTMLコンテンツを取得します。ドキュメント

   文字列変数を作成し、HTMLコンテンツを指すURLを割り当てて、HTMLコンテンツを取得します。

1. HTMLコンテンツをPDFに変換しますドキュメント。

   オブジェクト `GeneratePdfServiceClient` のメソッドを `htmlToPDF2` 呼び出し、次の値を渡します。

   * 変換 `java.lang.String` するHTMLファイルのURLを含むオブジェクトです。
   * 変換に `java.lang.String` 使用するファイルタイプ設定を含むオブジェクトです。 ファイルタイプの設定には、スパイダレベルを含めることができます。
   * 使用 `java.lang.String` するセキュリティ設定の名前を含むオブジェクトです。
   * PDF生成時 `com.adobe.idp.Document` に適用される設定を含むオプションのオブジェクトです。ドキュメント この情報を指定しない場合、設定は前の3つのパラメーターに基づいて自動的に選択されます。
   * PDFオブジェクト `com.adobe.idp.Document` に適用されるメタデータ情報を含むオプションのドキュメントです。

1. 結果を取得します。

   生成さ `htmlToPDF2` れた新しいPDF `HtmlToPdfResult` ドキュメントを含むオブジェクトを返します。 新しく作成されたPDFアクションを取得するには、次のドキュメントを実行します。

   * オブジェクトの `HtmlToPdfResult` メソッドを呼び出 `getCreatedDocument` します。 オブジェクトを返 `com.adobe.idp.Document` します。
   * オブジェクト `com.adobe.idp.Document` のメソッドを `copyToFile` 呼び出して、前の手順で作成したオブジェクトからPDFドキュメントを抽出します。

**関連トピック**

[HTMLドキュメントのPDFへの変換ドキュメント](converting-file-formats-pdf.md#converting-html-documents-to-pdf-documents)

[クイック開始（SOAPモード）:Java APIを使用したHTMLコンテンツのPDFドキュメントへの変換](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[クイック開始（SOAPモード）:Java APIを使用したHTMLコンテンツのPDFドキュメントへの変換](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したHTMLコンテンツのPDFドキュメントへの変換 {#convert-html-content-to-a-pdf-document-using-the-web-service-api}

Generate PDF API（Webサービス）を使用してHTMLコンテンツをPDFドキュメントに変換します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. Generate PDFクライアントの作成を参照してください。

   * Create a `GeneratePDFServiceClient` object by using its default constructor.
   * Create a `GeneratePDFServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLを指定するstring値をAEM Formsサービス(例： `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`.)に渡します。属性を使用する必要はありま `lc_version` せん。 ただし、を指定しま `?blob=mtom`す。
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得して、オブジェクトを作成 `GeneratePDFServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のオプションを実行して、基本的なHTTP認証を有効にします。タスク

      * AEM formsのユーザー名をフィールドに割り当てま `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `GeneratePDFServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールドに `HttpClientCredentialType.Basic` 割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールドに `BasicHttpSecurityMode.TransportCredentialOnly` 割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. PDFに変換するHTMLコンテンツを取得します。ドキュメント

   文字列変数を作成し、HTMLコンテンツを指すURLを割り当てて、HTMLコンテンツを取得します。

1. HTMLコンテンツをPDFに変換しますドキュメント。

   オブジェクトのメソッドを呼び出し、次の値を `GeneratePDFServiceService` 渡して、HTMLコン `HtmlToPDF2` テンツをPDFドキュメントに変換します。

   * 変換するHTMLコンテンツを含む文字列です。
   * 変換に `java.lang.String` 使用するファイルタイプ設定を含むオブジェクトです。
   * 使用するセキュリティ設定を含むstringオブジェクトです。
   * PDF生成時 `BLOB` に適用される設定を含むオプションのオブジェクトです。ドキュメント
   * PDFオブジェクト `BLOB` に適用されるメタデータ情報を含むオプションのドキュメントです。
   * メソッドによって設定さ `BLOB` れるタイプの出力パラメー `CreatePDF2` ター。 このメソッ `CreatePDF2` ドは、変換後のオブジェクトをこのオブジェクトにドキュメントします。 （このパラメーター値は、Webサービスの呼び出しにのみ必要です）。

1. 結果を取得します。

   * 変換されたPDFドキュメントを取得するには、オブジェクトの `BLOB` フィールドをバ `MTOM` イト配列に割り当てます。 バイト配列は、変換されたPDFドキュメントを表します。 メソッドの出力パラメ `BLOB` ーターとして使用するオブジェクトを使用してく `HtmlToPDF2` ださい。
   * コンストラクタ `System.IO.FileStream` ーを呼び出し、変換されたPDFフォルダーのファイルの場所を表すstring値を渡して、オブジェクトを作成します。ドキュメント
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡すことによって、バ `System.IO.BinaryWriter` イト配列の内 `Write` 容をPDFファイルに書き込みます。

**関連トピック**

[HTMLドキュメントのPDFへの変換ドキュメント](converting-file-formats-pdf.md#converting-html-documents-to-pdf-documents)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## PDFドキュメントの非画像形式への変換 {#converting-pdf-documents-to-non-image-formats}

この節では、Generate PDF Java APIとWebサービスAPIを使用して、PDFドキュメントをプログラムでRTFファイルに変換する方法について説明します。このファイルは画像以外の形式の例です。 その他の非画像形式には、HTML、テキスト、DOC、EPSが含まれます。 PDFドキュメントをRTFに変換する場合は、PDFドキュメントに送信ボタンなどのフォーム要素が含まれていないことを確認します。 フォーム要素は変換されません。

>[!NOTE]
>
>For more information about the Generate PDF service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-2}

PDFドキュメントをサポートされている任意の種類に変換するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Generate PDFクライアントの作成を参照してください。
1. 変換するPDFドキュメントを取得します。
1. 「Convert the PDF」ドキュメント
1. 変換したファイルを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

**Generate PDFクライアントの作成**

プログラムによってGenerate PDF操作を実行する前に、Generate PDFサービスクライアントを作成する必要があります。 Java APIを使用している場合は、オブジェクトを作成し `GeneratePdfServiceClient` ます。 WebサービスAPIを使用している場合は、オブジェクトを作成 `GeneratePDFServiceService` します。

**変換するPDFドキュメントの取得**

画像以外の形式に変換するPDFドキュメントを取得します。

**「Convert the PDF」ドキュメント**

サービスクライアントを作成したら、PDF書き出し操作を呼び出すことができます。 この操作には、変換するドキュメントに関する情報(ターゲットドキュメントのパスなど)が必要です。

**変換したファイルを保存**

変換したファイルを保存します。 例えば、PDFドキュメントをRTFファイルに変換する場合、変換後のドキュメントをRTFファイルに保存します。

**関連トピック**

[Java APIを使用したPDFドキュメントのRTFファイルへの変換](converting-file-formats-pdf.md#convert-a-pdf-document-to-a-rtf-file-using-the-java-api)

[WebサービスAPIを使用してPDFドキュメントをRTFファイルに変換する](converting-file-formats-pdf.md#convert-a-pdf-document-to-a-rtf-file-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Generate PDFサービスAPIのクイック開始](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### Java APIを使用したPDFドキュメントのRTFファイルへの変換 {#convert-a-pdf-document-to-a-rtf-file-using-the-java-api}

Generate PDF API(Java)を使用してPDFドキュメントをRTFファイルに変換します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-generatepdf-client.jarなどのクライアントJARファイルを含めます。

1. Generate PDFクライアントの作成を参照してください。

   コンストラクタ `GeneratePdfServiceClient` ーを使用し、接続プロパティを含むオブジェクトを渡 `ServiceClientFactory` して、オブジェクトを作成します。

1. 変換するPDFドキュメントを取得します。

   * コンストラクタ `java.io.FileInputStream` ーを使用して、変換するPDFドキュメントを表すオブジェクトを作成します。 PDFフォルダーの場所を指定するstring値を渡します。ドキュメント
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 「Convert the PDF」ドキュメント

   オブジェクト `GeneratePdfServiceClient` のメソッドを `exportPDF2` 呼び出し、次の値を渡します。

   * 変換す `com.adobe.idp.Document` るPDFファイルを表すオブジェクトです。
   * 変換す `java.lang.String` るファイルの名前を含むオブジェクトです。
   * Adobe PDF `java.lang.String` 設定の名前を含むオブジェクトです。
   * 変換の `ConvertPDFFormatType` ターゲットファイルの種類を指定するオブジェクト。
   * PDF生成時 `com.adobe.idp.Document` に適用される設定を含むオプションのオブジェクトです。ドキュメント
   このメソ `exportPDF2` ッドは、変換されたフ `ExportPDFResult` ァイルを含むオブジェクトを返します。

1. 「Convert the PDF」ドキュメント

   新しく作成したファイルを取得するには、次の操作を実行します。

   * オブジェクトの `ExportPDFResult` メソッドを呼び出 `getConvertedDocument` します。 オブジェクトを返 `com.adobe.idp.Document` します。
   * オブジェクト `com.adobe.idp.Document` のメソッドを呼 `copyToFile` び出して、新しいドキュメントを抽出します。

**関連トピック**

[手順の概要](converting-file-formats-pdf.md#summary-of-steps)

[クイック開始（SOAPモード）:Java APIを使用したHTMLコンテンツのPDFドキュメントへの変換](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用してPDFドキュメントをRTFファイルに変換する {#convert-a-pdf-document-to-a-rtf-file-using-the-web-service-api}

Generate PDF API（Webサービス）を使用してPDFドキュメントをRTFファイルに変換します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. Generate PDfクライアントを作成します。

   * Create a `GeneratePDFServiceClient` object by using its default constructor.
   * Create a `GeneratePDFServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLを指定するstring値をAEM Formsサービス(例： `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`.)に渡します。属性を使用する必要はありま `lc_version` せん。 ただし、を指定しま `?blob=mtom`す。
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得して、オブジェクトを作成 `GeneratePDFServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のオプションを実行して、基本的なHTTP認証を有効にします。タスク

      * AEM formsのユーザー名をフィールドに割り当てま `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `GeneratePDFServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールドに `HttpClientCredentialType.Basic` 割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールドに `BasicHttpSecurityMode.TransportCredentialOnly` 割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. 変換するPDFドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、変換されたPDFドキュメントの保存に使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、PDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトの内容を格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得す `System.IO.FileStream` ることで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイ `System.IO.FileStream` ト配列、開始位 `Read` 置およびストリームの長さを渡すことで、バイト配列にストリームデータを入力します。
   * オブジェクト `BLOB` にバイト配列の内容をプロパティ `MTOM` に割り当てて、オブジェクトを設定します。

1. 「Convert the PDF」ドキュメント

   オブジェクト `GeneratePDFServiceServiceWse` のメソッドを `ExportPDF2` 呼び出し、次の値を渡します。

   * 変換す `BLOB` るPDFファイルを表すオブジェクトです。
   * 変換するファイルのパス名を含む文字列。
   * ファイ `java.lang.String` ルの場所を指定するオブジェクト。
   * 変換のターゲットファイルタイプを指定するstringオブジェクト。 Specify `RTF`.
   * PDF生成時 `BLOB` に適用される設定を含むオプションのオブジェクトです。ドキュメント
   * メソッドによって設定さ `BLOB` れるタイプの出力パラメー `ExportPDF2` ター。 このメソッ `ExportPDF2` ドは、変換後のオブジェクトをこのオブジェクトにドキュメントします。 （このパラメーター値は、Webサービスの呼び出しにのみ必要です）。

1. 変換したファイルを保存します。

   * 変換されたRTFドキュメントを取得するには、オブジェクトの `BLOB` フィールドをバ `MTOM` イト配列に割り当てます。 バイト配列は、変換されたRTFドキュメントを表します。 メソッドの出力パラメ `BLOB` ーターとして使用するオブジェクトを使用してく `ExportPDF2` ださい。
   * Create a `System.IO.FileStream` object by invoking its constructor. RTFファイルの場所を表すstring値を渡します。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡すことによって、バ `System.IO.BinaryWriter` イト配列の内 `Write` 容をRTFファイルに書き込みます。

**関連トピック**

[手順の概要](converting-file-formats-pdf.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 追加のネイティブファイル形式のサポートの追加 {#adding-support-for-additional-native-file-formats}

この節では、追加のネイティブファイル形式のサポートを追加する方法について説明します。 Generate PDFサービスと、このサービスがネイティブファイル形式をPDFに変換する際に使用するネイティブアプリケーションとの間のインタラクションの概要を示します。

この節では、次の点についても説明します。

* この製品がネイティブファイル形式をPDFに変換する際に既に使用しているネイティブアプリケーションに対するGenerate PDFサービスの応答を変更する方法
* Generate PDFサービス、Generate PDFサービスのApplication Monitor(AppMon)コンポーネント、およびMicrosoft Wordなどのネイティブアプリケーション間のインタラクション
* XMLグラマーがこれらのインタラクションで果たす役割

### コンポーネントの操作 {#component-interactions}

Generate PDFサービスは、ファイル形式に関連付けられたドキュメントを呼び出してネイティブのファイル形式を変換し、アプリケーションとやり取りして、デフォルトのプリンターを使用してアプリケーションを印刷します。 デフォルトのプリンターは、Adobe PDFプリンターとして設定する必要があります。

次の図に、ネイティブアプリケーションのサポートに関連するコンポーネントとドライバを示します。 また、インタラクションに影響を与えるXMLグラマーについても説明します。

ネイティブファイル変換のコンポーネントのインタラクション

このドキュメントでは、Microsoft Wordなどのネ *イティブファイル形式の生成に使用するアプリケーションを* 、ネイティブアプリケーションという用語を使用して示します。

*AppMonは* 、ユーザーが表示されるダイアログボックス内を移動するのと同じ方法で、ネイティブアプリケーションとやり取りするエンタープライズコンポーネントです。 Microsoft Wordなどのアプリケーションでファイルを開いて印刷するように指示するためにAppMonで使用されるXMLグラマーには、次の順次タスクが含まれます。

1. ファイル/開くを選択してファイルを開く
1. Openダイアログボックスが表示されることを確認します。そうでない場合は、エラーの処理
1. 「ファイル名」フィールドにファイル名を指定し、「開く」ボタンをクリックします。
1. ファイルを実際に開くこと
1. ファイル/印刷を選択して、印刷ダイアログボックスを開きます。
1. 印刷ダイアログボックスが表示されることを確認する

AppMonは、標準のWin32 APIを使用して、キーストロークやマウスクリックなどのUIイベントを転送するためのサードパーティアプリケーションとのやり取りを行います。これらのアプリケーションを制御して、PDFファイルを生成するのに役立ちます。

これらのWin32 APIの制限により、AppMonは、（TextPadなどの一部のアプリケーションで見つかる）フローティングメニューバーや、Win32 APIを使用してコンテンツを取得できない特定の種類のダイアログなど、特定の種類のウィンドウにこれらのUIイベントを送出できません。

フローティングメニューバーを視覚的に識別するのは簡単です。ただし、特別な種類のダイアログは、視覚検査だけでは特定できない場合があります。 AppMonが標準のWin32 APIを使用してAppMonとやり取りできるかどうかを判断するダイアログを調べるには、Microsoft Spy++(Microsoft Visual C++開発環境の一部)または同等のWinID( [https://www.dennisbabkin.com/php/download.php?what=WinID](https://www.dennisbabkin.com/php/download.php?what=WinID))などのサードパーティアプリケーションが必要です。

WinIDがテキスト、サブウィンドウ、ウィンドウクラスIDなどのダイアログコンテンツを抽出できる場合、AppMonも同様に機能します。

次の表に、ネイティブリスト形式の印刷に使用される情報の種類を示します。

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
   <td><p>PDF設定、セキュリティ設定、ファイルタイプ設定が含まれます。 </p><p>ファイルタイプ設定は、ファイル名拡張子を対応するネイティブアプリケーションに関連付けます。 また、ファイルタイプの設定では、ネイティブファイルの印刷に使用するネイティブアプリケーション設定も指定します。 </p></td>
   <td><p>既にサポートされているネイティブアプリケーションの設定を変更するには、システム管理者が管理コンソールで「ファイルタイプ設定」を設定します。 </p><p>新しいネイティブファイル形式のサポートを追加するには、ファイルを手動で編集する必要があります。 (ネイティブ <a href="converting-file-formats-pdf.md#adding-or-modifying-support-for-a-native-file-format">ファイル形式のサポートの追加または変更を参照</a>)。 </p></td>
  </tr>
  <tr>
   <td><p>スクリプト </p></td>
   <td><p>Generate PDFサービスとネイティブアプリケーションの間のインタラクションを指定します。 このような操作を行うと、通常、アプリケーションはAdobe PDFドライバーにファイルを印刷するように指示されます。 </p><p>スクリプトには、ネイティブアプリケーションに特定のダイアログボックスを開くよう指示し、これらのダイアログボックスのフィールドやボタンに対して特定の応答を提供する手順が含まれています。 </p></td>
   <td><p>Generate PDFサービスには、サポートされているすべてのネイティブアプリケーションのスクリプトファイルが含まれます。 これらのファイルは、XML編集アプリケーションを使用して変更できます。</p><p>新しいネイティブアプリケーションのサポートを追加するには、新しいスクリプトファイルを作成する必要があります。 (ネイティブ <a href="converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application">アプリケーション用の追加のダイアログXMLファイルの作成または変更を参照</a>)。 </p></td>
  </tr>
  <tr>
   <td><p>一般的なダイアログボックスの説明 </p></td>
   <td><p>複数のアプリケーションに共通のダイアログボックスに対する応答方法を指定します。 このようなダイアログボックスは、オペレーティングシステム、ヘルパーアプリケーション（PDFMakerなど）、およびドライバーによって生成されます。 </p><p>この情報を含むファイルは、appmon.global.en_US.xmlです。</p></td>
   <td><p>このファイルは変更しないでください。 </p></td>
  </tr>
  <tr>
   <td><p>アプリケーション固有のダイアログボックスの手順</p></td>
   <td><p>アプリケーション固有のダイアログボックスに対する応答方法を指定します。 </p><p>この情報を含むファイルはappmonです。<i>`[appname]`</i>.dialog.<i>`[ロケール]`</i>.xml （appmon.word.en_US.xmlなど）。</p></td>
   <td><p>このファイルは変更しないでください。 </p><p>新しいネイティブアプリケーション用のダイアログボックスの手順を追加するに <a href="converting-file-formats-pdf.md#creating_or_modifying_an_additional_dialog_xml_file_for_a_native_application">は、ネイティブアプリケーション用の追加のダイアログXMLファイルの作成または変更を参照してくださ</a>い。</p></td>
  </tr>
  <tr>
   <td><p>その他のアプリケーション固有のダイアログボックスの手順 </p></td>
   <td><p>アプリケーション固有のダイアログボックスの手順に対する上書きと追加を指定します。 この章では、このような情報の例を示します。 </p><p>この情報を含むファイルはappmonです。<i>`[appname]`</i>.addition.<i>`[ロケール]`</i>.xml. appmon.addition.en_US.xmlのような例です。</p></td>
   <td><p>このタイプのファイルは、XML編集アプリケーションを使用して作成および変更できます。 (ネイティブ <a href="converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application">アプリケーション用の追加のダイアログXMLファイルの作成または変更を参照</a>)。 </p><p><strong>重要</strong>:サーバーがサポートするネイティブアプリケーションごとに、アプリケーション固有の追加のダイアログボックスの手順を作成する必要があります。 </p></td>
  </tr>
 </tbody>
</table>

### スクリプトとダイアログのXMLファイルについて {#about-the-script-and-dialog-xml-files}

スクリプトXMLファイルは、Generate PDFサービスに対して、ユーザーがアプリケーションダイアログボックスを操作するのと同じ方法で、アプリケーションダイアログボックス間を移動するよう指示します。 また、スクリプトXMLファイルは、ボタンの押し下げ、チェックボックスの選択と選択解除、メニュー項目の選択などの操作を実行して、Generate PDFサービスにダイアログボックスへの応答を指示します。

これに対し、ダイアログXMLファイルは、スクリプトXMLファイルで使用されているのと同じタイプのアクションを持つダイアログボックスに応答します。

#### ダイアログボックスとウィンドウ要素の用語 {#dialog-box-and-window-element-terminology}

この節と次の節では、説明するパースペクティブに応じて、ダイアログボックスとその中のコンポーネントに対して異なる用語を使用します。 ダイアログボックスのコンポーネントは、ボタン、フィールド、コンボボックスなどの項目です。

この節と次の節では、ユーザの視点からダイアログボックスとそのコンポーネントについて説明する場合、ダイアログボックス *、ボタンフィールド*、コンボボ *ックス、コンボボック***** スが使用されます。

この節と次の節で、内部表現の観点からダイアログボックスとそのコンポーネントについて説明する場合、「 *window」要素* が使用されます。 ウィンドウ要素の内部表現は階層で、各ウィンドウ要素のインスタンスはラベルで識別されます。 ウィンドウ要素インスタンスは、その物理的な特性と動作も記述します。

ユーザーの観点から見ると、ダイアログボックスとそのコンポーネントは異なる動作を示し、一部のダイアログボックス要素はアクティブ化されるまで非表示になります。 内部表現の観点からは、そのような動作の問題は存在しません。 例えば、ダイアログボックスの内部表現は、ダイアログボックス内でネストされている点を除いて、そのダイアログボックスに含まれるコンポーネントの内部表現と似ています。

ここでは、AppMonに手順を提供するXML要素について説明します。 これらの要素には、要素や要素な `dialog` どの名前が付けら `window` れます。 このドキュメントでは、XML要素を区別するために等幅フォントを使用します。 この要 `dialog` 素は、XMLスクリプトファイルが意図的に、または意図せずに表示される原因となる可能性のあるダイアログボックスを識別します。 要素は、 `window` ウィンドウ要素（ダイアログボックスまたはダイアログボックスのコンポーネント）を識別します。

#### 階層 {#hierarchy}

次の図に、スクリプトとダイアログのXMLの階層を示します。 スクリプトのXMLファイルは、script.xsdスキーマに準拠しており、この中にwindow.xsdスキーマが含まれます（XMLの意味では）。 同様に、ダイアログXMLファイルは、dialogs.xsdスキーマに準拠しており、この中にwindow.xsdスキーマも含まれています。

![as_as_xml_hierarchy](assets/as_as_xml_hierarchy.png)

スクリプトとダイアログのXMLの階層

#### スクリプトXMLファイル {#script-xml-files}

スクリ *プトXMLファイルは* 、ネイティブアプリケーションが特定のウィンドウ要素に移動し、それらの要素に応答を提供するように指示する一連の手順を指定します。 ほとんどの応答は、対応するダイアログボックスのフィールド、コンボボックス、またはボタンにユーザーが入力したテキストまたはキーストロークです。

Generate PDFサービスでスクリプトXMLファイルをサポートする目的は、ネイティブアプリケーションにネイティブファイルを印刷させることです。 ただし、スクリプトXMLファイルは、ネイティブアプリケーションのダイアログボックスを操作する際にユーザーが実行できるタスクを実行するために使用できます。

スクリプトXMLファイル内の手順は、分岐の機会なしに順番に実行されます。 唯一の条件付きテストは、タイムアウト/再試行に対してサポートされます。このテストを実行すると、特定の期間内および特定の数の再試行後に手順が正常に完了しなかった場合に、スクリプトが終了します。

順次的なステップに加えて、ステップ内の命令も順に実行される。 手順と手順が、ユーザーが同じ手順を実行する順序を反映していることを確認する必要があります。

スクリプトXMLファイルの各手順は、手順の手順が正常に実行された場合に表示されるウィンドウ要素を識別します。 スクリプト手順の実行中に予期しないダイアログボックスが表示された場合、Generate PDFサービスは、次の節の説明に従ってダイアログXMLファイルを検索します。

#### ダイアログXMLファイル {#dialog-xml-files}

ネイティブアプリケーションを実行すると、表示モードと非表示モードのどちらであるかに関係なく、異なるダイアログボックスが表示されます。 ダイアログボックスは、オペレーティングシステムまたはアプリケーション自体で生成できます。 ネイティブアプリケーションがGenerate PDFサービスの制御下で実行されている場合、システムおよびネイティブアプリケーションのダイアログボックスが非表示のウィンドウに表示されます。

ダイアログ *XMLファイルは* 、Generate PDFサービスがシステムまたはネイティブのアプリケーションのダイアログボックスに対してどのように応答するかを指定します。 ダイアログXMLファイルを使用すると、Generate PDFサービスは、変換プロセスを容易にする方法で、要求されないダイアログボックスに応答できます。

現在実行中のスクリプトXMLファイルで処理されないダイアログボックスがシステムまたはネイティブアプリケーションで表示された場合、Generate PDFサービスは、次の順序でダイアログXMLファイルを検索し、一致が見つかると停止します。

* 申し込み`[appname]`.追加の.`[locale]`.xml
* 申し込み`[appname]` です。`[locale]`.xml（このファイルは変更しないでください）
* appmon.global.`[locale]`.xml（このファイルは変更しないでください）

Generate PDFサービスは、ダイアログボックスに一致するものを見つけた場合、ダイアログボックスに対して指定されたキーストロークまたは他のアクションを送信して、ダイアログボックスを閉じます。 ダイアログボックスの指示で中止メッセージが指定されている場合、Generate PDFサービスは現在実行中のジョブを終了し、エラーメッセージを生成します。 このような中止メッセージは、スクリプトXML文法の `abortMessage` 要素で指定されます。

Generate PDFサービスで、前述のファイルのいずれにも記述されていないダイアログボックスが見つかった場合、Generate PDFサービスは、ダイアログボックスのキャプションをログファイルエントリに組み込みます。 現在実行中のジョブは、最終的にタイムアウトになります。 その後、ログファイル内の情報を使用して、ネイティブアプリケーション用の追加のダイアログXMLファイルの新しい手順を作成できます。

### ネイティブファイル形式のサポートの追加または変更 {#adding-or-modifying-support-for-a-native-file-format}

この節では、他のネイティブファイル形式をサポートするため、または既にサポートされているネイティブファイル形式のサポートを変更するために実行する必要があるタスクについて説明します。

サポートを追加または変更する前に、次のオプションをタスクします。

#### ウィンドウ要素を識別するツールの選択 {#choosing-a-tool-for-identifying-window-elements}

ダイアログおよびスクリプトのXMLファイルでは、ダイアログまたはスクリプト要素が応答するウィンドウ要素（ダイアログボックス、フィールド、または他のダイアログコンポーネント）を指定する必要があります。 例えば、スクリプトがネイティブ・アプリケーションのメニューを呼び出した後、スクリプトはキーストロークまたはアクションを適用するメニュー上のウィンドウ要素を識別する必要があります。

ダイアログボックスは、タイトルバーに表示されるキャプションで簡単に識別できます。 ただし、Microsoft Spy++などのツールを使用して、下位レベルのウィンドウ要素を識別する必要があります。 下位レベルのウィンドウ要素は、明らかではない様々な属性を通して識別できます。 また、各ネイティブアプリケーションでウィンドウ要素が異なって識別される場合があります。 その結果、ウィンドウ要素を識別する複数の方法があります。 ウィンドウ要素の識別を考慮するための推奨順序を次に示します。

1. 一意の場合のキャプション自体
1. コントロールID（特定のダイアログボックスに対して一意である場合とそうでない場合）
1. クラス名。一意である場合とそうでない場合があります。

ウィンドウを識別するために、これら3つの属性のいずれかまたは組み合わせを使用できます。

属性がキャプションを識別できない場合、親に対するインデックスを使用してウィンドウ要素を識別できます。 インデ *ックス* は、兄弟ウィンドウ要素を基準としたウィンドウ要素の位置を指定します。 多くの場合、コンボボックスを識別するにはインデックスのみが使用されます。

次の問題に注意してください。

* Microsoft Spy++では、キャプションをアンパサンド(&amp;)を使用してキャプションのホットキーを識別して表示します。 例えば、Spy++では、1つの印刷ダイアログボックスのキャプションが「n」と表示され、ホッ `Pri&nt`トキーが「n」であることが示さ *れます*。 スクリプトおよびダイアログのXMLファイルのキャプションタイトルでは、アンパサンドを省略する必要があります。
* 一部のキャプションには改行が含まれます。 generate PDFサービスは改行を識別できません。 キャプションに改行が含まれる場合は、キャプションを他のメニュー項目と区別するのに十分な量含め、省略された部分には正規式を使用します。 An example is ( `^Long caption title$`).]. (キャプション [属性での正規式の使用を参照](converting-file-formats-pdf.md#using-regular-expressions-in-caption-attributes))。
* 予約されたXML文字には、文字エンティティ（エスケープシーケンスとも呼ばれる）を使用します。 例えば、アンパサン `&` ド、より小さい `<` 記号とより大きい記号、アポストロ `>` フィ、引用符 `&apos;``&quot;` に使用します。

ダイアログまたはスクリプトXMLファイルを操作する場合は、Microsoft Spy++アプリケーションをインストールする必要があります。

#### ダイアログとスクリプトファイルのパッケージ解除 {#unpackaging-the-dialog-and-script-files}

ダイアログファイルとスクリプトファイルは、appmondata.jarファイルに存在します。 これらのファイルを変更したり、新しいスクリプトやダイアログファイルを追加したりする前に、このJARファイルのパッケージを解除する必要があります。 例えば、EditPlusアプリケーションのサポートを追加するとします。 2つのXMLファイル（appmon.editplus.script.en_US.xmlおよびappmon.editplus.script.addition.en_US.xml）を作成します。 次に示すように、これらのXMLスクリプトは、adobe-appmondata.jarファイルの2か所に追加する必要があります。

* adobe-livecycle-native-jboss-x86_win32.ear > adobe-Native2PDFSvc.war\WEB-INF\lib > adobe-native.jar > Native2PDFSvc-native.jar\bin > adobe-appmondata.jar\com\adobe\appmon adobe-livecycle-native-jboss-x86_win32.earファイルは、のexportフォルダーにあります `[AEM forms install directory]\configurationManager`。 （AEM Formsを別のJ2EEアプリケーションサーバーにデプロイする場合は、adobe-livecycle-native-jboss-x86_win32.earファイルを、ご使用のJ2EEアプリケーションサーバーに対応するEARファイルに置き換えます）。
* adobe-generatepdf-dsc.jar/adobe-appmondata.jar\com\adobe\appmon （adobe-appmondata.jarファイルはadobe-generatepdf-dsc.jarファイル内にあります）。 adobe-generatepdf-dsc.jarファイルは、このフォルダーにあり `[AEM forms install directory]\deploy` ます。

これらのXMLファイルをadobe-appmondata.jarファイルに追加した後、GeneratePDFコンポーネントを再デプロイする必要があります。 ダイアログおよびスクリプトのXMLファイルをadobe-appmondata.jarファイルに追加するには、次のタスクを実行します。

1. WinZipやWinRARなどのツールを使用して、adobe-livecycle-native-jboss-x86_win32.earfile > adobe-Native2PDFSvc.war\WEB-INF\lib > adobe-native.jar > Native2PDFSvc-native.jar\bin > adobe-appmondata.jarファイルを開きます。
1. ダイア追加ログとスクリプトのXMLファイルをappmondata.jarファイルに追加するか、このファイル内の既存のXMLファイルを変更します。 (ネイティブア [プリケーション用のスクリプトXMLファイルの作成または変更お](converting-file-formats-pdf.md#creating-or-modifying-a-script-xml-file-for-a-native-application)よびネ [イティブアプリケーション用の追加のダイアログXMLファイルの作成または変更を参照](converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application))。
1. WinZipやWinRARなどのツールを使用して、adobe-generatepdf-dsc.jar/adobe-appmondata.jarを開きます。
1. ダイア追加ログとスクリプトのXMLファイルをappmondata.jarファイルに追加するか、このファイル内の既存のXMLファイルを変更します。 (ネイティブア [プリケーション用のスクリプトXMLファイルの作成または変更お](converting-file-formats-pdf.md#creating-or-modifying-a-script-xml-file-for-a-native-application)よびネ [イティブアプリケーション用の追加のダイアログXMLファイルの作成または変更を参照](converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application))。XMLファイルをadobe-appmondata.jarファイルに追加したら、新しいadobe-appmondata.jarファイルをadobe-generatepdf-dsc.jarファイルに配置します。
1. 追加のネイティブファイル形式のサポートを追加した場合は、環境のパスを提供するシステム環境変数を作成します(ネイティブアプリケーションを検索するためのシステム変数の作成を参照 [](converting-file-formats-pdf.md#creating-an-environment-variable-to-locate-the-native-application))。

**GeneratePDFコンポーネントを再デプロイするには**

1. Workbenchにログインします。
1. Select **Window** > **Show Views** > **Components**. この操作により、Workbenchにコンポーネント表示が追加されます。
1. GeneratePDFコンポーネントを右クリックし、「Stop Component」を **選択します**。
1. コンポーネントが停止したら、右クリックし、「Uninstall Component」を選択して削除します。
1. Right-click the **Components** icon and select **Install Component**.
1. 変更したadobe-generatepdf-dsc.jarファイルを参照して選択し、「開く」をクリックします。 GeneratePDFコンポーネントの横に赤い四角形が表示されます。
1. GeneratePDFコンポーネントを展開し、「Service Descriptors」を選択し、「GeneratePDFService」を右クリックして、「Activate Service」を選択します。
1. 表示される設定ダイアログボックスで、適切な設定値を入力します。 これらの値を空白のままにすると、デフォルトの設定値が使用されます。
1. 「GeneratePDF」を右クリックし、「コンポーネントの開始」を選択します。
1. 「Active Services」を展開します。 サービス名が実行中の場合は、その横に緑色の矢印が表示されます。 それ以外の場合、サービスは停止状態になります。
1. サービスが停止状態の場合は、サービス名を右クリックし、「サービス」を開始します。

### ネイティブアプリケーションのスクリプトXMLファイルの作成または変更 {#creating-or-modifying-a-script-xml-file-for-a-native-application}

ファイルを新しいネイティブアプリケーションに転送する場合は、そのアプリケーションのスクリプトXMLファイルを作成する必要があります。 既にサポートされているネイティブアプリケーションとGenerate PDFサービスとのやり取りを変更する場合は、そのアプリケーションのスクリプトを変更する必要があります。

スクリプトには、ネイティブアプリケーションのウィンドウ要素間を移動し、それらの要素に対して特定の応答を提供する手順が含まれています。 この情報を含むファイルは、 `appmon.`[appname]&quot; `.script.`[localeです]`.xml`。 例えば、appmon.notepad.script.en_US.xmlなどです。

#### スクリプトが実行する必要のある手順の識別 {#identifying-steps-the-script-must-execute}

ネイティブアプリケーションを使用して、ナビゲートする必要のあるウィンドウ要素と、アプリを印刷するために実行する必要のある各応答をドキュメントします。 任意の応答から生じるダイアログボックスに注目してください。 手順は次の手順に似ています。

1. ファイル／開くを選択します。
1. パスを指定し、「開く」をクリックします。
1. メニューバーでファイル/印刷を選択します。
1. プリンタに必要なプロパティを指定します。
1. 「印刷」を選択し、名前を付けて保存ダイアログボックスが表示されるのを待ちます。 Generate PDFサービスでPDFファイルの保存先を指定するには、Save Asダイアログボックスが必要です。

#### キャプション属性で指定されたダイアログの識別 {#identifying-the-dialogs-specified-in-caption-attributes}

Microsoft Spy++を使用して、ネイティブアプリケーションのウィンドウ要素プロパティのIDを取得します。 スクリプトを記述するには、これらのIDが必要です。

#### キャプション属性での正規式の使用 {#using-regular-expressions-in-caption-attributes}

標準のキャプションを式で使用できます。 Generate PDFサービスは、このクラスを使用し `java.util.regex.Matcher` て正規式をサポートします。 このユーティリティは、で説明する正規式をサポートしま `java.util.regex.Pattern`す。 (JavaのWebサイト(https://java.sun.com/j2se/1.4.2/docs/api/java/util/regex/Pattern.html [](https://java.sun.com/j2se/1.4.2/docs/api/java/util/regex/Pattern.html))にアクセス)。

**通常の式で、メモ帳のバナーに付加されるファイル名を格納します。**

```as3
 <!-- The regular expression ".*Notepad" means any number of non-terminating characters followed by Notepad. -->
 <step>
     <expectedWindow>
         <window caption=".*Notepad"/>
     </expectedWindow>
 </step>
```

**印刷と印刷設定を区別する標準式**

```as3
 <!-- This regular expression differentiates the Print dialog box from the Print Setup dialog box. The "^" specifies the beginning of the line, and the "$" specifies the end of the line. -->
 <windowList>
     <window controlID="0x01" caption="^Print$" action="press"/>
 </windowList>
```

#### window要素とwindowList要素の順序付け {#ordering-the-window-and-windowlist-elements}

要素と要素は、次のよ `window` うに並べ `windowList` 替える必要があります。

* 複数の要素 `window` が1つまたは複数の要素の子と `windowList` して表 `dialog` 示される場合は、それらの要素の順番を降順に並べ、名前の長さ `window``caption` は順序内の位置を示します。
* 要素内に複数 `windowList` の要素が表 `window` 示される場合、最初の要素の属性の長さで、 `windowList` 要素の降順に並べ替えます。最初の要 `caption``indexes/`素の属性の長さは、順序内の位置を示します。

**ダイアログファイル内のウィンドウ要素の順序付け**

```as3
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

```as3
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

### ネイティブアプリケーション用の追加のダイアログXMLファイルの作成または変更 {#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application}

以前はサポートされていなかったネイティブアプリケーションのスクリプトを作成する場合は、そのアプリケーション用の追加のダイアログXMLファイルも作成する必要があります。 AppMonが使用するすべてのネイティブアプリケーションには、ダイアログXMLファイルを1つだけ追加する必要があります。 不要なダイアログボックスが期待されない場合でも、追加のダイアログXMLファイルが必要です。 追加のダイアログボックスには、その要素が単なるプレー `window` スホルダーである場合でも、少なくとも1 `window` つの要素が必要です。

>[!NOTE]
>
>この場合、additionalという用語は、 `appmon.[applicationname].addition.[locale]`.xmlファイルの内容を意味します。 このようなファイルは、ダイアログXMLファイルへの上書きと追加を指定します。

また、次の目的で、ネイティブアプリケーション用の追加のダイアログXMLファイルを変更することもできます。

* 別の応答を持つアプリケーションのダイアログXMLファイルを上書きするには
* ダイアログXMLファイル内で指定されていない応答をそのアプリケーションのダイアログボックスに追加するには

追加のdialogXMLファイルを識別するファイル名はです `appmon.[appname].addition.[locale].xml`。 例えば、appmon.excel.addition.en_US.xmlなどです。

追加のダイアログXMLファイルの名前は、形式を使用する必要があり `appmon.[applicationname].addition.[locale].xml`ます。 *applicationnameは* 、XML設定ファイルおよびスクリプトで使用されるアプリケーション名と完全に一致する必要があります。

>[!NOTE]
>
>native2pdfconfig.xml設定ファイルで指定された汎用アプリケーションには、プライマリダイアログXMLファイルがありません。 このような仕 [様については、「ネイティブファイル形式のサポートの追加と変更](converting-file-formats-pdf.md#adding-or-modifying-support-for-a-native-file-format) 」の節で説明しています。

要素内の子とし `windowList` て表示される要素を並べ替える必要があ `window` ります。 (window要素とwindowList [要素の順序付けを参照](converting-file-formats-pdf.md#ordering-the-window-and-windowlist-elements))。

### 一般ダイアログのXMLファイルの変更 {#modifying-the-general-dialog-xml-file}

一般的なダイアログXMLファイルを変更して、システムによって生成されたダイアログボックスに応答したり、複数のアプリケーションに共通するダイアログボックスに応答したりできます。

#### XML設定ファイルへのファイルタイプエントリの追加 {#adding-a-filetype-entry-in-the-xml-configuration-file}

この手順では、Generate PDFサービス設定ファイルを更新して、ファイルタイプをネイティブアプリケーションに関連付ける方法を説明します。 この設定ファイルを更新するには、管理コンソールを使用して設定データをファイルに書き出す必要があります。 設定データのデフォルトのファイル名は、native2pdfconfig.xmlです。

**Generate PDFサービス設定ファイルの更新**

1. ホーム **** /サービス **/** Adobe PDF Generator **/設定ファイル、設定ファイル、設定**********&#x200B;の書き出し設定を選択します。
1. 必要に応 `filetype-settings` じて、native2pdfconfig.xmlファイルの要素を変更します。
1. ホーム **** /サービス **/** Adobe PDF Generator **/設定ファイル、次に設定ファ**********&#x200B;イルの読み込み、設定ファイルの読み込みを選択します。 設定データがGenerate PDFサービスに読み込まれ、以前の設定と置き換えられます。

>[!NOTE]
>
>アプリケーションの名前は、要素の属性の値と `GenericApp` して指定され `name` ます。 この値は、そのアプリケーション用に開発するスクリプトで指定された、対応する名前と完全に一致する必要があります。 同様に、要素の属 `GenericApp` 性は、対応するス `displayName` クリプトのウィンドウのキャプションと完全に一致する必要 `expectedWindow` があります。 このような等価性は、または属性に表示される正規式を解決した後で `displayName` 評価さ `caption` れます。

この例では、Generate PDFサービスに付属のデフォルトの設定データを変更し、（Microsoft Wordではなく）メモ帳を使用してファイル名拡張子.txtのファイルを処理するように指定しています。 この変更前は、Microsoft Wordは、このようなファイルを処理するネイティブアプリケーションとして指定されていました。

**テキストファイルをメモ帳に転送するための変更(native2pdfconfig.xml)**

```as3
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

#### ネイティブ環境を検索するアプリケーション変数の作成 {#creating-an-environment-variable-to-locate-the-native-application}

ネイティブ環境の実行可能ファイルの場所を指定するアプリケーション変数を作成します。 この変数は、形式を使用する必要があ `[applicationname]_PATH`ります。 ** applicationnameは、XML設定ファイルおよびスクリプトで使用されるアプリケーション名と完全に一致し、パスには重複の引用符で囲まれた実行ファイルのパスが含まれている必要があります。 このような環境変数の例は、で `Photoshop_PATH`す。

新しい環境変数を作成したら、Generate PDFサービスをデプロイするサーバーを再起動する必要があります。

**Windows XPシステムでのシステム変数の作成環境**

1. コントロ **ールパネル/システムを選択しま**&#x200B;す。
1. [システムのプロパティ]ダイアログボックスで、[詳細]タブを **クリックし** 、[システム変数]を **環境します**。
1. [システム変数]ダイアログボックスの[環境変数]で、[新規]をクリ **ックしま**&#x200B;す。
1. New System Variableダイアログボックスの「 **Variable name** 」ボックスに、形式を使用する名前を入力します `[applicationname]_PATH`。
1. 「 **Variable value** 」ボックスに、アプリケーションの実行可能ファイルのフルパスとファイル名を入力し、「 **OK」をクリックします**。 For example, type: `c:\windows\Notepad.exe`
1. [環境変数]ダイアログボックスで、[ **OK**]をクリックします。

**コマンドラインからシステム変数を作成する**

1. コマンドラインウィンドウで、次の形式を使用して変数の定義を入力します。

   ```as3
            [applicationname]_PATH=[Full path name]
   ```

   For example, type: `NotePad_PATH=C:\WINDOWS\NOTEPAD.EXE`

1. 開始変数を有効にするための新しいコマンドラインプロンプト。

#### XMLファイル {#xml-files}

AEM FormsにはサンプルXMLファイルが含まれており、Generate PDFサービスでメモ帳を使用して、ファイル名拡張子.txtのファイルを処理します。 このコードは、この節に含まれています。 さらに、この節で説明するその他の変更を行う必要があります。

#### 追加のダイアログXMLファイル {#additional-dialog-xml-file}

次の例には、メモ帳アプリケーション用の追加のダイアログボックスが含まれています。 これらのダイアログボックスは、Generate PDFサービスで指定されたダイアログボックスに加えて使用できます。

**メモ帳ダイアログボックス(appmon.notepad.addition.en_US.xml)**

```as3
 <dialogs app="Notepad" locale="en_US" version="7.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="dialogs.xsd">
     <window caption="Caption Title">
         <windowList>
             <window className="Button" caption="OK" action="press"/>
         </windowList>
     </window>
 </dialogs>
```

#### スクリプトXMLファイル {#script-xml-file}

次の例は、Generate PDFサービスがメモ帳とやり取りし、Adobe PDFプリンターを使用してファイルを印刷する方法を指定します。

**メモ帳スクリプトのXMLファイル(appmon.notepad.script.en_US.xml)**

```as3
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

