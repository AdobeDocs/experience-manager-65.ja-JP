---
title: バーコードフォームの操作
seo-title: バーコードフォームの操作
description: Java APIおよびWebサービスAPIを使用して、PDFフォームまたはバーコードを含む画像からデータをデコードします。
seo-description: Java APIおよびWebサービスAPIを使用して、PDFフォームまたはバーコードを含む画像からデータをデコードします。
uuid: e56c3c94-384d-401f-b418-dd34cdc57eda
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: eb28ac30-265c-4611-8247-1f4bc826f254
role: Developer
exl-id: dd32808e-b773-48a2-90e1-7a277d349493
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1945'
ht-degree: 2%

---

# バーコードフォームの操作{#working-with-barcoded-forms}

**このドキュメントのサンプルと例は、JEE上のAEM Forms環境に限られています。**

## バーコードフォームサービスについて{#about-the-barcoded-forms-service}

バーコードフォームサービスは、入力および印刷フォームからのデータのキャプチャを自動化し、取り込んだ情報を組織の主要なITシステムに統合します。

バーコードフォームサービスを使用すると、1次元および2次元のバーコードをインタラクティブPDF formsに追加できます。 その後、バーコードフォームをWebサイトに公開したり、電子メールまたはCDで配布したりできます。 ユーザーがAdobe Reader、Acrobat Professional、Acrobat Standardを使用してバーコードフォームに入力すると、ユーザーが指定したフォームデータがエンコードされるようにバーコードが自動的に更新されます。 ユーザーは、フォームを電子的に送信したり、紙に印刷してメール、ファックス、または手渡しで送信したりできます。 後で、ユーザーが提供したデータを自動ワークフローの一部として抽出し、承認プロセスやビジネスシステム間でデータをルーティングできます。

バーコードフォームサービスについて詳しくは、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

## バーコードフォームデータのデコード{#decoding-barcoded-form-data}

バーコードフォームサービスAPIを使用して、PDFフォームまたはバーコードを含む画像からデータをデコードできます。 フォームデータのデコードとは、バーコード内のデータを抽出することです。 PDFフォーム（または画像）からデータをデコードするには、ユーザーがフォームにデータを入力する必要があります。

