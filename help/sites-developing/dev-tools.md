---
title: 開発ツール
description: JCR、Apache Sling または Adobe Experience Manager のアプリケーションを開発するために、いくつかのツールセットが用意されています。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: 97310ed5-f8fb-416c-8a66-68f652abeaa0
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 100%

---

# 開発ツール{#development-tools}

JCR、Apache Sling または Adobe Experience Manager（AEM）のアプリケーションを開発するために、以下のツールセットが用意されています。

* [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) と WebDAV で構成されたツールセット。CRXDE Lite は CRX／AEM に搭載されており、これを使用してブラウザー内で標準的な開発作業を実行できます。CRXDE Lite を使用すると、ファイル（.jsp、.java など）、フォルダー、テンプレート、コンポーネント、ダイアログ、ノード、プロパティ、バンドルを作成および編集することができ、さらに SVN によるロギングや統合が可能です。

  CRXDE Lite は、CRX／AEM サーバーに直接アクセスできない場合、すぐに使用可能なコンポーネントと Java™ バンドルを拡張または変更してアプリケーションを開発する場合、または専用のデバッガー、コード補完および構文のハイライト表示を必要としない場合にお勧めします。

* 以下で構成されたツールセット：
   * 統合開発環境。例：[Eclipse](/help/sites-developing/howto-projects-eclipse.md) または [IntelliJ](/help/sites-developing/ht-intellij.md)。
   * ビルドツール。例：[Apache Maven](/help/sites-developing/ht-projects-maven.md)。
   * リポジトリをファイルシステム、バージョン管理システムにマッピングするために開発された FileVault。例：Subversion。
   * バグ追跡システム。例：JIRA。
   * 依存関係中央管理システム。例：Apache Archiva。
   * ビルド自動化システム。例：Apache Continuum。

  この設定で、アプリケーション（コンテンツ、コード、設定）をあらゆる開発環境とプロセスに完全に統合できます。リポジトリのファイルシステムは FileVault によって様々な要素間のリンクで表わされ、前述のすべての開発ツールでファイルを操作できます。

## 統合開発環境の拡張機能 {#extensions-for-integrated-development-environments}

アドビは以下の拡張機能をリリースしました。

* [AEM Eclipse 拡張](/help/sites-developing/aem-eclipse.md)
* [AEM Brackets Extension](/help/sites-developing/aem-brackets.md)

### その他のツール {#other-tools}

AEM には、開発に役立つその他のツールが付属しています。

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
