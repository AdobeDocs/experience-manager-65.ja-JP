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
source-git-commit: f9389a06f9c2cd720919486765cee76257f272c3

---


# デジタル署名と認証ドキュメント {#digitally-signing-and-certifying-documents}

**Signatureサービスについて**

Signatureサービスを使用すると、組織で配布および受信するAdobe PDFドキュメントのセキュリティとプライバシーを保護できます。 このサービスでは、電子署名と証明書を使用して、意図した受信者のみが署名を変更できるようにします。 セキュリティ機能はドキュメント自体に適用されるので、ドキュメントは安全で、ライフサイクル全体にわたって制御されます。 ドキュメントは、オフラインでダウンロードされた場合、および組織に再び送信された場合、ファイアウォールの外部で安全な状態が維持されます。

>[!NOTE]
>
>PDF署名など、特定の操作が呼び出されたときに呼び出される、Signatureサービスのカスタム署名ハンドラーを作成できます。ドキュメント

**署名フィールド名**

一部のSignatureサービスの操作では、操作を実行する署名フィールドの名前を指定する必要があります。 例えば、PDF署名の場合、ドキュメントする署名フィールドの名前を指定します。 署名フィールドのフルネームがになっているとします `form1[0].Form1[0].SignatureField1[0]`。 の代わりにを指 `SignatureField1[0]` 定できま `form1[0].Form1[0].SignatureField1[0]`す。

競合が原因で、Signatureサービスが誤ったフィールドに署名する（または、署名フィールド名を必要とする別の操作を実行する）ことがあります。 この競合は、同じPDFドキュメント内の複数の場 `SignatureField1[0]` 所に名前が表示された結果発生します。 例えば、という名前の2つのドキュメントフィールドを含み、指定したPDF `form1[0].Form1[0].SignatureField1[0]` 署名 `form1[0].Form1[0].SubForm1[0].SignatureField1[0]` があるとしま `SignatureField1[0]`す。 この場合、Signatureサービスは、検出された最初の署名フィールドに署名し、その際に、ドキュメント内のすべての署名フィールドに対して反復処理を行います。

1つのPDFドキュメント内に複数の署名フィールドがある場合は、署名フィールドのフルネームを指定することをお勧めします。 つまり、の代わりにを指 `form1[0].Form1[0].SignatureField1[0]`定しま `SignatureField1[0]`す。

Signatureサービスを使用して、次のタスクを実行できます。

