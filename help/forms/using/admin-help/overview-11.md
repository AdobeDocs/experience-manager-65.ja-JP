---
title: ヘルスモニターの概要
description: このドキュメントでは、ヘルスモニターの概要と、ヘルスモニターへのアクセス方法について詳しく説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 05f8b430-141e-4921-98b1-a0d8f636e478
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 100%

---

# ヘルスモニターの概要 {#overview-of-health-monitor}

ヘルスモニターは、サーバー情報、メモリ使用量、プロセッサー使用量など、AEM Forms システムに関する重要な情報を提供します。また、キュー内の作業項目やジョブの数、そのステータスなど、ワークマネージャーの統計情報も入手できます。ヘルスモニターを使用して次のタスクを実行できます。

* システムが正常に稼動していることの確認
* システムでの問題発生時の診断に役立つ情報の表示
* 問題のある作業項目またはジョブに対する操作の実行
* ジョブマネージャーのデータベースからの古いレコードの削除

管理コンソールのヘルスモニターページには、次の 3 つのタブがあります。

* 「システム」タブには、リソースモニタリングチャートおよび Forms サーバー（またはクラスター環境のノード）に関する情報が表示されます。（[システム情報の表示](/help/forms/using/admin-help/view-system-information.md#view-system-information)を参照。）
* 「ワークマネージャー」タブには、ワークマネージャーキュー内の作業項目の数など、ワークマネージャーに関連するデータが表示されます。この情報は様々な条件に基づいてフィルタリングできます。また、操作ツールを使用して作業項目を個別に管理することもできます。（[ワークマネージャーに関連する統計情報の表示](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager)を参照。）
* 「ジョブクリアスケジューラー」タブでは、ジョブマネージャーのデータベースから古いレコードを削除できます。（[ジョブマネージャーのデータベースからのレコードの削除](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database)を参照。）

ヘルスモニター web ページには、Gemfire API によって集められた統計情報が表示されます。この API ではクラスター内のすべてのノードが自動的に検出されます。また、プロキシサーバーやロードバランサーを経由して統計情報を収集するときに発生する、セキュリティの問題を解決することもできます。Java オプションを利用してヘルスモニターを微調整できるので、AEM Forms 環境のパフォーマンスへの影響を抑えることができます。（[ヘルスモニターのパフォーマンスの最適なチューニング](/help/forms/using/admin-help/fine-tuning-health-monitor-performance.md#fine-tuning-health-monitor-performance)を参照。）

**ヘルスモニターへのアクセス**

1. 管理コンソールで、ページの右上隅にある「ヘルスモニター」をクリックします。
