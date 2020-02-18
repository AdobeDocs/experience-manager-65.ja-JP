---
title: XMPユーティリティの操作
seo-title: XMPユーティリティの操作
description: 'null'
seo-description: 'null'
uuid: 90ce6cef-efe1-456a-8e0c-5ba90249dda0
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 01d5677f-5c87-4a6e-987b-8eda9acc0b27
translation-type: tm+mt
source-git-commit: 06335b9a85414b6b1141dd19c863dfaad0812503

---


# XMPユーティリティの操作 {#working-with-xmp-utilities}

**XMP Utilitiesサービスについて**

PDFドキュメントにはメタデータが含まれています。メタデータは、ドキュメントに関する情報で、テキストやグラフィックなど、ドキュメントのコンテンツと区別されます。 Adobe Extensible Metadata Platform(XMP)は、ドキュメントのメタデータを処理するための標準です。

XMP Utilitiesサービスは、PDFドキュメントからXMPメタデータを取得して保存し、XMPメタデータをPDFドキュメントに読み込むことができます。

XMP Utilitiesサービスを使用して、次のタスクを実行できます。

* PDFドキュメントへのメタデータの読み込み (PDFドキュメント [へのメタデータの読み込みを参照](xmp-utilities.md#importing-metadata-into-pdf-documents))。
* PDFドキュメントからのメタデータの書き出し (PDFドキュメント [からのメタデータの書き出しを参照](xmp-utilities.md#exporting-metadata-from-pdf-documents))。

>[!NOTE]
>
>For more information about the XMP Utilities service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## PDFドキュメントへのメタデータの読み込み {#importing-metadata-into-pdf-documents}

XMP UtilitiesのJavaおよびWebサービスAPIを使用して、XMPメタデータをプログラム的にPDFドキュメントに読み込むことができます。 メタデータは、ドキュメントの作成者やドキュメントに関連するキーワードなど、PDFドキュメントに関する情報を提供します。 メタデータは、次の図に示すように、ドキュメントのドキュメントプロパティダイアログ内に配置できます。

![ww_ww_metadatadialog](assets/ww_ww_metadatadialog.png)

プログラムによってPDFドキュメントにメタデータを読み込む場合は、メタデータ値を指定する既存のXMLドキュメントを使用するか、またはタイプのオブジェクトを使用できま `XMPUtilityMetadata`す。 (『 [AEM Forms APIリファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)』を参照)。

>[!NOTE]
>
>この節では、XMLドキュメントを使用してメタデータをPDFドキュメントに読み込む方法について説明します。

次のXMLコードには、前の図に対応するメタデータ値が含まれています。 例えば、キーワードを指定する太字の項目に注目してください。

```as3
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
>For more information about the XMP Utilities service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary-of-steps}

XMPメタデータをPDFドキュメントに読み込むには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. XMPUtilityServiceクライアントを作成します。
1. XMPメタデータの読み込み操作を呼び出します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

**XMPUtilityServiceクライアントの作成**

プログラムでXMP Utilities操作を実行する前に、XMPUtilityServiceクライアントを作成する必要があります。 Java APIを使用すると、オブジェクトを作成することで実現で `XMPUtilityServiceClient` きます。 WebサービスAPIでは、オブジェクトを使用して行い `XMPUtilityServiceService` ます。

**XMPメタデータの読み込み操作の呼び出し**

サービスクライアントの作成後、XMPメタデータの読み込み操作の1つを呼び出して、指定したPDFドキュメントにXMPメタデータを読み込むことができます。

**関連トピック**

[Java APIを使用したXMPメタデータの読み込み](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[WebサービスAPIを使用したXMPメタデータの読み込み](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java APIを使用したXMPメタデータの読み込み {#import-xmp-metadata-using-the-java-api}

XMP Utilities API(Java)を使用してXMPメタデータを読み込みます。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-pdfutility-client.jarなどのクライアントJARファイルを含めます。

   >[!NOTE]
   >
   >adobe-pdfutility-client.jarファイルには、XMP Utilitiesサービスをプログラム的に呼び出すことを可能にするクラスが含まれています。

1. XMPUtilityServiceクライアントの作成

   コンストラク `XMPUtilityServiceClient` ターを使用し、接続プロパティを含むオブジェクトを `ServiceClientFactory` 渡して、オブジェクトを作成します。

1. XMPメタデータの読み込み操作の呼び出し

   XMPメタデータを変更するには、オブジェクトのメソ `XMPUtilityServiceClient` ッドまたはそのメ `importMetadata` ソッドを呼び出 `importXMP` します。

   この方法を使用する `importMetadata` 場合は、次の値を渡します。

   * PDFフ `com.adobe.idp.Document` ァイルを表すオブジェクトです。
   * 読み込 `XMPUtilityMetadata` むメタデータを含むオブジェクトです。
   この方法を使用する `importXMP` 場合は、次の値を渡します。

   * PDFフ `com.adobe.idp.Document` ァイルを表すオブジェクトです。
   * 読み込 `com.adobe.idp.Document` むメタデータが含まれるXMLファイルを表すオブジェクトです。
   どちらの場合も、返される値は、新しく読み込ま `com.adobe.idp.Document` れたメタデータを含むPDFファイルを表すオブジェクトです。 その後、このオブジェクトをディスクに保存できます。

**関連トピック**

[PDFドキュメントへのメタデータの読み込み](xmp-utilities.md#importing-metadata-into-pdf-documents)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したXMPメタデータの読み込み {#importing-xmp-metadata-using-the-web-service-api}

XMP Utilities webサービスAPIを使用してXMPメタデータをプログラムで読み込むには、次のタスクを実行します。

1. プロジェクトファイルを含める

   * XMP UtilitiesサービスのWSDLファイルを使用するMicrosoft .NETクライアントアセンブリを作成します。 (「Base64エンコ [ーディングを使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)」を参照)。
   * Microsoft .NETクライアントアセンブリを参照します。 (Base64エンコ [ーディングを使用した.NETクライアントアセンブリの作成を参照](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding))。

1. XMPUtilityServiceクライアントの作成

   プロキシクラス `XMPUtilityServiceService` のコンストラクターを使用して、オブジェクトを作成します。

1. XMPメタデータの読み込み操作の呼び出し

   XMPメタデータを変更するには、オブジェクトのメソ `XMPUtilityServiceService` ッドまたはそのメ `importMetadata` ソッドを呼び出 `importXMP` します。

   この方法を使用する `importMetadata` 場合は、次の値を渡します。

   * PDFフ `BLOB` ァイルを表すオブジェクトです。
   * 読み込 `XMPUtilityMetadata` むメタデータを含むオブジェクトです。
   この方法を使用する `importXMP` 場合は、次の値を渡します。

   * PDFフ `BLOB` ァイルを表すオブジェクトです。
   * 読み込 `BLOB` むメタデータが含まれるXMLファイルを表すオブジェクトです。
   どちらの場合も、返される値は、新しく読み込ま `BLOB` れたメタデータを含むPDFファイルを表すオブジェクトです。 その後、このオブジェクトをディスクに保存できます。

**関連トピック**

[PDFドキュメントへのメタデータの読み込み](xmp-utilities.md#importing-metadata-into-pdf-documents)

<!--REVIEW: [Quick Start (Base64): Importing XMP metadata using the web service API](unresolvedlink-lc-qs-xmp-utilities-xu.xml#ws624e3cba99b79e12e69a9941333732bac8-7be8.2)-->

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64エンコーディングを使用する.NETクライアントアセンブリの作成](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## PDFドキュメントからのメタデータの書き出し {#exporting-metadata-from-pdf-documents}

XMP UtilitiesのJavaおよびWebサービスAPIを使用して、PDFドキュメントからXMPメタデータをプログラム的に取得し、保存できます。

>[!NOTE]
>
>For more information about the XMP Utilities service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary_of_steps-1}

PDFドキュメントからXMPメタデータを書き出すには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. XMPUtilityServiceクライアントを作成します。
1. XMPメタデータの書き出し操作を呼び出します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

**XMPUtilityServiceクライアントの作成**

プログラムでXMP Utilities操作を実行する前に、XMPUtilityServiceクライアントを作成する必要があります。 Java APを使用する場合は、オブジェクトを作成することで実現で `XMPUtilityServiceClient` きます。 WebサービスAPIでは、これはオブジェクトを使用して行わ `XMPUtilityServiceService` れます。

**XMPメタデータの書き出し操作の呼び出し**

サービスクライアントの作成後、XMPメタデータの書き出し操作の1つを呼び出して、XMPメタデータの検査やディスクへの保存に使用できます。

**関連トピック**

[Java APIを使用したXMPメタデータの読み込み](xmp-utilities.md#import-xmp-metadata-using-the-java-api)

[WebサービスAPIを使用したXMPメタデータの読み込み](xmp-utilities.md#importing-xmp-metadata-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java APIを使用したXMPメタデータの書き出し {#export-xmp-metadata-using-the-java-api}

XMP Utilities API(Java)を使用したXMPメタデータの書き出し：

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-pdfutility-client.jarなどのクライアントJARファイルを含めます。

   >[!NOTE]
   >
   >adobe-pdfutility-client.jarファイルには、XMP Utilityサービスをプログラム的に呼び出すことを可能にするクラスが含まれています。

1. XMPUtilityServiceクライアントの作成

   コンストラク `XMPUtilityServiceClient` ターを使用し、接続プロパティを含むオブジェクトを `ServiceClientFactory` 渡して、オブジェクトを作成します。

1. XMPメタデータの読み込み操作の呼び出し

   XMPメタデータを調べるには、オブジェクトの `XMPUtilityServiceClient` メソッドを呼び出 `exportMetadata` し、PDFファイルを表すオ `com.adobe.idp.Document` ブジェクトを渡します。 取得したメタデータを `XMPUtilityMetadata` 含むオブジェクトを返します。

   XMPメタデータを取得して保存するには、オブジェクトのメ `XMPUtilityServiceClient` ソッドを呼び出 `exportXMP` し、PDFファイルを表 `com.adobe.idp.Document` すオブジェクトを渡します。 このメソッドは、取得し `com.adobe.idp.Document` たメタデータを含むオブジェクトを返します。このメタデータは、XMLファイルとしてディスクに保存できます。

**関連トピック**

[PDFドキュメントからのメタデータの書き出し](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したXMPメタデータの書き出し {#export-xmp-metadata-using-the-web-service-api}

XMP Utilities API（Webサービス）を使用してXMPメタデータを書き出します。

1. プロジェクトファイルを含める

   * XMP UtilitiesサービスのWSDLファイルを使用するMicrosoft .NETクライアントアセンブリを作成します。
   * Microsoft .NETクライアントアセンブリを参照します。

1. XMPUtilityServiceクライアントの作成

   プロキシクラス `XMPUtilityServiceService` のコンストラクターを使用して、オブジェクトを作成します。

1. XMPメタデータの読み込み操作の呼び出し

   XMPメタデータを調べるには、オブジェクトの `XMPUtilityServiceClient` メソッドを呼び出 `exportMetadata` し、PDFファイルを表すオ `BLOB` ブジェクトを渡します。 取得したメタデータを `XMPUtilityMetadata` 含むオブジェクトを返します。

   XMPメタデータを取得して保存するには、オブジェクトのメ `XMPUtilityServiceClient` ソッドを呼び出 `exportXMP` し、PDFファイルを表 `BLOB` すオブジェクトを渡します。 このメソッドは、取得し `BLOB` たメタデータを含むオブジェクトを返します。このメタデータは、XMLファイルとしてディスクに保存できます。

**関連トピック**

[PDFドキュメントからのメタデータの書き出し](xmp-utilities.md#exporting-metadata-from-pdf-documents)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Base64エンコーディングを使用する.NETクライアントアセンブリの作成](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
