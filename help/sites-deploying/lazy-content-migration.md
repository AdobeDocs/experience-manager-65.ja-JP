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
source-git-commit: 3885cc51f7e821cdb352737336a29f9c4f0c2f41
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 27%

---

# 遅延コンテンツ移行 {#lazy-content-migration}

下位互換性を保つため、のコンテンツと設定 **/etc** および **/content** Adobe Experience Manager(AEM)6.3 以降は、アップグレードの際に変更や直ちに変換はおこなわれません。 これは、顧客アプリケーションのこれらの構造に対する依存関係を確実に維持するためにおこなわれます。 標準搭載のAEM 6.5 内のコンテンツが別の場所でホストされる場合でも、これらのコンテンツ構造に関連する機能は同じです。

これらのすべての場所が自動的に変換されるわけではありませんが、いくつかの遅延した `CodeUpgradeTasks` も遅延コンテンツ移行と見なされます。これを使用すると、次のシステムプロパティを設定してインスタンスを再起動することで、これらの自動変換をトリガーできます。

```shell
-Dcom.adobe.upgrade.forcemigration=true
```

これにより、 `CodeUpgradeTasks` 移行中に実行される

目的は効率的な実行ですが、このアップグレードプロセスは同期的なので、処理する必要のあるコンテンツの量に応じてダウンタイムが発生します。 Adobeでは、実稼動システムより前のステージ環境での実行時間を評価して、対応するメンテナンスウィンドウを計画することをお勧めします。

通常は、アプリケーションの調整も必要なので、このアクティビティは、対応するアプリケーションのデプロイメントと共に実行する必要があります。

次に、6.5 で導入された `CodeUpgradeTasks` の完全なリストを示します。

| **名前** | **関連** **( 以前のAEMバージョンの場合 )** | **移行** **タイプ** | **詳細** |
|---|---|---|---|
| `Cq561ProjectContentUpgrade` | &lt; 5.6.1 | 即時 |  |
| `Cq60MSMContentUpgrade` | &lt; 6.0 | 即時 | 削除された `LiveRelationShips` からすべての `VersionStorage` を検出し、親に実行プロパティを追加します。 |
| `Cq61CloudServicesContentUpgrade` | &lt; 6.1 | 即時 | デフォルト設定でセキュリティで保護されたクラウドサービスを再構築します |
| `Cq62ConfContentUpgrade` | &lt; 6.2 | 即時 | 次の場所にあるプロパティベースのリンクを削除 **/content** から **/conf** （OSGi メカニズムに置き換え）、対応する OSGi 設定を生成します。 |
| `Cq62FormsContentUpgrade` | &lt; 6.2 | 即時 | merge_preserve の処理により、デフォルトで保護された拒否ルールが与えられた権限を上書きするので、アップグレード時に並べ替えを行う必要が生じます |
| `CQ62Html5SmartFileUpgrade` | &lt; 6.2 | 即時 | Html5SmartFile ウィジェットを使用してコンポーネントを検出し、コンテンツ内でのコンポーネントの使用を検索し、永続性を再構築し、バイナリを下のレベルに効果的に移動し、コンポーネントレベルに保存しません。 |
| `Cq62ProjectsCodeUpgrade` | &lt; 6.2 | 即時 | 次の場所から古いスタイルのプロジェクトを移動します： **/etc/projects** から **/content/projects** |
| `Cq62TargetCampaignsContentUpgrade` | &lt; 6.2 | 即時 | コンテナレイヤを階層 (Areas) に導入し、参照を調整します。 |
| `Cq62TargetContentUpgrade` | &lt; 6.2 | 即時 | 固定位置名をターゲットコンポーネントに設定します。 |
| `Cq62WorkflowContentUpgrade` | &lt; 6.2 | 即時 | ワークフローの複雑な変換では、6.2 の構造、インスタンス、通知にさかのぼり、**/var/backup** のバックアップの場所から結合し直してモデル化します。 |
| `CQ63AssetsMetadataFormsUpdate` | &lt; 6.3 | 即時 | 次の場所からアセット、カスタムメタデータスキーマ、処理プロファイルを移動します： **/apps** から **/conf** およびは、メタデータスキーマおよびメタデータプロファイルフォームを coral2 から coral3 に変換します。 |
| `CQ63AssetsSearchFacetsUpdate` | &lt; 6.3 | 即時 | アセットおよびカスタム検索ファセットを次の場所に移動： **/apps** から **/conf** およびは、メタデータスキーマおよびメタデータプロファイルフォームを coral2 から coral3 に変換します。 |
| `CQ63InboxItemsUpgrade` | &lt; 6.3 | 即時 | インボックス項目を並べ替えるための InboxItems を更新しました（効率的な並べ替えのためのメタデータの調整） |
| `CQ63MetadataSchemaConfigUpdate` | &lt; 6.3 | 即時 | 相対パスを **/conf** 代わりに **/apps** |
| `CQ63MobileAppsNavUpgrade` | &lt; 6.3 | 即時 | ナビゲーション構造の調整 |
| `CQ63MonitoringDashboardsConfigUpdate` | &lt; 6.3 | 即時 | 監視ダッシュボードのカスタム設定を次の場所に移動します： **/libs** および **/apps** |
| `CQ63ProcessingProfileConfigUpdate` | &lt; 6.3 | 即時 | 6.3 以降の構造と一致するように、Assets の processingProfile プロパティ（6.1 まで使用）を変換します。 また、プロファイルの相対パスを **/apps** の代わりに **/conf** に変更します。 |
| `CQ63ToolsMenuEntriesContentUpgrade` | &lt; 6.3 | 即時 | 古いCRXDE Liteと Web コンソールのメニューエントリを削除するアップグレードタスク（アップグレードがある場合）。 |
| `CQ64CommunitiesConfigsCleanupTask` | &lt; 6.3 | 遅延 | SRP クラウド設定の移行、コミュニティウォッチワード設定、クリーンアップ **/etc/social** および **/etc/enablement** （遅延移行を実行する場合は、参照とデータを調整する必要があります。アプリケーション部分は、この構造に依存しなくなりました）。 |
| `CQ64LegacyCloudSettingsCleanupTask` | &lt; 6.4 | 遅延 | クリーンアップ **/etc/cloudsettings** （ContextHub 設定を含む） 最初のアクセス時に設定が自動的に移行されます。 遅延コンテンツ移行を開始し、このコンテンツを **/etc/cloudsettings** アップグレードの前にパッケージで保持し、暗黙的な変換が開始されるように再インストールする必要があります。また、完了後にパッケージを以降にアンインストールする必要もあります。 |
| `CQ64UsersTitleFixTask` | &lt; 6.4 | 遅延 | 従来のタイトル構造をユーザープロファイルノードのタイトルに調整します。 |
| `CQ64CommerceMigrationTask` | &lt; 6.4 | 遅延 | コマースコンテンツを **/etc/commerce** から **/var/commerce** に移行します。移行中にコンテンツが移動され、移動されたコンテンツへの参照が更新されて、新しい場所が反映されます。 |
| `CQ65DMMigrationTask` | &lt; 6.5 | 遅延 | 従来のカタログ設定と Dynamic Media Cloud Services 設定を **/etc** から **/conf** に移行する |
| `CQ65LegacyClientlibsCleanupTask` | &lt; 6.5 | 遅延 | **/etc/clientlibs** の下に存在する従来の clientlibs をクリーンアップする |
