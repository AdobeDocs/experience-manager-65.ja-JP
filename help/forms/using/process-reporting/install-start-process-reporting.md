---
title: プロセスレポートの概要
seo-title: Getting Started with Process Reporting
description: ' AEM Forms on JEE のプロセスレポートを使用するために必要な手順'
seo-description: The steps you need to follow to get started with AEM Forms on JEE Process Reporting
uuid: 685cad39-da2c-411d-a0b0-201917438bcf
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
discoiquuid: 7c1fcde0-b983-4b24-bc19-fcee1d4f096b
docset: aem65
exl-id: 1272e854-fa64-4bfd-b073-8fbcf210e9b5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '1710'
ht-degree: 100%

---

# プロセスレポートの概要{#getting-started-with-process-reporting}

プロセスレポートを使用すると、AEM Forms のユーザーは、AEM Forms 実装で現在定義されている AEM Forms プロセスに関する情報を照会できます。ただし、プロセスレポートは、AEM Forms のリポジトリのデータに直接アクセスしません。まず、スケジュールに従ってプロセスレポートのリポジトリにデータが公開されます（*ProcessDataPublisher サービスおよび ProcessDataStorage サービスによって*&#x200B;行われます）。次に、リポジトリに公開されたプロセスレポートのデータから、プロセスレポートのレポートとクエリが生成されます。プロセスレポートは、Forms Workflow モジュールの一部としてインストールされています。

この記事では、プロセスレポートのリポジトリへの AEM Forms データの公開を有効にする手順を説明します。その後、プロセスレポートを使用して、レポートとクエリを実行できるようになります。この記事では、プロセスレポートサービスの設定に使用できるオプションについても説明します。

## プロセスレポートの前提条件 {#process-reporting-pre-requisites}

### 不要なプロセスのパージ {#purge-non-essential-processes}

現在 Forms Workflow を使用している場合、AEM Forms データベースには大量のデータが含まれている可能性があります。

プロセスレポート公開サービスは、データベースで現在使用可能なすべての AEM Forms データを公開します。つまり、レポートやクエリを実行する必要がないレガシーデータがデータベースに含まれている場合、そのデータはレポートする必要がないにもかかわらず、すべてリポジトリに公開されます。そのようなデータは、プロセスレポートリポジトリにデータを公開するサービスを実行する前に、パージすることをお勧めします。これにより、公開サービスと、レポートデータのクエリサービスの両方のパフォーマンスが向上します。

