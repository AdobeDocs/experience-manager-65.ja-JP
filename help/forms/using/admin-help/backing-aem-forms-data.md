---
title: Adobe Experience Manager Formsデータのバックアップ
description: このドキュメントでは、Adobe Experience Manager(AEM)forms データベース、GDS およびコンテンツ保存場所のルートディレクトリのホットバックアップ（オンラインバックアップ）を完了するために必要な手順について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 536615a4-ab42-4b72-83b1-fad110b011ee
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1533'
ht-degree: 10%

---

# Adobe Experience Manager(AEM)Formsデータのバックアップ {#backing-up-the-aem-forms-data}

<!-- back up is two words when used as a verb; backup is one word when used as an adjective or noun. -->

この節では、AEM Formsデータベース、GDS およびコンテンツ保存場所のルートディレクトリのホットバックアップ（オンラインバックアップ）を完了するために必要な手順について説明します。

AEM Formsをインストールして実稼動環境にデプロイした後は、データベース管理者がデータベースの初期フルバックアップ（コールドバックアップ）を実行する必要があります。 このバックアップを実行するには、データベースをシャットダウンする必要があります。 次に、データベースの差分バックアップまたは増分（またはホット）バックアップを定期的に実行する必要があります。

バックアップとリカバリを正常に行うには、システムイメージのバックアップを常に使用可能にしておく必要があります。 その後、損失が発生した場合は、環境全体を一貫性のある状態に回復できます。

GDS、AEMリポジトリ、およびコンテンツ保存場所のルートディレクトリのバックアップと同時にデータベースをバックアップすることで、回復が必要な場合に、これらのシステムを同期し続けることができます。

この節で説明するバックアップ手順では、AEM Formsデータベース、AEMリポジトリ、GDS、およびコンテンツ保存場所のルートディレクトリをバックアップする前に、セーフバックアップモードに入る必要があります。 バックアップが完了したら、セーフバックアップモードを終了する必要があります。 セーフバックアップモードは、GDS 内に存在する長期間有効な永続的なドキュメントをマークするために使用されます。 このモードでは、セーフバックアップモードが解放されるまで、自動ファイルクリーンアップメカニズム（ファイルコレクター）が期限切れのファイルを削除しないようにします。 GDS バックアップとデータベースバックアップの同期を維持する必要があります。

GDS の場所をバックアップする頻度は、AEM Formsの使用方法と使用可能なバックアップウィンドウによって異なります。 バックアップウィンドウは、数日間実行される可能性があるので、長期間有効なプロセスの影響を受ける場合があります。 このディレクトリ内のファイルを継続的に変更、追加、削除する場合は、GDS の場所をより頻繁にバックアップする必要があります。

前の節で説明したように、データベースがログ・モードで実行されている場合は、データベース・ログも頻繁にバックアップして、メディアの障害が発生した場合にデータベースのリストアに使用できるようにする必要があります。

>[!NOTE]
>
>参照されていないファイルは、回復プロセスの後で GDS ディレクトリに保持される場合があります。 これは、現在既知の制限です。

## データベース、GDS、AEMリポジトリおよびコンテンツ保存場所のルートディレクトリのバックアップ {#back-up-the-database-gds-aem-repository-and-content-storage-root-directories}

AEM Formsは、セーフバックアップ（スナップショット）モードまたはローリングバックアップ（継続的な有効範囲）モードのどちらかに設定する必要があります。 AEM Formsを設定していずれかのバックアップモードに入る前に、次の点を確認します。

* システムのバージョンを確認し、最後の完全なシステムイメージバックアップの実行後に適用されたパッチまたは更新を記録します。
* ローリングモードまたはスナップショットモードのバックアップを使用する場合は、データベースのホットバックアップを実行できるように、データベースに正しいログ設定が設定されていることを確認します。 ( 詳しくは、 [AEM Formsデータベース](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).)

これらに加えて、バックアップ/復元プロセスに関する次のガイドラインを確認します。

