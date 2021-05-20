---
title: 使用権限の割り当て
seo-title: 使用権限の割り当て
description: PDFドキュメントの使用権限を適用および削除するには、Acrobat Reader DC拡張機能JavaクライアントAPIとWebサービスAPIを使用します。
seo-description: PDFドキュメントの使用権限を適用および削除するには、Acrobat Reader DC拡張機能JavaクライアントAPIとWebサービスAPIを使用します。
uuid: 8c2020df-ea3c-49fa-916f-38a458f40d2b
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9e8db506-9ace-4e1f-8a7b-c4e9b15dde7e
role: Developer
exl-id: 6af148eb-427a-4b54-9c5f-8750736882d8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '3951'
ht-degree: 7%

---

# 使用権限の割り当て{#assigning-usage-rights}

**このドキュメントのサンプルと例は、JEE上のAEM Forms環境に限られています。**

## Acrobat Reader DC Extensionsサービス{#about-the-acrobat-reader-dc-extensions-service}について

Acrobat Reader DC Extensionsサービスを使用すると、Adobe Readerの機能を拡張して、組織でインタラクティブPDFドキュメントを簡単に共有できます。 Acrobat Reader DC Extensionsサービスは、PDF 1.7を含むすべてのPDFドキュメントを完全にサポートします。Adobe Reader 7.0以降で機能します。 このサービスは、PDFドキュメントに使用権限を追加し、Adobe Readerを使用してPDFドキュメントを開いた場合に通常使用できない機能をアクティベートします。 サードパーティユーザーは、使用権限を付与されたドキュメントを使用するために、追加のソフトウェアやプラグインを必要としません。

Acrobat Reader DC Extensionsサービスを使用すると、次のタスクを実行できます。

