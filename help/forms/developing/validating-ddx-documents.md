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


# DDXドキュメントを検証中{#validating-ddx-documents}

Assemblerサービスで使用されるDDXドキュメントをプログラムによって検証できます。 つまり、AssemblerサービスAPIを使用して、DDXドキュメントが有効かどうかを判断できます。 例えば、以前のAEM Formsバージョンからアップグレードした場合に、DDXドキュメントが有効であることを確認するには、Assembler Service APIを使用して検証できます。

>[!NOTE]
>
>Assemblerサービスについて詳しくは、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

>[!NOTE]
>
>DDXドキュメントについて詳しくは、「[Assembler Service and DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63)」を参照してください。

## 手順{#summary-of-steps}の概要

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

Assemblerサービスクライアントの作成後、DDXドキュメントを参照し、実行時オプションを設定した後、`invokeDDX`操作を呼び出してDDXドキュメントを検証できます。 DDXドキュメントを検証する場合、`null`をmapパラメーターとして渡すことができます(通常、このパラメーターには、DDXドキュメントで指定された操作の実行にアセンブラが必要とするPDFドキュメントが格納されます)。

検証に失敗すると、例外がスローされ、DDXドキュメントが無効である理由を`OperationException`インスタンスから取得できる理由をログファイルに示します。 基本的なXML解析とスキーマチェックの完了後、DDX仕様に対する検証が実行されます。 DDXドキュメントにあるすべてのエラーは、ログに記録されます。

**検証結果をログファイルに保存する**

Assemblerサービスは、XMLログファイルに書き込むことができる検証結果を返します。 Assemblerサービスがログファイルに書き込む詳細の量は、設定した実行時のオプションによって異なります。

**関連トピック**

