---
title: AEM Repo ツール
seo-title: AEM Repo Tool
description: AEM Repo ツールは、FTP に相当するコマンドラインを使用してローカルファイルシステムと AEM サーバーの間で JCR コンテンツを転送するためのシンプルなソリューションです。AEM Repo ツールは、Jackrabbit FileVault ツールに似ていますが、より高速で依存関係が極めて少ない、シンプルな bash スクリプトです。
seo-description: The AEM Repo Tool is a simple solution to transfer JCR content between your local filesystem and the AEM server via the command line comparable to FTP. The AEM Repo Tool is similar to the Jackrabbit FileVault tool, but is faster, has minimal dependencies, and is a simple bash script.
uuid: 6c4a3504-e8e8-46c0-83cb-c18d9791f93e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 7de7b2f9-770e-4af3-8a31-c7b4de64fd43
exl-id: c46c9f0c-b0d2-4f2f-b95c-90fd3ced32a9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '284'
ht-degree: 100%

---

# AEM Repo ツール{#aem-repo-tool}

AEM Repo ツールは、FTP に相当するコマンドラインを使用してローカルファイルシステムと AEM サーバーの間で JCR コンテンツを転送するためのシンプルなソリューションです。AEM Repo ツールは、[Jackrabbit FileVault ツール](/help/sites-developing/ht-vlttool.md)に似ていますが、より高速で依存関係が最小限であり、シンプルな bash スクリプトです。

このツールは、開発者によるファイルの転送をシンプルにします。また、IntelliJ および Eclipse と統合して開発をより効率的にできます。

## 概要 {#overview}

ファイルシステム上の `jcr_root` filevault 構造内の特定のパスの場合、AEM Repo ツールは、サブツリー全体に対する単一のフィルターを含むパッケージを作成し、それをサーバーにプッシュして（FTP の `put` と同じ）、サーバーから取得（`get`）または違いを比較（`status` および `diff`）します。

このツールは、複数のフィルターパスや FileVault の `filter.xml` をサポートしません。

>[!CAUTION]
>
>AEM Repo ツールは、指定したファイル全体またはディレクトリを常に上書きすることに注意してください。

## ダウンロードとドキュメント {#download-and-documentation}

[AEM Repo ツールは、このリンクの GitHub で利用できます](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo)。詳細なインストールおよび使用手順も用意されています。

AEM Repo ツールのソースをダウンロードする場合は、GitHub プロジェクト（次のリンク）を参照してください。

GitHub のコード

このページのコードは GitHub にあります

* [GitHub でツールのプロジェクトを開きます](https://github.com/Adobe-Marketing-Cloud/tools)
* プロジェクトを [ZIP ファイル](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)としてダウンロードします
