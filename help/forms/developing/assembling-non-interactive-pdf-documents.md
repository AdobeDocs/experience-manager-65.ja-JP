---
title: 非インタラクティブPDFドキュメントのアセンブリ
seo-title: 非インタラクティブPDFドキュメントのアセンブリ
description: Java APIとWeb Service APIを使用して非インタラクティブPDFドキュメントをアセンブリするには、非インタラクティブPDFフォームを入力として使用します。
seo-description: Java APIとWeb Service APIを使用して非インタラクティブPDFドキュメントをアセンブリするには、非インタラクティブPDFフォームを入力として使用します。
uuid: 0c7adeb4-9a3a-4ec5-ba33-c3642928d4ea
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8a75c201-bd88-4809-be08-69de94656489
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '1800'
ht-degree: 2%

---


# 非インタラクティブPDFドキュメントのアセンブリ{#assembling-non-interactive-pdf-documents}

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

このDDXドキュメント内で、source属性に`inDoc`という値が割り当てられています。 1つの入力PDFドキュメントのみがAssemblerサービスに渡され、1つのPDFドキュメントが返される場合に、`invokeOneDocument`操作を呼び出すには、値`inDoc`をPDFソース属性に割り当てます。 `invokeOneDocument`操作を呼び出すとき、`inDoc`値は、DDXドキュメントで指定する必要がある事前定義済みのキーです。

これに対し、2つ以上の入力PDFドキュメントをAssemblerサービスに渡す場合は、`invokeDDX`操作を呼び出すことができます。 この場合、入力PDFドキュメントのファイル名を`source`属性に割り当てます。

このDDXドキュメントには`NoXFA`要素が含まれています。この要素は、非インタラクティブPDFドキュメントを返すようAssemblerサービスに指示します。

Assemblerサービスは、入力PDFドキュメントがAcrobatフォームまたは静的XFAフォームを基にしている場合、OutputサービスがAEM formsインストールに含まれていなくても、非インタラクティブPDFドキュメントをアセンブルできます。 ただし、入力PDFドキュメントがダイナミックXFAフォームの場合は、OutputサービスがAEM formsのインストールに含まれている必要があります。 動的XFAフォームのアセンブリ時に、OutputサービスがAEM formsインストールの一部でない場合は、例外が発生します。 「[ドキュメント出力ストリームの作成](/help/forms/developing/creating-document-output-streams.md)」を参照してください。

>[!NOTE]
>
>この節を読む前に、Assemblerサービスを使用したPDFドキュメントのアセンブリについて理解しておくことをお勧めします。 ここでは、入力ドキュメントを含むコレクションオブジェクトの作成や、返されるコレクションオブジェクトから結果を抽出する方法の学習など、概念については説明しません。 (「[PDFドキュメントのプログラムによるアセンブリ](/help/forms/developing/programmatically-assembling-pdf-documents.md)」を参照)。

>[!NOTE]
>
>Assemblerサービスについて詳しくは、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

>[!NOTE]
>
>DDXドキュメントについて詳しくは、「[Assembler Service and DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63)」を参照してください。

## 手順{#summary-of-steps}の概要

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

aem formsがJBoss以外のサポート対象のJ2EEアプリケーションサーバーにデプロイされている場合は、adobe-utilities.jarファイルとjbossall-client.jarファイルを、AEM FormsがデプロイされているJ2EEアプリケーションサーバーに固有のJARファイルに置き換える必要があります。

**Assemblerクライアントの作成**

プログラムによってAssembler操作を実行する前に、Assemblerサービスクライアントを作成する必要があります。

**既存のDDXドキュメントの参照**

PDFドキュメントをアセンブリするには、DDXドキュメントを参照する必要があります。 このDDXドキュメントには`NoXFA`要素を含める必要があります。この要素は、非インタラクティブPDFドキュメントを返すようAssemblerサービスに指示します。

**インタラクティブPDFドキュメントの参照**

非インタラクティブPDFドキュメントを戻すには、インタラクティブPDFドキュメントを参照し、Assemblerサービスに渡す必要があります。

**実行時オプションの設定**

ジョブの実行中にAssemblerサービスの動作を制御する実行時オプションを設定できます。 例えば、エラーが発生した場合にジョブの処理を続行するようAssemblerサービスに指示するオプションを設定できます。

**PDFドキュメントのアセンブリ**

Assemblerサービスクライアントの作成、DDXドキュメントの参照、インタラクティブPDFドキュメントの参照、および実行時オプションの設定が完了したら、`invokeOneDocument`操作を呼び出すことができます。 Assemblerサービスに渡される入力PDFドキュメントは1つだけで、1つのドキュメントが返されるので、`invokeDDX`操作とは異なり、`invokeOneDocument`操作を使用できます。

**非インタラクティブPDFドキュメントの保存**

