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
source-git-commit: e3f700b52446505224fa4b4688d439750a66f471

---


# しおりを使用したPDFドキュメントのアセンブリ {#assembling-pdf-documents-with-bookmarks}

しおりを含むPDFドキュメントをアセンブリできます。 例えば、しおりを含まないPDFドキュメントがあり、しおりを指定して変更するとします。 Assemblerサービスを使用すると、ブックマークを含まないPDFドキュメントを渡し、ブックマークを含むPDFドキュメントを取得できます。

ブックマークには、次のプロパティが含まれます。

* 画面にテキストとして表示されるタイトル。
* ユーザーがブックマークをクリックしたときの動作を指定するアクション。 ブックマークの一般的な操作は、現在のドキュメント内の別の場所に移動するか、別のPDFドキュメントを開くことです。ただし、他の操作を指定することもできます。

この説明の目的で、次のDDXドキュメントを使用します。

```as3
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
       <PDF result="FinalDoc.pdf">
          <PDF source="Loan.pdf">
             <Bookmarks source="doc2" />
          </PDF>
       </PDF>
 </DDX>
```

このDDXドキュメント内で、source属性に値が割り当てられています `Loan.pdf`。 このDDXドキュメントは、単一のPDFドキュメントがAssemblerサービスに渡されることを指定します。 PDFドキュメントをしおりと組み合わせる場合は、結果のドキュメントでしおりを説明するしおりXMLドキュメントを指定する必要があります。 ブックマークXMLドキュメントを指定するには、DDXエレメントで `Bookmarks` 要素が指定されていることを確認します。ドキュメント

