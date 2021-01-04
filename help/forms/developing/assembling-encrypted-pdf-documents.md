---
title: 暗号化されたPDFドキュメントのアセンブリ
seo-title: 暗号化されたPDFドキュメントのアセンブリ
description: Java APIとWeb Service APIを使用して、暗号化されたPDFドキュメントをアセンブリします。
seo-description: Java APIとWeb Service APIを使用して、暗号化されたPDFドキュメントをアセンブリします。
uuid: d0948ec9-ab67-4fe4-9062-1c4938460b43
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 6d75c7b1-9c0e-47f3-bdb1-61acf16b97f9
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '1661'
ht-degree: 6%

---


# 暗号化されたPDFドキュメントのアセンブリ{#assembling-encrypted-pdf-documents}

Assemblerサービスを使用して、PDFドキュメントをパスワードで暗号化できます。 PDF ドキュメントがパスワードを使用して暗号化されている場合、Adobe Reader または Acrobat で PDF ドキュメントを表示するには、パスワードを指定する必要があります。パスワードを使用して PDF ドキュメントを暗号化するには、PDF ドキュメントの暗号化に必要な暗号化要素の値を DDX ドキュメントに含める必要があります。

この説明の目的で、次のDDXドキュメントが使用されているとします。

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

このDDXドキュメント内で、source属性に`inDoc`という値が割り当てられています。 1つの入力PDFドキュメントのみがAssemblerサービスに渡され、1つのPDFドキュメントが返される場合に、`invokeOneDocument`操作を呼び出すには、値`inDoc`をPDFソース属性に割り当てます。 `invokeOneDocument`操作を呼び出すとき、`inDoc`値は、DDXドキュメントで指定する必要がある事前定義済みのキーです。

これに対し、2つ以上の入力PDFドキュメントをAssemblerサービスに渡す場合は、`invokeDDX`操作を呼び出すことができます。 この場合、入力PDFドキュメントのファイル名を`source`属性に割り当てます。

PDFドキュメントをパスワードを使用して暗号化する場合、AEM formsのインストール環境にEncryptionサービスを含める必要はありません。 [PDFドキュメントの暗号化と復号化](/help/forms/developing/encrypting-decrypting-pdf-documents.md)を参照してください。

>[!NOTE]
>
>Assemblerサービスについて詳しくは、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

>[!NOTE]
>
>DDXドキュメントについて詳しくは、「[Assembler Service and DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63)」を参照してください。

## 手順{#summary-of-steps}の概要

暗号化されたPDFドキュメントをアセンブリするには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. PDFアセンブラクライアントを作成します。
1. 既存のDDXドキュメントの参照。
1. 保護されていないPDFドキュメントを参照します。
1. 実行時オプションを設定します。
1. ドキュメントを暗号化します。
1. 暗号化されたPDFドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(AEM FormsがJBossにデプロイされている場合に必要)
* jbossall-client.jar(AEM FormsがJBossにデプロイされている場合に必要)

aem formsがJBoss以外のサポート対象のJ2EEアプリケーションサーバーにデプロイされている場合は、adobe-utilities.jarファイルとjbossall-client.jarファイルを、AEM FormsがデプロイされているJ2EEアプリケーションサーバーに固有のJARファイルに置き換える必要があります。 すべてのAEM FormsJARファイルの場所については、「[AEM FormsJavaライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)」を参照してください。

**Assemblerクライアントの作成**

プログラムによってAssembler操作を実行する前に、Assemblerサービスクライアントを作成する必要があります。

**既存のDDXドキュメントの参照**

PDFドキュメントをアセンブリするには、DDXドキュメントを参照する必要があります。 例えば、この節で紹介したDDXドキュメントについて考えてみましょう。 PDFドキュメントを暗号化するには、DDXドキュメントに`PasswordEncryptionProfile`要素を含める必要があります。

**保護されていないPDFドキュメントの参照**

保護されていないPDFドキュメントは、参照してAssemblerサービスに渡し、暗号化する必要があります。 既に暗号化されているPDFドキュメントを参照すると、例外が発生します。

**実行時オプションの設定**

ジョブの実行中にAssemblerサービスの動作を制御する実行時オプションを設定できます。 例えば、エラーが発生した場合にジョブの処理を続行するようAssemblerサービスに指示するオプションを設定できます。 設定できる実行時オプションについて詳しくは、[AEM FormsAPIリファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)の`AssemblerOptionSpec`クラス参照を参照してください。

**ドキュメントを暗号化する**

Assemblerサービスクライアントの作成後、暗号化ドキュメントを含むDDXドキュメントを参照し、保護されていないPDF情報を参照し、実行時オプションを設定した後、`invokeOneDocument`操作を呼び出すことができます。 1つの入力PDFドキュメントのみがAssemblerサービスに渡されるので(1つのドキュメントが返される)、`invokeDDX`操作の代わりに`invokeOneDocument`操作を使用できます。

**暗号化されたPDFドキュメントの保存**

