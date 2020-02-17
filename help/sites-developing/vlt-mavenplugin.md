---
title: Maven を使用したパッケージの管理
seo-title: Maven を使用したパッケージの管理
description: パッケージ管理タスクを Maven プロジェクトに組み込むには、Content Package Maven Plugin を使用します
seo-description: パッケージ管理タスクを Maven プロジェクトに組み込むには、Content Package Maven Plugin を使用します
uuid: fa73f0d6-8848-4911-9b96-311c875b45be
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 943de371-0149-4307-be3a-b11c590b3451
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d

---


# Maven を使用したパッケージの管理{#managing-packages-using-maven}

パッケージ管理タスクを Maven プロジェクトに組み込むには、Content Package Maven Plugin を使用します。このプラグインのゴールとパラメーターにより、通常はパッケージマネージャーページまたは FileVault コマンドラインを使用して実行する多くのタスクを自動化できます。

* ファイルシステム内のファイルから新しいパッケージを作成します。
* CRX または CQ サーバーのパッケージをインストールおよびアンインストールします。
* サーバーで定義済みのパッケージをビルドします。
* サーバーにインストールされたパッケージのリストを取得します。
* サーバーからパッケージを削除します。

## POM ファイルへの Content Package Maven Plugin の追加 {#adding-the-content-package-maven-plugin-to-the-pom-file}

Content Package Maven Plugin を使用するには、POM ファイルのビルド要素内に次のプラグイン要素を追加します。

```xml
<plugin>
 <groupId>com.day.jcr.vault</groupId>
 <artifactId>content-package-maven-plugin</artifactId>
 <version>0.0.24</version>
 <configuration>
       <!-- parameters and values common to all goals, as required -->
 </configuration>
</plugin>
```

