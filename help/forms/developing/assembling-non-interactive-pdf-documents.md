---
title: 非インタラクティブ PDF ドキュメントの作成
seo-title: Assembling Non-Interactive PDF Documents
description: Java API および web サービス API を使用して非インタラクティブ PDF ドキュメントを作成するには、非インタラクティブ PDF フォームを入力として使用します。
seo-description: Use a non-interactive PDF form as input to assemble a non-interactive PDF document using the Java API and Web Service API.
uuid: 0c7adeb4-9a3a-4ec5-ba33-c3642928d4ea
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8a75c201-bd88-4809-be08-69de94656489
role: Developer
exl-id: 4677b9e5-3811-4de3-b4f4-9574b5898486
source-git-commit: 135f50cc80f8bb449b2f1621db5e2564f5075968
workflow-type: ht
source-wordcount: '1775'
ht-degree: 100%

---

# 非インタラクティブ PDF ドキュメントの作成 {#assembling-non-interactive-pdf-documents}

非インタラクティブ PDF ドキュメントは、インタラクティブ PDF フォームを入力として使用することで作成できます。つまり、ユーザーがフィールドにデータを入力できるフォームがあるとします。そのフォームを Assembler サービスに渡すと、ユーザーがフィールドにデータを入力できない PDF ドキュメントを Assembler サービスから受け取ることができます。このドキュメントが非インタラクティブ PDF フォームです。例えば、インタラクティブなフォームである住宅ローン申し込みフォームを次の図に示します。

この説明では、次の DDX ドキュメントが使用されていると仮定します。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDF result="out.pdf">
        <PDF source="inDoc"/>
        <NoXFA/>
      </PDF>
 </DDX>
