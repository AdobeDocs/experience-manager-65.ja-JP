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
workflow-type: tm+mt
source-wordcount: '1891'
ht-degree: 2%

---


# バーコードフォームの操作 {#working-with-barcoded-forms}

## Barcoded Formsサービスについて {#about-the-barcoded-forms-service}

バーコードフォームサービスは、記入と印刷のフォームからのデータの取得を自動化し、取得した情報を組織の中核的なITシステムに統合します。

バーコードフォームサービスを使用すると、1次元および2次元のバーコードをインタラクティブPDF formsに追加できます。 その後、バーコードフォームをWebサイトに発行したり、電子メールまたはCDで配布したりできます。 ユーザーがAdobe Reader、Acrobatプロフェッショナル、Acrobat Standardを使用してバーコードフォームに入力すると、バーコードが自動的に更新され、ユーザーが入力したフォームデータがエンコードされます。 ユーザーはフォームを電子的に送信したり、紙に印刷してメール、Fax、または手渡しで送信したりできます。 ユーザーが提供したデータは、後で自動化されたワークフローの一部として抽出し、承認プロセスやビジネスシステム間でルーティングできます。

For more information about the barcoded forms service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## バーコードフォームデータのデコード {#decoding-barcoded-form-data}

Barcoded FormsサービスAPIを使用して、PDFフォームまたはバーコードを含む画像からデータをデコードできます。 フォームデータのデコードとは、バーコード内のデータを抽出することです。 PDFフォーム（または画像）からデータをデコードする前に、ユーザーはフォームにデータを入力する必要があります。

>[!NOTE]
>
>For more information about the barcoded forms service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary-of-steps}

PDFフォームからデータをデコードするには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Barcoded FormsClient APIオブジェクトを作成します。
1. バーコードデータを含むPDFフォームを取得します。
1. PDFフォームからデータをデコードします。
1. データをXMLデータソースに変換します。
1. デコードされたデータを処理します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めます。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-barcodedforms-client.jar
* adobe-utilities.jar(AEM FormsがJBossにデプロイされている場合に必須)
* jbossall-client.jar(AEM FormsがJBossにデプロイされている場合に必須)
* xercesImpl.jar(&lt;install directory>/Adobe/Adobe/Experience_Manager_forms/sdk/client-libs\thirdpartyにあります)

AEM FormsがJBOSS以外のサポート対象のJ2EEアプリケーションサーバーにデプロイされている場合は、adobe-utilities.jarおよびjbossall-client.jarを、AEM FormsがデプロイされているJ2EEアプリケーションサーバーに固有のJARファイルに置き換える必要があります。 For information about the location of all AEM Forms JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**バーコードフォームクライアントAPIオブジェクトの作成**

プログラムを使用してBarcoded Formsサービスの操作を実行する前に、BarcodedFormsサービスクライアントを作成する必要があります。 Java APIを使用している場合は、 `BarcodedFormsServiceClient` オブジェクトを作成します。 Barcoded Forms WebサービスAPIを使用している場合は、 `BarcodedFormsServiceService` オブジェクトを作成します。

**バーコードデータを含むPDFフォームの取得**

ユーザーデータが埋め込まれたバーコードを含むPDFフォームを取得する必要があります。

**PDFフォームからデータをデコードする**

バーコードを含むPDFフォーム（または画像）を取得したら、データをデコードできます。 Barcoded Barcoded Serviceは、次の種類のバーコードをサポートします。

* PDF417バーコード。
* データマトリクスバーコード。
* QRコードバーコード。
* Codabarバーコード。
* Code 128バーコード。
* Code 39バーコード。
* EAN-13バーコード。
* EAN-8バーコード。

デコードAPIの16進数の文字セット入力は、バーコードの内容が16進文字列としてエンコードされることを意味します。 例えば、フォームで文字エンコーディングとしてUTF-8を指定し、デコード操作でHexを指定した場合、バーコードの内容は、デコードされた出力の&lt; `xb:content`>要素で16進文字列としてエンコードされます。 クライアントアプリケーションでアプリケーションロジックを作成すると、この16進値を変換して元の内容を取得できます。

**データをXMLデータソースに変換します**

