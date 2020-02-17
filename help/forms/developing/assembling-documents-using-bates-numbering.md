---
title: ベイツナンバリングを使用したドキュメントのアセンブリ
seo-title: ベイツナンバリングを使用したドキュメントのアセンブリ
description: 'null'
seo-description: 'null'
uuid: 28d5faeb-6915-41a2-b6a0-78d255df024f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 77e9b895-1313-4a5b-a2d5-cdb65bdc1966
translation-type: tm+mt
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d

---


# Assembling Documents Using Bates Numbering {#assembling-documents-using-bates-numbering}

ベイツナンバリングを使用して、一意のページ識別子を含むPDFドキュメントをアセンブリできます。 *ベイツナンバリングは* 、関連ドキュメントのバッチに一意の識別子を適用する方法です。 ドキュメント内の各ページ（またはドキュメントのセット）に、ページを一意に識別するベイツ番号が割り当てられます。 例えば、原材料情報を含む、1 つの組立部品の製造に関する生産ドキュメントに、1 つの識別子が割り当てられます。ベイツナンバリングの数値は連続した増分値で、オプションでプレフィックスやサフィックスが付きます。接頭辞+数値+接尾辞は、ベイツパターンと呼ば *れます*。

次の例は、ドキュメントのヘッダに一意の識別子を含む PDF ドキュメントを示しています。

![au_au_batesnumber](assets/au_au_batesnumber.png)

このディスカッションの目的では、一意のページ識別子がドキュメントのヘッダーに配置されます。 次のDDXドキュメントが使用されているとします。

```as3
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
        <PDF result="out.pdf">
        <Header>
         <Center>
             <StyledText>
                 <p font-size="20pt"><BatesNumber/></p>
             </StyledText>
         </Center>
     </Header>
           <PDF source="map.pdf" />
          <PDF source="directions.pdf" />
          </PDF>
 </DDX>
```

このDDXドキュメントは、 *map.pdfとdirections.pdfという名前の2つのPDF* ドキュメントを ** 1つのPDFドキュメントにマージします。 結果のPDFドキュメントには、一意のページ識別子で構成されるヘッダーが含まれます。 例えば、上の図のドキュメントでは000016と表示されています。

>[!NOTE]
>
>この節を読む前に、Assemblerサービスを使用したPDFドキュメントのアセンブリについて詳しく知ることをお勧めします。 ここでは、入力ドキュメントを含むコレクションオブジェクトの作成、返されたコレクションオブジェクトからの結果の抽出など、概念については説明しません。 (「プログラ [ムによるPDFドキュメントの集成](/help/forms/developing/programmatically-assembling-pdf-documents.md)」を参照)。

