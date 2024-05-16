---
title: PDF Generator を使用したファイルの変換
description: PDF Generator サービスは、ネイティブファイル形式を PDF に変換します。また、PDF を他のファイル形式に変換し、PDF ドキュメントのサイズを最適化します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/working_with_pdf_generator
products: SG_EXPERIENCEMANAGER/6.5/FORMS
feature: PDF Generator
exl-id: 0e2c12b5-24c8-4aca-8826-cb661051ce4f
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '1173'
ht-degree: 100%

---

# PDF Generator を使用したファイルの変換{#converting-files-using-pdf-generator}

PDF Generator web ページを使用してファイルを変換できます。

## PDF ファイルの作成 {#create-a-pdf-file}

1. 管理コンソールで、サービス／PDF Generator／PDF の作成をクリックします。
1. 「参照」をクリックしてファイルを見つけて選択します。

   >[!NOTE]
   >
   >PDF Generator は、ファイル名にファイルの拡張子がない場合でも、自動的に .doc、.xls、.ppt および .rtf ファイルのファイルタイプを検出できます。この機能は .docx、.xlsx および .pptx ファイルでは動作しません。

1. 「環境設定」で、「カスタム設定を使用」または「設定ファイルをアップロード」を選択します。

   * カスタム設定を使用している場合は、Adobe PDF 設定、セキュリティ設定およびファイルタイプ設定を選択し、タイムアウトを指定します。

     Adobe PDF 設定は、PS から PDF、EPS から PDF、PRN から PDF、画像から PDF（OCR が有効）およびネイティブから PDF の変換のみに適用できます。タイムアウト設定は、変換が完了するまでの最大時間を指定します。デフォルト値は 270 秒です。画像から PDF、および OpenOffice から PDF への変換中は、これらの設定は使用されません。

   * 設定ファイルをアップロードする場合、ボックスにファイルのパスと名前を入力するか、「参照」をクリックしてファイルを見つけて選択します。

