---
title: しおりを使用したPDFドキュメントのアセンブリ
seo-title: しおりを使用したPDFドキュメントのアセンブリ
description: 'null'
seo-description: 'null'
uuid: a306d2a6-0b12-4eb3-bff4-968a33417486
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9f4711a8-033c-4051-ab41-65a26838899b
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '2526'
ht-degree: 3%

---


# しおりを使用したPDFドキュメントのアセンブリ {#assembling-pdf-documents-with-bookmarks}

ブックマークを含むPDFドキュメントをアセンブリできます。 例えば、しおりが含まれていないPDFドキュメントがあり、しおりを指定して変更するとします。 Assemblerサービスを使用すると、ブックマークを含まないPDFドキュメントを渡して、ブックマークを含むPDFドキュメントに戻すことができます。

ブックマークには、次のプロパティが含まれます。

* 画面にテキストとして表示されるタイトル。
* ユーザーがブックマークをクリックした場合の動作を指定するアクション。 ブックマークの一般的な操作は、現在のドキュメント内の別の場所に移動するか、別のPDFドキュメントを開くことです。ただし、他の操作を指定することもできます。

この説明の目的で、次のDDXドキュメントが使用されているとします。

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

このDDXドキュメント内で、source属性に値が割り当てられてい `Loan.pdf`ます。 このDDXドキュメントは、1つのPDFドキュメントをAssemblerサービスに渡すことを指定します。 ブックマークを使用してPDFドキュメントをアセンブリする場合は、結果ドキュメントーでブックマークを説明するブックマークXMLドキュメントを指定する必要があります。 ブックマークXMLドキュメントを指定するには、 `Bookmarks` 要素がDDXドキュメントで指定されていることを確認します。

