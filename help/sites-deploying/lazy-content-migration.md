---
title: 遅延コンテンツ移行
description: Adobe Experience Manager 6.4 の遅延コンテンツ移行について説明します。
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
ht-degree: 100%

---

# 遅延コンテンツ移行 {#lazy-content-migration}

後方互換性に配慮し、Adobe Experience Manager（AEM）6.3 以降では、**/etc** および **/content** 内のコンテンツと設定は、アップグレードを行ってもすぐに変更または変換されません。これは、これらの構造上にあるお客様のアプリケーションの依存関係が変更されないようにするために行われます。AEM 6.5 のすぐに使用できるコンテンツが別の場所でホストされていても、これらのコンテンツ構造に関連する機能は同じままです。

これらのすべての場所が自動的に変換されるわけではありませんが、いくつかの遅延した `CodeUpgradeTasks` も遅延コンテンツ移行と見なされます。これを使用すると、次のシステムプロパティを設定してインスタンスを再起動することで、これらの自動変換をトリガーできます。

```shell
-Dcom.adobe.upgrade.forcemigration=true
```

これにより、移行中に `CodeUpgradeTasks` が実行されます。

目的は効率的な実行ですが、このアップグレード処理は同期的です。そのため、処理される必要のあるコンテンツの量に応じたダウンタイムを伴います。アドビでは、実稼動システムの前にステージ環境で実行時間を評価して、それに応じたメンテナンスウィンドウを計画することをお勧めします。

通常、これにもアプリケーションの調整が必要となるので、このアクティビティは対応するアプリケーションのデプロイメントと共に実行する必要があります。

次に、6.5 で導入された `CodeUpgradeTasks` の完全なリストを示します。

| **名前** | **関連する** **以前の AEM バージョン** | **移行の****タイプ** | **詳細** |
|---|---|---|---|
| `Cq561ProjectContentUpgrade` | &lt; 5.6.1 | 即時 |  |
| `Cq60MSMContentUpgrade` | &lt; 6.0 | 即時 | 削除された `LiveRelationShips` からすべての `VersionStorage` を検出し、親に実行プロパティを追加します。 |
| `Cq61CloudServicesContentUpgrade` | &lt; 6.1 | 即時 | デフォルトの保護設定でクラウドサービスを再構築します。 |
| `Cq62ConfContentUpgrade` | &lt; 6.2 | 即時 | **/content** から **/conf** へのプロパティベースのリンクを削除し（OSGi メカニズムで置き換え）、対応する OSGi 設定を生成します。 |
| `Cq62FormsContentUpgrade` | &lt; 6.2 | 即時 | merge_preserve 処理が原因で、デフォルトの保護拒否ルールが指定された権限を上書きするので、アップグレード時に並べ替えが必要になります。 |
| `CQ62Html5SmartFileUpgrade` | &lt; 6.2 | 即時 | Html5SmartFile ウィジェットを使用するコンポーネントを検出し、コンテンツ内でのコンポーネントの使用を検索して、実質的にバイナリを下のレベルに移動してコンポーネントレベルに格納しないことで永続性を再構築します。 |
| `Cq62ProjectsCodeUpgrade` | &lt; 6.2 | 即時 | 古いスタイルのプロジェクトを **/etc/projects** から **/content/projects** に移動します。 |
| `Cq62TargetCampaignsContentUpgrade` | &lt; 6.2 | 即時 | 階層（領域）にコンテナレイヤーを導入し、参照を調整します。 |
| `Cq62TargetContentUpgrade` | &lt; 6.2 | 即時 | 固定された場所名をターゲットコンポーネントに設定します。 |
| `Cq62WorkflowContentUpgrade` | &lt; 6.2 | 即時 | ワークフローの複雑な変換では、6.2 の構造、インスタンス、通知にさかのぼり、**/var/backup** のバックアップの場所から結合し直してモデル化します。 |
| `CQ63AssetsMetadataFormsUpdate` | &lt; 6.3 | 即時 | アセット、カスタムメタデータスキーマおよび処理プロファイルを **/apps** から **/conf** に移動して、メタデータスキーマおよびメタデータプロファイルフォームを coral2 から coral3 に変換します。 |
| `CQ63AssetsSearchFacetsUpdate` | &lt; 6.3 | 即時 | アセットとカスタム検索ファセットを **/apps** から **/conf** に移動し、メタデータスキーマとメタデータプロファイルフォームを coral2 から coral3 に変換します。 |
| `CQ63InboxItemsUpgrade` | &lt; 6.3 | 即時 | インボックス項目の順序付けのために InboxItems を更新します（効率的な並べ替えのためのメタデータの調整） |
| `CQ63MetadataSchemaConfigUpdate` | &lt; 6.3 | 即時 | 相対パスを **/apps** の代わりに **/conf** に置き換えることで、フォルダーの metadataSchema プロパティを調整します。 |
| `CQ63MobileAppsNavUpgrade` | &lt; 6.3 | 即時 | ナビゲーション構造の調整 |
| `CQ63MonitoringDashboardsConfigUpdate` | &lt; 6.3 | 即時 | 監視ダッシュボードのカスタム設定を **/libs** および **/apps** から移動します。 |
| `CQ63ProcessingProfileConfigUpdate` | &lt; 6.3 | 即時 | Assets 内の processingProfile プロパティ（6.1 まで使用）を、6.3 以降の構造に一致するように変換します。また、プロファイルの相対パスを **/apps** の代わりに **/conf** に変更します。 |
| `CQ63ToolsMenuEntriesContentUpgrade` | &lt; 6.3 | 即時 | アップグレードがある場合に、古い CRXDE Lite および web コンソールのメニューエントリを削除するアップグレードタスク。 |
| `CQ64CommunitiesConfigsCleanupTask` | &lt; 6.3 | 遅延 | SRP クラウド設定、コミュニティのウォッチワード設定を移動すると、**/etc/social** および **/etc/enablement** がクリーンアップされます（遅延移行を実行するときは、すべての参照とデータを調整する必要があります。アプリケーションのどの部分においてもこの構造に依存しないようにする必要があります）。 |
| `CQ64LegacyCloudSettingsCleanupTask` | &lt; 6.4 | 遅延 | **/etc/cloudsettings**（ContextHub 設定を含む）をクリーンアップします。設定は最初のアクセス時に自動的に移行されます。アップグレードとともに遅延コンテンツ移行が開始された場合、**/etc/cloudsettings** 内のこのコンテンツは、アップグレード前にパッケージ経由で保存し、暗黙的な変換を有効にするために再インストールする必要があります。また、完了後にパッケージをアンインストールする必要があります。 |
| `CQ64UsersTitleFixTask` | &lt; 6.4 | 遅延 | 従来のタイトル構造をユーザープロファイルノードのタイトルに適合させます。 |
| `CQ64CommerceMigrationTask` | &lt; 6.4 | 遅延 | コマースコンテンツを **/etc/commerce** から **/var/commerce** に移行します。移行中にコンテンツが移動され、移動されたコンテンツへの参照が更新されて、新しい場所が反映されます。 |
| `CQ65DMMigrationTask` | &lt; 6.5 | 遅延 | 従来のカタログ設定と Dynamic Media Cloud Services 設定を **/etc** から **/conf** に移行する |
| `CQ65LegacyClientlibsCleanupTask` | &lt; 6.5 | 遅延 | **/etc/clientlibs** の下に存在する従来の clientlibs をクリーンアップする |
