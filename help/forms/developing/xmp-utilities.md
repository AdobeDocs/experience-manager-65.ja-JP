---
title: XMP ユーティリティの操作
seo-title: Working with XMP Utilities
description: XMP ユーティリティ Java および web サービス API を使用して、XMP メタデータをプログラムで PDF ドキュメントにインポートして、PDF ドキュメントから XMP メタデータを取得して保存します。
seo-description: Use the XMP Utilities Java and Web Service APIs to programmatically import XMP metadata into a PDF document and retrieve and save XMP metadata from a PDF document.
uuid: 90ce6cef-efe1-456a-8e0c-5ba90249dda0
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 01d5677f-5c87-4a6e-987b-8eda9acc0b27
role: Developer
exl-id: cff65f74-ba95-438e-88a4-5ec7d22aafba
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1405'
ht-degree: 100%

---

# XMP ユーティリティの操作 {#working-with-xmp-utilities}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

**XMP ユーティリティサービスについて**

PDF ドキュメントにはメタデータが含まれます。メタデータは、ドキュメントの内容と区別されるドキュメントに関する情報（テキストやグラフィックなど）です。Adobe Extensive Metadata Platform（XMP）は、ドキュメントのメタデータを処理するための標準です。

XMP ユーティリティサービスでは、XMP メタデータを PDF ドキュメントから取得して保存し、XMPメタデータを PDF ドキュメントにインポートすることができます。

XMP ユーティリティサービスを使用して、次のタスクを実行できます。

