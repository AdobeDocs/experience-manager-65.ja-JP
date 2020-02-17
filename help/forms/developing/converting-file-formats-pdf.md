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
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d

---


# ファイル形式とPDFの変換 {#converting-between-file-formatsand-pdf}

**Generate PDFサービスについて**

Generate PDF サービスは、ネイティブファイル形式を PDF に変換します。また、PDF を他のファイル形式に変換し、PDF ドキュメントのサイズを最適化します。

Generate PDF サービスは、以下のファイル形式を PDF に変換する際にネイティブアプリケーションを使用します。特に説明がない限り、これらのアプリケーションはドイツ語版、フランス語版、英語版および日本語版のみサポートされています。*Windowsのみ* 、Windows Server® 2003およびWindows Server 2008のみがサポートされていることを示します。

* DOC、DOCX、RTF、TXT、XLS、XLSX、PPT、PPTX、VSD、MPP、MPPX、XPS、PUBの変換用のMicrosoft Office 2003および2007（Windowsのみ）

   **注意**:Microsoft XPS形式をPDFに変換するには、Acrobat® 9.2以降が必要です。*

* DWF、DWG、DXWを変換するAutodesk autoCAD 2005、2006、2007、2008、2009（英語のみ）
* Corel wordPerfect 12およびX4:WPD、QPW、SHWの変換（英語のみ）
* OpenOffice 2.0、2.4、3.0.1および3.1:ODT、ODP、ODG、ODF、SXW、SXI、SXC、SXD、DOC、DOCX、RTF、TXT、XLS、XLSX、PPT、pptx、VSD、MPP、MPPXおよびPUB

   ***注意&#x200B;**:Generate PDFサービスは64ビットバージョンのOpenOfficeをサポートしていません。*

* PSDを変換するAdobe Photoshop® CS2（Windowsのみ）

   ***注意**:Photoshop CS3およびCS4は、Windows Server 2003またはWindows Server 2008をサポートしていないので、サポートされていません。*

* FMを変換するAdobe FrameMaker® 7.2および8（Windowsのみ）
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
* PDF/A-1b（DeviceRGBカラースペースのみを使用）

Generate PDF サービスを使用するには、以下の管理タスクを実行する必要があります。

* 必要なネイティブアプリケーションを、AEM Forms をホストするコンピューター上にインストールする
* AEM formsをホストするコンピューターにAdobe Acrobat ProfessionalまたはAcrobat Pro Extended 9.2をインストールします。
* インストール後のセットアップタスクを実行する

これらのタスクは、『AEM formsの自動インストールおよびデプロイ（JBoss版）』で説明されています。

Generate PDFサービスを使用して、次のタスクを実行できます。

* ネイティブファイル形式からPDFに変換します。
* HTMLドキュメントをPDFドキュメントに変換します。
* PDFドキュメントをファイル形式に変換します。

