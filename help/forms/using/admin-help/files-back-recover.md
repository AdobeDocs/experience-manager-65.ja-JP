---
title: バックアップおよび回復するファイル
seo-title: Files to back up and recover
description: バックアップする必要のあるアプリケーションとデータファイルについて説明します。
seo-description: This document describes the application and data files that must be backed up.
uuid: ba04adb9-675a-48f2-ad52-39c1266e423b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 6f9a294d-24bd-4e4b-b929-2809f5e6cef9
exl-id: d2dd381d-a7d2-4fec-a8ba-7ca037fd9dc1
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '2072'
ht-degree: 98%

---

# バックアップおよび回復するファイル {#files-to-back-up-and-recover}

バックアップする必要のあるアプリケーションとデータファイルについては、以下の節で詳しく説明します。

バックアップと復旧に関して次の点を考慮してください。

* データベースは、GDS および AEM リポジトリの前にバックアップを取る必要があります。
* バックアップのためにクラスター環境内でノードを下げる必要がある場合は、セカンダリノードをプライマリノードの前にシャットダウンしてください。そうしないと、クラスターまたはサーバー内で一貫性がなくなる可能性があります。また、プライマリノードはすべてのセカンダリノードよりも前にライブにする必要があります。
* クラスターの復旧操作では、アプリケーションサーバーはクラスター内の各ノードごとに停止する必要があります。

## グローバルドキュメントストレージディレクトリ {#global-document-storage-directory}

GDS は、プロセス内で使用される長期間有効なファイルの保存に使用されるディレクトリです。長期間有効なファイルの有効期間内には、AEM Forms システムが 1 回以上起動され、期間は数日間、数年間に渡る場合もあります。長期間有効なファイルには、PDF、ポリシー、フォームテンプレートなどがあります。長期間有効なファイルは、多くの AEM Forms デプロイメントの全体的な状態の中で重要な部分です。長期間有効なドキュメントが一部でも失われたり破損したりすると、forms サーバーが不安定な状態になるおそれがあります。

非同期ジョブの呼び出しの入力ドキュメントも GDS に保存されます。これらのドキュメントは、要求を処理するために使用可能な状態になっている必要があります。したがって、GDS をホストするファイルシステムの信頼性を考慮し、サービス要件の品質およびレベルとして適切な RAID（Redundant Array of Independent Disks）またはその他のテクノロジーを採用することが重要です。