>[!NOTE]
>
>バーコードフォームサービスについて詳しくは、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順の概要{#summary-of-steps}

PDFフォームからデータをデコードするには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. バーコードフォームクライアントAPIオブジェクトを作成します。
1. バーコードデータを含むPDFフォームを取得します。
1. PDFフォームからデータをデコードします。
1. データをXMLデータソースに変換します。
1. デコードされたデータを処理します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用する場合は、プロキシファイルを必ず含めてください。

次のJARファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-barcodedforms-client.jar
* adobe-utilities.jar(AEM FormsがJBossにデプロイされている場合に必須)
* jbossall-client.jar(AEM FormsがJBossにデプロイされている場合に必須)
* xercesImpl.jar(&lt;install directory>/directory/Adobe/Experience_Manager_forms/sdk/client-libs\thirdpartyにあります)

AEM FormsがJBOSS以外のサポート対象のJ2EEアプリケーションサーバーにデプロイされている場合は、adobe-utilities.jarとjbossall-client.jarを、AEM FormsがデプロイされているJ2EEアプリケーションサーバーに固有のJARファイルに置き換える必要があります。 すべてのAEM Forms JARファイルの場所について詳しくは、「[AEM Forms Javaライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)」を参照してください。

**バーコードフォームクライアントAPIオブジェクトの作成**

プログラムによってバーコードフォームサービス操作を実行する前に、Barcoded Formsサービスクライアントを作成する必要があります。 Java APIを使用している場合は、`BarcodedFormsServiceClient`オブジェクトを作成します。 バーコードフォームWebサービスAPIを使用している場合は、`BarcodedFormsServiceService`オブジェクトを作成します。

**バーコードデータを含むPDFフォームの取得**

ユーザーデータが入力されたバーコードを含むPDFフォームを取得する必要があります。

**PDFフォームからのデータのデコード**

バーコードを含むPDFフォーム（または画像）を取得したら、データをデコードできます。 Barcoded Formsサービスは、次の種類のバーコードをサポートします。

* PDF417バーコード。
* データ・マトリックス・バーコード。
* QRコードバーコード。
* コダバールバーコード。
* Code 128バーコード。
* Code 39バーコード。
* EAN-13バーコード。
* EAN-8バーコード。

デコードAPIで16進数で入力された文字セットは、バーコードのコンテンツが16進文字列としてエンコードされることを意味します。 例えば、フォームで文字エンコーディングにUTF-8を指定し、デコード操作でHexを指定した場合、バーコードのコンテンツはデコード出力の`xb:content`要素で16進文字列としてエンコードされます。 クライアントアプリケーションでアプリケーションロジックを作成することで、この16進数値を変換して元のコンテンツを取得できます。

**データをXMLデータソースに変換する**

フォームデータをデコードした後、XDPまたはXFDFデータに変換できます。 例えば、データを別のフォームに読み込むとします。 データをXFAフォームに読み込むには、データをXDPデータに変換する必要があります。 詳しくは、「[フォームデータの読み込み](/help/forms/developing/importing-exporting-data.md#importing-form-data)」を参照してください。

**デコードされたデータを処理する**

変換後のデータは、ビジネス要件に合わせて処理できます。 例えば、データをデコードして変換した後に、ファイルに保存し、エンタープライズデータベースに保存し、別のフォームに入力するなどをおこなうことができます。 この節では、変換後のデータをXMLファイルとして保存する方法について説明します。

>[!NOTE]
>
>行区切り文字とフィールド区切り文字のパラメーターが同じ値の場合、バーコードフォームサービスはバーコードデータのデコードに失敗します

**関連トピック**

[Java APIを使用したバーコードフォームデータのデコード](barcoded-forms.md#decode-barcoded-form-data-using-the-java-api)

[WebサービスAPIを使用したバーコードフォームデータのデコード](barcoded-forms.md#decode-barcoded-form-data-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java APIを使用してバーコードフォームデータをデコードする{#decode-barcoded-form-data-using-the-java-api}

Barcoded Forms API(Java)を使用してフォームデータをデコードします。

1. プロジェクトファイルを含める

   クライアントJARファイルをJavaプロジェクトのクラスパスに含めます。

1. バーコードフォームクライアントAPIオブジェクトの作成

   コンストラクターを使用し、接続プロパティを含む`ServiceClientFactory`オブジェクトを渡して、`BarcodedFormsServiceClient`オブジェクトを作成します。

1. バーコードデータを含むPDFフォームの取得

   * コンストラクターを使用してPDFドキュメントの場所を指定する文字列値を渡すことで、バーコードデータを含むPDFフォームを表す`java.io.FileInputStream`オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. PDFフォームからのデータのデコード

   `BarcodedFormsServiceClient`オブジェクトの`decode`メソッドを呼び出し、次の値を渡してフォームデータをデコードします。

   * PDFフォームを含む`com.adobe.idp.Document`オブジェクト。
   * PDF417バーコードをデコードするかどうかを指定する`java.lang.Boolean`オブジェクト。
   * データマトリックスバーコードをデコードするかどうかを指定する`java.lang.Boolean`オブジェクト。
   * QRコードバーコードをデコードするかどうかを指定する`java.lang.Boolean`オブジェクト。
   * コーダバーコードをデコードするかどうかを指定する`java.lang.Boolean`オブジェクト。
   * コード128バーコードをデコードするかどうかを指定する`java.lang.Boolean`オブジェクト。
   * コード39バーコードをデコードするかどうかを指定する`java.lang.Boolean`オブジェクト。
   * EAN-13バーコードをデコードするかどうかを指定する`java.lang.Boolean`オブジェクト。
   * EAN-8バーコードをデコードするかどうかを指定する`java.lang.Boolean`オブジェクト。
   * バーコードで使用される文字セットエンコーディング値を指定する`com.adobe.livecycle.barcodedforms.CharSet`列挙値。

   `decode`メソッドは、デコードされたフォームデータを含む`org.w3c.dom.Document`オブジェクトを返します。

1. データをXMLデータソースに変換する

   `BarcodedFormsServiceClient`オブジェクトの`extractToXML`メソッドを呼び出し、次の値を渡して、デコードされたデータをXDPまたはXFDFデータに変換します。

   * デコードされたデータを格納する`org.w3c.dom.Document`オブジェクト（`decode`メソッドの戻り値を使用するようにしてください）。
   * 行の区切り文字を指定する`com.adobe.livecycle.barcodedforms.Delimiter`列挙値。 `Delimiter.Carriage_Return`を指定することをお勧めします。
   * フィールド区切り文字を指定する`com.adobe.livecycle.barcodedforms.Delimiter`列挙値。 例えば、`Delimiter.Tab`と指定します。
   * バーコードデータをXDPまたはXFDF XMLデータに変換するかどうかを指定する`com.adobe.livecycle.barcodedforms.XMLFormat`列挙値。 例えば、`XMLFormat.XDP`と指定してデータをXDPデータに変換します。

   >[!NOTE]
   >
   >行区切り文字とフィールド区切り文字のパラメーターに同じ値を指定しないでください。

   `extractToXML`メソッドは`java.util.List`オブジェクトを返します。各要素は`org.w3c.dom.Document`オブジェクトです。 フォーム上にあるバーコードごとに別々の要素があります。 つまり、フォームに4つのバーコードがある場合、返される`java.util.List`オブジェクトに4つの要素があります。

1. デコードされたデータを処理する

   * `java.util.List`オブジェクトを繰り返し処理して、リスト内の各`org.w3c.dom.Document`オブジェクトを取得します。
   * リスト内の各要素について、`org.w3c.dom.Document`オブジェクトを`com.adobe.idp.Document`オブジェクトに変換します。 （Java APIの例を使用したバーコード化されたフォームデータのデコードでは、 `org.w3c.dom.Document`オブジェクトを`com.adobe.idp.Document`オブジェクトに変換するアプリケーションロジックを示しています）。
   * `com.adobe.idp.Document`オブジェクトの`copyToFile`を呼び出し、そのXMLファイルを表すFileオブジェクトを渡すことにより、XMLデータをXMLファイルとして保存します。

**関連トピック**

[クイックスタート（SOAPモード）:Java APIを使用したバーコードされたフォームデータのデコード](/help/forms/developing/barcoded-forms-service-java-api.md#quick-start-soap-mode-decoding-barcoded-form-data-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#decode-barcoded-form-data-using-the-web-service-api}を使用してバーコードされたフォームデータをデコードします

バーコードフォームAPI（Webサービス）を使用してフォームデータをデコードする：

1. プロジェクトファイルを含める

   * Barcoded FormsサービスWSDLを使用するMicrosoft .NETクライアントアセンブリを作成します。 詳しくは、 [Base64エンコーディング](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)を使用したAEM Formsの呼び出しを参照してください。
   * Microsoft .NETクライアントアセンブリを参照します。 詳しくは、[Base64エンコーディング](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)を使用したAEM Formsの呼び出しの「.NETクライアントアセンブリの参照」を参照してください。

1. バーコードフォームクライアントAPIオブジェクトの作成

   バーコードフォームサービスのWSDLを使用するMicrosoft .NETクライアントアセンブリを使用して、デフォルトのコンストラクタを呼び出して`BarcodedFormsServiceService`オブジェクトを作成します。

1. バーコードデータを含むPDFフォームの取得

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、バーコードを含むPDFドキュメントを保存するために使用されます。
   * コンストラクターを呼び出し、PDFドキュメントのファイルの場所とファイルを開くモードを表すstring値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `System.IO.FileStream`オブジェクトの内容を格納するバイト配列を作成します。 `System.IO.FileStream`オブジェクトの`Length`プロパティを取得することで、バイト配列のサイズを判断できます。
   * `System.IO.FileStream`オブジェクトの`Read`メソッドを呼び出し、読み取るバイト配列、開始位置、ストリーム長を渡すことによって、バイト配列にストリームデータを入力します。
   * `BLOB`オブジェクトの`binaryData`プロパティにバイト配列の内容を割り当てて、オブジェクトを設定します。

1. PDFフォームからのデータのデコード

   `BarcodedFormsServiceService`オブジェクトの`decode`メソッドを呼び出し、次の値を渡してフォームデータをデコードします。

   * PDFフォームを含む`BLOB`オブジェクト。
   * PDF417バーコードをデコードするかどうかを指定する`Boolean`オブジェクト。
   * データマトリックスバーコードをデコードするかどうかを指定する`Boolean`オブジェクト。
   * QRコードバーコードをデコードするかどうかを指定する`Boolean`オブジェクト。
   * コーダバーコードをデコードするかどうかを指定する`Boolean`オブジェクト。
   * コード128バーコードをデコードするかどうかを指定する`Boolean`オブジェクト。
   * コード39バーコードをデコードするかどうかを指定する`Bolean`オブジェクト。
   * EAN-13バーコードをデコードするかどうかを指定する`Boolean`オブジェクト。
   * EAN-8バーコードをデコードするかどうかを指定する`Boolean`オブジェクト。
   * バーコードで使用される文字セットエンコーディング値を指定する`CharSet`列挙値。

   `decode`メソッドは、デコードされたフォームデータを含む文字列値を返します。

1. データをXMLデータソースに変換する

   `BarcodedFormsServiceService`オブジェクトの`extractToXML`メソッドを呼び出し、次の値を渡して、デコードされたデータをXDPまたはXFDFデータに変換します。

   * デコードされたデータを格納するstring値（`decode`メソッドの戻り値を使用するようにしてください）。
   * 行の区切り文字を指定する`Delimiter`列挙値。 `Delimiter.Carriage_Return`を指定することをお勧めします。
   * フィールド区切り文字を指定する`Delimiter`列挙値。 例えば、`Delimiter.Tab`と指定します。
   * バーコードデータをXDPまたはXFDF XMLデータに変換するかどうかを指定する`XMLFormat`列挙値。 例えば、`XMLFormat.XDP`と指定してデータをXDPデータに変換します。

   >[!NOTE]
   >
   >行区切り文字とフィールド区切り文字のパラメーターに同じ値を指定しないでください。

   `extractToXML`メソッドは、`Object`配列を返します。各要素は`BLOB`インスタンスです。 フォーム上にあるバーコードごとに別々の要素があります。 つまり、フォームに4つのバーコードがある場合、返される`Object`配列には4つの要素が含まれます。

1. デコードされたデータを処理する

   * コンストラクターを呼び出し、保護されたPDFドキュメントのファイルの場所を表す文字列値を渡して、`System.IO.FileStream`オブジェクトを作成します。
   * `encryptPDFUsingPassword`メソッドで返された`BLOB`オブジェクトのデータ内容を格納するバイト配列を作成します。 `BLOB`オブジェクトの`binaryData`データメンバーの値を取得して、バイト配列を設定します。
   * コンストラクターを呼び出し、`System.IO.FileStream`オブジェクトを渡して、`System.IO.BinaryWriter`オブジェクトを作成します。
   * `System.IO.BinaryWriter`オブジェクトの`Write`メソッドを呼び出し、バイト配列を渡すことにより、バイト配列の内容をPDFファイルに書き込みます。

**関連トピック**

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
