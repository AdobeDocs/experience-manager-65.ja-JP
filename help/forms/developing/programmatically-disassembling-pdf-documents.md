---
title: PDFドキュメントのプログラムによる分解
seo-title: PDFドキュメントのプログラムによる分解
description: Assemblerサービスを使用して、Java APIとWebサービスAPIを使用して、1つのPDFドキュメントを複数のPDFドキュメントにディスアセンブリします。
seo-description: Assemblerサービスを使用して、Java APIとWebサービスAPIを使用して、1つのPDFドキュメントを複数のPDFドキュメントにディスアセンブリします。
uuid: d71cc044-e948-4b7a-b598-b041723b69e9
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8e38a597-5d22-4d83-95fe-4494fb04e4a3
role: Developer
exl-id: c5e712e0-5c3f-48cd-91cf-fd347222a6b2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1788'
ht-degree: 3%

---

# プログラムによるPDFドキュメントの分解{#programmatically-disassembling-pdf-documents}

**このドキュメントのサンプルと例は、JEE上のAEM Forms環境に限られています。**

PDFドキュメントをAssemblerサービスに渡すことで、PDFドキュメントをディスアセンブリできます。 通常、このタスクは、PDFドキュメントが多数の個々のドキュメント（ステートメントのコレクションなど）から最初に作成された場合に役立ちます。 次の図では、DocAが複数の結果ドキュメントに分割されています。この場合、ページの第1レベル1のブックマークで、新しい結果ドキュメントの開始を示します。

![pd_pd_pdfsfrombookmarks](assets/pd_pd_pdfsfrombookmarks.png)

PDFドキュメントをディスアセンブリするには、DDXドキュメント内に`PDFsFromBookmarks`要素が配置されていることを確認します。 `PDFsFromBookmarks`要素は結果の要素で、`DDX`要素の子要素のみにできます。 `result`属性がないのは、複数のドキュメントが生成される可能性があるからです。

`PDFsFromBookmarks`要素を使用すると、ソースドキュメント内のレベル1のブックマークごとに1つのドキュメントが生成されます。

この説明では、次のDDXドキュメントが使用されているとします。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

>[!NOTE]
>
>この節を読む前に、Assemblerサービスを使用したPDFドキュメントのアセンブリについて理解しておくことをお勧めします。 （[PDFドキュメントのプログラムによるアセンブリ](/help/forms/developing/programmatically-assembling-pdf-documents.md)を参照）。

>[!NOTE]
>
>1つのPDFドキュメントをAssemblerサービスに渡して1つのドキュメントを取り戻す場合は、`invokeOneDocument`操作を呼び出すことができます。 ただし、PDFドキュメントをディスアセンブリする場合は、`invokeDDX`操作を使用します。1つの入力PDFドキュメントがAssemblerサービスに渡されますが、Assemblerサービスは1つ以上のドキュメントを含むコレクションオブジェクトを返します。

