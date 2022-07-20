---
title: PDF ポートフォリオのアセンブリ
seo-title: Assembling PDF Portfolios
description: PDF ポートフォリオをアセンブリして、Word ファイル、画像ファイル、PDF ドキュメントなど、様々なタイプの複数のドキュメントを組み合わせます。Java API と web サービス API を使用して、PDF ポートフォリオをアセンブリできます。
seo-description: Assemble a PDF portfolio to combine several documents of various types, including word file, image files, and PDF documents. You can assemble a PDF portfolio using a Java API and a Web Service API.
uuid: 1778c90b-9d26-466b-a7c7-401d737395e0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 023f0d9e-bfde-4879-a839-085fadffb48e
role: Developer
exl-id: d2bd7c3e-4f75-4234-a7aa-ee8524430493
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '1828'
ht-degree: 100%

---

# PDF ポートフォリオのアセンブリ {#assembling-pdf-portfolios}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

Assembler Java および web サービス API を使用して、PDF ポートフォリオをアセンブリできます。ポートフォリオは、word ファイル、画像ファイル（例えば、jpeg ファイル）、PDF ドキュメントなど、様々なタイプの複数のドキュメントを組み合わせることができます。ポートフォリオのレイアウトは、*プレビュー付きグリッド*、*画像上で*&#x200B;レイアウト、または&#x200B;*回転*&#x200B;など、様々なスタイルに設定できます。

次のイラストは、*画像上で*&#x200B;スタイルレイアウトが示されたポートフォリオのスクリーンショットです。

![ap_ap_portfolio](assets/ap_ap_portfolio.png)

PDF ポートフォリオを作成することで、ドキュメントをまとめて渡す代わりにペーパーレス化を実現できます。AEM Forms を使用して、構造化 DDX ドキュメントで Assembler サービスを呼び出すことにより、ポートフォリオを作成できます。次の DDX ドキュメントは、PDF ポートフォリオを作成する DDX ドキュメントの例です。

```xml
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     <PDF result="portfolio1.pdf">
         <Portfolio>
             <Navigator source="myNavigator">
                 <Resource name="navigator/image.xxx" source="myImage.png"/>
             </Navigator>
         </Portfolio>
         <PackageFiles source="dog1"  >
              <FieldData name="X">72</FieldData>
             <FieldData name="Y">72</FieldData>
             <File filename="saint_bernard.jpg" mimetype="image/jpeg"/>
         </PackageFiles>
         <PackageFiles source="dog2"  >
             <FieldData name="X">120</FieldData>
             <FieldData name="Y">216</FieldData>
             <File filename="greyhound.pdf"/>
         </PackageFiles>
     </PDF>
 </DDX>
```

DXX ドキュメントには、 ネストされた `Navigator` タグが付いた `Portfolio` タグが含まれている必要があります。`<Resource name="navigator/image.xxx" source="myImage.png"/>` タグが必要となるのは、`myNavigator` が onImage レイアウトナビゲーターとして割り当てられている場合に限ります。`AdobeOnImage.nav`このタグを使用すると、Assembler サービスは、ポートフォリオの背景として使用する画像を選択できます。`PackageFiles`タグおよび `File` タグを含めることで、パッケージ化されたファイルのファイル名と MIME タイプを定義します。

