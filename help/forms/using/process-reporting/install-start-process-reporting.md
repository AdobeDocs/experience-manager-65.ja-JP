---
title: プロセスレポートの概要
seo-title: プロセスレポートの概要
description: JEE上のAEM Formsのプロセスレポートを開始するために必要な手順
seo-description: JEE上のAEM Formsのプロセスレポートを開始するために必要な手順
uuid: 685cad39-da2c-411d-a0b0-201917438bcf
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
discoiquuid: 7c1fcde0-b983-4b24-bc19-fcee1d4f096b
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '1731'
ht-degree: 3%

---


# プロセスレポート使用の手引き{#getting-started-with-process-reporting}

プロセスのレポートにより、AEM Formsのユーザーは、AEM Formsの実装で現在定義されているAEM Formsプロセスに関する情報をクエリできます。 ただし、プロセスレポートは、AEM Formsリポジトリから直接データにアクセスすることはありません。 データは、最初に、ProcessDataPublisherおよびProcessDataStorageサービス&#x200B;*によって、スケジュールに基づいてプロセスレポートリポジトリに発行されます(*)。 次に、プロセスレポート内のレポートとクエリは、リポジトリに発行されたプロセスレポートデータから生成されます。 プロセスレポートは、Forms Workflowモジュールの一部としてインストールされます。

この記事では、AEM Formsデータをプロセスレポートリポジトリに発行する手順を説明します。 その後、プロセスレポートを使用してレポートやクエリを実行できます。 この記事では、プロセスレポートサービスを設定するために使用できるオプションについても説明します。

## プロセスレポートの前提条件{#process-reporting-pre-requisites}

### 不要なプロセス{#purge-non-essential-processes}を削除

現在Forms Workflowを使用している場合、AEM Formsのデータベースに大量のデータが含まれている可能性があります

プロセスレポート発行サービスは、現在データベースで使用可能なAEM Formsデータをすべて発行します。 つまり、レポートやクエリを実行したくないレガシーデータがデータベースに含まれている場合、レポートの必要がなくても、そのデータはすべてリポジトリに発行されます。 サービスを実行してデータをプロセスレポートリポジトリに発行する前に、このデータを削除することをお勧めします。 これにより、Publisherサービスと、レポート用にデータをクエリするサービスの両方のパフォーマンスが向上します。