Assemblerサービスに渡されるPDFドキュメントが1つだけの場合、Assemblerサービスは、コレクションオブジェクトではなく1つのドキュメントを返します。 つまり、`invokeOneDocument`操作を呼び出すと、1つのドキュメントが返されます。 この節で参照するDDXドキュメントには暗号化情報が含まれているので、Assemblerサービスはパスワードで暗号化されたPDFドキュメントを返します。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[プログラムによるPDFドキュメントのアセンブリ](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java API {#assemble-an-encrypted-pdf-document-using-the-java-api}を使用して暗号化PDFドキュメントをアセンブリする

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-assembler-client.jarなどのクライアントJARファイルを含めます。

1. Assemblerクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用し、`AssemblerServiceClient`オブジェクトを渡して、`ServiceClientFactory`オブジェクトを作成します。

1. 既存のDDXドキュメントの参照。

   * コンストラクターを使用し、DDXファイルの場所を指定する文字列値を渡して、DDXドキュメントを表す`java.io.FileInputStream`オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 保護されていないPDFドキュメントを参照します。

   * コンストラクターを使用し、保護されていないPDFドキュメントの場所を渡して、`java.io.FileInputStream`オブジェクトを作成します。
   * `com.adobe.idp.Document`オブジェクトを作成し、PDFドキュメントを含む`java.io.FileInputStream`オブジェクトを渡します。 この`com.adobe.idp.Document`オブジェクトは`invokeOneDocument`メソッドに渡されます。

1. 実行時オプションを設定します。

   * コンストラクターを使用して、実行時オプションを格納する`AssemblerOptionSpec`オブジェクトを作成します。
   * `AssemblerOptionSpec`オブジェクトに属するメソッドを呼び出して、ビジネス要件に合うように実行時オプションを設定します。 例えば、エラーが発生した場合にジョブの処理を続行するようにAssemblerサービスに指示するには、`AssemblerOptionSpec`オブジェクトの`setFailOnError`メソッドを呼び出し、`false`を渡します。

1. ドキュメントを暗号化します。

   `AssemblerServiceClient`オブジェクトの`invokeOneDocument`メソッドを呼び出し、次の値を渡します。

   * DDXドキュメントを表す`com.adobe.idp.Document`オブジェクトです。 このDDXドキュメントにPDFソース要素の値`inDoc`が含まれていることを確認してください。
   * 保護されていないPDFドキュメントが含まれる`com.adobe.idp.Document`オブジェクトです。
   * デフォルトのフォントとジョブログレベルを含む、実行時のオプションを指定する`com.adobe.livecycle.assembler.client.AssemblerOptionSpec`オブジェクト。

   `invokeOneDocument`メソッドは、パスワードで暗号化されたPDFドキュメントを含む`com.adobe.idp.Document`オブジェクトを返します。

1. 暗号化されたPDFドキュメントを保存します。

   * `java.io.File`オブジェクトを作成し、ファイル名の拡張子が.pdfであることを確認します。
   * `Document`オブジェクトの`copyToFile`メソッドを呼び出して、`Document`オブジェクトの内容をファイルにコピーします。 `invokeOneDocument`メソッドが返した`Document`オブジェクトを使用していることを確認してください。

**関連トピック**

[クイック開始（SOAPモード）:Java APIを使用した暗号化PDFドキュメントのアセンブリ](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-an-encrypted-pdf-document-using-the-java-api)

## WebサービスAPI {#assemble-an-encrypted-pdf-document-using-the-web-service-api}を使用して暗号化されたPDFドキュメントをアセンブリする

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 サービス参照を設定する際は、次のWSDL定義を使用してください。`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. Assemblerクライアントを作成します。

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
   * `BLOB`オブジェクトに、`MTOM`フィールドにバイト配列の内容を割り当てて入力します。

1. 保護されていないPDFドキュメントを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、入力PDFドキュメントの保存に使用されます。 この`BLOB`オブジェクトは、`invokeOneDocument`に引数として渡されます。
   * コンストラクターを呼び出し、入力PDFドキュメントーのファイルの場所と、ファイルを開くモードを表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得して、バイト配列のサイズを決定できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * `BLOB`オブジェクトに、`MTOM`フィールドにバイト配列の内容を割り当てて入力します。

1. 実行時オプションを設定します。

   * コンストラクターを使用して、実行時オプションを格納する`AssemblerOptionSpec`オブジェクトを作成します。
   * `AssemblerOptionSpec`オブジェクトに属するデータメンバに値を割り当てて、ビジネス要件に合うように実行時オプションを設定します。 例えば、エラーが発生した場合にジョブの処理を続行するようにAssemblerサービスに指示するには、`false`を`AssemblerOptionSpec`オブジェクトの`failOnError`データメンバーに割り当てます。

1. ドキュメントを暗号化します。

   `AssemblerServiceClient`オブジェクトの`invokeOneDocument`メソッドを呼び出し、次の値を渡します。

   * DDXドキュメントを表す`BLOB`オブジェクト
   * 保護されていないPDFドキュメントを表す`BLOB`オブジェクト
   * 実行時オプションを指定する`AssemblerOptionSpec`オブジェクト

   `invokeOneDocument`メソッドは、暗号化されたPDFドキュメントを含む`BLOB`オブジェクトを返します。

1. 暗号化されたPDFドキュメントを保存します。

   * コンストラクターを呼び出し、暗号化されたPDFドキュメントーのファイルの場所と、ファイルを開くモードを表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `invokeOneDocument`メソッドが返した`BLOB`オブジェクトの内容を格納するバイト配列を作成します。 `BLOB`オブジェクトの`MTOM`データメンバの値を取得して、バイト配列を入力します。
   * コンストラクターを呼び出して`System.IO.FileStream`オブジェクトを渡し、`System.IO.BinaryWriter`オブジェクトを作成します。
   * `System.IO.BinaryWriter`オブジェクトの`Write`メソッドを呼び出し、バイト配列を渡すことで、バイト配列の内容をPDFファイルに書き込みます。

**関連トピック**

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
