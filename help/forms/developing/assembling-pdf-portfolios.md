---
title: PDFポートフォリオのアセンブリ
seo-title: PDFポートフォリオのアセンブリ
description: 'null'
seo-description: 'null'
uuid: 1778c90b-9d26-466b-a7c7-401d737395e0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 023f0d9e-bfde-4879-a839-085fadffb48e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# PDFポートフォリオのアセンブリ {#assembling-pdf-portfolios}

Assembler javaおよびWebサービスAPIを使用して、PDFポートフォリオをアセンブルできます。 ポートフォリオでは、Wordファイル、画像ファイル（例えば、jpegファイル）、PDFドキュメントなど、様々な種類のドキュメントを組み合わせることができます。 ポートフォリオのレイアウトは、「プレビュー付きグリッド」、「画像レイアウト上 *」、「回転体」など*、様々なス *タイルに設定で* きます **。

次の図は、画像スタイルレイアウトのポートフォリオのス *クリーンショット* です。

![ap_ap_portfolio](assets/ap_ap_portfolio.png)

PDFポートフォリオの作成は、ドキュメントのコレクションを渡す代わりにペーパーレスで行うことができます。 AEM formsを使用すると、構造化DDXドキュメントでAssemblerサービスを呼び出してポートフォリオを作成できます。 次のDDXドキュメントは、PDFポートフォリオを作成するDDXドキュメントの例です。

```as3
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

DXXドキュメントには、タグが入れ子になっ `Portfolio` ている必要があ `Navigator` ります。 タグは、onImageレイアウ `<Resource name="navigator/image.xxx" source="myImage.png"/>` トナビゲーターとし `myNavigator` て割り当てられている場合にのみ必要です。 `AdobeOnImage.nav`. このタグを使用すると、Assemblerサービスでポートフォリオの背景として使用する画像を選択できます。 パッケ `PackageFiles` ージフ `File` ァイルのファイル名とMIMEタイプを定義するタグとタグを含めます。

>[!NOTE]
>
>For more information about the Assembler service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>DDXドキュメントについて詳しくは、 [Assembler Service and DDX Referenceを参照してください](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 手順の概要 {#summary-of-steps}

PDFポートフォリオを作成するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. PDFアセンブラクライアントを作成します。
1. 既存のDDXドキュメントを参照します。
1. 必要なドキュメントを参照します。
1. 実行時オプションを設定します。
1. ポートフォリオをアセンブルします。
1. 組み立てたポートフォリオを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar（AEM FormsがJBossにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsをJBossにデプロイする場合に必要）

**PDFアセンブラクライアントの作成**

プログラムによってAssembler操作を実行する前に、Assemblerサービスクライアントを作成します。

**既存のDDXドキュメントの参照**

PDFポートフォリオをアセンブリするには、DDXドキュメントを参照する必要があります。 このDDXドキュメントには、、およびエレメン `Portfolio`トを含め `Navigator` る必要が `PackageFiles` あります。

**必要なドキュメントの参照**

PDFポートフォリオをアセンブリするには、アセンブリ対象のドキュメントを表すすべてのファイルを参照します。 例えば、DDXドキュメントで指定されているすべての画像ファイルをAssemblerサービスに渡します。 これらのファイルは、この節で指定したDDXドキュメント内で参照されます。 *myImage.png* 、 *saint_bernard.jpg*。

PDFポートフォリオをアセンブリする場合は、NAVファイル（ナビゲーターファイル）をAssemblerサービスに渡します。 Assemblerサービスに渡すNAVファイルは、作成するPDFポートフォリオのタイプによって異なります。 例えば、On an Imageレイアウトを作 *成するには* 、AdobeOnImage.navファイルを渡します。 NAVファイルは次のフォルダーにあります。

`<Install folder>\Acrobat 9.0\Acrobat\Navigators`

Acrobat 9以降のインストールディレクトリからNAVファイルをコピーします。 NAVファイルは、クライアントアプリケーションがアクセスできる場所に配置します。 すべてのファイルは、Mapコレクションオブジェクト内でAssemblerサービスに渡されます。

>[!NOTE]
>
>PDFポートフォリオのアセンブリに関連するクイックスタートでは、AdobeOnImage.navを使用します。

**実行時オプションの設定**

ジョブの実行中にAssemblerサービスの動作を制御する実行時オプションを設定できます。 例えば、エラーが発生した場合にジョブの処理を続行するようAssemblerサービスに指示するオプションを設定できます。

**ポートフォリオのアセンブル**

PDFポートフォリオをアセンブリするには、操作を呼び出 `invokeDDX` します。 Assemblerサービスは、コレクションオブジェクト内のPDFポートフォリオを返します。

**組み立てたポートフォリオの保存**

PDFポートフォリオは、コレクションオブジェクト内で返されます。 コレクションオブジェクトを繰り返し処理し、PDFポートフォリオをPDFファイルとして保存します。

**関連トピック**

[Java APIを使用したPDFポートフォリオのアセンブリ](#assemble-a-pdf-portfolio-using-the-java-api)

[WebサービスAPIを使用したPDFポートフォリオのアセンブリ](#assemble-a-pdf-portfolio-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDFドキュメントのプログラムによるアセンブリ](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java APIを使用したPDFポートフォリオのアセンブリ {#assemble-a-pdf-portfolio-using-the-java-api}

Assembler Service API(Java)を使用してPDFポートフォリオをアセンブリします。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-assembler-client.jarなどのクライアントJARファイルを含めます。

1. PDFアセンブラクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `AssemblerServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. 既存のDDXドキュメントを参照します。

   * コンストラ `java.io.FileInputStream` クターを使用し、DDXファイルの場所を指定するstring値を渡して、DDXドキュメントを表すオブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 必要なドキュメントを参照します。

   * コンストラク `java.util.Map` ターを使用して、入力PDFドキュメントの保存に使用するオブジェクトを作成 `HashMap` します。
   * コンストラクタを使用して `java.io.FileInputStream` オブジェクトを作成します。必要なNAVファイルの場所を渡します（ポートフォリオの作成に必要な各ファイルに対してこのタスクを繰り返します）。
   * オブジェクト `com.adobe.idp.Document` を作成し、NAVファ `java.io.FileInputStream` イルを含むオブジェクトを渡します（ポートフォリオの作成に必要な各ファイルに対してこの作業を繰り返します）。
   * メソッドを呼び出し、次 `java.util.Map` の引数を渡して、オ `put` ブジェクトにエントリを追加します。

      * キー名を表すstring値です。 この値は、DDXドキュメントで指定されたソース要素の値と一致する必要があります。 （ポートフォリオの作成に必要な各ファイルに対して、このタスクを繰り返します）。
      * PDFドキ `com.adobe.idp.Document` ュメントを含むオブジェクトです。 （ポートフォリオの作成に必要な各ファイルに対して、このタスクを繰り返します）。

