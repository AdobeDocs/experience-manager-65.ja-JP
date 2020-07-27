---
title: データのインポートとエクスポート
seo-title: データのインポートとエクスポート
description: 'null'
seo-description: 'null'
uuid: 94ccb6f2-6e5f-43ea-a954-9a4402871a17
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 2e783745-c986-45ba-8e65-7437d114ca38
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '2742'
ht-degree: 6%

---


# データのインポートとエクスポート {#importing-and-exporting-data}

## Form Data Integration Serviceについて {#about-the-form-data-integration-service}

Form Data Integrationサービスでは、データをPDFフォームに読み込んだり、PDFフォームからデータを書き出したりできます。 インポート操作とエクスポート操作では、次の2種類のPDF formsがサポートされています。

* Acrobatフォーム（Acrobatで作成）は、フォームフィールドを含むPDFドキュメントです。
* Adobe XMLフォーム（Designerで作成）は、XML Adobe XMLフォームアーキテクチャ(XFA)に準拠するPDFドキュメントです。

フォームデータは、PDFフォームの種類に応じて、次のいずれかの形式で存在する場合があります。

* XFDF ファイル。Acrobat フォームデータ形式の XML バージョンです。
* XDP ファイル。フォームフィールド定義を含む XML ファイルです。フォームフィールドデータと埋め込まれた PDF ファイルが含まれる場合もあります。Designerで生成されたXDPファイルは、埋め込みのbase-64エンコードPDFドキュメントを使用する場合にのみ使用できます。

Form Data Integrationサービスを使用して、次のタスクを実行できます。

