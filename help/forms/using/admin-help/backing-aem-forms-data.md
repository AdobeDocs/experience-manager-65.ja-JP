---
title: AEM Forms データのバックアップ
seo-title: AEM Forms データのバックアップ
description: ここでは、AEM Forms データベース、GDS およびコンテンツ保存場所のルートディレクトリのホットバックアップ（オンラインバックアップ）の実行に必要な手順を説明します。
seo-description: ここでは、AEM Forms データベース、GDS およびコンテンツ保存場所のルートディレクトリのホットバックアップ（オンラインバックアップ）の実行に必要な手順を説明します。
uuid: ac7856be-e3b7-4b81-b8b9-fc909b5907b4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 52187196-b091-4683-85ae-cc7c250dee54
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1573'
ht-degree: 93%

---


# AEM Forms データのバックアップ {#backing-up-the-aem-forms-data}

ここでは、AEM Forms データベース、GDS およびコンテンツ保存場所のルートディレクトリのホットバックアップ（オンラインバックアップ）の実行に必要な手順を説明します。

AEM Forms がインストールされ、実稼働環境にデプロイされたら、データベース管理者はデータベースの初期完全バックアップ（コールドバックアップ）を実行する必要があります。このバックアップの場合は、データベースをシャットダウンする必要があります。その後、データベースの差分バックアップまたは増分（ホット）バックアップを定期的に行う必要があります。

バックアップと回復を正常に実行するには、システムイメージバックアップを常に使用可能にしておく必要があります。このようにすると、損失が発生した場合、環境全体を一貫性のある状態に回復できます。

GDS、AEM リポジトリ、およびコンテンツ保存場所のルートディレクトリのバックアップと同時にデータベースをバックアップすることで、回復が必要な場合にこれらのシステムを同期しておくことができます。

この節で説明するバックアップ手順では、AEM Forms データベース、AEM レポジトリ、GDS およびコンテンツ保存場所のルートディレクトリをバックアップする前にセーフバックアップモードにする必要があります。バックアップが完了したら、セーフバックアップモードを終了する必要があります。セーフバックアップモードは、GDS 内にある長期間有効なドキュメントと永続ドキュメントにマークを付けるために使用します。このモードによって、セーフバックアップモードが解放されるまで、自動化されたファイルのクリーンアップメカニズム（ファイルコレクター）によって有効期限の切れたファイルが削除されなくなります。GDS バックアップとデータベースバックアップの同期を維持する必要があります。

GDS の場所をバックアップする頻度は、AEM Forms の使用方法と使用可能なバックアップウィンドウに応じて異なります。バックアップウィンドウは、数日間実行される可能性のある長期間有効なプロセスの影響を受ける場合があります。このディレクトリ内のファイルを継続して変更、追加および削除する場合は、GDS の場所をより頻繁にバックアップするようにしてください。

データベースが前の節で説明したログモードで実行されている場合、データベースログを頻繁にバックアップして、メディアの障害が発生したときにデータベースの復元に使用できるようにすることが必要です。

>[!NOTE]
>
>参照されていないファイルは、回復プロセスの後に GDS ディレクトリ内で維持されます。これは、現在の既知の制限です。

## データベース、GDS、AEM リポジトリ、およびコンテンツ保存場所のルートディレクトリのバックアップ  {#back-up-the-database-gds-aem-repository-and-content-storage-root-directories}

AEM Forms は、セーフバックアップ（スナップショット）モードまたはローリングバックアップ（継続的な範囲）モードのいずれかにする必要があります。AEM Forms を設定していずれかのバックアップモードを開始する前に、以下のことを確認してください。

* システムのバージョンを確認し、最後のシステムイメージ完全バックアップ後に適用されたパッチや更新を記録します。
* ローリングモードまたはスナップショットモードのバックアップのいずれかを使用している場合、データベースのログが正しく設定されており、データベースのホットバックアップが実行可能であることを確認してください（[AEM Forms データベース](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database)を参照してください。）

これらに加えて、バックアップ／復元プロセスのための次のガイドラインを確認してください。

