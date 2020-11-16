---
title: 使用権限の割り当て
seo-title: 使用権限の割り当て
description: 'null'
seo-description: 'null'
uuid: 8c2020df-ea3c-49fa-916f-38a458f40d2b
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9e8db506-9ace-4e1f-8a7b-c4e9b15dde7e
translation-type: tm+mt
source-git-commit: 413af4ef9bc3652e05da78d622183bcf20a8bee7
workflow-type: tm+mt
source-wordcount: '3895'
ht-degree: 7%

---


# 使用権限の割り当て {#assigning-usage-rights}

## Acrobat Reader DC拡張サービスについて {#about-the-acrobat-reader-dc-extensions-service}

Acrobat Reader DC拡張サービスを使用すると、Adobe Readerの機能を拡張して、インタラクティブPDFドキュメントを簡単に共有できます。 Acrobat Reader DCエクステンションサービスは、PDF 1.7以降を含むすべてのPDFドキュメントを完全にサポートします。Adobe Reader7.0以降で機能します。 このサービスは、PDFドキュメントに使用権限を追加し、Adobe Readerを使用してPDFドキュメントを開いた場合に通常使用できない機能をアクティブ化します。 サードパーティユーザーは、使用権限を付与されたドキュメントを使用する場合に、追加のソフトウェアまたはプラグインを必要としません。

以下のタスクは、Acrobat Reader DCエクステンションサービスを使用して実行できます。

