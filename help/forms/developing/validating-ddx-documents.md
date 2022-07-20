---
title: DDX ドキュメントの検証
seo-title: Validating DDX Documents
description: Java API と web サービス API を使用して、プログラムによる DDX ドキュメントの検証を行います。
seo-description: Validate a DDX document programmatically using the Java API and the Web Service API.
uuid: da668170-d2e9-4fff-aef5-432a856bd0bd
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 693859b0-a0c3-43f1-95c0-be48a90d7d8d
role: Developer
exl-id: 1f5a2cf3-ef6b-45b4-8fa8-b300e492fee1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '1526'
ht-degree: 100%

---

# DDX ドキュメントの検証 {#validating-ddx-documents}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

Assembler サービスで使用される DDX ドキュメントをプログラムで検証できます。つまり、Assembler サービス API を使用して、DDX ドキュメントが有効かどうかを判断できます。例えば、以前の AEM Forms バージョンからアップグレードした場合に、DDX ドキュメントが有効であることを確認するには、Assembler サービス API を使用してドキュメントを検証します。

>[!NOTE]
>
>Assembler サービスについて詳しくは、[AEM Forms サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

>[!NOTE]
>
>DDX ドキュメントについて詳しくは、[Assembler サービスと DDX リファレンス](https://www.adobe.com/go/learn_aemforms_ddx_63)を参照してください。

## 手順の概要 {#summary-of-steps}

DDX ドキュメントを検証するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Assembler クライアントを作成します。
1. 既存の DDX ドキュメントを参照します。
1. DDX ドキュメントを検証するための実行時オプションを設定します。
1. 検証を実行します。
1. 検証結果をログファイルに保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar（AEM Forms が JBoss にデプロイされている場合に必要）
* jbossall-client.jar（AEM Formsが JBoss にデプロイされている場合に必要）

AEM Forms が JBoss 以外のサポート対象の J2EE アプリケーションサーバーにデプロイされている場合は、adobe-utilities.jar ファイルと jbossall-client.jar ファイルを、AEM Forms がデプロイされている J2EE アプリケーションサーバーに固有の JAR ファイルに置き換える必要があります。

**Assembler クライアントの PDF を作成**

Assembler 操作をプログラムで実行する前に、Assembler サービスクライアントを作成する必要があります。

**既存の DDX ドキュメントの参照**

DDX ドキュメントを検証するには、既存の DDX ドキュメントを参照する必要があります。

**DDX ドキュメントを検証するための実行時オプションの設定**

DDX ドキュメントを検証する場合は、DDX ドキュメントを実行するのではなく、Assembler サービスに DDX ドキュメントを検証するよう指示する特定の実行時オプションを設定する必要があります。また、Assembler サービスがログファイルに書き込む情報の量を増やすこともできます。

**検証の実行**

Assembler サービスクライアントを作成し、DDX ドキュメントを参照し、実行時オプションを設定したら、`invokeDDX` 操作を呼び出して DDX ドキュメントを検証します。DDX ドキュメントを検証する際に、`null` をマップパラメーターとして渡すことができます（通常、このパラメーターは DDX ドキュメントで指定された操作を行うために Assembler が必要とする PDF ドキュメントが格納されます）。

検証に失敗した場合は例外が発生し、DDX ドキュメントが無効な理由を説明する詳細を含むログファイルが `OperationException` インスタンスから取得できます。基本的な XML 解析とスキーマチェックを経て、DDX 仕様に対する検証が実行されます。DDX ドキュメントに含まれるすべてのエラーは、ログに記録されます。

**検証結果をログファイルに保存**

Assembler サービスは、XML ログファイルに書き込むことができる検証結果を返します。Assembler サービスがログファイルに書き込む詳細の量は、設定した実行時オプションによって異なります。

**関連トピック**

[Java API を使用した DDX ドキュメントの検証](#validate-a-ddx-document-using-the-java-api)

[Web サービス API を使用した DDX ドキュメントの検証](#validate-a-ddx-document-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDF ドキュメントをプログラムで組み立てる](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java API を使用した DDX ドキュメントの検証 {#validate-a-ddx-document-using-the-java-api}

Assembler サービス API（Java）を使用して DDX ドキュメントを検証します。

1. プロジェクトファイルを含めます。

   adobe-livecycle-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. PDF Assembler クライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して `ServiceClientFactory` オブジェクトを渡すことにより、`AssemblerServiceClient` オブジェクトを作成します。

1. 既存の DDX ドキュメントを参照します。

   * コンストラクタを使用し、DDX ファイルの場所を指定する文字列値を渡すことによって、その DDX ドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. DDX ドキュメントを検証するための実行時オプションを設定します。

   * コンストラクターを使用して、実行時オプションを格納する `AssemblerOptionSpec` オブジェクトを作成します。
   * DDX ドキュメントの検証を行うよう Assembler サービスに指示する実行時オプションを設定するには、`AssemblerOptionSpec` オブジェクトの setValidateOnly メソッドを呼び出して、`true` を渡します。
   * Assembler サービスがログファイルに書き込む情報量を設定するには、`AssemblerOptionSpec` オブジェクトの `getLogLevel` メソッドを呼び出して、要件を満たす文字列値を渡します。DDX ドキュメントを検証する場合、検証プロセスに役立つより多くの情報をログファイルに書き込みます。その結果、`FINE` または `FINER` という値を渡すことができます。

1. 検証を実行します。

   `AssemblerServiceClient` オブジェクトの `invokeDDX` メソッドを呼び出して、次の値を渡します。

   * DDX ドキュメントを表す `com.adobe.idp.Document` オブジェクトです。
   * 通常 PDF ドキュメントを格納する java.io.Map オブジェクトの値 `null` です。
   * 実行時オプションを指定する `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` オブジェクトです。

   `invokeDDX` メソッドは、DDX ドキュメントが有効かどうかを指定する情報が格納される `AssemblerResult` オブジェクトを返します。

1. 検証結果をログファイルに保存します。

   * `java.io.File` オブジェクトを作成し、ファイル名拡張子が .xml であることを確認します。
   * `AssemblerResult` オブジェクトの `getJobLog` メソッドを呼び出します。このメソッドは、検証情報を含む `com.adobe.idp.Document` インスタンスを返します。
   * `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを呼び出して、`com.adobe.idp.Document` オブジェクトの内容をファイルにコピーします。

   >[!NOTE]
   >
   >DDX ドキュメントが無効な場合、`OperationException` がスローされます。catch ステートメント内で、`OperationException` オブジェクトの `getJobLog` メソッドを呼び出すことができます。

**関連トピック**

[DDX ドキュメントの検証](#validating-ddx-documents)

[クイックスタート（SOAP モード）：Java API を使用した DDX ドキュメントの検証](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-validating-ddx-documents-using-the-java-api)（SOAP モード）

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Web サービス API を使用した DDX ドキュメントの検証 {#validate-a-ddx-document-using-the-web-service-api}

Assembler Service API（web サービス）を使用して DDX ドキュメントを検証します。

1. プロジェクトファイルを含めます。

   MTOM を使用する Microsoft .NET プロジェクトを作成します。次の WSDL 定義を使用していることを確認します。`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`

   >[!NOTE]
   >
   >localhost を Forms サーバーの IP アドレスに置き換えます。

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

   * コンストラクターを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、DDX ドキュメントの保存に使用されます。
   * `System.IO.FileStream` オブジェクトを作成するには、そのコンストラクターを呼び出し、DDX ドキュメントのファイルの場所とファイルを開くモードを表す文字列値を渡します。
   * `System.IO.FileStream` オブジェクトのコンテンツを保存するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することで、バイト配列のサイズを決定できます。
   * バイト配列にストリームデータを入力するには、`System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出し、バイト配列、開始位置、読み取るストリーム長を渡します。
   * `MTOM` プロパティにバイト配列のコンテンツを割り当てて、`BLOB` オブジェクトを入力します。

1. DDX ドキュメントを検証するための実行時オプションを設定します。

   * コンストラクターを使用して、実行時オプションを格納する `AssemblerOptionSpec` オブジェクトを作成します。
   * `AssemblerOptionSpec` オブジェクトの `validateOnly` データメンバーに true の値を割り当てることにより、DDX ドキュメントを検証するように Assembler サービスに指示する実行時オプションを設定します。
   * `AssemblerOptionSpec` オブジェクトの `logLevel` データメンバーに文字列値を割り当てて、Assembler サービスがログファイルに書き込む情報の量を設定します。DDX ドキュメントを検証する場合、検証プロセスに役立つ詳細情報をログファイルに書き込みます。その結果、`FINE` または `FINER` の値を指定できます。設定できる実行時オプションについて詳しくは、[AEM Forms API リファレンス](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ja)の `AssemblerOptionSpec` クラス参照を参照してください。

1. 検証を実行します。

   `AssemblerServiceClient` オブジェクトの `invokeDDX` メソッドを呼び出して、次の値を渡します。

   * DDX ドキュメントを表す `BLOB` オブジェクト。
   * 通常は PDF ドキュメントを格納する `Map` オブジェクトの値 `null`。
   * 実行時オプションを指定する `AssemblerOptionSpec` オブジェクト。

   `invokeDDX` メソッドは、DDX ドキュメントが有効かどうかを示す情報が格納される `AssemblerResult` オブジェクトを返します。

1. 検証結果をログファイルに保存します。

   * コンストラクターを呼び出し、ログファイルの場所とファイルを開くモードを表す文字列値を渡して、`System.IO.FileStream` オブジェクトを作成します。ファイル名の拡張子が .xml であることを確認します。
   * `AssemblerResult` オブジェクトの `jobLog` データメンバーの値を取得して、ログ情報を格納する `BLOB` オブジェクトを作成します。
   * `BLOB` オブジェクトのコンテンツを格納するバイト配列を作成します。`BLOB` オブジェクトの `MTOM` フィールドの値を取得して、バイト配列に入力します。
   * コンストラクターを呼び出し、`System.IO.FileStream` オブジェクトを渡すことによって、`System.IO.BinaryWriter` オブジェクトを作成します。
   * バイト配列のコンテンツを PDF ファイルに書き込むには、`System.IO.BinaryWriter` オブジェクトの `Write` メソッドを呼び出して、バイト配列を渡してください。

   >[!NOTE]
   >
   >DDX ドキュメントが無効な場合、`OperationException` がスローされます。catch ステートメント内で、`OperationException` オブジェクトの `jobLog` メンバーの値を取得できます。

**関連トピック**

[DDX ドキュメントの検証](#validating-ddx-documents)

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
