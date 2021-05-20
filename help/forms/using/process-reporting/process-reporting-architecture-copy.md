---
title: プロセスレポートの仕組み
seo-title: プロセスレポートの仕組み
description: JEE上のAEM Forms Process Reportingを構成するサービスの説明とProcess Reporting UIの概要
seo-description: JEE上のAEM Forms Process Reportingを構成するサービスの説明とProcess Reporting UIの概要
uuid: 4631b734-a679-495c-a708-2348bf22c1f7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
discoiquuid: a1af9920-5d2a-462f-bdee-ccec4c047c5b
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 1%

---


# プロセスレポートの仕組み{#how-process-reporting-works}

Process Reportingは、JEE上のAEM Formsのレポートモジュールです。

プロセスレポートを使用すると、AEM Formsのプロセスとタスクに関するレポートを実行できます。

Process Reportingは、組み込みのProcess Reportingリポジトリを使用してFormsデータを公開します。 その後、そのデータを使用してレポートを実行します。

Process Reportingは、次のモジュールで構成されています。

* [ProcessDataPublisherサービス](/help/forms/using/process-reporting/process-reporting-architecture.md#p-processdatapublisher-service-br-p)
* [ProcessDataStorageサービス](/help/forms/using/process-reporting/process-reporting-architecture.md#p-processdatastorageprovider-service-br-p)
* [OSGi サービス](/help/forms/using/process-reporting/process-reporting-architecture.md#p-osgi-service-br-p)
* [クエリデータサーブレット](/help/forms/using/process-reporting/process-reporting-architecture.md#p-querydataservlet-service-br-p)
* [Process Reportingユーザーインターフェイス](/help/forms/using/process-reporting/process-reporting-architecture.md#p-process-reporting-user-interface-br-p)

## プロセスレポートアーキテクチャ{#process-reporting-architecture-br}

![processreportingarchitecture](assets/processreportingarchitecture.png)

## プロセスレポートモジュール{#process-reporting-modules}

### ProcessDataPublisherサービス{#processdatapublisher-service-br}

ProcessDataPublisherサーバーは、AEM Formsデータベースで定期的に実行され、サービスの最後の実行以降に変更されたデータを抽出します。 次に、データをProcess Data Storageサービスに公開します。

サービスの設定について詳しくは、[ProcessDataPublisherサービスの設定](/help/forms/using/process-reporting/install-start-process-reporting.md#p-reportconfiguration-service-p)を参照してください。

### ProcessDataStorageProviderサービス{#processdatastorageprovider-service-br}

ProcessDataStorageProviderサービスは、ProcessDataPublisherサービスからプロセスデータを受け取り、そのデータをProcess Reportingリポジトリに保存します。

サービスの設定について詳しくは、[ProcessDataStorageProviderサービスの設定](/help/forms/using/process-reporting/install-start-process-reporting.md#p-to-configure-the-process-reporting-repository-locations-p)を参照してください。

### OSGi サービス {#osgi-service-br}

QueryDataServletは、このサービスを使用して、Process Reportingリポジトリからレポートデータを取得します。

### QueryDataServletサービス{#querydataservlet-service-br}

QueryDataServletサービスは、プロセスレポートユーザーインターフェイスからクエリを受け入れます。

次に、サービスはOSGiサービスを使用して関連するレポートデータを取得し、データを処理して、ユーザーインターフェイスにデータを返します。

### Process Reportingユーザーインターフェイス{#process-reporting-user-interface-br}

Process Reportingのユーザーインターフェイスは、Webブラウザーベースのインターフェイスです。 このインターフェイスを使用して、AEM Formsデータベースから公開されたプロセスおよびタスク情報を表示します。

### QueryDataServletサービス{#querydataservlet-service-br-1}

QueryDataServletサービスは、プロセスレポートユーザーインターフェイスからクエリを受け入れます。

次に、サービスはOSGiサービスを使用して関連するレポートデータを取得し、データを処理して、ユーザーインターフェイスにデータを返します。

### カスタムレポート{#custom-reports-br}

独自のカスタムレポートを作成し、これらのレポートをプロセスレポートユーザーインターフェイスの「カスタムレポート」タブに表示できます。

カスタムレポートを作成する手順については、「[プロセスレポートのカスタムレポート](/help/forms/using/process-reporting/process-reporting-custom-reports.md)」の記事「カスタムレポートを作成するには」を参照してください。
