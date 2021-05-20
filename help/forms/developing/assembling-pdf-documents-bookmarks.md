---
title: しおりを使用したPDFドキュメントのアセンブリ
seo-title: しおりを使用したPDFドキュメントのアセンブリ
description: Assemblerサービスを使用して、ブックマークを含むPDFドキュメントを変更し、Java APIとWebサービスAPIを使用してブックマークを含めます。
seo-description: Assemblerサービスを使用して、ブックマークを含むPDFドキュメントを変更し、Java APIとWebサービスAPIを使用してブックマークを含めます。
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
source-wordcount: '2588'
ht-degree: 2%

---

# しおり{#assembling-pdf-documents-with-bookmarks}によるPDFドキュメントのアセンブリ

**このドキュメントのサンプルと例は、JEE上のAEM Forms環境に限られています。**

しおりを含むPDFドキュメントをアセンブリできます。 例えば、しおりを含まないPDFドキュメントがあり、しおりを指定して変更するとします。 Assemblerサービスを使用すると、しおりを含まないPDFドキュメントにそのドキュメントを渡し、しおりを含むPDFドキュメントに戻すことができます。

ブックマークには、次のプロパティが含まれます。

* 画面にテキストとして表示されるタイトル。
* ユーザーがブックマークをクリックした場合の動作を指定するアクション。 ブックマークの一般的なアクションは、現在のドキュメント内の別の場所に移動するか、別のPDFドキュメントを開くことですが、他のアクションを指定することもできます。

この説明では、次のDDXドキュメントが使用されているとします。

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

このDDXドキュメント内で、ソース属性に値`Loan.pdf`が割り当てられていることに注意してください。 このDDXドキュメントは、単一のPDFドキュメントがAssemblerサービスに渡されるように指定します。 しおりを含むPDFドキュメントをアセンブリする場合は、結果ドキュメント内のしおりを説明するしおりXMLドキュメントを指定する必要があります。 ブックマークXMLドキュメントを指定するには、DDXドキュメントで`Bookmarks`要素が指定されていることを確認します。

