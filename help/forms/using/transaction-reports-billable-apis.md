---
title: トランザクションレポート請求可能 API
seo-title: Transaction Reports Billable APIs
description: トランザクションとして計上されるすべての API のリスト
seo-description: List of all the APIs that are accounted as transactions
uuid: d2f38ae4-75df-426f-af34-52ae6fb324f3
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 929a298d-7f22-487f-bf7d-8ab2556d0d81
docset: aem65
exl-id: 1bc99f3b-3f28-4e74-b259-6ebddc11ffc5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1949'
ht-degree: 100%

---

# トランザクションレポート請求可能 API{#transaction-reports-billable-apis}

AEM Forms には、フォームの送信、ドキュメントの処理、ドキュメントのレンダリングをおこなうための API がいくつか用意されています。一部の API はトランザクションとして計上され、それ以外は自由に使用できます。このドキュメントでは、トランザクションレポートでトランザクションとして計上されるすべての API のリストを示します。課金対象の API が使用される一般的なシナリオを次に示します。

* アダプティブフォーム、HTML5 フォーム、フォームセットの送信
* インタラクティブ通信の印刷バージョンまたは Web バージョンのレンダリング
* ある形式から別の形式へのドキュメントの変換
* ダイナミック PDF ドキュメントの統合
* レコードのドキュメントの生成
* インタラクティブ PDF ドキュメントと別の PDF ドキュメントの結合
* AEM Workflows のタスク割り当て手順とドキュメントサービス手順の使用
* アダプティブフォーム内でのアダプティブフォームの使用

請求 API は、ページ数、ドキュメントまたはフォームの長さ、レンダリング済みドキュメントの最終的な形式を考慮しません。トランザクションレポートは、トランザクションを、レンダリングされたドキュメントと送信されたフォームの 2 つのカテゴリに分類します。

* **送信済みフォーム：** AEM Forms で作成された任意のタイプのフォームからデータが送信され、そのデータが任意のデータストレージリポジトリーまたはデータベースに送信された場合、そのデータはフォーム送信と見なされます。例えば、アダプティブフォーム、HTML5 フォーム、PDF Forms、フォームセットは、送信済みフォームとして計上されます。フォームセット内の各フォームは、送信と見なされます。例えば、フォームセットに 5 つのフォームが含まれている場合、フォームセットが送信されると、トランザクションレポートサービスはそのフォームセットを 5 件の送信としてカウントします。

* **レンダリング済みドキュメント：** テンプレートとデータを組み合わせたドキュメントの生成、ドキュメントの電子署名または認証、ドキュメントサービスの課金可能なドキュメントサービス API の使用、ある形式から別の形式へのドキュメントの変換は、レンダリング済みドキュメントとして計上されます。

>[!NOTE]
>
>トランザクションレポート UI には、送信済み Forms、レンダリング済みドキュメント、処理済みドキュメントの 3 つのカテゴリが表示されます。レンダリング済みドキュメントと処理済みドキュメントの両方が、レンダリング済みドキュメントとして計上されます。

## 課金対象のドキュメントサービス API {#billable-document-services-apis}

