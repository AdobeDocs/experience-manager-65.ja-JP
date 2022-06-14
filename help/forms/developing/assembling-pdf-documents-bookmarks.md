---
title: ブックマークを含む PDF ドキュメントのアセンブリ
seo-title: Assembling PDF Documents with Bookmarks
description: Assembler サービスを使用して、ブックマークを含む PDF ドキュメントを変更し、Java API と Web Service API を使用してブックマークを含めます。
seo-description: Use the Assembler service to modify a PDF document that does contain bookmarks to include bookmarks using the Java API and the Web Service API.
uuid: a306d2a6-0b12-4eb3-bff4-968a33417486
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9f4711a8-033c-4051-ab41-65a26838899b
role: Developer
exl-id: 2b938410-f51b-420b-b5d4-2ed13ec29c5a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2558'
ht-degree: 100%

---

# ブックマークを含む PDF ドキュメントのアセンブリ {#assembling-pdf-documents-with-bookmarks}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

ブックマークを含む PDF ドキュメントをアセンブリできます。 例えば、ブックマークが含まれていない PDF ドキュメントにブックマークを追加したいとします。 Assembler サービスを使用すると、ブックマークを含まない PDF ドキュメントを渡し、ブックマークを含む PDF ドキュメントを受け取ることができます。

ブックマークには、次のプロパティが含まれます。

* 画面にテキストとして表示されるタイトル。
* ユーザーがブックマークをクリックしたときの動作を指定するアクション。 ブックマークの一般的なアクションは、現在のドキュメント内の別の場所に移動するか、別の PDF ドキュメントを開くことですが、他のアクションを指定することもできます。

この説明では、次の DDX ドキュメントが使用されていると仮定します。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
       <PDF result="FinalDoc.pdf">
          <PDF source="Loan.pdf">
             <Bookmarks source="doc2" />
          </PDF>
       </PDF>
 </DDX>
```

この DDX ドキュメント内では、 source 属性に値 `Loan.pdf` が割り当てられています。この DDX ドキュメントは、1 つの PDF ドキュメントを Assembler サービスに渡すように指定します。 ブックマークを含む PDF ドキュメントをアセンブリする場合は、結果ドキュメント内のブックマークを説明するブックマーク XML ドキュメントを指定する必要があります。 ブックマーク XML ドキュメントを指定するには、`Bookmarks` 要素を DDX ドキュメント内で指定してください。

この DDX ドキュメントの例では、 `Bookmarks` 要素が値として `doc2` を指定しています。 この値は、Assembler サービスに渡される入力マップに `doc2` という名前のキーが含まれていることを示します。`doc2` キーの値はブックマーク XML ドキュメントを表す `com.adobe.idp.Document` 値です（詳しくは、[Assembler サービスと DDX リファレンス](https://www.adobe.com/go/learn_aemforms_ddx_63)の「ブックマーク言語」を参照）。

このトピックでは、次の XML ブックマーク言語を使用して、ブックマークを含む PDF ドキュメントをアセンブリします。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <Bookmarks xmlns="https://ns.adobe.com/pdf/bookmarks" version="1.0">
       <Bookmark>
          <Action>
             <Launch NewWindow="true">
                <File Name="C:\Adobe\LoanDetails.pdf" />
             </Launch>
          </Action>
         <Title>Open the Loan document</Title>
       </Bookmark>
 <Bookmark>
          <Action>
             <Launch>
                <Win Name="C:\WINDOWS\notepad.exe" />
             </Launch>
          </Action>
     <Title>Launch NotePad</Title>
       </Bookmark>
 </Bookmarks>
```

このブックマーク XML ドキュメント内には、ユーザーがブックマークをクリックしたときに実行されるアクションを定義する Action 要素があります。 Action 要素の下には、NotePad などのアプリケーションを起動し、アプリケーションファイルなどのファイルを開く Launch 要素があります。 PDF ファイルを開くには、開くファイルを指定する File 要素を使用する必要があります。 例えば、このセクションで指定したブックマーク XML ファイルでは、開くファイルの名前は LoanDetails.pdf です。

