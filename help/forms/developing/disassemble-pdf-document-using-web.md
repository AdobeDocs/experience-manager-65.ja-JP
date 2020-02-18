---
title: WebサービスAPIを使用したPDFドキュメントのディスアセンブリ
seo-title: WebサービスAPIを使用したPDFドキュメントのディスアセンブリ
description: 'null'
seo-description: 'null'
uuid: d6283dc5-e333-49d0-abde-1d390662f4fe
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/programmatically_disassembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 49584fb4-8c3a-4d73-acd6-0879a67f6093
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# WebサービスAPIを使用したPDFドキュメントのディスアセンブリ {#disassemble-a-pdf-document-usingthe-web-service-api}

Assembler Service API（Webサービス）を使用してPDFドキュメントをディスアセンブリします。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 サービス参照を設定する際は、必ず次のWSDL定義を使用してください。 `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

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
   * Create a `System.IO.FileStream` object by invoking its constructor. DDXドキュメントのファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイト配列、開 `System.IO.FileStream` 始位置、ストリ `Read` ーム長を渡すことによって、バイト配列にストリームデータを設定します。
   * オブジェクト `BLOB` にバイト配列の内容をプロ `MTOM` パティに割り当てて、オブジェクトを設定します。

1. ディスアセンブリするPDFドキュメントを参照します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、入力PDFドキュメントの保存に使用されます。 このオ `BLOB` ブジェクトは、引数として `invokeOneDocument` に渡されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、入力PDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイト配列、開 `System.IO.FileStream` 始位置、ストリ `Read` ーム長を渡すことによって、バイト配列にストリームデータを設定します。
   * オブジェクトに `BLOB` バイト配列の内容をフィー `MTOM` ルドに割り当てて、オブジェクトを入力します。
   * Create a `MyMapOf_xsd_string_To_xsd_anyType` object. このコレクションオブジェクトは、ディスアセンブリするPDFを保存するために使用されます。
   * Create a `MyMapOf_xsd_string_To_xsd_anyType_Item` object.
   * キー名を表すstring値をオブジェクトのフィールド `MyMapOf_xsd_string_To_xsd_anyType_Item` に割り当て `key` ます。 この値は、DDXドキュメントで指定されたPDFソース要素の値と一致する必要があります。
   * PDFドキュメント `BLOB` を保存するオブジェクトをオブジェクトのフィー `MyMapOf_xsd_string_To_xsd_anyType_Item` ルドに割り当 `value` てます。
   * オブジェクト `MyMapOf_xsd_string_To_xsd_anyType_Item` をオブジェクトに追加 `MyMapOf_xsd_string_To_xsd_anyType` します。 オブジェクトの `MyMapOf_xsd_string_To_xsd_anyType` メソッドを呼 `Add` び出し、オブジェクトを渡 `MyMapOf_xsd_string_To_xsd_anyType` します。

1. 実行時オプションを設定します。

   * コンストラクタ `AssemblerOptionSpec` ーを使用して、実行時のオプションを格納するオブジェクトを作成します。
   * オブジェクトに属するデータメンバーに値を割り当てて、ビジネス要件に合わせて実行時オプションを設定 `AssemblerOptionSpec` します。 例えば、エラーが発生した場合にジョブの処理を続行するようAssemblerサービスに指示するには、オブジェクトのフ `false` ィールドに `AssemblerOptionSpec` 割り当て `failOnError` ます。

1. PDFドキュメントのディスアセンブリ

   オブジェクト `AssemblerServiceClient` のメソッドを `invokeDDX` 呼び出し、次の値を渡します。

   * PDFドキ `BLOB` ュメントをディスアセンブリするDDXドキュメントを表すオブジェクトです
   * ディスア `MyMapOf_xsd_string_To_xsd_anyType` センブリするPDFドキュメントを含むオブジェクト
   * 実行時 `AssemblerOptionSpec` のオプションを指定するオブジェクト
   このメ `invokeDDX` ソッドは、ジョ `AssemblerResult` ブの結果と発生した例外を含むオブジェクトを返します。

1. 分解されたPDFドキュメントを保存します。

   新しく作成されたPDFドキュメントを取得するには、次の操作を実行します。

   * オブジェクトのフ `AssemblerResult` ィールドにアク `documents` セスします。このフィールドは、ア `Map` センブル解除されたPDFドキュメントを含むオブジェクトです。
   * オブジェクトを繰り返し `Map` 処理し、各結果ドキュメントを取得します。 次に、その配列メンバーをにキャス `value` トします `BLOB`。
   * PDFドキュメントを表すバイナリデータを抽出するには、そのオブジェクトのプロパ `BLOB` ティにアクセス `MTOM` します。 PDFファイルに書き出し可能なバイト配列を返します。

**関連トピック**

[PDFドキュメントのプログラムによるディスアセンブリ](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
