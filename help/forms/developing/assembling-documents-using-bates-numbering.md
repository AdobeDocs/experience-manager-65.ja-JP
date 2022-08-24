---
title: 通し番号を使用したドキュメントのアセンブリ
seo-title: Assembling Documents Using Bates Numbering
description: '通し番号を使用して、Java および web サービス API を使用して PDF ドキュメントをアセンブリします。 '
seo-description: Use Bates numbering to assemble PDF documents using the Java and Web Service API.
uuid: 28d5faeb-6915-41a2-b6a0-78d255df024f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 77e9b895-1313-4a5b-a2d5-cdb65bdc1966
role: Developer
exl-id: 2a4e21c4-f2f5-44cd-b8ed-7b572782a2f1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1922'
ht-degree: 100%

---

# 通し番号を使用したドキュメントのアセンブリ {#assembling-documents-using-bates-numbering}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

通し番号を使用すると、個別ページの ID を含む PDF ドキュメントをアセンブリすることができます。*通し番号*&#x200B;は、関連するドキュメントのバッチに一意の ID を適用する方法です。ドキュメント内の各ページ（またはドキュメントのセット）に、ページを一意に識別する通し番号が割り当てられます。例えば、原材料情報を含む、1 つの組立部品の製造に関する生産ドキュメントに、1 つの識別子が割り当てられます。ベイツナンバリングの数値は連続した増分値で、オプションでプレフィックスやサフィックスが付きます。プレフィックス + 数値 + サフィックスは&#x200B;*通し番号パターン*&#x200B;と言われます。

次のイラストは、ドキュメントのヘッダーに一意の ID を含む PDF ドキュメントを示しています。

![au_au_batesnumber](assets/au_au_batesnumber.png)

このディスカッションの目的として、個別ページの ID がドキュメントのヘッダーに配置されます。 次の DDX ドキュメントが使用されているとします。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
        <PDF result="out.pdf">
        <Header>
         <Center>
             <StyledText>
                 <p font-size="20pt"><BatesNumber/></p>
             </StyledText>
         </Center>
     </Header>
           <PDF source="map.pdf" />
          <PDF source="directions.pdf" />
          </PDF>
 </DDX>
