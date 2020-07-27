---
title: ドキュメント出力ストリームの作成
seo-title: ドキュメント出力ストリームの作成
description: 'null'
seo-description: 'null'
uuid: 80c28efa-35ce-4073-9ca6-2d93bcd67fdd
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: de527d50-991b-4ca3-a8ac-44d5cab988e9
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '18972'
ht-degree: 4%

---


# ドキュメント出力ストリームの作成  {#creating-document-output-streams}

**Outputサービスについて**

Outputサービスでは、ドキュメントをPDF(PDF/Aドキュメントを含む)、PostScript、Printer Control Language(PCL)および次のラベル形式で出力できます。

* Zebra - ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

Outputサービスを使用すると、XMLフォームデータをフォームデザインとマージし、ドキュメントをネットワークプリンターまたはファイルに出力できます。

フォームデザイン（XDPファイル）をOutputサービスに渡す方法は2つあります。 フォームデザインを含む `com.adobe.idp.Document` インスタンスをOutputサービスに渡すこともできます。 または、フォームデザインの場所を指定するURI値を渡すことができます。 これらの方法は、「AEM Formsによるプ *ログラミング」で説明されています*。

>[!NOTE]
>
>Outputサービスは、アプリケーションオブジェクト固有のスクリプトを含むAcroform PDFドキュメントをサポートしません。 アプリケーションオブジェクト固有のスクリプトを含むAcroform PDFドキュメントはレンダリングされません。

次の節では、URI値を使用してフォームデザインをOutputサービスに渡す方法を示します。

