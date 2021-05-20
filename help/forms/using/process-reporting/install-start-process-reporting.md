---
title: プロセスレポートの概要
seo-title: プロセスレポートの概要
description: JEE上のAEM Forms Process Reportingの使用を開始するために必要な手順
seo-description: JEE上のAEM Forms Process Reportingの使用を開始するために必要な手順
uuid: 685cad39-da2c-411d-a0b0-201917438bcf
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
discoiquuid: 7c1fcde0-b983-4b24-bc19-fcee1d4f096b
docset: aem65
exl-id: 1272e854-fa64-4bfd-b073-8fbcf210e9b5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1731'
ht-degree: 3%

---

# プロセスレポートの概要{#getting-started-with-process-reporting}

プロセスレポートを使用すると、AEM Formsユーザーは、AEM Forms実装で現在定義されているAEM Formsプロセスに関する情報をクエリできます。 ただし、プロセスレポートは、AEM Formsリポジトリから直接データにアクセスするわけではありません。 データは、最初にProcessDataPublisherおよびProcessDataStorageサービス&#x200B;*によって、スケジュールに従ってProcess Reportingリポジトリに発行されます。*&#x200B;次に、プロセスレポートのレポートとクエリは、リポジトリに公開されたプロセスレポートデータから生成されます。 Process Reportingは、インストールモジュールの一部としてForms Workflowされます。

この記事では、Process ReportingリポジトリへのAEM Formsデータの公開を有効にする手順について詳しく説明します。 その後、プロセスレポートを使用して、レポートとクエリを実行できます。 この記事では、Process Reportingサービスの設定に使用できるオプションについても説明します。

## プロセスレポートの前提条件{#process-reporting-pre-requisites}

### 不要なプロセス{#purge-non-essential-processes}をパージします

現在AEM Formsを使用している場合は、Forms Workflowに大量のデータが含まれている可能性があります

Process Reporting公開サービスは、データベースで現在使用可能なすべてのAEM Formsデータを公開します。 つまり、レポートやクエリを実行しないレガシーデータがデータベースに含まれている場合、そのデータはレポートに必要ないにもかかわらず、すべてリポジトリに発行されます。 このデータは、サービスを実行してProcess Reportingリポジトリにデータを発行する前にパージすることをお勧めします。 これにより、パブリッシャーサービスと、レポート用にデータをクエリするサービスの両方のパフォーマンスが向上します。

