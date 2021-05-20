---
title: トランザクションレポート請求可能なAPI
seo-title: トランザクションレポート請求可能なAPI
description: トランザクションとして計上されるすべてのAPIのリスト
seo-description: トランザクションとして計上されるすべてのAPIのリスト
uuid: d2f38ae4-75df-426f-af34-52ae6fb324f3
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 929a298d-7f22-487f-bf7d-8ab2556d0d81
docset: aem65
exl-id: 1bc99f3b-3f28-4e74-b259-6ebddc11ffc5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1963'
ht-degree: 9%

---

# トランザクションレポート請求可能なAPI{#transaction-reports-billable-apis}

AEM Formsは、フォームの送信、ドキュメントの処理、ドキュメントのレンダリングを行うためのAPIを複数提供します。 一部のAPIはトランザクションとして計上され、他のAPIは自由に使用できます。 このドキュメントでは、トランザクションレポートでトランザクションとして計上されるすべてのAPIのリストを示します。 課金対象のAPIが使用される一般的なシナリオを以下に示します。

* アダプティブフォーム、HTML5フォーム、フォームセットの送信
* インタラクティブ通信の印刷版またはWeb版のレンダリング
* ドキュメントを別の形式に変換する
* ダイナミックPDFドキュメントのフラット化
* レコードのドキュメントの生成
* インタラクティブPDFドキュメントと別のPDFドキュメントの結合
* AEM Workflowsのタスク割り当て手順とドキュメントサービス手順の使用
* アダプティブフォーム内でのアダプティブフォームの使用

請求APIは、ページ数、ドキュメントまたはフォームの長さ、レンダリングされたドキュメントの最終形式を考慮しません。 トランザクション・レポートでは、トランザクションを次の2つのカテゴリに分けます。レンダリングされたドキュメントとFormsが送信されました。

* **Forms Submitted:** AEM Formsで作成された任意のタイプのフォームからデータが送信され、そのデータが任意のデータストレージリポジトリまたはデータベースに送信されると、フォームの送信と見なされます。例えば、アダプティブフォーム、HTML5フォーム、PDF forms、フォームセットを送信すると、フォームが送信済みと見なされます。 フォームセット内の各フォームは送信と見なされます。 例えば、フォームセットに5つのフォームが含まれている場合、フォームセットが送信されると、トランザクションレポートサービスはそのフォームセットを5件の送信としてカウントします。

* **レンダリングされたドキュメント：** テンプレートとデータを組み合わせ、ドキュメントのデジタル署名または認証、ドキュメントサービスの請求可能なドキュメントサービスAPIを使用したドキュメントの生成、またはドキュメントの形式間の変換をレンダリングしたドキュメントとして計上します。

>[!NOTE]
>
>トランザクションレポートUIには、次の3つのカテゴリが表示されます。Forms送信済み、レンダリングされたドキュメント、処理されたドキュメント。 「レンダリングされたドキュメント」と「処理されたドキュメント」の両方が「レンダリングされたドキュメント」として計上されます。

## 課金対象のドキュメントサービスAPI {#billable-document-services-apis}

### Generate PDFサービス{#generate-pdf-service}

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
   <td>サポートされているファイルタイプからAdobe PDFを作成します。</td>
   <td>処理済みドキュメント</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td>
   <td>サポートされているファイルタイプからAdobe PDFを作成します。</td>
   <td>処理済みドキュメント</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF</a></td>
   <td>Adobe PDFをサポートされているファイルタイプに変換します。 </td>
   <td>処理済みドキュメント<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF2</a></td>
   <td>Adobe PDFをサポートされているファイルタイプに変換します。 </td>
   <td>処理済みドキュメント<br /> </td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/GeneratePDFService.html#exportPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-" target="_blank">exportPDF3</a></td>
   <td>Adobe PDFをサポートされているファイルタイプに変換します。 </td>
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

### Distillerサービス{#distiller-service}

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
   <td>サポートされているファイルタイプからAdobe PDFを作成します。</td>
   <td>処理済みドキュメント</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/pdfg/service/api/DistillerService.html#createPDF2-com.adobe.aemfd.docmanager.Document-java.lang.String-java.lang.String-java.lang.String-com.adobe.aemfd.docmanager.Document-com.adobe.aemfd.docmanager.Document-" target="_blank">createPDF2</a></td>
   <td>サポートされているファイルタイプからAdobe PDFを作成します。</td>
   <td>処理済みドキュメント</td>
   <td> </td>
  </tr>
 </tbody>
