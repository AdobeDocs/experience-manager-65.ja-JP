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
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1639'
ht-degree: 6%

---


# 暗号化されたPDFドキュメントのアセンブリ {#assembling-encrypted-pdf-documents}

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

このDDXドキュメント内で、source属性に値が割り当てられてい `inDoc`ます。 1つの入力PDFドキュメントのみがAssemblerサービスに渡され、1つのPDFドキュメントが返される場合に、 `invokeOneDocument` 操作を呼び出すには、値をPDFソース属性 `inDoc` に割り当てます。 この `invokeOneDocument` 操作を呼び出すとき、 `inDoc` 値は、DDXドキュメントで指定する必要がある事前定義済みのキーになります。

一方、2つ以上の入力PDFドキュメントをAssemblerサービスに渡す場合は、この `invokeDDX` 操作を呼び出すことができます。 この場合、入力PDFドキュメントのファイル名を `source` 属性に割り当てます。

PDFドキュメントをパスワードで暗号化する場合、EncryptionサービスをAEM formsのインストールに含める必要はありません。 PDFドキュメントの [暗号化と復号化を参照してください](/help/forms/developing/encrypting-decrypting-pdf-documents.md)。

>[!NOTE]
>
>For more information about the Assembler service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>DDXドキュメントについて詳しくは、『 [Assembler Service and DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63)』を参照してください。

## 手順の概要 {#summary-of-steps}

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

AEM FormsがJBoss以外のサポート対象のJ2EEアプリケーションサーバーにデプロイされている場合は、adobe-utilities.jarファイルとjbossall-client.jarファイルを、AEM FormsがデプロイされているJ2EEアプリケーションサーバーに固有のJARファイルに置き換える必要があります。 For information about the location of all AEM Forms JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Assemblerクライアントの作成**

プログラムによってAssembler操作を実行する前に、Assemblerサービスクライアントを作成する必要があります。

**既存のDDXドキュメントの参照**

PDFドキュメントをアセンブリするには、DDXドキュメントを参照する必要があります。 例えば、この節で紹介したDDXドキュメントについて考えてみましょう。 PDFドキュメントを暗号化するには、DDXドキュメントにその `PasswordEncryptionProfile` 要素が含まれている必要があります。

**保護されていないPDFドキュメントの参照**

保護されていないPDFドキュメントは、参照してAssemblerサービスに渡し、暗号化する必要があります。 既に暗号化されているPDFドキュメントを参照すると、例外が発生します。

**実行時オプションの設定**