* PDFドキュメントに使用権限を適用します。 詳しくは、[PDFドキュメントへの使用権限の適用](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)を参照してください。
* PDFドキュメントから使用権限を削除します。 詳しくは、[PDFドキュメントからの使用権限の削除](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)を参照してください。
* 秘密鍵証明書の詳細を取得します。 詳しくは、[秘密鍵証明書情報の取得](assigning-usage-rights.md#retrieving-credential-information)を参照してください。

>[!NOTE]
>
>Acrobat Reader DC Extensionsサービスについて詳しくは、『 AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)のサービスリファレンス』を参照してください。[

## PDFドキュメントへの使用権限の適用{#applying-usage-rights-to-pdf-documents}

Acrobat Reader DC Extensions Java Client APIとWebサービスを使用して、PDFドキュメントに使用権限を適用できます。 使用権限は、Acrobat ではデフォルトで利用できるが Adobe Reader では利用できない機能（フォームにコメントを追加する機能や、フォームフィールドにデータを入力してフォームを保存する機能など）に関連しています。使用権限が与えられた PDF ドキュメントは、使用権限を付与されたドキュメントと呼ばれます。使用権限を付与されたドキュメントを Adobe Reader で開いたユーザーは、そのドキュメントで有効になっている操作を実行できます。

>[!NOTE]
>
>Java APIの一部である`applyUsageRights`メソッドを使用してPDFドキュメントに使用権限を適用する場合、 `ReaderExtensionsOptionSpec`オブジェクトの`isModeFinal`パラメーターを`false`に設定できます。 その結果、フォーム処理されたカウンターが更新されず、パフォーマンスが向上します。 フォーム処理カウンターの更新を気にしない場合は、`isModeFinal`パラメーターを`false`に設定することをお勧めします。

>[!NOTE]
>
>Acrobat Reader DC Extensionsサービスについて詳しくは、『 AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)のサービスリファレンス』を参照してください。[

### 手順の概要{#summary-of-steps}

PDFドキュメントに使用権限を適用するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Acrobat Reader DC Extensionsクライアントオブジェクトを作成します。
1. PDFドキュメントを取得します。
1. 適用する使用権限を指定します。
1. PDFドキュメントに使用権限を適用します。
1. 権限を付与されたPDFドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用する場合は、プロキシファイルを必ず含めてください。

**Acrobat Reader DC Extensionsクライアントオブジェクトの作成**

プログラムによってAcrobat Reader DC ExtensionsService操作を実行するには、Acrobat Reader DC Extensions Serviceクライアントオブジェクトを作成する必要があります。 Acrobat Reader DC拡張機能Java APIを使用している場合は、`ReaderExtensionsServiceClient`オブジェクトを作成します。 Acrobat Reader DC拡張機能WebサービスAPIを使用している場合は、`ReaderExtensionsServiceService`オブジェクトを作成します。

**PDFドキュメントの取得**

使用権限を適用するには、PDFドキュメントを取得する必要があります。 権限を付与されたPDFドキュメントには、使用権限辞書が含まれています。 Adobe Readerは、このような辞書を含むドキュメントを開くと、そのドキュメントの辞書で指定された使用権限のみを有効にします。 ドキュメントに使用権限辞書が含まれていない場合、Acrobat Reader DC Extensionsサービスによって作成されます。 既に辞書が含まれている場合、Acrobat Reader DC Extensionsサービスは、指定した使用権限で既存の使用権限を上書きします。 辞書は、有効にする使用権限を指定します。 ユーザーがAdobe Readerでドキュメントを開くと、辞書で指定されている使用権限のみが許可されます。

**適用する使用権限の指定**

設定できる使用権限は、Adobe Systems Incorporatedから購入した秘密鍵証明書によって決まります。 通常、資格情報には、インタラクティブフォームに関連する使用権限など、関連する使用権限のグループを設定する権限が付与されます。 各秘密鍵証明書には、一定数の権限を付与されたPDFドキュメントを作成する権限が付与されます。 評価用の資格情報を使用すると、無制限数のドラフトドキュメントを作成できます。

>[!NOTE]
>
>秘密鍵証明書で許可されていない使用権限を割り当てようとすると、例外が発生します。

**PDFドキュメントへの使用権限の適用**

PDFドキュメントに使用権限を適用するには、使用権限の適用に使用する秘密鍵証明書のエイリアスを参照します(秘密鍵証明書は通常、AEM Formsのインストール時にインストールされます)。 また、使用権限を適用するPDFドキュメントも指定する必要があります。 秘密鍵証明書の設定について詳しくは、使用しているアプリケーションサーバー版のインストールおよびデプロイガイドを参照してください。

**権限を付与されたPDFドキュメントの保存**

Acrobat Reader DC ExtensionsサービスがPDFドキュメントに使用権限を適用した後、使用権限を付与されたPDFドキュメントをPDFファイルとして保存できます。

**関連トピック**

[Java APIを使用した使用権限の適用](assigning-usage-rights.md#apply-usage-rights-using-the-java-api)

[WebサービスAPIを使用した使用権限の適用](assigning-usage-rights.md#apply-usage-rights-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Acrobat Reader DC ExtensionsサービスAPIのクイックスタート](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Java API {#apply-usage-rights-using-the-java-api}を使用して使用権限を適用します。

Acrobat Reader DC Extensions API(Java)を使用して、PDFドキュメントに使用権限を適用します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-reader-extensions-client.jarなどのクライアントJARファイルを含めます。

1. Acrobat Reader DC Extensionsクライアントオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `ReaderExtensionsServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. PDFドキュメントを取得します。

   * コンストラクターを使用し、PDFドキュメントの場所を指定する文字列値を渡すことで、PDFドキュメントを表す`java.io.FileInputStream`オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 適用する使用権限を指定します。

   * コンストラクターを使用して、使用権限を表す`UsageRights`オブジェクトを作成します。
   * 適用する使用権限ごとに、`UsageRights`オブジェクトに属する対応するメソッドを呼び出します。 例えば、`enableFormFillIn`使用権限を追加するには、`UsageRights`オブジェクトの`enableFormFillIn`メソッドを呼び出して`true`を渡します。 （適用する各使用権限に対して、この手順を繰り返します）。

1. PDFドキュメントに使用権限を適用します。

   * コンストラクタを使用して `ReaderExtensionsOptionSpec` オブジェクトを作成します。このオブジェクトには、Acrobat Reader DC Extensionsサービスに必要な実行時オプションが含まれています。 このコンストラクタを呼び出す場合は、次の値を指定する必要があります。

      * ドキュメントに適用する使用権限を含む`UsageRights`オブジェクト。
      * 使用権限を付与されたPDFドキュメントをAdobe Reader 7.xで開いたときにユーザーに表示されるメッセージを指定するstring値です。このメッセージは、Adobe Reader 8.0では表示されません。
   * `ReaderExtensionsServiceClient`オブジェクトの`applyUsageRights`メソッドを呼び出し、次の値を渡して使用権限をPDFドキュメントに適用します。

      * 使用権限が適用されるPDFドキュメントを含む`com.adobe.idp.Document`オブジェクト。
      * 使用権限を適用できる秘密鍵証明書のエイリアスを指定するstring値。
      * 対応するパスワード値を指定する文字列値. (現在、このパラメーターは無視されます。 `null`を渡すことができます。)
   * 実行時オプションを含む`ReaderExtensionsOptionSpec`オブジェクト。

   `applyUsageRights`メソッドは、権限を付与されたPDFドキュメントを含む`com.adobe.idp.Document`オブジェクトを返します。

1. 権限を付与されたPDFドキュメントを保存します。

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が .pdf であることを確認します。
   * `com.adobe.idp.Document`オブジェクトの`copyToFile`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトの内容をファイルにコピーします（`applyUsageRights`メソッドで返された`com.adobe.idp.Document`オブジェクトを使用するようにしてください）。

**関連トピック**

[PDFドキュメントへの使用権限の適用](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[クイックスタート（SOAPモード）:Java APIを使用した使用権限の適用](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-applying-usage-rights-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#apply-usage-rights-using-the-web-service-api}を使用して使用権限を適用します。

Acrobat Reader DC Extensions API（Webサービス）を使用して、PDFドキュメントに使用権限を適用します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. Acrobat Reader DC Extensionsクライアントオブジェクトを作成します。

   * デフォルトのコンストラクターを使用して`ReaderExtensionsServiceClient`オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`ReaderExtensionsServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに指定するstring値（例えば、`http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`）を渡します。 必ず`?blob=mtom`を指定してください。)
   * `ReaderExtensionsServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値は、MTOMが使用されるようにします。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールド`ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`にAEM formsユーザー名を割り当てます。
      * 対応するパスワード値をフィールド`ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * フィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に定数値`HttpClientCredentialType.Basic`を割り当てます。
      * フィールド`BasicHttpBindingSecurity.Security.Mode`に定数値`BasicHttpSecurityMode.TransportCredentialOnly`を割り当てます。

1. PDFドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、使用権限が適用されるPDFドキュメントを保存するために使用されます。
   * コンストラクターを呼び出し、PDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得することで、バイト配列のサイズを判断できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出して、バイト配列にストリームデータを入力します。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * `BLOB`オブジェクトの`MTOM`プロパティにバイト配列の内容を割り当てて、オブジェクトを設定します。

1. 適用する使用権限を指定します。

   * コンストラクターを使用して、使用権限を表す`UsageRights`オブジェクトを作成します。
   * 適用する各使用権限に対して、値`true`を、`UsageRights`オブジェクトに属する対応するデータメンバーに割り当てます。 例えば、`enableFormFillIn`使用権限を追加するには、`true`を`UsageRights`オブジェクトの`enableFormFillIn`データメンバーに割り当てます。 （適用する各使用権限に対して、この手順を繰り返します）。

1. PDFドキュメントに使用権限を適用します。

   * コンストラクタを使用して `ReaderExtensionsOptionSpec` オブジェクトを作成します。このオブジェクトには、Acrobat Reader DC Extensionsサービスに必要な実行時オプションが含まれています。
   * `UsageRights`オブジェクトを`ReaderExtensionsOptionSpec`オブジェクトの`usageRights`データメンバーに割り当てます。
   * Adobe Readerで使用権限を付与されたPDFドキュメントを`ReaderExtensionsOptionSpec`オブジェクトの`message`データメンバーに開いたときにユーザーに表示されるメッセージを指定するstring値を割り当てます。
   * `ReaderExtensionsServiceClient`オブジェクトの`applyUsageRights`メソッドを呼び出し、次の値を渡して使用権限をPDFドキュメントに適用します。

      * 使用権限が適用されるPDFドキュメントを含む`BLOB`オブジェクト。
      * 使用権限を適用できる秘密鍵証明書のエイリアスを指定するstring値。
      * 対応するパスワード値を指定する文字列値. (現在、このパラメーターは無視されます。 `null`を渡すことができます。)
   * 実行時オプションを含む`ReaderExtensionsOptionSpec`オブジェクト。

   `applyUsageRights`メソッドは、権限を付与されたPDFドキュメントを含む`BLOB`オブジェクトを返します。

1. 権限を付与されたPDFドキュメントを保存します。

   * コンストラクターを呼び出して、`System.IO.FileStream`オブジェクトを作成します。 権限を付与されたPDFドキュメントのファイルの場所を表すstring値を渡します。
   * `applyUsageRights`メソッドで返された`BLOB`オブジェクトのデータ内容を格納するバイト配列を作成します。 `BLOB`オブジェクトの`MTOM`データメンバーの値を取得して、バイト配列を設定します。
   * コンストラクターを呼び出し、`System.IO.FileStream`オブジェクトを渡して、`System.IO.BinaryWriter`オブジェクトを作成します。
   * `System.IO.BinaryWriter`オブジェクトの`Write`メソッドを呼び出し、バイト配列を渡すことにより、バイト配列の内容をPDFファイルに書き込みます。

**関連トピック**

[PDFドキュメントへの使用権限の適用](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## PDFドキュメントからの使用権限の削除{#removing-usage-rights-from-pdf-documents}

使用権限を付与されたドキュメントから使用権限を削除できます。 使用権限を付与されたPDFドキュメントに対して他のAEM Forms操作を実行するには、使用権限を削除する必要もあります。 例えば、PDF ドキュメントに対する電子署名（または認証）は、使用権限を設定する前に実行する必要があります。したがって、権限を付与されたドキュメントに対して操作を実行する場合は、PDFドキュメントから使用権限を削除し、その他の操作（ドキュメントの電子署名など）を実行してから、ドキュメントに使用権限を再適用する必要があります。

>[!NOTE]
>
>Acrobat Reader DC Extensionsサービスについて詳しくは、『 AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)のサービスリファレンス』を参照してください。[

### 手順の概要{#summary_of_steps-1}

使用権限を付与されたPDFドキュメントから使用権限を削除するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Acrobat Reader DC Extensionsクライアントオブジェクトを作成します。
1. 権限を付与されたPDFドキュメントを取得します。
1. PDFドキュメントから使用権限を削除します。
1. PDFドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用する場合は、プロキシファイルを必ず含めてください。

**Acrobat Reader DC Extensionsクライアントオブジェクトの作成**

プログラムによってAcrobat Reader DC Extensionsサービスの操作を実行する前に、Acrobat Reader DC Extensionsサービスクライアントオブジェクトを作成する必要があります。 Java APIを使用している場合は、`ReaderExtensionsServiceClient`オブジェクトを作成します。 Acrobat Reader DC拡張機能WebサービスAPIを使用している場合は、`ReaderExtensionsServiceService`オブジェクトを作成します。

**権限を付与されたPDFドキュメントの取得**

使用権限を削除するために、権限を付与されたPDFドキュメントを取得します。

**PDFドキュメントから使用権限を削除します**

権限を付与されたPDFドキュメントを取得したら、使用権限を削除できます。 使用権限を削除すると、Adobe Reader内で表示されている間、PDFドキュメントに追加機能は含まれなくなります。

**PDFドキュメントの保存**

使用権限がなくなったPDFドキュメントをPDFファイルとして保存できます。 PDFファイルとして保存すると、PDFドキュメントをAdobe ReaderまたはAcrobatで表示できます。

**関連トピック**

[Java APIを使用した使用権限の削除](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[WebサービスAPIを使用した使用権限の削除](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Acrobat Reader DC ExtensionsサービスAPIのクイックスタート](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

[PDFドキュメントへの使用権限の適用](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

### Java API {#remove-usage-rights-using-the-java-api}を使用して使用権限を削除します。

Acrobat Reader DC Extensions API(Java)を使用して、権限を付与されたPDFドキュメントから使用権限を削除します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-reader-extensions-client.jarなどのクライアントJARファイルを含めます。

1. Acrobat Reader DC Extensionsクライアントオブジェクトを作成します。

   コンストラクターを使用し、接続プロパティを含む`ServiceClientFactory`オブジェクトを渡して、`ReaderExtensionsServiceClient`オブジェクトを作成します。

1. PDFドキュメントを取得します。

   * コンストラクターを使用してPDFドキュメントの場所を指定するstring値を渡すことで、権限を付与されたPDFドキュメントを表す`java.io.FileInputStream`オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PDFドキュメントから使用権限を削除します。

   `ReaderExtensionsServiceClient`オブジェクトの`removeUsageRights`メソッドを呼び出し、権限を付与されたPDFドキュメントを含む`com.adobe.idp.Document`オブジェクトを渡すことで、PDFドキュメントから使用権限を削除します。 このメソッドは、使用権限のないPDFドキュメントを含む`com.adobe.idp.Document`オブジェクトを返します。

1. PDFドキュメントに使用権限を適用します。

   * `java.io.File`オブジェクトを作成し、ファイル拡張子が.PDFであることを確認します。
   * `Document`オブジェクトの`copyToFile`メソッドを呼び出して、`Document`オブジェクトの内容をファイルにコピーします（`removeUsageRights`メソッドで返された`Document`オブジェクトを使用するようにしてください）。

**関連トピック**

[PDFドキュメントからの使用権限の削除](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[クイックスタート（SOAPモード）:Java APIを使用したPDFドキュメントからの使用権限の削除](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-removing-usage-rights-from-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#remove-usage-rights-using-the-web-service-api}を使用して使用権限を削除します。

Acrobat Reader DC Extensions API（Webサービス）を使用して、権限を付与されたPDFドキュメントから使用権限を削除します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. Acrobat Reader DC Extensionsクライアントオブジェクトを作成します。

   * デフォルトのコンストラクターを使用して`ReaderExtensionsServiceClient`オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`ReaderExtensionsServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに指定するstring値（例えば、`http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`）を渡します。 必ず`?blob=mtom`を指定してください。)
   * `ReaderExtensionsServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値は、MTOMが使用されるようにします。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールド`ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`にAEM formsユーザー名を割り当てます。
      * 対応するパスワード値をフィールド`ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * フィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に定数値`HttpClientCredentialType.Basic`を割り当てます。
      * フィールド`BasicHttpBindingSecurity.Security.Mode`に定数値`BasicHttpSecurityMode.TransportCredentialOnly`を割り当てます。

1. PDFドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、使用権限が削除される権限が付与されたPDFドキュメントを保存するために使用されます。
   * コンストラクターを呼び出し、PDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得することで、バイト配列のサイズを判断できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことによって、バイト配列にストリームデータを入力します。
   * `BLOB`オブジェクトの`MTOM`プロパティにバイト配列の内容を割り当てて、オブジェクトを設定します。

1. PDFドキュメントから使用権限を削除します。

   `ReaderExtensionsServiceClient`オブジェクトの`removeUsageRights`メソッドを呼び出し、権限を付与されたPDFドキュメントを含む`BLOB`オブジェクトを渡すことで、PDFドキュメントから使用権限を削除します。 このメソッドは、使用権限のないPDFドキュメントを含む`BLOB`オブジェクトを返します。

1. PDFドキュメントに使用権限を適用します。

   * コンストラクターを呼び出し、PDFファイルの場所を表す文字列値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `removeUsageRights`メソッドで返された`BLOB`オブジェクトのデータ内容を格納するバイト配列を作成します。 `BLOB`オブジェクトの`MTOM`データメンバーの値を取得して、バイト配列を設定します。
   * コンストラクターを呼び出し、`System.IO.FileStream`オブジェクトを渡して、`System.IO.BinaryWriter`オブジェクトを作成します。

**関連トピック**

[PDFドキュメントからの使用権限の削除](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 資格情報{#retrieving-credential-information}の取得

使用権限を付与されたPDFドキュメントに使用権限を適用するために使用された秘密鍵証明書に関する情報を取得できます。 秘密鍵証明書に関する情報を取得することで、証明書が無効になった日付などの情報を取得できます。

>[!NOTE]
>
>Acrobat Reader DC Extensionsサービスについて詳しくは、『 AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)のサービスリファレンス』を参照してください。[

### 手順の概要{#summary_of_steps-2}

PDFドキュメントに使用権限を適用するために使用された秘密鍵証明書に関する情報を取得するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Acrobat Reader DC Extensionsクライアントオブジェクトを作成します。
1. 権限を付与されたPDFドキュメントを取得します。
1. 秘密鍵証明書に関する情報を取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用する場合は、プロキシファイルを必ず含めてください。

**Acrobat Reader DC Extensionsクライアントオブジェクトの作成**

プログラムによってAcrobat Reader DC Extensionsサービスの操作を実行する前に、Acrobat Reader DC Extensionsサービスクライアントオブジェクトを作成する必要があります。 Java APIを使用している場合は、`ReaderExtensionsServiceClient`オブジェクトを作成します。 Acrobat Reader DC拡張機能WebサービスAPIを使用している場合は、`ReaderExtensionsServiceService`オブジェクトを作成します。

**権限を付与されたPDFドキュメントの取得**

秘密鍵証明書に関する情報を取得するには、権限を付与されたPDFドキュメントを取得する必要があります。 エイリアスを指定して、秘密鍵証明書に関する情報を取得することもできます。ただし、使用権限を特定の権限を付与されたPDFドキュメントに適用するために使用された秘密鍵証明書に関する情報を取得する場合は、ドキュメントを取得する必要があります。

**秘密鍵証明書に関する情報の取得**

使用権限を付与されたPDFドキュメントを取得したら、使用権限の適用に使用された秘密鍵証明書に関する情報を取得できます。 秘密鍵証明書に関する次の情報を取得できます。

* 権限を付与されたPDFドキュメントを開いたときにAdobe Reader内で表示されるメッセージです。
* 秘密鍵証明書が無効になる日付。
* 秘密鍵証明書が無効な日付です。
* この権限を付与されたPDFドキュメントに設定された使用権限。
* 秘密鍵証明書が使用された回数。

**関連トピック**

[Java APIを使用した使用権限の削除](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[WebサービスAPIを使用した使用権限の削除](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Acrobat Reader DC ExtensionsサービスAPIのクイックスタート](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Java API {#retrieve-credential-information-using-the-java-api}を使用して秘密鍵証明書の情報を取得します

Acrobat Reader DC Extensions API(Java)を使用して秘密鍵証明書の情報を取得します。

1. プロジェクトファイルを含めます。

   Javaプロジェクトのクラスパスに、adobe-reader-extensions-client.jarなどのクライアントJARファイルを含めます。

1. Acrobat Reader DC Extensionsクライアントオブジェクトを作成します。

   コンストラクターを使用し、接続プロパティを含む`ServiceClientFactory`オブジェクトを渡して、`ReaderExtensionsServiceClient`オブジェクトを作成します。

1. PDFドキュメントを取得します。

   * コンストラクターを使用し、権限を付与されたPDFドキュメントの場所を指定する文字列値を渡すことで、権限を付与されたPDFドキュメントを表す`java.io.FileInputStream`オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PDFドキュメントから使用権限を削除します。

   * `ReaderExtensionsServiceClient`オブジェクトの`getDocumentUsageRights`メソッドを呼び出し、権限を付与されたPDFドキュメントを含む`com.adobe.idp.Document`オブジェクトを渡すことで、PDFドキュメントに使用権限を適用するために使用される秘密鍵証明書に関する情報を取得します。 このメソッドは、秘密鍵証明書情報を含む`GetUsageRightsResult`オブジェクトを返します。
   * `GetUsageRightsResult`オブジェクトの`getNotAfter`メソッドを呼び出して、秘密鍵証明書が無効になる日付を取得します。 このメソッドは、秘密鍵証明書が無効になった日付を表す`java.util.Date`オブジェクトを返します。
   * `GetUsageRightsResult`オブジェクトの`getMessage`メソッドを呼び出して、権限を付与されたPDFドキュメントを開いたときにAdobe Readerに表示されるメッセージを取得します。 このメソッドは、メッセージを表すstring値を返します。

**関連トピック**

[秘密鍵証明書情報の取得](assigning-usage-rights.md#retrieving-credential-information)

[クイックスタート（SOAPモード）:Java APIを使用した秘密鍵証明書情報の取得](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-retrieving-credential-information-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#retrieve-credential-information-using-the-web-service-api}を使用して資格情報を取得します

Acrobat Reader DC Extensions API（Webサービス）を使用して秘密鍵証明書の情報を取得します。

1. プロジェクトファイルを含めます。

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. Acrobat Reader DC Extensionsクライアントオブジェクトを作成します。

   * デフォルトのコンストラクターを使用して`ReaderExtensionsServiceClient`オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`ReaderExtensionsServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに指定するstring値（例えば、`http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`）を渡します。 必ず`?blob=mtom`を指定してください。)
   * `ReaderExtensionsServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値は、MTOMが使用されるようにします。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールド`ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName`にAEM formsユーザー名を割り当てます。
      * 対応するパスワード値をフィールド`ReaderExtensionsServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * フィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に定数値`HttpClientCredentialType.Basic`を割り当てます。
      * フィールド`BasicHttpBindingSecurity.Security.Mode`に定数値`BasicHttpSecurityMode.TransportCredentialOnly`を割り当てます。

1. PDFドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、権限を付与されたPDFドキュメントの保存に使用されます。
   * コンストラクターを呼び出し、権限を付与されたPDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得することで、バイト配列のサイズを判断できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことによって、バイト配列にストリームデータを入力します。
   * `BLOB`オブジェクトの`MTOM`プロパティにバイト配列の内容を割り当てて、オブジェクトを設定します。

1. PDFドキュメントから使用権限を削除します。

   * `ReaderExtensionsServiceClient`オブジェクトの`getDocumentUsageRights`メソッドを呼び出し、権限を付与されたPDFドキュメントを含む`com.adobe.idp.Document`オブジェクトを渡すことで、PDFドキュメントに使用権限を適用するために使用される秘密鍵証明書に関する情報を取得します。 このメソッドは、秘密鍵証明書情報を含む`GetUsageRightsResult`オブジェクトを返します。
   * `GetUsageRightsResult`オブジェクトの`notAfter`データメンバーの値を取得して、秘密鍵証明書が無効になる日付を取得します。 このデータメンバのデータ型は`System.DateTime`です。
   * `GetUsageRightsResult`オブジェクトの`message`データメンバーの値を取得して、権限を付与されたPDFドキュメントをAdobe Readerで開いたときに表示されるメッセージを取得します。 このデータメンバーのデータ型は文字列です。
   * `GetUsageRightsResult`オブジェクトの`useCount`データメンバーの値を取得して、秘密鍵証明書が使用された回数を取得します。 このデータメンバのデータ型は整数です。

**関連トピック**

[秘密鍵証明書情報の取得](assigning-usage-rights.md#retrieving-credential-information)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
