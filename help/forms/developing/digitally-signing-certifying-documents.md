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


# デジタル署名と認証ドキュメント{#digitally-signing-and-certifying-documents}

**Signatureサービスについて**

Signatureサービスを使用すると、組織は、配布および受信するAdobe PDFドキュメントのセキュリティとプライバシーを保護できます。 このサービスでは、電子署名と認証を使用して、意図した受信者だけがドキュメントを変更できるようにします。 セキュリティ機能はドキュメント自体に適用されるので、ドキュメントはライフサイクル全体にわたって安全で制御された状態を保ちます。 ドキュメントは、ファイアウォールの外部、オフラインでダウンロードされた場合、および組織に送り返された場合に、セキュリティで保護された状態のままとなります。

>[!NOTE]
>
>PDFドキュメントへの署名など、特定の操作が呼び出されたときに呼び出されるSignatureサービス用のカスタム署名ハンドラーを作成できます。

**署名フィールド名**

一部のSignatureサービス操作では、操作を実行する署名フィールドの名前を指定する必要があります。 例えば、PDFドキュメントに署名する場合、署名する署名フィールドの名前を指定します。 署名フィールドのフルネームが`form1[0].Form1[0].SignatureField1[0]`であるとします。 `form1[0].Form1[0].SignatureField1[0]`の代わりに`SignatureField1[0]`を指定できます。

競合が原因でSignatureサービスが誤ったフィールドに署名する（または、署名フィールド名を必要とする別の操作を実行する）場合があります。 この競合は、同じPDFドキュメント内の複数の場所に`SignatureField1[0]`という名前が表示された結果です。 例えば、`form1[0].Form1[0].SignatureField1[0]`と`form1[0].Form1[0].SubForm1[0].SignatureField1[0]`という2つの署名フィールドが含まれるPDFドキュメントで、`SignatureField1[0]`を指定したとします。 この場合、Signatureサービスは、ドキュメント内のすべての署名フィールドを反復する際に、検出された最初の署名フィールドに署名します。

1つのPDFドキュメント内に複数の署名フィールドがある場合は、署名フィールドの完全な名前を指定することをお勧めします。 つまり、`SignatureField1[0]`の代わりに`form1[0].Form1[0].SignatureField1[0]`を指定します。

Signatureサービスを使用して、次のタスクを実行できます。