AEM Formsのプロセスデータの削除について詳しくは、[プロセスデータの削除](https://help.adobe.com/en_US/livecycle/11.0/AdminHelp/WS92d06802c76abadb-5145d5d12905ce07e7-7cb2.2.html)を参照してください。

>[!NOTE]
>
>パージユーティリティのヒントとテクニックについては、[プロセスとジョブのパージ](https://www.adobe.com/content/dam/Adobe/en/devnet/livecycle/pdfs/purging_processes_jobs.pdf)のAdobe Developer Connectionの記事を参照してください。

## プロセスレポートサービスの設定{#configuring-process-reporting-services}

### プロセスデータの発行をスケジュール{#schedule-process-data-publishing}

プロセスレポートサービスは、AEM Formsデータベースからプロセスレポートリポジトリにデータをスケジュールに基づいて発行します。

この操作はリソースを大量に消費し、AEM Formsサーバーのパフォーマンスに影響を与える可能性があります。 このスケジュールは、AEM Formsサーバーのビジータイムスロットの外側で行うことをお勧めします。

デフォルトでは、データの公開は毎日午前2時に実行されるようにスケジュールされています。

次の手順を実行して、発行スケジュールを変更します。

>[!NOTE]
>
>クラスターでAEM Forms実装を実行している場合は、クラスターの各ノードで次の手順を実行します。

1. AEM Formsサーバーインスタンスを停止します。
1. &#x200B;

   * （Windowsの場合）`[JBoss root]/bin/run.conf.bat`ファイルをエディターで開きます。
   * （Linux、AIXおよびSolarisの場合）`[JBoss root]/bin/run.conf.sh`ファイルをエディターで開きます。

1. 追加JVM引数`-Dreporting.publisher.cron = <expression>.`

   例：次のcron式は、プロセスレポートがAEM Formsデータをプロセスレポートリポジトリに5時間ごとに発行する原因となります。

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. `run.conf.bat`ファイルを保存して閉じます。

1. AEM Formsサーバーインスタンスを再起動します。

1. AEM Formsサーバーインスタンスを停止します。
1. WebSphere Administrative Consoleにログインします。ナビゲーションツリーで、**Servers**/**Application servers**&#x200B;をクリックし、右側のウィンドウでサーバー名をクリックします。

1. 「Server Infrastructure」で、**Java and Process Management**/**Process Definition**&#x200B;をクリックします。

1. 「Additional Properties」で、「**Java Virtual Machine**」をクリックします。

   「Generic JVM arguments」ボックスに引数`-Dreporting.publisher.cron = <expression>.`を追加します。

   **例**:次のcron式は、プロセスレポートがAEM Formsデータをプロセスレポートリポジトリに5時間ごとに発行する原因となります。

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. 「**Apply**」をクリックし、「OK」をクリックして、「**Save directly to the master configuration**」をクリックします。
1. AEM Formsサーバーインスタンスを再起動します。
1. AEM Formsサーバーインスタンスを停止します。
1. WebLogic管理コンソールにログインします。 WebLogic管理コンソールのデフォルトアドレスは`https://[hostname]:[port]/console`です。
1. Change Center で、「**Lock &amp; Edit**」をクリックします。
1. 「Domain Structure」で、**Environment**／**Servers** をクリックし、右側のウィンドウで、管理対象サーバー名をクリックします。
1. 次の画面で、「**Configuration**」タブ／「**Server Start**」タブをクリックします。
1. 「Arguments」ボックスに、JVM引数`-Dreporting.publisher.cron = <expression>`を追加します。

   **例**:次のcron式は、プロセスレポートがAEM Formsデータをプロセスレポートリポジトリに5時間ごとに発行する原因となります。

   `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. 「**Save**」をクリックし、「**Activate Changes**」をクリックします。
1. AEM Formsサーバーインスタンスを再起動します。

![processdatapublisherservice](assets/processdatapublisherservice.png)

### ProcessDataStorageサービス{#processdatastorage-service}

ProcessDataStorageProviderサービスは、ProcessDataPublisherサービスからプロセスデータを受け取り、データをプロセスレポートリポジトリに保存します。

公開サイクルごとに、データは事前定義されたルートフォルダーのサブフォルダーに保存されます。

管理コンソールを使用して、ルート(**デフォルト**:`/content/reporting/pm`)場所とサブフォルダ(**デフォルト**:`/yyyy/mm/dd/hh/mi/ss`)プロセスデータが保存される階層形式。

#### プロセスレポートリポジトリの場所を設定するには{#to-configure-the-process-reporting-repository-locations}

1. 管理者の資格情報を使用して&#x200B;**管理コンソール**&#x200B;にログインします。 管理コンソールのデフォルトURLは`https://'[server]:[port]'/adminui`です
1. **ホーム**/**サービス**/**アプリケーションおよびサービス**/**サービスの管理**&#x200B;に移動し、**ProcessDataStorageProvider**&#x200B;サービスを開きます。

   ![process-data-ストレージサービス](assets/process-data-storage-service.png)

   **RootFolder**

   レポートのためにプロセスデータが格納されるCRXの場所です。

   `Default`: `/content/reporting/pm`

   **フォルダ階層**

   プロセス作成時間に基づいて、プロセスデータが格納されるフォルダー階層。

   `Default`:  `/yyyy/mm/dd/hh/mi/ss`

1. 「**保存**」をクリックします。

### ReportConfigurationサービス{#reportconfiguration-service}

ReportConfigurationサービスは、プロセスレポートがプロセスレポートクエリサービスを設定する際に使用します。

#### ReportingConfigurationサービスを構成するには{#to-configure-the-reportingconfiguration-service}

1. CRX管理者の資格情報を使用して&#x200B;**Configuration Manager**&#x200B;にログインします。 Configuration ManagerのデフォルトURLは`https://'[server]:[port]'/lc/system/console/configMgr`です
1. **ReportingConfiguration**&#x200B;サービスを開きます。
1. **レコード数**

   リポジトリでクエリを実行すると、結果に大量のレコードが含まれる可能性があります。 結果セットのサイズが大きい場合、クエリの実行によってサーバーリソースが消費される可能性があります。

   大きな結果セットを処理するために、ReportConfigurationサービスはクエリ処理をレコードのバッチに分割します。 これにより、システムの負荷が軽減されます。

   `Default`:  `1000`

   **CRXストレージパス**

   レポートのためにプロセスデータが格納されるCRX上の場所。

   `Default`:  `/content/reporting/pm`

   >[!NOTE]
   >
   >これは、ProcessDataStorage設定オプション&#x200B;**ルートフォルダー**&#x200B;で指定した場所と同じです。
   >
   >
   >ProcessDataStorage設定の「Root Folder」オプションを更新する場合は、ReportConfigurationサービスのCRXストレージパスの場所を更新する必要があります。

1. 「**保存**」をクリックし、**CQ Configuration Manager**&#x200B;を閉じます。

### ProcessDataPublisherサービス{#processdatapublisher-service}

ProcessDataPublisherサービスは、AEM Formsデータベースからプロセスデータをインポートし、ストレージのためにデータをProcessDataStorageProviderサービスに発行します。

#### ProcessDataPublisherサービスを設定するには   {#to-configure-processdatapublisher-service-nbsp}

1. 管理者の資格情報を使用して&#x200B;**管理コンソール**&#x200B;にログインします。

   デフォルトの URL は `https://'server':port]/adminui/` です。

1. **ホーム**/**サービス**/**アプリケーションおよびサービス**/**サービスの管理**&#x200B;に移動し、**ProcessDataPublisher**&#x200B;サービスを開きます。

![processdatapublisherservice-1](assets/processdatapublisherservice-1.png)

**データの発行**

開始発行プロセスデータに対してこのオプションを有効にします。 デフォルトでは、このオプションは無効になっています。

プロセスレポートコンポーネントに関連するすべての設定が適切に設定されている場合にのみ、プロセスレポートを有効にします。

または、不要になったプロセスデータの公開を無効にする場合は、このオプションを使用します。

`Default`:  `Off`

**バッチ間隔（秒）**

ProcessDataPublisherサービスが実行されるたびに、サービスが最後に実行された後の時間をBatch Intervalで分割します。 次に、AEM Formsデータの各間隔を別々に処理します。

これは、サイクル内の各実行（バッチ）中に、発行者が処理するデータのサイズを制御するのに役立ちます。

例えば、発行者が毎日実行する場合、1回の実行で1日分のデータ全体を処理する代わりに、デフォルトでは、1日に1時間ずつ24個のバッチに分割されます。

`Default`:  `3600`

`Unit`:  `Seconds`

**ロックタイムアウト（秒）**

パブリッシャーサービスは、開始がデータを処理する際にロックを取得するので、パブリッシャーの複数のインスタンスが開始を実行して同時にデータを処理することがないようにします。

ロックを取得したパブリッシャーサービスが、ロックのタイムアウト値で定義された秒数だけアイドル状態の場合、そのロックは解放され、他のパブリッシャーサービスインスタンスの処理を続行できます。

`Default`:  `3600`

`Unit`:  `Seconds`

**データの発行元**

AEM Forms環境には、環境が設定された時点のデータが含まれます。

デフォルトでは、ProcessDataPublisherサービスは、AEM Formsデータベースからすべてのデータをインポートします。

レポートのニーズに応じて、特定の日時以降にデータのレポートやクエリを実行する場合は、日時を指定することをお勧めします。 その後、発行サービスはその時刻以降の日付を発行します。

`Default`:  `01-01-1970 00:00:00`

`Format`:  `dd-MM-yyyy HH:mm:ss`

## プロセスレポートユーザーインターフェイスへのアクセス{#accessing-the-process-reporting-user-interface}

プロセスレポートのユーザーインターフェイスはブラウザーベースです。

プロセスレポートを設定した後、AEM Formsのインストール先の次の場所で、プロセスレポートの操作に開始できます。

`https://<server>:<port>/lc/pr`

### プロセスレポートにログイン{#log-in-to-process-reporting}

プロセスレポートのURL(https://&lt;server>:&lt;port>/lc/pr)に移動すると、ログイン画面が表示されます。

資格情報を指定してプロセスレポートモジュールにログインします。

>[!NOTE]
>
>プロセスレポートユーザーインターフェイスにログインするには、次のAEM Forms権限が必要です。
>
>`PERM_PROCESS_REPORTING_USER`

![プロセスレポートにログイン](assets/capture1_new.png)

プロセスレポートにログインすると、**[!UICONTROL ホーム]**&#x200B;画面が表示されます。

### プロセスレポートのホーム画面{#process-reporting-home-screen}

![process-レポート-home-screen](assets/process-reporting-home-screen.png)

**プロセスレポートツリー表示:** ホーム画面の左側のツリー表示には、プロセスレポートモジュールの項目が含まれています。

ツリー表示は、次の最上位レベルの項目で構成されます。

**レポート：** この項目には、プロセスレポートに付属の既成のレポートが含まれています。

事前定義済みのレポートについて詳しくは、「[プロセスレポートでの事前定義済みのレポート](/help/forms/using/process-reporting/pre-defined-reports-in-process-reporting.md)」を参照してください。

**アドホッククエリ:** この項目には、プロセスおよびタスクのフィルターベースの検索を実行するためのオプションが含まれます。

アドホッククエリについて詳しくは、[プロセスレポートのアドホッククエリ](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md)を参照してください。

**カスタム：「カスタム」ノード** には、作成したカスタムレポートが表示されます。

カスタムレポートを作成して表示する手順については、[プロセスレポートのカスタムレポート](/help/forms/using/process-reporting/process-reporting-custom-reports.md)を参照してください。

**プロセスレポートのタイトルバー：プロセスレポート** のタイトルバーには、ユーザーインターフェイスで作業する際に使用できる一般的なオプションが含まれています。

**プロセスレポートのタイトル：** プロセスレポートのタイトルは、タイトルバーの左隅に表示されます。

タイトルをクリックすると、いつでもホーム画面に戻ります。

**最終更新時間：プロセス** データは、スケジュールに基づいて、AEM Formsデータベースからプロセスレポートリポジトリに発行されます。

「Last Update Time」には、データ更新がプロセスレポートリポジトリにプッシュされた最後の日時が表示されます。

データ発行サービスとこのサービスのスケジュール方法について詳しくは、「プロセスレポート — はじめに」の「[プロセスデータの発行のスケジュール](/help/forms/using/process-reporting/install-start-process-reporting.md#p-schedule-process-data-publishing-p)」を参照してください。

**プロセスレポートユーザー：** ログインしたユーザー名は、最終更新時刻の右側に表示されます。

**プロセスレポートのタイトルバードロップダウンリスト:** プロセスレポートのタイトルバーの右隅にあるドロップダウンリストには、次のオプションが含まれています。

* **[!UICONTROL 同期]**:埋め込まれたプロセスレポートリポジトリをAEM Formsデータベースと同期します。
* **[!UICONTROL ヘルプ]**:プロセスレポートのヘルプドキュメントの表示
* **[!UICONTROL ログアウト]**:プロセスレポートからのログアウト
