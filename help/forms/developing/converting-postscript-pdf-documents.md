---
title: PostscriptドキュメントからPDFへの変換
seo-title: PostscriptドキュメントからPDFへの変換
description: Distillerサービスを使用して、PostScript®、Encapsulated PostScript(EPS)およびPRNファイルを、ネットワーク経由でコンパクトで信頼性の高い、より安全なPDFファイルに変換します。 Distillerサービスは、大量の印刷ドキュメントを、Java APIおよびWeb Service APIを使用する請求書や明細書などの電子ドキュメントに変換します。
seo-description: Distillerサービスを使用して、PostScript®、Encapsulated PostScript(EPS)およびPRNファイルを、ネットワーク経由でコンパクトで信頼性の高い、より安全なPDFファイルに変換します。 Distillerサービスは、大量の印刷ドキュメントを、Java APIおよびWeb Service APIを使用する請求書や明細書などの電子ドキュメントに変換します。
uuid: 2143f406-1fdd-4551-a738-1a8388f8d478
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 06ad343a-f74d-41f5-b3c8-b85bb723ceeb
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '1365'
ht-degree: 7%

---


# PostscriptからPDFドキュメントへの変換{#converting-postscript-to-pdf-documents}

## Distillerサービスについて{#about-the-distiller-service}

Distiller®サービスは、PostScript®、Encapsulated PostScript(EPS)およびPRNファイルを、ネットワーク経由でコンパクトで信頼性の高い、より安全なPDFファイルに変換します。 Distiller サービスは、請求書や明細書など、容量の大きい印刷ドキュメントを電子ドキュメントに変換する際によく使用されます。ドキュメントを PDF に変換して、顧客にドキュメントの印刷バージョンと電子バージョンを送付できます。

>[!NOTE]
>
>Distillerサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

## PostScriptからPDFドキュメントへの変換{#converting-postscript-to-pdf-documents-inner}

このトピックでは、DistillerサービスAPI（JavaおよびWebサービス）を使用して、PostScript(PS)、Encapsulated PostScript(EPS)およびPRNファイルをプログラムでPDFドキュメントに変換する方法について説明します。

>[!NOTE]
>
>Distillerサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

>[!NOTE]
>
>PostScriptファイルをPDFドキュメントに変換するには、AEM Formsをホストするサーバーに次のいずれかをインストールする必要があります。Acrobat 9またはMicrosoft Visual C++ 2005再配布可能パッケージ。

### 手順{#summary-of-steps}の概要

サポートされている任意の種類をPDFドキュメントに変換するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Distillerサービスクライアントを作成します。
1. 変換するファイルを取得します。
1. PDF作成操作を呼び出します。
1. PDFドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めてください。

**Distillerサービスクライアントの作成**

プログラムでDistillerサービスを実行する前に、Distillerサービスクライアントを作成する必要があります。 Java APIを使用している場合は、`DistillerServiceClient`オブジェクトを作成します。 WebサービスAPIを使用している場合は、`DistillerServiceService`オブジェクトを作成します。

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

### Java API {#convert-a-postscript-file-to-pdf-using-the-java-api}を使用したPostScriptファイルのPDFへの変換

DistillerサービスAPI(Java)を使用してPostScriptファイルをPDFドキュメントに変換します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-distiller-client.jarなどのクライアントJARファイルを含めます。

1. Distillerサービスクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用し、`DistillerServiceClient`オブジェクトを渡して、`ServiceClientFactory`オブジェクトを作成します。

1. 変換するファイルを取得します。

   * コンストラクターを使用し、ファイルの場所を指定する文字列値を渡して、変換するファイルを表す`java.io.FileInputStream`オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PDF作成操作を呼び出します。

   `DistillerServiceClient`オブジェクトの`createPDF`メソッドを呼び出し、次の値を渡します。

   * 変換するPS、EPS、またはPRNファイルを表す`com.adobe.idp.Document`オブジェクト
   * 変換するファイルの名前を含む`java.lang.String`オブジェクト
   * 使用するAdobe PDF設定の名前を含む`java.lang.String`オブジェクト
   * 使用するセキュリティ設定の名前が含まれる`java.lang.String`オブジェクト
   * PDFドキュメントの生成中に適用される設定を含む、オプションの`com.adobe.idp.Document`オブジェクトです
   * PDFドキュメントに適用するメタデータ情報を含む、オプションの`com.adobe.idp.Document`オブジェクトです

   `createPDF`メソッドは、新しいPDFドキュメントと、生成される可能性のあるログファイルを含む`CreatePDFResult`オブジェクトを返します。 通常、ログファイルには、変換要求によって生成されるエラーメッセージや警告メッセージが含まれます。

