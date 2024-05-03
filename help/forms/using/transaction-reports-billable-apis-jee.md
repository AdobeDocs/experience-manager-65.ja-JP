---
title: トランザクションレポート JEE 上のAEM Formsの課金対象 API。
description: JEE 上のAEM Formsのトランザクションとして計上されるすべての API のリスト。
topic-tags: forms-manager
feature: Transaction Reports
exl-id: dbb22369-c0a2-4cf6-b01b-096b4de13a14
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 54%

---

# JEE 上のAEM Formsのトランザクションレポート請求可能 API {#transaction-reports-billable-apis}

JEE 上のAEM Formsには、ドキュメントを送信、処理、レンダリングするための API がいくつか用意されています。 一部の API はトランザクションとして計上され、それ以外は自由に使用できます。このドキュメントでは、トランザクションとして計上されるすべての API のリストを示します。 課金対象の API が使用される一般的なシナリオを次に示します。

* ある形式から別の形式へのドキュメントの変換
* ダイナミック PDF ドキュメントの統合
* インタラクティブ PDF ドキュメントと別の PDF ドキュメントの結合

請求 API は、ページ数、ドキュメントまたはフォームの長さ、レンダリング済みドキュメントの最終的な形式を考慮しません。
<!--

* **Forms Submitted:** When data is submitted from any type of form created with AEM Forms and the data is submitted to any data storage repository or database is considered form submission. For example, submitting an HTML5 Form, PDF Forms are accounted as forms submitted. Each form in a form set is considered a submission. For example, if a form set has 5 forms, when the form set is submitted, transaction reporting service counts it as 5 submissions.

* **Documents Rendered:** Generating a document by combining a template and data, digitally signing or certifying a document, using a billable document services API for document services, or converting a document from one format to another are accounted as documents rendered.

-->

以下は、JEE で課金対象となる API のリストです。 リストを検索 [osgi 上のAEM Formsの課金対象 API](/help/forms/using/transaction-reports-billable-apis.md).

## 課金対象のドキュメントサービス API {#billable-document-services-apis}

### PDF 生成サービス {#generate-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>説明</td>
   <td>トランザクションレポートカテゴリ</td>
  </tr>
   <tr>
   <td><a>CreatePDF</a></td>
   <td>サポートされているファイルタイプにAdobe PDFを作成します。</td>
   <td>変換<br /> </td>
  </tr>
  <tr>
   <td><a>CreatePDF3</a></td>
   <td>サポートされているファイルタイプにAdobe PDFを作成します。 </td>
   <td>変換<br /> </td>
  </tr>
  <tr>
   <td><a> HtmlToPDF</a></td>
   <td>HTMLファイルをAdobe PDFに変換します。 </td>
   <td>変換<br /> </td>
  </tr>
  <tr>
   <td><a>ExportPDF</a></td>
   <td>サポートされているファイルタイプにPDFを書き出します。 </td>
   <td>変換<br /> </td>
  </tr>
  <tr>
   <td><a>ExportPDF2</a></td>
   <td><p>サポートされているファイルタイプにPDFを書き出します。</p> </td>
   <td>変換<br /> </td>
  </tr>
  <tr>
   <td><a>ExportPDF3</a></td>
   <td>サポートされているファイルタイプにPDFを書き出します。</td>
   <td>変換<br /> </td>
  </tr>
  <tr>
   <td><a>HtmlFileToPDF</a></td>
   <td>HTMLファイルをPDFに変換します。</td>
   <td>変換<br /> </td>
  </tr>
  <tr>
   <td><a>HtmlToPDF2</a></td>
   <td>HTMLファイルをPDFに変換します。</td>
   <td>変換<br /> </td>
  </tr>
  <tr>
   <td><a>OptimizePDF</a></td>
   <td>品質に影響を与えることなく不要なメタデータを削除することによって、ファイルサイズを縮小できるように PDF を最適化します。</td>
   <td>変換<br /> </td>
  </tr>
 </tbody>
</table>

### DocAssurance サービス {#DocAssurance-Service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>説明</td>
   <td>トランザクションレポートカテゴリ</td>
  </tr>
  <tr>
   <td><a>署名/認証</a><br /> </td>
   <td>この API を使用すると、ドキュメントを保護できます。API を使用して、PDFドキュメントに署名し、認証することができます。</td>
   <td>コンバージョン</td>
  </tr>
 </tbody>
