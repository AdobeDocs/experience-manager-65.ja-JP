---
title: プロセスレポートの概要
description: JEE 上の AEM Forms プロセスレポートの概要と主な機能
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
exl-id: 674d28dc-7353-49de-9e12-b1998e1509c7
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
source-wordcount: '305'
ht-degree: 100%
---
# プロセスレポートの概要{#introduction-to-process-reporting}

![process-reporting](assets/process-reporting.png)

プロセスレポートは、AEM Forms のプロセスとタスクに関するレポートを作成および表示するために使用する、ブラウザーベースのツールです。

プロセスレポートは、標準の一連のレポートを提供し、長時間実行中のプロセス、プロセス期間、ワークフローの量に関する情報のフィルタリングと表示を行います。

さらに、プロセスレポートには、アドホッククエリを実行し、カスタムレポートビューをプロセスレポートユーザーインターフェイスに統合するためのインターフェイスが用意されています。

サポートされているブラウザーの一覧については、 [AEM Forms サポートプラットフォーム](/help/forms/using/aem-forms-jee-supported-platforms.md)を参照してください。

プロセスレポートは、以下のモジュールにもとづいて構築されています。

* AEM Forms Database からプロセスデータを読み取る
* 埋め込みプロセスレポートリポジトリーにプロセスデータを公開
* レポートを表示するためのブラウザーベースのユーザーインターフェイスを提供

## 主な機能 {#key-capabilities}

### 常時稼動のレポート {#always-on-reporting}

![site-management](assets/site-management.png)

長時間実行されているプロセスのリスト、期間グラフの処理、およびフィルターを使用したカスタムクエリの実行を表示します。

また、プロセスレポートでは、レポートおよびクエリデータを CSV 形式で書き出すオプションも提供されます。

### アドホックレポート {#adhoc-reports}

![print-&amp;-color](assets/print-and-colour.png)

フィルターを使用して、データの特定の表示を取得します。

ID、期間、開始日と終了日、プロセスイニシエーターなどで、プロセスまたはタスクを検索できます。

複数のフィルターを組み合わせて、特定のレポートを作成できます。

その後、後で実行するようにレポートフィルターを保存できます。

### プロセス／タスクの履歴 {#process-task-history}

![file-management](assets/file-management.png)

AEM Forms サーバーは、多数のプロセスを並行して実行します。 これらのプロセスは、ある状態から別の状態への移行を続けます。 Forms のデータを一定の間隔でプロセスレポートリポジトリーに公開すると、プロセスレポートには、AEM Forms で実行中のプロセスに関する移行情報が保持されます。

### アクセス制御 {#access-control-br}

![名称未設定](assets/untitled.png)

プロセスレポートは、ユーザーインターフェイスへの権限ベースのアクセスを提供します。

つまり、レポート権限を持つユーザーのみがプロセスレポートのユーザーインターフェイスにアクセスできます。
