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
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d

---


# ドキュメント出力ストリームの作成 {#creating-document-output-streams}

**Outputサービスについて**

Outputサービスを使用すると、ドキュメントをPDF（PDF/Aドキュメントを含む）、PostScript、Printer Control Language(PCL)および次のラベル形式で出力できます。

* Zebra - ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

Outputサービスを使用すると、XMLフォームデータをフォームデザインとマージし、ドキュメントをネットワークプリンターまたはファイルに出力できます。

フォームデザイン（XDPファイル）をOutputサービスに渡す方法は2つあります。 フォームデザインを含むイ `com.adobe.idp.Document` ンスタンスをOutputサービスに渡すこともできます。 または、フォームデザインの場所を指定するURI値を渡すこともできます。 これらの方法は、「AEM formsによるプログラミング」で *説明されています*。

>[!NOTE]
>
>Outputサービスは、アプリケーションオブジェクト固有のスクリプトを含むAcroform PDFドキュメントをサポートしません。 アプリケーションオブジェクト固有のスクリプトを含むAcroform PDFドキュメントはレンダリングされません。

次の節では、URI値を使用してOutputサービスにフォームデザインを渡す方法を示します。

* [PDFドキュメントの作成](creating-document-output-streams.md#creating-pdf-documents)
* [PDF/Aドキュメントの作成](creating-document-output-streams.md#creating-pdf-a-documents)

次の節では、インスタンス内でフォームデザインを渡す方法を示 `com.adobe.idp.Document` します。

* [Content Services（非推奨）内のドキュメントをOutputサービスに渡す](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)
* [フラグメントを使用したPDFドキュメントの作成](creating-document-output-streams.md#creating-pdf-documents-using-fragments)

使用する方法を決定する際に考慮すべき点は、別のAEM Formsサービスからフォームデザインを取得し、それをインスタンス内で渡す場合 `com.adobe.idp.Document` です。 「Passing Documents *to the Output Service* 」と「 *Creating PDF Documents using Fragments* 」の両方の節で、別のAEM Formsサービスからフォームデザインを取得する方法を示します。 最初の節では、Content Services（非推奨）からフォームデザインを取得します。 2つ目の節では、Assemblerサービスからフォームデザインを取得します。

ファイルシステムなどの固定された場所からフォームデザインを取得する場合は、どちらの方法でも使用できます。 つまり、XDPファイルにURI値を指定したり、インスタンスを使用したりで `com.adobe.idp.Document` きます。

PDFドキュメントの作成時にフォームデザインの場所を指定するURI値を渡すには、この方法を使用し `generatePDFOutput` ます。 同様に、PDFドキュメントの作 `com.adobe.idp.Document` 成時にインスタンスをOutputサービスに渡す場合は、このメソッドを使用 `generatePDFOutput2` します。

出力ストリームをネットワークプリンターに送信する場合は、どちらの方法を使用することもできます。 フォームデザインを含むインスタンスを渡して出力ストリー `com.adobe.idp.Document` ムをプリンターに送信するには、このメソッドを使 `sendToPrinter2`用します。 URI値を渡して出力ストリームをプリンターに送信するには、このメソッドを使用 `sendToPrinter`します。 「プリン *ターへの印刷ストリームの送信* 」セクションでは、この方法を `sendToPrinter` 使用します。

Outputサービスを使用して、次のタスクを実行できます。

* [PDFドキュメントの作成](creating-document-output-streams.md#creating-pdf-documents)
* [PDF/Aドキュメントの作成](creating-document-output-streams.md#creating-pdf-a-documents)
* [Content Services（非推奨）内のドキュメントをOutputサービスに渡す](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)
* [フラグメントを使用したPDFドキュメントの作成](creating-document-output-streams.md#creating-pdf-documents-using-fragments)
* [ファイルへの印刷](creating-document-output-streams.md#printing-to-files)
* [プリンターへの印刷ストリームの送信](creating-document-output-streams.md#sending-print-streams-to-printers)
* [複数の出力ファイルの作成](creating-document-output-streams.md#creating-multiple-output-files)
* [検索ルールの作成](creating-document-output-streams.md#creating-search-rules)
* [PDFドキュメントの統合](creating-document-output-streams.md#flattening-pdf-documents)

   ***注意&#x200B;**:Outputサービスについて詳しくは、『AEM Formsサービスリファレ[ンス』を参照してください](https://www.adobe.com/go/learn_aemforms_services_63)。*

## PDFドキュメントの作成 {#creating-pdf-documents}

Outputサービスを使用して、指定したフォームデザインとXMLフォームデータに基づくPDFドキュメントを作成できます。 Outputサービスによって作成されるPDFドキュメントは、インタラクティブPDFドキュメントではありません。ユーザーはフォームデータを入力したり変更したりできません。

長期保存用のPDFドキュメントを作成する場合は、PDF/Aドキュメントを作成することをお勧めします。 (PDF/A [ドキュメントの作成を参照](creating-document-output-streams.md#creating-pdf-a-documents))。

ユーザーがデータを入力できるインタラクティブPDFフォームを作成するには、Formsサービスを使用します。 (インタラクティブPDF [フォームのレンダリングを参照](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms))。

>[!NOTE]
>
>For more information about the Output service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary-of-steps}

PDFドキュメントを作成するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Output clientオブジェクトを作成します。
1. XMLデータソースを参照します。
1. PDF実行時オプションを設定します。
1. レンダリングの実行時オプションを設定します。
1. PDFドキュメントを生成します。
1. 操作の結果を取得します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar（AEM FormsがJBossにデプロイされている場合に必須）
* jbossall-client.jar（AEM FormsがJBossにデプロイされている場合は必須）

aem formsがJBoss以外のサポート対象のJ2EEアプリケーションサーバーにデプロイされている場合は、adobe-utilities.jarファイルとjbossall-client.jarファイルを、AEM formsがデプロイされているJ2EEアプリケーションサーバーに固有のJARファイルに置き換える必要があります。

**Output clientオブジェクトの作成**

プログラムでOutputサービス操作を実行する前に、Outputサービスクライアントオブジェクトを作成する必要があります。 Java APIを使用している場合は、オブジェクトを作成し `OutputClient` ます。 Output webサービスAPIを使用している場合は、オブジェクトを作成し `OutputServiceService` ます。

**XMLデータソースの参照**

データをフォームデザインとマージするには、データを含むXMLデータソースを参照する必要があります。 XML要素は、データを入力するすべてのフォームフィールドに存在する必要があります。 XML要素名は、フィールド名と一致する必要があります。 XML要素がフォームフィールドに対応していない場合、またはXML要素名がフィールド名と一致しない場合、XML要素は無視されます。 すべてのXML要素を指定した場合、XML要素が表示される順序に一致する必要はありません。

次に、ローン申込フォームの例を示します。

![cp_cp_loanformdata](assets/cp_cp_loanformdata.png)

データをこのフォームデザインにマージするには、フォームに対応するXMLデータソースを作成する必要があります。 次のXMLは、住宅ローン申込フォームの例に対応するXDP XMLデータソースを表しています。

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

**PDF実行時オプションの設定**

PDFドキュメントを作成する際に、ファイルのURIオプションを設定します。 このオプションは、Outputサービスが生成するPDFファイルの名前と場所を指定します。

>[!NOTE]
>
>ファイルURIの実行時オプションを設定する代わりに、Outputサービスから返される複雑なデータ型からPDFドキュメントをプログラムで取得できます。 ただし、ファイルURIのランタイムオプションを設定することで、プログラムによってPDFドキュメントを取得するアプリケーションロジックを作成する必要はありません。

**レンダリングの実行時オプションの設定**

レンダリングの実行時オプションは、PDFドキュメントの作成時に設定できます。 これらのオプションは必須ではありませんが（必要なPDF実行時オプションとは異なり）、Outputサービスのパフォーマンス向上などのタスクを実行できます。 例えば、Outputサービスで使用するフォームデザインをキャッシュして、パフォーマンスを向上させることができます。

タグ付きAcrobatフォームを入力として使用する場合、OutputサービスのJavaまたはWebサービスのAPIを使用してタグ付き設定を無効にすることはできません。 プログラムでこのオプションをに設定しようとすると、結 `false`果のPDFドキュメントは引き続きタグ付けされます。

>[!NOTE]
>
>レンダリングの実行時オプションを指定しない場合は、デフォルト値が使用されます。 ランタイムオプションのレンダリングについて詳しくは、クラス参照を参 `RenderOptionsSpec` 照してください。 (『 [AEM Forms APIリファレンス』を参照](https://www.adobe.com/go/learn_aemforms_javadocs_63_en))。

**PDFドキュメントの生成**

フォームデータを含む有効なXMLデータソースを参照し、実行時のオプションを設定したら、Outputサービスを呼び出して、PDFドキュメントを生成できます。

PDFドキュメントを生成する場合は、OutputサービスでPDFドキュメントの作成に必要なURI値を指定します。 フォームデザインは、サーバーファイルシステムなどの場所に、またはAEM Formsアプリケーションの一部として保存できます。 Formsアプリケーションの一部として存在するフォームデザイン（または画像ファイルなど）は、コンテンツルートURI値を使用して参照できま `repository:///`す。 例えば、 *Applications/FormsApplicationという名前のFormsアプリケーション内にある* Loan.xdp *という名前の次のフォームデザインを考えてみます*。

![cp_cp_formrepository](assets/cp_cp_formrepository.png)

前の図に示したLoan.xdpファイルにアクセスするには、オブジェクトのメソッドに渡 `repository:///Applications/FormsApplication/1.0/FormsFolder/` される3番目のパラメーター `OutputClient` として指定 `generatePDFOutput` します。 オブジェクトのメソッドに渡す&#x200B;*2番目のパラメーターとして、フォーム名(* Loan.xdp `OutputClient` )を `generatePDFOutput` 指定します。

XDPファイルに画像（またはフラグメントなどの他のリソース）が含まれている場合は、XDPファイルと同じアプリケーションフォルダーにリソースを配置します。 AEM Formsは、画像への参照を解決するために、コンテンツルートURIをベースパスとして使用します。 例えば、Loan.xdpファイルに画像が含まれている場合は、必ずに画像を配置します `Applications/FormsApplication/1.0/FormsFolder/`。

>[!NOTE]
>
>オブジェクトまたはメソッドを呼び出すときに、Formsアプリケ `OutputClient` ーションURIを参 `generatePDFOutput` 照で `generatePrintedOutput` きます。

>[!NOTE]
>
>Formsアプリケーション内のXDPを参照してPDFドキュメントを作成する完全なクイックスタートについては、クイックスタート(EJBモ [ード)を参照してください。Java APIを使用したアプリケーションXDPファイルに基づくPDFドキュメントの作成](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api)。

**操作の結果の取得**

Outputサービスは、操作の実行後、操作が成功したかどうかを示すステータスXMLデータなど、様々なデータ項目を返します。

**関連トピック**

[Java APIを使用したPDFドキュメントの作成](creating-document-output-streams.md#create-a-pdf-document-using-the-java-api)

[WebサービスAPIを使用したPDFドキュメントの作成](creating-document-output-streams.md#create-a-pdf-document-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[OutputサービスAPIのクイックスタート](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Java APIを使用したPDFドキュメントの作成 {#create-a-pdf-document-using-the-java-api}

Output API(Java)を使用してPDFドキュメントを作成します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-output-client.jarなどのクライアントJARファイルを含めます。

1. Output clientオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `OutputClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. XMLデータソースを参照します。

   * PDFドキュメ `java.io.FileInputStream` ントのコンストラクターを使用し、XMLファイルの場所を指定するstring値を渡すことによって、PDFドキュメントの入力に使用されるXMLデータソースを表すオブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを作成します。Pass the `java.io.FileInputStream` object.

1. PDF実行時オプションを設定します。

   * コンストラクタを使用して `PDFOutputOptionsSpec` オブジェクトを作成します。
   * オブジェクトのメソッドを呼び出して、「File URI」 `PDFOutputOptionsSpec` オプションを設定 `setFileURI` します。 Outputサービスが生成するPDFファイルの場所を指定するstring値を渡します。 「ファイルURI」オプションは、クライアントコンピューターではなく、AEM formsをホストするJ2EEアプリケーションサーバーに対する相対パスです。

1. レンダリングの実行時オプションを設定します。

   * コンストラクタを使用して `RenderOptionsSpec` オブジェクトを作成します。
   * オブジェクトを呼び出して渡すことで、フォームデザインをキャッシュし、Outputサービスのパ `RenderOptionsSpec` フォーマンスを向 `setCacheEnabled` 上させま `true`す。
   >[!NOTE]
   >
   >入力ドキュメントがAcrobatフォーム（Acrobatで作成されたフォーム）または署名済みまたは認証済みのXFAドキュメントである場合は、オブジェクトのメソッドを使用してPDFドキュメントのバージョンを設定することはできません。 `RenderOptionsSpec``setPdfVersion` 出力PDFドキュメントは元のPDFバージョンを保持します。 同様に、入力ドキュメントがAcrobatフォーム、署名済みまたは認証済みのXFAドキュメントである場合は、オブジェクトのメソッドを呼び出して、タグ付きAdobe PDFオ `RenderOptionsSpec``setTaggedPDF` プションを設定することはできません。

   >[!NOTE]
   >
   >入力PDFドキュメントが認証またはデジタル署名されている場合は、オブ `RenderOptionsSpec` ジェクトの方 `setLinearizedPDF` 法を使用して線形化されたPDFオプションを設定することはできません。 (See [Digitally Signing PDF Documents](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)*.)*

1. PDFドキュメントを生成します。

   Create a PDF document by invoking the `OutputClient` object’s `generatePDFOutput` method and passing the following values:

   * 列 `TransformationFormat` 挙値。 PDFドキュメントを生成するには、を指定しま `TransformationFormat.PDF`す。
   * フォームデザイン名を指定する string 値。
   * フォームデザインが存在するコンテンツルートを指定するstring値。
   * PDF実行 `PDFOutputOptionsSpec` 時オプションを含むオブジェクトです。
   * レンダリ `RenderOptionsSpec` ングの実行時オプションを含むオブジェクトです。
   * フォー `com.adobe.idp.Document` ムデザインとマージするデータを含むXMLデータソースを含むオブジェクトです。
   The `generatePDFOutput` method returns an `OutputResult` object that contains the results of the operation.

   >[!NOTE]
   >
   >このメソッドを呼び出してPDFドキュメントを生成す `generatePDFOutput` る場合は、署名または認証されたXFA PDFフォームとデータをマージできないことに注意してください。 (ドキュメント [への電子署名と認証を参照](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-and-certifying-documents)*)。*

   >[!NOTE]
   >
   >オブジ `OutputResult` ェクトのメソッドが `getRecordLevelMetaDataList` 返します `null`*。*

   >[!NOTE]
   >
   >オブジェクトのメソッドを呼び出してPDFドキュメントを作 `OutputClient` 成することもで `generatePDFOutput2` きます。 (Content Services(非推 [奨)内のドキュメントをOutputサービスに渡すを参照](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)*)。*

1. 操作の結果を取得します。

   * オブジェクト `com.adobe.idp.Document` のメソッドを呼び出して、操作のステ `generatePDFOutput` ータスを表すオブジ `OutputResult` ェクトを取得 `getStatusDoc` します。 このメソッドは、操作が成功したかどうかを示すステータスXMLデータを返します。
   * 操作の結果 `java.io.File` を含むオブジェクトを作成します。 ファイル名の拡張子が.xmlであることを確認します。
   * オブジェクト `com.adobe.idp.Document` のメソッドを呼び出 `copyToFile` して、オブジェクトの内容をファイルにコピ `com.adobe.idp.Document` ーします(メソッドによって返されたオブジェクトを使用 `com.adobe.idp.Document` していることを確 `getStatusDoc` 認します)。
   Outputサービスは、オブジェクトのメソッドに渡された引数で指定された場所にPDFドキュメントを書き込みますが、オブジェクトのメソッドを呼び出すことで、プログラム的にPDF/Aドキュメ `PDFOutputOptionsSpec` ントを取得で `setFileURI``OutputResult``getGeneratedDoc` きます。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[クイックスタート（EJBモード）:Java APIを使用したPDFドキュメントの作成](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[クイックスタート（SOAPモード）:Java APIを使用したPDFドキュメントの作成](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したPDFドキュメントの作成 {#create-a-pdf-document-using-the-web-service-api}

Output API（Webサービス）を使用してPDFドキュメントを作成します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. Output clientオブジェクトを作成します。

   * デフォルトのコンス `OutputServiceClient` トラクターを使用して、オブジェクトを作成します。
   * コンストラクタ `OutputServiceClient.Endpoint.Address` ーを使用してオブジェクトを作 `System.ServiceModel.EndpointAddress` 成します。 WSDLを指定するstring値をAEM Formsサービスに渡します(例 `http://localhost:8080/soap/services/OutputService?blob=mtom`:)。属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。 ただし、MTOMを使用す `?blob=mtom` るように指定します。
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `OutputServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `OutputServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `OutputServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. XMLデータソースを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、PDFドキュメントとマージされるXMLデータの保存に使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、フォームデータを含むXMLファイルのファイル位置を表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイト配列、開 `System.IO.FileStream` 始位置、ストリ `Read` ーム長を渡すことによって、バイト配列にストリームデータを設定します。
   * オブジェクト `BLOB` にバイト配列の内容を `MTOM` フィールドに割り当てて、オブジェクトを入力します。

1. PDF実行時オプションの設定

   * コンストラクタを使用して `PDFOutputOptionsSpec` オブジェクトを作成します。
   * 「File URI」オプションを設定するには、Outputサービスが生成するPDFファイルの場所を指定するstring値をオブジェクトのデータメンバ `PDFOutputOptionsSpec` ーに割り当 `fileURI` てます。 「ファイルURI」オプションは、クライアントコンピューターではなく、AEM formsをホストするJ2EEアプリケーションサーバーに対する相対パスです。

1. レンダリングの実行時オプションを設定します。

   * コンストラクタを使用して `RenderOptionsSpec` オブジェクトを作成します。
   * フォームデザインをキャッシュして、オブジェクトのデータメンバーに値を割り当てることで、Outputサ `true` ービスのパフ `RenderOptionsSpec` ォーマンスを向 `cacheEnabled` 上させます。
   >[!NOTE]
   >
   >入力ドキュメントがAcrobatフォーム（Acrobatで作成されたフォーム）または署名済みまたは認証済みのXFAドキュメントである場合は、オブジェクトのメソッドを使用してPDFドキュメントのバージョンを設定することはできません。 `RenderOptionsSpec``setPdfVersion` 出力PDFドキュメントは元のPDFバージョンを保持します。 同様に、入力ドキュメントがAcrobatフォーム、署名済みまたは認証済みのXFAドキュメントである場合、オブジェクトの `RenderOptionsSpec``setTaggedPDF`*メソッドを呼び出してタグ付きAdobe PDFオプションを設定することはできません。*

   >[!NOTE]
   >
   >入力PDFドキュメントが認証済みまたはデジタル署名済みの場合、オブ `RenderOptionsSpec` ジェクトのメ `linearizedPDF` ンバーを使用して線形化されたPDFオプションを設定することはできません。 (See [Digitally Signing PDF Documents](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)*.)*

1. PDFドキュメントを生成します。

   Create a PDF document by invoking the `OutputServiceService` object’s `generatePDFOutput`method and passing the following values:

   * 列 `TransformationFormat` 挙値。 PDFドキュメントを生成するには、を指定しま `TransformationFormat.PDF`す。
   * フォームデザイン名を指定する string 値。
   * フォームデザインが存在するコンテンツルートを指定するstring値。
   * PDF実行 `PDFOutputOptionsSpec` 時オプションを含むオブジェクトです。
   * レンダリ `RenderOptionsSpec` ングの実行時オプションを含むオブジェクトです。
   * フォー `BLOB` ムデザインとマージするデータを含むXMLデータソースを含むオブジェクトです。
   * メソ `BLOB` ッドによって入力されるオブジェ `generatePDFOutput` クト。 このメソッ `generatePDFOutput` ドは、ドキュメントを記述する生成されたメタデータをこのオブジェクトに入力します。 （このパラメーター値はWebサービスの呼び出しにのみ必要です）。
   * メソ `BLOB` ッドによって入力されるオブジェ `generatePDFOutput` クト。 メソッド `generatePDFOutput` は、このオブジェクトに結果データを入力します。 （このパラメーター値はWebサービスの呼び出しにのみ必要です）。
   * 操作 `OutputResult` の結果を含むオブジェクトです。 （このパラメーター値はWebサービスの呼び出しにのみ必要です）。
   >[!NOTE]
   >
   >このメソッドを呼び出してPDFドキュメントを生成す `generatePDFOutput` る場合は、署名または認証されたXFA PDFフォームとデータをマージできないことに注意してください。 (ドキュメント [への電子署名と認証を参照](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-and-certifying-documents)*)。*

   >[!NOTE]
   >
   >オブジェクトのメソッドを呼び出してPDFドキュメントを作 `OutputClient` 成することもで `generatePDFOutput2` きます。 (Content Services(非推 [奨)内のドキュメントをOutputサービスに渡すを参照](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service)*)。*

1. 操作の結果を取得します。

   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、結果データを含むXMLファイルの場所を表すstring値を渡します。 ファイル名の拡張子が.xmlであることを確認します。
   * オブジェクトのメソッド（8番目のパラメーター）によって結果デ `BLOB` ータが入力されたオブジェクトのデータコンテンツを格納 `OutputServiceService` するバ `generatePDFOutput` イト配列を作成します。 オブジェクトの値を取得して、バイト配列 `BLOB` を設定しま `MTOM``field`す。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡すことで、バイ `System.IO.BinaryWriter` ト配列の内 `Write` 容をXMLファイルに書き込みます。
   関連トピック

   [手順の概要](creating-document-output-streams.md#summary-of-steps)

   [MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

   [SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

   >[!NOTE]
   >
   >オブジ `OutputServiceService` ェクトのメソッド `generateOutput` は非推奨です。

## PDF/Aドキュメントの作成 {#creating-pdf-a-documents}

Outputサービスを使用してPDF/Aドキュメントを作成できます。 PDF/Aはドキュメントのコンテンツを長期保存するためのアーカイブ形式なので、すべてのフォントが埋め込まれ、ファイルは圧縮されません。 その結果、通常、PDF/A ドキュメントは標準の PDF ドキュメントよりも大きくなります。また、PDF/Aドキュメントにはオーディオおよびビデオコンテンツは含まれません。 他のOutputサービスのタスクと同様に、フォームデザインとフォームデザインとマージするデータの両方を提供して、PDF/Aドキュメントを作成します。

PDF/A-1仕様は、2つの準拠レベル（aとb）で構成されています。この2つの主な違いは、論理構造（アクセシビリティ）のサポートに関するもので、準拠レベルbには必要ありません。準拠レベルに関係なく、PDF/A-1では、生成されたPDF/Aドキュメントにすべてのフォントが埋め込まれます。

PDF/AはPDFドキュメントのアーカイブの標準ですが、標準PDFドキュメントが会社のニーズを満たしている場合に、PDF/Aをアーカイブに使用する必要はありません。 PDF/A標準の目的は、ドキュメントの保存要件に合わせて長期間保存できるPDFファイルを確立することです。 例えば、URLが時間の経過と共に無効になる可能性があるので、URLをPDF/Aに埋め込むことはできません。

組織は、独自のニーズ、ドキュメントの保存期間、ファイルサイズに関する考慮事項を評価し、独自のアーカイブ戦略を決定する必要があります。 DocConverterサービスを使用すると、PDFドキュメントがPDF/Aに準拠しているかどうかをプログラムで判断できます。 (「プログラ [ムによるPDF/Aの準拠の判定](/help/forms/developing/pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)」を参照)。

PDF/Aドキュメントでは、フォームデザインで指定されたフォントを使用する必要があり、フォントを置き換えることはできません。 その結果、PDFドキュメント内のフォントがホストのオペレーティングシステム(OS)で使用できない場合は、例外が発生します。

PDF/AドキュメントをAcrobatで開くと、次の図に示すように、ドキュメントがPDF/Aドキュメントであることを確認するメッセージが表示されます。

![cp_cp_pdfamessage](assets/cp_cp_pdfamessage.png)

>[!NOTE]
>
>AIIMのWebサイトには、PDF/A FAQの節があり、https://www.aiim.org/documents/standards/19005-1_FAQ.pdfからアクセスでき [ます](https://www.aiim.org/documents/standards/19005-1_FAQ.pdf)。

>[!NOTE]
>
>For more information about the Output service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-1}

PDF/Aドキュメントを作成するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Output clientオブジェクトを作成します。
1. XMLデータソースを参照します。
1. PDF/Aランタイムオプションを設定します。
1. レンダリングの実行時オプションを設定します。
1. PDF/Aドキュメントを生成します。
1. 操作の結果を取得します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。 Javaを使用してカスタムアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar（AEM FormsがJBossにデプロイされている場合に必須）
* jbossall-client.jar（AEM FormsがJBossにデプロイされている場合は必須）

aem formsがJBoss以外のサポート対象のJ2EEアプリケーションサーバーにデプロイされている場合は、adobe-utilities.jarファイルとjbossall-client.jarファイルを、AEM formsがデプロイされているJ2EEアプリケーションサーバーに固有のJARファイルに置き換える必要があります。

**Output clientオブジェクトの作成**

プログラムでOutputサービス操作を実行する前に、Outputサービスクライアントオブジェクトを作成する必要があります。 Java APIを使用している場合は、オブジェクトを作成し `OutputClient` ます。 Output webサービスAPIを使用している場合は、オブジェクトを作成し `OutputServiceService` ます。

**XMLデータソースの参照**

データをフォームデザインとマージするには、データを含むXMLデータソースを参照する必要があります。 データを入力するすべてのフォームフィールドにXML要素が存在する必要があります。 XML要素名は、フィールド名と一致する必要があります。 XML要素がフォームフィールドに対応していない場合、またはXML要素名がフィールド名と一致しない場合、XML要素は無視されます。 すべてのXML要素を指定した場合、XML要素が表示される順序に一致する必要はありません。

**PDF/Aランタイムオプションの設定**

PDF/Aドキュメントの作成時に、「ファイルURI」オプションを設定できます。 このURIは、AEM formsをホストするJ2EEアプリケーションサーバーに対する相対パスです。 つまり、C:\Adobeを設定した場合、ファイルはクライアントコンピューターではなく、サーバー上のフォルダーに書き込まれます。 URIは、Outputサービスが生成するPDF/Aファイルの名前と場所を指定します。

**レンダリングの実行時オプションの設定**

レンダリングの実行時オプションは、PDF/Aドキュメントの作成時に設定できます。 設定できるPDF/A関連のオプションは、との値 `PDFAConformance` の2つ `PDFARevisionNumber` です。 The `PDFAConformance` value refers to how a PDF document adheres to requirements that specify how long-term electronic documents are preserved. このオプションの有効な値はと `A` です `B`。 レベルaとbの準拠について詳しくは、「 *ISO 19005-1 Document management」というPDF/A-1 ISO仕様を参照してください*。

この値 `PDFARevisionNumber` は、PDF/Aドキュメントのリビジョン番号を参照します。 PDF/Aドキュメントのリビジョン番号について詳しくは、「 *ISO 19005-1 Document management」というPDF/A-1 ISO仕様を参照してください*。

>[!NOTE]
>
>PDF/A 1A文書を作成する場合、タグ付きAdobe PDFオ `false` プションをに設定することはできません。 PDF/A 1Aは、常にタグ付きPDFドキュメントになります。 また、PDF/A 1Bドキュメントを作成する際に、タグ付きAdobe PDF `true` オプションをに設定することはできません。 PDF/A 1Bは、常にタグなしPDFドキュメントになります。

**PDF/Aドキュメントの生成**

フォームデータを含む有効なXMLデータソースを参照し、実行時のオプションを設定したら、Outputサービスを呼び出して、PDF/Aドキュメントを生成できます。

**操作の結果の取得**

Outputサービスは、操作の実行後、操作が成功したかどうかを示すXMLデータなど、様々なデータ項目を返します。

**関連トピック**

[Java APIを使用したPDF/Aドキュメントの作成](creating-document-output-streams.md#create-a-pdf-a-document-using-the-java-api)

[WebサービスAPIを使用したPDF/Aドキュメントの作成](creating-document-output-streams.md#create-a-pdf-a-document-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[OutputサービスAPIのクイックスタート](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Java APIを使用したPDF/Aドキュメントの作成 {#create-a-pdf-a-document-using-the-java-api}

Output API(Java)を使用してPDF/Aドキュメントを作成します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-output-client.jarなどのクライアントJARファイルを含めます。

1. Output clientオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `OutputClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. XMLデータソースを参照します。

   * PDF/Aドキ `java.io.FileInputStream` ュメントのコンストラクターを使用し、XMLファイルの場所を指定するstring値を渡すことによって、PDF/Aドキュメントの入力に使用されるXMLデータソースを表すオブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PDF/Aランタイムオプションを設定します。

   * コンストラクタを使用して `PDFOutputOptionsSpec` オブジェクトを作成します。
   * オブジェクトのメソッドを呼び出して、「File URI」 `PDFOutputOptionsSpec` オプションを設定 `setFileURI` します。 Outputサービスが生成するPDFファイルの場所を指定するstring値を渡します。 「ファイルURI」オプションは、クライアントコンピューターではなく、AEM formsをホストするJ2EEアプリケーションサーバーに対する相対パスです。

1. レンダリングの実行時オプションを設定します。

   * コンストラクタを使用して `RenderOptionsSpec` オブジェクトを作成します。
   * オブジェクト `PDFAConformance` のメソッドを呼び出 `RenderOptionsSpec` し、準拠レベ `setPDFAConformance` ルを指定する列挙 `PDFAConformance` 値を渡して、値を設定します。 例えば、準拠レベルAを指定するには、を渡しま `PDFAConformance.A`す。
   * オブジェクト `PDFARevisionNumber` のメソッドを呼び出し `RenderOptionsSpec` て渡すことで、値 `setPDFARevisionNumber` を設定しま `PDFARevisionNumber.Revision_1`す。
   >[!NOTE]
   >
   >PDF/AドキュメントのPDFバージョンは、オブジェクトのメソッドに指定した値に関係なく1.4 `RenderOptionsSpec` になり `setPdfVersion`*ます。*

1. PDF/Aドキュメントを生成します。

   オブジェクトのメソッドを呼び出し、次 `OutputClient` の値を渡して、PDF/A `generatePDFOutput` ドキュメントを作成します。

   * 列 `TransformationFormat` 挙値。 PDF/Aドキュメントを生成するには、を指定しま `TransformationFormat.PDFA`す。
   * フォームデザイン名を指定する string 値。
   * フォームデザインが存在するコンテンツルートを指定するstring値。
   * PDF実行 `PDFOutputOptionsSpec` 時オプションを含むオブジェクトです。
   * レンダリ `RenderOptionsSpec` ングの実行時オプションを含むオブジェクトです。
   * フォー `com.adobe.idp.Document` ムデザインとマージするデータを含むXMLデータソースを含むオブジェクトです。
   The `generatePDFOutput` method returns an `OutputResult` object that contains the results of the operation.

   >[!NOTE]
   >
   >オブジ `OutputResult` ェクトのメソッドが `getRecordLevelMetaDataList` 返します `null`。

   >[!NOTE]
   >
   >PDF/Aドキュメントは、オブジェクトの `OutputClient``generatePDFOutput`2メソッドを呼び出して作成することもできます。 (Content Services(非推 [奨)内のドキュメントをOutputサービスに渡すを参照](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service))。

1. 操作の結果を取得します。

   * オブジェクト `com.adobe.idp.Document` のメソッドを呼び出して、メソッドのステ `generatePDFOutput` ータスを表すオ `OutputResult` ブジェクトを作成 `getStatusDoc` します。
   * 操作の結 `java.io.File` 果を含むオブジェクトを作成します。 ファイル名の拡張子が.xmlであることを確認します。
   * オブジェクト `com.adobe.idp.Document` のメソッドを呼び出 `copyToFile` して、オブジェクトの内容をファイルにコピ `com.adobe.idp.Document` ーします(メソッドによって返されたオブジェクトを使用 `com.adobe.idp.Document` していることを確 `getStatusDoc` 認します)。
   >[!NOTE]
   >
   >Outputサービスは、オブジェクトのメソッドに渡された引数で指定された場所にPDF/Aドキュメントを書き込みますが、プログラムによってPDF/Aドキュメントを取得するには、オブジェクトのメソッドを呼び出 `PDFOutputOptionsSpec` し `setFileURI``OutputResult``getGeneratedDoc` ます。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[クイックスタート（SOAPモード）:Java APIを使用したPDF/Aドキュメントの作成](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-a-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

### WebサービスAPIを使用したPDF/Aドキュメントの作成 {#create-a-pdf-a-document-using-the-web-service-api}

Output API（Webサービス）を使用してPDF/Aドキュメントを作成します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. Output clientオブジェクトを作成します。

   * デフォルトのコンス `OutputServiceClient` トラクターを使用して、オブジェクトを作成します。
   * コンストラクタ `OutputServiceClient.Endpoint.Address` ーを使用してオブジェクトを作 `System.ServiceModel.EndpointAddress` 成します。 WSDLを指定するstring値をAEM Formsサービスに渡します(例 `http://localhost:8080/soap/services/OutputService?blob=mtom`:)。属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。 ただし、MTOMを使用す `?blob=mtom` るように指定します。
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `OutputServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `OutputServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `OutputServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. XMLデータソースを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、PDF/Aドキュメントとマージされるデータの保存に使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、暗号化するPDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイト配列、開 `System.IO.FileStream` 始位置、ストリ `Read` ーム長を渡すことによって、バイト配列にストリームデータを設定します。
   * オブジェクトにバ `BLOB` イト配列の内容をフ `MTOM` ィールドに割り当てて、オブジェクトを入力します。

1. PDF/Aランタイムオプションを設定します。

   * コンストラクタを使用して `PDFOutputOptionsSpec` オブジェクトを作成します。
   * 「File URI」オプションを設定するには、Outputサービスが生成するPDFファイルの場所を指定するstring値をオブジェクトのデータメンバ `PDFOutputOptionsSpec` ーに割り当 `fileURI` てます。 「ファイルURI」オプションは、クライアントコンピューターではなく、AEM formsをホストするJ2EEアプリケーションサーバーに対する相対パスです

1. レンダリングの実行時オプションを設定します。

   * コンストラクタを使用して `RenderOptionsSpec` オブジェクトを作成します。
   * オブジェクト `PDFAConformance` のデータメンバーに列挙 `PDFAConformance` 値を割り当てて、 `RenderOptionsSpec` 値を設定 `PDFAConformance` します。 例えば、準拠レベルAを指定するには、このデータメン `PDFAConformance.A` バーに割り当てます。
   * オブジェクト `PDFARevisionNumber` のデータメンバーに列挙 `PDFARevisionNumber` 値を割り当てて、 `RenderOptionsSpec` 値を設定 `PDFARevisionNumber` します。 このデ `PDFARevisionNumber.Revision_1` ータメンバに割り当てます。
   >[!NOTE]
   >
   >PDF/AドキュメントのPDFバージョンは、指定した値に関係なく1.4です。

1. PDF/Aドキュメントを生成します。

   Create a PDF document by invoking the `OutputServiceService` object’s `generatePDFOutput`method and passing the following values:

   * TransformationFormat列挙値。 PDFドキュメントを生成するには、を指定しま `TransformationFormat.PDFA`す。
   * フォームデザイン名を指定する string 値。
   * フォームデザインが存在するコンテンツルートを指定するstring値。
   * PDF実行 `PDFOutputOptionsSpec` 時オプションを含むオブジェクトです。
   * レンダリ `RenderOptionsSpec` ングの実行時オプションを含むオブジェクトです。
   * フォー `BLOB` ムデザインとマージするデータを含むXMLデータソースを含むオブジェクトです。
   * メソ `BLOB` ッドによって入力されるオブジェ `generatePDFOutput` クト。 このメソッ `generatePDFOutput` ドは、ドキュメントを記述する生成されたメタデータをこのオブジェクトに入力します。 （このパラメーター値は、Webサービスの呼び出しのみに必要です。）
   * メソ `BLOB` ッドによって入力されるオブジェ `generatePDFOutput` クト。 メソッド `generatePDFOutput` は、このオブジェクトに結果データを入力します。 （このパラメーター値は、Webサービスの呼び出しのみに必要です。）
   * 操作 `OutputResult` の結果を含むオブジェクトです。 （このパラメーター値は、Webサービスの呼び出しのみに必要です。）
   >[!NOTE]
   >
   >PDF/Aドキュメントは、オブジェクトの `OutputClient``generatePDFOutput`2メソッドを呼び出して作成することもできます。 (Content Services(非推 [奨)内のドキュメントをOutputサービスに渡すを参照](creating-document-output-streams.md#passing-documents-located-in-content-services-deprecated-to-the-output-service))。

1. 操作の結果を取得します。

   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、結果データを含むXMLファイルの場所を表すstring値を渡します。 ファイル名の拡張子が.xmlであることを確認します。
   * オブジェクトのメソッド（8番目のパラメーター）によって結果デ `BLOB` ータが入力されたオブジェクトのデータコンテンツを格納 `OutputServiceService` するバ `generatePDFOutput` イト配列を作成します。 オブジェクトのフィールドの値を取得して、バイト `BLOB` 配列を設定し `MTOM` ます。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡すことで、バイ `System.IO.BinaryWriter` ト配列の内 `Write` 容をXMLファイルに書き込みます。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Content Services（非推奨）内のドキュメントをOutputサービスに渡す {#passing-documents-located-in-content-services-deprecated-to-the-output-service}

Outputサービスは、通常はXDPファイルとして保存され、Designerで作成されたフォームデザインに基づく非インタラクティブPDFフォームをレンダリングします。 フォームデザインを含 `com.adobe.idp.Document` むオブジェクトをOutputサービスに渡すことができます。 次に、Outputサービスはオブジェクト内のフォームデザインをレンダリング `com.adobe.idp.Document` します。

オブジェクトをOutputサービスに渡 `com.adobe.idp.Document` す利点の1つは、他のAEM Formsサービス操作がインスタンスを返すこと `com.adobe.idp.Document` です。 つまり、別のサービス操作からインスタンスを取 `com.adobe.idp.Document` 得し、それをレンダリングすることができます。 例えば、次の図に示すように、XDPファイルがという名前のContent Services（非推奨）ノードに `/Company Home/Form Designs`保存されているとします。

プログラムによってContent Services（非推奨）からLoan.xdpを取得し、オブジェクト内のOutputサービスにXDPファイルを渡すことがで `com.adobe.idp.Document` きます。

>[!NOTE]
>
>For more information about the Forms service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-2}

Content Services（非推奨）から取得したドキュメントをOutputサービスに渡すには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. OutputおよびDocument Management Client APIオブジェクトを作成します。
1. Content Services（非推奨）からフォームデザインを取得します。
1. 非インタラクティブPDFフォームをレンダリングします。
1. データストリームを使用してアクションを実行します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを含めます。

**OutputおよびDocument Management Client APIオブジェクトの作成**

プログラムでOutputサービスAPI操作を実行する前に、Output Client APIオブジェクトを作成します。 また、このワークフローはContent Services（非推奨）からXDPファイルを取得するので、Document Management APIオブジェクトを作成します。

**Content Services（非推奨）からフォームデザインを取得する**

JavaまたはWebサービスAPIを使用して、Content Services（非推奨）からXDPファイルを取得します。 XDPファイルは、インスタンス(Webサービ `com.adobe.idp.Document` スを使用している場 `BLOB` 合はインスタンス)内で返されます。 その後、インスタンスをOutput `com.adobe.idp.Document` サービスに渡すことができます。

**非インタラクティブPDFフォームのレンダリング**

非インタラクティブフォームをレンダリングするには、Content Services(非推 `com.adobe.idp.Document` 奨)から返されたインスタンスをOutputサービスに渡します。

>[!NOTE]
>
>フォームデザインを含むオ `generatePDFOutput2`ブジェクトを受け `eneratePrintedOutput2`入れる、と `com.adobe.idp.Document` いう名前の2つの新しいメソッド。 また、印刷ストリームをネ `com.adobe.idp.Document`ットワークプリンターに送信する際に、フォームデザインを含むをOutputサービスに渡すこともできます。

**フォームデータストリームを使用したアクションの実行**

非インタラクティブフォームをPDFファイルとして保存できます。 フォームはAdobe readerまたはAcrobatで表示できます。

**関連トピック**

[Java APIを使用したOutput Serviceへのドキュメントの渡し](creating-document-output-streams.md#pass-documents-to-the-output-service-using-the-java-api)

[WebサービスAPIを使用してOutput Serviceにドキュメントを渡す](creating-document-output-streams.md#pass-documents-to-the-output-service-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[OutputサービスAPIのクイックスタート](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

[フラグメントを使用したPDFドキュメントの作成](creating-document-output-streams.md#creating-pdf-documents-using-fragments)

### Java APIを使用したOutput Serviceへのドキュメントの渡し {#pass-documents-to-the-output-service-using-the-java-api}

OutputサービスとContent Services（非推奨）API(Java)を使用してContent Services（非推奨）から取得したドキュメントを渡します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-output-client.jarやadobe-contentservices-client.jarなどのクライアントJARファイルを含めます。

1. OutputおよびDocument Management Client APIオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。（[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照。）
   * Create an `OutputClient` object by using its constructor and passing the `ServiceClientFactory` object.
   * コンストラクタを使用して `DocumentManagementServiceClientImpl` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. Content Services（非推奨）からフォームデザインを取得します。

   オブジェクト `DocumentManagementServiceClientImpl` のメソッドを `retrieveContent` 呼び出し、次の値を渡します。

   * コンテンツが追加されるストアを指定するstring値。 The default store is `SpacesStore`. この値は必須パラメーターです。
   * 取得するコンテンツの完全修飾パスを指定するstring値(例 `/Company Home/Form Designs/Loan.xdp`えば)。 この値は必須パラメーターです。
   * バージョンを指定するstring値。 この値はオプションのパラメーターで、空の文字列を渡すことができます。 この場合、最新バージョンが取得されます。
   このメ `retrieveContent` ソッドは、XDPファ `CRCResult` イルを含むオブジェクトを返します。 オブジェクトの `com.adobe.idp.Document` メソッドを呼び出して、イ `CRCResult` ンスタンスを取得 `getDocument` します。

1. 非インタラクティブPDFフォームをレンダリングします。

   オブジェクト `OutputClient` のメソッドを `generatePDFOutput2` 呼び出し、次の値を渡します。

   * 列 `TransformationFormat` 挙値。 PDFドキュメントを生成するには、を指定しま `TransformationFormat.PDF`す。
   * 画像などの追加リソースが存在するコンテンツルートを指定するstring値。
   * フォ `com.adobe.idp.Document` ームデザインを表すオブジェクト(オブジェクトのメソッドから返され `CRCResult` るインスタ `getDocument` ンスを使用)。
   * PDF実行 `PDFOutputOptionsSpec` 時オプションを含むオブジェクトです。
   * レンダリ `RenderOptionsSpec` ングの実行時オプションを含むオブジェクトです。
   * フォー `com.adobe.idp.Document` ムデザインとマージするデータを含むXMLデータソースを含むオブジェクトです。
   The `generatePDFOutput2` method returns an `OutputResult` object that contains the results of the operation.

1. フォームデータストリームを使用してアクションを実行します。

   * オブジェクト `com.adobe.idp.Document` のメソッドを呼び出して、非インタラクティブフォームを表すオ `OutputResult` ブジェクトを取得 `getGeneratedDoc` します。
   * 操作の結果 `java.io.File` を含むオブジェクトを作成します。 ファイル名の拡張子が.pdfであることを確認します。
   * オブジェクト `com.adobe.idp.Document` のメソッドを呼び出 `copyToFile` して、オブジェクトの内容をファイルにコピ `com.adobe.idp.Document` ーします(メソッドによって返されたオブジェクトを使用 `com.adobe.idp.Document` していることを確 `getGeneratedDoc` 認します)。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[クイックスタート（EJBモード）:Java APIを使用してOutputサービスにドキュメントを渡す](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[クイックスタート（SOAPモード）:Java APIを使用してOutputサービスにドキュメントを渡す](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用してOutput Serviceにドキュメントを渡す {#pass-documents-to-the-output-service-using-the-web-service-api}

OutputサービスとContent Services（非推奨）API（Webサービス）を使用して、Content Services（非推奨）から取得したドキュメントを渡します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 このクライアントアプリケーションは2つのAEM Formsサービスを呼び出すので、2つのサービス参照を作成します。 Outputサービスに関連付けられているサービス参照に対して、次のWSDL定義を使用します。 `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   Document Managementサービスに関連付けられているサービス参照に対して、次のWSDL定義を使用します。 `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`.

   このデータ `BLOB` 型は両方のサービス参照に共通なので、使用する際にはデータ型 `BLOB` を完全に修飾してください。 対応するWebサービスのクイックスタートでは、すべてのインスタ `BLOB` ンスが完全修飾されています。

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. OutputおよびDocument Management Client APIオブジェクトを作成します。

   * デフォルトのコンス `OutputServiceClient` トラクターを使用して、オブジェクトを作成します。
   * コンストラクタ `OutputServiceClient.Endpoint.Address` ーを使用してオブジェクトを作 `System.ServiceModel.EndpointAddress` 成します。 WSDLを指定するstring値をFormsサービスに渡します(例 `http://localhost:8080/soap/services/OutputService?blob=mtom`えば)。 属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。)
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `OutputServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `OutputServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `OutputServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
   * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。
   >[!NOTE]
   >
   >サービスクライアントに対して、この手順 `DocumentManagementServiceClient`を繰り返します。

1. Content Services（非推奨）からフォームデザインを取得します。

   オブジェクトのメソッドを呼び出し、 `DocumentManagementServiceClient` 次の値を渡 `retrieveContent` して、コンテンツを取得します。

   * コンテンツが追加されるストアを指定するstring値。 The default store is `SpacesStore`. この値は必須パラメーターです。
   * 取得するコンテンツの完全修飾パスを指定するstring値(例 `/Company Home/Form Designs/Loan.xdp`えば)。 この値は必須パラメーターです。
   * バージョンを指定するstring値。 この値はオプションのパラメーターで、空の文字列を渡すことができます。 この場合、最新バージョンが取得されます。
   * ブラウズリンクの値を格納する文字列出力パラメータ。
   * コンテ `BLOB` ンツを保存する出力パラメーター。 この出力パラメーターを使用して、コンテンツを取得できます。
   * コンテンツ `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` 属性を格納する出力パラメーター。
   * 出力パ `CRCResult` ラメーター。 このオブジェクトを使用する代わりに、出力パラメーターを使用し `BLOB` てコンテンツを取得することができます。

1. 非インタラクティブPDFフォームをレンダリングします。

   オブジェクト `OutputServiceClient` のメソッドを `generatePDFOutput2` 呼び出し、次の値を渡します。

   * 列 `TransformationFormat` 挙値。 PDFドキュメントを生成するには、を指定しま `TransformationFormat.PDF`す。
   * 画像などの追加リソースが存在するコンテンツルートを指定するstring値。
   * フォーム `BLOB` デザインを表すオブジェクト(Content Services（非推奨） `BLOB` から返されるインスタンスを使用)。
   * PDF実行 `PDFOutputOptionsSpec` 時オプションを含むオブジェクトです。
   * レンダリ `RenderOptionsSpec` ングの実行時オプションを含むオブジェクトです。
   * フォー `BLOB` ムデザインとマージするデータを含むXMLデータソースを含むオブジェクトです。
   * メソッドに `BLOB` よって設定される出力オブジェクト `generatePDFOutput2` です。 このメソッ `generatePDFOutput2` ドは、ドキュメントを記述する生成されたメタデータをこのオブジェクトに入力します。 （このパラメーター値はWebサービスの呼び出しにのみ必要です）。
   * 操作の結 `OutputResult` 果を含む出力オブジェクトです。 （このパラメーター値はWebサービスの呼び出しにのみ必要です）。
   このメソ `generatePDFOutput2` ッドは、非インタラ `BLOB` クティブPDFフォームを含むオブジェクトを返します。

1. フォームデータストリームを使用してアクションを実行します。

   * Create a `System.IO.FileStream` object by invoking its constructor. インタラクティブPDFドキュメントのファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * メソッドから取得したオブジェクトの内容を格納す `BLOB` るバイト配列を作成 `generatePDFOutput2` します。 オブジェクトのデータメンバーの値を取得して、バ `BLOB` イト配列を `MTOM` 設定します。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡すことで、バ `System.IO.BinaryWriter` イト配列の内 `Write` 容をPDFファイルに書き込みます。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## リポジトリ内のドキュメントをOutputサービスに渡す {#passing-documents-located-in-the-repository-to-the-output-service}

Outputサービスは、通常はXDPファイルとして保存され、Designerで作成されたフォームデザインに基づく非インタラクティブPDFフォームをレンダリングします。 フォームデザインを含 `com.adobe.idp.Document` むオブジェクトをOutputサービスに渡すことができます。 次に、Outputサービスはオブジェクト内のフォームデザインをレンダリング `com.adobe.idp.Document` します。

オブジェクトをOutputサービスに渡 `com.adobe.idp.Document` す利点の1つは、他のAEM Formsサービス操作がインスタンスを返すこと `com.adobe.idp.Document` です。 つまり、別のサービス操作からインスタンスを取 `com.adobe.idp.Document` 得し、それをレンダリングすることができます。 例えば、次の図に示すように、XDPファイルがAEM Formsリポジトリに保存されているとします。

![pd_pd_formrepository](assets/pd_pd_formrepository.png)

FormsFolder *フォルダーは* 、AEM Formsリポジトリ内のユーザー定義の場所です（この場所は例で、デフォルトでは存在しません）。 この例では、Loan.xdpという名前のフォームデザインがこのフォルダーに配置されています。 フォームデザインに加えて、画像などの他のフォームコラテラルもこの場所に保存できます。 AEM Formsリポジトリ内のリソースへのパスは次のとおりです。

`Applications/Application-name/Application-version/Folder.../Filename`

プログラムによってAEM FormsリポジトリからLoan.xdpを取得し、オブジェクト内のOutputサービスに渡すことがで `com.adobe.idp.Document` きます。

リポジトリ内のXDPファイルに基づいてPDFを作成するには、次の2つの方法があります。 XDPの場所は、参照によって渡すことも、プログラムによってリポジトリからXDPを取得し、XDPファイル内のOutputサービスに渡すこともできます。

[クイックスタート（EJBモード）:Java APIを使用したアプリケーションXDPファイルに基づくPDFドキュメントの作成](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-an-application-xdp-file-using-the-java-api) （参照でXDPファイルの場所を渡す方法を示します）。

[クイックスタート（EJBモード）:Java APIを使用してAEM Formsリポジトリ内のドキュメントをOutputサービスに渡す(AEM Forms RepositoryからXDPファイルをプログラム的に取得し、インスタンス内でOutputサービスに渡す方法を示](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api)`com.adobe.idp.Document` します)。 （この節では、このタスクの実行方法について説明します）。

>[!NOTE]
>
>For more information about the Forms service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-3}

AEM Formsリポジトリから取得したドキュメントをOutputサービスに渡すには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. OutputおよびDocument Management Client APIオブジェクトを作成します。
1. AEM Formsリポジトリからフォームデザインを取得します。
1. 非インタラクティブPDFフォームをレンダリングします。
1. データストリームを使用してアクションを実行します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを含めます。

**OutputおよびDocument Management Client APIオブジェクトの作成**

プログラムでOutputサービスAPI操作を実行する前に、Output Client APIオブジェクトを作成します。 また、このワークフローはContent Services（非推奨）からXDPファイルを取得するので、Document Management APIオブジェクトを作成します。

**AEM Formsリポジトリからフォームデザインを取得する**

Repository APIを使用して、AEM FormsリポジトリからXDPファイルを取得します。 ( [Reading Resources](/help/forms/developing/aem-forms-repository.md#reading-resources)を参照)。

XDPファイルは、インスタンス(Webサービ `com.adobe.idp.Document` スを使用している場 `BLOB` 合はインスタンス)内で返されます。 その後、インスタンスをOutput `com.adobe.idp.Document` サービスに渡すことができます。

**非インタラクティブPDFフォームのレンダリング**

非インタラクティブフォームをレンダリングするには、AEM Forms Repository API `com.adobe.idp.Document` を使用して返されたインスタンスを渡します。

>[!NOTE]
>
>フォームデザインを含むオブジ `generatePDFOutput2`ェクトの `generatePrintedOutput2`名前と受け `com.adobe.idp.Document`入れる2つの新しいメソッドが追加されました。 また、印刷ストリームをネ `com.adobe.idp.Document` ットワークプリンターに送信する際に、フォームデザインを含むフォームをOutputサービスに渡すこともできます。

**フォームデータストリームを使用したアクションの実行**

非インタラクティブフォームをPDFファイルとして保存できます。 フォームはAdobe readerまたはAcrobatで表示できます。

**関連トピック**

[Java APIを使用してリポジトリ内のドキュメントをOutputサービスに渡す](creating-document-output-streams.md#pass-documents-located-in-the-repository-to-the-output-service-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[OutputサービスAPIのクイックスタート](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

ResourceRepositoryClient

### Java APIを使用してリポジトリ内のドキュメントをOutputサービスに渡す {#pass-documents-located-in-the-repository-to-the-output-service-using-the-java-api}

OutputサービスとRepository API(Java)を使用して、リポジトリから取得したドキュメントを渡します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-output-client.jarやadobe-repository-client.jarなどのクライアントJARファイルを含めます。

1. OutputおよびDocument Management Client APIオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。（[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照。）
   * Create an `OutputClient` object by using its constructor and passing the `ServiceClientFactory` object.
   * コンストラクタを使用して `DocumentManagementServiceClientImpl` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. AEM Formsリポジトリからフォームデザインを取得します。

   オブジェクト `ResourceRepositoryClient` のメソッ `readResourceContent` ドを呼び出し、URIの場所を指定するstring値をXDPファイルに渡します。 For example, `/Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`. この値は必須です。 このメソッドは、XDPフ `com.adobe.idp.Document` ァイルを表すインスタンスを返します。

1. 非インタラクティブPDFフォームをレンダリングします。

   オブジェクト `OutputClient` のメソッドを `generatePDFOutput2` 呼び出し、次の値を渡します。

   * 列 `TransformationFormat` 挙値。 PDFドキュメントを生成するには、を指定しま `TransformationFormat.PDF`す。
   * 画像などの追加リソースが存在するコンテンツルートを指定するstring値。 For example, `repository:///Applications/FormsApplication/1.0/FormsFolder/`.
   * フォ `com.adobe.idp.Document` ームデザインを表すオブジェクト(オブジェクトのメソッドから返され `ResourceRepositoryClient` るインスタ `readResourceContent` ンスを使用)。
   * PDF実行 `PDFOutputOptionsSpec` 時オプションを含むオブジェクトです。
   * レンダリ `RenderOptionsSpec` ングの実行時オプションを含むオブジェクトです。
   * フォー `com.adobe.idp.Document` ムデザインとマージするデータを含むXMLデータソースを含むオブジェクトです。
   The `generatePDFOutput2` method returns an `OutputResult` object that contains the results of the operation.

1. フォームデータストリームを使用してアクションを実行します。

   * オブジェクト `com.adobe.idp.Document` のメソッドを呼び出して、非インタラクティブフォームを表すオ `OutputResult` ブジェクトを取得 `getGeneratedDoc` します。
   * 操作の結果 `java.io.File` を含むオブジェクトを作成します。 ファイル名の拡張子が.pdfであることを確認します。
   * オブジェクト `com.adobe.idp.Document` のメソッドを呼び出 `copyToFile` して、オブジェクトの内容をファイルにコピ `com.adobe.idp.Document` ーします(メソッドによって返されたオブジェクトを使用 `com.adobe.idp.Document` していることを確 `getGeneratedDoc` 認します)。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[クイックスタート（EJBモード）:Java APIを使用してAEM Formsリポジトリ内のドキュメントをOutputサービスに渡す](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## フラグメントを使用したPDFドキュメントの作成 {#creating-pdf-documents-using-fragments}

OutputサービスとAssemblerサービスを使用して、フラグメントに基づくPDFドキュメントなどの出力ストリームを作成できます。 Assemblerサービスは、複数のXDPファイル内のフラグメントに基づいてXDPドキュメントをアセンブリします。 アセンブリ済みのXDPドキュメントがOutputサービスに渡され、OutputサービスがPDFドキュメントを作成します。 このワークフローは、生成中のPDFドキュメントを示しますが、Outputサービスは、このワークフロー用にZPLなどの他の出力タイプを生成できます。 PDFドキュメントは、ディスカッションの目的でのみ使用されます。

次の図に、このワークフローを示します。

![cp_cp_outputassemblefragments](assets/cp_cp_outputassemblefragments.png)

「フラグメ *ントを使用したPDFドキュメントの作成」を読む前に*、Assemblerサービスを使用して複数のXDPドキュメントをアセンブリする方法を理解することをお勧めします。 (複数のXDPフ [ラグメントのアセンブリを参照](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments))。

>[!NOTE]
>
>また、Assemblerサービスによってアセンブリされたフォームデザインを、Outputサービスの代わりにFormsサービスに渡すこともできます。 OutputサービスとFormsサービスの主な違いは、FormsサービスでインタラクティブPDFドキュメントが生成され、Outputサービスで非インタラクティブPDFドキュメントが生成される点です。 また、Formsサービスは、ZPLなどのプリンターベースの出力ストリームを生成できません。

>[!NOTE]
>
>For more information about the Output service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-4}

フラグメントに基づいてPDFドキュメントを作成するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. OutputおよびAssembler clientオブジェクトを作成します。
1. Assemblerサービスを使用してフォームデザインを生成します。
1. Outputサービスを使用してPDFドキュメントを生成します。
1. PDFドキュメントをPDFファイルとして保存します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

**OutputおよびAssembler clientオブジェクトの作成**

プログラムでOutputサービスAPI操作を実行する前に、Output Client APIオブジェクトを作成します。 また、このワークフローはAssemblerサービスを呼び出してフォームデザインを作成するので、Assembler Client APIオブジェクトを作成します。

**Assemblerサービスを使用したフォームデザインの生成**

Assemblerサービスを使用して、フラグメントを使用してフォームデザインを生成します。 Assemblerサービスは、フォームデザイン `com.adobe.idp.Document` を含むインスタンスを返します。

**Outputサービスを使用したPDFドキュメントの生成**

Outputサービスを使用して、Assemblerサービスが作成したフォームデザインを使用してPDFドキュメントを生成できます。 Assemblerサービス `com.adobe.idp.Document` が返したインスタンスをOutputサービスに渡します。

**PDFドキュメントをPDFファイルとして保存**

OutputサービスでPDFドキュメントを生成した後、PDFファイルとして保存できます。

**関連トピック**

[Java APIを使用したフラグメントに基づくPDFドキュメントの作成](creating-document-output-streams.md#create-a-pdf-document-based-on-fragments-using-the-java-api)

[WebサービスAPIを使用したフラグメントに基づくPDFドキュメントの作成](creating-document-output-streams.md#create-a-pdf-document-based-on-fragments-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[OutputサービスAPIのクイックスタート](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

[複数のXDPフラグメントのアセンブリ](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments)

[PDFドキュメントの作成](creating-document-output-streams.md#creating-pdf-documents)

### Java APIを使用したフラグメントに基づくPDFドキュメントの作成 {#create-a-pdf-document-based-on-fragments-using-the-java-api}

Output Service APIとAssembler Service API(Java)を使用して、フラグメントに基づいてPDFドキュメントを作成します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-output-client.jarなどのクライアントJARファイルを含めます。

1. OutputおよびAssembler clientオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `OutputClient` object by using its constructor and passing the `ServiceClientFactory` object.
   * Create an `AssemblerServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. Assemblerサービスを使用してフォームデザインを生成します。

   オブジェクト `AssemblerServiceClient` のメソッドを呼 `invokeDDX` び出し、次の必要な値を渡します。

   * 使用す `com.adobe.idp.Document` るDDXドキュメントを表すオブジェクトです。
   * 入力XDP `java.util.Map` ファイルを含むオブジェクトです。
   * デフォ `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` ルトフォントやジョブログレベルなど、実行時のオプションを指定するオブジェクトです。
   このメソ `invokeDDX` ッドは、アセンブリ `com.adobe.livecycle.assembler.client.AssemblerResult` されたXDPドキュメントを含むオブジェクトを返します。 アセンブリ済みのXDPドキュメントを取得するには、次のアクションを実行します。

   * オブジェクト `AssemblerResult` のメソッドを呼び出 `getDocuments` します。 このメソッドは、オブジェクトを `java.util.Map` 返します。
   * 結果のオブジェクト `java.util.Map` が見つかるまで、オブジェクトを繰り返 `com.adobe.idp.Document` します。
   * オブジェクト `com.adobe.idp.Document` のメソッドを呼び `copyToFile` 出して、アセンブリ済みのXDPドキュメントを抽出します。


1. Outputサービスを使用してPDFドキュメントを生成します。

   オブジェクト `OutputClient` のメソッドを `generatePDFOutput2` 呼び出し、次の値を渡します。

   * 列 `TransformationFormat` 挙値。 PDFドキュメントを生成するには、 `TransformationFormat.PDF`
   * 画像などの追加リソースが存在するコンテンツルートを指定するstring値です
   * フォーム `com.adobe.idp.Document` デザインを表すオブジェクト（Assemblerサービスから返されるインスタンスを使用）
   * PDF実行 `PDFOutputOptionsSpec` 時オプションを含むオブジェクト
   * レンダリ `RenderOptionsSpec` ングの実行時オプションを含むオブジェクト
   * フォー `com.adobe.idp.Document` ムデザインとマージするデータを含むXMLデータソースを含むオブジェクトです
   The `generatePDFOutput2` method returns an `OutputResult` object that contains the results of the operation

1. PDFドキュメントをPDFファイルとして保存します。

   * オブジェクト `com.adobe.idp.Document` のメソッドを呼び出して、PDFドキュメントを表すオブ `OutputResult` ジェクトを取得 `getGeneratedDoc` します。
   * 操作の結果 `java.io.File` を含むオブジェクトを作成します。 ファイル名の拡張子が.pdfであることを確認します。
   * Invoke the `com.adobe.idp.Document` object’s `copyToFile` method to copy the contents of the `com.adobe.idp.Document` object to the file. (メソッドが返すオブジェクト `com.adobe.idp.Document` を必ず使用し `getGeneratedDoc` てください)。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[クイックスタート（EJBモード）:Java APIを使用したフラグメントに基づくPDFドキュメントの作成](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[クイックスタート（SOAPモード）:Java APIを使用したフラグメントに基づくPDFドキュメントの作成](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

### WebサービスAPIを使用したフラグメントに基づくPDFドキュメントの作成 {#create-a-pdf-document-based-on-fragments-using-the-web-service-api}

Output Service APIとAssembler Service API（Webサービス）を使用して、フラグメントに基づいてPDFドキュメントを作成します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 Outputサービスに関連付けられているサービス参照に対して、次のWSDL定義を使用します。

   ```as3
    http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1.
   ```

   Assemblerサービスに関連付けられているサービス参照に対して、次のWSDL定義を使用します。

   ```as3
    http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   このデータ `BLOB` 型は両方のサービス参照に共通なので、使用する際にはデータ型 `BLOB` を完全に修飾してください。 対応するWebサービスのクイックスタートでは、すべてのインスタ `BLOB` ンスが完全修飾されています。

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. OutputおよびAssembler clientオブジェクトを作成します。

   * デフォルトのコンス `OutputServiceClient` トラクターを使用して、オブジェクトを作成します。
   * コンストラクタ `OutputServiceClient.Endpoint.Address` ーを使用してオブジェクトを作 `System.ServiceModel.EndpointAddress` 成します。 WSDLを指定するstring値をAEM Formsサービスに渡します(例 `http://localhost:8080/soap/services/OutputService?blob=mtom`:)。属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。 ただし、MTOMを使用す `?blob=mtom` るように指定します。
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `OutputServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当 `OutputServiceClient.ClientCredentials.UserName.UserName`てます。
      * 対応するパスワード値をフィールドに割り当 `OutputServiceClient.ClientCredentials.UserName.Password`てます。
      * 定数値をフィールドに `HttpClientCredentialType.Basic` 割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
   * 定数値をフ `BasicHttpSecurityMode.TransportCredentialOnly` ィールドに割り当 `BasicHttpBindingSecurity.Security.Mode`てます。
   >[!NOTE]
   >
   >オブジェクトに対してこの手順を繰り `AssemblerServiceClient`返します。

1. Assemblerサービスを使用してフォームデザインを生成します。

   オブジェクト `AssemblerServiceClient` のメソッドを `invokeDDX` 呼び出し、次の値を渡します。

   * DDXドキ `BLOB` ュメントを表すオブジェクト
   * 必要な `MyMapOf_xsd_string_To_xsd_anyType` ファイルを含むオブジェクトです
   * 実行時 `AssemblerOptionSpec` のオプションを指定するオブジェクト
   このメ `invokeDDX` ソッドは、ジョ `AssemblerResult` ブの結果と発生した例外を含むオブジェクトを返します。 新しく作成されたXDPドキュメントを取得するには、次の操作を実行します。

   * 結果のPDFドキ `AssemblerResult` ュメントを含むオ `documents` ブジェクトのフ `Map` ィールドにアクセスします。
   * オブジェクトを繰り返し `Map` 処理して、アセンブリされたフォームデザインを取得します。 配列メンバーをにキャス `value` トします `BLOB`。 このインスタンス `BLOB` をOutputサービスに渡します。


1. Outputサービスを使用してPDFドキュメントを生成します。

   オブジェクト `OutputServiceClient` のメソッドを `generatePDFOutput2` 呼び出し、次の値を渡します。

   * 列 `TransformationFormat` 挙値。 PDFドキュメントを生成するには、を指定しま `TransformationFormat.PDF`す。
   * 画像などの追加リソースが存在するコンテンツルートを指定するstring値。
   * フォーム `BLOB` デザインを表すオブジェクト(Assemblerサービスから返さ `BLOB` れるインスタンスを使用)。
   * PDF実行 `PDFOutputOptionsSpec` 時オプションを含むオブジェクトです。
   * レンダリ `RenderOptionsSpec` ングの実行時オプションを含むオブジェクトです。
   * フォー `BLOB` ムデザインとマージするデータを含むXMLデータソースを含むオブジェクトです。
   * メソッドが `BLOB` 入力する出力オ `generatePDFOutput2` ブジェクトです。 このメソッ `generatePDFOutput2` ドは、ドキュメントを記述する生成されたメタデータをこのオブジェクトに入力します。 （このパラメーター値はWebサービスの呼び出しにのみ必要です）。
   * 操作の結 `OutputResult` 果を含む出力オブジェクトです。 （このパラメーター値はWebサービスの呼び出しにのみ必要です）。
   このメソ `generatePDFOutput2` ッドは、非インタラ `BLOB` クティブPDFフォームを含むオブジェクトを返します。

1. PDFドキュメントをPDFファイルとして保存します。

   * Create a `System.IO.FileStream` object by invoking its constructor. インタラクティブPDFドキュメントのファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * メソッドから取得したオブジェクトの内容を格納す `BLOB` るバイト配列を作成 `generatePDFOutput2` します。 オブジェクトのデータメンバーの値を取得して、バ `BLOB` イト配列を `MTOM` 設定します。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡すことで、バ `System.IO.BinaryWriter` イト配列の内 `Write` 容をPDFファイルに書き込みます。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## ファイルへの印刷 {#printing-to-files}

Outputサービスを使用して、PostScript、Printer Control Language(PCL)、次のラベル形式などのストリームをファイルに出力できます。

* Zebra - ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

Outputサービスを使用すると、XMLデータをフォームデザインとマージし、フォームをファイルに印刷できます。 次の図に、Outputサービスでのレーザーファイルとラベルファイルの作成を示します。

>[!NOTE]
>
>プリントストリームのプリンターへの送信の詳細は、Sending Print Streams [to Printersを参照してください](creating-document-output-streams.md#sending-print-streams-to-printers)。

>[!NOTE]
>
>For more information about the Output service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-5}

ファイルに出力するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Output clientオブジェクトを作成します。
1. XMLデータソースを参照します。
1. ファイルへの印刷に必要な印刷実行時オプションを設定します。
1. 印刷ストリームをファイルに印刷します。
1. 操作の結果を取得します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar（AEM FormsがJBossにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsをJBossにデプロイする場合に必要）

aem formsがJBoss以外のサポート対象のJ2EEアプリケーションサーバーにデプロイされている場合は、adobe-utilities.jarファイルとjbossall-client.jarファイルを、AEM formsがデプロイされているJ2EEアプリケーションサーバーに固有のJARファイルに置き換える必要があります。 （[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照。）

**Output clientオブジェクトの作成**

プログラムでOutputサービス操作を実行する前に、Outputサービスクライアントオブジェクトを作成する必要があります。 Java APIを使用している場合は、オブジェクトを作成し `OutputClient` ます。 Output webサービスAPIを使用している場合は、オブジェクトを作成し `OutputServiceService` ます。

**XMLデータソースの参照**

データを含むドキュメントを印刷するには、データを入力するすべてのフォームフィールドに対して、XML要素を含むXMLデータソースを参照する必要があります。 XML要素名は、フィールド名と一致する必要があります。 XML要素がフォームフィールドに対応していない場合、またはXML要素名がフィールド名と一致しない場合、XML要素は無視されます。 すべてのXML要素を指定した場合、XML要素が表示される順序に一致する必要はありません。

**ファイルへの印刷に必要な印刷実行時オプションを設定する**

ファイルに出力するには、Outputサービスが印刷するファイルの場所と名前を指定して、「File URI run-time」オプションを設定する必要があります。 例えば、OutputサービスでMortgageForm.psという名前のPostScriptファイルを印刷するように指 *示するには* 、C:\Adobe\MortgageForm.psを指定します。

>[!NOTE]
>
>オプションで定義できる実行時オプションがあります。 設定できるすべてのオプションについて詳しくは、『 `PrintedOutputOptionsSpec` AEM Forms APIリファレンス』の「クラス [リファレンス」を参](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)照してください。

**印刷ストリームをファイルに出力**

フォームデータを含む有効なXMLデータソースを参照し、印刷の実行時オプションを設定した後、Outputサービスを呼び出すと、ファイルが印刷されます。

**操作の結果の取得**

Outputサービスは、操作の実行後、操作が成功したかどうかを示すXMLデータなどの様々なデータ項目を返します。

**関連トピック**

[Java APIを使用したファイルへの印刷](creating-document-output-streams.md#print-to-files-using-the-java-api)

[WebサービスAPIを使用したファイルへの印刷](creating-document-output-streams.md#print-to-files-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[OutputサービスAPIのクイックスタート](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Java APIを使用したファイルへの印刷 {#print-to-files-using-the-java-api}

Output API(Java)を使用してファイルに出力する：

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-output-client.jarなどのクライアントJARファイルを含めます。

1. Output clientオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `OutputClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. XMLデータソースを参照します。

   * コンストラ `java.io.FileInputStream` クターを使用し、XMLファイルの場所を指定するstring値を渡すことによって、ドキュメントの入力に使用されるXMLデータソースを表すオブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. ファイルへの印刷に必要な印刷実行時オプションを設定します。

   * コンストラクタを使用して `PrintedOutputOptionsSpec` オブジェクトを作成します。
   * PrintedOutputOptionsSpecオブジェクトのメソッドを呼び出し、フ `setFileURI` ァイルの名前と場所を表すstring値を渡して、ファイルを指定します。 例えば、OutputサービスでC:\AdobeにあるMortgageForm.psという名前のPostScriptファイルを印刷する場合は、C:\\Adobe\MortgageForm.psを指定します。
   * オブジェクトのメソッドを呼び出し、部 `PrintedOutputOptionsSpec` 数を表す整 `setCopies` 数値を渡して、印刷する部数を指定します。

1. 印刷ストリームをファイルに印刷します。

   オブジェクトのメソッドを呼び出し、次 `OutputClient` の値を渡 `generatePrintedOutput` して、ファイルに出力します。

   * 作成す `PrintFormat` る印刷ストリーム形式を指定する列挙値。 例えば、PostScript印刷ストリームを作成するには、を渡しま `PrintFormat.PostScript`す。
   * フォームデザイン名を指定する string 値。
   * 画像ファイルなど、関連するコラテラルファイルの場所を指定するstring値。
   * 使用するXDCファイルの場所を指定するstring値(オブジェクトを使用して使用するXDC `null` ファイルを指定した場合は、渡すことがで `PrintedOutputOptionsSpec` きます)。
   * ファイル `PrintedOutputOptionsSpec` への印刷に必要な実行時オプションを含むオブジェクトです。
   * フォーム `com.adobe.idp.Document` データを含むXMLデータソースを含むオブジェクトです。
   The `generatePrintedOutput` method returns an `OutputResult` object that contains the results of the operation.

   >[!NOTE]
   >
   >オブジ `OutputResult` ェクトのメソッドが `getRecordLevelMetaDataList` 返します `null`。

1. 操作の結果を取得します。

   * オブジェクト `com.adobe.idp.Document` のメソッドを呼び出して、メソッドのステータスを表すオブジェク `generatePrintedOutput` トを作成します(オ `OutputResult` ブジェクトはメソッドによって返 `getStatusDoc``OutputResult``generatePrintedOutput` されました)。
   * 操作の結 `java.io.File` 果を含むオブジェクトを作成します。 ファイル拡張子がXMLであることを確認します。
   * オブジェクト `com.adobe.idp.Document` のメソッドを呼び出 `copyToFile` して、オブジェクトの内容をファイルにコピ `com.adobe.idp.Document` ーします(メソッドによって返されたオブジェクトを使用 `com.adobe.idp.Document` していることを確 `getStatusDoc` 認します)。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[クイックスタート（SOAPモード）:Java APIを使用したファイルへの印刷](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-printing-to-a-file-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

### WebサービスAPIを使用したファイルへの印刷 {#print-to-files-using-the-web-service-api}

Output API（Webサービス）を使用してファイルに出力します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. Output clientオブジェクトを作成します。

   * デフォルトのコンス `OutputServiceClient` トラクターを使用して、オブジェクトを作成します。
   * コンストラクタ `OutputServiceClient.Endpoint.Address` ーを使用してオブジェクトを作 `System.ServiceModel.EndpointAddress` 成します。 WSDLを指定するstring値をAEM Formsサービスに渡します(例 `http://localhost:8080/soap/services/OutputService?blob=mtom`:)。属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。 ただし、MTOMを使用す `?blob=mtom` るように指定します。
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `OutputServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `OutputServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `OutputServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. XMLデータソースを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオブ `BLOB` ジェクトは、フォームデータの保存に使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、フォームデータを含むXMLファイルの場所を指定するstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイト配列、開 `System.IO.FileStream` 始位置、ストリ `Read` ーム長を渡すことによって、バイト配列にストリームデータを設定します。
   * オブジェクト `BLOB` にバイト配列の内容をプロ `binaryData` パティに割り当てて、オブジェクトを設定します。

1. ファイルへの印刷に必要な印刷実行時オプションを設定します。

   * コンストラクタを使用して `PrintedOutputOptionsSpec` オブジェクトを作成します。
   * ファイルの場所と名前を表すstring値をオブジェクトのデータメンバーに割り当てて、 `PrintedOutputOptionsSpec` ファイルを指 `fileURI` 定します。 例えば、OutputサービスでC:\AdobeにあるPostScriptファイル *MortgageForm.ps* を印刷する場合は、C:\\Adobe\MortgageForm.psを指定します。
   * 印刷する部数を指定するには、オブジェクトのデータメンバーに部数を表す整数値を `PrintedOutputOptionsSpec` 割り当て `copies` ます。

1. 印刷ストリームをファイルに印刷します。

   オブジェクトのメソッドを呼び出し、次 `OutputServiceService` の値を渡 `generatePrintedOutput` して、ファイルに出力します。

   * 作成す `PrintFormat` る印刷ストリーム形式を指定する列挙値。 例えば、PostScript印刷ストリームを作成するには、を渡しま `PrintFormat.PostScript`す。
   * フォームデザイン名を指定する string 値。
   * 画像ファイルなど、関連するコラテラルファイルの場所を指定するstring値。
   * 使用するXDCファイルの場所を指定するstring値(オブジェクトを使用して使用するXDC `null` ファイルを指定した場合は、渡すことがで `PrintedOutputOptionsSpec` きます)。
   * ファイル `PrintedOutputOptionsSpec` への印刷に必要な印刷実行時オプションを含むオブジェクトです。
   * フォーム `BLOB` データを含むXMLデータソースを含むオブジェクトです。
   * メソ `BLOB` ッドによって入力されるオブジェ `generatePDFOutput` クト。 このメソッ `generatePDFOutput` ドは、ドキュメントを記述する生成されたメタデータをこのオブジェクトに入力します。 （このパラメーター値は、Webサービスの呼び出しのみに必要です。）
   * メソ `BLOB` ッドによって入力されるオブジェ `generatePDFOutput` クト。 メソッド `generatePDFOutput` は、このオブジェクトに結果データを入力します。 （このパラメーター値は、Webサービスの呼び出しのみに必要です。）
   * 操作 `OutputResult` の結果を含むオブジェクトです。 （このパラメーター値は、Webサービスの呼び出しのみに必要です。）

1. 操作の結果を取得します。

   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、結果データを含むXMLファイルの場所を表すstring値を渡します。 ファイル拡張子がXMLであることを確認します。
   * オブジェクトのメソッド（8番目のパラメーター）によって結果デ `BLOB` ータが入力されたオブジェクトのデータコンテンツを格納 `OutputServiceService` するバ `generatePDFOutput` イト配列を作成します。 オブジェクトのデータメンバーの値を取得して、バ `BLOB` イト配列を `MTOM` 設定します。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡すことで、バイ `System.IO.BinaryWriter` ト配列の内 `Write` 容をXMLファイルに書き込みます。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## プリンターへの印刷ストリームの送信 {#sending-print-streams-to-printers}

Outputサービスを使用して、PostScript、Printer Control Language(PCL)、または次のラベル形式などの印刷ストリームをネットワークプリンターに送信できます。

* Zebra - ZPL
* Intermec - IPL
* Datamax - DPL
* TecToshiba - TPCL

Outputサービスを使用すると、XMLデータをフォームデザインとマージし、フォームを印刷ストリームとして出力できます。 例えば、PostScript印刷ストリームを作成して、ネットワークプリンターに送信できます。 次の図は、印刷ストリームをネットワークプリンターに送信するOutputサービスを示しています。

>[!NOTE]
>
>印刷ストリームをネットワークプリンターに送信する方法を示すために、この節では、SharedPrinterプリンタープロトコルを使用してPostScript印刷ストリームをネットワークプリンターに送信します。

>[!NOTE]
>
>For more information about the Output service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-6}

印刷ストリームをネットワークプリンターに送信するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Output clientオブジェクトを作成します。
1. XMLデータソースを参照します。
1. 印刷の実行時オプションの設定
1. 印刷するドキュメントを取得します。
1. ドキュメントをネットワークプリンターに送信します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar（AEM FormsがJBossにデプロイされている場合に必須）
* jbossall-client.jar（AEM FormsがJBossにデプロイされている場合は必須）

aem formsがJBoss以外のサポート対象のJ2EEアプリケーションサーバーにデプロイされている場合は、adobe-utilities.jarファイルとjbossall-client.jarファイルを、AEM formsがデプロイされているJ2EEアプリケーションサーバーに固有のJARファイルに置き換える必要があります。

**Output clientオブジェクトの作成**

プログラムでOutputサービス操作を実行する前に、Outputサービスクライアントオブジェクトを作成します。 Java APIを使用している場合は、オブジェクトを作成し `OutputClient` ます。 Output webサービスAPIを使用している場合は、オブジェクトを作成し `OutputServiceClient` ます。

**XMLデータソースの参照**

データを含むドキュメントを印刷するには、データを入力するすべてのフォームフィールドに対して、XML要素を含むXMLデータソースを参照する必要があります。 XML要素名は、フィールド名と一致する必要があります。 XML要素がフォームフィールドに対応していない場合、またはXML要素名がフィールド名と一致しない場合、XML要素は無視されます。 すべてのXML要素を指定した場合、XML要素が表示される順序に一致する必要はありません。

**印刷の実行時オプションの設定**

プリントストリームをプリンターに送信する際に、実行時のオプションを設定できます。次に例を示します。

* **コピー**:プリンターに送信する部数を指定します。 デフォルト値は 1 です。
* **Staple**:XCIオプションは、ステープル印刷が使用される場合に設定されます。 このオプションは、設定モデルでstaple要素によって指定でき、PSプリンターとPCLプリンターにのみ使用されます。
* **OutputJog**:XCIオプションは、出力ページをジョグ（出力トレイで物理的に移動）する必要がある場合に設定されます。 このオプションはPSプリンターとPCLプリンターのみに適用されます。
* **OutputBin**:プリントドライバーが適切な出力binを選択できるようにするために使用されるXCI値です。

>[!NOTE]
>
>設定可能なすべての実行時オプションについて詳しくは、クラス参照を参照し `PrintedOutputOptionsSpec` てください。

**印刷するドキュメントの取得**

プリンターに送信する印刷ストリームを取得します。 例えば、PostScriptファイルを取得してプリンターに送信できます。

プリンターでPDFがサポートされている場合は、PDFファイルを送信するように選択できます。 ただし、PDFドキュメントをプリンターに送信する際の問題は、プリンターの製造元ごとにPDFインタープリターの実装が異なる点です。 つまり、一部の印刷メーカーはAdobe PDFの解釈を使用しますが、プリンターによって異なります。 他のプリンターには、独自のPDFインタープリターがあります。 その結果、印刷結果は異なる場合があります。

PDFドキュメントをプリンターに送信するもう1つの制限は、単に印刷されるだけです。両面印刷、用紙トレイの選択、ホチキス止めにはアクセスできません。ただし、プリンターの設定が必要です。

印刷するドキュメントを取得するには、このメソッドを使用 `generatePrintedOutput` します。 次の表に、このメソッドを使用する場合に特定の印刷ストリームに対して設定されるコンテンツタイプを示 `generatePrintedOutput` します。

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
   <td><p>DPL300DPI </p></td>
   <td><p>DPL 300 DPI出力ストリームを作成します。</p></td>
  </tr>
  <tr>
   <td><p>DPL406DPI </p></td>
   <td><p>DPL 400 DPI出力ストリームを作成します。</p></td>
  </tr>
  <tr>
   <td><p>DPL600DPI </p></td>
   <td><p>DPL 600 DPI出力ストリームを作成します。</p></td>
  </tr>
  <tr>
   <td><p>GenericColorPCL </p></td>
   <td><p>汎用カラーPCL(5c)出力ストリームを作成します。</p></td>
  </tr>
  <tr>
   <td><p>GenericPSLevel3 </p></td>
   <td><p>汎用PostScript Level 3出力ストリームを作成します。</p></td>
  </tr>
  <tr>
   <td><p>IPL </p></td>
   <td><p>カスタムIPL出力ストリームを作成します。</p></td>
  </tr>
  <tr>
   <td><p>IPL300DPI </p></td>
   <td><p>IPL 300 DPI出力ストリームを作成します。</p></td>
  </tr>
  <tr>
   <td><p>IPL400DPI </p></td>
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
   <td><p>TPCL305DPI </p></td>
   <td><p>TPCL 305 DPI出力ストリームを作成します。</p></td>
  </tr>
  <tr>
   <td><p>TPCL600DPI </p></td>
   <td><p>TPCL 600 DPI出力ストリームを作成します。</p></td>
  </tr>
  <tr>
   <td><p>ZPL </p></td>
   <td><p>ZPL 203 DPI出力ストリームを作成します。</p></td>
  </tr>
  <tr>
   <td><p>ZPL300DPI </p></td>
   <td><p>ZPL 300 DPI出力ストリームを作成します。</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>この方法を使用して、印刷ストリームをプリンターに送信することもで `generatePrintedOutput2` きます。 ただし、「プリントストリームをプリンターに送信」セクションに関連するクイックスタートでは、この方法を使 `generatePrintedOutput` 用します。

**印刷ストリームをネットワークプリンターに送信します**

印刷するドキュメントを取得した後、Outputサービスを呼び出すと、印刷ストリームがネットワークプリンターに送信されます。 Outputサービスでプリンターを正常に見つけるには、プリントサーバーとプリンター名の両方を指定する必要があります。 また、印刷プロトコルも指定する必要があります。

>[!NOTE]
>
>PDFGがformsサーバーにインストールされ、サーバーがWindows Server 2008で実行されている場合は、SharedPrinterプロパティを使用できません。 この場合は、別のプリンタープロトコルを使用します。

>[!NOTE]
>
>ネットワークプリンタを使用し、アクセスメカニズムがSharedPrinterの場合は、プリンタの完全なネットワークパスを指定する必要があります。Java APIを使用して、印刷ストリームをネットワークプリンタに送信します。

Output API(Java)を使用して、印刷ストリームをネットワークプリンターに送信します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-output-client.jarなどのクライアントJARファイルを含めます。

1. Output clientオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `OutputClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. XMLデータソースの参照

   * コンストラ `java.io.FileInputStream` クターを使用し、XMLファイルの場所を指定するstring値を渡すことによって、ドキュメントの入力に使用されるXMLデータソースを表すオブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 印刷の実行時オプションの設定

   印刷の実行時オ `PrintedOutputOptionsSpec` プションを表すオブジェクトを作成します。 例えば、オブジェクトのメソッドを呼び出して、印刷する部数を `PrintedOutputOptionsSpec` 指定でき `setCopies` ます。

   >[!NOTE]
   >
   >ZPL印刷ストリームを生成する場合は、オブジェクトの `PrintedOutputOptionsSpec` メソッドを使 `setPagination` 用してページネーションの値を設定することはできません。 同様に、ZPL印刷ストリームに対して次のオプションを設定することはできません。OutputJog、PageOffsetおよびStaple。 このメ `setPagination` ソッドはPostScript生成に対して無効です。 PCL生成に対してのみ有効です。

1. 印刷するドキュメントの取得

   * オブジェクトのメソッドを呼び出し、次 `OutputClient` の値を渡して、 `generatePrintedOutput` 印刷するドキュメントを取得します。

      * 印刷 `PrintFormat` ストリームを指定する列挙値。 例えば、PostScript印刷ストリームを作成するには、を渡しま `PrintFormat.PostScript`す。
      * フォームデザイン名を指定する string 値。
      * 画像ファイルなど、関連するコラテラルファイルの場所を指定するstring値。
      * 使用するXDCファイルの場所を指定するstring値です。
      * ファイル `PrintedOutputOptionsSpec` に出力するために必要な実行時オプションを含むオブジェクトです。
      * フォーム `com.adobe.idp.Document` デザインとマージするフォームデータが含まれるXMLデータソースを表すオブジェクトです。
      This method returns an `OutputResult` object that contains the results of the operation.

   * オブジェクト `com.adobe.idp.Document` のメソッドを呼び出して、プリンターに送信するオ `OutputResult` ブジェクトを作成 `getGeneratedDoc` します。 このメソッドは、オブジェクトを `com.adobe.idp.Document` 返します。


1. 印刷ストリームをネットワークプリンターに送信します

   オブジェクトのメソッドを呼び出し、次の値を渡して、印刷ストリ `OutputClient` ームをネットワーク `sendToPrinter` プリンターに送信します。

   * プリ `com.adobe.idp.Document` ンターに送信する印刷ストリームを表すオブジェクトです。
   * 使用す `PrinterProtocol` るプリンタープロトコルを指定する列挙値。 例えば、SharedPrinterプロトコルを指定するには、を渡しま `PrinterProtocol.SharedPrinter`す。
   * プリントサーバーの名前を指定するstring値。 例えば、プリントサーバーの名前がPrintServer1であると仮定して、を渡しま `\\\PrintSever1`す。
   * プリンターの名前を指定するstring値。 例えば、プリンターの名前がPrinter1の場合は、を渡します `\\\PrintSever1\Printer1`。
   >[!NOTE]
   >
   >このメ `sendToPrinter` ソッドは、バージョン8.2.1のAEM Forms APIに追加されました。

### WebサービスAPIを使用したプリンターへの印刷ストリームの送信 {#send-a-print-stream-to-a-printer-using-the-web-service-api}

Output API（Webサービス）を使用して、印刷ストリームをネットワークプリンターに送信します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. Output clientオブジェクトを作成します。

   * デフォルトのコンス `OutputServiceClient` トラクターを使用して、オブジェクトを作成します。
   * コンストラクタ `OutputServiceClient.Endpoint.Address` ーを使用してオブジェクトを作 `System.ServiceModel.EndpointAddress` 成します。 WSDLを指定するstring値をAEM Formsサービスに渡します(例 `http://localhost:8080/soap/services/OutputService?blob=mtom`:)。属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。 ただし、MTOMを使用す `?blob=mtom` るように指定します。
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `OutputServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `OutputServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `OutputServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. XMLデータソースを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオブ `BLOB` ジェクトは、フォームデータの保存に使用されます。
   * Create a `System.IO.FileStream` object by invoking its constructor. フォームデータを含むXMLファイルの場所を指定するstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 オブジェクトのプロパティを取得して、バイト配列の長 `System.IO.FileStream` さを決定 `Length` します。
   * オブジェクトのメソッドを呼び出し、読み取るバイト配列、開 `System.IO.FileStream` 始位置、ストリ `Read` ーム長を渡すことによって、バイト配列にストリームデータを設定します。
   * オブジェクト `BLOB` にバイト配列の内容を `MTOM` フィールドに割り当てて、オブジェクトを入力します。

1. 印刷の実行時オプションを設定します。

   コンストラクタを使用して `PrintedOutputOptionsSpec` オブジェクトを作成します。例えば、印刷部数を指定するには、オブジェクトのデータメンバーに部数を表す整数値を割り当 `PrintedOutputOptionsSpec` てる必要が `copies` あります。

   >[!NOTE]
   >
   >ZPL印刷ストリームを生成する場合は、オブジェクトの `PrintedOutputOptionsSpec` データメンバ `pagination` ーを使用してページネーション値を設定することはできません。 同様に、ZPL印刷ストリームに対して次のオプションを設定することはできません。OutputJog、PageOffsetおよびStaple。 デー `pagination` タメンバはPostScript生成に対して無効です。 PCL生成に対してのみ有効です。

1. 印刷するドキュメントを取得します。

   * オブジェクトのメソッドを呼び出し、次 `OutputServiceService` の値を渡して、 `generatePrintedOutput` 印刷するドキュメントを取得します。

      * 印刷 `PrintFormat` ストリームを指定する列挙値。 例えば、PostScript印刷ストリームを作成するには、を渡しま `PrintFormat.PostScript`す。
      * フォームデザイン名を指定する string 値。
      * 画像ファイルなど、関連するコラテラルファイルの場所を指定するstring値。
      * 使用するXDCファイルの場所を指定するstring値です。
      * 印刷ス `PrintedOutputOptionsSpec` トリームをネットワークプリンターに送信する際に使用される印刷実行時オプションを含むオブジェクトです。
      * フォーム `BLOB` データを含むXMLデータソースを含むオブジェクトです。
      * メソ `BLOB` ッドによって入力されるオブジェ `generatePrintedOutput` クト。 このメソッ `generatePrintedOutput` ドは、ドキュメントを記述する生成されたメタデータをこのオブジェクトに入力します。 （このパラメーター値は、Webサービスの呼び出しのみに必要です。）
      * メソ `BLOB` ッドによって入力されるオブジェ `generatePrintedOutput` クト。 メソッド `generatePrintedOutput` は、このオブジェクトに結果データを入力します。 （このパラメーター値は、Webサービスの呼び出しのみに必要です。）
      * 操作 `OutputResult` の結果を含むオブジェクトです。 （このパラメーター値は、Webサービスの呼び出しのみに必要です。）
   * オブジェクト `BLOB` のメソッドの値を取得して、プリンターに送信するオブジェクト `OutputResult` を作成 `generatedDoc` します。 このメソッドは、メソッ `BLOB` ドによって返されるPostScriptデータを含むオブジェクトを返 `generatePrintedOutput` します。


1. 印刷ストリームをネットワークプリンターに送信します。

   オブジェクトのメソッドを呼び出し、次の値を渡して、印刷ストリ `OutputClient` ームをネットワーク `sendToPrinter` プリンターに送信します。

   * プリ `BLOB` ンターに送信する印刷ストリームを表すオブジェクトです。
   * 使用す `PrinterProtocol` るプリンタープロトコルを指定する列挙値。 例えば、SharedPrinterプロトコルを指定するには、を渡しま `PrinterProtocol.SharedPrinter`す。
   * 以前の `bool` パラメーター値を使用するかどうかを指定する値。 値を渡します `true`。 （このパラメーター値は、Webサービスの呼び出しのみに必要です。）
   * プリントサーバーの名前を指定するstring値。 例えば、プリントサーバーの名前がPrintServer1であると仮定して、を渡します `\\\PrintSever1`。
   * プリンターの名前を指定するstring値。 例えば、プリンターの名前がPrinter1である場合は、を渡します `\\\PrintSever1\Printer1`。
   >[!NOTE]
   >
   >このメ `sendToPrinter` ソッドは、バージョン8.2.1のAEM Forms APIに追加されました。

## 複数の出力ファイルの作成 {#creating-multiple-output-files}

Outputサービスでは、XMLデータソース内の各レコードに対して個別のドキュメントを作成することも、すべてのレコードを含む単一のファイルを作成することもできます（この機能はデフォルトです）。 例えば、10件のレコードがXMLデータソース内に配置され、OutputサービスでOutputサービスAPIを使用して各レコードに対して個別のPDFドキュメント（または他の種類の出力）を作成するように指示したとします。 その結果、Outputサービスは10個のPDFドキュメントを生成します。 （ドキュメントを作成する代わりに、複数の印刷ストリームをプリンターに送信できます）。

次の図は、複数のレコードを含むXMLデータファイルを処理するOutputサービスを示しています。 ただし、すべてのデータレコードを含む単一のPDFドキュメントを作成するようにOutputサービスに指示したとします。 この場合、Outputサービスは、すべてのレコードを含む1つのドキュメントを生成します。

次の図は、複数のレコードを含むXMLデータファイルを処理するOutputサービスを示しています。 Outputサービスに対して、各データレコードに対して個別のPDFドキュメントを作成するように指示したとします。 この場合、Outputサービスは、各データレコードに対して個別のPDFドキュメントを生成します。

![cm_outputbatchmany](assets/cm_outputbatchmany.png)

次のXMLデータは、3つのデータレコードを含むデータファイルの例を示しています。

```as3
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

各データレコードを開始および終了するXML要素は、です `LoanRecord`。 このXML要素は、複数のファイルを生成するアプリケーションロジックによって参照されます。

>[!NOTE]
>
>For more information about the Output service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-7}

XMLデータソースに基づいて複数のPDFファイルを作成するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Output clientオブジェクトを作成します。
1. XMLデータソースを参照します。
1. PDF実行時オプションを設定します。
1. レンダリングの実行時オプションを設定します。
1. 複数のPDFファイルを生成します。
1. 操作の結果を取得します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar（AEM FormsがJBossにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsをJBossにデプロイする場合に必要）

aem formsがJBoss以外のサポート対象のJ2EEアプリケーションサーバーにデプロイされている場合は、adobe-utilities.jarファイルとjbossall-client.jarファイルを、AEM formsがデプロイされているJ2EEアプリケーションサーバーに固有のJARファイルに置き換える必要があります。

**Output clientオブジェクトの作成**

プログラムでOutputサービス操作を実行する前に、Outputサービスクライアントオブジェクトを作成する必要があります。 Java APIを使用している場合は、オブジェクトを作成し `OutputClient` ます。 Output webサービスAPIを使用している場合は、オブジェクトを作成し `OutputServiceService` ます。

**XMLデータソースの参照**

複数のレコードを含むXMLデータソースを参照します。 XML要素を使用してデータレコードを分離する必要があります。 例えば、この節で前述したXMLデータソースの例では、データレコードを区切るXML要素に名前が付けられていま `LoanRecord`す。

データを入力するすべてのフォームフィールドにXML要素が存在する必要があります。 XML要素名は、フィールド名と一致する必要があります。 XML要素がフォームフィールドに対応していない場合、またはXML要素名がフィールド名と一致しない場合、XML要素は無視されます。 すべてのXML要素を指定した場合、XML要素が表示される順序に一致する必要はありません。

**PDF実行時オプションの設定**

XMLデータソースに基づいて複数のファイルを正常に作成するには、Outputサービスの次の実行時オプションを設定する必要があります。

* **多数のファイル**:Outputサービスで1つのドキュメントを作成するか、複数のドキュメントを作成するかを指定します。 trueまたはfalseを指定できます。 XMLデータソースの各データレコードに対して別々のドキュメントを作成する場合は、trueを指定します。
* **ファイルURI**:Outputサービスが生成するファイルの場所を指定します。 例えば、C:\\Adobe\forms\Loan.pdfと指定したとします。 この場合、OutputサービスはLoan.pdfという名前のファイルを作成し、そのファイルをC:\\Adobe\forms folderフォルダーに配置します。 複数のファイルがある場合、ファイル名はLoan0001.pdf、Loan0002.pdf、Loan0003.pdfのようになります。 ファイルの場所を指定した場合、ファイルはクライアントコンピューターではなくサーバーに配置されます。
* **レコード名**:データレコードを区切るデータソース内のXML要素名を指定します。 例えば、この節で前述したXMLデータソースの例では、データレコードを区切るXML要素が呼び出されます `LoanRecord`。 (「レコード名」実行時オプションを設定する代わりに、データレコードを含む要素レベルを示す数値をレコードレベルに割り当てることで、レコードレベルを設定できます。 ただし、「レコード名」または「レコードレベル」のみを設定できます。 両方の値を設定することはできません)。

**レンダリングの実行時オプションの設定**

レンダリングの実行時オプションは、複数のファイルの作成時に設定できます。 これらのオプションは必須ではありませんが（必須の出力実行時オプションとは異なり）、Outputサービスのパフォーマンスの向上などのタスクを実行できます。 例えば、Outputサービスで使用するフォームデザインをキャッシュして、パフォーマンスを向上させることができます。

Outputサービスは、バッチレコードを処理する際に、複数のレコードを含むデータを増分的に読み取ります。 つまり、Outputサービスはデータをメモリに読み込み、レコードのバッチが処理されるとデータを解放します。 2つの実行時オプションのいずれかが設定されている場合、Outputサービスはデータを増分的に読み込みます。 Record name実行時オプションを設定した場合、Outputサービスはデータを増分的に読み取ります。 同様に、「Record Level」実行時オプションを2以上に設定した場合、Outputサービスはデータを増分的に読み取ります。

Outputサービスでインクリメンタル読み込みを実行するかどうかは、またはオブジェクトの `PDFOutputOptionsSpec` メソッドを使 `PrintedOutputOptionSpec` 用して制御で `setLazyLoading` きます。 このメソッドに値を渡すと、イ `false` ンクリメンタル読み込みがオフになります。

**複数のPDFファイルの生成**

複数のデータレコードを含む有効なXMLデータソースを参照し、実行時のオプションを設定した後、Outputサービスを呼び出すと、複数のファイルが生成されます。 複数のレコードを生成する場合、オブ `OutputResult` ジェクトのメソッドは `getGeneratedDoc` を返しま `null`す。

**操作の結果の取得**

Outputサービスは、操作の実行後、操作が成功したかどうかを示すXMLデータを返します。 次のXMLがOutputサービスから返されます。 この場合、Outputサービスは42個のドキュメントを生成しました。

```as3
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

### Java APIを使用した複数のPDFファイルの作成 {#create-multiple-pdf-files-using-the-java-api}

Output API(Java)を使用して複数のPDFファイルを作成します。

1. プロジェクトファイルを含める&quot;

   Javaプロジェクトのクラスパスに、adobe-output-client.jarなどのクライアントJARファイルを含めます。.

1. Output clientオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `OutputClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. XMLデータソースの参照

   * コンストラク `java.io.FileInputStream` ターを使用し、XMLファイルの場所を指定する文字列値を渡すことで、複数のレコードを含むXMLデータソースを表すオブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PDF実行時オプションの設定

   * コンストラクタを使用して `PDFOutputOptionsSpec` オブジェクトを作成します。
   * オブジェクトのメソッドを呼び出して、「多数のファ `PDFOutputOptionsSpec` イル」オプションを設 `setGenerateManyFiles` 定します。 例えば、XMLデータソースの各 `true` レコードに対して別々のPDFファイルを作成するようにOutputサービスに指示する値を渡します。 (渡した場合、Outputサ `false`ービスはすべてのレコードを含む単一のPDFドキュメントを生成します)。
   * オブジェクトのメソッドを呼び出し、Outputサ `PDFOutputOptionsSpec` ービスが生成 `setFileUri` するファイルの場所を指定するstring値を渡して、「File URI」オプションを設定します。 「ファイルURI」オプションは、クライアントコンピューターではなく、AEM formsをホストするJ2EEアプリケーションサーバーに対する相対パスです。
   * オブジェクトのメソッドを呼び出し、デー `OutputOptionsSpec` タレコードを区切るデータソ `setRecordName` ース内のXML要素名を指定する文字列値を渡して、「レコード名」オプションを設定します。 (例えば、この節で前述したXMLデータソースについて考えてみましょう。 データレコードを区切るXML要素の名前はLoanRecordです。

1. レンダリングの実行時オプションの設定

   * コンストラクタを使用して `RenderOptionsSpec` オブジェクトを作成します。
   * オブジェクトを呼び出し、の値を渡すことで、Outputサービスのパフォーマンスを向上させるた `RenderOptionsSpec` めにフォームデザ `setCacheEnabled` インをキャッ `Boolean` シュしま `true`す。

1. 複数のPDFファイルの生成

   オブジェクトのメソッドを呼び出し、次 `OutputClient` の値を渡して、 `generatePDFOutput` 複数のPDFファイルを生成します。

   * 列 `TransformationFormat` 挙値。 PDFドキュメントを生成するには、を指定しま `TransformationFormat.PDF`す。
   * フォームデザイン名を指定する string 値。
   * フォームデザインが存在するコンテンツルートを指定するstring値。
   * PDF実行 `PDFOutputOptionsSpec` 時オプションを含むオブジェクトです。
   * レンダリ `RenderOptionsSpec` ングの実行時オプションを含むオブジェクトです。
   * フォー `com.adobe.idp.Document` ムデザインとマージするデータを含むXMLデータソースを含むオブジェクトです。
   The `generatePDFOutput` method returns an `OutputResult` object that contains the results of the operation.

1. 操作の結果の取得

   * メソッド `java.io.File` の結果を含むXMLファイルを表すオブジェクトを作成し `generatePDFOutput` ます。 ファイル名の拡張子が.xmlであることを確認します。
   * オブジェクト `com.adobe.idp.Document` のメソッドを呼び出 `copyToFile` して、オブジェクトの内容をファイルにコピ `com.adobe.idp.Document` ーします(メソッドによって返されたオブジェクトを使用 `com.adobe.idp.Document` していることを確 `applyUsageRights` 認します)。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[クイックスタート（EJBモード）:Java APIを使用した複数のPDFファイルの作成](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-multiple-pdf-files-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用した複数のPDFファイルの作成 {#create-multiple-pdf-files-using-the-web-service-api}

Output API（Webサービス）を使用して複数のPDFファイルを作成します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. Output clientオブジェクトを作成します。

   * デフォルトのコンス `OutputServiceClient` トラクターを使用して、オブジェクトを作成します。
   * コンストラクタ `OutputServiceClient.Endpoint.Address` ーを使用してオブジェクトを作 `System.ServiceModel.EndpointAddress` 成します。 WSDLを指定するstring値をAEM Formsサービスに渡します(例 `http://localhost:8080/soap/services/OutputService?blob=mtom`:)。属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。 ただし、MTOMを使用す `?blob=mtom` るように指定します。
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `OutputServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `OutputServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `OutputServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. XMLデータソースを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオブ `BLOB` ジェクトは、複数のレコードを含むフォームデータを保存するために使用されます。
   * Create a `System.IO.FileStream` object by invoking its constructor. 複数のレコードを含むXMLファイルのファイルの場所を表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイト配列、開 `System.IO.FileStream` 始位置、ストリ `Read` ーム長を渡すことによって、バイト配列にストリームデータを設定します。
   * オブジェクト `BLOB` にバイト配列の内容を `MTOM` フィールドに割り当てて、オブジェクトを入力します。

1. PDF実行時オプションを設定します。

   * コンストラクタを使用して `PDFOutputOptionsSpec` オブジェクトを作成します。
   * オブジェクトのデータメンバーにブール値を割り当てて、「多数のファイル」 `OutputOptionsSpec` オプションを `generateManyFiles` 設定します。 例えば、このデータメンバーに値を割 `true` り当てて、XMLデータソースの各レコードに対して個別のPDFファイルを作成するようOutputサービスに指示します。 (このデータメンバ `false` ーに割り当てると、Outputサービスはすべてのレコードを含む単一のPDFを生成します)。
   * ファイルURIオプションを設定するには、Outputサービスが生成するファイルの場所を指定するstring値をオブジェクトのデータメンバー `OutputOptionsSpec` に割り当 `fileURI` てます。 「ファイルURI」オプションは、クライアントコンピューターではなく、AEM formsをホストするJ2EEアプリケーションサーバーに対する相対パスです。
   * レコード名オプションを設定するには、データレコードをオブジェクトのデータメンバーに分けるデータソース内のXML要素名を指定するstring値 `OutputOptionsSpec` を割り当 `recordName` てます。
   * copiesオプションを設定するには、Outputサービスが生成するコピーの数を指定する整数値をオブジェクトのデータメ `OutputOptionsSpec` ンバーに割り `copies` 当てます。

1. レンダリングの実行時オプションを設定します。

   * コンストラクタを使用して `RenderOptionsSpec` オブジェクトを作成します。
   * フォームデザインをキャッシュして、オブジェクトのデータメンバーに値を割り当てることで、Outputサ `true` ービスのパフ `RenderOptionsSpec` ォーマンスを向 `cacheEnabled` 上させます。

1. 複数のPDFファイルを生成します。

   オブジェクトのメソッドを呼び出し、次 `OutputServiceService` の値を渡して、 `generatePDFOutput`複数のPDFファイルを作成します。

   * TransformationFormat列挙値。 PDFドキュメントを生成するには、を指定しま `TransformationFormat.PDF`す。
   * フォームデザイン名を指定する string 値。
   * フォームデザインが存在するコンテンツルートを指定するstring値。
   * PDF実行 `PDFOutputOptionsSpec` 時オプションを含むオブジェクトです。
   * レンダリ `RenderOptionsSpec` ングの実行時オプションを含むオブジェクトです。
   * フォー `BLOB` ムデザインとマージするデータを含むXMLデータソースを含むオブジェクトです。
   * メソ `BLOB` ッドによって入力されるオブジェ `generatePDFOutput` クト。 このメソッ `generatePDFOutput` ドは、ドキュメントを記述する生成されたメタデータをこのオブジェクトに入力します。
   * メソ `BLOB` ッドによって入力されるオブジェ `generatePDFOutput` クト。 メソッド `generatePDFOutput` は、このオブジェクトに結果データを入力します。
   * 操作 `OutputResult` の結果を含むオブジェクトです。

1. 操作の結果の取得

   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、結果データを含むXMLファイルの場所を表すstring値を渡します。 ファイル名の拡張子が.xmlであることを確認します。
   * オブジェクトのメソッド（8番目のパラメーター）によって結果デ `BLOB` ータが入力されたオブジェクトのデータコンテンツを格納 `OutputServiceService` するバ `generatePDFOutput` イト配列を作成します。 オブジェクトのデータメンバーの値を取得して、バ `BLOB` イト配列を `binaryData` 設定します。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡すことで、バイ `System.IO.BinaryWriter` ト配列の内 `Write` 容をXMLファイルに書き込みます。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 検索ルールの作成 {#creating-search-rules}

入力データを調べ、データコンテンツに基づいて様々なフォームデザインを使用して出力を生成するOutputサービスの結果となる検索ルールを作成できます。 例えば、テキストmortgageが入 *力データ内に* 配置されている場合、OutputサービスはMortgage.xdpという名前のフォームデザインを使用できます。 同様に、テキスト *automobile* が入力データ内にある場合、OutputサービスはAutomobileLoan.xdpとして保存されたフォームデザインを使用できます。 Outputサービスでは様々な出力タイプを生成できますが、この節では、OutputサービスでPDFファイルが生成されることを前提としています。 次の図に、XMLデータファイルを処理し、多数のフォームデザインの1つを使用してPDFファイルを生成するOutputサービスを示します。

さらに、Outputサービスはドキュメントパッケージを生成でき、データセットに複数のレコードが提供され、各レコードがフォームデザインと一致し、1つのドキュメントが複数のフォームデザインで構成されます。

![cs_outputbatchmanyformdesigns2](assets/cs_outputbatchmanyformdesigns2.png)

>[!NOTE]
>
>For more information about the Output service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-8}

ドキュメントの生成時に検索ルールを使用するようにOutputサービスに指示するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Output clientオブジェクトを作成します。
1. XMLデータソースを参照します。
1. 検索ルールを定義します。
1. PDF実行時オプションを設定します。
1. レンダリングの実行時オプションを設定します。
1. PDFドキュメントを生成します。
1. 操作の結果を取得します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar（AEM FormsがJBossにデプロイされている場合に必須）
* jbossall-client.jar（AEM FormsがJBossにデプロイされている場合は必須）

aem formsがJBoss以外のサポート対象のJ2EEアプリケーションサーバーにデプロイされている場合は、adobe-utilities.jarおよびjbossall-client.jarを、AEM formsがデプロイされているJ2EEアプリケーションサーバーに固有のJARファイルに置き換える必要があります。

**Output clientオブジェクトの作成**

プログラムでOutputサービス操作を実行する前に、Outputサービスクライアントオブジェクトを作成する必要があります。

**XMLデータソースの参照**

データを入力するすべてのフォームフィールドにXML要素が存在する必要があります。 XML要素名は、フィールド名と一致する必要があります。 XML要素がフォームフィールドに対応していない場合、またはXML要素名がフィールド名と一致しない場合、XML要素は無視されます。 すべてのXML要素が指定されている限り、XML要素が表示される順序に一致する必要はありません。

**検索ルールの定義**

検索ルールを定義するには、Outputサービスが入力データ内で検索する1つ以上のテキストパターンを定義します。 定義する各テキストパターンに対して、テキストパターンが存在する場合に使用する対応するフォームデザインを指定します。 テキストパターンが見つかった場合、Outputサービスは対応するフォームデザインを使用して出力を生成します。 テキストパターンの例としては、住宅ローンがあ *ります*。

>[!NOTE]
>
>テキストパターンが見つからない場合は、デフォルトのフォームが使用されます。 使用するすべてのフォームデザインがコンテンツルート内にあることを確認します。

**PDF実行時オプションの設定**

Outputサービスが複数のフォームデザインに基づいてPDFドキュメントを正常に作成できるように、次のPDF実行時オプションを設定します。

* **ファイルURI**:Outputサービスが生成するPDFファイルの名前と場所を指定します。
* **ルール**:定義したルールを指定します。
* **LookAHead**:定義済みのテキストパターンをスキャンするために入力データファイルの先頭から使用するバイト数を指定します。 デフォルトは500バイトです。

**レンダリングの実行時オプションの設定**

レンダリングの実行時オプションは、PDFファイルの作成時に設定できます。 これらのオプションは必須ではありませんが（PDFランタイムオプションとは異なり）、Outputサービスのパフォーマンス向上などのタスクを実行できます。 例えば、Outputサービスで使用するフォームデザインをキャッシュして、パフォーマンスを向上させることができます。

**PDFドキュメントの生成**

有効なXMLデータソースを参照し、実行時のオプションを設定した後、Outputサービスを呼び出してPDFドキュメントを生成できます。 Outputサービスは、入力データ内で指定されたテキストパターンを見つけた場合、対応するフォームデザインを使用します。 テキストパターンを使用しない場合、Outputサービスはデフォルトのフォームデザインを使用します。

**操作の結果の取得**

Outputサービスは、操作の実行後、操作が成功したかどうかを示すXMLデータを返します。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[OutputサービスAPIのクイックスタート](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Java APIを使用した検索ルールの作成 {#create-search-rules-using-the-java-api}

Output API(Java)を使用して検索ルールを作成します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-output-client.jarなどのクライアントJARファイルを含めます。

1. Output clientオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `OutputClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. XMLデータソースを参照します。

   * PDFドキュメ `java.io.FileInputStream` ントのコンストラクターを使用し、XMLファイルの場所を指定するstring値を渡すことによって、PDFドキュメントの入力に使用されるXMLデータソースを表すオブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 検索ルールを定義します。

   * コンストラクタを使用して `Rule` オブジェクトを作成します。
   * オブジェクトのメソッドを呼び出し、テ `Rule` キストパターン `setPattern` を指定する文字列値を渡して、テキストパターンを定義します。
   * オブジェクトのメソッドを呼び出して、対応するフォ `Rule` ームデザインを定義 `setForm` します。 フォームデザインの名前を指定するstring値を渡します。
   >[!NOTE]
   >
   >定義するテキストパターンごとに、前の3つのサブステップを繰り返します。

   * Create a `java.util.List` object by using an `java.util.ArrayList` constructor.
   * 作成したオ `Rule` ブジェクトごとに、オブジェクトのメ `java.util.List` ソッドを呼び `add` 出し、オブジェクトを渡 `Rule` します。


1. PDF実行時オプションを設定します。

   * コンストラクタを使用して `PDFOutputOptionsSpec` オブジェクトを作成します。
   * オブジェクトのメソッドを呼び出して、Outputサービスが生成するPDFファイルの名前と場 `PDFOutputOptionsSpec` 所を指定し `setFileURI` ます。 PDFファイルの場所を指定するstring値を渡します。 「ファイルURI」オプションは、クライアントコンピューターではなく、AEM formsをホストするJ2EEアプリケーションサーバーに対する相対パスです。
   * オブジェクトのメソッドを呼び出して、定義し `PDFOutputOptionsSpec` たルールを設定 `setRules` します。 オブジェクト `java.util.List` を含むオブジェクトを渡 `Rule` します。
   * オブジェクトのメソッドを呼び出して、定義済みのテキストパターンをスキャンするバ `PDFOutputOptionsSpec` イト数を設定 `setLookAhead` します。 バイト数を表す整数値を渡します。

1. レンダリングの実行時オプションを設定します。

   * コンストラクタを使用して `RenderOptionsSpec` オブジェクトを作成します。
   * オブジェクトを呼び出して渡すことでOutputサービスのパフォーマンスを向上させるために、フォームデザイン `RenderOptionsSpec` をキャッシュ `setCacheEnabled` してくださ `true`い。

1. PDFドキュメントを生成します。

   オブジェクトのメソッドを呼び出し、次の値を渡すことで、複数のフォームデザ `OutputClient` インに基づくPDFドキ `generatePDFOutput` ュメントを生成します。

   * 列 `TransformationFormat` 挙値。 PDFドキュメントを生成するには、を指定しま `TransformationFormat.PDF`す。
   * デフォルトのフォームデザインの名前を指定するstring値。 つまり、テキストパターンが見つからない場合に使用されるフォームデザインです。
   * フォームデザインが配置されるコンテンツルートを指定するstring値。
   * PDF実行 `PDFOutputOptionsSpec` 時オプションを含むオブジェクトです。
   * レンダリ `RenderOptionsSpec` ングの実行時オプションを含むオブジェクトです。
   * 定義さ `com.adobe.idp.Document` れたテキストパターンについてOutputサービスで検索されるフォームデータを含むオブジェクトです。
   The `generatePDFOutput` method returns an `OutputResult` object that contains the results of the operation.

1. 操作の結果を取得します。

   * オブジェクト `com.adobe.idp.Document` のメソッドを呼び出して、メソッドのステ `generatePDFOutput` ータスを表すオ `OutputResult` ブジェクトを作成 `getStatusDoc` します。
   * 操作の結 `java.io.File` 果を含むオブジェクトを作成します。 ファイル拡張子が.xmlであることを確認します。
   * オブジェクト `com.adobe.idp.Document` のメソッドを呼び出 `copyToFile` して、オブジェクトの内容をファイルにコピ `com.adobe.idp.Document` ーします(メソッドによって返されたオブジェクトを使用 `com.adobe.idp.Document` していることを確 `getStatusDoc` 認します)。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[クイックスタート（EJBモード）:Java APIを使用した検索ルールの作成](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[クイックスタート（SOAPモード）:Java APIを使用した検索ルールの作成](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-search-rules-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用した検索ルールの作成 {#create-search-rules-using-the-web-service-api}

Output API（Webサービス）を使用して検索ルールを作成します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. Output clientオブジェクトを作成します。

   * デフォルトのコンス `OutputServiceClient` トラクターを使用して、オブジェクトを作成します。
   * コンストラクタ `OutputServiceClient.Endpoint.Address` ーを使用してオブジェクトを作 `System.ServiceModel.EndpointAddress` 成します。 WSDLを指定するstring値をAEM Formsサービスに渡します(例 `http://localhost:8080/soap/services/OutputService?blob=mtom`:)。属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。 ただし、MTOMを使用す `?blob=mtom` るように指定します。
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `OutputServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `OutputServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `OutputServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. XMLデータソースを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、PDFドキュメントとマージされるデータの保存に使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、暗号化するPDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイト配列、開 `System.IO.FileStream` 始位置、ストリ `Read` ーム長を渡すことによって、バイト配列にストリームデータを設定します。
   * オブジェクト `BLOB` にバイト配列の内容を `MTOM` フィールドに割り当てて、オブジェクトを入力します。

1. 検索ルールを定義します。

   * コンストラクタを使用して `Rule` オブジェクトを作成します。
   * テキストパターンを定義するには、オブジェクトのデータメンバーにテキストパターンを指定する `Rule` 文字列値を `pattern` 割り当てます。
   * オブジェクトのデータメンバーにフォームデザインを指定する文字列値を割り当てて、対応するフォ `Rule` ームデザインを `form` 定義します。
   >[!NOTE]
   >
   >定義するテキストパターンごとに、前の3つのサブステップを繰り返します。

   * ルールを保存 `MyArrayOf_xsd_anyType` するオブジェクトを作成します。
   * 各オブジェクト `Rule` を配列の要素に割り当て `MyArrayOf_xsd_anyType` ます。 各オブジェクト `MyArrayOf_xsd_anyType` に対してオブジェ `Add` クトのメソッドを呼び出 `Rule` します。


1. PDF実行時オプションの設定

   * コンストラクタを使用して `PDFOutputOptionsSpec` オブジェクトを作成します。
   * ファイルURIオプションを設定するには、Outputサービスが生成するPDFファイルの場所を指定するstring値をオブジェクトのデータメンバ `PDFOutputOptionsSpec` ーに割り当 `fileURI` てます。 「ファイルURI」オプションは、クライアントコンピューターではなく、AEM formsをホストするJ2EEアプリケーションサーバーに対する相対パスです。
   * copiesオプションを設定するには、Outputサービスが生成するコピーの数を指定する整数値をオブジェクトのデータメ `PDFOutputOptionsSpec` ンバーに割り `copies` 当てます。
   * 定義したルールを設定するには、ルールを保存するオ `MyArrayOf_xsd_anyType` ブジェクトをオブジェクトのデータメ `PDFOutputOptionsSpec` ンバーに割り `rules` 当てます。
   * 定義済みのテキストパターンをスキャンするバイト数を設定するには、スキャンするバイト数を表す整数値をオブジェクトのデータメソッド `PDFOutputOptionsSpec` に割り当 `lookAhead` てます。

1. レンダリングの実行時オプションの設定

   * コンストラクタを使用して `RenderOptionsSpec` オブジェクトを作成します。
   * オブジェクトのデータメンバーに値を割り当てて、Outputサービスのパフォーマンスを向上させるために、フ `true` ォームデザイン `RenderOptionsSpec` をキャッ `cacheEnabled` シュします。
   >[!NOTE]
   >
   >入力ドキュメントがAcrobatフォームの場合、オブジェクトのメンバ `RenderOptionsSpec` ーを使用してPDFドキ `pdfVersion` ュメントのバージョンを設定することはできません。 出力PDFドキュメントは、AcrobatフォームのPDFバージョンを保持します。 同様に、入力ドキュメントがAcrobatフォームの場合は、オブジェクトの方 `RenderOptionsSpec` 法を使用してタグ付 `taggedPDF` きPDFオプションを設定することはできません。

   >[!NOTE]
   >
   >入力PDFドキュメントが認証済みまたはデジタル署名済みの場合、オブ `RenderOptionsSpec` ジェクトのメ `linearizedPDF` ンバーを使用して線形化されたPDFオプションを設定することはできません。 詳しくは、「PDFドキュメントへ [の電子署名」を参照してくださ](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)い。

1. PDFドキュメントの生成

   Create a PDF document by invoking the `OutputServiceService` object’s `generatePDFOutput`method and passing the following values:

   * 列 `TransformationFormat` 挙値。 PDFドキュメントを生成するには、を指定しま `TransformationFormat.PDF`す。
   * フォームデザイン名を指定する string 値。
   * フォームデザインが存在するコンテンツルートを指定するstring値。
   * PDF実行 `PDFOutputOptionsSpec` 時オプションを含むオブジェクトです。
   * レンダリ `RenderOptionsSpec` ングの実行時オプションを含むオブジェクトです。
   * フォー `BLOB` ムデザインとマージするデータを含むXMLデータソースを含むオブジェクトです。
   * メソ `BLOB` ッドによって入力されるオブジェ `generatePDFOutput` クト。 このメソッ `generatePDFOutput` ドは、ドキュメントを記述する生成されたメタデータをこのオブジェクトに入力します。 （このパラメーター値はWebサービスの呼び出しにのみ必要です）。
   * メソ `BLOB` ッドによって入力されるオブジェ `generatePDFOutput` クト。 メソッド `generatePDFOutput` は、このオブジェクトに結果データを入力します。 （このパラメーター値はWebサービスの呼び出しにのみ必要です）。
   * 操作 `OutputResult` の結果を含むオブジェクトです。 （このパラメーター値はWebサービスの呼び出しにのみ必要です）。
   >[!NOTE]
   >
   >このメソッドを呼び出してPDFドキュメントを生成する場合は、署名済み、認証済み、または使用権限を含むXFA PDFフォームとデータをマージできないことに注意してください。 `generatePDFOutput` 使用権限について詳しくは、「PDFドキュメントへ [の使用権限の適用」を参照してください](/help/forms/developing/assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)。

1. 操作の結果の取得

   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、結果データを含むXMLファイルの場所を表すstring値を渡します。 ファイル拡張子がXMLであることを確認します。
   * オブジェクトのメソッド（8番目のパラメーター）によって結果デ `BLOB` ータが入力されたオブジェクトのデータコンテンツを格納 `OutputServiceService` するバ `generatePDFOutput` イト配列を作成します。 オブジェクトのデータメンバーの値を取得して、バ `BLOB` イト配列を `MTOM` 設定します。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡すことで、バイ `System.IO.BinaryWriter` ト配列の内 `Write` 容をXMLファイルに書き込みます。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## PDFドキュメントの統合 {#flattening-pdf-documents}

Outputサービスを使用して、インタラクティブPDFドキュメントを非インタラクティブPDFに変換できます。 インタラクティブPDFドキュメントを使用すると、ユーザーはPDFドキュメントフィールド内のデータを入力または変更できます。 The process of transforming an interactive PDF document to a non-interactive PDF document is called *flattening*. PDFドキュメントを統合すると、ユーザーはドキュメントフィールド内のデータを変更できません。 PDF ドキュメントを統合する理由の 1 つは、データを変更できないようにすることです。

次の種類のPDFドキュメントを統合できます。

* インタラクティブXFA PDFドキュメント
* Acrobat Forms

非インタラクティブPDFドキュメントであるPDFを統合しようとすると、例外が発生します。

>[!NOTE]
>
>For more information about the Output service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-9}

インタラクティブPDFドキュメントを非インタラクティブPDFドキュメントに統合するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Output clientオブジェクトを作成します。
1. インタラクティブPDFドキュメントを取得します。
1. PDFドキュメントを変換します。
1. 非インタラクティブPDFドキュメントをPDFファイルとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-output-client.jar
* adobe-utilities.jar（AEM FormsがJBossにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsをJBossにデプロイする場合に必要）

aem formsがJBoss以外のサポート対象のJ2EEアプリケーションサーバーにデプロイされている場合は、adobe-utilities.jarファイルとjbossall-client.jarファイルを、AEM formsがデプロイされているJ2EEアプリケーションサーバーに固有のJARファイルに置き換える必要があります。 For information about the location of all AEM Forms JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Output clientオブジェクトの作成**

プログラムでOutputサービス操作を実行する前に、Outputサービスクライアントオブジェクトを作成する必要があります。 Java APIを使用している場合は、オブジェクトを作成し `OutputClient` ます。 Output webサービスAPIを使用している場合は、オブジェクトを作成し `OutputServiceService` ます。

**インタラクティブPDFドキュメントの取得**

非インタラクティブPDFドキュメントに変換するインタラクティブPDFドキュメントを取得します。 非インタラクティブPDFドキュメントを変換しようとすると、例外が発生します。

**PDFドキュメントの変換**

インタラクティブPDFドキュメントを取得した後、非インタラクティブPDFドキュメントに変換できます。 Outputサービスは、非インタラクティブPDFドキュメントを返します。

**非インタラクティブPDFドキュメントをPDFファイルとして保存**

非インタラクティブPDFドキュメントをPDFファイルとして保存できます。

**関連トピック**

[Java APIを使用したPDFドキュメントの統合](creating-document-output-streams.md#flatten-a-pdf-document-using-the-java-api)

[WebサービスAPIを使用したPDFドキュメントの統合](creating-document-output-streams.md#flatten-a-pdf-document-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[OutputサービスAPIのクイックスタート](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Java APIを使用したPDFドキュメントの統合 {#flatten-a-pdf-document-using-the-java-api}

Output API(Java)を使用して、インタラクティブPDFドキュメントを非インタラクティブPDFドキュメントに統合します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-output-client.jarなどのクライアントJARファイルを含めます。

1. Output clientオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `OutputClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. インタラクティブPDFドキュメントを取得します。

   * コンストラクタ `java.io.FileInputStream` ーを使用し、インタラクティブPDFファイルの場所を指定するstring値を渡して、変換するインタラクティブPDFドキュメントを表すオブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PDFドキュメントを変換します。

   オブジェクトのメソッドを呼び出し、次の値を渡して、インタラクティブPDFドキュメ `OutputServiceService` ントを非インタラクティブPDF `transformPDF` ドキュメントに変換します。

   * インタラ `com.adobe.idp.Document` クティブPDFドキュメントを含むオブジェクトです。
   * 列 `TransformationFormat` 挙値。 非インタラクティブPDFドキュメントを生成するには、を指定しま `TransformationFormat.PDF`す。
   * A `PDFARevisionNumber` enum value that specifies the revision number. このパラメーターはPDF/Aドキュメント用なので、を指定できま `null`す。
   * 修正番号と年をコロンで区切って表すstring値です。 このパラメーターはPDF/Aドキュメント用なので、を指定できま `null`す。
   * PDF/ `PDFAConformance` A準拠レベルを表すenum値です。 このパラメーターはPDF/Aドキュメント用なので、を指定できま `null`す。
   このメソ `transformPDF` ッドは、非インタラ `com.adobe.idp.Document` クティブPDFドキュメントを含むオブジェクトを返します。

1. 非インタラクティブPDFドキュメントをPDFファイルとして保存します。

   * Create a `java.io.File` object and ensure that the file name extension is .pdf.
   * オブジェクト `Document` のメソッドを呼び出 `copyToFile` して、オブジェクトの内容をファイルにコピ `Document` ーします(メソッドによって返されたオブジェクトを使用 `Document` していることを確 `transformPDF` 認します)。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[クイックスタート（EJBモード）:Java APIを使用したPDFドキュメントの変換](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

[クイックスタート（SOAPモード）:Java APIを使用したPDFドキュメントの変換](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-transforming-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したPDFドキュメントの統合 {#flatten-a-pdf-document-using-the-web-service-api}

Output API（Webサービス）を使用して、インタラクティブPDFドキュメントを非インタラクティブPDFドキュメントに統合します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/OutputService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. Output clientオブジェクトを作成します。

   * デフォルトのコンス `OutputServiceClient` トラクターを使用して、オブジェクトを作成します。
   * コンストラクタ `OutputServiceClient.Endpoint.Address` ーを使用してオブジェクトを作 `System.ServiceModel.EndpointAddress` 成します。 WSDLを指定するstring値をAEM Formsサービスに渡します(例 `http://localhost:8080/soap/services/OutputService?blob=mtom`:)。属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。 ただし、MTOMを使用す `?blob=mtom` るように指定します。
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `OutputServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `OutputServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `OutputServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. インタラクティブPDFドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオブジ `BLOB` ェクトは、インタラクティブPDFドキュメントの保存に使用されます。
   * オブジェクトを `System.IO.FileStream` 作成するには、コンストラクターを呼び出し、インタラクティブPDFドキュメントのファイルの場所を表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイト配列、開 `System.IO.FileStream` 始位置、ストリ `Read` ーム長を渡すことによって、バイト配列にストリームデータを設定します。
   * オブジェクト `BLOB` にバイト配列の内容をプロ `MTOM` パティに割り当てて、オブジェクトを設定します。

1. PDFドキュメントを変換します。

   オブジェクトのメソッドを呼び出し、次の値を渡して、インタラクティブPDFドキュメ `OutputClient` ントを非インタラクティブPDF `transformPDF` ドキュメントに変換します。

   * インタラ `BLOB` クティブPDFドキュメントを含むオブジェクトです。
   * 列 `TransformationFormat` 挙値。 非インタラクティブPDFドキュメントを生成するには、を指定しま `TransformationFormat.PDF`す。
   * A `PDFARevisionNumber` enum value that specifies the revision number.
   * 列挙値を使用するかどうかを指 `PDFARevisionNumber` 定するBoolean値です。 このパラメーターはPDF/Aドキュメント用なので、を指定できま `false`す。
   * 修正番号と年をコロンで区切って表すstring値です。 このパラメーターはPDF/Aドキュメント用なので、を指定できま `null`す。
   * PDF/ `PDFAConformance` A準拠レベルを表すenum値です。
   * 列挙値が使用されるかど `PDFAConformance` うかを指定するブール値。 このパラメーターはPDF/Aドキュメント用なので、を指定できま `false`す。
   このメソ `transformPDF` ッドは、非インタラ `BLOB` クティブPDFドキュメントを含むオブジェクトを返します。

1. 非インタラクティブPDFドキュメントをPDFファイルとして保存します。

   * オブジェクトを `System.IO.FileStream` 作成するには、コンストラクターを呼び出し、非インタラクティブPDFドキュメントのファイルの場所を表すstring値を渡します。
   * メソッドによって返されたオブジェクトのデータ内容を格納 `BLOB` するバイト配列を作成 `transformPDF` します。 オブジェクトのデータメンバーの値を取得して、バ `BLOB` イト配列を `MTOM` 設定します。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡すことで、バ `System.IO.BinaryWriter` イト配列の内 `Write` 容をPDFファイルに書き込みます。

**関連トピック**

[手順の概要](creating-document-output-streams.md#summary-of-steps)

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
