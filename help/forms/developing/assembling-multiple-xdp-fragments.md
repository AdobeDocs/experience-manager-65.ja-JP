---
title: 複数の XDP フラグメントのアセンブル
seo-title: Assembling Multiple XDP Fragments
description: Java API と Web Service API を使用して、複数の XDP フラグメントを単一の XDP ドキュメントにアセンブルします。
seo-description: Assemble multiple XDP fragments into a single XDP document using the Java API and Web Service API.
uuid: 0e35ff85-ff40-4878-ae31-aa8da75bd3ec
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: c4706632-02e5-4510-ad9c-4f732d5fbdad
docset: aem65
role: Developer
exl-id: 54d98c69-2b2e-46cb-9f6a-7e9bdbe5c378
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '1887'
ht-degree: 100%

---

# 複数の XDP フラグメントのアセンブル{#assembling-multiple-xdp-fragments}

複数の XDP フラグメントを単一の XDP ドキュメントにアセンブルできます。例えば、各 XDP ファイルに、ヘルスフォームの作成に使用される 1 つ以上のサブフォームが含まれている XDP フラグメントについて考えてみましょう。 次の図に、アウトラインビューを示します（*複数の XDP フラグメントのアセンブル*&#x200B;クイックスタートで使用される tuc018_template_flowed.xdp ファイルを表わしています）。

![am_am_forma](assets/am_am_forma.png)

次の図に、「patient」セクションを示します（*複数の XDP フラグメントのアセンブル*&#x200B;クイックスタートで使用される tuc018_contact.xdp ファイルを表わしています）。

![am_am_formb](assets/am_am_formb.png)

次の図に、「patient health」セクションを示します（*複数の XDP フラグメントのアセンブル*&#x200B;クイックスタートで使用される tuc018_patient.xdp ファイルを表わしています）。

![am_am_formc](assets/am_am_formc.png)

このフラグメントには、*subPatientPhysical* および *subPatientHealth* という 2 つのサブフォームが含まれています。これらの両方のサブフォームは、Assembler サービスに渡される DDX ドキュメント内で参照されます。次の図に示すように、Assembler サービスを使用して、これらすべての XDP フラグメントを単一の XDP ドキュメントに組み合わせることができます。

![am_am_formd](assets/am_am_formd.png)

次の DDX ドキュメントは、複数の XDP フラグメントを単一の XDP ドキュメントにアセンブルします。

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

DDX ドキュメントには、結果の名前を指定する XDP `result` タグが含まれています。この場合、値は `tuc018result.xdp` です。この値は、Assembler サービスが結果を返した後に XDP ドキュメントを取得するために使用されるアプリケーションロジックで参照されます。例えば、アセンブルされた XDP ドキュメントを取得するために使用される次の Java アプリケーションロジックについて考えてみます（値が太字で示されています）。

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

`XDP source` タグは、完全な XDP ドキュメント（XDP フラグメントを追加するためのコンテナとして使用したり、順番に追加される多数のドキュメントの 1 つとして使用したりできる）を表す XDP ファイルを指定します。この場合、XDP ドキュメントはコンテナ（*複数の XDP フラグメントのアセンブル*&#x200B;に示した最初の図）としてのみ使用されます。つまり、他の XDP ファイルは XDP コンテナ内に配置されます。

サブフォームごとに、 `XDPContent` 要素（この要素はオプションです）を追加できます。 上記の例では、`subPatientContact`、`subPatientPhysical`、`subPatientHealth` の 3 つのサブフォームがあることに注意してください。両方の `subPatientPhysical` サブフォームおよび `subPatientHealth` サブフォームは、同じ XDP ファイル（tuc018_patient.xdp）に存在します。 fragment 要素は、Designer で定義されたサブフォームの名前を指定します。

