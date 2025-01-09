---
title: Adobe Experience Manager Forms データのバックアップ
description: ここでは、Adobe Experience Manager（AEM）Forms データベース、GDS およびコンテンツストレージのルートディレクトリのホットバックアップ（オンラインバックアップ）の実行に必要な手順を説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 536615a4-ab42-4b72-83b1-fad110b011ee
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '1527'
ht-degree: 100%

---

# Adobe Experience Manager（AEM）Forms データのバックアップ {#backing-up-the-aem-forms-data}

<!-- back up is two words when used as a verb; backup is one word when used as an adjective or noun. -->

ここでは、AEM Forms データベース、GDS およびコンテンツストレージのルートディレクトリのホットバックアップ（オンラインバックアップ）の実行に必要な手順を説明します。

AEM Forms をインストールし、実稼働環境にデプロイしたら、データベース管理者はデータベースの初期完全バックアップ（コールドバックアップ）を実行する必要があります。このバックアップを実行するには、データベースをシャットダウンする必要があります。その後、データベースの差分バックアップまたは増分（ホット）バックアップを定期的に行う必要があります。

バックアップと回復を正常に実行するには、システムイメージバックアップを常に使用可能にしておく必要があります。このようにすると、損失が発生した場合、環境全体を一貫性のある状態に回復できます。

GDS、AEM リポジトリ、およびコンテンツストレージのルートディレクトリのバックアップと同時にデータベースをバックアップすることで、回復が必要な場合に備えてこれらのシステムを同期しておくことができます。

この節で説明するバックアップ手順では、AEM Forms データベース、AEM レポジトリ、GDS およびコンテンツストレージのルートディレクトリをバックアップする前にセーフバックアップモードにする必要があります。バックアップが完了したら、セーフバックアップモードを終了する必要があります。セーフバックアップモードは、GDS 内にある長期間有効なドキュメントと永続ドキュメントにマークを付けるために使用します。このモードによって、セーフバックアップモードが解放されるまで、自動化されたファイルのクリーンアップメカニズム（ファイルコレクター）によって有効期限の切れたファイルが削除されなくなります。GDS バックアップとデータベースバックアップの同期を維持する必要があります。

GDS の場所をバックアップする頻度は、AEM Forms の使用方法と使用可能なバックアップウィンドウに応じて異なります。バックアップウィンドウは、数日間実行される可能性のある長期間有効なプロセスの影響を受ける場合があります。このディレクトリ内のファイルを継続して変更、追加および削除する場合は、GDS の場所をより頻繁にバックアップするようにしてください。

データベースが前の節で説明したログモードで実行されている場合、データベースログを頻繁にバックアップして、メディアの障害が発生したときにデータベースの復元に使用できるようにすることが必要です。

>[!NOTE]
>
>参照されていないファイルは、回復プロセスの後に GDS ディレクトリ内で維持されます。これは、現在の既知の制限です。

## データベース、GDS、AEM リポジトリ、およびコンテンツストレージのルートディレクトリをバックアップ {#back-up-the-database-gds-aem-repository-and-content-storage-root-directories}

AEM Forms は、セーフバックアップ（スナップショット）モードまたはローリングバックアップ（継続的カバレッジ）モードのいずれかにします。AEM Forms を設定していずれかのバックアップモードを開始する前に、以下のことを確認してください。

* システムのバージョンを確認し、最後のシステムイメージ完全バックアップ後に適用されたパッチやアップデートを記録します。
* ローリングモードまたはスナップショットモードのバックアップのいずれかを使用している場合、データベースのログが正しく設定されており、データベースのホットバックアップが実行可能であることを確認してください（[AEM Forms データベース](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database)を参照）。

これらに加えて、バックアップ／復元プロセスのための次のガイドラインを確認してください。

