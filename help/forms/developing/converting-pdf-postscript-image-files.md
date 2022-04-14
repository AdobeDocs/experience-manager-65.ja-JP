---
title: PDF から Postscript および画像ファイルへの変換
seo-title: Converting PDF to Postscript andImage Files
description: Convert PDF サービスでは、Java API および web サービス API を使用して、 PDF ドキュメントを PostScript および多数の画像形式（JPEG、JPEG 2000、PNG、TIFF）に変換できます。
seo-description: Use the Convert PDF service to convert PDF documents to PostScript and to a number of image formats (JPEG, JPEG 2000, PNG, and TIFF) using the Java API and Web Service API.
uuid: 07da0391-7180-4197-aaa6-ae753d753b84
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: f8707752-2c83-461a-b83d-708754b0f3f6
role: Developer
exl-id: 31730c24-46c3-4111-9391-ccd4342740e9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '2809'
ht-degree: 100%

---

# PDF の Postscript および画像ファイルへの変換 {#converting-pdf-to-postscript-andimage-files}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

**Convert PDF サービスについて**

Convert PDF サービスは、PDF ドキュメントを PostScript および多数の画像形式（JPEG、JPEG 2000、PNG および TIFF）に変換します。PDF ドキュメントの PostScript への変換は、PostScript プリンターでの無人のサーバーベース印刷に便利です。PDF ドキュメントをサポートしていないコンテンツ管理システムでドキュメントをアーカイブする場合、PDF ドキュメントをマルチページ TIFF ファイルに変換する方法が実用的です。

Convert PDF サービスを使用して、以下のタスクを実行できます。

* PDF ドキュメントを PostScript に変換します。
* PDFドキュメントを画像形式に変換します。

