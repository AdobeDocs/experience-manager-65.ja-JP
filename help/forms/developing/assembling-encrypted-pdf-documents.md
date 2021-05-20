---
title: 暗号化されたPDFドキュメントのアセンブリ
seo-title: 暗号化されたPDFドキュメントのアセンブリ
description: Java APIおよびWebサービスAPIを使用して、暗号化されたPDFドキュメントをアセンブリします。
seo-description: Java APIおよびWebサービスAPIを使用して、暗号化されたPDFドキュメントをアセンブリします。
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
source-wordcount: '1675'
ht-degree: 6%

---

# 暗号化されたPDFドキュメントのアセンブリ{#assembling-encrypted-pdf-documents}

**このドキュメントのサンプルと例は、JEE上のAEM Forms環境に限られています。**

Assemblerサービスを使用して、PDFドキュメントをパスワードで暗号化できます。 PDF ドキュメントがパスワードを使用して暗号化されている場合、Adobe Reader または Acrobat で PDF ドキュメントを表示するには、パスワードを指定する必要があります。パスワードを使用して PDF ドキュメントを暗号化するには、PDF ドキュメントの暗号化に必要な暗号化要素の値を DDX ドキュメントに含める必要があります。

この説明では、次のDDXドキュメントが使用されているとします。

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

このDDXドキュメント内で、ソース属性に値`inDoc`が割り当てられていることに注意してください。 1つの入力PDFドキュメントのみがAssemblerサービスに渡され、1つのPDFドキュメントが返された場合に、`invokeOneDocument`操作を呼び出して、値`inDoc`をPDFソース属性に割り当てます。 `invokeOneDocument`操作を呼び出す場合、`inDoc`値は事前定義済みのキーで、DDXドキュメントで指定する必要があります。

これに対し、2つ以上の入力PDFドキュメントをAssemblerサービスに渡す場合は、`invokeDDX`操作を呼び出すことができます。 この場合、入力PDFドキュメントのファイル名を`source`属性に割り当てます。

PDFドキュメントをパスワードで暗号化する場合、AEM formsのインストールにEncryptionサービスを含める必要はありません。 [PDFドキュメントの暗号化と復号化](/help/forms/developing/encrypting-decrypting-pdf-documents.md)を参照してください。

