---
title: DDXドキュメントの検証
seo-title: DDXドキュメントの検証
description: 'null'
seo-description: 'null'
uuid: da668170-d2e9-4fff-aef5-432a856bd0bd
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 693859b0-a0c3-43f1-95c0-be48a90d7d8d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# DDXドキュメントの検証 {#validating-ddx-documents}

Assemblerサービスで使用されるDDXドキュメントをプログラムによって検証できます。 つまり、AssemblerサービスAPIを使用して、DDXドキュメントが有効かどうかを判断できます。 例えば、以前のバージョンのAEM Formsからアップグレードした場合に、DDXドキュメントが有効であることを確認するには、AssemblerサービスAPIを使用してドキュメントを検証します。

>[!NOTE]
>
>For more information about the Assembler service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>DDXドキュメントについて詳しくは、 [Assembler Service and DDX Referenceを参照してください](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 手順の概要 {#summary-of-steps}

DDXドキュメントを検証するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Assemblerクライアントを作成します。
1. 既存のDDXドキュメントを参照します。
1. DDXドキュメントを検証するための実行時オプションを設定します。
1. 検証を実行します。
1. 検証結果をログファイルに保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar（AEM FormsがJBossにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsをJBossにデプロイする場合に必要）

aem formsがJBoss以外のサポート対象のJ2EEアプリケーションサーバーにデプロイされている場合は、adobe-utilities.jarファイルとjbossall-client.jarファイルを、AEM formsのデプロイ先のJ2EEアプリケーションサーバーに固有のJARファイルに置き換える必要があります。

**PDFアセンブラクライアントの作成**

プログラムでAssembler操作を実行する前に、Assemblerサービスクライアントを作成する必要があります。

**既存のDDXドキュメントの参照**

DDXドキュメントを検証するには、既存のDDXドキュメントを参照する必要があります。

**DDXドキュメントを検証するための実行時オプションの設定**

DDXドキュメントを検証する場合は、DDXドキュメントを実行するのではなく、AssemblerサービスにDDXドキュメントを検証するように指示する特定の実行時オプションを設定する必要があります。 また、Assemblerサービスがログファイルに書き込む情報の量を増やすこともできます。

**検証の実行**

Assemblerサービスクライアントを作成し、DDXドキュメントを参照し、実行時オプションを設定した後で、操作を呼び出してDDXドキュ `invokeDDX` メントを検証できます。 DDXドキュメントを検証する際に、mapパラメーターとして渡すことができます（通常、このパラメーターは、DDXドキュメントで指定された操作を実行するためにAssemblerで必要なPDFドキュメントを格納します）。 `null`

検証に失敗すると、例外がスローされ、DDXドキュメントが無効である理由を示す詳細がログファイルに含まれている場合は、そのインスタンスから取得で `OperationException` きます。 基本的なXML解析とスキーマチェックを過ぎると、DDX仕様に対する検証が実行されます。 DDXドキュメント内のエラーはすべてログで指定されます。

**検証結果をログファイルに保存します**

Assemblerサービスは、XMLログファイルに書き込むことができる検証結果を返します。 Assemblerサービスがログファイルに書き込む詳細の量は、設定した実行時オプションによって異なります。

**関連トピック**

[Java APIを使用したDDXドキュメントの検証](#validate-a-ddx-document-using-the-java-api)

[WebサービスAPIを使用したDDXドキュメントの検証](#validate-a-ddx-document-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDFドキュメントのプログラムによるアセンブリ](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java APIを使用したDDXドキュメントの検証 {#validate-a-ddx-document-using-the-java-api}

Assembler Service API(Java)を使用してDDXドキュメントを検証します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-assembler-client.jarなどのクライアントJARファイルを含めます。

1. PDFアセンブラクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `AssemblerServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. 既存のDDXドキュメントを参照します。

   * コンストラ `java.io.FileInputStream` クターを使用し、DDXファイルの場所を指定するstring値を渡して、DDXドキュメントを表すオブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. DDXドキュメントを検証するための実行時オプションを設定します。

   * コンストラクタ `AssemblerOptionSpec` ーを使用して、実行時のオプションを格納するオブジェクトを作成します。
   * オブジェクトのsetValidateOnlyメソッドを呼び出して渡すことで、DDXドキュメントの検証をAssemblerサービスに指示す `AssemblerOptionSpec` る実行時オプションを設定しま `true`す。
   * Assemblerサービスがログファイルに書き込む情報の量を設定するには、オブジェクトのメソッドを呼び出し、 `AssemblerOptionSpec` 必要に応じて `getLogLevel` 文字列値を渡す方法を指定します。 DDXドキュメントを検証する場合は、検証プロセスに役立つ詳細情報をログファイルに書き込む必要があります。 その結果、値またはを渡すことができ `FINE` ます `FINER`。

1. 検証を実行します。

   オブジェクト `AssemblerServiceClient` のメソッドを `invokeDDX` 呼び出し、次の値を渡します。

   * DDXドキ `com.adobe.idp.Document` ュメントを表すオブジェクトです。
   * 通常PDFドキュ `null` メントを格納するjava.io.Mapオブジェクトの値です。
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` object that specifies the run-time options.
   このメ `invokeDDX` ソッドは、DDXドキ `AssemblerResult` ュメントが有効かどうかを指定する情報を含むオブジェクトを返します。

1. 検証結果をログファイルに保存します。

   * Create a `java.io.File` object and ensure that the file name extension is .xml.
   * オブジェクト `AssemblerResult` のメソッドを呼び出 `getJobLog` します。 このメソッドは、検証情報 `com.adobe.idp.Document` を含むインスタンスを返します。
   * Invoke the `com.adobe.idp.Document` object’s `copyToFile` method to copy the contents of the `com.adobe.idp.Document` object to the file.
   >[!NOTE]
   >
   >DDXドキュメントが無効な場合は、がスロー `OperationException` されます。 catch文内で、オブジェクトのメソッドを呼 `OperationException` び出すことがで `getJobLog` きます。

**関連トピック**

[DDXドキュメントの検証](#validating-ddx-documents)

[クイックスタート（SOAPモード）:Java API](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-validating-ddx-documents-using-the-java-api) （SOAPモード）を使用したDDXドキュメントの検証

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## WebサービスAPIを使用したDDXドキュメントの検証 {#validate-a-ddx-document-using-the-web-service-api}

Assembler Service API（Webサービス）を使用してDDXドキュメントを検証します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >localhostをformsサーバーのIPアドレスに置き換えます。

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

1. DDXドキュメントを検証するための実行時オプションを設定します。

   * コンストラクタ `AssemblerOptionSpec` ーを使用して、実行時のオプションを格納するオブジェクトを作成します。
   * オブジェクトのデータメンバーに値trueを割り当ててDDXドキュメントを検証するようにAssemblerサービスに指示する実行時オ `AssemblerOptionSpec` プションを設 `validateOnly` 定します。
   * Assemblerサービスがログファイルに書き込む情報の量を設定するには、オブジェクトのデータメンバーに文字列 `AssemblerOptionSpec` 値を割り当 `logLevel` てます。 ddxドキュメントを検証する場合、検証プロセスに役立つ詳細情報をログファイルに書き込む必要があります。 その結果、またはの値を指定でき `FINE` ます `FINER`。 設定可能なランタイムオプションについて詳しくは、『 `AssemblerOptionSpec` AEM Forms APIリファレンス』のクラス [リファレンスを参照し](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)てください。

1. 検証を実行します。

   オブジェクト `AssemblerServiceClient` のメソッドを `invokeDDX` 呼び出し、次の値を渡します。

   * DDXドキ `BLOB` ュメントを表すオブジェクトです。
   * 通常PDFドキ `null` ュメントを `Map` 格納するオブジェクトの値です。
   * 実行時 `AssemblerOptionSpec` のオプションを指定するオブジェクトです。
   このメ `invokeDDX` ソッドは、DDXドキ `AssemblerResult` ュメントが有効かどうかを指定する情報を含むオブジェクトを返します。

1. 検証結果をログファイルに保存します。

   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、ログファイルの場所とファイルを開くモードを表すstring値を渡します。 ファイル名の拡張子が.xmlであることを確認します。
   * オブジェクト `BLOB` のデータメンバーの値を取得して、ログ情報を格納するオ `AssemblerResult` ブジェクトを `jobLog` 作成します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `BLOB` します。 オブジェクトのフィールドの値を取得して、バイト `BLOB` 配列を設定し `MTOM` ます。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡すことで、バ `System.IO.BinaryWriter` イト配列の内 `Write` 容をPDFファイルに書き込みます。
   >[!NOTE]
   >
   >DDXドキュメントが無効な場合は、がスロー `OperationException` されます。 catchステートメント内では、オブジェクトのメンバの値 `OperationException` を取得でき `jobLog` ます。

**関連トピック**

[DDXドキュメントの検証](#validating-ddx-documents)

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
