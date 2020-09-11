---
title: MongoDB をデモ用に設定する方法
seo-title: MongoDB をデモ用に設定する方法
description: 1 つのオーサーインスタンスと 1 つのパブリッシュインスタンス用に MSRP をセットアップする方法
seo-description: 1 つのオーサーインスタンスと 1 つのパブリッシュインスタンス用に MSRP をセットアップする方法
uuid: d2035a9e-f05c-4f90-949d-7cdae9646750
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 0b126218-b142-4d33-a28c-a91ab4fe99ac
translation-type: tm+mt
source-git-commit: 94bc3550a7e18b9203e7a0d495d195d7b798e012
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 55%

---


# MongoDB をデモ用に設定する方法 {#how-to-setup-mongodb-for-demo}

## 概要 {#introduction}

This tutorial describes how to setup [MSRP](msrp.md) for *one author* instance and *one publish* instance.

このセットアップを終えると、ユーザー生成コンテンツ（UGC）のフォワードまたはリバースレプリケーションをおこなわずに、オーサー環境とパブリッシュ環境の両方からコミュニティコンテンツにアクセスできるようになります。

この設定は、開発用やデモ用の環境など、*非実稼動*&#x200B;環境に適しています。

**実稼動環境では、以下のことが必要です。****

* レプリカ・セットでMongoDBを実行
* SolrCloudを使用
* 複数のパブリッシャーインスタンスを含む

## MongoDB {#mongodb}

### MongoDB のインストール {#install-mongodb}