>[!NOTE]
>
>Assembler サービスについて詳しくは、[AEM Forms サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

>[!NOTE]
>
>DDX ドキュメントについて詳しくは、[Assembler サービスと DDX リファレンス](https://www.adobe.com/go/learn_aemforms_ddx_63)を参照してください。

## 手順の概要 {#summary-of-steps}

PDF ポートフォリオを作成するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. PDF Assembler クライアントを作成します。
1. 既存の DDX ドキュメントを参照します。
1. 必要なドキュメントを参照します。
1. 実行時オプションを設定します。
1. ポートフォリオをアセンブリします。
1. アセンブリ済みのポートフォリオを保存します。

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

PDF ポートフォリオを組み立てるには、DDX ドキュメントを参照する必要があります。この DDX ドキュメントには `Portfolio` 要素、`Navigator` 要素および `PackageFiles` 要素を含める必要があります。

**必要なドキュメントの参照**

PDF ポートフォリオをアセンブリするには、アセンブリ対象のドキュメントを表すすべてのファイルを参照してください。例えば、DDX ドキュメントで指定されているすべての画像ファイルを Assembler サービスに渡します。次のファイルは、この節で指定した DDX ドキュメント内で参照されています。 *myImage.png* および *saint_bernard.jpg*。

PDF ポートフォリオをアセンブリする際に、NAV ファイル（ナビゲーターファイル）を Assembler サービスに渡してください。Assembler サービスに渡す NAV ファイルは、作成する PDF ポートフォリオの種類に応じて異なります。例えば、 *画像上* レイアウトを作成するには、 AdobeOnImage.nav ファイルを渡します。NAV ファイルは次のフォルダーにあります。

`<Install folder>\Acrobat 9.0\Acrobat\Navigators`

NAV ファイルを Acrobat 9（またはそれ以降）のインストールディレクトリからコピーします。NAV ファイルは、クライアントアプリケーションがアクセスできる場所に配置します。すべてのファイルは、Map コレクションオブジェクト内の Assembler サービスに渡されます。

>[!NOTE]
>
>PDF ポートフォリオのアセンブリに関連するクイックスタートでは、AdobeOnImage.nav を使用します。

**実行時オプションを設定**

ジョブを実行する際の Assembler サービスの動作を制御する実行時オプションを設定できます。例えば、エラーが発生した場合にジョブの処理を続行するよう Assembler サービスに指示するオプションを設定できます。

**ポートフォリオのアセンブリ**

PDF ポートフォリオをアセンブリするには、 `invokeDDX` 操作を呼び出します。Assembler サービスは、コレクションオブジェクト内の PDF ポートフォリオを返します。

**アセンブリされたポートフォリオの保存**

PDF ポートフォリオがコレクションオブジェクト内で返されます。コレクションオブジェクトを反復処理し、PDF ポートフォリオを PDF ファイルとして保存します。

**関連トピック**

[Java API を使用した PDF ポートフォリオのアセンブリ](#assemble-a-pdf-portfolio-using-the-java-api)

[Web サービス API を使用した PDF ポートフォリオのアセンブリ](#assemble-a-pdf-portfolio-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDF ドキュメントをプログラムで組み立てる](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java API を使用した PDF ポートフォリオのアセンブリ {#assemble-a-pdf-portfolio-using-the-java-api}

Assembler Service API（Java）を使用して PDF ポートフォリオをアセンブリします。

1. プロジェクトファイルを含めます。

   adobe-livecycle-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. PDF Assembler クライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して `ServiceClientFactory` オブジェクトを渡すことにより、`AssemblerServiceClient` オブジェクトを作成します。

1. 既存の DDX ドキュメントを参照します。

   * コンストラクタを使用し、DDX ファイルの場所を指定する文字列値を渡すことによって、その DDX ドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクターを使用して `java.io.FileInputStream` オブジェクトを渡すことによって、`com.adobe.idp.Document` オブジェクトを作成します。

1. 必要なドキュメントを参照します。

   * `HashMap` コンストラクターを使用することにより、入力 PDF ドキュメントの格納に使用する `java.util.Map` オブジェクトを作成します。
   * コンストラクターを使用して `java.io.FileInputStream` オブジェクトを作成します。必要な NAV ファイルの場所を渡します（ポートフォリオの作成に必要な各ファイルに対して、このタスクを繰り返します）。
   * `com.adobe.idp.Document` オブジェクトを作成して NAV ファイルを含む `java.io.FileInputStream` オブジェクトを渡してください（ポートフォリオの作成に必要なファイルごとに、このタスクを繰り返します）。
   * `put` メソッドを呼び出して次の引数を渡すことにより、`java.util.Map` オブジェクトにエントリを追加してください。

      * キー名を表す文字列値。この値は、DDX ドキュメントで指定されたソース要素の値と一致する必要があります。（ポートフォリオの作成に必要なファイルごとに、このタスクを繰り返します）。
      * PDF ドキュメントを含む `com.adobe.idp.Document` オブジェクト。（ポートフォリオの作成に必要なファイルごとに、このタスクを繰り返します）。

1. 実行時オプションを設定します。

   * コンストラクタを使用して、実行時オプションを格納する `AssemblerOptionSpec` オブジェクトを作成します。
   * `AssemblerOptionSpec` オブジェクトに属するメソッドを呼び出して、ビジネス要件を満たすよう実行時オプションを設定します。例えば、エラーが発生したときにジョブの処理を続行するように Assembler サービスに指示するには、`AssemblerOptionSpec` オブジェクトの `setFailOnError` メソッドを呼びだして `false` を渡します。

1. ポートフォリオをアセンブリします。

   `AssemblerServiceClient` オブジェクトの `invokeDDX` メソッドを呼び出して、以下の必須値を渡します。

   * 使用する DDX ドキュメントを表す `com.adobe.idp.Document` オブジェクト
   * PDF ポートフォリオの構築に必要なファイルを含む `java.util.Map` オブジェクト。
   * デフォルトのフォントやジョブログレベルなどの実行時オプションを指定する `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` オブジェクト

   `invokeDDX` メソッドは、 アセンブリ済みの PDF ポートフォリオと例外（発生した場合）を含む `com.adobe.livecycle.assembler.client.AssemblerResult` オブジェクトを返します。

1. アセンブリ済みのポートフォリオを保存します。

   PDF ポートフォリオを取得するには、次のアクションを実行します。

   * `AssemblerResult` オブジェクトの `getDocuments` メソッドを呼び出します。このメソッドは、`java.util.Map` オブジェクトを返します。
   * 結果の `com.adobe.idp.Document` オブジェクトが見つかるまで、`java.util.Map` オブジェクトを反復処理します。
   * `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを呼び出して、PDF ポートフォリオを抽出します。

**関連トピック**

[クイックスタート（SOAP モード）：Java API を使用した PDF ポートフォリオのアセンブリ](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-portfolios-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Web サービス API を使用した PDF ポートフォリオのアセンブリ {#assemble-a-pdf-portfolio-using-the-web-service-api}

Assembler サービス API（web サービス）を使用して PDF ポートフォリオをアセンブリします。

1. プロジェクトファイルを含めます。

   MTOM を使用する Microsoft .NET プロジェクトを作成します。サービスリファレンスを設定する際は、WSDL の定義 `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1` を必ず使用してください。 

   >[!NOTE]
   >
   >`localhost` を、AEM Forms をホストするサーバーの IP アドレスに置き換えます。

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
   * `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することでバイト配列のサイズを決定することができます。
   * `System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出して、バイト配列にストリームデータを入力します。読み取り対象のバイト配列、開始位置、ストリーム長を渡します。
   * `MTOM` プロパティにバイト配列の内容を割り当てることによって、`BLOB` オブジェクトに入力します。

1. 必要なドキュメントを参照します。

   * 入力ファイルごとに、コンストラクターを使用して `BLOB` オブジェクトを作成します。`BLOB` オブジェクトは、入力ファイルを保存するために使用されます。
   * コンストラクターを呼び出し、入力ファイルのファイルの場所とファイルを開くモードを表す文字列値を渡すことによって、`System.IO.FileStream` オブジェクトを作成します。
   *  `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することでバイト配列のサイズを決定することができます。
   * `System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出して、バイト配列にストリームデータを入力します。読み取り対象のバイト配列、開始位置、ストリーム長を渡します。
   * `MTOM` フィールドにバイト配列のコンテンツを割り当てて、`BLOB` オブジェクトを入力します。
   * `MyMapOf_xsd_string_To_xsd_anyType` オブジェクトを作成します。このコレクションオブジェクトは、PDF ポートフォリオの作成に必要な入力ファイルの格納に使用されます。
   * 入力ファイルごとに、 `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトを作成します。
   * `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトの `key` フィールドにキー名を表す文字列値を入力します。この値は、DDX ドキュメントで指定された要素の値と一致する必要があります（入力ファイルごとにこのタスクを実行します）。
   * 入力ファイルを格納する `BLOB` オブジェクトを `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトの `value` フィールドに割り当てます（入力 PDF ドキュメントごとにこのタスクを実行します）。
   * `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトを `MyMapOf_xsd_string_To_xsd_anyType` オブジェクトに追加します。`MyMapOf_xsd_string_To_xsd_anyType` オブジェクトの `Add` メソッドを呼び出し、`MyMapOf_xsd_string_To_xsd_anyType` オブジェクトを渡します。（入力 PDF ドキュメントごとにこのタスクを実行します）。

1. 実行時オプションを設定します。

   * ランタイムオプションを格納する `AssemblerOptionSpec` オブジェクトをコンストラクタで作成します。
   * `AssemblerOptionSpec` オブジェクトに属するデータメンバーに値を割り当てることで、ビジネス要件に応じたランタイムオプションを設定します。例えば、エラーが発生した場合にジョブの処理を続行するように Assembler サービスに指示するには、 `false` を `AssemblerOptionSpec` オブジェクトの `failOnError` データメンバーに割り当てます。

1. ポートフォリオをアセンブリします。

   `AssemblerServiceClient` オブジェクトの `invokeDDX` メソッドを呼び出して、次の値を渡します。

   * DDX ドキュメントを表す `BLOB` オブジェクト
   * 必要なファイルを含む `MyMapOf_xsd_string_To_xsd_anyType` オブジェクト
   * 実行時オプションを指定する `AssemblerOptionSpec` オブジェクト

   `invokeDDX` メソッドは、ジョブの結果と例外（発生した場合）を含む `AssemblerResult` オブジェクトを返します。

1. アセンブリ済みのポートフォリオを保存します。

   新しく作成された PDF ポートフォリオを取得するには、次のアクションを実行します。

   * `AssemblerResult` オブジェクトの `documents` フィールドにアクセスします。これは、結果の PDF ドキュメントを格納する `Map` オブジェクトです。
   * `Map` オブジェクトを反復処理して各結果ドキュメントを取得します。次に、その配列メンバーの`value`を`BLOB`にキャストします。
   * `BLOB`オブジェクトの`MTOM`プロパティにアクセスして、PDF ドキュメントを表すバイナリデータを抽出します。これにより、PDF ファイルに書き出すことができるバイト配列が返されます。

**関連トピック**

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
