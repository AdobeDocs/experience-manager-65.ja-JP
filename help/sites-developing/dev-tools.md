---
title: 開発ツール
seo-title: 開発ツール
description: JCR、Apache Sling または AEM のアプリケーションを開発するために、多くのツールセットが用意されています
seo-description: JCR、Apache Sling または AEM のアプリケーションを開発するために、多くのツールセットが用意されています
uuid: 1bee3a52-5d76-4b0c-a222-a02e12ff3a43
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 76c570e5-46ed-46be-9864-4fe4a83f0caf
translation-type: tm+mt
source-git-commit: c13eabdf4938a47ddf64d55b00f845199591b835
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 62%

---


# 開発ツール{#development-tools}

JCR、Apache Sling または AEM のアプリケーションを開発するために、以下のツールセットが用意されています。

* one set consisting of [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) and WebDAV. CRXDE Lite は CRX／AEM に搭載されており、これを使用してブラウザー内で標準的な開発作業を実行できます。CRXDE Lite を使用すると、ファイル（.jsp、.java など）、フォルダー、テンプレート、コンポーネント、ダイアログ、ノード、プロパティおよびバンドルを作成、編集することができ、さらに SVN によるロギングや統合が可能です。

   CRX/AEMサーバーに直接アクセスできない場合、標準搭載のコンポーネントとJavaバンドルを拡張または変更してアプリケーションを開発する場合、または専用のデバッガー、コード完了、構文のハイライトが不要な場合に、CRXDE Liteをお勧めします。

* one set consisting of an Integrated Development Environment (for example: [Eclipse](/help/sites-developing/howto-projects-eclipse.md) or [IntelliJ](/help/sites-developing/ht-intellij.md)), a build tool (for example: [Apache Maven](/help/sites-developing/ht-projects-maven.md)), FileVault which has been developed by Adobe to map a repository to a file system, a version control system (for example: Subversion), a bug tracker system (for example: Jira), a central dependency management system (for example: Apache Archiva) and a build automation system (for example: Apache Continuum).

   このセットアップで、アプリケーション（コンテンツ、コード、設定）をあらゆる開発環境とプロセスに完全に統合できます。リポジトリのファイルシステムは FileVault によって様々な要素間のリンクで表わされ、前述のすべての開発ツールでファイルを操作できます。

## 統合開発環境の拡張機能 {#extensions-for-integrated-development-environments}

アドビは以下の拡張機能をリリースしました。

* [AEM Eclipse 拡張](/help/sites-developing/aem-eclipse.md)
* [AEM Brackets Extension](/help/sites-developing/aem-brackets.md)
* [AEM IntelliJ 拡張](https://github.com/headwirecom/aem-ide-tooling-4-intellij/blob/master/documenation/AEM%20Tooling%20Plugin%20for%20IntelliJ%20IDEA.pdf)（Headwire）

### その他のツール {#other-tools}

AEM には開発に役立つその他のツールが付属しています。

* [ダイアログエディター](/help/sites-developing/dialog-editor.md)
* [トランスレーターを使用した辞書の管理](/help/sites-developing/i18n-translator.md)
* [Maven を使用したパッケージの管理](/help/sites-developing/vlt-mavenplugin.md)
* [Eclipse を使用して AEM プロジェクトを開発する方法](/help/sites-developing/howto-projects-eclipse.md)
* [Apache Maven を使用して AEM プロジェクトをビルドする方法](/help/sites-developing/ht-projects-maven.md)
* [IntelliJ IDEA を使用して AEM プロジェクトを開発する方法](/help/sites-developing/ht-intellij.md)
* [VLT ツールを使用する方法](/help/sites-developing/ht-vlttool.md)
* [プロキシサーバーツールを使用する方法](/help/sites-developing/ht-proxy-server.md)
* [ダイアログ変換ツール](/help/sites-developing/dialog-conversion.md)
* [AEM Repo ツール](/help/sites-developing/aem-repo-tool.md)

以下は、新しいプロジェクトの作成に役立つツールです。

* [AEM プロジェクトアーキタイプ](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)
* [AEM Lazybones テンプレート](https://github.com/Adobe-Consulting-Services/lazybones-aem-templates)

>[!NOTE]
>
>次のチュートリアルは、新しいAEMプロジェクトを開始する際に役立つ場合があります。
>[Getting Started with AEM Sites Part 1 - Project Setup](https://helpx.adobe.com/jp/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop/part1.html)

