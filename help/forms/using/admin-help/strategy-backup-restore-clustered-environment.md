---
title: クラスター環境でのバックアップと復元の方策
seo-title: Strategy for backup and restore in a clustered environment
description: AEM forms の実装環境で、追加のカスタムデータを別のデータベースに格納する場合は、そのデータをバックアップする方法を導入し、AEM forms のデータと同期を維持する必要があります。
seo-description: If your AEM forms implementation stores additional custom data in a different database, you must implement a strategy to back up this data ensuring that it remains in sync with the AEM forms data.
uuid: c29b989c-30ed-4a8e-bab8-9b7746291a33
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c332985b-4556-4056-961a-fce2356da88d
exl-id: 98c96349-f253-475f-b646-352269814a38
source-git-commit: 4fa868f3ae4778d3a637e90b91f7c5909fe5f8aa
workflow-type: tm+mt
source-wordcount: '1416'
ht-degree: 20%

---

# クラスター環境でのバックアップと復元の方策 {#strategy-for-backup-and-restore-in-a-clustered-environment}

>[!NOTE]
>
>AEM forms の実装環境で、追加のカスタムデータを別のデータベースに格納する場合は、そのデータをバックアップする方法を導入し、AEM forms のデータと同期を維持する必要があります。 また、追加のデータベースが同期しなくなるシナリオに対応できる堅牢性を備えたアプリケーションを設計する必要があります。 実行するデータベース操作は、トランザクションのコンテキストで実行し、一貫性のある状態を維持することを強くお勧めします。

エラーから回復するには、AEM forms システムの次の部分をバックアップする必要があります。

* AEM forms で使用されるデータベース
* 長期間有効なデータとその他の永続的なドキュメントを持つ GDS
* AEMデータベース (crx-repository)

>[!NOTE]
>
>カスタマーフォント、コネクタデータなど、AEM forms の設定で使用されている他のデータをバックアップする必要があります。

## クラスター環境のバックアップ {#back-up-a-clustered-environment}

このトピックでは、AEM forms クラスター環境をバックアップする次の方法について説明します。

* ダウンタイムを伴うオフラインバックアップ
* ダウンタイムを必要としないオフラインバックアップ（シャットダウンされているセカンダリノードのバックアップ）
* ダウンタイムなしで応答の遅延を伴うオンラインバックアップ
* Bootstrapプロパティファイルのバックアップ

### ダウンタイムを伴うオフラインバックアップ {#offline-backup-with-downtime}

