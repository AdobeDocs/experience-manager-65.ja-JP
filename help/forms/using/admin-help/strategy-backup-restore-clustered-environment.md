---
title: クラスター環境でのバックアップと復元の方策
seo-title: Strategy for backup and restore in a clustered environment
description: AEM Forms の実装で、追加のカスタムデータを異なるデータベースに格納する場合、そのカスタムデータをバックアップするための方法を導入し、AEM Forms データと同期させる必要があります。
seo-description: If your AEM forms implementation stores additional custom data in a different database, you must implement a strategy to back up this data ensuring that it remains in sync with the AEM forms data.
uuid: c29b989c-30ed-4a8e-bab8-9b7746291a33
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/aem_forms_backup_and_recovery
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c332985b-4556-4056-961a-fce2356da88d
exl-id: 98c96349-f253-475f-b646-352269814a38
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '1476'
ht-degree: 100%

---

# クラスター環境でのバックアップと復元の方策 {#strategy-for-backup-and-restore-in-a-clustered-environment}

>[!NOTE]
>
>AEM forms の実装で、追加のカスタムデータを異なるデータベースに格納する場合、そのカスタムデータをバックアップするための方法を導入し、AEM forms データと同期させる必要があります。また、追加のデータベースを同期しないシナリオにも対処できるように、アプリケーションを堅牢な方法で設計する必要があります。一貫性のある状態を維持するために、実行するデータベース操作をトランザクションコンテキストで行うことを強くお勧めします。

エラーから回復するためには、AEM Forms システムの次の部分をバックアップする必要があります。

* AEM Forms が使用するデータベース
* 長期のデータおよびその他の永続的なドキュメントを持つ GDS
* AEM データベース (crx-repository)

>[!NOTE]
>
>AEM Forms セットアップで使用されているその他のデータ（例えば、カスタマーフォント、コネクターデータなど）をすべてバックアップする必要があります。

## クラスター環境のバックアップ {#back-up-a-clustered-environment}

ここでは、AEM Forms クラスター環境をバックアップする次の方策について検討します。

* ダウンタイムを必要とするオフラインバックアップ
* ダウンタイムを必要としないオフラインバックアップ（シャットダウンされているセカンダリノードのバックアップ）
* ダウンタイムを必要としないがレスポンスに遅れが生じるオンラインバックアップ
* ブートストラッププロパティファイルのバックアップ

### ダウンタイムを必要とするオフラインバックアップ {#offline-backup-with-downtime}

1. クラスターと関連サービス全体をシャットダウンします（[サービスの開始と停止](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services)を参照してください）。
1. 任意のノード上で、データベース、GDS、およびコネクターをバックアップします（[バックアップおよび回復するファイル](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover)を参照してください）。
1. AEM リポジトリをオフラインでバックアップするには、次の手順を実行します。

   1. 各クラスターノードごとに、クラスターノード ID を持つファイルをバックアップします。
   1. すべてのセカンダリクラスターノードのすべてのファイル（サブディレクトリも含む）をバックアップします。
   1. 各クラスターノードのリポジトリ / システム ID を別々にバックアップします。

   手順について詳しくは、「[バックアップと復旧](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html)」を参照してください。

1. カスタマーフォントなど、その他すべてのデータをバックアップします。
1. クラスターを再び起動します。

### ダウンタイムを必要としないオフラインバックアップ {#offline-backup-with-no-downtime}

