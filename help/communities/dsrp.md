---
title: DSRP - リレーショナルデータベースストレージリソースプロバイダー
seo-title: DSRP - Relational Database Storage Resource Provider
description: リレーショナルデータベースを共通ストアとして使用するように AEM Communities を設定する
seo-description: Set up AEM Communities to use a relational database as its common store
uuid: f364e7da-ee54-4ab2-a630-7ec9239005ac
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d23acb18-6761-4290-9e7a-a434582791bd
role: Admin
exl-id: 15b3a594-efde-4702-9233-232ba1c7e5b0
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 49%

---

# DSRP - リレーショナルデータベースストレージリソースプロバイダー {#dsrp-relational-database-storage-resource-provider}

## DSRP について {#about-dsrp}

リレーショナルデータベースを共通ストアとして使用するように AEM Communities を設定すると、すべてのオーサーインスタンスとパブリッシュインスタンスからユーザー生成コンテンツ（UGC）にアクセスでき、同期やレプリケーションをおこなう必要はありません。

[SRP オプションの特性](working-with-srp.md#characteristics-of-srp-options)と[推奨されるトポロジ](topologies.md)も参照してください。

## 要件 {#requirements}

* [MySQL](#mysql-configuration)：リレーショナルデータベース.
* [Apache Solr](#solr-configuration)：検索プラットフォーム.

>[!NOTE]
>
>デフォルトのストレージ設定が conf path(`/conf/global/settings/community/srpc/defaultconfiguration`) の代わりに etc パス (`/etc/socialconfig/srpc/defaultconfiguration`) をクリックします。 以下をフォローするようお勧めします。 [移行手順](#zerodt-migration-steps) defaultsrp を期待どおりに動作させる。

## リレーショナルデータベースの設定 {#relational-database-configuration}

### MySQL 設定 {#mysql-configuration}

別々のデータベース（スキーマ）名と別々の接続（server:port）を使用することで、1 つの MySQL を同じ接続プール内のイネーブルメント機能と共通ストア（DSRP）の間で共有できます。

インストールと設定の詳細については、 [DSRP 用の MySQL 設定](dsrp-mysql.md).

### Solr 設定 {#solr-configuration}

別々のコレクションを使用することで、1 つの Solr をノードストア（Oak）と共通ストア（SRP）の間で共有できます。

Oak と SRP のコレクションがどちらも高頻度で使用される場合は、パフォーマンス上の理由から 2 つ目の Solr をインストールすることもできます。

実稼動環境では、SolrCloud モードを使用すると、スタンドアロンモード（単一のローカル Solr セットアップ）よりもパフォーマンスが向上します。

インストールと設定について詳しくは、[SRP 向け Solr 設定](solr.md)を参照してください。

### DSRP の選択 {#select-dsrp}

この [ストレージ設定コンソール](srp-config.md) では、使用する SRP の実装を指定するデフォルトのストレージ設定を選択できます。

オーサー環境でストレージ設定コンソールにアクセスするには

* 管理者権限でログイン
* 次の **メインメニュー**

   * 選択 **[!UICONTROL ツール]** （左側のウィンドウから）
   * 選択 **[!UICONTROL コミュニティ]**
   * 選択 **[!UICONTROL ストレージ設定]**

      * 例えば、結果として得られる場所は次のようになります。 [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)
      >[!NOTE]
      >
      >デフォルトのストレージ設定が conf path(`/conf/global/settings/community/srpc/defaultconfiguration`) の代わりに etc パス (`/etc/socialconfig/srpc/defaultconfiguration`) をクリックします。 以下をフォローするようお勧めします。 [移行手順](#zerodt-migration-steps) defaultsrp を期待どおりに動作させる。
   ![dsrp-config](assets/dsrp-config.png)

* 選択 **[!UICONTROL データベースストレージリソースプロバイダー (DSRP)]**
* **データベース設定**

   * **[!UICONTROL JDBC データソース名]**

      MySQL 接続に指定する名前は、 [JDBC OSGi 設定](dsrp-mysql.md#configurejdbcconnections)

      *デフォルト*:コミュニティ

   * **[!UICONTROL データベース名]**

      でスキーマに指定された名前 [init_schema.sql](dsrp-mysql.md#obtain-the-sql-script) スクリプト

      *デフォルト*:コミュニティ

* **SolrConfiguration**

   * **[](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files)Zookeeper ホスト**

      内部 ZooKeeper を使用して Solr を実行する場合は、この値を空白のままにします。 それ以外の場合は、で実行します [SolrCloud モード](solr.md#solrcloud-mode) 外部の ZooKeeper を使用して、この値を ZooKeeper の URI に設定します。例： *my.server.com:80*

      *デフォルト*: *&lt;blank>*

   * **[!UICONTROL Solr URL]**

      *デフォルト*:https://127.0.0.1:8983/solr/

   * **[!UICONTROL Solr コレクション]**

      *デフォルト*：collection1

* **[!UICONTROL 送信]**&#x200B;を選択します。

### defaultsrp のダウンタイムなしの移行手順 {#zerodt-migration-steps}

次の手順に従って、デフォルトの SRP ページが [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp) は期待どおりに動作します。

1. パスの名前をに変更します。 `/etc/socialconfig` から `/etc/socialconfig_old`を使用する場合、システム設定は jsrp（デフォルト）にフォールバックされます。
1. defaultsrp ページに移動 [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)（jsrp が設定されている場所） 次をクリック： **[!UICONTROL 送信]** ボタンを使用して、新しいデフォルト設定ノードを `/conf/global/settings/community/srpc`.
1. 作成したデフォルト設定を削除 `/conf/global/settings/community/srpc/defaultconfiguration`.
1. 古い設定をコピーします。 `/etc/socialconfig_old/srpc/defaultconfiguration` 削除されたノード (`/conf/global/settings/community/srpc/defaultconfiguration`) をクリックします。
1. 古い etc ノードを削除します。 `/etc/socialconfig_old`.

## 設定の公開 {#publishing-the-configuration}

すべてのオーサーインスタンスとパブリッシュインスタンスで、DSRP が共通ストアとして指定されている必要があります。

パブリッシュ環境で同一の設定を使用できるようにするには：

* 作成者：

   * メインメニューからに移動します。 **[!UICONTROL ツール]** > **[!UICONTROL 運用]** > **[!UICONTROL レプリケーション]**
   * ダブルクリック **[!UICONTROL ツリーをアクティベート]**
   * **開始パス**:

      * 参照先 `/etc/socialconfig/srpc/`
   * 確認 `Only Modified` が選択されていません。
   * 選択 **[!UICONTROL 有効化]**.


## ユーザーデータの管理 {#managing-user-data}

パブリッシュ環境で頻繁に入力されるユーザー、ユーザープロファイルおよびユーザーグループについては、以下を参照してください。******：

* [ユーザー同期](sync.md)
* [ユーザーとユーザーグループの管理](users.md)

## DSRP の Solr のインデックス再作成 {#reindexing-solr-for-dsrp}

DSRP Solr のインデックスを再作成するには、[MSRP のインデックスの再作成](msrp.md#msrp-reindex-tool)に関するドキュメントの説明に従います。ただし、DSRP のインデックスを再作成する場合は、この URL を使用します：**/services/social/datastore/rdb/reindex**

例えば、DSRP のインデックスを再作成する curl コマンドは次のようになります。

```shell
curl -u admin:password -X POST -F path=/ https://host:port/services/social/datastore/rdb/reindex
```
