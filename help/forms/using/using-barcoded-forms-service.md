---
title: Barcoded Forms サービス
description: AEM Forms Barcoded Formsサービスを使用して、バーコードの電子画像からデータを抽出します。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
docset: aem65
exl-id: edaf12be-473f-4175-b4e0-549b41159a55
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1022'
ht-degree: 25%

---

# Barcoded Forms サービス{#barcoded-forms-service}

## 概要 {#overview}

Barcoded Formsサービスは、バーコードの電子画像からデータを抽出します。 このサービスは、入力として 1 つまたは複数のバーコードを含んだ TIFF ファイルや PDF ファイルを受け取り、バーコードデータを抽出します。バーコードデータは、XML、区切り文字列、JavaScript で作成されたカスタム形式など、様々な形式で書式設定できます。

Barcoded Forms サービスは、スキャンされた TIFF または PDF ドキュメントとして提供される以下の&#x200B;**二次元**&#x200B;コードをサポートします。

* PDF417
* データマトリックス
* QR コード

このサービスはまた、スキャンされた TIFF または PDF ドキュメントとして提供される以下の&#x200B;**一次元**&#x200B;コードもサポートします。

* Codabar
* Code128
* Code 3 of 9
* EAN13
* EAN8

Barcoded Formsサービスを使用して、次のタスクを実行できます。

* バーコード画像 (TIFFまたはPDF) からバーコードデータを抽出します。 データは区切り文字付きテキストとして保存されます。
* 区切り文字付きテキストデータを XML（XDP または XFDF）に変換します。 XML データは、区切られたテキストよりも解析が容易です。 また、XDP 形式または XFDF 形式のデータは、AEM Formsの他のサービスの入力として使用できます。

Barcoded Formsサービスは、画像内の各バーコードを検索し、デコードして、データを抽出します。 このサービスは、バーコードデータを（必要に応じてエンティティエンコーディングを使用して）XML ドキュメントのコンテンツ要素で返します。 例えば、次のスキャンされたフォームTIFF画像には、2 つのバーコードが含まれています。

![例](assets/example.png)

Barcoded Formsサービスは、バーコードのデコード後に、次の XML ドキュメントを返します。

```xml
<?xml version="1.0" encoding="UTF-8" ?>  
<xb:scanned_image xmlns:xb="https://decoder.barcodedforms.adobe.com/xmlbeans"     path="tiff" version="1.0"> 
    <xb:decode> 
        <xb:date>2007-05-11T15:07:49.965-04:00</xb:date>  
        <xb:host_name>myhost.adobe.com</xb:host_name>  
        <xb:status type="success"> 
            <xb:message />  
        </xb:status> 
    </xb:decode> 
    <xb:barcode id="1"> 
        <xb:header symbology="pdf417"> 
            <xb:location page_no="1"> 
                <xb:coordinates> 
                    <xb:point x="0.119526625" y="0.60945123" />  
                    <xb:point x="0.44457594" y="0.60945123" />  
                    <xb:point x="0.44457594" y="0.78445125" />  
                    <xb:point x="0.119526625" y="0.78445125" />  
                </xb:coordinates> 
            </xb:location> 
        </xb:header> 
        <xb:body> 
            <xb:content encoding="utf-8">t_SID t_FirstName t_MiddleName t_LastName t_nFirstName t_nMiddleName t_nLastName 90210 Patti Y Penne Patti P Prosciutto</xb:content>  
        </xb:body> 
    </xb:barcode> 
    <xb:barcode id="2"> 
        <xb:header symbology="pdf417"> 
            <xb:location page_no="1"> 
                <xb:coordinates> 
                    <xb:point x="0.119526625" y="0.825" />  
                    <xb:point x="0.44457594" y="0.825" />  
                    <xb:point x="0.44457594" y="0.9167683" />  
                    <xb:point x="0.119526625" y="0.9167683" />  
                </xb:coordinates> 
            </xb:location> 
         </xb:header> 
        <xb:body> 
            <xb:content encoding="utf-8">t_FormType t_FormVersion ChangeName 20061128</xb:content>  
         </xb:body> 
    </xb:barcode> 
</xb:scanned_image>
```

