---
title: AEM Forms データの回復
seo-title: Recovering the AEM forms data
description: ここでは、AEM forms データを回復するために必要な手順について説明します。
seo-description: This document describes the steps required to recover the AEM forms data.
uuid: b5735196-5a8d-4358-884f-e9b8d8f4f682
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4e093114-219b-4018-9530-9002eb665448
exl-id: 9e648bab-9284-4fda-abb4-8bd7cd085981
source-git-commit: 4fa868f3ae4778d3a637e90b91f7c5909fe5f8aa
workflow-type: tm+mt
source-wordcount: '1180'
ht-degree: 17%

---

# AEM Forms データの回復 {#recovering-the-aem-forms-data}

ここでは、AEM forms データを回復するために必要な手順について説明します。 関連トピック [バックアップとリカバリに関する特別な考慮事項](/help/forms/using/admin-help/backup-recovery-strategy-aem-forms.md#special-considerations-for-backup-and-recovery).

>[!NOTE]
>
>データベース、GDS、AEMリポジトリ、およびコンテンツ保存場所のルートディレクトリは、元のディレクトリと同じ DNS 名を持つコンピューターに復元する必要があります。

AEM forms は、次のエラーから確実に回復します。

**ディスク障害：**&#x200B;データベースの内容を回復するには、最新のバックアップメディアが必要です。

**データの破損：**&#x200B;ファイルシステムは過去のトランザクションを記録せず、システムは誤って必要なプロセスデータを上書きする場合があります。

**ユーザーエラー：**&#x200B;回復は、対象のデータベースで使用可能にされたデータに制限されます。データが保存されていて、使用可能な場合、回復は簡単に実行できます。

**停電、システムクラッシュ：**&#x200B;ファイルシステム API には多くの場合、システムの予期しない障害に対する堅牢な設計方法や使用方法がありません。停電またはシステムクラッシュが発生した場合、データベースに格納されているドキュメントコンテンツは、ファイルシステムに格納されているコンテンツよりも最新である可能性が高くなります。

ローリングバックアップモードを使用している場合、回復後もバックアップモードのままです。 スナップショットバックアップモードを使用している場合、回復後はバックアップモードになりません。

バックアップから新しいシステムに復元する場合、次の設定が異なる場合があります。 この違いは、AEM forms アプリケーションの正常な回復には影響しません。

* IP アドレス
* 物理システムの構成（CPU、ディスク、メモリ）
* GDS の場所

>[!NOTE]
>
>コンテンツ保存場所のルートディレクトリのバックアップは、Content Services の設定時に設定されたディレクトリの場所に復元する必要があります。

多ノードクラスタの 1 つのノードで障害が発生し、クラスタの残りのノードが正しく動作している場合は、クラスタの単一ノードの回復手順を実行します。

## AEM forms データを回復する {#recover-the-aem-forms-data}

1. 実行中の場合は、AEM forms サービスおよびアプリケーションサーバーを停止します。
1. 必要に応じて、システムイメージから物理システムを再作成します。 例えば、リカバリの理由が障害のあるデータベースサーバーである場合は、この手順が必要ない場合があります。
1. イメージの作成後に適用されたAEM forms にパッチまたはアップデートを適用します。 この情報は、バックアップ手順で記録されました。 AEM forms は、システムのバックアップ時と同じパッチレベルにパッチを適用する必要があります。
1. (WebSphere® Application Server)WebSphere® Application Server の新しいインスタンスに回復する場合は、restoreConfig.bat/sh コマンドを実行します。
1. AEM forms データベースを回復します。まず、データベースのバックアップファイルを使用してデータベースの復元操作を実行し、次に、回復したデータベースにトランザクションのやり直しログを適用します。 ( [AEM forms データベース](/help/forms/using/admin-help/files-back-recover.md#aem-forms-database).) 詳しくは、次のナレッジベース記事を参照してください。

   * [AEM forms の DB2®バックアップと回復](https://experienceleague.adobe.com/docs/experience-manager-64/forms/administrator-help/aem-forms-backup-recovery/files-back-recover.html?lang=en#db2)
   * [AEM Forms の Oracle バックアップと回復](https://experienceleague.adobe.com/docs/experience-manager-64/forms/administrator-help/aem-forms-backup-recovery/files-back-recover.html?lang=en#oracle)
   * [AEM forms のMicrosoft® SQL Server バックアップと回復](https://experienceleague.adobe.com/docs/experience-manager-64/forms/administrator-help/aem-forms-backup-recovery/files-back-recover.html?lang=en#sql-server)
   * [AEM Forms の MySQL バックアップと回復](https://experienceleague.adobe.com/docs/experience-manager-64/forms/administrator-help/aem-forms-backup-recovery/files-back-recover.html?lang=en#mysql)

1. GDS ディレクトリを回復します。まず、AEM forms の既存のインストールで GDS ディレクトリの内容を削除し、次に、バックアップされた GDS から GDS ディレクトリの内容をコピーします。 GDS ディレクトリの場所を変更した場合は、 [回復中の GDS の場所の変更](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).
1. 次の例に示すように、復元する GDS バックアップディレクトリの名前を変更します。

   >[!NOTE]
   >
   >/restore ディレクトリが既に存在する場合は、バックアップしてから削除してから、最新のデータを含む/backup ディレクトリの名前を変更します。

   * (JBoss®) 名前を変更 `[appserver root]/server/'server'/svcnative/DocumentStorage/backup` 移動先：

      `[appserver root]/server/'server'/svcnative/DocumentStorage/restore`

   * （WebLogic）`[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/backup` を次に変更：

      `[appserverdomain]/'server'/adobe/AEMformsserver/DocumentStorage/restore`

   * (WebSphere®) 名前を変更 `[appserver root]/installedApps/adobe/'server'/DocumentStorage/backup` 移動先：

      `[appserver root]/installedApps/adobe/'server'/DocumentStorage/restore`

1. コンテンツ保存場所のルートディレクトリを復元するには、まずAEM forms の既存のインストールにあるコンテンツ保存場所のルートディレクトリの内容を削除し、次に、スタンドアロン環境またはクラスター環境のタスクに従って内容を復元します。

   >[!NOTE]
   >
   >コンテンツ保存場所のルートディレクトリのバックアップは、Content Services（非推奨）の設定時に設定されたコンテンツ保存場所のルートディレクトリの場所に復元する必要があります。

   **スタンドアロン：**&#x200B;回復プロセス中に、バックアップされたすべてのディレクトリを復元します。これらのディレクトリが復元されたら、/backup-lucene-indexes ディレクトリが存在する場合は、名前を/lucene-indexes に変更します。 そうしないと、lucene-indexes ディレクトリが既に存在し、アクションは不要になります。

   **クラスター：**&#x200B;回復プロセス中に、バックアップされたすべてのディレクトリを復元します。インデックスルートディレクトリを復元するには、クラスターの各ノードで次の手順を実行します。

   * インデックスルートディレクトリ内のコンテンツをすべて削除します。
   * /backup-lucene-indexes ディレクトリが存在する場合は、 *コンテンツ保存場所のルートディレクトリ*/backup-lucene-indexes ディレクトリからインデックスルートディレクトリに移動し、 *コンテンツ保存場所のルートディレクトリ*/backup-lucene-indexes ディレクトリ。
   * /lucene-indexes ディレクトリが存在する場合は、 *コンテンツ保存場所のルートディレクトリ*/lucene-indexes ディレクトリからインデックスルートディレクトリに移動します。

1. CRX-repository を復元または回復します。

   * **スタンドアロン**

      *作成者インスタンスおよび発行インスタンスの復元*：事故が発生した場合は、[バックアップと復元](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html)に説明されている手順を実行して、リポジトリを最新のバックアップ状態に復元できます。

      Author ノードを完全に復元すると、Forms Manager とAEM Forms Workspace データも復元されます。

   * **クラスター化**

      クラスター環境での復元については、 [クラスタ環境でのバックアップと復元の戦略](/help/forms/using/admin-help/strategy-backup-restore-clustered-environment.md#strategy-for-backup-and-restore-in-a-clustered-environment).

1. java.io.temp ディレクトリまたは一時ディレクトリ内に作成されたAEM forms 一時ファイルをすべてAdobeします。
1. AEM Forms を起動します（[サービスの開始と停止](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services)を参照）<!-- BROKEN LINK and the application server(s) (see [Maintaining the Application Server](/help/forms/using/admin-help/topics/maintaining-the-application-server.md))-->。

## 回復中の GDS の場所の変更 {#changing-the-gds-location-during-recovery}

GDS が元の場所以外の場所に復元された場合は、LCSetGDS スクリプトを実行して GDS を新しい場所に設定します。 スクリプトは `[aem-forms root]\sdk\misc\Foundation\SetGDSCommandline` フォルダーにあります。このスクリプトでは `defaultGDS` と `newGDS` の 2 つのパラメーターを使用します。スクリプトの実行方法については、同フォルダー内の `ReadMe.txt` ファイルを参照してください。

>[!NOTE]
>
>データベースへのドキュメントの保存を有効にしていた場合は、GDS の場所を変更する必要はありません。

>[!NOTE]
>
>この状況は、GDS の場所を変更するためにこのスクリプトを使用する必要がある唯一の状況です。 AEM forms の実行中に GDS の場所を変更するには、管理コンソールを使用します。 （[一般的な AEM Forms の設定](/help/forms/using/admin-help/configure-general-aem-forms-settings.md#configure-general-aem-forms-settings)を参照してください。）

>[!NOTE]
>
>GDS ディレクトリがドライブルート (D:\など ) にある場合、Windows でのコンポーネントのデプロイメントは失敗します。 GDS の場合、ディレクトリがドライブのルートではなく、サブディレクトリに配置されていることを確認する必要があります。 例えば、ディレクトリはD:\GDS and not simply D:\である必要があります。

## クラスター環境への GDS の復元 {#recovering-the-gds-to-a-clustered-environment}

クラスター環境で GDS の場所を変更するには、クラスター全体をシャットダウンし、クラスターの 1 つのノードで LCSetGDS スクリプトを実行します。 ( [回復中の GDS の場所の変更](recovering-aem-forms-data.md#changing-the-gds-location-during-recovery).) そのノードのみを起動します。 そのノードが完全に起動されると、クラスター内の他のノードが安全に起動され、新しい GDS を正しく指す場合があります。

>[!NOTE]
>
>他のノードを起動する前に、1 つのノードを完全に起動できない場合は、クラスタを起動する前に、クラスタ内のすべてのノードで LCSetGDS スクリプトを実行する必要があります。
