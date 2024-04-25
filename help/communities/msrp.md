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

関連トピック [SRP オプションの特徴](working-with-srp.md#characteristics-of-srp-options) および [推奨されるトポロジ](topologies.md).

## 要件 {#requirements}

* [MongoDB](https://www.mongodb.org/):

   * バージョン 2.6 以降
   * Mongos やシャーディングを設定する必要はありません
   * を使用することを強くお勧めします。 [レプリカ セット](#mongoreplicaset)
   * AEMと同じホスト上で実行するか、リモートで実行できる

* [Apache Solr](https://lucene.apache.org/solr/):

   * Solr バージョン 7.0
   * Solr には Java 1.7 以降が必要です
   * サービスは必要ありません
   * 実行モードの選択：
      * スタンドアロンモード
      * [SolrCloud モード](solr.md#solrcloud-mode) （実稼動環境での使用を推奨）
   * 多言語検索（MLS）の選択：
      * [標準 MLS のインストール](solr.md#installing-standard-mls)
      * [高度な MLS のインストール](solr.md#installing-advanced-mls)

## MongoDB の設定 {#mongodb-configuration}

### MSRP を選択 {#select-msrp}

この [ストレージ設定コンソール](srp-config.md) デフォルトのストレージ設定を選択でき、使用する SRP の実装を識別できます。

オーサー環境でストレージ設定コンソールにアクセスするには：

* グローバルナビゲーションから、を選択します。 **[!UICONTROL ツール]** > **[!UICONTROL コミュニティ]** > **[!UICONTROL ストレージ設定]**.

![msrp](assets/msrp.png)

* を選択 **[!UICONTROL MongoDB ストレージリソースプロバイダー（MSRP）]**
* **[!UICONTROL mongodb の設定]**

   * **[!UICONTROL mongoDB URI]**

     *default*: mongodb://localhost/?maxPoolSize=10&amp;waitQueueMultiple=5&amp;readPreference=secondaryPreferred

   * **[!UICONTROL mongoDB データベース]**

     *default*: communities

   * **[!UICONTROL mongoDB UGC コレクション]**

     *default*：コンテンツ

   * **[!UICONTROL mongoDB 添付ファイルコレクション]**

     *default*：添付ファイル

* **[!UICONTROL SolrConfiguration]**

   * **[飼育員](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files) ホスト**

     で実行する場合 [SolrCloud モード](solr.md#solrcloud-mode) 外部の ZooKeeper を使用する場合、この値を `HOST:PORT` ZooKeeper の場合（など） *my.server.com:2181*

     ZooKeeper アンサンブルの場合は、コンマ区切りにします `HOST:PORT` 値（例：） *host1:2181,host2:2181*

     内部の ZooKeeper を使用して Solr をスタンドアロンモードで実行する場合は、空白のままにします。
     *デフォルト*: *&lt;blank>*

      * **[!UICONTROL Solr URL]**
スタンドアロンモードで Solr との通信に使用する URL。
SolrCloud モードで実行する場合は空白のままにします。
        *デフォルト*: https://127.0.0.1:8983/solr/

      * **[!UICONTROL Solr コレクション]**
Solr コレクション名。
        *デフォルト*: collection1

* 「**[!UICONTROL 送信]**」を選択します。

>[!NOTE]
>
>mongoDB データベース（デフォルト値は名前） `communities`、に使用しているデータベース名に設定しないでください [ノードストアまたはデータ（バイナリ）ストア](../../help/sites-deploying/data-store-config.md). 関連トピック [AEM 6.5 のストレージ要素](../../help/sites-deploying/storage-elements-in-aem-6.md).

### MongoDB レプリカセット {#mongodb-replica-set}

実稼動環境の場合は、レプリカセット（プライマリセカンダリのレプリケーションと自動フェイルオーバーを実装する MongoDB サーバーのクラスター）を設定することを強くお勧めします。

レプリカセットについて詳しくは、MongoDB の [複製](https://docs.mongodb.org/manual/replication/) ドキュメント。

レプリカセットを操作し、アプリケーションと MongoDB インスタンス間の接続を定義する方法については、MongoDB の [接続文字列 URI 形式](https://docs.mongodb.org/manual/reference/connection-string/) ドキュメント。

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

Oak コレクションと MSRP コレクションの両方を集中的に使用する場合は、パフォーマンス上の理由から、2 つ目の Solr をインストールすることがあります。

実稼動環境の場合、 [SolrCloud モード](solr.md#solrcloud-mode) スタンドアロンモード（単一のローカル Solr セットアップ）よりもパフォーマンスが向上します。

設定について詳しくは、を参照してください [SRP 用の Solr 設定](solr.md).

### アップグレード {#upgrading}

MSRP が設定されている旧バージョンからアップグレードする場合、次の操作が必要になります。

1. を実行 [AEM Communitiesへのアップグレード](upgrade.md)
1. 新しい Solr 設定ファイルのインストール
   * の場合 [標準 MLS](solr.md#installing-standard-mls)
   * の場合 [高度 MLS](solr.md#installing-advanced-mls)
1. MSRP の再インデックス：セクションを参照 [MSRP インデックス再作成ツール](#msrp-reindex-tool)

## 設定の公開 {#publishing-the-configuration}

MSRP は、すべてのオーサーインスタンスとパブリッシュインスタンスで共通ストアとして識別される必要があります。

パブリッシュ環境で同一の設定を使用できるようにするには、オーサーインスタンスにログインし、次の手順に従います。

* メインメニューからに移動する **[!UICONTROL ツール]** > **[!UICONTROL 運用]** > **[!UICONTROL 複製]**.
* を選択 **[!UICONTROL ツリーのアクティベート]**
* **[!UICONTROL 開始パス]**:
   * を参照 `/etc/socialconfig/srpc/`
* を選択 **[!UICONTROL Activate]**

## ユーザーデータの管理 {#managing-user-data}

について *ユーザー*, *ユーザープロファイル* および *ユーザーグループ*（多くの場合、パブリッシュ環境で入力されます）

* [ユーザー同期](sync.md)
* [ユーザーとユーザーグループの管理](users.md)

## MSRP インデックス再作成ツール {#msrp-reindex-tool}

新しい設定ファイルをインストールする際や破損した Solr インデックスを修復する際に、MSRP 用の Solr のインデックスを再作成するための HTTP エンドポイントがあります。

このツールでは、MongoDB が次のソースとなります *真実* msrp の場合、バックアップに必要なのは MongoDB のみです。

UGC ツリー全体のインデックスを再作成することも、*path *data パラメーターで指定されているように、特定のサブツリーのみを再作成することもできます。

このツールは、cURL またはその他の HTTP ツールを使用して、コマンドラインから実行できます。

インデックスを再作成する場合、メモリとパフォーマンスは*batchSize*データパラメーターによって制御されるトレードオフがあります。このパラメーターは、バッチごとにインデックスを再作成する UGC レコードの数を指定します。

適切なデフォルトは 5000 です。

* メモリに問題がある場合は、より小さい数値を指定します
* 速度に問題がある場合は、より大きい数値を指定して速度を上げます

### cURL コマンドを使用した MSRP インデックス再作成ツールの実行 {#running-msrp-reindex-tool-using-curl-command}

次の cURL コマンドは、MSRP に格納された UGC を再インデックス化するための HTTP リクエストに必要な項目を示しています。

基本的な形式は次のとおりです。

cURL -u *サインイン* -d *データ* *reindex-url*

*サインイン* =administrator-id:password 例：admin:admin

*データ* = &quot;batchSize=*サイズ*&amp;path=*path&quot;*

*サイズ* =操作ごとに再インデックス化する UGC エントリの数
`/content/usergenerated/asi/mongo/`

*パス* =再インデックス化する UGC のツリーのルート位置

* すべての UGC を再インデックス化するには、の値を指定します。 `asipath`のプロパティ
  `/etc/socialconfig/srpc/defaultconfiguration`
* インデックスを一部の UGC に制限するには、次のサブツリーを指定します `asipath`

*reindex-url* = SRP のインデックス再作成用のエンドポイント
`http://localhost:4503/services/social/datastore/mongo/reindex`

>[!NOTE]
>
>次の場合： [dsrp Solr のインデックス再作成](dsrp.md)URL はです。 **/services/social/datastore/rdb/reindex**

### MSRP インデックス再作成の例 {#msrp-reindex-example}

```shell
curl -s -u admin:admin -d 'batchSize=10000&path=/content/usergenerated/asi/mongo/' http://localhost:4503/services/social/datastore/mongo/reindex
```

## MSRP のデモ方法 {#how-to-demo-msrp}

デモまたは開発環境用に MSRP を設定するには、を参照してください。 [MongoDB をデモ用に設定する方法](demo-mongo.md).

## トラブルシューティング {#troubleshooting}

### MongoDB に UGC が表示されない {#ugc-not-visible-in-mongodb}

ストレージオプションの設定をチェックして、MSRP がデフォルトのプロバイダーとして設定されていることを確認します。 デフォルトでは、ストレージリソースプロバイダーは JSRP です。

すべてのオーサーインスタンスおよびパブリッシュ AEMインスタンスで、次を再参照します [ストレージ設定コンソール](srp-config.md) または、AEM リポジトリを確認します。

* JCR で次の場合： [/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/)

   * 次を含まない [srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc) ノードの場合は、ストレージプロバイダーが JSRP であることを意味します。
   * srpc ノードが存在し、ノードがを含む場合 [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration)が設定されている場合は、defaultconfiguration のプロパティで MSRP をデフォルトのプロバイダーとして定義する必要があります。

### アップグレード後に UGC が表示されなくなる {#ugc-disappears-after-upgrade}

既存のAEM Communities 6.0 サイトからアップグレードする場合は、既存の UGC を、 [SRP](srp.md) AEM Communities 6.3 へのアップグレード後の API。

この目的のために、GitHub で利用できるオープンソースのツールがあります。

* [AEM Communities UGC Migration Tool](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

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

このエラーを解決するには、次の手順を行います： [標準 MLS のインストール](solr.md#installing-standard-mls)必ず以下を行ってください。

* XML 設定ファイルが正しい Solr の場所にコピーされました。
* 新しい設定ファイルが既存の設定ファイルに置き換えられた後、Solr が再起動された。

### MongoDB への安全な接続に失敗 {#secure-connection-to-mongodb-fails}

クラス定義が見つからないために MongoDB サーバーへのセキュリティで保護された接続を確立しようとする試みが失敗した場合は、MongoDB ドライバーバンドルを更新する必要があります。 `mongo-java-driver`公開 maven リポジトリから入手できます。

1. ドライバーのダウンロード元： [https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar](https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar) （バージョン 2.13.2 以降）。
1. バンドルをAEM インスタンスの「crx-quickstart/install」フォルダーにコピーします。
1. AEM インスタンスを再起動します。

## リソース {#resources}

* [MongoDB を備えた AEM](../../help/sites-deploying/aem-with-mongodb.md)
* [MongoDB のドキュメント](https://docs.mongodb.org/)
