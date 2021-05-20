---
title: DSRP 向け MySQL 設定
seo-title: DSRP 向け MySQL 設定
description: MySQL サーバーに接続し、UGC データベースを設定する方法
seo-description: MySQL サーバーに接続し、UGC データベースを設定する方法
uuid: c058cc88-7ca2-4aed-9a36-b080e603f886
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: edc3043c-7ec4-4e4a-b008-95f1784f012e
role: Administrator
exl-id: eafb60be-2963-4ac9-8618-50fd9bc6fe6c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '746'
ht-degree: 47%

---

# DSRP 向け MySQL 設定  {#mysql-configuration-for-dsrp}

MySQL は、ユーザー生成コンテンツ（UGC）の保存に使用できるリレーショナルデータベースです。

次の手順で、MySQL サーバーに接続し、UGC データベースを設定する方法について説明します。

## 要件 {#requirements}

* [最新のコミュニティ機能パック](deploy-communities.md#latestfeaturepack)
* [MySQL 用 JDBC ドライバー](deploy-communities.md#jdbc-driver-for-mysql)
* リレーショナル・データベース：

   * [MySQL ](https://dev.mysql.com/downloads/mysql/) serverCommunity Serverバージョン5.6以降

      * AEMと同じホスト上で実行するか、リモートで実行する
   * [MySQL Workbench](https://dev.mysql.com/downloads/tools/workbench/)


## MySQL のインストール  {#installing-mysql}

対象 OS の手順に従い、[MySQL](https://dev.mysql.com/downloads/mysql/) をダウンロードしてインストールする必要があります。

### 小文字のテーブル名 {#lower-case-table-names}

SQL では大文字と小文字が区別されます。大文字と小文字が区別されるオペレーティングシステムでは、すべてのテーブル名を小文字にする設定を含める必要があります。

例えば、Linux OS でテーブル名をすべて小文字に指定するには、

* ファイル`/etc/my.cnf`を編集
* `[mysqld]`セクションに次の行を追加します。

   `lower_case_table_names = 1`

### UTF8 文字セット {#utf-character-set}

より優れた多言語対応を実現するには、UTF8 文字セットを使用する必要があります。

以下の操作で MySQL の文字セットを UTF8 に変更します。

* mysql> SET NAMES &#39;utf8&#39;;

以下の操作で MySQL データベースをデフォルトから UTF8 に変更します。

* ファイル`/etc/my.cnf`を編集
* `[client]`セクションに次の行を追加します。

   `default-character-set=utf8`

* `[mysqld]`セクションに次の行を追加します。

   `character-set-server=utf8`

## MySQL Workbench のインストール {#installing-mysql-workbench}

MySQL Workbench には、スキーマと初期データをインストールする SQL スクリプトを実行するための UI が用意されています。

ターゲットOSの手順に従って、MySQL Workbenchをダウンロードし、インストールする必要があります。

## Communities の接続 {#communities-connection}

MySQL Workbench を初めて起動したときは（他の目的で既に使用されていない場合）、接続はまだ表示されません。

![mysqlconnection](assets/mysqlconnection.png)

### 新しい接続の設定 {#new-connection-settings}

1. `MySQL Connections`の右側にある`+`アイコンを選択します。
1. ダイアログ`Setup New Connection`で、使用するプラットフォームに適した値を入力します

   デモ用に、オーサーAEMインスタンスとMySQLを同じサーバー上に配置します。

   * 接続名: `Communities`
   * 接続方法：`Standard (TCP/IP)`
   * Hostname：`127.0.0.1`
   * ユーザー名: `root`
   * パスワード: `no password by default`
   * デフォルトのスキーマ：`leave blank`

1. `Test Connection`を選択して、実行中のMySQLサービスへの接続を確認します

**備考**:

* デフォルトのポートは`3306`です。
* 選択した接続名は、[JDBC OSGi configuration](#configurejdbcconnections)にデータソース名として入力されます。

#### 新しい Communities 接続 {#new-communities-connection}

![community-connection](assets/community-connection.png)

## データベースのセットアップ {#database-setup}

データベースをインストールするには、Communities 接続を開きます。

![install-database](assets/install-database.png)

### SQL スクリプトの取得 {#obtain-the-sql-script}

SQL スクリプトは、AEM リポジトリから取得されます。

1. CRXDE Lite

   * 例：[http://localhost:4502/crx/de](http://localhost:4502/crx/de)

1. /libs/social/config/datastore/dsrp/schemaフォルダーを選択します。
1. ダウンロード `init-schema.sql`

   ![database-schema-crxde](assets/database-schema-crxde.png)

スキーマをダウンロードする方法の1つは次のとおりです。

* sqlファイルの`jcr:content`ノードを選択します。
* `jcr:data`プロパティの値はビューリンクです

* データをローカルファイルに保存するには、表示リンクを選択します

### DSRP データベースの作成 {#create-the-dsrp-database}

以下の手順に従って、データベースをインストールします。 データベースのデフォルト名は`communities`です。

スクリプトでデータベース名を変更する場合は、[JDBC 設定](#configurejdbcconnections)でも変更してください。

#### 手順 1：SQL ファイルを開く {#step-open-sql-file}

MySQL Workbench で、以下の設定をおこないます。

* 「ファイル」プルダウンメニューから、「**[!UICONTROL SQLスクリプトを開く]**」オプションを選択します。
* ダウンロードした`init_schema.sql`スクリプトを選択します

![select-sql-script](assets/select-sql-script.png)

#### 手順 2：SQL スクリプトの実行 {#step-execute-sql-script}

手順1で開いたファイルのWorkbenchウィンドウで、スクリプトを実行する`lightening (flash) icon`を選択します。

以下の画像では、`init_schema.sql` ファイルは実行可能です。

![execute-sql-script](assets/execute-sql-script.png)

#### 更新 {#refresh}

スクリプトを実行したら、新しいデータベースを表示するために、`Navigator`の`SCHEMAS`セクションを更新する必要があります。 以下のように、「SCHEMAS」の右側にある更新アイコンを使用します。

![refresh-schema](assets/refresh-schema.png)

## JDBC 接続の設定 {#configure-jdbc-connection}

**Day Commons JDBC Connections Pool** の OSGi 設定では、MySQL JDBC ドライバーを設定します。

すべての AEM パブリッシュインスタンスおよびオーサーインスタンスが、同じ MySQL サーバーを指している必要があります。

MySQLをAEMとは別のサーバーで実行する場合は、JDBCコネクタの「localhost」の代わりにサーバーホスト名を指定する必要があります。

* 各オーサーインスタンスとパブリッシュAEMインスタンスで、
* 管理者権限でサインインしています。
* [Webコンソール](../../help/sites-deploying/configuring-osgi.md)にアクセスします。

   * 例： [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)

* `Day Commons JDBC Connections Pool`
* `+`アイコンを選択して、新しい接続設定を作成します。

   ![configure-jdbc-connection](assets/configure-jdbc-connection.png)

* 次の値を入力します。

   * **[!UICONTROL JDBC ドライバークラス]**: `com.mysql.jdbc.Driver`
   * **[!UICONTROL JDBC 接続 URI]**: `jdbc:mysql://localhost:3306/communities?characterEncoding=UTF-8`

      MySQLサーバーが「this」 AEM server *communities*&#x200B;がデフォルトのデータベース（スキーマ）名と同じでない場合は、localhostの代わりにサーバーを指定します。

   * **[!UICONTROL ユーザー名]**: `root`

      MySQLサーバーの設定済みのユーザー名（「root」でない場合）を入力します。

   * **[!UICONTROL パスワード]**:

      MySQLのパスワードが設定されていない場合は、このフィールドをクリアします。

      「 」を選択しない場合は、MySQLユーザー名用に設定したパスワードを入力します。

   * **[!UICONTROL データソース名]**:MySQL接続用に [入力された名前](#new-connection-settings)（例：「communities」）。

* 「**[!UICONTROL 保存]**」を選択します。
