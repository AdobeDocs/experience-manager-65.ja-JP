---
title: データの読み込みと書き出し
seo-title: Importing and Exporting Data
description: Form Data Integration サービスを使用して、Java API および web サービス API を使用して、PDF フォームにデータを読み込み、PDF フォームからデータを書き出します。
seo-description: Use the Form Data Integration service to import data into a PDF form and export data from a PDF form using the Java API and Web Service API.
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
source-wordcount: '2778'
ht-degree: 100%

---

# データの読み込みと書き出し {#importing-and-exporting-data}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

## Form Data Integration サービスについて {#about-the-form-data-integration-service}

Form Data Integration サービスを使用すると、データを PDF フォームに読み込んだり、PDF フォームからデータを書き出したりできます。読み込みおよび書き出し操作では、次の 2 種類の PDF forms がサポートされます。

* Acrobat フォーム（Acrobat で作成）は、フォームフィールドを含む PDF ドキュメントです。
* Adobe XML フォーム（Designer で作成）は、XML Adobe XML フォームアーキテクチャ（XFA）に準拠する PDF ドキュメントです。

フォームデータは、PDF フォームのタイプに応じて、次のいずれかの形式で存在します。

* XFDF ファイル。Acrobat フォームデータ形式の XML バージョンです。
* XDP ファイル。フォームフィールド定義を含む XML ファイルです。フォームフィールドデータと埋め込まれた PDF ファイルが含まれる場合もあります。Designer で生成された XDP ファイルは、埋め込み base-64 エンコード PDF ドキュメントを使用する場合にのみ利用できます。

次のタスクは、Form Data Integration サービスを使用して実行できます。