</table>


### Distiller サービス {#distiller-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>説明</td>
   <td>トランザクションレポートカテゴリ</td>
  </tr>
  <tr>
  <tr>
   <td><a>CreatePDF</a></td>
   <td>サポートされているファイルタイプから Adobe PDF を作成します。</td>
   <td>コンバージョン</td>
  </tr>
  <tr>
   <td><a>CreatePDF2</a></td>
   <td>サポートされているファイルタイプから Adobe PDF を作成します。</td>
   <td>コンバージョン</td>
  </tr>
 </tbody>
</table>

<!--

### Document of Record Service (DoR Service) {#document-of-record-service-dor-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/aemds/guide/addon/dor/DoRService.html#render-com.adobe.aemds.guide.addon.dor.DoROptions-" target="_blank">render</a></td>
   <td>Invokes the specified render method to generate a document of record using provided parameters.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
 </tbody>
</table>

-->

### Output サービス {#output-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>説明</td>
   <td>トランザクションレポートカテゴリ</td>
  </tr>
  <tr>
   <td><a>generateOutput</a></td>
   <td>データとテンプレートを結合して、PDF ドキュメントを作成します。</td>
   <td>レンダリング済みドキュメント</td>
  </tr>
  <tr>
   <td><a>generatePDFOutput</a></td>
   <td>データとテンプレートを結合して、PDF ドキュメントを作成します。</td>
   <td>レンダリング済みドキュメント</td>
  </tr>
  <tr>
   <td><a>generatePDFOutput2</a></td>
   <td>データとテンプレートを結合して、PDF ドキュメントを作成します。</td>
   <td>レンダリング済みドキュメント</td>
  </tr>
  <tr>
   <td><a>generatePrintedOutput</a></td>
   <td>XDP および PDF ドキュメントを PostScript（PS）、Printer Command Language（PCL）および ZPL ファイル形式に変換します。 </td>
   <td>レンダリング済みドキュメント</td>
  </tr>
  <tr>
   <td><a>generatePrintedOutput2</a></td>
   <td>XDP および PDF ドキュメントを PostScript（PS）、Printer Command Language（PCL）および ZPL ファイル形式に変換します。 </td>
   <td>レンダリング済みドキュメント</td>
  </tr>
  <tr>
   <td><a>transformPDF</a></td>
   <td>XDP および PDF ドキュメントのセットを、PostScript（PS）、Printer Command Language（PCL）および ZPL の各ファイル形式に変換します。 </td>
   <td>ドキュメントの変換</td>
  </tr>
 </tbody>
</table>

<!-- ### Forms Service {#forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#renderPDFForm-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.PDFFormRenderOptions-" target="_blank">renderPDFForm</a></td>
   <td>Renders PDF Form from XDP templates. The XDP templates are created in Forms Designer.</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#exportData-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.DataFormat-" target="_blank">exportData</a></td>
   <td>Extracts data from a PDF Form or XDP templates</td>
   <td>Documents Processed</td>
   <td> </td>
  </tr>
 </tbody>
</table>

-->

### Convert PDF サービス {#convert-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>説明</td>
   <td>トランザクションレポートカテゴリ</td>
  </tr>
  <tr>
   <td><a>toImage2</a></td>
   <td>PDF ドキュメントを画像ドキュメントのリストに変換します。サポートされる画像形式は、JPEG、JPEG2K、PNG、TIFF です。</td>
   <td>ドキュメントの変換</td>
  </tr>
  <tr>
   <td><a>toPS2</a></td>
   <td>オプション仕様で指定した PDF を使用して、フラットオプションファイルを PostScript 形式に変換します。</td>
   <td>ドキュメントの変換</td>
  </tr>
  <tr>
   <td><a>toSwf</a></td>
   <td>オプション仕様で指定されたオプションを使用して、フラットPDFファイルをSWFフォーマットに変換します。</td>
   <td>ドキュメントの変換</td>
  </tr>
 </tbody>
</table>

### Barcoded Forms サービス {#barcoded-forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>説明</td>
   <td>トランザクションレポートカテゴリ</td>
  </tr>
  <tr>
   <td><a>Decode</a></td>
   <td>Document オブジェクト内のすべてのバーコードをデコードし、バーコードから取得されたデータを含む org.w3c.dom.Document オブジェクトを返します。</td>
   <td>ドキュメントの変換</td>
  </tr>
 </tbody>
