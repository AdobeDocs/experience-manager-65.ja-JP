---
title: ドキュメントのデジタル署名と認証
description: Signature サービスを使用して、PDF ドキュメントに対するデジタル署名フィールドの追加と削除、PDF ドキュメント内の署名フィールドの名前の取得、署名フィールドの変更、PDF ドキュメントのデジタル署名、PDF ドキュメント内の認証、PDF ドキュメント内にあるデジタル署名の検証、PDF ドキュメント内にあるすべてのデジタル署名の検証および署名フィールドからデジタル署名の削除を行います。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: c200f345-40ab-46fd-b6ed-f3af0a23796b
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '17045'
ht-degree: 85%

---

# ドキュメントのデジタル署名と認証 {#digitally-signing-and-certifying-documents}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

**Signature サービスについて**

Signature サービスを使用して、組織は配布する PDF ドキュメントおよび受信する PDF ドキュメントのセキュリティとプライバシーを保護できます。このサービスでは、デジタル署名と証明書を使用して、意図された受信者のみがドキュメントを変更できるようにします。セキュリティ機能がドキュメント自体に適用されるので、ドキュメントは安全で、ライフサイクル全体にわたって制御されます。ドキュメントは、ファイアウォール外でも、オフラインでダウンロードされた場合でも、組織に送り返される場合であったとしても、保護された状態を維持します。

>[!NOTE]
>
>PDF ドキュメントへの署名など、特定の操作の呼び出し時に呼び出される Signature サービス用のカスタム署名ハンドラーを作成できます。

**署名フィールド名**

一部の Signature サービス操作では、操作を実行する署名フィールドの名前を指定する必要があります。例えば、PDF ドキュメントに署名する場合、署名する署名フィールドの名前を指定します。署名フィールドのフルネームが `form1[0].Form1[0].SignatureField1[0]` であるとします。`form1[0].Form1[0].SignatureField1[0]` の代わりに `SignatureField1[0]` を指定できます。

競合が原因で、Signature サービスが誤ったフィールドに署名する（または、署名フィールド名を必要とする別の操作を実行する）ことがあります。この競合は同じ PDF ドキュメント内で 2 つ以上の場所に表示される `SignatureField1[0]` という名前の原因です。例えば、PDF ドキュメントに、`form1[0].Form1[0].SignatureField1[0]`および`form1[0].Form1[0].SubForm1[0].SignatureField1[0]`という ２ つの署名フィールドが含まれ、`SignatureField1[0]`を指定するとします。この場合、Signature サービスは、ドキュメント内のすべての署名フィールドを繰り返し検索している間に検出された最初の署名フィールドに署名します。

PDF ドキュメント内に複数の署名フィールドがある場合は、署名フィールドのフルネームを指定することをお勧めします。つまり、`SignatureField1[0]` の代わりに `form1[0].Form1[0].SignatureField1[0]` を指定します。

Signature サービスを使用して、次のタスクを実行できます。

