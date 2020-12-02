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


# Formsサービスにドキュメントを渡す{#passing-documents-to-the-formsservice}

AEM Formsサービスは、ユーザーから情報を収集するために、クライアントデバイス（通常はWebブラウザー）に対してインタラクティブなPDF formsをレンダリングします。 インタラクティブPDFフォームは、通常、XDPファイルとして保存され、Designerで作成されるフォームデザインに基づいています。 AEM Forms時点では、フォームデザインを含む`com.adobe.idp.Document`オブジェクトをFormsサービスに渡すことができます。 次に、Formsサービスは、`com.adobe.idp.Document`オブジェクト内のフォームデザインをレンダリングします。

`com.adobe.idp.Document`オブジェクトをFormsサービスに渡す利点は、他のサービス操作が`com.adobe.idp.Document`インスタンスを返すことです。 つまり、別のサービス操作から`com.adobe.idp.Document`インスタンスを取得し、それをレンダリングできます。 例えば、次の図に示すように、XDPファイルが`/Company Home/Form Designs`という名前のContent Services（非推奨）ノードに保存されているとします。

プログラムによってContent Services（非推奨）（非推奨）からLoan.xdpを取得し、`com.adobe.idp.Document`オブジェクト内のFormsサービスにXDPファイルを渡すことができます。

>[!NOTE]
>
>Formsサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

## 手順{#summary-of-steps}の概要

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

JavaまたはWebサービスAPIを使用して、Content Services（非推奨）からXDPファイルを取得します。 XDPファイルは、`com.adobe.idp.Document`インスタンス（Webサービスを使用している場合は`BLOB`インスタンス）内で返されます。 その後、`com.adobe.idp.Document`インスタンスをFormsサービスに渡すことができます。

**インタラクティブPDFフォームのレンダリング**

インタラクティブフォームをレンダリングするには、Content Services（非推奨）から返された`com.adobe.idp.Document`インスタンスをFormsサービスに渡します。

>[!NOTE]
>
>フォームデザインを含む`com.adobe.idp.Document`をFormsサービスに渡すことができます。 `renderPDFForm2`と`renderHTMLForm2`という2つの新しいメソッドは、フォームデザインを含む`com.adobe.idp.Document`オブジェクトを受け入れます。

**フォームデータストリームを使用したアクションの実行**

