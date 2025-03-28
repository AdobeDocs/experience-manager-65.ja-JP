---
title: JEE 上のAEM Formsに対する Spring Framework の脆弱性の軽減
description: JEE 上のAEM Formsに対する Spring Framework の脆弱性の軽減
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: 61cce7cd8290156bec6dcc351a59093f545a4ec7
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 2%

---


# JEE 上のAEM Formsの Spring Framework の脆弱性の軽減

このドキュメントでは、JEE 上のAEM Formsに影響を与える Spring Framework の 2 つの重要な脆弱性に対処する際のガイダンスを提供します。

- **[CVE-2024-38819](https://spring.io/security/cve-2024-38819)**：機能 web フレームワークのパストラバーサルの脆弱性
- **[CVE-2024-38820](https://spring.io/security/cve-2024-38820)**:Spring Framework DataBinder で大文字と小文字を区別して一致する例外が発生しました

## 影響を受けるバージョン

- JEE 上のAdobe Experience Manager 6.5 Forms
- バージョン AEM 6.5 Forms GA から 6.5.22.0 へ

## 解決策

### バージョン固有のソリューション

| AEM Forms バージョン | 必須のアクション |
|-------------------|-----------------|
| 6.5.22.0 | 1. [ お使いの環境のホットフィックスをダウンロードします ](/help/release-notes/aem-forms-hotfix.md)。 </br>2.この修正プログラムをインストールするには、手順に従って [JEE 上のAEM フォームへのサービスパックのインストール ](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md) を行います。 |
| 6.5.17.0 - 6.5.21.0 | [ 手動による軽減手順を適用する ](#manual-mitigation-steps)。 |
| 6.5 - 6.5.16.0 | 1. [ 最新のサービスパックをインストールする ](/help/release-notes/release-notes.md)<br>2. 更新したバージョンに基づいて ](#version-specific-solutions) 適切なソリューションを実装 [ します。 |

> **メモ**:AEM Formsが公式にサポートしているサービスパックは、最新の 6 つのみです。 古いバージョンを使用しているユーザーは、まず最新のサービスパックにアップグレードしてから、必要なホットフィックスをインストールする必要があります。

## デプロイメントに関する考慮事項

### クラスター環境の場合

クラスター化されたデプロイメントを操作する場合：

- クラスター内の **すべてのノード** に JAR ファイルの置換を適用する（手順#4）
- すべてのサーバーで同一の JAR バージョンを使用して一貫性を維持する
- サービスを再起動する前に、すべてのノードの更新を完了してください
- システムのダウンタイムを最小限に抑えるための調整済みの再起動戦略を導入

### 単一ノード環境の場合

スタンドアロンデプロイメントで作業する場合：

- 管理するロケーターサーバーがないため、簡略化されたプロセスに従います
- ロケーターサーバーの構成または起動に関連する手順を省略します
- 指示に従って他のすべての手順、特に JAR の置き換えとマニフェストの更新を完了します
- すべての変更を実装したら、アプリケーションサーバーを再起動します

## 手動による軽減手順

1. アプリケーションサーバーを停止します。
1. およびロケーターサーバーを停止します。
1. コア EAR からスプリング JAR を削除する：
   1. `[Adobe_Experience_Manager_Forms installation directory]/deploy` に移動します。
   1. アーカイブ マネージャ ツールを使用して `adobe-core-<appserver>.ear` ファイルを開きます。 `<appserver>` には、環境に応じて JBoss、WebLogic または WebSphere を指定できます。
   - **JBoss の場合：** `ear/lib` フォルダーに移動し、次の JAR ファイルを削除します。
- `spring-core-<version>.jar`
- `spring-web-<version>.jar`

   - **WebLogic または WebSphere の場合：**EAR のルートから次の JAR ファイルを削除します。
- `spring-core-<version>.jar`
- `spring-web-<version>.jar`

   - **すべてのアプリケーションサーバーの場合：** `adobe-core-<appserver>.ear` のルートレベルで `adobe-dscf.jar` ファイルを開き、`META-INF/MANIFEST.MF` ファイルを編集して、次の JAR ファイルへの参照をすべて削除します。
- `spring-core-<version>.jar`
- `spring-web-<version>.jar`

1. Geode 配布の JAR ファイルを置換：
   1. `<Adobe_Experience_Manager_Forms>/lib/caching/lib` に移動します。
   1. 既存の JAR ファイルを更新後のバージョンに置き換えます。
   - `spring-context-<version>.jar` → `spring-context-6.1.14.jar`
   - `spring-beans-<version>.jar` → `spring-beans-6.1.14.jar`
   - `spring-core-<version>.jar` → `spring-core-6.1.14.jar`
   - `spring-jcl-<version>.jar` → `spring-jcl-6.1.14.jar`
   - `spring-web-<version>.jar` → `spring-web-6.1.14.jar`

   新しい JAR ファイルを取得するには、[Adobe ソフトウェア配布から spring-6.1.14-jars.zip ファイルをダウンロードし ](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/spring-6.1.14-jars.zip)ZIP ファイルを解凍して、更新された Spring Framework JAR ファイルにアクセスします。

   1. 次の JAR ファイルにある MANIFEST.MF ファイルを更新します。
   - `geode-server-all-<version>.jar`
   - `gfsh-dependencies.jar`

   各 JAR に対して：
   - アーカイブマネージャーツールを使用して JAR を開きます
   - `META-INF/MANIFEST.MF` ファイルを見つけて抽出します
   - テキストエディターで MANIFEST.MF ファイルを編集します
   - 「Class-Path」セクションを検索し、すべての Spring フレームワーク参照を更新します。
      - `spring-core-<version>.jar`コピー先：`spring-core-6.1.14.jar`
      - `spring-web-<version>.jar`コピー先：`spring-web-6.1.14.jar`
      - `spring-context-<version>.jar`コピー先：`spring-context-6.1.14.jar`
      - `spring-beans-<version>.jar`コピー先：`spring-beans-6.1.14.jar`
      - `spring-jcl-<version>.jar`コピー先：`spring-jcl-6.1.14.jar`
   - 変更した MANIFEST.MF ファイルを保存
   - JAR 内の元の MANIFEST.MF を更新後のバージョンに置き換えます
   - JAR ファイルを保存

   1. 注意が必要な一般的な問題：
      - マニフェストに重複するエントリがないことを確認します
      - 適切な行末を維持する
      - 参照されているすべての JAR が指定した場所に存在することを確認します

   1. 検証手順：
      - マニフェストが正しく更新されているかどうかを確認します
      - すべての Spring 依存関係が正しく参照されていることを確認します
      - 古いバージョン参照が残らないようにします。
      - アプリケーションをテストして、クラス読み込みの問題がないことを確認します

1. Configuration Manager を実行します。

1. サーバーの再起動：
   - JDK 17 を使用したロケーターサーバーの起動
   - 以前に使用したのと同じ JDK バージョン（JDK 8 または JDK 11）を使用して、アプリケーションサーバーを起動します。