この例のDDXドキュメントでは、 `Bookmarks` 要素が値と `doc2` して指定されます。 この値は、Assemblerサービスに渡される入力マップに、という名前のキーが含まれていることを示しま `doc2`す。 キーの値は、ブッ `doc2` クマークXML `com.adobe.idp.Document` ドキュメントを表す値です。 (『 [Assembler Service and DDX Reference』の「Bookmarks Language」を参照](https://www.adobe.com/go/learn_aemforms_ddx_63))。

このトピックでは、次のXMLしおり言語を使用して、しおりを含むPDFドキュメントをアセンブリします。

```as3
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

このブックマークXMLドキュメント内に、ユーザーがブックマークをクリックしたときに実行されるアクションを定義するAction要素があります。 アクション要素の下には、NotePadなどのアプリケーションを起動し、PDFファイルなどのファイルを開くLaunch要素があります。 PDFファイルを開くには、開くファイルを指定するFile要素を使用する必要があります。 例えば、この節で指定するブックマークXMLファイルでは、開くファイルの名前はLoanDetails.pdfです。

>[!NOTE]
>
>サポートされるアクションの詳細については、『Assembler Service and DDX Reference `Action` 』の「element」 [を参照してください](https://www.adobe.com/go/learn_aemforms_ddx_63)。

この節で指定したDDXドキュメントと、ブックマークXMLファイルを入力として指定した場合、Assemblerサービスは、次のブックマークを含むPDFドキュメントをアセンブルします。

![aw_aw_bmark](assets/aw_aw_bmark.png)

ユーザーが「Open the Loan Details ** 」ブックマークをクリックすると、LoanDetails.pdfが開きます。 同様に、ユーザーがNotePadのブックマークを起動す *ると* 、NotePadが起動します。

>[!NOTE]
>
>この節を読む前に、Assemblerサービスを使用したPDFドキュメントのアセンブリに関する知識が必要です。 ここでは、入力ドキュメントを含むコレクションオブジェクトの作成や、返されるコレクションオブジェクトから結果を抽出する方法の学習など、概念については説明しません。 (「プログラムに [よるPDFドキュメントの組み立て](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)」を参照)。

>[!NOTE]
>
>For more information about the Assembler service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>DDXドキュメントについて詳しくは、 [Assembler Service and DDX Referenceを参照してください](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 手順の概要 {#summary-of-steps}

しおりを含むPDFドキュメントをアセンブリするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. PDFアセンブラクライアントを作成します。
1. 既存のDDXドキュメントの参照
1. しおりを追加するPDFドキュメントを参照します。
1. ブックマークXMLドキュメントの参照。
1. PDFドキュメント追加とブックマークXMLドキュメントのMapコレクション。
1. 実行時オプションを設定します。
1. 「Assemble the PDF」ドキュメント。
1. しおりを含むPDFドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar（AEM FormsがJBossにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsがJBossにデプロイされている場合に必要）

aem FormsがJBoss以外のサポート対象のJ2EEアプリケーションサーバーにデプロイされている場合は、adobe-utilities.jarファイルとjbossall-client.jarファイルを、AEM Formsのデプロイ先のJ2EEアプリケーションサーバーに固有のJARファイルに置き換える必要があります。 For information about the location of all AEM Forms JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**PDFアセンブラクライアントの作成**

プログラムによってAssembler操作を実行する前に、Assemblerサービスクライアントを作成する必要があります。

**既存のDDXの参照ドキュメント**

PDFドキュメントをアセンブリするには、DDXアセンブリを参照する必要があります。ドキュメント このDDXドキュメントには要素が含まれている必要があ `Bookmarks` ります。この要素は、ブックマークを含むPDFをアセンブリするようAssemblerサービスに指示します。 (例については、この節で前述したDDXドキュメントを参照してください)。

**しおりが追加されるPDFドキュメントの参照**

しおりを追加するPDFドキュメントを参照します。 参照先のPDFドキュメントに既にしおりが含まれているかどうかは関係ありません。 要素がPDF `Bookmarks` ソース要素の子である場合、PDFソースに既に存在するしおりがしおりに置き換えられます。 ただし、既存のしおりを保持する場合は、がPDFソース要素の兄弟であ `Bookmarks` ることを確認してください。 例えば、次の例を考えてみましょう。

```as3
 <PDF result="foo">
      <PDF source="inDoc"/>
      <Bookmarks source="doc2"/>
 </PDF>
```

**ブックマークXMLドキュメント**

新しいしおりを含むPDFをアセンブリするには、しおりXMLドキュメントを参照します。 ブックマークXMLドキュメントは、Mapコレクションオブジェクト内のAssemblerサービスに渡されます。 (例については、この節で前述したブックマークXMLドキュメントを参照してください)。

>[!NOTE]
>
>『 [Assembler Service and DDX Reference』の「Bookmarks Language」を参照してください](https://www.adobe.com/go/learn_aemforms_ddx_63)。

**PDFドキュメント追加とMapコレクションへのブックマークXMLドキュメント**

ブックマークを追加するPDFドキュメントとブックマークXMLドキュメントの両方をMapコレクションに追加する必要があります。 したがって、 Mapコレクションオブジェクトには次の2つの要素が含まれます。pdfドキュメントとブックマークXMLドキュメント。

**実行時オプションの設定**

ジョブの実行中にAssemblerサービスの動作を制御する実行時オプションを設定できます。 例えば、エラーが発生した場合にジョブの処理を続行するようにAssemblerサービスに指示するオプションを設定できます。 設定できる実行時オプションについて詳しくは、『 `AssemblerOptionSpec` AEM Forms APIリファレンス』のクラス [参照を参照し](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)てください。

**「Assemble the PDF」ドキュメント**

新しいブックマークを含むPDFドキュメントをアセンブリするには、Assemblerサービスの操作を使用 `invokeDDX` します。 この操作を他のAssemblerサービスの操作（など）とは異なり、使用する必要があるのは、AssemblerサービスがMapコレクションオブジェクト内で渡されるブックマークXMLドキュメントを必要とする `invokeDDX``invokeOneDocument` ためです。 このオブジェクトは、操作のパラメー `invokeDDX` ターです。

**しおりを含むPDFドキュメントの保存**

返されたマップオブジェクトから結果を抽出し、対応するPDFオブジェクトを保存する必要があります。ドキュメント (「プログラムによるPDFドキュメントのアセンブリ」の「 [結果の抽出](/help/forms/developing/programmatically-assembling-pdf-documents.md)」を参照)。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[プログラムによるPDFドキュメント](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java APIを使用したPDFドキュメントのしおりによるアセンブリ {#assemble-pdf-documents-with-bookmarks-using-the-java-api}

Assembler Service API(Java)を使用して、PDFドキュメントをブックマークと共にアセンブリします。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-assembler-client.jarなどのクライアントJARファイルを含めます。

1. PDFアセンブラクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。（[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照。）
   * Create an `AssemblerServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. 既存のDDXドキュメントの参照

   * コンストラ `java.io.FileInputStream` クターを使用し、DDXファイルの場所を指定するstring値を渡して、DDXドキュメントを表すオブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. しおりを追加するPDFドキュメントを参照します。

   * コンストラクタ `java.io.FileInputStream` ーを使用し、PDFコンストラクターの場所を渡して、オブジェクトを作成します。ドキュメント
   * コンストラクタ `com.adobe.idp.Document` ーを使用してオブジェクトを作成し、PDFコン `java.io.FileInputStream` ストラクターを含むオブジェクトを渡します。ドキュメント

1. ブックマークXMLドキュメントの参照。

   * コンストラクタ `java.io.FileInputStream` ーを使用し、ブックマークXMLドキュメントーを表すXMLファイルの場所を渡して、オブジェクトを作成します。
   * オブジェクト `com.adobe.idp.Document` を作成し、PDFオ `java.io.FileInputStream` ブジェクトを渡します。ドキュメント

1. PDFドキュメント追加とブックマークXMLドキュメントのMapコレクション。

   * 入力PDF `java.util.Map` ドキュメントとブックマークXMLドキュメントの両方を保存する
   * 入追加力PDFドキュメントを使用するには、オブジェクトのメソッドを呼び出し、 `java.util.Map``put` 次の引数を渡します。

      * キー名を表すstring値です。 この値は、DDX要素で指定されたPDFソース要素の値と一致する必要があります。ドキュメント
      * 入力PDF `com.adobe.idp.Document` ドキュメントを含むオブジェクト。
   * ブ追加ックマークXMLドキュメントを使用するには、オブジェクトのメソッドを呼び出し `java.util.Map``put` 、次の引数を渡します。

      * キー名を表すstring値です。 この値は、DDX要素で指定されたBookmarksソース要素の値と一致する必要があります。ドキュメント
      * ブックマ `com.adobe.idp.Document` ークXMLドキュメントを含むオブジェクト。


1. 実行時オプションを設定します。

   * コンストラクタ `AssemblerOptionSpec` ーを使用して、実行時のオプションを格納するオブジェクトを作成します。
   * オブジェクトに属するメソッドを呼び出して、ビジネス要件に合わせて実行時のオプションを設定 `AssemblerOptionSpec` します。 例えば、エラーが発生した場合にジョブの処理を続行するようにAssemblerサービスに指示するには、オブジェクトのメ `AssemblerOptionSpec` ソッドを呼び出し `setFailOnError` て渡してくださ `false`い。

1. 「Assemble the PDF」ドキュメント。

   オブジェクト `AssemblerServiceClient` のメソッドを `invokeDDX` 呼び出し、次の必要な値を渡します。

   * 使用 `com.adobe.idp.Document` するDDXドキュメントを表すオブジェクト
   * 入力PDF `java.util.Map` ドキュメントとブックマークXMLドキュメントの両方を含むオブジェクト。
   * デフォ `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` ルトのフォントやジョブログレベルを含む、実行時のオプションを指定するオブジェクト。
   このメ `invokeDDX` ソッドは、ジ `com.adobe.livecycle.assembler.client.AssemblerResult` ョブの結果と発生した例外を含むオブジェクトを返します。

1. しおりを含むPDFドキュメントを保存します。

   新しく作成されたPDFアクションを取得するには、次のドキュメントを実行します。

   * オブジェクトの `AssemblerResult` メソッドを呼び出 `getDocuments` します。 オブジェクトを返 `java.util.Map` します。
   * 結果のオブジェクト `java.util.Map` が見つかるまで、オブジェクトを繰り返 `com.adobe.idp.Document` します。 (DDX要素で指定されたPDF結果ドキュメントを使用して、要素を取得できます)。
   * オブジェクト `com.adobe.idp.Document` のメソッドを呼 `copyToFile` び出して、PDFドキュメントを抽出します。

**関連トピック**

[クイック開始（SOAPモード）:Java APIを使用したPDFドキュメントとしおりのアセンブリ](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-documents-with-bookmarks-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## WebサービスAPIを使用して、PDFドキュメントをしおりでアセンブリする {#assemble-pdf-documents-with-bookmarks-using-the-web-service-api}

Assembler Service API（Webサービス）を使用して、PDFドキュメントをブックマークと共にアセンブリします。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. PDFアセンブラクライアントを作成します。

   * デフォルトのコンス `AssemblerServiceClient` トラクターを使用して、オブジェクトを作成します。
   * コンストラクタ `AssemblerServiceClient.Endpoint.Address` ーを使用してオブジェクトを作 `System.ServiceModel.EndpointAddress` 成します。 WSDLを指定するstring値をAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/AssemblerService?blob=mtom`)に渡します。 属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得して、オブジェクトを作成 `AssemblerServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のオプションを実行して、基本的なHTTP認証を有効にします。タスク

      * AEM formsのユーザー名をフィールドに割り当てま `AssemblerServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `AssemblerServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールドに `HttpClientCredentialType.Basic` 割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールドに `BasicHttpSecurityMode.TransportCredentialOnly` 割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. 既存のDDXドキュメントの参照

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオブ `BLOB` ジェクトは、DDXドキュメントの保存。
   * オブジェク `System.IO.FileStream` トを作成するには、コンストラクターを呼び出し、DDXドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトの内容を格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得す `System.IO.FileStream` ることで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイ `System.IO.FileStream` ト配列、開始位 `Read` 置およびストリームの長さを渡すことで、バイト配列にストリームデータを入力します。
   * バイト配列の `BLOB` 内容をフィールドに割り `MTOM` 当てて、オブジェクトを入力します。

1. しおりを追加するPDFドキュメントを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、入力PDFの保存に使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、入力PDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトの内容を格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得す `System.IO.FileStream` ることで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイ `System.IO.FileStream` ト配列、開始位 `Read` 置およびストリームの長さを渡すことで、バイト配列にストリームデータを入力します。
   * バイト配列の `BLOB` 内容をフィールドに割り `MTOM` 当てて、オブジェクトを入力します。

1. ブックマークXMLドキュメントの参照。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオブジ `BLOB` ェクトは、ブックマークXMLドキュメントの格納。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、入力PDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトの内容を格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得す `System.IO.FileStream` ることで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイ `System.IO.FileStream` ト配列、開始位 `Read` 置およびストリームの長さを渡すことで、バイト配列にストリームデータを入力します。
   * バイト配列の `BLOB` 内容をフィールドに割り `MTOM` 当てて、オブジェクトを入力します。

1. PDFドキュメント追加とブックマークXMLドキュメントのMapコレクション。

   * Create a `MyMapOf_xsd_string_To_xsd_anyType` object. このコレクションオブジェクトは、入力PDFコレクションとブックマークXMLドキュメントの格納に使用されます。ドキュメント
   * 入力PDFドキュメントとブックマークXMLドキュメントごとに、オブジェクトを作成 `MyMapOf_xsd_string_To_xsd_anyType_Item` します。
   * キー名を表すstring値をオブジェクトのフィールド `MyMapOf_xsd_string_To_xsd_anyType_Item` に割り当て `key` ます。 この値は、DDX要素で指定されたPDFソース要素の値と一致する必要があります。ドキュメント
   * PDFドキュメントを保 `BLOB` 存するオブジェクトをオブジェク `MyMapOf_xsd_string_To_xsd_anyType_Item` トのフィールドに割り当 `value` てます。
   * オ追加ブジェクト `MyMapOf_xsd_string_To_xsd_anyType_Item``MyMapOf_xsd_string_To_xsd_anyType` 。 Invoke the `MyMapOf_xsd_string_To_xsd_anyType` object&#39;s `Add` method and pass the `MyMapOf_xsd_string_To_xsd_anyType` object. (このタスクは、入力PDFドキュメントとブックマークXMLドキュメントごとに実行します)。

1. 実行時オプションを設定します。

   * コンストラクタ `AssemblerOptionSpec` ーを使用して、実行時のオプションを格納するオブジェクトを作成します。
   * オブジェクトに属するデータメンバーに値を割り当てて、ビジネス要件に合わせて実行時オプションを設定 `AssemblerOptionSpec` します。 例えば、エラーが発生した場合にジョブの処理を続行するようにAssemblerサービスに指示するには、オブジェクトの `false` データメ `AssemblerOptionSpec` ンバーに割り当 `failOnError` てます。

1. 「Assemble the PDF」ドキュメント。

   オブジェクト `AssemblerServiceClient` のメソッドを `invokeDDX` 呼び出し、次の値を渡します。

   * DDX `BLOB` ドキュメント
   * 入力 `MyMapOf_xsd_string_To_xsd_anyType` ドキュメント
   * 実行時 `AssemblerOptionSpec` のオプションを指定するオブジェクト
   このメ `invokeDDX` ソッドは、ジ `AssemblerResult` ョブの結果と発生した可能性のある例外を含むオブジェクトを返します。

1. しおりを含むPDFドキュメントを保存します。

   新しく作成されたPDFアクションを取得するには、次のドキュメントを実行します。

   * 結果のPDF `AssemblerResult` ドキュメントを `documents` 含むオブジェクト `Map` のフィールドにアクセスします。
   * 結果のオブジェ `Map` クトの名前と一致するキーが見つかるまで、オブジェクトを繰り返し処理します。ドキュメント 次に、その配列メンバーのをにキャ `value` ストしま `BLOB`す。
   * オブジェクトのフィールドにアクセスして、PDFドキュメントを表すバイナリ `BLOB` データを抽出 `MTOM` します。 PDFファイルに書き出すことのできるバイトの配列を返します。

**関連トピック**

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
