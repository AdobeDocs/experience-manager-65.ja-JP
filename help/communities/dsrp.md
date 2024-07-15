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

[SRP オプションの特性 ](working-with-srp.md#characteristics-of-srp-options) および [ 推奨されるトポロジ ](topologies.md) も参照してください。

## 要件 {#requirements}

* [MySQL](#mysql-configuration)：リレーショナルデータベース。
* [Apache Solr](#solr-configuration)：検索プラットフォーム

>[!NOTE]
>
>デフォルトのストレージ設定は、パス（`/etc/socialconfig/srpc/defaultconfiguration`）ではなく conf path （`/conf/global/settings/community/srpc/defaultconfiguration`） `etc` 保存されるようになりました。 defaultsrp が期待どおりに動作するように [ 移行手順 ](#zerodt-migration-steps) に従うことをお勧めします。

## リレーショナルデータベースの設定 {#relational-database-configuration}

### MySQL 設定 {#mysql-configuration}

MySQL インストールは、異なるデータベース（スキーマ）名と異なる接続（サーバー：ポート）を使用することで、同じ接続プール内のイネーブルメント機能と共通ストア（DSRP）の間で共有されます。

インストールと設定について詳しくは、[DSRP 用の MySQL 設定 ](dsrp-mysql.md) を参照してください。

### Solr 設定 {#solr-configuration}

Solr インストールは、異なるコレクションを使用して、ノードストア（Oak）と共通ストア（SRP）の間で共有できます。

Oakと SRP の両方のコレクションを集中的に使用する場合は、パフォーマンス上の理由から、2 つ目の Solr をインストールすることがあります。

実稼動環境では、SolrCloud モードはスタンドアロンモード（単一のローカル Solr セットアップ）よりもパフォーマンスが向上します。

インストールと設定について詳しくは、[SRP 用の Solr 設定 ](solr.md) を参照してください。

### DSRP を選択 {#select-dsrp}

[ ストレージ設定コンソール ](srp-config.md) では、デフォルトのストレージ設定を選択でき、使用する SRP の実装を識別できます。

オーサー環境で、ストレージ設定コンソールにアクセスします。

* 管理者権限でログイン
* **メインメニュー** から

   * 左側のパネルから **[!UICONTROL ツール]** を選択します
   * **[!UICONTROL Communities]** を選択します
   * 「**[!UICONTROL ストレージ設定]**」を選択します。

      * 例えば、結果の場所は [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp) になります。

     >[!NOTE]
     >
     >デフォルトのストレージ設定が conf path （`/conf/global/settings/community/srpc/defaultconfiguration`）に保存されるようになりました。      パス（`/etc/socialconfig/srpc/defaultconfiguration`） `etc` 代わりに使用します。 defaultsrp が期待どおりに動作するように [ 移行手順 ](#zerodt-migration-steps) に従うことをお勧めします。

  ![dsrp-config](assets/dsrp-config.png)

* 「**[!UICONTROL データベースストレージリソースプロバイダー（DSRP）]**」を選択します。
* **データベース構成**

   * **[!UICONTROL JDBC データソース名]**

     MySQL 接続に付ける名前は、[JDBC OSGi 設定 ](dsrp-mysql.md#configurejdbcconnections) で入力した名前と同じにする必要があります。

     *デフォルト*: communities

   * **[!UICONTROL データベース名]**

     [init_schema.sql](dsrp-mysql.md#obtain-the-sql-script) スクリプトでスキーマに指定された名前

     *デフォルト*: communities

* **SolrConfiguration**

   * **[Zookeeper](https://solr.apache.org/guide/6_6/using-zookeeper-to-manage-configuration-files.html) ホスト**

     内部の ZooKeeper を使用して Solr を実行する場合は、この値を空白のままにします。 それ以外の場合、外部の ZooKeeper を使用して [SolrCloud モード ](solr.md#solrcloud-mode) で実行する場合、この値を ZooKeeper の URI に設定します（*my.server.com:80など）*

     *デフォルト*: *&lt;blank>*

   * **[!UICONTROL Solr URL]**

     *デフォルト*:https://127.0.0.1:8983/solr/

   * **[!UICONTROL Solr コレクション]**

     *default*: collection1

* 「**[!UICONTROL 送信]**」を選択します。

### Defaultsrp のダウンタイムなしの移行手順 {#zerodt-migration-steps}

defaultsrp ページ [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp) が期待どおりに動作することを確認するには、次の手順に従います。

1. `/etc/socialconfig` のパスの名前を `/etc/socialconfig_old` に変更して、システム設定が jsrp （デフォルト）にフォールバックするようにします。
1. defaultsrp ページ [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp) に移動します。ここでは、jsrp が設定されています。 **[!UICONTROL 送信]** ボタンをクリックして、新しいデフォルト設定ノードが `/conf/global/settings/community/srpc` に作成されるようにします。
1. 作成したデフォルト設定 `/conf/global/settings/community/srpc/defaultconfiguration` を削除します。
1. 前の手順で削除したノード（`/conf/global/settings/community/srpc/defaultconfiguration`）の代わりに、古い設定 `/etc/socialconfig_old/srpc/defaultconfiguration` をコピーします。
1. 古い `etc` ノード `/etc/socialconfig_old` を削除します。

## 設定の公開 {#publishing-the-configuration}

DSRP は、すべてのオーサーインスタンスとパブリッシュインスタンスで共通ストアとして識別される必要があります。

パブリッシュ環境で同一の設定を使用できるようにするには：

* オーサー環境で：

   * メインメニューから **[!UICONTROL ツール]**/**[!UICONTROL オペレーション]**/**[!UICONTROL レプリケーション]** に移動します。
   * **[!UICONTROL ツリーをアクティブにする]** をダブルクリックします
   * **開始パス**:

      * `/etc/socialconfig/srpc/` を参照します

   * `Only Modified` が選択されていないことを確認します。
   * **[!UICONTROL アクティブ化]** を選択します。

## ユーザーデータの管理 {#managing-user-data}

パブリッシュ環境で入力されることが多い *ユーザー*、*ユーザープロファイル* および *ユーザーグループ* に関する情報は、次をご覧ください。

* [ユーザー同期](sync.md)
* [ユーザーとユーザーグループの管理](users.md)

## Solr for DSRP のインデックス再作成 {#reindexing-solr-for-dsrp}

DSRP Solr のインデックスを再作成するには、[MSRP のインデックス再作成 ](msrp.md#msrp-reindex-tool) のドキュメントに従います。ただし、DSRP のインデックスを再作成する場合は、代わりに次の URL を使用します。**/services/social/datastore/rdb/reindex**

例えば、DSRP を再インデックス化する curl コマンドは、次のようになります。

```shell
curl -u admin:password -X POST -F path=/ https://host:port/services/social/datastore/rdb/reindex
```
