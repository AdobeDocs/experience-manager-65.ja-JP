---
title: 非インタラクティブPDFドキュメントのアセンブリ
seo-title: 非インタラクティブPDFドキュメントのアセンブリ
description: Java APIおよびWebサービスAPIを使用して非インタラクティブPDFドキュメントをアセンブリするには、非インタラクティブPDFフォームを入力として使用します。
seo-description: Java APIおよびWebサービスAPIを使用して非インタラクティブPDFドキュメントをアセンブリするには、非インタラクティブPDFフォームを入力として使用します。
uuid: 0c7adeb4-9a3a-4ec5-ba33-c3642928d4ea
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8a75c201-bd88-4809-be08-69de94656489
role: Developer
exl-id: 4677b9e5-3811-4de3-b4f4-9574b5898486
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1800'
ht-degree: 2%

---

# 非インタラクティブPDFドキュメントのアセンブリ{#assembling-non-interactive-pdf-documents}

インタラクティブPDFフォームを入力として使用する場合、非インタラクティブPDFドキュメントをアセンブリできます。 つまり、ユーザーがフィールドにデータを入力するためのフォームがあるとします。 そのフォームをAssemblerサービスに渡すと、AssemblerサービスがPDFドキュメントを返すので、ユーザーはフィールドにデータを入力できません。 このドキュメントは非インタラクティブPDFフォームです。 例えば、次の図はインタラクティブなフォームを表す住宅ローン申し込みフォームを示しています。

この説明では、次のDDXドキュメントが使用されているとします。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDF result="out.pdf">
        <PDF source="inDoc"/>
        <NoXFA/>
      </PDF>
 </DDX>