Maven でプラグインをダウンロードできるようにするには、このページの [Content Package Maven Plugin の取得](#obtaining-the-content-package-maven-plugin)で提供されるプロファイルを使用します。

## Content Package Maven Plugin のゴール {#goals-of-the-content-package-maven-plugin}

Content Package Plugin に用意されているゴールおよびゴールパラメーターについては、以降の節で説明します。共通パラメーターの節に示すパラメーターはほとんどのゴールに使用できます。1 つのゴールに適用するパラメーターについては、そのゴールの節を参照してください。

**プラグインプレフィックス**

プラグインプレフィックスは content-package です。次の例に示すように、コマンドラインからゴールを実行するには、このプレフィックスを使用します。

```shell
mvn content-package:build
```

**パラメータープレフィックス**

特に指定がない限り、プラグインのゴールおよびパラメーターでは、次の例に示すように vault プレフィックスを使用します。

```shell
mvn content-package:install -Dvault.targetURL="https://192.168.1.100:4502/crx/packmgr/service.jsp"
```

**プロキシ**

CRX または CQ サーバーにプロキシを使用するゴールでは、Maven 設定で見つかった有効な最初のプロキシ設定を使用します。プロキシ設定が見つからない場合、プロキシは使用されません。共通設定の節の useProxy パラメーターを参照してください。

### 共通パラメーター {#common-parameters}

次の表に示すパラメーターは、すべてのゴールに共通のパラメーターです（「ゴール」列に記載されている場合を除く）。

<table>
 <tbody>
  <tr>
   <th>名前</th>
   <th>タイプ</th>
   <th>必須</th>
   <th>デフォルト値</th>
   <th>説明</th>
   <th>ゴール</th>
  </tr>
  <tr>
   <td>failOnError</td>
   <td>ブール型</td>
   <td>いいえ</td>
   <td>false</td>
   <td>値 <code>true</code> を指定すると、エラーの発生時にビルドが失敗します。値 <code>false</code> を指定すると、ビルドの際にエラーが無視されます。</td>
   <td>package を除くすべてのゴール</td>
  </tr>
  <tr>
   <td>name</td>
   <td>文字列</td>
   <td>build：はい<br />
install：いいえ<br />
rm：はい</td>
   <td>build：デフォルト値なし<br />
install：Maven プロジェクトの artifactId プロパティの値</td>
   <td>処理を行うパッケージの名前。</td>
   <td>ls を除くすべてのゴール</td>
  </tr>
  <tr>
   <td>password</td>
   <td>文字列</td>
   <td>はい</td>
   <td>admin</td>
   <td>CRX サーバーでの認証に使用するパスワード。</td>
   <td>package を除くすべてのゴール</td>
  </tr>
  <tr>
   <td>serverId</td>
   <td>文字列</td>
   <td>いいえ</td>
   <td></td>
   <td>認証用のユーザー名とパスワードの取得元のサーバー ID。</td>
   <td>package を除くすべてのゴール</td>
  </tr>
  <tr>
   <td>targetURL</td>
   <td>文字列</td>
   <td>はい</td>
   <td>http://localhost:4502/<br />
crx/packmgr/<br />
service.jsp</td>
   <td>CRX パッケージマネージャーの HTTP サービス API の URL。</td>
   <td>package を除くすべてのゴール</td>
  </tr>
  <tr>
   <td>timeout</td>
   <td>int</td>
   <td>いいえ</td>
   <td>5</td>
   <td>パッケージマネージャーサービスとの通信の接続タイムアウト（秒）。</td>
   <td>package を除くすべてのゴール</td>
  </tr>
  <tr>
   <td>useProxy</td>
   <td>ブール型</td>
   <td>いいえ</td>
   <td>true</td>
   <td>Maven 設定ファイルのプロキシ設定を使用するかどうかを指定します。A value of <code>true</code> causes the use of the first active proxy configuration found to proxy requests to the package manager. 値 false を指定すると、プロキシは使用されません。</td>
   <td>package を除くすべてのゴール</td>
  </tr>
  <tr>
   <td>userId</td>
   <td>文字列</td>
   <td>はい</td>
   <td>admin</td>
   <td>CRX サーバーで認証するユーザー名。</td>
   <td>package を除くすべてのゴール</td>
  </tr>
  <tr>
   <td>verbose</td>
   <td>ブール型</td>
   <td>いいえ</td>
   <td>false</td>
   <td>詳細ログを有効または無効にします。値 <code>true</code> を指定すると、詳細ログが有効になります。</td>
   <td>package を除くすべてのゴール</td>
  </tr>
 </tbody>
</table>

### build {#build}

AEMインスタンスで既に定義されているコンテンツパッケージを構築します。

>[!NOTE]
>
>Maven プロジェクト内でこのゴールを実行する必要はありません。

#### パラメーター {#parameters}

build ゴール用のすべてのパラメーターについては、[共通パラメーター](#common-parameters)を参照してください。

#### 例 {#example}

次の例は、IPアドレス10.36.79.223を使用してAEMインスタンスにインストールされるworkflow-mbeanパッケージを構築します。目標は、次のコマンドを使用して実行します。

```shell
mvn content-package:build
```

次の POM ファイルはコマンドラインツールの現在のディレクトリにあります。この POM では、パッケージ名およびパッケージサービスの URL を指定します。

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
  xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example</groupId>
  <artifactId>example-package</artifactId>
  <version>0.0.1-SNAPSHOT</version>
    <build>
        <plugins>
     <plugin>
  <groupId>com.day.jcr.vault</groupId>
  <artifactId>content-package-maven-plugin</artifactId>
  <version>0.0.24</version>
  <configuration>
   <name>workflow-mbean</name>
   <failOnError>true</failOnError>
   <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
  </configuration>
     </plugin>
 </plugins>
    </build>
</project>
```

### install {#install}

 リポジトリにパッケージをインストールします。このゴールの実行に Maven プロジェクトは不要です。このゴールは Maven のビルドライフサイクルの install フェーズにバインドされます。

#### パラメーター {#parameters-1}

In addition to the following parameters, see the descriptions in the [Common Parameters](#common-parameters) section.

<table>
 <tbody>
  <tr>
   <th>名前</th>
   <th>タイプ</th>
   <th>必須</th>
   <th>デフォルト値</th>
   <th>説明</th>
  </tr>
  <tr>
   <td>artifact</td>
   <td>文字列</td>
   <td>いいえ</td>
   <td>Maven プロジェクトの artifactId プロパティの値</td>
   <td>groupId:artifactId:version[:packaging] 形式の文字列</td>
  </tr>
  <tr>
   <td>artifactId</td>
   <td>文字列</td>
   <td>いいえ</td>
   <td></td>
   <td>インストールするアーティファクトの ID</td>
  </tr>
  <tr>
   <td>groupId</td>
   <td>文字列</td>
   <td>いいえ</td>
   <td></td>
   <td>インストールするアーティファクトのグループ ID</td>
  </tr>
  <tr>
   <td>install</td>
   <td>ブール型</td>
   <td>いいえ</td>
   <td>true</td>
   <td>アップロード時にパッケージを自動的に解凍するかどうかを指定します。値 true を指定するとパッケージが解凍され、false を指定するとパッケージは解凍されません。</td>
  </tr>
  <tr>
   <td>localRepository</td>
   <td>org.apache.maven.<br /> artifact. repository.<br /> ArtifactRepository</td>
   <td>いいえ</td>
   <td>localRepository システム変数の値</td>
   <td>ローカルの Maven リポジトリ。プラグイン設定を使用してこのパラメーターを設定することはできません。システムプロパティが常に使用されます。</td>
  </tr>
  <tr>
   <td>packageFile</td>
   <td>java.io.File</td>
   <td>いいえ</td>
   <td>Maven プロジェクト用に定義されるプライマリアーティファクト</td>
   <td>インストールするパッケージファイルの名前</td>
  </tr>
  <tr>
   <td>packaging</td>
   <td>文字列</td>
   <td>いいえ</td>
   <td>zip</td>
   <td>インストールするアーティファクトのパッケージ化のタイプ</td>
  </tr>
  <tr>
   <td>pomRemoteRepositories</td>
   <td>java.util.List</td>
   <td>はい</td>
   <td>Maven プロジェクト用に定義される remoteAtifactRepositories プロパティの値</td>
   <td>プラグイン設定を使用してこの値を設定することはできません。この値はプロジェクトで指定する必要があります。 </td>
  </tr>
  <tr>
   <td>project</td>
   <td>org.apache.maven.<br />
project.MavenProject</td>
   <td>はい</td>
   <td>プラグインが設定されるプロジェクト</td>
   <td>Maven プロジェクト。このプロジェクトはプラグイン設定を格納するので、暗黙的なプロジェクトです。</td>
  </tr>
  <tr>
   <td>repositoryId（POM）
repoID（コマンドライン）<i> </i><br /><i> </i></td>
   <td>文字列</td>
   <td>いいえ</td>
   <td>temp</td>
   <td>アーティファクトの取得元のリポジトリの ID。POM では repositoryID を使用します。コマンドラインでは repoID を使用します。</td>
  </tr>
  <tr>
   <td>repositoryUrl（POM）
repoURL（コマンドライン）<i> </i><br /><i> </i></td>
   <td>文字列</td>
   <td>いいえ</td>
   <td></td>
   <td>アーティファクトの取得元のリポジトリの URL。POM では repositoryURL を使用します。コマンドラインでは repoURL を使用します。</td>
  </tr>
  <tr>
   <td>version</td>
   <td>文字列</td>
   <td>いいえ</td>
   <td></td>
   <td>インストールするアーティファクトのバージョン</td>
  </tr>
 </tbody>
</table>

#### 例 {#example-1}

次の例では、workflow-mbean OSGi バンドルを格納するパッケージを作成して（[build](#build) ゴールの例を参照）インストールします。install ゴールは package install フェーズにバインドされるので、次のコマンドで install ゴールを実行します。

```shell
mvn install
```

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
    xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://maven.apache.org/POM/4.0.0
    https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example.myapp</groupId>
  <artifactId>workflow-mbean</artifactId>
  <version>0.0.3-SNAPSHOT</version>

  <build>
    <plugins>
      <plugin>
        <groupId>com.day.jcr.vault</groupId>
        <artifactId>content-package-maven-plugin</artifactId>
        <version>0.0.24</version>
        <configuration>
          <builtContentDirectory>jcr_root</builtContentDirectory>
          <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
        </configuration>
        <executions>
          <execution>
            <goals>
              <goal>package</goal>
            </goals>
          </execution>
        </executions>
      </plugin>
    </plugins>
  </build>
</project>
```

### ls {#ls}

パッケージマネージャーにデプロイされるパッケージを一覧表示します。

#### パラメーター {#parameters-2}

All parameters of the ls goal are described in the [Common Parameters](#common-parameters) section.

#### 例 {#example-2}

次の例は、IPアドレス10.36.79.223を持つAEMインスタンスにインストールされるパッケージを示しています。目標は、次のコマンドを使用して実行します。

```shell
mvn content-package:ls
```

次の POM ファイルはコマンドラインツールの現在のディレクトリにあります。この POM では、パッケージサービスの URL を指定します。

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
  xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example</groupId>
  <artifactId>example-package</artifactId>
  <version>0.0.1-SNAPSHOT</version>
    <build>
        <plugins>
     <plugin>
  <groupId>com.day.jcr.vault</groupId>
  <artifactId>content-package-maven-plugin</artifactId>
  <version>0.0.24</version>
  <configuration>
      <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
  </configuration>
      </plugin>
   </plugins>
     </build>
</project>
```

### rm {#rm}

パッケージマネージャーからパッケージを削除します。

#### パラメーター {#parameters-3}

All parameters of the rm goal are described in the [Common Parameters](#common-parameters) section.

#### 例 {#example-3}

次の例では、IPアドレス10.36.79.223を持つAEMインスタンスにインストールされているWorkflow-mbeanパッケージを削除します。目標は、次のコマンドを使用して実行します。

```shell
mvn content-package:rm
```

次の POM ファイルはコマンドラインツールの現在のディレクトリにあります。この POM では、パッケージサービスの URL およびパッケージの名前を指定します。

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
  xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example</groupId>
  <artifactId>example-package</artifactId>
  <version>0.0.1-SNAPSHOT</version>
    <build>
        <plugins>
     <plugin>
  <groupId>com.day.jcr.vault</groupId>
  <artifactId>content-package-maven-plugin</artifactId>
  <version>0.0.24</version>
  <configuration>
                    <name>workflow-mbean</name>
      <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
  </configuration>
      </plugin>
   </plugins>
     </build>
</project>
```

### uninstall {#uninstall}

パッケージをアンインストールします。このパッケージは、アンインストールされた状態でサーバーに残ります。

#### パラメーター {#parameters-4}

All parameters of the uninstall goal are described in the [Common Parameters](#common-parameters) section.

#### 例 {#example-4}

次の例では、IPアドレス10.36.79.223を持つAEMインスタンスにインストールされているworkflow-mbeanパッケージをアンインストールします。目標は、次のコマンドを使用して実行します。

```shell
mvn content-package:uninstall
```

次の POM ファイルはコマンドラインツールの現在のディレクトリにあります。この POM では、パッケージ名およびパッケージサービスの URL を指定します。

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
  xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example</groupId>
  <artifactId>workflow-mbean</artifactId>
  <version>0.0.3-SNAPSHOT</version>
    <build>
        <plugins>
     <plugin>
  <groupId>com.day.jcr.vault</groupId>
  <artifactId>content-package-maven-plugin</artifactId>
  <version>0.0.24</version>
  <configuration>
   <name>workflow-mbean</name>
   <failOnError>true</failOnError>
   <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
  </configuration>
     </plugin>
 </plugins>
    </build>
</project>
```

### package {#package}

コンテンツパッケージを作成します。package ゴールのデフォルト設定には、コンパイルしたファイルを保存するディレクトリのコンテンツが含まれます。package ゴールを実行するには、compile build フェーズを完了しておく必要があります。package ゴールは Maven のビルドライフサイクルの package フェーズにバインドされます。

#### パラメーター {#parameters-5}

In addition to the following parameters, see the description of the `name` parameter in the [Common Parameters](#common-parameters) section.

<table>
 <tbody>
  <tr>
   <th>名前</th>
   <th>タイプ</th>
   <th>必須</th>
   <th>デフォルト値</th>
   <th>説明</th>
  </tr>
  <tr>
   <td>archive</td>
   <td>org.apache.maven.<br /> archiver.<br /> MavenArchiveConfiguration</td>
   <td>いいえ</td>
   <td></td>
   <td>使用するアーカイブ設定。<a href="https://maven.apache.org/shared/maven-archiver/index.html">Maven Archiver のドキュメント</a>を参照してください。</td>
  </tr>
  <tr>
   <td>builtContentDirectory</td>
   <td>java.io.File</td>
   <td>はい</td>
   <td>Maven ビルドの出力ディレクトリの値</td>
   <td>パッケージに含めるコンテンツを格納するディレクトリ</td>
  </tr>
  <tr>
   <td>dependencies</td>
   <td>java.util.List</td>
   <td>いいえ</td>
   <td></td>
   <td></td>
  </tr>
  <tr>
   <td>embeddedTarget</td>
   <td>java.lang.String</td>
   <td>いいえ</td>
   <td></td>
   <td></td>
  </tr>
  <tr>
   <td>embeddeds</td>
   <td>java.util.List</td>
   <td>いいえ</td>
   <td></td>
   <td></td>
  </tr>
  <tr>
   <td>failOnMissingEmbed</td>
   <td>ブール型</td>
   <td>はい</td>
   <td>false</td>
   <td>値がtrueの場合、埋め込みアーティファクトがプロジェクトの依存関係に見つからないと、ビルドが失敗します。値offleを指定すると、ビルドでエラーが無視されます。</td>
  </tr>
  <tr>
   <td>filterSource</td>
   <td>java.io.File</td>
   <td>いいえ</td>
   <td></td>
   <td>ワークスペースフィルターのソースを指定するファイル。設定で指定され、embeddeds または subpackages を使用して挿入されるフィルターはファイルコンテンツと結合されます。</td>
  </tr>
  <tr>
   <td>filters</td>
   <td>com.day.jcr.<br /> vault.maven.pack.impl.<br /> DefaultWorkspaceFilter</td>
   <td>いいえ</td>
   <td></td>
   <td>パッケージのコンテンツを定義するフィルター要素を格納します。実行すると、filter.xml ファイルにフィルターが追加されます。以下の「フィルターの使用」の節を参照してください。</td>
  </tr>
  <tr>
   <td>finalName</td>
   <td>java.lang.String</td>
   <td>はい</td>
   <td>Maven プロジェクト（build フェーズ）で定義される finalName</td>
   <td>生成されるパッケージの ZIP ファイルの名前（ファイル拡張子 .zip を除く）</td>
  </tr>
  <tr>
   <td>group</td>
   <td>java.lang.String</td>
   <td>はい</td>
   <td>Maven プロジェクトで定義される groupID</td>
   <td>生成されるコンテンツパッケージのグループ ID。この値は、コンテンツパッケージのターゲットインストールパスに含まれます。</td>
  </tr>
  <tr>
   <td>outputDirectory</td>
   <td>java.io.File</td>
   <td>はい</td>
   <td>Maven プロジェクトで定義されるビルドディレクトリ</td>
   <td>コンテンツパッケージが保存されるローカルディレクトリ</td>
  </tr>
  <tr>
   <td>prefix</td>
   <td>java.lang.String</td>
   <td>いいえ</td>
   <td></td>
   <td></td>
  </tr>
  <tr>
   <td>project</td>
   <td>org.apache.maven.<br />
project.MavenProject</td>
   <td>はい</td>
   <td></td>
   <td>Maven プロジェクト。</td>
  </tr>
  <tr>
   <td>properties</td>
   <td>java.util.Map</td>
   <td>いいえ</td>
   <td></td>
   <td>properties.xml ファイルで設定できる追加のプロパティ。これらのプロパティで定義済みの次のプロパティを上書きすることはできません。
    <ul>
     <li>group：group パラメーターを使用して設定</li>
     <li>name：name パラメーターを使用して設定</li>
     <li>version：version パラメーターを使用して設定</li>
     <li>description：プロジェクトの説明から設定</li>
     <li>groupId：Maven プロジェクト記述子のグループ ID</li>
     <li>artifactId：Maven プロジェクト記述子のアーティファクト ID</li>
     <li>dependencies：dependencies パラメーターを使用して設定</li>
     <li>createdBy：user.name システムプロパティの値</li>
     <li>created：現在のシステム時刻</li>
     <li>requiresRoot：requiresRoot パラメーターを使用して設定</li>
     <li>packagePath：グループおよびパッケージの名前から自動的に生成</li>
    </ul> </td>
  </tr>
  <tr>
   <td>requiresRoot</td>
   <td>ブール型</td>
   <td>はい</td>
   <td>false</td>
   <td>パッケージにルートが必要かどうかを定義します。これは、properties.xml ファイルの &lt;code&gt;requiresRoot&lt;/code&gt; プロパティになります。</td>
  </tr>
  <tr>
   <td>subPackages</td>
   <td>java.util.List</td>
   <td>いいえ</td>
   <td></td>
   <td></td>
  </tr>
  <tr>
   <td>version</td>
   <td>java.lang.String</td>
   <td>はい</td>
   <td>Maven プロジェクトで定義されるバージョン</td>
   <td>コンテンツパッケージのバージョン</td>
  </tr>
  <tr>
   <td>workDirectory</td>
   <td>java.io.File</td>
   <td>はい</td>
   <td>Maven プロジェクト（build フェーズ）で定義されるディレクトリ</td>
   <td>パッケージに含めるコンテンツを格納するディレクトリ</td>
  </tr>
 </tbody>
</table>

#### フィルターの使用 {#using-filters}

パッケージのコンテンツを定義するには、フィルター要素を使用します。フィルターは、パッケージのファイル内のworkspaceFilter要素 `META-INF/vault/filter.xml` に追加されます。

次に示すフィルターの例は、使用する XML 構造を示しています。

```xml
<filter>
   <root>/apps/myapp</root>
   <mode>merge</mode>
       <includes>
              <include>/apps/myapp/install/</include>
              <include>/apps/myapp/components</include>
       </includes>
       <excludes>
              <exclude>/apps/myapp/config/*</exclude>
       </excludes>
</filter>
```

**読み込みモード**

`mode` 要素は、パッケージが読み込まれる際にリポジトリ内のコンテンツがどのような影響を受けるかを定義します。使用できる値は次のとおりです。

* **merge：**&#x200B;まだリポジトリに含まれていないパッケージのコンテンツが追加されます。パッケージ内およびリポジトリ内のコンテンツは変更されません。コンテンツがリポジトリから削除されることはありません。
* **** 置換：リポジトリにないパッケージ内のコンテンツがリポジトリに追加されます。リポジトリ内のコンテンツは、パッケージ内の一致するコンテンツに置き換えられます。コンテンツがパッケージに存在しない場合は、リポジトリからコンテンツが削除されます。
* **update：**&#x200B;リポジトリに含まれていないパッケージのコンテンツがリポジトリに追加されます。リポジトリ内のコンテンツは、パッケージ内の一致するコンテンツに置き換えられます。既存のコンテンツはリポジトリから削除されます。

フィルターに `mode` 要素が含まれていない場合は、デフォルト値 `replace` が使用されます。

#### 例 {#example-5}

次の例では、workflow-mbean OSGi バンドルを格納するパッケージを作成します。POM ファイルでは、jcr_root ディレクトリを builtContentDirectory プロパティの値と見なします。jcr_root ディレクトリでは、リポジトリをミラーリングするディレクトリ構造にバンドルの JAR ファイルが格納されます。

`jcr_root/apps/myapp/install/workflow-mbean-0.03-SNAPSHOT.jar`

このゴールは package build フェーズにバインドされるので、次のコマンドで package ゴールを実行します。

`mvn package`

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
    xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://maven.apache.org/POM/4.0.0
    https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example.myapp</groupId>
  <artifactId>workflow-mbean</artifactId>
  <version>0.0.3-SNAPSHOT</version>

  <build>
    <plugins>
      <plugin>
        <groupId>com.day.jcr.vault</groupId>
        <artifactId>content-package-maven-plugin</artifactId>
        <version>0.0.24</version>
        <configuration>
          <builtContentDirectory>jcr_root</builtContentDirectory>
          <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
        </configuration>
        <executions>
          <execution>
            <goals>
              <goal>package</goal>
            </goals>
          </execution>
        </executions>
      </plugin>
    </plugins>
  </build>
</project>
```

Instead of expressing the `package` goal in the plugin `executions` section, you can use `content-package` as the value of the project `packaging` element:

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
    xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://maven.apache.org/POM/4.0.0
    https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example.myapp</groupId>
  <artifactId>workflow-mbean</artifactId>
  <version>0.0.3-SNAPSHOT</version>
  <packaging>content-package</packaging>
  <build>
    <plugins>
      <plugin>
        <groupId>com.day.jcr.vault</groupId>
        <artifactId>content-package-maven-plugin</artifactId>
        <version>0.0.24</version>
        <configuration>
          <builtContentDirectory>jcr_root</builtContentDirectory>
          <targetURL>https://10.36.79.223:4502/crx/packmgr/service.jsp</targetURL>
        </configuration>
      </plugin>
    </plugins>
  </build>
</project>
```

### help {#help}

#### パラメーター {#parameters-6}

| 名前 | タイプ | 必須 | デフォルト値 | 説明 |
|---|---|---|---|---|
| detail | ブール型 | いいえ | false | 各ゴールに設定可能なプロパティをすべて表示するかどうかを指定します。値 true を指定すると、設定可能なプロパティがすべて表示されます。 |
| goal | 文字列 | いいえ |  | ヘルプを表示するゴールの名前。値を指定しない場合は、すべてのゴールのヘルプが表示されます。 |
| indentSize | int | いいえ | 2 | 各レベルのインデントに使用するスペースの数。値を指定する場合は、正の値を使用してください。 |
| lineLength | int | いいえ | 80 | 表示行の最大長。値を指定する場合は、正の値を使用してください。 |

## Content Package Maven Plugin の入手 {#obtaining-the-content-package-maven-plugin}

プラグインはアドビの公開リポジトリから入手できます。プラグインをダウンロードするには、次の Maven プロファイルを Maven 設定ファイルに追加してアクティブ化します。Maven コマンドを使用する場合は、必要に応じてプラグインがローカルリポジトリにダウンロードされます。

>[!NOTE]
>
>Adobe Public Releases リポジトリは参照可能なリポジトリではないので、Web ブラウザーを使用してリポジトリの URL にアクセスすると、「見つかりません」という内容のエラーが表示されます。ただし、Maven はリポジトリのディレクトリにアクセスできます。

```xml
<profile>
    <id>adobe-public</id>
    <activation>
         <activeByDefault>false</activeByDefault>
    </activation>
    <properties>
         <releaseRepository-Id>adobe-public-releases</releaseRepository-Id>
         <releaseRepository-Name>Adobe Public Releases</releaseRepository-Name>
         <releaseRepository-URL>https://repo.adobe.com/nexus/content/groups/public</releaseRepository-URL>
    </properties>
    <repositories>
         <repository>
             <id>adobe-public-releases</id>
             <name>Adobe Basel Public Repository</name>
             <url>https://repo.adobe.com/nexus/content/groups/public</url>
             <releases>
                 <enabled>true</enabled>
                 <updatePolicy>never</updatePolicy>
             </releases>
             <snapshots>
                 <enabled>false</enabled>
             </snapshots>
         </repository>
     </repositories>
     <pluginRepositories>
         <pluginRepository>
             <id>adobe-public-releases</id>
             <name>Adobe Basel Public Repository</name>
             <url>https://repo.adobe.com/nexus/content/groups/public</url>
             <releases>
                 <enabled>true</enabled>
                 <updatePolicy>never</updatePolicy>
             </releases>
             <snapshots>
                 <enabled>false</enabled>
             </snapshots>
         </pluginRepository>
     </pluginRepositories>
</profile>
```

## コンテンツパッケージへの OSGi バンドルの埋め込み {#embedding-osgi-bundles-in-a-content-package}

Content Package Maven Plugin を使用して、OSGi バンドルをコンテンツパッケージに埋め込みます。バンドルを埋め込むには、次の設定を実装します。

* Maven プロジェクトの依存関係としてバンドルを宣言する必要があります。
* プラグイン設定は、パッケージ内のバンドルの目的のパスを使用してバンドルを参照します。

次のサンプルの POM では、Apache Sling JCR UserManager バンドルを格納するパッケージを作成します。In the package, the bundle JAR is located in the `jcr_root/apps/myapp/install` folder:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="https://maven.apache.org/POM/4.0.0"
             xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
             xsi:schemaLocation="https://maven.apache.org/POM/4.0.0
             https://maven.apache.org/maven-v4_0_0.xsd">
 <modelVersion>4.0.0</modelVersion>
   <groupId>com.adobe.example.myapp</groupId>
 <artifactId>embedded-example</artifactId>
 <packaging>content-package</packaging>
 <version>1.0.0-SNAPSHOT</version>

   <build>
 <plugins>
     <plugin>
        <groupId>com.day.jcr.vault</groupId>
      <artifactId>content-package-maven-plugin</artifactId>
      <version>0.0.24</version>
      <extensions>true</extensions>
      <configuration>
   <filters>
       <filter>
    <root>/apps/myapp</root>
       </filter>
    </filters>
    <embeddeds>
       <embedded>
    <groupId>org.apache.sling</groupId>
    <artifactId>org.apache.sling.jcr.jackrabbit.usermanager</artifactId>
    <target>/apps/myproject/install</target>
        </embedded>
    </embeddeds>
       </configuration>
  </plugin>
    </plugins>
    </build>
    <dependencies>
 <dependency>
      <groupId>org.apache.sling</groupId>
      <artifactId>org.apache.sling.jcr.jackrabbit.usermanager</artifactId>
      <version>2.2.0</version>
 </dependency>
    </dependencies>
</project>
```

## パッケージへのサムネール画像またはプロパティファイルの追加 {#including-a-thumbnail-image-or-properties-file-in-the-package}

パッケージのプロパティをカスタマイズするには、デフォルトのパッケージ設定ファイルを置き換えます。例えば、パッケージを識別するためのサムネール画像をパッケージマネージャーとパッケージ共有に追加します。

パッケージでは、FileVault に特有のファイルは /META-INF/vault フォルダーにあります。ソースファイルはファイルシステム内の任意の場所に配置できます。POM ファイルでは、target/vault-work/META-INF にソースファイルをコピーするように、パッケージに追加するビルドのリソースを定義します。

次の POM コードでは、プロジェクトのソースの META-INF フォルダー内のファイルをパッケージに追加します。

```xml
<build>
    <resources>
        <!-- vault META-INF resources (thumbnail etc.) -->
        <resource>
            <directory>${basedir}/src/main/content/META-INF</directory>
            <targetPath>../vault-work/META-INF</targetPath>
        </resource>
    </resources>
</build>
```

次の POM コードでは、1 つのサムネール画像だけをパッケージに追加します。サムネール画像の名前を thumbnail.png と指定して、パッケージの META-INF/vault/definition フォルダーに配置してください。この例では、ソースファイルはプロジェクトの /src/main/content/META-INF/vault/definition フォルダーにあります。

```xml
<build>
    <resources>
        <!-- thumbnail only -->
        <resource>
            <directory>${basedir}/src/main/content/META-INF/vault/definition</directory>
            <targetPath>../vault-work/META-INF/vault/definition</targetPath>
        </resource>
    </resources>
</build>
```

## Using Archetypes To Generate AEM Projects {#using-archetypes-to-generate-aem-projects}

AEMプロジェクトの生成には、いくつかのMavenアーキタイプを使用できます。 開発目的に応じたアーキタイプを使用してください。

* A content package that installs resources for a AEM application: [simple-content-package-archetype](#simple-content-package-archetype)
* サードパーティのアーティファクトを含むコンテンツパッケージ：[simple-content-package-with-embedded-archetype](#simple-content-package-with-embedded-archetype)
* Java クラスの開発および単体テストに対応したマルチモジュールアプリケーション：[multimodule-content-package-archetype](#multimodule-content-package-archetype)

>[!NOTE]
>
>Apache Slingプロジェクトには、AEM開発に役立つアーキタイプも用意されています。 These are documented at [https://sling.apache.org/site/maven-archetypes.html](https://sling.apache.org/documentation/development/maven-archetypes.html).

各アーキタイプでは以下の項目を生成します。

* プロジェクトフォルダー構造
* POM ファイル
* FileVault 設定ファイル

アーキタイプアーティファクトはアドビの Maven 公開リポジトリから入手できます。アーキタイプをダウンロードして実行するには、Maven の archetype:generate コマンドのパラメーターを使用して、アーキタイプとアドビのリポジトリを特定します。

```shell
mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault \
-DarchetypeArtifactId={id_of_archetype} -DarchetypeVersion=1.0.2 \
-DarchetypeRepository=adobe-public-releases
```

Maven アーキタイププラグインは、シェルまたはコマンドプロンプトでインタラクティブモードを使用して、プロジェクトに関する情報を収集します。提供された情報は、プロジェクトの様々なプロパティ（フォルダー名、アーティファクト ID など）の設定に使用されます。

**POM ファイル**

生成されるPOMファイルには、コードのコンパイル、バンドルの作成、パッケージ内のAEMへのデプロイを行うコマンドが含まれます。 The `groupID`, `artifactId`, `version`, and `name` properties of the Maven project are automatically populated using the values that you provide to the Maven `archetype:generate` interactive prompt.

生成されたpom.xmlファイルで次のデフォルト値を変更できます。

* CQサーバー名またはIPアドレス：デフォルト値はです `localhost`。 下の要 `crx.host` 素にこの値 `project/properties` が含まれています。

* CQサーバーのポート番号：デフォルト値はです `4502`。 下の要 `crx.port` 素にこの値 `project/properties` が含まれています。

* Content Package Maven Plugin のバージョン：`version` の `artifactId` と共に、プラグインの `content-package-maven-plugin` 要素の内容として最新バージョンを使用します。デフォルト値は `0.0.24` です。

**アーキタイプの使用**

1. シェルウィンドウまたはコマンドプロンプトで、Maven の `archetype:generate` コマンドを入力します。メッセージが表示されたら、残りのパラメーターの値を指定します。

   各パラメーターの詳細については、使用しているアーキタイプの節を参照してください。

1. テキストエディターで pom.xml ファイルを開き、必要に応じてデフォルト値を編集します。
1. 生成されたフォルダーにリソースを配置します。
1. コマンドを入 `mvn clean install` 力します。

### simple-content-package-archetype {#simple-content-package-archetype}

単純なAEMアプリケーションのリソースのインストールに適したMavenプロジェクトを作成します。 The folder structure is that used below the `/apps` folder of the AEM repository. POMは、フォルダーに配置するリソースをパッケージ化し、AEMインスタンスにパッケージをインストールするためのコマンドを定義します。

**アーキタイプアーティファクトのプロパティ：**

* Group ID: `com.day.jcr.vault`
* Artifact ID: `simple-content-package-archetype`
* バージョン: `1.0.2`
* リポジトリ: `adobe-public-releases`

**Maven コマンド：**

```shell
mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault \
-DarchetypeArtifactId=simple-content-package-archetype \
-DarchetypeVersion=1.0.2 \
-DarchetypeRepository=adobe-public-releases
```

**アーキタイプのパラメーター：**

* groupId：Maven が生成するコンテンツパッケージのグループ ID。この値は POM ファイルで自動的に使用されます。
* artifactId：コンテンツパッケージの名前。この値はプロジェクトフォルダーの名前としても使用されます。
* version：コンテンツパッケージのバージョン。
* package：この値は simple-content-package-archetype には使用されません。
* appsFolderName：/apps の下にあるフォルダーの名前。
* artifactName：コンテンツパッケージの説明。
* packageGroup：コンテンツパッケージグループの名前。この値は、Content Package Maven Plugin の package ゴールの group パラメーターを設定します。

**フォルダー構造：**

```xml
${artifactId}
   |- pom.xml
   |- README.txt
   |- src
      |- main
         |- content
             |- jcr_root
                 |- apps
                     |- ${appsFolderName}
                            |- components
                               |- .content.xml
                            |- config
                            |- install
             |- META-INF
                 |- vault
                     |- config.xml
                     |- filter.xml
                     |- nodetypes.cnd
                     |- properties.xml
                     |- definition
                        |- .content.xml
```

### simple-content-package-with-embedded-archetype {#simple-content-package-with-embedded-archetype}

simple-content-package-archetype と同じタスクを実行します。また、Maven の公開リポジトリからアーティファクトをダウンロードして追加します。

**アーキタイプバンドルのプロパティ：**

* Group ID: `com.day.jcr.vault`
* Artifact ID: `simple-content-package-with-embedded-archetype`
* バージョン: `1.0.2`
* リポジトリ: `adobe-public-releases`

**Maven コマンド：**

```shell
mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault \
-DarchetypeArtifactId=simple-content-package-with-embedded-archetype \
-DarchetypeVersion=1.0.2 \
-DarchetypeRepository=adobe-public-releases
```

**アーキタイプのパラメーター：**

* groupId：Maven が生成するコンテンツパッケージのグループ ID。この値は POM ファイルで自動的に使用されます。
* artifactId：コンテンツパッケージの名前。この値はプロジェクトフォルダーの名前としても使用されます。
* version：コンテンツパッケージのバージョン。
* package：このパラメーターは使用されません。
* appsFolderName：/apps の下にあるフォルダーの名前。
* artifactName：コンテンツパッケージの説明。
* embeddedArtifactId：コンテンツパッケージに埋め込むアーティファクトの ID。
* embeddedGroupId：埋め込むアーティファクトのグループ ID。
* embeddedVersion：埋め込むアーティファクトのバージョン。
* packageGroup：コンテンツパッケージグループの名前。この値は、Content Package Maven Plugin の package ゴールの group パラメーターを設定します。

**フォルダー構造：**

```xml
${artifactId}
   |- pom.xml
   |- README.txt
   |- src
      |- main
         |- content
             |- jcr_root
                 |- apps
                     |- ${appsFolderName}
                            |- components
                            |- config
                            |- install
             |- META-INF
                 |- vault
                     |- config.xml
                     |- filter.xml
                     |- nodetypes.cnd
                     |- properties.xml
                     |- definition
```

### multimodule-content-package-archetype {#multimodule-content-package-archetype}

AEMアプリケーションを開発し、リソースをサーバーにインストールするためのフォルダー構造を含むMavenプロジェクトを作成します。

`bundle` フォルダーには、開発する Java および JUnit のソースファイルを格納するフォルダー構造が含まれています。このフォルダー内の pom.xml ファイルは OSGi バンドルを作成します。POM の以下の値によって、アーティファクトとバンドルが識別されます。

* artifactID: `${artifactID}-bundle`.
* Bundle-SymbolicName: `${groupId}.${artifactId}-bundle`.

`${artifactID}` とは、 `${groupId}` アーキタイプの実行時にこれらのパラメーターに指定する値です。

The `content` folder contains the resources that are installed to the AEM instance. The value of artifactID is `${artifactID}multimodule-bundle`.

親フォルダーには、Maven プラグインと依存関係を管理する親 POM が格納されます。

**アーキタイプバンドルのプロパティ：**

* Group ID: `com.day.jcr.vault`
* Artifact ID: `multimodule-content-package-archetype`
* バージョン: `1.0.2`
* リポジトリ: `adobe-public-releases`

**Maven コマンド：**

```shell
mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault \
-DarchetypeArtifactId=multimodule-content-package-archetype \
-DarchetypeVersion=1.0.2 \
-DarchetypeRepository=adobe-public-releases
```

**アーキタイプのパラメーター：**

* groupId：Maven が生成するコンテンツパッケージのグループ ID。この値は POM ファイルで自動的に使用されます。
* artifactId：コンテンツパッケージの名前。この値はプロジェクトフォルダーの名前としても使用されます。
* version：コンテンツパッケージのバージョン。
* package：この値は multimodule-content-package-archetype には使用されません。
* appsFolderName：/apps の下にあるフォルダーの名前。
* artifactName：コンテンツパッケージの説明。
* packageGroup：コンテンツパッケージグループの名前。この値は、Content Package Maven Plugin の package ゴールの group パラメーターを設定します。

**フォルダー構造：**

```xml
${artifactId}
   |- pom.xml
   |- bundle
      |- pom.xml
      |- src
         |- main
            |- java
               |- ${groupId}
                  |- SimpleDSComponent.java
         |- test
            |- java
               |- ${groupId}
                  |- SimpleUnitTest.java
   |- content
      |- pom.xml
      |- src
         |- main
            |- content
               |- jcr_root
                  |- apps
                     |- ${appsFolderName}
                            |- config
                            |- install
                  |- META-INF
                      |- vault
                         |- config.xml
                         |- filter.xml
                         |- nodetypes.cnd
                         |- properties.xml
                         |- definition
                            |- .content.xml
```

