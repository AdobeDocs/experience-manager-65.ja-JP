---
title: 暗号化された PDF ドキュメントのアセンブリ
seo-title: Assembling Encrypted PDF Documents
description: Java API および web サービス API を使用して、暗号化された PDF ドキュメントをアセンブリします。
seo-description: Assemble encrypted PDF documents using the Java API and Web Service API.
uuid: d0948ec9-ab67-4fe4-9062-1c4938460b43
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 6d75c7b1-9c0e-47f3-bdb1-61acf16b97f9
role: Developer
exl-id: 2caaca74-640a-4257-a81b-3e8b295cd182
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1659'
ht-degree: 100%

---

# 暗号化された PDF ドキュメントのアセンブリ {#assembling-encrypted-pdf-documents}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

Assembler サービスを使用して、PDF ドキュメントをパスワードで暗号化できます。PDF ドキュメントがパスワードを使用して暗号化されている場合、Adobe Reader または Acrobat で PDF ドキュメントを表示するには、パスワードを指定する必要があります。パスワードを使用して PDF ドキュメントを暗号化するには、PDF ドキュメントの暗号化に必要な暗号化要素の値を DDX ドキュメントに含める必要があります。

この説明では、次の DDX ドキュメントが使用されていると仮定します。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
        <PDF result="EncryptLoan.pdf" encryption="userProtect">
         <PDF source="inDoc" />
     </PDF>
     <PasswordEncryptionProfile name="userProtect" compatibilityLevel="Acrobat7">
         <OpenPassword>AdobeOpen</OpenPassword>
        </PasswordEncryptionProfile>
 </DDX>
