---
title: PDFからPostscriptおよび画像ファイルへの変換
seo-title: PDFからPostscriptおよび画像ファイルへの変換
description: Convert PDFサービスを使用して、PDFドキュメントをPostScriptに、またJava APIとWeb Service APIを使用して様々な画像形式(JPEG、JPEG 2000、PNG、TIFF)に変換します。
seo-description: Convert PDFサービスを使用して、PDFドキュメントをPostScriptに、またJava APIとWeb Service APIを使用して様々な画像形式(JPEG、JPEG 2000、PNG、TIFF)に変換します。
uuid: 07da0391-7180-4197-aaa6-ae753d753b84
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: f8707752-2c83-461a-b83d-708754b0f3f6
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '2832'
ht-degree: 5%

---


# PDFからPostscriptおよび画像ファイルへの変換{#converting-pdf-to-postscript-andimage-files}

**Convert PDFサービスについて**

Convert PDFサービスは、PDFドキュメントをPostScriptおよび様々な画像形式（JPEG、JPEG 2000、PNGおよびTIFF）に変換します。 PDF ドキュメントの PostScript への変換は、PostScript プリンターでの無人のサーバーベース印刷に便利です。PDF ドキュメントをサポートしていないコンテンツ管理システムでドキュメントをアーカイブする場合、PDF ドキュメントをマルチページ TIFF ファイルに変換する方法が実用的です。

Convert PDFサービスを使用して、次のタスクを実行できます。

* PDF ドキュメントを PostScript に変換します。
* PDFドキュメントを画像形式に変換します。

