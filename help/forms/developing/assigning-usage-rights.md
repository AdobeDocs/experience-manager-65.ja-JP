---
title: 使用権限の割り当て
seo-title: Assigning Usage Rights
description: Acrobat Reader DC エクステンション Java クライアント API と web サービス API を使用して、PDF ドキュメントに使用権限を適用したり削除したりできます。
seo-description: Use the Acrobat Reader DC extensions Java Client API and Web Service API to apply and remove usage rights from PDF documents.
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
source-wordcount: '3926'
ht-degree: 100%

---

# 使用権限の割り当て {#assigning-usage-rights}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

## Acrobat Reader DC エクステンションサービスについて {#about-the-acrobat-reader-dc-extensions-service}

Acrobat Reader DC エクステンションサービスを使用すると、Adobe Reader の機能を拡張することで、組織内でインタラクティブ PDF ドキュメントを簡単に共有できます。Acrobat Reader DC エクステンションサービスは、PDF 1.7 までのすべての PDF ドキュメントを完全にサポートします。Adobe Reader 7.0 以降で機能します。このサービスでは、PDF ドキュメントに使用権限を追加し、通常 Adobe Reader で PDF ドキュメントを開いたときに利用できない機能をアクティブにします。サードパーティユーザーは、権限を付与されたドキュメントを扱うためにソフトウェアまたはプラグインを追加する必要はありません。

Acrobat Reader DC エクステンションサービスを使用して、次のタスクを実行できます。

