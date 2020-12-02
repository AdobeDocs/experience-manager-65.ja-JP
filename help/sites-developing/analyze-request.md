---
title: リクエスト分析スクリプト
seo-title: リクエスト分析スクリプト
description: このリクエスト分析スクリプトは、access.log ファイルの分析を簡易化し、後の処理で役立つようにわかりやすいレポートを生成します。
seo-description: このリクエスト分析スクリプトは、access.log ファイルの分析を簡易化し、後の処理で役立つようにわかりやすいレポートを生成します。
uuid: 24eff3c6-5748-46f3-a30c-4a3a6427ce1d
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: testing
content-type: reference
discoiquuid: 1b5e0ccf-4157-45e3-8caf-1d6739d7d9d2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 36%

---


# リクエスト分析スクリプト{#request-analysis-script}

## ダウンロード {#download}

このスクリプトは、後で処理するために読み取り可能なレポートを生成する`access.log`ファイルの分析を容易にするために作成されました。

[ファイルを入手](assets/analyse-access.sh)

## 説明 {#description}

このスクリプトは、後で処理するために読み取り可能なレポートを生成する`access.log`ファイルの分析を容易にするために作成されました。

このスクリプトは、リクエストの全体番号、GET 対 POST、リクエスト配信の推移など多くのデータを生成します。

出力はMarkdown構文になっているので、pandocなどのツールを使用してPDFに変換したり、Markdown Viewerなどのプラグインを使用してブラウザーに表示したりすると、より簡単に行えます。

コマンドラインで提供されたカスタムパスを分析できます。

ファイル内のコメントから、その実行方法を示す情報を取得します。

CQ `access.log`を分析し、さまざまな情報を推定して`stdout`上でMarkdown出力を生成します。

## 使用方法 {#usage}

`./analyse-access.sh access.log.2013-&ast;`

コマンドラインで分析するカスタムパスを追加することができます

`/analyse-access.sh access.log.2013-&ast; /my/custom/path/1 /my/custom/path/2`

出力は、単純なパイピングで保存できます

`./analyse-access.sh access.log.2013-&ast; | tee yr2013.md`
