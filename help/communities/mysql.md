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
translation-type: tm+mt
source-git-commit: 871c42ee000eb250c1c6159d9a0c752e8ed4d7b8
workflow-type: tm+mt
source-wordcount: '1093'
ht-degree: 47%

---


# イネーブルメント機能のための MySQL 設定 {#mysql-configuration-for-enablement-features}

MySQL は、イネーブルメントリソースの SCORM 追跡データおよびレポートデータに主に使用されるリレーショナルデータベースです。ビデオの一時停止/再開の追跡など、その他の機能の表が含まれています。

この手順では、MySQL サーバーに接続する方法、イネーブルメントデータベースを構築する方法およびデータベースに初期データを入力する方法について説明します。

## 要件 {#requirements}

MySQL をコミュニティサイトのイネーブルメント機能用に設定する前に、以下をおこなう必要があります。

* [MySQL server](https://dev.mysql.com/downloads/mysql/) Community Serverバージョン5.6をインストールします。
   * バージョン5.7はSCORMではサポートされていません。
   * 作成者のAEMインスタンスと同じサーバーを使用できます。
* すべてのAEMインスタンスで、MySQL用の正式な[JDBCドライバー](deploy-communities.md#jdbc-driver-for-mysql)をインストールします。
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
* `[client]`セクションに次を追加します。`default-character-set=utf8`
* `[mysqld]`セクションに次を追加します。`character-set-server=utf8`

## MySQL Workbench のインストール {#installing-mysql-workbench}

MySQL Workbench には、スキーマと初期データをインストールする SQL スクリプトを実行するための UI が用意されています。

MySQL Workbenchは、ターゲットOSの指示に従ってダウンロードし、インストールする必要があります。

## イネーブルメント機能のための接続 {#enablement-connection}

MySQL Workbench を初めて起動したときは（他の目的で既に使用されていない場合）、接続はまだ表示されません。

![mysqlconnection](assets/mysqlconnection.png)

### 新しい接続の設定 {#new-connection-settings}

1. `MySQL Connections`の右にある「+」アイコンを選択します。
1. ダイアログ`Setup New Connection`に、作成者のAEMインスタンスとMySQLを同じサーバー上に置き、デモ用にプラットフォームに適した値を入力します。
   * 接続名: `Enablement`
   * 接続方法：`Standard (TCP/IP)`
   * Hostname：`127.0.0.1`
   * ユーザー名: `root`
   * パスワード: `no password by default`
   * デフォルトスキーマ:`leave blank`
1. `Test Connection`を選択して、実行中のMySQLサービスへの接続を確認します。

**備考**:
* デフォルトのポートは `3306` です。
* 選択された`Connection Name`は、[JDBC OSGi設定](#configure-jdbc-connections)の`datasource`名として入力されます。

#### 成功した接続 {#successful-connection}

![mysqlconnection1](assets/mysqlconnection1.png)

#### 新しい接続 Enablement {#new-enablement-connection}

![mysqlconnection2](assets/mysqlconnection2.png)

## データベースのセットアップ {#database-setup}

新しい接続 Enablement を開くと、テストスキーマとデフォルトのユーザーアカウントがあります。

![database-setup](assets/database-setup.png)

### SQL スクリプトの取得 {#obtain-sql-scripts}

SQL スクリプトを取得するには、オーサーインスタンスで CRXDE Lite を使用します。[SCORMパッケージ](deploy-communities.md#scorm)をインストールする必要があります。

1. CRXDE Liteを参照：
   * 例：[http://localhost:4502/crx/de](http://localhost:4502/crx/de)
1. `/libs/social/config/scorm/`フォルダーを展開します
1. ダウンロード `database_scormengine.sql`
1. ダウンロード `database_scorm_integration.sql`

![sqlscripts](assets/sqlscripts.png)

スキーマをダウンロードする方法の1つは、次のことです。

* SQLファイルの`jcr:content`ノードを選択します。
* `jcr:data`プロパティの値は表示リンクです。
* 表示リンクを選択して、データをローカルファイルに保存します。

### SCORM データベースの作成 {#create-scorm-database}

作成する有効化SCORMデータベースは次のとおりです。

* name: `ScormEngineDB`
* 以下のスクリプトから作成：
   * リストとして: `database_scormengine.sql`
   * data:`database_scorm_integration.sql`
次の手順に従います(
[各](#step-open-sql-file)SQLスクリプトをインストールするには、 [[開く]、[](#step-execute-sql-script)execute [](#obtain-sql-scripts) ])。[必要に応じて](#refresh) 更新し、スクリプトの実行結果を確認します。

データをインストールする前にスキーマをインストールしてください。

>[!CAUTION]
>
>データベース名を変更した場合は、以下の設定で適切な名前を指定してください。：
>
>* [JDBC 設定](#configure-jdbc-connections)
>* [SCORM 設定](#configure-scorm)


#### 手順 1：SQL ファイルを開く {#step-open-sql-file}

MySQL Workbench で、以下の設定をおこないます。

* [ファイル]プルダウンメニューから
*  `Open SQL Script ...`
* この順序で、次のいずれかを選択します。
   1. `database_scormengine.sql`
   1. `database_scorm_integration.sql`

![scrom-database](assets/scrom-database.png)

#### 手順 2：SQL スクリプトの実行 {#step-execute-sql-script}

手順1で開いたファイルのWorkbenchウィンドウで、`lightening (flash) icon`を選択してスクリプトを実行します。

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

MySQLがAEMとは異なるサーバーで実行される場合、JDBCコネクタの「localhost」の代わりにサーバーのホスト名を指定する必要があります（これにより[ScormEngine](#configurescormengineservice)の設定が入力されます）。

* 各作成者および発行AEMインスタンス
* 管理者権限を持つサインイン
* [Webコンソール](../../help/sites-deploying/configuring-osgi.md)にアクセス
   * 例：[http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)
* `Day Commons JDBC Connections Pool`
* `+`アイコンを選択して、新しい構成を作成します

   ![jdbcconnection1](assets/jdbcconnection1.png)

* 次の値を入力します。
   * **[!UICONTROL JDBC ドライバークラス]**: `com.mysql.jdbc.Driver`
   * **DBC接続URIJ**: `jdbc:mysql://localhost:3306/aem63reporting` MySQLサーバーが&#39;this&#39; AEMサーバーと同じでない場合は、localhostの代わりにserverを指定します。
   * **[!UICONTROL ユーザー名]**:「root」でない場合は、MySQLサーバーの設定済みユーザー名をrootにするか、入力します。
   * **[!UICONTROL パスワード]**:MySQLにパスワードが設定されていない場合は、このフィールドをクリアします。それ以外の場合は、MySQLユーザー名に設定済みのパスワードを入力します。
   * **[!UICONTROL データソース名]**:MySQL接続に対して入力された名前 [](#new-connection-settings)（例： &#39;enablement&#39;）。
* 「**[!UICONTROL 保存]**」を選択します。

## SCORM の設定 {#configure-scorm}

### AEM Communities ScormEngine Service {#aem-communities-scormengine-service}

**AEM Communities ScormEngine Service** の OSGi 設定では、イネーブルメントコミュニティで MySQL サーバーを使用するために SCORM を設定します。

[SCORM パッケージ](deploy-communities.md#scorm-package)がインストールされているときは、設定が表示されます。

すべてのパブリッシュインスタンスおよびオーサーインスタンスが、同じ MySQL サーバーを指している必要があります。

MySQLがAEMとは異なるサーバーで実行される場合、ScormEngineサービスでは「localhost」の代わりにサーバーホスト名を指定する必要があります。通常は、[JDBC接続](#configure-jdbc-connections)の設定から設定されます。

* 各作成者および発行AEMインスタンス
* 管理者権限を持つサインイン
* [Webコンソール](../../help/sites-deploying/configuring-osgi.md)にアクセス
   * 例：[http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)
* `AEM Communities ScormEngine Service`
* 編集アイコンを選択します

   ![scromエンジン](assets/scrom-engine.png)

* 次のパラメーター値が[JDBC Connection](#configurejdbcconnectionspool)設定と一致していることを確認します。
   * **[!UICONTROL JDBC接続URI]**: `jdbc:mysql://localhost:3306/ScormEngineDB` *ScormEngineDBは、SQLスクリプ* トのデフォルトのデータベース名です
   * **[!UICONTROL ユーザー名]**:「root」でない場合は、MySQLサーバーの設定済みのユーザー名をルートにするか、入力します。
   * **[!UICONTROL パスワード]**:MySQLにパスワードが設定されていない場合は、このフィールドをクリアします。それ以外の場合は、MySQLユーザー名に設定済みのパスワードを入力します
* 次のパラメーターに関して：
   * **[!UICONTROL Scormユーザーパスワード]**:編集しない

      内部でのみ使用する場合：AEM CommunitiesがSCORMエンジンと通信するのに使う特別なサービス利用者のためです。
* **[!UICONTROL 保存]**&#x200B;を選択

### Adobe Granite CSRF Filter {#adobe-granite-csrf-filter}

イネーブルメントコースがすべてのブラウザーで正しく動作するかを確認するには、Mozilla を CSRF フィルターでは確認されないユーザーエージェントとして追加する必要があります。

* 管理者権限でAEM発行インスタンスにログインします。
* [Webコンソール](../../help/sites-deploying/configuring-osgi.md)にアクセス
   * 例：[http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)
* `Adobe Granite CSRF Filter`を探します。
* 編集アイコンを選択します。

   ![jdbconnection2](assets/jdbcconnection2.png)

* `[+]`アイコンを選択して、セーフユーザーエージェントを追加します。
* Enter `Mozilla/*`.
* 「**[!UICONTROL 保存]**」を選択します。

