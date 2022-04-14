---
title: リクエスト分析スクリプト
seo-title: Request Analysis Script
description: このリクエスト分析スクリプトは、access.log ファイルの分析を簡易化し、後の処理で役立つようにわかりやすいレポートを生成します。
seo-description: The request analysis script is made to ease the analysis of the access.log files producing a readable report for later processing
uuid: 24eff3c6-5748-46f3-a30c-4a3a6427ce1d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 1b5e0ccf-4157-45e3-8caf-1d6739d7d9d2
exl-id: e14a9cda-890f-46b7-9433-1b52eb91eae3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '171'
ht-degree: 100%

---

# リクエスト分析スクリプト{#request-analysis-script}

## ダウンロード {#download}

このスクリプトは、`access.log` ファイルの分析を簡易化し、後の処理で役立つようにわかりやすいレポートを生成します。

[ファイルを入手](assets/analyse-access.sh)

## 説明 {#description}

このスクリプトは、`access.log` ファイルの分析を簡易化し、後の処理で役立つようにわかりやすいレポートを生成します。

このスクリプトは、リクエストの全体番号、GET 対 POST、リクエスト配信の推移など多くのデータを生成します。

出力は Markdown 構文で記述されるので、Pandoc などのツールを使用して PDF に容易に変換できます。また、Markdown ビューアなどのプラグインを使用すれば、ブラウザーに出力を容易に表示することもできます。

コマンドラインで指定されるカスタムパスも分析できます。

実行方法を示すファイル内のコメントを参照します。

CQ `access.log` を分析して様々な情報を推測し、Markdown 出力を `stdout` で生成します。

## 使用方法 {#usage}

`./analyse-access.sh access.log.2013-&ast;`

コマンドラインにカスタムパスを追加して、詳細に分析することもできます。

`/analyse-access.sh access.log.2013-&ast; /my/custom/path/1 /my/custom/path/2`

出力はシンプルなパイプ処理で保存できます。

`./analyse-access.sh access.log.2013-&ast; | tee yr2013.md`
