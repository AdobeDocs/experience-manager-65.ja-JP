---
title: MongoDB をデモ用に設定する方法
seo-title: How to Setup MongoDB for Demo
description: 1 つのオーサーインスタンスと 1 つのパブリッシュインスタンス用に MSRP をセットアップする方法
seo-description: How to setup MSRP for one author instance and one publish instance
uuid: d2035a9e-f05c-4f90-949d-7cdae9646750
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 0b126218-b142-4d33-a28c-a91ab4fe99ac
role: Admin
exl-id: 7e257b34-a0f5-47db-b1a9-e26333c287d9
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '774'
ht-degree: 51%

---

# MongoDB をデモ用に設定する方法 {#how-to-setup-mongodb-for-demo}

## はじめに {#introduction}

このチュートリアルでは、の設定方法について説明します [MSRP](msrp.md) 対象 *1 人の作者* インスタンスと *1 つの公開* インスタンス。

このセットアップを終えると、ユーザー生成コンテンツ（UGC）のフォワードまたはリバースレプリケーションをおこなわずに、オーサー環境とパブリッシュ環境の両方からコミュニティコンテンツにアクセスできるようになります。

この設定は、開発用やデモ用の環境など、*非実稼動*&#x200B;環境に適しています。

**実稼動環境では、以下のことが必要です。****

* レプリカセットで MongoDB を実行する
* SolrCloud を使用
* 複数のパブリッシャーインスタンスを含む

## MongoDB {#mongodb}

### MongoDB のインストール {#install-mongodb}

