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
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 2%

---


# WebサービスAPIを使用したDDXドキュメントの検証 {#validate-a-ddx-document-using-theweb-service-api}

Assembler Service API（Webサービス）を使用してDDXドキュメントを検証します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >localhostをformsサーバーのIPアドレスに置き換えます。

1. PDFアセンブラクライアントを作成します。

   * デフォルトのコンストラクターを使用して `AssemblerServiceClient` オブジェクトを作成します。
   * コンストラクターを使用して `AssemblerServiceClient.Endpoint.Address` オブジェクトを作成し `System.ServiceModel.EndpointAddress` ます。 WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/AssemblerService?blob=mtom`)に指定するstring値を渡します。 属性を使用する必要はありません `lc_version` 。 この属性は、サービス参照を作成する際に使用されます。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `AssemblerServiceClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当て `AssemblerServiceClient.ClientCredentials.UserName.UserName`ます。
      * 対応するパスワード値をフィールドに割り当て `AssemblerServiceClient.ClientCredentials.UserName.Password`ます。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当て `BasicHttpBindingSecurity.Security.Mode`ます。

1. 既存のDDXドキュメントの参照。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、DDXドキュメントの格納に使用されます。
   * コンストラクターを呼び出し、DDXドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
   * オブジェクトの `System.IO.FileStream``Read` メソッドを呼び出し、読み取るバイト配列、開始位置およびストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * オブジェクトのプロパティにバイト配列の内容を割り当てて、 `BLOB``MTOM` オブジェクトを入力します。

1. DDXドキュメントを検証するための実行時オプションを設定します。

   * コンストラクターを使用して、実行時のオプションを格納する `AssemblerOptionSpec` オブジェクトを作成します。
   * AssemblerサービスにDDXドキュメントの検証を指示する実行時オプションを設定します。この場合、値trueを `AssemblerOptionSpec` オブジェクトの `validateOnly` データメンバーに割り当てます。
   * Assemblerサービスがログファイルに書き込む情報の量を設定するには、 `AssemblerOptionSpec` オブジェクトの `logLevel` データメンバーに文字列値を割り当てます。 DDXドキュメントを検証する場合は、検証プロセスに役立つ詳細情報をログファイルに書き込む必要があります。 その結果、またはの値を指定でき `FINE` ま `FINER`す。 設定できる実行時オプションについて詳しくは、 `AssemblerOptionSpec` AEM FormsAPIリファレンスの [クラス参照を参照してください](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

1. 検証を実行します。

   オブジェクトの `AssemblerServiceClient``invokeDDX` メソッドを呼び出し、次の値を渡します。

   * DDXドキュメントを表す `BLOB` オブジェクトです。
   * 通常PDFドキュメント `null` を格納する `Map` オブジェクトの値です。
   * 実行時オプションを指定する `AssemblerOptionSpec` オブジェクトです。

   この `invokeDDX` メソッドは、DDXドキュメントが有効かどうかを指定する情報を含む `AssemblerResult` オブジェクトを返します。

1. 検証結果をログファイルに保存します。

   * コンストラクターを呼び出し、ログファイルのファイルの場所とファイルを開くモードを表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。 ファイル名の拡張子が.xmlであることを確認します。
   * オブジェクトの `BLOB` データメンバーの値を取得して、ログ情報を格納する `AssemblerResult``jobLog` オブジェクトを作成します。
   * オブジェクトの内容を格納するバイト配列を作成し `BLOB` ます。 オブジェクトのフィールドの値を取得して、 `BLOB` バイト配列を設定し `MTOM` ます。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡して、バイト配列の内容をPDFファイルに書き込み `System.IO.BinaryWriter` ま `Write` す。

   >[!NOTE]
   >
   >DDXドキュメントが無効な場合、がスロー `OperationException` されます。 catchステートメント内では、 `OperationException` オブジェクトの `jobLog` メンバの値を取得できます。

**関連トピック**

[DDXドキュメントの検証](/help/forms/developing/validating-ddx-documents.md#validating-ddx-documents)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
