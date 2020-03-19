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
translation-type: tm+mt
source-git-commit: d6c8bbb9aa763a2eb6660b6b6755aba75241e394

---


# DSRP 向け MySQL 設定 {#mysql-configuration-for-dsrp}

MySQL は、ユーザー生成コンテンツ（UGC）の保存に使用できるリレーショナルデータベースです。

次の手順で、MySQL サーバーに接続し、UGC データベースを設定する方法について説明します。

## 要件 {#requirements}

* [最新の Communities 機能パック](deploy-communities.md#latestfeaturepack)
* [MySQL 用 JDBC ドライバー](deploy-communities.md#jdbc-driver-for-mysql)
* リレーショナルデータベース：

   * [MySQL server](https://dev.mysql.com/downloads/mysql/) Community Serverバージョン5.6以降

      * AEMと同じホストで実行するか、リモートで実行できます。
   * [MySQL Workbench](https://dev.mysql.com/downloads/tools/workbench/)


## MySQL のインストール {#installing-mysql}

対象 OS の手順に従い、[MySQL](https://dev.mysql.com/downloads/mysql/) をダウンロードしてインストールする必要があります。

### 小文字のテーブル名 {#lower-case-table-names}

SQL では大文字と小文字が区別されます。大文字と小文字が区別されるオペレーティングシステムでは、すべてのテーブル名を小文字にする設定を含める必要があります。

例えば、Linux OS でテーブル名をすべて小文字に指定するには、

* ファイルの編集 `/etc/my.cnf`
* In the `[mysqld]` section, add the following line:

   `lower_case_table_names = 1`

### UTF8 文字セット {#utf-character-set}

より優れた多言語対応を実現するには、UTF8 文字セットを使用する必要があります。

以下の操作で MySQL の文字セットを UTF8 に変更します。

* mysql> SET NAMES &#39;utf8&#39;;

以下の操作で MySQL データベースをデフォルトから UTF8 に変更します。

* ファイルの編集 `/etc/my.cnf`
* In the `[client]` section, add the following line:

   `default-character-set=utf8`

* In the `[mysqld]` section, add the following line:

   `character-set-server=utf8`

## MySQL Workbench のインストール {#installing-mysql-workbench}

MySQL Workbench には、スキーマと初期データをインストールする SQL スクリプトを実行するための UI が用意されています。

MySQL Workbenchは、ターゲットOSの手順に従ってダウンロードし、インストールする必要があります。

## Communities の接続 {#communities-connection}

MySQL Workbench を初めて起動したときは（他の目的で既に使用されていない場合）、接続はまだ表示されません。

![chlimage_1-104](assets/chlimage_1-104.png)

### 新しい接続の設定 {#new-connection-settings}

1. Select the `+` icon to the right of `MySQL Connections`.
1. ダイアログで、プ `Setup New Connection`ラットフォームに適した値を入力します

   デモ用に、作成者のAEMインスタンスとMySQLを同じサーバー上に置きます。

   * 接続名: `Communities`
   * 接続方法： `Standard (TCP/IP)`
   * Hostname：`127.0.0.1`
   * ユーザー名: `root`
   * パスワード: `no password by default`
   * デフォルトのスキーマ： `leave blank`

1. Select `Test Connection` to verify the connection to the running MySQL service

**メモ**:

* The default port is `3306`
* The Connection Name chosen is entered as the datasource name in [JDBC OSGi configuration](#configurejdbcconnections)

#### 新しい Communities 接続 {#new-communities-connection}

![chlimage_1-105](assets/chlimage_1-105.png)

## データベースのセットアップ {#database-setup}

データベースをインストールするには、Communities 接続を開きます。

![chlimage_1-106](assets/chlimage_1-106.png)

### SQL スクリプトの取得 {#obtain-the-sql-script}

SQL スクリプトは、AEM リポジトリから取得されます。

1. CRXDE Liteを参照

   * 例：[http://localhost:4502/crx/de](http://localhost:4502/crx/de)

1. /libs/social/config/datastore/dsrp/schemaフォルダーを選択します
1. ダウンロード `init-schema.sql`

![chlimage_1-107](assets/chlimage_1-107.png)

スキーマをダウンロードする方法の1つは、

* Select the `jcr:content` node for the sql file
* Notice the value for the `jcr:data` property is a view link

* データをローカルファイルに保存するには、ビューリンクを選択します

### DSRP データベースの作成 {#create-the-dsrp-database}

次の手順に従って、データベースをインストールします。 The default name of the database is `communities`.

スクリプトでデータベース名を変更する場合は、[JDBC 設定](#configurejdbcconnections)でも変更してください。

#### 手順 1：SQL ファイルを開く {#step-open-sql-file}

MySQL Workbench で、以下の設定をおこないます。

* [ファイル]プルダウンメニューから
* ダウンロードした `init_schema.sql`

![chlimage_1-108](assets/chlimage_1-108.png)

#### 手順 2：SQL スクリプトの実行 {#step-execute-sql-script}

In the Workbench window for the file opened in Step 1, select the `lightening (flash) icon` to execute the script.

以下の画像では、`init_schema.sql` ファイルは実行可能です。

![chlimage_1-109](assets/chlimage_1-109.png)

#### 更新 {#refresh}

Once the script is executed, it is necessary to refresh the `SCHEMAS` section of the `Navigator` in order to see the new database. 以下のように、「SCHEMAS」の右側にある更新アイコンを使用します。

![chlimage_1-110](assets/chlimage_1-110.png)

## JDBC 接続の設定 {#configure-jdbc-connection}

**Day Commons JDBC Connections Pool** の OSGi 設定では、MySQL JDBC ドライバーを設定します。

すべての AEM パブリッシュインスタンスおよびオーサーインスタンスが、同じ MySQL サーバーを指している必要があります。

MySQLをAEMとは異なるサーバーで実行する場合、JDBCコネクタの「localhost」の代わりにサーバーのホスト名を指定する必要があります。

* 各作成者および発行AEMインスタンス
* 管理者権限でサインイン
* Access the [web console](../../help/sites-deploying/configuring-osgi.md)

   * For example, [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)

* を検索します。 `Day Commons JDBC Connections Pool`
* Select the `+` icon to create a new connection configuration

![chlimage_1-111](assets/chlimage_1-111.png)

* 次の値を入力します。

   * **[!UICONTROL JDBC ドライバークラス]**: `com.mysql.jdbc.Driver`
   * **[!UICONTROL JDBC 接続 URI]**: `jdbc:mysql://localhost:3306/communities?characterEncoding=UTF-8`

      MySQLサーバーが「this」AEMサーバーと同じでない場合は、localhostの代わりにサーバーを指定します。

      *communitiesは* 、デフォルトのデータベース（スキーマ）名です。

   * **[!UICONTROL ユーザー名]**: `root`

      または、MySQLサーバーの設定済みのユーザー名（「root」でない場合）を入力します。

   * **[!UICONTROL パスワード]**:

      MySQLにパスワードが設定されていない場合は、このフィールドをクリアします。

      それ以外の場合は、MySQLユーザー名用に設定されたパスワードを入力します。
   * **[!UICONTROL Datasource name]**： [MySQL connection](#new-connection-settings) に入力した名前（例：「communities」）

* Select **[!UICONTROL Save]**

