---
title: イネーブルメント機能のための MySQL 設定
seo-title: イネーブルメント機能のための MySQL 設定
description: MySQL サーバーの接続
seo-description: MySQL サーバーの接続
uuid: e02d9404-de75-4fdb-896c-ea3f64f980a3
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 9222bc93-c231-4ac8-aa28-30d784a4ca3b
role: Administrator
exl-id: 2d33e6ba-cd32-40d1-8983-58f636b21470
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1093'
ht-degree: 47%

---

# イネーブルメント機能のための MySQL 設定 {#mysql-configuration-for-enablement-features}

MySQL は、イネーブルメントリソースの SCORM 追跡データおよびレポートデータに主に使用されるリレーショナルデータベースです。ビデオの一時停止/再開の追跡など、その他の機能に関する表が含まれています。

この手順では、MySQL サーバーに接続する方法、イネーブルメントデータベースを構築する方法およびデータベースに初期データを入力する方法について説明します。

## 要件 {#requirements}

MySQL をコミュニティサイトのイネーブルメント機能用に設定する前に、以下をおこなう必要があります。

* [MySQL server](https://dev.mysql.com/downloads/mysql/) Community Server version 5.6をインストールします。
   * バージョン5.7はSCORMではサポートされていません。
   * オーサーのAEMインスタンスと同じサーバーになる場合があります。
* すべてのAEMインスタンスに、MySQL用の[JDBCドライバー](deploy-communities.md#jdbc-driver-for-mysql)を正式にインストールします。
* [MySQL workbench](https://dev.mysql.com/downloads/tools/workbench/)をインストールします。
* すべてのAEMインスタンスに、[SCORMパッケージ](enablement.md#scorm)をインストールします。

## MySQL のインストール {#installing-mysql}

対象 OS の手順に従い、MySQL をダウンロードしてインストールする必要があります。

### 小文字のテーブル名  {#lower-case-table-names}

SQL では大文字と小文字が区別されます。大文字と小文字が区別されるオペレーティングシステムでは、すべてのテーブル名を小文字にする設定を含める必要があります。

例えば、Linux OS でテーブル名をすべて小文字に指定するには、

* ファイル`/etc/my.cnf`を編集
* `[mysqld]`セクションに次の行を追加します。`lower_case_table_names = 1`

### UTF8 文字セット {#utf-character-set}

より優れた多言語対応を実現するには、UTF8 文字セットを使用する必要があります。

以下の操作で MySQL の文字セットを UTF8 に変更します。
* mysql> SET NAMES &#39;utf8&#39;;

以下の操作で MySQL データベースをデフォルトから UTF8 に変更します。
* ファイル`/etc/my.cnf`を編集
* `[client]`セクションで、次を追加します。`default-character-set=utf8`
* `[mysqld]`セクションで、次を追加します。`character-set-server=utf8`

## MySQL Workbench のインストール {#installing-mysql-workbench}

MySQL Workbench には、スキーマと初期データをインストールする SQL スクリプトを実行するための UI が用意されています。

ターゲットOSの手順に従って、MySQL Workbenchをダウンロードし、インストールする必要があります。

## イネーブルメント機能のための接続 {#enablement-connection}

MySQL Workbench を初めて起動したときは（他の目的で既に使用されていない場合）、接続はまだ表示されません。

![mysqlconnection](assets/mysqlconnection.png)

### 新しい接続の設定 {#new-connection-settings}

1. `MySQL Connections`の右側にある「+」アイコンを選択します。
1. ダイアログ`Setup New Connection`で、オーサーAEMインスタンスとMySQLを同じサーバー上に置き、デモ用にプラットフォームに適した値を入力します。
   * 接続名: `Enablement`
   * 接続方法：`Standard (TCP/IP)`
   * Hostname：`127.0.0.1`
   * ユーザー名: `root`
   * パスワード: `no password by default`
   * デフォルトのスキーマ：`leave blank`
1. `Test Connection`を選択して、実行中のMySQLサービスへの接続を確認します。

**備考**:
* デフォルトのポートは `3306` です。
* 選択した`Connection Name`は、[JDBC OSGi設定](#configure-jdbc-connections)に`datasource`名として入力されます。

#### 成功した接続 {#successful-connection}

![mysqlconnection1](assets/mysqlconnection1.png)

#### 新しい接続 Enablement {#new-enablement-connection}

![mysqlconnection2](assets/mysqlconnection2.png)

## データベースのセットアップ {#database-setup}

新しい接続 Enablement を開くと、テストスキーマとデフォルトのユーザーアカウントがあります。

![database-setup](assets/database-setup.png)

### SQL スクリプトの取得 {#obtain-sql-scripts}

SQL スクリプトを取得するには、オーサーインスタンスで CRXDE Lite を使用します。[SCORMパッケージ](deploy-communities.md#scorm)をインストールする必要があります。

1. CRXDE Liteの参照：
   * 例：[http://localhost:4502/crx/de](http://localhost:4502/crx/de)
1. `/libs/social/config/scorm/`フォルダーを展開します。
1. ダウンロード `database_scormengine.sql`
1. ダウンロード `database_scorm_integration.sql`

![sqlscripts](assets/sqlscripts.png)

スキーマをダウンロードする方法の1つは次のとおりです。

* sqlファイルの`jcr:content`ノードを選択します。
* `jcr:data`プロパティの値はビューリンクです。
* 表示リンクを選択して、データをローカルファイルに保存します。

### SCORM データベースの作成 {#create-scorm-database}

作成するイネーブルメントSCORMデータベースは次のとおりです。

* name: `ScormEngineDB`
* 以下のスクリプトから作成：
   * リストとして: `database_scormengine.sql`
   * データ：`database_scorm_integration.sql`
次の手順に従います(
[](#step-open-sql-file)を開き、 [execute](#step-execute-sql-script)を実行)、各SQLスクリプトをインス [トールします](#obtain-sql-scripts) 。[](#refresh) 必要に応じて更新し、スクリプト実行の結果を確認します。

データをインストールする前にスキーマをインストールしてください。

>[!CAUTION]
>
>データベース名を変更した場合は、以下の設定で適切な名前を指定してください。：
>
>* [JDBC 設定](#configure-jdbc-connections)
* [SCORM 設定](#configure-scorm)


#### 手順 1：SQL ファイルを開く {#step-open-sql-file}

MySQL Workbench で、以下の設定をおこないます。

* [ファイル]プルダウンメニューから
*  `Open SQL Script ...`
* この順序で、次のいずれかを選択します。
   1. `database_scormengine.sql`
   1. `database_scorm_integration.sql`

![scromデータベース](assets/scrom-database.png)

#### 手順 2：SQL スクリプトの実行 {#step-execute-sql-script}

手順1で開いたファイルのWorkbenchウィンドウで、スクリプトを実行する`lightening (flash) icon`を選択します。

`database_scormengine.sql` スクリプトを実行して SCORM データベースを作成するときは、完了までに少し時間がかかる場合があります。

![scrom-database1](assets/scrom-database1.png)

#### 更新 {#refresh}

スクリプトの実行が完了したら、新しいデータベースを表示するために、`SCHEMAS` の `Navigator` セクションを更新する必要があります。以下のように、「SCHEMAS」の右側にある更新アイコンを使用します。

![scrom-database2](assets/scrom-database2.png)

#### 結果：scormenginedb {#result-scormenginedb}

SCHEMAS のインストールと更新が完了すると、`scormenginedb` が表示されます。

![scrom-database3](assets/scrom-database3.png)

## Configure JDBC Connections {#configure-jdbc-connections}

**Day Commons JDBC Connections Pool** の OSGi 設定では、MySQL JDBC ドライバーを設定します。

すべての AEM パブリッシュインスタンスおよびオーサーインスタンスが、同じ MySQL サーバーを指している必要があります。

MySQLをAEMとは別のサーバーで実行する場合は、JDBCコネクタの「localhost」の代わりにサーバーホスト名を指定する必要があります（[ScormEngine](#configurescormengineservice)設定を入力します）。

* 各オーサーインスタンスとパブリッシュAEMインスタンスで
* 管理者権限でサインインしています
* [Webコンソール](../../help/sites-deploying/configuring-osgi.md)にアクセスします。
   * 例： [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)
* `Day Commons JDBC Connections Pool`
* `+`アイコンを選択して、新しい設定を作成します。

   ![jdbcconnection1](assets/jdbcconnection1.png)

* 次の値を入力します。
   * **[!UICONTROL JDBC ドライバークラス]**: `com.mysql.jdbc.Driver`
   * **DBC接続URIJ**: `jdbc:mysql://localhost:3306/aem63reporting` MySQLサーバーが「this」 AEMサーバーと同じでない場合は、localhostの代わりにserverを指定します。
   * **[!UICONTROL ユーザー名]**:rootを指定するか、MySQLサーバーの設定済みのユーザー名（「root」でない場合）を入力します。
   * **[!UICONTROL パスワード]**:MySQL用にパスワードが設定されていない場合は、このフィールドをクリアします。設定されていない場合は、MySQLユーザー名用に設定したパスワードを入力します。
   * **[!UICONTROL データソース名]**:MySQL接続用に [入力した名前](#new-connection-settings)（例：「enablement」）。
* 「**[!UICONTROL 保存]**」を選択します。

## SCORM の設定 {#configure-scorm}

### AEM Communities ScormEngine Service {#aem-communities-scormengine-service}

**AEM Communities ScormEngine Service** の OSGi 設定では、イネーブルメントコミュニティで MySQL サーバーを使用するために SCORM を設定します。

[SCORM パッケージ](deploy-communities.md#scorm-package)がインストールされているときは、設定が表示されます。

すべてのパブリッシュインスタンスおよびオーサーインスタンスが、同じ MySQL サーバーを指している必要があります。

MySQLをAEMとは異なるサーバーで実行する場合は、ScormEngineサービスの「localhost」の代わりにサーバーホスト名を指定する必要があります。通常は、[JDBC接続](#configure-jdbc-connections)設定から設定します。

* 各オーサーインスタンスとパブリッシュAEMインスタンスで
* 管理者権限でサインインしています
* [Webコンソール](../../help/sites-deploying/configuring-osgi.md)にアクセスします。
   * 例： [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)
* `AEM Communities ScormEngine Service`
* 編集アイコンを選択します。

   ![scromエンジン](assets/scrom-engine.png)

* 次のパラメーター値が[JDBC接続](#configurejdbcconnectionspool)設定と一致していることを確認します。
   * **[!UICONTROL JDBC接続URI]**: `jdbc:mysql://localhost:3306/ScormEngineDB` ** ScormEngineDBは、SQLスクリプトのデフォルトのデータベース名です
   * **[!UICONTROL ユーザー名]**:rootにするか、MySQLサーバーの設定済みのユーザー名（「root」でない場合）を入力します。
   * **[!UICONTROL パスワード]**:MySQL用にパスワードが設定されていない場合は、このフィールドをクリアします。設定されていない場合は、MySQLユーザー名用に設定されたパスワードを入力します。
* 次のパラメーターについて：
   * **[!UICONTROL SCORMユーザーパスワード]**:編集しない

      内部でのみ使用：AEM CommunitiesがSCORMエンジンと通信する特別なサービスユーザー用です。
* 「**[!UICONTROL 保存]**」を選択します。

### Adobe Granite CSRF Filter {#adobe-granite-csrf-filter}

イネーブルメントコースがすべてのブラウザーで正しく動作するかを確認するには、Mozilla を CSRF フィルターでは確認されないユーザーエージェントとして追加する必要があります。

* 管理者権限でAEMパブリッシュインスタンスにログインします。
* [Webコンソール](../../help/sites-deploying/configuring-osgi.md)にアクセスします。
   * 例： [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)
* `Adobe Granite CSRF Filter`を探します。
* 編集アイコンを選択します。

   ![jdbcconnection2](assets/jdbcconnection2.png)

* `[+]`アイコンを選択して、安全なユーザーエージェントを追加します。
* Enter `Mozilla/*`.
* 「**[!UICONTROL 保存]**」を選択します。
