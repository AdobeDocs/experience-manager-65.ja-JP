---
title: PDF Generator を使用したファイルの変換
description: PDF Generatorサービスは、ネイティブファイル形式をPDFに変換します。 また、PDF を他のファイル形式に変換し、PDF ドキュメントのサイズを最適化します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
exl-id: 0e2c12b5-24c8-4aca-8826-cb661051ce4f
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1173'
ht-degree: 11%

---

# PDF Generator を使用したファイルの変換{#converting-files-using-pdf-generator}

PDF Generatorの Web ページを使用して、ファイルを変換できます。

## PDFファイルの作成 {#create-a-pdf-file}

1. 管理コンソールで、サービス/PDF Generator/PDFを作成をクリックします。
1. 「参照」をクリックし、ファイルを探して選択します。

   >[!NOTE]
   >
   >PDF Generatorは、ファイル名にファイル拡張子がない場合でも、.doc、.xls、.ppt、.rtf ファイルのファイルタイプを自動的に検出できます。 この機能は、.docx、.xlsx および.pptx ファイルでは動作しません。

1. 「設定」で、「カスタム設定を使用」または「設定ファイルをアップロード」を選択します。

   * カスタム設定を使用している場合は、Adobe PDF設定、セキュリティ設定、およびファイルタイプ設定を選択し、タイムアウトを指定します。

     Adobe PDFの設定は、PS-to-PDF、EPS-to-PDF、PRN-to-PDF、OCR がオンの画像からPDFへ、およびネイティブからPDFへの変換にのみ適用できます。 タイムアウト設定は、変換が完了するまでの最大時間を指定します。 デフォルト値は 270 秒です。これらの設定は、画像からPDF、OpenOffice からPDFへの変換では使用されません。

   * 設定ファイルをアップロードする場合は、ボックスにファイルのパスと名前を入力するか、「参照」をクリックしてファイルを見つけて選択します。

