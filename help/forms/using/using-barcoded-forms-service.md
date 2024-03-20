---
title: Barcoded Forms サービス
description: AEM Forms Barcoded Forms サービスを使用して、バーコードの電子画像からデータを抽出します。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
docset: aem65
feature: Document Services
exl-id: d4b5cacd-0bac-48b5-a8a6-0f58883136d7
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 100%

---

# Barcoded Forms サービス{#barcoded-forms-service}

## 概要 {#overview}

Barcoded Forms サービスは、バーコードの電子画像からデータを抽出するサービスです。このサービスは、入力として 1 つまたは複数のバーコードを含んだ TIFF ファイルや PDF ファイルを受け取り、バーコードデータを抽出します。バーコード データは、XML、区切り文字列、JavaScript で作成されたカスタム形式など、様々な方法で形式設定できます。

Barcoded Forms サービスは、スキャンされた TIFF または PDF ドキュメントとして提供される以下の&#x200B;**二次元**&#x200B;コードをサポートします。

* PDF417
* データマトリックス
* QR コード

このサービスはまた、スキャンされた TIFF または PDF ドキュメントとして提供される以下の&#x200B;**一次元**&#x200B;コードもサポートします。

* Codabar
* Code128
* コード 3 / 9
* EAN13
* EAN8

Barcoded Forms サービスを使用して、次のタスクを実行できます。

* バーコード画像（TIFF または PDF）からバーコードデータを抽出します。データは区切り文字で区切られたテキストとして保存されます。
* 区切り文字で区切られたテキストデータを XML（XDP または XFDF）に変換します。XML データは、区切り文字付きテキストよりも解析が簡単です。また、XDP または XFDF 形式のデータは、AEM フォームの他のサービスの入力として使用できます。

画像内のバーコードごとに、Barcoded Forms サービスはバーコードを見つけてデコードし、データを抽出します。バーコードデータは、（必要に応じてエンティティエンコードを使用して）XML ドキュメントのコンテンツ要素として返されます。例えば、次の図は、2 つのバーコードを含んだフォームをスキャンした TIFF 画像です

![例](assets/example.png)

Barcoded Forms サービスは、バーコードのデコード後、次の XML ドキュメントを返します。

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

## このサービスに関する考慮事項 {#considerations}

### Barcoded Forms を使用するワークフロー {#workflows-that-use-barcoded-forms}

