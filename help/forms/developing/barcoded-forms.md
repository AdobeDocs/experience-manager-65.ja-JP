---
title: バーコードフォームの操作
seo-title: バーコードフォームの操作
description: 'null'
seo-description: 'null'
uuid: e56c3c94-384d-401f-b418-dd34cdc57eda
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: eb28ac30-265c-4611-8247-1f4bc826f254
translation-type: tm+mt
source-git-commit: 413af4ef9bc3652e05da78d622183bcf20a8bee7

---


# バーコードフォームの操作 {#working-with-barcoded-forms}

## バーコードフォームサービスについて {#about-the-barcoded-forms-service}

バーコードフォームサービスは、入力および印刷フォームからのデータの取得を自動化し、取得した情報を組織のコアITシステムに統合します。

バーコードフォームサービスを使用して、インタラクティブPDFフォームに1次元および2次元のバーコードを追加できます。 その後、バーコードフォームをWebサイトに発行したり、電子メールまたはCDで配布したりできます。 ユーザーがAdobe Reader、Acrobat ProfessionalまたはAcrobat Standardを使用してバーコードフォームに入力すると、バーコードは自動的に更新され、ユーザーが入力したフォームデータがエンコードされます。 ユーザーは、フォームを電子的に送信したり、紙に印刷して、メール、Fax、または手渡しで送信したりできます。 後で、ユーザーが提供したデータを自動ワークフローの一部として抽出し、承認プロセスやビジネスシステム間でデータをルーティングできます。

For more information about the barcoded forms service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## バーコードフォームデータのデコード {#decoding-barcoded-form-data}

バーコードフォームサービスAPIを使用して、PDFフォームまたはバーコードを含む画像からデータをデコードできます。 フォームデータのデコードとは、バーコード内のデータを抽出することです。 PDFフォーム（または画像）からデータをデコードする前に、ユーザーはフォームにデータを入力する必要があります。

>[!NOTE]
>
>For more information about the barcoded forms service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary-of-steps}

PDFフォームからデータをデコードするには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. バーコードフォームのClient APIオブジェクトを作成します。
1. バーコードデータを含むPDFフォームを取得します。
1. PDFフォームからデータをデコードします。
1. データをXMLデータソースに変換します。
1. デコードされたデータを処理します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-barcodedforms-client.jar
* adobe-utilities.jar（AEM FormsがJBossにデプロイされている場合に必須）
* jbossall-client.jar（AEM FormsがJBossにデプロイされている場合は必須）
* xercesImpl.jar（&lt;install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs\thirdpartyにあります）

AEM formsがJBOSS以外のサポート対象のJ2EEアプリケーションサーバーにデプロイされている場合は、adobe-utilities.jarおよびjbossall-client.jarを、AEM formsがデプロイされているJ2EEアプリケーションサーバーに固有のJARファイルに置き換える必要があります。 For information about the location of all AEM Forms JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**バーコードフォームクライアントAPIオブジェクトの作成**

プログラムでバーコードフォームサービス操作を実行する前に、Barcoded Formsサービスクライアントを作成する必要があります。 Java APIを使用している場合は、オブジェクトを作成し `BarcodedFormsServiceClient` ます。 バーコードフォームのWebサービスAPIを使用している場合は、オブジェクトを作成 `BarcodedFormsServiceService` します。

**バーコードデータを含むPDFフォームの取得**

ユーザーデータが入力されたバーコードを含むPDFフォームを取得する必要があります。

**PDFフォームからのデータのデコード**

バーコードを含むPDFフォーム（または画像）を取得したら、データをデコードできます。 Barcoded Formsサービスは、次の種類のバーコードをサポートします。

* PDF417バーコード。
* データマトリクスバーコード。
* QRコードバーコード。
* Codabarバーコード。
* Code 128バーコード。
* Code 39バーコード。
* EAN-13バーコード。
* EAN-8バーコード。

デコードAPIで16進数の文字セット入力は、バーコードのコンテンツが16進文字列としてエンコードされることを意味します。 例えば、フォームで文字エンコーディングとしてUTF-8を指定し、デコード操作でHexを指定した場合、バーコードのコンテンツは、デコードされた出力の&lt; `xb:content`>要素で16進文字列としてエンコードされます。 この16進数値を変換して元の内容を取得するには、クライアントアプリケーションでアプリケーションロジックを作成します。

**データをXMLデータソースに変換します**

