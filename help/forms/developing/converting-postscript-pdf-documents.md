---
title: PostscriptからPDFドキュメントへの変換
seo-title: PostscriptからPDFドキュメントへの変換
description: 'null'
seo-description: 'null'
uuid: 2143f406-1fdd-4551-a738-1a8388f8d478
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 06ad343a-f74d-41f5-b3c8-b85bb723ceeb
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# PostscriptからPDFドキュメントへの変換 {#converting-postscript-to-pdf-documents}

## Distillerサービスについて {#about-the-distiller-service}

Distiller®サービスは、PostScript®、Encapsulated postScript(EPS)およびPRNファイルを、ネットワーク経由でコンパクトで信頼性の高い、より安全なPDFファイルに変換します。 Distiller サービスは、請求書や明細書など、容量の大きい印刷ドキュメントを電子ドキュメントに変換する際によく使用されます。ドキュメントを PDF に変換して、顧客にドキュメントの印刷バージョンと電子バージョンを送付できます。

>[!NOTE]
>
>For more information about the Distiller service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## PostScriptドキュメントのPDFドキュメントへの変換 {#converting-postscript-to-pdf-documents-inner}

このトピックでは、Distiller Service API（JavaおよびWebサービス）を使用して、PostScript(PS)、Encapsulated postScript(EPS)およびPRNファイルをプログラムでPDFドキュメントに変換する方法について説明します。

>[!NOTE]
>
>For more information about the Distiller service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>PostScriptファイルをPDFドキュメントに変換するには、AEM formsをホストするサーバーに次のいずれかをインストールする必要があります。Acrobat 9またはMicrosoft Visual C++ 2005再配布可能パッケージ。

### 手順の概要 {#summary-of-steps}

サポートされているタイプをPDFドキュメントに変換するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Distillerサービスクライアントを作成します。
1. 変換するファイルを取得します。
1. PDF作成操作を呼び出します。
1. PDFドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めてください。

**Distillerサービスクライアントの作成**

プログラムを使用してDistillerサービス操作を実行する前に、Distillerサービスクライアントを作成する必要があります。 Java APIを使用している場合は、オブジェクトを作成し `DistillerServiceClient` ます。 WebサービスAPIを使用している場合は、オブジェクトを作成 `DistillerServiceService` します。

**変換するファイルを取得します**

変換するファイルを取得する必要があります。 例えば、PSファイルをPDFドキュメントに変換するには、PSファイルを取得する必要があります。

**PDF作成操作の呼び出し**

サービスクライアントを作成した後、PDF作成操作を呼び出すことができます。 この操作には、変換対象のドキュメントへのパスなど、変換対象のドキュメントに関する情報が必要です。

**PDFドキュメントの保存**

PDFドキュメントをPDFファイルとして保存できます。

**関連トピック**

