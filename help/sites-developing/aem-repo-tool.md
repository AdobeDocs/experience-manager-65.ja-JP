---
title: AEM Repo ツール
description: AEM Repo Tool は、FTP に相当するコマンドラインを使用して、ローカルファイルシステムとAEMサーバーの間で JCR コンテンツを転送する簡単なソリューションです。 AEM Repo ツールは、Jackrabbit FileVault ツールに似ていますが、より高速で依存関係が最小限であり、シンプルな bash スクリプトです。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: c46c9f0c-b0d2-4f2f-b95c-90fd3ced32a9
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 74%

---

# AEM Repo ツール{#aem-repo-tool}

AEM Repo ツールは、FTP に相当するコマンドラインを使用してローカルファイルシステムと AEM サーバーの間で JCR コンテンツを転送するためのシンプルなソリューションです。AEM Repo ツールは、[Jackrabbit FileVault ツール](/help/sites-developing/ht-vlttool.md)に似ていますが、より高速で依存関係が最小限であり、シンプルな bash スクリプトです。

このツールは、開発者向けのファイルの転送を簡素化し、IntelliJ と Eclipse に統合して開発をより効率的にすることもできます。

## 概要 {#overview}

ファイルシステム上の `jcr_root` filevault 構造内の特定のパスの場合、AEM Repo ツールは、サブツリー全体に対する単一のフィルターを含むパッケージを作成し、それをサーバーにプッシュして（FTP の `put` と同じ）、サーバーから取得（`get`）または違いを比較（`status` および `diff`）します。

このツールは、複数のフィルターパスや FileVault の `filter.xml` をサポートしません。

>[!CAUTION]
>
>AEM Repo Tool は、常に、指定されたファイルまたはディレクトリ全体を上書きします。

## ダウンロードとドキュメント {#download-and-documentation}

[AEM Repo ツールは、このリンクの GitHub で利用できます](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo)。詳細なインストールおよび使用手順も用意されています。

AEM Repo Tool のソースをダウンロードする場合は、以下にリンクされている GitHub プロジェクトを参照してください。

GitHub のコード

このページのコードは GitHub にあります

* [GitHub でツールのプロジェクトを開きます](https://github.com/Adobe-Marketing-Cloud/tools)
* プロジェクトを [ZIP ファイル](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)としてダウンロードします