1. （オプション）XMP メタデータファイルで、XMP ファイルのパスと名前を入力するか、「参照」をクリックしてファイルを見つけて選択します。XMP ファイルは、標準のメタデータ情報を含めるのに使用できます（[XMP ファイルについて](converting-files-using-pdf-generator.md#about-xmp-files)を参照）。
1. 「作成」をクリックします。ファイルが作成されると、そのファイルへのリンクが表示されます。変換中にエラーが発生すると、警告が表示されます。PostScript ファイルを作成している場合、警告にはログファイルへのリンクも含まれます。
1. PDF ファイルのリンクをクリックします。Acrobat でファイルが開きます。

### XMP ファイルについて {#about-xmp-files}

PDF Generator により Acrobat 5.0 またはそれ以降で作成される PDF ドキュメントには、XML 形式のドキュメントのメタデータが含まれます。*メタデータ*&#x200B;には、作成者の名前、キーワードおよび著作権情報などドキュメントとそのコンテンツに関する情報が含まれており、この情報は検索ユーティリティで使用できます。

ドキュメントのメタデータには、Acrobat のドキュメントのプロパティダイアログボックスの「説明」タブで表示される情報も含まれます（ただし、これには限定されません）。「説明」タブで行われた変更は、ドキュメントのメタデータに反映されます。ドキュメントのメタデータは、サードパーティの製品を使用して拡張したり、変更したりできます。

Adobe Extensible Metadata Platform（XMP）は、パブリッシングワークフロー間でのドキュメントのメタデータの作成、処理および交換を標準化する共通の XML フレームワークをアドビアプリケーションに提供します。ドキュメントのメタデータの XML ソースコードは XMP 形式で保存および読み込むことができるので、様々なドキュメント間でメタデータを簡単に共有できるようになります。XMP ファイルについて詳しくは、[Extensible Metadata Platform（XMP）](https://www.adobe.com/jp/products/dimension.html/)および [Adobe XMP Developer Center](https://www.adobe.com/devnet/xmp.html) を参照してください。

Acrobat では、XMP ファイルを作成できます。

## HTML ファイルまたは ZIP ファイルから PDF への変換 {#convert-an-html-file-or-zip-file-to-pdf}

PDF Generator を使用して、次の種類のファイルを Adobe PDF に変換できます。

* HTML ファイル。HTML ファイルをアップロードするか、web ページまたは Web サイトの URL を指定することによって変換できます。
* アーカイブファイル（ZIP）。HTML ファイル、画像ファイル、またはその両方を含めることができます。

ZIP ファイルで、フォルダー階層の最下位レベルに複数の HTML ファイルが含まれている場合、その ZIP ファイルには、index.htm または index.html ファイルも含まれている必要があります。

>[!NOTE]
>
>* HTML から PDF への変換機能を使用する場合、システムフォントディレクトリに特定のフォントが含まれている必要があります。Linux、Solaris および AIX システムでは、システムフォントディレクトリに Courier フォントが含まれている必要があります。Windows システムでは、システムフォントディレクトリに Times New Roman が含まれている必要があります。
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
>* ローカルファイルシステムからファイルをアップロードするには、HTML から PDF ページの「アップロードするファイル」オプションを使用します。

1. 管理コンソールで、サービス／PDF Generator／HTML から PDF をクリックします。
1. 次のいずれかを実行して、変換するファイルを指定します。

   * 「アップロードするファイル」に、HTML ファイルまたは ZIP ファイルのパスとファイル名を入力するか、「参照」をクリックして該当するファイルを探して選択します。
   * 「URL の指定」ボックスに、変換するページまたは web サイトの URL を入力します。

   >[!NOTE]
   >
   >変換するファイルのファイル拡張子は、.html、.htm または .zip である必要があります。

1. 設定を次のように指定します。

   * カスタム設定を使用するには、「カスタム設定を使用」を選択し、セキュリティおよびファイルタイプの設定を指定して、タイムアウト値を指定します。デフォルト値は 270 秒です。

   >[!NOTE]
   >
   >Acrobat WebCapture を使用するように Generate PDF サービスを設定している場合、このページで選択する「ファイルタイプごとの設定」は、生成される PDF には影響しません。代わりに、サーバーにインストールされている Acrobat のバージョンに適切な変更を行います。

   * 既存の設定ファイルを使用するには、「設定ファイルをアップロード」を選択し、「参照」をクリックしてファイルの場所に移動します。

1. XMP ファイルをアップロードするには、「参照」をクリックしてファイルの場所に移動します。XMP ファイルは、標準のメタデータ情報を含めるのに使用できます（[XMP ファイルについて](converting-files-using-pdf-generator.md#about-xmp-files)を参照）。
1. 「作成」をクリックします。ファイルが作成されると、その PDF ファイルへのリンクが表示されます。
1. PDF ドキュメントを Acrobat で表示するには、そのリンクをクリックします。

## 別のファイル形式への PDF ファイルの書き出し（Windows のみ） {#export-a-pdf-file-to-another-file-format-windows-only}

[サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)の「Generate PDF サービス」の章で説明したように、PDF ファイルは様々なファイル形式に書き出すことができます。

1. 管理コンソールで、サービス／PDF Generator／PDF の書き出しをクリックします。
1. 「参照」をクリックして、書き出す PDF ファイルを参照します。
1. 「PDF ファイルの書き出し先」リストで、PDF ファイルの書き出し先の形式を選択します。
1. 「タイムアウト時間の指定」ボックスに、アプリケーションがタイムアウトになるまでの待機時間を入力します。デフォルト値は 270 秒です。

   ファイル変換時に「変換時間」に表示される値は、ここで指定する値よりも長くなる場合があります。「変換時間」の値には、スレッドまたはプロセスの待機時間、ファイルの変換時間、およびフォールバックコンバーターにかかる時間（該当する場合）なども含まれています。時刻。「タイムアウトを指定」の値は、ファイルの変換にかかる時間です。

1. （オプション）**カスタム Preflight プロファイルを指定する**&#x200B;オプションで「参照」をクリックし、[カスタム Preflight プロファイル](https://helpx.adobe.com/jp/acrobat/using/overview-pdf-portfolios.html)を選択します。Preflight プロファイルは、ドキュメントを PDF アーカイブ（PDF/A）形式に変換する際にのみ使用されます。 
1. 「書き出し」をクリックします。変換が終了すると、書き出されたファイルへのリンクが表示されます。
1. 変換されたファイルを表示するには、そのリンクをクリックします。

## PDF の最適化（Windows のみ） {#optimize-a-pdf}

PDF Generator では、PDF ファイルのサイズを減らすことができます。

>[!NOTE]
>
>デジタル署名されたドキュメントを最適化すると、デジタル署名が削除されて無効になります。

1. 管理コンソールで、サービス／PDF Generator／PDF の最適化をクリックします。
1. 「参照」をクリックして、最適化する PDF ファイルを探します。
1. 設定を次のように指定します。

   * カスタム設定を使用するには、「カスタム設定を使用」を選択し、ファイルタイプの設定を指定して、タイムアウト値を指定します。デフォルト値は 270 秒です。
   * 既存の設定ファイルを使用するには、「設定ファイルをアップロード」を選択し、「参照」をクリックしてファイルの場所に移動します。

1. 「作成」をクリックします。