```

この DDX ドキュメント内では、source 属性に値 `inDoc` が割り当てられていることに着目してください。Assembler サービスに渡す入力 PDF ドキュメントが 1 つのみで、返されるのも 1 つの PDF ドキュメントであり、`invokeOneDocument` 操作を呼び出す場合は、値 `inDoc` を PDF の source 属性に割り当てます。`invokeOneDocument` 操作を呼び出す際は、`inDoc` 値が、DDX ドキュメントに指定する必要がある事前定義済みキーです。

これに対し、2 つ以上の入力 PDF ドキュメントを Assembler サービスに渡す場合は、`invokeDDX` 操作を呼び出すことができます。この場合、 入力 PDF ドキュメントのファイル名を `source` 属性に割り当てます。

PDF ドキュメントをパスワードを使用して暗号化するために、AEM Forms のインストールに Encryption サービスを含める必要はありません。詳しくは、 [PDF ドキュメントの暗号化および復号化 ](/help/forms/developing/encrypting-decrypting-pdf-documents.md)を参照してください。

>[!NOTE]
>
>Assembler サービスについて詳しくは、[AEM Forms サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

>[!NOTE]
>
>DDX ドキュメントについて詳しくは、[Assembler サービスと DDX リファレンス](https://www.adobe.com/go/learn_aemforms_ddx_63)を参照してください。

## 手順の概要 {#summary-of-steps}

暗号化された PDF ドキュメントをアセンブルするには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. PDF Assembler クライアントを作成します。
1. 既存の DDX ドキュメントを参照します。
1. 保護されていない PDF ドキュメントを参照します。
1. 実行時オプションを設定します。
1. ドキュメントを暗号化します。
1. 暗号化された PDF ドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar（AEM Forms が JBoss にデプロイされている場合に必要）
* jbossall-client.jar（AEM Formsが JBoss にデプロイされている場合に必要）

AEM Forms が JBoss 以外のサポート対象の J2EE アプリケーションサーバーにデプロイされている場合は、adobe-utilities.jar ファイルと jbossall-client.jar ファイルを、AEM Forms がデプロイされている J2EE アプリケーションサーバーに固有の JAR ファイルに置き換える必要があります。すべての AEM Forms JAR ファイルの場所について、詳しくは [AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。

**Assembler クライアントの作成**

Assembler 操作をプログラムで実行する前に、Assembler サービスクライアントを作成する必要があります。

**既存の DDX ドキュメントの参照**

DDX ドキュメントを参照して、PDF ドキュメントをアセンブリする必要があります。例えば、このセクションで紹介した DDX ドキュメントについて考えてみましょう。PDF ドキュメントを暗号化するには、DDX ドキュメントに `PasswordEncryptionProfile` 要素が含まれている必要があります。

**保護されていない PDF ドキュメントの参照**

保護されていない PDF ドキュメントを暗号化するには、PDFドキュメントを参照し、Assembler サービスに渡す必要があります。既に暗号化されている PDF ドキュメントを参照する場合、例外が発生します。

**実行時オプションの設定**

ジョブの実行中に Assembler サービスの動作を制御する実行時オプションを設定できます。例えば、エラーが発生した場合にジョブの処理を続行するよう Assembler サービスに指示するオプションを設定できます。設定できる実行時オプションについて詳しくは、 [AEM Forms API リファレンス](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ja)の `AssemblerOptionSpec` のクラス参照を参照してください。

**ドキュメントを暗号化**

Assembler サービスクライアントを作成し、暗号化情報を含む DDX ドキュメントを参照し、保護されていない PDF ドキュメントを参照し、実行時オプションを設定したら、 `invokeOneDocument` 操作を呼び出します。入力 PDF ドキュメントが 1 つだけ Assembler サービスに渡される（そして 1 つのドキュメントが返される）ので、 `invokeDDX` 操作の代わりに `invokeOneDocument` 操作を使用できます。

**暗号化された PDF ドキュメントを保存**

Assembler サービスに渡される PDF ドキュメントが 1 つだけの場合、Assembler サービスは、コレクションオブジェクトではなく 1 つのドキュメントを返します。つまり、 `invokeOneDocument` 操作を行うと、1 つのドキュメントが返されます。このセクションで参照する DDX ドキュメントには暗号化情報が含まれているので、Assembler サービスはパスワードで暗号化された PDF ドキュメントを返します。

**関連トピック**

[AEM Forms Java ライブラリファイルの組み込み](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDF ドキュメントをプログラムで組み立てる](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java API を使用した暗号化された PDF ドキュメントのアセンブリ {#assemble-an-encrypted-pdf-document-using-the-java-api}

1. プロジェクトファイルを含めます。

   adobe-livecycle-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. Assembler クライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して `ServiceClientFactory` オブジェクトを渡すことにより、`AssemblerServiceClient` オブジェクトを作成します。

1. 既存の DDX ドキュメントを参照します。

   * コンストラクタを使用し、DDX ファイルの場所を指定する文字列値を渡すことによって、その DDX ドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを作成し、`java.io.FileInputStream` オブジェクトを渡します。

1. 保護されていない PDF ドキュメントを参照します。

   * コンストラクターを使用して `java.io.FileInputStream` オブジェクトを作成し、保護されていない PDF ドキュメントの場所を渡します。
   * `com.adobe.idp.Document` オブジェクトを作成して、PDF ドキュメントを含む `java.io.FileInputStream` オブジェクトを渡します。この `com.adobe.idp.Document` オブジェクトが `invokeOneDocument` メソッドに渡されます。

1. 実行時オプションを設定します。

   * コンストラクタを使用して、実行時オプションを格納する `AssemblerOptionSpec` オブジェクトを作成します。
   * `AssemblerOptionSpec` オブジェクトに属するメソッドを呼び出して、ビジネス要件を満たすよう実行時オプションを設定します。例えば、エラーが発生時にジョブの処理を続行するように Assembler サービスに指示するには、`AssemblerOptionSpec` オブジェクトの `setFailOnError` メソッドとパス `false`を呼び出します。

1. ドキュメントを暗号化します。

   `AssemblerServiceClient` オブジェクトの `invokeOneDocument` メソッドを呼び出して、次の値を渡します。

   * DDX ドキュメントを表す `com.adobe.idp.Document` オブジェクト。この DDX ドキュメントに PDF ソース要素用の値 `inDoc` が含まれていることを確認してください。
   * 保護されていない PDF ドキュメントを含む `com.adobe.idp.Document` オブジェクト。
   * デフォルトのフォントやジョブログレベルを含む、実行時のオプションを指定する `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` オブジェクト。

   この `invokeOneDocument` メソッドは、パスワードで暗号化された PDF ドキュメントを含む `com.adobe.idp.Document` オブジェクトを返します。

1. 暗号化された PDF ドキュメントを保存します。

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が .pdf であることを確認します。
   * `Document` オブジェクトの `copyToFile` メソッドを呼び出して、`Document` オブジェクトのコンテンツをファイルにコピーします。必ず `invokeOneDocument` メソッドが返した `Document` オブジェクトを使用していることを確認してください。

**関連トピック**

[クイックスタート（SOAP モード）：Java API を使用した暗号化された PDF ドキュメントのアセンブリ](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-an-encrypted-pdf-document-using-the-java-api)

## Web サービス API を使用した暗号化 PDF ドキュメントのアセンブリ {#assemble-an-encrypted-pdf-document-using-the-web-service-api}

1. プロジェクトファイルを含めます。

   MTOM を使用する Microsoft .NET プロジェクトを作成します。サービスリファレンスを設定する際は、WSDL の定義 `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1` を必ず使用してください。 

   >[!NOTE]
   >
   >`localhost` を AEM Forms をホストするサーバーの IP アドレスに置き換えます。

1. Assembler クライアントを作成します。

   * デフォルトのコンストラクターを使用して `AssemblerServiceClient` オブジェクトを作成します。
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
   * `System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出し、バイト配列、開始位置、読み取るストリーム長を渡すことにより、バイト配列にストリームデータを入力します。
   * `BLOB` オブジェクトを入力するには、`MTOM` フィールドにバイト配列の内容を割り当てます。

