---
title: DSRP - リレーショナルデータベースストレージリソースプロバイダー
seo-title: DSRP - リレーショナルデータベースストレージリソースプロバイダー
description: リレーショナルデータベースを共通ストアとして使用するように AEM Communities を設定する
seo-description: リレーショナルデータベースを共通ストアとして使用するように AEM Communities を設定する
uuid: f364e7da-ee54-4ab2-a630-7ec9239005ac
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d23acb18-6761-4290-9e7a-a434582791bd
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 48%

---


# DSRP - リレーショナルデータベースストレージリソースプロバイダー  {#dsrp-relational-database-storage-resource-provider}

## DSRP について {#about-dsrp}

リレーショナルデータベースを共通ストアとして使用するように AEM Communities を設定すると、すべてのオーサーインスタンスとパブリッシュインスタンスからユーザー生成コンテンツ（UGC）にアクセスでき、同期やレプリケーションをおこなう必要はありません。

[SRP オプションの特性](working-with-srp.md#characteristics-of-srp-options)と[推奨されるトポロジ](topologies.md)も参照してください。

## 要件 {#requirements}

* [MySQL](#mysql-configuration)：リレーショナルデータベース.
* [Apache Solr](#solr-configuration)：検索プラットフォーム.

>[!NOTE]
>
>デフォルトのストレージ設定は、etcパス(`/etc/socialconfig/srpc/defaultconfiguration`)ではなくconfパス(`/conf/global/settings/community/srpc/defaultconfiguration`)に保存されるようになりました。 defaultsrpを期待どおりに動作させるには、[移行手順](#zerodt-migration-steps)に従うようにお勧めします。

## リレーショナルデータベースの設定 {#relational-database-configuration}

### MySQL 設定 {#mysql-configuration}

別々のデータベース（スキーマ）名と別々の接続（server:port）を使用することで、1 つの MySQL を同じ接続プール内のイネーブルメント機能と共通ストア（DSRP）の間で共有できます。

インストールと設定の詳細については、[MySQL Configuration for DSRP](dsrp-mysql.md)を参照してください。

### Solr 設定 {#solr-configuration}

別々のコレクションを使用することで、1 つの Solr をノードストア（Oak）と共通ストア（SRP）の間で共有できます。

Oak と SRP のコレクションがどちらも高頻度で使用される場合は、パフォーマンス上の理由から 2 つ目の Solr をインストールすることもできます。

実稼働環境では、SolrCloudモードを使用すると、スタンドアロンモード（ローカルで単一のSolr設定）よりもパフォーマンスが向上します。

インストールと設定について詳しくは、[SRP 向け Solr 設定](solr.md)を参照してください。

### DSRP の選択  {#select-dsrp}

[ストレージ設定コンソール](srp-config.md)では、デフォルトのストレージ設定を選択できます。これにより、使用するSRPの実装が識別されます。

オーサー環境でストレージ設定コンソールにアクセスするには

* 管理者権限でサインインする
* **メインメニュー**&#x200B;から

   * **[!UICONTROL ツール]**&#x200B;を選択します（左側のペインから）
   * **[!UICONTROL コミュニティ]**&#x200B;を選択
   * **[!UICONTROL ストレージ設定]**&#x200B;を選択

      * 例として、結果の場所は次のようになります。[http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)
      >[!NOTE]
      >
      >デフォルトのストレージ設定は、confパス(`/conf/global/settings/community/srpc/defaultconfiguration`)に保存されるようになりました。      の代わりに、etcパス(`/etc/socialconfig/srpc/defaultconfiguration`)が使用されます。 defaultsrpを期待どおりに動作させるには、[移行手順](#zerodt-migration-steps)に従うようにお勧めします。
   ![dsrp-config](assets/dsrp-config.png)

* **[!UICONTROL データベースストレージリソースプロバイダー(DSRP)]**&#x200B;を選択します
* **データベース設定**

   * **[!UICONTROL JDBC データソース名]**

      MySQL接続に指定する名前は、[JDBC OSGi設定](dsrp-mysql.md#configurejdbcconnections)に入力した名前と同じである必要があります

      *default*:コミュニティ

   * **[!UICONTROL データベース名]**

      [init_スキーマ.sql](dsrp-mysql.md#obtain-the-sql-script)スクリプトのスキーマに与えられた名前

      *default*:コミュニティ

* **SolrConfiguration**

   * **[](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files)Zookeeper ホスト**

      内部ZooKeeperを使用してSolrを実行する場合は、この値を空白のままにします。 それ以外の場合は、[SolrCloudモード](solr.md#solrcloud-mode)で外部のZooKeeperと共に実行する場合、*my.server.com:80*&#x200B;のように、この値をZooKeeperのURIに設定します。

      *default*:  *&lt;blank>*

   * **[!UICONTROL Solr URL]**

      *default*:https://127.0.0.1:8983/solr/

   * **[!UICONTROL Solr コレクション]**

      *デフォルト*：collection1

* 「**[!UICONTROL 送信]**」を選択します。

### defaultsrp {#zerodt-migration-steps}のダウンタイムをゼロにする

次の手順に従って、デフォルトのSRPページ[http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)が期待どおりに動作することを確認します。

1. パスの名前を`/etc/socialconfig`から`/etc/socialconfig_old`に変更し、システム設定がjsrp(default)にフォールバックされるようにします。
1. defaultsrpページ[http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)に移動します。ここで、jsrpが設定されています。 「**[!UICONTROL submit]**」ボタンをクリックすると、新しいデフォルト設定ノードが`/conf/global/settings/community/srpc`に作成されます。
1. 作成したデフォルトの構成`/conf/global/settings/community/srpc/defaultconfiguration`を削除します。
1. 前の手順で削除したノード(`/conf/global/settings/community/srpc/defaultconfiguration`)の代わりに、古い構成`/etc/socialconfig_old/srpc/defaultconfiguration`をコピーします。
1. 古いetcノード`/etc/socialconfig_old`を削除します。

## 設定の公開 {#publishing-the-configuration}

すべてのオーサーインスタンスとパブリッシュインスタンスで、DSRP が共通ストアとして指定されている必要があります。

パブリッシュ環境で同一の設定を使用できるようにするには：

* 作成者：

   * メインメニューから&#x200B;**[!UICONTROL ツール]** > **[!UICONTROL 操作]** > **[!UICONTROL レプリケーション]**&#x200B;に移動します。
   * **[!UICONTROL ツリーのアクティブ化]**&#x200B;を重複クリック
   * **開始パス**:

      * `/etc/socialconfig/srpc/`を参照
   * `Only Modified`が選択されていないことを確認します。
   * 「**[!UICONTROL アクティブ化]**」を選択します。


## ユーザーデータの管理 {#managing-user-data}

*ユーザー*、*ユーザープロファイル*、*ユーザーグループ*&#x200B;に関する情報は、次のページにアクセスしてください。

* [ユーザーの同期](sync.md)
* [ユーザーとユーザーグループの管理](users.md)

## DSRP の Solr のインデックス再作成  {#reindexing-solr-for-dsrp}

DSRP Solr のインデックスを再作成するには、[MSRP のインデックスの再作成](msrp.md#msrp-reindex-tool)に関するドキュメントの説明に従います。ただし、DSRP のインデックスを再作成する場合は、この URL を使用します：**/services/social/datastore/rdb/reindex**

例えば、DSRP のインデックスを再作成する curl コマンドは次のようになります。

```shell
curl -u admin:password -X POST -F path=/ https://host:port/services/social/datastore/rdb/reindex
```

