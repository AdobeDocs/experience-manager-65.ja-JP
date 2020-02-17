---
title: PDFドキュメントのプログラムによるアセンブリ
seo-title: PDFドキュメントのプログラムによるアセンブリ
description: 'null'
seo-description: 'null'
uuid: aa3f8f39-1fbc-48d0-82ff-6caaadf125fc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: ebe8136b-2a79-4035-b9d5-aa70a5bbd4af
translation-type: tm+mt
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d

---


# PDFドキュメントのプログラムによるアセンブリ {#programmatically-assembling-pdf-documents}

Assembler Service APIを使用すると、複数のPDFドキュメントを1つのPDFドキュメントにアセンブリできます。 次の図に、3つのPDFドキュメントを1つのPDFドキュメントに結合する例を示します。

![pa_pa_document_assembly](assets/pa_pa_document_assembly.png)

2つ以上のPDFドキュメントを1つのPDFドキュメントにアセンブリするには、DDXドキュメントが必要です。 DDXドキュメントは、Assemblerサービスによって生成されるPDFドキュメントを記述します。 つまり、DDXドキュメントは、実行するアクションをAssemblerサービスに指示します。

この説明の目的で、次のDDXドキュメントが使用されているとします。

```as3
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     <PDF result="out.pdf">
         <PDF source="map.pdf" />
         <PDF source="directions.pdf" />
     </PDF>
 </DDX>
```

このDDXドキュメントは、 *map.pdfとdirections.pdfという名前の2つのPDF* ドキュメントを ** 1つのPDFドキュメントにマージします。

>[!NOTE]
>
>PDFドキュメントをディスアセンブリするDDXドキュメントを表示するには、「PDFドキュメントのプログラムによ [るディスアセンブリ」を参照してくださ](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)い。

