---
title: Process Reportingの概要
seo-title: Process Reportingの概要
description: JEE上のAEM Forms Process Reportingの使用を開始する際に必要な手順
seo-description: JEE上のAEM Forms Process Reportingの使用を開始する際に必要な手順
uuid: 685cad39-da2c-411d-a0b0-201917438bcf
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
discoiquuid: 7c1fcde0-b983-4b24-bc19-fcee1d4f096b
docset: aem65
translation-type: tm+mt
source-git-commit: 8f90dc4865126d52e04effc9197ef7145b1a167e

---


# Getting Started with Process Reporting{#getting-started-with-process-reporting}

プロセスレポートを使用すると、AEM Formsユーザーは、AEM Forms実装で現在定義されているAEM Formsプロセスに関する情報を照会できます。 ただし、Process ReportingはAEM Formsリポジトリから直接データにアクセスすることはありません。 データは、最初に（ProcessDataPublisherおよびProcessDataStorageサービスによって）スケジュールに基づ&#x200B;*いてProcess Reportingリポジトリに発*&#x200B;行されます。 次に、プロセスレポート内のレポートとクエリーは、リポジトリに発行されたプロセスレポートデータから生成されます。 プロセスレポートは、Formsワークフローモジュールの一部としてインストールされます。

この記事では、AEM FormsデータをProcess Reportingリポジトリに発行する手順について詳しく説明します。 その後、プロセスレポートを使用してレポートやクエリーを実行できます。 この記事では、Process Reportingサービスを設定するために使用できるオプションについても説明します。

## プロセスレポートの前提条件 {#process-reporting-pre-requisites}

### 不要なプロセスの削除 {#purge-non-essential-processes}

現在Forms Workflowを使用している場合、AEM Formsデータベースに大量のデータが含まれている可能性があります

Process Reporting発行サービスは、データベースで現在使用可能なすべてのAEM Formsデータを発行します。 つまり、レポートやクエリを実行したくないレガシーデータがデータベースに含まれている場合、レポートに必要ないデータでも、そのすべてのデータがリポジトリに発行されます。 サービスを実行してProcess Reportingリポジトリにデータを発行する前に、このデータを削除することをお勧めします。 これにより、Publisherサービスと、レポート用にデータをクエリするサービスの両方のパフォーマンスが向上します。

