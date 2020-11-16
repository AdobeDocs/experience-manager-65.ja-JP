---
title: PDF Utilitiesの操作
seo-title: PDF Utilitiesの操作
description: 'null'
seo-description: 'null'
uuid: a2ea2359-c547-4f1b-b6ca-f276f816e36a
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d816bf2e-5236-4084-b7c4-c32b72cdff97
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '2548'
ht-degree: 5%

---


# PDF Utilitiesの操作 {#working-with-pdf-utilities}

**PDF Utilitiesサービスについて**

PDF Utilitiesサービスでは、PDFファイル形式とXDPファイル形式間の変換、PDFドキュメントプロパティの設定と取得、XMPメタデータの操作を行うことができます。 例えば、PDFドキュメントを別の形式に変換する前に、プロパティを調べて、変換用に呼び出すサービス操作を決定しておくと便利です。

PDF Utilitiesサービスを使用して、次のタスクを実行できます。

* PDFドキュメントをXDPドキュメントに変換します。
* XDPドキュメントをPDFドキュメントに変換します。 (XDPドキュメントのPDFドキュメントへの [変換を参照](pdf-utilities.md#converting-xdp-documents-into-pdf-documents))。
* PDFドキュメントのプロパティを取得します。 (PDFドキュメントのプロパティ [の取得を参照](pdf-utilities.md#retrieving-pdf-document-properties))。
* PDFドキュメントを保存し、Web表示用に最適化します。 (PDFドキュメントの保存モードの [設定を参照](pdf-utilities.md#setting-pdf-document-save-modes))。

>[!NOTE]
>
>For more information about the PDF Utilities service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## PDFドキュメントのXDPドキュメントへの変換 {#converting-pdf-documents-into-xdp-documents}

PDF UtilitiesのJavaおよびWebサービスAPIを使用して、PDFドキュメントをプログラム的にXDPドキュメントに変換できます。

>[!NOTE]
>
>For more information about the PDF Utilities service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary-of-steps}

PDFドキュメントをXDPドキュメントに変換するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. PDFUtilityServiceクライアントを作成します。
1. PDFからXDPへの変換操作を呼び出します

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めてください。

**PDFUtilityServiceクライアントの作成**

プログラムを使用してPDF Utilities操作を実行する前に、PDFUtilityServiceクライアントを作成する必要があります。 Java APIを使用して、これは `PDFUtilityServiceClient` オブジェクトを作成することで実現します。 WebサービスAPIでは、これは `PDFUtilityServiceService` オブジェクトを使用して実行されます。

**PDFからXDPへの変換操作の呼び出し**

サービスクライアントを作成したら、PDFからXDPへの変換操作を呼び出すことができます。

**関連トピック**

[Java APIを使用したPDFドキュメントのXDPドキュメントへの変換](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[WebサービスAPIを使用してPDFドキュメントをXDPドキュメントに変換する](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java APIを使用したPDFドキュメントのXDPドキュメントへの変換 {#convert-pdf-documents-into-xdp-documents-using-the-java-api}

PDF Utilities API(Java)を使用して、PDFドキュメントをXDPドキュメントに変換します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-pdfutility-client.jarなどのクライアントJARファイルを含めます。

1. PDFUtilityServiceクライアントの作成

   コンストラクタを使用し、接続プロパティを含むオブジェクトを渡して、 `PDFUtilityServiceClient``ServiceClientFactory` オブジェクトを作成します。

1. PDFからXDPへの変換操作の呼び出し

   変換を実行するには、 `PDFUtilityServiceClient` オブジェクトの `convertPDFtoXDP` メソッドを呼び出し、PDFファイルを表す `com.adobe.idp.Document` オブジェクトを渡します。 このメソッドは、新しく作成されたXDPファイルを表す `com.adobe.idp.Document` オブジェクトを返します。

**関連トピック**

[PDFドキュメントのXDPドキュメントへの変換](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用してPDFドキュメントをXDPドキュメントに変換する {#convert-pdf-documents-into-xdp-documents-using-the-web-service-api}

PDF Utilities API（Webサービス）を使用して、PDFドキュメントをXDPドキュメントに変換します。

1. プロジェクトファイルを含める

   * PDF UtilitiesサービスのWSDLファイルを使用するMicrosoft .NETクライアントアセンブリを作成します。
   * Microsoft .NETクライアントアセンブリを参照します。

1. PDFUtilityServiceクライアントの作成

   プロキシクラスのコンストラクターを使用して、 `PDFUtilityServiceService` オブジェクトを作成します。

1. PDFからXDPへの変換操作の呼び出し

   オブジェクトの `PDFUtilityServiceService` メソッドを呼び出し、PDFファイルを表す `convertPDFtoXDP``BLOB` オブジェクトを渡します。 このメソッドは、新しく作成されたXDPファイルを表す `BLOB` オブジェクトを返します。

**関連トピック**

[PDFドキュメントのXDPドキュメントへの変換](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64エンコーディングを使用する.NETクライアントアセンブリの作成](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## XDPドキュメントのPDFドキュメントへの変換 {#converting-xdp-documents-into-pdf-documents}

PDF UtilitiesのJavaおよびWebサービスAPIを使用して、XDPドキュメントをプログラム的にPDFドキュメントに変換できます。

>[!NOTE]
>
>For more information about the PDF Utilities service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-1}

XDPドキュメントをPDFドキュメントに変換するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. PDFUtilityServiceクライアントを作成します。
1. XDPからPDFへの変換操作を呼び出します

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めてください。

**PDFUtilityServiceクライアントの作成**

プログラムを使用してPDF Utilities操作を実行する前に、PDFUtilityServiceクライアントを作成する必要があります。 Java APIを使用して、これは `PDFUtilityServiceClient` オブジェクトを作成することで実現します。 WebサービスAPIでは、これは `PDFUtilityServiceService` オブジェクトを使用して実行されます。

**XDPからPDFへの変換操作の呼び出し**

サービスクライアントを作成したら、XDPからPDFへの変換操作を呼び出すことができます。

**関連トピック**

[Java APIを使用したXDPドキュメントのPDFドキュメントへの変換](pdf-utilities.md#convert-xdp-documents-into-pdf-documents-using-the-java-api)

[WebサービスAPIを使用したXDPドキュメントからPDFドキュメントへの変換](pdf-utilities.md#converting-xdp-documents-into-pdf-documents-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java APIを使用したXDPドキュメントのPDFドキュメントへの変換 {#convert-xdp-documents-into-pdf-documents-using-the-java-api}

PDF Utilities API(Java)を使用して、XDPドキュメントをPDFドキュメントに変換します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-pdfutility-client.jarなどのクライアントJARファイルを含めます。

1. PDFUtilityServiceクライアントの作成

   コンストラクタを使用し、接続プロパティを含むオブジェクトを渡して、 `PDFUtilityServiceClient``ServiceClientFactory` オブジェクトを作成します。

1. XDPからPDFへの変換操作の呼び出し

   変換を実行するには、 `PDFUtilityServiceClient` オブジェクトの `convertXDPtoPDF` メソッドを呼び出し、XDPファイルを表す `com.adobe.idp.Document` オブジェクトを渡します。 このメソッドは、新しく作成されたPDFファイルを表す `com.adobe.idp.Document` オブジェクトを返します。

**関連トピック**

[XDPドキュメントのPDFドキュメントへの変換](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したXDPドキュメントからPDFドキュメントへの変換 {#converting-xdp-documents-into-pdf-documents-using-the-web-service-api}

PDF Utilities API（WebサービスAPI）を使用して、XDPドキュメントをPDFドキュメントに変換します。

1. プロジェクトファイルを含める

   * PDF UtilitiesサービスのWSDLファイルを使用するMicrosoft .NETクライアントアセンブリを作成します。
   * Microsoft .NETクライアントアセンブリを参照します。

1. PDFUtilityServiceクライアントの作成

   プロキシクラスのコンストラクターを使用して、 `PDFUtilityServiceService` オブジェクトを作成します。

1. XDPからPDFへの変換操作の呼び出し

   変換を実行するには、 `PDFUtilityServiceService` オブジェクトの `convertXDPtoPDF` メソッドを呼び出し、XDPファイルを表す `BLOB` オブジェクトを渡します。 このメソッドは、新しく作成されたPDFファイルを表す `BLOB` オブジェクトを返します。

**関連トピック**

[XDPドキュメントのPDFドキュメントへの変換](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64エンコーディングを使用する.NETクライアントアセンブリの作成](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## PDFドキュメントのプロパティの取得 {#retrieving-pdf-document-properties}

PDF UtilitiesのJavaおよびWebサービスAPIを使用すると、ドキュメントを読み取るのに最低限必要なドキュメントが入力可能なフォームか、Acrobat版であるかなど、PDFドキュメントのプロパティをプログラムで取得できます。

>[!NOTE]
>
>For more information about the PDF Utilities service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)

### 手順の概要 {#summary_of_steps-2}

PDFドキュメントのプロパティを取得するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. PDFUtilityServiceクライアントを作成します。
1. プロパティ取得操作を呼び出します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めてください。

**PDFUtilityServiceクライアントの作成**

プログラムを使用してPDF Utilities操作を実行する前に、PDFUtilityServiceクライアントを作成する必要があります。 Java APIを使用して、これは `PDFUtilityServiceClient` オブジェクトを作成することで実現します。 WebサービスAPIでは、これは `PDFUtilityServiceService` オブジェクトを使用して実行されます。

**プロパティ取得操作を呼び出す**

サービスクライアントの作成後、プロパティ取得操作を呼び出すことができます。

**関連トピック**

[Java APIを使用したPDFドキュメントのプロパティの取得](pdf-utilities.md#retrieve-pdf-document-properties-using-the-java-api)

[WebサービスAPIを使用したPDFドキュメントのプロパティの取得](pdf-utilities.md#retrieve-pdf-document-properties-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java APIを使用したPDFドキュメントのプロパティの取得 {#retrieve-pdf-document-properties-using-the-java-api}

PDF Utilities API(Java)を使用してPDFドキュメントのプロパティを取得します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-pdfutility-client.jarなどのクライアントJARファイルを含めます。

1. PDFUtilityServiceクライアントの作成

   コンストラクタを使用し、接続プロパティを含むオブジェクトを渡して、 `PDFUtilityServiceClient``ServiceClientFactory` オブジェクトを作成します。

1. プロパティ取得操作を呼び出す

   変換を実行するには、 `PDFUtilityServiceClient` オブジェクトの `getPDFProperties` メソッドを呼び出し、次のように渡します。

   * A `com.adobe.idp.Document` object that represents the PDF document.
   * 評価対象のプロパティを含む `PDFPropertiesOptionSpec` オブジェクト。

   The method returns a `PDFPropertiesResult` object that contains the results of the query.

**関連トピック**

[PDFドキュメントのプロパティの取得](pdf-utilities.md#retrieving-pdf-document-properties)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したPDFドキュメントのプロパティの取得 {#retrieve-pdf-document-properties-using-the-web-service-api}

PDF Utilities WebサービスAPIを使用して、PDFドキュメントのプロパティを取得します。

1. プロジェクトファイルを含める

   * PDF UtilitiesサービスのWSDLファイルを使用するMicrosoft .NETクライアントアセンブリを作成します。
   * Microsoft .NETクライアントアセンブリを参照します。

1. PDFUtilityServiceクライアントの作成

   プロキシクラスのコンストラクターを使用して、 `PDFUtilityServiceService` オブジェクトを作成します。

1. プロパティ取得操作を呼び出す

   変換を実行するには、 `PDFUtilityServiceService` オブジェクトの `getPDFProperties` メソッドを呼び出し、次のように渡します。

   * A `BLOB` object that represents the PDF document.
   * 評価対象のプロパティを含む `PDFPropertiesOptionSpec` オブジェクト。

   The method returns a `PDFPropertiesResult` object that contains the results of the query.

**関連トピック**

[PDFドキュメントのプロパティの取得](pdf-utilities.md#retrieving-pdf-document-properties)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64エンコーディングを使用する.NETクライアントアセンブリの作成](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## PDFドキュメントの保存モードの設定 {#setting-pdf-document-save-modes}

PDFドキュメントの保存モードをプログラムで設定する場合は、PDF UtilitiesサービスのJavaおよびWebサービスのAPIを使用できます。 PDF Utilitiesサービスを使用して保存モードを設定する場合、PDF Utilitiesサービスは保存モードを設定するだけで、実際にはPDFドキュメントを保存しません。 PDFドキュメントは、別のサービス操作に渡されるときに保存されます。 例えば、PDF Utilitiesサービスを使用して特定の保存モードを設定し、それをEncryptionサービスに渡すことができます。Encryptionサービスでは、PDFドキュメントが実際に保存され、暗号化されます。

>[!NOTE]
>
>For more information about the PDF Utilities service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-3}

PDFドキュメントの保存オプションを設定するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. PDFUtilityServiceクライアントを作成します。
1. 保存モードを設定します。
1. 保存操作を呼び出します。
1. PDFドキュメントを別の操作に渡します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めてください。

**PDFUtilityServiceクライアントの作成**

プログラムを使用してPDF Utilities操作を実行する前に、PDFUtilityServiceクライアントを作成する必要があります。 Java APIを使用して、これは `PDFUtilityServiceClient` オブジェクトを作成することで実現します。 WebサービスAPIでは、これは `PDFUtilityServiceService` オブジェクトを使用して実行されます。

**保存モードの設定**

次の保存オプションのいずれかを選択できます。

* `INCREMENTAL`:増分的に保存し、保存に要する時間を短縮するには
* `FAST_WEB_VIEW`:Web表示用に保存
* `FULL`:フル保存を使用して（最適化なしで）保存するには

**「save style」操作を呼び出します**

サービスクライアントの作成後、プロパティ取得操作を呼び出すことができます。

**PDFドキュメントを別のAEM Forms操作に渡す**

PDF Utilitiesサービスで指定した保存モードが設定されたら、PDFドキュメントを別のAEM Forms操作に渡します。 その操作から戻ると、PDFドキュメントは指定されたモードで保存されます。 例えば、PDF Utilitiesサービスを使用して `FAST_WEB_VIEW` モードを設定し、そのPDFドキュメントをEncryptionサービスの `encryptUsingPassword` 操作に渡した場合、返されるPDFドキュメントはパスワードで暗号化され、 `FAST_WEB_VIEW` モードで保存されます。

>[!NOTE]
>
>このセクションに関連付けられているクイック開始で `FAST_WEB_VIEW` モードが設定され、PDFドキュメントがEncryptionサービスの `encryptUsingPassword` 操作に渡されます。

**関連トピック**

[Java APIを使用したPDFドキュメントの保存オプションの設定](pdf-utilities.md#set-pdf-document-save-options-using-the-java-api)

[WebサービスAPIを使用してPDFドキュメントの保存オプションを設定する](pdf-utilities.md#set-pdf-document-save-options-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDFドキュメントのパスワードによる暗号化](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Java APIを使用したPDFドキュメントの保存オプションの設定 {#set-pdf-document-save-options-using-the-java-api}

PDF Utilities API(Java)を使用して、PDFドキュメントの保存オプションを設定します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-pdfutility-client.jarなどのクライアントJARファイルを含めます。

1. PDFUtilityServiceクライアントの作成

   コンストラクタを使用し、接続プロパティを含むオブジェクトを渡して、 `PDFUtilityServiceClient``ServiceClientFactory` オブジェクトを作成します。

1. 保存モードの設定

   * コンストラクタを使用して `PDFUtilitySaveMode` オブジェクトを作成します。
   * オブジェクトのメソッドを呼び出し、保存モードを指定する文字列値を渡して、 `PDFUtilitySaveMode` 保存モードを設定し `setSaveStyle` ます。 例えば、Web表示を高速にするために保存するには、を渡し `FAST_WEB_VIEW`ます。

1. 「save style」操作を呼び出します

   オブジェクトの `PDFUtilityServiceClient``setSaveMode` メソッドを呼び出し、次の値を渡します。

   * A `com.adobe.idp.Document` object that represents the PDF document.
   * 使用する保存スタイルを含む `PDFUtilitySaveMode` オブジェクト。
   * 以前の設定を上書きするかどうかを決定するために使用されるBoolean値です。

   指定した保存スタイルを使用して形式設定された `com.adobe.idp.Document` オブジェクトを返します。

1. PDFドキュメントを別のAEM Forms操作に渡す

   * 返された `com.adobe.idp.Document` オブジェクトを別のAEM Forms操作に渡します。

**関連トピック**

[PDFドキュメントの保存モードの設定](pdf-utilities.md#setting-pdf-document-save-modes)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用してPDFドキュメントの保存オプションを設定する {#set-pdf-document-save-options-using-the-web-service-api}

PDF Utilities AP（Webサービス）を使用して、PDFドキュメントの保存オプションを設定します。

1. プロジェクトファイルを含める

   * PDF UtilitiesサービスのWSDLファイルを使用するMicrosoft .NETクライアントアセンブリを作成します。
   * Microsoft .NETクライアントアセンブリを参照します。

1. PDFUtilityServiceクライアントの作成

   プロキシクラスのコンストラクターを使用して、 `PDFUtilityServiceService` オブジェクトを作成します。

1. 保存モードの設定

   * コンストラクタを使用して `PDFUtilitySaveMode` オブジェクトを作成します。
   * 保存モードを設定するには、保存モードを指定する `PDFUtilitySaveMode` オブジェクトの `saveStyle` メソッドにstring値を割り当てます。 例えば、Web表示を高速にするために保存するには、を指定し `FAST_WEB_VIEW`ます。

1. 「save style」操作を呼び出します

   オブジェクトの `PDFUtilityServiceService``setSaveMode` メソッドを呼び出し、次の値を渡します。

   * A `BLOB` object that represents the PDF document.
   * 使用する保存スタイルを含む `PDFUtilitySaveMode` オブジェクト。
   * 以前の設定を上書きするかどうかを決定するために使用されるBoolean値です。

   指定した保存スタイルを使用して形式設定された `BLOB` オブジェクトを返します。 その後、そのオブジェクトをPDFドキュメントとして保存できます。

1. PDFドキュメントを別のForms操作に渡す

   * 返された `BLOB` オブジェクトを別のAEM Forms操作に渡します。

**関連トピック**

[PDFドキュメントの保存モードの設定](pdf-utilities.md#setting-pdf-document-save-modes)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64エンコーディングを使用する.NETクライアントアセンブリの作成](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## PDFドキュメントのサニタイズ {#sanitizing-pdf-documents}

PDF UtilitiesのJava APIを使用して、PDFドキュメントをプログラム的にXDPドキュメントに変換できます。

>[!NOTE]
>
>For more information about the PDF Utilities service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-4}

PDFドキュメントを不要にするには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. PDFUtilityServiceクライアントを作成します。
1. サニタイゼーション操作を呼び出します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成するには、必要なJARファイルを含めます。

**PDFUtilityServiceクライアントの作成**

プログラムによって改善操作を実行する前に、PDFUtilityServiceクライアントを作成する必要があります。 Java APIを使用して、これは `PDFUtilityServiceClient` オブジェクトを作成することで実現します。

**PDFからXDPへの変換操作の呼び出し**

サービスクライアントの作成後、サービス化操作を呼び出すことができます。

**関連トピック**

[Java APIを使用したPDFドキュメントのXDPドキュメントへの変換](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[WebサービスAPIを使用してPDFドキュメントをXDPドキュメントに変換する](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java APIを使用してPDFドキュメントを不要なものにする {#sanitize-pdf-documents-using-the-java-api}

PDF Utilities API(Java)を使用して、ドキュメントを削除します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-pdfutility-client.jarなどのクライアントJARファイルを含めます。

1. PDFUtilityServiceクライアントの作成

   コンストラクタを使用し、接続プロパティを含むオブジェクトを渡して、 `PDFUtilityServiceClient``ServiceClientFactory` オブジェクトを作成します。

1. PDFからXDPへの変換操作の呼び出し

   変換を実行するには、 `PDFUtilityServiceClient` オブジェクトの `convertPDFtoXDP` メソッドを呼び出し、PDFファイルを表す `com.adobe.idp.Document` オブジェクトを渡します。 このメソッドは、新しく作成されたXDPファイルを表す `com.adobe.idp.Document` オブジェクトを返します。

**関連トピック**

[PDFドキュメントのサニタイズ](/help/forms/developing/pdf-utilities-service-java-api.md#quick-start-soap-mode-sanitizing-pdf-documents)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