この例のDDXドキュメントでは、 `Bookmarks` 要素は値 `doc2` として指定されています。 この値は、Assemblerサービスに渡される入力マップに、という名前のキーが含まれていることを示し `doc2`ます。 キーの値は、ブックマークXML `doc2` ドキュメントを表す `com.adobe.idp.Document` 値です。 (『 [AssemblerサービスとDDXリファレンス』の「Bookmarks Language」を参照](https://www.adobe.com/go/learn_aemforms_ddx_63))。

このトピックでは、次のXMLブックマーク言語を使用して、ブックマークを含むPDFドキュメントをアセンブリします。

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

このブックマークXMLドキュメント内に、ユーザーがブックマークをクリックしたときに実行されるアクションを定義するAction要素があることに注意してください。 アクション要素の下に、NotePadなどのアプリケーションを起動し、PDFファイルなどのファイルを開くLaunch要素があります。 PDFファイルを開くには、開くファイルを指定するFile要素を使用する必要があります。 例えば、この節で指定するブックマークXMLファイルでは、開かれるファイルの名前はLoanDetails.pdfです。

>[!NOTE]
>
>サポートされているアクションについて詳しくは、『 `Action` Assembler Service and DDX Reference [](https://www.adobe.com/go/learn_aemforms_ddx_63)』の「element」を参照してください。

この節で指定するDDXドキュメントとブックマークXMLファイルを入力として指定した場合、Assemblerサービスは、次のブックマークを含むPDFドキュメントをアセンブリします。

![aw_aw_bmark](assets/aw_aw_bmark.png)

ユーザーがLoan Details *.pdfブックマークを* 開くと、LoanDetails.pdfが開きます。 同様に、ユーザーがNotePadの *起動ブックマークをクリックすると* 、NotePadが起動します。

>[!NOTE]
>
>この節を読む前に、Assemblerサービスを使用したPDFドキュメントのアセンブリについて理解しておくことをお勧めします。 ここでは、入力ドキュメントを含むコレクションオブジェクトの作成や、返されるコレクションオブジェクトから結果を抽出する方法の学習など、概念については説明しません。 (「 [プログラムによるPDFドキュメントのアセンブリ](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)」を参照)。

>[!NOTE]
>
>For more information about the Assembler service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>DDXドキュメントについて詳しくは、『 [Assembler Service and DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63)』を参照してください。

## 手順の概要 {#summary-of-steps}

ブックマークを含むPDFドキュメントをアセンブリするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. PDFアセンブラクライアントを作成します。
1. 既存のDDXドキュメントの参照。
1. ブックマークを追加するPDFドキュメントを参照します。
1. ブックマークXMLドキュメントを参照します。
1. 追加PDFドキュメントとブックマークXMLドキュメントをMapコレクションに追加します。
1. 実行時オプションを設定します。
1. PDFドキュメントをアセンブリします。
1. しおりが含まれているPDFドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(AEM FormsがJBossにデプロイされている場合に必要)
* jbossall-client.jar(AEM FormsがJBossにデプロイされている場合に必要)

AEM FormsがJBoss以外のサポート対象のJ2EEアプリケーションサーバーにデプロイされている場合は、adobe-utilities.jarファイルとjbossall-client.jarファイルを、AEM FormsがデプロイされているJ2EEアプリケーションサーバーに固有のJARファイルに置き換える必要があります。 For information about the location of all AEM Forms JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**PDFアセンブラクライアントの作成**

プログラムによってAssembler操作を実行する前に、Assemblerサービスクライアントを作成する必要があります。

**既存のDDXドキュメントの参照**

PDFドキュメントをアセンブリするには、DDXドキュメントを参照する必要があります。 このDDXドキュメントには `Bookmarks` 要素が含まれている必要があります。この要素は、ブックマークを含むPDFをアセンブリするようAssemblerサービスに指示します。 (例については、この節で前述したDDXドキュメントを参照してください)。

**ブックマークが追加されたPDFドキュメントの参照**

ブックマークを追加するPDFドキュメントを参照します。 参照先のPDFドキュメントに既にしおりが含まれているかどうかは関係ありません。 要素がPDFソース要素の子である場合、PDFソースに既に存在する `Bookmarks` しおりは、しおりに置き換えられます。 ただし、既存のしおりを保持する場合は、がPDFソース要素の兄弟であ `Bookmarks` ることを確認してください。 例えば、次の例を考えてみましょう。

```xml
 <PDF result="foo">
      <PDF source="inDoc"/>
      <Bookmarks source="doc2"/>
 </PDF>
```

**ブックマークXMLドキュメントの参照**

新しいブックマークを含むPDFをアセンブリするには、ブックマークXMLドキュメントを参照する必要があります。 ブックマークXMLドキュメントは、Mapコレクションオブジェクト内のAssemblerサービスに渡されます。 (例については、この節で前述したブックマークXMLドキュメントを参照してください)。

>[!NOTE]
>
>『 [AssemblerサービスとDDXリファレンス』の「ブックマークの言語」を参照してください](https://www.adobe.com/go/learn_aemforms_ddx_63)。

**追加PDFドキュメントとブックマークXMLドキュメントをMapコレクションにマックする**

ブックマークを追加するPDFドキュメントとブックマークXMLドキュメントの両方をMapコレクションに追加する必要があります。 したがって、Mapコレクションオブジェクトには2つの要素が含まれます。 PDFドキュメントとブックマークXMLドキュメント

**実行時オプションの設定**

ジョブの実行中にAssemblerサービスの動作を制御する実行時オプションを設定できます。 例えば、エラーが発生した場合にジョブの処理を続行するようAssemblerサービスに指示するオプションを設定できます。 設定できる実行時オプションについて詳しくは、『 `AssemblerOptionSpec` AEM FormsAPIリファレンス』の [クラス参照を参照してください](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

**PDFドキュメントのアセンブリ**

新しいブックマークを含むPDFドキュメントをアセンブリするには、Assemblerサービスの `invokeDDX` 操作を使用します。 この `invokeDDX``invokeOneDocument` 操作を他のAssemblerサービスの操作（など）とは異なり、使用する必要があるのは、AssemblerサービスがMapコレクションオブジェクト内で渡されるブックマークXMLドキュメントを必要とするからです。 このオブジェクトは、 `invokeDDX` 操作のパラメーターです。

**しおりが含まれているPDFドキュメントの保存**

返されたマップオブジェクトから結果を抽出し、対応するPDFドキュメントを保存する必要があります。 (「PDFドキュメントの [プログラムによるアセンブリ」の「結果の抽出」を参照](/help/forms/developing/programmatically-assembling-pdf-documents.md))。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[プログラムによるPDFドキュメントのアセンブリ](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java APIを使用したブックマークによるPDFドキュメントのアセンブリ {#assemble-pdf-documents-with-bookmarks-using-the-java-api}

Assembler Service API(Java)を使用して、ブックマークを使用してPDFドキュメントをアセンブリします。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-assembler-client.jarなどのクライアントJARファイルを含めます。

1. PDFアセンブラクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。（[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照。）
   * Create an `AssemblerServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. 既存のDDXドキュメントの参照。

   * コンストラクターを使用し、DDXファイルの場所を指定する文字列値を渡して、DDXドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. ブックマークを追加するPDFドキュメントを参照します。

   * コンストラクターを使用し、PDFドキュメントの場所を渡して、 `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクターを使用して `com.adobe.idp.Document` オブジェクトを作成し、PDFドキュメントを含む `java.io.FileInputStream` オブジェクトを渡します。

1. ブックマークXMLドキュメントを参照します。

   * コンストラクターを使用し、ブックマークXMLドキュメントーを表すXMLファイルの場所を渡して、 `java.io.FileInputStream` オブジェクトを作成します。
   * オブジェクトを作成し、PDF `com.adobe.idp.Document` ドキュメントを含む `java.io.FileInputStream` オブジェクトを渡します。

1. 追加PDFドキュメントとブックマークXMLドキュメントをMapコレクションに追加します。

   * 入力PDFドキュメントとブックマークXMLドキュメントの両方を保存するために使用する `java.util.Map` オブジェクトを作成します。
   * オ追加ブジェクトのメソッドを呼び出し、次の引数を渡すことにより、入力PDFドキュメントを作成します。 `java.util.Map``put`

      * キー名を表すstring値です。 この値は、DDXドキュメントで指定されたPDFソース要素の値と一致する必要があります。
      * 入力PDFドキュメントを含む `com.adobe.idp.Document` オブジェクトです。
   * 追加ブックマークXMLドキュメントを設定するには、 `java.util.Map` オブジェクトの `put` メソッドを呼び出し、次の引数を渡します。

      * キー名を表すstring値です。 この値は、DDXドキュメントで指定されたBookmarksソース要素の値と一致する必要があります。
      * ブックマークXMLドキュメントを含む `com.adobe.idp.Document` オブジェクトです。


1. 実行時オプションを設定します。

   * コンストラクターを使用して、実行時のオプションを格納する `AssemblerOptionSpec` オブジェクトを作成します。
   * オブジェクトに属するメソッドを呼び出して、ビジネス要件に合うように実行時オプションを設定し `AssemblerOptionSpec` ます。 例えば、エラーが発生した場合にジョブの処理を続行するようにAssemblerサービスに指示するには、 `AssemblerOptionSpec` オブジェクトの `setFailOnError` メソッドを呼び出して渡し `false`ます。

1. PDFドキュメントをアセンブリします。

   オブジェクトの `AssemblerServiceClient``invokeDDX` メソッドを呼び出し、次の必須値を渡します。

   * 使用されるDDXドキュメントを表す `com.adobe.idp.Document` オブジェクトです
   * 入力PDFドキュメントとブックマークXMLドキュメントの両方を含む `java.util.Map` オブジェクトです。
   * デフォルトのフォントとジョブログレベルなど、実行時のオプションを指定する `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` オブジェクトです

   この `invokeDDX` メソッドは、ジョブの結果と発生した例外を含む `com.adobe.livecycle.assembler.client.AssemblerResult` オブジェクトを返します。

1. しおりが含まれているPDFドキュメントを保存します。

   新しく作成されたPDFドキュメントを取得するには、次の操作を実行します。

   * オブジェクトの `AssemblerResult` メソッドを呼び出し `getDocuments` ます。 これは、 `java.util.Map` オブジェクトを返します。
   * オブジェクトを繰り返し処理して、結果のオブジ `java.util.Map``com.adobe.idp.Document` ェクトを見つけます。 (DDXドキュメントで指定されたPDF結果ドキュメントを使用して、要素を取得できます)。
   * オブジェクトの `com.adobe.idp.Document``copyToFile` メソッドを呼び出してPDFドキュメントを抽出します。

**関連トピック**

[クイック開始（SOAPモード）: Java APIを使用したブックマークによるPDFドキュメントのアセンブリ](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-documents-with-bookmarks-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## WebサービスAPIを使用したブックマークによるPDFドキュメントのアセンブリ {#assemble-pdf-documents-with-bookmarks-using-the-web-service-api}

Assembler Service API（Webサービス）を使用して、ブックマークを使用してPDFドキュメントをアセンブリします。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >サーバーホスト `localhost` AEM FormsのIPアドレスに置き換えます。

1. PDFアセンブラクライアントを作成します。

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

1. ブックマークを追加するPDFドキュメントを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、入力PDFを保存するために使用されます。
   * コンストラクターを呼び出し、入力PDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
   * オブジェクトの `System.IO.FileStream``Read` メソッドを呼び出し、読み取るバイト配列、開始位置およびストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * オブジェクトにバイト配列の内容を割り当てて、 `BLOB` オブジェクト `MTOM` を入力します。

1. ブックマークXMLドキュメントを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、ブックマークXMLドキュメントの格納に使用されます。
   * コンストラクターを呼び出し、入力PDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
   * オブジェクトの `System.IO.FileStream``Read` メソッドを呼び出し、読み取るバイト配列、開始位置およびストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * オブジェクトにバイト配列の内容を割り当てて、 `BLOB` オブジェクト `MTOM` を入力します。

1. 追加PDFドキュメントとブックマークXMLドキュメントをMapコレクションに追加します。

   * Create a `MyMapOf_xsd_string_To_xsd_anyType` object. このコレクションオブジェクトは、入力PDFドキュメントとブックマークXMLドキュメントの格納に使用されます。
   * 入力PDFドキュメントおよびブックマークXMLドキュメントごとに、 `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトを作成します。
   * キー名を表すstring値を `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトの `key` フィールドに割り当てます。 この値は、DDXドキュメントで指定されたPDFソース要素の値と一致する必要があります。
   * PDFドキュメントを保存している `BLOB` オブジェクトをオブジェクトのフィ `MyMapOf_xsd_string_To_xsd_anyType_Item` ー `value` ルドに割り当てます。
   * オ追加ブジェクトをオブジ `MyMapOf_xsd_string_To_xsd_anyType_Item``MyMapOf_xsd_string_To_xsd_anyType` ェクトに追加します。 Invoke the `MyMapOf_xsd_string_To_xsd_anyType` object&#39;s `Add` method and pass the `MyMapOf_xsd_string_To_xsd_anyType` object. (このタスクは、入力PDFドキュメントおよびブックマークXMLドキュメントごとに実行します)。

1. 実行時オプションを設定します。

   * コンストラクターを使用して、実行時のオプションを格納する `AssemblerOptionSpec` オブジェクトを作成します。
   * オブジェクトに属するデータメンバに値を割り当てることで、ビジネス要件に合った実行時オプションを設定し `AssemblerOptionSpec` ます。 例えば、エラーが発生した場合にジョブの処理を続行するようにAssemblerサービスに指示するには、 `false` オブジェクトの `AssemblerOptionSpec``failOnError` データメンバーに割り当てます。

1. PDFドキュメントをアセンブリします。

   オブジェクトの `AssemblerServiceClient``invokeDDX` メソッドを呼び出し、次の値を渡します。

   * DDXドキュメントを表す `BLOB` オブジェクトです
   * 入力ドキュメントーを含む `MyMapOf_xsd_string_To_xsd_anyType` 配列
   * 実行時オプションを指定する `AssemblerOptionSpec` オブジェクトです。

   この `invokeDDX` メソッドは、ジョブの結果と発生した可能性のある例外を含む `AssemblerResult` オブジェクトを返します。

1. しおりが含まれているPDFドキュメントを保存します。

   新しく作成されたPDFドキュメントを取得するには、次の操作を実行します。

   * オブジェクトのフ `AssemblerResult` ィールドにアクセスします。この `documents` フィールドは、結果のPDFドキュメントを含む `Map` オブジェクトです。
   * 結果のドキュメントの名前と一致するキーが見つかるまで、 `Map` オブジェクトを繰り返し処理します。 次に、その配列メンバーのをにキャスト `value` し `BLOB`ます。
   * PDFドキュメントを表すバイナリデータを抽出するには、その `BLOB` オブジェクトの `MTOM` フィールドにアクセスします。 PDFファイルに書き出すことができるバイトの配列を返します。

**関連トピック**

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
