---
title: ベイツナンバリングを使用したドキュメントのアセンブリ
seo-title: ベイツナンバリングを使用したドキュメントのアセンブリ
description: 'null'
seo-description: 'null'
uuid: 28d5faeb-6915-41a2-b6a0-78d255df024f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 77e9b895-1313-4a5b-a2d5-cdb65bdc1966
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1901'
ht-degree: 5%

---


# Assembling Documents Using Bates Numbering {#assembling-documents-using-bates-numbering}

ベイツナンバリングを使用して、一意のページ識別子を含むPDFドキュメントをアセンブリできます。 *ベイツナンバリング* ：関連するドキュメントのバッチに一意の識別子を適用する方法です。 ドキュメント内の各ページ(またはドキュメントのセット)に、ページを一意に識別するベイツ番号が割り当てられます。 例えば、原材料情報を含む、1 つの組立部品の製造に関する生産ドキュメントに、1 つの識別子が割り当てられます。ベイツナンバリングの数値は連続した増分値で、オプションでプレフィックスやサフィックスが付きます。プリフィックス+数値+サフィックスは、ベイツ *パターンと呼ばれ*&#x200B;ます。

次の例は、ドキュメントのヘッダに一意の識別子を含む PDF ドキュメントを示しています。

![au_au_batesnumber](assets/au_au_batesnumber.png)

この説明のため、一意のページ識別子はドキュメントのヘッダーに配置されます。 次のDDXドキュメントが使用されているとします。

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

このDDXドキュメントは、 *map.pdf* および ** directions.pdfという2つのPDFドキュメントを1つのPDFドキュメントにマージします。 結果のPDFドキュメントには、一意のページ識別子で構成されるヘッダーが含まれます。 例えば、上の図のドキュメントは000016と表示されています。

>[!NOTE]
>
>この節を読む前に、Assemblerサービスを使用したPDFドキュメントのアセンブリについて理解しておくことをお勧めします。 ここでは、入力ドキュメントを含むコレクションオブジェクトの作成、返されるコレクションオブジェクトからの結果の抽出などの概念については説明しません。 (「 [プログラムによるPDFドキュメントのアセンブリ](/help/forms/developing/programmatically-assembling-pdf-documents.md)」を参照)。

>[!NOTE]
>
>For more information about the Assembler service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>DDXドキュメントについて詳しくは、『 [Assembler Service and DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63)』を参照してください。

## 手順の概要 {#summary-of-steps}

一意のページ識別子（ベイツナンバリング）を含むPDFドキュメントをアセンブリするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. PDFアセンブラクライアントを作成します。
1. 既存のDDXドキュメントの参照。
1. 入力PDFドキュメントを参照します。
1. ベイツナンバリングの初期値を設定します。
1. 入力PDFドキュメントをアセンブリします。
1. 結果を抽出します。

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

PDFドキュメントをアセンブリするには、DDXドキュメントを参照する必要があります。 例えば、この節で紹介したDDXドキュメントについて考えてみましょう。 一意のページ識別子を含むPDFドキュメントをアセンブリするには、DDXドキュメントにその `BatesNumber` 要素を含める必要があります。

**参照入力PDFドキュメント**

PDFドキュメントをアセンブリするには、入力PDFドキュメントを参照する必要があります。 例えば、map.pdfおよびdirections.pdfドキュメントを参照して、これらのPDFドキュメントを1つのPDFドキュメントにアセンブリする必要があります。

**ベイツナンバリングの初期値を設定する**

ビジネス要件に合わせて、ベイツナンバリングの初期値を設定できます。 例えば、初期値を000100に設定する必要があるとします。 初期値を設定しない場合、最初のページの値は000000です。

**入力PDFドキュメントのアセンブリ**

Assemblerサービスクライアントの作成後、 `BatesNumber``invokeDDX` 要素ドキュメントを含むDDXドキュメントの参照、入力PDF情報の参照、実行時オプションの設定を行うと、Assemblerサービスを呼び出して、一意のページIDを含むPDFドキュメントをアセンブリできます。

**結果の抽出**

Assemblerサービスは、ジョブ結果を含むコレクションオブジェクトを返します。 結果のPDFドキュメントと、スローされた例外を抽出できます。 この場合、暗号化されたPDFドキュメントはコレクションオブジェクト内に配置されます。