</table>

### Assembler サービス {#assembler-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>説明</td>
   <td>トランザクションレポートカテゴリ</td>
  </tr>
  <tr>
   <td><a>呼び出し</a></td>
   <td>指定した DDX ドキュメントを実行し、結果のドキュメントを含む AssemblerResult オブジェクトを返します。 </td>
   <td>ドキュメントの変換</td>
  </tr>
  <tr>
   <td><a>invokeDDX</a></td>
   <td>指定した DDX ドキュメントを実行し、結果のドキュメントを含む AssemblerResult オブジェクトを返します。 </td>
   <td>ドキュメントの変換</td>
  </tr>
  <tr>
   <td><a>invokeOneDocument</a></td>
   <td>指定したオプションを使用して、指定したドキュメントを PDF/A に変換します。</td>
   <td>ドキュメントの変換</td>
  </tr>
  <tr>
   <td><a>invokeDDXOneDocument</a></td>
   <td>指定したオプションを使用して、指定したドキュメントを PDF/A に変換します。</td>
   <td>ドキュメントの変換</td>
  </tr>
  <tr>
   <td><a>toPDFA</a></td>
   <td>指定したオプションを使用して、指定したドキュメントを PDF/A に変換します。</td>
   <td>ドキュメントの変換</td>
  </tr>
 </tbody>
</table>

次の操作を 1 つ以上実行すると、呼び出し API の使用がトランザクションとしてカウントされます。
1. 非 PDF 形式から PDF 形式への変換。例えば、XDP 形式からPDF形式への変換などです。<!-- catering to both interactive and non-interactive forms of communication, and the conversion from Word to PDF.-->
1. PDF 形式から PDF/A 形式への変換。
1. PDF 形式から非 PDF 形式への変換。例としては、PDF 形式から画像形式への変換、または PDF 形式からテキスト形式への変換があります。

>[!NOTE]
>
>* Assembler サービスの invoke API は、入力に応じて別のサービスの課金対象 API を内部的に呼び出すことができます。では、 `invoke API` なし、単一または複数のトランザクションとして計上できます。 カウントされるトランザクションの数は、入力と呼び出される内部 API によって異なります。
>* 次のような Assembler サービスを使用して生成された 1 つのPDFドキュメント `invoke` および `invokeDDX`、は、0、単一、複数のトランザクションのいずれかとして計上される可能性があります。 カウントされるトランザクションの数は、指定されたによって異なります <!--DDX--> コード。

<!--
### PDF Utility Service  {#pdf-utility-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a>convertPDFtoXDP</a></td>
   <td>Converts a PDF document into an XDP file. For a PDF document to be successfully converted to an XDP file, the PDF document must contain an XFA stream in the AcroForm dictionary.</td>
   <td>Documents Conversion</td>
   <td> </td>
  </tr>
 </tbody>
</table>

-->

## 課金対象のデータキャプチャ API {#billable-data-capture-apis}

<!--All the submission events of Forms, HTML5 Forms, and form set are accounted as transactions. By default, submission of a PDF Form is not accounted as a transaction. Use the provided [transaction recorder API](record-transaction-custom-implementation.md) to record a PDF Forms submission as a transaction.-->

<!--
### Adaptive Forms {#adaptive-forms}

<table>
 <tbody>
  <tr>
   <td><p>Use Case</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Submitting an adaptive form</td>
   <td>Submits an adaptive form to configured submit action. </td>
   <td>Forms Submitted</td>
   <td>
    <ul>
     <li>Successful submissions account for single or two transactions. The number of transactions counted depends upon the type of submit action used for submission. For example, sending PDF through email submit action accounts for two counts of transactions. One transaction for form submission and another for PDF generated using the Document of Record (DOR) service. </li>
     <li>Using the adaptive form within an adaptive form (Adaptive form formset) accounts only single transaction. You can have any number of adaptive forms within an adaptive form.</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

-->

<!--### HTML5 Forms {#html-forms}

<table>
 <tbody>
  <tr>
   <td><p>Use Case</p> </td>
   <td>Description </td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Submitting an HTML5 Form</td>
   <td>Submits an HTML5 Form to submit URL configured in the form.</td>
   <td>Forms Submitted</td>
   <td> </td>
  </tr>
 </tbody>
