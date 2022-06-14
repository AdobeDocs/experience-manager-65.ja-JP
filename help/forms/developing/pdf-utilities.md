---
title: PDF ユーティリティの操作
seo-title: Working with PDF Utilities
description: PDF Utilities サービスを使用して、PDFと XDP のファイル形式の変換、PDF ドキュメントのプロパティの設定と取得、XMP メタデータの操作を行います。
seo-description: Use the PDF Utilities service to convert between PDF and XDP file formats, set and retrieve PDF document properties, and manipulate XMP metadata.
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
source-wordcount: '2579'
ht-degree: 100%

---

# PDF ユーティリティの操作 {#working-with-pdf-utilities}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

**PDF Utilities サービスについて**

PDF Utilities サービスを使用すると、PDF と XDP のファイル形式の変換、PDF ドキュメントのプロパティの設定と取得、XMP メタデータの操作を行うことができます。例えば、PDF ドキュメントを別の形式に変換する前にプロパティを調べておくと、変換用に呼び出すサービス操作を判断するのに役立ちます。

PDF Utilities サービスを使用して、次のタスクを行うことができます。

* PDF ドキュメントを XDP ドキュメントに変換する。
* XDP ドキュメントを PDF ドキュメントに変換する（[XDP ドキュメントから PDF ドキュメントへの変換](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)を参照してください）。
* PDF ドキュメントのプロパティを取得する（[PDF ドキュメントのプロパティの取得](pdf-utilities.md#retrieving-pdf-document-properties)を参照してください）。
* PDF ドキュメントを保存して、高速な web 表示用に最適化する（[PDF ドキュメントの保存モードの設定](pdf-utilities.md#setting-pdf-document-save-modes)を参照してください）。

>[!NOTE]
>
>PDF Utilities サービスについて詳しくは、「[AEM Forms サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)」を参照してください。

## PDF ドキュメントの XDP ドキュメントへの変換 {#converting-pdf-documents-into-xdp-documents}

PDF Utilities Java および web サービス API を使用すると、プログラムで PDF ドキュメントを XDP ドキュメントに変換できます。

>[!NOTE]
>
>PDF Utilities サービスについて詳しくは、「[AEM Forms サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)」を参照してください。

### 手順の概要 {#summary-of-steps}

PDF ドキュメントを XDP ドキュメントに変換するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. PDFUtilityService クライアントを作成します。
1. PDF を XDP に変換する操作を呼び出します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**PDFUtilityService クライアントを作成**

プログラムで PDF Utilities 操作を実行する前に、PDFUtilityService クライアントを作成する必要があります。Java API では、`PDFUtilityServiceClient` オブジェクトを作成して行います。Web サービス API では、`PDFUtilityServiceService` オブジェクトを使用して行います。

**PDF を XDP に変換する操作を呼び出す**

サービスクライアントを作成したら、PDF を XDP に変換する操作を呼び出すことができます。

**関連情報**

[Java API を使用して PDF ドキュメントを XDP ドキュメントに変換する](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[Web サービス API を使用して PDF ドキュメントを XDP ドキュメントに変換する](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティを設定する](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API を使用して PDF ドキュメントを XDP ドキュメントに変換する {#convert-pdf-documents-into-xdp-documents-using-the-java-api}

PDF Utilities API(Java) を使用して、PDF ドキュメントを XDP ドキュメントに変換します。

1. プロジェクトファイルを含める

   adobe-livecycle-client.jar などのクライアント JAR ファイルを、Java プロジェクトのクラスパスに含めます。

1. PDFUtilityService クライアントの作成

   コンストラクターを使用し、接続プロパティを含む `ServiceClientFactory` オブジェクトを渡すことにより、`PDFUtilityServiceClient` オブジェクトを作成します。

1. PDF を XDP に変換する操作を呼び出す

   コンバージョンを実行するには、 `PDFUtilityServiceClient` オブジェクトの `convertPDFtoXDP` メソッドを呼び出して PDF ファイルを表す `com.adobe.idp.Document` オブジェクトを渡します。このメソッドは、新しく作成された XDP ファイルを表す `com.adobe.idp.Document` オブジェクトを返します。

**関連情報**

[PDF ドキュメントの XDP ドキュメントへの変換](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティを設定する](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用して PDF ドキュメントを XDP ドキュメントに変換する {#convert-pdf-documents-into-xdp-documents-using-the-web-service-api}

PDF Utilities API（web サービス）を使用して、PDF ドキュメントを XDP ドキュメントに変換します。

1. プロジェクトファイルを含める

   * PDF Utilities サービスの WSDL ファイルを使用する、Microsoft .NET クライアントアセンブリを作成します。
   * Microsoft .NET クライアントアセンブリを参照します。

1. PDFUtilityService クライアントの作成

   プロキシクラスのコンストラクターを使用して、`PDFUtilityServiceService` オブジェクトを作成します。

1. PDF を XDP に変換する操作を呼び出す

   `PDFUtilityServiceService` オブジェクトの `convertPDFtoXDP` メソッドを呼び出して、PDF ファイルを表す `BLOB` オブジェクトに渡します。このメソッドは、新しく作成された XDP ファイルを表す `BLOB` オブジェクトを返します。

**関連情報**

[PDF ドキュメントの XDP ドキュメントへの変換](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[Base64 エンコーディングを使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64 エンコーディングを使用する .NET クライアントアセンブリの作成](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## XDP ドキュメントから PDF ドキュメントへの変換 {#converting-xdp-documents-into-pdf-documents}

PDF Utilities Java および web サービス API を使用すると、プログラムで XDP ドキュメントを PDF ドキュメントに変換できます。

>[!NOTE]
>
>PDF Utilities サービスについて詳しくは、「[AEM Forms サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)」を参照してください。

### 手順の概要 {#summary_of_steps-1}

XDP ドキュメントを PDF ドキュメントに変換するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. PDFUtilityService クライアントを作成します。
1. XDP を PDF に変換する操作を呼び出します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**PDFUtilityService クライアントを作成**

プログラムで PDF Utilities 操作を実行する前に、PDFUtilityService クライアントを作成する必要があります。Java API では、`PDFUtilityServiceClient` オブジェクトを作成して行います。Web サービス API では、`PDFUtilityServiceService` オブジェクトを使用して行います。

**XDP を PDF に変換する操作を呼び出す**

サービスクライアントを作成したら、XDP を PDF に変換する操作を呼び出すことができます。

**関連情報**

[Java API を使用して XDP ドキュメントを PDF ドキュメントに変換する](pdf-utilities.md#convert-xdp-documents-into-pdf-documents-using-the-java-api)

[Web サービス API を使用して XDP ドキュメントを PDF ドキュメントに変換する](pdf-utilities.md#converting-xdp-documents-into-pdf-documents-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティを設定する](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API を使用して XDP ドキュメントを PDF ドキュメントに変換する {#convert-xdp-documents-into-pdf-documents-using-the-java-api}

XDP ドキュメントを PDF ドキュメントに変換するには、PDF Utilities API (Java) を使用します。

1. プロジェクトファイルを含める

   adobe-livecycle-client.jar などのクライアント JAR ファイルを、Java プロジェクトのクラスパスに含めます。

1. PDFUtilityService クライアントの作成

   コンストラクターを使用して、接続プロパティを含む `ServiceClientFactory` オブジェクトを渡すことにより、`PDFUtilityServiceClient` オブジェクトを作成します。

1. XDP を PDF に変換する操作を呼び出す

   変換を実行するには、`PDFUtilityServiceClient` オブジェクトの `convertXDPtoPDF` メソッドを呼び出して、XDP ファイルを表す `com.adobe.idp.Document` オブジェクトに渡します。このメソッドは、新しく作成された PDF ファイルを表す `com.adobe.idp.Document` オブジェクトを返します。

**関連情報**

[XDP ドキュメントから PDF ドキュメントへの変換](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティを設定する](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用して XDP ドキュメントを PDF ドキュメントに変換する {#converting-xdp-documents-into-pdf-documents-using-the-web-service-api}

XDP ドキュメントを PDF ドキュメントに変換するには、PDF Utilities API（web サービス API）を使用します。

1. プロジェクトファイルを含める

   * PDF Utilities サービスの WSDL ファイルを使用する、Microsoft .NET クライアントアセンブリを作成します。
   * Microsoft .NET クライアントアセンブリを参照します。

1. PDFUtilityService クライアントの作成

   プロキシクラスのコンストラクターを使用して、`PDFUtilityServiceService` オブジェクトを作成します。

1. XDP を PDF に変換する操作を呼び出す

   変換を実行するには、`PDFUtilityServiceService` オブジェクトの `convertXDPtoPDF` メソッドを呼び出して、XDP ファイルを表す `BLOB` オブジェクトに渡します。このメソッドは、新しく作成された PDF ファイルを表す `BLOB` オブジェクトを返します。

**関連情報**

[XDP ドキュメントから PDF ドキュメントへの変換](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[Base64 エンコーディングを使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64 エンコーディングを使用する .NET クライアントアセンブリの作成](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## PDF ドキュメントのプロパティの取得 {#retrieving-pdf-document-properties}

PDF Utilities Java および web サービス API を使用すると、PDF ドキュメントのプロパティをプログラムで取得できます。プロパティからは、ドキュメントが入力可能なフォームであるか、ドキュメントを読むのに必要な最小バージョンの Acrobat であるかなどがわかります。

>[!NOTE]
>
>PDF Utilities サービスについて詳しくは、「[AEM Forms サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)」を参照してください。

### 手順の概要 {#summary_of_steps-2}

PDF ドキュメントのプロパティを取得するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. PDFUtilityService クライアントを作成します。
1. プロパティを取得する操作を呼び出します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**PDFUtilityService クライアントを作成**

プログラムで PDF Utilities 操作を実行する前に、PDFUtilityService クライアントを作成する必要があります。Java API では、`PDFUtilityServiceClient` オブジェクトを作成して行います。Web サービス API では、`PDFUtilityServiceService` オブジェクトを使用して行います。

**プロパティを取得する操作を呼び出す**

サービスクライアントを作成したら、プロパティを取得する操作を呼び出すことができます。

**関連情報**

[Java API を使用して PDF ドキュメントのプロパティを取得する](pdf-utilities.md#retrieve-pdf-document-properties-using-the-java-api)

[Web サービス API を使用して PDF ドキュメントのプロパティを取得する](pdf-utilities.md#retrieve-pdf-document-properties-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API を使用して PDF ドキュメントのプロパティを取得する {#retrieve-pdf-document-properties-using-the-java-api}

PDF Utilities API (Java) を使用して、PDF ドキュメントのプロパティを取得します。

1. プロジェクトファイルを含める

   adobe-livecycle-client.jar などのクライアント JAR ファイルを、Java プロジェクトのクラスパスに含めます。

1. PDFUtilityService クライアントの作成

   コンストラクターを使用して、接続プロパティを含む `ServiceClientFactory` オブジェクトを渡すことにより、`PDFUtilityServiceClient` オブジェクトを作成します。

1. プロパティ取得操作を呼び出す

   変換を実行するには、 `PDFUtilityServiceClient` オブジェクトの `getPDFProperties` メソッドを使用して、以下を渡します。

   * PDF ドキュメントを表す `com.adobe.idp.Document` オブジェクト。
   * 評価されるプロパティを含む `PDFPropertiesOptionSpec` オブジェクト。

   メソッドは、クエリの結果を含む `PDFPropertiesResult` オブジェクトを返します。

**関連項目**

[PDF ドキュメントのプロパティの取得](pdf-utilities.md#retrieving-pdf-document-properties)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用して PDF ドキュメントのプロパティを取得する {#retrieve-pdf-document-properties-using-the-web-service-api}

PDF Utilities web サービス API を使用して、PDF ドキュメントのプロパティを取得します。

1. プロジェクトファイルを含める

   * PDF Utilities サービスの WSDL ファイルを使用する、Microsoft .NET クライアントアセンブリを作成します。
   * Microsoft .NET クライアントアセンブリを参照します。

1. PDFUtilityService クライアントの作成

   プロキシクラスコンストラクターを使用して、`PDFUtilityServiceService` オブジェクトを作成します。

1. プロパティ取得操作を呼び出す

   変換を実行するには、 `PDFUtilityServiceService` オブジェクトの `getPDFProperties` メソッドを使用して、以下を渡します。

   * PDF ドキュメントを表す `BLOB` オブジェクト。
   * 評価されるプロパティを含む `PDFPropertiesOptionSpec` オブジェクト。

   メソッドは、クエリの結果を含む `PDFPropertiesResult` オブジェクトを返します。

**関連項目**

[PDF ドキュメントのプロパティの取得](pdf-utilities.md#retrieving-pdf-document-properties)

[Base64 エンコーディングを使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64 エンコーディングを使用する .NET クライアントアセンブリの作成](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## PDF ドキュメントの保存モードを設定する {#setting-pdf-document-save-modes}

PDF Utilities サービスの Java および web サービス API を使用して、PDF ドキュメントの保存モードをプログラムで設定することができます。PDF Utilities サービスを使用して保存モードを設定する場合、PDF Utilities サービスは保存モードのみを設定し、実際には PDF ドキュメントを保存しません。PDF ドキュメントは、別のサービス操作に渡されたときに保存されます。例えば、PDF Utilities サービスを使用して特定の保存モードを設定し、Encryption サービスに渡すことができます。この場合、PDF ドキュメントは実際に保存され暗号化されます。

>[!NOTE]
>
>PDF Utilities サービスについて詳しくは、「[AEM Forms サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)」を参照してください。

### 手順の概要 {#summary_of_steps-3}

PDF ドキュメントの保存オプションを設定するには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. PDFUtilityService クライアントを作成します。
1. 保存モードを設定します。
1. 保存操作を呼び出します。
1. PDF ドキュメントを別の操作に渡します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**PDFUtilityService クライアントを作成**

プログラムで PDF Utilities 操作を実行する前に、PDFUtilityService クライアントを作成する必要があります。Java API では、`PDFUtilityServiceClient` オブジェクトを作成して行います。Web サービス API では、`PDFUtilityServiceService` オブジェクトを使用してこれを実現します。

**保存モードを設定**

次のいずれかの保存オプションを指定できます。

* `INCREMENTAL`：増分を保存して保存にかかる時間を短縮する
* `FAST_WEB_VIEW`：web 表示を高速化するために保存する
* `FULL`：完全保存（最適化なしでの保存）を使用する

**スタイル保存操作を呼び出す**

サービスクライアントを作成したら、プロパティを取得する操作を呼び出すことができます。

**PDF ドキュメントを別の AEM Forms の操作に渡す**

指定の保存モードを PDF Utilities サービスで設定したら、PDF ドキュメントを別の AEM Forms の操作に渡します。その操作から返された PDF ドキュメントは、指定したモードで保存されます。例えば、PDF Utilities サービスで `FAST_WEB_VIEW` モードに設定して、PDF ドキュメントを暗号化サービスの `encryptUsingPassword` に渡すと、返される PDF ドキュメントはパスワードを付けて暗号化してから `FAST_WEB_VIEW` モードで保存されます。

>[!NOTE]
>
>このセクションに関連するクイックスタートでは、 `FAST_WEB_VIEW` モードに設定して、PDF ドキュメントを暗号化サービスの `encryptUsingPassword` 操作に渡します。

**関連情報**

[PDF ドキュメントの保存オプションを Java API を使用して設定する](pdf-utilities.md#set-pdf-document-save-options-using-the-java-api)

[PDF ドキュメントの保存オプションを web サービス API を使用して設定する](pdf-utilities.md#set-pdf-document-save-options-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティを設定する](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[パスワードを使用した PDF ドキュメントの暗号化](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### PDF ドキュメントの保存オプションを Java API を使用して設定する {#set-pdf-document-save-options-using-the-java-api}

PDF Utilities API（Java）を使用して、PDF ドキュメントの保存オプションを設定します。

1. プロジェクトファイルを含める

   adobe-livecycle-client.jar などのクライアント JAR ファイルを、Java プロジェクトのクラスパスに含めます。

1. PDFUtilityService クライアントの作成

   コンストラクターを使用して、接続プロパティを含む `ServiceClientFactory` オブジェクトを渡すことにより、`PDFUtilityServiceClient` オブジェクトを作成します。

1. 保存モードの設定

   * コンストラクターを使用して `PDFUtilitySaveMode` オブジェクトを作成します。
   * `PDFUtilitySaveMode` オブジェクトの `setSaveStyle` メソッドを呼び出して、保存モードを指定する文字列値を渡すことにより、保存モードを設定します。例えば、web 表示を高速化するために保存するには、`FAST_WEB_VIEW` を渡します。

1. スタイル保存操作を呼び出す

   `PDFUtilityServiceClient` オブジェクトの `setSaveMode` メソッドを呼び出して、次の値を渡します。

   * PDF ドキュメントを表す `com.adobe.idp.Document` オブジェクト。
   * 使用する保存スタイルを含む `PDFUtilitySaveMode` オブジェクト。
   * 以前の設定を上書きするかどうかを指定するブール値。

   このメソッドは、指定した保存スタイルで書式設定された `com.adobe.idp.Document` オブジェクトを返します。

1. PDFドキュメントを別の AEM Forms の操作に渡す

   * 返された `com.adobe.idp.Document` オブジェクトを別の AEM Forms の操作に渡します。

**関連情報**

[PDF ドキュメントの保存モードを設定する](pdf-utilities.md#setting-pdf-document-save-modes)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティを設定する](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### PDF ドキュメントの保存オプションを web サービス API を使用して設定する {#set-pdf-document-save-options-using-the-web-service-api}

PDF Utilities AP（web サービス）を使用して、PDF ドキュメントの保存オプションを設定します。

1. プロジェクトファイルを含める

   * PDF Utilities サービスの WSDL ファイルを使用する、Microsoft .NET クライアントアセンブリを作成します。
   * Microsoft .NET クライアントアセンブリを参照します。

1. PDFUtilityService クライアントの作成

   プロキシクラスコンストラクターを使用して、`PDFUtilityServiceService` オブジェクトを作成します。

1. 保存モードの設定

   * コンストラクターを使用して `PDFUtilitySaveMode` オブジェクトを作成します。
   * 保存モードを設定するには、保存モードを指定する `PDFUtilitySaveMode` オブジェクトの `saveStyle` メソッドに文字列値を割り当てます。例えば、web 表示を高速化するために保存するには、`FAST_WEB_VIEW` を指定します。

1. スタイル保存操作を呼び出す

   `PDFUtilityServiceService` オブジェクトの `setSaveMode` メソッドを呼び出して、次の値を渡します。

   * PDF ドキュメントを表す `BLOB` オブジェクト。
   * 使用する保存スタイルを含む `PDFUtilitySaveMode` オブジェクト。
   * 以前の設定を上書きするかどうかを指定するブール値。

   このメソッドは、指定した保存スタイルを使用して書式設定された `BLOB` オブジェクトを返します。 その後、そのオブジェクトを PDF ドキュメントとして保存できます。

1. PDF ドキュメントを別の Forms 操作に渡します

   * 返された `BLOB` オブジェクトを別の AEM Forms 操作に渡します。

**関連情報**

[PDF ドキュメントの保存モードを設定する](pdf-utilities.md#setting-pdf-document-save-modes)

[Base64 エンコーディングを使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64 エンコーディングを使用する .NET クライアントアセンブリの作成](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## PDF ドキュメントの不要部分を削除 {#sanitizing-pdf-documents}

PDF Utilities Java API を使用して、PDF ドキュメントを XDP ドキュメントにプログラムで変換できます。

>[!NOTE]
>
>PDF Utilities サービスについて詳しくは、[AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary_of_steps-4}

PDF ドキュメントの不要部分を削除するには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. PDFUtilityService クライアントを作成します。
1. 不要部分を削除する操作を呼び出します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成するには、必要な JAR ファイルを含めます。

**PDFUtilityService クライアントの作成**

プログラムで不要部分を削除する操作を実行する前に、PDFUtilityService クライアントを作成する必要があります。Java API を使用する場合は、`PDFUtilityServiceClient` オブジェクトの作成により実行できます。

**PDF を XDP に変換する操作を呼び出します**

サービスクライアントを作成したら、不要部分を削除する操作を呼び出すことができます。

**関連項目**

[Java API を使用して PDF ドキュメントを XDP ドキュメントに変換する](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[Web サービス API を使用して PDF ドキュメントを XDP ドキュメントに変換する](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API を使用してPDFドキュメントを削除する {#sanitize-pdf-documents-using-the-java-api}

PDF Utilities API (Java) を使用して、ドキュメントをサニタイズします。

1. プロジェクトファイルを含める

   adobe-pdfutility-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. PDFUtilityService クライアントの作成

   コンストラクターを使用し、接続プロパティを含む `ServiceClientFactory` オブジェクトを渡すことにより、`PDFUtilityServiceClient` オブジェクトを作成します。

1. PDF を XDP に変換する操作を呼び出す

   コンバージョンを実行するには、 `PDFUtilityServiceClient` オブジェクトの `convertPDFtoXDP` メソッドを呼び出して PDF ファイルを表す `com.adobe.idp.Document` オブジェクトを渡します。このメソッドは、新しく作成された XDP ファイルを表す `com.adobe.idp.Document` オブジェクトを返します。

**関連項目**

[PDFドキュメントのサニタイズ](/help/forms/developing/pdf-utilities-service-java-api.md#quick-start-soap-mode-sanitizing-pdf-documents)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