1. 実行時オプションを設定します。

   * コンストラクタ `AssemblerOptionSpec` ーを使用して、実行時のオプションを格納するオブジェクトを作成します。
   * オブジェクトに属するメソッドを呼び出して、ビジネス要件に合わせて実行時のオプションを設定 `AssemblerOptionSpec` します。 例えば、エラーが発生した場合にジョブの処理を続行するようにAssemblerサービスに指示するには、オブジェクトのメソッド `AssemblerOptionSpec` を呼び出して `setFailOnError` 渡してくださ `false`い。

1. ポートフォリオをアセンブルします。

   オブジェクト `AssemblerServiceClient` のメソッドを呼 `invokeDDX` び出し、次の必要な値を渡します。

   * 使用す `com.adobe.idp.Document` るDDXドキュメントを表すオブジェクトです
   * PDFポー `java.util.Map` トフォリオの構築に必要なファイルを含むオブジェクトです。
   * デフォ `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` ルトフォントやジョブログレベルを含む、ランタイムオプションを指定するオブジェクト。
   このメソ `invokeDDX` ッドは、アセンブリ `com.adobe.livecycle.assembler.client.AssemblerResult` されたPDFポートフォリオと発生した例外を含むオブジェクトを返します。

1. 組み立てたポートフォリオを保存します。

   PDFポートフォリオを取得するには、次の操作を実行します。

   * オブジェクト `AssemblerResult` のメソッドを呼び出 `getDocuments` します。 このメソッドは、オブジェクトを `java.util.Map` 返します。
   * 結果のオブジェクト `java.util.Map` が見つかるまで、オブジェクトを繰り返 `com.adobe.idp.Document` します。
   * オブジェクトの `com.adobe.idp.Document` メソッドを呼び `copyToFile` 出して、PDFポートフォリオを抽出します。

**関連トピック**

