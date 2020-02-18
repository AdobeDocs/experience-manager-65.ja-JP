---
title: 暗号化されたPDFドキュメントのアセンブリ
seo-title: 暗号化されたPDFドキュメントのアセンブリ
description: 'null'
seo-description: 'null'
uuid: d0948ec9-ab67-4fe4-9062-1c4938460b43
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 6d75c7b1-9c0e-47f3-bdb1-61acf16b97f9
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 暗号化されたPDFドキュメントのアセンブリ {#assembling-encrypted-pdf-documents}

Assemblerサービスを使用して、PDFドキュメントをパスワードで暗号化できます。 PDF ドキュメントがパスワードを使用して暗号化されている場合、Adobe Reader または Acrobat で PDF ドキュメントを表示するには、パスワードを指定する必要があります。パスワードを使用して PDF ドキュメントを暗号化するには、PDF ドキュメントの暗号化に必要な暗号化要素の値を DDX ドキュメントに含める必要があります。

この説明の目的で、次のDDXドキュメントが使用されているとします。

```as3
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

このDDXドキュメント内で、source属性に値が割り当てられています `inDoc`。 入力PDFドキュメントが1つだけAssemblerサービスに渡され、1つのPDFドキュメントが返され、操作を呼び出す場合は、PDFソース属性 `invokeOneDocument` に値 `inDoc` を割り当てます。 操作を呼び出す `invokeOneDocument` とき、値 `inDoc` は、DDXドキュメントで指定する必要がある事前定義済みのキーです。

これに対し、2つ以上の入力PDFドキュメントをAssemblerサービスに渡す場合は、操作を呼び出すことがで `invokeDDX` きます。 この場合、入力PDFドキュメントのファイル名を属性に割り当て `source` ます。

PDFドキュメントをパスワードで暗号化する場合、EncryptionサービスをAEM formsのインストールに含める必要はありません。 PDFドキュメ [ントの暗号化と復号化を参照してください](/help/forms/developing/encrypting-decrypting-pdf-documents.md)。

>[!NOTE]
>
>For more information about the Assembler service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>DDXドキュメントについて詳しくは、 [Assembler Service and DDX Referenceを参照してください](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 手順の概要 {#summary-of-steps}

暗号化されたPDFドキュメントをアセンブリするには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. PDFアセンブラクライアントを作成します。
1. 既存のDDXドキュメントを参照します。
1. 保護されていないPDFドキュメントを参照します。
1. 実行時オプションを設定します。
1. ドキュメントを暗号化します。
1. 暗号化されたPDFドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar（AEM FormsがJBossにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsをJBossにデプロイする場合に必要）

aem formsがJBoss以外のサポート対象のJ2EEアプリケーションサーバーにデプロイされている場合は、adobe-utilities.jarファイルとjbossall-client.jarファイルを、AEM formsのデプロイ先のJ2EEアプリケーションサーバーに固有のJARファイルに置き換える必要があります。 For information about the location of all AEM Forms JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Assemblerクライアントの作成**

プログラムでAssembler操作を実行する前に、Assemblerサービスクライアントを作成する必要があります。

**既存のDDXドキュメントの参照**

PDFドキュメントをアセンブリするには、DDXドキュメントを参照する必要があります。 例えば、この節で紹介したDDXドキュメントについて考えてみましょう。 PDFドキュメントを暗号化するには、DDXドキュメントにその要素が含まれている必要が `PasswordEncryptionProfile` あります。

**保護されていないPDFドキュメントの参照**

保護されていないPDFドキュメントを暗号化するには、そのドキュメントを参照し、Assemblerサービスに渡す必要があります。 既に暗号化されているPDFドキュメントを参照する場合は、例外が発生します。

**実行時オプションの設定**

ジョブの実行中にAssemblerサービスの動作を制御する実行時オプションを設定できます。 例えば、エラーが発生した場合にジョブの処理を続行するようAssemblerサービスに指示するオプションを設定できます。 設定可能なランタイムオプションについて詳しくは、『 `AssemblerOptionSpec` AEM Forms APIリファレンス』のクラス [リファレンスを参照し](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)てください。

**ドキュメントの暗号化**

Assemblerサービスクライアントを作成した後、暗号化情報を含むDDXドキュメントを参照し、保護されていないPDFドキュメントを参照し、実行時オプションを設定した後で、操作を呼び出すことがで `invokeOneDocument` きます。 入力PDFドキュメントが1つだけAssemblerサービスに渡されており、1つのドキュメントが返されるので、操作の代わりに操作 `invokeOneDocument` を使用でき `invokeDDX` ます。

**暗号化されたPDFドキュメントの保存**

Assemblerサービスに渡されるPDFドキュメントが1つだけの場合、Assemblerサービスはコレクションオブジェクトではなく1つのドキュメントを返します。 つまり、操作を呼び出すと、1 `invokeOneDocument` つのドキュメントが返されます。 この節で参照するDDXドキュメントには暗号化情報が含まれているので、Assemblerサービスはパスワードで暗号化されたPDFドキュメントを返します。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDFドキュメントのプログラムによるアセンブリ](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java APIを使用した暗号化されたPDFドキュメントのアセンブリ {#assemble-an-encrypted-pdf-document-using-the-java-api}

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-assembler-client.jarなどのクライアントJARファイルを含めます。

1. Assemblerクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `AssemblerServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. 既存のDDXドキュメントを参照します。

   * コンストラ `java.io.FileInputStream` クターを使用し、DDXファイルの場所を指定するstring値を渡して、DDXドキュメントを表すオブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 保護されていないPDFドキュメントを参照します。

   * コンストラク `java.io.FileInputStream` ターを使用し、保護されていないPDFドキュメントの場所を渡して、オブジェクトを作成します。
   * オブジェクト `com.adobe.idp.Document` を作成し、PDFドキュメントを含 `java.io.FileInputStream` むオブジェクトを渡します。 このオ `com.adobe.idp.Document` ブジェクトはメソッドに渡さ `invokeOneDocument` れます。

1. 実行時オプションを設定します。

   * コンストラクタ `AssemblerOptionSpec` ーを使用して、実行時のオプションを格納するオブジェクトを作成します。
   * オブジェクトに属するメソッドを呼び出して、ビジネス要件に合わせて実行時のオプションを設定 `AssemblerOptionSpec` します。 例えば、エラーが発生した場合にジョブの処理を続行するようにAssemblerサービスに指示するには、オブジェクトのメソッド `AssemblerOptionSpec` を呼び出して `setFailOnError` 渡してくださ `false`い。

1. ドキュメントを暗号化します。

   オブジェクト `AssemblerServiceClient` のメソッドを `invokeOneDocument` 呼び出し、次の値を渡します。

   * DDXドキ `com.adobe.idp.Document` ュメントを表すオブジェクトです。 このDDXドキュメントにPDFソース要素の値が含まれ `inDoc` ていることを確認します。
   * 保護され `com.adobe.idp.Document` ていないPDFドキュメントを含むオブジェクトです。
   * デフォ `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` ルトのフォントやジョブログレベルなど、実行時のオプションを指定するオブジェクトです。
   このメソ `invokeOneDocument` ッドは、パスワードで `com.adobe.idp.Document` 暗号化されたPDFドキュメントを含むオブジェクトを返します。

1. 暗号化されたPDFドキュメントを保存します。

   * Create a `java.io.File` object and ensure that the file name extension is .pdf.
   * Invoke the `Document` object’s `copyToFile` method to copy the contents of the `Document` object to the file. メソッドが返したオブジェクト `Document` を使用しているこ `invokeOneDocument` とを確認します。

**関連トピック**

[クイックスタート（SOAPモード）:Java APIを使用した暗号化されたPDFドキュメントのアセンブリ](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-an-encrypted-pdf-document-using-the-java-api)

## WebサービスAPIを使用した暗号化されたPDFドキュメントのアセンブリ {#assemble-an-encrypted-pdf-document-using-the-web-service-api}

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 サービス参照を設定する際は、必ず次のWSDL定義を使用してください。 `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. Assemblerクライアントを作成します。

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
   * オブジェクト `BLOB` にバイト配列の内容を `MTOM` フィールドに割り当てて、オブジェクトを入力します。

1. 保護されていないPDFドキュメントを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、入力PDFドキュメントの保存に使用されます。 このオ `BLOB` ブジェクトは、引数として `invokeOneDocument` に渡されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、入力PDFドキュメントのファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイト配列、開 `System.IO.FileStream` 始位置、ストリ `Read` ーム長を渡すことによって、バイト配列にストリームデータを設定します。
   * オブジェクト `BLOB` にバイト配列の内容を `MTOM` フィールドに割り当てて、オブジェクトを入力します。

1. 実行時オプションを設定します。

   * コンストラクタ `AssemblerOptionSpec` ーを使用して、実行時のオプションを格納するオブジェクトを作成します。
   * オブジェクトに属するデータメンバーに値を割り当てて、ビジネス要件に合わせて実行時オプションを設定 `AssemblerOptionSpec` します。 例えば、エラーが発生した場合にジョブの処理を続行するようAssemblerサービスに指示するには、オブジェクトの `false` データメ `AssemblerOptionSpec` ンバーに割り `failOnError` 当てます。

1. ドキュメントを暗号化します。

   オブジェクト `AssemblerServiceClient` のメソッドを `invokeOneDocument` 呼び出し、次の値を渡します。

   * DDXドキ `BLOB` ュメントを表すオブジェクト
   * 保護さ `BLOB` れていないPDFドキュメントを表すオブジェクト
   * 実行時 `AssemblerOptionSpec` のオプションを指定するオブジェクト
   このメソ `invokeOneDocument` ッドは、暗号化されたPDF `BLOB` ドキュメントを含むオブジェクトを返します。

1. 暗号化されたPDFドキュメントを保存します。

   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、暗号化されたPDFドキュメントのファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * メソッドが返したオブジェクトの内容を格納する `BLOB` バイト配列を作 `invokeOneDocument` 成します。 オブジェクトのデータメンバーの値を取得して、バ `BLOB` イト配列を `MTOM` 設定します。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡すことで、バ `System.IO.BinaryWriter` イト配列の内 `Write` 容をPDFファイルに書き込みます。

**関連トピック**

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
