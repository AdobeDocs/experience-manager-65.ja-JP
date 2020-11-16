---
title: 遅延コンテンツ移行
seo-title: 遅延コンテンツ移行
description: AEM 6.4 の遅延コンテンツ移行について説明します。
seo-description: AEM 6.4 の遅延コンテンツ移行について説明します。
uuid: f5b0aa84-5638-4708-9da2-89964d394632
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: d72b8844-d782-4b5b-8999-338217dbefb9
docset: aem65
translation-type: tm+mt
source-git-commit: 7d93df515bf98f0a947428b8093e059d63b21a34
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 87%

---


# 遅延コンテンツ移行 {#lazy-content-migration}

後方互換性に配慮し、AEM 6.3 以降では、 **/etc** および **/content** 内のコンテンツと設定は、アップグレードをおこなってもすぐに変更または変換されません。これは、これらの構造上にあるお客様のアプリケーションの依存関係が変更されないようにするためにおこなわれます。AEM 6.5 のすぐに使用できるコンテンツが別の場所でホストされていても、これらのコンテンツ構造に関連する機能は同じままです。

While not all of those locations may be transformed automatically, there are a few delayed `CodeUpgradeTasks` also referred to as Lazy Content Migration. これにより、次のsystemプロパティを使用してインスタンスを再起動することで、顧客はこれらの自動変換をトリガーできます。

```shell
-Dcom.adobe.upgrade.forcemigration=true
```

これにより、移行中に `CodeUpgradeTasks` が実行されます。

目的は効率的な実行ですが、このアップグレード処理は同期的です。そのため、処理される必要のあるコンテンツの量に応じたダウンタイムを伴います。実稼動システムの前にステージ環境で実行時間を評価して、それに応じたメンテナンスウィンドウを計画することをお勧めします。

通常、これにもアプリケーションの調整が必要となるので、このアクティビティは対応するアプリケーションのデプロイメントと共に実行する必要があります。

次に、6.5 で導入された `CodeUpgradeTasks` の完全なリストを示します。