```

このDDXドキュメント内で、ソース属性に値`inDoc`が割り当てられていることに注意してください。 1つの入力PDFドキュメントのみがAssemblerサービスに渡され、1つのPDFドキュメントが返された場合に、`invokeOneDocument`操作を呼び出して、値`inDoc`をPDFソース属性に割り当てます。 `invokeOneDocument`操作を呼び出す場合、`inDoc`値は事前定義済みのキーで、DDXドキュメントで指定する必要があります。

これに対し、2つ以上の入力PDFドキュメントをAssemblerサービスに渡す場合は、`invokeDDX`操作を呼び出すことができます。 この場合、入力PDFドキュメントのファイル名を`source`属性に割り当てます。

このDDXドキュメントには`NoXFA`要素が含まれています。この要素は、非インタラクティブPDFドキュメントを返すようAssemblerサービスに指示します。

Assemblerサービスは、入力PDFドキュメントがAcrobatフォームまたは静的XFAフォームに基づいている場合、AEM formsインストールの一部としてOutputサービスを使用せずに、非インタラクティブPDFドキュメントをアセンブリできます。 ただし、入力PDFドキュメントが動的XFAフォームの場合は、OutputサービスをAEM formsのインストールに含める必要があります。 動的XFAフォームのアセンブリ時にOutputサービスがAEM formsインストールの一部でない場合は、例外が発生します。 [ドキュメント出力ストリームの作成](/help/forms/developing/creating-document-output-streams.md)を参照してください。

>[!NOTE]
>
>この節を読む前に、Assemblerサービスを使用したPDFドキュメントのアセンブリについて理解しておくことをお勧めします。 この節では、入力ドキュメントを含むコレクションオブジェクトの作成や、返されたコレクションオブジェクトから結果を抽出する方法の学習など、概念については説明しません。 （[PDFドキュメントのプログラムによるアセンブリ](/help/forms/developing/programmatically-assembling-pdf-documents.md)を参照）。

>[!NOTE]
>
>Assemblerサービスについて詳しくは、『AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)向けサービスリファレンス』を参照してください。[

>[!NOTE]
>
>DDXドキュメントについて詳しくは、『[AssemblerサービスとDDXリファレンス](https://www.adobe.com/go/learn_aemforms_ddx_63)』を参照してください。

## 手順の概要{#summary-of-steps}

非インタラクティブPDFドキュメントをアセンブリするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. PDFアセンブラークライアントを作成します。
1. 既存のDDXドキュメントの参照
1. インタラクティブPDFドキュメントを参照します。
1. 実行時オプションを設定します。
1. PDFドキュメントをアセンブリします。
1. 非インタラクティブPDFドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用する場合は、プロキシファイルを必ず含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(AEM FormsをJBossにデプロイする場合に必要)
* jbossall-client.jar(AEM FormsをJBossにデプロイする場合に必要)

AEM FormsがJBoss以外のサポート対象のJ2EEアプリケーションサーバーにデプロイされている場合は、adobe-utilities.jarファイルとjbossall-client.jarファイルを、AEM FormsがデプロイされているJ2EEアプリケーションサーバーに固有のJARファイルに置き換える必要があります。

**Assemblerクライアントの作成**

プログラムでAssembler操作を実行する前に、Assemblerサービスクライアントを作成する必要があります。

**既存のDDXドキュメントの参照**

PDFドキュメントをアセンブリするには、DDXドキュメントを参照する必要があります。 このDDXドキュメントには、`NoXFA`要素が含まれている必要があります。この要素は、非インタラクティブPDFドキュメントを返すようAssemblerサービスに指示します。

**インタラクティブPDFドキュメントの参照**

非インタラクティブPDFドキュメントを戻すには、インタラクティブPDFドキュメントを参照してAssemblerサービスに渡す必要があります。

**実行時オプションの設定**

ジョブの実行中にAssemblerサービスの動作を制御する実行時オプションを設定できます。 例えば、エラーが発生した場合にジョブの処理を続行するようAssemblerサービスに指示するオプションを設定できます。

**PDFドキュメントのアセンブリ**

Assemblerサービスクライアントを作成し、DDXドキュメントを参照し、インタラクティブPDFドキュメントを参照し、実行時オプションを設定した後、`invokeOneDocument`操作を呼び出すことができます。 入力PDFドキュメントが1つだけAssemblerサービスに渡され、1つのドキュメントが返されるので、`invokeDDX`操作とは異なり、`invokeOneDocument`操作を使用できます。

**非インタラクティブPDFドキュメントの保存**

Assemblerサービスに渡されるPDFドキュメントが1つだけの場合、Assemblerサービスは、コレクションオブジェクトではなく1つのドキュメントを返します。 つまり、`invokeOneDocument`操作を呼び出すと、1つのドキュメントが返されます。 この節で参照されるDDXドキュメントには、非インタラクティブPDFドキュメントの作成手順が含まれているので、Assemblerサービスは、PDFファイルとして保存できる非インタラクティブPDFドキュメントを返します。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDFドキュメントのプログラムによるアセンブリ](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java API {#assemble-a-non-interactive-pdf-document-using-the-java-api}を使用した非インタラクティブPDFドキュメントのアセンブリ

AssemblerサービスAPI(Java)を使用して非インタラクティブPDFドキュメントをアセンブリします。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-assembler-client.jarなどのクライアントJARファイルを含めます。

1. Assemblerクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して`AssemblerServiceClient`オブジェクトを渡し、`ServiceClientFactory`オブジェクトを作成します。

1. 既存のDDXドキュメントの参照

   * コンストラクターを使用し、DDXファイルの場所を指定する文字列値を渡して、DDXドキュメントを表す`java.io.FileInputStream`オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. インタラクティブPDFドキュメントを参照します。

   * コンストラクターを使用してインタラクティブPDFドキュメントの場所を渡し、`java.io.FileInputStream`オブジェクトを作成します。
   * `com.adobe.idp.Document`オブジェクトを作成し、PDFドキュメントを含む`java.io.FileInputStream`オブジェクトを渡します。 この`com.adobe.idp.Document`オブジェクトは、`invokeOneDocument`メソッドに渡されます。

1. 実行時オプションを設定します。

   * コンストラクターを使用して、実行時オプションを格納する`AssemblerOptionSpec`オブジェクトを作成します。
   * `AssemblerOptionSpec`オブジェクトに属するメソッドを呼び出して、ビジネス要件に合った実行時オプションを設定します。 例えば、エラーが発生したときにジョブの処理を続行するようにAssemblerサービスに指示するには、`AssemblerOptionSpec`オブジェクトの`setFailOnError`メソッドを呼び出し、`false`を渡します。

1. PDFドキュメントをアセンブリします。

   `AssemblerServiceClient`オブジェクトの`invokeOneDocument`メソッドを呼び出し、次の値を渡します。

   * DDXドキュメントを表す`com.adobe.idp.Document`オブジェクト。 このDDXドキュメントにPDFソース要素の値`inDoc`が含まれていることを確認します。
   * インタラクティブPDFドキュメントを格納する`com.adobe.idp.Document`オブジェクト。
   * デフォルトのフォントやジョブのログレベルを含む、実行時のオプションを指定する`com.adobe.livecycle.assembler.client.AssemblerOptionSpec`オブジェクト。

   `invokeOneDocument`メソッドは、非インタラクティブPDFドキュメントを含む`com.adobe.idp.Document`オブジェクトを返します。

1. 非インタラクティブPDFドキュメントを保存します。

   * `java.io.File`オブジェクトを作成し、ファイル名拡張子が.pdfであることを確認します。
   * `Document`オブジェクトの`copyToFile`メソッドを呼び出して、`Document`オブジェクトの内容をファイルにコピーします。 `invokeOneDocument`メソッドが返す`Document`オブジェクトを使用していることを確認します。

* 「クイックスタート（SOAPモード）:Java APIを使用した非インタラクティブPDFドキュメントのアセンブリ»

## WebサービスAPI {#assemble-a-non-interactive-pdf-document-using-the-web-service-api}を使用した非インタラクティブPDFドキュメントのアセンブリ

AssemblerサービスAPI（Webサービス）を使用して非インタラクティブPDFドキュメントをアセンブリします。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

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
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出して、バイト配列にストリームデータを入力します。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * `BLOB`オブジェクトの`MTOM`フィールドにバイト配列の内容を割り当てて、オブジェクトを設定します。

1. インタラクティブPDFドキュメントを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、入力PDFドキュメントの保存に使用されます。 この`BLOB`オブジェクトは、引数として`invokeOneDocument`に渡されます。
   * コンストラクターを呼び出し、入力PDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得することで、バイト配列のサイズを判断できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出して、バイト配列にストリームデータを入力します。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * `BLOB`オブジェクトの`MTOM`フィールドにバイト配列の内容を割り当てて、オブジェクトを設定します。

1. 実行時オプションを設定します。

   * コンストラクターを使用して、実行時オプションを格納する`AssemblerOptionSpec`オブジェクトを作成します。
   * `AssemblerOptionSpec`オブジェクトに属するデータメンバーに値を割り当てて、ビジネス要件に合った実行時オプションを設定します。 例えば、エラーが発生したときにジョブの処理を続行するようにAssemblerサービスに指示するには、`false`を`AssemblerOptionSpec`オブジェクトの`failOnError`データメンバーに割り当てます。

1. PDFドキュメントをアセンブリします。

   `AssemblerServiceClient`オブジェクトの`invokeOneDocument`メソッドを呼び出し、次の値を渡します。

   * DDXドキュメントを表す`BLOB`オブジェクト
   * インタラクティブPDFドキュメントを表す`BLOB`オブジェクト
   * 実行時オプションを指定する`AssemblerOptionSpec`オブジェクト

   `invokeOneDocument`メソッドは、非インタラクティブPDFドキュメントを含む`BLOB`オブジェクトを返します。

1. 非インタラクティブPDFドキュメントを保存します。

   * コンストラクターを呼び出し、非インタラクティブPDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `invokeOneDocument`メソッドが返した`BLOB`オブジェクトの内容を格納するバイト配列を作成します。 `BLOB`オブジェクトの`MTOM`フィールドの値を取得して、バイト配列を設定します。
   * コンストラクターを呼び出し、`System.IO.FileStream`オブジェクトを渡して、`System.IO.BinaryWriter`オブジェクトを作成します。
   * `System.IO.BinaryWriter`オブジェクトの`Write`メソッドを呼び出し、バイト配列を渡すことにより、バイト配列の内容をPDFファイルに書き込みます。

* 「クイックスタート(MTOM):WebサービスAPIを使用した非インタラクティブPDFドキュメントのアセンブリ」を参照してください。

**関連トピック**

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
