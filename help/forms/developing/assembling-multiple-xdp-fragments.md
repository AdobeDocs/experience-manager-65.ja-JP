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
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1876'
ht-degree: 2%

---


# 複数のXDPフラグメントのアセンブリ{#assembling-multiple-xdp-fragments}

複数のXDPフラグメントを1つのXDPドキュメントにアセンブリできます。 例えば、各XDPファイルに、ヘルスフォームの作成に使用される1つ以上のサブフォームが含まれているXDPフラグメントについて考えてみましょう。 次の図に、アウトライン表示を示します(複数のXDPフラグメントの *アセンブリのクイック開始で使用されるtuc018_template_flowed.xdpファイルを表します* )。

![am_am_forma](assets/am_am_forma.png)

次の図に、患者のセクションを示します(複数のXDPフラグメントの *アセンブリのクイック開始で使用されるtuc018_contact.xdpファイルを表します* )。

![am_am_formb](assets/am_am_formb.png)

次の図に、患者の正常性の節を示します(複数のXDPフラグメントの *アセンブリのクイック開始で使用されるtuc018_patient.xdpファイルを表します* )。

![am_am_formc](assets/am_am_formc.png)

このフラグメントには、 *subPatientPhysical* およびsubPatientHealthという2つのサブフォームが含まれてい *ます*。 これらのサブフォームは両方とも、Assemblerサービスに渡されるDDXドキュメントで参照されます。 次の図に示すように、Assemblerサービスを使用すると、これらすべてのXDPフラグメントを1つのXDPドキュメントに結合できます。

![am_am_formd](assets/am_am_formd.png)

次のDDXドキュメントは、複数のXDPフラグメントをXDPドキュメントにアセンブリします。

```xml
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

DDXドキュメントには、結果の名前を指定するXDP `result` タグが含まれています。 この場合、値はです `tuc018result.xdp`。 この値は、Assemblerサービスが結果を返した後にXDPドキュメントを取得するために使用されるアプリケーションロジックで参照されます。 例えば、アセンブリ済みのXDPドキュメントを取得するために使用される次のJavaアプリケーションロジックについて考えてみます（値は太字で示しています）。

```java
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

