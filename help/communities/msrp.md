---
title: MSRP - MongoDB ストレージリソースプロバイダー
seo-title: MSRP - MongoDB ストレージリソースプロバイダー
description: リレーショナルデータベースを共通ストアとして使用するように AEM Communities を設定する
seo-description: リレーショナルデータベースを共通ストアとして使用するように AEM Communities を設定する
uuid: 9fc06d4f-a60f-4ce3-8586-bcc836aa7de6
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 048f7b30-20c3-4567-bd32-38cf2643cf39
role: Administrator
exl-id: 799d5ae1-caac-4c92-8835-696ad25de553
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 47%

---

# MSRP - MongoDB ストレージリソースプロバイダー {#msrp-mongodb-storage-resource-provider}

## MSRP について {#about-msrp}

AEM CommunitiesがMSRPを共通ストアとして使用するように設定されている場合、同期やレプリケーションを必要とせずに、すべてのオーサーインスタンスとパブリッシュインスタンスからユーザー生成コンテンツ(UGC)にアクセスできます。

[SRP オプションの特性](working-with-srp.md#characteristics-of-srp-options)と[推奨されるトポロジ](topologies.md)も参照してください。

## 要件 {#requirements}

* [MongoDB](https://www.mongodb.org/)：

   * バージョン2.6以降
   * モンゴや共有を設定する必要がない
   * [レプリカセット](#mongoreplicaset)の使用を強くお勧めします
   * AEMと同じホスト上で実行するか、リモートで実行する

* [Apache Solr](https://lucene.apache.org/solr/)：

   * Solrバージョン7.0
   * Solr には Java 1.7 以降が必要です。
   * サービスは不要
   * 実行モードの選択：
      * スタンドアロンモード
      * [SolrCloud モード](solr.md#solrcloud-mode)（実稼動環境で推奨）
   * 多言語検索(MLS)の選択：
      * [標準の MLS のインストール](solr.md#installing-standard-mls)
      * [高度な MLS のインストール](solr.md#installing-advanced-mls)

## MongoDB 設定 {#mongodb-configuration}

### MSRP の選択 {#select-msrp}

[ストレージ設定コンソール](srp-config.md)では、使用するSRPの実装を指定するデフォルトのストレージ設定を選択できます。

オーサー環境でストレージ設定コンソールにアクセスするには:

* グローバルナビゲーションから、**[!UICONTROL ツール]** / **[!UICONTROL コミュニティ]** / **[!UICONTROL ストレージ設定]**&#x200B;を選択します。

![msrp](assets/msrp.png)

* **[!UICONTROL MongoDB Storage Resource Provider (MSRP)]**&#x200B;を選択します。
* **[!UICONTROL MongoDB 設定]**

   * **[!UICONTROL MongoDB URI]**

      *デフォルト*:mongodb://localhost/?maxPoolSize=10&amp;waitQueueMultiple=5&amp;readPreference=secondaryPreferred

   * **[!UICONTROL MongoDB データベース]**

      *デフォルト*:communities

   * **[!UICONTROL MongoDB UGC コレクション]**

      *デフォルト*:コンテンツ

   * **[!UICONTROL MongoDB 添付ファイルコレクション]**

      *デフォルト*:attachments

* **[!UICONTROL SolrConfiguration]**

   * **[](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files)Zookeeper ホスト**

      [SolrCloudモード](solr.md#solrcloud-mode)で外部のZooKeeperと実行する場合は、*my.server.com:2181*&#x200B;のように、ZooKeeperの`HOST:PORT`にこの値を設定します。

      ZooKeeperアンサンブルの場合は、*host1:2181,host2:2181*&#x200B;のように、コンマ区切りの`HOST:PORT`値を入力します。

      内部のZooKeeperを使用してSolrをスタンドアロンモードで実行する場合は、空のままにします。
      *デフォルト*:  *&lt;blank>*

      * **[!UICONTROL Solr URL]**スタンドアロンモードで Solr と通信するために使用する URL。SolrCloud モードで実行している場合は、空白のままにします。

         *デフォルト*:https://127.0.0.1:8983/solr/

      * **[!UICONTROL Solr コレクション]**Solr コレクションの名前。

         *デフォルト*:collection1

* 「**[!UICONTROL 送信]**」を選択します。

>[!NOTE]
>
>mongoDB データベース（デフォルトの名前は `communities`）を、[ノードストアまたはデータ（バイナリ）ストア](../../help/sites-deploying/data-store-config.md)で使用されているデータベースの名前に設定することはできません。[AEM 6.5のストレージ要素](../../help/sites-deploying/storage-elements-in-aem-6.md)も参照してください。

### MongoDB レプリカセット {#mongodb-replica-set}

本番環境では、プライマリ・セカンダリ・レプリケーションと自動フェイルオーバーを実装するMongoDBサーバーのクラスタであるレプリカ・セットを設定することを強くお勧めします。

レプリカセットについて詳しくは、MongoDB の [レプリケーション](https://docs.mongodb.org/manual/replication/)に関するドキュメントを参照してください。

レプリカセットの操作と、アプリケーションと MongoDB のインスタンスとの間の接続を定義する方法については、MongoDB の[接続文字列の URI フォーマット](https://docs.mongodb.org/manual/reference/connection-string/)に関するドキュメントを参照してください。

#### レプリカセットに接続するための URL の例   {#example-url-for-connecting-to-a-replica-set}

```shell
# Example url for:
# servers "mongoserver1", "mongoserver2", "mongoserver3"
# replica set 'rs0'
# port numbers only necessary if not default port 27017
mongodb://mongoserver1:<mongoport1>,mongoserver2:<mongoport2>,mongoserver3:<mongoport3>/?replicaSet=rs0&maxPoolSize=100&waitQueueMultiple=50&readPreference=secondaryPreferred
```

## Solr 設定 {#solr-configuration}

別々のコレクションを使用することで、1 つの Solr をノードストア（Oak）と共通ストア（MSRP）の間で共有できます。

Oak と MSRP のコレクションがどちらも高頻度で使用される場合は、パフォーマンス上の理由から 2 つ目の Solr をインストールすることもできます。

実稼動環境では、[SolrCloudモード](solr.md#solrcloud-mode)を使用すると、スタンドアロンモード（単一のローカルSolr設定）よりもパフォーマンスが向上します。

設定について詳しくは、[SRP 用の Solr 設定](solr.md)を参照してください。

### アップグレード {#upgrading}

MSRPを使用して設定した以前のバージョンからアップグレードする場合は、次の操作が必要です。

1. AEM Communities[にアップグレードする](upgrade.md)
1. 新しいSolr設定ファイルのインストール
   * [標準のMLS](solr.md#installing-standard-mls)の場合
   * [高度なMLS](solr.md#installing-advanced-mls)の場合
1. MSRPの再インデックス
[MSRPインデックス再作成ツール](#msrp-reindex-tool)を参照してください。

## 設定の公開 {#publishing-the-configuration}

すべてのオーサーインスタンスとパブリッシュインスタンスで、MSRP が共通ストアとして指定されている必要があります。

パブリッシュ環境で同じ設定を使用できるようにするには、オーサーインスタンスにログインし、次の手順に従います。

* メインメニューから&#x200B;**[!UICONTROL ツール]** > **[!UICONTROL 操作]** > **[!UICONTROL レプリケーション]**&#x200B;に移動します。
* 「**[!UICONTROL ツリーをアクティブ化]**」を選択します。
* **[!UICONTROL 開始パス]**:
   * `/etc/socialconfig/srpc/`を参照します。
* **[!UICONTROL アクティブ化]**&#x200B;を選択します。

## ユーザーデータの管理 {#managing-user-data}

パブリッシュ環境で頻繁に入力されるユーザー、ユーザープロファイルおよびユーザーグループについては、以下を参照してください。******

* [ユーザー同期](sync.md)
* [ユーザーとユーザーグループの管理](users.md)

## MSRP インデックス再作成ツール {#msrp-reindex-tool}

新しい設定ファイルをインストールしたり、Solr のインデックスを修復したりするときは、MSRP 用の Solr のインデックス再作成用の HTTP エンドポイントを使用できます。

このツールでは、MongoDB が MSRP の情報源になるので、バックアップを取るときは MongoDB だけで十分です。**

UGCツリー全体のインデックスを再作成するか、*path *dataパラメーターで指定された特定のサブツリーのみを再インデックスできます。

このツールは、コマンドラインから cURL などの HTTP ツールを使用して実行できます。

インデックスを再作成する場合、メモリとパフォーマンスの間にトレードオフがあります。このトレードオフは*batchSize *dataパラメーターで制御し、バッチごとにインデックスを再作成するUGCレコードの数を指定します。

適切なデフォルト値は 5000 です。

* メモリに問題がある場合は、より小さい数値を指定します
* 速度が問題の場合は、速度を上げるために大きい数を指定します

### cURL コマンドを使用した MSRP インデックス再作成ツールの実行 {#running-msrp-reindex-tool-using-curl-command}

以下に示す cURL コマンドは、MSRP に格納されている UGC のインデックス再作成の HTTP リクエストに必要なコマンドです。

基本的な形式は以下のとおりです。

cURL -u *signin* -d *data* *reindex-url*

*signin*  = administrator-id:password例：admin:admin

*data*  = &quot;batchSize=*size* &amp;path=*path&quot;*

*size*  =操作ごとに再インデックスするUGCエントリの数 
`/content/usergenerated/asi/mongo/`

*path*  =インデックスを再作成するUGCツリーのルート位置

* すべてのUGCのインデックスを再作成するには、の`asipath`プロパティの値を指定します。
   `/etc/socialconfig/srpc/defaultconfiguration`
* インデックスを一部のUGCに制限するには、`asipath`のサブツリーを指定します。

*reindex-url*  = SRPのインデックス再作成のエンドポイント 
`http://localhost:4503/services/social/datastore/mongo/reindex`

>[!NOTE]
>
>[DSRP Solr](dsrp.md)のインデックスを再作成する場合、URLは&#x200B;**/services/social/datastore/rdb/reindex**&#x200B;です。

### MSRP インデックス再作成の例 {#msrp-reindex-example}

```shell
curl -s -u admin:admin -d 'batchSize=10000&path=/content/usergenerated/asi/mongo/' http://localhost:4503/services/social/datastore/mongo/reindex
```

## MSRP のデモの実行方法 {#how-to-demo-msrp}

MSRP をデモ用に設定するには、[MongoDB をデモ用に設定する方法](demo-mongo.md)を参照してください。

## トラブルシューティング {#troubleshooting}

### UGC が MongoDB で表示されない  {#ugc-not-visible-in-mongodb}

ストレージオプションの設定を確認し、MSRP がデフォルトのプロバイダーに設定されているかを確認してください。デフォルトでは、ストレージリソースプロバイダーはJSRPです。

すべてのオーサーインスタンスとパブリッシュAEMインスタンスで、[ストレージ設定コンソール](srp-config.md)に再度アクセスするか、AEMリポジトリを確認します。

* JCRで、 [/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/)

   * [srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc)ノードが含まれない場合は、ストレージプロバイダーがJSRPであることを意味します。
   * srpcノードが存在し、ノード[defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration)が含まれる場合は、defaultconfigurationのプロパティでMSRPがデフォルトのプロバイダーとして定義されている必要があります。

### アップグレード後に UGC が表示されない {#ugc-disappears-after-upgrade}

既存のAEM Communities 6.0サイトからアップグレードする場合は、AEM Communities 6.3にアップグレードした後、既存のUGCを、[SRP](srp.md) APIに必要な構造に合わせて変換する必要があります。

GitHubには、この目的で利用できるオープンソースツールがあります。

* [AEM Communities UGC Migration Tool](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

移行ツールは、AEM Social Communitiesの以前のバージョンからUGCを書き出してAEM Communities 6.1以降に読み込むようにカスタマイズできます。

### エラー - undefined field provider_id {#error-undefined-field-provider-id}

以下のエラーがログに表示された場合は、Solr スキーマファイルが適切に設定されていません。

#### JsonMappingException: undefined field provider_id  {#jsonmappingexception-undefined-field-provider-id}

```xml
Caused by: com.fasterxml.jackson.databind.JsonMappingException: undefined field provider_id
at com.fasterxml.jackson.databind.ser.DefaultSerializerProvider.serializeValue(DefaultSerializerProvider.java:129)
at com.fasterxml.jackson.databind.ObjectMapper.writeValue(ObjectMapper.java:1819)
at com.adobe.cq.social.scf.core.BaseSocialComponent.toJSONString(BaseSocialComponent.java:196)
... 124 common frames omitted
```

このエラーを解決するには、[標準のMLS](solr.md#installing-standard-mls)のインストール手順に従う場合は、次の点を確認します。

* XML設定ファイルが正しいSolrの場所にコピーされました。
* 新しい設定ファイルを既存のファイルと置き換えた後に Solr を再起動した.

### MongoDB へのセキュア接続が失敗する {#secure-connection-to-mongodb-fails}

MongoDB サーバーへのセキュア接続の試みが、クラス定義が見つからないという理由で失敗する場合は、MongoDB ドライバーバンドル `mongo-java-driver`（公開されている maven リポジトリで入手可能）を更新する必要があります。

1. [https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar](https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar)(バージョン2.13.2以降)からドライバをダウンロードします。
1. バンドルをAEMインスタンスの「crx-quickstart/install」フォルダーにコピーします。
1. AEM インスタンスを再起動します。

## リソース {#resources}

* [MongoDB を備えた AEM](../../help/sites-deploying/aem-with-mongodb.md)
* [MongoDB ドキュメント](https://docs.mongodb.org/)