>[!NOTE]
>
>For more information about the Generate PDF service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Word文書のPDF文書への変換 {#converting-word-documents-to-pdf-documents}

ここでは、Generate PDF APIを使用して、Microsoft wordドキュメントをPDFドキュメントにプログラム的に変換する方法について説明します。

>[!NOTE]
>
>その他のファイル形式の詳細については、「追加のネイティブフ [ァイル形式に対するサポートの追加」を参照してくださ](converting-file-formats-pdf.md#adding-support-for-additional-native-file-formats)い。

>[!NOTE]
>
>For more information about the Generate PDF service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary-of-steps}

Microsoft wordドキュメントをPDFドキュメントに変換するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Generate PDFクライアントを作成します。
1. PDFドキュメントに変換するファイルを取得します。
1. ファイルをPDFドキュメントに変換します。
1. 結果を取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

**Generate PDFクライアントの作成**

プログラムで「Generate PDF」操作を実行する前に、Generate PDFサービスクライアントを作成します。 Java APIを使用している場合は、オブジェクトを作成し `GeneratePdfServiceClient` ます。 WebサービスAPIを使用している場合は、オブジェクトを作成 `GeneratePDFServiceService` します。

**PDFドキュメントに変換するファイルの取得**

PDFドキュメントに変換するMicrosoft wordドキュメントを取得します。

**ファイルをPDFドキュメントに変換**

Generate PDFサービスクライアントを作成した後、このメソッドを呼び出すことがで `createPDF2` きます。 このメソッドには、変換するドキュメントに関する情報（ファイル拡張子を含む）が必要です。

**結果の取得**

ファイルがPDFドキュメントに変換された後、結果を取得できます。 例えば、WordファイルをPDFドキュメントに変換した後、PDFドキュメントを取得して保存できます。

**関連トピック**

[Java APIを使用したWord文書のPDF文書への変換](converting-file-formats-pdf.md#convert-word-documents-to-pdf-documents-using-the-java-api)

[WebサービスAPIを使用したWord文書のPDFドキュメントへの変換](converting-file-formats-pdf.md#convert-word-documents-to-pdf-documents-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Generate PDFサービスAPIクイックスタート](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### Java APIを使用したWord文書のPDF文書への変換 {#convert-word-documents-to-pdf-documents-using-the-java-api}

Generate PDF API(Java)を使用してMicrosoft word文書をPDF文書に変換します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-generatepdf-client.jarなどのクライアントJARファイルを含めます。

1. Generate PDFクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `GeneratePdfServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. PDFドキュメントに変換するファイルを取得します。

   * 変換するWord `java.io.FileInputStream` ファイルを表すオブジェクトを、コンストラクタを使用して作成します。 ファイルの場所を指定するstring値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. ファイルをPDFドキュメントに変換します。

   オブジェクトのメソッドを呼び出し、次の値を `GeneratePdfServiceClient` 渡して、ファ `createPDF2` イルをPDFドキュメントに変換します。

   * A `com.adobe.idp.Document` object that represents the file to convert.
   * ファイル `java.lang.String` 拡張子を含むオブジェクトです。
   * 変換に `java.lang.String` 使用されるファイルタイプ設定を含むオブジェクトです。 ファイルタイプの設定では、.docや.xlsなど、異なるファイルタイプに対する変換設定を指定します。
   * 使用 `java.lang.String` するPDF設定の名前を含むオブジェクトです。 例えば、を指定できます `Standard`。
   * 使用 `java.lang.String` するセキュリティ設定の名前を含むオブジェクトです。
   * PDFドキュメント `com.adobe.idp.Document` の生成時に適用される設定を含むオプションのオブジェクトです。
   * PDFドキュメント `com.adobe.idp.Document` に適用されるメタデータ情報を含むオプションのオブジェクトです。
   このメ `createPDF2` ソッドは、新し `CreatePDFResult` いPDFドキュメントとログ情報を含むオブジェクトを返します。 通常、ログファイルには、変換要求によって生成されたエラーメッセージまたは警告メッセージが含まれます。

1. 結果を取得します。

   PDFドキュメントを取得するには、次の操作を実行します。

   * オブジェクト `CreatePDFResult` のメソッドを呼び出 `getCreatedDocument` し、オブジェクトを返 `com.adobe.idp.Document` します。
   * オブジェクト `com.adobe.idp.Document` のメソッドを呼 `copyToFile` び出して、前の手順で作成したオブジェクトからPDFドキュメントを抽出します。
   この方法を使用してログ `createPDF2` ドキュメントを取得した場合（HTML変換には適用できません）、次の操作を実行します。

   * オブジェクト `CreatePDFResult` のメソッドを呼び出 `getLogDocument` します。 オブジェクトを返 `com.adobe.idp.Document` します。
   * オブジェクト `com.adobe.idp.Document` のメソッドを呼び `copyToFile` 出して、ログドキュメントを抽出します。


**関連トピック**

[手順の概要](converting-file-formats-pdf.md#summary-of-steps)

[クイックスタート（SOAPモード）:Java APIを使用したMicrosoft word文書のPDF文書への変換](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-a-microsoft-word-document-to-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したWord文書のPDFドキュメントへの変換 {#convert-word-documents-to-pdf-documents-using-the-web-service-api}

Generate PDF API（Webサービス）を使用してMicrosoft wordドキュメントをPDFドキュメントに変換します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. Generate PDFクライアントを作成します。

   * Create a `GeneratePDFServiceClient` object by using its default constructor.
   * Create a `GeneratePDFServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLを指定するstring値をAEM Formsサービスに渡します(例 `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`:)。属性を使用する必要はありま `lc_version` せん。 ただし、を指定しま `?blob=mtom`す。
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `GeneratePDFServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `GeneratePDFServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. PDFドキュメントに変換するファイルを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、PDFドキュメントに変換するファイルを保存するために使用されます。
   * Create a `System.IO.FileStream` object by invoking its constructor. 変換するファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイト配列、開 `System.IO.FileStream` 始位置、ストリ `Read` ーム長を渡すことによって、バイト配列にストリームデータを設定します。
   * オブジェクト `BLOB` にバイト配列の内容をプロパ `MTOM` ティに割り当てて、オブジェクトを設定します。

1. ファイルをPDFドキュメントに変換します。

   オブジェクトのメソッドを呼び出し、次の値を `GeneratePDFServiceService` 渡して、ファ `CreatePDF2` イルをPDFドキュメントに変換します。

   * 変換す `BLOB` るファイルを表すオブジェクトです。
   * ファイル拡張子を含む文字列。
   * 変換に `java.lang.String` 使用されるファイルタイプ設定を含むオブジェクトです。 ファイルタイプの設定では、.docや.xlsなど、異なるファイルタイプに対する変換設定を指定します。
   * 使用するPDF設定を含むstringオブジェクトです。 You can specify `Standard`.
   * 使用するセキュリティ設定を含むstringオブジェクトです。 You can specify `No Security`.
   * PDFドキュメント `BLOB` の生成時に適用される設定を含むオプションのオブジェクトです。
   * PDFドキュメント `BLOB` に適用されるメタデータ情報を含むオプションのオブジェクトです。
   * メソッドによって設定さ `BLOB` れるタイプの出力パラメー `CreatePDF2` ター。 このメソッ `CreatePDF2` ドは、変換されたドキュメントをこのオブジェクトに入力します。 （このパラメーター値はWebサービスの呼び出しにのみ必要です）。
   * メソッドによって設定さ `BLOB` れるタイプの出力パラメー `CreatePDF2` ター。 メソッド `CreatePDF2` は、このオブジェクトにログドキュメントを入力します。 （このパラメーター値はWebサービスの呼び出しにのみ必要です）。

1. 結果を取得します。

   * オブジェクトのフィールドをバイト配列に割り当て `BLOB` て、変換済みPDF `MTOM` ドキュメントを取得します。 バイト配列は、変換されたPDFドキュメントを表します。 メソッドの出力パラ `BLOB` メーターとして使用するオブジェクトを必ず使用してく `createPDF2` ださい。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、変換されたPDFドキュメントのファイルの場所を表すstring値を渡します。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡すことで、バ `System.IO.BinaryWriter` イト配列の内 `Write` 容をPDFファイルに書き込みます。

**関連トピック**

[手順の概要](converting-file-formats-pdf.md#summary-of-steps)

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## HTMLドキュメントのPDFドキュメントへの変換 {#converting-html-documents-to-pdf-documents}

ここでは、Generate PDF APIを使用して、HTMLドキュメントをPDFドキュメントにプログラム的に変換する方法について説明します。

>[!NOTE]
>
>For more information about the Generate PDF service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-1}

HTMLドキュメントをPDFドキュメントに変換するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Generate PDFクライアントを作成します。
1. PDFドキュメントに変換するHTMLコンテンツを取得します。
1. HTMLコンテンツをPDFドキュメントに変換します。
1. 結果を取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

**Generate PDFクライアントの作成**

プログラムで「Generate PDF」操作を実行する前に、Generate PDFサービスクライアントを作成する必要があります。 Java APIを使用している場合は、オブジェクトを作成し `GeneratePdfServiceClient` ます。 WebサービスAPIを使用している場合は、を作成しま `GeneratePDFServiceService`す。

**PDFドキュメントに変換するHTMLコンテンツの取得**

PDFドキュメントに変換するHTMLコンテンツを参照します。 HTMLファイルなどのHTMLコンテンツや、URLを使用してアクセス可能なHTMLコンテンツを参照できます。

**HTMLコンテンツのPDFドキュメントへの変換**

サービスクライアントを作成した後、適切なPDF作成操作を呼び出すことができます。 この操作には、変換対象のドキュメントへのパスなど、変換対象のドキュメントに関する情報が必要です。

**結果の取得**

HTMLコンテンツがPDFドキュメントに変換された後、結果を取得してPDFドキュメントを保存できます。

**関連トピック**

[Java APIを使用したHTMLコンテンツのPDFドキュメントへの変換](converting-file-formats-pdf.md#convert-html-content-to-a-pdf-document-using-the-java-api)

[WebサービスAPIを使用したHTMLコンテンツのPDFドキュメントへの変換](converting-file-formats-pdf.md#convert-html-content-to-a-pdf-document-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Generate PDFサービスAPIクイックスタート](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### Java APIを使用したHTMLコンテンツのPDFドキュメントへの変換 {#convert-html-content-to-a-pdf-document-using-the-java-api}

Generate PDF API(Java)を使用してHTMLドキュメントをPDFドキュメントに変換します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-generatepdf-client.jarなどのクライアントJARファイルを含めます。

1. Generate PDFクライアントを作成します。

   コンストラク `GeneratePdfServiceClient` ターを使用し、接続プロパティを含むオブジェクトを渡 `ServiceClientFactory` して、オブジェクトを作成します。

1. PDFドキュメントに変換するHTMLコンテンツを取得します。

   文字列変数を作成し、HTMLコンテンツを指すURLを割り当てて、HTMLコンテンツを取得します。

1. HTMLコンテンツをPDFドキュメントに変換します。

   オブジェクト `GeneratePdfServiceClient` のメソッドを `htmlToPDF2` 呼び出し、次の値を渡します。

   * 変換 `java.lang.String` するHTMLファイルのURLを含むオブジェクトです。
   * 変換に `java.lang.String` 使用されるファイルタイプ設定を含むオブジェクトです。 ファイルタイプ設定にはスパイダリングレベルを含めることができます。
   * 使用 `java.lang.String` するセキュリティ設定の名前を含むオブジェクトです。
   * PDFドキュメント `com.adobe.idp.Document` の生成時に適用される設定を含むオプションのオブジェクトです。 この情報を指定しない場合、設定は前の3つのパラメーターに基づいて自動的に選択されます。
   * PDFドキュメント `com.adobe.idp.Document` に適用されるメタデータ情報を含むオプションのオブジェクトです。

1. 結果を取得します。

   生成さ `htmlToPDF2` れた新しいPDFド `HtmlToPdfResult` キュメントを含むオブジェクトを返します。 新しく作成したPDFドキュメントを取得するには、次の操作を実行します。

   * オブジェクト `HtmlToPdfResult` のメソッドを呼び出 `getCreatedDocument` します。 オブジェクトを返 `com.adobe.idp.Document` します。
   * オブジェクト `com.adobe.idp.Document` のメソッドを呼 `copyToFile` び出して、前の手順で作成したオブジェクトからPDFドキュメントを抽出します。

**関連トピック**

[HTMLドキュメントのPDFドキュメントへの変換](converting-file-formats-pdf.md#converting-html-documents-to-pdf-documents)

[クイックスタート（SOAPモード）:Java APIを使用したHTMLコンテンツのPDFドキュメントへの変換](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[クイックスタート（SOAPモード）:Java APIを使用したHTMLコンテンツのPDFドキュメントへの変換](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したHTMLコンテンツのPDFドキュメントへの変換 {#convert-html-content-to-a-pdf-document-using-the-web-service-api}

Generate PDF API（Webサービス）を使用してHTMLコンテンツをPDFドキュメントに変換します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. Generate PDFクライアントを作成します。

   * Create a `GeneratePDFServiceClient` object by using its default constructor.
   * Create a `GeneratePDFServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLを指定するstring値をAEM Formsサービスに渡します(例 `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`:)。属性を使用する必要はありま `lc_version` せん。 ただし、を指定しま `?blob=mtom`す。
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `GeneratePDFServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `GeneratePDFServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. PDFドキュメントに変換するHTMLコンテンツを取得します。

   文字列変数を作成し、HTMLコンテンツを指すURLを割り当てて、HTMLコンテンツを取得します。

1. HTMLコンテンツをPDFドキュメントに変換します。

   オブジェクトのメソッドを呼び出し、次の値を渡して、HTML `GeneratePDFServiceService` コンテンツをPDF `HtmlToPDF2` ドキュメントに変換します。

   * 変換するHTMLコンテンツを含む文字列です。
   * 変換に `java.lang.String` 使用されるファイルタイプ設定を含むオブジェクトです。
   * 使用するセキュリティ設定を含むstringオブジェクトです。
   * PDFドキュメント `BLOB` の生成時に適用される設定を含むオプションのオブジェクトです。
   * PDFドキュメント `BLOB` に適用されるメタデータ情報を含むオプションのオブジェクトです。
   * メソッドによって設定さ `BLOB` れるタイプの出力パラメー `CreatePDF2` ター。 このメソッ `CreatePDF2` ドは、変換されたドキュメントをこのオブジェクトに入力します。 （このパラメーター値はWebサービスの呼び出しにのみ必要です）。

1. 結果を取得します。

   * オブジェクトのフィールドをバイト配列に割り当て `BLOB` て、変換済みPDF `MTOM` ドキュメントを取得します。 バイト配列は、変換されたPDFドキュメントを表します。 メソッドの出力パラ `BLOB` メーターとして使用するオブジェクトを必ず使用してく `HtmlToPDF2` ださい。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、変換されたPDFドキュメントのファイルの場所を表すstring値を渡します。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡すことで、バ `System.IO.BinaryWriter` イト配列の内 `Write` 容をPDFファイルに書き込みます。

**関連トピック**

[HTMLドキュメントのPDFドキュメントへの変換](converting-file-formats-pdf.md#converting-html-documents-to-pdf-documents)

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## PDFドキュメントの画像以外の形式への変換 {#converting-pdf-documents-to-non-image-formats}

ここでは、Generate PDF Java APIおよびWebサービスAPIを使用して、PDFドキュメントをRTFファイル（画像以外の形式の例）にプログラム的に変換する方法について説明します。 その他の画像以外の形式には、HTML、テキスト、DOC、EPSがあります。 PDFドキュメントをRTFに変換する場合は、PDFドキュメントに送信ボタンなどのフォーム要素が含まれていないことを確認します。 フォーム要素は変換されません。

>[!NOTE]
>
>For more information about the Generate PDF service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-2}

PDFドキュメントをサポートされている任意の種類に変換するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Generate PDFクライアントを作成します。
1. 変換するPDFドキュメントを取得します。
1. PDFドキュメントを変換します。
1. 変換したファイルを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

**Generate PDFクライアントの作成**

プログラムで「Generate PDF」操作を実行する前に、Generate PDFサービスクライアントを作成する必要があります。 Java APIを使用している場合は、オブジェクトを作成し `GeneratePdfServiceClient` ます。 WebサービスAPIを使用している場合は、オブジェクトを作成 `GeneratePDFServiceService` します。

**変換するPDFドキュメントの取得**

画像以外の形式に変換するPDFドキュメントを取得します。

**PDFドキュメントの変換**

サービスクライアントを作成したら、PDF書き出し操作を呼び出すことができます。 この操作には、変換対象のドキュメントへのパスなど、変換対象のドキュメントに関する情報が必要です。

**変換したファイルを保存**

変換したファイルを保存します。 例えば、PDFドキュメントをRTFファイルに変換する場合は、変換したドキュメントをRTFファイルに保存します。

**関連トピック**

[Java APIを使用したPDFドキュメントのRTFファイルへの変換](converting-file-formats-pdf.md#convert-a-pdf-document-to-a-rtf-file-using-the-java-api)

[WebサービスAPIを使用したPDFドキュメントのRTFファイルへの変換](converting-file-formats-pdf.md#convert-a-pdf-document-to-a-rtf-file-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Generate PDFサービスAPIクイックスタート](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### Java APIを使用したPDFドキュメントのRTFファイルへの変換 {#convert-a-pdf-document-to-a-rtf-file-using-the-java-api}

Generate PDF API(Java)を使用してPDFドキュメントをRTFファイルに変換します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-generatepdf-client.jarなどのクライアントJARファイルを含めます。

1. Generate PDFクライアントを作成します。

   コンストラク `GeneratePdfServiceClient` ターを使用し、接続プロパティを含むオブジェクトを渡 `ServiceClientFactory` して、オブジェクトを作成します。

1. 変換するPDFドキュメントを取得します。

   * コンストラクタ `java.io.FileInputStream` ーを使用して、変換するPDFドキュメントを表すオブジェクトを作成します。 PDFドキュメントの場所を指定するstring値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PDFドキュメントを変換します。

   オブジェクト `GeneratePdfServiceClient` のメソッドを `exportPDF2` 呼び出し、次の値を渡します。

   * 変換す `com.adobe.idp.Document` るPDFファイルを表すオブジェクトです。
   * 変換 `java.lang.String` するファイルの名前を含むオブジェクトです。
   * Adobe PDF `java.lang.String` 設定の名前を含むオブジェクトです。
   * 変換の `ConvertPDFFormatType` 対象となるファイルの種類を指定するオブジェクトです。
   * PDFドキュメント `com.adobe.idp.Document` の生成時に適用される設定を含むオプションのオブジェクトです。
   このメソ `exportPDF2` ッドは、変換されたフ `ExportPDFResult` ァイルを含むオブジェクトを返します。

1. PDFドキュメントを変換します。

   新しく作成したファイルを取得するには、次の操作を実行します。

   * オブジェクト `ExportPDFResult` のメソッドを呼び出 `getConvertedDocument` します。 オブジェクトを返 `com.adobe.idp.Document` します。
   * オブジェクト `com.adobe.idp.Document` のメソッドを呼び `copyToFile` 出して、新しいドキュメントを抽出します。

**関連トピック**

[手順の概要](converting-file-formats-pdf.md#summary-of-steps)

[クイックスタート（SOAPモード）:Java APIを使用したHTMLコンテンツのPDFドキュメントへの変換](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したPDFドキュメントのRTFファイルへの変換 {#convert-a-pdf-document-to-a-rtf-file-using-the-web-service-api}

Generate PDF API（Webサービス）を使用してPDFドキュメントをRTFファイルに変換します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. Generate PDFfクライアントを作成します。

   * Create a `GeneratePDFServiceClient` object by using its default constructor.
   * Create a `GeneratePDFServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLを指定するstring値をAEM Formsサービスに渡します(例 `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`:)。属性を使用する必要はありま `lc_version` せん。 ただし、を指定しま `?blob=mtom`す。
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `GeneratePDFServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `GeneratePDFServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. 変換するPDFドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、変換されたPDFドキュメントの保存に使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、PDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイト配列、開 `System.IO.FileStream` 始位置、ストリ `Read` ーム長を渡すことによって、バイト配列にストリームデータを設定します。
   * オブジェクト `BLOB` にバイト配列の内容をプロパ `MTOM` ティに割り当てて、オブジェクトを設定します。

1. PDFドキュメントを変換します。

   オブジェクト `GeneratePDFServiceServiceWse` のメソッドを `ExportPDF2` 呼び出し、次の値を渡します。

   * 変換す `BLOB` るPDFファイルを表すオブジェクトです。
   * 変換するファイルのパス名を含む文字列です。
   * ファイ `java.lang.String` ルの場所を指定するオブジェクトです。
   * 変換の対象となるファイルの種類を指定するstringオブジェクトです。 Specify `RTF`.
   * PDFドキュメント `BLOB` の生成時に適用される設定を含むオプションのオブジェクトです。
   * メソッドによって設定さ `BLOB` れるタイプの出力パラメー `ExportPDF2` ター。 このメソッ `ExportPDF2` ドは、変換されたドキュメントをこのオブジェクトに入力します。 （このパラメーター値はWebサービスの呼び出しにのみ必要です）。

1. 変換したファイルを保存します。

   * 変換されたRTFドキュメントを取得するには、オブジェクトの `BLOB` フィールドをバ `MTOM` イト配列に割り当てます。 バイト配列は、変換されたRTFドキュメントを表します。 メソッドの出力パラ `BLOB` メーターとして使用するオブジェクトを必ず使用してく `ExportPDF2` ださい。
   * Create a `System.IO.FileStream` object by invoking its constructor. RTFファイルの場所を表すstring値を渡します。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡して、バイト配列の `System.IO.BinaryWriter` 内容をRTFフ `Write` ァイルに書き込みます。

**関連トピック**

[手順の概要](converting-file-formats-pdf.md#summary-of-steps)

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 追加のネイティブファイル形式のサポートの追加 {#adding-support-for-additional-native-file-formats}

この節では、追加のネイティブファイル形式に対するサポートを追加する方法について説明します。 このサービスでネイティブファイル形式をPDFに変換する際に使用される、Generate PDFサービスとネイティブアプリケーション間のインタラクションの概要を示します。

この節では、以下についても説明します。

* この製品でネイティブファイル形式をPDFに変換する際に既に使用されているネイティブアプリケーションに対するGenerate PDFサービスの応答を変更する方法
* Generate PDFサービス、Generate PDFサービスのApplication Monitor(AppMon)コンポーネント、およびMicrosoft wordなどのネイティブアプリケーション間のインタラクション
* XMLグラマーがインタラクションで果たす役割

### コンポーネントの操作 {#component-interactions}

Generate PDFサービスは、ファイル形式に関連付けられたアプリケーションを呼び出してネイティブファイル形式を変換し、アプリケーションとやり取りして、デフォルトのプリンターを使用してドキュメントを印刷します。 デフォルトのプリンターは、Adobe PDFプリンターとして設定する必要があります。

次の図は、ネイティブアプリケーションのサポートに関連するコンポーネントとドライバーを示しています。 また、インタラクションに影響を与えるXMLグラマーについても説明します。

ネイティブファイル変換のコンポーネントのインタラクション

このドキュメントでは、ネイティブ *アプリケーション* （Microsoft wordなど）のネイティブファイル形式の作成に使用するアプリケーションを示します。

*AppMonは* 、ユーザーがそのアプリケーションで表示されるダイアログボックス内を移動するのと同じ方法でネイティブアプリケーションとやり取りするエンタープライズコンポーネントです。 AppMonがMicrosoft wordなどのアプリケーションにファイルを開いて印刷するよう指示するために使用するXMLグラマーには、次の順次タスクが含まれます。

1. ファイル/開くを選択してファイルを開く
1. Openダイアログボックスが表示されることを確認します。そうでない場合は、エラーの処理
1. 「ファイル名」フィールドにファイル名を指定し、「開く」ボタンをクリックします
1. ファイルを実際に開くこと
1. ファイル/印刷を選択して、印刷ダイアログボックスを開く
1. 印刷ダイアログボックスが表示されることを確認します

AppMonは、標準のWin32 APIを使用して、キーストロークやマウスクリックなどのUIイベントを転送するためにサードパーティアプリケーションとやり取りします。これらのアプリケーションを制御してPDFファイルを生成するのに役立ちます。

これらのWin32 APIの制限により、AppMonは、フローティングメニューバー（TextPadなどの一部のアプリケーションで使用）や、Win32 APIを使用してコンテンツを取得できない特定の種類のダイアログなど、特定の種類のウィンドウにこれらのUIイベントを送出できません。

フローティングメニューバーを視覚的に見分けるのは簡単です。ただし、特別な種類のダイアログは、視覚検査だけでは特定できない場合があります。 AppMonが標準のWin32 APIを使用してAppMonとやり取りできるかどうかを判断するダイアログを調べるには、Microsoft Spy++（Microsoft Visual C++開発環境の一部）や同等のWinID( [https://www.dennisbabkin.com/php/download.php?what=WinID](https://www.dennisbabkin.com/php/download.php?what=WinID))などのサードパーティアプリケーションが必要です。

WinIDがテキスト、サブウィンドウ、ウィンドウクラスIDなどのダイアログコンテンツを抽出できる場合、AppMonも同様に機能します。

次の表に、ネイティブファイル形式の印刷に使用される情報の種類を示します。

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
   <td><p>PDF設定、セキュリティ設定、ファイルタイプ設定が含まれます。 </p><p>ファイルタイプ設定では、ファイル名拡張子が対応するネイティブアプリケーションに関連付けられます。 また、ファイルタイプ設定では、ネイティブファイルの印刷に使用するネイティブアプリケーション設定も指定します。 </p></td>
   <td><p>既にサポートされているネイティブアプリケーションの設定を変更するには、システム管理者が管理コンソールで「ファイルタイプ設定」を設定します。 </p><p>新しいネイティブファイル形式のサポートを追加するには、ファイルを手動で編集する必要があります。 (ネイティブ <a href="converting-file-formats-pdf.md#adding-or-modifying-support-for-a-native-file-format">ファイル形式のサポートの追加または変更を参照</a>)。 </p></td>
  </tr>
  <tr>
   <td><p>スクリプト </p></td>
   <td><p>Generate PDFサービスとネイティブアプリケーションとの間のインタラクションを指定します。 このような操作を行うと、通常、アプリケーションはAdobe PDFドライバーにファイルを印刷するように指示されます。 </p><p>スクリプトには、ネイティブアプリケーションに特定のダイアログボックスを開くよう指示し、これらのダイアログボックスのフィールドとボタンに特定の応答を提供する手順が含まれています。 </p></td>
   <td><p>Generate PDFサービスには、サポートされるすべてのネイティブアプリケーション用のスクリプトファイルが含まれます。 これらのファイルは、XML編集アプリケーションを使用して変更できます。</p><p>新しいネイティブアプリケーションのサポートを追加するには、新しいスクリプトファイルを作成する必要があります。 (ネイティブ <a href="converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application">アプリケーション用の追加のダイアログXMLファイルの作成または変更を参照</a>)。 </p></td>
  </tr>
  <tr>
   <td><p>汎用ダイアログボックスの説明 </p></td>
   <td><p>複数のアプリケーションに共通のダイアログボックスに対する応答方法を指定します。 このようなダイアログボックスは、オペレーティングシステム、ヘルパーアプリケーション（PDFMakerなど）およびドライバーによって生成されます。 </p><p>この情報を含むファイルは、appmon.global.en_US.xmlです。</p></td>
   <td><p>このファイルは変更しないでください。 </p></td>
  </tr>
  <tr>
   <td><p>アプリケーション固有のダイアログボックスの手順</p></td>
   <td><p>アプリケーション固有のダイアログボックスに対する応答方法を指定します。 </p><p>この情報を含むファイルはappmonです。<i>[appname]</i>.dialog.<i>[locale]</i>.xml（例：appmon.word.en_US.xml）。</p></td>
   <td><p>このファイルは変更しないでください。 </p><p>新しいネイティブアプリケーション用のダイアログボックスの手順を追加するには、 <a href="converting-file-formats-pdf.md#creating_or_modifying_an_additional_dialog_xml_file_for_a_native_application">ネイティブアプリケーション用の追加のダイアログXMLファイルの作成または変更を参照してくださ</a>い。</p></td>
  </tr>
  <tr>
   <td><p>その他のアプリケーション固有のダイアログボックスの手順 </p></td>
   <td><p>アプリケーション固有のダイアログボックスの手順に対する上書きと追加を指定します。 この節では、このような情報の例を示します。 </p><p>この情報を含むファイルはappmonです。<i>[appname]</i>.addition.<i>[locale]</i>.xml. 例えば、appmon.addition.en_US.xmlなどです。</p></td>
   <td><p>この種類のファイルは、XML編集アプリケーションを使用して作成および変更できます。 (ネイティブ <a href="converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application">アプリケーション用の追加のダイアログXMLファイルの作成または変更を参照</a>)。 </p><p><strong>重要</strong>:サーバーがサポートするネイティブアプリケーションごとに、アプリケーション固有のダイアログボックスの追加の手順を作成する必要があります。 </p></td>
  </tr>
 </tbody>
</table>

### スクリプトとダイアログのXMLファイルについて {#about-the-script-and-dialog-xml-files}

スクリプトXMLファイルは、ユーザーがアプリケーションダイアログボックスを操作するのと同じ方法で、Generate PDFサービスにアプリケーションダイアログボックス間を移動するよう指示します。 また、スクリプトXMLファイルは、ボタンの押下、チェックボックスの選択/選択解除、メニュー項目の選択などの操作を実行して、Generate PDFサービスにダイアログボックスに応答するよう指示します。

これに対し、ダイアログXMLファイルは、スクリプトXMLファイルで使用されるのと同じタイプのアクションを持つダイアログボックスに応答するだけです。

#### ダイアログボックスとウィンドウ要素の用語 {#dialog-box-and-window-element-terminology}

この節と次の節では、説明するパースペクティブに応じて、ダイアログボックスとそれらに含まれるコンポーネントに対して異なる用語を使用します。 ダイアログボックスのコンポーネントは、ボタン、フィールド、コンボボックスなどの項目です。

この節と次節では、ユーザの視点からダイアログボックスとそのコンポーネントについて説明する場合、 *dialog box*、 *button* field **、 *combo box、* combo box usedなどの用語が使用されます。

この節と次の節で、内部表現の観点からダイアログボックスとそのコンポーネントについて説明する場合、「 *window」要素* 。 ウィンドウ要素の内部表現は階層で、各ウィンドウ要素のインスタンスはラベルで識別されます。 ウィンドウ要素インスタンスは、その物理的な特性と動作も記述します。

ユーザーの視点から見ると、ダイアログボックスとそのコンポーネントは異なる動作を示し、一部のダイアログボックス要素はアクティブ化されるまで非表示になります。 内部表現の観点からは、そのような動作の問題は存在しません。 例えば、ダイアログボックスの内部表現は、ダイアログボックス内にネストされている点を除いて、そのダイアログボックスに含まれるコンポーネントの内部表現と似ています。

ここでは、AppMonに手順を提供するXML要素について説明します。 これらの要素には、要素や要素な `dialog` どの名前が付けら `window` れます。 このドキュメントでは、XML要素を区別するために等幅フォントを使用します。 この要 `dialog` 素は、XMLスクリプトファイルが意図的または意図せずに表示される原因となる可能性のあるダイアログボックスを識別します。 この要 `window` 素は、ウィンドウ要素（ダイアログボックスまたはダイアログボックスのコンポーネント）を識別します。

#### 階層 {#hierarchy}

次の図に、スクリプトとダイアログのXMLの階層を示します。 スクリプトXMLファイルは、script.xsdスキーマに準拠しており、このスキーマにはwindow.xsdスキーマが含まれています（XMLの意味で）。 同様に、ダイアログXMLファイルは、dialogs.xsdスキーマに準拠しており、このスキーマにもwindow.xsdスキーマが含まれています。

![as_as_xml_hierarchy](assets/as_as_xml_hierarchy.png)

スクリプトとダイアログのXMLの階層

#### スクリプトXMLファイル {#script-xml-files}

スクリ *プトXMLファイルは* 、ネイティブアプリケーションが特定のウィンドウ要素に移動し、それらの要素に応答を提供するように指示する一連の手順を指定します。 ほとんどの応答は、対応するダイアログボックスのフィールド、コンボボックス、またはボタンにユーザーが入力するテキストまたはキーストロークです。

Generate PDFサービスでスクリプトXMLファイルをサポートする目的は、ネイティブアプリケーションにネイティブファイルを印刷させることです。 ただし、スクリプトXMLファイルは、ネイティブアプリケーションのダイアログボックスとの対話操作時にユーザーが実行できる任意のタスクを実行するために使用できます。

スクリプトXMLファイル内の手順は、分岐の機会なしに順番に実行されます。 唯一の条件付きテストはタイムアウト/再試行に対してサポートされ、特定の期間内および指定の再試行回数の後に手順が正常に完了しなかった場合にスクリプトが終了します。

順次的なステップに加えて、ステップ内の命令も順に実行されます。 手順と手順が、ユーザーが同じ手順を実行する順序を反映していることを確認する必要があります。

スクリプトXMLファイルの各手順は、手順の手順が正常に実行された場合に表示されると予想されるウィンドウ要素を識別します。 スクリプト手順の実行中に予期しないダイアログボックスが表示された場合、Generate PDFサービスは、次の節で説明するようにダイアログXMLファイルを検索します。

#### ダイアログXMLファイル {#dialog-xml-files}

ネイティブアプリケーションを実行すると、表示モードと非表示モードのどちらであるかに関係なく、異なるダイアログボックスが表示されます。 ダイアログボックスは、オペレーティングシステムによって生成されるか、アプリケーション自体によって生成されます。 ネイティブアプリケーションがGenerate PDFサービスの制御下で実行されている場合、システムおよびネイティブアプリケーションのダイアログボックスが非表示ウィンドウに表示されます。

ダイア *ログXMLファイルは* 、Generate PDFサービスがシステムまたはネイティブのアプリケーションダイアログボックスに対してどのように応答するかを指定します。 ダイアログXMLファイルを使用すると、Generate PDFサービスは、変換プロセスを容易にする方法で、要求されないダイアログボックスに応答できます。

現在実行中のスクリプトXMLファイルで処理されないダイアログボックスがシステムまたはネイティブアプリケーションに表示された場合、Generate PDFサービスは、ダイアログXMLファイルを次の順序で検索し、一致が見つかると停止します。

* appmon *[appname]*.additional.*[locale]*.xml
* appmon *[appname].[locale]*.xml （このファイルは変更しないでください。）
* appmon.global.*[locale]*.xml （このファイルは変更しないでください。）

Generate PDFサービスは、ダイアログボックスに一致するものを見つけた場合、そのダイアログボックスに対して指定されたキーストロークまたは他のアクションを送信して、ダイアログボックスを閉じます。 ダイアログボックスの指示で中止メッセージを指定した場合、Generate PDFサービスは現在実行中のジョブを終了し、エラーメッセージを生成します。 このような中止メッセージは、スクリプトXML文法の `abortMessage` 要素で指定されます。

Generate PDFサービスで、前述のファイルのいずれにも記述されていないダイアログボックスが検出された場合、Generate PDFサービスは、そのダイアログボックスのキャプションをログファイルエントリに組み込みます。 現在実行中のジョブは、最終的にタイムアウトになります。 その後、ログファイル内の情報を使用して、ネイティブアプリケーション用の追加のダイアログXMLファイルに新しい命令を作成できます。

### ネイティブファイル形式のサポートの追加または変更 {#adding-or-modifying-support-for-a-native-file-format}

この節では、他のネイティブファイル形式をサポートするため、または既にサポートされているネイティブファイル形式のサポートを変更するために実行する必要があるタスクについて説明します。

サポートを追加または変更する前に、次のタスクを実行する必要があります。

#### ウィンドウ要素を識別するツールの選択 {#choosing-a-tool-for-identifying-window-elements}

ダイアログおよびスクリプトのXMLファイルでは、ダイアログまたはスクリプト要素が応答するウィンドウ要素（ダイアログボックス、フィールド、またはその他のダイアログコンポーネント）を指定する必要があります。 例えば、スクリプトがネイティブアプリケーションのメニューを呼び出した後、スクリプトはキーストロークまたはアクションを適用するメニュー上のウィンドウ要素を識別する必要があります。

ダイアログボックスは、タイトルバーに表示されるキャプションによって簡単に識別できます。 ただし、Microsoft Spy++などのツールを使用して、下位レベルのウィンドウ要素を識別する必要があります。 下位レベルのウィンドウ要素は、明らかではない様々な属性を使用して識別できます。 また、各ネイティブアプリケーションでウィンドウ要素が異なって識別される場合があります。 その結果、ウィンドウ要素を識別する複数の方法があります。 ウィンドウ要素の識別を考慮するための推奨順序を次に示します。

1. 一意の場合のキャプション自体
1. コントロールID（特定のダイアログボックスに対して一意である場合とそうでない場合があります）
1. クラス名。一意である場合とそうでない場合があります。

これらの3つの属性のいずれかまたは組み合わせを使用して、ウィンドウを識別できます。

属性がキャプションを識別できない場合は、親に対するインデックスを使用してウィンドウ要素を識別できます。 インデ *ックスは* 、兄弟ウィンドウ要素を基準としたウィンドウ要素の位置を指定します。 多くの場合、コンボボックスを識別する唯一の方法はインデックスです。

次の問題に注意してください。

* Microsoft Spy++は、キャプションをアンパサンド(&amp;)を使用してキャプションのホットキーを識別して表示します。 例えば、Spy++は、1つの印刷ダイアログボックスのキャプションを表示します。これは、ホ `Pri&nt`ットキーがnであることを示 *します*。 スクリプトおよびダイアログのXMLファイルのキャプションタイトルでは、アンパサンドを省略する必要があります。
* 一部のキャプションには改行が含まれます。 generate PDFサービスは改行を識別できません。 キャプションに改行が含まれる場合は、キャプションを他のメニュー項目と区別するのに十分な量含め、省略した部分に正規表現を使用します。 An example is ( `^Long caption title$`).]. (キャプショ [ン属性での正規表現の使用を参照](converting-file-formats-pdf.md#using-regular-expressions-in-caption-attributes))。
* 予約されたXML文字には、文字エンティティ（エスケープシーケンスとも呼ばれます）を使用します。 例えば、アンパサン `&` ド、より小さい `<` 記号とより `>` 大きい記号、アポストロフィ、引用符 `&apos;` には、を `&quot;` 使用します。

ダイアログまたはスクリプトXMLファイルを操作する場合は、Microsoft Spy++アプリケーションをインストールする必要があります。

#### ダイアログファイルとスクリプトファイルのパッケージ解除 {#unpackaging-the-dialog-and-script-files}

ダイアログファイルとスクリプトファイルは、appmondata.jarファイルに格納されています。 これらのファイルを変更したり、新しいスクリプトやダイアログファイルを追加したりする前に、このJARファイルのパッケージを解除する必要があります。 例えば、EditPlusアプリケーションのサポートを追加するとします。 2つのXMLファイル（appmon.editplus.script.en_US.xmlおよびappmon.editplus.script.addition.en_US.xml）を作成します。 次に示すように、これらのXMLスクリプトは、adobe-appmondata.jarファイルの2か所に追加する必要があります。

* adobe-livecycle-native-jboss-x86_win32.ear > adobe-Native2PDFSvc.war\WEB-INF\lib > adobe-native.jar > Native2PDFSvc-native.jar\bin > adobe-appmondata.jar\com\adobe\appmon adobe-livecycle-native-jboss-x86_win32.earファイルは、次の場所にあるexportフォルダーにあります `[AEM forms install directory]\configurationManager`。 （AEM formsを別のJ2EEアプリケーションサーバーにデプロイする場合は、adobe-livecycle-native-jboss-x86_win32.earファイルを、ご使用のJ2EEアプリケーションサーバーに対応するEARファイルに置き換えます）。
* adobe-generatepdf-dsc.jar/adobe-appmondata.jar\com\adobe\appmon （adobe-appmondata.jarファイルは、adobe-generatepdf-dsc.jarファイル内にあります）。 adobe-generatepdf-dsc.jarファイルは、 *[AEM formsのinstall directory]*\deployフォルダーにあります。

これらのXMLファイルをadobe-appmondata.jarファイルに追加した後、GeneratePDFコンポーネントを再デプロイする必要があります。 adobe-appmondata.jarファイルにダイアログおよびスクリプトXMLファイルを追加するには、次のタスクを実行します。

1. WinZipやWinRARなどのツールを使用して、adobe-livecycle-native-jboss-x86_win32.earfile > adobe-Native2PDFSvc.war\WEB-INF\lib > adobe-native.jar > Native2PDFSvc-native.jar\bin > adobe-appmondata.jarファイルを開きます。
1. ダイアログおよびスクリプトXMLファイルをappmondata.jarファイルに追加するか、このファイル内の既存のXMLファイルを変更します。 (ネイティブ [アプリケーション用のスクリプトXMLファイルの作成または変更お](converting-file-formats-pdf.md#creating-or-modifying-a-script-xml-file-for-a-native-application)よびネ [イティブアプリケーション用の追加のダイアログXMLファイルの作成または変更を参照](converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application))。
1. WinZipやWinRARなどのツールを使用して、adobe-generatepdf-dsc.jar/adobe-appmondata.jarを開きます。
1. ダイアログおよびスクリプトXMLファイルをappmondata.jarファイルに追加するか、このファイル内の既存のXMLファイルを変更します。 (ネイティブ [アプリケーション用のスクリプトXMLファイルの作成または変更お](converting-file-formats-pdf.md#creating-or-modifying-a-script-xml-file-for-a-native-application)よびネ [イティブアプリケーション用の追加のダイアログXMLファイルの作成または変更を参照](converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application))。XMLファイルをadobe-appmondata.jarファイルに追加した後、新しいadobe-appmondata.jarファイルをadobe-generatepdf-dsc.jarファイルに配置します。
1. 追加のネイティブファイル形式のサポートを追加した場合は、アプリケーションのパスを提供するシステム環境変数を作成します(ネイティブアプリケーションを検索するための [環境変数の作成を参照](converting-file-formats-pdf.md#creating-an-environment-variable-to-locate-the-native-application))。

**GeneratePDFコンポーネントを再デプロイするには**

1. Workbenchにログインします。
1. Select **Window** > **Show Views** > **Components**. この操作により、コンポーネントビューがWorkbenchに追加されます。
1. GeneratePDFコンポーネントを右クリックし、「Stop Component」を **選択します**。
1. コンポーネントが停止したら、右クリックし、「Uninstall Component」を選択してコンポーネントを削除します。
1. Right-click the **Components** icon and select **Install Component**.
1. 変更したadobe-generatepdf-dsc.jarファイルを参照して選択し、「開く」をクリックします。 GeneratePDFコンポーネントの横に赤い四角が表示されます。
1. GeneratePDFコンポーネントを展開し、「サービス記述子」を選択して、「GeneratePDFService」を右クリックし、「サービスをアクティブ化」を選択します。
1. 表示される設定ダイアログボックスで、適切な設定値を入力します。 これらの値を空白のままにすると、デフォルトの設定値が使用されます。
1. 「GeneratePDF」を右クリックし、「Start Component」を選択します。
1. 「Active Services」を展開します。 サービス名が実行されている場合は、その横に緑色の矢印が表示されます。 それ以外の場合、サービスは停止状態にあります。
1. サービスが停止状態の場合は、サービス名を右クリックし、「Start Service」を選択します。

### ネイティブアプリケーション用のスクリプトXMLファイルの作成または変更 {#creating-or-modifying-a-script-xml-file-for-a-native-application}

ファイルを新しいネイティブアプリケーションに転送する場合は、そのアプリケーション用のスクリプトXMLファイルを作成する必要があります。 既にサポートされているネイティブアプリケーションとGenerate PDFサービスとのやり取りを変更する場合は、そのアプリケーションのスクリプトを変更する必要があります。

スクリプトには、ネイティブアプリケーションのウィンドウ要素間を移動し、それらの要素に対して特定の応答を提供する手順が含まれています。 この情報を含むファイルはappmonです。*[appname]*.script.*[locale]*.xml. 例えば、appmon.notepad.script.en_US.xmlなどです。

#### スクリプトが実行する必要のある手順の識別 {#identifying-steps-the-script-must-execute}

ネイティブアプリケーションを使用して、移動する必要のあるウィンドウ要素と、ドキュメントを印刷するために実行する必要のある各応答を決定します。 任意の応答から生じるダイアログボックスに注目してください。 手順は次の手順に似ています。

1. ファイル／開くを選択します。
1. パスを指定し、「開く」をクリックします。
1. メニューバーでファイル/印刷を選択します。
1. プリンターに必要なプロパティを指定します。
1. 「印刷」を選択し、名前を付けて保存ダイアログボックスが表示されるまで待ちます。 Generate PDFサービスでPDFファイルの保存先を指定するには、Save asダイアログボックスが必要です。

#### キャプション属性で指定されたダイアログの識別 {#identifying-the-dialogs-specified-in-caption-attributes}

Microsoft Spy++を使用して、ネイティブアプリケーションのウィンドウ要素プロパティのIDを取得します。 スクリプトを作成するには、これらのIDが必要です。

#### キャプション属性での正規表現の使用 {#using-regular-expressions-in-caption-attributes}

キャプションの指定には正規表現を使用できます。 Generate PDFサービスは、このクラスを使用し `java.util.regex.Matcher` て正規表現をサポートします。 このユーティリティは、で説明する正規表現をサポートしま `java.util.regex.Pattern`す。 (JavaのWebサイト(https://java.sun.com/j2se/1.4.2/docs/api/java/util/regex/Pattern.html [)にアクセス](https://java.sun.com/j2se/1.4.2/docs/api/java/util/regex/Pattern.html)。)

**メモ帳バナーのメモ帳に先頭に付加されるファイル名を格納する正規表現**

```as3
 <!-- The regular expression ".*Notepad" means any number of non-terminating characters followed by Notepad. -->
 <step>
     <expectedWindow>
         <window caption=".*Notepad"/>
     </expectedWindow>
 </step>
```

**印刷と印刷設定を区別する正規表現**

```as3
 <!-- This regular expression differentiates the Print dialog box from the Print Setup dialog box. The "^" specifies the beginning of the line, and the "$" specifies the end of the line. -->
 <windowList>
     <window controlID="0x01" caption="^Print$" action="press"/>
 </windowList>
```

#### window要素とwindowList要素の順序付け {#ordering-the-window-and-windowlist-elements}

要素と要素は、次のよ `window` うに並べ `windowList` 替える必要があります。

* 複数の要 `window` 素が1つまたは複数の要素の子として表示され `windowList` る場合は、 `dialog` それらの要素の順番を降順に並べ、名前の長さ `window``caption` は順序内の位置を示します。
* 要素内に複数 `windowList` の要素が表示され `window` る場合、最初の要素の属性の長さで順序内の位置を示し、 `windowList` それらの要素を降順 `caption``indexes/`に並べます。

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

以前はサポートされていなかったネイティブアプリケーションのスクリプトを作成する場合は、そのアプリケーション用に追加のダイアログXMLファイルも作成する必要があります。 AppMonで使用されるすべてのネイティブアプリケーションには、ダイアログXMLファイルが1つだけ追加されている必要があります。 未承諾のダイアログボックスが必要な場合でも、追加のダイアログXMLファイルが必要です。 追加のダイアログボックスには、その要素が単なるプレースホル `window` ダーであっても、少なくとも1つ `window` の要素が必要です。

>[!NOTE]
>
>この場合、「追加」とはアプリの内容を意味します。[applicationname].addition.[locale].xmlファイル。 このようなファイルは、ダイアログXMLファイルへの上書きと追加を指定します。

ネイティブアプリケーション用の追加のダイアログXMLファイルは、次の目的で変更することもできます。

* 別の応答を持つアプリケーションのダイアログXMLファイルを上書きするには
* そのアプリケーションのダイアログXMLファイルで指定されていないダイアログボックスに応答を追加するには

追加のdialogXMLファイルを識別するファイル名はappmonです。*[appname]*.addition.*[locale]*.xml. 例えば、appmon.excel.addition.en_US.xmlなどがあります。

追加のダイアログXMLファイルの名前は、appmonの形式を使用する必要があります。*[applicationname]*.addition.*[locale]*.xml。ここで、 *applicationnameは* 、XML設定ファイルおよびスクリプトで使用されるアプリケーション名と完全に一致する必要があります。

>[!NOTE]
>
>native2pdfconfig.xml設定ファイルで指定された汎用アプリケーションには、プライマリダイアログXMLファイルがありません。 このような仕 [様については、「ネイティブファイル形式のサポートの追加](converting-file-formats-pdf.md#adding-or-modifying-support-for-a-native-file-format) /変更」の節を参照してください。

要素内の子とし `windowList` て表示される要素の順序を指定する必要があ `window` ります。 (window要素と [windowList要素の順序を参照](converting-file-formats-pdf.md#ordering-the-window-and-windowlist-elements))。

### 一般ダイアログXMLファイルの変更 {#modifying-the-general-dialog-xml-file}

一般的なダイアログXMLファイルを変更して、システムによって生成されたダイアログボックスに応答したり、複数のアプリケーションに共通するダイアログボックスに応答したりできます。

#### XML設定ファイルへのファイルタイプエントリの追加 {#adding-a-filetype-entry-in-the-xml-configuration-file}

この手順では、Generate PDFサービス設定ファイルを更新して、ファイルタイプをネイティブアプリケーションに関連付ける方法を説明します。 この設定ファイルを更新するには、管理コンソールを使用して設定データをファイルに書き出す必要があります。 設定データのデフォルトのファイル名は、native2pdfconfig.xmlです。

**Generate PDFサービス設定ファイルの更新**

1. **Services** /Adobe PDF Generator **/Configuration Files** 、Export Configuration Home ************&#x200B;の順に選択します。
1. 必要に応じ `filetype-settings` て、native2pdfconfig.xmlファイルの要素を変更します。
1. **Services** /Adobe PDF Generator **/** Configuration Files **/********** Configuration Filesを選択し、Configuration Home Importを選択します。 設定データがGenerate PDFサービスに読み込まれ、以前の設定は置き換えられます。

>[!NOTE]
>
>アプリケーションの名前は、要素の属性の値と `GenericApp` して指定し `name` ます。 この値は、そのアプリケーション用に開発するスクリプトで指定された、対応する名前と完全に一致する必要があります。 同様に、要素の属 `GenericApp` 性は、対応するス `displayName` クリプトのウィンドウキャプションと完全に一致する必要 `expectedWindow` があります。 このような等価性は、またはの属性に表示される正規表現を解決した後で `displayName` 評価さ `caption` れます。

この例では、Generate PDFサービスに付属するデフォルトの設定データが、ファイル名拡張子.txtのファイルを処理する際にメモ帳（Microsoft wordではなく）を使用するように変更されています。 この変更前は、Microsoft wordは、そのようなファイルを処理するネイティブアプリケーションとして指定されていました。

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

#### ネイティブアプリケーションを検索するための環境変数の作成 {#creating-an-environment-variable-to-locate-the-native-application}

ネイティブアプリケーション実行可能ファイルの場所を指定する環境変数を作成します。 この変数は、applicationname *[_PATHの形式を使用する必要があります。]*** applicationnameは、XML設定ファイルおよびスクリプトで使用されるアプリケーション名と完全に一致し、パスには実行可能ファイルのパスが二重引用符で囲まれている必要があります。 このような環境変数の例を次に示します `Photoshop_PATH`。

新しい環境変数を作成した後、Generate PDFサービスをデプロイするサーバーを再起動する必要があります。

**Windows XP環境でのシステム変数の作成**

1. コントロ **ールパネル/システムを選択しま**&#x200B;す。
1. [システムプロパティ]ダイアログボックスで、[詳細設定]タブを **クリックし** 、[環境変数]を **クリックします**。
1. Environment Variablesダイアログボックスの「System Variables」で、「 **New」をクリックします**。
1. 「New System Variable」ダイアログ・ボックスの「 **Variable name** 」ボックスに、applicationname *[]*_PATHという形式を使用する名前を入力します。
1. 「 **Variable value** 」ボックスに、アプリケーションの実行可能ファイルのフルパスとファイル名を入力し、「 **OK」をクリックします**。 For example, type: `c:\windows\Notepad.exe`
1. Environment Variablesダイアログボックスで、「 **OK」をクリックします**。

**コマンドラインからシステム変数を作成する**

1. コマンドラインウィンドウで、次の形式を使用して変数定義を入力します。

   ```as3
            [applicationname]_PATH=[Full path name]
   ```

   For example, type: `NotePad_PATH=C:\WINDOWS\NOTEPAD.EXE`

1. システム変数を有効にする新しいコマンドラインプロンプトを起動します。

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

**メモ帳スクリプトXMLファイル(appmon.notepad.script.en_US.xml)**

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