### PDF 生成サービス {#generate-pdf-service}

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
   <td>サポートされているファイルタイプから Adobe PDF を作成します。</td>
   <td>処理済みドキュメント</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td>
   <td>サポートされているファイルタイプから Adobe PDF を作成します。</td>
   <td>処理済みドキュメント</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF</a></td>
   <td>Adobe PDF をサポートされるファイルタイプに変換します。 </td>
   <td>処理済みドキュメント<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF2</a></td>
   <td>Adobe PDF をサポートされるファイルタイプに変換します。 </td>
   <td>処理済みドキュメント<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF3</a></td>
   <td>Adobe PDF をサポートされるファイルタイプに変換します。 </td>
   <td>処理済みドキュメント<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlFileToPdf-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-">htmlFileToPdf</a></td>
   <td><p>HTML ページから PDF を作成します。</p> </td>
   <td>処理済みドキュメント<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf</a></td>
   <td>HTML ページを指す URL から PDF を作成します。</td>
   <td>処理済みドキュメント<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#htmlToPdf2-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">htmlToPdf2</a></td>
   <td>HTML ページを指す URL から PDF を作成します。</td>
   <td>処理済みドキュメント<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#optimizePDF-com.adobe.aemfd.docmanager.Document-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">optimizePDF</a></td>
   <td>品質に影響を与えることなく不要なメタデータを削除することによって、ファイルサイズを縮小できるように PDF を最適化します。</td>
   <td>処理済みドキュメント<br /> </td>
   <td> </td>
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
   <td>追加情報</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/DistillerService.html#createPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF</a><br /> </td>
   <td>サポートされているファイルタイプから Adobe PDF を作成します。</td>
   <td>処理済みドキュメント</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/DistillerService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td>
   <td>サポートされているファイルタイプから Adobe PDF を作成します。</td>
   <td>処理済みドキュメント</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### レコードのドキュメントサービス（DoR サービス） {#document-of-record-service-dor-service}

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
   <td>指定されたレンダリングメソッドを呼び出して、設定されたパラメーターを使用してレコードのドキュメントを生成します。</td>
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
   <td>データとテンプレートを結合して、PDF ドキュメントを作成します。</td>
   <td>処理済みドキュメント</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePDFOutput-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PDFOutputOptions-" target="_blank">generatePDFOutput</a></td>
   <td>データとテンプレートを結合して、PDF ドキュメントを作成します。</td>
   <td>処理済みドキュメント</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePDFOutputBatch-java.util.Map-java.util.Map-com.adobe.fd.output.api.PDFOutputOptions-com.adobe.fd.output.api.BatchOptions-" target="_blank">generatePDFOutputBatch</a></td>
   <td>データとテンプレートを結合して、一連の PDF ドキュメントを作成します。</td>
   <td>処理済みドキュメント</td>
   <td> generatePDFOutputBatch API は、フォームテンプレートとレコードを組み合わせ、PDF を生成します。レコードのバッチを処理する場合、トランザクションレポートサービスは各レコードを個別の PDF レンディションとしてカウントします。<br> <a href="https://helpx.adobe.com/jp/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--">getGenerateManyFiles</a> フラグを使用して、複数のレンディションを単一の PDF ファイルに結合します。フラグのステータスに関係なく、サービスは各レコードを個別の PDF レンディションとしてカウントします。 </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/jp/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutput-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PrintedOutputOptions-" target="_blank">generatePrintedOutput</a></td>
   <td>XDP および PDF ドキュメントを PostScript（PS）、Printer Command Language（PCL）および ZPL ファイル形式に変換します。 </td>
   <td>処理済みドキュメント</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/jp/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutput-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.output.api.PrintedOutputOptions-" target="_blank">generatePrintedOutput</a></td>
   <td>XDP および PDF ドキュメントを PostScript（PS）、Printer Command Language（PCL）および ZPL ファイル形式に変換します。 </td>
   <td>処理済みドキュメント</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/jp/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/OutputService.html#generatePrintedOutputBatch-java.util.Map-java.util.Map-com.adobe.fd.output.api.PrintedOutputOptions-com.adobe.fd.output.api.BatchOptions-" target="_blank">generatePrintedOutputBatch</a></td>
   <td>XDP および PDF ドキュメントのセットを、PostScript（PS）、Printer Command Language（PCL）および ZPL の各ファイル形式に変換します。 </td>
   <td>処理済みドキュメント</td>
   <td> generatePDFOutputBatch API は、フォームテンプレートとレコードを組み合わせ、PDF を生成します。レコードのバッチを処理する場合、トランザクションレポートサービスは各レコードを個別の PDF レンディションとしてカウントします。<br> <a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--">getGenerateManyFiles</a> フラグを使用して、複数のレンディションを単一の PDF ファイルに結合します。フラグのステータスに関係なく、サービスは各レコードを個別の PDF レンディションとしてカウントします。 </td>
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
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#renderPDFForm-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.PDFFormRenderOptions-" target="_blank">renderPDFForm</a></td>
   <td>PDF フォームを XDP テンプレートからレンダリングします。XP テンプレートは、Forms Designer で作成されます。</td>
   <td>処理済みドキュメント</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/jp/experience-manager/6-5/forms/javadocs/com/adobe/fd/forms/api/FormsService.html#exportData-com.adobe.aemfd.docmanager.Document-com.adobe.fd.forms.api.DataFormat-" target="_blank">exportData</a></td>
   <td>PDF フォームまたは XDP からデータを書き出し</td>
   <td>処理済みドキュメント</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Convert PDF サービス {#convert-pdf-service}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>説明</td>
   <td>トランザクションレポートカテゴリ</td>
   <td>追加情報</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/jp/experience-manager/6-5/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage-com.adobe.aemfd.docmanager.Document-com.adobe.fd.cpdf.api.ToImageOptionsSpec-" target="_blank">toImage</a></td>
   <td>PDF ドキュメントを画像ドキュメントのリストに変換します。サポートされる画像形式は、JPEG、JPEG2K、PNG、TIFF です。</td>
   <td>処理済みドキュメント</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage-com.adobe.aemfd.docmanager.Document-com.adobe.fd.cpdf.api.ToImageOptionsSpec-" target="_blank">toPS</a></td>
   <td>オプション仕様で指定した PDF を使用して、フラットオプションファイルを PostScript 形式に変換します。</td>
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
   <td><a href="https://helpx.adobe.com/jp/experience-manager/6-5/forms/javadocs/com/adobe/fd/bcf/api/BarcodedFormsService.html#decode-com.adobe.aemfd.docmanager.Document-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-java.lang.Boolean-com.adobe.fd.bcf.api.CharSet-" target="_blank">Decode</a></td>
   <td>Document オブジェクト内のすべてのバーコードをデコードし、バーコードから取得されたデータを含む org.w3c.dom.Document オブジェクトを返します。</td>
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
   <td>指定した DDX ドキュメントを実行し、結果のドキュメントを含む <a href="https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ja">AssemblerResult</a> オブジェクトを返します。 </td>
   <td>処理済みドキュメント</td>
   <td>次の操作はトランザクションとして計上されません。
    <ul>
     <li>パッケージまたはポートフォリオの作成</li>
     <li>複数の XDP のステッチ </li>
    </ul> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#invoke-com.adobe.aemfd.docmanager.Document-java.util.Map-com.adobe.fd.assembler.client.AssemblerOptionSpec-" target="_blank">呼び出し</a></td>
   <td>指定した DDX ドキュメントを実行し、結果のドキュメントを含む <a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/client/AssemblerResult.html">AssemblerResult</a> オブジェクトを返します。 </td>
   <td>処理済みドキュメント</td>
   <td>Assembler サービスは、PDFGenerator、Forms、Output サービスがサポートするすべての入力ファイル形式を、出力ファイル形式としてサポートします。 </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#toPDFA-com.adobe.aemfd.docmanager.Document-com.adobe.fd.assembler.client.PDFAConversionOptionSpec-">toPDFA</a></td>
   <td>指定したオプションを使用して、指定したドキュメントを PDF/A に変換します。</td>
   <td>処理済みドキュメント</td>
   <td> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* Assembler サービスの invoke API は、入力に応じて別のサービスの課金対象 API を内部的に呼び出すことができます。したがって、呼び出し API は、０、単一、複数のトランザクションのいずれかとして計上される可能性があります。カウントされるトランザクションの数は、入力と呼び出される内部 API によって異なります。
>* Assembler サービスを使用して生成された単一の PDF ドキュメントは、0、単一、複数のトランザクションのいずれかとして計上される可能性があります。カウントされるトランザクションの数は、指定された DDX コードによって異なります。
>


### PDF ユーティリティサービス  {#pdf-utility-service}

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
   <td>PDF ドキュメントを画像ファイルに変換します。PDF ドキュメントを XDP ファイルに正常に変換するには、辞書内の XFA ストリームが PDF ドキュメントに含まれている必要があります。</td>
   <td>処理済みドキュメント</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## 課金対象のデータキャプチャ API {#billable-data-capture-apis}

アダプティブフォーム、HTML5 Forms、フォームセットのすべての送信イベントは、トランザクションとして計上されます。デフォルトでは、トランザクションフォームの PDF はトランザクションとして計上されません。提供した[トランザクションレコーダー API](record-transaction-custom-implementation.md) を使用して、PDF フォームの送信をトランザクションとして記録します。

### アダプティブフォーム {#adaptive-forms}

<table>
 <tbody>
  <tr>
   <td><p>ユースケース</p> </td>
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
     <li>送信が成功した場合、1 回または 2 回のトランザクションが発生します。カウントされるトランザクションの数は、送信に使用する送信アクションのタイプによって異なります。例えば、電子メール送信アクションを使用した PDF の送信は、2 回のトランザクションが発生します。フォーム送信するトランザクション 1 回と、レコードのドキュメント（DOR）サービスを使用して PDF が生成されるトランザクション 1 回です。 </li>
     <li>アダプティブフォーム（アダプティブフォームフォームセット）内でアダプティブフォームを使用すると、1 回のトランザクションのみがカウントされます。アダプティブフォーム内には、任意の数のアダプティブフォームを含めることができます。</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

### HTML5 のフォーム {#html-forms}

<table>
 <tbody>
  <tr>
   <td><p>ユースケース</p> </td>
   <td>説明 </td>
   <td>トランザクションレポートカテゴリ</td>
   <td>追加情報</td>
  </tr>
  <tr>
   <td>HTML5 フォームの送信</td>
   <td>フォームで設定された URL を送信するために HTML5 フォームを送信します。</td>
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
   <td>フォームセットの管理</td>
   <td>フォームセットを、フォームセットで設定された送信 URL に送信します。</td>
   <td>送信済みフォーム</td>
   <td>
    <ul>
     <li>アダプティブフォーム（アダプティブフォームフォームセット）内でアダプティブフォームを使用すると、1 回のトランザクションのみがカウントされます。アダプティブフォーム内には、任意の数のアダプティブフォームを含めることができます。</li>
     <li>HTML5 Forms フォームセット内の各フォームは、別々のトランザクションとしてカウントされます。 </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## OSGi API 上の課金対象のインタラクティブ通信とフォーム中心の AEM ワークフロー {#billable-interactive-communication-and-form-centric-aem-workflows-on-osgi-apis}

OSGi 上の Form 中心の AEM Workflows のタスクとドキュメントサービスのステップと、インタラクティブ通信のすべてのレンディションを割り当てます。これらはトランザクションとしてカウントされます。オーサーインスタンス上でインタラクティブ通信をプレビューし、エージェント UI を使用してパブリッシュインスタンス上でプレビューすることは、トランザクションとしては考慮されません。ワークフローステップがトランザクションとして考慮され、ワークフローの完了に失敗した場合、トランザクション数は元に戻されません。

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
   <td>Web チャネルのレンダリング</td>
   <td>インタラクティブ通信の web バージョンを開きます。</td>
   <td>レンダリング済みドキュメント</td>
   <td>
    <div>
    </div> </td>
  </tr>
 </tbody>
</table>

### インタラクティブ通信 - 印刷チャンネル {#interactive-communication-print-channel}

<table>
 <tbody>
  <tr>
   <td><p>API</p> </td>
   <td>説明</td>
   <td>トランザクションレポートカテゴリ</td>
   <td>追加情報</td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/ccm/channels/print/api/model/PrintChannel.html" target="_blank">レンダー</a>（PDF に変換）</td>
   <td>インタラクティブ PDF の通信バージョンを生成します。</td>
   <td>レンダリングされたドキュメント</td>
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
   <td>割り当てタスクの送信手順</td>
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
   <td>エージェント UI からワークフローへのインタラクティブ通信（印刷チャネル）の送信</td>
   <td>レンダリングされたドキュメント</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## カスタムコードのトランザクションとしての課金対象 API の記録 {#recording-billable-apis-as-transactions-for-custom-code}

PDF フォームの送信、エージェント UI を使用したインタラクティブな通信のプレビュー、非標準のフォーム送信の使用、カスタム実装などのアクションは、トランザクションとして考慮されません。AEM Forms は、トランザクションなどのアクションを記録する API を提供します。カスタム実装から API を呼び出して、[トランザクションを記録](/help/forms/using/record-transaction-custom-implementation.md)することができます。

## 関連記事 {#related-articles}

* [トランザクションレポートの概要](../../forms/using/transaction-reports-overview.md)
* [トランザクションレポートの表示と理解](../../forms/using/viewing-and-understanding-transaction-reports.md)
* [カスタム実装のトランザクションの記録](/help/forms/using/record-transaction-custom-implementation.md)