* 使用可能なオペレーティングシステムまたはサードパーティのバックアップユーティリティを使用して、GDS ディレクトリをバックアップします。 ( 詳しくは、 [GDS の場所](/help/forms/using/admin-help/files-back-recover.md#gds-location).)
* （オプション）使用可能なオペレーティングシステムまたはサードパーティのバックアップとユーティリティを使用して、コンテンツ保存場所のルートディレクトリをバックアップします。 ( 詳しくは、 [コンテンツ保存場所のルートの場所（スタンドアロン環境）](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-stand-alone-environment) または [コンテンツ保存場所のルートの場所（クラスター環境）](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-clustered-environment).)
* オーサーインスタンスとパブリッシュインスタンス（ crx -repository バックアップ）をバックアップします。

  Correspondence Management Solution 環境をバックアップするには、オーサーインスタンスとパブリッシュインスタンスで手順を実行します。詳しくは、 [バックアップと復元](/help/sites-administering/backup-and-restore.md).

  オーサーインスタンスとパブリッシュインスタンスをバックアップする際は、次の点を考慮してください。

   * オーサーインスタンスとパブリッシュインスタンスのバックアップが同時に開始するように同期されていることを確認します。 バックアップの実行中も引き続きオーサーインスタンスとパブリッシュインスタンスを使用できますが、キャプチャされていない変更を避けるために、バックアップ中にアセットを公開しないことをお勧めします。 オーサーインスタンスとパブリッシュインスタンスの両方のバックアップが終了するのを待ってから、新しいアセットを公開します。
   * オーサーノードの完全なバックアップには、Forms Manager とAEM Forms Workspace データのバックアップが含まれます。
   * Workbench 開発者は、引き続きローカルでプロセスを操作できます。 バックアップフェーズ中に新しいプロセスをデプロイしないでください。
   * 各バックアップセッションの長さに関する決定は、AEM Forms(DB、GDS、AEMリポジトリ、およびその他の追加のカスタムデータ ) 内のすべてのデータのバックアップに要した合計時間に基づいておこなう必要があります。

トランザクションログを含むAEM Formsデータベースをバックアップします。 詳しくは、 [AEM Formsデータベース](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).

詳細については、使用するデータベースに適したナレッジベースを参照してください。
<!-- The four URLs below are all 404s; checked July 19, 2023 -->
* [AEM Formsのoracleバックアップと回復](https://www.adobe.com/go/kb403624)
* [AEM Forms向け MySQL バックアップと回復](https://www.adobe.com/go/kb403625)
* [AEM Forms向けMicrosoft® SQL Server のバックアップと回復](https://www.adobe.com/go/kb403623)
* [AEM Forms向け DB2®バックアップと回復](https://www.adobe.com/go/kb403626)

これらの記事は、データのバックアップと回復に関する基本的なデータベース機能に関するガイダンスを提供します。 特定のベンダーのデータベースバックアップ/リカバリ機能に関する包括的な技術ガイドとしての意図はありません。 AEM Formsアプリケーションデータの信頼性の高いデータベースバックアップ戦略を作成するために必要なコマンドの概要を説明します。

>[!NOTE]
>
>GDS のバックアップを開始する前に、データベースのバックアップが完了している必要があります。 データベースのバックアップが完了していない場合、データは同期されていません。

### バックアップモードの開始 {#entering-the-backup-modes}

管理コンソール、LCBackupMode コマンド、またはAEM Formsインストールで使用可能な API を使用して、バックアップモードを開始および終了できます。 ローリングバックアップ（継続的な対象）の場合、管理コンソールオプションは使用できません。コマンドラインオプションまたは API を使用する必要があります。 <!-- Fix broken link For information about using the API to enter and leave backup modes, see AEM Forms API Reference on Help and Tutorials page. -->

>[!NOTE]
>
>Forms Server で SSL を設定した場合、LCBackupMode.CMD スクリプトを使用してForms Server をバックアップモードにすることはできません。

**管理コンソールを使用したセーフバックアップモードの開始**

1. 管理コンソールにログインします。
1. 設定/コアシステム設定/バックアップユーティリティをクリックします。
1. 「セーフバックアップモードで動作」を選択し、「OK」をクリックします。

   この方法では、AEM Formsは無期限（タイムアウトなし）にバックアップモードになり、ローリングバックアップモードではなくスナップショットモードになります。

**コマンドラインオプションを使用したセーフバックアップモードの開始**

コマンドラインインターフェイスを使用できます。 `LCBackupMode` AEM Formsをセーフバックアップモードにするためのスクリプト。

1. ADOBE_LIVECYCLE を設定し、アプリケーションサーバーを起動します。
1. `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline` フォルダーに移動します。
1. オペレーティングシステムに応じて、`LCBackupMode.cmd` または `LCBackupMode.sh` スクリプトを編集して、システムに適合するデフォルト値を指定します。
1. コマンドプロンプトで、次のコマンドを 1 行で実行します。

   * （Windows）`LCBackupMode.cmd enter [-Host=`*ホスト名* `] [-port=`*ポート番号* `] [-user=`*ユーザー名* `] [-password=`*パスワード* `] [-label=`*ラベル名* `] [-timeout=`*秒数* `]`
   * (Linux®、UNIX®) `LCBackupMode.sh enter [-host=`*hostname* `] [-port=`*portnumber* `] [-user=`*ユーザー名* `] [-password=`*パスワード* `] [-label=`*labelname* `]`

   上記のコマンドでは、プレースホルダーは次のように定義されています。

   `Host` は、AEM Formsが実行されているホストの名前です。

   `port` は、AEM Formsが実行されているアプリケーションサーバーの WebServices ポートです。

   `user` は、AEM Forms管理者のユーザー名です。

   `password` は、AEM Forms管理者のパスワードです。

   `label` は、このバックアップのテキストラベルです（任意の文字列を指定可能）。

   `timeout` は、バックアップモードが自動的に終了するまでの秒数です。0 ～ 10,080 の値を指定できます。 0 （デフォルト）の場合、バックアップモードはタイムアウトしません。

   バックアップモードへのコマンドラインインターフェイスの詳細については、BackupRestoreCommandline ディレクトリの Readme ファイルを参照してください。

### バックアップモードの終了 {#leaving-backup-modes}

バックアップモードを終了するには、管理コンソールまたはコマンドラインオプションを使用できます。

**セーフバックアップモード（スナップショットモード）を終了**

管理コンソールを使用してAEM Formsのセーフバックアップモード（スナップショットモード）を解除するには、次のタスクを実行します。

1. 管理コンソールにログインします。
1. 設定/コアシステム設定/バックアップユーティリティをクリックします。
1. 「セーフバックアップモードで動作」の選択を解除し、「OK」をクリックします。

**すべてのバックアップモードを終了**

コマンドラインインターフェイスを使用して、AEM Formsをセーフバックアップモード（スナップショットモード）から切り離したり、現在のバックアップモードセッション（ローリングモード）を終了したりできます。 管理コンソールを使用してローリングバックアップモードを終了することはできません。 ローリングバックアップモードの場合、管理コンソールの [ バックアップユーティリティ ] コントロールは無効になります。 API 呼び出しを使用するか、LCBackupMode コマンドを使用します。

1. `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline` フォルダーに移動します。
1. オペレーティングシステムに応じて、`LCBackupMode.cmd` または `LCBackupMode.sh` スクリプトを編集して、システムに適合するデフォルト値を指定します。

   >[!NOTE]
   >
   >JAVA_HOME ディレクトリを、アプリケーション・サーバーの適切な章 ( [AEM Formsのインストールの準備](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63_jp)*.*

1. 次のコマンドを 1 行で実行します。

   * （Windows）`LCBackupMode.cmd leaveContinuousCoverage [-Host=`*ホスト名* `] [-port=`*ポート番号* `] [-user=`*ユーザー名* `] [-password=`*パスワード* `]`
   * (Linux®、UNIX®) `LCBackupMode.sh leaveContinuousCoverage [-Host=`*hostname* `] [-port=`*portnumber* `] [-user=`*ユーザー名* `] [-password=`*パスワード* `]`

     上記のコマンドでは、プレースホルダーは次のように定義されています。

     `Host` は、AEM Formsが実行されているホストの名前です。

     `port` は、アプリケーションサーバー上でAEM Formsが動作しているポートです。

     `user` は、AEM Forms管理者のユーザー名です。

     `password` は、AEM Forms管理者のパスワードです。

     `leaveContinuousCoverage` は、ローリングバックアップモードを完全に無効にする場合に使用します。

   >[!NOTE]
   >
   >バックアップモードがオフの場合は、継続的なカバレッジを再確立できません。 その間の変更は保護されません。

   >[!NOTE]
   >
   >データベースでドキュメントの保存を有効にした場合、スナップショットバックアップモードとローリングバックアップモードは使用できません。

   バックアップモードへのコマンドラインインターフェイスの詳細については、BackupRestoreCommandline ディレクトリの readme ファイルを参照してください。
