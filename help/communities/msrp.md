---
title: MSRP - MongoDB ストレージリソースプロバイダー
description: リレーショナルデータベースを共通ストアとして使用するようにAEM Communitiesを設定します
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 799d5ae1-caac-4c92-8835-696ad25de553
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1142'
ht-degree: 3%

---

# MSRP - MongoDB ストレージリソースプロバイダー {#msrp-mongodb-storage-resource-provider}

## MSRP について {#about-msrp}

MSRP を共通ストアとして使用するようにAEM Communitiesが設定されている場合、ユーザー生成コンテンツ（UGC）には、すべてのオーサーインスタンスとパブリッシュインスタンスからアクセスでき、同期やレプリケーションを行う必要はありません。

[SRP オプションの特性 &#x200B;](working-with-srp.md#characteristics-of-srp-options) および [&#x200B; 推奨されるトポロジ &#x200B;](topologies.md) も参照してください。

## 要件 {#requirements}

* [MongoDB](https://www.mongodb.org/):

   * バージョン 2.6 以降
   * Mongos やシャーディングを設定する必要はありません
   * [&#x200B; レプリカ セットの使用を強くお勧めします &#x200B;](#mongoreplicaset)
   * AEMと同じホスト上で実行するか、リモートで実行できる

* [Apache Solr](https://lucene.apache.org/solr/):

   * Solr バージョン 7.0
   * Solr には Java 1.7 以降が必要です
   * サービスは必要ありません
   * 実行モードの選択：
      * スタンドアロンモード
      * [SolrCloud モード &#x200B;](solr.md#solrcloud-mode) （実稼動環境で推奨）
   * 多言語検索（MLS）の選択：
      * [標準 MLS のインストール](solr.md#installing-standard-mls)
      * [高度な MLS のインストール](solr.md#installing-advanced-mls)

## MongoDB の設定 {#mongodb-configuration}

### MSRP を選択 {#select-msrp}

[&#x200B; ストレージ設定コンソール &#x200B;](srp-config.md) では、デフォルトのストレージ設定を選択でき、使用する SRP の実装を識別できます。

オーサー環境でストレージ設定コンソールにアクセスするには：

* グローバルナビゲーションから、**[!UICONTROL ツール]**/**[!UICONTROL コミュニティ]**/**[!UICONTROL ストレージ設定]** を選択します。

![msrp](assets/msrp.png)

* **[!UICONTROL MongoDB ストレージリソースプロバイダー（MSRP）]** を選択します。
* **[!UICONTROL mongoDB の設定]**

   * **[!UICONTROL mongoDB URI]**

     *デフォルト*:mongodb://localhost/?maxPoolSize=10&amp;waitQueueMultiple=5&amp;readPreference=secondaryPreferred

   * **[!UICONTROL mongoDB データベース]**

     *デフォルト*: communities

   * **[!UICONTROL mongoDB UGC コレクション]**

     *デフォルト*: content

   * **[!UICONTROL mongoDB 添付ファイルコレクション]**

     *デフォルト*：添付ファイル

* **[!UICONTROL SolrConfiguration]**

   * **[Zookeeper](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files) ホスト**

     外部の ZooKeeper を使用して [SolrCloud モード &#x200B;](solr.md#solrcloud-mode) で実行する場合、この値を ZooKeeper の `HOST:PORT` （*my.server.com:2181など）に設定しま*。

     ZooKeeper アンサンブルの場合、コンマ区切りの `HOST:PORT` 値を入力します（*host1:2181,host2:2181* など）。

     内部の ZooKeeper を使用して Solr をスタンドアロンモードで実行する場合は、空白のままにします。
     *デフォルト*:*&lt;blank>*

      * **[!UICONTROL Solr URL]**
スタンドアロンモードで Solr との通信に使用する URL。
SolrCloud モードで実行する場合は空白のままにします。
        *デフォルト*:https://127.0.0.1:8983/solr/

      * **[!UICONTROL Solr コレクション]**
Solr コレクション名。
        *デフォルト*:collection1

* 「**[!UICONTROL 送信]**」を選択します。

>[!NOTE]
>
>mongoDB データベース（デフォルトは名前 `communities`）は、[&#x200B; ノードストアまたはデータ（バイナリ）ストア &#x200B;](../../help/sites-deploying/data-store-config.md) に使用されているデータベースの名前に設定しないでください。 [AEM 6.5 のストレージ要素 &#x200B;](../../help/sites-deploying/storage-elements-in-aem-6.md) も参照してください。

### MongoDB レプリカセット {#mongodb-replica-set}

実稼動環境の場合は、レプリカセット（プライマリセカンダリのレプリケーションと自動フェイルオーバーを実装する MongoDB サーバーのクラスター）を設定することを強くお勧めします。

レプリカセットについて詳しくは、MongoDB の [&#x200B; レプリケーション &#x200B;](https://docs.mongodb.org/manual/replication/) ドキュメントを参照してください。

レプリカセットを操作し、アプリケーションと MongoDB インスタンス間の接続を定義する方法については、MongoDB の [&#x200B; 接続文字列 URI 形式 &#x200B;](https://docs.mongodb.org/manual/reference/connection-string/) ドキュメントを参照してください。

#### レプリカセットに接続するための Url の例  {#example-url-for-connecting-to-a-replica-set}

```shell
# Example url for:
# servers "mongoserver1", "mongoserver2", "mongoserver3"
# replica set 'rs0'
# port numbers only necessary if not default port 27017
mongodb://mongoserver1:<mongoport1>,mongoserver2:<mongoport2>,mongoserver3:<mongoport3>/?replicaSet=rs0&maxPoolSize=100&waitQueueMultiple=50&readPreference=secondaryPreferred
```

## Solr 設定 {#solr-configuration}

Solr インストールは、異なるコレクションを使用して、ノードストア（Oak）と共通ストア（MSRP）の間で共有できます。

Oak コレクションと MSRP コレクションの両方が集中的に使用される場合は、パフォーマンス上の理由から、2 つ目の Solr がインストールされることがあります。

実稼動環境の場合、[SolrCloud モード &#x200B;](solr.md#solrcloud-mode) は、スタンドアロンモード（単一のローカル Solr セットアップ）よりもパフォーマンスが向上します。

設定について詳しくは、[SRP 用の Solr 設定 &#x200B;](solr.md) を参照してください。

### アップグレード {#upgrading}

MSRP が設定されている旧バージョンからアップグレードする場合、次の操作が必要になります。

1. [AEM Communitiesへのアップグレード &#x200B;](upgrade.md) を実行します。
1. 新しい Solr 設定ファイルのインストール
   * [&#x200B; 標準 MLS](solr.md#installing-standard-mls) 用
   * [&#x200B; 高度な MLS](solr.md#installing-advanced-mls) の場合
1. MSRP の再インデックス
[MSRP 再インデックスツール &#x200B;](#msrp-reindex-tool) の節を参照してください。

## 設定の公開 {#publishing-the-configuration}

MSRP は、すべてのオーサーインスタンスとパブリッシュインスタンスで共通ストアとして識別される必要があります。

パブリッシュ環境で同一の設定を使用できるようにするには、オーサーインスタンスにログインし、次の手順に従います。

* メインメニューから **[!UICONTROL ツール]**/**[!UICONTROL オペレーション]**/**[!UICONTROL レプリケーション]** に移動します。
* **[!UICONTROL ツリーのアクティブ化]** を選択します。
* **[!UICONTROL 開始パス]**:
   * `/etc/socialconfig/srpc/` を参照します
* 「**[!UICONTROL アクティブ化]**」を選択します。

## ユーザーデータの管理 {#managing-user-data}

パブリッシュ環境で入力されることが多い *ユーザー*、*ユーザープロファイル* および *ユーザーグループ* に関する情報は、次をご覧ください。

* [ユーザー同期](sync.md)
* [ユーザーとユーザーグループの管理](users.md)

## MSRP インデックス再作成ツール {#msrp-reindex-tool}

新しい設定ファイルをインストールする際や破損した Solr インデックスを修復する際に、MSRP 用の Solr のインデックスを再作成するための HTTP エンドポイントがあります。

このツールを使用すると、MongoDB が MSRP の *true* のソースになります。バックアップに必要なのは MongoDB のみです。

UGC ツリー全体のインデックスを再作成することも、*path *data パラメーターで指定されているように、特定のサブツリーのみを再作成することもできます。

このツールは、cURL またはその他の HTTP ツールを使用して、コマンドラインから実行できます。

インデックスを再作成する場合、メモリとパフォーマンスは*batchSize*データパラメーターによって制御されるトレードオフがあります。このパラメーターは、バッチごとにインデックスを再作成する UGC レコードの数を指定します。

適切なデフォルトは 5000 です。

* メモリに問題がある場合は、より小さい数値を指定します
* 速度に問題がある場合は、より大きい数値を指定して速度を上げます

### cURL コマンドを使用した MSRP インデックス再作成ツールの実行 {#running-msrp-reindex-tool-using-curl-command}

次の cURL コマンドは、MSRP に格納された UGC を再インデックス化するための HTTP リクエストに必要な項目を示しています。

基本的な形式は次のとおりです。

cURL -u *サインイン* -d *data* *reindex-url*

*signin* = administrator-id:password
例：admin:admin

*data* = &quot;batchSize=*size*&amp;path=*path&quot;*

*size* = 1 回の操作で再インデックスする UGC エントリの数
`/content/usergenerated/asi/mongo/`

*path* =再インデックス化する UGC のツリーのルート位置

* すべての UGC のインデックスを再作成するには、以下の `asipath` プロパティの値を指定します。
  `/etc/socialconfig/srpc/defaultconfiguration`
* インデックスを一部の UGC に制限するには、`asipath` のサブツリーを指定します

*reindex-url* = SRP のインデックス再作成用のエンドポイント
`http://localhost:4503/services/social/datastore/mongo/reindex`

>[!NOTE]
>
>[DSRP Solr のインデックスを再作成 &#x200B;](dsrp.md) する場合、URL は、**/services/social/datastore/rdb/reindex** です。

### MSRP インデックス再作成の例 {#msrp-reindex-example}

```shell
curl -s -u admin:admin -d 'batchSize=10000&path=/content/usergenerated/asi/mongo/' http://localhost:4503/services/social/datastore/mongo/reindex
```

## MSRP のデモ方法 {#how-to-demo-msrp}

デモ用または開発環境用に MSRP を設定する方法については、[&#x200B; デモ用の MongoDB の設定方法 &#x200B;](demo-mongo.md) を参照してください。

## トラブルシューティング {#troubleshooting}

### MongoDB に UGC が表示されない {#ugc-not-visible-in-mongodb}

ストレージオプションの設定をチェックして、MSRP がデフォルトのプロバイダーとして設定されていることを確認します。 デフォルトでは、ストレージリソースプロバイダーは JSRP です。

すべてのオーサーインスタンスおよびパブリッシュ AEMインスタンスで、[&#x200B; ストレージ設定コンソール &#x200B;](srp-config.md) を再度参照するか、AEM リポジトリを確認します。

* JCR で、[/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/)

   * [srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc) ノードが含まれていない場合は、ストレージプロバイダーが JSRP であることを意味します。
   * srpc ノードが存在し、ノード [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration) が含まれている場合、defaultconfiguration のプロパティでは、MSRP をデフォルトのプロバイダーとして定義する必要があります。

### アップグレード後に UGC が表示されなくなる {#ugc-disappears-after-upgrade}

既存のAEM Communities 6.0 サイトからアップグレードする場合は、AEM Communities 6.3 にアップグレードした後、既存の UGC を変換して、[SRP](srp.md) API に必要な構造に準拠させる必要があります。

この目的のために、GitHub で利用できるオープンソースのツールがあります。

* [AEM Communities UGC 移行ツール &#x200B;](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

移行ツールは、以前のバージョンのAEM Social Communities から UGC を書き出して、AEM Communities 6.1 以降に読み込むようにカスタマイズできます。

### エラー – 未定義のフィールド provider_id {#error-undefined-field-provider-id}

ログに次のエラーが表示される場合は、Solr スキーマファイルが正しく設定されていないことを示しています。

#### JsonMappingException：未定義のフィールド provider_id {#jsonmappingexception-undefined-field-provider-id}

```xml
Caused by: com.fasterxml.jackson.databind.JsonMappingException: undefined field provider_id
at com.fasterxml.jackson.databind.ser.DefaultSerializerProvider.serializeValue(DefaultSerializerProvider.java:129)
at com.fasterxml.jackson.databind.ObjectMapper.writeValue(ObjectMapper.java:1819)
at com.adobe.cq.social.scf.core.BaseSocialComponent.toJSONString(BaseSocialComponent.java:196)
... 124 common frames omitted
```

このエラーを解決するには、[&#x200B; 標準 MLS のインストール &#x200B;](solr.md#installing-standard-mls) の手順に従って、以下を確認してください。

* XML 設定ファイルが正しい Solr の場所にコピーされました。
* 新しい設定ファイルが既存の設定ファイルに置き換えられた後、Solr が再起動された。

### MongoDB への安全な接続に失敗 {#secure-connection-to-mongodb-fails}

クラス定義の欠落が原因で MongoDB サーバーへのセキュリティで保護された接続を確立しようとする試みが失敗した場合は、MongoDB ドライバーバンドル（`mongo-java-driver`）を更新し、公開 Maven リポジトリから入手する必要があります。

1. [https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar](https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar) （バージョン 2.13.2 以降）からドライバーをダウンロードします。
1. バンドルをAEM インスタンスの「crx-quickstart/install」フォルダーにコピーします。
1. AEM インスタンスを再起動します。

## リソース {#resources}

* [MongoDB を備えた AEM](../../help/sites-deploying/aem-with-mongodb.md)
* [MongoDB のドキュメント &#x200B;](https://docs.mongodb.org/)
