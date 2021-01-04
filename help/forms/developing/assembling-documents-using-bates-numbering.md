---
title: ベイツナンバリングを使用したドキュメントのアセンブリ
seo-title: ベイツナンバリングを使用したドキュメントのアセンブリ
description: 'ベイツナンバリングを使用して、JavaとWeb Service APIを使用してPDFドキュメントをアセンブリします。 '
seo-description: 'ベイツナンバリングを使用して、JavaとWeb Service APIを使用してPDFドキュメントをアセンブリします。 '
uuid: 28d5faeb-6915-41a2-b6a0-78d255df024f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 77e9b895-1313-4a5b-a2d5-cdb65bdc1966
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '1927'
ht-degree: 5%

---


# ベイツナンバリングを使用したドキュメントのアセンブリ{#assembling-documents-using-bates-numbering}

ベイツナンバリングを使用して、一意のページ識別子を含むPDFドキュメントをアセンブリできます。 *ベイツ* ナンバリングは、関連するドキュメントのバッチに固有の識別子を適用する方法です。ドキュメント内の各ページ(またはドキュメントのセット)に、ページを一意に識別するベイツ番号が割り当てられます。 例えば、原材料情報を含む、1 つの組立部品の製造に関する生産ドキュメントに、1 つの識別子が割り当てられます。ベイツナンバリングの数値は連続した増分値で、オプションでプレフィックスやサフィックスが付きます。プレフィックス+数値+サフィックスは、*ベイツパターン*&#x200B;と呼ばれます。

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

このDDXドキュメントは、*map.pdf*&#x200B;および&#x200B;*directions.pdf*&#x200B;という2つのPDFドキュメントを1つのPDFドキュメントにマージします。 結果のPDFドキュメントには、一意のページ識別子で構成されるヘッダーが含まれます。 例えば、上の図のドキュメントは000016と表示されています。

>[!NOTE]
>
>この節を読む前に、Assemblerサービスを使用したPDFドキュメントのアセンブリについて理解しておくことをお勧めします。 ここでは、入力ドキュメントを含むコレクションオブジェクトの作成、返されるコレクションオブジェクトからの結果の抽出などの概念については説明しません。 (「[PDFドキュメントのプログラムによるアセンブリ](/help/forms/developing/programmatically-assembling-pdf-documents.md)」を参照)。

>[!NOTE]
>
>Assemblerサービスについて詳しくは、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