1. （オプション）「XMP Metadata File」で、XMPファイルのパスと名前を入力するか、「参照」をクリックしてファイルを探して選択します。 XMPファイルを使用して、標準のメタデータ情報を含めることができます。 ( 詳しくは、 [XMPファイルについて](converting-files-using-pdf-generator.md#about-xmp-files).)
1. 「作成」をクリックします。ファイルが作成されると、そのファイルへのリンクが表示されます。 変換中にエラーが発生した場合は、警告が表示されます。 Postscript ファイルを作成している場合は、警告にはログファイルへのリンクも含まれます。
1. PDF・ファイルのリンクをクリックします。 ファイルがAcrobatで開きます。

### XMPファイルについて {#about-xmp-files}

PDFがAcrobat 5.0 以降で作成するPDF Generatorドキュメントには、XML 形式のドキュメントメタデータが含まれます。 *メタデータ* には、作成者の名前、キーワード、著作権情報など、ドキュメントとその内容に関する情報が含まれます。この情報は、検索ユーティリティで使用できます。

ドキュメントメタデータには、Acrobatのドキュメントのプロパティダイアログボックスの「説明」タブにも表示される情報が含まれます（ただし、これらに限定されません）。 「説明」タブで行った変更は、ドキュメントメタデータに反映されます。 ドキュメントのメタデータは、サードパーティ製品を使用して拡張および変更できます。

AdobeExtensible Metadata Platform(XMP) は、公開ワークフロー間でのドキュメントメタデータの作成、処理、交換を標準化する共通の XML フレームワークをAdobeアプリケーションに提供します。 ドキュメントメタデータ XML ソースコードをXMP形式で保存および読み込むことができるので、様々なドキュメント間でメタデータを簡単に共有できます。 XMPファイルについて詳しくは、 [拡張可能なメタデータプラットフォーム (XMP)](https://www.adobe.com/jp/products/dimension.html/) および [AdobeXMPデベロッパーセンター](https://www.adobe.com/devnet/xmp.html).

AcrobatでXMPファイルを作成できます。

## HTMLファイルまたは ZIP ファイルをPDFに変換する {#convert-an-html-file-or-zip-file-to-pdf}

PDF Generatorを使用して、次の種類のファイルをAdobe PDFに変換できます。

* HTMLファイル。HTMLファイルをアップロードするか、Web ページまたは Web サイトの URL を指定することで変換できます。
* アーカイブファイル (ZIP)。HTMLファイル、画像ファイル、またはその両方を含めることができます。

ZIP ファイルのHTML階層の最下位レベルに複数のフォルダファイルが含まれている場合は、その ZIP ファイルに index.htm または index.html ファイルも含まれている必要があります。

>[!NOTE]
>
>* HTMLからPDFへの変換機能を使用するには、システムフォントディレクトリに特定のフォントが必要です。 Linux、Solaris、AIX システムでは、システムフォントディレクトリに Courier フォントが含まれている必要があります。 Windows システムでは、システムフォントディレクトリに Times New Roman が含まれている必要があります。
>
>* （UNIX ベースのシステムのみ）日本語フォントを使用した web ページを PDFドキュメントに変換するには、AEM Forms サーバーで以下の日本語フォントが使用可能である必要があります。
>
>  * 「Sazanami Gothic」
>  * 「Kozuka Gothic Pro-VI」
>  * 「Kozuka Mincho Pro-VI」
>  * 「Sazanami Gothic」
>  * 「Kozuka Mincho Pr6N」
>  * 「Sazanami Mincho」
>  * 「Adobe Heiti Std」
>  * 「Adobe Song Std」
>
>* ローカルファイルシステムからファイルをアップロードするには、「PDFへのHTML」ページの「ファイルのアップロード」オプションを使用します。

1. 管理コンソールで、サービス/PDF Generator/PDFへのHTMLをクリックします。
1. 次のいずれかのタスクを実行して、変換するファイルを指定します。

   * 「ファイルのアップロード」で、HTMLファイルまたは ZIP ファイルのパスとファイル名を入力するか、「参照」をクリックしてファイルを探して選択します。
   * 「URL の指定」ボックスに、変換するページまたは Web サイトの URL を入力します。

   >[!NOTE]
   >
   >変換するファイルのファイル名拡張子は、.html、.htm、.zip のいずれかにする必要があります。

1. 次の設定を指定します。

   * カスタム設定を使用するには、「カスタム設定を使用」を選択し、セキュリティとファイルタイプの設定を指定して、タイムアウト値を指定します。 デフォルト値は 270 秒です。

   >[!NOTE]
   >
   >Acrobat WebCapture を使用するように GeneratePDFサービスを設定した場合、このページで選択する「File Type Settings」は生成されるPDFには影響しません。 代わりに、サーバーにインストールされているAcrobatのバージョンに適切な変更を加えます。

   * 既存の設定ファイルを使用するには、「設定ファイルをアップロード」を選択し、「参照」をクリックしてファイルの場所に移動します。

1. XMPファイルをアップロードするには、「参照」をクリックし、ファイルの場所に移動します。 XMPファイルを使用して、標準のメタデータ情報を含めることができます。 ( 詳しくは、 [XMPファイルについて](converting-files-using-pdf-generator.md#about-xmp-files).)
1. 「作成」をクリックします。ファイルを作成すると、PDF・ファイルへのリンクが表示されます。
1. リンクをクリックして、AcrobatでPDFドキュメントを表示します。

## PDFファイルを別のファイル形式で書き出す（Windows のみ） {#export-a-pdf-file-to-another-file-format-windows-only}

PDFファイルは、の「 GeneratePDFサービス」の章で説明されているように、様々なファイル形式に書き出すことができます。 [サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63).

1. 管理コンソールで、サービス/PDF Generator/Export PDFをクリックします。
1. 「参照」をクリックして、書き出すPDFファイルを指定します。
1. [Export PDFファイルの一覧 ] で、書き出すPDFファイルの形式を選択します。
1. 「Specify A Timeout」ボックスに、アプリケーションがタイムアウトするまでの待機時間を入力します。 デフォルト値は 270 秒です。

   ファイルの変換時に表示される変換時間は、ここで指定した値よりも長くなる場合があります。 変換時間には、スレッドまたはプロセスの待機時間、ファイルの変換に要した時間、およびフォールバックコンバーターが要した時間（該当する場合）が含まれます。 時刻。「タイムアウト値を指定」は、ファイルの変換にかかる時間です。

1. （オプション）**カスタム Preflight プロファイルを指定する**&#x200B;オプションで「参照」をクリックし、[カスタム Preflight プロファイル](https://helpx.adobe.com/jp/acrobat/using/overview-pdf-portfolios.html)を選択します。Preflight プロファイルは、ドキュメントを PDF アーカイブ（PDF/A）形式に変換する際にのみ使用されます。 
1. 「書き出し」をクリックします。 変換処理が完了すると、書き出されたファイルへのリンクが表示されます。
1. リンクをクリックすると、変換されたファイルが表示されます。

## PDFの最適化（Windows のみ） {#optimize-a-pdf}

PDF Generatorは、PDFファイルのサイズの縮小をサポートします。

>[!NOTE]
>
>デジタル署名付きドキュメントを最適化すると、デジタル署名が削除され、無効になります。

1. 管理コンソールで、サービス/PDF Generator/Optimize PDFをクリックします。
1. 「参照」をクリックし、最適化するPDFファイルを指定します。
1. 次の設定を指定します。

   * カスタム設定を使用するには、「カスタム設定を使用」を選択し、ファイルタイプ設定を指定して、タイムアウト値を指定します。 デフォルト値は 270 秒です。
   * 既存の設定ファイルを使用するには、「設定ファイルをアップロード」を選択し、「参照」をクリックしてファイルの場所に移動します。

1. 「作成」をクリックします。