1. クラスター全体と関連サービスをシャットダウンします。 ( [サービスの開始と停止](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. 任意のノードで、データベース、GDS およびコネクタをバックアップします。 ( [バックアップおよびリカバリするファイル](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. AEMリポジトリをオフラインでバックアップするには、次の手順を実行します。

   1. 各クラスターノードに対して、クラスターノード ID を含むファイルをバックアップします。
   1. すべてのセカンダリクラスターノードのすべてのファイル（サブディレクトリも含む）をバックアップします。
   1. 各クラスターノードのリポジトリ / システム ID を別々にバックアップします。

   詳細な手順については、 [バックアップと復元](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html).

1. カスタマーフォントなど、その他のデータをバックアップします。
1. クラスターを再起動します。

### ダウンタイムなしのオフラインバックアップ {#offline-backup-with-no-downtime}

1. ローリングバックアップモードに入ります。 ( [バックアップモードの開始](/help/forms/using/admin-help/backing-aem-forms-data.md#entering-the-backup-modes))

   リカバリ後は、ローリングバックアップモードを終了します。

1. AEMに関するクラスターのセカンダリノードをシャットダウンします。 ( [サービスの開始と停止](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. 任意のノードで、データベース、GDS およびコネクタをバックアップします。 ( [バックアップおよびリカバリするファイル](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. AEMリポジトリをオフラインでバックアップするには、次の手順を実行します。

   1. 各クラスターノードに対して、クラスターノード ID を含むファイルをバックアップします。
   1. すべてのセカンダリクラスターノードのすべてのファイル（サブディレクトリも含む）をバックアップします。
   1. 各クラスターノードのリポジトリ / system.id を別々にバックアップします。

   詳細な手順については、 [バックアップと復元](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html).

1. カスタマーフォントなど、その他のデータをバックアップします。
1. クラスターを再起動します。

### ダウンタイムなしで応答の遅延を伴うオンラインバックアップ {#online-backup-with-no-downtime-but-delay-in-response}

1. ローリングバックアップモードに入ります。 ( [バックアップモードの開始](/help/forms/using/admin-help/backing-aem-forms-data.md#entering-the-backup-modes))

   リカバリ後は、ローリングバックアップモードを終了します。

1. AEMに関するクラスターのセカンダリノードをシャットダウンします。 ( [サービスの開始と停止](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services))
1. 任意のノードで、データベース、GDS およびコネクタをバックアップします。 ( [バックアップおよびリカバリするファイル](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover))
1. AEMリポジトリをオンラインでバックアップするには、次の手順を実行します。

   1. 各クラスタノードに対して、 cluster_node.id を含むファイルをバックアップします。
   1. 各クラスターノードのリポジトリ / system.id を別々にバックアップします。
   1. 任意のセカンダリノード上で、リポジトリのオンラインバックアップを行います。手順について詳しくは「オンラインバックアップ」を参照してください。

1. カスタマーフォントなど、その他のデータをバックアップします。
1. クラスターを再起動します。

### Bootstrapプロパティファイルのバックアップ {#back-up-the-bootstrap-properties-file}

AEM クラスターを作成すると、すべてのセカンダリノードに対してアプリケーションサーバー内にプロパティファイルが作成されます。Bootstrap・プロパティ・ファイルをバックアップすることをお勧めします。 ファイルは、アプリケーションサーバー上の次の場所にあります。

* JBoss®:BIN ディレクトリ内
* WebLogic:ドメインディレクトリ内
* WebSphere®:プロファイルディレクトリ内

AEMセカンダリ・ノードの災害復旧シナリオ用のファイルをバックアップし、リストアされた場合は、アプリケーション・サーバ上の指定した場所に置き換えます。

## クラスター環境での回復 {#recovery-in-a-clustered-environment}

クラスタ全体または単一のノードに障害が発生した場合は、バックアップを使用して復元します。

単一ノードのリカバリの場合は、単一ノードをシャットダウンし、単一ノードのリカバリ手順を実行します。

データベースのクラッシュなどの障害が原因でクラスター全体が失敗した場合は、次の手順を実行します。 復元は、使用するバックアップの方法によって異なります。

### 単一ノードの復元 {#restoring-a-single-node}

1. 破損したノードを停止します。

   >[!NOTE]
   >
   >障害ノードが AEM プライマリノードの場合は、クラスターノード全体をシャットダウンします。

1. システムイメージから物理システムを再作成します。
1. イメージの作成後に適用されたAEM forms にパッチまたはアップデートを適用します。 この情報は、バックアップ手順中に記録されました。 AEM forms は、システムのバックアップ時と同じパッチレベルに復元する必要があります。
1. (*オプション*) その他のすべてのノードが正常に動作している場合は、AEMリポジトリも破損している可能性があります。 この場合、AEMリポジトリの error.log ファイルにリポジトリの非同期メッセージが表示されます。

   リポジトリを復元するには、次の手順を実行します。

   >[!NOTE]
   >
   >圧縮された crx-repository バックアップがオンラインになった場合は、任意の場所で展開し、オフラインの復元プロセスに従います。

   1. ノードの clusterNode ディレクトリにある repository、shared、version および workspaces ディレクトリを削除します。
   1. クラスターノード（サブディレクトリも含む）のバックアップをノードに復元します。
   1. ノードのclusterNode/revision.logファイルを削除します。
   1. ノードに.lock が存在する場合は、そのノードを削除します。
   1. ノードにrepository/system.idが存在する場合は、そのノードを削除します。
   1. ノード上に &amp;ast;&amp;ast;/listener.properties ファイルが存在する場合は削除します。
   1. 個々のクラスターノードに対してrepository/cluster_node.idを復元します。

>[!NOTE]
>
>次の点を考慮してください。

* 障害ノードが AEM プライマリノードの場合は、セカンダリリポジトリフォルダーのすべてのコンテンツ（crx-repository\crx.0000、ここで 0000 は任意の桁数）を crx-repository\ リポジトリフォルダーにコピーし、セカンダリリポジトリフォルダーを削除します。
* クラスターノードを再起動する前に、プライマリノードからリポジトリ /clusterd.txt を削除します。
* プライマリノードが最初に起動し、起動後に他のノードを起動します。

### クラスター全体の復元 {#restoring-the-entire-cluster}

1. すべてのクラスターノードを停止します。
1. システムイメージから物理システムを再作成します。
1. イメージの作成後に適用されたAEM forms にパッチまたはアップデートを適用します。 この情報は、バックアップ手順の手順 1 で記録されました。 AEM forms は、システムのバックアップ時と同じパッチレベルに復元する必要があります。
1. データベース、GDS、およびコネクタを復元します。
1. 次の手順を実行して、AEMリポジトリをオフラインで復元します。

   >[!NOTE]
   >
   >圧縮された crx-repository バックアップがオンラインになった場合は、任意の場所で展開し、オフラインの復元プロセスに従います。

   1. すべてのクラスターノードで、clusterNode ディレクトリ内の repository、shared、version、および workspaces ディレクトリを削除します。
   1. 共有ディレクトリ内のすべてのファイルとディレクトリを削除します。
   1. クラスターノード（サブディレクトリを含む）のバックアップを 1 つのクラスターノードに復元します。
   1. 復元したクラスターノードのすべてのファイルを、他のすべてのクラスターノードにコピーします。 完了すると、各クラスターノードに同じデータが含まれます。
   1. すべてのクラスターノードでclusterNode/revision.logファイルを削除します。
   1. すべてのクラスターノードに.lock が存在する場合は、それを削除します。
   1. repository/system.idすべてのクラスターノードが存在する場合は削除します。
   1. すべてのクラスターノードで &amp;ast;&amp;ast;/listener.properties ファイルが存在する場合は削除します。
   1. 個々のクラスターノードに対してrepository/cluster_node.idを復元します。

>[!NOTE]
>
>次の点を考慮してください。

* 障害ノードが AEM プライマリノードの場合は、セカンダリリポジトリフォルダーのすべてのコンテンツ（crx-repository\crx.0000 のようなもので、0000 は任意の桁数）を crx-repository\ リポジトリフォルダーにコピーします。
* クラスターノードを再起動する前に、プライマリノードからリポジトリ /clusterd.txt を削除します。
* プライマリノードが最初に起動し、起動後に他のノードを起動します。

## Correspondence Management Solution パブリッシュノードのバックアップと復元 {#back-up-and-restore-correspondence-management-solution-publish-node}

パブリッシャーノードは、クラスター環境ではプライマリとセカンダリの関係がありません。任意のパブリッシャーノードのバックアップを作成するには、次の手順を実行します [バックアップと復元](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html).

### 単一のパブリッシャーノードを復元する {#recover-a-single-publisher-node}

1. 復元が必要なノードをシャットダウンし、ノードが再び立ち上がるまで公開アクティビティを実行しないでください。
1. 次を使用してパブリッシュノードを復元します。 [バックアップの復元](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html).

### クラスターの復元 {#recover-a-cluster}

1. クラスタをシャットダウンします。
1. 次を使用してパブリッシュノードを復元します。 [バックアップの復元](https://helpx.adobe.com/experience-manager/kb/CRXBackupAndRestoreProcedure.html).
1. 作成者クラスターのプライマリノードを起動してからセカンダリノードを起動します。