>[!NOTE]
>
>DDXドキュメントについて詳しくは、「[Assembler Service and DDX Reference](https://www.adobe.com/go/learn_aemforms_ddx_63)」を参照してください。

## 手順{#summary-of-steps}の概要

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

AEM FormsがJBoss以外のサポート対象のJ2EEアプリケーションサーバーにデプロイされている場合は、adobe-utilities.jarファイルとjbossall-client.jarファイルを、AEM FormsがデプロイされているJ2EEアプリケーションサーバーに固有のJARファイルに置き換える必要があります。 すべてのAEM FormsJARファイルの場所については、「[AEM FormsJavaライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)」を参照してください。

**PDFアセンブラクライアントの作成**

プログラムによってAssembler操作を実行する前に、Assemblerサービスクライアントを作成する必要があります。

**既存のDDXドキュメントの参照**

PDFドキュメントをアセンブリするには、DDXドキュメントを参照する必要があります。 例えば、この節で紹介したDDXドキュメントについて考えてみましょう。 一意のページ識別子を含むPDFドキュメントをアセンブリするには、DDXドキュメントに`BatesNumber`要素を含める必要があります。

**参照入力PDFドキュメント**

PDFドキュメントをアセンブリするには、入力PDFドキュメントを参照する必要があります。 例えば、map.pdfおよびdirections.pdfドキュメントを参照して、これらのPDFドキュメントを1つのPDFドキュメントにアセンブリする必要があります。

**ベイツナンバリングの初期値を設定する**

ビジネス要件に合わせて、ベイツナンバリングの初期値を設定できます。 例えば、初期値を000100に設定する必要があるとします。 初期値を設定しない場合、最初のページの値は000000です。

**入力PDFドキュメントのアセンブリ**

Assemblerサービスクライアントの作成後、`BatesNumber`要素ドキュメントを含むDDXドキュメントの参照、入力PDF情報の参照、実行時オプションの設定を行った後、`invokeDDX`操作を呼び出すと、一意のページ識別子を含むPDFドキュメントをAssemblerサービスでアセンブリできます。

**結果の抽出**

Assemblerサービスは、ジョブ結果を含むコレクションオブジェクトを返します。 結果のPDFドキュメントと、スローされた例外を抽出できます。 この場合、暗号化されたPDFドキュメントはコレクションオブジェクト内に配置されます。

>[!NOTE]
>
>`invokeDDX`操作を呼び出すと、コレクションオブジェクトが返されます。 この操作は、2つ以上の入力PDFドキュメントをAssemblerサービスに渡す場合に使用されます。 ただし、1つの入力PDFドキュメントのみをAssemblerサービスに渡す場合は、`invokeOneDocument`操作を呼び出す必要があります。 この操作の使用について詳しくは、[暗号化されたPDFドキュメントのアセンブリ](/help/forms/developing/assembling-encrypted-pdf-documents.md)を参照してください。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[プログラムによるPDFドキュメントのアセンブリ](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java API {#assemble-documents-with-bates-numbering-using-the-java-api}を使用してベイツナンバリングを使用してドキュメントをアセンブル

Assembler Service API(Java)を使用して、一意のページ識別子（ベイツナンバリング）を使用するPDFドキュメントをアセンブリします。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-assembler-client.jarなどのクライアントJARファイルを含めます。

1. PDFアセンブラクライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用し、`AssemblerServiceClient`オブジェクトを渡して、`ServiceClientFactory`オブジェクトを作成します。

1. 既存のDDXドキュメントの参照。

   * コンストラクターを使用し、DDXファイルの場所を指定する文字列値を渡して、DDXドキュメントを表す`java.io.FileInputStream`オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 入力PDFドキュメントを参照します。

   * `java.util.Map`コンストラクターを使用して、入力PDFドキュメントの格納に使用する&lt;a0/>オブジェクトを作成します。`HashMap`
   * 各入力PDFドキュメントに対して、コンストラクターを使用し、入力PDFドキュメントーの場所を渡して、`java.io.FileInputStream`オブジェクトを作成します。 この場合、保護されていないPDFドキュメントの場所を渡します。
   * 入力PDFドキュメントごとに、`com.adobe.idp.Document`オブジェクトを作成し、PDFドキュメントを含む`java.io.FileInputStream`オブジェクトを渡します。
   * &lt;a0追加/>オブジェクトへのエントリ。その`java.util.Map`メソッドを呼び出し、次の引数を渡すことによって作成します。`put`

      * キー名を表すstring値です。 この値は、DDXドキュメントで指定されたPDFソース要素の値と一致する必要があります。 例えば、この節で紹介するDDXドキュメントで指定されているPDFソースファイルの名前はLoan.pdfです。
      * 保護されていないPDFドキュメントが含まれる`com.adobe.idp.Document`オブジェクトです。

1. ベイツナンバリングの初期値を設定します。

   * コンストラクターを使用して、実行時オプションを格納する`AssemblerOptionSpec`オブジェクトを作成します。
   * `AssemblerOptionSpec`オブジェクトの`setFirstBatesNumber`を呼び出し、初期値を指定する数値を渡して、初期ベイツ数を設定します。

1. 入力PDFドキュメントをアセンブリします。

   `AssemblerServiceClient`オブジェクトの`invokeDDX`メソッドを呼び出し、次の必須値を渡します。

   * DDXドキュメントを表す`com.adobe.idp.Document`オブジェクトです。
   * 保護されていない入力PDFファイルが含まれる`java.util.Map`オブジェクトです。
   * デフォルトのフォントとジョブログレベルを含む、実行時のオプションを指定する`com.adobe.livecycle.assembler.client.AssemblerOptionSpec`オブジェクト。

   `invokeDDX`メソッドは、パスワードで暗号化されたPDFドキュメントを含む`com.adobe.livecycle.assembler.client.AssemblerResult`オブジェクトを返します。

1. 結果を抽出します。

   新しく作成されたPDFドキュメントを取得するには、次の操作を実行します。

   * `AssemblerResult`オブジェクトの`getDocuments`メソッドを呼び出します。 このアクションは`java.util.Map`オブジェクトを返します。
   * `java.util.Map`オブジェクトを繰り返し処理して、`com.adobe.idp.Document`オブジェクトを見つけます。
   * `com.adobe.idp.Document`オブジェクトの`copyToFile`メソッドを呼び出してPDFドキュメントを抽出します。

**関連トピック**

[クイック開始（SOAPモード）:Java APIを使用したベイトナンバリングによるPDFドキュメントのアセンブリ](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-with-bates-numbering-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## WebサービスAPI {#assemble-documents-with-bates-numbering-using-the-web-service-api}を使用してベイツナンバリングを使用してドキュメントをアセンブル

Assembler Service API（Webサービス）を使用して、一意のページ識別子（ベイツナンバリング）を使用するPDFドキュメントをアセンブリします。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. PDFアセンブラクライアントを作成します。

   * `AssemblerServiceClient`オブジェクトを作成するには、そのオブジェクトのデフォルトのコンストラクタを使用します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`AssemblerServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに指定するstring値を渡します（例：`http://localhost:8080/soap/services/AssemblerService?blob=mtom`）。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する際に使用されます。
   * `AssemblerServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * AEM formsユーザー名をフィールド`AssemblerServiceClient.ClientCredentials.UserName.UserName`に割り当てます。
      * 対応するパスワード値をフィールド`AssemblerServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * 定数値`HttpClientCredentialType.Basic`をフィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に割り当てます。
      * 定数値`BasicHttpSecurityMode.TransportCredentialOnly`をフィールド`BasicHttpBindingSecurity.Security.Mode`に割り当てます。

1. 既存のDDXドキュメントの参照。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、DDXドキュメントの保存に使用されます。
   * コンストラクターを呼び出し、DDXドキュメントのファイルの場所と、ファイルを開くモードを表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得して、バイト配列のサイズを決定できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出して、バイト配列にストリームデータを入力します。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * `BLOB`オブジェクトに、`MTOM`フィールドにバイト配列の内容を割り当てて入力します。

1. 入力PDFドキュメントを参照します。

   * 各入力PDFドキュメントに対して、コンストラクターを使用して`BLOB`オブジェクトを作成します。 `BLOB`オブジェクトは、入力PDFドキュメントの保存に使用されます。
   * コンストラクターを呼び出して、`System.IO.FileStream`オブジェクトを作成します。 入力PDFドキュメントーのファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得して、バイト配列のサイズを決定できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出して、バイト配列にストリームデータを入力します。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * `BLOB`オブジェクトに`MTOM`プロパティを割り当て、バイト配列の内容を指定します。
   * `MyMapOf_xsd_string_To_xsd_anyType`オブジェクトを作成します。 このコレクションオブジェクトは、入力PDFドキュメントの格納に使用されます。
   * 入力PDFドキュメントごとに、`MyMapOf_xsd_string_To_xsd_anyType_Item`オブジェクトを作成します。 例えば、2つの入力PDFドキュメントを使用する場合は、2つの`MyMapOf_xsd_string_To_xsd_anyType_Item`オブジェクトを作成します。
   * キー名を表すstring値を`MyMapOf_xsd_string_To_xsd_anyType_Item`オブジェクトの`key`フィールドに割り当てます。 この値は、DDXドキュメントで指定されたPDFソース要素の値と一致する必要があります。 (このタスクは、入力PDFドキュメントごとに実行します)。
   * PDFドキュメントを格納している`BLOB`オブジェクトを`MyMapOf_xsd_string_To_xsd_anyType_Item`オブジェクトの`value`フィールドに割り当てます。 (このタスクは、入力PDFドキュメントごとに実行します)。
   * 追加`MyMapOf_xsd_string_To_xsd_anyType`オブジェクトの`MyMapOf_xsd_string_To_xsd_anyType_Item`オブジェクト。 `MyMapOf_xsd_string_To_xsd_anyType`オブジェクトの`Add`メソッドを呼び出し、`MyMapOf_xsd_string_To_xsd_anyType`オブジェクトを渡します。 (このタスクは、入力PDFドキュメントごとに実行します)。

1. ベイツナンバリングの初期値を設定します。

   * コンストラクターを使用して、実行時オプションを格納する`AssemblerOptionSpec`オブジェクトを作成します。
   * `AssemblerOptionSpec`オブジェクトに属する`firstBatesNumber`データメンバに数値を割り当てて、初期のベイツ数を設定します。

1. 入力PDFドキュメントをアセンブリします。

   `AssemblerServiceClient`オブジェクトの`invoke`メソッドを呼び出し、次の値を渡します。

   * DDXドキュメントを表す`BLOB`オブジェクトです。
   * 入力PDFドキュメントが含まれる`MyMapOf_xsd_string_To_xsd_anyType`オブジェクトです。 このキーはPDFソースファイルの名前と一致する必要があり、その値はそれらのファイルに対応する`BLOB`オブジェクトである必要があります。
   * 実行時オプションを指定する`AssemblerOptionSpec`オブジェクト。

   `invoke`メソッドは、ジョブの結果と発生した例外を含む`AssemblerResult`オブジェクトを返します。

1. 結果を抽出します。

   新しく作成されたPDFドキュメントを取得するには、次の操作を実行します。

   * `AssemblerResult`オブジェクトの`documents`フィールドにアクセスします。これは、結果のPDFドキュメントを含む`Map`オブジェクトです。
   * `Map`オブジェクトを繰り返し処理して、結果のドキュメントの名前と一致するキーを見つけます。 次に、その配列メンバーの`value`を`BLOB`にキャストします。
   * `BLOB`オブジェクトの`MTOM`プロパティにアクセスして、PDFドキュメントを表すバイナリデータを抽出します。 PDFファイルに書き出すことができるバイトの配列を返します。

**関連トピック**

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
