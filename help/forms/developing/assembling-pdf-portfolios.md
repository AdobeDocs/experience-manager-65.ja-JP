---
title: PDFPortfolioのアセンブリ
seo-title: PDFPortfolioのアセンブリ
description: PDFポートフォリオをアセンブリして、Wordファイル、画像ファイル、PDFドキュメントなど、様々な種類のドキュメントを組み合わせます。 Java APIとWeb Service APIを使用してPDFポートフォリオをアセンブリできます。
seo-description: PDFポートフォリオをアセンブリして、Wordファイル、画像ファイル、PDFドキュメントなど、様々な種類のドキュメントを組み合わせます。 Java APIとWeb Service APIを使用してPDFポートフォリオをアセンブリできます。
uuid: 1778c90b-9d26-466b-a7c7-401d737395e0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 023f0d9e-bfde-4879-a839-085fadffb48e
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '1851'
ht-degree: 3%

---


# PDFPortfolioのアセンブリ{#assembling-pdf-portfolios}

Assembler JavaおよびWebサービスAPIを使用してPDFPortfolioをアセンブリできます。 ポートフォリオは、Wordファイル、画像ファイル（jpegファイルなど）、PDFドキュメントなど、様々な種類のドキュメントを組み合わせることができます。 ポートフォリオのレイアウトは、*プレビュー付きグリッド*、*画像*&#x200B;レイアウトまたは&#x200B;*回転*&#x200B;など、異なるスタイルに設定できます。

次の図は、*画像*&#x200B;スタイルレイアウトのポートフォリオのスクリーンショットです。

![ap_ap_portfolio](assets/ap_ap_portfolio.png)

PDFPortfolioを作成すると、ドキュメントの集まりを渡す代わりに、ペーパーレスで行うことができます。 AEM Formsを使用すると、構造化DDXドキュメントを使用してAssemblerサービスを呼び出し、ポートフォリオを作成できます。 次のDDXドキュメントは、PDFPortfolioを作成するDDXドキュメントの例です。

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

DXXドキュメントには、`Portfolio`タグと入れ子の`Navigator`タグが含まれている必要があります。 タグ`<Resource name="navigator/image.xxx" source="myImage.png"/>`は、`myNavigator`がonImageレイアウトナビゲーターとして割り当てられている場合にのみ必要です。`AdobeOnImage.nav`。 このタグを使用すると、Assemblerサービスでポートフォリオの背景として使用する画像を選択できます。 パッケージファイルのファイル名とMIMEタイプを定義するには、`PackageFiles`タグと`File`タグを含めます。

>[!NOTE]
>
>Assemblerサービスについて詳しくは、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

>[!NOTE]
>
>DDXドキュメントについて詳しくは、「[Assembler Service and DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63)」を参照してください。

## 手順{#summary-of-steps}の概要

PDFPortfolioを作成するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. PDFアセンブラクライアントを作成します。
1. 既存のDDXドキュメントの参照。
1. 必要なドキュメントを参照します。
1. 実行時オプションを設定します。
1. ポートフォリオをアセンブルします。
1. 組み立てたポートフォリオを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(AEM FormsがJBossにデプロイされている場合に必要)
* jbossall-client.jar(AEM FormsがJBossにデプロイされている場合に必要)

**PDFアセンブラクライアントの作成**

プログラムによってAssembler操作を実行する前に、Assemblerサービスクライアントを作成します。

**既存のDDXドキュメントの参照**

PDFPortfolioをアセンブリするには、DDXドキュメントを参照する必要があります。 このDDXドキュメントには、`Portfolio`、`Navigator`および`PackageFiles`要素を含める必要があります。

**必要なドキュメントの参照**

PDFPortfolioをアセンブリするには、アセンブリ対象のドキュメントを表すすべてのファイルを参照します。 例えば、DDXドキュメントで指定されているすべての画像ファイルをAssemblerサービスに渡します。 これらのファイルは、この節で指定するDDXドキュメントで参照されます。*myImage.png*&#x200B;と&#x200B;*saint_bernard.jpg*

PDFPortfolioのアセンブリ時に、NAVファイル（ナビゲータファイル）をAssemblerサービスに渡します。 Assemblerサービスに渡すNAVファイルは、作成するPDFPortfolioのタイプに応じて異なります。 例えば、*On an Image*&#x200B;レイアウトを作成するには、AdobeOnImage.navファイルを渡します。 NAVファイルは次のフォルダーにあります。

`<Install folder>\Acrobat 9.0\Acrobat\Navigators`

NAVファイルをAcrobat 9（またはそれ以降）のインストールディレクトリからコピーします。 NAVファイルは、クライアントアプリケーションがアクセスできる場所に配置します。 すべてのファイルは、Mapコレクションオブジェクト内でAssemblerサービスに渡されます。

>[!NOTE]
>
>PDFPortfolioのアセンブリに関連付けられているクイック開始では、AdobeOnImage.navを使用します。