* 使用権限を PDF ドキュメントに適用します。詳しくは、[PDF ドキュメントへの使用権限の適用](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)を参照してください。
* 使用権限を PDF ドキュメントから削除します。詳しくは、[PDF ドキュメントへの使用権限の削除](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)を参照してください。
* 資格情報の詳細を取得します。詳しくは、[資格情報の取得](assigning-usage-rights.md#retrieving-credential-information)を参照してください。

>[!NOTE]
>
>Acrobat Reader DC エクステンションサービスについて詳しくは、[AEM Forms サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

## PDF ドキュメントへの使用権限を適用 {#applying-usage-rights-to-pdf-documents}

Acrobat Reader DC エクステンション Java クライアント API および web サービスを使用すると、PDF ドキュメントに使用権限を適用できます。使用権限は、Acrobat ではデフォルトで利用できるが Adobe Reader では利用できない機能（フォームにコメントを追加する機能や、フォームフィールドにデータを入力してフォームを保存する機能など）に関連しています。使用権限が与えられた PDF ドキュメントは、使用権限を付与されたドキュメントと呼ばれます。使用権限を付与されたドキュメントを Adobe Reader で開いたユーザーは、そのドキュメントで有効になっている操作を実行できます。

>[!NOTE]
>
>`applyUsageRights` メソッド（Java API の一部）を使用して PDF ドキュメントに使用権限を適用する場合、`ReaderExtensionsOptionSpec` オブジェクトの `isModeFinal` パラメーターを `false` に設定します。その結果、フォーム処理カウンターが更新されず、パフォーマンスが向上します。フォーム処理カウンターの更新を気にしなければ、`isModeFinal` パラメータを `false` に設定することをお勧めします。

>[!NOTE]
>
>Acrobat Reader DC エクステンションサービスについて詳しくは、[AEM Forms サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary-of-steps}

使用権限を PDF ドキュメントに適用するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. Acrobat Reader DC エクステンションのクライアントオブジェクトを作成します。
1. PDF ドキュメントを取得します。
1. 適用する使用権限を指定します。
1. 使用権限を PDF ドキュメントに適用します。
1. 権限が付与された PDF ドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めるようにします。

**Acrobat Reader DC エクステンションのクライアントオブジェクトを作成**

プログラムによって Acrobat Reader DC エクステンションサービスの操作を実行するには、Acrobat Reader DC エクステンションサービスのクライアントオブジェクトを作成する必要があります。Acrobat Reader DC エクステンション Java API を使用している場合は、`ReaderExtensionsServiceClient` オブジェクトを作成します。Acrobat Reader DC エクステンション web サービス API を使用している場合は、`ReaderExtensionsServiceService` オブジェクトを作成します。

**PDF ドキュメントを取得**

使用権限を適用するには、PDF ドキュメントを取得する必要があります。権限が付与された PDF ドキュメントには、使用権限ディクショナリが含まれています。Adobe Reader がそのようなディクショナリを含むドキュメントを開くと、そのドキュメントに対してのみディクショナリで指定された使用権限が有効になります。ドキュメントに使用権限ディクショナリが含まれていない場合、Acrobat Reader DC エクステンションサービスは使用権限ディクショナリを作成します。既にディクショナリが含まれている場合、Acrobat Reader DC エクステンションサービスは、指定した使用権限で既存の使用権限を上書きします。ディクショナリは、有効にする使用権限を指定します。ユーザーが Adobe Reader でドキュメントを開くと、ディクショナリで指定されている使用権限のみが許可されます。

**適用する使用権限を指定**

設定できる使用権限は、Adobe Systems Inc で購入した資格によって決まります。通常、資格情報は、インタラクティブフォームに関連する使用権限など、関連する使用権限のグループを設定する権限が付与されます。各資格情報は、一定数の権限が付与された PDF ドキュメントを作成する権限を付与します。評価資格情報を使用すると、無制限の数のドラフトドキュメントを作成する権限が付与されます。

>[!NOTE]
>
>証明書で許可されていない使用権限を割り当てようとすると、例外が発生します。

**PDF ドキュメントに使用権限を適用**

PDF ドキュメントに使用権限を適用するには、使用権限の適用に使用している資格情報のエイリアスを参照します（通常、資格情報は AEM Forms のインストール時にインストールされます）。また、使用権限を適用する PDF ドキュメント を指定する必要があります。資格情報の設定に関する情報については、アプリケーションサーバーのインストールとデプロイのガイドを参照してください。

**権限が付与された PDF ドキュメントを保存**

Acrobat Reader DC エクステンションサービスが PDF ドキュメントに使用権限を適用したら、権限が付与された PDF ドキュメントを PDF ファイルとして保存できます。

**関連トピック**

[Java API を使用して使用権限を適用](assigning-usage-rights.md#apply-usage-rights-using-the-java-api)

[Web サービス API を使用して使用権限を適用](assigning-usage-rights.md#apply-usage-rights-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Acrobat Reader DC Extensions サービス API クイックスタート](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Java API を使用して使用権限を適用 {#apply-usage-rights-using-the-java-api}

Acrobat Reader DC エクステンション API（Java）を使用して、PDF ドキュメントに使用権限を適用します。

1. プロジェクトファイルを含める

   adobe-livecycle-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. Acrobat Reader DC エクステンションのクライアントオブジェクトを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `ReaderExtensionsServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. PDF ドキュメントを取得します。

   * コンストラクターを使用し、PDF ドキュメントの場所を指定する文字列値を渡して、PDF ドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。
   * `com.adobe.idp.Document` オブジェクトを作成するには、コンストラクタを使用して、`java.io.FileInputStream` オブジェクトを渡します。

1. 適用する使用権限を指定します。

   * コンストラクターを使用して、使用権限を表す `UsageRights` オブジェクトを作成します。
   * 適用する使用権限ごとに、`UsageRights` オブジェクトに属する対応するメソッドを呼び出します。例えば、`enableFormFillIn` 使用権限を追加するには、`UsageRights` オブジェクトの `enableFormFillIn` メソッドを呼び出して、`true` を渡します。（適用する各使用権限に対して、この手順を繰り返します）。

1. 使用権限を PDF ドキュメントに適用します。

   * コンストラクタを使用して `ReaderExtensionsOptionSpec` オブジェクトを作成します。このオブジェクトには、Acrobat Reader DC エクステンションサービスで必要な実行時オプションが含まれています。このコンストラクターを呼び出す場合は、次の値を指定する必要があります。

      * ドキュメントに適用する使用権限を含む `UsageRights` オブジェクト。
      * Adobe Reader 7.x で権限が付与された PDF ドキュメントを開く際にユーザーに表示されるメッセージを指定する文字列値。このメッセージは、Adobe Reader 8.0 では表示されません。
   * 使用権限を PDF ドキュメントに適用するには、`ReaderExtensionsServiceClient` オブジェクトの `applyUsageRights` メソッドを呼び出して、次の値を渡してください。

      * 使用権限が適用される PDF ドキュメントを含む `com.adobe.idp.Document` オブジェクトです。
      * 使用権限を適用できる証明書のエイリアスを指定する文字列値です。
      * 対応するパスワード値を指定する文字列値です。（現在、このパラメーターは無視されます。`null` を渡すことができます。）
   * 実行時オプションを含む `ReaderExtensionsOptionSpec` オブジェクトです。

   `applyUsageRights` メソッドは、権限が付与された PDF ドキュメントを含む `com.adobe.idp.Document` オブジェクト返します。

1. 権限が付与された PDF ドキュメントを保存します。

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が .pdf であることを確認します。
   * `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを呼び出して、`com.adobe.idp.Document` オブジェクトのコンテンツをファイルにコピーします（`applyUsageRights` メソッドによって返された `com.adobe.idp.Document` オブジェクトを必ず使用してください）。

**関連トピック**

[PDF ドキュメントへの使用権限を適用](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[クイックスタート（SOAP モード）：Java API を使用した使用権限の適用](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-applying-usage-rights-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用して使用権限を適用 {#apply-usage-rights-using-the-web-service-api}

Acrobat Reader DC Extensions API（web サービス）を使用することにより、PDF ドキュメントに使用権限を適用してください。

1. プロジェクトファイルを含めます。

   MTOM を使用する Microsoft .NET プロジェクトを作成します。WSDL 定義 `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1` を使用するようにします。

   >[!NOTE]
   >
   >`localhost` を AEM Forms をホストするサーバーの IP アドレスに置き換えます。

1. Acrobat Reader DC エクステンションのクライアントオブジェクトを作成します。

   * デフォルトのコンストラクタを使用して `ReaderExtensionsServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクタを使用して `ReaderExtensionsServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`。必ず `?blob=mtom` を指定します）。
   * `ReaderExtensionsServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` フィールドを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
      * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` をフィールド `BasicHttpBindingSecurity.Security.Mode` に割り当てます。

1. PDF ドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB` オブジェクトは、使用権限が適用される PDF ドキュメントを保存するために使用されます。
   * コンストラクターを呼び出し、PDF ドキュメントのファイルの場所とファイルを開くモードを表す文字列値を渡して、`System.IO.FileStream` オブジェクトを作成します。
   * `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することでバイト配列のサイズを決定することができます。
   * `System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出して、バイト配列にストリームデータを入力します。読み取り対象のバイト配列、開始位置、ストリーム長を渡します。
   * `MTOM` プロパティにバイト配列のコンテンツを割り当てて、`BLOB` オブジェクトを入力します。

1. 適用する使用権限を指定します。

   * コンストラクタを使用して、使用権限を表す `UsageRights` オブジェクトを作成します。
   * 適用する使用権限ごとに、`UsageRights` オブジェクトに属し、対応するデータメンバーに値 `true` を割り当てます。例えば、`enableFormFillIn` 使用権限を追加するには、`true` を `UsageRights` オブジェクトの `enableFormFillIn` データメンバーに割り当てます。（適用する各使用権限に対して、この手順を繰り返します）。

1. 使用権限を PDF ドキュメントに適用します。

   * コンストラクタを使用して `ReaderExtensionsOptionSpec` オブジェクトを作成します。このオブジェクトには、Acrobat Reader DC Extensions サービスで必要な実行時オプションが含まれています。
   * `UsageRights` オブジェクトを `ReaderExtensionsOptionSpec` オブジェクトの `usageRights` データメンバーに割り当てます。
   * Adobe Reader で権限を付与された PDF ドキュメントを開く際に、ユーザーに表示されるメッセージを指定する文字列値を `ReaderExtensionsOptionSpec` オブジェクトの `message` データメンバーに割り当てます。
   * 使用権限を PDF ドキュメントに適用するには、`ReaderExtensionsServiceClient` オブジェクトの `applyUsageRights` メソッドを呼び出して、次の値を渡します。

      * 使用権限が適用される PDF ドキュメントを含む `BLOB` オブジェクトです。
      * 使用権限を適用できる証明書のエイリアスを指定する文字列値です。
      * 対応するパスワード値を指定する文字列値です。（現在、このパラメーターは無視されます。`null` を渡すことができます。）
   * 実行時オプションを含む `ReaderExtensionsOptionSpec` オブジェクトです。

   `applyUsageRights` メソッドは、権限が付与された PDF ドキュメントを含む `BLOB` オブジェクト返します。

1. 権限が付与された PDF ドキュメントを保存します。

   * コンストラクタを呼び出して `System.IO.FileStream` オブジェクトを作成します。権限が付与された PDF ドキュメントのファイルの場所を表す文字列値を渡します。
   * `applyUsageRights` メソッドが返した `BLOB` オブジェクトのデータコンテンツを格納するバイト配列を作成します。`BLOB` オブジェクトの `MTOM` データメンバーの値を取得して、バイト配列を生成します。
   * コンストラクターを使用して `System.IO.BinaryWriter` オブジェクトを渡すことによって、`System.IO.FileStream` オブジェクトを作成します。
   * `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを呼び出して、バイト配列を渡すことによって、バイト配列の内容を PDF ファイルに書き込みます。

**関連トピック**

[PDF ドキュメントへの使用権限を適用](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## PDF ドキュメントから使用権限を削除 {#removing-usage-rights-from-pdf-documents}

権限を付与されたドキュメントから使用権限を削除できます。ドキュメントに対してその他の AEM Forms の操作を実行するには、権限を付与された PDF ドキュメントから使用権限を削除する必要があります。例えば、PDF ドキュメントに対する電子署名（または認証）は、使用権限を設定する前に実行する必要があります。したがって、権限を付与されたドキュメントに対して操作を行う場合、その PDF ドキュメントから使用権限を削除し、ドキュメントへのデジタル署名など、その他の操作を行った後にドキュメントに対して使用権限を再び適用してください。

>[!NOTE]
>
>Acrobat Reader DC Extensions サービスに関する詳細は、[AEM Forms サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary_of_steps-1}

権限を付与された PDF ドキュメントから使用権限を削除するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. Acrobat Reader DC エクステンションのクライアントオブジェクトを作成します。
1. 権限付き PDF ドキュメントを取得します。
1. 使用権限を PDF ドキュメントから削除します。
1. PDF ドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めるようにします。

**Acrobat Reader DC Extensions のクライアントオブジェクトを作成**

Acrobat Reader DC エクステンションサービスの操作をプログラムで実行する前に、Acrobat Reader DC エクステンションサービスのクライアントオブジェクトを作成する必要があります。Java API を使用している場合は、`ReaderExtensionsServiceClient` オブジェクトを作成してください。Acrobat Reader DC Extensions web サービス API を使用している場合は、`ReaderExtensionsServiceService` オブジェクトを作成してください。

**権限が付与された PDF ドキュメントを取得**

使用権限を削除するために、権限を付与された PDF ドキュメントを取得します。

**使用権限を PDF ドキュメントから削除**

権限を付与された PDF ドキュメントを取得したら、使用権限を削除できます。使用権限を削除すると、PDF ドキュメントを Adobe Reader 内で表示する間、機能は追加されません。

**PDF ドキュメントを保存**

使用権限を含まない PDF ドキュメントは、PDF ファイルとして保存できます。PDF ドキュメントを PDF ファイルとして保存すると、Adobe Reader または Acrobat で表示できます。

**関連トピック**

[Java API を使用して使用権限を削除する](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[Web サービス API を使用して使用権限を削除する](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Acrobat Reader DC Extensions サービス API クイックスタート](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

[PDF ドキュメントへの使用権限を適用](assigning-usage-rights.md#applying-usage-rights-to-pdf-documents)

### Java API を使用して使用権限を削除する {#remove-usage-rights-using-the-java-api}

Acrobat Reader DC Extensions API（Java）を使用して、権限を付与された PDF ドキュメントから使用権限を削除します。

1. プロジェクトファイルを含めます。

   adobe-livecycle-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. Acrobat Reader DC エクステンションのクライアントオブジェクトを作成します。

   `ReaderExtensionsServiceClient` オブジェクトを作成するには、それ自身のコンストラクタを使用し、接続プロパティを含む `ServiceClientFactory` オブジェクトを渡します。

1. PDF ドキュメントを取得します。

   * `java.io.FileInputStream` オブジェクト（権限を付与された PDF ドキュメントを表す）を作成するには、それ自身のコンストラクタを使用し、PDFドキュメントの場所を指定する文字列値を渡します。
   * `com.adobe.idp.Document` オブジェクトを作成するには、それ自身のコンストラクタを使用し、`java.io.FileInputStream` オブジェクトを渡します。

1. 使用権限を PDF ドキュメントから削除します。

   `ReaderExtensionsServiceClient` オブジェクトの `removeUsageRights` メソッドを呼び出し、権限が付与された PDF ドキュメントを含む `com.adobe.idp.Document` オブジェクトを渡すことによって、使用権限を PDF ドキュメントから削除します。このメソッドは、使用権限のない PDF ドキュメントを含む `com.adobe.idp.Document` オブジェクトを返します。

1. 使用権限を PDF ドキュメントに適用します。

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が .pdf であることを確認します。
   * `Document` オブジェクトの `copyToFile` メソッドを呼び出して、 `Document` オブジェクトのコンテンツをファイルにコピーします。この際に必ず、`removeUsageRights` メソッドが返した `Document` オブジェクトを使ってください。

**関連トピック**

[PDF ドキュメントから使用権限を削除](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[クイックスタート（SOAP モード）：Java API を使用した PDF ドキュメントからの使用権限の削除](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-removing-usage-rights-from-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用して使用権限を削除する {#remove-usage-rights-using-the-web-service-api}

Acrobat Reader DC Extensions API（Web サービス）を使用して、権限を付与された PDF ドキュメントから使用権限を削除します。

1. プロジェクトファイルを含めます。

   MTOM を使用する Microsoft .NET プロジェクトを作成します。WSDL 定義 `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1` を使用するようにします。

   >[!NOTE]
   >
   >`localhost` を AEM Forms をホストするサーバーの IP アドレスに置き換えます。

1. Acrobat Reader DC エクステンションのクライアントオブジェクトを作成します。

   * デフォルトのコンストラクタを使用して `ReaderExtensionsServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクタを使用して `ReaderExtensionsServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`。必ず `?blob=mtom` を指定します）。
   * `ReaderExtensionsServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` フィールドを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
      * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` をフィールド `BasicHttpBindingSecurity.Security.Mode` に割り当てます。

1. PDF ドキュメントを取得します。

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB` オブジェクトは、使用権限が削除された権限付き PDF ドキュメントを保存するために使用されます。
   * `System.IO.FileStream` オブジェクトを作成するには、コンストラクターを呼び出し、PDF ドキュメントのファイルの場所を表す文字列値とファイルを開くモードを渡します。
   * `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することで、バイト配列のサイズを決定できます。
   * バイト配列にストリームデータを入力するには、`System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出し、バイト配列、開始位置、読み取るストリーム長を渡します。
   * `MTOM` プロパティにバイト配列の内容を割り当てることで、`BLOB` オブジェクトにデータを入力します。

1. 使用権限を PDF ドキュメントから削除します。

   `ReaderExtensionsServiceClient` オブジェクトの `removeUsageRights` メソッドを呼び出し、権限が付与された PDF ドキュメントを含む `BLOB` オブジェクトを渡すことによって、使用権限を PDF ドキュメントから削除します。このメソッドは、使用権限のない PDF ドキュメントを含む `BLOB` オブジェクトを返します。

1. 使用権限を PDF ドキュメントに適用します。

   * `System.IO.FileStream` オブジェクトを作成するには、コンストラクタを呼び出し、PDF ファイルの場所を表す文字列値を渡します。
   * `removeUsageRights` メソッドで返された `BLOB` オブジェクトのデータコンテンツを格納するバイト配列を作成します。`BLOB` オブジェクトの `MTOM` データメンバーの値を取得して、バイト配列を生成します。
   * `System.IO.BinaryWriter` オブジェクトを作成するには、コンストラクタを呼び出して、`System.IO.FileStream` オブジェクトを渡します。

**関連トピック**

[PDF ドキュメントから使用権限を削除](assigning-usage-rights.md#removing-usage-rights-from-pdf-documents)

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 資格情報の取得 {#retrieving-credential-information}

権限付き PDF ドキュメントに使用権限を適用するために使用された資格に関する情報を取得できます。資格に関する情報を取得することで、証明書が無効になった日付などの情報を取得できます。

>[!NOTE]
>
>Acrobat Reader DC エクステンションサービスに関する詳細は、『[AEM Forms サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順の概要 {#summary_of_steps-2}

使用権限を PDF ドキュメントに適用するために使用された資格に関する情報を取得するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. Acrobat Reader DC エクステンションのクライアントオブジェクトを作成します。
1. 権限付き PDF ドキュメントを取得します。
1. 資格に関する情報を取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めるようにします。

**Acrobat Reader DC Extensions のクライアントオブジェクトを作成**

Acrobat Reader DC エクステンションサービスの操作をプログラムで実行する前に、Acrobat Reader DC エクステンションサービスのクライアントオブジェクトを作成する必要があります。Java API を使用している場合は、`ReaderExtensionsServiceClient` オブジェクトを作成してください。Acrobat Reader DC Extensions web サービス API を使用している場合は、`ReaderExtensionsServiceService` オブジェクトを作成してください。

**権限付き PDF ドキュメントを取得**

資格に関する情報を取得するには、権限付き PDF ドキュメントを取得する必要があります。エイリアスを指定して、資格に関する情報を取得することもできます。ただし、使用権限を特定の権限付き PDF ドキュメントに適用するために使用された資格に関する情報を取得する場合は、ドキュメントを取得する必要があります。

**資格に関する情報の取得**

権限付き PDF ドキュメントを取得したら、使用権限を適用するために使用された資格に関する情報を取得できます。資格に関する次の情報を取得できます。

* 権限を持つ PDF ドキュメントを開く際に、Adobe Reader 内で表示されるメッセージです。
* 資格が無効になった後の日付です。
* 資格が無効になる前の日付です。
* この権限を持つ PDF ドキュメントに設定された使用権限です。
* 秘密鍵証明書が使用された回数。

**関連トピック**

[Java API を使用して使用権限を削除する](assigning-usage-rights.md#remove-usage-rights-using-the-java-api)

[Web サービス API を使用して使用権限を削除する](assigning-usage-rights.md#remove-usage-rights-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Acrobat Reader DC Extensions サービス API クイックスタート](/help/forms/developing/acrobat-reader-dc-extensions-service.md#acrobat-reader-dc-extensions-service-java-api-quick-start-soap)

### Java API を使用した秘密鍵証明書情報の取得 {#retrieve-credential-information-using-the-java-api}

Acrobat Reader DC Extensions API（Java）を使用して、秘密鍵証明書情報を取得します。

1. プロジェクトファイルを含めます。

   adobe-livecycle-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. Acrobat Reader DC エクステンションのクライアントオブジェクトを作成します。

   `ReaderExtensionsServiceClient` オブジェクトを作成するには、それ自身のコンストラクタを使用し、接続プロパティを含む `ServiceClientFactory` オブジェクトを渡します。

1. PDF ドキュメントを取得します。

   * 権限が付与された PDF ドキュメントを表す `java.io.FileInputStream` オブジェクトを作成するには、それ自身のコンストラクタを使用し、権限が付与された PDF ドキュメントの場所を指定する文字列値を渡します。
   * `com.adobe.idp.Document` オブジェクトを作成するには、それ自身のコンストラクタを使用し、`java.io.FileInputStream` オブジェクトを渡します。

1. 使用権限を PDF ドキュメントから削除します。

   * `ReaderExtensionsServiceClient` オブジェクトの `getDocumentUsageRights` メソッドを呼び出し、使用権限を付与された PDF ドキュメントを含む `com.adobe.idp.Document` オブジェクトを渡すことによって、PDF ドキュメントに使用権限を適用するために使用される、秘密鍵証明書に関する情報を取得します。このメソッドは、秘密鍵証明書情報を含む `GetUsageRightsResult` オブジェクトを返します。
   * `GetUsageRightsResult` オブジェクトの `getNotAfter` メソッドを呼び出して、秘密鍵証明書が有効でなくなった日付を取得します。このメソッドは、 `java.util.Date` 秘密鍵証明書が有効でなくなる日付を表すオブジェクトを返します。
   * `GetUsageRightsResult` オブジェクトの `getMessage` メソッドを呼び出して、権限を付与された PDF ドキュメントが開かれたときに、Adobe Reader に表示されるメッセージを取得します。このメソッドは、メッセージを表す文字列値を返します。

**関連トピック**

[資格情報の取得](assigning-usage-rights.md#retrieving-credential-information)

[クイックスタート（SOAP モード）：Java API を使用した秘密鍵証明書情報の取得](/help/forms/developing/acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-retrieving-credential-information-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用して秘密鍵証明書に関する情報を取得 {#retrieve-credential-information-using-the-web-service-api}

Acrobat Reader DC Extensions API（Web サービス）を使用して秘密鍵証明書に関する情報を取得します。

1. プロジェクトファイルを含めます。

   MTOM を使用する Microsoft .NET プロジェクトを作成します。WSDL 定義 `http://localhost:8080/soap/services/ReaderExtensionsService?WSDL&lc_version=9.0.1` を使用するようにします。

   >[!NOTE]
   >
   >`localhost` を AEM Forms をホストするサーバーの IP アドレスに置き換えます。

1. Acrobat Reader DC エクステンションのクライアントオブジェクトを作成します。

   * デフォルトのコンストラクターを使用して `ReaderExtensionsServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して `ReaderExtensionsServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/ReaderExtensionsService?blob=mtom`。必ず `?blob=mtom` を指定します）。
   * `ReaderExtensionsServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` フィールドを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `ReaderExtensionsServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `ReaderExtensionsServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
      * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` をフィールド `BasicHttpBindingSecurity.Security.Mode` に割り当てます。

1. PDF ドキュメントを取得します。

   * コンストラクターを使用して `BLOB` オブジェクトを作成します。`BLOB` オブジェクトは、権限を持つ PDF ドキュメントの保存に使用されます。
   * コンストラクターを呼び出し、権限付き PDF ドキュメントのファイルの場所とファイルを開くモードを表す文字列値を渡すことによって、`System.IO.FileStream` オブジェクトを作成します。
   * `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することで、バイト配列のサイズを決定できます。
   * バイト配列にストリームデータを入力するには、`System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出し、バイト配列、開始位置、読み取るストリーム長を渡します。
   * `MTOM` プロパティにバイト配列の内容を割り当てることで、`BLOB` オブジェクトにデータを入力します。

1. 使用権限を PDF ドキュメントから削除します。

   * `ReaderExtensionsServiceClient` オブジェクトの `getDocumentUsageRights` メソッドを呼び出し、権限付き PDF ドキュメントを含む `com.adobe.idp.Document` オブジェクトを渡すことによって、使用権限を PDF ドキュメントに適用するのに使用する資格情報を取得します。このメソッドは、資格情報を含む `GetUsageRightsResult` オブジェクトを返します。
   * `GetUsageRightsResult` オブジェクトの `notAfter` データメンバーの値を取得して、資格情報の有効期限日を取得します。このデータメンバーのデータタイプは `System.DateTime` です。
   * `GetUsageRightsResult`オブジェクトの`message`データメンバーの値を取得して、Adobe Reader で権限付き PDF ドキュメントを開いたときに表示されるメッセージを取得します。このデータメンバーのデータタイプは文字列です。
   * `GetUsageRightsResult`オブジェクトの`useCount`データメンバーの値を取得して、資格情報が使用された回数を取得します。このデータメンバーのデータタイプは整数です。

**関連トピック**

[資格情報の取得](assigning-usage-rights.md#retrieving-credential-information)

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
