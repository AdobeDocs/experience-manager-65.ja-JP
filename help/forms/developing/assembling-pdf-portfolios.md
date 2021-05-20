---
title: PDFPortfolioのアセンブリ
seo-title: PDFPortfolioのアセンブリ
description: PDFポートフォリオをアセンブリして、Wordファイル、画像ファイル、PDFドキュメントなど、様々なタイプの複数のドキュメントを組み合わせます。 Java APIとWebサービスAPIを使用して、PDFポートフォリオをアセンブリできます。
seo-description: PDFポートフォリオをアセンブリして、Wordファイル、画像ファイル、PDFドキュメントなど、様々なタイプの複数のドキュメントを組み合わせます。 Java APIとWebサービスAPIを使用して、PDFポートフォリオをアセンブリできます。
uuid: 1778c90b-9d26-466b-a7c7-401d737395e0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 023f0d9e-bfde-4879-a839-085fadffb48e
role: Developer
exl-id: d2bd7c3e-4f75-4234-a7aa-ee8524430493
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1865'
ht-degree: 3%

---

# PDFPortfolioのアセンブリ{#assembling-pdf-portfolios}

**このドキュメントのサンプルと例は、JEE上のAEM Forms環境に限られています。**

Assembler JavaおよびWebサービスAPIを使用してPDFPortfolioをアセンブリできます。 ポートフォリオは、wordファイル、画像ファイル（例えば、jpegファイル）、PDFドキュメントなど、様々なタイプの複数のドキュメントを組み合わせることができます。 ポートフォリオのレイアウトは、*プレビュー付きグリッド*、*画像上*、さらには&#x200B;*回転*&#x200B;など、異なるスタイルに設定できます。

次の図は、*画像*&#x200B;スタイルレイアウトのポートフォリオのスクリーンショットです。

![ap_ap_portfolio](assets/ap_ap_portfolio.png)

PDFPortfolioを作成すると、ドキュメントのコレクションを渡す代わりに、ペーパーレスで作成できます。 AEM Formsを使用して、構造化DDXドキュメントでAssemblerサービスを呼び出すことで、ポートフォリオを作成できます。 次のDDXドキュメントは、PDFドキュメントを作成するDDXドキュメントの例です。Portfolio

```xml
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     <PDF result="portfolio1.pdf">
         <Portfolio>
             <Navigator source="myNavigator">
                 <Resource name="navigator/image.xxx" source="myImage.png"/>
             </Navigator>
         </Portfolio>
         <PackageFiles source="dog1"  >
              <FieldData name="X">72</FieldData>
             <FieldData name="Y">72</FieldData>
             <File filename="saint_bernard.jpg" mimetype="image/jpeg"/>
         </PackageFiles>
         <PackageFiles source="dog2"  >
             <FieldData name="X">120</FieldData>
             <FieldData name="Y">216</FieldData>
             <File filename="greyhound.pdf"/>
         </PackageFiles>
     </PDF>
 </DDX>
```

DXXドキュメントには、入れ子になった`Navigator`タグを含む`Portfolio`タグが必要です。 タグ`<Resource name="navigator/image.xxx" source="myImage.png"/>`は、 `myNavigator`がonImageレイアウトナビゲーターとして割り当てられている場合にのみ必要です。`AdobeOnImage.nav`. このタグを使用すると、Assemblerサービスは、ポートフォリオの背景として使用する画像を選択できます。 `PackageFiles`タグと`File`タグを含めて、パッケージファイルのファイル名とMIMEタイプを定義します。

