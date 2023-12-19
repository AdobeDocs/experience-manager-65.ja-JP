---
title: Process Reporting の仕組み
description: JEE 上 の AEM Forms Process Reporting を構成するサービスの説明と Process Reporting UI の概要
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 100%

---


# Process Reporting の仕組み {#how-process-reporting-works}

Process Reporting は、JEE 上の AEM Forms のレポートモジュールです。

Process Reporting を使用すると、AEM Forms のプロセスとタスクに関するレポートを実行できます。

Process Reporting は、組み込みの Process Reporting リポジトリを使用して Forms データを公開します。その後、そのデータを使用してレポートを実行します。

Process Reporting は、以下のモジュールで構成されています。

* [ProcessDataPublisher サービス](/help/forms/using/process-reporting/process-reporting-architecture.md#p-processdatapublisher-service-br-p)
* [ProcessDataStorage サービス](/help/forms/using/process-reporting/process-reporting-architecture.md#p-processdatastorageprovider-service-br-p)
* [OSGi サービス](/help/forms/using/process-reporting/process-reporting-architecture.md#p-osgi-service-br-p)
* [クエリデータサーブレット](/help/forms/using/process-reporting/process-reporting-architecture.md#p-querydataservlet-service-br-p)
* [Process Reporting ユーザーインターフェイス](/help/forms/using/process-reporting/process-reporting-architecture.md#p-process-reporting-user-interface-br-p)

## Process Reporting のアーキテクチャー {#process-reporting-architecture-br}

![processreportingarchitecture](assets/processreportingarchitecture.png)

## Process Reporting モジュール {#process-reporting-modules}

### ProcessDataPublisher サービス {#processdatapublisher-service-br}

ProcessDataPublisher サーバーは、AEM Forms データベースで定期的に実行され、サービスの最後の実行以降に変更されたデータを抽出します。その後、Process Data Storage サービスにデータを公開します。

サービスの設定について詳しくは、[ProcessDataPublisher サービスの設定](/help/forms/using/process-reporting/install-start-process-reporting.md#p-reportconfiguration-service-p)を参照してください。

### ProcessDataStorageProvider サービス {#processdatastorageprovider-service-br}

ProcessDataStorageProvider サービスは、ProcessDataPublisher サービスからプロセスデータを受け取り、そのデータを Process Reporting リポジトリに保存します。

サービスの設定について詳しくは、[ProcessDataStorageProvider サービスの設定](/help/forms/using/process-reporting/install-start-process-reporting.md#p-to-configure-the-process-reporting-repository-locations-p)を参照してください。

### OSGi サービス {#osgi-service-br}

QueryDataServlet は、このサービスを使用して、Process Reporting リポジトリからレポートデータを取得します。

### QueryDataServlet サービス {#querydataservlet-service-br}

QueryDataServlet サービスは、Process Reporting ユーザーインターフェイスからクエリを受け入れます。

次に、このサービスは OSGi サービスを使用して関連するレポートデータを取得し、そのデータを処理して、ユーザーインターフェイスにデータを返します。

### Process Reporting ユーザーインターフェイス {#process-reporting-user-interface-br}

Process Reporting のユーザーインターフェイスは、web ブラウザーベースのインターフェイスです。このインターフェイスを使用して、AEM Forms データベースから公開されたプロセスおよびタスク情報を表示します。

### QueryDataServlet サービス {#querydataservlet-service-br-1}

QueryDataServlet サービスは、Process Reporting ユーザーインターフェイスからクエリを受け入れます。

次に、このサービスは OSGi サービスを使用して関連するレポートデータを取得し、そのデータを処理して、ユーザーインターフェイスにデータを返します。

### カスタムレポート {#custom-reports-br}

独自のカスタムレポートを作成し、これらのレポートを Process Reporting ユーザーインターフェイスの「カスタムレポート」タブに表示できます。

カスタムレポートを作成する手順については、[Process Reporting のカスタムレポート](/help/forms/using/process-reporting/process-reporting-custom-reports.md)記事の「カスタムレポートを作成するには」を参照してください。
