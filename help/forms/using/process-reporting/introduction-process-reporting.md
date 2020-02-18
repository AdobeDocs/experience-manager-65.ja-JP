---
title: プロセスレポートの概要
seo-title: プロセスレポートの概要
description: JEE上のAEM Forms Process Reportingの概要と主な機能
seo-description: JEE上のAEM Forms Process Reportingの概要と主な機能
uuid: a7f2455b-1b09-41a7-817b-e2e7a1ff9936
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4e83ed7b-3f48-4bf6-be4c-89f79949c1df
docset: aem65
translation-type: tm+mt
source-git-commit: d9975c0dcc02ae71ac64aadb6b4f82f7c993f32c

---


# プロセスレポートの概要{#introduction-to-process-reporting}

![プロセス報告](assets/process-reporting.png)

プロセスレポートは、AEM Formsのプロセスとタスクに関するレポートを作成および表示するために使用するブラウザベースのツールです。

プロセスレポートは、すぐに使用できる一連のレポートを提供し、長時間実行中のプロセス、プロセス期間、ワークフローの量に関する情報をフィルター、表示できます。

また、プロセスレポートには、アドホッククエリを実行し、カスタムレポートビューをプロセスレポートユーザーインターフェイスに統合するためのインターフェイスも用意されています。

サポートされるブラウザのリストについては、「 [AEM Formsでサポートされるプラットフォーム](/help/forms/using/aem-forms-jee-supported-platforms.md)」を参照してください。

Process Reportingは、次の機能を持つモジュールに基づいて構築されています。

* AEM Formsデータベースからのプロセスデータの読み取り
* 埋め込みのProcess Reportingリポジトリへのプロセスデータの発行
* レポートを表示するためのブラウザベースのユーザインターフェイスを提供します。

## Key Capabilities {#key-capabilities}

### 常にオンのレポート {#always-on-reporting}

![現場管理](assets/site-management.png)

長時間実行されるプロセスのリスト、プロセス期間グラフの表示、およびフィルターを使用したカスタムクエリの実行を行います。

また、プロセスレポートには、レポートおよびクエリデータをCSV形式で書き出すオプションも用意されています。

### アドホックレポート {#adhoc-reports}

![print-&amp;-color](assets/print-&-colour.png)

フィルターを使用して、データの特定のビューを取得します。

ID、期間、開始日と終了日、プロセス開始者などでプロセスやタスクを検索できます。

複数のフィルターを組み合わせて、特定のレポートを作成できます。

その後、後で実行するようにレポートフィルターを保存できます。

### プロセス/タスクの履歴 {#process-task-history}

![ファイル管理](assets/file-management.png)

AEM Formsサーバーは、多数のプロセスを並行して実行します。 これらのプロセスは、ある状態から別の状態への移行を継続します。 Formsデータを一定の間隔でProcess Reportingリポジトリに発行すると、Process ReportingはAEM Formsで実行されているプロセスに関する移行情報を保持します。

### アクセス制御 {#access-control-br}

![無題の](assets/untitled.png)

Process Reporingは、ユーザーインターフェイスへの権限ベースのアクセスを提供します。

つまり、レポート権限を持つユーザーのみがプロセスレポートのユーザーインターフェイスにアクセスできます。

[サポートへのお問い合わせ](https://www.adobe.com/account/sign-in.supportportal.html)
