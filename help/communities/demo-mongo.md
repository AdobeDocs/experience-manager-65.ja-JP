---
title: MongoDB をデモ用に設定する方法
description: 1 つのオーサーインスタンスと 1 つのパブリッシュインスタンスに MSRP を設定する方法
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 7e257b34-a0f5-47db-b1a9-e26333c287d9
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 1%

---

# MongoDB をデモ用に設定する方法 {#how-to-setup-mongodb-for-demo}

## はじめに {#introduction}

このチュートリアルでは、の設定方法を説明します [MSRP](msrp.md) （用） *一人の著者* インスタンスと *1 件の公開* インスタンス。

この設定では、ユーザー生成コンテンツ（UGC）を転送またはリバースレプリケーションしなくても、オーサー環境とパブリッシュ環境の両方からコミュニティコンテンツにアクセスできます。

この設定は、 *実稼動以外* 開発やデモのための環境など。

**A *実稼動* 環境は以下を行う必要があります。**

* レプリカセットでの MongoDB の実行
* SolrCloud の使用
* 複数のパブリッシャーインスタンスを含む

## MongoDB {#mongodb}

### MongoDB のインストール {#install-mongodb}

* から MongoDB をダウンロード [https://www.mongodb.com/](https://www.mongodb.com/)

   * OS の選択：

      * Linux®
      * Mac 10.8
      * Windows 7

   * バージョンの選択：

      * 少なくとも、バージョン 2.6 を使用します

* 基本設定

   * MongoDB のインストール手順に従います。
   * mongod 用にを設定します。

      * Mongos やシャーディングを設定する必要はありません。

   * インストールされた MongoDB フォルダーは、です。 &lt;mongo-install>.
   * 定義されたデータディレクトリパスはと呼ばれます &lt;mongo-dbpath>.

* MongoDB は、AEMと同じホストで実行することも、リモートで実行することもできます。

### MongoDB の起動 {#start-mongodb}

* &lt;mongo-install>/bin/mongod —dbpath &lt;mongo-dbpath>

これにより、デフォルトのポート 27017 を使用して MongoDB サーバーが起動します。

* Macの場合、start arg &#39;ulimit -n 2048&#39;で ulimit を増やします。

>[!NOTE]
>
>MongoDB が起動されている場合 *後* AEM、 **再起動** all **AEM** インスタンスを使用して、MongoDB に正しく接続できるようにします。

### デモ実稼働オプション：MongoDB レプリカセットの設定 {#demo-production-option-setup-mongodb-replica-set}

次のコマンドは、localhost 上の 3 つのノードを使用してレプリカセットを設定する例です。

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

* から Solr をダウンロード [Apache Lucene](https://archive.apache.org/dist/lucene/solr/):

   * あらゆる OS に適しています。
   * Solr バージョン 7.0。
   * Solr には Java™ 1.7 以降が必要です。

* 基本設定

   * Solr の「例」の設定に従います。
   * サービスは必要ありません。
   * インストールされた Solr フォルダーは、 &lt;solr-install>.

### AEM Communities用の Solr の設定 {#configure-solr-for-aem-communities}

デモ用に MSRP の Solr コレクションを設定するには、次の 2 つの決定を行う必要があります（詳しくは、メインドキュメントへのリンクを選択してください）。

1. Solr をスタンドアロンで実行または [SolrCloud モード](msrp.md#solrcloudmode).
1. インストール [標準](msrp.md#installingstandardmls) または [詳細](msrp.md#installingadvancedmls) 多言語検索（MLS）

### スタンドアロン Solr {#standalone-solr}

Solr の実行方法は、インストールのバージョンと方法によって異なる場合があります。 この [Solr リファレンスガイド](https://archive.apache.org/dist/lucene/solr/ref-guide/) は、信頼できるドキュメントです。

簡単にするために、バージョン 4.10 を例として使用し、Solr をスタンドアロンモードで起動します。

* cd を次へ &lt;solrinstall>/例
* Java™ -jar start.jar

このプロセスは、デフォルトのポート 8983 を使用して Solr HTTP サーバーを起動します。 Solr コンソールを参照して、テスト用の Solr コンソールを取得できます。

* デフォルトの Solr コンソール： [http://localhost:8983/solr/](http://localhost:8983/solr/)

>[!NOTE]
>
>Solr コンソールが使用できない場合は、次の場所でログを確認してください &lt;solrinstall>/example/logs に保存します。 SOLR が解決できない特定のホスト名（例えば「user-macbook-pro」）にバインドしようとしているかどうかを確認します。
>
その場合は、を更新します `etc/hosts` このホスト名の新しいエントリを持つファイル（例：127.0.0.1 user-macbook-pro）で、Solr を正しく起動します。

### SolrCloud {#solrcloud}

基本的な（実稼動以外の） solrCloud 設定を実行するには、次のように solr を起動します。

* `java -Dbootstrap_confdir=./solr/collection1/conf -Dbootstrap_conf=true -DzkRun -jar start.jar`

## MongoDB を共通ストアとして識別します。 {#identify-mongodb-as-common-store}

必要に応じて、オーサーインスタンスとパブリッシュ AEM インスタンスを起動します。

MongoDB の起動前にAEMを実行していた場合は、AEM インスタンスを再起動する必要があります。

メインのドキュメントページの手順に従います。 [MSRP - MongoDB 共通ストア](msrp.md)

## テスト {#test}

MongoDB 共通ストアをテストおよび検証するには、パブリッシュインスタンスにコメントを投稿してオーサーインスタンスで表示し、MongoDB と Solr で UGC を表示します。

1. パブリッシュインスタンスで、を参照します。 [コミュニティコンポーネントガイド](http://localhost:4503/content/community-components/en/comments.html) を表示して、コメント コンポーネントを選択します。
1. ログインしてコメントを投稿：
1. コメント テキスト入力ボックスにテキストを入力し、をクリックします **[!UICONTROL 投稿]**

   ![コメント後](assets/post-comment.png)

1. に関するコメントを表示するだけです [オーサーインスタンス](http://localhost:4502/content/community-components/en/comments.html) （おそらく引き続き管理者/管理者としてログインしています）。

   ![view-comment](assets/view-comment.png)

   メモ：の下に JCR ノードがある場合 *asipath* オーサー環境では、これらのノードは SCF フレームワーク用です。 実際の UGC は JCR ではなく、MongoDB にあります。

1. mongodb での UGC の表示 **[!UICONTROL コミュニティ]** > **[!UICONTROL コレクション]** > **[!UICONTROL コンテンツ]**

   ![ugc-content](assets/ugc-content.png)

1. Solr で UGC を表示します。

   * Solr ダッシュボードを参照： [http://localhost:8983/solr/](http://localhost:8983/solr/).
   * ユーザー `core selector` 選択する `collection1`.
   * `Query` を選択します。
   * `Execute Query` を選択します。

   ![ugc-solr](assets/ugc-solr.png)

## トラブルシューティング {#troubleshooting}

### UGC が表示されない {#no-ugc-appears}

1. MongoDB が正しくインストールされ、実行されていることを確認します。

1. MSRP がデフォルトのプロバイダーに設定されていることを確認します。

   * すべてのオーサーインスタンスおよびパブリッシュ AEMインスタンスで、次を再参照します [ストレージ設定コンソール](srp-config.md)または、AEM リポジトリを確認します。

   * JCR で次の場合： [/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/) 次を含まない [srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc) ノードの場合は、ストレージプロバイダーが JSRP であることを意味します。
   * srpc ノードが存在し、ノードがを含む場合 [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration)が設定されている場合は、defaultconfiguration のプロパティで MSRP をデフォルトのプロバイダーとして定義する必要があります。

1. MSRP が選択された後に、AEMが再起動されたことを確認します。
