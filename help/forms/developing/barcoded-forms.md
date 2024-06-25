---
title: Barcoded Forms の操作
description: Java API および web サービス API を使用して、PDF フォームまたはバーコードを含む画像からデータをデコードします。
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: dd32808e-b773-48a2-90e1-7a277d349493
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations,Barcoded Forms
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1911'
ht-degree: 100%

---

# Barcoded Forms の操作 {#working-with-barcoded-forms}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

## Barcoded Forms サービスについて {#about-the-barcoded-forms-service}

Barcoded Forms サービスは、印刷および記入用フォームからのデータのキャプチャを自動化し、取り込んだ情報を組織の主要な IT システムに統合します。

Barcoded Forms サービスを使用すると、1 次元および 2 次元のバーコードをインタラクティブ PDF forms に追加できます。その後、Barcoded Forms を web サイトに公開したり、メールまたは CD で配布したりできます。ユーザーが Adobe Reader、Acrobat Professional またはAcrobat Standard でバーコードフォームに入力すると、バーコードが自動的に更新され、フォームデータがエンコードされます。ユーザーは、フォームをメールで送ったり、紙に印刷して、郵送や FAX で送信したり、直接配布したりできます。後で、自動化されたワークフローの一部として、ユーザーが指定したデータを抽出し、承認プロセスやビジネスシステム間でデータをルーティングできます。

