---
title: トランザクションレポート請求可能API
seo-title: トランザクションレポート請求可能API
description: トランザクションとして計上されるすべてのAPIのリスト
seo-description: トランザクションとして計上されるすべてのAPIのリスト
uuid: d2f38ae4-75df-426f-af34-52ae6fb324f3
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 929a298d-7f22-487f-bf7d-8ab2556d0d81
docset: aem65
translation-type: tm+mt
source-git-commit: 13016df927448d93af86899f746199e1815fdfe7
workflow-type: tm+mt
source-wordcount: '1963'
ht-degree: 9%

---


# トランザクションレポート請求可能API{#transaction-reports-billable-apis}

AEM Formsは、フォームの送信、プロセスドキュメント、レンダリングドキュメントのためのいくつかのAPIを提供しています。 一部のAPIはトランザクションとして計上され、その他のAPIは無料で使用できます。 このドキュメントは、トランザクションレポートでトランザクションとして計上されるすべてのAPIのリストを提供します。 課金対象のAPIが使用される一般的なシナリオを以下に示します。

* アダプティブフォーム、HTML5フォーム、フォームセットの送信
* インタラクティブな通信の印刷版またはWeb版のレンダリング
* ドキュメントの形式間の変換
* ダイナミックPDFドキュメントの統合
* レコードのドキュメントの生成
* インタラクティブPDFドキュメントと別のPDFドキュメントの結合
* AEMワークフローのタスクの割り当て手順とドキュメントサービス手順の使用
* アダプティブフォーム内でのアダプティブフォームの使用

課金APIは、ページ数、ドキュメントやフォームの長さ、レンダリングされたドキュメントの最終的な形式を考慮しません。 取引レポートでは、取引が次の2つのカテゴリに分割されます。ドキュメントがレンダリングされ、Formsが送信されました。

* **Forms提出：** AEM Formsで作成された任意の種類のフォームからデータが送信され、そのデータが任意のデータストレージリポジトリまたはデータベースに送信される場合、フォーム送信と見なされます。 例えば、アダプティブフォーム、HTML5フォーム、PDF forms、フォームセットの送信は、フォーム送信と見なされます。 フォームセット内の各フォームは送信と見なされます。 例えば、フォームセットに5つのフォームが含まれる場合、フォームセットが送信されると、トランザクションレポートサービスはフォームセットを5件の送信としてカウントします。

* **レンダリングされたドキュメント:** テンプレートとデータを組み合わせてドキュメントを生成し、ドキュメントに電子署名または認証し、ドキュメントサービスの請求可能なドキュメントサービスAPIを使用したり、ある形式から別の形式にドキュメントを変換したりして、をドキュメントとしてカウントします。

>[!NOTE]
>
>トランザクションレポートUIに3つのカテゴリが表示されます。Formsが送信、ドキュメントがレンダリングされ、ドキュメントが処理されました。 「レンダリング済み」と「処理済みのドキュメント」の両方が、「レンダリング済みのドキュメント」として計上されます。

## 請求対象ドキュメントサービスAPI {#billable-document-services-apis}