>[!NOTE]
>
>Convert PDF サービスについて詳しくは、[AEM Forms サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

## PDF ドキュメントの PostScript への変換 {#converting-pdf-documents-to-postscript}

ここでは、Convert PDF サービス API（Java および web サービス）を使用して、PDF ドキュメントを PostScript ファイルにプログラムで変換する方法について説明します。PostScript ファイルに変換する PDF ドキュメントは、非インタラクティブ PDF ドキュメントである必要があります。つまり、インタラクティブ PDF ドキュメントを PostScript ファイルに変換しようとすると、例外がスローされます。

>[!NOTE]
>
>Convert PDF サービスについて詳しくは、[AEM Forms サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary-of-steps}

PDF ドキュメントを PostScript ファイルに変換するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Convert PDF サービスクライアントを作成します。
1. PostScript ファイルに変換する PDF ドキュメントを参照します。
1. 変換の実行時オプションを設定します。
1. PDF ドキュメントを PostScript ファイルに変換します。
1. PostScript ファイルを保存します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、必ずプロキシファイルを含めてください。

**Convert PDF クライアントを作成**

プログラムによって Convert PDF サービスの操作を実行する前に、Convert PDF サービスクライアントを作成する必要があります。Java API を使用している場合は、`ConvertPdfServiceClient` オブジェクトを作成します。Web サービス API を使用している場合は、`ConvertPDFServiceService` オブジェクトを作成します。

このセクションでは、AEM Forms で導入された web サービス機能を使用します。新しい機能にアクセスするには、`lc_version` 属性を使用してプロキシオブジェクトを構築する必要があります。（[Web サービスを使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)の「web サービスを使用した新しい機能へのアクセス」を参照。）

**PostScript ファイルに変換する PDF ドキュメントを参照**

PostScript ファイルに変換する PDF ドキュメントを参照します。このトピックで前述したように、PDF ドキュメントは非インタラクティブ PDF ドキュメントである必要があります。インタラクティブ PDF ドキュメントを PostScript ファイルに変換しようとすると、例外がスローされます。

**コンバージョン実行時オプションを設定**

PDF ドキュメントを PostScript ファイルに変換する際に、作成する PostScript タイプを指定する実行時オプションを定義できます。例えば、レベル 3 の PostScript ファイルを定義できます。

通常、生成される PostScript ファイルは、入力 PDF ドキュメントのサイズを反映します。`ShrinkToFit` オプション（ページに合わせて PostScript ファイルの出力を縮小する）を選択した場合、入力 PDF ドキュメントと生成された PostScript ファイルの間に違いはありません。`ShrinkToFit` オプションは、入力 PDF ドキュメントよりも小さいページサイズで出力することを選択した場合にのみ有効になります。 小さいページサイズを選択するには、`PageSize` オプションを定義します。また、`RotateAndCenter`オプションを `true` に設定して、正しい PostScript 出力を取得することをお勧めします。

同様に、`ExpandToFit` オプション（ページに合わせて PostScript ファイルの出力を拡張する）を選択した場合、入力 PDF ドキュメントよりも大きいページサイズで出力するように選択した場合にのみ有効になります。大きいページサイズを選択するには、`PageSize` オプションを定義します。また、`RotateAndCenter` オプションを `true` に設定して、正しい PostScript 出力を取得することをお勧めします。

>[!NOTE]
>
>設定できる実行時の値について詳しくは、[AEM Forms API リファレンス](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ja)の `ToPSOptionsSpec` クラスレファレンスを参照してください。

**PDF ドキュメントを PostScript ファイルに変換**

サービスクライアントを作成し、実行時オプションを設定したら、PostScript 変換操作を呼び出すことができます。この操作では、変換するドキュメントに関する情報（ターゲットドキュメントに適した PostScript レベルを含む）が必要になります。

**PostScript ファイルを保存**

PDF ドキュメントを PostScript に変換したら、出力を PostScript ファイルとして保存できます。

**関連トピック**

[Java API を使用して PDF ドキュメントを PS に変換](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-java-api)

[Web サービス API を使用して PDF ドキュメントを PS に変換](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Convert PDF サービス API クイックスタート](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Java API を使用して PDF ドキュメントを PS に変換 {#convert-a-pdf-document-to-ps-using-the-java-api}

Convert PDF サービス API（Java）を使用して、PDF ドキュメントを PostScript に変換します。

1. プロジェクトファイルを含めます。

   adobe-convertpdf-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. Convert PDF クライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `ConvertPdfServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. PostScript ファイルに変換する PDF ドキュメントを参照します。

   * コンストラクターを使用して `java.io.FileInputStream` オブジェクトを作成し、変換する PDF ドキュメントの場所を指定する文字列値を渡します。
   * `com.adobe.idp.Document` コンストラクターを使用して、PDF ドキュメントを格納する `com.adobe.idp.Document` を作成します。PDF ドキュメントを含んだ `java.io.FileInputStream` オブジェクトを渡します。

1. 変換の実行時オプションを設定します。

   * コンストラクターを呼び出して `ToPSOptionsSpec` オブジェクトを作成します。
   * `ToPSOptionsSpec` オブジェクトに属する適切なメソッドを呼び出して、実行時オプションを設定します。 例えば、作成される PostScript レベルを定義するには、 `ToPSOptionsSpec` オブジェクトの `setPsLevel` メソッドを呼び出して、 PostScript レベルを指定する `PSLevel` 列挙値を渡します。設定できるすべての実行時の値について詳しくは、 [AEM Forms API リファレンス](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ja)の `ToPSOptionsSpec` クラスリファレンスを参照してください。

1. PDF ドキュメントを PostScript ファイルに変換します。

   `ConvertPdfServiceClient` オブジェクトの `toPS2` メソッドを呼び出して、次の値を渡します。

   * PostScript ファイルに変換する PDF ドキュメントを表す `com.adobe.idp.Document` オブジェクト
   * PostScript の実行時オプションを指定する `ToPSOptionsSpec` オブジェクト

   この `toPS2` メソッドは、新しい PostScript ドキュメントを含んだ `Document` オブジェクトを返します。

1. PostScript ファイルを保存します。

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が .ps であることを確認します。
   * `Document` オブジェクトの `copyToFile` メソッドを呼び出して、 `Document` オブジェクトの内容をファイルにコピーします（必ず、`toPS2` メソッドから返された `Document` オブジェクトを使用します）。

**関連トピック**

[手順の概要](converting-pdf-postscript-image-files.md#summary-of-steps)

[クイックスタート（SOAP モード）：Java API を使用した PDF ドキュメントの PostScript への変換](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-postscript-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用して PDF ドキュメントを PS に変換 {#convert-a-pdf-document-to-ps-using-the-web-service-api}

Convert PDF サービス API（web サービス）を使用して、PDF キュメントを PostScript に変換します。

1. プロジェクトファイルを含めます。

   MTOM を使用する Microsoft .NET プロジェクトを作成します。必ず、WSDL 定義 `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1` を使用します。

   >[!NOTE]
   >
   >`localhost` を、AEM Forms をホストするサーバーの IP アドレスに置き換えます。

1. Convert PDF クライアントを作成します。

   * デフォルトのコンストラクターを使用して `ConvertPdfServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して `ConvertPdfServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を指定する文字列値を AEM Forms サービス（例：`http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`）に渡します。`lc_version` 属性を使用する必要はありません。 ただし、 `?blob=mtom` を指定ください。
   *  `ConvertPdfServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` フィールドを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `ConvertPdfServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM forms ユーザー名を割り当てます。
      * 対応するパスワード値を `ConvertPdfServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` をフィールド `BasicHttpBindingSecurity.Transport.ClientCredentialType` に割り当てます。
      * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` をフィールド `BasicHttpBindingSecurity.Security.Mode` に割り当てます。

1. PostScript ファイルに変換する PDF ドキュメントを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、PostScript ファイルに変換された PDF ドキュメントを格納するために使用されます。
   * `System.IO.FileStream` オブジェクトを作成します。それには、コンストラクターを呼び出し、変換する PDF ドキュメントのファイルの場所と、ファイルを開くモードを表す文字列値を渡します。
   * `System.IO.FileStream` オブジェクトの内容を格納するバイト配列を作成します。バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティを取得して決定できます。
   * `System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことにより、バイト配列にストリームデータを入力します。
   * `MTOM` フィールドにバイト配列の内容を割り当てることにより、`BLOB` オブジェクトに入力します。

1. 変換の実行時オプションを設定します。

   * コンストラクターを使用して `ToPSOptionsSpec` オブジェクトを作成します。
   * `ToPSOptionsSpec` オブジェクトのデータメンバーに値を割り当てて、実行時オプションを設定します。例えば、作成する PostScript レベルを定義するには、`ToPSOptionsSpec` オブジェクトの `psLevel` データメンバーに `PSLevel` 列挙値を割り当てます。

1. PDF ドキュメントを PostScript ファイルに変換します。

   `GeneratePDFServiceService` オブジェクトの `toPS2` メソッドを呼び出して、次の値を渡します。

   * PostScript ファイルに変換する PDF ドキュメントを表す `BLOB` オブジェクト
   * 実行時のオプションを指定する `ToPSOptionsSpec` オブジェクト

   変換が完了したら、`BLOB` オブジェクトの `MTOM` プロパティにアクセスして、PostScript ドキュメントを表すバイナリデータを抽出します。PostScript ファイルに書き出すことができるバイト配列を返します。

1. PostScript ファイルを保存します。

   * コンストラクターを呼び出して、`System.IO.FileStream` オブジェクトを作成します。PS ファイルの場所を表す文字列値を渡します。
   * `encryptPDFUsingPassword` メソッドから返された `BLOB` オブジェクトのデータ内容を格納するバイト配列を作成します。`BLOB` オブジェクトの `MTOM` フィールドの値を取得して、バイト配列に入力します。
   * コンストラクターを呼び出し `System.IO.FileStream` オブジェクトを渡して、`System.IO.BinaryWriter` オブジェクトを作成します。
   * `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを呼び出し、バイト配列を渡して、バイト配列の内容を PostScript ファイルに書き込ます。

**関連トピック**

[手順の概要](converting-pdf-postscript-image-files.md#summary-of-steps)

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## PDFドキュメントの画像形式への変換 {#converting-pdf-documents-to-image-formats}

Convert PDF サービスを使用すると、PDF ドキュメントを JPEG、JPEG 2000、TIFF、PNG などの画像形式にプログラムで変換できます。PDF ドキュメントを画像ファイルに変換することにより、PDF ドキュメントを画像ファイルとして使用できます。例えば、画像をストレージ用のエンタープライズコンテンツ管理システムに配置できます。

Convert PDF サービスは、PDF ドキュメントを画像に変換する際に、ドキュメント内のページごとに個別の画像を作成します。例えば、ドキュメントのページ数が 20 の場合、 Convert PDF サービスは 20 個の画像ファイルを作成します。PDF ドキュメントを PDF 形式に変換する場合、PDF ドキュメント内のページごとに個々の画像を作成するか、画像ドキュメント全体の単一の画像ファイルを作成できます。

>[!NOTE]
>
>Convert PDF サービスについて詳しくは、[AEM Forms サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary_of_steps-1}

PDF ドキュメントをサポートされている任意のタイプに変換するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Convert PDF サービスクライアントを作成します。
1. 変換する PDF ドキュメントを取得します。
1. 実行時オプションを設定します。
1. PDF を画像に変換します。
1. コレクションから画像ファイルを取得します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、必ずプロキシファイルを含めてください。

**変換 PDF クライアントの作成**

プログラムによって Convert PDF サービスの操作を実行する前に、Convert PDF サービスクライアントを作成する必要があります。Java API を使用している場合は、`ConvertPdfServiceClient` オブジェクトを作成します。Web サービス API を使用している場合は、`ConvertPDFServiceService` オブジェクトを作成します。

**変換する PDF ドキュメントを取得**

画像に変換する PDF ドキュメントを取得する必要があります。インタラクティブ PDF ドキュメントを画像に変換することはできません。その操作を実行しようとすると、例外が発生します。インタラクティブ PDF ドキュメントを画像ファイルに変換するには、変換前に PDF ドキュメントを統合する必要があります（[PDF ドキュメントの統合](/help/forms/developing/creating-document-output-streams.md#flattening-pdf-documents)を参照してください）。

**実行時オプションを設定**

画像形式や解像度の値など、実行時オプションを設定する必要があります。実行時の値について詳しくは、[AEM Forms API リファレンス](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ja)の `ToImageOptionsSpec` のクラス参照を参照してください。

**PDF を画像に変換**

サービスクライアントを作成し、実行時オプションを設定すると、PDF ドキュメントを画像に変換できます。画像を含むコレクションオブジェクトが返されます。

**コレクションからの画像ファイルの取得**

Convert PDF サービスが返すコレクションオブジェクトから画像ファイルを取得できます。コレクションの各要素は `com.adobe.idp.Document` インスタンス（web サービスを使用している場合は `BLOB` インスタンス）であり、JPG ファイルなどの画像ファイルとして保存できます。

画像ファイルの形式は、`ImageConvertFormat` 実行時オプション によって異なります。例えば、`ImageConvertFormat` 実行時オプションを `ImageConvertFormat.JPEG` に設定すると、画像ファイルを JPG ファイルとして保存できます。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Convert PDF サービス API クイックスタート](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Java API を使用して PDF ドキュメントを画像ファイルに変換 {#convert-a-pdf-document-to-image-files-using-the-java-api}

Convert PDF サービス API（Java）を使用して、PDFドキュメントを画像形式に変換します。

1. プロジェクトファイルを含めます。

   adobe-convertpdf-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. Convert PDF クライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `ConvertPdfServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 変換する PDF ドキュメントを取得します。

   * コンストラクターを使用して、PDF ドキュメントの場所を指定する文字列値を渡すことにより、変換する PDF ドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 実行時オプションを設定します。

   * コンストラクタを使用して `ToImageOptionsSpec` オブジェクトを作成します。
   * 必要に応じて、このオブジェクトに属するメソッドを呼び出します。例えば、`setImageConvertFormat` メソッドを呼び出して、形式のタイプを 指定する `ImageConvertFormat` 列挙値を渡すことにより、画像のタイプを設定します。

   >[!NOTE]
   >
   >`ImageConvertFormat` 列挙値の設定は必須です。

1. PDF を画像に変換します。

   `ConvertPdfServiceClient` オブジェクトの `toImage2` メソッドを呼び出して、次の値を渡します。

   * 変換する PDF ドキュメントを表す `com.adobe.idp.Document` オブジェクト。
   * ターゲット画像の形式に関する各種の環境設定が含まれる `com.adobe.livecycle.converpdfservice.client.ToImageOptionsSpec` オブジェクト。

   `toImage2` メソッドは、画像が含まれる `java.util.List` オブジェクトを返します。コレクションに含まれる各要素は、`com.adobe.idp.Document` のインスタンスです。

1. コレクションから画像ファイルを取得します。

   `java.util.List` オブジェクトを繰り返して、画像が存在するかを判断します。各要素は、`com.adobe.idp.Document` のインスタンスです。`com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを呼び出し、`java.io.File` オブジェクトを渡して、画像を保存します。

**関連トピック**

[クイックスタート（SOAP モード）：Java API を使用した PDF ドキュメントの JPEG ファイルへの変換](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-jpeg-files-using-the-java-api)

### Web サービス API を使用して PDF ドキュメントを画像ファイルに変換 {#convert-a-pdf-document-to-image-files-using-the-web-service-api}

Convert PDF サービス API（web サービス）を使用して、PDF ドキュメントを画像の形式に変換します。

1. プロジェクトファイルを含めます。

   MTOM を使用する Microsoft .NET プロジェクトを作成します。次の WSDL 定義を使用します。`http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`

   >[!NOTE]
   >
   >`localhost` を、AEM Forms をホストしているサーバーの IP アドレスに置き換えます。

1. Convert PDF クライアントを作成します。

   * デフォルトのコンストラクターを使用して `ConvertPdfServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して `ConvertPdfServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`）。`lc_version` 属性を使用する必要はありません。ただし、`?blob=mtom` を指定します。
   * `ConvertPdfServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` フィールドを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * AEM Forms のユーザー名を `ConvertPdfServiceClient.ClientCredentials.UserName.UserName` フィールドに割り当てます。
      * 対応するパスワード値を `ConvertPdfServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を `BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
      * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` を `BasicHttpBindingSecurity.Security.Mode` フィールドに割り当てます。

1. 変換する PDF ドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、PDF フォームを格納するために使用します。
   * コンストラクターを呼び出して `System.IO.FileStream` オブジェクトを作成します。PDF フォームの場所と、ファイルを開くときのモードを指定する文字列値を渡します。
   * `System.IO.FileStream` オブジェクトの内容を格納するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得して、バイト配列のサイズを決定します。
   * `System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出して、バイト配列にストリームデータを入力します。読み取り対象のバイト配列、開始位置、ストリーム長を渡します。
   * `MTOM` フィールドを割り当てることにより、`BLOB` オブジェクトにバイト配列の内容を入力します。

1. 実行時オプションを設定します。

   * コンストラクタを使用して `ToImageOptionsSpec` オブジェクトを作成します。
   * 必要に応じて、このオブジェクトに属するメソッドを呼び出します。例えば、画像のタイプを設定するには、`setImageConvertFormat` メソッドを呼び出し、フォーマットタイプを指定する `ImageConvertFormat` 列挙値を渡します。

   >[!NOTE]
   >
   >`ImageConvertFormat` 列挙値の設定は必須です。

1. PDF を画像に変換します。

   `ConvertPDFServiceService` オブジェクトの `toImage2` メソッドを呼び出して次の値を渡します。

   * 変換するファイルを表す `BLOB` オブジェクト
   * ターゲット画像形式に関する様々な環境設定を含む `ToImageOptionsSpec` オブジェクト

   `toImage2` メソッドは、新しく作成された画像ファイルを含む `MyArrayOfBLOB` オブジェクトを返します。

1. コレクションから画像ファイルを取得します。

   * `MyArrayOfBLOB` オブジェクトの `Count` フィールドの値を取得し、その中の要素数を決定します。各要素は 画像を含む `BLOB` オブジェクトです。
   * `MyArrayOfBLOB` オブジェクトを繰り返し処理し、各画像ファイルを保存します。

**関連トピック**

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