## 変換サービスに関する考慮事項 {#considerations}

### バーコードフォームを使用するワークフロー {#workflows-that-use-barcoded-forms}

フォーム作成者は、Designer を使用してインタラクティブなバーコードフォームを作成します。 （「[Designer ヘルプ](https://www.adobe.com/go/learn_aemforms_designer_63_jp)」を参照）。ユーザーがAdobe ReaderまたはAcrobatを使用してバーコードフォームに入力すると、バーコードは自動的に更新され、フォームデータがエンコードされます。

Barcoded Formsサービスは、紙に存在するデータを電子形式に変換する場合に役立ちます。 例えば、バーコードフォームに入力して印刷する場合、印刷されたコピーをスキャンして、Barcoded Formsサービスへの入力として使用できます。

通常、監視フォルダーエンドポイントは、Barcoded Formsサービスを使用するアプリケーションを起動するために使用されます。 例えば、バーコードフォームのTIFF画像やPDF画像を監視フォルダーに保存することができます。 監視フォルダーエンドポイントは、画像をデコード用にサービスに渡します。

### 推奨されるエンコーディングおよびデコーディングの形式 {#recommended-encoding-and-decoding-formats}

バーコードフォームを作成する場合は、バーコード内のデータのエンコーディングにシンプルな区切り形式（タブ区切りなど）を使用することをお勧めします。 また、フィールドの区切り文字にキャリッジリターンは使用しないでください。 Designer では、区切られたエンコーディングを選択できます。区切られたエンコーディングでは、バーコードをエンコードする JavaScript スクリプトが自動的に生成されます。 デコードされたデータは、最初の行にフィールド名と 2 行目に値を持ち、各フィールドの間にタブがあります。

バーコードをデコードする場合は、フィールドの区切りに使用する文字を指定します。 デコード用に指定した文字は、バーコードのエンコードに使用した文字と同じである必要があります。 例えば、推奨されるタブ区切り形式を使用する場合、「Extract to XML」操作では、フィールド区切り文字にデフォルト値の Tab を使用する必要があります。

### ユーザー指定の文字セット {#user-specified-character-sets}

フォーム作成者が Designer を使用してフォームにバーコードオブジェクトを追加する場合、文字エンコーディングを指定できます。 認識されるエンコーディングは、UTF-8、ISO-8859-1、ISO-8859-2、ISO-8859-7、Shift-JIS、KSC-5601、Big-Five、GB-2312、UTF-16 です。 デフォルトでは、すべてのデータはバーコードで UTF-8 としてエンコードされます。

バーコードをデコードする際に、使用する文字セットエンコーディングを指定できます。 すべてのデータが正しくデコードされるようにするには、フォームのデザイン時に指定した文字セットと同じ文字セットを指定します。

### API の制限 {#api-limitations}

BCF API を使用する場合は、次の制限事項を考慮してください。

* ダイナミックフォームはサポートされていません。
* インタラクティブフォームは、統合されていない限り、正しくデコードされません。
* 1-D バーコードには、英数字のみを含める必要があります（サポートされている場合）。 特殊記号を含む 1-D バーコードはデコードされません。

### その他の制限事項 {#other-limitations}

Barcoded Forms サービスを使用するときは、次の制限事項についても考慮する必要があります。

* このサービスは、Adobe ReaderまたはAcrobatを使用して保存された 2D バーコードを含む AcroForms および静的フォームを完全にサポートします。 ただし、1D バーコードの場合は、フォームを統合するか、スキャンされたPDFまたはTIFF文書としてフォームを指定します。
* 動的 XFA フォームは完全にはサポートされていません。 動的フォーム内の 1D および 2D バーコードを適切にデコードするには、フォームを統合するか、スキャンされたPDFまたはTIFFドキュメントとしてフォームを指定します。

また、サービスは前記の制限事項に触れない限り、サポートされているコードが使用されていれば、どのようなバーコードでもデコードできます。インタラクティブなバーコードフォームの作成方法について詳しくは、[Designer ヘルプ](https://www.adobe.com/go/learn_aemforms_designer_63_jp)を参照してください。

## サービスのプロパティを設定します   {#configureproperties}

以下を使用すると、 **AEMFD Barcoded Forms Service** AEMコンソールで、このサービスのプロパティを設定します。 AEM コンソールのデフォルト URL は `https://[host]:'port'/system/console/configMgr` です。

## サービスの使用 {#using}

Barcoded Forms Service は、次の 2 つの API を提供します。

* **[decode](https://helpx.adobe.com/jp/experience-manager/6-3/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode)**：Input PDF ドキュメントまたは TIFF 画像で使用可能なすべてのバーコードをデコードします。入力ドキュメントまたは画像内で使用可能なすべてのバーコードから抽出されたデータを含む別の XML ドキュメントを返します。

* **[extractToXML](https://helpx.adobe.com/jp/experience-manager/6-3/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode)**：decode API を使用してデコードされたデータを XML データに変換します。この XML データは XFA フォームとマージできます。 バーコードごとに 1 つずつ、XML ドキュメントのリストを返します。

### JSP またはサーブレットでの BCF サービスの使用 {#using-bcf-service-with-a-jsp-or-servlets}

次のサンプルコードはドキュメント内のバーコードをデコードして、Output XML をディスクに保存します。

```jsp
<%@ page import="java.util.List,
                com.adobe.fd.bcf.api.BarcodedFormsService,
                com.adobe.fd.bcf.api.CharSet,
                com.adobe.fd.bcf.api.Delimiter,
                com.adobe.fd.bcf.api.XMLFormat,
                com.adobe.aemfd.docmanager.Document,
                javax.xml.transform.Transformer,
                javax.xml.transform.TransformerFactory,
                java.io.StringWriter,
                javax.xml.transform.stream.StreamResult,
                javax.xml.transform.dom.DOMSource,
                javax.servlet.jsp.JspWriter,
                org.apache.commons.lang.StringEscapeUtils" %><%
%><%@taglib prefix="sling" uri="https://sling.apache.org/taglibs/sling/1.0" %><%
%><sling:defineObjects/><%

 // Get reference to BarcodedForms OSGi service.
 // Within an OSGi bundle @Reference annotation 
 // can be used to retrieve service reference

 BarcodedFormsService bcfService = sling.getService(BarcodedFormsService.class);

 // Path to image containing barcodes in AEM repository. 
 // Replace this with path to image in your repository
 String documentPath = "/content/dam/TestImage-010.tif";

 // Create a Docmanager Document object for 
 // the tiff file containing barcode
 // See Docmanager Document javadoc for
 // more details
 Document inputDoc = new Document(documentPath);

 // Invoke decode operation of barcoded forms service 
 // Second parameter is set to true to decode PDF417 barcode symbology
 // See javadoc for details of parameters

 org.w3c.dom.Document result = bcfService.decode(inputDoc, // Input Document Object
                                                    true, 
                                                    false,  
                                                    false,
                                                    false,
                                                    false,
                                                    false,
                                                    false,
                                                    false,
                                                    CharSet.UTF_8);// use UTF-8 character encoding 

 out.println("<h2> Output Returned from decode operation </h2>");
 printDoc(result,out);

 // Invoke extractToXML to convert Carriage 
 // return / Tab delimited data to XML 

 List<org.w3c.dom.Document> listResult = bcfService.extractToXML(result, // w3c document from the output of decode operation
                                                                    Delimiter.Carriage_Return, // Lines are separated using "\r"
                                                                    Delimiter.Tab, // Fields are separated using "\t" 
                                                                    XMLFormat.XDP); // wraps generated XML in <xdp:xdp> packet

 out.println("<h2> Output returned from extractToXML </h2>");
 printDoc(listResult.get(0),out);

%><%!

 // helper function to convert w3c document to string

 String convertToString(org.w3c.dom.Document inputDoc) throws Exception {
   TransformerFactory tf = TransformerFactory.newInstance();
   Transformer tr = tf.newTransformer();
   StringWriter sw = new StringWriter();
   StreamResult sr = new StreamResult(sw);
   tr.transform(new DOMSource(inputDoc), sr);
   return sw.toString();
 }

 // helper function to render XML to response

 void printDoc(org.w3c.dom.Document inputDoc,JspWriter out) throws Exception {
   String escapedString = StringEscapeUtils.escapeHtml(convertToString(inputDoc));
   out.println(escapedString);
 }

%>
```

### AEM Workflows での BCF サービスの使用 {#using-the-bcf-service-with-aem-workflows}

ワークフローから Barcoded Formsサービスを実行することは、JSP/Servlet からサービスを実行する場合と似ています。 唯一の違いは、JSP/Servlet からサービスを実行する場合、ドキュメントオブジェクトは ResourceResolverHelper オブジェクトから ResourceResolver オブジェクトのインスタンスを自動的に取得する点です。 この自動メカニズムは、コードがワークフローから呼び出される場合は機能しません。

ワークフローの場合、ResourceResolver オブジェクトのインスタンスを Document クラスのコンストラクタに明示的に渡します。続いて、Document オブジェクトは渡された ResourceResolver オブジェクトを使用してリポジトリからコンテンツを読み込みます。

以下のサンプルワークフロープロセスでは、ドキュメント内のバーコードをデコードし、結果をディスクに保存します。 コードは ECMAScript で記述され、ドキュメントはワークフローペイロードとして渡されます。

```javascript
/*
 * Imports 
 */
var BarcodedFormsService = Packages.com.adobe.fd.bcf.api.BarcodedFormsService;
var CharSet = Packages.com.adobe.fd.bcf.api.CharSet;

var Document = Packages.com.adobe.aemfd.docmanager.Document;
var File = Packages.java.io.File;
var FileOutputStream = Packages.java.io.FileOutputStream;
var TransformerFactory = Packages.javax.xml.transform.TransformerFactory;
var Transformer = Packages.javax.xml.transform.Transformer;
var StreamResult = Packages.javax.xml.transform.stream.StreamResult;
var DOMSource = Packages.javax.xml.transform.dom.DOMSource;

var ResourceResolverFactory = Packages.org.apache.sling.api.resource.ResourceResolverFactory;

// get reference to BarcodedFormsService
var bcfService = sling.getService(BarcodedFormsService);

/*
 * workflow payload and path to it
 */
var payload = graniteWorkItem.getWorkflowData().getPayload();
var payload_path = payload.toString();

/* Create resource resolver using current session 
 * this resource resolver needs to be passed to Document
 * object constructor when file is to be read from 
 * crx repository. 
 */

/* get ResourceResolverFactory service reference , used 
 * to construct resource resolver
 */
var resourceResolverFactory = sling.getService(ResourceResolverFactory);

var authInfo = {
    "user.jcr.session":graniteWorkflowSession.getSession()
};

var resourceResolver = resourceResolverFactory.getResourceResolver(authInfo);

// Create Document object from payload_path 
var inputDocument = new Document(payload_path, resourceResolver);

// invoke decode operation to decode barcodes in inputDocument
var decodedBarcode = bcfService.decode(inputDocument, true, false, false, false, false, false, false, false, CharSet.UTF_8);

// save decoded barcode data to disk
saveW3CDocument(decodedBarcode, "C:/temp/decoded.xml");

/*
 * Helper function to save W3C Document
 * to a file on disk
 */
function saveW3CDocument(inputDoc, filePath) {
   var tf = TransformerFactory.newInstance();
   var tr = tf.newTransformer();
   var os = new FileOutputStream(filePath);
   var sr = new StreamResult(os);
   tr.transform(new DOMSource(inputDoc), sr);
   os.close();
}
```