### Generate PDF Service {#generate-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>説明</td>
   <td>トランザクションレポートカテゴリ</td>
   <td>追加情報</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#createPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF</a></td>
   <td>サポートされるファイルタイプからAdobe PDFを作成します。</td>
   <td>処理済みドキュメント</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td>
   <td>サポートされるファイルタイプからAdobe PDFを作成します。</td>
   <td>処理済みドキュメント</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF</a></td>
   <td>Adobe PDFを対応ファイル形式に変換します。 </td>
   <td>処理済みドキュメント<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF2</a></td>
   <td>Adobe PDFを対応ファイル形式に変換します。 </td>
   <td>処理済みドキュメント<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF3</a></td>
   <td>Adobe PDFを対応ファイル形式に変換します。 </td>
   <td>処理済みドキュメント<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlFileToPdf-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-">htmlFileToPdf</a></td>
   <td><p>HTMLページからPDFを作成します。</p> </td>
   <td>処理済みドキュメント<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf</a></td>
   <td>HTMLページを指すURLからPDFを作成します。</td>
   <td>処理済みドキュメント<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf2-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf2</a></td>
   <td>HTMLページを指すURLからPDFを作成します。</td>
   <td>処理済みドキュメント<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#optimizePDF-com.adobe.aemfd.docmanager.Document-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">optimizePDF</a></td>
   <td>画質に影響を与えることなく不要なメタデータを削除し、PDFを最適化してファイルサイズを縮小します。</td>
   <td>処理済みドキュメント<br /> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Distiller Service {#distiller-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>説明</td>
   <td>トランザクションレポートカテゴリ</td>
   <td>追加情報</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/DistillerService.html#createPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF</a><br /> </td>
   <td>サポートされるファイルタイプからAdobe PDFを作成します。</td>
   <td>処理済みドキュメント</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/DistillerService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td>
   <td>サポートされるファイルタイプからAdobe PDFを作成します。</td>
   <td>処理済みドキュメント</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### レコードサービス（DoRサービス）のドキュメント {#document-of-record-service-dor-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>説明</td>
   <td>トランザクションレポートカテゴリ</td>
   <td>追加情報</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/aemds/guide/addon/dor/DoRService.html#render-com.adobe.aemds.guide.addon.dor.DoROptions-" target="_blank">render</a></td>
   <td>指定したレンダリングメソッドを呼び出して、指定したパラメーターを使用してレコードのドキュメントを生成します。</td>
   <td>処理済みドキュメント</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Output サービス {#output-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>説明</td>
   <td>トランザクションレポートカテゴリ</td>
   <td>追加情報</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePDFOutput-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PDFOutputOptions-" target="_blank">generatePDFOutput</a></td>
   <td>データとテンプレートをマージしてPDFドキュメントを作成します。</td>
   <td>処理済みドキュメント</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePDFOutput-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PDFOutputOptions-" target="_blank">generatePDFOutput</a></td>
   <td>データとテンプレートをマージしてPDFドキュメントを作成します。</td>
   <td>処理済みドキュメント</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePDFOutputBatch-java.util.Map-java.util.Map-com.adobe.fd.output.api.PDFOutputOptions-com.adobe.fd.output.api.BatchOptions-" target="_blank">generatePDFOutputBatch</a></td>
   <td>データとテンプレートをマージして、PDFドキュメントのセットを作成します。</td>
   <td>処理済みドキュメント</td>
   <td> generatePDFOutputBatch APIは、フォームテンプレートとレコードを組み合わせてPDFを生成します。 レコードのバッチを処理する場合、トランザクションレポートサービスは各レコードを個別のPDFレンディションとしてカウントします。 <br> getGenerateManyFiles <a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--"></a> フラグを使用すると、複数のレンディションを単一のPDFファイルに組み合わせることができます。 フラグのステータスに関係なく、サービスは各レコードを個別のPDFレンディションとしてカウントします。 </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutput-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PrintedOutputOptions-" target="_blank">generatePrintedOutput</a></td>
   <td>XDPおよびPDFドキュメントをPostScript(PS)、Printer Command Language(PCL)およびZPLファイル形式に変換します。 </td>
   <td>処理済みドキュメント</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutput-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PrintedOutputOptions-" target="_blank">generatePrintedOutput</a></td>
   <td>XDPおよびPDFドキュメントをPostScript(PS)、Printer Command Language(PCL)およびZPLファイル形式に変換します。 </td>
   <td>処理済みドキュメント</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutputBatch-java.util.Map-java.util.Map-com.adobe.fd.output.api.PrintedOutputOptions-com.adobe.fd.output.api.BatchOptions-" target="_blank">generatePrintedOutputBatch</a></td>
   <td>XDPおよびPDFドキュメントのセットを、PostScript(PS)、Printer Command Language(PCL)およびZPLファイル形式のセットに変換します。 </td>
   <td>処理済みドキュメント</td>
   <td> generatePDFOutputBatch APIは、フォームテンプレートとレコードを組み合わせてPDFを生成します。 レコードのバッチを処理する場合、トランザクションレポートサービスは各レコードを個別のPDFレンディションとしてカウントします。 <br> getGenerateManyFiles <a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--"></a> フラグを使用すると、複数のレンディションを単一のPDFファイルに組み合わせることができます。 フラグのステータスに関係なく、サービスは各レコードを個別のPDFレンディションとしてカウントします。 </td>
  </tr>
 </tbody>
</table>

### Forms サービス {#forms-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>説明</td>
   <td>トランザクションレポートカテゴリ</td>
   <td>追加情報</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#renderPDFForm-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.PDFFormRenderOptions-" target="_blank">｢renderPDFForm｣操作</a></td>
   <td>XDPテンプレートからPDFフォームをレンダリングします。 XPテンプレートは、Formsデザイナで作成されます。</td>
   <td>処理済みドキュメント</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#exportData-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.DataFormat-" target="_blank">exportData</a></td>
   <td>PDFフォームまたはXDPテンプレートからデータを抽出します</td>
   <td>処理済みドキュメント</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Convert PDF Service {#convert-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>説明</td>
   <td>トランザクションレポートカテゴリ</td>
   <td>追加情報</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage-com.adobe.aemfd.docmanager.Document-com.adobe.fd.cpdf.api.ToImageOptionsSpec-" target="_blank">toImage</a></td>
   <td>PDFドキュメントを画像ドキュメントのリストに変換します。 サポートされる画像形式は、JPEG、JPEG 2000、PNGおよびTIFFです。</td>
   <td>処理済みドキュメント</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage-com.adobe.aemfd.docmanager.Document-com.adobe.fd.cpdf.api.ToImageOptionsSpec-" target="_blank">toPS</a></td>
   <td>option specで指定したオプションを使用して、フラットPDFファイルをPostScript形式に変換します。</td>
   <td>処理済みドキュメント</td>
   <td> </td>
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
   <td>追加情報</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode-com.adobe.aemfd.docmanager.Document-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-com.adobe.fd.bcf.api.CharSet-" target="_blank">decode</a></td>
   <td>ドキュメントオブジェクト内のすべてのバーコードをデコードし、org.w3c.dom.barcodeオブジェクトを返します。このオブジェクトには、バーコードから取得したデータが含まれます。</td>
   <td>処理済みドキュメント</td>
   <td> </td>
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
   <td>追加情報</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#invoke-com.adobe.aemfd.docmanager.Document-java.util.Map-com.adobe.fd.assembler.client.AssemblerOptionSpec-">呼び出し</a></td>
   <td>指定したDDXドキュメントを実行し、結果のドキュメントを含む <a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/client/AssemblerResult.html">AssemblerResult</a> オブジェクトを返します。 </td>
   <td>処理済みドキュメント</td>
   <td>次の工程は取引として計上されません。
    <ul>
     <li>パッケージまたはポートフォリオの作成</li>
     <li>複数のXDPのステッチ </li>
    </ul> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#invoke-com.adobe.aemfd.docmanager.Document-java.util.Map-com.adobe.fd.assembler.client.AssemblerOptionSpec-" target="_blank">呼び出し</a></td>
   <td>指定したDDXドキュメントを実行し、結果のドキュメントを含む <a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/client/AssemblerResult.html">AssemblerResult</a> オブジェクトを返します。 </td>
   <td>処理済みドキュメント</td>
   <td>PDF Generator、Forms、Outputの各サービスでサポートされるすべての入力ファイル形式で、Assemblerサービスは、出力ファイル形式としてこれらのすべての形式をサポートします。 </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#toPDFA-com.adobe.aemfd.docmanager.Document-com.adobe.fd.assembler.client.PDFAConversionOptionSpec-">toPDFA</a></td>
   <td>指定したドキュメントをPDF/Aに変換します。</td>
   <td>処理済みドキュメント</td>
   <td> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* Assemblerサービスの呼び出しAPIは、入力に応じて、別のサービスの請求可能なAPIを内部的に呼び出すことができます。 したがって、呼び出しAPIは、なし、単一または複数のトランザクションと見なすことができます。 カウントされるトランザクションの数は、入力APIと呼び出される内部APIによって異なります。
>* Assemblerサービスを使用して生成された単一のPDFドキュメントは、なし、単一または複数のトランザクションと見なすことができます。 カウントされるトランザクションの数は、指定されたDDXコードによって異なります。

>



### PDF Utilityサービス  {#pdf-utility-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>説明</td>
   <td>トランザクションレポートカテゴリ</td>
   <td>追加情報</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/pdfutility/services/PDFUtilityService.html#convertPDFtoXDP-com.adobe.aemfd.docmanager.Document-" target="_blank">convertPDFtoXDP</a></td>
   <td>PDFドキュメントをXDPファイルに変換します。 PDFドキュメントをXDPファイルに正しく変換するには、PDFドキュメントにAcroFormディクショナリ内のXFAストリームが含まれている必要があります。</td>
   <td>処理済みドキュメント</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## 請求対象データ取得API {#billable-data-capture-apis}

アダプティブフォーム、HTML5Forms、フォームセットの送信イベントはすべて、トランザクションと見なされます。 デフォルトでは、PDFフォームの送信はトランザクションとして考慮されません。 提供されている [トランザクションレコーダーAPI](record-transaction-custom-implementation.md) 。PDF formsの送信をトランザクションとして記録します。

### アダプティブフォーム {#adaptive-forms}

<table>
 <tbody>
  <tr>
   <td><p>使用例</p> </td>
   <td>説明</td>
   <td>トランザクションレポートカテゴリ</td>
   <td>追加情報</td>
  </tr>
  <tr>
   <td>アダプティブフォームの送信</td>
   <td>アダプティブフォームを設定済みの送信アクションに送信します。 </td>
   <td>送信済みフォーム</td>
   <td>
    <ul>
     <li>送信が成功すると、1つまたは2つのトランザクションが考慮されます。 カウントされるトランザクションの数は、送信に使用される送信アクションのタイプによって異なります。 例えば、電子メール送信アクションを使用してPDFを送信すると、2つのトランザクションのカウントが考慮されます。 フォーム送信用のトランザクションと、レコードのドキュメント(DOR)サービスを使用して生成されたPDF用のトランザクションです。 </li>
     <li>アダプティブフォーム（アダプティブフォームフォームセット）内でアダプティブフォームを使用すると、単一のトランザクションのみが考慮されます。 アダプティブフォーム内には、任意の数のアダプティブフォームを含めることができます。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### HTML5 のフォーム {#html-forms}

<table>
 <tbody>
  <tr>
   <td><p>使用例</p> </td>
   <td>説明 </td>
   <td>トランザクションレポートカテゴリ</td>
   <td>追加情報</td>
  </tr>
  <tr>
   <td>HTML5フォームの送信</td>
   <td>HTML5フォームを送信して、フォームに設定されたURLを送信します。</td>
   <td>送信済みフォーム</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### フォームセット {#form-set}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>説明</td>
   <td>トランザクションレポートカテゴリ</td>
   <td>追加情報</td>
  </tr>
  <tr>
   <td>フォームセットの送信</td>
   <td>フォームセットを、フォームセットに設定されている送信URLに送信します。</td>
   <td>送信済みフォーム</td>
   <td>
    <ul>
     <li>アダプティブフォーム（アダプティブフォームフォームセット）内でアダプティブフォームを使用すると、単一のトランザクションのみが考慮されます。 アダプティブフォーム内には、任意の数のアダプティブフォームを含めることができます。</li>
     <li>HTML5Formsフォームセット内のすべてのフォームは、個別のトランザクションとしてアカウントされます。 </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## OSGi APIに関する請求対象となるインタラクティブコミュニケーションおよびフォーム中心のAEMワークフロー {#billable-interactive-communication-and-form-centric-aem-workflows-on-osgi-apis}

OSGi上でフォーム中心のAEMワークフローのタスクおよびドキュメントサービスの手順を割り当て、インタラクティブ通信のすべてのレンディションを割り当て、トランザクションと見なします。 オーサーインスタンスでインタラクティブな通信をプレビューし、エージェントUIを使用してパブリッシュインスタンスでプレビューする場合、トランザクションとして考慮されません。 ワークフローステップでトランザクションが計算され、ワークフローの完了に失敗した場合、トランザクション数は取り消されません。

### インタラクティブ通信 - Web チャネル {#interactive-communication-web-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>説明</td>
   <td>トランザクションレポートカテゴリ</td>
   <td>追加情報</td>
  </tr>
  <tr>
   <td>Webチャネルのレンダリング</td>
   <td>インタラクティブ通信のWebバージョンを開きます。</td>
   <td>レタリング済みドキュメント</td>
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
   <td>説明</td>
   <td>トランザクションレポートカテゴリ</td>
   <td>追加情報</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/ccm/channels/print/api/model/PrintChannel.html" target="_blank">render</a> （PDFに変換）</td>
   <td>インタラクティブ通信のPDFバージョンを生成します。</td>
   <td>レタリング済みドキュメント</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

### OSGi 上のフォームベース AEM ワークフロー  {#form-centric-aem-workflows-on-osgi}

<table>
 <tbody>
  <tr>
   <td><p>使用例</p> </td>
   <td>トランザクションレポートカテゴリ</td>
   <td>追加情報</td>
  </tr>
  <tr>
   <td>タスクの割り当て手順の送信</td>
   <td>送信済みフォーム</td>
   <td>
    <div>
    </div> </td>
  </tr>
  <tr>
   <td>ワークフローアプリケーションのスタートポイントの送信 </td>
   <td>送信済みフォーム</td>
   <td> </td>
  </tr>
  <tr>
   <td>Agent UIからワークフローへの対話型通信(印刷チャネル)の送信</td>
   <td>レタリング済みドキュメント</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## 請求可能なAPIをカスタムコードのトランザクションとして記録する {#recording-billable-apis-as-transactions-for-custom-code}

PDFフォームの送信、エージェントUIを使用した対話型通信のプレビュー、非標準フォームの送信、カスタム実装などのアクションは、トランザクションとして考慮されません。 AEM Formsは、トランザクションなどのアクションを記録するAPIを提供しています。 カスタム実装からAPIを呼び出して、トランザクションを [記録できます](/help/forms/using/record-transaction-custom-implementation.md)。

## 関連記事 {#related-articles}

* [トランザクションレポートの概要](../../forms/using/transaction-reports-overview.md)
* [取引レポートの表示と理解](../../forms/using/viewing-and-understanding-transaction-reports.md)
* [カスタム実装用のトランザクションの記録](/help/forms/using/record-transaction-custom-implementation.md)

