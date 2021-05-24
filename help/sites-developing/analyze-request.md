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
exl-id: e14a9cda-890f-46b7-9433-1b52eb91eae3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 36%

---

# リクエスト分析スクリプト{#request-analysis-script}

## ダウンロード {#download}

このスクリプトは、後で処理するために読み取り可能なレポートを生成する`access.log`ファイルの分析を容易にするように作られています。

[ファイルを入手](assets/analyse-access.sh)

## 説明 {#description}

このスクリプトは、後で処理するために読み取り可能なレポートを生成する`access.log`ファイルの分析を容易にするように作られています。

このスクリプトは、リクエストの全体番号、GET 対 POST、リクエスト配信の推移など多くのデータを生成します。

出力はMarkdown構文なので、pandocなどのツールを使用してPDFに変換したり、Markdownビューアなどのプラグインを使用してブラウザーに表示したりすると、より簡単になります。

コマンドラインで提供されたカスタムパスを分析できます。

ファイル内のコメントから、実行方法を示すコメントを取得します。

CQ `access.log`を分析し、様々な情報を推定し、`stdout`にMarkdown出力を生成します。

## 使用方法 {#usage}

`./analyse-access.sh access.log.2013-&ast;`

コマンドラインで分析する追加のカスタムパスを指定できます。

`/analyse-access.sh access.log.2013-&ast; /my/custom/path/1 /my/custom/path/2`

出力は、単純な配管で保存できます

`./analyse-access.sh access.log.2013-&ast; | tee yr2013.md`