>[!NOTE]
>
>Assemblerサービスについて詳しくは、『AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)向けサービスリファレンス』を参照してください。[

>[!NOTE]
>
>DDXドキュメントについて詳しくは、『[AssemblerサービスとDDXリファレンス](https://www.adobe.com/go/learn_aemforms_ddx_63)』を参照してください。

## 手順の概要{#summary-of-steps}

PDFドキュメントをディスアセンブリするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. PDFアセンブラークライアントを作成します。
1. 既存のDDXドキュメントの参照
1. ディスアセンブリするPDFドキュメントの参照。
1. 実行時オプションを設定します。
1. PDFドキュメントのディスアセンブリ。
1. アセンブリ解除したPDFドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用する場合は、プロキシファイルを必ず含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(AEM FormsをJBossにデプロイする場合に必要)
* jbossall-client.jar(AEM FormsをJBossにデプロイする場合に必要)

AEM FormsがJBoss以外のサポート対象のJ2EEアプリケーションサーバーにデプロイされている場合は、adobe-utilities.jarとjbossall-client.jarを、AEM FormsがデプロイされているJ2EEアプリケーションサーバーに固有のJARファイルに置き換える必要があります。

**PDFアセンブラークライアントの作成**

プログラムでAssembler操作を実行する前に、Assemblerサービスクライアントを作成する必要があります。

**既存のDDXドキュメントの参照**

PDFドキュメントをディスアセンブリするには、DDXドキュメントを参照する必要があります。 このDDXドキュメントには、`PDFsFromBookmarks`要素が含まれている必要があります。

**ディスアセンブリするPDFドキュメントの参照**

PDFドキュメントをディスアセンブリするには、ディスアセンブリするPDFドキュメントを表すPDFファイルを参照します。 Assemblerサービスに渡されると、ドキュメント内のレベル1のブックマークごとに個別のPDFドキュメントが返されます。

**実行時オプションの設定**

ジョブの実行中にAssemblerサービスの動作を制御する実行時オプションを設定できます。 例えば、エラーが発生した場合にジョブの処理を続行するようAssemblerサービスに指示するオプションを設定できます。

**PDFドキュメントのディスアセンブリ**

Assemblerサービスクライアントを作成し、DDXドキュメントを参照し、PDFドキュメントを参照してアセンブルを解除し、実行時オプションを設定した後、`invokeDDX`メソッドを呼び出してPDFドキュメントをディスアセンブリできます。 DDXドキュメントにPDFドキュメントのディスアセンブリの命令が含まれている場合、Assemblerサービスはコレクションオブジェクト内でアセンブル解除されたPDFドキュメントを返します。

**分解したPDFドキュメントの保存**

アセンブリが解除されたPDFドキュメントはすべて、コレクションオブジェクト内で返されます。 コレクションオブジェクトを繰り返し処理し、各PDFドキュメントをPDFファイルとして保存します。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDFドキュメントのプログラムによるアセンブリ](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java API {#disassemble-a-pdf-document-using-the-java-api}を使用したPDFドキュメントのディスアセンブリ

AssemblerサービスAPI(Java)を使用したPDFドキュメントのディスアセンブリ：

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-assembler-client.jarなどのクライアントJARファイルを含めます。

1. PDFアセンブラークライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して`AssemblerServiceClient`オブジェクトを渡し、`ServiceClientFactory`オブジェクトを作成します。

1. 既存のDDXドキュメントの参照

   * コンストラクターを使用し、DDXファイルの場所を指定する文字列値を渡して、DDXドキュメントを表す`java.io.FileInputStream`オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. ディスアセンブリするPDFドキュメントの参照。

   * `HashMap`コンストラクターを使用して、入力PDFドキュメントの格納に使用する`java.util.Map`オブジェクトを作成します。
   * コンストラクターを使用し、ディスアセンブリするPDFドキュメントの場所を渡すことで、`java.io.FileInputStream`オブジェクトを作成します。
   * `com.adobe.idp.Document`オブジェクトを作成し、ディスアセンブリするPDFドキュメントを含む`java.io.FileInputStream`オブジェクトを渡します。
   * `put`メソッドを呼び出し、次の引数を渡して、`java.util.Map`オブジェクトにエントリを追加します。

      * キー名を表すstring値です。 この値は、DDXドキュメントで指定されたPDFソース要素の値と一致する必要があります。
      * ディスアセンブリするPDFドキュメントを含む`com.adobe.idp.Document`オブジェクト。

1. 実行時オプションを設定します。

   * コンストラクターを使用して、実行時オプションを格納する`AssemblerOptionSpec`オブジェクトを作成します。
   * `AssemblerOptionSpec`オブジェクトに属するメソッドを呼び出して、ビジネス要件に合った実行時オプションを設定します。 例えば、エラーが発生したときにジョブの処理を続行するようにAssemblerサービスに指示するには、`AssemblerOptionSpec`オブジェクトの`setFailOnError`メソッドを呼び出し、`false`を渡します。

1. PDFドキュメントのディスアセンブリ。

   `AssemblerServiceClient`オブジェクトの`invokeDDX`メソッドを呼び出し、次の必須値を渡します。

   * 使用するDDXドキュメントを表す`com.adobe.idp.Document`オブジェクト
   * ディスアセンブリするPDFドキュメントを含む`java.util.Map`オブジェクト
   * デフォルトのフォントやジョブのログレベルを含む、実行時のオプションを指定する`com.adobe.livecycle.assembler.client.AssemblerOptionSpec`オブジェクト

   `invokeDDX`メソッドは、分解されたPDFドキュメントと発生した例外を含む`com.adobe.livecycle.assembler.client.AssemblerResult`オブジェクトを返します。

1. アセンブリ解除したPDFドキュメントを保存します。

   分解されたPDFドキュメントを取得するには、次の操作を実行します。

   * `AssemblerResult`オブジェクトの`getDocuments`メソッドを呼び出します。 `java.util.Map`オブジェクトを返します。
   * `java.util.Map`オブジェクトを繰り返し処理して、結果の`com.adobe.idp.Document`オブジェクトを見つけます。
   * `com.adobe.idp.Document`オブジェクトの`copyToFile`メソッドを呼び出して、PDFドキュメントを抽出します。

**関連トピック**

[PDFドキュメントのプログラムによる分解](#programmatically-disassembling-pdf-documents)

[クイックスタート（SOAPモード）:Java APIを使用したPDFドキュメントのディスアセンブリ](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-disassembling-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## WebサービスAPI {#disassemble-a-pdf-document-using-the-web-service-api}を使用したPDFドキュメントのディスアセンブリ

AssemblerサービスAPI（Webサービス）を使用してPDFドキュメントをディスアセンブリする

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
   * コンストラクターを呼び出して、`System.IO.FileStream`オブジェクトを作成します。 DDXドキュメントのファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得することで、バイト配列のサイズを判断できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことによって、バイト配列にストリームデータを入力します。
   * `BLOB`オブジェクトの`MTOM`プロパティにバイト配列の内容を割り当てて、オブジェクトを設定します。

1. ディスアセンブリするPDFドキュメントの参照。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、入力PDFドキュメントの保存に使用されます。 この`BLOB`オブジェクトは、引数として`invokeOneDocument`に渡されます。
   * コンストラクターを呼び出し、入力PDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得することで、バイト配列のサイズを判断できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことによって、バイト配列にストリームデータを入力します。
   * `BLOB`オブジェクトの`MTOM`フィールドにバイト配列の内容を割り当てて、オブジェクトを設定します。
   * `MyMapOf_xsd_string_To_xsd_anyType`オブジェクトを作成します。 このコレクションオブジェクトは、ディスアセンブリするPDFを保存するために使用されます。
   * `MyMapOf_xsd_string_To_xsd_anyType_Item`オブジェクトを作成します。
   * `MyMapOf_xsd_string_To_xsd_anyType_Item`オブジェクトの`key`フィールドに、キー名を表すstring値を割り当てます。 この値は、DDXドキュメントで指定されたPDFソース要素の値と一致する必要があります。
   * PDFドキュメントを格納する`BLOB`オブジェクトを`MyMapOf_xsd_string_To_xsd_anyType_Item`オブジェクトの`value`フィールドに割り当てます。
   * `MyMapOf_xsd_string_To_xsd_anyType_Item`オブジェクトを`MyMapOf_xsd_string_To_xsd_anyType`オブジェクトに追加します。 `MyMapOf_xsd_string_To_xsd_anyType`オブジェクト&#39; `Add`メソッドを呼び出して、`MyMapOf_xsd_string_To_xsd_anyType`オブジェクトを渡します。

1. 実行時オプションを設定します。

   * コンストラクターを使用して、実行時オプションを格納する`AssemblerOptionSpec`オブジェクトを作成します。
   * `AssemblerOptionSpec`オブジェクトに属するデータメンバーに値を割り当てて、ビジネス要件に合った実行時オプションを設定します。 例えば、エラーが発生したときにジョブの処理を続行するようにAssemblerサービスに指示するには、`false`を`AssemblerOptionSpec`オブジェクトの`failOnError`フィールドに割り当てます。

1. PDFドキュメントのディスアセンブリ。

   `AssemblerServiceClient`オブジェクトの`invokeDDX`メソッドを呼び出し、次の値を渡します。

   * PDFドキュメントをディスアセンブリするDDXドキュメントを表す`BLOB`オブジェクト
   * ディスアセンブリするPDFドキュメントを含む`MyMapOf_xsd_string_To_xsd_anyType`オブジェクト
   * 実行時オプションを指定する`AssemblerOptionSpec`オブジェクト

   `invokeDDX`メソッドは、ジョブの結果と発生した例外を含む`AssemblerResult`オブジェクトを返します。

1. アセンブリ解除したPDFドキュメントを保存します。

   新しく作成したPDFドキュメントを取得するには、次の操作を実行します。

   * `AssemblerResult`オブジェクトの`documents`フィールドにアクセスします。これは、分解されたPDFドキュメントを含む`Map`オブジェクトです。
   * `Map`オブジェクトを繰り返し処理して、各結果ドキュメントを取得します。 次に、配列メンバの`value`を`BLOB`にキャストします。
   * `BLOB`オブジェクトの`MTOM`プロパティにアクセスして、PDFドキュメントを表すバイナリデータを抽出します。 PDFファイルに書き出すことができるバイトの配列を返します。

**関連トピック**

[PDFドキュメントのプログラムによる分解](#programmatically-disassembling-pdf-documents)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
