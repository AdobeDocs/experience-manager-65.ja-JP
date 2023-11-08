---
title: ヘルスモニターの概要
seo-title: Overview of Health Monitor
description: このドキュメントでは、ヘルスモニターの概要とアクセス方法の詳細を説明します。
seo-description: This document provides the overview of the Health monitor, and details about how you can access it.
uuid: 5934fd2d-80a5-4c6d-b3ee-882c2865705b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c303e967-944d-40b0-96ca-f91e2f42a0d0
exl-id: 05f8b430-141e-4921-98b1-a0d8f636e478
source-git-commit: c4cd9a61a226ace2a72d60b5b7b7432de12cb873
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 2%

---

# ヘルスモニターの概要 {#overview-of-health-monitor}

ヘルスモニターは、サーバー情報、メモリ使用量、プロセッサー使用量など、AEM forms システムに関する重要な情報を提供します。 また、キュー内の作業項目やジョブの数、そのステータスなど、ワークマネージャーの統計も使用できます。 ヘルスモニターを使用して、次のタスクを実行できます。

* システムが正しく動作していることを確認します。
* 発生時のシステムの問題の診断に役立つ情報を表示
* 問題を表示する作業項目またはジョブに対する操作を実行します
* Job Manager データベースから古いレコードを削除する

管理コンソールのヘルスモニターページには、次の 3 つのタブがあります。

* 「システム」タブには、リソース監視のグラフと、Forms Server（またはクラスター環境のノード）に関する情報が表示されます。 ( 詳しくは、 [システム情報の表示](/help/forms/using/admin-help/view-system-information.md#view-system-information).)
* 「ワークマネージャー」タブには、ワークマネージャーキュー内の作業項目の数など、ワークマネージャーに関連するデータが表示されます。 様々な基準を使用して情報をフィルタリングしたり、操作ツールを使用して個々の作業項目を管理したりできます。 ( 詳しくは、 [ワークマネージャーに関連する統計を表示](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager).)
* 「ジョブのパージスケジューラ」タブを使用すると、ジョブマネージャーデータベースから古いレコードをパージできます。 ( 詳しくは、 [ジョブマネージャーデータベースからレコードをパージします](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database).)

ヘルスモニター Web ページには、Gemfire API を通じて収集された統計情報が入力されます。 この API は、クラスター内のすべてのノードを自動的に検出します。 また、プロキシサーバーやロードバランサーの背後から統計を収集する際に発生するセキュリティの問題も解決します。 Java オプションを使用してヘルスモニターを微調整し、AEM forms 環境のパフォーマンスへの影響を減らすことができます。 ( 詳しくは、 [ヘルスモニタのパフォーマンスの微調整](/help/forms/using/admin-help/fine-tuning-health-monitor-performance.md#fine-tuning-health-monitor-performance).)

**ヘルスモニターにアクセス**

1. 管理コンソールで、ページの右上隅にある「ヘルスモニター」をクリックします。
