---
title: ヘルスモニターの概要
seo-title: ヘルスモニターの概要
description: ヘルスモニターの概要とアクセス方法の詳細について説明します。
seo-description: ヘルスモニターの概要とアクセス方法の詳細について説明します。
uuid: 5934fd2d-80a5-4c6d-b3ee-882c2865705b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c303e967-944d-40b0-96ca-f91e2f42a0d0
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 100%

---


# ヘルスモニターの概要 {#overview-of-health-monitor}

ヘルスモニターでは、AEM Forms システムに関する重要な情報、例えばサーバー情報、メモリ使用量、プロセッサーの使用状況などを確認できます。また、キュー内の作業項目やジョブの数、そのステータスなど、ワークマネージャーの統計情報も入手できます。ヘルスモニターを使用して次のタスクを実行できます。

* システムが正常に稼働していることの確認
* システムでの問題発生時に診断に役立つ情報の表示
* 問題のある作業項目またはジョブに対する操作の実行
* ジョブマネージャーのデータベースからの古いレコードの削除

管理コンソールのヘルスモニターページには、次の 3 つのタブがあります。

* 「システム」タブには、リソースモニタリングチャートおよび forms サーバー（またはクラスター環境のノード）に関する情報が表示されます（[システム情報の表示](/help/forms/using/admin-help/view-system-information.md#view-system-information)を参照）。
* 「ワークマネージャー」タブには、ワークマネージャーキュー内の作業項目の数など、ワークマネージャーに関連するデータが表示されます。この情報は様々な条件に基づいてフィルタリングできます。また、操作ツールを使用して作業項目を個別に管理することもできます（[ワークマネージャーに関連する統計情報の表示](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager)を参照）。
* 「ジョブクリアスケジューラー」タブでは、ジョブマネージャーのデータベースから古いレコードを削除できます（[ジョブマネージャーのデータベースからの古いレコードの削除](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database)を参照）。

ヘルスモニター Web ページには、Gemfire API によって集められた統計情報が表示されます。この API ではクラスター内のすべてのノードが自動的に検出されます。また、プロキシサーバーやロードバランサーを経由して統計情報を収集するときに発生する、セキュリティの問題を解決することもできます。Java オプションを利用してヘルスモニターを微調整できるので、AEM Forms 環境のパフォーマンスへの影響を抑えることができます（[ヘルスモニターのパフォーマンスの最適なチューニング](/help/forms/using/admin-help/fine-tuning-health-monitor-performance.md#fine-tuning-health-monitor-performance)を参照）。

**ヘルスモニターへのアクセス**

1. 管理コンソールで、ページの右上隅にある「ヘルスモニター」をクリックします。

