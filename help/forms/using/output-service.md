---
title: Output サービス
seo-title: Output Service
description: AEM ドキュメントサービスの一部である「出力サービス」の説明
seo-description: Describes Output Service, which is part of AEM Document Services
uuid: edddef59-b43c-486f-8734-3f97961ecf4d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 51ab91ff-c0c0-4165-ae02-f306e45eea03
docset: aem65
exl-id: 1b62e1c1-428d-4c0f-98a8-486f319fa581
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 100%

---

# Output サービス{#output-service}

## 概要 {#overview}

出力サービスは、AEM ドキュメントサービスの一部である OSGi サービスの一種です。出力サービスは、様々な出力形式や、AEM Forms Designer の出力設計機能をサポートしています。出力サービスでは、XFA テンプレートと XML データを変換することにより、様々な形式の印刷ドキュメントを生成することができます。

出力サービスにより、以下のような機能を備えたアプリケーションを作成することができます。

* テンプレートファイルに XML データを格納することで、最終形式のドキュメントを生成する。
* 非インタラクティブ PDF、ポストスクリプト、PCL、および ZPL のプリントストリームを含む様々な形式でフォームを出力する
* XFA フォームの PDF ファイルから印刷用 PDF を生成する。
* 付属のテンプレートを用いて複数のデータセットを結合することにより、PDF、ポストスクリプト、PCL および ZPL の形式のドキュメントを一括生成する

>[!NOTE]
>
>Output サービスは、32 ビットアプリケーションです。Microsoft Windows では、32 ビットアプリケーションが使用できるメモリは最大 2 GB です。この制限は Output サービスにも適用されます。

## 非インタラクティブ形式のドキュメントを作成する {#creating-non-interactive-form-documents}

![usingoutput_modified](assets/usingoutput_modified.png)

通常、テンプレートは AEM Forms Designer を使用して作成します。これらのテンプレートは、出力サービスの `generatePDFOutput` と `generatePrintedOutput` の各 API により、PDF、ポストスクリプト、ZPL や PCL などの様々な形式に直接変換することができます。

`generatePDFOutput` 操作は PDF を生成する一方で、`generatePrintedOutput` 操作は、PostScript、ZPL、および PCL の形式でドキュメントを生成します。各演算の最初のパラメーターは、テンプレートファイルの名前（例えば、`ExpenseClaim.xdp`）、またはテンプレートが含まれているドキュメントオブジェクトのいずれかを受け取ります。テンプレートファイルの名前を指定した場合は、テンプレートを含むフォルダへのパスとしてのコンテンツルートも指定します。コンテンツルートの指定には、`PDFOutputOptions` または `PrintedOutputOptions` パラメータのいずれかを使用します。これらのパラメータを使用して指定できる他のオプションの詳細については、Javadoc を参照してください。

2 番目のパラメーターは、出力ドキュメントの生成中にテンプレートと結合される XML ドキュメントを受け取ります。

`generatePDFOutput` 演算では、XFA ベースの PDF フォームを入力として受け取り、出力として非インタラクティブの PDF フォームを返すこともできます。

## 非インタラクティブ形式のドキュメントを作成する {#generating-non-interactive-form-documents}

例えば、1 つ以上のテンプレートが存在しており、各テンプレートには XML データの複数のレコードがあるシナリオを考えてみましょう。

各レコードの印刷文書を生成するために、出力サービスの `generatePDFOutputBatch` と `generatePrintedOutputBatch` の演算を使用します。

また、単一のドキュメントにレコードを組み合わせることもできます。いずれの演算でも、4 つのパラメータが必要です。

最初のパラメータはマップであり、この中には、任意の文字列が鍵として、およびテンプレートファイルの名前が値として収められています。

2番目のパラメータは別のマップです。この値は、XML データを含むドキュメントオブジェクトです。この鍵は、最初のパラメータに指定したものと同じものです。

`generatePDFOutputBatch` または `generatePrintedOutputBatch` の 3 番目のパラメーターは、それぞれ `PDFOutputOptions` タイプまたは `PrintedOutputOptions` タイプです。

パラメータータイプは `generatePDFOutput` と `generatePrintedOutput` 演算のためのパラメーターのタイプと同じで、効果も同じです。

第 4 のパラメーターはタイプ `BatchOptions` です。これは、レコードごとに別のファイルを生成するかどうかを指定するために使用します。このパラメータのデフォルト値は false です。

`generatePrintedOutputBatch` と `generatePDFOutputBatch` は、共にタイプ `BatchResult` の値を返します。値には、生成されたドキュメントのリストが含まれています。また、XML形式のメタデータドキュメントも含まれており、この中には、生成された各ドキュメントに関連する情報が収められています。
