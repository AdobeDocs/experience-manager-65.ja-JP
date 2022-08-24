---
title: ドキュメント Output ストリームの作成
seo-title: Creating Document Output Streams
description: Output サービスを使用すると、ドキュメントを PDF（PDF/A ドキュメントを含む）、PostScript、Printer Control Language（PCL）および Zebra - ZPL、Intermec - IPL、Datamax - DPL、TecToshiba - TPCL ラベル形式に変換できます。
seo-description: Use the Output service to convert documents as PDF (including PDF/A documents), PostScript, Printer Control Language (PCL), and Zebra - ZPL, Intermec - IPL, Datamax - DPL, and TecToshiba - TPCL label formats.
uuid: 80c28efa-35ce-4073-9ca6-2d93bcd67fdd
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: de527d50-991b-4ca3-a8ac-44d5cab988e9
role: Developer
exl-id: a521bfac-f417-4002-9c5c-8d7794d3eec7
source-git-commit: 74882ccf78a62d543f1598f12ee009f9922c18a4
workflow-type: tm+mt
source-wordcount: '19016'
ht-degree: 100%

---

# ドキュメント Output ストリームの作成  {#creating-document-output-streams}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

**Output サービスについて**

Output サービスを使用すると、ドキュメントを PDF（PDF/A ドキュメントを含む）、PostScript、Printer Control Language（PCL）および次のラベル形式で出力できます。

* Zebra - ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

Output サービスを使用すると、XML フォームデータをフォームデザインと結合し、ドキュメントをネットワークプリンターまたはファイルに出力できます。

フォームデザイン（XDP ファイル）を Output サービスに渡す方法は 2 とおりあります。フォームデザインを含んだ `com.adobe.idp.Document` インスタンスを Output サービスに渡すことができます。または、フォームデザインの場所を指定する URI 値を渡すこともできます。これらの方法については、*AEM Forms によるプログラミング*&#x200B;を参照してください。

>[!NOTE]
>
>Output サービスでは、アプリケーションオブジェクト固有のスクリプトを含んだ Acroform PDF ドキュメントをサポートしていません。アプリケーションオブジェクト固有のスクリプトを含む Acroform PDF ドキュメントは、レンダリングされません。

次の節では、URI 値を使用してフォームデザインを Output サービスに渡す方法を説明します。