この `XDP source` タグは、XDPフラグメントを追加するコンテナとして、またはXDPフラグメントを追加する多数のドキュメントの1つとして使用できる完全なXDPドキュメントを表すXDPファイルを指定します。 この場合、XDPドキュメントはコンテナとしてのみ使用されます(最初の図は「 *複数のXDPフラグメントの*&#x200B;アセンブリ」に示しています)。 つまり、他のXDPファイルはXDPコンテナ内に配置されます。

各サブフォームに対して、要素を追加できます(この `XDPContent` 要素はオプションです)。 上の例では、3つのサブフォームがあることに注意してください。 `subPatientContact`、 `subPatientPhysical`および `subPatientHealth`。 サブフォームとサブフォ `subPatientPhysical``subPatientHealth` ームの両方が同じXDPファイルtuc018_patient.xdpに存在します。 フラグメント要素は、Designerで定義されたサブフォームの名前を指定します。

>[!NOTE]
>
>For more information about the Assembler service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>DDXドキュメントについて詳しくは、『 [Assembler Service and DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63)』を参照してください。

## 手順の概要 {#summary-of-steps}

複数のXDPフラグメントをアセンブリするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. PDFアセンブラクライアントを作成します。
1. 既存のDDXドキュメントの参照。
1. XDPドキュメントを参照します。
1. 実行時オプションを設定します。
1. 複数のXDPドキュメントをアセンブリします。
1. アセンブリ済みのXDPドキュメントを取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(AEM FormsがJBossにデプロイされている場合に必要)
* jbossall-client.jar(AEM FormsがJBossにデプロイされている場合に必要)

**PDFアセンブラクライアントの作成**

プログラムによってAssembler操作を実行する前に、Assemblerサービスクライアントを作成します。

**既存のDDXドキュメントの参照**

複数のXDPドキュメントをアセンブリするには、DDXドキュメントを参照する必要があります。 このDDXドキュメントには、 `XDP result`、、 `XDP source`およびの各 `XDPContent` 要素が含まれている必要があります。

**XDPドキュメントの参照**

複数のXDPドキュメントをアセンブリするには、結果のXDPドキュメントのアセンブリに使用されるすべてのXDPファイルを参照します。 属性で参照されるXDPドキュメントに含まれるサブフォームの名前が、属性で指定されているこ `source` とを確認し `fragment` ます。 サブフォームはDesignerで定義されます。 例えば、次のXMLを考えてみましょう。

```xml
 <XDPContent insertionPoint="ddx_fragment" source="tuc018_contact.xdp" fragment="subPatientContact" required="false"/>
```

subPatientContactという名前のサブフォームは、 *tuc018_contact.xdpという名前のXDPファイル内に存在する* 必要があります **。

**実行時オプションの設定**

ジョブの実行中にAssemblerサービスの動作を制御する実行時オプションを設定できます。 例えば、エラーが発生した場合にジョブの処理を続行するようAssemblerサービスに指示するオプションを設定できます。

**複数のXDPドキュメントのアセンブリ**

複数のXDPファイルをアセンブリするには、 `invokeDDX` 操作を呼び出します。 Assemblerサービスは、コレクションオブジェクト内でアセンブルされたXDPドキュメントを返します。

**アセンブリ済みXDPドキュメントの取得**

アセンブリされたXDPドキュメントがコレクションオブジェクト内で返されます。 コレクションオブジェクトを繰り返し処理し、XDPドキュメントをXDPファイルとして保存します。 また、XDPドキュメントをOutputなどの別のAEM Formsサービスに渡すこともできます。

**関連トピック**

[Java APIを使用した複数のXDPフラグメントのアセンブリ](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-java-api)

[WebサービスAPIを使用した複数のXDPフラグメントのアセンブリ](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[プログラムによるPDFドキュメントのアセンブリ](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)

[フラグメントを使用したPDFドキュメントの作成](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments)

## Java APIを使用した複数のXDPフラグメントのアセンブリ {#assemble-multiple-xdp-fragments-using-the-java-api}

Assembler Service API(Java)を使用して、複数のXDPフラグメントをアセンブリします。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-assembler-client.jarなどのクライアントJARファイルを含めます。

1. PDFアセンブラクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `AssemblerServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. 既存のDDXドキュメントの参照。

   * コンストラクターを使用し、DDXファイルの場所を指定する文字列値を渡して、DDXドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. XDPドキュメントを参照します。

   * コンストラクターを使用して、入力XDPドキュメントの格納に使用する `java.util.Map` オブジェクトを作成し `HashMap` ます。
   * オブジェクトを作成し、入力XDPファイルを含む `com.adobe.idp.Document``java.io.FileInputStream` オブジェクトを渡します(このタスクはXDPファイルごとに繰り返します)。
   * メソッド追加を呼び出し、次の引数を渡すことによって、オブジェクトに対するエントリを作成します。 `java.util.Map``put`

      * キー名を表すstring値です。 この値は、DDXドキュメントで指定された `source` element値と一致する必要があります(このタスクを各XDPファイルに対して繰り返します)。
      * 要素に対応するXDPドキュメントを含む `com.adobe.idp.Document` オブジェクト( `source` このタスクをXDPファイルごとに繰り返します)。

1. 実行時オプションを設定します。

   * コンストラクターを使用して、実行時のオプションを格納する `AssemblerOptionSpec` オブジェクトを作成します。
   * オブジェクトに属するメソッドを呼び出して、ビジネス要件に合うように実行時オプションを設定し `AssemblerOptionSpec` ます。 例えば、エラーが発生した場合にジョブの処理を続行するようにAssemblerサービスに指示するには、 `AssemblerOptionSpec` オブジェクトの `setFailOnError` メソッドを呼び出して渡し `false`ます。

1. 複数のXDPドキュメントをアセンブリします。

   オブジェクトの `AssemblerServiceClient``invokeDDX` メソッドを呼び出し、次の必須値を渡します。

   * 使用するDDXドキュメントを表す `com.adobe.idp.Document` オブジェクトです
   * 入力XDPファイルを含む `java.util.Map` オブジェクト
   * デフォルトフォントやジョブログレベルなど、実行時のオプションを指定する `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` オブジェクト。

   この `invokeDDX` メソッドは、アセンブリされたXDPドキュメントを含む `com.adobe.livecycle.assembler.client.AssemblerResult` オブジェクトを返します。

1. アセンブリ済みのXDPドキュメントを取得します。

   アセンブリ済みのXDPドキュメントを取得するには、次の操作を実行します。

   * オブジェクトの `AssemblerResult` メソッドを呼び出し `getDocuments` ます。 このメソッドは、 `java.util.Map` オブジェクトを返します。
   * オブジェクトを繰り返し処理して、結果のオブジ `java.util.Map``com.adobe.idp.Document` ェクトを見つけます。
   * オブジェクトの `com.adobe.idp.Document``copyToFile` メソッドを呼び出して、アセンブリ済みのXDPドキュメントを抽出します。

**関連トピック**

[複数のXDPフラグメント](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)[クイック開始のアセンブリ（SOAPモード）: Java API](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-multiple-xdp-fragments-using-the-java-api)[IncludingAEM FormsJavaライブラリファイルを使用した複数のXDPフラグメントのアセンブリ接続プロパティ](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)[の設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## WebサービスAPIを使用した複数のXDPフラグメントのアセンブリ {#assemble-multiple-xdp-fragments-using-the-web-service-api}

Assembler Service API（Webサービス）を使用して、複数のXDPフラグメントをアセンブリします。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 サービス参照を設定する際は、次のWSDL定義を使用してください。

   ```java
    https://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   >[!NOTE]
   >
   >サーバーホスト `localhost` AEM FormsのIPアドレスに置き換えます。

1. PDFアセンブラクライアントを作成します。

   * デフォルトのコンストラクターを使用して `AssemblerServiceClient` オブジェクトを作成します。
   * コンストラクターを使用して `AssemblerServiceClient.Endpoint.Address` オブジェクトを作成し `System.ServiceModel.EndpointAddress` ます。 WSDLをAEM Formsサービス(など `https://localhost:8080/soap/services/AssemblerService?blob=mtom`)に渡すstring値を渡します。 属性を使用する必要はありません `lc_version` 。 この属性は、サービス参照を作成する際に使用されます。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `AssemblerServiceClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * AEM formsのユーザー名を `AssemblerServiceClient.ClientCredentials.UserName.UserName` フィールドに割り当てます。
      * 対応するパスワード値を `AssemblerServiceClient.ClientCredentials.UserName.Password`フィールドに割り当てます。
      * 定数値をフィー `HttpClientCredentialType.Basic``BasicHttpBindingSecurity.Transport.ClientCredentialType`ルドに割り当てます。
      * 定数値をフィー `BasicHttpSecurityMode.TransportCredentialOnly``BasicHttpBindingSecurity.Security.Mode`ルドに割り当てます。

1. 既存のDDXドキュメントの参照。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、DDXドキュメントの格納に使用されます。
   * コンストラクターを呼び出し、DDXドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
   * オブジェクトのメソッドを呼び出して、バイト配列にストリームデータ `System.IO.FileStream` を入力し `Read` ます。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * オブジェクトのプロパティにバイト配列の内容を割り当てて、 `BLOB``MTOM` オブジェクトを入力します。

1. XDPドキュメントを参照します。

   * 入力XDPファイルごとに、コンストラクターを使用して `BLOB` オブジェクトを作成します。 この `BLOB` オブジェクトは、入力ファイルの保存に使用されます。
   * コンストラクターを呼び出し、入力ファイルのファイルの場所とファイルを開くモードを表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
   * オブジェクトのメソッドを呼び出して、バイト配列にストリームデータ `System.IO.FileStream` を入力し `Read` ます。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * オブジェクトにバイト配列の内容を割り当てて、 `BLOB` オブジェクト `MTOM` を入力します。
   * Create a `MyMapOf_xsd_string_To_xsd_anyType` object. このコレクションオブジェクトは、アセンブリされたXDPドキュメントの作成に必要な入力ファイルの格納に使用します。
   * 各入力ファイルに対して、 `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトを作成します。
   * キー名を表すstring値を `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトの `key` フィールドに割り当てます。 この値は、DDXドキュメントで指定された要素の値と一致する必要があります。 (このタスクは、入力XDPファイルごとに実行します)。
   * 入力ファイルを格納している `BLOB` オブジェクトをオブジェクトのフィー `MyMapOf_xsd_string_To_xsd_anyType_Item` ルドに割り当て `value` ます。 (このタスクは、入力XDPファイルごとに実行します)。
   * オ追加ブジェクトをオブジ `MyMapOf_xsd_string_To_xsd_anyType_Item``MyMapOf_xsd_string_To_xsd_anyType` ェクトに追加します。 Invoke the `MyMapOf_xsd_string_To_xsd_anyType` object&#39;s `Add` method and pass the `MyMapOf_xsd_string_To_xsd_anyType` object. (このタスクは、入力XDPドキュメントごとに実行します)。

1. 実行時オプションを設定します。

   * コンストラクターを使用して、実行時のオプションを格納する `AssemblerOptionSpec` オブジェクトを作成します。
   * オブジェクトに属するデータメンバに値を割り当てることで、ビジネス要件に合った実行時オプションを設定し `AssemblerOptionSpec` ます。 例えば、エラーが発生した場合にジョブの処理を続行するようにAssemblerサービスに指示するには、 `false` オブジェクトの `AssemblerOptionSpec``failOnError` データメンバーに割り当てます。

1. 複数のXDPドキュメントをアセンブリします。

   オブジェクトの `AssemblerServiceClient``invokeDDX` メソッドを呼び出し、次の値を渡します。

   * DDXドキュメントを表す `BLOB` オブジェクトです
   * 必要なファイルを含む `MyMapOf_xsd_string_To_xsd_anyType` オブジェクトです
   * 実行時オプションを指定する `AssemblerOptionSpec` オブジェクトです。

   この `invokeDDX` メソッドは、ジョブの結果と発生した例外を含む `AssemblerResult` オブジェクトを返します。

1. アセンブリ済みのXDPドキュメントを取得します。

   新しく作成されたXDPドキュメントを取得するには、次の操作を実行します。

   * オブジェクトのフ `AssemblerResult` ィールドにアクセスします。この `documents` フィールドは、結果のPDFドキュメントを含む `Map` オブジェクトです。
   * オブジェクトを繰り返し処理して、 `Map` 各結果ドキュメントを取得します。 次に、その配列メンバーをにキャスト `value` し `BLOB`ます。
   * PDFドキュメントを表すバイナリデータを抽出するには、その `BLOB` オブジェクトの `MTOM` プロパティにアクセスします。 XDPファイルに書き出すことができるバイト配列を返します。

**関連トピック**

[MTOMを使用した複数のXDPフラグメントのアセンブリ](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)[呼び出しAEM Forms](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)