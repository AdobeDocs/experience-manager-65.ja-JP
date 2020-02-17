---
title: ドキュメントのデジタル署名と認証
seo-title: ドキュメントのデジタル署名と認証
description: 'null'
seo-description: 'null'
uuid: 6331de8a-2a9c-45bf-89d2-29f1ad5cc856
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 42de04bf-25e4-4478-a411-38671ed871ae
translation-type: tm+mt
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d

---


# ドキュメントのデジタル署名と認証 {#digitally-signing-and-certifying-documents}

**Signatureサービスについて**

Signatureサービスを使用すると、組織で配布および受け取るAdobe PDFドキュメントのセキュリティとプライバシーを保護できます。 このサービスでは、電子署名と証明書を使用して、対象の受信者だけがドキュメントを変更できるようにします。 セキュリティ機能はドキュメント自体に適用されるので、ドキュメントはライフサイクル全体にわたって安全で制御された状態が維持されます。 ドキュメントは、ファイアウォールの外部、オフラインでダウンロードされた場合、および組織に返送される場合に、セキュリティで保護された状態のままになります。

>[!NOTE]
>
>PDFドキュメントへの署名など、特定の操作が呼び出されたときに呼び出されるSignatureサービス用のカスタム署名ハンドラーを作成できます。

**署名フィールド名**

一部のSignatureサービス操作では、操作を実行する署名フィールドの名前を指定する必要があります。 例えば、PDFドキュメントに署名する場合、署名する署名フィールドの名前を指定します。 署名フィールドのフルネームがであるとします `form1[0].Form1[0].SignatureField1[0]`。 の代わりにを指 `SignatureField1[0]` 定できます `form1[0].Form1[0].SignatureField1[0]`。

競合が原因で、Signatureサービスが間違ったフィールドに署名する（または、署名フィールド名を必要とする別の操作を実行する）ことがあります。 この競合は、同じPDFドキュメント内の複 `SignatureField1[0]` 数の場所に名前が表示された結果発生します。 例えば、とという名前の2つの署名フィールドが含まれ、ユーザーが指定したPDFドキュ `form1[0].Form1[0].SignatureField1[0]` メント `form1[0].Form1[0].SubForm1[0].SignatureField1[0]` があるとしま `SignatureField1[0]`す。 この場合、Signatureサービスは、ドキュメント内のすべての署名フィールドに対して反復処理を行う際に、検出された最初の署名フィールドに署名します。

PDFドキュメント内に複数の署名フィールドがある場合は、署名フィールドのフルネームを指定することをお勧めします。 つまり、の代わりにを `form1[0].Form1[0].SignatureField1[0]`指定しま `SignatureField1[0]`す。

Signatureサービスを使用して、次のタスクを実行できます。

