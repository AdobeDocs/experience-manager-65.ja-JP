---
title: アプリケーションサーバーのインストール
description: Adobe Experience Manager をアプリケーションサーバーと共にインストールする方法について説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
exl-id: 3a90f1d2-e53f-4cc4-8122-024ad6500de0
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
source-git-commit: a28883778c5e8fb90cbbd0291ded17059ab2ba7e
workflow-type: tm+mt
source-wordcount: '1166'
ht-degree: 93%

---

# アプリケーションサーバーのインストール{#application-server-install}

>[!NOTE]
>
>Adobe Experience Manager（AEM）がリリースされているファイル形式は `JAR` と `WAR` です。これらの形式に対しては、アドビが提供するサポートレベルを維持できるよう、品質保証プロセスが実施されています。
>

この節では、アプリケーションサーバーを使用してAdobe Experience Manager（AEM）をインストールする方法について説明します。個々のアプリケーションサーバーに提供されている特定のサポートのレベルについては、「[サポートされているプラットフォーム](/help/sites-deploying/technical-requirements.md#servlet-engines-application-servers)」セクションを参照してください。

以下のアプリケーションサーバーのインストール手順について説明します。

* [WebSphere](#websphere)
* [JBoss](#jboss-eap)
* [Oracle WebLogic 12.1.3／12.2](#oracle-weblogic)
* [Tomcat 8／8.5](#tomcat)

Web アプリケーションのインストール、サーバーの設定、サーバーの起動および停止方法について詳しくは、該当するアプリケーションサーバーのドキュメントを参照してください。

>[!NOTE]
>
>WAR デプロイメントで Dynamic Media を使用している場合は、[Dynamic Media のドキュメント](/help/assets/config-dynamic.md#enabling-dynamic-media)を参照してください。

## 概要 {#general-description}

### アプリケーションサーバーに AEM をインストールするときのデフォルトの動作 {#default-behaviour-when-installing-aem-in-an-application-server}

AEM は、単一の war ファイルとしてデプロイされます。

デプロイすると、デフォルトで次のようになります。

* 実行モードは `author`
* インスタンス（リポジトリ、Felix OSGI 環境、バンドルなど）が、`${user.dir}/crx-quickstart` にインストールされる（ここで、`${user.dir}` は現在の作業ディレクトリで、crx-quickstart へのこのバスを `sling.home` と呼ぶ）

* コンテキストルートは war ファイル名（例：`aem-6`）

#### 設定 {#configuration}

デフォルトの動作は次のように変更できます。

* 実行モード：デプロイメント前に、AEM war ファイルの `sling.run.modes` ファイルで `WEB-INF/web.xml` パラメーターを設定

* sling.home：デプロイメント前に、AEM war ファイルの `WEB-INF/web.xml` ファイルで `sling.home` パラメーターを設定

* コンテキストルート：AEM war ファイル名を変更

#### パブリッシュインストール {#publish-installation}

パブリッシュインスタンスをデプロイするには、実行モードを publish に設定する必要があります。

* AEM war ファイルから WEB-INF/web.xml を展開
* sling.run.modes パラメーターを publish に変更
* web.xml ファイルを AEM war ファイルに再圧縮
* AEM war ファイルをデプロイします。

#### インストールの確認 {#installation-check}

すべてがインストールされているかどうかは、次の手順で確認します。

* `error.log` ファイルに対して「テール」を実行して、すべてのコンテンツがインストールされていることを確認
* `/system/console` を調べて、すべてのバンドルがインストールされていることを確認

#### 同じアプリケーションサーバーに 2 つのインスタンス {#two-instances-on-the-same-application-server}

デモンストレーション目的で、オーサーインスタンスとパブリッシュインスタンスを 1 つのアプリケーションサーバーにインストールすることが適切な場合があります。そのためには、次の手順に従います。

1. パブリッシュインスタンスの sling.home 変数と sling.run.modes 変数を変更します。
1. AEM war ファイルから WEB-INF/web.xml ファイルを展開します。
1. sling.home パラメーターを別のパス（絶対パスと相対パスが指定可能）に変更します。
1. sling.run.modes を、パブリッシュインスタンス用に publish に変更します。
1. web.xml ファイルを再圧縮します。
1. war ファイルの名前を、別々の名前になるように変更します。例えば、一方を aemauthor.war に、もう一方を aempublish.war に変更します。
1. 高めのメモリ設定を使用します。例えば、デフォルトの AEM インスタンスの場合は、`-Xmx3072m` などを使用します。
1. 2 つの web アプリケーションをデプロイします。
1. デプロイメント後、2 つの web アプリケーションを停止します。
1. オーサーインスタンスとパブリッシュインスタンスの両方で、sling.properties ファイルで property felix.service.urlhandlers=false が false に設定されていると仮定します（デフォルトでは true に設定）。
1. 2 つの web アプリケーションを再起動します。

## アプリケーションサーバーのインストール手順 {#application-servers-installation-procedures}

### WebSphere® 8.5 {#websphere}

デプロイメントの前に、上記の[概要](#general-description)をお読みください。

**サーバーの準備**

* Basic 認証ヘッダーを無効にします。

   * AEM にユーザーを認証させる方法の 1 つは、WebSphere® サーバーのグローバル管理セキュリティを無効にすることです。無効にするには、セキュリティ／グローバル セキュリティに移動し、「Enable administrative security」チェックボックスをオフにして、保存し、サーバーを再起動します。

* `"JAVA_OPTS= -Xmx2048m"` の設定
* コンテキストルート = / を使用して AEM をインストールする場合は、既存のデフォルト web アプリケーションのコンテキストルートを変更します。

**AEM web アプリケーションのデプロイ**

* AEM war ファイルをダウンロードします。
* 必要に応じて、web.xml で設定します（上記の概要を参照）。

   * WEB-INF/web.xml ファイルを解凍
   * sling.run.modes パラメーターを publish に変更
   * sling.home 初期パラメーターをコメント解除し、必要に応じてこのパスを設定
   * web.xml ファイルを再圧縮

* AEM war ファイルをデプロイします。

   * コンテキストルートを選択します（Sling 実行モードを設定する場合は、デプロイウィザードの詳細な手順を選択し、ウィザードの手順 6 で指定する必要があります）。

* AEM web アプリケーションの起動

#### JBoss® EAP 6.3.0/6.4.0 {#jboss-eap}

デプロイメントの前に、上記の[概要](#general-description)をお読みください。

**JBoss® サーバーの準備**

設定ファイル（`standalone.conf` など）でメモリ引数を設定

* JAVA_OPTS=&quot;-Xms64m -Xmx2048m&quot;

deployment-scanner を使用して AEM web アプリケーションをインストールする場合は、`deployment-timeout,` の値を増やすことをお勧めします。そのためには、インスタンスの xml ファイル（`configuration/standalone.xml)` など）で `deployment-timeout` 属性を設定します。

```xml
<subsystem xmlns="urn:jboss:domain:deployment-scanner:1.1">
            <deployment-scanner path="deployments" relative-to="jboss.server.base.dir" scan-interval="5000" deployment-timeout="1000"/>
</subsystem>
```

**AEM web アプリケーションのデプロイ**

* JBoss® 管理コンソールで AEM web アプリケーションをアップロードします。

* AEM web アプリケーションを有効にします。

#### Oracle WebLogic 12.1.3／12.2 {#oracle-weblogic}

デプロイメントの前に、上記の[概要](#general-description)をお読みください。

これは、管理サーバーのみを備えたシンプルなサーバーレイアウトを使用します。

**WebLogic サーバーの準備**

* `${myDomain}/config/config.xml` で、security-configuration セクションに以下を追加します。

   * `<enforce-valid-basic-auth-credentials>false</enforce-valid-basic-auth-credentials>`正確な位置については、[https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd](https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd) を参照してください（デフォルトではセクションの最後に追加すれば問題ありません）。

* VM メモリ設定の値を増やします。

   * `${myDomain}/bin/setDomainEnv.cmd`（resp .sh）を開いて WLS_MEM_ARGS を検索し、設定します（例：`WLS_MEM_ARGS_64BIT=-Xms256m -Xmx2048m` を設定）
   * WebLogic Server を再起動します。

* `${myDomain}` に packages フォルダーを作成し、その中に cq フォルダー、その中に Plan フォルダーを作成します。

**AEM web アプリケーションのデプロイ**

* AEM war ファイルをダウンロードします。
* AEM war ファイルを the ${myDomain}/packages/cq フォルダー内に配置します。
* 必要に応じて、`WEB-INF/web.xml` で設定します（上記の「概要」を参照）。

   * `WEB-INF/web.xml`ファイルを解凍します
   * sling.run.modes パラメーターを publish に変更
   * sling.home 初期パラメーターをコメント解除し、必要に応じてこのパスを設定します（「概要」を参照）。
   * web.xml ファイルを再圧縮

* AEM war ファイルをアプリケーションとしてデプロイします（他の設定にはデフォルト設定を使用します）。
* インストールには時間がかかる場合があります。
* 上記の概要で説明した方法で、インストールが完了したことを確認します（error.log を追跡するなど）。
* コンテキストルートは、WebLogic `/console` の web アプリケーションの「設定」タブで変更できます。

#### Tomcat 8／8.5 {#tomcat}

デプロイ前に、上記の[概要](#general-description)をお読みください。

* **Tomcat サーバーの準備**

   * VM メモリ設定の値を増やします。

      * `bin/catalina.bat`（UNIX® の場合は `catalina.sh`）に、次の設定を追加します。
      * `set "JAVA_OPTS= -Xmx2048m`

   * Tomcat では、インストール時に管理者もマネージャーもアクセスできません。そのため、次のアカウントへのアクセスを許可するには `tomcat-users.xml` を手動で編集する必要があります。

      * `tomcat-users.xml` を編集して、管理者およびマネージャーのアクセスを含めます。設定は次の例のようになります。

        ```xml
        <?xml version='1.0' encoding='utf-8'?>
        <tomcat-users>
        role rolename="manager"/>
        role rolename="tomcat"/>
        <role rolename="admin"/>
        <role rolename="role1"/>
        <role rolename="manager-gui"/>
        <user username="both" password="tomcat" roles="tomcat,role1"/>
        <user username="tomcat" password="tomcat" roles="tomcat"/>
        <user username="admin" password="admin" roles="admin,manager-gui"/>
        <user username="role1" password="tomcat" roles="role1"/>
        </tomcat-users>
        ```

   * コンテキストルート「/」を使用して AEM をデプロイする場合は、既存の ROOT web アプリケーションのコンテキストルートを変更する必要があります。

      * ROOT web アプリケーションを停止してデプロイ解除します。
      * Tomcat の web アプリケーションフォルダーで ROOT.war フォルダーの名前を変更します。
      * Web アプリケーションを再起動します。

   * manager-gui を使用して AEM web アプリケーションをインストールする場合は、アップロードファイルの最大サイズを増やす必要があります。デフォルトで許可されているアップロードサイズは 50 MB のみです。これに対して、マネージャー web アプリケーションの web.xml を開き、

     `webapps/manager/WEB-INF/web.xml`

     max-file-size と max-request-size を 500 MB 以上に増やします。そのような `web.xml` ファイルの例として、次の `multipart-config` の例を参照してください。

     ```xml
     <multipart-config>
     <!-- 500MB max -->
     <max-file-size>524288000</max-file-size>
     <max-request-size>524288000</max-request-size>
     <file-size-threshold>0</file-size-threshold>
     </multipart-config>
     ```

* **AEM web アプリケーションのデプロイ**

   * AEM war ファイルをダウンロードします。
   * 必要に応じて、web.xml で設定します（上記の「概要」を参照）。

      * WEB-INF/web.xml ファイルを解凍します。
      * sling.run.modes パラメーターを publish に変更します。
      * sling.home 初期パラメーターをコメント解除し、必要に応じてこのパスを設定します。
      * web.xml ファイルを再圧縮します。

   * AEM war ファイルをルート Web アプリケーションとしてデプロイする場合は、名前を ROOT.war に変更します。 aemauthor をコンテキストルートにする場合は、aemauthor.war に名前を変更します。
   * Tomcat の webapps フォルダーにコピーします。
   * AEMがインストールされるまで待ちます。

## トラブルシューティング {#troubleshooting}

インストール時に発生する可能性のある問題の対処方法について詳しくは、以下を参照してください。

* [トラブルシューティング](/help/sites-deploying/troubleshooting.md)