* 使用可能なオペレーティングシステムまたはサードパーティのバックアップユーティリティを使用して GDS ディレクトリをバックアップします（[GDS の場所](/help/forms/using/admin-help/files-back-recover.md#gds-location)を参照）。
* （オプション）使用可能なオペレーティングシステム、またはサードパーティのバックアップ機能やユーティリティを使用して、コンテンツストレージのルートディレクトリをバックアップします（[コンテンツストレージのルートディレクトリ（スタンドアロン環境）](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-stand-alone-environment)または[コンテンツストレージのルートディレクトリ（クラスター環境）](/help/forms/using/admin-help/files-back-recover.md#content-storage-root-location-clustered-environment)を参照）。
* オーサーインスタンスとパブリッシュインスタンスをバックアップします（crx-repository のバックアップ）。

  Correspondence Management ソリューション環境をバックアップするには、[バックアップと復元](/help/sites-administering/backup-and-restore.md)に説明されているように、オーサーインスタンスとパブリッシュインスタンスに対して手順を実行します。

  オーサーインスタンスとパブリッシュインスタンスをバックアップするときには、次の点を考慮してください。

   * オーサーインスタンスとパブリッシュインスタンスのバックアップが同時に開始するように同期されていることを確認します。バックアップの実行中もオーサーインスタンスとパブリッシュインスタンスを継続して使用できますが、キャプチャされない変更が生じないようにするために、バックアップ中はアセットを公開しないことをお勧めします。新しいアセットを公開する前に、オーサーインスタンスとパブリッシュインスタンスの両方のバックアップが終了するまで待機してください。
   * オーサーノードの完全なバックアップには、Forms Manager および AEM Forms Workspace データのバックアップが含まれます。
   * ワークベンチ開発者はそのプロセスに対してローカルで作業を継続できます。ワークベンチ開発者は、バックアップ段階では新しいプロセスをデプロイしないでください。
   * 各バックアップセッションの長さについての決定（ローリングバックアップモードの場合）は、AEM Forms 内のすべてのデータ（DB、GDS、AEM レポジトリ、その他すべての追加カスタムデータ）をバックアップするための合計時間に基づいて行ってください。

すべてのトランザクションログを含む、AEM Forms データベースをバックアップします（[AEM Forms データベース](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database)を参照）。

詳しくは、ご使用のデータベースに該当するナレッジベース記事を参照してください。
<!-- The four URLs below are all 404s; checked July 19, 2023 -->
* [AEM Forms の Oracle バックアップと回復](https://www.adobe.com/go/kb403624)
* [AEM Forms の MySQL バックアップと回復](https://www.adobe.com/go/kb403625)
* [AEM Forms の Microsoft® SQL Server バックアップと回復](https://www.adobe.com/go/kb403623)
* [AEM Forms の DB2® バックアップと回復](https://www.adobe.com/go/kb403626)

これらの記事では、データをバックアップおよび回復するための、基本的なデータベース機能の概要について説明しています。これらの記事は、特定ベンダーのデータベースのバックアップ機能および回復機能に対する包括的な技術ガイドを目的とするものではありません。AEM Forms アプリケーションデータ用の信頼性のあるデータベースバックアップ方法で必要となるコマンドについて、概要を説明しています。

>[!NOTE]
>
>GDS のバックアップを開始する前に、データベースのバックアップを完了しておく必要があります。データベースのバックアップが完了していない場合、データは同期されません。

### バックアップモードの開始 {#entering-the-backup-modes}

管理コンソール、LCBackupMode コマンド、またはAEM Formsインストールで使用可能な API のいずれかを使用して、バックアップモードを開始および終了できます。ローリングバックアップ（継続的カバレッジ）の場合、管理コンソールオプションは使用できません。コマンドラインオプションまたは API のいずれかを使用する必要があります。<!-- Fix broken link For information about using the API to enter and leave backup modes, see AEM Forms API Reference on Help and Tutorials page. -->

>[!NOTE]
>
>Forms サーバーで SSL を設定した場合、LCBackupMode.CMD スクリプトを使用して Forms サーバーをバックアップモードにすることはできません。

**管理コンソールを使用したセーフバックアップモードの開始**

1. 管理コンソールにログインします。
1. 設定／コアシステム設定／バックアップユーティリティの順にクリックします。
1. 「セーフバックアップモードで稼働する」を選択し、「OK」をクリックします。

   この方法によって、AEM Forms は無制限（タイムアウトなし）のバックアップモードになり、ローリングバックアップモードではなくスナップショットモードに移行します。

**コマンドラインオプションを使用したセーフバックアップモードの開始**

コマンドラインインターフェイスの `LCBackupMode` スクリプトを使用して、AEM Forms をセーフバックアップモードにすることができます。

1. ADOBE_LIVECYCLE を設定し、アプリケーションサーバーを起動します。
1. `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline` フォルダーに移動します。
1. オペレーティングシステムに応じて、`LCBackupMode.cmd` または `LCBackupMode.sh` スクリプトを編集して、システムに適合するデフォルト値を指定します。
1. コマンドプロンプトで、次のコマンドを 1 行で実行します。

   * （Windows）`LCBackupMode.cmd enter [-Host=`*ホスト名* `] [-port=`*ポート番号* `] [-user=`*ユーザー名* `] [-password=`*パスワード* `] [-label=`*ラベル名* `] [-timeout=`*秒数* `]`
   * （Linux®、UNIX®）`LCBackupMode.sh enter [-host=`*ホスト名* `] [-port=`*ポート番号* `] [-user=`*ユーザー名* `] [-password=`*パスワード* `] [-label=`*ラベル名* `]`

   上記のコマンドでは、プレースホルダーは次のように定義されています。

   `Host` は、AEM Forms が実行されているホストの名前です。

   `port` は、AEM Forms が実行されているアプリケーションサーバーの WebService ポートです。

   `user` は、AEM Forms 管理者のユーザー名です。

   `password` は、AEM Forms 管理者のパスワードです。

   `label` は、このバックアップのテキストラベルです（任意の文字列を指定可能）。

   `timeout` は、バックアップモードが自動的に終了するまでの秒数です。0 ～ 10,080 の値を指定できます。0（デフォルト）の場合、バックアップモードはタイムアウトしません。

   バックアップモードへのコマンドラインインターフェイスについて詳しくは、BackupRestoreCommandline ディレクトリ内にある Readme ファイルを参照してください。

### バックアップモードの終了 {#leaving-backup-modes}

>[!NOTE]
> 
> ユーザーが管理者コンソールにアクセスする管理者権限を持っていることを確認します。

バックアップモードを終了するには、管理コンソールまたはコマンドラインオプションのいずれかを使用します。

**セーフバックアップモード（スナップショットモード）を終了**

管理コンソールを使用して AEM Forms をセーフバックアップモード（スナップショットモード）を終了するには、以下のタスクを実行します。

1. 管理コンソールにログインします。
1. 設定／コアシステム設定／バックアップユーティリティの順にクリックします。
1. 「セーフバックアップモードで稼働する」を選択して、「OK」をクリックします。

**すべてのバックアップモードを終了**

コマンドラインインターフェイスを使用して、AEM Forms のセーフバックアップモード（スナップショットモード）または現在のバックアップモードセッション（ローリングモード）を終了できます。管理コンソールを使用してローリングバックアップモードを終了することはできません。ローリングバックアップモード中は、管理コンソールのバックアップユーティリティコントロールは無効です。API 呼び出しを使用するか、LCBackupMode コマンドを使用します。

1. `*[aem-forms root]*/sdk/misc/Foundation/BackupRestoreCommandline` フォルダーに移動します。
1. オペレーティングシステムに応じて、`LCBackupMode.cmd` または `LCBackupMode.sh` スクリプトを編集して、システムに適合するデフォルト値を指定します。

   >[!NOTE]
   >
   >JAVA_HOME ディレクトリは、ご利用のアプリケーションサーバーに該当する章（[AEM Forms のインストールの準備](https://www.adobe.com/go/learn_aemforms_prepareInstallsingle_63_jp)*）に記載されているとおりに設定する必要があります。*

1. 次のコマンドを 1 行で実行します。

   * （Windows）`LCBackupMode.cmd leaveContinuousCoverage [-Host=`*ホスト名* `] [-port=`*ポート番号* `] [-user=`*ユーザー名* `] [-password=`*パスワード* `]`
   * （Linux®、UNIX®）`LCBackupMode.sh leaveContinuousCoverage [-Host=`*ホスト名* `] [-port=`*ポート番号* `] [-user=`*ユーザー名* `] [-password=`*パスワード* `]`

     上記のコマンドでは、プレースホルダーは次のように定義されています。

     `Host` は、AEM Forms が実行されているホストの名前です。

     `port` は、AEM Forms が実行されているアプリケーションサーバー上のポートです。

     `user` は、AEM Forms 管理者のユーザー名です。

     `password` は、AEM Forms 管理者のパスワードです。

     `leaveContinuousCoverage` は、ローリングバックアップモードを完全に無効にする場合に使用します。

   >[!NOTE]
   >
   >バックアップモードがオフの間は、継続的なカバレッジを再確立できません。その間の変更は保護されません。

   >[!NOTE]
   >
   >データベースでドキュメントの保存を有効にした場合、スナップショットバックアップモードとローリングバックアップモードは使用できません。

   バックアップモードへのコマンドラインインターフェイスについて詳しくは、BackupRestoreCommandline ディレクトリ内にある Readme ファイルを参照してください。