[Java APIを使用したDDXドキュメントの検証](#validate-a-ddx-document-using-the-java-api)

[WebサービスAPIを使用したDDXドキュメントの検証](#validate-a-ddx-document-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[プログラムによるPDFドキュメントのアセンブリ](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java API {#validate-a-ddx-document-using-the-java-api}を使用したDDXドキュメントの検証

Assembler Service API(Java)を使用してDDXドキュメントを検証します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-assembler-client.jarなどのクライアントJARファイルを含めます。

1. PDFアセンブラクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用し、`AssemblerServiceClient`オブジェクトを渡して、`ServiceClientFactory`オブジェクトを作成します。

1. 既存のDDXドキュメントの参照。

   * コンストラクターを使用し、DDXファイルの場所を指定する文字列値を渡して、DDXドキュメントを表す`java.io.FileInputStream`オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. DDXドキュメントを検証するための実行時オプションを設定します。

   * コンストラクターを使用して、実行時オプションを格納する`AssemblerOptionSpec`オブジェクトを作成します。
   * `AssemblerOptionSpec`オブジェクトのsetValidateOnlyメソッドを呼び出し、`true`を渡すことで、DDXドキュメントの検証をAssemblerサービスに指示する実行時オプションを設定します。
   * Assemblerサービスがログファイルに書き込む情報の量を設定するには、`AssemblerOptionSpec`オブジェクトの`getLogLevel`メソッドを呼び出し、必要に応じて文字列値を渡します。 DDXドキュメントを検証する場合、検証プロセスに役立つ詳細情報をログファイルに書き込む必要があります。 その結果、`FINE`または`FINER`の値を渡すことができます。

1. 検証を実行します。

   `AssemblerServiceClient`オブジェクトの`invokeDDX`メソッドを呼び出し、次の値を渡します。

   * DDXドキュメントを表す`com.adobe.idp.Document`オブジェクトです。
   * 通常PDFドキュメントを格納するjava.io.Mapオブジェクトの値`null`です。
   * 実行時オプションを指定する`com.adobe.livecycle.assembler.client.AssemblerOptionSpec`オブジェクト。

   `invokeDDX`メソッドは、DDXドキュメントが有効かどうかを指定する情報を含む`AssemblerResult`オブジェクトを返します。

1. 検証結果をログファイルに保存します。

   * `java.io.File`オブジェクトを作成し、ファイル名の拡張子が.xmlであることを確認します。
   * `AssemblerResult`オブジェクトの`getJobLog`メソッドを呼び出します。 このメソッドは、検証情報を含む`com.adobe.idp.Document`インスタンスを返します。
   * `com.adobe.idp.Document`オブジェクトの`copyToFile`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトの内容をファイルにコピーします。

   >[!NOTE]
   >
   >DDXドキュメントが無効な場合は、`OperationException`がスローされます。 catchステートメント内で、`OperationException`オブジェクトの`getJobLog`メソッドを呼び出すことができます。

**関連トピック**

[DDXドキュメントの検証](#validating-ddx-documents)

[クイック開始（SOAPモード）:Java API](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-validating-ddx-documents-using-the-java-api) （SOAPモード）を使用したDDXドキュメントの検証

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## WebサービスAPI {#validate-a-ddx-document-using-the-web-service-api}を使用したDDXドキュメントの検証

Assembler Service API（Webサービス）を使用してDDXドキュメントを検証します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >localhostをformsサーバーのIPアドレスに置き換えます。

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
   * コンストラクターを呼び出し、DDXドキュメントのファイルの場所と、ファイルを開くモードを表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得して、バイト配列のサイズを決定できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * `BLOB`オブジェクトに`MTOM`プロパティを割り当て、バイト配列の内容を指定します。

1. DDXドキュメントを検証するための実行時オプションを設定します。

   * コンストラクターを使用して、実行時オプションを格納する`AssemblerOptionSpec`オブジェクトを作成します。
   * `AssemblerOptionSpec`オブジェクトの`validateOnly`データメンバーに値trueを割り当てることで、DDXドキュメントの検証をAssemblerサービスに指示する実行時オプションを設定します。
   * Assemblerサービスがログファイルに書き込む情報の量を設定するには、`AssemblerOptionSpec`オブジェクトの`logLevel`データメンバーに文字列値を割り当てます。 DDXドキュメントを検証する場合は、検証プロセスに役立つ詳細情報をログファイルに書き込む必要があります。 その結果、`FINE`または`FINER`の値を指定できます。 設定できる実行時オプションについて詳しくは、[AEM FormsAPIリファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)の`AssemblerOptionSpec`クラス参照を参照してください。

1. 検証を実行します。

   `AssemblerServiceClient`オブジェクトの`invokeDDX`メソッドを呼び出し、次の値を渡します。

   * DDXドキュメントを表す`BLOB`オブジェクトです。
   * 通常PDFドキュメントを格納する`Map`オブジェクトの値`null`です。
   * 実行時オプションを指定する`AssemblerOptionSpec`オブジェクト。

   `invokeDDX`メソッドは、DDXドキュメントが有効かどうかを指定する情報を含む`AssemblerResult`オブジェクトを返します。

1. 検証結果をログファイルに保存します。

   * コンストラクターを呼び出し、ログファイルのファイルの場所とファイルを開くモードを表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。 ファイル名の拡張子が.xmlであることを確認します。
   * `AssemblerResult`オブジェクトの`jobLog`データメンバの値を取得して、ログ情報を格納する`BLOB`オブジェクトを作成します。
   * `BLOB`オブジェクトの内容を格納するバイト配列を作成します。 `BLOB`オブジェクトの`MTOM`フィールドの値を取得して、バイト配列を入力します。
   * コンストラクターを呼び出して`System.IO.FileStream`オブジェクトを渡し、`System.IO.BinaryWriter`オブジェクトを作成します。
   * `System.IO.BinaryWriter`オブジェクトの`Write`メソッドを呼び出し、バイト配列を渡すことで、バイト配列の内容をPDFファイルに書き込みます。

   >[!NOTE]
   >
   >DDXドキュメントが無効な場合は、`OperationException`がスローされます。 catchステートメント内では、`OperationException`オブジェクトの`jobLog`メンバの値を取得できます。

**関連トピック**

[DDXドキュメントの検証](#validating-ddx-documents)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
