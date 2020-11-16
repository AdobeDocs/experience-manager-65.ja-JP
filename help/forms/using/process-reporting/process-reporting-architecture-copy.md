---
title: プロセスレポートの仕組み
seo-title: プロセスレポートの仕組み
description: JEE上のAEM Formsのプロセスレポートを構成するサービスの説明とプロセスレポートUIの紹介
seo-description: JEE上のAEM Formsのプロセスレポートを構成するサービスの説明とプロセスレポートUIの紹介
uuid: 4631b734-a679-495c-a708-2348bf22c1f7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
discoiquuid: a1af9920-5d2a-462f-bdee-ccec4c047c5b
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 1%

---


# プロセスレポートの仕組み {#how-process-reporting-works}

プロセスレポートは、JEE上のAEM Formsのレポートモジュールです。

プロセスレポートを使用すると、AEM Formsのプロセスとタスクに関するレポートを実行できます。

プロセスレポートは、埋め込みのプロセスレポートリポジトリを使用してFormsデータを発行します。 その後、そのデータを使用してレポートが実行されます。

プロセスレポートは、次のモジュールで構成されます。

* [ProcessDataPublisherサービス](/help/forms/using/process-reporting/process-reporting-architecture.md#p-processdatapublisher-service-br-p)
* [ProcessDataStorageサービス](/help/forms/using/process-reporting/process-reporting-architecture.md#p-processdatastorageprovider-service-br-p)
* [OSGi サービス](/help/forms/using/process-reporting/process-reporting-architecture.md#p-osgi-service-br-p)
* [クエリデータサーブレット](/help/forms/using/process-reporting/process-reporting-architecture.md#p-querydataservlet-service-br-p)
* [プロセスレポートユーザーインターフェイス](/help/forms/using/process-reporting/process-reporting-architecture.md#p-process-reporting-user-interface-br-p)

## プロセスレポートアーキテクチャ {#process-reporting-architecture-br}

![processreportingarchitecture](assets/processreportingarchitecture.png)

## プロセスレポートモジュール {#process-reporting-modules}

### ProcessDataPublisherサービス {#processdatapublisher-service-br}

ProcessDataPublisherサーバーは定期的にAEM Formsデータベース上で実行され、サービスの最後の実行以降に変更されたデータを抽出します。 次に、データをProcess Dataストレージサービスに発行します。

サービスの設定について詳しくは、「ProcessDataPublisherサービスの [設定](/help/forms/using/process-reporting/install-start-process-reporting.md#p-reportconfiguration-service-p)」を参照してください。

### ProcessDataStorageProviderサービス {#processdatastorageprovider-service-br}

ProcessDataStorageProviderサービスは、ProcessDataPublisherサービスからプロセスデータを受け取り、データをプロセスレポートリポジトリに保存します。

サービスの設定について詳しくは、「ProcessDataStorageProviderサービスの [設定](/help/forms/using/process-reporting/install-start-process-reporting.md#p-to-configure-the-process-reporting-repository-locations-p)」を参照してください。

### OSGi サービス {#osgi-service-br}

QueryDataServletは、このサービスを使用して、プロセスレポートリポジトリからレポートデータを取得します。

### QueryDataServletサービス {#querydataservlet-service-br}

QueryDataServletサービスは、プロセスレポートユーザーインターフェイスからクエリを受け入れます。

次に、サービスはOSGiサービスを使用して関連するレポートデータを取得し、データを処理し、データをユーザーインターフェイスに返します。

### プロセスレポートユーザーインターフェイス {#process-reporting-user-interface-br}

プロセスレポートのユーザーインターフェイスは、Webブラウザーベースのインターフェイスです。 このインターフェースを使用して、AEM Formsデータベースから公開された表示処理とタスク情報を行います。

### QueryDataServletサービス {#querydataservlet-service-br-1}

QueryDataServletサービスは、プロセスレポートユーザーインターフェイスからクエリを受け入れます。

次に、サービスはOSGiサービスを使用して関連するレポートデータを取得し、データを処理し、データをユーザーインターフェイスに返します。

### カスタムレポート {#custom-reports-br}

独自のカスタムレポートを作成して、プロセスレポートユーザーインターフェイスの「カスタムレポート」タブに表示できます。

カスタムレポートを作成する手順については、プロセスレポートのカスタムレポートの記事でカスタムレポートを作成するにはを参照して [ください](/help/forms/using/process-reporting/process-reporting-custom-reports.md)。
