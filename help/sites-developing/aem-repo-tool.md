---
title: AEM Repo ツール
seo-title: AEM Repo ツール
description: AEM Repo ツールは、FTP に相当するコマンドラインを使用してローカルファイルシステムと AEM サーバーの間で JCR コンテンツを転送するためのシンプルなソリューションです。AEM Repo ツールは、Jackrabbit FileVault ツールに似ていますが、より高速で依存関係が極めて少ない、シンプルな bash スクリプトです。
seo-description: AEM Repo ツールは、FTP に相当するコマンドラインを使用してローカルファイルシステムと AEM サーバーの間で JCR コンテンツを転送するためのシンプルなソリューションです。AEM Repo ツールは、Jackrabbit FileVault ツールに似ていますが、より高速で依存関係が極めて少ない、シンプルな bash スクリプトです。
uuid: 6c4a3504-e8e8-46c0-83cb-c18d9791f93e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 7de7b2f9-770e-4af3-8a31-c7b4de64fd43
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 70%

---


# AEM Repo ツール{#aem-repo-tool}

AEM Repo ツールは、FTP に相当するコマンドラインを使用してローカルファイルシステムと AEM サーバーの間で JCR コンテンツを転送するためのシンプルなソリューションです。The AEM Repo Tool is similar to the [Jackrabbit FileVault tool](/help/sites-developing/ht-vlttool.md), but is faster, has minimal dependencies, and is a simple bash script.

このツールは、開発者によるファイルの転送をシンプルにします。また、IntelliJ および Eclipse と統合して開発をより効率的にできます。

## 概要 {#overview}

For a given path inside a `jcr_root` filevault structure on the filesystem, AEM Repo Tool creates a package with a single filter for the entire subtree and pushes that to the server (similar to FTP `put`), fetches it from the server ( `get`) or compares the differences ( `status` and `diff`).

The tool does not support multiple filter paths or FileVault&#39;s `filter.xml`.

>[!CAUTION]
>
>AEM Repo ツールは、指定したファイル全体またはディレクトリを常に上書きすることに注意してください。

## ダウンロードとドキュメント {#download-and-documentation}

The [AEM Repo Tool is available on GitHub via this link](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo) along with detailed installation and usage instructions.

AEM Repo ツールのソースをダウンロードする場合は、GitHub プロジェクト（次のリンク）を参照してください。

GitHub のコード

このページのコードは GitHub にあります

* [GitHubでツールプロジェクトを開く](https://github.com/Adobe-Marketing-Cloud/tools)
* プロジェクトを [ZIP ファイル](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)としてダウンロードします

