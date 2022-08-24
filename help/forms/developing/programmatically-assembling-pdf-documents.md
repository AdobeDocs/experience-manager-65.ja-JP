---
title: PDF ドキュメントをプログラムで組み立てる
seo-title: Programmatically Assembling PDF Documents
description: Assembler サービス API および Java API と web サービス API を使用して、複数の PDF ドキュメントを 1 つの PDF ドキュメントにアセンブリします。
seo-description: Use the Assembler service API to assemble multiple PDF documents into a single PDF document using the Java API and the Web Service API.
uuid: aa3f8f39-1fbc-48d0-82ff-6caaadf125fc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: ebe8136b-2a79-4035-b9d5-aa70a5bbd4af
role: Developer
exl-id: 7d6fd230-e477-4286-9fb3-18a3474e3e48
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2124'
ht-degree: 100%

---

# PDF ドキュメントをプログラムで組み立てる {#programmatically-assembling-pdf-documents}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

Assembler サービス API を使用して、複数の PDF ドキュメントを 1 つの PDF ドキュメントにアセンブリすることができます。次のイラストは、3 つの PDF ドキュメントを 1 つの PDF ドキュメントに統合する様子を示しています。

![pa_pa_document_assembly](assets/pa_pa_document_assembly.png)

2 つ以上の PDF ドキュメントを 1 つの PDF ドキュメントにアセンブリするには、DDX ドキュメントが必要です。DDX ドキュメントは、Assembler サービスが生成する PDF ドキュメントを記述します。つまり、DDX ドキュメントは Assembler サービスに対して、実行するアクションを指示します。

この説明では、次の DDX ドキュメントが使用されていると仮定します。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     <PDF result="out.pdf">
         <PDF source="map.pdf" />
         <PDF source="directions.pdf" />
     </PDF>
 </DDX>
