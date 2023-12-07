---
title: Assembler サービスの使用
description: Assembler サービスを使用すると、PDFドキュメントと XDP ドキュメントを組み合わせ、並べ替え、拡張し、PDFドキュメントに関する情報を取得できます。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
docset: aem65
exl-id: 2acd6b19-0fe8-4994-b0f4-c9d5b9f3fdf1
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '2118'
ht-degree: 20%

---

# Assembler サービスの使用{#using-assembler-service}

Assembler サービスを使用すると、PDFドキュメントと XDP ドキュメントを組み合わせ、並べ替え、拡張し、PDFドキュメントに関する情報を取得できます。 Assembler サービスに送信される各ジョブには、Document Description XML(DDX) ドキュメント、ソースドキュメント、および外部リソース（文字列とグラフィック）が含まれます。 Assembler サービスについて詳しくは、 [Assembler サービスの概要](../../forms/using/overview-aem-document-services.md#p-assembler-service-p).

以下の操作において Assembler サービスを使用できます。

## PDF ドキュメントのアセンブリ {#assemble-pdf-documents}

Assembler サービスを使用すると、複数のPDFドキュメントを 1 つのPDFドキュメントまたはPDFPortfolioに組み立てることができます。 また、ナビゲーションを支援する機能やセキュリティを強化するPDFドキュメントに機能を適用することもできます。 次に、PDF ドキュメントのアセンブリ方法を示します。

### 単純な PDF ドキュメントのアセンブリ {#assemble-a-simple-pdf-document}

次の図は、3 つのソースドキュメントを 1 つの結果ドキュメントにマージする様子を示しています。

![複数の PDF ドキュメントから単一の PDF ドキュメントへのアセンブリ](assets/as_document_assembly.png)

複数の PDF ドキュメントから単一の PDF ドキュメントへのアセンブリ

次の例は、ドキュメントのアセンブリに使用される単純な DDX ドキュメントです。 結果のドキュメントの生成に使用するソースドキュメントの名前と、結果のドキュメントの名前を指定します。

```xml
<PDF result="Doc4">
<PDF source="Doc1"/>
<PDF source="Doc2"/>
<PDF source="Doc3"/>
</PDF>
```

ドキュメントのアセンブリは、以下のコンテンツと特性を備えた結果ドキュメントを生成します。\
特徴：

* 各ソースドキュメントのすべてまたは一部
* アセンブリされた結果のドキュメントに対して正規化された、各ソースドキュメントのしおりのすべてまたは一部
* メタデータ、ページラベル、ページサイズなど、ベースドキュメント (Doc1) から採用されたその他の特性
* オプションで、結果のドキュメントには、ソースドキュメント内のしおりから構築された目次が含まれます

### PDF ポートフォリオの作成 {#create-a-pdf-portfolio}

Assembler サービスは、一連のドキュメントと自己完結型のPDFインターフェイスを含むユーザーPortfolioを作成できます。 このインターフェイスは、PDFPortfolioレイアウトまたはPDFPortfolioナビゲーター（ナビゲーター）と呼ばれます。 PDFPortfolioは、ナビゲーター、PDFー、ようこそページを追加することで、フォルダーパッケージの機能を拡張します。 このインターフェイスは、ローカライズされたテキスト文字列、カスタムカラースキーム、グラフィックリソースを利用して、ユーザーエクスペリエンスを強化できます。 また、PDFPortfolioには、ポートフォリオ内のファイルを整理するためのフォルダを含めることもできます。

Assembler サービスが以下の DDX ドキュメントを解釈すると、PDFPortfolioナビゲーターと 2 つのファイルのパッケージを含むPDFPortfolioがアセンブルされます。 ナビゲータは、myNavigator ソースで指定された場所から取得されます。 ナビゲータのデフォルトのカラースキームを pinkScheme カラースキームに変更します。

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<PDF result="Untitled 1">
<Portfolio>
<Navigator source="myNavigator"/>
<ColorScheme scheme="pinkScheme"/>
</Portfolio>
<PackageFiles>
<PDF source="sourcePDF1"/>
<PDF source="sourcePDF2"/>
</PackageFiles>
</PDF>
</DDX>
```

### 暗号化ドキュメントのアセンブリ {#assemble-encrypted-documents}

ドキュメントを組み立てる際に、パスワードを使用してPDFドキュメントを暗号化することもできます。 PDFドキュメントがパスワードで暗号化された後、ユーザーは、Adobe ReaderまたはAcrobatでPDFドキュメントを表示するために、パスワードを指定する必要があります。 PDFドキュメントをPDFで暗号化するには、パスワードドキュメントの暗号化に必要な暗号化要素の値が DDX ドキュメントに含まれている必要があります。

PDFドキュメントをパスワードで暗号化する場合、LiveCycleのインストールに Encryption サービスを含める必要はありません。

1 つ以上の入力ドキュメントが暗号化されている場合は、DDX の一部としてドキュメントを開くためのパスワードを指定します。

### ベイツナンバリングを使用したドキュメントのアセンブリ {#assemble-documents-using-bates-numbering}

ドキュメントを組み立てる際に、ベイツナンバリングを使用して、各ページに一意のページ識別子を適用できます。 通し番号を使用すると、ドキュメント（またはドキュメントのセット）内の各ページに、ページを一意に識別する番号が割り当てられます。 たとえば、部品表情報を含み、アセンブリの製造に関連付けられている製造ドキュメントには、識別子を含めることができます。 Bates の数値には、連続して増分される数値と、オプションの接頭辞と接尾辞が含まれます。 プレフィックス+数値+サフィックスは、ベイツパターンと呼ばれます。

次の図は、ドキュメントのPDFに一意の ID が含まれるヘッダードキュメントを示しています。

![ドキュメントのPDFに一意の識別子が含まれるヘッダードキュメント](do-not-localize/as_batesnumber.png)

ドキュメントのPDFに一意の識別子が含まれるヘッダードキュメント

### ドキュメントの統合およびアセンブリ {#flatten-and-assemble-documents}

Assembler サービスを使用して、インタラクティブPDFドキュメント（フォームなど）を非インタラクティブPDFドキュメントに変換できます。 インタラクティブPDFドキュメントを使用すると、ユーザーは「PDFドキュメント」フィールドにデータを入力または変更できます。 インタラクティブ PDF ドキュメントを非インタラクティブ PDF ドキュメントに変換するプロセスは「フラット化」と呼ばれます。PDFドキュメントを統合すると、フォームフィールドはグラフィカルな外観を保持しますが、インタラクティブではなくなります。 PDF ドキュメントを統合する理由の 1 つは、データを変更できないようにすることです。また、フィールドに関連付けられたスクリプトは機能しなくなりました。

インタラクティブPDFドキュメントからアセンブルされたPDFドキュメントを作成する場合、Assembler サービスは、それらのフォームを統合してから結果ドキュメントにアセンブリします。

>[!NOTE]
>
>Assembler サービスは、Output サービスを使用して動的 XFA フォームを統合します。 Assembler サービスが XFA 動的フォームのフラット化を要求する DDX を処理し、Output サービスを使用できない場合は、例外がスローされます。 Assembler サービスは、Output サービスを使用せずに、Acrobatフォームまたは静的 XFA フォームを統合できます。

## XDP ドキュメントのアセンブリ {#assemble-xdp-documents}

Assembler サービスを使用して、複数の XDP ドキュメントを 1 つの XDP ドキュメントにアセンブリしたり、PDFドキュメントにアセンブリしたりできます。 挿入ポイントを含むソース XDP ファイルの場合、挿入するフラグメントを指定できます。

XDP ドキュメントをアセンブリする方法を次に示します。

### 単純な XDP ドキュメントのアセンブリ {#assemble-a-simple-xdp-document}

次の図は、3 つのソース XDP ドキュメントを 1 つの結果 XDP ドキュメントにアセンブリする場合の様子を示しています。 結果の XDP ドキュメントには、3 つのソース XDP ドキュメントが含まれ、その中に関連するデータも含まれます。 結果ドキュメントには、ベースドキュメント（最初のソース XDP ドキュメント）から基本属性が受け継がれます。

![複数の XDP ドキュメントから単一の XDP ドキュメントへのアセンブリ](assets/as_assembler_xdpassembly.png)

複数の XDP ドキュメントから単一の XDP ドキュメントへのアセンブリ

上の図に示す結果を生成する DDX ドキュメントを次に示します。

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="MyXDPResult">
<XDP source="sourceXDP1"/>
<XDP source="sourceXDP2"/>
<XDP source="sourceXDP3"/>
</XDP>
</DDX>
```

### アセンブリ中の参照の解決 {#resolving-references-during-assembly}

通常、XDP ドキュメントには、絶対参照または相対参照を使用して参照される画像を含めることができます。 Assembler サービスは、デフォルトで結果の XDP ドキュメント内の画像への参照を保持します。

Assembler サービスでは、ソース XDP ドキュメント内で参照されている画像を、アセンブル時に XDP ファイル内の絶対参照または相対参照を使用して処理する方法を指定できます。 相対参照や絶対参照を含めないように、すべての画像を結果に埋め込むように選択できます。 これを定義するには、次のオプションを使用できる resolveAssets タグの値を設定します。 デフォルトでは、結果ドキュメント内で参照が解決されません。

<table>
 <tbody> 
  <tr> 
   <th>値</th> 
   <th>説明</th> 
  </tr> 
  <tr> 
   <td>none</td> 
   <td>参照を解決しません。</td> 
  </tr> 
  <tr> 
   <td>all</td> 
   <td>ソース XDP ドキュメント内のすべての参照画像を埋め込みます。</td> 
  </tr> 
  <tr> 
   <td>相対的</td> 
   <td>ソース XDP 内の相対参照を通じて参照されるすべての画像を埋め込みます<br /> 文書。</td> 
  </tr> 
  <tr> 
   <td>absolute</td> 
   <td>ソース XDP の絶対参照を介して参照されるすべての画像を埋め込みます<br /> 文書。</td> 
  </tr> 
 </tbody> 
</table>

resolveAssets 属性の値は、XDP ソースタグまたは親 XDP 結果タグで指定できます。 属性が XDP の結果タグに指定されている場合、XDP 結果の子であるすべての XDP ソース要素に継承されます。 ただし、ソース要素の属性を明示的に指定すると、そのソースドキュメントの結果要素の設定だけが上書きされます。

#### XDP ドキュメント内のすべてのソース参照を解決する {#resolve-all-source-references-in-an-xdp-document}

ソース XDP ドキュメント内のすべての参照を解決するには、以下の例のように、結果ドキュメントの resolveAssets 属性を all に\
指定します。

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="result.xdp" resolveAssets="all">
<XDP source="input1.xdp" />
<XDP source="input2.xdp" />
<XDP source="input3.xdp" />
</XDP>
</DDX
```

また、すべてのソース XDP ドキュメントの属性を個別に指定した場合も、同じ結果に\
なります。

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="result.xdp">
<XDP source="input1.xdp" resolveAssets="all"/>
<XDP source="input2.xdp" resolveAssets="all"/>
<XDP source="input3.xdp" resolveAssets="all"/>
</XDP>
</DDX>
```

#### XDP ドキュメント内の選択したソース参照の解決 {#resolve-selected-source-references-in-an-xdp-document}

解決するソース参照を選択的に指定するには、そのソース参照の resolveAssets 属性を指定します。 個々のソースドキュメントの属性は、結果の XDP ドキュメントの設定に優先します。 この例では、含まれるフラグメントも解決されます。

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="result.xdp" resolveAssets="all">
<XDP source="input1.xdp" >
<XDPContent source="fragment.xdp" insertionPoint="MyInsertionPoint"
fragment="myFragment"/>
</XDP>
<XDP source="input2.xdp" />
</XDP>
</DDX>
```

#### 絶対参照または相対参照を選択的に解決する {#selectively-resolve-absolute-or-relative-references}

次の例に示すように、すべてのまたは一部のソースドキュメントの絶対参照または相対参照を選択して解決できます。

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="result.xdp" resolveAssets="absolute">
<XDP source="input1.xdp" />
<XDP source="input2.xdp" />
</XDP>
</DDX
```

### フォームフラグメントを XFA フォームに動的に挿入する {#dynamically-insert-form-fragments-into-an-xfa-form}

Assembler サービスを使用して、フラグメントを挿入する別の XFA フォームから作成された XFA フォームを作成できます。 この機能を使用すると、フラグメントを使用して複数のフォームを作成できます。

フォームフラグメントの動的挿入のサポートは、シングルソースコントロールをサポートします。 一般的に使用されるコンポーネントの 1 つのソースを維持できます。 例えば、会社のバナー用のフラグメントを作成できます。 バナーが変更された場合は、フラグメントを変更するだけで済みます。 フラグメントを含むその他のフォームは変更されません。

フォームデザイナーは、LiveCycle Designer を使用してフォームフラグメントを作成します。これらのフラグメントは、XFA フォーム内で一意の名前を持つサブフォームです。 また、フォームデザイナーは Designer を使用して、一意の名前を持つ挿入ポイントを持つ XFA フォームを作成します。 DDX ドキュメントは、フラグメントを XFA フォームに挿入する方法を指定する（プログラマー）ユーザーが作成します。

次の図に、2 つの XML フォーム（XFA テンプレート）を示します。 左側のフォームには、myInsertionPoint という名前の挿入ポイントが含まれています。 右側のフォームには、myFragment という名前のフラグメントが含まれています。

![フォームフラグメントの XFA フォームへの挿入](assets/as_assembler_fragment_assy_assembled.png)

フォームフラグメントの XFA フォームへの挿入

Assembler サービスが以下の DDX ドキュメントを解釈すると、別の XML フォームを含む XML フォームが作成されます。 myFragmentSource ドキュメントの myFragment サブフォームが、myFormSource ドキュメントの myInsertionPoint の位置に挿入されます。

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<XDP result="myFormResult">
<XDP source="myFormSource">
<XDPContent fragment="myFragment" insertionPoint="myInsertionPoint"
source="myFragmentSource"/>
</XDP>
</XDP>
</DDX
```

### XDP ドキュメントのパッケージ化をPDF {#package-an-xdp-document-as-pdf}

Assembler サービスを使用して、XDP ドキュメントをPDFドキュメントとしてパッケージ化できます（この DDX ドキュメントを参照）。

```xml
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<PDF result="Untitled 1" encryption="passEncProfile1">
<XDP>
<XDP source="sourceXDP3"/>
<XDP source="sourceXDP4"/>
</XDP>
</PDF>
</DDX>
```

## PDF ドキュメントのディスアセンブリ {#disassemble-pdf-documents}

Assembler サービスを使用して、Assembler ドキュメントをPDFできます。 このサービスでは、ソースドキュメントからページを抽出したり、しおりに基づいてソースドキュメントを分割したりできます。 通常、このタスクは PDF ドキュメントが最初に多数の個別ドキュメント（明細書など）から作成された場合に役立ちます。

### ソースドキュメントからのページの抽出 {#extract-pages-from-a-source-document}

次の図では、1 ～ 3 ページがソースドキュメントから抽出され、新しい結果ドキュメントに配置されています。

![ソースドキュメントからの特定ページの抽出](assets/as_intro_page_extraction.png)

ソースドキュメントからの特定ページの抽出

次の例は、ドキュメントのディスアセンブリに使用される DDX ドキュメントです。

```xml
<PDF result="Doc4">
<PDF source="Doc2" pages="1-3"/>
</PDF>
```

### しおりに基づいたソースドキュメントの分割 {#divide-a-source-document-based-on-bookmarks}

以下のイラストでは、DocA が複数の結果ドキュメントに分割されています。ページの初めのレベル 1 のブックマークで、新しい結果ドキュメントの開始が示されています。

![ブックマークに基づいたソースドキュメントの複数のドキュメントへの分割](assets/as_intro_pdfsfrombookmarks.png)

ブックマークに基づいたソースドキュメントの複数のドキュメントへの分割

次の例は、しおりを使用してソースドキュメントを分解する DDX ドキュメントです。

```xml
<PDFsFromBookmarks prefix="A">
<PDF source="DocA"/>
</PDFsFromBookmarks>
```

## ドキュメントがPDF/A に準拠しているかどうかを確認 {#determine-whether-documents-are-pdf-a-compliant}

Assembler サービスを使用して、PDFドキュメントがPDF/A に準拠しているかどうかを判断できます。 PDF/A は、ドキュメントのコンテンツを長期保存するためのアーカイブ形式です。 フォントはドキュメントに埋め込まれ、ファイルは非圧縮になります。その結果、通常、PDF/A ドキュメントは標準の PDF ドキュメントよりも大きくなります。なお、PDF/A ドキュメントには、オーディオおよびビデオのコンテンツは含まれません。

## PDF文書に関する情報の取得 {#obtain-information-about-a-pdf-document}

Assembler サービスを使用して、取得するドキュメントに関する次の情報をPDFできます。

* テキスト情報。

   * ドキュメントの各ページに含まれる単語
   * ドキュメントの各ページでの各単語の位置
   * ドキュメントの各ページの各段落の文

* ブックマーク（ページ番号、タイトル、宛先、外観など）。 PDF ドキュメントから\
  このデータをエクスポートして、別の PDF ドキュメントにインポートすることができます。

* 添付ファイル（ファイル情報を含む）。ページレベルの添付ファイルの場合は、\
  添付ファイル注釈の場所が含まれます。PDF ドキュメントからこのデータをエクスポートして、\
  別の PDF ドキュメントにインポートすることができます。

* パッケージファイル（ファイル情報、フォルダー、パッケージ、スキーマ、フィールドデータを含む）。 このデータは、PDFドキュメントから書き出し、PDFドキュメントに読み込むことができます。

## DDX ドキュメントの検証 {#validate-ddx-documents}

Assembler サービスを使用して、DDX ドキュメントが有効かどうかを判断できます。 例えば、以前のバージョンからアップグレードした場合、検証は DDXLiveCycleが有効であることを確認します。

## 他のサービスを呼び出す {#call-other-services}

Assembler サービスが以下の LiveCycle サービスを呼び出す原因となる DDX ドキュメントを使用できます。 Assembler サービスは、Assembler と共にインストールされたサービスのみを呼び出すことができますLiveCycle。

**Reader拡張サービス**:Adobe Readerユーザーが結果の署名ドキュメントに電子署名をPDFできます。

**Formsサービス**:XDP ファイルと XML データファイルを結合して、入力済みのインタラクティブフォームを含むPDFドキュメントを作成します。

**Output サービス**：動的な XML フォームを、非インタラクティブフォームを含むPDFドキュメントに変換します（フォームが統合されます）。 Assembler サービスでは、静的な XML フォームと Acrobat フォームを統合する際に Output サービスを呼び出しません。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
<PDF result="outDoc">
<PDF source="doc1"/>
<PDF source="doc2"/>
<ReaderRights
credentialAlias="LCESCred"
digitalSignatures="true"/>
</PDF>
</DDX>
```

DDX と Assembler サービスを使用して他の LiveCycle サービスを呼び出すと、プロセスダイアグラムを簡略化できます。 ワークフローのカスタマイズに費やす労力を減らすこともできます。 （関連トピック
