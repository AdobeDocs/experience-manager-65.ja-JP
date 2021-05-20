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
exl-id: 674d28dc-7353-49de-9e12-b1998e1509c7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# プロセスレポートの概要{#introduction-to-process-reporting}

![プロセスレポート](assets/process-reporting.png)

プロセスレポートは、AEM Formsのプロセスとタスクに関するレポートを作成および表示するために使用する、ブラウザーベースのツールです。

Process Reportingは、長時間実行されるプロセス、プロセス期間、ワークフローの量に関する情報をフィルター、表示できる、あらかじめ用意された一連のレポートを提供します。

さらに、プロセスレポートには、アドホッククエリを実行し、カスタムレポートビューをプロセスレポートユーザーインターフェイスに統合するためのインターフェイスが用意されています。

サポートされているブラウザーの一覧については、「[AEM Formsでサポートされているプラットフォーム](/help/forms/using/aem-forms-jee-supported-platforms.md)」を参照してください。

Process Reportingは、次のモジュールに基づいて構築されています。

* AEM Forms Databaseからのプロセスデータの読み取り
* 埋め込みのProcess Reportingリポジトリへのプロセスデータの公開
* レポートを表示するためのブラウザーベースのユーザーインターフェイスを提供します

## 主な機能{#key-capabilities}

### 常時稼動するレポート{#always-on-reporting}

![site-management](assets/site-management.png)

長時間実行されているプロセスのリスト、プロセス期間グラフの表示、フィルターを使用したカスタムクエリの実行を行います。

プロセスレポートには、レポートおよびクエリデータをCSV形式で書き出すオプションも用意されています。

### アドホックレポート{#adhoc-reports}

![print-&amp;-color](assets/print-&-colour.png)

フィルターを使用して、データの特定の表示を取得します。

ID、期間、開始日と終了日、プロセス開始者などで、プロセスまたはタスクを検索できます。

複数のフィルターを組み合わせて、特定のレポートを作成できます。

その後、後で実行するようにレポートフィルターを保存できます。

### プロセス/タスクの履歴{#process-task-history}

![ファイル管理](assets/file-management.png)

AEM Formsサーバーは、多数のプロセスを並行して実行します。 これらのプロセスは、ある状態から別の状態への移行を継続します。 Formsのデータを一定の間隔でProcess Reportingリポジトリに公開すると、Process ReportingはAEM Formsで実行されているプロセスに関する移行情報を保持します。

### アクセス制御 {#access-control-br}

![名称未設定](assets/untitled.png)

Process Reportingは、ユーザーインターフェイスに対する権限ベースのアクセスを提供します。

つまり、レポート権限を持つユーザーのみがProcess Reportingユーザーインターフェイスにアクセスできます。