* Download MongoDB from [https://www.mongodb.org/](https://www.mongodb.org/)

   * OSの選択：

      * Linux
      * Mac 10.8
      * Windows 7
   * バージョンの選択：

      * 少なくともバージョン2.6を使用してください


* 基本設定

   * MongoDBのインストール手順に従います。
   * Mongod用の設定：

      * モンゴや共有を設定する必要はありません。
   * インストールされたMongoDBフォルダは&lt;mongo-install>と呼ばれます。
   * 定義されたデータ・ディレクトリ・パスは、&lt;mongo-dbpath>と呼ばれます。


* MongoDBはAEMと同じホスト上で実行するか、リモートで実行できます。

### MongoDB を起動します。{#start-mongodb}

* &lt;mongo-install>/bin/mongod --dbpath &lt;mongo-dbpath>

すると MongoDB サーバーが起動します。使用されるデフォルトポートは 27017 です。

* Mac では、起動引数「ulimit -n 2048」を使用して ulimit を増やします。

>[!NOTE]
>
>If MongoDB is started *after* AEM, **restart** all **AEM** instances so they properly connect to MongoDB.


### 実稼動デモのオプション：MongoDB レプリカセットのセットアップ {#demo-production-option-setup-mongodb-replica-set}

以下のコマンドは、ローカルホストに 3 つのノードを持つレプリカセットの設定例です。

* `bin/mongod --port 27017 --dbpath data --replSet rs0&`
* `bin/mongo`

   * `cfg = {"_id": "rs0","version": 1,"members": [{"_id": 0,"host": "127.0.0.1:27017"}]}`
   * `rs.initiate(cfg)`

* `bin/mongod --port 27018 --dbpath data1 --replSet rs0&`
* `bin/mongod --port 27019 --dbpath data2 --replSet rs0&`
* `bin/mongo`

   * `rs.add("127.0.0.1:27018")`
   * `rs.add("127.0.0.1:27019")`
   * `rs.status()`

## Solr {#solr}

### Solr のインストール {#install-solr}

* Download Solr from [Apache Lucene](https://archive.apache.org/dist/lucene/solr/):

   * 任意のOSに適しています。
   * Solrバージョン7.0。
   * SolrではJava 1.7以降が必要です。

* 基本設定

   * 「例」Solr設定に従います。
   * サービスは不要です。
   * インストールされたSolrフォルダは、&lt;solr-install>と呼ばれます。

### AEM Communities のための Solr の設定 {#configure-solr-for-aem-communities}

MSRP のための Solr コレクションをデモ目的で設定するには、以下の 2 点を決定する必要があります（詳しくは、主なドキュメントへのリンクを選択してください）。

1. Run Solr in standalone or [SolrCloud mode](msrp.md#solrcloudmode).
1. Install [standard](msrp.md#installingstandardmls) or [advanced](msrp.md#installingadvancedmls) multilingual search (MLS).

### スタンドアロンの Solr {#standalone-solr}

Solr を実行する方法は、バージョンとインストール方法によって異なる場合があります。詳しくは、公式ドキュメントである [Solr リファレンスガイド](https://archive.apache.org/dist/lucene/solr/ref-guide/)を参照してください。

ここでは簡単に、バージョン 4.10 を使用して、Solr をスタンドアロンモードで起動します。

* cd to &lt;solrinstall>/example
* java -jar start.jar

これにより、Solr HTTP サーバーが起動します。使用されるデフォルトポートは 8983 です。Solr コンソールを参照し、Solr コンソールを試しに開くことができます。

* デフォルトの Solr コンソール：[http://localhost:8983/solr/](http://localhost:8983/solr/)

>[!NOTE]
>
>Solr コンソールが使用できない場合は、&lt;solrinstall>/example/logs にあるログを確認します。SOLRが解決できない特定のホスト名(例：&quot;user-macbook-pro&quot;)。
その場合、このホスト名の新しいエントリ（127.0.0.1 user-macbook-pro など）を使用して etc/hosts ファイルを更新します。すると Solr が適切に起動します。


### SolrCloud {#solrcloud}

非常に基本的な（実稼動用ではない）solrCloud のセットアップを実行するには、以下のコマンドで Solr を起動します。

* `java -Dbootstrap_confdir=./solr/collection1/conf -Dbootstrap_conf=true -DzkRun -jar start.jar`

##  MongoDB を共通ストアとして指定{#identify-mongodb-as-common-store}

AEM オーサーインスタンスとパブリッシュインスタンスを起動します（必要な場合）。

AEM が MongoDB を起動する前に実行されている場合、AEM インスタンスを再起動する必要があります。

詳しくは、[MSRP - MongoDB 共通ストア](msrp.md)の手順に従ってください。

## テスト {#test}

MongoDB 共通ストアをテストおよび検証するために、パブリッシュインスタンスにコメントを投稿して、オーサーインスタンスでそのコメントを表示し、さらに MongoDB と Solr で UGC を表示します。

1. On the publish instance, browse to the [Community Components Guide](http://localhost:4503/content/community-components/en/comments.html) page and select the Comments component.
1. サインインしてコメントを投稿する：
1. Enter text in the comment text entry box and click **[!UICONTROL Post]**

   ![chlimage_1-191](assets/chlimage_1-191.png)

1. Simply view the comment on the [author instance](http://localhost:4502/content/community-components/en/comments.html) (likely still signed in as admin / admin).

   ![chlimage_1-192](assets/chlimage_1-192.png)

   注意：オーサーインスタンスの *asipath* の下には JCR ノードがありますが、これらは SCF フレームワーク用のものです。実際のUGCはJCRにはなく、MongoDBにあります。

1. View the UGC in mongodb **[!UICONTROL Communities]** > **[!UICONTROL Collections]** > **[!UICONTROL Content]**

   ![chlimage_1-193](assets/chlimage_1-193.png)

1. UGCをSolrで表示:

   * Browse to Solr dashboard: [http://localhost:8983/solr/](http://localhost:8983/solr/)
   * 選択 `core selector` するユーザー `collection1`
   *  `Query`
   *  `Execute Query`

   ![chlimage_1-194](assets/chlimage_1-194.png)

## トラブルシューティング {#troubleshooting}

### UGC が表示されない {#no-ugc-appears}

1. MongoDBが正しくインストールされ、動作していることを確認します。

1. MSRPがデフォルトのプロバイダーに設定されていることを確認します。

   * すべての作成者および発行AEMインスタンスで、 [ストレージ設定コンソールに再度アクセスします](srp-config.md)

   または、AEMリポジトリを確認します。

   * In JCR, if [/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/)

   * Does not contain an [srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc) node, it means the storage provider is JSRP
   * If the srpc node exists and contains node [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration), the defaultconfiguration&#39;s properties should define MSRP to be the default provider


1. MSRPを選択した後にAEMが再起動されたことを確認します。
