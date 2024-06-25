---
title: EMC Documentum リポジトリのバックアップと回復
description: ここでは、AEM Forms 環境用に設定された EMC Documentum リポジトリをバックアップおよび回復するために必要なタスクについて説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: bc21659f-88d6-4dff-8baf-12746e1b3ed9
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: ht
source-wordcount: '790'
ht-degree: 100%

---

# EMC Documentum リポジトリのバックアップと回復 {#backing-up-and-recovering-the-emc-documentum-repository}

ここでは、AEM Forms 環境用に設定された EMC Documentum リポジトリをバックアップおよび回復するために必要なタスクについて説明します。

>[!NOTE]
>
>これらの手順は、AEM Forms と Connectors for ECM および EMC Documentum Content Server が、必要に応じてインストールされ、設定されていることを前提としています。

バックアッププロセスにも復元プロセスにも、2 つの主要なタスクがあります。

* AEM Forms 環境のバックアップ（または復元）。
* EMC Documentum Content Server のバックアップ（または復元）。

>[!NOTE]
>
>EMC Documentum システムをバックアップする前に AEM Forms データをバックアップし、続いて、EMC Documentum システムを復元してから AEM Forms 環境を復元します。

## ソフトウェア要件 {#software-requirements}

必要なバックアップタスクを EMC Documentum Content Server で実行するために、EMC の EMC NetWorker または CYA の CYA SmartRecovery for EMC Documentum などの適切なサードパーティのユーティリティを購入します。次の手順では、EMC NetWorker Module バージョン 7.2.2 を使用する操作について説明します。

次の EMC NetWorker モジュールを使用する必要があります。

* NetWorker モジュール
* NetWorker 設定ウィザード
* NetWorker デバイス設定ウィザード
* Content Server で使用するデータベースタイプ用の NetWorker モジュール
* Documentum 用 NetWorker モジュール

## EMC Document Content Server のバックアップおよび復元の準備 {#preparing-the-emc-document-content-server-for-backup-and-recovery}

ここでは、EMC NetWorker ソフトウェアを Content Server にインストールおよび設定する方法について説明します。

**EMC Documentum サーバーのバックアップ用の準備**

1. EMC Documentum Content Server で、すべてのデフォルトを受け入れて EMC NetWorker モジュールをインストールします。

   インストールプロセス中、「*NetWorker Server Name*」として Content Server コンピューターのサーバー名の入力を求められます。EMC NetWorker Module をデータベース用にインストールする場合は、「完全」インストールを選択します。

