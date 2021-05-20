---
title: データのインポートおよびエクスポート
seo-title: データのインポートおよびエクスポート
description: Form Data Integrationサービスを使用して、データをPDFフォームに読み込み、Java APIおよびWeb Service APIを使用してPDFフォームからデータを書き出します。
seo-description: Form Data Integrationサービスを使用して、データをPDFフォームに読み込み、Java APIおよびWeb Service APIを使用してPDFフォームからデータを書き出します。
uuid: 94ccb6f2-6e5f-43ea-a954-9a4402871a17
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 2e783745-c986-45ba-8e65-7437d114ca38
role: Developer
exl-id: 96310e0a-8e95-4a55-9508-5298b8d67f83
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2810'
ht-degree: 5%

---

# データのインポートおよびエクスポート{#importing-and-exporting-data}

**このドキュメントのサンプルと例は、JEE上のAEM Forms環境に限られています。**

## フォームデータ統合サービス{#about-the-form-data-integration-service}について

Form Data Integrationサービスを使用すると、データをPDFフォームに読み込んだり、PDFフォームからデータを書き出したりできます。 インポートおよびエクスポート操作では、次の2種類のPDF formsがサポートされます。

* Acrobatフォーム(Acrobatで作成)は、フォームフィールドを含むPDFドキュメントです。
* AdobeXMLフォーム（Designerで作成）は、XMLAdobeXML Formsアーキテクチャ(XFA)に準拠したPDFドキュメントです。

フォームデータは、PDFフォームの種類に応じて、次のいずれかの形式で使用できます。

* XFDF ファイル。Acrobat フォームデータ形式の XML バージョンです。
* XDP ファイル。フォームフィールド定義を含む XML ファイルです。フォームフィールドデータと埋め込まれた PDF ファイルが含まれる場合もあります。Designerで生成されたXDPファイルは、埋め込まれたbase-64-encoded PDFドキュメントを使用する場合にのみ使用できます。

次のタスクは、Form Data Integrationサービスを使用して実行できます。