* PDF追加署名フィールドの削除を行います。 (Adding Signature Fields [](digitally-signing-certifying-documents.md#adding-signature-fields)を参照)。
* PDF署名内の署名フィールドの名前を取得します。ドキュメント (署名フィ [ールド名の取得を参照](digitally-signing-certifying-documents.md#retrieving-signature-field-names))。
* 署名フィールドを変更します。 (Modifying Signature Fields [](digitally-signing-certifying-documents.md#modifying-signature-fields)を参照)。
* PDFドキュメントの電子署名 (See [Digitally Signing PDF Documents](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)
* PDFの認証ドキュメント (See [Certifying PDF Documents](digitally-signing-certifying-documents.md#certifying-pdf-documents).)
* PDF署名を検証します。PDFドキュメント (電子署名 [の検証を参照](digitally-signing-certifying-documents.md#verifying-digital-signatures))。
* PDF署名内のすべての電子署名を検証します。ドキュメント (See [Verifying Multiple Digital Signatures](digitally-signing-certifying-documents.md#verifying-digital-signatures).)
* 署名フィールドから電子署名を削除します。 (電子署名 [の削除を参照](digitally-signing-certifying-documents.md#removing-digital-signatures))。

>[!NOTE]
>
> For more information about the Signature service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)..

## 署名フィールドの追加 {#adding-signature-fields}

電子署名は、署名のグラフィック表現を含むフォームフィールドである署名フィールドに表示されます。 署名フィールドは、表示または非表示に設定することができます。署名者は、既存の署名フィールドを使用するか、プログラムによって署名フィールドを追加することができます。 どちらの場合においても、PDF ドキュメントに署名できるようにするには、署名フィールドが存在している必要があります。

プログラムによって署名フィールドを追加するには、Signature サービス Java API や 署名 Web サービス API を使用します。1つのPDF署名に複数の署名フィールドを追加できます。ドキュメントただし、各署名フィールド名は一意である必要があります。

>[!NOTE]
>
>一部のPDFドキュメントタイプでは、プログラムによって署名フィールドを追加できません。 Signatureサービスと署名フィールドの追加について詳しくは、『AEM Formsサービスリフ [ァレンス』を参照してください](https://www.adobe.com/go/learn_aemforms_services_63)。

### 手順の概要 {#summary-of-steps}

署名フィールドをPDFドキュメントに追加するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. 署名クライアントの作成を参照してください。
1. 署名フィールドを追加するPDFドキュメントを取得します。
1. 追加署名フィールド。
1. PDFファイルとしてPDFドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar（AEM FormsがJBossにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsがJBossにデプロイされている場合に必要）

**署名クライアントの作成**

プログラムによってSignatureサービスの操作を実行する前に、Signatureサービスクライアントを作成する必要があります。

**署名フィールドを追加するPDFドキュメントの取得**

署名フィールドを追加するPDFドキュメントを取得する必要があります。

**追加署名欄**

署名フィールドをPDFドキュメントに正しく追加するには、署名フィールドの場所を示す座標値を指定します。 （非表示の署名フィールドを追加する場合、これらの値は不要です）。また、署名フィールドに署名が適用された後にロックするPDFドキュメント内のフィールドを指定することもできます。

**PDFファイルとしてPDFドキュメントを保存します**

SignatureサービスがPDFドキュメントにドキュメントフィールドを追加したら、署名をPDFファイルとして保存し、ユーザーがAcrobatまたはAdobe Readerで開くことができるようにします。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDFへの電子署名のドキュメント](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### Java APIを追加使用した署名フィールド {#add-signature-fields-using-the-java-api}

署追加名API(Java)を使用した署名フィールド：

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-signatures-client.jarなどのクライアントJARファイルを含めます。

1. 署名クライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `SignatureServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 署名フィールドを追加するPDFドキュメントの取得

   * 署名フィ `java.io.FileInputStream` ールドの追加先のPDFドキュメントを表すオブジェクトを作成します。この場合は、コンストラクターを使用し、PDFドキュメントの場所を指定するstring値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 追加署名欄

   * コンストラク `PositionRectangle` ターを使用して、署名フィールドの場所を指定するオブジェクトを作成します。 コンストラクター内で、座標値を指定します。
   * 必要に応じて、電子署名が署 `FieldMDPOptions` 名フィールドに適用されたときにロックされるフィールドを指定するオブジェクトを作成します。
   * オ追加ブジェクトのメソッドを呼び出し、次の値を渡すことにより、PDFドキュメントに署名フ `SignatureServiceClient``addSignatureField` ィールドを割り当てます。

      * A `com.adobe.idp`. `Document` 署名フィールドを追加するPDFドキュメントを表すオブジェクトです。
      * 署名フィールドの名前を指定するstring値です。
      * 署名 `java.lang.Integer` フィールドを追加するページ番号を表す値です。
      * 署名フ `PositionRectangle` ィールドの場所を指定するオブジェクトです。
      * 電子署 `FieldMDPOptions` 名が署名フィールドに適用された後にロックされるPDFドキュメント内のフィールドを指定するオブジェクトです。 このパラメータ値はオプションで、渡すことができま `null`す。
   * 様々な `PDFSeedValueOptions` 実行時値を指定するオブジェクトです。 このパラメータ値はオプションで、渡すことができま `null`す。

      メソッド `addSignatureField` は、aを返しま `com.adobe.idp`す。 `Document` 署名フィールドを含むPDFドキュメントを表すオブジェクトです。
   >[!NOTE]
   >
   >オブジェクトのメソッドを呼 `SignatureServiceClient` び出して、非 `addInvisibleSignatureField` 表示の署名フィールドを追加できます。

1. PDFファイルとしてPDFドキュメントを保存します

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が .pdf であることを確認します。
   * を起動しま `com.adobe.idp`す。 `Document` オブジェクトの `copyToFile` 内容をファイルにコピーす `Document` る方法です。 を必ず使用してくださ `com.adobe.idp`い。 `Document` メソッドによって返されたオブジェク `addSignatureField` トです。

**関連トピック**

[SignatureサービスAPIのクイック開始](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

### Webサ追加ービスAPIを使用した署名フィールド {#add-signature-fields-using-the-web-service-api}

Signature API（Webサービス）を使用して署名フィールドを追加するには：

1. プロジェクトファイルを含める

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. 署名クライアントの作成

   * Create a `SignatureServiceClient` object by using its default constructor.
   * Create a `SignatureServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLを指定するstring値をAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/SignatureService?WSDL`)に渡します。 属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます)。
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得して、オブジェクトを作成 `SignatureServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のオプションを実行して、基本的なHTTP認証を有効にします。タスク

      * AEM formsのユーザー名をフィールドに割り当てま `SignatureServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `SignatureServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールドに `HttpClientCredentialType.Basic` 割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールドに `BasicHttpSecurityMode.TransportCredentialOnly` 割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. 署名フィールドを追加するPDFドキュメントの取得

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、署名フィールドを含むPDFドキュメントを保存するために使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、PDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトの内容を格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得す `System.IO.FileStream` ることで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイ `System.IO.FileStream` ト配列、開始位 `Read` 置およびストリームの長さを渡すことで、バイト配列にストリームデータを入力します。
   * オブジェクト `BLOB` にバイト配列の内容を割り `MTOM` 当てて、オブジェクトを設定します。

1. 追加署名欄

   オ追加ブジェクトのメソッドを呼び出し、次の値を渡すことにより、PDFドキュメントに署 `SignatureServiceClient``addSignatureField` 名フィールドを割り当てます。

   * A `BLOB` object that represents the PDF document to which a signature field is added.
   * 署名フィールド名を指定するstring値です。
   * 署名フィールドを追加するページ番号を表すinteger値です。
   * 署名フ `PositionRect` ィールドの場所を指定するオブジェクトです。
   * 電子署 `FieldMDPOptions` 名が署名フィールドに適用された後にロックされるPDFドキュメント内のフィールドを指定するオブジェクトです。 このパラメータ値はオプションで、渡すことができま `null`す。
   * 様々な `PDFSeedValueOptions` 実行時値を指定するオブジェクトです。 このパラメータ値はオプションで、渡すことができま `null`す。
   署名フ `addSignatureField` ィールドを含 `BLOB` むPDFドキュメントを表すオブジェクトを返します。

1. PDFファイルとしてPDFドキュメントを保存します

   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、署名フィールドとファイルを開くモードを含むPDFドキュメントのファイルの場所を表すstring値を渡します。
   * メソッドによって返されたオブジェクトの内容を `BLOB` 格納するバイト配列を作成し `addSignatureField` ます。 オブジェクトのデータメンバーの値を取得して、バ `BLOB` イト配列を設 `binaryData` 定します。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡すことによって、バ `System.IO.BinaryWriter` イト配列の内 `Write` 容をPDFファイルに書き込みます。

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
1. 署名クライアントの作成を参照してください。
1. 署名フィールドを含むPDFドキュメントを取得します。
1. 署名フィールド名を取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar（AEM FormsがJBossにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsがJBossにデプロイされている場合に必要）

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**署名クライアントの作成**

プログラムによってSignatureサービスの操作を実行する前に、Signatureサービスクライアントを作成する必要があります。

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

   * オブジェクトのメソッドを呼び出し、署名フィー `SignatureServiceClient` ルドを含むPDF `getSignatureFieldList` ドキュメントを含むオ `com.adobe.idp.Document` ブジェクトを渡して、署名フィールド名を取得します。 このメソッドは、各要素に `java.util.List` 1つのオブジェクトが含まれているオブジェクトを返 `PDFSignatureField` します。 このオブジェクトを使用すると、署名フィールドが表示されるかどうかなど、署名フィールドに関する追加情報を取得できます。
   * オブジェクトを繰り返 `java.util.List` し処理し、署名フィールド名があるかどうかを確認します。 PDF署名フィールドごとに、別のドキュメントを取得でき `PDFSignatureField` ます。 署名フィールドの名前を取得するには、オブジェクトの `PDFSignatureField` メソッドを呼び出 `getName` します。 このメソッドは、署名フィールド名を指定するstring値を返します。

**関連トピック**

[署名フィールド名の取得](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[クイック開始（SOAPモード）:Java APIを使用した署名フィールド名の取得](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-retrieving-signature-field-names-using-the-java-api)

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
   * Create a `SignatureServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLを指定するstring値をAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/SignatureService?WSDL`)に渡します。 属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます)。
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得して、オブジェクトを作成 `SignatureServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のオプションを実行して、基本的なHTTP認証を有効にします。タスク

      * AEM formsのユーザー名をフィールドに割り当てま `SignatureServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `SignatureServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールドに `HttpClientCredentialType.Basic` 割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールドに `BasicHttpSecurityMode.TransportCredentialOnly` 割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. 署名フィールドを含むPDFドキュメントの取得

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオブジ `BLOB` ェクトは、署名フィールドを含むPDFドキュメントを保存するために使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、PDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトの内容を格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得す `System.IO.FileStream` ることで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイ `System.IO.FileStream` ト配列、開始位 `Read` 置およびストリームの長さを渡すことで、バイト配列にストリームデータを入力します。
   * オブジェクトにバ `BLOB` イト配列の内容をフィールド `MTOM` に割り当てて、オブジェクトを入力します。

1. 署名フィールド名の取得

   * オブジェクトのメソッドを呼び出し、署名フ `SignatureServiceClient` ィールドを含むPDF `getSignatureFieldList` ドキュメントを含むオ `BLOB` ブジェクトを渡すことで、署名フィールド名を取得します。 このメソッドは、各要素に1つ `MyArrayOfPDFSignatureField` のオブジェクトが含まれるコレクションオブジェクトを返 `PDFSignatureField` します。
   * オブジェクトを繰り返し `MyArrayOfPDFSignatureField` 処理し、署名フィールド名があるかどうかを判断します。 PDF署名内の各署名フィールドに対して、ドキュメントを取得でき `PDFSignatureField` ます。 署名フィールドの名前を取得するには、オブジェクトの `PDFSignatureField` メソッドを呼び出 `getName` します。 このメソッドは、署名フィールド名を指定するstring値を返します。

**関連トピック**

[署名フィールド名の取得](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Modifying Signature Fields {#modifying-signature-fields}

Java APIとWebサービスAPIを使用して、PDFドキュメント内の署名フィールドを変更できます。 署名フィールドの署名フィールドロックディクショナリまたはシード値ディクショナリの値を操作することで署名フィールドを変更します。

A *field lock dictionary* specifies a list of fields that are locked when the signature field is signed. フィールドがロックされると、ユーザーはフィールドを変更できません。A *seed value dictionary* contains constraining information that is used at the time the signature is applied. 例えば、署名を無効にすることなく実行できるアクションを制御する権限設定を変更することができます。

既存の署名フィールドを変更すると、ビジネス要件の変化を反映してPDFドキュメントを変更できます。 例えば、新しいビジネス要件では、ビジネスへの署名後にすべてのドキュメントフィールドをロックする必要がある場合があります。

この節では、フィールドロックディクショナリとシード値ディクショナリの両方の値を変更して、署名フィールドを変更する方法について説明します。 署名フィールドロックディクショナリに変更を加えると、署名フィールドへの署名時に、PDFドキュメント内のすべてのフィールドがロックされます。 シード値ディクショナリに対して行われた変更により、特定の種類の変更がドキュメントに対して禁止されます。

>[!NOTE]
>
>Signatureサービスと署名フィールドの変更について詳しくは、『AEM Formsサービスリフ [ァレンス』を参照してください](https://www.adobe.com/go/learn_aemforms_services_63)。

### 手順の概要 {#summary_of_steps-2}

PDF署名内の署名フィールドを変更するには、次のドキュメントを実行します。

1. プロジェクトファイルを含めます。
1. 署名クライアントの作成を参照してください。
1. 変更する署名フィールドを含むPDFドキュメントを取得します。
1. 辞書の値を設定します。
1. 署名フィールドを変更します。
1. PDFファイルとしてPDFドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar（AEM FormsがJBossにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsがJBossにデプロイされている場合に必要）

For information about the location of these JAR files, see [Including LiveCycle Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**署名クライアントの作成**

プログラムによってSignatureサービスの操作を実行する前に、Signatureサービスクライアントを作成する必要があります。

**変更する署名フィールドを含むPDFドキュメントを取得します**

変更する署名フィールドを含むPDFドキュメントを取得します。

**辞書の値の設定**

署名フィールドを変更するには、フィールドロックディクショナリまたはシード値ディクショナリに値を割り当てます。 署名フィールドロックディクショナリ値の指定には、署名フィールドのドキュメント時にロックされるPDF署名フィールドの指定が含まれます。 （この節では、すべてのフィールドをロックする方法を説明します）。

次のシード値ディクショナリ値を設定できます。

* **リビジョンの確認**:署名が署名フィールドに適用された場合に失効確認を実行するかどうかを指定します。
* **証明書のオプション**:証明書のシード値ディクショナリに値を割り当てます。 証明書のオプションを指定する前に、証明書のシード値ディクショナリについて理解することをお勧めします。 (『 [PDF Reference](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf)』を参照)。
* **Digest options**:署名に使用するダイジェストアルゴリズムを割り当てます。 有効な値は、SHA1、SHA256、SHA384、SHA512およびRIPEMD160です。
* **フィルタ**:署名フィールドで使用するフィルターを指定します。 例えば、Adobe.PPKLiteフィルターを使用できます。 (『 [PDF Reference](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf)』を参照)。
* **フラグのオプション**:この署名フィールドに関連付けられているフラグ値を指定します。 値が1の場合、署名者は指定した値のみをエントリに使用する必要があります。 値が0の場合、他の値も許可されます。 以下に、ビット位置を示します。

   * **1（フィルタ）:** 署名フィールドへの署名に使用する署名ハンドラーです
   * **2(SubFilter):** 署名時に使用する有効なエンコーディングを示す名前の配列です
   * **3 (V)**: The minimum required version number of the signature handler to be used to sign the signature field
   * **4（理由）:** 署名に必要な理由を指定する文字列の配列ですドキュメント
   * **5(PDFLegalWarnings):** 法的証明を指定する文字列の配列

* **Legal attestations**:ドキュメントが認証されると、ドキュメントの表示内容をあいまいにしたり誤解を招く可能性のある、特定のタイプのコンテンツが自動的にスキャンされます。 例えば、注釈では、認証対象を理解する上で重要なテキストを隠すことができます。 スキャン処理では、この種類のコンテンツの存在を示す警告が生成されます。 また、警告が生成された可能性のあるコンテンツに関する追加の説明も提供されます。
* **権限**:署名を無効にせずにPDF署名で使用できるドキュメントを指定します。
* **理由**:この署名が必要な理由をドキュメントに指定します。
* **タイムスタンプ**:タイムスタンプオプションを指定します。 例えば、使用するタイムスタンプサーバーのURLを設定できます。
* **バージョン**:署名フィールドへの署名に使用する署名ハンドラーの最小バージョン番号を指定します。

**署名フィールドの変更**

Signatureサービスクライアントを作成し、変更する署名フィールドを含むPDFドキュメントを取得し、ディクショナリ値を設定した後、Signatureサービスに対して署名フィールドを変更するように指示できます。 次に、Signatureサービスは、変更された署名フィールドを含むPDFドキュメントを返します。 元のPDFドキュメントは影響を受けません。

**PDFファイルとしてPDFドキュメントを保存します**

変更した署名フィールドを含むPDFドキュメントをPDFファイルとして保存し、ユーザーがAcrobatまたはAdobe Readerで開けるようにします。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Signature Service API Quick Starts](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

[PDFへの電子署名のドキュメント](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

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
   * オブジェクトのメソッドを呼び出し、 `PDFSeedValueOptionSpec` ドキュメント値を渡すことで、PDF `setMdpValue` 定義済みリストの変更を許可し `MDPPermissions.NoChanges` ません。
   * コンストラクタを使用して `FieldMDPOptionSpec` オブジェクトを作成します。このオブジェクトを使用すると、署名フィールドロックディクショナリの値を設定できます。
   * オブジェクトのメソッドを呼び出し、 `FieldMDPOptionSpec` 定義済みリスト値を渡すことで、PDFドキュメント内の `setMdpValue` すべてのフィールドをロ `FieldMDPAction.ALL` ックします。
   * オブジェクトのメソッドを呼び出し、オブジ `PDFSignatureFieldProperties` ェクトを渡すこ `setSeedValue` とで、シード値ディクショナリ情報を設 `PDFSeedValueOptionSpec` 定します。
   * 署名フィールドのロックディクショナリ情報を設定するには、オ `PDFSignatureFieldProperties`ブジェクトのメソッド `setFieldMDP` を呼び出し、オブジェクトを渡 `FieldMDPOptionSpec` します。
   >[!NOTE]
   >
   >設定可能なすべてのシード値ディクショナリ値を確認するには、クラス参照を参 `PDFSeedValueOptionSpec` 照してください。 (『 [AEM Forms APIリファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)』を参照)。

1. 署名フィールドの変更

   オブジェクトのメソッドを呼び出し、次 `SignatureServiceClient` の値を渡し `modifySignatureField` て、署名フィールドを変更します。

   * 変更する `com.adobe.idp.Document` 署名フィールドを含むPDFドキュメントを格納するオブジェクトです
   * 署名フィールドの名前を指定するstring値です
   * 署名フィ `PDFSignatureFieldProperties` ールドロックディクショナリとシード値ディクショナリ情報を格納するオブジェクトです
   このメソ `modifySignatureField` ッドは、変更さ `com.adobe.idp.Document` れた署名フィールドを含むPDFドキュメントを格納するオブジェクトを返します。

1. PDFファイルとしてPDFドキュメントを保存します

   * Create a `java.io.File` object and ensure that the file name extension is .pdf.
   * Invoke the `com.adobe.idp.Document` object’s `copyToFile` method to copy the contents of the `com.adobe.idp.Document` object to the file. メソッドが返すオブジェクト `com.adobe.idp.Document` を使用しているこ `modifySignatureField` とを確認します。

### WebサービスAPIを使用した署名フィールドの変更 {#modify-signature-fields-using-the-web-service-api}

Signature API（Webサービス）を使用して署名フィールドを変更します。

1. プロジェクトファイルを含める

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. 署名クライアントの作成

   * Create a `SignatureServiceClient` object by using its default constructor.
   * Create a `SignatureServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLを指定するstring値をAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/SignatureService?WSDL`)に渡します。 属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます)。
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得して、オブジェクトを作成 `SignatureServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のオプションを実行して、基本的なHTTP認証を有効にします。タスク

      * AEM formsのユーザー名をフィールドに割り当てま `SignatureServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `SignatureServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールドに `HttpClientCredentialType.Basic` 割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールドに `BasicHttpSecurityMode.TransportCredentialOnly` 割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. 変更する署名フィールドを含むPDFドキュメントを取得します

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、変更する署名フィールドを含むPDFドキュメントの保存に使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、PDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトの内容を格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得す `System.IO.FileStream` ることで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイ `System.IO.FileStream` ト配列、開始位 `Read` 置およびストリームの長さを渡すことで、バイト配列にストリームデータを入力します。
   * オブジェクトの `BLOB` プロパティにバイト配列の `MTOM` 内容を割り当てて、オブジェクトを設定します。

1. 辞書の値の設定

   * コンストラクタを使用して `PDFSignatureFieldProperties` オブジェクトを作成します。このオブジェクトは、署名フィールドロックディクショナリとシード値ディクショナリの情報を格納します。
   * コンストラクタを使用して `PDFSeedValueOptionSpec` オブジェクトを作成します。このオブジェクトを使用すると、シード値ディクショナリの値を設定できます。
   * オブジェクトのデータドキュメントに `MDPPermissions.NoChanges` 定義済みリスト値を割り当てることで、PDF `PDFSeedValueOptionSpec` メンバーの変 `mdpValue` 更を許可しない。
   * コンストラクタを使用して `FieldMDPOptionSpec` オブジェクトを作成します。このオブジェクトを使用すると、署名フィールドロックディクショナリの値を設定できます。
   * オブジェクトのデータドキュメントに `FieldMDPAction.ALL` 定義済みリスト値を割り当てて、PDFメンバー内のす `FieldMDPOptionSpec` べてのフィー `mdpValue` ルドをロックします。
   * オブジェクトのデータメンバーにオブジェクトを割 `PDFSeedValueOptionSpec` り当てて、シ `PDFSignatureFieldProperties` ード値ディクショナリ `seedValue` 情報を設定します。
   * 署名フィールドのロックディクショナリ情報を設定するには、オ `FieldMDPOptionSpec` ブジェクトをオブジ `PDFSignatureFieldProperties` ェクトのデータメン `fieldMDP` バーに割り当てます。
   >[!NOTE]
   >
   >設定可能なすべてのシード値ディクショナリ値を確認するには、クラス参照を参 `PDFSeedValueOptionSpec` 照してください。 (『 [AEM Forms APIリファレンス』を参照](https://www.adobe.com/go/learn_aemforms_javadocs_63_en))。

1. 署名フィールドの変更

   オブジェクトのメソッドを呼び出し、次 `SignatureServiceClient` の値を渡し `modifySignatureField` て、署名フィールドを変更します。

   * 変更する `BLOB` 署名フィールドを含むPDFドキュメントを格納するオブジェクトです
   * 署名フィールドの名前を指定するstring値です
   * 署名フィ `PDFSignatureFieldProperties` ールドロックディクショナリとシード値ディクショナリ情報を格納するオブジェクトです
   このメソ `modifySignatureField` ッドは、変更さ `BLOB` れた署名フィールドを含むPDFドキュメントを格納するオブジェクトを返します。

1. PDFファイルとしてPDFドキュメントを保存します

   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、署名フィールドを含むPDFドキュメントのファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * メソッドが返すオブジェクトの内容を格納する `BLOB` バイト配列を作 `addSignatureField` 成します。 オブジェクトのデータメンバーの値を取得して、バ `BLOB` イト配列を設 `MTOM` 定します。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡すことによって、バ `System.IO.BinaryWriter` イト配列の内 `Write` 容をPDFファイルに書き込みます。

**関連トピック**

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Digitally Signing PDF Documents {#digitally-signing-pdf-documents}

セキュリティレベルの提供のため、PDF に電子署名を適用することができます。手書き署名のような電子署名は、署名者を識別したり、ドキュメントに関するステートメントを作成する手段として使用できます。ドキュメントの電子署名に使用されている技術は、署名者と受信者の両方が、何に署名されているのかを明確にし、その署名によりドキュメントに変更がないことを確認するのに役立ちます。

PDF ドキュメントは、公開鍵を用いて署名されます。署名者は公開鍵と秘密鍵の 2 つの鍵を持っています。秘密鍵は、署名時に使用可能にする必要があるユーザーの秘密鍵証明書に保存されます。 公開鍵はユーザーの証明書に保存され、署名を検証するには受信者が使用できる必要があります。 失効した証明書に関する情報は、認証機関から配布される証明書失効リスト（CRL）およびオンライン証明書ステータスプロトコル（OCSP）応答内にあります。署名が行われた時間は、タイムスタンプ局として知られる信頼できるソースから取得されます。

>[!NOTE]
>
>PDF署名をデジタル署名する前に、ドキュメントをAEM Formsに追加しておく必要があります。 証明書は、管理コンソールを使用して、またはTrust Manager APIを使用してプログラムによって追加されます。 (Trust Manager APIを [使用した秘密鍵証明書の読み込みを参照](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api))。

PDF署名は、プログラムによってデジタル署名することができます。ドキュメント PDF署名を電子署名する場合、AEM Formsに存在するドキュメント証明書を参照する必要があります。 証明書は署名に使用する秘密鍵となります。

PDF署名が行われると、Signatureサービスは次の手順をドキュメントします。

1. Signatureサービスは、要求で指定されたエイリアスを渡すことで、Truststoreから秘密鍵証明書を取得します。
1. Truststoreは、指定された秘密鍵証明書を検索します。
1. 秘密鍵証明書はSignatureサービスに返され、署名に使用されます。ドキュメント また、証明書は、今後の要求のためにエイリアスに対してキャッシュされます。

セキュリティ証明書の取り扱いに関する詳細は、ご使用のアプリケ *ーションサーバー版の『AEM Formsのインストール* およびデプロイ』ガイドを参照してください。

>[!NOTE]
>
>署名と認証のドキュメントには、 (See [Certifying PDF Documents](digitally-signing-certifying-documents.md#certifying-pdf-documents).)

>[!NOTE]
>
>署名をサポートしていないPDFドキュメントもあります。 Signatureサービスと電子署名ドキュメントについて詳しくは、『AEM Formsサービスリフ [ァレンス』を参照してください](https://www.adobe.com/go/learn_aemforms_services_63)。

>[!NOTE]
>
>Signatureサービスは、操作の入力として埋め込まれたPDFデータ（認証など）を持つXDPファイルをサポートしません。ドキュメント この操作を行うと、SignatureサービスでSignatureがスローされま `PDFOperationException`す。 この問題を解決するには、PDF Utilitiesサービスを使用してXDPファイルをPDFファイルに変換し、変換したPDFファイルをSignatureサービス操作に渡します。 (PDF Utilities [の操作を参照](/help/forms/developing/pdf-utilities.md#working-with-pdf-utilities))。

**nCipher nShield HSM秘密鍵証明書**

PDFドキュメントの署名や認証にnCipher nShield HSM秘密鍵証明書を使用する場合、AEM Formsのデプロイ先のJ2EEアプリケーションサーバーが再起動されるまで、新しい秘密鍵証明書は使用できません。 ただし、設定値を設定すると、J2EEアプリケーションサーバーを再起動しなくても、署名または認証の操作が機能します。

次の設定値をcknfastrcファイルに追加できます。このファイルは/opt/nfast/cknfastrc(またはc:\nfast\cknfastrc)にあります。

```as3
 CKNFAST_ASSUME_SINGLE_PROCESS=0
```

この設定値をcknfastrcファイルに追加すると、J2EEアプリケーションサーバーを再起動しなくても、新しい秘密鍵証明書を使用できます。

**署名が信頼されていません**

同じPDFドキュメントの認証と署名を行う場合、認証用署名が信頼されていないと、AcrobatまたはAdobe ReaderでPDFドキュメントを開くときに、最初の署名に対して黄色い三角印が表示されます。 この状況を回避するには、認証署名を信頼する必要があります。

**XFAベースのドキュメントである署名フォーム**

SignatureサービスAPIを使用してXFAベースのフォームに署名しようとすると、Acrobatにあるデータが見つからない `View``Signed``Version` 可能性があります。 例えば、次のワークフローを考えてみましょう。

* Designerを使用して作成したXDPファイルを使用して、署名フィールドを含むフォームデザインと、フォームデータを含むXMLデータを結合します。 Formsサービスを使用して、インタラクティブPDFドキュメントを生成します。
* PDFドキュメントに署名するには、SignatureサービスAPIを使用します。

### 手順の概要 {#summary_of_steps-3}

PDF署名をデジタル署名するには、ドキュメントを次のタスクします。

1. プロジェクトファイルを含めます。
1. Signatureサービスクライアントを作成します。
1. 署名するPDFドキュメントを取得します。
1. 「PDFへの署名」ドキュメント
1. 署名済みPDFドキュメントをPDFファイルとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar（AEM FormsがJBossにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsがJBossにデプロイされている場合に必要）

**Signaturesクライアントの作成**

プログラムによってSignatureサービスの操作を実行する前に、Signatureサービスクライアントを作成する必要があります。

**署名するPDFドキュメントの取得**

PDF署名を行うには、ドキュメントフィールドを含むPDFドキュメントを取得する必要があります。 PDFドキュメントに署名フィールドが含まれていない場合は、署名できません。 署名フィールドは、Designerを使用して追加することも、プログラムを使用して追加することもできます。

**「Sign the PDF」ドキュメント**

PDF署名時に、Signatureドキュメントサービスで使用する実行時オプションを設定できます。 次のオプションを設定できます。

* 外観オプション
* 失効確認
* タイムスタンプ値

外観オプションは、オブジェクトを使用して設定 `PDFSignatureAppearanceOptionSpec` します。 例えば、オブジェクトのメソッドを呼び出して渡すことで、署名内に日 `PDFSignatureAppearanceOptionSpec` 付を表示するこ `setShowDate` とができま `true`す。

また、PDFドキュメントのデジタル署名に使用される証明書が失効したかどうかを判定する失効確認を実行するかどうかを指定することもできます。 失効確認を実行するには、次のいずれかの値を指定します。

* **NoCheck**:失効確認を実行しません。
* **BestEffort**:常に、チェーン内のすべての証明書の失効の確認を試みます。 確認で問題が発生した場合、失効は有効であると見なされます。 エラーが発生した場合は、証明書が失効していないと仮定します。
* **CheckIfAvailable:** 失効情報が利用可能な場合、チェーン内のすべての証明書の失効を確認します。 チェックで問題が発生した場合、失効は無効であると見なされます。 エラーが発生した場合は、証明書が失効し、無効であると仮定します。 （これがデフォルト値です）。
* **AlwaysCheck**:チェーン内のすべての証明書の失効を確認します。 失効情報が証明書に存在しない場合、失効は無効であると見なされます。

証明書に対して失効確認を実行するには、オブジェクトを使用して、証明書失効リスト(CRL)サーバーへのURLを指定で `CRLOptionSpec` きます。 ただし、失効確認を実行し、CRLサーバーへのURLを指定しない場合は、Signatureサービスは証明書からURLを取得します。

失効確認を実行する際は、CRLサーバーを使用する代わりに、オンライン証明書ステータスプロトコル(OCSP)サーバーを使用できます。 通常、CRLサーバーとは異なり、OCSPサーバーを使用する場合、失効確認の実行が高速になります。 (https://tools.ietf.org/html/rfc2560の「Online Certificate Status Protocol」を参 [照](https://tools.ietf.org/html/rfc2560))。

Signatureサービスで使用するCRLおよびOCSPサーバーの順序は、Adobe Applications and Servicesを使用して設定できます。 例えば、OCSPサーバーがAdobe Applications and Servicesで最初に設定されている場合は、OCSPサーバーがチェックされ、次にCRLサーバーがチェックされます。 （AACヘルプの「Trust Storeを使用した証明書と秘密鍵証明書の管理」を参照）。

失効確認を実行しないように指定した場合、Signatureサービスは、ドキュメントの署名または認証に使用された証明書が失効したかどうかを確認しません。 つまり、CRLおよびOCSPサーバー情報は無視されます。

>[!NOTE]
>
>CRLまたはOCSPサーバーは証明書で指定できますが、とオブジェクトを使用して、証明書で指定されたURLを上書きする `CRLOptionSpec` ことができ `OCSPOptionSpec` ます。 例えば、CRLサーバーを上書きするには、オブジェクトのメ `CRLOptionSpec` ソッドを呼び出し `setLocalURI` ます。

タイムスタンプとは、署名済みまたは認証済みのドキュメントが変更された時刻を追跡する処理です。 ドキュメントの署名後は、署名の所有者でも変更しないでください。 タイムスタンプを使用すると、署名済みまたは認証済みのドキュメントの有効性を強制できます。 オブジェクトを使用して、タイムスタンプオプションを設定 `TSPOptionSpec` できます。 例えば、タイムスタンププロバイダー(TSP)サーバーのURLを指定できます。

>[!NOTE]
>
>JavaおよびWebサービスの各セクションと対応するクイック開始では、失効確認が使用されます。 CRLまたはOCSPサーバー情報が指定されていないので、サーバー情報は、PDFサーバーのデジタル署名に使用された証明書から取得されます。ドキュメント

PDFドキュメントに正しく署名するには、電子署名を含む署名フィールドの完全修飾名（など）を指定します `form1[0].#subform[1].SignatureField3[3]`。 XFAフォームフィールドを使用する場合、署名フィールドの名前の一部を使用することもできます。 `SignatureField3[3]`.

また、PDF署名をデジタル署名するには、セキュリティ証明書を参照する必要がありますドキュメント。 セキュリティ証明書を参照するには、エイリアスを指定します。 エイリアスは、PKCS#12ファイル（.pfx拡張子付き）またはハードウェアセキュリティモジュール(HSM)内に存在する可能性のある、実際の秘密鍵証明書への参照です。 セキュリティ証明書について詳しくは、使用しているアプリケ *ーションサーバー版の『AEM Formsのインストール* およびデプロイ』ガイドを参照してください。

**署名済みPDFの保存ドキュメント**

SignatureサービスでPDFドキュメントに電子署名した後、PDFファイルとして保存し、ユーザーがAcrobatまたはAdobe Readerで開くことができるようにすることができます。

**関連トピック**

[Java APIを使用したPDFドキュメントへの電子署名](digitally-signing-certifying-documents.md#digitally-sign-pdf-documents-using-the-java-api)

[WebサービスAPIを使用したPDFドキュメントへのデジタル署名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[署名フィールドの追加](digitally-signing-certifying-documents.md#adding-signature-fields)

[署名フィールド名の取得](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

### Java APIを使用したPDFドキュメントへの電子署名 {#digitally-sign-pdf-documents-using-the-java-api}

署名API(Java)を使用してPDFドキュメントに電子署名する：

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-signatures-client.jarなどのクライアントJARファイルを含めます。

1. Signaturesクライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `SignatureServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 署名するPDFドキュメントの取得

   * コンストラ `java.io.FileInputStream` クターを使用し、PDFドキュメントの場所を指定する文字列値を渡して、デジタル署名するPDFドキュメントを表すオブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 「Sign the PDF」ドキュメント

   オブジェクトのドキュメントを呼び出し、 `SignatureServiceClient` 次の値を渡 `sign` して、PDFメソッドに署名します。

   * A `com.adobe.idp.Document` object that represents the PDF document to sign.
   * 電子署名を含む署名フィールドの名前を表すstring値です。
   * A `Credential` object that represents the credential that is used to digitally sign the PDF document. オブジェクト `Credential` の静的メソッドを呼 `Credential` び出し、セキュリテ `getInstance` ィ秘密鍵証明書に対応するエイリアス値を指定するstring値を渡して、オブジェクトを作成します。
   * PDFアルゴリズム `HashAlgorithm` のダイジェストの作成に使用するハッシュアルゴリズムを表す静的データメンバーを指定するオブジェクトです。ドキュメント。 例えば、SHA1アルゴリズムを使 `HashAlgorithm.SHA1` 用するように指定できます。
   * PDF署名が電子署名された理由を表すstringドキュメント値です。
   * 署名者の連絡先情報を表すstring値です。
   * 電子署 `PDFSignatureAppearanceOptions` 名の外観を制御するオブジェクトです。 例えば、このオブジェクトを使用して、電子署名にカスタムロゴを追加できます。
   * 署名者 `java.lang.Boolean` の証明書に対して失効確認を実行するかどうかを指定するオブジェクトです。
   * オンラ `OCSPOptionSpec` イン証明書ステータスプロトコル(OCSP)サポートの環境設定を格納するオブジェクトです。 失効確認が行われない場合、このパラメーターは使用されず、指定できま `null`す。
   * 証明書失 `CRLPreferences` 効リスト(CRL)の環境設定を格納するオブジェクトです。 失効確認が行われない場合、このパラメーターは使用されず、指定できま `null`す。
   * タイムス `TSPPreferences` タンププロバイダー(TSP)サポートの環境設定を格納するオブジェクトです。 このパラメーターはオプションで、を指定できま `null`す。 For more information, see [AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   このメソ `sign` ッドは、署名済みPDF `com.adobe.idp.Document` メッセージを表すオブジェクトを返しますドキュメント。

1. 署名済みPDFの保存ドキュメント

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が .pdf であることを確認します。
   * Invoke the `com.adobe.idp.Document` object’s `copyToFile` method and pass `java.io.File`to copy the contents of the `Document` object to the file. `com.adobe.idp.Document` メソッドから返された `sign` オブジェクトを必ず使用してください。

**関連トピック**

[PDFへの電子署名のドキュメント](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[クイック開始（SOAPモード）:Java APIを使用したPDFドキュメントのデジタル署名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

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
   * Create a `SignatureServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLを指定するstring値をAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/SignatureService?WSDL`)に渡します。 属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます)。
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得して、オブジェクトを作成 `SignatureServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のオプションを実行して、基本的なHTTP認証を有効にします。タスク

      * AEM formsのユーザー名をフィールドに割り当てま `SignatureServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `SignatureServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールドに `HttpClientCredentialType.Basic` 割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールドに `BasicHttpSecurityMode.TransportCredentialOnly` 割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. 署名するPDFドキュメントの取得

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、署名されたPDFドキュメントの保存に使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、署名するPDFドキュメントーのファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * オブジェクトの内容を格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得す `System.IO.FileStream` ることで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイ `System.IO.FileStream` ト配列、開始位 `Read` 置およびストリームの長さを渡すことで、バイト配列にストリームデータを入力します。
   * オブジェクトの `BLOB` プロパティにバイト配列の `MTOM` 内容を割り当てて、オブジェクトを設定します。

1. 「Sign the PDF」ドキュメント

   オブジェクトのドキュメントを呼び出し、 `SignatureServiceClient` 次の値を渡 `sign` して、PDFメソッドに署名します。

   * A `BLOB` object that represents the PDF document to sign.
   * 電子署名を含む署名フィールドの名前を表すstring値です。
   * A `Credential` object that represents the credential that is used to digitally sign the PDF document. コンストラクタ `Credential` ーを使用してオブジェクトを作成し、オブジェクトのプロパティに値を割り当ててエイリ `Credential` アスを指定 `alias` します。
   * PDFアルゴリズム `HashAlgorithm` のダイジェストの作成に使用するハッシュアルゴリズムを表す静的データメンバーを指定するオブジェクトです。ドキュメント。 例えば、SHA1アルゴリズムを使 `HashAlgorithm.SHA1` 用するように指定できます。
   * ハッシュアルゴリズムを使用するかどうかを指定するBoolean値です。
   * PDF署名が電子署名された理由を表すstringドキュメント値です。
   * 署名者の場所を表すstring値です。
   * 署名者の連絡先情報を表すstring値です。
   * 電子署 `PDFSignatureAppearanceOptions` 名の外観を制御するオブジェクトです。 例えば、このオブジェクトを使用して、電子署名にカスタムロゴを追加できます。
   * 署名者 `System.Boolean` の証明書に対して失効確認を実行するかどうかを指定するオブジェクトです。 この失効確認が行われると、署名に埋め込まれます。 デフォルトは、`false` です。
   * オンラ `OCSPOptionSpec` イン証明書ステータスプロトコル(OCSP)サポートの環境設定を格納するオブジェクトです。 失効確認が行われない場合、このパラメーターは使用されず、指定できま `null`す。 このオブジェクトに関する詳細は、『 [AEM Forms APIリファレンス』を参照してください](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   * 証明書失 `CRLPreferences` 効リスト(CRL)の環境設定を格納するオブジェクトです。 失効確認が行われない場合、このパラメーターは使用されず、指定できま `null`す。
   * タイムス `TSPPreferences` タンププロバイダー(TSP)サポートの環境設定を格納するオブジェクトです。 このパラメーターはオプションで、を指定できま `null`す。
   このメソ `sign` ッドは、署名済みPDF `BLOB` メッセージを表すオブジェクトを返しますドキュメント。

1. 署名済みPDFの保存ドキュメント

   * Create a `System.IO.FileStream` object by invoking its constructor. 署名済みPDFドキュメントのファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * メソッドによって返されたオブジェクトの内容を `BLOB` 格納するバイト配列を作成し `sign` ます。 オブジェクトのデータメンバーの値を取得して、バ `BLOB` イト配列を設 `MTOM` 定します。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡すことによって、バ `System.IO.BinaryWriter` イト配列の内 `Write` 容をPDFファイルに書き込みます。

**関連トピック**

[PDFへの電子署名のドキュメント](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## インタラクティブフォームへの電子署名 {#digitally-signing-interactive-forms}

Formsサービスで作成されるインタラクティブフォームに署名できます。 例えば、次のワークフローを考えてみましょう。

* Designerを使用して作成されたXFAベースのPDFフォームと、Formsサービスを使用してXMLドキュメント内のフォームデータを結合します。 Formsサーバーはインタラクティブフォームをレンダリングします。
* インタラクティブフォームに署名するには、SignatureサービスAPIを使用します。

この結果、デジタル署名されたインタラクティブPDFフォームが作成されます。 XFAフォームに基づくPDFフォームに署名する場合は、PDFファイルをAdobeスタティックPDFフォームとして保存します。 AdobeダイナミックPDFフォームとして保存されたPDFフォームに署名しようとすると、例外が発生します。 Formsサービスから返されるフォームに署名するので、フォームに署名フィールドが含まれていることを確認します。

>[!NOTE]
>
>インタラクティブフォームに電子署名する前に、証明書をAEM Formsに追加する必要があります。 証明書は、管理コンソールを使用して、またはTrust Manager APIを使用してプログラムによって追加されます。 (Trust Manager APIを [使用した秘密鍵証明書の読み込みを参照](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api))。

Forms Service APIを使用する場合は、実行時のオ `GenerateServerAppearance` プションをに設定しま `true`す。 この実行時オプションを使用すると、サーバー上で生成されたフォームの外観が、AcrobatまたはAdobe Readerで開いたときにも有効なままになります。 Forms APIを使用して署名するインタラクティブフォームを生成する場合は、この実行時オプションを設定することをお勧めします。

>[!NOTE]
>
>インタラクティブフォームへのデジタル署名を読む前に、PDF署名に関する知識があることをお勧めします。ドキュメント (See [Digitally Signing PDF Documents](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents).)

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
* jbossall-client.jar（AEM FormsがJBossにデプロイされている場合に必要）

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Forms &amp; Signaturesクライアントの作成**

このワークフローはFormsとSignatureの両方のサービスを呼び出すので、FormsサービスクライアントとSignatureサービスクライアントの両方を作成します。

**Formsサービスを使用してインタラクティブフォームを取得する**

Formsサービスを使用して、署名するインタラクティブPDFフォームを取得できます。 AEM Formsでは、レンダリングするフォームを `com.adobe.idp.Document` 含むオブジェクトをFormsサービスに渡すことができます。 このメソッドの名前はです `renderPDFForm2`。 このメソッドは、署名する `com.adobe.idp.Document` フォームを含むオブジェクトを返します。 このインスタンスは、Signatureサ `com.adobe.idp.Document` ービスに渡すことができます。

同様に、Webサービスを使用している場合は、Formsサービスが返 `BLOB` すインスタンスをSignatureサービスに渡すことができます。

>[!NOTE]
>
>「インタラクティブフォームに電子署名」セクションに関連付けられたクイック開始が、このメソッドを呼び `renderPDFForm2` 出します。

**インタラクティブフォームへの署名**

PDF署名時に、Signatureドキュメントサービスで使用する実行時オプションを設定できます。 次のオプションを設定できます。

* 外観オプション
* 失効確認
* タイムスタンプ値

外観オプションは、オブジェクトを使用して設定 `PDFSignatureAppearanceOptionSpec` します。 例えば、オブジェクトのメソッドを呼び出して渡すことで、署名内に日 `PDFSignatureAppearanceOptionSpec` 付を表示するこ `setShowDate` とができま `true`す。

**署名済みPDFの保存ドキュメント**

SignatureサービスがPDF署名をデジタル化した後、ドキュメントをPDFファイルとして保存できます。 PDFファイルは、AcrobatまたはAdobe Readerで開くことができます。

**関連トピック**

[Java APIを使用したインタラクティブフォームへの電子署名](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-java-api)

[WebサービスAPIを使用してインタラクティブフォームに電子署名する](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDFへの電子署名のドキュメント](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[インタラクティブPDFフォームのレンダリング](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms)

### Java APIを使用したインタラクティブフォームへの電子署名 {#digitally-sign-an-interactive-form-using-the-java-api}

Forms and Signature API(Java)を使用してインタラクティブフォームに電子署名する：

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-signatures-client.jarやadobe-forms-client.jarなどのクライアントJARファイルを含めます。

1. Forms &amp; Signaturesクライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `SignatureServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `FormsServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. Formsサービスを使用してインタラクティブフォームを取得する

   * コンストラ `java.io.FileInputStream` クターを使用して、Formsサービスに渡すPDFドキュメントを表すオブジェクトを作成します。 PDFフォルダーの場所を指定するstring値を渡します。ドキュメント
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。
   * コンストラク `java.io.FileInputStream` ターを使用して、Formsサービスに渡すフォームデータを含むXMLドキュメントを表すオブジェクトを作成します。 XMLファイルの場所を指定するstring値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。
   * 実行時オプシ `PDFFormRenderSpec` ョンの設定に使用するオブジェクトを作成します。 オブジェクト `PDFFormRenderSpec` のメソッドを呼び `setGenerateServerAppearance` 出し、渡しま `true`す。
   * オブジェクト `FormsServiceClient` のメソッドを `renderPDFForm2` 呼び出し、次の値を渡します。

      * レンダリング `com.adobe.idp.Document` するPDFフォームを含むオブジェクトです。
      * フォーム `com.adobe.idp.Document` とマージするデータを含むオブジェクトです。
      * 実行時 `PDFFormRenderSpec` のオプションを格納するオブジェクト。
      * Formsサ `URLSpec` ービスで必要なURI値を含むオブジェクトです。 このパラメータ `null` ー値を指定できます。
      * 添付ファ `java.util.HashMap` イルを格納するオブジェクト。 これはオプションのパラメーターで、フォームにフ `null` ァイルを添付しないかどうかを指定できます。
      このメソ `renderPDFForm2` ッドは、フォームデ `FormsResult` ータストリームを含むオブジェクトを返します

   * オブジェクトのメソッドを呼び出して、PDF `FormsResult` フォームを取得 `getOutputContent` します。 このメソッドは、インタラクティブ `com.adobe.idp.Document` フォームを表すオブジェクトを返します。


1. インタラクティブフォームへの署名

   オブジェクトのドキュメントを呼び出し、 `SignatureServiceClient` 次の値を渡 `sign` して、PDFメソッドに署名します。

   * A `com.adobe.idp.Document` object that represents the PDF document to sign. このオブジェクトがFormsサービスから取得さ `com.adobe.idp.Document` れたオブジェクトであることを確認します。
   * 署名された署名フィールドの名前を表すstring値です。
   * A `Credential` object that represents the credential that is used to digitally sign the PDF document. オブジェクトの `Credential` 静的メソッドを呼び出し `Credential` て、オブジェクトを作成 `getInstance` します。 セキュリティ証明書に対応するエイリアス値を指定するstring値を渡します。
   * PDFアルゴリズム `HashAlgorithm` のダイジェストの作成に使用するハッシュアルゴリズムを表す静的データメンバーを指定するオブジェクトです。ドキュメント。 例えば、SHA1アルゴリズムを使 `HashAlgorithm.SHA1` 用するように指定できます。
   * PDF署名が電子署名された理由を表すstringドキュメント値です。
   * 署名者の連絡先情報を表すstring値です。
   * 電子署 `PDFSignatureAppearanceOptions` 名の外観を制御するオブジェクトです。 例えば、このオブジェクトを使用して、電子署名にカスタムロゴを追加できます。
   * 署名者 `java.lang.Boolean` の証明書に対して失効確認を実行するかどうかを指定するオブジェクトです。
   * オンラ `OCSPPreferences` イン証明書ステータスプロトコル(OCSP)サポートの環境設定を格納するオブジェクトです。 失効確認が行われない場合、このパラメーターは使用されず、指定できま `null`す。
   * 証明書失 `CRLPreferences` 効リスト(CRL)の環境設定を格納するオブジェクトです。 失効確認が行われない場合、このパラメーターは使用されず、指定できま `null`す。
   * タイムス `TSPPreferences` タンププロバイダー(TSP)サポートの環境設定を格納するオブジェクトです。 このパラメーターはオプションで、を指定できま `null`す。
   このメソ `sign` ッドは、署名済みPDF `com.adobe.idp.Document` メッセージを表すオブジェクトを返しますドキュメント。

1. 署名済みPDFの保存ドキュメント

   * Create a `java.io.File` object and ensure that the filename extension is .pdf.
   * Invoke the `com.adobe.idp.Document` object’s `copyToFile` method and pass `java.io.File`to copy the contents of the `Document` object to the file. メソッドが返すオブジェクト `com.adobe.idp.Document` を使用しているこ `sign` とを確認します。

**関連トピック**

[インタラクティブフォームへの電子署名](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[クイック開始（SOAPモード）:Java APIを使用したPDFドキュメントのデジタル署名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用してインタラクティブフォームに電子署名する {#digitally-sign-an-interactive-form-using-the-web-service-api}

Forms and Signature API（Webサービス）を使用して、インタラクティブフォームに電子署名します。

1. プロジェクトファイルを含める

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 このクライアントアプリケーションは2つのAEM Formsサービスを呼び出すので、2つのサービス参照を作成します。 Signatureサービスに関連付けられたサービス参照に対して、次のWSDL定義を使用します。 `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   Formsサービスに関連付けられたサービス参照に対して、次のWSDL定義を使用します。 `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   このデータ `BLOB` 型は両方のサービス参照に共通なので、使用する場合はデータ型 `BLOB` を完全に修飾してください。 対応するWebサービスクイック開始では、すべてのイ `BLOB` ンスタンスが完全修飾されます。

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. Forms &amp; Signaturesクライアントの作成

   * Create a `SignatureServiceClient` object by using its default constructor.
   * Create a `SignatureServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLを指定するstring値をAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/SignatureService?WSDL`)に渡します。 属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます)。
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得して、オブジェクトを作成 `SignatureServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のオプションを実行して、基本的なHTTP認証を有効にします。タスク

      * AEM formsのユーザー名をフィールドに割り当てま `SignatureServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `SignatureServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールドに `HttpClientCredentialType.Basic` 割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
   * 定数値をフィールドに `BasicHttpSecurityMode.TransportCredentialOnly` 割り当てま `BasicHttpBindingSecurity.Security.Mode`す。
   >[!NOTE]
   >
   >Formsサービスクライアントに対して、この手順を繰り返します。

1. Formsサービスを使用してインタラクティブフォームを取得する

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、署名されたPDFドキュメントの保存に使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、署名するPDFドキュメントーのファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * オブジェクトの内容を格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得す `System.IO.FileStream` ることで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイ `System.IO.FileStream` ト配列、開始位 `Read` 置およびストリームの長さを渡すことで、バイト配列にストリームデータを入力します。
   * オブジェクトの `BLOB` プロパティにバイト配列の `MTOM` 内容を割り当てて、オブジェクトを設定します。
   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオブジ `BLOB` ェクトは、フォームデータの格納に使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、フォームデータを含むXMLファイルのファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * オブジェクトの内容を格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得す `System.IO.FileStream` ることで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイ `System.IO.FileStream` ト配列、開始位 `Read` 置およびストリームの長さを渡すことで、バイト配列にストリームデータを入力します。
   * オブジェクトの `BLOB` プロパティにバイト配列の `MTOM` 内容を割り当てて、オブジェクトを設定します。
   * 実行時オプシ `PDFFormRenderSpec` ョンの設定に使用するオブジェクトを作成します。 オブジェクトのフ `true` ィールドに値 `PDFFormRenderSpec` を割り当て `generateServerAppearance` ます。
   * オブジェクト `FormsServiceClient` のメソッドを `renderPDFForm2` 呼び出し、次の値を渡します。

      * レンダリング `BLOB` するPDFフォームを含むオブジェクトです。
      * フォーム `BLOB` とマージするデータを含むオブジェクトです。
      * 実行時 `PDFFormRenderSpec` のオプションを格納するオブジェクト。
      * Formsサ `URLSpec` ービスで必要なURI値を含むオブジェクトです。 このパラメータ `null` ー値を指定できます。
      * 添付ファ `java.util.HashMap` イルを格納するオブジェクト。 これはオプションのパラメーターで、フォームにフ `null` ァイルを添付しないかどうかを指定できます。
      * フォーム内のページ数の保存に使用される長い出力パラメーター。
      * ロケール値に使用される文字列出力パラメーター。
      * インタ `FormResult` ラクティブフォームの保存に使用される出力パラメーターである値です。
   * オブジェクトのフィールドを呼び出してPDF `FormsResult` フォームを取得 `outputContent` します。 このフィールドには、インタラクティブ `BLOB` フォームを表すオブジェクトが格納されます。


1. インタラクティブフォームへの署名

   オブジェクトのドキュメントを呼び出し、 `SignatureServiceClient` 次の値を渡 `sign` して、PDFメソッドに署名します。

   * A `BLOB` object that represents the PDF document to sign. Formsサービスから `BLOB` 返されるインスタンスを使用します。
   * 署名された署名フィールドの名前を表すstring値です。
   * A `Credential` object that represents the credential that is used to digitally sign the PDF document. コンストラクタ `Credential` ーを使用してオブジェクトを作成し、オブジェクトのプロパティに値を割り当ててエイリ `Credential` アスを指定 `alias` します。
   * PDFアルゴリズム `HashAlgorithm` のダイジェストの作成に使用するハッシュアルゴリズムを表す静的データメンバーを指定するオブジェクトです。ドキュメント。 例えば、SHA1アルゴリズムを使 `HashAlgorithm.SHA1` 用するように指定できます。
   * ハッシュアルゴリズムを使用するかどうかを指定するBoolean値です。
   * PDF署名が電子署名された理由を表すstringドキュメント値です。
   * 署名者の場所を表すstring値です。
   * 署名者の連絡先情報を表すstring値です。
   * 電子署 `PDFSignatureAppearanceOptions` 名の外観を制御するオブジェクトです。 例えば、このオブジェクトを使用して、電子署名にカスタムロゴを追加できます。
   * 署名者 `System.Boolean` の証明書に対して失効確認を実行するかどうかを指定するオブジェクトです。 この失効確認が行われると、署名に埋め込まれます。 デフォルトは、`false` です。
   * オンラ `OCSPPreferences` イン証明書ステータスプロトコル(OCSP)サポートの環境設定を格納するオブジェクトです。 失効確認が行われない場合、このパラメーターは使用されず、指定できま `null`す。 このオブジェクトに関する詳細は、『 [AEM Forms APIリファレンス』を参照してください](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   * 証明書失 `CRLPreferences` 効リスト(CRL)の環境設定を格納するオブジェクトです。 失効確認が行われない場合、このパラメーターは使用されず、指定できま `null`す。
   * タイムス `TSPPreferences` タンププロバイダー(TSP)サポートの環境設定を格納するオブジェクトです。 このパラメーターはオプションで、を指定できま `null`す。
   このメソ `sign` ッドは、署名済みPDF `BLOB` メッセージを表すオブジェクトを返しますドキュメント。

1. 署名済みPDFの保存ドキュメント

   * Create a `System.IO.FileStream` object by invoking its constructor. 署名済みPDFドキュメントのファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * メソッドによって返されたオブジェクトの内容を `BLOB` 格納するバイト配列を作成し `sign` ます。 オブジェクトのデータメンバーの値を取得して、バ `BLOB` イト配列を設 `MTOM` 定します。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡すことによって、バ `System.IO.BinaryWriter` イト配列の内 `Write` 容をPDFファイルに書き込みます。

**関連トピック**

[インタラクティブフォームへの電子署名](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## PDF ドキュメントの認証 {#certifying-pdf-documents}

認証署名と呼ばれる特定のタイプの署名によって PDF ドキュメントを認証することで、PDF ドキュメントを保護することができます。認証署名は、以下の方法で電子署名と区別されます。

* 認証署名は PDF ドキュメントに適用される最初の署名です。つまり、認証署名が適用されるときは、ドキュメント内の他の署名フィールドは未署名でなければいけません。認証署名は 1 つの PDF ドキュメントにつき 1 つです。PDF ドキュメントを署名および認証するには、署名の前に認証を行う必要があります。PDF ドキュメントの認証後、他の署名フィールドに電子署名を行うことができます。
* ドキュメントの作成者または発信者は、認証署名を無効にすることなく、特定の方法でドキュメントの変更が可能になるように指定することができます。例えば、フォームへの入力やコメント入力を許可するドキュメントなどがあります。作成者が特定の変更を許可しないように設定を行った場合は、Acrobat はユーザーのその方法によるドキュメントの変更を制限します。別のアプリケーションを使用するなどしてそのような変更が行われた場合は、認証署名は無効となり、Acrobat はユーザーがドキュメントを開いた際に警告を発します。（未認証の署名では、変更を防ぐことはできません。また、通常の編集操作では元の署名は無効になりません。）
* 署名時に、ドキュメントのコンテンツにあいまいさや誤解をもたらす可能性のある、特定の種類のコンテンツをスキャンします。例えば、注釈により、認証される対象を把握するために重要なページ上のテキストが隠れてしまう場合があります。そのようなコンテンツに関する、説明（法的証明）を提供することができます。

SignatureサービスのJava APIまたはSignature WebサービスのAPIを使用して、PDFドキュメントをプログラムで認証できます。 PDF認証を行う場合は、ドキュメントサービスに存在するセキュリティ証明書を参照する必要があります。 セキュリティ証明書について詳しくは、使用しているアプリケ *ーションサーバー版の『AEM Formsのインストール* およびデプロイ』ガイドを参照してください。

>[!NOTE]
>
>同じPDFドキュメントの認証と署名を行う場合、認証署名が信頼されていないと、AcrobatまたはAdobe ReaderでPDFドキュメントを開いたときに、最初の署名の横に黄色い三角形が表示されます。 このような状況を避けるには、認証署名を信頼する必要があります。

>[!NOTE]
>
>PDFドキュメントの署名や認証にnCipher nShield HSM秘密鍵証明書を使用する場合、AEM FormsがデプロイされているJ2EEアプリケーションサーバーを再起動するまで、新しい秘密鍵証明書は使用できません。 ただし、設定値を設定すると、J2EEアプリケーションサーバーを再起動しなくても、署名または認証の操作が機能します。

次の設定値をcknfastrcファイルに追加できます。このファイルは/opt/nfast/cknfastrc(またはc:\nfast\cknfastrc)にあります。

```as3
             CKNFAST_ASSUME_SINGLE_PROCESS=0
```

この設定値をcknfastrcファイルに追加すると、J2EEアプリケーションサーバーを再起動しなくても、新しい秘密鍵証明書を使用できます。

>[!NOTE]
>
>Signatureサービスと認証ドキュメントについて詳しくは、『AEM Formsサービスリフ [ァレンス』を参照してください](https://www.adobe.com/go/learn_aemforms_services_63)。

### 手順の概要 {#summary_of_steps-5}

PDF認証を行うには、次のドキュメントを実行します。

1. プロジェクトファイルを含めます。
1. 署名クライアントの作成を参照してください。
1. 認証するPDFドキュメントを取得します。
1. 「PDFの認証」ドキュメント
1. 認証済みPDFファイルをPDFドキュメントとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar（AEM FormsがJBossにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsがJBossにデプロイされている場合に必要）

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**署名クライアントの作成**

プログラムによって署名操作を実行する前に、署名クライアントを作成する必要があります。

**認証するPDFドキュメントの取得**

PDF署名を認証するには、ドキュメントフィールドを含むPDFドキュメントを取得する必要があります。 PDFドキュメントに署名フィールドが含まれていない場合は、認証できません。 署名フィールドは、Designerを使用して追加することも、プログラムを使用して追加することもできます。 プログラムによる署名フィールドの追加について詳しくは、「署名フィールドの追 [加」を参照してくださ](digitally-signing-certifying-documents.md#adding-signature-fields)い。

**「Certify the PDF」ドキュメント**

PDFドキュメントを正常に認証するには、SignatureサービスでPDFドキュメントの認証に使用される次の入力値が必要です。

* **PDFドキュメント**:署名フィールドを含むPDFドキュメント。認証署名のグラフィック表現を含むフォームフィールドです。 PDFドキュメントを認証する前に、署名フィールドを含める必要があります。 署名フィールドは、Designerを使用して追加することも、プログラムを使用して追加することもできます。 (Adding Signature Fields [](digitally-signing-certifying-documents.md#adding-signature-fields)を参照)。
* **署名フィールド名**:認証される署名フィールドの完全修飾名です。 次の値は例です。 `form1[0].#subform[1].SignatureField3[3]`. XFAフォームフィールドを使用する場合、署名フィールドの名前の一部を使用することもできます。 `SignatureField3[3]`. フィールド名にnull値が渡されると、非表示の署名フィールドが動的に作成され、認証されます。
* **セキュリティ証明書**:PDF認証の認証に使用される秘密鍵証明書です。ドキュメント このセキュリティ証明書には、パスワードとエイリアスが含まれています。このエイリアスは、Credentialサービス内の秘密鍵証明書に表示されるエイリアスと一致する必要があります。 エイリアスは、PKCS#12ファイル（拡張子.pfx付き）またはハードウェアセキュリティモジュール(HSM)内にある実際の秘密鍵証明書への参照です。
* **ハッシュアルゴリズム**:PDFアルゴリズムのダイジェストの作成に使用するハッシュドキュメントです。
* **署名の理由**:他のユーザーがPDFユーザーを認証した理由を知るためにAcrobatまたはAdobe Readerで表示されるドキュメントです。
* **署名者の場所**:秘密鍵証明書で指定された署名者の場所です。
* **連絡先情報**:署名者の住所や電話番号などの連絡先情報。
* **権限情報**:認証署名を無効にすることなく、エンドユーザーがドキュメントで実行できるアクションを制御する権限です。 例えば、権限を設定して、PDF署名を変更すると認証署名がドキュメントになるようにすることができます。
* **法的説明**:ドキュメントが認証されると、認証の内容をあいまいにしたり誤解を招く可能性のある特定のタイプのコンテンツが、ドキュメントによって自動的にスキャンされます。 例えば、注釈により、認証される対象を把握するために重要なページ上のテキストが隠れてしまう場合があります。スキャン処理では、これらのタイプのコンテンツに関する警告が生成されます。 この値は、警告が生成された可能性のあるコンテンツの追加の説明を提供します。
* **外観オプション**:認証署名の外観を制御するオプションです。 例えば、認証署名に日付情報を表示できます。
* **失効確認**:この値は、署名者の証明書に対して失効確認を行うかどうかを指定します。 デフォルト設定のでは、失 `false` 効確認は行われません。
* **OCSP settings**:PDFドキュメントの認証に使用される秘密鍵証明書のステータスに関する情報を提供する、オンライン証明書ステータスプロトコル(OCSP)のサポートの設定です。 例えば、PDFサーバーへのサインオンに使用する秘密鍵証明書に関する情報を提供するサーバーのURLを指定できます。ドキュメント
* **CRL settings**:証明書失効リスト(CRL)の設定（失効確認が行われた場合）。 例えば、秘密鍵証明書が失効したかどうかを常に確認するように指定できます。
* **タイムスタンプ**:認証署名に適用されるタイムスタンプ情報を定義する設定です。 タイムスタンプは、特定の時間の前に特定のデータが確立されたことを示します。 この知識は、署名者と検証者の間に信頼関係を構築するのに役立ちます。

**認証済みPDFドキュメントをPDFファイルとして保存**

SignatureサービスがPDFドキュメントを認証したら、PDFファイルとして保存し、ユーザーがAcrobatまたはAdobe Readerで開くことができるようにすることができます。

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

   * コンストラ `java.io.FileInputStream` クターを使用し、PDFドキュメントの場所を指定するstring値を渡すことで、認証するPDFドキュメントを表すオブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 「Certify the PDF」ドキュメント

   オブジェクトのドキュメントを呼び出し、 `SignatureServiceClient` 次の値を渡 `certify` して、PDFメソッドを認証します。

   * 認証す `com.adobe.idp.Document` るPDFドキュメントを表すオブジェクトです。
   * 署名を含む署名フィールドの名前を表すstring値です。
   * A `Credential` object that represents the credential that is used to certify the PDF document. オブジェクト `Credential` の静的メソッドを呼 `Credential` び出し、セキュリテ `getInstance` ィ秘密鍵証明書に対応するエイリアス値を指定するstring値を渡して、オブジェクトを作成します。
   * PDFアルゴリズム `HashAlgorithm` のダイジェストの作成に使用されるハッシュアルゴリズムを表す静的データメンバーを指定するドキュメントです。 例えば、SHA1アルゴリズムを使 `HashAlgorithm.SHA1` 用するように指定できます。
   * PDF認証が行われた理由を表すstringドキュメント値です。
   * 署名者の連絡先情報を表すstring値です。
   * 署名を `MDPPermissions` 無効にするPDFドキュメントで実行できるアクションを指定するオブジェクトです。
   * 認証署 `PDFSignatureAppearanceOptions` 名の外観を制御するオブジェクトです。 必要に応じて、などのメソッドを呼び出して、署名の外観を変更しま `setShowDate`す。
   * 署名を無効にするアクションに関する説明を提供するstring値です。
   * 署名者 `java.lang.Boolean` の証明書に対して失効確認を実行するかどうかを指定するオブジェクトです。 この失効確認が行われると、署名に埋め込まれます。 デフォルトは、`false` です。
   * 認証さ `java.lang.Boolean` れる署名フィールドをロックするかどうかを指定するオブジェクトです。 フィールドをロックすると、署名フィールドは読み取り専用としてマークされ、プロパティを変更できなくなり、必要な権限を持たないユーザーはこのフィールドをクリアできません。 デフォルトは、`false` です。
   * オンラ `OCSPPreferences` イン証明書ステータスプロトコル(OCSP)サポートの環境設定を格納するオブジェクトです。 失効確認が行われない場合、このパラメーターは使用されず、指定できま `null`す。 このオブジェクトに関する詳細は、『 [AEM Forms APIリファレンス』を参照してください](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。
   * 証明書失 `CRLPreferences` 効リスト(CRL)の環境設定を格納するオブジェクトです。 失効確認が行われない場合、このパラメーターは使用されず、指定できま `null`す。
   * タイムス `TSPPreferences` タンププロバイダー(TSP)サポートの環境設定を格納するオブジェクトです。 例えば、オブジェクトを作成し `TSPPreferences` た後、オブジェクトのメソッドを呼び出して、TSPサーバーのURLを `TSPPreferences` 設定でき `setTspServerURL` ます。 このパラメーターはオプションで、を指定できま `null`す。 For more information, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).
   このメソ `certify` ッドは、認証済みのPDF `com.adobe.idp.Document` ドキュメントを表すオブジェクトを返します。

1. 認証済みPDFドキュメントをPDFファイルとして保存

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が .pdf であることを確認します。
   * Invoke the `com.adobe.idp.Document` object’s `copyToFile` method to copy the contents of the `com.adobe.idp.Document` object to the file.

**関連トピック**

[PDF ドキュメントの認証](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[クイック開始（SOAPモード）:Java APIを使用したPDFドキュメントの認証](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-certifying-a-pdf-document-using-the-java-api)

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
   * Create a `SignatureServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLを指定するstring値をAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/SignatureService?WSDL`)に渡します。 属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます)。
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得して、オブジェクトを作成 `SignatureServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のオプションを実行して、基本的なHTTP認証を有効にします。タスク

      * AEM formsのユーザー名をフィールドに割り当てま `SignatureServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `SignatureServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールドに `HttpClientCredentialType.Basic` 割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールドに `BasicHttpSecurityMode.TransportCredentialOnly` 割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. 認証するPDFドキュメントの取得

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。オブジェクト `BLOB` は、認証済みのPDFドキュメントの保存に使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、認証するPDFドキュメントーのファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * オブジェクトの内容を格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得す `System.IO.FileStream` ることで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイ `System.IO.FileStream` ト配列、開始位 `Read` 置およびストリームの長さを渡すことで、バイト配列にストリームデータを入力します。
   * データメン `BLOB` バにバイト配列の内容を割り `MTOM` 当てて、オブジェクトを設定します。

1. 「Certify the PDF」ドキュメント

   オブジェクトのドキュメントを呼び出し、 `SignatureServiceClient` 次の値を渡 `certify` して、PDFメソッドを認証します。

   * 認証す `BLOB` るPDFドキュメントを表すオブジェクトです。
   * 署名を含む署名フィールドの名前を表すstring値です。
   * A `Credential` object that represents the credential that is used to certify the PDF document. コンストラクタ `Credential` ーを使用してオブジェクトを作成し、オブジェクトのプロパティに値を割り当ててエイリ `Credential` アスを指定 `alias` します。
   * PDFアルゴリズム `HashAlgorithm` のダイジェストの作成に使用されるハッシュアルゴリズムを表す静的データメンバーを指定するドキュメントです。 例えば、SHA1アルゴリズムを使 `HashAlgorithm.SHA1` 用するように指定できます。
   * ハッシュアルゴリズムを使用するかどうかを指定するBoolean値です。
   * PDF認証が行われた理由を表すstringドキュメント値です。
   * 署名者の場所を表すstring値です。
   * 署名者の連絡先情報を表すstring値です。
   * 署名を `MDPPermissions` 無効にするPDFドキュメントで実行できるアクションを指定するオブジェクトの静的データメンバーです。
   * 前のパラメーター値として渡されたオブジ `MDPPermissions` ェクトを使用するかどうかを指定するBoolean値です。
   * 署名を無効にするアクションを説明するstring値です。
   * 認証署 `PDFSignatureAppearanceOptions` 名の外観を制御するオブジェクトです。 コンストラクタを使用して `PDFSignatureAppearanceOptions` オブジェクトを作成します。署名の外観は、そのデータメンバーの1つを設定することで変更できます。
   * 署名者 `System.Boolean` の証明書に対して失効確認を実行するかどうかを指定するオブジェクトです。 この失効確認が行われると、署名に埋め込まれます。 デフォルトは、`false` です。
   * 認証さ `System.Boolean` れる署名フィールドをロックするかどうかを指定するオブジェクトです。 フィールドをロックすると、署名フィールドは読み取り専用としてマークされ、プロパティを変更できなくなり、必要な権限を持たないユーザーはこのフィールドをクリアできません。 デフォルトは、`false` です。
   * 署名フ `System.Boolean` ィールドをロックするかどうかを指定するオブジェクトです。 つまり、前のパラメーター `true` に渡した場合は、このパラメー `true` ターに渡します。
   * PDFドキュメント `OCSPPreferences` の認証に使用される秘密鍵証明書のステータスに関する情報を提供する、オンライン証明書ステータスプロトコル(OCSP)サポートの環境設定を格納するオブジェクトです。 失効確認が行われない場合、このパラメーターは使用されず、指定できま `null`す。
   * 証明書失 `CRLPreferences` 効リスト(CRL)の環境設定を格納するオブジェクトです。 失効確認が行われない場合、このパラメーターは使用されず、指定できま `null`す。
   * タイムス `TSPPreferences` タンププロバイダー(TSP)サポートの環境設定を格納するオブジェクトです。 例えば、オブジェクトを作成し `TSPPreferences` た後に、オブジェクトのデータメンバーを設定することで、TSPのURL `TSPPreferences` を設定するこ `tspServerURL` とができます。 このパラメーターはオプションで、を指定できま `null`す。
   このメソ `certify` ッドは、認証済みのPDF `BLOB` ドキュメントを表すオブジェクトを返します。

1. 認証済みPDFドキュメントをPDFファイルとして保存

   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、認証済みのPDFドキュメントーと、そのファイルを開くモードを含むPDFドキュメントーのファイルの場所を表すstring値を渡します。
   * メソッドによって返されたオブジェクトの内容を `BLOB` 格納するバイト配列を作成し `certify` ます。 オブジェクトのデータメンバーの値を取得して、バ `BLOB` イト配列を設 `binaryData` 定します。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡すことによって、バ `System.IO.BinaryWriter` イト配列の内 `Write` 容をPDFファイルに書き込みます。

**関連トピック**

[PDF ドキュメントの認証](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Verifying Digital Signatures {#verifying-digital-signatures}

電子署名を検証することで、署名された PDF ドキュメントに変更がなく、電子署名が有効であることを確認することができます。電子署名を検証する際に、署名のステータスや、署名者のIDなどの署名のプロパティを確認できます。 電子署名を信用する前に、検証することをおすすめします。電子署名を検証する際、電子署名を含む PDF ドキュメントを参照します。

署名者のIDが不明であるとします。 次の図に示すように、AcrobatでPDFドキュメントを開くと、署名者のIDが不明であることを示す警告メッセージが表示されます。

![vd_vd_verifysig](assets/vd_vd_verifysig.png)

同様に、プログラムによって電子署名を検証する場合、署名者のIDのステータスを判断できます。 例えば、前の図に示したドキュメントで電子署名を検証した場合、署名者のIDが不明になります。

>[!NOTE]
>
>Signatureサービスと電子署名の検証について詳しくは、『AEM Formsサービスリファレ [ンス』を参照してください](https://www.adobe.com/go/learn_aemforms_services_63)。

### 手順の概要 {#summary_of_steps-6}

電子署名を検証するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. 署名クライアントの作成を参照してください。
1. 検証する署名が含まれるPDFドキュメントを取得します。
1. PKI実行時オプションを設定します。
1. 電子署名を検証します。
1. 署名のステータスを確認します。
1. 署名者のIDを特定します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを含めます。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar（AEM FormsがJBossにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsがJBossにデプロイされている場合に必要）

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**署名クライアントの作成**

プログラムによってSignatureサービスの操作を実行する前に、Signatureサービスクライアントを作成します。

**検証する署名を含むPDFドキュメントを取得します**

PDF署名のデジタル署名または認証に使用されるドキュメントを検証するには、署名を含むPDFドキュメントを取得します。

**PKI実行時オプションの設定**

PDFドキュメントの署名を検証する際にSignatureサービスで使用するPKIランタイムオプションを設定します。

* 検証時刻
* 失効確認
* タイムスタンプ値

これらのオプションの設定の一環として、検証時間を指定できます。 例えば、現在の時刻（バリデーターのコンピューター上の時刻）を選択し、現在の時刻を使用するように指定できます。 様々な時間値について詳しくは、『 `VerificationTime` AEM Forms APIリファレンス』の「 [定義済みリスト値」を参](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)照してください。

また、検証プロセスの一部として失効確認を実行するかどうかを指定できます。 例えば、証明書が失効しているかどうかを確認するための失効確認を実行できます。 失効確認オプションについて詳しくは、『 `RevocationCheckStyle` AEM Forms APIリファレンス』の「 [定義済みリストの値」を参照し](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)てください。

証明書に対して失効確認を実行するには、オブジェクトを使用して、証明書失効リスト(CRL)サーバーへのURLを指定 `CRLOptionSpec` します。 ただし、CRLサーバーへのURLを指定しない場合、Signatureサービスは証明書からURLを取得します。

失効確認を実行する際は、CRLサーバーを使用する代わりに、オンライン証明書ステータスプロトコル(OCSP)サーバーを使用できます。 通常、CRLサーバーとは異なるOCSPサーバーを使用する場合、失効確認の実行が速くなります。 (See [Online Certificate Status Protocol](https://tools.ietf.org/html/rfc2560).)

Signatureサービスで使用するCRLおよびOCSPサーバーの順序は、Adobe Applications and Servicesを使用して設定できます。 例えば、OCSPサーバーがAdobe Applications and Servicesで最初に設定されている場合は、OCSPサーバーがチェックされ、次にCRLサーバーがチェックされます。

失効確認を実行しない場合、Signatureサービスは、証明書が失効しているかどうかを確認しません。 つまり、CRLおよびOCSPサーバー情報は無視されます。

>[!NOTE]
>
>証明書で指定されたURLは、およびオブジェクトを使用して上 `CRLOptionSpec` 書きでき `OCSPOptionSpec` ます。 例えば、CRLサーバーを上書きするには、オブジェクトのメ `CRLOptionSpec` ソッドを呼び出し `setLocalURI` ます。

タイムスタンプとは、署名済みまたは認証済みのドキュメントが変更された時刻を追跡する処理です。 署名後は、ドキュメントを変更することはできません。 タイムスタンプを使用すると、署名済みまたは認証済みのドキュメントの有効性を強制できます。 オブジェクトを使用して、タイムスタンプオプションを設定 `TSPOptionSpec` できます。 例えば、タイムスタンププロバイダー(TSP)サーバーのURLを指定できます。

>[!NOTE]
>
>JavaおよびWebサービスのクイック開始では、検証時刻がに設定され、失 `VerificationTime.CURRENT_TIME` 効確認がに設定されま `RevocationCheckStyle.BestEffort`す。 CRLまたはOCSPサーバー情報が指定されていないので、サーバー情報は証明書から取得されます。

**電子署名の検証**

署名を正しく検証するには、署名が含まれる署名フィールドの完全修飾名（など）を指定しま `form1[0].#subform[1].SignatureField3[3]`す。 XFAフォームフィールドを使用する場合は、署名フィールドの名前の一部を使用することもできます。 `SignatureField3`.

デフォルトでは、Signatureサービスは、検証後にドキュメントに署名できる時間を65分に制限します。 ユーザーが現在の時刻に署名を検証しようとし、その時刻が現在の時刻より後で、65分以内になった場合、Signatureサービスは検証エラーを作成しません。

>[!NOTE]
>
>署名を検証する際に必要なその他の値については、『 [AEM Forms APIリファレンス』を参照してください](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)。

**署名のステータスの確認**

電子署名の検証の一環として、署名のステータスを確認できます。

**署名者のIDの確認**

署名者のIDを特定できます。次の値のいずれかを使用できます。

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

1. 検証する署名を含むPDFドキュメントを取得します

   * 検証する署 `java.io.FileInputStream` 名を含むPDFドキュメントを表すオブジェクトを、コンストラクターを使用して作成します。 PDFフォルダーの場所を指定するstring値を渡します。ドキュメント
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PKI実行時オプションの設定

   * コンストラクタを使用して `PKIOptions` オブジェクトを作成します。
   * 検証時間を設定するには、オブジェクトのメ `PKIOptions` ソッドを呼び出 `setVerificationTime` し、検証時間を指定する `VerificationTime` 定義済みリスト値を渡します。
   * 失効確認オプションを設定するには、オブジェク `PKIOptions` トのメソッドを `setRevocationCheckStyle` 呼び出し、失効確認を実行するかどう `RevocationCheckStyle` かを指定する定義済みリスト値を渡します。

1. 電子署名の検証

   オブジェクトのメソッドを呼び出し、 `SignatureServiceClient` 次の値を渡 `verify2` して、署名を検証します。

   * デジタル署 `com.adobe.idp.Document` 名された、または認証されたPDFドキュメントを含むオブジェクト。
   * 検証する署名が含まれている署名フィールド名を表すstring値です。
   * PKI実行 `PKIOptions` 時オプションを含むオブジェクトです。
   * SPI情報 `VerifySPIOptions` を含むインスタンスです。 このパラメーター `null` を指定できます。
   このメ `verify2` ソッドは、電 `PDFSignatureVerificationInfo` 子署名の検証に使用できる情報を含むオブジェクトを返します。

1. 署名のステータスの確認

   * オブジェクトのメソッドを呼び出して、署名のス `PDFSignatureVerificationInfo` テータスを特定 `getStatus` します。 このメソッドは、署名のステ `SignatureStatus` ータスを指定するオブジェクトを返します。 例えば、署名済みPDFドキュメントが変更されない場合、このメソッドはを返しま `SignatureStatus.DocumentSigNoChanges`す。

1. 署名者のIDの確認

   * オブジェクトのメソッドを呼び出して、署名者のID `PDFSignatureVerificationInfo` を特定し `getSigner` ます。 このメソッドは、オブジェクトを `IdentityInformation` 返します。
   * オブジェクト `IdentityInformation` のメソッドを `getStatus` 呼び出して、署名者のIDを特定します。 このメソッドは、IDを指 `IdentityStatus` 定する定義済みリスト値を返します。 例えば、署名者が信頼できる場合、このメソッドはを返しま `IdentityStatus.TRUSTED`す。

**関連トピック**

[電子署名の検証](#verify-digital-signatures-using-the-java-api)

[クイック開始（SOAPモード）:Java APIを使用した電子署名の検証](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-a-digital-signature-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用した電子署名の検証 {#verify-digital-signatures-using-the-web-service-api}

Signature Service API（Webサービス）を使用して、デジタル署名を検証します。

1. プロジェクトファイルを含める

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。 `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Formsをホ `localhost` ストするサーバーのIPアドレスで置き換えます。

1. 署名クライアントの作成

   * Create a `SignatureServiceClient` object by using its default constructor.
   * Create a `SignatureServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLを指定するstring値をAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/SignatureService?WSDL`)に渡します。 属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます)。
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得して、オブジェクトを作成 `SignatureServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のオプションを実行して、基本的なHTTP認証を有効にします。タスク

      * AEM formsのユーザー名をフィールドに割り当てま `SignatureServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `SignatureServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールドに `HttpClientCredentialType.Basic` 割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールドに `BasicHttpSecurityMode.TransportCredentialOnly` 割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. 検証する署名を含むPDFドキュメントを取得します

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、検証するデジタル署名または認証ドキュメントを含むPDF署名を保存するために使用されます。
   * Create a `System.IO.FileStream` object by invoking its constructor. 署名済みPDFドキュメントのファイルの場所と、ファイルを開くモードを表すstring値を渡します。
   * オブジェクトの内容を格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得す `System.IO.FileStream` ることで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出して、バイト配列にストリ `System.IO.FileStream` ームデータを入力 `Read` します。 読み取るバイト配列、開始位置およびストリーム長を渡します。
   * オブジェクトの `BLOB` プロパティにバイト配列の `MTOM` 内容を割り当てて、オブジェクトを設定します。

1. PKI実行時オプションの設定

   * コンストラクタを使用して `PKIOptions` オブジェクトを作成します。
   * 検証時刻を設定するには、オブジェクトのデ `PKIOptions` ータメンバ `verificationTime` ーに検証時刻を指 `VerificationTime` 定する定義済みリスト値を割り当てます。
   * 失効確認オプションを設定するには、オブジェクトのデ `PKIOptions` ータメンバーに失 `revocationCheckStyle` 効確認を実行するかどう `RevocationCheckStyle` かを指定する定義済みリスト値を割り当てます。

1. 電子署名の検証

   オブジェクトのメソッドを呼び出し、 `SignatureServiceClient` 次の値を渡 `verify2` して、署名を検証します。

   * デジタル署 `BLOB` 名された、または認証されたPDFドキュメントを含むオブジェクト。
   * 検証する署名が含まれている署名フィールド名を表すstring値です。
   * PKI実行 `PKIOptions` 時オプションを含むオブジェクトです。
   * SPI情報 `VerifySPIOptions` を含むインスタンスです。 このパラメーター `null` を指定できます。
   このメ `verify2` ソッドは、電 `PDFSignatureVerificationInfo` 子署名の検証に使用できる情報を含むオブジェクトを返します。

1. 署名のステータスの確認

   オブジェクトのデータメンバーの値を取得して、署名のス `PDFSignatureVerificationInfo` テータスを決 `status` 定します。 このデータメンバーは、署名のス `SignatureStatus` テータスを指定するオブジェクトを格納します。 例えば、署名済みPDFドキュメントが変更された場合、データメ `status` ンバーに値が格納されま `SignatureStatus.DocumentSigNoChanges`す。

1. 署名者のIDの確認

   * オブジェクトのデータメンバーの値を取得して、署名者のID `PDFSignatureVerificationInfo` を特定 `signer` します。 このメンバはオブジェクトを `IdentityInformation` 返します。
   * 署名者のID `IdentityInformation` を特定す `status` るオブジェクトのデータメンバーを取得します。 このデータメンバは、IDを指 `IdentityStatus` 定する定義済みリスト値を返します。 例えば、署名者が信頼できる場合、このメンバーはを返しま `IdentityStatus.TRUSTED`す。

**関連トピック**

[電子署名の検証](#verify-digital-signatures-using-the-java-api)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Verifying Multiple Digital Signatures {#verifying-multiple-digital-signatures}

AEM Formsは、PDF署名内のすべての電子署名を検証する手段を提供します。ドキュメント PDFドキュメントに複数の電子署名が含まれているとします。これは、複数の署名者による署名が必要なビジネスプロセスの結果です。 例えば、融資担当者と管理者の両方の署名が必要な金融トランザクションについて考えてみましょう。 SignatureサービスのJava APIまたはWebサービスAPIを使用して、PDFドキュメント内のすべての署名を検証できます。 複数の署名を検証する際は、それぞれの署名のステータスやプロパティを確認できます。電子署名を信頼する前に、検証することをお勧めします。 単一の電子署名の検証について詳しく理解することをお勧めします。

>[!NOTE]
>
>Signatureサービスと電子署名の検証について詳しくは、『AEM Formsサービスリファレ [ンス』を参照してください](https://www.adobe.com/go/learn_aemforms_services_63)。

### 手順の概要 {#summary_of_steps-7}

複数の電子署名を検証するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. 署名クライアントの作成を参照してください。
1. 検証する署名が含まれるPDFドキュメントを取得します。
1. PKI実行時オプションを設定します。
1. すべての電子署名を取得します。
1. すべての署名を繰り返し処理します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを含めます。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar（AEM FormsがJBossにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsがJBossにデプロイされている場合に必要）

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**署名クライアントの作成**

プログラムによってSignatureサービスの操作を実行する前に、Signatureサービスクライアントを作成します。

**検証する署名を含むPDFドキュメントを取得します**

PDF署名のデジタル署名または認証に使用されるドキュメントを検証するには、署名を含むPDFドキュメントを取得します。

**PKIランタイムオプションの設定**

PDFドキュメント内のすべての署名を検証する際にSignatureサービスで使用するPKIランタイムオプションを設定します。

* 検証時刻
* 失効確認
* タイムスタンプ値

これらのオプションの設定の一環として、検証時間を指定できます。 例えば、現在の時刻（バリデーターのコンピューター上の時刻）を選択し、現在の時刻を使用するように指定できます。 様々な時間値について詳しくは、『 `VerificationTime` AEM Forms APIリファレンス』の「 [定義済みリスト値」を参](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)照してください。

また、検証プロセスの一部として失効確認を実行するかどうかを指定できます。 例えば、証明書が失効しているかどうかを確認するための失効確認を実行できます。 失効確認オプションについて詳しくは、『 `RevocationCheckStyle` AEM Forms APIリファレンス』の「 [定義済みリストの値」を参照し](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)てください。

証明書に対して失効確認を実行するには、オブジェクトを使用して、証明書失効リスト(CRL)サーバーへのURLを指定 `CRLOptionSpec` します。 ただし、CRLサーバーへのURLを指定しない場合、Signatureサービスは証明書からURLを取得します。

失効確認を実行する際は、CRLサーバーを使用する代わりに、オンライン証明書ステータスプロトコル(OCSP)サーバーを使用できます。 通常、CRLサーバーではなくOCSPサーバーを使用する場合、失効確認の実行が高速になります。 (See [Online Certificate Status Protocol](https://tools.ietf.org/html/rfc2560).)

Signatureサービスで使用するCRLおよびOCSPサーバーの順序は、Adobe Applications and Servicesを使用して設定できます。 例えば、OCSPサーバーがAdobe Applications and Servicesで最初に設定されている場合、OCSPサーバーがチェックされ、その後にCRLサーバーがチェックされます。

失効確認を実行しない場合、Signatureサービスは、証明書が失効しているかどうかを確認しません。 つまり、CRLおよびOCSPサーバー情報は無視されます。

>[!NOTE]
>
>証明書で指定されたURLは、およびオブジェクトを使用して上 `CRLOptionSpec` 書きでき `OCSPOptionSpec` ます。 例えば、CRLサーバーを上書きするには、オブジェクトのメ `CRLOptionSpec` ソッドを呼び出し `setLocalURI` ます。

タイムスタンプとは、署名済みまたは認証済みのドキュメントが変更された時刻を追跡する処理です。 署名後は、ドキュメントを変更することはできません。 タイムスタンプを使用すると、署名済みまたは認証済みのドキュメントの有効性を強制できます。 タイムスタンプオプションは、オブジェクトを使用して設定 `TSPOptionSpec` できます。 例えば、タイムスタンププロバイダー(TSP)サーバーのURLを指定できます。

>[!NOTE]
>
>JavaおよびWebサービスのクイック開始では、検証時刻がに設定され、失 `VerificationTime.CURRENT_TIME` 効確認がに設定されま `RevocationCheckStyle.BestEffort`す。 CRLまたはOCSPサーバー情報が指定されていないので、サーバー情報は証明書から取得されます。

**すべての電子署名の取得**

PDFドキュメント内のすべての電子署名を検証するには、PDFドキュメントから電子署名を取得します。 すべての署名が1つの署名で返されます。リスト 電子署名の検証の一環として、署名のステータスを確認します。

>[!NOTE]
>
>単一の電子署名を検証する場合とは異なり、複数の署名を検証する場合は、署名フィールド名を指定する必要はありません。

**すべての署名を繰り返し処理します**

各署名を繰り返し処理します。 つまり、各署名について、電子署名を検証し、署名者のIDと各署名のステータスを確認します。 (電子署名 [の検証を参照](#verify-digital-signatures-using-the-java-api))。

>[!NOTE]
>
>要件が署名全体である場合は、すべての署名を繰り返し処理する必要はありません。ドキュメント

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

1. 検証する署名を含むPDFドキュメントを取得します

   * 複数の電子署 `java.io.FileInputStream` 名を含むPDFドキュメントを表すオブジェクトを作成し、そのコンストラクターを使用して検証します。 PDFフォルダーの場所を指定するstring値を渡します。ドキュメント
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PKIランタイムオプションの設定

   * コンストラクタを使用して `PKIOptions` オブジェクトを作成します。
   * 検証時間を設定するには、オブジェクトのメ `PKIOptions` ソッドを呼び出 `setVerificationTime` し、検証時間を指定する `VerificationTime` 定義済みリスト値を渡します。
   * 失効確認オプションを設定するには、オブジェ `PKIOptions` クトのメソッ `setRevocationCheckStyle` ドを呼び出し、失効確認を実行するかどう `RevocationCheckStyle` かを指定する定義済みリスト値を渡します。

1. すべての電子署名の取得

   オブジェクト `SignatureServiceClient` のメソッドを `verifyPDFDocument` 呼び出し、次の値を渡します。

   * 複数の電 `com.adobe.idp.Document` 子署名を含むPDFドキュメントを含むオブジェクトです。
   * PKI実行 `PKIOptions` 時オプションを含むオブジェクトです。
   * SPI情報 `VerifySPIOptions` を含むインスタンスです。 このパラメーター `null` を指定できます。
   このメソ `verifyPDFDocument` ッドは、PDF `PDFDocumentVerificationInfo` メソッド内のすべての電子署名に関する情報を含むオブジェクトを返します。ドキュメント

1. すべての署名を繰り返し処理します

   * オブジェクトのメソッドを呼び出して、すべての `PDFDocumentVerificationInfo` 署名を繰り返し処 `getVerificationInfos` 理します。 このメソッドは、各要素がオ `java.util.List` ブジェクトであるオブジェクトを返 `PDFSignatureVerificationInfo` します。 オブジェクト `java.util.Iterator` を使用して、署名のリストを繰り返します。
   * オブジェクト `PDFSignatureVerificationInfo` を使用すると、タスクのステータスを判断するなど、オブジェクトのメソッドを呼び出すこ `PDFSignatureVerificationInfo` とで署名を実行で `getStatus` きます。 このメソッドは、署名のス `SignatureStatus` テータスを通知する静的データメンバーを持つオブジェクトを返します。 例えば、署名が不明な場合、このメソッドはを返しま `SignatureStatus.DocumentSignatureUnknown`す。

**関連トピック**

[複数の電子署名の検証](#verifying-multiple-digital-signatures)

[クイック開始（SOAPモード）:Java APIを使用した複数の電子署名の検証](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-multiple-digital-signatures-using-the-java-api)

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
   * Create a `SignatureServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLを指定するstring値をAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/SignatureService?WSDL`)に渡します。 属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます)。
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得して、オブジェクトを作成 `SignatureServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のオプションを実行して、基本的なHTTP認証を有効にします。タスク

      * AEM formsのユーザー名をフィールドに割り当てま `SignatureServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `SignatureServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールドに `HttpClientCredentialType.Basic` 割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールドに `BasicHttpSecurityMode.TransportCredentialOnly` 割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. 検証する署名を含むPDFドキュメントを取得します

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオブジ `BLOB` ェクトには、検証する複数の電子署名を含むPDFドキュメントが格納されます。
   * Create a `System.IO.FileStream` object by invoking its constructor. PDFファイルの場所と、ファイルを開くドキュメントを表すstring値を渡します。
   * オブジェクトの内容を格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得す `System.IO.FileStream` ることで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出して、バイト配列にストリ `System.IO.FileStream` ームデータを入力 `Read` します。 読み取るバイト配列、開始位置およびストリーム長を渡します。
   * オブジェクトの `BLOB` プロパティにバイト配列の `MTOM` 内容を割り当てて、オブジェクトを設定します。

1. PKIランタイムオプションの設定

   * コンストラクタを使用して `PKIOptions` オブジェクトを作成します。
   * 検証時刻を設定するには、オブジェクトのデ `PKIOptions` ータメンバ `verificationTime` ーに検証時刻を指 `VerificationTime` 定する定義済みリスト値を割り当てます。
   * 失効確認オプションを設定するには、オブジェク `PKIOptions` トのデータメン `revocationCheckStyle` バーに失効確認を実行する `RevocationCheckStyle` かどうかを指定する定義済みリスト値を割り当てます。

1. すべての電子署名の取得

   オブジェクト `SignatureServiceClient` のメソッドを `verifyPDFDocument` 呼び出し、次の値を渡します。

   * 複数の電 `BLOB` 子署名を含むPDFドキュメントを含むオブジェクトです。
   * PKI実行 `PKIOptions` 時オプションを含むオブジェクトです。
   * SPI情報 `VerifySPIOptions` を含むインスタンスです。 このパラメーターにはnullを指定できます。
   このメソ `verifyPDFDocument` ッドは、PDF `PDFDocumentVerificationInfo` メソッド内のすべての電子署名に関する情報を含むオブジェクトを返します。ドキュメント

1. すべての署名を繰り返し処理します

   * オブジェクトのデータメンバーを取得して、す `PDFDocumentVerificationInfo` べての署名を繰り返 `verificationInfos` し処理します。 このデータメンバは、各要 `Object` 素がオブジェクトである配列を返 `PDFSignatureVerificationInfo` します。
   * このオブジ `PDFSignatureVerificationInfo` ェクトを使用すると、タスクのデータメンバーを取得して、署名のステータスを決定する `PDFSignatureVerificationInfo` などの操作を実 `status` 行できます。 このデータメンバは、署名のス `SignatureStatus` テータスを通知する静的データメンバを持つオブジェクトを返します。 例えば、署名が不明な場合、このメソッドはを返しま `SignatureStatus.DocumentSignatureUnknown`す。

**関連トピック**

[複数の電子署名の検証](#verifying-multiple-digital-signatures)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Removing Digital Signatures {#removing-digital-signatures}

新しい電子署名を適用する前に、電子署名を署名フィールドから削除する必要があります。 電子署名は上書きできません。 署名を含む署名フィールドに電子署名を適用しようとすると、例外が発生します。

>[!NOTE]
>
>For more information about the Signature service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-8}

署名フィールドから電子署名を削除するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. 署名クライアントの作成を参照してください。
1. 削除する署名を含むPDFドキュメントを取得します。
1. 署名フィールドから電子署名を削除します。
1. PDFファイルとしてPDFドキュメントを保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar（AEM FormsがJBossにデプロイされている場合に必要）
* jbossall-client.jar（AEM FormsがJBossにデプロイされている場合に必要）

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**署名クライアントの作成**

プログラムによってSignatureサービスの操作を実行する前に、Signatureサービスクライアントを作成する必要があります。

**削除する署名を含むPDFドキュメントを取得します**

PDF署名を削除するには、ドキュメントを含むPDFドキュメントを取得する必要があります。

**署名フィールドからの電子署名の削除**

PDFドキュメントから電子署名を正しく削除するには、電子署名が含まれる署名フィールドの名前を指定する必要があります。 また、電子署名を削除する権限が必要です。それ以外の場合は、例外が発生します。

**PDFファイルとしてPDFドキュメントを保存します**

Signatureサービスで署名フィールドから電子署名を削除した後、PDFドキュメントをPDFファイルとして保存し、AcrobatまたはAdobe Readerで開くことができます。

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

1. 署名クライアントの作成を参照してください。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `SignatureServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 削除する署名を含むPDFドキュメントを取得します

   * コンストラ `java.io.FileInputStream` クターを使用し、PDFドキュメントの場所を指定するstring値を渡すことで、削除する署名が含まれるPDFドキュメントを表すオブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 署名フィールドからの電子署名の削除

   オブジェクトのメソッドを呼び出し、次の値を渡して、署 `SignatureServiceClient` 名フィールド `clearSignatureField` から電子署名を削除します。

   * 削除す `com.adobe.idp.Document` る署名が含まれているPDFドキュメントを表すオブジェクトです。
   * 電子署名が含まれる署名フィールドの名前を指定するstring値です。
   電子署 `clearSignatureField` 名が削除さ `com.adobe.idp.Document` れたPDFドキュメントを表すオブジェクトを返します。

1. PDFファイルとしてPDFドキュメントを保存します

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が .pdf であることを確認します。
   * オブジェクトの `com.adobe.idp.Document` メソッドを呼び出 `copyToFile` します。 オブジェクト `java.io.File` を渡して、オブジェクトの内容をフ `com.adobe.idp.Document` ァイルにコピーします。 `Document` メソッドから返された `clearSignatureField` オブジェクトを必ず使用してください。

**関連トピック**

[電子署名の削除](digitally-signing-certifying-documents.md#removing-digital-signatures)

[クイック開始（SOAPモード）:Java APIを使用した電子署名の削除](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-removing-a-digital-signature-using-the-java-api)

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
   * Create a `SignatureServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLを指定するstring値をAEM Formsサービス(例えば、 `http://localhost:8080/soap/services/SignatureService?WSDL`)に渡します。 属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます)。
   * フィールド `System.ServiceModel.BasicHttpBinding` の値を取得して、オブジェクトを作成 `SignatureServiceClient.Endpoint.Binding` します。 戻り値を `BasicHttpBinding` にキャストします。
   * オブジェクト `System.ServiceModel.BasicHttpBinding` のフィールドをに `MessageEncoding` 設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
   * 次のオプションを実行して、基本的なHTTP認証を有効にします。タスク

      * AEM formsのユーザー名をフィールドに割り当てま `SignatureServiceClient.ClientCredentials.UserName.UserName`す。
      * 対応するパスワード値をフィールドに割り当てま `SignatureServiceClient.ClientCredentials.UserName.Password`す。
      * 定数値をフィールドに `HttpClientCredentialType.Basic` 割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
      * 定数値をフィールドに `BasicHttpSecurityMode.TransportCredentialOnly` 割り当てま `BasicHttpBindingSecurity.Security.Mode`す。

1. 削除する署名を含むPDFドキュメントを取得します

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、削除する電子署名が含まれるPDFドキュメントを保存するために使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、署名済みPDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトの内容を格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得す `System.IO.FileStream` ることで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出して、バイト配列にストリ `System.IO.FileStream` ームデータを入力 `Read` します。 読み取るバイト配列、開始位置およびストリーム長を渡します。
   * オブジェクトに `BLOB` バイト配列の内容を割り当 `MTOM` てて、オブジェクトにデータを入力します。

1. 署名フィールドからの電子署名の削除

   オブジェクトのメソッドを呼び出し、次 `SignatureServiceClient` の値を渡し `clearSignatureField` て、電子署名を削除します。

   * 署名済 `BLOB` みPDFドキュメントを含むオブジェクト。
   * 削除する電子署名が含まれる署名フィールドの名前を表すstring値です。
   電子署 `clearSignatureField` 名が削除さ `BLOB` れたPDFドキュメントを表すオブジェクトを返します。

1. PDFファイルとしてPDFドキュメントを保存します

   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、空の署名フィールドと、ファイルを開くモードを含むPDFドキュメントーのファイルの場所を表すstring値を渡します。
   * メソッドによって返されたオブジェクトの内容を `BLOB` 格納するバイト配列を作成し `sign` ます。 オブジェクトのデータメンバーの値を取得して、バ `BLOB` イト配列を設 `MTOM` 定します。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡すことによって、バ `System.IO.BinaryWriter` イト配列の内 `Write` 容をPDFファイルに書き込みます。

**関連トピック**

[電子署名の削除](digitally-signing-certifying-documents.md#removing-digital-signatures)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