1. 以下のサンプルコンテンツを使用して、*nsrnmd_win.cfg* という名前の設定ファイルを作成し、Content Server 上のアクセス可能な位置に保存します。このファイルは、バックアップおよび復元コマンドによって呼び出されます。

   次のテキストには、レイアウトのために 1 行が分割されている部分があります。そのため、このテキストをこのドキュメント以外の場所にコピーする場合は、1 ブロックずつコピーし、ペーストしたテキストから不要な改行を削除してください。

   ```shell
    ################################################
    # NetWorker Module for Documentum v1.2 nsrnmd_win.cfg D5.3+ example with
    # typical set of working parameters.  THIS FILE MUST BE SITE-CUSTOMISED.
    #
    # Parameters not shown can be set in this file (as per site customisation) #or from the command-line.
    #
    # See the user Guides for details on all parameters, including
    # those not listed below.
    # Note: DCTM environment for D6 is slightly different from D5, refer to D6
    # Installation Guide to update the values.
    ################################################
    #Can get values for most of below from doing as the dctm inst owner: cmd> set DOCUMENTUM=C:\Documentum
    DM_HOME=C:\Documentum\product\6.0
    JAVA_HOME=C:\Progra~1\Documentum\java\1.5.0_12
    JAVA_PATH=C:\Progra~1\Documentum\java\1.5.0_12\bin
    PATH=C:\WINNT\system32;C:\WINNT;C:\WINNT\system32\WBEM;C:\Documentum\product\6.0\bin;C:\Documentum\fulltext\fast;C:\Documentum\product\6.0\fusion;C:\Program Files\Documentum\Shared;C:\Program Files\Legato\nsr\bin;C:\Program Files\Microsoft SQL Server\80\Tools\Binn;C:\Program Files\Microsoft SQL Server\90\DTS\Binn\;C:\Program Files\Microsoft SQL Server\90\Tools\binn;C:\Program Files\Microsoft SQL Server\90\Tools\Binn\VSShell\Common7\IDE;C:\Program Files\Documentum\java\1.5.0_12\bin;C:\Documentum\config;C:\Documentum
    #See also manifest dctm.jar file for class path locations
    CLASSPATH=.;C:\Program Files\Legato\nsr\bin;C:\Program Files\Legato\nsr\bin\nsrnmdde.jar;C:\Program Files\Documentum\java\1.5.0_12\lib\tools.jar;C:\Program Files\Documentum\Shared\dfc.jar;C:\Program Files\Documentum\Shared\aspectjrt.jar;C:\Program Files\Documentum\dctm.jar;C:\Program Files\Documentum\Shared\workflow.jar;C:\Program Files\Documentum\Shared\log4j.jar;C:\Program Files\Documentum\java\1.5.0_12\lib\dt.jar;C:\Documentum\config
   
    ################################################
    #If not using nsrnmdsv -m ALL|DB|DB_LOG|FTI|FTI_ALL|ICF|SA|SA_ALL, set #for backup
    NMD_SCOPE=ALL
    #Mandatory when scope (backup or restore) is FTI/SA without -a option
    #NMD_OBJECT_NAME=filestore_01
    ################################################
    NMDDE_DM_DOCBASE=Docbase
    NMDDE_DM_USER=Administrator
    #NMDDE_DM_PASSWD must be set via running: nsrnmdsv -f <nmdcfg> -P <pwd>.
    ################################################
    #DB related hooks to invoke arbitrary scripts:
    #Set if DB is on a remote host
    #NMD_DB_HOST=dbhost
    #Pure basename implies remote host execution; absolute path ... local
    #execution as in NMD v1.0.
    #
    #Remote execution requires script be put in remote nsrexecd bin directory
    #and D5.3+ host be added to remote nsr\res\servers file w/ nsrexecd recycled
    #
    #Refer to user Guides for sample script code.
    NMD_DB_FULL_BACKUP_CMD=C:\DocumentumBackup\Scripts\nsrnmddbf.bat
    NMD_DB_LOG_BACKUP_CMD=C:\DocumentumBackup\Scripts\nsrnmddbl.bat
    NMD_DB_INCR_BACKUP_CMD=C:\DocumentumBackup\Scripts\nsrnmddbi.bat
    ################################################
    #For D5.3+ only: NMD_FTI_INCLUDED, NMD_FTI_HOST, NMD_FTI_USER,
    #NMD_FTI_PASSWD & NMD_FTI_SUBDIRS.
    #Optional for remote D5.3+ FTI server
    NMD_FTI_INCLUDED=no
    #NMD_FTI_HOST=ftihost
    #Recommended for D5.3+ FTI server quiesce/unquiesce
    #NMD_FTI_USER=ftiadmin
    #The index name: optional for D5.3+ FTI server, used with -M FTI_ALL or
    #-M ALL
    #NMD_FTI_NAME=rep_name_ftindex_01
    #Recommended for D5.3+ FTI server quiesce/unquiesce
    #NMDDE_FTI_PASSWD must be set via running: nsrnmdsv -f <nmdcfg> -P <pwd>
    #-M FTI.
    #Pure basename implies remote host execution; absolute path ... local execution
    #as in NMD v1.0.
    #
    #Remote execution requires script be put in remote nsrexecd bin directory
    #and D5.3+ host be added to remote nsr\res\servers file w/ nsrexecd
    #recycled.
    #
    #See example nsrnmdfti*.bat examples.
    #
    #Mandatory for D5.3+
    #NMD_BACKUP_FTI_QUIESCE=nsrnmdftiq.bat
    #NMD_BACKUP_FTI_UNQUIESCE=nsrnmdftiu.bat
    #Used for D5.3+ to get InstallProfile.xml FTI file in multinode
    #discovery.
    #Optional, if not specified, will treat as single-node FTI.
    #NMD_FTI_GET_INSTPROF=nsrnmdfti_instprof.bat
    #Mandatory for D5.3+. No spaces in paths or around comma separators.
    #For remote FTI, paths must be valid at the FTI host.
    #NMD_FTI_SUBDIRS=F:\Documentum_idx\data\fulltext\fixml,F:\Documentum_idx
    #\data\fulltext\index
    ################################################
    #Mandatory. No spaces in paths or before comma
    #separators in NMD_ICF_SUBDIRS_xxx:
    #NMD_ICF_INCLUDED=yes
    #NMD_ICF_SUBDIRS=C:\Documentum\dba,C:\Documentum\product\5.3
    ################################################
    NMD_FILEREPORT_INCLUDED=yes
    NMDDE_METADATA_OUTPUT_DEST=C:\docbase_freports\
    ################################################
    #Other misc recommended NMD_xxx parameters
    #Recommended to get more meaningful saveset names
    NMD_USE_DEFAULT_SAVESET_NAMES=yes
    #Use following to skip unwanted ICF, FTI and non-SnapImage SA dirs/files.
    #For example, "<</>> +skip: dm_ftwork_dir" line will skip non-data
    #files.
    #
    #The path will be the same and must exist on D5.3+, remote FTI host, and
    #RCS hosts correspondingly if used.
    #NMD_DIRECTIVES_FILE=E:\Program Files\Legato\nsr\res\nsrnmddirectives.txt
    #For non-SnapImage SA backup
    #NMD_SA_FULL_NUM_SAVESET=16
    #NMD_SA_INCR_NUM_SAVESET=4
    #NMD_USE_SNAPIMAGE=yes
    ################################################
    # DSA setup
    ################################################
    # Name of the config file at the remote sites;
    # Mandatory, listed in the config file at the primary host.
    # (if skipped, backup is treated as local)
    # NMD_RCS_CFG_FILE=rep_name_rcs.cfg
   
    # SA-host mapping add, optional, will override far-store list info.
    # No space around comma.
    # NMD_HOST_SAS_MAP=host01,sa_01,sa_02
    # NMD_HOST_SAS_MAP=host02,sa_03
    ################################################
    NSR_SERVER=con-dctm
    #NSR_CLIENT=d5svrhost
    NSR_GROUP=Default
    NSR_DATA_VOLUME_POOL=Default
    #NSR_SNAPIMAGE_DATA_VOLUME_POOL=Default
    #Relocation dir will be the same on D5+ and remote FTI/SA hosts.
    NSR_RELOCATION=C:\reloc
    #NSR_PARALLELISM=16
    NSR_DEBUG_FILE=C:\Program Files\Legato\nsr\applogs\nmd.log
    NSR_DEBUG_LEVEL=9
    ################################################
    NMDDE_DM_PASSWD=XAtup9pl
   ```

   設定ファイルのパスワードフィールド `NMDDE_DM_PASSWD` は、空白のままにします。パスワードは次の手順で設定します。

