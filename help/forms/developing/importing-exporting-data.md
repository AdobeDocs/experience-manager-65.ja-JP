---
title: データの読み込みと書き出し
seo-title: データの読み込みと書き出し
description: 'null'
seo-description: 'null'
uuid: 94ccb6f2-6e5f-43ea-a954-9a4402871a17
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 2e783745-c986-45ba-8e65-7437d114ca38
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# データの読み込みと書き出し {#importing-and-exporting-data}

## Form Data Integration Serviceについて {#about-the-form-data-integration-service}

Form Data Integrationサービスでは、データをPDFフォームに読み込み、PDFフォームからデータを書き出すことができます。 読み込み操作と書き出し操作では、次の2種類のPDFフォームがサポートされます。

* Acrobatフォーム（Acrobatで作成）は、フォームフィールドを含むPDFドキュメントです。
* Adobe XMLフォーム（Designerで作成）は、XML Adobe XMLフォームアーキテクチャ(XFA)に準拠したPDFドキュメントです。

フォームデータは、PDFフォームの種類に応じて、次のいずれかの形式で存在する場合があります。

* XFDF ファイル。Acrobat フォームデータ形式の XML バージョンです。
* XDP ファイル。フォームフィールド定義を含む XML ファイルです。フォームフィールドデータと埋め込まれた PDF ファイルが含まれる場合もあります。Designerで生成されたXDPファイルは、埋め込みのbase-64エンコードPDFドキュメントを使用する場合にのみ使用できます。

Form Data Integrationサービスを使用して、次のタスクを実行できます。

