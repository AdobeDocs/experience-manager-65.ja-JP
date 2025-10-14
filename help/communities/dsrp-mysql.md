---
title: DSRP 向け MySQL 設定
description: MySQL サーバーに接続し、UGC データベースを確立する方法
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: eafb60be-2963-4ac9-8618-50fd9bc6fe6c
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 2%

---

# DSRP 向け MySQL 設定 {#mysql-configuration-for-dsrp}

MySQL は、ユーザー生成コンテンツ（UGC）の保存に使用できるリレーショナルデータベースです。

これらの手順では、MySQL サーバーに接続し、UGC データベースを確立する方法について説明します。

## 要件 {#requirements}

* [最新の Communities 機能パック](deploy-communities.md#latestfeaturepack)
* [MySQL 用 JDBC ドライバー](deploy-communities.md#jdbc-driver-for-mysql)
* リレーショナルデータベース：

   * [MySQL サーバー &#x200B;](https://dev.mysql.com/downloads/mysql/) Community Server バージョン 5.6 以降

      * AEMと同じホスト上で実行するか、リモートで実行できる

   * [MySQL ワークベンチ &#x200B;](https://dev.mysql.com/downloads/tools/workbench/)

## MySQL のインストール {#installing-mysql}

対象 OS の手順に従って、[MySQL](https://dev.mysql.com/downloads/mysql/) をダウンロードしてインストールします。

### 小文字のテーブル名 {#lower-case-table-names}

SQL では大文字と小文字が区別されないので、大文字と小文字を区別するオペレーティングシステムの場合は、すべてのテーブル名を小文字にする設定を含める必要があります。

例えば、Linux OS ですべての小文字テーブル名を指定するには、次のようにします。

* ファイル `/etc/my.cnf` を編集
* 「`[mysqld]`」セクションで、次の行を追加します。

  `lower_case_table_names = 1`

### UTF8 文字セット {#utf-character-set}

多言語サポートを向上させるには、UTF8 文字セットを使用する必要があります。

MySQL を変更し、文字セットとして UTF8 を使用します。

* mysql > SET NAMES &#39;utf8&#39;;

MySQL データベースをデフォルトの UTF8 に変更します。

* ファイル `/etc/my.cnf` を編集
* 「`[client]`」セクションで、次の行を追加します。

  `default-character-set=utf8`

* 「`[mysqld]`」セクションで、次の行を追加します。

  `character-set-server=utf8`

## MySQL Workbench のインストール {#installing-mysql-workbench}

MySQL Workbench は、スキーマと初期データをインストールする SQL スクリプトを実行するための UI を提供します。

対象 OS の手順に従って、MySQL Workbench をダウンロードしてインストールします。

## Communities 接続 {#communities-connection}

MySQL Workbench を初めて起動したときに、他の目的ですでに使用されている場合を除き、まだ接続は表示されません。

![mysqlconnection](assets/mysqlconnection.png)

### 新しい接続設定 {#new-connection-settings}

1. `MySQL Connections` の右側にある「`+`」アイコンを選択します。
1. ダイアログ `Setup New Connection` ックスで、プラットフォームに適した値を入力します

   デモンストレーション用に、同じサーバー上のオーサーAEM インスタンスと MySQL を使用します。

   * 接続名：`Communities`
   * 接続方法：`Standard (TCP/IP)`
   * ホスト名：`127.0.0.1`
   * ユーザー名：`root`
   * パスワード：`no password by default`
   * 既定のスキーマ：`leave blank`

1. 「`Test Connection`」を選択して、実行中の MySQL サービスへの接続を確認します

**注**:

* デフォルトのポートは `3306`
* 選択した接続名は、[JDBC OSGi 設定でデータソース名として入力され &#x200B;](#configurejdbcconnections) す。

#### 新しい Communities 接続 {#new-communities-connection}

![community-connection](assets/community-connection.png)

## データベース設定 {#database-setup}

Communities 接続を開いてデータベースをインストールします。

![install-database](assets/install-database.png)

### SQL スクリプトを取得 {#obtain-the-sql-script}

SQL スクリプトはAEM リポジトリから取得されます。

1. CRXDE Liteを参照

   * 例：[http://localhost:4502/crx/de](http://localhost:4502/crx/de)

1. /libs/social/config/datastore/dsrp/schema フォルダーを選択します
1. Download `init-schema.sql`

   ![database-schema-crxde](assets/database-schema-crxde.png)

スキーマをダウンロードする方法の 1 つは、次の操作です。

* SQL ファイルの `jcr:content` ノードを選択します
* `jcr:data` プロパティの値はビューリンクです

* 表示リンクを選択して、データをローカルファイルに保存します

### DSRP データベースの作成 {#create-the-dsrp-database}

次の手順に従って、データベースをインストールします。 データベースのデフォルト名は `communities` です。

スクリプト内でデータベース名が変更された場合は、必ず [JDBC 設定 &#x200B;](#configurejdbcconnections) 内でも変更してください。

#### 手順 1:SQL ファイルを開く {#step-open-sql-file}

MySQL Workbench で、次の手順を実行します

* ファイル プルダウンメニューから **[!UICONTROL SQL スクリプトを開く]** オプションを選択します
* ダウンロードした `init_schema.sql` スクリプトを選択します

![select-sql-script](assets/select-sql-script.png)

#### 手順 2:SQL スクリプトを実行 {#step-execute-sql-script}

手順 1 で開いたファイルの Workbench ウィンドウで、スクリプトを実行する `lightening (flash) icon` を選択します。

次の画像では、`init_schema.sql` ファイルを実行する準備が整っています。

![execute-sql-script](assets/execute-sql-script.png)

#### 更新 {#refresh}

スクリプトを実行したら、新しいデータベースを表示するために、スクリプトの `SCHEMAS` セクションを `Navigator` 新する必要があります。 「スキーマ」の右側にある更新アイコンを使用します。

![refresh-schema](assets/refresh-schema.png)

## JDBC 接続の設定 {#configure-jdbc-connection}

**Day Commons JDBC Connections Pool** の OSGi 設定によって、MySQL JDBC ドライバーが設定されます。

すべてのパブリッシュインスタンスとオーサーAEM インスタンスは、同じ MySQL Server を指す必要があります。

MySQL がAEMとは異なるサーバーで実行されている場合は、JDBC コネクタで「localhost」の代わりにサーバーホスト名を指定する必要があります。

* 各オーサーおよびパブリッシュ AEM インスタンスで。
* 管理者権限でサインインしました。
* [Web コンソール &#x200B;](../../help/sites-deploying/configuring-osgi.md) にアクセスします。

   * 例：[http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)

* `Day Commons JDBC Connections Pool` を見つけます。
* `+` アイコンを選択して、接続設定を作成します。

  ![configure-jdbc-connection](assets/configure-jdbc-connection.png)

* 次の値を入力します。

   * **[!UICONTROL JDBC ドライバークラス]**: `com.mysql.jdbc.Driver`
   * **[!UICONTROL JDBC 接続 URI]**:`jdbc:mysql://localhost:3306/communities?characterEncoding=UTF-8`

     MySQL サーバーが「this」と同じでない場合、AEM サーバー（communities *がデフォルトのデータベース（スキーマ* 名である場合は、localhost の代わりに server を指定します。

   * **[!UICONTROL ユーザー名]**: `root`

     または、MySQL サーバーのユーザー名を入力します（「root」でない場合）。

   * **[!UICONTROL パスワード]**:

     MySQL にパスワードが設定されていない場合は、このフィールドをクリアします。

     それ以外の場合は、MySQL ユーザー名に設定されているパスワードを入力します。

   * **[!UICONTROL データソース名]**: [MySQL 接続 &#x200B;](#new-connection-settings) に入力された名前（例：「communities」）。

* 「**[!UICONTROL 保存]**」を選択します
