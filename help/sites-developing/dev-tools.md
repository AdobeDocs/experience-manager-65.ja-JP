---
title: 開発ツール
description: JCR、Apache Sling、またはAdobe Experience Managerアプリケーションを開発するために、いくつかのツールセットを使用できます。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: 97310ed5-f8fb-416c-8a66-68f652abeaa0
source-git-commit: fc2f26a69c208947c14e8c6036825bb217901481
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 35%

---

# 開発ツール{#development-tools}

JCR、Apache Sling、またはAdobe Experience Manager(AEM) アプリケーションを開発するには、次のツールセットを使用できます。

* [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) と WebDAV で構成されたツールセット。CRXDE Lite は CRX／AEM に搭載されており、これを使用してブラウザー内で標準的な開発作業を実行できます。CRXDE Liteを使用すると、SVN とのログ記録と統合時に、ファイル（.jspや.java など）、フォルダ、テンプレート、コンポーネント、ダイアログ、ノード、プロパティ、バンドルを作成および編集できます。

  CRX/AEMサーバーに直接アクセスできない場合、標準コンポーネントと Java™バンドルを拡張または変更してアプリケーションを開発する場合、または専用のデバッガー、コード補完、構文のハイライトが必要ない場合に、CRXDE Liteをお勧めします。

* 次のセットで構成される 1 つのセット：
   * 統合開発環境。 例： [Eclipse](/help/sites-developing/howto-projects-eclipse.md) または [IntelliJ](/help/sites-developing/ht-intellij.md).
   * ビルドツール。 例： [Apache Maven](/help/sites-developing/ht-projects-maven.md).
   * FileVault は、リポジトリをファイルシステム（バージョン管理システム）にマッピングするためにAdobeが開発しました。 例えば、Subversion と入力します。
   * バグトラッカーシステム。 例えば、Jira。
   * 中央依存管理システム。 例えば、Apache Archiva などです。
   * ビルドオートメーションシステム。 例えば、Apache Continuum などです。

  このセットアップにより、アプリケーション（コンテンツ、コード、設定）をあらゆる開発環境およびプロセスに完全に統合できます。 前述のすべての開発ツールでファイルを操作できるので、異なる要素間のリンクは、FileVault を介したリポジトリのファイルシステム表現です。

## 統合開発環境の拡張 {#extensions-for-integrated-development-environments}

Adobeは、次の拡張機能をリリースしました。

* [AEM Eclipse 拡張](/help/sites-developing/aem-eclipse.md)
* [AEM Brackets Extension](/help/sites-developing/aem-brackets.md)

### その他のツール {#other-tools}

AEMには、開発を容易にする他のツールが付属しています。

* [ダイアログエディター](/help/sites-developing/dialog-editor.md)
* [トランスレーターを使用した辞書の管理](/help/sites-developing/i18n-translator.md)
* [Maven を使用したパッケージの管理](/help/sites-developing/vlt-mavenplugin.md)
* [Eclipse を使用して AEM プロジェクトを開発する方法](/help/sites-developing/howto-projects-eclipse.md)
* [Apache Maven を使用して AEM プロジェクトをビルドする方法](/help/sites-developing/ht-projects-maven.md)
* [IntelliJ IDEA を使用して AEM プロジェクトを開発する方法](/help/sites-developing/ht-intellij.md)
* [VLT ツールを使用する方法](/help/sites-developing/ht-vlttool.md)
* [プロキシサーバーツールを使用する方法](/help/sites-developing/ht-proxy-server.md)
* [AEM Modernization Tools](/help/sites-developing/modernization-tools.md)
* [AEM Repo ツール](/help/sites-developing/aem-repo-tool.md)

以下は、新しいプロジェクトの作成に役立つツールです。

* [AEM プロジェクトアーキタイプ](https://github.com/adobe/aem-project-archetype)
* [AEM Lazybones テンプレート](https://github.com/Adobe-Consulting-Services/lazybones-aem-templates)

>[!NOTE]
>
>新しい AEM プロジェクトを開始する際には、次のチュートリアルが参考になる場合があります。
>[AEM Sites の概要（第 1 章）- プロジェクトの設定](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop/part1.html)