[クイックスタート（SOAPモード）:Java APIを使用したPDFポートフォリオの集成](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-portfolios-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## WebサービスAPIを使用したPDFポートフォリオのアセンブリ {#assemble-a-pdf-portfolio-using-the-web-service-api}

Assembler Service API（Webサービス）を使用してPDFポートフォリオをアセンブリします。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 サービス参照を設定する際は、必ず次のWSDL定義を使用してください。 `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. PDFアセンブラクライアントを作成します。

   * デフォルトのコンス `AssemblerServiceClient` トラクターを使用して、オブジェクトを作成します。
   * コンストラクタ `AssemblerServiceClient.Endpoint.Address` ーを使用してオブジェクトを作 `System.ServiceModel.EndpointAddress` 成します。 WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/AssemblerService?blob=mtom`)に渡すstring値。 属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `AssemblerServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `AssemblerServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `AssemblerServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. 既存のDDXドキュメントを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオブ `BLOB` ジェクトは、DDXドキュメントの保存に使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、DDXドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出して、バイト配列にストリームデ `System.IO.FileStream` ータを入力 `Read` します。 読み取るバイト配列、開始位置およびストリーム長を渡します。
   * オブジェクト `BLOB` にバイト配列の内容をプロ `MTOM` パティに割り当てて、オブジェクトを設定します。

1. 必要なドキュメントを参照します。

   * 各入力ファイルに対して、コンストラクターを使 `BLOB` 用してオブジェクトを作成します。 このオ `BLOB` ブジェクトは、入力ファイルの保存に使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、入力ファイルのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出して、バイト配列にストリームデ `System.IO.FileStream` ータを入力 `Read` します。 読み取るバイト配列、開始位置およびストリーム長を渡します。
   * オブジェクト `BLOB` にバイト配列の内容を `MTOM` フィールドに割り当てて、オブジェクトを入力します。
   * Create a `MyMapOf_xsd_string_To_xsd_anyType` object. このコレクションオブジェクトは、PDFポートフォリオの作成に必要な入力ファイルの保存に使用されます。
   * 入力ファイルごとに、オブジェクトを作成 `MyMapOf_xsd_string_To_xsd_anyType_Item` します。
   * キー名を表すstring値をオブジェクトのフィールド `MyMapOf_xsd_string_To_xsd_anyType_Item` に割り当て `key` ます。 この値は、DDXドキュメントで指定されたエレメントの値と一致する必要があります。 （入力ファイルごとにこのタスクを実行します）。
   * 入力ファイル `BLOB` を格納するオブジェクトをオブジェクトのフィー `MyMapOf_xsd_string_To_xsd_anyType_Item` ルドに割り当 `value` てます。 （入力PDFドキュメントごとにこのタスクを実行します）。
   * オブジェクト `MyMapOf_xsd_string_To_xsd_anyType_Item` をオブジェクトに追加 `MyMapOf_xsd_string_To_xsd_anyType` します。 Invoke the `MyMapOf_xsd_string_To_xsd_anyType` object&#39;s `Add` method and pass the `MyMapOf_xsd_string_To_xsd_anyType` object. （入力PDFドキュメントごとにこのタスクを実行します）。

1. 実行時オプションを設定します。

   * コンストラクタ `AssemblerOptionSpec` ーを使用して、実行時のオプションを格納するオブジェクトを作成します。
   * オブジェクトに属するデータメンバーに値を割り当てて、ビジネス要件に合わせて実行時オプションを設定 `AssemblerOptionSpec` します。 例えば、エラーが発生した場合にジョブの処理を続行するようAssemblerサービスに指示するには、オブジェクトの `false` データメ `AssemblerOptionSpec` ンバーに割り `failOnError` 当てます。

1. ポートフォリオをアセンブルします。

   オブジェクト `AssemblerServiceClient` のメソッドを `invokeDDX` 呼び出し、次の値を渡します。

   * DDXドキ `BLOB` ュメントを表すオブジェクト
   * 必要な `MyMapOf_xsd_string_To_xsd_anyType` ファイルを含むオブジェクトです
   * 実行時 `AssemblerOptionSpec` のオプションを指定するオブジェクト
   このメ `invokeDDX` ソッドは、ジョ `AssemblerResult` ブの結果と発生した例外を含むオブジェクトを返します。

1. 組み立てたポートフォリオを保存します。

   新しく作成されたPDFポートフォリオを取得するには、次の操作を実行します。

   * 結果のPDFドキ `AssemblerResult` ュメントを含むオ `documents` ブジェクトのフ `Map` ィールドにアクセスします。
   * オブジェクトを繰り返し `Map` 処理し、各結果ドキュメントを取得します。 次に、その配列メンバーをにキャス `value` トします `BLOB`。
   * PDFドキュメントを表すバイナリデータを抽出するには、そのオブジェクトのプロパ `BLOB` ティにアクセス `MTOM` します。 PDFファイルに書き出し可能なバイト配列を返します。

**関連トピック**

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