```

この DDX ドキュメントは *map.pdf* および *directions.pdf* という名前が付いた 2 つの PDF ドキュメントを単一の PDF ドキュメントに結合します。結果の PDF ドキュメントには、個別のページの ID で構成されるヘッダーが含まれます。例えば、上のイラストのドキュメントは 000016 です。

>[!NOTE]
>
>このセクションを読む前に、Assembler サービスを使用した PDF ドキュメントのアセンブリに関する知識を身に付けておくことをお勧めします。 この節では、入力ドキュメントを含むコレクションオブジェクトの作成や、返されたコレクションオブジェクトからの結果の抽出など、概念については説明しません（[プログラムによる PDF ドキュメントのアセンブリ](/help/forms/developing/programmatically-assembling-pdf-documents.md)を参照）。

>[!NOTE]
>
>Assembler サービスについて詳しくは、[AEM Formsサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

>[!NOTE]
>
>DDX ドキュメントについて詳しくは、[Assembler サービスと DDX リファレンス](https://www.adobe.com/go/learn_aemforms_ddx_63)を参照してください。

## 手順の概要 {#summary-of-steps}

個別ページの ID（通し番号の追加）を含む PDF ドキュメントをアセンブリするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. PDF Assembler クライアントを作成します。
1. 既存の DDX ドキュメントを参照します。
1. 入力 PDF ドキュメントを参照します。
1. ベイツ番号の初期値を設定します。
1. 入力 PDF ドキュメントをアセンブリします。
1. 結果を抽出します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar（AEM Forms が JBoss にデプロイされている場合に必要）
* jbossall-client.jar（AEM Formsが JBoss にデプロイされている場合に必要）

AEM Forms が JBoss 以外のサポート対象の J2EE アプリケーションサーバーにデプロイされている場合は、adobe-utilities.jar ファイルと jbossall-client.jar ファイルを、AEM Forms がデプロイされている J2EE アプリケーションサーバーに固有の JAR ファイルに置き換える必要があります。すべての AEM Forms JAR ファイルの場所については、[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。

**PDF Assembler クライアントの作成**

Assembler 操作をプログラムで実行する前に、Assembler サービスクライアントを作成する必要があります。

**既存の DDX ドキュメントの参照**

DDX ドキュメントを参照して、PDF ドキュメントをアセンブリする必要があります。例えば、このセクションで紹介した DDX ドキュメントについて考えてみましょう。 個別ページの ID を含む PDF ドキュメントをアセンブリするには、DDX ドキュメントに `BatesNumber` 要素を含める必要があります。

**参照入力 PDF ドキュメント**

入力 PDF ドキュメントを参照して、PDF ドキュメントをアセンブリする必要があります。例えば、map.pdf ドキュメントと directions.pdf ドキュメントを参照して、これらの PDF ドキュメントを 1 つの PDF ドキュメントにアセンブリする必要があります。

**初期通し番号値を設定**

ビジネス要件に合わせて、初期通し番号値を設定できます。例えば、初期値を 000100 に設定する必要があるとします。初期値を設定しない場合、最初のページの値は 000000 になります。

**入力 PDF ドキュメントのアセンブリ**

Assembler サービスクライアントを作成したら、`BatesNumber` 要素情報を含む DDX ドキュメントを参照し、入力 PDF ドキュメントを参照し、実行時オプションを設定すると、`invokeDDX` 操作を呼び出して、Assembler サービスが一意のページ ID を含む PDF ドキュメントをアセンブリすることができます。

**結果を抽出**

Assembler サービスは、ジョブの結果を含むコレクションオブジェクトを返します。結果の PDF ドキュメントと、例外が投げられた場合はそれを抽出できます。この場合、暗号化された PDF ドキュメントは、コレクションオブジェクト内に配置されます。

>[!NOTE]
>
>コレクションオブジェクトが返されるのは、`invokeDDX` 操作を呼び出した場合です。この操作は、2 つ以上の入力 PDF ドキュメントを Assembler サービスに渡す場合に使用します。ただし、1 つの入力 PDFドキュメントのみを Assembler サービスに渡す場合は、`invokeOneDocument` 操作を呼び出す必要があります。この操作の使用方法については、[暗号化された PDF ドキュメントのアセンブリ](/help/forms/developing/assembling-encrypted-pdf-documents.md)を参照してください。

**関連情報**

[AEM Forms Java ライブラリファイルの組み込み](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDF ドキュメントをプログラムで組み立てる](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java API を使用して通し番号のあるドキュメントをアセンブリ {#assemble-documents-with-bates-numbering-using-the-java-api}

Assembler サービス API（Java）を使用して、一意のページ ID（通し番号）を使用する PDFドキュメントをアセンブリします。

1. プロジェクトファイルを含めます。

   adobe-livecycle-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. PDF Assembler クライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して `ServiceClientFactory` オブジェクトを渡すことにより、`AssemblerServiceClient` オブジェクトを作成します。

1. 既存の DDX ドキュメントを参照します。

   * コンストラクタを使用し、DDX ファイルの場所を指定する文字列値を渡すことによって、その DDX ドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクターを使用して `java.io.FileInputStream` オブジェクトを渡すことにより、`com.adobe.idp.Document` オブジェクトを作成します。

1. 入力 PDF ドキュメントを参照します。

   * `HashMap` コンストラクターを使用して、入力 PDF ドキュメントを格納するために使用する `java.util.Map` オブジェクトを作成します。
   * 入力 PDF ドキュメントごとに、コンストラクターを使用して入力 PDF ドキュメントの場所を渡すことにより、`java.io.FileInputStream` オブジェクトを作成します。この場合は、安全でない PDF ドキュメントの場所が渡されます。
   * 入力 PDF ドキュメントごとに、`com.adobe.idp.Document` オブジェクトを作成して PDF ドキュメントを含んだ `java.io.FileInputStream` オブジェクトを渡します。
   * `java.util.Map` オブジェクトにエントリを追加するには、`put` メソッドを呼び出して、以下の引数を渡します。

      * キー名を表す文字列値。この値は、DDX ドキュメントで指定された PDF ソース要素の値と一致する必要があります例えば、この節で紹介する DDX ドキュメントで指定された PDF ソースファイルの名前は Loan.pdf です。
      * 安全でない PDF ドキュメントを含んだ `com.adobe.idp.Document` オブジェクト

1. ベイツ番号の初期値を設定します。

   * コンストラクターを使用して、実行時オプションを格納する `AssemblerOptionSpec` オブジェクトを作成します。
   * `AssemblerOptionSpec` オブジェクトの `setFirstBatesNumber` を呼び出し、初期値を指定する数値を渡すことで、ベイツ番号の初期値を設定します。

1. 入力 PDF ドキュメントをアセンブリします。

   `AssemblerServiceClient` オブジェクトの `invokeDDX` メソッドを呼び出して、以下の必須の値を渡します。

   * DDX ドキュメントを表す `com.adobe.idp.Document` オブジェクト
   * 安全でない入力 PDF ファイルを含んだ `java.util.Map` オブジェクト
   * デフォルトのフォントやジョブログレベルなどの実行時オプションを指定する `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` オブジェクト

   `invokeDDX` メソッドは、パスワードで暗号化された PDF ドキュメントを含んだ `com.adobe.livecycle.assembler.client.AssemblerResult` オブジェクトを返します。

1. 結果を抽出します。

   新しく作成した PDF ドキュメントを取得するには、次のアクションを実行します。

   * `AssemblerResult` オブジェクトの `getDocuments` メソッドを呼び出します。このアクションは `java.util.Map` オブジェクトを返します。
   * `com.adobe.idp.Document` オブジェクトが見つかるまで、`java.util.Map` オブジェクトを反復処理します。
   * `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを呼び出して、PDFドキュメントを抽出します。

