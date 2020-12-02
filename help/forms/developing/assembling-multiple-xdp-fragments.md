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

複数のXDPフラグメントを1つのXDPドキュメントにアセンブリできます。 例えば、各XDPファイルに、ヘルスフォームの作成に使用される1つ以上のサブフォームが含まれているXDPフラグメントについて考えてみましょう。 次の図に、アウトライン表示を示します（tuc018_template_flowed.xdpファイルを表します）。このファイルは、*複数のXDPフラグメントのアセンブリ*&#x200B;クイック開始で使用されます。

![am_am_forma](assets/am_am_forma.png)

次の図に、患者のセクション(*複数のXDPフラグメントのアセンブリ*&#x200B;クイック開始で使用されるtuc018_contact.xdpファイルを表します)を示します。

![am_am_formb](assets/am_am_formb.png)

次の図に、患者の正常性のセクションを示します(*複数のXDPフラグメントのアセンブリ*&#x200B;クイック開始で使用されるtuc018_patient.xdpファイルを表します)。

![am_am_formc](assets/am_am_formc.png)

このフラグメントには、*subPatientPhysical*&#x200B;および&#x200B;*subPatientHealth*&#x200B;という2つのサブフォームが含まれています。 これらのサブフォームは両方とも、Assemblerサービスに渡されるDDXドキュメントで参照されます。 次の図に示すように、Assemblerサービスを使用すると、これらすべてのXDPフラグメントを1つのXDPドキュメントに結合できます。

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

DDXドキュメントには、結果の名前を指定するXDP `result`タグが含まれています。 この場合、値は`tuc018result.xdp`です。 この値は、Assemblerサービスが結果を返した後にXDPドキュメントを取得するために使用されるアプリケーションロジックで参照されます。 例えば、アセンブリ済みのXDPドキュメントを取得するために使用される次のJavaアプリケーションロジックについて考えてみます（値は太字で示しています）。

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

`XDP source`タグは、XDPフラグメントを追加するコンテナとして、またはXDPフラグメントを追加する多数のドキュメントの1つとして使用できる完全なXDPドキュメントを表すXDPファイルを指定します。 この場合、XDPドキュメントはコンテナとしてのみ使用されます（最初の図は「*複数のXDPフラグメントのアセンブリ*」に示しています）。 つまり、他のXDPファイルはXDPコンテナ内に配置されます。

各サブフォームに対して、`XDPContent`要素を追加できます（この要素はオプションです）。 上の例では、3つのサブフォームがあることに注意してください。`subPatientContact`、`subPatientPhysical`、`subPatientHealth`。 `subPatientPhysical`サブフォームと`subPatientHealth`サブフォームはどちらも同じXDPファイルtuc018_patient.xdpに存在します。 フラグメント要素は、Designerで定義されたサブフォームの名前を指定します。

>[!NOTE]
>
>Assemblerサービスについて詳しくは、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

>[!NOTE]
>
>DDXドキュメントについて詳しくは、「[Assembler Service and DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63)」を参照してください。

## 手順{#summary-of-steps}の概要

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

複数のXDPドキュメントをアセンブリするには、DDXドキュメントを参照する必要があります。 このDDXドキュメントには、`XDP result`、`XDP source`および`XDPContent`の各要素を含める必要があります。

**XDPドキュメントの参照**

複数のXDPドキュメントをアセンブリするには、結果のXDPドキュメントのアセンブリに使用されるすべてのXDPファイルを参照します。 `source`属性で参照されるXDPドキュメントに含まれるサブフォームの名前が`fragment`属性で指定されていることを確認します。 サブフォームはDesignerで定義されます。 例えば、次のXMLを考えてみましょう。

```xml
 <XDPContent insertionPoint="ddx_fragment" source="tuc018_contact.xdp" fragment="subPatientContact" required="false"/>
```

*subPatientContact*&#x200B;という名前のサブフォームは、*tuc018_contact.xdp*&#x200B;という名前のXDPファイル内に存在する必要があります。

**実行時オプションの設定**

ジョブの実行中にAssemblerサービスの動作を制御する実行時オプションを設定できます。 例えば、エラーが発生した場合にジョブの処理を続行するようAssemblerサービスに指示するオプションを設定できます。

**複数のXDPドキュメントのアセンブリ**

複数のXDPファイルをアセンブリするには、`invokeDDX`操作を呼び出します。 Assemblerサービスは、コレクションオブジェクト内でアセンブルされたXDPドキュメントを返します。

**アセンブリ済みXDPドキュメントの取得**

アセンブリされたXDPドキュメントがコレクションオブジェクト内で返されます。 コレクションオブジェクトを繰り返し処理し、XDPドキュメントをXDPファイルとして保存します。 XDPドキュメントは、Outputなどの別のAEM Formsサービスに渡すこともできます。

**関連トピック**

[Java APIを使用した複数のXDPフラグメントのアセンブリ](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-java-api)

[WebサービスAPIを使用した複数のXDPフラグメントのアセンブリ](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[プログラムによるPDFドキュメントのアセンブリ](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)

[フラグメントを使用したPDFドキュメントの作成](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments)

## Java API {#assemble-multiple-xdp-fragments-using-the-java-api}を使用した複数のXDPフラグメントのアセンブリ

Assembler Service API(Java)を使用して、複数のXDPフラグメントをアセンブリします。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-assembler-client.jarなどのクライアントJARファイルを含めます。

1. PDFアセンブラクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用し、`AssemblerServiceClient`オブジェクトを渡して、`ServiceClientFactory`オブジェクトを作成します。

1. 既存のDDXドキュメントの参照。

   * コンストラクターを使用し、DDXファイルの場所を指定する文字列値を渡して、DDXドキュメントを表す`java.io.FileInputStream`オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. XDPドキュメントを参照します。

   * `HashMap`コンストラクターを使用して、入力XDPドキュメントの格納に使用する`java.util.Map`オブジェクトを作成します。
   * `com.adobe.idp.Document`オブジェクトを作成し、入力XDPファイルを含む`java.io.FileInputStream`オブジェクトを渡します(このタスクを各XDPファイルに対して繰り返します)。
   * &lt;a0追加/>オブジェクトへのエントリ。その`java.util.Map`メソッドを呼び出し、次の引数を渡すことによって作成します。`put`

      * キー名を表すstring値です。 この値は、DDXドキュメントで指定された`source`要素の値と一致する必要があります(XDPファイルごとにこのタスクを繰り返します)。
      * `source`要素に対応するXDPドキュメントを含む`com.adobe.idp.Document`オブジェクト(XDPファイルごとにこのタスクを繰り返します)。

1. 実行時オプションを設定します。

   * コンストラクターを使用して、実行時オプションを格納する`AssemblerOptionSpec`オブジェクトを作成します。
   * `AssemblerOptionSpec`オブジェクトに属するメソッドを呼び出して、ビジネス要件に合うように実行時オプションを設定します。 例えば、エラーが発生した場合にジョブの処理を続行するようにAssemblerサービスに指示するには、`AssemblerOptionSpec`オブジェクトの`setFailOnError`メソッドを呼び出し、`false`を渡します。

1. 複数のXDPドキュメントをアセンブリします。

   `AssemblerServiceClient`オブジェクトの`invokeDDX`メソッドを呼び出し、次の必須値を渡します。

   * 使用するDDXドキュメントを表す`com.adobe.idp.Document`オブジェクト
   * 入力XDPファイルが含まれる`java.util.Map`オブジェクト
   * デフォルトフォントとジョブログレベルを含む、実行時のオプションを指定する`com.adobe.livecycle.assembler.client.AssemblerOptionSpec`オブジェクト

   `invokeDDX`メソッドは、アセンブリされたXDPドキュメントを含む`com.adobe.livecycle.assembler.client.AssemblerResult`オブジェクトを返します。

1. アセンブリ済みのXDPドキュメントを取得します。

   アセンブリ済みのXDPドキュメントを取得するには、次の操作を実行します。

   * `AssemblerResult`オブジェクトの`getDocuments`メソッドを呼び出します。 このメソッドは、`java.util.Map`オブジェクトを返します。
   * `java.util.Map`オブジェクトを繰り返し処理して、結果の`com.adobe.idp.Document`オブジェクトを見つけます。
   * `com.adobe.idp.Document`オブジェクトの`copyToFile`メソッドを呼び出して、アセンブリ済みのXDPドキュメントを抽出します。

**関連トピック**

[複数のXDP](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)
[フラグメントのアセンブリクイック開始（SOAPモード）:Java APIを使用した複数のXDPフラグメントのアセンブリ(AEM FormsJavaライブラリ](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-multiple-xdp-fragments-using-the-java-api)
[](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[ファイルを含む)接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## WebサービスAPI {#assemble-multiple-xdp-fragments-using-the-web-service-api}を使用して複数のXDPフラグメントをアセンブリする

Assembler Service API（Webサービス）を使用して、複数のXDPフラグメントをアセンブリします。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 サービス参照を設定する際は、次のWSDL定義を使用してください。

   ```java
    https://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. PDFアセンブラクライアントを作成します。

   * `AssemblerServiceClient`オブジェクトを作成するには、そのオブジェクトのデフォルトのコンストラクタを使用します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`AssemblerServiceClient.Endpoint.Address`オブジェクトを作成します。 `https://localhost:8080/soap/services/AssemblerService?blob=mtom`など、WSDLをAEM Formsサービスに渡す文字列値を渡します。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する際に使用されます。
   * `AssemblerServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * AEM formsユーザー名を`AssemblerServiceClient.ClientCredentials.UserName.UserName`フィールドに割り当てます。
      * 対応するパスワード値を`AssemblerServiceClient.ClientCredentials.UserName.Password`フィールドに割り当てます。
      * `HttpClientCredentialType.Basic`定数値を`BasicHttpBindingSecurity.Transport.ClientCredentialType`フィールドに割り当てます。
      * `BasicHttpSecurityMode.TransportCredentialOnly`定数値を`BasicHttpBindingSecurity.Security.Mode`フィールドに割り当てます。

1. 既存のDDXドキュメントの参照。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、DDXドキュメントの保存に使用されます。
   * コンストラクターを呼び出し、DDXドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得して、バイト配列のサイズを決定できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出して、バイト配列にストリームデータを入力します。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * `BLOB`オブジェクトに`MTOM`プロパティを割り当て、バイト配列の内容を指定します。

1. XDPドキュメントを参照します。

   * 各入力XDPファイルに対して、コンストラクターを使用して`BLOB`オブジェクトを作成します。 `BLOB`オブジェクトは、入力ファイルの保存に使用されます。
   * コンストラクターを呼び出し、入力ファイルのファイルの場所とファイルを開くモードを表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得して、バイト配列のサイズを決定できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出して、バイト配列にストリームデータを入力します。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * `BLOB`オブジェクトに、`MTOM`フィールドにバイト配列の内容を割り当てて入力します。
   * `MyMapOf_xsd_string_To_xsd_anyType`オブジェクトを作成します。 このコレクションオブジェクトは、アセンブリされたXDPドキュメントの作成に必要な入力ファイルの格納に使用します。
   * 入力ファイルごとに、`MyMapOf_xsd_string_To_xsd_anyType_Item`オブジェクトを作成します。
   * キー名を表すstring値を`MyMapOf_xsd_string_To_xsd_anyType_Item`オブジェクトの`key`フィールドに割り当てます。 この値は、DDXドキュメントで指定された要素の値と一致する必要があります。 (このタスクは、入力XDPファイルごとに実行します)。
   * 入力ファイルを保存する`BLOB`オブジェクトを`MyMapOf_xsd_string_To_xsd_anyType_Item`オブジェクトの`value`フィールドに割り当てます。 (このタスクは、入力XDPファイルごとに実行します)。
   * 追加`MyMapOf_xsd_string_To_xsd_anyType`オブジェクトの`MyMapOf_xsd_string_To_xsd_anyType_Item`オブジェクト。 `MyMapOf_xsd_string_To_xsd_anyType`オブジェクトの`Add`メソッドを呼び出し、`MyMapOf_xsd_string_To_xsd_anyType`オブジェクトを渡します。 (このタスクは、入力XDPドキュメントごとに実行します)。

1. 実行時オプションを設定します。

   * コンストラクターを使用して、実行時オプションを格納する`AssemblerOptionSpec`オブジェクトを作成します。
   * `AssemblerOptionSpec`オブジェクトに属するデータメンバに値を割り当てて、ビジネス要件に合うように実行時オプションを設定します。 例えば、エラーが発生した場合にジョブの処理を続行するようにAssemblerサービスに指示するには、`false`を`AssemblerOptionSpec`オブジェクトの`failOnError`データメンバーに割り当てます。

1. 複数のXDPドキュメントをアセンブリします。

   `AssemblerServiceClient`オブジェクトの`invokeDDX`メソッドを呼び出し、次の値を渡します。

   * DDXドキュメントを表す`BLOB`オブジェクト
   * 必要なファイルを含む`MyMapOf_xsd_string_To_xsd_anyType`オブジェクト
   * 実行時オプションを指定する`AssemblerOptionSpec`オブジェクト

   `invokeDDX`メソッドは、ジョブの結果と発生した例外を含む`AssemblerResult`オブジェクトを返します。

1. アセンブリ済みのXDPドキュメントを取得します。

   新しく作成されたXDPドキュメントを取得するには、次の操作を実行します。

   * `AssemblerResult`オブジェクトの`documents`フィールドにアクセスします。これは、結果のPDFドキュメントを含む`Map`オブジェクトです。
   * `Map`オブジェクトを繰り返し処理して、各結果ドキュメントを取得します。 次に、その配列メンバーの`value`を`BLOB`にキャストします。
   * `BLOB`オブジェクトの`MTOM`プロパティにアクセスして、PDFドキュメントを表すバイナリデータを抽出します。 XDPファイルに書き出すことができるバイト配列を返します。

**関連トピック**

[複数のXDP](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)
[フラグメントのアセンブリMTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)