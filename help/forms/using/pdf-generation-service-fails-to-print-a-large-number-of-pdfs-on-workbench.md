---
title: PDF 生成で多数の PDF を WorkBench で印刷できない
description: お客様が WorkBench を通じて実装されたサービスを使用して多数の PDF を生成すると、印刷サービスは失敗します。
exl-id: f3746b8e-4c38-447a-b5bf-d11fc77556f7
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, Troubleshooting
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 100%

---

# PDF 生成で多数の PDF を WorkBench で印刷できない {#PDF-generation-fails-to-print-a-large-number-of-PDFs-via-WorkBench}

## 問題 {#issue}

お客様が WorkBench を通じて実装されたサービスを使用して多数の PDF を生成する場合。サービスはメモリ不足のため失敗します。エラーは、次のように表示されます。

`ALC-OUT-002-013: XMLFormFactory, PAexecute failure: "0: Out of Memory"`

<!-- Attached is a simplified template (BollatoRiservatiLandscape_table_simple.xdp) that simulates the problem.
Using the Designer, if we associate the template "BollatoRiservatiLandscape_table_semplice.xdp" with the XML file "BollatoRiservati.xml" during the generation of the pdf, the process comes to occupy 1.6 Gb of RAM. On the server side, with the complete template, the pdf generation process breaks down, occupying 2 GB of RAM.-->

これは、Windows では印刷要求の最大ページ数が約 1,000 ページに制限されているからです。印刷出力を生成する際は、テンプレートとデータをメモリに読み込む必要があり、結果のレイアウトはメモリ内に作成されます。つまり、最終的な出力のサイズに制限があります。印刷出力を生成するプロセスは 32 ビットタスクで、Windows では 2 GB の RAM に制限されます。<!--and 4 GB on UNIX-->

## 適用先 {#applies-to}

この解決策は x86_win32 XMLFM 用の AEM Forms <!--JEE Server and AEM Forms on OSGi Server--> に適用されます。

## 解決策 {#solution}

メモリ使用量に影響する最大の要因は、フォーム上のデータ量です。ただし、フォームの設計には、メモリ使用量に対してそれほど影響を与えないその他の要因があります。これらの要因を認識している場合は、より大規模な印刷出力用のフォームを設計できます。次の節では、メモリフットプリントに影響を与える要因を優先順に示します。

### 影響要因 {#impact-factor}

**高**

1. **選択サブフォーム** - 選択サブフォームセットは、サブフォームセットオブジェクトの一種で、条件ステートメントを使用してサブフォームセット内の特定のサブフォームの表示をカスタマイズするのに使用できます。
1. **キャプションの代わりに静的テキストを使用** - ほとんどのフィールドでは内部にキャプションが用意されているので、ユーザーは、静的テキストをキャプションとして追加するのではなく、このキャプションを使用する必要があります。
1. 可能な限り、**リッチテキスト形式（RTF）**&#x200B;を使用します。

**平均**

メモリ使用量の改善に役立つフォームテンプレート設計時に考慮すべき追加要因を次に示します。

1. 静的テキストを使用してフィールドにラベルを付けるのを避けます。代わりに、テキストフィールドのキャプションを使用します。
2. 長方形、線、オブジェクトおよびテーブルを使用しすぎないようにします。
3. リッチテキストや選択サブフォームの使用はできるだけ避けます。
4. サブフォームやネストされたサブフォームの過度の使用を避けます。

### データサイズの制限 {#data-size-limitations}

プロセスのメモリ量に上限があるので、プロセスで消費されるメモリ量はデータファイルのサイズにのみ依存するわけではありません。フォームデザインに密接に関係し、フォーム内で結合される実際の量のデータにもある程度関係しています。

小さなデータを持つ小さなノードがフォームに多数ある場合、プロセスは、大きなデータを持つ少数のノードがあるフォームよりも多くのメモリを消費します（したがって、メモリ不足が発生しやすくなります）。

詳しくは、[以下の付録](#appendix)を参照してください。そこで示されるテスト結果は印刷フォーム（タグなし PDF）に基づいています。タグ付き PDF を使用すると、プロセスに必要なメモリが増えます。また、フォーム内のフィールドの数にも左右されます。大まかに、プロセスに必要なメモリは、タグなし PDF の場合の 1.5 倍をわずかに上回ります。

### インタラクティブフォーム {#interactive-forms}

インタラクティブフォームでは、インタラクティブフィールドが再びレンダリングされるので、印刷フォームよりも多くのメモリを消費します。実施したテストでは、メモリ消費量が印刷フォームと比べて約 1.5 倍増加し、これらは静的なインタラクティブフォームでした。

### 画像形式 {#image-formats}

特定の画像形式はお勧めしません。ただし、PNG（Portable Network Graphics）などの、より小さいサイズの画像を使用することをお勧めします。また、サイズが数百メガバイトもあるような高解像度の画像を使用することもお勧めしません。さらに、解凍時にサイズが数百メガバイトに増大する圧縮画像の使用はお勧めしません。

### 付録 {#appendix}

**テーブルの例**

単純なテーブルと複雑なテーブルのレンダリングページ数とデータサイズの比較を示すテーブルの様々な例を次に示します。

1. 1 列のテーブル（5,000 ページの PDF が生成され、データファイルサイズが 24 MB で、30,000 件のレコードを含む）。

   ![table_single_column](/help/forms/using/assets/table_single_column.png)

1. 多数の小さな列を持つテーブル（800 ページの PDF が生成され、データファイルサイズが 4.6 MB で、20,000 件のレコードを含む）。
   ![table_many_small_columns](/help/forms/using/assets/table_many_small_columns.png)

1. 多数の小さな列を持つテーブル（より大きな xml タグ名を使用しているので、データファイルがより大きくなる）。
これは前のテーブルと同じですが、xml タグ名が大きくなっており（そのため実際の有効なデータが増えずにデータファイルサイズが大きくなる）、最終結果（上限）はほぼ同じです。ただし、データファイルサイズは 4.6 MB から 44.6 MB に増加しました。このテーブルでは、800 ページの PDF が生成され、データファイルサイズが 44.6 MB で、20,000 件のレコードを含んでいます。

   ![table_bigger_xml_tagname](/help/forms/using/assets/table_bigger_xml_tagname.png)

したがって、データファイルサイズに一般的な上限を設けるのは困難です。各フォームは固有のものなので、メモリ消費量はフォームごとに異なります。
