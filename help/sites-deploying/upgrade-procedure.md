---
title: アップグレード手順
seo-title: アップグレード手順
description: AEM のアップグレード手順について説明します。
seo-description: AEM のアップグレード手順について説明します。
uuid: 81126a70-c082-4f01-a1ad-7152182da88b
contentOwner: sarchiz
topic-tags: upgrading
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: 5c035d4c-6e03-48b6-8404-800b52d659b8
docset: aem65
targetaudience: target-audience upgrader
translation-type: tm+mt
source-git-commit: 5f8198f0fd6c335708f2b771848b2e66dfc242b3
workflow-type: tm+mt
source-wordcount: '835'
ht-degree: 93%

---


# アップグレード手順 {#upgrade-procedure}

>[!NOTE]
>
>ほとんどの AEM のアップグレードはインプレースで実行されるので、アップグレードにはオーサー層のダウンタイムが必要になります。これらのベストプラクティスに従うことによって、パブリッシュ層のダウンタイムを最小限に抑えたり、排除したりすることができます。

AEM 環境をアップグレードする場合は、作成者とエンドユーザーのダウンタイムを最小化するために、オーサー環境とパブリッシュ環境のアップグレードのアプローチの違いを考慮する必要があります。このページでは、AEM 6.x のバージョンで現在実行されている AEM トポロジをアップグレードする手順の概要を説明します。オーサー層とパブリッシュ層および Mongo ベースと TarMK ベースのデプロイメントではプロセスが異なるので、各層およびマイクロカーネルは個別の節に記載されています。デプロイメントを実行するときは、最初にオーサー環境をアップグレードし、成功を確認してから、パブリッシュ環境をアップグレードすることをお勧めします。

<!--
>[!IMPORTANT]
>
>The downtime during the upgrade can be significally reduced by indexing the repository before performing the upgrade. For more information, see [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)
-->

## TarMK のオーサー層 {#tarmk-author-tier}

### トポロジの開始 {#starting-topology}

この節で想定されるトポロジは、TarMK で実行されているオーサーサーバーとコールドスタンバイで構成されています。オーサーサーバーから TarMK パブリッシュファームにレプリケーションがおこなわれます。ここには示されていませんが、このアプローチは、オフロードを使用するデプロイメントでも活用できます。オーサーインスタンスでレプリケーションエージェントを無効にして再度有効にする前に、新しいバージョンでオフロードインスタンスをアップグレードまたは再構築してください。

![tarmk_starting_topology](assets/tarmk_starting_topology.jpg)

### アップグレードの準備 {#upgrade-preparation}

![upgrade-preparation-author](assets/upgrade-preparation-author.png)

1. コンテンツのオーサリングを停止します。

1. スタンバイインスタンスを停止します。

1. オーサーのレプリケーションエージェントを無効にします。

1. [アップグレード前のメンテナンスタスク](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)を実行します。

### アップグレードの実行 {#upgrade-execution}

![execute_upgrade](assets/execute_upgrade.jpg)

1. [インプレースアップグレード](/help/sites-deploying/in-place-upgrade.md)を実行します。
1. *必要に応じて*、Dispatcher モジュールを更新します。

1. QA がアップグレードを検証します。

1. オーサーインスタンスをシャットダウンします。

### 成功した場合 {#if-successful}

![if_successful](assets/if_successful.jpg)

1. 新しいコールドスタンバイを作成するために、アップグレードされたインスタンスをコピーします。

1. オーサーインスタンスを起動します。

1. スタンバイインスタンスを起動します。

### If Unsuccessful (Rollback) {#if-unsuccessful-rollback}

![ロールバック](assets/rollback.jpg)

1. コールドスタンバイインスタンスを新しいプライマリとして起動します。

1. コールドスタンバイからオーサー環境を再構築します。

## MongoMK オーサークラスター {#mongomk-author-cluster}

### トポロジの開始 {#starting-topology-1}

この節で想定されるトポロジは、2 つ以上の MongoMK データベースを使用する 2 つ以上の AEM オーサーインスタンスを含む MongoMK オーサークラスターで構成されています。すべてのオーサーインスタンスは 1 つのデータストアを共有します。以下の手順は、S3 データストアとファイルデータストアの両方に適用できます。オーサーサーバーから TarMK パブリッシュファームへのレプリケーションが発生します。

![モンゴトポロジー](assets/mongo-topology.jpg)

### アップグレードの準備 {#upgrade-preparation-1}

![mongo_upgrade_prep](assets/mongo-upgrade_prep.jpg)

1. コンテンツのオーサリングを停止します。
1. バックアップ用のデータストアのクローンを作成します。
1. 1 つの AEM オーサーインスタンス（プライマリオーサー）以外をすべて停止します。
1. 1つを除くすべてのMongoDBノードをレプリカセットから削除します。プライマリMongoインスタンスです
1. Update the `DocumentNodeStoreService.cfg` file on the primary Author to reflect your single member replica set
1. プライマリオーサーを再起動して、正常に再起動することを確認します。
1. プライマリオーサーのレプリケーションエージェントを無効にします。
1. プライマリオーサーインスタンスで[アップグレード前のメンテナンスタスク](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)を実行します。
1. 必要に応じて、プライマリ Mongo インスタンスの MongoDB を WiredTiger が搭載されたバージョン 3.2 にアップグレードします。

