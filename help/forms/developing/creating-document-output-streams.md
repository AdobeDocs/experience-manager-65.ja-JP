---
title: ドキュメント出力ストリームの作成
seo-title: ドキュメント出力ストリームの作成
description: Outputサービスを使用して、ドキュメントをPDF（PDF/Aドキュメントを含む）、PostScript、Printer Control Language(PCL)およびZebra - ZPL、Intermec - IPL、Datamax - DPL、TecToshiba - TPCLラベル形式で変換します。
seo-description: Outputサービスを使用して、ドキュメントをPDF（PDF/Aドキュメントを含む）、PostScript、Printer Control Language(PCL)およびZebra - ZPL、Intermec - IPL、Datamax - DPL、TecToshiba - TPCLラベル形式で変換します。
uuid: 80c28efa-35ce-4073-9ca6-2d93bcd67fdd
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: de527d50-991b-4ca3-a8ac-44d5cab988e9
role: Developer
exl-id: a521bfac-f417-4002-9c5c-8d7794d3eec7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '19044'
ht-degree: 4%

---

# ドキュメント出力ストリームの作成{#creating-document-output-streams}

**このドキュメントのサンプルと例は、JEE上のAEM Forms環境に限られています。**

**Outputサービスについて**

Outputサービスを使用すると、ドキュメントをPDF（PDF/Aドキュメントを含む）、PostScript、Printer Control Language(PCL)および次のラベル形式で出力できます。

* ゼブラ — ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

Outputサービスを使用すると、XMLフォームデータをフォームデザインとマージし、ドキュメントをネットワークプリンターまたはファイルに出力できます。

フォームデザイン（XDPファイル）をOutputサービスに渡す方法は2つあります。 フォームデザインを含む`com.adobe.idp.Document`インスタンスをOutputサービスに渡すこともできます。 または、フォームデザインの場所を指定するURI値を渡すこともできます。 これらの方法は、*AEM formsによるプログラミング*&#x200B;で説明します。

>[!NOTE]
>
>Outputサービスは、アプリケーションオブジェクト固有のスクリプトを含むAcroform PDFドキュメントをサポートしていません。 アプリケーションオブジェクト固有のスクリプトを含むAcroform PDFドキュメントは、レンダリングされません。

次の節では、URI値を使用してフォームデザインをOutputサービスに渡す方法について説明します。

