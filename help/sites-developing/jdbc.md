---
title: SQL データベースへの接続
seo-title: Connecting to SQL Databases
description: 外部 SQL データベースにアクセスして、AEM アプリケーションがデータを操作できるようにします
seo-description: Access an external SQL database to so that your AEM applications can interact with the data
uuid: 0af0ed08-9487-4c37-87ce-049c9b4c1ea2
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 11a11803-bce4-4099-9b50-92327608f37b
exl-id: 1082b2d7-2d1b-4c8c-a31d-effa403b21b2
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '917'
ht-degree: 85%

---

# SQL データベースへの接続{#connecting-to-sql-databases}

外部 SQL データベースにアクセスして、CQ アプリケーションがデータを操作できるようにします。

1. [JDBC ドライバーパッケージを書き出す OSGi バンドルを作成または取得します](#bundling-the-jdbc-database-driver)。
1. [JDBC データソースプールプロバイダーを設定します](#configuring-the-jdbc-connection-pool-service)。
1. [データソースオブジェクトを取得し、コード内で接続を作成します](#connecting-to-the-database)。

## JDBC データベースドライバーのバンドル {#bundling-the-jdbc-database-driver}

一部のデータベースベンダーは、OSGi バンドルで JDBC ドライバーを提供しています。例えば、 [MySQL](https://dev.mysql.com/downloads/connector/j/).データベースの JDBC ドライバーが OSGi バンドルとして使用できない場合は、ドライバー JAR を取得し、OSGi バンドルに含めます。バンドルは、データベースサーバーとの対話に必要なパッケージを書き出す必要があります。また、バンドルは、参照するパッケージもインポートする必要があります。

次の例では、[Maven 用プラグインのバンドル](https://felix.apache.org/documentation/subprojects/apache-felix-maven-bundle-plugin-bnd.html)を使用して、HSQLDB ドライバーを OSGi バンドル内にラップします。POM では、このプラグインに対して、hsqldb.jar ファイルを埋め込み、そのファイルを依存関係として識別するように指示します。すべての org.hsqldb パッケージが書き出されます。

このプラグインは、インポートすべきパッケージを自動的に決定し、それらをバンドルの MANIFEST.MF ファイルに記載します。CQ サーバーで使用できないパッケージがある場合、インストール時にバンドルが起動しません。次の 2 つの解決策が考えられます。

* POM で、パッケージがオプションであることを示します。この解決策は、JDBC 接続で実際にはそのパッケージのメンバーが不要である場合に使用します。次の例に示すように、Import-Package 要素を使用してオプションのパッケージを指定します。

  `<Import-Package>org.jboss.*;resolution:=optional,*</Import-Package>`
* パッケージを含む JAR ファイルを、パッケージを書き出す OSGi バンドルにラップし、そのバンドルをデプロイします。この解決策は、コード実行中にパッケージのメンバーが必要になる場合に使用します。

ソースコードを知ることで、どちらの解決策を使用すべきかを判断できます。また、いずれかの解決策を試してテストを実行し、解決策の妥当性を検証することもできます。

### hsqldb.jar をバンドルする POM {#pom-that-bundles-hsqldb-jar}

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
  xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>

  <groupId>com.adobe.example.myapp</groupId>
  <artifactId>hsqldb-jdbc-driver-bundle</artifactId>
  <version>0.0.1-SNAPSHOT</version>
  <name>wrapper-bundle-hsqldb-driver</name>
  <url>www.adobe.com</url>
  <description>Exports the HSQL JDBC driver</description>
  <packaging>bundle</packaging>
  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
  </properties>
  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.felix</groupId>
        <artifactId>maven-bundle-plugin</artifactId>
        <version>1.4.3</version>
        <extensions>true</extensions>
        <configuration>
         <instructions>
            <Embed-Dependency>*</Embed-Dependency>
            <_exportcontents>org.hsqldb.*</_exportcontents>
          </instructions>
        </configuration>
      </plugin>
    </plugins>
  </build>
  <dependencies>
    <dependency>
      <groupId>hsqldb</groupId>
      <artifactId>hsqldb</artifactId>
      <version>2.2.9</version>
    </dependency>
  </dependencies>
</project>
```

次のリンクより、一般的なデータベース製品のダウンロードページを開くことができます。

* [Microsoft® SQL Server](https://www.microsoft.com/en-us/sql-server/sql-server-downloads)
* [Oracle](https://www.oracle.com/database/technologies/appdev/jdbc-downloads.html)
* [IBM® DB2®](https://www.ibm.com/support/pages/download-db2-fix-packs-version-db2-linux-unix-and-windows)

### JDBC 接続プールサービスの設定 {#configuring-the-jdbc-connection-pool-service}

JDBC ドライバーを使用してデータソースオブジェクトを作成する JDBC Connections Pool サービスの設定を追加します。アプリケーションコードではこのサービスを使用してデータソースオブジェクトを取得し、データベースに接続します。

JDBC 接続プール（`com.day.commons.datasource.jdbcpool.JdbcPoolService`）はファクトリサービスです。読み取り専用や読み取り/書き込みアクセスなど、異なるプロパティを使用する接続が必要な場合は、複数の設定を作成します。

CQ で作業する場合は、いくつかの方法でこのようなサービスの設定を管理できます。詳しくは、[OSGi の設定](/help/sites-deploying/configuring-osgi.md)を参照してください。

プールに入れられた接続サービスを設定するには、次のプロパティを使用できます。プロパティ名は、web コンソールに表示されるとおりに表示されます。`sling:OsgiConfig` ノードに対応する名前を括弧内に示しています。エイリアスが `mydb` である HSQLDB サーバーおよびデータベースの値の例を示しています。

* JDBC ドライバークラス ( `jdbc.driver.class`):java.sql.Driver インターフェイスを実装するために使用する Java™クラス。例： `org.hsqldb.jdbc.JDBCDriver`. データタイプは `String` です。

* JDBC 接続 URI ( `jdbc.connection.uri`)：接続の作成に使用するデータベースの URL（例： ） `jdbc:hsqldb:hsql//10.36.79.223:9001/mydb`. URL の形式は、java.sql.DriverManager クラスの getConnection メソッドで使用する場合に有効である必要があります。データタイプは `String` です。

* ユーザー名（`jdbc.username`）：データベースサーバーでの認証に使用するユーザー名。データタイプは `String` です。

* Password（`jdbc.password`）：ユーザーの認証に使用するパスワード。データタイプは `String` です。

* 検証クエリ ( `jdbc.validation.query`)：接続が成功したことを検証するために使用する SQL 文（例： ） `select 1 from INFORMATION_SCHEMA.SYSTEM_USERS`. データタイプは `String` です。

* デフォルトで読み取り専用（default.readonly）：この接続を読み取り専用アクセスにする場合に、このオプションを選択します。データタイプは `Boolean` です。
* デフォルトで自動コミット（`default.autocommit`）：データベースに送信される SQL コマンドごとに個別のトランザクションを作成し、各トランザクションを自動的にコミットする場合は、このオプションを選択します。コード内でトランザクションを明示的にコミットする場合は、このオプションを選択しないでください。データタイプは `Boolean` です。

* プールサイズ（`pool.size`）：データベースに対して使用可能にする同時接続の数です。データタイプは `Long` です。

* プール待機時間（`pool.max.wait.msec`）：接続リクエストがタイムアウトするまでの時間です。データタイプは `Long` です。

* データソース名（`datasource.name`）：このデータソースの名前です。データタイプは `String` です。

* 追加のサービスプロパティ（`datasource.svc.properties`）：接続 URL に追加する名前と値のペアのセットです。データタイプは `String[]` です。

JDBC 接続プールサービスはファクトリです。そのため、`sling:OsgiConfig` ノードを使用して接続サービスを設定する場合、ノード名には、ファクトリサービス PID に *`-alias`* が続く名前を含める必要があります。使用するエイリアスは、その PID のすべての設定ノードで一意である必要があります。ノード名は、例えば `com.day.commons.datasource.jdbcpool.JdbcPoolService-myhsqldbpool` のような形式になります。

![chlimage_1-7](assets/chlimage_1-7a.png)

### データベースへの接続 {#connecting-to-the-database}

Java™ コードでは、DataSourcePool サービスを使用して、作成した設定に対応する `javax.sql.DataSource` オブジェクトを取得する必要があります。DataSourcePool サービスには `getDataSource` メソッドがあり、このメソッドは指定したデータソース名の `DataSource` オブジェクトを返します。メソッド引数として、JDBC 接続プール設定で指定した データソース名（または `datasource.name`）プロパティの値を使用します。

次の JSP コードの例では、hsqldbds データソースのインスタンスを取得し、単純な SQL クエリを実行し、返される結果の数を表示します。

#### データベースルックアップを実行する JSP {#jsp-that-performs-a-database-lookup}

```java
<%@include file="/libs/foundation/global.jsp"%><%
%><%@page session="false"%><%
%><%@ page import="com.day.commons.datasource.poolservice.DataSourcePool" %><%
%><%@ page import="javax.sql.DataSource" %><%
%><%@ page import="java.sql.Connection" %><%
%><%@ page import="java.sql.SQLException" %><%
%><%@ page import="java.sql.Statement" %><%
%><%@ page import="java.sql.ResultSet"%><%
%><html>
<cq:include script="head.jsp"/>
<body>
<%DataSourcePool dspService = sling.getService(DataSourcePool.class);
  try {
     DataSource ds = (DataSource) dspService.getDataSource("hsqldbds");
     if(ds != null) {
         %><p>Obtained the datasource!</p><%
         %><%final Connection connection = ds.getConnection();
          final Statement statement = connection.createStatement();
          final ResultSet resultSet = statement.executeQuery("SELECT * from INFORMATION_SCHEMA.SYSTEM_USERS");
          int r=0;
          while(resultSet.next()){
             r=r+1;
          }
          resultSet.close();
          %><p>Number of results: <%=r%></p><%
      }
   }catch (Exception e) {
        %><p>error! <%=e.getMessage()%></p><%
    }
%></body>
</html>
```

>[!NOTE]
>
>データソースが見つからないため、getDataSource メソッドが例外を発生する場合は、Connections Pool サービスの設定が正しいことを確認してください。プロパティ名、値およびデータタイプを確認します。
>

<!-- Link below redirects to the "Get started with AEM Sites - WKND tutorial"
>[!NOTE]
>
>To learn how to inject a DataSourcePool into an OSGi bundle, see [Injecting a DataSourcePool Service into an Adobe Experience Manager OSGi bundle](https://helpx.adobe.com/experience-manager/using/datasourcepool.html). -->
