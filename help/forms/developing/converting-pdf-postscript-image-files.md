---
title: PDFからPostscriptおよび画像ファイルへの変換
seo-title: PDFからPostscriptおよび画像ファイルへの変換
description: 'null'
seo-description: 'null'
uuid: 07da0391-7180-4197-aaa6-ae753d753b84
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: f8707752-2c83-461a-b83d-708754b0f3f6
translation-type: tm+mt
source-git-commit: f9389a06f9c2cd720919486765cee76257f272c3

---


# PDFからPostscriptおよび画像ファイルへの変換 {#converting-pdf-to-postscript-andimage-files}

**Convert PDFサービスについて**

Convert PDFサービスは、PDFドキュメントをPostScriptおよび様々な画像形式（JPEG、JPEG 2000、PNGおよびTIFF）に変換します。 PDF ドキュメントの PostScript への変換は、PostScript プリンターでの無人のサーバーベース印刷に便利です。PDF ドキュメントをサポートしていないコンテンツ管理システムでドキュメントをアーカイブする場合、PDF ドキュメントをマルチページ TIFF ファイルに変換する方法が実用的です。

Convert PDFサービスを使用して、次のタスクを実行できます。

* PDF ドキュメントを PostScript に変換します。
* PDF画像をドキュメント形式に変換します。

>[!NOTE]
>
>For more information about the Convert PDF service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Converting PDF Documents to PostScript {#converting-pdf-documents-to-postscript}

このトピックでは、Convert PDF Service API（JavaおよびWebサービス）を使用して、PDFドキュメントをPostScriptファイルにプログラム的に変換する方法について説明します。 PostScriptファイルに変換されるPDFドキュメントは、非インタラクティブPDFドキュメントです。 つまり、インタラクティブPDFドキュメントをPostScriptファイルに変換しようとすると、例外が発生します。

>[!NOTE]
>
>For more information about the Convert PDF service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary-of-steps}

PDFドキュメントをPostScriptファイルに変換するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Convert PDFサービスクライアントの作成を参照してください。
1. PDFドキュメントを参照して、PostScriptファイルに変換します。
1. 変換の実行時オプションを設定します。
1. PDFドキュメントをPostScriptファイルに変換します。
1. PostScriptファイルを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

**Convert PDFクライアントの作成**

プログラムによってConvert PDFサービス操作を実行する前に、Convert PDFサービスクライアントを作成する必要があります。 Java APIを使用している場合は、オブジェクトを作成し `ConvertPdfServiceClient` ます。 WebサービスAPIを使用している場合は、オブジェクトを作成 `ConvertPDFServiceService` します。

この節では、AEM Formsで導入されたWebサービス機能を使用します。 新しい機能にアクセスするには、属性を使用してプロキシオブジェクトを作成する必要が `lc_version` あります。 (「Webサービスを使用したAEM Formsの呼び出し」の「Webサ [ービスを使用した新機能へのアクセス](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)」を参照)。

**PDFドキュメントを参照してPostScriptファイルに変換**

PostScriptファイルに変換するPDFドキュメントを参照します。 このトピックで前述したように、PDFドキュメントは非インタラクティブPDFドキュメントです。 インタラクティブPDFドキュメントをPostScriptファイルに変換しようとすると、例外が発生します。

**変換の実行時オプションの設定**

PDFドキュメントをPostScriptファイルに変換する場合、作成するPostScriptの種類を指定する実行時オプションを定義できます。 例えば、レベル3のPostScriptファイルを定義できます。

通常、生成されるPostScriptファイルは、入力PDFファイルのサイズを反映したドキュメントです。 このオプションを `ShrinkToFit` 選択すると（ページに合わせてPostScriptファイルの出力が縮小されます）、入力PDFドキュメントと生成されたPostScriptファイルの間に違いは見られません。 このオ `ShrinkToFit` プションは、入力PDFオプションよりも小さいページサイズで印刷する場合にのみ有効になります。ドキュメント 小さいページサイズを選択するには、このオプションを定義 `PageSize` します。 また、正しいPostScript出力を取得するために、このオプ `RotateAndCenter` ションをに設 `true` 定することをお勧めします。

