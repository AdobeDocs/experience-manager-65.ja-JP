---
title: DSRP - リレーショナルデータベースストレージリソースプロバイダー
description: リレーショナルデータベースを共通ストアとして使用するようにAEM Communitiesを設定します
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 15b3a594-efde-4702-9233-232ba1c7e5b0
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 4%

---

# DSRP - リレーショナルデータベースストレージリソースプロバイダー {#dsrp-relational-database-storage-resource-provider}

## DSRP について {#about-dsrp}

リレーショナルデータベースを共通ストアとして使用するようにAEM Communitiesが設定されている場合、ユーザー生成コンテンツ（UGC）には、すべてのオーサーインスタンスとパブリッシュインスタンスからアクセスでき、同期やレプリケーションを行う必要はありません。

関連トピック [SRP オプションの特徴](working-with-srp.md#characteristics-of-srp-options) および [推奨されるトポロジ](topologies.md).

## 要件 {#requirements}

* [MySQL](#mysql-configuration)：リレーショナルデータベース。
* [Apache Solr](#solr-configuration)：検索プラットフォーム

>[!NOTE]
>
>デフォルトのストレージ設定は、conf path （`/conf/global/settings/community/srpc/defaultconfiguration`）に設定します。 `etc` パス （`/etc/socialconfig/srpc/defaultconfiguration`）に設定します。 次の手順に従うことをお勧めします [移行手順](#zerodt-migration-steps) デフォルトの srp が期待どおりに動作するようにします。

## リレーショナルデータベースの設定 {#relational-database-configuration}

### MySQL 設定 {#mysql-configuration}

MySQL インストールは、異なるデータベース（スキーマ）名と異なる接続（サーバー：ポート）を使用することで、同じ接続プール内のイネーブルメント機能と共通ストア（DSRP）の間で共有されます。

インストールと設定の詳細については、を参照してください。 [DSRP 用の MySQL 設定](dsrp-mysql.md).

### Solr 設定 {#solr-configuration}

Solr インストールは、異なるコレクションを使用して、ノードストア（Oak）と共通ストア（SRP）の間で共有できます。

Oak コレクションと SRP コレクションの両方を集中的に使用する場合は、パフォーマンス上の理由から、2 つ目の Solr をインストールすることがあります。

実稼動環境では、SolrCloud モードはスタンドアロンモード（単一のローカル Solr セットアップ）よりもパフォーマンスが向上します。

インストールと設定の詳細については、を参照してください。 [SRP 用の Solr 設定](solr.md).

### DSRP を選択 {#select-dsrp}

この [ストレージ設定コンソール](srp-config.md) デフォルトのストレージ設定を選択でき、使用する SRP の実装を識別できます。

オーサー環境で、ストレージ設定コンソールにアクセスします。

* 管理者権限でログイン
* から **メインメニュー**

   * を選択 **[!UICONTROL ツール]** （左側のウィンドウから）
   * を選択 **[!UICONTROL コミュニティ]**
   * を選択 **[!UICONTROL ストレージ設定]**

      * 例えば、次の場所が生成されます。 [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)

     >[!NOTE]
     >
     >デフォルトのストレージ設定は、conf path （`/conf/global/settings/community/srpc/defaultconfiguration`）に設定します。 `etc` パス （`/etc/socialconfig/srpc/defaultconfiguration`）に設定します。 次の手順に従うことをお勧めします [移行手順](#zerodt-migration-steps) デフォルトの srp が期待どおりに動作するようにします。

  ![dsrp-config](assets/dsrp-config.png)

* を選択 **[!UICONTROL データベースストレージリソースプロバイダー（DSRP）]**
* **データベース設定**

   * **[!UICONTROL JDBC データソース名]**

     MySQL 接続に指定する名前は、で入力した名前と同じである必要があります [JDBC OSGi 設定](dsrp-mysql.md#configurejdbcconnections)

     *default*: communities

   * **[!UICONTROL データベース名]**

     のスキーマに指定された名前 [init_schema.sql](dsrp-mysql.md#obtain-the-sql-script) script

     *default*: communities

* **SolrConfiguration**

   * **[飼育員](https://solr.apache.org/guide/6_6/using-zookeeper-to-manage-configuration-files.html) ホスト**

     内部の ZooKeeper を使用して Solr を実行する場合は、この値を空白のままにします。 それ以外の場合（で実行している場合） [SolrCloud モード](solr.md#solrcloud-mode) 外部の ZooKeeper で、次のように、この値を ZooKeeper の URI に設定します *my.server.com:80*

     *default*: *&lt;blank>*

   * **[!UICONTROL Solr URL]**

     *default*: https://127.0.0.1:8983/solr/

   * **[!UICONTROL Solr コレクション]**

     *default*: collection1

* 「**[!UICONTROL 送信]**」を選択します。

### Defaultsrp のダウンタイムなしの移行手順 {#zerodt-migration-steps}

デフォルトの srp ページの確認方法 [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp) は期待どおりに動作します。次の手順に従います。

1. でパスの名前を変更します `/etc/socialconfig` 対象： `/etc/socialconfig_old`システム設定が jsrp （デフォルト）にフォールバックするようにします。
1. defaultsrp ページに移動 [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)ここでは、jsrp が設定されています。 「」をクリックします **[!UICONTROL submit]** ボタンをクリックして、新しいデフォルト設定ノードがに作成されるようにします `/conf/global/settings/community/srpc`.
1. 作成したデフォルト設定の削除 `/conf/global/settings/community/srpc/defaultconfiguration`.
1. 古い設定をコピーします `/etc/socialconfig_old/srpc/defaultconfiguration` 削除したノードの代わりに（`/conf/global/settings/community/srpc/defaultconfiguration`）を選択します。
1. 旧バージョンを削除 `etc` ノード `/etc/socialconfig_old`.

## 設定の公開 {#publishing-the-configuration}

DSRP は、すべてのオーサーインスタンスとパブリッシュインスタンスで共通ストアとして識別される必要があります。

パブリッシュ環境で同一の設定を使用できるようにするには：

* オーサー環境で：

   * メインメニューからに移動する **[!UICONTROL ツール]** > **[!UICONTROL 運用]** > **[!UICONTROL 複製]**
   * ダブルクリック **[!UICONTROL ツリーのアクティベート]**
   * **開始パス**:

      * を参照 `/etc/socialconfig/srpc/`

   * 確保する `Only Modified` が選択されていません。
   * を選択 **[!UICONTROL Activate]**.

## ユーザーデータの管理 {#managing-user-data}

について *ユーザー*, *ユーザープロファイル* および *ユーザーグループ*（パブリッシュ環境で入力することが多い）次を参照してください。

* [ユーザー同期](sync.md)
* [ユーザーとユーザーグループの管理](users.md)

## Solr for DSRP のインデックス再作成 {#reindexing-solr-for-dsrp}

DSRP Solr のインデックスを再作成するには、次のドキュメントに従います [msrp のインデックス再作成](msrp.md#msrp-reindex-tool)ただし、DSRP のインデックスを再作成する場合は、代わりにこの URL を使用します。 **/services/social/datastore/rdb/reindex**

例えば、DSRP を再インデックス化する curl コマンドは、次のようになります。

```shell
curl -u admin:password -X POST -F path=/ https://host:port/services/social/datastore/rdb/reindex
```
