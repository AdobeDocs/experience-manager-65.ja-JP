---
title: PDFドキュメントのプログラムによるディスアセンブリ
seo-title: PDFドキュメントのプログラムによるディスアセンブリ
description: 'null'
seo-description: 'null'
uuid: d71cc044-e948-4b7a-b598-b041723b69e9
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8e38a597-5d22-4d83-95fe-4494fb04e4a3
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# PDFドキュメントのプログラムによるディスアセンブリ {#programmatically-disassembling-pdf-documents}

PDFドキュメントをAssemblerサービスに渡すことで、PDFドキュメントをディスアセンブリできます。 通常、このタスクは、PDFドキュメントが元々、多くの個々のドキュメント（明細書の集まりなど）から作成された場合に役立ちます。 次の図では、DocAが複数の結果ドキュメントに分割されています。この場合、ページ上の第1レベル1のブックマークが、新しい結果ドキュメントの開始を示します。

![pd_pd_pdfsfrombookmarks](assets/pd_pd_pdfsfrombookmarks.png)

PDFドキュメントをディスアセンブリするには、要素がDDX `PDFsFromBookmarks` ドキュメント内にあることを確認します。 要素 `PDFsFromBookmarks` は結果の要素で、要素の子要素のみになりま `DDX` す。 複数のドキュメントが生成さ `result` れる可能性があるので、属性がありません。

この要 `PDFsFromBookmarks` 素を使用すると、ソースドキュメント内のレベル1のブックマークごとに1つのドキュメントが生成されます。

この説明の目的で、次のDDXドキュメントが使用されているとします。

```as3
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

>[!NOTE]
>
>この節を読む前に、Assemblerサービスを使用したPDFドキュメントのアセンブリについて詳しく知ることをお勧めします。 (「プログラ [ムによるPDFドキュメントの集成](/help/forms/developing/programmatically-assembling-pdf-documents.md)」を参照)。

>[!NOTE]
>
>単一のPDFドキュメントをAssemblerサービスに渡し、単一のドキュメントを取得する場合は、操作を呼び出すことがで `invokeOneDocument` きます。 ただし、PDFドキュメントをディスアセンブリするには、操作を使用します。1つの入力PDFドキュメントがAssemblerサービスに渡されますが、Assemblerサービスは1つ以上のドキュメントを含むコレクションオブジェクトを返します。 `invokeDDX`

>[!NOTE]
>
>For more information about the Assembler service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>DDXドキュメントについて詳しくは、 [Assembler Service and DDX Referenceを参照してください](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 手順の概要 {#summary-of-steps}

PDFドキュメントをディスアセンブリするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. PDFアセンブラクライアントを作成します。
1. 既存のDDXドキュメントを参照します。
1. ディスアセンブリするPDFドキュメントを参照します。
1. 実行時オプションを設定します。
1. PDFドキュメントのディスアセンブリ
1. 分解されたPDFドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar（AEM FormsがJBossにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsをJBossにデプロイする場合に必要）

aem formsがJBoss以外のサポート対象のJ2EEアプリケーションサーバーにデプロイされている場合は、adobe-utilities.jarおよびjbossall-client.jarを、AEM formsがデプロイされているJ2EEアプリケーションサーバーに固有のJARファイルに置き換える必要があります。

**PDFアセンブラクライアントの作成**

プログラムでAssembler操作を実行する前に、Assemblerサービスクライアントを作成する必要があります。

**既存のDDXドキュメントの参照**

PDFドキュメントをディスアセンブリするには、DDXドキュメントを参照する必要があります。 このDDXドキュメントには、このエレメントが含まれている必要 `PDFsFromBookmarks` があります。

**ディスアセンブリするPDFドキュメントの参照**

PDFドキュメントをディスアセンブリするには、ディスアセンブリ対象のPDFドキュメントを表すPDFファイルを参照します。 Assemblerサービスに渡されると、ドキュメント内のレベル1のブックマークごとに別々のPDFドキュメントが返されます。

**実行時オプションの設定**

ジョブの実行中にAssemblerサービスの動作を制御する実行時オプションを設定できます。 例えば、エラーが発生した場合にジョブの処理を続行するようAssemblerサービスに指示するオプションを設定できます。

**PDFドキュメントのディスアセンブリ**

Assemblerサービスクライアントを作成し、DDXドキュメントを参照し、PDFドキュメントを参照してディスアセンブリし、実行時オプションを設定した後、このメソッドを呼び出してPDFドキュメントをディスアセンブリで `invokeDDX` きます。 DDXドキュメントにPDFドキュメントのディスアセンブリの命令が含まれている場合、Assemblerサービスは、コレクションオブジェクト内でディスアセンブリされたPDFドキュメントを返します。

**分解されたPDFドキュメントの保存**

分解されたすべてのPDFドキュメントは、コレクションオブジェクト内で返されます。 コレクションオブジェクトを繰り返し処理し、各PDFドキュメントをPDFファイルとして保存します。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDFドキュメントのプログラムによるアセンブリ](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java APIを使用したPDFドキュメントのディスアセンブリ {#disassemble-a-pdf-document-using-the-java-api}

Assembler Service API(Java)を使用してPDFドキュメントをディスアセンブリします。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-assembler-client.jarなどのクライアントJARファイルを含めます。

1. PDFアセンブラクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `AssemblerServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. 既存のDDXドキュメントを参照します。

   * コンストラ `java.io.FileInputStream` クターを使用し、DDXファイルの場所を指定するstring値を渡して、DDXドキュメントを表すオブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. ディスアセンブリするPDFドキュメントを参照します。

   * コンストラク `java.util.Map` ターを使用して、入力PDFドキュメントの保存に使用するオブジェクトを作成 `HashMap` します。
   * コンストラク `java.io.FileInputStream` ターを使用し、ディスアセンブリするPDFドキュメントの場所を渡して、オブジェクトを作成します。
   * オブジェクトを `com.adobe.idp.Document` 作成し、ディスアセンブ `java.io.FileInputStream` リするPDFドキュメントを含むオブジェクトを渡します。
   * メソッドを呼び出し、次 `java.util.Map` の引数を渡して、オ `put` ブジェクトにエントリを追加します。

      * キー名を表すstring値です。 この値は、DDXドキュメントで指定されたPDFソース要素の値と一致する必要があります。
      * ディスア `com.adobe.idp.Document` センブルするPDFドキュメントを含むオブジェクトです。