* PDFフォームへのデータの読み込み 詳しくは、「フォームデータ [の読み込み」を参照してくださ](importing-exporting-data.md#importing-form-data)い。
* PDFフォームからのデータの書き出し 詳しくは、「フォームデータの書 [き出し」を参照してくださ](importing-exporting-data.md#exporting-form-data)い。

>[!NOTE]
>
>For more information about the Form Data Integration service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## フォームデータの読み込み {#importing-form-data}

Form Data Integrationサービスを使用して、インタラクティブPDFフォームにフォームデータを読み込むことができます。 インタラクティブPDFフォームとは、ユーザーから情報を収集したり、カスタム情報を表示したりするための1つ以上のフィールドを含むPDFドキュメントです。 Form Data Integrationサービスは、フォームの演算、検証、スクリプティングをサポートしていません。

Designerで作成したフォームにデータを読み込むには、有効なXDP XMLデータソースを参照する必要があります。 次の住宅ローン申し込みフォームの例を考えてみましょう。

![ie_ie_loanformdata](assets/ie_ie_loanformdata.png)

このフォームにデータ値を読み込むには、フォームに対応する有効なXDP XMLデータソースが必要です。 任意のXMLデータソースを使用して、Form Data Integrationサービスを使用してフォームにデータを読み込むことはできません。 任意のXMLデータソースとXDP XMLデータソースの違いは、XDPデータソースがXMLフォームアーキテクチャ(XFA)に準拠していることです。 次のXMLは、住宅ローン申込フォームの例に対応するXDP XMLデータソースを表しています。

```as3
 <?xml version="1.0" encoding="UTF-8" ?>
 - <xfa:datasets xmlns:xfa="https://www.xfa.org/schema/xfa-data/1.0/">
 - <xfa:data>
 - <data>
     - <Layer>
         <closeDate>1/26/2007</closeDate>
         <lastName>Johnson</lastName>
         <firstName>Jerry</firstName>
         <mailingAddress>JJohnson@NoMailServer.com</mailingAddress>
         <city>New York</city>
         <zipCode>00501</zipCode>
         <state>NY</state>
         <dateBirth>26/08/1973</dateBirth>
         <middleInitials>D</middleInitials>
         <socialSecurityNumber>(555) 555-5555</socialSecurityNumber>
         <phoneNumber>5555550000</phoneNumber>
     </Layer>
     - <Mortgage>
         <mortgageAmount>295000.00</mortgageAmount>
         <monthlyMortgagePayment>1724.54</monthlyMortgagePayment>
         <purchasePrice>300000</purchasePrice>
         <downPayment>5000</downPayment>
         <term>25</term>
         <interestRate>5.00</interestRate>
     </Mortgage>
 </data>
 </xfa:data>
 </xfa:datasets>
```

>[!NOTE]
>
>For more information about the Form Data Integration service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary-of-steps}

フォームデータをPDFフォームに読み込むには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Form Data Integrationサービスクライアントを作成します。
1. PDFフォームの参照。
1. XMLデータソースを参照します。
1. PDFフォームにデータを読み込みます。
1. PDFフォームをPDFファイルとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar（AEM FormsがJBossにデプロイされている場合に必須）
* jbossall-client.jar（AEM FormsがJBossにデプロイされている場合は必須）

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Form Data Integrationサービスクライアントの作成**

プログラムでデータをPDFフォームのクライアントAPIに読み込む前に、Data Integrationサービスクライアントを作成する必要があります。 サービスクライアントを作成する場合は、サービスの呼び出しに必要な接続設定を定義します。 詳しくは、接続プロパティ [の設定を参照してくださ](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)い。

**PDFフォームの参照**

PDFフォームにデータを読み込むには、Designerで作成されたXMLフォームまたはAcrobatで作成されたAcrobatフォームを参照する必要があります。

**XMLデータソースの参照**

フォームデータを読み込むには、有効なデータソースを参照する必要があります。 Designerで作成したXFA XMLフォームにデータを読み込むには、XDP XMLデータソースを使用する必要があります。 Acrobatフォームを参照する場合は、XFDFデータソースを使用する必要があります。 データの読み込み先の各フィールドに対して、値を指定する必要があります。 XMLデータソース内の要素がフォーム内のフィールドに対応していない場合、その要素は無視されます。

**PDFフォームへのデータの読み込み**

PDFフォームと有効なXMLデータソースを参照した後、データをPDFフォームに読み込むことができます。

**PDFフォームをPDFファイルとして保存**

データをフォームに読み込んだ後、フォームをPDFファイルとして保存できます。 PDFファイルとして保存したフォームは、Adobe ReaderまたはAcrobatで開き、読み込んだデータを含むフォームを表示できます。

**関連トピック**

[Java APIを使用したフォームデータの読み込み](importing-exporting-data.md#import-form-data-using-the-java-api)

[WebサービスAPIを使用したフォームデータの読み込み](importing-exporting-data.md#import-form-data-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Form Data Integration Service APIクイックスタート](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[フォームデータの書き出し](importing-exporting-data.md#exporting-form-data)

### Java APIを使用したフォームデータの読み込み {#import-form-data-using-the-java-api}

Form Data Integration API(Java)を使用してフォームデータを読み込みます。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-formdataintegration-client.jarなどのクライアントJARファイルを含めます。

1. Form Data Integrationサービスクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `FormDataIntegrationClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. PDFフォームの参照。

   * コンストラクタを使用して `java.io.FileInputStream` オブジェクトを作成します。PDFフォームの場所を指定するstring値を渡します。
   * コンストラク `com.adobe.idp.Document` ターを使用して、PDFフォームを保存するオブジェクトを作成 `com.adobe.idp.Document` します。 PDFフォームを `java.io.FileInputStream` 含むオブジェクトをコンストラクターに渡します。

1. XMLデータソースを参照します。

   * オブジェクト `java.io.FileInputStream` を作成するには、コンストラクターを使用し、フォームに読み込むデータを含むXMLファイルの場所を指定するstring値を渡します。
   * コンストラクタ `com.adobe.idp.Document` ーを使用して、フォームデータを格納するオブジェクトを作成 `com.adobe.idp.Document` します。 フォームデー `java.io.FileInputStream` タを含むオブジェクトをコンストラクターに渡します。

1. PDFフォームにデータを読み込みます。

   オブジェクトのメソッドを呼び出し、次 `FormDataIntegrationClient` の値を渡して、PDF `importData` フォームにデータを読み込みます。

   * PDFフ `com.adobe.idp.Document` ォームを保存するオブジェクトです。
   * フォーム `com.adobe.idp.Document` データを格納するオブジェクトです。
   このメ `importData` ソッドは、XMLデ `com.adobe.idp.Document` ータソース内のデータを含むPDFフォームを格納するオブジェクトを返します。

1. PDFフォームをPDFファイルとして保存します。

   * Create a `java.io.File` object and ensure that the file extension is “.PDF”.
   * オブジェクト `Document` のメソッドを呼び出 `copyToFile` して、オブジェクトの内容をファイルにコピ `Document` ーします(メソッドによって返されたオブジェクトを使用 `Document` していることを確 `importData` 認します)。

**関連トピック**

[手順の概要](importing-exporting-data.md#summary-of-steps)

[クイックスタート（SOAPモード）:Java APIを使用したフォームデータの読み込み](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-importing-form-data-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したフォームデータの読み込み {#import-form-data-using-the-web-service-api}

Form Data Integration API（Webサービス）を使用してフォームデータを読み込みます。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. Form Data Integrationサービスクライアントを作成します。

   * Create a `FormDataIntegrationClient` object by using its default constructor.
   * Create a `FormDataIntegrationClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLを指定するstring値をAEM Formsサービスに渡します(例 `http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`:)。属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。 ただし、MTOMを使用す `?blob=mtom` るように指定します。
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `FormDataIntegrationClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `FormDataIntegrationClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `FormDataIntegrationClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. PDFフォームの参照。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、PDFフォームの保存に使用されます。
   * Create a `System.IO.FileStream` object by invoking its constructor. PDFフォームの場所とファイルを開くモードを指定するstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出して、バイト配列にストリームデ `System.IO.FileStream` ータを入力 `Read` します。 読み取るバイト配列、開始位置およびストリーム長を渡します。
   * オブジェクト `BLOB` にバイト配列の内容を `MTOM` フィールドに割り当てて、オブジェクトを入力します。

1. XMLデータソースを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、フォームに読み込まれるデータを保存するために使用します。
   * Create a `System.IO.FileStream` object by invoking its constructor. 読み込むデータが含まれるXMLファイルの場所と、ファイルを開くモードを指定するstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出して、バイト配列にストリームデ `System.IO.FileStream` ータを入力 `Read` します。 読み取るバイト配列、開始位置およびストリーム長を渡します。
   * オブジェクト `BLOB` にバイト配列の内容を `MTOM` フィールドに割り当てて、オブジェクトを入力します。

1. PDFフォームにデータを読み込みます。

   オブジェクトのメソッドを呼び出し、次の値を `FormDataIntegrationClient` 渡して、PDFフォ `importData` ームにデータを読み込みます。

   * PDFフ `BLOB` ォームを保存するオブジェクトです。
   * フォーム `BLOB` データを格納するオブジェクトです。
   このメ `importData` ソッドは、XMLデ `BLOB` ータソース内のデータを含むPDFフォームを格納するオブジェクトを返します。

1. PDFフォームをPDFファイルとして保存します。

   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、PDFファイルのファイルの場所を表すstring値を渡します。
   * メソッドによって返されたオブジェクトのデータ内容を格納 `BLOB` するバイト配列を作成 `importData` します。 オブジェクトのフィールドの値を取得して、バイト `BLOB` 配列を設定し `MTOM` ます。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡すことで、バ `System.IO.BinaryWriter` イト配列の内 `Write` 容をPDFファイルに書き込みます。

**関連トピック**

[手順の概要](importing-exporting-data.md#summary-of-steps)

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## フォームデータの書き出し {#exporting-form-data}

Form Data Integrationサービスを使用して、インタラクティブPDFフォームからフォームデータを書き出すことができます。 書き出されるデータの形式は、フォームの種類によって異なります。 フォームの種類がAcrobatで作成されたAcrobatフォームの場合、書き出されるデータはXFDFです。 フォームの種類がDesignerで作成されたXMLフォームの場合、書き出されたデータはXDPになります。

>[!NOTE]
>
>For more information about the Form Data Integration service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-1}

PDFフォームからフォームデータを書き出すには、次の手順を実行します。

1. プロジェクトファイルを含める
1. Form Data Integrationサービスクライアントを作成します。
1. PDFフォームの参照。
1. PDFフォームからデータを書き出します。
1. 書き出したデータをXMLファイルとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar（AEM FormsがJBossにデプロイされている場合に必須）
* jbossall-client.jar（AEM FormsがJBossにデプロイされている場合は必須）

**Form Data Integrationサービスクライアントの作成**

プログラムでデータをPDF formClient APIに読み込む前に、Data Integrationサービスクライアントを作成する必要があります。 サービスクライアントを作成する場合は、サービスの呼び出しに必要な接続設定を定義します。 詳しくは、接続プ [ロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。

**PDFフォームの参照**

PDFフォームからデータを書き出すには、DesignerまたはAcrobatで作成され、フォームデータを含むPDFフォームを参照する必要があります。 空のPDFフォームからデータを書き出そうとすると、空のXMLスキーマが取得されます。

**PDFフォームからのデータの書き出し**

フォームデータを含むPDFフォームを参照した後、フォームからデータを書き出すことができます。 データは、フォームに基づくXMLスキーマ内で書き出されます。

**フォームデータをXMLファイルとして保存**

フォームデータを書き出した後、データをXMLファイルとして保存できます。 XMLファイルとして保存したXMLファイルをXMLビューアで開いて、フォームデータを表示できます。

**関連トピック**

[Java APIを使用したフォームデータの書き出し](importing-exporting-data.md#export-form-data-using-the-java-api)

[WebサービスAPIを使用したフォームデータの書き出し](importing-exporting-data.md#export-form-data-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Form Data Integration Service APIクイックスタート](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[フォームデータの読み込み](importing-exporting-data.md#importing-form-data)

### Java APIを使用したフォームデータの書き出し {#export-form-data-using-the-java-api}

Form Data Integration API(Java)を使用してフォームデータを書き出すには：

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-formdataintegration-client.jarなどのクライアントJARファイルを含めます。

1. Form Data Integrationサービスクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `FormDataIntegrationClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. PDFフォームの参照。

   * オブジェクト `java.io.FileInputStream` を作成するには、コンストラクターを使用し、書き出すデータを含むPDFフォームの場所を指定するstring値を渡します。
   * コンストラク `com.adobe.idp.Document` ターを使用して、PDFフォームを保存するオブジェクトを作成 `com.adobe.idp.Document` します。 PDFフォームを `java.io.FileInputStream` 含むオブジェクトをコンストラクターに渡します。

1. PDFフォームからデータを書き出します。

   オブジェクトのメソッドを呼び出し、PDF `FormDataIntegrationClient` フォームを保 `exportData` 存するオブジ `com.adobe.idp.Document` ェクトを渡して、フォームデータを書き出します。 このメソッドは、フォーム `com.adobe.idp.Document` データをXMLスキーマとして格納するオブジェクトを返します。

1. PDFフォームをPDFファイルとして保存します。

   * Create a `java.io.File` object and ensure that the file extension is XML.
   * オブジェクト `Document` のメソッドを呼び出 `copyToFile` して、オブジェクトの内容をファイルにコピ `Document` ーします(メソッドによって返されたオブジェクトを使用 `Document` していることを確 `exportData` 認します)。

**関連トピック**

[手順の概要](importing-exporting-data.md#summary-of-steps)

[クイックスタート（SOAPモード）:Java APIを使用したフォームデータの書き出し](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-exporting-form-data-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したフォームデータの書き出し {#export-form-data-using-the-web-service-api}

Form Data Integration API（Webサービス）を使用してフォームデータを書き出します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`.

   * AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. Form Data Integrationサービスクライアントを作成します。

   * Create a `FormDataIntegrationClient` object by using its default constructor.
   * Create a `FormDataIntegrationClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLを指定するstring値をAEM Formsサービスに渡します(例 `http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`:)。属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。 ただし、MTOMを使用す `?blob=mtom` るように指定します。
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `FormDataIntegrationClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `FormDataIntegrationClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `FormDataIntegrationClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. PDFフォームの参照。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、データの書き出し元のPDFフォームを保存するために使用します。
   * Create a `System.IO.FileStream` object by invoking its constructor. PDFフォームの場所とファイルを開くモードを指定するstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイト配列、開 `System.IO.FileStream` 始位置、ストリ `Read` ーム長を渡すことによって、バイト配列にストリームデータを設定します。
   * オブジェクト `BLOB` にバイト配列の内容を `MTOM` フィールドに割り当てて、オブジェクトを入力します。

1. PDFフォームからデータを書き出します。

   オブジェクトのメソッドを呼び出し、PDFフォームを `FormDataIntegrationClient` 保存するオブ `exportData` ジェクトを渡すこ `BLOB` とで、データをPDFフォームに読み込みます。 このメソッドは、フォーム `BLOB` データをXMLスキーマとして格納するオブジェクトを返します。

1. PDFフォームをPDFファイルとして保存します。

   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、XMLファイルの場所を表すstring値を渡します。
   * メソッドによって返されたオブジェクトのデータ内容を格納 `BLOB` するバイト配列を作成 `exportData` します。 オブジェクトのフィールドの値を取得して、バイト `BLOB` 配列を設定し `MTOM` ます。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡すことで、バイ `System.IO.BinaryWriter` ト配列の内 `Write` 容をXMLファイルに書き込みます。

**関連トピック**

[手順の概要](importing-exporting-data.md#summary-of-steps)

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
