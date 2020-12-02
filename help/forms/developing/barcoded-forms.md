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


# バーコードフォームの操作{#working-with-barcoded-forms}

## バーコードフォームサービスについて{#about-the-barcoded-forms-service}

バーコードフォームサービスは、記入と印刷のフォームからのデータの取得を自動化し、取得した情報を組織の中核的なITシステムに統合します。

バーコードフォームサービスを使用すると、1次元および2次元のバーコードをインタラクティブPDF formsに追加できます。 その後、バーコードフォームをWebサイトに発行したり、電子メールまたはCDで配布したりできます。 ユーザーがAdobe Reader、Acrobatプロフェッショナル、Acrobat Standardを使用してバーコードフォームに入力すると、バーコードが自動的に更新され、ユーザーが入力したフォームデータがエンコードされます。 ユーザーはフォームを電子的に送信したり、紙に印刷してメール、Fax、または手渡しで送信したりできます。 ユーザーが提供したデータは、後で自動化されたワークフローの一部として抽出し、承認プロセスやビジネスシステム間でルーティングできます。

バーコードフォームサービスの詳細については、『[AEM Forms向けサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

## Barcoded Form Data {#decoding-barcoded-form-data}のデコード

Barcoded FormsサービスAPIを使用して、PDFフォームまたはバーコードを含む画像からデータをデコードできます。 フォームデータのデコードとは、バーコード内のデータを抽出することです。 PDFフォーム（または画像）からデータをデコードする前に、ユーザーはフォームにデータを入力する必要があります。

>[!NOTE]
>
>バーコードフォームサービスの詳細については、『[AEM Forms向けサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順{#summary-of-steps}の概要

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

AEM FormsがJBOSS以外のサポート対象のJ2EEアプリケーションサーバーにデプロイされている場合は、adobe-utilities.jarおよびjbossall-client.jarを、AEM FormsがデプロイされているJ2EEアプリケーションサーバーに固有のJARファイルに置き換える必要があります。 すべてのAEM FormsJARファイルの場所については、「[AEM FormsJavaライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)」を参照してください。

**バーコードフォームクライアントAPIオブジェクトの作成**

プログラムを使用してBarcoded Formsサービスの操作を実行する前に、BarcodedFormsサービスクライアントを作成する必要があります。 Java APIを使用している場合は、`BarcodedFormsServiceClient`オブジェクトを作成します。 Barcoded Forms WebサービスAPIを使用している場合は、`BarcodedFormsServiceService`オブジェクトを作成します。

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

デコードAPIの16進数の文字セット入力は、バーコードの内容が16進文字列としてエンコードされることを意味します。 例えば、フォームで文字エンコーディングとしてUTF-8を指定し、デコード操作でHexを指定した場合、バーコードの内容はデコードされた出力の`xb:content`要素に16進文字列としてエンコードされます。 クライアントアプリケーションでアプリケーションロジックを作成すると、この16進値を変換して元の内容を取得できます。

**データをXMLデータソースに変換します**

フォームデータをデコードした後、XDPまたはXFDFデータに変換できます。 例えば、データを別のフォームに読み込むとします。 データをXFAフォームに読み込むには、データをXDPデータに変換する必要があります。 詳しくは、[フォームデータの読み込み](/help/forms/developing/importing-exporting-data.md#importing-form-data)を参照してください。

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

### Java API {#decode-barcoded-form-data-using-the-java-api}を使用してバーコードフォームデータをデコードする

Barcoded Forms API(Java)を使用してフォームデータをデコードします。

1. プロジェクトファイルを含める

   JavaプロジェクトのクラスパスにクライアントJARファイルを含めます。

1. バーコードフォームクライアントAPIオブジェクトの作成

   コンストラクターを使用し、接続プロパティを含む`ServiceClientFactory`オブジェクトを渡して、`BarcodedFormsServiceClient`オブジェクトを作成します。

1. バーコードデータを含むPDFフォームの取得

   * コンストラクターを使用し、PDFドキュメントの場所を指定する文字列値を渡して、バーコードデータを含むPDFフォームを表す`java.io.FileInputStream`オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PDFフォームからデータをデコードする

   `BarcodedFormsServiceClient`オブジェクトの`decode`メソッドを呼び出し、次の値を渡して、フォームデータをデコードします。

   * PDFフォームを含む`com.adobe.idp.Document`オブジェクトです。
   * PDF417バーコードをデコードするかどうかを指定する`java.lang.Boolean`オブジェクト。
   * データマトリクスバーコードをデコードするかどうかを指定する`java.lang.Boolean`オブジェクト。
   * QRコードバーコードをデコードするかどうかを指定する`java.lang.Boolean`オブジェクトです。
   * codabarバーコードをデコードするかどうかを指定する`java.lang.Boolean`オブジェクト。
   * コード128バーコードをデコードするかどうかを指定する`java.lang.Boolean`オブジェクト。
   * コード39バーコードをデコードするかどうかを指定する`java.lang.Boolean`オブジェクト。
   * EAN-13バーコードをデコードするかどうかを指定する`java.lang.Boolean`オブジェクト。
   * EAN-8バーコードをデコードするかどうかを指定する`java.lang.Boolean`オブジェクト。
   * バーコードで使用される文字セットエンコーディング値を指定する`com.adobe.livecycle.barcodedforms.CharSet`定義済みリスト値。

   `decode`メソッドは、デコードされたフォームデータを含む`org.w3c.dom.Document`オブジェクトを返します。

1. データをXMLデータソースに変換します

   `BarcodedFormsServiceClient`オブジェクトの`extractToXML`メソッドを呼び出し、次の値を渡して、デコードされたデータをXDPまたはXFDFデータに変換します。

   * デコードされたデータを含む`org.w3c.dom.Document`オブジェクト（`decode`メソッドの戻り値を使用してください）。
   * 行区切り文字を指定する`com.adobe.livecycle.barcodedforms.Delimiter`定義済みリスト値。 `Delimiter.Carriage_Return`を指定することをお勧めします。
   * フィールド区切り文字を指定する`com.adobe.livecycle.barcodedforms.Delimiter`定義済みリスト値。 例えば、`Delimiter.Tab`と指定します。
   * バーコードデータをXDPまたはXFDFのXMLデータに変換するかどうかを指定する`com.adobe.livecycle.barcodedforms.XMLFormat`定義済みリスト値。 例えば、`XMLFormat.XDP`を指定してデータをXDPデータに変換します。

   >[!NOTE]
   >
   >行区切り文字パラメーターとフィールド区切り文字パラメーターには、同じ値を指定しないでください。

   `extractToXML`メソッドは、`java.util.List`オブジェクトを返します。各要素は`org.w3c.dom.Document`オブジェクトです。 フォーム上のバーコードごとに個別の要素があります。 つまり、フォームに4つのバーコードがある場合、返される`java.util.List`オブジェクトに4つの要素があります。

1. デコードされたデータを処理します

   * `java.util.List`オブジェクトを繰り返し処理して、リスト内の各`org.w3c.dom.Document`オブジェクトを取得します。
   * リスト内の各要素について、`org.w3c.dom.Document`オブジェクトを`com.adobe.idp.Document`オブジェクトに変換します。 （Java APIの例を使用したバーコードフォームデータのデコードでは、`org.w3c.dom.Document`オブジェクトを`com.adobe.idp.Document`オブジェクトに変換するアプリケーションロジックを示します）。
   * `com.adobe.idp.Document`オブジェクトの`copyToFile`を呼び出し、そのXMLファイルを表すFileオブジェクトを渡して、XMLデータをXMLファイルとして保存します。

**関連トピック**

[クイック開始（SOAPモード）:Java APIを使用したバーコードフォームデータのデコード](/help/forms/developing/barcoded-forms-service-java-api.md#quick-start-soap-mode-decoding-barcoded-form-data-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#decode-barcoded-form-data-using-the-web-service-api}を使用してバーコードフォームデータをデコードする

Barcoded Forms API（Webサービス）を使用してフォームデータをデコードします。

1. プロジェクトファイルを含める

   * バーコードフォームサービスWSDLを使用するMicrosoft .NETクライアントアセンブリを作成します。 詳しくは、[Base64エンコードを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)を参照してください。
   * Microsoft .NETクライアントアセンブリを参照します。 詳しくは、[Base64エンコード](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)を使用したAEM Formsの呼び出しの「.NETクライアントアセンブリの参照」を参照してください。

1. バーコードフォームクライアントAPIオブジェクトの作成

   Barcoded Forms Service WSDLを使用するMicrosoft .NETクライアントアセンブリを使用し、デフォルトのコンストラクターを呼び出して`BarcodedFormsServiceService`オブジェクトを作成します。

1. バーコードデータを含むPDFフォームの取得

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、バーコードを含むPDFドキュメントの保存に使用されます。
   * コンストラクターを呼び出し、PDFドキュメントーのファイルの場所とファイルを開くモードを表す文字列値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得して、バイト配列のサイズを決定できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことで、バイト配列にストリームデータを入力します。
   * `BLOB`オブジェクトに`binaryData`プロパティを割り当て、バイト配列の内容を指定します。

1. PDFフォームからデータをデコードする

   `BarcodedFormsServiceService`オブジェクトの`decode`メソッドを呼び出し、次の値を渡して、フォームデータをデコードします。

   * PDFフォームを含む`BLOB`オブジェクトです。
   * PDF417バーコードをデコードするかどうかを指定する`Boolean`オブジェクト。
   * データマトリクスバーコードをデコードするかどうかを指定する`Boolean`オブジェクト。
   * QRコードバーコードをデコードするかどうかを指定する`Boolean`オブジェクトです。
   * codabarバーコードをデコードするかどうかを指定する`Boolean`オブジェクト。
   * コード128バーコードをデコードするかどうかを指定する`Boolean`オブジェクト。
   * コード39バーコードをデコードするかどうかを指定する`Bolean`オブジェクト。
   * EAN-13バーコードをデコードするかどうかを指定する`Boolean`オブジェクト。
   * EAN-8バーコードをデコードするかどうかを指定する`Boolean`オブジェクト。
   * バーコードで使用される文字セットエンコーディング値を指定する`CharSet`定義済みリスト値。

   `decode`メソッドは、デコードされたフォームデータを含む文字列値を返します。

1. データをXMLデータソースに変換します

   `BarcodedFormsServiceService`オブジェクトの`extractToXML`メソッドを呼び出し、次の値を渡して、デコードされたデータをXDPまたはXFDFデータに変換します。

   * デコードされたデータを含むstring値（`decode`メソッドの戻り値を必ず使用してください）。
   * 行区切り文字を指定する`Delimiter`定義済みリスト値。 `Delimiter.Carriage_Return`を指定することをお勧めします。
   * フィールド区切り文字を指定する`Delimiter`定義済みリスト値。 例えば、`Delimiter.Tab`と指定します。
   * バーコードデータをXDPまたはXFDFのXMLデータに変換するかどうかを指定する`XMLFormat`定義済みリスト値。 例えば、`XMLFormat.XDP`を指定してデータをXDPデータに変換します。

   >[!NOTE]
   >
   >行区切り文字パラメーターとフィールド区切り文字パラメーターには、同じ値を指定しないでください。

   `extractToXML`メソッドは、`Object`配列を返します。各要素は`BLOB`インスタンスです。 フォーム上のバーコードごとに個別の要素があります。 つまり、フォームに4つのバーコードがある場合、返される`Object`配列に4つの要素があります。

1. デコードされたデータを処理します

   * コンストラクターを呼び出し、保護されたPDFドキュメントーのファイルの場所を表す文字列値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `encryptPDFUsingPassword`メソッドから返された`BLOB`オブジェクトのデータ内容を格納するバイト配列を作成します。 `BLOB`オブジェクトの`binaryData`データメンバの値を取得して、バイト配列を入力します。
   * コンストラクターを呼び出して`System.IO.FileStream`オブジェクトを渡し、`System.IO.BinaryWriter`オブジェクトを作成します。
   * `System.IO.BinaryWriter`オブジェクトの`Write`メソッドを呼び出し、バイト配列を渡すことで、バイト配列の内容をPDFファイルに書き込みます。

**関連トピック**

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
