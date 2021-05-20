---
title: DDXドキュメントの検証
seo-title: DDXドキュメントの検証
description: Java APIとWeb Service APIを使用して、DDXドキュメントをプログラムで検証します。
seo-description: Java APIとWeb Service APIを使用して、DDXドキュメントをプログラムで検証します。
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
workflow-type: tm+mt
source-wordcount: '1543'
ht-degree: 3%

---

# DDXドキュメントの検証{#validating-ddx-documents}

**このドキュメントのサンプルと例は、JEE上のAEM Forms環境に限られています。**

Assemblerサービスで使用されるDDXドキュメントをプログラムで検証できます。 つまり、AssemblerサービスAPIを使用して、DDXドキュメントが有効かどうかを判断できます。 例えば、以前のAEM Formsバージョンからアップグレードした場合に、DDXドキュメントが有効であることを確認するには、AssemblerサービスAPIを使用して検証できます。

>[!NOTE]
>
>Assemblerサービスについて詳しくは、『AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)向けサービスリファレンス』を参照してください。[

>[!NOTE]
>
>DDXドキュメントについて詳しくは、『[AssemblerサービスとDDXリファレンス](https://www.adobe.com/go/learn_aemforms_ddx_63)』を参照してください。

## 手順の概要{#summary-of-steps}

DDXドキュメントを検証するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Assemblerクライアントを作成します。
1. 既存のDDXドキュメントの参照
1. DDXドキュメントを検証するための実行時オプションを設定します。
1. 検証を実行します。
1. 検証結果をログファイルに保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用する場合は、プロキシファイルを必ず含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(AEM FormsをJBossにデプロイする場合に必要)
* jbossall-client.jar(AEM FormsをJBossにデプロイする場合に必要)

AEM FormsがJBoss以外のサポート対象のJ2EEアプリケーションサーバーにデプロイされている場合は、adobe-utilities.jarファイルとjbossall-client.jarファイルを、AEM FormsがデプロイされているJ2EEアプリケーションサーバーに固有のJARファイルに置き換える必要があります。

**PDFアセンブラークライアントの作成**

プログラムでAssembler操作を実行する前に、Assemblerサービスクライアントを作成する必要があります。

**既存のDDXドキュメントの参照**

DDXドキュメントを検証するには、既存のDDXドキュメントを参照する必要があります。

**DDXドキュメントを検証するための実行時オプションの設定**

DDXドキュメントを検証する場合は、DDXドキュメントを実行するのではなく、DDXドキュメントを検証するようにAssemblerサービスに指示する特定の実行時オプションを設定する必要があります。 また、Assemblerサービスがログファイルに書き込む情報の量を増やすこともできます。

**検証の実行**

Assemblerサービスクライアントを作成し、DDXドキュメントを参照し、実行時オプションを設定した後、`invokeDDX`操作を呼び出してDDXドキュメントを検証できます。 DDXドキュメントを検証する際に、`null`をmapパラメーターとして渡すことができます（通常、このパラメーターには、DDXドキュメントで指定された操作をAssemblerが実行するために必要なPDFドキュメントが格納されます）。

検証が失敗すると、例外がスローされ、`OperationException`インスタンスからDDXドキュメントが無効な理由を取得できる理由をログファイルに示します。 基本的なXML解析とスキーマチェックを経たら、DDX仕様に対する検証が実行されます。 DDXドキュメント内のすべてのエラーがログに記録されます。

**検証結果をログファイルに保存する**

Assemblerサービスは、XMLログファイルに書き込むことができる検証結果を返します。 Assemblerサービスがログファイルに書き込む詳細の量は、設定した実行時オプションによって異なります。

**関連トピック**

[Java APIを使用したDDXドキュメントの検証](#validate-a-ddx-document-using-the-java-api)

[WebサービスAPIを使用したDDXドキュメントの検証](#validate-a-ddx-document-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDFドキュメントのプログラムによるアセンブリ](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java API {#validate-a-ddx-document-using-the-java-api}を使用したDDXドキュメントの検証

AssemblerサービスAPI(Java)を使用してDDXドキュメントを検証します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-assembler-client.jarなどのクライアントJARファイルを含めます。

1. PDFアセンブラークライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して`AssemblerServiceClient`オブジェクトを渡し、`ServiceClientFactory`オブジェクトを作成します。

1. 既存のDDXドキュメントの参照

   * コンストラクターを使用し、DDXファイルの場所を指定する文字列値を渡して、DDXドキュメントを表す`java.io.FileInputStream`オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. DDXドキュメントを検証するための実行時オプションを設定します。

   * コンストラクターを使用して、実行時オプションを格納する`AssemblerOptionSpec`オブジェクトを作成します。
   * `AssemblerOptionSpec`オブジェクトのsetValidateOnlyメソッドを呼び出して`true`を渡すことで、DDXドキュメントを検証するようAssemblerサービスに指示する実行時オプションを設定します。
   * `AssemblerOptionSpec`オブジェクトの`getLogLevel`メソッドを呼び出し、必要に応じて文字列値を渡すことで、Assemblerサービスがログファイルに書き込む情報の量を設定します。 DDXドキュメントを検証する場合、検証プロセスに役立つ詳細情報をログファイルに書き込む必要があります。 その結果、値`FINE`または`FINER`を渡すことができます。

1. 検証を実行します。

   `AssemblerServiceClient`オブジェクトの`invokeDDX`メソッドを呼び出し、次の値を渡します。

   * DDXドキュメントを表す`com.adobe.idp.Document`オブジェクト。
   * 通常PDFドキュメントを格納するjava.io.Mapオブジェクトの値`null`。
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

[クイックスタート（SOAPモード）:Java API](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-validating-ddx-documents-using-the-java-api) （SOAPモード）を使用したDDXドキュメントの検証

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## WebサービスAPI {#validate-a-ddx-document-using-the-web-service-api}を使用したDDXドキュメントの検証

Assembler Service API（Webサービス）を使用してDDXドキュメントを検証します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >localhostをformsサーバーのIPアドレスに置き換えます。

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
   * コンストラクターを呼び出し、DDXドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得することで、バイト配列のサイズを判断できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことによって、バイト配列にストリームデータを入力します。
   * `BLOB`オブジェクトの`MTOM`プロパティにバイト配列の内容を割り当てて、オブジェクトを設定します。

1. DDXドキュメントを検証するための実行時オプションを設定します。

   * コンストラクターを使用して、実行時オプションを格納する`AssemblerOptionSpec`オブジェクトを作成します。
   * 値trueを`AssemblerOptionSpec`オブジェクトの`validateOnly`データメンバーに割り当てて、DDXドキュメントを検証するようAssemblerサービスに指示する実行時オプションを設定します。
   * `AssemblerOptionSpec`オブジェクトの`logLevel`データメンバーに文字列値を割り当てて、Assemblerサービスがログファイルに書き込む情報の量を設定します。 メソッドを使用してDDXドキュメントを検証する場合、検証プロセスに役立つ詳細情報をログファイルに書き込む必要があります。 その結果、値`FINE`または`FINER`を指定できます。 設定できる実行時オプションについて詳しくは、『[AEM Forms APIリファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)』の`AssemblerOptionSpec`クラス参照を参照してください。

1. 検証を実行します。

   `AssemblerServiceClient`オブジェクトの`invokeDDX`メソッドを呼び出し、次の値を渡します。

   * DDXドキュメントを表す`BLOB`オブジェクト。
   * 通常PDFドキュメントを格納する`Map`オブジェクトの値`null`です。
   * 実行時オプションを指定する`AssemblerOptionSpec`オブジェクト。

   `invokeDDX`メソッドは、DDXドキュメントが有効かどうかを指定する情報を含む`AssemblerResult`オブジェクトを返します。

1. 検証結果をログファイルに保存します。

   * コンストラクターを呼び出し、ログファイルのファイルの場所とファイルを開くモードを表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。 ファイル名の拡張子が.xmlであることを確認します。
   * `AssemblerResult`オブジェクトの`jobLog`データメンバーの値を取得して、ログ情報を格納する`BLOB`オブジェクトを作成します。
   * `BLOB`オブジェクトの内容を格納するバイト配列を作成します。 `BLOB`オブジェクトの`MTOM`フィールドの値を取得して、バイト配列を設定します。
   * コンストラクターを呼び出し、`System.IO.FileStream`オブジェクトを渡して、`System.IO.BinaryWriter`オブジェクトを作成します。
   * `System.IO.BinaryWriter`オブジェクトの`Write`メソッドを呼び出し、バイト配列を渡すことにより、バイト配列の内容をPDFファイルに書き込みます。

   >[!NOTE]
   >
   >DDXドキュメントが無効な場合は、`OperationException`がスローされます。 catchステートメント内で、`OperationException`オブジェクトの`jobLog`メンバの値を取得できます。

**関連トピック**

[DDXドキュメントの検証](#validating-ddx-documents)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