>[!NOTE]
>
>Assemblerサービスについて詳しくは、『AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)向けサービスリファレンス』を参照してください。[

>[!NOTE]
>
>DDXドキュメントについて詳しくは、『[AssemblerサービスとDDXリファレンス](https://www.adobe.com/go/learn_aemforms_ddx_63)』を参照してください。

## 手順の概要{#summary-of-steps}

暗号化されたPDFドキュメントをアセンブリするには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. PDFアセンブラークライアントを作成します。
1. 既存のDDXドキュメントの参照
1. 保護されていないPDFドキュメントを参照します。
1. 実行時オプションを設定します。
1. ドキュメントを暗号化します。
1. 暗号化されたPDFドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用する場合は、プロキシファイルを必ず含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(AEM FormsをJBossにデプロイする場合に必要)
* jbossall-client.jar(AEM FormsをJBossにデプロイする場合に必要)

AEM FormsがJBoss以外のサポート対象のJ2EEアプリケーションサーバーにデプロイされている場合は、adobe-utilities.jarファイルとjbossall-client.jarファイルを、AEM FormsがデプロイされているJ2EEアプリケーションサーバーに固有のJARファイルに置き換える必要があります。 すべてのAEM Forms JARファイルの場所について詳しくは、「[AEM Forms Javaライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)」を参照してください。

**Assemblerクライアントの作成**

プログラムでAssembler操作を実行する前に、Assemblerサービスクライアントを作成する必要があります。

**既存のDDXドキュメントの参照**

PDFドキュメントをアセンブリするには、DDXドキュメントを参照する必要があります。 例えば、この節で紹介したDDXドキュメントについて考えてみましょう。 PDFドキュメントを暗号化するには、DDXドキュメントに`PasswordEncryptionProfile`要素を含める必要があります。

**保護されていないPDFドキュメントの参照**

保護されていないPDFドキュメントを暗号化するには、参照してAssemblerサービスに渡す必要があります。 既に暗号化されているPDFドキュメントを参照する場合は、例外がスローされます。

**実行時オプションの設定**

ジョブの実行中にAssemblerサービスの動作を制御する実行時オプションを設定できます。 例えば、エラーが発生した場合にジョブの処理を続行するようAssemblerサービスに指示するオプションを設定できます。 設定できる実行時オプションについて詳しくは、『[AEM Forms APIリファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)』の`AssemblerOptionSpec`クラス参照を参照してください。

**ドキュメントを暗号化**

Assemblerサービスクライアントを作成し、暗号化情報を含むDDXドキュメントを参照し、保護されていないPDFドキュメントを参照し、実行時オプションを設定したら、`invokeOneDocument`操作を呼び出すことができます。 入力PDFドキュメントが1つだけAssemblerサービスに渡される（そして1つのドキュメントが返される）ので、`invokeDDX`操作の代わりに`invokeOneDocument`操作を使用できます。

**暗号化されたPDFドキュメントの保存**

Assemblerサービスに渡されるPDFドキュメントが1つだけの場合、Assemblerサービスは、コレクションオブジェクトではなく1つのドキュメントを返します。 つまり、`invokeOneDocument`操作を呼び出すと、1つのドキュメントが返されます。 この節で参照するDDXドキュメントには暗号化情報が含まれているので、Assemblerサービスはパスワードで暗号化されたPDFドキュメントを返します。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDFドキュメントのプログラムによるアセンブリ](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java API {#assemble-an-encrypted-pdf-document-using-the-java-api}を使用した暗号化PDFドキュメントのアセンブリ

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-assembler-client.jarなどのクライアントJARファイルを含めます。

1. Assemblerクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して`AssemblerServiceClient`オブジェクトを渡し、`ServiceClientFactory`オブジェクトを作成します。

1. 既存のDDXドキュメントの参照

   * コンストラクターを使用し、DDXファイルの場所を指定する文字列値を渡して、DDXドキュメントを表す`java.io.FileInputStream`オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 保護されていないPDFドキュメントを参照します。

   * コンストラクターを使用して保護されていないPDFドキュメントの場所を渡すことで、`java.io.FileInputStream`オブジェクトを作成します。
   * `com.adobe.idp.Document`オブジェクトを作成し、PDFドキュメントを含む`java.io.FileInputStream`オブジェクトを渡します。 この`com.adobe.idp.Document`オブジェクトは、`invokeOneDocument`メソッドに渡されます。

1. 実行時オプションを設定します。

   * コンストラクターを使用して、実行時オプションを格納する`AssemblerOptionSpec`オブジェクトを作成します。
   * `AssemblerOptionSpec`オブジェクトに属するメソッドを呼び出して、ビジネス要件に合った実行時オプションを設定します。 例えば、エラーが発生したときにジョブの処理を続行するようにAssemblerサービスに指示するには、`AssemblerOptionSpec`オブジェクトの`setFailOnError`メソッドを呼び出し、`false`を渡します。

1. ドキュメントを暗号化します。

   `AssemblerServiceClient`オブジェクトの`invokeOneDocument`メソッドを呼び出し、次の値を渡します。

   * DDXドキュメントを表す`com.adobe.idp.Document`オブジェクト。 このDDXドキュメントにPDFソース要素の値`inDoc`が含まれていることを確認します。
   * 保護されていないPDFドキュメントを含む`com.adobe.idp.Document`オブジェクト。
   * デフォルトのフォントやジョブのログレベルを含む、実行時のオプションを指定する`com.adobe.livecycle.assembler.client.AssemblerOptionSpec`オブジェクト。

   `invokeOneDocument`メソッドは、パスワードで暗号化されたPDFドキュメントを含む`com.adobe.idp.Document`オブジェクトを返します。

1. 暗号化されたPDFドキュメントを保存します。

   * `java.io.File`オブジェクトを作成し、ファイル名拡張子が.pdfであることを確認します。
   * `Document`オブジェクトの`copyToFile`メソッドを呼び出して、`Document`オブジェクトの内容をファイルにコピーします。 `invokeOneDocument`メソッドが返す`Document`オブジェクトを使用していることを確認します。

**関連トピック**

[クイックスタート（SOAPモード）:Java APIを使用した暗号化されたPDFドキュメントのアセンブリ](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-an-encrypted-pdf-document-using-the-java-api)

## WebサービスAPI {#assemble-an-encrypted-pdf-document-using-the-web-service-api}を使用して暗号化されたPDFドキュメントをアセンブリする

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 サービス参照を設定する際は、次のWSDL定義を使用してください。`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. Assemblerクライアントを作成します。

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
   * `BLOB`オブジェクトの`MTOM`フィールドにバイト配列の内容を割り当てて、オブジェクトを設定します。

1. 保護されていないPDFドキュメントを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、入力PDFドキュメントの保存に使用されます。 この`BLOB`オブジェクトは、引数として`invokeOneDocument`に渡されます。
   * コンストラクターを呼び出し、入力PDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得することで、バイト配列のサイズを判断できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことによって、バイト配列にストリームデータを入力します。
   * `BLOB`オブジェクトの`MTOM`フィールドにバイト配列の内容を割り当てて、オブジェクトを設定します。

1. 実行時オプションを設定します。

   * コンストラクターを使用して、実行時オプションを格納する`AssemblerOptionSpec`オブジェクトを作成します。
   * `AssemblerOptionSpec`オブジェクトに属するデータメンバーに値を割り当てて、ビジネス要件に合った実行時オプションを設定します。 例えば、エラーが発生したときにジョブの処理を続行するようにAssemblerサービスに指示するには、`false`を`AssemblerOptionSpec`オブジェクトの`failOnError`データメンバーに割り当てます。

1. ドキュメントを暗号化します。

   `AssemblerServiceClient`オブジェクトの`invokeOneDocument`メソッドを呼び出し、次の値を渡します。

   * DDXドキュメントを表す`BLOB`オブジェクト
   * 保護されていないPDFドキュメントを表す`BLOB`オブジェクト
   * 実行時オプションを指定する`AssemblerOptionSpec`オブジェクト

   `invokeOneDocument`メソッドは、暗号化されたPDFドキュメントを含む`BLOB`オブジェクトを返します。

1. 暗号化されたPDFドキュメントを保存します。

   * コンストラクターを呼び出し、暗号化されたPDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `invokeOneDocument`メソッドが返した`BLOB`オブジェクトの内容を格納するバイト配列を作成します。 `BLOB`オブジェクトの`MTOM`データメンバーの値を取得して、バイト配列を設定します。
   * コンストラクターを呼び出し、`System.IO.FileStream`オブジェクトを渡して、`System.IO.BinaryWriter`オブジェクトを作成します。
   * `System.IO.BinaryWriter`オブジェクトの`Write`メソッドを呼び出し、バイト配列を渡すことにより、バイト配列の内容をPDFファイルに書き込みます。

**関連トピック**

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