>[!NOTE]
>
>For more information about the Assembler service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>DDXドキュメントについて詳しくは、 [Assembler Service and DDX Referenceを参照してください](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 手順の概要 {#summary-of-steps}

一意のページ識別子（ベイツナンバリング）を含むPDFドキュメントをアセンブリするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. PDFアセンブラクライアントを作成します。
1. 既存のDDXドキュメントを参照します。
1. 入力PDFドキュメントを参照します。
1. ベイツ番号の初期値を設定します。
1. 入力PDFドキュメントをアセンブリします。
1. 結果を抽出します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar（AEM FormsがJBossにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsをJBossにデプロイする場合に必要）

AEM formsをJBoss以外のサポート対象のJ2EEアプリケーションサーバーにデプロイする場合は、adobe-utilities.jarファイルとjbossall-client.jarファイルを、AEM FormsがデプロイされるJ2EEアプリケーションサーバーに固有のJARファイルに置き換える必要があります。 For information about the location of all AEM Forms JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**PDFアセンブラクライアントの作成**

プログラムでAssembler操作を実行する前に、Assemblerサービスクライアントを作成する必要があります。

**既存のDDXドキュメントの参照**

PDFドキュメントをアセンブリするには、DDXドキュメントを参照する必要があります。 例えば、この節で紹介したDDXドキュメントについて考えてみましょう。 一意のページ識別子を含むPDFドキュメントをアセンブリするには、DDXドキュメントにその要素が含まれている必要があ `BatesNumber` ります。

**入力PDFドキュメントの参照**

PDFドキュメントをアセンブリするには、入力PDFドキュメントを参照する必要があります。 例えば、map.pdfおよびdirections.pdfドキュメントを参照して、これらのPDFドキュメントを1つのPDFドキュメントにアセンブリする必要があります。

**ベイツ番号の初期値を設定**

ビジネス要件に合わせて、ベイツナンバリングの初期値を設定できます。 例えば、初期値を000100に設定する必要があるとします。 初期値を設定しない場合、最初のページの値は000000です。

**入力PDFドキュメントのアセンブリ**

Assemblerサービスクライアントを作成し、要素情報を含むDDXドキュメントを参照し、入力PDFドキュメントを参照し、実行時オプションを設定した後で、Assemblerサービスを呼び出して、一意のページ識別子を含むPDFドキュメントをアセンブリできます。 `BatesNumber``invokeDDX`

**結果の抽出**

Assemblerサービスは、ジョブ結果を含むコレクションオブジェクトを返します。 結果のPDFドキュメントと、スローされた例外を抽出できます。 この場合、暗号化されたPDFドキュメントはコレクションオブジェクト内に配置されます。

>[!NOTE]
>
>操作を呼び出すと、コレクションオブジェクトが返さ `invokeDDX` れます。 この操作は、2つ以上の入力PDFドキュメントをAssemblerサービスに渡す場合に使用されます。 ただし、1つの入力PDFドキュメントのみをAssemblerサービスに渡す場合は、操作を呼び出す必要があ `invokeOneDocument` ります。 この操作の使用に関する詳細は、暗号化されたPDFドキュメ [ントのアセンブリを参照してくださ](/help/forms/developing/assembling-encrypted-pdf-documents.md)い。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDFドキュメントのプログラムによるアセンブリ](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java APIを使用したベイツナンバリングによるドキュメントのアセンブリ {#assemble-documents-with-bates-numbering-using-the-java-api}

Assembler Service API(Java)を使用して、一意のページ識別子（ベイツナンバリング）を使用するPDFドキュメントをアセンブリします。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-assembler-client.jarなどのクライアントJARファイルを含めます。

1. PDFアセンブラクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `AssemblerServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. 既存のDDXドキュメントを参照します。

   * コンストラ `java.io.FileInputStream` クターを使用し、DDXファイルの場所を指定するstring値を渡して、DDXドキュメントを表すオブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 入力PDFドキュメントを参照します。

   * コンストラクタ `java.util.Map` ーを使用して、入力PDFドキュメントの保存に使用するオブジェクトを作成 `HashMap` します。
   * 各入力PDFドキュメントに対して、コンストラク `java.io.FileInputStream` ターを使用し、入力PDFドキュメントの場所を渡して、オブジェクトを作成します。 この場合、保護されていないPDFドキュメントの場所を渡します。
   * 入力PDFドキュメントごとに、オブジェクトを作成 `com.adobe.idp.Document` し、そのPDFドキュメントを `java.io.FileInputStream` 含むオブジェクトを渡します。
   * メソッドを呼び出し、次 `java.util.Map` の引数を渡して、オ `put` ブジェクトにエントリを追加します。

      * キー名を表すstring値です。 この値は、DDXドキュメントで指定されたPDFソース要素の値と一致する必要があります。 例えば、この節で紹介するDDXドキュメントで指定されているPDFソースファイルの名前はLoan.pdfです。
      * 保護され `com.adobe.idp.Document` ていないPDFドキュメントを含むオブジェクトです。

1. ベイツ番号の初期値を設定します。

   * コンストラクタ `AssemblerOptionSpec` ーを使用して、実行時のオプションを格納するオブジェクトを作成します。
   * オブジェクトを呼び出し、初期値を `AssemblerOptionSpec` 指定する数 `setFirstBatesNumber` 値を渡して、初期ベイツ番号を設定します。

1. 入力PDFドキュメントをアセンブリします。

   オブジェクト `AssemblerServiceClient` のメソッドを呼 `invokeDDX` び出し、次の必要な値を渡します。

   * DDXドキ `com.adobe.idp.Document` ュメントを表すオブジェクトです。
   * 保護さ `java.util.Map` れていない入力PDFファイルを含むオブジェクトです。
   * デフォ `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` ルトのフォントやジョブログレベルなど、実行時のオプションを指定するオブジェクトです。
   このメソ `invokeDDX` ッドは、パスワードで `com.adobe.livecycle.assembler.client.AssemblerResult` 暗号化されたPDFドキュメントを含むオブジェクトを返します。

1. 結果を抽出します。

   新しく作成したPDFドキュメントを取得するには、次の操作を実行します。

   * オブジェクト `AssemblerResult` のメソッドを呼び出 `getDocuments` します。 このアクションはオブジェクトを `java.util.Map` 返します。
   * オブジェクトが見つか `java.util.Map` るまで、オブジェクトを繰り返 `com.adobe.idp.Document` します。
   * オブジェクト `com.adobe.idp.Document` のメソッドを呼 `copyToFile` び出してPDFドキュメントを抽出します。

**関連トピック**

[クイックスタート（SOAPモード）:Java APIを使用したベイツナンバリングを使用したPDFドキュメントのアセンブリ](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-with-bates-numbering-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## WebサービスAPIを使用してベイツナンバリングを使用してドキュメントをアセンブリする {#assemble-documents-with-bates-numbering-using-the-web-service-api}

Assembler Service API（Webサービス）を使用して、一意のページ識別子（ベイツナンバリング）を使用するPDFドキュメントをアセンブリします。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

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
   * オブジェクト `BLOB` にバイト配列の内容を `MTOM` フィールドに割り当てて、オブジェクトを入力します。

1. 入力PDFドキュメントを参照します。

   * 入力PDFドキュメントごとに、コンストラクターを使用 `BLOB` してオブジェクトを作成します。 このオ `BLOB` ブジェクトは、入力PDFドキュメントの保存に使用されます。
   * Create a `System.IO.FileStream` object by invoking its constructor. 入力PDFドキュメントのファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出して、バイト配列にストリームデ `System.IO.FileStream` ータを入力 `Read` します。 読み取るバイト配列、開始位置およびストリーム長を渡します。
   * オブジェクト `BLOB` にバイト配列の内容をプロ `MTOM` パティに割り当てて、オブジェクトを設定します。
   * Create a `MyMapOf_xsd_string_To_xsd_anyType` object. このコレクションオブジェクトは、入力PDFドキュメントの保存に使用されます。
   * 入力PDFドキュメントごとに、オブジェクトを作成 `MyMapOf_xsd_string_To_xsd_anyType_Item` します。 例えば、2つの入力PDFドキュメントを使用する場合は、2つのオブジェクトを作成 `MyMapOf_xsd_string_To_xsd_anyType_Item` します。
   * キー名を表すstring値をオブジェクトのフィールド `MyMapOf_xsd_string_To_xsd_anyType_Item` に割り当て `key` ます。 この値は、DDXドキュメントで指定されたPDFソース要素の値と一致する必要があります。 （入力PDFドキュメントごとにこのタスクを実行します）。
   * PDFドキュメント `BLOB` を保存するオブジェクトをオブジェクトのフィー `MyMapOf_xsd_string_To_xsd_anyType_Item` ルドに割り当 `value` てます。 （入力PDFドキュメントごとにこのタスクを実行します）。
   * オブジェクト `MyMapOf_xsd_string_To_xsd_anyType_Item` をオブジェクトに追加 `MyMapOf_xsd_string_To_xsd_anyType` します。 Invoke the `MyMapOf_xsd_string_To_xsd_anyType` object&#39;s `Add` method and pass the `MyMapOf_xsd_string_To_xsd_anyType` object. （入力PDFドキュメントごとにこのタスクを実行します）。

1. ベイツ番号の初期値を設定します。

   * コンストラクタ `AssemblerOptionSpec` ーを使用して、実行時のオプションを格納するオブジェクトを作成します。
   * オブジェクトに属するデータ・メンバーに数値を割り当て `firstBatesNumber` て、初期ベイツ番号を設定 `AssemblerOptionSpec` します。

1. 入力PDFドキュメントをアセンブリします。

   オブジェクト `AssemblerServiceClient` のメソッドを `invoke` 呼び出し、次の値を渡します。

   * DDXドキ `BLOB` ュメントを表すオブジェクトです。
   * 入力PDF `MyMapOf_xsd_string_To_xsd_anyType` ドキュメントを含むオブジェクトです。 そのキーはPDFソースファイルの名前と一致し、その値はそれらのファイルに対応するオブジ `BLOB` ェクトである必要があります。
   * 実行時 `AssemblerOptionSpec` のオプションを指定するオブジェクトです。
   このメ `invoke` ソッドは、ジョ `AssemblerResult` ブの結果と発生した例外を含むオブジェクトを返します。

1. 結果を抽出します。

   新しく作成したPDFドキュメントを取得するには、次の操作を実行します。

   * 結果のPDFドキュ `AssemblerResult` メントを含むオ `documents` ブジェクトのフ `Map` ィールドにアクセスします。
   * 結果のドキュメント `Map` の名前と一致するキーが見つかるまで、オブジェクトを繰り返し処理します。 次に、その配列メンバーのをにキャス `value` トしま `BLOB`す。
   * PDFドキュメントを表すバイナリデータを抽出するには、そのオブジェクトのプロパ `BLOB` ティにアクセス `MTOM` します。 PDFファイルに書き出し可能なバイト配列を返します。

**関連トピック**

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