* [PDFドキュメントの作成](creating-document-output-streams.md#creating-pdf-documents)
* [PDF/Aドキュメントの作成](creating-document-output-streams.md#creating-pdf-a-documents)

次の節では、インスタンス内でフォームデザインを渡す方法を示し `com.adobe.idp.Document` ます。

* [Content Services（非推奨）にあるドキュメントーをOutputサービスに渡す](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)
* [フラグメントを使用したPDFドキュメントの作成](creating-document-output-streams.md#creating-pdf-documents-using-fragments)

使用する方法を決定する際には、別のAEM Formsサービスからフォームデザインを取得し、それを `com.adobe.idp.Document` インスタンス内で渡す場合に考慮する必要があります。 「Outputサービスに *渡す」ドキュメントと「Creating PDFドキュメントusing Fragments*** 」セクションの両方で、別のAEM Formsサービスからフォームデザインを取得する方法を示します。 最初の節では、Content Services（非推奨）からフォームデザインを取得します。 2つ目の節では、Assemblerサービスからフォームデザインを取得します。

ファイルシステムなどの固定された場所からフォームデザインを取得する場合は、どちらの方法でも使用できます。 つまり、URI値をXDPファイルに指定するか、インスタンスを使用することができ `com.adobe.idp.Document` ます。

PDFドキュメントの作成時にフォームデザインの場所を指定するURI値を渡すには、この `generatePDFOutput` 方法を使用します。 同様に、PDFドキュメントの作成時に `com.adobe.idp.Document` インスタンスをOutputサービスに渡すには、この `generatePDFOutput2` メソッドを使用します。

出力ストリームをネットワークプリンターに送信する場合は、どちらの方法でも使用できます。 フォームデザインを含む `com.adobe.idp.Document` インスタンスを渡して出力ストリームをプリンターに送信するには、この `sendToPrinter2`メソッドを使用します。 URI値を渡して出力ストリームをプリンターに送信するには、この `sendToPrinter`メソッドを使用します。 「プリンターへの *印刷ストリームの* 送信」セクションでは、この `sendToPrinter` メソッドを使用します。

次のタスクは、Outputサービスを使用して実行できます。

* [PDFドキュメントの作成](creating-document-output-streams.md#creating-pdf-documents)
* [PDF/Aドキュメントの作成](creating-document-output-streams.md#creating-pdf-a-documents)
* [Content Services（非推奨）にあるドキュメントーをOutputサービスに渡す](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)
* [フラグメントを使用したPDFドキュメントの作成](creating-document-output-streams.md#creating-pdf-documents-using-fragments)
* [ファイルへの印刷](creating-document-output-streams.md#printing-to-files)
* [プリントストリームをプリンタに送信する](creating-document-output-streams.md#sending-print-streams-to-printers)
* [複数の出力ファイルの作成](creating-document-output-streams.md#creating-multiple-output-files)
* [検索ルールの作成](creating-document-output-streams.md#creating-search-rules)
* [PDFドキュメントの統合](creating-document-output-streams.md#flattening-pdf-documents)

>[!NOTE]
>
>For more information about the Output service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## PDFドキュメントの作成 {#creating-pdf-documents}

Outputサービスを使用して、指定したフォームデザインとXMLフォームデータに基づくPDFドキュメントを作成できます。 Outputサービスによって作成されるPDFドキュメントは、インタラクティブなPDFドキュメントではありません。 ユーザーはフォームデータを入力したり変更したりできません。

長期ストレージを目的としたPDFドキュメントを作成する場合は、PDF/Aドキュメントを作成することをお勧めします。 (PDF/Aドキュメントの [作成を参照](creating-document-output-streams.md#creating-pdf-a-documents))。

ユーザーがデータを入力できるインタラクティブPDFフォームを作成するには、Formsサービスを使用します。 (インタラクティブPDF formsの [レンダリングを参照](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms))。

>[!NOTE]
>
>For more information about the Output service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary-of-steps}

PDFドキュメントを作成するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Output Clientオブジェクトを作成します。
1. XMLデータソースを参照します。
1. PDFランタイムオプションを設定します。
1. レンダリングの実行時オプションを設定します。
1. PDFドキュメントを生成します。
1. 操作の結果を取得します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めます。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(AEM FormsがJBossにデプロイされている場合に必須)
* jbossall-client.jar(AEM FormsがJBossにデプロイされている場合に必須)

AEM Formsが、JBoss以外のサポート対象のJ2EEアプリケーションサーバーにデプロイされている場合は、adobe-utilities.jarファイルとjbossall-client.jarファイルを、AEM FormsがデプロイされているJ2EEアプリケーションサーバーに固有のJARファイルに置き換える必要があります。

**Output Clientオブジェクトの作成**

プログラムを使用してOutputサービス操作を実行する前に、Outputサービスクライアントオブジェクトを作成する必要があります。 Java APIを使用している場合は、 `OutputClient` オブジェクトを作成します。 Output WebサービスAPIを使用している場合は、 `OutputServiceService` オブジェクトを作成します。

**XMLデータソースの参照**

データをフォームデザインとマージするには、データを含むXMLデータソースを参照する必要があります。 XML要素は、データを入力するすべてのフォームフィールドに存在する必要があります。 XML要素名は、フィールド名と一致する必要があります。 XML要素がフォームフィールドに対応していない場合、またはXML要素名がフィールド名と一致しない場合、XML要素は無視されます。 すべてのXML要素が指定されている場合、XML要素が表示される順序と一致させる必要はありません。

次に、ローン申し込みフォームの例を示します。

![cp_cp_loanformdata](assets/cp_cp_loanformdata.png)

データをこのフォームデザインにマージするには、フォームに対応するXMLデータソースを作成する必要があります。 次のXMLは、住宅ローン申し込みフォームの例に対応するXDP XMLデータソースを表しています。

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

**PDFランタイムオプションの設定**

PDFドキュメントを作成する場合は、ファイルのURIオプションを設定します。 このオプションは、Outputサービスが生成するPDFファイルの名前と場所を指定します。

>[!NOTE]
>
>ファイルURIランタイムオプションを設定する代わりに、Outputサービスから返される複雑なデータ型からPDFドキュメントをプログラムで取得できます。 ただし、ファイルURIランタイムオプションを設定することで、プログラムによってPDFドキュメントを取得するアプリケーションロジックを作成する必要はありません。

**レンダリングの実行時オプションの設定**

レンダリングの実行時オプションは、PDFドキュメントの作成時に設定できます。 これらのオプションは必須ではありませんが（必要なPDFランタイムオプションとは異なり）、Outputサービスのパフォーマンスの向上などのタスクを実行できます。 例えば、Outputサービスでパフォーマンスを向上させるために使用するフォームデザインをキャッシュできます。

タグ付きAcrobatフォームを入力として使用する場合、OutputサービスJavaまたはWebサービスAPIを使用してタグ付き設定を無効にすることはできません。 プログラムでこのオプションをに設定しようとすると、結果のPDFドキュメント `false`は引き続きタグ付けされます。

>[!NOTE]
>
>レンダリングの実行時オプションを指定しない場合は、デフォルト値が使用されます。 実行時オプションのレンダリングについて詳しくは、クラス参照を参照してください。 `RenderOptionsSpec` ( [AEM FormsAPIリファレンスを参照](https://www.adobe.com/go/learn_aemforms_javadocs_63_en))。

**PDFドキュメントの生成**

フォームデータを含む有効なXMLデータソースを参照し、実行時オプションを設定したら、Outputサービスを呼び出して、PDFドキュメントを生成できます。

PDFドキュメントを生成する場合は、OutputサービスでPDFドキュメントを作成するために必要なURI値を指定します。 フォームデザインは、サーバーファイルシステムなどの場所に、またはAEM Formsアプリケーションの一部として保存できます。 Formsアプリケーションの一部として存在するフォームデザイン（または画像ファイルなどの他のリソース）は、コンテンツルートURI値を使用して参照でき `repository:///`ます。 例えば、 *Applications/FormsApplicationという名前のFormsアプリケーション内にある* Loan.xdp *という名前の次のフォームデザインを考えてみましょう*。

![cp_cp_formrepository](assets/cp_cp_formrepository.png)

前の図に示すLoan.xdpファイルにアクセスするには、3番目 `repository:///Applications/FormsApplication/1.0/FormsFolder/` のパラメーターとして `OutputClient` オブジェクトの `generatePDFOutput` メソッドに渡すパラメーターを指定します。 オブジェクトのメ&#x200B;*ソッドに渡す2番目のパラメーターとして、フォーム名(* Loan.xdp `OutputClient``generatePDFOutput` )を指定します。

XDPファイルに画像（またはフラグメントなどの他のリソース）が含まれている場合は、XDPファイルと同じアプリケーションフォルダーにリソースを配置します。 AEM Formsは、コンテンツルートURIをベースパスとして使用し、画像への参照を解決します。 例えば、Loan.xdpファイルに画像が含まれている場合は、必ずにその画像を配置してくだ `Applications/FormsApplication/1.0/FormsFolder/`さい。

>[!NOTE]
>
>FormsアプリケーションのURIは、 `OutputClient` オブジェクトまたはメソッドを呼び出すときに参照でき `generatePDFOutput` ま `generatePrintedOutput` す。

>[!NOTE]
>
>Formsドキュメント内のXDPを参照してPDF開始を作成する完全なクイック開始については、「 [クイックモード（EJBモード）」を参照してください。 Java APIを使用したアプリケーションXDPファイルに基づくPDFドキュメントの作成](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api)。

**操作の結果を取得します**

Outputサービスは、操作の実行後、操作が成功したかどうかを示すステータスXMLデータなどの様々なデータ項目を返します。

**関連トピック**

[Java APIを使用したPDFドキュメントの作成](creating-document-output-streams.md#create-a-pdf-document-using-the-java-api)

[WebサービスAPIを使用したPDFドキュメントの作成](creating-document-output-streams.md#create-a-pdf-document-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[OutputサービスAPIのクイック開始](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Java APIを使用したPDFドキュメントの作成 {#create-a-pdf-document-using-the-java-api}

Output API(Java)を使用してPDFドキュメントを作成します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-output-client.jarなどのクライアントJARファイルを含めます。

1. Output Clientオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `OutputClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. XMLデータソースを参照します。

   * コンストラクターを使用し、XMLファイルの場所を指定する文字列値を渡して、PDFドキュメントの入力に使用されるXMLデータソースを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを作成します。Pass the `java.io.FileInputStream` object.

1. PDFランタイムオプションを設定します。

   * コンストラクタを使用して `PDFOutputOptionsSpec` オブジェクトを作成します。
   * オブジェクトの `PDFOutputOptionsSpec``setFileURI` メソッドを呼び出して、「ファイルURI」オプションを設定します。 Outputサービスが生成するPDFファイルの場所を指定するstring値を渡します。 「ファイルのURI」オプションは、クライアントコンピューターではなく、J2EEアプリケーションAEM Formsをホストするサーバーに対する相対パスです。

1. レンダリングの実行時オプションを設定します。

   * コンストラクタを使用して `RenderOptionsSpec` オブジェクトを作成します。
   * オブジェクトを呼び出して渡すことで、フォームデザインをキャッシュし、Outputサービスのパフォーマンスを向上させ `RenderOptionsSpec` ま `setCacheEnabled``true`す。

   >[!NOTE]
   >
   >入力ドキュメントがAcrobatフォーム（Acrobatで作成されたフォーム）または署名または認証されたXFAドキュメントの場合、 `RenderOptionsSpec` オブジェクトの `setPdfVersion` ドキュメントを使用してPDFバージョンを設定することはできません。 出力PDFドキュメントは、元のPDFバージョンを保持します。 同様に、入力ドキュメントがAcrobatフォーム、署名済みまたは認証済みのXFAドキュメントである場合、 `RenderOptionsSpec` オブジェクトの `setTaggedPDF` メソッドを呼び出してタグ付きAdobe PDFオプションを設定することはできません。

   >[!NOTE]
   >
   >線形化されたPDFオプションは、入力PDFドキュメントが認証済みまたはデジタル署名されている場合は、 `RenderOptionsSpec` オブジェクトの `setLinearizedPDF` メソッドを使用して設定することはできません。 (See [Digitally Signing PDF Documents](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)*.)*

1. PDFドキュメントを生成します。

   Create a PDF document by invoking the `OutputClient` object’s `generatePDFOutput` method and passing the following values:

   * 定義済みリスト `TransformationFormat` 値。 PDFドキュメントを生成するには、を指定し `TransformationFormat.PDF`ます。
   * フォームデザイン名を指定する string 値。
   * フォームデザインが配置されているコンテンツルートを指定するstring値。
   * PDF実行時オプションを含む `PDFOutputOptionsSpec` オブジェクトです。
   * レンダリングの実行時オプションを含む `RenderOptionsSpec` オブジェクトです。
   * フォームデザインとマージするデータを含むXMLデータソースを含む `com.adobe.idp.Document` オブジェクトです。

   The `generatePDFOutput` method returns an `OutputResult` object that contains the results of the operation.

   >[!NOTE]
   >
   >この `generatePDFOutput` メソッドを呼び出してPDFドキュメントを生成する場合、署名または認証されたXFA PDFフォームとはデータを結合できないことに注意してください。 ( [電子署名と認証ドキュメントを参照](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-and-certifying-documents)*)。*

   >[!NOTE]
   >
   >オブ `OutputResult` ジェクトの `getRecordLevelMetaDataList` メソッドが返し `null`*ます。*

   >[!NOTE]
   >
   >オブジェクトのメソッドを呼び出してPDFドキュメントを作成するこ `OutputClient` ともでき `generatePDFOutput2` ます。 (Content Services（非推奨）内のドキュメントーをOutputサービスに [渡すを参照](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)*)。*

1. 操作の結果を取得します。

   * オブジェクトの `com.adobe.idp.Document` メソッドを呼び出して、操作のステータスを表す `generatePDFOutput` オブジェクトを取得し `OutputResult``getStatusDoc` ます。 このメソッドは、操作が成功したかどうかを示すステータスXMLデータを返します。
   * 操作の結果を含む `java.io.File` オブジェクトを作成します。 ファイル名の拡張子が.xmlであることを確認します。
   * オブジェクトのメ `com.adobe.idp.Document` ソッドを呼び出して、 `copyToFile` オブジェクトの内容をファイルにコピーします(メソッドから返された `com.adobe.idp.Document``com.adobe.idp.Document``getStatusDoc` オブジェクトを必ず使用してください)。

   Outputサービスは、オブジェクトのメソッドに渡される引数で指定された場所にPDFドキュメントを書き込みますが、 `PDFOutputOptionsSpec` オブジェクトのドキュメントを呼び出すことで、PDF/Aメソッド `setFileURI` をプログラムで取得でき `OutputResult``getGeneratedDoc` ます。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[クイック開始（EJBモード）: Java APIを使用したPDFドキュメントの作成](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[クイック開始（SOAPモード）: Java APIを使用したPDFドキュメントの作成](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したPDFドキュメントの作成 {#create-a-pdf-document-using-the-web-service-api}

Output API（Webサービス）を使用してPDFドキュメントを作成します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >サーバーホスト `localhost` AEM FormsのIPアドレスに置き換えます。

1. Output Clientオブジェクトを作成します。

   * デフォルトのコンストラクターを使用して `OutputServiceClient` オブジェクトを作成します。
   * コンストラクターを使用して `OutputServiceClient.Endpoint.Address` オブジェクトを作成し `System.ServiceModel.EndpointAddress` ます。 WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/OutputService?blob=mtom`)に渡すstring値を渡します。 属性を使用する必要はありません `lc_version` 。 この属性は、サービス参照を作成する際に使用されます。 ただし、MTOMを使用す `?blob=mtom` るように指定します。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `OutputServiceClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールドにAEM formsのユーザー名を割り当て `OutputServiceClient.ClientCredentials.UserName.UserName`ます。
      * 対応するパスワード値をフィールドに割り当て `OutputServiceClient.ClientCredentials.UserName.Password`ます。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当て `BasicHttpBindingSecurity.Security.Mode`ます。

1. XMLデータソースを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、PDFドキュメントとマージされるXMLデータの格納に使用されます。
   * コンストラクターを呼び出し、フォームデータを含むXMLファイルのファイル位置を表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
   * オブジェクトの `System.IO.FileStream``Read` メソッドを呼び出し、読み取るバイト配列、開始位置およびストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * オブジェクトにバイト配列の内容を割り当てて、 `BLOB` オブジェクト `MTOM` を入力します。

1. PDFランタイムオプションの設定

   * コンストラクタを使用して `PDFOutputOptionsSpec` オブジェクトを作成します。
   * 「File URI」オプションを設定するには、Outputサービスが生成するPDFファイルの場所を指定するstring値を `PDFOutputOptionsSpec` オブジェクトの `fileURI` データメンバーに割り当てます。 「ファイルのURI」オプションは、クライアントコンピューターではなく、J2EEアプリケーションAEM Formsをホストするサーバーに対する相対パスです。

1. レンダリングの実行時オプションを設定します。

   * コンストラクタを使用して `RenderOptionsSpec` オブジェクトを作成します。
   * フォームデザインをキャッシュし、Outputサービスのパフォーマンスを向上させるために、 `true` オブジェクトの `RenderOptionsSpec``cacheEnabled` データメンバーに値を割り当てます。

   >[!NOTE]
   >
   >入力ドキュメントがAcrobatフォーム（Acrobatで作成されたフォーム）または署名または認証されたXFAドキュメントの場合、 `RenderOptionsSpec` オブジェクトの `setPdfVersion` ドキュメントを使用してPDFバージョンを設定することはできません。 出力PDFドキュメントは、元のPDFバージョンを保持します。 同様に、入力ドキュメントがAcrobatフォームまたは署名済みまたは認証済みのXFAドキュメントである場合、 `RenderOptionsSpec` オブジェクトの `setTaggedPDF`*メソッドを呼び出してタグ付きAdobe PDFオプションを設定することはできません。*

   >[!NOTE]
   >
   >入力PDFドキュメントが認証済みまたはデジタル署名されている場合、 `RenderOptionsSpec` オブジェクトの `linearizedPDF` メンバを使用して線形化PDFオプションを設定することはできません。 (See [Digitally Signing PDF Documents](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)*.)*

1. PDFドキュメントを生成します。

   Create a PDF document by invoking the `OutputServiceService` object’s `generatePDFOutput`method and passing the following values:

   * 定義済みリスト `TransformationFormat` 値。 PDFドキュメントを生成するには、を指定し `TransformationFormat.PDF`ます。
   * フォームデザイン名を指定する string 値。
   * フォームデザインが配置されているコンテンツルートを指定するstring値。
   * PDF実行時オプションを含む `PDFOutputOptionsSpec` オブジェクトです。
   * レンダリングの実行時オプションを含む `RenderOptionsSpec` オブジェクトです。
   * フォームデザインとマージするデータを含むXMLデータソースを含む `BLOB` オブジェクトです。
   * メソッドによって入力される `BLOB` オブジェクト `generatePDFOutput` です。 この `generatePDFOutput` メソッドは、ドキュメントを表す生成されたメタデータをこのオブジェクトに入力します。 （このパラメーター値は、Webサービスの呼び出しの場合にのみ必要です）。
   * メソッドによって入力される `BLOB` オブジェクト `generatePDFOutput` です。 この `generatePDFOutput` メソッドは、このオブジェクトに結果データを入力します。 （このパラメーター値は、Webサービスの呼び出しの場合にのみ必要です）。
   * 操作の結果を含む `OutputResult` オブジェクトです。 （このパラメーター値は、Webサービスの呼び出しの場合にのみ必要です）。

   >[!NOTE]
   >
   >この `generatePDFOutput` メソッドを呼び出してPDFドキュメントを生成する場合、署名または認証されたXFA PDFフォームとはデータを結合できないことに注意してください。 ( [電子署名と認証ドキュメントを参照](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-and-certifying-documents)*)。*

   >[!NOTE]
   >
   >オブジェクトのメソッドを呼び出してPDFドキュメントを作成するこ `OutputClient` ともでき `generatePDFOutput2` ます。 (Content Services（非推奨）内のドキュメントーをOutputサービスに [渡すを参照](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)*)。*

1. 操作の結果を取得します。

   * コンストラクターを呼び出し、結果データを含むXMLファイルの場所を表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。 ファイル名の拡張子が.xmlであることを確認します。
   * オブジェクトの `BLOB` メソッド（8番目のパラメーター）によって結果データが入力された `OutputServiceService``generatePDFOutput` オブジェクトのデータ内容を格納するバイト配列を作成します。 オブジェクトの値を取得して、 `BLOB` バイト配列を設定し `MTOM``field`ます。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡して、バイト配列の内容をXMLファイルに書き込み `System.IO.BinaryWriter` ま `Write` す。

   関連トピック

   [手順の概要](creating-document-output-streams.md#summary-of-steps)

   [MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

   [SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

   >[!NOTE]
   >
   >この `OutputServiceService` オブジェクトの `generateOutput` メソッドは非推奨です。

## PDF/Aドキュメントの作成 {#creating-pdf-a-documents}

Outputサービスを使用してPDF/Aドキュメントを作成できます。 PDF/Aはドキュメントのコンテンツを長期間保存するためのアーカイブ形式なので、すべてのフォントが埋め込まれ、ファイルは圧縮されません。 その結果、通常、PDF/A ドキュメントは標準の PDF ドキュメントよりも大きくなります。また、PDF/Aドキュメントには、オーディオおよびビデオコンテンツは含まれません。 他のOutputサービスタスクと同様に、フォームデザインとフォームデザインとマージするデータの両方を提供し、PDF/Aドキュメントを作成します。

PDF/A-1仕様は、aとbの2つの準拠レベルで構成されています。 この2つの主な違いは、論理構造（アクセシビリティ）のサポートに関するものですが、これは準拠レベルbには必要ありません。 準拠レベルに関係なく、PDF/A-1では、生成されるPDF/Aドキュメントにすべてのフォントが埋め込まれます。

PDF/AはPDFドキュメントのアーカイブの標準ですが、標準のPDFドキュメントが会社のニーズを満たしている場合、PDF/Aをアーカイブに使用する必要はありません。 PDF/A標準の目的は、長期間保存できるPDFファイルを確立し、ドキュメントの保存要件を満たすことです。 例えば、URLが時間の経過と共に無効になる可能性があるので、URLをPDF/Aに埋め込むことはできません。

組織は、独自のニーズ、ドキュメントの維持期間、ファイル・サイズに関する考慮事項を評価し、独自のアーカイブ戦略を決定する必要があります。 DocConverterサービスを使用すると、PDFドキュメントがPDF/Aに準拠しているかどうかをプログラムで判断できます。 (「PDF/Aへの準拠 [のプログラムによる決定](/help/forms/developing/pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)」を参照)。

PDF/Aドキュメントは、フォームデザインで指定されたフォントを使用する必要があり、フォントを置き換えることはできません。 その結果、PDFドキュメント内にあるフォントがホストのオペレーティングシステム(OS)で使用できない場合は、例外が発生します。

PDF/AドキュメントをAcrobatで開くと、次の図に示すように、ドキュメントがPDF/Aドキュメントであることを確認するメッセージが表示されます。

![cp_cp_pdfamessage](assets/cp_cp_pdfamessage.png)

>[!NOTE]
>
>AIIMのWebサイトには、PDF/A FAQの節があります。この節はhttps://www.aiim.org/documents/standards/19005-1_FAQ.pdfでアクセスでき [ます](https://www.aiim.org/documents/standards/19005-1_FAQ.pdf)。

>[!NOTE]
>
>For more information about the Output service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-1}

PDF/Aドキュメントを作成するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Output Clientオブジェクトを作成します。
1. XMLデータソースを参照します。
1. PDF/Aランタイムオプションを設定します。
1. レンダリングの実行時オプションを設定します。
1. PDF/Aドキュメントの生成を参照してください。
1. 操作の結果を取得します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。 Javaを使用してカスタムアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めます。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(AEM FormsがJBossにデプロイされている場合に必須)
* jbossall-client.jar(AEM FormsがJBossにデプロイされている場合に必須)

AEM Formsが、JBoss以外のサポート対象のJ2EEアプリケーションサーバーにデプロイされている場合は、adobe-utilities.jarファイルとjbossall-client.jarファイルを、AEM FormsがデプロイされているJ2EEアプリケーションサーバーに固有のJARファイルに置き換える必要があります。

**Output Clientオブジェクトの作成**

プログラムを使用してOutputサービス操作を実行する前に、Outputサービスクライアントオブジェクトを作成する必要があります。 Java APIを使用している場合は、 `OutputClient` オブジェクトを作成します。 Output WebサービスAPIを使用している場合は、 `OutputServiceService` オブジェクトを作成します。

**XMLデータソースの参照**

データをフォームデザインとマージするには、データを含むXMLデータソースを参照する必要があります。 データを入力するフォームフィールドごとに、XML要素が存在する必要があります。 XML要素名は、フィールド名と一致する必要があります。 XML要素がフォームフィールドに対応していない場合、またはXML要素名がフィールド名と一致しない場合、XML要素は無視されます。 すべてのXML要素が指定されている場合、XML要素が表示される順序と一致させる必要はありません。

**PDF/Aランタイムオプションの設定**

PDF/Aドキュメントの作成時に、「ファイルURI」オプションを設定できます。 このURIは、AEM FormsをホストするJ2EEアプリケーションサーバーに対する相対パスです。 つまり、C:\Adobeを設定した場合、ファイルはクライアントコンピューターではなく、サーバー上のフォルダーに書き込まれます。 URIは、Outputサービスが生成するPDF/Aファイルの名前と場所を指定します。

**レンダリングの実行時オプションの設定**

レンダリングの実行時オプションは、PDF/Aドキュメントの作成時に設定できます。 との値を設定できる2つのPDF/A関連のオプション `PDFAConformance` があり `PDFARevisionNumber` ます。 The `PDFAConformance` value refers to how a PDF document adheres to requirements that specify how long-term electronic documents are preserved. このオプションの有効な値は `A` とで `B`す。 レベルaおよびbの準拠について詳しくは、PDF/A-1 ISO仕様(「 *ISO 19005-1ドキュメント管理*」)を参照してください。

この `PDFARevisionNumber` 値は、PDF/Aドキュメントのリビジョン番号を示します。 PDF/Aドキュメントのリビジョン番号について詳しくは、「 *ISO 19005-1ドキュメント管理*」というPDF/A-1 ISO仕様を参照してください。

>[!NOTE]
>
>PDF/A 1Aドキュメントの作成時に、タグ付きAdobe PDFオプションをに設定するこ `false` とはできません。 PDF/A 1Aは、常にタグ付きPDFドキュメントになります。 また、PDF/A 1Bドキュメントを作成する `true` 場合は、タグ付きAdobe PDFオプションをに設定することはできません。 PDF/A 1Bは、常にタグなしPDFドキュメントになります。

**PDF/Aドキュメントの生成**

フォームデータを含む有効なXMLデータソースを参照し、実行時オプションを設定したら、Outputサービスを呼び出して、PDF/Aドキュメントを生成できます。

**操作の結果を取得します**

Outputサービスは、操作の実行後、操作が成功したかどうかを示すXMLデータなどの様々なデータ項目を返します。

**関連トピック**

[Java APIを使用したPDF/Aドキュメントの作成](creating-document-output-streams.md#create-a-pdf-a-document-using-the-java-api)

[WebサービスAPIを使用したPDF/Aドキュメントの作成](creating-document-output-streams.md#create-a-pdf-a-document-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[OutputサービスAPIのクイック開始](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Java APIを使用したPDF/Aドキュメントの作成 {#create-a-pdf-a-document-using-the-java-api}

Output API(Java)を使用してPDF/Aドキュメントを作成します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-output-client.jarなどのクライアントJARファイルを含めます。

1. Output Clientオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `OutputClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. XMLデータソースを参照します。

   * コンストラクターを使用し、XMLファイルの場所を指定する文字列値を渡して、PDF/Aドキュメントへの入力に使用されるXMLデータソースを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PDF/Aランタイムオプションを設定します。

   * コンストラクタを使用して `PDFOutputOptionsSpec` オブジェクトを作成します。
   * オブジェクトの `PDFOutputOptionsSpec``setFileURI` メソッドを呼び出して、「ファイルURI」オプションを設定します。 Outputサービスが生成するPDFファイルの場所を指定するstring値を渡します。 「ファイルのURI」オプションは、クライアントコンピューターではなく、J2EEアプリケーションAEM Formsをホストするサーバーに対する相対パスです。

1. レンダリングの実行時オプションを設定します。

   * コンストラクタを使用して `RenderOptionsSpec` オブジェクトを作成します。
   * オブジェクトの `PDFAConformance` メソッドを呼び出し、準拠レベルを指定する `RenderOptionsSpec``setPDFAConformance``PDFAConformance` 列挙値を渡して、値を設定します。 例えば、準拠レベルAを指定するには、を渡し `PDFAConformance.A`ます。
   * オブジェクトの `PDFARevisionNumber` メソッドを呼び出して渡すことで、 `RenderOptionsSpec` 値を設定し `setPDFARevisionNumber``PDFARevisionNumber.Revision_1`ます。

   >[!NOTE]
   >
   >PDF/AドキュメントのPDFバージョンは、オブジェクトの `RenderOptionsSpec``setPdfVersion`*メソッドに指定した値に関係なく1.4になります。*

1. PDF/Aドキュメントの生成を参照してください。

   オブジェクトの `OutputClient``generatePDFOutput` メソッドを呼び出し、次の値を渡して、PDF/Aドキュメントを作成します。

   * 定義済みリスト `TransformationFormat` 値。 PDF/Aドキュメントを生成するには、を指定し `TransformationFormat.PDFA`ます。
   * フォームデザイン名を指定する string 値。
   * フォームデザインが配置されているコンテンツルートを指定するstring値。
   * PDF実行時オプションを含む `PDFOutputOptionsSpec` オブジェクトです。
   * レンダリングの実行時オプションを含む `RenderOptionsSpec` オブジェクトです。
   * フォームデザインとマージするデータが含まれるXMLデータソースを含む `com.adobe.idp.Document` オブジェクトです。

   The `generatePDFOutput` method returns an `OutputResult` object that contains the results of the operation.

   >[!NOTE]
   >
   >オブ `OutputResult` ジェクトの `getRecordLevelMetaDataList` メソッドが返し `null`ます。

   >[!NOTE]
   >
   >オブジェクトの `OutputClient` 2ドキュメントを呼び出して、PDF/Aメソッドを作成することもでき `generatePDFOutput`ます。 (Content Services（非推奨）内のドキュメントーをOutputサービスに [渡すを参照](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service))。

1. 操作の結果を取得します。

   * オブジェクトのメソッドを呼び出して、その `com.adobe.idp.Document` メソッドのステータスを表す `generatePDFOutput` オブジェクトを作成し `OutputResult``getStatusDoc` ます。
   * 操作の結果を含む `java.io.File` オブジェクトを作成します。 ファイル名の拡張子が.xmlであることを確認します。
   * オブジェクトのメ `com.adobe.idp.Document` ソッドを呼び出して、 `copyToFile` オブジェクトの内容をファイルにコピーします(メソッドから返された `com.adobe.idp.Document``com.adobe.idp.Document``getStatusDoc` オブジェクトを必ず使用してください)。

   >[!NOTE]
   >
   >Outputサービスは、PDF/Aドキュメントを、オブジェクトのメソッドに渡される引数で指定された場所に書き込みますが、 `PDFOutputOptionsSpec` オブジェクトのドキュメントを呼び出すことで、PDF/Aメソッド `setFileURI` をプログラムで取得でき `OutputResult``getGeneratedDoc` ます。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[クイック開始（SOAPモード）: Java APIを使用したPDF/Aドキュメントの作成](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-a-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

### WebサービスAPIを使用したPDF/Aドキュメントの作成 {#create-a-pdf-a-document-using-the-web-service-api}

Output API（Webサービス）を使用してPDF/Aドキュメントを作成します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >サーバーホスト `localhost` AEM FormsのIPアドレスに置き換えます。

1. Output Clientオブジェクトを作成します。

   * デフォルトのコンストラクターを使用して `OutputServiceClient` オブジェクトを作成します。
   * コンストラクターを使用して `OutputServiceClient.Endpoint.Address` オブジェクトを作成し `System.ServiceModel.EndpointAddress` ます。 WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/OutputService?blob=mtom`)に渡すstring値を渡します。 属性を使用する必要はありません `lc_version` 。 この属性は、サービス参照を作成する際に使用されます。 ただし、MTOMを使用す `?blob=mtom` るように指定します。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `OutputServiceClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールドにAEM formsのユーザー名を割り当て `OutputServiceClient.ClientCredentials.UserName.UserName`ます。
      * 対応するパスワード値をフィールドに割り当て `OutputServiceClient.ClientCredentials.UserName.Password`ます。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当て `BasicHttpBindingSecurity.Security.Mode`ます。

1. XMLデータソースを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、PDF/Aドキュメントと統合されるデータの保存に使用されます。
   * コンストラクターを呼び出し、暗号化するPDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
   * オブジェクトの `System.IO.FileStream``Read` メソッドを呼び出し、読み取るバイト配列、開始位置およびストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * オブジェクトにバイト配列の内容を割り当てて、 `BLOB` オブジェクト `MTOM` を入力します。

1. PDF/Aランタイムオプションを設定します。

   * コンストラクタを使用して `PDFOutputOptionsSpec` オブジェクトを作成します。
   * 「File URI」オプションを設定するには、Outputサービスが生成するPDFファイルの場所を指定するstring値を `PDFOutputOptionsSpec` オブジェクトの `fileURI` データメンバーに割り当てます。 「ファイルのURI」オプションは、クライアントコンピューターではなく、J2EEアプリケーションサーバーがホストするAEM Formsに対する相対パスです

1. レンダリングの実行時オプションを設定します。

   * コンストラクタを使用して `RenderOptionsSpec` オブジェクトを作成します。
   * 値を設定するには、 `PDFAConformance` オブジェクトの `PDFAConformance` データメンバに `RenderOptionsSpec``PDFAConformance` 列挙値を割り当てます。 例えば、準拠レベルAを指定するには、このデータメンバ `PDFAConformance.A` ーに割り当てます。
   * 値を設定するには、 `PDFARevisionNumber` オブジェクトの `PDFARevisionNumber` データメンバに `RenderOptionsSpec``PDFARevisionNumber` 列挙値を割り当てます。 このデータメンバ `PDFARevisionNumber.Revision_1` ーに割り当てます。

   >[!NOTE]
   >
   >PDF/AドキュメントのPDFバージョンは、指定した値に関係なく1.4です。

1. PDF/Aドキュメントの生成を参照してください。

   Create a PDF document by invoking the `OutputServiceService` object’s `generatePDFOutput`method and passing the following values:

   * TransformationFormat定義済みリスト値。 PDFドキュメントを生成するには、を指定し `TransformationFormat.PDFA`ます。
   * フォームデザイン名を指定する string 値。
   * フォームデザインが配置されているコンテンツルートを指定するstring値。
   * PDF実行時オプションを含む `PDFOutputOptionsSpec` オブジェクトです。
   * レンダリングの実行時オプションを含む `RenderOptionsSpec` オブジェクトです。
   * フォームデザインとマージするデータを含むXMLデータソースを含む `BLOB` オブジェクトです。
   * メソッドによって入力される `BLOB` オブジェクト `generatePDFOutput` です。 この `generatePDFOutput` メソッドは、ドキュメントを表す生成されたメタデータをこのオブジェクトに入力します。 （このパラメーター値は、Webサービス呼び出しのみで必要です）。
   * メソッドによって入力される `BLOB` オブジェクト `generatePDFOutput` です。 この `generatePDFOutput` メソッドは、このオブジェクトに結果データを入力します。 （このパラメーター値は、Webサービス呼び出しのみで必要です）。
   * 操作の結果を含む `OutputResult` オブジェクトです。 （このパラメーター値は、Webサービス呼び出しのみで必要です）。

   >[!NOTE]
   >
   >オブジェクトの `OutputClient` 2ドキュメントを呼び出して、PDF/Aメソッドを作成することもでき `generatePDFOutput`ます。 (Content Services（非推奨）内のドキュメントーをOutputサービスに [渡すを参照](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service))。

1. 操作の結果を取得します。

   * コンストラクターを呼び出し、結果データを含むXMLファイルの場所を表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。 ファイル名の拡張子が.xmlであることを確認します。
   * オブジェクトの `BLOB` メソッド（8番目のパラメーター）によって結果データが入力された `OutputServiceService``generatePDFOutput` オブジェクトのデータ内容を格納するバイト配列を作成します。 オブジェクトのフィールドの値を取得して、 `BLOB` バイト配列を設定し `MTOM` ます。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡して、バイト配列の内容をXMLファイルに書き込み `System.IO.BinaryWriter` ま `Write` す。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Content Services（非推奨）にあるドキュメントーをOutputサービスに渡す {#passing-documents-located-in-content-services-deprecated-to-the-output-service}

Outputサービスは、通常、XDPファイルとして保存され、Designerで作成されるフォームデザインに基づく非インタラクティブPDFフォームをレンダリングします。 フォームデザインを含む `com.adobe.idp.Document` オブジェクトをOutputサービスに渡すことができます。 次に、Outputサービスは、オブジェクト内のフォームデザインをレンダリングし `com.adobe.idp.Document` ます。

オブジェクトをOutputサービスに渡す利点の1つは、他の `com.adobe.idp.Document` AEM Formsサービス操作がインスタンスを返すことで `com.adobe.idp.Document` す。 つまり、別のサービス操作から `com.adobe.idp.Document` インスタンスを取得してレンダリングできます。 例えば、次の図に示すように、XDPファイルがという名前のContent Services（非推奨）ノードに格納されている `/Company Home/Form Designs`とします。

プログラムを使用してContent Services（非推奨）からLoan.xdpを取得し、そのXDPファイルを `com.adobe.idp.Document` オブジェクト内のOutputサービスに渡すことができます。

>[!NOTE]
>
>For more information about the Forms service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-2}

Content Services（非推奨）から取得したドキュメントをOutputサービスに渡すには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. 出力とドキュメント管理クライアントAPIオブジェクトを作成します。
1. Content Services（非推奨）からフォームデザインを取得します。
1. 非インタラクティブPDFフォームをレンダリングします。
1. データストリームでアクションを実行します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを含めます。

**出力とドキュメント管理クライアントAPIオブジェクトの作成**

プログラムでOutputサービスAPI操作を実行する前に、OutputクライアントAPIオブジェクトを作成します。 また、このワークフローはContent Services（非推奨）からXDPファイルを取得するので、ドキュメント管理APIオブジェクトを作成します。

**Content Services（非推奨）からフォームデザインを取得する**

JavaまたはWebサービスAPIを使用して、Content Services（非推奨）からXDPファイルを取得します。 XDPファイルは、インスタンス(Webサービスを使用している場合は `com.adobe.idp.Document` インスタンス)内で返され `BLOB` ます。 その後、この `com.adobe.idp.Document` インスタンスをOutputサービスに渡すことができます。

**非インタラクティブPDFフォームのレンダリング**

非インタラクティブフォームをレンダリングするには、Content Services（非推奨）から返された `com.adobe.idp.Document` インスタンスをOutputサービスに渡します。

>[!NOTE]
>
>とgという2つの新しいメソッド `generatePDFOutput2`は、フォームデザインを含む `eneratePrintedOutput2`オブジェクトを `com.adobe.idp.Document` 受け入れます。 印刷ストリームをネットワークプリンター `com.adobe.idp.Document`に送信する場合、フォームデザインを含むフォームをOutputサービスに渡すこともできます。

**フォームデータストリームを使用したアクションの実行**

非インタラクティブフォームをPDFファイルとして保存できます。 フォームは、Adobe ReaderまたはAcrobatで表示できます。

**関連トピック**

[Java APIを使用してOutput Serviceにドキュメントを渡す](creating-document-output-streams.md#pass-documents-to-the-output-service-using-the-java-api)

[WebサービスAPIを使用してOutputサービスにドキュメントを渡す](creating-document-output-streams.md#pass-documents-to-the-output-service-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[OutputサービスAPIのクイック開始](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

[フラグメントを使用したPDFドキュメントの作成](creating-document-output-streams.md#creating-pdf-documents-using-fragments)

### Java APIを使用してOutput Serviceにドキュメントを渡す {#pass-documents-to-the-output-service-using-the-java-api}

OutputサービスとContent Services（非推奨）API(Java)を使用してContent Services（非推奨）から取得したドキュメントを渡します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-output-client.jarやadobe-contentservices-client.jarなどのクライアントJARファイルを含めます。

1. Outputとドキュメント管理クライアントAPIオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。（[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照。）
   * Create an `OutputClient` object by using its constructor and passing the `ServiceClientFactory` object.
   * コンストラクタを使用して `DocumentManagementServiceClientImpl` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. Content Services（非推奨）からフォームデザインを取得します。

   オブジェクトの `DocumentManagementServiceClientImpl``retrieveContent` メソッドを呼び出し、次の値を渡します。

   * コンテンツが追加されるストアを指定するstring値です。 The default store is `SpacesStore`. この値は必須のパラメータです。
   * 取得するコンテンツの完全修飾パスを指定するstring値(例えば、 `/Company Home/Form Designs/Loan.xdp`)。 この値は必須のパラメータです。
   * バージョンを指定するstring値。 この値はオプションのパラメーターであり、空の文字列を渡すことができます。 この場合、最新バージョンが取得されます。

   この `retrieveContent` メソッドは、XDPファイルを含む `CRCResult` オブジェクトを返します。 オブジェクトの `com.adobe.idp.Document` メソッドを呼び出して、 `CRCResult` インスタンスを取得し `getDocument` ます。

1. 非インタラクティブPDFフォームをレンダリングします。

   オブジェクトの `OutputClient``generatePDFOutput2` メソッドを呼び出し、次の値を渡します。

   * 定義済みリスト `TransformationFormat` 値。 PDFドキュメントを生成するには、を指定し `TransformationFormat.PDF`ます。
   * 画像などの追加リソースが存在するコンテンツルートを指定するstring値です。
   * フォームデザインを表す `com.adobe.idp.Document` オブジェクト(オブジェクトのメソッドから返される `CRCResult` インスタンスを使用 `getDocument` )。
   * PDF実行時オプションを含む `PDFOutputOptionsSpec` オブジェクトです。
   * レンダリングの実行時オプションを含む `RenderOptionsSpec` オブジェクトです。
   * フォームデザインとマージするデータを含むXMLデータソースを含む `com.adobe.idp.Document` オブジェクトです。

   The `generatePDFOutput2` method returns an `OutputResult` object that contains the results of the operation.

1. フォームデータストリームでアクションを実行します。

   * オブジェクトの `com.adobe.idp.Document` メソッドを呼び出して、非インタラクティブフォームを表す `OutputResult``getGeneratedDoc` オブジェクトを取得します。
   * 操作の結果を含む `java.io.File` オブジェクトを作成します。 ファイル名の拡張子が.pdfであることを確認します。
   * オブジェクトのメ `com.adobe.idp.Document` ソッドを呼び出して、 `copyToFile` オブジェクトの内容をファイルにコピーします(メソッドから返された `com.adobe.idp.Document``com.adobe.idp.Document``getGeneratedDoc` オブジェクトを必ず使用してください)。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[クイック開始（EJBモード）: Java APIを使用してOutputサービスにドキュメントを渡す](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[クイック開始（SOAPモード）: Java APIを使用してOutputサービスにドキュメントを渡す](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用してOutputサービスにドキュメントを渡す {#pass-documents-to-the-output-service-using-the-web-service-api}

OutputサービスとContent Services（非推奨）API（Webサービス）を使用してContent Services（非推奨）から取得したドキュメントを渡します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 このクライアントアプリケーションは2つのAEM Formsサービスを呼び出すので、2つのサービス参照を作成します。 Outputサービスに関連付けられているサービス参照には、次のWSDL定義を使用します。 `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   ドキュメント管理サービスに関連付けられたサービス参照に対して、次のWSDL定義を使用します。 `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`.

   この `BLOB` データ型は両方のサービス参照に共通なので、使用する場合は `BLOB` データ型を完全に限定します。 対応するWebサービスクイック開始では、すべての `BLOB` インスタンスが完全修飾されます。

   >[!NOTE]
   >
   >サーバーホスト `localhost` AEM FormsのIPアドレスに置き換えます。

1. Outputとドキュメント管理クライアントAPIオブジェクトを作成します。

   * デフォルトのコンストラクターを使用して `OutputServiceClient` オブジェクトを作成します。
   * コンストラクターを使用して `OutputServiceClient.Endpoint.Address` オブジェクトを作成し `System.ServiceModel.EndpointAddress` ます。 WSDLをFormsサービス(例えば、 `http://localhost:8080/soap/services/OutputService?blob=mtom`)に渡すstring値を渡します。 属性を使用する必要はありません `lc_version` 。 この属性は、サービス参照を作成する場合に使用されます)。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `OutputServiceClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールドにAEM formsのユーザー名を割り当て `OutputServiceClient.ClientCredentials.UserName.UserName`ます。
      * 対応するパスワード値をフィールドに割り当て `OutputServiceClient.ClientCredentials.UserName.Password`ます。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
   * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当て `BasicHttpBindingSecurity.Security.Mode`ます。

   >[!NOTE]
   >
   >サー `DocumentManagementServiceClient`ビスクライアントに対してこの手順を繰り返します。

1. Content Services（非推奨）からフォームデザインを取得します。

   オブジェクトのメソッドを呼び出し、次の値を渡して、 `DocumentManagementServiceClient``retrieveContent` コンテンツを取得します。

   * コンテンツが追加されるストアを指定するstring値です。 The default store is `SpacesStore`. この値は必須のパラメータです。
   * 取得するコンテンツの完全修飾パスを指定するstring値(例えば、 `/Company Home/Form Designs/Loan.xdp`)。 この値は必須のパラメータです。
   * バージョンを指定するstring値。 この値はオプションのパラメーターであり、空の文字列を渡すことができます。 この場合、最新バージョンが取得されます。
   * ブラウズリンクの値を格納する文字列出力パラメーター。
   * コンテンツを格納する `BLOB` 出力パラメーター。 この出力パラメーターを使用して、コンテンツを取得できます。
   * コンテンツ属性を格納する `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` 出力パラメーター。
   * 出 `CRCResult` 力パラメータ。 このオブジェクトを使用する代わりに、 `BLOB` 出力パラメーターを使用してコンテンツを取得できます。

1. 非インタラクティブPDFフォームをレンダリングします。

   オブジェクトの `OutputServiceClient``generatePDFOutput2` メソッドを呼び出し、次の値を渡します。

   * 定義済みリスト `TransformationFormat` 値。 PDFドキュメントを生成するには、を指定し `TransformationFormat.PDF`ます。
   * 画像などの追加リソースが存在するコンテンツルートを指定するstring値です。
   * フォームデザインを表す `BLOB` オブジェクト(Content Services（非推奨）から返される `BLOB` インスタンスを使用)。
   * PDF実行時オプションを含む `PDFOutputOptionsSpec` オブジェクトです。
   * レンダリングの実行時オプションを含む `RenderOptionsSpec` オブジェクトです。
   * フォームデザインとマージするデータを含むXMLデータソースを含む `BLOB` オブジェクトです。
   * メソッドによって入力される出力 `BLOB` オブジェクト `generatePDFOutput2` です。 この `generatePDFOutput2` メソッドは、ドキュメントを表す生成されたメタデータをこのオブジェクトに入力します。 （このパラメーター値は、Webサービスの呼び出しの場合にのみ必要です）。
   * 操作の結果を含む出力 `OutputResult` オブジェクトです。 （このパラメーター値は、Webサービスの呼び出しの場合にのみ必要です）。

   この `generatePDFOutput2` メソッドは、非インタラクティブPDFフォームを含む `BLOB` オブジェクトを返します。

1. フォームデータストリームでアクションを実行します。

   * Create a `System.IO.FileStream` object by invoking its constructor. インタラクティブPDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * メソッドから取得した `BLOB` オブジェクトの内容を格納するバイト配列を作成し `generatePDFOutput2` ます。 オブジェクトのデータメンバーの値を取得して、 `BLOB` バイト配列を入力し `MTOM` ます。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡して、バイト配列の内容をPDFファイルに書き込み `System.IO.BinaryWriter` ま `Write` す。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## リポジトリ内のドキュメントーをOutputサービスに渡す {#passing-documents-located-in-the-repository-to-the-output-service}

Outputサービスは、通常、XDPファイルとして保存され、Designerで作成されるフォームデザインに基づく非インタラクティブPDFフォームをレンダリングします。 フォームデザインを含む `com.adobe.idp.Document` オブジェクトをOutputサービスに渡すことができます。 次に、Outputサービスは、オブジェクト内のフォームデザインをレンダリングし `com.adobe.idp.Document` ます。

オブジェクトをOutputサービスに渡す利点の1つは、他の `com.adobe.idp.Document` AEM Formsサービス操作がインスタンスを返すことで `com.adobe.idp.Document` す。 つまり、別のサービス操作から `com.adobe.idp.Document` インスタンスを取得してレンダリングできます。 例えば、次の図に示すように、XDPファイルがAEM Formsリポジトリに保存されているとします。

![pd_pd_formrepository](assets/pd_pd_formrepository.png)

FormsFolder ** フォルダーは、AEM Formsリポジトリ内のユーザー定義の場所です（この場所は例で、デフォルトでは存在しません）。 この例では、Loan.xdpという名前のフォームデザインがこのフォルダー内にあります。 フォームデザインに加えて、画像などの他のフォームコラテラルもこの場所に保存できます。 AEM Formsリポジトリ内のリソースへのパスは次のとおりです。

`Applications/Application-name/Application-version/Folder.../Filename`

プログラムを使用して、AEM FormsリポジトリからLoan.xdpを取得し、オブジェクト内のOutputサービスに渡すことができ `com.adobe.idp.Document` ます。

リポジトリ内にあるXDPファイルに基づいてPDFを作成するには、次の2つの方法があります。 XDPの場所は、参照によって渡すことも、プログラムでリポジトリからXDPを取得して、XDPファイル内のOutputサービスに渡すこともできます。

[クイック開始（EJBモード）: Java APIを使用したアプリケーションXDPファイルに基づくPDFドキュメントの作成](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api) （参照によるXDPファイルの場所の渡し方法を示します）。

[クイック開始（EJBモード）: Java APIを使用してAEM Formsリポジトリ内のドキュメントーをOutputサービスに渡す(プログラムでAEM FormsリポジトリからXDPファイルを取得し、インスタンス内でOutputサービスに渡す方法を示し](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api)`com.adobe.idp.Document` ます)。 (このタスクの実行方法について説明します)。

>[!NOTE]
>
>For more information about the Forms service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-3}

AEM Formsリポジトリから取得したドキュメントをOutputサービスに渡すには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. 出力とドキュメント管理クライアントAPIオブジェクトを作成します。
1. AEM Formsリポジトリからフォームデザインを取得します。
1. 非インタラクティブPDFフォームをレンダリングします。
1. データストリームでアクションを実行します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを含めます。

**出力とドキュメント管理クライアントAPIオブジェクトの作成**

プログラムでOutputサービスAPI操作を実行する前に、OutputクライアントAPIオブジェクトを作成します。 また、このワークフローはContent Services（非推奨）からXDPファイルを取得するので、ドキュメント管理APIオブジェクトを作成します。

**AEM Formsリポジトリからフォームデザインを取得する**

Repository APIを使用して、AEM FormsリポジトリからXDPファイルを取得します。 ( [Reading Resources](/help/forms/developing/aem-forms-repository.md#reading-resources)を参照)。

XDPファイルは、インスタンス(Webサービスを使用している場合は `com.adobe.idp.Document` インスタンス)内で返され `BLOB` ます。 その後、この `com.adobe.idp.Document` インスタンスをOutputサービスに渡すことができます。

**非インタラクティブPDFフォームのレンダリング**

非インタラクティブフォームをレンダリングするには、AEM FormsリポジトリAPIを使用して返された `com.adobe.idp.Document` インスタンスを渡します。

>[!NOTE]
>
>フォームデザインを含む `generatePDFOutput2`オブジェクトを、という名前で `generatePrintedOutput2``com.adobe.idp.Document`受け入れる2つの新しいメソッドが追加されました。 印刷ストリームをネットワークプリンター `com.adobe.idp.Document` に送信する場合は、フォームデザインを含むフォームをOutputサービスに渡すこともできます。

**フォームデータストリームを使用したアクションの実行**

非インタラクティブフォームをPDFファイルとして保存できます。 フォームは、Adobe ReaderまたはAcrobatで表示できます。

**関連トピック**

[Java APIを使用して、リポジトリ内のドキュメントーをOutputサービスに渡す](creating-document-output-streams.md#pass-documents-located-in-the-repository-to-the-output-service-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[OutputサービスAPIのクイック開始](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

ResourceRepositoryClient

### Java APIを使用して、リポジトリ内のドキュメントーをOutputサービスに渡す {#pass-documents-located-in-the-repository-to-the-output-service-using-the-java-api}

OutputサービスとRepository API(Java)を使用して、リポジトリから取得したドキュメントを渡します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-output-client.jarやadobe-repository-client.jarなどのクライアントJARファイルを含めます。

1. Outputとドキュメント管理クライアントAPIオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。（[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照。）
   * Create an `OutputClient` object by using its constructor and passing the `ServiceClientFactory` object.
   * コンストラクタを使用して `DocumentManagementServiceClientImpl` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. AEM Formsリポジトリからフォームデザインを取得します。

   オブジェクトの `ResourceRepositoryClient``readResourceContent` メソッドを呼び出し、URIの場所を指定するstring値をXDPファイルに渡します。 例えば、`/Applications/FormsApplication/1.0/FormsFolder/Loan.xdp` のようになります。この値は必須です。 このメソッドは、XDPファイルを表す `com.adobe.idp.Document` インスタンスを返します。

1. 非インタラクティブPDFフォームをレンダリングします。

   オブジェクトの `OutputClient``generatePDFOutput2` メソッドを呼び出し、次の値を渡します。

   * 定義済みリスト `TransformationFormat` 値。 PDFドキュメントを生成するには、を指定し `TransformationFormat.PDF`ます。
   * 画像などの追加リソースが存在するコンテンツルートを指定するstring値です。 例： `repository:///Applications/FormsApplication/1.0/FormsFolder/`
   * フォームデザインを表す `com.adobe.idp.Document` オブジェクト(オブジェクトのメソッドから返される `ResourceRepositoryClient` インスタンスを使用 `readResourceContent` )。
   * PDF実行時オプションを含む `PDFOutputOptionsSpec` オブジェクトです。
   * レンダリングの実行時オプションを含む `RenderOptionsSpec` オブジェクトです。
   * フォームデザインとマージするデータを含むXMLデータソースを含む `com.adobe.idp.Document` オブジェクトです。

   The `generatePDFOutput2` method returns an `OutputResult` object that contains the results of the operation.

1. フォームデータストリームでアクションを実行します。

   * オブジェクトの `com.adobe.idp.Document` メソッドを呼び出して、非インタラクティブフォームを表す `OutputResult``getGeneratedDoc` オブジェクトを取得します。
   * 操作の結果を含む `java.io.File` オブジェクトを作成します。 ファイル名の拡張子が.pdfであることを確認します。
   * オブジェクトのメ `com.adobe.idp.Document` ソッドを呼び出して、 `copyToFile` オブジェクトの内容をファイルにコピーします(メソッドから返された `com.adobe.idp.Document``com.adobe.idp.Document``getGeneratedDoc` オブジェクトを必ず使用してください)。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[クイック開始（EJBモード）: Java APIを使用して、AEM Formsリポジトリ内のドキュメントをOutputサービスに渡す](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## フラグメントを使用したPDFドキュメントの作成 {#creating-pdf-documents-using-fragments}

OutputサービスとAssemblerサービスを使用して、フラグメントに基づく出力ストリーム(PDFドキュメントなど)を作成できます。 Assemblerサービスは、複数のXDPファイル内のフラグメントに基づいてXDPドキュメントをアセンブリします。 アセンブリ済みのXDPドキュメントがOutputサービスに渡され、そこでPDFドキュメントが作成されます。 このワークフローは、生成中のPDFドキュメントを示しますが、Outputサービスは、このワークフロー用に、ZPLなどの他の出力タイプを生成できます。 PDFドキュメントは、ディスカッションの目的でのみ使用します。

次の図に、このワークフローを示します。

![cp_cp_outputassemblefragments](assets/cp_cp_outputassemblefragments.png)

「Fragmentsを使用したPDFドキュメントの **&#x200B;作成」を読む前に、Assemblerサービスを使用して複数のXDPドキュメントをアセンブリする方法を理解することをお勧めします。 (複数のXDPフラグメントの [アセンブリを参照](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments))。

>[!NOTE]
>
>また、Assemblerサービスによってアセンブリされたフォームデザインを、Outputサービスの代わりにFormsサービスに渡すこともできます。 OutputサービスとFormsサービスの主な違いは、FormsサービスでインタラクティブPDFドキュメントが生成され、Outputサービスで非インタラクティブPDFドキュメントが生成される点です。 また、Formsサービスでは、ZPLのようなプリンターベースの出力ストリームを生成できません。

>[!NOTE]
>
>For more information about the Output service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-4}

フラグメントに基づいてPDFドキュメントを作成するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. OutputおよびAssembler Clientオブジェクトを作成します。
1. Assemblerサービスを使用してフォームデザインを生成します。
1. Outputサービスを使用してPDFドキュメントを生成します。
1. PDFドキュメントをPDFファイルとして保存します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めます。

**OutputおよびAssembler Clientオブジェクトの作成**

プログラムでOutputサービスAPI操作を実行する前に、OutputクライアントAPIオブジェクトを作成します。 また、このワークフローはAssemblerサービスを呼び出してフォームデザインを作成するので、Assembler Client APIオブジェクトを作成します。

**Assemblerサービスを使用したフォームデザインの生成**

Assemblerサービスを使用して、フラグメントを使用してフォームデザインを生成します。 Assemblerサービスは、フォームデザインを含む `com.adobe.idp.Document` インスタンスを返します。

**Outputサービスを使用したPDFドキュメントの生成**

Outputサービスを使用して、Assemblerサービスが作成したフォームデザインを使用してPDFドキュメントを生成できます。 Assemblerサービスが返した `com.adobe.idp.Document` インスタンスをOutputサービスに渡します。

**PDFドキュメントをPDFファイルとして保存**

OutputサービスがPDFドキュメントを生成したら、それをPDFファイルとして保存できます。

**関連トピック**

[Java APIを使用したフラグメントに基づくPDFドキュメントの作成](creating-document-output-streams.md#create-a-pdf-document-based-on-fragments-using-the-java-api)

[WebサービスAPIを使用したフラグメントに基づくPDFドキュメントの作成](creating-document-output-streams.md#create-a-pdf-document-based-on-fragments-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[OutputサービスAPIのクイック開始](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

[複数のXDPフラグメントのアセンブリ](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments)

[PDFドキュメントの作成](creating-document-output-streams.md#creating-pdf-documents)

### Java APIを使用したフラグメントに基づくPDFドキュメントの作成 {#create-a-pdf-document-based-on-fragments-using-the-java-api}

Output Service APIとAssembler Service API(Java)を使用して、フラグメントに基づいてPDFドキュメントを作成します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-output-client.jarなどのクライアントJARファイルを含めます。

1. OutputおよびAssembler Clientオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `OutputClient` object by using its constructor and passing the `ServiceClientFactory` object.
   * Create an `AssemblerServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. Assemblerサービスを使用してフォームデザインを生成します。

   オブジェクトの `AssemblerServiceClient``invokeDDX` メソッドを呼び出し、次の必須値を渡します。

   * 使用するDDXドキュメントを表す `com.adobe.idp.Document` オブジェクトです。
   * 入力XDPファイルを含む `java.util.Map` オブジェクトです。
   * デフォルトフォントやジョブログレベルなど、実行時のオプションを指定する `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` オブジェクト。

   この `invokeDDX` メソッドは、アセンブリされたXDPドキュメントを含む `com.adobe.livecycle.assembler.client.AssemblerResult` オブジェクトを返します。 アセンブリ済みのXDPドキュメントを取得するには、次の操作を実行します。

   * オブジェクトの `AssemblerResult` メソッドを呼び出し `getDocuments` ます。 このメソッドは、 `java.util.Map` オブジェクトを返します。
   * オブジェクトを繰り返し処理して、結果のオブジ `java.util.Map``com.adobe.idp.Document` ェクトを見つけます。
   * オブジェクトの `com.adobe.idp.Document``copyToFile` メソッドを呼び出して、アセンブリ済みのXDPドキュメントを抽出します。


1. Outputサービスを使用してPDFドキュメントを生成します。

   オブジェクトの `OutputClient``generatePDFOutput2` メソッドを呼び出し、次の値を渡します。

   * 定義済みリスト `TransformationFormat` 値。 PDFドキュメントを生成するには、 `TransformationFormat.PDF`
   * 画像などの追加リソースが存在するコンテンツルートを指定するstring値です
   * フォームデザインを表す `com.adobe.idp.Document` オブジェクト（Assemblerサービスから返されるインスタンスを使用）
   * PDF実行時オプションを含む `PDFOutputOptionsSpec` オブジェクト
   * レンダリングの実行時オプションを含む `RenderOptionsSpec` オブジェクト
   * フォームデザインとマージするデータを含むXMLデータソースを含む `com.adobe.idp.Document` オブジェクトです

   The `generatePDFOutput2` method returns an `OutputResult` object that contains the results of the operation

1. PDFドキュメントをPDFファイルとして保存します。

   * オブジェクトの `com.adobe.idp.Document` メソッドを呼び出して、PDFドキュメントを表す `OutputResult` オブジェクトを取得し `getGeneratedDoc` ます。
   * 操作の結果を含む `java.io.File` オブジェクトを作成します。 ファイル名の拡張子が.pdfであることを確認します。
   * Invoke the `com.adobe.idp.Document` object’s `copyToFile` method to copy the contents of the `com.adobe.idp.Document` object to the file. ( `com.adobe.idp.Document``getGeneratedDoc` メソッドが返したオブジェクトを使用していることを確認してください)。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[クイック開始（EJBモード）: Java APIを使用したフラグメントに基づくPDFドキュメントの作成](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[クイック開始（SOAPモード）: Java APIを使用したフラグメントに基づくPDFドキュメントの作成](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

### WebサービスAPIを使用したフラグメントに基づくPDFドキュメントの作成 {#create-a-pdf-document-based-on-fragments-using-the-web-service-api}

Output Service APIとAssembler Service API（Webサービス）を使用して、フラグメントに基づいてPDFドキュメントを作成します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 Outputサービスに関連付けられているサービス参照には、次のWSDL定義を使用します。

   ```java
    http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1.
   ```

   Assemblerサービスに関連付けられたサービス参照には、次のWSDL定義を使用します。

   ```java
    http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   この `BLOB` データ型は両方のサービス参照に共通なので、使用する場合は `BLOB` データ型を完全に限定します。 対応するWebサービスクイック開始では、すべての `BLOB` インスタンスが完全修飾されます。

   >[!NOTE]
   >
   >サーバーホスト `localhost` AEM FormsのIPアドレスに置き換えます。

1. OutputおよびAssembler Clientオブジェクトを作成します。

   * デフォルトのコンストラクターを使用して `OutputServiceClient` オブジェクトを作成します。
   * コンストラクターを使用して `OutputServiceClient.Endpoint.Address` オブジェクトを作成し `System.ServiceModel.EndpointAddress` ます。 WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/OutputService?blob=mtom`)に渡すstring値を渡します。 属性を使用する必要はありません `lc_version` 。 この属性は、サービス参照を作成する際に使用されます。 ただし、MTOMを使用す `?blob=mtom` るように指定します。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `OutputServiceClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * AEM formsのユーザー名を `OutputServiceClient.ClientCredentials.UserName.UserName`フィールドに割り当てます。
      * 対応するパスワード値を `OutputServiceClient.ClientCredentials.UserName.Password`フィールドに割り当てます。
      * 定数値を `HttpClientCredentialType.Basic``BasicHttpBindingSecurity.Transport.ClientCredentialType`フィールドに割り当てます。
   * 定数値をフィー `BasicHttpSecurityMode.TransportCredentialOnly``BasicHttpBindingSecurity.Security.Mode`ルドに割り当てます。

   >[!NOTE]
   >
   >オブジェクトに対してこの手順を繰り返し `AssemblerServiceClient`ます。

1. Assemblerサービスを使用してフォームデザインを生成します。

   オブジェクトの `AssemblerServiceClient``invokeDDX` メソッドを呼び出し、次の値を渡します。

   * DDXドキュメントを表す `BLOB` オブジェクトです
   * 必要なファイルを含む `MyMapOf_xsd_string_To_xsd_anyType` オブジェクトです
   * 実行時オプションを指定する `AssemblerOptionSpec` オブジェクトです。

   この `invokeDDX` メソッドは、ジョブの結果と発生した例外を含む `AssemblerResult` オブジェクトを返します。 新しく作成されたXDPドキュメントを取得するには、次の操作を実行します。

   * オブジェクトのフ `AssemblerResult` ィールドにアクセスします。この `documents` フィールドは、結果のPDFドキュメントを含む `Map` オブジェクトです。
   * オブジェクトを繰り返し処理して、アセンブルされたフォームデザインを取得します。 `Map` 配列メンバーをにキャスト `value` し `BLOB`ます。 この `BLOB` インスタンスをOutputサービスに渡します。


1. Outputサービスを使用してPDFドキュメントを生成します。

   オブジェクトの `OutputServiceClient``generatePDFOutput2` メソッドを呼び出し、次の値を渡します。

   * 定義済みリスト `TransformationFormat` 値。 PDFドキュメントを生成するには、を指定し `TransformationFormat.PDF`ます。
   * 画像などの追加リソースが存在するコンテンツルートを指定するstring値です。
   * フォームデザインを表す `BLOB` オブジェクト(Assemblerサービスから返される `BLOB` インスタンスを使用)。
   * PDF実行時オプションを含む `PDFOutputOptionsSpec` オブジェクトです。
   * レンダリングの実行時オプションを含む `RenderOptionsSpec` オブジェクトです。
   * フォームデザインとマージするデータを含むXMLデータソースを含む `BLOB` オブジェクトです。
   * メソッドが入力する出力 `BLOB` オブジェクト `generatePDFOutput2` です。 この `generatePDFOutput2` メソッドは、ドキュメントを表す生成されたメタデータをこのオブジェクトに入力します。 （このパラメーター値は、Webサービスの呼び出しの場合にのみ必要です）。
   * 操作の結果を含む出力 `OutputResult` オブジェクトです。 （このパラメーター値は、Webサービスの呼び出しの場合にのみ必要です）。

   この `generatePDFOutput2` メソッドは、非インタラクティブPDFフォームを含む `BLOB` オブジェクトを返します。

1. PDFドキュメントをPDFファイルとして保存します。

   * Create a `System.IO.FileStream` object by invoking its constructor. インタラクティブPDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * メソッドから取得した `BLOB` オブジェクトの内容を格納するバイト配列を作成し `generatePDFOutput2` ます。 オブジェクトのデータメンバーの値を取得して、 `BLOB` バイト配列を入力し `MTOM` ます。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡して、バイト配列の内容をPDFファイルに書き込み `System.IO.BinaryWriter` ま `Write` す。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## ファイルへの印刷 {#printing-to-files}

Outputサービスを使用して、PostScript、Printer Control Language(PCL)、次のラベル形式などのストリームをファイルに印刷できます。

* Zebra - ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

Outputサービスを使用すると、XMLデータをフォームデザインとマージし、フォームをファイルに印刷できます。 次の図に、レーザーファイルとラベルファイルを作成するOutputサービスを示します。

>[!NOTE]
>
>プリント・ストリームのプリンタへの送信の詳細は、「プリント・ストリームのプリンタへの [送信](creating-document-output-streams.md#sending-print-streams-to-printers)」を参照してください。

>[!NOTE]
>
>For more information about the Output service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-5}

ファイルに出力するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Output Clientオブジェクトを作成します。
1. XMLデータソースを参照します。
1. ファイルに印刷するために必要な印刷実行時オプションを設定します。
1. 印刷ストリームをファイルに印刷します。
1. 操作の結果を取得します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めます。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(AEM FormsがJBossにデプロイされている場合に必要)
* jbossall-client.jar(AEM FormsがJBossにデプロイされている場合に必要)

AEM Formsが、JBoss以外のサポート対象のJ2EEアプリケーションサーバーにデプロイされている場合は、adobe-utilities.jarファイルとjbossall-client.jarファイルを、AEM FormsがデプロイされているJ2EEアプリケーションサーバーに固有のJARファイルに置き換える必要があります。 （[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照。）

**Output Clientオブジェクトの作成**

プログラムを使用してOutputサービス操作を実行する前に、Outputサービスクライアントオブジェクトを作成する必要があります。 Java APIを使用している場合は、 `OutputClient` オブジェクトを作成します。 Output WebサービスAPIを使用している場合は、 `OutputServiceService` オブジェクトを作成します。

**XMLデータソースの参照**

データを含むドキュメントを印刷するには、データを入力するすべてのフォームフィールドに対して、XML要素を含むXMLデータソースを参照する必要があります。 XML要素名は、フィールド名と一致する必要があります。 XML要素がフォームフィールドに対応していない場合、またはXML要素名がフィールド名と一致しない場合、XML要素は無視されます。 すべてのXML要素が指定されている場合、XML要素が表示される順序と一致させる必要はありません。

**ファイルへの印刷に必要な実行時オプションの設定**

ファイルに出力するには、Outputサービスが印刷するファイルの場所と名前を指定して、「ファイルURIランタイム」オプションを設定する必要があります。 例えば、MortgageForm.psという名前のPostScriptファイルをC:\Adobeに印刷するようにOutputサービスに指示するには、C:\Adobe\MortgageForm.ps ** を指定します。

>[!NOTE]
>
>オプションで定義できる実行時オプションがあります。 設定できるすべてのオプションについて詳しくは、 `PrintedOutputOptionsSpec` AEM FormsAPIリファレンスの [クラス参照を参照してください](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

**印刷ストリームをファイルに印刷する**

フォームデータを含む有効なXMLデータソースを参照し、印刷の実行時オプションを設定したら、Outputサービスを呼び出して、ファイルを印刷できます。

**操作の結果を取得します**

Outputサービスは、操作の実行後、XMLデータなど、操作が成功したかどうかを示す様々なデータ項目を返します。

**関連トピック**

[Java APIを使用してファイルに出力する](creating-document-output-streams.md#print-to-files-using-the-java-api)

[WebサービスAPIを使用してファイルに出力する](creating-document-output-streams.md#print-to-files-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[OutputサービスAPIのクイック開始](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Java APIを使用してファイルに出力する {#print-to-files-using-the-java-api}

Output API(Java)を使用してファイルに出力する：

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-output-client.jarなどのクライアントJARファイルを含めます。

1. Output Clientオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `OutputClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. XMLデータソースを参照します。

   * コンストラクターを使用し、XMLファイルの場所を指定する文字列値を渡すことで、ドキュメントの入力に使用されるXMLデータソースを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. ファイルに印刷するために必要な印刷実行時オプションを設定します。

   * コンストラクタを使用して `PrintedOutputOptionsSpec` オブジェクトを作成します。
   * PrintedOutputOptionsSpecオブジェクトのメソッドを呼び出し、ファイルの名前と場所を表すstring値を渡して、ファイルを指定します。 `setFileURI` 例えば、OutputサービスをC:\AdobeにあるMortgageForm.psというPostScriptファイルに印刷する場合は、C:\\Adobe\MortgageForm.psを指定します。
   * オブジェクトの `PrintedOutputOptionsSpec``setCopies` メソッドを呼び出し、部数を表す整数値を渡して、印刷する部数を指定します。

1. 印刷ストリームをファイルに印刷します。

   オブジェクトの `OutputClient``generatePrintedOutput` メソッドを呼び出し、次の値を渡して、ファイルに出力します。

   * 作成する印刷ストリームの形式を指定する `PrintFormat` 定義済みリスト値。 例えば、PostScript印刷ストリームを作成するには、を渡し `PrintFormat.PostScript`ます。
   * フォームデザイン名を指定する string 値。
   * 画像ファイルなど、関連するコラテラルファイルの場所を指定するstring値。
   * 使用するXDCファイルの場所を指定するstring値です(オブジェクトを使用して使用するXDCファイルを指定し `null` た場合は、渡すことができ `PrintedOutputOptionsSpec` ます)。
   * ファイルに印刷するために必要な実行時オプションを含む `PrintedOutputOptionsSpec` オブジェクトです。
   * フォームデータを含むXMLデータソースを含む `com.adobe.idp.Document` オブジェクトです。

   The `generatePrintedOutput` method returns an `OutputResult` object that contains the results of the operation.

   >[!NOTE]
   >
   >オブ `OutputResult` ジェクトの `getRecordLevelMetaDataList` メソッドが返し `null`ます。

1. 操作の結果を取得します。

   * オブジェクトのメソッドを呼び出して（そのオブジェクトがメソッドによって返された）、そのメソッドのステータスを表す `com.adobe.idp.Document` オブジェクトを作成します。このオブ `generatePrintedOutput``OutputResult``getStatusDoc``OutputResult``generatePrintedOutput` ジェクトは、メソッドによって返されたものです。
   * 操作の結果を含む `java.io.File` オブジェクトを作成します。 ファイル拡張子がXMLであることを確認します。
   * オブジェクトのメ `com.adobe.idp.Document` ソッドを呼び出して、 `copyToFile` オブジェクトの内容をファイルにコピーします(メソッドから返された `com.adobe.idp.Document``com.adobe.idp.Document``getStatusDoc` オブジェクトを必ず使用してください)。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[クイック開始（SOAPモード）: Java APIを使用したファイルへの印刷](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-printing-to-a-file-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

### WebサービスAPIを使用してファイルに出力する {#print-to-files-using-the-web-service-api}

Output API（Webサービス）を使用してファイルに出力します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >サーバーホスト `localhost` AEM FormsのIPアドレスに置き換えます。

1. Output Clientオブジェクトを作成します。

   * デフォルトのコンストラクターを使用して `OutputServiceClient` オブジェクトを作成します。
   * コンストラクターを使用して `OutputServiceClient.Endpoint.Address` オブジェクトを作成し `System.ServiceModel.EndpointAddress` ます。 WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/OutputService?blob=mtom`)に渡すstring値を渡します。 属性を使用する必要はありません `lc_version` 。 この属性は、サービス参照を作成する際に使用されます。 ただし、MTOMを使用す `?blob=mtom` るように指定します。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `OutputServiceClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールドにAEM formsのユーザー名を割り当て `OutputServiceClient.ClientCredentials.UserName.UserName`ます。
      * 対応するパスワード値をフィールドに割り当て `OutputServiceClient.ClientCredentials.UserName.Password`ます。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当て `BasicHttpBindingSecurity.Security.Mode`ます。

1. XMLデータソースを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、フォームデータの格納に使用されます。
   * コンストラクターを呼び出し、フォームデータを含むXMLファイルの場所を指定する文字列値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
   * オブジェクトの `System.IO.FileStream``Read` メソッドを呼び出し、読み取るバイト配列、開始位置およびストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * オブジェクトのプロパティにバイト配列の内容を割り当てて、 `BLOB``binaryData` オブジェクトを入力します。

1. ファイルに印刷するために必要な印刷実行時オプションを設定します。

   * コンストラクタを使用して `PrintedOutputOptionsSpec` オブジェクトを作成します。
   * ファイルの場所と名前を表すstring値を `PrintedOutputOptionsSpec` オブジェクトの `fileURI` データメンバーに割り当てて、ファイルを指定します。 例えば、C:\AdobeにあるPostScriptファイルMortgageForm.ps ** （ファイル名：PostScript）にOutputサービスを印刷する場合は、C:\\Adobe\MortgageForm.psを指定します。
   * 印刷する部数を指定するには、 `PrintedOutputOptionsSpec` オブジェクトの `copies` データメンバーの部数を表す整数値を割り当てます。

1. 印刷ストリームをファイルに印刷します。

   オブジェクトの `OutputServiceService``generatePrintedOutput` メソッドを呼び出し、次の値を渡して、ファイルに出力します。

   * 作成する印刷ストリームの形式を指定する `PrintFormat` 定義済みリスト値。 例えば、PostScript印刷ストリームを作成するには、を渡し `PrintFormat.PostScript`ます。
   * フォームデザイン名を指定する string 値。
   * 画像ファイルなど、関連するコラテラルファイルの場所を指定するstring値。
   * 使用するXDCファイルの場所を指定するstring値です(オブジェクトを使用して使用するXDCファイルを指定し `null` た場合は、渡すことができ `PrintedOutputOptionsSpec` ます)。
   * ファイルに印刷するために必要な印刷実行時オプションを含む `PrintedOutputOptionsSpec` オブジェクトです。
   * フォームデータを含むXMLデータソースを含む `BLOB` オブジェクトです。
   * メソッドによって入力される `BLOB` オブジェクト `generatePDFOutput` です。 この `generatePDFOutput` メソッドは、ドキュメントを表す生成されたメタデータをこのオブジェクトに入力します。 （このパラメーター値は、Webサービス呼び出しのみで必要です）。
   * メソッドによって入力される `BLOB` オブジェクト `generatePDFOutput` です。 この `generatePDFOutput` メソッドは、このオブジェクトに結果データを入力します。 （このパラメーター値は、Webサービス呼び出しのみで必要です）。
   * 操作の結果を含む `OutputResult` オブジェクトです。 （このパラメーター値は、Webサービス呼び出しのみで必要です）。

1. 操作の結果を取得します。

   * コンストラクターを呼び出し、結果データを含むXMLファイルの場所を表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。 ファイル拡張子がXMLであることを確認します。
   * オブジェクトの `BLOB` メソッド（8番目のパラメーター）によって結果データが入力された `OutputServiceService``generatePDFOutput` オブジェクトのデータ内容を格納するバイト配列を作成します。 オブジェクトのデータメンバーの値を取得して、 `BLOB` バイト配列を入力し `MTOM` ます。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡して、バイト配列の内容をXMLファイルに書き込み `System.IO.BinaryWriter` ま `Write` す。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## プリントストリームをプリンタに送信する {#sending-print-streams-to-printers}

Outputサービスを使用して、PostScript、Printer Control Language(PCL)、次のラベル形式などの印刷ストリームをネットワークプリンターに送信できます。

* Zebra - ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

Outputサービスを使用すると、XMLデータをフォームデザインとマージし、フォームを印刷ストリームとして出力できます。 例えば、PostScript印刷ストリームを作成して、ネットワークプリンターに送信できます。 次の図に、印刷ストリームをネットワークプリンターに送信するOutputサービスを示します。

>[!NOTE]
>
>このセクションでは、印刷ストリームをネットワークプリンターに送信する方法を示すために、SharedPrinterプロトコルを使用してPostScript印刷ストリームをネットワークプリンターに送信します。

>[!NOTE]
>
>For more information about the Output service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-6}

印刷ストリームをネットワークプリンターに送信するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Output Clientオブジェクトを作成します。
1. XMLデータソースを参照します。
1. 実行時の印刷オプションの設定
1. 印刷するドキュメントを取得します。
1. ドキュメントをネットワークプリンターに送信します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めます。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(AEM FormsがJBossにデプロイされている場合に必須)
* jbossall-client.jar(AEM FormsがJBossにデプロイされている場合に必須)

AEM Formsが、JBoss以外のサポート対象のJ2EEアプリケーションサーバーにデプロイされている場合は、adobe-utilities.jarファイルとjbossall-client.jarファイルを、AEM FormsがデプロイされているJ2EEアプリケーションサーバーに固有のJARファイルに置き換える必要があります。

**Output Clientオブジェクトの作成**

プログラムを使用してOutputサービス操作を実行する前に、Outputサービスクライアントオブジェクトを作成します。 Java APIを使用している場合は、 `OutputClient` オブジェクトを作成します。 Output WebサービスAPIを使用している場合は、 `OutputServiceClient` オブジェクトを作成します。

**XMLデータソースの参照**

データを含むドキュメントを印刷するには、データを入力するすべてのフォームフィールドに対して、XML要素を含むXMLデータソースを参照する必要があります。 XML要素名は、フィールド名と一致する必要があります。 XML要素がフォームフィールドに対応していない場合、またはXML要素名がフィールド名と一致しない場合、XML要素は無視されます。 すべてのXML要素が指定されている場合、XML要素が表示される順序と一致させる必要はありません。

**実行時の印刷オプションの設定**

印刷ストリームをプリンターに送信する際に、実行時のオプションを設定できます。次に例を示します。

* **コピー**: プリンターに送信する部数を指定します。 デフォルト値は 1 です。
* **Staple**: XCIオプションは、ステープル印刷が使用される場合に設定されます。 このオプションは、設定モデルでstaple要素によって指定でき、PSプリンターとPCLプリンターにのみ使用されます。
* **OutputJog**: XCIオプションは、出力ページにジョグを付ける（出力トレイで物理的に移動する）必要がある場合に設定されます。 このオプションは、PSプリンターとPCLプリンターのみに使用できます。
* **OutputBin**: プリントドライバーが適切な出力binを選択できるようにするために使用されるXCI値です。

>[!NOTE]
>
>設定可能なすべての実行時オプションについて詳しくは、クラス参照を参照してください `PrintedOutputOptionsSpec` 。

**印刷するドキュメントを取得する**

プリンターに送信する印刷ストリームを取得します。 例えば、PostScriptファイルを取得してプリンターに送信できます。

プリンターでPDFがサポートされている場合は、PDFファイルを送信するように選択できます。 ただし、プリンターにPDFドキュメントを送信する際の問題は、プリンターの製造元ごとにPDFインタープリターの実装が異なることです。 つまり、一部の印刷メーカーはAdobe PDFの解釈を使用していますが、プリンターによって異なります。 その他のプリンターには、独自のPDFインタープリターがあります。 その結果、印刷結果が異なる場合があります。

PDFドキュメントをプリンターに送信する際のもう1つの制限は、単に印刷されるだけです。 両面印刷、用紙トレイの選択、ホチキス止めは、プリンタの設定を通じてのみ使用できます。

印刷するドキュメントを取得するには、この `generatePrintedOutput` メソッドを使用します。 次の表に、この `generatePrintedOutput` メソッドを使用する場合に特定の印刷ストリームに対して設定されるコンテンツタイプを示します。

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
   <td><p>汎用PostScriptレベル3出力ストリームを作成します。</p></td>
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
   <td><p>汎用PostScriptレベル2出力ストリームを作成します。</p></td>
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
>この方法を使用して、印刷ストリームをプリンターに送信することもでき `generatePrintedOutput2` ます。 ただし、[プリントストリームをプリンタに送信する]セクションに関連付けられているクイック開始では、この `generatePrintedOutput` メソッドを使用します。

**印刷ストリームをネットワークプリンターに送信します**

印刷するドキュメントを取得した後、Outputサービスを呼び出すと、印刷ストリームがネットワークプリンターに送信されます。 Outputサービスでプリンターを正しく検索するには、プリントサーバーとプリンター名の両方を指定する必要があります。 また、印刷プロトコルも指定する必要があります。

>[!NOTE]
>
>PDFGがformsサーバーにインストールされていて、サーバーがWindows Server 2008で実行されている場合、SharedPrinterプロパティを使用することはできません。 この場合は、別のプリンタープロトコルを使用します。

>[!NOTE]
>
>ネットワークプリンターを使用していて、アクセスメカニズムがSharedPrinterの場合は、プリンターの完全なネットワークパスを指定する必要があります。Java APIを使用して、印刷ストリームをネットワークプリンターに送信します。

Output API(Java)を使用して、印刷ストリームをネットワークプリンターに送信します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-output-client.jarなどのクライアントJARファイルを含めます。

1. Output Clientオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `OutputClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. XMLデータソースの参照

   * コンストラクターを使用し、XMLファイルの場所を指定する文字列値を渡すことで、ドキュメントの入力に使用されるXMLデータソースを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 実行時の印刷オプションの設定

   印刷の実行時オプションを表す `PrintedOutputOptionsSpec` オブジェクトを作成します。 例えば、オブジェクトの `PrintedOutputOptionsSpec``setCopies` メソッドを呼び出して、印刷部数を指定できます。

   >[!NOTE]
   >
   >ZPL印刷ストリームを生成する場合、 `PrintedOutputOptionsSpec` オブジェクトの `setPagination` メソッドを使用してページネーションの値を設定することはできません。 同様に、ZPL印刷ストリームに対して次のオプションを設定することはできません。 OutputJog、PageOffset、Staple。 この `setPagination` メソッドはPostScriptの生成に対して無効です。 PCL生成に対してのみ有効です。

1. 印刷するドキュメントを取得する

   * オブジェクトの `OutputClient` メソッドを呼び出し、次の値を渡して、印刷するドキュメントを取得し `generatePrintedOutput` ます。

      * 印刷ストリームを指定する `PrintFormat` 定義済みリスト値。 例えば、PostScript印刷ストリームを作成するには、を渡し `PrintFormat.PostScript`ます。
      * フォームデザイン名を指定する string 値。
      * 画像ファイルなど、関連するコラテラルファイルの場所を指定するstring値。
      * 使用するXDCファイルの場所を指定するstring値です。
      * ファイルに印刷するために必要な実行時オプションを含む `PrintedOutputOptionsSpec` オブジェクトです。
      * フォームデザインとマージするフォームデータが含まれるXMLデータソースを表す `com.adobe.idp.Document` オブジェクトです。

      This method returns an `OutputResult` object that contains the results of the operation.

   * オブジェクトの `com.adobe.idp.Document` メソッドを呼び出して、プリンタに送信する `OutputResult` オブジェクトを作成し `getGeneratedDoc` ます。 このメソッドは、 `com.adobe.idp.Document` オブジェクトを返します。


1. 印刷ストリームをネットワークプリンターに送信します

   オブジェクトの `OutputClient``sendToPrinter` メソッドを呼び出し、次の値を渡して、印刷ストリームをネットワークプリンターに送信します。

   * プリンターに送信する印刷ストリームを表す `com.adobe.idp.Document` オブジェクトです。
   * 使用するプリンタープロトコルを指定する `PrinterProtocol` 定義済みリスト値。 例えば、SharedPrinterプロトコルを指定するには、を渡し `PrinterProtocol.SharedPrinter`ます。
   * プリントサーバーの名前を指定するstring値です。 例えば、プリントサーバーの名前がPrintSever1であると仮定して、を渡 `\\\PrintSever1`します。
   * プリンターの名前を指定するstring値です。 例えば、プリンター名がPrinter1の場合は、を渡し `\\\PrintSever1\Printer1`ます。

   >[!NOTE]
   >
   >この `sendToPrinter` メソッドは、バージョン8.2.1でAEM FormsAPIに追加されました。

### WebサービスAPIを使用したプリンターへの印刷ストリームの送信 {#send-a-print-stream-to-a-printer-using-the-web-service-api}

Output API（Webサービス）を使用して、印刷ストリームをネットワークプリンターに送信します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >サーバーホスト `localhost` AEM FormsのIPアドレスに置き換えます。

1. Output Clientオブジェクトを作成します。

   * デフォルトのコンストラクターを使用して `OutputServiceClient` オブジェクトを作成します。
   * コンストラクターを使用して `OutputServiceClient.Endpoint.Address` オブジェクトを作成し `System.ServiceModel.EndpointAddress` ます。 WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/OutputService?blob=mtom`)に渡すstring値を渡します。 属性を使用する必要はありません `lc_version` 。 この属性は、サービス参照を作成する際に使用されます。 ただし、MTOMを使用す `?blob=mtom` るように指定します。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `OutputServiceClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールドにAEM formsのユーザー名を割り当て `OutputServiceClient.ClientCredentials.UserName.UserName`ます。
      * 対応するパスワード値をフィールドに割り当て `OutputServiceClient.ClientCredentials.UserName.Password`ます。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当て `BasicHttpBindingSecurity.Security.Mode`ます。

1. XMLデータソースを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、フォームデータの格納に使用されます。
   * Create a `System.IO.FileStream` object by invoking its constructor. フォームデータを含むXMLファイルの場所を指定するstring値を渡します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 オブジェクトのプロパティを取得して、バイト配列の長さ `System.IO.FileStream` を決定し `Length` ます。
   * オブジェクトの `System.IO.FileStream``Read` メソッドを呼び出し、読み取るバイト配列、開始位置およびストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * オブジェクトにバイト配列の内容を割り当てて、 `BLOB` オブジェクト `MTOM` を入力します。

1. 実行時の印刷オプションを設定します。

   コンストラクタを使用して `PrintedOutputOptionsSpec` オブジェクトを作成します。例えば、印刷部数を指定するには、部数を表す整数値を `PrintedOutputOptionsSpec` オブジェクトの `copies` データメンバに割り当てます。

   >[!NOTE]
   >
   >ZPL印刷ストリームを生成する場合、 `PrintedOutputOptionsSpec` オブジェクトの `pagination` データメンバを使用してページネーション値を設定することはできません。 同様に、ZPL印刷ストリームに対して次のオプションを設定することはできません。 OutputJog、PageOffsetおよびStaple。 PostScript生成に対して `pagination` データメンバが無効です。 PCL生成に対してのみ有効です。

1. 印刷するドキュメントを取得します。

   * オブジェクトの `OutputServiceService` メソッドを呼び出し、次の値を渡して、印刷するドキュメントを取得し `generatePrintedOutput` ます。

      * 印刷ストリームを指定する `PrintFormat` 定義済みリスト値。 例えば、PostScript印刷ストリームを作成するには、を渡し `PrintFormat.PostScript`ます。
      * フォームデザイン名を指定する string 値。
      * 画像ファイルなど、関連するコラテラルファイルの場所を指定するstring値。
      * 使用するXDCファイルの場所を指定するstring値です。
      * 印刷ストリームをネットワークプリンターに送信するときに使用される印刷実行時オプションを含む `PrintedOutputOptionsSpec` オブジェクトです。
      * フォームデータを含むXMLデータソースを含む `BLOB` オブジェクトです。
      * メソッドによって入力される `BLOB` オブジェクト `generatePrintedOutput` です。 この `generatePrintedOutput` メソッドは、ドキュメントを表す生成されたメタデータをこのオブジェクトに入力します。 （このパラメーター値は、Webサービス呼び出しのみで必要です）。
      * メソッドによって入力される `BLOB` オブジェクト `generatePrintedOutput` です。 この `generatePrintedOutput` メソッドは、このオブジェクトに結果データを入力します。 （このパラメーター値は、Webサービス呼び出しのみで必要です）。
      * 操作の結果を含む `OutputResult` オブジェクトです。 （このパラメーター値は、Webサービス呼び出しのみで必要です）。
   * オブジェクトの `BLOB` メソッドの値を取得して、プリンタに送信する `OutputResult` オブジェクトを作成し `generatedDoc` ます。 このメソッドは、メソッドによって返されるPostScriptデータを含む `BLOB` オブジェクトを返し `generatePrintedOutput` ます。


1. 印刷ストリームをネットワークプリンターに送信します。

   オブジェクトの `OutputClient``sendToPrinter` メソッドを呼び出し、次の値を渡して、印刷ストリームをネットワークプリンターに送信します。

   * プリンターに送信する印刷ストリームを表す `BLOB` オブジェクトです。
   * 使用するプリンタープロトコルを指定する `PrinterProtocol` 定義済みリスト値。 例えば、SharedPrinterプロトコルを指定するには、を渡し `PrinterProtocol.SharedPrinter`ます。
   * 以前のパラメーター値を使用するかどうかを指定する `bool` 値。 値を渡し `true`ます。 （このパラメーター値は、Webサービス呼び出しのみで必要です）。
   * プリントサーバーの名前を指定するstring値です。 例えば、プリントサーバーの名前がPrintSever1であると仮定して、を渡し `\\\PrintSever1`ます。
   * プリンターの名前を指定するstring値です。 例えば、プリンター名がPrinter1である場合は、を渡し `\\\PrintSever1\Printer1`ます。

   >[!NOTE]
   >
   >この `sendToPrinter` メソッドは、バージョン8.2.1でAEM FormsAPIに追加されました。

## 複数の出力ファイルの作成 {#creating-multiple-output-files}

Outputサービスでは、XMLデータソース内のレコードごとに個別のドキュメントを作成することも、すべてのレコードを含む単一のファイルを作成することもできます（この機能はデフォルトです）。 例えば、10件のレコードがXMLデータソース内にあり、OutputサービスAPIを使用して各レコードに対して個別のPDFドキュメント（または他の種類の出力）を作成するようにOutputサービスに指示したとします。 その結果、Outputサービスは10個のPDFドキュメントを生成します。 (ドキュメントを作成する代わりに、1台のプリンターに複数のプリントストリームを送信できます)。

次の図は、複数のレコードを含むXMLデータファイルを処理するOutputサービスも示しています。 ただし、すべてのデータレコードを含む単一のPDFドキュメントを作成するようにOutputサービスに指示したとします。 この場合、Outputサービスは、すべてのレコードを含む1つのドキュメントを生成します。

次の図に、複数のレコードを含むXMLデータファイルを処理するOutputサービスを示します。 Outputサービスに対して、各データレコードに対して個別のPDFドキュメントを作成するように指示したとします。 この場合、Outputサービスは、各データレコードに対して個別のPDFドキュメントを生成します。

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

各データレコードを開始および終了するXML要素は、 `LoanRecord`です。 このXML要素は、複数のファイルを生成するアプリケーションロジックから参照されます。

>[!NOTE]
>
>For more information about the Output service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-7}

XMLデータソースに基づいて複数のPDFファイルを作成するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Output Clientオブジェクトを作成します。
1. XMLデータソースを参照します。
1. PDFランタイムオプションを設定します。
1. レンダリングの実行時オプションを設定します。
1. 複数のPDFファイルを生成します。
1. 操作の結果を取得します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めます。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(AEM FormsがJBossにデプロイされている場合に必要)
* jbossall-client.jar(AEM FormsがJBossにデプロイされている場合に必要)

AEM Formsが、JBoss以外のサポート対象のJ2EEアプリケーションサーバーにデプロイされている場合は、adobe-utilities.jarファイルとjbossall-client.jarファイルを、AEM FormsがデプロイされているJ2EEアプリケーションサーバーに固有のJARファイルに置き換える必要があります。

**Output Clientオブジェクトの作成**

プログラムを使用してOutputサービス操作を実行する前に、Outputサービスクライアントオブジェクトを作成する必要があります。 Java APIを使用している場合は、 `OutputClient` オブジェクトを作成します。 Output WebサービスAPIを使用している場合は、 `OutputServiceService` オブジェクトを作成します。

**XMLデータソースの参照**

複数のレコードを含むXMLデータソースを参照します。 XML要素を使用してデータレコードを区切る必要があります。 例えば、この節で前述したXMLデータソースの例では、データレコードを区切るXML要素に名前が付けられてい `LoanRecord`ます。

データを入力するフォームフィールドごとに、XML要素が存在する必要があります。 XML要素名は、フィールド名と一致する必要があります。 XML要素がフォームフィールドに対応していない場合、またはXML要素名がフィールド名と一致しない場合、XML要素は無視されます。 すべてのXML要素が指定されている場合、XML要素が表示される順序と一致させる必要はありません。

**PDFランタイムオプションの設定**

XMLデータソースに基づいて複数のファイルを正しく作成するには、Outputサービスに次の実行時オプションを設定する必要があります。

* **多数のファイル**: Outputサービスで作成するドキュメントを1つにするか、複数にするかを指定します。 trueまたはfalseを指定できます。 XMLデータソースのデータレコードごとに個別のドキュメントを作成する場合は、trueを指定します。
* **ファイルURI**: Outputサービスが生成するファイルの場所を指定します。 例えば、C:\\Adobe\forms\Loan.pdfと指定したとします。 この場合、OutputサービスはLoan.pdfという名前のファイルを作成し、そのファイルをC:\\Adobe\forms folderフォルダーに配置します。 複数のファイルがある場合、ファイル名はLoan0001.pdf、Loan0002.pdf、Loan0003.pdfなどになります。 ファイルの場所を指定した場合、ファイルはクライアントコンピューターではなくサーバー上に配置されます。
* **レコード名**: データレコードを区切るデータソース内のXML要素名を指定します。 例えば、前の節で示したXMLデータソースの例では、データレコードを区切るXML要素が呼び出され `LoanRecord`ます。 (「レコード名」実行時オプションを設定する代わりに、データレコードを含む要素レベルを示す数値をレコードレベルに割り当てることで、レコードレベルを設定できます。 ただし、「レコード名」または「レコードレベル」のみ設定できます。 両方の値を設定することはできません)。

**レンダリングの実行時オプションの設定**

レンダリングの実行時オプションは、複数のファイルの作成時に設定できます。 これらのオプションは必須ではありませんが（必須の出力実行時オプションとは異なり）、Outputサービスのパフォーマンスの向上などのタスクを実行できます。 例えば、Outputサービスでパフォーマンスを向上させるために使用されるフォームデザインをキャッシュできます。

Outputサービスは、バッチレコードを処理する場合、複数のレコードを含むデータをインクリメンタルに読み取ります。 つまり、Outputサービスは、データをメモリに読み取り、レコードのバッチ処理としてデータを解放します。 2つの実行時オプションのいずれかが設定されている場合、Outputサービスはデータをインクリメンタルに読み込みます。 「Record Name」実行時オプションを設定した場合、Outputサービスはデータをインクリメンタルに読み取ります。 同様に、「Record Level」実行時オプションを2以上に設定した場合、Outputサービスはデータをインクリメンタルに読み取ります。

Outputサービスでインクリメンタル読み込みを実行するかどうかを制御するには、また `PDFOutputOptionsSpec` は `PrintedOutputOptionSpec` オブジェクトの `setLazyLoading` メソッドを使用します。 このメソッドに値を渡すと、インクリメンタル読み込み `false` をオフにできます。

**複数のPDFファイルの生成**

複数のデータレコードを含み、実行時オプションを設定する有効なXMLデータソースを参照した後、Outputサービスを呼び出すと、複数のファイルが生成されます。 複数のレコードを生成する場合、 `OutputResult` オブジェクトの `getGeneratedDoc` メソッドが返され `null`ます。

**操作の結果を取得します**

Outputサービスは、操作の実行後、操作が成功したかどうかを示すXMLデータを返します。 次のXMLは、Outputサービスから返されます。 この場合、Outputサービスは42ドキュメントを生成しました。

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

[OutputサービスAPIのクイック開始](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Java APIを使用した複数のPDFファイルの作成 {#create-multiple-pdf-files-using-the-java-api}

Output API(Java)を使用して複数のPDFファイルを作成します。

1. プロジェクトファイルを含める&quot;

   Javaプロジェクトのクラスパスに、adobe-output-client.jarなどのクライアントJARファイルを含めます。 .

1. Output Clientオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `OutputClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. XMLデータソースの参照

   * コンストラクターを使用し、XMLファイルの場所を指定する文字列値を渡すことで、複数のレコードを含むXMLデータソースを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PDFランタイムオプションの設定

   * コンストラクタを使用して `PDFOutputOptionsSpec` オブジェクトを作成します。
   * オブジェクトの `PDFOutputOptionsSpec``setGenerateManyFiles` メソッドを呼び出して、「多数のファイル」オプションを設定します。 例えば、値を渡して、XMLデータソース `true` の各レコードに対して個別のPDFファイルを作成するようOutputサービスに指示します。 (を渡すと、Outputサービス `false`によって、すべてのレコードを含む単一のPDFドキュメントが生成されます)。
   * オブジェクトの `PDFOutputOptionsSpec``setFileUri` メソッドを呼び出し、Outputサービスが生成するファイルの場所を指定する文字列値を渡して、「File URI」オプションを設定します。 「ファイルのURI」オプションは、クライアントコンピューターではなく、J2EEアプリケーションAEM Formsをホストするサーバーに対する相対パスです。
   * オブジェクトの `OutputOptionsSpec``setRecordName` メソッドを呼び出し、データレコードを区切るデータソース内のXML要素名を指定する文字列値を渡して、「レコード名」オプションを設定します。 (例えば、この節で前述したXMLデータソースについて考えてみましょう。 データレコードを区切るXML要素の名前は、LoanRecordです)。

1. レンダリングの実行時オプションの設定

   * コンストラクタを使用して `RenderOptionsSpec` オブジェクトを作成します。
   * オブジェクトを呼び出し、の `RenderOptionsSpec` 値を渡すことで、フォームデザインをキャッシュして、Outputサービスのパフォーマンス `setCacheEnabled` を向上させ `Boolean``true`ます。

1. 複数のPDFファイルの生成

   オブジェクトの `OutputClient``generatePDFOutput` メソッドを呼び出し、次の値を渡して、複数のPDFファイルを生成します。

   * 列挙 `TransformationFormat` 値。 PDFドキュメントを生成するには、を指定し `TransformationFormat.PDF`ます。
   * フォームデザイン名を指定する string 値。
   * フォームデザインが配置されているコンテンツルートを指定するstring値。
   * PDF実行時オプションを含む `PDFOutputOptionsSpec` オブジェクトです。
   * レンダリングの実行時オプションを含む `RenderOptionsSpec` オブジェクトです。
   * フォームデザインとマージするデータを含むXMLデータソースを含む `com.adobe.idp.Document` オブジェクトです。

   The `generatePDFOutput` method returns an `OutputResult` object that contains the results of the operation.

1. 操作の結果を取得します

   * メソッドの結果を含むXMLファイルを表す `java.io.File` オブジェクトを作成し `generatePDFOutput` ます。 ファイル名の拡張子が.xmlであることを確認します。
   * オブジェクトのメ `com.adobe.idp.Document` ソッドを呼び出して、 `copyToFile` オブジェクトの内容をファイルにコピーします(メソッドから返された `com.adobe.idp.Document``com.adobe.idp.Document``applyUsageRights` オブジェクトを必ず使用してください)。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[クイック開始（EJBモード）: Java APIを使用した複数のPDFファイルの作成](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-multiple-pdf-files-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用して複数のPDFファイルを作成する {#create-multiple-pdf-files-using-the-web-service-api}

Output API（Webサービス）を使用して複数のPDFファイルを作成します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >サーバーホスト `localhost` AEM FormsのIPアドレスに置き換えます。

1. Output Clientオブジェクトを作成します。

   * デフォルトのコンストラクターを使用して `OutputServiceClient` オブジェクトを作成します。
   * コンストラクターを使用して `OutputServiceClient.Endpoint.Address` オブジェクトを作成し `System.ServiceModel.EndpointAddress` ます。 WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/OutputService?blob=mtom`)に渡すstring値を渡します。 属性を使用する必要はありません `lc_version` 。 この属性は、サービス参照を作成する際に使用されます。 ただし、MTOMを使用す `?blob=mtom` るように指定します。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `OutputServiceClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールドにAEM formsのユーザー名を割り当て `OutputServiceClient.ClientCredentials.UserName.UserName`ます。
      * 対応するパスワード値をフィールドに割り当て `OutputServiceClient.ClientCredentials.UserName.Password`ます。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当て `BasicHttpBindingSecurity.Security.Mode`ます。

1. XMLデータソースを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、複数のレコードを含むフォームデータを格納するために使用します。
   * Create a `System.IO.FileStream` object by invoking its constructor. 複数のレコードを含むXMLファイルのファイルの場所を表すstring値を渡します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
   * オブジェクトの `System.IO.FileStream``Read` メソッドを呼び出し、読み取るバイト配列、開始位置およびストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * オブジェクトにバイト配列の内容を割り当てて、 `BLOB` オブジェクト `MTOM` を入力します。

1. PDFランタイムオプションを設定します。

   * コンストラクタを使用して `PDFOutputOptionsSpec` オブジェクトを作成します。
   * 「多数のファイル」オプションを設定するには、 `OutputOptionsSpec` オブジェクトの `generateManyFiles` データメンバにブール値を割り当てます。 例えば、このデータメンバー `true` に値を割り当てて、Outputサービスに対して、XMLデータソースの各レコードに対して個別のPDFファイルを作成するように指示します。 (このデータメンバ `false` ーに割り当てる場合、Outputサービスは、すべてのレコードを含む単一のPDFを生成します)。
   * Outputサービスが生成するファイルの場所を指定するstring値を `OutputOptionsSpec` オブジェクトの `fileURI` データメンバーに割り当てて、file URIオプションを設定します。 「ファイルのURI」オプションは、クライアントコンピューターではなく、J2EEアプリケーションAEM Formsをホストするサーバーに対する相対パスです。
   * レコード名オプションを設定するには、データレコードを `OutputOptionsSpec``recordName` オブジェクトのデータメンバに分けるデータソース内のXML要素名を指定する文字列値を割り当てます。
   * 「コピー数」オプションを設定するには、Outputサービスが生成するコピー数を指定する整数値を `OutputOptionsSpec` オブジェクトの `copies` データメンバーに割り当てます。

1. レンダリングの実行時オプションを設定します。

   * コンストラクタを使用して `RenderOptionsSpec` オブジェクトを作成します。
   * フォームデザインをキャッシュし、Outputサービスのパフォーマンスを向上させるために、 `true` オブジェクトの `RenderOptionsSpec``cacheEnabled` データメンバーに値を割り当てます。

1. 複数のPDFファイルを生成します。

   オブジェクトの `OutputServiceService``generatePDFOutput`メソッドを呼び出し、次の値を渡して、複数のPDFファイルを作成します。

   * TransformationFormat列挙値。 PDFドキュメントを生成するには、を指定し `TransformationFormat.PDF`ます。
   * フォームデザイン名を指定する string 値。
   * フォームデザインが配置されているコンテンツルートを指定するstring値。
   * PDF実行時オプションを含む `PDFOutputOptionsSpec` オブジェクトです。
   * レンダリングの実行時オプションを含む `RenderOptionsSpec` オブジェクトです。
   * フォームデザインとマージするデータを含むXMLデータソースを含む `BLOB` オブジェクトです。
   * メソッドによって入力される `BLOB` オブジェクト `generatePDFOutput` です。 この `generatePDFOutput` メソッドは、ドキュメントを表す生成されたメタデータをこのオブジェクトに入力します。
   * メソッドによって入力される `BLOB` オブジェクト `generatePDFOutput` です。 この `generatePDFOutput` メソッドは、このオブジェクトに結果データを入力します。
   * 操作の結果を含む `OutputResult` オブジェクトです。

1. 操作の結果を取得します

   * コンストラクターを呼び出し、結果データを含むXMLファイルの場所を表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。 ファイル名の拡張子が.xmlであることを確認します。
   * オブジェクトの `BLOB` メソッド（8番目のパラメーター）によって結果データが入力された `OutputServiceService``generatePDFOutput` オブジェクトのデータ内容を格納するバイト配列を作成します。 オブジェクトのデータメンバーの値を取得して、 `BLOB` バイト配列を入力し `binaryData` ます。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡して、バイト配列の内容をXMLファイルに書き込み `System.IO.BinaryWriter` ま `Write` す。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 検索ルールの作成 {#creating-search-rules}

入力データを調べ、データコンテンツに基づいて様々なフォームデザインを使用して出力を生成するOutputサービスの結果となる検索ルールを作成できます。 例えば、テキスト *mortgage* が入力データ内にある場合、OutputサービスはMortgage.xdpという名前のフォームデザインを使用できます。 同様に、テキスト *automobile* が入力データ内にある場合、OutputサービスはAutomobileLoan.xdpとして保存されたフォームデザインを使用できます。 Outputサービスでは様々な出力タイプを生成できますが、この節では、OutputサービスでPDFファイルが生成されることを前提としています。 次の図に、XMLデータファイルを処理し、多数のフォームデザインの1つを使用してPDFファイルを生成するOutputサービスを示します。

また、Outputサービスではドキュメントパッケージを生成できます。このパッケージでは、データセットに複数のレコードが含まれ、各レコードがフォームデザインに一致し、1つのドキュメントが複数のフォームデザインで構成されます。

![cs_outputbatchmanyformdesigns2](assets/cs_outputbatchmanyformdesigns2.png)

>[!NOTE]
>
>For more information about the Output service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-8}

ドキュメントの生成時に検索ルールを使用するようにOutputサービスに指示するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Output Clientオブジェクトを作成します。
1. XMLデータソースを参照します。
1. 検索ルールを定義します。
1. PDFランタイムオプションを設定します。
1. レンダリングの実行時オプションを設定します。
1. PDFドキュメントを生成します。
1. 操作の結果を取得します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めます。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(AEM FormsがJBossにデプロイされている場合に必須)
* jbossall-client.jar(AEM FormsがJBossにデプロイされている場合に必須)

AEM FormsがJBoss以外のサポート対象のJ2EEアプリケーションサーバー上にデプロイされている場合は、adobe-utilities.jarおよびjbossall-client.jarを、AEM FormsがデプロイされているJ2EEアプリケーションサーバーに固有のJARファイルに置き換える必要があります。

**Output Clientオブジェクトの作成**

プログラムを使用してOutputサービス操作を実行する前に、Outputサービスクライアントオブジェクトを作成する必要があります。

**XMLデータソースの参照**

データを入力するフォームフィールドごとに、XML要素が存在する必要があります。 XML要素名は、フィールド名と一致する必要があります。 XML要素がフォームフィールドに対応していない場合、またはXML要素名がフィールド名と一致しない場合、XML要素は無視されます。 すべてのXML要素が指定されている限り、XML要素が表示される順序と一致させる必要はありません。

**検索ルールの定義**

検索ルールを定義するには、Outputサービスが入力データで検索する1つ以上のテキストパターンを定義します。 定義するテキストパターンごとに、テキストパターンがある場合に使用する、対応するフォームデザインを指定します。 テキストパターンが見つかった場合、Outputサービスは対応するフォームデザインを使用して出力を生成します。 テキストパターンの例として、 *住宅ローンがあります*。

>[!NOTE]
>
>テキストパターンが見つからない場合は、デフォルトのフォームが使用されます。 使用するすべてのフォームデザインがコンテンツルート内にあることを確認します。

**PDFランタイムオプションの設定**

Outputサービスが複数のフォームデザインに基づいてPDFドキュメントを正常に作成できるように、次のPDFランタイムオプションを設定します。

* **ファイルURI**: Outputサービスが生成するPDFファイルの名前と場所を指定します。
* **ルール**: 定義したルールを指定します。
* **LookAHead**: 定義済みのテキストパターンをスキャンするために入力データファイルの先頭から使用するバイト数を指定します。 デフォルトは500バイトです。

**レンダリングの実行時オプションの設定**

レンダリングの実行時オプションは、PDFファイルの作成時に設定できます。 これらのオプションは必須ではありませんが（PDFランタイムオプションとは異なり）、Outputサービスのパフォーマンスの向上などのタスクを実行できます。 例えば、Outputサービスでパフォーマンスを向上させるために使用されるフォームデザインをキャッシュできます。

**PDFドキュメントの生成**

有効なXMLデータソースを参照し、実行時オプションを設定したら、Outputサービスを呼び出してPDFドキュメントを生成できます。 Outputサービスは、入力データ内で指定したテキストパターンを見つけた場合、対応するフォームデザインを使用します。 テキストパターンを使用しない場合、Outputサービスではデフォルトのフォームデザインが使用されます。

**操作の結果を取得します**

Outputサービスは、操作の実行後、操作が成功したかどうかを示すXMLデータを返します。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[OutputサービスAPIのクイック開始](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Java APIを使用した検索ルールの作成 {#create-search-rules-using-the-java-api}

Output API(Java)を使用して検索ルールを作成します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-output-client.jarなどのクライアントJARファイルを含めます。

1. Output Clientオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `OutputClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. XMLデータソースを参照します。

   * コンストラクターを使用し、XMLファイルの場所を指定する文字列値を渡して、PDFドキュメントの入力に使用されるXMLデータソースを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 検索ルールを定義します。

   * コンストラクタを使用して `Rule` オブジェクトを作成します。
   * オブジェクトの `Rule``setPattern` メソッドを呼び出し、テキストパターンを指定する文字列値を渡して、テキストパターンを定義します。
   * オブジェクトのメソッドを呼び出して、対応する `Rule` フォームデザインを定義し `setForm` ます。 フォームデザインの名前を指定するstring値を渡します。

   >[!NOTE]
   >
   >定義するテキストパターンごとに、前の3つのサブ手順を繰り返します。

   * Create a `java.util.List` object by using an `java.util.ArrayList` constructor.
   * 作成した `Rule` オブジェクトごとに、 `java.util.List` オブジェクトの `add` メソッドを呼び出し、 `Rule` オブジェクトを渡します。


1. PDFランタイムオプションを設定します。

   * コンストラクタを使用して `PDFOutputOptionsSpec` オブジェクトを作成します。
   * Outputサービスが生成するPDFファイルの名前と場所を指定します。この場合、 `PDFOutputOptionsSpec` オブジェクトの `setFileURI` メソッドを呼び出します。 PDFファイルの場所を指定するstring値を渡します。 「ファイルのURI」オプションは、クライアントコンピューターではなく、J2EEアプリケーションAEM Formsをホストするサーバーに対する相対パスです。
   * オブジェクトのメソッドを呼び出して、定義した `PDFOutputOptionsSpec` ルールを設定し `setRules` ます。 オブジェクトを含む `java.util.List` オブジェクトを渡し `Rule` ます。
   * オブジェクトのメソッドを呼び出して、定義済みのテキストパターンをスキャンするバイト数を設定し `PDFOutputOptionsSpec` ま `setLookAhead` す。 バイト数を表す整数値を渡します。

1. レンダリングの実行時オプションを設定します。

   * コンストラクタを使用して `RenderOptionsSpec` オブジェクトを作成します。
   * オブジェクトを呼び出して渡すことでOutputサービスのパフォーマンスを向上させるために、フォームデザインをキャッシュ `RenderOptionsSpec` し `setCacheEnabled``true`ます。

1. PDFドキュメントを生成します。

   オブジェクトのメソッドを呼び出し、次の値を渡すことで、複数のフォームデザインに基づくPDFドキュメント `OutputClient` を生成し `generatePDFOutput` ます。

   * 定義済みリスト `TransformationFormat` 値。 PDFドキュメントを生成するには、を指定し `TransformationFormat.PDF`ます。
   * つまり、テキストパターンが見つからない場合に使用されるフォームデザインです。
   * フォームデザインが配置されるコンテンツルートを指定するstring値。
   * PDF実行時オプションを含む `PDFOutputOptionsSpec` オブジェクトです。
   * レンダリングの実行時オプションを含む `RenderOptionsSpec` オブジェクトです。
   * 定義済みのテキストパターンについてOutputサービスが検索するフォームデータを含む `com.adobe.idp.Document` オブジェクトです。

   The `generatePDFOutput` method returns an `OutputResult` object that contains the results of the operation.

1. 操作の結果を取得します。

   * オブジェクトのメソッドを呼び出して、その `com.adobe.idp.Document` メソッドのステータスを表す `generatePDFOutput` オブジェクトを作成し `OutputResult``getStatusDoc` ます。
   * 操作の結果を含む `java.io.File` オブジェクトを作成します。 ファイル拡張子が.xmlであることを確認します。
   * オブジェクトのメ `com.adobe.idp.Document` ソッドを呼び出して、 `copyToFile` オブジェクトの内容をファイルにコピーします(メソッドから返された `com.adobe.idp.Document``com.adobe.idp.Document``getStatusDoc` オブジェクトを必ず使用してください)。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[クイック開始（EJBモード）: Java APIを使用した検索ルールの作成](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[クイック開始（SOAPモード）: Java APIを使用した検索ルールの作成](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用した検索ルールの作成 {#create-search-rules-using-the-web-service-api}

Output API（Webサービス）を使用して検索ルールを作成します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >サーバーホスト `localhost` AEM FormsのIPアドレスに置き換えます。

1. Output Clientオブジェクトを作成します。

   * デフォルトのコンストラクターを使用して `OutputServiceClient` オブジェクトを作成します。
   * コンストラクターを使用して `OutputServiceClient.Endpoint.Address` オブジェクトを作成し `System.ServiceModel.EndpointAddress` ます。 WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/OutputService?blob=mtom`)に渡すstring値を渡します。 属性を使用する必要はありません `lc_version` 。 この属性は、サービス参照を作成する際に使用されます。 ただし、MTOMを使用す `?blob=mtom` るように指定します。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `OutputServiceClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールドにAEM formsのユーザー名を割り当て `OutputServiceClient.ClientCredentials.UserName.UserName`ます。
      * 対応するパスワード値をフィールドに割り当て `OutputServiceClient.ClientCredentials.UserName.Password`ます。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当て `BasicHttpBindingSecurity.Security.Mode`ます。

1. XMLデータソースを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、PDFドキュメントとマージされるデータの保存に使用されます。
   * コンストラクターを呼び出し、暗号化するPDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
   * オブジェクトの `System.IO.FileStream``Read` メソッドを呼び出し、読み取るバイト配列、開始位置およびストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * オブジェクトにバイト配列の内容を割り当てて、 `BLOB` オブジェクト `MTOM` を入力します。

1. 検索ルールを定義します。

   * コンストラクタを使用して `Rule` オブジェクトを作成します。
   * テキストパターンを定義するには、テキストパターンを指定する文字列値を `Rule` オブジェクトの `pattern` データメンバーに割り当てます。
   * フォームデザインを指定する文字列値を `Rule` オブジェクトの `form` データメンバーに割り当てて、対応するフォームデザインを定義します。

   >[!NOTE]
   >
   >定義するテキストパターンごとに、前の3つのサブ手順を繰り返します。

   * ルールを保存する `MyArrayOf_xsd_anyType` オブジェクトを作成します。
   * 各 `Rule` オブジェクトを配列の要素に割り当て `MyArrayOf_xsd_anyType` ます。 各オブジェクトに対して `MyArrayOf_xsd_anyType` オブジェクトの `Add` メソッドを呼び出し `Rule` ます。


1. PDFランタイムオプションの設定

   * コンストラクタを使用して `PDFOutputOptionsSpec` オブジェクトを作成します。
   * Outputサービスが生成するPDFファイルの場所を指定するstring値を `PDFOutputOptionsSpec` オブジェクトの `fileURI` データメンバーに割り当てて、file URIオプションを設定します。 「ファイルのURI」オプションは、クライアントコンピューターではなく、J2EEアプリケーションAEM Formsをホストするサーバーに対する相対パスです。
   * 「コピー数」オプションを設定するには、Outputサービスが生成するコピー数を指定する整数値を `PDFOutputOptionsSpec` オブジェクトの `copies` データメンバーに割り当てます。
   * ルールを保存する `MyArrayOf_xsd_anyType` オブジェクトをオブジェクトの `PDFOutputOptionsSpec``rules` データメンバに割り当てて、定義したルールを設定します。
   * 定義済みのテキストパターンをスキャンするバイト数を設定するには、スキャンするバイト数を表す整数値を `PDFOutputOptionsSpec` オブジェクトの `lookAhead` dataメソッドに割り当てます。

1. レンダリングの実行時オプションの設定

   * コンストラクタを使用して `RenderOptionsSpec` オブジェクトを作成します。
   * Outputサービスのパフォーマンスを向上させるためにフォームデザインをキャッシュします。この値は、 `true` オブジェクトの `RenderOptionsSpec``cacheEnabled` データメンバーに割り当てます。

   >[!NOTE]
   >
   >入力ドキュメントがAcrobatフォームの場合、 `RenderOptionsSpec` オブジェクトの `pdfVersion` メンバを使用してPDFドキュメントのバージョンを設定することはできません。 出力PDFドキュメントは、AcrobatフォームのPDFバージョンを保持します。 同様に、入力ドキュメントがAcrobatフォームの場合、 `RenderOptionsSpec` オブジェクトの `taggedPDF` メソッドを使用してタグ付きPDFオプションを設定することはできません。

   >[!NOTE]
   >
   >入力PDFドキュメントが認証済みまたはデジタル署名されている場合、 `RenderOptionsSpec` オブジェクトの `linearizedPDF` メンバを使用して線形化PDFオプションを設定することはできません。 詳しくは、「PDFドキュメントへの [デジタル署名](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)」を参照してください。

1. PDFドキュメントの生成

   Create a PDF document by invoking the `OutputServiceService` object’s `generatePDFOutput`method and passing the following values:

   * 定義済みリスト `TransformationFormat` 値。 PDFドキュメントを生成するには、を指定し `TransformationFormat.PDF`ます。
   * フォームデザイン名を指定する string 値。
   * フォームデザインが配置されているコンテンツルートを指定するstring値。
   * PDF実行時オプションを含む `PDFOutputOptionsSpec` オブジェクトです。
   * レンダリングの実行時オプションを含む `RenderOptionsSpec` オブジェクトです。
   * フォームデザインとマージするデータを含むXMLデータソースを含む `BLOB` オブジェクトです。
   * メソッドによって入力される `BLOB` オブジェクト `generatePDFOutput` です。 この `generatePDFOutput` メソッドは、ドキュメントを表す生成されたメタデータをこのオブジェクトに入力します。 （このパラメーター値は、Webサービスの呼び出しの場合にのみ必要です）。
   * メソッドによって入力される `BLOB` オブジェクト `generatePDFOutput` です。 この `generatePDFOutput` メソッドは、このオブジェクトに結果データを入力します。 （このパラメーター値は、Webサービスの呼び出しの場合にのみ必要です）。
   * 操作の結果を含む `OutputResult` オブジェクトです。 （このパラメーター値は、Webサービスの呼び出しの場合にのみ必要です）。

   >[!NOTE]
   >
   >この `generatePDFOutput` メソッドを呼び出してPDFドキュメントを生成する場合、署名、認証、または使用権限を含むXFA PDFフォームには、データをマージできないことに注意してください。 使用権限について詳しくは、「PDFドキュメントへの使用権限の [適用](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)」を参照してください。

1. 操作の結果を取得します

   * コンストラクターを呼び出し、結果データを含むXMLファイルの場所を表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。 ファイル拡張子がXMLであることを確認します。
   * オブジェクトの `BLOB` メソッド（8番目のパラメーター）によって結果データが入力された `OutputServiceService``generatePDFOutput` オブジェクトのデータ内容を格納するバイト配列を作成します。 オブジェクトのデータメンバーの値を取得して、 `BLOB` バイト配列を入力し `MTOM` ます。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡して、バイト配列の内容をXMLファイルに書き込み `System.IO.BinaryWriter` ま `Write` す。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## PDFドキュメントの統合 {#flattening-pdf-documents}

Outputサービスを使用して、インタラクティブPDFドキュメントを非インタラクティブPDFに変換できます。 インタラクティブPDFドキュメントを使用すると、ユーザーはPDFドキュメントフィールドにデータを入力または変更できます。 The process of transforming an interactive PDF document to a non-interactive PDF document is called *flattening*. PDFドキュメントを統合すると、ドキュメントフィールド内のデータを変更できなくなります。 PDF ドキュメントを統合する理由の 1 つは、データを変更できないようにすることです。

次の種類のPDFドキュメントを統合できます。

* インタラクティブXFA PDFドキュメント
* Acrobat Forms

非インタラクティブPDFドキュメントであるPDFをフラット化しようとすると、例外が発生します。

>[!NOTE]
>
>For more information about the Output service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-9}

インタラクティブPDFドキュメントを非インタラクティブPDFドキュメントに統合するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Output Clientオブジェクトを作成します。
1. インタラクティブPDFドキュメントを取得します。
1. PDFドキュメントを変換します。
1. 非インタラクティブPDFドキュメントをPDFファイルとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar(AEM FormsがJBossにデプロイされている場合に必要)
* jbossall-client.jar(AEM FormsがJBossにデプロイされている場合に必要)

AEM Formsが、JBoss以外のサポート対象のJ2EEアプリケーションサーバーにデプロイされている場合は、adobe-utilities.jarファイルとjbossall-client.jarファイルを、AEM FormsがデプロイされているJ2EEアプリケーションサーバーに固有のJARファイルに置き換える必要があります。 For information about the location of all AEM Forms JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Output Clientオブジェクトの作成**

プログラムを使用してOutputサービス操作を実行する前に、Outputサービスクライアントオブジェクトを作成する必要があります。 Java APIを使用している場合は、 `OutputClient` オブジェクトを作成します。 Output WebサービスAPIを使用している場合は、 `OutputServiceService` オブジェクトを作成します。

**インタラクティブPDFドキュメントの取得**

非インタラクティブPDFドキュメントに変換するインタラクティブPDFドキュメントを取得します。 非インタラクティブPDFドキュメントを変換しようとすると、例外が発生します。

**PDFドキュメントの変換**

インタラクティブPDFドキュメントを取得したら、非インタラクティブPDFドキュメントに変換できます。 Outputサービスは、非インタラクティブPDFドキュメントを返します。

**非インタラクティブPDFドキュメントをPDFファイルとして保存**

非インタラクティブPDFドキュメントは、PDFファイルとして保存できます。

**関連トピック**

[Java APIを使用したPDFドキュメントの統合](creating-document-output-streams.md#flatten-a-pdf-document-using-the-java-api)

[WebサービスAPIを使用したPDFドキュメントの統合](creating-document-output-streams.md#flatten-a-pdf-document-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[OutputサービスAPIのクイック開始](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Java APIを使用したPDFドキュメントの統合 {#flatten-a-pdf-document-using-the-java-api}

Output API(Java)を使用して、インタラクティブPDFドキュメントを非インタラクティブPDFドキュメントに統合します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-output-client.jarなどのクライアントJARファイルを含めます。

1. Output Clientオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `OutputClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. インタラクティブPDFドキュメントを取得します。

   * コンストラクターを使用し、インタラクティブPDFファイルの場所を指定するstring値を渡して、変換するインタラクティブPDFドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PDFドキュメントを変換します。

   オブジェクトのドキュメントを呼び出し、次の値を渡して、インタラクティブPDFドキュメントを非インタラクティブPDFメソッドに変換し `OutputServiceService``transformPDF` ます。

   * インタラクティブPDFドキュメントを含む `com.adobe.idp.Document` オブジェクトです。
   * 列挙 `TransformationFormat` 値。 非インタラクティブPDFドキュメントを生成するには、を指定し `TransformationFormat.PDF`ます。
   * A `PDFARevisionNumber` enum value that specifies the revision number. このパラメーターはPDF/Aドキュメントを対象としているので、指定でき `null`ます。
   * 修正番号と修正年をコロンで区切って表すstring値です。 このパラメーターはPDF/Aドキュメントを対象としているので、指定でき `null`ます。
   * PDF/A準拠レベルを表す `PDFAConformance` enum値です。 このパラメーターはPDF/Aドキュメントを対象としているので、指定でき `null`ます。

   非インタラクティブPDFドキュメントを含む `transformPDF``com.adobe.idp.Document` オブジェクトを返します。

1. 非インタラクティブPDFドキュメントをPDFファイルとして保存します。

   * Create a `java.io.File` object and ensure that the file name extension is .pdf.
   * オブジェクトのメ `Document` ソッドを呼び出して、 `copyToFile` オブジェクトの内容をファイルにコピーします(メソッドから返された `Document``Document``transformPDF` オブジェクトを必ず使用してください)。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[クイック開始（EJBモード）: Java APIを使用したPDFドキュメントの変換](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

[クイック開始（SOAPモード）: Java APIを使用したPDFドキュメントの変換](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したPDFドキュメントの統合 {#flatten-a-pdf-document-using-the-web-service-api}

Output API（Webサービス）を使用して、インタラクティブPDFドキュメントを非インタラクティブPDFドキュメントに統合します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >サーバーホスト `localhost` AEM FormsのIPアドレスに置き換えます。

1. Output Clientオブジェクトを作成します。

   * デフォルトのコンストラクターを使用して `OutputServiceClient` オブジェクトを作成します。
   * コンストラクターを使用して `OutputServiceClient.Endpoint.Address` オブジェクトを作成し `System.ServiceModel.EndpointAddress` ます。 WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/OutputService?blob=mtom`)に渡すstring値を渡します。 属性を使用する必要はありません `lc_version` 。 この属性は、サービス参照を作成する際に使用されます。 ただし、MTOMを使用す `?blob=mtom` るように指定します。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `OutputServiceClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールドにAEM formsのユーザー名を割り当て `OutputServiceClient.ClientCredentials.UserName.UserName`ます。
      * 対応するパスワード値をフィールドに割り当て `OutputServiceClient.ClientCredentials.UserName.Password`ます。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当て `BasicHttpBindingSecurity.Security.Mode`ます。

1. インタラクティブPDFドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、インタラクティブPDFドキュメントの保存に使用されます。
   * コンストラクターを呼び出し、インタラクティブPDF `System.IO.FileStream` ドキュメントのファイルの場所を表すstring値を渡して、オブジェクトを作成します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
   * オブジェクトの `System.IO.FileStream``Read` メソッドを呼び出し、読み取るバイト配列、開始位置およびストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * オブジェクトのプロパティにバイト配列の内容を割り当てて、 `BLOB``MTOM` オブジェクトを入力します。

1. PDFドキュメントを変換します。

   オブジェクトのドキュメントを呼び出し、次の値を渡して、インタラクティブPDFドキュメントを非インタラクティブPDFメソッドに変換し `OutputClient``transformPDF` ます。

   * インタラクティブPDFドキュメントを含む `BLOB` オブジェクトです。
   * 定義済みリスト `TransformationFormat` 値。 非インタラクティブPDFドキュメントを生成するには、を指定し `TransformationFormat.PDF`ます。
   * A `PDFARevisionNumber` enum value that specifies the revision number.
   * 列挙値を使用するかどうかを指定するBoolean値 `PDFARevisionNumber` です。 このパラメーターはPDF/Aドキュメントを対象としているので、指定でき `false`ます。
   * 修正番号と修正年をコロンで区切って表すstring値です。 このパラメーターはPDF/Aドキュメントを対象としているので、指定でき `null`ます。
   * PDF/A準拠レベルを表す `PDFAConformance` enum値です。
   * 列挙値を使用するかどうかを指定するブ `PDFAConformance` ール値。 このパラメーターはPDF/Aドキュメントを対象としているので、指定でき `false`ます。

   非インタラクティブPDFドキュメントを含む `transformPDF``BLOB` オブジェクトを返します。

1. 非インタラクティブPDFドキュメントをPDFファイルとして保存します。

   * コンストラクターを呼び出し、非インタラクティブPDF `System.IO.FileStream` ドキュメントーのファイルの場所を表すstring値を渡して、オブジェクトを作成します。
   * メソッドが返した `BLOB` オブジェクトのデータ内容を格納するバイト配列を作成し `transformPDF` ます。 オブジェクトのデータメンバーの値を取得して、 `BLOB` バイト配列を入力し `MTOM` ます。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡して、バイト配列の内容をPDFファイルに書き込み `System.IO.BinaryWriter` ま `Write` す。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