* [PDF ドキュメントの作成](creating-document-output-streams.md#creating-pdf-documents)
* [PDF/A ドキュメントの作成](creating-document-output-streams.md#creating-pdf-a-documents)

次の節では、`com.adobe.idp.Document` インスタンス内でフォームデザインを渡す方法について説明します。

* [コンテンツサービス（非推奨）にあるドキュメントを Output サービスに渡す方法](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)
* [フラグメントを使用した PDF ドキュメントの作成](creating-document-output-streams.md#creating-pdf-documents-using-fragments)

どの手法を使用するかを決定する際の考慮事項の 1 つは、別の AEM Forms サービスからフォームデザインを取得して `com.adobe.idp.Document` インスタンス内で渡すかどうかです。*Output サービスへのドキュメントの受け渡し*&#x200B;と&#x200B;*フラグメントを使用した PDF ドキュメントの作成*&#x200B;の両方の節で、別の AEM Forms サービスからフォームデザインを取得する方法を説明します。最初の節では、コンテンツサービス（非推奨）からフォームデザインを取得します。2 つ目の節では、Assembler サービスからフォームデザインを取得します。

ファイルシステムのような固定された場所からフォームデザインを取得する場合は、どちらの方法も使用できます。つまり、URI 値を XDP ファイルに指定するか、`com.adobe.idp.Document` インスタンスを使用できます。

フォームデザインの場所を指定する URI 値を PDF ドキュメントの作成時に渡すには、`generatePDFOutput` メソッドを使用します。同様に、PDFドキュメントを作成する際に `com.adobe.idp.Document` インスタンスを Output サービスに渡すには、`generatePDFOutput2` メソッドを使用します。

Output ストリームをネットワークプリンターに送信する場合は、どちらの方法でも使用できます。フォームデザインを含んだ `com.adobe.idp.Document` インスタンスを渡して Output ストリームをプリンターに送信するには、`sendToPrinter2` メソッドを使用します。URI 値を渡して Output ストリームをプリンターに送信するには、`sendToPrinter` メソッドを使用します。*プリンターへの印刷ストリームの送信*&#x200B;の節では、`sendToPrinter` メソッドを使用しています。

Output サービスを使用して、以下のタスクを実行できます。

* [PDF ドキュメントの作成](creating-document-output-streams.md#creating-pdf-documents)
* [PDF/A ドキュメントの作成](creating-document-output-streams.md#creating-pdf-a-documents)
* [コンテンツサービス（非推奨）にあるドキュメントを Output サービスに渡す方法](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)
* [フラグメントを使用した PDF ドキュメントの作成](creating-document-output-streams.md#creating-pdf-documents-using-fragments)
* [ファイルへの印刷](creating-document-output-streams.md#printing-to-files)
* [プリンターへの印刷ストリームの送信](creating-document-output-streams.md#sending-print-streams-to-printers)
* [複数の Output ファイルの作成](creating-document-output-streams.md#creating-multiple-output-files)
* [検索ルールの作成](creating-document-output-streams.md#creating-search-rules)
* [PDF ドキュメントの平坦化](creating-document-output-streams.md#flattening-pdf-documents)

>[!NOTE]
>
>Output サービスについて詳しくは、[AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

## PDF ドキュメントの作成 {#creating-pdf-documents}

Output サービスを使用すると、提供するフォームデザインと XML フォームデータに基づいた PDF ドキュメントを作成できます。Output サービスで作成される PDF ドキュメントは、インタラクティブな PDF ドキュメントではないので、ユーザーがフォームデータを入力したり変更したりできません。

長期保存を目的とした PDF ドキュメントを作成する場合は、PDF/A ドキュメントを作成することをお勧めします。詳しくは、[PDF/A ドキュメントの作成](creating-document-output-streams.md#creating-pdf-a-documents)を参照してください。

ユーザーがデータを入力できるインタラクティブな PDF フォームを作成するには、Forms サービスを使用します。詳しくは、[インタラクティブ PDF Forms のレンダリング](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms)を参照してください。

>[!NOTE]
>
>Output サービスについて詳しくは、[AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary-of-steps}

PDF ドキュメントを作成するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Output クライアントオブジェクトを作成します。
1. XML データソースを参照します。
1. PDF の実行時オプションを設定します。
1. レンダリングの実行時オプションを設定します。
1. PDF ドキュメントの生成
1. 操作の結果を取得します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、必ずプロキシファイルを含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar（AEM Forms を JBoss にデプロイする場合に必要）
* jbossall-client.jar（AEM Forms が JBoss にデプロイされている場合に必要）

AEM Forms が JBoss 以外のサポート対象の J2EE アプリケーションサーバーにデプロイされている場合は、adobe-utilities.jar ファイルと jbossall-client.jar ファイルを、AEM Forms がデプロイされている J2EE アプリケーションサーバーに固有の JAR ファイルに置き換える必要があります。

**Output クライアントオブジェクトの作成**

プログラムで Output サービスの操作を実行する前に、Output サービスのクライアントオブジェクトを作成する必要があります。Java API を使用している場合は、`OutputClient` オブジェクトを作成します。Output web サービス API を使用している場合は、`OutputServiceService` オブジェクトを作成します。

**XML データソースの参照**

データをフォームデザインと結合するには、データを含む XML データソースを参照する必要があります。XML 要素は、データを入力するすべてのフォームフィールドに存在する必要があります。XML 要素名は、フィールド名と一致する必要があります。XML 要素がフォームフィールドに対応していない場合や、XML 要素名がフィールド名と一致しない場合、XML 要素は無視されます。すべての XML 要素が指定されている場合、XML 要素の表示順序を一致させる必要はありません。

次のローン申し込みフォームのサンプルについて考えてみましょう。

![cp_cp_loanformdata](assets/cp_cp_loanformdata.png)

このフォームデザインにデータを結合するには、フォームに対応する XML データソースを作成する必要があります。次の XML は、住宅ローン申し込みフォームのサンプルに対応する XML データソースを表しています。

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

**PDF 実行時オプションの設定**

PDF ドキュメントを作成する際に、ファイル URI オプションを設定します。このオプションは、Output サービスが生成する PDF ファイルの名前と場所を指定します。

>[!NOTE]
>
>ファイル URI 実行時オプションを設定する代わりに、Output サービスから返される複雑なデータタイプから PDF ドキュメントをプログラム的に取得できます。ただし、ファイル URI 実行時オプションを設定すれば、PDF ドキュメントをプログラム的に取得するアプリケーションロジックを作成する必要はありません。

**レンダリング実行時オプションの設定**

PDF ドキュメントの作成時に、レンダリング実行時オプションを設定できます。これらのオプションは必須ではありません（必須の PDF 実行時オプションとは異なります）が、Output サービスのパフォーマンス向上などのタスクを実行できます。例えば、パフォーマンスを向上させるために Output サービスが使用するフォームデザインをキャッシュできます。

タグ付き Acrobat フォームを入力として使用する場合、Output サービス Java または Web サービス API を使用してタグ付き設定をオフにすることはできません。このオプションをプログラム的に `false` に設定しようとしても、結果の PDF ドキュメントにはタグが付いたままになります。

>[!NOTE]
>
>レンダリング実行時オプションを指定しない場合は、デフォルト値が使用されます。レンダリング実行時オプションについて詳しくは、`RenderOptionsSpec` クラスリファレンスを参照してください。（[AEM Forms API リファレンス](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ja)を参照）。

**PDF ドキュメントの生成**

フォームデータを含む有効な XML データソースを参照し、実行時オプションを設定した後、Output サービスを呼び出すと、PDF ドキュメントが生成されます。

PDFドキュメントを生成するときは、Output サービスで PDF ドキュメントを作成するために必要な URI 値を指定します。フォームデザインは、サーバーファイルシステムなどの場所に保存することも、AEM Forms アプリケーションの一部として保存することもできます。Forms アプリケーションの一部として存在するフォームデザイン（または画像ファイルなどの他のリソース）は、コンテンツルート URI 値を使用して参照できます `repository:///`。例えば、*Applications/FormsApplication* という名前の Forms アプリケーション内にある *Loan.xdp* という名前の次のフォームデザインについて考えてみます。

![cp_cp_formrepository](assets/cp_cp_formrepository.png)

前の図に示す Loan.xdp ファイルにアクセスするには、`OutputClient` オブジェクトの `generatePDFOutput` メソッドに渡す 3 番目のパラメーターとして `repository:///Applications/FormsApplication/1.0/FormsFolder/` を指定します。`OutputClient` オブジェクトの `generatePDFOutput` メソッドに渡す 2 番目のパラメータとしてフォーム名（*Loan.xdp*）を指定します。

XDP ファイルに画像（またはフラグメントなどの他のリソース）が含まれている場合は、XDP ファイルと同じアプリケーションフォルダーにリソースを配置します。AEM Forms は、画像への参照を解決するためのベースパスとしてコンテンツルート URI を使用します。例えば、Loan.xdp ファイルに画像が含まれている場合、画像は必ず `Applications/FormsApplication/1.0/FormsFolder/` に配置します。

>[!NOTE]
>
>`OutputClient` オブジェクトの `generatePDFOutput` メソッドまたは `generatePrintedOutput` メソッドを呼び出すときに、Forms アプリケーション URI を参照できます。

>[!NOTE]
>
>Forms アプリケーションにある XDP を参照して PDF ドキュメントを作成する完全なクイックスタートについては、[クイックスタート（EJB モード）：Java API を使用したアプリケーション XDP ファイルに基づく PDF ドキュメントの作成](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api)を参照してください。

**操作の結果の取得**

Output サービスは、操作を実行した後、操作が成功したかどうかを指定するステータス XML データなど、様々なデータ項目を返します。

**関連トピック**

[Java API を使用した PDF ドキュメントの作成](creating-document-output-streams.md#create-a-pdf-document-using-the-java-api)

[Web サービス API を使用した PDF ドキュメントの作成](creating-document-output-streams.md#create-a-pdf-document-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Output Service API のクイックスタート](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Java API を使用した PDF ドキュメントの作成 {#create-a-pdf-document-using-the-java-api}

Output API（Java）を使用して PDF ドキュメントを作成します。

1. プロジェクトファイルを含めます。

   adobe-output-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. Output クライアントオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して `ServiceClientFactory` オブジェクトを渡すことにより、`OutputClient` オブジェクトを作成します。

1. XML データソースを参照します。

   * コンストラクターを使用し、XML ファイルの場所を指定する文字列値を渡すことにより、PDF ドキュメントの入力に使用される XML データソースを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクターを使用して `com.adobe.idp.Document` オブジェクトを作成します。`java.io.FileInputStream` オブジェクトを渡します。

1. PDF の実行時オプションを設定します。

   * コンストラクターを使用して `PDFOutputOptionsSpec` オブジェクトを作成します。
   * `PDFOutputOptionsSpec` オブジェクトの `setFileURI` メソッドを呼び出して、ファイル URI オプションを設定します。Output サービスが生成する PDF ファイルの場所を指定する文字列値を渡します。ファイル URI オプションは、クライアントコンピューターではなく、AEM Forms をホストする J2EE アプリケーションサーバーに対する相対パスです。

1. レンダリングの実行時オプションを設定します。

   * コンストラクターを使用して `RenderOptionsSpec` オブジェクトを作成します。
   * フォームデザインをキャッシュして、`RenderOptionsSpec` オブジェクトの `setCacheEnabled` を呼び出し、`true` を渡すことにより、Output サービスのパフォーマンスを向上させます。

   >[!NOTE]
   >
   >入力ドキュメントが Acrobat フォーム（Acrobat で作成されたフォーム）または署名や認証を行った XFA ドキュメントの場合、`RenderOptionsSpec` オブジェクトの `setPdfVersion` メソッドを使用して PDF ドキュメントのバージョンを設定することはできません。Output PDF ドキュメントには、元の PDF バージョンが保持されます。同様に、入力ドキュメントが Acrobat フォームまたは署名済みまたは認定済みの XFA ドキュメントである場合、`RenderOptionsSpec` オブジェクトの `setTaggedPDF` メソッドを呼び出してタグ付き Adobe PDF オプションを設定することはできません。

   >[!NOTE]
   >
   >入力 PDF ドキュメントが認証済みまたはデジタル署名されている場合、`RenderOptionsSpec` オブジェクトの `setLinearizedPDF` メソッドを使用してリニアライズド PDF オプションを設定することはできません。（[PDF ドキュメントへのデジタル署名&#x200B;](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)*を参照。）*

1. PDF ドキュメントの生成

   `OutputClient` オブジェクトの `generatePDFOutput` メソッドを呼び出し、次の値を渡すことによって、PDF ドキュメントを作成します。

   * `TransformationFormat` 列挙値。PDF ドキュメントを生成するには、`TransformationFormat.PDF` を指定します。
   * フォームデザイン名を指定する文字列値。
   * フォームデザインが配置されているコンテンツルートを指定する文字列の値です。
   * PDF 実行時オプションを含む `PDFOutputOptionsSpec` オブジェクト。
   * レンダリング実行時オプションを含む `RenderOptionsSpec` オブジェクト。
   * フォームデザインと結合するデータを含む XML データソースを含む `com.adobe.idp.Document` オブジェクト。

   `generatePDFOutput` メソッドは、操作の結果を含む `OutputResult` オブジェクトを返します。

   >[!NOTE]
   >
   >`generatePDFOutput` メソッドを呼び出して PDF ドキュメントを生成する場合、署名または認証された XFA PDF フォームとデータを結合することはできません。（[ドキュメントのデジタル署名と認証&#x200B;](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-and-certifying-documents)*。）*

   >[!NOTE]
   >
   >`OutputResult` オブジェクトの `getRecordLevelMetaDataList` メソッドの戻り値 `null`*。*

   >[!NOTE]
   >
   >また、`OutputClient` オブジェクトの `generatePDFOutput2` メソッドを呼び出して、PDF ドキュメントを作成することもできます。（[コンテンツサービス（非推奨）にあるドキュメントを Output サービスに渡す&#x200B;](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)*を参照。）*

1. 操作の結果を取得します。

   *  `OutputResult` オブジェクトの `getStatusDoc` メソッドを呼び出して、`generatePDFOutput` 操作のステータスを表す `com.adobe.idp.Document` オブジェクトを取得します。このメソッドは、操作が成功したかどうかを指定するステータス XML データを返します。
   * 操作の結果を含む `java.io.File` オブジェクトを作成します。ファイル名の拡張子が .xml であることを確認します。
   * `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを呼び出して、`com.adobe.idp.Document` オブジェクトの内容をファイルにコピーします（`getStatusDoc` メソッドが返した `com.adobe.idp.Document` オブジェクトを使用します）。

   Output サービスは、`PDFOutputOptionsSpec` オブジェクトの `setFileURI` メソッドに渡された引数で指定された場所に PDF ドキュメントを書き込みますが、`OutputResult` オブジェクトの `getGeneratedDoc` メソッドを呼び出して、プログラムで PDF/A ドキュメントを取得できます。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[クイックスタート（EJB モード）：Java API を使用した PDF ドキュメントの作成](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[クイックスタート（SOAP モード）：Java API を使用した PDF ドキュメントの作成](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用した PDF ドキュメントの作成 {#create-a-pdf-document-using-the-web-service-api}

Output API（web サービス）を使用して PDF ドキュメントを作成します。

1. プロジェクトファイルを含めます。

   MTOM を使用する Microsoft .NET プロジェクトを作成します。WSDL 定義 `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1` を使用するようにします。

   >[!NOTE]
   >
   >`localhost` を、AEM Forms をホストするサーバーの IP アドレスで置換します。

1. Output クライアントオブジェクトを作成します。

   * デフォルトのコンストラクターを使用して、`OutputServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して、`OutputServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/OutputService?blob=mtom`）。`lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。ただし、`?blob=mtom` を指定して MTOM を使用します。
   * `OutputServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` フィールドを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `OutputServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `OutputServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
      * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` を`BasicHttpBindingSecurity.Security.Mode` フィールドに割り当てます。

1. XML データソースを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB` オブジェクトは、PDF ドキュメントと結合される XML データを格納するために使用します。
   * コンストラクターを呼び出し、フォームデータを含む XML ファイルのファイルの場所を表す文字列値を渡すことにより、`System.IO.FileStream` オブジェクトを作成します。
   * `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することで、バイト配列のサイズを決定できます。
   * `System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出し、バイト配列、開始位置、読み取るストリーム長を渡すことにより、バイト配列にストリームデータを入力します。
   * `MTOM` フィールドにバイト配列の内容を割り当てて、`BLOB` オブジェクトにデータを入力します。

1. PDF 実行時オプションを設定

   * コンストラクタを使用して `PDFOutputOptionsSpec` オブジェクトを作成します。
   * Output サービスが生成する PDF ファイルの場所を `PDFOutputOptionsSpec` オブジェクトの `fileURI` データメンバーに指定する文字列値を割り当てて、「File URI」オプションを設定します。ファイル URI オプションは、クライアントコンピューターではなく、AEM Forms をホストする J2EE アプリケーションサーバーに対する相対パスです。

1. レンダリングの実行時オプションを設定します。

   * コンストラクタを使用して `RenderOptionsSpec` オブジェクトを作成します。
   * 値 `true` を `RenderOptionsSpec` オブジェクトの `cacheEnabled` データメンバーに割り当てて、Output サービスのパフォーマンスを向上させるためにフォームデザインをキャッシュします。

   >[!NOTE]
   >
   >入力ドキュメントが、Acrobat フォーム（Acrobat で作成されたフォーム）、または署名もしくは認証された XFA ドキュメントの場合、`RenderOptionsSpec` オブジェクトの `setPdfVersion` メソッドを使用して、PDF ドキュメントのバージョンを設定することはできません。Output PDF ドキュメントには、元の PDF バージョンが保持されます。同様に、入力ドキュメントが Acrobat フォーム、または署名済みもしくは認証済みの XFA ドキュメントの場合、`RenderOptionsSpec` オブジェクトの `setTaggedPDF`* メソッドを呼び出して、タグ付けされた「Adobe PDF」オプションを設定することはできません。

   >[!NOTE]
   >
   >入力 PDF ドキュメントが認証済みもしくはデジタル署名済みの場合、`RenderOptionsSpec` オブジェクトの `linearizedPDF` メンバーを使用して、線形化 PDF オプションを設定することはできません。（[PDF ドキュメントへのデジタル署名&#x200B;](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)*を参照してください）。*

1. PDF ドキュメントの生成

   `OutputServiceService` オブジェクトの `generatePDFOutput` メソッドを呼び出し、次の値を渡すことによって PDF ドキュメントを作成します。

   * `TransformationFormat` 列挙値。PDF ドキュメントを生成するには、`TransformationFormat.PDF` を指定します。
   * フォームデザイン名を指定する文字列値。
   * フォームデザインが配置されているコンテンツルートを指定する文字列の値です。
   * PDF 実行時オプションを含む `PDFOutputOptionsSpec` オブジェクト。
   * レンダリング実行時オプションを含む `RenderOptionsSpec` オブジェクト。
   * フォームデザインと結合するデータが含まれる XML データソースを含む `BLOB` オブジェクト。
   * `generatePDFOutput` メソッドによって入力される `BLOB` オブジェクト。`generatePDFOutput` メソッドは、ドキュメントを説明する生成されたメタデータをこのオブジェクトに入力します。（このパラメーター値は、web サービスの呼び出しにのみ必要です）。
   * `generatePDFOutput` メソッドによって入力される `BLOB` オブジェクト。`generatePDFOutput` メソッドは、このオブジェクトに結果データを入力します。（このパラメーター値は、web サービスの呼び出しにのみ必要です）。
   * 操作の結果を含む `OutputResult` オブジェクト。（このパラメーター値は、web サービスの呼び出しにのみ必要です）。

   >[!NOTE]
   >
   >`generatePDFOutput` メソッドを呼び出して PDF ドキュメントを生成する場合、署名または認証された XFA PDF フォームとデータを結合することはできません。（[ドキュメントのデジタル署名と認証&#x200B;](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-and-certifying-documents)*を参照してください）。*

   >[!NOTE]
   >
   >また、`OutputClient` オブジェクトの `generatePDFOutput2` メソッドを呼び出して PDF ドキュメントの作成ができます。（[コンテンツサービス（非推奨）にあるドキュメントを Output サービスに渡す&#x200B;](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)*を参照。）*

1. 操作の結果を取得します。

   * コンストラクタを呼び出し、結果データを保持する XML ファイルの場所を表す string 値を渡すことにより、`System.IO.FileStream` オブジェクトを作成します。ファイル名の拡張子が .xml であることを確認します。
   * `OutputServiceService` オブジェクトの `generatePDFOutput` メソッドにより結果データを入力した `BLOB` オブジェクトのデータコンテンツを格納するバイト配列を作成します（第 8 パラメータ）。バイト配列を生成するには、`BLOB` オブジェクトの `MTOM` `field` の値を取得します。
   * コンストラクターを呼び出し、`System.IO.FileStream` オブジェクトを渡すことによって、`System.IO.BinaryWriter` オブジェクトを作成します。
   * `System.IO.BinaryWriter` オブジェクトの `Write` メソッドをを呼び出して、バイト配列を渡すことにより、バイト配列の内容を XML ファイルに書き込みます。

   関連トピック

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

   >[!NOTE]
   >
   >この `OutputServiceService` オブジェクトの `generateOutput` メソッドは非推奨です。

## PDF/A ドキュメントの作成 {#creating-pdf-a-documents}

Output サービスを使用して PDF/A ドキュメントを作成できます。PDF/A はドキュメントの内容を長期保存するためのアーカイブ形式なので、すべてのフォントが埋め込まれ、ファイルが非圧縮になります。その結果、通常、PDF/A ドキュメントは標準の PDF ドキュメントよりも大きくなります。また、PDF/A ドキュメントには、オーディオとビデオのコンテンツは含まれません。他の Output サービスタスクと同様に、フォームデザインとデータの両方を提供して、フォームデザインと結合し、PDF/A ドキュメントを作成します。

PDF/A-1 仕様は、a と b の 2 つの適合レベルで構成されます。この 2 つの主な違いは、論理構造（アクセシビリティ）のサポートに関するもので、適合レベル b には必要ありません。適合レベルに関係なく、PDF/A-1 では、生成された PDF/A ドキュメントにすべてのフォントが埋め込まれます。

PDF/A は PDF ドキュメントのアーカイブの標準ですが、標準 PDF ドキュメントがお客様の業務上のニーズを満たす場合、アーカイブに PDF/A を使用する必要はありません。PDF/A 規格の目的は、ドキュメントの保存要件を満たし、長期間保存できる PDF ファイルを確立することです。例えば、ある URL を PDF/A に埋め込むことはできません。これは、URL が時間の経過と共に無効になる可能性があるためです。

組織は、独自のニーズ、ドキュメントの保持期間、ファイルサイズに関する考慮事項を評価し、独自のアーカイブ戦略を決定する必要があります。DocConverter サービスを使用すると、PDF ドキュメントが PDF/A に準拠しているかどうかをプログラム的に判断できます。（[プログラムによる PDF/A 準拠の判断](/help/forms/developing/pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)を参照してください）。

PDF/A ドキュメントでは、フォームデザインで指定されたフォントを使用する必要があり、フォントを置き換えることはできません。その結果、PDF ドキュメント内のフォントがホストオペレーティングシステム（OS）上で使用できない場合は、例外が発生します。

Acrobat で PDF/A ドキュメントを開くと、次の図に示すように、ドキュメントが PDF/A ドキュメントであることを確認するメッセージが表示されます。

![cp_cp_pdfamessage](assets/cp_cp_pdfamessage.png)

>[!NOTE]
>
>AIIM の Web サイトには、[https://www.loc.gov/preservation/digital/formats/fdd/fdd000125.shtml](https://www.loc.gov/preservation/digital/formats/fdd/fdd000125.shtml) からアクセスできる PDF/A の FAQ セクションがあります。

>[!NOTE]
>
>Output サービスについて詳しくは、[AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_65_jp)を参照してください。

### 手順の概要 {#summary_of_steps-1}

PDF/A ドキュメントを作成するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Output クライアントオブジェクトを作成します。
1. XML データソースを参照します。
1. PDF/A 実行時オプションを設定します。
1. レンダリングの実行時オプションを設定します。
1. PDF/A ドキュメントを生成します。
1. 操作の結果を取得します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。Java を使用してカスタムアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、必ずプロキシファイルを含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar（AEM Forms を JBoss にデプロイする場合に必要）
* jbossall-client.jar（AEM Forms が JBoss にデプロイされている場合に必要）

AEM Forms が JBoss 以外のサポート対象の J2EE アプリケーションサーバーにデプロイされている場合は、adobe-utilities.jar ファイルと jbossall-client.jar ファイルを、AEM Forms がデプロイされている J2EE アプリケーションサーバーに固有の JAR ファイルに置き換える必要があります。

**Output クライアントオブジェクトの作成**

プログラムで Output サービスの操作を実行する前に、Output サービスのクライアントオブジェクトを作成する必要があります。Java API を使用している場合は、`OutputClient` オブジェクトを作成します。Output web サービス API を使用している場合は、`OutputServiceService` オブジェクトを作成します。

**XML データソースの参照**

データをフォームデザインと結合するには、データを含む XML データソースを参照する必要があります。データを入力するフォームフィールドごとに、XML 要素が存在している必要があります。XML 要素名は、フィールド名と一致する必要があります。XML 要素がフォームフィールドに対応していない場合や、XML 要素名がフィールド名と一致しない場合、XML 要素は無視されます。すべての XML 要素が指定されている場合、XML 要素の表示順序を一致させる必要はありません。

**PDF/A 実行時オプションを設定**

PDF/A ドキュメントの作成時に「ファイル URI」オプションを設定できます。URI は、AEM Forms をホストする J2EE アプリケーションサーバーに対して相対的です。つまり、C:\Adobe を設定した場合、ファイルはクライアントコンピューターではなく、サーバー上のフォルダーに書き込まれます。URI は、Output サービスが生成する PDF/A ファイルの名前と場所を指定します。

**レンダリング実行時オプションを設定**

レンダリングの実行時オプションは、PDF/A ドキュメントの作成時に設定できます。設定できる PDF/A 関連のオプションは `PDFAConformance` および `PDFARevisionNumber` 値です。`PDFAConformance` 値は、電子ドキュメントの長期保存方法を規定する要件に PDF ドキュメントがどの程度準拠しているかを参照します。このオプションの有効な値は `A` および `B` です。レベル a および b の準拠について詳しくは、タイトルが『*ISO 19005-1 文書管理*』の PDF/A-1 ISO 仕様を参照してください。

この `PDFARevisionNumber` の値は、PDF/A ドキュメントのリビジョン番号を参照します。PDF/A ドキュメントのリビジョン番号について詳しくは、タイトルが『*ISO 19005-1 文書管理*』の PDF/A-1 ISO 仕様を参照してください。

>[!NOTE]
>
>PDF/A 1A ドキュメントの作成時にタグ付けされた Adobe PDF オプションを `false` に設定することはできません。PDF/A 1A は、常にタグ付けされた PDF ドキュメントになります。また、PDF/A 1B ドキュメントの作成時、タグ付けされた Adobe PDF オプションを `true` に設定することはできません。PDF/A 1B は、常にタグなしの PDF ドキュメントになります。

**PDF/A ドキュメントを生成**

フォームデータを含む有効な XML データソースを参照し、実行時オプションを設定した後、Output サービスを呼び出して、PDF/A ドキュメントを生成することができます。

**操作の結果の取得**

Output サービスは操作を実行した後、操作が成功したかどうかを示す、XML データなどの様々なデータ項目を返します。

**関連トピック**

[Java API を使用した PDF/A ドキュメントの作成](creating-document-output-streams.md#create-a-pdf-a-document-using-the-java-api)

[Web サービス API を使用して PDF/A ドキュメントを作成する](creating-document-output-streams.md#create-a-pdf-a-document-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Output Service API のクイックスタート](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Java API を使用した PDF/A ドキュメントの作成 {#create-a-pdf-a-document-using-the-java-api}

Output API（Java）を使用して PDF/A ドキュメントを作成します。

1. プロジェクトファイルを含めます。

   adobe-output-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. Output クライアントオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して `ServiceClientFactory` オブジェクトを渡すことにより、`OutputClient` オブジェクトを作成します。

1. XML データソースを参照します。

   * コンストラクターを使用し、XML ファイルの場所を指定する string 値を渡すことによって、PDF/A ドキュメントにデータを取り込むために使用される、XML データソースを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクターを使用し、`java.io.FileInputStream` オブジェクトを渡すことによって、`com.adobe.idp.Document` オブジェクトを作成します。

1. PDF/A 実行時オプションを設定します。

   * コンストラクターを使用して `PDFOutputOptionsSpec` オブジェクトを作成します。
   * `PDFOutputOptionsSpec` オブジェクトの `setFileURI` メソッドを呼び出して、ファイル URI オプションを設定します。Output サービスが生成する PDF ファイルの場所を指定する文字列値を渡します。ファイル URI オプションは、クライアントコンピューターではなく、AEM Forms をホストする J2EE アプリケーションサーバーに対する相対パスです。

1. レンダリングの実行時オプションを設定します。

   * コンストラクターを使用して `RenderOptionsSpec` オブジェクトを作成します。
   * `RenderOptionsSpec` オブジェクトの `setPDFAConformance` メソッドを呼び出し、適合レベルを指定する `PDFAConformance` 列挙値を渡すことによって、`PDFAConformance` 値を設定します。例えば、適合レベル A を指定するには、`PDFAConformance.A` を渡します。
   * `RenderOptionsSpec` オブジェクトの `setPDFARevisionNumber` メソッドを呼び出し、`PDFARevisionNumber.Revision_1` を渡すことによって、`PDFARevisionNumber` 値を設定します。

   >[!NOTE]
   >
   >`RenderOptionsSpec` オブジェクトの `setPdfVersion`*メソッドに指定する値に関係なく、PDF/A ドキュメントの PDF バージョンは 1.4 です。*

1. PDF/A ドキュメントを生成します。

   `OutputClient` オブジェクトの `generatePDFOutput` メソッドを呼び出し、次の値を渡して、PDF/A ドキュメントを作成します。

   * `TransformationFormat` 列挙値。PDF/A ドキュメントを生成するには、`TransformationFormat.PDFA` を指定します。
   * フォームデザイン名を指定する文字列値。
   * フォームデザインが配置されているコンテンツルートを指定する文字列の値です。
   * PDF 実行時オプションを含む `PDFOutputOptionsSpec` オブジェクト。
   * レンダリング実行時オプションを含む `RenderOptionsSpec` オブジェクト。
   * フォームデザインと結合するデータを含む XML データソースを含む `com.adobe.idp.Document` オブジェクト。

   `generatePDFOutput` メソッドは、操作の結果を含む `OutputResult` オブジェクトを返します。

   >[!NOTE]
   >
   >`OutputResult` オブジェクトの `getRecordLevelMetaDataList` メソッドの戻り値 `null`。

   >[!NOTE]
   >
   >また、 `OutputClient` オブジェクトの `generatePDFOutput`2 メソッドを呼び出して、PDF/A ドキュメントを作成することもできます（[コンテンツサービス（非推奨）にあるドキュメントを Output サービスに渡す](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)を参照）。

1. 操作の結果を取得します。

   * `OutputResult` オブジェクトの `getStatusDoc` メソッドを呼び出して、`generatePDFOutput` メソッドのステータスを表す `com.adobe.idp.Document` オブジェクトを作成します。
   * 操作の結果を含む `java.io.File` オブジェクトを作成します。ファイル名の拡張子が .xml であることを確認します。
   * `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを呼び出して、`com.adobe.idp.Document` オブジェクトの内容をファイルにコピーします（`getStatusDoc` メソッドが返した `com.adobe.idp.Document` オブジェクトを使用していることを確認します）。

   >[!NOTE]
   >
   >Output サービスは、`PDFOutputOptionsSpec` オブジェクトの `setFileURI` メソッドに渡される引数で指定された場所に PDF/A ドキュメントを書き込みますが、`OutputResult` オブジェクトの `getGeneratedDoc` メソッドを呼び出すことにより、プログラムで PDF/A ドキュメントを取得できます。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[クイックスタート（SOAP モード）：Java API を使用した PDF/A ドキュメントの作成](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-a-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用して PDF/A ドキュメントを作成する {#create-a-pdf-a-document-using-the-web-service-api}

Output API（web サービス）を使用して PDF/A ドキュメントを作成します。

1. プロジェクトファイルを含めます。

   MTOM を使用する Microsoft .NET プロジェクトを作成します。WSDL 定義 `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1` を使用するようにします。

   >[!NOTE]
   >
   >`localhost` を、AEM Forms をホストするサーバーの IP アドレスで置換します。

1. Output クライアントオブジェクトを作成します。

   * デフォルトのコンストラクターを使用して、`OutputServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して、`OutputServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/OutputService?blob=mtom`）。`lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。ただし、`?blob=mtom` を指定して MTOM を使用します。
   * `OutputServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` フィールドを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `OutputServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `OutputServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
      * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` を`BasicHttpBindingSecurity.Security.Mode` フィールドに割り当てます。

1. XML データソースを参照します。

   * コンストラクターを使用して `BLOB` オブジェクトを作成します。`BLOB` オブジェクトは、PDF/A ドキュメントと結合されるデータを格納するために使用します。
   * コンストラクターを呼び出し、暗号化する PDF ドキュメントのファイルの場所とファイルを開くモードを表す文字列値を渡して、`System.IO.FileStream` オブジェクトを作成します。
   * `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することで、バイト配列のサイズを決定できます。
   * `System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出し、バイト配列、開始位置、読み取るストリーム長を渡すことにより、バイト配列にストリームデータを入力します。
   * `MTOM` フィールドにバイト配列の内容を割り当てて、`BLOB` オブジェクトにデータを入力します。

1. PDF/A 実行時オプションを設定します。

   * コンストラクターを使用して `PDFOutputOptionsSpec` オブジェクトを作成します。
   * Output サービスが生成する PDF ファイルの場所を指定する文字列値を `PDFOutputOptionsSpec` オブジェクトの `fileURI` データメンバーに割り当てて、「ファイル URI」オプションを設定します。「ファイル URI」オプションは、AEM Forms をホストしている J2EE アプリケーションサーバーに対する相対パスであり、クライアントコンピューターに対する相対パスではありません

1. レンダリングの実行時オプションを設定します。

   * コンストラクターを使用して `RenderOptionsSpec` オブジェクトを作成します。
   *  `PDFAConformance` 列挙値を `RenderOptionsSpec` オブジェクトの `PDFAConformance` データメンバーに割り当てて、`PDFAConformance` 値を設定します。例えば、適合レベル A を指定するには、`PDFAConformance.A` をこのデータメンバーに割り当てます。
   * `PDFARevisionNumber` 列挙値を `RenderOptionsSpec` オブジェクトの `PDFARevisionNumber` データメンバーに割り当てて、`PDFARevisionNumber` 値を設定します。`PDFARevisionNumber.Revision_1` をこのデータメンバーに割り当てます。

   >[!NOTE]
   >
   >PDF/A ドキュメントの PDF バージョンは、指定した値に関係なく 1.4 です。

1. PDF/A ドキュメントを生成します。

   `OutputServiceService` オブジェクトの `generatePDFOutput` メソッドを呼び出し、次の値を渡すことによって、PDF ドキュメントを作成します。

   * TransformationFormat 列挙値。PDF ドキュメントを生成するには、`TransformationFormat.PDFA` を指定します。
   * フォームデザイン名を指定する文字列値。
   * フォームデザインが配置されているコンテンツルートを指定する文字列の値です。
   * PDF 実行時オプションを含む `PDFOutputOptionsSpec` オブジェクト。
   * レンダリング実行時オプションを含む `RenderOptionsSpec` オブジェクト。
   * フォームデザインと結合するデータが含まれる XML データソースを含む `BLOB` オブジェクト。
   * `generatePDFOutput` メソッドによって入力される `BLOB` オブジェクト。この `generatePDFOutput` メソッドは、ドキュメントを説明する生成されたメタデータをこのオブジェクトに入力します。（このパラメーター値は、web サービスの呼び出しにのみ必要です）。
   * `generatePDFOutput` メソッドによって入力される `BLOB` オブジェクト。この `generatePDFOutput` メソッドは、このオブジェクトに結果データを入力します。（このパラメーター値は、web サービスの呼び出しにのみ必要です）。
   * 操作の結果を含める `OutputResult` オブジェクト。（このパラメーター値は、web サービスの呼び出しにのみ必要です）。

   >[!NOTE]
   >
   >また、`OutputClient` オブジェクトの `generatePDFOutput`2 メソッドを呼び出して、PDF/A ドキュメントを作成することもできます（[コンテンツサービス（非推奨）にあるドキュメントを Output サービスに渡す](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)を参照）。

1. 操作の結果を取得します。

   * コンストラクタを呼び出し、結果データを保持する XML ファイルの場所を表す string 値を渡すことにより、`System.IO.FileStream` オブジェクトを作成します。ファイル名の拡張子が .xml であることを確認します。
   * `OutputServiceService` オブジェクトの `generatePDFOutput` メソッド（8 番目のパラメーター）によって結果データが入力された `BLOB` オブジェクトのデータコンテンツを格納するバイト配列を作成します。`BLOB` オブジェクトの `MTOM` フィールドの値を取得して、バイト配列にデータを入力します。
   * コンストラクターを呼び出して `System.IO.FileStream` オブジェクトを渡すことにより、`System.IO.BinaryWriter` オブジェクトを作成します。
   * バイト配列の内容を XML ファイルに書き込むには、`System.IO.BinaryWriter` オブジェクトの `Write` メソッドを呼び出して、バイト配列を渡します。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## コンテンツサービス（非推奨）にあるドキュメントを Output サービスに渡す方法 {#passing-documents-located-in-content-services-deprecated-to-the-output-service}

Output サービスは、通常 XDP ファイルとして保存され、Designer で作成されたフォームデザインに基づく、非インタラクティブな PDF フォームを処理します。フォームデザインを含む `com.adobe.idp.Document` オブジェクトを Output サービスに渡すことができます。次に、Output サービスは `com.adobe.idp.Document` オブジェクトにあるフォームデザインを処理します。

`com.adobe.idp.Document` オブジェクトを Output サービスに渡すことの利点は、他の AEM Forms サービス操作が `com.adobe.idp.Document` インスタンスを返すことです。つまり、別のサービス操作から `com.adobe.idp.Document` インスタンスを取得し、それをレンダリングできます。例えば、次の図に示すように、XDP ファイルが `/Company Home/Form Designs` という名前のコンテンツサービス（非推奨）ノードに格納されているとします。

プログラムでコンテンツサービス（非推奨）から Loan.xdp を取得し、XDP ファイルを `com.adobe.idp.Document` オブジェクト内の Output サービスに渡すことができます。

>[!NOTE]
>
>Forms サービスについて詳しくは、[AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary_of_steps-2}

コンテンツサービス（非推奨）から取得したドキュメントを Output サービスに渡すには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Output と Document Management Client API オブジェクトを作成します。
1. コンテンツサービス（非推奨）からフォームデザインを取得します。
1. 非インタラクティブ PDF フォームをレンダリング
1. データストリームでアクションを実行します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを含めます。

**Output と Document Management Client API オブジェクトの作成**

プログラムで Output service API 操作を実行する前に、Output Client API オブジェクトを作成します。また、このワークフローはコンテンツサービス（非推奨）から XDP ファイルを取得するため、Document Management API オブジェクトを作成します。

**コンテンツサービス（非推奨）からフォームデザインを取得する**

Java または web サービス API を使用して、コンテンツサービス（非推奨）から XDP ファイルを取得します。XDP ファイルは、`com.adobe.idp.Document` インスタンス（または web サービスを使用している場合は `BLOB` インスタンス）内で返されます。その後、`com.adobe.idp.Document` インスタンスを Output サービスに渡すことができます。

**非インタラクティブ PDF フォームのレンダリング**

非インタラクティブフォームをレンダリングするには、コンテンツサービス（非推奨）から返された `com.adobe.idp.Document` インスタンスを Output サービスに渡します。

>[!NOTE]
>
>`generatePDFOutput2` および g `eneratePrintedOutput2` という名前の 2 つの新しいメソッドは、フォームデザインを含む `com.adobe.idp.Document` オブジェクトを受け入れます。また、ネットワークプリンターに印刷ストリームを送信する際に、フォームデザインを含む `com.adobe.idp.Document` を Output サービスに渡すこともできます。

**フォームデータストリームを使ったアクションの実行**

非インタラクティブフォームは、PDF ファイルとして保存できます。フォームは、Adobe Reader または Acrobat で表示できます。

**関連トピック**

[Java API を使用してドキュメントを Output サービスに渡す](creating-document-output-streams.md#pass-documents-to-the-output-service-using-the-java-api)

[Web サービス API を使用してドキュメントを Output サービスに渡す](creating-document-output-streams.md#pass-documents-to-the-output-service-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Output Service API のクイックスタート](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

[フラグメントを使用した PDF ドキュメントの作成](creating-document-output-streams.md#creating-pdf-documents-using-fragments)

### Java API を使用してドキュメントを Output サービスに渡す {#pass-documents-to-the-output-service-using-the-java-api}

Output サービスおよび Content Services（非推奨）API（Java））を使用して、Content Services（非推奨）から取得したドキュメントを渡します。

1. プロジェクトファイルを含めます。

   adobe-livecycle-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. Output と Document Management Client API オブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。（[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照）
   * コンストラクターを使用して `ServiceClientFactory` オブジェクトを渡すことによって、`OutputClient` オブジェクトを作成します。
   * コンストラクターを使用して `ServiceClientFactory` オブジェクトを渡すことによって、`DocumentManagementServiceClientImpl` オブジェクトを作成します。

1. コンテンツサービス（非推奨）からフォームデザインを取得します。

   `DocumentManagementServiceClientImpl` オブジェクトの `retrieveContent` メソッドを呼び出して、次の値を渡します。

   * コンテンツの追加先となるストアを指定する文字列値です。デフォルトのストアは `SpacesStore` です。この値は必須パラメーターです。
   * 取得するコンテンツの完全修飾パスを指定する文字列値（例：`/Company Home/Form Designs/Loan.xdp`）。この値は必須パラメーターです。
   * バージョンを指定する文字列値。この値はオプションのパラメーターであり、空の文字列を渡すことができます。この場合、最新バージョンが取得されます。

   `retrieveContent` メソッドは、XDP ファイルを含む `CRCResult` オブジェクトを返します。`CRCResult` オブジェクトの `getDocument` メソッドを呼び出して、`com.adobe.idp.Document` インスタンスを取得します。

1. 非インタラクティブ PDF フォームをレンダリング

   `OutputClient` オブジェクトの `generatePDFOutput2` メソッドを呼び出して、次の値を渡します。

   * `TransformationFormat` 列挙値。PDF ドキュメントを生成するには、`TransformationFormat.PDF` を指定します。
   * 画像などの追加リソースが存在するコンテンツルートを指定する文字列値。
   * フォームデザインを表す `com.adobe.idp.Document` オブジェクト（`CRCResult` オブジェクトの `getDocument` メソッドが返すインスタンスを使用）。
   * PDF 実行時オプションを含む `PDFOutputOptionsSpec` オブジェクト。
   * レンダリング実行時オプションを含む `RenderOptionsSpec` オブジェクト。
   * フォームデザインと結合するデータを含む XML データソースを含む `com.adobe.idp.Document` オブジェクト。

   `generatePDFOutput2` メソッドは、操作の結果を含む `OutputResult` オブジェクトを返します。

1. フォームデータストリームを使用してアクションを実行します。

   * `OutputResult` オブジェクトの `getGeneratedDoc` メソッドを呼び出して、非インタラクティブフォームを表す `com.adobe.idp.Document` オブジェクトを取得します。
   * 操作の結果を含む `java.io.File` オブジェクトを作成します。ファイル名の拡張子が .pdf であることを確認します。
   * `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを呼び出して、`com.adobe.idp.Document` オブジェクトの内容をファイルにコピーします（`getGeneratedDoc` が返した `com.adobe.idp.Document` オブジェクトを使用していることを確認します）。

**関連情報**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[クイックスタート（EJB モード）：Java API を使用して Output サービスにドキュメントを渡す](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[クイックスタート（SOAP モード）：Java API を使用して Output サービスにドキュメントを渡す](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用してドキュメントを Output サービスに渡す {#pass-documents-to-the-output-service-using-the-web-service-api}

Output サービスとコンテンツサービス（非推奨）API（web サービス）を使用して、コンテンツサービス（非推奨）から取得したドキュメントを渡すには、以下の手順を実行します。

1. プロジェクトファイルを含めます。

   MTOM を使用する Microsoft .NET プロジェクトを作成します。このクライアントアプリケーションは 2 つの AEM Forms サービスを呼び出すので、2 つのサービス参照を作成します。Output サービスに関連付けられたサービス参照には、「`http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`」という WSDL 定義を使用します。

   Document Management サービスに関連付けられたサービス参照には、「`http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`」という WSDL 定義を使用します。

   `BLOB` データタイプは両方のサービス参照に共通なので、使用する場合は `BLOB` データタイプを完全に修飾します。対応する web サービスのクイックスタートでは、すべての `BLOB` インスタンスが完全に修飾されています。

   >[!NOTE]
   >
   >`localhost` を、AEM Forms のホストサーバーの IP アドレスに置き換えてください。

1. Output と Document Management Client API オブジェクトを作成します。

   * デフォルトのコンストラクターを使用して、`OutputServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して、`OutputServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を指定する文字列値を Forms サービスに渡します（例：`http://localhost:8080/soap/services/OutputService?blob=mtom`）。`lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。
   * `OutputServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` フィールドを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `OutputServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `OutputServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
   * フィールド `BasicHttpBindingSecurity.Security.Mode` に定数値 `BasicHttpSecurityMode.TransportCredentialOnly` を割り当てます。

   >[!NOTE]
   >
   >`DocumentManagementServiceClient` サービスクライアントに対してこれらの手順を繰り返します。

1. コンテンツサービス（非推奨）からフォームデザインを取得します。

   `DocumentManagementServiceClient` オブジェクトの `retrieveContent` メソッドを呼び出し、以下の値を渡してコンテンツを取得します。

   * コンテンツの追加先となるストアを指定する文字列値です。デフォルトのストアは `SpacesStore` です。この値は必須パラメーターです。
   * 取得するコンテンツの完全修飾パスを指定する文字列値（例：`/Company Home/Form Designs/Loan.xdp`）。この値は必須パラメーターです。
   * バージョンを指定する文字列値。この値はオプションのパラメーターであり、空の文字列を渡すことができます。この場合、最新バージョンが取得されます。
   * 参照リンクの値を格納する文字列出力パラメーター。
   * コンテンツを格納する `BLOB` 出力パラメーター。この出力パラメーターを使用して、コンテンツを取得できます。
   * コンテンツ属性を格納する `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` 出力パラメーター。
   * `CRCResult` 出力パラメーター。このオブジェクトを使用する代わりに、`BLOB` 出力パラメーターを使用してコンテンツを取得できます。

1. 非インタラクティブ PDF フォームをレンダリング

   `OutputServiceClient` オブジェクトの `generatePDFOutput2` メソッドを呼び出して、次の値を渡します。

   * `TransformationFormat` 列挙値。PDF ドキュメントを生成するには、`TransformationFormat.PDF` を指定します。
   * 画像などの追加リソースが存在するコンテンツルートを指定する文字列値。
   * フォームデザインを表す `BLOB` オブジェクト（コンテンツサービス（非推奨）から返された `BLOB` インスタンスを使用）。
   * PDF 実行時オプションを含む `PDFOutputOptionsSpec` オブジェクト。
   * レンダリング実行時オプションを含む `RenderOptionsSpec` オブジェクト。
   * フォームデザインと結合するデータを含む XML データソースを含む `BLOB` オブジェクト。
   * `generatePDFOutput2` メソッドによって入力される出力 `BLOB` オブジェクト。`generatePDFOutput2` メソッドは、ドキュメントを説明する生成されたメタデータをこのオブジェクトに入力します（このパラメーター値は、web サービスの呼び出しにのみ必要です）。
   * 操作の結果を含む出力 `OutputResult` オブジェクトです。（このパラメーター値は、web サービスの呼び出しにのみ必要です）。

   `generatePDFOutput2` メソッドは、非インタラクティブ PDF フォームを含む `BLOB` オブジェクトを返します。

1. フォームデータストリームを使用してアクションを実行します。

   * コンストラクターを呼び出して `System.IO.FileStream` オブジェクトを作成します。インタラクティブ PDF ドキュメントのファイルの場所と、ファイルを開くモードを表す文字列値を渡します。
   * `generatePDFOutput2` メソッドから取得した `BLOB` オブジェクトのコンテンツを格納するバイト配列を作成します。`BLOB` オブジェクトの `MTOM` データメンバーの値を取得して、バイト配列に格納します。
   * コンストラクターを使用して `System.IO.BinaryWriter` オブジェクトを渡すことによって、`System.IO.FileStream` オブジェクトを作成します。
   * `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを呼び出して、バイト配列を渡すことによって、バイト配列の内容を PDF ファイルに書き込みます。

**関連トピック：**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## リポジトリ内のドキュメントを Output サービスに渡す {#passing-documents-located-in-the-repository-to-the-output-service}

Output サービスは、通常 XDP ファイルとして保存され、Designer で作成されたフォームデザインに基づく、非インタラクティブな PDF フォームを処理します。フォームデザインを含む `com.adobe.idp.Document` オブジェクトを Output サービスに渡すことができます。次に、Output サービスは `com.adobe.idp.Document` オブジェクトにあるフォームデザインを処理します。

`com.adobe.idp.Document` オブジェクトを Output サービスに渡すことの利点は、他の AEM Forms サービス操作が `com.adobe.idp.Document` インスタンスを返すことです。すなわち、別のサービス操作から `com.adobe.idp.Document` インスタンスを取得し、それを処理できます。例えば、以下の図に示すように、XDP ファイルが AEM Forms リポジトリに格納されているとします。

![pd_pd_formrepository](assets/pd_pd_formrepository.png)

*FormsFolder* フォルダーは、AEM Forms リポジトリ内のユーザー定義の場所です（この場所は例であり、デフォルトでは存在しません）。この例では、Loan.xdp という名前のフォームデザインがこのフォルダー内にあります。フォームデザインに加えて、フォーム作成に使用する他のファイル（画像など）もこの場所に保存できます。AEM Forms リポジトリにあるリソースへのパスは次のとおりです。

`Applications/Application-name/Application-version/Folder.../Filename`

プログラムで AEM Forms リポジトリから Loan.xdp を取得し、それを `com.adobe.idp.Document` オブジェクト内の Output サービスに渡すことができます。

2 つの方法のいずれかを使用して、リポジトリにある XDP ファイルに基づいて PDF を作成できます。XDP の場所は、参照によって渡すことも、プログラムによってリポジトリから XDP を取得し、XDP ファイル内で Output サービスに渡すこともできます。

[クイックスタート（EJB モード）：Java API を使用してアプリケーション XDP ファイルに基づいて PDF ドキュメントを作成します](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api)（XDP ファイルの場所を参照で渡す方法を示します）。

[クイックスタート（EJB モード）：Java API を使用して AEM Forms リポジトリにあるドキュメントを Output サービスに渡します](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api)（プログラムで AEM Forms リポジトリから XDP ファイルを取得し、`com.adobe.idp.Document` インスタンス内の Output サービスに渡す方法を示します）。（このセクションでは、このタスクの実行方法について説明します）。

>[!NOTE]
>
>Forms サービスについて詳しくは、[AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary_of_steps-3}

AEM Forms リポジトリから取得したドキュメントを Output サービスに渡すには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Output と Document Management Client API オブジェクトを作成します。
1. AEM Forms リポジトリからフォームデザインを取得します。
1. 非インタラクティブ PDF フォームをレンダリング
1. データストリームでアクションを実行します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを含めます。

**Output と Document Management Client API オブジェクトの作成**

プログラムで Output service API 操作を実行する前に、Output Client API オブジェクトを作成します。また、このワークフローはコンテンツサービス（非推奨）から XDP ファイルを取得するため、Document Management API オブジェクトを作成します。

**AEM Forms リポジトリからフォームデザインを取得する**

Repository API を使用して、AEM Forms リポジトリから XDP ファイルを取得します（[リソースの読み取り](/help/forms/developing/aem-forms-repository.md#reading-resources)を参照。）

XDP ファイルは、`com.adobe.idp.Document` インスタンス（または web サービスを使用している場合は `BLOB` インスタンス）内で返されます。その後、`com.adobe.idp.Document` インスタンスを Output サービスに渡すことができます。

**非インタラクティブ PDF フォームのレンダリング**

非インタラクティブフォームをレンダリングするには、AEM Forms Repository API を使用して返された `com.adobe.idp.Document` インスタンスを渡します。

>[!NOTE]
>
>`generatePDFOutput2` および `generatePrintedOutput2` という名前の 2 つの新しいメソッドは、フォームデザインを含む `com.adobe.idp.Document` オブジェクトを受け入れます。また、ネットワークプリンターに印刷ストリームを送信する際に、フォームデザインを含む `com.adobe.idp.Document` を Output サービスに渡すこともできます。

**フォームデータストリームを使用してアクションを実行する**

非インタラクティブフォームは、PDF ファイルとして保存できます。フォームは、Adobe Reader または Acrobat で表示できます。

**関連トピック**

[Java API を使用して、リポジトリにあるドキュメントを Output サービスに渡す](creating-document-output-streams.md#pass-documents-located-in-the-repository-to-the-output-service-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Output Service API のクイックスタート](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

ResourceRepositoryClient

### Java API を使用して、リポジトリにあるドキュメントを Output サービスに渡す {#pass-documents-located-in-the-repository-to-the-output-service-using-the-java-api}

Output サービスと Repository API（Java）を使用して、リポジトリから取得したドキュメントを渡します。

1. プロジェクトファイルを含めます。

   adobe-output-client.jar や adobe-repository-client.jar などのクライアント JAR ファイルを、Java プロジェクトのクラスパスに含めます。

1. Output と Document Management Client API オブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。（[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照）
   * コンストラクターを使用して `ServiceClientFactory` オブジェクトを渡すことによって、`OutputClient` オブジェクトを作成します。
   * コンストラクターを使用して `ServiceClientFactory` オブジェクトを渡すことにより、`DocumentManagementServiceClientImpl` オブジェクトを作成します。

1. AEM Forms リポジトリからフォームデザインを取得します。

   `ResourceRepositoryClient` オブジェクトの `readResourceContent` メソッドを呼び出し、URI の場所を指定する文字列値を XDP ファイルに渡します。例えば、`/Applications/FormsApplication/1.0/FormsFolder/Loan.xdp` のようになります。この値は必須ではありません。このメソッドは、XDP ファイルを表す `com.adobe.idp.Document` インスタンスを返します。

1. 非インタラクティブ PDF フォームをレンダリング

   `OutputClient` オブジェクトの `generatePDFOutput2` メソッドを呼び出して、次の値を渡します。

   * `TransformationFormat` 列挙値。PDF ドキュメントを生成するには、`TransformationFormat.PDF` を指定します。
   * 画像などの追加リソースが配置されているコンテンツルートを指定する文字列値。例：`repository:///Applications/FormsApplication/1.0/FormsFolder/`。
   * フォームデザインを表す `com.adobe.idp.Document` オブジェクト（`ResourceRepositoryClient` オブジェクトの `readResourceContent` メソッドが返すインスタンスを使用）。
   * PDF 実行時オプションを含む `PDFOutputOptionsSpec` オブジェクト。
   * レンダリング実行時オプションを含む `RenderOptionsSpec` オブジェクト。
   * フォームデザインと結合するデータを含む XML データソースを含む `com.adobe.idp.Document` オブジェクト。

   `generatePDFOutput2` メソッドは、操作の結果を含む `OutputResult` オブジェクトを返します。

1. フォームデータストリームを使用してアクションを実行します。

   * `OutputResult` オブジェクトの `getGeneratedDoc` メソッドを呼び出して、非インタラクティブフォームを表す `com.adobe.idp.Document` オブジェクトを取得します。
   * 操作の結果を含む `java.io.File` オブジェクトを作成します。ファイル名の拡張子が .pdf であることを確認します。
   * `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを呼び出して、`com.adobe.idp.Document` オブジェクトの内容をファイルにコピーします（`getGeneratedDoc` が返した `com.adobe.idp.Document` オブジェクトを使用していることを確認します）。

**関連情報**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[クイックスタート（EJB モード）：Java API を使用して AEM Forms リポジトリ内のドキュメントを Output サービスに渡す](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api)

[AEM Forms Java ライブラリファイルの組み込み](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## フラグメントを使用した PDF ドキュメントの作成 {#creating-pdf-documents-using-fragments}

Output サービスと Assembler サービスを使用して、フラグメントに基づいた出力ストリーム（PDF ドキュメントなど）を作成できます。Assembler サービスは、複数の XDP ファイル内に配置されたフラグメントに基づく XDP ドキュメントを組み立てます。組み立てられた XDP ドキュメントが Output サービスに渡されて、PDF ドキュメントが作成されます。このワークフローでは、PDF ドキュメントが生成される様子が示されていますが、Output サービスでは、このワークフローに対して ZPL などの他の出力タイプも生成できます。PDF ドキュメントは、説明目的でのみ使用されています。

次の図は、このワークフローを示しています。

![cp_cp_outputassemblefragments](assets/cp_cp_outputassemblefragments.png)

*フラグメントを使用した PDF ドキュメントの作成*&#x200B;を読む前に、Assembler サービスを使用して複数の XDP ドキュメントを作成する方法を理解しておくことをお勧めします。詳しくは、[複数の XDP フラグメントの作成](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments)を参照してください。

>[!NOTE]
>
>また、Assembler サービスで作成されたフォームデザインを、Output サービスではなく Forms サービスに渡すこともできます。Output サービスと Forms サービスの主な違いは、Forms サービスがインタラクティブな PDF ドキュメントを生成し、Output サービスが非インタラクティブな PDF ドキュメントを生成する点です。また、Forms サービスは、ZPL などのプリンターベースの出力ストリームを生成できません。

>[!NOTE]
>
>Output サービスについて詳しくは、[AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary_of_steps-4}

フラグメントに基づいて PDF ドキュメントを作成するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Output および Assembler クライアントオブジェクトを作成します。
1. フォームデザインを生成するには、Assembler サービスを使用します。
1. Output サービスを使用して PDF ドキュメントを生成します。
1. PDF ドキュメントを PDF ファイルとして保存します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、必ずプロキシファイルを含めてください。

**Output および Assembler クライアントオブジェクトの作成**

プログラムで Output サービス API 操作を実行する前に、Output クライアント API オブジェクトを作成します。また、このワークフローは Assembler サービスを呼び出してフォームデザインを作成するため、Asembler クライアント API オブジェクトを作成します。

**Assembler サービスを使用してフォームデザインを生成する**

Assembler サービスを使用して、フラグメントに基づくフォームデザインを生成します。Assembler サービスは、フォームデザインを含んだ `com.adobe.idp.Document` インスタンスを返します。

**Output サービスを使用して PDF ドキュメントを生成**

Output サービスを使用して、Assembler サービスで作成されたフォームデザインに基づく PDF ドキュメントを生成できます。Assembler サービスから返された `com.adobe.idp.Document` インスタンスを Output サービスに渡します。

**PDF ドキュメントを PDF ファイルとして保存**

Output サービスが PDF ドキュメントを生成したら、それを PDF ファイルとして保存できます。

**関連トピック**

[Java API を使用してフラグメントに基づく PDF ドキュメントを作成する](creating-document-output-streams.md#create-a-pdf-document-based-on-fragments-using-the-java-api)

[Web サービス API を使用し、フラグメントに基づいて PDF ドキュメントを作成します](creating-document-output-streams.md#create-a-pdf-document-based-on-fragments-using-the-web-service-api)

[AEM Forms Java ライブラリファイルの組み込み](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Output Service API のクイックスタート](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

[複数の XDP フラグメントのアセンブル](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments)

[PDF ドキュメントの作成](creating-document-output-streams.md#creating-pdf-documents)

### Java API を使用してフラグメントに基づく PDF ドキュメントを作成する {#create-a-pdf-document-based-on-fragments-using-the-java-api}

Output サービス API と Assembler サービス API（Java）を使用して、フラグメントに基いた PDF ドキュメントを作成します。

1. プロジェクトファイルを含めます。

   adobe-output-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. Output および Assembler クライアントオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して `ServiceClientFactory` オブジェクトを渡すことにより、`OutputClient` オブジェクトを作成します。
   * コンストラクターを使用して `ServiceClientFactory` オブジェクトを渡すことにより、`AssemblerServiceClient` オブジェクトを作成します。

1. フォームデザインを生成するには、Assembler サービスを使用します。

   `AssemblerServiceClient` オブジェクトの `invokeDDX` メソッドを呼び出し、次の必要な値を渡します。

   * 使用する DDX ドキュメントを表す `com.adobe.idp.Document` オブジェクト。
   * 入力 XDP ファイルを含む `java.util.Map` オブジェクト。
   * デフォルトのフォントやジョブのログレベルなどの実行時オプションを指定する `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` オブジェクト。

   `invokeDDX` メソッドは、アセンブルされた XDP ドキュメントを含んだ `com.adobe.livecycle.assembler.client.AssemblerResult` オブジェクトを返します。アセンブルされた XDP ドキュメントを取得するには、次のアクションを実行します。

   * `AssemblerResult` オブジェクトの `getDocuments` メソッドを呼び出します。このメソッドは、`java.util.Map` オブジェクトを返します。
   * 結果の `com.adobe.idp.Document` オブジェクトが見つかるまで、`java.util.Map` オブジェクトを反復処理します。
   * `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッド呼び出して、アセンブルされた XDP ドキュメントを抽出します。


1. Output サービスを使用して PDF ドキュメントを生成します。

   `OutputClient` オブジェクトの `generatePDFOutput2` メソッドをを呼び出して、次の値を渡します。

   * `TransformationFormat` 列挙値。PDF ドキュメントを生成するには、`TransformationFormat.PDF` を指定します。
   * 画像などの追加リソースが存在しているコンテンツルートを指定する文字列値
   * フォームデザインを表す `com.adobe.idp.Document` オブジェクト（Assembler サービスが返すインスタンスを使用）
   * PDF 実行時オプションを含んだ `PDFOutputOptionsSpec` オブジェクト
   * レンダリング実行時オプションを含んだ `RenderOptionsSpec` オブジェクト
   * フォームデザインと結合するデータが格納されている XML データソースを含んだ `com.adobe.idp.Document` オブジェクト

   `generatePDFOutput2` メソッドは、操作の結果を含む `OutputResult` オブジェクトを返します。

1. PDF ドキュメントを PDF ファイルとして保存します。

   * `OutputResult` オブジェクトの `getGeneratedDoc` メソッドを呼び出して、PDF ドキュメントを表す `com.adobe.idp.Document` オブジェクトを取得します。 
   * 操作の結果を含む `java.io.File` オブジェクトを作成します。ファイル名の拡張子が .pdf であることを確認します。
   * `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを呼び出して、`com.adobe.idp.Document` オブジェクトの内容をファイルにコピーします。（必ず `getGeneratedDoc` メソッドが返した `com.adobe.idp.Document` オブジェクトを使用します）。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[クイックスタート（EJB モード）：Java API を使用して、フラグメントに基づく PDF ドキュメントを作成](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[クイックスタート（SOAP モード）：Java API を使用して、フラグメントに基づく PDF ドキュメントを作成](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

### Web サービス API を使用し、フラグメントに基づいて PDF ドキュメントを作成します {#create-a-pdf-document-based-on-fragments-using-the-web-service-api}

Output サービス API と Assembler サービス API（web サービス）を使用し、フラグメントに基づいて PDF ドキュメントを作成します。

1. プロジェクトファイルを含めます。

   MTOM を使用する Microsoft .NET プロジェクトを作成します。Output サービスに関連付けられたサービス参照に、次の WSDL 定義を使用します。

   ```java
    http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1.
   ```

   Assembler サービスに関連付けられたサービス参照に対して、次の WSDL 定義を使用します。

   ```java
    http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   `BLOB` データ型は両方のサービス参照に共通なので、これを使用すると `BLOB` データ型が完全に修飾されます。対応する web サービスのクイックスタートでは、すべての `BLOB` インスタンスが完全に修飾されています。

   >[!NOTE]
   >
   >`localhost` を、AEM Forms をホストするサーバーの IP アドレスに置換します。

1. Output および Assembler クライアントオブジェクトを作成します。

   * デフォルトのコンストラクタを使用して、`OutputServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して、`OutputServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/OutputService?blob=mtom`）。`lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。ただし、`?blob=mtom` を指定して MTOM を使用します。
   * `OutputServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` フィールドを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * AEM Forms のユーザー名を `OutputServiceClient.ClientCredentials.UserName.UserName` フィールドに割り当てます。
      * 対応するパスワード値を `OutputServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を `BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
   * `BasicHttpSecurityMode.TransportCredentialOnly` 定数値を `BasicHttpBindingSecurity.Security.Mode` フィールドに割り当てます。

   >[!NOTE]
   >
   >`AssemblerServiceClient` オブジェクトに対してこれらの手順を繰り返します。

1. フォームデザインを生成するには、Assembler サービスを使用します。

   `AssemblerServiceClient` オブジェクトの `invokeDDX` メソッドを呼び出して、次の値を渡します。

   * DDX ドキュメントを表す `BLOB` オブジェクト
   * 必要なファイルを含む `MyMapOf_xsd_string_To_xsd_anyType` オブジェクト
   * 実行時のオプションを指定する `AssemblerOptionSpec` オブジェクト

   `invokeDDX` メソッドは、ジョブの結果と発生した例外を含む `AssemblerResult` オブジェクトを返します。新しく作成した XDP ドキュメントを取得するには、次の操作を実行します。

   * `AssemblerResult` オブジェクトの `documents` フィールドにアクセスします。これは、生成された PDF ドキュメントを含む `Map` オブジェクトです。
   * `Map` オブジェクトを繰り返して、アセンブルされたフォームデザインを取得します。その配列メンバーの `value` を `BLOB` にキャストします。この `BLOB` インスタンスを Output サービスに渡します。


1. Output サービスを使用して PDF ドキュメントを生成します。

   `OutputServiceClient` オブジェクトの `generatePDFOutput2` メソッドをを呼び出して、次の値を渡します。

   * `TransformationFormat` 列挙値。PDF ドキュメントを生成するには、`TransformationFormat.PDF` を指定します。
   * 画像などその他のリソースが存在するコンテンツルートを指定する文字列値です。
   * フォームデザインを表す `BLOB` オブジェクトです（Assembler サービスによって返される `BLOB` インスタンスを使用します）。
   * PDF の実行時オプションを含む `PDFOutputOptionsSpec` オブジェクトです。
   * レンダリング実行時オプションを含む `RenderOptionsSpec` オブジェクト。
   * フォームデザインとマージするデータが含まれる XML データソースを持つ `BLOB` オブジェクトです。
   * `generatePDFOutput2` メソッドがデータを設定する出力 `BLOB` オブジェクトです。`generatePDFOutput2` メソッドは、ドキュメントを表す生成されたメタデータをこのオブジェクトに設定します。（このパラメーター値は、web サービスの呼び出しにのみ必要です）。
   * 操作の結果を含む出力 `OutputResult` オブジェクトです。（このパラメーター値は、web サービスの呼び出しにのみ必要です）。

   `generatePDFOutput2` メソッドは、非インタラクティブ PDF フォームを含む `BLOB` オブジェクトを返します。

1. PDF ドキュメントを PDF ファイルとして保存します。

   * コンストラクタを呼び出して `System.IO.FileStream` オブジェクトを作成します。インタラクティブ PDF ドキュメントのファイルの場所と、ファイルを開くモードを表す文字列値を渡します。
   * `generatePDFOutput2` メソッドから取得した `BLOB` オブジェクトのコンテンツを格納するバイト配列を作成します。`BLOB` オブジェクトの `MTOM` データメンバーの値を取得して、バイト配列に格納します。
   * コンストラクターを使用して `System.IO.BinaryWriter` オブジェクトを渡すことによって、`System.IO.FileStream` オブジェクトを作成します。
   * `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを呼び出して、バイト配列を渡すことによって、バイト配列の内容を PDF ファイルに書き込みます。

**関連トピック：**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## ファイルへの印刷 {#printing-to-files}

Output サービスを使用すると、PostScript、PCL（Printer Control Language）または次のラベル形式などのストリームをファイルに印刷できます。

* ゼブラ — ZPL
* Intermec - IPL
* Datamax - DPL
* 東芝 — TPCL

Output サービスを使用すると、XML データをフォームデザインと結合し、フォームをファイルに印刷できます。次の図に、レーザーファイルとラベルファイルを作成する Output サービスを示します。

>[!NOTE]
>
>プリンターに印刷ストリームを送信する方法については、[プリンタへの印刷ストリームの送信](creating-document-output-streams.md#sending-print-streams-to-printers)を参照してください。

>[!NOTE]
>
>Output サービスについて詳しくは、[AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary_of_steps-5}

ファイルに印刷するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Output クライアントオブジェクトを作成します。
1. XML データソースを参照します。
1. ファイルへの印刷に必要な印刷実行時オプションを設定します。
1. 印刷ストリームをファイルに印刷します。
1. 操作の結果を取得します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、必ずプロキシファイルを含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar（AEM Forms が JBoss にデプロイされている場合に必要）
* jbossall-client.jar（AEM Formsが JBoss にデプロイされている場合に必要）

AEM Forms が JBoss 以外のサポート対象の J2EE アプリケーションサーバーにデプロイされている場合は、adobe-utilities.jar ファイルと jbossall-client.jar ファイルを、AEM Forms がデプロイされている J2EE アプリケーションサーバーに固有の JAR ファイルに置き換える必要があります。（[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照。）

**Output クライアントオブジェクトの作成**

プログラムで Output サービスの操作を実行する前に、Output サービスのクライアントオブジェクトを作成する必要があります。Java API を使用している場合は、`OutputClient` オブジェクトを作成します。Output web サービス API を使用している場合は、`OutputServiceService` オブジェクトを作成します。

**XML データソースの参照**

データを含むドキュメントを印刷するには、データを入力するすべてのフォームフィールドの XML 要素を含む XML データソースを参照する必要があります。XML 要素名は、フィールド名と一致する必要があります。XML 要素がフォームフィールドに対応していない場合や、XML 要素名がフィールド名と一致しない場合、XML 要素は無視されます。すべての XML 要素が指定されている場合、XML 要素の表示順序を一致させる必要はありません。

**ファイルへの印刷に必要な印刷実行時オプションの設定**

ファイルに印刷するには、Output サービスが印刷するファイルの場所と名前を指定して、「ファイル URI 実行時」オプションを設定する必要があります。例えば、*MortgageForm.ps* という名前の PostScript ファイルを C:\Adobe に印刷するよう Output サービスに指示するには、C:\Adobe\MortgageForm.ps を指定します。

>[!NOTE]
>
>定義できる実行時オプションがあります。設定できるすべてのオプションについては、[AEM Forms API リファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)の `PrintedOutputOptionsSpec` クラスリファレンスを参照してください。

**印刷ストリームをファイルに印刷**

フォームデータを含む有効な XML データソースを参照し、印刷の実行時オプションを設定した後、Output サービスを呼び出して、ファイルを印刷できます。

**操作の結果の取得**

Output サービスは操作を実行した後、XML データなど、操作が成功したかどうかを示す様々なデータ項目を返します。

**関連トピック**

[Java API を使用したファイルへの印刷](creating-document-output-streams.md#print-to-files-using-the-java-api)

[Web サービス API を使用したファイルへの印刷](creating-document-output-streams.md#print-to-files-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Output Service API のクイックスタート](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Java API を使用したファイルへの印刷 {#print-to-files-using-the-java-api}

Output API（Java） を使用してファイルに印刷します。

1. プロジェクトファイルを含めます。

   adobe-output-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. Output クライアントオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して `ServiceClientFactory` オブジェクトを渡すことにより、`OutputClient` オブジェクトを作成します。

1. XML データソースを参照します。

   * コンストラクターを使用し、XML ファイルの場所を指定する文字列値を渡すことにより、ドキュメントにデータを入力するために使用される XML データソースを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクターを使用して `java.io.FileInputStream` オブジェクトを渡すことにより、`com.adobe.idp.Document` オブジェクトを作成します。

1. ファイルへの印刷に必要な印刷実行時オプションを設定します。

   * コンストラクターを使用して `PrintedOutputOptionsSpec` オブジェクトを作成します。
   * PrintedOutputOptionsSpec オブジェクトの `setFileURI` メソッドを呼び出し、ファイルの名前と場所を表す文字列値を渡すことにより、ファイルを指定します。例えば、Output サービスを C:\Adobe にある MortgageForm.ps という名前の PostScript ファイルに印刷する場合は、C:\\Adobe\MortgageForm.ps と指定します。
   * `PrintedOutputOptionsSpec` オブジェクトの `setCopies` メソッドを呼び出し、コピー数を表す整数値を渡すことにより、印刷する部数を指定します。

1. 印刷ストリームをファイルに印刷します。

   `OutputClient` オブジェクトの `generatePrintedOutput` メソッドを呼び出して、次の値を渡すことにより、ファイルに印刷します。

   * 作成する印刷ストリーム形式を指定する `PrintFormat` 列挙値。例えば、PostScript 印刷ストリームを作成するには、`PrintFormat.PostScript` を渡します。
   * フォームデザイン名を指定する文字列値。
   * 画像ファイルなど、関連する販促物ファイルの場所を指定する文字列値です。
   * 使用する XDC ファイルの場所を指定する文字列値（`PrintedOutputOptionsSpec` オブジェクトを使用して使用する XDC ファイルを指定した場合は、`null` を渡すことができます）。
   * ファイルに印刷するために必要な実行時オプションを含む `PrintedOutputOptionsSpec` オブジェクト。
   * フォームデータを含む XML データソースを含む `com.adobe.idp.Document` オブジェクト。

   この `generatePrintedOutput` メソッドは操作の結果を含む `OutputResult` オブジェクトを返します。

   >[!NOTE]
   >
   >この `OutputResult` オブジェクトの `getRecordLevelMetaDataList` メソッドは `null` を返します。

1. 操作の結果を取得します。

   * `OutputResult` オブジェクトの `getStatusDoc` メソッドを呼び出して、`generatePrintedOutput` メソッドのステータスを表す `com.adobe.idp.Document` オブジェクトを作成します（`OutputResult` オブジェクトは `generatePrintedOutput` メソッドによって返されました）。
   * 操作の結果を含む `java.io.File` オブジェクトを作成します。ファイル拡張子が XML であることを確認します。
   * `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを呼び出して、`com.adobe.idp.Document` オブジェクトの内容をファイルにコピーします（`getStatusDoc` メソッドによって返された `com.adobe.idp.Document` オブジェクトを使用してください）。

**関連情報**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[クイックスタート（SOAP モード）：Java API を使用したファイルへの印刷](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-printing-to-a-file-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)。

### Web サービス API を使用したファイルへの印刷 {#print-to-files-using-the-web-service-api}

Output API（web サービス）を使用してファイルに印刷します。

1. プロジェクトファイルを含めます。

   MTOM を使用する Microsoft .NET プロジェクトを作成します。WSDL 定義 `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1` を使用するようにします。

   >[!NOTE]
   >
   >`localhost` を、AEM Forms をホストするサーバーの IP アドレスで置換します。

1. Output クライアントオブジェクトを作成します。

   * デフォルトのコンストラクターを使用して、`OutputServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して、`OutputServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/OutputService?blob=mtom`）。`lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。ただし、`?blob=mtom` を指定して MTOM を使用します。
   * `OutputServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` フィールドを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `OutputServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `OutputServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
      * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` を`BasicHttpBindingSecurity.Security.Mode` フィールドに割り当てます。

1. XML データソースを参照します。

   * コンストラクターを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、フォームデータの保存に使用されます。
   * `System.IO.FileStream` オブジェクトを作成するには、そのコンストラクターを呼び出し、フォームデータを含む XML ファイルの場所を指定する文字列値を渡します。
   * `System.IO.FileStream` オブジェクトの内容を格納するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することで、バイト配列のサイズを決定できます。
   * バイト配列にストリームデータを入力するには、`System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出し、バイト配列、開始位置、読み取るストリーム長を渡します。
   * `binaryData` プロパティを割り当てて、`BLOB` オブジェクトにバイト配列の内容を入力します。

1. ファイルへの印刷に必要な印刷実行時オプションを設定します。

   * コンストラクターを使用して `PrintedOutputOptionsSpec` オブジェクトを作成します。
   * `PrintedOutputOptionsSpec` オブジェクトの `fileURI` データメンバーにファイルを指定するには、ファイルの場所と名前を表す文字列を入力します。例えば、Output サービスを PostScript ファイル（C:\Adobe にある *MortgageForm.ps*）に印刷する場合は、C:\\Adobe\MortgageForm.ps と指定します。
   * 印刷部数を指定するには、`PrintedOutputOptionsSpec` オブジェクトの `copies` データメンバーに印刷部数を表す整数値を入力します。

1. 印刷ストリームをファイルに印刷します。

   `OutputServiceService` オブジェクトの `generatePrintedOutput` メソッドを呼び出して、次の値を渡すことにより、ファイルに印刷します。

   * 作成する印刷ストリーム形式を指定する `PrintFormat` 列挙値。例えば、PostScript 印刷ストリームを作成するには、`PrintFormat.PostScript` を渡します。
   * フォームデザイン名を指定する文字列値。
   * 画像ファイルなど、関連する販促物ファイルの場所を指定する文字列値です。
   * 使用する XDC ファイルの場所を指定する文字列値（`PrintedOutputOptionsSpec` オブジェクトを使用して使用する XDC ファイルを指定した場合は、`null` を渡すことができます）。
   * ファイルに印刷するために必要な印刷実行時オプションを含む `PrintedOutputOptionsSpec` オブジェクト。
   * フォームデータを含む XML データソースを含む `BLOB` オブジェクト。
   * `generatePDFOutput` メソッドによって入力される `BLOB` オブジェクト。この `generatePDFOutput` メソッドは、ドキュメントを説明する生成されたメタデータをこのオブジェクトに入力します。（このパラメーター値は、web サービスの呼び出しにのみ必要です）。
   * `generatePDFOutput` メソッドによって入力される `BLOB` オブジェクト。この `generatePDFOutput` メソッドは、このオブジェクトに結果データを入力します。（このパラメーター値は、web サービスの呼び出しにのみ必要です）。
   * 操作の結果を含める `OutputResult` オブジェクト。（このパラメーター値は、web サービスの呼び出しにのみ必要です）。

1. 操作の結果を取得します。

   * `System.IO.FileStream` オブジェクトを作成し、そのコンストラクターを呼び出して、結果データを含む XML ファイルの場所を表す文字列値を渡します。ファイル拡張子が XML であることを確認します。
   * `OutputServiceService` オブジェクトの `generatePDFOutput` メソッド（8 番目のパラメーター）によって結果データが入力された `BLOB` オブジェクトのデータコンテンツを格納するバイト配列を作成します。`BLOB` オブジェクトの `MTOM` データメンバーの値を取得して、バイト配列にデータを入力します。
   * コンストラクターを呼び出して `System.IO.FileStream` オブジェクトを渡すことによって、`System.IO.BinaryWriter` オブジェクトを作成します。
   * バイト配列の内容を XML ファイルに書き込むには、`System.IO.BinaryWriter` オブジェクトの `Write` メソッドを呼び出して、バイト配列を渡します。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## プリンターへの印刷ストリームの送信 {#sending-print-streams-to-printers}

出力サービスを使用すると、PostScript、PCL（Printer Control Language）または次のラベル形式などのプリントストリームをネットワークプリンターに送信できます。

* ゼブラ — ZPL
* Intermec - IPL
* Datamax - DPL
* 東芝 — TPCL

Output サービスを使用すると、XML データをフォームデザインと結合し、フォームをプリントストリームとして出力できます。例えば、PostScript プリントストリームを作成して、ネットワークプリンターに送信できます。次の図は、プリントストリームをネットワークプリンターに送信する Output サービスを示しています。

>[!NOTE]
>
>プリントストリームをネットワークプリンターに送信する方法を示すために、このセクションでは、SharedPrinter プリンタープロトコルを使用して PostScript プリントストリームをネットワークプリンターに送信します。

>[!NOTE]
>
>Output サービスの詳細については、「[AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)」を参照してください。

### 手順の概要 {#summary_of_steps-6}

プリントストリームをネットワークプリンターに送信するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. Output クライアントオブジェクトを作成します。
1. XML データソースを参照します。
1. 印刷実行時オプションの設定
1. 印刷するドキュメントを取得します。
1. ドキュメントをネットワークプリンターに送信します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、必ずプロキシファイルを含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar（AEM Forms を JBoss にデプロイする場合に必要）
* jbossall-client.jar（AEM Forms が JBoss にデプロイされている場合に必要）

AEM Forms が JBoss 以外のサポート対象の J2EE アプリケーションサーバーにデプロイされている場合は、adobe-utilities.jar ファイルと jbossall-client.jar ファイルを、AEM Forms がデプロイされている J2EE アプリケーションサーバーに固有の JAR ファイルに置き換える必要があります。

**Output クライアントオブジェクトの作成**

Output サービスの操作をプログラム的に実行する前に、Output サービスのクライアントオブジェクトを作成します。Java API を使用する場合は、`OutputClient` オブジェクトを作成します。Output web サービス API を使用している場合は、`OutputServiceClient` オブジェクトを作成します。

**XML データソースの参照**

データを含むドキュメントを印刷するには、データを入力するすべてのフォームフィールドの XML 要素を含む XML データソースを参照する必要があります。XML 要素名は、フィールド名と一致する必要があります。XML 要素がフォームフィールドに対応していない場合や、XML 要素名がフィールド名と一致しない場合、XML 要素は無視されます。すべての XML 要素が指定されている場合、XML 要素の表示順序を一致させる必要はありません。

**印刷実行時オプションを設定する**

印刷ストリームをプリンターに送信する際に、次のオプションを含む実行時のオプションを設定できます。

* **コピー**：プリンターに送信する部数を指定します。デフォルト値は 1 です。
* **ホチキス止め**：ステープル印刷が使用されると、XCI オプションが設定されます。このオプションは、構成モデルにおいてステープル要素で指定することができ、PS および PCL プリンターにのみ使用されます。
* **OutputJog**：XCI オプションは、出力ページを（出力トレイで物理的にシフトした）ジョグ付けする場合に設定されます。このオプションは、PS および PCL プリンター専用です。
* **OutputBin**：プリントドライバーが適切な出力ビンを選択するために使用する XCI 値です。

>[!NOTE]
>
>設定可能なすべてのランタイムオプションについては、`PrintedOutputOptionsSpec` クラスのリファレンスを参照してください。

**印刷するドキュメントを取得する**。

プリンターに送信する印刷ストリームを取得します。たとえば、PostScript ファイルを取り出して、プリンターに送信することができます。

プリンターが PDF に対応している場合は、PDF ファイルの送信を選択することができます。しかし、PDF ドキュメントをプリンターに送信する場合、プリンターメーカーごとに PDF インタープリターの実装が異なるという問題があります。つまり、印刷メーカーによっては、Adobe PDF の解釈を採用しているところもありますが、プリンターによって異なります。他のプリンターには、独自の PDF インタープリターがあります。その結果、印刷の出来が異なる場合があります。

プリンターに PDF ドキュメントを送信するもう 1 つの制限は、単純に印刷することです。両面印刷、用紙トレイの選択、ホチキス止めは、プリンターの設定を使用しない限り使用できません。

印刷するドキュメントを取得するには、`generatePrintedOutput` メソッドを使用します。次の表は `generatePrintedOutput` メソッドを使用する際、指定した印刷ストリーミング用に設定されるコンテンツタイプを決定します。

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
   <td><p>デフォルトまたはカスタムの xdc 出力ストリームで dpl203.xdc を作成します。</p></td>
  </tr>
  <tr>
   <td><p>DPL300DPI </p></td>
   <td><p>DPL 300 DPI 出力ストリームを作成します。</p></td>
  </tr>
  <tr>
   <td><p>DPL406DPI </p></td>
   <td><p>DPL 400 DPI 出力ストリームを作成します。</p></td>
  </tr>
  <tr>
   <td><p>DPL600DPI </p></td>
   <td><p>DPL 600 DPI 出力ストリームを作成します。</p></td>
  </tr>
  <tr>
   <td><p>GenericColorPCL </p></td>
   <td><p>Generic Color PCL（5c）出力ストリームを作成します。</p></td>
  </tr>
  <tr>
   <td><p>GenericPSLevel3 </p></td>
   <td><p>汎用 PostScript レベル 3 出力ストリームを作成します。</p></td>
  </tr>
  <tr>
   <td><p>IPL </p></td>
   <td><p>カスタム IPL 出力ストリームを作成します。</p></td>
  </tr>
  <tr>
   <td><p>IPL300DPI </p></td>
   <td><p>IPL 300 DPI 出力ストリームを作成します。</p></td>
  </tr>
  <tr>
   <td><p>IPL400DPI </p></td>
   <td><p>IPL 400 DPI 出力ストリームを作成します。</p></td>
  </tr>
  <tr>
   <td><p>PCL </p></td>
   <td><p>Generic Monochrome PCL（5e）出力ストリームを作成します。</p></td>
  </tr>
  <tr>
   <td><p>PostScript </p></td>
   <td><p>汎用 PostScript レベル 2 出力ストリームを作成します。</p></td>
  </tr>
  <tr>
   <td><p>TPCL </p></td>
   <td><p>カスタム TPCL 出力ストリームを作成します。</p></td>
  </tr>
  <tr>
   <td><p>TPCL305DPI </p></td>
   <td><p>TPCL 305 DPI 出力ストリームを作成します。</p></td>
  </tr>
  <tr>
   <td><p>TPCL600DPI </p></td>
   <td><p>TPCL 600 DPI 出力ストリームを作成します。</p></td>
  </tr>
  <tr>
   <td><p>ZPL </p></td>
   <td><p>ZPL 203 DPI 出力ストリームを作成します。</p></td>
  </tr>
  <tr>
   <td><p>ZPL300DPI </p></td>
   <td><p>ZPL 300 DPI 出力ストリームを作成します。</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>また、 `generatePrintedOutput2` メソッドを使用して、プリンターに印刷ストリーミングを送ることもできます。ただし、「プリンターへの印刷ストリーミングの送信」セクションに関連するクイックスタートでは、 `generatePrintedOutput` メソッドを使用します。

**印刷ストリーミングをネットワークプリンターに送信**

印刷するドキュメントを取得した後、Output サービスを呼び出すと、印刷ストリーミングがネットワークプリンターに送信されます。Output サービスでプリンターを正常に見つけるには、印刷サーバーとプリンター名の両方を指定する必要があります。また、印刷プロトコルも指定する必要があります。

>[!NOTE]
>
>PDFG が Forms サーバーにインストールされ、そのサーバーが Windows Server 2008 で実行されている場合、SharedPrinter プロパティは使用できません。この場合は、別のプリンタープロトコルを使用します。

>[!NOTE]
>
>ネットワークプリンターを使用し、アクセスメカニズムが SharedPrinter の場合は、プリンターのネットワークパスを完全に指定する必要があります。Java API を使用して、ネットワークプリンターに印刷ストリーミングを送信します。

Output API（Java）を使用して、印刷ストリーミングをネットワークプリンターに送信します。

1. プロジェクトファイルを含めます。

   adobe-output-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. Output クライアントオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用し `ServiceClientFactory` オブジェクトを渡すことで、`OutputClient` オブジェクトを作成します。

1. XML データソースの参照

   * コンストラクタを使用し、XML ファイルの場所を指定する文字列値を渡すことによって、ドキュメントにデータを設定するのに使用される XML データソースを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクタを使用し、`java.io.FileInputStream` オブジェクトを渡すことによって、`com.adobe.idp.Document` オブジェクトを作成します。

1. 印刷実行時オプションの設定

   印刷実行時オプションを表す `PrintedOutputOptionsSpec` オブジェクトを作成します。例えば、`PrintedOutputOptionsSpec` オブジェクトの `setCopies` メソッドを呼び出すことによって、印刷する部数を指定することができます。

   >[!NOTE]
   >
   >ZPL 印刷ストリームを生成する場合、`PrintedOutputOptionsSpec` オブジェクトの `setPagination` メソッドを使用してページネーションの値を設定することはできません。同様に、ZPL 印刷ストリームに対して、OutputJog、PageOffset、Staple のオプションを設定することはできません。`setPagination` メソッドは PostScript の生成には無効です。PCL の生成にのみ有効です。

1. 印刷するドキュメントの取得

   * `OutputClient` オブジェクトの `generatePrintedOutput` メソッドを呼び出し、次の値を渡すことによって、印刷するドキュメントを取得します。

      * 印刷ストリームを指定する `PrintFormat` 列挙値。例えば、PostScript 印刷ストリームを作成するには、`PrintFormat.PostScript` を渡します。
      * フォームデザイン名を指定する文字列値。
      * 関連する販促物ファイル（画像ファイルなど）の場所を指定する文字列値です。
      * 使用する XDC ファイルの場所を指定する文字列値です。
      * ファイルに印刷するために必要な実行時オプションを含む `PrintedOutputOptionsSpec` オブジェクトです。
      * フォームデザインと統合するフォームデータが含まれる XML データソースを表す `com.adobe.idp.Document` オブジェクトです。

      このメソッドは、操作の結果を含む `OutputResult` オブジェクトを返します。

   * `OutputResult` オブジェクトの `getGeneratedDoc` メソッドを呼び出すことによって、プリンターに送信する `com.adobe.idp.Document` オブジェクトを作成します。このメソッドは、`com.adobe.idp.Document` オブジェクトを返します。


1. ネットワークプリンターへの印刷ストリームの送信

   `OutputClient` オブジェクトの `sendToPrinter` メソッドを呼び出し、次の値を渡すことによって、印刷ストリームをネットワークプリンターに送信します。

   * プリンターに送信する印刷ストリームを表す `com.adobe.idp.Document` オブジェクト。
   * 使用するプリンタープロトコルを指定する `PrinterProtocol` 列挙値。例えば、SharedPrinter プロトコルを指定するには、`PrinterProtocol.SharedPrinter` を渡します。
   * 印刷サーバーの名前を指定する文字列値です。例えば、印刷サーバーの名前が「PrintServer1」である場合、`\\\PrintSever1` を渡します。
   * プリンターの名前を指定する文字列値。例えば、プリンター名が「Printer1」の場合、`\\\PrintSever1\Printer1` を渡します。

   >[!NOTE]
   >
   >この `sendToPrinter` メソッドが AEM Forms API バージョン 8.2.1 に追加されました。

### Web サービス API を使用してプリンターに印刷ストリームを送信する {#send-a-print-stream-to-a-printer-using-the-web-service-api}

Output API（web サービス）を使用して、印刷ストリームをネットワークプリンターに送信します。

1. プロジェクトファイルを含めます。

   MTOM を使用する Microsoft .NET プロジェクトを作成します。WSDL 定義 `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1` を使用するようにします。

   >[!NOTE]
   >
   >`localhost` を、AEM Forms をホストするサーバーの IP アドレスで置換します。

1. Output クライアントオブジェクトを作成します。

   * デフォルトのコンストラクターを使用して、`OutputServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して、`OutputServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/OutputService?blob=mtom`）。`lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。ただし、`?blob=mtom` を指定して MTOM を使用します。
   * `OutputServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` フィールドを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `OutputServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `OutputServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
      * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` を`BasicHttpBindingSecurity.Security.Mode` フィールドに割り当てます。

1. XML データソースを参照します。

   * コンストラクターを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、フォームデータの保存に使用されます。
   * コンストラクターを呼び出して `System.IO.FileStream` オブジェクトを作成します。フォームデータを含む XML ファイルの場所を指定する文字列値を渡します。
   * `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得して、バイト配列の長さを決定します。
   * バイト配列にストリームデータを入力するには、`System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出し、バイト配列、開始位置、読み取るストリーム長を渡します。
   * `MTOM` フィールドを割り当てて、`BLOB` オブジェクトにバイト配列の内容を入力します。

1. 印刷実行時オプションを設定します。

   コンストラクターを使用して `PrintedOutputOptionsSpec` オブジェクトを作成します。例えば、`PrintedOutputOptionsSpec` オブジェクトの `copies` データメンバーに部数を表す整数値を割り当てることによって、印刷する部数を指定できます。

   >[!NOTE]
   >
   >ZPL 印刷ストリームを生成している場合、`PrintedOutputOptionsSpec` オブジェクトの `pagination` データメンバーを使用してページネーションの値を設定することはできません。同様に、ZPL 印刷ストリームに対して、OutputJog、PageOffset、Staple のオプションを設定することはできません。この `pagination` データメンバーは PostScript の生成に対して無効です。PCL の生成にのみ有効です。

1. 印刷するドキュメントを取得します。

   * 印刷するドキュメントを取得するには、`OutputServiceService` オブジェクトの `generatePrintedOutput` メソッドを呼び出し、次の値を渡します。

      * 印刷ストリームを指定する `PrintFormat` 列挙値。例えば、PostScript 印刷ストリームを作成するには、`PrintFormat.PostScript` を渡します。
      * フォームデザイン名を指定する文字列値。
      * 関連する販促物ファイル（画像ファイルなど）の場所を指定する文字列値です。
      * 使用する XDCファイルの場所を指定する文字列値。
      * ネットワークプリンターに印刷ストリームを送信する際に使用される印刷実行時のオプションを含む `PrintedOutputOptionsSpec` オブジェクト。
      * フォームデータを含んだ XML データソースを含む `BLOB` オブジェクト。
      * `generatePrintedOutput` メソッドによって入力される `BLOB` オブジェクト。この `generatePrintedOutput` メソッドは、ドキュメントを説明する生成されたメタデータをこのオブジェクトに入力します。（このパラメーター値は、web サービスの呼び出しにのみ必要です）。
      * `generatePrintedOutput` メソッドによって入力される `BLOB` オブジェクト。この `generatePrintedOutput` メソッドは、このオブジェクトに結果データを入力します。（このパラメーター値は、web サービスの呼び出しにのみ必要です）。
      * 操作の結果を含める `OutputResult` オブジェクト。（このパラメーター値は、web サービスの呼び出しにのみ必要です）。
   * `OutputResult` オブジェクトの `generatedDoc` メソッドの値を取得して、プリンターに送信する `BLOB` オブジェクトを作成します。このメソッドは、`generatePrintedOutput` メソッドによって返される PostScript データを含む `BLOB` オブジェクトを返します。


1. 印刷ストリームをネットワークプリンターに送信します。

   印刷ストリームをネットワークプリンターに送信するには、`OutputClient` オブジェクトの `sendToPrinter` メソッドを呼び出し、次の値を渡します。

   * プリンターに送信する印刷ストリームを表す `BLOB` オブジェクト。
   * 使用するプリンタープロトコルを指定する `PrinterProtocol` 列挙値。例えば、SharedPrinter プロトコルを指定するには、`PrinterProtocol.SharedPrinter` を渡します。
   * 以前のパラメーター値を使用するかどうかを指定する `bool` 値。値 `true` を渡します。（このパラメーター値は、web サービスの呼び出しにのみ必要です）。
   * 印刷サーバーの名前を指定する文字列値です。例えば、印刷サーバーの名前が「PrintServer1」であると仮定した場合、`\\\PrintSever1` を渡します。
   * プリンターの名前を指定する文字列値です。例えば、プリンター名が「Printer1」であると仮定した場合、`\\\PrintSever1\Printer1` を渡します。

   >[!NOTE]
   >
   >この `sendToPrinter` メソッドが AEM Forms API バージョン 8.2.1 に追加されました。

## 複数の Output ファイルの作成 {#creating-multiple-output-files}

Output サービスでは、XML データソース内のレコードごとに個別のドキュメントを作成することも、すべてのレコードを含む単一のファイルを作成することもできます（この機能はデフォルトです）。例えば、10 個のレコードが XML データソース内に配置され、Output Service API を使用して、各レコードに対して個別の PDF ドキュメント（または他の種類の出力）を作成するように Output サービスに指示したとします。その結果、Output サービスは 10 個の PDF ドキュメントを生成します（ドキュメントを作成する代わりに、1 台のプリンターに複数の印刷ストリームを送信できます）。

次の図は、複数のレコードを含んだ XML データファイルを Output サービスで処理する様子も示しています。ただし、すべてのデータレコードを含んだ単一の PDF ドキュメントを作成するように Output サービスに指示した場合は、Output サービスは、すべてのレコードを含んだ 1 つのドキュメントを生成します。

次の図は、複数のレコードを含んだ XML データファイルを Output サービスで処理する様子を示しています。データレコードごとに個別の PDF ドキュメントを作成するように Output サービスに指示するとします。この場合、Output サービスは、データレコードごとに個別の PDF ドキュメントを生成します。

![cm_outputbatchmany](assets/cm_outputbatchmany.png)

次の XML データは、3 つのデータレコードを含むデータファイルの例を示しています。

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

各データレコードを開始および終了する XML 要素は、`LoanRecord` であることに注意してください。この XML 要素は、複数のファイルを生成するアプリケーションロジックによって参照されます。

>[!NOTE]
>
>Output サービスについて詳しくは、[AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary_of_steps-7}

XML データソースに基づいて複数の PDF ファイルを作成するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Output クライアントオブジェクトを作成します。
1. XML データソースを参照します。
1. PDF の実行時オプションを設定します。
1. レンダリングの実行時オプションを設定します。
1. 複数の PDF ファイルを生成します。
1. 操作の結果を取得します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、必ずプロキシファイルを含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar（AEM Forms が JBoss にデプロイされている場合に必要）
* jbossall-client.jar（AEM Formsが JBoss にデプロイされている場合に必要）

AEM Forms が JBoss 以外のサポート対象の J2EE アプリケーションサーバーにデプロイされている場合は、adobe-utilities.jar ファイルと jbossall-client.jar ファイルを、AEM Forms がデプロイされている J2EE アプリケーションサーバーに固有の JAR ファイルに置き換える必要があります。

**Output クライアントオブジェクトの作成**

プログラムで Output サービスの操作を実行する前に、Output サービスのクライアントオブジェクトを作成する必要があります。Java API を使用している場合は、`OutputClient` オブジェクトを作成します。Output web サービス API を使用している場合は、`OutputServiceService` オブジェクトを作成します。

**XML データソースの参照**

複数のレコードを含む XML データソースを参照します。データレコードを区切るには、XML 要素を使用する必要があります。例えば、この節で前述した XML データソースの例では、データレコードを区切る XML 要素の名前は `LoanRecord` です。

データを入力するフォームフィールドごとに、XML 要素が存在している必要があります。XML 要素名は、フィールド名と一致する必要があります。XML 要素がフォームフィールドに対応していない場合や、XML 要素名がフィールド名と一致しない場合、XML 要素は無視されます。すべての XML 要素が指定されている場合、XML 要素の表示順序を一致させる必要はありません。

**PDF 実行時オプションの設定**

XML データソースに基づいて複数のファイルを正常に作成するには、Output サービスに次の実行時オプションを設定する必要があります。

* **多数のファイル**：Output サービスで 1 つのドキュメントを作成するか、複数のドキュメントを作成するかを指定します。true または false を指定できます。XML データソース内のデータレコードごとに個別のドキュメントを作成するには、true を指定します。
* **ファイル URI**：Output サービスで生成されるファイルの場所を指定します。例えば、C:\\Adobe\forms\Loan.pdf と指定したとします。この場合、Output サービスは Loan.pdf という名前のファイルを作成して C:\\Adobe\forms フォルダーに配置します。複数のファイルが存在する場合、ファイル名は Loan0001.pdf、Loan0002.pdf、Loan0003.pdf などになります。ファイルの場所を指定した場合、ファイルはクライアントコンピューターではなくサーバーに配置されます。
* **レコード名**：データレコードを区切るデータソース内の XML 要素名を指定します。例えば、この節で前述した XML データソースの例では、データレコードを区切る XML 要素の名前は `LoanRecord` になります。なお、「レコード名」実行時オプションを設定する代わりに、データレコードを含んだ要素レベルを示す数値をレコードレベルに割り当てることで、「レコードレベル」を設定できます。ただし、設定できるのは「レコード名」または「レコードレベル」のみです。両方の値を設定することはできません。

**レンダリング実行時オプションの設定**

複数のファイルを作成しながら、レンダリング実行時オプションを設定できます。これらのオプションは必須ではありませんが（必須の出力実行時オプションとは異なります）、Output サービスのパフォーマンス向上などのタスクを実行できます。例えば、Output サービスで使用するフォームデザインをキャッシュして、パフォーマンスを向上させることができます。

Output サービスは、バッチレコードを処理するときに、複数のレコードを含んだデータを増分的に読み込みます。つまり、Output サービスはデータをメモリに読み込み、レコードのバッチが処理されるとデータを解放します。Output サービスは、2 つの実行時オプションのいずれかが設定されている場合、増分的にデータを読み込みます。「レコード名」実行時オプションを設定する場合、Output サービスは増分的にデータを読み込みます。同様に、「レコードレベル」実行時オプションを 2 以上に設定した場合、Output サービスは増分的にデータを読み込みます。

`PDFOutputOptionsSpec` または `PrintedOutputOptionSpec` オブジェクトの `setLazyLoading` メソッドを使用して、Output サービスで増分読み込みを実行するかどうかを制御できます 。このメソッドに値 `false` を渡すと、増分読み込みがオフになります。

**複数の PDF ファイルの生成**

複数のデータレコードを含んだ有効な XML データソースを参照し、実行時オプションを設定した後、Output サービスを呼び出して、複数のファイルを生成できます。複数のレコードを生成する場合、`OutputResult` オブジェクトの `getGeneratedDoc` メソッドは `null` を返します。

**操作の結果の取得**

Output サービスが操作を実行すると、操作が成功したかどうかを示す XML データが返されます。次の XML が Output サービスから返されます。この例では、Output サービスは 42 個のドキュメントを生成しました。

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

[AEM Forms Java ライブラリファイルの組み込み](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Output Service API のクイックスタート](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Java API を使用した複数の PDF ファイルの作成 {#create-multiple-pdf-files-using-the-java-api}

Output API（Java）を使用して複数の PDF ファイルを作成するには、次の手順に従います。

1. プロジェクトファイルの組み込み

   adobe-livecycle-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. Output クライアントオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用し `ServiceClientFactory` オブジェクトを渡すことで、`OutputClient` オブジェクトを作成します。

1. XML データソースの参照

   * コンストラクターを使用し、XML ファイルの場所を指定する文字列値を渡すことで、複数のレコードを含んだ XML データソースを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクターを使用し `java.io.FileInputStream` オブジェクトを渡すことで、`com.adobe.idp.Document` オブジェクトを作成します。

1. PDF 実行時オプションを設定

   * コンストラクターを使用して `PDFOutputOptionsSpec` オブジェクトを作成します。
   * 「多数のファイル」オプションを設定するには、`PDFOutputOptionsSpec` オブジェクトの `setGenerateManyFiles` メソッドを呼び出します。例えば、XML データソース内のレコードごとに個別の PDF ファイルを作成するように Output サービスに指示するには、値 `true` を渡します。なお、`false` を渡した場合、Output サービスはすべてのレコードを含んだ単一の PDF ドキュメントを生成します。
   * 「 ファイル URI 」オプションを設定するには、`PDFOutputOptionsSpec` オブジェクトの `setFileUri` メソッドを呼び出して、Output サービスが生成するファイルの場所を指定する文字列値を渡します。ファイル URI オプションは、クライアントコンピューターではなく、AEM Forms をホストする J2EE アプリケーションサーバーに対する相対パスです。
   * 「レコード名」オプションを設定するには、`OutputOptionsSpec` オブジェクトの `setRecordName` メソッドを呼び出して、データレコードを区切るデータソース内の XML 要素名を指定する文字列値を渡します。例えば、この節で前述した XML データソースを考えてみましょう。この場合、データレコードを区切る XML 要素の名前は LoanRecord です。

1. レンダリング実行時オプションの設定

   * コンストラクターを使用して `RenderOptionsSpec` オブジェクトを作成します。
   * フォームデザインをキャッシュして Output サービスのパフォーマンスを向上させるには、`RenderOptionsSpec` オブジェクトの `setCacheEnabled` を呼び出し、`true` の `Boolean` 値を渡します。

1. 複数の PDF ファイルの生成

   複数の PDF ファイルを生成するには、`OutputClient` オブジェクトの `generatePDFOutput` メソッドを呼び出し、次の値を渡します。

   * `TransformationFormat` 列挙値。PDF ドキュメントを生成するには、`TransformationFormat.PDF` を指定します。
   * フォームデザイン名を指定する文字列値。
   * フォームデザインが配置されているコンテンツルートを指定する文字列の値です。
   * PDF 実行時オプションを含む `PDFOutputOptionsSpec` オブジェクト。
   * レンダリング実行時オプションを含む `RenderOptionsSpec` オブジェクト。
   * フォームデザインと結合するデータを含む XML データソースを含む `com.adobe.idp.Document` オブジェクト。

   この `generatePDFOutput` メソッドは、操作の結果を含む `OutputResult` オブジェクトを返します。

1. 操作の結果を取得します。

   * `generatePDFOutput` メソッドの結果を含む XML ファイルを表す `java.io.File` オブジェクトを作成します。ファイル名の拡張子が .xml であることを確認します。
   * `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを呼び出して、`com.adobe.idp.Document` オブジェクトの内容をファイルにコピーします（`applyUsageRights` メソッドによって返された `com.adobe.idp.Document` オブジェクトを使用していることを確認してください）。

**関連情報**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[クイックスタート（EJB モード）：Java API を使用した複数の PDF ファイルの作成](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-multiple-pdf-files-using-the-java-api)

[AEM Forms Java ライブラリファイルの組み込み](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用した複数の PDF ファイルの作成 {#create-multiple-pdf-files-using-the-web-service-api}

Output API（web サービス）を使用して複数の PDF ファイルを作成します。

1. プロジェクトファイルを含めます。

   MTOM を使用する Microsoft .NET プロジェクトを作成します。WSDL 定義 `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1` を使用するようにします。

   >[!NOTE]
   >
   >`localhost` を、AEM Forms をホストするサーバーの IP アドレスで置換します。

1. Output クライアントオブジェクトを作成します。

   * デフォルトのコンストラクターを使用して、`OutputServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して、`OutputServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/OutputService?blob=mtom`）。`lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。ただし、`?blob=mtom` を指定して MTOM を使用します。
   * `OutputServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` フィールドを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `OutputServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `OutputServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
      * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` を`BasicHttpBindingSecurity.Security.Mode` フィールドに割り当てます。

1. XML データソースを参照します。

   * コンストラクターを使用して `BLOB` オブジェクトを作成します。`BLOB` オブジェクトは、複数のレコードを含むフォームデータを保存するために使用します。
   * コンストラクターを呼び出して `System.IO.FileStream` オブジェクトを作成します。複数のレコードを含む XML ファイルの場所を表す文字列値を渡します。
   * `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することで、バイト配列のサイズを決定できます。
   * `System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出し、バイト配列、開始位置、読み取るストリーム長を渡すことにより、バイト配列にストリームデータを入力します。
   * バイト配列の内容を `MTOM` フィールドに割り当てることによって、`BLOB` オブジェクトにデータを設定します。

1. PDF の実行時オプションを設定します。

   * コンストラクターを使用して `PDFOutputOptionsSpec` オブジェクトを作成します。
   * `OutputOptionsSpec` オブジェクトの `generateManyFiles` データメンバーに boolean 値を割り当てることによって、「多数のファイル」オプションを設定します。例えば、値 `true` をこのデータメンバーに割り当てて、XML データソース内のレコードごとに個別の PDF ファイルを作成するよう Output サービスに指示します（このデータメンバーに `false` を割り当てると、Output サービスは、すべてのレコードを含む単一の PDF を生成します）。
   * Output サービスが生成するファイルの場所を指定する文字列値を、`OutputOptionsSpec` オブジェクトの `fileURI` データメンバーに割り当てることによって、「ファイル URI」オプションを設定します。ファイル URI オプションは、クライアントコンピューターではなく、AEM Forms をホストする J2EE アプリケーションサーバーに対する相対パスです。
   * データレコードを分割するデータソース内の XML 要素名を指定する文字列値を、`OutputOptionsSpec` オブジェクトの `recordName` データメンバーに割り当てることによって、レコード名オプションを設定します。
   * Output サービスが生成するコピー数を指定する整数値を、`OutputOptionsSpec` オブジェクトの `copies` データメンバーに割り当てることによって、コピー数オプションを設定します。

1. レンダリングの実行時オプションを設定します。

   * コンストラクタを使用して `RenderOptionsSpec` オブジェクトを作成します。
   * Output サービスのパフォーマンスを向上させるために、値 `true` を `RenderOptionsSpec` オブジェクトの `cacheEnabled` データメンバーに割り当てることによってフォームデザインをキャッシュします。

1. 複数の PDF ファイルを生成します。

   `OutputServiceService` オブジェクトの `generatePDFOutput` メソッドを呼び出し、次の値を渡すことによって、複数の PDF ファイルを作成します。

   * TransformationFormat 列挙値。PDFドキュメントを生成するために、`TransformationFormat.PDF` を指定します。
   * フォームデザイン名を指定する文字列値。
   * フォームデザインが配置されているコンテンツルートを指定する文字列の値です。
   * PDF 実行時オプションを含む `PDFOutputOptionsSpec` オブジェクト。
   * レンダリング実行時オプションを含む `RenderOptionsSpec` オブジェクト。
   * フォームデザインと結合するデータが含まれる XML データソースを含む `BLOB` オブジェクト。
   * `generatePDFOutput` メソッドによって設定される `BLOB` オブジェクトです。`generatePDFOutput` メソッドは、ドキュメントを表す生成されたメタデータをこのオブジェクトに設定します。
   * `generatePDFOutput` メソッドで入力した `BLOB` オブジェクト。`generatePDFOutput` メソッドは、このオブジェクトに結果データを入力します。
   * 操作の結果を格納する `OutputResult` オブジェクト。

1. 操作の結果を取得します。

   * コンストラクターを呼び出し、結果データを含む XML ファイルの場所を表す文字列の値を渡すことにより、`System.IO.FileStream` オブジェクトを作成します。ファイル名の拡張子が .xml であることを確認します。
   * `BLOB` オブジェクトのデータコンテンツを格納するバイト配列を作成します。このオブジェクトには、`OutputServiceService` オブジェクトの `generatePDFOutput` メソッド（ 8 番目のパラメーター）によって結果データが入力されています。`BLOB` オブジェクトの `binaryData` データメンバーの値を取得して、バイト配列にデータを入力します。
   * コンストラクターを呼び出して `System.IO.FileStream` オブジェクトを渡すことによって、`System.IO.BinaryWriter` オブジェクトを作成します。
   * バイト配列の内容を XML ファイルに書き込むには、`System.IO.BinaryWriter` オブジェクトの `Write` メソッドを呼び出して、バイト配列を渡します。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 検索ルールの作成 {#creating-search-rules}

入力データを調べ、出力を生成するデータコンテンツに基づいた様々なフォームデザインを使用することで、Output サービスを導き出す検索ルールを作成できます。例えば、 *mortgage* というテキストが入力データ内にある場合、Output サービスは Mortgage.xdp という名前のフォームデザインを使用できます。同様に、 *automobile* というテキストが入力データにある場合、Output サービスは、AutomobileLoan.xdp として保存されたフォームデザインを使用できます。Output サービスでは異なる出力タイプを生成できますが、この節では、Output サービスが PDF ファイルを生成することを前提としています。以下の図は、XML データファイルを処理し、多数のフォームデザインの 1 つを使用して PDF ファイルを生成する Output サービスを示しています。

また、Output サービスではドキュメントパッケージを生成できます。このパッケージでは、データセットに複数のレコードが含まれており、各レコードがフォームデザインと照合され、1 つのドキュメントが複数のフォームデザインで構成されます。

![cs_outputbatchmanyformdesigns2](assets/cs_outputbatchmanyformdesigns2.png)

>[!NOTE]
>
>Output サービスについて詳しくは、[AEM Forms サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary_of_steps-8}

ドキュメントの生成時に検索ルールを使用するように Output サービスを設定するには、以下の手順を実行します。

1. プロジェクトファイルを含めます。
1. Output クライアントオブジェクトを作成します。
1. XML データソースを参照します。
1. 検索ルールを定義します。
1. PDF の実行時オプションを設定します。
1. レンダリングの実行時オプションを設定します。
1. PDF ドキュメントの生成
1. 操作の結果を取得します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めるようにします。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar（AEM Forms を JBoss にデプロイする場合に必要）
* jbossall-client.jar（AEM Forms が JBoss にデプロイされている場合に必要）

AEM Forms が JBoss 以外のサポート対象の J2EE アプリケーションサーバーにデプロイされている場合は、adobe-utilities.jar ファイルと jbossall-client.jar ファイルを、AEM Forms がデプロイされている J2EE アプリケーションサーバーに固有の JAR ファイルに置き換える必要があります。

**Output クライアントオブジェクトの作成**

Output サービスの処理をプログラムで実行する前に、Output サービスのクライアントオブジェクトを作成する必要があります。

**XML データソースの参照**

データを入力するフォームフィールドごとに、XML 要素が存在している必要があります。XML 要素名は、フィールド名と一致する必要があります。XML 要素がフォームフィールドに対応していない場合や、XML 要素名がフィールド名と一致しない場合、XML 要素は無視されます。すべての XML 要素が指定されている場合、XML 要素の表示順序を一致させる必要はありません。

**検索ルールの定義**

検索ルールを定義するには、Output サービスで検索する 1 つ以上のテキストパターンを入力データに定義します。定義する各テキストパターンに対して、そのテキストパターンが存在する場合に使用するフォームデザインを指定します。テキストパターンが存在する場合、Output サービスは対応するフォームデザインを使用して出力を生成します。テキストパターンの例は&#x200B;*mortgage*&#x200B;とします。

>[!NOTE]
>
>テキストパターンが存在しない場合は、デフォルトのフォームが使用されます。使用するすべてのフォームデザインを、コンテンツルートに必ず配置します。

**PDF 実行時オプションの設定**

Output サービスで、複数のフォームデザインに基づいて PDF ドキュメントを正しく作成するために、以下の PDF 実行時オプションを設定します。

* **ファイル URI**：Output サービスで生成する PDF ファイルの名前と場所を指定します。
* **ルール**: 定義したルールを指定します。
* **LookAHead**：定義されたテキストパターンをスキャンするために、入力データファイルの先頭から使用するバイト数を指定します。デフォルトは 500 バイトです。

**レンダリング実行時オプションの設定**

レンダリング実行時オプションは、PDF ファイルの作成時に設定できます。（PDF 実行時オプションとは異なり）これらのオプションは必須ではありませんが、Output サービスのパフォーマンス向上などのタスクを実行できます。例えば、Output サービスで使用するフォームデザインをキャッシュして、パフォーマンスを向上させることができます。

**PDF ドキュメントの生成**

有効な XML データソースを参照し、実行時オプションを設定した後、Output サービスを呼び出すと、PDF ドキュメントが生成されます。Output サービスが入力データ内で指定されたテキストパターンを見つけた場合は、対応するフォームデザインを使用します。テキストパターンを使用しない場合、Output サービスはデフォルトのフォームデザインを使用します。

**操作の結果を取得する**

Output サービスが処理を実行すると、処理が成功したかどうかを示す XML データが返されます。

**関連項目**

[AEM Forms Java ライブラリファイルの組み込み](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Output Service API のクイックスタート](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Java API を使用した検索ルールの作成 {#create-search-rules-using-the-java-api}

Output API（Java）を使用して検索ルールを作成するには、以下の手順を実行します。

1. プロジェクトファイルを含めます。

   adobe-output-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. Output クライアントオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して `ServiceClientFactory` オブジェクトを渡すことにより、`OutputClient` オブジェクトを作成します。

1. XML データソースを参照します。

   * XML データソースを表す `java.io.FileInputStream` オブジェクトを作成します。この XML データソースのコンストラクターを使用して、XML ファイルの場所を指定する文字列の値を渡すことで、PDF ドキュメントが追加されます。
   * コンストラクターを使用して `java.io.FileInputStream` オブジェクトを渡し、`com.adobe.idp.Document` オブジェクトを作成します。

1. 検索ルールを定義します。

   * コンストラクターを使用して `Rule` オブジェクトを作成します。
   * `Rule` オブジェクトの `setPattern` メソッドを呼び出し、テキストパターンを指定する文字列の値を渡して、テキストパターンを定義します。
   * `Rule` オブジェクトの `setForm` メソッドを呼び出して、対応するフォームデザインを定義します。フォームデザイン名を指定する文字列の値を渡します。

   >[!NOTE]
   >
   >定義するテキストパターンごとに、上述の 3 つのサブステップを繰り返します。

   * `java.util.ArrayList` コンストラクターを使用して `java.util.List` オブジェクトを作成します。
   * 作成した `Rule` オブジェクトごとに、`java.util.List` オブジェクトの `add` メソッドを呼び出して `Rule` オブジェクトを渡します。


1. PDF の実行時オプションを設定します。

   * コンストラクターを使用して `PDFOutputOptionsSpec` オブジェクトを作成します。
   * `PDFOutputOptionsSpec` オブジェクトの `setFileURI` メソッドを呼び出して、Output サービスが生成する PDF ファイルの名前と場所を指定します。PDF ファイルの場所を指定する文字列の値を渡します。ファイル URI オプションは、クライアントコンピューターではなく、AEM Forms をホストする J2EE アプリケーションサーバーに対する相対パスです。
   * `PDFOutputOptionsSpec` オブジェクトの `setRules` メソッドを呼び出して、定義したルールを設定します。`Rule` オブジェクトを含む `java.util.List` オブジェクトを渡します。
   * `PDFOutputOptionsSpec` オブジェクトの `setLookAhead` メソッドを呼び出して、定義したテキストパターンをスキャンするバイト数を設定します。バイト数を表す整数値を渡します。

1. レンダリングの実行時オプションを設定します。

   * コンストラクターを使用して `RenderOptionsSpec` オブジェクトを作成します。
   * Output サービスのパフォーマンスを向上させるために、`RenderOptionsSpec` オブジェクトの `setCacheEnabled` を呼び出して `true` を渡すことにより、フォームデザインをキャッシュします。

1. PDF ドキュメントの生成

   `OutputClient` オブジェクトの `generatePDFOutput` メソッドを呼び出して以下の値を渡すことで、複数のフォームデザインに基づく PDF ドキュメントを生成します。

   * `TransformationFormat` 列挙値。PDF ドキュメントを生成するには、`TransformationFormat.PDF` を指定します。
   * デフォルトのフォームデザインの名前を指定する文字列の値。テキストパターンが見つからない場合に使用するフォームデザインです。
   * フォームデザインが配置されているコンテンツルートを指定する文字列の値です。
   * PDF の実行時オプションを含む `PDFOutputOptionsSpec` オブジェクト。
   * レンダリングの実行時オプションを含む `RenderOptionsSpec` オブジェクト。
   * フォームデータを含む `com.adobe.idp.Document` オブジェクト。このフォームデータは、定義したテキストパターンを Output サービスで検索するためのものです。

   `generatePDFOutput` メソッドは、操作の結果を含む `OutputResult` オブジェクトを返します。

1. 操作の結果を取得します。

   * `OutputResult` オブジェクトの `getStatusDoc` メソッドを呼び出して、`generatePDFOutput` メソッドのステータスを表す `com.adobe.idp.Document` オブジェクトを作成します。
   * 操作の結果を格納する `java.io.File` オブジェクトを作成します。ファイル拡張子が .xml であることを確認します。
   * `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを呼び出して、`com.adobe.idp.Document` オブジェクトのコンテンツをファイルにコピーします（`getStatusDoc` メソッドが返した `com.adobe.idp.Document` オブジェクトを使用してください）。

**関連情報**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[クイックスタート（EJB モード）：Java API を使用した検索ルールの作成](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[クイックスタート（SOAP モード）：Java API を使用した検索ルールの作成](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[AEM Forms の Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用して検索ルールを作成する {#create-search-rules-using-the-web-service-api}

Output API（web サービス）を使用して検索ルールを作成します。

1. プロジェクトファイルを含めます。

   MTOM を使用する Microsoft .NET プロジェクトを作成します。WSDL 定義 `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1` を使用するようにします。

   >[!NOTE]
   >
   >`localhost` を、AEM Forms をホストするサーバーの IP アドレスで置換します。

1. Output クライアントオブジェクトを作成します。

   * デフォルトのコンストラクターを使用して、`OutputServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して、`OutputServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/OutputService?blob=mtom`）。`lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。ただし、`?blob=mtom` を指定して MTOM を使用します。
   * `OutputServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` フィールドを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `OutputServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `OutputServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
      * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` を`BasicHttpBindingSecurity.Security.Mode` フィールドに割り当てます。

1. XML データソースを参照します。

   * コンストラクターを使用して `BLOB` オブジェクトを作成します。`BLOB` オブジェクトは、PDF ドキュメントと結合されるデータを格納するために使用されます。
   * コンストラクターを呼び出し、暗号化する PDF ドキュメントのファイルの場所とファイルを開くモードを表す文字列値を渡して、`System.IO.FileStream` オブジェクトを作成します。
   * `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することで、バイト配列のサイズを決定できます。
   * `System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出し、バイト配列、開始位置、読み取るストリーム長を渡すことにより、バイト配列にストリームデータを入力します。
   * `MTOM` フィールドにバイト配列の内容を割り当てて、`BLOB` オブジェクトにデータを入力します。

1. 検索ルールを定義します。

   * コンストラクターを使用して `Rule` オブジェクトを作成します。
   * `Rule` オブジェクトの `pattern` データメンバーにテキストパターンを指定する文字列値を割り当てることにより、テキストパターンを定義します。
   * フォームデザインを指定する文字列値を `Rule` オブジェクトの `form` データメンバーに割り当てることにより、対応するフォームデザインを定義します。

   >[!NOTE]
   >
   >定義するテキストパターンごとに、上述の 3 つのサブステップを繰り返します。

   * ルールを格納する `MyArrayOf_xsd_anyType` オブジェクトを作成します。
   * 各 `Rule` オブジェクトを `MyArrayOf_xsd_anyType` 配列の要素に割り当てます。`Rule` オブジェクトごとに `MyArrayOf_xsd_anyType` オブジェクトの `Add` メソッドを呼び出します。


1. PDF 実行時オプションを設定

   * コンストラクターを使用して `PDFOutputOptionsSpec` オブジェクトを作成します。
   * Output サービスが生成する PDF ファイルの場所を指定する文字列値を `PDFOutputOptionsSpec` オブジェクトの `fileURI` データメンバーに割り当てることにより、ファイル URI オプションを設定します。ファイル URI オプションは、クライアントコンピューターではなく、AEM Forms をホストする J2EE アプリケーションサーバーに対する相対パスです。
   * Output サービスが生成するコピー数を指定する整数値を `PDFOutputOptionsSpec` オブジェクトの `copies` データメンバーに割り当てることで、コピーオプションを設定します。
   * ルールを格納する `MyArrayOf_xsd_anyType` オブジェクトを `PDFOutputOptionsSpec` オブジェクトの `rules` データメンバーに割り当てて、定義したルールを設定します。
   * スキャンするバイト数を表す整数値を `PDFOutputOptionsSpec` オブジェクトの `lookAhead` データメソッドに割り当てることにより、定義されたテキストパターンをスキャンするバイト数を設定します。

1. レンダリング実行時オプションの設定

   * コンストラクターを使用して `RenderOptionsSpec` オブジェクトを作成します。
   * Output サービスのパフォーマンスを向上させるために、`RenderOptionsSpec` オブジェクトの `cacheEnabled` データメンバーに値 `true` を割り当てて、フォームデザインをキャッシュします。

   >[!NOTE]
   >
   >入力ドキュメントが Acrobat フォームの場合、`RenderOptionsSpec` オブジェクトの `pdfVersion` メンバーを使用して PDF ドキュメントのバージョンを設定することはできません。出力 PDF ドキュメントには、Acrobat フォームの PDF バージョンが保持されます。同様に、入力ドキュメントが Acrobat フォームの場合、`RenderOptionsSpec` オブジェクトの `taggedPDF` メソッドを使用してタグ付き PDF オプションを設定することはできません。

   >[!NOTE]
   >
   >入力 PDF ドキュメントが認証済みまたはデジタル署名されている場合、`RenderOptionsSpec` オブジェクトの `linearizedPDF` メンバーを使用してリニアライズド PDF オプションを設定することはできません。詳しくは、 [PDF ドキュメントのデジタル署名](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)を参照してください。

1. PDF ドキュメントの生成

   `OutputServiceService` オブジェクトの `generatePDFOutput` メソッドを呼び出し、次の値を渡して PDF ドキュメントを作成します。

   * `TransformationFormat` 列挙値。PDF ドキュメントを生成するには、`TransformationFormat.PDF` を指定します。
   * フォームデザイン名を指定する文字列値。
   * フォームデザインが配置されているコンテンツルートを指定する文字列の値です。
   * PDF 実行時オプションを含む `PDFOutputOptionsSpec` オブジェクト。
   * レンダリング実行時オプションを含む `RenderOptionsSpec` オブジェクト。
   * フォームデザインと結合するデータが含まれる XML データソースを含む `BLOB` オブジェクト。
   * `generatePDFOutput` メソッドによって入力される `BLOB` オブジェクト。`generatePDFOutput` メソッドは、ドキュメントを説明する生成されたメタデータをこのオブジェクトに入力します。（このパラメーター値は、web サービスの呼び出しにのみ必要です）。
   * `generatePDFOutput` メソッドによって入力される `BLOB` オブジェクト。`generatePDFOutput` メソッドは、このオブジェクトに結果データを入力します。（このパラメーター値は、web サービスの呼び出しにのみ必要です）。
   * 操作の結果を含む `OutputResult` オブジェクト。（このパラメーター値は、web サービスの呼び出しにのみ必要です）。

   >[!NOTE]
   >
   >`generatePDFOutput` メソッドを呼び出して PDF ドキュメントを生成する場合、署名、認証、使用権限を含む XFA PDFフォームにデータを結合することはできません。使用権限について詳しくは、[PDF ドキュメントへの使用権限の適用](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)を参照してください。

1. 操作の結果を取得します。

   * コンストラクターを呼び出し、結果データを含む XML ファイルの場所を表す文字列値を渡すことにより、`System.IO.FileStream` オブジェクトを作成します。ファイル拡張子が XML であることを確認します。
   * `OutputServiceService` オブジェクトの `generatePDFOutput` メソッド（8 番目のパラメーター）によって結果データが入力された `BLOB` オブジェクトのデータコンテンツを格納するバイト配列を作成します。`BLOB` オブジェクトの `MTOM` データメンバーの値を取得して、バイト配列にデータを入力します。
   * コンストラクターを呼び出して `System.IO.FileStream` オブジェクトを渡すことによって、`System.IO.BinaryWriter` オブジェクトを作成します。
   * バイト配列の内容を XML ファイルに書き込むには、`System.IO.BinaryWriter` オブジェクトの `Write` メソッドを呼び出して、バイト配列を渡します。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## PDF ドキュメントの平坦化 {#flattening-pdf-documents}

Output サービスを使用すると、インタラクティブ PDF ドキュメントを非インタラクティブ PDF に変換できます。インタラクティブ PDF ドキュメントでは、ユーザーは PDF ドキュメントフィールドにデータを入力したり、このフィールドのデータを変更したりできます。インタラクティブ PDF ドキュメントを非インタラクティブ PDF ドキュメントに変換するプロセスは「*フラット化*」と呼ばれます。PDF ドキュメントをフラット化すると、ユーザーはドキュメントフィールドにあるデータを変更できなくなります。PDF ドキュメントを統合する理由の 1 つは、データを変更できないようにすることです。

次のタイプの PDF ドキュメントを統合できます。

* インタラクティブ XFA PDF ドキュメント
* Acrobat フォーム

非インタラクティブ PDF ドキュメントの PDF をフラット化しようとすると、例外が発生します。

>[!NOTE]
>
>Output サービスについて詳しくは、[AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary_of_steps-9}

インタラクティブ PDF ドキュメントを非インタラクティブ PDF ドキュメントにフラット化するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. Output クライアントオブジェクトを作成します。
1. インタラクティブな PDF ドキュメントを取得します。
1. PDF ドキュメントを変換します。
1. 非インタラクティブ PDF ドキュメントを PDF ファイルとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用する場合は、必ずプロキシファイルを含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar（AEM Forms が JBoss にデプロイされている場合に必要）
* jbossall-client.jar（AEM Formsが JBoss にデプロイされている場合に必要）

AEM Forms が JBoss 以外のサポート対象の J2EE アプリケーションサーバーにデプロイされている場合は、adobe-utilities.jar ファイルと jbossall-client.jar ファイルを、AEM Forms がデプロイされている J2EE アプリケーションサーバーに固有の JAR ファイルに置き換える必要があります。すべての AEM Forms JAR ファイルの場所については、 [AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。

**Output クライアントオブジェクトの作成**

プログラムで Output サービスの操作を実行する前に、Output サービスのクライアントオブジェクトを作成する必要があります。Java API を使用している場合は、`OutputClient` オブジェクトを作成します。Output web サービス API を使用している場合は、`OutputServiceService` オブジェクトを作成します。

**インタラクティブ PDF ドキュメントの取得**

非インタラクティブ PDF ドキュメントに変換するインタラクティブ PDF ドキュメントを取得します。非インタラクティブ PDF ドキュメントを変換しようとすると、例外が発生します。

**PDF ドキュメントの変換**

インタラクティブ PDF ドキュメントを取得した後、そのドキュメントを非インタラクティブ PDF ドキュメントに変換できます。Output サービスは、非インタラクティブ PDF ドキュメントを返します。

**非インタラクティブ PDF ドキュメントを PDF ファイルとして保存**

非インタラクティブ PDF ドキュメントは、PDF ファイルとして保存できます。

**関連トピック**

[Java API を使用した PDF ドキュメントのフラット化](creating-document-output-streams.md#flatten-a-pdf-document-using-the-java-api)

[Web サービス API を使用した PDFドキュメントの統合](creating-document-output-streams.md#flatten-a-pdf-document-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Output Service API のクイックスタート](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Java API を使用した PDF ドキュメントのフラット化 {#flatten-a-pdf-document-using-the-java-api}

Output API（Java）を用いて、インタラクティブな PDF ドキュメントを非インタラクティブな PDF ドキュメントにフラット化することができます。

1. プロジェクトファイルを含めます。

   adobe-output-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. Output クライアントオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して `OutputClient` オブジェクトを作成し、`ServiceClientFactory` オブジェクトを渡します。

1. インタラクティブな PDF ドキュメントを取得します。

   * 変換するインタラクティブ PDF ドキュメントを表す `java.io.FileInputStream` オブジェクトを作成し、そのコンストラクターを使用して、インタラクティブ PDF ファイルの場所を指定する文字列値を渡します。
   * コンストラクターを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PDF ドキュメントを変換します。

   `OutputServiceService` オブジェクトの `transformPDF` メソッドを呼び出し、次の値を渡すことによって、インタラクティブな PDF ドキュメントを非インタラクティブな PDF ドキュメントに変換します。

   * インタラクティブな PDF ドキュメントを含む `com.adobe.idp.Document` オブジェクト。
   * `TransformationFormat` enum の値。非インタラクティブ PDF ドキュメントを生成するには、`TransformationFormat.PDF` を指定します。
   * リビジョン番号を指定する `PDFARevisionNumber` enum 値。このパラメータは PDF/A ドキュメント向けであるため、`null` を指定できます。
   * 修正番号と年がコロンで区切られた文字列の値。このパラメータは PDF/A ドキュメント向けであるため、`null` を指定できます。
   * PDF/A 準拠レベルを表す `PDFAConformance` enum 値。このパラメータは PDF/A 文書向けであるため、`null` を指定できます。

   `transformPDF` メソッドは、非インタラクティブな PDF ドキュメントを含む `com.adobe.idp.Document` オブジェクトを返します。

1. 非インタラクティブ PDF ドキュメントを PDF ファイルとして保存します。

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が .pdf であることを確認します。
   * `Document` オブジェクトの `copyToFile` メソッドを呼び出して、`Document` オブジェクトの内容をファイルにコピーします（必ず、`transformPDF` メソッドが返した `Document` オブジェクトを使ってください）。

**関連情報**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[クイックスタート（EJB モード）：Java API を使用して PDF 文書を変換する](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

[クイックスタート（SOAP モード）：Java API を使用して PDF ドキュメントを変換する](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用した PDFドキュメントの統合 {#flatten-a-pdf-document-using-the-web-service-api}

Output API（Web サービス）を利用して、インタラクティブな PDF ドキュメントを非インタラクティブな PDF ドキュメントにフラット化することができます。

1. プロジェクトファイルを含めます。

   MTOM を使用する Microsoft .NET プロジェクトを作成します。WSDL 定義 `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1` を使用するようにします。

   >[!NOTE]
   >
   >`localhost` を、AEM Forms をホストするサーバーの IP アドレスで置換します。

1. Output クライアントオブジェクトを作成します。

   * デフォルトのコンストラクターを使用して、`OutputServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して、`OutputServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/OutputService?blob=mtom`）。`lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。ただし、`?blob=mtom` を指定して MTOM を使用します。
   * `OutputServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` フィールドを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `OutputServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `OutputServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
      * フィールド `BasicHttpBindingSecurity.Security.Mode` に定数値 `BasicHttpSecurityMode.TransportCredentialOnly` を割り当てます。

1. インタラクティブな PDF ドキュメントを取得します。

   * コンストラクターを使用して `BLOB` オブジェクトを作成します。`BLOB` オブジェクトは、インタラクティブな PDF ドキュメントを格納するために使用されます。
   * `System.IO.FileStream` オブジェクトを作成するには、そのコンストラクターを呼び出し、インタラクティブ PDF ドキュメントのファイルの場所を表す文字列の値を渡します。
   * `System.IO.FileStream` オブジェクトの内容を格納するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することで、バイト配列のサイズを決定できます。
   * バイト配列にストリームデータを入力するには、`System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出し、バイト配列、開始位置、読み取るストリーム長を渡します。
   * `MTOM` プロパティを割り当てて、`BLOB` オブジェクトにバイト配列の内容を入力します。

1. PDF ドキュメントを変換します。

   インタラクティブ PDF ドキュメントを非インタラクティブ PDF ドキュメントに変換するには、`OutputClient` オブジェクトの `transformPDF` メソッドを呼び出し、次の値を渡します。

   * インタラクティブ PDF ドキュメントを含む `BLOB` オブジェクト。
   * `TransformationFormat` 列挙値。非インタラクティブ PDF ドキュメントを生成するには、`TransformationFormat.PDF` を指定します。
   * リビジョン番号を指定する `PDFARevisionNumber` 列挙値。
   * `PDFARevisionNumber` 列挙値を使用するかどうかを指定するブール値。このパラメーターは PDF/A ドキュメント向けなので、`false` を指定できます。
   * 修正番号と年がコロンで区切られた文字列の値。このパラメーターは PDF/A ドキュメント向けなので、`null` を指定できます。
   * PDF/A 適合レベルを表す `PDFAConformance` 列挙値。
   * `PDFAConformance` 列挙値を使用するかどうかを指定するブール値。このパラメーターは PDF/A ドキュメント向けなので、`false` を指定できます。

   `transformPDF` メソッドは、非インタラクティブな PDF ドキュメントを含む `BLOB` オブジェクトを返します。

1. 非インタラクティブ PDF ドキュメントを PDF ファイルとして保存します。

   * `System.IO.FileStream` オブジェクトを作成するには、そのコンストラクターを呼び出し、非インタラクティブ PDF ドキュメントのファイルの場所を表す文字列値を渡します。
   * `transformPDF` メソッドによって返された `BLOB` オブジェクトのデータコンテンツを格納するバイト配列を作成します。`BLOB` オブジェクトの `MTOM` データメンバーの値を取得して、バイト配列を生成します。
   * コンストラクターを使用して `System.IO.BinaryWriter` オブジェクトを渡すことによって、`System.IO.FileStream` オブジェクトを作成します。
   * `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを呼び出して、バイト配列を渡すことによって、バイト配列の内容を PDF ファイルに書き込みます。

**関連トピック：**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