* メタデータを PDF ドキュメントにインポートします。（[メタデータを PDF ドキュメントにインポート](xmp-utilities.md#importing-metadata-into-pdf-documents)を参照。）
* PDF ドキュメントからメタデータをエクスポート（[PDF ドキュメントからのメタデータのエクスポート](xmp-utilities.md#exporting-metadata-from-pdf-documents)を参照。）

>[!NOTE]
>
>XMP ユーティリティサービスについて詳しくは、[AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

## メタデータの PDF ドキュメントへのインポート {#importing-metadata-into-pdf-documents}

XMP ユーティリティ Java および web サービス API を使用して、XMP メタデータをプログラムで PDF ドキュメントにインポートできます。メタデータは、ドキュメントの作成者やドキュメントに関連するキーワードなど、PDF ドキュメントに関する情報を提供します。メタデータは、次の図に示すように、ドキュメントの「ドキュメントのプロパティ」ダイアログに配置できます。

![ww_ww_metadatadialog](assets/ww_ww_metadatadialog.png)

プログラムによってメタデータを PDF ドキュメントにインポートするには、メタデータ値を指定する既存の XML ドキュメントを使用するか、タイプ `XMPUtilityMetadata` のオブジェクトを使用できます。（[AEM Forms API リファレンス](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ja)を参照。）

>[!NOTE]
>
>この節では、XML ドキュメントを使用してメタデータを PDF ドキュメントにインポートする方法を説明します。

次の XML コードには、以前のイラストに対応するメタデータ値が含まれています。例えば、キーワードを指定する太字の項目に注意してください。

```xml
 <?xpacket begin="?" id="W5M0MpCehiHzreSzNTczkc9d"?>
 <x:xmpmeta xmlns:x="adobe:ns:meta/" x:xmptk="Adobe XMP Core 4.2-jc015 52.349034, 2008 Jun 20 00:30:39-PDT (debug)">
       <rdf:RDF xmlns:rdf="https://www.w3.org/1999/02/22-rdf-syntax-ns#">
          <rdf:Description rdf:about=""
                xmlns:xmp="https://ns.adobe.com/xap/1.0/">
             <xmp:MetadataDate>2008-10-22T10:52:21-04:00</xmp:MetadataDate>
             <xmp:CreatorTool>AEM Forms</xmp:CreatorTool>
             <xmp:ModifyDate>2008-10-22T10:52:21-04:00</xmp:ModifyDate>
             <xmp:CreateDate>2008-02-13T11:00:18-05:00</xmp:CreateDate>
          </rdf:Description>
          <rdf:Description rdf:about=""
                xmlns:pdf="https://ns.adobe.com/pdf/1.3/">
             <pdf:Producer>AEM Forms</pdf:Producer>
             <pdf:Keywords>keyword1, keyword2, keyword3,keyword4</pdf:Keywords>
          </rdf:Description>
          <rdf:Description rdf:about=""
                xmlns:xmpMM="https://ns.adobe.com/xap/1.0/mm/">
             <xmpMM:DocumentID>uuid:1cce1f84-331e-4d8d-8538-15441c271dd7</xmpMM:DocumentID>
             <xmpMM:InstanceID>uuid:cdda0ca6-7c91-4771-9dc9-796c8fe59350</xmpMM:InstanceID>
          </rdf:Description>
          <rdf:Description rdf:about=""
                >
             <dc:format>application/pdf</dc:format>
             <dc:description>
                <rdf:Alt>
                   <rdf:li xml:lang="x-default">Adobe Designer Sample</rdf:li>
                </rdf:Alt>
             </dc:description>
             <dc:title>
                <rdf:Alt>
                   <rdf:li xml:lang="x-default">Grant Application</rdf:li>
                </rdf:Alt>
             </dc:title>
             <dc:creator>
                <rdf:Seq>
                   <rdf:li>Tony Blue</rdf:li>
                </rdf:Seq>
             </dc:creator>
             <dc:subject>
                <rdf:Bag>
                   <rdf:li>keyword1</rdf:li>
                   <rdf:li>keyword2</rdf:li>
                   <rdf:li>keyword3</rdf:li>
                   <rdf:li>keyword4</rdf:li>
                </rdf:Bag>
             </dc:subject>
          </rdf:Description>
          <rdf:Description rdf:about=""
                xmlns:desc="https://ns.adobe.com/xfa/promoted-desc/">
             <desc:version rdf:parseType="Resource">
                <rdf:value>1.0</rdf:value>
                <desc:ref>/template/subform[1]</desc:ref>
             </desc:version>
             <desc:contact rdf:parseType="Resource">
                <rdf:value>Adobe Systems Incorporated</rdf:value>
                <desc:ref>/template/subform[1]</desc:ref>
             </desc:contact>
          </rdf:Description>
       </rdf:RDF>
 </x:xmpmeta>
```

>[!NOTE]
>
>XMP ユーティリティサービスについて詳しくは、[AEM Forms サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary-of-steps}

XMP メタデータを PDF ドキュメントにインポートするには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. XMPUtilityService クライアントを作成します。
1. XMP メタデータのインポート操作を呼び出します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**XMPUtilityService クライアントを作成**

プログラムで XMP ユーティリティの操作をプログラムで実行する前に、XMPUtilityService クライアントを作成する必要があります。Java API では、これは `XMPUtilityServiceClient` オブジェクトを作成することによって実現できます。Web サービス API では、これは `XMPUtilityServiceService` オブジェクトを使用することによって実現できます。

**XMP メタデータインポート操作を呼び出す**

サービスクライアントを作成したら、XMP メタデータインポート操作の 1 つを呼び出して、XMP のメタデータを指定した PDF ドキュメントにインポートできます。

**関連トピック**

[Java API を使用して XMP メタデータをインポート](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[Web サービス API を使用した XMP メタデータのインポート](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API を使用して XMP メタデータをインポート {#import-xmp-metadata-using-the-java-api}

XMP ユーティリティ API（Java）を使用して XMP メタデータをインポートします。

1. プロジェクトファイルを含める

   adobe-livecycle-client.jar などのクライアント JAR ファイルを、Java プロジェクトのクラスパスに含めます。

   >[!NOTE]
   >
   >adobe-pdfutility-client.jar ファイルには、XMP ユーティリティサービスをプログラムで呼び出すことを可能にするクラスが含まれています。

1. XMPUtilityService クライアントを作成

   `XMPUtilityServiceClient` オブジェクトを作成するには、コンストラクターを使用し、接続プロパティを含む `ServiceClientFactory` オブジェクトを渡します。

1. XMP メタデータのインポート操作の呼び出し

   XMP メタデータを変更するには、`XMPUtilityServiceClient` オブジェクトの `importMetadata` メソッドまたは `importXMP` メソッドを呼び出します。

   `importMetadata` メソッドを使用する場合、次の値を渡します。

   * PDF ファイルを表す `com.adobe.idp.Document` オブジェクト。
   * インポートするメタデータを含む `XMPUtilityMetadata` オブジェクト。

   `importXMP` メソッドを使用する場合、次の値を渡します。

   * PDF ファイルを表す `com.adobe.idp.Document` オブジェクト。
   * インポートするメタデータを含む XML ファイルを表す `com.adobe.idp.Document` オブジェクト。

   どちらの場合も、返される値は新しくインポートされたメタデータを含む PDF ファイルを表す `com.adobe.idp.Document` オブジェクトです。このオブジェクトをディスクに保存できます。

**関連トピック**

[メタデータの PDF ドキュメントへの読み込み](xmp-utilities.md#importing-metadata-into-pdf-documents)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用した XMP メタデータのインポート {#importing-xmp-metadata-using-the-web-service-api}

XMP ユーティリティ web サービス API を使用してプログラムで XMP メタデータをインポートするには、次のタスクを実行します。

1. プロジェクトファイルを含める

   * XMP Utilities サービスの WSDL ファイルを使用する Microsoft .NET クライアントアセンブリを作成します。（[Base64 エンコーディングを使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)を参照してください）。
   * Microsoft .NET クライアントアセンブリを参照します（[Base64 エンコーディングを使用する .NET クライアントアセンブリの作成](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)を参照してください）。

1. XMPUtilityService クライアントを作成

   プロキシクラスのコンストラクターを使用して `XMPUtilityServiceService` オブジェクトを作成します。

1. XMP メタデータのインポート操作の呼び出し

   XMP メタデータを変更するには、`XMPUtilityServiceService` オブジェクトの `importMetadata` メソッドまたは `importXMP` メソッドを呼び出します。

   `importMetadata` メソッドを使用する場合、次の値を渡します。

   * PDF ファイルを表す `BLOB` オブジェクト。
   * インポートするメタデータを含む `XMPUtilityMetadata` オブジェクト。

   `importXMP` メソッドを使用する場合、次の値を渡します。

   * PDF ファイルを表す `BLOB` オブジェクト。
   * インポートするメタデータを含む XML ファイルを表す `BLOB` オブジェクト。

   どちらの場合も、返される値は新しくインポートされたメタデータを含む PDF ファイルを表す `BLOB` オブジェクトです。このオブジェクトをディスクに保存できます。

**関連トピック**

[メタデータの PDF ドキュメントへのインポート](xmp-utilities.md#importing-metadata-into-pdf-documents)

<!--REVIEW: [Quick Start (Base64): Importing XMP metadata using the web service API](unresolvedlink-lc-qs-xmp-utilities-xu.xml#ws624e3cba99b79e12e69a9941333732bac8-7be8.2)-->

[Base64 エンコーディングを使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64 エンコーディングを使用する .NET クライアントアセンブリの作成](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## PDF ドキュメントからのメタデータへの書き出し {#exporting-metadata-from-pdf-documents}

XMP Utilities Java および web サービス API を使用すると、プログラムによって PDF ドキュメントから XMP メタデータを取得および保存することができます。

>[!NOTE]
>
>XMP Utilities サービスについて詳しくは、[AEM Forms サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary_of_steps-1}

PDF ドキュメントから XMP メタデータをエクスポートするには、次の手順に従います。

1. プロジェクトファイルを含めます。
1. XMPUtilityService クライアントを作成します。
1. XMP メタデータのエクスポート操作を呼び出します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**XMPUtilityService クライアントを作成**

プログラムで XMP ユーティリティの操作をプログラムで実行する前に、XMPUtilityService クライアントを作成する必要があります。Java API では、これは `XMPUtilityServiceClient` オブジェクトを作成することで実行されます。Web サービス API でこれを実行するには、`XMPUtilityServiceService` オブジェクトを使用します。

**XMPメタデータのエクスポート操作を呼び出す**

サービスクライアントを作成したら、XMP メタデータのエクスポート操作を 1 つ呼び出すことができます。これを使用すると、XMP のメタデータを確認したり、ディスクに保存したりすることができます。

**関連トピック**

[Java API を使用して XMP メタデータをインポート](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[Web サービス API を使用した XMP メタデータのインポート](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API を使用した XMP メタデータのエクスポート {#export-xmp-metadata-using-the-java-api}

XMP Utilities API（Java）を使用して XMP メタデータをエクスポートします。

1. プロジェクトファイルを含める

   adobe-livecycle-client.jar などのクライアント JAR ファイルを、Java プロジェクトのクラスパスに含めます。

   >[!NOTE]
   >
   >adobe-pdfutility-client.jar ファイルには、XMP Utility サービスをプログラムで呼び出すことができるクラスが含まれています。

1. XMPUtilityService クライアントを作成

   `XMPUtilityServiceClient` オブジェクトを作成するには、コンストラクターを使用し、接続プロパティを含む `ServiceClientFactory` オブジェクトを渡します。

1. XMP メタデータのインポート操作の呼び出し

   XMP メタデータを検査するには、`XMPUtilityServiceClient` オブジェクトの `exportMetadata` メソッドを呼び出して、PDF ファイルを表す `com.adobe.idp.Document` オブジェクトを渡します。このメソッドは、取得したメタデータを含む `XMPUtilityMetadata` オブジェクトを返します。

   XMP メタデータを取得して保存するには、`XMPUtilityServiceClient` オブジェクトの `exportXMP` メソッドを呼び出して、PDF ファイルを表す `com.adobe.idp.Document` オブジェクトを渡します。このメソッドは、取得したメタデータを含む `com.adobe.idp.Document` オブジェクトを返します。このオブジェクトは、XML ファイルとしてディスクに保存できます。

**関連項目**

[PDF ドキュメントからのメタデータへの書き出し](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用した XMP メタデータのエクスポート {#export-xmp-metadata-using-the-web-service-api}

XMP Utilities API（web サービス）を使用して XMP メタデータをエクスポートします。

1. プロジェクトファイルを含める

   * XMP Utilities サービスの WSDL ファイルを使用する Microsoft .NET クライアントアセンブリを作成します。
   * Microsoft .NET クライアントアセンブリを参照します。

1. XMPUtilityService クライアントを作成

   プロキシクラスのコンストラクターを使用して `XMPUtilityServiceService` オブジェクトを作成します。

1. XMP メタデータのインポート操作の呼び出し

   XMP メタデータを検査するには、`XMPUtilityServiceClient` オブジェクトの `exportMetadata` メソッドを呼び出して、PDF ファイルを表す `BLOB` オブジェクトを渡します。このメソッドは、取得したメタデータを含む `XMPUtilityMetadata` オブジェクトを返します。

   XMP メタデータを取得して保存するには、`XMPUtilityServiceClient` オブジェクトの `exportXMP` メソッドを呼び出して、PDF ファイルを表す `BLOB` オブジェクトを渡します。このメソッドは、取得したメタデータを含む `BLOB` オブジェクトを返します。このオブジェクトは、XML ファイルとしてディスクに保存できます。

**関連項目**

[PDF ドキュメントからのメタデータへの書き出し](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[Base64 エンコーディングを使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64 エンコーディングを使用する .NET クライアントアセンブリの作成](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
