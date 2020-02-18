---
title: FormsServiceへのドキュメントの引き渡し
seo-title: FormsServiceへのドキュメントの引き渡し
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

---


# Formsサービスへのドキュメントの引き渡し {#passing-documents-to-the-formsservice}

AEM Formsサービスは、ユーザーから情報を収集するために、インタラクティブPDFフォームをクライアントデバイス（通常はWebブラウザー）にレンダリングします。 インタラクティブPDFフォームは、通常XDPファイルとして保存され、Designerで作成されるフォームデザインに基づいています。 AEM Formsでは、フォームデザインを含むオブジ `com.adobe.idp.Document` ェクトをFormsサービスに渡すことができます。 次に、Formsサービスは、オブジェクト内のフォームデザインをレンダリング `com.adobe.idp.Document` します。

オブジェクトをFormsサービスに渡 `com.adobe.idp.Document` す利点の1つは、他のサービス操作がインスタンスを返すこと `com.adobe.idp.Document` です。 つまり、別のサービス操作からインスタンスを取 `com.adobe.idp.Document` 得し、それをレンダリングすることができます。 例えば、次の図に示すように、XDPファイルがという名前のContent Services（非推奨）ノードに `/Company Home/Form Designs`保存されているとします。

Content Services（非推奨）からLoan.xdpをプログラムで取得し、オブジェクト内のFormsサービスにXDPファイルを渡すことができ `com.adobe.idp.Document` ます。

>[!NOTE]
>
>For more information about the Forms service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## 手順の概要 {#summary-of-steps}

Content Services（非推奨）から取得したドキュメントをFormsサービスに渡すには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. FormsおよびDocument Management Client APIオブジェクトを作成します。
1. Content Services（非推奨）からフォームデザインを取得します。
1. インタラクティブPDFフォームをレンダリングします。
1. フォームデータストリームを使用してアクションを実行します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを含めます。

**FormsとDocument Management Client APIオブジェクトの作成**

プログラムでFormsサービスAPI操作を実行する前に、フォームクライアントAPIオブジェクトを作成します。 また、このワークフローはContent Services（非推奨）からXDPファイルを取得するので、Document Management APIオブジェクトを作成します。

**Content Services（非推奨）からフォームデザインを取得する**

JavaまたはWebサービスAPIを使用して、Content Services（非推奨）からXDPファイルを取得します。 XDPファイルは、インスタンス(Webサービ `com.adobe.idp.Document` スを使用している場 `BLOB` 合はインスタンス)内で返されます。 その後、このインスタンスをForms `com.adobe.idp.Document` サービスに渡すことができます。

**インタラクティブPDFフォームのレンダリング**

インタラクティブフォームをレンダリングするに `com.adobe.idp.Document` は、Content Services（非推奨）から返されたインスタンスをFormsサービスに渡します。

>[!NOTE]
>
>フォームデザインを含 `com.adobe.idp.Document` むフォームをFormsサービスに渡すことができます。 フォームデザインを含むオブジ `renderPDFForm2` ェクトの名 `renderHTMLForm2` 前と受け `com.adobe.idp.Document` 入れる2つの新しいメソッド。

**フォームデータストリームを使用したアクションの実行**