AEM Forms プロセスデータのパージについて詳しくは、[プロセスデータのパージ](https://help.adobe.com/ja_JP/livecycle/11.0/AdminHelp/WS92d06802c76abadb-5145d5d12905ce07e7-7cb2.2.html)を参照してください。

>[!NOTE]
>
>パージユーティリティのヒントとテクニックについては、Adobe Developer Connection の「[プロセスとジョブのパージ](https://www.adobe.com/content/dam/Adobe/en/devnet/livecycle/pdfs/purging_processes_jobs.pdf)」に関する記事を参照してください。

## プロセスレポートサービスの設定 {#configuring-process-reporting-services}

### プロセスデータの公開をスケジュール {#schedule-process-data-publishing}

プロセスレポートサービスは、AEM Forms データベースから Process Reporting リポジトリに、スケジュールに従ってデータを公開します。

この操作はリソースを大量に消費する可能性があり、AEM Forms サーバーのパフォーマンスに影響を与える可能性があります。AEM Forms サーバーが混んでいない時間帯でスケジュールすることをお勧めします。

デフォルトでは、データの公開は毎日午前 2 時に実行されるようにスケジュールされています。

デフォルトのスケジュールを変更するには、次の手順を実行します。

>[!NOTE]
>
>クラスターで AEM Forms を実装して実行している場合は、クラスターの各ノードで次の手順を実行します。

1. AEM Forms サーバーインスタンスを停止します。
1. &#x200B;

   * （Windows の場合）`[JBoss root]/bin/run.conf.bat` ファイルをエディターで開きます。
   * （Linux、AIX、Solaris の場合）`[JBoss root]/bin/run.conf.sh` ファイルをエディターで開きます。

1. JVM 引数 `-Dreporting.publisher.cron = <expression>.` を追加します。

   例：次の Cron 式を使用すると、プロセスレポートは 5 時間ごとに AEM Forms データをプロセスレポートリポジトリに公開します。

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. `run.conf.bat` ファイルを保存して閉じます。

1. AEM Forms サーバーインスタンスを再起動します。

1. AEM Forms サーバーインスタンスを停止します。
1. WebSphere 管理コンソールにログインします。ナビゲーションツリーで&#x200B;**サーバー**／**アプリケーションサーバー**&#x200B;をクリックし、右側のウィンドウでサーバー名をクリックします。

1. サーバーインフラストラクチャーで&#x200B;**Java およびプロセス管理**／**プロセス定義**&#x200B;をクリックします。

1. 「その他のプロパティ」で「**Java 仮想マシン**」をクリックします。

   「汎用 JVM 引数」ボックスで引数 `-Dreporting.publisher.cron = <expression>.` を追加します。

   **例**：次の Cron 式を使用すると、プロセスレポートは 5 時間ごとに AEM Forms データをプロセスレポートリポジトリに公開します。

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. 「**適用**」をクリックし、次に「**マスター設定に直接保存**」をクリックします。
1. AEM Forms サーバーインスタンスを再起動します。
1. AEM Forms サーバーインスタンスを停止します。
1. WebLogic 管理コンソールにログインします。WebLogic 管理コンソールのデフォルトのアドレスは、`https://[hostname]:[port]/console` です。
1. Change Center で、「**Lock &amp; Edit**」をクリックします。
1. 「Domain Structure」で、**Environment**／**Servers** をクリックし、右側のウィンドウで、管理対象サーバー名をクリックします。
1. 次の画面で、「**設定**&#x200B;タブ」、「**サーバー起動**」タブをクリックします。
1. 「引数」ボックスに、JVM 引数 `-Dreporting.publisher.cron = <expression>` を追加します。

   **例**：次の Cron 式を使用すると、プロセスレポートは 5 時間ごとに AEM Forms データをプロセスレポートリポジトリに公開します。

   `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. 「**保存**」をクリックし、「**変更をアクティベート**」をクリックします。
1. AEM Forms サーバーインスタンスを再起動します。

![processdatapublisherservice](assets/processdatapublisherservice.png)

### ProcessDataStorage サービス {#processdatastorage-service}

ProcessDataStorageProvider サービスは、ProcessDataPublisher サービスからプロセスデータを受け取り、そのデータを Process Reporting リポジトリに保存します。

公開サイクルごとに、事前に定義されたルートフォルダーのサブフォルダーにデータが保存されます。

管理コンソールを使用すると、プロセスデータが格納される、ルート（**デフォルト**：`/content/reporting/pm`）の場所とサブフォルダー（**デフォルト**：`/yyyy/mm/dd/hh/mi/ss`）の階層形式を設定できます。

#### プロセスレポートリポジトリの場所の設定 {#to-configure-the-process-reporting-repository-locations}

1. 管理者の資格情報で&#x200B;**管理コンソール**&#x200B;にログインします。管理コンソールのデフォルト URL は `https://'[server]:[port]'/adminui`です。
1. **ホーム**／**サービス**／**アプリケーションとサービス**／**サービス管理**&#x200B;に移動して **ProcessDataStorageProvider** サービスを開きます。

   ![process-data-storage-service](assets/process-data-storage-service.png)

   **RootFolder**

   レポート用にプロセスデータが格納される CRX の場所。

   `Default`：`/content/reporting/pm`

   **フォルダー階層**

   プロセス作成時間に基づいて、プロセスデータが格納されるフォルダー階層。

   `Default`：`/yyyy/mm/dd/hh/mi/ss`

1. 「**保存**」をクリックします。

### ReportConfiguration サービス {#reportconfiguration-service}

ReportConfiguration サービスは、プロセスレポートのクエリサービスを設定するために、プロセスレポートで使用されます。

#### ReportingConfiguration サービスを設定するには： {#to-configure-the-reportingconfiguration-service}

1. CRX 管理者の資格情報で&#x200B;**設定マネージャー**&#x200B;にログインします。設定マネージャーのデフォルトの URL は `https://'[server]:[port]'/lc/system/console/configMgr` です。
1. **ReportingConfiguration** サービスを開きます。
1. **レコード数**

   リポジトリでクエリを実行すると、結果に大量のレコードが含まれる可能性があります。結果セットが大きい場合、クエリの実行によってサーバーリソースが消費される可能性があります。

   大きな結果セットを処理するために、ReportConfiguration サービスはクエリ処理を複数のレコードに分割します。これにより、システムの負荷が軽減されます。

   `Default`：`1000`

   **CRX ストレージパス**

   レポート用にプロセスデータを格納する CRX の場所。

   `Default`：`/content/reporting/pm`

   >[!NOTE]
   >
   >これは、「ProcessDataStorage 構成」オプションで&#x200B;**ルートフォルダー**&#x200B;に指定した場所と同じです。
   >
   >
   >ProcessDataStorage 設定の「ルートフォルダー」オプションを更新する場合は、ReportConfiguration サービスの CRX ストレージパスの場所を更新する必要があります。

1. 「**保存**」をクリックして **CQ 設定マネージャー**&#x200B;を閉じます。

### ProcessDataPublisher サービス {#processdatapublisher-service}

ProcessDataPublisher サービスは、AEM Forms データベースからプロセスデータをインポートし、格納のためにそのデータを ProcessDataStorageProvider サービスにパブリッシュします。

#### ProcessDataPublisher サービスの設定 {#to-configure-processdatapublisher-service-nbsp}

1. 管理者の資格情報で&#x200B;**管理コンソール**&#x200B;にログインします。

   デフォルトの URL は `https://'server':port]/adminui/` です。

1. **ホーム**／**サービス**／**アプリケーションとサービス**／**サービス管理**&#x200B;に移動して **ProcessDataPublisher** サービスを開きます。

![processdatapublisherservice-1](assets/processdatapublisherservice-1.png)

**データを公開**

プロセスデータの公開を開始するには、このオプションを有効にします。デフォルトでは、このオプションは無効になっています。

プロセスレポートコンポーネントに関連するすべての構成が適切に設定されている場合にのみ、プロセスレポートを有効にします。

または、不要になったプロセスデータの公開を無効にするために、このオプションを使用します。

`Default`：`Off`

**バッチ間隔（秒）**

ProcessDataPublisher サービスが実行されるたびに、このサービスはまず、最後のサービス実行からの時間をバッチ間隔で分割します。次にこのサービスは、AEM Forms データの各間隔を個別に処理します。

これは、サイクル内の各実行（バッチ）中に、パブリッシャーがエンドツーエンドで処理するデータのサイズを制御するのに役立ちます。

例えばパブリッシャーを毎日実行する場合、1 回の実行で 1 日分のデータをすべて処理する代わりに、デフォルトで、それぞれ 1 時間の 24 個のバッチに分割して処理します。

`Default`：`3600`

`Unit`：`Seconds`

**ロックタイムアウト（秒）**

パブリッシャーサービスは、データの処理を開始する際にロックを取得するので、パブリッシャーの複数のインスタンスが実行を開始したり、データを同時に処理したりすることはありません。

ロックを取得したパブリッシャーサービスが、ロックタイムアウト値で定義された秒数の間アイドル状態になった場合は、そのロックが解除され、他のパブリッシャーサービスインスタンスが処理を続行できるようになります。

`Default`：`3600`

`Unit`：`Seconds`

**次の時間からデータを公開**

AEM Forms 環境には、環境が設定された時点からのデータが含まれています。

デフォルトでは、ProcessDataPublisher サービスは AEM Forms データベースからすべてのデータを読み込みます。

レポートのニーズに応じて、特定の日時の後にデータに対してレポートやクエリを実行する予定がある場合は、日時を指定することをお勧めします。その後、パブリッシングサービスは、その日時以降に日付を公開します。

`Default`：`01-01-1970 00:00:00`

`Format`：`dd-MM-yyyy HH:mm:ss`

## プロセスレポートユーザーインターフェイスへのアクセス {#accessing-the-process-reporting-user-interface}

プロセスレポートのユーザーインターフェイスは、ブラウザーベースです。

プロセスレポートを設定したら、AEM Forms のインストール先の次の場所で、プロセスレポートの使用を開始できます。

`https://<server>:<port>/lc/pr`

### プロセスレポートへのログイン {#log-in-to-process-reporting}

プロセスレポートの URL（https://&lt;server>:&lt;port>/lc/pr）に移動すると、ログイン画面が表示されます。

プロセスレポートモジュールにログインするための認証情報を指定します。

>[!NOTE]
>
>プロセスレポートユーザーインターフェイスにログインするには、次の AEM Forms 権限が必要です。
>
>`PERM_PROCESS_REPORTING_USER`

![プロセスレポートへのログイン](assets/capture1_new.png)

プロセスレポートにログインすると、**[!UICONTROL ホーム]**&#x200B;画面が表示されます。

### プロセスレポートのホーム画面 {#process-reporting-home-screen}

![process-reporting-home-screen](assets/process-reporting-home-screen.png)

**プロセスレポートのツリー表示：**&#x200B;ホーム画面の左側にあるツリー表示には、プロセスレポートモジュールの項目が表示されます。

ツリー表示は、次の最上位項目で構成されます。

**レポート：**&#x200B;この項目には、プロセスレポートに付属する、そのままで使用できるレポートが含まれています。

事前定義済みレポートについて詳しくは、[プロセスレポートの事前定義済みレポート](/help/forms/using/process-reporting/pre-defined-reports-in-process-reporting.md)を参照してください。

**アドホッククエリ：**&#x200B;この項目には、プロセスとタスクをフィルターベースで検索するオプションが含まれています。

アドホッククエリについて詳しくは、[プロセスレポートのアドホッククエリ](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md)を参照してください。

**カスタム：**&#x200B;カスタムノードには、作成したカスタムレポートが表示されます。

カスタムレポートの作成と表示の手順については、[プロセスレポートのカスタムレポート](/help/forms/using/process-reporting/process-reporting-custom-reports.md)を参照してください。

**プロセスレポートのタイトルバー：**&#x200B;プロセスレポートのタイトルバーには、ユーザーインターフェイスで作業する際に使用できる一般的なオプションがいくつか含まれています。

**プロセスレポートのタイトル：**&#x200B;プロセスレポートのタイトルは、タイトルバーの左隅に表示されます。

タイトルをクリックすれば、いつでもホーム画面に戻ることができます。

**最終更新時間：**&#x200B;プロセスデータは、AEM Forms データベースからプロセスレポートリポジトリに、スケジュールに従って公開されます。

最終更新時間には、データの更新がプロセスレポートリポジトリにプッシュされた最終日時が表示されます。

データ公開サービスおよびこのサービスのスケジュール方法について詳しくは、「プロセスレポートの概要」の[プロセスデータの公開をスケジュール](/help/forms/using/process-reporting/install-start-process-reporting.md#p-schedule-process-data-publishing-p)を参照してください。

**プロセスレポートのユーザー：**&#x200B;ログインしたユーザーの名前が、最終更新時間の右側に表示されます。

**プロセスレポートのタイトルバーのドロップダウンリスト：**&#x200B;プロセスレポートのタイトルバーの右隅にあるドロップダウンリストには、次のオプションが含まれます。

* **[!UICONTROL 同期]**：埋め込まれたプロセスレポートリポジトリを AEM Forms データベースと同期します。
* **[!UICONTROL ヘルプ]**：プロセスレポートに関するヘルプドキュメントを表示します。
* **[!UICONTROL ログアウト]**：プロセスレポートからログアウトします