</table>

-->

### Forms {#form-set}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>説明</td>
   <td>トランザクションレポートカテゴリ</td>
  </tr>
  <tr>
   <td>exportData</td>
   <td>フォームを送信します</td>
   <td>送信済みフォーム</td>
  </tr>
  <tr>
   <td>exportData2</td>
   <td>フォームを送信します</td>
   <td>送信済みフォーム</td>
  </tr>
  <tr>
   <td>renderForm</td>
   <td>フォームを送信します</td>
   <td>レンダリング済みForms</td>
  </tr>
  <tr>
   <td>renderHTMLForm</td>
   <td>フォームを送信します</td>
   <td>レンダリング済みForms</td>
  </tr>
  <tr>
   <td>renderHTMLForm2</td>
   <td>フォームを送信します</td>
   <td>レンダリング済みForms</td>
  </tr>
  <tr>
   <td>renderPDFForm</td>
   <td>フォームを送信します</td>
   <td>レンダリング済みForms</td>
  </tr>
  <tr>
   <td>renderPDFForm2</td>
   <td>フォームを送信します</td>
   <td>レンダリング済みForms</td>
  </tr>
  <tr>
   <td>renderPDFFormWithUsageRights</td>
   <td>フォームを送信します</td>
   <td>レンダリング済みForms</td>
  </tr>
 </tbody>
</table>

<!-- ## Billable Interactive Communication and Form-centric AEM Workflows on OSGi APIs {#billable-interactive-communication-and-form-centric-aem-workflows-on-osgi-apis}

Assign task and document services steps of Form-centric AEM Workflows on OSGi and all the renditions of interactive communication and are accounted as transactions. Previewing an interactive communication on the author instance and previewing on the publish instance using Agent UI are not accounted as transactions. If a workflow step accounts a transaction and the workflow fails to complete, the transaction count is not reversed.

<!--

### Interactive Communication - Web Channel {#interactive-communication-web-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Rendering a web channel</td>
   <td>Opens the web version of an interactive communication.</td>
   <td>Documents Rendered</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

### Interactive Communication - Print Channel {#interactive-communication-print-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>Description</td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/ccm/channels/print/api/model/PrintChannel.html" target="_blank">render</a> (convert to PDF)</td>
   <td>Generates the PDF version of an interactive communication.</td>
   <td>Documents Rendered</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

-->


<!--
### Form-centric AEM Workflows on OSGi  {#form-centric-aem-workflows-on-osgi}

<table>
 <tbody>
  <tr>
   <td><p>Use case</p> </td>
   <td>Transaction report category</td>
   <td>Additional Information</td>
  </tr>
  <tr>
   <td>Submitting an Assign Task step</td>
   <td>Forms Submitted</td>
   <td>
    <div>
    </div> </td>
  </tr>
  <tr>
   <td>Submitting a workflow application startpoint </td>
   <td>Forms Submitted</td>
   <td> </td>
  </tr>
  <tr>
   <td>Submitting an interactive communication (Print Channel) from the Agent UI to a workflow</td>
   <td>Documents Rendered</td>
   <td> </td>
  </tr>
 </tbody>
</table>

-->


<!--

WILL ADD THIS ONE - 

## Recording billable APIs as transactions for custom code {#recording-billable-apis-as-transactions-for-custom-code}

Actions like submitting a PDF Form, using Agent UI to preview an interactive communication, using non-standard form submission, and custom implementations are not accounted as transactions. AEM Forms provides an API to record such actions as transactions. You can call the API from your custom implementations to [record a transaction](/help/forms/using/record-transaction-custom-implementation.md).

## Related Articles {#related-articles}

* [Transaction Reports Overview](../../forms/using/transaction-reports-overview.md)
* [Viewing and Understanding a Transaction Reports](../../forms/using/viewing-and-understanding-transaction-reports.md)
* [Record a transaction for custom implementations](/help/forms/using/record-transaction-custom-implementation.md)

-->

## 関連記事

* [JEE 上のAEM Formsのトランザクションレポートの有効化と表示](/help/forms/using/transaction-report-overview-jee.md)
* [JEE 上のAEM Formsのカスタムコンポーネント API のトランザクションの記録](/help/forms/using/record-transaction-custom-component-jee.md)
