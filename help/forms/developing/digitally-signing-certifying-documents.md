---
title: デジタル署名と認証ドキュメント
seo-title: デジタル署名と認証ドキュメント
description: 'null'
seo-description: 'null'
uuid: 6331de8a-2a9c-45bf-89d2-29f1ad5cc856
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 42de04bf-25e4-4478-a411-38671ed871ae
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '16977'
ht-degree: 8%

---


# デジタル署名と認証ドキュメント {#digitally-signing-and-certifying-documents}

**Signatureサービスについて**

Signatureサービスを使用すると、組織で配布および受信するAdobe PDFドキュメントのセキュリティとプライバシーを保護できます。 このサービスでは、電子署名と認証を使用して、意図した受信者だけがドキュメントを変更できるようにします。 セキュリティ機能はドキュメント自体に適用されるので、ドキュメントはライフサイクル全体にわたって安全で制御された状態を保ちます。 ドキュメントは、ファイアウォールの外部、オフラインでダウンロードされた場合、および組織に送り返された場合に、セキュリティで保護された状態のままとなります。

>[!NOTE]
>
>PDFドキュメントへの署名など、特定の操作が呼び出されたときに呼び出されるSignatureサービス用のカスタム署名ハンドラーを作成できます。

**署名フィールド名**

一部のSignatureサービス操作では、操作を実行する署名フィールドの名前を指定する必要があります。 例えば、PDFドキュメントに署名する場合、署名する署名フィールドの名前を指定します。 署名フィールドのフルネームが次のようになるとし `form1[0].Form1[0].SignatureField1[0]`ます。 代わりに、を指定 `SignatureField1[0]` でき `form1[0].Form1[0].SignatureField1[0]`ます。

競合が原因でSignatureサービスが誤ったフィールドに署名する（または、署名フィールド名を必要とする別の操作を実行する）場合があります。 この競合は、同じPDFドキュメント内の複数の場所に名前が表示さ `SignatureField1[0]` れた結果です。 例えば、という名前の2つの署名フィールドが含まれ、かつ指定したPDFドキュメント `form1[0].Form1[0].SignatureField1[0]` があると `form1[0].Form1[0].SubForm1[0].SignatureField1[0]` し `SignatureField1[0]`ます。 この場合、Signatureサービスは、ドキュメント内のすべての署名フィールドを反復する際に、検出された最初の署名フィールドに署名します。

1つのPDFドキュメント内に複数の署名フィールドがある場合は、署名フィールドの完全な名前を指定することをお勧めします。 つまり、の `form1[0].Form1[0].SignatureField1[0]`代わりにを指定し `SignatureField1[0]`ます。

Signatureサービスを使用して、次のタスクを実行できます。