```

この DDX ドキュメント内では、source 属性に値 `inDoc` が割り当てられていることに着目してください。Assembler サービスに渡す入力 PDF ドキュメントが 1 つのみで、返されるのも 1 つの PDF ドキュメントであり、`invokeOneDocument` 操作を呼び出す場合は、値 `inDoc` を PDF の source 属性に割り当てます。`invokeOneDocument` 操作を呼び出す際は、`inDoc` 値が、DDX ドキュメントに指定する必要がある事前定義済みキーです。

これに対し、2 つ以上の入力 PDF ドキュメントを Assembler サービスに渡す場合は、`invokeDDX` 操作を呼び出すことができます。この場合は、入力 PDF ドキュメントのファイル名を `source` 属性に割り当てます。

この DDX ドキュメントには `NoXFA` 要素が含まれており、この要素は Assembler サービスに非インタラクティブ PDF ドキュメントを返すよう指示します。

Assembler サービスは、入力 PDF ドキュメントが Acrobat フォームまたは静的 XFA フォームに基づいていれば、Output サービスが AEM Forms インストール環境に含まれていなくても、非インタラクティブ PDF ドキュメントを作成することができます。ただし、入力 PDF ドキュメントが動的 XFA フォームの場合は、Output サービスが AEM Forms インストール環境に含まれている必要があります。動的 XFA フォームの作成時に Output サービスが AEM Forms インストール環境に含まれていない場合は、例外がスローされます。詳しくは、[ドキュメント Output ストリームの作成](/help/forms/developing/creating-document-output-streams.md)を参照してください。

>[!NOTE]
>
>このセクションを読む前に、Assembler サービスを使用した PDF ドキュメントのアセンブリに関する知識を身に付けておくことをお勧めします。このセクションでは、入力ドキュメントを含むコレクションオブジェクトの作成や、返されたコレクションオブジェクトから結果を抽出する方法の学習など、概念については説明しません（[プログラムによる PDF ドキュメントの作成](/help/forms/developing/programmatically-assembling-pdf-documents.md)を参照）。

>[!NOTE]
>
>Assembler サービスについて詳しくは、[AEM Formsサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

>[!NOTE]
>
>DDX ドキュメントについて詳しくは、[Assembler サービスと DDX リファレンス](https://www.adobe.com/go/learn_aemforms_ddx_63)を参照してください。

## 手順の概要 {#summary-of-steps}

非インタラクティブ PDF ドキュメントを作成するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. PDF Assembler クライアントを作成します。
1. 既存の DDX ドキュメントを参照します。
1. インタラクティブ PDF ドキュメントを参照します。
1. 実行時オプションを設定します。
1. PDF ドキュメントをアセンブリします。
1. 非インタラクティブ PDF ドキュメントを保存します。

**プロジェクトファイルのインクルード**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar（AEM Forms が JBoss にデプロイされている場合に必要）
* jbossall-client.jar（AEM Formsが JBoss にデプロイされている場合に必要）

AEM Forms が JBoss 以外のサポート対象の J2EE アプリケーションサーバーにデプロイされている場合は、adobe-utilities.jar ファイルと jbossall-client.jar ファイルを、AEM Forms がデプロイされている J2EE アプリケーションサーバーに固有の JAR ファイルに置き換える必要があります。

**Assembler クライアントの作成**

Assembler 操作をプログラムで実行する前に、Assembler サービスクライアントを作成する必要があります。

**既存の DDX ドキュメントの参照**

DDX ドキュメントを参照して、PDF ドキュメントをアセンブリする必要があります。この DDX ドキュメントには `NoXFA` 要素が含まれている必要があり、この要素は Assembler サービスに非インタラクティブ PDF ドキュメントを返すよう指示します。

**インタラクティブ PDF ドキュメントの参照**

非インタラクティブ PDF ドキュメントを取得するには、インタラクティブ PDF ドキュメントを参照して Assembler サービスに渡す必要があります。

**実行時オプションの設定**

ジョブを実行する際の Assembler サービスの動作を制御する実行時オプションを設定できます。例えば、エラーが発生した場合にジョブの処理を続行するよう Assembler サービスに指示するオプションを設定できます。

**PDF ドキュメントの作成**

Assembler サービスクライアントの作成、DDX ドキュメントの参照、インタラクティブ PDF ドキュメントの参照および実行時オプションの設定が完了したら、`invokeOneDocument` 操作を呼び出すことができます。Assembler サービスに渡す入力 PDF ドキュメントは 1 つだけで、返されるドキュメントも 1 つなので、`invokeDDX` 操作ではなく `invokeOneDocument` 操作を使用できます。

**非インタラクティブ PDF ドキュメントの保存**

Assembler サービスに渡す PDF ドキュメントが 1 つのみであれば、コレクションオブジェクトではなく 1 つのドキュメントが Assembler サービスから返されます。つまり、`invokeOneDocument` 操作を呼び出すと、1 つのドキュメントが返されます。このセクションで参照している DDX ドキュメントには、非インタラクティブ PDF ドキュメントを作成する指示が含まれているので、Assembler サービスは、PDF ファイルとして保存できる非インタラクティブ PDF ドキュメントを返します。

**関連トピック**

[AEM Forms Java ライブラリファイルの組み込み](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDF ドキュメントをプログラムで組み立てる](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java API を使用した非インタラクティブ PDF ドキュメントの作成 {#assemble-a-non-interactive-pdf-document-using-the-java-api}

Assembler サービス API（Java）を使用して、非インタラクティブ PDF ドキュメントを作成します。

1. プロジェクトファイルを含めます。

   adobe-livecycle-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. Assembler クライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して `ServiceClientFactory` オブジェクトを渡すことにより、`AssemblerServiceClient` オブジェクトを作成します。

1. 既存の DDX ドキュメントを参照します。

   * コンストラクタを使用し、DDX ファイルの場所を指定する文字列値を渡すことによって、その DDX ドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. インタラクティブ PDF ドキュメントを参照します。

   * コンストラクターを使用し、インタラクティブ PDF ドキュメントの場所を渡すことにより、`java.io.FileInputStream` オブジェクトを作成します。
   * `com.adobe.idp.Document` オブジェクトを作成し、PDF ドキュメントを含んだ `java.io.FileInputStream` オブジェクトを渡します。この `com.adobe.idp.Document` オブジェクトが `invokeOneDocument` メソッドに渡されます。

1. 実行時オプションを設定します。

   * コンストラクタを使用して、実行時オプションを格納する `AssemblerOptionSpec` オブジェクトを作成します。
   * `AssemblerOptionSpec` オブジェクトに属するメソッドを呼び出して、ビジネス要件を満たすよう実行時オプションを設定します。例えば、エラーが発生してもジョブの処理を続行するよう Assembler サービスに指示するには、`AssemblerOptionSpec` オブジェクトの `setFailOnError` メソッドを呼び出して `false` を渡します。

1. PDF ドキュメントをアセンブリします。

   `AssemblerServiceClient` オブジェクトの `invokeOneDocument` メソッドを呼び出して、次の値を渡します。

   * DDX ドキュメントを表す `com.adobe.idp.Document` オブジェクト。この DDX ドキュメントに PDF ソース要素の値 `inDoc` が含まれていることを確認してください。
   * インタラクティブ PDF ドキュメントを格納する `com.adobe.idp.Document` オブジェクト。
   * デフォルトのフォントやジョブログレベルを含む、実行時のオプションを指定する `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` オブジェクト。

   `invokeOneDocument` メソッドは、非インタラクティブ PDF ドキュメントを含む `com.adobe.idp.Document` オブジェクトを返します。

1. 非インタラクティブ PDF ドキュメントを保存します。

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が .pdf であることを確認します。
   * `Document` オブジェクトの `copyToFile` メソッドを呼び出して、`Document` オブジェクトのコンテンツをファイルにコピーします。必ず `invokeOneDocument` メソッドが返した `Document` オブジェクトを使用するように確認します。

* 「クイックスタート（SOAP モード）：Java API を使用した PDF ドキュメントのアセンブリ」

## Web サービス API を使用した非インタラクティブ PDF ドキュメントのアセンブリ {#assemble-a-non-interactive-pdf-document-using-the-web-service-api}

Assembler Service API（web サービス）を使用して、非インタラクティブ PDF ドキュメントをアセンブリします。

1. プロジェクトファイルを含めます。

   MTOM を使用する Microsoft .NET プロジェクトを作成します。WSDL 定義 `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1` を使用するようにします。

   >[!NOTE]
   >
   >`localhost` を、AEM Forms をホストするサーバーの IP アドレスに置換します。

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
   * `System.IO.FileStream` オブジェクトのコンテンツを保存するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することでバイト配列のサイズを決定することができます。
   * `System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出して、バイト配列にストリームデータを入力します。読み取り対象のバイト配列、開始位置、ストリーム長を渡します。
   * `MTOM` フィールドにバイト配列のコンテンツを割り当てて、`BLOB`オ ブジェクトを入力します。

