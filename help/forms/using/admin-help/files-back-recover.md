---
title: バックアップおよび回復するファイル
description: このドキュメントでは、バックアップする必要のあるアプリケーションとデータファイルについて説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: d2dd381d-a7d2-4fec-a8ba-7ca037fd9dc1
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '2017'
ht-degree: 13%

---

# バックアップおよび回復するファイル {#files-to-back-up-and-recover}

バックアップが必要なアプリケーションとデータ・ファイルについては、以降のセクションで詳しく説明します。

バックアップとリカバリに関して、次の点を考慮します。

* データベースは、GDS およびAEMリポジトリの前にバックアップする必要があります。
* バックアップのためにクラスター環境内でノードを下げる必要がある場合は、セカンダリノードをプライマリノードの前にシャットダウンしてください。そうしないと、クラスターまたはサーバー内で一貫性がなくなる可能性があります。また、プライマリノードはすべてのセカンダリノードよりも前にライブにする必要があります。
* クラスタの復元操作の場合、クラスタ内の各ノードに対してアプリケーションサーバを停止する必要があります。

## グローバルドキュメントストレージディレクトリ {#global-document-storage-directory}

GDS は、プロセス内で使用される長期間有効なファイルの保存に使用されるディレクトリです。 長期間有効なファイルの有効期間は、AEM forms システムの 1 つ以上の起動にまたがることを目的としており、日数と年数を超える場合もあります。 長期間有効なファイルには、PDF、ポリシー、フォームテンプレートが含まれる場合があります。 長期間有効なファイルは、多くのAEM forms デプロイメントの全体的な状態の重要な部分です。 長期間有効なドキュメントの一部またはすべてが失われたり破損したりした場合は、Forms Server が不安定になる可能性があります。

非同期ジョブの呼び出し用の入力ドキュメントも GDS に保存されます。要求の処理には、このドキュメントを使用できる必要があります。 したがって、GDS をホストするファイルシステムの信頼性を考慮し、品質とサービスレベルの要件に応じて、RAID(Redundant Array of Independent Disks) やその他のテクノロジーを適切に使用することが重要です。