* [PDFドキュメントの作成](creating-document-output-streams.md#creating-pdf-documents)
* [PDF/Aドキュメントの作成](creating-document-output-streams.md#creating-pdf-a-documents)

以下の節では、`com.adobe.idp.Document`インスタンス内でフォームデザインを渡す方法を示します。

* [Content Services（非推奨）にあるドキュメントをOutputサービスに渡す](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)
* [フラグメントを使用したPDFドキュメントの作成](creating-document-output-streams.md#creating-pdf-documents-using-fragments)

使用する方法を決定する際の考慮事項の1つは、別のAEM Formsサービスからフォームデザインを取得し、`com.adobe.idp.Document`インスタンス内で渡す場合です。 「*Apsing Documents to the Output Service*」および「*Creating PDF Documents using Fragments*」の両方の節で、別のAEM Formsサービスからフォームデザインを取得する方法を示します。 最初の節では、Content Services（非推奨）からフォームデザインを取得します。 2つ目の節では、フォームデザインをAssemblerサービスから取得します。

ファイルシステムなどの固定の場所からフォームデザインを取得する場合は、どちらの方法でも使用できます。 つまり、URI値をXDPファイルに指定するか、`com.adobe.idp.Document`インスタンスを使用できます。

PDFドキュメントの作成時にフォームデザインの場所を指定するURI値を渡すには、`generatePDFOutput`メソッドを使用します。 同様に、PDFドキュメントの作成時に`com.adobe.idp.Document`インスタンスをOutputサービスに渡すには、`generatePDFOutput2`メソッドを使用します。

出力ストリームをネットワークプリンターに送信する場合は、どちらの方法も使用できます。 フォームデザインを含む`com.adobe.idp.Document`インスタンスを渡して出力ストリームをプリンターに送信するには、`sendToPrinter2`メソッドを使用します。 URI値を渡して出力ストリームをプリンターに送信するには、`sendToPrinter`メソッドを使用します。 *プリンターへの印刷ストリームの送信*&#x200B;セクションでは、`sendToPrinter`メソッドを使用します。

Outputサービスを使用して、次のタスクを実行できます。

* [PDFドキュメントの作成](creating-document-output-streams.md#creating-pdf-documents)
* [PDF/Aドキュメントの作成](creating-document-output-streams.md#creating-pdf-a-documents)
* [Content Services（非推奨）にあるドキュメントをOutputサービスに渡す](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)
* [フラグメントを使用したPDFドキュメントの作成](creating-document-output-streams.md#creating-pdf-documents-using-fragments)
* [ファイルへの印刷](creating-document-output-streams.md#printing-to-files)
* [プリンターへの印刷ストリームの送信](creating-document-output-streams.md#sending-print-streams-to-printers)
* [複数の出力ファイルの作成](creating-document-output-streams.md#creating-multiple-output-files)
* [検索ルールの作成](creating-document-output-streams.md#creating-search-rules)
* [PDFドキュメントの統合](creating-document-output-streams.md#flattening-pdf-documents)

>[!NOTE]
>
>Outputサービスについて詳しくは、『AEM Formsのサービスリファレンス[』を参照してください。](https://www.adobe.com/go/learn_aemforms_services_63)

## PDFドキュメントの作成{#creating-pdf-documents}

Outputサービスを使用して、指定したフォームデザインとXMLフォームデータに基づくPDFドキュメントを作成できます。 Outputサービスで作成されるPDFドキュメントは、インタラクティブPDFドキュメントではありません。ユーザーはフォームデータを入力または変更できません。

長期保存を目的としたPDFドキュメントを作成する場合は、PDF/Aドキュメントを作成することをお勧めします。 （[PDF/Aドキュメントの作成](creating-document-output-streams.md#creating-pdf-a-documents)を参照）。

ユーザーがデータを入力できるインタラクティブPDFフォームを作成するには、Formsサービスを使用します。 ([インタラクティブPDF formsのレンダリング](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms)を参照)。

>[!NOTE]
>
>Outputサービスについて詳しくは、『AEM Formsのサービスリファレンス[』を参照してください。](https://www.adobe.com/go/learn_aemforms_services_63)

### 手順の概要{#summary-of-steps}

PDFドキュメントを作成するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Outputクライアントオブジェクトを作成します。
1. XMLデータソースを参照します。
1. PDF実行時オプションを設定します。
1. レンダリングの実行時オプションを設定します。
1. PDFドキュメントを生成します。
1. 操作の結果を取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用する場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(AEM FormsがJBossにデプロイされている場合に必須)
* jbossall-client.jar(AEM FormsがJBossにデプロイされている場合に必須)

AEM FormsがJBoss以外のサポート対象のJ2EEアプリケーションサーバーにデプロイされている場合は、adobe-utilities.jarファイルとjbossall-client.jarファイルを、AEM FormsがデプロイされているJ2EEアプリケーションサーバーに固有のJARファイルに置き換える必要があります。

**Outputクライアントオブジェクトの作成**

プログラムによってOutputサービス操作を実行する前に、Outputサービスクライアントオブジェクトを作成する必要があります。 Java APIを使用している場合は、`OutputClient`オブジェクトを作成します。 Output WebサービスAPIを使用している場合は、`OutputServiceService`オブジェクトを作成します。

**XMLデータソースの参照**

データとフォームデザインを結合するには、データを含むXMLデータソースを参照する必要があります。 データを入力するフォームフィールドごとに、XML要素が存在する必要があります。 XML要素名は、フィールド名と一致する必要があります。 XML要素がフォームフィールドに対応していない場合や、XML要素名がフィールド名と一致しない場合は無視されます。 すべてのXML要素を指定した場合、XML要素の表示順序を一致させる必要はありません。

次のサンプルのローン申し込みフォームを考えてみましょう。

![cp_cp_loanformdata](assets/cp_cp_loanformdata.png)

このフォームデザインにデータをマージするには、フォームに対応するXMLデータソースを作成する必要があります。 次のXMLは、サンプルの住宅ローン申し込みフォームに対応するXDP XMLデータソースを表しています。

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

**PDF実行時オプションの設定**

PDFドキュメントを作成する際に「file URI」オプションを設定します。 このオプションは、Outputサービスが生成するPDFファイルの名前と場所を指定します。

>[!NOTE]
>
>ファイルURIランタイムオプションを設定する代わりに、Outputサービスから返される複雑なデータ型からPDFドキュメントをプログラムで取得できます。 ただし、ファイルURIランタイムオプションを設定することで、PDFドキュメントをプログラムで取得するアプリケーションロジックを作成する必要はありません。

**レンダリング実行時オプションの設定**

PDFドキュメントの作成時にレンダリングの実行時オプションを設定できます。 これらのオプションは必須ではありませんが（必要なPDFランタイムオプションとは異なり）、Outputサービスのパフォーマンス向上などのタスクを実行できます。 例えば、Outputサービスが使用するフォームデザインをキャッシュして、パフォーマンスを向上させることができます。

タグ付きAcrobatフォームを入力として使用する場合、OutputサービスJavaまたはWebサービスAPIを使用してタグ付き設定をオフにすることはできません。 プログラムでこのオプションを`false`に設定しようとすると、結果のPDFドキュメントは引き続きタグ付けされます。

>[!NOTE]
>
>レンダリング実行時オプションを指定しない場合は、デフォルト値が使用されます。 実行時オプションのレンダリングについて詳しくは、`RenderOptionsSpec`クラス参照を参照してください。 (『AEM Forms APIリファレンス[』を参照)。](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)

**PDFドキュメントの生成**

フォームデータを含む有効なXMLデータソースを参照し、実行時オプションを設定したら、Outputサービスを呼び出すと、PDFドキュメントが生成されます。

PDFドキュメントを生成する場合、PDFドキュメントを作成するためにOutputサービスで必要なURI値を指定します。 フォームデザインは、サーバーファイルシステムなどの場所や、AEM Formsアプリケーションの一部として保存できます。 Formsアプリケーションの一部として存在するフォームデザイン（または画像ファイルなどの他のリソース）は、コンテンツルートURI値`repository:///`を使用して参照できます。 例えば、*Applications/FormsApplication*&#x200B;という名前のFormsアプリケーション内にある&#x200B;*Loan.xdp*&#x200B;という名前のフォームデザインを考えてみましょう。

![cp_cp_formrepository](assets/cp_cp_formrepository.png)

前の図に示すLoan.xdpファイルにアクセスするには、`OutputClient`オブジェクトの`generatePDFOutput`メソッドに渡す3番目のパラメーターとして`repository:///Applications/FormsApplication/1.0/FormsFolder/`を指定します。 フォーム名(*Loan.xdp*)を、`OutputClient`オブジェクトの`generatePDFOutput`メソッドに渡す2番目のパラメーターとして指定します。

XDPファイルに画像（またはフラグメントなどの他のリソース）が含まれている場合は、XDPファイルと同じアプリケーションフォルダーにリソースを配置します。 AEM Formsは、コンテンツルートURIをベースパスとして使用して、画像への参照を解決します。 例えば、Loan.xdpファイルに画像が含まれている場合、必ず`Applications/FormsApplication/1.0/FormsFolder/`に画像を配置してください。

>[!NOTE]
>
>`OutputClient`オブジェクトの`generatePDFOutput`または`generatePrintedOutput`メソッドを呼び出すときに、FormsアプリケーションURIを参照できます。

>[!NOTE]
>
>Formsアプリケーション内のXDPを参照してPDFドキュメントを作成する完全なクイックスタートを確認するには、「[クイックスタート（EJBモード）」を参照してください。Java API](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api)を使用したアプリケーションXDPファイルに基づくPDFドキュメントの作成

**操作の結果の取得**

Outputサービスが操作を実行すると、その操作が成功したかどうかを示すステータスXMLデータなど、様々なデータ項目が返されます。

**関連トピック**

[Java APIを使用したPDFドキュメントの作成](creating-document-output-streams.md#create-a-pdf-document-using-the-java-api)

[WebサービスAPIを使用したPDFドキュメントの作成](creating-document-output-streams.md#create-a-pdf-document-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[OutputサービスAPIのクイックスタート](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Java API {#create-a-pdf-document-using-the-java-api}を使用してPDFドキュメントを作成します

Output API(Java)を使用してPDFドキュメントを作成します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-output-client.jarなどのクライアントJARファイルを含めます。

1. Outputクライアントオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して`OutputClient`オブジェクトを渡し、`ServiceClientFactory`オブジェクトを作成します。

1. XMLデータソースを参照します。

   * PDFドキュメントのコンストラクターを使用し、XMLファイルの場所を指定する文字列値を渡すことで、PDFドキュメントの入力に使用されるXMLデータソースを表す`java.io.FileInputStream`オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを作成します。`java.io.FileInputStream`オブジェクトを渡します。

1. PDF実行時オプションを設定します。

   * コンストラクタを使用して `PDFOutputOptionsSpec` オブジェクトを作成します。
   * `PDFOutputOptionsSpec`オブジェクトの`setFileURI`メソッドを呼び出して、「 File URI 」オプションを設定します。 Outputサービスが生成するPDFファイルの場所を指定するstring値を渡します。 「ファイルURI 」オプションは、AEM FormsをホストするJ2EEアプリケーションサーバーに対して相対的なもので、クライアントコンピューターに対しては相対的なものではありません。

1. レンダリングの実行時オプションを設定します。

   * コンストラクタを使用して `RenderOptionsSpec` オブジェクトを作成します。
   * `RenderOptionsSpec`オブジェクトの`setCacheEnabled`を呼び出して`true`を渡すことで、フォームデザインをキャッシュし、Outputサービスのパフォーマンスを向上させます。

   >[!NOTE]
   >
   >入力ドキュメントがAcrobatフォーム(Acrobatで作成されたフォーム)または署名または認証されたXFAドキュメントの場合は、 `RenderOptionsSpec`オブジェクトの`setPdfVersion`メソッドを使用してPDFドキュメントのバージョンを設定することはできません。 出力PDFドキュメントは、元のPDFバージョンを保持します。 同様に、入力ドキュメントがAcrobatフォームまたは署名済みまたは認証済みのXFAドキュメントの場合、 `RenderOptionsSpec`オブジェクトの`setTaggedPDF`メソッドを呼び出して、タグ付きAdobe PDFオプションを設定することはできません。

   >[!NOTE]
   >
   >入力PDFドキュメントが認証またはデジタル署名されている場合、`RenderOptionsSpec`オブジェクトの`setLinearizedPDF`メソッドを使用して線形化されたPDFオプションを設定することはできません。 （[PDFドキュメントのデジタル署名&#x200B;](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)*を参照）*

1. PDFドキュメントを生成します。

   `OutputClient`オブジェクトの`generatePDFOutput`メソッドを呼び出し、次の値を渡してPDFドキュメントを作成します。

   * `TransformationFormat`列挙値。 PDFドキュメントを生成するには、`TransformationFormat.PDF`を指定します。
   * フォームデザイン名を指定する string 値。
   * フォームデザインが存在するコンテンツルートを指定するstring値。
   * PDFランタイムオプションを含む`PDFOutputOptionsSpec`オブジェクト。
   * レンダリングの実行時オプションを含む`RenderOptionsSpec`オブジェクト。
   * フォームデザインとマージするデータを含むXMLデータソースを含む`com.adobe.idp.Document`オブジェクト。

   `generatePDFOutput`メソッドは、操作の結果を含む`OutputResult`オブジェクトを返します。

   >[!NOTE]
   >
   >`generatePDFOutput`メソッドを呼び出してPDFドキュメントを生成する場合、署名または認証されたXFA PDFフォームとデータを結合することはできません。 （[Digital Signing and Certifying Documents ](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-and-certifying-documents)*を参照）。*

   >[!NOTE]
   >
   >`OutputResult`オブジェクトの`getRecordLevelMetaDataList`メソッドは、`null`*.*&#x200B;を返します。

   >[!NOTE]
   >
   >`OutputClient`オブジェクトの`generatePDFOutput2`メソッドを呼び出して、PDFドキュメントを作成することもできます。 ([Content Services（非推奨）にあるドキュメントをOutputサービスに渡す&#x200B;](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)*を参照)*

1. 操作の結果を取得します。

   * `OutputResult`オブジェクトの`getStatusDoc`メソッドを呼び出して、`generatePDFOutput`操作のステータスを表す`com.adobe.idp.Document`オブジェクトを取得します。 このメソッドは、操作が成功したかどうかを示すステータスXMLデータを返します。
   * 操作の結果を格納する`java.io.File`オブジェクトを作成します。 ファイル名の拡張子が.xmlであることを確認します。
   * `com.adobe.idp.Document`オブジェクトの`copyToFile`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトの内容をファイルにコピーします（`getStatusDoc`メソッドで返された`com.adobe.idp.Document`オブジェクトを使用するようにしてください）。

   Outputサービスは、 `PDFOutputOptionsSpec`オブジェクトの`setFileURI`メソッドに渡される引数で指定された場所にPDFドキュメントを書き込みますが、 `OutputResult`オブジェクトの`getGeneratedDoc`メソッドを呼び出すことで、プログラムでPDF/Aドキュメントを取得できます。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[クイックスタート（EJBモード）:Java APIを使用したPDFドキュメントの作成](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[クイックスタート（SOAPモード）:Java APIを使用したPDFドキュメントの作成](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#create-a-pdf-document-using-the-web-service-api}を使用してPDFドキュメントを作成します

Output API（Webサービス）を使用してPDFドキュメントを作成します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. Outputクライアントオブジェクトを作成します。

   * デフォルトのコンストラクターを使用して`OutputServiceClient`オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`OutputServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに渡す文字列値（例：`http://localhost:8080/soap/services/OutputService?blob=mtom`）を渡します。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する際に使用されます。 ただし、MTOMを使用する場合は`?blob=mtom`を指定します。
   * `OutputServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値は、MTOMが使用されるようにします。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールド`OutputServiceClient.ClientCredentials.UserName.UserName`にAEM formsユーザー名を割り当てます。
      * 対応するパスワード値をフィールド`OutputServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * フィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に定数値`HttpClientCredentialType.Basic`を割り当てます。
      * フィールド`BasicHttpBindingSecurity.Security.Mode`に定数値`BasicHttpSecurityMode.TransportCredentialOnly`を割り当てます。

1. XMLデータソースを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、PDFドキュメントとマージされるXMLデータを保存するために使用されます。
   * コンストラクターを呼び出し、フォームデータを含むXMLファイルのファイル位置を表す文字列値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得することで、バイト配列のサイズを判断できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことによって、バイト配列にストリームデータを入力します。
   * `BLOB`オブジェクトの`MTOM`フィールドにバイト配列の内容を割り当てて、オブジェクトを設定します。

1. PDF実行時オプションの設定

   * コンストラクタを使用して `PDFOutputOptionsSpec` オブジェクトを作成します。
   * Outputサービスが生成するPDFファイルの場所を指定する文字列値を`PDFOutputOptionsSpec`オブジェクトの`fileURI`データメンバーに割り当てて、「File URI」オプションを設定します。 「ファイルURI 」オプションは、AEM FormsをホストするJ2EEアプリケーションサーバーに対して相対的なもので、クライアントコンピューターに対しては相対的なものではありません。

1. レンダリングの実行時オプションを設定します。

   * コンストラクタを使用して `RenderOptionsSpec` オブジェクトを作成します。
   * 値`true`を`RenderOptionsSpec`オブジェクトの`cacheEnabled`データメンバーに割り当てることで、フォームデザインをキャッシュして、Outputサービスのパフォーマンスを向上させます。

   >[!NOTE]
   >
   >入力ドキュメントがAcrobatフォーム(Acrobatで作成されたフォーム)または署名または認証されたXFAドキュメントの場合は、 `RenderOptionsSpec`オブジェクトの`setPdfVersion`メソッドを使用してPDFドキュメントのバージョンを設定することはできません。 出力PDFドキュメントは、元のPDFバージョンを保持します。 同様に、入力ドキュメントがAcrobatフォームまたは署名済みまたは認証済みのXFAドキュメントの場合、 `RenderOptionsSpec`オブジェクトの`setTaggedPDF`*メソッドを呼び出して、タグ付きAdobe PDFオプションを設定することはできません。*

   >[!NOTE]
   >
   >入力PDFドキュメントが認証またはデジタル署名されている場合、`RenderOptionsSpec`オブジェクトの`linearizedPDF`メンバを使用して線形化されたPDFオプションを設定することはできません。 （[PDFドキュメントのデジタル署名&#x200B;](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)*を参照）*

1. PDFドキュメントを生成します。

   `OutputServiceService`オブジェクトの`generatePDFOutput`メソッドを呼び出し、次の値を渡してPDFドキュメントを作成します。

   * `TransformationFormat`列挙値。 PDFドキュメントを生成するには、`TransformationFormat.PDF`を指定します。
   * フォームデザイン名を指定する string 値。
   * フォームデザインが存在するコンテンツルートを指定するstring値。
   * PDFランタイムオプションを含む`PDFOutputOptionsSpec`オブジェクト。
   * レンダリングの実行時オプションを含む`RenderOptionsSpec`オブジェクト。
   * フォームデザインとマージするデータを含むXMLデータソースを含む`BLOB`オブジェクト。
   * `generatePDFOutput`メソッドによって設定される`BLOB`オブジェクト。 `generatePDFOutput`メソッドは、このオブジェクトに、ドキュメントを表す生成済みのメタデータを入力します。 （このパラメーター値は、Webサービスの呼び出しにのみ必要です）。
   * `generatePDFOutput`メソッドによって設定される`BLOB`オブジェクト。 `generatePDFOutput`メソッドは、このオブジェクトに結果データを入力します。 （このパラメーター値は、Webサービスの呼び出しにのみ必要です）。
   * 操作の結果を格納する`OutputResult`オブジェクト。 （このパラメーター値は、Webサービスの呼び出しにのみ必要です）。

   >[!NOTE]
   >
   >`generatePDFOutput`メソッドを呼び出してPDFドキュメントを生成する場合、署名または認証されたXFA PDFフォームとデータを結合することはできません。 （[Digital Signing and Certifying Documents ](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-and-certifying-documents)*を参照）。*

   >[!NOTE]
   >
   >`OutputClient`オブジェクトの`generatePDFOutput2`メソッドを呼び出して、PDFドキュメントを作成することもできます。 ([Content Services（非推奨）にあるドキュメントをOutputサービスに渡す&#x200B;](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)*を参照)*

1. 操作の結果を取得します。

   * コンストラクターを呼び出し、結果データを含むXMLファイルの場所を表す文字列値を渡すことで、`System.IO.FileStream`オブジェクトを作成します。 ファイル名の拡張子が.xmlであることを確認します。
   * `OutputServiceService`オブジェクトの`generatePDFOutput`メソッド（8番目のパラメーター）によって結果データが入力された`BLOB`オブジェクトのデータコンテンツを格納するバイト配列を作成します。 `BLOB`オブジェクトの`MTOM` `field`の値を取得して、バイト配列を設定します。
   * コンストラクターを呼び出し、`System.IO.FileStream`オブジェクトを渡して、`System.IO.BinaryWriter`オブジェクトを作成します。
   * `System.IO.BinaryWriter`オブジェクトの`Write`メソッドを呼び出し、バイト配列を渡すことにより、バイト配列の内容をXMLファイルに書き込みます。

   関連トピック

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

   >[!NOTE]
   >
   >`OutputServiceService`オブジェクトの`generateOutput`メソッドは非推奨です。

## PDF/Aドキュメントの作成{#creating-pdf-a-documents}

Outputサービスを使用してPDF/Aドキュメントを作成できます。 PDF/Aはドキュメントのコンテンツを長期保存するためのアーカイブ形式なので、すべてのフォントが埋め込まれ、ファイルが非圧縮になります。 その結果、通常、PDF/A ドキュメントは標準の PDF ドキュメントよりも大きくなります。また、PDF/Aドキュメントにはオーディオおよびビデオコンテンツは含まれません。 他のOutputサービスタスクと同様に、フォームデザインとフォームデザインとのマージ用のデータの両方を提供して、PDF/Aドキュメントを作成します。

PDF/A-1仕様は、aとbの2つの準拠レベルで構成されています。この2つの主な違いは、論理構造（アクセシビリティ）のサポートに関するもので、適合レベルbには必要ありません。適合レベルに関係なく、PDF/A-1では、生成されるPDF/Aドキュメントにすべてのフォントが埋め込まれます。

PDF/AはPDFドキュメントのアーカイブの標準ですが、会社のニーズを満たす標準PDFドキュメントの場合は、PDF/Aをアーカイブに使用する必要はありません。 PDF/A標準の目的は、ドキュメントの保存要件を満たすと共に、長期間保存できるPDFファイルを確立することです。 例えば、URLが無効になる可能性があるので、PDF/AにURLを埋め込むことはできません。

組織は、独自のニーズ、ドキュメントの保持期間、ファイルサイズに関する考慮事項を評価し、独自のアーカイブ戦略を決定する必要があります。 DocConverterサービスを使用すると、PDFドキュメントがPDF/Aに準拠しているかどうかをプログラムで判断できます。 （[プログラムによるPDF/Aの準拠の判別](/help/forms/developing/pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)を参照）。

PDF/Aドキュメントでは、フォームデザインで指定されたフォントを使用する必要があり、フォントを置き換えることはできません。 その結果、PDFドキュメント内のフォントがホストオペレーティングシステム(OS)で使用できない場合、例外が発生します。

AcrobatでPDF/Aドキュメントを開くと、次の図に示すように、ドキュメントがPDF/Aドキュメントであることを確認するメッセージが表示されます。

![cp_cp_pdfamessage](assets/cp_cp_pdfamessage.png)

>[!NOTE]
>
>AIIMのWebサイトには、[https://www.aiim.org/documents/standards/19005-1_FAQ.pdf](https://www.aiim.org/documents/standards/19005-1_FAQ.pdf)でアクセスできるPDF/AのFAQセクションがあります。

>[!NOTE]
>
>Outputサービスについて詳しくは、『AEM Formsのサービスリファレンス[』を参照してください。](https://www.adobe.com/go/learn_aemforms_services_63)

### 手順の概要{#summary_of_steps-1}

PDF/Aドキュメントを作成するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Outputクライアントオブジェクトを作成します。
1. XMLデータソースを参照します。
1. PDF/Aランタイムオプションを設定します。
1. レンダリングの実行時オプションを設定します。
1. PDF/Aドキュメントを生成します。
1. 操作の結果を取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してカスタムアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用する場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(AEM FormsがJBossにデプロイされている場合に必須)
* jbossall-client.jar(AEM FormsがJBossにデプロイされている場合に必須)

AEM FormsがJBoss以外のサポート対象のJ2EEアプリケーションサーバーにデプロイされている場合は、adobe-utilities.jarファイルとjbossall-client.jarファイルを、AEM FormsがデプロイされているJ2EEアプリケーションサーバーに固有のJARファイルに置き換える必要があります。

**Outputクライアントオブジェクトの作成**

プログラムによってOutputサービス操作を実行する前に、Outputサービスクライアントオブジェクトを作成する必要があります。 Java APIを使用している場合は、`OutputClient`オブジェクトを作成します。 Output WebサービスAPIを使用している場合は、`OutputServiceService`オブジェクトを作成します。

**XMLデータソースの参照**

データとフォームデザインを結合するには、データを含むXMLデータソースを参照する必要があります。 データを入力するフォームフィールドごとに、XML要素が存在する必要があります。 XML要素名は、フィールド名と一致する必要があります。 XML要素がフォームフィールドに対応していない場合や、XML要素名がフィールド名と一致しない場合は無視されます。 すべてのXML要素を指定した場合、XML要素の表示順序を一致させる必要はありません。

**PDF/Aランタイムオプションの設定**

PDF/Aドキュメントを作成する際に、「ファイルURI 」オプションを設定できます。 このURIは、AEM FormsをホストするJ2EEアプリケーションサーバーに対する相対パスです。 つまり、C:\Adobeを設定した場合、ファイルはクライアントコンピューターではなく、サーバー上のフォルダーに書き込まれます。 このURIは、Outputサービスが生成するPDF/Aファイルの名前と場所を指定します。

**レンダリング実行時オプションの設定**

PDF/Aドキュメントの作成時にレンダリングの実行時オプションを設定できます。 PDF/Aに関連して設定できるオプションは、`PDFAConformance`と`PDFARevisionNumber`の2つです。 `PDFAConformance`の値は、電子ドキュメントの長期保存方法を指定する要件にPDFドキュメントがどのように従うかを示します。 このオプションの有効な値は`A`と`B`です。 レベルaおよびbの準拠について詳しくは、「*ISO 19005-1 Document management*」というタイトルのPDF/A-1 ISO仕様を参照してください。

`PDFARevisionNumber`値は、PDF/Aドキュメントのリビジョン番号を参照します。 PDF/Aドキュメントのリビジョン番号について詳しくは、「*ISO 19005-1 Document management*」というタイトルのPDF/A-1 ISO仕様を参照してください。

>[!NOTE]
>
>PDF/A 1Aドキュメントを作成する際に、タグ付きAdobe PDFオプションを`false`に設定することはできません。 PDF/A 1Aは、常にタグ付きPDFドキュメントになります。 また、PDF/A 1Bドキュメントを作成する際に、タグ付きAdobe PDFオプションを`true`に設定することはできません。 PDF/A 1Bは、常にタグなしのPDFドキュメントになります。

**PDF/Aドキュメントの生成**

フォームデータを含む有効なXMLデータソースを参照し、ランタイムオプションを設定した後、Outputサービスを呼び出して、PDF/Aドキュメントを生成することができます。

**操作の結果の取得**

Outputサービスが操作を実行すると、その操作が成功したかどうかを示すXMLデータなど、様々なデータ項目が返されます。

**関連トピック**

[Java APIを使用したPDF/Aドキュメントの作成](creating-document-output-streams.md#create-a-pdf-a-document-using-the-java-api)

[WebサービスAPIを使用したPDF/Aドキュメントの作成](creating-document-output-streams.md#create-a-pdf-a-document-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[OutputサービスAPIのクイックスタート](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Java API {#create-a-pdf-a-document-using-the-java-api}を使用したPDF/Aドキュメントの作成

Output API(Java)を使用してPDF/Aドキュメントを作成します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-output-client.jarなどのクライアントJARファイルを含めます。

1. Outputクライアントオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して`OutputClient`オブジェクトを渡し、`ServiceClientFactory`オブジェクトを作成します。

1. XMLデータソースを参照します。

   * PDF/Aドキュメントのコンストラクターを使用し、XMLファイルの場所を指定する文字列値を渡すことで、PDF/Aドキュメントの入力に使用されるXMLデータソースを表す`java.io.FileInputStream`オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PDF/Aランタイムオプションを設定します。

   * コンストラクタを使用して `PDFOutputOptionsSpec` オブジェクトを作成します。
   * `PDFOutputOptionsSpec`オブジェクトの`setFileURI`メソッドを呼び出して、「 File URI 」オプションを設定します。 Outputサービスが生成するPDFファイルの場所を指定するstring値を渡します。 「ファイルURI 」オプションは、AEM FormsをホストするJ2EEアプリケーションサーバーに対して相対的なもので、クライアントコンピューターに対しては相対的なものではありません。

1. レンダリングの実行時オプションを設定します。

   * コンストラクタを使用して `RenderOptionsSpec` オブジェクトを作成します。
   * `RenderOptionsSpec`オブジェクトの`setPDFAConformance`メソッドを呼び出し、適合レベルを指定する`PDFAConformance`列挙値を渡すことで、`PDFAConformance`値を設定します。 例えば、適合レベルAを指定するには、`PDFAConformance.A`を渡します。
   * `RenderOptionsSpec`オブジェクトの`setPDFARevisionNumber`メソッドを呼び出して`PDFARevisionNumber.Revision_1`を渡すことで、`PDFARevisionNumber`値を設定します。

   >[!NOTE]
   >
   >PDF/AドキュメントのPDFバージョンは、`RenderOptionsSpec`オブジェクトの&#x200B;`setPdfVersion`*メソッドに対してどの値を指定したかに関係なく、1.4です。*

1. PDF/Aドキュメントを生成します。

   `OutputClient`オブジェクトの`generatePDFOutput`メソッドを呼び出し、次の値を渡してPDF/Aドキュメントを作成します。

   * `TransformationFormat`列挙値。 PDF/Aドキュメントを生成するには、`TransformationFormat.PDFA`を指定します。
   * フォームデザイン名を指定する string 値。
   * フォームデザインが存在するコンテンツルートを指定するstring値。
   * PDFランタイムオプションを含む`PDFOutputOptionsSpec`オブジェクト。
   * レンダリングの実行時オプションを含む`RenderOptionsSpec`オブジェクト。
   * フォームデザインとマージするデータを含むXMLデータソースを含む`com.adobe.idp.Document`オブジェクト。

   `generatePDFOutput`メソッドは、操作の結果を含む`OutputResult`オブジェクトを返します。

   >[!NOTE]
   >
   >`OutputResult`オブジェクトの`getRecordLevelMetaDataList`メソッドは`null`を返します。

   >[!NOTE]
   >
   >`OutputClient`オブジェクトの`generatePDFOutput`2メソッドを呼び出して、PDF /Aドキュメントを作成することもできます。 ([Content Services（非推奨）にあるドキュメントをOutputサービスに渡す](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)を参照)。

1. 操作の結果を取得します。

   * `OutputResult`オブジェクトの`getStatusDoc`メソッドを呼び出して、`generatePDFOutput`メソッドのステータスを表す`com.adobe.idp.Document`オブジェクトを作成します。
   * 操作の結果を格納する`java.io.File`オブジェクトを作成します。 ファイル名の拡張子が.xmlであることを確認します。
   * `com.adobe.idp.Document`オブジェクトの`copyToFile`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトの内容をファイルにコピーします（`getStatusDoc`メソッドで返された`com.adobe.idp.Document`オブジェクトを使用するようにしてください）。

   >[!NOTE]
   >
   >Outputサービスは、 `PDFOutputOptionsSpec`オブジェクトの`setFileURI`メソッドに渡される引数で指定された場所にPDF/Aドキュメントを書き込みますが、 `OutputResult`オブジェクトの`getGeneratedDoc`メソッドを呼び出すことで、プログラムでPDF/Aドキュメントを取得できます。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[クイックスタート（SOAPモード）:Java APIを使用したPDF/Aドキュメントの作成](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-a-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

### WebサービスAPI {#create-a-pdf-a-document-using-the-web-service-api}を使用してPDF/Aドキュメントを作成します

Output API（Webサービス）を使用してPDF/Aドキュメントを作成します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. Outputクライアントオブジェクトを作成します。

   * デフォルトのコンストラクターを使用して`OutputServiceClient`オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`OutputServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに渡す文字列値（例：`http://localhost:8080/soap/services/OutputService?blob=mtom`）を渡します。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する際に使用されます。 ただし、MTOMを使用する場合は`?blob=mtom`を指定します。
   * `OutputServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値は、MTOMが使用されるようにします。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールド`OutputServiceClient.ClientCredentials.UserName.UserName`にAEM formsユーザー名を割り当てます。
      * 対応するパスワード値をフィールド`OutputServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * フィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に定数値`HttpClientCredentialType.Basic`を割り当てます。
      * フィールド`BasicHttpBindingSecurity.Security.Mode`に定数値`BasicHttpSecurityMode.TransportCredentialOnly`を割り当てます。

1. XMLデータソースを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、PDF/Aドキュメントとマージされるデータを保存するために使用します。
   * コンストラクターを呼び出し、暗号化するPDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得することで、バイト配列のサイズを判断できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことによって、バイト配列にストリームデータを入力します。
   * `BLOB`オブジェクトの`MTOM`フィールドにバイト配列の内容を割り当てて、オブジェクトを設定します。

1. PDF/Aランタイムオプションを設定します。

   * コンストラクタを使用して `PDFOutputOptionsSpec` オブジェクトを作成します。
   * Outputサービスが生成するPDFファイルの場所を指定する文字列値を`PDFOutputOptionsSpec`オブジェクトの`fileURI`データメンバーに割り当てて、「File URI」オプションを設定します。 「ファイルURI 」オプションは、AEM FormsをホストするJ2EEアプリケーションサーバーに対して相対的なもので、クライアントコンピューターに対しては相対的なものではありません

1. レンダリングの実行時オプションを設定します。

   * コンストラクタを使用して `RenderOptionsSpec` オブジェクトを作成します。
   * `PDFAConformance`値を設定するには、`RenderOptionsSpec`オブジェクトの`PDFAConformance`データメンバーに`PDFAConformance`列挙値を割り当てます。 例えば、適合レベルAを指定するには、このデータメンバーに`PDFAConformance.A`を割り当てます。
   * `PDFARevisionNumber`値を設定するには、`RenderOptionsSpec`オブジェクトの`PDFARevisionNumber`データメンバーに`PDFARevisionNumber`列挙値を割り当てます。 `PDFARevisionNumber.Revision_1`をこのデータメンバーに割り当てます。

   >[!NOTE]
   >
   >PDF/AドキュメントのPDFバージョンは、指定した値に関係なく1.4です。

1. PDF/Aドキュメントを生成します。

   `OutputServiceService`オブジェクトの`generatePDFOutput`メソッドを呼び出し、次の値を渡してPDFドキュメントを作成します。

   * TransformationFormat列挙値。 PDFドキュメントを生成するには、`TransformationFormat.PDFA`を指定します。
   * フォームデザイン名を指定する string 値。
   * フォームデザインが存在するコンテンツルートを指定するstring値。
   * PDFランタイムオプションを含む`PDFOutputOptionsSpec`オブジェクト。
   * レンダリングの実行時オプションを含む`RenderOptionsSpec`オブジェクト。
   * フォームデザインとマージするデータを含むXMLデータソースを含む`BLOB`オブジェクト。
   * `generatePDFOutput`メソッドによって設定される`BLOB`オブジェクト。 `generatePDFOutput`メソッドは、このオブジェクトに、ドキュメントを表す生成済みのメタデータを入力します。 （このパラメーター値は、Webサービスの呼び出しのみに必要です）。
   * `generatePDFOutput`メソッドによって設定される`BLOB`オブジェクト。 `generatePDFOutput`メソッドは、このオブジェクトに結果データを入力します。 （このパラメーター値は、Webサービスの呼び出しのみに必要です）。
   * 操作の結果を格納する`OutputResult`オブジェクト。 （このパラメーター値は、Webサービスの呼び出しのみに必要です）。

   >[!NOTE]
   >
   >`OutputClient`オブジェクトの`generatePDFOutput`2メソッドを呼び出して、PDF /Aドキュメントを作成することもできます。 ([Content Services（非推奨）にあるドキュメントをOutputサービスに渡す](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)を参照)。

1. 操作の結果を取得します。

   * コンストラクターを呼び出し、結果データを含むXMLファイルの場所を表す文字列値を渡すことで、`System.IO.FileStream`オブジェクトを作成します。 ファイル名の拡張子が.xmlであることを確認します。
   * `OutputServiceService`オブジェクトの`generatePDFOutput`メソッド（8番目のパラメーター）によって結果データが入力された`BLOB`オブジェクトのデータコンテンツを格納するバイト配列を作成します。 `BLOB`オブジェクトの`MTOM`フィールドの値を取得して、バイト配列を設定します。
   * コンストラクターを呼び出し、`System.IO.FileStream`オブジェクトを渡して、`System.IO.BinaryWriter`オブジェクトを作成します。
   * `System.IO.BinaryWriter`オブジェクトの`Write`メソッドを呼び出し、バイト配列を渡すことにより、バイト配列の内容をXMLファイルに書き込みます。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Content Services（非推奨）にあるドキュメントをOutputサービスに渡す{#passing-documents-located-in-content-services-deprecated-to-the-output-service}

Outputサービスは、通常はXDPファイルとして保存され、Designerで作成されたフォームデザインに基づく非インタラクティブPDFフォームをレンダリングします。 フォームデザインを含む`com.adobe.idp.Document`オブジェクトをOutputサービスに渡すことができます。 次に、Outputサービスは、`com.adobe.idp.Document`オブジェクト内のフォームデザインをレンダリングします。

`com.adobe.idp.Document`オブジェクトをOutputサービスに渡す利点の1つは、他のAEM Formsサービス操作が`com.adobe.idp.Document`インスタンスを返すことです。 つまり、別のサービス操作から`com.adobe.idp.Document`インスタンスを取得してレンダリングできます。 例えば、次の図に示すように、XDPファイルが`/Company Home/Form Designs`という名前のContent Services（非推奨）ノードに格納されているとします。

プログラムによってContent Services（非推奨）からLoan.xdpを取得し、`com.adobe.idp.Document`オブジェクト内でXDPファイルをOutputサービスに渡すことができます。

>[!NOTE]
>
>Formsサービスについて詳しくは、『 AEM Formsのサービスリファレンス[ 』を参照してください。](https://www.adobe.com/go/learn_aemforms_services_63)

### 手順の概要{#summary_of_steps-2}

Content Services（非推奨）から取得したドキュメントをOutputサービスに渡すには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. OutputとDocument Management Client APIオブジェクトを作成します。
1. Content Services（非推奨）からフォームデザインを取得します。
1. 非インタラクティブPDFフォームをレンダリングします。
1. データストリームを使用してアクションを実行します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを含めます。

**出力とドキュメント管理クライアントAPIオブジェクトの作成**

プログラムでOutputサービスAPI操作を実行する前に、OutputクライアントAPIオブジェクトを作成します。 また、このワークフローはContent Services（非推奨）からXDPファイルを取得するので、Document Management APIオブジェクトを作成します。

**Content Services（非推奨）からフォームデザインを取得する**

JavaまたはWebサービスAPIを使用して、Content Services（非推奨）からXDPファイルを取得します。 XDPファイルは、`com.adobe.idp.Document`インスタンス（Webサービスを使用している場合は`BLOB`インスタンス）内で返されます。 その後、`com.adobe.idp.Document`インスタンスをOutputサービスに渡すことができます。

**非インタラクティブPDFフォームのレンダリング**

非インタラクティブフォームをレンダリングするには、Content Services（非推奨）から返された`com.adobe.idp.Document`インスタンスをOutputサービスに渡します。

>[!NOTE]
>
>`generatePDFOutput2`およびg `eneratePrintedOutput2`という2つの新しいメソッドは、フォームデザインを含む`com.adobe.idp.Document`オブジェクトを受け取ります。 また、印刷ストリームをネットワークプリンターに送信する際に、フォームデザインを含む`com.adobe.idp.Document`をOutputサービスに渡すこともできます。

**フォームデータストリームを使用してアクションを実行する**

非インタラクティブフォームをPDFファイルとして保存できます。 フォームは、Adobe ReaderまたはAcrobatで表示できます。

**関連トピック**

[Java APIを使用してドキュメントをOutputサービスに渡す](creating-document-output-streams.md#pass-documents-to-the-output-service-using-the-java-api)

[WebサービスAPIを使用してドキュメントをOutputサービスに渡す](creating-document-output-streams.md#pass-documents-to-the-output-service-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[OutputサービスAPIのクイックスタート](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

[フラグメントを使用したPDFドキュメントの作成](creating-document-output-streams.md#creating-pdf-documents-using-fragments)

### Java API {#pass-documents-to-the-output-service-using-the-java-api}を使用してドキュメントをOutputサービスに渡す

OutputサービスおよびContent Services（非推奨）API(Java)を使用してContent Services（非推奨）から取得したドキュメントを渡します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-output-client.jarやadobe-contentservices-client.jarなどのクライアントJARファイルを含めます。

1. OutputとDocument Management Client APIオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。（[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照。）
   * コンストラクターを使用して`OutputClient`オブジェクトを渡し、`ServiceClientFactory`オブジェクトを作成します。
   * コンストラクタを使用して `DocumentManagementServiceClientImpl` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. Content Services（非推奨）からフォームデザインを取得します。

   `DocumentManagementServiceClientImpl`オブジェクトの`retrieveContent`メソッドを呼び出し、次の値を渡します。

   * コンテンツが追加されるストアを指定するstring値。 デフォルトのストアは`SpacesStore`です。 この値は必須のパラメーターです。
   * 取得するコンテンツの完全修飾パスを指定するstring値（例：`/Company Home/Form Designs/Loan.xdp`）。 この値は必須のパラメーターです。
   * バージョンを指定するstring値。 この値はオプションのパラメーターで、空の文字列を渡すことができます。 この場合、最新バージョンが取得されます。

   `retrieveContent`メソッドは、XDPファイルを含む`CRCResult`オブジェクトを返します。 `CRCResult`オブジェクトの`getDocument`メソッドを呼び出して、`com.adobe.idp.Document`インスタンスを取得します。

1. 非インタラクティブPDFフォームをレンダリングします。

   `OutputClient`オブジェクトの`generatePDFOutput2`メソッドを呼び出し、次の値を渡します。

   * `TransformationFormat`列挙値。 PDFドキュメントを生成するには、`TransformationFormat.PDF`を指定します。
   * 画像などの追加リソースが配置されるコンテンツルートを指定するstring値。
   * フォームデザインを表す`com.adobe.idp.Document`オブジェクト（`CRCResult`オブジェクトの`getDocument`メソッドから返されるインスタンスを使用）。
   * PDFランタイムオプションを含む`PDFOutputOptionsSpec`オブジェクト。
   * レンダリングの実行時オプションを含む`RenderOptionsSpec`オブジェクト。
   * フォームデザインとマージするデータを含むXMLデータソースを含む`com.adobe.idp.Document`オブジェクト。

   `generatePDFOutput2`メソッドは、操作の結果を含む`OutputResult`オブジェクトを返します。

1. フォームデータストリームを使用してアクションを実行します。

   * `OutputResult`オブジェクトの`getGeneratedDoc`メソッドを呼び出して、非インタラクティブフォームを表す`com.adobe.idp.Document`オブジェクトを取得します。
   * 操作の結果を格納する`java.io.File`オブジェクトを作成します。 ファイル名の拡張子が.pdfであることを確認します。
   * `com.adobe.idp.Document`オブジェクトの`copyToFile`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトの内容をファイルにコピーします（`getGeneratedDoc`メソッドで返された`com.adobe.idp.Document`オブジェクトを使用するようにしてください）。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[クイックスタート（EJBモード）:Java APIを使用してOutputサービスにドキュメントを渡す](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[クイックスタート（SOAPモード）:Java APIを使用してOutputサービスにドキュメントを渡す](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#pass-documents-to-the-output-service-using-the-web-service-api}を使用してドキュメントをOutputサービスに渡す

OutputサービスおよびContent Services（非推奨）API（Webサービス）を使用してContent Services（非推奨）から取得したドキュメントを渡します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 このクライアントアプリケーションは2つのAEM Formsサービスを呼び出すので、2つのサービス参照を作成します。 Outputサービスに関連付けられたサービス参照に、次のWSDL定義を使用します。`http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   Document Managementサービスに関連付けられたサービス参照に、次のWSDL定義を使用します。`http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`.

   `BLOB`データ型は両方のサービス参照に共通なので、`BLOB`データ型を使用する際には完全に修飾します。 対応するWebサービスのクイックスタートでは、すべての`BLOB`インスタンスが完全に認定されます。

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. OutputとDocument Management Client APIオブジェクトを作成します。

   * デフォルトのコンストラクターを使用して`OutputServiceClient`オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`OutputServiceClient.Endpoint.Address`オブジェクトを作成します。 FormsサービスにWSDLを指定するstring値を渡します（例：`http://localhost:8080/soap/services/OutputService?blob=mtom`）。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する際に使用されます)。
   * `OutputServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値は、MTOMが使用されるようにします。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールド`OutputServiceClient.ClientCredentials.UserName.UserName`にAEM formsユーザー名を割り当てます。
      * 対応するパスワード値をフィールド`OutputServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * フィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に定数値`HttpClientCredentialType.Basic`を割り当てます。
   * フィールド`BasicHttpBindingSecurity.Security.Mode`に定数値`BasicHttpSecurityMode.TransportCredentialOnly`を割り当てます。

   >[!NOTE]
   >
   >`DocumentManagementServiceClient`サービスクライアントに対して、この手順を繰り返します。

1. Content Services（非推奨）からフォームデザインを取得します。

   `DocumentManagementServiceClient`オブジェクトの`retrieveContent`メソッドを呼び出し、次の値を渡して、コンテンツを取得します。

   * コンテンツが追加されるストアを指定するstring値。 デフォルトのストアは`SpacesStore`です。 この値は必須のパラメーターです。
   * 取得するコンテンツの完全修飾パスを指定するstring値（例：`/Company Home/Form Designs/Loan.xdp`）。 この値は必須のパラメーターです。
   * バージョンを指定するstring値。 この値はオプションのパラメーターで、空の文字列を渡すことができます。 この場合、最新バージョンが取得されます。
   * 参照リンクの値を格納する文字列出力パラメーター。
   * コンテンツを格納する`BLOB`出力パラメーター。 この出力パラメーターを使用して、コンテンツを取得できます。
   * コンテンツ属性を格納する`ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType`出力パラメーター。
   * `CRCResult`出力パラメータ。 このオブジェクトを使用する代わりに、 `BLOB`出力パラメーターを使用してコンテンツを取得できます。

1. 非インタラクティブPDFフォームをレンダリングします。

   `OutputServiceClient`オブジェクトの`generatePDFOutput2`メソッドを呼び出し、次の値を渡します。

   * `TransformationFormat`列挙値。 PDFドキュメントを生成するには、`TransformationFormat.PDF`を指定します。
   * 画像などの追加リソースが配置されるコンテンツルートを指定するstring値。
   * フォームデザインを表す`BLOB`オブジェクト(Content Services（非推奨）から返される`BLOB`インスタンスを使用)。
   * PDFランタイムオプションを含む`PDFOutputOptionsSpec`オブジェクト。
   * レンダリングの実行時オプションを含む`RenderOptionsSpec`オブジェクト。
   * フォームデザインとマージするデータを含むXMLデータソースを含む`BLOB`オブジェクト。
   * `generatePDFOutput2`メソッドによって設定される出力`BLOB`オブジェクト。 `generatePDFOutput2`メソッドは、このオブジェクトに、ドキュメントを表す生成済みのメタデータを入力します。 （このパラメーター値は、Webサービスの呼び出しにのみ必要です）。
   * 操作の結果を含む出力`OutputResult`オブジェクト。 （このパラメーター値は、Webサービスの呼び出しにのみ必要です）。

   `generatePDFOutput2`メソッドは、非インタラクティブPDFフォームを含む`BLOB`オブジェクトを返します。

1. フォームデータストリームを使用してアクションを実行します。

   * コンストラクターを呼び出して、`System.IO.FileStream`オブジェクトを作成します。 インタラクティブPDFドキュメントのファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * `generatePDFOutput2`メソッドから取得した`BLOB`オブジェクトの内容を格納するバイト配列を作成します。 `BLOB`オブジェクトの`MTOM`データメンバーの値を取得して、バイト配列を設定します。
   * コンストラクターを呼び出し、`System.IO.FileStream`オブジェクトを渡して、`System.IO.BinaryWriter`オブジェクトを作成します。
   * `System.IO.BinaryWriter`オブジェクトの`Write`メソッドを呼び出し、バイト配列を渡すことにより、バイト配列の内容をPDFファイルに書き込みます。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## リポジトリ内のドキュメントをOutputサービスに渡す{#passing-documents-located-in-the-repository-to-the-output-service}

Outputサービスは、通常はXDPファイルとして保存され、Designerで作成されたフォームデザインに基づく非インタラクティブPDFフォームをレンダリングします。 フォームデザインを含む`com.adobe.idp.Document`オブジェクトをOutputサービスに渡すことができます。 次に、Outputサービスは、`com.adobe.idp.Document`オブジェクト内のフォームデザインをレンダリングします。

`com.adobe.idp.Document`オブジェクトをOutputサービスに渡す利点の1つは、他のAEM Formsサービス操作が`com.adobe.idp.Document`インスタンスを返すことです。 つまり、別のサービス操作から`com.adobe.idp.Document`インスタンスを取得してレンダリングできます。 例えば、次の図に示すように、XDPファイルがAEM Formsリポジトリに格納されているとします。

![pd_pd_formrepository](assets/pd_pd_formrepository.png)

*FormsFolder*&#x200B;フォルダーは、AEM Formsリポジトリ内のユーザー定義の場所です（この場所は例で、デフォルトでは存在しません）。 この例では、Loan.xdpという名前のフォームデザインがこのフォルダーに配置されています。 この場所には、フォームデザインに加えて、画像などの他のフォームの販促物を格納できます。 AEM Formsリポジトリ内のリソースへのパスは次のとおりです。

`Applications/Application-name/Application-version/Folder.../Filename`

プログラムによってAEM FormsリポジトリからLoan.xdpを取得し、`com.adobe.idp.Document`オブジェクト内でOutputサービスに渡すことができます。

リポジトリ内のXDPファイルをベースにしたPDFを作成するには、次の2つの方法のいずれかを使用します。 XDPの場所は、参照によって渡すことも、XDPをプログラムでリポジトリから取得し、XDPファイル内でOutputサービスに渡すこともできます。

[クイックスタート（EJBモード）:Java APIを使用したアプリケーションXDPファイルに基づくPDFドキュメントの作成](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api) （参照でXDPファイルの場所を渡す方法を示します）。

[クイックスタート（EJBモード）:Java APIを使用してAEM Formsリポジトリ内のドキュメントをOutputサービスに渡す方法](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api) (プログラムによってAEM FormsリポジトリからXDPファイルを取得し、インスタンス内でOutputサービスに渡す方法を示し `com.adobe.idp.Document` ます)。（この節では、このタスクの実行方法について説明します）。

>[!NOTE]
>
>Formsサービスについて詳しくは、『 AEM Formsのサービスリファレンス[ 』を参照してください。](https://www.adobe.com/go/learn_aemforms_services_63)

### 手順の概要{#summary_of_steps-3}

AEM Formsリポジトリから取得したドキュメントをOutputサービスに渡すには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. OutputとDocument Management Client APIオブジェクトを作成します。
1. AEM Formsリポジトリからフォームデザインを取得します。
1. 非インタラクティブPDFフォームをレンダリングします。
1. データストリームを使用してアクションを実行します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを含めます。

**出力とドキュメント管理クライアントAPIオブジェクトの作成**

プログラムでOutputサービスAPI操作を実行する前に、OutputクライアントAPIオブジェクトを作成します。 また、このワークフローはContent Services（非推奨）からXDPファイルを取得するので、Document Management APIオブジェクトを作成します。

**AEM Formsリポジトリからフォームデザインを取得する**

Repository APIを使用して、AEM FormsリポジトリからXDPファイルを取得します。 （[リソースの読み取り](/help/forms/developing/aem-forms-repository.md#reading-resources)を参照）。

XDPファイルは、`com.adobe.idp.Document`インスタンス（Webサービスを使用している場合は`BLOB`インスタンス）内で返されます。 その後、`com.adobe.idp.Document`インスタンスをOutputサービスに渡すことができます。

**非インタラクティブPDFフォームのレンダリング**

非インタラクティブフォームをレンダリングするには、AEM FormsリポジトリAPIを使用して返された`com.adobe.idp.Document`インスタンスを渡します。

>[!NOTE]
>
>`generatePDFOutput2`および`generatePrintedOutput2`という2つの新しいメソッドは、フォームデザインを含む`com.adobe.idp.Document`オブジェクトを受け取ります。 また、印刷ストリームをネットワークプリンターに送信する際に、フォームデザインを含む`com.adobe.idp.Document`をOutputサービスに渡すこともできます。

**フォームデータストリームを使用してアクションを実行する**

非インタラクティブフォームをPDFファイルとして保存できます。 フォームは、Adobe ReaderまたはAcrobatで表示できます。

**関連トピック**

[Java APIを使用して、リポジトリ内のドキュメントをOutputサービスに渡す](creating-document-output-streams.md#pass-documents-located-in-the-repository-to-the-output-service-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[OutputサービスAPIのクイックスタート](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

ResourceRepositoryClient

### Java API {#pass-documents-located-in-the-repository-to-the-output-service-using-the-java-api}を使用して、リポジトリ内のドキュメントをOutputサービスに渡します。

OutputサービスとリポジトリAPI(Java)を使用してリポジトリから取得したドキュメントを渡します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-output-client.jarやadobe-repository-client.jarなどのクライアントJARファイルを含めます。

1. OutputとDocument Management Client APIオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。（[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照。）
   * コンストラクターを使用して`OutputClient`オブジェクトを渡し、`ServiceClientFactory`オブジェクトを作成します。
   * コンストラクタを使用して `DocumentManagementServiceClientImpl` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. AEM Formsリポジトリからフォームデザインを取得します。

   `ResourceRepositoryClient`オブジェクトの`readResourceContent`メソッドを呼び出し、URIの場所を指定する文字列値をXDPファイルに渡します。 例えば、`/Applications/FormsApplication/1.0/FormsFolder/Loan.xdp` のようになります。この値は必須です。 このメソッドは、XDPファイルを表す`com.adobe.idp.Document`インスタンスを返します。

1. 非インタラクティブPDFフォームをレンダリングします。

   `OutputClient`オブジェクトの`generatePDFOutput2`メソッドを呼び出し、次の値を渡します。

   * `TransformationFormat`列挙値。 PDFドキュメントを生成するには、`TransformationFormat.PDF`を指定します。
   * 画像などの追加リソースが配置されるコンテンツルートを指定するstring値。 （例：`repository:///Applications/FormsApplication/1.0/FormsFolder/`）。
   * フォームデザインを表す`com.adobe.idp.Document`オブジェクト（`ResourceRepositoryClient`オブジェクトの`readResourceContent`メソッドから返されるインスタンスを使用）。
   * PDFランタイムオプションを含む`PDFOutputOptionsSpec`オブジェクト。
   * レンダリングの実行時オプションを含む`RenderOptionsSpec`オブジェクト。
   * フォームデザインとマージするデータを含むXMLデータソースを含む`com.adobe.idp.Document`オブジェクト。

   `generatePDFOutput2`メソッドは、操作の結果を含む`OutputResult`オブジェクトを返します。

1. フォームデータストリームを使用してアクションを実行します。

   * `OutputResult`オブジェクトの`getGeneratedDoc`メソッドを呼び出して、非インタラクティブフォームを表す`com.adobe.idp.Document`オブジェクトを取得します。
   * 操作の結果を格納する`java.io.File`オブジェクトを作成します。 ファイル名の拡張子が.pdfであることを確認します。
   * `com.adobe.idp.Document`オブジェクトの`copyToFile`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトの内容をファイルにコピーします（`getGeneratedDoc`メソッドで返された`com.adobe.idp.Document`オブジェクトを使用するようにしてください）。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[クイックスタート（EJBモード）:Java APIを使用してAEM Formsリポジトリ内のドキュメントをOutputサービスに渡す](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## フラグメント{#creating-pdf-documents-using-fragments}を使用したPDFドキュメントの作成

OutputサービスとAssemblerサービスを使用して、フラグメントに基づく出力ストリーム（PDFドキュメントなど）を作成できます。 Assemblerサービスは、複数のXDPファイル内のフラグメントに基づくXDPドキュメントをアセンブリします。 アセンブリされたXDPドキュメントがOutputサービスに渡され、PDFドキュメントが作成されます。 このワークフローでは、生成中のPDFドキュメントが表示されますが、Outputサービスでは、このワークフローに対してZPLなどの他の出力タイプを生成できます。 PDFドキュメントは、ディスカッションの目的でのみ使用します。

次の図に、このワークフローを示します。

![cp_cp_outputassemblefragments](assets/cp_cp_outputassemblefragments.png)

*Fragments*&#x200B;を使用したPDFドキュメントの作成を読む前に、Assemblerサービスを使用して複数のXDPドキュメントをアセンブリする方法を理解しておくことをお勧めします。 （[複数のXDPフラグメントのアセンブリ](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments)を参照）。

>[!NOTE]
>
>また、Assemblerサービスによってアセンブルされたフォームデザインを、Outputサービスの代わりにFormsサービスに渡すこともできます。 OutputサービスとFormsサービスの主な違いは、FormsサービスでインタラクティブPDFドキュメントが生成され、Outputサービスで非インタラクティブPDFドキュメントが生成される点です。 また、Formsサービスは、ZPLなどのプリンターベースの出力ストリームを生成できません。

>[!NOTE]
>
>Outputサービスについて詳しくは、『AEM Formsのサービスリファレンス[』を参照してください。](https://www.adobe.com/go/learn_aemforms_services_63)

### 手順の概要{#summary_of_steps-4}

フラグメントに基づいてPDFドキュメントを作成するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. OutputおよびAssembler Clientオブジェクトを作成します。
1. フォームデザインを生成するには、Assemblerサービスを使用します。
1. Outputサービスを使用してPDFドキュメントを生成します。
1. PDFドキュメントをPDFファイルとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用する場合は、必ずプロキシファイルを含めてください。

**出力およびアセンブラクライアントオブジェクトの作成**

プログラムでOutputサービスAPI操作を実行する前に、OutputクライアントAPIオブジェクトを作成します。 また、このワークフローはAssemblerサービスを呼び出してフォームデザインを作成するので、AssemblerクライアントAPIオブジェクトを作成します。

**フォームデザインの生成にAssemblerサービスを使用する**

Assemblerサービスを使用して、フラグメントを使用してフォームデザインを生成します。 Assemblerサービスは、フォームデザインを含む`com.adobe.idp.Document`インスタンスを返します。

**Outputサービスを使用してPDFドキュメントを生成する**

Outputサービスを使用して、Assemblerサービスが作成したフォームデザインを使用してPDFドキュメントを生成できます。 Assemblerサービスが返した`com.adobe.idp.Document`インスタンスをOutputサービスに渡します。

**PDFドキュメントをPDFファイルとして保存**

OutputサービスでPDFドキュメントが生成されたら、PDFファイルとして保存できます。

**関連トピック**

[Java APIを使用して、フラグメントに基づくPDFドキュメントを作成する](creating-document-output-streams.md#create-a-pdf-document-based-on-fragments-using-the-java-api)

[WebサービスAPIを使用して、フラグメントに基づくPDFドキュメントを作成する](creating-document-output-streams.md#create-a-pdf-document-based-on-fragments-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[OutputサービスAPIのクイックスタート](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

[複数のXDPフラグメントのアセンブリ](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments)

[PDFドキュメントの作成](creating-document-output-streams.md#creating-pdf-documents)

### Java API {#create-a-pdf-document-based-on-fragments-using-the-java-api}を使用して、フラグメントに基づいたPDFドキュメントを作成します

OutputサービスAPIとAssemblerサービスAPI(Java)を使用して、フラグメントに基づいたPDFドキュメントを作成します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-output-client.jarなどのクライアントJARファイルを含めます。

1. OutputおよびAssembler Clientオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して`OutputClient`オブジェクトを渡し、`ServiceClientFactory`オブジェクトを作成します。
   * コンストラクターを使用して`AssemblerServiceClient`オブジェクトを渡し、`ServiceClientFactory`オブジェクトを作成します。

1. フォームデザインを生成するには、Assemblerサービスを使用します。

   `AssemblerServiceClient`オブジェクトの`invokeDDX`メソッドを呼び出し、次の必須値を渡します。

   * 使用するDDXドキュメントを表す`com.adobe.idp.Document`オブジェクト。
   * 入力XDPファイルを格納する`java.util.Map`オブジェクト。
   * デフォルトのフォントやジョブのログレベルなど、実行時のオプションを指定する`com.adobe.livecycle.assembler.client.AssemblerOptionSpec`オブジェクト。

   `invokeDDX`メソッドは、アセンブリされたXDPドキュメントを含む`com.adobe.livecycle.assembler.client.AssemblerResult`オブジェクトを返します。 アセンブリ済みのXDPドキュメントを取得するには、次の操作を実行します。

   * `AssemblerResult`オブジェクトの`getDocuments`メソッドを呼び出します。 このメソッドは`java.util.Map`オブジェクトを返します。
   * `java.util.Map`オブジェクトを繰り返し処理して、結果の`com.adobe.idp.Document`オブジェクトを見つけます。
   * `com.adobe.idp.Document`オブジェクトの`copyToFile`メソッドを呼び出して、アセンブリされたXDPドキュメントを抽出します。


1. Outputサービスを使用してPDFドキュメントを生成します。

   `OutputClient`オブジェクトの`generatePDFOutput2`メソッドを呼び出し、次の値を渡します。

   * `TransformationFormat`列挙値。 PDFドキュメントを生成するには、`TransformationFormat.PDF`を指定します。
   * 画像などの追加リソースが存在するコンテンツルートを指定するstring値
   * フォームデザインを表す`com.adobe.idp.Document`オブジェクト（Assemblerサービスから返されたインスタンスを使用）
   * PDFランタイムオプションを含む`PDFOutputOptionsSpec`オブジェクト
   * レンダリング実行時オプションを含む`RenderOptionsSpec`オブジェクト
   * フォームデザインとマージするデータが含まれるXMLデータソースを含む`com.adobe.idp.Document`オブジェクト

   `generatePDFOutput2`メソッドは、操作の結果を含む`OutputResult`オブジェクトを返します

1. PDFドキュメントをPDFファイルとして保存します。

   * `OutputResult`オブジェクトの`getGeneratedDoc`メソッドを呼び出して、PDFドキュメントを表す`com.adobe.idp.Document`オブジェクトを取得します。
   * 操作の結果を格納する`java.io.File`オブジェクトを作成します。 ファイル名の拡張子が.pdfであることを確認します。
   * `com.adobe.idp.Document`オブジェクトの`copyToFile`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトの内容をファイルにコピーします。 （`getGeneratedDoc`メソッドが返す`com.adobe.idp.Document`オブジェクトを使用してください）。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[クイックスタート（EJBモード）:Java APIを使用したフラグメントに基づくPDFドキュメントの作成](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[クイックスタート（SOAPモード）:Java APIを使用したフラグメントに基づくPDFドキュメントの作成](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

### WebサービスAPI {#create-a-pdf-document-based-on-fragments-using-the-web-service-api}を使用して、フラグメントに基づいてPDFドキュメントを作成します

OutputサービスAPIとAssemblerサービスAPI（Webサービス）を使用して、フラグメントに基づいたPDFドキュメントを作成します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 Outputサービスに関連付けられたサービス参照に、次のWSDL定義を使用します。

   ```java
    http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1.
   ```

   Assemblerサービスに関連付けられたサービス参照には、次のWSDL定義を使用します。

   ```java
    http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   `BLOB`データ型は両方のサービス参照に共通なので、`BLOB`データ型を使用する際には完全に修飾します。 対応するWebサービスのクイックスタートでは、すべての`BLOB`インスタンスが完全に認定されます。

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. OutputおよびAssembler Clientオブジェクトを作成します。

   * デフォルトのコンストラクターを使用して`OutputServiceClient`オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`OutputServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに渡す文字列値（例：`http://localhost:8080/soap/services/OutputService?blob=mtom`）を渡します。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する際に使用されます。 ただし、MTOMを使用する場合は`?blob=mtom`を指定します。
   * `OutputServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値は、MTOMが使用されるようにします。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * `OutputServiceClient.ClientCredentials.UserName.UserName`フィールドにAEM formsユーザー名を割り当てます。
      * 対応するパスワード値を`OutputServiceClient.ClientCredentials.UserName.Password`フィールドに割り当てます。
      * 定数値`HttpClientCredentialType.Basic`を`BasicHttpBindingSecurity.Transport.ClientCredentialType`フィールドに割り当てます。
   * `BasicHttpSecurityMode.TransportCredentialOnly`定数値を`BasicHttpBindingSecurity.Security.Mode`フィールドに割り当てます。

   >[!NOTE]
   >
   >`AssemblerServiceClient`オブジェクトに対して、次の手順を繰り返します。

1. フォームデザインを生成するには、Assemblerサービスを使用します。

   `AssemblerServiceClient`オブジェクトの`invokeDDX`メソッドを呼び出し、次の値を渡します。

   * DDXドキュメントを表す`BLOB`オブジェクト
   * 必要なファイルを含む`MyMapOf_xsd_string_To_xsd_anyType`オブジェクト
   * 実行時オプションを指定する`AssemblerOptionSpec`オブジェクト

   `invokeDDX`メソッドは、ジョブの結果と発生した例外を含む`AssemblerResult`オブジェクトを返します。 新しく作成したXDPドキュメントを取得するには、次の操作を実行します。

   * `AssemblerResult`オブジェクトの`documents`フィールド（結果のPDFドキュメントを含む`Map`オブジェクト）にアクセスします。
   * `Map`オブジェクトを繰り返し処理して、アセンブリされたフォームデザインを取得します。 配列メンバの`value`を`BLOB`にキャストします。 この`BLOB`インスタンスをOutputサービスに渡します。


1. Outputサービスを使用してPDFドキュメントを生成します。

   `OutputServiceClient`オブジェクトの`generatePDFOutput2`メソッドを呼び出し、次の値を渡します。

   * `TransformationFormat`列挙値。 PDFドキュメントを生成するには、`TransformationFormat.PDF`を指定します。
   * 画像などの追加リソースが存在するコンテンツルートを指定するstring値。
   * フォームデザインを表す`BLOB`オブジェクト（Assemblerサービスから返される`BLOB`インスタンスを使用）。
   * PDFランタイムオプションを含む`PDFOutputOptionsSpec`オブジェクト。
   * レンダリングの実行時オプションを含む`RenderOptionsSpec`オブジェクト。
   * フォームデザインとマージするデータを含むXMLデータソースを含む`BLOB`オブジェクト。
   * `generatePDFOutput2`メソッドが設定する出力`BLOB`オブジェクト。 `generatePDFOutput2`メソッドは、このオブジェクトに、ドキュメントを表す生成済みのメタデータを入力します。 （このパラメーター値は、Webサービスの呼び出しにのみ必要です）。
   * 操作の結果を含む出力`OutputResult`オブジェクト。 （このパラメーター値は、Webサービスの呼び出しにのみ必要です）。

   `generatePDFOutput2`メソッドは、非インタラクティブPDFフォームを含む`BLOB`オブジェクトを返します。

1. PDFドキュメントをPDFファイルとして保存します。

   * コンストラクターを呼び出して、`System.IO.FileStream`オブジェクトを作成します。 インタラクティブPDFドキュメントのファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * `generatePDFOutput2`メソッドから取得した`BLOB`オブジェクトの内容を格納するバイト配列を作成します。 `BLOB`オブジェクトの`MTOM`データメンバーの値を取得して、バイト配列を設定します。
   * コンストラクターを呼び出し、`System.IO.FileStream`オブジェクトを渡して、`System.IO.BinaryWriter`オブジェクトを作成します。
   * `System.IO.BinaryWriter`オブジェクトの`Write`メソッドを呼び出し、バイト配列を渡すことにより、バイト配列の内容をPDFファイルに書き込みます。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## ファイル{#printing-to-files}への印刷

Outputサービスを使用して、PostScript、Printer Control Language(PCL)、または次のラベル形式などのストリームをファイルに印刷できます。

* ゼブラ — ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

Outputサービスを使用すると、XMLデータをフォームデザインとマージし、フォームをファイルに印刷できます。 次の図に、Outputサービスでのレーザーファイルとラベルファイルの作成を示します。

>[!NOTE]
>
>プリントストリームをプリンターに送信する方法については、[Sending Print Streams to Printers](creating-document-output-streams.md#sending-print-streams-to-printers)を参照してください。

>[!NOTE]
>
>Outputサービスについて詳しくは、『AEM Formsのサービスリファレンス[』を参照してください。](https://www.adobe.com/go/learn_aemforms_services_63)

### 手順の概要{#summary_of_steps-5}

ファイルに印刷するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Outputクライアントオブジェクトを作成します。
1. XMLデータソースを参照します。
1. ファイルに印刷するために必要な印刷実行時オプションを設定します。
1. 印刷ストリームをファイルに印刷します。
1. 操作の結果を取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用する場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(AEM FormsをJBossにデプロイする場合に必要)
* jbossall-client.jar(AEM FormsをJBossにデプロイする場合に必要)

AEM FormsがJBoss以外のサポート対象のJ2EEアプリケーションサーバーにデプロイされている場合は、adobe-utilities.jarファイルとjbossall-client.jarファイルを、AEM FormsがデプロイされているJ2EEアプリケーションサーバーに固有のJARファイルに置き換える必要があります。 （[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照。）

**Outputクライアントオブジェクトの作成**

プログラムによってOutputサービス操作を実行する前に、Outputサービスクライアントオブジェクトを作成する必要があります。 Java APIを使用している場合は、`OutputClient`オブジェクトを作成します。 Output WebサービスAPIを使用している場合は、`OutputServiceService`オブジェクトを作成します。

**XMLデータソースの参照**

データを含むドキュメントを印刷するには、データを入力するすべてのフォームフィールドに対して、XML要素を含むXMLデータソースを参照する必要があります。 XML要素名は、フィールド名と一致する必要があります。 XML要素がフォームフィールドに対応していない場合や、XML要素名がフィールド名と一致しない場合は無視されます。 すべてのXML要素を指定した場合、XML要素の表示順序を一致させる必要はありません。

**ファイルへの印刷に必要な印刷実行時オプションの設定**

ファイルに印刷するには、Outputサービスが印刷するファイルの場所と名前を指定して、「ファイルURIランタイム」オプションを設定する必要があります。 例えば、Outputサービスに&#x200B;*MortgageForm.ps*&#x200B;という名前のPostScriptファイルをC:\Adobeに印刷するように指示するには、C:\Adobe\MortgageForm.psと指定します。

>[!NOTE]
>
>オプションで定義できる実行時オプションがあります。 設定できるすべてのオプションについて詳しくは、「 [AEM Forms APIリファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en) 」の`PrintedOutputOptionsSpec`クラス参照を参照してください。

**印刷ストリームをファイルに印刷する**

フォームデータを含む有効なXMLデータソースを参照し、印刷実行時オプションを設定した後、Outputサービスを呼び出すと、ファイルが印刷されます。

**操作の結果の取得**

Outputサービスが操作を実行すると、XMLデータなど、操作が成功したかどうかを示す様々なデータ項目が返されます。

**関連トピック**

[Java APIを使用してファイルに出力](creating-document-output-streams.md#print-to-files-using-the-java-api)

[WebサービスAPIを使用してファイルに出力](creating-document-output-streams.md#print-to-files-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[OutputサービスAPIのクイックスタート](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Java API {#print-to-files-using-the-java-api}を使用してファイルに出力します

出力API(Java)を使用してファイルに出力：

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-output-client.jarなどのクライアントJARファイルを含めます。

1. Outputクライアントオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して`OutputClient`オブジェクトを渡し、`ServiceClientFactory`オブジェクトを作成します。

1. XMLデータソースを参照します。

   * コンストラクタを使用し、XMLファイルの場所を指定する文字列値を渡すことで、ドキュメントの入力に使用されるXMLデータソースを表す`java.io.FileInputStream`オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. ファイルに印刷するために必要な印刷実行時オプションを設定します。

   * コンストラクタを使用して `PrintedOutputOptionsSpec` オブジェクトを作成します。
   * PrintedOutputOptionsSpecオブジェクトの`setFileURI`メソッドを呼び出し、ファイルの名前と場所を表す文字列値を渡すことによって、ファイルを指定します。 例えば、C:\AdobeにあるMortgageForm.psという名前のPostScriptファイルにOutputサービスを印刷する場合は、C:\\Adobe\MortgageForm.psと指定します。
   * `PrintedOutputOptionsSpec`オブジェクトの`setCopies`メソッドを呼び出し、印刷部数を表す整数値を渡して、印刷部数を指定します。

1. 印刷ストリームをファイルに印刷します。

   `OutputClient`オブジェクトの`generatePrintedOutput`メソッドを呼び出し、次の値を渡して、ファイルに出力します。

   * 作成する印刷ストリーム形式を指定する`PrintFormat`列挙値。 例えば、PostScript印刷ストリームを作成するには、`PrintFormat.PostScript`を渡します。
   * フォームデザイン名を指定する string 値。
   * 画像ファイルなど、関連する販促物ファイルの場所を指定するstring値。
   * 使用するXDCファイルの場所を指定するstring値（`PrintedOutputOptionsSpec`オブジェクトを使用して使用するXDCファイルを指定した場合、`null`を渡すことができます）。
   * ファイルに印刷するために必要な実行時オプションを含む`PrintedOutputOptionsSpec`オブジェクト。
   * フォームデータを含むXMLデータソースを含む`com.adobe.idp.Document`オブジェクト。

   `generatePrintedOutput`メソッドは、操作の結果を含む`OutputResult`オブジェクトを返します。

   >[!NOTE]
   >
   >`OutputResult`オブジェクトの`getRecordLevelMetaDataList`メソッドは`null`を返します。

1. 操作の結果を取得します。

   * `OutputResult`オブジェクトの`getStatusDoc`メソッド（`generatePrintedOutput`メソッドで返された`OutputResult`オブジェクト）を呼び出して、`generatePrintedOutput`メソッドの状態を表す`com.adobe.idp.Document`オブジェクトを作成します。
   * 操作の結果を格納する`java.io.File`オブジェクトを作成します。 ファイル拡張子がXMLであることを確認します。
   * `com.adobe.idp.Document`オブジェクトの`copyToFile`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトの内容をファイルにコピーします（`getStatusDoc`メソッドで返された`com.adobe.idp.Document`オブジェクトを使用するようにしてください）。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[クイックスタート（SOAPモード）:Java APIを使用したファイルへの印刷](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-printing-to-a-file-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

### WebサービスAPI {#print-to-files-using-the-web-service-api}を使用してファイルに出力します

Output API（Webサービス）を使用してファイルに出力します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. Outputクライアントオブジェクトを作成します。

   * デフォルトのコンストラクターを使用して`OutputServiceClient`オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`OutputServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに渡す文字列値（例：`http://localhost:8080/soap/services/OutputService?blob=mtom`）を渡します。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する際に使用されます。 ただし、MTOMを使用する場合は`?blob=mtom`を指定します。
   * `OutputServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値は、MTOMが使用されるようにします。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールド`OutputServiceClient.ClientCredentials.UserName.UserName`にAEM formsユーザー名を割り当てます。
      * 対応するパスワード値をフィールド`OutputServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * フィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に定数値`HttpClientCredentialType.Basic`を割り当てます。
      * フィールド`BasicHttpBindingSecurity.Security.Mode`に定数値`BasicHttpSecurityMode.TransportCredentialOnly`を割り当てます。

1. XMLデータソースを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、フォームデータの格納に使用されます。
   * コンストラクターを呼び出し、フォームデータを含むXMLファイルの場所を指定する文字列値を渡すことで、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得することで、バイト配列のサイズを判断できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことによって、バイト配列にストリームデータを入力します。
   * `BLOB`オブジェクトの`binaryData`プロパティにバイト配列の内容を割り当てて、オブジェクトを設定します。

1. ファイルに印刷するために必要な印刷実行時オプションを設定します。

   * コンストラクタを使用して `PrintedOutputOptionsSpec` オブジェクトを作成します。
   * ファイルの場所と名前を表すstring値を`PrintedOutputOptionsSpec`オブジェクトの`fileURI`データメンバーに割り当てて、ファイルを指定します。 例えば、C:\AdobeにあるPostScriptファイル&#x200B;*MortgageForm.ps*&#x200B;にOutputサービスを印刷する場合は、C:\\Adobe\MortgageForm.psと指定します。
   * `PrintedOutputOptionsSpec`オブジェクトの`copies`データメンバにコピー数を表す整数値を割り当てて、印刷するコピー数を指定します。

1. 印刷ストリームをファイルに印刷します。

   `OutputServiceService`オブジェクトの`generatePrintedOutput`メソッドを呼び出し、次の値を渡して、ファイルに出力します。

   * 作成する印刷ストリーム形式を指定する`PrintFormat`列挙値。 例えば、PostScript印刷ストリームを作成するには、`PrintFormat.PostScript`を渡します。
   * フォームデザイン名を指定する string 値。
   * 画像ファイルなど、関連する販促物ファイルの場所を指定するstring値。
   * 使用するXDCファイルの場所を指定するstring値（`PrintedOutputOptionsSpec`オブジェクトを使用して使用するXDCファイルを指定した場合、`null`を渡すことができます）。
   * ファイルに印刷するために必要な印刷実行時オプションを含む`PrintedOutputOptionsSpec`オブジェクト。
   * フォームデータを含むXMLデータソースを含む`BLOB`オブジェクト。
   * `generatePDFOutput`メソッドによって設定される`BLOB`オブジェクト。 `generatePDFOutput`メソッドは、このオブジェクトに、ドキュメントを表す生成済みのメタデータを入力します。 （このパラメーター値は、Webサービスの呼び出しのみに必要です）。
   * `generatePDFOutput`メソッドによって設定される`BLOB`オブジェクト。 `generatePDFOutput`メソッドは、このオブジェクトに結果データを入力します。 （このパラメーター値は、Webサービスの呼び出しのみに必要です）。
   * 操作の結果を格納する`OutputResult`オブジェクト。 （このパラメーター値は、Webサービスの呼び出しのみに必要です）。

1. 操作の結果を取得します。

   * コンストラクターを呼び出し、結果データを含むXMLファイルの場所を表す文字列値を渡すことで、`System.IO.FileStream`オブジェクトを作成します。 ファイル拡張子がXMLであることを確認します。
   * `OutputServiceService`オブジェクトの`generatePDFOutput`メソッド（8番目のパラメーター）によって結果データが入力された`BLOB`オブジェクトのデータコンテンツを格納するバイト配列を作成します。 `BLOB`オブジェクトの`MTOM`データメンバーの値を取得して、バイト配列を設定します。
   * コンストラクターを呼び出し、`System.IO.FileStream`オブジェクトを渡して、`System.IO.BinaryWriter`オブジェクトを作成します。
   * `System.IO.BinaryWriter`オブジェクトの`Write`メソッドを呼び出し、バイト配列を渡すことにより、バイト配列の内容をXMLファイルに書き込みます。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## プリンタへの印刷ストリームの送信{#sending-print-streams-to-printers}

Outputサービスを使用して、PostScript、Printer Control Language(PCL)、または次のラベル形式などの印刷ストリームをネットワークプリンターに送信できます。

* ゼブラ — ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

Outputサービスを使用すると、XMLデータをフォームデザインとマージし、フォームを印刷ストリームとして出力できます。 例えば、PostScript印刷ストリームを作成して、ネットワークプリンターに送信できます。 次の図は、印刷ストリームをネットワークプリンターに送信するOutputサービスを示しています。

>[!NOTE]
>
>この節では、印刷ストリームをネットワークプリンタに送信する方法を示すために、SharedPrinterプロトコルを使用してPostScript印刷ストリームをネットワークプリンタに送信します。

>[!NOTE]
>
>Outputサービスについて詳しくは、『AEM Formsのサービスリファレンス[』を参照してください。](https://www.adobe.com/go/learn_aemforms_services_63)

### 手順の概要{#summary_of_steps-6}

印刷ストリームをネットワークプリンタに送信するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. Outputクライアントオブジェクトを作成します。
1. XMLデータソースを参照します。
1. 印刷実行時オプションの設定
1. 印刷するドキュメントを取得します。
1. ドキュメントをネットワークプリンターに送信します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用する場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(AEM FormsがJBossにデプロイされている場合に必須)
* jbossall-client.jar(AEM FormsがJBossにデプロイされている場合に必須)

AEM FormsがJBoss以外のサポート対象のJ2EEアプリケーションサーバーにデプロイされている場合は、adobe-utilities.jarファイルとjbossall-client.jarファイルを、AEM FormsがデプロイされているJ2EEアプリケーションサーバーに固有のJARファイルに置き換える必要があります。

**Outputクライアントオブジェクトの作成**

プログラムによってOutputサービス操作を実行する前に、Outputサービスクライアントオブジェクトを作成します。 Java APIを使用している場合は、`OutputClient`オブジェクトを作成します。 Output WebサービスAPIを使用している場合は、`OutputServiceClient`オブジェクトを作成します。

**XMLデータソースの参照**

データを含むドキュメントを印刷するには、データを入力するすべてのフォームフィールドに対して、XML要素を含むXMLデータソースを参照する必要があります。 XML要素名は、フィールド名と一致する必要があります。 XML要素がフォームフィールドに対応していない場合や、XML要素名がフィールド名と一致しない場合は無視されます。 すべてのXML要素を指定した場合、XML要素の表示順序を一致させる必要はありません。

**印刷実行時オプションの設定**

印刷ストリームをプリンターに送信する際に、次のオプションを含む実行時オプションを設定できます。

* **コピー**:プリンタに送信する部数を指定します。デフォルト値は 1 です。
* **ステープル**:ステープル印刷が使用されると、XCIオプションが設定されます。このオプションは、設定モデルでステープル要素で指定でき、PSプリンターとPCLプリンターにのみ使用されます。
* **OutputJog**:XCIオプションは、出力ページをジョグ（出力トレイ内で物理的にシフト）する必要がある場合に設定されます。このオプションは、PSおよびPCLプリンター専用です。
* **出力ビン**:印刷ドライバが適切な出力binを選択できるようにするために使用されるXCI値。

>[!NOTE]
>
>設定できるすべての実行時オプションについて詳しくは、`PrintedOutputOptionsSpec`クラス参照を参照してください。

**印刷するドキュメントの取得**

プリンターに送信する印刷ストリームを取得します。 例えば、PostScriptファイルを取得してプリンターに送信できます。

プリンターがPDFをサポートしている場合は、PDFファイルを送信するように選択できます。 ただし、PDFドキュメントをプリンターに送信する際の問題は、プリンターの製造元ごとにPDFインタープリターの実装が異なる点です。 つまり、一部の印刷メーカーはAdobe PDFの解釈を使用しますが、プリンターによって異なります。 その他のプリンターには、独自のPDFインタープリターがあります。 その結果、印刷結果が異なる場合があります。

PDFドキュメントをプリンターに送信するもう1つの制限は、単に印刷することです。両面印刷、用紙トレイの選択、ホチキス止めは、プリンタの設定を使用しない限り使用できません。

印刷するドキュメントを取得するには、`generatePrintedOutput`メソッドを使用します。 次の表は、`generatePrintedOutput`メソッドを使用する際に指定の印刷ストリームに設定されるコンテンツタイプを示しています。

<table>
 <thead>
  <tr>
   <th><p>印刷形式 </p></th>
   <th><p>説明</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>DPL </p></td>
   <td><p>デフォルトまたはカスタムのxdc出力ストリームでdpl203.xdcを作成します。</p></td>
  </tr>
  <tr>
   <td><p>DPL 300 DPI </p></td>
   <td><p>DPL 300 DPI出力ストリームを作成します。</p></td>
  </tr>
  <tr>
   <td><p>DPL 406 DPI </p></td>
   <td><p>DPL 400 DPI出力ストリームを作成します。</p></td>
  </tr>
  <tr>
   <td><p>DPL 600 DPI </p></td>
   <td><p>DPL 600 DPI出力ストリームを作成します。</p></td>
  </tr>
  <tr>
   <td><p>GenericColorPCL </p></td>
   <td><p>汎用カラーPCL(5c)出力ストリームを作成します。</p></td>
  </tr>
  <tr>
   <td><p>GenericPSLevel3 </p></td>
   <td><p>汎用PostScriptレベル3の出力ストリームを作成します。</p></td>
  </tr>
  <tr>
   <td><p>IPL </p></td>
   <td><p>カスタムIPL出力ストリームを作成します。</p></td>
  </tr>
  <tr>
   <td><p>IPL 300 DPI </p></td>
   <td><p>IPL 300 DPI出力ストリームを作成します。</p></td>
  </tr>
  <tr>
   <td><p>IPL 400 DPI </p></td>
   <td><p>IPL 400 DPI出力ストリームを作成します。</p></td>
  </tr>
  <tr>
   <td><p>PCL </p></td>
   <td><p>汎用モノクロPCL(5e)出力ストリームを作成します。</p></td>
  </tr>
  <tr>
   <td><p>PostScript </p></td>
   <td><p>汎用PostScriptレベル2の出力ストリームを作成します。</p></td>
  </tr>
  <tr>
   <td><p>TPCL </p></td>
   <td><p>カスタムTPCL出力ストリームを作成します。</p></td>
  </tr>
  <tr>
   <td><p>TPCL 305 DPI </p></td>
   <td><p>TPCL 305 DPI出力ストリームを作成します。</p></td>
  </tr>
  <tr>
   <td><p>TPCL 600 DPI </p></td>
   <td><p>TPCL 600 DPI出力ストリームを作成します。</p></td>
  </tr>
  <tr>
   <td><p>ZPL </p></td>
   <td><p>ZPL 203 DPI出力ストリームを作成します。</p></td>
  </tr>
  <tr>
   <td><p>ZPL 300 DPI </p></td>
   <td><p>ZPL 300 DPI出力ストリームを作成します。</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>`generatePrintedOutput2`メソッドを使用して、印刷ストリームをプリンターに送信することもできます。 ただし、「プリントストリームをプリンターに送信する」セクションに関連するクイックスタートでは、`generatePrintedOutput`メソッドを使用します。

**印刷ストリームをネットワークプリンタに送信する**

印刷するドキュメントを取得した後、Outputサービスを呼び出すと、印刷ストリームがネットワークプリンターに送信されます。 Outputサービスでプリンターを正しく見つけるには、プリントサーバーとプリンター名の両方を指定する必要があります。 また、印刷プロトコルも指定する必要があります。

>[!NOTE]
>
>PDFGがformsサーバーにインストールされ、サーバーがWindows Server 2008で実行されている場合、SharedPrinterプロパティは使用できません。 この場合は、別のプリンタープロトコルを使用します。

>[!NOTE]
>
>ネットワークプリンタを使用し、アクセスメカニズムがSharedPrinterの場合は、プリンタの完全なネットワークパスを指定する必要があります。Java APIを使用して、印刷ストリームをネットワークプリンタに送信します

Output API(Java)を使用して、印刷ストリームをネットワークプリンターに送信します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-output-client.jarなどのクライアントJARファイルを含めます。

1. Outputクライアントオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して`OutputClient`オブジェクトを渡し、`ServiceClientFactory`オブジェクトを作成します。

1. XMLデータソースの参照

   * コンストラクタを使用し、XMLファイルの場所を指定する文字列値を渡すことで、ドキュメントの入力に使用されるXMLデータソースを表す`java.io.FileInputStream`オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 印刷実行時オプションの設定

   印刷ランタイムオプションを表す`PrintedOutputOptionsSpec`オブジェクトを作成します。 例えば、 `PrintedOutputOptionsSpec`オブジェクトの`setCopies`メソッドを呼び出して、印刷する部数を指定できます。

   >[!NOTE]
   >
   >ZPL印刷ストリームを生成する場合は、 `PrintedOutputOptionsSpec`オブジェクトの`setPagination`メソッドを使用してページネーション値を設定することはできません。 同様に、ZPL印刷ストリームに対して次のオプションを設定することはできません。OutputJog、PageOffset、およびStaple。 `setPagination`メソッドはPostScriptの生成には無効です。 PCL生成にのみ有効です。

1. 印刷するドキュメントの取得

   * `OutputClient`オブジェクトの`generatePrintedOutput`メソッドを呼び出し、次の値を渡して、印刷するドキュメントを取得します。

      * 印刷ストリームを指定する`PrintFormat`列挙値。 例えば、PostScript印刷ストリームを作成するには、`PrintFormat.PostScript`を渡します。
      * フォームデザイン名を指定する string 値。
      * 関連する販促物ファイル（画像ファイルなど）の場所を指定するstring値。
      * 使用するXDCファイルの場所を指定するstring値。
      * ファイルに印刷するために必要な実行時オプションを含む`PrintedOutputOptionsSpec`オブジェクト。
      * フォームデザインとマージするフォームデータが含まれるXMLデータソースを表す`com.adobe.idp.Document`オブジェクト。

      このメソッドは、操作の結果を含む`OutputResult`オブジェクトを返します。

   * `OutputResult`オブジェクトの`getGeneratedDoc`メソッドを呼び出して、プリンターに送信する`com.adobe.idp.Document`オブジェクトを作成します。 このメソッドは`com.adobe.idp.Document`オブジェクトを返します。


1. 印刷ストリームをネットワークプリンタに送信する

   `OutputClient`オブジェクトの`sendToPrinter`メソッドを呼び出し、次の値を渡して、印刷ストリームをネットワークプリンターに送信します。

   * プリンターに送信する印刷ストリームを表す`com.adobe.idp.Document`オブジェクト。
   * 使用するプリンタープロトコルを指定する`PrinterProtocol`列挙値。 例えば、SharedPrinterプロトコルを指定するには、`PrinterProtocol.SharedPrinter`を渡します。
   * プリントサーバーの名前を指定するstring値。 例えば、プリントサーバーの名前がPrintSever1の場合、`\\\PrintSever1`を渡します。
   * プリンターの名前を指定するstring値。 例えば、プリンター名がPrinter1の場合、`\\\PrintSever1\Printer1`を渡します。

   >[!NOTE]
   >
   >`sendToPrinter`メソッドがバージョン8.2.1のAEM Forms APIに追加されました。

### WebサービスAPI {#send-a-print-stream-to-a-printer-using-the-web-service-api}を使用して印刷ストリームをプリンターに送信します

Output API（Webサービス）を使用して、印刷ストリームをネットワークプリンターに送信します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. Outputクライアントオブジェクトを作成します。

   * デフォルトのコンストラクターを使用して`OutputServiceClient`オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`OutputServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに渡す文字列値（例：`http://localhost:8080/soap/services/OutputService?blob=mtom`）を渡します。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する際に使用されます。 ただし、MTOMを使用する場合は`?blob=mtom`を指定します。
   * `OutputServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値は、MTOMが使用されるようにします。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールド`OutputServiceClient.ClientCredentials.UserName.UserName`にAEM formsユーザー名を割り当てます。
      * 対応するパスワード値をフィールド`OutputServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * フィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に定数値`HttpClientCredentialType.Basic`を割り当てます。
      * フィールド`BasicHttpBindingSecurity.Security.Mode`に定数値`BasicHttpSecurityMode.TransportCredentialOnly`を割り当てます。

1. XMLデータソースを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、フォームデータの格納に使用されます。
   * コンストラクターを呼び出して、`System.IO.FileStream`オブジェクトを作成します。 フォームデータを含むXMLファイルの場所を指定するstring値を渡します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得して、バイト配列の長さを決定します。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことによって、バイト配列にストリームデータを入力します。
   * `BLOB`オブジェクトの`MTOM`フィールドにバイト配列の内容を割り当てて、オブジェクトを設定します。

1. 印刷実行時オプションを設定します。

   コンストラクタを使用して `PrintedOutputOptionsSpec` オブジェクトを作成します。例えば、`PrintedOutputOptionsSpec`オブジェクトの`copies`データメンバーにコピー数を表す整数値を割り当てて、印刷するコピー数を指定できます。

   >[!NOTE]
   >
   >ZPL印刷ストリームを生成する場合は、`PrintedOutputOptionsSpec`オブジェクトの`pagination`データメンバを使用してページネーション値を設定することはできません。 同様に、ZPL印刷ストリームに対して次のオプションを設定することはできません。OutputJog、PageOffsetおよびStaple。 `pagination`データメンバはPostScriptの生成には無効です。 PCL生成にのみ有効です。

1. 印刷するドキュメントを取得します。

   * `OutputServiceService`オブジェクトの`generatePrintedOutput`メソッドを呼び出し、次の値を渡して、印刷するドキュメントを取得します。

      * 印刷ストリームを指定する`PrintFormat`列挙値。 例えば、PostScript印刷ストリームを作成するには、`PrintFormat.PostScript`を渡します。
      * フォームデザイン名を指定する string 値。
      * 関連する販促物ファイル（画像ファイルなど）の場所を指定するstring値。
      * 使用するXDCファイルの場所を指定するstring値。
      * 印刷ストリームをネットワークプリンターに送信する際に使用される印刷実行時オプションを含む`PrintedOutputOptionsSpec`オブジェクト。
      * フォームデータを含むXMLデータソースを含む`BLOB`オブジェクト。
      * `generatePrintedOutput`メソッドによって設定される`BLOB`オブジェクト。 `generatePrintedOutput`メソッドは、このオブジェクトに、ドキュメントを表す生成済みのメタデータを入力します。 （このパラメーター値は、Webサービスの呼び出しのみに必要です）。
      * `generatePrintedOutput`メソッドによって設定される`BLOB`オブジェクト。 `generatePrintedOutput`メソッドは、このオブジェクトに結果データを入力します。 （このパラメーター値は、Webサービスの呼び出しのみに必要です）。
      * 操作の結果を格納する`OutputResult`オブジェクト。 （このパラメーター値は、Webサービスの呼び出しのみに必要です）。
   * `OutputResult`オブジェクトの`generatedDoc`メソッドの値を取得して、プリンターに送信する`BLOB`オブジェクトを作成します。 このメソッドは、 `generatePrintedOutput`メソッドで返されるPostScriptデータを含む`BLOB`オブジェクトを返します。


1. 印刷ストリームをネットワークプリンタに送信します。

   `OutputClient`オブジェクトの`sendToPrinter`メソッドを呼び出し、次の値を渡して、印刷ストリームをネットワークプリンターに送信します。

   * プリンターに送信する印刷ストリームを表す`BLOB`オブジェクト。
   * 使用するプリンタープロトコルを指定する`PrinterProtocol`列挙値。 例えば、SharedPrinterプロトコルを指定するには、`PrinterProtocol.SharedPrinter`を渡します。
   * 前のパラメータ値を使用するかどうかを指定する`bool`値。 値`true`を渡します。 （このパラメーター値は、Webサービスの呼び出しのみに必要です）。
   * プリントサーバーの名前を指定するstring値。 例えば、プリントサーバーの名前がPrintSever1である場合は、`\\\PrintSever1`を渡します。
   * プリンターの名前を指定するstring値。 例えば、プリンター名がPrinter1である場合は、`\\\PrintSever1\Printer1`を渡します。

   >[!NOTE]
   >
   >`sendToPrinter`メソッドがバージョン8.2.1のAEM Forms APIに追加されました。

## 複数の出力ファイルの作成{#creating-multiple-output-files}

Outputサービスでは、XMLデータソース内のレコードごとに別々のドキュメントを作成することも、すべてのレコードを含む単一のファイルを作成することもできます（この機能はデフォルトです）。 例えば、10件のレコードがXMLデータソース内に配置され、Output Service APIを使用して各レコードに対して個別のPDFドキュメント（または他のタイプの出力）を作成するようにOutputサービスに指示したとします。 その結果、Outputサービスは10個のPDFドキュメントを生成します。 （ドキュメントを作成する代わりに、1台のプリンターに複数の印刷ストリームを送信できます）。

次の図に、複数のレコードを含むXMLデータファイルを処理するOutputサービスを示します。 ただし、すべてのデータレコードを含む単一のPDFドキュメントを作成するようにOutputサービスに指示したとします。 この場合、Outputサービスは、すべてのレコードを含む1つのドキュメントを生成します。

次の図に、複数のレコードを含むXMLデータファイルを処理するOutputサービスを示します。 Outputサービスに対して、データレコードごとに個別のPDFドキュメントを作成するよう指示したとします。 この場合、Outputサービスは、データレコードごとに個別のPDFドキュメントを生成します。

![cm_outputbatchmany](assets/cm_outputbatchmany.png)

次のXMLデータは、3つのデータレコードを含むデータファイルの例を示しています。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <batch>
 <LoanRecord>
     <mortgageAmount>500000</mortgageAmount>
     <lastName>Blue</lastName>
     <firstName>Tony</firstName>
     <SSN>555666777</SSN>
     <PositionTitle>Product Manager</PositionTitle>
     <Address>555 No Where Dr</Address>
     <City>New York</City>
     <StateProv>New York</StateProv>
     <ZipCode>51256</ZipCode>
     <Email>TBlue@NoMailServer.com</Email>
     <PhoneNum>555-7418</PhoneNum>
     <FaxNum>555-9981</FaxNum>
     <Description>Buy a home</Description>
 </LoanRecord>
 <LoanRecord>
     <mortgageAmount>300000</mortgageAmount>
     <lastName>White</lastName>
     <firstName>Sam</firstName>
     <SSN>555666222</SSN>
     <PositionTitle>Program Manager</PositionTitle>
     <Address>557 No Where Dr</Address>
     <City>New York</City>
     <StateProv>New York</StateProv>
     <ZipCode>51256</ZipCode>
     <Email>SWhite@NoMailServer.com</Email>
     <PhoneNum>555-7445</PhoneNum>
     <FaxNum>555-9986</FaxNum>
     <Description>Buy a home</Description>
 </LoanRecord>
 <LoanRecord>
     <mortgageAmount>700000</mortgageAmount>
     <lastName>Green</lastName>
     <firstName>Steve</firstName>
     <SSN>55566688</SSN>
     <PositionTitle>Project Manager</PositionTitle>
     <Address>445 No Where Dr</Address>
     <City>New York</City>
     <StateProv>New York</StateProv>
     <ZipCode>51256</ZipCode>
     <Email>SGreeb@NoMailServer.com</Email>
     <PhoneNum>555-2211</PhoneNum>
     <FaxNum>555-2221</FaxNum>
     <Description>Buy a home</Description>
 </LoanRecord>
 </batch>
```

各データレコードを開始および終了するXML要素は`LoanRecord`です。 このXML要素は、複数のファイルを生成するアプリケーションロジックによって参照されます。

>[!NOTE]
>
>Outputサービスについて詳しくは、『AEM Formsのサービスリファレンス[』を参照してください。](https://www.adobe.com/go/learn_aemforms_services_63)

### 手順の概要{#summary_of_steps-7}

1つのXMLデータソースに基づいて複数のPDFファイルを作成するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Outputクライアントオブジェクトを作成します。
1. XMLデータソースを参照します。
1. PDF実行時オプションを設定します。
1. レンダリングの実行時オプションを設定します。
1. 複数のPDFファイルを生成します。
1. 操作の結果を取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用する場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(AEM FormsをJBossにデプロイする場合に必要)
* jbossall-client.jar(AEM FormsをJBossにデプロイする場合に必要)

AEM FormsがJBoss以外のサポート対象のJ2EEアプリケーションサーバーにデプロイされている場合は、adobe-utilities.jarファイルとjbossall-client.jarファイルを、AEM FormsがデプロイされているJ2EEアプリケーションサーバーに固有のJARファイルに置き換える必要があります。

**Outputクライアントオブジェクトの作成**

プログラムによってOutputサービス操作を実行する前に、Outputサービスクライアントオブジェクトを作成する必要があります。 Java APIを使用している場合は、`OutputClient`オブジェクトを作成します。 Output WebサービスAPIを使用している場合は、`OutputServiceService`オブジェクトを作成します。

**XMLデータソースの参照**

複数のレコードを含むXMLデータソースを参照します。 データレコードを区切るには、XML要素を使用する必要があります。 例えば、この節で前述したXMLデータソースの例では、データレコードを区切るXML要素の名前は`LoanRecord`です。

データを入力するフォームフィールドごとに、XML要素が存在する必要があります。 XML要素名は、フィールド名と一致する必要があります。 XML要素がフォームフィールドに対応していない場合や、XML要素名がフィールド名と一致しない場合は無視されます。 すべてのXML要素を指定した場合、XML要素の表示順序を一致させる必要はありません。

**PDF実行時オプションの設定**

XMLデータソースに基づいて複数のファイルを正常に作成するには、Outputサービスに次のランタイムオプションを設定する必要があります。

* **多数のファイル**:Outputサービスで1つのドキュメントを作成するか、複数のドキュメントを作成するかを指定します。trueまたはfalseを指定できます。 XMLデータソース内のデータレコードごとに個別のドキュメントを作成するには、trueを指定します。
* **ファイルURI**:Outputサービスが生成するファイルの場所を指定します。例えば、C:\\Adobe\forms\Loan.pdfと指定したとします。 この場合、OutputサービスはLoan.pdfという名前のファイルを作成し、C:\\Adobe\forms folderフォルダーに配置します。 複数のファイルが存在する場合、ファイル名はLoan0001.pdf、Loan0002.pdf、Loan0003.pdfなどです。 ファイルの場所を指定した場合、ファイルはクライアントコンピューターではなくサーバーに配置されます。
* **レコード名**:データレコードを区切るデータソース内のXML要素名を指定します。例えば、この節で前に示したXMLデータソースの例では、データレコードを区切るXML要素は`LoanRecord`と呼ばれます。 (「レコード名」実行時オプションを設定する代わりに、データレコードを含む要素レベルを示す数値をレコードレベルに割り当てて、レコードレベルを設定できます。 ただし、「レコード名」または「レコードレベル」のみを設定できます。 両方の値を設定することはできません)。

**レンダリング実行時オプションの設定**

複数のファイルを作成する際に、レンダリングの実行時オプションを設定できます。 これらのオプションは必須ではありませんが（必須の出力ランタイムオプションとは異なり）、Outputサービスのパフォーマンス向上などのタスクを実行できます。 例えば、Outputサービスが使用するフォームデザインをキャッシュして、パフォーマンスを向上させることができます。

Outputサービスがバッチレコードを処理する場合、複数のレコードを含むデータを増分方法で読み取ります。 つまり、Outputサービスはデータをメモリに読み取り、レコードのバッチが処理されるたびにデータを解放します。 Outputサービスは、2つのランタイムオプションのいずれかが設定されている場合、増分方法でデータを読み込みます。 「Record Name」ランタイムオプションを設定した場合、Outputサービスは増分方法でデータを読み取ります。 同様に、「Record Level」実行時オプションを2以上に設定した場合、Outputサービスは増分方法でデータを読み取ります。

`PDFOutputOptionsSpec`または`PrintedOutputOptionSpec`オブジェクトの`setLazyLoading`メソッドを使用して、Outputサービスで増分読み込みを実行するかどうかを制御できます。 このメソッドに値`false`を渡すと、増分読み込みがオフになります。

**複数のPDFファイルの生成**

複数のデータレコードと実行時オプションを設定した有効なXMLデータソースを参照した後、Outputサービスを呼び出すと、複数のファイルが生成されます。 複数のレコードを生成する場合、`OutputResult`オブジェクトの`getGeneratedDoc`メソッドは`null`を返します。

**操作の結果の取得**

Outputサービスが操作を実行すると、その操作が成功したかどうかを示すXMLデータが返されます。 次のXMLがOutputサービスによって返されます。 この場合、Outputサービスは42個のドキュメントを生成しました。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <printResult>
 <status>0</status>
 <requestId>4ad85f9e2</requestId>
 <context/>
 <messages>
 <message>Printed all 42 records successfully.</message>
 </messages>
 <printSpec>
 <input>
 <validated>true</validated>
 <dataFile recordIdField="" recordLevel="0" recordName="LoanRecord"/>
 <sniffRules lookAhead="300"/>
 <formDesign>Loan.xdp</formDesign>
 <contentRoot>C:\Adobe</contentRoot>
 <metadata-spec record="false"/>
 </input>
 <output>
 <format>PDF</format>
 <fileURI>C:\Adobe\forms\Loan.pdf</fileURI>
 <optionString>cacheenabled=true&padebug=false&linearpdf=false&pdfarevisionnumber=1&pdfaconformance=A&taggedpdf=false&TransactionTimeOut=180</optionString>
 <waitForResponse>true</waitForResponse>
 <outputStream>multiple</outputStream>
 </output>
 </printSpec>
 </printResult>
```

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[OutputサービスAPIのクイックスタート](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Java API {#create-multiple-pdf-files-using-the-java-api}を使用して複数のPDFファイルを作成します

Output API(Java)を使用して複数のPDFファイルを作成します。

1. プロジェクトファイルを含める&quot;

   Javaプロジェクトのクラスパスに、adobe-output-client.jarなどのクライアントJARファイルを含めます。.

1. Outputクライアントオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して`OutputClient`オブジェクトを渡し、`ServiceClientFactory`オブジェクトを作成します。

1. XMLデータソースの参照

   * コンストラクタを使用し、XMLファイルの場所を指定する文字列値を渡すことで、複数のレコードを含むXMLデータソースを表す`java.io.FileInputStream`オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PDF実行時オプションの設定

   * コンストラクタを使用して `PDFOutputOptionsSpec` オブジェクトを作成します。
   * `PDFOutputOptionsSpec`オブジェクトの`setGenerateManyFiles`メソッドを呼び出して、「多数のファイル」オプションを設定します。 例えば、値`true`を渡して、XMLデータソース内の各レコードに対して個別のPDFファイルを作成するようにOutputサービスに指示します。 （`false`を渡すと、すべてのレコードを含む単一のPDFドキュメントがOutputサービスによって生成されます）。
   * `PDFOutputOptionsSpec`オブジェクトの`setFileUri`メソッドを呼び出し、Outputサービスが生成するファイルの場所を指定する文字列値を渡すことで、「File URI」オプションを設定します。 「ファイルURI 」オプションは、AEM FormsをホストするJ2EEアプリケーションサーバーに対して相対的なもので、クライアントコンピューターに対しては相対的なものではありません。
   * `OutputOptionsSpec`オブジェクトの`setRecordName`メソッドを呼び出し、データレコードを区切るデータソース内のXML要素名を指定する文字列値を渡すことで、「レコード名」オプションを設定します。 (例えば、この節で前述したXMLデータソースについて考えてみましょう。 データレコードを区切るXML要素の名前はLoanRecordです。

1. レンダリング実行時オプションの設定

   * コンストラクタを使用して `RenderOptionsSpec` オブジェクトを作成します。
   * `RenderOptionsSpec`オブジェクトの`setCacheEnabled`を呼び出し、`true`の`Boolean`値を渡すことで、フォームデザインをキャッシュしてOutputサービスのパフォーマンスを向上させます。

1. 複数のPDFファイルの生成

   `OutputClient`オブジェクトの`generatePDFOutput`メソッドを呼び出し、次の値を渡して、複数のPDFファイルを生成します。

   * `TransformationFormat`列挙値。 PDFドキュメントを生成するには、`TransformationFormat.PDF`を指定します。
   * フォームデザイン名を指定する string 値。
   * フォームデザインが存在するコンテンツルートを指定するstring値。
   * PDFランタイムオプションを含む`PDFOutputOptionsSpec`オブジェクト。
   * レンダリングの実行時オプションを含む`RenderOptionsSpec`オブジェクト。
   * フォームデザインとマージするデータを含むXMLデータソースを含む`com.adobe.idp.Document`オブジェクト。

   `generatePDFOutput`メソッドは、操作の結果を含む`OutputResult`オブジェクトを返します。

1. 操作の結果の取得

   * `generatePDFOutput`メソッドの結果を格納するXMLファイルを表す`java.io.File`オブジェクトを作成します。 ファイル名の拡張子が.xmlであることを確認します。
   * `com.adobe.idp.Document`オブジェクトの`copyToFile`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトの内容をファイルにコピーします（`applyUsageRights`メソッドで返された`com.adobe.idp.Document`オブジェクトを使用するようにしてください）。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[クイックスタート（EJBモード）:Java APIを使用した複数のPDFファイルの作成](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-multiple-pdf-files-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#create-multiple-pdf-files-using-the-web-service-api}を使用して複数のPDFファイルを作成します

Output API（Webサービス）を使用して複数のPDFファイルを作成します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. Outputクライアントオブジェクトを作成します。

   * デフォルトのコンストラクターを使用して`OutputServiceClient`オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`OutputServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに渡す文字列値（例：`http://localhost:8080/soap/services/OutputService?blob=mtom`）を渡します。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する際に使用されます。 ただし、MTOMを使用する場合は`?blob=mtom`を指定します。
   * `OutputServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値は、MTOMが使用されるようにします。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールド`OutputServiceClient.ClientCredentials.UserName.UserName`にAEM formsユーザー名を割り当てます。
      * 対応するパスワード値をフィールド`OutputServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * フィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に定数値`HttpClientCredentialType.Basic`を割り当てます。
      * フィールド`BasicHttpBindingSecurity.Security.Mode`に定数値`BasicHttpSecurityMode.TransportCredentialOnly`を割り当てます。

1. XMLデータソースを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、複数のレコードを含むフォームデータを格納するために使用します。
   * コンストラクターを呼び出して、`System.IO.FileStream`オブジェクトを作成します。 複数のレコードを含むXMLファイルのファイルの場所を表すstring値を渡します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得することで、バイト配列のサイズを判断できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことによって、バイト配列にストリームデータを入力します。
   * `BLOB`オブジェクトの`MTOM`フィールドにバイト配列の内容を割り当てて、オブジェクトを設定します。

1. PDF実行時オプションを設定します。

   * コンストラクタを使用して `PDFOutputOptionsSpec` オブジェクトを作成します。
   * `OutputOptionsSpec`オブジェクトの`generateManyFiles`データメンバーにブール値を割り当てて、「多数のファイル」オプションを設定します。 例えば、このデータメンバーに値`true`を割り当てて、XMLデータソース内の各レコードに対して個別のPDFファイルを作成するようにOutputサービスに指示します。 （このデータメンバーに`false`を割り当てると、Outputサービスは、すべてのレコードを含む単一のPDFを生成します）。
   * Outputサービスが生成するファイルの場所を指定する文字列値を`OutputOptionsSpec`オブジェクトの`fileURI`データメンバーに割り当てて、「file URI」オプションを設定します。 「ファイルURI 」オプションは、AEM FormsをホストするJ2EEアプリケーションサーバーに対して相対的なもので、クライアントコンピューターに対しては相対的なものではありません。
   * `OutputOptionsSpec`オブジェクトの`recordName`データメンバーにデータレコードを分離するデータソース内のXML要素名を指定する文字列値を割り当てて、レコード名オプションを設定します。
   * Outputサービスが`OutputOptionsSpec`オブジェクトの`copies`データメンバーに生成するコピー数を指定する整数値を割り当てて、copiesオプションを設定します。

1. レンダリングの実行時オプションを設定します。

   * コンストラクタを使用して `RenderOptionsSpec` オブジェクトを作成します。
   * 値`true`を`RenderOptionsSpec`オブジェクトの`cacheEnabled`データメンバーに割り当てることで、フォームデザインをキャッシュして、Outputサービスのパフォーマンスを向上させます。

1. 複数のPDFファイルを生成します。

   `OutputServiceService`オブジェクトの`generatePDFOutput`メソッドを呼び出し、次の値を渡して、複数のPDFファイルを作成します。

   * TransformationFormat列挙値。 PDFドキュメントを生成するには、`TransformationFormat.PDF`を指定します。
   * フォームデザイン名を指定する string 値。
   * フォームデザインが存在するコンテンツルートを指定するstring値。
   * PDFランタイムオプションを含む`PDFOutputOptionsSpec`オブジェクト。
   * レンダリングの実行時オプションを含む`RenderOptionsSpec`オブジェクト。
   * フォームデザインとマージするデータを含むXMLデータソースを含む`BLOB`オブジェクト。
   * `generatePDFOutput`メソッドによって設定される`BLOB`オブジェクト。 `generatePDFOutput`メソッドは、このオブジェクトに、ドキュメントを表す生成済みのメタデータを入力します。
   * `generatePDFOutput`メソッドによって設定される`BLOB`オブジェクト。 `generatePDFOutput`メソッドは、このオブジェクトに結果データを入力します。
   * 操作の結果を格納する`OutputResult`オブジェクト。

1. 操作の結果の取得

   * コンストラクターを呼び出し、結果データを含むXMLファイルの場所を表す文字列値を渡すことで、`System.IO.FileStream`オブジェクトを作成します。 ファイル名の拡張子が.xmlであることを確認します。
   * `OutputServiceService`オブジェクトの`generatePDFOutput`メソッド（8番目のパラメーター）によって結果データが入力された`BLOB`オブジェクトのデータコンテンツを格納するバイト配列を作成します。 `BLOB`オブジェクトの`binaryData`データメンバーの値を取得して、バイト配列を設定します。
   * コンストラクターを呼び出し、`System.IO.FileStream`オブジェクトを渡して、`System.IO.BinaryWriter`オブジェクトを作成します。
   * `System.IO.BinaryWriter`オブジェクトの`Write`メソッドを呼び出し、バイト配列を渡すことにより、バイト配列の内容をXMLファイルに書き込みます。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 検索ルールの作成{#creating-search-rules}

Outputサービスで入力データを調べ、データコンテンツに基づいて様々なフォームデザインを使用して出力を生成する検索ルールを作成できます。 例えば、入力データ内にテキスト&#x200B;*mortgage*&#x200B;が配置されている場合、OutputサービスはMortgage.xdpという名前のフォームデザインを使用できます。 同様に、入力データ内にテキスト&#x200B;*automobile*&#x200B;が配置されている場合、Outputサービスでは、AutomobileLoan.xdpとして保存されたフォームデザインを使用できます。 Outputサービスでは異なる出力タイプを生成できますが、この節では、OutputサービスでPDFファイルが生成されることを前提としています。 次の図に、XMLデータファイルを処理し、様々なフォームデザインの1つを使用してPDFファイルを生成するOutputサービスを示します。

さらに、Outputサービスでは、複数のレコードがデータセットに提供され、各レコードがフォームデザインに一致し、1つのドキュメントが複数のフォームデザインで構成されるドキュメントパッケージを生成できます。

![cs_outputbatchmanyformdesigns2](assets/cs_outputbatchmanyformdesigns2.png)

>[!NOTE]
>
>Outputサービスについて詳しくは、『AEM Formsのサービスリファレンス[』を参照してください。](https://www.adobe.com/go/learn_aemforms_services_63)

### 手順の概要{#summary_of_steps-8}

ドキュメントの生成時に検索ルールを使用するようにOutputサービスに指示するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Outputクライアントオブジェクトを作成します。
1. XMLデータソースを参照します。
1. 検索ルールを定義します。
1. PDF実行時オプションを設定します。
1. レンダリングの実行時オプションを設定します。
1. PDFドキュメントを生成します。
1. 操作の結果を取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用する場合は、プロキシファイルを必ず含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(AEM FormsがJBossにデプロイされている場合に必須)
* jbossall-client.jar(AEM FormsがJBossにデプロイされている場合に必須)

AEM FormsがJBoss以外のサポート対象のJ2EEアプリケーションサーバーにデプロイされている場合は、adobe-utilities.jarとjbossall-client.jarを、AEM FormsがデプロイされているJ2EEアプリケーションサーバーに固有のJARファイルに置き換える必要があります。

**Outputクライアントオブジェクトの作成**

プログラムによってOutputサービス操作を実行する前に、Outputサービスクライアントオブジェクトを作成する必要があります。

**XMLデータソースの参照**

データを入力するフォームフィールドごとに、XML要素が存在する必要があります。 XML要素名は、フィールド名と一致する必要があります。 XML要素がフォームフィールドに対応していない場合や、XML要素名がフィールド名と一致しない場合は無視されます。 すべてのXML要素が指定されている限り、XML要素の表示順を一致させる必要はありません。

**検索ルールの定義**

検索ルールを定義するには、Outputサービスが入力データ内で検索する1つ以上のテキストパターンを定義します。 定義するテキストパターンごとに、テキストパターンが存在する場合に使用する対応するフォームデザインを指定します。 テキストパターンが見つかった場合、Outputサービスは対応するフォームデザインを使用して出力を生成します。 例えば、*mortgage*&#x200B;などのテキストパターンがあります。

>[!NOTE]
>
>テキストパターンが見つからない場合は、デフォルトのフォームが使用されます。 使用するすべてのフォームデザインがコンテンツルートに配置されていることを確認します。

**PDF実行時オプションの設定**

Outputサービスが複数のフォームデザインに基づいてPDFドキュメントを正常に作成するために、次のPDFランタイムオプションを設定します。

* **ファイルURI**:Outputサービスが生成するPDFファイルの名前と場所を指定します。
* **ルール**:定義したルールを指定します。
* **LookAhead**:定義済みのテキストパターンをスキャンするために入力データファイルの先頭から使用するバイト数を指定します。デフォルトは500バイトです。

**レンダリング実行時オプションの設定**

PDFファイルの作成時にレンダリングの実行時オプションを設定できます。 PDFの実行時オプションとは異なり、これらのオプションは必須ではありませんが、Outputサービスのパフォーマンス向上などのタスクを実行できます。 例えば、Outputサービスが使用するフォームデザインをキャッシュして、パフォーマンスを向上させることができます。

**PDFドキュメントの生成**

有効なXMLデータソースを参照し、実行時オプションを設定した後、Outputサービスを呼び出すと、PDFドキュメントが生成されます。 Outputサービスが入力データ内で指定されたテキストパターンを見つけた場合は、対応するフォームデザインが使用されます。 テキストパターンを使用しない場合、Outputサービスはデフォルトのフォームデザインを使用します。

**操作の結果の取得**

Outputサービスが操作を実行すると、その操作が成功したかどうかを示すXMLデータが返されます。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[OutputサービスAPIのクイックスタート](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Java API {#create-search-rules-using-the-java-api}を使用した検索ルールの作成

Output API(Java)を使用して検索ルールを作成します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-output-client.jarなどのクライアントJARファイルを含めます。

1. Outputクライアントオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して`OutputClient`オブジェクトを渡し、`ServiceClientFactory`オブジェクトを作成します。

1. XMLデータソースを参照します。

   * PDFドキュメントのコンストラクターを使用し、XMLファイルの場所を指定する文字列値を渡すことで、PDFドキュメントの入力に使用されるXMLデータソースを表す`java.io.FileInputStream`オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 検索ルールを定義します。

   * コンストラクタを使用して `Rule` オブジェクトを作成します。
   * `Rule`オブジェクトの`setPattern`メソッドを呼び出し、テキストパターンを指定する文字列値を渡すことで、テキストパターンを定義します。
   * `Rule`オブジェクトの`setForm`メソッドを呼び出して、対応するフォームデザインを定義します。 フォームデザインの名前を指定するstring値を渡します。

   >[!NOTE]
   >
   >定義するテキストパターンごとに、前の3つのサブ手順を繰り返します。

   * `java.util.ArrayList`コンストラクターを使用して`java.util.List`オブジェクトを作成します。
   * 作成した各`Rule`オブジェクトに対して、`java.util.List`オブジェクトの`add`メソッドを呼び出し、`Rule`オブジェクトを渡します。


1. PDF実行時オプションを設定します。

   * コンストラクタを使用して `PDFOutputOptionsSpec` オブジェクトを作成します。
   * `PDFOutputOptionsSpec`オブジェクトの`setFileURI`メソッドを呼び出して、Outputサービスが生成するPDFファイルの名前と場所を指定します。 PDFファイルの場所を指定するstring値を渡します。 「ファイルURI 」オプションは、AEM FormsをホストするJ2EEアプリケーションサーバーに対して相対的なもので、クライアントコンピューターに対しては相対的なものではありません。
   * `PDFOutputOptionsSpec`オブジェクトの`setRules`メソッドを呼び出して、定義したルールを設定します。 `Rule`オブジェクトを含む`java.util.List`オブジェクトを渡します。
   * `PDFOutputOptionsSpec`オブジェクトの`setLookAhead`メソッドを呼び出して、定義済みのテキストパターンをスキャンするバイト数を設定します。 バイト数を表す整数値を渡します。

1. レンダリングの実行時オプションを設定します。

   * コンストラクタを使用して `RenderOptionsSpec` オブジェクトを作成します。
   * `RenderOptionsSpec`オブジェクトの`setCacheEnabled`を呼び出して`true`を渡すことで、Outputサービスのパフォーマンスを向上させるためにフォームデザインをキャッシュします。

1. PDFドキュメントを生成します。

   `OutputClient`オブジェクトの`generatePDFOutput`メソッドを呼び出し、次の値を渡すことで、複数のフォームデザインに基づいたPDFドキュメントを生成します。

   * `TransformationFormat`列挙値。 PDFドキュメントを生成するには、`TransformationFormat.PDF`を指定します。
   * デフォルトのフォームデザインの名前を指定するstring値。 つまり、テキストパターンが見つからない場合に使用されるフォームデザインです。
   * フォームデザインが配置されるコンテンツルートを指定するstring値。
   * PDFランタイムオプションを含む`PDFOutputOptionsSpec`オブジェクト。
   * レンダリングの実行時オプションを含む`RenderOptionsSpec`オブジェクト。
   * 定義されたテキストパターンについてOutputサービスが検索するフォームデータを含む`com.adobe.idp.Document`オブジェクト。

   `generatePDFOutput`メソッドは、操作の結果を含む`OutputResult`オブジェクトを返します。

1. 操作の結果を取得します。

   * `OutputResult`オブジェクトの`getStatusDoc`メソッドを呼び出して、`generatePDFOutput`メソッドのステータスを表す`com.adobe.idp.Document`オブジェクトを作成します。
   * 操作の結果を格納する`java.io.File`オブジェクトを作成します。 ファイル拡張子が.xmlであることを確認します。
   * `com.adobe.idp.Document`オブジェクトの`copyToFile`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトの内容をファイルにコピーします（`getStatusDoc`メソッドで返された`com.adobe.idp.Document`オブジェクトを使用するようにしてください）。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[クイックスタート（EJBモード）:Java APIを使用した検索ルールの作成](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[クイックスタート（SOAPモード）:Java APIを使用した検索ルールの作成](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#create-search-rules-using-the-web-service-api}を使用して検索ルールを作成します。

Output API（Webサービス）を使用して検索ルールを作成します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. Outputクライアントオブジェクトを作成します。

   * デフォルトのコンストラクターを使用して`OutputServiceClient`オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`OutputServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに渡す文字列値（例：`http://localhost:8080/soap/services/OutputService?blob=mtom`）を渡します。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する際に使用されます。 ただし、MTOMを使用する場合は`?blob=mtom`を指定します。
   * `OutputServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値は、MTOMが使用されるようにします。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールド`OutputServiceClient.ClientCredentials.UserName.UserName`にAEM formsユーザー名を割り当てます。
      * 対応するパスワード値をフィールド`OutputServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * フィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に定数値`HttpClientCredentialType.Basic`を割り当てます。
      * フィールド`BasicHttpBindingSecurity.Security.Mode`に定数値`BasicHttpSecurityMode.TransportCredentialOnly`を割り当てます。

1. XMLデータソースを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、PDFドキュメントとマージされるデータを保存するために使用されます。
   * コンストラクターを呼び出し、暗号化するPDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得することで、バイト配列のサイズを判断できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことによって、バイト配列にストリームデータを入力します。
   * `BLOB`オブジェクトの`MTOM`フィールドにバイト配列の内容を割り当てて、オブジェクトを設定します。

1. 検索ルールを定義します。

   * コンストラクタを使用して `Rule` オブジェクトを作成します。
   * `Rule`オブジェクトの`pattern`データメンバにテキストパターンを指定する文字列値を割り当てて、テキストパターンを定義します。
   * `Rule`オブジェクトの`form`データメンバーにフォームデザインを指定する文字列値を割り当てて、対応するフォームデザインを定義します。

   >[!NOTE]
   >
   >定義するテキストパターンごとに、前の3つのサブ手順を繰り返します。

   * ルールを保存する`MyArrayOf_xsd_anyType`オブジェクトを作成します。
   * 各`Rule`オブジェクトを`MyArrayOf_xsd_anyType`配列の要素に割り当てます。 各`Rule`オブジェクトに対して`MyArrayOf_xsd_anyType`オブジェクトの`Add`メソッドを呼び出します。


1. PDF実行時オプションの設定

   * コンストラクタを使用して `PDFOutputOptionsSpec` オブジェクトを作成します。
   * Outputサービスが生成するPDFファイルの場所を指定する文字列値を`PDFOutputOptionsSpec`オブジェクトの`fileURI`データメンバーに割り当てて、「file URI」オプションを設定します。 「ファイルURI 」オプションは、AEM FormsをホストするJ2EEアプリケーションサーバーに対して相対的なもので、クライアントコンピューターに対しては相対的なものではありません。
   * Outputサービスが`PDFOutputOptionsSpec`オブジェクトの`copies`データメンバーに生成するコピー数を指定する整数値を割り当てて、copiesオプションを設定します。
   * ルールを格納する`MyArrayOf_xsd_anyType`オブジェクトを`PDFOutputOptionsSpec`オブジェクトの`rules`データメンバーに割り当てて、定義したルールを設定します。
   * 定義済みのテキストパターンをスキャンするバイト数を設定します。スキャンするバイト数を表す整数値を`PDFOutputOptionsSpec`オブジェクトの`lookAhead`データメソッドに割り当てます。

1. レンダリング実行時オプションの設定

   * コンストラクタを使用して `RenderOptionsSpec` オブジェクトを作成します。
   * 値`true`を`RenderOptionsSpec`オブジェクトの`cacheEnabled`データメンバーに割り当てて、Outputサービスのパフォーマンスを向上させるためにフォームデザインをキャッシュします。

   >[!NOTE]
   >
   >入力ドキュメントがAcrobatフォームの場合、`RenderOptionsSpec`オブジェクトの`pdfVersion`メンバーを使用してPDFドキュメントのバージョンを設定することはできません。 出力PDFドキュメントには、AcrobatフォームのPDFバージョンが保持されます。 同様に、入力ドキュメントがAcrobatフォームの場合は、 `RenderOptionsSpec`オブジェクトの`taggedPDF`メソッドを使用して、タグ付きPDFオプションを設定することはできません。

   >[!NOTE]
   >
   >入力PDFドキュメントが認証またはデジタル署名されている場合、`RenderOptionsSpec`オブジェクトの`linearizedPDF`メンバを使用して線形化されたPDFオプションを設定することはできません。 詳しくは、[PDFドキュメントのデジタル署名](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)を参照してください。

1. PDFドキュメントの生成

   `OutputServiceService`オブジェクトの`generatePDFOutput`メソッドを呼び出し、次の値を渡してPDFドキュメントを作成します。

   * `TransformationFormat`列挙値。 PDFドキュメントを生成するには、`TransformationFormat.PDF`を指定します。
   * フォームデザイン名を指定する string 値。
   * フォームデザインが存在するコンテンツルートを指定するstring値。
   * PDFランタイムオプションを含む`PDFOutputOptionsSpec`オブジェクト。
   * レンダリングの実行時オプションを含む`RenderOptionsSpec`オブジェクト。
   * フォームデザインとマージするデータを含むXMLデータソースを含む`BLOB`オブジェクト。
   * `generatePDFOutput`メソッドによって設定される`BLOB`オブジェクト。 `generatePDFOutput`メソッドは、このオブジェクトに、ドキュメントを表す生成済みのメタデータを入力します。 （このパラメーター値は、Webサービスの呼び出しにのみ必要です）。
   * `generatePDFOutput`メソッドによって設定される`BLOB`オブジェクト。 `generatePDFOutput`メソッドは、このオブジェクトに結果データを入力します。 （このパラメーター値は、Webサービスの呼び出しにのみ必要です）。
   * 操作の結果を格納する`OutputResult`オブジェクト。 （このパラメーター値は、Webサービスの呼び出しにのみ必要です）。

   >[!NOTE]
   >
   >`generatePDFOutput`メソッドを呼び出してPDFドキュメントを生成する場合、使用権限を含む、署名済みまたは認証済みのXFA PDFフォームとのデータの結合はできないことに注意してください。 使用権限について詳しくは、[PDFドキュメントへの使用権限の適用](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)を参照してください。

1. 操作の結果の取得

   * コンストラクターを呼び出し、結果データを含むXMLファイルの場所を表す文字列値を渡すことで、`System.IO.FileStream`オブジェクトを作成します。 ファイル拡張子がXMLであることを確認します。
   * `OutputServiceService`オブジェクトの`generatePDFOutput`メソッド（8番目のパラメーター）によって結果データが入力された`BLOB`オブジェクトのデータコンテンツを格納するバイト配列を作成します。 `BLOB`オブジェクトの`MTOM`データメンバーの値を取得して、バイト配列を設定します。
   * コンストラクターを呼び出し、`System.IO.FileStream`オブジェクトを渡して、`System.IO.BinaryWriter`オブジェクトを作成します。
   * `System.IO.BinaryWriter`オブジェクトの`Write`メソッドを呼び出し、バイト配列を渡すことにより、バイト配列の内容をXMLファイルに書き込みます。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## PDFドキュメントのフラット化{#flattening-pdf-documents}

Outputサービスを使用して、インタラクティブPDFドキュメントを非インタラクティブPDFに変換できます。 インタラクティブPDFドキュメントを使用すると、ユーザーはPDFドキュメントフィールドにデータを入力または変更できます。 インタラクティブPDFドキュメントを非インタラクティブPDFドキュメントに変換するプロセスは、*統合*&#x200B;と呼ばれます。 PDFドキュメントを統合すると、ユーザーはドキュメントフィールド内のデータを変更できなくなります。 PDF ドキュメントを統合する理由の 1 つは、データを変更できないようにすることです。

次のタイプのPDFドキュメントを統合できます。

* インタラクティブXFA PDFドキュメント
* AcrobatForms

非インタラクティブPDFドキュメントのPDFをフラット化しようとすると、例外が発生します。

>[!NOTE]
>
>Outputサービスについて詳しくは、『AEM Formsのサービスリファレンス[』を参照してください。](https://www.adobe.com/go/learn_aemforms_services_63)

### 手順の概要{#summary_of_steps-9}

インタラクティブPDFドキュメントを非インタラクティブPDFドキュメントに統合するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Outputクライアントオブジェクトを作成します。
1. インタラクティブPDFドキュメントを取得します。
1. PDFドキュメントを変換します。
1. 非インタラクティブPDFドキュメントをPDFファイルとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用する場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(AEM FormsをJBossにデプロイする場合に必要)
* jbossall-client.jar(AEM FormsをJBossにデプロイする場合に必要)

AEM FormsがJBoss以外のサポート対象のJ2EEアプリケーションサーバーにデプロイされている場合は、adobe-utilities.jarファイルとjbossall-client.jarファイルを、AEM FormsがデプロイされているJ2EEアプリケーションサーバーに固有のJARファイルに置き換える必要があります。 すべてのAEM Forms JARファイルの場所について詳しくは、「[AEM Forms Javaライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)」を参照してください。

**Outputクライアントオブジェクトの作成**

プログラムによってOutputサービス操作を実行する前に、Outputサービスクライアントオブジェクトを作成する必要があります。 Java APIを使用している場合は、`OutputClient`オブジェクトを作成します。 Output WebサービスAPIを使用している場合は、`OutputServiceService`オブジェクトを作成します。

**インタラクティブPDFドキュメントの取得**

非インタラクティブPDFドキュメントに変換するインタラクティブPDFドキュメントを取得します。 非インタラクティブPDFドキュメントを変換しようとすると、例外が発生します。

**PDFドキュメントの変換**

インタラクティブPDFドキュメントを取得した後、そのドキュメントを非インタラクティブPDFドキュメントに変換できます。 Outputサービスは非インタラクティブPDFドキュメントを返します。

**非インタラクティブPDFドキュメントをPDFファイルとして保存します**

非インタラクティブPDFドキュメントをPDFファイルとして保存できます。

**関連トピック**

[Java APIを使用したPDFドキュメントの統合](creating-document-output-streams.md#flatten-a-pdf-document-using-the-java-api)

[WebサービスAPIを使用したPDFドキュメントの統合](creating-document-output-streams.md#flatten-a-pdf-document-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[OutputサービスAPIのクイックスタート](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Java API {#flatten-a-pdf-document-using-the-java-api}を使用したPDFドキュメントの統合

Output API(Java)を使用して、インタラクティブPDFドキュメントを非インタラクティブPDFドキュメントに統合します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-output-client.jarなどのクライアントJARファイルを含めます。

1. Outputクライアントオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して`OutputClient`オブジェクトを渡し、`ServiceClientFactory`オブジェクトを作成します。

1. インタラクティブPDFドキュメントを取得します。

   * 変換するインタラクティブPDFドキュメントを表す`java.io.FileInputStream`オブジェクトを作成します。その際、コンストラクターを使用し、インタラクティブPDFファイルの場所を指定するstring値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PDFドキュメントを変換します。

   `OutputServiceService`オブジェクトの`transformPDF`メソッドを呼び出し、次の値を渡すことで、インタラクティブPDFドキュメントを非インタラクティブPDFドキュメントに変換します。

   * インタラクティブPDFドキュメントを格納する`com.adobe.idp.Document`オブジェクト。
   * `TransformationFormat`列挙値。 非インタラクティブPDFドキュメントを生成するには、`TransformationFormat.PDF`を指定します。
   * リビジョン番号を指定する`PDFARevisionNumber`列挙値。 このパラメーターはPDF/Aドキュメント用なので、`null`を指定できます。
   * 修正番号と年をコロンで区切って表すstring値です。 このパラメーターはPDF/Aドキュメント用なので、`null`を指定できます。
   * PDF/A準拠レベルを表す`PDFAConformance`列挙値。 このパラメーターはPDF/Aドキュメント用なので、`null`を指定できます。

   `transformPDF`メソッドは、非インタラクティブPDFドキュメントを含む`com.adobe.idp.Document`オブジェクトを返します。

1. 非インタラクティブPDFドキュメントをPDFファイルとして保存します。

   * `java.io.File`オブジェクトを作成し、ファイル名拡張子が.pdfであることを確認します。
   * `Document`オブジェクトの`copyToFile`メソッドを呼び出して、`Document`オブジェクトの内容をファイルにコピーします（`transformPDF`メソッドで返された`Document`オブジェクトを使用するようにしてください）。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[クイックスタート（EJBモード）:Java APIを使用したPDFドキュメントの変換](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

[クイックスタート（SOAPモード）:Java APIを使用したPDFドキュメントの変換](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#flatten-a-pdf-document-using-the-web-service-api}を使用してPDFドキュメントを統合する

Output API（Webサービス）を使用して、インタラクティブPDFドキュメントを非インタラクティブPDFドキュメントに統合します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. Outputクライアントオブジェクトを作成します。

   * デフォルトのコンストラクターを使用して`OutputServiceClient`オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`OutputServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに渡す文字列値（例：`http://localhost:8080/soap/services/OutputService?blob=mtom`）を渡します。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する際に使用されます。 ただし、MTOMを使用する場合は`?blob=mtom`を指定します。
   * `OutputServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値は、MTOMが使用されるようにします。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールド`OutputServiceClient.ClientCredentials.UserName.UserName`にAEM formsユーザー名を割り当てます。
      * 対応するパスワード値をフィールド`OutputServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * フィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に定数値`HttpClientCredentialType.Basic`を割り当てます。
      * フィールド`BasicHttpBindingSecurity.Security.Mode`に定数値`BasicHttpSecurityMode.TransportCredentialOnly`を割り当てます。

1. インタラクティブPDFドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、インタラクティブPDFドキュメントの保存に使用されます。
   * コンストラクターを呼び出し、インタラクティブPDFドキュメントのファイルの場所を表すstring値を渡すことで、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得することで、バイト配列のサイズを判断できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことによって、バイト配列にストリームデータを入力します。
   * `BLOB`オブジェクトの`MTOM`プロパティにバイト配列の内容を割り当てて、オブジェクトを設定します。

1. PDFドキュメントを変換します。

   `OutputClient`オブジェクトの`transformPDF`メソッドを呼び出し、次の値を渡すことで、インタラクティブPDFドキュメントを非インタラクティブPDFドキュメントに変換します。

   * インタラクティブPDFドキュメントを格納する`BLOB`オブジェクト。
   * `TransformationFormat`列挙値。 非インタラクティブPDFドキュメントを生成するには、`TransformationFormat.PDF`を指定します。
   * リビジョン番号を指定する`PDFARevisionNumber`列挙値。
   * `PDFARevisionNumber`列挙値を使用するかどうかを指定するBoolean値。 このパラメーターはPDF/Aドキュメント用なので、`false`を指定できます。
   * 修正番号と年をコロンで区切って表すstring値です。 このパラメーターはPDF/Aドキュメント用なので、`null`を指定できます。
   * PDF/A準拠レベルを表す`PDFAConformance`列挙値。
   * `PDFAConformance`列挙値を使用するかどうかを指定するブール値。 このパラメーターはPDF/Aドキュメント用なので、`false`を指定できます。

   `transformPDF`メソッドは、非インタラクティブPDFドキュメントを含む`BLOB`オブジェクトを返します。

1. 非インタラクティブPDFドキュメントをPDFファイルとして保存します。

   * コンストラクターを呼び出し、非インタラクティブPDFドキュメントのファイルの場所を表すstring値を渡すことで、`System.IO.FileStream`オブジェクトを作成します。
   * `transformPDF`メソッドで返された`BLOB`オブジェクトのデータ内容を格納するバイト配列を作成します。 `BLOB`オブジェクトの`MTOM`データメンバーの値を取得して、バイト配列を設定します。
   * コンストラクターを呼び出し、`System.IO.FileStream`オブジェクトを渡して、`System.IO.BinaryWriter`オブジェクトを作成します。
   * `System.IO.BinaryWriter`オブジェクトの`Write`メソッドを呼び出し、バイト配列を渡すことにより、バイト配列の内容をPDFファイルに書き込みます。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