1. 設定ファイルのパスワードを、次のように設定します。

   * コマンドプロンプトを開き、`[NetWorker_root]\Legato\nsr\bin` に変更します。
   * 次のコマンドを実行します： `-nsrnmdsv.exe -f`*&lt;path_to_cfg_file> -P &lt;password>*

1. データベースのバックアップに使用する実行可能なバッチファイル（.bat）を作成します（NetWorker のドキュメントを参照）。インストールされている状態に応じて、バッチファイルの詳細を設定します。

   * 完全なデータベースバックアップ（nsrnmddbf.bat）：

     `NetWorker_database_module_root` `-s`*&lt;NetWorker_Server_Name>* `-U``[username]` `-P`*[password ]*`-l full`*&lt;database_name>*

   * 増分データベースバックアップ（nsrnmddbi.bat）：

     `[NetWorker_database_module_root]` `-s`*&lt;NetWorker_Server_Name>* `-U``[username]` `-P``[password]` `-l 1 -R`*&lt;database_name>*

   * データベースログバックアップ（nsrnmddbl.bat）： 

     `[NetWorker_database_module_root]` `-s``<NetWorker_Server_Name>` `-U``[username]` `-P``[password]` `-l incr -R`*&lt;database_name>*

     ここで、

     `[NetWorker_database_module_root]` は NetWorker モジュールのインストールディレクトリです。例えば、NetWorker Module for SQL Server のデフォルトのインストールディレクトリは、C:¥Program Files¥Legato¥nsr¥bin¥nsrsqlsv です。

     `NetWorker_Server_Name` は、NetWorker がインストールされているサーバーです。

     `username` と `password` は、データベース管理者ユーザーのユーザー名とパスワードです。

     `database_name` は、バックアップするデータベースの名前です。