1. インタラクティブ PDF ドキュメントを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB` オブジェクトは、入力 PDF ドキュメントを格納するために使用します。この `BLOB` オブジェクトは引数として `invokeOneDocument` に渡されます。
   * コンストラクターを呼び出し、入力 PDF ドキュメントのファイルの場所とファイルを開くモードを表す文字列値を渡すことにより、`System.IO.FileStream` オブジェクトを作成します。
   * `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することでバイト配列のサイズを決定することができます。
   * `System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出して、バイト配列にストリームデータを入力します。読み取り対象のバイト配列、開始位置、ストリーム長を渡します。
   * `MTOM` フィールドを割り当てることにより、`BLOB` オブジェクトにバイト配列の内容を入力します。

1. 実行時オプションを設定します。

   * ランタイムオプションを格納する `AssemblerOptionSpec` オブジェクトをコンストラクタで作成します。
   * `AssemblerOptionSpec` オブジェクトに属するデータメンバーに値を割り当てることで、ビジネス要件に応じたランタイムオプションを設定します。例えば、エラーが発生したときに Assembler サービスにジョブの処理を継続するように指示するには、`AssemblerOptionSpec` オブジェクトの `failOnError` データメンバーに `false` を入力します。

1. PDF ドキュメントをアセンブリします。

   `AssemblerServiceClient` オブジェクトの `invokeOneDocument` メソッドを呼び出し、次の値を渡します。

   * DDX ドキュメントを表す `BLOB` オブジェクト
   * インタラクティブ PDF ドキュメントを表す `BLOB` オブジェクト
   * 実行時のオプションを指定する `AssemblerOptionSpec` オブジェクト

   `invokeOneDocument` メソッドは、非インタラクティブ PDF キュメントを含む `BLOB` オブジェクトを返します。

1. 非インタラクティブ PDF ドキュメントを保存します。

   * `System.IO.FileStream` オブジェクトを作成するには、そのコンストラクターを呼び出し、非インタラクティブ PDF ドキュメントのファイルの場所とファイルを開くモードを表す文字列値を渡します。
   * `invokeOneDocument` メソッドから返された `BLOB` オブジェクトのコンテンツを格納するバイト配列を作成します。`BLOB` オブジェクトの `MTOM` フィールドの値を取得して、バイト配列に入力します。
   * コンストラクターを呼び出し、`System.IO.FileStream` オブジェクトを渡すことによって、`System.IO.BinaryWriter` オブジェクトを作成します。
   * `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを呼び出して、バイト配列を渡すことによって、バイト配列の内容を PDF ファイルに書き込みます。

* 「クイックスタート（MTOM）：web サービス API を使用した非インタラクティブ PDF ドキュメントのアセンブリ」

**関連トピック**

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
