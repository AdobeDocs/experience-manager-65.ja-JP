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

このチュートリアルでは、*1 つのオーサー [&#128279;](msrp.md) インスタンスと* 1 つのパブリッシュ *インスタンスに MSRP* を設定する方法について説明します。

この設定では、ユーザー生成コンテンツ（UGC）を転送またはリバースレプリケーションしなくても、オーサー環境とパブリッシュ環境の両方からコミュニティコンテンツにアクセスできます。

この設定は、開発やデモなどの *実稼動以外* の環境に適しています。

**A *実稼動* 環境では、次の操作を行う必要があります。**

* レプリカセットでの MongoDB の実行
* SolrCloud の使用
* 複数のパブリッシャーインスタンスを含む

## MongoDB {#mongodb}

### MongoDB のインストール {#install-mongodb}

* [https://www.mongodb.com/](https://www.mongodb.com/) から MongoDB をダウンロード

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

   * インストールされた MongoDB フォルダーは、&lt;mongo-install> と呼ばれます。
   * 定義されたデータディレクトリパスは、&lt;mongo-dbpath> と呼ばれます。

* MongoDB は、AEMと同じホストで実行することも、リモートで実行することもできます。

### MongoDB の起動 {#start-mongodb}

* &lt;mongo-install>/bin/mongod —dbpath &lt;mongo-dbpath>

これにより、デフォルトのポート 27017 を使用して MongoDB サーバーが起動します。

* Macの場合、start arg &#39;ulimit -n 2048&#39;で ulimit を増やします。

>[!NOTE]
>
>MongoDB を起動した場合 *after* AEM, **restart** すべての **AEM** インスタンスが MongoDB に正しく接続されます。

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

* [Apache Lucene](https://archive.apache.org/dist/lucene/solr/) から Solr をダウンロードします。

   * あらゆる OS に適しています。
   * Solr バージョン 7.0。
   * Solr には Java™ 1.7 以降が必要です。

* 基本設定

   * Solr の「例」の設定に従います。
   * サービスは必要ありません。
   * インストールされた Solr フォルダーの名前は &lt;solr-install> です。

### AEM Communities用の Solr の設定 {#configure-solr-for-aem-communities}

デモ用に MSRP の Solr コレクションを設定するには、次の 2 つの決定を行う必要があります（詳しくは、メインドキュメントへのリンクを選択してください）。

1. Solr をスタンドアロンまたは [SolrCloud モード &#x200B;](msrp.md#solrcloudmode) で実行します。
1. [&#x200B; 標準 &#x200B;](msrp.md#installingstandardmls) または [&#x200B; 詳細 &#x200B;](msrp.md#installingadvancedmls) 多言語検索（MLS）をインストールします。

### スタンドアロン Solr {#standalone-solr}

Solr の実行方法は、インストールのバージョンと方法によって異なる場合があります。 [Solr リファレンスガイド &#x200B;](https://archive.apache.org/dist/lucene/solr/ref-guide/) は、信頼できるドキュメントです。

簡単にするために、バージョン 4.10 を例として使用し、Solr をスタンドアロンモードで起動します。

* cd to &lt;solrinstall>/example
* Java™ -jar start.jar

このプロセスは、デフォルトのポート 8983 を使用して Solr HTTP サーバーを起動します。 Solr コンソールを参照して、テスト用の Solr コンソールを取得できます。

* デフォルト Solr コンソール：[http://localhost:8983/solr/](http://localhost:8983/solr/)

>[!NOTE]
>
>Solr コンソールが使用できない場合は、&lt;solrinstall>/example/logs の下のログを確認します。 SOLR が解決できない特定のホスト名（例えば「user-macbook-pro」）にバインドしようとしているかどうかを確認します。
>
>その場合は、`etc/hosts` のホスト名の新しいエントリ（例：127.0.0.1 user-macbook-pro）でファイルを更新して、Solr を正しく起動します。

### SolrCloud {#solrcloud}

基本的な（実稼動以外の） solrCloud 設定を実行するには、次のように solr を起動します。

* `java -Dbootstrap_confdir=./solr/collection1/conf -Dbootstrap_conf=true -DzkRun -jar start.jar`

## MongoDB を共通ストアとして識別します。 {#identify-mongodb-as-common-store}

必要に応じて、オーサーインスタンスとパブリッシュ AEM インスタンスを起動します。

MongoDB の起動前にAEMを実行していた場合は、AEM インスタンスを再起動する必要があります。

メインのドキュメントページの手順に従います。[MSRP - MongoDB 共通ストア &#x200B;](msrp.md)

## テスト {#test}

MongoDB 共通ストアをテストおよび検証するには、パブリッシュインスタンスにコメントを投稿してオーサーインスタンスで表示し、MongoDB と Solr で UGC を表示します。

1. パブリッシュインスタンスで、「[&#x200B; コミュニティコンポーネントガイド &#x200B;](http://localhost:4503/content/community-components/en/comments.html)」ページを参照し、コメント コンポーネントを選択します。
1. ログインしてコメントを投稿：
1. コメント テキスト入力ボックスにテキストを入力し、**[!UICONTROL Post]** をクリックします

   ![&#x200B; コメント後 &#x200B;](assets/post-comment.png)

1. [&#x200B; オーサーインスタンス &#x200B;](http://localhost:4502/content/community-components/en/comments.html) に関するコメントを表示するだけです（管理者/管理者としてログインしている可能性があります）。

   ![view-comment](assets/view-comment.png)

   メモ：作成者の *asipath* の下には JCR ノードがありますが、これらのノードは SCF フレームワーク用です。 実際の UGC は JCR ではなく、MongoDB にあります。

1. mongodb で UGC を表示します **[!UICONTROL Communities]**/（コレクション **/** コンテンツ **&#x200B;**。

   ![ugc-content](assets/ugc-content.png)

1. Solr で UGC を表示します。

   * Solr ダッシュボード：[http://localhost:8983/solr/](http://localhost:8983/solr/) を参照します。
   * ユーザー `core selector` 選択 `collection1` ます。
   * `Query` を選択します。
   * `Execute Query` を選択します。

   ![ugc-solr](assets/ugc-solr.png)

## トラブルシューティング {#troubleshooting}

### UGC が表示されない {#no-ugc-appears}

1. MongoDB が正しくインストールされ、実行されていることを確認します。

1. MSRP がデフォルトのプロバイダーに設定されていることを確認します。

   * すべてのオーサーおよびパブリッシュ AEM インスタンスで、[&#x200B; ストレージ設定コンソール &#x200B;](srp-config.md) に再度アクセスするか、AEM リポジトリを確認します。

   * JCR で [/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/) に [srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc) ノードが含まれていない場合は、ストレージプロバイダーが JSRP です。
   * srpc ノードが存在し、ノード [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration) が含まれている場合、defaultconfiguration のプロパティでは、MSRP をデフォルトのプロバイダーとして定義する必要があります。

1. MSRP が選択された後に、AEMが再起動されたことを確認します。
