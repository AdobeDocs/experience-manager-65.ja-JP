---
title: AEM Forms データの回復
seo-title: AEM Forms データの回復
description: ここでは、AEM Forms データの回復に必要な手順について説明します。
seo-description: ここでは、AEM Forms データの回復に必要な手順について説明します。
uuid: b5735196-5a8d-4358-884f-e9b8d8f4f682
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4e093114-219b-4018-9530-9002eb665448
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# AEM Forms データの回復 {#recovering-the-aem-forms-data}

ここでは、AEM Forms データの回復に必要な手順について説明します。[バックアップと回復に関する考慮事項](/help/forms/using/admin-help/backup-recovery-strategy-aem-forms.md#special-considerations-for-backup-and-recovery)も参照してください。

>[!NOTE]
>
>データベース、GDS、AEM リポジトリ、およびコンテンツ保存場所のルートディレクトリは、元のものと同じ DNS 名を持つコンピューターに復元する必要があります。

AEM Forms は、以下の障害から安全な方法で回復します。

**ディスク障害：**&#x200B;データベースの内容を回復するには、最新のバックアップメディアが必要です。

**データの破損：**&#x200B;ファイルシステムは過去のトランザクションを記録せず、システムは誤って必要なプロセスデータを上書きする場合があります。

**ユーザーエラー：**&#x200B;回復は、対象のデータベースで使用可能にされたデータに制限されます。データが保存されていて、使用可能な場合、回復は簡単に実行できます。

**停電、システムクラッシュ：**&#x200B;ファイルシステム API には多くの場合、システムの予期しない障害に対する堅牢な設計方法や使用方法がありません。停電またはシステムクラッシュが発生した場合、ファイルシステムに格納されているドキュメントコンテンツよりも、データベースに格納されているドキュメントコンテンツの方が最新の状態である可能性が高くなります。

ローリングバックアップモードを使用すると、回復後にバックアップモードになります。スナップショットバックアップモードを使用すると、回復後にバックアップモードになりません。

バックアップから新しいシステムに復元すると、次の設定が異なる場合があります。この相違点は、AEM Forms アプリケーションの正常な回復には影響しません。

* IP アドレス
* 物理的なシステム設定（CPU、ディスク、メモリ）
* GDS の場所

>[!NOTE]
>
>コンテンツ保存場所のルートディレクトリのバックアップは、Content Services の設定時に指定したディレクトリの場所に復元する必要があります。

複数ノードで構成されるクラスターのいずれかのノードで障害が発生し、クラスターのその他のノードが適切に稼働している場合は、クラスターのシングルノード回復手順を実行します。

## AEM Forms データを回復する {#recover-the-aem-forms-data}

1. AEM Forms サービスとアプリケーションサーバーが実行中の場合は停止します。
1. 必要に応じて、システムイメージから物理システムを再作成します。例えば、回復の理由が障害のあるデータベースサーバーである場合、この手順は必要ありません。
1. イメージの作成後に適用されたパッチまたはアップデートを AEM Forms に適用します。この情報は、バックアップ手順で記録されたものです。システムをバックアップしたときと同じパッチレベルを AEM Forms に適用する必要があります。
1. （WebSphere Application Server）WebSphere Application Server の新規インスタンスに回復している場合、restoreConfig.bat／sh コマンドを実行します。
1. AEM forms データベースを回復します。そのためには、最初にデータベースバックアップファイルを使用してデータベース復元操作を実行し、次に復元後のデータベースにトランザクションのやり直しログを適用します（「[AEM Forms データベース](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database)」を参照）。詳しくは、次のナレッジベース記事を参照してください。

   * [AEM Forms の Oracle バックアップと回復](https://www.adobe.com/go/kb403624)
   * [AEM Forms の MySQL バックアップと回復](https://www.adobe.com/go/kb403625)
   * [AEM Forms の Microsoft SQL Server バックアップと回復](https://www.adobe.com/go/kb403623)
   * [AEM Forms の DB2 バックアップと回復](https://www.adobe.com/go/kb403626)

1. GDS ディレクトリを回復します。そのためには、最初に AEM Forms の既存のインストール環境にある GDS ディレクトリのコンテンツを削除し、次にバックアップ GDS から GDS ディレクトリのコンテンツをコピーします。GDS ディレクトリの場所を変更した場合は、[回復中の GDS の場所の変更](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery)を参照してください。
1. 次の例で示すとおり、復元される GDS バックアップディレクトリの名前を変更します。

   >[!NOTE]
   >
   >/restore ディレクトリが既に存在する場合、それをバックアップし、最新データを含む /backup ディレクトリを名前変更する前に削除します。

   * (JBoss)名前を次の名前に `[appserver root]/server/'server'/svcnative/DocumentStorage/backup` 変更：

      `[appserver root]/server/'server'/svcnative/DocumentStorage/restore` です。

   * (WebLogic)名前を次の名前に `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/backup` 変更：

      `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/restore` です。

   * (WebSphere)名前を次の名前 `[appserver root]/installedApps/adobe/'server'/DocumentStorage/backup` に変更：

      `[appserver root]/installedApps/adobe/'server'/DocumentStorage/restore` です。

1. コンテンツ保存場所のルートディレクトリを回復します。そのためには、最初に AEM Forms の既存のインストール環境にあるコンテンツ保存場所のルートディレクトリの内容を削除し、スタンドアロン環境またはクラスター環境のいずれかのタスクに従って、このルートディレクトリの内容を回復します。

   >[!NOTE]
   >
   >コンテンツ保存場所のルートディレクトリのバックアップは、Content Services（非推奨）の設定時に指定したコンテンツ保存場所のルートディレクトリの場所に復元する必要があります。

   **スタンドアロン：**&#x200B;回復プロセス中に、バックアップされたすべてのディレクトリを復元します。これらのディレクトリが復元されたときに、/backup-lucene-indexes ディレクトリが存在する場合、/lucene-indexes に名前変更します。そうでない場合は、lucene-indexes ディレクトリは存在するはずなので、必要な作業はありません。

   **クラスター：**&#x200B;回復プロセス中に、バックアップされたすべてのディレクトリを復元します。インデックスルートディレクトリを復元するには、クラスターの各ノードで次の手順を実行します。

   * インデックスルートディレクトリ内のコンテンツをすべて削除します。
   * /backup-lucene-indexes ディレクトリが存在する場合、*Content Storage Root directory*/backup-lucene-indexes ディレクトリの内容をインデックスルートディレクトリにコピーし、*Content Storage Root directory*/backup-lucene-indexes ディレクトリを削除します。
   * /lucene-indexes ディレクトリが存在する場合、*Content Storage Root directory*/lucene-indexes ディレクトリの内容をインデックスルートディレクトリにコピーします。

1. CRX-repository を復元/復旧します。

   * **スタンドアロン**

      *作成者インスタンスおよび発行インスタンスの復元*：事故が発生した場合は、[バックアップと復元](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html)に説明されている手順を実行して、リポジトリを最新のバックアップ状態に復元できます。

      Author ノードを完全に復元すれば、Forms Manager および AEM Forms Workspace データも復元されます。

   * **クラスター化**

      クラスター環境での復元については、[クラスター環境でのバックアップと復元の方策](/help/forms/using/admin-help/strategy-backup-restore-clustered-environment.md#strategy-for-backup-and-restore-in-a-clustered-environment)を参照してください。

1. java.io.temp ディレクトリまたは Adobe temp ディレクトリに作成された AEM forms の一時ファイルをすべて削除します。
1. 開始AEM forms(「サ [ービスの開始と停止](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services)」を参照<!-- BROKEN LINK and the application server(s) (see [Maintaining the Application Server](/help/forms/using/admin-help/topics/maintaining-the-application-server.md))-->)。

## 回復中の GDS の場所の変更 {#changing-the-gds-location-during-recovery}

GDS を元の場所とは異なる場所に復元する場合は、LCSetGDS スクリプトを実行して GDS を新しい場所に設定します。スクリプトはフォルダー内にあ `[aem-forms root]\sdk\misc\Foundation\SetGDSCommandline` ります。 The script takes two parameters, `defaultGDS` and `newGDS`. スクリプトの実行方法については、同フォルダー内の `ReadMe.txt` ファイルを参照してください。

>[!NOTE]
>
>データベースへのドキュメントの保存を有効にした場合、GDS の場所を変更する必要はありません。

>[!NOTE]
>
>これは、GDS の場所の変更にこのスクリプトを使用する必要がある唯一の状況です。AEM Forms の実行中に GDS の場所を変更するには、管理コンソールを使用します。（[一般的な AEM Forms の設定](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)を参照してください。）

>[!NOTE]
>
>GDS ディレクトリがドライブのルート（D:\ など）にある場合、Windows でのコンポーネントのデプロイメントは失敗します。GDS の場合、ディレクトリがドライブのルートではなく、サブディレクトリに配置されていることを確認する必要があります。例えば、ディレクトリは単に D:\ ではなく D:\GDS にする必要があります。

## クラスター環境への GDS の回復 {#recovering-the-gds-to-a-clustered-environment}

クラスター環境における GDS の場所を変更するには、クラスター全体をシャットダウンし、クラスター内の 1 つのノードで LCSetGDS スクリプトを実行します（[回復中の GDS の場所の変更](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery)を参照）。そのノードのみを起動します。ノードが完全に起動したら、クラスター内の他のノードも安全に起動できるので、新規 GDS が正しく指定されます。

>[!NOTE]
>
>他のノードを起動する前に、最初の 1 つのノードが完全に起動していることを確認できない場合、クラスターを起動する前に、クラスター内のすべてのノードで LCSetGDS スクリプトを実行する必要があります。