この例のDDXドキュメントでは、 `Bookmarks`要素で`doc2`を値として指定しています。 この値は、Assemblerサービスに渡される入力マップに`doc2`という名前のキーが含まれていることを示します。 `doc2`キーの値は、ブックマークXMLドキュメントを表す`com.adobe.idp.Document`値です。 （『[AssemblerサービスとDDXリファレンス](https://www.adobe.com/go/learn_aemforms_ddx_63)』の「ブックマーク言語」を参照）。

このトピックでは、次のXMLしおり言語を使用して、しおりを含むPDFドキュメントを構成します。

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

このブックマークXMLドキュメント内に、ユーザーがブックマークをクリックしたときに実行されるアクションを定義するAction要素があることに注意してください。 Action要素の下には、NotePadなどのアプリケーションを起動し、PDFファイルなどのファイルを開くLaunch要素があります。 PDFファイルを開くには、開くファイルを指定するFile要素を使用する必要があります。 例えば、この節で指定するブックマークXMLファイルでは、開くファイルの名前はLoanDetails.pdfです。

>[!NOTE]
>
>サポートされるアクションについて詳しくは、『[AssemblerサービスとDDXリファレンス](https://www.adobe.com/go/learn_aemforms_ddx_63)』の「`Action`要素」を参照してください。

この節で指定したDDXドキュメントと、XMLファイルを入力としてブックマークすると、Assemblerサービスは、次のブックマークを含むPDFドキュメントをアセンブリします。

![aw_aw_bmark](assets/aw_aw_bmark.png)

ユーザーが&#x200B;*Open the Loan Details*&#x200B;ブックマークをクリックすると、LoanDetails.pdfが開きます。 同様に、ユーザーが&#x200B;*NotePad*&#x200B;のブックマークをクリックすると、NotePadが起動します。

>[!NOTE]
>
>この節を読む前に、Assemblerサービスを使用したPDFドキュメントのアセンブリについて理解しておくことをお勧めします。 この節では、入力ドキュメントを含むコレクションオブジェクトの作成や、返されたコレクションオブジェクトから結果を抽出する方法の学習など、概念については説明しません。 （[PDFドキュメントのプログラムによるアセンブリ](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)を参照）。

>[!NOTE]
>
>Assemblerサービスについて詳しくは、『AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)向けサービスリファレンス』を参照してください。[

>[!NOTE]
>
>DDXドキュメントについて詳しくは、『[AssemblerサービスとDDXリファレンス](https://www.adobe.com/go/learn_aemforms_ddx_63)』を参照してください。

## 手順の概要{#summary-of-steps}

しおりを含むPDFドキュメントをアセンブリするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. PDFアセンブラークライアントを作成します。
1. 既存のDDXドキュメントの参照
1. しおりを追加するPDFドキュメントを参照します。
1. ブックマークXMLドキュメントを参照します。
1. PDFドキュメントとブックマークXMLドキュメントをMapコレクションに追加します。
1. 実行時オプションを設定します。
1. PDFドキュメントをアセンブリします。
1. しおりを含むPDFドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用する場合は、プロキシファイルを必ず含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(AEM FormsをJBossにデプロイする場合に必要)
* jbossall-client.jar(AEM FormsをJBossにデプロイする場合に必要)

AEM FormsがJBoss以外のサポート対象のJ2EEアプリケーションサーバーにデプロイされている場合は、adobe-utilities.jarファイルとjbossall-client.jarファイルを、AEM FormsがデプロイされているJ2EEアプリケーションサーバーに固有のJARファイルに置き換える必要があります。 すべてのAEM Forms JARファイルの場所について詳しくは、「[AEM Forms Javaライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)」を参照してください。

**PDFアセンブラークライアントの作成**

プログラムでAssembler操作を実行する前に、Assemblerサービスクライアントを作成する必要があります。

**既存のDDXドキュメントの参照**

PDFドキュメントをアセンブリするには、DDXドキュメントを参照する必要があります。 このDDXドキュメントには`Bookmarks`要素が必要です。この要素は、ブックマークを含むPDFをアセンブルするようにAssemblerサービスに指示します。 （この節で前述したDDXドキュメントの例を参照）。

**しおりを追加するPDFドキュメントの参照**

しおりを追加するPDFドキュメントを参照します。 参照先のPDFドキュメントに既にしおりが含まれているかどうかは関係ありません。 `Bookmarks`要素がPDFソース要素の子の場合、PDFソースに既に存在するしおりがしおりに置き換えられます。 ただし、既存のしおりを保持する場合は、 `Bookmarks`がPDFソース要素の兄弟であることを確認してください。 例えば、次の例を考えてみましょう。

```xml
 <PDF result="foo">
      <PDF source="inDoc"/>
      <Bookmarks source="doc2"/>
 </PDF>
```

**ブックマークXMLドキュメントの参照**

新しいしおりを含むPDFをアセンブリするには、しおりXMLドキュメントを参照する必要があります。 ブックマークXMLドキュメントは、Mapコレクションオブジェクト内のAssemblerサービスに渡されます。 （例については、この節で前述したブックマークXMLドキュメントを参照してください）。

>[!NOTE]
>
>『[AssemblerサービスとDDXリファレンス](https://www.adobe.com/go/learn_aemforms_ddx_63)』の「ブックマーク言語」を参照してください。

**PDFドキュメントとブックマークXMLドキュメントをMapコレクションに追加します**

ブックマークを追加するPDFドキュメントとブックマークXMLドキュメントの両方をMapコレクションに追加する必要があります。 したがって、 Mapコレクションオブジェクトには次の2つの要素が含まれます。PDFドキュメントとブックマークXMLドキュメント。

**実行時オプションの設定**

ジョブの実行中にAssemblerサービスの動作を制御する実行時オプションを設定できます。 例えば、エラーが発生した場合にジョブの処理を続行するようAssemblerサービスに指示するオプションを設定できます。 設定できる実行時オプションについて詳しくは、『[AEM Forms APIリファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)』の`AssemblerOptionSpec`クラス参照を参照してください。

**PDFドキュメントのアセンブリ**

新しいブックマークを含むPDFドキュメントをアセンブリするには、Assemblerサービスの`invokeDDX`操作を使用します。 `invokeOneDocument`などの他のAssemblerサービス操作とは異なり、`invokeDDX`操作を使用する必要があるのは、Assemblerサービスには、Mapコレクションオブジェクト内で渡されるブックマークXMLドキュメントが必要だからです。 このオブジェクトは、`invokeDDX`操作のパラメーターです。

**しおりを含むPDFドキュメントを保存します**

返されたマップオブジェクトから結果を抽出し、対応するPDFドキュメントを保存する必要があります。 （[PDFドキュメントのプログラムによるアセンブリ](/help/forms/developing/programmatically-assembling-pdf-documents.md)の「結果の抽出」を参照）。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDFドキュメントのプログラムによるアセンブリ](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java API {#assemble-pdf-documents-with-bookmarks-using-the-java-api}を使用して、しおりを使用してPDFドキュメントをアセンブリします。

AssemblerサービスAPI(Java)を使用して、ブックマークを含むPDFドキュメントをアセンブリします。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-assembler-client.jarなどのクライアントJARファイルを含めます。

1. PDFアセンブラークライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。（[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照。）
   * コンストラクターを使用して`AssemblerServiceClient`オブジェクトを渡し、`ServiceClientFactory`オブジェクトを作成します。

1. 既存のDDXドキュメントの参照

   * コンストラクターを使用し、DDXファイルの場所を指定する文字列値を渡して、DDXドキュメントを表す`java.io.FileInputStream`オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. しおりを追加するPDFドキュメントを参照します。

   * コンストラクターを使用してPDFドキュメントの場所を渡し、`java.io.FileInputStream`オブジェクトを作成します。
   * コンストラクターを使用して`com.adobe.idp.Document`オブジェクトを作成し、PDFドキュメントを含む`java.io.FileInputStream`オブジェクトを渡します。

1. ブックマークXMLドキュメントを参照します。

   * コンストラクターを使用して、ブックマークXMLドキュメントを表すXMLファイルの場所を渡し、`java.io.FileInputStream`オブジェクトを作成します。
   * `com.adobe.idp.Document`オブジェクトを作成し、PDFドキュメントを含む`java.io.FileInputStream`オブジェクトを渡します。

1. PDFドキュメントとブックマークXMLドキュメントをMapコレクションに追加します。

   * 入力PDFドキュメントとブックマークXMLドキュメントの両方を保存するための`java.util.Map`オブジェクトを作成します。
   * `java.util.Map`オブジェクトの`put`メソッドを呼び出し、次の引数を渡して、入力PDFドキュメントを追加します。

      * キー名を表すstring値です。 この値は、DDXドキュメントで指定されたPDFソース要素の値と一致する必要があります。
      * 入力PDFドキュメントを含む`com.adobe.idp.Document`オブジェクト。
   * `java.util.Map`オブジェクトの`put`メソッドを呼び出し、次の引数を渡して、ブックマークXMLドキュメントを追加します。

      * キー名を表すstring値です。 この値は、DDXドキュメントで指定されているBookmarks source要素の値と一致する必要があります。
      * ブックマークXMLドキュメントを含む`com.adobe.idp.Document`オブジェクト。


1. 実行時オプションを設定します。

   * コンストラクターを使用して、実行時オプションを格納する`AssemblerOptionSpec`オブジェクトを作成します。
   * `AssemblerOptionSpec`オブジェクトに属するメソッドを呼び出して、ビジネス要件に合った実行時オプションを設定します。 例えば、エラーが発生したときにジョブの処理を続行するようにAssemblerサービスに指示するには、`AssemblerOptionSpec`オブジェクトの`setFailOnError`メソッドを呼び出し、`false`を渡します。

1. PDFドキュメントをアセンブリします。

   `AssemblerServiceClient`オブジェクトの`invokeDDX`メソッドを呼び出し、次の必須値を渡します。

   * 使用するDDXドキュメントを表す`com.adobe.idp.Document`オブジェクト
   * 入力PDFドキュメントとブックマークXMLドキュメントの両方を含む`java.util.Map`オブジェクト。
   * デフォルトのフォントやジョブのログレベルを含む、実行時のオプションを指定する`com.adobe.livecycle.assembler.client.AssemblerOptionSpec`オブジェクト

   `invokeDDX`メソッドは、ジョブの結果と発生した例外を含む`com.adobe.livecycle.assembler.client.AssemblerResult`オブジェクトを返します。

1. しおりを含むPDFドキュメントを保存します。

   新しく作成したPDFドキュメントを取得するには、次の操作を実行します。

   * `AssemblerResult`オブジェクトの`getDocuments`メソッドを呼び出します。 `java.util.Map`オブジェクトを返します。
   * `java.util.Map`オブジェクトを繰り返し処理して、結果の`com.adobe.idp.Document`オブジェクトを見つけます。 （DDXドキュメントで指定されたPDF結果要素を使用して、ドキュメントを取得できます）。
   * `com.adobe.idp.Document`オブジェクトの`copyToFile`メソッドを呼び出して、PDFドキュメントを抽出します。

**関連トピック**

[クイックスタート（SOAPモード）:Java APIを使用したしおりを使用したPDFドキュメントのアセンブリ](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-documents-with-bookmarks-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## WebサービスAPI {#assemble-pdf-documents-with-bookmarks-using-the-web-service-api}を使用して、PDFドキュメントをブックマークと組み合わせます。

AssemblerサービスAPI（Webサービス）を使用して、ブックマークを含むPDFドキュメントをアセンブリします。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. PDFアセンブラークライアントを作成します。

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

1. しおりを追加するPDFドキュメントを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、入力PDFを保存するために使用されます。
   * コンストラクターを呼び出し、入力PDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得することで、バイト配列のサイズを判断できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことによって、バイト配列にストリームデータを入力します。
   * `BLOB`オブジェクトの`MTOM`フィールドにバイト配列の内容を割り当てて、オブジェクトを設定します。

1. ブックマークXMLドキュメントを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、ブックマークXMLドキュメントの保存に使用されます。
   * コンストラクターを呼び出し、入力PDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得することで、バイト配列のサイズを判断できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことによって、バイト配列にストリームデータを入力します。
   * `BLOB`オブジェクトの`MTOM`フィールドにバイト配列の内容を割り当てて、オブジェクトを設定します。

1. PDFドキュメントとブックマークXMLドキュメントをMapコレクションに追加します。

   * `MyMapOf_xsd_string_To_xsd_anyType`オブジェクトを作成します。 このコレクションオブジェクトは、入力PDFドキュメントとブックマークXMLドキュメントを保存するために使用します。
   * 入力PDFドキュメントとブックマークXMLドキュメントごとに、 `MyMapOf_xsd_string_To_xsd_anyType_Item`オブジェクトを作成します。
   * `MyMapOf_xsd_string_To_xsd_anyType_Item`オブジェクトの`key`フィールドに、キー名を表すstring値を割り当てます。 この値は、DDXドキュメントで指定されたPDFソース要素の値と一致する必要があります。
   * PDFドキュメントを格納する`BLOB`オブジェクトを`MyMapOf_xsd_string_To_xsd_anyType_Item`オブジェクトの`value`フィールドに割り当てます。
   * `MyMapOf_xsd_string_To_xsd_anyType_Item`オブジェクトを`MyMapOf_xsd_string_To_xsd_anyType`オブジェクトに追加します。 `MyMapOf_xsd_string_To_xsd_anyType`オブジェクトの`Add`メソッドを呼び出して、`MyMapOf_xsd_string_To_xsd_anyType`オブジェクトを渡します。 （このタスクは、入力PDFドキュメントとブックマークXMLドキュメントごとに実行します）。

1. 実行時オプションを設定します。

   * コンストラクターを使用して、実行時オプションを格納する`AssemblerOptionSpec`オブジェクトを作成します。
   * `AssemblerOptionSpec`オブジェクトに属するデータメンバーに値を割り当てて、ビジネス要件に合った実行時オプションを設定します。 例えば、エラーが発生したときにジョブの処理を続行するようにAssemblerサービスに指示するには、`false`を`AssemblerOptionSpec`オブジェクトの`failOnError`データメンバーに割り当てます。

1. PDFドキュメントをアセンブリします。

   `AssemblerServiceClient`オブジェクトの`invokeDDX`メソッドを呼び出し、次の値を渡します。

   * DDXドキュメントを表す`BLOB`オブジェクト
   * 入力ドキュメントを含む`MyMapOf_xsd_string_To_xsd_anyType`配列
   * 実行時オプションを指定する`AssemblerOptionSpec`オブジェクト

   `invokeDDX`メソッドは、ジョブの結果と発生した可能性のある例外を含む`AssemblerResult`オブジェクトを返します。

1. しおりを含むPDFドキュメントを保存します。

   新しく作成したPDFドキュメントを取得するには、次の操作を実行します。

   * `AssemblerResult`オブジェクトの`documents`フィールド（結果のPDFドキュメントを含む`Map`オブジェクト）にアクセスします。
   * 結果のドキュメントの名前と一致するキーが見つかるまで、`Map`オブジェクトを繰り返し処理します。 次に、配列メンバの`value`を`BLOB`にキャストします。
   * `BLOB`オブジェクトの`MTOM`フィールドにアクセスして、PDFドキュメントを表すバイナリデータを抽出します。 PDFファイルに書き出すことができるバイトの配列を返します。

**関連トピック**

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