GDS の場所は、AEM forms のインストールプロセス中に決定されるか、後で管理コンソールを使用して決定されます。 GDS の高可用性の場所を維持するだけでなく、ドキュメントのデータベースストレージを有効にすることもできます。 詳しくは、 [データベースをドキュメントストレージに使用する場合のバックアップオプション](files-back-recover.md#backup-options-when-database-is-used-for-document-storage).

### GDS の場所 {#gds-location}

インストール時に場所の設定を空のままにした場合、アプリケーションサーバーのインストール下のディレクトリがデフォルトの場所になります。 アプリケーションサーバーの次のディレクトリをバックアップします。

* (JBoss) `[appserver root]/server/'server'/svcnative/DocumentStorage`
* (WebLogic) `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage`
* (WebSphere) `[appserver root]/installedApps/adobe/'server'/DocumentStorage`

GDS の場所をデフォルト以外の場所に変更した場合は、次のように決定できます。

* 管理コンソールにログインし、設定/コアシステム設定/設定をクリックします。
* 「グローバルドキュメントストレージディレクトリ」ボックスで指定した場所を記録します。

クラスター環境では、通常、GDS はネットワーク上で共有されるディレクトリを指し、すべてのクラスターノードに対して読み取り/書き込みアクセス可能です。

元の場所が使用できなくなった場合、回復中に GDS の場所が変更される可能性があります。 ( 詳しくは、 [回復中の GDS の場所の変更](/help/forms/using/admin-help/recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).)

### データベースをドキュメントストレージに使用する場合のバックアップオプション {#backup-options-when-database-is-used-for-document-storage}

管理コンソールを使用して、AEM forms データベースでAEM forms ドキュメントの保存を有効にすることができます。 このオプションを選択すると、すべての永続的なドキュメントがデータベースに保持されますが、AEM forms では、AEM forms のセッションや呼び出しに関連する永続的なファイルやリソースを保存するために、ファイルシステムベースの GDS ディレクトリが必要です。

管理コンソールの「コアシステム設定」、または Configuration Manager を使用して「データベースへのドキュメントの保存を有効にする」オプションを選択すると、AEM Forms ではスナップショットバックアップモードおよびローリングバックアップモードが許可されません。したがって、AEM forms を使用してバックアップモードを管理する必要はありません。 このオプションを使用する場合、このオプションを有効にした後、1 回だけ GDS をバックアップする必要があります。 バックアップからAEM forms を回復する場合、GDS のバックアップディレクトリの名前を変更したり、GDS を復元したりする必要はありません。

## AEMリポジトリ {#aem-repository}

AEM forms のインストール中に crx-repository が設定されている場合は、AEMリポジトリ (crx-repository) が作成されます。 crx-repository ディレクトリの場所は、AEM forms のインストールプロセス中に決定されます。 AEM forms で一貫性のあるAEM forms データを使用するには、AEMリポジトリのバックアップと復元が、データベースおよび GDS と共に必要です。 AEMリポジトリには、Correspondence Management Solution、Forms Manager、AEM Forms Workspace のデータが含まれます。

### Correspondence Management Solution {#correspondence-management-solution}

Correspondence Management Solution は、安全でパーソナライズされたインタラクティブな通信の作成、アセンブリ、および配信を一元化および管理します。 これにより、作成からアーカイブに至るまで、合理化されたプロセスで、承認済みコンテンツとカスタム作成コンテンツの両方から通信を迅速に組み立てることができます。 その結果、顧客はタイムリーで正確で便利で安全で関連性の高いコミュニケーションを取ることができます。 簡単、迅速、生産性を実現するために合理化されたプロセスを使用して、顧客とのやり取りの価値を最大限にし、コストとリスクを最小限に抑えます。

シンプルな Correspondence Management Solution のセットアップには、同じマシンまたは異なるマシン上に、オーサーインスタンスとパブリッシュインスタンスが含まれます。

### Forms Manager {#forms-manager}

forms manager は、フォームの更新、管理、および削除のプロセスを合理化します。

### AEM Forms Workspace {#html-workspace}

AEM Forms Workspace は、(JEE 上のAEM forms では廃止 )Flex Workspace の機能と一致し、Workspace を拡張および統合してより使いやすくする新しい機能を追加します。

>[!NOTE]
>
>AEM Forms のリリースでは Flex Workspace は廃止されています。

これにより、Flash PlayerやAdobe Readerを使用しないクライアントでタスクを管理できます。 PDF formsやFlexフォームに加えて、HTMLFormsのレンディションを容易にします。

## AEM forms データベース {#aem-forms-database}

AEM forms データベースには、フォームアーティファクト、サービス設定、プロセス状態、GDS 内のファイルへのデータベース参照（Content Services 用）などのコンテンツが格納されます。 データベースのバックアップは、サービスを中断することなく、リアルタイムで実行でき、特定の時点または特定の変更に対してリカバリを実行できます。 この項では、データベースをリアルタイムでバックアップできるように構成する方法について説明します。

適切に設定されたAEM forms システムでは、システム管理者とデータベース管理者が簡単に連携して、システムを一貫性のある既知の状態に回復できます。

データベースをリアルタイムでバックアップするには、スナップショットモードを使用するか、指定したログモードで実行するようにデータベースを構成する必要があります。 これにより、データベースが開かれ、使用可能な状態で、データベースファイルをバックアップできます。 さらに、データベースは、これらのモードで実行されているときに、ロールバックとトランザクション・ログを保持します。

>[!NOTE]
>
>Adobe®LiveCycle® Content Services ES（非推奨）は、LiveCycleと共にインストールされるコンテンツ管理システムです。 これにより、ユーザーは人間中心のプロセスを設計、管理、監視、最適化できます。 Content Services（非推奨）のサポートは12/31/2014で終了します。 [アドビ製品のライフサイクルに関するドキュメント](https://www.adobe.com/support/products/enterprise/eol/eol_matrix.html?lang=ja)を参照してください。

### DB2 {#db2}

DB2 データベースをアーカイブログモードで実行するように設定します。

>[!NOTE]
>
AEM forms 環境が以前のバージョンのAEM forms からアップグレードされ、DB2 を使用している場合、オンラインバックアップはサポートされません。 この場合、AEM forms をシャットダウンし、オフラインバックアップを実行する必要があります。 今後のバージョンのAEM Forms では、アップグレード版のお客様向けのオンラインバックアップをサポートする予定です。

IBMには、データベース管理者がバックアップ/リカバリタスクを管理するのに役立つ、一連のツールとヘルプシステムが用意されています。

* IBM DB2 Archive Log Accelerator
* IBM DB2 Data Archive エキスパート

DB2 には、Tivoli Storage Manager にデータベースをバックアップする組み込み機能が備わっています。 Tivoli Storage Manager を使用すると、DB2 バックアップを他のメディアまたはローカルハードドライブに保存できます。

### Oracle {#oracle}

スナップショットバックアップを使用するか、Oracle・データベースをアーカイブ・ログ・モードで実行するように構成します。 ( 詳しくは、 [Oracleバックアップ：はじめに](https://www.databasedesign-resource.com/oracle-backup.md).) oracle・データベースのバックアップとリカバリの詳細については、次のサイトを参照してください。

[Oracleのバックアップとリカバリ：](https://www.oracle.com/technetwork/database/features/availability/br-overview-097160.html) バックアップと回復の概念、および Recovery Manager (RMAN) を使用したバックアップ、回復、レポート作成の最も一般的な方法について詳しく説明し、バックアップと回復戦略の計画方法の詳細を示します。

[Oracle・データベース・バックアップ/リカバリ・ユーザー・ガイド：](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10642.pdf) RMAN のアーキテクチャ、バックアップと回復の概念とメカニズム、ポイント・イン・タイム・リカバリやデータベース・フラッシュバック機能などの高度なリカバリ手法、バックアップとリカバリのパフォーマンス・チューニングに関する詳細情報を提供します。 また、RMAN の代わりにホストオペレーティングシステムの機能を使用して、ユーザーが管理するバックアップとリカバリについても説明します。 このボリュームは、より高度なデータベース展開のバックアップとリカバリ、および高度なリカバリシナリオに不可欠です。

[Oracle・データベースのバックアップ/リカバリ・リファレンス：](https://download.oracle.com/docs/cd/E11882_01/backup.112/e10643.pdf) すべての RMAN コマンドの構文とセマンティクスに関する完全な情報を提供し、バックアップと回復アクティビティのレポートに使用できるデータベースビューについて説明します。

### SQL Server {#sql-server}

スナップショットバックアップを使用するか、SQL Server データベースをトランザクションログモードで実行するように構成します。

また、SQL Server には、次の 2 つのバックアップ/リカバリ・ツールが用意されています。

* SQL Server Management Studio (GUI)
* T-SQL（コマンドライン）

詳しくは、[バックアップと復元](https://msdn.microsoft.com/en-us/library/ms187048(v=SQL.90).aspx)を参照してください。

### MySQL {#mysql}

MySQLAdmin を使用するか、Windows で INI ファイルを変更して、MySQL データベースをバイナリログモードで実行するように構成します。 ( 詳しくは、 [MySQL バイナリログ](https://dev.mysql.com/doc/refman/5.1/en/binary-log.html).) MySQL 用のホットバックアップツールは、InnoBase ソフトウェアからも入手できます。 ( 詳しくは、 [Innobase ホットバックアップ](https://www.innodb.com/hot-backup/features.md).)

>[!NOTE]
>
MySQL のデフォルトのバイナリログモードは「Statement」です。このモードでは、Content Services（非推奨）で使用されるテーブルとの互換性がありません。 このデフォルトモードでバイナリログを使用すると、Content Services（非推奨）が失敗します。 システムに Content Services（非推奨）が含まれている場合は、「混在」ログモードを使用します。 「混在」ログを有効にするには、my.ini ファイルに次の引数を追加します。 `binlog_format=mixed log-bin=logname`

mysqldump ユーティリティを使用して、完全なデータベースバックアップを取得できます。 フル・バックアップが必要ですが、常に便利とは限りません。 大きなバックアップファイルを作成し、生成に時間がかかります。 増分バックアップを実行する場合は、前の節で説明したように `log-bin` オプションを使用してサーバーを起動してください。MySQL サーバーが再起動するたびに、現在のバイナリログへの書き込みが停止し、新しいログが作成され、以降はそのログが現在のバイナリログになります。`FLUSH LOGS SQL` コマンドを使用すると、手動で強制的に切り替えることができます。最初の完全バックアップ後の増分バックアップは、mysqladmin ユーティリティと `flush-logs` コマンドを使用して実行されます。これにより新しいログファイルが作成されます。

詳しくは、 [バックアップ戦略の概要](https://dev.mysql.com/doc/refman/5.5/en/backup-strategy-summary.html).

```text
binlog_format=mixed
log-bin=logname
```

## コンテンツ保存場所のルートディレクトリ（Content Services のみ） {#content-storage-root-directory-content-services-only}

コンテンツ保存場所のルートディレクトリには、すべてのドキュメント、アーティファクト、インデックスが保存される Content Services（非推奨）リポジトリが含まれます。 コンテンツ保存場所のルートディレクトリツリーをバックアップする必要があります。 この節では、スタンドアロン環境とクラスター環境の両方でコンテンツ保存場所のルートディレクトリの場所を決定する方法について説明します。

### コンテンツ保存場所のルートの場所（スタンドアロン環境） {#content-storage-root-location-stand-alone-environment}

コンテンツ保存場所のルートディレクトリは、Content Services（非推奨）のインストール時に作成されます。 コンテンツ保存場所のルートディレクトリの場所は、AEM forms のインストールプロセス中に決定されます。

コンテンツ保存場所のルートディレクトリのデフォルトの場所は、`[aem-forms root]/lccs_data` です。

コンテンツ保存場所のルートディレクトリにある次のディレクトリをバックアップします。

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-indexes

/backup-lucene-indexes ディレクトリが存在しない場合は、/lucene-indexes ディレクトリをバックアップします。また、コンテンツ保存場所のルートディレクトリにもバックアップします。 /backup-lucene-indexes ディレクトリが存在する場合は、/lucene-indexes ディレクトリをバックアップしないでください。エラーが発生する可能性があります。

### コンテンツ保存場所のルートの場所（クラスター環境） {#content-storage-root-location-clustered-environment}

クラスター環境に Content Services（非推奨）をインストールすると、コンテンツ保存場所のルートディレクトリは次の 2 つの異なるディレクトリに分割されます。

**コンテンツ保存場所のルートディレクトリ：** 通常、クラスター内のすべてのノードに対して読み取り/書き込みアクセス可能な共有ネットワークディレクトリ

**インデックスのルートディレクトリ：** クラスター内の各ノードに作成され、常に同じパスとディレクトリ名を持つディレクトリ

コンテンツ保存場所のルートディレクトリのデフォルトの場所は `[GDS root]/lccs_data` です。`[GDS root]` は [GDS の場所](files-back-recover.md#gds-location)で説明されている場所です。コンテンツ保存場所のルートディレクトリにある次のディレクトリをバックアップします。

/audit.contentstore

/contentstore

/contentstore.deleted

/backup-lucene-indexes

/backup-lucene-indexes ディレクトリが存在しない場合は、/lucene-indexes ディレクトリをバックアップします。また、コンテンツ保存場所のルートディレクトリにもバックアップします。 /backup-lucene-indexes ディレクトリが存在する場合は、/lucene-indexes ディレクトリをバックアップしないでください。エラーが発生する可能性があります。

インデックスルートディレクトリのデフォルトの場所は、各ノード上の `[aem-forms root]/lucene-indexes` です。

## ユーザーがインストールしたフォント {#customer-installed-fonts}

AEM forms 環境に追加のフォントをインストールした場合は、それらのフォントを個別にバックアップする必要があります。 管理コンソールの設定/コアAdobe/設定で指定されている、システムおよび顧客のフォントのディレクトリをすべてバックアップします。 フォントディレクトリ全体をバックアップしてください。

>[!NOTE]
>
デフォルトでは、AEM forms と共にインストールされるAdobeフォントは、 `[aem-forms root]/fonts` ディレクトリ。

ホストコンピューター上のオペレーティングシステムを再初期化し、以前のオペレーティングシステムのフォントを使用する場合は、システムフォントディレクトリの内容もバックアップする必要があります。 （具体的な手順については、ご使用のオペレーティングシステムのドキュメントを参照してください）。