* PDF formsにデータをインポートします。 詳しくは、「フォームデータの [読み込み](importing-exporting-data.md#importing-form-data)」を参照してください。
* PDF formsからデータをエクスポートします。 詳しくは、「フォームデータの [書き出し](importing-exporting-data.md#exporting-form-data)」を参照してください。

>[!NOTE]
>
>For more information about the Form Data Integration service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## フォームデータの読み込み {#importing-form-data}

Form Data Integrationサービスを使用して、フォームデータをインタラクティブPDF formsに読み込むことができます。 インタラクティブPDFフォームは、ユーザーから情報を収集したり、カスタムドキュメントを表示したりするための1つ以上のフィールドを含むPDF情報です。 Form Data Integrationサービスは、フォームの演算、検証、スクリプティングをサポートしていません。

Designerで作成されたフォームにデータを読み込むには、有効なXDP XMLデータソースを参照する必要があります。 次の住宅ローン申し込みフォームの例を考えてみましょう。

![ie_ie_loanformdata](assets/ie_ie_loanformdata.png)

このフォームにデータ値を読み込むには、フォームに対応する有効なXDP XMLデータソースが必要です。 任意のXMLデータソースを使用して、Form Data Integrationサービスを使用してデータをフォームに読み込むことはできません。 任意のXMLデータソースとXDP XMLデータソースの違いは、XDPデータソースがXMLフォームアーキテクチャ(XFA)に準拠していることです。 次のXMLは、住宅ローン申し込みフォームの例に対応するXDP XMLデータソースを表しています。

```xml
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
1. PDFフォームの参照
1. XMLデータソースを参照します。
1. PDFフォームにデータを読み込みます。
1. PDFフォームをPDFファイルとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めます。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar(AEM FormsがJBossにデプロイされている場合に必須)
* jbossall-client.jar(AEM FormsがJBossにデプロイされている場合に必須)

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Form Data Integrationサービスクライアントの作成**

プログラムでデータをPDFフォームのクライアントAPIに読み込む前に、Data Integrationサービスクライアントを作成する必要があります。 サービスクライアントを作成する場合、サービスの呼び出しに必要な接続設定を定義します。 詳しくは、「接続プロパティの [設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)」を参照してください。

**PDFフォームの参照**

PDFフォームにデータを読み込むには、Designerで作成されたXMLフォームまたはAcrobatで作成されたAcrobatフォームを参照する必要があります。

**XMLデータソースの参照**

フォームデータを読み込むには、有効なデータソースを参照する必要があります。 Designerで作成したXFA XMLフォームにデータを読み込むには、XDP XMLデータソースを使用する必要があります。 Acrobatフォームを参照する場合は、XFDFデータソースを使用する必要があります。 データの読み込み先のフィールドごとに、値を指定する必要があります。 XMLデータソース内の要素がフォーム内のフィールドに対応していない場合、その要素は無視されます。

**PDFフォームへのデータの読み込み**

PDFフォームと有効なXMLデータソースを参照した後、データをPDFフォームに読み込むことができます。

**PDFフォームをPDFファイルとして保存する**

フォームにデータを読み込んだ後、フォームをPDFファイルとして保存できます。 PDFファイルとして保存すると、ユーザーはAdobe ReaderまたはAcrobatでフォームを開き、読み込んだデータを含むフォームを確認できます。

**関連トピック**

[Java APIを使用したフォームデータの読み込み](importing-exporting-data.md#import-form-data-using-the-java-api)

[WebサービスAPIを使用したフォームデータの読み込み](importing-exporting-data.md#import-form-data-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Form Data Integration Service APIクイック開始](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[フォームデータの書き出し](importing-exporting-data.md#exporting-form-data)

### Java APIを使用したフォームデータの読み込み {#import-form-data-using-the-java-api}

Form Data Integration API(Java)を使用してフォームデータを読み込みます。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-formdataintegration-client.jarなどのクライアントJARファイルを含めます。

1. Form Data Integrationサービスクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `FormDataIntegrationClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. PDFフォームの参照

   * コンストラクタを使用して `java.io.FileInputStream` オブジェクトを作成します。PDFフォームの場所を指定するstring値を渡します。
   * コンストラクターを使用して、PDFフォームを格納する `com.adobe.idp.Document` オブジェクトを作成し `com.adobe.idp.Document` ます。 PDFフォームを含む `java.io.FileInputStream` オブジェクトをコンストラクターに渡します。

1. XMLデータソースを参照します。

   * コンストラクターを使用して `java.io.FileInputStream` オブジェクトを作成し、フォームに読み込むデータが含まれるXMLファイルの場所を指定するstring値を渡します。
   * フォームデータを格納する `com.adobe.idp.Document` オブジェクトを作成するには、コンストラクターを使用 `com.adobe.idp.Document` します。 フォームデータを含む `java.io.FileInputStream` オブジェクトをコンストラクターに渡します。

1. PDFフォームにデータを読み込みます。

   オブジェクトのメソッドを呼び出し、次の値を渡して、 `FormDataIntegrationClient``importData` データをPDFフォームに読み込みます。

   * PDFフォームを保存する `com.adobe.idp.Document` オブジェクトです。
   * フォームデータを格納する `com.adobe.idp.Document` オブジェクトです。

   この `importData` メソッドは、XMLデータソース内のデータを含むPDFフォームを格納する `com.adobe.idp.Document` オブジェクトを返します。

1. PDFフォームをPDFファイルとして保存します。

   * Create a `java.io.File` object and ensure that the file extension is “.PDF”.
   * オブジェクトのメ `Document` ソッドを呼び出して、 `copyToFile` オブジェクトの内容をファイルにコピーします(メソッドから返された `Document``Document``importData` オブジェクトを必ず使用してください)。

**関連トピック**

[手順の概要](importing-exporting-data.md#summary-of-steps)

[クイック開始（SOAPモード）: Java APIを使用したフォームデータの読み込み](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-importing-form-data-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したフォームデータの読み込み {#import-form-data-using-the-web-service-api}

Form Data Integration API（Webサービス）を使用してフォームデータを読み込みます。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >サーバーホスト `localhost` AEM FormsのIPアドレスに置き換えます。

1. Form Data Integrationサービスクライアントを作成します。

   * Create a `FormDataIntegrationClient` object by using its default constructor.
   * Create a `FormDataIntegrationClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`)に渡すstring値を渡します。 属性を使用する必要はありません `lc_version` 。 この属性は、サービス参照を作成する際に使用されます。 ただし、MTOMを使用す `?blob=mtom` るように指定します。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `FormDataIntegrationClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールドにAEM formsのユーザー名を割り当て `FormDataIntegrationClient.ClientCredentials.UserName.UserName`ます。
      * 対応するパスワード値をフィールドに割り当て `FormDataIntegrationClient.ClientCredentials.UserName.Password`ます。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当て `BasicHttpBindingSecurity.Security.Mode`ます。

1. PDFフォームの参照

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、PDFフォームの保存に使用されます。
   * Create a `System.IO.FileStream` object by invoking its constructor. PDFフォームの場所とファイルを開くモードを指定するstring値を渡します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
   * オブジェクトのメソッドを呼び出して、バイト配列にストリームデータ `System.IO.FileStream` を入力し `Read` ます。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * オブジェクトにバイト配列の内容を割り当てて、 `BLOB` オブジェクト `MTOM` を入力します。

1. XMLデータソースを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、フォームに読み込まれるデータを保存するために使用します。
   * Create a `System.IO.FileStream` object by invoking its constructor. 読み込むデータが含まれるXMLファイルの場所と、ファイルを開くモードを指定するstring値を渡します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
   * オブジェクトのメソッドを呼び出して、バイト配列にストリームデータ `System.IO.FileStream` を入力し `Read` ます。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * オブジェクトにバイト配列の内容を割り当てて、 `BLOB` オブジェクト `MTOM` を入力します。

1. PDFフォームにデータを読み込みます。

   オブジェクトのメソッドを呼び出し、次の値を渡して、PDFフォームにデータ `FormDataIntegrationClient` を読み込み `importData` ます。

   * PDFフォームを保存する `BLOB` オブジェクトです。
   * フォームデータを格納する `BLOB` オブジェクトです。

   この `importData` メソッドは、XMLデータソース内のデータを含むPDFフォームを格納する `BLOB` オブジェクトを返します。

1. PDFフォームをPDFファイルとして保存します。

   * コンストラクターを呼び出し、PDFファイルのファイルの場所を表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * メソッドが返した `BLOB` オブジェクトのデータ内容を格納するバイト配列を作成し `importData` ます。 オブジェクトのフィールドの値を取得して、 `BLOB` バイト配列を設定し `MTOM` ます。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡して、バイト配列の内容をPDFファイルに書き込み `System.IO.BinaryWriter` ま `Write` す。

**関連トピック**

[手順の概要](importing-exporting-data.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## フォームデータの書き出し {#exporting-form-data}

Form Data Integrationサービスを使用して、インタラクティブPDFフォームからフォームデータを書き出すことができます。 書き出されるデータの形式は、フォームの種類によって異なります。 フォームの種類がAcrobatで作成されたAcrobatフォームの場合、書き出されるデータはXFDFです。 フォームの種類がDesignerで作成されたXMLフォームの場合、書き出されたデータはXDPになります。

>[!NOTE]
>
>For more information about the Form Data Integration service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-1}

PDFフォームからフォームデータを書き出すには、次の手順を実行します。

1. プロジェクトファイルを含める
1. Form Data Integrationサービスクライアントを作成します。
1. PDFフォームの参照
1. PDFフォームからデータを書き出します。
1. 書き出したデータをXMLファイルとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めます。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar(AEM FormsがJBossにデプロイされている場合に必須)
* jbossall-client.jar(AEM FormsがJBossにデプロイされている場合に必須)

**Form Data Integrationサービスクライアントの作成**

プログラムでデータをPDF formClient APIに読み込む前に、Data Integrationサービスクライアントを作成する必要があります。 サービスクライアントを作成する場合、サービスの呼び出しに必要な接続設定を定義します。 詳しくは、接続プロパティ [の設定を参照してください](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。

**PDFフォームの参照**

PDFフォームからデータを書き出すには、DesignerまたはAcrobatで作成され、フォームデータを含むPDFフォームを参照する必要があります。 空のPDFフォームからデータを書き出そうとすると、空のXMLスキーマが返されます。

**PDFフォームからのデータの書き出し**

フォームデータを含むPDFフォームを参照した後、フォームからデータを書き出すことができます。 データは、フォームに基づくXMLスキーマ内で書き出されます。

**フォームデータをXMLファイルとして保存する**

フォームデータを書き出した後、データをXMLファイルとして保存できます。 XMLファイルとして保存したXMLファイルは、XMLビューア内で開いてフォームデータを表示できます。

**関連トピック**

[Java APIを使用したフォームデータの書き出し](importing-exporting-data.md#export-form-data-using-the-java-api)

[WebサービスAPIを使用したフォームデータの書き出し](importing-exporting-data.md#export-form-data-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Form Data Integration Service APIクイック開始](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[フォームデータの読み込み](importing-exporting-data.md#importing-form-data)

### Java APIを使用したフォームデータの書き出し {#export-form-data-using-the-java-api}

Form Data Integration API(Java)を使用してフォームデータを書き出す：

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-formdataintegration-client.jarなどのクライアントJARファイルを含めます。

1. Form Data Integrationサービスクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `FormDataIntegrationClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. PDFフォームの参照

   * コンストラクターを使用して `java.io.FileInputStream` オブジェクトを作成し、書き出すデータが含まれるPDFフォームの場所を指定するstring値を渡します。
   * コンストラクターを使用して、PDFフォームを格納する `com.adobe.idp.Document` オブジェクトを作成し `com.adobe.idp.Document` ます。 PDFフォームを含む `java.io.FileInputStream` オブジェクトをコンストラクターに渡します。

1. PDFフォームからデータを書き出します。

   オブジェクトの `FormDataIntegrationClient` メソッドを呼び出してフォームデータを書き出し、PDFフォームを保存する `exportData``com.adobe.idp.Document` オブジェクトを渡します。 このメソッドは、フォームデータをXMLスキーマとして格納する `com.adobe.idp.Document` オブジェクトを返します。

1. PDFフォームをPDFファイルとして保存します。

   * Create a `java.io.File` object and ensure that the file extension is XML.
   * オブジェクトのメ `Document` ソッドを呼び出して、 `copyToFile` オブジェクトの内容をファイルにコピーします(メソッドから返された `Document``Document``exportData` オブジェクトを必ず使用してください)。

**関連トピック**

[手順の概要](importing-exporting-data.md#summary-of-steps)

[クイック開始（SOAPモード）: Java APIを使用したフォームデータの書き出し](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-exporting-form-data-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したフォームデータの書き出し {#export-form-data-using-the-web-service-api}

Form Data Integration API（Webサービス）を使用してフォームデータを書き出すには：

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`.

   * サーバーホスト `localhost` AEM FormsのIPアドレスに置き換えます。

1. Form Data Integrationサービスクライアントを作成します。

   * Create a `FormDataIntegrationClient` object by using its default constructor.
   * Create a `FormDataIntegrationClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`)に渡すstring値を渡します。 属性を使用する必要はありません `lc_version` 。 この属性は、サービス参照を作成する際に使用されます。 ただし、MTOMを使用す `?blob=mtom` るように指定します。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `FormDataIntegrationClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールドにAEM formsのユーザー名を割り当て `FormDataIntegrationClient.ClientCredentials.UserName.UserName`ます。
      * 対応するパスワード値をフィールドに割り当て `FormDataIntegrationClient.ClientCredentials.UserName.Password`ます。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当て `BasicHttpBindingSecurity.Security.Mode`ます。

1. PDFフォームの参照

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、データの書き出し元のPDFフォームを保存するために使用します。
   * Create a `System.IO.FileStream` object by invoking its constructor. PDFフォームの場所とファイルを開くモードを指定するstring値を渡します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
   * オブジェクトの `System.IO.FileStream``Read` メソッドを呼び出し、読み取るバイト配列、開始位置およびストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * オブジェクトにバイト配列の内容を割り当てて、 `BLOB` オブジェクト `MTOM` を入力します。

1. PDFフォームからデータを書き出します。

   オブジェクトの `FormDataIntegrationClient` メソッドを呼び出し、PDFフォームを格納している `exportData``BLOB` オブジェクトを渡して、PDFフォームにデータを読み込みます。 このメソッドは、フォームデータをXMLスキーマとして格納する `BLOB` オブジェクトを返します。

1. PDFフォームをPDFファイルとして保存します。

   * コンストラクターを呼び出し、XMLファイルの場所を表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * メソッドが返した `BLOB` オブジェクトのデータ内容を格納するバイト配列を作成し `exportData` ます。 オブジェクトのフィールドの値を取得して、 `BLOB` バイト配列を設定し `MTOM` ます。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡して、バイト配列の内容をXMLファイルに書き込み `System.IO.BinaryWriter` ま `Write` す。

**関連トピック**

[手順の概要](importing-exporting-data.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