**関連情報**

[クイックスタート（SOAP モード）：ベイツ番号を使用した PDF ドキュメントを、Java API を使用してアセンブリする](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-with-bates-numbering-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## ベイツ番号を使用したドキュメントを、web サービス API を使用してアセンブリする {#assemble-documents-with-bates-numbering-using-the-web-service-api}

Assembler サービス API（web サービス）を使用して、一意のページ識別子（ベイツ番号）を使用する PDF ドキュメントを組み立てます。

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

   * コンストラクターを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、DDX ドキュメントの保存に使用されます。
   * `System.IO.FileStream` オブジェクトを作成するには、そのコンストラクターを呼び出し、DDX ドキュメントのファイルの場所とファイルを開くモードを表す文字列値を渡します。
   * `System.IO.FileStream` オブジェクトのコンテンツを保存するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することでバイト配列のサイズを決定することができます。
   * `System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出して、バイト配列にストリームデータを入力します。読み取り対象のバイト配列、開始位置、ストリーム長を渡します。
   * `MTOM` フィールドにバイト配列の内容を割り当てることで、`BLOB` オブジェクトにデータを入力します。

1. 入力 PDF ドキュメントを参照します。

   * 入力 PDF ドキュメントごとに、コンストラクタを使用して、`BLOB` オブジェクトを作成します。`BLOB` オブジェクトは、入力 PDF ドキュメントを格納するために使用します。
   * コンストラクターを呼び出して `System.IO.FileStream` オブジェクトを作成します。入力 PDF ドキュメントのファイルの場所と、ファイルを開くモードを表す文字列値を渡します。
   * `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することでバイト配列のサイズを決定することができます。
   * `System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出して、バイト配列にストリームデータを入力します。読み取り対象のバイト配列、開始位置、ストリーム長を渡します。
   * `MTOM` プロパティにバイト配列の内容を割り当てることで、`BLOB` オブジェクトにデータを入力します。
   * `MyMapOf_xsd_string_To_xsd_anyType` オブジェクトを作成します。このコレクションオブジェクトは、入力 PDF ドキュメントを格納するために使用されます。
   * 入力 PDF ドキュメントごとに、`MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトを作成します。例えば、2 つの入力 PDF ドキュメントを使用する場合、`MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトを作成します。
   * キー名を表す文字列値を `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトの `key` フィールドに割り当てます。この値は、DDX ドキュメントで指定された PDF ソース要素の値と一致する必要があります（入力 PDF ドキュメントごとにこのタスクを実行します）。
   * PDF ドキュメントを格納する `BLOB` オブジェクトを `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトの `value` フィールドに割り当てます。（入力 PDF ドキュメントごとにこのタスクを実行します）。
   * `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトを `MyMapOf_xsd_string_To_xsd_anyType` オブジェクトに追加します。`MyMapOf_xsd_string_To_xsd_anyType` オブジェクトの `Add` メソッドを呼び出し、`MyMapOf_xsd_string_To_xsd_anyType` オブジェクトを渡します。（入力 PDF ドキュメントごとにこのタスクを実行します）。

1. ベイツ番号の初期値を設定します。

   * コンストラクターを使用して、実行時オプションを格納する `AssemblerOptionSpec` オブジェクトを作成します。
   * `AssemblerOptionSpec` オブジェクトに属する `firstBatesNumber` データメンバーに数値を割り当てて、ベイツ番号の初期値を設定します。

1. 入力 PDF ドキュメントをアセンブリします。

   `AssemblerServiceClient` オブジェクトの `invoke` メソッドを呼び出して、次の値を渡します。

   * DDX ドキュメントを表す `BLOB` オブジェクト。
   * 入力 PDF ドキュメントを格納する `MyMapOf_xsd_string_To_xsd_anyType` オブジェクト。キーは PDF ソースファイルの名前と一致する必要があり、値はこれらのファイルに対応する `BLOB` オブジェクトである必要があります。
   * 実行時オプションを指定する `AssemblerOptionSpec` オブジェクト。

   `invoke` メソッドは、ジョブの結果と例外（発生した場合）を含む `AssemblerResult` オブジェクトを返します。

1. 結果を抽出します。

   新しく作成した PDF ドキュメントを取得するには、次のアクションを実行します。

   * `AssemblerResult` オブジェクトの `documents` フィールドにアクセスし、結果の PDF ドキュメントを含む `Map` オブジェクトにアクセスします。
   * 結果のドキュメントの名前と一致するキーが見つかるまで、`Map` オブジェクトを繰り返し実行します。次に、その配列メンバーの `value` を `BLOB` にキャストします。
   * PDF ドキュメントを表すバイナリデータを、`BLOB` オブジェクトの `MTOM` プロパティにアクセスして抽出します 。これにより、PDF ファイルに書き出すことができるバイト配列が返されます。

**関連トピック**

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