</table>

### レコードのドキュメントサービス（DoRサービス） {#document-of-record-service-dor-service}

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
   <td>指定されたレンダリングメソッドを呼び出して、指定されたパラメーターを使用してレコードのドキュメントを生成します。</td>
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
   <td> generatePDFOutputBatch APIは、フォームテンプレートとレコードを組み合わせてPDFを生成します。 レコードのバッチを処理する場合、トランザクションレポートサービスは各レコードを個別のPDFレンディションとしてカウントします。 <br> getGenerateManyFilesフラグを使用する <a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--"></a> と、複数のレンディションを単一のPDFファイルに組み合わせることができます。フラグのステータスに関係なく、サービスは各レコードを個別のPDFレンディションとしてカウントします。 </td>
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
   <td>XDPおよびPDFドキュメントのセットを、PostScript(PS)、Printer Command Language(PCL)およびZPLの各ファイル形式に変換します。 </td>
   <td>処理済みドキュメント</td>
   <td> generatePDFOutputBatch APIは、フォームテンプレートとレコードを組み合わせてPDFを生成します。 レコードのバッチを処理する場合、トランザクションレポートサービスは各レコードを個別のPDFレンディションとしてカウントします。 <br> getGenerateManyFilesフラグを使用する <a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/output/api/BatchOptions.html#getGenerateManyFiles--"></a> と、複数のレンディションを単一のPDFファイルに組み合わせることができます。フラグのステータスに関係なく、サービスは各レコードを個別のPDFレンディションとしてカウントします。 </td>
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
   <td>XDPテンプレートからPDFフォームをレンダリングします。 XPテンプレートは、Forms Designerで作成されます。</td>
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

### Convert PDFサービス{#convert-pdf-service}

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
   <td>PDFドキュメントを画像ドキュメントのリストに変換します。 サポートされる画像形式は、JPEG、JPEG2K、PNGおよびTIFFです。</td>
   <td>処理済みドキュメント</td>
   <td> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/cpdf/api/ConvertPdfService.html#toImage-com.adobe.aemfd.docmanager.Document-com.adobe.fd.cpdf.api.ToImageOptionsSpec-" target="_blank">toPS</a></td>
   <td>オプション仕様で指定されたオプションを使用して、フラットPDFファイルをPostScript形式に変換します。</td>
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
   <td>Documentオブジェクト内のすべてのバーコードをデコードし、バーコードから取得されたデータを含むorg.w3c.dom.Documentオブジェクトを返します。</td>
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
   <td>指定したDDXドキュメントを実行し、結果のドキュメントを含む<a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/client/AssemblerResult.html">AssemblerResult</a>オブジェクトを返します。 </td>
   <td>処理済みドキュメント</td>
   <td>次の操作はトランザクションとして計上されません。
    <ul>
     <li>パッケージまたはポートフォリオの作成</li>
     <li>複数のXDPのステッチ </li>
    </ul> </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#invoke-com.adobe.aemfd.docmanager.Document-java.util.Map-com.adobe.fd.assembler.client.AssemblerOptionSpec-" target="_blank">呼び出し</a></td>
   <td>指定したDDXドキュメントを実行し、結果のドキュメントを含む<a href="https://helpx.adobe.com/experience-manager/6-3/forms/javadocs/com/adobe/fd/assembler/client/AssemblerResult.html">AssemblerResult</a>オブジェクトを返します。 </td>
   <td>処理済みドキュメント</td>
   <td>PDF Generator、Forms、およびOutputサービスでサポートされるすべての入力ファイル形式、Assemblerサービスでは、出力ファイル形式としてこれらすべての形式がサポートされます。 </td>
  </tr>
  <tr>
   <td><a href="https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/assembler/service/AssemblerService.html#toPDFA-com.adobe.aemfd.docmanager.Document-com.adobe.fd.assembler.client.PDFAConversionOptionSpec-">toPDFA</a></td>
   <td>指定したオプションを使用して、指定したドキュメントをPDF/Aに変換します。</td>
   <td>処理済みドキュメント</td>
   <td> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>* Assemblerサービスのinvoke APIは、入力に応じて、別のサービスの課金対象APIを内部的に呼び出すことができます。 したがって、呼び出しAPIは、なし、単一または複数のトランザクションとして計上できます。 カウントされるトランザクションの数は、入力と呼び出された内部APIによって異なります。
