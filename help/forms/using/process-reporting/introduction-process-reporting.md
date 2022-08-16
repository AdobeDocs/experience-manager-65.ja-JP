---
title: プロセスレポートの概要
seo-title: Introduction to Process Reporting
description: JEE 上の AEM Forms Process Reporting の概要と主な機能
seo-description: Introduction and key capabilities of AEM Forms on JEE Process Reporting
uuid: a7f2455b-1b09-41a7-817b-e2e7a1ff9936
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4e83ed7b-3f48-4bf6-be4c-89f79949c1df
docset: aem65
exl-id: 674d28dc-7353-49de-9e12-b1998e1509c7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 100%

---

# プロセスレポートの概要{#introduction-to-process-reporting}

![process-reporting](assets/process-reporting.png)

プロセスレポートは、AEM Forms のプロセスとタスクに関するレポートを作成および表示するために使用する、ブラウザーベースのツールです。

Process Reporting は、標準の一連のレポートを提供し、長時間実行中のプロセス、プロセス期間、ワークフローの量に関する情報のフィルタリングと表示をおこないます。

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

また、レポートおよびクエリデータを CSV 形式でエクスポートするオプションも提供されます。

### アドホックレポート {#adhoc-reports}

![print-&amp;-color](assets/print-&-colour.png)

フィルターを使用して、データの特定の表示を取得します。

ID、期間、開始日と終了日、プロセス開始者などで、プロセスまたはタスクを検索できます。

複数のフィルターを組み合わせて、特定のレポートを作成できます。

その後、後で実行するようにレポートフィルターを保存できます。

### プロセス／タスクの履歴 {#process-task-history}

![file-management](assets/file-management.png)

AEM Forms サーバーは、多数のプロセスを並行して実行します。これらのプロセスは、ある状態から別の状態への移行を続けます。Forms のデータを一定の間隔でプロセスレポートリポジトリーに公開すると、プロセスレポートには、AEM Forms で実行中のプロセスに関する移行情報が保持されます。

### アクセス制御 {#access-control-br}

![名称未設定](assets/untitled.png)

プロセスレポートは、ユーザーインターフェイスへの権限ベースのアクセスを提供します。

つまり、レポート権限を持つユーザーのみがプロセスレポートのユーザーインターフェイスにアクセスできます。