AEM Formsのプロセスデータのパージについて詳しくは、[プロセスデータのパージ](https://help.adobe.com/en_US/livecycle/11.0/AdminHelp/WS92d06802c76abadb-5145d5d12905ce07e7-7cb2.2.html)を参照してください。

>[!NOTE]
>
>パージユーティリティのヒントとテクニックについては、[プロセスとジョブのパージ](https://www.adobe.com/content/dam/Adobe/en/devnet/livecycle/pdfs/purging_processes_jobs.pdf)に関するAdobe Developer Connectionの記事を参照してください。

## Process Reportingサービスの設定{#configuring-process-reporting-services}

### プロセスデータの発行のスケジュール{#schedule-process-data-publishing}

Process Reportingサービスは、AEM FormsデータベースからProcess Reportingリポジトリにデータをスケジュールに従って公開します。

この操作はリソースを大量に消費する可能性があり、AEM Formsサーバーのパフォーマンスに影響を与える可能性があります。 AEM Formsサーバーのビジータイムスロット外でスケジュールすることをお勧めします。

デフォルトでは、データの公開は毎日午前2時に実行されるようにスケジュールされています。

公開スケジュールを変更するには、次の手順を実行します。

>[!NOTE]
>
>クラスターでAEM Forms実装を実行している場合は、クラスターの各ノードで次の手順を実行します。

1. AEM Formsサーバーインスタンスを停止します。
1. &#x200B;

   * （Windowsの場合）`[JBoss root]/bin/run.conf.bat`ファイルをエディターで開きます。
   * （Linux、AIX、Solarisの場合）エディターの`[JBoss root]/bin/run.conf.sh`ファイル。

1. JVM引数`-Dreporting.publisher.cron = <expression>.`を追加します。

   例：次のCron式を使用すると、プロセスレポートでは5時間ごとにAEM FormsデータがProcess Reportingリポジトリに公開されます。

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. `run.conf.bat` ファイルを保存して閉じます。

1. AEM Formsサーバーインスタンスを再起動します。

1. AEM Formsサーバーインスタンスを停止します。
1. WebSphere Administrative Consoleにログインします。ナビゲーションツリーで、**Servers** > **Application servers**&#x200B;をクリックし、右側のウィンドウで、サーバー名をクリックします。

1. 「Server Infrastructure」で、「**Java and Process Management**」>「**Process Definition**」をクリックします。

1. 「Additional Properties」で、「**Java Virtual Machine**」をクリックします。

   「 Generic JVM arguments 」ボックスに、引数`-Dreporting.publisher.cron = <expression>.`を追加します。

   **例**:次のCron式を使用すると、プロセスレポートでは5時間ごとにAEM FormsデータがProcess Reportingリポジトリに公開されます。

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. **「**&#x200B;を適用」をクリックし、「OK」をクリックして、「**マスター設定に直接保存**」をクリックします。
1. AEM Formsサーバーインスタンスを再起動します。
1. AEM Formsサーバーインスタンスを停止します。
1. WebLogic管理コンソールにログインします。 WebLogic管理コンソールのデフォルトアドレスは`https://[hostname]:[port]/console`です。
1. Change Center で、「**Lock &amp; Edit**」をクリックします。
1. 「Domain Structure」で、**Environment**／**Servers** をクリックし、右側のウィンドウで、管理対象サーバー名をクリックします。
1. 次の画面で、「**Configuration**」タブ／「**Server Start**」タブをクリックします。
1. 「引数」ボックスに、JVM引数`-Dreporting.publisher.cron = <expression>`を追加します。

   **例**:次のCron式を使用すると、プロセスレポートでは5時間ごとにAEM FormsデータがProcess Reportingリポジトリに公開されます。

   `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. 「**Save**」をクリックし、「**Activate Changes**」をクリックします。
1. AEM Formsサーバーインスタンスを再起動します。

![processdatapublisherservice](assets/processdatapublisherservice.png)

### ProcessDataStorageサービス{#processdatastorage-service}

ProcessDataStorageProviderサービスは、ProcessDataPublisherサービスからプロセスデータを受け取り、そのデータをProcess Reportingリポジトリに保存します。

公開サイクルごとに、データは事前定義されたルートフォルダーのサブフォルダーに保存されます。

管理コンソールを使用して、ルート(**default**)を設定できます。`/content/reporting/pm`)の場所とサブフォルダー(**default**:`/yyyy/mm/dd/hh/mi/ss`)プロセスデータを保存する階層形式。

#### Process Reportingリポジトリの場所{#to-configure-the-process-reporting-repository-locations}を設定するには

1. 管理者の資格情報を使用して&#x200B;**管理コンソール**&#x200B;にログインします。 管理コンソールのデフォルトURLは`https://'[server]:[port]'/adminui`です。
1. **ホーム** / **サービス** / **アプリケーションおよびサービス** /**サービスの管理**&#x200B;に移動し、**ProcessDataStorageProvider**&#x200B;サービスを開きます。

   ![process-data-storage-service](assets/process-data-storage-service.png)

   **RootFolder**

   レポート用にプロセスデータが格納されるCRXの場所。

   `Default`: `/content/reporting/pm`

   **フォルダー階層**

   プロセス作成時間に基づいてプロセスデータが格納されるフォルダー階層。

   `Default`:  `/yyyy/mm/dd/hh/mi/ss`

1. 「**保存**」をクリックします。

### ReportConfigurationサービス{#reportconfiguration-service}

ReportConfigurationサービスは、プロセスレポートクエリサービスを設定するためにプロセスレポートで使用されます。

#### ReportingConfigurationサービス{#to-configure-the-reportingconfiguration-service}を構成するには、以下を実行します。

1. CRX管理者の資格情報を使用して&#x200B;**Configuration Manager**&#x200B;にログインします。 Configuration ManagerのデフォルトURLは`https://'[server]:[port]'/lc/system/console/configMgr`です。
1. **ReportingConfiguration**&#x200B;サービスを開きます。
1. **レコード数**

   リポジトリでクエリを実行する場合、結果に大量のレコードが含まれる可能性があります。 結果セットが大きい場合、クエリの実行でサーバーリソースを消費する可能性があります。

   大きな結果セットを処理するために、 ReportConfigurationサービスは、クエリ処理を複数のレコードに分割します。 これにより、システムの負荷が軽減されます。

   `Default`:  `1000`

   **CRXストレージパス**

   レポート用にプロセスデータが格納されるCRXの場所。

   `Default`:  `/content/reporting/pm`

   >[!NOTE]
   >
   >これは、ProcessDataStorage設定オプション&#x200B;**Root Folder**&#x200B;で指定した場所と同じです。
   >
   >
   >ProcessDataStorage設定の「Root Folder」オプションを更新する場合は、ReportConfigurationサービスの「CRX Storage Path」の場所を更新する必要があります。

1. 「**保存**」をクリックして、**CQ Configuration Manager**&#x200B;を閉じます。

### ProcessDataPublisherサービス{#processdatapublisher-service}

ProcessDataPublisherサービスは、AEM Formsデータベースからプロセスデータをインポートし、格納用にそのデータをProcessDataStorageProviderサービスに公開します。

#### ProcessDataPublisherサービスを設定するには   {#to-configure-processdatapublisher-service-nbsp}

1. 管理者の資格情報を使用して&#x200B;**管理コンソール**&#x200B;にログインします。

   デフォルトの URL は `https://'server':port]/adminui/` です。

1. **ホーム** / **サービス** / **アプリケーションおよびサービス** /**サービスの管理**&#x200B;に移動し、**ProcessDataPublisher**&#x200B;サービスを開きます。

![processdatapublisherservice-1](assets/processdatapublisherservice-1.png)

**データの公開**

プロセスデータの公開を開始するには、このオプションを有効にします。 デフォルトでは、このオプションは無効になっています。

Process Reportingコンポーネントに関連するすべての設定が適切に設定されている場合にのみ、Process Reportingを有効にします。

または、このオプションを使用して、プロセスデータの公開が不要になったときに無効にします。

`Default`:  `Off`

**バッチ間隔（秒）**

ProcessDataPublisherサービスが実行されるたびに、サービスは最初にBatch Intervalによってサービスの最後の実行からの時間を分割します。 次に、サービスはAEM Formsデータの各間隔を個別に処理します。

これは、1サイクル内の各実行（バッチ）中に、パブリッシャーが処理するデータのサイズを制御するのに役立ちます。

例えば、パブリッシャーが毎日実行する場合、1回の実行で1日分のデータ全体を処理する代わりに、デフォルトでは、1時間ごとに24個のバッチに処理を分割します。

`Default`:  `3600`

`Unit`:  `Seconds`

**ロックタイムアウト（秒）**

パブリッシャーサービスは、データの処理を開始する際にロックを取得し、パブリッシャーの複数のインスタンスが実行を開始してデータを同時に処理しないようにします。

ロックを取得したパブリッシャーサービスがロックタイムアウト値で定義された秒数だけアイドル状態の場合は、そのロックが解除され、他のパブリッシャーサービスインスタンスが処理を続行できるようになります。

`Default`:  `3600`

`Unit`:  `Seconds`

**データの公開元**

AEM Forms環境には、環境が設定された時点のデータが含まれます。

デフォルトでは、ProcessDataPublisherサービスは、AEM Formsデータベースからすべてのデータをインポートします。

レポートのニーズに応じて、特定の日時の後にデータに対してレポートやクエリを実行する予定がある場合は、日時を指定することをお勧めします。 その後、公開サービスはその日付になります。

`Default`:  `01-01-1970 00:00:00`

`Format`:  `dd-MM-yyyy HH:mm:ss`

## Process Reportingユーザーインターフェイス{#accessing-the-process-reporting-user-interface}へのアクセス

プロセスレポートのユーザーインターフェイスは、ブラウザーベースです。

Process Reportingを設定したら、AEM Formsの次の場所でProcess Reportingの使用を開始できます。

`https://<server>:<port>/lc/pr`

### プロセスレポートにログインします。 {#log-in-to-process-reporting}

Process Reporting URL(https://&lt;server>:&lt;port>/lc/pr)に移動すると、ログイン画面が表示されます。

プロセスレポートモジュールにログインするための資格情報を指定します。

>[!NOTE]
>
>Process Reportingユーザーインターフェイスにログインするには、次のAEM Forms権限が必要です。
>
>`PERM_PROCESS_REPORTING_USER`

![プロセスレポートへのログイン](assets/capture1_new.png)

Process Reportingにログインすると、**[!UICONTROL ホーム]**&#x200B;画面が表示されます。

### プロセスレポートのホーム画面{#process-reporting-home-screen}

![process-reporting-home-screen](assets/process-reporting-home-screen.png)

**Process Reportingツリー・ビュー：** ホーム画面の左側にあるツリー・ビューには、プロセス・レポート・モジュールの項目が含まれます。

ツリービューは、次の最上位項目で構成されます。

**レポート：** この項目には、Process Reportingに付属する標準のレポートが含まれています。

事前定義済みレポートについて詳しくは、[プロセスレポートの事前定義済みレポート](/help/forms/using/process-reporting/pre-defined-reports-in-process-reporting.md)を参照してください。

**アドホッククエリ：** この項目には、プロセスとタスクをフィルターベースで検索するオプションが含まれます。

アドホッククエリについて詳しくは、「プロセスレポートのアドホッククエリ](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md)」を参照してください。[

**カスタム：** 「カスタム」ノードは、作成したカスタムレポートを表示します。

カスタムレポートの作成と表示の手順については、[プロセスレポートのカスタムレポート](/help/forms/using/process-reporting/process-reporting-custom-reports.md)を参照してください。

**プロセスレポートのタイトルバー：** プロセスレポートのタイトルバーには、ユーザーインターフェイスで作業する際に使用できる一般的なオプションがいくつか含まれています。

**プロセスレポートのタイトル：** プロセスレポートのタイトルは、タイトルバーの左隅に表示されます。

タイトルをクリックすれば、いつでもホーム画面に戻ることができます。

**最終更新時間：** プロセスデータは、AEM FormsデータベースからProcess Reportingリポジトリにスケジュールに従って公開されます。

最終更新時刻は、データの更新がProcess Reportingリポジトリにプッシュされた最後の日時を表示します。

データ発行サービスの詳細とこのサービスのスケジュール方法については、「プロセスレポートの概要」の「[プロセスデータの発行をスケジュール](/help/forms/using/process-reporting/install-start-process-reporting.md#p-schedule-process-data-publishing-p)」を参照してください。

**Process Reportingユーザー：** ログインしたユーザー名が最終更新時刻の右側に表示されます。

**プロセスレポートのタイトルバードロップダウンリスト：** プロセスレポートのタイトルバーの右隅にあるドロップダウンリストには、次のオプションが含まれます。

* **[!UICONTROL 同期]**:埋め込みProcess ReportingリポジトリをAEM Formsデータベースと同期します。
* **[!UICONTROL ヘルプ]**:プロセスレポートに関するヘルプドキュメントを表示します。
* **[!UICONTROL ログアウト]**:プロセスレポートからのログアウト
