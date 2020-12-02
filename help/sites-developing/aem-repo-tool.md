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

AEM Repo ツールは、FTP に相当するコマンドラインを使用してローカルファイルシステムと AEM サーバーの間で JCR コンテンツを転送するためのシンプルなソリューションです。AEM Repo Toolは[Jackrabbit FileVaultツール](/help/sites-developing/ht-vlttool.md)に似ていますが、高速で依存性が最小限で、単純なbashスクリプトです。

このツールは、開発者によるファイルの転送をシンプルにします。また、IntelliJ および Eclipse と統合して開発をより効率的にできます。

## 概要 {#overview}

ファイルシステム上の`jcr_root`ファイルの結果構造内の特定のパスに対して、AEM Repo Toolはサブツリー全体に対して単一のフィルタを持つパッケージを作成し（FTP `put`と同様）、サーバから取り込むか（ `status`と`diff`）、差を比較します。`get`

このツールは、複数のフィルタパスまたはFileVaultの`filter.xml`をサポートしていません。

>[!CAUTION]
>
>AEM Repo ツールは、指定したファイル全体またはディレクトリを常に上書きすることに注意してください。

## ダウンロードとドキュメント  {#download-and-documentation}

[AEM Repo Toolは、GitHub上で、このリンク](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo)と共に、詳細なインストールおよび使用方法に関する説明と共に利用できます。

AEM Repo ツールのソースをダウンロードする場合は、GitHub プロジェクト（次のリンク）を参照してください。

GitHub のコード

このページのコードは GitHub にあります

* [GitHubでツールプロジェクトを開く](https://github.com/Adobe-Marketing-Cloud/tools)
* プロジェクトを [ZIP ファイル](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)としてダウンロードします