* PDFドキュメント追加の電子署名フィールドを削除します。 (署名フィールドの [追加を参照](digitally-signing-certifying-documents.md#adding-signature-fields))。
* PDFドキュメント内の署名フィールドの名前を取得します。 (署名フィールド名の [取得を参照](digitally-signing-certifying-documents.md#retrieving-signature-field-names))。
* 署名フィールドを変更します。 (Modifying Signature Fieldsを参照 [](digitally-signing-certifying-documents.md#modifying-signature-fields))。
* PDFドキュメントへのデジタル署名。 (See [Digitally Signing PDF Documents](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)
* PDFドキュメントを認証します。 (See [Certifying PDF Documents](digitally-signing-certifying-documents.md#certifying-pdf-documents).)
* PDFドキュメント内の電子署名を検証します。 (デジタル署名の [検証を参照](digitally-signing-certifying-documents.md#verifying-digital-signatures))。
* PDFドキュメント内のすべての電子署名を検証します。 (See [Verifying Multiple Digital Signatures](digitally-signing-certifying-documents.md#verifying-digital-signatures).)
* 署名フィールドから電子署名を削除します。 (電子署名の [削除を参照](digitally-signing-certifying-documents.md#removing-digital-signatures))。

>[!NOTE]
>
>For more information about the Signature service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)..

## 署名フィールドの追加 {#adding-signature-fields}

電子署名は、署名のグラフィック表現を含むフォームフィールドである署名フィールドに表示されます。 署名フィールドは、表示または非表示に設定することができます。署名者は、既存の署名フィールドを使用することも、プログラムを使用して署名フィールドを追加することもできます。 どちらの場合においても、PDF ドキュメントに署名できるようにするには、署名フィールドが存在している必要があります。

プログラムによって署名フィールドを追加するには、Signature サービス Java API や 署名 Web サービス API を使用します。1つのPDFドキュメントに複数の署名フィールドを追加できます。 ただし、各署名フィールド名は一意である必要があります。

>[!NOTE]
>
>一部のPDFドキュメントタイプでは、プログラムによって署名フィールドを追加できません。 Signatureサービスと署名フィールドの追加について詳しくは、『AEM Forms向け [サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順の概要 {#summary-of-steps}

署名フィールドをPDFドキュメントに追加するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. 署名クライアントを作成します。
1. 署名フィールドが追加されるPDFドキュメントを取得します。
1. 追加署名フィールドです。
1. PDFドキュメントをPDFファイルとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(AEM FormsがJBossにデプロイされている場合に必要)
* jbossall-client.jar(AEM FormsがJBossにデプロイされている場合に必要)

**署名クライアントの作成**

プログラムを使用してSignatureサービスの操作を実行する前に、Signatureサービスクライアントを作成する必要があります。

**署名フィールドが追加されたPDFドキュメントの取得**

署名フィールドを追加するPDFドキュメントを取得する必要があります。

**追加署名フィールド**

署名フィールドをPDFドキュメントに正しく追加するには、署名フィールドの場所を識別する座標値を指定します。 （非表示の署名フィールドを追加する場合、これらの値は不要です）。 また、署名フィールドに署名が適用された後にロックするPDFドキュメントのフィールドを指定することもできます。

**PDFドキュメントをPDFファイルとして保存**

SignatureサービスがPDFドキュメントに署名フィールドを追加した後、ドキュメントをPDFファイルとして保存して、AcrobatまたはAdobe Readerで開くことができるようにすることができます。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDFドキュメントへのデジタル署名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### Java APIを追加使用した署名フィールド {#add-signature-fields-using-the-java-api}

署名API追加 (Java)を使用した署名フィールド：

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-signatures-client.jarなどのクライアントJARファイルを含めます。

1. 署名クライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `SignatureServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 署名フィールドが追加されたPDFドキュメントの取得

   * 署名フィールドの追加先のPDFドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。そのためには、コンストラクターを使用し、PDFドキュメントの場所を指定するstring値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 追加署名フィールド

   * コンストラクターを使用して、署名フィールドの場所を指定する `PositionRectangle` オブジェクトを作成します。 コンストラクタ内で、座標値を指定します。
   * 必要に応じて、電子署名が署名フィールドに適用されたときにロックされるフィールドを指定する `FieldMDPOptions` オブジェクトを作成します。
   * オ追加ブジェクトの `SignatureServiceClient``addSignatureField` メソッドを呼び出し、次の値を渡すことによって、PDFドキュメントに署名フィールドを割り当てます。

      * A `com.adobe.idp`. `Document` 署名フィールドを追加するPDFドキュメントを表すオブジェクトです。
      * 署名フィールドの名前を指定するstring値です。
      * 署名フィールドを追加するページ番号を表す `java.lang.Integer` 値です。
      * 署名フィールドの場所を指定する `PositionRectangle` オブジェクトです。
      * 電子署名が署名フィールドに適用された後にロックされるPDFドキュメント内のフィールドを指定する `FieldMDPOptions` オブジェクトです。 このパラメーターの値はオプションで、渡すことができ `null`ます。
   * 様々な実行時値を指定する `PDFSeedValueOptions` オブジェクト。 このパラメーターの値はオプションで、渡すことができ `null`ます。

      この `addSignatureField` メソッドは、aを返し `com.adobe.idp`ます。 `Document` 署名フィールドが含まれるPDFドキュメントを表すオブジェクトです。
   >[!NOTE]
   >
   >この `SignatureServiceClient` オブジェクトの `addInvisibleSignatureField` メソッドを呼び出して、非表示の署名フィールドを追加できます。

1. PDFドキュメントをPDFファイルとして保存

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が .pdf であることを確認します。
   * を呼び出し `com.adobe.idp`ます。 `Document` オブジェクトの `copyToFile` メソッドを使用して、オブジェクトの内容をフ `Document` ァイルにコピーします。 を必ず使用してくだ `com.adobe.idp`さい。 `Document` メソッドによって返されたオブジェクト `addSignatureField` 。

**関連トピック**

[SignatureサービスAPIのクイック開始](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

### webサ追加ービスAPIを使用した署名フィールド {#add-signature-fields-using-the-web-service-api}

署名API（Webサービス）を使用して署名フィールドを追加するには：

1. プロジェクトファイルを含める

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >サーバーホスト `localhost` AEM FormsのIPアドレスに置き換えます。

1. 署名クライアントの作成

   * Create a `SignatureServiceClient` object by using its default constructor.
   * Create a `SignatureServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/SignatureService?WSDL`)に渡すstring値を渡します。 属性を使用する必要はありません `lc_version` 。 この属性は、サービス参照を作成する場合に使用されます)。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `SignatureServiceClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールドにAEM formsのユーザー名を割り当て `SignatureServiceClient.ClientCredentials.UserName.UserName`ます。
      * 対応するパスワード値をフィールドに割り当て `SignatureServiceClient.ClientCredentials.UserName.Password`ます。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当て `BasicHttpBindingSecurity.Security.Mode`ます。

1. 署名フィールドが追加されたPDFドキュメントの取得

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、署名フィールドを含むPDFドキュメントを保存するために使用されます。
   * コンストラクターを呼び出し、PDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
   * オブジェクトの `System.IO.FileStream``Read` メソッドを呼び出し、読み取るバイト配列、開始位置およびストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * オブジェクトのプロパティにバイト配列の内容を割り当てて、 `BLOB``MTOM` オブジェクトを入力します。

1. 追加署名フィールド

   オ追加ブジェクトのメソッドを呼び出し、次の値を渡すことにより、署名フィールドをPDFドキュメントに割り当てます。 `SignatureServiceClient``addSignatureField`

   * A `BLOB` object that represents the PDF document to which a signature field is added.
   * 署名フィールド名を指定するstring値です。
   * 署名フィールドを追加するページ番号を表すinteger値です。
   * 署名フィールドの場所を指定する `PositionRect` オブジェクトです。
   * 電子署名が署名フィールドに適用された後にロックされるPDFドキュメント内のフィールドを指定する `FieldMDPOptions` オブジェクトです。 このパラメーターの値はオプションで、渡すことができ `null`ます。
   * 様々な実行時値を指定する `PDFSeedValueOptions` オブジェクト。 このパラメーターの値はオプションで、渡すことができ `null`ます。

   署名フィールドを含むPDFドキュメントを表す `addSignatureField``BLOB` オブジェクトを返します。

1. PDFドキュメントをPDFファイルとして保存

   * コンストラクターを呼び出し、署名フィールドとファイルを開くモードを含むPDFドキュメントのファイルの場所を表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * メソッドが返した `BLOB` オブジェクトの内容を格納するバイト配列を作成し `addSignatureField` ます。 オブジェクトのデータメンバーの値を取得して、 `BLOB` バイト配列を入力し `binaryData` ます。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡して、バイト配列の内容をPDFファイルに書き込み `System.IO.BinaryWriter` ま `Write` す。

**関連トピック**

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 署名フィールド名の取得 {#retrieving-signature-field-names}

署名または認証する PDF ドキュメント内のすべての署名フィールドの名前を取得できます。PDF ドキュメント内の署名フィールド名が分からない場合や、名前を検証したい場合に、プログラムによって名前を取得することができます。The Signature service returns the fully qualified name of the signature field, such as `form1[0].grantApplication[0].page1[0].SignatureField1[0]`.

>[!NOTE]
>
>For more information about the Signature service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)

### 手順の概要 {#summary_of_steps-1}

署名フィールド名を取得するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. 署名クライアントを作成します。
1. 署名フィールドを含むPDFドキュメントを取得します。
1. 署名フィールド名を取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(AEM FormsがJBossにデプロイされている場合に必要)
* jbossall-client.jar(AEM FormsがJBossにデプロイされている場合に必要)

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**署名クライアントの作成**

プログラムを使用してSignatureサービスの操作を実行する前に、Signatureサービスクライアントを作成する必要があります。

**署名フィールドを含むPDFドキュメントの取得**

署名フィールドを含むPDFドキュメントを取得します。

**署名フィールド名の取得**

1つ以上の署名フィールドを含むPDFドキュメントを取得した後に、署名フィールド名を取得できます。

**関連トピック**

[Java APIを使用した署名フィールド名の取得](digitally-signing-certifying-documents.md#retrieve-signature-field-names-using-the-java-api)

[WebサービスAPIを使用した署名フィールドの取得](digitally-signing-certifying-documents.md#retrieve-signature-field-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[署名フィールドの追加](digitally-signing-certifying-documents.md#adding-signature-fields)

### Java APIを使用した署名フィールド名の取得 {#retrieve-signature-field-names-using-the-java-api}

署名API(Java)を使用して署名フィールド名を取得します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-signatures-client.jarなどのクライアントJARファイルを含めます。

1. 署名クライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `SignatureServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 署名フィールドを含むPDFドキュメントの取得

   * コンストラクターを使用し、PDFドキュメントの場所を指定するstring値を渡すことで、署名フィールドを含むPDFドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 署名フィールド名の取得

   * オブジェクトの `SignatureServiceClient` メソッドを呼び出し、署名フィールドを含むPDFドキュメントを含む `getSignatureFieldList``com.adobe.idp.Document` オブジェクトを渡して、署名フィールド名を取得します。 このメソッドは、 `java.util.List` オブジェクトを返します。このオブジェクト内の各要素には、1つの `PDFSignatureField` オブジェクトが含まれます。 このオブジェクトを使用すると、署名フィールドが表示されているかどうかなど、署名フィールドに関する追加情報を取得できます。
   * オブジェクトを繰り返し処理して、署名フィールド名があるかどうかを確認します。 `java.util.List` PDFドキュメントの各署名フィールドに対して、別々の `PDFSignatureField` オブジェクトを取得できます。 署名フィールドの名前を取得するには、 `PDFSignatureField` オブジェクトの `getName` メソッドを呼び出します。 このメソッドは、署名フィールド名を指定するstring値を返します。

**関連トピック**

[署名フィールド名の取得](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[クイック開始（SOAPモード）: Java APIを使用した署名フィールド名の取得](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-retrieving-signature-field-names-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用した署名フィールドの取得 {#retrieve-signature-field-using-the-web-service-api}

署名API（Webサービス）を使用して署名フィールド名を取得します。

1. プロジェクトファイルを含める

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >サーバーホスト `localhost` AEM FormsのIPアドレスに置き換えます。

1. 署名クライアントの作成

   * Create a `SignatureServiceClient` object by using its default constructor.
   * Create a `SignatureServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/SignatureService?WSDL`)に渡すstring値を渡します。 属性を使用する必要はありません `lc_version` 。 この属性は、サービス参照を作成する場合に使用されます)。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `SignatureServiceClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールドにAEM formsのユーザー名を割り当て `SignatureServiceClient.ClientCredentials.UserName.UserName`ます。
      * 対応するパスワード値をフィールドに割り当て `SignatureServiceClient.ClientCredentials.UserName.Password`ます。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当て `BasicHttpBindingSecurity.Security.Mode`ます。

1. 署名フィールドを含むPDFドキュメントの取得

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、署名フィールドを含むPDFドキュメントを保存するために使用されます。
   * コンストラクターを呼び出し、PDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
   * オブジェクトの `System.IO.FileStream``Read` メソッドを呼び出し、読み取るバイト配列、開始位置およびストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * オブジェクトにバイト配列の内容をフィールドに割り当てて、 `BLOB` オブジェクトを入力し `MTOM` ます。

1. 署名フィールド名の取得

   * オブジェクトの `SignatureServiceClient` メソッドを呼び出し、署名フィールドを含むPDFドキュメントを含む `getSignatureFieldList``BLOB` オブジェクトを渡して、署名フィールド名を取得します。 このメソッドは、各要素にオブジェクトが含まれる `MyArrayOfPDFSignatureField` コレクションオブジェクトを返し `PDFSignatureField` ます。
   * オブジェクトを繰り返し処理して、署名フィールド名があるかどうかを確認します。 `MyArrayOfPDFSignatureField` PDFドキュメントの各署名フィールドに対して、 `PDFSignatureField` オブジェクトを取得できます。 署名フィールドの名前を取得するには、 `PDFSignatureField` オブジェクトの `getName` メソッドを呼び出します。 このメソッドは、署名フィールド名を指定するstring値を返します。

**関連トピック**

[署名フィールド名の取得](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Modifying Signature Fields {#modifying-signature-fields}

Java APIとWebサービスAPIを使用して、PDFドキュメント内の署名フィールドを変更できます。 署名フィールドの署名フィールドロックディクショナリまたはシード値ディクショナリの値を操作することで署名フィールドを変更します。

A *field lock dictionary* specifies a list of fields that are locked when the signature field is signed. フィールドがロックされると、ユーザーはフィールドを変更できません。A *seed value dictionary* contains constraining information that is used at the time the signature is applied. 例えば、署名を無効にすることなく実行できるアクションを制御する権限設定を変更することができます。

既存の署名フィールドを変更すると、PDFドキュメントに変更を加え、ビジネス要件の変更を反映させることができます。 例えば、新しいビジネス要件では、ドキュメントの署名後にすべてのドキュメントフィールドのロックが必要になる場合があります。

この節では、フィールドロックディクショナリとシード値ディクショナリの両方の値を変更して、署名フィールドを変更する方法について説明します。 署名フィールドロックディクショナリに変更を加えると、署名フィールドへの署名時に、PDFドキュメント内のすべてのフィールドがロックされます。 シード値ディクショナリに変更を加えると、ドキュメントに対する特定の種類の変更が禁止されます。

>[!NOTE]
>
>Signatureサービスと署名フィールドの変更について詳しくは、『AEM Forms用 [サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順の概要 {#summary_of_steps-2}

PDFドキュメント内の署名フィールドを変更するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. 署名クライアントを作成します。
1. 変更する署名フィールドが含まれているPDFドキュメントを取得します。
1. 辞書の値を設定します。
1. 署名フィールドを変更します。
1. PDFドキュメントをPDFファイルとして保存します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(AEM FormsがJBossにデプロイされている場合に必要)
* jbossall-client.jar(AEM FormsがJBossにデプロイされている場合に必要)

For information about the location of these JAR files, see [Including LiveCycle Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**署名クライアントの作成**

プログラムを使用してSignatureサービスの操作を実行する前に、Signatureサービスクライアントを作成する必要があります。

**変更する署名フィールドが含まれているPDFドキュメントの取得**

変更する署名フィールドが含まれているPDFドキュメントを取得します。

**ディクショナリ値の設定**

署名フィールドを変更するには、フィールドロックディクショナリまたはシード値ディクショナリに値を割り当てます。 署名フィールドロックディクショナリ値を指定するには、ドキュメントフィールドの署名時にロックされるPDF署名フィールドを指定する必要があります。 （この節では、すべてのフィールドをロックする方法について説明します）。

次のシード値ディクショナリ値を設定できます。

* **リビジョンの確認**: 署名フィールドに署名が適用された場合に失効確認を実行するかどうかを指定します。
* **証明書のオプション**: 証明書のシード値ディクショナリに値を割り当てます。 証明書のオプションを指定する前に、証明書のシード値ディクショナリについて理解することをお勧めします。 (『 [PDF Reference](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf)』を参照)。
* **ダイジェストオプション**: 署名に使用するダイジェストアルゴリズムを割り当てます。 有効な値はSHA1、SHA256、SHA384、SHA512およびRIPEMD160です。
* **フィルタ**: 署名フィールドで使用するフィルターを指定します。 例えば、Adobe.PPKLiteフィルターを使用できます。 (『 [PDF Reference](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf)』を参照)。
* **フラグのオプション**: この署名フィールドに関連付けられているフラグ値を指定します。 値が1の場合、署名者は指定された値のみをエントリに使用する必要があります。 値が0の場合、他の値も許可されます。 ビット位置は次のとおりです。

   * **1（フィルタ）:** 署名フィールドへの署名に使用する署名ハンドラーです
   * **2(SubFilter):** 署名時に使用する有効なエンコーディングを示す名前の配列です
   * **3(V)**: 署名フィールドへの署名に使用する署名ハンドラーの必要最小限のバージョン番号です
   * **4（理由）:** ドキュメントに署名する理由を指定する文字列の配列です
   * **5(PDFLegalWarnings):** 考えられる法的証明を指定する文字列の配列です

* **法的証明**: ドキュメントを認証すると、ドキュメントの表示されるコンテンツをあいまいにしたり誤解を招く可能性のある、特定の種類のコンテンツを自動的にスキャンします。 例えば、注釈によって、認証対象を把握するために重要なテキストが隠される場合があります。 スキャン処理では、この種類のコンテンツの存在を示す警告が生成されます。 また、警告を生成した可能性のあるコンテンツに関する追加の説明も提供します。
* **権限**: 署名を無効にすることなく、PDFドキュメントで使用できる権限を指定します。
* **理由**: このドキュメントに署名が必要な理由を指定します。
* **タイムスタンプ**: タイムスタンプオプションを指定します。 例えば、使用するタイムスタンプサーバーのURLを設定できます。
* **バージョン**: 署名フィールドへの署名に使用する署名ハンドラーの最小バージョン番号を指定します。

**署名フィールドの変更**

Signatureサービスクライアントを作成した後、変更する署名フィールドを含むPDFドキュメントを取得し、Dictionary値を設定した後、Signatureサービスに対して署名フィールドを変更するよう指示できます。 次に、Signatureサービスは、変更された署名フィールドを含むPDFドキュメントを返します。 元のPDFドキュメントは影響を受けません。

**PDFドキュメントをPDFファイルとして保存**

変更した署名フィールドが含まれているPDFドキュメントをPDFファイルとして保存し、AcrobatまたはAdobe Readerで開けるようにします。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[SignatureサービスAPIのクイック開始](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

[PDFドキュメントへのデジタル署名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### Java APIを使用した署名フィールドの変更 {#modify-signature-fields-using-the-java-api}

署名API (Java)を使用して署名フィールドを変更します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-signatures-client.jarなどのクライアントJARファイルを含めます。

1. 署名クライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `SignatureServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 変更する署名フィールドが含まれているPDFドキュメントの取得

   * コンストラクターを使用し、PDFドキュメントの場所を指定するstring値を渡して、変更する署名フィールドを含むPDFドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. ディクショナリ値の設定

   * コンストラクタを使用して `PDFSignatureFieldProperties` オブジェクトを作成します。オブジェクトは、署名フィールドロックディクショナリとシード値ディクショナリ情報を格納します。 `PDFSignatureFieldProperties`
   * コンストラクタを使用して `PDFSeedValueOptionSpec` オブジェクトを作成します。このオブジェクトを使用すると、シード値ディクショナリの値を設定できます。
   * オブジェクトの `PDFSeedValueOptionSpec` メソッドを呼び出し、 `setMdpValue``MDPPermissions.NoChanges` 定義済みリスト値を渡すことで、PDFドキュメントに対する変更を許可しないようにします。
   * コンストラクタを使用して `FieldMDPOptionSpec` オブジェクトを作成します。このオブジェクトを使用すると、署名フィールドロックディクショナリの値を設定できます。
   * オブジェクトのメソッドを呼び出し、 `FieldMDPOptionSpec``setMdpValue``FieldMDPAction.ALL` 定義済みリスト値を渡すことで、PDFドキュメントのすべてのフィールドをロックします。
   * オブジェクトのメソッドを呼び出し、オブジェクトを渡して、シ `PDFSignatureFieldProperties` ード値ディクショナリ情報を設定し `setSeedValue` ま `PDFSeedValueOptionSpec` す。
   * オブジェクトのメソッドを呼び出し、 `PDFSignatureFieldProperties`オブジェクトを渡すことで、署名フィールドロックディクショナリ情報を設定し `setFieldMDP``FieldMDPOptionSpec` ます。

   >[!NOTE]
   >
   >設定可能なすべてのシード値ディクショナリ値を確認するには、クラス参照を参照して `PDFSeedValueOptionSpec` ください。 ( [AEM FormsAPIリファレンスを参照](https://www.adobe.com/go/learn_aemforms_javadocs_63_en))。

1. 署名フィールドの変更

   署名フィールドを変更するには、 `SignatureServiceClient` オブジェクトの `modifySignatureField` メソッドを呼び出し、次の値を渡します。

   * 変更する署名フィールドが含まれるPDFドキュメントを格納する `com.adobe.idp.Document` オブジェクトです
   * 署名フィールドの名前を指定するstring値です
   * 署名フィールドロックディクショナリとシード値ディクショナリの情報を格納する `PDFSignatureFieldProperties` オブジェクトです

   この `modifySignatureField` メソッドは、変更された署名フィールドを含むPDFドキュメントを格納する `com.adobe.idp.Document` オブジェクトを返します。

1. PDFドキュメントをPDFファイルとして保存

   * Create a `java.io.File` object and ensure that the file name extension is .pdf.
   * Invoke the `com.adobe.idp.Document` object’s `copyToFile` method to copy the contents of the `com.adobe.idp.Document` object to the file. メソッドが返した `com.adobe.idp.Document` オブジェクトを使用していることを確認し `modifySignatureField` ます。

### WebサービスAPIを使用した署名フィールドの変更 {#modify-signature-fields-using-the-web-service-api}

Signature API（Webサービス）を使用して署名フィールドを変更します。

1. プロジェクトファイルを含める

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >サーバーホスト `localhost` AEM FormsのIPアドレスに置き換えます。

1. 署名クライアントの作成

   * Create a `SignatureServiceClient` object by using its default constructor.
   * Create a `SignatureServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/SignatureService?WSDL`)に渡すstring値を渡します。 属性を使用する必要はありません `lc_version` 。 この属性は、サービス参照を作成する場合に使用されます)。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `SignatureServiceClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールドにAEM formsのユーザー名を割り当て `SignatureServiceClient.ClientCredentials.UserName.UserName`ます。
      * 対応するパスワード値をフィールドに割り当て `SignatureServiceClient.ClientCredentials.UserName.Password`ます。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当て `BasicHttpBindingSecurity.Security.Mode`ます。

1. 変更する署名フィールドが含まれているPDFドキュメントの取得

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、変更する署名フィールドが含まれるPDFドキュメントの保存に使用されます。
   * コンストラクターを呼び出し、PDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
   * オブジェクトの `System.IO.FileStream``Read` メソッドを呼び出し、読み取るバイト配列、開始位置およびストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * オブジェクトのプロパティにバイト配列の内容を割り当てて、 `BLOB``MTOM` オブジェクトを入力します。

1. ディクショナリ値の設定

   * コンストラクタを使用して `PDFSignatureFieldProperties` オブジェクトを作成します。このオブジェクトは、署名フィールドロックディクショナリとシード値ディクショナリの情報を格納します。
   * コンストラクタを使用して `PDFSeedValueOptionSpec` オブジェクトを作成します。このオブジェクトを使用すると、シード値ディクショナリの値を設定できます。
   * PDFドキュメントの変更を許可しない場合は、 `MDPPermissions.NoChanges` 定義済みリスト値を `PDFSeedValueOptionSpec` オブジェクトの `mdpValue` データメンバーに割り当てます。
   * コンストラクタを使用して `FieldMDPOptionSpec` オブジェクトを作成します。このオブジェクトを使用すると、署名フィールドロックディクショナリの値を設定できます。
   * PDFドキュメント内のすべてのフィールドをロックするには、 `FieldMDPAction.ALL` 定義済みリスト値を `FieldMDPOptionSpec` オブジェクトの `mdpValue` データメンバーに割り当てます。
   * シード値ディクショナリ情報を設定するには、 `PDFSeedValueOptionSpec` オブジェクトを `PDFSignatureFieldProperties` オブジェクトの `seedValue` データメンバーに割り当てます。
   * 署名フィールドロックディクショナリ情報を設定するには、 `FieldMDPOptionSpec` オブジェクトを `PDFSignatureFieldProperties` オブジェクトの `fieldMDP` データメンバに割り当てます。

   >[!NOTE]
   >
   >設定可能なすべてのシード値ディクショナリ値を確認するには、クラス参照を参照して `PDFSeedValueOptionSpec` ください。 ( [AEM FormsAPIリファレンスを参照](https://www.adobe.com/go/learn_aemforms_javadocs_63_en))。

1. 署名フィールドの変更

   署名フィールドを変更するには、 `SignatureServiceClient` オブジェクトの `modifySignatureField` メソッドを呼び出し、次の値を渡します。

   * 変更する署名フィールドが含まれるPDFドキュメントを格納する `BLOB` オブジェクトです
   * 署名フィールドの名前を指定するstring値です
   * 署名フィールドロックディクショナリとシード値ディクショナリの情報を格納する `PDFSignatureFieldProperties` オブジェクトです

   この `modifySignatureField` メソッドは、変更された署名フィールドを含むPDFドキュメントを格納する `BLOB` オブジェクトを返します。

1. PDFドキュメントをPDFファイルとして保存

   * オブジェクトを作成するには、コンストラクターを呼び出し、署名フィールドを含むPDFドキュメントのファイルの場所と、ファイルを開くモードを表すstring値を渡します。 `System.IO.FileStream`
   * メソッドが返す `BLOB` オブジェクトの内容を格納するバイト配列を作成し `addSignatureField` ます。 オブジェクトのデータメンバーの値を取得して、 `BLOB` バイト配列を入力し `MTOM` ます。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡して、バイト配列の内容をPDFファイルに書き込み `System.IO.BinaryWriter` ま `Write` す。

**関連トピック**

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Digitally Signing PDF Documents {#digitally-signing-pdf-documents}

セキュリティレベルの提供のため、PDF に電子署名を適用することができます。手書き署名のような電子署名は、署名者を識別したり、ドキュメントに関するステートメントを作成する手段として使用できます。ドキュメントの電子署名に使用されている技術は、署名者と受信者の両方が、何に署名されているのかを明確にし、その署名によりドキュメントに変更がないことを確認するのに役立ちます。

PDF ドキュメントは、公開鍵を用いて署名されます。署名者は公開鍵と秘密鍵の 2 つの鍵を持っています。秘密鍵はユーザーの秘密鍵証明書に保存されます。この資格情報は署名時に使用可能にする必要があります。 公開鍵はユーザーの証明書に保存されます。受信者が署名を検証するには、この証明書を使用できる必要があります。 失効した証明書に関する情報は、認証機関から配布される証明書失効リスト（CRL）およびオンライン証明書ステータスプロトコル（OCSP）応答内にあります。署名が行われた時間は、タイムスタンプ局として知られる信頼できるソースから取得されます。

>[!NOTE]
>
>PDFドキュメントに電子署名を行う前に、AEM Formsに証明書が追加されていることを確認する必要があります。 証明書は、管理コンソールを使用して、またはTrust Manager APIをプログラムで使用して追加します。 (Trust Manager APIを使用した秘密鍵証明書の [読み込みを参照](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api))。

PDFドキュメントにプログラムによってデジタル署名を行うことができます。 PDFドキュメントに電子署名する場合は、AEM Formsに存在するセキュリティ証明書を参照する必要があります。 証明書は署名に使用する秘密鍵となります。

Signatureサービスは、PDFドキュメントが署名されるときに次の手順を実行します。

1. Signatureサービスは、要求で指定されたエイリアスを渡すことで、Truststoreから秘密鍵証明書を取得します。
1. Truststoreは、指定した秘密鍵証明書を検索します。
1. 秘密鍵証明書がSignatureサービスに返され、ドキュメントへの署名に使用されます。 証明書は、後で要求を行う場合にエイリアスに対してもキャッシュされます。

セキュリティ証明書の処理について詳しくは、使用しているアプリケーションサーバー版の『 *AEM Formsのインストールおよびデプロイ* 』ガイドを参照してください。

>[!NOTE]
>
>署名ドキュメントと認証ユーザーには違いがあります。 (See [Certifying PDF Documents](digitally-signing-certifying-documents.md#certifying-pdf-documents).)

>[!NOTE]
>
>PDFドキュメントによっては、署名がサポートされていない場合があります。 Signatureサービスとデジタル署名ドキュメントについて詳しくは、『AEM Forms用 [サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

>[!NOTE]
>
>Signatureサービスは、ドキュメントの認証など、操作への入力としてPDFデータが埋め込まれたXDPファイルをサポートしません。 この操作により、Signatureサービスでは、 `PDFOperationException`この問題を解決するには、PDF Utilitiesサービスを使用してXDPファイルをPDFファイルに変換し、変換したPDFファイルをSignatureサービス操作に渡します。 (「PDF Utilitiesの [操作](/help/forms/developing/pdf-utilities.md#working-with-pdf-utilities)」を参照)。

**nCipher nShield HSM秘密鍵証明書**

PDFドキュメントの署名や認証にnCipher nShield HSM秘密鍵証明書を使用する場合、AEM Formsのデプロイ先のJ2EEアプリケーションサーバーが再起動されるまで、新しい秘密鍵証明書は使用できません。 ただし、設定値を設定すると、J2EEアプリケーションサーバーを再起動しなくても、署名または認証の操作が動作します。

次の設定値をcknfastrcファイルに追加できます。このファイルは/opt/nfast/cknfastrc(またはc:\nfast\cknfastrc)にあります。

```shell
    CKNFAST_ASSUME_SINGLE_PROCESS=0
```

この設定値をcknfastrcファイルに追加すると、J2EEアプリケーションサーバーを再起動しなくても、新しい秘密鍵証明書を使用できます。

**署名は信頼されていません**

同じPDFドキュメントの認証および署名時に、認証署名が信頼されていない場合、AcrobatまたはAdobe ReaderでPDFドキュメントを開くときに、最初の署名に対して黄色い三角形が表示されます。 この状況を回避するには、認証署名を信頼する必要があります。

**XFAベースのフォームである署名ドキュメント**

SignatureサービスAPIを使用してXFAベースのフォームに署名しようとすると、Acrobatに `View` あるデータが失われる場合があり `Signed``Version` ます。 例えば、次のワークフローを考えてみましょう。

* Designerを使用して作成したXDPファイルを使用して、署名フィールドを含むフォームデザインと、フォームデータを含むXMLデータを結合します。 インタラクティブPDFドキュメントを生成するには、Formsサービスを使用します。
* SignatureサービスAPIを使用してPDFドキュメントに署名します。

### 手順の概要 {#summary_of_steps-3}

PDFドキュメントに電子署名するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Signatureサービスクライアントを作成します。
1. 署名するPDFドキュメントを取得します。
1. PDFドキュメントに署名します。
1. 署名済みPDFドキュメントをPDFファイルとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(AEM FormsがJBossにデプロイされている場合に必要)
* jbossall-client.jar(AEM FormsがJBossにデプロイされている場合に必要)

**Signaturesクライアントの作成**

プログラムを使用してSignatureサービスの操作を実行する前に、Signatureサービスクライアントを作成する必要があります。

**PDFドキュメントに署名を依頼する**

PDFドキュメントに署名するには、署名フィールドを含むPDFドキュメントを取得する必要があります。 PDFドキュメントに署名フィールドが含まれていない場合、署名を行うことはできません。 署名フィールドは、Designerを使用して追加することも、プログラムを使用して追加することもできます。

**PDFドキュメントへの署名**

PDFドキュメントに署名する場合、Signatureサービスで使用する実行時オプションを設定できます。 次のオプションを設定できます。

* 外観オプション
* 失効確認
* タイムスタンプ値

外観のオプションは、 `PDFSignatureAppearanceOptionSpec` オブジェクトを使用して設定します。 例えば、 `PDFSignatureAppearanceOptionSpec` オブジェクトの `setShowDate` メソッドを呼び出して渡すことで、署名内の日付を表示でき `true`ます。

PDFドキュメントのデジタル署名に使用される証明書が失効したかどうかを判定する失効確認を実行するかどうかを指定することもできます。 失効確認を実行するには、次のいずれかの値を指定します。

* **NoCheck**: 失効確認を実行しません。
* **BestEffort**: 常に、チェーン内のすべての証明書の失効を確認しようとします。 チェックで何らかの問題が発生した場合、失効は有効であると見なされます。 エラーが発生した場合は、証明書が失効していないと想定します。
* **CheckIfAvailable:** 失効情報が利用できる場合、チェーン内のすべての証明書の失効を確認します。 チェックで問題が発生した場合、失効は無効であると見なされます。 エラーが発生した場合は、証明書が失効し、無効であると仮定します。 （これがデフォルト値です）。
* **AlwaysCheck**: チェーン内のすべての証明書の失効を確認します。 どの証明書にも失効情報が存在しない場合、失効は無効であると見なされます。

証明書に対して失効確認を実行するには、 `CRLOptionSpec` オブジェクトを使用して、証明書失効リスト(CRL)サーバーへのURLを指定します。 ただし、失効確認を実行する場合で、CRLサーバーへのURLを指定しない場合は、Signatureサービスは証明書からURLを取得します。

失効確認を実行する際は、CRLサーバーを使用する代わりに、オンライン証明書ステータスプロトコル(OCSP)サーバーを使用できます。 通常、CRLサーバーとは異なり、OCSPサーバーを使用する場合は、失効確認の実行が高速になります。 (https://tools.ietf.org/html/rfc2560の「Online Certificate Status Protocol」を参照 [](https://tools.ietf.org/html/rfc2560))。

SignatureサービスでAdobe Applications and Servicesを使用する場合に、CRLおよびOCSPサーバーの順序を設定できます。 例えば、Adobe Applications and ServicesでOCSPサーバーが最初に設定されている場合は、OCSPサーバーを確認し、次にCRLサーバーを確認します。 （AACヘルプの「Trust Storeを使用した証明書と秘密鍵証明書の管理」を参照）。

失効確認を実行しないように指定した場合、Signatureサービスは、ドキュメントの署名または認証に使用された証明書が失効したかどうかを確認しません。 つまり、CRLおよびOCSPサーバー情報は無視されます。

>[!NOTE]
>
>証明書ではCRLまたはOCSPサーバーを指定できますが、証明書で指定されているURLを上書きするには、およびオブジ `CRLOptionSpec``OCSPOptionSpec` ェクトを使用します。 例えば、CRLサーバーを上書きするには、 `CRLOptionSpec` オブジェクトの `setLocalURI` メソッドを呼び出します。

タイムスタンプとは、署名済みまたは認証済みのドキュメントが変更された時間を追跡するプロセスを指します。 ドキュメントの署名後は、ドキュメントの所有者によっても、署名を変更しないでください。 タイムスタンプ機能を使用すると、署名済みまたは認証済みのドキュメントの有効性を強化できます。 タイムスタンプオプションは、 `TSPOptionSpec` オブジェクトを使用して設定できます。 例えば、タイムスタンププロバイダー(TSP)サーバーのURLを指定できます。

>[!NOTE]
>
>JavaおよびWebサービスのセクションや対応するクイック開始のウォークスルーでは、失効確認が使用されます。 CRLまたはOCSPサーバー情報が指定されていないので、サーバー情報は、PDFドキュメントのデジタル署名に使用される証明書から取得されます。

PDFドキュメントに正しく署名するには、電子署名を含める署名フィールドの完全修飾名を指定します（例：） `form1[0].#subform[1].SignatureField3[3]`。 XFAフォームフィールドを使用する場合は、署名フィールドの名前の一部を使用することもできます。 `SignatureField3[3]`.

また、PDFドキュメントに電子署名するためのセキュリティ証明書を参照する必要もあります。 セキュリティ証明書を参照するには、エイリアスを指定します。 エイリアスは、PKCS#12ファイル（拡張子.pfx付き）またはハードウェアセキュリティモジュール(HSM)内の実際の秘密鍵証明書への参照です。 セキュリティ証明書について詳しくは、使用しているアプリケーションサーバー版の『 *AEM Formsのインストールおよびデプロイ* 』ガイドを参照してください。

**署名済みPDFドキュメントの保存**

SignatureサービスがPDFドキュメントに電子署名した後、その画像をPDFファイルとして保存して、ユーザーがAcrobatまたはAdobe Readerで開くことができるようにすることができます。

**関連トピック**

[Java APIを使用したPDFドキュメントへのデジタル署名](digitally-signing-certifying-documents.md#digitally-sign-pdf-documents-using-the-java-api)

[WebサービスAPIを使用したPDFドキュメントへのデジタル署名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[署名フィールドの追加](digitally-signing-certifying-documents.md#adding-signature-fields)

[署名フィールド名の取得](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

### Java APIを使用したPDFドキュメントへのデジタル署名 {#digitally-sign-pdf-documents-using-the-java-api}

署名API(Java)を使用してPDFドキュメントに電子署名する：

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-signatures-client.jarなどのクライアントJARファイルを含めます。

1. Signaturesクライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `SignatureServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. PDFドキュメントに署名を依頼する

   * コンストラクターを使用し、PDFドキュメントの場所を指定する文字列値を渡して、デジタル署名するPDFドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PDFドキュメントへの署名

   オブジェクトの `SignatureServiceClient``sign` メソッドを呼び出し、次の値を渡して、PDFドキュメントに署名します。

   * A `com.adobe.idp.Document` object that represents the PDF document to sign.
   * 電子署名を含む署名フィールドの名前を表すstring値です。
   * A `Credential` object that represents the credential that is used to digitally sign the PDF document. オブジェクトの静的な `Credential` メソッドを呼び出し、セキュリティ証明書に対応するエイリアス値を指定する文字列値を渡して、 `Credential``getInstance` オブジェクトを作成します。
   * PDFドキュメントのダイジェストの作成に使用するハッシュアルゴリズムを表す静的データメンバーを指定する `HashAlgorithm` オブジェクトです。 例えば、SHA1アルゴリズム `HashAlgorithm.SHA1` を使用するように指定できます。
   * PDFドキュメントがデジタル署名された理由を表すstring値です。
   * 署名者の連絡先情報を表すstring値です。
   * 電子署名の外観を制御する `PDFSignatureAppearanceOptions` オブジェクトです。 例えば、このオブジェクトを使用して、電子署名にカスタムロゴを追加できます。
   * 署名者の証明書に対して失効確認を実行するかどうかを指定する `java.lang.Boolean` オブジェクトです。
   * オンライン証明書ステータスプロトコル(OCSP)サポートの環境設定を格納する `OCSPOptionSpec` オブジェクトです。 失効確認が実行されない場合、このパラメーターは使用されず、指定でき `null`ます。
   * 証明書失効リスト(CRL)の環境設定を格納する `CRLPreferences` オブジェクトです。 失効確認が実行されない場合、このパラメーターは使用されず、指定でき `null`ます。
   * タイムスタンププロバイダー(TSP)でサポートされる環境設定を格納する `TSPPreferences` オブジェクトです。 このパラメーターはオプションで、を指定でき `null`ます。 For more information, see [AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

   署名済みPDFドキュメントを表す `sign``com.adobe.idp.Document` オブジェクトを返します。

1. 署名済みPDFドキュメントの保存

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が .pdf であることを確認します。
   * Invoke the `com.adobe.idp.Document` object’s `copyToFile` method and pass `java.io.File`to copy the contents of the `Document` object to the file. `com.adobe.idp.Document` メソッドから返された `sign` オブジェクトを必ず使用してください。

**関連トピック**

[PDFドキュメントへのデジタル署名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[クイック開始（SOAPモード）: Java APIを使用したPDFドキュメントへのデジタル署名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したPDFドキュメントへのデジタル署名 {#digitally-signing-pdf-documents-using-the-web-service-api}

Signature API（Webサービス）を使用してPDFドキュメントに電子署名するには：

1. プロジェクトファイルを含める

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >サーバーホスト `localhost` AEM FormsのIPアドレスに置き換えます。

1. Signaturesクライアントの作成

   * Create a `SignatureServiceClient` object by using its default constructor.
   * Create a `SignatureServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/SignatureService?WSDL`)に渡すstring値を渡します。 属性を使用する必要はありません `lc_version` 。 この属性は、サービス参照を作成する場合に使用されます)。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `SignatureServiceClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールドにAEM formsのユーザー名を割り当て `SignatureServiceClient.ClientCredentials.UserName.UserName`ます。
      * 対応するパスワード値をフィールドに割り当て `SignatureServiceClient.ClientCredentials.UserName.Password`ます。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当て `BasicHttpBindingSecurity.Security.Mode`ます。

1. PDFドキュメントに署名を依頼する

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、署名されたPDFドキュメントの保存に使用されます。
   * コンストラクターを呼び出し、署名するPDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
   * オブジェクトの `System.IO.FileStream``Read` メソッドを呼び出し、読み取るバイト配列、開始位置およびストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * オブジェクトのプロパティにバイト配列の内容を割り当てて、 `BLOB``MTOM` オブジェクトを入力します。

1. PDFドキュメントへの署名

   オブジェクトの `SignatureServiceClient``sign` メソッドを呼び出し、次の値を渡して、PDFドキュメントに署名します。

   * A `BLOB` object that represents the PDF document to sign.
   * 電子署名を含む署名フィールドの名前を表すstring値です。
   * A `Credential` object that represents the credential that is used to digitally sign the PDF document. コンストラクターを使用して `Credential` オブジェクトを作成し、オブジェクトのプロパティに値を割り当ててエイリアスを指定し `Credential` ま `alias` す。
   * PDFドキュメントのダイジェストの作成に使用するハッシュアルゴリズムを表す静的データメンバーを指定する `HashAlgorithm` オブジェクトです。 例えば、SHA1アルゴリズム `HashAlgorithm.SHA1` を使用するように指定できます。
   * ハッシュアルゴリズムを使用するかどうかを指定するBoolean値です。
   * PDFドキュメントがデジタル署名された理由を表すstring値です。
   * 署名者の場所を表すstring値です。
   * 署名者の連絡先情報を表すstring値です。
   * 電子署名の外観を制御する `PDFSignatureAppearanceOptions` オブジェクトです。 例えば、このオブジェクトを使用して、電子署名にカスタムロゴを追加できます。
   * 署名者の証明書に対して失効確認を実行するかどうかを指定する `System.Boolean` オブジェクトです。 この失効確認が行われると、署名に埋め込まれます。 デフォルトは、`false` です。
   * オンライン証明書ステータスプロトコル(OCSP)サポートの環境設定を格納する `OCSPOptionSpec` オブジェクトです。 失効確認が実行されない場合、このパラメーターは使用されず、指定でき `null`ます。 このオブジェクトについて詳しくは、『 [AEM FormsAPIリファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)』を参照してください。
   * 証明書失効リスト(CRL)の環境設定を格納する `CRLPreferences` オブジェクトです。 失効確認が実行されない場合、このパラメーターは使用されず、指定でき `null`ます。
   * タイムスタンププロバイダー(TSP)でサポートされる環境設定を格納する `TSPPreferences` オブジェクトです。 このパラメーターはオプションで、を指定でき `null`ます。

   署名済みPDFドキュメントを表す `sign``BLOB` オブジェクトを返します。

1. 署名済みPDFドキュメントの保存

   * Create a `System.IO.FileStream` object by invoking its constructor. 署名済みPDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * メソッドが返した `BLOB` オブジェクトの内容を格納するバイト配列を作成し `sign` ます。 オブジェクトのデータメンバーの値を取得して、 `BLOB` バイト配列を入力し `MTOM` ます。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡して、バイト配列の内容をPDFファイルに書き込み `System.IO.BinaryWriter` ま `Write` す。

**関連トピック**

[PDFドキュメントへのデジタル署名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## インタラクティブフォームへのデジタル署名 {#digitally-signing-interactive-forms}

Formsサービスが作成するインタラクティブフォームに署名できます。 例えば、次のワークフローを考えてみましょう。

* Designerを使用して作成されたXFAベースのPDFフォームと、Formsサービスを使用してXMLドキュメント内のフォームデータを結合します。 Formsサーバーはインタラクティブフォームをレンダリングします。
* インタラクティブフォームにはSignatureサービスAPIを使用して署名します。

この結果、デジタル署名されたインタラクティブPDFフォームが生成されます。 XFAフォームに基づくPDFフォームに署名する場合は、PDFファイルをAdobeスタティックPDFフォームとして保存する必要があります。 AdobeダイナミックPDFフォームとして保存されたPDFフォームに署名しようとすると、例外が発生します。 Formsサービスから返されるフォームに署名するので、フォームに署名フィールドが含まれていることを確認してください。

>[!NOTE]
>
>インタラクティブフォームに電子署名する前に、AEM Formsに証明書を追加しておく必要があります。 証明書は、管理コンソールを使用して、またはTrust Manager APIをプログラムで使用して追加します。 (Trust Manager APIを使用した秘密鍵証明書の [読み込みを参照](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api))。

Forms Service APIを使用する場合、 `GenerateServerAppearance` 実行時オプションをに設定し `true`ます。 この実行時オプションを使用すると、サーバーで生成されたフォームの外観を、AcrobatまたはAdobe Readerで開いたときにも有効なままにすることができます。 Forms APIを使用して署名するインタラクティブフォームを生成する場合は、この実行時オプションを設定することをお勧めします。

>[!NOTE]
>
>「デジタル署名インタラクティブフォーム」を読む前に、PDFドキュメントの署名についてよく理解しておくことをお勧めします。 (See [Digitally Signing PDF Documents](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)

### 手順の概要 {#summary_of_steps-4}

Formsサービスが返すインタラクティブフォームに電子署名するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Forms &amp; Signaturesクライアントを作成します。
1. Formsサービスを使用してインタラクティブフォームを取得します。
1. インタラクティブフォームに署名します。
1. 署名済みPDFドキュメントをPDFファイルとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-forms-client.jar
* adobe-utilities.jar(AEM FormsがJBossにデプロイされている場合に必要)
* jbossall-client.jar(AEM FormsがJBossにデプロイされている場合に必要)

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Forms &amp; Signaturesクライアントの作成**

このワークフローはFormsサービスとSignatureサービスの両方を呼び出すので、FormsサービスクライアントとSignatureサービスクライアントの両方を作成します。

**Formsサービスを使用してインタラクティブフォームを取得する**

Formsサービスを使用して、署名するインタラクティブPDFフォームを取得できます。 AEM Forms時点では、レンダリングするフォームを含むFormsサービスに `com.adobe.idp.Document` オブジェクトを渡すことができます。 このメソッドの名前はです `renderPDFForm2`。 このメソッドは、署名するフォームを含む `com.adobe.idp.Document` オブジェクトを返します。 この `com.adobe.idp.Document` インスタンスはSignatureサービスに渡すことができます。

同様に、Webサービスを使用している場合は、Formsサービスが返す `BLOB` インスタンスをSignatureサービスに渡すことができます。

>[!NOTE]
>
>「デジタル署名インタラクティブフォーム」セクションに関連付けられているクイック開始が呼び出され `renderPDFForm2` ます。

**インタラクティブフォームに署名する**

PDFドキュメントに署名する場合、Signatureサービスで使用する実行時オプションを設定できます。 次のオプションを設定できます。

* 外観オプション
* 失効確認
* タイムスタンプ値

外観のオプションは、 `PDFSignatureAppearanceOptionSpec` オブジェクトを使用して設定します。 例えば、 `PDFSignatureAppearanceOptionSpec` オブジェクトの `setShowDate` メソッドを呼び出して渡すことで、署名内の日付を表示でき `true`ます。

**署名済みPDFドキュメントの保存**

SignatureサービスがPDFドキュメントに電子署名した後、その画像をPDFファイルとして保存できます。 PDFファイルは、AcrobatまたはAdobe Readerで開くことができます。

**関連トピック**

[Java APIを使用したインタラクティブフォームへの電子署名](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-java-api)

[WebサービスAPIを使用したインタラクティブフォームへの電子署名](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDFドキュメントへのデジタル署名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[インタラクティブPDF formsのレンダリング](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms)

### Java APIを使用したインタラクティブフォームへの電子署名 {#digitally-sign-an-interactive-form-using-the-java-api}

フォームと署名API (Java)を使用してインタラクティブフォームに電子署名する：

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-signatures-client.jarやadobe-forms-client.jarなどのクライアントJARファイルを含めます。

1. Forms &amp; Signaturesクライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `SignatureServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `FormsServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. Formsサービスを使用してインタラクティブフォームを取得する

   * Formsサービスに渡すPDFドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。このオブジェクトは、コンストラクターを使用して作成します。 PDFドキュメントの場所を指定するstring値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクターを使用して、Formsサービスに渡すフォームデータを含むXMLドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。 XMLファイルの場所を指定するstring値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。
   * 実行時オプションの設定に使用する `PDFFormRenderSpec` オブジェクトを作成します。 オブジェクトの `PDFFormRenderSpec` メソッドを呼び出し、 `setGenerateServerAppearance` 渡し `true`ます。
   * オブジェクトの `FormsServiceClient``renderPDFForm2` メソッドを呼び出し、次の値を渡します。

      * レンダリングするPDFフォームを含む `com.adobe.idp.Document` オブジェクトです。
      * フォームとマージするデータを含む `com.adobe.idp.Document` オブジェクト。
      * 実行時オプションを格納する `PDFFormRenderSpec` オブジェクト。
      * Formsサービスに必要なURI値を含む `URLSpec` オブジェクトです。 このパラメーター値 `null` を指定できます。
      * 添付ファイルを格納する `java.util.HashMap` オブジェクトです。 これはオプションのパラメーターで、フォームにファイルを添付しない `null` かどうかを指定できます。

      この `renderPDFForm2` メソッドは、フォームデータストリームを含む `FormsResult` オブジェクトを返します

   * オブジェクトのメソッドを呼び出して、PDF `FormsResult` フォームを取得し `getOutputContent` ます。 このメソッドは、インタラクティブフォームを表す `com.adobe.idp.Document` オブジェクトを返します。


1. インタラクティブフォームに署名する

   オブジェクトの `SignatureServiceClient``sign` メソッドを呼び出し、次の値を渡して、PDFドキュメントに署名します。

   * A `com.adobe.idp.Document` object that represents the PDF document to sign. このオブジェクトがFormsサービスから取得された `com.adobe.idp.Document` オブジェクトであることを確認します。
   * 署名された署名フィールドの名前を表すstring値です。
   * A `Credential` object that represents the credential that is used to digitally sign the PDF document. オブジェクトのスタティック `Credential` メソッドを呼び出して、 `Credential``getInstance` オブジェクトを作成します。 セキュリティ秘密鍵証明書に対応するエイリアス値を指定するstring値を渡します。
   * PDFドキュメントのダイジェストの作成に使用するハッシュアルゴリズムを表す静的データメンバーを指定する `HashAlgorithm` オブジェクトです。 例えば、SHA1アルゴリズム `HashAlgorithm.SHA1` を使用するように指定できます。
   * PDFドキュメントがデジタル署名された理由を表すstring値です。
   * 署名者の連絡先情報を表すstring値です。
   * 電子署名の外観を制御する `PDFSignatureAppearanceOptions` オブジェクトです。 例えば、このオブジェクトを使用して、電子署名にカスタムロゴを追加できます。
   * 署名者の証明書に対して失効確認を実行するかどうかを指定する `java.lang.Boolean` オブジェクトです。
   * オンライン証明書ステータスプロトコル(OCSP)サポートの環境設定を格納する `OCSPPreferences` オブジェクトです。 失効確認が実行されない場合、このパラメーターは使用されず、指定でき `null`ます。
   * 証明書失効リスト(CRL)の環境設定を格納する `CRLPreferences` オブジェクトです。 失効確認が実行されない場合、このパラメーターは使用されず、指定でき `null`ます。
   * タイムスタンププロバイダー(TSP)でサポートされる環境設定を格納する `TSPPreferences` オブジェクトです。 このパラメーターはオプションで、を指定でき `null`ます。

   署名済みPDFドキュメントを表す `sign``com.adobe.idp.Document` オブジェクトを返します。

1. 署名済みPDFドキュメントの保存

   * Create a `java.io.File` object and ensure that the filename extension is .pdf.
   * Invoke the `com.adobe.idp.Document` object’s `copyToFile` method and pass `java.io.File`to copy the contents of the `Document` object to the file. メソッドが返した `com.adobe.idp.Document` オブジェクトを使用していることを確認し `sign` ます。

**関連トピック**

[インタラクティブフォームへのデジタル署名](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[クイック開始（SOAPモード）: Java APIを使用したPDFドキュメントへのデジタル署名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したインタラクティブフォームへの電子署名 {#digitally-sign-an-interactive-form-using-the-web-service-api}

Forms and Signature API（Webサービス）を使用してインタラクティブフォームに電子署名するには：

1. プロジェクトファイルを含める

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 このクライアントアプリケーションは2つのAEM Formsサービスを呼び出すので、2つのサービス参照を作成します。 Signatureサービスに関連付けられたサービス参照には、次のWSDL定義を使用します。 `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   Formsサービスに関連付けられたサービス参照に対して、次のWSDL定義を使用します。 `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   この `BLOB` データ型は両方のサービス参照に共通なので、使用する場合は `BLOB` データ型を完全に限定します。 対応するWebサービスクイック開始では、すべての `BLOB` インスタンスが完全修飾されます。

   >[!NOTE]
   >
   >サーバーホスト `localhost` AEM FormsのIPアドレスに置き換えます。

1. Forms &amp; Signaturesクライアントの作成

   * Create a `SignatureServiceClient` object by using its default constructor.
   * Create a `SignatureServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/SignatureService?WSDL`)に渡すstring値を渡します。 属性を使用する必要はありません `lc_version` 。 この属性は、サービス参照を作成する場合に使用されます)。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `SignatureServiceClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールドにAEM formsのユーザー名を割り当て `SignatureServiceClient.ClientCredentials.UserName.UserName`ます。
      * 対応するパスワード値をフィールドに割り当て `SignatureServiceClient.ClientCredentials.UserName.Password`ます。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
   * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当て `BasicHttpBindingSecurity.Security.Mode`ます。

   >[!NOTE]
   >
   >Formsサービスクライアントに対して、この手順を繰り返します。

1. Formsサービスを使用してインタラクティブフォームを取得する

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、署名されたPDFドキュメントの保存に使用されます。
   * コンストラクターを呼び出し、署名するPDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
   * オブジェクトの `System.IO.FileStream``Read` メソッドを呼び出し、読み取るバイト配列、開始位置およびストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * オブジェクトのプロパティにバイト配列の内容を割り当てて、 `BLOB``MTOM` オブジェクトを入力します。
   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、フォームデータの格納に使用されます。
   * コンストラクターを呼び出し、フォームデータを含むXMLファイルのファイルの場所とファイルを開くモードを表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
   * オブジェクトの `System.IO.FileStream``Read` メソッドを呼び出し、読み取るバイト配列、開始位置およびストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * オブジェクトのプロパティにバイト配列の内容を割り当てて、 `BLOB``MTOM` オブジェクトを入力します。
   * 実行時オプションの設定に使用する `PDFFormRenderSpec` オブジェクトを作成します。 値をオブジェクト `true` のフ `PDFFormRenderSpec``generateServerAppearance` ィールドに割り当てます。
   * オブジェクトの `FormsServiceClient``renderPDFForm2` メソッドを呼び出し、次の値を渡します。

      * レンダリングするPDFフォームを含む `BLOB` オブジェクトです。
      * フォームとマージするデータを含む `BLOB` オブジェクト。
      * 実行時オプションを格納する `PDFFormRenderSpec` オブジェクト。
      * Formsサービスに必要なURI値を含む `URLSpec` オブジェクトです。 このパラメーター値 `null` を指定できます。
      * 添付ファイルを格納する `java.util.HashMap` オブジェクトです。 これはオプションのパラメーターで、フォームにファイルを添付しない `null` かどうかを指定できます。
      * フォーム内のページ数を保存するために使用される長い出力パラメーター。
      * ロケール値に使用される文字列出力パラメーターです。
      * インタラクティブフォームの保存に使用される出力パラメーターである `FormResult` 値です。
   * オブジェクトのフィールドを呼び出して、PDF `FormsResult` フォームを取得し `outputContent` ます。 このフィールドには、インタラクティブフォームを表す `BLOB` オブジェクトが格納されます。


1. インタラクティブフォームに署名する

   オブジェクトの `SignatureServiceClient``sign` メソッドを呼び出し、次の値を渡して、PDFドキュメントに署名します。

   * A `BLOB` object that represents the PDF document to sign. Formsサービスから返される `BLOB` インスタンスを使用します。
   * 署名された署名フィールドの名前を表すstring値です。
   * A `Credential` object that represents the credential that is used to digitally sign the PDF document. コンストラクターを使用して `Credential` オブジェクトを作成し、オブジェクトのプロパティに値を割り当ててエイリアスを指定し `Credential` ま `alias` す。
   * PDFドキュメントのダイジェストの作成に使用するハッシュアルゴリズムを表す静的データメンバーを指定する `HashAlgorithm` オブジェクトです。 例えば、SHA1アルゴリズム `HashAlgorithm.SHA1` を使用するように指定できます。
   * ハッシュアルゴリズムを使用するかどうかを指定するBoolean値です。
   * PDFドキュメントがデジタル署名された理由を表すstring値です。
   * 署名者の場所を表すstring値です。
   * 署名者の連絡先情報を表すstring値です。
   * 電子署名の外観を制御する `PDFSignatureAppearanceOptions` オブジェクトです。 例えば、このオブジェクトを使用して、電子署名にカスタムロゴを追加できます。
   * 署名者の証明書に対して失効確認を実行するかどうかを指定する `System.Boolean` オブジェクトです。 この失効確認が行われると、署名に埋め込まれます。 デフォルトは、`false` です。
   * オンライン証明書ステータスプロトコル(OCSP)サポートの環境設定を格納する `OCSPPreferences` オブジェクトです。 失効確認が実行されない場合、このパラメーターは使用されず、指定でき `null`ます。 このオブジェクトについて詳しくは、『 [AEM FormsAPIリファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)』を参照してください。
   * 証明書失効リスト(CRL)の環境設定を格納する `CRLPreferences` オブジェクトです。 失効確認が実行されない場合、このパラメーターは使用されず、指定でき `null`ます。
   * タイムスタンププロバイダー(TSP)でサポートされる環境設定を格納する `TSPPreferences` オブジェクトです。 このパラメーターはオプションで、を指定でき `null`ます。

   署名済みPDFドキュメントを表す `sign``BLOB` オブジェクトを返します。

1. 署名済みPDFドキュメントの保存

   * Create a `System.IO.FileStream` object by invoking its constructor. 署名済みPDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * メソッドが返した `BLOB` オブジェクトの内容を格納するバイト配列を作成し `sign` ます。 オブジェクトのデータメンバーの値を取得して、 `BLOB` バイト配列を入力し `MTOM` ます。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡して、バイト配列の内容をPDFファイルに書き込み `System.IO.BinaryWriter` ま `Write` す。

**関連トピック**

[インタラクティブフォームへのデジタル署名](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## PDF ドキュメントの認証 {#certifying-pdf-documents}

認証署名と呼ばれる特定のタイプの署名によって PDF ドキュメントを認証することで、PDF ドキュメントを保護することができます。認証署名は、以下の方法で電子署名と区別されます。

* 認証署名は PDF ドキュメントに適用される最初の署名です。つまり、認証署名が適用されるときは、ドキュメント内の他の署名フィールドは未署名でなければいけません。認証署名は 1 つの PDF ドキュメントにつき 1 つです。PDF ドキュメントを署名および認証するには、署名の前に認証を行う必要があります。PDF ドキュメントの認証後、他の署名フィールドに電子署名を行うことができます。
* ドキュメントの作成者または発信者は、認証署名を無効にすることなく、特定の方法でドキュメントの変更が可能になるように指定することができます。例えば、フォームへの入力やコメント入力を許可するドキュメントなどがあります。作成者が特定の変更を許可しないように設定を行った場合は、Acrobat はユーザーのその方法によるドキュメントの変更を制限します。別のアプリケーションを使用するなどしてそのような変更が行われた場合は、認証署名は無効となり、Acrobat はユーザーがドキュメントを開いた際に警告を発します。（未認証の署名では、変更を防ぐことはできません。また、通常の編集操作では元の署名は無効になりません。）
* 署名時に、ドキュメントのコンテンツにあいまいさや誤解をもたらす可能性のある、特定の種類のコンテンツをスキャンします。例えば、注釈により、認証される対象を把握するために重要なページ上のテキストが隠れてしまう場合があります。そのようなコンテンツに関する、説明（法的証明）を提供することができます。

SignatureサービスJava APIまたはSignature WebサービスAPIを使用して、PDFドキュメントをプログラムで認証できます。 PDFドキュメントを認証する場合は、秘密鍵証明書サービスに存在するセキュリティ秘密鍵証明書を参照する必要があります。 セキュリティ証明書について詳しくは、使用しているアプリケーションサーバー版の『 *AEM Formsのインストールおよびデプロイ* 』ガイドを参照してください。

>[!NOTE]
>
>同じPDFドキュメントの認証および署名時に、認証署名が信頼されていない場合、AcrobatまたはAdobe ReaderでPDFドキュメントを開くと、最初の署名の横に黄色い三角形が表示されます。 この状況を回避するには、認証署名を信頼する必要があります。

>[!NOTE]
>
>PDFドキュメントの署名や認証にnCipher nShield HSM秘密鍵証明書を使用する場合、AEM FormsがデプロイされるJ2EEアプリケーションサーバーを再起動するまで、新しい秘密鍵証明書は使用できません。 ただし、設定値を設定すると、J2EEアプリケーションサーバーを再起動しなくても、署名または認証の操作が動作します。

次の設定値をcknfastrcファイルに追加できます。このファイルは/opt/nfast/cknfastrc(またはc:\nfast\cknfastrc)にあります。

```shell
    CKNFAST_ASSUME_SINGLE_PROCESS=0
```

この設定値をcknfastrcファイルに追加すると、J2EEアプリケーションサーバーを再起動しなくても、新しい秘密鍵証明書を使用できます。

>[!NOTE]
>
>Signatureサービスとドキュメントの認証について詳しくは、『AEM Forms用 [サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順の概要 {#summary_of_steps-5}

PDFドキュメントを認証するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. 署名クライアントを作成します。
1. 認証するPDFドキュメントを取得します。
1. PDFドキュメントを認証します。
1. 認証済みPDFドキュメントをPDFファイルとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(AEM FormsがJBossにデプロイされている場合に必要)
* jbossall-client.jar(AEM FormsがJBossにデプロイされている場合に必要)

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**署名クライアントの作成**

プログラムによってSignature操作を実行する前に、Signatureクライアントを作成する必要があります。

**認証用のPDFドキュメントの取得**

PDFドキュメントを認証するには、署名フィールドを含むPDFドキュメントを取得する必要があります。 PDFドキュメントに署名フィールドが含まれていない場合は、認証できません。 署名フィールドは、Designerを使用して追加することも、プログラムを使用して追加することもできます。 プログラムによる署名フィールドの追加について詳しくは、「署名フィールドの [追加](digitally-signing-certifying-documents.md#adding-signature-fields)」を参照してください。

**PDFドキュメントの認証**

PDFドキュメントを正常に認証するには、SignatureサービスでPDFドキュメントの認証に使用される次の入力値が必要です。

* **PDFドキュメント**: 署名フィールドを含むPDFドキュメントです。署名フィールドは、認証署名のグラフィック表現を含むフォームフィールドです。 PDFドキュメントを認証するには、その前に署名フィールドがPDF署名に含まれている必要があります。 署名フィールドは、Designerを使用して追加することも、プログラムを使用して追加することもできます。 (署名フィールドの [追加を参照](digitally-signing-certifying-documents.md#adding-signature-fields))。
* **署名フィールド名**: 認証される署名フィールドの完全修飾名です。 次の値は例です。 `form1[0].#subform[1].SignatureField3[3]`. XFAフォームフィールドを使用する場合は、署名フィールドの名前の一部を使用することもできます。 `SignatureField3[3]`. フィールド名にnull値が渡されると、非表示の署名フィールドが動的に作成され、認証されます。
* **セキュリティ証明書**: PDFドキュメントの認証に使用する秘密鍵証明書です。 このセキュリティ証明書には、パスワードとエイリアスが含まれています。これは、Credentialサービス内の秘密鍵証明書に表示されるエイリアスと一致する必要があります。 エイリアスは、PKCS#12ファイル（拡張子.pfx付き）またはハードウェアセキュリティモジュール(HSM)内の実際の秘密鍵証明書への参照です。
* **ハッシュアルゴリズム**: PDFドキュメントのダイジェストの作成に使用するハッシュアルゴリズムです。
* **署名の理由**: PDFドキュメントが認証された理由を他のユーザーが把握できるようにAcrobatまたはAdobe Readerで表示される値です。
* **署名者の場所**: 秘密鍵証明書で指定された署名者の場所です。
* **連絡先情報**: 署名者の住所や電話番号などの連絡先情報。
* **権限情報**: 認証署名を無効にすることなく、エンドユーザーがドキュメントに対して実行できる操作を制御する権限です。 例えば、権限を設定して、PDFドキュメントを変更すると認証署名が無効になるようにすることができます。
* **法的説明**: ドキュメントを認証すると、ドキュメントのコンテンツをあいまいにしたり誤解を招く可能性のある、特定のタイプのコンテンツを自動的にスキャンします。 例えば、注釈により、認証される対象を把握するために重要なページ上のテキストが隠れてしまう場合があります。スキャン処理では、この種のコンテンツに関する警告が生成されます。 この値は、警告が生成された可能性のあるコンテンツに関する追加の説明を提供します。
* **外観オプション**: 認証署名の外観を制御するオプションです。 例えば、認証署名には日付情報を表示できます。
* **失効確認**: この値は、署名者の証明書に対して失効確認を行うかどうかを指定します。 デフォルト設定ので `false` は、失効確認は行われません。
* **OCSP settings**: PDFドキュメントの認証に使用される秘密鍵証明書のステータスに関する情報を提供する、オンライン証明書ステータスプロトコル(OCSP)サポートの設定です。 例えば、PDFドキュメントへのサインオンに使用する秘密鍵証明書に関する情報を提供するサーバーのURLを指定できます。
* **CRL settings**: 失効確認が行われた場合の証明書失効リスト(CRL)の環境設定です。 例えば、秘密鍵証明書が失効したかどうかを常に確認するように指定できます。
* **タイムスタンプ**: 認証署名に適用されるタイムスタンプ情報を定義する設定です。 タイムスタンプは、特定のデータが特定の時間の前に確立されたことを示します。 この情報は、署名者と検証者の間に信頼関係を構築するのに役立ちます。

**認証済みPDFドキュメントをPDFファイルとして保存する**

SignatureサービスがPDFドキュメントを認証したら、PDFファイルとして保存して、ユーザーがAcrobatまたはAdobe Readerで開けるようにできます。

**関連トピック**

[Java APIを使用したPDFドキュメントの認証](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-java-api)

[WebサービスAPIを使用したPDFドキュメントの認証](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[署名フィールドの追加](digitally-signing-certifying-documents.md#adding-signature-fields)

### Java APIを使用したPDFドキュメントの認証 {#certify-pdf-documents-using-the-java-api}

Signature API(Java)を使用してPDFドキュメントを認証します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-signatures-client.jarなどのクライアントJARファイルを含めます。

1. 署名クライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `SignatureServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 認証用のPDFドキュメントの取得

   * コンストラクターを使用し、PDFドキュメントの場所を指定するstring値を渡して、認証するPDFドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PDFドキュメントの認証

   オブジェクトの `SignatureServiceClient` メソッドを呼び出し、次の値を渡して、PDFドキュメントを認証し `certify` ます。

   * 認証するPDFドキュメントを表す `com.adobe.idp.Document` オブジェクトです。
   * 署名を含む署名フィールドの名前を表すstring値です。
   * A `Credential` object that represents the credential that is used to certify the PDF document. オブジェクトの静的な `Credential` メソッドを呼び出し、セキュリティ証明書に対応するエイリアス値を指定する文字列値を渡して、 `Credential``getInstance` オブジェクトを作成します。
   * PDFドキュメントのダイジェストの作成に使用されるハッシュアルゴリズムを表す静的データメンバーを指定する `HashAlgorithm` オブジェクトです。 例えば、SHA1アルゴリズム `HashAlgorithm.SHA1` を使用するように指定できます。
   * PDFドキュメントが認証された理由を表すstring値です。
   * 署名者の連絡先情報を表すstring値です。
   * 署名を無効にするPDFドキュメントで実行できるアクションを指定する `MDPPermissions` オブジェクトです。
   * 認証署名の外観を制御する `PDFSignatureAppearanceOptions` オブジェクトです。 必要に応じて、などのメソッドを呼び出して、署名の外観を変更し `setShowDate`ます。
   * 署名を無効にするアクションについての説明を提供するstring値です。
   * 署名者の証明書に対して失効確認を実行するかどうかを指定する `java.lang.Boolean` オブジェクトです。 この失効確認が行われると、署名に埋め込まれます。 デフォルトは、`false` です。
   * 認証する署名フィールドがロックされているかどうかを指定する `java.lang.Boolean` オブジェクトです。 フィールドをロックすると、署名フィールドは読み取り専用としてマークされ、プロパティを変更できなくなり、必要な権限を持たないユーザーはこのフィールドをクリアできなくなります。 デフォルトは、`false` です。
   * オンライン証明書ステータスプロトコル(OCSP)サポートの環境設定を格納する `OCSPPreferences` オブジェクトです。 失効確認が実行されない場合、このパラメーターは使用されず、指定でき `null`ます。 このオブジェクトについて詳しくは、『 [AEM FormsAPIリファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)』を参照してください。
   * 証明書失効リスト(CRL)の環境設定を格納する `CRLPreferences` オブジェクトです。 失効確認が実行されない場合、このパラメーターは使用されず、指定でき `null`ます。
   * タイムスタンププロバイダー(TSP)でサポートされる環境設定を格納する `TSPPreferences` オブジェクトです。 例えば、 `TSPPreferences` オブジェクトを作成した後、オブジェクトの `TSPPreferences``setTspServerURL` メソッドを呼び出して、TSPサーバーのURLを設定できます。 このパラメーターはオプションで、を指定でき `null`ます。 For more information, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

   認証済みのPDFドキュメントを表す `certify``com.adobe.idp.Document` オブジェクトを返します。

1. 認証済みPDFドキュメントをPDFファイルとして保存する

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が .pdf であることを確認します。
   * Invoke the `com.adobe.idp.Document` object’s `copyToFile` method to copy the contents of the `com.adobe.idp.Document` object to the file.

**関連トピック**

[PDF ドキュメントの認証](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[クイック開始（SOAPモード）: Java APIを使用したPDFドキュメントの認証](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-certifying-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したPDFドキュメントの認証 {#certify-pdf-documents-using-the-web-service-api}

Signature API（Webサービス）を使用してPDFドキュメントを認証します。

1. プロジェクトファイルを含める

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >サーバーホスト `localhost` AEM FormsのIPアドレスに置き換えます。

1. 署名クライアントの作成

   * Create a `SignatureServiceClient` object by using its default constructor.
   * Create a `SignatureServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/SignatureService?WSDL`)に渡すstring値を渡します。 属性を使用する必要はありません `lc_version` 。 この属性は、サービス参照を作成する場合に使用されます)。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `SignatureServiceClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールドにAEM formsのユーザー名を割り当て `SignatureServiceClient.ClientCredentials.UserName.UserName`ます。
      * 対応するパスワード値をフィールドに割り当て `SignatureServiceClient.ClientCredentials.UserName.Password`ます。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当て `BasicHttpBindingSecurity.Security.Mode`ます。

1. 認証用のPDFドキュメントの取得

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、認証済みのPDFドキュメントの保存に使用されます。
   * コンストラクターを呼び出し、認証するPDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
   * オブジェクトの `System.IO.FileStream``Read` メソッドを呼び出し、読み取るバイト配列、開始位置およびストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * データメンバにバイト配列の内容を割り当てて、 `BLOB``MTOM` オブジェクトを入力します。

1. PDFドキュメントの認証

   オブジェクトの `SignatureServiceClient` メソッドを呼び出し、次の値を渡して、PDFドキュメントを認証し `certify` ます。

   * 認証するPDFドキュメントを表す `BLOB` オブジェクトです。
   * 署名を含む署名フィールドの名前を表すstring値です。
   * A `Credential` object that represents the credential that is used to certify the PDF document. コンストラクターを使用して `Credential` オブジェクトを作成し、オブジェクトのプロパティに値を割り当ててエイリアスを指定し `Credential` ま `alias` す。
   * PDFドキュメントのダイジェストの作成に使用されるハッシュアルゴリズムを表す静的データメンバーを指定する `HashAlgorithm` オブジェクトです。 例えば、SHA1アルゴリズム `HashAlgorithm.SHA1` を使用するように指定できます。
   * ハッシュアルゴリズムを使用するかどうかを指定するBoolean値です。
   * PDFドキュメントが認証された理由を表すstring値です。
   * 署名者の場所を表すstring値です。
   * 署名者の連絡先情報を表すstring値です。
   * 署名を無効にするPDFドキュメントで実行できるアクションを指定する `MDPPermissions` オブジェクトの静的データメンバーです。
   * 前のパラメーター値として渡された `MDPPermissions` オブジェクトを使用するかどうかを指定するBoolean値です。
   * 署名を無効にするアクションを説明するstring値です。
   * 認証署名の外観を制御する `PDFSignatureAppearanceOptions` オブジェクトです。 コンストラクタを使用して `PDFSignatureAppearanceOptions` オブジェクトを作成します。データメンバーの1つを設定して、署名の外観を変更できます。
   * 署名者の証明書に対して失効確認を実行するかどうかを指定する `System.Boolean` オブジェクトです。 この失効確認が行われると、署名に埋め込まれます。 デフォルトは、`false` です。
   * 認証する署名フィールドがロックされているかどうかを指定する `System.Boolean` オブジェクトです。 フィールドをロックすると、署名フィールドは読み取り専用としてマークされ、プロパティを変更できなくなり、必要な権限を持たないユーザーはこのフィールドをクリアできなくなります。 デフォルトは、`false` です。
   * 署名フィールドをロックするかどうかを指定する `System.Boolean` オブジェクトです。 つまり、前のパラメーター `true` に渡した場合は、このパラメーター `true` に渡します。
   * オンライン証明書ステータスプロトコル(OCSP)サポートの環境設定を格納する `OCSPPreferences` オブジェクトです。PDFドキュメントの認証に使用される秘密鍵証明書のステータスに関する情報を提供します。 失効確認が実行されない場合、このパラメーターは使用されず、指定でき `null`ます。
   * 証明書失効リスト(CRL)の環境設定を格納する `CRLPreferences` オブジェクトです。 失効確認が実行されない場合、このパラメーターは使用されず、指定でき `null`ます。
   * タイムスタンププロバイダー(TSP)でサポートされる環境設定を格納する `TSPPreferences` オブジェクトです。 例えば、 `TSPPreferences` オブジェクトを作成した後に、オブジェクトの `TSPPreferences``tspServerURL` データメンバーを設定して、TSPのURLを設定できます。 このパラメーターはオプションで、を指定でき `null`ます。

   認証済みのPDFドキュメントを表す `certify``BLOB` オブジェクトを返します。

1. 認証済みPDFドキュメントをPDFファイルとして保存する

   * コンストラクターを呼び出し、認証済みのPDF `System.IO.FileStream` ドキュメントと、そのファイルを開くモードを含むPDFドキュメントのファイルの場所を表すstring値を渡して、オブジェクトを作成します。
   * メソッドが返した `BLOB` オブジェクトの内容を格納するバイト配列を作成し `certify` ます。 オブジェクトのデータメンバーの値を取得して、 `BLOB` バイト配列を入力し `binaryData` ます。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡して、バイト配列の内容をPDFファイルに書き込み `System.IO.BinaryWriter` ま `Write` す。

**関連トピック**

[PDF ドキュメントの認証](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Verifying Digital Signatures {#verifying-digital-signatures}

電子署名を検証することで、署名された PDF ドキュメントに変更がなく、電子署名が有効であることを確認することができます。電子署名を検証する際に、署名のステータスや、署名者のIDなどの署名のプロパティを確認できます。 電子署名を信用する前に、検証することをおすすめします。電子署名を検証する際、電子署名を含む PDF ドキュメントを参照します。

署名者のIDが不明であるとします。 次の図に示すように、AcrobatでPDFドキュメントを開くと、署名者のIDが不明であることを示す警告メッセージが表示されます。

![vd_vd_verifysig](assets/vd_vd_verifysig.png)

同様に、プログラムで電子署名を検証する場合、署名者のIDのステータスを判断できます。 例えば、前の図に示すドキュメントで電子署名を検証すると、署名者のIDが不明になります。

>[!NOTE]
>
>Signatureサービスと電子署名の検証について詳しくは、『 [AEM Forms用サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順の概要 {#summary_of_steps-6}

電子署名を検証するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. 署名クライアントを作成します。
1. 検証する署名が含まれているPDFドキュメントを取得します。
1. PKIランタイムオプションを設定します。
1. 電子署名を検証します。
1. 署名のステータスを決定します。
1. 署名者のIDを決定します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを含めます。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(AEM FormsがJBossにデプロイされている場合に必要)
* jbossall-client.jar(AEM FormsがJBossにデプロイされている場合に必要)

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**署名クライアントの作成**

プログラムを使用してSignatureサービス操作を実行する前に、Signatureサービスクライアントを作成します。

**検証する署名が含まれているPDFドキュメントを取得します**

PDF署名のデジタル署名や認証に使用されるドキュメントを検証するには、署名が含まれるPDFドキュメントを取得します。

**PKIランタイムオプションの設定**

PDFドキュメントの署名を検証する際にSignatureサービスで使用する次のPKIランタイムオプションを設定します。

* 検証時刻
* 失効確認
* タイムスタンプ値

これらのオプションの設定の一環として、検証時刻を指定できます。 例えば、現在の時間（バリデーターのコンピューター上の時間）を選択できます。これは現在の時間を使用することを示します。 様々な時間値について詳しくは、 `VerificationTime` AEM FormsAPIリファレンスの [定義済みリスト値を参照してください](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

検証プロセスの一環として失効確認を実行するかどうかを指定することもできます。 例えば、失効確認を実行して、証明書が失効したかどうかを判断できます。 失効確認オプションについて詳しくは、『 `RevocationCheckStyle` AEM FormsAPIリファレンス』の「 [定義済みリストの値」を参照してください](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

証明書に対して失効確認を実行するには、 `CRLOptionSpec` オブジェクトを使用して、証明書失効リスト(CRL)サーバーへのURLを指定します。 ただし、URLをCRLサーバーに指定しない場合、Signatureサービスは証明書からURLを取得します。

失効確認を実行する際は、CRLサーバーを使用する代わりに、オンライン証明書ステータスプロトコル(OCSP)サーバーを使用できます。 通常、CRLサーバーとは異なり、OCSPサーバーを使用する場合は、失効確認の実行が高速になります。 (See [Online Certificate Status Protocol](https://tools.ietf.org/html/rfc2560).)

Signatureサービスで使用するCRLおよびOCSPサーバーの順序は、Adobe Applications and Servicesを使用して設定できます。 例えば、Adobe Applications and ServicesでOCSPサーバーが最初に設定されている場合は、OCSPサーバーを確認し、次にCRLサーバーを確認します。

失効確認を実行しない場合、Signatureサービスでは、証明書が失効したかどうかを確認しません。 つまり、CRLおよびOCSPサーバー情報は無視されます。

>[!NOTE]
>
>証明書で指定されたURLは、とオブジェクトを使用して上書き `CRLOptionSpec` でき `OCSPOptionSpec` ます。 例えば、CRLサーバーを上書きするには、 `CRLOptionSpec` オブジェクトの `setLocalURI` メソッドを呼び出します。

タイムスタンプとは、署名済みまたは認証済みのドキュメントが変更された時間を追跡するプロセスです。 ドキュメントに署名した後は、誰もその署名を変更できません。 タイムスタンプ機能を使用すると、署名済みまたは認証済みのドキュメントの有効性を強化できます。 タイムスタンプオプションは、 `TSPOptionSpec` オブジェクトを使用して設定できます。 例えば、タイムスタンププロバイダー(TSP)サーバーのURLを指定できます。

>[!NOTE]
>
>JavaおよびWebサービスのクイック開始では、検証時刻はに、失効確認は `VerificationTime.CURRENT_TIME` に設定され `RevocationCheckStyle.BestEffort`ます。 CRLまたはOCSPサーバー情報が指定されていないので、サーバー情報は証明書から取得されます。

**電子署名の検証**

署名を正しく検証するには、署名が含まれる署名フィールドの完全修飾名を指定します（例：） `form1[0].#subform[1].SignatureField3[3]`。 XFAフォームフィールドを使用する場合は、署名フィールドの名前の一部を使用することもできます。 `SignatureField3`.

デフォルトでは、Signatureサービスでは、検証後にドキュメントに署名できる時間が65分に制限されます。 ユーザーが現在の時刻に署名を検証しようとしたときに、署名時刻が現在の時刻より後で65分以内になった場合、Signatureサービスでは検証エラーは作成されません。

>[!NOTE]
>
>署名の検証時に必要なその他の値については、『 [AEM FormsAPIリファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)』を参照してください。

**署名のステータスの確認**

電子署名の検証中に、署名のステータスを確認できます。

**署名者のIDの確認**

署名者のIDを特定できます。次の値のいずれかになります。

* **不明**: 署名者の検証を実行できないため、署名者が不明です。
* **信頼済み**: この署名者は信頼されています。
* **信頼できません**: この署名者は信頼されていません。

**関連トピック**

[Java APIを使用した電子署名の検証](#verify-digital-signatures-using-the-java-api)

[WebサービスAPIを使用した電子署名の検証](#verify-digital-signatures-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java APIを使用した電子署名の検証 {#verify-digital-signatures-using-the-java-api}

Signature Service API(Java)を使用して電子署名を検証します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-signatures-client.jarなどのクライアントJARファイルを含めます。

1. 署名クライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `SignatureServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 検証する署名が含まれているPDFドキュメントを取得します

   * 検証する署名が含まれているPDFドキュメントを表す `java.io.FileInputStream` オブジェクトを、コンストラクターを使用して作成します。 PDFドキュメントの場所を指定するstring値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PKIランタイムオプションの設定

   * コンストラクタを使用して `PKIOptions` オブジェクトを作成します。
   * 検証時刻を設定するには、 `PKIOptions` オブジェクトの `setVerificationTime` メソッドを呼び出し、検証時刻を指定する `VerificationTime` 定義済みリスト値を渡します。
   * 失効確認オプションを設定するには、 `PKIOptions` オブジェクトの `setRevocationCheckStyle` メソッドを呼び出し、失効確認を実行するかどうかを指定する `RevocationCheckStyle` 定義済みリスト値を渡します。

1. 電子署名の検証

   オブジェクトの `SignatureServiceClient``verify2` メソッドを呼び出し、次の値を渡して署名を検証します。

   * デジタル署名された、または認証されたPDFドキュメントを含む `com.adobe.idp.Document` オブジェクトです。
   * 検証する署名が含まれている署名フィールド名を表すstring値です。
   * PKI実行時オプションを含む `PKIOptions` オブジェクトです。
   * SPI情報を含む `VerifySPIOptions` インスタンスです。 このパラメーター `null` を指定できます。

   この `verify2``PDFSignatureVerificationInfo` メソッドは、電子署名の検証に使用できる情報を含むオブジェクトを返します。

1. 署名のステータスの確認

   * オブジェクトのメソッドを呼び出して、署名のステータス `PDFSignatureVerificationInfo` を特定し `getStatus` ます。 このメソッドは、署名ステータスを指定する `SignatureStatus` オブジェクトを返します。 例えば、署名済みPDFドキュメントが変更されていない場合、このメソッドはを返し `SignatureStatus.DocumentSigNoChanges`ます。

1. 署名者のIDの確認

   * オブジェクトのメソッドを呼び出して、署名者のID `PDFSignatureVerificationInfo` を特定し `getSigner` ます。 このメソッドは、 `IdentityInformation` オブジェクトを返します。
   * 署名者のIDを決定するために、 `IdentityInformation` オブジェクトの `getStatus` メソッドを呼び出します。 このメソッドは、IDを指定する `IdentityStatus` 定義済みリスト値を返します。 例えば、署名者が信頼できる場合、このメソッドは、を返し `IdentityStatus.TRUSTED`ます。

**関連トピック**

[電子署名の検証](#verify-digital-signatures-using-the-java-api)

[クイック開始（SOAPモード）: Java APIを使用したデジタル署名の検証](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-a-digital-signature-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用した電子署名の検証 {#verify-digital-signatures-using-the-web-service-api}

Signature Service API（Webサービス）を使用して電子署名を検証します。

1. プロジェクトファイルを含める

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >サーバーホスト `localhost` AEM FormsのIPアドレスに置き換えます。

1. 署名クライアントの作成

   * Create a `SignatureServiceClient` object by using its default constructor.
   * Create a `SignatureServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/SignatureService?WSDL`)に渡すstring値を渡します。 属性を使用する必要はありません `lc_version` 。 この属性は、サービス参照を作成する場合に使用されます)。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `SignatureServiceClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールドにAEM formsのユーザー名を割り当て `SignatureServiceClient.ClientCredentials.UserName.UserName`ます。
      * 対応するパスワード値をフィールドに割り当て `SignatureServiceClient.ClientCredentials.UserName.Password`ます。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当て `BasicHttpBindingSecurity.Security.Mode`ます。

1. 検証する署名が含まれているPDFドキュメントを取得します

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、検証するデジタル署名または認証署名が含まれているPDFドキュメントの保存に使用されます。
   * Create a `System.IO.FileStream` object by invoking its constructor. 署名済みPDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
   * オブジェクトのメソッドを呼び出して、バイト配列にストリームデータ `System.IO.FileStream` を入力し `Read` ます。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * オブジェクトのプロパティにバイト配列の内容を割り当てて、 `BLOB``MTOM` オブジェクトを入力します。

1. PKIランタイムオプションの設定

   * コンストラクタを使用して `PKIOptions` オブジェクトを作成します。
   * 検証時刻を設定するには、 `PKIOptions` オブジェクトの `verificationTime` データメンバに検証時刻を指定する `VerificationTime` 定義済みリスト値を割り当てます。
   * 失効確認オプションを設定するには、 `PKIOptions` オブジェクトの `revocationCheckStyle` データメンバに失効確認を実行するかどうかを指定する `RevocationCheckStyle` 定義済みリスト値を割り当てます。

1. 電子署名の検証

   オブジェクトの `SignatureServiceClient``verify2` メソッドを呼び出し、次の値を渡して署名を検証します。

   * デジタル署名された、または認証されたPDFドキュメントを含む `BLOB` オブジェクトです。
   * 検証する署名が含まれている署名フィールド名を表すstring値です。
   * PKI実行時オプションを含む `PKIOptions` オブジェクトです。
   * SPI情報を含む `VerifySPIOptions` インスタンスです。 このパラメーター `null` を指定できます。

   この `verify2``PDFSignatureVerificationInfo` メソッドは、電子署名の検証に使用できる情報を含むオブジェクトを返します。

1. 署名のステータスの確認

   オブジェクトの `PDFSignatureVerificationInfo``status` データメンバーの値を取得して、署名のステータスを決定します。 このデータメンバーには、署名のステータスを指定する `SignatureStatus` オブジェクトが格納されます。 例えば、署名済みPDFドキュメントが変更された場合、 `status` データメンバーに値が格納され `SignatureStatus.DocumentSigNoChanges`ます。

1. 署名者のIDの確認

   * オブジェクトのデータメンバーの値を取得して、署名者のID `PDFSignatureVerificationInfo``signer` を特定します。 このメンバは、 `IdentityInformation` オブジェクトを返します。
   * 署名者のIDを特定する `IdentityInformation` オブジェクトの `status` データメンバーを取得します。 このデータメンバは、IDを指定する `IdentityStatus` 定義済みリスト値を返します。 例えば、署名者が信頼できる場合、このメンバーは、を返し `IdentityStatus.TRUSTED`ます。

**関連トピック**

[電子署名の検証](#verify-digital-signatures-using-the-java-api)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Verifying Multiple Digital Signatures {#verifying-multiple-digital-signatures}

AEM Formsは、PDFドキュメント内のすべての電子署名を検証する手段を提供します。 複数の署名者からの署名が必要なビジネスプロセスの結果として、PDFドキュメントに複数の電子署名が含まれているとします。 例えば、融資担当者の署名と管理者の署名の両方が必要な金融トランザクションについて考えてみましょう。 SignatureサービスのJava APIまたはWebサービスのAPIを使用して、PDFドキュメント内のすべての署名を検証できます。 複数の署名を検証する際は、それぞれの署名のステータスやプロパティを確認できます。電子署名を信頼する前に、検証することをお勧めします。 単一の電子署名の検証について詳しく知ることをお勧めします。

>[!NOTE]
>
>Signatureサービスと電子署名の検証について詳しくは、『 [AEM Forms用サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順の概要 {#summary_of_steps-7}

複数の電子署名を検証するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. 署名クライアントを作成します。
1. 検証する署名が含まれているPDFドキュメントを取得します。
1. PKIランタイムオプションを設定します。
1. すべての電子署名を取得します。
1. すべての署名を繰り返し実行します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを含めます。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(AEM FormsがJBossにデプロイされている場合に必要)
* jbossall-client.jar(AEM FormsがJBossにデプロイされている場合に必要)

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**署名クライアントの作成**

プログラムを使用してSignatureサービス操作を実行する前に、Signatureサービスクライアントを作成します。

**検証する署名が含まれているPDFドキュメントを取得します**

PDF署名のデジタル署名や認証に使用されるドキュメントを検証するには、署名が含まれるPDFドキュメントを取得します。

**PKIランタイムオプションの設定**

PDFドキュメントのすべての署名を検証する際にSignatureサービスで使用する次のPKIランタイムオプションを設定します。

* 検証時刻
* 失効確認
* タイムスタンプ値

これらのオプションの設定の一環として、検証時刻を指定できます。 例えば、現在の時間（バリデーターのコンピューター上の時間）を選択できます。これは現在の時間を使用することを示します。 様々な時間値について詳しくは、 `VerificationTime` AEM FormsAPIリファレンスの [定義済みリスト値を参照してください](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

検証プロセスの一環として失効確認を実行するかどうかを指定することもできます。 例えば、失効確認を実行して、証明書が失効したかどうかを判断できます。 失効確認オプションについて詳しくは、『 `RevocationCheckStyle` AEM FormsAPIリファレンス』の「 [定義済みリストの値」を参照してください](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

証明書に対して失効確認を実行するには、 `CRLOptionSpec` オブジェクトを使用して、証明書失効リスト(CRL)サーバーへのURLを指定します。 ただし、CRLサーバーへのURLを指定しない場合、Signatureサービスは証明書からURLを取得します。

失効確認を実行する際は、CRLサーバーを使用する代わりに、オンライン証明書ステータスプロトコル(OCSP)サーバーを使用できます。 通常、CRLサーバーではなくOCSPサーバーを使用する場合は、失効確認の実行が高速になります。 (See [Online Certificate Status Protocol](https://tools.ietf.org/html/rfc2560).)

Signatureサービスで使用するCRLおよびOCSPサーバーの順序は、Adobe Applications and Servicesを使用して設定できます。 例えば、Adobe Applications and ServicesでOCSPサーバーが最初に設定されている場合は、OCSPサーバーがチェックされ、次にCRLサーバーがチェックされます。

失効確認を実行しない場合、Signatureサービスでは、証明書が失効したかどうかを確認しません。 つまり、CRLおよびOCSPサーバー情報は無視されます。

>[!NOTE]
>
>証明書で指定されたURLは、とオブジェクトを使用して上書き `CRLOptionSpec` でき `OCSPOptionSpec` ます。 例えば、CRLサーバーを上書きするには、 `CRLOptionSpec` オブジェクトの `setLocalURI` メソッドを呼び出します。

タイムスタンプとは、署名済みまたは認証済みのドキュメントが変更された時間を追跡するプロセスです。 ドキュメントに署名した後は、誰もその署名を変更できません。 タイムスタンプ機能を使用すると、署名済みまたは認証済みのドキュメントの有効性を強化できます。 タイムスタンプオプションは、 `TSPOptionSpec` オブジェクトを使用して設定できます。 例えば、タイムスタンププロバイダー(TSP)サーバーのURLを指定できます。

>[!NOTE]
>
>JavaおよびWebサービスのクイック開始では、検証時刻はに、失効確認は `VerificationTime.CURRENT_TIME` に設定され `RevocationCheckStyle.BestEffort`ます。 CRLまたはOCSPサーバー情報が指定されていないので、サーバー情報は証明書から取得されます。

**すべての電子署名を取得する**

PDFドキュメント内のすべての電子署名を検証するには、PDFドキュメントから電子署名を取得します。 すべての署名がリストで返されます。 電子署名の検証の一環として、署名のステータスを確認します。

>[!NOTE]
>
>1つの電子署名を検証する場合とは異なり、複数の署名を検証する場合は、署名フィールド名を指定する必要はありません。

**すべての署名を繰り返し実行**

各署名を繰り返し処理します。 つまり、各署名について、デジタル署名を検証し、署名者のIDと各署名のステータスを確認します。 (デジタル署名の [検証を参照](#verify-digital-signatures-using-the-java-api))。

>[!NOTE]
>
>ドキュメント全体が要件の場合は、すべての署名を繰り返し実行する必要はありません。

**関連トピック**

[Java APIを使用した複数の電子署名の検証](#verify-digital-signatures-using-the-java-api)

[WebサービスAPIを使用した複数の電子署名の検証](#verify-digital-signatures-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java APIを使用した複数の電子署名の検証 {#verify-multiple-digital-signatures-using-the-java-api}

Signature Service API(Java)を使用して複数の電子署名を検証します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-signatures-client.jarなどのクライアントJARファイルを含めます。

1. 署名クライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `SignatureServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 検証する署名が含まれているPDFドキュメントを取得します

   * 複数の電子署名を含むPDFドキュメントを表す `java.io.FileInputStream` オブジェクトを作成し、そのコンストラクターを使用して検証を行います。 PDFドキュメントの場所を指定するstring値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PKIランタイムオプションの設定

   * コンストラクタを使用して `PKIOptions` オブジェクトを作成します。
   * 検証時刻を設定するには、 `PKIOptions` オブジェクトの `setVerificationTime` メソッドを呼び出し、検証時刻を指定する `VerificationTime` 定義済みリスト値を渡します。
   * 失効確認オプションを設定するには、 `PKIOptions` オブジェクトの `setRevocationCheckStyle` メソッドを呼び出し、失効確認を実行するかどうかを指定する `RevocationCheckStyle` 定義済みリスト値を渡します。

1. すべての電子署名を取得する

   オブジェクトの `SignatureServiceClient``verifyPDFDocument` メソッドを呼び出し、次の値を渡します。

   * 複数の電子署名を含むPDFドキュメントを含む `com.adobe.idp.Document` オブジェクトです。
   * PKI実行時オプションを含む `PKIOptions` オブジェクトです。
   * SPI情報を含む `VerifySPIOptions` インスタンスです。 このパラメーター `null` を指定できます。

   この `verifyPDFDocument``PDFDocumentVerificationInfo` メソッドは、PDFドキュメント内のすべての電子署名に関する情報を含むオブジェクトを返します。

1. すべての署名を繰り返し実行

   * オブジェクトの `PDFDocumentVerificationInfo``getVerificationInfos` メソッドを呼び出して、すべての署名を繰り返し実行します。 このメソッドは、各要素がオブジェクトである `java.util.List` オブジェクトを返し `PDFSignatureVerificationInfo` ます。 署名のリストを繰り返すには、 `java.util.Iterator` オブジェクトを使用します。
   * この `PDFSignatureVerificationInfo` オブジェクトを使用すると、オブジェクトの `PDFSignatureVerificationInfo``getStatus` メソッドを呼び出して、署名のステータスを特定するなどのタスクを実行できます。 このメソッドは、署名のステータスを通知する静的データメンバーを持つ `SignatureStatus` オブジェクトを返します。 例えば、署名が不明な場合は、このメソッドはを返し `SignatureStatus.DocumentSignatureUnknown`ます。

**関連トピック**

[複数の電子署名の検証](#verifying-multiple-digital-signatures)

[クイック開始（SOAPモード）: Java APIを使用した複数の電子署名の検証](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-multiple-digital-signatures-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[電子署名の検証](#verify-digital-signatures-using-the-java-api)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用した複数の電子署名の検証 {#verifying-multiple-digital-signatures-using-the-web-service-api}

Signature Service API（Webサービス）を使用して複数の電子署名を検証します。

1. プロジェクトファイルを含める

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >サーバーホスト `localhost` AEM FormsのIPアドレスに置き換えます。

1. 署名クライアントの作成

   * Create a `SignatureServiceClient` object by using its default constructor.
   * Create a `SignatureServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/SignatureService?WSDL`)に渡すstring値を渡します。 属性を使用する必要はありません `lc_version` 。 この属性は、サービス参照を作成する場合に使用されます)。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `SignatureServiceClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールドにAEM formsのユーザー名を割り当て `SignatureServiceClient.ClientCredentials.UserName.UserName`ます。
      * 対応するパスワード値をフィールドに割り当て `SignatureServiceClient.ClientCredentials.UserName.Password`ます。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当て `BasicHttpBindingSecurity.Security.Mode`ます。

1. 検証する署名が含まれているPDFドキュメントを取得します

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、検証する複数の電子署名が含まれるPDFドキュメントを保存します。
   * Create a `System.IO.FileStream` object by invoking its constructor. PDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
   * オブジェクトのメソッドを呼び出して、バイト配列にストリームデータ `System.IO.FileStream` を入力し `Read` ます。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * オブジェクトのプロパティにバイト配列の内容を割り当てて、 `BLOB``MTOM` オブジェクトを入力します。

1. PKIランタイムオプションの設定

   * コンストラクタを使用して `PKIOptions` オブジェクトを作成します。
   * 検証時刻を設定するには、 `PKIOptions` オブジェクトの `verificationTime` データメンバに検証時刻を指定する `VerificationTime` 定義済みリスト値を割り当てます。
   * 失効確認オプションを設定するには、 `PKIOptions` オブジェクトの `revocationCheckStyle` データメンバに失効確認を実行するかどうかを指定する `RevocationCheckStyle` 定義済みリスト値を割り当てます。

1. すべての電子署名を取得する

   オブジェクトの `SignatureServiceClient``verifyPDFDocument` メソッドを呼び出し、次の値を渡します。

   * 複数の電子署名を含むPDFドキュメントを含む `BLOB` オブジェクトです。
   * PKI実行時オプションを含む `PKIOptions` オブジェクトです。
   * SPI情報を含む `VerifySPIOptions` インスタンスです。 このパラメーターにはnullを指定できます。

   この `verifyPDFDocument``PDFDocumentVerificationInfo` メソッドは、PDFドキュメント内のすべての電子署名に関する情報を含むオブジェクトを返します。

1. すべての署名を繰り返し実行

   * オブジェクトの `PDFDocumentVerificationInfo``verificationInfos` データメンバーを取得して、すべての署名を繰り返し処理します。 このデータ・メンバは、各要素が `Object``PDFSignatureVerificationInfo` オブジェクトである配列を戻します。
   * この `PDFSignatureVerificationInfo` オブジェクトを使用すると、オブジェクトの `PDFSignatureVerificationInfo``status` データメンバーを取得して、署名のステータスを判断するなどのタスクを実行できます。 このデータ・メンバーは、静的データ・メンバーが署名のステータスを通知する `SignatureStatus` オブジェクトを戻します。 例えば、署名が不明な場合は、このメソッドはを返し `SignatureStatus.DocumentSignatureUnknown`ます。

**関連トピック**

[複数の電子署名の検証](#verifying-multiple-digital-signatures)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Removing Digital Signatures {#removing-digital-signatures}

新しい電子署名を適用する前に、電子署名を署名フィールドから削除する必要があります。 電子署名は上書きできません。 署名が含まれる署名フィールドに電子署名を適用しようとすると、例外が発生します。

>[!NOTE]
>
>For more information about the Signature service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-8}

署名フィールドから電子署名を削除するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. 署名クライアントを作成します。
1. 削除する署名が含まれているPDFドキュメントを取得します。
1. 署名フィールドから電子署名を削除します。
1. PDFドキュメントをPDFファイルとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めます。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar(AEM FormsがJBossにデプロイされている場合に必要)
* jbossall-client.jar(AEM FormsがJBossにデプロイされている場合に必要)

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**署名クライアントの作成**

プログラムを使用してSignatureサービスの操作を実行する前に、Signatureサービスクライアントを作成する必要があります。

**削除する署名が含まれているPDFドキュメントの取得**

PDFドキュメントから署名を削除するには、署名が含まれるPDFドキュメントを取得する必要があります。

**署名フィールドからの電子署名の削除**

PDFドキュメントから電子署名を正しく削除するには、電子署名が含まれる署名フィールドの名前を指定する必要があります。 また、電子署名を削除する権限が必要です。 それ以外の場合は、例外が発生します。

**PDFドキュメントをPDFファイルとして保存**

Signatureサービスで署名フィールドから電子署名を削除した後、PDFドキュメントをPDFファイルとして保存し、ユーザーがAcrobatまたはAdobe Readerで開けるようにすることができます。

**関連トピック**

[Java APIを使用した電子署名の削除](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-java-api)

[WebサービスAPIを使用した電子署名の削除](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[署名フィールドの追加](digitally-signing-certifying-documents.md#adding-signature-fields)

### Java APIを使用した電子署名の削除 {#remove-digital-signatures-using-the-java-api}

署名API(Java)を使用して電子署名を削除します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-signatures-client.jarなどのクライアントJARファイルを含めます。

1. 署名クライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `SignatureServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 削除する署名が含まれているPDFドキュメントの取得

   * コンストラクターを使用し、PDFドキュメントの場所を指定するstring値を渡して、削除するドキュメントが含まれるPDF署名を表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 署名フィールドからの電子署名の削除

   オブジェクトのメソッドを呼び出し、次の値を渡して、署名フィールドから電子署名を削除し `SignatureServiceClient` ま `clearSignatureField` す。

   * 削除する署名が含まれているPDFドキュメントを表す `com.adobe.idp.Document` オブジェクトです。
   * 電子署名が含まれる署名フィールドの名前を指定するstring値です。

   電子署名が削除されたPDFドキュメントを表す `clearSignatureField``com.adobe.idp.Document` オブジェクトを返します。

1. PDFドキュメントをPDFファイルとして保存

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が .pdf であることを確認します。
   * オブジェクトの `com.adobe.idp.Document` メソッドを呼び出し `copyToFile` ます。 オブジェクトを渡して、 `java.io.File` オブジェクトの内容をフ `com.adobe.idp.Document` ァイルにコピーします。 `Document` メソッドから返された `clearSignatureField` オブジェクトを必ず使用してください。

**関連トピック**

[電子署名の削除](digitally-signing-certifying-documents.md#removing-digital-signatures)

[クイック開始（SOAPモード）: Java APIを使用した電子署名の削除](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-removing-a-digital-signature-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用した電子署名の削除 {#remove-digital-signatures-using-the-web-service-api}

Signature API（Webサービス）を使用して電子署名を削除します。

1. プロジェクトファイルを含める

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >サーバーホスト `localhost` AEM FormsのIPアドレスに置き換えます。

1. 署名クライアントの作成

   * Create a `SignatureServiceClient` object by using its default constructor.
   * Create a `SignatureServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/SignatureService?WSDL`)に渡すstring値を渡します。 属性を使用する必要はありません `lc_version` 。 この属性は、サービス参照を作成する場合に使用されます)。
   * フィールドの値を取得して `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `SignatureServiceClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクトの `System.ServiceModel.BasicHttpBinding` フィールドをに設定し `MessageEncoding` ま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * フィールドにAEM formsのユーザー名を割り当て `SignatureServiceClient.ClientCredentials.UserName.UserName`ます。
      * 対応するパスワード値をフィールドに割り当て `SignatureServiceClient.ClientCredentials.UserName.Password`ます。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当て `BasicHttpBindingSecurity.Security.Mode`ます。

1. 削除する署名が含まれているPDFドキュメントの取得

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、削除する電子署名が含まれるPDFドキュメントを保存するために使用されます。
   * コンストラクターを呼び出し、署名済みPDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
   * オブジェクトのメソッドを呼び出して、バイト配列にストリームデータ `System.IO.FileStream` を入力し `Read` ます。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * オブジェクトのプロパティにバイト配列の内容を割り当てて、 `BLOB``MTOM` オブジェクトを入力します。

1. 署名フィールドからの電子署名の削除

   オブジェクトのメソッドを呼び出し、次の値を渡して、電子署名を削除し `SignatureServiceClient``clearSignatureField` ます。

   * 署名済みPDFドキュメントを含む `BLOB` オブジェクトです。
   * 削除する電子署名が含まれている署名フィールドの名前を表すstring値です。

   電子署名が削除されたPDFドキュメントを表す `clearSignatureField``BLOB` オブジェクトを返します。

1. PDFドキュメントをPDFファイルとして保存

   * オブジェクトを作成するには、コンストラクターを呼び出し、空の署名フィールドとファイルを開くドキュメントを含むPDFのファイルの場所を表すstring値を渡します。 `System.IO.FileStream`
   * メソッドが返した `BLOB` オブジェクトの内容を格納するバイト配列を作成し `sign` ます。 オブジェクトのデータメンバーの値を取得して、 `BLOB` バイト配列を入力し `MTOM` ます。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡して、バイト配列の内容をPDFファイルに書き込み `System.IO.BinaryWriter` ま `Write` す。

**関連トピック**

[電子署名の削除](digitally-signing-certifying-documents.md#removing-digital-signatures)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