1. 実行時オプションを設定します。

   * コンストラクタ `AssemblerOptionSpec` ーを使用して、実行時のオプションを格納するオブジェクトを作成します。
   * オブジェクトに属するメソッドを呼び出して、ビジネス要件に合わせて実行時のオプションを設定 `AssemblerOptionSpec` します。 例えば、エラーが発生した場合にジョブの処理を続行するようにAssemblerサービスに指示するには、オブジェクトのメソッド `AssemblerOptionSpec` を呼び出して `setFailOnError` 渡してくださ `false`い。

1. PDFドキュメントのディスアセンブリ

   オブジェクト `AssemblerServiceClient` のメソッドを呼 `invokeDDX` び出し、次の必要な値を渡します。

   * 使用す `com.adobe.idp.Document` るDDXドキュメントを表すオブジェクトです
   * ディスア `java.util.Map` センブルするPDFドキュメントを含むオブジェクト
   * デフォ `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` ルトフォントやジョブログレベルなど、実行時のオプションを指定するオブジェクトです
   このメソ `invokeDDX` ッドは、分解さ `com.adobe.livecycle.assembler.client.AssemblerResult` れたPDFドキュメントと発生した例外を含むオブジェクトを返します。

1. 分解されたPDFドキュメントを保存します。

   分解されたPDFドキュメントを取得するには、次の操作を実行します。

   * オブジェクト `AssemblerResult` のメソッドを呼び出 `getDocuments` します。 オブジェクトを返 `java.util.Map` します。
   * 結果のオブジェクト `java.util.Map` が見つかるまで、オブジェクトを繰り返 `com.adobe.idp.Document` します。
   * オブジェクト `com.adobe.idp.Document` のメソッドを呼 `copyToFile` び出してPDFドキュメントを抽出します。

**関連トピック**

