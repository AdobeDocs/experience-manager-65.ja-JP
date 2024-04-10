---
title: 遅延コンテンツ移行
description: Adobe Experience Manager 6.4 での遅延コンテンツ移行について説明します。
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
docset: aem65
feature: Upgrading
exl-id: 946c7c2a-806b-4461-a38b-9c2e5ef1e958
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 27%

---

# 遅延コンテンツ移行 {#lazy-content-migration}

下位互換性を保つため、でのコンテンツと設定 **/etc** および **/content** Adobe Experience Manager（AEM） 6.3 以降では、アップグレードによってすぐに変更されることはありません。 これは、これらの構造に対する顧客アプリケーションの依存関係が損なわれないようにするために行われます。 標準搭載のAEM 6.5 のコンテンツが別の場所でホストされる場合でも、これらのコンテンツ構造に関連する機能は引き続き同じです。

これらのすべての場所が自動的に変換されるわけではありませんが、いくつかの遅延した `CodeUpgradeTasks` も遅延コンテンツ移行と見なされます。これを使用すると、次のシステムプロパティを設定してインスタンスを再起動することで、これらの自動変換をトリガーできます。

```shell
-Dcom.adobe.upgrade.forcemigration=true
```

この結果、 `CodeUpgradeTasks` 移行中に実行されます。

AIM は効率的に実行されますが、このアップグレードプロセスは同期されているので、処理する必要があるコンテンツの量に応じてダウンタイムが発生します。 Adobeでは、実稼動システムより前のステージング環境で実行時間を評価し、それに応じたメンテナンスウィンドウを計画することをお勧めします。

通常、これにはアプリケーションの調整も必要なので、このアクティビティは対応するアプリケーションのデプロイメントと共に実行する必要があります。

次に、6.5 で導入された `CodeUpgradeTasks` の完全なリストを示します。

| **名前** | **関連する** **（以前のAEM バージョン）** | **移行** **タイプ** | **詳細** |
|---|---|---|---|
| `Cq561ProjectContentUpgrade` | &lt; 5.6.1 | 即時 |  |
| `Cq60MSMContentUpgrade` | &lt; 6.0 | 即時 | 削除された `LiveRelationShips` からすべての `VersionStorage` を検出し、親に実行プロパティを追加します。 |
| `Cq61CloudServicesContentUpgrade` | &lt; 6.1 | 即時 | デフォルトの設定でセキュリティで保護されたクラウドサービスを再構築 |
| `Cq62ConfContentUpgrade` | &lt; 6.2 | 即時 | プロパティベースのリンクを次から削除 **/content** 対象： **/conf** （OSGi メカニズムに置き換えられます）が、対応する OSGi 設定を生成します |
| `Cq62FormsContentUpgrade` | &lt; 6.2 | 即時 | merge_preserve の処理により、デフォルトのセキュアな拒否ルールは指定された権限を上書きし、アップグレード時に並べ替えが必要になります |
| `CQ62Html5SmartFileUpgrade` | &lt; 6.2 | 即時 | Html5SmartFile ウィジェットを使用してコンポーネントを検出し、コンテンツ内でコンポーネントの使用を検索し、永続性を再構築して、バイナリをコンポーネントレベルで格納するのではなく、事実上レベル下に移動します。 |
| `Cq62ProjectsCodeUpgrade` | &lt; 6.2 | 即時 | 古いスタイルプロジェクトの移動元 **/etc/projects** 対象： **/content/projects** |
| `Cq62TargetCampaignsContentUpgrade` | &lt; 6.2 | 即時 | 階層（領域）にコンテナレイヤーを導入し、参照を調整します。 |
| `Cq62TargetContentUpgrade` | &lt; 6.2 | 即時 | ターゲット コンポーネントに固定の場所の名前を設定します。 |
| `Cq62WorkflowContentUpgrade` | &lt; 6.2 | 即時 | ワークフローの複雑な変換では、6.2 の構造、インスタンス、通知にさかのぼり、**/var/backup** のバックアップの場所から結合し直してモデル化します。 |
| `CQ63AssetsMetadataFormsUpdate` | &lt; 6.3 | 即時 | アセット、カスタムメタデータスキーマおよび処理プロファイルをから移動します **/apps** 対象： **/conf** および、メタデータスキーマとメタデータプロファイルフォームを coral2 から coral3 に変換します。 |
| `CQ63AssetsSearchFacetsUpdate` | &lt; 6.3 | 即時 | アセットとカスタム検索ファセットをから移動 **/apps** 対象： **/conf** および、メタデータスキーマとメタデータプロファイルフォームを coral2 から coral3 に変換します。 |
| `CQ63InboxItemsUpgrade` | &lt; 6.3 | 即時 | インボックス項目の並べ替えに対応するようにインボックス項目を更新（メタデータを調整して効率的な並べ替えを実現） |
| `CQ63MetadataSchemaConfigUpdate` | &lt; 6.3 | 即時 | 相対パスをに置き換えて、フォルダーの metadataSchema プロパティを調整します。 **/conf** の代わりに **/apps** |
| `CQ63MobileAppsNavUpgrade` | &lt; 6.3 | 即時 | ナビゲーション構造の調整 |
| `CQ63MonitoringDashboardsConfigUpdate` | &lt; 6.3 | 即時 | 監視ダッシュボードのカスタム設定をから移動します **/libs** および **/apps** |
| `CQ63ProcessingProfileConfigUpdate` | &lt; 6.3 | 即時 | Assets の processingProfile プロパティ（6.1 まで使用）を 6.3 以降の構造に一致するように翻訳します。 また、プロファイルの相対パスを **/apps** の代わりに **/conf** に変更します。 |
| `CQ63ToolsMenuEntriesContentUpgrade` | &lt; 6.3 | 即時 | アップグレードがある場合に、古いCRXDE Liteと Web コンソール メニューのエントリを削除するアップグレード タスク。 |
| `CQ64CommunitiesConfigsCleanupTask` | &lt; 6.3 | 遅延 | SRP クラウド設定、コミュニティウォッチワード設定を移動すると、クリーンアップされます **/etc/social** および **/etc/enablement** （遅延移行の実行時に、参照とデータを調整する必要があります。アプリケーション部分がこの構造に依存しなくなりました）。 |
| `CQ64LegacyCloudSettingsCleanupTask` | &lt; 6.4 | 遅延 | クリーンアップ **/etc/cloudsettings** （ContextHub 設定を含む）。 設定は初回アクセス時に自動的に移行されます。 遅延コンテンツ移行が、このコンテンツのアップグレードと共にで開始された場合 **/etc/cloudsettings** アップグレードの前にパッケージを通じて保存し、暗黙的な変換を開始および完了後にパッケージをアンインストールするには、再インストールする必要があります。 |
| `CQ64UsersTitleFixTask` | &lt; 6.4 | 遅延 | 従来のタイトル構造を、ユーザープロファイルのノードのタイトルに調整します。 |
| `CQ64CommerceMigrationTask` | &lt; 6.4 | 遅延 | コマースコンテンツを **/etc/commerce** から **/var/commerce** に移行します。移行中にコンテンツが移動され、移動されたコンテンツへの参照が更新されて、新しい場所が反映されます。 |
| `CQ65DMMigrationTask` | &lt; 6.5 | 遅延 | 従来のカタログ設定と Dynamic Media Cloud Services 設定を **/etc** から **/conf** に移行する |
| `CQ65LegacyClientlibsCleanupTask` | &lt; 6.5 | 遅延 | **/etc/clientlibs** の下に存在する従来の clientlibs をクリーンアップする |
