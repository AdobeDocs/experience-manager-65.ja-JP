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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# しおりを使用したPDFドキュメントのアセンブリ {#assembling-pdf-documents-with-bookmarks}

ブックマークを含むPDFドキュメントをアセンブリできます。 例えば、しおりを含まないPDFドキュメントがあり、しおりを指定して変更するとします。 Assemblerサービスを使用して、ブックマークを含まないPDFドキュメントを渡し、ブックマークを含むPDFドキュメントを取得できます。

ブックマークには、次のプロパティが含まれます。

* 画面にテキストとして表示されるタイトル。
* ユーザーがブックマークをクリックしたときの動作を指定するアクション。 ブックマークの一般的な操作は、現在のドキュメント内の別の場所に移動するか、別のPDFドキュメントを開くことですが、他の操作を指定することもできます。

この説明の目的で、次のDDXドキュメントが使用されているとします。

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

このDDXドキュメント内で、source属性に値が割り当てられています `Loan.pdf`。 このDDXドキュメントは、単一のPDFドキュメントがAssemblerサービスに渡されることを指定します。 PDFドキュメントをしおりとアセンブリする場合は、結果ドキュメントのしおりを説明するしおりXMLドキュメントを指定する必要があります。 ブックマークXMLドキュメントを指定するには、DDXドキュメントで `Bookmarks` 要素が指定されていることを確認します。