* PDF ドキュメントへのデジタル署名フィールドの追加および削除を行います。（[署名フィールドの追加](digitally-signing-certifying-documents.md#adding-signature-fields)を参照してください）。
* PDF ドキュメント内の署名フィールドの名前を取得します。（[署名フィールド名の取得](digitally-signing-certifying-documents.md#retrieving-signature-field-names)を参照してください）。
* 署名フィールドを変更します。（[署名フィールドの変更](digitally-signing-certifying-documents.md#modifying-signature-fields)を参照してください）。
* PDF ドキュメントにデジタル署名を行います。（[PDF ドキュメントへのデジタル署名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)を参照してください）。
* PDF ドキュメントを認証します。（[PDF ドキュメントの認証](digitally-signing-certifying-documents.md#certifying-pdf-documents)を参照してください）。
* PDF ドキュメント内のデジタル署名を検証します。（[電子署名の検証](digitally-signing-certifying-documents.md#verifying-digital-signatures)を参照してください。）
* PDF ドキュメント内のすべてのデジタル署名を検証します。（[複数のデジタル署名の検証](digitally-signing-certifying-documents.md#verifying-digital-signatures)を参照してください。）
* 署名フィールドからデジタル署名を削除します。（[電子署名の削除](digitally-signing-certifying-documents.md#removing-digital-signatures)を参照してください。）

>[!NOTE]
>
>Signature サービスについて詳しくは、[AEM Forms サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

## 署名フィールドの追加 {#adding-signature-fields}

デジタル署名は、署名の画像表示を含むフォームフィールドである署名フィールドに表示されます。署名フィールドは、表示または非表示に設定することができます。署名者は既存の署名フィールドを使用することができます。また、プログラムによって署名フィールドを追加することもできます。どちらの場合においても、PDF ドキュメントに署名するには、署名フィールドが存在している必要があります。

プログラムによって署名フィールドを追加するには、Signature サービス Java API や 署名 Web サービス API を使用します。PDF ドキュメントに複数の署名フィールドを追加できます。ただし、各署名フィールド名は一意である必要があります。

>[!NOTE]
>
>一部の PDF ドキュメントタイプでは、プログラムによって署名フィールドを追加することができません。Signature サービスと署名フィールドの追加について詳しくは、[AEM Forms サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary-of-steps}

PDF ドキュメントに署名フィールドを追加するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Signature クライアントを作成します。
1. 署名フィールドが追加された PDF ドキュメントを取得します。
1. 署名フィールドを追加します。
1. PDF ドキュメントを PDF ファイルとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar（AEM Forms が JBoss にデプロイされている場合に必要）
* jbossall-client.jar（AEM Formsが JBoss にデプロイされている場合に必要）

**Signature クライアントの作成**

Signature サービスの操作をプログラムで実行する前に、Signature サービスクライアントを作成する必要があります。

**署名フィールドが追加された PDF ドキュメントを取得する**

署名フィールドを追加した PDF ドキュメントを取得する必要があります。

**署名フィールドを追加する**

PDFドキュメントに正常に署名フィールドを追加するには、署名フィールドの場所を特定する座標値を指定します。（非表示の署名フィールドを追加する場合、これらの値は不要です）。また、署名が署名フィールドに適用された後にロックされる PDF ドキュメント内のフィールドを指定することもできます。

**PDF ドキュメントを PDF ファイルとして保存する**

Signature サービスが PDF ドキュメントに署名フィールドを追加した後、そのドキュメントを PDF ファイルとして保存すると、ユーザーは、Acrobat または Adobe Reader でそのドキュメントを開くことができます。

**関連トピック**

[AEM Forms Java ライブラリファイルの組み込み](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDF ドキュメントの電子署名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### Java API を使用した署名フィールドの追加 {#add-signature-fields-using-the-java-api}

Signature API (Java) を使用して署名フィールドを追加します。

1. プロジェクトファイルを含める

   Java プロジェクトのクラスパスに、adobe-signatures-client.jar などのクライアント JAR ファイルを含めます。

1. Signature クライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * `SignatureServiceClient` オブジェクトを作成するには、コンストラクタを使用して、`ServiceClientFactory` オブジェクトを渡します。

1. 署名フィールドが追加された PDF ドキュメントを取得する

   * 署名フィールドが追加された PDF ドキュメントを表す `java.io.FileInputStream` オブジェクトを作成するには、コンストラクタを使用して、PDF ドキュメントの場所を指定する文字列値を渡してください。
   * `com.adobe.idp.Document` オブジェクトを作成するには、コンストラクタを使用して、`java.io.FileInputStream` オブジェクトを渡します。

1. 署名フィールドを追加する

   * コンストラクタを使用して、署名フィールドの場所を指定する `PositionRectangle` オブジェクトを作成します。コンストラクタ内で、座標値を指定します。
   * 必要に応じて、デジタル署名が署名フィールドに適用された際にロックするフィールドを指定する `FieldMDPOptions` オブジェクトを作成します。
   * を呼び出して、PDFドキュメントに署名フィールドを追加する `SignatureServiceClient` オブジェクトの `addSignatureField` メソッドを使用して、次の値を渡します。

      * `com.adobe.idp` です。署名フィールドを追加する PDF ドキュメントを表す `Document` オブジェクトです。
      * 署名フィールドの名前を指定する文字列値です。
      * 署名フィールドを追加するページ番号を表す `java.lang.Integer` 値です。
      * 署名フィールドの場所を指定する `PositionRectangle` オブジェクトです。
      * デジタル署名が署名フィールドに適用された後にロックされる PDF ドキュメント内のフィールドを指定する `FieldMDPOptions` オブジェクトです。このパラメータ値はオプションで、 `null` を渡すことができます。

   * 様々な実行時の値を指定する `PDFSeedValueOptions` オブジェクトです。このパラメータ値はオプションで、 `null` を渡すことができます。

     `addSignatureField` メソッドは `com.adobe.idp` を返します。署名フィールドを含む PDF ドキュメントを表す`Document`オブジェクトです。

   >[!NOTE]
   >
   >を呼び出すことができます。 `SignatureServiceClient` オブジェクトの `addInvisibleSignatureField` メソッドを使用して、非表示の署名フィールドを追加します。

1. PDFドキュメントを PDF ファイルとして保存する

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が .pdf であることを確認します。
   *  `com.adobe.idp` を呼び出します。`Document` オブジェクトの `copyToFile` メソッドを使用して、 `Document` オブジェクトをファイルに追加します。 必ず `com.adobe.idp` を使用してください。`addSignatureField` メソッドによって返された `Document`オブジェクトです。

**関連トピック**

[Signature サービス API クイックスタート](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

### Web サービス API を使用して署名フィールドを追加する {#add-signature-fields-using-the-web-service-api}

Signature API（Web サービス）を使用して署名フィールドを追加するには：

1. プロジェクトファイルを含める

   MTOM を使用する Microsoft .NET プロジェクトを作成します。WSDL 定義 `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1` を使用するようにします。

   >[!NOTE]
   >
   >`localhost` を、AEM Forms をホストするサーバーの IP アドレスに置き換えてください。

1. Signature クライアントの作成

   * デフォルトのコンストラクターを使用して `SignatureServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して`SignatureServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を 指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/SignatureService?WSDL`）。`lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。
   * `SignatureServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * を設定します。 `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `SignatureServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `SignatureServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
      * フィールド `BasicHttpBindingSecurity.Security.Mode` に定数値 `BasicHttpSecurityMode.TransportCredentialOnly` を割り当てます。

1. 署名フィールドが追加された PDF ドキュメントを取得する

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB` オブジェクトは、署名フィールドを含む PDF ドキュメントを保存するために使用されます。
   * `System.IO.FileStream` オブジェクトを作成するには、コンストラクターを呼び出して、PDF ドキュメントのファイルの場所を表す文字列値とファイルを開くモードを渡します。
   * `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッドを使用し、読み込むバイト配列、開始位置、ストリームの長さを渡す。
   * `BLOB` オブジェクトを入力するには、`MTOM` プロパティにバイト配列のコンテンツを割り当てます。

1. 署名フィールドを追加する

   を呼び出して、PDFドキュメントに署名フィールドを追加する `SignatureServiceClient` オブジェクトの `addSignatureField` メソッドを使用して、次の値を渡します。

   * 署名フィールドが追加された PDF ドキュメントを表す `BLOB` オブジェクトです。
   * 署名フィールド名を指定する文字列値です。
   * 署名フィールドを追加するページ番号を表す整数値です。
   * 署名フィールドの場所を指定する `PositionRect` オブジェクトです。
   * デジタル署名が署名フィールドに適用された後にロックされる PDF ドキュメント内のフィールドを指定する `FieldMDPOptions` オブジェクトです。このパラメータ値はオプションで、 `null` を渡すことができます。
   * 様々な実行時の値を指定する `PDFSeedValueOptions` オブジェクトです。このパラメータ値はオプションで、`null`を渡すことができます。

   `addSignatureField` メソッドは、署名フィールドを含む PDF ドキュメントを表す `BLOB` オブジェクトを返します。

1. PDFドキュメントを PDF ファイルとして保存する

   * `System.IO.FileStream` オブジェクトを作成するには、コンストラクターを呼び出して、署名フィールドを含む PDF ドキュメントのファイルの場所を表す文字列値およびファイルを開くモードを渡します。
   * `addSignatureField` メソッドによって返された `BLOB` オブジェクトのコンテンツを格納するバイト配列を作成します。バイト配列を生成するには、 `BLOB` オブジェクトの `binaryData` データメンバー。
   * コンストラクターを呼び出して `System.IO.FileStream` オブジェクトを渡すことによって、`System.IO.BinaryWriter` オブジェクトを作成します。
   * を呼び出して、バイト配列の内容をPDFファイルに書き込みます。 `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを使用してバイト配列を渡す。

**関連トピック**

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 署名フィールド名の取得 {#retrieving-signature-field-names}

署名または認証する署名ドキュメント内のすべてのPDFフィールドの名前を取得できます。 PDFドキュメント内の署名フィールド名が不明な場合や、名前を検証する場合は、プログラムを使用して名前を取得できます。 Signature サービスは、`form1[0].grantApplication[0].page1[0].SignatureField1[0]` のような署名フィールドの完全修飾名を返します。

>[!NOTE]
>
>Signature サービスについて詳しくは、[AEM Forms サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary_of_steps-1}

署名フィールド名を取得するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Signature クライアントを作成します。
1. 署名フィールドを含む PDF ドキュメントを取得します。
1. 署名フィールド名を取得します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar（AEM Forms が JBoss にデプロイされている場合に必要）
* jbossall-client.jar（AEM Formsが JBoss にデプロイされている場合に必要）

これらの JAR ファイルの場所については、[AEM Forms Java ライブラリファイルの組み込み](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。

**署名クライアントの作成**

Signature サービスの操作をプログラムで実行する前に、Signature サービスクライアントを作成する必要があります。

**署名フィールドを含む PDF ドキュメントを取得する**

署名フィールドを含む PDF ドキュメントを取得します。

**署名フィールド名の取得**

1 つ以上の署名フィールドを含む PDF ドキュメントを取得した後に、署名フィールド名を取得できます。

**関連トピック**

[Java API を使用した署名フィールド名の取得](digitally-signing-certifying-documents.md#retrieve-signature-field-names-using-the-java-api)

[Web サービス API を使用した署名フィールドの取得](digitally-signing-certifying-documents.md#retrieve-signature-field-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[署名フィールドの追加](digitally-signing-certifying-documents.md#adding-signature-fields)

### Java API を使用した署名フィールド名の取得 {#retrieve-signature-field-names-using-the-java-api}

Signature API (Java) を使用して署名フィールド名を取得します。

1. プロジェクトファイルを含める

   Java プロジェクトのクラスパスに、 adobe-signatures-client.jar などのクライアント JAR ファイルを含めます。

1. Signature クライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `ServiceClientFactory` オブジェクトを渡すことによって、`SignatureServiceClient` オブジェクトを作成します。

1. 署名フィールドを含む PDF ドキュメントを取得する

   * 署名フィールドを含む PDF ドキュメントを表す `java.io.FileInputStream` オブジェクトを作成するには、コンストラクターを使用し、PDF ドキュメントの場所を指定する文字列値を渡します。
   * コンストラクタを使用して`java.io.FileInputStream` オブジェクトを渡すことによって、`com.adobe.idp.Document` オブジェクトを作成します。

1. 署名フィールド名の取得

   * を呼び出して、署名フィールド名を取得します。 `SignatureServiceClient` オブジェクトの `getSignatureFieldList` メソッドおよび `com.adobe.idp.Document` 署名フィールドを含むPDFドキュメントを格納するオブジェクト。 このメソッドは、各要素に `PDFSignatureField` オブジェクトをが含まれる `java.util.List` オブジェクトを返します。このオブジェクトを使用すると、署名フィールドが表示されているかどうかなど、署名フィールドに関する追加情報を取得できます。
   * `java.util.List` オブジェクトを繰り返して、署名フィールド名があるかどうかを確認します。PDF ドキュメントの各署名フィールドに対して、個別の `PDFSignatureField` オブジェクトを取得できます。署名フィールドの名前を取得するには、 `PDFSignatureField` オブジェクトの `getName` メソッド。 このメソッドは、署名フィールド名を指定する文字列値を返します。

**関連トピック**

[署名フィールド名の取得](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[クイックスタート（SOAP モード）：Java API を使用した署名フィールド名の取得](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-retrieving-signature-field-names-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用した署名フィールドの取得 {#retrieve-signature-field-using-the-web-service-api}

Signature API（Web サービス）を使用して署名フィールド名を取得します。

1. プロジェクトファイルを含める

   MTOM を使用する Microsoft .NET プロジェクトを作成します。WSDL 定義 `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1` を使用するようにします。

   >[!NOTE]
   >
   >`localhost` を、AEM Forms をホストするサーバーの IP アドレスに置き換えてください。

1. Signature クライアントの作成

   * デフォルトのコンストラクターを使用して `SignatureServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して`SignatureServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を 指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/SignatureService?WSDL`）。`lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。
   * `SignatureServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * を設定します。 `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `SignatureServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `SignatureServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
      * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` をフィールド `BasicHttpBindingSecurity.Security.Mode` に割り当てます。

1. 署名フィールドを含む PDF ドキュメントを取得する

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB` オブジェクトは、署名フィールドを含む PDF ドキュメントを保存するために使用されます。
   * `System.IO.FileStream` オブジェクトを作成するには、コンストラクタを呼び出して、PDF ドキュメントのファイルの場所を表す文字列値およびファイルを開くモードを渡します。
   * `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッドを使用し、読み込むバイト配列、開始位置、ストリームの長さを渡す。
   * `BLOB` オブジェクトを入力するには、`MTOM` フィールドにバイト配列のコンテンツを割り当てます。

1. 署名フィールド名の取得

   * を呼び出して署名フィールド名を取得する `SignatureServiceClient` オブジェクトの `getSignatureFieldList` メソッドおよび `BLOB` 署名フィールドを含むPDFドキュメントを格納するオブジェクト。 このメソッドは、各要素に `PDFSignatureField` オブジェクトを含む `MyArrayOfPDFSignatureField` コレクションオブジェクトを返します。
   * `MyArrayOfPDFSignatureField` オブジェクトを繰り返して、署名フィールド名があるかどうかを確認します。PDF ドキュメントの各署名フィールドに対して、`PDFSignatureField` オブジェクトを取得できます。署名フィールドの名前を取得するには、 `PDFSignatureField` オブジェクトの `getName` メソッド。 このメソッドは、署名フィールド名を指定する文字列値を返します。

**関連トピック**

[署名フィールド名の取得](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 署名フィールドの変更 {#modifying-signature-fields}

Java API と web サービス API を使用して、PDF ドキュメント内の署名フィールドを変更できます。署名フィールドの署名フィールドロックディクショナリまたはシード値ディクショナリの値を操作することで署名フィールドを変更します。

*フィールドロックディクショナリ*&#x200B;は、署名フィールドへの署名時にロックするフィールドのリストを指定します。フィールドがロックされると、ユーザーはフィールドを変更できません。*シード値ディクショナリ*&#x200B;には、署名の適用時に使用される制約情報が含まれます。例えば、署名を無効にすることなく実行できるアクションを制御する権限設定を変更することができます。

既存の署名フィールドを変更することで、PDF ドキュメントに対して変更を加えて、ビジネス要件の変更を反映させることができます。例えば、新しいビジネス要件ではドキュメントに署名が行われた後にすべてのドキュメントフィールドをロックしなければいけない場合などです。

このセクションでは、フィールドロックディクショナリとシード値ディクショナリの値の両方を修正して署名フィールドを変更する方法について説明します。署名フィールドロックディクショナリに変更を加えると、PDF ドキュメント内のすべてのフィールドが、署名フィールドに署名する際にロックされます。シード値ディクショナリを変更すると、ドキュメントに対する特定の種類の変更が禁止されます。

>[!NOTE]
>
>Signature サービスと署名フィールドの変更について詳しくは、[AEM Forms サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary_of_steps-2}

PDF ドキュメント内の署名フィールドを変更するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Signature クライアントを作成します。
1. 変更する署名フィールドを含む PDF ドキュメントを取得します。
1. ディクショナリの値を設定します。
1. 署名フィールドを変更します。
1. PDF ドキュメントを PDF ファイルとして保存します。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar（AEM Forms が JBoss にデプロイされている場合に必要）
* jbossall-client.jar（AEM Formsが JBoss にデプロイされている場合に必要）

これらの JAR ファイルの場所については、[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。

**Signature クライアントの作成**

Signature サービスの操作をプログラムで実行する前に、Signature サービスクライアントを作成する必要があります。

**変更する署名フィールドを含む PDF ドキュメントを取得**

変更する署名フィールドを含む PDF ドキュメントを取得します。

**ディクショナリの値を設定**

署名フィールドを変更するには、そのフィールドロックディクショナリまたはシード値ディクショナリに値を割り当てます。署名フィールドのロックディクショナリ値を指定するには、署名フィールドが署名された際にロックする PDF ドキュメントフィールドを指定します（このセクションでは、すべてのフィールドをロックする方法について説明します）。

次のシード値ディクショナリ値を設定できます。

* **リビジョンの確認**：署名フィールドに署名が適用された場合に失効確認を実行するかどうかを指定します。
* **証明書オプション**：証明書のシード値ディクショナリに値を割り当てます。証明書のオプションを指定する前に、証明書のシード値ディクショナリに慣れておくことをお勧めします。（[PDF リファレンス](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf)を参照してください）。
* **ダイジェストオプション**：署名に使用するダイジェストアルゴリズムを割り当てます。有効な値は 、SHA1、SHA256、SHA384、SHA512 および RIPEMD160 です。
* **フィルター**：署名フィールドで使用するフィルタを指定します。例えば、Adobe.PPKLite フィルターを使用できます。（[PDF リファレンス](https://www.adobe.com/devnet/acrobat/pdfs/pdf_reference_1-7.pdf)を参照してください）。
* **フラグオプション**：この署名フィールドに関連付けられているフラグ値を指定します。値が 1 の場合、署名者は指定された値のみをエントリに使用する必要があります。値が 0 の場合、他の値も許可されています。ビット位置は次のとおりです。

   * **1（フィルター）：**&#x200B;署名フィールドへの署名に使用する署名ハンドラー
   * **2（サブフィルタ）：**&#x200B;署名時に使用する有効なエンコードを示す名前の配列
   * **3 (V)**：署名フィールドへの署名に使用される署名ハンドラーの必要最小限のバージョン番号
   * **4 （理由）：**&#x200B;ドキュメントに署名する理由を指定する文字列の配列
   * **5（PDFLegalWarnings）：**&#x200B;可能な法的証明を指定する文字列の配列

* **法的証明**：ドキュメントを認証すると、ドキュメントの表示内容をあいまいにしたり誤解を招く可能性のある特定の種類のコンテンツが自動的にスキャンされます。例えば、注釈により、認証される対象を把握するために重要なテキストが隠れてしまう場合があります。スキャン処理により、こうした種類のコンテンツの存在を示す警告が生成されます。また、警告が発生した可能性のあるコンテンツに関する追加の説明も提供されます。
* **権限**：署名を無効にせずに、PDF ドキュメントで使用できる権限を指定します。
* **理由**：このドキュメントに署名する理由を指定します。
* **タイムスタンプ**：タイムスタンプオプションを指定します。例えば、使用するタイムスタンプサーバーの URL を設定できます。
* **バージョン**：署名フィールドへの署名に使用する署名ハンドラーの最小バージョン番号を指定します。

**署名フィールドの変更**

Signature サービスクライアントを作成し、変更する署名フィールドが含まれている PDF ドキュメントを取得し、ディクショナリの値を設定した後、Signature サービスに対して、署名フィールドを変更するように指示できます。次に、Signature サービスは、変更された署名フィールドを含む PDF ドキュメントを返します。元の PDF ドキュメントは影響を受けません。

**PDF ドキュメントを PDF ファイルとして保存**

変更された署名フィールドを含む PDF ドキュメントを PDF ファイルとして保存すると、ユーザーは Acrobat または Adobe Reader で開くことができます。

**関連トピック**

[AEM Forms Java ライブラリファイルの組み込み](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Signature サービス API クイックスタート](/help/forms/developing/signature-service-java-api-quick.md#signature-service-java-api-quick-start-soap)

[PDF ドキュメントの電子署名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

### Java API を使用した署名フィールドの変更 {#modify-signature-fields-using-the-java-api}

Signature API（Java）を使用して署名フィールドを変更します。

1. プロジェクトファイルを含める

   Java プロジェクトのクラスパスに、adobe-signatures-client.jar などのクライアント JAR ファイルを含めます。

1. Signature クライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `ServiceClientFactory` オブジェクトを渡すことによって、`SignatureServiceClient` オブジェクトを作成します。

1. 変更する署名フィールドを含む PDF ドキュメントを取得

   * 変更する署名フィールドを含む PDF ドキュメントを表す `java.io.FileInputStream` オブジェクトを作成するには、コンストラクタを使用し、PDF ドキュメントの場所を指定する文字列値を渡します。
   * コンストラクタを使用して `java.io.FileInputStream` オブジェクトを渡すことによって、`com.adobe.idp.Document` オブジェクトを作成します。

1. ディクショナリの値を設定

   * コンストラクタを使用して `PDFSignatureFieldProperties` オブジェクトを作成します。`PDFSignatureFieldProperties` オブジェクトは、署名フィールドロックディクショナリとシード値ディクショナリ情報を格納します。
   * コンストラクタを使用して `PDFSeedValueOptionSpec` オブジェクトを作成します。このオブジェクトを使用すると、シード値ディクショナリの値を設定できます。
   * を呼び出して、PDFドキュメントの変更を許可しない `PDFSeedValueOptionSpec` オブジェクトの `setMdpValue` メソッドおよび `MDPPermissions.NoChanges` 列挙値。
   * コンストラクタを使用して `FieldMDPOptionSpec` オブジェクトを作成します。このオブジェクトを使用すると、署名フィールドのロックディクショナリ値を設定できます。
   * を呼び出して、PDFドキュメント内のすべてのフィールドをロックする `FieldMDPOptionSpec` オブジェクトの `setMdpValue` メソッドおよび `FieldMDPAction.ALL` 列挙値。
   * を呼び出して、シード値のディクショナリ情報を設定します。 `PDFSignatureFieldProperties` オブジェクトの `setSeedValue` メソッドおよび `PDFSeedValueOptionSpec` オブジェクト。
   * を呼び出して、署名フィールドロック辞書情報を設定します。 `PDFSignatureFieldProperties`オブジェクトの `setFieldMDP` メソッドおよび `FieldMDPOptionSpec` オブジェクト。

   >[!NOTE]
   >
   >設定可能なすべてのシード値ディクショナリの値を確認するには、 `PDFSeedValueOptionSpec` クラスリファレンスを参照してください。（[AEM Forms API リファレンス](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ja)を参照してください）。

1. 署名フィールドの変更

   を呼び出して署名フィールドを変更する `SignatureServiceClient` オブジェクトの `modifySignatureField` メソッドを使用して、次の値を渡します。

   * 変更する署名フィールドを含む PDFドキュメントを格納する `com.adobe.idp.Document` オブジェクト
   * 署名フィールドの名前を指定する文字列値
   * 署名フィールドロックディクショナリとシード値ディクショナリ情報を格納する `PDFSignatureFieldProperties` オブジェクト

   `modifySignatureField` メソッドは、変更された署名フィールドを含む PDF ドキュメントを保存する `com.adobe.idp.Document` オブジェクトです。

1. PDFドキュメントを PDF ファイルとして保存する

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が .pdf であることを確認します。
   * を呼び出す `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを使用して、 `com.adobe.idp.Document` オブジェクトをファイルに追加します。 必ず `modifySignatureField` メソッドが返した `com.adobe.idp.Document` オブジェクトを使用するように確認します。

### Web サービス API を使用した署名フィールドの変更 {#modify-signature-fields-using-the-web-service-api}

Signature API（web サービス）を使用して署名フィールドを変更します。

1. プロジェクトファイルを含める

   MTOM を使用する Microsoft .NET プロジェクトを作成します。WSDL 定義 `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1` を使用するようにします。

   >[!NOTE]
   >
   >`localhost` を、AEM Forms をホストするサーバーの IP アドレスに置き換えてください。

1. Signature クライアントの作成

   * デフォルトのコンストラクターを使用して `SignatureServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して`SignatureServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を 指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/SignatureService?WSDL`）。`lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。
   * `SignatureServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * を設定します。 `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `SignatureServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `SignatureServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
      * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` をフィールド `BasicHttpBindingSecurity.Security.Mode` に割り当てます。

1. 変更する署名フィールドを含む PDF ドキュメントを取得

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB` オブジェクトは、変更する署名フィールドを含む PDF ドキュメントを保存するために使用されます。
   * `System.IO.FileStream` オブジェクトを作成するには、コンストラクタを呼び出して、PDF ドキュメントのファイル場所を示す文字列値およびファイルを開くモードを渡します。
   * `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッドを使用し、読み込むバイト配列、開始位置、ストリームの長さを渡す。
   * `BLOB` オブジェクトを入力するには、`MTOM` プロパティに、バイト配列のコンテンツを割り当てます。

1. ディクショナリの値を設定

   * コンストラクタを使用して `PDFSignatureFieldProperties` オブジェクトを作成します。このオブジェクトは、署名フィールドロックディクショナリとシード値ディクショナリ情報を格納します。
   * コンストラクタを使用して `PDFSeedValueOptionSpec` オブジェクトを作成します。このオブジェクトを使用すると、シード値ディクショナリの値を設定できます。
   * 割り当てによるPDFドキュメントの変更を許可しない `MDPPermissions.NoChanges` 列挙値を `PDFSeedValueOptionSpec` オブジェクトの `mdpValue` データメンバー。
   * コンストラクタを使用して `FieldMDPOptionSpec` オブジェクトを作成します。このオブジェクトを使用すると、署名フィールドのロックディクショナリ値を設定できます。
   * 割り当てによってPDFドキュメント内のすべてのフィールドをロックする `FieldMDPAction.ALL` 列挙値を `FieldMDPOptionSpec` オブジェクトの `mdpValue` データメンバー。
   * シード値ディクショナリ情報を設定するには、 `PDFSeedValueOptionSpec` オブジェクトを `PDFSignatureFieldProperties` オブジェクトの `seedValue` データメンバー。
   * 署名フィールドロック辞書情報を設定するには、 `FieldMDPOptionSpec` オブジェクトを `PDFSignatureFieldProperties` オブジェクトの `fieldMDP` データメンバー。

   >[!NOTE]
   >
   >設定可能なすべてのシード値ディクショナリの値を表示するには、`PDFSeedValueOptionSpec` クラスレファレンスを参照してください。（[AEM Forms API リファレンス](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ja) を参照してください）。

1. 署名フィールドの変更

   を呼び出して署名フィールドを変更する `SignatureServiceClient` オブジェクトの `modifySignatureField` メソッドを使用して、次の値を渡します。

   * 変更する署名フィールドを含む PDFドキュメントを格納する `BLOB` オブジェクト
   * 署名フィールドの名前を指定する文字列値
   * 署名フィールドロックディクショナリとシード値ディクショナリ情報を格納する `PDFSignatureFieldProperties` オブジェクト

   `modifySignatureField` メソッドは、変更された署名フィールドを含む PDF ドキュメントを保存する `BLOB` オブジェクトです。

1. PDFドキュメントを PDF ファイルとして保存する

   * コンストラクターを呼び出し、署名フィールドを含む PDF ドキュメントのファイルの場所とファイルを開くモードを表す文字列値を渡して、`System.IO.FileStream` オブジェクトを作成します。
   * `addSignatureField` メソッドが返す `BLOB` オブジェクトのコンテンツを格納するバイト配列を作成します。バイト配列を生成するには、 `BLOB` オブジェクトの `MTOM` データメンバー。
   * コンストラクターを呼び出して `System.IO.FileStream` オブジェクトを渡すことによって、`System.IO.BinaryWriter` オブジェクトを作成します。
   * を呼び出して、バイト配列の内容をPDFファイルに書き込みます。 `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを使用してバイト配列を渡す。

**関連トピック**

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## PDF ドキュメントの電子署名 {#digitally-signing-pdf-documents}

デジタル署名を PDF ドキュメントに適用して、一定レベルのセキュリティを提供できます。デジタル署名は、手書きの署名と同様に、署名者が自分自身を識別し、ドキュメントに関するステートメントを作成する手段を提供します。ドキュメントに電子署名を行う技術は、署名者と受信者の両方が、何が署名されたかを明確にし、ドキュメントが署名後に変更されなかったことを確実に示すのに役立ちます。

PDFドキュメントは、公開鍵技術によって署名されます。 署名者には、公開鍵と秘密鍵の 2 つの鍵があります。 秘密鍵は、署名時に使用可能である必要があるユーザーの資格情報に保存されます。 公開鍵はユーザーの証明書に保存されます。この証明書は、受信者が署名を検証するために使用できる必要があります。 失効した証明書に関する情報は、証明機関 (CA) から配布された証明書失効リスト (CRL) およびオンライン証明書ステータスプロトコル (OCSP) 応答に含まれています。 署名時刻は、タイムスタンプ機関と呼ばれる、信頼できるソースから取得できます。

>[!NOTE]
>
>PDF ドキュメントに電子署名する前に、AEM Forms に証明書を追加していることを確認する必要があります。証明書は、管理コンソールを使用して、または Trust Manager API を使用してプログラムで追加されます。（[Trust Manager API を使用した資格情報の読み込み](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api)を参照してください。）

プログラムで PDF ドキュメントにデジタル署名できます。PDF ドキュメントに電子署名する場合、AEM Forms に存在するセキュリティ資格情報を参照する必要があります。資格情報は署名に使用する秘密鍵となります。

Signature サービスは、PDF ドキュメントに署名する際に、次の手順を実行します。

1. Signature サービスは、リクエストで指定されたエイリアスを渡すことにより、Truststore から資格情報を取得します。
1. Truststore は指定した資格情報を検索します。
1. 資格情報が Signature サービスに返され、ドキュメントへの署名に使用されます。また、資格情報は、将来のリクエストのためにエイリアスに対してキャッシュされます。

セキュリティ資格情報の取り扱いについては、アプリケーションサーバーの *AEM Forms のインストールとデプロイ* ガイドを参照してください。

>[!NOTE]
>
>ドキュメントに署名することと認証することには違いがあります。（[PDF ドキュメントの認証](digitally-signing-certifying-documents.md#certifying-pdf-documents) を参照してください。）

>[!NOTE]
>
>署名をサポートしていない PDF ドキュメントもあります。Signature サービスとドキュメントへの電子署名について詳しくは、[AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

>[!NOTE]
>
>Signature サービスは、ドキュメントの認証など、操作への入力として PDF データが埋め込まれた XDP ファイルをサポートしていません。このアクションにより、Signature サービスは `PDFOperationException` をスローします。この問題を解決するには、PDF Utilities サービスを使用して XDP ファイルを PDF ファイルに変換し、変換された PDF ファイルを Signature サービスの操作に渡します。（[PDF Utilities の操作](/help/forms/developing/pdf-utilities.md#working-with-pdf-utilities)を参照してください。）

**nCipher nShield HSM 資格情報**

PDF ドキュメントの署名や認証に nCipher nShield HSM 資格情報を使用する場合、AEM Forms がデプロイされている J2EE アプリケーションサーバーが再起動するまで、新しい資格情報は使用できません。ただし、設定値を設定すると、J2EE アプリケーションサーバーを再起動しなくても、署名や認証の処理が機能します。

/opt/nfast/cknfastrc（または c:\nfastcknfastrc）にある cknfastrc ファイルに、次の設定値を追加できます。

```shell
    CKNFAST_ASSUME_SINGLE_PROCESS=0
```

この設定値を cknfastrc ファイルに追加すると、J2EE アプリケーションサーバーを再起動しなくても、新しい資格情報を使用できます。

**署名は信頼されていません**

同じ PDF ドキュメントの認証と署名を行う際に、認証署名が信頼されていない場合、Acrobat または Adobe Reader で PDF ドキュメントを開くと、最初の署名に対して黄色い三角形が表示されます。この状況を避けるには、認証用署名を信頼する必要があります。

**XFA ベースのフォームのドキュメントに署名**

XFA ベースのフォームに Signature サービス API を使用して署名しようとすると、Acrobat にある `View` `Signed` `Version` からデータが欠落する場合があります。例えば、次のようなワークフローが考えられます。

* Designer を使用して作成された XDP ファイルを使用して、署名フィールドを含むフォームデザインと、フォームデータを含む XML データを結合します。Forms サービスを使用して、インタラクティブ PDF ドキュメントを生成します。
* Signature サービス API を使用して PDF ドキュメントに署名します。

### 手順の概要 {#summary_of_steps-3}

PDF ドキュメントにデジタル署名を行うには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Signature サービスクライアントを作成します。
1. 署名する PDF ドキュメントを取得します。
1. PDF ドキュメントに署名します。
1. 署名済み PDF ドキュメントを PDF ファイルとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar（AEM Forms が JBoss にデプロイされている場合に必要）
* jbossall-client.jar（AEM Formsが JBoss にデプロイされている場合に必要）

**Signatures クライアントの作成**

Signature サービスの操作をプログラムで実行する前に、Signature サービスクライアントを作成する必要があります。

**署名する PDF ドキュメントを取得**

PDF ドキュメントに署名するには、署名フィールドを含む PDF ドキュメントを取得する必要があります。PDF ドキュメントに署名フィールドが含まれていない場合、署名できません。署名フィールドは、Designer を使用して追加することも、プログラムを使用して追加することもできます。

**PDF ドキュメントに署名する**

PDF ドキュメントに署名する際に、Signature サービスで使用する実行時オプションを設定できます。以下のオプションを設定できます。

* アピアランスオプション
* 失効確認
* タイムスタンプ値

外観のオプションは、`PDFSignatureAppearanceOptionSpec` オブジェクトを使用して設定します。例えば、 `PDFSignatureAppearanceOptionSpec` オブジェクトの `setShowDate` メソッドとパス `true`.

また、PDF ドキュメントへのデジタル署名に使用された証明書が失効したかどうかを判断する失効確認を実行するかどうかを指定することもできます。失効確認を実行するには、次のいずれかの値を指定します。

* **NoCheck**：失効確認を実行しません。
* **BestEffort**：常に、チェーン内のすべての証明書の失効を確認しようとします。確認中に問題が発生した場合、失効は有効と見なされます。エラーが発生した場合は、証明書が失効していないと仮定します。
* **CheckIfAvailable**：失効情報が利用できる場合は、チェーン内のすべての証明書の失効を確認します。確認中に問題が発生した場合、失効は無効と見なされます。エラーが発生した場合は、証明書が失効し、無効であるとみなされます。（これがデフォルト値です。）
* **AlwaysCheck**：チェーン内のすべての証明書の失効を確認します。どの証明書にも失効情報が存在しない場合、失効は無効と見なされます。

証明書に対して失効確認を実行するには、`CRLOptionSpec` オブジェクトを使用して証明書失効リスト （CRL）サーバーへの URL を指定します。ただし、失効確認を実行し、CRL サーバーへの URL を指定しない場合、Signature サービスは証明書から URL を取得します。

失効確認を実行する際には、CRL サーバーを使用する代わりに、オンライン証明書ステータスプロトコル（OCSP）サーバーを使用することができます。通常、CRL サーバーとは異なり、OCSP サーバーを使用する場合は、失効確認が高速で実行されます。（[https://tools.ietf.org/html/rfc2560](https://tools.ietf.org/html/rfc2560) にある「オンライン証明書ステータスプロトコル」を参照してください。）

Adobe Applications and Services を使用して、Signature サービスが使用する CRL および OCSP サーバーの順序を設定できます。例えば、OCSP サーバーがアドビのアプリケーションおよびサービスで最初に設定されている場合、OCSP サーバー、CRL サーバーの順にチェックされます。（AAC ヘルプの「トラストストアを使用した証明書と資格情報の管理」を参照してください。）

失効確認を実行しないように指定した場合、Signature サービスは、ドキュメントの署名または認証に使用された証明書が失効したかどうかを確認しません。つまり、CRL および OCSP サーバーの情報は無視されます。

>[!NOTE]
>
>証明書に CRL または OCSP サーバーを指定することもできますが、`CRLOptionSpec` および `OCSPOptionSpec` オブジェクトを使用して証明書で指定された URL を上書きできます。例えば、CRL サーバーを上書きする場合は、 `CRLOptionSpec` オブジェクトの `setLocalURI` メソッド。

タイムスタンプとは、署名済みまたは認証済みのドキュメントが変更された時間を追跡するプロセスを指します。ドキュメントの署名後は、ドキュメントの所有者であってもドキュメントを変更しないでください。タイムスタンプを使用すると、署名済みまたは認証済みのドキュメントの有効性を強制することができます。タイムスタンプオプションは、 `TSPOptionSpec` オブジェクトを使用して設定できます。例えば、タイムスタンププロバイダー（TSP）サーバーの URL を指定できます。

>[!NOTE]
>
>Java および Web サービスの詳細セクションおよび対応するクイックスタートでは、失効確認が使用されます。CRL または OCSP サーバー情報が指定されていないので、サーバー情報は、PDF ドキュメントにデジタル署名するために使用される証明書から取得されます。

PDF ドキュメントに正常に署名するには、`form1[0].#subform[1].SignatureField3[3]` のような、デジタル署名を含む署名フィールドの完全修飾名を指定できます。XFA フォームフィールドを使用する場合、署名フィールドの名前の一部を使用することもできます：`SignatureField3[3]`。

また、PDF ドキュメントにデジタル署名するには、セキュリティ資格情報を参照する必要があります。セキュリティ資格情報を参照するには、エイリアスを指定します。エイリアスは、PKCS#12 ファイル（拡張子が .pfx）またはハードウェアセキュリティモジュール（HSM）に含まれている可能性のある実際の資格情報への参照です。セキュリティ資格情報については、アプリケーションサーバーの *AEM Forms のインストールと導入*&#x200B;ガイドを参照してください。

**署名済み PDF ドキュメントを保存**

Signature サービスで PDF ドキュメントにデジタル署名した後、ユーザーが Acrobat またはAdobe Readerで開くことができるように、PDF ファイルとして保存できます。

**関連トピック**

[Java API を使用した PDF ドキュメントのデジタル署名](digitally-signing-certifying-documents.md#digitally-sign-pdf-documents-using-the-java-api)

[Web サービス API を使用した PDF ドキュメントのデジタル署名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[署名フィールドの追加](digitally-signing-certifying-documents.md#adding-signature-fields)

[署名フィールド名の取得](digitally-signing-certifying-documents.md#retrieving-signature-field-names)

### Java API を使用した PDF ドキュメントのデジタル署名 {#digitally-sign-pdf-documents-using-the-java-api}

Signature API（Java）を使用した PDF ドキュメントのデジタル署名：

1. プロジェクトファイルを含める

   Java プロジェクトのクラスパスに、adobe-signatures-client.jar などのクライアント JAR ファイルを含めます。

1. Signatures クライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して `ServiceClientFactory` オブジェクトを渡すことによって、`SignatureServiceClient` オブジェクトを作成します。

1. 署名する PDF ドキュメントを取得

   * コンストラクターを使用し、PDF ドキュメントの場所を指定する文字列値を渡すことにより、デジタル署名する PDF ドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクターを使用して `java.io.FileInputStream` オブジェクトを渡すことによって、`com.adobe.idp.Document` オブジェクトを作成します。

1. PDF ドキュメントに署名

   を呼び出してPDFドキュメントに署名する `SignatureServiceClient` オブジェクトの `sign` メソッドを使用して、次の値を渡します。

   * 署名する PDF ドキュメントを表す `com.adobe.idp.Document` オブジェクト。
   * デジタル署名を含む署名フィールドの名前を表す文字列値です。
   * PDF ドキュメントへのデジタル署名に使用する資格情報を表す `Credential` オブジェクト。の作成 `Credential` を呼び出すことによって、オブジェクトを `Credential` オブジェクトの静的 `getInstance` メソッドを使用し、セキュリティ秘密鍵証明書に対応するエイリアス値を指定する string 値を渡す。
   * PDF ドキュメントのダイジェストに使用するハッシュアルゴリズムを表す、静的データメンバーを指定する `HashAlgorithm` オブジェクト。例えば、SHA1 アルゴリズムを使用するには `HashAlgorithm.SHA1` を指定できます。
   * PDF ドキュメントがデジタル署名された理由を表す文字列値です。
   * 署名者の連絡先情報を表す string 値です。
   * デジタル署名の外観を制御する `PDFSignatureAppearanceOptions` オブジェクト。例えば、このオブジェクトを使用して、デジタル署名にカスタムロゴを追加できます。
   * 署名者の証明書に対して失効確認を実行するかどうかを指定する `java.lang.Boolean` オブジェクト。
   * オンライン証明書ステータスプロトコル（OCSP）サポートの設定を格納する `OCSPOptionSpec` オブジェクト。失効確認を実行しない場合、このパラメーターは使用されず、`null` を指定できます。
   * 証明書失効リスト（CRL）の環境設定を保存する `CRLPreferences` オブジェクトです。失効確認が実行されない場合、このパラメーターは使用されず、`null` を指定できます。
   * タイムスタンププロバイダー（TSP）がサポートする環境設定を格納する `TSPPreferences` オブジェクト。このパラメーターはオプションで、`null` にすることができます。詳しくは、[AEM Forms API リファレンス](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ja)を参照してください。

   `sign` メソッドは、署名済み PDF ドキュメントを表す `com.adobe.idp.Document` オブジェクトを返します。

1. 署名済み PDF ドキュメントを保存

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が .pdf であることを確認します。
   * を呼び出す `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドとパス `java.io.File`内容をコピーするには `Document` オブジェクトをファイルに追加します。 `sign` メソッドから返された `com.adobe.idp.Document` オブジェクトを必ず使用してください。

**関連トピック**

[PDF ドキュメントの電子署名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[クイックスタート（SOAP モード）：Java API を使用した PDF ドキュメントのデジタル署名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用した PDF ドキュメントのデジタル署名 {#digitally-signing-pdf-documents-using-the-web-service-api}

Signature API（web サービス）を使用した PDF ドキュメントのデジタル署名：

1. プロジェクトファイルを含める

   MTOM を使用する Microsoft .NET プロジェクトを作成します。WSDL 定義 `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1` を使用するようにします。

   >[!NOTE]
   >
   >`localhost` を、AEM Forms をホストするサーバーの IP アドレスに置き換えます。

1. Signatures クライアントの作成

   * デフォルトのコンストラクタを使用して `SignatureServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して`SignatureServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を 指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/SignatureService?WSDL`）。`lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。
   * `SignatureServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * を設定します。 `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `SignatureServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `SignatureServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
      * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` をフィールドに `BasicHttpBindingSecurity.Security.Mode` に割り当てます。

1. 署名する PDF ドキュメントを取得

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、署名された PDF ドキュメントを保存するために使用されます。
   * コンストラクタを呼び出し、署名する PDF ドキュメントのファイルの場所と、ファイルを開くモードを表す文字列値を渡すことによって、`System.IO.FileStream` オブジェクトを作成します。
   * `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッドを使用し、読み込むバイト配列、開始位置、ストリームの長さを渡す。
   * `MTOM` プロパティをバイト配列の内容に割り当てることで、`BLOB` オブジェクトを生成します。

1. PDF ドキュメントに署名

   を呼び出してPDFドキュメントに署名する `SignatureServiceClient` オブジェクトの `sign` メソッドを使用して、次の値を渡します。

   * 署名する PDF ドキュメントを表す `BLOB` オブジェクト。
   * デジタル署名を含む署名フィールドの名前を表す文字列値です。
   * PDF ドキュメントへのデジタル署名に使用する資格情報を表す `Credential` オブジェクト。の作成 `Credential` オブジェクトを指定するには、コンストラクタを使用し、 `Credential` オブジェクトの `alias` プロパティ。
   * PDF ドキュメントのダイジェストに使用するハッシュアルゴリズムを表す、静的データメンバーを指定する `HashAlgorithm` オブジェクト。例えば、`HashAlgorithm.SHA1` を指定して SHA1 アルゴリズムを使用することができます。
   * ハッシュアルゴリズムを使用するかどうかを指定するブール値です。
   * PDF ドキュメントがデジタル署名された理由を表す文字列値です。
   * 署名者の場所を表す string 値です。
   * 署名者の連絡先情報を表す string 値です。
   * デジタル署名の外観を制御する `PDFSignatureAppearanceOptions` オブジェクト。例えば、このオブジェクトを使用して、デジタル署名にカスタムロゴを追加できます。
   * 署名者の証明書に対して失効確認を実行するかどうかを指定する `System.Boolean` オブジェクト。失効確認を実行すると、署名に埋め込まれます。デフォルトは、`false` です。
   * オンライン証明書ステータスプロトコル（OCSP）サポートの環境設定を格納する `OCSPOptionSpec` オブジェクト。失効確認が実行されない場合、このパラメーターは使用されず、`null` を指定できます。このオブジェクトについて詳しくは、[AEM Forms API リファレンス](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ja)を参照してください。
   * 証明書失効リスト（CRL）の環境設定を保存する `CRLPreferences` オブジェクト。失効確認が実行されない場合、このパラメーターは使用されず、`null` を指定できます。
   * タイムスタンププロバイダー（TSP）がサポートする環境設定を保存する `TSPPreferences` オブジェクト。このパラメーターはオプションで、`null` を設定することもできます。

   この `sign` メソッドは、署名済み PDF ドキュメントを表す `BLOB` オブジェクトを返します。

1. 署名済み PDF ドキュメントを保存

   * コンストラクタを呼び出して `System.IO.FileStream` オブジェクトを作成します。署名済み PDF ドキュメントのファイルの場所と、ファイルを開くモードを表す文字列値を渡します。
   * `sign` メソッドが返した `BLOB` オブジェクトの内容を格納するバイト配列を作成します。バイト配列を生成するには、 `BLOB` オブジェクトの `MTOM` データメンバー。
   * コンストラクターを呼び出して `System.IO.FileStream` オブジェクトを渡すことによって、`System.IO.BinaryWriter` オブジェクトを作成します。
   * を呼び出して、バイト配列の内容をPDFファイルに書き込みます。 `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを使用してバイト配列を渡す。

**関連トピック**

[PDF ドキュメントの電子署名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## インタラクティブに Forms を電子署名 {#digitally-signing-interactive-forms}

Forms サービスで作成されるインタラクティブフォームに署名することができます。例えば、次のようなワークフローが考えられます。

* Designer を使用して作成した XFA ベースの PDF フォームと、Forms サービスを使用した XML ドキュメント内のフォームデータを結合します。Forms サーバーはインタラクティブフォームをレンダリングします。
* Signature サービス API を使用してインタラクティブフォームに署名します。

その結果、電子署名されたインタラクティブ PDF フォームが生成されます。XFA フォームに基づく PDF フォームに署名する場合は、その PDF ファイルを Adobe スタティック PDF フォームとして保存します。Adobe ダイナミック PDF フォームとして保存された PDF フォームに署名しようとすると、例外が発生します。Forms サービスから返されるフォームに署名するので、フォームに署名フィールドが含まれていることを確認してください。

>[!NOTE]
>
>インタラクティブフォームに電子署名する前に、証明書を AEM Forms に追加する必要があります証明書は、管理コンソールを使用して、または Trust Manager API を使用してプログラムで追加されます。（[Trust Manager API を使用した資格情報の読み込み](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api)を参照）。

Forms サービス API を使用する場合は、`GenerateServerAppearance` 実行時オプションを `true` に設定します。この実行時オプションを使用すると、サーバー上で生成されるフォームを Acrobat または Adobe Reader で開いたときにも、その外観が有効なままになります。署名するインタラクティブフォームを Forms API を使用して生成する場合は、このランタイムオプションを設定することをお勧めします。

>[!NOTE]
>
>インタラクティブフォームへの電子署名を読む前に、PDF ドキュメントへの署名に関して理解を深めておくことをお勧めします。（[PDF ドキュメントへの電子署名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)を参照してください）。

### 手順の概要 {#summary_of_steps-4}

Forms サービスが返すインタラクティブフォームに電子署名するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Forms および Signatures クライアントを作成します。
1. Forms サービスを使用してインタラクティブフォームを取得します。
1. インタラクティブフォームに署名します。
1. 署名済み PDF ドキュメントを PDF ファイルとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-forms-client.jar
* adobe-utilities.jar（AEM Forms が JBoss にデプロイされている場合に必要）
* jbossall-client.jar（AEM Formsが JBoss にデプロイされている場合に必要）

これらの JAR ファイルの場所について詳しくは、[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。

**Forms クライアントと Signatures クライアントの作成**

このワークフローは Forms サービスと Signature サービスの両方を呼び出すので、Forms サービスクライアントと Signature サービスクライアントの両方を作成します。

**Forms サービスを使用したインタラクティブフォームの取得**

Forms サービスを使用して、署名するインタラクティブ PDF フォームを取得できます。AEM Forms がリリースされたことで、`com.adobe.idp.Document` オブジェクトを、レンダリングするフォームを含む Forms サービスに渡すことができるようになりました。このメソッドの名前は `renderPDFForm2` です。このメソッドは、署名するフォームを含む `com.adobe.idp.Document` オブジェクトを返します。この `com.adobe.idp.Document` インスタンスを Signature サービスに渡すことができます。

同様に、web サービスを使用している場合、Forms サービスが返す `BLOB` インスタンスを Signature サービスに渡すことができます。

>[!NOTE]
>
>「インタラクティブフォームへの電子署名」セクションに関連付けられたクイックスタートは、`renderPDFForm2` メソッドを呼び出します。

**インタラクティブフォームへの署名**

PDF ドキュメントに署名する際に、Signature サービスが使用する実行時オプションを設定できます。以下のオプションを設定できます。

* アピアランスオプション
* 失効確認
* タイムスタンプ値

外観のオプションは、`PDFSignatureAppearanceOptionSpec` オブジェクトを使用して設定します。例えば、 `PDFSignatureAppearanceOptionSpec` オブジェクトの `setShowDate` メソッドとパス `true`.

**署名済み PDF ドキュメントを保存**

Signature サービスが PDF ドキュメントに電子署名を行った後、そのドキュメントを PDF ファイルとして保存できます。PDF ファイルは、Acrobat または Adobe Reader で開くことができます。

**関連トピック**

[Java API を使用したインタラクティブフォームの電子署名](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-java-api)

[Web サービス API を使用したインタラクティブフォームの電子署名](digitally-signing-certifying-documents.md#digitally-sign-an-interactive-form-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDF ドキュメントの電子署名](digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)

[インタラクティブ PDF Forms のレンダリング](/help/forms/developing/rendering-forms.md#rendering-interactive-pdf-forms)

### Java API を使用したインタラクティブフォームの電子署名 {#digitally-sign-an-interactive-form-using-the-java-api}

Forms と Signature API（Java）を使用してインタラクティブフォームに電子署名します。

1. プロジェクトファイルを含める

   Java プロジェクトのクラスパスに、adobe-signatures-client.jar や adobe-forms-client.jar などのクライアント JAR ファイルを含めます。

1. Forms および Signatures クライアントを作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して `ServiceClientFactory` オブジェクトを渡すことにより、`SignatureServiceClient` オブジェクトを作成します。
   * コンストラクターを使用して `ServiceClientFactory` オブジェクトを渡すことにより、`FormsServiceClient` オブジェクトを作成します。

1. Forms サービスを使用してインタラクティブフォームを取得

   * コンストラクターを使用して、Forms サービスに渡す PDF ドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。PDF ドキュメントの場所を指定する文字列値を渡します。
   * コンストラクターを使用して `java.io.FileInputStream` オブジェクトを渡すことにより、`com.adobe.idp.Document` オブジェクトを作成します。
   * コンストラクターを使用して、Forms サービスに渡すフォームデータを含む XML ドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。XML ファイルの場所を指定する文字列値を渡します。
   * コンストラクターを使用して `java.io.FileInputStream` オブジェクトを渡すことにより、`com.adobe.idp.Document` オブジェクトを作成します。
   * 実行時オプションの設定に使用する `PDFFormRenderSpec` オブジェクトを作成します。を呼び出す `PDFFormRenderSpec` オブジェクトの `setGenerateServerAppearance` メソッドとパス `true`.
   * を呼び出す `FormsServiceClient` オブジェクトの `renderPDFForm2` メソッドを使用して、次の値を渡します。

      * レンダリングする PDF フォームを含む `com.adobe.idp.Document` オブジェクト。
      * フォームに結合するデータを含む `com.adobe.idp.Document` オブジェクト。
      * 実行時オプションを格納する `PDFFormRenderSpec` オブジェクト。
      * Forms サービスで必要な URI 値を格納する `URLSpec` オブジェクト。このパラメーター値として `null` を指定できます。
      * 添付ファイルを格納する `java.util.HashMap` オブジェクト。これはオプションのパラメーターであり、フォームにファイルを添付しない場合に `null` を指定できます。

     `renderPDFForm2` メソッドは、 フォームデータストリームを含む `FormsResult` オブジェクトを返します。

   * を呼び出してPDFフォームを取得する `FormsResult` オブジェクトの `getOutputContent` メソッド。 このメソッドは、インタラクティブフォームを表す `com.adobe.idp.Document` オブジェクトを返します。

1. インタラクティブフォームに署名する

   を呼び出してPDFドキュメントに署名する `SignatureServiceClient` オブジェクトの `sign` メソッドを使用して、次の値を渡します。

   * 署名する PDF ドキュメントを表す `com.adobe.idp.Document` オブジェクト。このオブジェクトが、Forms サービスから取得された `com.adobe.idp.Document` オブジェクトであることを確認します。
   * 署名された署名フィールドの名前を表す文字列値です。
   * PDF ドキュメントへの電子署名に使用する資格情報を表す `Credential` オブジェクト。の作成 `Credential` を呼び出すことによって、オブジェクトを `Credential` オブジェクトの静的 `getInstance` メソッド。 セキュリティ資格情報に対応するエイリアス値を指定する文字列値を渡します。
   * PDF ドキュメントのダイジェストに使用するハッシュアルゴリズムを表す静的データメンバーを指定する `HashAlgorithm` オブジェクト。例えば、SHA1 アルゴリズムを使用するには `HashAlgorithm.SHA1` を指定できます。
   * PDF ドキュメントがデジタル署名された理由を表す文字列値です。
   * 署名者の連絡先情報を表す string 値です。
   * デジタル署名の外観を制御する `PDFSignatureAppearanceOptions` オブジェクト。例えば、このオブジェクトを使用して、デジタル署名にカスタムロゴを追加できます。
   * 署名者の証明書に対して失効確認を実行するかどうかを指定する `java.lang.Boolean` オブジェクト。
   * オンライン証明書ステータスプロトコル（OCSP）サポートの設定を格納する `OCSPPreferences` オブジェクト。失効確認を実行しない場合、このパラメーターは使用されず、`null` を指定できます。
   * 証明書失効リスト（CRL）の環境設定を保存する `CRLPreferences` オブジェクトです。失効確認が実行されない場合、このパラメーターは使用されず、`null` を指定できます。
   * タイムスタンププロバイダー（TSP）がサポートする環境設定を保存する `TSPPreferences` オブジェクト。このパラメーターはオプションで、`null` を設定することもできます。

   この `sign` メソッドは、署名済み PDF ドキュメントを表す `com.adobe.idp.Document` オブジェクトを返します。

1. 署名済み PDF ドキュメントを保存

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が .pdf であることを確認します。
   * を呼び出す `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドとパス `java.io.File`内容をコピーするには `Document` オブジェクトをファイルに追加します。 必ず `sign` メソッドが返した `com.adobe.idp.Document` オブジェクトを使用します 。

**関連トピック**

[インタラクティブに Forms を電子署名](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[クイックスタート（SOAP モード）：Java API を使用した PDF ドキュメントへの電子署名](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用したインタラクティブフォームの電子署名 {#digitally-sign-an-interactive-form-using-the-web-service-api}

Forms and Signature API（web サービス）を使用して、インタラクティブフォームに電子署名します。

1. プロジェクトファイルを含める

   MTOM を使用する Microsoft .NET プロジェクトを作成します。このクライアントアプリケーションは 2 つの AEM Forms サービスを呼び出すので、2 つのサービス参照を作成します。Signature サービスに関連付けられたサービス参照に、次の WSDL 定義を使用します：`http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1`。

   Forms サービスに関連付けられたサービス参照に、次の WSDL 定義を使用します：`http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`。

   `BLOB` データタイプは、両方のサービス参照に共通であるため、`BLOB` データタイプを使用する場合は完全に修飾してください。対応する web サービスのクイックスタートでは、すべての `BLOB` インスタンスが完全に修飾されています。

   >[!NOTE]
   >
   >`localhost` を、AEM Forms をホストするサーバーの IP アドレスに置換します。

1. Forms および Signatures クライアントを作成

   * デフォルトのコンストラクターを使用して `SignatureServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して`SignatureServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を 指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/SignatureService?WSDL`）。`lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。
   * `SignatureServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * を設定します。 `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `SignatureServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `SignatureServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。

   * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` をフィールド `BasicHttpBindingSecurity.Security.Mode` に割り当てます。

   >[!NOTE]
   >
   >Forms サービスクライアントに対して、これらの手順を繰り返します。

1. Forms サービスを使用してインタラクティブフォームを取得

   * コンストラクターを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、署名された PDF ドキュメントを保存するために使用されます。
   * コンストラクタを呼び出し、署名する PDF ドキュメントのファイルの場所と、ファイルを開くモードを表す文字列値を渡すことによって、`System.IO.FileStream` オブジェクトを作成します。
   * `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッドを使用し、読み込むバイト配列、開始位置、ストリームの長さを渡す。
   * `MTOM` プロパティにバイト配列のコンテンツを割り当てて、`BLOB` オブジェクトを設定します。
   * コンストラクターを使用して `BLOB` オブジェクトを作成します。`BLOB` オブジェクトは、フォームデータの格納に使用されます。
   * コンストラクターを呼び出し、フォームデータを含む XML ファイルのファイルの場所とファイルを開くモードを表す文字列値を渡すことにより、`System.IO.FileStream` オブジェクトを作成します。
   * `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッドを使用し、読み込むバイト配列、開始位置、ストリームの長さを渡す。
   * `MTOM` プロパティにバイト配列のコンテンツを割り当てて、`BLOB` オブジェクトを設定します。
   * 実行時オプションの設定に使用される `PDFFormRenderSpec` オブジェクトを作成します。値を割り当て `true` から `PDFFormRenderSpec` オブジェクトの `generateServerAppearance` フィールドに入力します。
   * を呼び出す `FormsServiceClient` オブジェクトの `renderPDFForm2` メソッドを使用して、次の値を渡します。

      * レンダリングする PDF フォームを含む `BLOB` オブジェクト。
      * フォームに結合するデータを含む `BLOB` オブジェクト。
      * 実行時オプションを格納する `PDFFormRenderSpec` オブジェクト。
      * Forms サービスで必要な URI 値を格納する `URLSpec` オブジェクト。このパラメーター値として `null` を指定できます。
      * 添付ファイルを格納する `java.util.HashMap` オブジェクト。これはオプションのパラメーターで、フォームにファイルを添付しない場合、`null` を指定できます。
      * フォームにページ数を保存するために使用される長い出力パラメーターです。
      * ロケール値に使用される文字列出力パラメーターです。
      * インタラクティブフォームの保存に使用される出力パラメーターの `FormResult` 値です。

   * を呼び出してPDFフォームを取得します。 `FormsResult` オブジェクトの `outputContent` フィールドに入力します。 このフィールドは、インタラクティブフォームを表す `BLOB` オブジェクトを保存します。

1. インタラクティブフォームに署名する

   を呼び出してPDFドキュメントに署名する `SignatureServiceClient` オブジェクトの `sign` メソッドを使用して、次の値を渡します。

   * 署名する PDF ドキュメントを表す `BLOB` オブジェクトです。Forms サービスによって返された `BLOB` インスタンスを使用します。
   * 署名された署名フィールドの名前を表す文字列値です。
   * PDF ドキュメントへの電子署名に使用する資格情報を表す `Credential` オブジェクト。の作成 `Credential` オブジェクトを指定するには、コンストラクタを使用し、 `Credential` オブジェクトの `alias` プロパティ。
   * PDF ドキュメントのダイジェストに使用するハッシュアルゴリズムを表す、静的データメンバーを指定する `HashAlgorithm` オブジェクト。例えば、`HashAlgorithm.SHA1` を指定して SHA1 アルゴリズムを使用することができます。
   * ハッシュアルゴリズムを使用するかどうかを指定するブール値です。
   * PDF ドキュメントがデジタル署名された理由を表す文字列値です。
   * 署名者の場所を表す string 値です。
   * 署名者の連絡先情報を表す string 値です。
   * デジタル署名の外観を制御する `PDFSignatureAppearanceOptions` オブジェクト。例えば、このオブジェクトを使用して、デジタル署名にカスタムロゴを追加できます。
   * 署名者の証明書に対して失効確認を実行するかどうかを指定する `System.Boolean` オブジェクト。失効確認を実行すると、署名に埋め込まれます。デフォルトは、`false` です。
   * オンライン証明書ステータスプロトコル（OCSP）サポートの環境設定を格納する `OCSPPreferences` オブジェクト。失効確認が実行されない場合、このパラメーターは使用されず、`null` を指定できます。このオブジェクトについて詳しくは、[AEM Forms API リファレンス](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ja)を参照してください。
   * 証明書失効リスト（CRL）の環境設定を保存する `CRLPreferences` オブジェクト。失効確認が実行されない場合、このパラメーターは使用されず、`null` を指定できます。
   * タイムスタンププロバイダー（TSP）がサポートする環境設定を保存する `TSPPreferences` オブジェクト。このパラメーターはオプションで、`null` を設定することもできます。

   この `sign` メソッドは、署名済み PDF ドキュメントを表す `BLOB` オブジェクトを返します。

1. 署名済み PDF ドキュメントを保存

   * コンストラクタを呼び出して `System.IO.FileStream` オブジェクトを作成します。署名済み PDF ドキュメントのファイルの場所と、ファイルを開くモードを表す文字列値を渡します。
   * `sign` メソッドが返した `BLOB` オブジェクトの内容を格納するバイト配列を作成します。バイト配列を生成するには、 `BLOB` オブジェクトの `MTOM` データメンバー。
   * コンストラクターを呼び出して `System.IO.FileStream` オブジェクトを渡すことによって、`System.IO.BinaryWriter` オブジェクトを作成します。
   * を呼び出して、バイト配列の内容をPDFファイルに書き込みます。 `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを使用してバイト配列を渡す。

**関連トピック**

[インタラクティブに Forms を電子署名](digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

## PDF ドキュメントの認証 {#certifying-pdf-documents}

認証済みPDFと呼ばれる特定の種類の署名を使用して認証することで、署名ドキュメントを保護できます。 認証済みの署名は、次の点でデジタル署名と区別されます。

* 認証署名は PDF ドキュメントに適用される最初の署名です。つまり、認証署名が適用されるときは、ドキュメント内の他の署名フィールドは未署名でなければいけません。認証署名は 1 つの PDF ドキュメントにつき 1 つです。PDF ドキュメントを署名および認証するには、署名の前に認証を行う必要があります。署名ドキュメントを認証した後、PDFフィールドに電子署名を行うことができます。
* ドキュメントの作成者または作成者は、認証された署名を無効にすることなく、特定の方法でドキュメントを変更できるように指定できます。 例えば、フォームへの入力やコメント入力を許可するドキュメントなどがあります。作成者が特定の変更を許可しない設定を行った場合は、その方法でのドキュメントの変更は Acrobat によって制限されます。別のアプリケーションの使用などによる変更がおこなわれた場合、認証署名は無効になり、Acrobatはユーザーがドキュメントを開いたときに警告を発します。 （未認証の署名の場合、変更は防止されず、通常の編集操作で元の署名が無効になることはありません）。
* 署名時に、文書の内容をあいまいにしたり誤解を招く可能性のある特定の種類のコンテンツを文書にスキャンします。 例えば、注釈により、認証される対象を把握するために重要なページ上のテキストが隠れてしまう場合があります。このようなコンテンツに関する説明（法的証明）を提供できます。

Signature サービス Java API や Signature web サービス API を使用して、プログラムによって PDF ドキュメントを認証できます。PDF ドキュメントを認証する際は、Credential サービスに存在するセキュリティ資格情報を参照する必要があります。セキュリティ資格情報について詳しくは、ご使用のアプリケーションサーバーに応じた *AEM Forms のインストールとデプロイ*&#x200B;ガイドを参照してください。

>[!NOTE]
>
>同じ PDF ドキュメントを認証および署名する際に、認証用の署名が信頼できない場合、Acrobat または Adobe Reader で PDF ドキュメントを開くと、最初の署名の横に黄色い三角形が表示されます。この状況を避けるには、認証用署名を信頼する必要があります。

>[!NOTE]
>
>PDF ドキュメントの署名や証明に nCipher nShield HSM 資格情報を使用する場合、AEM Forms がデプロイされている J2EE アプリケーションサーバーが再起動されるまで、新しい資格情報は使用できません。ただし、設定値を設定すると、J2EE アプリケーションサーバーを再起動しなくても、署名や認証の処理が機能します。

/opt/nfast/cknfastrc（または c:\nfastcknfastrc）にある cknfastrc ファイルに、次の設定値を追加できます。

```shell
    CKNFAST_ASSUME_SINGLE_PROCESS=0
```

この設定値を cknfastrc ファイルに追加すると、J2EE アプリケーションサーバーを再起動しなくても、新しい資格情報を使用できます。

>[!NOTE]
>
>Signature サービスとドキュメントの認証について詳しくは、 [AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary_of_steps-5}

PDF ドキュメントを認証するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Signature クライアントを作成します。
1. 認証する PDF ドキュメントを取得します。
1. PDF パッケージを認証します。
1. 認証済み PDF ドキュメントを PDF ファイルとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar（AEM Forms が JBoss にデプロイされている場合に必要）
* jbossall-client.jar（AEM Formsが JBoss にデプロイされている場合に必要）

これらの JAR ファイルの場所については、[AEM Forms Java ライブラリファイルの組み込み](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。

**署名クライアントの作成**

Signature 操作をプログラムで実行する前に、Signature クライアントを作成する必要があります。

**認証する PDF ドキュメントの取得**

PDF ドキュメントを認証するには、署名フィールドを含んだ PDF ドキュメントを取得する必要があります。PDF ドキュメントに署名フィールドが含まれていない場合は、認証できません。署名フィールドは、Designer またはプログラムを使用して追加することができます。プログラムによる署名フィールドの追加について詳しくは、[署名フィールドの追加](digitally-signing-certifying-documents.md#adding-signature-fields)を参照してください。

**PDF ドキュメントの認証**

PDF ドキュメントを正常に認証するには、Signature サービスで PDF ドキュメントの認証に使用される次の入力値が必要です。

* **PDF ドキュメント**：署名フィールドを含んだ PDF ドキュメント。署名フィールドは、認証済みの署名のグラフィック表現を含んだフォームフィールドです。PDF ドキュメントを認証する前に、署名フィールドを含める必要があります。署名フィールドは、Designer またはプログラムを使用して追加することができます。（[署名フィールドの追加](digitally-signing-certifying-documents.md#adding-signature-fields)を参照してください）。
* **署名フィールド名**：認証される署名フィールドの完全修飾名。 例えば、`form1[0].#subform[1].SignatureField3[3]` のような値です。XFA フォームフィールドを使用する場合は、`SignatureField3[3]` のように、署名フィールドの名前の一部を使用することもできます。フィールド名に null 値が渡されると、非表示の署名フィールドが動的に作成され、認証されます。
* **セキュリティ資格情報**：PDF ドキュメントの認証に使用される資格情報です。このセキュリティ資格情報には、パスワードとエイリアスが含まれています。このエイリアスは、Credential サービス内にある資格情報に含まれるエイリアスと一致する必要があります。エイリアスは、PKCS#12 ファイル（.pfx の拡張子付き）またはハードウェアセキュリティモジュール（HSM）に存在する実際の資格情報への参照です。
* **ハッシュアルゴリズム**：PDF ドキュメントのダイジェストに使用するハッシュアルゴリズムです。
* **署名の理由**：PDF ドキュメントが認証された理由が他のユーザーにわかるように Acrobat または Adobe Reader に表示される値です。
* **署名者の場所**：資格情報で指定された署名者の場所です。
* **連絡先情報**：署名者の住所や電話番号などの連絡先情報です。
* **権限情報**：認証済みの署名を無効にせずにエンドユーザーがドキュメントに対して実行できるアクションを制御する権限です。例えば、PDF ドキュメントに変更を加えると認証済みの署名が無効になるように権限を設定することができます。
* **法的説明**：ドキュメントを認証すると、ドキュメントがスキャンされて、ドキュメントの内容があいまいになったり誤解を招いたりする可能性のある特定の種類のコンテンツが含まれていないか確認されます。例えば、注釈により、認証される対象を把握するために重要なページ上のテキストが隠れてしまう場合があります。スキャン処理では、これらの種類のコンテンツに関する警告が生成されます。この値は、警告を生成したコンテンツに関する追加の説明を提供します。
* **外観オプション**：認証済みの署名の外観を制御するオプションです。例えば、認証済みの署名に日付情報を表示することができます。
* **失効確認**：この値は、署名者の証明書に対して失効確認を行うかどうかを指定します。`false` のデフォルト設定は、失効確認が行われていないことを意味します。
* **OCSP 設定**：オンライン証明書ステータスプロトコル（OCSP）サポートの設定です。この設定は、PDF ドキュメントの認証に使用される資格情報のステータスに関する情報を提供します。例えば、PDF ドキュメントへのサインオンに使用する資格情報に関する情報を提供するサーバーの URL を指定できます。
* **CRL 設定**：失効確認が行われる場合の、証明書失効リスト（CRL）環境設定の設定です。例えば、資格情報が失効したかどうかを常に確認するように指定できます。
* **タイムスタンプ**：認証済みの署名に適用されるタイムスタンプ情報を定義する設定です。タイムスタンプは、特定のデータが特定の時間より前に作成されたことを示します。この情報は、署名者と検証者の間に信頼関係を構築するのに役立ちます。

**認証済み PDF ドキュメントの PDF ファイルとしての保存**

Signature サービスで PDF ドキュメントが認証されたら、そのドキュメントを PDF ファイルとして保存して、Acrobat または Adobe Reader でユーザーが開けるようにすることができます。

**関連トピック**

[Java API を使用した PDF ドキュメントの認証](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-java-api)

[Web サービス API を使用した PDF ドキュメントの認証](digitally-signing-certifying-documents.md#certify-pdf-documents-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[署名フィールドの追加](digitally-signing-certifying-documents.md#adding-signature-fields)

### Java API を使用した PDF ドキュメントの認証 {#certify-pdf-documents-using-the-java-api}

Signature API（Java）を使用して PDF ドキュメントを認証するには、次の手順に従います。

1. プロジェクトファイルを含める

   Java プロジェクトのクラスパスに、adobe-signatures-client.jar などのクライアント JAR ファイルを含めます。

1. Signature クライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `ServiceClientFactory` オブジェクトを渡すことによって、`SignatureServiceClient` オブジェクトを作成します。

1. 認証する PDF ドキュメントを取得

   * コンストラクタを使用し、PDF ドキュメントの場所を指定する文字列値を渡すことで、認証する PDF ドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクタを使用して `java.io.FileInputStream` オブジェクトを渡すことによって、`com.adobe.idp.Document` オブジェクトを作成します。

1. PDF ドキュメントの認証

   を呼び出してPDFドキュメントを認証する `SignatureServiceClient` オブジェクトの `certify` メソッドを使用して、次の値を渡します。

   * 認証する PDF ドキュメントを表す `com.adobe.idp.Document` オブジェクト
   * 署名を含む署名フィールドの名前を表す文字列値。
   * PDF ドキュメントの認証に使用する資格情報を表す `Credential` オブジェクト。の作成 `Credential` を呼び出すことによって、オブジェクトを `Credential` オブジェクトの静的 `getInstance` メソッドを使用し、セキュリティ秘密鍵証明書に対応するエイリアス値を指定する string 値を渡す。
   * PDF ドキュメントのダイジェストに使用するハッシュアルゴリズムを表すスタティックデータメンバーを指定する `HashAlgorithm` オブジェクトです。例えば、`HashAlgorithm.SHA1` を指定して、SHA1 アルゴリズムを使用できます。
   * PDF ドキュメントが認証された理由を表す文字列値。
   * 署名者の連絡先情報を表す string 値です。
   * 署名を無効にする PDF ドキュメントで実行できるアクションを指定する `MDPPermissions` オブジェクトです。
   * 認証済みの署名の外観を制御する `PDFSignatureAppearanceOptions` オブジェクト。必要に応じて `setShowDate` などのメソッドを呼び出し、署名の外観を変更します。
   * 署名を無効にするアクションの説明を提供する文字列値です。
   * 署名者の証明書に対して失効確認を実行するかどうかを指定する `java.lang.Boolean` オブジェクトです。失効確認を実行すると、署名に埋め込まれます。デフォルトは、`false` です。
   * 認証される署名フィールドをロックするかどうかを指定する `java.lang.Boolean` オブジェクトです。署名フィールドをロックすると、このフィールドは読み取り専用としてマークされ、プロパティは変更できません。また、必要な権限を持たないユーザーはこのフィールドをクリアできません。デフォルトは、`false` です。
   * オンライン証明書ステータスプロトコル（OCSP）サポートの環境設定を格納する `OCSPPreferences` オブジェクト。失効確認を実行しない場合、このパラメーターは使用されず、`null` を指定できます。このオブジェクトについて詳しくは、[AEM Forms API リファレンス](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ja)を参照してください。
   * 証明書失効リスト（CRL）の環境設定を保存する `CRLPreferences` オブジェクトです。失効確認が実行されない場合、このパラメーターは使用されず、`null` を指定できます。
   * タイムスタンププロバイダー（TSP）がサポートする環境設定を格納する `TSPPreferences` オブジェクト。例えば、 `TSPPreferences` オブジェクトを使用する場合は、 `TSPPreferences` オブジェクトの `setTspServerURL` メソッド。 このパラメーターはオプションで、`null` にすることができます。詳しくは、[AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

   `certify` メソッドは、認証済み PDF ドキュメントを表す `com.adobe.idp.Document` オブジェクトを返します。

1. 認証済み PDF ドキュメントを PDF ファイルとして保存

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が .pdf であることを確認します。
   * を呼び出す `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを使用して、 `com.adobe.idp.Document` オブジェクトをファイルに追加します。

**関連トピック**

[PDF ドキュメントの認証](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[クイックスタート（SOAP モード）：Java API を使用した PDF ドキュメントの認証](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-certifying-a-pdf-document-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用した PDF ドキュメントの認証 {#certify-pdf-documents-using-the-web-service-api}

Signature API（web サービス）を使用して PDF ドキュメントを認証します。

1. プロジェクトファイルを含める

   MTOM を使用する Microsoft .NET プロジェクトを作成します。WSDL 定義 `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1` を使用するようにします。

   >[!NOTE]
   >
   >`localhost` を、AEM Forms をホストするサーバーの IP アドレスに置き換えてください。

1. Signature クライアントの作成

   * デフォルトのコンストラクターを使用して `SignatureServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して`SignatureServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を 指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/SignatureService?WSDL`）。`lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。
   * `SignatureServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * を設定します。 `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `SignatureServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `SignatureServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
      * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` をフィールド `BasicHttpBindingSecurity.Security.Mode` に割り当てます。

1. 認証する PDF ドキュメントを取得

   * コンストラクターを使用して `BLOB` オブジェクトを作成します。`BLOB` オブジェクトは、認証済みの PDF ドキュメントを格納するために使用されます。
   * コンストラクターを呼び出し、認証する PDF ドキュメントのファイルの場所とファイルを開くモードを表す文字列値を渡すことにより、`System.IO.FileStream` オブジェクトを作成します。
   * `System.IO.FileStream` オブジェクトの内容を格納するバイト配列を作成します。バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッドを使用し、読み込むバイト配列、開始位置、ストリームの長さを渡す。
   * `MTOM` データメンバーにバイト配列の内容を割り当てて、`BLOB` オブジェクトにデータを入力します。

1. PDF ドキュメントの認証

   を呼び出してPDFドキュメントを認証する `SignatureServiceClient` オブジェクトの `certify` メソッドを使用して、次の値を渡します。

   * 認証する PDF ドキュメントを表す `BLOB` オブジェクト
   * 署名を含む署名フィールドの名前を表す文字列値。
   * PDF ドキュメントの認証に使用する資格情報を表す `Credential` オブジェクト。の作成 `Credential` オブジェクトを指定するには、コンストラクタを使用し、 `Credential` オブジェクトの `alias` プロパティ。
   * PDF ドキュメントのダイジェストに使用するハッシュアルゴリズムを表すスタティックデータメンバーを指定する `HashAlgorithm` オブジェクトです。例えば、SHA1 アルゴリズムを使用するために `HashAlgorithm.SHA1` を指定できます。
   * ハッシュアルゴリズムを使用するかどうかを指定するブール値です。
   * PDF ドキュメントが認証された理由を表す文字列値。
   * 署名者の場所を表す string 値です。
   * 署名者の連絡先情報を表す string 値です。
   * An `MDPPermissions` 署名を無効にする署名ドキュメントで実行できるアクションを指定する、PDFの静的なデータメンバーです。
   * 前のパラメータ値として渡された `MDPPermissions` オブジェクトを使用するかどうかを指定するブール値。
   * どのようなアクションで署名が無効になるかを説明する文字列値。
   * 認証された署名の外観を制御する `PDFSignatureAppearanceOptions` オブジェクト。コンストラクタを使用して `PDFSignatureAppearanceOptions` オブジェクトを作成します。署名のデータメンバーのいずれかを設定することで、署名の外観を変更できます。
   * 署名者の証明書に対して失効確認を実行するかどうかを指定する `System.Boolean` オブジェクトです。失効確認を実行すると、署名に埋め込まれます。デフォルトは、`false` です。
   * 認証される署名フィールドをロックするかどうかを指定する `System.Boolean` オブジェクトです。署名フィールドをロックすると、このフィールドは読み取り専用としてマークされ、プロパティは変更できません。また、必要な権限を持たないユーザーはこのフィールドをクリアできません。デフォルトは、`false` です。
   * 署名フィールドをロックするかどうかを指定する `System.Boolean` オブジェクトです。つまり、 `true` を前のパラメーターに渡す場合は、`true` をこのパラメーターに渡します。
   * オンライン証明書ステータスプロトコル（OCSP）のサポートの環境設定を保存する `OCSPPreferences` オブジェクトです。このオブジェクトは、PDF ドキュメントの認証に使用される資格情報のステータスに関する情報を提供します。失効確認を実行しない場合、このパラメーターは使用されず、`null` を指定できます。
   * 証明書失効リスト（CRL）の環境設定を保存する `CRLPreferences` オブジェクトです。失効確認が実行されない場合、このパラメーターは使用されず、`null` を指定できます。
   * タイムスタンププロバイダー（TSP）がサポートする環境設定を格納する `TSPPreferences` オブジェクト。例えば、 `TSPPreferences` オブジェクトの場合は、TSP の URL を設定できます。 `TSPPreferences` オブジェクトの `tspServerURL` データメンバー。 このパラメーターはオプションで、`null` にすることができます。

   `certify` メソッドは、認証済みPDF オブジェクトを表す `BLOB` オブジェクトを返します。

1. 認証済み PDF ドキュメントを PDF ファイルとして保存

   * コンストラクタを呼び出し、認証された PDF ドキュメントを含む PDF ドキュメントのファイルの場所とファイルを開くモードを表す文字列値を渡すことによって、`System.IO.FileStream` オブジェクトを作成します。
   * `certify` メソッドによって返された `BLOB` オブジェクトのコンテンツを格納するバイト配列を作成します。バイト配列を生成するには、 `BLOB` オブジェクトの `binaryData` データメンバー。
   * コンストラクターを呼び出して `System.IO.FileStream` オブジェクトを渡すことによって、`System.IO.BinaryWriter` オブジェクトを作成します。
   * を呼び出して、バイト配列の内容をPDFファイルに書き込みます。 `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを使用してバイト配列を渡す。

**関連トピック**

[PDF ドキュメントの認証](digitally-signing-certifying-documents.md#certifying-pdf-documents)

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## デジタル署名の検証 {#verifying-digital-signatures}

電子署名を検証することで、署名された PDF ドキュメントに変更がなく、電子署名が有効であることを確認することができます。電子署名を検証する際に、署名のステータスや、署名者の ID などの署名のプロパティを確認できます。 デジタル署名を信頼する前に、検証することをお勧めします。 デジタル署名を検証する場合は、デジタルPDFを含む署名ドキュメントを参照します。

署名者の ID が不明であるとします。AcrobatでPDFドキュメントを開くと、次の図に示すように、署名者の ID が不明であることを示す警告メッセージが表示されます。

![vd_vd_verifysig](assets/vd_vd_verifysig.png)

同様に、プログラムによって電子署名を検証する場合、署名者の ID のステータスを判断できます。 例えば、前の図で示したドキュメントで電子署名を検証した場合、結果として、署名者の ID が不明になります。

>[!NOTE]
>
>Signature サービスとデジタル署名の検証について詳しくは、 [AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary_of_steps-6}

デジタル署名を検証するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Signature クライアントを作成します。
1. 検証する署名が含まれている PDF ドキュメントを取得します。
1. PKI の実行時オプションを設定します。
1. デジタル署名を検証します。
1. 署名のステータスを決定します。
1. 署名者の ID を指定します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを含めます。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar（AEM Forms が JBoss にデプロイされている場合に必要）
* jbossall-client.jar（AEM Formsが JBoss にデプロイされている場合に必要）

これらの JAR ファイルの場所については、[AEM Forms Java ライブラリファイルの組み込み](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。

**Signature クライアントの作成**

Signature サービスの操作をプログラムで実行する前に、Signature サービスクライアントを作成します。

**検証する署名を含む PDF ドキュメントを取得**

PDF ドキュメントのデジタル署名または認証に使用される署名を確認するには、署名を含む PDF ドキュメントを入手します。

**PKI 実行時オプションを設定**

PDF ドキュメントの署名を検証するときに署名サービスが使用する次の PKI 実行時オプションを設定します。

* 検証時刻
* 失効確認
* タイムスタンプ値

これらのオプションを設定する際に、検証時刻を指定できます。例えば、現在の時刻（バリデーターのコンピューター上の時刻）を選択し、現在の時刻を使用するように指定できます。 さまざまな時間値の詳細については、[AEM FormsAPI リファレンス](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ja)の `VerificationTime` 列挙値を参照してください。

また、検証プロセスの一環として失効確認を実行するかどうかを指定することもできます。例えば、失効確認を実行して、証明書が失効しているかどうかを判断できます。失効確認オプションについて詳しくは、[AEM Forms APIリファレンス](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ja)の `RevocationCheckStyle`列挙値を参照してください。

証明書の失効チェックを実行するには、`CRLOptionSpec` オブジェクトを使用して、証明書失効リスト（CRL）サーバーへの URL を指定します。ただし、CRL サーバーへの URL を指定しない場合、署名サービスは証明書から URL を取得します。

失効確認を実行する際には、CRL サーバーを使用する代わりに、オンライン証明書ステータスプロトコル（OCSP）サーバーを使用することができます。通常、CRL サーバーではなく OCSP サーバーを使用すると、失効チェックがより高速に実行されます（[オンライン証明書ステータスプロトコル](https://tools.ietf.org/html/rfc2560)を参照）。

Signature サービスが使用する CRL および OCSP サーバーの順序は、アドビのアプリケーションおよびサービスを使用して設定できます。例えば、OCSP サーバーが最初にアドビのアプリケーションとサービスで設定されている場合、OCSP サーバーが確認され、次に CRL サーバーが確認されます。

失効確認を実行しない場合、Signature サービスは証明書が失効しているかどうかを確認しません。つまり、CRL および OCSP サーバーの情報は無視されます。

>[!NOTE]
>
>証明書で指定された URL を上書きするには、`CRLOptionSpec` および `OCSPOptionSpec` オブジェクトを使用します。例えば、CRL サーバーを上書きする場合は、 `CRLOptionSpec` オブジェクトの `setLocalURI` メソッド。

タイムスタンプとは、署名済みまたは認証済みのドキュメントが変更された時刻を追跡するプロセスです。ドキュメントが署名された後は、誰もドキュメントを変更できません。タイムスタンプを使用すると、署名済みまたは認証済みのドキュメントの有効性を強制することができます。タイムスタンプオプションは、 `TSPOptionSpec` オブジェクトを使用して設定できます。例えば、タイムスタンププロバイダー（TSP）サーバーの URL を指定できます。

>[!NOTE]
>
>Java および web サービスのクイックスタートでは、検証時間が `VerificationTime.CURRENT_TIME` に設定されており、失効確認は `RevocationCheckStyle.BestEffort` に設定されています。CRL または OCSP のいずれのサーバー情報も指定されていないため、証明書からサーバー情報が取得されます。

**電子署名の検証**

署名を正しく検証するには、署名が含まれている署名フィールドの完全修飾名を指定します（例：`form1[0].#subform[1].SignatureField3[3]`）。XFA フォームフィールドを使用している場合は、署名フィールドの一部の名前を使用することもできます（例：`SignatureField3`）。

Signature サービスでは、デフォルトにより、検証時刻を経過した後、ドキュメントに署名できる時間が 65 分に制限されます。ユーザーが現在の時刻に署名の検証を試みたときに、署名の時刻が現在の時刻よりも後、かつ 65 分以内になっている場合、Signature サービスでは検証エラーは作成されません。

>[!NOTE]
>
>署名の検証時に必要なその他の値については、[AEM Forms API リファレンス](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ja)を参照してください。

**署名のステータスの判断**

電子署名の検証の一環として、署名のステータスを確認できます。

**署名者の ID の判断**

次のいずれかの値により、署名者の ID を判断できます。

* **不明**：署名者の検証が実行できないため、この署名者は不明になります。
* **信頼済み**：信頼できる署名者です。
* **信頼できない**：この署名者は信頼できません。

**関連トピック**

[Java API を使用した電子署名の検証](#verify-digital-signatures-using-the-java-api)

[Web サービス API を使用した電子署名の検証](#verify-digital-signatures-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API を使用した電子署名の検証 {#verify-digital-signatures-using-the-java-api}

Signature サービス API（Java）を使用した電子署名の検証：

1. プロジェクトファイルを含める

   Java プロジェクトのクラスパスに、adobe-signatures-client.jar などのクライアント JAR ファイルを含めます。

1. Signature クライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `ServiceClientFactory` オブジェクトを渡すことによっり、`SignatureServiceClient` オブジェクトを作成します。

1. 検証する署名を含む PDF ドキュメントを取得する

   * コンストラクタを使用して、検証する署名が含まれる PDF ドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。PDFドキュメントの場所を指定する文字列値値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PKI 実行時オプションを設定する

   * コンストラクタを使用して `PKIOptions` オブジェクトを作成します。
   * を呼び出して検証時間を設定 `PKIOptions` オブジェクトの `setVerificationTime` メソッドと `VerificationTime` 検証時間を指定する列挙値。
   * を呼び出して、失効確認オプションを設定します。 `PKIOptions` オブジェクトの `setRevocationCheckStyle` メソッドと `RevocationCheckStyle` 失効確認を実行するかどうかを指定する列挙値。

1. 電子署名の検証

   を呼び出して、署名を検証します。 `SignatureServiceClient` オブジェクトの `verify2` メソッドを使用して、次の値を渡します。

   * 電子署名、または認証済みの PDF ドキュメントを含む `com.adobe.idp.Document` オブジェクト。
   * 検証する署名が含まれている署名フィールド名を表す文字列値。
   * PKI 実行時オプションを含む `PKIOptions` オブジェクト。
   * SPI 情報を含む `VerifySPIOptions` インスタンス。このパラメーターには、`null` を指定できます。

   `verify2` メソッドでは、電子署名の検証に使用できる情報を含む `PDFSignatureVerificationInfo` オブジェクトが返されます。

1. 署名のステータスの判断

   * を呼び出して、署名のステータスを判断します。 `PDFSignatureVerificationInfo` オブジェクトの `getStatus` メソッド。 このメソッドは、署名のステータスを指定する `SignatureStatus` オブジェクトを返します。例えば、署名済みの PDF ドキュメントに変更がない場合は、このメソッドにより `SignatureStatus.DocumentSigNoChanges` が返されます。

1. 署名者の ID の判断

   * を呼び出して、署名者の ID を特定します。 `PDFSignatureVerificationInfo` オブジェクトの `getSigner` メソッド。 このメソッドは、`IdentityInformation` オブジェクトを返します。
   * を呼び出す `IdentityInformation` オブジェクトの `getStatus` 署名者の id を決定する方法です。 このメソッドは、ID を特定する `IdentityStatus` 列挙値を返します。例えば、信頼されている署名者の場合、このメソッドでは `IdentityStatus.TRUSTED` が返されます。

**関連トピック**

[デジタル署名の検証](#verify-digital-signatures-using-the-java-api)

[クイックスタート（SOAP モード）：Java API を使用したデジタル署名の検証](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-a-digital-signature-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用した電子署名の検証 {#verify-digital-signatures-using-the-web-service-api}

Signature Service API（Web サービス）を使用してデジタル署名を検証します。

1. プロジェクトファイルを含める

   MTOM を使用する Microsoft .NET プロジェクトを作成します。WSDL 定義 `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1` を使用するようにします。

   >[!NOTE]
   >
   >`localhost` を、AEM Forms をホストするサーバーの IP アドレスに置き換えてください。

1. Signature クライアントの作成

   * デフォルトのコンストラクターを使用して `SignatureServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して`SignatureServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を 指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/SignatureService?WSDL`）。`lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。
   * `SignatureServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * を設定します。 `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `SignatureServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `SignatureServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
      * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` をフィールド `BasicHttpBindingSecurity.Security.Mode` に割り当てます。

1. 検証する署名を含む PDF ドキュメントを取得する

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB` オブジェクトは、検証するデジタルまたは認証済み署名が含まれる PDF ドキュメントを格納するために使用されます。
   * コンストラクタを使用して `System.IO.FileStream` オブジェクトを作成します。署名済み PDF ドキュメントのファイルの場所と、ファイルを開くモードを表す文字列値を渡します。
   *  `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッド。 読み取り対象のバイト配列、開始位置、ストリーム長を渡します。
   * `MTOM` プロパティにバイト配列のコンテンツを割り当てて、`BLOB` オブジェクトを設定します。

1. PKI 実行時オプションを設定する

   * コンストラクタを使用して `PKIOptions` オブジェクトを作成します。
   * 検証時間を設定するには、 `PKIOptions` オブジェクトの `verificationTime` データメンバー a `VerificationTime` 検証時間を指定する列挙値。
   * 失効確認オプションを設定するには、 `PKIOptions` オブジェクトの `revocationCheckStyle` データメンバー a `RevocationCheckStyle` 失効確認を実行するかどうかを指定する列挙値。

1. 電子署名の検証

   を呼び出して、署名を検証します。 `SignatureServiceClient` オブジェクトの `verify2` メソッドを使用して、次の値を渡します。

   * デジタル署名された、または認証された PDF ドキュメントを含む `BLOB` オブジェクト。
   * 検証する署名が含まれている署名フィールド名を表す文字列値。
   * PKI 実行時オプションを含む `PKIOptions` オブジェクト。
   * SPI 情報を含む `VerifySPIOptions` インスタンス。このパラメーターには、`null` を指定できます。

   `verify2` メソッドでは、電子署名の検証に使用できる情報を含む `PDFSignatureVerificationInfo` オブジェクトが返されます。

1. 署名のステータスの判断

   署名のステータスを決定するには、 `PDFSignatureVerificationInfo` オブジェクトの `status` データメンバー。 このデータメンバーは、 `SignatureStatus` 署名のステータスを指定するオブジェクト。 例えば、署名済みの PDF ドキュメントを変更する場合、`status` データメンバーに値 `SignatureStatus.DocumentSigNoChanges` が格納されます。

1. 署名者の ID の判断

   * 署名者の ID を確認するには、 `PDFSignatureVerificationInfo` オブジェクトの `signer` データメンバー。 このメンバーは `IdentityInformation` オブジェクトを返します。
   * を取得する `IdentityInformation` オブジェクトの `status` 署名者の ID を決定するデータメンバー。 このデータメンバーは、id を指定する `IdentityStatus` 列挙値を返します。例えば、署名者が信頼されている場合、このメンバーは `IdentityStatus.TRUSTED` を返します。

**関連トピック**

[デジタル署名の検証](#verify-digital-signatures-using-the-java-api)

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## 複数のデジタル署名の検証 {#verifying-multiple-digital-signatures}

AEM Forms は、PDF ドキュメント内のすべてのデジタル署名を検証する手段を提供します。複数の署名者からの署名を必要とするビジネスプロセスの結果として、PDF ドキュメントに複数のデジタル署名が含まれていると想定します。例えば、融資担当者の署名と管理者の署名の両方を必要とする金融取引を考えてみましょう。 Signature サービス Java API または Web サービス API を使用して、PDF ドキュメント内のすべての署名を検証できます。複数の署名を検証する際は、それぞれの署名のステータスやプロパティを確認できます。デジタル署名を信用する前に、検証することをお勧めします。単一のデジタル署名の検証に精通していることをお勧めします。

>[!NOTE]
>
>Signature サービスとデジタル署名の検証について詳しくは、 [AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary_of_steps-7}

複数のデジタル署名を検証するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Signature クライアントを作成します。
1. 検証する PDF が含まれている署名ドキュメントを取得します。
1. PKI の実行時オプションを設定します。
1. すべてのデジタル署名を取得します。
1. すべての署名を繰り返し処理します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを含めます。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar（AEM Forms が JBoss にデプロイされている場合に必要）
* jbossall-client.jar（AEM Formsが JBoss にデプロイされている場合に必要）

これらの JAR ファイルの場所については、[AEM Forms Java ライブラリファイルの組み込み](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。

**Signature クライアントの作成**

Signature サービスの操作をプログラムで実行する前に、Signature サービスクライアントを作成します。

**検証する署名を含む PDF ドキュメントの取得**

PDF ドキュメントのデジタル署名または認証に使用される署名を確認するには、署名を含む PDF ドキュメントを入手します。

**PKI 実行時オプションの設定**

PDF ドキュメント内のすべての署名を検証する際に Signature サービスが使用する、以下の PKI 実行時オプションを設定します。

* 検証時刻
* 失効確認
* タイムスタンプ値

これらのオプションを設定する際に、検証時刻を指定できます。例えば、現在の時刻（バリデーターのコンピューター上の時刻）を選択し、現在の時刻を使用するように指定できます。 さまざまな時間値の詳細については、[AEM FormsAPI リファレンス](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ja)の `VerificationTime` 列挙値を参照してください。

また、検証プロセスの一環として失効確認を実行するかどうかを指定することもできます。例えば、失効確認を実行して、証明書が失効しているかどうかを判断できます。失効確認オプションについて詳しくは、[AEM Forms APIリファレンス](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ja)の `RevocationCheckStyle`列挙値を参照してください。

証明書に対して失効確認を実行するには、`CRLOptionSpec` オブジェクトを使用して証明書失効リスト（CRL）サーバーへの URL を指定します。ただし、CRL サーバーへの URL を指定しない場合、Signature サービスが証明書から URL を取得します。

失効確認を実行する際には、CRL サーバーを使用する代わりに、オンライン証明書ステータスプロトコル（OCSP）サーバーを使用することができます。一般的に、CRL サーバーではなく OCSP サーバーを使用すると、失効確認の実行速度が向上します（[オンライン証明書ステータスプロトコル](https://tools.ietf.org/html/rfc2560)を参照してください）。

Signature サービスが使用する CRL および OCSP サーバーの順序は、アドビのアプリケーションおよびサービスを使用して設定できます。例えば、アドビのアプリケーションおよびサービスで OCSP サーバーが最初に設定されている場合、OCSP サーバーがチェックされ、その後に CRL サーバーがチェックされます。

失効確認を実行しない場合、Signature サービスは証明書が失効しているかどうかを確認しません。つまり、CRL および OCSP サーバーの情報は無視されます。

>[!NOTE]
>
>証明書で指定された URL を上書きするには、`CRLOptionSpec` および `OCSPOptionSpec` オブジェクトを使用します。例えば、CRL サーバーを上書きする場合は、 `CRLOptionSpec` オブジェクトの `setLocalURI` メソッド。

タイムスタンプとは、署名済みまたは認証済みのドキュメントが変更された時刻を追跡するプロセスです。ドキュメントが署名された後は、誰もドキュメントを変更できません。タイムスタンプは、署名済みまたは認証済みのドキュメントの有効性を確保するのに役立ちます。タイムスタンプオプションは、`TSPOptionSpec` オブジェクトを使用して設定することができます。例えば、タイムスタンププロバイダー（TSP）サーバーの URL を指定できます。

>[!NOTE]
>
>Java および web サービスのクイックスタートでは、検証時間が `VerificationTime.CURRENT_TIME` に設定されており、失効確認は `RevocationCheckStyle.BestEffort` に設定されています。CRL または OCSP サーバーの情報が指定されていないので、サーバー情報は証明書から取得されます。

**すべての電子署名の取得**

PDF ドキュメント内のすべてのデジタル署名を検証するには、PDF ドキュメントからデジタル署名を取得します。すべての署名がリスト形式で返されます。電子署名の検証の一環として、署名のステータスを確認します。

>[!NOTE]
>
>単一の電子署名を検証する場合とは異なり、複数の署名を検証する場合は、署名フィールド名を指定する必要はありません。

**すべての署名の繰り返し処理**

各署名を繰り返し処理します。つまり、署名ごとに電子署名を検証し、署名者の ID と各署名のステータスを確認します。 （[電子署名の検証](#verify-digital-signatures-using-the-java-api)を参照してください）。

>[!NOTE]
>
>ドキュメント全体が検証対象となっている場合は、すべての署名を繰り返し処理する必要はありません。

**関連トピック**

[Java API を使用した複数の電子署名の検証](#verify-digital-signatures-using-the-java-api)

[Web サービス API を使用した複数のデジタル署名の検証](#verify-digital-signatures-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API を使用した複数の電子署名の検証 {#verify-multiple-digital-signatures-using-the-java-api}

Signature サービス API（Java）を使用して、複数の電子署名を検証します。

1. プロジェクトファイルを含める

   Java プロジェクトのクラスパスに、adobe-signatures-client.jar などのクライアント JAR ファイルを含めます。

1. Signature クライアントの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `ServiceClientFactory` オブジェクトを渡すことによって、`SignatureServiceClient` オブジェクトを作成します。

1. 検証する署名が含まれている PDF ドキュメントを取得します

   * コンストラクターを使用して、検証対象である複数のデジタル署名を含む PDF ドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。PDF ドキュメントの場所を指定する文字列値を渡します。
   * コンストラクタを使用して `java.io.FileInputStream` オブジェクトを渡すことによって、`com.adobe.idp.Document` オブジェクトを作成します。

1. PKI ランタイムオプションを設定

   * コンストラクタを使用して `PKIOptions` オブジェクトを作成します。
   * を呼び出して検証時間を設定 `PKIOptions` オブジェクトの `setVerificationTime` メソッドと `VerificationTime` 検証時間を指定する列挙値。
   * を呼び出して、失効確認オプションを設定します。 `PKIOptions` オブジェクトの `setRevocationCheckStyle` メソッドと `RevocationCheckStyle` 失効確認を実行するかどうかを指定する列挙値。

1. すべてのデジタル署名を取得する

   を呼び出す `SignatureServiceClient` オブジェクトの `verifyPDFDocument` メソッドを使用して、次の値を渡します。

   * 複数のデジタル署名を含む PDF ドキュメントが格納されている `com.adobe.idp.Document` オブジェクト。
   * PKI 実行時オプションが格納されている `PKIOptions` オブジェクト。
   * SPI 情報を含む `VerifySPIOptions` インスタンス。このパラメーターには `null` を指定できます。

   この `verifyPDFDocument` メソッドは、PDF ドキュメントにあるすべてのデジタル署名に関する情報が格納されている `PDFDocumentVerificationInfo` オブジェクトを返します。

1. すべての署名を反復処理

   * を呼び出すことで、すべての署名を繰り返し処理します。 `PDFDocumentVerificationInfo` オブジェクトの `getVerificationInfos` メソッド。 このメソッドは、各要素が `PDFSignatureVerificationInfo` オブジェクトである `java.util.List` オブジェクトを返します。`java.util.Iterator` オブジェクトを使用して、署名のリストを反復処理します。
   * の使用 `PDFSignatureVerificationInfo` オブジェクトを使用すると、 `PDFSignatureVerificationInfo` オブジェクトの `getStatus` メソッド。 このメソッドは、静的データメンバーが署名のステータスを通知する `SignatureStatus` オブジェクトを返します。例えば署名が不明な場合、このメソッドは `SignatureStatus.DocumentSignatureUnknown` を返します。

**関連トピック**

[複数のデジタル署名の検証](#verifying-multiple-digital-signatures)

[クイックスタート（SOAP モード）：Java API を使用した複数のデジタル署名の検証](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-verifying-multiple-digital-signatures-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[デジタル署名の検証](#verify-digital-signatures-using-the-java-api)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用した複数のデジタル署名の検証 {#verifying-multiple-digital-signatures-using-the-web-service-api}

Signature Service API（web サービス）を使用して、複数のデジタル署名を検証します。

1. プロジェクトファイルを含める

   MTOM を使用する Microsoft .NET プロジェクトを作成します。WSDL 定義 `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1` を使用するようにします。

   >[!NOTE]
   >
   >`localhost` を、AEM Forms をホストするサーバーの IP アドレスに置き換えてください。

1. Signature クライアントの作成

   * デフォルトのコンストラクターを使用して `SignatureServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して`SignatureServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を 指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/SignatureService?WSDL`）。`lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。
   * `SignatureServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * を設定します。 `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `SignatureServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `SignatureServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
      * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` をフィールド `BasicHttpBindingSecurity.Security.Mode` に割り当てます。

1. 検証する署名が含まれている PDF ドキュメントを取得します

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、検証する複数のデジタル署名を含む PDF ドキュメントを格納します。
   * コンストラクターを呼び出して `System.IO.FileStream` オブジェクトを作成します。PDF ドキュメントのファイルの場所と、ファイルを開くモードを表す文字列値を渡します。
   * `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッド。 読み取り対象のバイト配列、開始位置、ストリーム長を渡します。
   * バイト配列の内容の `MTOM` プロパティを割り当てることで、`BLOB` オブジェクトを生成します。

1. PKI ランタイムオプションを設定

   * コンストラクタを使用して `PKIOptions` オブジェクトを作成します。
   * 検証時間を設定するには、 `PKIOptions` オブジェクトの `verificationTime` データメンバー a `VerificationTime` 検証時間を指定する列挙値。
   * 失効確認オプションを設定するには、 `PKIOptions` オブジェクトの `revocationCheckStyle` データメンバー a `RevocationCheckStyle` 失効確認を実行するかどうかを指定する列挙値。

1. すべてのデジタル署名を取得する

   を呼び出す `SignatureServiceClient` オブジェクトの `verifyPDFDocument` メソッドを使用して、次の値を渡します。

   * 複数のデジタル署名を含む PDF ドキュメントが格納されている `BLOB` オブジェクト。
   * PKI 実行時オプションが格納されている `PKIOptions` オブジェクト。
   * SPI 情報を含む `VerifySPIOptions` インスタンス。このパラメーターには null を指定できます。

   この `verifyPDFDocument` メソッドは、PDF ドキュメント内のすべてのデジタル署名に関する情報を含む `PDFDocumentVerificationInfo` オブジェクトを返します。

1. すべての署名を反復処理

   * すべての署名を繰り返し処理し、 `PDFDocumentVerificationInfo` オブジェクトの `verificationInfos` データメンバー。 このデータメンバは、各要素が `PDFSignatureVerificationInfo` オブジェクトである `Object` 配列を返します。
   * の使用 `PDFSignatureVerificationInfo` オブジェクトを使用すると、署名のステータスを確認するタスクなどを実行できます。その場合は、 `PDFSignatureVerificationInfo` オブジェクトの `status` データメンバー。 このデータメンバーは、静的データメンバーが署名のステータスについて通知する `SignatureStatus` オブジェクトを返します。例えば、署名が不明な場合、このメソッドは `SignatureStatus.DocumentSignatureUnknown` を返します。

**関連トピック**

[複数のデジタル署名の検証](#verifying-multiple-digital-signatures)

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## デジタル署名の削除 {#removing-digital-signatures}

署名フィールドからデジタル署名を削除してから、新しいデジタル署名を適用する必要があります。デジタル署名は上書きできません。署名が含まれている署名フィールドにデジタル署名を適用しようとすると、例外が発生します。

>[!NOTE]
>
>Signature サービスについて詳しくは、[AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary_of_steps-8}

署名フィールドからデジタル署名を削除するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Signature クライアントを作成します。
1. 削除する署名が含まれている PDF ドキュメントを取得します。
1. 署名フィールドからデジタル署名を削除します。
1. PDF ドキュメントを PDF ファイルとして保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めるようにします。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-signatures-client.jar
* adobe-utilities.jar（AEM Forms が JBoss にデプロイされている場合に必要）
* jbossall-client.jar（AEM Formsが JBoss にデプロイされている場合に必要）

これらの JAR ファイルの場所については、[AEM Forms Java ライブラリファイルの組み込み](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。

**署名クライアントの作成**

Signature サービスの操作をプログラムで実行する前に、Signature サービスクライアントを作成する必要があります。

**削除する署名を含む PDF ドキュメントの取得**

PDF ドキュメントから署名を削除するには、署名が含まれる PDF ドキュメントを取得する必要があります。

**署名フィールドからデジタル署名の削除**

PDF ドキュメントからデジタル署名を正しく削除するには、デジタル署名が含まれている署名フィールドの名前を指定する必要があります。また、デジタル署名を削除する権限が必要です。この権限がない場合は、例外が発生します。

**PDF ドキュメントを PDF ファイルとして保存**

Signature サービスで署名フィールドからデジタル署名が削除されたら、PDF ドキュメントを PDF ファイルとして保存し、Acrobat または Adobe Reader で開くことができます。

**関連トピック**

[Java API を使用したデジタル署名の削除](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-java-api)

[Web サービス API を使用したデジタル署名の削除](digitally-signing-certifying-documents.md#remove-digital-signatures-using-the-web-service-api)

[AEM Forms Java ライブラリファイルの組み込み](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[署名フィールドの追加](digitally-signing-certifying-documents.md#adding-signature-fields)

### Java API を使用したデジタル署名の削除 {#remove-digital-signatures-using-the-java-api}

Signature API（Java）を使用してデジタル署名を削除するには、次の手順を実行します。

1. プロジェクトファイルを含める

   Java プロジェクトのクラスパスに、adobe-signatures-client.jar などのクライアント JAR ファイルを含めます。

1. Signature クライアントを作成します。

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して `ServiceClientFactory` オブジェクトを渡すことにより、`SignatureServiceClient`オブジェクトを作成します。

1. 削除する署名が含まれている PDF ドキュメントを取得します。

   * 削除する署名が含まれている PDF ドキュメントを表す `java.io.FileInputStream` オブジェクトを作成します。このため、このオブジェクトのコンストラクターを使用して、PDF ドキュメントの場所を指定する文字列値を渡します。
   * コンストラクターを使用して `java.io.FileInputStream` オブジェクトを渡すことにより、`com.adobe.idp.Document` オブジェクトを作成します。

1. 署名フィールドからデジタル署名を削除します。

   を呼び出して、署名フィールドから電子署名を削除する `SignatureServiceClient` オブジェクトの `clearSignatureField` メソッドを使用して、次の値を渡します。

   * 削除する署名が含まれている PDF ドキュメントを表す `com.adobe.idp.Document` オブジェクト。
   * デジタル署名が含まれている署名フィールドの名前を示す文字列値。

   `clearSignatureField` メソッドは、デジタル署名が削除された PDF ドキュメントを表す `com.adobe.idp.Document` オブジェクトを返します。

1. PDFドキュメントを PDF ファイルとして保存する

   * `java.io.File` オブジェクトを作成し、ファイル拡張子が .pdf であることを確認します。
   * を呼び出す `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッド。 `java.io.File` オブジェクトを渡して、`com.adobe.idp.Document` オブジェクトの内容をファイルにコピーします。  `clearSignatureField` メソッドから返された `Document` オブジェクトを必ず使用してください。

**関連トピック**

[デジタル署名の削除](digitally-signing-certifying-documents.md#removing-digital-signatures)

[クイックスタート（SOAP モード）：Java API を使用したデジタル署名の削除](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-removing-a-digital-signature-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用したデジタル署名の削除 {#remove-digital-signatures-using-the-web-service-api}

Signature API（Web サービス）を使用してデジタル署名を削除します。

1. プロジェクトファイルを含める

   MTOM を使用する Microsoft .NET プロジェクトを作成します。WSDL 定義 `http://localhost:8080/soap/services/SignatureService?WSDL&lc_version=9.0.1` を使用するようにします。

   >[!NOTE]
   >
   >`localhost` を、AEM Forms をホストするサーバーの IP アドレスに置き換えてください。

1. Signature クライアントの作成

   * デフォルトのコンストラクターを使用して `SignatureServiceClient` オブジェクトを作成します。
   * `System.ServiceModel.EndpointAddress` コンストラクターを使用して`SignatureServiceClient.Endpoint.Address` オブジェクトを作成します。WSDL を 指定する文字列値を AEM Forms サービスに渡します（例：`http://localhost:8080/soap/services/SignatureService?WSDL`）。`lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。
   * `SignatureServiceClient.Endpoint.Binding` フィールドの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
   * を設定します。 `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` ～に向かって `WSMessageEncoding.Mtom`. この値により、MTOM が確実に使用されます。
   * 次のタスクを実行して、HTTP 基本認証を有効にします。

      * `SignatureServiceClient.ClientCredentials.UserName.UserName` フィールドに AEM Forms ユーザー名を割り当てます。
      * 対応するパスワード値を `SignatureServiceClient.ClientCredentials.UserName.Password` フィールドに割り当てます。
      * 定数値 `HttpClientCredentialType.Basic` を`BasicHttpBindingSecurity.Transport.ClientCredentialType` フィールドに割り当てます。
      * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` をフィールド `BasicHttpBindingSecurity.Security.Mode` に割り当てます。

1. 削除する署名が含まれている PDF ドキュメントを取得します。

   * コンストラクターを使用して `BLOB` オブジェクトを作成します。`BLOB` オブジェクトは、削除するデジタル署名が含まれる PDF ドキュメントを格納するため使用されます。
   * `System.IO.FileStream` オブジェクトを作成します。このため、このオブジェクトのコンストラクターを呼び出し、署名付き PDF ドキュメントのファイルの場所と、ファイルを開くモードを表す文字列値を渡します。
   * `System.IO.FileStream` オブジェクトのコンテンツを格納するバイト配列を作成します。バイト配列のサイズは、 `System.IO.FileStream` オブジェクトの `Length` プロパティ。
   * を呼び出して、バイト配列にストリームデータを入力します。 `System.IO.FileStream` オブジェクトの `Read` メソッド。 読み取り対象のバイト配列、開始位置、ストリーム長を渡します。
   * `MTOM` プロパティを割り当てることで、`BLOB` オブジェクトにバイト配列のコンテンツを入力します。

1. 署名フィールドからデジタル署名を削除します。

   を呼び出して電子署名を削除する `SignatureServiceClient` オブジェクトの `clearSignatureField` メソッドを使用して、次の値を渡します。

   * 署名付き PDF ドキュメントを含む `BLOB` オブジェクト。
   * 削除するデジタル署名が含まれている署名フィールドの名前を表す文字列値です。

   この `clearSignatureField` メソッドは、デジタル署名が削除された PDF ドキュメントを表す `BLOB` オブジェクトを返します。

1. PDFドキュメントを PDF ファイルとして保存する

   * `System.IO.FileStream` オブジェクトを作成するには、そのコンストラクターを呼び出し、空の署名フィールドとファイルを開くモードを含む PDF ドキュメントのファイルの場所を表す文字列値を渡します。
   * `sign` メソッドによって返された `BLOB` オブジェクトのコンテンツを格納するバイト配列を作成します。バイト配列を生成するには、 `BLOB` オブジェクトの `MTOM` データメンバー。
   * コンストラクターを呼び出して `System.IO.FileStream` オブジェクトを渡すことによって、`System.IO.BinaryWriter` オブジェクトを作成します。
   * を呼び出して、バイト配列の内容をPDFファイルに書き込みます。 `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを使用してバイト配列を渡す。

**関連トピック**

[デジタル署名の削除](digitally-signing-certifying-documents.md#removing-digital-signatures)

[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