GDS の場所は、AEM forms のインストールプロセス中に決定するか、管理コンソールを使用して後から決定することもできます。GDS の高可用性を実現する場所を維持するほかに、ドキュメントのデータベース保存を有効にすることもできます。[ドキュメントの保存にデータベースを使用する場合のバックアップオプション](files-back-recover.md#backup-options-when-database-is-used-for-document-storage)を参照してください。

### GDS の場所 {#gds-location}

インストール時に場所を指定しないと、アプリケーションサーバーのインストールディレクトリの下にあるディレクトリがデフォルトの場所になります。アプリケーションサーバーの次のディレクトリをバックアップする必要があります。

* (JBoss) `[appserver root]/server/'server'/svcnative/DocumentStorage`
* (WebLogic) `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage`
* (WebSphere) `[appserver root]/installedApps/adobe/'server'/DocumentStorage`

GDS の場所をデフォルト以外の場所に変更した場合は、新しい場所を次のように確認できます。

* 管理コンソールにログインし、設定／コアシステム設定／設定をクリックします。
* 「グローバルドキュメントストレージディレクトリ」ボックスで指定されている場所を記録します。

クラスター環境では通常、GDS はネットワーク上で共有されているディレクトリを指し、すべてのクラスターノードに対して読み取り / 書き込みアクセスが可能です。

元の場所が使用できなくなった場合、回復中に GDS の場所を変更できます（[回復中の GDS の場所の変更](/help/forms/using/admin-help/recovering-aem-forms-data.md#changing-the-gds-location-during-recovery)を参照）。

### ドキュメントの保存にデータベースを使用する場合のバックアップオプション {#backup-options-when-database-is-used-for-document-storage}

管理コンソールを使用して AEM Forms のデータベースで AEM Forms ドキュメントの保存を有効にすることができます。このオプションを使用してすべての永続ドキュメントをデータベースに保存する場合でも、AEM Forms にはファイルシステムベースの GDS ディレクトリが必要です。その理由は、AEM Forms のセッションと呼び出しに関連する永続ファイル、一時ファイルおよびリソースの保存に GDS ディレクトリが使用されるためです。

管理コンソールのコアシステム設定の「データベースでドキュメントの保存を有効にする」オプションを選択した場合、または Configuration Manager を使用した場合、AEM forms ではスナップショットバックアップモードおよびローリングバックアップモードが許可されません。 したがって、AEM Forms を使用してバックアップモードを管理する必要がなくなります。このオプションを使用する場合は、オプションを有効にした後、1 回のみ GDS をバックアップする必要があります。バックアップから AEM Forms を回復する場合、GDS のバックアップディレクトリの名前を変更したり GDS を復元したりする必要はありません。

## AEM リポジトリ {#aem-repository}

AEM リポジトリ（crx-repository）は、AEM Forms のインストール時に crx-repository が設定された場合に作成されます。crx-repository ディレクトリの場所は、AEM Forms のインストールプロセス中に決まります。AEM Forms における AEM Forms データの一貫性を保つために、データベースと GDS と一緒に AEM リポジトリのバックアップと復旧が必要です。AEM リポジトリには、Correspondence Management Solution、Forms Manager および AEM Forms Workspace のデータが含まれます。

### Correspondence Management Solution {#correspondence-management-solution}

Correspondence Management Solution は、安全でパーソナライズされたインタラクティブな通信の作成、アセンブリおよび配信を集中管理します。作成からアーカイブまで合理化されたプロセスで、承認済みコンテンツおよびカスタム作成コンテンツから通信情報を簡単にまとめることができます。その結果、カスタマーは、適時の正確で便利な安全の適切なコミュニケーションが得られます。簡易性、速度および生産性のために合理化されたプロセスによって、顧客との対話の価値を最大限にし、コストとリスクを最小限に抑えます。

シンプルな Correspondence Managemant Solutions セットアップには、同じマシンまたは別々のマシンに、オーサーインスタンスとパブリッシュインスタンスが含まれます。

### Forms Manager {#forms-manager}

Forms Manager は、フォームの更新、管理、リタイアのプロセスを効率的に実行します。

### AEM Forms Workspace {#html-workspace}

AEM Forms Workspace は、Flex Workspace（JEE 上の AEM Forms では廃止されています）の性能に匹敵しており、Workspace を展開、統合する新しい機能を追加して、よりユーザーフレンドリなものにします。

>[!NOTE]
>
>AEM Forms のリリースでは Flex Workspace は廃止されています。

Flash Player と Adobe Reader を使用しなくてもクライアントでタスク管理が可能です。 PDF フォームと Flex フォームの他に、HTML フォームのレンダリングを容易にします。

## AEM Forms データベース {#aem-forms-database}

AEM Forms データベースに格納される情報には、フォームの生成結果、サービスの設定、プロセスの状態、GDS 内にあるファイルへのデータベース参照、およびコンテンツ保存場所のルートディレクトリ内にあるファイルへのデータベース参照（Content Services の場合）などがあります。データベースのバックアップはサービスを中断することなくリアルタイムで実行でき、特定の時点または特定の変更に回復できます。ここでは、バックアップをリアルタイムで実行するためのデータベースの設定方法について説明します。

正しく設定された AEM Forms システムでは、システム管理者とデータベース管理者は、簡単な調整だけで、システムを一貫性のある既知の状態に回復できます。

データベースをリアルタイムでバックアップするには、スナップショットモードを使用するか、指定されたログモードで実行されるようにデータベースを設定する必要があります。この設定により、データベースが開いており、使用可能な状態になっているときに、データベースファイルをバックアップできます。さらに、データベースをこれらのモードで実行している場合は、データベースでそのロールバックとトランザクションログが維持されます。

>[!NOTE]
>
>Adobe® LiveCycle® Content Services ES（非推奨）は LiveCycle と共にインストールされるコンテンツ管理システムです。Content Services では、ユーザーは人間中心のプロセスを設計、管理、監視および最適化することができます。Content Services（非推奨）のサポートは 2014 年 12 月 31 日をもって終了しています。[アドビ製品のライフサイクルに関するドキュメント](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html?lang=ja)を参照してください。

### DB2 {#db2}

DB2 データベースをアーカイブログモードで実行されるように設定します。

>[!NOTE]
>
>ご利用の AEM Forms 環境が以前のバージョンの AEM Forms からアップグレードされており、DB2 を使用している場合、オンラインバックアップはサポートされません。この場合、AEM Forms をシャットダウンして、オフラインバックアップを実行する必要があります。今後のバージョンの AEM Forms では、アップグレードユーザーの場合でもオンラインバックアップがサポートされる予定です。

IBM は、データベース管理者がバックアップと回復タスクを実行する際に役に立つ次のようなツールやヘルプシステムを提供しています。

* IBM DB2 Archive Log Accelerator
* IBM DB2 Data Archive エキスパート

DB2 には、Tivoli Storage Manager にデータベースをバックアップするための組み込み機能があります。Tivoli Storage Manager を使用して、DB2 バックアップを他のメディアやローカルのハードドライブに保存できます。

### Oracle {#oracle}

スナップショットバックアップを使用するか、Oracle データベースをアーカイブログモードで実行されるように設定します（「[Oracle Backup: An Introduction](https://www.databasedesign-resource.com/oracle-backup.md)」を参照。）Oracle データベースのバックアップと回復について詳しくは、次のサイトを参照してください。

[Oracle Backup and Recovery：](https://www.oracle.com/technetwork/database/features/availability/br-overview-097160.html)バックアップと回復の概念、および Recovery Manager（RMAN）を使用したバックアップ、回復およびレポートの最も一般的な方法について詳しく説明し、バックアップと回復の計画の立て方の詳細についても説明しています。

[Oracle Database Backup and Recovery User&#39;s Guide：](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10642.pdf)RMAN アーキテクチャ、バックアップと回復の概念とメカニズム、高度な回復方法（ポイントインタイム回復やデータベースフラッシュバック機能など）、およびバックアップと回復のパフォーマンスチューニングについて詳しく説明しています。また、RMAN ではなく、ホストのオペレーティングシステム機能を使用したユーザー管理のバックアップと回復についても説明しています。このマニュアルは、より高度なデータベースデプロイメントのバックアップと回復および高度な回復シナリオを行う場合は参照する必要があります。

[Oracle Database Backup and Recovery Reference：](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10643.pdf)RMAN の全コマンドの構文とセマンティクスが完全に網羅されています。また、バックアップと回復アクティビティのレポートに使用できるデータベースビューについて説明しています。

### SQL Server {#sql-server}

スナップショットバックアップを使用するか、SQL Server データベースをトランザクションログモードで実行されるように設定します。

SQL Server には、次の 2 つのバックアップと回復ツールもあります。

* SQL Server Management Studio（GUI）
* T-SQL（コマンドライン）

詳しくは、[バックアップと復元](https://msdn.microsoft.com/en-us/library/ms187048(v=SQL.90).aspx)を参照してください。

### MySQL {#mysql}

MySQLAdmin を使用するか Windows で INI ファイルを変更して、MySQL データベースがバイナリログモードで実行されるように設定します（「[MySQL binary logging](https://dev.mysql.com/doc/refman/5.1/en/binary-log.html)」を参照）。MySQL のホットバックアップツールも InnoBase ソフトウェアから利用できます（「[Innobase Hot Backup](https://www.innodb.com/hot-backup/features.md)」を参照）。

>[!NOTE]
>
>MySQL のデフォルトのバイナリログモードは「STATEMENT」です。このモードでは、Content Services（非推奨）で使用されるテーブルとの互換性がありません。このデフォルトのモードでバイナリログを使用すると、Content Services（非推奨）でエラーが発生します。システム内に Content Services（非推奨）が含まれている場合は、「MIXED」ログモードを使用します。「MIXED」ログを有効にするには、my.ini ファイルに次の引数を追加します。 `binlog_format=mixed log-bin=logname`

mysqldump ユーティリティを使用して、完全なデータベースバックアップを取得できます。完全バックアップは必要ですが、その実行が容易ではない場合があります。完全バックアップによって大量のバックアップファイルが生成され、処理に時間がかかります。増分バックアップを実行する場合は、前の節で説明したように `log-bin` オプションを使用してサーバーを起動してください。MySQL サーバーが再起動するたびに、現在のバイナリログへの書き込みが停止し、新しいログが作成され、以降はそのログが現在のバイナリログになります。`FLUSH LOGS SQL` コマンドを使用すると、手動で強制的に切り替えることができます。最初の完全バックアップ後の増分バックアップは、mysqladmin ユーティリティと `flush-logs` コマンドを使用して実行されます。これにより新しいログファイルが作成されます。

「[Backup Strategy Summary](https://dev.mysql.com/doc/refman/5.5/en/backup-strategy-summary.html)」を参照してください。

```text
binlog_format=mixed
log-bin=logname
```

## コンテンツ保存場所のルートディレクトリ（Content Services のみ） {#content-storage-root-directory-content-services-only}

コンテンツ保存場所のルートディレクトリには、すべてのドキュメント、アーティファクト、およびインデックスの格納された Content Services（非推奨）リポジトリが含まれています。コンテンツ保存場所のルートディレクトリツリーは、バックアップする必要があります。ここでは、スタンドアロン環境およびクラスター環境で、コンテンツ保存場所のルートディレクトリの位置を判別する方法について説明します。

### コンテンツ保存場所のルートディレクトリ（スタンドアロン環境） {#content-storage-root-location-stand-alone-environment}

Content Services（非推奨）のインストール時に、コンテンツ保存場所のルートディレクトリが作成されます。コンテンツ保存場所のルートディレクトリの場所は、AEM Forms のインストールプロセス中に決まります。

コンテンツ保存場所のルートディレクトリのデフォルトの場所は、`[aem-forms root]/lccs_data` です。

コンテンツ保存場所のルートディレクトリにある次のディレクトリをバックアップします。

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-indexes

/backup-lucene-indexes ディレクトリが存在しない場合、/lucene-indexes ディレクトリをバックアップします（コンテンツ保存場所のルートディレクトリにあります）。/backup-lucene-indexes ディレクトリが存在する場合、/lucene-indexes ディレクトリをバックアップしないでください。エラーが発生する可能性があります。

### コンテンツ保存場所のルートディレクトリ（クラスター環境） {#content-storage-root-location-clustered-environment}

クラスター環境に Content Services（非推奨）をインストールする場合、コンテンツ保存場所のルートディレクトリは次に示す 2 つの異なるディレクトリに分けられます。

**コンテンツ保存場所のルートディレクトリ：**&#x200B;通常、クラスター内のすべてのノードが読み取り／書き込みアクセス権を持つ共有ネットワークディレクトリです。

**インデックスのルートディレクトリ：**&#x200B;クラスター内の各ノードに作成されるディレクトリであり、常に同じパスおよびディレクトリ名を保持します。

コンテンツ保存場所のルートディレクトリのデフォルトの場所は `[GDS root]/lccs_data` です。`[GDS root]` は [GDS の場所](files-back-recover.md#gds-location)で説明されている場所です。コンテンツ保存場所のルートディレクトリにある次のディレクトリをバックアップします。

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-indexes

/backup-lucene-indexes ディレクトリが存在しない場合、/lucene-indexes ディレクトリをバックアップします（コンテンツ保存場所のルートディレクトリにあります）。/backup-lucene-indexes ディレクトリが存在する場合、/lucene-indexes ディレクトリをバックアップしないでください。エラーが発生する可能性があります。

インデックスルートディレクトリのデフォルトの場所は、各ノード上の `[aem-forms root]/lucene-indexes` です。

## ユーザーによるインストールフォント {#customer-installed-fonts}

AEM Forms 環境に追加のフォントをインストールした場合、それらのフォントを個別にバックアップする必要があります。管理コンソールの設定／コアシステム／設定で指定されている、ユーザーによるインストールフォントおよび Adobe フォントのディレクトリをすべてバックアップします。フォントディレクトリ全体をバックアップしてください。

>[!NOTE]
>
>デフォルトでは、AEM Forms と共にインストールされる Adobe Fonts は、 `[aem-forms root]/fonts` ディレクトリにあります。

ホストコンピューター上でオペレーティングシステムを再初期化し、以前のオペレーティングシステムのフォントを使用する場合、システムフォントディレクトリの内容もバックアップする必要があります（詳細な手順については、ご使用のオペレーティングシステムのマニュアルを参照してください）。