この例のDDXドキュメントでは、要素が `Bookmarks` 値として指 `doc2` 定されています。 この値は、Assemblerサービスに渡される入力マップに、という名前のキーが含まれていることを示しま `doc2`す。 キーの値は、ブッ `doc2` クマークXMLド `com.adobe.idp.Document` キュメントを表す値です。 (『 [Assembler Service and DDX Reference』の「Bookmarks Language」を参照](https://www.adobe.com/go/learn_aemforms_ddx_63))。

このトピックでは、次のXMLブックマーク言語を使用して、ブックマークを含むPDFドキュメントをアセンブリします。

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

このブックマークXMLドキュメント内に、ユーザーがブックマークをクリックしたときに実行されるアクションを定義するAction要素があることに注意してください。 アクション要素の下には、NotePadなどのアプリケーションを起動し、PDFファイルなどのファイルを開くLaunch要素があります。 PDFファイルを開くには、開くファイルを指定するFile要素を使用する必要があります。 例えば、この節で指定するブックマークXMLファイルでは、開かれるファイルの名前はLoanDetails.pdfです。

>[!NOTE]
>
>サポートされているアクションの詳細については、『 `Action` Assembler Service and DDX Reference』の「element」を参照してください [](https://www.adobe.com/go/learn_aemforms_ddx_63)。

この節で指定したDDXドキュメントと、ブックマークXMLファイルを入力として指定した場合、Assemblerサービスは、次のブックマークを含むPDFドキュメントをアセンブリします。

![aw_aw_bmark](assets/aw_aw_bmark.png)

ユーザーがOpen the Loan Details ** .pdfブックマークをクリックすると、LoanDetails.pdfが開きます。 同様に、ユーザーがNotePadの起動ブックマークをク *リックすると* 、NotePadが起動します。

>[!NOTE]
>
>この節を読む前に、Assemblerサービスを使用したPDFドキュメントのアセンブリについて詳しく知ることをお勧めします。 ここでは、入力ドキュメントを含むコレクションオブジェクトの作成や、返されるコレクションオブジェクトから結果を抽出する方法の学習など、概念については説明しません。 ( [Programmatically Assembling PDF Documents](/help/forms/developing/programmatically-assembling-pdf-documents-programmatical-assembling-pdf-documents-programmatics.md#programmatically-assembling-pdf-documents)を参照)。

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
1. 既存のDDXドキュメントを参照します。
1. ブックマークが追加されたPDFドキュメントを参照します。
1. ブックマークXMLドキュメントを参照します。
1. PDFドキュメントとブックマークXMLドキュメントをMapコレクションに追加します。
1. 実行時オプションを設定します。
1. PDFドキュメントをアセンブリします。
1. しおりを含むPDFドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar（AEM FormsがJBossにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsをJBossにデプロイする場合に必要）

aem formsがJBoss以外のサポート対象のJ2EEアプリケーションサーバーにデプロイされている場合は、adobe-utilities.jarファイルとjbossall-client.jarファイルを、AEM formsのデプロイ先のJ2EEアプリケーションサーバーに固有のJARファイルに置き換える必要があります。 For information about the location of all AEM Forms JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**PDFアセンブラクライアントの作成**

プログラムでAssembler操作を実行する前に、Assemblerサービスクライアントを作成する必要があります。

**既存のDDXドキュメントの参照**

PDFドキュメントをアセンブリするには、DDXドキュメントを参照する必要があります。 このDDXドキュメントには要素が含まれている必要が `Bookmarks` あります。この要素は、ブックマークを含むPDFをアセンブリするようAssemblerサービスに指示します。 （例については、この節で前述したDDXドキュメントを参照してください）。

**ブックマークが追加されたPDFドキュメントの参照**

ブックマークが追加されたPDFドキュメントを参照します。 参照先のPDFドキュメントに既にしおりが含まれているかどうかは関係ありません。 要素がPDF `Bookmarks` ソース要素の子である場合、PDFソースに既に存在するしおりがしおりに置き換えられます。 ただし、既存のしおりを維持する場合は、がPDFソース要素の兄弟であ `Bookmarks` ることを確認してください。 例えば、次の例を考えてみましょう。

```as3
 <PDF result="foo">
      <PDF source="inDoc"/>
      <Bookmarks source="doc2"/>
 </PDF>
```

**ブックマークXMLドキュメントの参照**

新しいしおりを含むPDFをアセンブリするには、しおりXMLドキュメントを参照する必要があります。 ブックマークXMLドキュメントは、Mapコレクションオブジェクト内のAssemblerサービスに渡されます。 （例については、この節で前述したブックマークXMLドキュメントを参照してください）。

>[!NOTE]
>
>『 [Assembler Service and DDX Reference』の「Bookmarks Language」を参照してください](https://www.adobe.com/go/learn_aemforms_ddx_63)。

**PDFドキュメントとブックマークXMLドキュメントをMapコレクションに追加します**

ブックマークを追加するPDFドキュメントとブックマークXMLドキュメントの両方をMapコレクションに追加する必要があります。 したがって、 mapコレクションオブジェクトには2つの要素が含まれます。pdfドキュメントとブックマークXMLドキュメント。

**実行時オプションの設定**

ジョブの実行中にAssemblerサービスの動作を制御する実行時オプションを設定できます。 例えば、エラーが発生した場合にジョブの処理を続行するようAssemblerサービスに指示するオプションを設定できます。 設定可能なランタイムオプションについて詳しくは、『 `AssemblerOptionSpec` AEM Forms APIリファレンス』のクラス [リファレンスを参照し](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)てください。

**PDFドキュメントのアセンブリ**

新しいブックマークを含むPDFドキュメントをアセンブリするには、Assemblerサービスの操作を使用 `invokeDDX` します。 この操作を他のAssemblerサービス操作（など）とは異なり使用する必要があるのは、AssemblerサービスがMapコレクションオブジェクト内で渡されるブックマークXMLドキュメントを必要とするからで `invokeDDX``invokeOneDocument` す。 このオブジェクトは、操作のパラメータ `invokeDDX` ーです。

**しおりを含むPDFドキュメントの保存**

返されたマップオブジェクトから結果を抽出し、対応するPDFドキュメントを保存する必要があります。 (『PDFドキュメントのプログラムによるアセンブリ』の [「結果の抽出」を参照](/help/forms/developing/programmatically-assembling-pdf-documents.md))。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDFドキュメントのプログラムによるアセンブリ](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java APIを使用したしおりを使用したPDFドキュメントのアセンブリ {#assemble-pdf-documents-with-bookmarks-using-the-java-api}

Assembler Service API(Java)を使用して、ブックマークを使用してPDFドキュメントをアセンブリします。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-assembler-client.jarなどのクライアントJARファイルを含めます。

1. PDFアセンブラクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。（[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照。）
   * Create an `AssemblerServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. 既存のDDXドキュメントを参照します。

   * コンストラ `java.io.FileInputStream` クターを使用し、DDXファイルの場所を指定するstring値を渡して、DDXドキュメントを表すオブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. ブックマークが追加されたPDFドキュメントを参照します。

   * コンストラクタ `java.io.FileInputStream` ーを使用し、PDFドキュメントの場所を渡して、オブジェクトを作成します。
   * コンストラクタ `com.adobe.idp.Document` ーを使用してオブジェクトを作成し、PDFドキュメントを含む `java.io.FileInputStream` オブジェクトを渡します。

1. ブックマークXMLドキュメントを参照します。

   * コンストラクタ `java.io.FileInputStream` ーを使用し、ブックマークXMLドキュメントを表すXMLファイルの場所を渡して、オブジェクトを作成します。
   * オブジェクト `com.adobe.idp.Document` を作成し、PDFドキュメントを含 `java.io.FileInputStream` むオブジェクトを渡します。

1. PDFドキュメントとブックマークXMLドキュメントをMapコレクションに追加します。

   * 入力PDFドキュ `java.util.Map` メントとブックマークXMLドキュメントの両方を保存するために使用するオブジェクトを作成します。
   * オブジェクトのメソッドを呼び出し、次の引 `java.util.Map` 数を渡して、入 `put` 力PDFドキュメントを追加します。

      * キー名を表すstring値です。 この値は、DDXドキュメントで指定されたPDFソース要素の値と一致する必要があります。
      * 入力PDF `com.adobe.idp.Document` ドキュメントを含むオブジェクトです。
   * オブジェクトのメソッドを呼び出し、次の引数を `java.util.Map` 渡して、ブックマ `put` ークXMLドキュメントを追加します。

      * キー名を表すstring値です。 この値は、DDXドキュメントで指定されたBookmarksソース要素の値と一致する必要があります。
      * ブックマ `com.adobe.idp.Document` ークXMLドキュメントを含むオブジェクトです。


1. 実行時オプションを設定します。

   * コンストラクタ `AssemblerOptionSpec` ーを使用して、実行時のオプションを格納するオブジェクトを作成します。
   * オブジェクトに属するメソッドを呼び出して、ビジネス要件に合わせて実行時のオプションを設定 `AssemblerOptionSpec` します。 例えば、エラーが発生した場合にジョブの処理を続行するようにAssemblerサービスに指示するには、オブジェクトのメソッド `AssemblerOptionSpec` を呼び出して `setFailOnError` 渡してくださ `false`い。

1. PDFドキュメントをアセンブリします。

   オブジェクト `AssemblerServiceClient` のメソッドを呼 `invokeDDX` び出し、次の必要な値を渡します。

   * 使用 `com.adobe.idp.Document` するDDXドキュメントを表すオブジェクト
   * 入力PDF `java.util.Map` ドキュメントとブックマークXMLドキュメントの両方を含むオブジェクトです。
   * デフォ `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` ルトのフォントやジョブログレベルを含む、実行時のオプションを指定するオブジェクト。
   このメ `invokeDDX` ソッドは、ジョ `com.adobe.livecycle.assembler.client.AssemblerResult` ブの結果と発生した例外を含むオブジェクトを返します。

1. しおりを含むPDFドキュメントを保存します。

   新しく作成したPDFドキュメントを取得するには、次の操作を実行します。

   * オブジェクト `AssemblerResult` のメソッドを呼び出 `getDocuments` します。 オブジェクトを返 `java.util.Map` します。
   * 結果のオブジェクト `java.util.Map` が見つかるまで、オブジェクトを繰り返 `com.adobe.idp.Document` します。 （DDXドキュメントで指定されたPDF結果要素を使用して、ドキュメントを取得できます）。
   * オブジェクト `com.adobe.idp.Document` のメソッドを呼 `copyToFile` び出してPDFドキュメントを抽出します。

**関連トピック**

[クイックスタート（SOAPモード）:Java APIを使用したブックマークを使用したPDFドキュメントのアセンブリ](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-documents-with-bookmarks-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## WebサービスAPIを使用したブックマークを使用したPDFドキュメントのアセンブリ {#assemble-pdf-documents-with-bookmarks-using-the-web-service-api}

Assembler Service API（Webサービス）を使用して、ブックマークを使用してPDFドキュメントをアセンブリします。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. PDFアセンブラクライアントを作成します。

   * デフォルトのコンス `AssemblerServiceClient` トラクターを使用して、オブジェクトを作成します。
   * コンストラクタ `AssemblerServiceClient.Endpoint.Address` ーを使用してオブジェクトを作 `System.ServiceModel.EndpointAddress` 成します。 WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/AssemblerService?blob=mtom`)に渡すstring値。 属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `AssemblerServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `AssemblerServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `AssemblerServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. 既存のDDXドキュメントを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオブ `BLOB` ジェクトは、DDXドキュメントの保存に使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、DDXドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイト配列、開 `System.IO.FileStream` 始位置、ストリ `Read` ーム長を渡すことによって、バイト配列にストリームデータを設定します。
   * オブジェクト `BLOB` にバイト配列の内容を `MTOM` フィールドに割り当てて、オブジェクトを入力します。

1. ブックマークが追加されたPDFドキュメントを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、入力PDFの保存に使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、入力PDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイト配列、開 `System.IO.FileStream` 始位置、ストリ `Read` ーム長を渡すことによって、バイト配列にストリームデータを設定します。
   * オブジェクト `BLOB` にバイト配列の内容を `MTOM` フィールドに割り当てて、オブジェクトを入力します。

1. ブックマークXMLドキュメントを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオブ `BLOB` ジェクトは、ブックマークXMLドキュメントの保存に使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、入力PDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイト配列、開 `System.IO.FileStream` 始位置、ストリ `Read` ーム長を渡すことによって、バイト配列にストリームデータを設定します。
   * オブジェクト `BLOB` にバイト配列の内容を `MTOM` フィールドに割り当てて、オブジェクトを入力します。

1. PDFドキュメントとブックマークXMLドキュメントをMapコレクションに追加します。

   * Create a `MyMapOf_xsd_string_To_xsd_anyType` object. このコレクションオブジェクトは、入力PDFドキュメントとブックマークXMLドキュメントを保存するために使用されます。
   * 入力PDFドキュメントとブックマークXMLドキュメントごとに、オブジェクトを作成 `MyMapOf_xsd_string_To_xsd_anyType_Item` します。
   * キー名を表すstring値をオブジェクトのフィールド `MyMapOf_xsd_string_To_xsd_anyType_Item` に割り当て `key` ます。 この値は、DDXドキュメントで指定されたPDFソース要素の値と一致する必要があります。
   * PDFドキュメント `BLOB` を保存するオブジェクトをオブジェクトのフィー `MyMapOf_xsd_string_To_xsd_anyType_Item` ルドに割り当 `value` てます。
   * オブジェクト `MyMapOf_xsd_string_To_xsd_anyType_Item` をオブジェクトに追加 `MyMapOf_xsd_string_To_xsd_anyType` します。 Invoke the `MyMapOf_xsd_string_To_xsd_anyType` object&#39;s `Add` method and pass the `MyMapOf_xsd_string_To_xsd_anyType` object. （このタスクは、入力PDFドキュメントとブックマークXMLドキュメントごとに実行します）。

1. 実行時オプションを設定します。

   * コンストラクタ `AssemblerOptionSpec` ーを使用して、実行時のオプションを格納するオブジェクトを作成します。
   * オブジェクトに属するデータメンバーに値を割り当てて、ビジネス要件に合わせて実行時オプションを設定 `AssemblerOptionSpec` します。 例えば、エラーが発生した場合にジョブの処理を続行するようAssemblerサービスに指示するには、オブジェクトの `false` データメ `AssemblerOptionSpec` ンバーに割り `failOnError` 当てます。

1. PDFドキュメントをアセンブリします。

   オブジェクト `AssemblerServiceClient` のメソッドを `invokeDDX` 呼び出し、次の値を渡します。

   * DDXドキ `BLOB` ュメントを表すオブジェクト
   * 入力ド `MyMapOf_xsd_string_To_xsd_anyType` キュメントを含む配列
   * 実行時 `AssemblerOptionSpec` のオプションを指定するオブジェクト
   このメ `invokeDDX` ソッドは、ジョ `AssemblerResult` ブの結果と発生した可能性のある例外を含むオブジェクトを返します。

1. しおりを含むPDFドキュメントを保存します。

   新しく作成したPDFドキュメントを取得するには、次の操作を実行します。

   * 結果のPDFドキュ `AssemblerResult` メントを含むオ `documents` ブジェクトのフ `Map` ィールドにアクセスします。
   * 結果のドキュメント `Map` の名前と一致するキーが見つかるまで、オブジェクトを繰り返し処理します。 次に、その配列メンバーのをにキャス `value` トしま `BLOB`す。
   * オブジェクトのフィールドにアクセスして、PDFドキュメントを表すバイナ `BLOB` リデータを抽出 `MTOM` します。 PDFファイルに書き出し可能なバイト配列を返します。

**関連トピック**

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