>[!NOTE]
>
>For more information about the Assembler service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>DDXドキュメントについて詳しくは、 [Assembler Service and DDX Referenceを参照してください](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## Webサービスを使用してAssemblerサービスを呼び出す場合の考慮事項 {#considerations-when-invoking-assembler-service-using-web-services}

大きなドキュメントのアセンブリ中にヘッダーとフッターを追加すると、エラーが発生し、ファ `OutOfMemory` イルがアセンブリされない場合があります。 この問題が発生する可能性を低くするには、次の例に示すよ `DDXProcessorSetting` うに、DDXドキュメントに要素を追加します。

`<DDXProcessorSetting name="checkpoint" value="2000" />`

この要素は、要素の子として、または要素の子と `DDX` して追加することができ `PDF result` ます。 この設定のデフォルト値は0（ゼロ）で、チェックポイントがオフになり、DDXは要素が存在しない場合と同じよ `DDXProcessorSetting` うに動作します。 エラーが発生した場 `OutOfMemory` 合は、値を整数（通常は500 ～ 5000）に設定する必要があります。 チェックポイントの値を小さくすると、チェックポイントが頻繁に発生します。

## 手順の概要 {#summary-of-steps}

複数のPDFドキュメントから1つのPDFドキュメントをアセンブリするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. PDFアセンブラクライアントを作成します。
1. 既存のDDXドキュメントを参照します。
1. 入力PDFドキュメントを参照します。
1. 実行時オプションを設定します。
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

aem formsがJBoss以外のサポート対象のJ2EEアプリケーションサーバーにデプロイされている場合は、adobe-utilities.jarファイルとjbossall-client.jarファイルを、AEM FormsがデプロイされているJ2EEアプリケーションサーバーに固有のJARファイルに置き換える必要があります。

**PDFアセンブラクライアントの作成**

プログラムによってAssembler操作を実行する前に、Assemblerクライアントを作成する必要があります。

**既存のDDXドキュメントの参照**

PDFドキュメントをアセンブリするには、DDXドキュメントを参照する必要があります。 例えば、この節で紹介したDDXドキュメントについて考えてみましょう。 このDDXドキュメントは、2つのPDFドキュメントを1つのPDFドキュメントにマージするようAssemblerサービスに指示します。

**入力PDFドキュメントの参照**

Assemblerサービスに渡す入力PDFドキュメントを参照します。 例えば、MapとDirectionsという名前の2つの入力PDFドキュメントを渡す場合は、対応するPDFファイルを渡す必要があります。

map.pdfファイルとdirections.pdfファイルは、両方ともコレクションオブジェクトに配置する必要があります。 キーの名前は、DDXドキュメントのPDF source属性の値と一致する必要があります。 DDXドキュメント内のキーとsource属性が一致する場合、PDFファイルの名前は関係ありません。

>[!NOTE]
>
>操作を `AssemblerResult` 呼び出すと、コレクションオブジェクトを含むオブジェクトが返さ `invokeDDX` れます。 この操作は、2つ以上の入力PDFドキュメントをAssemblerサービスに渡す場合に使用されます。 ただし、Assemblerサービスに1つの入力PDFのみを渡し、戻りドキュメントが1つだけ必要な場合は、操作を呼び出 `invokeOneDocument` します。 この操作を呼び出すと、1つのドキュメントが返されます。 この操作の使用について詳しくは、 [Assembling Encrypted PDF Documents](/help/forms/developing/assembling-encrypted-pdf-documents-assembling-encrypted-pdf-documents-assembling.md#assembling-encrypted-pdf-documents)を参照してください。

**実行時オプションの設定**

ジョブの実行中にAssemblerサービスの動作を制御する実行時オプションを設定できます。 例えば、エラーが発生した場合にジョブの処理を続行するようAssemblerサービスに指示するオプションを設定できます。 設定可能なランタイムオプションについて詳しくは、『 `AssemblerOptionSpec` AEM Forms APIリファレンス』のクラス [リファレンスを参照し](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)てください。

**入力PDFドキュメントのアセンブリ**

サービスクライアントを作成し、DDXファイルを参照し、入力PDFドキュメントを格納するコレクションオブジェクトを作成し、実行時オプションを設定した後で、DDX操作を呼び出すことができます。 この節で指定したDDXドキュメントを使用する場合、map.pdfファイルとdirection.pdfファイルが1つのPDFドキュメントにマージされます。

**結果の抽出**

Assemblerサービスは、オブジェクト `java.util.Map` から取得でき、操作結果を含むオ `AssemblerResult` ブジェクトを返します。 返されるオブジ `java.util.Map` ェクトには、結果のドキュメントと例外が含まれます。

次の表に、返されるオブジェクトに配置できるキー値とオブジェクトタイプの概要を示し `java.util.Map` ます。

<table>
 <thead>
  <tr>
   <th><p>キー値</p></th>
   <th><p>オブジェクトタイプ</p></th>
   <th><p>説明</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p><code><i>documentName</i></code></p></td>
   <td><p><code>com.adobe.idp.Document</code></p></td>
   <td><p>DDX結果要素で指定された結果ドキュメントが含まれます</p></td>
  </tr>
  <tr>
   <td><p><code><i>documentName</i></code></p></td>
   <td><p><code>Exception</code></p></td>
   <td><p>ドキュメントの例外を含む</p></td>
  </tr>
  <tr>
   <td><p><code>OutputMapConstants.LOG_NAME</code></p></td>
   <td><p><code>com.adobe.idp.Documen</code></p></td>
   <td><p>ジョブログが含まれます</p></td>
  </tr>
 </tbody>
</table>

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDFドキュメントのプログラムによるディスアセンブリ](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## Java APIを使用したPDFドキュメントのアセンブリ {#assemble-pdf-documents-using-the-java-api}

Assembler Service API(Java)を使用してPDFドキュメントをアセンブリします。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-assembler-client.jarなどのクライアントJARファイルを含めます。

1. PDFアセンブラクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `AssemblerServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. 既存のDDXドキュメントを参照します。

   * コンストラ `java.io.FileInputStream` クターを使用し、DDXファイルの場所を指定するstring値を渡して、DDXドキュメントを表すオブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 入力PDFドキュメントを参照します。

   * コンストラク `java.util.Map` ターを使用して、入力PDFドキュメントの保存に使用するオブジェクトを作成 `HashMap` します。
   * 各入力PDFドキュメントに対して、コンストラク `java.io.FileInputStream` ターを使用し、入力PDFドキュメントの場所を渡して、オブジェクトを作成します。
   * 入力PDFドキュメントごとに、オブジェクトを作成 `com.adobe.idp.Document` し、そのPDFドキュメントを `java.io.FileInputStream` 含むオブジェクトを渡します。
   * 各入力ドキュメントに対して、そのメソッドを呼び出し、次 `java.util.Map` の引数を渡して、オブジ `put` ェクトにエントリを追加します。

      * キー名を表すstring値です。 この値は、DDXドキュメントで指定されたPDFソース要素の値と一致する必要があります。
      * ソースPDF `com.adobe.idp.Document` ドキュメ `java.util.List` ントを含むオブジェクト（または複数のドキュメントを指定するオブジェクト）。

1. 実行時オプションを設定します。

   * コンストラクタ `AssemblerOptionSpec` ーを使用して、実行時のオプションを格納するオブジェクトを作成します。
   * オブジェクトに属するメソッドを呼び出して、ビジネス要件に合わせて実行時のオプションを設定 `AssemblerOptionSpec` します。 例えば、エラーが発生した場合にジョブの処理を続行するようにAssemblerサービスに指示するには、オブジェクトのメソッド `AssemblerOptionSpec` を呼び出して `setFailOnError` 渡してくださ `false`い。

1. 入力PDFドキュメントをアセンブリします。

   オブジェクト `AssemblerServiceClient` のメソッドを呼 `invokeDDX` び出し、次の必要な値を渡します。

   * 使用 `com.adobe.idp.Document` するDDXドキュメントを表すオブジェクト
   * アセンブリ `java.util.Map` 対象の入力PDFファイルを含むオブジェクトです
   * デフォ `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` ルトのフォントやジョブログレベルを含む、実行時のオプションを指定するオブジェクト。
   このメ `invokeDDX` ソッドは、ジョ `com.adobe.livecycle.assembler.client.AssemblerResult` ブの結果と発生した例外を含むオブジェクトを返します。

1. 結果を抽出します。

   新しく作成したPDFドキュメントを取得するには、次の操作を実行します。

   * オブジェクト `AssemblerResult` のメソッドを呼び出 `getDocuments` します。 オブジェクトを返 `java.util.Map` します。
   * 結果のオブジェクト `java.util.Map` が見つかるまで、オブジェクトを繰り返 `com.adobe.idp.Document` します。 （DDXドキュメントで指定されたPDF結果要素を使用して、ドキュメントを取得できます）。
   * オブジェクト `com.adobe.idp.Document` のメソッドを呼 `copyToFile` び出してPDFドキュメントを抽出します。
   >[!NOTE]
   >
   >ログを `LOG_LEVEL` 生成するように設定した場合は、オブジェクトのメソッドを使用してログを `AssemblerResult` 抽出でき `getJobLog` ます。

**関連トピック**

[クイックスタート（SOAPモード）:Java APIを使用したPDFドキュメントのアセンブリ](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## WebサービスAPIを使用したPDFドキュメントのアセンブリ {#assemble-pdf-documents-using-the-web-service-api}

Assembler Service API（Webサービス）を使用してPDFドキュメントをアセンブリします。

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
   * オブジェクトのメソッドを呼び出し、読み取るバイト配列、開 `System.IO.FileStream` 始位置、ストリ `Read` ーム長を渡すことによって、バイト配列にストリームデータを設定します。
   * オブジェクト `BLOB` にバイト配列の内容をプロ `MTOM` パティに割り当てて、オブジェクトを設定します。

1. 入力PDFドキュメントを参照します。

   * 入力PDFドキュメントごとに、コンストラクターを使用 `BLOB` してオブジェクトを作成します。 このオ `BLOB` ブジェクトは、入力PDFドキュメントの保存に使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、入力PDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出して、バイト配列にストリームデ `System.IO.FileStream` ータを入力 `Read` します。 読み取るバイト配列、開始位置およびストリーム長を渡します。
   * オブジェクト `BLOB` にバイト配列の内容を `MTOM` フィールドに割り当てて、オブジェクトを入力します。
   * Create a `MyMapOf_xsd_string_To_xsd_anyType` object. このコレクションオブジェクトは、入力PDFドキュメントの保存に使用されます。
   * 入力PDFドキュメントごとに、オブジェクトを作成 `MyMapOf_xsd_string_To_xsd_anyType_Item` します。 例えば、2つの入力PDFドキュメントを使用する場合は、2つのオブジェクトを作成 `MyMapOf_xsd_string_To_xsd_anyType_Item` します。
   * キー名を表すstring値をオブジェクトのフィールド `MyMapOf_xsd_string_To_xsd_anyType_Item` に割り当て `key` ます。 この値は、DDXドキュメントで指定されたPDFソース要素の値と一致する必要があります。 （入力PDFドキュメントごとにこのタスクを実行します）。
   * PDFドキュメント `BLOB` を保存するオブジェクトをオブジェクトのフィー `MyMapOf_xsd_string_To_xsd_anyType_Item` ルドに割り当 `value` てます。 （入力PDFドキュメントごとにこのタスクを実行します）。
   * オブジェクト `MyMapOf_xsd_string_To_xsd_anyType_Item` をオブジェクトに追加 `MyMapOf_xsd_string_To_xsd_anyType` します。 Invoke the `MyMapOf_xsd_string_To_xsd_anyType` object&#39;s `Add` method and pass the `MyMapOf_xsd_string_To_xsd_anyType` object. （入力PDFドキュメントごとにこのタスクを実行します）。

1. 実行時オプションを設定します。

   * コンストラクタ `AssemblerOptionSpec` ーを使用して、実行時のオプションを格納するオブジェクトを作成します。
   * オブジェクトに属するデータメンバーに値を割り当てて、ビジネス要件に合わせて実行時オプションを設定 `AssemblerOptionSpec` します。 例えば、エラーが発生した場合にジョブの処理を続行するようAssemblerサービスに指示するには、オブジェクトの `false` データメ `AssemblerOptionSpec` ンバーに割り `failOnError` 当てます。

1. 入力PDFドキュメントをアセンブリします。

   オブジェクト `AssemblerServiceClient` のメソッドを `invoke` 呼び出し、次の値を渡します。

   * DDXドキ `BLOB` ュメントを表すオブジェクトです。
   * 入力PDF `mapItem` ドキュメントを含む配列です。 そのキーはPDFソースファイルの名前と一致し、その値はそれらのファイルに対応するオブジ `BLOB` ェクトである必要があります。
   * 実行時 `AssemblerOptionSpec` のオプションを指定するオブジェクトです。
   このメ `invoke` ソッドは、ジョ `AssemblerResult` ブの結果と発生した可能性のある例外を含むオブジェクトを返します。

1. 結果を抽出します。

   新しく作成したPDFドキュメントを取得するには、次の操作を実行します。

   * 結果のPDFドキュ `AssemblerResult` メントを含むオ `documents` ブジェクトのフ `Map` ィールドにアクセスします。
   * 結果のドキュメント `Map` の名前と一致するキーが見つかるまで、オブジェクトを繰り返し処理します。 次に、その配列メンバーのをにキャス `value` トしま `BLOB`す。
   * PDFドキュメントを表すバイナリデータを抽出するには、そのオブジェクトのプロパ `BLOB` ティにアクセス `MTOM` します。 PDFファイルに書き出し可能なバイト配列を返します。
   >[!NOTE]
   >
   >ログを `LOG_LEVEL` 生成するように設定した場合は、オブジェクトのデータメンバの値を取得してログ `AssemblerResult` を抽出で `jobLog` きます。

**関連トピック**

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
