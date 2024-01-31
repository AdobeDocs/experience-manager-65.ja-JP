---
title: PDFの生成で、WorkBench で大量のPDFを印刷できない
description: お客様が WorkBench を通じて実装されたサービスを通じて多数のPDFを生成した場合、印刷サービスは失敗します。
source-git-commit: 9cdf22918f08fe505c3efd0ce43235e3442165d5
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# PDFの生成で、WorkBench を介して大量のPDFを印刷できない {#PDF-generation-fails-to-print-a-large-number-of-PDFs-via-WorkBench}

## 問題 {#issue}

お客様が WorkBench を通じて実装されたサービスを通じて多数のPDFを生成する場合。 メモリ不足のため、サービスに失敗します。 エラーは次のように表示されます。

`ALC-OUT-002-013: XMLFormFactory, PAexecute failure: "0: Out of Memory"`

<!-- Attached is a simplified template (BollatoRiservatiLandscape_table_simple.xdp) that simulates the problem.
Using the Designer, if we associate the template "BollatoRiservatiLandscape_table_semplice.xdp" with the XML file "BollatoRiservati.xml" during the generation of the pdf, the process comes to occupy 1.6 Gb of RAM. On the server side, with the complete template, the pdf generation process breaks down, occupying 2 GB of RAM.-->

これは、印刷要求の最大ページ数が、Windows では約 1,000 ページに制限されているためです。 印刷出力を生成する際は、テンプレートとデータをメモリに読み込み、結果のレイアウトをメモリに組み込む必要があります。 つまり、最終的な出力のサイズに制限があります。 印刷出力を生成するプロセスは 32 ビットのタスクで、Windows では 2 GB の RAM に制限されます。 <!--and 4 GB on UNIX-->.

## 適用先 {#applies-to}

このソリューションは、AEM Formsに適用されます <!--JEE Server and AEM Forms on OSGi Server--> （x86_win32 XMLFM 用）

## 解決策 {#solution}

メモリ使用量に影響する最大の要因は、フォーム上のデータ量です。 ただし、メモリ使用量に影響を与えるフォームデザインには、その他の要因があります。 これらの要因を認識している場合は、より大きな印刷出力用のフォームをデザインできます。 次のセクションは、メモリフットプリントに影響を与える要因を優先順位付けした順序で示します。

### 影響係数 {#impact-factor}

**高**

1. **選択サブフォーム**  — 選択サブフォームセットはサブフォームセットオブジェクトの一種です。条件ステートメントを使用して、サブフォームセット内の特定のサブフォームの表示をカスタマイズできます。
1. **キャプションの代わりに静的テキストを使用する**  — ほとんどのフィールドでは、内にキャプションが提供されます。ユーザーは、キャプションとして静的テキストを追加する代わりに、キャプションを使用する必要があります。
1. 用途 **リッチテキスト形式 (RTF)** 可能な限り

**平均**

メモリ使用量を改善するために、フォームテンプレートをデザインする際に考慮すべき追加要因を次に示します。

1. 静的テキストを使用してフィールドにラベルを付けるのを避けます。 代わりに、テキストフィールドにキャプションを使用します。
2. [ 長方形 ]、[ 線分 ]、[ オブジェクト ]、[ テーブル ] を使いすぎないでください。
3. 可能な場合は、リッチテキストおよび選択サブフォームの使用を避けます。
4. サブフォームやネストされたサブフォームを過剰に使用しないようにします。

### データサイズの制限 {#data-size-limitations}

プロセスの最大メモリ量に制限があるので、プロセスが消費するメモリ量はデータファイルのサイズに依存するだけではありません。 フォームデザインとは非常に密接に関係しており、ある程度は、フォーム内で結合される実際の量のデータと密接に関係しています。

フォームに小さなデータを持つ小さなノードが多数ある場合、プロセスは大きなデータを持つノード数（さらに）を少なくしたフォームよりも多くのメモリを消費します（したがって、メモリ不足になります）。

詳しくは、 [以下の付録](#appendix) 詳細については、テスト結果が印刷フォーム ( タグなしPDF) に基づく場所を参照してください。 タグ付きPDFプロセスのメモリ要件の使用が増加します。 また、フォーム内のフィールドの数によって異なります。処理メモリの要件は、タグ付けされていないPDFの 1.5 倍をわずかに超えます。

### インタラクティブForms {#interactive-forms}

インタラクティブフォームは、インタラクティブフィールドが再びレンダリングされるので、Print Formsよりも多くのメモリを消費することになります。 実施したテストでは、メモリ消費量が印刷フォームと比べて約 1.5 倍増加し、これらは静的なインタラクティブフォームでした。

### 画像形式 {#image-formats}

Adobeでは、特定の画像形式をお勧めしません。 ただし、PNG(Portable Network Graphics) など、より小さいサイズの画像を使用すると便利です。 また、サイズが数百メガバイトの数値を変える高解像度の画像を使用することはお勧めしません。 また、解凍時に数百メガバイトのデータに拡張されるサイズの圧縮画像は使用しないでください。

### 付録 {#appendix}

**表の例**

次に、単純なテーブルと複雑なテーブルのレンダリング数とデータサイズを示すテーブルの様々なバリアントを示します。

1. 1 列で 5,000 ページのPDFが生成され、データファイルサイズが 24 MB、30,000 レコードのテーブル。

   ![table_single_column](/help/forms/using/assets/table_single_column.png)

1. 800 ページのPDFが生成される多数の小さな列を持つテーブルで、データファイルのサイズは 4.6 MB および 20,000 レコードです。
   ![table_many_small_columns](/help/forms/using/assets/table_many_small_columns.png)

1. 大きな xmlTag 名を使用するために、多くの小さな列を持つが、大きなデータファイルを持つテーブル。
ここでは、前と同じですが、xml タグ名は大きく（実際の有効なデータが増えずにデータファイルのサイズが大きくなるように）、最終的な結果（上限）はほぼ同じです。 ただし、データファイルのサイズは 4.6 MB から 44.6 MB に増加しました。 ここでは、800 ページのPDFが生成され、データファイルのサイズは 44.6 MB と 20,000 レコードです。

   ![table_bigger_xml_tagname](/help/forms/using/assets/table_bigger_xml_tagname.png)

したがって、データファイルのサイズに一般的な上限を設けるのは困難です。 各フォームは一意なので、メモリ消費量はフォームごとに異なります。