クライアントアプリケーションの種類に応じて、フォームをクライアントのWebブラウザーに書き込んだり、フォームをPDFファイルとして保存したりできます。 Webベースのアプリケーションは、通常、フォームをWebブラウザーに書き込みます。 ただし、通常、デスクトップアプリケーションはフォームをPDFファイルとして保存します。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[FormsサービスAPIクイック開始](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

## Java API {#pass-documents-to-the-forms-service-using-the-java-api}を使用してFormsサービスにドキュメントを渡す

FormsサービスおよびContent Services（非推奨）API(Java)を使用して、Content Services（非推奨）から取得したドキュメントを渡します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-forms-client.jarやadobe-contentservices-client.jarなどのクライアントJARファイルを含めます。

1. Formsとドキュメント管理クライアントAPIオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。（[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照。）
   * コンストラクターを使用し、`FormsServiceClient`オブジェクトを渡して、`ServiceClientFactory`オブジェクトを作成します。
   * コンストラクタを使用して `DocumentManagementServiceClientImpl` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. Content Services（非推奨）からフォームデザインを取得する

   `DocumentManagementServiceClientImpl`オブジェクトの`retrieveContent`メソッドを呼び出し、次の値を渡します。

   * コンテンツが追加されるストアを指定するstring値です。 デフォルトのストアは`SpacesStore`です。 この値は必須のパラメータです。
   * 取得するコンテンツの完全修飾パスを指定するstring値（例：`/Company Home/Form Designs/Loan.xdp`）。 この値は必須のパラメータです。
   * バージョンを指定するstring値。 この値はオプションのパラメーターであり、空の文字列を渡すことができます。 この場合、最新バージョンが取得されます。

   `retrieveContent`メソッドは、XDPファイルを含む`CRCResult`オブジェクトを返します。 `CRCResult`オブジェクトの`getDocument`メソッドを呼び出して、`com.adobe.idp.Document`インスタンスを取得します。

1. インタラクティブPDFフォームのレンダリング

   `FormsServiceClient`オブジェクトの`renderPDFForm2`メソッドを呼び出し、次の値を渡します。

   * Content Services（非推奨）から取得されたフォームデザインが含まれる`com.adobe.idp.Document`オブジェクト。
   * フォームとマージするデータを含む`com.adobe.idp.Document`オブジェクト。 データをマージしない場合は、空の`com.adobe.idp.Document`オブジェクトを渡します。
   * 実行時オプションを格納する`PDFFormRenderSpec`オブジェクト。 この値はオプションのパラメーターです。実行時のオプションを指定しない場合は、`null`を指定できます。
   * URI値を含む`URLSpec`オブジェクト。 この値はオプションのパラメータで、`null`を指定できます。
   * 添付ファイルを格納する`java.util.HashMap`オブジェクト。 この値はオプションのパラメーターです。フォームにファイルを添付しない場合は、`null`を指定できます。

   `renderPDFForm`メソッドは、クライアントのWebブラウザーに書き込む必要があるフォームデータストリームを含む`FormsResult`オブジェクトを返します。

1. フォームデータストリームを使用したアクションの実行

   * `FormsResult`オブジェクト&#39;s `getOutputContent`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトを作成します。
   * `getContentType`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトのコンテンツタイプを取得します。
   * `javax.servlet.http.HttpServletResponse`オブジェクトのコンテンツタイプを設定するには、`setContentType`メソッドを呼び出し、`com.adobe.idp.Document`オブジェクトのコンテンツタイプを渡します。
   * `javax.servlet.http.HttpServletResponse`オブジェクトの`getOutputStream`メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに書き込むために使用する`javax.servlet.ServletOutputStream`オブジェクトを作成します。
   * `com.adobe.idp.Document`オブジェクトの`getInputStream`メソッドを呼び出して、`java.io.InputStream`オブジェクトを作成します。
   * バイト配列を作成し、`InputStream`オブジェクトの`read`メソッドを呼び出して、フォームデータストリームを設定します。 バイト配列を引数として渡します。
   * `javax.servlet.ServletOutputStream`オブジェクトの`write`メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに送信します。 バイト配列を`write`メソッドに渡します。

**関連トピック**

[クイック開始（SOAPモード）:Java APIを使用してFormsサービスにドキュメントを渡す](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## WebサービスAPI {#pass-documents-to-the-forms-service-using-the-web-service-api}を使用してドキュメントをFormsサービスに渡す

FormsサービスとContent Services（非推奨）API（Webサービス）を使用して、Content Services（非推奨）から取得したドキュメントを渡します。

1. プロジェクトファイルを含める

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 このクライアントアプリケーションは2つのAEM Formsサービスを呼び出すので、2つのサービス参照を作成します。 Formsサービスに関連付けられたサービス参照には、次のWSDL定義を使用します。`http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   ドキュメント管理サービスに関連付けられたサービス参照に対して、次のWSDL定義を使用します。`http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`.

   `BLOB`データ型は両方のサービス参照に共通なので、`BLOB`データ型を使用する場合は完全に修飾します。 対応するWebサービスクイック開始では、すべての`BLOB`インスタンスが完全修飾されます。

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. Formsとドキュメント管理クライアントAPIオブジェクトの作成

   * `FormsServiceClient`オブジェクトを作成するには、そのデフォルトのコンストラクタを使用します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`FormsServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに指定するstring値を渡します（例：`http://localhost:8080/soap/services/FormsService?WSDL`）。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する場合に使用されます)。
   * `FormsServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * AEM formsユーザー名をフィールド`FormsServiceClient.ClientCredentials.UserName.UserName`に割り当てます。
      * 対応するパスワード値をフィールド`FormsServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * 定数値`HttpClientCredentialType.Basic`をフィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に割り当てます。
   * 定数値`BasicHttpSecurityMode.TransportCredentialOnly`をフィールド`BasicHttpBindingSecurity.Security.Mode`に割り当てます。

   >[!NOTE]
   >
   >`DocumentManagementServiceClient`サービスクライアントに対してこの手順を繰り返します。

1. Content Services（非推奨）からフォームデザインを取得する

   `DocumentManagementServiceClient`オブジェクトの`retrieveContent`メソッドを呼び出し、次の値を渡して、コンテンツを取得します。

   * コンテンツが追加されるストアを指定するstring値です。 デフォルトのストアは`SpacesStore`です。 この値は必須のパラメータです。
   * 取得するコンテンツの完全修飾パスを指定するstring値（例：`/Company Home/Form Designs/Loan.xdp`）。 この値は必須のパラメータです。
   * バージョンを指定するstring値。 この値はオプションのパラメーターであり、空の文字列を渡すことができます。 この場合、最新バージョンが取得されます。
   * ブラウズリンクの値を格納する文字列出力パラメーター。
   * コンテンツを格納する`BLOB`出力パラメーター。 この出力パラメーターを使用して、コンテンツを取得できます。
   * コンテンツ属性を格納する`ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType`出力パラメーター。
   * `CRCResult`出力パラメーター。 このオブジェクトを使用する代わりに、`BLOB`出力パラメーターを使用してコンテンツを取得できます。

1. インタラクティブPDFフォームのレンダリング

   `FormsServiceClient`オブジェクトの`renderPDFForm2`メソッドを呼び出し、次の値を渡します。

   * Content Services（非推奨）から取得されたフォームデザインが含まれる`BLOB`オブジェクト。
   * フォームとマージするデータを含む`BLOB`オブジェクト。 データをマージしない場合は、空の`BLOB`オブジェクトを渡します。
   * 実行時オプションを格納する`PDFFormRenderSpec`オブジェクト。 この値はオプションのパラメーターです。実行時のオプションを指定しない場合は、`null`を指定できます。
   * URI値を含む`URLSpec`オブジェクト。 この値はオプションのパラメータで、`null`を指定できます。
   * 添付ファイルを格納する`Map`オブジェクト。 この値はオプションのパラメーターです。フォームにファイルを添付しない場合は、`null`を指定できます。
   * ページ数の格納に使用される長い出力パラメーター。
   * ロケール値の格納に使用される文字列出力パラメーター。
   * インタラクティブPDFフォーム`.`の保存に使用される`FormsResult`出力パラメーター

   `renderPDFForm2`メソッドは、インタラクティブPDFフォームを含む`FormsResult`オブジェクトを返します。

1. フォームデータストリームを使用したアクションの実行

   * `FormsResult`オブジェクトの`outputContent`フィールドの値を取得して、フォームデータを含む`BLOB`オブジェクトを作成します。
   * コンストラクターを呼び出して、`System.IO.FileStream`オブジェクトを作成します。 インタラクティブPDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * `FormsResult`オブジェクトから取得した`BLOB`オブジェクトの内容を格納するバイト配列を作成します。 `BLOB`オブジェクトの`MTOM`データメンバの値を取得して、バイト配列を入力します。
   * コンストラクターを呼び出して`System.IO.FileStream`オブジェクトを渡し、`System.IO.BinaryWriter`オブジェクトを作成します。
   * `System.IO.BinaryWriter`オブジェクトの`Write`メソッドを呼び出し、バイト配列を渡すことで、バイト配列の内容をPDFファイルに書き込みます。

**関連トピック**

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
