---
title: XMPユーティリティの操作
seo-title: XMPユーティリティの操作
description: XMP UtilitiesのJavaおよびWeb Service APIを使用して、プログラムによってXMPメタデータをPDFドキュメントに読み込み、XMPメタデータをPDFドキュメントから取得して保存します。
seo-description: XMP UtilitiesのJavaおよびWeb Service APIを使用して、プログラムによってXMPメタデータをPDFドキュメントに読み込み、XMPメタデータをPDFドキュメントから取得して保存します。
uuid: 90ce6cef-efe1-456a-8e0c-5ba90249dda0
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 01d5677f-5c87-4a6e-987b-8eda9acc0b27
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '1423'
ht-degree: 3%

---


# XMPユーティリティの操作{#working-with-xmp-utilities}

**XMP Utilitiesサービスについて**

PDFドキュメントにはメタデータが含まれます。メタデータは、ドキュメントに関する情報で、テキストやグラフィックなどのドキュメントのコンテンツと区別されます。 Adobe拡張メタデータプラットフォーム(XMP)は、ドキュメントのメタデータを処理するための標準です。

XMP Utilitiesサービスは、PDFドキュメントからXMPメタデータを取得して保存し、XMPメタデータをPDFドキュメントに読み込むことができます。

XMP Utilitiesサービスを使用して、次のタスクを実行できます。