クライアントアプリケーションの種類に応じて、クライアントWebブラウザーにフォームを書き込んだり、フォームをPDFファイルとして保存したりできます。 Webベースのアプリケーションは、通常、Webブラウザーにフォームを書き込みます。 ただし、デスクトップアプリケーションは通常、フォームをPDFファイルとして保存します。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[FormsサービスAPIのクイックスタート](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

## Java APIを使用したFormsサービスへのドキュメントの渡し {#pass-documents-to-the-forms-service-using-the-java-api}

FormsサービスとContent Services（非推奨）API(Java)を使用して、Content Services（非推奨）から取得したドキュメントを渡します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-forms-client.jarやadobe-contentservices-client.jarなどのクライアントJARファイルを含めます。

1. FormsとDocument Management Client APIオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。（[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照。）
   * Create an `FormsServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.
   * コンストラクタを使用して `DocumentManagementServiceClientImpl` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. Content Services（非推奨）からフォームデザインを取得する

   オブジェクト `DocumentManagementServiceClientImpl` のメソッドを `retrieveContent` 呼び出し、次の値を渡します。

   * コンテンツが追加されるストアを指定するstring値。 The default store is `SpacesStore`. この値は必須パラメーターです。
   * 取得するコンテンツの完全修飾パスを指定するstring値(例 `/Company Home/Form Designs/Loan.xdp`えば)。 この値は必須パラメーターです。
   * バージョンを指定するstring値。 この値はオプションのパラメーターで、空の文字列を渡すことができます。 この場合、最新バージョンが取得されます。
   このメ `retrieveContent` ソッドは、XDPファ `CRCResult` イルを含むオブジェクトを返します。 オブジェクトの `com.adobe.idp.Document` メソッドを呼び出して、イ `CRCResult` ンスタンスを取得 `getDocument` します。

1. インタラクティブPDFフォームのレンダリング

   オブジェクト `FormsServiceClient` のメソッドを `renderPDFForm2` 呼び出し、次の値を渡します。

   * Content Services( `com.adobe.idp.Document` 非推奨)から取得したフォームデザインを含むオブジェクトです。
   * フォーム `com.adobe.idp.Document` とマージするデータを含むオブジェクトです。 データをマージしない場合は、空のオブジェクトを渡し `com.adobe.idp.Document` ます。
   * 実行時 `PDFFormRenderSpec` のオプションを格納するオブジェクトです。 この値はオプションのパラメーターで、実行時のオ `null` プションを指定しないかどうかを指定できます。
   * URI値を `URLSpec` 含むオブジェクトです。 この値はオプションのパラメーターで、指定できま `null`す。
   * 添付フ `java.util.HashMap` ァイルを格納するオブジェクト。 この値はオプションのパラメーターで、フォームにフ `null` ァイルを添付しないかどうかを指定できます。
   このメソ `renderPDFForm` ッドは、クライア `FormsResult` ントのWebブラウザーに書き込む必要があるフォームデータストリームを含むオブジェクトを返します。

1. フォームデータストリームを使用したアクションの実行

   * オブジェクトの `com.adobe.idp.Document` メソッドを呼び出して、オ `FormsResult` ブジェクトを作成 `getOutputContent` します。
   * メソッドを呼び出して、オブジェ `com.adobe.idp.Document` クトのコンテンツタイプを取得 `getContentType` します。
   * メソッドを呼 `javax.servlet.http.HttpServletResponse` び出し、オブジェクトのコンテンツタ `setContentType` イプを渡すことで、オブジェクトのコンテンツタイプを設定 `com.adobe.idp.Document` します。
   * オブジェクトの `javax.servlet.ServletOutputStream` メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに書き込むために使用する `javax.servlet.http.HttpServletResponse` オブジェクトを作 `getOutputStream` 成します。
   * オブジェクト `java.io.InputStream` のメソッドを呼び出して、オ `com.adobe.idp.Document` ブジェクトを作成 `getInputStream` します。
   * バイト配列を作成し、オブジェクトのメソッドを呼び出してフォームデータストリ `InputStream` ームを設定 `read` します。 バイト配列を引数として渡します。
   * オブジェクト `javax.servlet.ServletOutputStream` のメソッドを呼び `write` 出して、フォームデータストリームをクライアントWebブラウザーに送信します。 バイト配列をメソッドに渡し `write` ます。

**関連トピック**

[クイックスタート（SOAPモード）:Java APIを使用してFormsサービスにドキュメントを渡す](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## WebサービスAPIを使用してFormsサービスにドキュメントを渡す {#pass-documents-to-the-forms-service-using-the-web-service-api}

FormsサービスとContent Services（非推奨）API（Webサービス）を使用して、Content Services（非推奨）から取得したドキュメントを渡します。

1. プロジェクトファイルを含める

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 このクライアントアプリケーションは2つのAEM Formsサービスを呼び出すので、2つのサービス参照を作成します。 Formsサービスに関連付けられているサービス参照に対して、次のWSDL定義を使用します。 `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   Document Managementサービスに関連付けられているサービス参照に対して、次のWSDL定義を使用します。 `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`.

   このデータ `BLOB` 型は両方のサービス参照に共通なので、使用する際にはデータ型 `BLOB` を完全に修飾してください。 対応するWebサービスのクイックスタートでは、すべてのインスタ `BLOB` ンスが完全修飾されています。

   >[!NOTE]
   >
   >AEM Formsをホ `localhost`ストするサーバーのIPアドレスに置き換えます。

1. FormsとDocument Management Client APIオブジェクトの作成

   * Create a `FormsServiceClient` object by using its default constructor.
   * Create a `FormsServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/FormsService?WSDL`)に渡すstring値。 属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。)
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `FormsServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `FormsServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `FormsServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
   * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。
   >[!NOTE]
   >
   >サービスクライアントに対して、この手順 `DocumentManagementServiceClient`を繰り返します。

1. Content Services（非推奨）からフォームデザインを取得する

   オブジェクトのメソッドを呼び出し、 `DocumentManagementServiceClient` 次の値を渡 `retrieveContent` して、コンテンツを取得します。

   * コンテンツが追加されるストアを指定するstring値。 The default store is `SpacesStore`. この値は必須パラメーターです。
   * 取得するコンテンツの完全修飾パスを指定するstring値(例 `/Company Home/Form Designs/Loan.xdp`えば)。 この値は必須パラメーターです。
   * バージョンを指定するstring値。 この値はオプションのパラメーターで、空の文字列を渡すことができます。 この場合、最新バージョンが取得されます。
   * ブラウズリンクの値を格納する文字列出力パラメータ。
   * コンテ `BLOB` ンツを保存する出力パラメーター。 この出力パラメーターを使用して、コンテンツを取得できます。
   * コンテンツ `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` 属性を格納する出力パラメーター。
   * 出力パ `CRCResult` ラメーター。 このオブジェクトを使用する代わりに、出力パラメーターを使用し `BLOB` てコンテンツを取得することができます。

1. インタラクティブPDFフォームのレンダリング

   オブジェクト `FormsServiceClient` のメソッドを `renderPDFForm2` 呼び出し、次の値を渡します。

   * Content Services( `BLOB` 非推奨)から取得したフォームデザインを含むオブジェクトです。
   * フォーム `BLOB` とマージするデータを含むオブジェクトです。 データをマージしない場合は、空のオブジェクトを渡し `BLOB` ます。
   * 実行時 `PDFFormRenderSpec` のオプションを格納するオブジェクトです。 この値はオプションのパラメーターで、実行時のオ `null` プションを指定しないかどうかを指定できます。
   * URI値を `URLSpec` 含むオブジェクトです。 この値はオプションのパラメーターで、指定できま `null`す。
   * 添付フ `Map` ァイルを格納するオブジェクト。 この値はオプションのパラメーターで、フォームにフ `null` ァイルを添付しないかどうかを指定できます。
   * ページ数の保存に使用される長い出力パラメーター。
   * ロケール値の格納に使用される文字列出力パラメーター。
   * インタラ `FormsResult` クティブPDFフォームの保存に使用される出力パラメーター `.`
   このメソ `renderPDFForm2` ッドは、インタラクティブPDF `FormsResult` フォームを含むオブジェクトを返します。

1. フォームデータストリームを使用したアクションの実行

   * オブジェクト `BLOB` のフィールドの値を取得して、フォームデータを含むオブジ `FormsResult` ェクトを作成 `outputContent` します。
   * Create a `System.IO.FileStream` object by invoking its constructor. インタラクティブPDFドキュメントのファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * オブジェクトから取得したオブジェクトの内容を格納す `BLOB` るバイト配列を作成 `FormsResult` します。 オブジェクトのデータメンバーの値を取得して、バ `BLOB` イト配列を `MTOM` 設定します。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡すことで、バ `System.IO.BinaryWriter` イト配列の内 `Write` 容をPDFファイルに書き込みます。

**関連トピック**

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