AEM Formsプロセスデータの削除について詳しくは、「プロセスデータの削 [除」を参照してください](https://help.adobe.com/en_US/livecycle/11.0/AdminHelp/WS92d06802c76abadb-5145d5d12905ce07e7-7cb2.2.html)。

>[!NOTE]
>
>パージユーティリティのヒントとテクニックについては、プロセスとジョブの削除に関するAdobe Developer Connectionの記 [事を参照してください](https://www.adobe.com/content/dam/Adobe/en/devnet/livecycle/pdfs/purging_processes_jobs.pdf)。

## Process Reportingサービスの設定 {#configuring-process-reporting-services}

### プロセスデータの公開のスケジュール {#schedule-process-data-publishing}

Process Reportingサービスは、AEM FormsデータベースからProcess Reportingリポジトリにデータをスケジュールに基づいて発行します。

この操作はリソースを大量に消費し、AEM Formsサーバーのパフォーマンスに影響を与える可能性があります。 AEM Formsサーバーのビジータイムスロットの外部でこのスケジュールを設定することをお勧めします。

デフォルトでは、データの公開は毎日午前2時に実行されるようにスケジュールされています。

発行スケジュールを変更するには、次の手順を実行します。

>[!NOTE]
>
>AEM Forms実装をクラスター上で実行する場合は、クラスターの各ノードで次の手順を実行します。

1. AEM formsサーバーインスタンスを停止します。
1.

    * （Windowsの場合）ファイルをエデ `[JBoss root]/bin/run.conf.bat` ィターで開きます。
    * （Linux、AIXおよびSolarisの場合）エディタ `[JBoss root]/bin/run.conf.sh` ー内のファイル。

1. JVM引数の追加 `-Dreporting.publisher.cron = <expression>.`

   例：次のCron形式を使用すると、Process Reportingは5時間ごとにAEM FormsデータをProcess Reportingリポジトリに発行します。

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. Save and close the `run.conf.bat` file.

1. AEM formsサーバーインスタンスを再起動します。

1. AEM formsサーバーインスタンスを停止します。
1. Log in to the WebSphere Administrative Console. In the navigation tree, click **Servers** > **Application servers** and then, in the right pane, click the server name.

1. Under Server Infrastructure, click **Java and Process Management** > **Process Definition**.

1. 「Additional Properties」で、「**Java Virtual Machine**」をクリックします。

   In the Generic JVM arguments box, add the argument `-Dreporting.publisher.cron = <expression>.`

   **例**:次のCron形式を使用すると、Process Reportingは5時間ごとにAEM FormsデータをProcess Reportingリポジトリに発行します。

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. Click **Apply**, click OK, and then click **Save directly to the master configuration**.
1. AEM formsサーバーインスタンスを再起動します。
1. AEM formsサーバーインスタンスを停止します。
1. WebLogic管理コンソールにログインします。 WebLogic管理コンソールのデフォルトアドレスはです `https://[hostname]:[port]/console`。
1. Change Center で、「**Lock &amp; Edit**」をクリックします。
1. 「Domain Structure」で、**Environment**／**Servers** をクリックし、右側のウィンドウで、管理対象サーバー名をクリックします。
1. 次の画面で、「**Configuration**」タブ／「**Server Start**」タブをクリックします。
1. 「Arguments」ボックスにJVM引数を追加します `-Dreporting.publisher.cron = <expression>`。

   **例**:次のCron形式を使用すると、Process Reportingは5時間ごとにAEM FormsデータをProcess Reportingリポジトリに発行します。

   `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. 「**Save**」をクリックし、「**Activate Changes**」をクリックします。
1. AEM formsサーバーインスタンスを再起動します。

![processdatapublisherservice](assets/processdatapublisherservice.png)

### ProcessDataStorageサービス {#processdatastorage-service}

ProcessDataStorageProviderサービスは、ProcessDataPublisherサービスからプロセスデータを受け取り、データをProcess Reportingリポジトリに保存します。

公開サイクルごとに、データは事前定義されたルートフォルダーのサブフォルダーに保存されます。

管理コンソールを使用して、ルート(デフォルト&#x200B;****: `/content/reporting/pm`)場所とサブフォルダー(デ&#x200B;**フォルト**: `/yyyy/mm/dd/hh/mi/ss`)プロセスデータが保存される階層形式。

#### Process Reportingリポジトリの場所を設定するには {#to-configure-the-process-reporting-repository-locations}

1. 管理者の資格情報を使 **用して** 、管理コンソールにログインします。 The default URL of Administration Console is `https://[server]:[port]/adminui`
1. ホーム/サービス **/アプリケーシ** ョン **・サービス/サービス** /サービス管理データ・スト ************ レージ・プロバイダ・サービスに移動します。

   ![process-data-storage-service](assets/process-data-storage-service.png)

   **RootFolder**

   レポート用にプロセスデータが保存されるCRXの場所。

   `Default`: `/content/reporting/pm`

   **フォルダ階層**

   プロセス作成時間に基づいて、プロセスデータが格納されるフォルダー階層。

   `Default`: `/yyyy/mm/dd/hh/mi/ss`

1. 「**保存**」をクリックします。

### ReportConfigurationサービス {#reportconfiguration-service}

ReportConfigurationサービスは、プロセスレポートクエリサービスを設定するためにプロセスレポートで使用されます。

#### To configure the ReportingConfiguration service {#to-configure-the-reportingconfiguration-service}

1. CRX管理者資格情報を使 **用して** Configuration Managerにログインします。 Configuration ManagerのデフォルトのURLは `https://[server]:[port]/lc/system/console/configMgr`
1. ReportingConfigurationサービスを **開きます** 。
1. **レコード数**

   リポジトリでクエリーを実行すると、結果に大量のレコードが含まれる可能性があります。 結果セットが大きい場合、クエリの実行でサーバーリソースを消費する可能性があります。

   大きな結果セットを処理するために、ReportConfigurationサービスはクエリ処理をレコードのバッチに分割します。 これにより、システムの負荷が軽減されます。

   `Default`: `1000`

   **CRXストレージパス**

   レポート用にプロセスデータを保存するCRXの場所。

   `Default`: `/content/reporting/pm`

   >[!NOTE]
   >
   >これは、ProcessDataStorage設定オプションの **Root folderで指定した場所と同じです**。
   >
   >
   >ProcessDataStorage設定で「Root Folder」オプションを更新する場合は、ReportConfigurationサービスでCRX Storage pathの場所を更新する必要があります。

1. 「 **Save** 」をクリックし **、CQ Configuration Managerを閉じます**。

### ProcessDataPublisherサービス {#processdatapublisher-service}

ProcessDataPublisherサービスは、AEM Formsデータベースからプロセスデータをインポートし、データをProcessDataStorageProviderサービスに発行して保存します。

#### ProcessDataPublisherサービスを設定するには {#to-configure-processdatapublisher-service-nbsp}

1. 管理者の資格情報を使 **用して** 、管理コンソールにログインします。

   The default URL is `https://[server]:port]/adminui/`.

1. ホーム/サービス **/アプリケーション** ・サービス **/アプリケーションおよびサービス** /サービス管理データ・パブリッ ************ シャ・データ・パブリッシャ・サービスに移動します。

![processdatapublisherservice-1](assets/processdatapublisherservice-1.png)

**データの発行**

プロセスデータの発行を開始するには、このオプションを有効にします。 デフォルトでは、このオプションは無効になっています。

プロセスレポートコンポーネントに関連するすべての設定が適切に設定されている場合にのみ、プロセスレポートを有効にします。

または、不要になったプロセスデータの公開を無効にする場合は、このオプションを使用します。

`Default`: `Off`

**バッチ間隔（秒）**

ProcessDataPublisherサービスが実行されるたびに、サービスは、最後に実行されたサービスからの時間をBatch Intervalで最初に分割します。 次に、AEM Formsデータの各間隔を別々に処理します。

これは、サイクル内の各実行（バッチ）の間に、パブリッシャーが処理するデータのサイズを制御するのに役立ちます。

例えば、発行者が毎日実行し、1回の実行で1日分のデータ全体を処理する代わりに、デフォルトでは、各1時間につき24のバッチに処理を分割します。

`Default`: `3600`

`Unit`: `Seconds`

**ロックタイムアウト（秒）**

パブリッシャーサービスは、データの処理を開始する際にロックを取得するので、パブリッシャーの複数のインスタンスが実行を開始して同時にデータを処理する必要がありません。

ロックを取得したパブリッシャーサービスが、Lock Timeout値で定義された秒数アイドル状態の場合、そのロックが解放され、他のパブリッシャーサービスインスタンスの処理を継続できます。

`Default`: `3600`

`Unit`: `Seconds`

**データの発行元**

AEM Forms環境には、環境が設定された時点からのデータが含まれます。

デフォルトでは、ProcessDataPublisherサービスはAEM Formsデータベースからすべてのデータをインポートします。

レポートのニーズに応じて、特定の日時以降にレポートやクエリを実行する場合は、日時を指定することをお勧めします。 その後、発行サービスはその日付以降に発行されます。

`Default`: `01-01-1970 00:00:00`

`Format`: `dd-MM-yyyy HH:mm:ss`

## Process Reportingユーザーインターフェイスへのアクセス {#accessing-the-process-reporting-user-interface}

プロセスレポートのユーザーインターフェイスはブラウザーベースです。

プロセスレポートを設定した後、AEM Formsのインストール先の次の場所で、プロセスレポートの操作を開始できます。

`https://<server>:<port>/lc/pr`

### Process Reportingへのログイン {#log-in-to-process-reporting}

プロセスレポートURL(https://&lt;server>:&lt;port>/lc/pr)に移動すると、ログイン画面が表示されます。

資格情報を指定して、プロセスレポートモジュールにログインします。

>[!NOTE]
>
>Process Reportingユーザーインターフェイスにログインするには、次のAEM Forms権限が必要です。
>
>`PERM_PROCESS_REPORTING_USER`

![Process Reportingにログイン](assets/capture1_new.png)

Process Reportingにログインすると、ホーム画面が **[!UICONTROL 表示されます]** 。

### プロセスレポートのホーム画面 {#process-reporting-home-screen}

![process-reporting-home-screen](assets/process-reporting-home-screen.png)

**** Process Reportingのツリービュー：ホーム画面の左側のツリービューには、プロセスレポートモジュールの項目が含まれています。

ツリービューは、次の最上位レベルの項目で構成されます。

**** レポート：この項目には、プロセスレポートに付属の既製のレポートが含まれています。

事前定義済みのレポートについて詳しくは、「プロセスレポ [ートでの事前定義済みのレポート](/help/forms/using/process-reporting/pre-defined-reports-in-process-reporting.md)」を参照してください。

**** アドホッククエリ：この項目には、プロセスとタスクに対してフィルターベースの検索を実行するためのオプションが含まれています。

アドホッククエリーについて詳しくは、「プロセスレポ [ートのアドホッククエリー」を参照してください](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md)。

**** カスタム：「カスタム」ノードには、作成したカスタムレポートが表示されます。

カスタムレポートを作成して表示する手順については、「プロセスレポートでのカ [スタムレポート」を参照してください](/help/forms/using/process-reporting/process-reporting-custom-reports.md)。

**** Process Reportingのタイトルバー：プロセスレポートのタイトルバーには、ユーザーインターフェイスで作業する際に使用できる一般的なオプションが含まれています。

**** Process Reportingタイトル：プロセスレポートのタイトルは、タイトルバーの左隅に表示されます。

タイトルをクリックすると、ホーム画面に戻ります。

**** 最終更新時刻：プロセスデータは、スケジュールに基づいてAEM FormsデータベースからProcess Reportingリポジトリに発行されます。

「Last Update Time」は、データ更新がProcess Reportingリポジトリにプッシュされた最後の日時を表示します。

データ公開サービスとこのサービスのスケジュール方法について詳しくは、「プロセスレポートの概要」の [「プロセスデータの公開のスケジュール](/help/forms/using/process-reporting/install-start-process-reporting.md#p-schedule-process-data-publishing-p) 」を参照してください。

**** Process Reportingユーザー：ログインしたユーザー名は、最終更新時刻の右側に表示されます。

**** プロセスレポートのタイトルバードロップダウンリスト：「プロセスレポート」タイトルバーの右隅にあるドロップダウンリストには、次のオプションが含まれています。

* **[!UICONTROL 同期]**:埋め込まれたProcess ReportingリポジトリをAEM Formsデータベースと同期します。
* **[!UICONTROL ヘルプ]**:プロセスレポートのヘルプドキュメントを表示します。
* **[!UICONTROL ログアウト]**:プロセスレポートからのログアウト

[サポートへのお問い合わせ](https://www.adobe.com/account/sign-in.supportportal.html)
