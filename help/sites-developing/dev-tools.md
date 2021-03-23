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
source-git-commit: 7035c19a109ff67655ee0419aa37d1723e2189cc
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 62%

---


# 開発ツール{#development-tools}

JCR、Apache Sling または AEM のアプリケーションを開発するために、以下のツールセットが用意されています。

* [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)とWebDAVで構成される1セット。 CRXDE Lite は CRX／AEM に搭載されており、これを使用してブラウザー内で標準的な開発作業を実行できます。CRXDE Lite を使用すると、ファイル（.jsp、.java など）、フォルダー、テンプレート、コンポーネント、ダイアログ、ノード、プロパティおよびバンドルを作成、編集することができ、さらに SVN によるロギングや統合が可能です。

   CRX/AEMサーバーに直接アクセスできない場合、標準搭載のコンポーネントとJavaバンドルを拡張または変更してアプリケーションを開発する場合、または専用のデバッガー、コード完了、構文のハイライトが不要な場合は、CRXDE Liteをお勧めします。

* 統合開発環境から成る1セット(例：[Eclipse](/help/sites-developing/howto-projects-eclipse.md)または[IntelliJ](/help/sites-developing/ht-intellij.md))、ビルドツール(例：[Apache Maven](/help/sites-developing/ht-projects-maven.md))、Adobeがリポジトリをファイルシステム、バージョン管理システム(例：Subversion)、バグトラッカーシステム(例：(Jira)は、中央依存関係管理システム(例：Apache Archiva)とビルド自動化システム(例：Apache Continuum)。

   このセットアップで、アプリケーション（コンテンツ、コード、設定）をあらゆる開発環境とプロセスに完全に統合できます。リポジトリのファイルシステムは FileVault によって様々な要素間のリンクで表わされ、前述のすべての開発ツールでファイルを操作できます。

## 統合開発環境の拡張機能 {#extensions-for-integrated-development-environments}

アドビは以下の拡張機能をリリースしました。

* [AEM Eclipse 拡張](/help/sites-developing/aem-eclipse.md)
* [AEM Brackets Extension](/help/sites-developing/aem-brackets.md)
* [AEM IntelliJ 拡張](https://github.com/headwirecom/aem-ide-tooling-4-intellij/blob/master/documenation/AEM%20Tooling%20Plugin%20for%20IntelliJ%20IDEA.pdf)（Headwire）

### その他のツール  {#other-tools}

AEM には開発に役立つその他のツールが付属しています。

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

* [AEM プロジェクトアーキタイプ](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype)
* [AEM Lazybones テンプレート](https://github.com/Adobe-Consulting-Services/lazybones-aem-templates)

>[!NOTE]
>
>次のチュートリアルは、新しいAEMプロジェクトを開始する際に役立つ場合があります。
>[AEM Sitesの使用の手引き1 — プロジェクトのセットアップ](https://helpx.adobe.com/jp/experience-manager/kt/sites/using/getting-started-wknd-tutorial-develop/part1.html)

