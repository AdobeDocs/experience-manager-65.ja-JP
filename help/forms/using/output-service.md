---
title: Output サービス
description: AEM Document Services の一部である Output Service を記述します
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
docset: aem65
exl-id: 1b62e1c1-428d-4c0f-98a8-486f319fa581
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 60%

---

# Output サービス{#output-service}

## 概要 {#overview}

出力サービスは、AEM ドキュメントサービスの一部を成す OSGi サービスです。出力サービスは、様々な出力形式や、AEM Forms Designer の出力設計機能をサポートしています。出力サービスでは、XFA テンプレートと XML データを変換して、様々な形式の印刷ドキュメントを生成することができます。

出力サービスを使用すると、次のことを可能にするアプリケーションを作成できます。

* テンプレートファイルに XML データを格納することで、最終形式のドキュメントを生成する。
* 非インタラクティブPDF、ポストスクリプト、PCL、ZPL の印刷ストリームなど、様々な形式で出力フォームを生成します。
* XFA フォームの PDF ファイルから印刷用 PDF を生成する。
* 付属のテンプレートを用いて複数のデータセットを結合することにより、PDF、ポストスクリプト、PCL および ZPL の形式のドキュメントを一括生成する

>[!NOTE]
>
>出力サービスは 32 ビットアプリケーションです。 Microsoft Windows では、32 ビットアプリケーションで最大 2 GB のメモリを使用できます。 この制限は、出力サービスにも適用されます。

## 非インタラクティブ形式のドキュメントを作成する {#creating-non-interactive-form-documents}

![usingoutput_modified](assets/usingoutput_modified.png)

通常、テンプレートは AEM Forms Designer を使用して作成します。これらのテンプレートは、出力サービスの `generatePDFOutput` と `generatePrintedOutput` の各 API により、PDF、ポストスクリプト、ZPL や PCL などの様々な形式に直接変換することができます。

`generatePDFOutput` 操作は PDF を生成する一方で、`generatePrintedOutput` 操作は、PostScript、ZPL、および PCL の形式でドキュメントを生成します。両方の操作の最初のパラメーターは、テンプレートファイルの名前 ( 例： `ExpenseClaim.xdp`) またはテンプレートを格納する Document オブジェクト。 テンプレートファイルの名前を指定した場合は、テンプレートを含むフォルダへのパスとしてのコンテンツルートも指定します。コンテンツルートの指定には、`PDFOutputOptions` または `PrintedOutputOptions` パラメータのいずれかを使用します。これらのパラメータを使用して指定できる他のオプションの詳細は、Javadoc を参照してください。

2 番目のパラメーターは、出力ドキュメントの生成中にテンプレートと結合される XML ドキュメントを受け取ります。

`generatePDFOutput` 演算では、XFA ベースの PDF フォームを入力として受け取り、出力として非インタラクティブの PDF フォームを返すこともできます。

## 非インタラクティブフォームドキュメントの生成 {#generating-non-interactive-form-documents}

例えば、1 つ以上のテンプレートが存在しており、各テンプレートには XML データの複数のレコードがあるシナリオを考えてみましょう。

各レコードの印刷文書を生成するために、出力サービスの `generatePDFOutputBatch` と `generatePrintedOutputBatch` の演算を使用します。

また、レコードを 1 つのドキュメントに組み合わせることもできます。 どちらの演算も 4 つのパラメータを取ります。

最初のパラメータは、任意の文字列をキーとし、テンプレートファイルの名前を値として含むマップです。

2 番目のパラメータは別のマップです。この値は、XML データを含む Document オブジェクトです。 キーは、最初のパラメーターに指定したキーと同じです。

`generatePDFOutputBatch` または `generatePrintedOutputBatch` の 3 番目のパラメーターは、それぞれ `PDFOutputOptions` タイプまたは `PrintedOutputOptions` タイプです。

パラメータータイプは `generatePDFOutput` と `generatePrintedOutput` 演算のためのパラメーターのタイプと同じで、効果も同じです。

第 4 のパラメーターはタイプ `BatchOptions` です。これは、レコードごとに別のファイルを生成するかどうかを指定するために使用します。このパラメータのデフォルト値は false です。

`generatePrintedOutputBatch` と `generatePDFOutputBatch` は、共にタイプ `BatchResult` の値を返します。値には、生成されたドキュメントのリストが含まれます。 また、XML 形式のメタデータドキュメントも含まれ、この中には、生成される各ドキュメントに関する情報が格納されます。