```

この DDX ドキュメントは、*map.pdf* および *directions.pdf* と名前が付いた 2 つの PDF ドキュメントを単一の PDF ドキュメントに統合します。

>[!NOTE]
>
>PDF ドキュメントを分解する DDX ドキュメントを確認するには、[プログラムによる PDF ドキュメントの分解](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)を参照してください。

>[!NOTE]
>
>Assembler サービスについて詳しくは、[AEM Forms サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

>[!NOTE]
>
>DDX ドキュメントについて詳しくは、[Assembler サービスと DDX リファレンス](https://www.adobe.com/go/learn_aemforms_ddx_63)を参照してください。

## Web サービスを使用して Assembler サービスを呼び出す際の考慮事項 {#considerations-when-invoking-assembler-service-using-web-services}

大きなドキュメントのアセンブリ中にヘッダーとフッターを追加すると、`OutOfMemory` エラーが発生する場合があり、その際はファイルがアセンブリされません。この問題が発生する可能性を減らすには、`DDXProcessorSetting` 要素を DDX ドキュメントに追加します（以下の例に参照）。

`<DDXProcessorSetting name="checkpoint" value="2000" />`

この要素を `DDX` 要素の子として、または `PDF result` 要素の子として追加できます。この設定のデフォルト値は 0（ゼロ）で、チェックポイントがオフになり、DDX は `DDXProcessorSetting` 要素が存在しないかのように動作します。もし `OutOfMemory` エラーが発生した場合は、値を整数値（通常は 500 ～ 5000）に設定しなければならない場合があります。チェックポイントの値が小さいと、チェックポイントが頻繁に行われます。

## 手順の概要 {#summary-of-steps}

複数の PDF ドキュメントから 1 つの PDF ドキュメントをアセンブリするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. PDF Assembler クライアントを作成します。
1. 既存の DDX ドキュメントを参照します。
1. 入力 PDF ドキュメントを参照します。
1. 実行時オプションを設定します。
1. 入力 PDF ドキュメントをアセンブリします。
1. 結果を抽出します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar（AEM Forms が JBoss にデプロイされている場合に必要）
* jbossall-client.jar（AEM Formsが JBoss にデプロイされている場合に必要）

AEM Forms が JBoss 以外のサポート対象の J2EE アプリケーションサーバーにデプロイされている場合は、adobe-utilities.jar ファイルと jbossall-client.jar ファイルを、AEM Forms がデプロイされている J2EE アプリケーションサーバーに固有の JAR ファイルに置き換える必要があります。

**PDF Assembler クライアントの作成**

Assembler 操作をプログラムで実行する前に、Assembler クライアントを作成する必要があります。

**既存の DDX ドキュメントの参照**

DDX ドキュメントを参照して、PDF ドキュメントをアセンブリする必要があります。例えば、このセクションで紹介した DDX ドキュメントについて考えてみましょう。 この DDX ドキュメントは、2 つの PDF ドキュメントを 1 つの PDF ドキュメントに統合するよう Assembler サービスに指示します。

**入力 PDF ドキュメントの参照**

Assembler サービスに渡す入力 PDF ドキュメントを参照します。例えば、Map と Directions という名前の 2 つの入力 PDF ドキュメントを渡す場合は、対応する PDF ファイルを渡す必要があります。

map.pdf ファイルと dorictions.pdf ファイルの両方をコレクションオブジェクトに配置する必要があります。キーの名前は、DDX ドキュメントの PDF ソース属性の値と一致する必要があります。DDX ドキュメント内のキーとソース属性が一致する場合、PDF ファイルの名前は関係ありません。

>[!NOTE]
>
>コレクションオブジェクトを含む `AssemblerResult` オブジェクトは、`invokeDDX` 操作を呼び出す場合に返されます。この操作は、2 つ以上の入力 PDF ドキュメントを Assembler サービスに渡す場合に使用されます。ただし、Assembler サービスに 1 つの入力 PDF のみを渡し、1 つのドキュメントのみが返されるのを想定している場合は、 `invokeOneDocument` 操作を呼び出します。この操作を呼び出すと、1 つのドキュメントが返されます。この操作の使用方法については、[暗号化された PDF ドキュメントのアセンブリ](/help/forms/developing/assembling-encrypted-pdf-documents.md#assembling-encrypted-pdf-documents)を参照してください。

**実行時オプションを設定**

ジョブの実行中に Assembler サービスの動作を制御する実行時オプションを設定できます。例えば、エラーが発生した場合にジョブの処理を続行するよう Assembler サービスに指示するオプションを設定できます。設定できる実行時オプションについて詳しくは、[AEM Forms API リファレンス](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ja)の `AssemblerOptionSpec` のクラス参照を確認してください。

**入力 PDF ドキュメントのアセンブリ**

サービスクライアントを作成し、DDX ファイルを参照し、入力 PDF ドキュメントを格納するコレクションオブジェクトを作成して、実行時オプションを設定すると、DDX 操作を呼び出すことができます。この節で指定した DDX ドキュメントを使用する場合、map.pdf ファイルと direction.pdf ファイルが 1 つの PDF ドキュメントに結合されます。

**結果を抽出**

Assembler サービスは、`AssemblerResult` オブジェクトから取得できる `java.util.Map` オブジェクトを返し、その中には操作結果が含まれています。返された `java.util.Map` オブジェクトには、結果のドキュメントと例外が含まれます。

次のテーブルは、返された `java.util.Map` オブジェクトの中にあるキーの値とオブジェクトタイプの一部をまとめたものです。

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
   <td><p>DDX 結果要素で指定された結果のドキュメントを含みます</p></td>
  </tr>
  <tr>
   <td><p><code><i>documentName</i></code></p></td>
   <td><p><code>Exception</code></p></td>
   <td><p>ドキュメントの例外を含みます</p></td>
  </tr>
  <tr>
   <td><p><code>OutputMapConstants.LOG_NAME</code></p></td>
   <td><p><code>com.adobe.idp.Documen</code></p></td>
   <td><p>ジョブのログを含みます</p></td>
  </tr>
 </tbody>
</table>

**関連項目**

[AEM Forms Java ライブラリファイルの組み込み](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[プログラムによる PDF ドキュメントの分割](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## Java API を使用した PDF ドキュメントのアセンブリ {#assemble-pdf-documents-using-the-java-api}

Assembler Service API（Java）を使用して PDF ドキュメントをアセンブリします。

1. プロジェクトファイルを含めます。

   adobe-livecycle-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. PDF Assembler クライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して `ServiceClientFactory` オブジェクトを渡すことにより、`AssemblerServiceClient` オブジェクトを作成します。

1. 既存の DDX ドキュメントを参照します。

   * コンストラクタを使用し、DDX ファイルの場所を指定する文字列値を渡すことによって、その DDX ドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクターを使用して `java.io.FileInputStream` オブジェクトを渡すことにより、`com.adobe.idp.Document` オブジェクトを作成します。

1. 入力 PDF ドキュメントを参照します。

   * `HashMap` コンストラクターを使用することにより、入力 PDF ドキュメントの格納に使用する `java.util.Map` オブジェクトを作成します。
   * 入力 PDF ドキュメントごとに、コンストラクターを使用して入力 PDF ドキュメントの場所を渡すことにより、`java.io.FileInputStream` オブジェクトを作成します。
   * 入力 PDF ドキュメントごとに、`com.adobe.idp.Document` オブジェクトを作成して、PDF ドキュメントを含む `java.io.FileInputStream` オブジェクトを渡します。
   * 入力ドキュメントごとに、`put` メソッドを呼び出して次の引数を渡すことにより、`java.util.Map` オブジェクトにエントリーを追加します。

      * キー名を表す文字列値。この値は、DDX ドキュメントで指定された PDF ソース要素の値と一致している必要があります。
      * ソース PDF ドキュメントを含む `com.adobe.idp.Document` オブジェクト（または複数のドキュメントを指定する `java.util.List` オブジェクト）。

1. 実行時オプションを設定します。

   * コンストラクタを使用して、実行時オプションを格納する `AssemblerOptionSpec` オブジェクトを作成します。
   * `AssemblerOptionSpec` オブジェクトに属するメソッドを呼び出して、ビジネス要件を満たすよう実行時オプションを設定します。例えば、エラーが発生したときにジョブの処理を続行するように Assembler サービスに指示するには、`AssemblerOptionSpec` オブジェクトの `setFailOnError` メソッドを呼びだして `false` を渡します。

1. 入力 PDF ドキュメントをアセンブリします。

   `AssemblerServiceClient` オブジェクトの `invokeDDX` メソッドを呼び出して、以下の必須値を渡します。

   * 使用する DDX ドキュメントを表す `com.adobe.idp.Document` オブジェクト
   * アセンブリ対象の入力 PDF ファイルを含む `java.util.Map` オブジェクト
   * デフォルトのフォントやジョブのログレベルなどの実行時のオプションを指定する `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` オブジェクト

   `invokeDDX` メソッドは、ジョブの結果と発生した例外を含む `com.adobe.livecycle.assembler.client.AssemblerResult` オブジェクトを返します。

1. 結果を抽出します。

   新しく作成した PDF ドキュメントを取得するには、次のアクションを実行します。

   * `AssemblerResult` オブジェクトの `getDocuments` メソッドを呼び出します。これにより、`java.util.Map` オブジェクトが返されます。
   * 結果の `com.adobe.idp.Document` オブジェクトが見つかるまで `java.util.Map` オブジェクトを反復処理します（DDX ドキュメントで指定された PDF 結果要素を使用して、ドキュメントを取得できます）。
   * `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを呼び出して、PDF ドキュメントを抽出します。

   >[!NOTE]
   >
   >`LOG_LEVEL` がログを生成するように設定されている場合は、`AssemblerResult` オブジェクトの `getJobLog` メソッドを使用してログを抽出できます。