>[!NOTE]
>
>操作を呼び出すと、コレクションオブジェクトが返され `invokeDDX` ます。 この操作は、2つ以上の入力PDFドキュメントをAssemblerサービスに渡す場合に使用されます。 ただし、1つの入力PDFドキュメントのみをAssemblerサービスに渡す場合は、この `invokeOneDocument` 操作を呼び出す必要があります。 この操作の使用について詳しくは、暗号化されたPDFドキュメントの [アセンブリを参照してください](/help/forms/developing/assembling-encrypted-pdf-documents.md)。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[プログラムによるPDFドキュメントのアセンブリ](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java APIを使用したベイツナンバリングを使用したドキュメントのアセンブリ {#assemble-documents-with-bates-numbering-using-the-java-api}

Assembler Service API(Java)を使用して、一意のページ識別子（ベイツナンバリング）を使用するPDFドキュメントをアセンブリします。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-assembler-client.jarなどのクライアントJARファイルを含めます。

1. PDFアセンブラクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `AssemblerServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. 既存のDDXドキュメントの参照。

   * コンストラクターを使用し、DDXファイルの場所を指定する文字列値を渡して、DDXドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 入力PDFドキュメントを参照します。

   * コンストラクターを使用して、入力PDFドキュメントの格納に使用する `java.util.Map` オブジェクトを作成し `HashMap` ます。
   * 各入力PDFドキュメントに対して、コンストラクターを使用し、入力PDFドキュメントの場所を渡して、 `java.io.FileInputStream` オブジェクトを作成します。 この場合、保護されていないPDFドキュメントの場所を渡します。
   * 各入力PDFドキュメントに対して、 `com.adobe.idp.Document` オブジェクトを作成し、PDFドキュメントを含む `java.io.FileInputStream` オブジェクトを渡します。
   * メソッド追加を呼び出し、次の引数を渡すことによって、オブジェクトに対するエントリを作成します。 `java.util.Map``put`

      * キー名を表すstring値です。 この値は、DDXドキュメントで指定されたPDFソース要素の値と一致する必要があります。 例えば、この節で紹介するDDXドキュメントで指定されているPDFソースファイルの名前はLoan.pdfです。
      * 保護されていないPDFドキュメントを含む `com.adobe.idp.Document` オブジェクトです。

1. ベイツナンバリングの初期値を設定します。

   * コンストラクターを使用して、実行時のオプションを格納する `AssemblerOptionSpec` オブジェクトを作成します。
   * オブジェクトを呼び出し、初期値を指定する数値を渡すことで、 `AssemblerOptionSpec` 初期ベイツ数 `setFirstBatesNumber` を設定します。

1. 入力PDFドキュメントをアセンブリします。

   オブジェクトの `AssemblerServiceClient``invokeDDX` メソッドを呼び出し、次の必須値を渡します。

   * DDXドキュメントを表す `com.adobe.idp.Document` オブジェクトです。
   * 入力の保護されていないPDFファイルを含む `java.util.Map` オブジェクトです。
   * デフォルトのフォントやジョブログレベルなど、実行時のオプションを指定する `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` オブジェクト。

   パスワードで暗号化されたPDFドキュメントを含む `invokeDDX``com.adobe.livecycle.assembler.client.AssemblerResult` オブジェクトを返します。

1. 結果を抽出します。

   新しく作成されたPDFドキュメントを取得するには、次の操作を実行します。

   * オブジェクトの `AssemblerResult` メソッドを呼び出し `getDocuments` ます。 このアクションは、 `java.util.Map` オブジェクトを返します。
   * オブジェクトが見つかるまで、 `java.util.Map` オブジェクトを繰り返し処理 `com.adobe.idp.Document` します。
   * オブジェクトの `com.adobe.idp.Document``copyToFile` メソッドを呼び出してPDFドキュメントを抽出します。

**関連トピック**

[クイック開始（SOAPモード）: Java APIを使用したベイトナンバリングによるPDFドキュメントのアセンブリ](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-with-bates-numbering-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## WebサービスAPIを使用してベイツナンバリングを使用してドキュメントをアセンブルする {#assemble-documents-with-bates-numbering-using-the-web-service-api}

Assembler Service API（Webサービス）を使用して、一意のページ識別子（ベイツナンバリング）を使用するPDFドキュメントをアセンブリします。

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
   * オブジェクトのメソッドを呼び出して、バイト配列にストリームデータ `System.IO.FileStream` を入力し `Read` ます。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * オブジェクトにバイト配列の内容を割り当てて、 `BLOB` オブジェクト `MTOM` を入力します。

1. 入力PDFドキュメントを参照します。

   * 入力PDFドキュメントごとに、コンストラクターを使用して `BLOB` オブジェクトを作成します。 この `BLOB` オブジェクトは、入力PDFドキュメントの保存に使用されます。
   * Create a `System.IO.FileStream` object by invoking its constructor. 入力PDFドキュメントーのファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
   * オブジェクトのメソッドを呼び出して、バイト配列にストリームデータ `System.IO.FileStream` を入力し `Read` ます。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * オブジェクトのプロパティにバイト配列の内容を割り当てて、 `BLOB``MTOM` オブジェクトを入力します。
   * Create a `MyMapOf_xsd_string_To_xsd_anyType` object. このコレクションオブジェクトは、入力PDFドキュメントの格納に使用されます。
   * 入力PDFドキュメントごとに、 `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトを作成します。 例えば、2つの入力PDFドキュメントを使用する場合は、2つの `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトを作成します。
   * キー名を表すstring値を `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトの `key` フィールドに割り当てます。 この値は、DDXドキュメントで指定されたPDFソース要素の値と一致する必要があります。 (このタスクは、入力PDFドキュメントごとに実行します)。
   * PDFドキュメントを保存している `BLOB` オブジェクトをオブジェクトのフィ `MyMapOf_xsd_string_To_xsd_anyType_Item` ー `value` ルドに割り当てます。 (このタスクは、入力PDFドキュメントごとに実行します)。
   * オ追加ブジェクトをオブジ `MyMapOf_xsd_string_To_xsd_anyType_Item``MyMapOf_xsd_string_To_xsd_anyType` ェクトに追加します。 Invoke the `MyMapOf_xsd_string_To_xsd_anyType` object&#39;s `Add` method and pass the `MyMapOf_xsd_string_To_xsd_anyType` object. (このタスクは、入力PDFドキュメントごとに実行します)。

1. ベイツナンバリングの初期値を設定します。

   * コンストラクターを使用して、実行時のオプションを格納する `AssemblerOptionSpec` オブジェクトを作成します。
   * オブジェクトに属する `firstBatesNumber` データメンバーに数値を割り当てて、初期のベイツ数を設定し `AssemblerOptionSpec` ます。

1. 入力PDFドキュメントをアセンブリします。

   オブジェクトの `AssemblerServiceClient``invoke` メソッドを呼び出し、次の値を渡します。

   * DDXドキュメントを表す `BLOB` オブジェクトです。
   * 入力PDFドキュメントを含む `MyMapOf_xsd_string_To_xsd_anyType` オブジェクトです。 このキーはPDFソースファイルの名前と一致する必要があり、その値はそれらのファイルに対応する `BLOB` オブジェクトである必要があります。
   * 実行時オプションを指定する `AssemblerOptionSpec` オブジェクトです。

   この `invoke` メソッドは、ジョブの結果と発生した例外を含む `AssemblerResult` オブジェクトを返します。

1. 結果を抽出します。

   新しく作成されたPDFドキュメントを取得するには、次の操作を実行します。

   * オブジェクトのフ `AssemblerResult` ィールドにアクセスします。この `documents` フィールドは、結果のPDFドキュメントを含む `Map` オブジェクトです。
   * 結果のドキュメントの名前と一致するキーが見つかるまで、 `Map` オブジェクトを繰り返し処理します。 次に、その配列メンバーのをにキャスト `value` し `BLOB`ます。
   * PDFドキュメントを表すバイナリデータを抽出するには、その `BLOB` オブジェクトの `MTOM` プロパティにアクセスします。 PDFファイルに書き出すことができるバイトの配列を返します。

**関連トピック**

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