>[!NOTE]
>
>Convert PDFサービスについて詳しくは、『[AEM Forms向けサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

## PDFドキュメントのPostScriptへの変換{#converting-pdf-documents-to-postscript}

このトピックでは、Convert PDF Service API（JavaおよびWebサービス）を使用して、PDFドキュメントをPostScriptファイルにプログラム的に変換する方法について説明します。 PostScriptファイルに変換されるPDFドキュメントは、非インタラクティブPDFドキュメントである必要があります。 つまり、インタラクティブPDFドキュメントをPostScriptファイルに変換しようとすると、例外が発生します。

>[!NOTE]
>
>Convert PDFサービスについて詳しくは、『[AEM Forms向けサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順{#summary-of-steps}の概要

PDFドキュメントをPostScriptファイルに変換するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Convert PDFサービスクライアントを作成します。
1. PDFドキュメントを参照して、PostScriptファイルに変換します。
1. 変換の実行時オプションを設定します。
1. PDFドキュメントをPostScriptファイルに変換します。
1. PostScriptファイルを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めてください。

**Convert PDFクライアントの作成**

プログラムでConvert PDFサービス操作を実行する前に、Convert PDFサービスクライアントを作成する必要があります。 Java APIを使用している場合は、`ConvertPdfServiceClient`オブジェクトを作成します。 WebサービスAPIを使用している場合は、`ConvertPDFServiceService`オブジェクトを作成します。

この節では、AEM Formsで導入されたWebサービス機能を使用します。 新しい機能にアクセスするには、`lc_version`属性を使用してプロキシオブジェクトを作成する必要があります。 (「[Webサービスを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)」の「Webサービスを使用した新しい機能へのアクセス」を参照)。

**PDFドキュメントを参照してPostScriptファイルに変換する**

PostScriptファイルに変換するPDFドキュメントを参照します。 このトピックで前述したように、PDFドキュメントは非インタラクティブPDFドキュメントである必要があります。 インタラクティブPDFドキュメントをPostScriptファイルに変換しようとすると、例外が発生します。

**変換の実行時オプションの設定**

PDFドキュメントをPostScriptファイルに変換する場合、作成されるPostScriptの種類を指定する実行時オプションを定義できます。 例えば、レベル3のPostScriptファイルを定義できます。

通常、生成されるPostScriptファイルは、入力PDFドキュメントのサイズを反映します。 `ShrinkToFit`オプションを選択すると（ページに合わせてPostScriptファイルの出力を縮小します）、入力PDFドキュメントと生成されたPostScriptファイルの間に違いは表示されません。 `ShrinkToFit`オプションは、入力PDFドキュメントよりも小さいページサイズで印刷するよう選択した場合にのみ有効になります。 小さいページサイズを選択するには、`PageSize`オプションを定義します。 また、正しいPostScript出力を取得するには、`RotateAndCenter`オプションを`true`に設定することをお勧めします。

同様に、`ExpandToFit`オプションを選択すると（PostScriptファイルの出力がページに合うように拡大されます）、入力PDFドキュメントよりも大きいページサイズで印刷することを選択した場合にのみ有効になります。 大きいページサイズを選択するには、`PageSize`オプションを定義します。 また、正しいPostScript出力を取得するには、`RotateAndCenter`オプションを`true`に設定することをお勧めします。

>[!NOTE]
>
>設定できる実行時の値について詳しくは、[AEM FormsAPIリファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)の`ToPSOptionsSpec`クラス参照を参照してください。

**PDFドキュメントのPostScriptファイルへの変換**

サービスクライアントを作成し、実行時オプションを設定した後で、PostScript変換操作を呼び出すことができます。 この操作には、ターゲットドキュメントに適したPostScriptレベルなど、変換するドキュメントに関する情報が必要です。

**PostScriptファイルの保存**

PDFドキュメントをPostScriptに変換した後、出力をPostScriptファイルとして保存できます。

**関連トピック**

[Java APIを使用したPDFドキュメントのPSへの変換](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-java-api)

[WebサービスAPIを使用してPDFドキュメントをPSに変換する](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Convert PDF Service APIクイック開始](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Java APIを使用したPDFドキュメントのPSへの変換{#convert-a-pdf-document-to-ps-using-the-java-api}

Convert PDF Service API(Java)を使用してPDFドキュメントをPostScriptに変換します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-convertpdf-client.jarなどのクライアントJARファイルを含めます。

1. Convert PDFクライアントの作成を参照してください。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `ConvertPdfServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. PDFドキュメントを参照して、PostScriptファイルに変換します。

   * コンストラクターを使用して`java.io.FileInputStream`オブジェクトを作成し、変換するPDFドキュメントの場所を指定する文字列値を渡します。
   * `com.adobe.idp.Document`コンストラクターを使用して、PDFドキュメントを格納する&lt;a0/>オブジェクトを作成します。 `com.adobe.idp.Document`PDFドキュメントを含む`java.io.FileInputStream`オブジェクトを渡します。

1. 変換の実行時オプションを設定します。

   * コンストラクターを呼び出して、`ToPSOptionsSpec`オブジェクトを作成します。
   * `ToPSOptionsSpec`オブジェクトに属する適切なメソッドを呼び出して、実行時のオプションを設定します。 例えば、作成されるPostScriptレベルを定義するには、`ToPSOptionsSpec`オブジェクトの`setPsLevel`メソッドを呼び出し、PostScriptレベルを指定する`PSLevel`定義済みリスト値を渡します。 設定できるすべての実行時の値について詳しくは、[AEM FormsAPIリファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)の`ToPSOptionsSpec`クラス参照を参照してください。

1. PDFドキュメントをPostScriptファイルに変換します。

   `ConvertPdfServiceClient`オブジェクトの`toPS2`メソッドを呼び出し、次の値を渡します。

   * PostScriptファイルに変換するPDFドキュメントを表す`com.adobe.idp.Document`オブジェクトです。
   * PostScriptの実行時オプションを指定する`ToPSOptionsSpec`オブジェクト。

   `toPS2`メソッドは、新しいPostScriptドキュメントを含む`Document`オブジェクトを返します。

1. PostScriptファイルを保存します。

   * `java.io.File`オブジェクトを作成し、ファイル名の拡張子が.psであることを確認します。
   * `Document`オブジェクトの`copyToFile`メソッドを呼び出して、`Document`オブジェクトの内容をファイルにコピーします（`toPS2`メソッドから返された`Document`オブジェクトを必ず使用してください）。

**関連トピック**

[手順の概要](converting-pdf-postscript-image-files.md#summary-of-steps)

[クイック開始（SOAPモード）:Java APIを使用したPDFドキュメントのPostScriptへの変換](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-postscript-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#convert-a-pdf-document-to-ps-using-the-web-service-api}を使用してPDFドキュメントをPSに変換する

Convert PDF Service API（Webサービス）を使用してPDFドキュメントをPostScriptに変換します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. Convert PDFクライアントの作成を参照してください。

   * `ConvertPdfServiceClient`オブジェクトを作成するには、そのデフォルトのコンストラクタを使用します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`ConvertPdfServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに指定するstring値を渡します（例：`http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`）。 `lc_version`属性を使用する必要はありません。 ただし、`?blob=mtom`を指定します。
   * `ConvertPdfServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * AEM formsユーザー名をフィールド`ConvertPdfServiceClient.ClientCredentials.UserName.UserName`に割り当てます。
      * 対応するパスワード値をフィールド`ConvertPdfServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * 定数値`HttpClientCredentialType.Basic`をフィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に割り当てます。
      * 定数値`BasicHttpSecurityMode.TransportCredentialOnly`をフィールド`BasicHttpBindingSecurity.Security.Mode`に割り当てます。

1. PDFドキュメントを参照して、PostScriptファイルに変換します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、PostScriptファイルに変換されたPDFドキュメントの保存に使用されます。
   * コンストラクターを呼び出し、変換するPDFドキュメントのファイルの場所と、ファイルを開くモードを表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得して、バイト配列のサイズを決定できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * `BLOB`オブジェクトに、`MTOM`フィールドにバイト配列の内容を割り当てて入力します。

1. 変換の実行時オプションを設定します。

   * コンストラクターを呼び出して、`ToPSOptionsSpec`オブジェクトを作成します。
   * `ToPSOptionsSpec`オブジェクトのデータメンバに値を割り当てて、実行時オプションを設定します。 例えば、作成されるPostScriptレベルを定義するには、`PSLevel`定義済みリスト値を`ToPSOptionsSpec`オブジェクトの`psLevel`データメンバに割り当てます。

1. PDFドキュメントをPostScriptファイルに変換します。

   `GeneratePDFServiceService`オブジェクトの`toPS2`メソッドを呼び出し、次の値を渡します。

   * PostScriptファイルに変換するPDFドキュメントを表す`BLOB`オブジェクト
   * 実行時オプションを指定する`ToPSOptionsSpec`オブジェクト

   変換が完了したら、`BLOB`オブジェクトの`MTOM`プロパティにアクセスして、PostScriptドキュメントを表すバイナリデータを抽出します。 これは、PostScriptファイルに書き出すことのできるバイト配列を返します。

1. PostScriptファイルを保存します。

   * コンストラクターを呼び出して、`System.IO.FileStream`オブジェクトを作成します。 PSファイルのファイルの場所を表すstring値を渡します。
   * `encryptPDFUsingPassword`メソッドから返された`BLOB`オブジェクトのデータ内容を格納するバイト配列を作成します。 `BLOB`オブジェクトの`MTOM`フィールドの値を取得して、バイト配列を入力します。
   * コンストラクターを呼び出して`System.IO.FileStream`オブジェクトを渡し、`System.IO.BinaryWriter`オブジェクトを作成します。
   * `System.IO.BinaryWriter`オブジェクトの`Write`メソッドを呼び出し、バイト配列を渡すことで、バイト配列の内容をPostScriptファイルに書き込みます。

**関連トピック**

[手順の概要](converting-pdf-postscript-image-files.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## PDFドキュメントの画像形式への変換{#converting-pdf-documents-to-image-formats}

Convert PDFサービスを使用すると、PDFドキュメントをJPEG、JPEG 2000、TIFF、PNGなどの画像形式にプログラム的に変換できます。 PDFドキュメントを画像ファイルに変換すると、そのPDFドキュメントを画像ファイルとして使用できます。 例えば、ストレージ用に企業コンテンツ管理システムに画像を配置できます。

PDFドキュメントを画像に変換する場合、Convert PDFサービスは、ドキュメントの各ページに対して個別の画像を作成します。 つまり、ドキュメントに20ページが含まれる場合、Convert PDFサービスは20個の画像ファイルを作成します。 PDFドキュメントを画像形式に変換する場合、PDFドキュメント内の各ページに対して個別の画像を作成するか、PDFドキュメント全体に対して単一の画像ファイルを作成できます。

>[!NOTE]
>
>Convert PDFサービスについて詳しくは、『[AEM Forms向けサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順{#summary_of_steps-1}の概要

PDFドキュメントをサポートされている任意の種類に変換するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Convert PDFサービスクライアントを作成します。
1. 変換するPDFドキュメントを取得します。
1. 実行時オプションを設定します。
1. PDFを画像に変換します。
1. コレクションから画像ファイルを取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めてください。

**Convert PDFクライアントの作成**

プログラムでConvert PDFサービス操作を実行する前に、Convert PDFサービスクライアントを作成する必要があります。 Java APIを使用している場合は、`ConvertPdfServiceClient`オブジェクトを作成します。 WebサービスAPIを使用している場合は、`ConvertPDFServiceService`オブジェクトを作成します。

**変換するPDFドキュメントを取得します**

画像に変換するPDFドキュメントを取得する必要があります。 インタラクティブPDFドキュメントを画像に変換することはできません。 これを行うと、例外が発生します。 インタラクティブPDFドキュメントを画像ファイルに変換するには、変換前にPDFドキュメントを統合する必要があります。 ([PDFドキュメントの分割・統合](/help/forms/developing/creating-document-output-streams.md#flattening-pdf-documents)を参照)。

**実行時オプションの設定**

画像形式や解像度の値など、実行時のオプションを設定する必要があります。 ランタイム値について詳しくは、[AEM FormsAPIリファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)の`ToImageOptionsSpec`クラスリファレンスを参照してください。

**PDFを画像に変換します**

サービスクライアントを作成し、実行時オプションを設定した後で、PDFドキュメントを画像に変換できます。 画像を含むコレクションオブジェクトが返されます。

**コレクションから画像ファイルを取得する**

Convert PDFサービスが返すコレクションオブジェクトから画像ファイルを取得できます。 コレクション内の各要素は`com.adobe.idp.Document`インスタンス（Webサービスを使用している場合は`BLOB`インスタンス）で、JPGファイルなどの画像ファイルとして保存できます。

イメージファイルの形式は、`ImageConvertFormat`実行時オプションによって異なります。 つまり、`ImageConvertFormat`実行時オプションを`ImageConvertFormat.JPEG`に設定した場合は、画像ファイルをJPGファイルとして保存できます。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Convert PDF Service APIクイック開始](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Java API {#convert-a-pdf-document-to-image-files-using-the-java-api}を使用してPDFドキュメントを画像ファイルに変換する

Convert PDFサービスAPI(Java)を使用して、PDFドキュメントを画像形式に変換します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-convertpdf-client.jarなどのクライアントJARファイルを含めます。

1. Convert PDFクライアントの作成を参照してください。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `ConvertPdfServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 変換するPDFドキュメントを取得します。

   * コンストラクターを使用し、PDFドキュメントの場所を指定するstring値を渡して、変換するPDFドキュメントを表す`java.io.FileInputStream`オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 実行時オプションを設定します。

   * コンストラクタを使用して `ToImageOptionsSpec` オブジェクトを作成します。
   * 必要に応じて、このオブジェクトに属するメソッドを呼び出します。 例えば、`setImageConvertFormat`メソッドを呼び出し、形式の種類を指定する`ImageConvertFormat`列挙値を渡して、イメージの種類を設定します。

   >[!NOTE]
   >
   >`ImageConvertFormat`定義済みリスト値の設定は必須です。

1. PDFを画像に変換します。

   `ConvertPdfServiceClient`オブジェクトの`toImage2`メソッドを呼び出し、次の値を渡します。

   * 変換するPDFファイルを表す`com.adobe.idp.Document`オブジェクトです。
   * ターゲット画像形式に関する様々な環境設定を含む`com.adobe.livecycle.converpdfservice.client.ToImageOptionsSpec`オブジェクト。

   `toImage2`メソッドは、画像を含む`java.util.List`オブジェクトを返します。 コレクション内の各要素は`com.adobe.idp.Document`インスタンスです。

1. コレクションから画像ファイルを取得します。

   `java.util.List`オブジェクトを繰り返し処理して、画像が存在するかどうかを判断します。 各要素は`com.adobe.idp.Document`インスタンスです。 `com.adobe.idp.Document`オブジェクトの`copyToFile`メソッドを呼び出し、`java.io.File`オブジェクトを渡して、画像を保存します。

**関連トピック**

[クイック開始（SOAPモード）:Java APIを使用したPDFドキュメントのJPEGファイルへの変換](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-jpeg-files-using-the-java-api)

### WebサービスAPI {#convert-a-pdf-document-to-image-files-using-the-web-service-api}を使用してPDFドキュメントを画像ファイルに変換する

Convert PDF Service API（Webサービス）を使用してPDFドキュメントを画像形式に変換します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. convert PDFクライアントを作成します。

   * `ConvertPdfServiceClient`オブジェクトを作成するには、そのデフォルトのコンストラクタを使用します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`ConvertPdfServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに指定するstring値を渡します（例：`http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`）。 `lc_version`属性を使用する必要はありません。 ただし、`?blob=mtom`を指定します。
   * `ConvertPdfServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * AEM formsユーザー名をフィールド`ConvertPdfServiceClient.ClientCredentials.UserName.UserName`に割り当てます。
      * 対応するパスワード値をフィールド`ConvertPdfServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * 定数値`HttpClientCredentialType.Basic`をフィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に割り当てます。
      * 定数値`BasicHttpSecurityMode.TransportCredentialOnly`をフィールド`BasicHttpBindingSecurity.Security.Mode`に割り当てます。

1. 変換するPDFドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この`BLOB`オブジェクトは、PDFフォームの保存に使用されます。
   * コンストラクターを呼び出して、`System.IO.FileStream`オブジェクトを作成します。 PDFフォームの場所とファイルを開くモードを指定するstring値を渡します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得して、バイト配列のサイズを決定します。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出して、バイト配列にストリームデータを入力します。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * `BLOB`オブジェクトに、`MTOM`フィールドにバイト配列の内容を割り当てて入力します。

1. 実行時オプションを設定します。

   * コンストラクタを使用して `ToImageOptionsSpec` オブジェクトを作成します。
   * 必要に応じて、このオブジェクトに属するメソッドを呼び出します。 例えば、`setImageConvertFormat`メソッドを呼び出し、形式の種類を指定する`ImageConvertFormat`定義済みリスト値を渡して、画像の種類を設定します。

   >[!NOTE]
   >
   >`ImageConvertFormat`定義済みリスト値の設定は必須です。

1. PDFを画像に変換します。

   `ConvertPDFServiceService`オブジェクトの`toImage2`メソッドを呼び出し、次の値を渡します。

   * 変換するファイルを表す`BLOB`オブジェクト
   * ターゲット画像形式に関する様々な環境設定を含む`ToImageOptionsSpec`オブジェクト

   `toImage2`メソッドは、新しく作成された画像ファイルを含む`MyArrayOfBLOB`オブジェクトを返します。

1. コレクションから画像ファイルを取得します。

   * `Count`フィールドの値を取得して、`MyArrayOfBLOB`オブジェクトの要素数を決定します。 各要素は、画像を含む`BLOB`オブジェクトです。
   * `MyArrayOfBLOB`オブジェクトを繰り返し処理し、各画像ファイルを保存します。

**関連トピック**

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