同様に、このオプションを選択すると( `ExpandToFit` PostScriptファイルの出力がページに合わせて拡大される)、入力PDFドキュメントよりも大きいページサイズで印刷するように選択した場合にのみ、このオプションが有効になります。 大きいページサイズを選択するには、このオプションを定義 `PageSize` します。 また、正しいPostScript出力を取得するために、このオプ `RotateAndCenter` ションをに設 `true` 定することをお勧めします。

>[!NOTE]
>
>設定できる実行時の値について詳しくは、『 `ToPSOptionsSpec` AEM Forms APIリファレンス』のクラス [参照を参照し](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)てください。

**PDFドキュメントのPostScriptファイルへの変換**

サービスクライアントを作成し、実行時オプションを設定したら、PostScript変換操作を呼び出すことができます。 この操作には、変換するドキュメントに関する情報（変換レベルの推奨PostScriptレベルなど）が必要です。ターゲットドキュメント

**PostScriptファイルの保存**

PDFドキュメントをPostScriptに変換した後、出力をPostScriptファイルとして保存できます。

**関連トピック**

[Java APIを使用したPDFドキュメントのPSへの変換](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-java-api)

[WebサービスAPIを使用してPDFドキュメントをPSに変換する](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Convert PDFサービスAPIのクイック開始](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Java APIを使用したPDFドキュメントのPSへの変換 {#convert-a-pdf-document-to-ps-using-the-java-api}

Convert PDF Service API(Java)を使用してPDFドキュメントをPostScriptに変換します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-convertpdf-client.jarなどのクライアントJARファイルを含めます。

1. Convert PDFクライアントの作成を参照してください。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `ConvertPdfServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. PDFドキュメントを参照して、PostScriptファイルに変換します。

   * コンストラク `java.io.FileInputStream` ターを使用してオブジェクトを作成し、変換するPDFドキュメントの場所を指定するstring値を渡します。
   * コンストラク `com.adobe.idp.Document` ターを使用して、PDFドキュメントを格納するオブジェクトを作成 `com.adobe.idp.Document` します。 PDFを含むオ `java.io.FileInputStream` ブジェクトを渡します。ドキュメント

1. 変換の実行時オプションを設定します。

   * Create a `ToPSOptionsSpec` object by invoking its constructor.
   * オブジェクトに属する適切なメソッドを呼び出して、実行時のオプションを設定 `ToPSOptionsSpec` します。 例えば、作成されるPostScriptレベルを定義するには、オブジェクトのメソッ `ToPSOptionsSpec` ドを呼び出 `setPsLevel` し、PostScriptレベルを指定する `PSLevel` 定義済みリスト値を渡します。 設定できるすべての実行時の値について詳しくは、『 `ToPSOptionsSpec` AEM Forms APIリファレンス』のクラス [参照を参照し](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)てください。

1. PDFドキュメントをPostScriptファイルに変換します。

   オブジェクト `ConvertPdfServiceClient`のメソッドを `toPS2` 呼び出し、次の値を渡します。

   * PostScriptフ `com.adobe.idp.Document` ァイルに変換するPDFドキュメントを表すオブジェクトです。
   * PostScriptの実 `ToPSOptionsSpec` 行時オプションを指定するオブジェクトです。
   このメソ `toPS2` ッドは、新しいPostScript `Document` メソッドを含むオブジェクトを返します。ドキュメント

1. PostScriptファイルを保存します。

   * Create a `java.io.File` object and ensure that the file name extension is .ps.
   * オブジェクト `Document` のメソッ `copyToFile` ドを呼び出して、オブジェクトの内容をファイルにコピ `Document` ーします(メソッドから返されたオブジェクトを使用 `Document` していることを `toPS2` 確認します)。

**関連トピック**

[手順の概要](converting-pdf-postscript-image-files.md#summary-of-steps)

[クイック開始（SOAPモード）:Java APIを使用したPDFドキュメントのPostScriptへの変換](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-postscript-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用してPDFドキュメントをPSに変換する {#convert-a-pdf-document-to-ps-using-the-web-service-api}

Convert PDF Service API（Webサービス）を使用してPDFドキュメントをPostScriptに変換します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. Convert PDFクライアントの作成を参照してください。

   * Create a `ConvertPdfServiceClient` object by using its default constructor.
   * Create a `ConvertPdfServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLを指定するstring値をAEM Formsサービス(例： `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`.)に渡します。属性を使用する必要はありま `lc_version` せん。 ただし、を指定しま `?blob=mtom`す。
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得して、オブジェクトを作成 `ConvertPdfServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のオプションを実行して、基本的なHTTP認証を有効にします。タスク

      * AEM formsのユーザー名をフィールドに割り当てま `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `ConvertPdfServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールドに `HttpClientCredentialType.Basic` 割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールドに `BasicHttpSecurityMode.TransportCredentialOnly` 割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. PDFドキュメントを参照して、PostScriptファイルに変換します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、PostScriptファイルに変換されたPDFドキュメントの保存に使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、変換するPDFドキュメントーのファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * オブジェクトの内容を格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得す `System.IO.FileStream` ることで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイ `System.IO.FileStream` ト配列、開始位 `Read` 置およびストリームの長さを渡すことで、バイト配列にストリームデータを入力します。
   * バイト配列の `BLOB` 内容をフィールドに割り `MTOM` 当てて、オブジェクトを入力します。

1. 変換の実行時オプションを設定します。

   * Create a `ToPSOptionsSpec` object by invoking its constructor.
   * オブジェクトのデータメンバーに値を割り当てて、実行時 `ToPSOptionsSpec` のオプションを設定します。 例えば、作成されるPostScriptレベルを定義するには、オブジェクトのデ `PSLevel` ータメンバーに `ToPSOptionsSpec` 定義済みリスト `psLevel` 値を割り当てます。

1. PDFドキュメントをPostScriptファイルに変換します。

   オブジェクト `GeneratePDFServiceService` のメソッドを `toPS2` 呼び出し、次の値を渡します。

   * PostScriptフ `BLOB` ァイルに変換するPDFドキュメントを表すオブジェクトです。
   * 実行時 `ToPSOptionsSpec` のオプションを指定するオブジェクト
   変換が完了したら、オブジェクトのプロパティにアクセスして、PostScriptドキュメントを表すバイナリデ `BLOB` ータを抽出 `MTOM` します。 PostScriptファイルに書き出し可能なバイト配列を返します。

1. PostScriptファイルを保存します。

   * Create a `System.IO.FileStream` object by invoking its constructor. PSファイルのファイルの場所を表すstring値を渡します。
   * メソッドによって返されたオブジェクトのデータ内容を `BLOB` 格納するバイト配列を作成 `encryptPDFUsingPassword` します。 オブジェクトのフィールドの値を取得して、バ `BLOB` イト配列を設定 `MTOM` します。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡して、バイ `System.IO.BinaryWriter` ト配列の内 `Write` 容をPostScriptファイルに書き込みます。

**関連トピック**

[手順の概要](converting-pdf-postscript-image-files.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## PDF画像からドキュメント形式への変換 {#converting-pdf-documents-to-image-formats}

Convert PDFサービスを使用すると、PDFドキュメントをJPEG、JPEG 2000、TIFFおよびPNGなどの画像形式にプログラム的に変換できます。 PDF画像を画像ファイルにドキュメントすることで、PDFドキュメントを画像ファイルとして使用できます。 例えば、画像をエンタープライズコンテンツ管理システムに配置してストレージできます。

PDFドキュメントを画像に変換する場合、Convert PDFサービスは画像内の各ページに対して個別の画像を作成します。ドキュメント つまり、ドキュメントのページ数が20ページの場合、Convert PDFサービスは20個の画像ファイルを作成します。 PDFドキュメントを画像形式に変換する場合、PDFドキュメント内の各ページの個々の画像を作成するか、PDFドキュメント全体の単一の画像ファイルを作成できます。

>[!NOTE]
>
>For more information about the Convert PDF service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-1}

PDFドキュメントをサポートされている任意の種類に変換するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Convert PDFサービスクライアントの作成を参照してください。
1. 変換するPDFドキュメントを取得します。
1. 実行時オプションを設定します。
1. PDFを画像に変換します。
1. コレクションから画像ファイルを取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

**Convert PDFクライアントの作成**

プログラムによってConvert PDFサービス操作を実行する前に、Convert PDFサービスクライアントを作成する必要があります。 Java APIを使用している場合は、オブジェクトを作成し `ConvertPdfServiceClient` ます。 WebサービスAPIを使用している場合は、オブジェクトを作成 `ConvertPDFServiceService` します。

**変換するPDFドキュメントの取得**

画像に変換するPDFドキュメントを取得する必要があります。 インタラクティブPDF画像を画像にドキュメントすることはできません。 これを行うと、例外が発生します。 インタラクティブPDFドキュメントを画像ファイルに変換するには、変換前にPDFドキュメントを統合する必要があります。 (PDFドキュメント [の統合](/help/forms/developing/creating-document-output-streams.md#flattening-pdf-documents)を参照)。

**実行時オプションの設定**

画像形式や解像度の値などの実行時のオプションを設定する必要があります。 ランタイム値について詳しくは、『 `ToImageOptionsSpec` AEM Forms APIリファレンス』のクラス [リファレンスを参](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)照してください。

**PDFを画像に変換**

サービスクライアントを作成し、実行時のオプションを設定したら、PDFドキュメントを画像に変換できます。 画像を含むコレクションオブジェクトが返されます。

**コレクションからの画像ファイルの取得**

Convert PDFサービスが返すコレクションオブジェクトから画像ファイルを取得できます。 コレクション内の各要素は、JPGフ `com.adobe.idp.Document` ァイルなどの画像フ `BLOB` ァイルとして保存できるインスタンス（Webサービスを使用している場合はインスタンス）です。

画像ファイルの形式は、実行時のオプションに `ImageConvertFormat` よって異なります。 つまり、「実行時」オプション `ImageConvertFormat` をに設定した場合は、画 `ImageConvertFormat.JPEG`像ファイルをJPGファイルとして保存できます。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Convert PDFサービスAPIのクイック開始](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Java APIを使用したPDFドキュメントの画像ファイルへの変換 {#convert-a-pdf-document-to-image-files-using-the-java-api}

Convert PDFサービスAPI(Java)を使用して、PDFドキュメントを画像形式に変換します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-convertpdf-client.jarなどのクライアントJARファイルを含めます。

1. Convert PDFクライアントの作成を参照してください。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `ConvertPdfServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 変換するPDFドキュメントを取得します。

   * コンストラ `java.io.FileInputStream` クターを使用し、PDFドキュメントーの場所を指定するstring値を渡して、変換するPDFドキュメントーを表すオブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 実行時オプションを設定します。

   * コンストラクタを使用して `ToImageOptionsSpec` オブジェクトを作成します。
   * 必要に応じて、このオブジェクトに属するメソッドを呼び出します。 例えば、メソッドを呼び出し、形式の種類を指 `setImageConvertFormat` 定する列挙値を渡 `ImageConvertFormat` して、イメージの種類を設定します。
   >[!NOTE]
   >
   >定義済みリスト値の設 `ImageConvertFormat` 定は必須です。

1. PDFを画像に変換します。

   オブジェクト `ConvertPdfServiceClient` のメソッドを `toImage2` 呼び出し、次の値を渡します。

   * 変換す `com.adobe.idp.Document` るPDFファイルを表すオブジェクトです。
   * 画像 `com.adobe.livecycle.converpdfservice.client.ToImageOptionsSpec` の画像形式に関する様々な環境設定を含むターゲット。
   このメソッ `toImage2` ドは、画像を含む `java.util.List` オブジェクトを返します。 コレクション内の各要素はインスタンス `com.adobe.idp.Document` です。

1. コレクションから画像ファイルを取得します。

   オブジェクトを繰り返し `java.util.List` 処理し、画像が存在するかどうかを判断します。 各要素はインスタンス `com.adobe.idp.Document` です。 オブジェクトのメソッドを呼び出し、 `com.adobe.idp.Document` オブジェクトを `copyToFile` 渡すことで、画像を保存 `java.io.File` します。

**関連トピック**

[クイック開始（SOAPモード）:Java APIを使用したPDFドキュメントからJPEGファイルへの変換](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-jpeg-files-using-the-java-api)

### WebサービスAPIを使用してPDFドキュメントを画像ファイルに変換する {#convert-a-pdf-document-to-image-files-using-the-web-service-api}

Convert PDF Service API（Webサービス）を使用して、PDFドキュメントを画像形式に変換します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. 変換PDFクライアントを作成します。

   * Create a `ConvertPdfServiceClient` object by using its default constructor.
   * Create a `ConvertPdfServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLを指定するstring値をAEM Formsサービス(例： `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`.)に渡します。属性を使用する必要はありま `lc_version` せん。 ただし、を指定しま `?blob=mtom`す。
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得して、オブジェクトを作成 `ConvertPdfServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のオプションを実行して、基本的なHTTP認証を有効にします。タスク

      * AEM formsのユーザー名をフィールドに割り当てま `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `ConvertPdfServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールドに `HttpClientCredentialType.Basic` 割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールドに `BasicHttpSecurityMode.TransportCredentialOnly` 割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. 変換するPDFドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、PDFフォームの保存に使用されます。
   * Create a `System.IO.FileStream` object by invoking its constructor. PDFフォームの場所とファイルを開くモードを指定するstring値を渡します。
   * オブジェクトの内容を格納するバイト配列を作成 `System.IO.FileStream` します。 オブジェクトのプロパティを取得して、バイト配列 `System.IO.FileStream` のサイズを決定 `Length` します。
   * オブジェクトのメソッドを呼び出して、バイト配列にストリ `System.IO.FileStream` ームデータを入力 `Read` します。 読み取るバイト配列、開始位置およびストリーム長を渡します。
   * バイト配列 `BLOB` の内容をフィールドに割り `MTOM` 当てて、オブジェクトを入力します。

1. 実行時オプションを設定します。

   * コンストラクタを使用して `ToImageOptionsSpec` オブジェクトを作成します。
   * 必要に応じて、このオブジェクトに属するメソッドを呼び出します。 例えば、メソッドを呼び出し、形式の種類を指 `setImageConvertFormat` 定する `ImageConvertFormat` 定義済みリスト値を渡して、画像の種類を設定します。
   >[!NOTE]
   >
   >定義済みリスト値の設 `ImageConvertFormat` 定は必須です。

1. PDFを画像に変換します。

   オブジェクト `ConvertPDFServiceService` のメソッドを `toImage2` 呼び出し、次の値を渡します。

   * 変換す `BLOB` るファイルを表すオブジェクトです。
   * 画像 `ToImageOptionsSpec` 形式に関する様々な環境設定を含むターゲット
   このメソ `toImage2` ッドは、新しく作 `MyArrayOfBLOB` 成された画像ファイルを含むオブジェクトを返します。

1. コレクションから画像ファイルを取得します。

   * フィールドの値を取得して、オ `MyArrayOfBLOB` ブジェクト内の要素数を決定し `Count` ます。 各要素は、画像を含 `BLOB` むオブジェクトです。
   * オブジェクトを繰り返 `MyArrayOfBLOB` し処理し、各画像ファイルを保存します。

**関連トピック**

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
