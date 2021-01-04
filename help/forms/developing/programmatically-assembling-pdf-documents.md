---
title: プログラムによるPDFドキュメントのアセンブリ
seo-title: プログラムによるPDFドキュメントのアセンブリ
description: AssemblerサービスAPIを使用すると、Java APIとWeb Service APIを使用して複数のPDFドキュメントを単一のPDFドキュメントにアセンブリできます。
seo-description: AssemblerサービスAPIを使用すると、Java APIとWeb Service APIを使用して複数のPDFドキュメントを単一のPDFドキュメントにアセンブリできます。
uuid: aa3f8f39-1fbc-48d0-82ff-6caaadf125fc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: ebe8136b-2a79-4035-b9d5-aa70a5bbd4af
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '2138'
ht-degree: 2%

---


# プログラムによるPDFドキュメントのアセンブリ{#programmatically-assembling-pdf-documents}

Assembler Service APIを使用すると、複数のPDFドキュメントを1つのPDFドキュメントにアセンブリできます。 次の図は、3つのPDFドキュメントを1つのPDFドキュメントに結合する様子を示しています。

![pa_pa_ドキュメント_アセンブリ](assets/pa_pa_document_assembly.png)

2つ以上のPDFドキュメントを1つのPDFドキュメントにアセンブリするには、DDXドキュメントが必要です。 DDXドキュメントは、Assemblerサービスが生成するPDFドキュメントを記述します。 つまり、DDXドキュメントは、実行するアクションをAssemblerサービスに指示します。

この説明の目的で、次のDDXドキュメントが使用されているとします。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     <PDF result="out.pdf">
         <PDF source="map.pdf" />
         <PDF source="directions.pdf" />
     </PDF>
 </DDX>
