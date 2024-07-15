---
title: クラスター環境でのバックアップと復元の方策
description: AEM Forms の実装で、追加のカスタムデータを別のデータベースに格納する場合、そのカスタムデータをバックアップするための方法を導入し、AEM Forms データと同期させる必要があります。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 98c96349-f253-475f-b646-352269814a38
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '1396'
ht-degree: 100%

---

# クラスター環境でのバックアップと復元の方策 {#strategy-for-backup-and-restore-in-a-clustered-environment}

>[!NOTE]
>
>AEM Forms の実装で、追加のカスタムデータを別のデータベースに格納する場合、そのカスタムデータをバックアップするための方法を導入し、AEM Forms データと同期させる必要があります。また、追加のデータベースを同期しないシナリオにも対処できるように、アプリケーションを堅牢な方法で設計する必要があります。一貫性のある状態を維持するために、実行するデータベース操作をトランザクションコンテキストで行うことを強くお勧めします。

エラーから回復するには、AEM forms システムの次の部分をバックアップする必要があります。

* AEM Forms が使用するデータベース
* 長期のデータおよびその他の永続的なドキュメントを持つ GDS
* AEM データベース (crx-repository)

>[!NOTE]
>
>AEM Forms セットアップで使用されているその他のデータ（例えば、カスタマーフォント、コネクターデータなど）をすべてバックアップする必要があります。

## クラスター環境のバックアップ {#back-up-a-clustered-environment}

このトピックでは、AEM Forms クラスター環境をバックアップする次の方策について検討します。

* ダウンタイムを伴うオフラインバックアップ
* ダウンタイムを必要としないオフラインバックアップ（シャットダウンされているセカンダリノードのバックアップ）
* ダウンタイムは伴わないが、レスポンスに遅れが生じるオンラインバックアップ
* Bootstrap プロパティファイルのバックアップ

### ダウンタイムを伴うオフラインバックアップ {#offline-backup-with-downtime}

