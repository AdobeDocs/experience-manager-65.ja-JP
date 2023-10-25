---
title: AEM 6 での監査ログのメンテナンス
seo-title: Audit Log Maintenance in AEM 6
description: Adobe Experience Manager(AEM) での監査ログのメンテナンスについて説明します。
seo-description: Learn about Audit Log Maintenance in Adobe Experience Manager (AEM).
uuid: 212de4df-6bf4-434c-94e1-74186d21945a
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 565d89de-b3ca-41a5-8e1c-d10905c25fb5
exl-id: 1e05faf5-619a-4ea3-acbf-2fd37c71e6d2
feature: Operations
source-git-commit: c7c32130a3257c14c98b52f9db31d80587d7993a
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 51%

---

# AEM 6 での監査ログのメンテナンス{#audit-log-maintenance-in-aem}

監査ログの対象となるAEMイベントは、多くのアーカイブデータを生成します。 このデータは、レプリケーション、アセットのアップロード、およびその他のシステムアクティビティによって、短期間で増大する可能性があります。

監査ログのメンテナンスには、特定のポリシーで監査ログのメンテナンスを自動化できる機能のいくつかの部分が含まれています。

設定可能な週別メンテナンスタスクとして実装され、操作ダッシュボードの監視コンソールからアクセスできます。

詳しくは、[操作ダッシュボードのドキュメント](/help/sites-administering/operations-dashboard.md)を参照してください。

監査ログのパージオプションには 3 つのタイプがあります。

1. [ページ監査ログのパージの設定](/help/sites-administering/operations-audit-log.md#configure-page-audit-log-purging)
1. [DAM 監査ログのパージの設定](/help/sites-administering/operations-audit-log.md#configure-dam-audit-log-purging)
1. [レプリケーション監査ログのパージの設定](/help/sites-administering/operations-audit-log.md#configure-replication-audit-log-purging)

それぞれ AEM の web コンソールでルールを作成して設定できます。設定後、**ツール／操作／メンテナンス／週別メンテナンスウィンドウ**&#x200B;に移動して、**監査ログのメンテナンスタスク**&#x200B;でそれらを実行することができます。

## ページ監査ログのパージの設定 {#configure-page-audit-log-purging}

監査ログのパージを設定するには、次の手順に従います。

1. ブラウザーに `http://localhost:4502/system/console/configMgr/` と入力して、web コンソール管理に移動します。

1. 「**ページ監査ログパージルール**」という項目を検索してクリックします。

   ![chlimage_1-365](assets/chlimage_1-365.png)

1. 次に、必要に応じてパージスケジューラーを設定します。 使用できるオプションは以下のとおりです。

   * **ルール名：** 監査ポリシー規則の名前
   * **Content path：**&#x200B;ルールが適用されるコンテンツのパス。
   * **最小年齢：** 監査ログを保持する必要がある日数。
   * **監査ログの種類：** パージする監査ログのタイプ。

   >[!NOTE]
   >
   >コンテンツパスは、リポジトリの `/var/audit/com.day.cq.wcm.core.page` ノードの子にのみ適用されます。

1. ルールを保存します。
1. 作成したルールを実行するには、操作ダッシュボードに公開する必要があります。 そのためには、AEM のようこそ画面から&#x200B;**ツール／操作／メンテナンス**&#x200B;に移動します。

1. **週別メンテナンスウィンドウ**&#x200B;カードをクリックします。

1. メンテナンスタスクは、**AuditLog メンテナンスタスク**&#x200B;カードの下に既に存在しています。

   ![chlimage_1-366](assets/chlimage_1-366.png)

1. 次回実行の日付を調べて設定するか、再生ボタンをクリックして手動で実行できます。

AEM 6.3 では、監査ログのパージタスクが完了する前に、スケジュールされたメンテナンスウィンドウを閉じると、タスクは自動的に停止します。次回のメンテナンスウィンドウを開くと、タスクは再開されます。

**AEM 6.5** で実行中の監査ログのパージタスクを手動で停止するには、「**停止**」アイコンをクリックします。次回の実行時に、タスクは安全に再開されます。

>[!NOTE]
>
>メンテナンスタスクを停止すると、既に進行中のジョブのトラッキングを失うことなく、実行を停止します。

## DAM 監査ログのパージの設定 {#configure-dam-audit-log-purging}

1. *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr* にあるシステムコンソールに移動します。
1. を検索 **DAM 監査ログのパージ** ルールを作成し、結果をクリックします。
1. 次のウィンドウで、適宜ルールを設定します。 オプションは次のとおりです。

   * **ルール名：** 監査ポリシー規則の名前
   * **Content path：**&#x200B;ルールが適用されるコンテンツのパス。
   * **最小年齢：** 監査ログを保持する必要がある日数
   * **監査ログ DAM イベントタイプ：** パージする必要がある DAM 監査イベントのタイプ。

1. クリック **保存** 設定を保存するには、以下を実行します。

## レプリケーション監査ログのパージの設定  {#configure-replication-audit-log-purging}

1. *https://&lt;serveraddress>:&lt;serverport>/system/console/configMgr* にあるシステムコンソールに移動します。
1. を検索 **レプリケーション監査ログパージスケジューラ** 結果をクリックします。
1. 次のウィンドウで、適宜ルールを設定します。 オプションは次のとおりです。

   * **ルール名：** 監査ポリシールールの名前
   * **Content path：**&#x200B;ルールが適用されるコンテンツのパス。
   * **最小年齢：** 監査ログを保持する必要がある日数
   * **監査ログレプリケーションイベントタイプ：** パージする必要があるレプリケーション監査イベントのタイプ

1. クリック **保存** 設定を保存します。
