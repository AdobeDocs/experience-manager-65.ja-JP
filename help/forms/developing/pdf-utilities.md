---
title: PDFユーティリティの操作
seo-title: PDFユーティリティの操作
description: PDF Utilitiesサービスを使用して、PDFファイル形式とXDPファイル形式の変換、PDFドキュメントプロパティの設定と取得、XMPメタデータの操作を行います。
seo-description: PDF Utilitiesサービスを使用して、PDFファイル形式とXDPファイル形式の変換、PDFドキュメントプロパティの設定と取得、XMPメタデータの操作を行います。
uuid: a2ea2359-c547-4f1b-b6ca-f276f816e36a
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d816bf2e-5236-4084-b7c4-c32b72cdff97
role: Developer
exl-id: e4b204ee-7261-42b8-8db8-a92aa9fd0a28
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2606'
ht-degree: 5%

---

# PDFユーティリティの操作{#working-with-pdf-utilities}

**このドキュメントのサンプルと例は、JEE上のAEM Forms環境に限られています。**

**PDF Utilitiesサービスについて**

PDF Utilitiesサービスは、PDFファイル形式とXDPファイル形式の変換、PDFドキュメントプロパティの設定と取得、XMPメタデータの操作をおこなえます。 例えば、PDFドキュメントを別の形式に変換する前に、プロパティを調べて、変換用に呼び出すサービス操作を判断すると便利です。

PDF Utilitiesサービスを使用して、次のタスクを実行できます。