フォームデータをデコードした後、XDPまたはXFDFデータに変換できます。 例えば、データを別のフォームに読み込むとします。 データをXFAフォームに読み込むには、データをXDPデータに変換する必要があります。 詳しくは、「フォームデータの [読み込み](/help/forms/developing/importing-exporting-data.md#importing-form-data)」を参照してください。

**デコードされたデータを処理します**

変換されたデータは、ビジネス要件に合わせて処理できます。 例えば、データをデコードして変換した後に、データをファイルに保存し、エンタープライズデータベースに保存し、別のフォームに入力するなどの操作を行うことができます。 この節では、変換されたデータをXMLファイルとして保存する方法について説明します。

>[!NOTE]
>
>行区切り文字とフィールド区切り文字のパラメーターの値が同じ場合、バーコードフォームサービスはバーコードデータのデコードに失敗します

**関連トピック**

[Java APIを使用したバーコードフォームデータのデコード](barcoded-forms.md#decode-barcoded-form-data-using-the-java-api)

[WebサービスAPIを使用したバーコードフォームデータのデコード](barcoded-forms.md#decode-barcoded-form-data-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java APIを使用したバーコードフォームデータのデコード {#decode-barcoded-form-data-using-the-java-api}

Barcoded Forms API(Java)を使用してフォームデータをデコードします。

1. プロジェクトファイルを含める

   JavaプロジェクトのクラスパスにクライアントJARファイルを含めます。

1. バーコードフォームクライアントAPIオブジェクトの作成

   コンストラクタを使用し、接続プロパティを含むオブジェクトを渡して、 `BarcodedFormsServiceClient``ServiceClientFactory` オブジェクトを作成します。

1. バーコードデータを含むPDFフォームの取得

   * コンストラクターを使用し、PDFドキュメントの場所を指定するstring値を渡して、バーコードデータが含まれるPDFフォームを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PDFフォームからデータをデコードする

   オブジェクトの `BarcodedFormsServiceClient` メソッドを呼び出し、次の値を渡して、フォームデータをデコードし `decode` ます。

   * PDFフォームを含む `com.adobe.idp.Document` オブジェクトです。
   * PDF417バーコードをデコードするかどうかを指定する `java.lang.Boolean` オブジェクトです。
   * データマトリクスバーコードをデコードするかどうかを指定する `java.lang.Boolean` オブジェクトです。
   * QRコードバーコードをデコードするかどうかを指定する `java.lang.Boolean` オブジェクトです。
   * Codabar Barcodeをデコードするかどうかを指定する `java.lang.Boolean` オブジェクトです。
   * コード128バーコードをデコードするかどうかを指定する `java.lang.Boolean` オブジェクト。
   * コード39バーコードをデコードするかどうかを指定する `java.lang.Boolean` オブジェクト。
   * EAN-13バーコードをデコードするかどうかを指定する `java.lang.Boolean` オブジェクト。
   * EAN-8バーコードをデコードするかどうかを指定する `java.lang.Boolean` オブジェクト。
   * A `com.adobe.livecycle.barcodedforms.CharSet` enumeration value that specifies the character set encoding value used in the barcode.

   この `decode` メソッドは、デコードされたフォームデータを含む `org.w3c.dom.Document` オブジェクトを返します。

1. データをXMLデータソースに変換します

   オブジェクトのメソッドを呼び出し、次の値を渡して、デコードされたデータをXDPまたはXFDF `BarcodedFormsServiceClient` データに変換し `extractToXML` ます。

   * デコードされたデータを含む `org.w3c.dom.Document` オブジェクト( `decode` メソッドの戻り値を必ず使用)。
   * 行区切り文字を指定する `com.adobe.livecycle.barcodedforms.Delimiter` 定義済みリスト値。 指定することをお勧めし `Delimiter.Carriage_Return`ます。
   * フィールド区切り文字を指定する `com.adobe.livecycle.barcodedforms.Delimiter` 定義済みリスト値。 For example, specify `Delimiter.Tab`.
   * バーコードデータをXDPデータに変換するかXFDF XMLデータに変換するかを指定する `com.adobe.livecycle.barcodedforms.XMLFormat` 定義済みリスト値です。 例えば、データをXDPデータ `XMLFormat.XDP` に変換するように指定します。

   >[!NOTE]
   >
   >行区切り文字パラメーターとフィールド区切り文字パラメーターには、同じ値を指定しないでください。

   この `extractToXML` メソッドは、各要素がオブジェクトである `java.util.List` オブジェクトを返 `org.w3c.dom.Document` します。 フォーム上のバーコードごとに個別の要素があります。 つまり、フォームに4つのバーコードがある場合、返される `java.util.List` オブジェクトには4つの要素があります。

1. デコードされたデータを処理します

   * オブジェクトを繰り返し処理して、リスト内の各 `java.util.List``org.w3c.dom.Document` オブジェクトを取得します。
   * リスト内の各要素に対して、その `org.w3c.dom.Document` オブジェクトをオブジェクトに変換し `com.adobe.idp.Document` ます。 (Java APIの例を使用したバーコードフォームデータのデコードでは、 `org.w3c.dom.Document` オブジェクトを `com.adobe.idp.Document` オブジェクトに変換するアプリケーションロジックを示します)。
   * オブジェクトを呼び出し、そのXMLファイルを表すFileオブジェクトを渡すことで、XML `com.adobe.idp.Document` データをXMLファイル `copyToFile`として保存します。

**関連トピック**

[クイック開始（SOAPモード）:Java APIを使用したバーコードフォームデータのデコード](/help/forms/developing/barcoded-forms-service-java-api.md#quick-start-soap-mode-decoding-barcoded-form-data-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したバーコードフォームデータのデコード {#decode-barcoded-form-data-using-the-web-service-api}

Barcoded Forms API（Webサービス）を使用してフォームデータをデコードします。

1. プロジェクトファイルを含める

   * バーコードフォームサービスWSDLを使用するMicrosoft .NETクライアントアセンブリを作成します。 詳しくは、Base64エンコーディングを使用した [AEM Formsの呼び出しを参照してください](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)。
   * Microsoft .NETクライアントアセンブリを参照します。 詳しくは、「Base64エンコーディングを使用したAEM Formsの [呼び出し」の「.NETクライアントアセンブリの参照」を参照してください](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)。

1. バーコードフォームクライアントAPIオブジェクトの作成

   Barcoded Forms Service WSDLを使用するMicrosoft .NETクライアントアセンブリを使用し、デフォルトのコンストラクターを呼び出して `BarcodedFormsServiceService` オブジェクトを作成します。

1. バーコードデータを含むPDFフォームの取得

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。この `BLOB` オブジェクトは、バーコードが含まれるPDFドキュメントの保存に使用されます。
   * コンストラクターを呼び出し、PDFドキュメントーのファイルの場所とファイルを開くモードを表すstring値を渡して、 `System.IO.FileStream` オブジェクトを作成します。
   * オブジェクトの内容を格納するバイト配列を作成し `System.IO.FileStream` ます。 バイト配列のサイズは、 `System.IO.FileStream` オブジェクトのプロパティを取得して決定でき `Length` ます。
   * オブジェクトの `System.IO.FileStream``Read` メソッドを呼び出し、読み取るバイト配列、開始位置およびストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * オブジェクトのプロパティにバイト配列の内容を割り当てて、 `BLOB``binaryData` オブジェクトを入力します。

1. PDFフォームからデータをデコードする

   オブジェクトの `BarcodedFormsServiceService` メソッドを呼び出し、次の値を渡して、フォームデータをデコードし `decode` ます。

   * PDFフォームを含む `BLOB` オブジェクトです。
   * PDF417バーコードをデコードするかどうかを指定する `Boolean` オブジェクトです。
   * データマトリクスバーコードをデコードするかどうかを指定する `Boolean` オブジェクトです。
   * QRコードバーコードをデコードするかどうかを指定する `Boolean` オブジェクトです。
   * Codabar Barcodeをデコードするかどうかを指定する `Boolean` オブジェクトです。
   * コード128バーコードをデコードするかどうかを指定する `Boolean` オブジェクト。
   * コード39バーコードをデコードするかどうかを指定する `Bolean` オブジェクト。
   * EAN-13バーコードをデコードするかどうかを指定する `Boolean` オブジェクト。
   * EAN-8バーコードをデコードするかどうかを指定する `Boolean` オブジェクト。
   * A `CharSet` enumeration value that specifies the character set encoding value used in the barcode.

   この `decode` メソッドは、デコードされたフォームデータを含む文字列値を返します。

1. データをXMLデータソースに変換します

   オブジェクトのメソッドを呼び出し、次の値を渡して、デコードされたデータをXDPまたはXFDF `BarcodedFormsServiceService` データに変換し `extractToXML` ます。

   * デコードされたデータを格納するstring値( `decode` メソッドの戻り値を必ず使用)。
   * 行区切り文字を指定する `Delimiter` 定義済みリスト値。 指定することをお勧めし `Delimiter.Carriage_Return`ます。
   * フィールド区切り文字を指定する `Delimiter` 定義済みリスト値。 For example, specify `Delimiter.Tab`.
   * バーコードデータをXDPデータに変換するかXFDF XMLデータに変換するかを指定する `XMLFormat` 定義済みリスト値です。 例えば、データをXDPデータ `XMLFormat.XDP` に変換するように指定します。

   >[!NOTE]
   >
   >行区切り文字パラメーターとフィールド区切り文字パラメーターには、同じ値を指定しないでください。

   この `extractToXML` メソッドは、各要素がインスタンスである `Object` 配列を返 `BLOB` します。 フォーム上のバーコードごとに個別の要素があります。 つまり、フォームに4つのバーコードがある場合、返される `Object` 配列には4つの要素があります。

1. デコードされたデータを処理します

   * コンストラクターを呼び出し、保護されたPDF `System.IO.FileStream` ドキュメントーのファイルの場所を表すstring値を渡して、オブジェクトを作成します。
   * メソッドが返した `BLOB` オブジェクトのデータ内容を格納するバイト配列を作成し `encryptPDFUsingPassword` ます。 オブジェクトのデータメンバーの値を取得して、 `BLOB` バイト配列を入力し `binaryData` ます。
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * オブジェクトのメソッドを呼び出し、バイト配列を渡して、バイト配列の内容をPDFファイルに書き込み `System.IO.BinaryWriter` ま `Write` す。

**関連トピック**

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
