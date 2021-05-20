---
title: プロセスレポートの仕組み
seo-title: プロセスレポートの仕組み
description: JEE上のAEM Forms Process Reportingを構成するサービスの説明とProcess Reporting UIの概要
seo-description: JEE上のAEM Forms Process Reportingを構成するサービスの説明とProcess Reporting UIの概要
uuid: 37e31985-088a-4ef6-ba57-10a01597a873
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
discoiquuid: a6ff50df-273d-48f7-b0c6-0e69e900b97f
docset: aem65
exl-id: 66dfac36-5b7e-40be-9921-efa9f2a9521c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 1%

---

# プロセスレポートの仕組み{#how-process-reporting-works}

Process Reportingは、JEE上のAEM Formsのレポートモジュールです。

プロセスレポートを使用すると、AEM Formsのプロセスとタスクに関するレポートを実行できます。

Process Reportingは、組み込みのProcess Reportingリポジトリを使用してFormsデータを公開します。 その後、そのデータを使用してレポートを実行します。

Process Reportingは、次のモジュールで構成されています。

* [ProcessDataPublisherサービス](#processdatapublisher-service-br-p)
* [ProcessDataStorageサービス](#processdatastorageprovider-service-br-p)
* [OSGi サービス](#osgi-service-br-p)
* [クエリデータサーブレット](#querydataservlet-service-br-p)
* [Process Reportingユーザーインターフェイス](#process-reporting-user-interface-br-p)

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

プロセス・レポートのユーザー・インタフェースの概要は、[プロセス・レポートのユーザー・インタフェース](/help/forms/using/process-reporting/introduction-process-reporting.md)を参照してください。

### QueryDataServletサービス{#querydataservlet-service-br-1}

QueryDataServletサービスは、プロセスレポートユーザーインターフェイスからクエリを受け入れます。

次に、サービスはOSGiサービスを使用して関連するレポートデータを取得し、データを処理して、ユーザーインターフェイスにデータを返します。

### カスタムレポート{#custom-reports-br}

独自のカスタムレポートを作成し、これらのレポートをプロセスレポートユーザーインターフェイスの「カスタムレポート」タブに表示できます。

カスタムレポートを作成する手順については、「[プロセスレポートのカスタムレポート](/help/forms/using/process-reporting/process-reporting-custom-reports.md)」の記事「カスタムレポートを作成するには」を参照してください。
