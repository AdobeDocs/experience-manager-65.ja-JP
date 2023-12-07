---
title: デモ用の MongoDB の設定方法
description: 1 つのオーサーインスタンスと 1 つのパブリッシュインスタンスに対して MSRP を設定する方法
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 7e257b34-a0f5-47db-b1a9-e26333c287d9
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 0%

---

# デモ用の MongoDB の設定方法 {#how-to-setup-mongodb-for-demo}

## はじめに {#introduction}

このチュートリアルでは、の設定方法について説明します。 [MSRP](msrp.md) 対象： *1 人の作者* インスタンスと *1 つの公開* インスタンス。

この設定により、ユーザー生成コンテンツ (UGC) を転送またはリバースレプリケーションする必要なく、オーサー環境とパブリッシュ環境の両方からコミュニティコンテンツにアクセスできるようになります。

この設定は、次の場合に適しています。 *非実稼動* 環境（開発やデモ用など）。

**A *実稼動* 環境は次のようにする必要があります。**

* レプリカセットで MongoDB を実行する
* SolrCloud を使用
* 複数のパブリッシャーインスタンスを含む

## MongoDB {#mongodb}

### MongoDB のインストール {#install-mongodb}

* から MongoDB をダウンロード [https://www.mongodb.com/](https://www.mongodb.com/)

   * OS の選択：

      * Linux®
      * Mac 10.8
      * Windows 7

   * バージョンの選択：

      * 少なくとも、バージョン 2.6 を使用してください。

* 基本設定

   * MongoDB のインストール手順に従います。
   * mongod 用に設定：

      * モンゴや共有を設定する必要はありません。

   * インストールされている MongoDB フォルダーの名前はです。 &lt;mongo-install>.
   * 定義されたデータディレクトリのパスがと呼ばれます。 &lt;mongo-dbpath>.

* MongoDB は、AEMと同じホストで実行するか、リモートで実行できます。

### MongoDB を起動します {#start-mongodb}

* &lt;mongo-install>/bin/mongod —dbpath &lt;mongo-dbpath>

これにより、デフォルトのポート27017を使用して MongoDB サーバーが起動します。

* Macの場合、開始引数「ulimit -n 2048」で ulimit を増やします。

>[!NOTE]
>
>MongoDB が起動している場合 *次より後* AEM, **再起動** すべて **AEM** インスタンスが MongoDB に正しく接続されるようにします。

### デモ実稼動オプション：MongoDBレプリカセットの設定 {#demo-production-option-setup-mongodb-replica-set}

次のコマンドは、ローカルホストで 3 つのノードを持つレプリカセットを設定する例です。

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
   * Solr には Java™ 1.7 以降が必要です。

* 基本設定

   * 「例」Solr 設定に従います。
   * サービスは必要ありません。
   * インストールされている Solr フォルダーの名前はです。 &lt;solr-install>.

### AEM Communities用の Solr の設定 {#configure-solr-for-aem-communities}

デモ用に MSRP 用の Solr コレクションを設定するには、次の 2 つの決定をおこなう必要があります（詳しくは、メインドキュメントへのリンクを選択してください）。

1. スタンドアロンで Solr を実行するか、 [SolrCloud モード](msrp.md#solrcloudmode).
1. インストール [標準](msrp.md#installingstandardmls) または [詳細](msrp.md#installingadvancedmls) 多言語検索 (MLS)。

### スタンドアロン Solr {#standalone-solr}

Solr を実行する方法は、インストールのバージョンと方法によって異なる場合があります。 The [Solr リファレンスガイド](https://archive.apache.org/dist/lucene/solr/ref-guide/) は、権限を持つドキュメントです。

簡単にするために、バージョン 4.10 を例として使用し、Solr をスタンドアロンモードで起動します。

* cd に移動 &lt;solrinstall>/example
* Java™ -jar start.jar

このプロセスは、デフォルトポート 8983 を使用して Solr HTTP サーバーを起動します。 Solr コンソールを参照して、テスト用の Solr コンソールを取得できます。

* デフォルトの Solr コンソール： [http://localhost:8983/solr/](http://localhost:8983/solr/)

>[!NOTE]
>
>Solr コンソールが使用できない場合は、以下のログを確認します。 &lt;solrinstall>/example/logs. SOLR が、解決できない特定のホスト名（例えば、「user-macbook-pro」）にバインドしようとしているかどうかを確認します。
>
該当する場合は、 `etc/hosts` ファイルに、このホスト名の新しいエントリ（例えば、127.0.0.1 user-macbook-pro）を含め、Solr を正しく起動します。

### SolrCloud {#solrcloud}

（実稼動ではなく）基本的な solrCloud 設定を実行するには、次の設定で solr を起動します。

* `java -Dbootstrap_confdir=./solr/collection1/conf -Dbootstrap_conf=true -DzkRun -jar start.jar`

## MongoDB を共通ストアとして識別します。 {#identify-mongodb-as-common-store}

必要に応じて、オーサーインスタンスとパブリッシュAEMインスタンスを起動します。

MongoDB が起動する前にAEMが実行されていた場合は、AEMインスタンスを再起動する必要があります。

メインドキュメントページの手順に従います。 [MSRP - MongoDB 共通ストア](msrp.md)

## テスト {#test}

MongoDB 共通ストアをテストおよび検証するには、パブリッシュインスタンスにコメントを投稿してオーサーインスタンスで表示し、MongoDB と Solr で UGC を表示します。

1. パブリッシュインスタンスで、 [コミュニティコンポーネントガイド](http://localhost:4503/content/community-components/en/comments.html) ページを開き、コメントコンポーネントを選択します。
1. サインインしてコメントを投稿：
1. コメントテキスト入力ボックスにテキストを入力し、 **[!UICONTROL 投稿]**

   ![コメント後](assets/post-comment.png)

1. 単に [オーサーインスタンス](http://localhost:4502/content/community-components/en/comments.html) （管理者/管理者としてまだサインインしている可能性があります）。

   ![view-comment](assets/view-comment.png)

   注意： JCR ノードは *asipath* オーサー環境では、これらのノードは SCF フレームワーク用です。 実際の UGC は JCR には含まれず、MongoDB に含まれます。

1. mongodb での UGC の表示 **[!UICONTROL Communities]** > **[!UICONTROL コレクション]** > **[!UICONTROL コンテンツ]**

   ![ugc-content](assets/ugc-content.png)

1. Solr で UGC を表示します。

   * Solr ダッシュボードを参照します。 [http://localhost:8983/solr/](http://localhost:8983/solr/).
   * ユーザー `core selector` 選択 `collection1`.
   * 選択 `Query`.
   * 選択 `Execute Query`.

   ![ugc-solr](assets/ugc-solr.png)

## トラブルシューティング {#troubleshooting}

### UGC が表示されません {#no-ugc-appears}

1. MongoDB がインストールされ、正しく実行されていることを確認します。

1. MSRP がデフォルトのプロバイダーに設定されていることを確認します。

   * すべてのオーサーインスタンスとパブリッシュAEMインスタンスで、 [ストレージ設定コンソール](srp-config.md)またはAEMリポジトリを確認します。

   * JCR で、 [/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/) 次を含まない [srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc) ノードの場合、ストレージプロバイダーが JSRP であることを意味します。
   * srpc ノードが存在し、ノードが含まれる場合 [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration)の場合、デフォルトの設定のプロパティでは、MSRP がデフォルトのプロバイダーとして定義されている必要があります。

1. MSRP を選択した後にAEMが再起動されたことを確認します。
