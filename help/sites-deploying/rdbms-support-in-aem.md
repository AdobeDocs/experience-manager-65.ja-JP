---
title: AEM 6.4 の RDBMS サポート
seo-title: AEM 6.4 の RDBMS サポート
description: AEM 6.4 でのリレーショナルデータベース永続性のサポートおよび使用可能な設定オプションについて説明します。
seo-description: AEM 6.4 でのリレーショナルデータベース永続性のサポートおよび使用可能な設定オプションについて説明します。
uuid: c8422b0d-c6df-488d-bb6a-af92c9afda50
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 6a754d42-da30-4c2f-8b9c-369e1f1f92b5
docset: aem65
translation-type: tm+mt
source-git-commit: 38ef8fc8d80009c8ca79aca9e45cf10bd70e1f1e
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 78%

---


# AEM 6.4 の RDBMS サポート{#rdbms-support-in-aem}

## 概要 {#overview}

AEM でのリレーショナルデータベース永続性のサポートは、Document Microkernel を使用して実装されています。Document Microkernel は、MongoDB 永続性の実装にも使用されている基盤です。

このサポートは、Mongo Java API に基づいた Java API により構成されています。BlobStore API の実装も提供されています。デフォルトで、Blob はデータベース内に保存されます。

実装詳細について詳しくは、[RDBDocumentStore](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/oak/plugins/document/rdb/RDBDocumentStore.html) および [RDBBlobStore](https://jackrabbit.apache.org/oak/docs/apidocs/org/apache/jackrabbit/oak/plugins/document/rdb/RDBBlobStore.html) のドキュメントを参照してください。

>[!NOTE]
>
>**PostgreSQL 9.4** もサポートされていますが、デモ目的に限られます。本番環境では使用できません。

## サポートされているデータベース {#supported-databases}

AEM でのリレーショナルデータベースのサポートレベルについて詳しくは、[技術要件のページ](/help/sites-deploying/technical-requirements.md)を参照してください。

## 設定手順 {#configuration-steps}

リポジトリは、`DocumentNodeStoreService` OSGi サービスを設定することで作成されます。このサービスは、MongoDB に加えてリレーショナルデータベース永続性もサポートするように拡張されています。

このサービスが動作するためには、AEM でデータソースを設定する必要があります。This is done via the `org.apache.sling.datasource.DataSourceFactory.config` file. ローカル設定内の OSGi バンドルとは別に、対応するデータベースの JDBC ドライバを指定する必要があります。

JDBC ドライバ用の OSGi バンドルの作成手順については、Apache Sling Web サイトの[こちらのドキュメント](https://sling.apache.org/documentation/bundles/datasource-providers.html#convert-driver-jars-to-bundle)を参照してください。

バンドルを配置したら、AEM に RDB 永続性を設定するための次の手順に従ってください。

1. データベースのデーモンが起動しており、AEM で使用するためのアクティブなデータベースがあることを確認します。
1. AEM 6.3 jar をインストールディレクトリにコピーします。
1. Create a folder called `crx-quickstart\install` in the installation directory.
1. ドキュメントノードストアを設定するために、この `crx-quickstart\install` ディレクトリ内に、次の名前の設定ファイルを作成します。

   * `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`

1. データソースと JDBC パラメーターを設定するために、この `crx-quickstart\install` フォルダー内に、また別の次の名前の設定ファイルを作成します。

   * `org.apache.sling.datasource.DataSourceFactory-oak.config`
   >[!NOTE]
   >
   >サポートされているそれぞれのデータベースに関するデータソース設定について詳しくは、[データソース設定オプション](/help/sites-deploying/rdbms-support-in-aem.md#data-source-configuration-options)を参照してください。

1. 次に、AEM で使用する JDBC OSGi バンドルを準備します。

   1. In the `crx-quickstart/install` folder, create a folder named `9`.

   1. この新しいフォルダー内に JDBC jar を配置します。

1. Finally, start AEM with the `crx3` and `crx3rdb` runmodes:

   ```java
   java -jar quickstart.jar -r crx3,crx3rdb
   ```

## データソース設定オプション {#data-source-configuration-options}

AEM とデータベース永続性レイヤー間の通信のために必要になるパラメーターの設定には、`org.apache.sling.datasource.DataSourceFactory-oak.config` OSGi 設定を使用します。

以下の設定オプションを使用できます。

* `datasource.name:`データソース名。デフォルトは、`oak` です。

* `url:` JDBCで使用する必要があるデータベースのURL文字列。 データベースタイプごとに独自の URL 文字列の形式が設定されています。詳しくは、後述の [URL 文字列の形式](/help/sites-deploying/rdbms-support-in-aem.md#url-string-formats)を参照してください。

* `driverClassName:` JDBCドライバーのクラス名。 これは、使用するデータベースと、その後接続に必要なドライバによって異なります。 AEMがサポートするすべてのデータベースのクラス名を次に示します。

   * `org.postgresql.Driver` PostgreSQLの場合；
   * `com.ibm.db2.jcc.DB2Driver` for DB2;
   * `oracle.jdbc.OracleDriver` Oracleの場合
   * `com.mysql.jdbc.Driver`（MySQL および MariaDB、試行用）
   * c `om.microsoft.sqlserver.jdbc.SQLServerDriver` for Microsoft SQL Server (experimental).

* `username:` データベースが実行されるユーザー名。

* `password:` データベースのパスワード。

### URL 文字列の形式 {#url-string-formats}

データソース設定では、使用する必要のあるデータベースタイプに応じて、異なる URL 文字列の形式を使用します。以下に、AEM で現在サポートされているデータベース向けの形式を一覧で示します。

* `jdbc:postgresql:databasename` PostgreSQLの場合；
* `jdbc:db2://localhost:port/databasename` for DB2;
* `jdbc:oracle:thin:localhost:port:SID` Oracleの場合
* `jdbc:mysql://localhost:3306/databasename`（MySQL および MariaDB、試行用）
* `jdbc:sqlserver://localhost:1453;databaseName=name` (Microsoft SQL Server （試験的）用)

## 既知の制限事項 {#known-limitations}

単一データベースに対する複数の AEM インスタンスの同時使用は RDBMS の永続性によってサポートされますが、同時インストールはサポートされません。

この制限を回避するには、まず 1 つのメンバーでインストールを実行し、最初のインストールが完了した後で、他のメンバーを追加します。