1. 保護されていない PDF ドキュメントを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB` オブジェクトは、入力 PDF ドキュメントを格納するために使用します。この `BLOB` オブジェクトは引数として `invokeOneDocument` に渡されます。
   * コンストラクターを呼び出し、入力 PDF ドキュメントのファイルの場所とファイルを開くモードを表す文字列値を渡すことにより、`System.IO.FileStream` オブジェクトを作成します。
   * `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することで、バイト配列のサイズを決定できます。
   * `System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出し、バイト配列、開始位置、読み取るストリーム長を渡すことにより、バイト配列にストリームデータを入力します。
   * `BLOB` オブジェクトを入力するには、`MTOM` フィールドにバイト配列のコンテンツを割り当てます。

1. 実行時オプションを設定します。

   * ランタイムオプションを格納する `AssemblerOptionSpec` オブジェクトをコンストラクタで作成します。
   * `AssemblerOptionSpec` オブジェクトに属するデータメンバーに値を割り当てることで、ビジネス要件に応じたランタイムオプションを設定します。例えば、エラーが発生した場合にジョブの処理を続行するように Assembler サービスに指示するには、 `false` を `AssemblerOptionSpec` オブジェクトの `failOnError` データメンバーに割り当てます。

1. ドキュメントを暗号化します。

   `AssemblerServiceClient` オブジェクトの `invokeOneDocument` メソッドを呼び出して、次の値を渡します。

   * DDX ドキュメントを表す `BLOB` オブジェクト
   * 保護されていない PDF ドキュメントを表す `BLOB` オブジェクト
   * 実行時のオプションを指定する `AssemblerOptionSpec` オブジェクト

   `invokeOneDocument` メソッドは、暗号化された PDF ドキュメントを含む `BLOB` オブジェクトを返します。

1. 暗号化された PDF ドキュメントを保存します。

   * `System.IO.FileStream` オブジェクトを作成するには、コンストラクターを呼び出し、暗号化された PDF ドキュメントのファイルの場所と、ファイルを開くモードを表す文字列値を渡します。
   *  `invokeOneDocument` メソッドが返した `BLOB` オブジェクトのコンテンツを格納するバイト配列を作成します。バイト配列を生成するには、 `BLOB` オブジェクトの `MTOM` データメンバーの値を取得します。
   * コンストラクターを使用して `System.IO.BinaryWriter` オブジェクトを渡すことによって、`System.IO.FileStream` オブジェクトを作成します。
   * `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを呼び出して、バイト配列を渡すことによって、バイト配列の内容を PDF ファイルに書き込みます。

**関連トピック**

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
