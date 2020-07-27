---
title: 非インタラクティブPDFドキュメントのアセンブリ
seo-title: 非インタラクティブPDFドキュメントのアセンブリ
description: 'null'
seo-description: 'null'
uuid: 0c7adeb4-9a3a-4ec5-ba33-c3642928d4ea
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8a75c201-bd88-4809-be08-69de94656489
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1760'
ht-degree: 3%

---


# 非インタラクティブPDFドキュメントのアセンブリ {#assembling-non-interactive-pdf-documents}

インタラクティブPDFフォームを入力として使用する場合は、非インタラクティブPDFドキュメントをアセンブリできます。 つまり、ユーザーがフィールドにデータを入力するために使用できるフォームがあるとします。 このフォームをAssemblerサービスに渡すと、AssemblerサービスからPDFドキュメントが返され、ユーザーはフィールドにデータを入力できなくなります。 このドキュメントは非インタラクティブPDFフォームです。 例えば、次の図に、インタラクティブフォームを表す住宅ローン申込書を示します。

この説明の目的で、次のDDXドキュメントが使用されているとします。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDF result="out.pdf">
        <PDF source="inDoc"/>
        <NoXFA/>
      </PDF>
 </DDX>
```

このDDXドキュメント内で、source属性に値が割り当てられてい `inDoc`ます。 1つの入力PDFドキュメントのみがAssemblerサービスに渡され、1つのPDFドキュメントが返される場合に、 `invokeOneDocument` 操作を呼び出すには、値をPDFソース属性 `inDoc` に割り当てます。 この `invokeOneDocument` 操作を呼び出すとき、 `inDoc` 値は、DDXドキュメントで指定する必要がある事前定義済みのキーになります。

一方、2つ以上の入力PDFドキュメントをAssemblerサービスに渡す場合は、この `invokeDDX` 操作を呼び出すことができます。 この場合、入力PDFドキュメントのファイル名を `source` 属性に割り当てます。

このDDXドキュメントには `NoXFA` 要素が含まれています。この要素は、非インタラクティブPDFドキュメントを返すようAssemblerサービスに指示します。

Acrobatフォームまたは静的XFAフォームに基づく入力PDFドキュメントの場合、OutputサービスをAEM formsインストールに含めずに、非インタラクティブPDFドキュメントをAssemblerサービスでアセンブルできます。 ただし、入力PDFドキュメントがダイナミックXFAフォームの場合は、OutputサービスがAEM formsのインストールに含まれている必要があります。 動的なXFAフォームがアセンブリされたときに、OutputサービスがAEM formsインストールの一部でない場合は、例外が発生します。 「ドキュメント出力ストリームの [作成](/help/forms/developing/creating-document-output-streams.md)」を参照してください。

>[!NOTE]
>
>この節を読む前に、Assemblerサービスを使用したPDFドキュメントのアセンブリについて理解しておくことをお勧めします。 ここでは、入力ドキュメントを含むコレクションオブジェクトの作成や、返されるコレクションオブジェクトから結果を抽出する方法の学習など、概念については説明しません。 (「 [プログラムによるPDFドキュメントのアセンブリ](/help/forms/developing/programmatically-assembling-pdf-documents.md)」を参照)。

>[!NOTE]
>
>For more information about the Assembler service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>DDXドキュメントについて詳しくは、『 [Assembler Service and DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63)』を参照してください。

## 手順の概要 {#summary-of-steps}

非インタラクティブPDFドキュメントをアセンブリするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. PDFアセンブラクライアントを作成します。
1. 既存のDDXドキュメントの参照。
1. インタラクティブPDFドキュメントの参照
1. 実行時オプションを設定します。
1. PDFドキュメントをアセンブリします。
1. 非インタラクティブPDFドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(AEM FormsがJBossにデプロイされている場合に必要)
* jbossall-client.jar(AEM FormsがJBossにデプロイされている場合に必要)

AEM FormsがJBoss以外のサポート対象のJ2EEアプリケーションサーバーにデプロイされている場合は、adobe-utilities.jarファイルとjbossall-client.jarファイルを、AEM FormsがデプロイされているJ2EEアプリケーションサーバーに固有のJARファイルに置き換える必要があります。

**Assemblerクライアントの作成**

プログラムによってAssembler操作を実行する前に、Assemblerサービスクライアントを作成する必要があります。

**既存のDDXドキュメントの参照**

PDFドキュメントをアセンブリするには、DDXドキュメントを参照する必要があります。 このDDXドキュメントには `NoXFA` 要素を含める必要があります。この要素は、非インタラクティブPDFドキュメントを返すようAssemblerサービスに指示します。

**インタラクティブPDFドキュメントの参照**

非インタラクティブPDFドキュメントを戻すには、インタラクティブPDFドキュメントを参照し、Assemblerサービスに渡す必要があります。

**実行時オプションの設定**

ジョブの実行中にAssemblerサービスの動作を制御する実行時オプションを設定できます。 例えば、エラーが発生した場合にジョブの処理を続行するようAssemblerサービスに指示するオプションを設定できます。

**PDFドキュメントのアセンブリ**

Assemblerサービスクライアントの作成後、DDXドキュメントの参照、インタラクティブPDFドキュメントの参照、および実行時オプションの設定を行った後、この `invokeOneDocument` 操作を呼び出すことができます。 Assemblerサービスに渡される入力PDFドキュメントは1つだけで、1つのドキュメントが返されるので、この `invokeOneDocument` 操作は、この `invokeDDX` 操作とは異なり、使用できます。

**非インタラクティブPDFドキュメントの保存**

Assemblerサービスに渡されるPDFドキュメントが1つだけの場合、Assemblerサービスは、コレクションオブジェクトではなく1つのドキュメントを返します。 つまり、 `invokeOneDocument` 操作を呼び出すと、1つのドキュメントが返されます。 この節で参照するDDXドキュメントには非インタラクティブPDFドキュメントの作成手順が含まれているので、Assemblerサービスは、PDFファイルとして保存できる非インタラクティブPDFドキュメントを返します。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[プログラムによるPDFドキュメントのアセンブリ](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java APIを使用した非インタラクティブPDFドキュメントのアセンブリ {#assemble-a-non-interactive-pdf-document-using-the-java-api}

Assembler Service API(Java)を使用して、非インタラクティブPDFドキュメントをアセンブリします。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-assembler-client.jarなどのクライアントJARファイルを含めます。

1. Assemblerクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `AssemblerServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. 既存のDDXドキュメントの参照。

   * コンストラクターを使用し、DDXファイルの場所を指定する文字列値を渡して、DDXドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. インタラクティブPDFドキュメントの参照

   * コンストラクターを使用し、インタラクティブPDFドキュメントの場所を渡して、 `java.io.FileInputStream` オブジェクトを作成します。
   * オブジェクトを作成し、PDF `com.adobe.idp.Document` ドキュメントを含む `java.io.FileInputStream` オブジェクトを渡します。 この `com.adobe.idp.Document` オブジェクトはメソッドに渡され `invokeOneDocument` ます。

