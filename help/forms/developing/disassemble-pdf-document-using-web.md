---
title: Web サービス API を使用したPDFドキュメントの分割
seo-title: Disassemble a PDF document usingthe web service API
description: Assembler サービス API を使用したPDFドキュメントの分割
seo-description: Disassemble a PDF document using the Assembler Service API
uuid: d6283dc5-e333-49d0-abde-1d390662f4fe
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/programmatically_disassembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 49584fb4-8c3a-4d73-acd6-0879a67f6093
role: Developer
exl-id: de2f90ad-5dea-40a0-8c6d-d6b08228310d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 100%

---

# Web サービス API を使用した PDF ドキュメントの分割 {#disassemble-a-pdf-document-usingthe-web-service-api}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

Assembler サービス API（web サービス）を使用して PDF ドキュメントを分割します。

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

   * コンストラクターを使用して `BLOB` オブジェクトを作成します。`BLOB` オブジェクトは、DDX ドキュメントを保存するために使用されます。
   * コンストラクタを呼び出して `System.IO.FileStream` オブジェクトを作成します。DDX ドキュメントのファイルの場所を表す文字列値と、ファイルを開くモードを表す文字列値を渡します。
   * `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することで、バイト配列のサイズを決定できます。
   * バイト配列にストリームデータを入力するには、`System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出し、バイト配列、開始位置、読み取るストリーム長を渡します。
   * `MTOM` プロパティにバイト配列の内容を割り当てることによって、`BLOB` オブジェクトにデータを入力します。

1. 分割する PDF ドキュメントを参照します。

   * コンストラクターを使用して `BLOB` オブジェクトを作成します。`BLOB` オブジェクトは、入力 PDF ドキュメントを格納するために使用します。この `BLOB` オブジェクトは引数として `invokeOneDocument` に渡されます。
   * コンストラクタを呼び出し、入力 PDF ドキュメントのファイルの場所とファイルを開くモードを表す文字列値を渡すことによって、`System.IO.FileStream` オブジェクトを作成します。
   * `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することで、バイト配列のサイズを決定できます。
   * `System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出し、バイト配列、開始位置、読み取るストリーム長を渡すことによって、バイト配列にストリームデータを入力します。
   * バイト配列の内容を `MTOM` フィールドに割り当てることで、`BLOB` オブジェクトにデータを入力します。
   * `MyMapOf_xsd_string_To_xsd_anyType` オブジェクトを作成します。このコレクションオブジェクトは、ディスアセンブルする PDF を保存するために使用されます。
   * `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトを作成します。
   * キー名を表す文字列値を `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトの `key` フィールドに割り当てます。この値は、DDX ドキュメントで指定された PDF ソース要素の値と一致している必要があります。
   * PDF ドキュメントを格納する `BLOB` オブジェクトを、`MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトの `value` フィールドに割り当てます。
   * `MyMapOf_xsd_string_To_xsd_anyType_Item` オブジェクトを `MyMapOf_xsd_string_To_xsd_anyType` オブジェクトに追加します。`MyMapOf_xsd_string_To_xsd_anyType` オブジェクトの `Add` メソッドを呼び出して、`MyMapOf_xsd_string_To_xsd_anyType` オブジェクトを渡します。

1. 実行時オプションを設定します。

   * ランタイムオプションを格納する `AssemblerOptionSpec` オブジェクトをコンストラクタで作成します。
   * `AssemblerOptionSpec` オブジェクトに属するデータメンバーに値を割り当てることで、ビジネス要件を満たす実行時オプションを設定します。例えば、エラーが発生してもジョブの処理を続行するよう Assembler サービスに指示するには、`AssemblerOptionSpec` オブジェクトの `failOnError` フィールドに `false` を割り当てます。

1. PDF ドキュメントを分割します。

   `AssemblerServiceClient` オブジェクトの `invokeDDX` メソッドを呼び出して、次の値を渡します。

   * PDF ドキュメントをディスアセンブルする DDX ドキュメントを表す `BLOB` オブジェクト
   * ディスアセンブルする PDF ドキュメントを含む `MyMapOf_xsd_string_To_xsd_anyType` オブジェクト
   * 実行時オプションを指定する `AssemblerOptionSpec` オブジェクト

   `invokeDDX` メソッドは、ジョブの結果および発生した例外を含む `AssemblerResult` オブジェクトを返します。

1. 分割した PDF ドキュメントを保存します。

   新しく作成した PDF ドキュメントを取得するには、次の操作を実行します。

   * `AssemblerResult` オブジェクトの `documents` フィールド（ディスアセンブリされた PDF ドキュメントを含む `Map` オブジェクト）にアクセスします。
   * `Map`オブジェクトを反復処理して、各結果ドキュメントを取得します。次に、その配列メンバーの`value`を`BLOB`にキャストします。
   * `BLOB`オブジェクトの`MTOM`プロパティにアクセスして、PDF ドキュメントを表すバイナリデータを抽出します。これにより、PDF ファイルに書き出すことができるバイト配列が返されます。

**関連トピック**

[プログラムによる PDF ドキュメントの分割](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
