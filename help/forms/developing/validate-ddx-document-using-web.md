---
title: WebサービスAPIを使用したDDXドキュメントの検証
seo-title: WebサービスAPIを使用したDDXドキュメントの検証
description: Assembler Service APIを使用してDDXドキュメントを検証します。
seo-description: Assembler Service APIを使用してDDXドキュメントを検証します。
uuid: f6125746-6138-4e46-a1c4-fb24fd7399c5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/validating_ddx_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a6fe91ab-3aa0-4b3d-87c0-6cf69a2c4cc4
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 2%

---


# WebサービスAPI {#validate-a-ddx-document-using-theweb-service-api}を使用したDDXドキュメントの検証

Assembler Service API（Webサービス）を使用してDDXドキュメントを検証します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >localhostをformsサーバーのIPアドレスに置き換えます。

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
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * `BLOB`オブジェクトに`MTOM`プロパティを割り当て、バイト配列の内容を指定します。

1. DDXドキュメントを検証するための実行時オプションを設定します。

   * コンストラクターを使用して、実行時オプションを格納する`AssemblerOptionSpec`オブジェクトを作成します。
   * `AssemblerOptionSpec`オブジェクトの`validateOnly`データメンバーに値trueを割り当てることで、DDXドキュメントの検証をAssemblerサービスに指示する実行時オプションを設定します。
   * Assemblerサービスがログファイルに書き込む情報の量を設定するには、`AssemblerOptionSpec`オブジェクトの`logLevel`データメンバーに文字列値を割り当てます。 DDXドキュメントを検証する場合は、検証プロセスに役立つ詳細情報をログファイルに書き込む必要があります。 その結果、`FINE`または`FINER`の値を指定できます。 設定できる実行時オプションについて詳しくは、[AEM FormsAPIリファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)の`AssemblerOptionSpec`クラス参照を参照してください。

1. 検証を実行します。

   `AssemblerServiceClient`オブジェクトの`invokeDDX`メソッドを呼び出し、次の値を渡します。

   * DDXドキュメントを表す`BLOB`オブジェクトです。
   * 通常PDFドキュメントを格納する`Map`オブジェクトの値`null`です。
   * 実行時オプションを指定する`AssemblerOptionSpec`オブジェクト。

   `invokeDDX`メソッドは、DDXドキュメントが有効かどうかを指定する情報を含む`AssemblerResult`オブジェクトを返します。

1. 検証結果をログファイルに保存します。

   * コンストラクターを呼び出し、ログファイルのファイルの場所とファイルを開くモードを表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。 ファイル名の拡張子が.xmlであることを確認します。
   * `AssemblerResult`オブジェクトの`jobLog`データメンバの値を取得して、ログ情報を格納する`BLOB`オブジェクトを作成します。
   * `BLOB`オブジェクトの内容を格納するバイト配列を作成します。 `BLOB`オブジェクトの`MTOM`フィールドの値を取得して、バイト配列を入力します。
   * コンストラクターを呼び出して`System.IO.FileStream`オブジェクトを渡し、`System.IO.BinaryWriter`オブジェクトを作成します。
   * `System.IO.BinaryWriter`オブジェクトの`Write`メソッドを呼び出し、バイト配列を渡すことで、バイト配列の内容をPDFファイルに書き込みます。

   >[!NOTE]
   >
   >DDXドキュメントが無効な場合は、`OperationException`がスローされます。 catchステートメント内では、`OperationException`オブジェクトの`jobLog`メンバの値を取得できます。

**関連トピック**

[DDXドキュメントの検証](/help/forms/developing/validating-ddx-documents.md#validating-ddx-documents)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