1. 実行時オプションを設定します。

   * コンストラクターを使用して、実行時のオプションを格納する `AssemblerOptionSpec` オブジェクトを作成します。
   * オブジェクトに属するメソッドを呼び出して、ビジネス要件に合うように実行時オプションを設定し `AssemblerOptionSpec` ます。 例えば、エラーが発生した場合にジョブの処理を続行するようにAssemblerサービスに指示するには、 `AssemblerOptionSpec` オブジェクトの `setFailOnError` メソッドを呼び出して渡し `false`ます。

1. PDFドキュメントをアセンブリします。

   オブジェクトの `AssemblerServiceClient``invokeOneDocument` メソッドを呼び出し、次の値を渡します。

   * DDXドキュメントを表す `com.adobe.idp.Document` オブジェクトです。 このDDXドキュメントにPDFソース要素の値が含まれてい `inDoc` ることを確認してください。
   * インタラクティブPDFドキュメントを含む `com.adobe.idp.Document` オブジェクトです。
   * デフォルトのフォントやジョブログレベルなど、実行時のオプションを指定する `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` オブジェクト。

   非インタラクティブPDFドキュメントを含む `invokeOneDocument``com.adobe.idp.Document` オブジェクトを返します。

1. 非インタラクティブPDFドキュメントを保存します。

   * Create a `java.io.File` object and ensure that the file name extension is .pdf.
   * Invoke the `Document` object’s `copyToFile` method to copy the contents of the `Document` object to the file. メソッドが返した `Document` オブジェクトを使用していることを確認し `invokeOneDocument` ます。

* 「クイック開始（SOAPモード）: Java APIを使用した非インタラクティブPDFドキュメントのアセンブリ»

## WebサービスAPIを使用した非インタラクティブPDFドキュメントのアセンブリ {#assemble-a-non-interactive-pdf-document-using-the-web-service-api}

Assembler Service API（Webサービス）を使用して非インタラクティブPDFドキュメントをアセンブリします。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

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
   * オブジェクトのメソッドを呼び出して、バイト配列にストリームデータ `System.IO.FileStream` を入力し `Read` ます。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * オブジェクトにバイト配列の内容を割り当てて、 `BLOB` オブジェクト `MTOM` を入力します。

1. インタラクティブPDFドキュメントの参照

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、入力PDFドキュメントの保存に使用されます。 この `BLOB` オブジェクトは、引数としてに渡 `invokeOneDocument` されます。
   * コンストラクターを呼び出し、入力PDFドキュメントーのファイルの場所と、ファイルを開くモードを表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
   * オブジェクトのメソッドを呼び出して、バイト配列にストリームデータ `System.IO.FileStream` を入力し `Read` ます。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * オブジェクトにバイト配列の内容を割り当てて、 `BLOB` オブジェクト `MTOM` を入力します。

1. 実行時オプションを設定します。

   * コンストラクターを使用して、実行時のオプションを格納する `AssemblerOptionSpec` オブジェクトを作成します。
   * オブジェクトに属するデータメンバに値を割り当てることで、ビジネス要件に合った実行時オプションを設定し `AssemblerOptionSpec` ます。 例えば、エラーが発生した場合にジョブの処理を続行するようにAssemblerサービスに指示するには、 `false` オブジェクトの `AssemblerOptionSpec``failOnError` データメンバーに割り当てます。

1. PDFドキュメントをアセンブリします。

   オブジェクトの `AssemblerServiceClient``invokeOneDocument` メソッドを呼び出し、次の値を渡します。

   * DDXドキュメントを表す `BLOB` オブジェクトです
   * A `BLOB` object that represents the interactive PDF document
   * 実行時オプションを指定する `AssemblerOptionSpec` オブジェクトです。

   非インタラクティブPDFドキュメントを含む `invokeOneDocument``BLOB` オブジェクトを返します。

1. 非インタラクティブPDFドキュメントを保存します。

   * コンストラクターを呼び出し、非インタラクティブPDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * メソッドが返した `BLOB` オブジェクトの内容を格納するバイト配列を作成し `invokeOneDocument` ます。 オブジェクトのフィールドの値を取得して、 `BLOB` バイト配列を設定し `MTOM` ます。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡して、バイト配列の内容をPDFファイルに書き込み `System.IO.BinaryWriter` ま `Write` す。

* 「クイック開始(MTOM): WebサービスAPIを使用した非インタラクティブPDFドキュメントのアセンブリ」を参照してください。

**関連トピック**

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
