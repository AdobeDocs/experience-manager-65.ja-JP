---
title: PostscriptドキュメントからPDFへの変換
seo-title: PostscriptドキュメントからPDFへの変換
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
workflow-type: tm+mt
source-wordcount: '1269'
ht-degree: 7%

---


# PostscriptドキュメントからPDFへの変換 {#converting-postscript-to-pdf-documents}

## Distiller事務について {#about-the-distiller-service}

Distiller®サービスは、PostScript®、Encapsulated PostScript(EPS)およびPRNファイルを、ネットワーク経由でコンパクトで信頼性の高い、より安全なPDFファイルに変換します。 Distiller サービスは、請求書や明細書など、容量の大きい印刷ドキュメントを電子ドキュメントに変換する際によく使用されます。ドキュメントを PDF に変換して、顧客にドキュメントの印刷バージョンと電子バージョンを送付できます。

>[!NOTE]
>
>For more information about the Distiller service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## PostScriptからPDFドキュメントへの変換 {#converting-postscript-to-pdf-documents-inner}

このトピックでは、DistillerサービスAPI（JavaおよびWebサービス）を使用して、PostScript(PS)、Encapsulated PostScript(EPS)およびPRNファイルをプログラムでPDFドキュメントに変換する方法について説明します。

>[!NOTE]
>
>For more information about the Distiller service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>PostScriptファイルをPDFドキュメントに変換するには、AEM Formsをホストするサーバーに次のいずれかをインストールする必要があります。Acrobat 9またはMicrosoft Visual C++ 2005再配布可能パッケージ。

### 手順の概要 {#summary-of-steps}

サポートされている任意の種類をPDFドキュメントに変換するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Distillerサービスクライアントを作成します。
1. 変換するファイルを取得します。
1. PDF作成操作を呼び出します。
1. PDFドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めてください。

**Distillerサービスクライアントの作成**

プログラムでDistillerサービスを実行する前に、Distillerサービスクライアントを作成する必要があります。 Java APIを使用している場合は、 `DistillerServiceClient` オブジェクトを作成します。 WebサービスAPIを使用している場合は、 `DistillerServiceService` オブジェクトを作成します。

**変換するファイルを取得します**

変換するファイルを取得する必要があります。 例えば、PSファイルをPDFドキュメントに変換するには、PSファイルを取得する必要があります。

**PDF作成操作の呼び出し**

サービスクライアントを作成したら、PDF作成操作を呼び出すことができます。 この操作には、ターゲットドキュメントへのパスなど、変換するドキュメントに関する情報が必要です。

**PDFドキュメントの保存**

PDFドキュメントをPDFファイルとして保存できます。

**関連トピック**