フォームデータをデコードした後、XDPまたはXFDFデータに変換できます。 例えば、データを別のフォームに読み込むとします。 データをXFAフォームに読み込むには、データをXDPデータに変換する必要があります。 詳しくは、「フォームデータ [の読み込み」を参照してくださ](/help/forms/developing/importing-exporting-data.md#importing-form-data)い。

**デコードされたデータを処理します**

変換されたデータは、ビジネス要件に合わせて処理できます。 例えば、データをデコードして変換した後に、データをファイルに保存し、エンタープライズデータベースに保存し、別のフォームに入力するなどができます。 この節では、変換されたデータをXMLファイルとして保存する方法について説明します。

>[!NOTE]
>
>行区切り文字とフィールド区切り文字のパラメーターの値が同じ場合、バーコードフォームサービスはバーコードデータのデコードに失敗します

**関連トピック**

[Java APIを使用したバーコードフォームデータのデコード](barcoded-forms.md#decode-barcoded-form-data-using-the-java-api)

[WebサービスAPIを使用したバーコードフォームデータのデコード](barcoded-forms.md#decode-barcoded-form-data-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java APIを使用したバーコードフォームデータのデコード {#decode-barcoded-form-data-using-the-java-api}

バーコードフォームAPI(Java)を使用してフォームデータをデコードします。

1. プロジェクトファイルを含める

   JavaプロジェクトのクラスパスにクライアントJARファイルを含めます。

1. バーコードフォームクライアントAPIオブジェクトの作成

   コンストラク `BarcodedFormsServiceClient` ターを使用し、接続プロパティを含むオブジェクトを渡 `ServiceClientFactory` して、オブジェクトを作成します。

1. バーコードデータを含むPDFフォームの取得

   * コンストラク `java.io.FileInputStream` ターを使用し、PDFドキュメントの場所を指定するstring値を渡すことで、バーコードデータを含むPDFフォームを表すオブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PDFフォームからのデータのデコード

   オブジェクトのメソッドを呼び出し、次 `BarcodedFormsServiceClient` の値を渡して、 `decode` フォームデータをデコードします。

   * PDFフォ `com.adobe.idp.Document` ームを含むオブジェクトです。
   * PDF417バ `java.lang.Boolean` ーコードをデコードするかどうかを指定するオブジェクトです。
   * データ `java.lang.Boolean` マトリクスバーコードをデコードするかどうかを指定するオブジェクトです。
   * QRコー `java.lang.Boolean` ドバーコードをデコードするかどうかを指定するオブジェクトです。
   * コードバ `java.lang.Boolean` ーコードをデコードするかどうかを指定するオブジェクトです。
   * コード128 `java.lang.Boolean` バーコードをデコードするかどうかを指定するオブジェクトです。
   * コード39 `java.lang.Boolean` バーコードをデコードするかどうかを指定するオブジェクトです。
   * EAN-13 `java.lang.Boolean` バーコードをデコードするかどうかを指定するオブジェクトです。
   * EAN-8 `java.lang.Boolean` バーコードをデコードするかどうかを指定するオブジェクトです。
   * A `com.adobe.livecycle.barcodedforms.CharSet` enumeration value that specifies the character set encoding value used in the barcode.
   このメソ `decode` ッドは、デコードされた `org.w3c.dom.Document` フォームデータを含むオブジェクトを返します。

1. データをXMLデータソースに変換します

   オブジェクトのメソッドを呼び出し、次の値を渡して、デコードされたデ `BarcodedFormsServiceClient` ータをXDPまた `extractToXML` はXFDFデータに変換します。

   * デコ `org.w3c.dom.Document` ードされたデータを含むオブジェクトです(メソッドの戻り値 `decode` を必ず使用してください)。
   * 行区 `com.adobe.livecycle.barcodedforms.Delimiter` 切りを指定する列挙値。 指定することをお勧めしま `Delimiter.Carriage_Return`す。
   * フィ `com.adobe.livecycle.barcodedforms.Delimiter` ールド区切り文字を指定する列挙値。 For example, specify `Delimiter.Tab`.
   * バー `com.adobe.livecycle.barcodedforms.XMLFormat` コードデータをXDPまたはXFDF XMLデータに変換するかどうかを指定する列挙値。 例えば、データをXDP `XMLFormat.XDP` データに変換するように指定します。
   >[!NOTE]
   >
   >行区切り文字とフィールド区切り文字のパラメーターには、同じ値を指定しないでください。

   このメソ `extractToXML` ッドは、各要素がオ `java.util.List` ブジェクトであるオブジェクトを返 `org.w3c.dom.Document` します。 フォーム上のバーコードごとに別々の要素があります。 つまり、フォームにバーコードが4つある場合、返されるオブジェクトには4つの要素があ `java.util.List` ります。

1. デコードされたデータを処理します

   * オブジェクトを繰 `java.util.List` り返し処理して、リスト内の `org.w3c.dom.Document` 各オブジェクトを取得します。
   * リスト内の各要素に対して、オブジェクトをオブ `org.w3c.dom.Document` ジェクトに変換 `com.adobe.idp.Document` します。 (Java APIの例を使用したバーコードフォームデ `org.w3c.dom.Document` ータのデコードには、オ `com.adobe.idp.Document` ブジェクトをオブジェクトに変換するアプリケーションロジックが示されています)。
   * XMLデータをXMLファイルとして保存します。保存するには、オブジ `com.adobe.idp.Document` ェクトを呼び出 `copyToFile`し、XMLファイルを表すFileオブジェクトを渡します。

**関連トピック**

[クイックスタート（SOAPモード）:Java APIを使用したバーコードフォームデータのデコード](/help/forms/developing/barcoded-forms-service-java-api.md#quick-start-soap-mode-decoding-barcoded-form-data-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したバーコードフォームデータのデコード {#decode-barcoded-form-data-using-the-web-service-api}

バーコードフォームAPI（Webサービス）を使用してフォームデータをデコードします。

1. プロジェクトファイルを含める

   * バーコードフォームサービスWSDLを使用するMicrosoft .NETクライアントアセンブリを作成します。 詳しくは、「Base64エンコーデ [ィングを使用したAEM formsの呼び出し」を参照してくださ](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)い。
   * Microsoft .NETクライアントアセンブリを参照します。 詳しくは、「Base64エンコーディングを使用したAEM Formsの呼び出し」の「.NETク [ライアントアセンブリの参照](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)」を参照してください。

1. バーコードフォームクライアントAPIオブジェクトの作成

   バーコードフォームサービスWSDLを使用するMicrosoft .NETクライアントアセンブリを使用し、デフォルトのコンストラクターを呼び `BarcodedFormsServiceService` 出してオブジェクトを作成します。

1. バーコードデータを含むPDFフォームの取得

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、バーコードを含むPDFドキュメントの保存に使用されます。
   * オブジェクト `System.IO.FileStream` を作成するには、コンストラクターを呼び出し、PDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡します。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `System.IO.FileStream` します。 バイト配列のサイズは、オブジェクトのプロパティを取得するこ `System.IO.FileStream` とで指定で `Length` きます。
   * オブジェクトのメソッドを呼び出し、読み取るバイト配列、開 `System.IO.FileStream` 始位置、ストリ `Read` ーム長を渡すことによって、バイト配列にストリームデータを設定します。
   * オブジェクト `BLOB` にバイト配列の内容をプロ `binaryData` パティに割り当てて、オブジェクトを設定します。

1. PDFフォームからのデータのデコード

   オブジェクトのメソッドを呼び出し、次 `BarcodedFormsServiceService` の値を渡して、 `decode` フォームデータをデコードします。

   * PDFフォ `BLOB` ームを含むオブジェクトです。
   * PDF417バ `Boolean` ーコードをデコードするかどうかを指定するオブジェクトです。
   * データ `Boolean` マトリクスバーコードをデコードするかどうかを指定するオブジェクトです。
   * QRコー `Boolean` ドバーコードをデコードするかどうかを指定するオブジェクトです。
   * コードバ `Boolean` ーコードをデコードするかどうかを指定するオブジェクトです。
   * コード128 `Boolean` バーコードをデコードするかどうかを指定するオブジェクトです。
   * コード39 `Bolean` バーコードをデコードするかどうかを指定するオブジェクトです。
   * EAN-13 `Boolean` バーコードをデコードするかどうかを指定するオブジェクトです。
   * EAN-8 `Boolean` バーコードをデコードするかどうかを指定するオブジェクトです。
   * A `CharSet` enumeration value that specifies the character set encoding value used in the barcode.
   このメ `decode` ソッドは、デコードされたフォームデータを含むstring値を返します。

1. データをXMLデータソースに変換します

   オブジェクトのメソッドを呼び出し、次の値を渡して、デコードされたデ `BarcodedFormsServiceService` ータをXDPまた `extractToXML` はXFDFデータに変換します。

   * デコードされたデータを含むstring値(メソッドの戻り値を `decode` 必ず使用してください)。
   * 行区 `Delimiter` 切りを指定する列挙値。 指定することをお勧めしま `Delimiter.Carriage_Return`す。
   * フィ `Delimiter` ールド区切り文字を指定する列挙値。 For example, specify `Delimiter.Tab`.
   * バー `XMLFormat` コードデータをXDPまたはXFDF XMLデータに変換するかどうかを指定する列挙値。 例えば、データをXDP `XMLFormat.XDP` データに変換するように指定します。
   >[!NOTE]
   >
   >行区切り文字とフィールド区切り文字のパラメーターには、同じ値を指定しないでください。

   このメ `extractToXML` ソッドは、各要素 `Object` がインスタンスである配列を返 `BLOB` します。 フォーム上のバーコードごとに別々の要素があります。 つまり、フォームにバーコードが4つある場合、返される配列には4つの要素が含まれ `Object` ます。

1. デコードされたデータを処理します

   * オブジェクトを `System.IO.FileStream` 作成するには、コンストラクターを呼び出し、保護されたPDFドキュメントのファイルの場所を表すstring値を渡します。
   * メソッドによって返されたオブジェクトのデータ内容を格納 `BLOB` するバイト配列を作成 `encryptPDFUsingPassword` します。 オブジェクトのデータメンバーの値を取得して、バ `BLOB` イト配列を `binaryData` 設定します。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡すことで、バ `System.IO.BinaryWriter` イト配列の内 `Write` 容をPDFファイルに書き込みます。

**関連トピック**

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