ジョブの実行中にAssemblerサービスの動作を制御する実行時オプションを設定できます。 例えば、エラーが発生した場合にジョブの処理を続行するようAssemblerサービスに指示するオプションを設定できます。 設定できる実行時オプションについて詳しくは、『 `AssemblerOptionSpec` AEM FormsAPIリファレンス』の [クラス参照を参照してください](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

**ドキュメントを暗号化する**

Assemblerサービスクライアントを作成したら、暗号化ドキュメントを含むDDXドキュメントを参照し、保護されていないPDF情報を参照し、実行時のオプションを設定した後で、この `invokeOneDocument` 操作を呼び出すことができます。 Assemblerサービスに渡される入力PDFドキュメントは1つだけなので(1つのドキュメントが返される)、この `invokeOneDocument` 操作の代わりにこの `invokeDDX` 操作を使用できます。

**暗号化されたPDFドキュメントの保存**

Assemblerサービスに渡されるPDFドキュメントが1つだけの場合、Assemblerサービスは、コレクションオブジェクトではなく1つのドキュメントを返します。 つまり、 `invokeOneDocument` 操作を呼び出すと、1つのドキュメントが返されます。 この節で参照するDDXドキュメントには暗号化情報が含まれているので、Assemblerサービスはパスワードで暗号化されたPDFドキュメントを返します。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[プログラムによるPDFドキュメントのアセンブリ](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java APIを使用した暗号化PDFドキュメントのアセンブリ {#assemble-an-encrypted-pdf-document-using-the-java-api}

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-assembler-client.jarなどのクライアントJARファイルを含めます。

1. Assemblerクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `AssemblerServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. 既存のDDXドキュメントの参照。

   * コンストラクターを使用し、DDXファイルの場所を指定する文字列値を渡して、DDXドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 保護されていないPDFドキュメントを参照します。

   * コンストラクターを使用し、保護されていないPDFドキュメントの場所を渡して、 `java.io.FileInputStream` オブジェクトを作成します。
   * オブジェクトを作成し、PDF `com.adobe.idp.Document` ドキュメントを含む `java.io.FileInputStream` オブジェクトを渡します。 この `com.adobe.idp.Document` オブジェクトはメソッドに渡され `invokeOneDocument` ます。

1. 実行時オプションを設定します。

   * コンストラクターを使用して、実行時のオプションを格納する `AssemblerOptionSpec` オブジェクトを作成します。
   * オブジェクトに属するメソッドを呼び出して、ビジネス要件に合うように実行時オプションを設定し `AssemblerOptionSpec` ます。 例えば、エラーが発生した場合にジョブの処理を続行するようにAssemblerサービスに指示するには、 `AssemblerOptionSpec` オブジェクトの `setFailOnError` メソッドを呼び出して渡し `false`ます。

1. ドキュメントを暗号化します。

   オブジェクトの `AssemblerServiceClient``invokeOneDocument` メソッドを呼び出し、次の値を渡します。

   * DDXドキュメントを表す `com.adobe.idp.Document` オブジェクトです。 このDDXドキュメントにPDFソース要素の値が含まれてい `inDoc` ることを確認してください。
   * 保護されていないPDFドキュメントを含む `com.adobe.idp.Document` オブジェクトです。
   * デフォルトのフォントやジョブログレベルなど、実行時のオプションを指定する `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` オブジェクト。

   パスワードで暗号化されたPDFドキュメントを含む `invokeOneDocument``com.adobe.idp.Document` オブジェクトを返します。

1. 暗号化されたPDFドキュメントを保存します。

   * Create a `java.io.File` object and ensure that the file name extension is .pdf.
   * Invoke the `Document` object’s `copyToFile` method to copy the contents of the `Document` object to the file. メソッドが返した `Document` オブジェクトを使用していることを確認し `invokeOneDocument` ます。

**関連トピック**

[クイック開始（SOAPモード）: Java APIを使用した暗号化PDFドキュメントのアセンブリ](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-an-encrypted-pdf-document-using-the-java-api)

## WebサービスAPIを使用した暗号化PDFドキュメントのアセンブリ {#assemble-an-encrypted-pdf-document-using-the-web-service-api}

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 サービス参照を設定する際は、次のWSDL定義を使用してください。 `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >サーバーホスト `localhost` AEM FormsのIPアドレスに置き換えます。

1. Assemblerクライアントを作成します。

   * デフォルトのコンストラクターを使用して `AssemblerServiceClient` オブジェクトを作成します。
   * コンストラクターを使用して `AssemblerServiceClient.Endpoint.Address` オブジェクトを作成し `System.ServiceModel.EndpointAddress` ます。 WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/AssemblerService?blob=mtom`)に渡すstring値を渡します。 属性を使用する必要はありません `lc_version` 。 この属性は、サービス参照を作成する際に使用されます。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `AssemblerServiceClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールドにAEM formsのユーザー名を割り当て `AssemblerServiceClient.ClientCredentials.UserName.UserName`ます。
      * 対応するパスワード値をフィールドに割り当て `AssemblerServiceClient.ClientCredentials.UserName.Password`ます。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当て `BasicHttpBindingSecurity.Security.Mode`ます。

1. 既存のDDXドキュメントの参照。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、DDXドキュメントの格納に使用されます。
   * コンストラクターを呼び出し、DDXドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
   * オブジェクトの `System.IO.FileStream``Read` メソッドを呼び出し、読み取るバイト配列、開始位置およびストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * オブジェクトにバイト配列の内容を割り当てて、 `BLOB` オブジェクト `MTOM` を入力します。

1. 保護されていないPDFドキュメントを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、入力PDFドキュメントの保存に使用されます。 この `BLOB` オブジェクトは、引数としてに渡 `invokeOneDocument` されます。
   * コンストラクターを呼び出し、入力PDFドキュメントーのファイルの場所と、ファイルを開くモードを表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
   * オブジェクトの `System.IO.FileStream``Read` メソッドを呼び出し、読み取るバイト配列、開始位置およびストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * オブジェクトにバイト配列の内容を割り当てて、 `BLOB` オブジェクト `MTOM` を入力します。

1. 実行時オプションを設定します。

   * コンストラクターを使用して、実行時のオプションを格納する `AssemblerOptionSpec` オブジェクトを作成します。
   * オブジェクトに属するデータメンバに値を割り当てることで、ビジネス要件に合った実行時オプションを設定し `AssemblerOptionSpec` ます。 例えば、エラーが発生した場合にジョブの処理を続行するようにAssemblerサービスに指示するには、 `false` オブジェクトの `AssemblerOptionSpec``failOnError` データメンバーに割り当てます。

1. ドキュメントを暗号化します。

   オブジェクトの `AssemblerServiceClient``invokeOneDocument` メソッドを呼び出し、次の値を渡します。

   * DDXドキュメントを表す `BLOB` オブジェクトです
   * 保護されていないPDFドキュメントを表す `BLOB` オブジェクトです
   * 実行時オプションを指定する `AssemblerOptionSpec` オブジェクトです。

   暗号化されたPDFドキュメントを含む `invokeOneDocument``BLOB` オブジェクトを返します。

1. 暗号化されたPDFドキュメントを保存します。

   * コンストラクターを呼び出し、暗号化されたPDFドキュメントーのファイルの場所と、ファイルを開くモードを表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * メソッドが返した `BLOB` オブジェクトの内容を格納するバイト配列を作成し `invokeOneDocument` ます。 オブジェクトのデータメンバーの値を取得して、 `BLOB` バイト配列を入力し `MTOM` ます。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡して、バイト配列の内容をPDFファイルに書き込み `System.IO.BinaryWriter` ま `Write` す。

**関連トピック**

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
