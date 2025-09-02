---
title: AEM Forms on JEE に関する Spring Framework の脆弱性の軽減
description: AEM Forms on JEE に関する Spring Framework の脆弱性の軽減
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
exl-id: f704b58a-7bd8-401e-8d7e-2cc3b580c570
source-git-commit: d2ae4817720cae92b038789804124e0c2465f9c8
workflow-type: ht
source-wordcount: '563'
ht-degree: 100%

---

# AEM Forms on JEE に関する Spring Framework の脆弱性の軽減

このドキュメントでは、AEM Forms on JEE に影響を与える 2 つの重要な Spring Framework の脆弱性に対処する際のガイダンスを提供します。

- **[CVE-2024-38819](https://spring.io/security/cve-2024-38819)**：関数型 web フレームワークでのパストラバーサルの脆弱性
- **[CVE-2024-38820](https://spring.io/security/cve-2024-38820)**：Spring Framework DataBinder の大文字と小文字を区別する一致例外

## 影響を受けるバージョン

- Adobe Experience Manager 6.5 Forms on JEE
- バージョン AEM 6.5 Forms GA ～6.5.22.0

## 解決策

### バージョン固有の解決策

| AEM Forms バージョン | 必須のアクション |
|-------------------|-----------------|
| 6.5.22.0 | &#x200B;1. [環境のホットフィックスをダウンロードします](/help/release-notes/aem-forms-hotfix.md)。</br>2.この修正をインストールするには、[AEM Form on JEE にサービスパックをインストール](/help/release-notes/aem-forms-current-service-pack-installation-instructions.md)する手順に従います。 |
| 6.5.17.0 - 6.5.21.0 | [手動の軽減手順を適用します](#manual-mitigation-steps)。 |
| 6.5～6.5.16.0 | &#x200B;1. [最新のサービスパックをインストールします](/help/release-notes/release-notes.md)<br>2.更新されたバージョンに基づいて[適切なソリューションを実装します](#version-specific-solutions)。 |

> **メモ**：AEM Forms が公式にサポートしているサービスパックは、最新の 6 つのみです。 古いバージョンのユーザーは、まず最新のサービスパックにアップグレードしてから、必要なホットフィックスをインストールする必要があります。

## デプロイメントに関する考慮事項

### クラスター環境の場合

クラスター化されたデプロイメントを操作する場合：

- クラスター内の&#x200B;**すべてのノード**&#x200B;に JAR ファイルの置換（手順 4）を適用します
- すべてのサーバーで同一の JAR バージョンを使用して一貫性を維持します
- サービスの再起動を開始する前に、すべてのノードで更新を完了します
- システムのダウンタイムを最小限に抑えるために、調整された再起動戦略を実装します

### 単一ノード環境の場合

スタンドアロンデプロイメントを操作する場合：

- 管理するロケーターサーバーがないので、簡素化されたプロセスに従います
- ロケーターサーバーの設定や起動に関連する手順を省略します
- 指示に従って他のすべての手順、特に JAR の置換とマニフェストの更新を完了します。
- すべての変更を実装したら、アプリケーションサーバーを再起動します

## 手動の軽減手順

1. アプリケーションサーバーを停止します。
1. ロケーターサーバーを停止します。
1. コア EAR から Spring JAR を削除します。
   1. `[Adobe_Experience_Manager_Forms installation directory]/deploy` に移動します。
   1. アーカイブマネージャーツールを使用して `adobe-core-<appserver>.ear` ファイルを開きます。`<appserver>` は、環境に応じて JBoss、WebLogic または WebSphere のいずれかに指定できます。
   - **JBoss の場合：**`ear/lib` フォルダーに移動し、次の JAR ファイルを削除します。
- `spring-core-<version>.jar`
- `spring-web-<version>.jar`

   - **WebLogic または WebSphere の場合：**EAR のルートから次の JAR ファイルを削除します。
- `spring-core-<version>.jar`
- `spring-web-<version>.jar`

   - **すべてのアプリケーションサーバーの場合：**`adobe-core-<appserver>.ear` のルートレベルで `adobe-dscf.jar` ファイルを開き、`META-INF/MANIFEST.MF` ファイルを編集して、次の JAR ファイルへの参照を削除します。
- `spring-core-<version>.jar`
- `spring-web-<version>.jar`

1. Geode 配布からの JAR ファイルを置き換えます。
   1. `<Adobe_Experience_Manager_Forms>/lib/caching/lib` に移動します。
   1. 既存の JAR ファイルを更新されたバージョンに置き換えます。
   - `spring-context-<version>.jar` → `spring-context-6.1.14.jar`
   - `spring-beans-<version>.jar` → `spring-beans-6.1.14.jar`
   - `spring-core-<version>.jar` → `spring-core-6.1.14.jar`
   - `spring-jcl-<version>.jar` → `spring-jcl-6.1.14.jar`
   - `spring-web-<version>.jar` → `spring-web-6.1.14.jar`

   新しい JAR ファイルを取得するには、[Adobe ソフトウェア配布](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/aem-6-5-0-hotfix-vuln-30727/spring-6.1.14-jars.zip)から spring-6.1.14-jars.zip ファイルをダウンロードし、ZIP ファイルを抽出して、更新された Spring フレームワーク JAR ファイルにアクセスします。

   1. 次の JAR ファイル内の MANIFEST.MF ファイルを更新します。
   - `geode-server-all-<version>.jar`
   - `gfsh-dependencies.jar`

   各 JAR の場合：
   - アーカイブマネージャーツールを使用して JAR を開きます
   - `META-INF/MANIFEST.MF` ファイルを見つけて抽出します
   - MANIFEST.MF ファイルをテキストエディターで編集します
   - 「Class-Path」セクションを見つけて、すべての Spring フレームワーク参照を更新します。
      - `spring-core-<version>.jar`コピー先：`spring-core-6.1.14.jar`
      - `spring-web-<version>.jar`コピー先：`spring-web-6.1.14.jar`
      - `spring-context-<version>.jar`コピー先：`spring-context-6.1.14.jar`
      - `spring-beans-<version>.jar`コピー先：`spring-beans-6.1.14.jar`
      - `spring-jcl-<version>.jar`コピー先：`spring-jcl-6.1.14.jar`
   - 変更した MANIFEST.MF ファイルを保存します
   - JAR 内の元の MANIFEST.MF を更新されたバージョンに置き換えます
   - JAR ファイルを保存します

   1. 注意が必要な一般的な問題：
      - マニフェストに重複エントリがないことを確認します
      - 適切な行末を維持します
      - 参照されているすべての JAR が指定した場所に存在することを検証します

   1. 検証手順：
      - マニフェストが適切に更新されているかどうかを確認します
      - すべての Spring 依存関係が正しく参照されていることを検証します
      - 古いバージョンの参照が残っていないことを確認します
      - アプリケーションをテストして、クラスの読み込みに問題がないことを確認します

1. Configuration Manager を実行します。

1. サーバーを再起動します。
   - JDK 17 を使用してロケーターサーバーを起動します
   - 以前使用したのと同じ JDK バージョン（JDK 8 または JDK 11）を使用して、アプリケーションサーバーを起動します。
