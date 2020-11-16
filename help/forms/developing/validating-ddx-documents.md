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
workflow-type: tm+mt
source-wordcount: '1503'
ht-degree: 3%

---


# DDXドキュメントの検証 {#validating-ddx-documents}

Assemblerサービスで使用されるDDXドキュメントをプログラムによって検証できます。 つまり、AssemblerサービスAPIを使用して、DDXドキュメントが有効かどうかを判断できます。 例えば、以前のAEM Formsバージョンからアップグレードした場合に、DDXドキュメントが有効であることを確認するには、Assembler Service APIを使用して検証できます。

>[!NOTE]
>
>For more information about the Assembler service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>DDXドキュメントについて詳しくは、『 [Assembler Service and DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63)』を参照してください。

## 手順の概要 {#summary-of-steps}

DDXドキュメントを検証するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Assemblerクライアントを作成します。
1. 既存のDDXドキュメントの参照。
1. DDXドキュメントを検証するための実行時オプションを設定します。
1. 検証を実行します。
1. 検証結果をログファイルに保存します。

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

プログラムによってAssembler操作を実行する前に、Assemblerサービスクライアントを作成する必要があります。

**既存のDDXドキュメントの参照**

DDXドキュメントを検証するには、既存のDDXドキュメントを参照する必要があります。

**DDXドキュメントを検証するための実行時オプションの設定**

DDXドキュメントを検証する場合は、実行するのではなくDDXドキュメントを検証するようAssemblerサービスに指示する、特定の実行時オプションを設定する必要があります。 また、Assemblerサービスがログファイルに書き込む情報量を増やすこともできます。

**検証の実行**

Assemblerサービスクライアントの作成後、DDXドキュメントを参照し、実行時オプションを設定した後、この `invokeDDX` 操作を呼び出してDDXドキュメントを検証できます。 DDXドキュメントを検証する場合、mapパラメーター `null` として渡すことができます(通常、このパラメーターは、DDXドキュメントで指定された操作の実行にAssemblerが必要とするPDFドキュメントを格納します)。

検証に失敗すると、例外がスローされ、DDXドキュメントが無効である理由をログファイルに示す詳細が `OperationException` インスタンスから取得できます。 基本的なXML解析とスキーマチェックの完了後、DDX仕様に対する検証が実行されます。 DDXドキュメントにあるすべてのエラーは、ログに記録されます。

**検証結果をログファイルに保存する**

Assemblerサービスは、XMLログファイルに書き込むことができる検証結果を返します。 Assemblerサービスがログファイルに書き込む詳細の量は、設定した実行時のオプションによって異なります。

**関連トピック**