* データをPDF formsに読み込む。 詳しくは、「[フォームデータの読み込み](importing-exporting-data.md#importing-form-data)」を参照してください。
* データをPDF formsから書き出す。 詳しくは、[フォームデータの書き出し](importing-exporting-data.md#exporting-form-data)を参照してください。

>[!NOTE]
>
>Form Data Integrationサービスについて詳しくは、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

## フォームデータのインポート{#importing-form-data}

Form Data Integrationサービスを使用して、フォームデータをインタラクティブPDF formsに読み込むことができます。 インタラクティブPDFフォームは、ユーザーから情報を収集したり、カスタム情報を表示したりするための1つ以上のフィールドを含むPDFドキュメントです。 Form Data Integrationサービスは、フォームの演算、検証、スクリプティングをサポートしていません。

Designerで作成したフォームにデータを読み込むには、有効なXDP XMLデータソースを参照する必要があります。 次の住宅ローン申し込みフォームの例を考えてみましょう。

![ie_ie_loanformdata](assets/ie_ie_loanformdata.png)

このフォームにデータ値を読み込むには、フォームに対応する有効なXDP XMLデータソースが必要です。 任意のXMLデータソースを使用して、Form Data Integrationサービスを使用してフォームにデータを読み込むことはできません。 任意のXMLデータソースとXDP XMLデータソースの違いは、XDPデータソースがXML Forms Architecture(XFA)に準拠している点です。 次のXMLは、サンプルの住宅ローン申し込みフォームに対応するXDP XMLデータソースを表しています。

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
>Form Data Integrationサービスについて詳しくは、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順の概要{#summary-of-steps}

フォームデータをPDFフォームに読み込むには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Form Data Integrationサービスクライアントを作成します。
1. PDFフォームの参照
1. XMLデータソースを参照します。
1. PDFフォームにデータを読み込みます。
1. PDFフォームをPDFファイルとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用する場合は、プロキシファイルを必ず含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar(AEM FormsがJBossにデプロイされている場合に必須)
* jbossall-client.jar(AEM FormsがJBossにデプロイされている場合に必須)

これらのJARファイルの場所について詳しくは、「[AEM Forms Javaライブラリファイル](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を含める」を参照してください。

**Form Data Integrationサービスクライアントの作成**

プログラムによってデータをPDFフォームのクライアントAPIに読み込む前に、データ統合サービスクライアントを作成する必要があります。 サービスクライアントを作成する場合、サービスを呼び出すために必要な接続設定を定義します。 詳しくは、[接続プロパティ](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)の設定を参照してください。

**PDFフォームの参照**

データをPDFフォームに読み込むには、Designerで作成されたXMLフォームまたはAcrobatで作成されたAcrobatフォームを参照する必要があります。

**XMLデータソースの参照**

フォームデータを読み込むには、有効なデータソースを参照する必要があります。 Designerで作成したXFA XMLフォームにデータを読み込むには、XDP XMLデータソースを使用する必要があります。 Acrobatフォームを参照する場合は、XFDFデータソースを使用する必要があります。 データのインポート先のフィールドごとに、値を指定する必要があります。 XMLデータソース内の要素がフォーム内のフィールドに対応していない場合、その要素は無視されます。

**PDFフォームへのデータの読み込み**

PDFフォームと有効なXMLデータソースを参照した後で、データをPDFフォームに読み込むことができます。

**PDFフォームをPDFファイルとして保存します**

データをフォームに読み込んだ後、フォームをPDFファイルとして保存できます。 PDFファイルとして保存したフォームは、Adobe ReaderまたはAcrobatで開き、読み込んだデータを含むフォームを確認することができます。

**関連トピック**

[Java APIを使用したフォームデータの読み込み](importing-exporting-data.md#import-form-data-using-the-java-api)

[WebサービスAPIを使用したフォームデータの読み込み](importing-exporting-data.md#import-form-data-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[フォームデータ統合サービスAPIクイックスタート](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[フォームデータの書き出し](importing-exporting-data.md#exporting-form-data)

### Java API {#import-form-data-using-the-java-api}を使用したフォームデータの読み込み

フォームデータ統合API(Java)を使用してフォームデータを読み込みます。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-formdataintegration-client.jarなどのクライアントJARファイルを含めます。

1. Form Data Integrationサービスクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `FormDataIntegrationClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. PDFフォームの参照

   * コンストラクタを使用して `java.io.FileInputStream` オブジェクトを作成します。PDFフォームの場所を指定するstring値を渡します。
   * `com.adobe.idp.Document`コンストラクターを使用して、PDFフォームを保存する`com.adobe.idp.Document`オブジェクトを作成します。 PDFフォームを含む`java.io.FileInputStream`オブジェクトをコンストラクターに渡します。

1. XMLデータソースを参照します。

   * コンストラクターを使用して`java.io.FileInputStream`オブジェクトを作成し、フォームに読み込むデータが含まれるXMLファイルの場所を指定する文字列値を渡します。
   * `com.adobe.idp.Document`コンストラクターを使用して、フォームデータを格納する`com.adobe.idp.Document`オブジェクトを作成します。 フォームデータを含む`java.io.FileInputStream`オブジェクトをコンストラクターに渡します。

1. PDFフォームにデータを読み込みます。

   `FormDataIntegrationClient`オブジェクトの`importData`メソッドを呼び出し、次の値を渡して、データをPDFフォームに読み込みます。

   * PDFフォームを保存する`com.adobe.idp.Document`オブジェクト。
   * フォームデータを格納する`com.adobe.idp.Document`オブジェクト。

   `importData`メソッドは、XMLデータソース内のデータを含むPDFフォームを保存する`com.adobe.idp.Document`オブジェクトを返します。

1. PDFフォームをPDFファイルとして保存します。

   * `java.io.File`オブジェクトを作成し、ファイル拡張子が「.PDF」であることを確認します。
   * `Document`オブジェクトの`copyToFile`メソッドを呼び出して、`Document`オブジェクトの内容をファイルにコピーします（`importData`メソッドで返された`Document`オブジェクトを使用するようにしてください）。

**関連トピック**

[手順の概要](importing-exporting-data.md#summary-of-steps)

[クイックスタート（SOAPモード）:Java APIを使用したフォームデータの読み込み](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-importing-form-data-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#import-form-data-using-the-web-service-api}を使用したフォームデータの読み込み

フォームデータ統合API（Webサービス）を使用してフォームデータを読み込みます。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. Form Data Integrationサービスクライアントを作成します。

   * デフォルトのコンストラクターを使用して`FormDataIntegrationClient`オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`FormDataIntegrationClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに渡す文字列値（例：`http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`）を渡します。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する際に使用されます。 ただし、MTOMを使用する場合は`?blob=mtom`を指定します。
   * `FormDataIntegrationClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値は、MTOMが使用されるようにします。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールド`FormDataIntegrationClient.ClientCredentials.UserName.UserName`にAEM formsユーザー名を割り当てます。
      * 対応するパスワード値をフィールド`FormDataIntegrationClient.ClientCredentials.UserName.Password`に割り当てます。
      * フィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に定数値`HttpClientCredentialType.Basic`を割り当てます。
      * フィールド`BasicHttpBindingSecurity.Security.Mode`に定数値`BasicHttpSecurityMode.TransportCredentialOnly`を割り当てます。

1. PDFフォームの参照

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この`BLOB`オブジェクトは、PDFフォームの保存に使用されます。
   * コンストラクターを呼び出して、`System.IO.FileStream`オブジェクトを作成します。 PDFフォームの場所とファイルを開くモードを指定するstring値を渡します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得することで、バイト配列のサイズを判断できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出して、バイト配列にストリームデータを入力します。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * `BLOB`オブジェクトの`MTOM`フィールドにバイト配列の内容を割り当てて、オブジェクトを設定します。

1. XMLデータソースを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この`BLOB`オブジェクトは、フォームに読み込まれるデータを保存するために使用されます。
   * コンストラクターを呼び出して、`System.IO.FileStream`オブジェクトを作成します。 読み込むデータが含まれるXMLファイルの場所と、ファイルを開くモードを指定するstring値を渡します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得することで、バイト配列のサイズを判断できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出して、バイト配列にストリームデータを入力します。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * `BLOB`オブジェクトの`MTOM`フィールドにバイト配列の内容を割り当てて、オブジェクトを設定します。

1. PDFフォームにデータを読み込みます。

   `FormDataIntegrationClient`オブジェクトの`importData`メソッドを呼び出し、次の値を渡して、データをPDFフォームに読み込みます。

   * PDFフォームを保存する`BLOB`オブジェクト。
   * フォームデータを格納する`BLOB`オブジェクト。

   `importData`メソッドは、XMLデータソース内のデータを含むPDFフォームを保存する`BLOB`オブジェクトを返します。

1. PDFフォームをPDFファイルとして保存します。

   * コンストラクターを呼び出し、PDFファイルのファイル位置を表す文字列値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `importData`メソッドで返された`BLOB`オブジェクトのデータ内容を格納するバイト配列を作成します。 `BLOB`オブジェクトの`MTOM`フィールドの値を取得して、バイト配列を設定します。
   * コンストラクターを呼び出し、`System.IO.FileStream`オブジェクトを渡して、`System.IO.BinaryWriter`オブジェクトを作成します。
   * `System.IO.BinaryWriter`オブジェクトの`Write`メソッドを呼び出し、バイト配列を渡すことにより、バイト配列の内容をPDFファイルに書き込みます。

**関連トピック**

[手順の概要](importing-exporting-data.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## フォームデータの書き出し{#exporting-form-data}

Form Data Integrationサービスを使用して、インタラクティブPDFフォームからフォームデータを書き出すことができます。 書き出されるデータの形式は、フォームの種類によって異なります。 フォームタイプがAcrobatで作成されたAcrobatフォームの場合、書き出されるデータはXFDFになります。 フォームタイプがDesignerで作成されたXMLフォームの場合、書き出されるデータはXDPになります。

>[!NOTE]
>
>Form Data Integrationサービスについて詳しくは、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順の概要{#summary_of_steps-1}

PDFフォームからフォームデータを書き出すには、次の手順を実行します。

1. プロジェクトファイルを含める
1. Form Data Integrationサービスクライアントを作成します。
1. PDFフォームの参照
1. PDFフォームからデータを書き出します。
1. 書き出したデータをXMLファイルとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用する場合は、プロキシファイルを必ず含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar(AEM FormsがJBossにデプロイされている場合に必須)
* jbossall-client.jar(AEM FormsがJBossにデプロイされている場合に必須)

**Form Data Integrationサービスクライアントの作成**

プログラムによってデータをPDF formClient APIに読み込む前に、Data Integrationサービスクライアントを作成する必要があります。 サービスクライアントを作成する場合、サービスを呼び出すために必要な接続設定を定義します。 詳しくは、[接続プロパティ](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)の設定を参照してください。

**PDFフォームの参照**

PDFフォームからデータを書き出すには、DesignerまたはAcrobatで作成され、フォームデータを含むPDFフォームを参照する必要があります。 空のPDFフォームからデータを書き出そうとすると、空のXMLスキーマが取得されます。

**PDFフォームからのデータの書き出し**

フォームデータを含むPDFフォームを参照した後で、フォームからデータを書き出すことができます。 データは、フォームに基づくXMLスキーマ内で書き出されます。

**フォームデータをXMLファイルとして保存する**

フォームデータを書き出した後、データをXMLファイルとして保存できます。 XMLファイルとして保存したXMLファイルをXMLビューアで開いて、フォームデータを表示できます。

**関連トピック**

[Java APIを使用したフォームデータの書き出し](importing-exporting-data.md#export-form-data-using-the-java-api)

[WebサービスAPIを使用したフォームデータの書き出し](importing-exporting-data.md#export-form-data-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[フォームデータ統合サービスAPIクイックスタート](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[フォームデータの読み込み](importing-exporting-data.md#importing-form-data)

### Java API {#export-form-data-using-the-java-api}を使用したフォームデータの書き出し

フォームデータ統合API(Java)を使用してフォームデータを書き出すには：

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-formdataintegration-client.jarなどのクライアントJARファイルを含めます。

1. Form Data Integrationサービスクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `FormDataIntegrationClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. PDFフォームの参照

   * コンストラクターを使用して`java.io.FileInputStream`オブジェクトを作成し、書き出すデータが含まれるPDFフォームの場所を指定する文字列値を渡します。
   * `com.adobe.idp.Document`コンストラクターを使用して、PDFフォームを保存する`com.adobe.idp.Document`オブジェクトを作成します。 PDFフォームを含む`java.io.FileInputStream`オブジェクトをコンストラクターに渡します。

1. PDFフォームからデータを書き出します。

   `FormDataIntegrationClient`オブジェクトの`exportData`メソッドを呼び出し、PDFフォームを保存する`com.adobe.idp.Document`オブジェクトを渡すことで、フォームデータを書き出します。 このメソッドは、フォームデータをXMLスキーマとして保存する`com.adobe.idp.Document`オブジェクトを返します。

1. PDFフォームをPDFファイルとして保存します。

   * `java.io.File`オブジェクトを作成し、ファイル拡張子がXMLであることを確認します。
   * `Document`オブジェクトの`copyToFile`メソッドを呼び出して、`Document`オブジェクトの内容をファイルにコピーします（`exportData`メソッドで返された`Document`オブジェクトを使用するようにしてください）。

**関連トピック**

[手順の概要](importing-exporting-data.md#summary-of-steps)

[クイックスタート（SOAPモード）:Java APIを使用したフォームデータの書き出し](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-exporting-form-data-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#export-form-data-using-the-web-service-api}を使用したフォームデータの書き出し

フォームデータ統合API（Webサービス）を使用してフォームデータを書き出すには：

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1`.

   * `localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. Form Data Integrationサービスクライアントを作成します。

   * デフォルトのコンストラクターを使用して`FormDataIntegrationClient`オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`FormDataIntegrationClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに渡す文字列値（例：`http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`）を渡します。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する際に使用されます。 ただし、MTOMを使用する場合は`?blob=mtom`を指定します。
   * `FormDataIntegrationClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値は、MTOMが使用されるようにします。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールド`FormDataIntegrationClient.ClientCredentials.UserName.UserName`にAEM formsユーザー名を割り当てます。
      * 対応するパスワード値をフィールド`FormDataIntegrationClient.ClientCredentials.UserName.Password`に割り当てます。
      * フィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に定数値`HttpClientCredentialType.Basic`を割り当てます。
      * フィールド`BasicHttpBindingSecurity.Security.Mode`に定数値`BasicHttpSecurityMode.TransportCredentialOnly`を割り当てます。

1. PDFフォームの参照

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この`BLOB`オブジェクトは、データの書き出し元のPDFフォームを保存するために使用されます。
   * コンストラクターを呼び出して、`System.IO.FileStream`オブジェクトを作成します。 PDFフォームの場所とファイルを開くモードを指定するstring値を渡します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得することで、バイト配列のサイズを判断できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことによって、バイト配列にストリームデータを入力します。
   * `BLOB`オブジェクトの`MTOM`フィールドにバイト配列の内容を割り当てて、オブジェクトを設定します。

1. PDFフォームからデータを書き出します。

   `FormDataIntegrationClient`オブジェクトの`exportData`メソッドを呼び出し、PDFフォームを保存する`BLOB`オブジェクトを渡すことによって、データをPDFフォームに読み込みます。 このメソッドは、フォームデータをXMLスキーマとして保存する`BLOB`オブジェクトを返します。

1. PDFフォームをPDFファイルとして保存します。

   * コンストラクターを呼び出し、XMLファイルの場所を表す文字列値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `exportData`メソッドで返された`BLOB`オブジェクトのデータ内容を格納するバイト配列を作成します。 `BLOB`オブジェクトの`MTOM`フィールドの値を取得して、バイト配列を設定します。
   * コンストラクターを呼び出し、`System.IO.FileStream`オブジェクトを渡して、`System.IO.BinaryWriter`オブジェクトを作成します。
   * `System.IO.BinaryWriter`オブジェクトの`Write`メソッドを呼び出し、バイト配列を渡すことにより、バイト配列の内容をXMLファイルに書き込みます。

**関連トピック**

[手順の概要](importing-exporting-data.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