1. ローリングバックアップモードに入ります（[バックアップモードの開始](/help/forms/using/admin-help/backing-aem-forms-data.md#entering-the-backup-modes)を参照してください）。

   回復後にローリングバックアップモードを終了する必要があることに注意してください。

1. AEM に関してクラスターのセカンダリノードをすべてシャットダウンします。（[サービスの開始と停止](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services)を参照してください）。
1. 任意のノード上で、データベース、GDS、およびコネクターをバックアップします（[バックアップおよび回復するファイル](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover)を参照してください）。
1. AEM リポジトリをオフラインでバックアップするには、次の手順を実行します。

   1. 各クラスターノードごとに、クラスターノード ID を持つファイルをバックアップします。
   1. すべてのセカンダリクラスターノードのすべてのファイル（サブディレクトリも含む）をバックアップします。
   1. 各クラスターノードのリポジトリ / system.id を別々にバックアップします。

   手順について詳しくは、「[バックアップと復旧](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html)」を参照してください。

1. カスタマーフォントなど、その他すべてのデータをバックアップします。
1. クラスターを再び起動します。

### ダウンタイムを必要としないがレスポンスに遅れが生じるオンラインバックアップ {#online-backup-with-no-downtime-but-delay-in-response}

1. ローリングバックアップモードに入ります（[バックアップモードの開始](/help/forms/using/admin-help/backing-aem-forms-data.md#entering-the-backup-modes)を参照してください）。

   回復後にローリングバックアップモードを終了する必要があることに注意してください。

1. AEM に関してクラスターのセカンダリノードをすべてシャットダウンします。（[サービスの開始と停止](/help/forms/using/admin-help/starting-stopping-services.md#starting-and-stopping-services)を参照してください）。
1. 任意のノード上で、データベース、GDS、およびコネクターをバックアップします（[バックアップおよび回復するファイル](/help/forms/using/admin-help/files-back-recover.md#files-to-back-up-and-recover)を参照してください）。
1. AEM リポジトリをオンラインでバックアップするには、次の手順を実行します。

   1. 各クラスターノードごとに、cluster_node.id を持つファイルをバックアップします。
   1. 各クラスターノードのリポジトリ / system.id を別々にバックアップします。
   1. 任意のセカンダリノード上で、リポジトリのオンラインバックアップを行います。手順について詳しくは「オンラインバックアップ」を参照してください。

1. カスタマーフォントなど、その他すべてのデータをバックアップします。
1. クラスターを再び起動します。

### ブートストラッププロパティファイルのバックアップ {#back-up-the-bootstrap-properties-file}

AEM クラスターを作成すると、すべてのセカンダリノードに対してアプリケーションサーバー内にプロパティファイルが作成されます。ブートストラッププロパティファイルをバックアップすることをお勧めします。このファイルは、アプリケーションサーバー上の次の場所にあります。

* JBoss: BIN ディレクトリ内
* WebLogic: ドメインディレクトリ内
* WebSphere: プロファイルディレクトリ内

AEM サカンダリノードの災害時復旧シナリオのためにこのファイルをバックアップし、リストアする場合はアプリケーションサーバーの指定場所でそれを置き換える必要があります。

## クラスター環境の回復 {#recovery-in-a-clustered-environment}

クラスター全体または単一ノードが故障した場合、バックアップを使ってそれを復元する必要があります。

単一ノードの回復の場合は、その単一ノードをシャットダウンし、単一ノード回復手順を実行する必要があります。

データベースのクラッシュなどの障害でクラスター全体が故障した場合は、次の手順を実行する必要があります。復元は、使用したバックアップの方法に依存します。

### 単一ノードの復元 {#restoring-a-single-node}

1. 障害ノードを停止します。

   >[!NOTE]
   >
   >障害ノードが AEM プライマリノードの場合は、クラスターノード全体をシャットダウンします。

1. システムイメージから物理システムを再作成します。
1. イメージの作成後に適用されたパッチまたはアップデートを AEM Forms に適用します。この情報は、バックアップ手順で記録されたものです。システムをバックアップしたときと同じパッチレベルに AEM Forms を回復する必要があります。
1. （*オプション*）その他すべてのノードが正常に機能している場合は、AEM リポジトリも障害がある可能性があります。この場合は、AEM リポジトリの error.log ファイル内にリポジトリ非同期メッセージがあります。

   リポジトリを復元するには、次の手順を実行します。

   >[!NOTE]
   >
   >圧縮された crx-repository バックアップをオンラインで取得した場合は、それを任意の場所に解凍し、オフライン復元プロセスに従ってください。

   1. ノードの clusterNode ディレクトリ内にある repository、shared、version、および workspaces ディレクトリを削除します。
   1. クラスターノードのバックアップ（サブディレクトリも含む）をノードに復元します。
   1. ノードにある clusterNode/revision.log ファイルを削除します。
   1. ノードに .lock がある場合は、それを削除します。
   1. ノードに repository/system.id がある場合は、それを削除します。
   1. ノード上に &amp;ast;&amp;ast;/listener.properties ファイルが存在する場合は削除します。
   1. 各クラスターノードごとに、repository/cluster_node.id を復元します。

>[!NOTE]
>
>次の点を考慮してください。

* 障害ノードが AEM プライマリノードの場合は、セカンダリリポジトリフォルダーのすべてのコンテンツ（crx-repository\crx.0000、ここで 0000 は任意の桁数）を crx-repository\ リポジトリフォルダーにコピーし、セカンダリリポジトリフォルダーを削除します。
* クラスターノードを再起動する前に、プライマリノードからリポジトリ /clusterd.txt を削除します。
* 最初にプライマリノードを起動し、それが完全に立ち上がったら、他のノードを起動します。

### クラスター全体の復元 {#restoring-the-entire-cluster}

1. すべてのクラスターノードを停止します。
1. システムイメージから物理システムを再作成します。
1. イメージの作成後に適用されたパッチまたはアップデートを AEM Forms に適用します。この情報は、バックアップの確認事項の最初の項目に基づいて、記録したものです。システムをバックアップしたときと同じパッチレベルに AEM Forms を回復する必要があります。
1. データベース、GDS、およびコネクターを復元します
1. 次の操作を実行して、AEM リポジトリをオフラインで回復します。

   >[!NOTE]
   >
   >圧縮された crx-repository バックアップをオンラインで取得した場合は、それを任意の場所に解凍し、オフライン復元プロセスに従ってください。

   1. すべてのクラスターノードで、clusterNode ディレクトリ内にある repository、shared、version、および workspaces ディレクトリを削除します。
   1. 共有ディレクトリ内にあるすべてのファイルとディレクトリを削除します。
   1. クラスターノードのバックアップ（サブディレクトリも含む）を 1 つのクラスターノードに復元します。
   1. 復元したクラスターノードのすべてのファイルを、その他のすべてのクラスターノードにコピーします。この作業が完了すれば、各クラスターノードには同じデータが含まれます。
   1. すべてのクラスターノードにある clusterNode/revision.log ファイルを削除します。
   1. すべてのクラスターノードで .lock がある場合は、それを削除します。
   1. すべてのクラスターノードで repository/system.id がある場合は、それを削除します。
   1. すべてのクラスターノードで &amp;ast;&amp;ast;/listener.properties ファイルが存在する場合は削除します。
   1. 各クラスターノードごとに、repository/cluster_node.id を復元します。

>[!NOTE]
>
>次の点を考慮してください。

* 障害ノードが AEM プライマリノードの場合は、セカンダリリポジトリフォルダーのすべてのコンテンツ（crx-repository\crx.0000 のようなもので、0000 は任意の桁数）を crx-repository\ リポジトリフォルダーにコピーします。
* クラスターノードを再起動する前に、プライマリノードからリポジトリ /clusterd.txt を削除します。
* 最初にプライマリノードを起動し、それが完全に立ち上がったら、他のノードを起動します。

## Correspondence Management Solution パブリッシュノードのバックアップと復元 {#back-up-and-restore-correspondence-management-solution-publish-node}

パブリッシャーノードは、クラスター環境ではプライマリとセカンダリの関係がありません。パブリッシャーノードのバックアップは、「[バックアップと復元](https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html)」に従って行うことができます。

### 単一パブリッシャーノードの回復 {#recover-a-single-publisher-node}

1. 回復する必要のあるノードをシャットダウンし、そのノードが再び立ち上がるまではパブリッシュ作業を行わないようにします。
1. [バックアップの復元]（https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html#Restoring the Backup）を使用してパブリッシュノードを復元します。

### クラスターの回復 {#recover-a-cluster}

1. クラスターをシャットダウンします。
1. [バックアップの復元]（https://docs.adobe.com/docs/en/crx/current/administering/backup_and_restore.html#Restoring the Backup）を使用してパブリッシュノードを復元します。
1. 作成者クラスターのプライマリノードを起動してからセカンダリノードを起動します。