1. クラスターと関連サービス全体をシャットダウンします（[サービスの開始と停止](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services)を参照してください）。
1. 任意のノードで、データベース、GDS およびコネクタをバックアップします（[バックアップおよび回復するファイル](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover)を参照してください）。
1. AEM リポジトリをオフラインでバックアップするには、次の手順を実行します。

   1. クラスターの各ノードに対して、クラスターノード ID を含むファイルをバックアップします。
   1. すべてのセカンダリクラスターノードのすべてのファイル（サブディレクトリも含む）をバックアップします。
   1. 各クラスターノードのリポジトリ / システム ID を別々にバックアップします。

   手順について詳しくは、[バックアップと復旧](https://helpx.adobe.com/jp/experience-manager/kb/CRXBackupAndRestoreProcedure.html)を参照してください。

1. カスタマーフォントなど、その他すべてのデータをバックアップします。
1. クラスターを再起動します。

### ダウンタイムなしのオフラインバックアップ {#offline-backup-with-no-downtime}

1. ローリングバックアップモードに入ります（[バックアップモードの開始](/help/forms/using/admin-help/backing-aem-forms-data.md#entering-the-backup-modes)を参照してください）。

   リカバリ後は、ローリングバックアップモードを終了します。

1. AEM に関わるクラスターのセカンダリノードをすべてシャットダウンします（[サービスの開始と停止](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services)を参照してください）。
1. 任意のノードで、データベース、GDS およびコネクタをバックアップします（[バックアップおよび回復するファイル](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover)を参照してください）。
1. AEM リポジトリをオフラインでバックアップするには、次の手順を実行します。

   1. クラスターの各ノードに対して、クラスターノード ID を含むファイルをバックアップします。
   1. すべてのセカンダリクラスターノードのすべてのファイル（サブディレクトリも含む）をバックアップします。
   1. 各クラスターノードのリポジトリ / system.id を別々にバックアップします。

   手順について詳しくは、[バックアップとリストア](https://helpx.adobe.com/jp/experience-manager/kb/CRXBackupAndRestoreProcedure.html)を参照してください。

1. カスタマーフォントなど、その他すべてのデータをバックアップします。
1. クラスターを再起動します。

### ダウンタイムは伴わないが、レスポンスに遅れが生じるオンラインバックアップ {#online-backup-with-no-downtime-but-delay-in-response}

1. ローリングバックアップモードに入ります（[バックアップモードの開始](/help/forms/using/admin-help/backing-aem-forms-data.md#entering-the-backup-modes)を参照してください）。

   リカバリ後は、ローリングバックアップモードを終了します。

1. AEM に関わるクラスターのセカンダリノードをすべてシャットダウンします（[サービスの開始と停止](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services)を参照してください）。
1. 任意のノードで、データベース、GDS およびコネクタをバックアップします（[バックアップおよび回復するファイル](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover)を参照してください）。
1. AEM リポジトリをオンラインでバックアップするには、次の手順を実行します。

   1. クラスターの各ノードに対して、cluster_node.id を含むファイルをバックアップします。
   1. 各クラスターノードのリポジトリ / system.id を別々にバックアップします。
   1. 任意のセカンダリノード上で、リポジトリのオンラインバックアップを行います。手順について詳しくは「オンラインバックアップ」を参照してください。

1. カスタマーフォントなど、その他すべてのデータをバックアップします。
1. クラスターを再起動します。

### Bootstrap プロパティファイルのバックアップ {#back-up-the-bootstrap-properties-file}

AEM クラスターを作成すると、すべてのセカンダリノードに対してアプリケーションサーバー内にプロパティファイルが作成されます。Bootstrap プロパティファイルをバックアップすることをお勧めします。このファイルは、アプリケーションサーバーの次の場所にあります。

* JBoss®：BIN ディレクトリ内
* WebLogic：ドメインディレクトリ内
* WebSphere®：プロファイルディレクトリ内

AEM セカンダリノードの災害時復旧シナリオのためにこのファイルをバックアップする必要があります。リストアする場合は、アプリケーションサーバーの指定場所でこのファイルを置き換える必要があります。

## クラスター環境での復元 {#recovery-in-a-clustered-environment}

クラスター全体または単一のノードに障害が発生した場合は、バックアップを使用して復元します。

単一ノードのリカバリの場合は、単一ノードをシャットダウンし、単一ノードのリカバリ手順を実行します。

データベースのクラッシュなどの障害が原因でクラスター全体に障害が発生した場合は、次の手順を実行します。復元は、使用するバックアップの方法によって異なります。

### 単一ノードの復元 {#restoring-a-single-node}

1. 破損したノードを停止します。

   >[!NOTE]
   >
   >障害ノードが AEM プライマリノードの場合は、クラスターノード全体をシャットダウンします。

1. システムイメージから物理システムを再作成します。
1. イメージの作成後に適用されたパッチまたはアップデートを AEM forms に適用します。この情報は、バックアップ手順で記録されたものです。システムをバックアップしたときと同じパッチレベルに AEM forms を回復する必要があります。
1. （*オプション*）その他のすべてのノードが正常に動作している場合は、AEM リポジトリも破損している可能性があります。この場合、AEM リポジトリの error.log ファイルにリポジトリ非同期メッセージが表示されます。

   リポジトリを復元するには、次の手順を実行します。

   >[!NOTE]
   >
   >圧縮された crx-repository バックアップがオンラインになった場合は、任意の場所で展開し、オフラインの復元プロセスに従います。

   1. ノードの clusterNode ディレクトリにある repository、shared、version および workspaces ディレクトリを削除します。
   1. クラスターノード（サブディレクトリも含む）のバックアップをそのノードに復元します。
   1. ノードにある clusterNode/revision.log ファイルを削除します。
   1. ノードに .lock がある場合は、それを削除します。
   1. ノードに repository/system.id がある場合は、それを削除します。
   1. ノード上に &amp;ast;&amp;ast;/listener.properties ファイルが存在する場合は削除します。
   1. クラスターノードごとに、repository/cluster_node.id を復元します。

>[!NOTE]
>
>次の点を考慮してください。

* 障害ノードが AEM プライマリノードの場合は、セカンダリリポジトリフォルダーのすべてのコンテンツ（crx-repository\crx.0000、ここで 0000 は任意の桁数）を crx-repository\ リポジトリフォルダーにコピーし、セカンダリリポジトリフォルダーを削除します。
* クラスターノードを再起動する前に、プライマリノードからリポジトリ /clusterd.txt を削除します。
* 最初にプライマリノードを起動し、それが完全に立ち上がったら、他のノードを起動します。

### クラスター全体の復元 {#restoring-the-entire-cluster}

1. すべてのクラスターノードを停止します。
1. システムイメージから物理システムを再作成します。
1. イメージの作成後に適用されたパッチまたはアップデートを AEM Forms に適用します。この情報は、バックアップ手順の手順 1 で記録されたものです。システムをバックアップしたときと同じパッチレベルに AEM forms を回復する必要があります。
1. データベース、GDS、およびコネクタを復元します。
1. 次の手順を実行して、AEM リポジトリをオフラインで復元します。

   >[!NOTE]
   >
   >圧縮された crx-repository バックアップがオンラインになった場合は、任意の場所で展開し、オフラインの復元プロセスに従います。

   1. すべてのクラスターノードで、clusterNode ディレクトリ内の repository、shared、version、および workspaces ディレクトリを削除します。
   1. 共有ディレクトリ内のすべてのファイルとディレクトリを削除します。
   1. クラスターノード（サブディレクトリを含む）のバックアップをクラスターの 1 つのノードに復元します。
   1. 復元したクラスターノードのすべてのファイルを、その他のすべてのクラスターノードにコピーします。この作業が完了すれば、各クラスターノードには同じデータが含まれます。
   1. すべてのクラスターノードで clusterNode/revision.log ファイルを削除します。
   1. .lock がある場合は、すべてのクラスターノードでそれを削除します。
   1. repository/system.id がある場合は、すべてのクラスターノードでそれを削除します。
   1. すべてのクラスターノードで &amp;ast;&amp;ast;/listener.properties ファイルが存在する場合は削除します。
   1. クラスターノードごとに、repository/cluster_node.id を復元します。

>[!NOTE]
>
>次の点を考慮してください。

* 障害ノードが AEM プライマリノードの場合は、セカンダリリポジトリフォルダーのすべてのコンテンツ（crx-repository\crx.0000 のようなもので、0000 は任意の桁数）を crx-repository\ リポジトリフォルダーにコピーします。
* クラスターノードを再起動する前に、プライマリノードからリポジトリ /clusterd.txt を削除します。
* 最初にプライマリノードを起動し、それが完全に立ち上がったら、他のノードを起動します。

## Correspondence Management Solution パブリッシュノードのバックアップと復元 {#back-up-and-restore-correspondence-management-solution-publish-node}

パブリッシャーノードは、クラスター環境ではプライマリとセカンダリの関係がありません。パブリッシャーノードのバックアップは、「[バックアップと復元](https://helpx.adobe.com/jp/experience-manager/kb/CRXBackupAndRestoreProcedure.html)」に従って行うことができます。

### 単一パブリッシャーノードの復元 {#recover-a-single-publisher-node}

1. 回復する必要のあるノードをシャットダウンし、そのノードが再び立ち上がるまではパブリッシュ作業を行わないようにします。
1. [復元とバックアップ](https://helpx.adobe.com/jp/experience-manager/kb/CRXBackupAndRestoreProcedure.html)に従って、パブリッシュノードを復元します。

### クラスターの復元 {#recover-a-cluster}

1. クラスターをシャットダウンします。
1. [復元とバックアップ](https://helpx.adobe.com/jp/experience-manager/kb/CRXBackupAndRestoreProcedure.html)に従って、パブリッシュノードを復元します。
1. オーサークラスターのプライマリノードを起動してからセカンダリノードを起動します。