Assemblerサービスに渡されるPDFドキュメントが1つだけの場合、Assemblerサービスは、コレクションオブジェクトではなく1つのドキュメントを返します。 つまり、`invokeOneDocument`操作を呼び出すと、1つのドキュメントが返されます。 この節で参照するDDXドキュメントには非インタラクティブPDFドキュメントの作成手順が含まれているので、Assemblerサービスは、PDFファイルとして保存できる非インタラクティブPDFドキュメントを返します。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[プログラムによるPDFドキュメントのアセンブリ](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java API {#assemble-a-non-interactive-pdf-document-using-the-java-api}を使用して非インタラクティブPDFドキュメントをアセンブリする

Assembler Service API(Java)を使用して、非インタラクティブPDFドキュメントをアセンブリします。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-assembler-client.jarなどのクライアントJARファイルを含めます。

1. Assemblerクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用し、`AssemblerServiceClient`オブジェクトを渡して、`ServiceClientFactory`オブジェクトを作成します。

1. 既存のDDXドキュメントの参照。

   * コンストラクターを使用し、DDXファイルの場所を指定する文字列値を渡して、DDXドキュメントを表す`java.io.FileInputStream`オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. インタラクティブPDFドキュメントの参照

   * コンストラクターを使用し、インタラクティブPDFドキュメントの場所を渡して、`java.io.FileInputStream`オブジェクトを作成します。
   * `com.adobe.idp.Document`オブジェクトを作成し、PDFドキュメントを含む`java.io.FileInputStream`オブジェクトを渡します。 この`com.adobe.idp.Document`オブジェクトは`invokeOneDocument`メソッドに渡されます。

1. 実行時オプションを設定します。

   * コンストラクターを使用して、実行時オプションを格納する`AssemblerOptionSpec`オブジェクトを作成します。
   * `AssemblerOptionSpec`オブジェクトに属するメソッドを呼び出して、ビジネス要件に合うように実行時オプションを設定します。 例えば、エラーが発生した場合にジョブの処理を続行するようにAssemblerサービスに指示するには、`AssemblerOptionSpec`オブジェクトの`setFailOnError`メソッドを呼び出し、`false`を渡します。

1. PDFドキュメントをアセンブリします。

   `AssemblerServiceClient`オブジェクトの`invokeOneDocument`メソッドを呼び出し、次の値を渡します。

   * DDXドキュメントを表す`com.adobe.idp.Document`オブジェクトです。 このDDXドキュメントにPDFソース要素の値`inDoc`が含まれていることを確認してください。
   * インタラクティブPDFドキュメントを含む`com.adobe.idp.Document`オブジェクトです。
   * デフォルトのフォントとジョブログレベルを含む、実行時のオプションを指定する`com.adobe.livecycle.assembler.client.AssemblerOptionSpec`オブジェクト。

   `invokeOneDocument`メソッドは、非インタラクティブPDFドキュメントを含む`com.adobe.idp.Document`オブジェクトを返します。

1. 非インタラクティブPDFドキュメントを保存します。

   * `java.io.File`オブジェクトを作成し、ファイル名の拡張子が.pdfであることを確認します。
   * `Document`オブジェクトの`copyToFile`メソッドを呼び出して、`Document`オブジェクトの内容をファイルにコピーします。 `invokeOneDocument`メソッドが返した`Document`オブジェクトを使用していることを確認してください。

* 「クイック開始（SOAPモード）:Java APIを使用した非インタラクティブPDFドキュメントのアセンブリ»

## WebサービスAPI {#assemble-a-non-interactive-pdf-document-using-the-web-service-api}を使用して非インタラクティブPDFドキュメントをアセンブリする

Assembler Service API（Webサービス）を使用して非インタラクティブPDFドキュメントをアセンブリします。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

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
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出して、バイト配列にストリームデータを入力します。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * `BLOB`オブジェクトに、`MTOM`フィールドにバイト配列の内容を割り当てて入力します。

1. インタラクティブPDFドキュメントの参照

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、入力PDFドキュメントの保存に使用されます。 この`BLOB`オブジェクトは、`invokeOneDocument`に引数として渡されます。
   * コンストラクターを呼び出し、入力PDFドキュメントーのファイルの場所と、ファイルを開くモードを表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得して、バイト配列のサイズを決定できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出して、バイト配列にストリームデータを入力します。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * `BLOB`オブジェクトに、`MTOM`フィールドにバイト配列の内容を割り当てて入力します。

1. 実行時オプションを設定します。

   * コンストラクターを使用して、実行時オプションを格納する`AssemblerOptionSpec`オブジェクトを作成します。
   * `AssemblerOptionSpec`オブジェクトに属するデータメンバに値を割り当てて、ビジネス要件に合うように実行時オプションを設定します。 例えば、エラーが発生した場合にジョブの処理を続行するようにAssemblerサービスに指示するには、`false`を`AssemblerOptionSpec`オブジェクトの`failOnError`データメンバーに割り当てます。

1. PDFドキュメントをアセンブリします。

   `AssemblerServiceClient`オブジェクトの`invokeOneDocument`メソッドを呼び出し、次の値を渡します。

   * DDXドキュメントを表す`BLOB`オブジェクト
   * インタラクティブPDFドキュメントを表す`BLOB`オブジェクト
   * 実行時オプションを指定する`AssemblerOptionSpec`オブジェクト

   `invokeOneDocument`メソッドは、非インタラクティブPDFドキュメントを含む`BLOB`オブジェクトを返します。

1. 非インタラクティブPDFドキュメントを保存します。

   * コンストラクターを呼び出し、非インタラクティブPDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `invokeOneDocument`メソッドが返した`BLOB`オブジェクトの内容を格納するバイト配列を作成します。 `BLOB`オブジェクトの`MTOM`フィールドの値を取得して、バイト配列を入力します。
   * コンストラクターを呼び出して`System.IO.FileStream`オブジェクトを渡し、`System.IO.BinaryWriter`オブジェクトを作成します。
   * `System.IO.BinaryWriter`オブジェクトの`Write`メソッドを呼び出し、バイト配列を渡すことで、バイト配列の内容をPDFファイルに書き込みます。

* 「クイック開始(MTOM):WebサービスAPIを使用した非インタラクティブPDFドキュメントのアセンブリ」を参照してください。

**関連トピック**

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
