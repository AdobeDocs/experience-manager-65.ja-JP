---
title: FormsService にドキュメントを渡す
seo-title: Passing Documents to the FormsService
description: 'フォームデザインを含む com.adobe.idp.Document オブジェクトを Forms サービスに渡します。Forms サービスは、com.adobe.idp.Document オブジェクトにあるフォームデザインをレンダリングします。 '
seo-description: Pass a com.adobe.idp.Document object that contains the form design to the Forms service. The Forms service renders the form design located in the com.adobe.idp.Document object.
uuid: 841e97f3-ebb8-4340-81a9-b6db11f0ec82
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: e23de3c3-f8a0-459f-801e-a0942fb1c6aa
role: Developer
exl-id: 29c7ebda-407a-464b-a9db-054163f5b737
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '1684'
ht-degree: 100%

---

# Forms サービスにドキュメントを渡す {#passing-documents-to-the-formsservice}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

AEM Forms サービスは、ユーザーから情報を収集するために、インタラクティブ PDF Forms をクライアントデバイス（通常は web ブラウザー）にレンダリングします。インタラクティブ PDF フォームは、通常 XDP ファイルとして保存され、Designer で作成されるフォームデザインに基づいています。AEM Forms では、フォームデザインを含む `com.adobe.idp.Document` オブジェクトを Forms サービスに渡すことができます。次に、Forms サービスは、`com.adobe.idp.Document` オブジェクトにあるフォームデザインをレンダリングします。

`com.adobe.idp.Document` オブジェクトを Forms サービスに渡す利点は、他のサービス操作が `com.adobe.idp.Document` インスタンスを返すことです。つまり、別のサービス操作から `com.adobe.idp.Document` インスタンスを取得し、レンダリングできます。例えば、（次の図に示すように）XDP ファイルが `/Company Home/Form Designs` という名前のコンテンツサービス（非推奨）ノードに格納されているとします。

プログラムによってコンテンツサービス（非推奨）から Loan.xdp を取得し、XDP ファイルを `com.adobe.idp.Document` オブジェクト内で Forms サービスに渡します。