* PDFドキュメントへの電子署名フィールドの追加と削除を行います。 (Adding [Signature Fieldsを参照](digitally-signing-certifying-documents.md#adding-signature-fields))。
* PDFドキュメント内の署名フィールドの名前を取得します。 (署名フィ [ールド名の取得を参照](digitally-signing-certifying-documents.md#retrieving-signature-field-names))。
* 署名フィールドを変更します。 (Modifying Signature Fields [を参照](digitally-signing-certifying-documents.md#modifying-signature-fields))。
* PDFドキュメントに電子署名を行います。 (See [Digitally Signing PDF Documents](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)
* PDFドキュメントの認証 (See [Certifying PDF Documents](digitally-signing-certifying-documents.md#certifying-pdf-documents).)
* PDFドキュメント内の電子署名を検証します。 (電子署名 [の検証を参照](digitally-signing-certifying-documents.md#verifying-digital-signatures))。
* PDFドキュメント内のすべての電子署名を検証します。 (See [Verifying Multiple Digital Signatures](digitally-signing-certifying-documents.md#verifying-digital-signatures).)
* 署名フィールドから電子署名を削除します。 (電子署名 [の削除を参照](digitally-signing-certifying-documents.md#removing-digital-signatures))。

   ***注意&#x200B;**:Signatureサービスについて詳しくは、『AEM Formsサービスリファレ[ンス』を参照してください](https://www.adobe.com/go/learn_aemforms_services_63)。*

## 署名フィールドの追加 {#adding-signature-fields}

電子署名は、署名のグラフィック表現を含むフォームフィールドである署名フィールドに表示されます。 署名フィールドは、表示または非表示に設定することができます。署名者は、既存の署名フィールドを使用することも、プログラムによって署名フィールドを追加することもできます。 どちらの場合においても、PDF ドキュメントに署名できるようにするには、署名フィールドが存在している必要があります。

プログラムによって署名フィールドを追加するには、Signature サービス Java API や 署名 Web サービス API を使用します。1つのPDFドキュメントに複数の署名フィールドを追加できます。ただし、各署名フィールド名は一意である必要があります。

>[!NOTE]
>
>一部のPDFドキュメントタイプでは、プログラムによって署名フィールドを追加できません。 Signatureサービスと署名フィールドの追加について詳しくは、『AEM Formsサービスリファレ [ンス』を参照してください](https://www.adobe.com/go/learn_aemforms_services_63)。

### 手順の概要 {#summary-of-steps}

PDFドキュメントに署名フィールドを追加するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. 署名クライアントを作成します。
1. 署名フィールドが追加されたPDFドキュメントを取得します。
1. 署名フィールドを追加します。
1. PDFドキュメントをPDFファイルとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar（AEM FormsがJBossにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsをJBossにデプロイする場合に必要）

**署名クライアントの作成**

プログラムでSignatureサービス操作を実行する前に、Signatureサービスクライアントを作成する必要があります。

**署名フィールドが追加されたPDFドキュメントの取得**

署名フィールドを追加するPDFドキュメントを取得する必要があります。

**署名フィールドの追加**

PDFドキュメントに署名フィールドを正しく追加するには、署名フィールドの場所を識別する座標値を指定します。 （非表示の署名フィールドを追加する場合、これらの値は必須ではありません）。また、署名フィールドに署名が適用された後にロックするPDFドキュメント内のフィールドを指定することもできます。

**PDFドキュメントをPDFファイルとして保存**

SignatureサービスがPDFドキュメントに署名フィールドを追加した後、ドキュメントをPDFファイルとして保存し、ユーザーがAcrobatまたはAdobe Readerで開けるようにすることができます。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDFドキュメントへのデジタル署名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### Java APIを使用した署名フィールドの追加 {#add-signature-fields-using-the-java-api}

署名API(Java)を使用して署名フィールドを追加します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-signatures-client.jarなどのクライアントJARファイルを含めます。

1. 署名クライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `SignatureServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 署名フィールドが追加されたPDFドキュメントの取得

   * 署名フィ `java.io.FileInputStream` ールドを追加するPDFドキュメントを表すオブジェクトを作成します。このオブジェクトは、コンストラクターを使用し、PDFドキュメントの場所を指定するstring値を渡すことによって作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 署名フィールドの追加

   * コンストラク `PositionRectangle` ターを使用して、署名フィールドの場所を指定するオブジェクトを作成します。 コンストラクター内で、座標値を指定します。
   * 必要に応じて、電子署名が署 `FieldMDPOptions` 名フィールドに適用されたときにロックされるフィールドを指定するオブジェクトを作成します。
   * オブジェクトのメソッドを呼び出し、次の値を渡して、PDFドキュ `SignatureServiceClient` メントに署 `addSignatureField` 名フィールドを追加します。

      * A `com.adobe.idp`. `Document` 署名フィールドが追加されるPDFドキュメントを表すオブジェクトです。
      * 署名フィールドの名前を指定するstring値です。
      * 署名 `java.lang.Integer` フィールドを追加するページ番号を表す値です。
      * 署名フ `PositionRectangle` ィールドの場所を指定するオブジェクトです。
      * 電子署 `FieldMDPOptions` 名が署名フィールドに適用された後にロックされる、PDFドキュメント内のフィールドを指定するオブジェクトです。 このパラメーター値はオプションで、渡すことができま `null`す。
   * 様々な `PDFSeedValueOptions` 実行時値を指定するオブジェクトです。 このパラメーター値はオプションで、渡すことができま `null`す。

      メソッド `addSignatureField` は、aを返しま `com.adobe.idp`す。 `Document` 署名フィールドが含まれるPDFドキュメントを表すオブジェクトです。
   >[!NOTE]
   >
   >オブジェクトのメソッドを呼 `SignatureServiceClient` び出して、非 `addInvisibleSignatureField` 表示署名フィールドを追加できます。

1. PDFドキュメントをPDFファイルとして保存

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が .pdf であることを確認します。
   * を起動しま `com.adobe.idp`す。 `Document` オブジェクトの `copyToFile` コンテンツをファイルにコピ `Document` ーするメソッド。 を必ず使用してくださ `com.adobe.idp`い。 `Document` メソッドによって返されたオブジェ `addSignatureField` クト。

**関連トピック**

[SignatureサービスAPIのクイックスタート](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

### WebサービスAPIを使用した署名フィールドの追加 {#add-signature-fields-using-the-web-service-api}

Signature API（Webサービス）を使用して署名フィールドを追加するには：

1. プロジェクトファイルを含める

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. 署名クライアントの作成

   * Create a `SignatureServiceClient` object by using its default constructor.
   * Create a `SignatureServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/SignatureService?WSDL`)に渡すstring値。 属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。)
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `SignatureServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `SignatureServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `SignatureServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. 署名フィールドが追加されたPDFドキュメントの取得

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、署名フィールドを含むPDFドキュメントを保存するために使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、PDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイト配列、開 `System.IO.FileStream` 始位置、ストリ `Read` ーム長を渡すことによって、バイト配列にストリームデータを設定します。
   * オブジェクト `BLOB` にバイト配列の内容をプロ `MTOM` パティに割り当てて、オブジェクトを設定します。

1. 署名フィールドの追加

   オブジェクトのメソッドを呼び出し、次の値を渡して、PDFドキュ `SignatureServiceClient` メントに署名フ `addSignatureField` ィールドを追加します。

   * A `BLOB` object that represents the PDF document to which a signature field is added.
   * 署名フィールド名を指定するstring値です。
   * 署名フィールドを追加するページ番号を表すinteger値です。
   * 署名フ `PositionRect` ィールドの場所を指定するオブジェクトです。
   * 電子署 `FieldMDPOptions` 名が署名フィールドに適用された後にロックされる、PDFドキュメント内のフィールドを指定するオブジェクトです。 このパラメーター値はオプションで、渡すことができま `null`す。
   * 様々な `PDFSeedValueOptions` 実行時値を指定するオブジェクトです。 このパラメーター値はオプションで、渡すことができま `null`す。
   このメソ `addSignatureField` ッドは、署名フィ `BLOB` ールドを含むPDFドキュメントを表すオブジェクトを返します。

1. PDFドキュメントをPDFファイルとして保存

   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、署名フィールドとファイルを開くモードを含むPDFドキュメントのファイルの場所を表すstring値を渡します。
   * メソッドによって返されたオブジェクトの内容を格納 `BLOB` するバイト配列を作成し `addSignatureField` ます。 オブジェクトのデータメンバーの値を取得して、バ `BLOB` イト配列を `binaryData` 設定します。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡すことで、バ `System.IO.BinaryWriter` イト配列の内 `Write` 容をPDFファイルに書き込みます。

**関連トピック**

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

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

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar（AEM FormsがJBossにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsをJBossにデプロイする場合に必要）

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**署名クライアントの作成**

プログラムでSignatureサービス操作を実行する前に、Signatureサービスクライアントを作成する必要があります。

**署名フィールドを含むPDFドキュメントの取得**

署名フィールドを含むPDFドキュメントを取得します。

**署名フィールド名の取得**

1つ以上の署名フィールドを含むPDFドキュメントを取得した後で、署名フィールド名を取得できます。

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

   * コンストラク `java.io.FileInputStream` ターを使用し、PDFドキュメントの場所を指定するstring値を渡すことで、署名フィールドを含むPDFドキュメントを表すオブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 署名フィールド名の取得

   * オブジェクトのメソッドを呼び出し、署名フィー `SignatureServiceClient` ルドを含むPDFドキ `getSignatureFieldList` ュメントを含むオ `com.adobe.idp.Document` ブジェクトを渡して、署名フィールド名を取得します。 このメソッドは、各要素に `java.util.List` 1つのオブジェクトが含まれるオブジェクトを返 `PDFSignatureField` します。 このオブジェクトを使用すると、署名フィールドが表示されているかどうかなど、署名フィールドに関する追加情報を取得できます。
   * オブジェクトを繰り返 `java.util.List` し処理し、署名フィールド名があるかどうかを確認します。 PDFドキュメントの各署名フィールドに対して、別々のオブジェクトを取得で `PDFSignatureField` きます。 署名フィールドの名前を取得するには、オブジェクトの `PDFSignatureField` メソッドを呼び出 `getName` します。 このメソッドは、署名フィールド名を指定するstring値を返します。

**関連トピック**

[署名フィールド名の取得](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[クイックスタート（SOAPモード）:Java APIを使用した署名フィールド名の取得](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-retrieving-signature-field-names-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用した署名フィールドの取得 {#retrieve-signature-field-using-the-web-service-api}

Signature API（Webサービス）を使用して署名フィールド名を取得します。

1. プロジェクトファイルを含める

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. 署名クライアントの作成

   * Create a `SignatureServiceClient` object by using its default constructor.
   * Create a `SignatureServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/SignatureService?WSDL`)に渡すstring値。 属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。)
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `SignatureServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `SignatureServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `SignatureServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. 署名フィールドを含むPDFドキュメントの取得

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオブ `BLOB` ジェクトは、署名フィールドを含むPDFドキュメントの保存に使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、PDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイト配列、開 `System.IO.FileStream` 始位置、ストリ `Read` ーム長を渡すことによって、バイト配列にストリームデータを設定します。
   * オブジェクトにバ `BLOB` イト配列の内容をフィールドに `MTOM` 割り当てて、オブジェクトを設定します。

1. 署名フィールド名の取得

   * オブジェクトのメソッドを呼び出し、署名フィー `SignatureServiceClient` ルドを含むPDFドキ `getSignatureFieldList` ュメントを含むオ `BLOB` ブジェクトを渡して、署名フィールド名を取得します。 このメソッドは、各要素にオ `MyArrayOfPDFSignatureField` ブジェクトが含まれるコレクションオブジェクトを返 `PDFSignatureField` します。
   * オブジェクトを繰り返し `MyArrayOfPDFSignatureField` 処理して、署名フィールド名があるかどうかを判断します。 PDFドキュメントの各署名フィールドに対して、オブジェクトを取得でき `PDFSignatureField` ます。 署名フィールドの名前を取得するには、オブジェクトの `PDFSignatureField` メソッドを呼び出 `getName` します。 このメソッドは、署名フィールド名を指定するstring値を返します。

**関連トピック**

[署名フィールド名の取得](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Modifying Signature Fields {#modifying-signature-fields}

Java APIおよびWebサービスAPIを使用して、PDFドキュメント内の署名フィールドを変更できます。 署名フィールドの署名フィールドロックディクショナリまたはシード値ディクショナリの値を操作することで署名フィールドを変更します。

A *field lock dictionary* specifies a list of fields that are locked when the signature field is signed. フィールドがロックされると、ユーザーはフィールドを変更できません。A *seed value dictionary* contains constraining information that is used at the time the signature is applied. 例えば、署名を無効にすることなく実行できるアクションを制御する権限設定を変更することができます。

既存の署名フィールドを変更すると、ビジネス要件の変化を反映してPDFドキュメントに変更を加えることができます。 例えば、新しいビジネス要件では、ドキュメントの署名後にすべてのドキュメントフィールドをロックする必要がある場合があります。

この節では、フィールドロックディクショナリとシード値ディクショナリの値の両方を変更して、署名フィールドを変更する方法について説明します。 署名フィールドロックディクショナリに変更を加えると、署名フィールドへの署名時にPDFドキュメント内のすべてのフィールドがロックされます。 シード値ディクショナリを変更すると、ドキュメントに対する特定の種類の変更が禁止されます。

>[!NOTE]
>
>Signatureサービスと署名フィールドの変更について詳しくは、『AEM Formsサービスリファレ [ンス』を参照してください](https://www.adobe.com/go/learn_aemforms_services_63)。

### 手順の概要 {#summary_of_steps-2}

PDFドキュメント内の署名フィールドを変更するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. 署名クライアントを作成します。
1. 変更する署名フィールドが含まれるPDFドキュメントを取得します。
1. 辞書の値を設定します。
1. 署名フィールドを変更します。
1. PDFドキュメントをPDFファイルとして保存します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar（AEM FormsがJBossにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsをJBossにデプロイする場合に必要）

For information about the location of these JAR files, see [Including LiveCycle Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**署名クライアントの作成**

プログラムでSignatureサービス操作を実行する前に、Signatureサービスクライアントを作成する必要があります。

**変更する署名フィールドを含むPDFドキュメントを取得します**

変更する署名フィールドが含まれるPDFドキュメントを取得します。

**辞書の値の設定**

署名フィールドを変更するには、フィールドロックディクショナリまたはシード値ディクショナリに値を割り当てます。 署名フィールドロックディクショナリ値の指定には、署名フィールドへの署名時にロックされるPDFドキュメントフィールドの指定が含まれます。 （この節では、すべてのフィールドをロックする方法について説明します）。

次のシード値ディクショナリ値を設定できます。

* **リビジョンの確認**:署名フィールドに署名が適用された場合に失効確認を実行するかどうかを指定します。
* **証明書のオプション**:証明書のシード値ディクショナリに値を割り当てます。 証明書のオプションを指定する前に、証明書のシード値ディクショナリについて理解することをお勧めします。 (『 [PDF Reference](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf)』を参照)。
* **Digest options**:署名に使用するダイジェストアルゴリズムを割り当てます。 有効な値は、SHA1、SHA256、SHA384、SHA512およびRIPEMD160です。
* **フィルタ**:署名フィールドで使用するフィルターを指定します。 例えば、Adobe.PPKLiteフィルターを使用できます。 (『 [PDF Reference](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf)』を参照)。
* **フラグオプション**:この署名フィールドに関連付けられているフラグ値を指定します。 値が1の場合、署名者は指定した値のみをエントリに使用する必要があります。 値が0の場合、他の値も許可されます。 ビット位置を次に示します。

   * **** 1（フィルタ）:署名フィールドへの署名に使用する署名ハンドラーです
   * **** 2(SubFilter):署名時に使用する有効なエンコーディングを示す名前の配列
   * **3(V)**:署名フィールドへの署名に使用する署名ハンドラーの最小限必要なバージョン番号です
   * **** 4（理由）:ドキュメントに署名する理由を指定する文字列の配列
   * **** 5(PDFLegalWarnings):法的証明を指定する文字列の配列

* **Legal attestations**:ドキュメントを認証すると、ドキュメントの表示されるコンテンツをあいまいにしたり誤解を招く可能性のある特定の種類のコンテンツが、ドキュメントに自動的にスキャンされます。 例えば、注釈によって、認証対象を把握するために重要なテキストを隠すことができます。 スキャン処理では、この種類のコンテンツの存在を示す警告が生成されます。 また、警告が生成された可能性のあるコンテンツに関する追加の説明も提供されます。
* **権限**:署名を無効にせずにPDFドキュメントで使用できる権限を指定します。
* **理由**:このドキュメントに署名が必要な理由を指定します。
* **タイムスタンプ**:タイムスタンプオプションを指定します。 例えば、使用するタイムスタンプサーバーのURLを設定できます。
* **バージョン**:署名フィールドへの署名に使用する署名ハンドラーの最小バージョン番号を指定します。

**署名フィールドの変更**

Signatureサービスクライアントを作成し、変更する署名フィールドを含むPDFドキュメントを取得し、ディクショナリ値を設定した後、Signatureサービスに署名フィールドを変更するように指示できます。 次に、Signatureサービスは、変更された署名フィールドを含むPDFドキュメントを返します。 元のPDFドキュメントは影響を受けません。

**PDFドキュメントをPDFファイルとして保存**

変更した署名フィールドを含むPDFドキュメントをPDFファイルとして保存し、ユーザーがAcrobatまたはAdobe readerで開けるようにします。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[SignatureサービスAPIのクイックスタート](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

[PDFドキュメントへのデジタル署名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### Java APIを使用した署名フィールドの変更 {#modify-signature-fields-using-the-java-api}

署名API(Java)を使用して署名フィールドを変更します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-signatures-client.jarなどのクライアントJARファイルを含めます。

1. 署名クライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `SignatureServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 変更する署名フィールドを含むPDFドキュメントを取得します

   * コンストラク `java.io.FileInputStream` ターを使用し、PDFドキュメントの場所を指定するstring値を渡すことで、変更する署名フィールドを含むPDFドキュメントを表すオブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 辞書の値の設定

   * コンストラクタを使用して `PDFSignatureFieldProperties` オブジェクトを作成します。オブジェクト `PDFSignatureFieldProperties` は、署名フィールドロックディクショナリとシード値ディクショナリ情報を格納します。
   * コンストラクタを使用して `PDFSeedValueOptionSpec` オブジェクトを作成します。このオブジェクトを使用すると、シード値ディクショナリの値を設定できます。
   * オブジェクトのメソッドを呼び出し、列挙値を渡すこ `PDFSeedValueOptionSpec` とで、PDFドキュ `setMdpValue` メントに対する変更を `MDPPermissions.NoChanges` 許可しません。
   * コンストラクタを使用して `FieldMDPOptionSpec` オブジェクトを作成します。このオブジェクトを使用すると、署名フィールドロックディクショナリの値を設定できます。
   * オブジェクトのメソッドを呼び出し、列挙値を渡すこ `FieldMDPOptionSpec` とで、PDFドキュメ `setMdpValue` ント内のすべてのフィールドを `FieldMDPAction.ALL` ロックします。
   * オブジェクトのメソッドを呼び出し、オブジェクトを `PDFSignatureFieldProperties` 渡すことで、シ `setSeedValue` ード値ディクショナリ情報を設 `PDFSeedValueOptionSpec` 定します。
   * 署名フィールドのロックディクショナリ情報を設定するには、オ `PDFSignatureFieldProperties`ブジェクトのメソッド `setFieldMDP` を呼び出し、オブジェクトを渡 `FieldMDPOptionSpec` します。
   >[!NOTE]
   >
   >設定可能なすべてのシード値ディクショナリ値を確認するには、クラス参照を参 `PDFSeedValueOptionSpec` 照してください。 (『 [AEM Forms APIリファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)』を参照)。

1. 署名フィールドの変更

   署名フィールドを変更するには、オブジェクトの `SignatureServiceClient` メソッドを呼び出 `modifySignatureField` し、次の値を渡します。

   * 変更す `com.adobe.idp.Document` る署名フィールドが含まれるPDFドキュメントを格納するオブジェクトです
   * 署名フィールドの名前を指定するstring値です
   * 署名フィ `PDFSignatureFieldProperties` ールドロックディクショナリとシード値ディクショナリ情報を格納するオブジェクトです
   このメソ `modifySignatureField` ッドは、変更された署 `com.adobe.idp.Document` 名フィールドを含むPDFドキュメントを格納するオブジェクトを返します。

1. PDFドキュメントをPDFファイルとして保存

   * Create a `java.io.File` object and ensure that the file name extension is .pdf.
   * Invoke the `com.adobe.idp.Document` object’s `copyToFile` method to copy the contents of the `com.adobe.idp.Document` object to the file. メソッドが返したオブジェクト `com.adobe.idp.Document` を使用しているこ `modifySignatureField` とを確認します。

### WebサービスAPIを使用した署名フィールドの変更 {#modify-signature-fields-using-the-web-service-api}

Signature API（Webサービス）を使用して署名フィールドを変更します。

1. プロジェクトファイルを含める

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. 署名クライアントの作成

   * Create a `SignatureServiceClient` object by using its default constructor.
   * Create a `SignatureServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/SignatureService?WSDL`)に渡すstring値。 属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。)
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `SignatureServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `SignatureServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `SignatureServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. 変更する署名フィールドを含むPDFドキュメントを取得します

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、変更する署名フィールドを含むPDFドキュメントの保存に使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、PDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイト配列、開 `System.IO.FileStream` 始位置、ストリ `Read` ーム長を渡すことによって、バイト配列にストリームデータを設定します。
   * オブジェクトにバ `BLOB` イト配列の内容をプロ `MTOM` パティに割り当てて、オブジェクトを設定します。

1. 辞書の値の設定

   * コンストラクタを使用して `PDFSignatureFieldProperties` オブジェクトを作成します。このオブジェクトは、署名フィールドロックディクショナリとシード値ディクショナリの情報を格納します。
   * コンストラクタを使用して `PDFSeedValueOptionSpec` オブジェクトを作成します。このオブジェクトを使用すると、シード値ディクショナリの値を設定できます。
   * PDFドキュメントの変更を許可しない場合は、オブジェクトの `MDPPermissions.NoChanges` データメンバーに列 `PDFSeedValueOptionSpec` 挙値を割り `mdpValue` 当てます。
   * コンストラクタを使用して `FieldMDPOptionSpec` オブジェクトを作成します。このオブジェクトを使用すると、署名フィールドロックディクショナリの値を設定できます。
   * PDFドキュメント内のすべてのフィールドをロックするには、オブジ `FieldMDPAction.ALL` ェクトのデータメンバーに列 `FieldMDPOptionSpec` 挙値を割り `mdpValue` 当てます。
   * オブジェクトのデータメンバーにオブジェクトを割り当て `PDFSeedValueOptionSpec` て、シード値ディク `PDFSignatureFieldProperties` ショナリ情報を `seedValue` 設定します。
   * 署名フィールドのロックディクショナリ情報を設定するには、オ `FieldMDPOptionSpec` ブジェクトをオブジ `PDFSignatureFieldProperties` ェクトのデータメン `fieldMDP` バーに割り当てます。
   >[!NOTE]
   >
   >設定可能なすべてのシード値ディクショナリ値を確認するには、クラス参照を参 `PDFSeedValueOptionSpec` 照してください。 (『 [AEM Forms APIリファレンス』を参照](https://www.adobe.com/go/learn_aemforms_javadocs_63_en))。

1. 署名フィールドの変更

   署名フィールドを変更するには、オブジェクトの `SignatureServiceClient` メソッドを呼び出 `modifySignatureField` し、次の値を渡します。

   * 変更す `BLOB` る署名フィールドが含まれるPDFドキュメントを格納するオブジェクトです
   * 署名フィールドの名前を指定するstring値です
   * 署名フィ `PDFSignatureFieldProperties` ールドロックディクショナリとシード値ディクショナリ情報を格納するオブジェクトです
   このメソ `modifySignatureField` ッドは、変更された署 `BLOB` 名フィールドを含むPDFドキュメントを格納するオブジェクトを返します。

1. PDFドキュメントをPDFファイルとして保存

   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、署名フィールドを含むPDFドキュメントのファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * メソッドが返すオブジェクトの内容を格納するバ `BLOB` イト配列を作 `addSignatureField` 成します。 オブジェクトのデータメンバーの値を取得して、バ `BLOB` イト配列を `MTOM` 設定します。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡すことで、バ `System.IO.BinaryWriter` イト配列の内 `Write` 容をPDFファイルに書き込みます。

**関連トピック**

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Digitally Signing PDF Documents {#digitally-signing-pdf-documents}

セキュリティレベルの提供のため、PDF に電子署名を適用することができます。手書き署名のような電子署名は、署名者を識別したり、ドキュメントに関するステートメントを作成する手段として使用できます。ドキュメントの電子署名に使用されている技術は、署名者と受信者の両方が、何に署名されているのかを明確にし、その署名によりドキュメントに変更がないことを確認するのに役立ちます。

PDF ドキュメントは、公開鍵を用いて署名されます。署名者は公開鍵と秘密鍵の 2 つの鍵を持っています。秘密鍵は、署名時に使用できる必要があるユーザーの秘密鍵証明書に保存されます。 公開鍵はユーザーの証明書に保存され、受信者が署名を検証するにはこの証明書を使用できる必要があります。 失効した証明書に関する情報は、認証機関から配布される証明書失効リスト（CRL）およびオンライン証明書ステータスプロトコル（OCSP）応答内にあります。署名が行われた時間は、タイムスタンプ局として知られる信頼できるソースから取得されます。

>[!NOTE]
>
>PDFドキュメントに電子署名を行う前に、証明書がAEM Formsに追加されていることを確認する必要があります。 証明書は、管理コンソールを使用して、またはTrust Manager APIを使用してプログラムで追加されます。 (Trust Manager APIを [使用した秘密鍵証明書の読み込みを参照](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api))。

PDFドキュメントにプログラム的に電子署名を行うことができます。 PDFドキュメントに電子署名する場合は、AEM Formsに存在するセキュリティ証明書を参照する必要があります。 証明書は署名に使用する秘密鍵となります。

Signatureサービスは、PDFドキュメントが署名されるときに次の手順を実行します。

1. Signatureサービスは、要求で指定されたエイリアスを渡すことで、Truststoreから秘密鍵証明書を取得します。
1. Truststoreは、指定された秘密鍵証明書を検索します。
1. 秘密鍵証明書はSignatureサービスに返され、ドキュメントへの署名に使用されます。 また、証明書は、今後の要求のためにエイリアスに対してキャッシュされます。

セキュリティ証明書の処理に関する詳細は、使用しているアプリケーシ *ョンサーバー版の『AEM Formsのインストール* およびデプロイ』ガイドを参照してください。

>[!NOTE]
>
>ドキュメントの署名と認証には違いがあります。 (See [Certifying PDF Documents](digitally-signing-certifying-documents.md#certifying-pdf-documents).)

>[!NOTE]
>
>署名がサポートされていないPDFドキュメントもあります。 Signatureサービスとドキュメントへの電子署名について詳しくは、『AEM Formsサービスリファレ [ンス』を参照してください](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>Signatureサービスは、ドキュメントの認証など、操作への入力としてPDFデータが埋め込まれたXDPファイルをサポートしません。 この操作を行うと、Signatureサービスで `PDFOperationException`、 この問題を解決するには、PDF Utilitiesサービスを使用してXDPファイルをPDFファイルに変換し、変換したPDFファイルをSignatureサービス操作に渡します。 (PDF Utilities [の操作を参照](/help/forms/developing/pdf-utilities.md#working-with-pdf-utilities))。

**nCipher nShield HSM秘密鍵証明書**

PDFドキュメントの署名や認証にnCipher nShield HSM秘密鍵証明書を使用する場合、AEM Formsのデプロイ先のJ2EEアプリケーションサーバーが再起動されるまで、新しい秘密鍵証明書は使用できません。 ただし、設定値を設定すると、J2EEアプリケーションサーバーを再起動しなくても、署名または認証の操作が機能します。

次の設定値をcknfastrcファイルに追加できます。このファイルは/opt/nfast/cknfastrc(またはc:\nfast\cknfastrc)にあります。

```as3
 CKNFAST_ASSUME_SINGLE_PROCESS=0
```

この設定値をcknfastrcファイルに追加した後、新しい秘密鍵証明書は、J2EEアプリケーションサーバーを再起動しなくても使用できます。

**署名が信頼されていません**

同じPDFドキュメントを認証および署名する場合、認証署名が信頼されていないと、AcrobatまたはAdobe ReaderでPDFドキュメントを開くときに、最初の署名に対して黄色い三角形が表示されます。 この状況を回避するには、認証署名を信頼する必要があります。

**XFAベースのフォームであるドキュメントへの署名**

SignatureサービスAPIを使用してXFAベースのフォームに署名しようとすると、Acrobatにあるデータが見つからない可能 `View``Signed``Version` 性があります。 例えば、次のワークフローを考えてみましょう。

* Designerで作成したXDPファイルを使用して、署名フィールドを含むフォームデザインと、フォームデータを含むXMLデータを結合します。 インタラクティブPDFドキュメントを生成するには、Formsサービスを使用します。
* PDFドキュメントにはSignatureサービスAPIを使用して署名します。

### 手順の概要 {#summary_of_steps-3}

PDFドキュメントに電子署名するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Signatureサービスクライアントを作成します。
1. 署名するPDFドキュメントを取得します。
1. PDFドキュメントに署名します。
1. 署名済みPDFドキュメントをPDFファイルとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar（AEM FormsがJBossにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsをJBossにデプロイする場合に必要）

**Signaturesクライアントの作成**

プログラムでSignatureサービス操作を実行する前に、Signatureサービスクライアントを作成する必要があります。

**署名するPDFドキュメントの取得**

PDFドキュメントに署名するには、署名フィールドを含むPDFドキュメントを取得する必要があります。 PDFドキュメントに署名フィールドが含まれていない場合は、署名を行うことはできません。 署名フィールドは、Designerを使用して追加することも、プログラムを使用して追加することもできます。

**PDFドキュメントへの署名**

PDFドキュメントに署名する場合、Signatureサービスで使用する実行時オプションを設定できます。 次のオプションを設定できます。

* 外観オプション
* 失効確認
* タイムスタンプ値

外観オプションは、オブジェクトを使用して設定 `PDFSignatureAppearanceOptionSpec` します。 例えば、オブジェクトのメソッドを呼び出して渡すことで、署名内に日 `PDFSignatureAppearanceOptionSpec` 付を表示するこ `setShowDate` とができま `true`す。

また、PDFドキュメントのデジタル署名に使用される証明書が失効したかどうかを判定する失効確認を実行するかどうかを指定することもできます。 失効確認を実行するには、次の値のいずれかを指定できます。

* **NoCheck**:失効確認を実行しません。
* **BestEffort**:常に、チェーン内のすべての証明書の失効の確認を試みます。 確認で問題が発生した場合、失効は有効であると見なされます。 エラーが発生した場合は、証明書が失効していないと仮定します。
* **** CheckIfAvailable:失効情報が利用可能な場合、チェーン内のすべての証明書の失効を確認します。 確認で問題が発生した場合、失効は無効であると見なされます。 エラーが発生した場合は、証明書が失効済みで無効であると仮定します。 （これがデフォルト値です。）
* **AlwaysCheck**:チェーン内のすべての証明書の失効を確認します。 失効情報が証明書に存在しない場合、失効は無効であると見なされます。

証明書に対して失効確認を実行するには、オブジェクトを使用して、証明書失効リスト(CRL)サーバーのURLを指定で `CRLOptionSpec` きます。 ただし、失効確認を実行し、CRLサーバーへのURLを指定しない場合は、Signatureサービスは証明書からURLを取得します。

失効確認を実行する際は、CRLサーバーを使用する代わりに、オンライン証明書ステータスプロトコル(OCSP)サーバーを使用できます。 通常、CRLサーバーとは異なり、OCSPサーバーを使用する場合、失効確認の実行時間が短縮されます。 (https://tools.ietf.org/html/rfc2560の「オンライン証明書ステータスプロトコル」を参 [照してください](https://tools.ietf.org/html/rfc2560)。)

SignatureサービスでAdobe Applications and Servicesを使用して使用するCRLおよびOCSPサーバーの順序を設定できます。 例えば、OCSPサーバーがAdobe Applications and Servicesで最初に設定されている場合は、OCSPサーバーが確認され、次にCRLサーバーが確認されます。 （AACヘルプの「Trust storeを使用した証明書と秘密鍵証明書の管理」を参照）。

失効確認を実行しないように指定した場合、Signatureサービスは、ドキュメントの署名または認証に使用された証明書が失効したかどうかを確認しません。 つまり、CRLおよびOCSPサーバー情報は無視されます。

>[!NOTE]
>
>CRLまたはOCSPサーバーは証明書で指定できますが、とオブジェクトを使用して、証明書で指定されたURLを上書きする `CRLOptionSpec` ことができ `OCSPOptionSpec` ます。 例えば、CRLサーバーを上書きするには、オブジェクトのメソッド `CRLOptionSpec` を呼び出すことがで `setLocalURI` きます。

タイムスタンプとは、署名済みまたは認証済みのドキュメントが変更された時間を追跡するプロセスです。 ドキュメントの署名後は、ドキュメントの所有者によってもドキュメントを変更しないでください。 タイムスタンプ機能を使用すると、署名済みまたは認証済みのドキュメントの有効性を強化できます。 オブジェクトを使用して、タイムスタンプオプションを設定 `TSPOptionSpec` できます。 例えば、タイムスタンププロバイダー(TSP)サーバーのURLを指定できます。

>[!NOTE]
>
>JavaおよびWebサービスの各セクションと対応するクイックスタートでは、失効確認が使用されます。 CRLまたはOCSPサーバー情報が指定されていないので、PDFドキュメントのデジタル署名に使用された証明書からサーバー情報が取得されます。

PDFドキュメントに正常に署名するには、電子署名を含む署名フィールドの完全修飾名を指定します（例：） `form1[0].#subform[1].SignatureField3[3]`。 XFAフォームフィールドを使用する場合、署名フィールドの名前の一部を使用することもできます。 `SignatureField3[3]`.

また、PDFドキュメントに電子署名するには、セキュリティ証明書を参照する必要があります。 セキュリティ証明書を参照するには、エイリアスを指定します。 エイリアスは、PKCS#12ファイル（.pfx拡張子付き）またはハードウェアセキュリティモジュール(HSM)内に存在する可能性がある、実際の秘密鍵証明書への参照です。 セキュリティ証明書について詳しくは、使用しているアプリケーシ *ョンサーバー版の『AEM Formsのインストール* およびデプロイ』ガイドを参照してください。

**署名済みPDFドキュメントの保存**

SignatureサービスでPDFドキュメントに電子署名した後、PDFファイルとして保存し、ユーザーがAcrobatまたはAdobe Readerで開けるようにすることができます。

**関連トピック**

[Java APIを使用したPDFドキュメントへの電子署名](digitally-signing-certifying-documents.md#digitally-sign-pdf-documents-using-the-java-api)

[WebサービスAPIを使用したPDFドキュメントへのデジタル署名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[署名フィールドの追加](digitally-signing-certifying-documents.md#adding-signature-fields)

[署名フィールド名の取得](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

### Java APIを使用したPDFドキュメントへの電子署名 {#digitally-sign-pdf-documents-using-the-java-api}

署名API(Java)を使用してPDFドキュメントに電子署名を行います。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-signatures-client.jarなどのクライアントJARファイルを含めます。

1. Signaturesクライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `SignatureServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 署名するPDFドキュメントの取得

   * コンストラク `java.io.FileInputStream` ターを使用し、PDFドキュメントの場所を指定する文字列値を渡して、デジタル署名するPDFドキュメントを表すオブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PDFドキュメントへの署名

   オブジェクトのメソッドを呼び出し、次 `SignatureServiceClient` の値を渡して、PDF `sign` ドキュメントに署名します。

   * A `com.adobe.idp.Document` object that represents the PDF document to sign.
   * 電子署名を含む署名フィールドの名前を表すstring値です。
   * A `Credential` object that represents the credential that is used to digitally sign the PDF document. オブジェクト `Credential` を作成するには、オ `Credential` ブジェクトの静的メソッドを呼び出 `getInstance` し、セキュリティ秘密鍵証明書に対応するエイリアス値を指定するstring値を渡します。
   * PDFドキ `HashAlgorithm` ュメントのダイジェストの作成に使用するハッシュアルゴリズムを表す静的データメンバーを指定するオブジェクトです。 例えば、SHA1アルゴリズムを `HashAlgorithm.SHA1` 使用するように指定できます。
   * PDFドキュメントが電子署名された理由を表すstring値です。
   * 署名者の連絡先情報を表すstring値です。
   * 電子署 `PDFSignatureAppearanceOptions` 名の外観を制御するオブジェクトです。 例えば、このオブジェクトを使用して、電子署名にカスタムロゴを追加できます。
   * 署名者 `java.lang.Boolean` の証明書に対して失効確認を実行するかどうかを指定するオブジェクトです。
   * オンラ `OCSPOptionSpec` イン証明書ステータスプロトコル(OCSP)サポートの環境設定を格納するオブジェクトです。 失効確認が行われない場合、このパラメーターは使用されず、指定できま `null`す。
   * 証明書 `CRLPreferences` 失効リスト(CRL)の環境設定を格納するオブジェクトです。 失効確認が行われない場合、このパラメーターは使用されず、指定できま `null`す。
   * タイム `TSPPreferences` スタンププロバイダー(TSP)サポートの環境設定を格納するオブジェクトです。 このパラメーターはオプションで、を指定できま `null`す。 For more information, see [AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   このメソ `sign` ッドは、署名済みPDFド `com.adobe.idp.Document` キュメントを表すオブジェクトを返します。

1. 署名済みPDFドキュメントの保存

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が .pdf であることを確認します。
   * Invoke the `com.adobe.idp.Document` object’s `copyToFile` method and pass `java.io.File`to copy the contents of the `Document` object to the file. `com.adobe.idp.Document` メソッドから返された `sign` オブジェクトを必ず使用してください。

**関連トピック**

[PDFドキュメントへのデジタル署名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[クイックスタート（SOAPモード）:Java APIを使用したPDFドキュメントへの電子署名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したPDFドキュメントへのデジタル署名 {#digitally-signing-pdf-documents-using-the-web-service-api}

Signature API（Webサービス）を使用してPDFドキュメントに電子署名するには：

1. プロジェクトファイルを含める

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. Signaturesクライアントの作成

   * Create a `SignatureServiceClient` object by using its default constructor.
   * Create a `SignatureServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/SignatureService?WSDL`)に渡すstring値。 属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。)
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `SignatureServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `SignatureServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `SignatureServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. 署名するPDFドキュメントの取得

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、署名済みのPDFドキュメントを保存するために使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、署名するPDFドキュメントのファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイト配列、開 `System.IO.FileStream` 始位置、ストリ `Read` ーム長を渡すことによって、バイト配列にストリームデータを設定します。
   * オブジェクトにバ `BLOB` イト配列の内容をプロ `MTOM` パティに割り当てて、オブジェクトを設定します。

1. PDFドキュメントへの署名

   オブジェクトのメソッドを呼び出し、次 `SignatureServiceClient` の値を渡して、PDF `sign` ドキュメントに署名します。

   * A `BLOB` object that represents the PDF document to sign.
   * 電子署名を含む署名フィールドの名前を表すstring値です。
   * A `Credential` object that represents the credential that is used to digitally sign the PDF document. オブジェクト `Credential` を作成するには、そのコンストラクターを使用し、オブジェクトのプロパティに値を割り当て `Credential` てエイリアスを指定 `alias` します。
   * PDFドキ `HashAlgorithm` ュメントのダイジェストの作成に使用するハッシュアルゴリズムを表す静的データメンバーを指定するオブジェクトです。 例えば、SHA1アルゴリズムを `HashAlgorithm.SHA1` 使用するように指定できます。
   * ハッシュアルゴリズムを使用するかどうかを指定するBoolean値です。
   * PDFドキュメントが電子署名された理由を表すstring値です。
   * 署名者の場所を表すstring値です。
   * 署名者の連絡先情報を表すstring値です。
   * 電子署 `PDFSignatureAppearanceOptions` 名の外観を制御するオブジェクトです。 例えば、このオブジェクトを使用して、電子署名にカスタムロゴを追加できます。
   * 署名者 `System.Boolean` の証明書に対して失効確認を実行するかどうかを指定するオブジェクトです。 この失効確認が行われると、署名に埋め込まれます。 デフォルトは、`false` です。
   * オンラ `OCSPOptionSpec` イン証明書ステータスプロトコル(OCSP)サポートの環境設定を格納するオブジェクトです。 失効確認が行われない場合、このパラメーターは使用されず、指定できま `null`す。 このオブジェクトに関する詳細は、『 [AEM Forms APIリファレンス』を参照してください](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   * 証明書 `CRLPreferences` 失効リスト(CRL)の環境設定を格納するオブジェクトです。 失効確認が行われない場合、このパラメーターは使用されず、指定できま `null`す。
   * タイム `TSPPreferences` スタンププロバイダー(TSP)サポートの環境設定を格納するオブジェクトです。 このパラメーターはオプションで、を指定できま `null`す。
   このメソ `sign` ッドは、署名済みPDFド `BLOB` キュメントを表すオブジェクトを返します。

1. 署名済みPDFドキュメントの保存

   * Create a `System.IO.FileStream` object by invoking its constructor. 署名済みPDFドキュメントのファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * メソッドによって返されたオブジェクトの内容を格納 `BLOB` するバイト配列を作成し `sign` ます。 オブジェクトのデータメンバーの値を取得して、バ `BLOB` イト配列を `MTOM` 設定します。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡すことで、バ `System.IO.BinaryWriter` イト配列の内 `Write` 容をPDFファイルに書き込みます。

**関連トピック**

[PDFドキュメントへのデジタル署名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## インタラクティブフォームへの電子署名 {#digitally-signing-interactive-forms}

Formsサービスで作成されるインタラクティブフォームに署名できます。 例えば、次のワークフローを考えてみましょう。

* Designerを使用して作成されたXFAベースのPDFフォームと、Formsサービスを使用してXMLドキュメント内のフォームデータを結合します。 Formsサーバーはインタラクティブフォームをレンダリングします。
* インタラクティブフォームにはSignatureサービスAPIを使用して署名します。

デジタル署名されたインタラクティブPDFフォームが生成されます。 XFAフォームに基づくPDFフォームに署名する場合は、PDFファイルをAdobeスタティックPDFフォームとして保存する必要があります。 AdobeダイナミックPDFフォームとして保存されたPDFフォームに署名しようとすると、例外が発生します。 Formsサービスから返されるフォームに署名するので、フォームに署名フィールドが含まれていることを確認します。

>[!NOTE]
>
>インタラクティブフォームに電子署名する前に、証明書がAEM Formsに追加されていることを確認する必要があります。 証明書は、管理コンソールを使用して、またはTrust Manager APIを使用してプログラムで追加されます。 (Trust Manager APIを [使用した秘密鍵証明書の読み込みを参照](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api))。

Forms Service APIを使用する場合は、実行時のオ `GenerateServerAppearance` プションをに設定しま `true`す。 この実行時オプションを使用すると、AcrobatまたはAdobe readerで開いた場合に、サーバー上で生成されたフォームの外観が有効なままになります。 Forms APIを使用して署名するインタラクティブフォームを生成する場合は、この実行時オプションを設定することをお勧めします。

>[!NOTE]
>
>インタラクティブフォームのデジタル署名を読む前に、PDFドキュメントへの署名に関する知識があることをお勧めします。 (See [Digitally Signing PDF Documents](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)

### 手順の概要 {#summary_of_steps-4}

Formsサービスが返すインタラクティブフォームに電子署名するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Forms &amp; Signaturesクライアントを作成します。
1. Formsサービスを使用してインタラクティブフォームを取得します。
1. インタラクティブフォームに署名します。
1. 署名済みPDFドキュメントをPDFファイルとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-forms-client.jar
* adobe-utilities.jar（AEM FormsがJBossにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsをJBossにデプロイする場合に必要）

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Forms &amp; Signaturesクライアントの作成**

このワークフローはFormsサービスとSignatureサービスの両方を呼び出すので、FormsサービスクライアントとSignatureサービスクライアントの両方を作成します。

**Formsサービスを使用してインタラクティブフォームを取得する**

Formsサービスを使用して、署名するインタラクティブPDFフォームを取得できます。 AEM formsでは、レンダリングするフォームを含むForms `com.adobe.idp.Document` サービスにオブジェクトを渡すことができます。 このメソッドの名前はです `renderPDFForm2`。 このメソッドは、署名する `com.adobe.idp.Document` フォームを含むオブジェクトを返します。 このインスタンスはSignature `com.adobe.idp.Document` サービスに渡すことができます。

同様に、Webサービスを使用している場合は、Formsサービスが返すイ `BLOB` ンスタンスをSignatureサービスに渡すことができます。

>[!NOTE]
>
>「インタラクティブフォームに電子署名」セクションに関連付けられたクイックスタートが、このメソッドを呼び `renderPDFForm2` 出します。

**インタラクティブフォームへの署名**

PDFドキュメントに署名する場合、Signatureサービスで使用する実行時オプションを設定できます。 次のオプションを設定できます。

* 外観オプション
* 失効確認
* タイムスタンプ値

外観オプションは、オブジェクトを使用して設定 `PDFSignatureAppearanceOptionSpec` します。 例えば、オブジェクトのメソッドを呼び出して渡すことで、署名内に日 `PDFSignatureAppearanceOptionSpec` 付を表示するこ `setShowDate` とができま `true`す。

**署名済みPDFドキュメントの保存**

SignatureサービスがPDFドキュメントに電子署名した後、そのドキュメントをPDFファイルとして保存できます。 PDFファイルは、AcrobatまたはAdobe Readerで開くことができます。

**関連トピック**

[Java APIを使用したインタラクティブフォームへの電子署名](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-java-api)

[WebサービスAPIを使用してインタラクティブフォームに電子署名する](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDFドキュメントへのデジタル署名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[インタラクティブPDFフォームのレンダリング](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms)

### Java APIを使用したインタラクティブフォームへの電子署名 {#digitally-sign-an-interactive-form-using-the-java-api}

Forms and Signature API(Java)を使用してインタラクティブフォームに電子署名します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-signatures-client.jarやadobe-forms-client.jarなどのクライアントJARファイルを含めます。

1. Forms &amp; Signaturesクライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `SignatureServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `FormsServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. Formsサービスを使用してインタラクティブフォームを取得する

   * コンストラ `java.io.FileInputStream` クターを使用して、Formsサービスに渡すPDFドキュメントを表すオブジェクトを作成します。 PDFドキュメントの場所を指定するstring値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。
   * コンストラク `java.io.FileInputStream` ターを使用して、Formsサービスに渡すフォームデータを含むXMLドキュメントを表すオブジェクトを作成します。 XMLファイルの場所を指定するstring値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。
   * 実行時オプシ `PDFFormRenderSpec` ョンの設定に使用するオブジェクトを作成します。 オブジェクト `PDFFormRenderSpec` のメソッドを呼び出 `setGenerateServerAppearance` して渡しま `true`す。
   * オブジェクト `FormsServiceClient` のメソッドを `renderPDFForm2` 呼び出し、次の値を渡します。

      * レンダリング `com.adobe.idp.Document` するPDFフォームを含むオブジェクトです。
      * フォーム `com.adobe.idp.Document` とマージするデータを含むオブジェクトです。
      * 実行時 `PDFFormRenderSpec` のオプションを格納するオブジェクトです。
      * Formsサ `URLSpec` ービスに必要なURI値を含むオブジェクトです。 このパラメータ `null` ー値を指定できます。
      * 添付フ `java.util.HashMap` ァイルを格納するオブジェクト。 これはオプションのパラメーターで、フォームにフ `null` ァイルを添付しないかどうかを指定できます。
      このメソ `renderPDFForm2` ッドは、フォームデ `FormsResult` ータストリームを含むオブジェクトを返します

   * オブジェクトのメソッドを呼び出して、PDF `FormsResult` フォームを取得 `getOutputContent` します。 このメソッドは、インタラクティブ `com.adobe.idp.Document` フォームを表すオブジェクトを返します。


1. インタラクティブフォームへの署名

   オブジェクトのメソッドを呼び出し、次 `SignatureServiceClient` の値を渡して、PDF `sign` ドキュメントに署名します。

   * A `com.adobe.idp.Document` object that represents the PDF document to sign. このオブジェクトがFormsサービスから取得 `com.adobe.idp.Document` されたオブジェクトであることを確認します。
   * 署名された署名フィールドの名前を表すstring値です。
   * A `Credential` object that represents the credential that is used to digitally sign the PDF document. オブジェクト `Credential` の静的メソッドを呼び出し `Credential` て、オブジェクトを作成 `getInstance` します。 セキュリティ秘密鍵証明書に対応するエイリアス値を指定するstring値を渡します。
   * PDFドキ `HashAlgorithm` ュメントのダイジェストの作成に使用するハッシュアルゴリズムを表す静的データメンバーを指定するオブジェクトです。 例えば、SHA1アルゴリズムを `HashAlgorithm.SHA1` 使用するように指定できます。
   * PDFドキュメントが電子署名された理由を表すstring値です。
   * 署名者の連絡先情報を表すstring値です。
   * 電子署 `PDFSignatureAppearanceOptions` 名の外観を制御するオブジェクトです。 例えば、このオブジェクトを使用して、電子署名にカスタムロゴを追加できます。
   * 署名者 `java.lang.Boolean` の証明書に対して失効確認を実行するかどうかを指定するオブジェクトです。
   * オンラ `OCSPPreferences` イン証明書ステータスプロトコル(OCSP)サポートの環境設定を格納するオブジェクトです。 失効確認が行われない場合、このパラメーターは使用されず、指定できま `null`す。
   * 証明書 `CRLPreferences` 失効リスト(CRL)の環境設定を格納するオブジェクトです。 失効確認が行われない場合、このパラメーターは使用されず、指定できま `null`す。
   * タイム `TSPPreferences` スタンププロバイダー(TSP)サポートの環境設定を格納するオブジェクトです。 このパラメーターはオプションで、を指定できま `null`す。
   このメソ `sign` ッドは、署名済みPDFド `com.adobe.idp.Document` キュメントを表すオブジェクトを返します。

1. 署名済みPDFドキュメントの保存

   * Create a `java.io.File` object and ensure that the filename extension is .pdf.
   * Invoke the `com.adobe.idp.Document` object’s `copyToFile` method and pass `java.io.File`to copy the contents of the `Document` object to the file. メソッドが返したオブジェクト `com.adobe.idp.Document` を使用しているこ `sign` とを確認します。

**関連トピック**

[インタラクティブフォームへの電子署名](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[クイックスタート（SOAPモード）:Java APIを使用したPDFドキュメントへの電子署名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用してインタラクティブフォームに電子署名する {#digitally-sign-an-interactive-form-using-the-web-service-api}

Forms and Signature API（Webサービス）を使用してインタラクティブフォームに電子署名します。

1. プロジェクトファイルを含める

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 このクライアントアプリケーションは2つのAEM Formsサービスを呼び出すので、2つのサービス参照を作成します。 Signatureサービスに関連付けられているサービス参照に対して、次のWSDL定義を使用します。 `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   Formsサービスに関連付けられているサービス参照に対して、次のWSDL定義を使用します。 `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   このデータ `BLOB` 型は両方のサービス参照に共通なので、使用する際にはデータ型 `BLOB` を完全に修飾してください。 対応するWebサービスのクイックスタートでは、すべてのインスタ `BLOB` ンスが完全修飾されています。

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. Forms &amp; Signaturesクライアントの作成

   * Create a `SignatureServiceClient` object by using its default constructor.
   * Create a `SignatureServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/SignatureService?WSDL`)に渡すstring値。 属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。)
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `SignatureServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `SignatureServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `SignatureServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
   * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。
   >[!NOTE]
   >
   >Formsサービスクライアントに対してこれらの手順を繰り返します。

1. Formsサービスを使用してインタラクティブフォームを取得する

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、署名済みのPDFドキュメントを保存するために使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、署名するPDFドキュメントのファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイト配列、開 `System.IO.FileStream` 始位置、ストリ `Read` ーム長を渡すことによって、バイト配列にストリームデータを設定します。
   * オブジェクトにバ `BLOB` イト配列の内容をプロ `MTOM` パティに割り当てて、オブジェクトを設定します。
   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオブ `BLOB` ジェクトは、フォームデータの保存に使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、フォームデータを含むXMLファイルのファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイト配列、開 `System.IO.FileStream` 始位置、ストリ `Read` ーム長を渡すことによって、バイト配列にストリームデータを設定します。
   * オブジェクトにバ `BLOB` イト配列の内容をプロ `MTOM` パティに割り当てて、オブジェクトを設定します。
   * 実行時オプシ `PDFFormRenderSpec` ョンの設定に使用するオブジェクトを作成します。 値をオブジェクト `true` のフィールド `PDFFormRenderSpec` に割り当て `generateServerAppearance` ます。
   * オブジェクト `FormsServiceClient` のメソッドを `renderPDFForm2` 呼び出し、次の値を渡します。

      * レンダリング `BLOB` するPDFフォームを含むオブジェクトです。
      * フォーム `BLOB` とマージするデータを含むオブジェクトです。
      * 実行時 `PDFFormRenderSpec` のオプションを格納するオブジェクトです。
      * Formsサ `URLSpec` ービスに必要なURI値を含むオブジェクトです。 このパラメータ `null` ー値を指定できます。
      * 添付フ `java.util.HashMap` ァイルを格納するオブジェクト。 これはオプションのパラメーターで、フォームにフ `null` ァイルを添付しないかどうかを指定できます。
      * フォーム内のページ数の保存に使用される長い出力パラメーター。
      * ロケール値に使用される文字列出力パラメーター。
      * イン `FormResult` タラクティブフォームの保存に使用される出力パラメーターです。
   * オブジェクトのフィールドを呼び出してPDF `FormsResult` フォームを取得 `outputContent` します。 このフィールドには、インタラクティブ `BLOB` フォームを表すオブジェクトが格納されます。


1. インタラクティブフォームへの署名

   オブジェクトのメソッドを呼び出し、次 `SignatureServiceClient` の値を渡して、PDF `sign` ドキュメントに署名します。

   * A `BLOB` object that represents the PDF document to sign. Formsサービスから `BLOB` 返されるインスタンスを使用します。
   * 署名された署名フィールドの名前を表すstring値です。
   * A `Credential` object that represents the credential that is used to digitally sign the PDF document. オブジェクト `Credential` を作成するには、そのコンストラクターを使用し、オブジェクトのプロパティに値を割り当て `Credential` てエイリアスを指定 `alias` します。
   * PDFドキ `HashAlgorithm` ュメントのダイジェストの作成に使用するハッシュアルゴリズムを表す静的データメンバーを指定するオブジェクトです。 例えば、SHA1アルゴリズムを `HashAlgorithm.SHA1` 使用するように指定できます。
   * ハッシュアルゴリズムを使用するかどうかを指定するBoolean値です。
   * PDFドキュメントが電子署名された理由を表すstring値です。
   * 署名者の場所を表すstring値です。
   * 署名者の連絡先情報を表すstring値です。
   * 電子署 `PDFSignatureAppearanceOptions` 名の外観を制御するオブジェクトです。 例えば、このオブジェクトを使用して、電子署名にカスタムロゴを追加できます。
   * 署名者 `System.Boolean` の証明書に対して失効確認を実行するかどうかを指定するオブジェクトです。 この失効確認が行われると、署名に埋め込まれます。 デフォルトは、`false` です。
   * オンラ `OCSPPreferences` イン証明書ステータスプロトコル(OCSP)サポートの環境設定を格納するオブジェクトです。 失効確認が行われない場合、このパラメーターは使用されず、指定できま `null`す。 このオブジェクトに関する詳細は、『 [AEM Forms APIリファレンス』を参照してください](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   * 証明書 `CRLPreferences` 失効リスト(CRL)の環境設定を格納するオブジェクトです。 失効確認が行われない場合、このパラメーターは使用されず、指定できま `null`す。
   * タイム `TSPPreferences` スタンププロバイダー(TSP)サポートの環境設定を格納するオブジェクトです。 このパラメーターはオプションで、を指定できま `null`す。
   このメソ `sign` ッドは、署名済みPDFド `BLOB` キュメントを表すオブジェクトを返します。

1. 署名済みPDFドキュメントの保存

   * Create a `System.IO.FileStream` object by invoking its constructor. 署名済みPDFドキュメントのファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * メソッドによって返されたオブジェクトの内容を格納 `BLOB` するバイト配列を作成し `sign` ます。 オブジェクトのデータメンバーの値を取得して、バ `BLOB` イト配列を `MTOM` 設定します。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡すことで、バ `System.IO.BinaryWriter` イト配列の内 `Write` 容をPDFファイルに書き込みます。

**関連トピック**

[インタラクティブフォームへの電子署名](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## PDF ドキュメントの認証 {#certifying-pdf-documents}

認証署名と呼ばれる特定のタイプの署名によって PDF ドキュメントを認証することで、PDF ドキュメントを保護することができます。認証署名は、以下の方法で電子署名と区別されます。

* 認証署名は PDF ドキュメントに適用される最初の署名です。つまり、認証署名が適用されるときは、ドキュメント内の他の署名フィールドは未署名でなければいけません。認証署名は 1 つの PDF ドキュメントにつき 1 つです。PDF ドキュメントを署名および認証するには、署名の前に認証を行う必要があります。PDF ドキュメントの認証後、他の署名フィールドに電子署名を行うことができます。
* ドキュメントの作成者または発信者は、認証署名を無効にすることなく、特定の方法でドキュメントの変更が可能になるように指定することができます。例えば、フォームへの入力やコメント入力を許可するドキュメントなどがあります。作成者が特定の変更を許可しないように設定を行った場合は、Acrobat はユーザーのその方法によるドキュメントの変更を制限します。別のアプリケーションを使用するなどしてそのような変更が行われた場合は、認証署名は無効となり、Acrobat はユーザーがドキュメントを開いた際に警告を発します。（未認証の署名では、変更を防ぐことはできません。また、通常の編集操作では元の署名は無効になりません。）
* 署名時に、ドキュメントのコンテンツにあいまいさや誤解をもたらす可能性のある、特定の種類のコンテンツをスキャンします。例えば、注釈により、認証される対象を把握するために重要なページ上のテキストが隠れてしまう場合があります。そのようなコンテンツに関する、説明（法的証明）を提供することができます。

SignatureサービスJava APIまたはSignature webサービスAPIを使用して、PDFドキュメントをプログラムで認証できます。 PDFドキュメントを認証する場合は、秘密鍵証明書サービスに存在するセキュリティ秘密鍵証明書を参照する必要があります。 セキュリティ証明書について詳しくは、使用しているアプリケーシ *ョンサーバー版の『AEM Formsのインストール* およびデプロイ』ガイドを参照してください。

>[!NOTE]
>
>同じPDFドキュメントを認証および署名する場合、認証署名が信頼されていないと、AcrobatまたはAdobe ReaderでPDFドキュメントを開くと、最初の署名の横に黄色い三角形が表示されます。 この状況を避けるには、認証署名を信頼する必要があります。

>[!NOTE]
>
>PDFドキュメントの署名や認証にnCipher nShield HSM秘密鍵証明書を使用する場合、AEM FormsがデプロイされているJ2EEアプリケーションサーバーを再起動するまで、新しい秘密鍵証明書は使用できません。 ただし、設定値を設定すると、J2EEアプリケーションサーバーを再起動しなくても、署名または認証の操作が機能します。

次の設定値をcknfastrcファイルに追加できます。このファイルは/opt/nfast/cknfastrc(またはc:\nfast\cknfastrc)にあります。

```as3
             CKNFAST_ASSUME_SINGLE_PROCESS=0
```

この設定値をcknfastrcファイルに追加した後、新しい秘密鍵証明書は、J2EEアプリケーションサーバーを再起動しなくても使用できます。

>[!NOTE]
>
>Signatureサービスとドキュメントの認証について詳しくは、『AEM Formsサービスリファレ [ンス』を参照してください](https://www.adobe.com/go/learn_aemforms_services_63)。

### 手順の概要 {#summary_of_steps-5}

PDFドキュメントを認証するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. 署名クライアントを作成します。
1. 認証するPDFドキュメントを取得します。
1. PDFドキュメントを認証します。
1. 認証済みPDFドキュメントをPDFファイルとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar（AEM FormsがJBossにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsをJBossにデプロイする場合に必要）

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**署名クライアントの作成**

プログラムでSignature操作を実行する前に、Signatureクライアントを作成する必要があります。

**認証するPDFドキュメントの取得**

PDFドキュメントを認証するには、署名フィールドを含むPDFドキュメントを取得する必要があります。 PDFドキュメントに署名フィールドが含まれていない場合は、認証できません。 署名フィールドは、Designerを使用して追加することも、プログラムを使用して追加することもできます。 プログラムによる署名フィールドの追加について詳しくは、「署名フィールドの追 [加」を参照してくださ](digitally-signing-certifying-documents.md#adding-signature-fields)い。

**PDFドキュメントの認証**

PDFドキュメントを正常に認証するには、PDFドキュメントの認証にSignatureサービスで使用される次の入力値が必要です。

* **PDFドキュメント**:署名フィールドを含むPDFドキュメント。認証署名のグラフィック表現を含むフォームフィールドです。 PDFドキュメントを認証するには、署名フィールドがPDFドキュメントに含まれている必要があります。 署名フィールドは、Designerを使用して追加することも、プログラムを使用して追加することもできます。 (Adding [Signature Fieldsを参照](digitally-signing-certifying-documents.md#adding-signature-fields))。
* **署名フィールド名**:認証される署名フィールドの完全修飾名です。 次に例を示します。 `form1[0].#subform[1].SignatureField3[3]`. XFAフォームフィールドを使用する場合、署名フィールドの名前の一部を使用することもできます。 `SignatureField3[3]`. フィールド名にnull値が渡されると、非表示の署名フィールドが動的に作成され、認証されます。
* **セキュリティ証明書**:PDFドキュメントの認証に使用される秘密鍵証明書です。 このセキュリティ証明書には、パスワードとエイリアスが含まれています。これは、秘密鍵証明書サービス内の秘密鍵証明書に表示されるエイリアスと一致する必要があります。 エイリアスは、PKCS#12ファイル（.pfx拡張子付き）またはハードウェアセキュリティモジュール(HSM)内にある実際の秘密鍵証明書への参照です。
* **ハッシュアルゴリズム**:PDFドキュメントのダイジェストの作成に使用するハッシュアルゴリズムです。
* **署名の理由**:他のユーザーがPDFドキュメントが認証された理由を知るためにAcrobatまたはAdobe Readerで表示される値です。
* **署名者の場所**:秘密鍵証明書で指定された署名者の場所です。
* **連絡先情報**:署名者の住所や電話番号などの連絡先情報。
* **権限情報**:認証署名を無効にすることなく、エンドユーザーがドキュメントに対して実行できるアクションを制御する権限です。 例えば、PDFドキュメントを変更すると認証署名が無効になるように権限を設定できます。
* **法的説明**:ドキュメントを認証すると、ドキュメントのコンテンツが曖昧で紛らわしいものになる可能性のある特定の種類のコンテンツが自動的にスキャンされます。 例えば、注釈により、認証される対象を把握するために重要なページ上のテキストが隠れてしまう場合があります。スキャン処理では、これらのタイプのコンテンツに関する警告が生成されます。 この値は、警告が生成された可能性のあるコンテンツに関する追加の説明を提供します。
* **外観オプション**:認証署名の外観を制御するオプションです。 例えば、認証署名に日付情報を表示できます。
* **失効確認**:この値は、署名者の証明書に対して失効確認を行うかどうかを指定します。 デフォルト設定ので `false` は、失効確認は行われません。
* **OCSP settings**:PDFドキュメントの認証に使用される秘密鍵証明書のステータスに関する情報を提供する、オンライン証明書ステータスプロトコル(OCSP)サポートの設定です。 例えば、PDFドキュメントへのサインオンに使用する秘密鍵証明書に関する情報を提供するサーバーのURLを指定できます。
* **CRL settings**:失効確認が実行された場合の証明書失効リスト(CRL)の環境設定です。 例えば、秘密鍵証明書が失効したかどうかを常に確認するように指定できます。
* **タイムスタンプ**:認証署名に適用されるタイムスタンプ情報を定義する設定です。 タイムスタンプは、特定の時間の前に特定のデータが確立されたことを示します。 この知識は、署名者と検証者の間に信頼関係を構築するのに役立ちます。

**認証済みPDFドキュメントをPDFファイルとして保存**

SignatureサービスがPDFドキュメントを認証した後、PDFファイルとして保存し、ユーザーがAcrobatまたはAdobe Readerで開けるようにすることができます。

**関連トピック**

[Java APIを使用したPDFドキュメントの認証](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-java-api)

[WebサービスAPIを使用したPDFドキュメントの認証](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[署名フィールドの追加](digitally-signing-certifying-documents.md#adding-signature-fields)

### Java APIを使用したPDFドキュメントの認証 {#certify-pdf-documents-using-the-java-api}

署名API(Java)を使用してPDFドキュメントを認証します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-signatures-client.jarなどのクライアントJARファイルを含めます。

1. 署名クライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `SignatureServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 認証するPDFドキュメントの取得

   * コンストラ `java.io.FileInputStream` クターを使用し、PDFドキュメントの場所を指定するstring値を渡して、認証するPDFドキュメントを表すオブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PDFドキュメントの認証

   オブジェクトのメソッドを呼び出し、次 `SignatureServiceClient` の値を渡して、PDF `certify` ドキュメントを認証します。

   * 認証す `com.adobe.idp.Document` るPDFドキュメントを表すオブジェクトです。
   * 署名を含む署名フィールドの名前を表すstring値です。
   * A `Credential` object that represents the credential that is used to certify the PDF document. オブジェクト `Credential` を作成するには、オ `Credential` ブジェクトの静的メソッドを呼び出 `getInstance` し、セキュリティ秘密鍵証明書に対応するエイリアス値を指定するstring値を渡します。
   * PDFドキ `HashAlgorithm` ュメントのダイジェストの作成に使用されるハッシュアルゴリズムを表す静的データメンバーを指定するオブジェクトです。 例えば、SHA1アルゴリズムを `HashAlgorithm.SHA1` 使用するように指定できます。
   * PDFドキュメントが認証された理由を表すstring値です。
   * 署名者の連絡先情報を表すstring値です。
   * 署名を `MDPPermissions` 無効にするPDFドキュメントに対して実行できるアクションを指定するオブジェクトです。
   * 認証 `PDFSignatureAppearanceOptions` 署名の外観を制御するオブジェクトです。 必要に応じて、などのメソッドを呼び出して、署名の外観を変更します `setShowDate`。
   * 署名を無効にするアクションについての説明を提供するstring値です。
   * 署名者 `java.lang.Boolean` の証明書に対して失効確認を実行するかどうかを指定するオブジェクトです。 この失効確認が行われると、署名に埋め込まれます。 デフォルトは、`false` です。
   * 認証さ `java.lang.Boolean` れる署名フィールドがロックされているかどうかを指定するオブジェクトです。 フィールドをロックすると、署名フィールドは読み取り専用としてマークされ、プロパティを変更できず、必要な権限を持たないユーザーはこのフィールドをクリアできません。 デフォルトは、`false` です。
   * オンラ `OCSPPreferences` イン証明書ステータスプロトコル(OCSP)サポートの環境設定を格納するオブジェクトです。 失効確認が行われない場合、このパラメーターは使用されず、指定できま `null`す。 このオブジェクトについて詳しくは、『 [AEM Forms APIリファレンス』を参照してください](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   * 証明書 `CRLPreferences` 失効リスト(CRL)の環境設定を格納するオブジェクトです。 失効確認が行われない場合、このパラメーターは使用されず、指定できま `null`す。
   * タイム `TSPPreferences` スタンププロバイダー(TSP)サポートの環境設定を格納するオブジェクトです。 例えば、オブジェクトを作成し `TSPPreferences` た後、オブジェクトのメソッドを呼び出して、TSPサーバーのURLを設 `TSPPreferences` 定でき `setTspServerURL` ます。 このパラメーターはオプションで、を指定できま `null`す。 For more information, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).
   このメソ `certify` ッドは、認証済みPDF `com.adobe.idp.Document` ドキュメントを表すオブジェクトを返します。

1. 認証済みPDFドキュメントをPDFファイルとして保存

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が .pdf であることを確認します。
   * Invoke the `com.adobe.idp.Document` object’s `copyToFile` method to copy the contents of the `com.adobe.idp.Document` object to the file.

**関連トピック**

[PDF ドキュメントの認証](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[クイックスタート（SOAPモード）:Java APIを使用したPDFドキュメントの認証](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-certifying-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したPDFドキュメントの認証 {#certify-pdf-documents-using-the-web-service-api}

Signature API（Webサービス）を使用してPDFドキュメントを認証します。

1. プロジェクトファイルを含める

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. 署名クライアントの作成

   * Create a `SignatureServiceClient` object by using its default constructor.
   * Create a `SignatureServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/SignatureService?WSDL`)に渡すstring値。 属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。)
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `SignatureServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `SignatureServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `SignatureServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. 認証するPDFドキュメントの取得

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、認証済みのPDFドキュメントの保存に使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、認証するPDFドキュメントのファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイト配列、開 `System.IO.FileStream` 始位置、ストリ `Read` ーム長を渡すことによって、バイト配列にストリームデータを設定します。
   * データメンバ `BLOB` ーにバイト配列の内容を割り `MTOM` 当てて、オブジェクトを入力します。

1. PDFドキュメントの認証

   オブジェクトのメソッドを呼び出し、次 `SignatureServiceClient` の値を渡して、PDF `certify` ドキュメントを認証します。

   * 認証す `BLOB` るPDFドキュメントを表すオブジェクトです。
   * 署名を含む署名フィールドの名前を表すstring値です。
   * A `Credential` object that represents the credential that is used to certify the PDF document. オブジェクト `Credential` を作成するには、そのコンストラクターを使用し、オブジェクトのプロパティに値を割り当て `Credential` てエイリアスを指定 `alias` します。
   * PDFドキ `HashAlgorithm` ュメントのダイジェストの作成に使用されるハッシュアルゴリズムを表す静的データメンバーを指定するオブジェクトです。 例えば、SHA1アルゴリズムを `HashAlgorithm.SHA1` 使用するように指定できます。
   * ハッシュアルゴリズムを使用するかどうかを指定するBoolean値です。
   * PDFドキュメントが認証された理由を表すstring値です。
   * 署名者の場所を表すstring値です。
   * 署名者の連絡先情報を表すstring値です。
   * 署名を `MDPPermissions` 無効にするPDFドキュメントで実行できるアクションを指定する、オブジェクトの静的データメンバーです。
   * 前のパラメーター値として渡されたオブジ `MDPPermissions` ェクトを使用するかどうかを指定するBoolean値です。
   * 署名を無効にするアクションを説明するstring値です。
   * 認証 `PDFSignatureAppearanceOptions` 署名の外観を制御するオブジェクトです。 コンストラクタを使用して `PDFSignatureAppearanceOptions` オブジェクトを作成します。データメンバーの1つを設定することで、署名の外観を変更できます。
   * 署名者 `System.Boolean` の証明書に対して失効確認を実行するかどうかを指定するオブジェクトです。 この失効確認が行われると、署名に埋め込まれます。 デフォルトは、`false` です。
   * 認証さ `System.Boolean` れる署名フィールドがロックされているかどうかを指定するオブジェクトです。 フィールドをロックすると、署名フィールドは読み取り専用としてマークされ、プロパティを変更できず、必要な権限を持たないユーザーはこのフィールドをクリアできません。 デフォルトは、`false` です。
   * 署名フ `System.Boolean` ィールドをロックするかどうかを指定するオブジェクトです。 つまり、前のパラメーター `true` に渡した場合は、このパラメーター `true` に渡します。
   * オンラ `OCSPPreferences` イン証明書ステータスプロトコル(OCSP)サポートの環境設定を格納するオブジェクトです。PDFドキュメントの認証に使用される秘密鍵証明書のステータスに関する情報を提供します。 失効確認が行われない場合、このパラメーターは使用されず、指定できま `null`す。
   * 証明書 `CRLPreferences` 失効リスト(CRL)の環境設定を格納するオブジェクトです。 失効確認が行われない場合、このパラメーターは使用されず、指定できま `null`す。
   * タイム `TSPPreferences` スタンププロバイダー(TSP)サポートの環境設定を格納するオブジェクトです。 例えば、オブジェクトを作成し `TSPPreferences` た後に、オブジェクトのデータメンバーを設定して、TSPのURL `TSPPreferences` を設定で `tspServerURL` きます。 このパラメーターはオプションで、を指定できま `null`す。
   このメソ `certify` ッドは、認証済みPDF `BLOB` ドキュメントを表すオブジェクトを返します。

1. 認証済みPDFドキュメントをPDFファイルとして保存

   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、認証済みPDFドキュメントを含むPDFドキュメントのファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * メソッドによって返されたオブジェクトの内容を格納 `BLOB` するバイト配列を作成し `certify` ます。 オブジェクトのデータメンバーの値を取得して、バ `BLOB` イト配列を `binaryData` 設定します。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡すことで、バ `System.IO.BinaryWriter` イト配列の内 `Write` 容をPDFファイルに書き込みます。

**関連トピック**

[PDF ドキュメントの認証](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Verifying Digital Signatures {#verifying-digital-signatures}

電子署名を検証することで、署名された PDF ドキュメントに変更がなく、電子署名が有効であることを確認することができます。電子署名を検証する際に、署名のステータスや、署名者のIDなどの署名のプロパティを確認できます。 電子署名を信用する前に、検証することをおすすめします。電子署名を検証する際、電子署名を含む PDF ドキュメントを参照します。

署名者のIDが不明であるとします。 次の図に示すように、PDFドキュメントをAcrobatで開くと、署名者のIDが不明であることを示す警告メッセージが表示されます。

![vd_vd_verifysig](assets/vd_vd_verifysig.png)

同様に、プログラムで電子署名を検証する場合、署名者のIDのステータスを判断できます。 例えば、前の図に示したドキュメントの電子署名を検証した場合、署名者のIDが不明になります。

>[!NOTE]
>
>Signatureサービスと電子署名の検証について詳しくは、『AEM Formsサービスリファレ [ンス』を参照してください](https://www.adobe.com/go/learn_aemforms_services_63)。

### 手順の概要 {#summary_of_steps-6}

電子署名を検証するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. 署名クライアントを作成します。
1. 検証する署名が含まれているPDFドキュメントを取得します。
1. PKIランタイムオプションを設定します。
1. 電子署名を検証します。
1. 署名のステータスを決定します。
1. 署名者のIDを特定します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを含めます。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar（AEM FormsがJBossにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsをJBossにデプロイする場合に必要）

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**署名クライアントの作成**

プログラムでSignatureサービス操作を実行する前に、Signatureサービスクライアントを作成します。

**検証する署名が含まれているPDFドキュメントの取得**

PDFドキュメントのデジタル署名または認証に使用される署名を検証するには、署名を含むPDFドキュメントを取得します。

**PKIランタイムオプションの設定**

PDFドキュメントの署名を検証する際にSignatureサービスで使用するPKIランタイムオプションを設定します。

* 検証時刻
* 失効確認
* タイムスタンプ値

これらのオプションの設定の一環として、検証時間を指定できます。 例えば、現在の時間（バリデーターのコンピューター上の時間）を選択し、現在の時間を使用するように指定できます。 異なる時間値について詳しくは、『 `VerificationTime` AEM Forms API Reference』の列挙値を参照してください [](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

また、検証プロセスの一環として失効確認を実行するかどうかを指定することもできます。 例えば、証明書が失効しているかどうかを判断するために失効確認を実行できます。 失効確認オプションについて詳しくは、『 `RevocationCheckStyle` AEM Forms API Reference』の列挙値を参照してください [](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

証明書に対して失効確認を実行するには、オブジェクトを使用して、証明書失効リスト(CRL)サーバーのURLを指定 `CRLOptionSpec` します。 ただし、CRLサーバーへのURLを指定しない場合、Signatureサービスは証明書からURLを取得します。

失効確認を実行する際は、CRLサーバーを使用する代わりに、オンライン証明書ステータスプロトコル(OCSP)サーバーを使用できます。 通常、CRLサーバーとは異なり、OCSPサーバーを使用する場合、失効確認の実行時間が短縮されます。 (See [Online Certificate Status Protocol](https://tools.ietf.org/html/rfc2560).)

Signatureサービスで使用するCRLおよびOCSPサーバーの順序は、Adobe Applications and Servicesを使用して設定できます。 例えば、OCSPサーバーがAdobe Applications and Servicesで最初に設定されている場合は、OCSPサーバーが確認され、次にCRLサーバーが確認されます。

失効確認を実行しない場合、Signatureサービスは証明書が失効しているかどうかを確認しません。 つまり、CRLおよびOCSPサーバー情報は無視されます。

>[!NOTE]
>
>証明書で指定されたURLは、およびオブジェクトを使用して上書 `CRLOptionSpec` きでき `OCSPOptionSpec` ます。 例えば、CRLサーバーを上書きするには、オブジェクトのメソッド `CRLOptionSpec` を呼び出すことがで `setLocalURI` きます。

タイムスタンプとは、署名済みまたは認証済みのドキュメントが変更された時間を追跡するプロセスです。 ドキュメントが署名された後は、誰もドキュメントを変更できません。 タイムスタンプ機能を使用すると、署名済みまたは認証済みのドキュメントの有効性を強化できます。 オブジェクトを使用して、タイムスタンプオプションを設定 `TSPOptionSpec` できます。 例えば、タイムスタンププロバイダー(TSP)サーバーのURLを指定できます。

>[!NOTE]
>
>JavaおよびWebサービスのクイックスタートでは、検証時刻がに設定され、失 `VerificationTime.CURRENT_TIME` 効確認がに設定されま `RevocationCheckStyle.BestEffort`す。 CRLまたはOCSPサーバー情報が指定されていないので、サーバー情報は証明書から取得されます。

**電子署名の検証**

署名を正常に検証するには、署名が含まれる署名フィールドの完全修飾名を指定します（例：） `form1[0].#subform[1].SignatureField3[3]`。 XFAフォームフィールドを使用する場合は、署名フィールドの名前の一部を使用することもできます。 `SignatureField3`.

デフォルトでは、Signatureサービスは、検証後にドキュメントに署名できる時間を65分に制限します。 ユーザーが現在の時刻に署名を検証しようとし、署名時刻が現在の時刻より後で65分以内である場合、Signatureサービスは検証エラーを作成しません。

>[!NOTE]
>
>署名を検証する際に必要なその他の値については、『 [AEM Forms APIリファレンス』を参照してください](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

**署名のステータスの確認**

電子署名の検証の一環として、署名のステータスを確認できます。

**署名者のIDの確認**

署名者のIDを決定できます。次の値のいずれかを指定できます。

* **不明**:署名者の検証を実行できないため、署名者が不明です。
* **信頼済み**:この署名者は信頼できます。
* **信頼できない**:この署名者は信頼されていません。

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

1. 検証する署名が含まれているPDFドキュメントの取得

   * 検証する署 `java.io.FileInputStream` 名が含まれるPDFドキュメントを表すオブジェクトを、コンストラクターを使用して作成します。 PDFドキュメントの場所を指定するstring値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PKIランタイムオプションの設定

   * コンストラクタを使用して `PKIOptions` オブジェクトを作成します。
   * オブジェクトのメソッドを呼び出し、検 `PKIOptions` 証時間を指 `setVerificationTime` 定する列 `VerificationTime` 挙値を渡して、検証時間を設定します。
   * 失効確認オプションを設定するには、オブジェク `PKIOptions` トのメソッドを呼 `setRevocationCheckStyle` び出し、失効確認を実 `RevocationCheckStyle` 行するかどうかを指定する列挙値を渡します。

1. 電子署名の検証

   オブジェクトのメソッドを呼び出し、 `SignatureServiceClient` 次の値を渡 `verify2` して、署名を検証します。

   * デジタル `com.adobe.idp.Document` 署名されたPDFドキュメントまたは認証されたPDFドキュメントを含むオブジェクトです。
   * 検証する署名が含まれている署名フィールド名を表すstring値です。
   * PKI実行 `PKIOptions` 時オプションを含むオブジェクトです。
   * SPI情報 `VerifySPIOptions` を含むインスタンスです。 このパラメーター `null` を指定できます。
   このメ `verify2` ソッドは、電子署 `PDFSignatureVerificationInfo` 名の検証に使用できる情報を含むオブジェクトを返します。

1. 署名のステータスの確認

   * オブジェクトのメソッドを呼び出して、署名のス `PDFSignatureVerificationInfo` テータスを特定 `getStatus` します。 このメソッドは、署名のス `SignatureStatus` テータスを指定するオブジェクトを返します。 例えば、署名済みPDFドキュメントが変更されていない場合、このメソッドはを返しま `SignatureStatus.DocumentSigNoChanges`す。

1. 署名者のIDの確認

   * オブジェクトのメソッドを呼び出して、署名者のID `PDFSignatureVerificationInfo` を特定し `getSigner` ます。 このメソッドは、オブジェクトを `IdentityInformation` 返します。
   * オブジェクト `IdentityInformation` のメソッドを呼 `getStatus` び出して、署名者のIDを特定します。 このメソッドは、ID `IdentityStatus` を指定する列挙値を返します。 例えば、署名者が信頼できる場合、このメソッドはを返しま `IdentityStatus.TRUSTED`す。

**関連トピック**

[電子署名の検証](#verify-digital-signatures-using-the-java-api)

[クイックスタート（SOAPモード）:Java APIを使用した電子署名の検証](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-a-digital-signature-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用した電子署名の検証 {#verify-digital-signatures-using-the-web-service-api}

Signature Service API（Webサービス）を使用して電子署名を検証します。

1. プロジェクトファイルを含める

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. 署名クライアントの作成

   * Create a `SignatureServiceClient` object by using its default constructor.
   * Create a `SignatureServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/SignatureService?WSDL`)に渡すstring値。 属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。)
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `SignatureServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `SignatureServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `SignatureServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. 検証する署名が含まれているPDFドキュメントの取得

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、検証するデジタル署名または認証署名が含まれるPDFドキュメントの保存に使用されます。
   * Create a `System.IO.FileStream` object by invoking its constructor. 署名済みPDFドキュメントのファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出して、バイト配列にストリームデ `System.IO.FileStream` ータを入力 `Read` します。 読み取るバイト配列、開始位置およびストリーム長を渡します。
   * オブジェクトにバ `BLOB` イト配列の内容をプロ `MTOM` パティに割り当てて、オブジェクトを設定します。

1. PKIランタイムオプションの設定

   * コンストラクタを使用して `PKIOptions` オブジェクトを作成します。
   * 検証時間を設定するには、オブジェクトのデ `PKIOptions` ータメンバ `verificationTime` ーに検証時 `VerificationTime` 間を指定する列挙値を割り当てます。
   * 失効確認オプションを設定するには、オブジェクトのデ `PKIOptions` ータメンバーに失効確 `revocationCheckStyle` 認を実行する `RevocationCheckStyle` かどうかを指定する列挙値を割り当てます。

1. 電子署名の検証

   オブジェクトのメソッドを呼び出し、 `SignatureServiceClient` 次の値を渡 `verify2` して、署名を検証します。

   * デジタル `BLOB` 署名されたPDFドキュメントまたは認証されたPDFドキュメントを含むオブジェクトです。
   * 検証する署名が含まれている署名フィールド名を表すstring値です。
   * PKI実行 `PKIOptions` 時オプションを含むオブジェクトです。
   * SPI情報 `VerifySPIOptions` を含むインスタンスです。 このパラメーター `null` を指定できます。
   このメ `verify2` ソッドは、電子署 `PDFSignatureVerificationInfo` 名の検証に使用できる情報を含むオブジェクトを返します。

1. 署名のステータスの確認

   オブジェクトのデータメンバーの値を取得して、署名のス `PDFSignatureVerificationInfo` テータスを決 `status` 定します。 このデータメンバーは、署名の `SignatureStatus` ステータスを指定するオブジェクトを格納します。 例えば、署名済みPDFドキュメントが変更された場合、データメ `status` ンバーに値が格納されま `SignatureStatus.DocumentSigNoChanges`す。

1. 署名者のIDの確認

   * オブジェクトのデータメンバーの値を取得して、署名者のID `PDFSignatureVerificationInfo` を特定 `signer` します。 このメンバはオブジェクトを `IdentityInformation` 返します。
   * 署名者のID `IdentityInformation` を特定す `status` るオブジェクトのデータメンバーを取得します。 このデータメンバは、ID `IdentityStatus` を指定する列挙値を返します。 例えば、署名者が信頼できる場合、このメンバーはを返しま `IdentityStatus.TRUSTED`す。

**関連トピック**

[電子署名の検証](#verify-digital-signatures-using-the-java-api)

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Verifying Multiple Digital Signatures {#verifying-multiple-digital-signatures}

AEM Formsは、PDFドキュメント内のすべての電子署名を検証する手段を提供します。 PDFドキュメントに複数の電子署名が含まれているとします。これは、複数の署名者による署名が必要なビジネスプロセスの結果です。 例えば、融資担当者と管理者の両方の署名が必要な金融トランザクションについて考えてみましょう。 SignatureサービスのJava APIまたはWebサービスAPIを使用して、PDFドキュメント内のすべての署名を検証できます。 複数の署名を検証する際は、それぞれの署名のステータスやプロパティを確認できます。電子署名を信頼する前に、検証することをお勧めします。 単一の電子署名の検証について詳しく理解することをお勧めします。

>[!NOTE]
>
>Signatureサービスと電子署名の検証について詳しくは、『AEM Formsサービスリファレ [ンス』を参照してください](https://www.adobe.com/go/learn_aemforms_services_63)。

### 手順の概要 {#summary_of_steps-7}

複数の電子署名を検証するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. 署名クライアントを作成します。
1. 検証する署名が含まれているPDFドキュメントを取得します。
1. PKIランタイムオプションを設定します。
1. すべての電子署名を取得します。
1. すべての署名を繰り返し処理します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを含めます。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar（AEM FormsがJBossにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsをJBossにデプロイする場合に必要）

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**署名クライアントの作成**

プログラムでSignatureサービス操作を実行する前に、Signatureサービスクライアントを作成します。

**検証する署名が含まれているPDFドキュメントを取得します**

PDFドキュメントのデジタル署名または認証に使用される署名を検証するには、署名を含むPDFドキュメントを取得します。

**PKIランタイムオプションの設定**

PDFドキュメント内のすべての署名を検証する際にSignatureサービスで使用するPKIランタイムオプションを設定します。

* 検証時刻
* 失効確認
* タイムスタンプ値

これらのオプションの設定の一環として、検証時間を指定できます。 例えば、現在の時間（バリデーターのコンピューター上の時間）を選択し、現在の時間を使用するように指定できます。 異なる時間値について詳しくは、『 `VerificationTime` AEM Forms API Reference』の列挙値を参照してください [](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

また、検証プロセスの一環として失効確認を実行するかどうかを指定することもできます。 例えば、証明書が失効しているかどうかを判断するために失効確認を実行できます。 失効確認オプションについて詳しくは、『 `RevocationCheckStyle` AEM Forms API Reference』の列挙値を参照してください [](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

証明書に対して失効確認を実行するには、オブジェクトを使用して、証明書失効リスト(CRL)サーバーのURLを指定 `CRLOptionSpec` します。 ただし、CRLサーバーへのURLを指定しない場合、Signatureサービスは証明書からURLを取得します。

失効確認を実行する際は、CRLサーバーを使用する代わりに、オンライン証明書ステータスプロトコル(OCSP)サーバーを使用できます。 通常、CRLサーバーではなくOCSPサーバーを使用する場合、失効確認の実行時間が短縮されます。 (See [Online Certificate Status Protocol](https://tools.ietf.org/html/rfc2560).)

Signatureサービスで使用するCRLおよびOCSPサーバーの順序は、Adobe Applications and Servicesを使用して設定できます。 例えば、Adobe Applications and ServicesでOCSPサーバーが最初に設定されている場合は、OCSPサーバーが確認され、次にCRLサーバーが確認されます。

失効確認を実行しない場合、Signatureサービスは証明書が失効しているかどうかを確認しません。 つまり、CRLおよびOCSPサーバー情報は無視されます。

>[!NOTE]
>
>証明書で指定されたURLは、およびオブジェクトを使用して上書 `CRLOptionSpec` きでき `OCSPOptionSpec` ます。 例えば、CRLサーバーを上書きするには、オブジェクトのメソッド `CRLOptionSpec` を呼び出すことがで `setLocalURI` きます。

タイムスタンプとは、署名済みまたは認証済みのドキュメントが変更された時間を追跡するプロセスです。 ドキュメントが署名された後は、誰もドキュメントを変更できません。 タイムスタンプ機能を使用すると、署名済みまたは認証済みのドキュメントの有効性を強化できます。 タイムスタンプオプションは、オブジェクトを使用して設定で `TSPOptionSpec` きます。 例えば、タイムスタンププロバイダー(TSP)サーバーのURLを指定できます。

>[!NOTE]
>
>JavaおよびWebサービスのクイックスタートでは、検証時刻がに設定され、失 `VerificationTime.CURRENT_TIME` 効確認がに設定されま `RevocationCheckStyle.BestEffort`す。 CRLまたはOCSPサーバー情報が指定されていないので、サーバー情報は証明書から取得されます。

**すべての電子署名を取得する**

PDFドキュメント内のすべての電子署名を検証するには、PDFドキュメントから電子署名を取得します。 すべての署名がリストに返されます。 電子署名の検証中に、署名のステータスを確認します。

>[!NOTE]
>
>単一の電子署名を検証する場合とは異なり、複数の署名を検証する場合は、署名フィールド名を指定する必要はありません。

**すべての署名を繰り返し処理します**

各署名を繰り返し処理します。 つまり、各署名について、電子署名を検証し、署名者のIDと各署名のステータスを確認します。 (電子署名 [の検証を参照](#verify-digital-signatures-using-the-java-api))。

>[!NOTE]
>
>ドキュメント全体が必要な場合は、すべての署名を繰り返し実行する必要はありません。

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

   * 複数の電子署 `java.io.FileInputStream` 名を含むPDFドキュメントを表すオブジェクトを作成し、そのコンストラクターを使用して検証を行います。 PDFドキュメントの場所を指定するstring値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PKIランタイムオプションの設定

   * コンストラクタを使用して `PKIOptions` オブジェクトを作成します。
   * オブジェクトのメソッドを呼び出し、検 `PKIOptions` 証時間を指 `setVerificationTime` 定する列 `VerificationTime` 挙値を渡して、検証時間を設定します。
   * 失効確認オプションを設定するには、オブジェ `PKIOptions` クトのメソッドを呼び `setRevocationCheckStyle` 出し、失効確認を実 `RevocationCheckStyle` 行するかどうかを指定する列挙値を渡します。

1. すべての電子署名を取得する

   オブジェクト `SignatureServiceClient` のメソッドを `verifyPDFDocument` 呼び出し、次の値を渡します。

   * 複数の `com.adobe.idp.Document` 電子署名を含むPDFドキュメントを含むオブジェクトです。
   * PKI実行 `PKIOptions` 時オプションを含むオブジェクトです。
   * SPI情報 `VerifySPIOptions` を含むインスタンスです。 このパラメーター `null` を指定できます。
   このメソ `verifyPDFDocument` ッドは、PDFドキュ `PDFDocumentVerificationInfo` メント内のすべての電子署名に関する情報を含むオブジェクトを返します。

1. すべての署名を繰り返し処理します

   * オブジェクトのメソッドを呼び出して、すべて `PDFDocumentVerificationInfo` の署名を繰り返 `getVerificationInfos` します。 このメソッドは、各要素が `java.util.List` オブジェクトであるオブジェクトを返 `PDFSignatureVerificationInfo` します。 オブジェクト `java.util.Iterator` を使用して、署名のリストを繰り返し処理します。
   * オブジェクト `PDFSignatureVerificationInfo` を使用すると、オブジェクトのメソッドを呼び出して、署名のステータスを確認するなどのタス `PDFSignatureVerificationInfo` クを実行で `getStatus` きます。 このメソッドは、静的デ `SignatureStatus` ータ・メンバーが署名のステータスを通知するオブジェクトを戻します。 例えば、署名が不明な場合、このメソッドはを返します `SignatureStatus.DocumentSignatureUnknown`。

**関連トピック**

[複数の電子署名の検証](#verifying-multiple-digital-signatures)

[クイックスタート（SOAPモード）:Java APIを使用した複数の電子署名の検証](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-multiple-digital-signatures-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[電子署名の検証](#verify-digital-signatures-using-the-java-api)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用した複数の電子署名の検証 {#verifying-multiple-digital-signatures-using-the-web-service-api}

Signature Service API（Webサービス）を使用して複数の電子署名を検証します。

1. プロジェクトファイルを含める

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. 署名クライアントの作成

   * Create a `SignatureServiceClient` object by using its default constructor.
   * Create a `SignatureServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/SignatureService?WSDL`)に渡すstring値。 属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。)
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `SignatureServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `SignatureServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `SignatureServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. 検証する署名が含まれているPDFドキュメントを取得します

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオブジ `BLOB` ェクトは、検証する複数の電子署名を含むPDFドキュメントを保存します。
   * Create a `System.IO.FileStream` object by invoking its constructor. PDFドキュメントのファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出して、バイト配列にストリームデ `System.IO.FileStream` ータを入力 `Read` します。 読み取るバイト配列、開始位置およびストリーム長を渡します。
   * オブジェクトにバ `BLOB` イト配列の内容をプロ `MTOM` パティに割り当てて、オブジェクトを設定します。

1. PKIランタイムオプションの設定

   * コンストラクタを使用して `PKIOptions` オブジェクトを作成します。
   * 検証時間を設定するには、オブジェクトのデ `PKIOptions` ータメンバ `verificationTime` ーに検証時 `VerificationTime` 間を指定する列挙値を割り当てます。
   * 失効確認オプションを設定するには、オブジェクトのデ `PKIOptions` ータメンバーに失効確 `revocationCheckStyle` 認を実行する `RevocationCheckStyle` かどうかを指定する列挙値を割り当てます。

1. すべての電子署名を取得する

   オブジェクト `SignatureServiceClient` のメソッドを `verifyPDFDocument` 呼び出し、次の値を渡します。

   * 複数の `BLOB` 電子署名を含むPDFドキュメントを含むオブジェクトです。
   * PKI実行 `PKIOptions` 時オプションを含むオブジェクトです。
   * SPI情報 `VerifySPIOptions` を含むインスタンスです。 このパラメーターにはnullを指定できます。
   このメソ `verifyPDFDocument` ッドは、PDFドキュ `PDFDocumentVerificationInfo` メント内のすべての電子署名に関する情報を含むオブジェクトを返します。

1. すべての署名を繰り返し処理します

   * オブジェクトのデータメンバーを取得して、すべ `PDFDocumentVerificationInfo` ての署名を繰り返 `verificationInfos` し処理します。 このデータ・メンバは、各 `Object` 要素がオブジェクトである配列を返 `PDFSignatureVerificationInfo` します。
   * オブジェクト `PDFSignatureVerificationInfo` を使用すると、オブジェクトのデータメンバーを取得して、署名のステータスを確認するなどのタ `PDFSignatureVerificationInfo` スクを実 `status` 行できます。 このデータ・メンバーは、静的 `SignatureStatus` データ・メンバーが署名のステータスを通知するオブジェクトを戻します。 例えば、署名が不明な場合、このメソッドはを返します `SignatureStatus.DocumentSignatureUnknown`。

**関連トピック**

[複数の電子署名の検証](#verifying-multiple-digital-signatures)

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

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
1. 削除する署名を含むPDFドキュメントを取得します。
1. 署名フィールドから電子署名を削除します。
1. PDFドキュメントをPDFファイルとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar（AEM FormsがJBossにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsをJBossにデプロイする場合に必要）

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**署名クライアントの作成**

プログラムでSignatureサービス操作を実行する前に、Signatureサービスクライアントを作成する必要があります。

**削除する署名を含むPDFドキュメントの取得**

PDFドキュメントから署名を削除するには、署名が含まれるPDFドキュメントを取得する必要があります。

**署名フィールドからの電子署名の削除**

PDFドキュメントから電子署名を正常に削除するには、電子署名が含まれる署名フィールドの名前を指定する必要があります。 また、電子署名を削除する権限が必要です。それ以外の場合は、例外が発生します。

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

1. 削除する署名を含むPDFドキュメントの取得

   * コンストラ `java.io.FileInputStream` クターを使用し、PDFドキュメントの場所を指定するstring値を渡すことで、削除する署名が含まれるPDFドキュメントを表すオブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 署名フィールドからの電子署名の削除

   オブジェクトのメソッドを呼び出し、次の値を渡して、署 `SignatureServiceClient` 名フィールドか `clearSignatureField` ら電子署名を削除します。

   * 削除す `com.adobe.idp.Document` る署名が含まれているPDFドキュメントを表すオブジェクトです。
   * 電子署名が含まれる署名フィールドの名前を指定するstring値です。
   電子署 `clearSignatureField` 名が削除さ `com.adobe.idp.Document` れたPDFドキュメントを表すオブジェクトを返します。

1. PDFドキュメントをPDFファイルとして保存

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が .pdf であることを確認します。
   * オブジェクト `com.adobe.idp.Document` のメソッドを呼び出 `copyToFile` します。 オブジェクト `java.io.File` を渡して、オブジェクトの内容をフ `com.adobe.idp.Document` ァイルにコピーします。 `Document` メソッドから返された `clearSignatureField` オブジェクトを必ず使用してください。

**関連トピック**

[電子署名の削除](digitally-signing-certifying-documents.md#removing-digital-signatures)

[クイックスタート（SOAPモード）:Java APIを使用した電子署名の削除](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-removing-a-digital-signature-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用した電子署名の削除 {#remove-digital-signatures-using-the-web-service-api}

Signature API（Webサービス）を使用して電子署名を削除します。

1. プロジェクトファイルを含める

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. 署名クライアントの作成

   * Create a `SignatureServiceClient` object by using its default constructor.
   * Create a `SignatureServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLをAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/SignatureService?WSDL`)に渡すstring値。 属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。)
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得してオブジェクトを作成 `SignatureServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本HTTP認証を有効にします。

      * フィールドにAEM formsユーザー名を割り当てま `SignatureServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `SignatureServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールド `HttpClientCredentialType.Basic` に割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールド `BasicHttpSecurityMode.TransportCredentialOnly` に割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. 削除する署名を含むPDFドキュメントの取得

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、削除する電子署名が含まれるPDFドキュメントを保存するために使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、署名済みPDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出して、バイト配列にストリームデ `System.IO.FileStream` ータを入力 `Read` します。 読み取るバイト配列、開始位置およびストリーム長を渡します。
   * オブジェクト `BLOB` にバイト配列の内容をプロ `MTOM` パティに割り当てて、オブジェクトを設定します。

1. 署名フィールドからの電子署名の削除

   オブジェクトのメソッドを呼び出し、次 `SignatureServiceClient` の値を渡して、 `clearSignatureField` 電子署名を削除します。

   * 署名済 `BLOB` みPDFドキュメントを含むオブジェクトです。
   * 削除する電子署名が含まれる署名フィールドの名前を表すstring値です。
   電子署 `clearSignatureField` 名が削除さ `BLOB` れたPDFドキュメントを表すオブジェクトを返します。

1. PDFドキュメントをPDFファイルとして保存

   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、空の署名フィールドとファイルを開くモードを含むPDFドキュメントのファイルの場所を表すstring値を渡します。
   * メソッドによって返されたオブジェクトの内容を格納 `BLOB` するバイト配列を作成し `sign` ます。 オブジェクトのデータメンバーの値を取得して、バ `BLOB` イト配列を `MTOM` 設定します。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡すことで、バ `System.IO.BinaryWriter` イト配列の内 `Write` 容をPDFファイルに書き込みます。

**関連トピック**

[電子署名の削除](digitally-signing-certifying-documents.md#removing-digital-signatures)

[MTOMを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