| **名前** | **関連する** **AEM バージョン** | **移行の****タイプ** | **詳細** |
|---|---|---|---|
| `Cq561ProjectContentUpgrade` | &lt; 5.6.1 | 即時 |  |
| `Cq60MSMContentUpgrade` | &lt; 6.0 | 即時 | 削除された `LiveRelationShips` からすべての `VersionStorage` を検出し、親に実行プロパティを追加します。 |
| `Cq61CloudServicesContentUpgrade` | &lt; 6.1 | 即時 | デフォルトの保護設定でクラウドサービスを再構築します。 |
| `Cq62ConfContentUpgrade` | &lt; 6.2 | 即時 | **/content** から **/conf** へのプロパティベースのリンクを削除し（OSGi メカニズムで置き換え）、対応する OSGi 設定を生成します。 |
| `Cq62FormsContentUpgrade` | &lt; 6.2 | 即時 | merge_preserve 処理が原因で、デフォルトの保護拒否ルールが指定された権限を上書きするので、アップグレード時に並べ替えが必要になります。 |
| `CQ62Html5SmartFileUpgrade` | &lt; 6.2 | 即時 | Html5SmartFile ウィジェットを使用するコンポーネントを検出し、コンテンツ内でのコンポーネントの使用を検索して、実質的にバイナリを下のレベルに移動してコンポーネントレベルに格納しないことで永続性を再構築します。 |
| `Cq62ProjectsCodeUpgrade` | &lt; 6.2 | 即時 | 古いスタイルのプロジェクトを **/etc/projects** から **/content/projects** に移動します。 |
| `Cq62TargetCampaignsContentUpgrade` | &lt; 6.2 | 即時 | 階層（Areas）にコンテナレイヤーを導入し、参照を調整します。 |
| `Cq62TargetContentUpgrade` | &lt; 6.2 | 即時 | 固定された場所名をターゲットコンポーネントに設定します。 |
| `Cq62WorkflowContentUpgrade` | &lt; 6.2 | 即時 | ワークフローの複雑な変換では、6.2 の構造、インスタンス、通知にさかのぼり、**/var/backup** のバックアップの場所から結合し直してモデル化します。 |
| `CQ63AssetsMetadataFormsUpdate` | &lt; 6.3 | 即時 | アセット、カスタムメタデータスキーマおよび処理プロファイルを **/apps** から **/conf** に移動して、メタデータスキーマおよびメタデータプロファイルフォームを coral2 から coral3 に変換します。 |
| `CQ63AssetsSearchFacetsUpdate` | &lt; 6.3 | 即時 | アセットおよびカスタム検索ファセットを **/apps** から **/conf** に移動して、メタデータスキーマおよびメタデータプロファイルフォームを coral2 から coral3 に変換します。 |
| `CQ63InboxItemsUpgrade` | &lt; 6.3 | 即時 | インボックス項目を並べ替えるために InboxItems を更新（効率的な並べ替えのためにメタデータを調整）します。 |
| `CQ63MetadataSchemaConfigUpdate` | &lt; 6.3 | 即時 | 相対パスを **/apps** の代わりに **/conf** に置き換えることで、フォルダーの metadataSchema プロパティを調整します。 |
| `CQ63MobileAppsNavUpgrade` | &lt; 6.3 | 即時 | ナビゲーション構造を調整します。 |
| `CQ63MonitoringDashboardsConfigUpdate` | &lt; 6.3 | 即時 | 監視ダッシュボードのカスタム設定を **/libs** および **/apps** から移動します。 |
| `CQ63ProcessingProfileConfigUpdate` | &lt; 6.3 | 即時 | 6.3 以降の構造に合致させるために、（6.1 まで使用されていた）アセットの processingProfile プロパティを変換します。また、プロファイルの相対パスを **/apps** の代わりに **/conf** に変更します。 |
| `CQ63ToolsMenuEntriesContentUpgrade` | &lt; 6.3 | 即時 | アップグレードの場合に、廃止された CRXDE Lite および Web コンソールのメニューエントリを削除するアップグレードタスク。 |
| `CQ64CommunitiesConfigsCleanupTask` | &lt; 6.3 | 遅延 | SRP クラウド設定、コミュニティウォッチワード設定を移動して、**/etc/social** および **/etc/enablement** をクリーンアップします（遅延移行が実行される際に、参照およびデータを調整する必要があります。アプリケーション部分がこの構造に依存しなくなるようにする必要があります）。 |
| `CQ64LegacyCloudSettingsCleanupTask` | &lt; 6.4 | 遅延 | **/etc/cloudsettings** をクリーンアップします（ContextHub 設定を含む）。最初のアクセス時に設定が自動的に移行されます。アップグレードに伴って遅延コンテンツ移行が開始される場合、**/etc/cloudsettings** にあるこのコンテンツは、アップグレード前にパッケージを介して保持し、暗黙的な変換を開始するために再インストールする必要があります。パッケージは移行の完了後にアンインストールされます。 |
| `CQ64UsersTitleFixTask` | &lt; 6.4 | 遅延 | 従来のタイトル構造をユーザープロファイルノードのタイトルに適合させます。 |
| `CQ64CommerceMigrationTask` | &lt; 6.4 | 遅延 | コマースコンテンツを/etc/commerce **から/var/commerce** に移行します ****。 移行中に、コンテンツが移動され、移動されたコンテンツへの参照が更新されて、新しい場所が反映されます。 |
| `CQ65DMMigrationTask` | &lt; 6.5 | 遅延 | 従来のカタログ設定と動的メディアクラウドサービス設定を **/etc** から **/confに移行** |
| `CQ65LegacyClientlibsCleanupTask` | &lt; 6.5 | 遅延 | /etc/clientlibsの下に存在する既存の既存のクライアント **ライブラリをクリーンアップする** |