* PDFドキュメントをXDPドキュメントに変換します。
* XDPドキュメントをPDFドキュメントに変換します。 （[XDPドキュメントのPDFドキュメントへの変換](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)を参照）。
* PDFドキュメントのプロパティを取得します。 （[PDFドキュメントのプロパティの取得](pdf-utilities.md#retrieving-pdf-document-properties)を参照）。
* PDFドキュメントを保存し、Web表示用に最適化します。 （[PDFドキュメントの保存モードの設定](pdf-utilities.md#setting-pdf-document-save-modes)を参照）。

>[!NOTE]
>
>PDF Utilitiesサービスについて詳しくは、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

## PDFドキュメントのXDPドキュメントへの変換{#converting-pdf-documents-into-xdp-documents}

PDF Utilities JavaおよびWebサービスAPIを使用して、PDFドキュメントをプログラムでXDPドキュメントに変換できます。

>[!NOTE]
>
>PDF Utilitiesサービスについて詳しくは、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順の概要{#summary-of-steps}

PDFドキュメントをXDPドキュメントに変換するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. PDFUtilityServiceクライアントを作成します。
1. 「PDF to XDP conversion」操作を呼び出します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用する場合は、プロキシファイルを必ず含めてください。

**PDFUtilityServiceクライアントの作成**

プログラムでPDF Utilities操作を実行する前に、PDFUtilityServiceクライアントを作成する必要があります。 Java APIを使用すると、`PDFUtilityServiceClient`オブジェクトを作成することでこれを実現できます。 WebサービスAPIでは、`PDFUtilityServiceService`オブジェクトを使用してこれを実行します。

**「PDF to XDP conversion」操作を呼び出す**

サービスクライアントを作成した後で、PDFからXDPへの変換操作を呼び出すことができます。

**関連トピック**

[Java APIを使用したPDFドキュメントのXDPドキュメントへの変換](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[WebサービスAPIを使用したPDFドキュメントのXDPドキュメントへの変換](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API {#convert-pdf-documents-into-xdp-documents-using-the-java-api}を使用してPDFドキュメントをXDPドキュメントに変換します

PDF Utilities API(Java)を使用してPDFドキュメントをXDPドキュメントに変換します。

1. プロジェクトファイルを含める

   adobe-pdfutility-client.jarなどのクライアントJARファイルをJavaプロジェクトのクラスパスに含めます。

1. PDFUtilityServiceクライアントの作成

   コンストラクターを使用し、接続プロパティを含む`ServiceClientFactory`オブジェクトを渡して、`PDFUtilityServiceClient`オブジェクトを作成します。

1. 「PDF to XDP conversion」操作を呼び出す

   変換を実行するには、`PDFUtilityServiceClient`オブジェクトの`convertPDFtoXDP`メソッドを呼び出して、PDFファイルを表す`com.adobe.idp.Document`オブジェクトを渡します。 このメソッドは、新しく作成されたXDPファイルを表す`com.adobe.idp.Document`オブジェクトを返します。

**関連トピック**

[PDFドキュメントからXDPドキュメントへの変換](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#convert-pdf-documents-into-xdp-documents-using-the-web-service-api}を使用してPDFドキュメントをXDPドキュメントに変換します

PDF Utilities API（Webサービス）を使用してPDFドキュメントをXDPドキュメントに変換します。

1. プロジェクトファイルを含める

   * PDF UtilitiesサービスのWSDLファイルを使用するMicrosoft .NETクライアントアセンブリを作成します。
   * Microsoft .NETクライアントアセンブリを参照します。

1. PDFUtilityServiceクライアントの作成

   プロキシクラスのコンストラクターを使用して`PDFUtilityServiceService`オブジェクトを作成します。

1. 「PDF to XDP conversion」操作を呼び出す

   `PDFUtilityServiceService`オブジェクトの`convertPDFtoXDP`メソッドを呼び出して、PDFファイルを表す`BLOB`オブジェクトを渡します。 このメソッドは、新しく作成されたXDPファイルを表す`BLOB`オブジェクトを返します。

**関連トピック**

[PDFドキュメントからXDPドキュメントへの変換](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64エンコーディングを使用する.NETクライアントアセンブリの作成](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## XDPドキュメントのPDFドキュメントへの変換{#converting-xdp-documents-into-pdf-documents}

PDF Utilities JavaおよびWebサービスAPIを使用して、XDPドキュメントをプログラムでPDFドキュメントに変換できます。

>[!NOTE]
>
>PDF Utilitiesサービスについて詳しくは、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順の概要{#summary_of_steps-1}

XDPドキュメントをPDFドキュメントに変換するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. PDFUtilityServiceクライアントを作成します。
1. 「XDP to PDF conversion」操作を呼び出します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用する場合は、プロキシファイルを必ず含めてください。

**PDFUtilityServiceクライアントの作成**

プログラムでPDF Utilities操作を実行する前に、PDFUtilityServiceクライアントを作成する必要があります。 Java APIを使用すると、`PDFUtilityServiceClient`オブジェクトを作成することでこれを実現できます。 WebサービスAPIでは、`PDFUtilityServiceService`オブジェクトを使用してこれを実行します。

**「XDP to PDF conversion」操作を呼び出す**

サービスクライアントを作成した後で、XDPからPDFへの変換操作を呼び出すことができます。

**関連トピック**

[Java APIを使用したXDPドキュメントのPDFドキュメントへの変換](pdf-utilities.md#convert-xdp-documents-into-pdf-documents-using-the-java-api)

[WebサービスAPIを使用したXDPドキュメントのPDFドキュメントへの変換](pdf-utilities.md#converting-xdp-documents-into-pdf-documents-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java APIを使用してXDPドキュメントをPDFドキュメントに変換します。 {#convert-xdp-documents-into-pdf-documents-using-the-java-api}

PDF Utilities API(Java)を使用してXDPドキュメントをPDFドキュメントに変換します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-pdfutility-client.jarなどのクライアントJARファイルを含めます。

1. PDFUtilityServiceクライアントの作成

   コンストラクターを使用し、接続プロパティを含む`ServiceClientFactory`オブジェクトを渡して、`PDFUtilityServiceClient`オブジェクトを作成します。

1. 「XDP to PDF conversion」操作を呼び出す

   変換を実行するには、`PDFUtilityServiceClient`オブジェクトの`convertXDPtoPDF`メソッドを呼び出して、XDPファイルを表す`com.adobe.idp.Document`オブジェクトを渡します。 このメソッドは、新しく作成されたPDFファイルを表す`com.adobe.idp.Document`オブジェクトを返します。

**関連トピック**

[XDPドキュメントからPDFドキュメントへの変換](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#converting-xdp-documents-into-pdf-documents-using-the-web-service-api}を使用したXDPドキュメントのPDFドキュメントへの変換

PDF Utilities API（WebサービスAPI）を使用してXDPドキュメントをPDFドキュメントに変換します。

1. プロジェクトファイルを含める

   * PDF UtilitiesサービスのWSDLファイルを使用するMicrosoft .NETクライアントアセンブリを作成します。
   * Microsoft .NETクライアントアセンブリを参照します。

1. PDFUtilityServiceクライアントの作成

   プロキシクラスのコンストラクターを使用して`PDFUtilityServiceService`オブジェクトを作成します。

1. 「XDP to PDF conversion」操作を呼び出す

   変換を実行するには、`PDFUtilityServiceService`オブジェクトの`convertXDPtoPDF`メソッドを呼び出して、XDPファイルを表す`BLOB`オブジェクトを渡します。 このメソッドは、新しく作成されたPDFファイルを表す`BLOB`オブジェクトを返します。

**関連トピック**

[XDPドキュメントからPDFドキュメントへの変換](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64エンコーディングを使用する.NETクライアントアセンブリの作成](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## PDFドキュメントのプロパティ{#retrieving-pdf-document-properties}の取得

PDF Utilities JavaおよびWebサービスAPIを使用して、ドキュメントが入力可能なフォームであるか、ドキュメントを読むのに最低限必要なAcrobatバージョンであるかなど、PDFドキュメントのプロパティをプログラムで取得できます。

>[!NOTE]
>
>PDF Utilitiesサービスについて詳しくは、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順の概要{#summary_of_steps-2}

PDFドキュメントのプロパティを取得するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. PDFUtilityServiceクライアントを作成します。
1. プロパティ取得操作を呼び出します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用する場合は、プロキシファイルを必ず含めてください。

**PDFUtilityServiceクライアントの作成**

プログラムでPDF Utilities操作を実行する前に、PDFUtilityServiceクライアントを作成する必要があります。 Java APIを使用すると、`PDFUtilityServiceClient`オブジェクトを作成することでこれを実現できます。 WebサービスAPIでは、`PDFUtilityServiceService`オブジェクトを使用してこれを実行します。

**「Properties」取得操作を呼び出す**

サービスクライアントを作成した後で、プロパティ取得操作を呼び出すことができます。

**関連トピック**

[Java APIを使用したPDFドキュメントのプロパティの取得](pdf-utilities.md#retrieve-pdf-document-properties-using-the-java-api)

[WebサービスAPIを使用したPDFドキュメントプロパティの取得](pdf-utilities.md#retrieve-pdf-document-properties-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API {#retrieve-pdf-document-properties-using-the-java-api}を使用してPDFドキュメントのプロパティを取得します

PDF Utilities API(Java)を使用してPDFドキュメントのプロパティを取得します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-pdfutility-client.jarなどのクライアントJARファイルを含めます。

1. PDFUtilityServiceクライアントの作成

   コンストラクターを使用し、接続プロパティを含む`ServiceClientFactory`オブジェクトを渡して、`PDFUtilityServiceClient`オブジェクトを作成します。

1. 「Properties」取得操作を呼び出す

   変換を実行するには、`PDFUtilityServiceClient`オブジェクトの`getPDFProperties`メソッドを呼び出して、次のように渡します。

   * PDFドキュメントを表す`com.adobe.idp.Document`オブジェクト。
   * 評価するプロパティを含む`PDFPropertiesOptionSpec`オブジェクト。

   メソッドは、クエリの結果を含む`PDFPropertiesResult`オブジェクトを返します。

**関連トピック**

[PDFドキュメントのプロパティの取得](pdf-utilities.md#retrieving-pdf-document-properties)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#retrieve-pdf-document-properties-using-the-web-service-api}を使用してPDFドキュメントのプロパティを取得します

PDF Utilities WebサービスAPIを使用してPDFドキュメントのプロパティを取得します。

1. プロジェクトファイルを含める

   * PDF UtilitiesサービスのWSDLファイルを使用するMicrosoft .NETクライアントアセンブリを作成します。
   * Microsoft .NETクライアントアセンブリを参照します。

1. PDFUtilityServiceクライアントの作成

   プロキシクラスのコンストラクターを使用して`PDFUtilityServiceService`オブジェクトを作成します。

1. 「Properties」取得操作を呼び出す

   変換を実行するには、`PDFUtilityServiceService`オブジェクトの`getPDFProperties`メソッドを呼び出して、次のように渡します。

   * PDFドキュメントを表す`BLOB`オブジェクト。
   * 評価するプロパティを含む`PDFPropertiesOptionSpec`オブジェクト。

   メソッドは、クエリの結果を含む`PDFPropertiesResult`オブジェクトを返します。

**関連トピック**

[PDFドキュメントのプロパティの取得](pdf-utilities.md#retrieving-pdf-document-properties)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64エンコーディングを使用する.NETクライアントアセンブリの作成](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## PDFドキュメントの保存モードの設定{#setting-pdf-document-save-modes}

PDF UtilitiesサービスのJavaおよびWebサービスAPIを使用して、PDFドキュメントの保存モードをプログラムで設定できます。 PDF Utilitiesサービスを使用して保存モードを設定する場合、PDF Utilitiesサービスは保存モードのみを設定し、実際にはPDFドキュメントを保存しません。 PDFドキュメントは、別のサービス操作に渡される際に保存されます。 例えば、PDF Utilitiesサービスを使用して特定の保存モードを設定し、Encryptionサービスに渡すことができます。Encryptionサービスでは、PDFドキュメントが実際に保存および暗号化されます。

>[!NOTE]
>
>PDF Utilitiesサービスについて詳しくは、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順の概要{#summary_of_steps-3}

PDFドキュメントの保存オプションを設定するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. PDFUtilityServiceクライアントを作成します。
1. 保存モードを設定します。
1. 保存操作を呼び出します。
1. PDFドキュメントを別の操作に渡します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用する場合は、プロキシファイルを必ず含めてください。

**PDFUtilityServiceクライアントの作成**

プログラムでPDF Utilities操作を実行する前に、PDFUtilityServiceクライアントを作成する必要があります。 Java APIを使用すると、`PDFUtilityServiceClient`オブジェクトを作成することでこれを実現できます。 WebサービスAPIでは、`PDFUtilityServiceService`オブジェクトを使用してこれを実行します。

**保存モードの設定**

次の保存オプションのいずれかを選択できます。

* `INCREMENTAL`:増分的に保存し、保存に要する時間を短縮する
* `FAST_WEB_VIEW`:Web表示用に保存
* `FULL`:完全保存を使用して（最適化を行わずに）保存するには

**「save style」操作を呼び出す**

サービスクライアントを作成した後で、プロパティ取得操作を呼び出すことができます。

**PDFドキュメントを別のAEM Forms操作に渡す**

PDF Utilitiesサービスが指定した保存モードを設定したら、PDFドキュメントを別のAEM Forms操作に渡します。 この操作から戻ると、PDFドキュメントは指定されたモードで保存されます。 例えば、PDF Utilitiesサービスを使用して`FAST_WEB_VIEW`モードを設定し、そのPDFドキュメントをEncryptionサービスの`encryptUsingPassword`操作に渡す場合、返されるPDFドキュメントはパスワードで暗号化され、`FAST_WEB_VIEW`モードで保存されます。

>[!NOTE]
>
>このセクションに関連付けられているクイックスタートは、`FAST_WEB_VIEW`モードを設定し、PDFドキュメントをEncryptionサービスの`encryptUsingPassword`操作に渡します。

**関連トピック**

[Java APIを使用したPDFドキュメントの保存オプションの設定](pdf-utilities.md#set-pdf-document-save-options-using-the-java-api)

[WebサービスAPIを使用したPDFドキュメントの保存オプションの設定](pdf-utilities.md#set-pdf-document-save-options-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDFドキュメントのパスワードによる暗号化](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Java API {#set-pdf-document-save-options-using-the-java-api}を使用してPDFドキュメントの保存オプションを設定します

PDF Utilities API(Java)を使用してPDFドキュメントの保存オプションを設定します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-pdfutility-client.jarなどのクライアントJARファイルを含めます。

1. PDFUtilityServiceクライアントの作成

   コンストラクターを使用し、接続プロパティを含む`ServiceClientFactory`オブジェクトを渡して、`PDFUtilityServiceClient`オブジェクトを作成します。

1. 保存モードの設定

   * コンストラクタを使用して `PDFUtilitySaveMode` オブジェクトを作成します。
   * `PDFUtilitySaveMode`オブジェクトの`setSaveStyle`メソッドを呼び出し、保存モードを指定する文字列値を渡すことで、保存モードを設定します。 例えば、Web表示用に保存するには、`FAST_WEB_VIEW`を渡します。

1. 「save style」操作を呼び出す

   `PDFUtilityServiceClient`オブジェクトの`setSaveMode`メソッドを呼び出し、次の値を渡します。

   * PDFドキュメントを表す`com.adobe.idp.Document`オブジェクト。
   * 使用する保存スタイルを含む`PDFUtilitySaveMode`オブジェクト。
   * 以前の設定を上書きするかどうかを決定するために使用されるBoolean値。

   このメソッドは、指定した保存スタイルを使用して書式設定された`com.adobe.idp.Document`オブジェクトを返します。

1. PDFドキュメントを別のAEM Forms操作に渡す

   * 返された`com.adobe.idp.Document`オブジェクトを別のAEM Forms操作に渡します。

**関連トピック**

[PDFドキュメントの保存モードの設定](pdf-utilities.md#setting-pdf-document-save-modes)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#set-pdf-document-save-options-using-the-web-service-api}を使用してPDFドキュメントの保存オプションを設定します

PDF Utilities AP（Webサービス）を使用して、PDFドキュメントの保存オプションを設定します。

1. プロジェクトファイルを含める

   * PDF UtilitiesサービスのWSDLファイルを使用するMicrosoft .NETクライアントアセンブリを作成します。
   * Microsoft .NETクライアントアセンブリを参照します。

1. PDFUtilityServiceクライアントの作成

   プロキシクラスのコンストラクターを使用して`PDFUtilityServiceService`オブジェクトを作成します。

1. 保存モードの設定

   * コンストラクタを使用して `PDFUtilitySaveMode` オブジェクトを作成します。
   * 保存モードを指定する`PDFUtilitySaveMode`オブジェクトの`saveStyle`メソッドに文字列値を割り当てて、保存モードを設定します。 例えば、Webを高速に表示するために保存するには、`FAST_WEB_VIEW`と指定します。

1. 「save style」操作を呼び出す

   `PDFUtilityServiceService`オブジェクトの`setSaveMode`メソッドを呼び出し、次の値を渡します。

   * PDFドキュメントを表す`BLOB`オブジェクト。
   * 使用する保存スタイルを含む`PDFUtilitySaveMode`オブジェクト。
   * 以前の設定を上書きするかどうかを決定するために使用されるBoolean値。

   このメソッドは、指定した保存スタイルを使用して書式設定された`BLOB`オブジェクトを返します。 そのオブジェクトをPDFドキュメントとして保存できます。

1. PDFドキュメントを別のForms操作に渡す

   * 返された`BLOB`オブジェクトを別のAEM Forms操作に渡します。

**関連トピック**

[PDFドキュメントの保存モードの設定](pdf-utilities.md#setting-pdf-document-save-modes)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64エンコーディングを使用する.NETクライアントアセンブリの作成](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## PDFドキュメントの不要部分の削除{#sanitizing-pdf-documents}

PDF Utilities Java APIを使用して、PDFドキュメントをプログラムでXDPドキュメントに変換できます。

>[!NOTE]
>
>PDF Utilitiesサービスについて詳しくは、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順の概要{#summary_of_steps-4}

PDFドキュメントの不要部分を削除するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. PDFUtilityServiceクライアントを作成します。
1. サニタイズ操作を呼び出します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成するには、必要なJARファイルを含めます。

**PDFUtilityServiceクライアントの作成**

プログラムによって削除操作を実行する前に、PDFUtilityServiceクライアントを作成する必要があります。 Java APIを使用すると、`PDFUtilityServiceClient`オブジェクトを作成することでこれを実現できます。

**「PDF to XDP conversion」操作を呼び出す**

サービスクライアントを作成した後で、サニタイズ化操作を呼び出すことができます。

**関連トピック**

[Java APIを使用したPDFドキュメントのXDPドキュメントへの変換](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[WebサービスAPIを使用したPDFドキュメントのXDPドキュメントへの変換](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API {#sanitize-pdf-documents-using-the-java-api}を使用して、PDFドキュメントを不要部分にします。

PDF Utilities API(Java)を使用してドキュメントの不要部分を削除します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-pdfutility-client.jarなどのクライアントJARファイルを含めます。

1. PDFUtilityServiceクライアントの作成

   コンストラクターを使用し、接続プロパティを含む`ServiceClientFactory`オブジェクトを渡して、`PDFUtilityServiceClient`オブジェクトを作成します。

1. 「PDF to XDP conversion」操作を呼び出す

   変換を実行するには、`PDFUtilityServiceClient`オブジェクトの`convertPDFtoXDP`メソッドを呼び出して、PDFファイルを表す`com.adobe.idp.Document`オブジェクトを渡します。 このメソッドは、新しく作成されたXDPファイルを表す`com.adobe.idp.Document`オブジェクトを返します。

**関連トピック**

[PDFドキュメントの不要部分の削除](/help/forms/developing/pdf-utilities-service-java-api.md#quick-start-soap-mode-sanitizing-pdf-documents)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