* から MongoDB をダウンロード [https://www.mongodb.org/](https://www.mongodb.org/)

   * OS の選択：

      * Linux
      * Mac 10.8
      * Windows 7
   * バージョンの選択：

      * 少なくとも、バージョン 2.6 を使用してください


* 基本設定

   * MongoDB のインストール手順に従います。
   * mongod 用に設定：

      * モンゴや共有を設定する必要はありません。
   * インストールされた MongoDB フォルダーは、 &lt;mongo-install>.
   * 定義されたデータディレクトリのパスは、 &lt;mongo-dbpath>.


* MongoDB は、AEMと同じホストで実行するか、リモートで実行できます。

### MongoDB を起動します。 {#start-mongodb}

* &lt;mongo-install>/bin/mongod --dbpath &lt;mongo-dbpath>

すると MongoDB サーバーが起動します。使用されるデフォルトポートは 27017 です。

* Mac では、起動引数「ulimit -n 2048」を使用して ulimit を増やします。

>[!NOTE]
>
>MongoDB が起動している場合 *後* AEM, **再起動** すべて **AEM** インスタンスが MongoDB に正しく接続されるようにします。

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

* から Solr をダウンロード [Apache Lucene](https://archive.apache.org/dist/lucene/solr/):

   * 任意の OS に適しています。
   * Solr バージョン 7.0。
   * Solr には Java 1.7 以降が必要です。

* 基本設定

   * 「例」Solr 設定に従います。
   * サービスは必要ありません。
   * インストールされた Solr フォルダーは、 &lt;solr-install>.

### AEM Communities のための Solr の設定 {#configure-solr-for-aem-communities}

MSRP のための Solr コレクションをデモ目的で設定するには、以下の 2 点を決定する必要があります（詳しくは、主なドキュメントへのリンクを選択してください）。

1. スタンドアロンで Solr を実行するか、 [SolrCloud モード](msrp.md#solrcloudmode).
1. インストール [標準](msrp.md#installingstandardmls) または [詳細](msrp.md#installingadvancedmls) 多言語検索 (MLS)。

### スタンドアロンの Solr {#standalone-solr}

Solr を実行する方法は、バージョンとインストール方法によって異なる場合があります。詳しくは、公式ドキュメントである [Solr リファレンスガイド](https://archive.apache.org/dist/lucene/solr/ref-guide/)を参照してください。

ここでは簡単に、バージョン 4.10 を使用して、Solr をスタンドアロンモードで起動します。

* cd to &lt;solrinstall>/example
* java -jar start.jar

これにより、Solr HTTP サーバーが起動します。使用されるデフォルトポートは 8983 です。Solr コンソールを参照し、Solr コンソールを試しに開くことができます。

* デフォルトの Solr コンソール：[http://localhost:8983/solr/](http://localhost:8983/solr/)

>[!NOTE]
>
>Solr コンソールが使用できない場合は、&lt;solrinstall>/example/logs にあるログを確認します。SOLR が解決できない特定のホスト名 ( 例：&quot;user-macbook-pro&quot;) です。
その場合、このホスト名の新しいエントリ（127.0.0.1 user-macbook-pro など）を使用して etc/hosts ファイルを更新します。すると Solr が適切に起動します。

### SolrCloud {#solrcloud}

非常に基本的な（実稼動用ではない）solrCloud のセットアップを実行するには、以下のコマンドで Solr を起動します。

* `java -Dbootstrap_confdir=./solr/collection1/conf -Dbootstrap_conf=true -DzkRun -jar start.jar`

##  MongoDB を共通ストアとして指定 {#identify-mongodb-as-common-store}

AEM オーサーインスタンスとパブリッシュインスタンスを起動します（必要な場合）。

AEM が MongoDB を起動する前に実行されている場合、AEM インスタンスを再起動する必要があります。

詳しくは、[MSRP - MongoDB 共通ストア](msrp.md)の手順に従ってください。

## テスト {#test}

MongoDB 共通ストアをテストおよび検証するために、パブリッシュインスタンスにコメントを投稿して、オーサーインスタンスでそのコメントを表示し、さらに MongoDB と Solr で UGC を表示します。

1. パブリッシュインスタンスで、 [コミュニティコンポーネントガイド](http://localhost:4503/content/community-components/en/comments.html) ページを開き、コメントコンポーネントを選択します。
1. サインインしてコメントを投稿：
1. コメントテキスト入力ボックスにテキストを入力し、 **[!UICONTROL 投稿]**

   ![コメント後](assets/post-comment.png)

1. 単に [オーサーインスタンス](http://localhost:4502/content/community-components/en/comments.html) （管理者/管理者としてまだサインインしている可能性があります）。

   ![view-comment](assets/view-comment.png)

   注意：JCR ノードは *asipath* オーサー環境では、これらは SCF フレームワーク用です。 実際の UGC は JCR には含まれず、MongoDB に含まれます。

1. mongodb での UGC の表示 **[!UICONTROL コミュニティ]** > **[!UICONTROL コレクション]** > **[!UICONTROL コンテンツ]**

   ![ugc-content](assets/ugc-content.png)

1. Solr で UGC を表示します。

   * Solr ダッシュボードを参照します。 [http://localhost:8983/solr/](http://localhost:8983/solr/).
   * ユーザー `core selector` 選択 `collection1`.
   * 選択 `Query`.
   * 選択 `Execute Query`.

   ![ugc-solr](assets/ugc-solr.png)

## トラブルシューティング {#troubleshooting}

### UGC が表示されない {#no-ugc-appears}

1. MongoDB がインストールされ、正しく実行されていることを確認します。

1. MSRP がデフォルトのプロバイダーに設定されていることを確認します。

   * すべてのオーサーインスタンスとパブリッシュAEMインスタンスで、 [ストレージ設定コンソール](srp-config.md) AEMリポジトリを確認します。

   * JCR で、 [/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/) 次を含まない [srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc) ノードの場合、ストレージプロバイダーが JSRP であることを意味します。
   * srpc ノードが存在し、ノードが含まれる場合 [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration)の場合、デフォルトの設定のプロパティでは、MSRP がデフォルトのプロバイダーとして定義されている必要があります。

1. MSRP を選択した後にAEMが再起動されたことを確認します。