* PDFドキュメントへのメタデータの読み込み (「[PDFドキュメントへのメタデータの読み込み](xmp-utilities.md#importing-metadata-into-pdf-documents)」を参照)。
* PDFドキュメントからのメタデータの書き出し ([PDFドキュメントからのメタデータの書き出し](xmp-utilities.md#exporting-metadata-from-pdf-documents)を参照)。

>[!NOTE]
>
>XMP Utilitiesサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

## PDFドキュメントへのメタデータの読み込み{#importing-metadata-into-pdf-documents}

XMP UtilitiesのJavaおよびWebサービスAPIを使用して、XMPメタデータをPDFドキュメントにプログラム的に読み込むことができます。 メタデータは、ドキュメントの作成者やドキュメントに関連するキーワードなど、PDFドキュメントに関する情報を提供します。 メタデータは、次の図に示すように、ドキュメントのドキュメントプロパティダイアログにあります。

![ww_ww_metadatadialog](assets/ww_ww_metadatadialog.png)

プログラムによってメタデータをPDFドキュメントに読み込むには、メタデータ値を指定する既存のXMLドキュメントを使用するか、`XMPUtilityMetadata`型のオブジェクトを使用します。 (「[AEM FormsAPIリファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)」を参照)。

>[!NOTE]
>
>この節では、XMLドキュメントを使用してメタデータをPDFドキュメントに読み込む方法について説明します。

次のXMLコードには、前の図に対応するメタデータ値が含まれています。 例えば、太字の項目でキーワードを指定しています。

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
>XMP Utilitiesサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順{#summary-of-steps}の概要

XMPメタデータをPDFドキュメントに読み込むには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. XMPUtilityServiceクライアントを作成します。
1. XMPメタデータの読み込み操作を呼び出します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めてください。

**XMPUtilityServiceクライアントの作成**

プログラムによってXMP Utilities操作を実行する前に、XMPUtilityServiceクライアントを作成する必要があります。 Java APIを使用すると、`XMPUtilityServiceClient`オブジェクトを作成することで実現できます。 WebサービスAPIでは、`XMPUtilityServiceService`オブジェクトを使用して実行します。

**XMPメタデータの読み込み操作を呼び出します**

サービスクライアントの作成後、XMPメタデータの読み込み操作の1つを呼び出して、指定したPDFドキュメントにXMPメタデータを読み込むことができます。

**関連トピック**

[Java APIを使用したXMPメタデータの読み込み](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[WebサービスAPIを使用したXMPメタデータの読み込み](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API {#import-xmp-metadata-using-the-java-api}を使用したXMPメタデータの読み込み

XMP Utilities API(Java)を使用してXMPメタデータを読み込みます。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-pdfutility-client.jarなどのクライアントJARファイルを含めます。

   >[!NOTE]
   >
   >adobe-pdfutility-client.jarファイルには、XMP Utilitiesサービスをプログラムで呼び出すことを可能にするクラスが含まれています。

1. XMPUtilityServiceクライアントの作成

   コンストラクターを使用し、接続プロパティを含む`ServiceClientFactory`オブジェクトを渡して、`XMPUtilityServiceClient`オブジェクトを作成します。

1. XMPメタデータの読み込み操作を呼び出します

   XMPメタデータを変更するには、`XMPUtilityServiceClient`オブジェクトの`importMetadata`メソッドまたは`importXMP`メソッドを呼び出します。

   `importMetadata`メソッドを使用する場合は、次の値を渡します。

   * PDFファイルを表す`com.adobe.idp.Document`オブジェクトです。
   * 読み込むメタデータを含む`XMPUtilityMetadata`オブジェクト。

   `importXMP`メソッドを使用する場合は、次の値を渡します。

   * PDFファイルを表す`com.adobe.idp.Document`オブジェクトです。
   * 読み込むメタデータを含むXMLファイルを表す`com.adobe.idp.Document`オブジェクト。

   いずれの場合も、返される値は、新しく読み込まれたメタデータが含まれたPDFファイルを表す`com.adobe.idp.Document`オブジェクトです。 その後、このオブジェクトをディスクに保存できます。

**関連トピック**

[PDFドキュメントへのメタデータの読み込み](xmp-utilities.md#importing-metadata-into-pdf-documents)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#importing-xmp-metadata-using-the-web-service-api}を使用したXMPメタデータの読み込み

XMP Utilities WebサービスAPIを使用してXMPメタデータをプログラムで読み込むには、次のタスクを実行します。

1. プロジェクトファイルを含める

   * XMP UtilitiesサービスのWSDLファイルを使用するMicrosoft .NETクライアントアセンブリを作成します。 (「[Base64エンコードを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)」を参照)。
   * Microsoft .NETクライアントアセンブリを参照します。 （「[Base64エンコード](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)を使用する.NETクライアントアセンブリの作成」を参照）。

1. XMPUtilityServiceクライアントの作成

   プロキシクラスのコンストラクターを使用して`XMPUtilityServiceService`オブジェクトを作成します。

1. XMPメタデータの読み込み操作を呼び出します

   XMPメタデータを変更するには、`XMPUtilityServiceService`オブジェクトの`importMetadata`メソッドまたは`importXMP`メソッドを呼び出します。

   `importMetadata`メソッドを使用する場合は、次の値を渡します。

   * PDFファイルを表す`BLOB`オブジェクトです。
   * 読み込むメタデータを含む`XMPUtilityMetadata`オブジェクト。

   `importXMP`メソッドを使用する場合は、次の値を渡します。

   * PDFファイルを表す`BLOB`オブジェクトです。
   * 読み込むメタデータを含むXMLファイルを表す`BLOB`オブジェクト。

   いずれの場合も、返される値は、新しく読み込まれたメタデータが含まれたPDFファイルを表す`BLOB`オブジェクトです。 その後、このオブジェクトをディスクに保存できます。

**関連トピック**

[PDFドキュメントへのメタデータの読み込み](xmp-utilities.md#importing-metadata-into-pdf-documents)

<!--REVIEW: [Quick Start (Base64): Importing XMP metadata using the web service API](unresolvedlink-lc-qs-xmp-utilities-xu.xml#ws624e3cba99b79e12e69a9941333732bac8-7be8.2)-->

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64エンコーディングを使用する.NETクライアントアセンブリの作成](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## PDFドキュメントからのメタデータの書き出し{#exporting-metadata-from-pdf-documents}

XMP UtilitiesのJavaおよびWebサービスAPIを使用して、PDFドキュメントからXMPメタデータをプログラム的に取得し、保存できます。

>[!NOTE]
>
>XMP Utilitiesサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順{#summary_of_steps-1}の概要

PDFドキュメントからXMPメタデータを書き出すには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. XMPUtilityServiceクライアントを作成します。
1. XMPメタデータ書き出し操作を呼び出します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めてください。

**XMPUtilityServiceクライアントの作成**

プログラムによってXMP Utilities操作を実行する前に、XMPUtilityServiceクライアントを作成する必要があります。 Java APでは、`XMPUtilityServiceClient`オブジェクトを作成することで実現します。 WebサービスAPIでは、これは`XMPUtilityServiceService`オブジェクトを使用して実行されます。

**XMPメタデータ書き出し操作の呼び出し**

サービスクライアントを作成したら、XMPメタデータの書き出し操作の1つを呼び出します。この操作は、XMPメタデータを検査したり、ディスクに保存したりするのに使用できます。

**関連トピック**

[Java APIを使用したXMPメタデータの読み込み](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[WebサービスAPIを使用したXMPメタデータの読み込み](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API {#export-xmp-metadata-using-the-java-api}を使用したXMPメタデータの書き出し

XMP Utilities API(Java)を使用してXMPメタデータを書き出します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-pdfutility-client.jarなどのクライアントJARファイルを含めます。

   >[!NOTE]
   >
   >adobe-pdfutility-client.jarファイルには、XMP Utilityサービスをプログラム的に呼び出すことを可能にするクラスが含まれています。

1. XMPUtilityServiceクライアントの作成

   コンストラクターを使用し、接続プロパティを含む`ServiceClientFactory`オブジェクトを渡して、`XMPUtilityServiceClient`オブジェクトを作成します。

1. XMPメタデータの読み込み操作を呼び出します

   XMPメタデータを検査するには、`XMPUtilityServiceClient`オブジェクトの`exportMetadata`メソッドを呼び出し、PDFファイルを表す`com.adobe.idp.Document`オブジェクトを渡します。 このメソッドは、取得したメタデータを含む`XMPUtilityMetadata`オブジェクトを返します。

   XMPメタデータを取得して保存するには、`XMPUtilityServiceClient`オブジェクトの`exportXMP`メソッドを呼び出し、PDFファイルを表す`com.adobe.idp.Document`オブジェクトを渡します。 このメソッドは、取得したメタデータを含む`com.adobe.idp.Document`オブジェクトを返します。このオブジェクトは、XMLファイルとしてディスクに保存できます。

**関連トピック**

[PDFドキュメントからのメタデータの書き出し](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#export-xmp-metadata-using-the-web-service-api}を使用したXMPメタデータの書き出し

XMP Utilities API（Webサービス）を使用してXMPメタデータを書き出します。

1. プロジェクトファイルを含める

   * XMP UtilitiesサービスのWSDLファイルを使用するMicrosoft .NETクライアントアセンブリを作成します。
   * Microsoft .NETクライアントアセンブリを参照します。

1. XMPUtilityServiceクライアントの作成

   プロキシクラスのコンストラクターを使用して`XMPUtilityServiceService`オブジェクトを作成します。

1. XMPメタデータの読み込み操作を呼び出します

   XMPメタデータを検査するには、`XMPUtilityServiceClient`オブジェクトの`exportMetadata`メソッドを呼び出し、PDFファイルを表す`BLOB`オブジェクトを渡します。 このメソッドは、取得したメタデータを含む`XMPUtilityMetadata`オブジェクトを返します。

   XMPメタデータを取得して保存するには、`XMPUtilityServiceClient`オブジェクトの`exportXMP`メソッドを呼び出し、PDFファイルを表す`BLOB`オブジェクトを渡します。 このメソッドは、取得したメタデータを含む`BLOB`オブジェクトを返します。このオブジェクトは、XMLファイルとしてディスクに保存できます。

**関連トピック**

[PDFドキュメントからのメタデータの書き出し](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64エンコーディングを使用する.NETクライアントアセンブリの作成](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