* 使用可能なオペレーティングシステムまたはサードパーティのバックアップユーティリティを使用して GDS ディレクトリをバックアップします（[GDS の場所](/help/forms/using/admin-help/files-back-recover.md#gds-location)を参照）。
* （オプション）使用可能なオペレーティングシステム、またはサードパーティのバックアップ機能やユーティリティを使用して、コンテンツ保存場所のルートディレクトリをバックアップします（[コンテンツ保存場所のルートディレクトリ（スタンドアロン環境）](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-stand-alone-environment)または[コンテンツ保存場所のルートディレクトリ（クラスター環境）](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-clustered-environment)を参照）。
* オーサーインスタンスと   オーサーインスタンスとパブリッシュインスタンス（crx -repositoryバックアップ）。

   Correspondence Management Solution 環境をバックアップするには、[バックアップと復旧](/help/sites-administering/backup-and-restore.md)に説明されているように、オーサーインスタンスとパブリッシュインスタンスに対して手順を実行します。

   オーサーインスタンスとパブリッシュインスタンスをバックアップするときには、次の点を考慮してください。

   * オーサーインスタンスと  作成者インスタンスと発行インスタンスは同時に開始に同期されます。バックアップの実行中も、作成者インスタンスと発行インスタンスを引き続き使用できますが、バックアップ中にアセットを発行しないで、キャプチャされない変更を防ぐことをお勧めします。 新しいアセットをパブリッシュする前に、オーサーインスタンスとパブリッシュインスタンスの両方のバックアップが終了するまで待機してください。
   * Author ノードの完全なバックアップには、Forms Manager および AEM Forms ワークスペースデータのバックアップが含まれます。
   * ワークベンチ開発者はそのプロセスに対してローカルで作業を継続できます。ワークベンチ開発者は、バックアップ段階では新しいプロセスをデプロイするべきではありません。
   * 各バックアップセッションの長さについての決定（ローリングバックアップモードの場合）は、AEM forms 内のすべてのデータ（DB、GDS、AEM レポジトリ、その他すべての追加カスタムデータ）をバックアップするための合計時間に基づいて行ってください。

すべてのトランザクションログを含む、AEM forms データベースをバックアップする必要があります（[AEM Forms データベース](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database)を参照してください。）詳しくは、ご使用のデータベースに該当するナレッジベース記事を参照してください。

* [AEM Forms の Oracle バックアップと回復](https://www.adobe.com/go/kb403624)
* [AEM Forms の MySQL バックアップと回復](https://www.adobe.com/go/kb403625)
* [AEM Forms の Microsoft SQL Server バックアップと回復](https://www.adobe.com/go/kb403623)
* [AEM Forms の DB2 バックアップと回復](https://www.adobe.com/go/kb403626)

これらの記事では、データをバックアップおよび回復するための、基本的なデータベース機能の概要について説明しています。これらの記事は、特定ベンダーのデータベースのバックアップ機能および回復機能に対する包括的な技術ガイドを目的とするものではありません。AEM Forms アプリケーションデータ用の信頼性のあるデータベースバックアップ方法で必要となるコマンドについて、概要を説明しています。

>[!NOTE]
>
>データベースのバックアップは、GDS のバックアップを開始する前に完了しておく必要があります。データベースのバックアップが完了していない場合、データは同期されません。

### バックアップモードの開始  {#entering-the-backup-modes}

バックアップモードを開始および終了するには、管理コンソール、LCBackupMode コマンド、AEM forms インストールで使用可能な API のいずれかを使用します。ローリングバックアップ（継続的な取得）では管理コンソールオプションを使用できないことに注意してください。コマンドラインオプションか API のいずれかを使用する必要があります。<!-- Fix broken link For information about using the API to enter and leave backup modes, see AEM forms API Reference on Help and Tutorials page. -->

>[!NOTE]
>
>forms サーバーで SSL を設定した場合、LCBackupMode.CMD スクリプトを使用して Forms サーバーをバックアップモードにすることはできません。

**管理コンソールを使用したセーフバックアップモードの開始**

1. 管理コンソールにログインします。
1. 設定／コアシステム設定／バックアップユーティリティをクリックします。
1. 「セーフバックアップモードで稼働する」を選択して、「OK」をクリックします。

   この方法によって、AEM Forms は無制限（タイムアウトなし）のバックアップモードになり、ローリングバックアップモードではなくスナップショットモードになります。

**コマンドラインオプションを使用したセーフバックアップモードの開始**

コマンドラインインターフェイスの `LCBackupMode` スクリプトを使用して、AEM Forms をセーフバックアップモードにすることができます。

1. ADOBE_LIVECYCLE を設定し、アプリケーションサーバーを起動します。
1. `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline`フォルダーに移動します。
1. オペレーティングシステムに応じて、`LCBackupMode.cmd` または `LCBackupMode.sh` スクリプトを編集して、システムに適合するデフォルト値を指定します。
1. コマンドプロンプトで、次のコマンドを 1 行で実行します。

   * (Windows)`LCBackupMode.cmd enter [-Host=`*hostname* `] [-port=`*portnumber* `] [-user=`*username* `] [-password=`*password* `] [-label=`*labelname* `] [-timeout=`*seconds* `]`
   * (Linux、UNIX)`LCBackupMode.sh enter [-host=`*hostname* `] [-port=`*portnumber* `] [-user=`*username* `] [-password=`*password* `] [-label=`*labelname* `]`

   上記のコマンドでは、プレースホルダーは次のように定義されています。

   `Host` は、AEM Forms が実行されているホストの名前です。

   `port` は、AEM Forms が実行されているアプリケーションサーバーの WebService ポートです。

   `user` は、AEM Forms 管理者のユーザー名です。

   `password` は、AEM Forms 管理者のパスワードです。

   `label` は、このバックアップのテキストラベルです（任意の文字列を指定可能）。

   `timeout` は、バックアップモードが自動的に終了するまでの秒数です。0～10,080 の値を指定できます。0 を指定すると、バックアップモードはタイムアウトしません（デフォルト）。

   バックアップモードのコマンドラインインターフェイスについて詳しくは、BackupRestoreCommandline ディレクトリ内にある、お読みくださいファイルを参照してください。

### バックアップモードの終了  {#leaving-backup-modes}

バックアップモードを終了するには、管理コンソールまたはコマンドラインオプションのいずれかを使用します。

**セーフバックアップモード（スナップショットモード）の終了**

管理コンソールを使用して AEM Forms のセーフバックアップモード（スナップショットモード）を終了するには、以下のタスクを実行します。

1. 管理コンソールにログインします。
1. 設定／コアシステム設定／バックアップユーティリティをクリックします。
1. 「セーフバックアップモードで稼働する」を選択して、「OK」をクリックします。

**すべてのバックアップモードの終了**

コマンドラインインターフェイスを使用して、AEM Forms のセーフバックアップモード（スナップショットモード）または現在のバックアップモードセッション（ローリングモード）を終了できます。管理コンソールからはローリングバックアップモードを終了できないことに注意してください。ローリングバックアップモードの場合、管理コンソールのバックアップユーティリティのコントロールは無効になります。API 呼び出しを使用するか、LCBackupMode コマンドを使用することが必要です。

1. `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline`フォルダーに移動します。
1. オペレーティングシステムに応じて、`LCBackupMode.cmd` または `LCBackupMode.sh` スクリプトを編集して、システムに適合するデフォルト値を指定します。

   >[!NOTE]
   >
   >「[AEM Forms のインストールの準備](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63)」を参照し、ご使用のアプリケーションに該当する章の説明に従って JAVA_HOME ディレクトリを設定する必要があります。**

1. 次のコマンドを 1 行で実行します。

   * (Windows)`LCBackupMode.cmd leaveContinuousCoverage [-Host=`*hostname* `] [-port=`*portnumber* `] [-user=`*username* `] [-password=`*password* `]`
   * (Linux、UNIX)`LCBackupMode.sh leaveContinuousCoverage [-Host=`*hostname* `] [-port=`*portnumber* `] [-user=`*username* `] [-password=`*password* `]`

      上記のコマンドでは、プレースホルダーは次のように定義されています。

      `Host` は、AEM Forms が実行されているホストの名前です。

      `port` は、AEM Forms が実行されているアプリケーションサーバー上のポートです。

      `user` は、AEM Forms 管理者のユーザー名です。

      `password` は、AEM Forms 管理者のパスワードです。

      `leaveContinuousCoverage` は、ローリングバックアップモードを完全に無効にする場合に使用します。
   >[!NOTE]
   >
   >バックアップモードがオフのとき、継続的な取得を再確立できません。このときの変更は保護されません。

   >[!NOTE]
   >
   >データベースへのドキュメントの保存を有効にした場合、スナップショットバックアップモードとローリングバックアップモードは使用できません。

   バックアップモードのコマンドラインインターフェイスについて詳しくは、BackupRestoreCommandline ディレクトリ内にある、お読みくださいファイルを参照してください。