>* Assemblerサービスを使用して生成された単一のPDFドキュメントは、なし、単一または複数のトランザクションと見なすことができます。 カウントされるトランザクションの数は、指定されたDDXコードによって異なります。

>



### PDFユーティリティサービス{#pdf-utility-service}

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
   <td>PDFドキュメントをXDPファイルに変換します。 PDFドキュメントをXDPファイルに正常に変換するには、PDFドキュメントにAcroFormsディクショナリ内にXFAストリームが含まれている必要があります。</td>
   <td>処理済みドキュメント</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## 課金対象のデータキャプチャAPI {#billable-data-capture-apis}

アダプティブフォーム、HTML5 Forms、フォームセットの送信イベントはすべてトランザクションとして計上されます。 デフォルトでは、PDFフォームの送信はトランザクションとして考慮されません。 提供された[トランザクションレコーダーAPI](record-transaction-custom-implementation.md)を使用して、PDF formsの送信をトランザクションとして記録します。

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
     <li>送信が成功した場合、1つまたは2つのトランザクションが考慮されます。 カウントされるトランザクションの数は、送信に使用する送信アクションのタイプによって異なります。 例えば、電子メール送信アクションを使用してPDFを送信すると、2つのトランザクション数が計算されます。 フォーム送信用のトランザクションと、レコードのドキュメント(DOR)サービスを使用して生成されたPDF用のトランザクションです。 </li>
     <li>アダプティブフォーム（アダプティブフォームフォームセット）内でアダプティブフォームを使用すると、1回のトランザクションのみが考慮されます。 アダプティブフォーム内には、任意の数のアダプティブフォームを含めることができます。</li>
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
   <td>フォームセットをフォームセット内で設定された送信URLに送信します。</td>
   <td>送信済みフォーム</td>
   <td>
    <ul>
     <li>アダプティブフォーム（アダプティブフォームフォームセット）内でアダプティブフォームを使用すると、1回のトランザクションのみが考慮されます。 アダプティブフォーム内には、任意の数のアダプティブフォームを含めることができます。</li>
     <li>HTML5 Formsフォームセット内の各フォームは、個別のトランザクションとして考慮されます。 </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## OSGi API上の請求可能なインタラクティブ通信とフォーム中心のAEMワークフロー{#billable-interactive-communication-and-form-centric-aem-workflows-on-osgi-apis}

OSGi上のフォーム中心のAEM Workflowsのタスクとドキュメントサービスのステップと、インタラクティブ通信のすべてのレンディションを割り当てます。このステップはトランザクションとして考慮されます。 オーサーインスタンス上でインタラクティブ通信をプレビューし、エージェントUIを使用してパブリッシュインスタンス上でプレビューすることは、トランザクションとして考慮されません。 ワークフローステップでトランザクションが考慮され、ワークフローの完了に失敗した場合、トランザクション数は元に戻されません。

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

### インタラクティブ通信 — 印刷チャネル{#interactive-communication-print-channel}

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
   <td>エージェントUIからワークフローへのインタラクティブ通信（印刷チャネル）の送信</td>
   <td>レタリング済みドキュメント</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## 請求可能なAPIをカスタムコード{#recording-billable-apis-as-transactions-for-custom-code}のトランザクションとして記録する

PDFフォームの送信、エージェントUIを使用したインタラクティブ通信のプレビュー、非標準のフォーム送信、カスタム実装の処理は、トランザクションとして考慮されません。 AEM Formsは、トランザクションなどのアクションを記録するAPIを提供します。 カスタム実装からAPIを呼び出して、[トランザクション](/help/forms/using/record-transaction-custom-implementation.md)を記録できます。

## 関連記事 {#related-articles}

* [トランザクションレポートの概要](../../forms/using/transaction-reports-overview.md)
* [トランザクション・レポートの表示と理解](../../forms/using/viewing-and-understanding-transaction-reports.md)
* [カスタム実装のトランザクションの記録](/help/forms/using/record-transaction-custom-implementation.md)