フォーム作成者は、Designer を使用してインタラクティブなバーコードフォームを作成します。（「[Designer ヘルプ](https://www.adobe.com/go/learn_aemforms_designer_63_jp)」を参照）。ユーザーが Adobe Reader または Acrobat でバーコードフォームに入力すると、バーコードは自動的に更新され、フォームデータがエンコードされます。

Barcoded Forms サービスは、紙面上のデータを電子的なフォーマットに変換させる場合に役立ちます。例えば、バーコードフォームに記入して印刷した後で、その印刷出力をスキャンし、Barcoded Forms サービスへの入力として使用できます。

通常、監視フォルダーのエンドポイントは、Barcoded Forms サービスを使用するアプリケーションを起動するときに使用されます。例えば、ドキュメントスキャナーは、Barcoded Forms の TIFF または PDF 画像を監視フォルダーに保存できます。監視フォルダーのエンドポイントは、デコードのために画像をサービスに渡します。

### 推奨されるエンコードおよびデコードの形式 {#recommended-encoding-and-decoding-formats}

バーコードフォームを作成する場合、バーコードのデータをエンコードするときに単純な区切り形式（タブ区切りなど）を使用することをお勧めします。また、フィールド区切り文字としてキャリッジリターンは使用しないようにしてください。Designer には、バーコードをエンコードするための JavaScript スクリプトを自動的に生成する、区切り文字で区切られたエンコードの選択が用意されています。デコードされたデータの 1 行目はフィールド名、2 行目はその値であり、各フィールドの間にはタブがあります。

バーコードのデコード時には、フィールドの区切りに使用する文字を指定します。デコード用に指定する文字は、バーコードのエンコーディングで使用された文字と同じであることが必要です。例えば、推奨されるタブ区切り形式が使用された場合、XML 抽出操作でも、フィールド区切り文字にデフォルト値の Tab を使用する必要があります。

### ユーザー指定の文字セット {#user-specified-character-sets}

フォームの作成者は、Designer を使用してバーコードオブジェクトをそのフォームに追加するときに、文字エンコードを指定できます。認識可能なエンコードは、UTF-8、ISO-8859-1、ISO-8859-2、ISO-8859-7、Shift-JIS、KSC-5601、Big-Five、GB-2312、UTF-16 です。デフォルトでは、バーコード内のすべてのデータが UTF-8 としてエンコードされます。

バーコードのデコード時には、使用する文字セットエンコーディングを指定できます。すべてのデータが正常にデコードされるようにするには、フォームのデザイン時にフォームの作成者が指定した文字セットと同じ文字セットを指定してください。

### API の制限事項 {#api-limitations}

BCF API を使用するときは、次の制限事項に考慮してください。

* 動的フォームはサポートされていません。
* インタラクティブフォームは、フラット化されているもの以外は正しくデコードされません。
* 1-D バーコード（サポートされている場合）に英数字以外の文字を含めることはできません。特殊記号を含んだ 1-D バーコードはデコードされません。

### その他の制限事項 {#other-limitations}

Barcoded Forms サービスを使用するときは、次の制限事項についても考慮する必要があります。

* このサービスは、Adobe Reader または Acrobat を使用して保存された、2D バーコードを含む AcroForms および静的フォームを完全にサポートします。ただし、1D バーコードの場合は、フォームを統合するか、フォームを変換してスキャンされた PDF または TIFF ドキュメントとして提供してください。
* 動的 XFA フォームは完全にサポートされているわけではありません。動的フォーム内の 1D および 2D バーコードを正しくデコードするには、フォームを統合するか、フォームを変換してスキャンされた PDF または TIFF ドキュメントとして提供してください。

また、サービスは前記の制限事項に触れない限り、サポートされているコードが使用されていれば、どのようなバーコードでもデコードできます。インタラクティブなバーコードフォームの作成方法について詳しくは、[Designer ヘルプ](https://www.adobe.com/go/learn_aemforms_designer_63_jp)を参照してください。

## サービスのプロパティの設定 {#configureproperties}

AEM コンソールにある **AEMFD Barcoded Forms サービス**&#x200B;を使用すると、このサービスのプロパティを設定できます。AEM コンソールのデフォルト URL は `https://[host]:'port'/system/console/configMgr` です。

## サービスの使用 {#using}

Barcoded Forms サービスには次の 2 つの API があります。

* **[decode](https://helpx.adobe.com/jp/experience-manager/6-3/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode)**：Input PDF ドキュメントまたは TIFF 画像で使用可能なすべてのバーコードをデコードします。入力ドキュメントまたは画像内で使用可能なすべてのバーコードから抽出されたデータを含む別の XML ドキュメントを返します。

* **[extractToXML](https://helpx.adobe.com/jp/experience-manager/6-3/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode)**：decode API を使用してデコードされたデータを XML データに変換します。この XML データは XFA フォームと結合できます。バーコードごとに 1 つずつ XML ドキュメントのリストを返します。

### JSP またはサーブレットを使用した BCF サービスの使用 {#using-bcf-service-with-a-jsp-or-servlets}

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

### AEM ワークフローを使用した BCF サービスの使用 {#using-the-bcf-service-with-aem-workflows}

ワークフローから Barcoded Forms サービスを実行することは、JSP またはサーブレットからサービスを実行することに似ています。唯一の相違点は、JSP またはサーブレットからこのサービスを実行する場合、ドキュメントが ResourceResolverHelper オブジェクトから ResourceResolver オブジェクトのインスタンスを自動で取得する点です。この自動メカニズムは、コードがワークフローから呼び出される場合は機能しません。

ワークフローの場合、ResourceResolver オブジェクトのインスタンスを Document クラスのコンストラクタに明示的に渡します。続いて、Document オブジェクトは渡された ResourceResolver オブジェクトを使用してリポジトリからコンテンツを読み込みます。

次のサンプルワークフロープロセスは、ドキュメント内のバーコードをデコードして結果をディスクに保存します。コードは ECMAScript で記述され、ドキュメントはワークフローペイロードとして渡されます。

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