```

このDDXドキュメントは、*map.pdf*&#x200B;および&#x200B;*directions.pdf*&#x200B;という2つのPDFドキュメントを1つのPDFドキュメントにマージします。

>[!NOTE]
>
>PDFドキュメントをディスアセンブリするDDXドキュメントを確認するには、[PDFドキュメントのプログラムによるディスアセンブリ](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)を参照してください。

>[!NOTE]
>
>Assemblerサービスについて詳しくは、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

>[!NOTE]
>
>DDXドキュメントについて詳しくは、「[Assembler Service and DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63)」を参照してください。

## Webサービス{#considerations-when-invoking-assembler-service-using-web-services}を使用してAssemblerサービスを呼び出す場合の考慮事項

大きなドキュメントのアセンブリ中にヘッダーとフッターを追加すると、`OutOfMemory`エラーが発生し、ファイルがアセンブルされない場合があります。 この問題が発生する可能性を低くするには、次の例に示すように、DDXドキュメントに`DDXProcessorSetting`要素を追加します。

`<DDXProcessorSetting name="checkpoint" value="2000" />`

この要素は、`DDX`要素の子として、または`PDF result`要素の子として追加できます。 この設定のデフォルト値は0（ゼロ）で、チェックポイントがオフになり、DDXは`DDXProcessorSetting`要素が存在しないかのように動作します。 `OutOfMemory`エラーが発生した場合は、値を整数（通常は500 ～ 5000）に設定する必要があります。 チェックポイントの値を小さくすると、チェックポイントの頻度が高くなります。

## 手順{#summary-of-steps}の概要

複数のPDFドキュメントから単一のPDFドキュメントをアセンブリするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. PDFアセンブラクライアントを作成します。
1. 既存のDDXドキュメントの参照。
1. 入力PDFドキュメントを参照します。
1. 実行時オプションを設定します。
1. 入力PDFドキュメントをアセンブリします。
1. 結果を抽出します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(AEM FormsがJBossにデプロイされている場合に必要)
* jbossall-client.jar(AEM FormsがJBossにデプロイされている場合に必要)

aem formsがJBoss以外のサポート対象のJ2EEアプリケーションサーバーにデプロイされている場合は、adobe-utilities.jarファイルとjbossall-client.jarファイルを、AEM FormsがデプロイされているJ2EEアプリケーションサーバーに固有のJARファイルに置き換える必要があります。

**PDFアセンブラクライアントの作成**

プログラムによってAssembler操作を実行する前に、Assemblerクライアントを作成する必要があります。

**既存のDDXドキュメントの参照**

PDFドキュメントをアセンブリするには、DDXドキュメントを参照する必要があります。 例えば、この節で紹介したDDXドキュメントについて考えてみましょう。 このDDXドキュメントは、2つのPDFドキュメントを1つのPDFドキュメントに結合するようAssemblerサービスに指示します。

**参照入力PDFドキュメント**

Assemblerサービスに渡す入力PDFドキュメントを参照します。 例えば、MapとDirectionsという名前の2つの入力PDFドキュメントーを渡す場合は、対応するPDFファイルを渡す必要があります。

map.pdfファイルとdirections.pdfファイルは、両方ともコレクションオブジェクトに配置する必要があります。 キーの名前は、DDXドキュメントのPDF source属性の値と一致する必要があります。 DDXドキュメントのkey属性とsource属性が一致した場合、PDFファイルの名前は関係ありません。

>[!NOTE]
>
>`AssemblerResult`操作を呼び出すと、コレクションオブジェクトを含む&lt;a0/>オブジェクトが返されます。 `invokeDDX`この操作は、2つ以上の入力PDFドキュメントをAssemblerサービスに渡す場合に使用します。 ただし、Assemblerサービスに1つの入力PDFのみを渡し、1つの戻りドキュメントのみが必要な場合は、`invokeOneDocument`操作を呼び出します。 この操作を呼び出すと、1つのドキュメントが返されます。 この操作の使用について詳しくは、[暗号化されたPDFドキュメントのアセンブリ](/help/forms/developing/assembling-encrypted-pdf-documents.md#assembling-encrypted-pdf-documents)を参照してください。

**実行時オプションの設定**

ジョブの実行中にAssemblerサービスの動作を制御する実行時オプションを設定できます。 例えば、エラーが発生した場合にジョブの処理を続行するようAssemblerサービスに指示するオプションを設定できます。 設定できる実行時オプションについて詳しくは、[AEM FormsAPIリファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)の`AssemblerOptionSpec`クラス参照を参照してください。

**入力PDFドキュメントのアセンブリ**

サービスクライアントを作成し、DDXファイルを参照し、入力PDFドキュメントを格納するコレクションオブジェクトを作成し、実行時オプションを設定した後で、DDX操作を呼び出すことができます。 この節で指定するDDXドキュメントを使用する場合、map.pdfファイルとdirection.pdfファイルが1つのPDFドキュメントにマージされます。

**結果の抽出**

Assemblerサービスは、`java.util.Map`オブジェクトを返します。このオブジェクトは`AssemblerResult`オブジェクトから取得でき、操作結果を含みます。 返される`java.util.Map`オブジェクトには、結果のドキュメントと例外が含まれます。

次の表に、返される`java.util.Map`オブジェクト内にあるキー値とオブジェクトの種類の一部を示します。

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
   <td><p>DDX結果ドキュメントに指定された結果要素を含みます</p></td>
  </tr>
  <tr>
   <td><p><code><i>documentName</i></code></p></td>
   <td><p><code>Exception</code></p></td>
   <td><p>ドキュメントに対する例外が含まれます</p></td>
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

[プログラムによるPDFドキュメントのディスアセンブリ](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## Java API {#assemble-pdf-documents-using-the-java-api}を使用したPDFドキュメントのアセンブリ

Assembler Service API(Java)を使用してPDFドキュメントをアセンブリします。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-assembler-client.jarなどのクライアントJARファイルを含めます。

1. PDFアセンブラクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用し、`AssemblerServiceClient`オブジェクトを渡して、`ServiceClientFactory`オブジェクトを作成します。

1. 既存のDDXドキュメントの参照。

   * コンストラクターを使用し、DDXファイルの場所を指定する文字列値を渡して、DDXドキュメントを表す`java.io.FileInputStream`オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 入力PDFドキュメントを参照します。

   * `HashMap`コンストラクターを使用して、入力PDFドキュメントの格納に使用する`java.util.Map`オブジェクトを作成します。
   * 各入力PDFドキュメントに対して、コンストラクターを使用し、入力PDFドキュメントーの場所を渡して、`java.io.FileInputStream`オブジェクトを作成します。
   * 入力PDFドキュメントごとに、`com.adobe.idp.Document`オブジェクトを作成し、PDFドキュメントを含む`java.io.FileInputStream`オブジェクトを渡します。
   * 各入力ドキュメントーに対して、`put`メソッドを呼び出し、次の引数を渡して、`java.util.Map`オブジェクトにエントリを追加します。

      * キー名を表すstring値です。 この値は、DDXドキュメントで指定されたPDFソース要素の値と一致する必要があります。
      * ソースPDFドキュメントを含む`com.adobe.idp.Document`オブジェクト(または複数のドキュメントを指定する`java.util.List`オブジェクト)。

1. 実行時オプションを設定します。

   * コンストラクターを使用して、実行時オプションを格納する`AssemblerOptionSpec`オブジェクトを作成します。
   * `AssemblerOptionSpec`オブジェクトに属するメソッドを呼び出して、ビジネス要件に合うように実行時オプションを設定します。 例えば、エラーが発生した場合にジョブの処理を続行するようにAssemblerサービスに指示するには、`AssemblerOptionSpec`オブジェクトの`setFailOnError`メソッドを呼び出し、`false`を渡します。

1. 入力PDFドキュメントをアセンブリします。

   `AssemblerServiceClient`オブジェクトの`invokeDDX`メソッドを呼び出し、次の必須値を渡します。

   * 使用するDDXドキュメントを表す`com.adobe.idp.Document`オブジェクト
   * アセンブリ対象の入力PDFファイルが含まれる`java.util.Map`オブジェクト
   * デフォルトのフォントとジョブログレベルを含む、実行時のオプションを指定する`com.adobe.livecycle.assembler.client.AssemblerOptionSpec`オブジェクト

   `invokeDDX`メソッドは、ジョブの結果と発生した例外を含む`com.adobe.livecycle.assembler.client.AssemblerResult`オブジェクトを返します。

1. 結果を抽出します。

   新しく作成されたPDFドキュメントを取得するには、次の操作を実行します。

   * `AssemblerResult`オブジェクトの`getDocuments`メソッドを呼び出します。 `java.util.Map`オブジェクトを返します。
   * `java.util.Map`オブジェクトを繰り返し処理して、結果の`com.adobe.idp.Document`オブジェクトを見つけます。 (DDXドキュメントで指定されたPDF結果ドキュメントを使用して、要素を取得できます)。
   * `com.adobe.idp.Document`オブジェクトの`copyToFile`メソッドを呼び出してPDFドキュメントを抽出します。

   >[!NOTE]
   >
   >`LOG_LEVEL`がログを生成するように設定されている場合は、`AssemblerResult`オブジェクトの`getJobLog`メソッドを使用してログを抽出できます。

**関連トピック**

[クイック開始（SOAPモード）:Java APIを使用したPDFドキュメントのアセンブリ](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## WebサービスAPI {#assemble-pdf-documents-using-the-web-service-api}を使用してPDFドキュメントをアセンブリ

Assembler Service API（Webサービス）を使用してPDFドキュメントをアセンブリします。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

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
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * `BLOB`オブジェクトに`MTOM`プロパティを割り当て、バイト配列の内容を指定します。

1. 入力PDFドキュメントを参照します。

   * 各入力PDFドキュメントに対して、コンストラクターを使用して`BLOB`オブジェクトを作成します。 `BLOB`オブジェクトは、入力PDFドキュメントの保存に使用されます。
   * コンストラクターを呼び出し、入力PDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得して、バイト配列のサイズを決定できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出して、バイト配列にストリームデータを入力します。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * `BLOB`オブジェクトに、`MTOM`フィールドにバイト配列の内容を割り当てて入力します。
   * `MyMapOf_xsd_string_To_xsd_anyType`オブジェクトを作成します。 このコレクションオブジェクトは、入力PDFドキュメントの格納に使用されます。
   * 入力PDFドキュメントごとに、`MyMapOf_xsd_string_To_xsd_anyType_Item`オブジェクトを作成します。 例えば、2つの入力PDFドキュメントを使用する場合は、2つの`MyMapOf_xsd_string_To_xsd_anyType_Item`オブジェクトを作成します。
   * キー名を表すstring値を`MyMapOf_xsd_string_To_xsd_anyType_Item`オブジェクトの`key`フィールドに割り当てます。 この値は、DDXドキュメントで指定されたPDFソース要素の値と一致する必要があります。 (このタスクは、入力PDFドキュメントごとに実行します)。
   * PDFドキュメントを格納している`BLOB`オブジェクトを`MyMapOf_xsd_string_To_xsd_anyType_Item`オブジェクトの`value`フィールドに割り当てます。 (このタスクは、入力PDFドキュメントごとに実行します)。
   * 追加`MyMapOf_xsd_string_To_xsd_anyType`オブジェクトの`MyMapOf_xsd_string_To_xsd_anyType_Item`オブジェクト。 `MyMapOf_xsd_string_To_xsd_anyType`オブジェクトの`Add`メソッドを呼び出し、`MyMapOf_xsd_string_To_xsd_anyType`オブジェクトを渡します。 (このタスクは、入力PDFドキュメントごとに実行します)。

1. 実行時オプションを設定します。

   * コンストラクターを使用して、実行時オプションを格納する`AssemblerOptionSpec`オブジェクトを作成します。
   * `AssemblerOptionSpec`オブジェクトに属するデータメンバに値を割り当てて、ビジネス要件に合うように実行時オプションを設定します。 例えば、エラーが発生した場合にジョブの処理を続行するようにAssemblerサービスに指示するには、`false`を`AssemblerOptionSpec`オブジェクトの`failOnError`データメンバーに割り当てます。

1. 入力PDFドキュメントをアセンブリします。

   `AssemblerServiceClient`オブジェクトの`invoke`メソッドを呼び出し、次の値を渡します。

   * DDXドキュメントを表す`BLOB`オブジェクトです。
   * 入力PDFドキュメントが含まれる`mapItem`配列です。 このキーはPDFソースファイルの名前と一致する必要があり、その値はそれらのファイルに対応する`BLOB`オブジェクトである必要があります。
   * 実行時オプションを指定する`AssemblerOptionSpec`オブジェクト。

   `invoke`メソッドは、ジョブの結果と発生した可能性のある例外を含む`AssemblerResult`オブジェクトを返します。

1. 結果を抽出します。

   新しく作成されたPDFドキュメントを取得するには、次の操作を実行します。

   * `AssemblerResult`オブジェクトの`documents`フィールドにアクセスします。これは、結果のPDFドキュメントを含む`Map`オブジェクトです。
   * `Map`オブジェクトを繰り返し処理して、結果のドキュメントの名前と一致するキーを見つけます。 次に、その配列メンバーの`value`を`BLOB`にキャストします。
   * `BLOB`オブジェクトの`MTOM`プロパティにアクセスして、PDFドキュメントを表すバイナリデータを抽出します。 PDFファイルに書き出すことができるバイトの配列を返します。

   >[!NOTE]
   >
   >`LOG_LEVEL`がログを生成するように設定されている場合は、`AssemblerResult`オブジェクトの`jobLog`データメンバの値を取得してログを抽出できます。

**関連トピック**

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
