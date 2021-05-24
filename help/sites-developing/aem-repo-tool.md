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
exl-id: c46c9f0c-b0d2-4f2f-b95c-90fd3ced32a9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 80%

---

# AEM Repo ツール{#aem-repo-tool}

AEM Repo ツールは、FTP に相当するコマンドラインを使用してローカルファイルシステムと AEM サーバーの間で JCR コンテンツを転送するためのシンプルなソリューションです。AEM Repo Toolは[Jackrabbit FileVaultツール](/help/sites-developing/ht-vlttool.md)に似ていますが、より高速で、依存関係が最小限で、単純なbashスクリプトです。

このツールは、開発者によるファイルの転送をシンプルにします。また、IntelliJ および Eclipse と統合して開発をより効率的にできます。

## 概要 {#overview}

ファイルシステム上の`jcr_root`ファイルバルト構造内の特定のパスに対して、AEM Repo Toolは、サブツリー全体に対して単一のフィルターを持つパッケージを作成し、（FTP `put`と同様に）サーバーにプッシュし、サーバー( `get` )から取得するか、違い（ `status`と`diff`）を比較します。

このツールは、複数のフィルターパスや FileVault の `filter.xml` をサポートしません。

>[!CAUTION]
>
>AEM Repo ツールは、指定したファイル全体またはディレクトリを常に上書きすることに注意してください。

## ダウンロードとドキュメント  {#download-and-documentation}

[AEM Repo ツールは、このリンクの GitHub で利用できます](https://github.com/Adobe-Marketing-Cloud/tools/tree/master/repo)。詳細なインストールおよび使用手順も用意されています。

AEM Repo ツールのソースをダウンロードする場合は、GitHub プロジェクト（次のリンク）を参照してください。

GitHub のコード

このページのコードは GitHub にあります

* [GitHub でツールのプロジェクトを開きます](https://github.com/Adobe-Marketing-Cloud/tools)
* プロジェクトを [ZIP ファイル](https://github.com/Adobe-Marketing-Cloud/tools/archive/master.zip)としてダウンロードします
