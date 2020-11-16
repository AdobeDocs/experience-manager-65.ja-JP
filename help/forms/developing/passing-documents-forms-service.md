---
title: FormsServiceにドキュメントを渡す
seo-title: FormsServiceにドキュメントを渡す
description: 'null'
seo-description: 'null'
uuid: 841e97f3-ebb8-4340-81a9-b6db11f0ec82
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: e23de3c3-f8a0-459f-801e-a0942fb1c6aa
translation-type: tm+mt
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d
workflow-type: tm+mt
source-wordcount: '1652'
ht-degree: 3%

---


# Formsサービスにドキュメントを渡す {#passing-documents-to-the-formsservice}

AEM Formsサービスは、ユーザーから情報を収集するために、クライアントデバイス（通常はWebブラウザー）に対してインタラクティブなPDF formsをレンダリングします。 インタラクティブPDFフォームは、通常、XDPファイルとして保存され、Designerで作成されるフォームデザインに基づいています。 AEM Forms時点では、フォームデザインを含む `com.adobe.idp.Document` オブジェクトをFormsサービスに渡すことができます。 次に、Formsサービスは、 `com.adobe.idp.Document` オブジェクト内のフォームデザインをレンダリングします。

オブジェクトをFormsサービスに渡す利点の1つは、 `com.adobe.idp.Document` 他のサービス操作がインスタンスを返すことで `com.adobe.idp.Document` す。 つまり、別のサービス操作から `com.adobe.idp.Document` インスタンスを取得してレンダリングできます。 例えば、次の図に示すように、XDPファイルがという名前のContent Services（非推奨）ノードに格納されている `/Company Home/Form Designs`とします。

プログラムを使用してContent Services（非推奨）（非推奨）からLoan.xdpを取得し、XDPファイルを `com.adobe.idp.Document` オブジェクト内のFormsサービスに渡すことができます。

>[!NOTE]
>
>For more information about the Forms service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## 手順の概要 {#summary-of-steps}

Content Services（非推奨）から取得したドキュメントをFormsサービスに渡すには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Formsおよびドキュメント管理クライアントAPIオブジェクトを作成します。
1. Content Services（非推奨）からフォームデザインを取得します。
1. インタラクティブPDFフォームをレンダリングします。
1. フォームデータストリームでアクションを実行します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを含めます。

**Formsとドキュメント管理クライアントAPIオブジェクトの作成**

プログラムでFormsサービスAPI操作を実行する前に、FormsクライアントAPIオブジェクトを作成します。 また、このワークフローはContent Services（非推奨）からXDPファイルを取得するので、ドキュメント管理APIオブジェクトを作成します。

**Content Services（非推奨）からフォームデザインを取得する**

JavaまたはWebサービスAPIを使用して、Content Services（非推奨）からXDPファイルを取得します。 XDPファイルは、インスタンス(Webサービスを使用している場合は `com.adobe.idp.Document` インスタンス)内で返され `BLOB` ます。 その後、この `com.adobe.idp.Document` インスタンスをFormsサービスに渡すことができます。

**インタラクティブPDFフォームのレンダリング**

インタラクティブフォームをレンダリングするには、Content Services（非推奨）から返された `com.adobe.idp.Document` インスタンスをFormsサービスに渡します。

>[!NOTE]
>
>フォームデザインを含むフォーム `com.adobe.idp.Document` をFormsサービスに渡すことができます。 フォームデザインを含む `renderPDFForm2` オブジェクトを、という名前で `renderHTMLForm2``com.adobe.idp.Document` 受け入れる2つの新しいメソッドが追加されました。

**フォームデータストリームを使用したアクションの実行**

