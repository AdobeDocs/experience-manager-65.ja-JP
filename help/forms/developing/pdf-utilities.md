---
title: PDFユーティリティの操作
seo-title: PDFユーティリティの操作
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

---


# PDFユーティリティの操作 {#working-with-pdf-utilities}

**PDF Utilitiesサービスについて**

PDF Utilitiesサービスでは、PDFファイル形式とXDPファイル形式間の変換、PDFドキュメントプロパティの設定と取得、XMPメタデータの操作を行うことができます。 例えば、PDFドキュメントを別の形式に変換する前に、そのプロパティを調べて、変換用に呼び出すサービス操作を決定すると便利です。

PDF Utilitiesサービスを使用して、次のタスクを実行できます。

* PDFドキュメントをXDPドキュメントに変換します。
* XDPドキュメントをPDFドキュメントに変換します。 (XDPドキュ [メントのPDFドキュメントへの変換を参照](pdf-utilities.md#converting-xdp-documents-into-pdf-documents))。
* PDFドキュメントのプロパティを取得します。 (PDFドキュメ [ントのプロパティの取得を参照](pdf-utilities.md#retrieving-pdf-document-properties))。
* PDFドキュメントを保存し、Web表示用に最適化します。 (PDFドキュメ [ントの保存モードの設定を参照](pdf-utilities.md#setting-pdf-document-save-modes))。

>[!NOTE]
>
>For more information about the PDF Utilities service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## PDFドキュメントのXDPドキュメントへの変換 {#converting-pdf-documents-into-xdp-documents}

PDF UtilitiesのJavaおよびWebサービスAPIを使用して、PDFドキュメントをXDPドキュメントにプログラム的に変換できます。

>[!NOTE]
>
>For more information about the PDF Utilities service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary-of-steps}

PDFドキュメントをXDPドキュメントに変換するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. PDFUtilityServiceクライアントを作成します。
1. PDFからXDPへの変換操作を呼び出します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

**PDFUtilityServiceクライアントの作成**

プログラムで「PDF Utilities」操作を実行する前に、PDFUtilityServiceクライアントを作成する必要があります。 Java APIを使用すると、オブジェクトを作成することで実現で `PDFUtilityServiceClient` きます。 WebサービスAPIでは、オブジェクトを使用して行い `PDFUtilityServiceService` ます。

**「PDF to XDP conversion」操作の呼び出し**

サービスクライアントを作成した後、PDFからXDPへの変換操作を呼び出すことができます。

**関連トピック**

[Java APIを使用したPDFドキュメントのXDPドキュメントへの変換](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[WebサービスAPIを使用したPDFドキュメントのXDPドキュメントへの変換](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java APIを使用したPDFドキュメントのXDPドキュメントへの変換 {#convert-pdf-documents-into-xdp-documents-using-the-java-api}

PDF Utilities API(Java)を使用してPDFドキュメントをXDPドキュメントに変換します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-pdfutility-client.jarなどのクライアントJARファイルを含めます。

1. PDFUtilityServiceクライアントの作成

   コンストラク `PDFUtilityServiceClient` ターを使用し、接続プロパティを含むオブジェクトを渡 `ServiceClientFactory` して、オブジェクトを作成します。

1. 「PDF to XDP conversion」操作の呼び出し

   変換を実行するには、オブジェクトの `PDFUtilityServiceClient` メソッドを呼び出 `convertPDFtoXDP` し、PDFファイルを表 `com.adobe.idp.Document` すオブジェクトを渡します。 このメソッドは、新しく `com.adobe.idp.Document` 作成されたXDPファイルを表すオブジェクトを返します。

**関連トピック**

[PDFドキュメントのXDPドキュメントへの変換](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したPDFドキュメントのXDPドキュメントへの変換 {#convert-pdf-documents-into-xdp-documents-using-the-web-service-api}

PDF Utilities API（Webサービス）を使用してPDFドキュメントをXDPドキュメントに変換します。

1. プロジェクトファイルを含める

   * PDF UtilitiesサービスのWSDLファイルを使用するMicrosoft .NETクライアントアセンブリを作成します。
   * Microsoft .NETクライアントアセンブリを参照します。

1. PDFUtilityServiceクライアントの作成

   プロキシクラス `PDFUtilityServiceService` のコンストラクターを使用して、オブジェクトを作成します。

1. 「PDF to XDP conversion」操作の呼び出し

   オブジェクト `PDFUtilityServiceService` のメソッドを `convertPDFtoXDP` 呼び出し、PDFファイルを表 `BLOB` すオブジェクトを渡します。 このメソッドは、新しく `BLOB` 作成されたXDPファイルを表すオブジェクトを返します。

**関連トピック**

[PDFドキュメントのXDPドキュメントへの変換](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64エンコーディングを使用する.NETクライアントアセンブリの作成](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## XDPドキュメントからPDFドキュメントへの変換 {#converting-xdp-documents-into-pdf-documents}

PDF UtilitiesのJavaおよびWebサービスAPIを使用して、XDPドキュメントをPDFドキュメントにプログラム的に変換できます。

>[!NOTE]
>
>For more information about the PDF Utilities service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-1}

XDPドキュメントをPDFドキュメントに変換するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. PDFUtilityServiceクライアントを作成します。
1. XDPからPDFへの変換操作を呼び出します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

**PDFUtilityServiceクライアントの作成**

プログラムで「PDF Utilities」操作を実行する前に、PDFUtilityServiceクライアントを作成する必要があります。 Java APIを使用すると、オブジェクトを作成することで実現で `PDFUtilityServiceClient` きます。 WebサービスAPIでは、オブジェクトを使用して行い `PDFUtilityServiceService` ます。

**XDPからPDFへの変換操作の呼び出し**

サービスクライアントを作成した後、XDPからPDFへの変換操作を呼び出すことができます。

**関連トピック**

[Java APIを使用したXDPドキュメントのPDFドキュメントへの変換](pdf-utilities.md#convert-xdp-documents-into-pdf-documents-using-the-java-api)

[WebサービスAPIを使用したXDPドキュメントのPDFドキュメントへの変換](pdf-utilities.md#converting-xdp-documents-into-pdf-documents-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java APIを使用したXDPドキュメントのPDFドキュメントへの変換 {#convert-xdp-documents-into-pdf-documents-using-the-java-api}

PDF Utilities API(Java)を使用してXDPドキュメントをPDFドキュメントに変換します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-pdfutility-client.jarなどのクライアントJARファイルを含めます。

1. PDFUtilityServiceクライアントの作成

   コンストラク `PDFUtilityServiceClient` ターを使用し、接続プロパティを含むオブジェクトを渡 `ServiceClientFactory` して、オブジェクトを作成します。

1. XDPからPDFへの変換操作の呼び出し

   変換を実行するには、オブジェクトの `PDFUtilityServiceClient` メソッドを呼び出 `convertXDPtoPDF` し、XDPファイルを表 `com.adobe.idp.Document` すオブジェクトを渡します。 このメソッドは、新しく `com.adobe.idp.Document` 作成されたPDFファイルを表すオブジェクトを返します。

**関連トピック**

[XDPドキュメントからPDFドキュメントへの変換](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したXDPドキュメントのPDFドキュメントへの変換 {#converting-xdp-documents-into-pdf-documents-using-the-web-service-api}

PDF Utilities API（WebサービスAPI）を使用してXDPドキュメントをPDFドキュメントに変換します。

1. プロジェクトファイルを含める

   * PDF UtilitiesサービスのWSDLファイルを使用するMicrosoft .NETクライアントアセンブリを作成します。
   * Microsoft .NETクライアントアセンブリを参照します。

1. PDFUtilityServiceクライアントの作成

   プロキシクラス `PDFUtilityServiceService` のコンストラクターを使用して、オブジェクトを作成します。

1. XDPからPDFへの変換操作の呼び出し

   変換を実行するには、オブジェクトの `PDFUtilityServiceService` メソッドを呼び出 `convertXDPtoPDF` し、XDPファイルを表 `BLOB` すオブジェクトを渡します。 このメソッドは、新しく `BLOB` 作成されたPDFファイルを表すオブジェクトを返します。

**関連トピック**

[XDPドキュメントからPDFドキュメントへの変換](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64エンコーディングを使用する.NETクライアントアセンブリの作成](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## PDFドキュメントのプロパティの取得 {#retrieving-pdf-document-properties}

ドキュメントが入力可能なフォームか、ドキュメントの読み取りに最低限必要なAcrobatバージョンかなど、PDF UtilitiesのJavaおよびWebサービスAPIを使用して、PDFドキュメントのプロパティをプログラムで取得できます。

>[!NOTE]
>
>For more information about the PDF Utilities service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)

### 手順の概要 {#summary_of_steps-2}

PDFドキュメントのプロパティを取得するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. PDFUtilityServiceクライアントを作成します。
1. プロパティ取得操作を呼び出します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

**PDFUtilityServiceクライアントの作成**

プログラムで「PDF Utilities」操作を実行する前に、PDFUtilityServiceクライアントを作成する必要があります。 Java APIを使用すると、オブジェクトを作成することで実現で `PDFUtilityServiceClient` きます。 WebサービスAPIでは、これはオブジェクトを使用して行わ `PDFUtilityServiceService` れます。

**プロパティ取得操作を呼び出します**

サービスクライアントを作成した後、プロパティ取得操作を呼び出すことができます。

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

   コンストラク `PDFUtilityServiceClient` ターを使用し、接続プロパティを含むオブジェクトを渡 `ServiceClientFactory` して、オブジェクトを作成します。

1. プロパティ取得操作を呼び出します

   変換を実行するには、オブジェクトの `PDFUtilityServiceClient` メソッドを呼び出 `getPDFProperties` し、次のように渡します。

   * A `com.adobe.idp.Document` object that represents the PDF document.
   * 評価す `PDFPropertiesOptionSpec` るプロパティを含むオブジェクトです。
   The method returns a `PDFPropertiesResult` object that contains the results of the query.

**関連トピック**

[PDFドキュメントのプロパティの取得](pdf-utilities.md#retrieving-pdf-document-properties)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したPDFドキュメントのプロパティの取得 {#retrieve-pdf-document-properties-using-the-web-service-api}

PDF Utilities webサービスAPIを使用してPDFドキュメントのプロパティを取得します。

1. プロジェクトファイルを含める

   * PDF UtilitiesサービスのWSDLファイルを使用するMicrosoft .NETクライアントアセンブリを作成します。
   * Microsoft .NETクライアントアセンブリを参照します。

1. PDFUtilityServiceクライアントの作成

   プロキシクラス `PDFUtilityServiceService` のコンストラクターを使用して、オブジェクトを作成します。

1. プロパティ取得操作を呼び出します

   変換を実行するには、オブジェクトの `PDFUtilityServiceService` メソッドを呼び出 `getPDFProperties` し、次のように渡します。

   * A `BLOB` object that represents the PDF document.
   * 評価す `PDFPropertiesOptionSpec` るプロパティを含むオブジェクトです。
   The method returns a `PDFPropertiesResult` object that contains the results of the query.

**関連トピック**

[PDFドキュメントのプロパティの取得](pdf-utilities.md#retrieving-pdf-document-properties)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64エンコーディングを使用する.NETクライアントアセンブリの作成](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## PDFドキュメントの保存モードの設定 {#setting-pdf-document-save-modes}

PDF UtilitiesサービスのJavaおよびWebサービスAPIを使用して、PDFドキュメントの保存モードをプログラムで設定できます。 PDF Utilitiesサービスを使用して保存モードを設定する場合、PDF Utilitiesサービスは保存モードを設定するだけで、実際にはPDFドキュメントを保存しません。 PDFドキュメントは、別のサービス操作に渡されるときに保存されます。 例えば、PDF Utilitiesサービスを使用して特定の保存モードを設定し、それをEncryptionサービスに渡すと、PDFドキュメントが実際に保存され、暗号化されます。

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

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

**PDFUtilityServiceクライアントの作成**

プログラムで「PDF Utilities」操作を実行する前に、PDFUtilityServiceクライアントを作成する必要があります。 Java APIを使用すると、オブジェクトを作成することで実現で `PDFUtilityServiceClient` きます。 WebサービスAPIでは、これはオブジェクトを使用して行わ `PDFUtilityServiceService` れます。

**保存モードの設定**

次の保存オプションのいずれかを選択できます。

* `INCREMENTAL`:保存に要する時間を短縮するために増分的に保存するには
* `FAST_WEB_VIEW`:Web表示用に保存
* `FULL`:完全保存を使用して保存するには（最適化を行わないで）

**「save style」操作の呼び出し**

サービスクライアントを作成した後、プロパティ取得操作を呼び出すことができます。

**PDFドキュメントを別のAEM Forms操作に渡す**

PDF Utilitiesサービスで指定した保存モードを設定したら、PDFドキュメントを別のAEM Forms操作に渡します。 その操作から戻ると、PDFドキュメントは指定したモードで保存されます。 例えば、PDF Utilitiesサービスを使用してモードを設定し、そのPDFドキュメントをEncryptionサービスの操作に渡す場合、返されたPDFドキュメントはパスワードで暗号化され、 `FAST_WEB_VIEW` モードで保存され `encryptUsingPassword``FAST_WEB_VIEW` ます。

>[!NOTE]
>
>このセクションに関連付けられているクイックスタートでモ `FAST_WEB_VIEW` ードが設定され、PDFドキュメントがEncryptionサービスの操作に渡さ `encryptUsingPassword` れます。

**関連トピック**

[Java APIを使用したPDFドキュメントの保存オプションの設定](pdf-utilities.md#set-pdf-document-save-options-using-the-java-api)

[WebサービスAPIを使用したPDFドキュメントの保存オプションの設定](pdf-utilities.md#set-pdf-document-save-options-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[PDFドキュメントのパスワードによる暗号化](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Java APIを使用したPDFドキュメントの保存オプションの設定 {#set-pdf-document-save-options-using-the-java-api}

PDF Utilities API(Java)を使用してPDFドキュメントの保存オプションを設定します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-pdfutility-client.jarなどのクライアントJARファイルを含めます。

1. PDFUtilityServiceクライアントの作成

   コンストラク `PDFUtilityServiceClient` ターを使用し、接続プロパティを含むオブジェクトを渡 `ServiceClientFactory` して、オブジェクトを作成します。

1. 保存モードの設定

   * コンストラクタを使用して `PDFUtilitySaveMode` オブジェクトを作成します。
   * オブジェクトのメソッドを呼び出し、保 `PDFUtilitySaveMode` 存モードを指 `setSaveStyle` 定するstring値を渡して、保存モードを設定します。 例えば、Web表示用に保存するには、を渡しま `FAST_WEB_VIEW`す。

1. 「save style」操作の呼び出し

   オブジェクト `PDFUtilityServiceClient` のメソッドを `setSaveMode` 呼び出し、次の値を渡します。

   * A `com.adobe.idp.Document` object that represents the PDF document.
   * 使用す `PDFUtilitySaveMode` る保存スタイルを含むオブジェクトです。
   * 以前の設定を上書きするかどうかを指定するために使用されるBoolean値です。
   このメソッドは、指定した保存ス `com.adobe.idp.Document` タイルを使用して形式設定されたオブジェクトを返します。

1. PDFドキュメントを別のAEM Forms操作に渡す

   * 返されたオブジェクト `com.adobe.idp.Document` を別のAEM Forms操作に渡します。

**関連トピック**

[PDFドキュメントの保存モードの設定](pdf-utilities.md#setting-pdf-document-save-modes)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したPDFドキュメントの保存オプションの設定 {#set-pdf-document-save-options-using-the-web-service-api}

PDF Utilities AP（Webサービス）を使用して、PDFドキュメントの保存オプションを設定します。

1. プロジェクトファイルを含める

   * PDF UtilitiesサービスのWSDLファイルを使用するMicrosoft .NETクライアントアセンブリを作成します。
   * Microsoft .NETクライアントアセンブリを参照します。

1. PDFUtilityServiceクライアントの作成

   プロキシクラス `PDFUtilityServiceService` のコンストラクターを使用して、オブジェクトを作成します。

1. 保存モードの設定

   * コンストラクタを使用して `PDFUtilitySaveMode` オブジェクトを作成します。
   * 保存モードを設定するには、保存モードを指定するオブジェクト `PDFUtilitySaveMode` のメソッドに `saveStyle` string値を割り当てます。 例えば、Web表示用に保存するには、を指定しま `FAST_WEB_VIEW`す。

1. 「save style」操作の呼び出し

   オブジェクト `PDFUtilityServiceService` のメソッドを `setSaveMode` 呼び出し、次の値を渡します。

   * A `BLOB` object that represents the PDF document.
   * 使用す `PDFUtilitySaveMode` る保存スタイルを含むオブジェクトです。
   * 以前の設定を上書きするかどうかを指定するために使用されるBoolean値です。
   このメソッドは、指定した保存ス `BLOB` タイルを使用して形式設定されたオブジェクトを返します。 その後、そのオブジェクトをPDFドキュメントとして保存できます。

1. PDFドキュメントを別のForms操作に渡す

   * 返されたオブジェクト `BLOB` を別のAEM Forms操作に渡します。

**関連トピック**

[PDFドキュメントの保存モードの設定](pdf-utilities.md#setting-pdf-document-save-modes)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64エンコーディングを使用する.NETクライアントアセンブリの作成](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## PDFドキュメントのサニタイズ {#sanitizing-pdf-documents}

PDF Utilities Java APIを使用して、PDFドキュメントをXDPドキュメントにプログラム的に変換できます。

>[!NOTE]
>
>For more information about the PDF Utilities service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-4}

PDFドキュメントを削除するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. PDFUtilityServiceクライアントを作成します。
1. サニタイズ操作を呼び出します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成するには、必要なJARファイルを含めます。

**PDFUtilityServiceクライアントの作成**

プログラムでサニタイゼーション操作を実行する前に、PDFUtilityServiceクライアントを作成する必要があります。 Java APIを使用すると、オブジェクトを作成することで実現で `PDFUtilityServiceClient` きます。

**「PDF to XDP conversion」操作の呼び出し**

サービスクライアントを作成した後で、サービス化操作を呼び出すことができます。

**関連トピック**

[Java APIを使用したPDFドキュメントのXDPドキュメントへの変換](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[WebサービスAPIを使用したPDFドキュメントのXDPドキュメントへの変換](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java APIを使用してPDFドキュメントを削除する {#sanitize-pdf-documents-using-the-java-api}

PDF Utilities API(Java)を使用してドキュメントを削除します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-pdfutility-client.jarなどのクライアントJARファイルを含めます。

1. PDFUtilityServiceクライアントの作成

   コンストラク `PDFUtilityServiceClient` ターを使用し、接続プロパティを含むオブジェクトを渡 `ServiceClientFactory` して、オブジェクトを作成します。

1. 「PDF to XDP conversion」操作の呼び出し

   変換を実行するには、オブジェクトの `PDFUtilityServiceClient` メソッドを呼び出 `convertPDFtoXDP` し、PDFファイルを表 `com.adobe.idp.Document` すオブジェクトを渡します。 このメソッドは、新しく `com.adobe.idp.Document` 作成されたXDPファイルを表すオブジェクトを返します。

**関連トピック**

[PDFドキュメントのサニタイズ](/help/forms/developing/pdf-utilities-service-java-api.md#quick-start-soap-mode-sanitizing-pdf-documents)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
