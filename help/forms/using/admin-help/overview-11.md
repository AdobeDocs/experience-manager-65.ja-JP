---
title: ヘルスモニターの概要
description: このドキュメントでは、ヘルスモニターの概要と、ヘルスモニターへのアクセス方法について詳しく説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 05f8b430-141e-4921-98b1-a0d8f636e478
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 100%
---
# ヘルスモニターの概要 {#overview-of-health-monitor}

ヘルスモニターは、サーバー情報、メモリ使用量、プロセッサー使用量など、AEM Forms システムに関する重要な情報を提供します。 また、キュー内の作業項目やジョブの数、そのステータスなど、ワークマネージャーの統計情報も入手できます。 ヘルスモニターを使用して次のタスクを実行できます。

* システムが正常に稼動していることの確認
* システムでの問題発生時の診断に役立つ情報の表示
* 問題のある作業項目またはジョブに対する操作の実行
* ジョブマネージャーのデータベースからの古いレコードの削除

管理コンソールのヘルスモニターページには、次の 3 つのタブがあります。

* 「システム」タブには、リソースモニタリングチャートおよび Forms サーバー（またはクラスター環境のノード）に関する情報が表示されます。 （[システム情報の表示](/help/forms/using/admin-help/view-system-information.md#view-system-information)を参照。）
* 「ワークマネージャー」タブには、ワークマネージャーキュー内の作業項目の数など、ワークマネージャーに関連するデータが表示されます。 この情報は様々な条件に基づいてフィルタリングできます。また、操作ツールを使用して作業項目を個別に管理することもできます。 （[ワークマネージャーに関連する統計情報の表示](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager)を参照。）
* 「ジョブクリアスケジューラー」タブでは、ジョブマネージャーのデータベースから古いレコードを削除できます。 （[ジョブマネージャーのデータベースからのレコードの削除](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database)を参照。）

ヘルスモニター web ページには、Gemfire API によって集められた統計情報が表示されます。 この API ではクラスター内のすべてのノードが自動的に検出されます。 また、プロキシサーバーやロードバランサーを経由して統計情報を収集するときに発生する、セキュリティの問題を解決することもできます。 Java オプションを利用してヘルスモニターを微調整できるので、AEM Forms 環境のパフォーマンスへの影響を抑えることができます。 （[ヘルスモニターのパフォーマンスの最適なチューニング](/help/forms/using/admin-help/fine-tuning-health-monitor-performance.md#fine-tuning-health-monitor-performance)を参照。）

**ヘルスモニターへのアクセス**

1. 管理コンソールで、ページの右上隅にある「ヘルスモニター」をクリックします。