**バックアップデバイスの作成**

1. EMC Documentum サーバーにディレクトリを作成し、すべてのユーザーに完全な権限を与えることによってフォルダーを共有します。
1. EMC NetWorker Administrator を起動し、Media Management／Devices をクリックします。
1. 「デバイス」を右クリックし、「作成」を選択します。
1. 次の値を入力し、「OK」をクリックします。

   **Name：**&#x200B;共有ディレクトリのフルパス

   **メディアタイプ：** `File`

1. 新しいデバイスを右クリックして、「操作」をクリックします。
1. 「ラベル」を選択し、名前を入力して、「OK」、「マウント」の順にクリックします。

バックアップファイルが保存されるデバイスが追加されます。複数のデバイスを様々な形式で追加することができます。

## EMC Documentum Content Server のバックアップ {#back-up-the-emc-documentum-content-server}

AEM Forms データの完全バックアップを完了してから、以下のタスクを実行します（[AEM Forms データのバックアップ](/help/forms/using/admin-help/backing-aem-forms-data.md#backing-up-the-aem-forms-data)を参照）。

>[!NOTE]
>
>コマンドスクリプトには、[EMC Document Content Server のバックアップおよび復元の準備](backing-recovering-emc-documentum-repository.md#preparing-the-emc-document-content-server-for-backup-and-recovery)で作成した nsrnmd_win.cfg ファイルへのフルパスが必要です。

1. コマンドプロンプトを開き、`[NetWorker_root]\Legato\nsr\bin` に変更します。
1. 次のコマンドを実行します。

   ```shell
    - nsrnmdsv.exe -f <path_to_cfg_file>
   ```

## EMC Documentum Content Server の復元 {#restore-the-emc-documentum-content-server}

以下のタスクを実行してから、AEM Forms データを復元します（[AEM forms データの回復](/help/forms/using/admin-help/recovering-aem-forms-data.md#recovering-the-aem-forms-data)を参照）。

>[!NOTE]
>
>コマンドスクリプトには、[EMC Document Content Server のバックアップおよび復元の準備](backing-recovering-emc-documentum-repository.md#preparing-the-emc-document-content-server-for-backup-and-recovery)で作成した nsrnmd_win.cfg ファイルへのフルパスが必要です。

1. 復元する Docbase サービスを停止します。
1. データベースモジュール用の NetWorker User ユーティリティを起動します（例えば、「*NetWorker User for SQL Server*」）。
1. Restore ツールをクリックし、「Normal」をクリックします。
1. 画面の左側で、Docbase のデータベースを選択し、ツールバーの「Start」ボタンをクリックします。
1. データベースが復元されたら、Docbase サービスを再起動します。
1. コマンドプロンプトを開き、*[NetWorker_root]*\Legato\nsr\bin に変更します。
1. 次のコマンドを実行します。

   ```shell
    - nsrnmdrs.exe -B <docbase_name> -f <path_to_cfg_file> -C SA
   ```
