---
title: 複数のXDPフラグメントのアセンブリ
seo-title: 複数のXDPフラグメントのアセンブリ
description: 'null'
seo-description: 'null'
uuid: 0e35ff85-ff40-4878-ae31-aa8da75bd3ec
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: c4706632-02e5-4510-ad9c-4f732d5fbdad
docset: aem65
translation-type: tm+mt
source-git-commit: 9678b4979580bab23dea8ca7493b48b63d5bcfa6

---


# 複数のXDPフラグメントのアセンブリ{#assembling-multiple-xdp-fragments}

複数のXDPフラグメントを1つのXDPドキュメントにアセンブリできます。 例えば、各XDPファイルに、ヘルスフォームの作成に使用する1つ以上のサブフォームが含まれているXDPフラグメントについて考えてみましょう。 次の図に、アウトラインビューを示します(複数のXDPフラグメントのアセンブリクイックスタートで使用されるtuc018_template_flowed.xdp *ファイルを表し* ます)。

![am_am_forma](assets/am_am_forma.png)

次の図に、患者のセクションを示します(複数のXDPフラグメントのアセンブリクイックスタートで使用されるtuc018_contact.xdp *ファイルを表し* ます)。

![am_am_formb](assets/am_am_formb.png)

次の図に、患者の健康に関する節を示します(複数のXDPフラグメントのアセンブリのクイックスタートで使用されるtuc018_patient.xdp *ファイルを表します* )。

![am_am_formc](assets/am_am_formc.png)

このフラグメントには、subPatientPhysicalとsubPatientHealthという2つのサブフォ *ーム* が含ま *れます*。 これらのサブフォームは両方とも、Assemblerサービスに渡されるDDXドキュメント内で参照されます。 次の図に示すように、Assemblerサービスを使用して、これらすべてのXDPフラグメントを1つのXDPドキュメントに組み合わせることができます。

![am_am_formd](assets/am_am_formd.png)

次のDDXドキュメントは、複数のXDPフラグメントを1つのXDPドキュメントにアセンブリします。

```as3
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
         <XDP result="tuc018result.xdp">
            <XDP source="tuc018_template_flowed.xdp">
             <XDPContent insertionPoint="ddx_fragment" source="tuc018_contact.xdp" fragment="subPatientContact" required="false"/>
               <XDPContent insertionPoint="ddx_fragment" source="tuc018_patient.xdp" fragment="subPatientPhysical" required="false"/>
               <XDPContent insertionPoint="ddx_fragment" source="tuc018_patient.xdp" fragment="subPatientHealth" required="false"/>
            </XDP>
         </XDP>
 </DDX>
```

DDXドキュメントには、結果の名 `result` 前を指定するXDPタグが含まれています。 この場合、値はです `tuc018result.xdp`。 この値は、Assemblerサービスが結果を返した後にXDPドキュメントを取得するために使用されるアプリケーションロジックで参照されます。 例えば、アセンブリ済みのXDPドキュメントを取得するために使用される次のJavaアプリケーションロジックについて考えてみます（値は太字で示されています）。

```as3
 //Iterate through the map object to retrieve the result XDP document
 for (Iterator i = allDocs.entrySet().iterator(); i.hasNext();) {
     // Retrieve the Map object’s value
     Map.Entry e = (Map.Entry)i.next();
     //Get the key name as specified in the
     //DDX document
     String keyName = (String)e.getKey();
     if (keyName.equalsIgnoreCase("tuc018result.xdp"))
                 {
         Object o = e.getValue();
         outDoc = (Document)o;
         //Save the result PDF file
         File myOutFile = new File("C:\\AssemblerResultXDP.xdp");
         outDoc.copyToFile(myOutFile);
     }
 }
```

このタ `XDP source` グは、XDPフラグメントを追加するコンテナとして、または同時に追加される多数のドキュメントの1つとして使用できる完全なXDPドキュメントを表すXDPファイルを指定します。 この場合、XDPドキュメントはコンテナとしてのみ使用されます(最初の図は「複数のXDPフラグメントの *アセンブリ*」を参照)。 つまり、他のXDPファイルはXDPコンテナ内に配置されます。