* 使用権限をPDFドキュメントに適用します。 詳しくは、「PDFドキュメントへの使用権限の [適用](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)」を参照してください。
* PDFドキュメントから使用権限を削除します。 詳しくは、「PDFドキュメントからの使用権限の [削除](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)」を参照してください。
* 秘密鍵証明書の詳細を取得します。 詳しくは、秘密鍵証明書情報の [取得を参照してください](assigning-usage-rights.md#retrieving-credential-information)。

>[!NOTE]
>
>For more information about the Acrobat Reader DC extensions service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Applying Usage Rights to PDF Documents {#applying-usage-rights-to-pdf-documents}

Acrobat Reader DC拡張機能Java Client APIおよびWebサービスを使用して、PDFドキュメントに使用権限を適用できます。 使用権限は、Acrobat ではデフォルトで利用できるが Adobe Reader では利用できない機能（フォームにコメントを追加する機能や、フォームフィールドにデータを入力してフォームを保存する機能など）に関連しています。使用権限が与えられた PDF ドキュメントは、使用権限を付与されたドキュメントと呼ばれます。使用権限を付与されたドキュメントを Adobe Reader で開いたユーザーは、そのドキュメントで有効になっている操作を実行できます。

>[!NOTE]
>
>Java APIの一部である `applyUsageRights` メソッドを使用してPDFドキュメントに使用権限を適用する場合、 `isModeFinal` オブジェクトの `ReaderExtensionsOptionSpec` パラメータをに設定できま `false`す。 その結果、フォーム処理済みカウンターが更新されず、パフォーマンスが向上します。 フォーム処理済みカウンターの更新を心配しない場合は、この `isModeFinal` パラメーターをに設定することをお勧めし `false`ます。

>[!NOTE]
>
>For more information about the Acrobat Reader DC extensions service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary-of-steps}

PDFドキュメントに使用権限を適用するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Acrobat Reader DC拡張クライアントオブジェクトを作成します。
1. PDFドキュメントを取得します。
1. 適用する使用権限を指定します。
1. 使用権限をPDFドキュメントに適用します。
1. 使用権限を付与されたPDFドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めます。

**Acrobat Reader DC拡張クライアントオブジェクトの作成**

プログラムによってAcrobat Reader DC拡張サービスの操作を実行するには、Acrobat Reader DC拡張サービスクライアントオブジェクトを作成する必要があります。 Acrobat Reader DC拡張機能のJava APIを使用している場合は、 `ReaderExtensionsServiceClient` オブジェクトを作成します。 Acrobat Reader DC拡張WebサービスAPIを使用している場合は、 `ReaderExtensionsServiceService` オブジェクトを作成します。

**PDFドキュメントの取得**

使用権限を適用するには、PDFドキュメントを取得する必要があります。 使用権限を付与されたPDFドキュメントには、使用権限ディクショナリが含まれています。 このような辞書を含むドキュメントをAdobe Readerが開くと、そのドキュメントに対してのみ、辞書で指定されている使用権限が有効になります。 ドキュメントに使用権限ディクショナリが含まれていない場合、Acrobat Reader DC拡張サービスによって使用権限ディクショナリが作成されます。 既にディクショナリが含まれている場合、Acrobat Reader DC拡張サービスは、既存の使用権限を指定した使用権限で上書きします。 この辞書は、有効にする使用権限を指定します。 ユーザーがAdobe Readerでドキュメントを開くと、その辞書で指定されている使用権限のみが許可されます。

**適用する使用権限の指定**

設定できる使用権限は、Adobe Systems Incorporatedから購入した秘密鍵証明書によって決まります。 通常、資格情報は、インタラクティブフォームに関連する使用権限など、関連する使用権限のグループを設定する権限を与えます。 各秘密鍵証明書には、特定の数の権限を付与されたPDFドキュメントを作成する権限が与えられます。 評価用の秘密鍵証明書によって、無制限の数のドラフトドキュメントを作成する権利が与えられます。

>[!NOTE]
>
>秘密鍵証明書で許可されていない使用権限を割り当てようとすると、例外が発生します。

**PDFドキュメントへの使用権限の適用**

使用権限をPDFドキュメントに適用するには、使用権限の適用に使用する秘密鍵証明書のエイリアスを参照します(秘密鍵証明書は通常、AEM Formsのインストール時にインストールされます)。 また、使用権限を適用するPDFドキュメントを指定する必要があります。 秘密鍵証明書の設定について詳しくは、使用しているアプリケーションサーバー版のインストールおよびデプロイに関するガイドを参照してください。

**使用権限を付与されたPDFドキュメントの保存**

Acrobat Reader DC拡張機能サービスが使用権限をPDFドキュメントに適用した後、使用権限を付与されたPDFドキュメントをPDFファイルとして保存できます。

**関連トピック**

[Java APIを使用した使用権限の適用](assigning-usage-rights.md#apply-usage-rights-using-the-java-api)

[WebサービスAPIを使用した使用権限の適用](assigning-usage-rights.md#apply-usage-rights-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Acrobat Reader DC拡張サービスAPIクイック開始](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Java APIを使用した使用権限の適用 {#apply-usage-rights-using-the-java-api}

Acrobat Reader DC拡張機能API(Java)を使用して、PDFドキュメントに使用権限を適用します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-reader-extensions-client.jarなどのクライアントJARファイルを含めます。

1. Acrobat Reader DC拡張クライアントオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `ReaderExtensionsServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. PDFドキュメントを取得します。

   * コンストラクターを使用し、PDFドキュメントの場所を指定するstring値を渡して、PDFドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 適用する使用権限を指定します。

   * コンストラクタを使用して、使用権限を表す `UsageRights` オブジェクトを作成します。
   * 適用する各使用権限に対して、その `UsageRights` オブジェクトに属する対応するメソッドを呼び出します。 例えば、 `enableFormFillIn` 使用権限を追加するには、 `UsageRights` オブジェクトの `enableFormFillIn` メソッドを呼び出して渡し `true`ます。 （適用する使用権限ごとに、この手順を繰り返します）。

1. 使用権限をPDFドキュメントに適用します。

   * コンストラクタを使用して `ReaderExtensionsOptionSpec` オブジェクトを作成します。このオブジェクトには、Acrobat Reader DC拡張サービスで必要な実行時オプションが含まれます。 このコンストラクターを呼び出す場合、次の値を指定する必要があります。

      * ドキュメントに適用する使用権限を含む `UsageRights` オブジェクト。
      * 使用権限を付与されたPDFドキュメントをAdobe Reader7.xで開いたときにユーザーに表示されるメッセージを指定するstring値です。このメッセージは、Adobe Reader8.0では表示されません。
   * オブジェクトのメソッドを呼び出し、次の値を渡して、使用権限をPDF `ReaderExtensionsServiceClient` ドキュメントに適用し `applyUsageRights` ます。

      * 使用権限が適用されるPDFドキュメントを含む `com.adobe.idp.Document` オブジェクト。
      * 使用権限の適用を可能にする秘密鍵証明書のエイリアスを指定するstring値。
      * 対応するパスワード値を指定する文字列値. (現在、このパラメーターは無視されます。 合格 `null`)。
   * 実行時オプションを含む `ReaderExtensionsOptionSpec` オブジェクトです。

   この `applyUsageRights` メソッドは、使用権限を付与されたPDFドキュメントを含む `com.adobe.idp.Document` オブジェクトを返します。

1. 使用権限を付与されたPDFドキュメントを保存します。

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が .pdf であることを確認します。
   * オブジェクトのメ `com.adobe.idp.Document` ソッドを呼び出して、 `copyToFile` オブジェクトの内容をファイルにコピーします(メソッドから返された `com.adobe.idp.Document``com.adobe.idp.Document``applyUsageRights` オブジェクトを必ず使用してください)。

**関連トピック**

[PDFドキュメントへの使用権限の適用](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[クイック開始（SOAPモード）:Java APIを使用した使用権限の適用](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-applying-usage-rights-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用した使用権限の適用 {#apply-usage-rights-using-the-web-service-api}

Acrobat Reader DC拡張機能API（Webサービス）を使用して、PDFドキュメントに使用権限を適用します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Forms `localhost` をホストするサーバーのIPアドレスに置き換えます。

1. Acrobat Reader DC拡張クライアントオブジェクトを作成します。

   * Create a `ReaderExtensionsServiceClient` object by using its default constructor.
   * Create a `ReaderExtensionsServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLをAEM Formsサービスに指定するstring値を渡します(例えば、 `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`)。 必ず、を指定してくだ `?blob=mtom`さい)。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `ReaderExtensionsServiceClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当て `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`ます。
      * 対応するパスワード値をフィールドに割り当て `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`ます。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当て `BasicHttpBindingSecurity.Security.Mode`ます。

1. PDFドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、使用権限が適用されるPDFドキュメントの保存に使用されます。
   * コンストラクターを呼び出し、PDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
   * オブジェクトのメソッドを呼び出して、バイト配列にストリームデータ `System.IO.FileStream` を入力し `Read` ます。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * オブジェクトのプロパティにバイト配列の内容を割り当てて、 `BLOB``MTOM` オブジェクトを入力します。

1. 適用する使用権限を指定します。

   * コンストラクタを使用して、使用権限を表す `UsageRights` オブジェクトを作成します。
   * 適用する使用権限ごとに、そのオブジェクトに属する対応するデータメンバー `true` に値を割り当て `UsageRights` ます。 例えば、 `enableFormFillIn` 使用権限を追加するには、 `true` オブジェクトの `UsageRights``enableFormFillIn` データメンバに割り当てます。 （適用する使用権限ごとに、この手順を繰り返します）。

1. 使用権限をPDFドキュメントに適用します。

   * コンストラクタを使用して `ReaderExtensionsOptionSpec` オブジェクトを作成します。このオブジェクトには、Acrobat Reader DC拡張サービスで必要な実行時オプションが含まれます。
   * オブジェクト `UsageRights` をオブジェクトの `ReaderExtensionsOptionSpec``usageRights` データメンバーに割り当てます。
   * 使用権限を付与されたPDFドキュメントをAdobe Readerで開いた場合にユーザーに表示されるメッセージを指定するstring値を `ReaderExtensionsOptionSpec` オブジェクトの `message` データメンバーに割り当てます。
   * オブジェクトのメソッドを呼び出し、次の値を渡して、使用権限をPDF `ReaderExtensionsServiceClient` ドキュメントに適用し `applyUsageRights` ます。

      * 使用権限が適用されるPDFドキュメントを含む `BLOB` オブジェクト。
      * 使用権限の適用を可能にする秘密鍵証明書のエイリアスを指定するstring値。
      * 対応するパスワード値を指定する文字列値. (現在、このパラメーターは無視されます。 合格 `null`)。
   * 実行時オプションを含む `ReaderExtensionsOptionSpec` オブジェクトです。

   この `applyUsageRights` メソッドは、使用権限を付与されたPDFドキュメントを含む `BLOB` オブジェクトを返します。

1. 使用権限を付与されたPDFドキュメントを保存します。

   * Create a `System.IO.FileStream` object by invoking its constructor. 使用権限を付与されたPDFドキュメントのファイルの場所を表すstring値を渡します。
   * メソッドが返した `BLOB` オブジェクトのデータ内容を格納するバイト配列を作成し `applyUsageRights` ます。 オブジェクトのデータメンバーの値を取得して、 `BLOB` バイト配列を入力し `MTOM` ます。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡して、バイト配列の内容をPDFファイルに書き込み `System.IO.BinaryWriter` ま `Write` す。

**関連トピック**

[PDFドキュメントへの使用権限の適用](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## PDFドキュメントからの使用権限の削除 {#removing-usage-rights-from-pdf-documents}

使用権限を有効にしたドキュメントから使用権限を削除できます。 使用権限を付与されたPDFドキュメントから使用権限を削除することも、その他のAEM Forms操作を実行するために必要です。 例えば、PDF ドキュメントに対する電子署名（または認証）は、使用権限を設定する前に実行する必要があります。したがって、使用権限を付与されたドキュメントに対して操作を実行する場合は、PDFドキュメントから使用権限を削除し、ドキュメントへの電子署名など他の操作を実行してから、ドキュメントに使用権限を再適用する必要があります。

>[!NOTE]
>
>For more information about the Acrobat Reader DC extensions service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-1}

使用権限を付与されたPDFドキュメントから使用権限を削除するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Acrobat Reader DC拡張クライアントオブジェクトを作成します。
1. 使用権限を付与されたPDFドキュメントを取得します。
1. PDFドキュメントから使用権限を削除します。
1. PDFドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めます。

**Acrobat Reader DC拡張クライアントオブジェクトの作成**

プログラムを使用してAcrobat Reader DC拡張サービスの操作を実行する前に、Acrobat Reader DC拡張サービスクライアントオブジェクトを作成する必要があります。 Java APIを使用している場合は、 `ReaderExtensionsServiceClient` オブジェクトを作成します。 Acrobat Reader DC拡張WebサービスAPIを使用している場合は、 `ReaderExtensionsServiceService` オブジェクトを作成します。

**使用権限を付与されたPDFドキュメントの取得**

使用権限を削除するために、使用権限を付与されたPDFドキュメントを取得します。

**PDFドキュメントからの使用権限の削除**

使用権限を付与されたPDFドキュメントを取得したら、使用権限を削除できます。 使用権限を削除すると、PDFドキュメントはAdobe Reader内で表示中、追加機能を持ちません。

**PDFドキュメントの保存**

使用権限がなくなったPDFドキュメントをPDFファイルとして保存できます。 PDFファイルとして保存すると、PDFドキュメントはAdobe ReaderまたはAcrobatで表示できます。

**関連トピック**

[Java APIを使用した使用権限の削除](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[WebサービスAPIを使用した使用権限の削除](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Acrobat Reader DC拡張サービスAPIクイック開始](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

[PDFドキュメントへの使用権限の適用](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

### Java APIを使用した使用権限の削除 {#remove-usage-rights-using-the-java-api}

Acrobat Reader DC拡張機能API(Java)を使用して、使用権限を付与されたPDFドキュメントから使用権限を削除します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-reader-extensions-client.jarなどのクライアントJARファイルを含めます。

1. Acrobat Reader DC拡張クライアントオブジェクトを作成します。

   コンストラクタを使用し、接続プロパティを含むオブジェクトを渡して、 `ReaderExtensionsServiceClient``ServiceClientFactory` オブジェクトを作成します。

1. PDFドキュメントを取得します。

   * コンストラクターを使用し、PDFドキュメントの場所を指定するstring値を渡して、使用権限を付与されたPDFドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PDFドキュメントから使用権限を削除します。

   オブジェクトの `ReaderExtensionsServiceClient` メソッドを呼び出し、使用権限を付与されたPDFドキュメントを含む `removeUsageRights``com.adobe.idp.Document` オブジェクトを渡すことで、使用権限をPDFドキュメントから削除します。 使用権限のないPDFドキュメントを含む `com.adobe.idp.Document` オブジェクトを返します。

1. 使用権限をPDFドキュメントに適用します。

   * Create a `java.io.File` object and ensure that the file extension is .PDF.
   * オブジェクトのメ `Document` ソッドを呼び出して、 `copyToFile` オブジェクトの内容をファイルにコピーします(メソッドから返された `Document``Document``removeUsageRights` オブジェクトを必ず使用してください)。

**関連トピック**

[PDFドキュメントからの使用権限の削除](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[クイック開始（SOAPモード）:Java APIを使用したPDFドキュメントからの使用権限の削除](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-removing-usage-rights-from-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用した使用権限の削除 {#remove-usage-rights-using-the-web-service-api}

Acrobat Reader DC拡張機能API（Webサービス）を使用して、使用権限を付与されたPDFドキュメントから使用権限を削除します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Forms `localhost` をホストするサーバーのIPアドレスに置き換えます。

1. Acrobat Reader DC拡張クライアントオブジェクトを作成します。

   * Create a `ReaderExtensionsServiceClient` object by using its default constructor.
   * Create a `ReaderExtensionsServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLをAEM Formsサービスに指定するstring値を渡します(例えば、 `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`)。 必ず、を指定してくだ `?blob=mtom`さい)。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `ReaderExtensionsServiceClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当て `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`ます。
      * 対応するパスワード値をフィールドに割り当て `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`ます。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当て `BasicHttpBindingSecurity.Security.Mode`ます。

1. PDFドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、使用権限が削除された、使用権限を付与されたPDFドキュメントの保存に使用されます。
   * コンストラクターを呼び出し、PDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
   * オブジェクトの `System.IO.FileStream``Read` メソッドを呼び出し、読み取るバイト配列、開始位置およびストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * オブジェクトのプロパティにバイト配列の内容を割り当てて、 `BLOB``MTOM` オブジェクトを入力します。

1. PDFドキュメントから使用権限を削除します。

   オブジェクトの `ReaderExtensionsServiceClient` メソッドを呼び出し、使用権限を付与されたPDFドキュメントを含む `removeUsageRights``BLOB` オブジェクトを渡すことで、使用権限をPDFドキュメントから削除します。 使用権限のないPDFドキュメントを含む `BLOB` オブジェクトを返します。

1. 使用権限をPDFドキュメントに適用します。

   * コンストラクターを呼び出し、PDFファイルの場所を表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * メソッドが返した `BLOB` オブジェクトのデータ内容を格納するバイト配列を作成し `removeUsageRights` ます。 オブジェクトのデータメンバーの値を取得して、 `BLOB` バイト配列を入力し `MTOM` ます。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.

**関連トピック**

[PDFドキュメントからの使用権限の削除](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 秘密鍵証明書情報の取得 {#retrieving-credential-information}

使用権限を付与されたPDFドキュメントに使用権限を適用するために使用された秘密鍵証明書に関する情報を取得できます。 秘密鍵証明書に関する情報を取得することで、証明書が無効になる日付などの情報を取得できます。

>[!NOTE]
>
>For more information about the Acrobat Reader DC extensions service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-2}

使用権限をPDFドキュメントに適用するために使用された秘密鍵証明書に関する情報を取得するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Acrobat Reader DC拡張クライアントオブジェクトを作成します。
1. 使用権限を付与されたPDFドキュメントを取得します。
1. 秘密鍵証明書に関する情報を取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めます。

**Acrobat Reader DC拡張クライアントオブジェクトの作成**

プログラムを使用してAcrobat Reader DC拡張サービスの操作を実行する前に、Acrobat Reader DC拡張サービスクライアントオブジェクトを作成する必要があります。 Java APIを使用している場合は、 `ReaderExtensionsServiceClient` オブジェクトを作成します。 Acrobat Reader DC拡張WebサービスAPIを使用している場合は、 `ReaderExtensionsServiceService` オブジェクトを作成します。

**使用権限を付与されたPDFドキュメントの取得**

秘密鍵証明書に関する情報を取得するには、使用権限を付与されたPDFドキュメントを取得する必要があります。 エイリアスを指定して、秘密鍵証明書に関する情報を取得することもできます。ただし、使用権限を特定の使用権限を付与されたPDFドキュメントに適用するために使用された秘密鍵証明書に関する情報を取得する場合は、ドキュメントを取得する必要があります。

**秘密鍵証明書に関する情報の取得**

使用権限を付与されたPDFドキュメントを取得したら、使用権限の適用に使用された秘密鍵証明書に関する情報を取得できます。 秘密鍵証明書に関する次の情報を取得できます。

* 使用権限を付与されたPDFドキュメントが開かれたときにAdobe Reader内に表示されるメッセージです。
* 秘密鍵証明書の失効日です。
* 秘密鍵証明書の有効期限が切れる日付です。
* この権限を付与されたPDFドキュメントに設定された使用権限です。
* 秘密鍵証明書が使用された回数。

**関連トピック**

[Java APIを使用した使用権限の削除](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[WebサービスAPIを使用した使用権限の削除](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Acrobat Reader DC拡張サービスAPIクイック開始](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Java APIを使用した秘密鍵証明書情報の取得 {#retrieve-credential-information-using-the-java-api}

Acrobat Reader DC拡張機能API(Java)を使用して秘密鍵証明書の情報を取得します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-reader-extensions-client.jarなどのクライアントJARファイルを含めます。

1. Acrobat Reader DC拡張クライアントオブジェクトを作成します。

   コンストラクタを使用し、接続プロパティを含むオブジェクトを渡して、 `ReaderExtensionsServiceClient``ServiceClientFactory` オブジェクトを作成します。

1. PDFドキュメントを取得します。

   * コンストラクターを使用し、権限を付与されたPDFドキュメントの場所を指定するstring値を渡すことで、権限を付与されたPDFドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PDFドキュメントから使用権限を削除します。

   * オブジェクトの `ReaderExtensionsServiceClient` メソッドを呼び出し、使用権限を付与されたPDFドキュメントを含む `getDocumentUsageRights``com.adobe.idp.Document` オブジェクトを渡すことで、PDFドキュメントに使用権限を適用するために使用される秘密鍵証明書に関する情報を取得します。 このメソッドは、秘密鍵証明書情報を含む `GetUsageRightsResult` オブジェクトを返します。
   * オブジェクトの `GetUsageRightsResult``getNotAfter` メソッドを呼び出して、秘密鍵証明書が無効になる日付を取得します。 このメソッドは、秘密鍵証明書の失効日を表す `java.util.Date` オブジェクトを返します。
   * 使用権限を付与されたPDFドキュメントを開いたときに、Adobe Readerに表示されるメッセージを取得します。その際には、 `GetUsageRightsResult` オブジェクトの `getMessage` メソッドを呼び出します。 このメソッドは、メッセージを表すstring値を返します。

**関連トピック**

[秘密鍵証明書情報の取得](assigning-usage-rights.md#retrieving-credential-information)

[クイック開始（SOAPモード）:Java APIを使用した秘密鍵証明書情報の取得](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-retrieving-credential-information-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用した秘密鍵証明書情報の取得 {#retrieve-credential-information-using-the-web-service-api}

Acrobat Reader DC拡張機能API（Webサービス）を使用して秘密鍵証明書の情報を取得します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Forms `localhost` をホストするサーバーのIPアドレスに置き換えます。

1. Acrobat Reader DC拡張クライアントオブジェクトを作成します。

   * デフォルトのコンストラクターを使用して `ReaderExtensionsServiceClient` オブジェクトを作成します。
   * Create a `ReaderExtensionsServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLをAEM Formsサービスに指定するstring値を渡します(例えば、 `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`)。 必ず、を指定してくだ `?blob=mtom`さい)。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `ReaderExtensionsServiceClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当て `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`ます。
      * 対応するパスワード値をフィールドに割り当て `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`ます。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当て `BasicHttpBindingSecurity.Security.Mode`ます。

1. PDFドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、使用権限を付与されたPDFドキュメントの保存に使用されます。
   * コンストラクターを呼び出し、使用権限を付与されたPDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
   * オブジェクトの `System.IO.FileStream``Read` メソッドを呼び出し、読み取るバイト配列、開始位置およびストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * オブジェクトのプロパティにバイト配列の内容を割り当てて、 `BLOB``MTOM` オブジェクトを入力します。

1. PDFドキュメントから使用権限を削除します。

   * オブジェクトの `ReaderExtensionsServiceClient` メソッドを呼び出し、使用権限を付与されたPDFドキュメントを含む `getDocumentUsageRights``com.adobe.idp.Document` オブジェクトを渡すことで、PDFドキュメントに使用権限を適用するために使用される秘密鍵証明書に関する情報を取得します。 このメソッドは、秘密鍵証明書情報を含む `GetUsageRightsResult` オブジェクトを返します。
   * オブジェクトの `GetUsageRightsResult``notAfter` データメンバーの値を取得して、秘密鍵証明書が無効になる日付を取得します。 このデータメンバのデータ型はで `System.DateTime`す。
   * オブジェクトの `GetUsageRightsResult``message` データメンバーの値を取得して、使用権限を付与されたPDFドキュメントをAdobe Readerで開いたときに表示されるメッセージを取得します。 このデータメンバのデータ型は文字列です。
   * オブジェクトの `GetUsageRightsResult``useCount` データメンバーの値を取得して、秘密鍵証明書が使用された回数を取得します。 このデータメンバのデータ型は整数です。

**関連トピック**

[秘密鍵証明書情報の取得](assigning-usage-rights.md#retrieving-credential-information)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
