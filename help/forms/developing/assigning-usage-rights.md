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

---


# 使用権限の割り当て {#assigning-usage-rights}

## Acrobat Reader DCエクステンションサービスについて {#about-the-acrobat-reader-dc-extensions-service}

Acrobat Reader DCエクステンションサービスを使用すると、Adobe Readerの機能を拡張して、組織でインタラクティブPDFドキュメントを簡単に共有できます。 Acrobat Reader DCエクステンションサービスは、PDF 1.7以前のPDFドキュメントを完全にサポートします。Adobe Reader 7.0以降で動作します。 このサービスは、PDFドキュメントに使用権限を追加し、Adobe Readerを使用してPDFドキュメントを開いた場合に通常使用できない機能をアクティブ化します。 サードパーティユーザーは、使用権限を付与されたドキュメントを使用するために追加のソフトウェアまたはプラグインを必要としません。

Acrobat Reader DCエクステンションサービスを使用して、次のタスクを実行できます。

* PDFドキュメントに使用権限を適用します。 詳しくは、「PDFドキュメント [への使用権限の適用」を参照してください](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)。
* PDFドキュメントから使用権限を削除します。 詳しくは、「PDFドキュメン [トからの使用権限の削除」を参照してください](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)。
* 秘密鍵証明書の詳細を取得します。 詳しくは、秘密鍵証明書情報の取 [得を参照してください](assigning-usage-rights.md#retrieving-credential-information)。

>[!NOTE]
>
>For more information about the Acrobat Reader DC extensions service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Applying Usage Rights to PDF Documents {#applying-usage-rights-to-pdf-documents}

Acrobat Reader DC Extensions Java Client APIおよびWebサービスを使用して、PDFドキュメントに使用権限を適用できます。 使用権限は、Acrobat ではデフォルトで利用できるが Adobe Reader では利用できない機能（フォームにコメントを追加する機能や、フォームフィールドにデータを入力してフォームを保存する機能など）に関連しています。使用権限が与えられた PDF ドキュメントは、使用権限を付与されたドキュメントと呼ばれます。使用権限を付与されたドキュメントを Adobe Reader で開いたユーザーは、そのドキュメントで有効になっている操作を実行できます。

>[!NOTE]
>
>Java APIの一部であるメソッドを使用してPDF `applyUsageRights` ドキュメントに使用権限を適用する場合は、オブジェクトのパラメー `isModeFinal` ターをに設定 `ReaderExtensionsOptionSpec` できま `false`す。 その結果、フォーム処理済みのカウンターが更新されず、パフォーマンスが向上します。 フォーム処理済みのカウンターの更新を気にしない場合は、このパラメーターをに設定することをお `isModeFinal` 勧めしま `false`す。

>[!NOTE]
>
>For more information about the Acrobat Reader DC extensions service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary-of-steps}

PDFドキュメントに使用権限を適用するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Acrobat Reader DC Extensions clientオブジェクトを作成します。
1. PDFドキュメントを取得します。
1. 適用する使用権限を指定します。
1. PDFドキュメントに使用権限を適用します。
1. 使用権限を付与されたPDFドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

**Acrobat Reader DC Extensionsクライアントオブジェクトの作成**

プログラムによってAcrobat Reader DC Extensionsサービスの操作を実行するには、Acrobat Reader DC Extensionsサービスクライアントオブジェクトを作成する必要があります。 Acrobat Reader DC Extensions Java APIを使用している場合は、オブジェクトを作成し `ReaderExtensionsServiceClient` ます。 Acrobat Reader DC Extensions webサービスAPIを使用している場合は、オブジェクトを作成し `ReaderExtensionsServiceService` ます。

**PDFドキュメントの取得**

使用権限を適用するには、PDFドキュメントを取得する必要があります。 使用権限を付与されたPDFドキュメントには、使用権限ディクショナリが含まれています。 Adobe Readerは、その辞書を含むドキュメントを開くと、そのドキュメントに対してのみ、辞書で指定された使用権限を有効にします。 ドキュメントに使用権限ディクショナリが含まれていない場合、Acrobat Reader DCエクステンションサービスによって使用権限ディクショナリが作成されます。 既に辞書が含まれている場合、Acrobat Reader DCエクステンションサービスは、指定した使用権限で既存の使用権限を上書きします。 この辞書は、有効にする使用権限を指定します。 ユーザーがAdobe readerでドキュメントを開くと、辞書で指定された使用権限のみが許可されます。

**適用する使用権限の指定**

設定できる使用権限は、Adobe Systems Incorporatedで購入した秘密鍵証明書によって決まります。 通常、資格情報は、インタラクティブフォームに関連する使用権限など、関連する使用権限のグループを設定する権限を提供します。 各秘密鍵証明書は、特定の数の権限を付与されたPDFドキュメントを作成する権限を提供します。 評価用の秘密鍵証明書を使用すると、無制限の数のドラフトドキュメントを作成できます。

>[!NOTE]
>
>秘密鍵証明書で許可されていない使用権限を割り当てようとすると、例外が発生します。

**PDFドキュメントへの使用権限の適用**

PDFドキュメントに使用権限を適用するには、使用権限の適用に使用する秘密鍵証明書のエイリアスを参照します（秘密鍵証明書は通常、AEM Formsのインストール時にインストールされます）。 また、使用権限が適用されるPDFドキュメントを指定する必要があります。 秘密鍵証明書の設定について詳しくは、使用しているアプリケーションサーバー版のインストールおよびデプロイに関するガイドを参照してください。

**使用権限を付与されたPDFドキュメントの保存**

Acrobat Reader DCエクステンションサービスで使用権限をPDFドキュメントに適用した後、使用権限を付与されたPDFドキュメントをPDFファイルとして保存できます。

**関連トピック**

[Java APIを使用した使用権限の適用](assigning-usage-rights.md#apply-usage-rights-using-the-java-api)

[WebサービスAPIを使用した使用権限の適用](assigning-usage-rights.md#apply-usage-rights-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Acrobat Reader DC ExtensionsサービスAPIクイックスタート](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Java APIを使用した使用権限の適用 {#apply-usage-rights-using-the-java-api}

Acrobat Reader DC Extensions API(Java)を使用してPDFドキュメントに使用権限を適用します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-reader-extensions-client.jarなどのクライアントJARファイルを含めます。

1. Acrobat Reader DC Extensions clientオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `ReaderExtensionsServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. PDFドキュメントを取得します。

   * PDFドキュメ `java.io.FileInputStream` ントを表すオブジェクトを作成します。このオブジェクトは、コンストラクターを使用し、PDFドキュメントの場所を指定するstring値を渡すことによって作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 適用する使用権限を指定します。

   * コンストラク `UsageRights` ターを使用して、使用権限を表すオブジェクトを作成します。
   * 適用する各使用権限に対して、オブジェクトに属する対応するメソッドを呼び出 `UsageRights` します。 例えば、使用権限を追加す `enableFormFillIn` るには、オブジェクトのメ `UsageRights` ソッドを呼び出 `enableFormFillIn` して渡しま `true`す。 （適用する各使用権限に対して、この手順を繰り返します）。

1. PDFドキュメントに使用権限を適用します。

   * コンストラクタを使用して `ReaderExtensionsOptionSpec` オブジェクトを作成します。このオブジェクトには、Acrobat Reader DCエクステンションサービスで必要な実行時オプションが含まれています。 このコンストラクターを呼び出す場合は、次の値を指定する必要があります。

      * ドキュメント `UsageRights` に適用する使用権限を含むオブジェクトです。
      * 使用権限を付与されたPDFドキュメントをAdobe Reader 7.xで開いたときにユーザーに表示されるメッセージを指定するstring値です。このメッセージはAdobe Reader 8.0では表示されません。
   * オブジェクトのメソッドを呼び出し、次の値を渡して、PDF `ReaderExtensionsServiceClient` ドキュメントに `applyUsageRights` 使用権限を適用します。

      * 使用権 `com.adobe.idp.Document` 限が適用されるPDFドキュメントを含むオブジェクトです。
      * 使用権限の適用を可能にする秘密鍵証明書のエイリアスを指定するstring値。
      * 対応するパスワード値を指定する文字列値. (現在、このパラメーターは無視されます。 合格 `null`)
   * 実行時 `ReaderExtensionsOptionSpec` のオプションを含むオブジェクトです。
   このメソ `applyUsageRights` ッドは、使用権限を付与 `com.adobe.idp.Document` されたPDFドキュメントを含むオブジェクトを返します。

1. 使用権限を付与されたPDFドキュメントを保存します。

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が .pdf であることを確認します。
   * オブジェクト `com.adobe.idp.Document` のメソッドを呼び出 `copyToFile` して、オブジェクトの内容をファイルにコピ `com.adobe.idp.Document` ーします(メソッドによって返されたオブジェクトを使用 `com.adobe.idp.Document` していることを確 `applyUsageRights` 認します)。

**関連トピック**

[PDFドキュメントへの使用権限の適用](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[クイックスタート（SOAPモード）:Java APIを使用した使用権限の適用](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-applying-usage-rights-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用した使用権限の適用 {#apply-usage-rights-using-the-web-service-api}

Acrobat Reader DC Extensions API（Webサービス）を使用して、PDFドキュメントに使用権限を適用します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. Acrobat Reader DC Extensions clientオブジェクトを作成します。

   * Create a `ReaderExtensionsServiceClient` object by using its default constructor.
   * Create a `ReaderExtensionsServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLを指定するstring値をAEM Formsサービスに渡します(例： `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`)。 必ず、を指定し `?blob=mtom`ます。)
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `ReaderExtensionsServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. PDFドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、使用権限が適用されるPDFドキュメントの保存に使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、PDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出して、バイト配列にストリームデ `System.IO.FileStream` ータを入力 `Read` します。 読み取るバイト配列、開始位置およびストリーム長を渡します。
   * オブジェクト `BLOB` にバイト配列の内容をプロ `MTOM` パティに割り当てて、オブジェクトを設定します。

1. 適用する使用権限を指定します。

   * コンストラク `UsageRights` ターを使用して、使用権限を表すオブジェクトを作成します。
   * 適用する各使用権限に対して、オブジェクトに属す `true` る対応するデータメンバーに値を割り当て `UsageRights` ます。 例えば、使用権限を追加す `enableFormFillIn` るには、オブジェクトの `true` データメ `UsageRights` ンバーに割り当 `enableFormFillIn` てます。 （適用する各使用権限に対して、この手順を繰り返します）。

1. PDFドキュメントに使用権限を適用します。

   * コンストラクタを使用して `ReaderExtensionsOptionSpec` オブジェクトを作成します。このオブジェクトには、Acrobat Reader DCエクステンションサービスで必要な実行時オプションが含まれています。
   * オブジェクト `UsageRights` をオブジェクトのデ `ReaderExtensionsOptionSpec` ータメンバーに `usageRights` 割り当てます。
   * 使用権限を付与されたPDFドキュメントをAdobe Readerで開いたときにユーザーに表示されるメッセージをオブジェクトのデータメンバ `ReaderExtensionsOptionSpec` ーに割り当 `message` てます。
   * オブジェクトのメソッドを呼び出し、次の値を渡して、PDF `ReaderExtensionsServiceClient` ドキュメントに `applyUsageRights` 使用権限を適用します。

      * 使用権 `BLOB` 限が適用されるPDFドキュメントを含むオブジェクトです。
      * 使用権限の適用を可能にする秘密鍵証明書のエイリアスを指定するstring値。
      * 対応するパスワード値を指定する文字列値. (現在、このパラメーターは無視されます。 合格 `null`)
   * 実行時 `ReaderExtensionsOptionSpec` のオプションを含むオブジェクトです。
   このメソ `applyUsageRights` ッドは、使用権限を付与 `BLOB` されたPDFドキュメントを含むオブジェクトを返します。

1. 使用権限を付与されたPDFドキュメントを保存します。

   * Create a `System.IO.FileStream` object by invoking its constructor. 使用権限を付与されたPDFドキュメントのファイルの場所を表すstring値を渡します。
   * メソッドによって返されたオブジェクトのデータ内容を格納 `BLOB` するバイト配列を作成 `applyUsageRights` します。 オブジェクトのデータメンバーの値を取得して、バ `BLOB` イト配列を `MTOM` 設定します。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡すことで、バ `System.IO.BinaryWriter` イト配列の内 `Write` 容をPDFファイルに書き込みます。

**関連トピック**

[PDFドキュメントへの使用権限の適用](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## PDFドキュメントからの使用権限の削除 {#removing-usage-rights-from-pdf-documents}

使用権限を付与されたドキュメントから使用権限を削除できます。 使用権限を付与されたPDFドキュメントに対して他のAEM Forms操作を実行するには、そのドキュメントから使用権限を削除する必要もあります。 例えば、PDF ドキュメントに対する電子署名（または認証）は、使用権限を設定する前に実行する必要があります。したがって、使用権限を付与されたドキュメントに対して操作を実行する場合は、PDFドキュメントから使用権限を削除し、その他の操作（ドキュメントへの電子署名など）を実行して、使用権限をドキュメントに再適用する必要があります。

>[!NOTE]
>
>For more information about the Acrobat Reader DC extensions service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-1}

使用権限を付与されたPDFドキュメントから使用権限を削除するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Acrobat Reader DC Extensions clientオブジェクトを作成します。
1. 使用権限を付与されたPDFドキュメントを取得します。
1. PDFドキュメントから使用権限を削除します。
1. PDFドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

**Acrobat Reader DC Extensionsクライアントオブジェクトの作成**

プログラムを使用してAcrobat Reader DC Extensionsサービスの操作を実行する前に、Acrobat Reader DC Extensionsサービスクライアントオブジェクトを作成する必要があります。 Java APIを使用している場合は、オブジェクトを作成し `ReaderExtensionsServiceClient` ます。 Acrobat Reader DC Extensions webサービスAPIを使用している場合は、オブジェクトを作成し `ReaderExtensionsServiceService` ます。

**使用権限を付与されたPDFドキュメントの取得**

使用権限を削除するために、使用権限を付与されたPDFドキュメントを取得します。

**PDFドキュメントからの使用権限の削除**

使用権限を付与されたPDFドキュメントを取得した後、使用権限を削除できます。 使用権限を削除すると、Adobe reader内で表示中に、PDFドキュメントに追加機能が追加されなくなります。

**PDFドキュメントの保存**

使用権限がなくなったPDFドキュメントをPDFファイルとして保存できます。 PDFファイルとして保存すると、そのPDFドキュメントをAdobe readerまたはAcrobatで表示できます。

**関連トピック**

[Java APIを使用した使用権限の削除](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[WebサービスAPIを使用した使用権限の削除](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Acrobat Reader DC ExtensionsサービスAPIクイックスタート](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

[PDFドキュメントへの使用権限の適用](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

### Java APIを使用した使用権限の削除 {#remove-usage-rights-using-the-java-api}

Acrobat Reader DC Extensions API(Java)を使用して、使用権限を付与されたPDFドキュメントから使用権限を削除します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-reader-extensions-client.jarなどのクライアントJARファイルを含めます。

1. Acrobat Reader DC Extensions clientオブジェクトを作成します。

   コンストラク `ReaderExtensionsServiceClient` ターを使用し、接続プロパティを含むオブジェクトを渡 `ServiceClientFactory` して、オブジェクトを作成します。

1. PDFドキュメントを取得します。

   * コンストラ `java.io.FileInputStream` クターを使用し、PDFドキュメントの場所を指定するstring値を渡して、使用権限を付与されたPDFドキュメントを表すオブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PDFドキュメントから使用権限を削除します。

   オブジェクトのメソッドを呼び出し、使用権限を付与されたPDFドキ `ReaderExtensionsServiceClient` ュメントを含むオ `removeUsageRights` ブジェクトを渡すこ `com.adobe.idp.Document` とで、PDFドキュメントから使用権限を削除します。 このメソッドは、使用 `com.adobe.idp.Document` 権限のないPDFドキュメントを含むオブジェクトを返します。

1. PDFドキュメントに使用権限を適用します。

   * Create a `java.io.File` object and ensure that the file extension is .PDF.
   * オブジェクト `Document` のメソッドを呼び出 `copyToFile` して、オブジェクトの内容をファイルにコピ `Document` ーします(メソッドによって返されたオブジェクトを使用 `Document` していることを確 `removeUsageRights` 認します)。

**関連トピック**

[PDFドキュメントからの使用権限の削除](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[クイックスタート（SOAPモード）:Java APIを使用したPDFドキュメントからの使用権限の削除](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-removing-usage-rights-from-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用した使用権限の削除 {#remove-usage-rights-using-the-web-service-api}

Acrobat Reader DCエクステンションAPI（Webサービス）を使用して、使用権限を付与されたPDFドキュメントから使用権限を削除します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. Acrobat Reader DC Extensions clientオブジェクトを作成します。

   * Create a `ReaderExtensionsServiceClient` object by using its default constructor.
   * Create a `ReaderExtensionsServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLを指定するstring値をAEM Formsサービスに渡します(例： `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`)。 必ず、を指定し `?blob=mtom`ます。)
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `ReaderExtensionsServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. PDFドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、使用権限が削除された、使用権限を付与されたPDFドキュメントの保存に使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、PDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイト配列、開 `System.IO.FileStream` 始位置、ストリ `Read` ーム長を渡すことによって、バイト配列にストリームデータを設定します。
   * オブジェクト `BLOB` にバイト配列の内容をプロ `MTOM` パティに割り当てて、オブジェクトを設定します。

1. PDFドキュメントから使用権限を削除します。

   オブジェクトのメソッドを呼び出し、使用権限を付与されたPDFドキ `ReaderExtensionsServiceClient` ュメントを含むオ `removeUsageRights` ブジェクトを渡すこ `BLOB` とで、PDFドキュメントから使用権限を削除します。 このメソッドは、使用 `BLOB` 権限のないPDFドキュメントを含むオブジェクトを返します。

1. PDFドキュメントに使用権限を適用します。

   * オブジェクトを `System.IO.FileStream` 作成するには、コンストラクターを呼び出し、PDFファイルの場所を表すstring値を渡します。
   * メソッドによって返されたオブジェクトのデータ内容を格納 `BLOB` するバイト配列を作成 `removeUsageRights` します。 オブジェクトのデータメンバーの値を取得して、バ `BLOB` イト配列を `MTOM` 設定します。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.

**関連トピック**

[PDFドキュメントからの使用権限の削除](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 秘密鍵証明書情報の取得 {#retrieving-credential-information}

使用権限を付与されたPDFドキュメントに使用権限を適用するために使用された秘密鍵証明書に関する情報を取得できます。 秘密鍵証明書に関する情報を取得することで、証明書が無効になる日付などの情報を取得できます。

>[!NOTE]
>
>For more information about the Acrobat Reader DC extensions service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-2}

PDFドキュメントに使用権限を適用するために使用された秘密鍵証明書に関する情報を取得するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Acrobat Reader DC Extensions clientオブジェクトを作成します。
1. 使用権限を付与されたPDFドキュメントを取得します。
1. 秘密鍵証明書に関する情報を取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

**Acrobat Reader DC Extensionsクライアントオブジェクトの作成**

プログラムを使用してAcrobat Reader DC Extensionsサービスの操作を実行する前に、Acrobat Reader DC Extensionsサービスクライアントオブジェクトを作成する必要があります。 Java APIを使用している場合は、オブジェクトを作成し `ReaderExtensionsServiceClient` ます。 Acrobat Reader DC Extensions webサービスAPIを使用している場合は、オブジェクトを作成し `ReaderExtensionsServiceService` ます。

**使用権限を付与されたPDFドキュメントの取得**

秘密鍵証明書に関する情報を取得するには、使用権限を付与されたPDFドキュメントを取得する必要があります。 また、秘密鍵証明書のエイリアスを指定して、秘密鍵証明書に関する情報を取得することもできます。ただし、使用権限を付与された特定のPDFドキュメントに使用権限を適用するために使用された秘密鍵証明書に関する情報を取得する場合は、ドキュメントを取得する必要があります。

**秘密鍵証明書に関する情報の取得**

使用権限を付与されたPDFドキュメントを取得した後、使用権限の適用に使用された秘密鍵証明書に関する情報を取得できます。 秘密鍵証明書に関する次の情報を取得できます。

* 使用権限を付与されたPDFドキュメントを開いたときにAdobe reader内で表示されるメッセージです。
* 秘密鍵証明書が無効になる日付です。
* 秘密鍵証明書が無効な日付です。
* この権限を付与されたPDFドキュメントに設定された使用権限です。
* 秘密鍵証明書が使用された回数です。

**関連トピック**

[Java APIを使用した使用権限の削除](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[WebサービスAPIを使用した使用権限の削除](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Acrobat Reader DC ExtensionsサービスAPIクイックスタート](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Java APIを使用した秘密鍵証明書情報の取得 {#retrieve-credential-information-using-the-java-api}

Acrobat Reader DC Extensions API(Java)を使用して秘密鍵証明書情報を取得します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-reader-extensions-client.jarなどのクライアントJARファイルを含めます。

1. Acrobat Reader DC Extensions clientオブジェクトを作成します。

   コンストラク `ReaderExtensionsServiceClient` ターを使用し、接続プロパティを含むオブジェクトを渡 `ServiceClientFactory` して、オブジェクトを作成します。

1. PDFドキュメントを取得します。

   * コンストラ `java.io.FileInputStream` クターを使用し、権限を付与されたPDFドキュメントの場所を指定するstring値を渡して、権限を付与されたPDFドキュメントを表すオブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PDFドキュメントから使用権限を削除します。

   * オブジェクトのメソッドを呼び出し、使用権限を付与されたPDFドキュメントを含むオブジェクトを渡すことによって、PDFドキュメントに使用権限を適用するた `ReaderExtensionsServiceClient``getDocumentUsageRights``com.adobe.idp.Document` めに使用される秘密鍵証明書に関する情報を取得します。 このメソッドは、秘密鍵証明書 `GetUsageRightsResult` 情報を含むオブジェクトを返します。
   * オブジェクトのメソッドを呼び出して、秘密鍵証明書が無効になる `GetUsageRightsResult` 日付を取得し `getNotAfter` ます。 このメソッドは、秘密鍵 `java.util.Date` 証明書の失効日を表すオブジェクトを返します。
   * 使用権限を付与されたPDFドキュメントを開いたときにAdobe readerに表示されるメッセージを取得するには、オブジェクトのメソッド `GetUsageRightsResult` を呼び出 `getMessage` します。 このメソッドは、メッセージを表すstring値を返します。

**関連トピック**

[秘密鍵証明書情報の取得](assigning-usage-rights.md#retrieving-credential-information)

[クイックスタート（SOAPモード）:Java APIを使用した秘密鍵証明書情報の取得](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-retrieving-credential-information-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用した秘密鍵証明書情報の取得 {#retrieve-credential-information-using-the-web-service-api}

Acrobat Reader DC Extensions API（Webサービス）を使用して秘密鍵証明書情報を取得します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. Acrobat Reader DC Extensions clientオブジェクトを作成します。

   * デフォルトのコンス `ReaderExtensionsServiceClient` トラクターを使用して、オブジェクトを作成します。
   * Create a `ReaderExtensionsServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLを指定するstring値をAEM Formsサービスに渡します(例： `http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`)。 必ず、を指定し `?blob=mtom`ます。)
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `ReaderExtensionsServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. PDFドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、使用権限を付与されたPDFドキュメントの保存に使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、使用権限を付与されたPDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイト配列、開 `System.IO.FileStream` 始位置、ストリ `Read` ーム長を渡すことによって、バイト配列にストリームデータを設定します。
   * オブジェクト `BLOB` にバイト配列の内容をプロ `MTOM` パティに割り当てて、オブジェクトを設定します。

1. PDFドキュメントから使用権限を削除します。

   * オブジェクトのメソッドを呼び出し、使用権限を付与されたPDFドキュメントを含むオブジェクトを渡すことによって、PDFドキュメントに使用権限を適用するた `ReaderExtensionsServiceClient``getDocumentUsageRights``com.adobe.idp.Document` めに使用される秘密鍵証明書に関する情報を取得します。 このメソッドは、秘密鍵証明書 `GetUsageRightsResult` 情報を含むオブジェクトを返します。
   * オブジェクトのデータメンバーの値を取得して、秘密鍵証明書が無効にな `GetUsageRightsResult` った日付を取 `notAfter` 得します。 このデータメンバのデータ型はです `System.DateTime`。
   * オブジェクトのデータメンバーの値を取得して、使用権限を付与されたPDFドキュメントをAdobe readerで開いたときに表示されるメ `GetUsageRightsResult` ッセージを取 `message` 得します。 このデータメンバのデータ型は文字列です。
   * オブジェクトのデータメンバーの値を取得して、秘密鍵証明書が使用さ `GetUsageRightsResult` れた回数を取 `useCount` 得します。 このデータメンバのデータ型は整数です。

**関連トピック**

[秘密鍵証明書情報の取得](assigning-usage-rights.md#retrieving-credential-information)

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
