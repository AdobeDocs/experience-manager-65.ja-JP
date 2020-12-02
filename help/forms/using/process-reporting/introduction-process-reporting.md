---
title: プロセスレポートの概要
seo-title: プロセスレポートの概要
description: JEE上のAEM Formsのプロセスレポートの概要と主な機能
seo-description: JEE上のAEM Formsのプロセスレポートの概要と主な機能
uuid: a7f2455b-1b09-41a7-817b-e2e7a1ff9936
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4e83ed7b-3f48-4bf6-be4c-89f79949c1df
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---


# プロセスレポートの概要{#introduction-to-process-reporting}

![プロセスレポート](assets/process-reporting.png)

プロセスのレポートは、AEM Formsのプロセスとタスクに関するレポートを作成し、表示するために使用するブラウザベースのツールです。

プロセスレポートは、すぐに使用できる一連のレポートを提供し、長時間実行しているプロセス、プロセス期間、ワークフローの量に関する表示情報をフィルタリング、検索できます。

また、プロセスレポートは、アドホッククエリを実行し、カスタムレポート表示をプロセスレポートユーザーインターフェイスに統合するためのインターフェイスも提供します。

サポートされるブラウザーのリストについては、「[AEM Formsでサポートされるプラットフォーム](/help/forms/using/aem-forms-jee-supported-platforms.md)」を参照してください。

プロセスレポートは、次の機能を持つモジュールに基づいて構築されています。

* AEM Formsデータベースからプロセスデータを読み取ります
* 埋め込みプロセスレポートリポジトリへのプロセスデータの発行
* 表示レポートにブラウザベースのユーザインターフェイスを提供します。

## 主な機能{#key-capabilities}

### 常時オンレポート{#always-on-reporting}

![サイト管理](assets/site-management.png)

フィルターを使用して、長時間実行するプロセス、プロセス期間グラフおよびカスタムクエリを実行するリストを表示します。

プロセスレポートには、レポートおよびクエリデータをCSV形式で書き出すオプションも用意されています。

### アドホックレポート{#adhoc-reports}

![print-&amp;-color](assets/print-&-colour.png)

フィルターを使用して、データの特定の表示を取得します。

ID、期間、開始日、終了日、プロセス開始者などを使用して、プロセスまたはタスクを検索できます。

複数のフィルターを組み合わせて特定のレポートを作成できます。

その後、後で実行するレポートフィルターを保存できます。

### プロセス/タスク履歴{#process-task-history}

![ファイル管理](assets/file-management.png)

AEM Formsサーバは、多数のプロセスを並行して実行します。 これらのプロセスは、ある状態から別の状態への移行を継続します。 Formsのデータを一定の間隔でプロセスレポートリポジトリに発行することで、プロセスレポートはAEM Formsで実行されているプロセスに関する移行情報を保持します。

### アクセス制御 {#access-control-br}

![無題の](assets/untitled.png)

Process Reportingは、ユーザーインターフェイスへの権限ベースのアクセスを提供します。

つまり、レポート権限を持つユーザーのみがプロセスレポートユーザーインターフェイスにアクセスできます。