* PDFドキュメント追加の電子署名フィールドを削除します。 （「[署名フィールドの追加](digitally-signing-certifying-documents.md#adding-signature-fields)」を参照）。
* PDFドキュメント内の署名フィールドの名前を取得します。 （[署名フィールド名の取得](digitally-signing-certifying-documents.md#retrieving-signature-field-names)を参照）。
* 署名フィールドを変更します。 （「[署名フィールドの変更](digitally-signing-certifying-documents.md#modifying-signature-fields)」を参照）。
* PDFドキュメントへのデジタル署名。 (「[PDFドキュメントのデジタル署名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)」を参照)。
* PDFドキュメントを認証します。 ([PDFドキュメントの認証](digitally-signing-certifying-documents.md#certifying-pdf-documents)を参照)。
* PDFドキュメント内の電子署名を検証します。 （[電子署名の検証](digitally-signing-certifying-documents.md#verifying-digital-signatures)を参照）。
* PDFドキュメント内のすべての電子署名を検証します。 （[複数のデジタル署名の検証](digitally-signing-certifying-documents.md#verifying-digital-signatures)を参照）。
* 署名フィールドから電子署名を削除します。 （「[電子署名の削除](digitally-signing-certifying-documents.md#removing-digital-signatures)」を参照）。

>[!NOTE]
>
>Signatureサービスについて詳しくは、「[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)」を参照してください。

## 署名フィールドの追加{#adding-signature-fields}

電子署名は、署名のグラフィック表現を含むフォームフィールドである署名フィールドに表示されます。 署名フィールドは、表示または非表示に設定することができます。署名者は、既存の署名フィールドを使用することも、プログラムを使用して署名フィールドを追加することもできます。 どちらの場合においても、PDF ドキュメントに署名できるようにするには、署名フィールドが存在している必要があります。

プログラムによって署名フィールドを追加するには、Signature サービス Java API や 署名 Web サービス API を使用します。1つのPDFドキュメントに複数の署名フィールドを追加できます。ただし、各署名フィールド名は一意である必要があります。

>[!NOTE]
>
>一部のPDFドキュメントタイプでは、プログラムによって署名フィールドを追加できません。 Signatureサービスと署名フィールドの追加について詳しくは、『[AEM Forms向けサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順{#summary-of-steps}の概要

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

SignatureサービスがPDFドキュメントに署名フィールドを追加した後、ドキュメントをPDFファイルとして保存し、AcrobatまたはAdobe Readerで開くことができるようにすることができます。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDFドキュメントへのデジタル署名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### Java API &lt;a0追加/>を使用した署名フィールド{#add-signature-fields-using-the-java-api}

署名API追加 (Java)を使用した署名フィールド：

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-signatures-client.jarなどのクライアントJARファイルを含めます。

1. 署名クライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `SignatureServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 署名フィールドが追加されたPDFドキュメントの取得

   * 署名フィールドの追加先のPDFドキュメントを表す`java.io.FileInputStream`オブジェクトを作成します。そのためには、コンストラクターを使用し、PDFドキュメントの場所を指定する文字列値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 追加署名フィールド

   * コンストラクターを使用して、署名フィールドの場所を指定する`PositionRectangle`オブジェクトを作成します。 コンストラクタ内で、座標値を指定します。
   * 必要に応じて、電子署名が署名フィールドに適用されたときにロックされるフィールドを指定する`FieldMDPOptions`オブジェクトを作成します。
   * 追加`SignatureServiceClient`オブジェクトの`addSignatureField`メソッドを呼び出し、次の値を渡すことによって、PDFドキュメントに署名フィールドを挿入します。

      * A `com.adobe.idp`. `Document` 署名フィールドを追加するPDFドキュメントを表すオブジェクトです。
      * 署名フィールドの名前を指定するstring値です。
      * 署名フィールドを追加するページ番号を表す`java.lang.Integer`値です。
      * 署名フィールドの場所を指定する`PositionRectangle`オブジェクトです。
      * 電子署名が署名フィールドに適用された後にロックされるPDFドキュメントのフィールドを指定する`FieldMDPOptions`オブジェクトです。 このパラメーターの値はオプションで、`null`を渡すことができます。
   * 様々な実行時値を指定する`PDFSeedValueOptions`オブジェクト。 このパラメーターの値はオプションで、`null`を渡すことができます。

      `addSignatureField`メソッドは`com.adobe.idp`を返します。 `Document` 署名フィールドが含まれるPDFドキュメントを表すオブジェクトです。
   >[!NOTE]
   >
   >`SignatureServiceClient`オブジェクトの`addInvisibleSignatureField`メソッドを呼び出して、非表示の署名フィールドを追加できます。

1. PDFドキュメントをPDFファイルとして保存

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が .pdf であることを確認します。
   * `com.adobe.idp`を呼び出します。 `Document` オブジェクトの `copyToFile` メソッドを使用して、 `Document` オブジェクトの内容をファイルにコピーします。`com.adobe.idp`を使用していることを確認します。 `Document` メソッドによって返されたオブ `addSignatureField` ジェクト。

**関連トピック**

[SignatureサービスAPIのクイック開始](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

### web追加サービスAPI {#add-signature-fields-using-the-web-service-api}を使用した署名フィールド

署名API（Webサービス）を使用して署名フィールドを追加するには：

1. プロジェクトファイルを含める

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. 署名クライアントの作成

   * `SignatureServiceClient`オブジェクトを作成するには、そのデフォルトのコンストラクタを使用します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`SignatureServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに指定するstring値を渡します（例：`http://localhost:8080/soap/services/SignatureService?WSDL`）。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する場合に使用されます)。
   * `SignatureServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * AEM formsユーザー名をフィールド`SignatureServiceClient.ClientCredentials.UserName.UserName`に割り当てます。
      * 対応するパスワード値をフィールド`SignatureServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * 定数値`HttpClientCredentialType.Basic`をフィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に割り当てます。
      * 定数値`BasicHttpSecurityMode.TransportCredentialOnly`をフィールド`BasicHttpBindingSecurity.Security.Mode`に割り当てます。

1. 署名フィールドが追加されたPDFドキュメントの取得

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、署名フィールドを含むPDFドキュメントを保存するために使用します。
   * コンストラクターを呼び出し、PDFドキュメントーのファイルの場所とファイルを開くモードを表す文字列値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得して、バイト配列のサイズを決定できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * `BLOB`オブジェクトに`MTOM`プロパティを割り当て、バイト配列の内容を指定します。

1. 追加署名フィールド

   追加`SignatureServiceClient`オブジェクトの`addSignatureField`メソッドを呼び出し、次の値を渡すことによって、PDFドキュメントに署名フィールドを挿入します。

   * 署名フィールドを追加するPDFドキュメントを表す`BLOB`オブジェクトです。
   * 署名フィールド名を指定するstring値です。
   * 署名フィールドを追加するページ番号を表すinteger値です。
   * 署名フィールドの場所を指定する`PositionRect`オブジェクトです。
   * 電子署名が署名フィールドに適用された後にロックされるPDFドキュメントのフィールドを指定する`FieldMDPOptions`オブジェクトです。 このパラメーターの値はオプションで、`null`を渡すことができます。
   * 様々な実行時値を指定する`PDFSeedValueOptions`オブジェクト。 このパラメーターの値はオプションで、`null`を渡すことができます。

   `addSignatureField`メソッドは、署名フィールドを含むPDFドキュメントを表す`BLOB`オブジェクトを返します。

1. PDFドキュメントをPDFファイルとして保存

   * コンストラクターを呼び出し、署名フィールドとファイルを開くモードを含むPDFドキュメントのファイルの場所を表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `addSignatureField`メソッドから返された`BLOB`オブジェクトの内容を格納するバイト配列を作成します。 `BLOB`オブジェクトの`binaryData`データメンバの値を取得して、バイト配列を入力します。
   * コンストラクターを呼び出して`System.IO.FileStream`オブジェクトを渡し、`System.IO.BinaryWriter`オブジェクトを作成します。
   * `System.IO.BinaryWriter`オブジェクトの`Write`メソッドを呼び出し、バイト配列を渡すことで、バイト配列の内容をPDFファイルに書き込みます。

**関連トピック**

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 署名フィールド名の取得{#retrieving-signature-field-names}

署名または認証する PDF ドキュメント内のすべての署名フィールドの名前を取得できます。PDF ドキュメント内の署名フィールド名が分からない場合や、名前を検証したい場合に、プログラムによって名前を取得することができます。Signatureサービスは、`form1[0].grantApplication[0].page1[0].SignatureField1[0]`などの署名フィールドの完全修飾名を返します。

>[!NOTE]
>
>Signatureサービスについて詳しくは、[『AEM Forms用サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順{#summary_of_steps-1}の概要

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

これらのJARファイルの場所について詳しくは、「[AEM FormsJavaライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)」を参照してください。

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

### Java API {#retrieve-signature-field-names-using-the-java-api}を使用した署名フィールド名の取得

署名API(Java)を使用して署名フィールド名を取得します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-signatures-client.jarなどのクライアントJARファイルを含めます。

1. 署名クライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `SignatureServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 署名フィールドを含むPDFドキュメントの取得

   * 署名フィールドを含むPDFドキュメントを表す`java.io.FileInputStream`オブジェクトを作成します。そのためには、コンストラクターを使用し、PDFドキュメントの場所を指定する文字列値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 署名フィールド名の取得

   * `SignatureServiceClient`オブジェクトの`getSignatureFieldList`メソッドを呼び出し、署名フィールドを含むPDFドキュメントを含む`com.adobe.idp.Document`オブジェクトを渡して、署名フィールド名を取得します。 このメソッドは、`java.util.List`オブジェクトを返します。このオブジェクト内の各要素には`PDFSignatureField`オブジェクトが含まれます。 このオブジェクトを使用すると、署名フィールドが表示されているかどうかなど、署名フィールドに関する追加情報を取得できます。
   * `java.util.List`オブジェクトを繰り返し処理して、署名フィールド名があるかどうかを確認します。 PDFドキュメントの各署名フィールドに対して、個別の`PDFSignatureField`オブジェクトを取得できます。 署名フィールドの名前を取得するには、`PDFSignatureField`オブジェクトの`getName`メソッドを呼び出します。 このメソッドは、署名フィールド名を指定するstring値を返します。

**関連トピック**

[署名フィールド名の取得](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[クイック開始（SOAPモード）:Java APIを使用した署名フィールド名の取得](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-retrieving-signature-field-names-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#retrieve-signature-field-using-the-web-service-api}を使用して署名フィールドを取得する

署名API（Webサービス）を使用して署名フィールド名を取得します。

1. プロジェクトファイルを含める

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. 署名クライアントの作成

   * `SignatureServiceClient`オブジェクトを作成するには、そのデフォルトのコンストラクタを使用します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`SignatureServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに指定するstring値を渡します（例：`http://localhost:8080/soap/services/SignatureService?WSDL`）。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する場合に使用されます)。
   * `SignatureServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * AEM formsユーザー名をフィールド`SignatureServiceClient.ClientCredentials.UserName.UserName`に割り当てます。
      * 対応するパスワード値をフィールド`SignatureServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * 定数値`HttpClientCredentialType.Basic`をフィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に割り当てます。
      * 定数値`BasicHttpSecurityMode.TransportCredentialOnly`をフィールド`BasicHttpBindingSecurity.Security.Mode`に割り当てます。

1. 署名フィールドを含むPDFドキュメントの取得

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、署名フィールドを含むPDFドキュメントを保存するために使用します。
   * コンストラクターを呼び出し、PDFドキュメントーのファイルの場所とファイルを開くモードを表す文字列値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得して、バイト配列のサイズを決定できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * `BLOB`オブジェクトにバイト配列の内容を`MTOM`フィールドに割り当てて入力します。

1. 署名フィールド名の取得

   * `SignatureServiceClient`オブジェクトの`getSignatureFieldList`メソッドを呼び出し、署名フィールドを含むPDFドキュメントを含む`BLOB`オブジェクトを渡して、署名フィールド名を取得します。 このメソッドは、`MyArrayOfPDFSignatureField`コレクションオブジェクトを返します。各要素には`PDFSignatureField`オブジェクトが含まれます。
   * `MyArrayOfPDFSignatureField`オブジェクトを繰り返し処理して、署名フィールド名があるかどうかを判断します。 PDFドキュメントの各署名フィールドに対して、`PDFSignatureField`オブジェクトを取得できます。 署名フィールドの名前を取得するには、`PDFSignatureField`オブジェクトの`getName`メソッドを呼び出します。 このメソッドは、署名フィールド名を指定するstring値を返します。

**関連トピック**

[署名フィールド名の取得](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 署名フィールドの変更{#modifying-signature-fields}

Java APIとWebサービスAPIを使用して、PDFドキュメント内の署名フィールドを変更できます。 署名フィールドの署名フィールドロックディクショナリまたはシード値ディクショナリの値を操作することで署名フィールドを変更します。

*フィールドロックディクショナリ*&#x200B;は、署名フィールドが署名されたときにロックされるフィールドのリストを指定します。 フィールドがロックされると、ユーザーはフィールドを変更できません。*シード値ディクショナリ*&#x200B;には、署名の適用時に使用される制約情報が含まれています。 例えば、署名を無効にすることなく実行できるアクションを制御する権限設定を変更することができます。

既存の署名フィールドを変更すると、PDFドキュメントに変更を加え、ビジネス要件の変更を反映させることができます。 例えば、新しいビジネス要件では、ドキュメントの署名後にすべてのドキュメントフィールドのロックが必要になる場合があります。

この節では、フィールドロックディクショナリとシード値ディクショナリの両方の値を変更して、署名フィールドを変更する方法について説明します。 署名フィールドロックディクショナリに変更を加えると、署名フィールドへの署名時に、PDFドキュメント内のすべてのフィールドがロックされます。 シード値ディクショナリに変更を加えると、ドキュメントに対する特定の種類の変更が禁止されます。

>[!NOTE]
>
>Signatureサービスと署名フィールドの変更について詳しくは、『[AEM Forms向けサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順{#summary_of_steps-2}の概要

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

これらのJARファイルの場所について詳しくは、「[LiveCycleJavaライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)」を参照してください。

**署名クライアントの作成**

プログラムを使用してSignatureサービスの操作を実行する前に、Signatureサービスクライアントを作成する必要があります。

**変更する署名フィールドが含まれているPDFドキュメントの取得**

変更する署名フィールドが含まれているPDFドキュメントを取得します。

**ディクショナリ値の設定**

署名フィールドを変更するには、フィールドロックディクショナリまたはシード値ディクショナリに値を割り当てます。 署名フィールドロックディクショナリ値を指定するには、ドキュメントフィールドの署名時にロックされるPDF署名フィールドを指定する必要があります。 （この節では、すべてのフィールドをロックする方法について説明します）。

次のシード値ディクショナリ値を設定できます。

* **リビジョンの確認**:署名フィールドに署名が適用された場合に失効確認を実行するかどうかを指定します。
* **証明書のオプション**:証明書のシード値ディクショナリに値を割り当てます。証明書のオプションを指定する前に、証明書のシード値ディクショナリについて理解することをお勧めします。 （「[PDFリファレンス](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf)」を参照）。
* **ダイジェストオプション**:署名に使用するダイジェストアルゴリズムを割り当てます。有効な値はSHA1、SHA256、SHA384、SHA512およびRIPEMD160です。
* **フィルタ**:署名フィールドで使用するフィルターを指定します。例えば、Adobe.PPKLiteフィルターを使用できます。 （「[PDFリファレンス](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf)」を参照）。
* **フラグのオプション**:この署名フィールドに関連付けられているフラグ値を指定します。値が1の場合、署名者は指定された値のみをエントリに使用する必要があります。 値が0の場合、他の値も許可されます。 ビット位置は次のとおりです。

   * **1(Filter)：署名フィ** ールドへの署名に使用する署名ハンドラーです
   * **2(SubFilter)：署名時** に使用する有効なエンコーディングを示す名前の配列
   * **3(V)**:署名フィールドへの署名に使用する署名ハンドラーの必要最小限のバージョン番号です
   * **4(Reasons):ドキュメント** に署名する理由を指定する文字列の配列です
   * **5(PDFLegalWarnings)：考えら** れる法的証明を指定する文字列の配列です

* **法的証明**:ドキュメントを認証すると、ドキュメントの表示されるコンテンツをあいまいにしたり誤解を招く可能性のある、特定の種類のコンテンツを自動的にスキャンします。例えば、注釈によって、認証対象を把握するために重要なテキストが隠される場合があります。 スキャン処理では、この種類のコンテンツの存在を示す警告が生成されます。 また、警告を生成した可能性のあるコンテンツに関する追加の説明も提供します。
* **権限**:署名を無効にすることなく、PDFドキュメントで使用できる権限を指定します。
* **理由**:このドキュメントに署名が必要な理由を指定します。
* **タイムスタンプ**:タイムスタンプオプションを指定します。例えば、使用するタイムスタンプサーバーのURLを設定できます。
* **バージョン**:署名フィールドへの署名に使用する署名ハンドラーの最小バージョン番号を指定します。

**署名フィールドの変更**

Signatureサービスクライアントを作成した後、変更する署名フィールドを含むPDFドキュメントを取得し、Dictionary値を設定した後、Signatureサービスに対して署名フィールドを変更するよう指示できます。 次に、Signatureサービスは、変更された署名フィールドを含むPDFドキュメントを返します。 元のPDFドキュメントは影響を受けません。

**PDFドキュメントをPDFファイルとして保存**

変更した署名フィールドを含むPDFドキュメントをPDFファイルとして保存し、ユーザーがAcrobatまたはAdobe Readerで開けるようにします。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[SignatureサービスAPIのクイック開始](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

[PDFドキュメントへのデジタル署名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### Java API {#modify-signature-fields-using-the-java-api}を使用した署名フィールドの変更

署名API (Java)を使用して署名フィールドを変更します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-signatures-client.jarなどのクライアントJARファイルを含めます。

1. 署名クライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `SignatureServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 変更する署名フィールドが含まれているPDFドキュメントの取得

   * コンストラクターを使用し、PDFドキュメントの場所を指定する文字列値を渡して、変更する署名フィールドを含むPDFドキュメントを表す`java.io.FileInputStream`オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. ディクショナリ値の設定

   * コンストラクタを使用して `PDFSignatureFieldProperties` オブジェクトを作成します。`PDFSignatureFieldProperties`オブジェクトは、署名フィールドロックディクショナリとシード値ディクショナリ情報を格納します。
   * コンストラクタを使用して `PDFSeedValueOptionSpec` オブジェクトを作成します。このオブジェクトを使用すると、シード値ディクショナリの値を設定できます。
   * `PDFSeedValueOptionSpec`オブジェクトの`setMdpValue`メソッドを呼び出し、`MDPPermissions.NoChanges`定義済みリスト値を渡すことで、PDFドキュメントの変更を許可しない。
   * コンストラクタを使用して `FieldMDPOptionSpec` オブジェクトを作成します。このオブジェクトを使用すると、署名フィールドロックディクショナリの値を設定できます。
   * `FieldMDPOptionSpec`オブジェクトの`setMdpValue`メソッドを呼び出し、`FieldMDPAction.ALL`定義済みリスト値を渡すことで、PDFドキュメント内のすべてのフィールドをロックします。
   * `PDFSignatureFieldProperties`オブジェクトの`setSeedValue`メソッドを呼び出し、`PDFSeedValueOptionSpec`オブジェクトを渡して、シード値ディクショナリ情報を設定します。
   * `PDFSignatureFieldProperties`オブジェクトの`setFieldMDP`メソッドを呼び出し、`FieldMDPOptionSpec`オブジェクトを渡して、署名フィールドロックディクショナリ情報を設定します。

   >[!NOTE]
   >
   >設定可能なシード値ディクショナリの値をすべて表示するには、`PDFSeedValueOptionSpec`クラス参照を参照してください。 (「[AEM FormsAPIリファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)」を参照)。

1. 署名フィールドの変更

   `SignatureServiceClient`オブジェクトの`modifySignatureField`メソッドを呼び出し、次の値を渡して、署名フィールドを変更します。

   * 変更する署名フィールドを含むPDFドキュメントを格納する`com.adobe.idp.Document`オブジェクトです
   * 署名フィールドの名前を指定するstring値です
   * 署名フィールドロックディクショナリとシード値ディクショナリ情報を格納する`PDFSignatureFieldProperties`オブジェクト

   `modifySignatureField`メソッドは、変更された署名フィールドを含むPDFドキュメントを格納する`com.adobe.idp.Document`オブジェクトを返します。

1. PDFドキュメントをPDFファイルとして保存

   * `java.io.File`オブジェクトを作成し、ファイル名の拡張子が.pdfであることを確認します。
   * `com.adobe.idp.Document`オブジェクトの`copyToFile`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトの内容をファイルにコピーします。 `modifySignatureField`メソッドが返した`com.adobe.idp.Document`オブジェクトを使用していることを確認してください。

### WebサービスAPI {#modify-signature-fields-using-the-web-service-api}を使用して署名フィールドを変更する

Signature API（Webサービス）を使用して署名フィールドを変更します。

1. プロジェクトファイルを含める

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. 署名クライアントの作成

   * `SignatureServiceClient`オブジェクトを作成するには、そのデフォルトのコンストラクタを使用します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`SignatureServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに指定するstring値を渡します（例：`http://localhost:8080/soap/services/SignatureService?WSDL`）。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する場合に使用されます)。
   * `SignatureServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * AEM formsユーザー名をフィールド`SignatureServiceClient.ClientCredentials.UserName.UserName`に割り当てます。
      * 対応するパスワード値をフィールド`SignatureServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * 定数値`HttpClientCredentialType.Basic`をフィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に割り当てます。
      * 定数値`BasicHttpSecurityMode.TransportCredentialOnly`をフィールド`BasicHttpBindingSecurity.Security.Mode`に割り当てます。

1. 変更する署名フィールドが含まれているPDFドキュメントの取得

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、変更する署名フィールドを含むPDFドキュメントを保存するために使用します。
   * コンストラクターを呼び出し、PDFドキュメントーのファイルの場所とファイルを開くモードを表す文字列値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得して、バイト配列のサイズを決定できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * `BLOB`オブジェクトに、`MTOM`プロパティにバイト配列の内容を割り当てて入力します。

1. ディクショナリ値の設定

   * コンストラクタを使用して `PDFSignatureFieldProperties` オブジェクトを作成します。このオブジェクトは、署名フィールドロックディクショナリとシード値ディクショナリの情報を格納します。
   * コンストラクタを使用して `PDFSeedValueOptionSpec` オブジェクトを作成します。このオブジェクトを使用すると、シード値ディクショナリの値を設定できます。
   * `MDPPermissions.NoChanges`定義済みリスト値を`PDFSeedValueOptionSpec`オブジェクトの`mdpValue`データメンバに割り当てて、PDFドキュメントの変更を許可しない。
   * コンストラクタを使用して `FieldMDPOptionSpec` オブジェクトを作成します。このオブジェクトを使用すると、署名フィールドロックディクショナリの値を設定できます。
   * `FieldMDPAction.ALL`定義済みリスト値を`FieldMDPOptionSpec`オブジェクトの`mdpValue`データメンバに割り当てて、PDFドキュメント内のすべてのフィールドをロックします。
   * シード値ディクショナリ情報を設定するには、`PDFSeedValueOptionSpec`オブジェクトを`PDFSignatureFieldProperties`オブジェクトの`seedValue`データメンバに割り当てます。
   * `FieldMDPOptionSpec`オブジェクトを`PDFSignatureFieldProperties`オブジェクトの`fieldMDP`データメンバに割り当てて、署名フィールドロックディクショナリ情報を設定します。

   >[!NOTE]
   >
   >設定可能なシード値ディクショナリの値をすべて表示するには、`PDFSeedValueOptionSpec`クラス参照を参照してください。 (「[AEM FormsAPIリファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)」を参照)。

1. 署名フィールドの変更

   `SignatureServiceClient`オブジェクトの`modifySignatureField`メソッドを呼び出し、次の値を渡して、署名フィールドを変更します。

   * 変更する署名フィールドを含むPDFドキュメントを格納する`BLOB`オブジェクトです
   * 署名フィールドの名前を指定するstring値です
   * 署名フィールドロックディクショナリとシード値ディクショナリ情報を格納する`PDFSignatureFieldProperties`オブジェクト

   `modifySignatureField`メソッドは、変更された署名フィールドを含むPDFドキュメントを格納する`BLOB`オブジェクトを返します。

1. PDFドキュメントをPDFファイルとして保存

   * コンストラクターを呼び出し、署名フィールドを含むPDFドキュメントのファイルの場所、およびファイルを開くモードを表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `addSignatureField`メソッドが返す`BLOB`オブジェクトの内容を格納するバイト配列を作成します。 `BLOB`オブジェクトの`MTOM`データメンバの値を取得して、バイト配列を入力します。
   * コンストラクターを呼び出して`System.IO.FileStream`オブジェクトを渡し、`System.IO.BinaryWriter`オブジェクトを作成します。
   * `System.IO.BinaryWriter`オブジェクトの`Write`メソッドを呼び出し、バイト配列を渡すことで、バイト配列の内容をPDFファイルに書き込みます。

**関連トピック**

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## PDFドキュメントへのデジタル署名{#digitally-signing-pdf-documents}

セキュリティレベルの提供のため、PDF に電子署名を適用することができます。手書き署名のような電子署名は、署名者を識別したり、ドキュメントに関するステートメントを作成する手段として使用できます。ドキュメントの電子署名に使用されている技術は、署名者と受信者の両方が、何に署名されているのかを明確にし、その署名によりドキュメントに変更がないことを確認するのに役立ちます。

PDF ドキュメントは、公開鍵を用いて署名されます。署名者は公開鍵と秘密鍵の 2 つの鍵を持っています。秘密鍵はユーザーの秘密鍵証明書に保存されます。この資格情報は署名時に使用可能にする必要があります。 公開鍵はユーザーの証明書に保存されます。受信者が署名を検証するには、この証明書を使用できる必要があります。 失効した証明書に関する情報は、認証機関から配布される証明書失効リスト（CRL）およびオンライン証明書ステータスプロトコル（OCSP）応答内にあります。署名が行われた時間は、タイムスタンプ局として知られる信頼できるソースから取得されます。

>[!NOTE]
>
>PDFドキュメントに電子署名する前に、証明書がAEM Formsに追加されていることを確認する必要があります。 証明書は、管理コンソールを使用して、またはTrust Manager APIをプログラムで使用して追加します。 （「[Trust Manager APIを使用した秘密鍵証明書の読み込み](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api)」を参照）。

PDFドキュメントにプログラムによってデジタル署名を行うことができます。 PDFドキュメントに電子署名する場合は、AEM Formsに存在するセキュリティ証明書を参照する必要があります。 証明書は署名に使用する秘密鍵となります。

Signatureサービスは、PDFドキュメントが署名されるときに次の手順を実行します。

1. Signatureサービスは、要求で指定されたエイリアスを渡すことで、Truststoreから秘密鍵証明書を取得します。
1. Truststoreは、指定した秘密鍵証明書を検索します。
1. 秘密鍵証明書がSignatureサービスに返され、ドキュメントへの署名に使用されます。 証明書は、後で要求を行う場合にエイリアスに対してもキャッシュされます。

セキュリティ証明書の処理について詳しくは、使用しているアプリケーションサーバー版の『*AEM Formsのインストールと展開*』ガイドを参照してください。

>[!NOTE]
>
>署名ドキュメントと認証ユーザーには違いがあります。 ([PDFドキュメントの認証](digitally-signing-certifying-documents.md#certifying-pdf-documents)を参照)。

>[!NOTE]
>
>PDFドキュメントによっては、署名がサポートされていない場合があります。 Signatureサービスとデジタル署名ドキュメントの詳細については、『[AEM Forms向けサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

>[!NOTE]
>
>Signatureサービスは、ドキュメントの認証など、操作への入力としてPDFデータが埋め込まれたXDPファイルをサポートしません。 この操作により、Signatureサービスは`PDFOperationException`をスローします。 この問題を解決するには、PDF Utilitiesサービスを使用してXDPファイルをPDFファイルに変換し、変換したPDFファイルをSignatureサービス操作に渡します。 （「[PDFユーティリティの操作](/help/forms/developing/pdf-utilities.md#working-with-pdf-utilities)」を参照）。

**nCipher nShield HSM秘密鍵証明書**

PDFドキュメントの署名や認証にnCipher nShield HSM秘密鍵証明書を使用する場合、AEM FormsがデプロイされているJ2EEアプリケーションサーバーを再起動するまで、新しい秘密鍵証明書は使用できません。 ただし、設定値を設定すると、J2EEアプリケーションサーバーを再起動しなくても、署名または認証の操作が動作します。

次の設定値をcknfastrcファイルに追加できます。このファイルは/opt/nfast/cknfastrc(またはc:\nfast\cknfastrc)にあります。

```shell
    CKNFAST_ASSUME_SINGLE_PROCESS=0
```

この設定値をcknfastrcファイルに追加すると、J2EEアプリケーションサーバーを再起動しなくても、新しい秘密鍵証明書を使用できます。

**署名は信頼されていません**

同じPDFドキュメントの認証および署名時に、認証署名が信頼されていない場合、AcrobatまたはAdobe ReaderでPDFドキュメントを開くときに、最初の署名に対して黄色い三角形が表示されます。 この状況を回避するには、認証署名を信頼する必要があります。

**XFAベースのフォームである署名ドキュメント**

SignatureサービスAPIを使用してXFAベースのフォームに署名しようとすると、Acrobatにある`View` `Signed` `Version`にデータがない可能性があります。 例えば、次のワークフローを考えてみましょう。

* Designerを使用して作成したXDPファイルを使用して、署名フィールドを含むフォームデザインと、フォームデータを含むXMLデータを結合します。 インタラクティブPDFドキュメントを生成するには、Formsサービスを使用します。
* SignatureサービスAPIを使用してPDFドキュメントに署名します。

### 手順{#summary_of_steps-3}の概要

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

PDFドキュメントに署名する場合、Signatureサービスで使用する実行時オプションを設定できます。 以下のオプションを設定できます。

* 外観オプション
* 失効確認
* タイムスタンプ値

`PDFSignatureAppearanceOptionSpec`オブジェクトを使用して外観のオプションを設定します。 例えば、`PDFSignatureAppearanceOptionSpec`オブジェクトの`setShowDate`メソッドを呼び出して`true`を渡すことで、署名内に日付を表示できます。

PDFドキュメントのデジタル署名に使用される証明書が失効したかどうかを判定する失効確認を実行するかどうかを指定することもできます。 失効確認を実行するには、次のいずれかの値を指定します。

* **NoCheck**:失効確認を実行しません。
* **BestEffort**:常に、チェーン内のすべての証明書の失効を確認しようとします。チェックで何らかの問題が発生した場合、失効は有効であると見なされます。 エラーが発生した場合は、証明書が失効していないと想定します。
* **CheckIfAvailable：失効情報が利用可能な場合に、チェーン内のすべての証明書の失効を** 確認します。チェックで問題が発生した場合、失効は無効であると見なされます。 エラーが発生した場合は、証明書が失効し、無効であると仮定します。 （これがデフォルト値です）。
* **AlwaysCheck**:チェーン内のすべての証明書の失効を確認します。どの証明書にも失効情報が存在しない場合、失効は無効であると見なされます。

証明書に対して失効確認を実行するには、`CRLOptionSpec`オブジェクトを使用して、証明書失効リスト(CRL)サーバーへのURLを指定します。 ただし、失効確認を実行する場合で、CRLサーバーへのURLを指定しない場合は、Signatureサービスは証明書からURLを取得します。

失効確認を実行する際は、CRLサーバーを使用する代わりに、オンライン証明書ステータスプロトコル(OCSP)サーバーを使用できます。 通常、CRLサーバーとは異なり、OCSPサーバーを使用する場合は、失効確認の実行が高速になります。 ([https://tools.ietf.org/html/rfc2560](https://tools.ietf.org/html/rfc2560)の「Online Certificate Status Protocol」を参照)。

SignatureサービスでAdobeのアプリケーションおよびサービスを使用するCRLおよびOCSPサーバーの順序を設定できます。 例えば、「Adobeアプリケーションおよびサービス」でOCSPサーバーを最初に設定した場合、OCSPサーバーを確認し、次にCRLサーバーを確認します。 （AACヘルプの「Trust Storeを使用した証明書と秘密鍵証明書の管理」を参照）。

失効確認を実行しないように指定した場合、Signatureサービスは、ドキュメントの署名または認証に使用された証明書が失効したかどうかを確認しません。 つまり、CRLおよびOCSPサーバー情報は無視されます。

>[!NOTE]
>
>証明書にはCRLまたはOCSPサーバーが指定されている場合がありますが、`CRLOptionSpec`および`OCSPOptionSpec`オブジェクトを使用して、証明書で指定されているURLを上書きできます。 例えば、CRLサーバーを上書きするには、`CRLOptionSpec`オブジェクトの`setLocalURI`メソッドを呼び出します。

タイムスタンプとは、署名済みまたは認証済みのドキュメントが変更された時間を追跡するプロセスを指します。 ドキュメントの署名後は、ドキュメントの所有者によっても、署名を変更しないでください。 タイムスタンプ機能を使用すると、署名済みまたは認証済みのドキュメントの有効性を強化できます。 `TSPOptionSpec`オブジェクトを使用して、タイムスタンプオプションを設定できます。 例えば、タイムスタンププロバイダー(TSP)サーバーのURLを指定できます。

>[!NOTE]
>
>JavaおよびWebサービスのセクションや対応するクイック開始のウォークスルーでは、失効確認が使用されます。 CRLまたはOCSPサーバー情報が指定されていないので、サーバー情報は、PDFドキュメントのデジタル署名に使用される証明書から取得されます。

PDFドキュメントに正しく署名するには、`form1[0].#subform[1].SignatureField3[3]`など、電子署名を含む署名フィールドの完全修飾名を指定します。 XFAフォームフィールドを使用する場合は、署名フィールドの名前の一部を使用することもできます。`SignatureField3[3]`.

また、PDFドキュメントに電子署名するためのセキュリティ証明書を参照する必要もあります。 セキュリティ証明書を参照するには、エイリアスを指定します。 エイリアスは、PKCS#12ファイル（拡張子.pfx付き）またはハードウェアセキュリティモジュール(HSM)内の実際の秘密鍵証明書への参照です。 セキュリティ証明書について詳しくは、使用しているアプリケーションサーバー版の『*AEM Forms*&#x200B;のインストールおよびデプロイ』ガイドを参照してください。

**署名済みPDFドキュメントの保存**

SignatureサービスがPDFドキュメントに電子署名した後、その画像をPDFファイルとして保存して、ユーザーがAcrobatまたはAdobe Readerで開けるようにすることができます。

**関連トピック**

[Java APIを使用したPDFドキュメントへのデジタル署名](digitally-signing-certifying-documents.md#digitally-sign-pdf-documents-using-the-java-api)

[WebサービスAPIを使用したPDFドキュメントへのデジタル署名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[署名フィールドの追加](digitally-signing-certifying-documents.md#adding-signature-fields)

[署名フィールド名の取得](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

### Java API {#digitally-sign-pdf-documents-using-the-java-api}を使用したPDFドキュメントへのデジタル署名

署名API(Java)を使用してPDFドキュメントに電子署名する：

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-signatures-client.jarなどのクライアントJARファイルを含めます。

1. Signaturesクライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `SignatureServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. PDFドキュメントに署名を依頼する

   * コンストラクターを使用し、PDFドキュメントの場所を指定する文字列値を渡して、デジタル署名するPDFドキュメントを表す`java.io.FileInputStream`オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PDFドキュメントへの署名

   `SignatureServiceClient`オブジェクトの`sign`メソッドを呼び出し、次の値を渡して、PDFドキュメントに署名します。

   * 署名するPDFドキュメントを表す`com.adobe.idp.Document`オブジェクトです。
   * 電子署名を含む署名フィールドの名前を表すstring値です。
   * PDFドキュメントのデジタル署名に使用される秘密鍵証明書を表す`Credential`オブジェクトです。 `Credential`オブジェクトの静的な`getInstance`メソッドを呼び出し、セキュリティ証明書に対応するエイリアス値を指定する文字列値を渡して、`Credential`オブジェクトを作成します。
   * PDFドキュメントのダイジェストの作成に使用するハッシュアルゴリズムを表す静的データメンバーを指定する`HashAlgorithm`オブジェクトです。 例えば、`HashAlgorithm.SHA1`にSHA1アルゴリズムを使用するよう指定できます。
   * PDFドキュメントがデジタル署名された理由を表すstring値です。
   * 署名者の連絡先情報を表すstring値です。
   * 電子署名の外観を制御する`PDFSignatureAppearanceOptions`オブジェクトです。 例えば、このオブジェクトを使用して、電子署名にカスタムロゴを追加できます。
   * 署名者の証明書に対して失効確認を実行するかどうかを指定する`java.lang.Boolean`オブジェクトです。
   * オンライン証明書ステータスプロトコル(OCSP)サポートの環境設定を格納する`OCSPOptionSpec`オブジェクトです。 失効確認が実行されない場合、このパラメーターは使用されず、`null`を指定できます。
   * 証明書失効リスト(CRL)の環境設定を格納する`CRLPreferences`オブジェクトです。 失効確認が実行されない場合、このパラメーターは使用されず、`null`を指定できます。
   * タイムスタンププロバイダー(TSP)サポートの環境設定を格納する`TSPPreferences`オブジェクトです。 このパラメーターはオプションで、`null`にすることができます。 詳しくは、[AEM FormsAPIリファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)を参照してください。

   `sign`メソッドは、署名済みPDFドキュメントを表す`com.adobe.idp.Document`オブジェクトを返します。

1. 署名済みPDFドキュメントの保存

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が .pdf であることを確認します。
   * `com.adobe.idp.Document`オブジェクトの`copyToFile`メソッドを呼び出し、`java.io.File`を渡して`Document`オブジェクトの内容をファイルにコピーします。 `com.adobe.idp.Document` メソッドから返された `sign` オブジェクトを必ず使用してください。

**関連トピック**

[PDFドキュメントへのデジタル署名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[クイック開始（SOAPモード）:Java APIを使用したPDFドキュメントへのデジタル署名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#digitally-signing-pdf-documents-using-the-web-service-api}を使用したPDFドキュメントへのデジタル署名

Signature API（Webサービス）を使用してPDFドキュメントに電子署名するには：

1. プロジェクトファイルを含める

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. Signaturesクライアントの作成

   * `SignatureServiceClient`オブジェクトを作成するには、そのデフォルトのコンストラクタを使用します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`SignatureServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに指定するstring値を渡します（例：`http://localhost:8080/soap/services/SignatureService?WSDL`）。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する場合に使用されます)。
   * `SignatureServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * AEM formsユーザー名をフィールド`SignatureServiceClient.ClientCredentials.UserName.UserName`に割り当てます。
      * 対応するパスワード値をフィールド`SignatureServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * 定数値`HttpClientCredentialType.Basic`をフィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に割り当てます。
      * 定数値`BasicHttpSecurityMode.TransportCredentialOnly`をフィールド`BasicHttpBindingSecurity.Security.Mode`に割り当てます。

1. PDFドキュメントに署名を依頼する

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、署名されたPDFドキュメントの保存に使用されます。
   * コンストラクターを呼び出し、署名するPDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得して、バイト配列のサイズを決定できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * `BLOB`オブジェクトに、`MTOM`プロパティにバイト配列の内容を割り当てて入力します。

1. PDFドキュメントへの署名

   `SignatureServiceClient`オブジェクトの`sign`メソッドを呼び出し、次の値を渡して、PDFドキュメントに署名します。

   * 署名するPDFドキュメントを表す`BLOB`オブジェクトです。
   * 電子署名を含む署名フィールドの名前を表すstring値です。
   * PDFドキュメントのデジタル署名に使用される秘密鍵証明書を表す`Credential`オブジェクトです。 `Credential`オブジェクトを作成するには、コンストラクターを使用します。また、`Credential`オブジェクトの`alias`プロパティに値を割り当ててエイリアスを指定します。
   * PDFドキュメントのダイジェストの作成に使用するハッシュアルゴリズムを表す静的データメンバーを指定する`HashAlgorithm`オブジェクトです。 例えば、`HashAlgorithm.SHA1`にSHA1アルゴリズムを使用するよう指定できます。
   * ハッシュアルゴリズムを使用するかどうかを指定するBoolean値です。
   * PDFドキュメントがデジタル署名された理由を表すstring値です。
   * 署名者の場所を表すstring値です。
   * 署名者の連絡先情報を表すstring値です。
   * 電子署名の外観を制御する`PDFSignatureAppearanceOptions`オブジェクトです。 例えば、このオブジェクトを使用して、電子署名にカスタムロゴを追加できます。
   * 署名者の証明書に対して失効確認を実行するかどうかを指定する`System.Boolean`オブジェクトです。 この失効確認が行われると、署名に埋め込まれます。 デフォルトは、`false` です。
   * オンライン証明書ステータスプロトコル(OCSP)サポートの環境設定を格納する`OCSPOptionSpec`オブジェクトです。 失効確認が実行されない場合、このパラメーターは使用されず、`null`を指定できます。 このオブジェクトについて詳しくは、[AEM FormsAPIリファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)を参照してください。
   * 証明書失効リスト(CRL)の環境設定を格納する`CRLPreferences`オブジェクトです。 失効確認が実行されない場合、このパラメーターは使用されず、`null`を指定できます。
   * タイムスタンププロバイダー(TSP)サポートの環境設定を格納する`TSPPreferences`オブジェクトです。 このパラメーターはオプションで、`null`にすることができます。

   `sign`メソッドは、署名済みPDFドキュメントを表す`BLOB`オブジェクトを返します。

1. 署名済みPDFドキュメントの保存

   * コンストラクターを呼び出して、`System.IO.FileStream`オブジェクトを作成します。 署名済みPDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * `sign`メソッドから返された`BLOB`オブジェクトの内容を格納するバイト配列を作成します。 `BLOB`オブジェクトの`MTOM`データメンバの値を取得して、バイト配列を入力します。
   * コンストラクターを呼び出して`System.IO.FileStream`オブジェクトを渡し、`System.IO.BinaryWriter`オブジェクトを作成します。
   * `System.IO.BinaryWriter`オブジェクトの`Write`メソッドを呼び出し、バイト配列を渡すことで、バイト配列の内容をPDFファイルに書き込みます。

**関連トピック**

[PDFドキュメントへのデジタル署名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## デジタル署名インタラクティブForms{#digitally-signing-interactive-forms}

Formsサービスが作成するインタラクティブフォームに署名できます。 例えば、次のワークフローを考えてみましょう。

* Designerを使用して作成されたXFAベースのPDFフォームと、Formsサービスを使用してXMLドキュメント内のフォームデータを結合します。 Formsサーバーはインタラクティブフォームをレンダリングします。
* インタラクティブフォームにはSignatureサービスAPIを使用して署名します。

この結果、デジタル署名されたインタラクティブPDFフォームが生成されます。 XFAフォームに基づくPDFフォームに署名する場合は、PDFファイルをAdobeスタティックPDFフォームとして保存する必要があります。 AdobeダイナミックPDFフォームとして保存されたPDFフォームに署名しようとすると、例外が発生します。 Formsサービスから返されるフォームに署名するので、フォームに署名フィールドが含まれていることを確認してください。

>[!NOTE]
>
>インタラクティブフォームに電子署名する前に、証明書をAEM Formsに追加しておく必要があります。 証明書は、管理コンソールを使用して、またはTrust Manager APIをプログラムで使用して追加します。 （「[Trust Manager APIを使用した秘密鍵証明書の読み込み](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api)」を参照）。

FormsサービスAPIを使用する場合は、`GenerateServerAppearance`ランタイムオプションを`true`に設定します。 この実行時オプションを使用すると、サーバーで生成されたフォームの外観を、AcrobatまたはAdobe Readerで開いたときにも有効なままにすることができます。 FormsAPIを使用して署名するインタラクティブフォームを生成する場合は、このランタイムオプションを設定することをお勧めします。

>[!NOTE]
>
>「デジタル署名のインタラクティブForms」を読む前に、PDFドキュメントの署名について理解しておくことをお勧めします。 (「[PDFドキュメントのデジタル署名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)」を参照)。

### 手順{#summary_of_steps-4}の概要

Formsサービスが返すインタラクティブフォームに電子署名するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Formsおよび署名クライアントを作成します。
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

これらのJARファイルの場所について詳しくは、「[AEM FormsJavaライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)」を参照してください。

**Formsおよび署名クライアントの作成**

このワークフローは、FormsサービスとSignatureサービスの両方を呼び出すので、FormsサービスクライアントとSignatureサービスクライアントの両方を作成します。

**Formsサービスを使用してインタラクティブフォームを取得する**

Formsサービスを使用して、署名するインタラクティブPDFフォームを取得できます。 AEM Forms時点では、レンダリングするフォームを含むFormsサービスに`com.adobe.idp.Document`オブジェクトを渡すことができます。 このメソッドの名前は`renderPDFForm2`です。 このメソッドは、署名するフォームを含む`com.adobe.idp.Document`オブジェクトを返します。 この`com.adobe.idp.Document`インスタンスをSignatureサービスに渡すことができます。

同様に、Webサービスを使用している場合は、Formsサービスが返す`BLOB`インスタンスをSignatureサービスに渡すことができます。

>[!NOTE]
>
>[デジタル署名のインタラクティブなForms]セクションに関連付けられたクイック開始は、`renderPDFForm2`メソッドを呼び出します。

**インタラクティブフォームに署名する**

PDFドキュメントに署名する場合、Signatureサービスで使用する実行時オプションを設定できます。 以下のオプションを設定できます。

* 外観オプション
* 失効確認
* タイムスタンプ値

`PDFSignatureAppearanceOptionSpec`オブジェクトを使用して外観のオプションを設定します。 例えば、`PDFSignatureAppearanceOptionSpec`オブジェクトの`setShowDate`メソッドを呼び出して`true`を渡すことで、署名内に日付を表示できます。

**署名済みPDFドキュメントの保存**

SignatureサービスがPDFドキュメントに電子署名した後、その画像をPDFファイルとして保存できます。 PDFファイルは、AcrobatまたはAdobe Readerで開くことができます。

**関連トピック**

[Java APIを使用したインタラクティブフォームへの電子署名](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-java-api)

[WebサービスAPIを使用したインタラクティブフォームへの電子署名](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDFドキュメントへのデジタル署名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[インタラクティブPDF formsのレンダリング](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms)

### Java API {#digitally-sign-an-interactive-form-using-the-java-api}を使用したインタラクティブフォームへのデジタル署名

Formsおよび署名API(Java)を使用して、インタラクティブフォームに電子署名する：

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-signatures-client.jarやadobe-forms-client.jarなどのクライアントJARファイルを含めます。

1. Formsおよび署名クライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `SignatureServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `FormsServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. Formsサービスを使用してインタラクティブフォームを取得する

   * コンストラクターを使用して、Formsサービスに渡すPDFドキュメントを表す`java.io.FileInputStream`オブジェクトを作成します。 PDFドキュメントの場所を指定するstring値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクターを使用して、Formsサービスに渡すフォームデータを含むXMLドキュメントを表す`java.io.FileInputStream`オブジェクトを作成します。 XMLファイルの場所を指定するstring値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。
   * 実行時オプションの設定に使用する`PDFFormRenderSpec`オブジェクトを作成します。 `PDFFormRenderSpec`オブジェクトの`setGenerateServerAppearance`メソッドを呼び出し、`true`を渡します。
   * `FormsServiceClient`オブジェクトの`renderPDFForm2`メソッドを呼び出し、次の値を渡します。

      * レンダリングするPDFフォームを含む`com.adobe.idp.Document`オブジェクト。
      * フォームとマージするデータを含む`com.adobe.idp.Document`オブジェクト。
      * 実行時オプションを格納する`PDFFormRenderSpec`オブジェクト。
      * Formsサービスに必要なURI値を含む`URLSpec`オブジェクト。 このパラメーター値には`null`を指定できます。
      * 添付ファイルを格納する`java.util.HashMap`オブジェクト。 これはオプションのパラメーターです。フォームにファイルを添付しない場合は、`null`を指定できます。

      `renderPDFForm2`メソッドは、フォームデータストリームを含む`FormsResult`オブジェクトを返します

   * `FormsResult`オブジェクトの`getOutputContent`メソッドを呼び出して、PDFフォームを取得します。 このメソッドは、インタラクティブフォームを表す`com.adobe.idp.Document`オブジェクトを返します。


1. インタラクティブフォームに署名する

   `SignatureServiceClient`オブジェクトの`sign`メソッドを呼び出し、次の値を渡して、PDFドキュメントに署名します。

   * 署名するPDFドキュメントを表す`com.adobe.idp.Document`オブジェクトです。 このオブジェクトが、Formsサービスから取得した`com.adobe.idp.Document`オブジェクトであることを確認します。
   * 署名された署名フィールドの名前を表すstring値です。
   * PDFドキュメントのデジタル署名に使用される秘密鍵証明書を表す`Credential`オブジェクトです。 `Credential`オブジェクトの静的`getInstance`メソッドを呼び出して、`Credential`オブジェクトを作成します。 セキュリティ秘密鍵証明書に対応するエイリアス値を指定するstring値を渡します。
   * PDFドキュメントのダイジェストの作成に使用するハッシュアルゴリズムを表す静的データメンバーを指定する`HashAlgorithm`オブジェクトです。 例えば、`HashAlgorithm.SHA1`にSHA1アルゴリズムを使用するよう指定できます。
   * PDFドキュメントがデジタル署名された理由を表すstring値です。
   * 署名者の連絡先情報を表すstring値です。
   * 電子署名の外観を制御する`PDFSignatureAppearanceOptions`オブジェクトです。 例えば、このオブジェクトを使用して、電子署名にカスタムロゴを追加できます。
   * 署名者の証明書に対して失効確認を実行するかどうかを指定する`java.lang.Boolean`オブジェクトです。
   * オンライン証明書ステータスプロトコル(OCSP)サポートの環境設定を格納する`OCSPPreferences`オブジェクトです。 失効確認が実行されない場合、このパラメーターは使用されず、`null`を指定できます。
   * 証明書失効リスト(CRL)の環境設定を格納する`CRLPreferences`オブジェクトです。 失効確認が実行されない場合、このパラメーターは使用されず、`null`を指定できます。
   * タイムスタンププロバイダー(TSP)サポートの環境設定を格納する`TSPPreferences`オブジェクトです。 このパラメーターはオプションで、`null`にすることができます。

   `sign`メソッドは、署名済みPDFドキュメントを表す`com.adobe.idp.Document`オブジェクトを返します。

1. 署名済みPDFドキュメントの保存

   * `java.io.File`オブジェクトを作成し、ファイル名の拡張子が.pdfであることを確認します。
   * `com.adobe.idp.Document`オブジェクトの`copyToFile`メソッドを呼び出し、`java.io.File`を渡して`Document`オブジェクトの内容をファイルにコピーします。 `sign`メソッドが返した`com.adobe.idp.Document`オブジェクトを使用していることを確認してください。

**関連トピック**

[デジタル署名インタラクティブForms](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[クイック開始（SOAPモード）:Java APIを使用したPDFドキュメントへのデジタル署名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#digitally-sign-an-interactive-form-using-the-web-service-api}を使用してインタラクティブフォームにデジタル署名する

Formsおよび署名API（Webサービス）を使用して、インタラクティブフォームに電子署名する：

1. プロジェクトファイルを含める

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 このクライアントアプリケーションは2つのAEM Formsサービスを呼び出すので、2つのサービス参照を作成します。 Signatureサービスに関連付けられたサービス参照には、次のWSDL定義を使用します。`http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   Formsサービスに関連付けられたサービス参照には、次のWSDL定義を使用します。`http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   `BLOB`データ型は両方のサービス参照に共通なので、`BLOB`データ型を使用する場合は完全に修飾します。 対応するWebサービスクイック開始では、すべての`BLOB`インスタンスが完全修飾されます。

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. Formsおよび署名クライアントの作成

   * `SignatureServiceClient`オブジェクトを作成するには、そのデフォルトのコンストラクタを使用します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`SignatureServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに指定するstring値を渡します（例：`http://localhost:8080/soap/services/SignatureService?WSDL`）。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する場合に使用されます)。
   * `SignatureServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * AEM formsユーザー名をフィールド`SignatureServiceClient.ClientCredentials.UserName.UserName`に割り当てます。
      * 対応するパスワード値をフィールド`SignatureServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * 定数値`HttpClientCredentialType.Basic`をフィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に割り当てます。
   * 定数値`BasicHttpSecurityMode.TransportCredentialOnly`をフィールド`BasicHttpBindingSecurity.Security.Mode`に割り当てます。

   >[!NOTE]
   >
   >Formsサービスクライアントに対して、この手順を繰り返します。

1. Formsサービスを使用してインタラクティブフォームを取得する

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、署名されたPDFドキュメントの保存に使用されます。
   * コンストラクターを呼び出し、署名するPDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得して、バイト配列のサイズを決定できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * `BLOB`オブジェクトに、`MTOM`プロパティにバイト配列の内容を割り当てて入力します。
   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、フォームデータの格納に使用されます。
   * コンストラクターを呼び出し、フォームデータを含むXMLファイルのファイル位置、およびファイルを開くモードを表す文字列値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得して、バイト配列のサイズを決定できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * `BLOB`オブジェクトに、`MTOM`プロパティにバイト配列の内容を割り当てて入力します。
   * 実行時オプションの設定に使用する`PDFFormRenderSpec`オブジェクトを作成します。 値`true`を`PDFFormRenderSpec`オブジェクトの`generateServerAppearance`フィールドに割り当てます。
   * `FormsServiceClient`オブジェクトの`renderPDFForm2`メソッドを呼び出し、次の値を渡します。

      * レンダリングするPDFフォームを含む`BLOB`オブジェクト。
      * フォームとマージするデータを含む`BLOB`オブジェクト。
      * 実行時オプションを格納する`PDFFormRenderSpec`オブジェクト。
      * Formsサービスに必要なURI値を含む`URLSpec`オブジェクト。 このパラメーター値には`null`を指定できます。
      * 添付ファイルを格納する`java.util.HashMap`オブジェクト。 これはオプションのパラメーターです。フォームにファイルを添付しない場合は、`null`を指定できます。
      * フォーム内のページ数を保存するために使用される長い出力パラメーター。
      * ロケール値に使用される文字列出力パラメーターです。
      * インタラクティブフォームの保存に使用される出力パラメーターである`FormResult`値。
   * `FormsResult`オブジェクトの`outputContent`フィールドを呼び出して、PDFフォームを取得します。 このフィールドには、インタラクティブフォームを表す`BLOB`オブジェクトが格納されます。


1. インタラクティブフォームに署名する

   `SignatureServiceClient`オブジェクトの`sign`メソッドを呼び出し、次の値を渡して、PDFドキュメントに署名します。

   * 署名するPDFドキュメントを表す`BLOB`オブジェクトです。 Formsサービスから返される`BLOB`インスタンスを使用します。
   * 署名された署名フィールドの名前を表すstring値です。
   * PDFドキュメントのデジタル署名に使用される秘密鍵証明書を表す`Credential`オブジェクトです。 `Credential`オブジェクトを作成するには、コンストラクターを使用します。また、`Credential`オブジェクトの`alias`プロパティに値を割り当ててエイリアスを指定します。
   * PDFドキュメントのダイジェストの作成に使用するハッシュアルゴリズムを表す静的データメンバーを指定する`HashAlgorithm`オブジェクトです。 例えば、`HashAlgorithm.SHA1`にSHA1アルゴリズムを使用するよう指定できます。
   * ハッシュアルゴリズムを使用するかどうかを指定するBoolean値です。
   * PDFドキュメントがデジタル署名された理由を表すstring値です。
   * 署名者の場所を表すstring値です。
   * 署名者の連絡先情報を表すstring値です。
   * 電子署名の外観を制御する`PDFSignatureAppearanceOptions`オブジェクトです。 例えば、このオブジェクトを使用して、電子署名にカスタムロゴを追加できます。
   * 署名者の証明書に対して失効確認を実行するかどうかを指定する`System.Boolean`オブジェクトです。 この失効確認が行われると、署名に埋め込まれます。 デフォルトは、`false` です。
   * オンライン証明書ステータスプロトコル(OCSP)サポートの環境設定を格納する`OCSPPreferences`オブジェクトです。 失効確認が実行されない場合、このパラメーターは使用されず、`null`を指定できます。 このオブジェクトについて詳しくは、[AEM FormsAPIリファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)を参照してください。
   * 証明書失効リスト(CRL)の環境設定を格納する`CRLPreferences`オブジェクトです。 失効確認が実行されない場合、このパラメーターは使用されず、`null`を指定できます。
   * タイムスタンププロバイダー(TSP)サポートの環境設定を格納する`TSPPreferences`オブジェクトです。 このパラメーターはオプションで、`null`にすることができます。

   `sign`メソッドは、署名済みPDFドキュメントを表す`BLOB`オブジェクトを返します。

1. 署名済みPDFドキュメントの保存

   * コンストラクターを呼び出して、`System.IO.FileStream`オブジェクトを作成します。 署名済みPDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * `sign`メソッドから返された`BLOB`オブジェクトの内容を格納するバイト配列を作成します。 `BLOB`オブジェクトの`MTOM`データメンバの値を取得して、バイト配列を入力します。
   * コンストラクターを呼び出して`System.IO.FileStream`オブジェクトを渡し、`System.IO.BinaryWriter`オブジェクトを作成します。
   * `System.IO.BinaryWriter`オブジェクトの`Write`メソッドを呼び出し、バイト配列を渡すことで、バイト配列の内容をPDFファイルに書き込みます。

**関連トピック**

[デジタル署名インタラクティブForms](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## PDF ドキュメントの認証 {#certifying-pdf-documents}

認証署名と呼ばれる特定のタイプの署名によって PDF ドキュメントを認証することで、PDF ドキュメントを保護することができます。認証署名は、以下の方法で電子署名と区別されます。

* 認証署名は PDF ドキュメントに適用される最初の署名です。つまり、認証署名が適用されるときは、ドキュメント内の他の署名フィールドは未署名でなければいけません。認証署名は 1 つの PDF ドキュメントにつき 1 つです。PDF ドキュメントを署名および認証するには、署名の前に認証を行う必要があります。PDF ドキュメントの認証後、他の署名フィールドに電子署名を行うことができます。
* ドキュメントの作成者または発信者は、認証署名を無効にすることなく、特定の方法でドキュメントの変更が可能になるように指定することができます。例えば、フォームへの入力やコメント入力を許可するドキュメントなどがあります。作成者が特定の変更を許可しないように設定を行った場合は、Acrobat はユーザーのその方法によるドキュメントの変更を制限します。別のアプリケーションを使用するなどしてそのような変更が行われた場合は、認証署名は無効となり、Acrobat はユーザーがドキュメントを開いた際に警告を発します。（未認証の署名では、変更を防ぐことはできません。また、通常の編集操作では元の署名は無効になりません。）
* 署名時に、ドキュメントのコンテンツにあいまいさや誤解をもたらす可能性のある、特定の種類のコンテンツをスキャンします。例えば、注釈により、認証される対象を把握するために重要なページ上のテキストが隠れてしまう場合があります。そのようなコンテンツに関する、説明（法的証明）を提供することができます。

SignatureサービスJava APIまたはSignature WebサービスAPIを使用して、PDFドキュメントをプログラムで認証できます。 PDFドキュメントを認証する場合は、秘密鍵証明書サービスに存在するセキュリティ秘密鍵証明書を参照する必要があります。 セキュリティ証明書について詳しくは、使用しているアプリケーションサーバー版の『*AEM Forms*&#x200B;のインストールおよびデプロイ』ガイドを参照してください。

>[!NOTE]
>
>同じPDFドキュメントの認証および署名時に、認証署名が信頼されていない場合、AcrobatまたはAdobe ReaderでPDFドキュメントを開くと、最初の署名の横に黄色い三角形が表示されます。 この状況を回避するには、認証署名を信頼する必要があります。

>[!NOTE]
>
>PDFドキュメントの署名や認証にnCipher nShield HSM秘密鍵証明書を使用する場合、AEM FormsがデプロイされているJ2EEアプリケーションサーバーを再起動するまで、新しい秘密鍵証明書は使用できません。 ただし、設定値を設定すると、J2EEアプリケーションサーバーを再起動しなくても、署名または認証の操作が動作します。

次の設定値をcknfastrcファイルに追加できます。このファイルは/opt/nfast/cknfastrc(またはc:\nfast\cknfastrc)にあります。

```shell
    CKNFAST_ASSUME_SINGLE_PROCESS=0
```

この設定値をcknfastrcファイルに追加すると、J2EEアプリケーションサーバーを再起動しなくても、新しい秘密鍵証明書を使用できます。

>[!NOTE]
>
>Signatureサービスとドキュメントの認証について詳しくは、『[AEM Forms向けサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順{#summary_of_steps-5}の概要

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

これらのJARファイルの場所について詳しくは、「[AEM FormsJavaライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)」を参照してください。

**署名クライアントの作成**

プログラムによってSignature操作を実行する前に、Signatureクライアントを作成する必要があります。

**認証用のPDFドキュメントの取得**

PDFドキュメントを認証するには、署名フィールドを含むPDFドキュメントを取得する必要があります。 PDFドキュメントに署名フィールドが含まれていない場合は、認証できません。 署名フィールドは、Designerを使用して追加することも、プログラムを使用して追加することもできます。 プログラムによる署名フィールドの追加について詳しくは、「[署名フィールドの追加](digitally-signing-certifying-documents.md#adding-signature-fields)」を参照してください。

**PDFドキュメントの認証**

PDFドキュメントを正常に認証するには、SignatureサービスでPDFドキュメントの認証に使用される次の入力値が必要です。

* **PDFドキュメント**:署名フィールドを含むPDFドキュメントです。署名フィールドは、認証署名のグラフィック表現を含むフォームフィールドです。PDFドキュメントを認証するには、その前に署名フィールドがPDF署名に含まれている必要があります。 署名フィールドは、Designerを使用して追加することも、プログラムを使用して追加することもできます。 （「[署名フィールドの追加](digitally-signing-certifying-documents.md#adding-signature-fields)」を参照）。
* **署名フィールド名**:認証される署名フィールドの完全修飾名です。次の値は例です。`form1[0].#subform[1].SignatureField3[3]`. XFAフォームフィールドを使用する場合は、署名フィールドの名前の一部を使用することもできます。`SignatureField3[3]`. フィールド名にnull値が渡されると、非表示の署名フィールドが動的に作成され、認証されます。
* **セキュリティ証明書**:PDFドキュメントの認証に使用する秘密鍵証明書です。このセキュリティ証明書には、パスワードとエイリアスが含まれています。これは、Credentialサービス内の秘密鍵証明書に表示されるエイリアスと一致する必要があります。 エイリアスは、PKCS#12ファイル（拡張子.pfx付き）またはハードウェアセキュリティモジュール(HSM)内の実際の秘密鍵証明書への参照です。
* **ハッシュアルゴリズム**:PDFドキュメントのダイジェストの作成に使用するハッシュアルゴリズムです。
* **署名の理由**:PDFドキュメントが認証された理由を他のユーザーが把握できるように、AcrobatまたはAdobe Readerに表示される値です。
* **署名者の場所**:秘密鍵証明書で指定された署名者の場所です。
* **連絡先情報**:署名者の住所や電話番号などの連絡先情報。
* **権限情報**:認証署名を無効にすることなく、エンドユーザーがドキュメントに対して実行できる操作を制御する権限です。例えば、権限を設定して、PDFドキュメントを変更すると認証署名が無効になるようにすることができます。
* **法的説明**:ドキュメントを認証すると、ドキュメントのコンテンツをあいまいにしたり誤解を招く可能性のある、特定のタイプのコンテンツを自動的にスキャンします。例えば、注釈により、認証される対象を把握するために重要なページ上のテキストが隠れてしまう場合があります。スキャン処理では、この種のコンテンツに関する警告が生成されます。 この値は、警告が生成された可能性のあるコンテンツに関する追加の説明を提供します。
* **外観オプション**:認証署名の外観を制御するオプションです。例えば、認証署名には日付情報を表示できます。
* **失効確認**:この値は、署名者の証明書に対して失効確認を行うかどうかを指定します。デフォルト設定の`false`では、失効確認は実行されません。
* **OCSP settings**:PDFドキュメントの認証に使用される秘密鍵証明書のステータスに関する情報を提供する、オンライン証明書ステータスプロトコル(OCSP)サポートの設定です。例えば、PDFドキュメントへのサインオンに使用する秘密鍵証明書に関する情報を提供するサーバーのURLを指定できます。
* **CRL settings**:失効確認が行われた場合の証明書失効リスト(CRL)の環境設定です。例えば、秘密鍵証明書が失効したかどうかを常に確認するように指定できます。
* **タイムスタンプ**:認証署名に適用されるタイムスタンプ情報を定義する設定です。タイムスタンプは、特定のデータが特定の時間の前に確立されたことを示します。 この情報は、署名者と検証者の間に信頼関係を構築するのに役立ちます。

**認証済みPDFドキュメントをPDFファイルとして保存する**

SignatureサービスがPDFドキュメントを認証した後、その画像をPDFファイルとして保存し、ユーザーがAcrobatまたはAdobe Readerで開けるようにできます。

**関連トピック**

[Java APIを使用したPDFドキュメントの認証](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-java-api)

[WebサービスAPIを使用したPDFドキュメントの認証](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[署名フィールドの追加](digitally-signing-certifying-documents.md#adding-signature-fields)

### Java API {#certify-pdf-documents-using-the-java-api}を使用してPDFドキュメントを認証する

Signature API(Java)を使用してPDFドキュメントを認証します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-signatures-client.jarなどのクライアントJARファイルを含めます。

1. 署名クライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `SignatureServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 認証用のPDFドキュメントの取得

   * コンストラクターを使用し、PDFドキュメントの場所を指定するstring値を渡して、認証するPDFドキュメントを表す`java.io.FileInputStream`オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PDFドキュメントの認証

   `SignatureServiceClient`オブジェクトの`certify`メソッドを呼び出し、次の値を渡して、PDFドキュメントを認証します。

   * 認証するPDFドキュメントを表す`com.adobe.idp.Document`オブジェクトです。
   * 署名を含む署名フィールドの名前を表すstring値です。
   * PDFドキュメントの認証に使用される秘密鍵証明書を表す`Credential`オブジェクトです。 `Credential`オブジェクトの静的な`getInstance`メソッドを呼び出し、セキュリティ証明書に対応するエイリアス値を指定する文字列値を渡して、`Credential`オブジェクトを作成します。
   * PDFドキュメントのダイジェストの作成に使用されるハッシュアルゴリズムを表す静的データメンバーを指定する`HashAlgorithm`オブジェクトです。 例えば、`HashAlgorithm.SHA1`にSHA1アルゴリズムを使用するよう指定できます。
   * PDFドキュメントが認証された理由を表すstring値です。
   * 署名者の連絡先情報を表すstring値です。
   * 署名を無効にするPDFドキュメントで実行できるアクションを指定する`MDPPermissions`オブジェクトです。
   * 認証署名の外観を制御する`PDFSignatureAppearanceOptions`オブジェクトです。 必要に応じて、`setShowDate`などのメソッドを呼び出して、署名の外観を変更します。
   * 署名を無効にするアクションについての説明を提供するstring値です。
   * 署名者の証明書に対して失効確認を実行するかどうかを指定する`java.lang.Boolean`オブジェクトです。 この失効確認が行われると、署名に埋め込まれます。 デフォルトは、`false` です。
   * 認証する署名フィールドがロックされているかどうかを指定する`java.lang.Boolean`オブジェクトです。 フィールドをロックすると、署名フィールドは読み取り専用としてマークされ、プロパティを変更できなくなり、必要な権限を持たないユーザーはこのフィールドをクリアできなくなります。 デフォルトは、`false` です。
   * オンライン証明書ステータスプロトコル(OCSP)サポートの環境設定を格納する`OCSPPreferences`オブジェクトです。 失効確認が実行されない場合、このパラメーターは使用されず、`null`を指定できます。 このオブジェクトについて詳しくは、「[AEM FormsAPIリファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)」を参照してください。
   * 証明書失効リスト(CRL)の環境設定を格納する`CRLPreferences`オブジェクトです。 失効確認が実行されない場合、このパラメーターは使用されず、`null`を指定できます。
   * タイムスタンププロバイダー(TSP)サポートの環境設定を格納する`TSPPreferences`オブジェクトです。 例えば、`TSPPreferences`オブジェクトを作成した後、`TSPPreferences`オブジェクトの`setTspServerURL`メソッドを呼び出して、TSPサーバーのURLを設定できます。 このパラメーターはオプションで、`null`にすることができます。 詳しくは、[『AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)サービスリファレンス』を参照してください。

   `certify`メソッドは、認証済みPDFドキュメントを表す`com.adobe.idp.Document`オブジェクトを返します。

1. 認証済みPDFドキュメントをPDFファイルとして保存する

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が .pdf であることを確認します。
   * `com.adobe.idp.Document`オブジェクトの`copyToFile`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトの内容をファイルにコピーします。

**関連トピック**

[PDF ドキュメントの認証](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[クイック開始（SOAPモード）:Java APIを使用したPDFドキュメントの認証](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-certifying-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#certify-pdf-documents-using-the-web-service-api}を使用してPDFドキュメントを認証する

Signature API（Webサービス）を使用してPDFドキュメントを認証します。

1. プロジェクトファイルを含める

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. 署名クライアントの作成

   * `SignatureServiceClient`オブジェクトを作成するには、そのデフォルトのコンストラクタを使用します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`SignatureServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに指定するstring値を渡します（例：`http://localhost:8080/soap/services/SignatureService?WSDL`）。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する場合に使用されます)。
   * `SignatureServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * AEM formsユーザー名をフィールド`SignatureServiceClient.ClientCredentials.UserName.UserName`に割り当てます。
      * 対応するパスワード値をフィールド`SignatureServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * 定数値`HttpClientCredentialType.Basic`をフィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に割り当てます。
      * 定数値`BasicHttpSecurityMode.TransportCredentialOnly`をフィールド`BasicHttpBindingSecurity.Security.Mode`に割り当てます。

1. 認証用のPDFドキュメントの取得

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、認証済みのPDFドキュメントを保存するために使用します。
   * コンストラクターを呼び出し、認証するPDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得して、バイト配列のサイズを決定できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * `BLOB`オブジェクトに、`MTOM`データメンバにバイト配列の内容を割り当てて、&lt;a0/>オブジェクトを入力します。

1. PDFドキュメントの認証

   `SignatureServiceClient`オブジェクトの`certify`メソッドを呼び出し、次の値を渡して、PDFドキュメントを認証します。

   * 認証するPDFドキュメントを表す`BLOB`オブジェクトです。
   * 署名を含む署名フィールドの名前を表すstring値です。
   * PDFドキュメントの認証に使用される秘密鍵証明書を表す`Credential`オブジェクトです。 `Credential`オブジェクトを作成するには、コンストラクターを使用します。エイリアスを指定するには、`Credential`オブジェクトの`alias`プロパティに値を割り当てます。
   * PDFドキュメントのダイジェストの作成に使用されるハッシュアルゴリズムを表す静的データメンバーを指定する`HashAlgorithm`オブジェクトです。 例えば、`HashAlgorithm.SHA1`にSHA1アルゴリズムを使用するよう指定できます。
   * ハッシュアルゴリズムを使用するかどうかを指定するBoolean値です。
   * PDFドキュメントが認証された理由を表すstring値です。
   * 署名者の場所を表すstring値です。
   * 署名者の連絡先情報を表すstring値です。
   * 署名を無効にするPDFドキュメントで実行できるアクションを指定する`MDPPermissions`オブジェクトの静的データメンバーです。
   * 前のパラメーター値として渡された`MDPPermissions`オブジェクトを使用するかどうかを指定するBoolean値。
   * 署名を無効にするアクションを説明するstring値です。
   * 認証署名の外観を制御する`PDFSignatureAppearanceOptions`オブジェクトです。 コンストラクタを使用して `PDFSignatureAppearanceOptions` オブジェクトを作成します。データメンバーの1つを設定して、署名の外観を変更できます。
   * 署名者の証明書に対して失効確認を実行するかどうかを指定する`System.Boolean`オブジェクトです。 この失効確認が行われると、署名に埋め込まれます。 デフォルトは、`false` です。
   * 認証する署名フィールドがロックされているかどうかを指定する`System.Boolean`オブジェクトです。 フィールドをロックすると、署名フィールドは読み取り専用としてマークされ、プロパティを変更できなくなり、必要な権限を持たないユーザーはこのフィールドをクリアできなくなります。 デフォルトは、`false` です。
   * 署名フィールドをロックするかどうかを指定する`System.Boolean`オブジェクトです。 つまり、前のパラメーターに`true`を渡す場合は、このパラメーターに`true`を渡します。
   * オンライン証明書ステータスプロトコル(OCSP)サポートの環境設定を格納する`OCSPPreferences`オブジェクトです。PDFドキュメントの認証に使用される秘密鍵証明書のステータスに関する情報を提供します。 失効確認が実行されない場合、このパラメーターは使用されず、`null`を指定できます。
   * 証明書失効リスト(CRL)の環境設定を格納する`CRLPreferences`オブジェクトです。 失効確認が実行されない場合、このパラメーターは使用されず、`null`を指定できます。
   * タイムスタンププロバイダー(TSP)サポートの環境設定を格納する`TSPPreferences`オブジェクトです。 例えば、`TSPPreferences`オブジェクトを作成した後、`TSPPreferences`オブジェクトの`tspServerURL`データメンバーを設定することで、TSPのURLを設定できます。 このパラメーターはオプションで、`null`にすることができます。

   `certify`メソッドは、認証済みPDFドキュメントを表す`BLOB`オブジェクトを返します。

1. 認証済みPDFドキュメントをPDFファイルとして保存する

   * コンストラクターを呼び出し、認証済みのPDFドキュメントーとファイルを開くモードを含むPDFドキュメントーのファイルの場所を表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `certify`メソッドから返された`BLOB`オブジェクトの内容を格納するバイト配列を作成します。 `BLOB`オブジェクトの`binaryData`データメンバの値を取得して、バイト配列を入力します。
   * コンストラクターを呼び出して`System.IO.FileStream`オブジェクトを渡し、`System.IO.BinaryWriter`オブジェクトを作成します。
   * `System.IO.BinaryWriter`オブジェクトの`Write`メソッドを呼び出し、バイト配列を渡すことで、バイト配列の内容をPDFファイルに書き込みます。

**関連トピック**

[PDF ドキュメントの認証](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## デジタル署名の検証{#verifying-digital-signatures}

電子署名を検証することで、署名された PDF ドキュメントに変更がなく、電子署名が有効であることを確認することができます。電子署名を検証する際に、署名のステータスや、署名者のIDなどの署名のプロパティを確認できます。 電子署名を信用する前に、検証することをおすすめします。電子署名を検証する際、電子署名を含む PDF ドキュメントを参照します。

署名者のIDが不明であるとします。 AcrobatでPDFドキュメントを開くと、次の図に示すように、署名者のIDが不明であることを示す警告メッセージが表示されます。

![vd_vd_verifysig](assets/vd_vd_verifysig.png)

同様に、プログラムで電子署名を検証する場合、署名者のIDのステータスを判断できます。 例えば、前の図に示すドキュメントで電子署名を検証すると、署名者のIDが不明になります。

>[!NOTE]
>
>Signatureサービスと電子署名の検証について詳しくは、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順{#summary_of_steps-6}の概要

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

これらのJARファイルの場所について詳しくは、「[AEM FormsJavaライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)」を参照してください。

**署名クライアントの作成**

プログラムを使用してSignatureサービス操作を実行する前に、Signatureサービスクライアントを作成します。

**検証する署名が含まれているPDFドキュメントを取得します**

PDF署名のデジタル署名や認証に使用されるドキュメントを検証するには、署名が含まれるPDFドキュメントを取得します。

**PKIランタイムオプションの設定**

PDFドキュメントの署名を検証する際にSignatureサービスで使用する次のPKIランタイムオプションを設定します。

* 検証時刻
* 失効確認
* タイムスタンプ値

これらのオプションの設定の一環として、検証時刻を指定できます。 例えば、現在の時間（バリデーターのコンピューター上の時間）を選択できます。これは現在の時間を使用することを示します。 異なる時間値について詳しくは、[AEM FormsAPIリファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)の`VerificationTime`定義済みリスト値を参照してください。

検証プロセスの一環として失効確認を実行するかどうかを指定することもできます。 例えば、失効確認を実行して、証明書が失効したかどうかを判断できます。 失効確認オプションについて詳しくは、『[AEM FormsAPIリファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)』の`RevocationCheckStyle`定義済みリスト値を参照してください。

証明書に対して失効確認を実行するには、`CRLOptionSpec`オブジェクトを使用して、証明書失効リスト(CRL)サーバーへのURLを指定します。 ただし、URLをCRLサーバーに指定しない場合、Signatureサービスは証明書からURLを取得します。

失効確認を実行する際は、CRLサーバーを使用する代わりに、オンライン証明書ステータスプロトコル(OCSP)サーバーを使用できます。 通常、CRLサーバーとは異なるOCSPサーバーを使用する場合、失効確認は高速に実行されます。 （[オンライン証明書ステータスプロトコル](https://tools.ietf.org/html/rfc2560)を参照）。

Signatureサービスで使用するCRLおよびOCSPAdobeの順序は、「Applications and Services」を使用して設定できます。 例えば、「Adobeアプリケーションおよびサービス」でOCSPサーバーを最初に設定した場合、OCSPサーバーを確認し、次にCRLサーバーを確認します。

失効確認を実行しない場合、Signatureサービスでは、証明書が失効したかどうかを確認しません。 つまり、CRLおよびOCSPサーバー情報は無視されます。

>[!NOTE]
>
>`CRLOptionSpec`および`OCSPOptionSpec`オブジェクトを使用して、証明書で指定されたURLを上書きできます。 例えば、CRLサーバーを上書きするには、`CRLOptionSpec`オブジェクトの`setLocalURI`メソッドを呼び出します。

タイムスタンプとは、署名済みまたは認証済みのドキュメントが変更された時間を追跡するプロセスです。 ドキュメントに署名した後は、誰もその署名を変更できません。 タイムスタンプ機能を使用すると、署名済みまたは認証済みのドキュメントの有効性を強化できます。 `TSPOptionSpec`オブジェクトを使用して、タイムスタンプオプションを設定できます。 例えば、タイムスタンププロバイダー(TSP)サーバーのURLを指定できます。

>[!NOTE]
>
>JavaおよびWebサービスのクイック開始では、検証時刻は`VerificationTime.CURRENT_TIME`に、失効確認は`RevocationCheckStyle.BestEffort`に設定されます。 CRLまたはOCSPサーバー情報が指定されていないので、サーバー情報は証明書から取得されます。

**電子署名の検証**

署名を正しく検証するには、署名が含まれる署名フィールドの完全修飾名を指定します（例：`form1[0].#subform[1].SignatureField3[3]`）。 XFAフォームフィールドを使用する場合は、署名フィールドの名前の一部を使用することもできます。`SignatureField3`.

デフォルトでは、Signatureサービスでは、検証後にドキュメントに署名できる時間が65分に制限されます。 ユーザーが現在の時刻に署名を検証しようとしたときに、署名時刻が現在の時刻より後で65分以内になった場合、Signatureサービスでは検証エラーは作成されません。

>[!NOTE]
>
>署名を検証する際に必要なその他の値については、『[AEM FormsAPIリファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)』を参照してください。

**署名のステータスの確認**

電子署名の検証中に、署名のステータスを確認できます。

**署名者のIDの確認**

署名者のIDを特定できます。次の値のいずれかになります。

* **不明**:署名者の検証を実行できないため、署名者が不明です。
* **信頼済み**:この署名者は信頼されています。
* **信頼できません**:この署名者は信頼されていません。

**関連トピック**

[Java APIを使用した電子署名の検証](#verify-digital-signatures-using-the-java-api)

[WebサービスAPIを使用した電子署名の検証](#verify-digital-signatures-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java APIを使用した電子署名の検証{#verify-digital-signatures-using-the-java-api}

Signature Service API(Java)を使用して電子署名を検証します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-signatures-client.jarなどのクライアントJARファイルを含めます。

1. 署名クライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `SignatureServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 検証する署名が含まれているPDFドキュメントを取得します

   * 検証する署名が含まれているPDFドキュメントを表す`java.io.FileInputStream`オブジェクトを、コンストラクターを使用して作成します。 PDFドキュメントの場所を指定するstring値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PKIランタイムオプションの設定

   * コンストラクタを使用して `PKIOptions` オブジェクトを作成します。
   * `PKIOptions`オブジェクトの`setVerificationTime`メソッドを呼び出し、検証時刻を指定する`VerificationTime`定義済みリスト値を渡して、検証時刻を設定します。
   * `PKIOptions`オブジェクトの`setRevocationCheckStyle`メソッドを呼び出し、失効確認を実行するかどうかを指定する`RevocationCheckStyle`定義済みリスト値を渡して、失効確認オプションを設定します。

1. 電子署名の検証

   `SignatureServiceClient`オブジェクトの`verify2`メソッドを呼び出し、次の値を渡して、署名を検証します。

   * デジタル署名された、または認証されたPDFドキュメントを含む`com.adobe.idp.Document`オブジェクトです。
   * 検証する署名が含まれている署名フィールド名を表すstring値です。
   * PKIランタイムオプションを含む`PKIOptions`オブジェクト。
   * SPI情報を含む`VerifySPIOptions`インスタンスです。 このパラメーターには`null`を指定できます。

   `verify2`メソッドは、デジタル署名の検証に使用できる情報を含む`PDFSignatureVerificationInfo`オブジェクトを返します。

1. 署名のステータスの確認

   * `PDFSignatureVerificationInfo`オブジェクトの`getStatus`メソッドを呼び出して、署名のステータスを判断します。 このメソッドは、署名の状態を指定する`SignatureStatus`オブジェクトを返します。 例えば、署名済みPDFのドキュメントが変更されていない場合、このメソッドは`SignatureStatus.DocumentSigNoChanges`を返します。

1. 署名者のIDの確認

   * `PDFSignatureVerificationInfo`オブジェクトの`getSigner`メソッドを呼び出して、署名者のIDを特定します。 このメソッドは、`IdentityInformation`オブジェクトを返します。
   * `IdentityInformation`オブジェクトの`getStatus`メソッドを呼び出して、署名者のIDを特定します。 このメソッドは、IDを指定する`IdentityStatus`定義済みリスト値を返します。 例えば、署名者が信頼できる場合、このメソッドは`IdentityStatus.TRUSTED`を返します。

**関連トピック**

[電子署名の検証](#verify-digital-signatures-using-the-java-api)

[クイック開始（SOAPモード）:Java APIを使用したデジタル署名の検証](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-a-digital-signature-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#verify-digital-signatures-using-the-web-service-api}を使用した電子署名の検証

Signature Service API（Webサービス）を使用して電子署名を検証します。

1. プロジェクトファイルを含める

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. 署名クライアントの作成

   * `SignatureServiceClient`オブジェクトを作成するには、そのデフォルトのコンストラクタを使用します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`SignatureServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに指定するstring値を渡します（例：`http://localhost:8080/soap/services/SignatureService?WSDL`）。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する場合に使用されます)。
   * `SignatureServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * AEM formsユーザー名をフィールド`SignatureServiceClient.ClientCredentials.UserName.UserName`に割り当てます。
      * 対応するパスワード値をフィールド`SignatureServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * 定数値`HttpClientCredentialType.Basic`をフィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に割り当てます。
      * 定数値`BasicHttpSecurityMode.TransportCredentialOnly`をフィールド`BasicHttpBindingSecurity.Security.Mode`に割り当てます。

1. 検証する署名が含まれているPDFドキュメントを取得します

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、検証するデジタル署名または認証署名が含まれるPDFドキュメントを保存するために使用します。
   * コンストラクターを呼び出して、`System.IO.FileStream`オブジェクトを作成します。 署名済みPDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得して、バイト配列のサイズを決定できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出して、バイト配列にストリームデータを入力します。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * `BLOB`オブジェクトに、`MTOM`プロパティにバイト配列の内容を割り当てて入力します。

1. PKIランタイムオプションの設定

   * コンストラクタを使用して `PKIOptions` オブジェクトを作成します。
   * `PKIOptions`オブジェクトの`verificationTime`データメンバに検証時刻を指定する`VerificationTime`定義済みリスト値を割り当てて、検証時刻を設定します。
   * 失効確認オプションを設定するには、`PKIOptions`オブジェクトの`revocationCheckStyle`データメンバに失効確認を実行するかどうかを指定する`RevocationCheckStyle`定義済みリスト値を割り当てます。

1. 電子署名の検証

   `SignatureServiceClient`オブジェクトの`verify2`メソッドを呼び出し、次の値を渡して、署名を検証します。

   * デジタル署名された、または認証されたPDFドキュメントを含む`BLOB`オブジェクトです。
   * 検証する署名が含まれている署名フィールド名を表すstring値です。
   * PKIランタイムオプションを含む`PKIOptions`オブジェクト。
   * SPI情報を含む`VerifySPIOptions`インスタンスです。 このパラメーターには`null`を指定できます。

   `verify2`メソッドは、デジタル署名の検証に使用できる情報を含む`PDFSignatureVerificationInfo`オブジェクトを返します。

1. 署名のステータスの確認

   `PDFSignatureVerificationInfo`オブジェクトの`status`データメンバーの値を取得して、署名のステータスを決定します。 このデータメンバーには、署名のステータスを指定する`SignatureStatus`オブジェクトが格納されます。 例えば、署名済みPDFドキュメントが変更された場合、`status`データメンバーに値`SignatureStatus.DocumentSigNoChanges`が格納されます。

1. 署名者のIDの確認

   * `PDFSignatureVerificationInfo`オブジェクトの`signer`データメンバの値を取得して、署名者のIDを特定します。 このメンバは`IdentityInformation`オブジェクトを返します。
   * `IdentityInformation`オブジェクトの`status`データメンバーを取得して、署名者のIDを特定します。 このデータメンバは、IDを指定する`IdentityStatus`定義済みリスト値を返します。 例えば、署名者が信頼できる場合、このメンバーは`IdentityStatus.TRUSTED`を返します。

**関連トピック**

[電子署名の検証](#verify-digital-signatures-using-the-java-api)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 複数の電子署名の検証{#verifying-multiple-digital-signatures}

AEM Formsは、PDFドキュメント内のすべての電子署名を検証する手段を提供します。 複数の署名者からの署名が必要なビジネスプロセスの結果として、PDFドキュメントに複数の電子署名が含まれているとします。 例えば、融資担当者の署名と管理者の署名の両方が必要な金融トランザクションについて考えてみましょう。 SignatureサービスのJava APIまたはWebサービスのAPIを使用して、PDFドキュメント内のすべての署名を検証できます。 複数の署名を検証する際は、それぞれの署名のステータスやプロパティを確認できます。電子署名を信頼する前に、検証することをお勧めします。 単一の電子署名の検証について詳しく知ることをお勧めします。

>[!NOTE]
>
>Signatureサービスと電子署名の検証について詳しくは、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順{#summary_of_steps-7}の概要

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

これらのJARファイルの場所について詳しくは、「[AEM FormsJavaライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)」を参照してください。

**署名クライアントの作成**

プログラムを使用してSignatureサービス操作を実行する前に、Signatureサービスクライアントを作成します。

**検証する署名が含まれているPDFドキュメントを取得します**

PDF署名のデジタル署名や認証に使用されるドキュメントを検証するには、署名が含まれるPDFドキュメントを取得します。

**PKIランタイムオプションの設定**

PDFドキュメントのすべての署名を検証する際にSignatureサービスで使用する次のPKIランタイムオプションを設定します。

* 検証時刻
* 失効確認
* タイムスタンプ値

これらのオプションの設定の一環として、検証時刻を指定できます。 例えば、現在の時間（バリデーターのコンピューター上の時間）を選択できます。これは現在の時間を使用することを示します。 異なる時間値について詳しくは、[AEM FormsAPIリファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)の`VerificationTime`定義済みリスト値を参照してください。

検証プロセスの一環として失効確認を実行するかどうかを指定することもできます。 例えば、失効確認を実行して、証明書が失効したかどうかを判断できます。 失効確認オプションについて詳しくは、『[AEM FormsAPIリファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)』の`RevocationCheckStyle`定義済みリスト値を参照してください。

証明書に対して失効確認を実行するには、`CRLOptionSpec`オブジェクトを使用して、証明書失効リスト(CRL)サーバーへのURLを指定します。 ただし、CRLサーバーへのURLを指定しない場合、Signatureサービスは証明書からURLを取得します。

失効確認を実行する際は、CRLサーバーを使用する代わりに、オンライン証明書ステータスプロトコル(OCSP)サーバーを使用できます。 通常、CRLサーバーではなくOCSPサーバーを使用する場合は、失効確認の実行が高速になります。 （[オンライン証明書ステータスプロトコル](https://tools.ietf.org/html/rfc2560)を参照）。

Signatureサービスで使用するCRLおよびOCSPAdobeの順序は、「Applications and Services」を使用して設定できます。 例えば、「Adobeアプリケーションおよびサービス」でOCSPサーバーが最初に設定されている場合、OCSPサーバーがチェックされ、次にCRLサーバーがチェックされます。

失効確認を実行しない場合、Signatureサービスでは、証明書が失効したかどうかを確認しません。 つまり、CRLおよびOCSPサーバー情報は無視されます。

>[!NOTE]
>
>`CRLOptionSpec`および`OCSPOptionSpec`オブジェクトを使用して、証明書で指定されたURLを上書きできます。 例えば、CRLサーバーを上書きするには、`CRLOptionSpec`オブジェクトの`setLocalURI`メソッドを呼び出します。

タイムスタンプとは、署名済みまたは認証済みのドキュメントが変更された時間を追跡するプロセスです。 ドキュメントに署名した後は、誰もその署名を変更できません。 タイムスタンプ機能を使用すると、署名済みまたは認証済みのドキュメントの有効性を強化できます。 タイムスタンプオプションは、`TSPOptionSpec`オブジェクトを使用して設定できます。 例えば、タイムスタンププロバイダー(TSP)サーバーのURLを指定できます。

>[!NOTE]
>
>JavaおよびWebサービスのクイック開始では、検証時刻は`VerificationTime.CURRENT_TIME`に、失効確認は`RevocationCheckStyle.BestEffort`に設定されます。 CRLまたはOCSPサーバー情報が指定されていないので、サーバー情報は証明書から取得されます。

**すべての電子署名を取得する**

PDFドキュメント内のすべての電子署名を検証するには、PDFドキュメントから電子署名を取得します。 すべての署名がリストで返されます。 電子署名の検証の一環として、署名のステータスを確認します。

>[!NOTE]
>
>1つの電子署名を検証する場合とは異なり、複数の署名を検証する場合は、署名フィールド名を指定する必要はありません。

**すべての署名を繰り返し実行**

各署名を繰り返し処理します。 つまり、各署名について、デジタル署名を検証し、署名者のIDと各署名のステータスを確認します。 （[電子署名の検証](#verify-digital-signatures-using-the-java-api)を参照）。

>[!NOTE]
>
>ドキュメント全体が要件の場合は、すべての署名を繰り返し実行する必要はありません。

**関連トピック**

[Java APIを使用した複数の電子署名の検証](#verify-digital-signatures-using-the-java-api)

[WebサービスAPIを使用した複数の電子署名の検証](#verify-digital-signatures-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java APIを使用した複数の電子署名の検証{#verify-multiple-digital-signatures-using-the-java-api}

Signature Service API(Java)を使用して複数の電子署名を検証します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-signatures-client.jarなどのクライアントJARファイルを含めます。

1. 署名クライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `SignatureServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 検証する署名が含まれているPDFドキュメントを取得します

   * 複数の電子署名を含むPDFドキュメントを表す`java.io.FileInputStream`オブジェクトを作成し、そのコンストラクターを使用して検証します。 PDFドキュメントの場所を指定するstring値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PKIランタイムオプションの設定

   * コンストラクタを使用して `PKIOptions` オブジェクトを作成します。
   * `PKIOptions`オブジェクトの`setVerificationTime`メソッドを呼び出し、検証時刻を指定する`VerificationTime`定義済みリスト値を渡して、検証時刻を設定します。
   * `PKIOptions`オブジェクトの`setRevocationCheckStyle`メソッドを呼び出し、失効確認を実行するかどうかを指定する`RevocationCheckStyle`定義済みリスト値を渡して、失効確認オプションを設定します。

1. すべての電子署名を取得する

   `SignatureServiceClient`オブジェクトの`verifyPDFDocument`メソッドを呼び出し、次の値を渡します。

   * 複数の電子署名を含むPDFドキュメントを含む`com.adobe.idp.Document`オブジェクトです。
   * PKIランタイムオプションを含む`PKIOptions`オブジェクト。
   * SPI情報を含む`VerifySPIOptions`インスタンスです。 このパラメーターには`null`を指定できます。

   `verifyPDFDocument`メソッドは、PDFドキュメント内のすべての電子署名に関する情報を含む`PDFDocumentVerificationInfo`オブジェクトを返します。

1. すべての署名を繰り返し実行

   * `PDFDocumentVerificationInfo`オブジェクトの`getVerificationInfos`メソッドを呼び出すことで、すべての署名を繰り返します。 このメソッドは、`java.util.List`オブジェクトを返します。各要素は`PDFSignatureVerificationInfo`オブジェクトです。 署名のリストを繰り返すには、`java.util.Iterator`オブジェクトを使用します。
   * `PDFSignatureVerificationInfo`オブジェクトを使用すると、`PDFSignatureVerificationInfo`オブジェクトの`getStatus`メソッドを呼び出して、署名のステータスを特定するなどのタスクを実行できます。 このメソッドは、署名の状態を通知する静的データメンバーの`SignatureStatus`オブジェクトを返します。 例えば、署名が不明な場合、このメソッドは`SignatureStatus.DocumentSignatureUnknown`を返します。

**関連トピック**

[複数の電子署名の検証](#verifying-multiple-digital-signatures)

[クイック開始（SOAPモード）:Java APIを使用した複数の電子署名の検証](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-multiple-digital-signatures-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[電子署名の検証](#verify-digital-signatures-using-the-java-api)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#verifying-multiple-digital-signatures-using-the-web-service-api}を使用した複数の電子署名の検証

Signature Service API（Webサービス）を使用して複数の電子署名を検証します。

1. プロジェクトファイルを含める

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. 署名クライアントの作成

   * `SignatureServiceClient`オブジェクトを作成するには、そのデフォルトのコンストラクタを使用します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`SignatureServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに指定するstring値を渡します（例：`http://localhost:8080/soap/services/SignatureService?WSDL`）。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する場合に使用されます)。
   * `SignatureServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * AEM formsユーザー名をフィールド`SignatureServiceClient.ClientCredentials.UserName.UserName`に割り当てます。
      * 対応するパスワード値をフィールド`SignatureServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * 定数値`HttpClientCredentialType.Basic`をフィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に割り当てます。
      * 定数値`BasicHttpSecurityMode.TransportCredentialOnly`をフィールド`BasicHttpBindingSecurity.Security.Mode`に割り当てます。

1. 検証する署名が含まれているPDFドキュメントを取得します

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、検証する複数の電子署名を含むPDFドキュメントを保存します。
   * コンストラクターを呼び出して、`System.IO.FileStream`オブジェクトを作成します。 PDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得して、バイト配列のサイズを決定できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出して、バイト配列にストリームデータを入力します。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * `BLOB`オブジェクトに、`MTOM`プロパティにバイト配列の内容を割り当てて入力します。

1. PKIランタイムオプションの設定

   * コンストラクタを使用して `PKIOptions` オブジェクトを作成します。
   * `PKIOptions`オブジェクトの`verificationTime`データメンバに検証時刻を指定する`VerificationTime`定義済みリスト値を割り当てて、検証時刻を設定します。
   * 失効確認オプションを設定するには、`PKIOptions`オブジェクトの`revocationCheckStyle`データメンバに失効確認を実行するかどうかを指定する`RevocationCheckStyle`定義済みリスト値を割り当てます。

1. すべての電子署名を取得する

   `SignatureServiceClient`オブジェクトの`verifyPDFDocument`メソッドを呼び出し、次の値を渡します。

   * 複数の電子署名を含むPDFドキュメントを含む`BLOB`オブジェクトです。
   * PKIランタイムオプションを含む`PKIOptions`オブジェクト。
   * SPI情報を含む`VerifySPIOptions`インスタンスです。 このパラメーターにはnullを指定できます。

   `verifyPDFDocument`メソッドは、PDFドキュメント内のすべての電子署名に関する情報を含む`PDFDocumentVerificationInfo`オブジェクトを返します。

1. すべての署名を繰り返し実行

   * `PDFDocumentVerificationInfo`オブジェクトの`verificationInfos`データメンバーを取得して、すべての署名を繰り返します。 このデータメンバは、`Object`配列を返します。各要素は`PDFSignatureVerificationInfo`オブジェクトです。
   * `PDFSignatureVerificationInfo`オブジェクトを使用すると、`PDFSignatureVerificationInfo`オブジェクトの`status`データメンバを取得して、署名のステータスの特定などのタスクを実行できます。 このデータメンバは、`SignatureStatus`オブジェクトを返します。このオブジェクトの静的データメンバは、署名の状態を通知します。 例えば、署名が不明な場合、このメソッドは`SignatureStatus.DocumentSignatureUnknown`を返します。

**関連トピック**

[複数の電子署名の検証](#verifying-multiple-digital-signatures)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 電子署名の削除{#removing-digital-signatures}

新しい電子署名を適用する前に、電子署名を署名フィールドから削除する必要があります。 電子署名は上書きできません。 署名が含まれる署名フィールドに電子署名を適用しようとすると、例外が発生します。

>[!NOTE]
>
>Signatureサービスについて詳しくは、「[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)」を参照してください。

### 手順{#summary_of_steps-8}の概要

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

これらのJARファイルの場所について詳しくは、「[AEM FormsJavaライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)」を参照してください。

**署名クライアントの作成**

プログラムを使用してSignatureサービスの操作を実行する前に、Signatureサービスクライアントを作成する必要があります。

**削除する署名が含まれているPDFドキュメントの取得**

PDFドキュメントから署名を削除するには、署名が含まれるPDFドキュメントを取得する必要があります。

**署名フィールドからの電子署名の削除**

PDFドキュメントから電子署名を正しく削除するには、電子署名が含まれる署名フィールドの名前を指定する必要があります。 また、電子署名を削除する権限が必要です。それ以外の場合は、例外が発生します。

**PDFドキュメントをPDFファイルとして保存**

Signatureサービスで署名フィールドから電子署名を削除した後、PDFドキュメントをPDFファイルとして保存し、ユーザーがAcrobatまたはAdobe Readerで開けるようにすることができます。

**関連トピック**

[Java APIを使用した電子署名の削除](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-java-api)

[WebサービスAPIを使用した電子署名の削除](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[署名フィールドの追加](digitally-signing-certifying-documents.md#adding-signature-fields)

### Java API {#remove-digital-signatures-using-the-java-api}を使用した電子署名の削除

署名API(Java)を使用して電子署名を削除します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-signatures-client.jarなどのクライアントJARファイルを含めます。

1. 署名クライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `SignatureServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. 削除する署名が含まれているPDFドキュメントの取得

   * コンストラクターを使用し、PDFドキュメントの場所を指定する文字列値を渡して、削除するドキュメントが含まれるPDF署名を表す`java.io.FileInputStream`オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 署名フィールドからの電子署名の削除

   `SignatureServiceClient`オブジェクトの`clearSignatureField`メソッドを呼び出し、次の値を渡して、署名フィールドから電子署名を削除します。

   * 削除する署名が含まれているPDFドキュメントを表す`com.adobe.idp.Document`オブジェクトです。
   * 電子署名が含まれる署名フィールドの名前を指定するstring値です。

   `clearSignatureField`メソッドは、電子署名が削除されたPDFドキュメントを表す`com.adobe.idp.Document`オブジェクトを返します。

1. PDFドキュメントをPDFファイルとして保存

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が .pdf であることを確認します。
   * `com.adobe.idp.Document`オブジェクトの`copyToFile`メソッドを呼び出します。 `java.io.File`オブジェクトを渡して、`com.adobe.idp.Document`オブジェクトの内容をファイルにコピーします。 `Document` メソッドから返された `clearSignatureField` オブジェクトを必ず使用してください。

**関連トピック**

[電子署名の削除](digitally-signing-certifying-documents.md#removing-digital-signatures)

[クイック開始（SOAPモード）:Java APIを使用した電子署名の削除](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-removing-a-digital-signature-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#remove-digital-signatures-using-the-web-service-api}を使用した電子署名の削除

Signature API（Webサービス）を使用して電子署名を削除します。

1. プロジェクトファイルを含める

   MTOMを使用するMicrosoft .NETプロジェクトを作成します。 次のWSDL定義を使用していることを確認します。`http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`を、AEM FormsをホストするサーバーのIPアドレスに置き換えます。

1. 署名クライアントの作成

   * `SignatureServiceClient`オブジェクトを作成するには、そのデフォルトのコンストラクタを使用します。
   * `System.ServiceModel.EndpointAddress`コンストラクターを使用して`SignatureServiceClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに指定するstring値を渡します（例：`http://localhost:8080/soap/services/SignatureService?WSDL`）。 `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する場合に使用されます)。
   * `SignatureServiceClient.Endpoint.Binding`フィールドの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
   * `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`フィールドを`WSMessageEncoding.Mtom`に設定します。 この値により、MTOMが使用されます。
   * 次のタスクを実行して、基本的なHTTP認証を有効にします。

      * AEM formsユーザー名をフィールド`SignatureServiceClient.ClientCredentials.UserName.UserName`に割り当てます。
      * 対応するパスワード値をフィールド`SignatureServiceClient.ClientCredentials.UserName.Password`に割り当てます。
      * 定数値`HttpClientCredentialType.Basic`をフィールド`BasicHttpBindingSecurity.Transport.ClientCredentialType`に割り当てます。
      * 定数値`BasicHttpSecurityMode.TransportCredentialOnly`をフィールド`BasicHttpBindingSecurity.Security.Mode`に割り当てます。

1. 削除する署名が含まれているPDFドキュメントの取得

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、削除する電子署名を含むPDFドキュメントを保存するために使用します。
   * コンストラクターを呼び出し、署名済みPDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得して、バイト配列のサイズを決定できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出して、バイト配列にストリームデータを入力します。 読み取るバイト配列、開始位置、ストリーム長を渡します。
   * `BLOB`オブジェクトに`MTOM`プロパティを割り当て、バイト配列の内容を指定します。

1. 署名フィールドからの電子署名の削除

   `SignatureServiceClient`オブジェクトの`clearSignatureField`メソッドを呼び出し、次の値を渡して、デジタル署名を削除します。

   * 署名済みPDFドキュメントを含む`BLOB`オブジェクトです。
   * 削除する電子署名が含まれている署名フィールドの名前を表すstring値です。

   `clearSignatureField`メソッドは、電子署名が削除されたPDFドキュメントを表す`BLOB`オブジェクトを返します。

1. PDFドキュメントをPDFファイルとして保存

   * コンストラクターを呼び出し、空の署名フィールドとファイルを開くモードを含むPDFドキュメントのファイルの場所を表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `sign`メソッドから返された`BLOB`オブジェクトの内容を格納するバイト配列を作成します。 `BLOB`オブジェクトの`MTOM`データメンバの値を取得して、バイト配列を入力します。
   * コンストラクターを呼び出して`System.IO.FileStream`オブジェクトを渡し、`System.IO.BinaryWriter`オブジェクトを作成します。
   * `System.IO.BinaryWriter`オブジェクトの`Write`メソッドを呼び出し、バイト配列を渡すことで、バイト配列の内容をPDFファイルに書き込みます。

**関連トピック**

[電子署名の削除](digitally-signing-certifying-documents.md#removing-digital-signatures)

[MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRefを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