Barcoded Forms サービスについて詳しくは、[AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

## バーコードフォームデータのデコード {#decoding-barcoded-form-data}

Barcoded Forms API を使用して、バーコードを含む PDF フォームまたは画像からデータをデコードできます。フォームデータのデコードとは、バーコード内のデータを抽出することを意味します。データを PDF フォーム（または画像）からデコードする前に、フォームにはデータが入力されている必要があります。

>[!NOTE]
>
>Barcoded Forms サービスについて詳しくは、[AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary-of-steps}

データを PDF フォームからデコードするには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Barcoded FormsClient API オブジェクトを作成します。
1. バーコードデータを含む PDF フォームを取得します。
1. データを PDF フォームからデコードします。
1. データを XML データソースに変換します。
1. デコードされたデータを処理します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めるようにします。

次の JAR ファイルをプロジェクトのクラスパスに追加する必要があります。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-barcodedforms-client.jar
* adobe-utilities.jar（AEM Forms を JBoss にデプロイする場合に必要）
* jbossall-client.jar（AEM Forms が JBoss にデプロイされている場合に必要）
* xercesImpl.jar（&lt;install directory=&quot;&quot;>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs\thirdparty）

AEM Forms が、JBOSS 以外のサポート対象の J2EE アプリケーションサーバー上にデプロイされている場合は、adobe-utilities.jar と jbossall-client.jar を、AEM Forms がデプロイされている J2EE アプリケーションサーバー固有の JAR ファイルに置き換える必要があります。すべての AEM Forms JAR ファイルの場所については、[AEM Forms Java ライブラリファイルの組み込み](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。

**Barcoded Forms Client API オブジェクトの作成**

プログラムによる Barcoded Forms サービスの操作を実行する前に、Barcoded Forms サービスクライアントを作成する必要があります。Java API を使用している場合は、`BarcodedFormsServiceClient` オブジェクトを作成します。Barcoded Forms web サービス API を使用している場合は、`BarcodedFormsServiceService` オブジェクトを作成します。

**バーコードデータを含む PDF フォームの取得**

ユーザーデータが入力されたバーコードを含む PDF フォームを取得します。

**データを PDF フォームからデコード**

バーコードを含む PDF フォーム（または画像）を取得したら、データをデコードできます。Barcoded Forms サービスは、次の種類のバーコードをサポートしています。

* PDF417 バーコード。
* データマトリックスバーコード。
* QR コードのバーコード。
* Codabar バーコード。
* Code 128 バーコード。
* Code 39 バーコード。
* EAN-13 バーコード。
* EAN-8 バーコード。

デコード API で 16 進数の文字セットを入力した場合は、バーコードの内容が 16 進文字列としてエンコードされます。例えば、フォームで文字エンコーディングに UTF-8 を指定し、デコード操作で 16 進数を指定した場合、バーコードの内容はデコードされた出力の &lt; `xb:content`> 要素で 16 進文字列としてエンコードされます。この 16 進数値を変換して元のコンテンツを取得するには、クライアントアプリケーションでアプリケーションロジックを作成します。

**データを XML データソースに変換**

フォームデータをデコードした後、XDP または XFDF データに変換できます。例えば、別のフォームにデータを読み込むとします。データを XFA フォームに読み込むには、そのデータを XDP データに変換する必要があります。詳しくは、[フォームデータの読み込み](/help/forms/developing/importing-exporting-data.md#importing-form-data)を参照してください。

**デコードされたデータを処理**

変換後のデータを処理して、ビジネス要件を満たすことができます。例えば、データをデコードして変換した後に、ファイルに保存し、エンタープライズデータベースに格納し、別のフォームに入力することができます。この節では、変換後のデータを XML ファイルとして保存する方法について説明します。

>[!NOTE]
>
>行区切りパラメーターとフィールド区切りパラメーターの値が同じ場合、Barcoded Forms サービスはバーコードデータをデコードできません

**関連トピック**

[Java API を使用したバーコードフォームデータのデコード](barcoded-forms.md#decode-barcoded-form-data-using-the-java-api)

[Web サービス API を使用したバーコードフォームデータのデコード](barcoded-forms.md#decode-barcoded-form-data-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API を使用したバーコードフォームデータのデコード {#decode-barcoded-form-data-using-the-java-api}

Barcoded Forms API（Java）を使用してフォームデータをデコードします。

1. プロジェクトファイルを含める

   クライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. Barcoded Forms クライアント API オブジェクトの作成

   コンストラクターを使用し、接続プロパティを含む `ServiceClientFactory` オブジェクトを渡すことにより、`BarcodedFormsServiceClient` オブジェクトを作成します。

1. バーコードデータを含む PDF フォームを取得する

   * コンストラクターを使用し、PDF ドキュメントの場所を指定する文字列値を渡すことにより、バーコードデータを含む PDF フォームを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. データを PDF フォームからデコード

   `BarcodedFormsServiceClient` オブジェクトの `decode` メソッドを呼び出し、次の値を渡すことにより、フォームデータをデコードします。

   * PDF フォームを含む `com.adobe.idp.Document` オブジェクト。
   * PDF417 バーコードをデコードするかどうかを指定する `java.lang.Boolean` オブジェクト。
   * データマトリックスバーコードをデコードするかどうかを指定する `java.lang.Boolean` オブジェクト。
   * QR コードバーコードをデコードするかどうかを指定する `java.lang.Boolean` オブジェクト。
   * codabar バーコードをデコードするかどうかを指定する `java.lang.Boolean` オブジェクト。
   * コード 128 バーコードをデコードするかどうかを指定する `java.lang.Boolean` オブジェクト。
   * コード 39 バーコードをデコードするかどうかを指定する `java.lang.Boolean` オブジェクト。
   * EAN-13 バーコードをデコードするかどうかを指定する `java.lang.Boolean` オブジェクト。
   * EAN-8 バーコードをデコードするかどうかを指定する `java.lang.Boolean` オブジェクト。
   * バーコードで使用される文字セットのエンコード値を指定する `com.adobe.livecycle.barcodedforms.CharSet` 定義済みリスト値。

   `decode` メソッドは、デコードされたフォームデータを含む `org.w3c.dom.Document` オブジェクトを返します。

1. データを XML データソースに変換する

   `BarcodedFormsServiceClient` オブジェクトの `extractToXML` メソッドを呼び出し、次の値を渡すことにより、デコードされたデータを XDP または XFDF データに変換します。

   * デコードされたデータを含む `org.w3c.dom.Document` オブジェクト（`decode` メソッドの戻り値を使用していることを確認してください）。
   * 行の区切りを指定する `com.adobe.livecycle.barcodedforms.Delimiter` 定義済みリスト値。`Delimiter.Carriage_Return` を指定することをお勧めします。
   * フィールド区切りを指定する `com.adobe.livecycle.barcodedforms.Delimiter` 定義済みリスト値。例えば、`Delimiter.Tab` を指定します。
   * バーコードデータを XDP または XFDF XML データに変換するかどうかを指定する `com.adobe.livecycle.barcodedforms.XMLFormat` 定義済みリスト値。例えば、データを XDP データに変換するには `XMLFormat.XDP` を指定します。

   >[!NOTE]
   >
   >行区切りパラメーターとフィールド区切りパラメーターに同じ値を指定しないでください。

   `extractToXML` メソッドは、各要素が `org.w3c.dom.Document` オブジェクトである `java.util.List` オブジェクトを返します。フォーム上のバーコードごとに別々の要素があります。つまり、フォームに 4 つのバーコードがある場合、返された `java.util.List` オブジェクトには 4 つの要素が含まれます。

1. デコードされたデータを処理

   * `java.util.List` オブジェクトを反復処理して、リストにある各 `org.w3c.dom.Document` オブジェクトを取得します。
   * リストの各要素に対して、 `org.w3c.dom.Document` オブジェクトを `com.adobe.idp.Document` オブジェクトに変換します（`org.w3c.dom.Document` オブジェクトを `com.adobe.idp.Document` オブジェクトに変換するアプリケーションロジックは、「Java API を使用したバーコード化されたフォームデータのデコード」の例で示しています）。
   * `com.adobe.idp.Document` オブジェクトの `copyToFile` を呼び出し、XML ファイルを表す File オブジェクトを渡すことにより、XML データを XML ファイルとして保存します。

**関連トピック**

[クイックスタート（SOAP モード）：Java API を使用してバーコードフォームデータをデコード](/help/forms/developing/barcoded-forms-service-java-api.md#quick-start-soap-mode-decoding-barcoded-form-data-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用したバーコードフォームデータのデコード {#decode-barcoded-form-data-using-the-web-service-api}

Barcoded Forms API（web サービス）を使用したフォームデータのデコード：

1. プロジェクトファイルを含める

   * Barcoded Forms サービス WSDL を使用する Microsoft .NET クライアントアセンブリを作成します。詳しくは、 [Base64 エンコーディングを使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)を参照してください。
   * Microsoft .NET クライアントアセンブリを参照します詳しくは、[Base64 エンコーディングを使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)の「.NET クライアントアセンブリの参照」を参照してください。

1. Barcoded Forms クライアント API オブジェクトの作成

   Barcoded Forms サービス WSDL を使用する Microsoft .NET クライアントアセンブリを使用して、デフォルトのコンストラクターを呼び出し、 `BarcodedFormsServiceService` オブジェクトを作成します。

1. バーコードデータを含む PDF フォームを取得する

   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB` オブジェクトは、バーコードを含む PDF ドキュメントを保存するために使用されます。
   * コンストラクターを呼び出し、PDF ドキュメントのファイルの場所とファイルを開くモードを表す文字列値を渡して、`System.IO.FileStream` オブジェクトを作成します。
   * `System.IO.FileStream` オブジェクトのコンテンツを保存するバイト配列を作成します。 バイト配列のサイズは、`System.IO.FileStream` オブジェクトの `Length` プロパティを取得することで決定できます。
   * バイト配列にストリームデータを入力するには、`System.IO.FileStream` オブジェクトの `Read` メソッドを呼び出し、バイト配列、開始位置、読み取るストリーム長を渡します。
   * `binaryData` プロパティにバイト配列の内容を割り当てて、`BLOB` オブジェクトを入力します。

1. データを PDF フォームからデコード

   `BarcodedFormsServiceService` オブジェクトの `decode` メソッドを呼び出し、次の値を渡すことにより、フォームデータをデコードします。

   * PDF フォームを含む `BLOB` オブジェクト。
   * PDF417 バーコードをデコードするかどうかを指定する `Boolean` オブジェクト。
   * データマトリックスバーコードをデコードするかどうかを指定する `Boolean` オブジェクト。
   * QR コードバーコードをデコードするかどうかを指定する `Boolean` オブジェクト。
   * codabar バーコードをデコードするかどうかを指定する `Boolean` オブジェクト。
   * コード 128 バーコードをデコードするかどうかを指定する `Boolean` オブジェクト。
   * コード 39 バーコードをデコードするかどうかを指定する `Bolean` オブジェクト。
   * EAN-13 バーコードをデコードするかどうかを指定する `Boolean` オブジェクト。
   * EAN-8 バーコードをデコードするかどうかを指定する `Boolean` オブジェクト。
   * バーコードで使用されている文字セットのエンコーディング値を指定する `CharSet` 列挙値

   この `decode` メソッドは、デコードされたフォームデータを含む文字列値を返します。

1. データを XML データソースに変換する

   `BarcodedFormsServiceService` オブジェクトの `extractToXML` メソッドを呼び出し、次の値を渡して、デコードされたデータを XDP データまたは XFDF データに変換します。

   * デコードされたデータを含む文字列値（`decode` メソッドの戻り値を使用していることを確認します）
   * 行の区切りを指定する `Delimiter` 定義済みリスト値。`Delimiter.Carriage_Return` を指定することをお勧めします。
   * フィールド区切りを指定する `Delimiter` 定義済みリスト値。例えば、`Delimiter.Tab` を指定します。
   * バーコードデータを XDP または XFDF XML データに変換するかどうかを指定する `XMLFormat` 定義済みリスト値。例えば、データを XDP データに変換するには `XMLFormat.XDP` を指定します。

   >[!NOTE]
   >
   >行区切りパラメーターとフィールド区切りパラメーターに同じ値を指定しないでください。

   `extractToXML` メソッドは、 各要素が `BLOB` インスタンスである `Object` 配列を返します。フォーム上のバーコードごとに別々の要素があります。つまり、フォームに 4 つのバーコードがある場合、返される `Object` 配列には 4 つの要素が含まれます。

1. デコードされたデータを処理

   * コンストラクターを呼び出し、保護された PDF ドキュメントのファイルの場所を表す文字列の値を渡して、`System.IO.FileStream` オブジェクトを作成します。
   * `encryptPDFUsingPassword` メソッドが返した `BLOB` オブジェクトのデータコンテンツを格納するバイト配列を作成します。`BLOB` オブジェクトの `binaryData` データメンバーの値を取得して、バイト配列にデータを入力します。
   * コンストラクターを呼び出して `System.IO.FileStream` オブジェクトを渡すことによって、`System.IO.BinaryWriter` オブジェクトを作成します。
   * `System.IO.BinaryWriter` オブジェクトの `Write` メソッドを呼び出してバイト配列を渡すことにより、バイト配列の内容を PDF ファイルに書き込みます。

**関連トピック**

[Base64 エンコーディングを使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
