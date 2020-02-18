---
title: WebサービスAPIを使用したDDXドキュメントの検証
seo-title: WebサービスAPIを使用したDDXドキュメントの検証
description: 'null'
seo-description: 'null'
uuid: f6125746-6138-4e46-a1c4-fb24fd7399c5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/validating_ddx_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a6fe91ab-3aa0-4b3d-87c0-6cf69a2c4cc4
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# WebサービスAPIを使用したDDXドキュメントの検証 {#validate-a-ddx-document-using-theweb-service-api}

Assembler Service API（Webサービス）を使用してDDXドキュメントを検証します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >localhostをformsサーバーのIPアドレスに置き換えます。

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
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、DDXドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイト配列、開 `System.IO.FileStream` 始位置、ストリ `Read` ーム長を渡すことによって、バイト配列にストリームデータを設定します。
   * オブジェクト `BLOB` にバイト配列の内容をプロ `MTOM` パティに割り当てて、オブジェクトを設定します。

1. DDXドキュメントを検証するための実行時オプションを設定します。

   * コンストラクタ `AssemblerOptionSpec` ーを使用して、実行時のオプションを格納するオブジェクトを作成します。
   * オブジェクトのデータメンバーに値trueを割り当ててDDXドキュメントを検証するようにAssemblerサービスに指示する実行時オ `AssemblerOptionSpec` プションを設 `validateOnly` 定します。
   * Assemblerサービスがログファイルに書き込む情報の量を設定するには、オブジェクトのデータメンバーに文字列 `AssemblerOptionSpec` 値を割り当 `logLevel` てます。 ddxドキュメントを検証する場合、検証プロセスに役立つ詳細情報をログファイルに書き込む必要があります。 その結果、またはの値を指定でき `FINE` ます `FINER`。 設定可能なランタイムオプションについて詳しくは、『 `AssemblerOptionSpec` AEM Forms APIリファレンス』のクラス [リファレンスを参照し](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)てください。

1. 検証を実行します。

   オブジェクト `AssemblerServiceClient` のメソッドを `invokeDDX` 呼び出し、次の値を渡します。

   * DDXドキ `BLOB` ュメントを表すオブジェクトです。
   * 通常PDFドキ `null` ュメントを `Map` 格納するオブジェクトの値です。
   * 実行時 `AssemblerOptionSpec` のオプションを指定するオブジェクトです。
   このメ `invokeDDX` ソッドは、DDXドキ `AssemblerResult` ュメントが有効かどうかを指定する情報を含むオブジェクトを返します。

1. 検証結果をログファイルに保存します。

   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、ログファイルの場所とファイルを開くモードを表すstring値を渡します。 ファイル名の拡張子が.xmlであることを確認します。
   * オブジェクト `BLOB` のデータメンバーの値を取得して、ログ情報を格納するオ `AssemblerResult` ブジェクトを `jobLog` 作成します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `BLOB` します。 オブジェクトのフィールドの値を取得して、バイト `BLOB` 配列を設定し `MTOM` ます。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡すことで、バ `System.IO.BinaryWriter` イト配列の内 `Write` 容をPDFファイルに書き込みます。
   >[!NOTE]
   >
   >DDXドキュメントが無効な場合は、がスロー `OperationException` されます。 catchステートメント内では、オブジェクトのメンバの値 `OperationException` を取得でき `jobLog` ます。

**関連トピック**

[DDXドキュメントの検証](/help/forms/developing/validating-ddx-documents.md#validating-ddx-documents)

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