>[!NOTE]
>
>Assembler サービスについて詳しくは、[AEM Forms サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

>[!NOTE]
>
>DDX ドキュメントについて詳しくは、[Assembler サービスと DDX リファレンス](https://www.adobe.com/go/learn_aemforms_ddx_63)を参照してください。

## 手順の概要 {#summary-of-steps}

複数の XDP フラグメントをアセンブルするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. PDF Assembler クライアントを作成します。
1. 既存の DDX ドキュメントを参照します。
1. XDP ドキュメントを参照します。
1. 実行時オプションを設定します。
1. 複数の XDP ドキュメントをアセンブリします。
1. アセンブルされた XDP ドキュメントを取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar（AEM Forms が JBoss にデプロイされている場合に必要）
* jbossall-client.jar（AEM Formsが JBoss にデプロイされている場合に必要）

**PDF Assembler クライアントの作成**

Assembler 操作をプログラムで実行する前に、Assembler サービスクライアントを作成します。

**既存の DDX ドキュメントの参照**

複数の XDP ドキュメントをアセンブルするには、DDX ドキュメントを参照する必要があります。この DDX ドキュメントには、`XDP result`、`XDP source`、`XDPContent` 要素を含める必要があります。

**XDP ドキュメントの参照**

複数の XDP ドキュメントをアセンブルするには、結果の XDP ドキュメントをアセンブルするために使用されるすべての XDP ファイルを参照します。`source` 属性によって参照される XDP ドキュメントに含まれるサブフォームの名前が、`fragment` 属性で指定されていることを確認してください。サブフォームは Designer で定義されます。 例えば、次のような XML を考えてみましょう。

```xml
 <XDPContent insertionPoint="ddx_fragment" source="tuc018_contact.xdp" fragment="subPatientContact" required="false"/>
```

*subPatientContact* という名前のサブフォームは、 *tuc018_contact.xdp* という名前の XDP ファイル内にある必要があります。

**実行時オプションの設定**

ジョブを実行する際の Assembler サービスの動作を制御する実行時オプションを設定できます。例えば、エラーが発生した場合にジョブの処理を続行するよう Assembler サービスに指示するオプションを設定できます。

**複数の XDP ドキュメントのアセンブリ**

複数の XDP ファイルをアセンブリするには、 `invokeDDX` 操作を呼び出します。 Assembler サービスは、コレクションオブジェクト内でアセンブルされた XDP ドキュメントを返します。

**アセンブルされた XDP ドキュメントの取得**

アセンブルされた XDP ドキュメントがコレクションオブジェクト内で返されます。コレクションオブジェクトを繰り返し処理し、XDP ドキュメントを XDP ファイルとして保存します。また、XDP ドキュメントを別の AEM Forms サービス（Output など）に渡すこともできます。

**関連トピック**

[Java API を使用した複数の XDP フラグメントのアセンブル](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-java-api)

[Web サービス API を使用した複数の XDP フラグメントのアセンブル](assembling-multiple-xdp-fragments.md#assemble-multiple-xdp-fragments-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDF ドキュメントをプログラムで組み立てる](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)

[フラグメントを使用した PDF ドキュメントの作成](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments)

## Java API を使用した複数の XDP フラグメントのアセンブル {#assemble-multiple-xdp-fragments-using-the-java-api}

Assembler Service API（Java）を使用して、複数の XDP フラグメントをアセンブルします。

1. プロジェクトファイルを含めます。

   adobe-livecycle-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. PDF Assembler クライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して、`ServiceClientFactory` オブジェクトを渡すことで、`AssemblerServiceClient` オブジェクトを作成します。

1. 既存の DDX ドキュメントを参照します。

   * コンストラクターを使用して、DDX ファイルの場所を指定する文字列値を渡すことで、DDXドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクターを使用して `java.io.FileInputStream` オブジェクトを渡すことによって、`com.adobe.idp.Document` オブジェクトを作成します。

1. XDP ドキュメントを参照します。

   * `HashMap` コンストラクターを使用することで、入力 XDP ドキュメントを格納するために使用される `java.util.Map` オブジェクトを作成します。
   * `com.adobe.idp.Document` オブジェクトを作成して、入力 XDP ファイルを含む `java.io.FileInputStream` オブジェクトを渡します（XDP ファイルごとにこのタスクを繰り返します）。
   * `put` メソッドを呼び出して次の引数を渡すことで、エントリを `java.util.Map` オブジェクトに追加します。

      * キー名を表す文字列値。この値は、DDX ドキュメントで指定された `source` 要素値に一致する必要があります（XDP ファイルごとにこのタスクを繰り返します）。
      * `source` 要素に対応する XDP ドキュメントを含む `com.adobe.idp.Document` オブジェクト（XDP ファイルごとにこのタスクを繰り返します）。

1. 実行時オプションを設定します。

   * コンストラクターを使用して、実行時オプションを格納する `AssemblerOptionSpec` オブジェクトを作成します。
   * `AssemblerOptionSpec` オブジェクトに属するメソッドを呼び出して、ビジネス要件を満たすように実行時オプションを設定します。例えば、エラーが発生したときにジョブの処理を続行するように Assembler サービスに指示するには、`AssemblerOptionSpec` オブジェクトの `setFailOnError` メソッドを呼び出して `false` を渡します。

1. 複数の XDP ドキュメントをアセンブリします。

   `AssemblerServiceClient` オブジェクトの `invokeDDX` メソッドを呼び出して、以下の必須値を渡します。

   * 使用する DDX ドキュメントを表す `com.adobe.idp.Document` オブジェクト
   * 入力 XDP ファイルを格納する `java.util.Map` オブジェクト
   * デフォルトのフォントやジョブのログレベルを含む、実行時のオプションを指定する `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` オブジェクト

   `invokeDDX` メソッドは、作成された XDP ドキュメントを格納する `com.adobe.livecycle.assembler.client.AssemblerResult` オブジェクトを返します。

1. アセンブルされた XDP ドキュメントを取得します。

   作成された XDP ドキュメントを取得するには、以下の操作を実行します。

   * `AssemblerResult` オブジェクトの `getDocuments` メソッドを呼び出します。 このメソッドは、 `java.util.Map` オブジェクトを返します。
   * 結果の `com.adobe.idp.Document` オブジェクトが見つかるまで `java.util.Map` オブジェクトを反復処理します。
   * `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを呼び出して、作成された XDP ドキュメントを抽出します。

**関連トピック**

[複数の XDP フラグメントの作成](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)
[クイックスタート（SOAP モード）：Java API を使用した複数の XDP フラグメントの作成](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-multiple-xdp-fragments-using-the-java-api)
[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Web サービス API を使用した複数の XDP フラグメントのアセンブル {#assemble-multiple-xdp-fragments-using-the-web-service-api}

Assembler Service API（web サービス）を使用して、複数の XDP フラグメントを作成します。

1. プロジェクトファイルを含めます。

   MTOM を使用する Microsoft .NET プロジェクトを作成します。サービス参照を設定する際は、以下の WSDL 定義を必ず使用してください。

   ```java
    https://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1.
   ```

   >[!NOTE]
   >
   >`localhost` を、AEM Forms をホストするサーバーの IP アドレスに置換します。

1. PDF Assembler クライアントを作成します。

   * デフォルトのコンストラクターを使用して `AssemblerServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して `AssemblerServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を指定する文字列値（例：`https://localhost:8080/soap/services/AssemblerService?blob=mtom`）を AEM Forms サービスに渡します。`lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。
   * `AssemblerServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` フィールドを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `AssemblerServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms のユーザー名を割り当てます。
      * `AssemblerServiceClient.ClientCredentials.UserName.Password` フィールドに対応するパスワード値を割り当てます。
      * `BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに `HttpClientCredentialType.Basic` 定数値を割り当てます。
      * `BasicHttpBindingSecurity.Security.Mode` フィールドに `BasicHttpSecurityMode.TransportCredentialOnly` 定数値を割り当てます。

1. 既存の DDX ドキュメントを参照します。

   * コンストラクターを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、DDX ドキュメントを格納するために使用されます。
   * コンストラクターを呼び出し、DDX ドキュメントのファイルの場所とファイルを開くモードを表す文字列値を渡して、`System.IO.FileStream` オブジェクトを作成します。
   * `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティを取得して決定します。
   * `System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出して、バイト配列にストリームデータを入力します。読み取り対象のバイト配列、開始位置、ストリーム長を渡します。
   * `MTOM` プロパティにバイト配列の内容を割り当てて、`BLOB` オブジェクトに入力します。

1. XDP ドキュメントを参照します。

   * 入力 XDP ファイルごとに、コンストラクタ―を使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、入力ファイルを格納するために使用されます。
   * コンストラクターを呼び出し、入力ファイルのファイルの場所とファイルを開くモードを表す文字列値を渡すことによって、`System.IO.FileStream` オブジェクトを作成します。
   *  `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティを取得して決定します。
   * `System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出して、バイト配列にストリームデータを入力します。読み取り対象のバイト配列、開始位置、ストリーム長を渡します。
   * `MTOM` フィールドにバイト配列の内容を割り当てて、`BLOB` オブジェクトにデータを入力します。
   * `MyMapOf_xsd_string_To_xsd_anyType` オブジェクトを作成します。このコレクションオブジェクトは、XDP ドキュメントの作成に必要な入力ファイルを格納するために使用されます。
   * 入力ファイルごとに、`MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトを作成します。
   * `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトの `key` フィールドにキー名を表す文字列値を入力します。この値は、DDX ドキュメントで指定された要素の値と一致する必要があります（このタスクは入力 XDP ファイルごとに実行します）。
   * 入力ファイルを格納する `BLOB` オブジェクトを `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトの `value` フィールドに割り当てます（このタスクは入力 XDP ファイルごとに実行します）。
   * `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトを `MyMapOf_xsd_string_To_xsd_anyType` オブジェクトに追加します。`MyMapOf_xsd_string_To_xsd_anyType` オブジェクトの `Add` メソッドを呼び出し、`MyMapOf_xsd_string_To_xsd_anyType` オブジェクトを渡します（このタスクは入力 XDP ドキュメントごとに実行します）。

1. 実行時オプションを設定します。

   * コンストラクターを使用して、実行時オプションを格納する `AssemblerOptionSpec` オブジェクトを作成します。
   * `AssemblerOptionSpec` オブジェクトに属するデータメンバーに値を割り当てて、ビジネス要件を満たすように実行時オプションを設定します。例えば、エラーが発生した場合にジョブの処理を続行するように Assembler サービスに指示するには、 `false` を `AssemblerOptionSpec` オブジェクトの `failOnError` データメンバーに割り当てます。

1. 複数の XDP ドキュメントをアセンブリします。

   `AssemblerServiceClient` オブジェクトの `invokeDDX` メソッドを呼び出して、以下の値を渡します。

   * DDX ドキュメントを表す `BLOB` オブジェクト
   * 必須ファイルを含む `MyMapOf_xsd_string_To_xsd_anyType` オブジェクト
   * 実行時オプションを指定する `AssemblerOptionSpec` オブジェクト

   `invokeDDX` メソッドは、ジョブの結果と例外（発生した場合）を含む `AssemblerResult` オブジェクトを返します。

1. アセンブルされた XDP ドキュメントを取得します。

   新しく作成した XDP ドキュメントを取得するには、次の操作を実行します。

   * `AssemblerResult` オブジェクトの `documents` フィールドにアクセスします。これは、結果の PDF ドキュメントを格納する `Map` オブジェクトです。
   * `Map` オブジェクトを反復処理して各結果ドキュメントを取得します。次に、その配列メンバーの `value` を `BLOB` にキャストします。
   * `BLOB` オブジェクトの `MTOM` プロパティにアクセスして、PDF ドキュメントを表すバイナリデータを抽出します。XDP ファイルに書き出すことができるバイトの配列を返します。

**関連トピック**

[複数の XDP フラグメントの作成](assembling-multiple-xdp-fragments.md#assembling-multiple-xdp-fragments)
[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