**実行時オプションの設定**

ジョブの実行中にAssemblerサービスの動作を制御する実行時オプションを設定できます。 例えば、エラーが発生した場合にジョブの処理を続行するようAssemblerサービスに指示するオプションを設定できます。

**ポートフォリオの編成**

PDFPortfolioをアセンブリするには、`invokeDDX`操作を呼び出します。 Assemblerサービスは、コレクションオブジェクト内でPDFPortfolioを返します。

**組み立てたポートフォリオの保存**

コレクションオブジェクト内でPDFPortfolioが返されます。 コレクションオブジェクトを繰り返し処理し、PDFPortfolioをPDFファイルとして保存します。

**関連トピック**

[Java APIを使用したPDFPortfolioのアセンブリ](#assemble-a-pdf-portfolio-using-the-java-api)

[WebサービスAPIを使用したPDFPortfolioのアセンブリ](#assemble-a-pdf-portfolio-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[プログラムによるPDFドキュメントのアセンブリ](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java API {#assemble-a-pdf-portfolio-using-the-java-api}を使用したPDFPortfolioのアセンブリ

Assembler Service API(Java)を使用してPDFPortfolioをアセンブリします。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-assembler-client.jarなどのクライアントJARファイルを含めます。

1. PDFアセンブラクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用し、`AssemblerServiceClient`オブジェクトを渡して、`ServiceClientFactory`オブジェクトを作成します。

1. 既存のDDXドキュメントの参照。

   * コンストラクターを使用し、DDXファイルの場所を指定する文字列値を渡して、DDXドキュメントを表す`java.io.FileInputStream`オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 必要なドキュメントを参照します。

   * `HashMap`コンストラクターを使用して、入力PDFドキュメントの格納に使用する`java.util.Map`オブジェクトを作成します。
   * コンストラクタを使用して `java.io.FileInputStream` オブジェクトを作成します。必要なNAVファイルの場所を渡します(ポートフォリオの作成に必要な各ファイルに対してこのタスクを繰り返します)。
   * `com.adobe.idp.Document`オブジェクトを作成し、NAVファイルを含む`java.io.FileInputStream`オブジェクトを渡します(ポートフォリオの作成に必要な各ファイルに対してこのタスクを繰り返します)。
   * &lt;a0追加/>オブジェクトへのエントリ。その`java.util.Map`メソッドを呼び出し、次の引数を渡すことによって作成します。`put`

      * キー名を表すstring値です。 この値は、DDXドキュメントで指定されたソース要素の値と一致する必要があります。 (ポートフォリオの作成に必要なファイルごとに、このタスクを繰り返します)。
      * PDFドキュメントを含む`com.adobe.idp.Document`オブジェクトです。 (ポートフォリオの作成に必要なファイルごとに、このタスクを繰り返します)。

1. 実行時オプションを設定します。

   * コンストラクターを使用して、実行時オプションを格納する`AssemblerOptionSpec`オブジェクトを作成します。
   * `AssemblerOptionSpec`オブジェクトに属するメソッドを呼び出して、ビジネス要件に合うように実行時オプションを設定します。 例えば、エラーが発生した場合にジョブの処理を続行するようにAssemblerサービスに指示するには、`AssemblerOptionSpec`オブジェクトの`setFailOnError`メソッドを呼び出し、`false`を渡します。

1. ポートフォリオをアセンブルします。

   `AssemblerServiceClient`オブジェクトの`invokeDDX`メソッドを呼び出し、次の必須値を渡します。

   * 使用するDDXドキュメントを表す`com.adobe.idp.Document`オブジェクト
   * PDFPortfolioの構築に必要なファイルが含まれる`java.util.Map`オブジェクトです。
   * デフォルトフォントとジョブログレベルを含む、ランタイムオプションを指定する`com.adobe.livecycle.assembler.client.AssemblerOptionSpec`オブジェクト

   `invokeDDX`メソッドは、アセンブリされたPDFPortfolioと発生した例外を含む`com.adobe.livecycle.assembler.client.AssemblerResult`オブジェクトを返します。

1. 組み立てたポートフォリオを保存します。

   PDFPortfolioを取得するには、次の操作を実行します。

   * `AssemblerResult`オブジェクトの`getDocuments`メソッドを呼び出します。 このメソッドは、`java.util.Map`オブジェクトを返します。
   * `java.util.Map`オブジェクトを繰り返し処理して、結果の`com.adobe.idp.Document`オブジェクトを見つけます。
   * `com.adobe.idp.Document`オブジェクトの`copyToFile`メソッドを呼び出してPDFPortfolioを抽出します。

**関連トピック**

[クイック開始（SOAPモード）:Java APIを使用したPDFPortfolioのアセンブリ](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-portfolios-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## WebサービスAPI {#assemble-a-pdf-portfolio-using-the-web-service-api}を使用してPDFPortfolioをアセンブリする

Assembler Service API（Webサービス）を使用してPDFPortfolioをアセンブリします。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 サービス参照を設定する際は、次のWSDL定義を使用してください。`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. PDFアセンブラクライアントを作成します。

   * `AssemblerServiceClient`オブジェクトを作成するには、そのオブジェクトのデフォルトのコンストラクタを使用します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`AssemblerServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに指定するstring値を渡します（例：`http://localhost:8080/soap/services/AssemblerService?blob=mtom`）。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する際に使用されます。
   * `AssemblerServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * AEM formsユーザー名をフィールド`AssemblerServiceClient.ClientCredentials.UserName.UserName`に割り当てます。
      * 対応するパスワード値をフィールド`AssemblerServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * 定数値`HttpClientCredentialType.Basic`をフィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に割り当てます。
      * 定数値`BasicHttpSecurityMode.TransportCredentialOnly`をフィールド`BasicHttpBindingSecurity.Security.Mode`に割り当てます。

1. 既存のDDXドキュメントの参照。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、DDXドキュメントの保存に使用されます。
   * コンストラクターを呼び出し、DDXドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得して、バイト配列のサイズを決定できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出して、バイト配列にストリームデータを入力します。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * `BLOB`オブジェクトに`MTOM`プロパティを割り当て、バイト配列の内容を指定します。

1. 必要なドキュメントを参照します。

   * 各入力ファイルに対して、コンストラクタを使用して`BLOB`オブジェクトを作成します。 `BLOB`オブジェクトは、入力ファイルの保存に使用されます。
   * コンストラクターを呼び出し、入力ファイルのファイルの場所とファイルを開くモードを表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得して、バイト配列のサイズを決定できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出して、バイト配列にストリームデータを入力します。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * `BLOB`オブジェクトに、`MTOM`フィールドにバイト配列の内容を割り当てて入力します。
   * `MyMapOf_xsd_string_To_xsd_anyType`オブジェクトを作成します。 このコレクションオブジェクトは、PDFPortfolioの作成に必要な入力ファイルの格納に使用されます。
   * 入力ファイルごとに、`MyMapOf_xsd_string_To_xsd_anyType_Item`オブジェクトを作成します。
   * キー名を表すstring値を`MyMapOf_xsd_string_To_xsd_anyType_Item`オブジェクトの`key`フィールドに割り当てます。 この値は、DDXドキュメントで指定された要素の値と一致する必要があります。 (このタスクは、入力ファイルごとに実行します)。
   * 入力ファイルを保存する`BLOB`オブジェクトを`MyMapOf_xsd_string_To_xsd_anyType_Item`オブジェクトの`value`フィールドに割り当てます。 (このタスクは、入力PDFドキュメントごとに実行します)。
   * 追加`MyMapOf_xsd_string_To_xsd_anyType`オブジェクトの`MyMapOf_xsd_string_To_xsd_anyType_Item`オブジェクト。 `MyMapOf_xsd_string_To_xsd_anyType`オブジェクトの`Add`メソッドを呼び出し、`MyMapOf_xsd_string_To_xsd_anyType`オブジェクトを渡します。 (このタスクは、入力PDFドキュメントごとに実行します)。

1. 実行時オプションを設定します。

   * コンストラクターを使用して、実行時オプションを格納する`AssemblerOptionSpec`オブジェクトを作成します。
   * `AssemblerOptionSpec`オブジェクトに属するデータメンバに値を割り当てて、ビジネス要件に合うように実行時オプションを設定します。 例えば、エラーが発生した場合にジョブの処理を続行するようにAssemblerサービスに指示するには、`false`を`AssemblerOptionSpec`オブジェクトの`failOnError`データメンバーに割り当てます。

1. ポートフォリオをアセンブルします。

   `AssemblerServiceClient`オブジェクトの`invokeDDX`メソッドを呼び出し、次の値を渡します。

   * DDXドキュメントを表す`BLOB`オブジェクト
   * 必要なファイルを含む`MyMapOf_xsd_string_To_xsd_anyType`オブジェクト
   * 実行時オプションを指定する`AssemblerOptionSpec`オブジェクト

   `invokeDDX`メソッドは、ジョブの結果と発生した例外を含む`AssemblerResult`オブジェクトを返します。

1. 組み立てたポートフォリオを保存します。

   新しく作成されたPDFPortfolioを取得するには、次の操作を実行します。

   * `AssemblerResult`オブジェクトの`documents`フィールドにアクセスします。これは、結果のPDFドキュメントを含む`Map`オブジェクトです。
   * `Map`オブジェクトを繰り返し処理して、各結果ドキュメントを取得します。 次に、その配列メンバーの`value`を`BLOB`にキャストします。
   * `BLOB`オブジェクトの`MTOM`プロパティにアクセスして、PDFドキュメントを表すバイナリデータを抽出します。 PDFファイルに書き出すことができるバイトの配列を返します。

**関連トピック**

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