[PDFドキュメントのプログラムによるディスアセンブリ](#programmatically-disassembling-pdf-documents)

[クイックスタート（SOAPモード）:Java APIを使用したPDFドキュメントのディスアセンブリ](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-disassembling-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## WebサービスAPIを使用したPDFドキュメントのディスアセンブリ {#disassemble-a-pdf-document-using-the-web-service-api}

Assembler Service API（Webサービス）を使用してPDFドキュメントをディスアセンブリします。

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
   * Create a `System.IO.FileStream` object by invoking its constructor. DDXドキュメントのファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイト配列、開 `System.IO.FileStream` 始位置、ストリ `Read` ーム長を渡すことによって、バイト配列にストリームデータを設定します。
   * オブジェクト `BLOB` にバイト配列の内容をプロ `MTOM` パティに割り当てて、オブジェクトを設定します。

1. ディスアセンブリするPDFドキュメントを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、入力PDFドキュメントの保存に使用されます。 このオ `BLOB` ブジェクトは、引数として `invokeOneDocument` に渡されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、入力PDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイト配列、開 `System.IO.FileStream` 始位置、ストリ `Read` ーム長を渡すことによって、バイト配列にストリームデータを設定します。
   * オブジェクトに `BLOB` バイト配列の内容をフィー `MTOM` ルドに割り当てて、オブジェクトを入力します。
   * Create a `MyMapOf_xsd_string_To_xsd_anyType` object. このコレクションオブジェクトは、ディスアセンブリするPDFを保存するために使用されます。
   * Create a `MyMapOf_xsd_string_To_xsd_anyType_Item` object.
   * キー名を表すstring値をオブジェクトのフィールド `MyMapOf_xsd_string_To_xsd_anyType_Item` に割り当て `key` ます。 この値は、DDXドキュメントで指定されたPDFソース要素の値と一致する必要があります。
   * PDFドキュメント `BLOB` を保存するオブジェクトをオブジェクトのフィー `MyMapOf_xsd_string_To_xsd_anyType_Item` ルドに割り当 `value` てます。
   * オブジェクト `MyMapOf_xsd_string_To_xsd_anyType_Item` をオブジェクトに追加 `MyMapOf_xsd_string_To_xsd_anyType` します。 オブジェクトの `MyMapOf_xsd_string_To_xsd_anyType` メソッドを呼 `Add` び出し、オブジェクトを渡 `MyMapOf_xsd_string_To_xsd_anyType` します。

1. 実行時オプションを設定します。

   * コンストラクタ `AssemblerOptionSpec` ーを使用して、実行時のオプションを格納するオブジェクトを作成します。
   * オブジェクトに属するデータメンバーに値を割り当てて、ビジネス要件に合わせて実行時オプションを設定 `AssemblerOptionSpec` します。 例えば、エラーが発生した場合にジョブの処理を続行するようAssemblerサービスに指示するには、オブジェクトのフ `false` ィールドに `AssemblerOptionSpec` 割り当て `failOnError` ます。

1. PDFドキュメントのディスアセンブリ

   オブジェクト `AssemblerServiceClient` のメソッドを `invokeDDX` 呼び出し、次の値を渡します。

   * PDFドキ `BLOB` ュメントをディスアセンブリするDDXドキュメントを表すオブジェクトです
   * ディスア `MyMapOf_xsd_string_To_xsd_anyType` センブリするPDFドキュメントを含むオブジェクト
   * 実行時 `AssemblerOptionSpec` のオプションを指定するオブジェクト
   このメ `invokeDDX` ソッドは、ジョ `AssemblerResult` ブの結果と発生した例外を含むオブジェクトを返します。

1. 分解されたPDFドキュメントを保存します。

   新しく作成されたPDFドキュメントを取得するには、次の操作を実行します。

   * オブジェクトのフ `AssemblerResult` ィールドにアク `documents` セスします。このフィールドは、ア `Map` センブル解除されたPDFドキュメントを含むオブジェクトです。
   * オブジェクトを繰り返し `Map` 処理し、各結果ドキュメントを取得します。 次に、その配列メンバーをにキャス `value` トします `BLOB`。
   * PDFドキュメントを表すバイナリデータを抽出するには、そのオブジェクトのプロパ `BLOB` ティにアクセス `MTOM` します。 PDFファイルに書き出し可能なバイト配列を返します。

**関連トピック**

[PDFドキュメントのプログラムによるディスアセンブリ](#programmatically-disassembling-pdf-documents)

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