* PDF forms にデータを読み込みます。詳しくは、[フォームデータの読み込み](importing-exporting-data.md#importing-form-data)を参照してください。
* PDF forms からデータを書き出します。詳しくは、[フォームデータの書き出し](importing-exporting-data.md#exporting-form-data)を参照してください。

>[!NOTE]
>
>Form Data Integration サービスについて詳しくは、[AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

## フォームデータの読み込み {#importing-form-data}

Form Data Integration サービスを使用して、フォームデータをインタラクティブ PDF forms に読み込むことができます。インタラクティブ PDF フォームは、ユーザーから情報を収集したり、カスタム情報を表示したりするための 1 つ以上のフィールドを含む PDF ドキュメントです。Form Data Integration サービスは、フォームの演算、検証、スクリプティングをサポートしていません。

Designer で作成したフォームにデータを読み込むには、有効な XDP XML データソースを参照する必要があります。次の住宅ローン申し込みフォームサンプルについて見てみましょう。

![ie_ie_loanformdata](assets/ie_ie_loanformdata.png)

データ値をこのフォームに読み込むには、フォームに対応する有効な XDP XML データソースが必要です。任意の XML データソースを使用して、Form Data Integration サービスを使用してデータをフォームに読み込むことはできません。任意の XML データソースと XDP XML データソースの違いは、XDP データソースが XML フォームアーキテクチャ（XFA）に準拠している点です。次の XML は、住宅ローン申し込みフォームのサンプルに対応する XML データソースを表しています。

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
>Form Data Integration サービスについて詳しくは、[AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary-of-steps}

フォームデータを PDF フォームに読み込むには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. フォームデータ統合サービスクライアントを作成します。
1. PDF フォームを参照します。
1. XML データソースを参照します。
1. データを PDF フォームにインポートします。
1. PDF フォームを PDF ファイルとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めるようにします。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar（AEM Forms を JBoss にデプロイする場合に必要）
* jbossall-client.jar（AEM Forms が JBoss にデプロイされている場合に必要）

これらの JAR ファイルの場所について詳しくは、[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files) を参照してください。

**Form Data Integration サービスクライアントの作成**

プログラムによってデータを PDF form クライアント API に読み込む前に、Data Integration Service クライアントを作成する必要があります。 サービスクライアントを作成する際は、サービスを呼び出すために必要な接続設定を定義します。詳しくは、[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照してください。

**PDF フォームの参照**

データを PDF フォームに読み込むには、Designer で作成した XML フォームまたは Acrobat で作成した Acrobat フォームを参照する必要があります。

**XML データソースの参照**

フォームデータを読み込むには、有効なデータソースを参照する必要があります。Designer で作成した XFA XML フォームにデータを読み込むには、XDP XML データソースを使用する必要があります。Acrobat フォームを参照する場合は、XFDF データソースを使用する必要があります。データのインポート先のフィールドごとに、値を指定する必要があります。XML データソース内の要素がフォーム内のフィールドに対応していない場合、その要素は無視されます。

**データを PDF フォームに読み込み**

PDF フォームと有効な XML データソースを参照した後、データを PDF フォームに読み込むことができます。

**PDF フォームを PDF ファイルとして保存**

データをフォームに読み込んだ後、フォームを PDF ファイルとして保存できます。PDF ファイルとして保存したフォームを Adobe Reader または Acrobat で開くと、読み込まれたデータがフォームに表示されます。

**関連トピック**

[Java API を使用したフォームデータの読み込み](importing-exporting-data.md#import-form-data-using-the-java-api)

[Web サービス API を使用したフォームデータの読み込み](importing-exporting-data.md#import-form-data-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[フォームデータ統合サービス API クイックスタート](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[フォームデータのエクスポート](importing-exporting-data.md#exporting-form-data)

### Java API を使用したフォームデータの読み込み {#import-form-data-using-the-java-api}

フォームデータ統合 API（Java）を使用してフォームデータをインポートします。

1. プロジェクトファイルを含めます。

   adobe-formdataintegration-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. フォームデータ統合サービスクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `FormDataIntegrationClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. PDF フォームを参照します。

   * コンストラクタを使用して `java.io.FileInputStream` オブジェクトを作成します。PDF フォームの場所を指定する文字列の値を渡します。
   * `com.adobe.idp.Document` コンストラクタを使用して、PDF フォームを格納する `com.adobe.idp.Document` オブジェクトを作成します。PDF フォームが格納された `java.io.FileInputStream` オブジェクトをコンストラクタに渡します。

1. XML データソースを参照します。

   * コンストラクタを使用して `java.io.FileInputStream` オブジェクトを作成し、フォームにインポートするデータが格納されている XML ファイルの場所を示す文字列値を渡します。
   * `com.adobe.idp.Document` コンストラクタを使用して、フォームデータが格納される `com.adobe.idp.Document` オブジェクトを作成します。フォームデータを含む `java.io.FileInputStream` オブジェクトをコンストラクターに渡します。

1. データを PDF フォームにインポートします。

   `FormDataIntegrationClient` オブジェクトの `importData` メソッドを呼び出して次の値を渡すことにより、データを PDF フォームにインポートします。

   * PDF フォームが格納された `com.adobe.idp.Document` オブジェクト。
   * フォームデータが格納された `com.adobe.idp.Document` オブジェクト。

   `importData` メソッドは、XML データソースにあるデータを含む PDF フォームが格納された `com.adobe.idp.Document` オブジェクトを返します。

1. PDF フォームを PDF ファイルとして保存します。

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が「.PDF」であることを確認します。
   * `Document` オブジェクトの `copyToFile` メソッドを呼び出して、`Document` オブジェクトの内容をファイルにコピーします（`importData` メソッドによって返された `Document` オブジェクトを使用していることを確認します）。

**関連情報**

[手順の概要](importing-exporting-data.md#summary-of-steps)

[クイックスタート（SOAP モード）：Java API を使用したフォームデータの読み込み](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-importing-form-data-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用したフォームデータの読み込み {#import-form-data-using-the-web-service-api}

フォームデータ統合 API（web サービス）を使用してフォームデータをインポートします。

1. プロジェクトファイルを含めます。

   MTOM を使用する Microsoft .NET プロジェクトを作成します。WSDL 定義 `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1` を使用するようにします。

   >[!NOTE]
   >
   >`localhost` を、AEM Forms をホストするサーバーの IP アドレスに置き換えます。

1. フォームデータ統合サービスクライアントを作成します。

   * デフォルトのコンストラクターを使用して `FormDataIntegrationClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して `FormDataIntegrationClient.Endpoint.Address` オブジェクトを作成します。WSDL を指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`）。`lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。ただし、`?blob=mtom` を指定して MTOM を使用します。
   * `FormDataIntegrationClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` フィールドを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `FormDataIntegrationClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `FormDataIntegrationClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
      * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` をフィールド `BasicHttpBindingSecurity.Security.Mode` に割り当てます。

1. PDF フォームを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、PDF フォームを格納するために使用します。
   * コンストラクターを呼び出して `System.IO.FileStream` オブジェクトを作成します。PDF フォームの場所とファイルを開くモードを指定する文字列値を渡します。
   * `System.IO.FileStream` オブジェクトの内容を格納するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することでバイト配列のサイズを決定することができます。
   * `System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出して、バイト配列にストリームデータを入力します。読み取り対象のバイト配列、開始位置、ストリーム長を渡します。
   * `MTOM` フィールドにバイト配列の内容を割り当てて、`BLOB` オブジェクトに入力します。

1. XML データソースを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、フォームにインポートされたデータを格納するために使用されます。
   * コンストラクターを呼び出して `System.IO.FileStream` オブジェクトを作成します。インポートするデータを含む XML ファイルの場所と、ファイルを開くモードを指定する文字列値を渡します。
   * `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することでバイト配列のサイズを決定することができます。
   * `System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出して、バイト配列にストリームデータを入力します。読み取り対象のバイト配列、開始位置、ストリーム長を渡します。
   * `MTOM` フィールドにバイト配列の内容を割り当てて、`BLOB` オブジェクトにデータを入力します。

1. データを PDF フォームにインポートします。

   `FormDataIntegrationClient` オブジェクトの `importData` メソッドを呼び出し、次の値を渡すことによって、PDF フォームにデータをインポートします。

   * PDF フォームを格納する `BLOB` オブジェクト。
   * フォームデータが格納された `BLOB` オブジェクト。

   `importData` メソッドは、XML データソースにあるデータを含む PDF フォームが格納された `BLOB` オブジェクトを返します。

1. PDF フォームを PDF ファイルとして保存します。

   * コンストラクターを呼び出し、PDF ファイルの場所を表す文字列値を渡すことによって、`System.IO.FileStream` オブジェクトを作成します。
   * `importData` メソッドによって返された `BLOB` オブジェクトのデータコンテンツを格納するバイト配列を作成します。`BLOB` オブジェクトの `MTOM` フィールドの値を取得してバイト配列を入力します。
   * コンストラクターを呼び出し、`System.IO.FileStream` オブジェクトを渡すことによって、`System.IO.BinaryWriter` オブジェクトを作成します。
   * `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを呼び出して、バイト配列を渡すことによって、バイト配列の内容を PDF ファイルに書き込みます。

**関連トピック：**

[手順の概要](importing-exporting-data.md#summary-of-steps)

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## フォームデータのエクスポート {#exporting-form-data}

Form Data Integration サービスを使用して、インタラクティブ PDF フォームからフォームデータをエクスポートできます。エクスポートされるデータの形式は、フォームタイプによって異なります。フォームタイプが、Acrobat で作成された Acrobat フォームであれば、エクスポートされるデータは XFDF になります。フォームタイプが、Designer で作成された XML フォームであれば、エクスポートされるデータは XDP になります。

>[!NOTE]
>
>Form Data Integration サービスについて詳しくは、[AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary_of_steps-1}

PDF フォームからフォームデータをエクスポートするには、次の手順を実行します。

1. プロジェクトファイルを含める
1. フォームデータ統合サービスクライアントを作成します。
1. PDF フォームを参照します。
1. PDF フォームからデータを書き出します。
1. エクスポートしたデータを XML ファイルとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めるようにします。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-formdataintegration-client.jar
* adobe-utilities.jar（AEM Forms を JBoss にデプロイする場合に必要）
* jbossall-client.jar（AEM Forms が JBoss にデプロイされている場合に必要）

**Form Data Integration サービスクライアントを作成**

PDF フォーム Client API にプログラムによってデータをインポートする前に、Data Integration サービスクライアントを作成する必要があります。サービスクライアントを作成する際は、サービスを呼び出すために必要な接続設定を定義します。詳しくは、[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照してください。

**PDF フォームの参照**

PDF フォームからデータを書き出すには、Designer または Acrobat で作成され、フォームデータを含む PDF フォームを参照する必要があります。空の PDF フォームからデータを書き出そうとすると、空の XML スキーマを取得することになります。

**PDF フォームからのデータの書き出し**

フォームデータを含む PDF フォームを参照した後で、フォームからデータを書き出すことができます。 データは、フォームに基づく XML スキーマ内で書き出されます。

**フォームデータを XML ファイルとして保存する**

フォームデータを書き出した後は、データを XML ファイルとして保存できます。 XML ファイルとして保存した XML ファイルを XML ビューアで開くと、フォームデータを表示できます。

**関連トピック**

[Java API を使用したフォームデータの書き出し](importing-exporting-data.md#export-form-data-using-the-java-api)

[Web サービス API を使用したフォームデータの書き出し](importing-exporting-data.md#export-form-data-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[フォームデータ統合サービス API クイックスタート](/help/forms/developing/form-data-integration-service-java.md#form-data-integration-service-java-api-quick-start-soap)

[フォームデータの読み込み](importing-exporting-data.md#importing-form-data)

### Java API を使用したフォームデータの書き出し {#export-form-data-using-the-java-api}

フォームデータ統合 API（Java）を使用してフォームデータを書き出すには、次の手順を実行します。

1. プロジェクトファイルを含めます。

   adobe-formdataintegration-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. フォームデータ統合サービスクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `FormDataIntegrationClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. PDF フォームを参照します。

   * コンストラクターを使用して `java.io.FileInputStream` オブジェクトを作成し、書き出すデータを含む PDF フォームの場所を指定する文字列値を渡します。
   * `com.adobe.idp.Document` コンストラクターを使用して、PDF フォームを格納する `com.adobe.idp.Document` オブジェクトを作成します。PDF フォームを含む `java.io.FileInputStream` オブジェクトをコンストラクターに渡します。

1. PDF フォームからデータを書き出します。

   `FormDataIntegrationClient` オブジェクトの `exportData` メソッドを呼び出してデータを書き出し、PDF フォームを格納する `com.adobe.idp.Document` オブジェクトを渡します。このメソッドは、フォームデータを XML スキーマとして格納する `com.adobe.idp.Document` オブジェクトを返します。

1. PDF フォームを PDF ファイルとして保存します。

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が XML であることを確認します。
   * `Document` オブジェクトの `copyToFile` メソッドを呼び出して、`Document` オブジェクトの内容をファイルにコピーします（`exportData` メソッドで返された `Document` オブジェクトを使用していることを確認します）。

**関連情報**

[手順の概要](importing-exporting-data.md#summary-of-steps)

[クイックスタート（SOAP モード）：Java API を使用したフォームデータの書き出し](/help/forms/developing/form-data-integration-service-java.md#quick-start-soap-mode-exporting-form-data-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用したフォームデータの書き出し {#export-form-data-using-the-web-service-api}

フォームデータ統合 API（web サービス）を使用してフォームデータを書き出すには、次の手順を実行します。

1. プロジェクトファイルを含めます。

   MTOM を使用する Microsoft .NET プロジェクトを作成します。WSDL 定義 `http://localhost:8080/soap/services/FormDataIntegration?WSDL&lc_version=9.0.1` を使用するようにします。

   * `localhost` を、AEM Forms をホストするサーバーの IP アドレスに置き換えます。

1. フォームデータ統合サービスクライアントを作成します。

   * デフォルトのコンストラクターを使用して `FormDataIntegrationClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して `FormDataIntegrationClient.Endpoint.Address` オブジェクトを作成します。WSDL を指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/FormDataIntegration?blob=mtom`）。`lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。ただし、`?blob=mtom` を指定して MTOM を使用します。
   * `FormDataIntegrationClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` フィールドを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `FormDataIntegrationClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `FormDataIntegrationClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
      * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` をフィールド `BasicHttpBindingSecurity.Security.Mode` に割り当てます。

1. PDF フォームを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、データの書き出し元の PDF フォームを格納するために使用されます。
   * コンストラクターを呼び出して `System.IO.FileStream` オブジェクトを作成します。PDF フォームの場所とファイルを開くモードを指定する文字列値を渡します。
   * `System.IO.FileStream` オブジェクトの内容を格納するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することで、バイト配列のサイズを決定できます。
   * `System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出し、バイト配列、開始位置、読み取るストリーム長を渡すことにより、バイト配列にストリームデータを入力します。
   * `MTOM` フィールドにバイト配列の内容を割り当てて、`BLOB` オブジェクトにデータを入力します。

1. PDF フォームからデータを書き出します。

   `FormDataIntegrationClient` オブジェクトの `exportData` メソッドを呼び出して PDF フォームにデータをインポートし、PDF フォームを格納する `BLOB` オブジェクトを渡します。このメソッドは、フォームデータを XML スキーマとして格納する `BLOB` オブジェクトを返します。

1. PDF フォームを PDF ファイルとして保存します。

   * コンストラクターを呼び出し、XML ファイルの場所を表す文字列値を渡すことで `System.IO.FileStream` オブジェクトを作成します。
   * `exportData` メソッドによって返された `BLOB` オブジェクトのデータコンテンツを格納するバイト配列を作成します。 `BLOB` オブジェクトの `MTOM` フィールドの値を取得してバイト配列を入力します。
   * コンストラクターを呼び出して `System.IO.FileStream` オブジェクトを渡すことによって、`System.IO.BinaryWriter` オブジェクトを作成します。
   * `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを呼び出してバイト配列を渡すことによって、バイト配列の内容を XML ファイルに書き込みます。

**関連トピック**

[手順の概要](importing-exporting-data.md#summary-of-steps)

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