[Java APIを使用したPostScriptファイルのPDFへの変換](converting-postscript-pdf-documents.md#convert-a-postscript-file-to-pdf-using-the-java-api)

[WebサービスAPIを使用したPostScriptファイルのPDFへの変換](converting-postscript-pdf-documents.md#converting-a-postscript-file-to-pdf-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[OutputサービスAPIのクイックスタート](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Java APIを使用したPostScriptファイルのPDFへの変換 {#convert-a-postscript-file-to-pdf-using-the-java-api}

Distiller Service API(Java)を使用してPostScriptファイルをPDFドキュメントに変換します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-distiller-client.jarなどのクライアントJARファイルを含めます。

1. Distillerサービスクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `DistillerServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. 変換するファイルを取得します。

   * 変換するフ `java.io.FileInputStream` ァイルを表すオブジェクトを作成します。このオブジェクトは、コンストラクターを使用し、ファイルの場所を指定するstring値を渡すことによって作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PDF作成操作を呼び出します。

   オブジェクト `DistillerServiceClient` のメソッドを `createPDF` 呼び出し、次の値を渡します。

   * 変換 `com.adobe.idp.Document` するPS、EPS、またはPRNファイルを表すオブジェクトです。
   * 変換 `java.lang.String` するファイルの名前を含むオブジェクトです
   * 使用 `java.lang.String` するAdobe PDF設定の名前を含むオブジェクト
   * 使用 `java.lang.String` するセキュリティ設定の名前を含むオブジェクトです
   * PDFドキュメント `com.adobe.idp.Document` の生成時に適用される設定を含むオプションのオブジェクトです
   * PDFドキュメント `com.adobe.idp.Document` に適用されるメタデータ情報を含むオプションのオブジェクトです
   このメ `createPDF` ソッドは、新し `CreatePDFResult` いPDFドキュメントと生成される可能性のあるログファイルを含むオブジェクトを返します。 通常、ログファイルには、変換要求によって生成されたエラーメッセージまたは警告メッセージが含まれます。

1. PDFドキュメントを保存します。

   新しく作成したPDFドキュメントを取得するには、次の操作を実行します。

   * オブジェクト `CreatePDFResult` のメソッドを呼び出 `getCreatedDocument` します。 オブジェクトを返 `com.adobe.idp.Document` します。
   * オブジェクト `com.adobe.idp.Document` のメソッドを呼 `copyToFile` び出してPDFドキュメントを抽出します。
   同様に、ログドキュメントを取得するには、次の操作を実行します。

   * オブジェクト `CreatePDFResult` のメソッドを呼び出 `getLogDocument` します。 オブジェクトを返 `com.adobe.idp.Document` します。
   * オブジェクト `com.adobe.idp.Document` のメソッドを呼び `copyToFile` 出して、ログドキュメントを抽出します。


**関連トピック**

[手順の概要](converting-postscript-pdf-documents.md#summary-of-steps)

[クイックスタート（SOAPモード）:Java APIを使用したPostScriptファイルのPDFドキュメントへの変換](/help/forms/developing/distiller-service-java-api-quick.md#quick-start-soap-mode-converting-a-postscript-file-to-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したPostScriptファイルのPDFへの変換 {#converting-a-postscript-file-to-pdf-using-the-web-service-api}

Distiller Service API（Webサービス）を使用してPostScriptファイルをPDFドキュメントに変換します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/DistillerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. Distillerサービスクライアントを作成します。

   * Create a `DistillerServiceClient` object by using its default constructor.
   * Create a `DistillerServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLを指定するstring値をAEM Formsサービスに渡します(例 `http://localhost:8080/soap/services/DistillerService?blob=mtom`:)。属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。 ただし、MTOMを使用す `?blob=mtom` るように指定します。
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `DistillerServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `DistillerServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `DistillerServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. 変換するファイルを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、PDFドキュメントに変換するファイルを保存するために使用します。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、ファイルを開く場所とモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイト配列、開 `System.IO.FileStream` 始位置、ストリ `Read` ーム長を渡すことによって、バイト配列にストリームデータを設定します。
   * オブジェクト `BLOB` にバイト配列の内容をプロ `MTOM` パティに割り当てて、オブジェクトを設定します。

1. PDF作成操作を呼び出します。

   オブジェクト `DistillerServiceService` のメソッドを呼 `CreatePDF2` び出し、次の必要な値を渡します。

   * 変換 `BLOB` するPSファイルを表すオブジェクトです。
   * 変換するファイルのパス名を含む文字列
   * 使用するAdobe PDF設定を含むstringオブジェクト(例 `Standard`)
   * 使用するセキュリティ設定(例： `No Securit`y)を含むstringオブジェクト
   * PDFドキュメント `BLOB` の生成時に適用される設定を含むオプションのオブジェクトです
   * PDFドキュメント `BLOB` に適用されるメタデータ情報を含むオプションのオブジェクトです
   * PDFドキ `BLOB` ュメントの保存に使用する出力パラメーター
   * ログの `BLOB` 保存に使用する出力パラメーター

1. PDFドキュメントを保存します。

   * Create a `System.IO.FileStream` object by invoking its constructor. 署名済みPDFドキュメントのファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * メソッド（出力パラメーター）によって返された `BLOB` オブジェクトの内容を格納す `CreatePDF2` るバイト配列を作成します。 オブジェクトのデータメンバーの値を取得して、バ `BLOB` イト配列を `MTOM` 設定します。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡すことで、バ `System.IO.BinaryWriter` イト配列の内 `Write` 容をPDFファイルに書き込みます。

**関連トピック**

[手順の概要](converting-postscript-pdf-documents.md#summary-of-steps)

<!-- UNRESOLVED LINKS
[Quick Start (MTOM): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7f01.2)

[Quick Start (SwaRef): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7eff.2)
-->

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