[Java APIを使用したPostScriptファイルのPDFへの変換](converting-postscript-pdf-documents.md#convert-a-postscript-file-to-pdf-using-the-java-api)

[WebサービスAPIを使用したPostScriptファイルのPDFへの変換](converting-postscript-pdf-documents.md#converting-a-postscript-file-to-pdf-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[OutputサービスAPIのクイック開始](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Java APIを使用したPostScriptファイルのPDFへの変換 {#convert-a-postscript-file-to-pdf-using-the-java-api}

DistillerサービスAPI(Java)を使用してPostScriptファイルをPDFドキュメントに変換します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-distiller-client.jarなどのクライアントJARファイルを含めます。

1. Distillerサービスクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `DistillerServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. 変換するファイルを取得します。

   * コンストラクターを使用し、ファイルの場所を指定する文字列値を渡して、変換するファイルを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PDF作成操作を呼び出します。

   オブジェクトの `DistillerServiceClient``createPDF` メソッドを呼び出し、次の値を渡します。

   * 変換するPS、EPS、またはPRNファイルを表す `com.adobe.idp.Document` オブジェクトです。
   * 変換するファイルの名前を含む `java.lang.String` オブジェクトです。
   * 使用するAdobe PDF設定の名前を含む `java.lang.String` オブジェクトです
   * 使用するセキュリティ設定の名前を含む `java.lang.String` オブジェクトです
   * PDFドキュメントの生成時に適用される設定を含むオプションの `com.adobe.idp.Document` オブジェクトです
   * PDFドキュメントに適用されるメタデータ情報を含むオプションの `com.adobe.idp.Document` オブジェクトです

   この `createPDF` メソッドは、新しいPDFドキュメントと、生成される可能性のあるログファイルを含む `CreatePDFResult` オブジェクトを返します。 通常、ログファイルには、変換要求によって生成されるエラーメッセージや警告メッセージが含まれます。

1. PDFドキュメントを保存します。

   新しく作成されたPDFドキュメントを取得するには、次の操作を実行します。

   * オブジェクトの `CreatePDFResult` メソッドを呼び出し `getCreatedDocument` ます。 これは、 `com.adobe.idp.Document` オブジェクトを返します。
   * オブジェクトの `com.adobe.idp.Document``copyToFile` メソッドを呼び出してPDFドキュメントを抽出します。

   同様に、ログドキュメントを取得するには、次の操作を実行します。

   * オブジェクトの `CreatePDFResult` メソッドを呼び出し `getLogDocument` ます。 これは、 `com.adobe.idp.Document` オブジェクトを返します。
   * オブジェクトの `com.adobe.idp.Document``copyToFile` メソッドを呼び出してログドキュメントを抽出します。


**関連トピック**

[手順の概要](converting-postscript-pdf-documents.md#summary-of-steps)

[クイック開始（SOAPモード）:Java APIを使用したPostScriptファイルのPDFドキュメントへの変換](/help/forms/developing/distiller-service-java-api-quick.md#quick-start-soap-mode-converting-a-postscript-file-to-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したPostScriptファイルのPDFへの変換 {#converting-a-postscript-file-to-pdf-using-the-web-service-api}

DistillerサービスAPI（Webサービス）を使用してPostScriptファイルをPDFドキュメントに変換します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/DistillerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Forms `localhost` をホストするサーバーのIPアドレスに置き換えます。

1. Distillerサービスクライアントを作成します。

   * Create a `DistillerServiceClient` object by using its default constructor.
   * Create a `DistillerServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/DistillerService?blob=mtom`)に指定するstring値を渡します。 属性を使用する必要はありません `lc_version` 。 この属性は、サービス参照を作成する際に使用されます。 ただし、MTOMを使用す `?blob=mtom` るように指定します。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `DistillerServiceClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当て `DistillerServiceClient.ClientCredentials.UserName.UserName`ます。
      * 対応するパスワード値をフィールドに割り当て `DistillerServiceClient.ClientCredentials.UserName.Password`ます。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当て `BasicHttpBindingSecurity.Security.Mode`ます。

1. 変換するファイルを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、PDFドキュメントに変換するファイルの保存に使用されます。
   * コンストラクターを呼び出し、ファイルを開く場所とモードを表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
   * オブジェクトの `System.IO.FileStream``Read` メソッドを呼び出し、読み取るバイト配列、開始位置およびストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * オブジェクトのプロパティにバイト配列の内容を割り当てて、 `BLOB``MTOM` オブジェクトを入力します。

1. PDF作成操作を呼び出します。

   オブジェクトの `DistillerServiceService``CreatePDF2` メソッドを呼び出し、次の必須値を渡します。

   * 変換するPSファイルを表す `BLOB` オブジェクトです。
   * 変換するファイルのパス名を含む文字列です
   * 使用するAdobe PDF設定を含むstringオブジェクト(例： `Standard`)
   * 使用するセキュリティ設定が格納されているstringオブジェクト( `No Securit`yなど)
   * PDFドキュメントの生成時に適用される設定を含むオプションの `BLOB` オブジェクトです
   * PDFドキュメントに適用されるメタデータ情報を含むオプションの `BLOB` オブジェクトです
   * PDFドキュメントの保存に使用される `BLOB` 出力パラメーター
   * ログの保存に使用される `BLOB` 出力パラメーター

1. PDFドキュメントを保存します。

   * Create a `System.IO.FileStream` object by invoking its constructor. 署名済みPDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * メソッド（出力パラメーター）によって返された `BLOB` オブジェクトの内容を格納するバイト配列を作成し `CreatePDF2` ます。 オブジェクトのデータメンバーの値を取得して、 `BLOB` バイト配列を入力し `MTOM` ます。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡して、バイト配列の内容をPDFファイルに書き込み `System.IO.BinaryWriter` ま `Write` す。

**関連トピック**

[手順の概要](converting-postscript-pdf-documents.md#summary-of-steps)

<!-- UNRESOLVED LINKS
[Quick Start (MTOM): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7f01.2)

[Quick Start (SwaRef): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7eff.2)
-->

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