>[!NOTE]
>
>サポートされるアクションの詳細については、[Assembler サービスと DDX リファレンス](https://www.adobe.com/go/learn_aemforms_ddx_63)の「`Action` 要素」 を参照してください。

ここで指定した DDX ドキュメントとブックマーク XML ファイルを入力として指定した場合、Assembler サービスは、次のブックマークを含む PDF ドキュメントをアセンブルします。

![aw_aw_bmark](assets/aw_aw_bmark.png)

ユーザーが&#x200B;*ローンの詳細を開く*&#x200B;ブックマークをクリックすると、LoanDetails.pdf が開きます。 同様に、ユーザーが *NotePad を起動*&#x200B;ブックマークをクリックすると、NotePad が起動します。

>[!NOTE]
>
>このセクションを読む前に、Assembler サービスを使用した PDF ドキュメントのアセンブリに関する知識を身に付けておくことをお勧めします。 このセクションでは、入力ドキュメントを含むコレクションオブジェクトの作成や、返されたコレクションオブジェクトから結果を抽出する方法の学習など、概念については説明しません（[プログラムによる PDF ドキュメントの作成](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)を参照）。

>[!NOTE]
>
>Assembler サービスについて詳しくは、[AEM Formsサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

>[!NOTE]
>
>DDX ドキュメントについて詳しくは、[Assembler サービスと DDX リファレンス](https://www.adobe.com/go/learn_aemforms_ddx_63)を参照してください。

## 手順の概要 {#summary-of-steps}

ブックマークを含む PDF ドキュメントをアセンブリするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. PDF Assembler クライアントを作成します。
1. 既存の DDX ドキュメントを参照します。
1. ブックマークを追加する PDF ドキュメントを参照します。
1. ブックマーク XML ドキュメントを参照します。
1. Map コレクションに PDF ドキュメントとブックマーク XML ドキュメントを追加します。
1. 実行時オプションを設定します。
1. PDF ドキュメントをアセンブリします。
1. ブックマークを含む PDF ドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar（AEM Forms が JBoss にデプロイされている場合に必要）
* jbossall-client.jar（AEM Formsが JBoss にデプロイされている場合に必要）

AEM Forms が JBoss 以外のサポート対象の J2EE アプリケーションサーバーにデプロイされている場合は、adobe-utilities.jar ファイルと jbossall-client.jar ファイルを、AEM Forms がデプロイされている J2EE アプリケーションサーバーに固有の JAR ファイルに置き換える必要があります。 すべての AEM Forms JAR ファイルの場所については、[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。

**PDF Assembler クライアントの作成**

Assembler 操作をプログラムで実行する前に、Assembler サービスクライアントを作成する必要があります。

**既存の DDX ドキュメントの参照**

DDX ドキュメントを参照して、PDF ドキュメントをアセンブリする必要があります。 この DDX ドキュメントには `Bookmarks` 要素を含める必要があります。これは、ブックマークを含む PDF をアセンブルするよう Assembler サービスに指示します（このセクションで前述した DDX ドキュメントの例を参照）。

**ブックマークを追加する PDF ドキュメントの参照**

ブックマークを追加する PDF ドキュメントを参照します。 参照先のブックマークドキュメントに既に PDF が含まれているかどうかは関係ありません。 `Bookmarks` 要素が PDF ソース要素の子である場合、ブックマークは PDF ソースに既に存在する要素を置き換えます。 ただし、既存のブックマークを保持する場合は、 `Bookmarks` を PDF ソース要素の兄弟にしてください。例えば、次のようなシナリオを考えます。

```xml
 <PDF result="foo">
      <PDF source="inDoc"/>
      <Bookmarks source="doc2"/>
 </PDF>
```

**ブックマーク XML ドキュメントの参照**

新しいブックマークを含む PDF をアセンブリするには、ブックマーク XML ドキュメントを参照する必要があります。ブックマーク XML ドキュメントは、Map コレクションオブジェクト内の Assembler サービスに渡されます。（このセクションで前述したブックマーク XML ドキュメントを参照してください）。

>[!NOTE]
>
>詳しくは、[Assembler サービスと DDX リファレンス](https://www.adobe.com/go/learn_aemforms_ddx_63)にある「ブックマーク言語」を参照してください。

**PDF ドキュメントとブックマーク XML ドキュメントを Map コレクションに追加する**

ブックマークを追加する PDF ドキュメントと、ブックマーク XML ドキュメントの両方を Map コレクションに追加する必要があります。したがって、Map コレクションオブジェクトには、PDF ドキュメントとブックマーク XML ドキュメントという 2 つの要素が含まれます。

**実行時オプションの設定**

ジョブを実行する際の Assembler サービスの動作を制御する実行時オプションを設定できます。例えば、エラーが発生した場合にジョブの処理を続行するよう Assembler サービスに指示するオプションを設定できます。 設定できる実行時オプションについて詳しくは、[AEM Forms API リファレンス](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ja)にある `AssemblerOptionSpec` クラスリファレンスを参照してください。

**PDF ドキュメントのアセンブリ**

新しいブックマークを含む PDF ドキュメントをアセンブリするには、Assembler サービスの `invokeDDX` 操作を使用します。`invokeOneDocument` などといった Assembler サービスの他の操作ではなく `invokeDDX` 操作を使用する必要がある理由は、Assembler サービスでは、Map コレクションオブジェクト内に渡されるブックマーク XML ドキュメントが必要だからです。このオブジェクトは、`invokeDDX` 操作のパラメーターです。

**ブックマークを含む PDF ドキュメントの保存**

返された Map オブジェクトから結果を抽出し、対応する PDF ドキュメントを保存する必要があります。（[プログラムによる PDF ドキュメントのアセンブリ](/help/forms/developing/programmatically-assembling-pdf-documents.md)にある「結果の抽出」を参照してください）。

**関連トピック**

[AEM Forms Java ライブラリファイルの組み込み](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDF ドキュメントをプログラムで組み立てる](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java API を使用してブックマークとともに PDF ドキュメントをアセンブリする {#assemble-pdf-documents-with-bookmarks-using-the-java-api}

Assembler サービス API（Java）を使用して、ブックマークとともに PDF ドキュメントをアセンブリします。

1. プロジェクトファイルを含めます。

   adobe-livecycle-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. PDF Assembler クライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。（[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照）
   * コンストラクタを使用して `ServiceClientFactory` オブジェクトを渡すことによって、`AssemblerServiceClient` オブジェクトを作成します。

1. 既存の DDX ドキュメントを参照します。

   * コンストラクタを使用し、DDX ファイルの場所を指定する文字列値を渡すことによって、その DDX ドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクタを使用して `java.io.FileInputStream` オブジェクトを渡すことによって、`com.adobe.idp.Document` オブジェクトを作成します。

1. ブックマークを追加する PDF ドキュメントを参照します。

   * コンストラクタを使用し、PDF ドキュメントの場所を渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクタを使用し、PDF ドキュメントを含む `java.io.FileInputStream` オブジェクトを渡すことによって、`com.adobe.idp.Document` オブジェクトを作成します。

1. ブックマーク XML ドキュメントを参照します。

   * コンストラクタを使用し、ブックマーク XML ドキュメントを表す XML ファイルの場所を渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。
   * `com.adobe.idp.Document` オブジェクトを作成し、PDF ドキュメントを含む `java.io.FileInputStream` オブジェクトを渡します。

1. Map コレクションに PDF ドキュメントとブックマーク XML ドキュメントを追加します。

   * 入力 PDF ドキュメントとブックマーク XML ドキュメントの両方を格納するのに使用する `java.util.Map` オブジェクトを作成します。
   * `java.util.Map` オブジェクトの `put` メソッドを呼び出し、次の引数を渡すことによって、入力 PDF ドキュメントを追加します。

      * キー名を表す文字列値。この値は、DDX ドキュメントで指定された PDF ソース要素の値と一致している必要があります。
      * 入力 PDF ドキュメントを含む `com.adobe.idp.Document` オブジェクト。
   * `java.util.Map` オブジェクトの `put` メソッドを呼び出し、次の引数を渡すことによって、ブックマーク XML ドキュメントを追加します。

      * キー名を表す文字列値。この値は、DDX ドキュメントで指定されているブックマークソース要素の値と一致する必要があります。
      * ブックマーク XML ドキュメントを含む `com.adobe.idp.Document` オブジェクト。


1. 実行時オプションを設定します。

   * コンストラクタを使用して、実行時オプションを格納する `AssemblerOptionSpec` オブジェクトを作成します。
   * `AssemblerOptionSpec` オブジェクトに属するメソッドを呼び出して、ビジネス要件を満たすよう実行時オプションを設定します。例えば、エラーが発生してもジョブの処理を続行するよう Assembler サービスに指示するには、`AssemblerOptionSpec` オブジェクトの `setFailOnError` メソッドを呼び出して `false` を渡します。

1. PDF ドキュメントをアセンブリします。

   `AssemblerServiceClient` オブジェクトの `invokeDDX` メソッドを呼び出し、以下の必須の値を渡します。

   * 使用する DDX ドキュメントを表す `com.adobe.idp.Document` オブジェクト
   * 入力 PDF ドキュメントとブックマーク XML ドキュメントの両方を含む `java.util.Map` オブジェクト。
   * デフォルトのフォントやジョブログレベルを含む、実行時のオプションを指定する `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` オブジェクト

   `invokeDDX` メソッドは、ジョブの結果と例外（発生した場合）を含む `com.adobe.livecycle.assembler.client.AssemblerResult` オブジェクトを返します。

1. ブックマークを含む PDF ドキュメントを保存します。

   新しく作成した PDF ドキュメントを取得するには、次のアクションを実行します。

   * `AssemblerResult` オブジェクトの `getDocuments` メソッドを呼び出します。これにより、`java.util.Map` オブジェクトが返されます。
   * 結果の `com.adobe.idp.Document` オブジェクトが見つかるまで `java.util.Map` オブジェクトを反復処理します（DDX ドキュメントで指定された PDF 結果要素を使用して、ドキュメントを取得できます）。
   * `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを呼び出して、PDF ドキュメントを抽出します。

**関連トピック**

[クイックスタート（SOAP モード）：Java API を使用した、ブックマークを含む PDF ドキュメントのアセンブリ](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-documents-with-bookmarks-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Web サービス API を使用した、ブックマークを含む PDF ドキュメントのアセンブリ {#assemble-pdf-documents-with-bookmarks-using-the-web-service-api}

Assembler Service API（web サービス）を使用して、ブックマークを含む PDF ドキュメントをアセンブリします。

1. プロジェクトファイルを含めます。

   MTOM を使用する Microsoft .NET プロジェクトを作成します。WSDL 定義 `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1` を使用するようにします。

   >[!NOTE]
   >
   >`localhost` を、AEM Forms をホストするサーバーの IP アドレスに置換します。

1. PDF Assembler クライアントを作成します。

   * デフォルトのコンストラクターを使用して、`AssemblerServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して、`AssemblerServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/AssemblerService?blob=mtom`）。`lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。
   * `AssemblerServiceClient.Endpoint.Binding` フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` フィールドを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `AssemblerServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `AssemblerServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
      * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` をフィールド `BasicHttpBindingSecurity.Security.Mode` に割り当てます。

1. 既存の DDX ドキュメントを参照します。

   * コンストラクターを使用して `BLOB` オブジェクトを作成します。`BLOB` オブジェクトは、DDX ドキュメントを格納するために使用されます。
   * コンストラクターを呼び出し、DDX ドキュメントのファイルの場所とファイルを開くモードを表す文字列値を渡すことによって、`System.IO.FileStream` オブジェクトを作成します。
   * `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することで、バイト配列のサイズを決定できます。
   * `System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出し、バイト配列、開始位置、読み取るストリーム長を渡すことにより、バイト配列にストリームデータを入力します。
   * `MTOM` フィールドにバイト配列の内容を割り当てて、`BLOB` オブジェクトにデータを入力します。

1. ブックマークを追加する PDF ドキュメントを参照します。

   * コンストラクターを使用して `BLOB` オブジェクトを作成します。`BLOB` オブジェクトは、入力 PDF を格納するために使用されます。
   * コンストラクターを呼び出し、入力 PDF ドキュメントのファイルの場所とファイルを開くモードを表す文字列値を渡すことによって、`System.IO.FileStream` オブジェクトを作成します。
   * `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することで、バイト配列のサイズを決定できます。
   * `System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出し、バイト配列、開始位置、読み取るストリーム長を渡すことにより、バイト配列にストリームデータを入力します。
   * `MTOM` フィールドにバイト配列のコンテンツを割り当てて、`BLOB` オブジェクトを設定します。

1. ブックマーク XML ドキュメントを参照します。

   * コンストラクターを使用して `BLOB` オブジェクトを作成します。`BLOB` オブジェクトは、ブックマーク XML ドキュメントを格納するために使用されます。
   * コンストラクターを呼び出し、入力 PDF ドキュメントのファイルの場所とファイルを開くモードを表す文字列値を渡すことによって、`System.IO.FileStream` オブジェクトを作成します。
   * `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することで、バイト配列のサイズを決定できます。
   * `System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出し、バイト配列、開始位置、読み取るストリーム長を渡すことにより、バイト配列にストリームデータを入力します。
   * `MTOM` フィールドにバイト配列の内容を割り当てることで、`BLOB` オブジェクトにデータを入力します。

1. Map コレクションに PDF ドキュメントとブックマーク XML ドキュメントを追加します。

   * `MyMapOf_xsd_string_To_xsd_anyType` オブジェクトを作成します。このコレクションオブジェクトは、入力された PDF ドキュメントとブックマーク XML ドキュメントを保存するために使用されます。
   * 各入力 PDF ドキュメントとブックマーク XML ドキュメントに対して、`MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトを作成します。
   * `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトの `key` フィールドに、キー名を表す文字列値を割り当てます。この値は、DDX ドキュメントで指定された PDF ソース要素の値と一致している必要があります。
   * PDF ドキュメントを格納する `BLOB` オブジェクトを `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトの `value` フィールドに入力します。
   * `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトを `MyMapOf_xsd_string_To_xsd_anyType` オブジェクトに追加します。`MyMapOf_xsd_string_To_xsd_anyType` オブジェクトの `Add` メソッドを呼び出し、`MyMapOf_xsd_string_To_xsd_anyType` オブジェクトを渡します（このタスクは、入力した PDF ドキュメントとブックマーク XML ドキュメントそれぞれについておこないます）。

1. 実行時オプションを設定します。

   * ランタイムオプションを格納する `AssemblerOptionSpec` オブジェクトをコンストラクタで作成します。
   * `AssemblerOptionSpec` オブジェクトに属するデータメンバーに値を割り当てることで、ビジネス要件に応じたランタイムオプションを設定します。例えば、エラーが発生したときに Assembler サービスにジョブの処理を継続するように指示するには、`AssemblerOptionSpec` オブジェクトの `failOnError` データメンバーに `false` を入力します。

1. PDF ドキュメントをアセンブリします。

   `AssemblerServiceClient` オブジェクトの `invokeDDX` メソッドを呼び出し、次の値を渡します。

   * DDX ドキュメントを表す `BLOB` オブジェクト
   * 入力ドキュメントを格納する `MyMapOf_xsd_string_To_xsd_anyType` 配列
   * ランタイムオプションを指定する `AssemblerOptionSpec` オブジェクト

   `invokeDDX` メソッドは、ジョブの結果や発生した例外を含む `AssemblerResult` オブジェクトを返します。

1. ブックマークを含む PDF ドキュメントを保存します。

   新しく作成した PDF ドキュメントを取得するには、次のアクションを実行します。

   * `AssemblerResult` オブジェクトの `documents` フィールドにアクセスし、結果の PDF ドキュメントを含む `Map` オブジェクトにアクセスします。
   * 結果のドキュメントの名前と一致するキーが見つかるまで、`Map` オブジェクトを繰り返し実行します。そして、その配列メンバーの `value` を `BLOB` にキャストします。
   * PDF ドキュメントの `BLOB` オブジェクトの `MTOM` フィールドにアクセスして、そのドキュメントを表すバイナリデータを抽出します。これにより、PDF ファイルに書き出すことができるバイト配列が返されます。

**関連トピック**

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