**関連項目**

[クイックスタート（SOAP モード）：Java API を使用した PDF ドキュメントのアセンブリ](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Web サービス API を使用して PDF ドキュメントをアセンブリ {#assemble-pdf-documents-using-the-web-service-api}

Assembler Service API（web サービス）を使用して PDF ドキュメントをアセンブリします。

1. プロジェクトファイルを含めます。

   MTOM を使用する Microsoft .NET プロジェクトを作成します。WSDL 定義 `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1` を使用するようにします。

   >[!NOTE]
   >
   >`localhost` を、AEM Forms をホストするサーバーの IP アドレスに置換します。

1. PDF Assembler クライアントを作成します。

   * デフォルトのコンストラクターを使用して、`AssemblerServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して、`AssemblerServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/AssemblerService?blob=mtom`）。`lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。
   * `AssemblerServiceClient.Endpoint.Binding` フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` フィールドを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `AssemblerServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `AssemblerServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
      * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` をフィールド `BasicHttpBindingSecurity.Security.Mode` に割り当てます。

1. 既存の DDX ドキュメントを参照します。

   * コンストラクターを使用して `BLOB` オブジェクトを作成します。`BLOB` オブジェクトは、DDX ドキュメントを格納するために使用されます。
   * コンストラクターを呼び出し、DDX ドキュメントのファイルの場所とファイルを開くモードを表す文字列値を渡すことによって、`System.IO.FileStream` オブジェクトを作成します。
   * `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することで、バイト配列のサイズを決定できます。
   * バイト配列にストリームデータを入力するには、`System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出し、バイト配列、開始位置、読み取るストリーム長を渡します。
   * `MTOM` プロパティにバイト配列の内容を割り当てることにより、`BLOB` オブジェクトに値を入力します。

1. 入力 PDF ドキュメントを参照します。

   * 入力 PDF ドキュメントごとに、コンストラクタを使用して、`BLOB` オブジェクトを作成します。`BLOB` オブジェクトは、入力 PDF ドキュメントを格納するために使用します。
   * コンストラクターを呼び出し、入力 PDF ドキュメントのファイルの場所とファイルを開くモードを表す文字列値を渡すことにより、`System.IO.FileStream` オブジェクトを作成します。
   * `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することでバイト配列のサイズを決定することができます。
   * `System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出して、バイト配列にストリームデータを入力します。読み取り対象のバイト配列、開始位置、ストリーム長を渡します。
   * `MTOM` フィールドにバイト配列のコンテンツを割り当てて、`BLOB` オブジェクトを入力します。
   * `MyMapOf_xsd_string_To_xsd_anyType` オブジェクトを作成します。このコレクションオブジェクトは、入力 PDF ドキュメントを格納するために使用されます。
   * 入力 PDF ドキュメントごとに、`MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトを作成します。例えば、2 つの入力 PDF ドキュメントを使用する場合、`MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトを作成します。
   * キー名を表す文字列値を `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトの `key` フィールドに割り当てます。この値は、DDX ドキュメントで指定された PDF ソース要素の値と一致する必要があります（入力 PDF ドキュメントごとにこのタスクを実行します）。
   * PDF ドキュメントを格納する `BLOB` オブジェクトを `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトの `value` フィールドに割り当てます。（入力 PDF ドキュメントごとにこのタスクを実行します）。
   * `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトを `MyMapOf_xsd_string_To_xsd_anyType` オブジェクトに追加します。`MyMapOf_xsd_string_To_xsd_anyType` オブジェクトの `Add` メソッドを呼び出し、`MyMapOf_xsd_string_To_xsd_anyType` オブジェクトを渡します。（入力 PDF ドキュメントごとにこのタスクを実行します）。

1. 実行時オプションを設定します。

   * ランタイムオプションを格納する `AssemblerOptionSpec` オブジェクトをコンストラクタで作成します。
   * `AssemblerOptionSpec` オブジェクトに属するデータメンバーに値を割り当てることで、ビジネス要件に応じたランタイムオプションを設定します。例えば、エラーが発生した場合にジョブの処理を続行するように Assembler サービスに指示するには、`false` を `AssemblerOptionSpec` オブジェクトの `failOnError` データメンバーに割り当てます。

1. 入力 PDF ドキュメントをアセンブリします。

   `AssemblerServiceClient` オブジェクトの `invoke` メソッドを呼び出して、次の値を渡します。

   * DDX ドキュメントを表す `BLOB` オブジェクトです。
   * 入力 PDF ドキュメントを格納する `mapItem` 配列です。キーは PDF ソースファイルの名前と一致する必要があり、その値はそれらのファイルに対応する `BLOB` オブジェクトである必要があります。
   * 実行時オプションを指定する `AssemblerOptionSpec` オブジェクトです。

   `invoke` メソッドは、ジョブの結果と発生した可能性のある例外を含む `AssemblerResult` オブジェクトを返します。

1. 結果を抽出します。

   新しく作成した PDF ドキュメントを取得するには、次のアクションを実行します。

   * `AssemblerResult` オブジェクトの `documents` フィールドにアクセスし、結果の PDF ドキュメントを含む `Map` オブジェクトにアクセスします。
   * 結果のドキュメントの名前と一致するキーが見つかるまで、`Map` オブジェクトを繰り返し実行します。次に、その配列メンバーの `value` を `BLOB` にキャストします。
   * PDF ドキュメントを表すバイナリデータを、`BLOB` オブジェクトの `MTOM` プロパティにアクセスして抽出します 。これにより、PDF ファイルに書き出すことができるバイト配列が返されます。

   >[!NOTE]
   >
   >`LOG_LEVEL` がログを生成するように設定されている場合、`AssemblerResult` オブジェクトの `jobLog` データメンバーの値を取得することによりログを抽出できます。

**関連トピック**

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