各サブフォームに対して、要素を追加できます(こ `XDPContent` の要素はオプションです)。 上の例では、3つのサブフォームがあることに注意してください。 `subPatientContact`、 `subPatientPhysical`、、 `subPatientHealth`、 サブフォ `subPatientPhysical` ームとサブフ `subPatientHealth` ォームの両方が同じXDPファイルtuc018_patient.xdp内にあります。 フラグメント要素は、Designerで定義されたサブフォームの名前を指定します。

>[!NOTE]
>
>For more information about the Assembler service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>DDXドキュメントについて詳しくは、 [Assembler Service and DDX Referenceを参照してください](https://www.adobe.com/go/learn_aemforms_ddx_63)。

## 手順の概要 {#summary-of-steps}

複数のXDPフラグメントをアセンブリするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. PDFアセンブラクライアントを作成します。
1. 既存のDDXドキュメントを参照します。
1. XDPドキュメントの参照。
1. 実行時オプションを設定します。
1. 複数のXDPドキュメントをアセンブリします。
1. アセンブリされたXDPドキュメントを取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar（AEM FormsがJBossにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsをJBossにデプロイする場合に必要）

**PDFアセンブラクライアントの作成**

プログラムによってAssembler操作を実行する前に、Assemblerサービスクライアントを作成します。

**既存のDDXドキュメントの参照**

複数のXDPドキュメントをアセンブリするには、DDXドキュメントを参照する必要があります。 このDDXドキュメントには、、、およ `XDP result`びのエレメ `XDP source`ントが含まれて `XDPContent` いる必要があります。

**XDPドキュメントの参照**

複数のXDPドキュメントをアセンブリするには、結果のXDPドキュメントのアセンブリに使用されるすべてのXDPファイルを参照します。 属性で参照されるXDPドキュメントに含まれるサブフォームの名前が属性で指定されてい `source` ることを確認してく `fragment` ださい。 サブフォームはDesignerで定義します。 例えば、次のXMLを考えてみましょう。

```as3
 <XDPContent insertionPoint="ddx_fragment" source="tuc018_contact.xdp" fragment="subPatientContact" required="false"/>
```

subPatientContactという名前のサブフ *ォームは* 、 *tuc018_contact.xdpという名前のXDPファイル内に存在する必要があります*。

**実行時オプションの設定**

ジョブの実行中にAssemblerサービスの動作を制御する実行時オプションを設定できます。 例えば、エラーが発生した場合にジョブの処理を続行するようAssemblerサービスに指示するオプションを設定できます。

**複数のXDPドキュメントのアセンブリ**

複数のXDPファイルをアセンブリするには、操作を呼び出 `invokeDDX` します。 Assemblerサービスは、コレクションオブジェクト内でアセンブリされたXDPドキュメントを返します。

**アセンブリ済みXDPドキュメントの取得**

アセンブリ済みのXDPドキュメントがコレクションオブジェクト内で返されます。 コレクションオブジェクトを繰り返し処理し、XDPドキュメントをXDPファイルとして保存します。 また、XDPドキュメントをOutputなどの別のAEM Formsサービスに渡すこともできます。

**関連トピック**

[Java APIを使用した複数のXDPフラグメントのアセンブリ](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-java-api)

[WebサービスAPIを使用した複数のXDPフラグメントのアセンブリ](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDFドキュメントのプログラムによるアセンブリ](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)

[フラグメントを使用したPDFドキュメントの作成](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments)

## Java APIを使用した複数のXDPフラグメントのアセンブリ {#assemble-multiple-xdp-fragments-using-the-java-api}

Assembler Service API(Java)を使用して、複数のXDPフラグメントをアセンブリします。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-assembler-client.jarなどのクライアントJARファイルを含めます。

1. PDFアセンブラクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `AssemblerServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. 既存のDDXドキュメントを参照します。

   * コンストラ `java.io.FileInputStream` クターを使用し、DDXファイルの場所を指定するstring値を渡して、DDXドキュメントを表すオブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. XDPドキュメントの参照。

   * コンストラク `java.util.Map` ターを使用して、入力XDPドキュメントの保存に使用するオブジェクトを作成 `HashMap` します。
   * オブジェクト `com.adobe.idp.Document` を作成し、入力XDPフ `java.io.FileInputStream` ァイルを含むオブジェクトを渡します（各XDPファイルに対してこのタスクを繰り返します）。
   * メソッドを呼び出し、次 `java.util.Map` の引数を渡して、オ `put` ブジェクトにエントリを追加します。

      * キー名を表すstring値です。 この値は、DDXドキュメントで `source` 指定された要素の値と一致する必要があります（各XDPファイルに対してこのタスクを繰り返します）。
      * 要素 `com.adobe.idp.Document` に対応するXDPドキュメントを含むオブジェクト(各XDP `source` ファイルに対してこのタスクを繰り返します)。

1. 実行時オプションを設定します。

   * コンストラクタ `AssemblerOptionSpec` ーを使用して、実行時のオプションを格納するオブジェクトを作成します。
   * オブジェクトに属するメソッドを呼び出して、ビジネス要件に合わせて実行時のオプションを設定 `AssemblerOptionSpec` します。 例えば、エラーが発生した場合にジョブの処理を続行するようにAssemblerサービスに指示するには、オブジェクトのメソッド `AssemblerOptionSpec` を呼び出して `setFailOnError` 渡してくださ `false`い。

1. 複数のXDPドキュメントをアセンブリします。

   オブジェクト `AssemblerServiceClient` のメソッドを呼 `invokeDDX` び出し、次の必要な値を渡します。

   * 使用す `com.adobe.idp.Document` るDDXドキュメントを表すオブジェクトです
   * 入力XDP `java.util.Map` ファイルを含むオブジェクト
   * デフォ `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` ルトフォントやジョブログレベルなど、実行時のオプションを指定するオブジェクトです
   このメソ `invokeDDX` ッドは、アセンブリ `com.adobe.livecycle.assembler.client.AssemblerResult` されたXDPドキュメントを含むオブジェクトを返します。

1. アセンブリされたXDPドキュメントを取得します。

   アセンブリ済みのXDPドキュメントを取得するには、次の操作を実行します。

   * オブジェクト `AssemblerResult` のメソッドを呼び出 `getDocuments` します。 このメソッドは、オブジェクトを `java.util.Map` 返します。
   * 結果のオブジェクト `java.util.Map` が見つかるまで、オブジェクトを繰り返 `com.adobe.idp.Document` します。
   * オブジェクト `com.adobe.idp.Document` のメソッドを呼び `copyToFile` 出して、アセンブリ済みのXDPドキュメントを抽出します。

**関連トピック**

[Assembling Multiple XDP Fragments](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)[Quick Start（SOAPモード）:AEM Forms javaライブラリファイルを含むJava APIを使用した複数のXDP](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-multiple-xdp-fragments-using-the-java-api)[フラグメントのアセンブリ接続プロパティの](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)[設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## WebサービスAPIを使用した複数のXDPフラグメントのアセンブリ {#assemble-multiple-xdp-fragments-using-the-web-service-api}

Assembler Service API（Webサービス）を使用して、複数のXDPフラグメントをアセンブリします。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 サービス参照を設定する際は、必ず次のWSDL定義を使用してください。

   ```as3
    https://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. PDFアセンブラクライアントを作成します。

   * デフォルトのコンス `AssemblerServiceClient` トラクターを使用して、オブジェクトを作成します。
   * コンストラクタ `AssemblerServiceClient.Endpoint.Address` ーを使用してオブジェクトを作 `System.ServiceModel.EndpointAddress` 成します。 WSDLをAEM Formsサービス（例：）に渡すstring値 `https://localhost:8080/soap/services/AssemblerService?blob=mtom`。 属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `AssemblerServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当 `AssemblerServiceClient.ClientCredentials.UserName.UserName` てます。
      * 対応するパスワード値をフィールドに割り当 `AssemblerServiceClient.ClientCredentials.UserName.Password`てます。
      * 定数値をフ `HttpClientCredentialType.Basic` ィールドに割り当 `BasicHttpBindingSecurity.Transport.ClientCredentialType`てます。
      * 定数値をフ `BasicHttpSecurityMode.TransportCredentialOnly` ィールドに割り当 `BasicHttpBindingSecurity.Security.Mode`てます。

1. 既存のDDXドキュメントを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオブ `BLOB` ジェクトは、DDXドキュメントの保存に使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、DDXドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出して、バイト配列にストリームデ `System.IO.FileStream` ータを入力 `Read` します。 読み取るバイト配列、開始位置およびストリーム長を渡します。
   * オブジェクト `BLOB` にバイト配列の内容をプロ `MTOM` パティに割り当てて、オブジェクトを設定します。

1. XDPドキュメントの参照。

   * 各入力XDPファイルに対して、コンストラクターを使 `BLOB` 用してオブジェクトを作成します。 このオ `BLOB` ブジェクトは、入力ファイルの保存に使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、入力ファイルのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出して、バイト配列にストリームデ `System.IO.FileStream` ータを入力 `Read` します。 読み取るバイト配列、開始位置およびストリーム長を渡します。
   * オブジェクト `BLOB` にバイト配列の内容を `MTOM` フィールドに割り当てて、オブジェクトを入力します。
   * Create a `MyMapOf_xsd_string_To_xsd_anyType` object. このコレクションオブジェクトは、アセンブリ済みのXDPドキュメントの作成に必要な入力ファイルの保存に使用されます。
   * 入力ファイルごとに、オブジェクトを作成 `MyMapOf_xsd_string_To_xsd_anyType_Item` します。
   * キー名を表すstring値をオブジェクトのフィールド `MyMapOf_xsd_string_To_xsd_anyType_Item` に割り当て `key` ます。 この値は、DDXドキュメントで指定されたエレメントの値と一致する必要があります。 （入力XDPファイルごとにこのタスクを実行します）。
   * 入力ファイル `BLOB` を格納するオブジェクトをオブジェクトのフィー `MyMapOf_xsd_string_To_xsd_anyType_Item` ルドに割り当 `value` てます。 （入力XDPファイルごとにこのタスクを実行します）。
   * オブジェクト `MyMapOf_xsd_string_To_xsd_anyType_Item` をオブジェクトに追加 `MyMapOf_xsd_string_To_xsd_anyType` します。 Invoke the `MyMapOf_xsd_string_To_xsd_anyType` object&#39;s `Add` method and pass the `MyMapOf_xsd_string_To_xsd_anyType` object. （このタスクは、入力XDPドキュメントごとに実行します）。

1. 実行時オプションを設定します。

   * コンストラクタ `AssemblerOptionSpec` ーを使用して、実行時のオプションを格納するオブジェクトを作成します。
   * オブジェクトに属するデータメンバーに値を割り当てて、ビジネス要件に合わせて実行時オプションを設定 `AssemblerOptionSpec` します。 例えば、エラーが発生した場合にジョブの処理を続行するようAssemblerサービスに指示するには、オブジェクトの `false` データメ `AssemblerOptionSpec` ンバーに割り `failOnError` 当てます。

1. 複数のXDPドキュメントをアセンブリします。

   オブジェクト `AssemblerServiceClient` のメソッドを `invokeDDX` 呼び出し、次の値を渡します。

   * DDXドキ `BLOB` ュメントを表すオブジェクト
   * 必要な `MyMapOf_xsd_string_To_xsd_anyType` ファイルを含むオブジェクトです
   * 実行時 `AssemblerOptionSpec` のオプションを指定するオブジェクト
   このメ `invokeDDX` ソッドは、ジョ `AssemblerResult` ブの結果と発生した例外を含むオブジェクトを返します。

1. アセンブリされたXDPドキュメントを取得します。

   新しく作成されたXDPドキュメントを取得するには、次の操作を実行します。

   * 結果のPDFドキ `AssemblerResult` ュメントを含むオ `documents` ブジェクトのフ `Map` ィールドにアクセスします。
   * オブジェクトを繰り返し `Map` 処理し、各結果ドキュメントを取得します。 次に、その配列メンバーをにキャス `value` トします `BLOB`。
   * PDFドキュメントを表すバイナリデータを抽出するには、そのオブジェクトのプロパ `BLOB` ティにアクセス `MTOM` します。 XDPファイルに書き出すことができるバイトの配列を返します。

**関連トピック**

[MTOMを使用した複数のXDPフラグメ](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)[ントのアセンブリAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)