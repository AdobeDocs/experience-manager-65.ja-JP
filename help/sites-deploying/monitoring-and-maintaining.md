---
title: Adobe Experience Managerインスタンスの監視と保守
description: AEMの監視方法の詳細
uuid: 14466552-5c92-4730-a427-85675a2b121c
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 5d2364b7-4497-4f8b-85ef-6e780bfb8c36
docset: aem65
feature: Configuring
exl-id: d3375935-090d-4052-8234-68ef4ddbab6a
source-git-commit: bb27c7dfedd5a16728674f7584b0c462a92646e6
workflow-type: tm+mt
source-wordcount: '5934'
ht-degree: 37%

---

# Adobe Experience Managerインスタンスの監視と保守{#monitoring-and-maintaining-your-aem-instance}

AEMインスタンスをデプロイした後は、その操作、パフォーマンス、整合性を監視および維持する必要があります。

ここでの主な要因は、潜在的な問題を認識するために、システムの外観と動作を通常の状態で把握する必要がある点です。 この機能は、システムを監視し、時間の経過と共に情報を収集することで最適です。

| チェック項目 | 検討事項 | コメント/アクション |
|---|---|---|
| バックアップ計画。 |  | 所要時間 [インスタンスのバックアップ](/help/sites-deploying/monitoring-and-maintaining.md#backups). |
| 災害復旧プラン | お客様の企業の災害復旧ガイドライン |  |
| 問題を報告するためのエラー追跡システムが利用可能であること | 例： [バグジラ](https://www.bugzilla.org/), [ジラ](https://www.atlassian.com/software/jira)または他の多数の |  |
| ファイル・システムが監視されている。 | 十分な空きディスク容量がない場合、CRX リポジトリは「フリーズ」します。 スペースが利用可能になった後に再開されます。 | 空き容量が少なくなると、「`*ERROR* LowDiskSpaceBlocker`」メッセージがログファイルに表示されます。 |
| [ログファイル](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files)が監視されていること |  |  |
| システム監視は（常に）バックグラウンドで実行されています。 | CPU、メモリ、ディスク、ネットワーク使用量を含みます。 例えば、iostat / vmstat / perfmon を使用します。 | ログに記録されたデータは視覚化され、パフォーマンスの問題の追跡に使用できます。 生データにもアクセスできます。 |
| [AEMのパフォーマンスが監視されています](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance). | 次を含む [要求カウンター](/help/sites-deploying/monitoring-and-maintaining.md#request-counters) トラフィックレベルを監視する。 | パフォーマンスが大幅に低下した、または長期的に低下した場合は、詳細な調査を行う必要があります。 |
| [レプリケーションエージェント](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-your-replication-agents)を監視していること。 |  |  |
| ワークフローインスタンスを定期的にパージします。 | リポジトリのサイズとワークフローのパフォーマンス。 | 詳しくは、 [ワークフローインスタンスの定期的なパージ](/help/sites-administering/workflows-administering.md#regular-purging-of-workflow-instances). |

## バックアップ {#backups}

次のバックアップを実行することをお勧めします。

* ソフトウェアのインストール — 構成の大幅な変更の前後
* リポジトリ内に保持されるコンテンツ — 定期的

お客様の会社では、バックアップポリシーに従っている可能性が高く、バックアップの対象と時期に関するその他の考慮事項として、次の事項が挙げられます。

* システムとデータの重要性。
* ソフトウェアまたはデータの変更頻度。
* データ量バックアップを実行する時間と同様に、容量が問題になる場合があります。
* ユーザーがオンライン中にバックアップを実施できるかどうか。可能な場合は、パフォーマンスへの影響。
* ユーザの地理的分布つまり、（影響を最小限に抑えるために）バックアップするのに最適なタイミングはいつですか？
* 災害復旧ポリシーバックアップ・データの格納先に関するガイドライン（オフサイトや特定のメディアなど）があります。

多くの場合、フル・バックアップは、1 日、1 週間、1 月など、一定の間隔で実行され、差分バックアップはその間（1 時間、1 日、1 週間など）に実行されます。

>[!CAUTION]
>
>実稼動インスタンスのバックアップを実装する場合、テストは *必須* バックアップを正常に復元できるように作成します。
>
>このテストを行わないと、バックアップが無駄になる可能性があります（最悪の場合）。

>[!NOTE]
>
>バックアップのパフォーマンスの詳細については、 [パフォーマンスのバックアップ](/help/sites-deploying/configuring-performance.md#backup-performance) 」セクションに入力します。

### ソフトウェアインストールのバックアップ {#backing-up-your-software-installation}

インストール後、または設定を大幅に変更した後、ソフトウェアインストールのバックアップを作成します。

このタスクを実行するには、次の手順に従います。 [リポジトリ全体のバックアップ](#backing-up-your-repository) そして次に、

1. AEMを停止します。
1. ファイルシステムから `<cq-installation-dir>` 全体をバックアップします。

>[!CAUTION]
>
>サードパーティのアプリケーションサーバーを運用している場合は、別の場所に追加のフォルダーが存在する場合があり、バックアップする必要もあります。 アプリケーションサーバーのインストールについて詳しくは、[アプリケーションサーバーと共に AEM をインストールする方法](/help/sites-deploying/application-server-install.md)を参照してください。

>[!CAUTION]
>
>ファイルデータストアの増分バックアップがサポートされています。他のコンポーネント（Lucene インデックスなど）に対して増分バックアップを使用する場合は、削除されたファイルもバックアップで削除済みとしてマークされるようにします。

>[!NOTE]
>
>ディスク・ミラーリングは、バックアップ・メカニズムとしても使用できます。

### リポジトリのバックアップ {#backing-up-your-repository}

この [バックアップと復元](/help/sites-administering/backup-and-restore.md) CRX リポジトリのバックアップに関するすべての問題については、CRX ドキュメントの節で説明しています。

オンラインでの「ホット」バックアップの作成の詳細については、 [オンラインバックアップの作成](/help/sites-administering/backup-and-restore.md#online-backup).

## バージョンのパージ {#version-purging}

この **バージョンをパージ** このツールは、リポジトリ内のノードまたはノードの階層のバージョンをパージすることを目的としています。 その主な目的は、古いバージョンのノードを削除して、リポジトリのサイズを小さくすることです。

この節では、AEMのバージョン管理機能に関連するメンテナンス操作について説明します。 この **バージョンをパージ** このツールは、リポジトリ内のノードまたはノードの階層のバージョンをパージすることを目的としています。 その主な目的は、古いバージョンのノードを削除して、リポジトリのサイズを小さくすることです。

### 概要 {#overview}

**バージョンのパージ**&#x200B;ツールは、週次メンテナンスタスクとして使用できます。 を初めて使用する前に、セグメントを追加して設定する必要があります。 その後はリクエストに応じて、または週間ベースで実行することができます。

### Web サイトのバージョンのパージ {#purging-versions-of-a-web-site}

Web サイトのバージョンをパージするには、次の手順を実行します。

1. **[ツール](/help/sites-administering/tools-consoles.md)** **コンソール**&#x200B;に移動し、**操作**／**メンテナンス**／**週別メンテナンスウィンドウ**&#x200B;を選択します。

1. 上部ツールバーの「**+追加**」を選択します。

   ![バージョンのパージを追加](assets/version-purge-add.png)

1. 選択 **バージョンのパージ** 」を選択します。 **新規タスクの追加** ダイアログ。 次に「**保存**」します。

   ![バージョンのパージを追加](assets/version-purge-add-new-task.png)

1. この **バージョンのパージ** タスクが追加されます。 カードアクションを使用して、以下を実行できます。
   * 選択 — 上部のツールバーに追加のアクションが表示されます
   * 実行 - 設定したパージを直ちに実行します。
   * 設定 - 週次パージタスクを設定します

   ![バージョンのパージアクション](assets/version-purge-actions.png)

1. **設定**&#x200B;アクションを選択し、**Day CQ WCM バージョンパージタスク**&#x200B;の web コンソールを開いて、以下を設定することができます。

   ![バージョンのパージ設定](assets/version-purge-configuration.png)

   * **パスをパージ**
パージするコンテンツの開始パスを設定します。例： 
`/content/wknd`。

      >[!CAUTION]
      >
      >Adobeでは、各 Web サイトに対して複数のパスを定義することをお勧めします。
      >
      >子が多すぎるパスを定義すると、パージを実行する時間が大幅に長くなる場合があります。

   * **バージョンを再帰的にパージ**

      * パスで定義したノードのみをパージする場合は、選択を解除します。
      * パスで定義したノードおよびその下位のノードをパージする場合に選択します。
   * **バージョンの最大数**
保持するバージョンの（各ノードの）最大数を設定します。 この設定を使用しない場合は、空のままにします。

   * **バージョンの最小数**
保持するバージョンの（各ノードの）最小数を設定します。 この設定を使用しない場合は、空のままにします。

   * **バージョンの最長有効期間**
保持するバージョンの（各ノードに対の）最長有効期間を日数で設定します。 この設定を使用しない場合は、空のままにします。
   次に、 **保存**&#x200B;します。

1. **週別メンテナンスウィンドウ**&#x200B;のウィンドウに移動または戻り、「**実行**」を選択して、プロセスをすぐに起動します。

>[!CAUTION]
>
>クラシック UI ダイアログを使用して、設定した[ドライラン](#analyzing-the-console)を実行することができます。
>
>* http://localhost:4502/etc/versioning/purge.html
>
>パージされたノードは、リポジトリを復元しないと元に戻すことができません。 パージの前に必ずドライランを実行して、設定を慎重に行ってください。

#### ドライラン - コンソールの分析 {#analyzing-the-console}

クラシック UI では、次からの&#x200B;**ドライラン**&#x200B;オプションが提供されます。

* http://localhost:4502/etc/versioning/purge.html

この処理では、処理されたすべてのノードがリストされます。 この処理の間、ノードには次のいずれかのステータスを設定できます。

* `ignore (not versionnable)`：ノードはバージョン管理をサポートしないので、処理中は無視されます。

* `ignore (no version)`：ノードにバージョンが含まれていないので、処理中は無視されます。

* `retained`：ノードはパージされません。
* `purged`：ノードはパージされます。

さらに、コンソールでは、バージョンに関して次のような有益な情報が提供されます。

* `V 1.0`：バージョン番号。
* `V 1.0.1`&#42;：星形は、バージョンが現在の（基本）バージョンであり、パージできないことを示しています。

* `Thu Mar 15 2012 08:37:32 GMT+0100`：バージョンの日付。

例を以下に示します。

* この **[!DNL Shirts]** バージョンの年齢が 2 日を超えているので、バージョンはパージされます。
* **[!DNL Tonga Fashions!]** のバージョンは、バージョンの数が 5 を超えているので、パージされます。

![global_version_screenshot](assets/global_version_screenshot.png)

## 監査レコードとログファイルの操作 {#working-with-audit-records-and-log-files}

Adobe Experience Manager(AEM) に関する監査レコードおよびログファイルは、様々な場所で見つけることができます。 次に、検索内容の概要と検索場所を示します。

### ログの使用 {#working-with-logs}

AEM WCM は詳細なログを記録します。 クイックスタートを解凍して起動した後、次の場所でログを検索できます。

* `<cq-installation-dir>/crx-quickstart/logs/`

* `<cq-installation-dir>/crx-quickstart/repository/`

#### ログファイルのローテーション {#log-file-rotation}

ログファイルのローテーションとは、ファイルを定期的に作成することでファイルの増加を制限するプロセスを指します。 AEMで、 `error.log` は、指定されたルールに従って、1 日に 1 回回転されます。

* `error.log` ファイルは、{original_filename} `.yyyy-MM-dd` というパターンに従って名前が変更されます。例えば、2010 年 7 月 11 日に、現在のログファイルの名前が変更されます `error.log-2010-07-10`、新しい `error.og` が作成されました。

* 以前のログファイルは削除されないので、古いログファイルを定期的にクリーンアップして、ディスクの使用量を制限する必要があります。

>[!NOTE]
>
>AEMのインストールをアップグレードすると、AEMで使用されなくなった既存のログファイルがディスクに残ります。 安全に削除できます。 すべての新しいログエントリは、新しいログファイルに書き込まれます。

### ログファイルの検索 {#finding-the-log-files}

AEMをインストールしたファイルサーバーには、次のような様々なログファイルが保持されます。

* `<cq-installation-dir>/crx-quickstart/logs`

   * `access.log`
AEM WCM およびリポジトリへのすべてのアクセス要求は、ここに登録されます。

   * `audit.log`
モデレートアクションはここに登録されます。

   * `error.log`
エラーメッセージ（様々な深刻度レベル）はここに登録されます。

   * [ `ImageServer-<PortId>-yyyy>-<mm>-<dd>.log`](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/config-admin/server-logging/c-image-server-log.html?lang=ja)
このログは、[!DNL Dynamic Media] が有効になっている場合にのみ使用されます。内部の ImageServer プロセスの動作を分析するための統計情報と分析情報を提供します。

   * `request.log`
各アクセス要求が、応答と共にここに登録されます。

   * [ `s7access-<yyyy>-<mm>-<dd>.log`](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/config-admin/server-logging/c-access-log.html?lang=ja)
このログは、[!DNL Dynamic Media] が有効になっている場合にのみ使用されます。s7access ログには、`/is/image` および `/is/content` 経由で [!DNL Dynamic Media] に対して実行された各リクエストが記録されます。

   * `stderr.log`
起動時に生成される様々な深刻度レベルのエラーメッセージを保持します。デフォルトでは、ログレベルの設定は次のようになっています。 
`Warning`（`WARN`）

   * `stdout.log`
起動時のイベントを示すログメッセージを保持します。

   * `upgrade.log`
すべてのアップグレード操作のログを提供します。アップグレード操作が実行されるのは、 
`com.day.compat.codeupgrade` および `com.adobe.cq.upgradesexecutor` の各パッケージです。

* `<cq-installation-dir>/crx-quickstart/repository/segmentstore`

   * `journal.log`
リビジョンジャーナル処理の情報。

>[!NOTE]
>
>ImageServer ログと s7access ログは、system/console/status-Bundlelist ページから生成される「すべてダウンロード」パッケージには含まれません。サポート目的で、 [!DNL Dynamic Media] 問題が発生した場合は、カスタマーサポートに問い合わせる際に ImageServer と s7access ログを追加します。

### デバッグログレベルのアクティベート {#activating-the-debug-log-level}

デフォルトのログレベル ([Apache Sling Logging Configuration](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingconfiguration)) は情報なので、デバッグメッセージはログに記録されません。

ロガーのデバッグログレベルをアクティブにするには、リポジトリでプロパティ `org.apache.sling.commons.log.level` をデバッグに設定します。例えば、`/libs/sling/config/org.apache.sling.commons.log.LogManager` で [global Apache Sling Logging](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingconfiguration) を設定します。

>[!CAUTION]
>
>デバッグログレベルのログを必要以上に長く残さないでください。これは、多数のログエントリが生成され、リソースを消費するからです。

デバッグファイルの行は、通常は DEBUG で始まり、ログレベル、インストーラーのアクション、ログメッセージを示します。 次に例を示します。

```shell
DEBUG 3 WebApp Panel: WebApp successfully deployed
```

ログレベルは次のとおりです。

| 0 | 致命的なエラー | アクションに失敗したので、インストーラーを続行できません。 |
|---|---|---|
| 1 | エラー | アクションが失敗しました。 インストールは続行しますが、AEM WCM の一部が正しくインストールされず、機能しません。 |
| 2 | 警告 | アクションは成功しましたが、問題が発生しました。 AEM WCM は正常に機能する場合と機能しない場合があります。 |
| 3 | 情報 | アクションが成功しました。 |

### カスタムログファイルの作成 {#create-a-custom-log-file}

>[!NOTE]
>
>Adobe Experience Managerを操作する場合、このようなサービスの設定を管理する方法はいくつかあります。参照 [OSGi の設定](/help/sites-deploying/configuring-osgi.md) を参照してください。

状況によっては、異なるログレベルでカスタムログファイルを作成する必要があります。 リポジトリで、次の操作を実行します。

1. 存在しない場合は、設定フォルダー ( `sling:Folder`) をプロジェクト用に作成します `/apps/<project-name>/config`.
1. `/apps/<project-name>/config` の下に、新しい [Apache Sling Logging Logger Configuration](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingloggerconfigurationfactoryconfiguration) 用のノードを作成します。

   * 名前：`org.apache.sling.commons.log.LogManager.factory.config-<identifier>`

      `<identifier>` の部分は、インスタンスを識別するフリーテキストに置き換えます（この情報は省略できません）。

      例：`org.apache.sling.commons.log.LogManager.factory.config-MINE`

   * 型：`sling:OsgiConfig`
   >[!NOTE]
   >
   >技術的に必須ではありませんが、`<identifier>` は一意にすることをお勧めします。

1. このノードで次のプロパティを設定します。

   * 名前：`org.apache.sling.commons.log.file`

      タイプ：String

      値：ログファイルを指定します。例：`logs/myLogFile.log`

   * 名前：`org.apache.sling.commons.log.names`

      タイプ：文字列[] （文字列 + 複数）

      値：ロガーがメッセージをログに記録する OSGi サービスを指定する。例えば、次のすべてが該当します。

      * `org.apache.sling`
      * `org.apache.felix`
      * `com.day`
   * 名前：`org.apache.sling.commons.log.level`

      タイプ：String

      値：必要なログレベル ( `debug`, `info`, `warn`または `error`);例： `debug`

   * 必要に応じてその他のパラメーターを設定します。

      * 名前：`org.apache.sling.commons.log.pattern`

         型：`String`

         値：必要に応じてログメッセージのパターンを指定します。次に例を示します。

         `{0,date,dd.MM.yyyy HH:mm:ss.SSS} *{4}* [{2}] {3} {5}`
   >[!NOTE]
   >
   >`org.apache.sling.commons.log.pattern` では、最大 6 個の引数がサポートされています。
   >
   >{0} タイプ `java.util.Date` のタイムスタンプ
   >
   >{1} ログマーカー
   >
   >{2} 現在のスレッドの名前
   >
   >{3} ロガーの名前
   >
   >{4} ログレベル
   >
   >{5} ログメッセージ
   >
   >ログ呼び出しに `Throwable`の場合、 stacktrace がメッセージに追加されます。

   >[!CAUTION]
   >
   >org.apache.sling.commons.log.names には値が必要です。

   >[!NOTE]
   >
   >ログライターのパスは、`crx-quickstart` の場所と相対的です。
   >
   >したがって、ログファイルが
   >
   >`logs/thelog.log`
   >
   >と指定されている場合、書き込み先は以下となります。
   >
   >`<cq-installation-dir>/crx-quickstart/logs/thelog.log`。
   >
   >また、ログファイルが
   >
   >`../logs/thelog.log`
   >
   >と指定されている場合、書き込み先は以下のディレクトリとなります。
   >
   >`<cq-installation-dir>/logs/`\
   >( つまり、 `<cq-installation-dir>/crx-quickstart/`)

1. この手順は、新しいライターが必要な場合（つまり、デフォルトのライターとは異なる設定を使用した場合）にのみ必要です。

   >[!CAUTION]
   >
   >新しい Logging Writer Configuration は、既存のデフォルトが適切でない場合にのみ必要です。
   >
   >明示的なライターが設定されていない場合、デフォルトに基づいて暗黙的なライターが自動的に生成されます。

   `/apps/<project-name>/config` の下に、新しい [Apache Sling Logging Writer Configuration](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingwriterconfigurationfactoryconfiguration) 用のノードを作成します。

   * 名前： `org.apache.sling.commons.log.LogManager.factory.writer-<identifier>` （作家）

      Logger の場合のように、`<identifier>` の部分は、インスタンスを識別するフリーテキストに置き換えます（この情報は省略できません）。例：`org.apache.sling.commons.log.LogManager.factory.writer-MINE`

   * 型：`sling:OsgiConfig`
   >[!NOTE]
   >
   >技術的に必須ではありませんが、`<identifier>` は一意にすることをお勧めします。

   このノードで次のプロパティを設定します。

   * 名前：`org.apache.sling.commons.log.file`

      型：`String`

      値：Logger で指定したファイルと一致するようにログファイルを指定します。

      この例の場合は `../logs/myLogFile.log` です。

   * 必要に応じてその他のパラメーターを設定します。

      * 名前：`org.apache.sling.commons.log.file.number`

         型：`Long`

         値：保持するログファイルの数を指定します。例： `5`

      * 名前：`org.apache.sling.commons.log.file.size`

         型：`String`

         値：ファイルのローテーションをサイズや日付によって制御するために、必要に応じて指定します。例えば、`'.'yyyy-MM-dd` とします。
   >[!NOTE]
   >
   >`org.apache.sling.commons.log.file.size` は、次のいずれかを設定することによって、ログファイルのローテーションを制御します。
   >
   >* 最大ファイルサイズ
   >* 時刻／日付のスケジュール

   >
   >：新しいファイルをいつ作成するかを示します（および、名前のパターンに従って既存のファイルの名前を変更します）。
   >
   >* サイズの制限は数値で指定できます。サイズインジケータが指定されていない場合は、バイト数と見なされます。または、サイズインジケータの 1 つを追加することもできます。 `KB`, `MB`または `GB` （大文字と小文字は無視されます）。
   >* 日時スケジュールは、`java.util.SimpleDateFormat` パターンとして指定できます。ファイルが回転されるまでの期間を定義します。 また、回転後のファイルに追加されるサフィックス（識別用）。

   >
   >デフォルトは「.」です。yyyy-MM-dd（毎日のログローテーションの場合）
   >
   >例えば、2010 年 1 月 20 日午前 0 時（またはこの日付以降の最初のログメッセージが正確に表示された場合）に、../logs/error.logは../logs/error.log.2010-01-20に名前が変更されます。 1 月 21 日のログは、次の日の変更にロールオーバーされるまで、（新しい空の） ../logs/error.logに出力されます。
   >
   >| `'.'yyyy-MM` | 毎月の初めにローテーション。 |
   >|---|---|
   >| `'.'yyyy-ww` | 毎週最初の日（ロケールによって異なる）にローテーション。 |
   >| `'.'yyyy-MM-dd` | 毎日深夜 12 時にローテーション。 |
   >| `'.'yyyy-MM-dd-a` | 毎日深夜 12 時および正午にローテーション。 |
   >| `'.'yyyy-MM-dd-HH` | 毎正時にローテーション。 |
   >| `'.'yyyy-MM-dd-HH-mm` | 毎分の初めにローテーション。 |
   >
   >メモ：日時を指定する場合：
   >
   >1. 一重引用符（&#39; &#39;）の範囲内で、リテラルテキストを「エスケープ」する必要があります。
      >
      >    特定の文字がパターン文字として解釈されるのを防ぎます。
   >
   >1. オプションの任意の場所で、有効なファイル名に使用できる文字のみを使用します。


1. 任意のツールで新しいログファイルを読み取ります。

   この例で作成されるログファイルは、です。 `../crx-quickstart/logs/myLogFile.log`.

Felix コンソールでは、Sling Log Support に関する情報も提供されます ( `../system/console/slinglog`;例： `https://localhost:4502/system/console/slinglog`.

### 監査レコードの検索 {#finding-the-audit-records}

監査記録は、誰がいつ何をしたかを記録するために保持されます。 AEM WCM と OSGi の両方のイベントに対して、異なる監査レコードが生成されます。

#### ページオーサリング時に表示されるAEM WCM 監査レコード {#aem-wcm-audit-records-shown-when-page-authoring}

1. ページを開きます。
1. サイドキックから、ロックアイコン付きのタブを選択し、ダブルクリックします。 **監査ログ…**
1. 新しいウィンドウが開き、現在のページの監査レコードのリストが表示されます。

   ![screen_shot_2012-02-02at43601pm](assets/screen_shot_2012-02-02at43601pm.png)

1. クリック **OK** ウィンドウを閉じるとき。

#### リポジトリ内のAEM WCM 監査レコード {#aem-wcm-auditing-records-within-the-repository}

`/var/audit` フォルダー内で、監査レコードは、リソースに応じて保持されます。個々のレコードとそのレコードに含まれる情報が表示されるまで、ドリルダウンできます。

これらのエントリには、ページの編集時に表示される情報と同じ情報が含まれます。

#### Web コンソールからの OSGi 監査レコード {#osgi-audit-records-from-the-web-console}

OSGi イベントで生成される監査記録は、AEM Web コンソールの「**設定ステータス**」タブ／「**ログファイル**」タブから確認できます。 

![screen_shot_2012-02-13at50346pm](assets/screen_shot_2012-02-13at50346pm.png)

## レプリケーションエージェントの監視 {#monitoring-your-replication-agents}

次の項目を監視できます： [レプリケーションキュー](/help/sites-deploying/replication.md) キューが停止したかブロックされたかを検出するには、次の手順を実行します。この場合、パブリッシュインスタンスまたは外部システムに問題がある可能性があります。

* すべての必須キューを有効にしますか？
* 無効なキューがまだ必要か
* `enabled`（有効な状態）のキューはすべて、ステータスが `idle` または `active` であり、これは正常な動作を示します。キューを `blocked`（ブロック状態）にしてはいけません。ブロックされている場合、多くは受信者側に問題があります。

* キューのサイズが時間の経過と共に大きくなる場合は、ブロックされたキューを示す可能性があります。

レプリケーションエージェントを監視するには：

1. 次にアクセス： **ツール** 」タブをAEMでクリックします。
1. クリック **レプリケーション**.
1. 適切な環境のエージェントへのリンク（左または右のウィンドウ）をダブルクリックします。例： **作成者のエージェント**.

   表示されるウィンドウには、オーサー環境のすべてのレプリケーションエージェントの概要が表示されます。この概要には、ターゲットとステータスも含まれます。

1. 適切なエージェント名（リンク）をクリックすると、そのエージェントに関する詳細情報が表示されます。

   ![chlimage_1](assets/chlimage_1.jpeg)

   ここでは、以下のことができます。

   * エージェントが有効かどうかを確認します。
   * レプリケーションのターゲットを確認します。
   * レプリケーションキューがアクティブ（有効）かどうかを確認します。
   * キュー内に項目があるかどうかを確認します。
   * **更新** または **クリア** ：キュー・エントリの表示を更新します。 これにより、キューに入ってから離れた項目を確認できます。
   * **ログを表示** をクリックして、レプリケーションエージェントによるアクションのログにアクセスします。
   * **接続をテスト** をターゲットインスタンスに追加します。
   * **再試行を強制** （必要に応じて）任意のキュー項目に対して。

   >[!CAUTION]
   >
   >パブリッシュインスタンスのリバースレプリケーションアウトボックスには、「接続をテスト」リンクを使用しないでください。
   >
   >送信トレイキューに対してレプリケーションテストを実行すると、リバースレプリケーションのたびに、テストレプリケーションより古い項目が再処理されます。
   >
   >このような項目がキュー内に存在する場合は、次の XPath JCR クエリを使用して見つかり、削除する必要があります。
   >
   >`/jcr:root/var/replication/outbox//*[@cq:repActionType='TEST']`

ここでも、すべてのレプリケーションエージェント（`/etc/replication/author` または `/etc/replication/publish` の下）を検出して、エージェントのステータス（`enabled`、`disabled`）および基になるキューのステータス（`active`、`idle`、`blocked`）を確認するソリューションを開発できます。

## パフォーマンスの監視 {#monitoring-performance}

[パフォーマンスの最適化](/help/sites-deploying/configuring-performance.md) は、開発中にフォーカスを受け取るインタラクティブなプロセスです。 デプロイ後は、特定の間隔またはイベントの後にレビューされます。

最適化のための情報収集に使用する方法は、継続中の監視にも使用できます。

>[!NOTE]
>
>具体的な[パフォーマンス向上のための設定](/help/sites-deploying/configuring-performance.md#configuring-for-performance)も確認できます。

次に、発生する一般的なパフォーマンスの問題と、その見つけ方、および対処方法に関する提案を示します。

| 領域 | 症状 | 容量を増やすには… | ボリュームを減らすには… |
|---|---|---|---|
| クライアント | クライアントの CPU 使用率が高くなります。 | より高いパフォーマンスでクライアント CPU をインストールします。 | (HTML) レイアウトを簡素化します。 |
|  | サーバーの CPU 使用率が低い。 | より高速なブラウザーにアップグレードします。 | クライアント側のキャッシュを改善します。 |
|  | 高速のクライアントと低速のクライアントがある。 |  |  |
| サーバー |  |  |  |
| ネットワーク | サーバーとクライアントの両方で CPU 使用率が低い。 | ネットワークのボトルネックを解消します。 | クライアントキャッシュの設定を改善/最適化します。 |
|  | サーバー上のローカルでの閲覧は（比較的）高速です。 | ネットワーク帯域幅を増やします。 | Web ページの「重み付け」を軽減します ( 例えば、画像の量を減らし、HTMLを最適化 )。 |
| Web サーバー | Web サーバーの CPU 使用率が高い。 | Web サーバーをクラスター化します。 | ページあたりのヒット数を減らす（訪問）。 |
|  |  | ハードウェアのロードバランサーを使用。 |  |
| アプリケーション | サーバの CPU 使用率が高い。 | AEMインスタンスをクラスター化します。 | CPU およびメモリのホグ（コードレビューとタイミング出力を使用）を検索し、除去します。 |
|  | メモリ消費率が高い。 |  | すべてのレベルでキャッシュを改善。 |
|  | 応答時間が遅い。 |  | テンプレートとコンポーネント（構造、ロジックなど）を最適化します。 |
| リポジトリ |  |  |  |
| キャッシュ |  |  |  |

パフォーマンスの問題は、接続速度の一時的な遅延、CPU 負荷など、Web サイトとは何の関係もない様々な原因に起因する場合があります。

また、すべての訪問者に影響を与えるか、一部の訪問者にのみ影響を与える場合があります。

一般的なパフォーマンスを最適化したり、特定の問題を解決したりする前に、これらの情報をすべて取得、並べ替え、分析する必要があります。

* パフォーマンスに関する問題が発生する前に、次の手順に従ってください。

   * 通常の状況下で、システムに関する十分な実務知識を構築するためにできるだけ多くの情報を収集する

* パフォーマンスの問題が発生した場合：

   * 1 つ（または複数）の標準の Web ブラウザーを使用して、（可能であれば）サーバー自体や一般的なパフォーマンスが優れていることがわかっている別のクライアント上で、それをレプリケートしてみます。
   * （システムに関連する）何かが適切な時間内に変更されたかどうか、およびこれらの変更がパフォーマンスに影響を与えた可能性があるかどうかを確認します
   * 次のような質問をします。

      * 問題は特定の時間にのみ発生しますか？
      * 問題は特定のページでのみ発生しますか？
      * 他のリクエストに影響があるか
   * 通常の状況でのシステムに関する知識と比較できるだけ多くの情報を収集します。


### パフォーマンスの監視および分析用ツール {#tools-for-monitoring-and-analyzing-performance}

次に、パフォーマンスの監視と分析に使用できるツールの一部の概要を示します。

これらのツールの一部は、オペレーティングシステムによって異なります。

<table>
 <tbody>
  <tr>
   <td>ツール</td>
   <td>分析に使用…</td>
   <td>使用状況/詳細情報…</td>
  </tr>
  <tr>
   <td>request.log</td>
   <td>応答時間と同時実行性。</td>
   <td><a href="#interpreting-the-request-log">request.log の解釈</a>.</td>
  </tr>
  <tr>
   <td>トラス/ストレース</td>
   <td>ページ読み込み</td>
   <td><p>システムの呼び出しおよびシグナルをトレースする Unix／Linux コマンド。ログレベルを <code>INFO</code> に上げます。</p> <p>リクエストごとのページ読み込み数とページを分析します。</p> </td>
  </tr>
  <tr>
   <td>スレッドダンプ</td>
   <td>JVM スレッドを観察します。 競合、ロック、および長期実行者を特定します。</td>
   <td><p>オペレーティングシステムによって異なります。<br /> - Unix／Linux：<code>kill -QUIT &lt;<em>pid</em>&gt;</code><br /> - Windows（コンソールモード）：Ctrl キーを押しながら Break キーをクリック<br /> </p> <p>また、 <a href="https://github.com/irockel/tda">TDA</a>.<br /> </p> </td>
  </tr>
  <tr>
   <td>ヒープダンプ</td>
   <td>パフォーマンスが低下する原因となるメモリ不足の問題。</td>
   <td><p>以下を追加します。<br /> <code>-XX:+HeapDumpOnOutOfMemoryError</code><br /> オプションからAEMへの Java™呼び出しへのアクセスが許可されます。</p> <p><a href="https://docs.oracle.com/javase/8/docs/technotes/guides/troubleshoot/prepapp002.html#CEGBHDFH">JVM のトラブルシューティングページのオプション／フラグ</a>を参照してください。</p> </td>
  </tr>
  <tr>
   <td>システムコール</td>
   <td>タイミングの問題を特定します。</td>
   <td><p>への呼び出し <code>System.currentTimeMillis()</code> または <code>com.day.util</code>. タイミングは、コードから、または <a href="#html-comments">HTMLコメント</a>.</p> <p><strong>注意：</strong> 必要に応じてアクティベート/アクティベート解除できるように、これらを実装します。システムがスムーズに動作している場合は、統計を収集するオーバーヘッドは不要です。</p> </td>
  </tr>
  <tr>
   <td>Apache Bench</td>
   <td>メモリリークを特定し、応答時間を選択的に分析します。</td>
   <td><p>基本的な使用方法は次のとおりです。</p> <p><code>ab -k -n &lt;<em>requests</em>&gt; -c &lt;<em>concurrency</em>&gt; &lt;<em>url</em>&gt;</code></p> <p>詳しくは、<a href="#apache-bench">Apache Bench</a> および <a href="https://httpd.apache.org/docs/2.4/programs/ab.html">ab man ページ</a>を参照してください。</p> </td>
  </tr>
  <tr>
   <td>Search Analysis</td>
   <td> </td>
   <td>検索クエリをオフラインで実行し、クエリの応答時間を特定し、結果セットをテストして確認します。<br /> </td>
  </tr>
  <tr>
   <td>JMeter</td>
   <td>読み込みおよび機能テスト。</td>
   <td><a href="https://jmeter.apache.org/">https://jmeter.apache.org/</a></td>
  </tr>
  <tr>
   <td>JProfiler</td>
   <td>CPU とメモリの詳細なプロファイル。</td>
   <td><a href="https://www.ej-technologies.com/">https://www.ej-technologies.com/</a></td>
  </tr>
  <tr>
   <td>Java™ Flight Recorder</td>
   <td>Java™ Flight Recorder(JFR) は、実行中の Java™アプリケーションに関する診断およびプロファイルデータを収集するためのツールです。</td>
   <td><a href="https://docs.oracle.com/javase/8/docs/technotes/guides/troubleshoot/tooldescr004.html#BABJJEEE">https://docs.oracle.com/javase/8/docs/technotes/guides/troubleshoot/tooldescr004.html#BABJJEEE</a></td>
  </tr>
  <tr>
   <td>JConsole</td>
   <td>JVM の指標とスレッドを観察します。</td>
   <td><p>使用方法：jconsole</p> <p><a href="https://docs.oracle.com/javase/8/docs/technotes/guides/management/jconsole.html">jconsole</a> および <a href="#monitoring-performance-using-jconsole">JConsole を使用したパフォーマンスの監視</a> を参照してください。</p> <p><strong>メモ：</strong>JDK 1.8 では、Top や TDA（Thread Dump Analyzer）などのプラグインを使用して JConsole を拡張できます。</p> </td>
  </tr>
  <tr>
   <td>Java™ VisualVM</td>
   <td>JVM 指標、スレッド、メモリ、およびプロファイルを観察します。</td>
   <td><p>使用法：jvisualvm または visualvm<br /> </p> <p><a href="https://docs.oracle.com/javase/8/docs/technotes/guides/visualvm/">visualvm</a> および <a href="#monitoring-performance-using-j-visualvm">(J)VisualVM</a> を使用したパフォーマンスの監視を参照してください。</p> <p><strong>メモ：</strong>JDK 1.8 では、プラグインを使用して VisualVM を拡張できます。VisualVM は JDK 9 以降で廃止されます。代わりに、Java™ Flight Recorder を使用します。</p> </td>
  </tr>
  <tr>
   <td>トラス、ストラス、lsof</td>
   <td>詳細なカーネル呼び出しとプロセス分析 (UNIX®)。</td>
   <td>Unix/Linux コマンド。</td>
  </tr>
  <tr>
   <td>タイミング統計</td>
   <td>ページのレンダリングのタイミングの統計を参照してください。</td>
   <td><p>ページレンダリングのタイミングの統計を確認するには、 <strong>Ctrl+Shift+U</strong> と一緒に <code>?debugClientLibs=true</code> を URL に設定します。</p> </td>
  </tr>
  <tr>
   <td>CPU およびメモリプロファイリングツール<br /> </td>
   <td><a href="#interpreting-the-request-log">開発中に低速の要求を分析する際に使用</a>。</td>
   <td>例えば、<a href="https://www.yourkit.com/">YourKit</a> などです。または <a href="https://docs.oracle.com/javase/8/docs/technotes/guides/troubleshoot/tooldescr004.html#BABJJEEE">Java™ Flight Recorder</a>.</td>
  </tr>
  <tr>
   <td><a href="#information-collection">情報収集</a></td>
   <td>インストールの進行中の状態。</td>
   <td>また、インストールに関する情報を可能な限り把握することで、パフォーマンスの変化の原因となった可能性がある項目を追跡し、その変更が正当かどうかを確認するのに役立ちます。 これらの指標を一定の間隔で収集し、大幅な変更を簡単に確認できるようにします。</td>
  </tr>
 </tbody>
</table>

### request.log の解釈 {#interpreting-the-request-log}

このファイルは、AEMに対しておこなわれたすべてのリクエストに関する基本情報を登録します。 このことから、貴重な結論を引き出すことができます。

`request.log` は、リクエストにかかる時間を確認するための組み込みの方法を提供します。開発目的では、次の操作をおこなうと便利です。 `tail -f` の `request.log` また、応答時間が遅いかどうかを確認します。 より大きなを分析するには `request.log`を使用する場合、Adobeは [使用 `rlog.jar` 応答時間に応じて並べ替えおよびフィルタリングできます。](#using-rlog-jar-to-find-requests-with-long-duration-times).

Adobeは、「低速」ページを `request.log`を設定し、それぞれを調整してパフォーマンスを向上させます。 コンポーネントごとのパフォーマンス指標を含めるか、次のようなパフォーマンスプロファイルツールを使用します。 ` [yourkit](https://www.yourkit.com/)`.

#### Web サイト上のトラフィックの監視 {#monitoring-traffic-on-your-website}

リクエストログは、おこなわれた各リクエストと、おこなわれた応答を登録します。

```xml
09:43:41 [66] -> GET /author/y.html HTTP/1.1
09:43:41 [66] <- 200 text/html 797ms
```

特定の期間（例えば、様々な 24 時間の期間）内のすべてのGETエントリを合計することで、Web サイトの平均トラフィックに関する情報を提供できます。

#### request.log を使用した応答時間の監視 {#monitoring-response-times-with-the-request-log}

パフォーマンス分析は、request.log から始めることをお勧めします。

`<cq-installation-dir>/crx-quickstart/logs/request.log`

ログは次のようになります（行が短くなり、簡単になります）。

```xml
31/Mar/2009:11:32:57 +0200 [379] -> GET /path/x HTTP/1.1
31/Mar/2009:11:32:57 +0200 [379] <- 200 text/html 33ms
31/Mar/2009:11:33:17 +0200 [380] -> GET /path/y HTTP/1.1
31/Mar/2009:11:33:17 +0200 [380] <- 200 application/json 39ms
```

このログは、リクエストまたは応答ごとに 1 行です。

* 各リクエストまたは応答がおこなわれた日付。
* リクエストの番号を角括弧で囲みます。 この数は、リクエストと応答に一致します。
* リクエスト（右向き矢印）か応答（左向き矢印）かを示す矢印です。
* 要求の行には、以下が含まれます。

   * メソッド ( 通常、GET、HEAD、POST)
   * リクエストされたページ
   * 議定書

* 応答の行には、以下が含まれます。

   * ステータスコード（200 は「成功」、404 は「ページが見つかりません」
   * MIME タイプ
   * 応答時間

小さなスクリプトを使用して、必要な情報をログファイルから抽出し、必要な統計を組み立てることができます。 これらの統計から、どのページまたはページのタイプが低速か、および全体的なパフォーマンスが満足のいくものかを確認できます。

#### request.log を使用した検索応答時間の監視 {#monitoring-search-response-times-with-the-request-log}

検索リクエストもログファイルに登録されます。

```xml
31/Mar/2009:11:35:34 +0200 [338] -> GET /author/playground/en/tools/search.html?query=dilbert&size=5&dispenc=utf-8 HTTP/1.1
31/Mar/2009:11:35:34 +0200 [338] <- 200 text/html 1562ms
```

したがって、上記のように、スクリプトを使用して関連情報を抽出し、統計を構築できます。

ただし、応答時間を決定した後は、リクエストに時間がかかっている理由と、応答を改善するために実行できる操作を分析します。

#### 現在のユーザーの数と影響の監視 {#monitoring-the-number-and-impact-of-concurrent-users}

ここでも、`request.log` を使用して、並行性およびそれに対するシステムの反応を監視できます。

負の影響が見られる前に、システムが処理できる同時ユーザー数を判断するためにテストを実施する必要があります。 ログファイルから結果を抽出するスクリプトを再度使用できます。

* 特定の期間内（1 分など）におこなわれるリクエストの数を監視します。
* 特定の数のユーザーがすべて同じリクエストを同時に（できるだけ近い場所で）おこなった場合の影響をテストします。 例えば、30 人のユーザーが **保存** 同時に

```xml
31/Mar/2009:11:45:29 +0200 [333] -> GET /author/libs/Personalize/content/statics.close.gif HTTP/1.1
31/Mar/2009:11:45:29 +0200 [334] -> GET /author/libs/Personalize/content/statics.detach.gif HTTP/1.1
31/Mar/2009:11:45:30 +0200 [335] -> GET /author/libs/CFC/content/imgs/logo.rZMNURccynWcTpCxyuBNiTCoiBMmw000.default.gif HTTP/1.1
31/Mar/2009:11:45:32 +0200 [335] <- 304 text/html 0ms
31/Mar/2009:11:45:33 +0200 [334] <- 200 image/gif 31ms
31/Mar/2009:11:45:38 +0200 [333] <- 200 image/gif 31ms
31/Mar/2009:11:45:42 +0200 [336] -> GET /author/libs/CFC/content/imgs/logo.rZMNURccynWcTZRXunQbbQtvuuCMbRRBuWXz0000.default.gif HTTP/1.1
31/Mar/2009:11:45:43 +0200 [337] -> GET /author/titlebar_bg.gif HTTP/1.1
31/Mar/2009:11:45:43 +0200 [336] <- 304 text/html 0ms
31/Mar/2009:11:45:44 +0200 [337] <- 304 text/html 0ms
```

### rlog.jar を使用した長期間のリクエストの検索 {#using-rlog-jar-to-find-requests-with-long-duration-times}

AEMには、次の様々なヘルパーツールが含まれています。
`<cq-installation-dir>/crx-quickstart/opt/helpers`

この道具の一つは `rlog.jar`を使用すると、すばやく並べ替えることができます `request.log` リクエストは、最長から最短の時間で、期間別に表示されます。

次のコマンドは、考えられる引数を示しています。

```shell
$java -jar rlog.jar
Request Log Analyzer Version 21584 Copyright 2005 Day Management AG
Usage:
  java -jar rlog.jar [options] <filename>
Options:
  -h               Prints this usage.
  -n <maxResults>  Limits output to <maxResults> lines.
  -m <maxRequests> Limits input to <maxRequest> requests.
  -xdev            Exclude POST request to CRXDE.
```

例えば、 `request.log` ファイルをパラメーターとして指定し、最も長い期間を持つ 10 件目のリクエストを表示します。

```shell
$ java -jar ../opt/helpers/rlog.jar -n 10 request.log
*Info * Parsed 464 requests.
*Info * Time for parsing: 22ms
*Info * Time for sorting: 2ms
*Info * Total Memory: 1mb
*Info * Free Memory: 1mb
*Info * Used Memory: 0mb
------------------------------------------------------
     18051ms 31/Mar/2009:11:15:34 +0200 200 GET /content/geometrixx/en/company.html text/ html
      2198ms 31/Mar/2009:11:15:20 +0200 200 GET /libs/cq/widgets.js application/x-javascript
      1981ms 31/Mar/2009:11:15:11 +0200 200 GET /libs/wcm/content/welcome.html text/html
      1973ms 31/Mar/2009:11:15:52 +0200 200 GET /content/campaigns/geometrixx.teasers..html text/html
      1883ms 31/Mar/2009:11:15:20 +0200 200 GET /libs/security/cq-security.js application/x-javascript
      1876ms 31/Mar/2009:11:15:20 +0200 200 GET /libs/tagging/widgets.js application/x-javascript
      1869ms 31/Mar/2009:11:15:20 +0200 200 GET /libs/tagging/widgets/themes/default.js application/x-javascript
      1729ms 30/Mar/2009:16:45:56 +0200 200 GET /libs/wcm/content/welcome.html text/html; charset=utf-8
      1510ms 31/Mar/2009:11:15:34 +0200 200 GET /bin/wcm/contentfinder/asset/view.json/ content/dam?_dc=1238490934657&query=&mimeType=image&_charset_=utf-8 application/json
      1462ms 30/Mar/2009:17:23:08 +0200 200 GET /libs/wcm/content/welcome.html text/html; charset=utf-8
```

個人を連結 `request.log` ファイルを参照してください。

### Apache Bench {#apache-bench}

特殊なケース（ガベージコレクションなど）の影響を最小限に抑えるために、 `apachebench` ( 例： [ab](https://httpd.apache.org/docs/2.4/programs/ab.html) を参照 ) を使用して、メモリリークの特定と応答時間の選択的な分析をおこなうことができます。

Apache Bench は次の方法で使用できます。

```shell
$ ab -c 5 -k -n 1000 "https://localhost:4503/content/geometrixx/en/company.html"
This is ApacheBench, Version 2.3 <$Revision: 655654 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, https://www.zeustech.net/
Licensed to The Apache Software Foundation, https://www.apache.org/

Benchmarking localhost (be patient)
Completed 100 requests
Completed 200 requests
Completed 300 requests
Completed 400 requests
Completed 500 requests
Completed 600 requests
Completed 700 requests
Completed 800 requests
Completed 900 requests
Completed 1000 requests
Finished 1000 requests

Server Software: Day-Servlet-Engine/4.1.52
Server Hostname: localhost
Server Port: 4503

Document Path: /content/geometrixx/en/company.html
Document Length: 24127 bytes

Concurrency Level: 5
Time taken for tests: 69.766 seconds
Complete requests: 1000
Failed requests: 998
(Connect: 0, Receive: 0, Length: 998, Exceptions: 0)
Write errors: 0
Keep-Alive requests: 0
Total transferred: 24160923 bytes
HTML transferred: 24010923 bytes
Requests per second: 14.33 /sec (mean)
Time per request: 348.828 [ms] (mean)
Time per request: 69.766 [ms] (mean, across all concurrent requests)
Transfer rate: 338.20 [Kbytes/sec] received

Connection Times (ms)
min mean[+/-sd] median max
Connect: 0 1 3.9 0 58
Processing: 138 347 568.5 282 8106
Waiting: 137 344 568.1 281 8106
Total: 139 348 568.4 283 8106

Percentage of the requests served within a certain time (ms)
50% 283
66% 323
75% 356
80% 374
90% 439
95% 512
98% 1047
99% 1132
100% 8106 (longest request)
```

上記の番号は、デフォルトのAEMインストールに含まれている、Geometrixx会社のページにアクセスする標準の MAcBook Pro ノートパソコン（2010 年中頃）から取得されます。 ページはシンプルですが、パフォーマンス向けに最適化されていません。

この `apachebench` また、すべての同時リクエストの平均値としてリクエストあたりの時間も表示します。参照 `Time per request: 54.595 [ms]` （つまり、すべての同時リクエストに対して）。 同時実行パラメーター `-c` の値（一度に実行する複数リクエストの数）を変更して、影響を確認できます。

### 要求カウンター {#request-counters}

リクエストトラフィックに関する情報（特定の期間内のリクエスト数）は、インスタンスの負荷を示します。 この情報は、 [request.log](#interpreting-the-request-log)カウンターを使用すると、データ収集を自動化して次のことを確認できます。

* アクティビティの大きな違い（「多数のリクエスト」と「低アクティビティ」を区別）
* インスタンスが使用されていない場合
* 再起動（カウンタが 0 にリセットされる）が発生した場合

情報の収集を自動化するには、RequestFilter をインストールして、リクエストごとにカウンタを増やすこともできます。 異なる期間に対して複数のカウンタを使用できます。

収集された情報は、次の内容を示すために使用できます。

* 活動の大きな変化
* 冗長なインスタンス
* 再起動（カウンターが 0 にリセットされた場合）

### HTMLコメント {#html-comments}

サーバーのパフォーマンスのために、すべてのプロジェクトに `html comments` を含めることをお勧めします。多くの良い公的な例が見つかります。ページを選択し、表示するページソースを開いて、下までスクロールします。次のようなコードが表示されます。

```xml
</body>
 </html>
        <!--
        Page took 58 milliseconds to be rendered by server
         -->
```

### JConsole を使用したパフォーマンスの監視 {#monitoring-performance-using-jconsole}

ツールコマンド `jconsole` を、JDK で使用できます。

1. AEM インスタンスを起動します。
1. 実行 `jconsole.`
1. AEM インスタンスを選択して「**接続**」をクリックします。

1. 内から `Local` アプリケーション、ダブルクリック `com.day.crx.quickstart.Main`;概要はデフォルトで表示されます。

   ![chlimage_1-1](assets/chlimage_1-1.png)

   これで、他のオプションを選択できます。

### （J）VisualVM を使用したパフォーマンスの監視 {#monitoring-performance-using-j-visualvm}

JDK 6～8 の場合、ツールコマンド `visualvm` を使用できます。JDK をインストールしたら、次の手順を実行できます。

1. AEM インスタンスを起動します。

   >[!NOTE]
   >
   >Java™ 5 を使用している場合、 `-Dcom.sun.management.jmxremote` JVM を起動する Java™コマンドラインへの引数。 JMX は、Java™ 6 ではデフォルトで有効になっています。

1. 次のいずれかを実行します。

   * `jvisualvm`：JDK 1.6 bin フォルダー内（テスト済みバージョン）
   * `visualvm`：[VisualVM](https://docs.oracle.com/javase/8/docs/technotes/guides/visualvm/) からダウンロードできます（最先端バージョン）

1. 内から `Local` アプリケーション、ダブルクリック `com.day.crx.quickstart.Main`. 「概要」がデフォルトで表示されます。

   ![chlimage_1-2](assets/chlimage_1-2.png)

   これで、「モニター」など、他のオプションを選択できます。

   ![chlimage_1-3](assets/chlimage_1-3.png)

このツールを使用して、スレッドダンプとメモリヘッドダンプを生成できます。 この情報は、多くの場合、テクニカルサポートチームからリクエストされます。

### 情報収集 {#information-collection}

インストールに関する情報を可能な限り把握することで、パフォーマンスの変化の原因となった可能性がある項目を追跡し、その変更が正当かどうかを確認できます。 これらの指標を一定の間隔で収集し、大幅な変更を簡単に確認できるようにします。

有益な情報を以下に示します。

* [システムで作業をしている作成者の数](#how-many-authors-are-working-with-the-system)
* [1 日あたりのページアクティベーションの平均数](#what-is-the-average-number-of-page-activations-per-day)
* [このシステムで現在保守しているページ数](#how-many-pages-do-you-currently-maintain-on-this-system)
* [MSM を使用する場合は、1 ヶ月あたりのロールアウトの平均数](#if-you-use-msm-what-is-the-average-number-of-rollouts-per-month)
* [1 ヶ月あたりのライブコピーの平均数](#what-is-the-average-number-of-live-copies-per-month)
* [AEM Assets を使用する場合は、Assets で現在保守しているアセットの数](#ifyouusecqdamhowmanyassetsdoyoucurrentlymaintainincqdam)
* [アセットの平均サイズ](#what-is-the-average-size-of-the-assets)
* [現在使用されているテンプレートの数](#how-many-templates-are-currently-used)
* [現在使用されているコンポーネントの数](#how-many-components-are-currently-used)
* [ピーク時のオーサーシステムの 1 時間あたりの要求数](#how-many-requests-per-hour-do-you-have-on-the-author-system-at-peak-time)
* [ピーク時のパブリッシュシステムの 1 時間あたりの要求数](#how-many-requests-per-hour-do-you-have-on-the-publish-system-at-peak-time)

#### システムで作業をしている作成者の数 {#how-many-authors-are-working-with-the-system}

インストール以降にシステムを使用した作成者の数を確認するには、次のコマンドラインを使用します。

```shell
cd <cq-installation-dir>/crx-quickstart/logs
cut -d " " -f 3 access.log | sort -u | wc -l
```

特定の日付で作業している作成者の数を確認するには：

```shell
grep "<date>" access.log | cut -d " " -f 3 | sort -u | wc -l
```

#### 1 日あたりのページアクティベーションの平均数 {#what-is-the-average-number-of-page-activations-per-day}

サーバーのインストール以降のページのアクティベーションの合計数を確認するには、リポジトリクエリを使用します。CRXDE を使用して — ツール/クエリ：

* **型** `XPath`

* **パス** `/`

* **クエリ** `//element(*, cq:AuditEvent)[@cq:type='Activate']`

その後、インストール以降の経過日数を計算し、平均を計算します。

#### このシステムで現在保守しているページ数 {#how-many-pages-do-you-currently-maintain-on-this-system}

サーバー上の現在のページ数を確認するには、リポジトリクエリを使用します。CRXDE — ツール — クエリ：

* **型** `XPath`

* **パス** `/`

* **クエリ** `//element(*, cq:Page)`

#### MSM を使用する場合は、1 ヶ月あたりのロールアウトの平均数 {#if-you-use-msm-what-is-the-average-number-of-rollouts-per-month}

インストール後のロールアウトの合計数を判断するには、リポジトリクエリを使用します。CRXDE を使用して — ツール/クエリ：

* **型** `XPath`

* **パス** `/`

* **クエリ** `//element(*, cq:AuditEvent)[@cq:type='PageRolledOut']`

インストール以降の経過月数を計算し、平均を計算します。

#### 1 ヶ月あたりのライブコピーの平均数 {#what-is-the-average-number-of-live-copies-per-month}

インストール後に行われたライブコピーの合計数を確認するには、リポジトリクエリを使用します。CRXDE — ツール — クエリ：

* **型** `XPath`

* **パス** `/`

* **クエリ** `//element(*, cq:LiveSyncConfig)`

ここでも、インストール以降の経過月数を使用して、平均を計算します。

#### AEM Assets を使用する場合は、Assets で現在保守しているアセットの数 {#if-you-use-aem-assets-how-many-assets-do-you-currently-maintain-in-assets}

現在保守している DAM アセットの数を確認するには、リポジトリクエリを使用します。CRXDE のツール／クエリで、次のように指定します。

* **型** `XPath`
* **パス** `/`
* **クエリ** `/jcr:root/content/dam//element(*, dam:Asset)`

#### アセットの平均サイズ {#what-is-the-average-size-of-the-assets}

`/var/dam` フォルダーの合計サイズを特定するには：

1. WebDAV を使用して、 リポジトリをローカルファイルシステムにマップします。

1. 次のコマンドラインを使用します。

   ```shell
   cd /Volumes/localhost/var
   du -sh dam/
   ```

   平均サイズを取得するには、グローバルサイズを、`/var/dam` 内のアセットの合計数（上記で得られた値）で割ります。

#### 現在使用されているテンプレートの数 {#how-many-templates-are-currently-used}

現在サーバー上にあるテンプレートの数を確認するには、リポジトリクエリを使用します。CRXDE — ツール — クエリ：

* **型** `XPath`
* **パス** `/`
* **クエリ** `//element(*, cq:Template)`

#### 現在使用されているコンポーネントの数 {#how-many-components-are-currently-used}

現在サーバー上にあるコンポーネントの数を確認するには、リポジトリクエリを使用します。CRXDE — ツール — クエリ：

* **型** `XPath`
* **パス** `/`
* **クエリ** `//element(*, cq:Component)`

#### ピーク時のオーサーシステムの 1 時間あたりの要求数 {#how-many-requests-per-hour-do-you-have-on-the-author-system-at-peak-time}

ピーク時のオーサーシステム上の 1 時間あたりの要求数を判断するには、次の手順を実行します。

1. インストール後の要求の総数を確認するには、次のコマンドラインを使用します。

   ```shell
   cd <cq-installation-dir>/crx-quickstart/logs
   grep -R "\->" request.log | wc -l
   ```

1. 開始日と終了日を特定するには、以下を使用します。

   ```shell
   vim request.log
   G / 1G: for the last/first lines
   ```

   これらの値を使用して、インストール後の経過時間数を計算し、1 時間あたりの平均リクエスト数を計算します。

#### ピーク時のパブリッシュシステムの 1 時間あたりの要求数 {#how-many-requests-per-hour-do-you-have-on-the-publish-system-at-peak-time}

パブリッシュインスタンスで上記の手順を繰り返します。

## 具体的なシナリオの分析 {#analyzing-specific-scenarios}

次に、特定のパフォーマンスの問題が発生し始めた場合の確認方法に関する推奨事項を示します。 リストは（残念ながら）完全に網羅的ではありません。

>[!NOTE]
詳しくは、以下の記事も参照してください。
* [スレッドダンプ](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17452.html?lang=ja)
* [メモリの問題の分析](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17482.html?lang=ja)
* [ビルトインプロファイラーによる分析](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17499.html?lang=ja)
* [遅いプロセスとブロックされたプロセスの分析](https://helpx.adobe.com/jp/experience-manager/kb/AnalyzeSlowAndBlockedProcesses.html)
>


### 100 %の CPU {#cpu-at}

システムの CPU が常に 100 %で稼働している場合は、次の点を確認してください。

* ナレッジベース

   * [遅延しているプロセスおよびブロックされたプロセスの分析](https://helpx.adobe.com/jp/experience-manager/kb/AnalyzeSlowAndBlockedProcesses.html)

### メモリ不足 {#out-of-memory}

このようなエラーは開発およびテスト中に検出されるはずですが、一部のシナリオが誤って検出される場合があります。

システムのメモリが不足している場合は、パフォーマンスの低下やサブテキストを含むエラーメッセージなど、様々な方法でこの問題が見られます。

`java.lang.OutOfMemoryError`

このような場合は、以下をチェックします。

* [AEM を起動](/help/sites-deploying/deploy.md#getting-started)するために使用される JVM 設定
* ナレッジベース

   * [メモリの問題を分析](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17482.html?lang=ja)

### ディスク I/O {#disk-i-o}

システムのディスク容量が不足しているか、ディスクがスラッシュしている場合は、次を参照してください。

* デバッグ情報の収集を無効にしているかどうかに関わらず、次のような様々な場所で設定できます。

   * [Apache Sling JSP Script Handler](/help/sites-deploying/osgi-configuration-settings.md#apacheslingjspscripthandler)
   * [Apache Sling JavaScript Handler](/help/sites-deploying/osgi-configuration-settings.md#apacheslingjavascripthandler)
   * [Apache Sling Logging Configuration](/help/sites-deploying/osgi-configuration-settings.md#apacheslingloggingconfiguration)
   * [CQ HTML Library Manager](/help/sites-deploying/osgi-configuration-settings.md#daycqhtmllibrarymanager)
   * [CQ WCM Debug Filter](/help/sites-deploying/osgi-configuration-settings.md#daycqwcmdebugfilter)
   * [Logger](/help/sites-deploying/monitoring-and-maintaining.md#activating-the-debug-log-level)

* [バージョンのパージ](/help/sites-deploying/version-purging.md)を設定しているかどうかと、その設定方法
* ナレッジベース

   * [開いているファイルが多すぎます](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17470.html?lang=ja)
   * [ジャーナルの消費ディスク容量が多すぎます](https://helpx.adobe.com/jp/experience-manager/kb/JournalTooMuchDiskSpace.html)

### 通常のパフォーマンス低下 {#regular-performance-degradation}

再起動後（場合によっては 1 週間以降）にインスタンスのパフォーマンスが低下している場合は、次の点を確認できます。

* [メモリ不足](#outofmemory)
* ナレッジベース

   * [閉じられていないセッション](https://helpx.adobe.com/jp/experience-manager/kb/AnalyzeUnclosedSessions.html)

### JVM の調整 {#jvm-tuning}

Java™ Virtual Machine(JVM) は、チューニング ( 特に Java™ 7 以降 ) に関して改善されました。 したがって、適切な固定 JVM サイズを指定し、デフォルトを使用することが適している場合が多いです。

デフォルトの設定が適切でない場合は、GC のパフォーマンスを監視および評価する方法を確立することが重要です。 JVM を調整する前に、調整を行ってください。 このプロセスには、ヒープサイズ、アルゴリズム、その他の側面を含む監視要因が含まれます。

一般的な選択肢は次のとおりです。

* VerboseGC：

   ```
   -verbose:gc \
    -Xloggc:$LOGS/verbosegc.log \
    -XX:+PrintGCDetails \
    -XX:+PrintGCDateStamps
   ```

結果のログは、次のような GC 可視化機能によって取り込み可能です。

` [https://www.ibm.com/developerworks/library/j-ibmtools2/](https://www.ibm.com/developerworks/library/j-ibmtools2/)`

JConsole の場合は以下のとおりです。

* これらの設定は、「広く開放された」JMX 接続用です。

   ```
   -Dcom.sun.management.jmxremote \
    -Dcom.sun.management.jmxremote.port=8889 \
    -Dcom.sun.management.jmxremote.authenticate=false \
    -Dcom.sun.management.jmxremote.ssl=false
   ```

* 次に、JConsole を使用して JVM に接続します。以下を参照してください。
   ` [https://docs.oracle.com/javase/8/docs/technotes/guides/management/jconsole.html](https://docs.oracle.com/javase/8/docs/technotes/guides/management/jconsole.html)`

使用されているメモリ量、使用されている GC アルゴリズム、実行に要する時間、およびこのプロセスがアプリケーションのパフォーマンスに与える影響を確認できます。 これがなければ、チューニングは単に「ランダムにひねくれるノブ」に過ぎません。

>[!NOTE]
oracleの VM の場合、次の場所にも情報があります。
[https://docs.oracle.com/javase/8/docs/technotes/guides/vm/server-class.html](https://docs.oracle.com/javase/8/docs/technotes/guides/vm/server-class.html)