>[!NOTE]
>
>Forms サービスについて詳しくは、[AEM Forms サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

## 手順の概要 {#summary-of-steps}

コンテンツサービス（非推奨）から取得したドキュメントを Forms サービスに渡すには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Forms と Document Management Client API オブジェクトを作成します。
1. コンテンツサービス（非推奨）からフォームデザインを取得します。
1. インタラクティブ PDF フォームをレンダリングします。
1. フォームデータストリームを使用してアクションを実行します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを含めます。

**Forms と Document Management Client API オブジェクトの作成**

プログラムで Forms Service API 操作を実行する前に、Forms Client API オブジェクトを作成します。また、このワークフローはコンテンツサービス（非推奨）から XDP ファイルを取得するため、Document Management API オブジェクトを作成します。

**コンテンツサービス（非推奨）からフォームデザインを取得**

Java または web サービス API を使用して、コンテンツサービス（非推奨）から XDP ファイルを取得します。XDP ファイルは、`com.adobe.idp.Document` インスタンス 内（または web サービスを使用する場合は `BLOB` インスタンス）で返されます。その後、 Forms サービスに `com.adobe.idp.Document` インスタンスを渡します。

**インタラクティブ PDF フォームのレンダリング**

インタラクティブフォームをレンダリングするには、コンテンツサービス（非推奨）から返された `com.adobe.idp.Document` インスタンスを Forms サービスに渡します。

>[!NOTE]
>
>フォームデザインを含んだ `com.adobe.idp.Document` を Forms サービスに渡します。`renderPDFForm2` および `renderHTMLForm2` という名前の 2 つの新しいメソッドは、フォームデザインを含む `com.adobe.idp.Document` オブジェクトを受け入れます。

**フォームデータストリームを使用してアクションを実行**

クライアントアプリケーションの種類に応じて、フォームをクライアント web ブラウザーに書き込んだり、フォームを PDF ファイルとして保存したりできます。通常、web ベースのアプリケーションは、フォームを web ブラウザーに書き込みます。ただし、デスクトップアプリケーションは通常フォームを PDF ファイルとして保存します。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms サービス API のクイックスタート](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

## Java API を使用して Forms サービスにドキュメントを渡す {#pass-documents-to-the-forms-service-using-the-java-api}

Forms サービスとコンテンツサービス（非推奨）API (Java) を使用して、コンテンツサービス（非推奨）から取得したドキュメントを渡します。

1. プロジェクトファイルを含める

   adobe-forms-client.jar やadobe-contentservices-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. Forms と Document Management Client API オブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。（[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照。）
   * コンストラクターを使用して `ServiceClientFactory` オブジェクトを渡すことによって、`FormsServiceClient` オブジェクトを作成します。
   * コンストラクタを使用して `DocumentManagementServiceClientImpl` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. コンテンツサービス（非推奨）からフォームデザインを取得する

   `DocumentManagementServiceClientImpl` オブジェクトの `retrieveContent` メソッドを呼び出して、次の値を渡します。

   * コンテンツの追加先となるストアを指定する文字列値です。 デフォルトストアは `SpacesStore` です。この値は必須パラメーターです。
   * 取得するコンテンツの完全修飾パスを指定する文字列値（例：`/Company Home/Form Designs/Loan.xdp`）です。 この値は必須パラメーターです。
   * バージョンを指定する文字列値。この値はオプションのパラメーターであり、空の文字列を渡すことができます。この場合、最新バージョンが取得されます。

   `retrieveContent` メソッドは、XDP ファイルを含む `CRCResult` オブジェクトを返します。`CRCResult` オブジェクトの `getDocument` メソッドを呼び出して、`com.adobe.idp.Document` インスタンスを取得します。

1. インタラクティブ PDF フォームのレンダリング

   `FormsServiceClient` オブジェクトの `renderPDFForm2` メソッドを呼び出して、次の値を渡します。

   * コンテンツサービス（非推奨）から取得したフォームデザインを含む `com.adobe.idp.Document` オブジェクトです。
   * フォームに結合するデータを含む `com.adobe.idp.Document` オブジェクトです。データを結合しない場合は、空の `com.adobe.idp.Document` オブジェクトを渡します。
   * 実行時オプションを保存する `PDFFormRenderSpec` オブジェクト。この値はオプションのパラメーターであり、実行時のオプションを指定しない場合は、`null` を指定できます。
   * URI 値を格納する `URLSpec` オブジェクト。 この値はオプションのパラメーターであり、`null` を指定できます。
   * 添付ファイルを保存する `java.util.HashMap` オブジェクト。 この値はオプションのパラメーターであり、フォームにファイルを添付しない場合は、`null` を指定できます。

   この `renderPDFForm` メソッドは、クライアントの web ブラウザーに書き込む必要があるフォームデータストリームを含む `FormsResult` オブジェクトを返します。

1. フォームデータストリームを使用してアクションを実行

   * `FormsResult` オブジェクトの `getOutputContent` メソッドを呼び出して、`com.adobe.idp.Document` オブジェクトを作成します。
   * `getContentType` メソッドを呼び出して `com.adobe.idp.Document` オブジェクトのコンテンツタイプを取得します。
   * `setContentType` メソッドを呼び出し、`com.adobe.idp.Document` オブジェクトのコンテンツタイプを渡して、`javax.servlet.http.HttpServletResponse` オブジェクトのコンテンツタイプを設定します。
   * `javax.servlet.http.HttpServletResponse` オブジェクトの `getOutputStream` メソッドを呼び出して、フォームデータストリームをクライアント web ブラウザーに書き出すために使用される `javax.servlet.ServletOutputStream` オブジェクトを作成します。
   * `com.adobe.idp.Document` オブジェクトの `getInputStream` メソッドを呼び出すことによって、`java.io.InputStream` オブジェクトを作成します。
   * バイト配列を作成し、`InputStream` オブジェクトの `read` メソッドを呼び出して、フォームデータストリームを入力します。 バイト配列を引数として渡します。
   * `javax.servlet.ServletOutputStream` オブジェクトの `write` メソッドを呼び出して、フォームデータストリームをクライアント web ブラウザーに送信します。バイト配列を `write` メソッドに渡します。

**関連トピック**

[クイックスタート（SOAP モード）：Java API を使用した、Forms サービスへのドキュメントの受け渡し](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Web サービス API を使用してドキュメントを Forms サービスに渡す {#pass-documents-to-the-forms-service-using-the-web-service-api}

Forms サービスおよびコンテンツサービス（非推奨） API（web サービス）を使用してコンテンツサービス（非推奨）から取得したドキュメントを渡すには、以下の手順を実行します。

1. プロジェクトファイルを含める

   MTOM を使用する Microsoft .NET プロジェクトを作成します。このクライアントアプリケーションは 2 つの AEM Forms サービスを呼び出すので、2 つのサービス参照を作成します。Forms サービスに関連付けられたサービス参照には、WSDL 定義 `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1` を使用します。

   Document Management サービスに関連付けられたサービス参照には、WSDL 定義 `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1` を使用します。

   これは、 `BLOB` データタイプは、両方のサービス参照に共通なので、これを使用すると `BLOB` データ型が完全に修飾されます。対応する web サービスのクイックスタートで、`BLOB` インスタンスは完全に修飾されています。

   >[!NOTE]
   >
   >`localhost` を AEM Forms をホストしているサーバーの IP アドレスに置き換えます。

1. Forms と Document Management Client API オブジェクトの作成

   * デフォルトのコンストラクターを使用して `FormsServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して `FormsServiceClient.Endpoint.Address` オブジェクトを作成します。AEM Forms サービスに WSDL を指定する文字列の値を渡します（例：`http://localhost:8080/soap/services/FormsService?WSDL`）。`lc_version` フィールド名を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトを作成するには、`FormsServiceClient.Endpoint.Binding` フィールドに入力します。戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` フィールドを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `FormsServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms のユーザー名を割り当てます。
      * `FormsServiceClient.ClientCredentials.UserName.Password` フィールドに対応するパスワード値を割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` をフィールド `BasicHttpBindingSecurity.Transport.ClientCredentialType` に割り当てます。
   * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` をフィールド `BasicHttpBindingSecurity.Security.Mode` に割り当てます。

   >[!NOTE]
   >
   >`DocumentManagementServiceClient` サービスクライアント向けに、以下の手順を繰り返します。

1. コンテンツサービス（非推奨）からフォームデザインを取得する

   `DocumentManagementServiceClient` オブジェクトの `retrieveContent` メソッドを呼び出し、以下の値を渡してコンテンツを取得します。

   * コンテンツの追加先となるストアを指定する文字列値です。 デフォルトのストアは `SpacesStore` です。この値は必須パラメーターです。
   * 取得するコンテンツの完全修飾パスを指定する string 値 ( 例： `/Company Home/Form Designs/Loan.xdp`) 。この値は必須パラメーターです。
   * バージョンを指定する文字列値。この値はオプションのパラメーターであり、空の文字列を渡すことができます。この場合、最新バージョンが取得されます。
   * 参照リンクの値を格納する文字列出力パラメーター。
   * コンテンツを格納する `BLOB` 出力パラメーター。 この出力パラメーターを使用して、コンテンツを取得できます。
   * コンテンツのフィールド名を格納する `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` 出力パラメーター。
   * `CRCResult` 出力パラメーター。 このオブジェクトを使用する代わりに、 `BLOB` 出力パラメーターを使用して、コンテンツを取得できます。

1. インタラクティブ PDF フォームのレンダリング

   `FormsServiceClient` オブジェクトの `renderPDFForm2` メソッドを呼び出して、次の値を渡します。

   * コンテンツサービス（非推奨）から取得したフォームデザインを含む `BLOB` オブジェクトです。
   * フォームに結合するデータを含む `BLOB` オブジェクトです。 データを結合しない場合は、空の `BLOB` オブジェクトを渡します。
   * 実行時オプションを保存する `PDFFormRenderSpec` オブジェクトです。この値はオプションのパラメーターで、実行時オプションを指定しない場合、`null` を指定できます。
   * URI 値を格納する `URLSpec` オブジェクトです。この値はオプションのパラメーターで、`null` を指定できます。
   * 添付ファイルを保存する `Map` オブジェクトです。この値はオプションのパラメーターで、フォームにファイルを添付しない場合は、`null` を指定できます。
   * ページ数の保存に使用される長い出力パラメーターです。
   * ロケール値の格納に使用される文字列出力パラメーターです。
   * インタラクティブ PDF フォーム `.` の保存に使用する `FormsResult` 出力パラメーター

   `renderPDFForm2` メソッドは、インタラクティブ PDF フォームを含む `FormsResult` オブジェクトを返します。

1. フォームデータストリームを使用してアクションを実行

   * `FormsResult` オブジェクトの `outputContent` フィールドの値を取得して、フォームデータを含む `BLOB` オブジェクトを作成します。
   * コンストラクターを呼び出して `System.IO.FileStream` オブジェクトを作成します。インタラクティブ PDF ドキュメントのファイルの場所と、ファイルを開くモードを表す文字列値を渡します。
   * `FormsResult` オブジェクトから取得した `BLOB` オブジェクトのコンテンツを格納するバイト配列を作成します。バイト配列を入力するには、`BLOB` オブジェクトの `MTOM` データメンバーの値を取得します。
   * コンストラクターを呼び出して `System.IO.FileStream` オブジェクトを渡すことによって、`System.IO.BinaryWriter` オブジェクトを作成します。
   * バイト配列のコンテンツを PDF ファイルに書き込むには、`System.IO.BinaryWriter` オブジェクトの `Write` メソッドを呼び出して、バイト配列を渡します。

**関連トピック**

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