1. PDFドキュメントを保存します。

   新しく作成されたPDFドキュメントを取得するには、次の操作を実行します。

   * `CreatePDFResult`オブジェクトの`getCreatedDocument`メソッドを呼び出します。 `com.adobe.idp.Document`オブジェクトを返します。
   * `com.adobe.idp.Document`オブジェクトの`copyToFile`メソッドを呼び出してPDFドキュメントを抽出します。

   同様に、ログドキュメントを取得するには、次の操作を実行します。

   * `CreatePDFResult`オブジェクトの`getLogDocument`メソッドを呼び出します。 `com.adobe.idp.Document`オブジェクトを返します。
   * `com.adobe.idp.Document`オブジェクトの`copyToFile`メソッドを呼び出して、ログドキュメントを抽出します。


**関連トピック**

[手順の概要](converting-postscript-pdf-documents.md#summary-of-steps)

[クイック開始（SOAPモード）:Java APIを使用したPostScriptファイルのPDFドキュメントへの変換](/help/forms/developing/distiller-service-java-api-quick.md#quick-start-soap-mode-converting-a-postscript-file-to-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#converting-a-postscript-file-to-pdf-using-the-web-service-api}を使用したPostScriptファイルのPDFへの変換

DistillerサービスAPI（Webサービス）を使用してPostScriptファイルをPDFドキュメントに変換します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/DistillerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. Distillerサービスクライアントを作成します。

   * `DistillerServiceClient`オブジェクトを作成するには、そのデフォルトのコンストラクタを使用します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`DistillerServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに指定するstring値を渡します（例：`http://localhost:8080/soap/services/DistillerService?blob=mtom`）。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する際に使用されます。 ただし、MTOMを使用するには`?blob=mtom`を指定します。
   * `DistillerServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * AEM formsユーザー名をフィールド`DistillerServiceClient.ClientCredentials.UserName.UserName`に割り当てます。
      * 対応するパスワード値をフィールド`DistillerServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * 定数値`HttpClientCredentialType.Basic`をフィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に割り当てます。
      * 定数値`BasicHttpSecurityMode.TransportCredentialOnly`をフィールド`BasicHttpBindingSecurity.Security.Mode`に割り当てます。

1. 変換するファイルを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この`BLOB`オブジェクトは、PDFドキュメントに変換するファイルを保存するために使用します。
   * コンストラクターを呼び出し、ファイルを開く場所とモードを表す文字列値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得して、バイト配列のサイズを決定できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * `BLOB`オブジェクトに`MTOM`プロパティを割り当て、バイト配列の内容を指定します。

1. PDF作成操作を呼び出します。

   `DistillerServiceService`オブジェクトの`CreatePDF2`メソッドを呼び出し、次の必須値を渡します。

   * 変換するPSファイルを表す`BLOB`オブジェクトです
   * 変換するファイルのパス名を含む文字列です
   * 使用するAdobe PDF設定を含むstringオブジェクト（例：`Standard`）
   * 使用するセキュリティ設定を含む文字列オブジェクト（例：`No Securit`y）
   * PDFドキュメントの生成中に適用される設定を含む、オプションの`BLOB`オブジェクトです
   * PDFドキュメントに適用するメタデータ情報を含む、オプションの`BLOB`オブジェクトです
   * PDFドキュメントの保存に使用される`BLOB`出力パラメーター
   * ログの保存に使用する`BLOB`出力パラメーター

1. PDFドキュメントを保存します。

   * コンストラクターを呼び出して、`System.IO.FileStream`オブジェクトを作成します。 署名済みPDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * `CreatePDF2`メソッド（出力パラメーター）によって返された`BLOB`オブジェクトの内容を格納するバイト配列を作成します。 `BLOB`オブジェクトの`MTOM`データメンバの値を取得して、バイト配列を入力します。
   * コンストラクターを呼び出して`System.IO.FileStream`オブジェクトを渡し、`System.IO.BinaryWriter`オブジェクトを作成します。
   * `System.IO.BinaryWriter`オブジェクトの`Write`メソッドを呼び出し、バイト配列を渡すことで、バイト配列の内容をPDFファイルに書き込みます。

**関連トピック**

[手順の概要](converting-postscript-pdf-documents.md#summary-of-steps)

<!-- UNRESOLVED LINKS
[Quick Start (MTOM): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7f01.2)

[Quick Start (SwaRef): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7eff.2)
-->

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