>[!NOTE]
>
>Assemblerサービスについて詳しくは、『AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)向けサービスリファレンス』を参照してください。[

>[!NOTE]
>
>DDXドキュメントについて詳しくは、『[AssemblerサービスとDDXリファレンス](https://www.adobe.com/go/learn_aemforms_ddx_63)』を参照してください。

## 手順の概要{#summary-of-steps}

PDFタスクを作成するには、次のPortfolioを実行します。

1. プロジェクトファイルを含めます。
1. PDFアセンブラークライアントを作成します。
1. 既存のDDXドキュメントの参照
1. 必要なドキュメントを参照します。
1. 実行時オプションを設定します。
1. ポートフォリオを組み立てます。
1. 組み立てたポートフォリオを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用する場合は、プロキシファイルを必ず含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(AEM FormsをJBossにデプロイする場合に必要)
* jbossall-client.jar(AEM FormsをJBossにデプロイする場合に必要)

**PDFアセンブラークライアントの作成**

プログラムでAssembler操作を実行する前に、Assemblerサービスクライアントを作成します。

**既存のDDXドキュメントの参照**

PDFドキュメントをアセンブリするには、DDXドキュメントを参照する必要があります。Portfolio このDDXドキュメントには、 `Portfolio`、 `Navigator`および`PackageFiles`の各要素が含まれている必要があります。

**必要なドキュメントの参照**

PDFアセンブリをアセンブリするには、Portfolioするドキュメントを表すすべてのファイルを参照します。 例えば、DDXドキュメントで指定されているすべての画像ファイルをAssemblerサービスに渡します。 これらのファイルは、この節で指定するDDXドキュメントで参照されています。*myImage.png*&#x200B;と&#x200B;*saint_bernard.jpg*

PDFPortfolioをアセンブリする際に、NAVファイル（ナビゲーターファイル）をAssemblerサービスに渡します。 Assemblerサービスに渡すNAVファイルは、作成するPDFPortfolioの種類に応じて異なります。 例えば、*画像*&#x200B;レイアウトを作成するには、AdobeOnImage.navファイルを渡します。 NAVファイルは、次のフォルダーにあります。

`<Install folder>\Acrobat 9.0\Acrobat\Navigators`

NAVファイルをAcrobat 9（またはそれ以降）のインストールディレクトリからコピーします。 NAVファイルを、クライアントアプリケーションがアクセスできる場所に配置します。 すべてのファイルは、Mapコレクションオブジェクト内でAssemblerサービスに渡されます。

>[!NOTE]
>
>PDFイメージのアセンブリに関連するクイックスタートでは、AdobeOnImage.navをPortfolioします。

**実行時オプションの設定**

ジョブの実行中にAssemblerサービスの動作を制御する実行時オプションを設定できます。 例えば、エラーが発生した場合にジョブの処理を続行するようAssemblerサービスに指示するオプションを設定できます。

**ポートフォリオの構成**

PDFPortfolioをアセンブリするには、`invokeDDX`操作を呼び出します。 Assemblerサービスは、コレクションオブジェクト内のPDFPortfolioを返します。

**組み立てたポートフォリオを保存**

PDFPortfolioがコレクションオブジェクト内で返されます。 コレクションオブジェクトを繰り返し処理し、PDFPortfolioをPDFファイルとして保存します。

**関連トピック**

[Java APIを使用したPDFPortfolioのアセンブリ](#assemble-a-pdf-portfolio-using-the-java-api)

[WebサービスAPIを使用したPDFPortfolioのアセンブリ](#assemble-a-pdf-portfolio-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDFドキュメントのプログラムによるアセンブリ](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java API {#assemble-a-pdf-portfolio-using-the-java-api}を使用したPDFPortfolioのアセンブリ

AssemblerサービスAPI(Java)を使用してPDFPortfolioをアセンブリします。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-assembler-client.jarなどのクライアントJARファイルを含めます。

1. PDFアセンブラークライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して`AssemblerServiceClient`オブジェクトを渡し、`ServiceClientFactory`オブジェクトを作成します。

1. 既存のDDXドキュメントの参照

   * コンストラクターを使用し、DDXファイルの場所を指定する文字列値を渡して、DDXドキュメントを表す`java.io.FileInputStream`オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 必要なドキュメントを参照します。

   * `HashMap`コンストラクターを使用して、入力PDFドキュメントの格納に使用する`java.util.Map`オブジェクトを作成します。
   * コンストラクタを使用して `java.io.FileInputStream` オブジェクトを作成します。必要なNAVファイルの場所を渡します（ポートフォリオの作成に必要な各ファイルに対して、このタスクを繰り返します）。
   * `com.adobe.idp.Document`オブジェクトを作成し、NAVファイルを含む`java.io.FileInputStream`オブジェクトを渡します（ポートフォリオの作成に必要な各ファイルに対して、このタスクを繰り返します）。
   * `put`メソッドを呼び出し、次の引数を渡して、`java.util.Map`オブジェクトにエントリを追加します。

      * キー名を表すstring値です。 この値は、DDXドキュメントで指定されたソース要素の値と一致する必要があります。 （ポートフォリオの作成に必要なファイルごとに、このタスクを繰り返します）。
      * PDFドキュメントを含む`com.adobe.idp.Document`オブジェクト。 （ポートフォリオの作成に必要なファイルごとに、このタスクを繰り返します）。

1. 実行時オプションを設定します。

   * コンストラクターを使用して、実行時オプションを格納する`AssemblerOptionSpec`オブジェクトを作成します。
   * `AssemblerOptionSpec`オブジェクトに属するメソッドを呼び出して、ビジネス要件に合った実行時オプションを設定します。 例えば、エラーが発生したときにジョブの処理を続行するようにAssemblerサービスに指示するには、`AssemblerOptionSpec`オブジェクトの`setFailOnError`メソッドを呼び出し、`false`を渡します。

1. ポートフォリオを組み立てます。

   `AssemblerServiceClient`オブジェクトの`invokeDDX`メソッドを呼び出し、次の必須値を渡します。

   * 使用するDDXドキュメントを表す`com.adobe.idp.Document`オブジェクト
   * PDFPortfolioの構築に必要なファイルを格納する`java.util.Map`オブジェクト。
   * デフォルトのフォントやジョブのログレベルを含む、ランタイムオプションを指定する`com.adobe.livecycle.assembler.client.AssemblerOptionSpec`オブジェクト

   `invokeDDX`メソッドは、アセンブリされたPDFPortfolioと発生した例外を含む`com.adobe.livecycle.assembler.client.AssemblerResult`オブジェクトを返します。

1. 組み立てたポートフォリオを保存します。

   PDFアクションを取得するには、次のPortfolioを実行します。

   * `AssemblerResult`オブジェクトの`getDocuments`メソッドを呼び出します。 このメソッドは`java.util.Map`オブジェクトを返します。
   * `java.util.Map`オブジェクトを繰り返し処理して、結果の`com.adobe.idp.Document`オブジェクトを見つけます。
   * `com.adobe.idp.Document`オブジェクトの`copyToFile`メソッドを呼び出して、PDFPortfolioを抽出します。

**関連トピック**

[クイックスタート（SOAPモード）:Java APIを使用したPDFPortfolioのアセンブリ](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-portfolios-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## WebサービスAPI {#assemble-a-pdf-portfolio-using-the-web-service-api}を使用したPDFPortfolioのアセンブリ

AssemblerサービスAPI（Webサービス）を使用してPDFPortfolioをアセンブリします。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 サービス参照を設定する際は、次のWSDL定義を使用してください。`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. PDFアセンブラークライアントを作成します。

   * デフォルトのコンストラクターを使用して`AssemblerServiceClient`オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`AssemblerServiceClient.Endpoint.Address`オブジェクトを作成します。 AEM FormsサービスにWSDLを指定するstring値を渡します（例：`http://localhost:8080/soap/services/AssemblerService?blob=mtom`）。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する際に使用されます。
   * `AssemblerServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値は、MTOMが使用されるようにします。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールド`AssemblerServiceClient.ClientCredentials.UserName.UserName`にAEM formsユーザー名を割り当てます。
      * 対応するパスワード値をフィールド`AssemblerServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * フィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に定数値`HttpClientCredentialType.Basic`を割り当てます。
      * フィールド`BasicHttpBindingSecurity.Security.Mode`に定数値`BasicHttpSecurityMode.TransportCredentialOnly`を割り当てます。

1. 既存のDDXドキュメントの参照

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、DDXドキュメントの格納に使用されます。
   * コンストラクターを呼び出し、DDXドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得することで、バイト配列のサイズを判断できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出して、バイト配列にストリームデータを入力します。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * `BLOB`オブジェクトの`MTOM`プロパティにバイト配列の内容を割り当てて、オブジェクトを設定します。

1. 必要なドキュメントを参照します。

   * 各入力ファイルに対して、コンストラクタを使用して`BLOB`オブジェクトを作成します。 `BLOB`オブジェクトは、入力ファイルの保存に使用されます。
   * コンストラクターを呼び出し、入力ファイルのファイルの場所とファイルを開くモードを表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得することで、バイト配列のサイズを判断できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出して、バイト配列にストリームデータを入力します。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * `BLOB`オブジェクトの`MTOM`フィールドにバイト配列の内容を割り当てて、オブジェクトを設定します。
   * `MyMapOf_xsd_string_To_xsd_anyType`オブジェクトを作成します。 このコレクションオブジェクトは、PDFコレクションの作成に必要な入力ファイルのPortfolioに使用されます。
   * 入力ファイルごとに、`MyMapOf_xsd_string_To_xsd_anyType_Item`オブジェクトを作成します。
   * `MyMapOf_xsd_string_To_xsd_anyType_Item`オブジェクトの`key`フィールドに、キー名を表すstring値を割り当てます。 この値は、DDXドキュメントで指定されたエレメントの値と一致する必要があります。 （入力ファイルごとにこのタスクを実行します）。
   * 入力ファイルを格納する`BLOB`オブジェクトを`MyMapOf_xsd_string_To_xsd_anyType_Item`オブジェクトの`value`フィールドに割り当てます。 （このタスクは、入力PDFドキュメントごとに実行します）。
   * `MyMapOf_xsd_string_To_xsd_anyType_Item`オブジェクトを`MyMapOf_xsd_string_To_xsd_anyType`オブジェクトに追加します。 `MyMapOf_xsd_string_To_xsd_anyType`オブジェクトの`Add`メソッドを呼び出して、`MyMapOf_xsd_string_To_xsd_anyType`オブジェクトを渡します。 （このタスクは、入力PDFドキュメントごとに実行します）。

1. 実行時オプションを設定します。

   * コンストラクターを使用して、実行時オプションを格納する`AssemblerOptionSpec`オブジェクトを作成します。
   * `AssemblerOptionSpec`オブジェクトに属するデータメンバーに値を割り当てて、ビジネス要件に合った実行時オプションを設定します。 例えば、エラーが発生したときにジョブの処理を続行するようにAssemblerサービスに指示するには、`false`を`AssemblerOptionSpec`オブジェクトの`failOnError`データメンバーに割り当てます。

1. ポートフォリオを組み立てます。

   `AssemblerServiceClient`オブジェクトの`invokeDDX`メソッドを呼び出し、次の値を渡します。

   * DDXドキュメントを表す`BLOB`オブジェクト
   * 必要なファイルを含む`MyMapOf_xsd_string_To_xsd_anyType`オブジェクト
   * 実行時オプションを指定する`AssemblerOptionSpec`オブジェクト

   `invokeDDX`メソッドは、ジョブの結果と発生した例外を含む`AssemblerResult`オブジェクトを返します。

1. 組み立てたポートフォリオを保存します。

   新しく作成したPDFPortfolioを取得するには、次の操作を実行します。

   * `AssemblerResult`オブジェクトの`documents`フィールド（結果のPDFドキュメントを含む`Map`オブジェクト）にアクセスします。
   * `Map`オブジェクトを繰り返し処理して、各結果ドキュメントを取得します。 次に、配列メンバの`value`を`BLOB`にキャストします。
   * `BLOB`オブジェクトの`MTOM`プロパティにアクセスして、PDFドキュメントを表すバイナリデータを抽出します。 PDFファイルに書き出すことができるバイトの配列を返します。

**関連トピック**

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
