---
title: イネーブルメント機能のための MySQL 設定
seo-title: MySQL Configuration for Enablement Features
description: MySQL サーバーの接続
seo-description: Connecting your MySQL server
uuid: e02d9404-de75-4fdb-896c-ea3f64f980a3
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 9222bc93-c231-4ac8-aa28-30d784a4ca3b
role: Admin
exl-id: 2d33e6ba-cd32-40d1-8983-58f636b21470
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '1084'
ht-degree: 46%

---

# イネーブルメント機能のための MySQL 設定 {#mysql-configuration-for-enablement-features}

MySQL は、イネーブルメントリソースの SCORM 追跡データおよびレポートデータに主に使用されるリレーショナルデータベースです。ビデオの一時停止/再開の追跡など、その他の機能に関する表が含まれています。

この手順では、MySQL サーバーに接続する方法、イネーブルメントデータベースを構築する方法およびデータベースに初期データを入力する方法について説明します。

## 要件 {#requirements}

MySQL をコミュニティサイトのイネーブルメント機能用に設定する前に、以下をおこなう必要があります。

* インストール [MySQL サーバー](https://dev.mysql.com/downloads/mysql/) Community Server バージョン 5.6:
   * バージョン 5.7 は、SCORM ではサポートされていません。
   * オーサーAEMインスタンスと同じサーバーになる場合があります。
* すべてのAEMインスタンスで、公式の [MySQL 用 JDBC ドライバー](deploy-communities.md#jdbc-driver-for-mysql).
* インストール [MySQL workbench](https://dev.mysql.com/downloads/tools/workbench/).
* すべてのAEMインスタンスで、 [SCORM パッケージ](enablement.md#scorm).

## MySQL のインストール {#installing-mysql}

対象 OS の手順に従い、MySQL をダウンロードしてインストールする必要があります。

### 小文字のテーブル名 {#lower-case-table-names}

SQL では大文字と小文字が区別されます。大文字と小文字が区別されるオペレーティングシステムでは、すべてのテーブル名を小文字にする設定を含める必要があります。

例えば、Linux OS でテーブル名をすべて小文字に指定するには、

* ファイルを編集 `/etc/my.cnf`
* 内 `[mysqld]` セクションで、次の行を追加します。 `lower_case_table_names = 1`

### UTF8 文字セット {#utf-character-set}

より優れた多言語対応を実現するには、UTF8 文字セットを使用する必要があります。

以下の操作で MySQL の文字セットを UTF8 に変更します。
* mysql> SET NAMES &#39;utf8&#39;;

以下の操作で MySQL データベースをデフォルトから UTF8 に変更します。
* ファイルを編集 `/etc/my.cnf`
* 内 `[client]` セクションに次を追加します。 `default-character-set=utf8`
* 内 `[mysqld]` セクションに次を追加します。 `character-set-server=utf8`

## MySQL Workbench のインストール {#installing-mysql-workbench}

MySQL Workbench には、スキーマと初期データをインストールする SQL スクリプトを実行するための UI が用意されています。

ターゲット OS の手順に従って、MySQL Workbench をダウンロードし、インストールする必要があります。

## イネーブルメント機能のための接続 {#enablement-connection}

MySQL Workbench を初めて起動したときは（他の目的で既に使用されていない場合）、接続はまだ表示されません。

![mysqlconnection](assets/mysqlconnection.png)

### 新しい接続の設定 {#new-connection-settings}

1. の右にある「+」アイコンを選択します。 `MySQL Connections`.
1. ダイアログ内 `Setup New Connection`を使用する場合は、プラットフォームのデモ用に適切な値を入力します。オーサーAEMインスタンスと MySQL を同じサーバー上に置きます。
   * 接続名: `Enablement`
   * 接続方法： `Standard (TCP/IP)`
   * Hostname：`127.0.0.1`
   * ユーザー名: `root`
   * パスワード: `no password by default`
   * デフォルトのスキーマ： `leave blank`
1. 選択 `Test Connection` をクリックして、実行中の MySQL サービスへの接続を検証します。

**備考**:
* デフォルトのポートは `3306` です。
* この `Connection Name` 次の項目を選択しました： `datasource` 名前を入力 [JDBC OSGi 設定](#configure-jdbc-connections).

#### 成功した接続 {#successful-connection}

![mysqlconnection1](assets/mysqlconnection1.png)

#### 新しい接続 Enablement  {#new-enablement-connection}

![mysqlconnection2](assets/mysqlconnection2.png)

## データベースのセットアップ {#database-setup}

新しい接続 Enablement を開くと、テストスキーマとデフォルトのユーザーアカウントがあります。

![database-setup](assets/database-setup.png)

### SQL スクリプトの取得 {#obtain-sql-scripts}

SQL スクリプトを取得するには、オーサーインスタンスで CRXDE Lite を使用します。この [SCORM パッケージ](deploy-communities.md#scorm) をインストールする必要があります。

1. 参照先CRXDE Lite:
   * 例：[http://localhost:4502/crx/de](http://localhost:4502/crx/de)
1. を展開します。 `/libs/social/config/scorm/` フォルダー
1. ダウンロード `database_scormengine.sql`
1. ダウンロード `database_scorm_integration.sql`

![sqlscripts](assets/sqlscripts.png)

スキーマをダウンロードする方法の 1 つは次のとおりです。

* を選択します。 `jcr:content` sql ファイルのノード。
* の値 `jcr:data` プロパティはビューリンクです。
* データをローカルファイルに保存するには、表示リンクを選択します。

### SCORM データベースの作成 {#create-scorm-database}

作成するイネーブルメント SCORM データベースは次のとおりです。

* name: `ScormEngineDB`
* 以下のスクリプトから作成：
   * リストとして: `database_scormengine.sql`
   * データ： `database_scorm_integration.sql`
以下の手順に従います (
[open](#step-open-sql-file), [execute](#step-execute-sql-script)) をインストールします。 [SQL スクリプト](#obtain-sql-scripts) . [更新](#refresh) 必要に応じて、スクリプトの実行結果を確認します。

データをインストールする前にスキーマをインストールしてください。

>[!CAUTION]
>
>データベース名を変更した場合は、以下の設定で適切な名前を指定してください。：
>
>* [JDBC 設定](#configure-jdbc-connections)
>* [SCORM 設定](#configure-scorm)


#### Step 1 : open SQL file {#step-open-sql-file}

MySQL Workbench で、以下の設定をおこないます。

* [ ファイル ] プルダウンメニューから
* 選択 `Open SQL Script ...`
* この順序で、次のいずれかを選択します。
   1. `database_scormengine.sql`
   1. `database_scorm_integration.sql`

![scrom データベース](assets/scrom-database.png)

#### Step 2 : execute SQL Script {#step-execute-sql-script}

手順 1 で開いたファイルの Workbench ウィンドウで、 `lightening (flash) icon` スクリプトを実行します。

`database_scormengine.sql` スクリプトを実行して SCORM データベースを作成するときは、完了までに少し時間がかかる場合があります。

![scrom-database1](assets/scrom-database1.png)

#### 更新 {#refresh}

スクリプトの実行が完了したら、新しいデータベースを表示するために、`SCHEMAS` の `Navigator` セクションを更新する必要があります。以下のように、「SCHEMAS」の右側にある更新アイコンを使用します。

![scrom-database2](assets/scrom-database2.png)

#### 結果：scormenginedb {#result-scormenginedb}

SCHEMAS のインストールと更新が完了すると、`scormenginedb` が表示されます。

![scrom-database3](assets/scrom-database3.png)

## JDBC 接続の設定 {#configure-jdbc-connections}

**Day Commons JDBC Connections Pool** の OSGi 設定では、MySQL JDBC ドライバーを設定します。

すべての AEM パブリッシュインスタンスおよびオーサーインスタンスが、同じ MySQL サーバーを指している必要があります。

MySQL をAEMとは異なるサーバーで実行する場合は、JDBC コネクタの「localhost」の代わりにサーバーホスト名を指定する必要があります ( これにより、 [ScormEngine](#configurescormengineservice) 設定 ) を参照してください。

* 各オーサーおよびパブリッシュAEMインスタンスで
* 管理者権限でサインインしています
* 次にアクセス： [web コンソール](../../help/sites-deploying/configuring-osgi.md)
   * 例： [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)
* を `Day Commons JDBC Connections Pool`
* を選択します。 `+` 新しい設定を作成するアイコン

   ![jdbcconnection1](assets/jdbcconnection1.png)

* 次の値を入力します。
   * **[!UICONTROL JDBC ドライバークラス]**: `com.mysql.jdbc.Driver`
   * **DBC 接続 URIJ**: `jdbc:mysql://localhost:3306/aem63reporting` MySQL サーバーが「this」AEMサーバーと同じでない場合は、localhost の代わりにサーバーを指定します。
   * **[!UICONTROL ユーザー名]**:Root を指定するか、MySQL サーバーに設定されているユーザー名（「root」でない場合）を入力します。
   * **[!UICONTROL パスワード]**:MySQL のパスワードが設定されていない場合は、このフィールドをクリアします。設定されていない場合は、MySQL ユーザー名用に設定されたパスワードを入力します。
   * **[!UICONTROL データソース名]**:次に対して入力した名前： [MySQL 接続](#new-connection-settings)例： &#39;enablement&#39;
* 「**[!UICONTROL 保存]**」を選択します。

## SCORM の設定 {#configure-scorm}

### AEM Communities ScormEngine Service {#aem-communities-scormengine-service}

**AEM Communities ScormEngine Service** の OSGi 設定では、イネーブルメントコミュニティで MySQL サーバーを使用するために SCORM を設定します。

[SCORM パッケージ](deploy-communities.md#scorm-package)がインストールされているときは、設定が表示されます。

すべてのパブリッシュインスタンスおよびオーサーインスタンスが、同じ MySQL サーバーを指している必要があります。

MySQL をAEMとは異なるサーバーで実行する場合は、ScormEngine サービスの「localhost」の代わりにサーバーホスト名を指定する必要があります。このホスト名は通常、 [JDBC 接続](#configure-jdbc-connections) config.

* 各オーサーおよびパブリッシュAEMインスタンスで
* 管理者権限でサインインしています
* 次にアクセス： [web コンソール](../../help/sites-deploying/configuring-osgi.md)
   * 例： [http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)
* を `AEM Communities ScormEngine Service`
* 編集アイコンを選択します。

   ![scrom エンジン](assets/scrom-engine.png)

* 次のパラメータ値が [JDBC 接続](#configurejdbcconnectionspool) config:
   * **[!UICONTROL JDBC 接続 URI]**: `jdbc:mysql://localhost:3306/ScormEngineDB` *ScormEngineDB* は、SQL スクリプトのデフォルトのデータベース名です
   * **[!UICONTROL ユーザー名]**:Root にするか、MySQL サーバー用に設定されたユーザー名を入力します（「root」でない場合）。
   * **[!UICONTROL パスワード]**:MySQL のパスワードが設定されていない場合はこのフィールドをクリアし、設定されていない場合は MySQL ユーザー名用に設定されたパスワードを入力します
* 次のパラメーターに関して：
   * **[!UICONTROL Scorm ユーザーパスワード]**:編集しない

      内部でのみ使用します。AEM Communitiesが SCORM エンジンと通信する際に使用する特別なサービスユーザー用です。
* 選択 **[!UICONTROL 保存]**

### Adobe Granite CSRF Filter {#adobe-granite-csrf-filter}

イネーブルメントコースがすべてのブラウザーで正しく動作するかを確認するには、Mozilla を CSRF フィルターでは確認されないユーザーエージェントとして追加する必要があります。

* 管理者権限でAEMパブリッシュインスタンスにログインします。
* 次にアクセス： [web コンソール](../../help/sites-deploying/configuring-osgi.md)
   * 例： [http://localhost:4503/system/console/configMgr](http://localhost:4503/system/console/configMgr)
* 場所 `Adobe Granite CSRF Filter`.
* 編集アイコンを選択します。

   ![jdbcconnection2](assets/jdbcconnection2.png)

* を選択します。 `[+]` アイコンをクリックして Safe User Agent を追加します。
* Enter `Mozilla/*`.
* 「**[!UICONTROL 保存]**」を選択します。