### アップグレードの実行 {#Upgrade-execution-1}

![モンゴ処刑](assets/mongo-execution.jpg)

1. プライマリオーサーで[インプレースアップグレード](/help/sites-deploying/in-place-upgrade.md)を実行します。
1. *必要に応じて*、Dispatcher モジュールまたは Web モジュールを更新します。
1. QA がアップグレードを検証します。

### 成功した場合 {#if-successful-1}

![モンゴ秒](assets/mongo-secondaries.jpg)

1. アップグレードされた Mongo インスタンスに接続する新しい 6.5 オーサーインスタンスを作成します。

1. クラスターから削除された MongoDB ノードを再構築します。

1. レプリカのフルセットが反映されるように、`DocumentNodeStoreService.cfg` ファイルを更新します。

1. オーサーインスタンスを 1 つずつ再起動します。

1. クローン作成されたデータストアを削除します。

### If Unsuccessful (Rollback)  {#if-unsuccessful-rollback-2}

![1回のロールバック](assets/mongo-rollback.jpg)

1. クローン作成されたデータストアに接続するために、セカンダリオーサーインスタンスを再設定します。

1. アップグレードされたオーサープライマリインスタンスをシャットダウンします。

1. アップグレードされた Mongo プライマリインスタンスをシャットダウンします。

1. セカンダリ Mongo インスタンスを起動し、そのうちの 1 つを新しいプライマリとして設定します。

1. アップグレードされていない Mongo インスタンスのレプリカセットを指すように、セカンダリオーサーインスタンスで `DocumentNodeStoreService.cfg` ファイルを設定します。

1. セカンダリオーサーインスタンスを起動します。

1. アップグレードされたオーサーインスタンス、Mongo ノードおよびデータストアをクリーンアップします。

## TarMK パブリッシュファーム {#tarmk-publish-farm}

### TarMK パブリッシュファーム {#tarmk-publish-farm-1}

この節で想定されるトポロジは、ロードバランサーと Dispatcher を介して動作する 2 つの TarMK パブリッシュインスタンスで構成されています。オーサーサーバーから TarMK パブリッシュファームにレプリケーションがおこなわれます。

![tarmk-pub-farmv5](assets/tarmk-pub-farmv5.png)

### アップグレードの実行 {#upgrade-execution-2}

![upgrade-publish2](assets/upgrade-publish2.png)

1. ロードバランサーで Publish 2 インスタンスへのトラフィックを停止します。
1. Publish 2 で[アップグレード前のメンテナンスタスク](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)を実行します。
1. Publish 2 で[インプレースアップグレード](/help/sites-deploying/in-place-upgrade.md)を実行します。
1. *必要に応じて*、Dispatcher モジュールまたは Web モジュールを更新します。
1. Dispatcher キャッシュをフラッシュします。
1. QA が、ファイアウォールの後ろにある Dispatcher を介して Publish 2 を検証します。
1. Publish 2 をシャットダウンします。
1. Publish 2 インスタンスをコピーします。
1. Publish 2 を起動します。

### 成功した場合 {#if-successful-2}

![upgrade-publish1](assets/upgrade-publish1.png)

1. Publish 2 へのトラフィックを有効にします。
1. Publish 1 へのトラフィックを停止します。
1. Publish 1 インスタンスを停止します。
1. Publish 1 インスタンスを Publish 2 のコピーに置き換えます。
1. *必要に応じて*、Dispatcher モジュールまたは Web モジュールを更新します。
1. Publish 1 の Dispatcher キャッシュをフラッシュします。
1. Publish 1 を起動します。
1. QA が、ファイアウォールの後ろにある Dispatcher を介して Publish 1 を検証します。

### If Unsuccessful (Rollback) {#if-unsuccessful-rollback-1}

![pub_rollback](assets/pub_rollback.jpg)

1. Publish 1 のコピーを作成します。
1. Publish 2 インスタンスを Publish 1 のコピーに置き換えます。
1. Publish 2 の Dispatcher キャッシュをフラッシュします。
1. Publish 2 を起動します。
1. QA が、ファイアウォールの後ろにある Dispatcher を介して Publish 2 を検証します。
1. Publish 2 へのトラフィックを有効にします。

## アップグレードの最終手順 {#final-upgrade-steps}

1. Publish 1 へのトラフィックを有効にします。
1. QA がパブリック URL から最終検証を実行します。
1. オーサー環境からレプリケーションエージェントを有効にします。
1. コンテンツのオーサリングを再開します。
1. [アップグレード後のチェック](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)を実行します。

![final](assets/final.jpg)