[Java APIを使用したDDXドキュメントの検証](#validate-a-ddx-document-using-the-java-api)

[WebサービスAPIを使用したDDXドキュメントの検証](#validate-a-ddx-document-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[プログラムによるPDFドキュメントのアセンブリ](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java APIを使用したDDXドキュメントの検証 {#validate-a-ddx-document-using-the-java-api}

Assembler Service API(Java)を使用してDDXドキュメントを検証します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-assembler-client.jarなどのクライアントJARファイルを含めます。

1. PDFアセンブラクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `AssemblerServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. 既存のDDXドキュメントの参照。

   * コンストラクターを使用し、DDXファイルの場所を指定する文字列値を渡して、DDXドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. DDXドキュメントを検証するための実行時オプションを設定します。

   * コンストラクターを使用して、実行時のオプションを格納する `AssemblerOptionSpec` オブジェクトを作成します。
   * オブジェクトのsetValidateOnlyメソッドを呼び出して渡すことで、DDXドキュメントの検証をAssemblerサービスに指示する実行時 `AssemblerOptionSpec` のオプションを設定 `true`します。
   * Assemblerサービスがログファイルに書き込む情報の量を設定するには、 `AssemblerOptionSpec` オブジェクトの `getLogLevel` メソッドを呼び出し、必要に応じて文字列値を渡します。 DDXドキュメントを検証する場合、検証プロセスに役立つ詳細情報をログファイルに書き込む必要があります。 その結果、値 `FINE` またはを渡すことができ `FINER`ます。

1. 検証を実行します。

   オブジェクトの `AssemblerServiceClient``invokeDDX` メソッドを呼び出し、次の値を渡します。

   * DDXドキュメントを表す `com.adobe.idp.Document` オブジェクトです。
   * 通常PDFドキュメント `null` を格納するjava.io.Mapオブジェクトの値です。
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` object that specifies the run-time options.

   この `invokeDDX` メソッドは、DDXドキュメントが有効かどうかを指定する情報を含む `AssemblerResult` オブジェクトを返します。

1. 検証結果をログファイルに保存します。

   * Create a `java.io.File` object and ensure that the file name extension is .xml.
   * オブジェクトの `AssemblerResult` メソッドを呼び出し `getJobLog` ます。 このメソッドは、検証情報を含む `com.adobe.idp.Document` インスタンスを返します。
   * Invoke the `com.adobe.idp.Document` object’s `copyToFile` method to copy the contents of the `com.adobe.idp.Document` object to the file.

   >[!NOTE]
   >
   >DDXドキュメントが無効な場合、がスロー `OperationException` されます。 catchステートメント内で、 `OperationException` オブジェクトの `getJobLog` メソッドを呼び出すことができます。

**関連トピック**

[DDXドキュメントの検証](#validating-ddx-documents)

[クイック開始（SOAPモード）:Java API](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-validating-ddx-documents-using-the-java-api) （SOAPモード）を使用したDDXドキュメントの検証

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

   * デフォルトのコンストラクターを使用して `AssemblerServiceClient` オブジェクトを作成します。
   * コンストラクターを使用して `AssemblerServiceClient.Endpoint.Address` オブジェクトを作成し `System.ServiceModel.EndpointAddress` ます。 WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/AssemblerService?blob=mtom`)に指定するstring値を渡します。 属性を使用する必要はありません `lc_version` 。 この属性は、サービス参照を作成する際に使用されます。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `AssemblerServiceClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当て `AssemblerServiceClient.ClientCredentials.UserName.UserName`ます。
      * 対応するパスワード値をフィールドに割り当て `AssemblerServiceClient.ClientCredentials.UserName.Password`ます。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当て `BasicHttpBindingSecurity.Security.Mode`ます。

1. 既存のDDXドキュメントの参照。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、DDXドキュメントの格納に使用されます。
   * コンストラクターを呼び出し、DDXドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
   * オブジェクトの `System.IO.FileStream``Read` メソッドを呼び出し、読み取るバイト配列、開始位置およびストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * オブジェクトのプロパティにバイト配列の内容を割り当てて、 `BLOB``MTOM` オブジェクトを入力します。

1. DDXドキュメントを検証するための実行時オプションを設定します。

   * コンストラクターを使用して、実行時のオプションを格納する `AssemblerOptionSpec` オブジェクトを作成します。
   * AssemblerサービスにDDXドキュメントの検証を指示する実行時オプションを設定します。この場合、値trueを `AssemblerOptionSpec` オブジェクトの `validateOnly` データメンバーに割り当てます。
   * Assemblerサービスがログファイルに書き込む情報の量を設定するには、 `AssemblerOptionSpec` オブジェクトの `logLevel` データメンバーに文字列値を割り当てます。 DDXドキュメントを検証する場合は、検証プロセスに役立つ詳細情報をログファイルに書き込む必要があります。 その結果、またはの値を指定でき `FINE` ま `FINER`す。 設定できる実行時オプションについて詳しくは、 `AssemblerOptionSpec` AEM FormsAPIリファレンスの [クラス参照を参照してください](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

1. 検証を実行します。

   オブジェクトの `AssemblerServiceClient``invokeDDX` メソッドを呼び出し、次の値を渡します。

   * DDXドキュメントを表す `BLOB` オブジェクトです。
   * 通常PDFドキュメント `null` を格納する `Map` オブジェクトの値です。
   * 実行時オプションを指定する `AssemblerOptionSpec` オブジェクトです。

   この `invokeDDX` メソッドは、DDXドキュメントが有効かどうかを指定する情報を含む `AssemblerResult` オブジェクトを返します。

1. 検証結果をログファイルに保存します。

   * コンストラクターを呼び出し、ログファイルのファイルの場所とファイルを開くモードを表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。 ファイル名の拡張子が.xmlであることを確認します。
   * オブジェクトの `BLOB` データメンバーの値を取得して、ログ情報を格納する `AssemblerResult``jobLog` オブジェクトを作成します。
   * オブジェクトの内容を格納するバイト配列を作成し `BLOB` ます。 オブジェクトのフィールドの値を取得して、 `BLOB` バイト配列を設定し `MTOM` ます。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡して、バイト配列の内容をPDFファイルに書き込み `System.IO.BinaryWriter` ま `Write` す。

   >[!NOTE]
   >
   >DDXドキュメントが無効な場合、がスロー `OperationException` されます。 catchステートメント内では、 `OperationException` オブジェクトの `jobLog` メンバの値を取得できます。

**関連トピック**

[DDXドキュメントの検証](#validating-ddx-documents)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