クライアントアプリケーションの種類に応じて、フォームをクライアントのWebブラウザーに書き込んだり、フォームをPDFファイルとして保存したりできます。 Webベースのアプリケーションは、通常、フォームをWebブラウザーに書き込みます。 ただし、通常、デスクトップアプリケーションはフォームをPDFファイルとして保存します。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[FormsサービスAPIクイック開始](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

## Java APIを使用してFormsサービスにドキュメントを渡す {#pass-documents-to-the-forms-service-using-the-java-api}

FormsサービスおよびContent Services（非推奨）API(Java)を使用して、Content Services（非推奨）から取得したドキュメントを渡します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-forms-client.jarやadobe-contentservices-client.jarなどのクライアントJARファイルを含めます。

1. Formsとドキュメント管理クライアントAPIオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。（[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照。）
   * Create an `FormsServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.
   * コンストラクタを使用して `DocumentManagementServiceClientImpl` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. Content Services（非推奨）からフォームデザインを取得する

   オブジェクトの `DocumentManagementServiceClientImpl``retrieveContent` メソッドを呼び出し、次の値を渡します。

   * コンテンツが追加されるストアを指定するstring値です。 The default store is `SpacesStore`. この値は必須のパラメータです。
   * 取得するコンテンツの完全修飾パスを指定するstring値(例えば、 `/Company Home/Form Designs/Loan.xdp`)。 この値は必須のパラメータです。
   * バージョンを指定するstring値。 この値はオプションのパラメーターであり、空の文字列を渡すことができます。 この場合、最新バージョンが取得されます。

   この `retrieveContent` メソッドは、XDPファイルを含む `CRCResult` オブジェクトを返します。 オブジェクトの `com.adobe.idp.Document` メソッドを呼び出して、 `CRCResult` インスタンスを取得し `getDocument` ます。

1. インタラクティブPDFフォームのレンダリング

   オブジェクトの `FormsServiceClient``renderPDFForm2` メソッドを呼び出し、次の値を渡します。

   * Content Services（非推奨）から取得されたフォームデザインを含む `com.adobe.idp.Document` オブジェクトです。
   * フォームとマージするデータを含む `com.adobe.idp.Document` オブジェクト。 データをマージしない場合は、空の `com.adobe.idp.Document` オブジェクトを渡します。
   * 実行時オプションを格納する `PDFFormRenderSpec` オブジェクト。 この値はオプションのパラメーターです。実行時のオプションを指定しない `null` かどうかを指定できます。
   * URI値を含む `URLSpec` オブジェクト。 この値はオプションのパラメーターで、指定でき `null`ます。
   * 添付ファイルを格納する `java.util.HashMap` オブジェクトです。 この値はオプションのパラメーターです。フォームにファイルを添付しない `null` かどうかを指定できます。

   この `renderPDFForm``FormsResult` メソッドは、クライアントのWebブラウザーに書き込む必要があるフォームデータストリームを含むオブジェクトを返します。

1. フォームデータストリームを使用したアクションの実行

   * オブジェクトの `com.adobe.idp.Document` メソッドを呼び出して、 `FormsResult` オブジェクトを作成し `getOutputContent` ます。
   * メソッドを呼び出して、 `com.adobe.idp.Document` オブジェクトのコンテンツタイプを取得し `getContentType` ます。
   * メソッドを呼び出し、オブジェクトの `javax.servlet.http.HttpServletResponse` コンテンツタイプを渡すことで、 `setContentType``com.adobe.idp.Document` オブジェクトのコンテンツタイプを設定します。
   * オブジェクトの `javax.servlet.ServletOutputStream` メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに書き込むために使用する `javax.servlet.http.HttpServletResponse``getOutputStream` オブジェクトを作成します。
   * オブジェクトの `java.io.InputStream` メソッドを呼び出して、 `com.adobe.idp.Document` オブジェクトを作成 `getInputStream` します。
   * バイト配列を作成し、 `InputStream` オブジェクトの `read` メソッドを呼び出して、フォームデータストリームを設定します。 バイト配列を引数として渡します。
   * オブジェクトの `javax.servlet.ServletOutputStream``write` メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに送信します。 バイト配列を `write` メソッドに渡します。

**関連トピック**

[クイック開始（SOAPモード）:Java APIを使用してFormsサービスにドキュメントを渡す](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## WebサービスAPIを使用してFormsサービスにドキュメントを渡す {#pass-documents-to-the-forms-service-using-the-web-service-api}

FormsサービスとContent Services（非推奨）API（Webサービス）を使用して、Content Services（非推奨）から取得したドキュメントを渡します。

1. プロジェクトファイルを含める

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 このクライアントアプリケーションは2つのAEM Formsサービスを呼び出すので、2つのサービス参照を作成します。 Formsサービスに関連付けられたサービス参照には、次のWSDL定義を使用します。 `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   ドキュメント管理サービスに関連付けられたサービス参照に対して、次のWSDL定義を使用します。 `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`.

   この `BLOB` データ型は両方のサービス参照に共通なので、使用する場合は `BLOB` データ型を完全に限定します。 対応するWebサービスクイック開始では、すべての `BLOB` インスタンスが完全修飾されます。

   >[!NOTE]
   >
   >AEM Forms `localhost`をホストするサーバーのIPアドレスに置き換えます。

1. Formsとドキュメント管理クライアントAPIオブジェクトの作成

   * Create a `FormsServiceClient` object by using its default constructor.
   * Create a `FormsServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/FormsService?WSDL`)に指定するstring値を渡します。 属性を使用する必要はありません `lc_version` 。 この属性は、サービス参照を作成する場合に使用されます)。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `FormsServiceClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当て `FormsServiceClient.ClientCredentials.UserName.UserName`ます。
      * 対応するパスワード値をフィールドに割り当て `FormsServiceClient.ClientCredentials.UserName.Password`ます。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
   * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当て `BasicHttpBindingSecurity.Security.Mode`ます。

   >[!NOTE]
   >
   >サー `DocumentManagementServiceClient`ビスクライアントに対して、この手順を繰り返します。

1. Content Services（非推奨）からフォームデザインを取得する

   オブジェクトのメソッドを呼び出し、次の値を渡して、 `DocumentManagementServiceClient``retrieveContent` コンテンツを取得します。

   * コンテンツが追加されるストアを指定するstring値です。 The default store is `SpacesStore`. この値は必須のパラメータです。
   * 取得するコンテンツの完全修飾パスを指定するstring値(例えば、 `/Company Home/Form Designs/Loan.xdp`)。 この値は必須のパラメータです。
   * バージョンを指定するstring値。 この値はオプションのパラメーターであり、空の文字列を渡すことができます。 この場合、最新バージョンが取得されます。
   * ブラウズリンクの値を格納する文字列出力パラメーター。
   * コンテンツを格納する `BLOB` 出力パラメーター。 この出力パラメーターを使用して、コンテンツを取得できます。
   * コンテンツ属性を格納する `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` 出力パラメーター。
   * 出 `CRCResult` 力パラメータ。 このオブジェクトを使用する代わりに、 `BLOB` 出力パラメーターを使用してコンテンツを取得できます。

1. インタラクティブPDFフォームのレンダリング

   オブジェクトの `FormsServiceClient``renderPDFForm2` メソッドを呼び出し、次の値を渡します。

   * Content Services（非推奨）から取得されたフォームデザインを含む `BLOB` オブジェクトです。
   * フォームとマージするデータを含む `BLOB` オブジェクト。 データをマージしない場合は、空の `BLOB` オブジェクトを渡します。
   * 実行時オプションを格納する `PDFFormRenderSpec` オブジェクト。 この値はオプションのパラメーターです。実行時のオプションを指定しない `null` かどうかを指定できます。
   * URI値を含む `URLSpec` オブジェクト。 この値はオプションのパラメーターで、指定でき `null`ます。
   * 添付ファイルを格納する `Map` オブジェクトです。 この値はオプションのパラメーターです。フォームにファイルを添付しない `null` かどうかを指定できます。
   * ページ数の格納に使用される長い出力パラメーター。
   * ロケール値の格納に使用される文字列出力パラメーター。
   * インタラクティブPDFフォームの保存に使用される `FormsResult` 出力パラメーター `.`

   この `renderPDFForm2` メソッドは、インタラクティブPDFフォームを含む `FormsResult` オブジェクトを返します。

1. フォームデータストリームを使用したアクションの実行

   * オブジェクトのフィ `BLOB` ールドの値を取得して、フォームデータを含む `FormsResult` オブジェクトを作成し `outputContent` ます。
   * Create a `System.IO.FileStream` object by invoking its constructor. インタラクティブPDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトから取得した `BLOB` オブジェクトの内容を格納するバイト配列を作成し `FormsResult` ます。 オブジェクトのデータメンバーの値を取得して、 `BLOB` バイト配列を入力し `MTOM` ます。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡して、バイト配列の内容をPDFファイルに書き込み `System.IO.BinaryWriter` ま `Write` す。

**関連トピック**

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
