---
title: アプリケーションサーバーのインストール
seo-title: Application Server Install
description: AEM をアプリケーションサーバーと共にインストールする方法を学習します。
seo-description: Learn how to install AEM with an application server.
uuid: c9571f80-6ed1-46fe-b7c3-946658dfc3f4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 6fdce35d-2709-41cc-87fb-27a4b867e960
exl-id: 3a90f1d2-e53f-4cc4-8122-024ad6500de0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '1163'
ht-degree: 100%

---

# アプリケーションサーバーのインストール{#application-server-install}

>[!NOTE]
>
>AEM がリリースされているファイル形式は `JAR` と `WAR` です。これらの形式に対しては、アドビが提供するサポートレベルを維持できるよう、品質保証プロセスが実施されています。

この節では、Adobe Experience Manager（AEM）をアプリケーションサーバーと共にインストールする方法について説明します。個々のアプリケーションサーバーに提供されているサポートのレベルについては、[サポートされているプラットフォーム](/help/sites-deploying/technical-requirements.md#servlet-engines-application-servers)を参照してください。

以下のアプリケーションサーバーのインストール手順について説明します。

* [WebSphere 8.5](#websphere)
* [JBoss EAP 6.3.0／6.4.0](#jboss-eap)
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
* インスタンス（リポジトリ、Felix OSGI 環境、バンドルなど）は `${user.dir}/crx-quickstart` にインストールされます。`${user.dir}` は現在の作業ディレクトリです。crx-quickstart へのこのパスは `sling.home` と呼ばれます。

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

デモンストレーション目的で、オーサーインスタンスとパブリッシュインスタンスを 1 つのアプリケーションサーバーにインストールすることが適切な場合があります。そのためには、次の手順を実行します。

1. パブリッシュインスタンスの sling.home 変数と sling.run.modes 変数を変更します。
1. AEM war ファイルから WEB-INF/web.xml ファイルを展開します。
1. sling.home パラメーターを別のパス（絶対パスと相対パスが指定可能）に変更します。
1. sling.run.modes を、パブリッシュインスタンス用に publish に変更します。
1. web.xml ファイルを再圧縮します。
1. war ファイルの名前を、別々の名前になるように変更します。例えば、一方を aemauthor.war に、もう一方を aempublish.war に変更します。
1. 高めのメモリ設定を使用します。例えば、デフォルトの AEM インスタンスの場合は、-Xmx3072m などを使用します。
1. 2 つの Web アプリケーションをデプロイします。
1. デプロイ後に、2 つの Web アプリケーションを停止します。
1. オーサーインスタンスとパブリッシュインスタンスの両方で、sling.properties ファイルで property felix.service.urlhandlers=false が false に設定されていると仮定します（デフォルトでは true に設定）。
1. 2 つの Web アプリケーションを再度起動します。

## アプリケーションサーバーのインストール手順 {#application-servers-installation-procedures}

### WebSphere 8.5 {#websphere}

デプロイメントの前に、上記の[概要](#general-description)をお読みください。

**サーバーの準備**

* Basic 認証ヘッダーを無効にします。

   * AEM でユーザーを認証する方法の 1 つは、WebSphere サーバーのグローバル管理セキュリティを無効にすることです。これを行うには、Security／Global Security で「Enable administrative security」チェックボックスを解除し、保存して、サーバーを再起動します。

* `"JAVA_OPTS= -Xmx2048m"` を設定
* コンテキストルート = / を使用して AEM をインストールする場合は、まず既存のデフォルト web アプリケーションのコンテキストルートを変更する必要があります

**AEM web アプリケーションのデプロイ**

* AEM war ファイルをダウンロードします。
* 必要に応じて、web.xml で設定します（上記の「概要」を参照）。

   * WEB-INF/web.xml ファイルを解凍
   * sling.run.modes パラメーターを publish に変更
   * sling.home 初期パラメーターをコメント解除し、必要に応じてこのパスを設定
   * web.xml ファイルを再圧縮

* AEM war ファイルをデプロイします。

   * コンテキストルートを選択します（sling 実行モードを設定する場合は、デプロイウィザードの詳細な手順を選択し、ウィザードの手順 6 でコンテキストルートを指定する必要があります）。

* AEM Web アプリケーションを起動します。

#### JBoss EAP 6.3.0／6.4.0 {#jboss-eap}

デプロイメントの前に、上記の[概要](#general-description)をお読みください。

**JBoss サーバーの準備**

設定ファイル（`standalone.conf` など）でメモリ引数を設定

* JAVA_OPTS=&quot;-Xms64m -Xmx2048m&quot;

deployment-scanner を使用して AEM web アプリケーションをインストールする場合は、`deployment-timeout,` の値を増やすことをお勧めします。そのためには、インスタンスの xml ファイル（`configuration/standalone.xml)` など）で `deployment-timeout` 属性を設定してください。

```xml
<subsystem xmlns="urn:jboss:domain:deployment-scanner:1.1">
            <deployment-scanner path="deployments" relative-to="jboss.server.base.dir" scan-interval="5000" deployment-timeout="1000"/>
</subsystem>
```

**AEM web アプリケーションのデプロイ**

* JBoss 管理コンソールで AEM web アプリケーションをアップロードします。

* AEM web アプリケーションを有効にします。

#### Oracle WebLogic 12.1.3／12.2 {#oracle-weblogic}

デプロイメントの前に、上記の[概要](#general-description)をお読みください。

管理サーバーが 1 つだけのシンプルなサーバーレイアウトを使用します。

**WebLogic Server の準備**

* `${myDomain}/config/config.xml` で、security-configuration セクションに以下を追加します。

   * `<enforce-valid-basic-auth-credentials>false</enforce-valid-basic-auth-credentials>`正確な位置については、[https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd](https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd) を参照してください（デフォルトではセクションの最後に追加すれば問題ありません）。

* VM メモリ設定の値を増やします。

   * `${myDomain}/bin/setDomainEnv.cmd`（resp .sh）を開いて WLS_MEM_ARGS を検索し、設定します（例：set `WLS_MEM_ARGS_64BIT=-Xms256m -Xmx2048m`）
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

* AEM war ファイルをアプリケーションとしてデプロイします（他の設定にはデフォルト設定を使用）。
* インストールには時間がかかる場合があります。
* 上記の「概要」で説明した方法で、インストールが完了したことを確認します（error.log を追跡するなど）。
* コンテキストルートは、WebLogic `/console` の web アプリケーションの「設定」タブで変更できます。

#### Tomcat 8／8.5 {#tomcat}

デプロイ前に、上記の[概要](#general-description)をお読みください。

* **Tomcat サーバーの準備**

   * VM メモリ設定の値を増やします。

      * `bin/catalina.bat`（Unix の場合は `catalina.sh`）に、次の設定を追加します。
      * `set "JAVA_OPTS= -Xmx2048m`
   * Tomcat では、インストール時に管理者もマネージャもアクセスできません。そのため、次のアカウントへのアクセスを許可するには `tomcat-users.xml` を手動で編集する必要があります。

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
   * コンテキストルート「/」を使用して AEM をデプロイする場合は、既存の ROOT Web アプリケーションのコンテキストルートを変更する必要があります。

      * ROOT Web アプリケーションを停止してデプロイ解除します。
      * Tomcat の webapps フォルダーで ROOT.war フォルダーの名前を変更します。
      * Web アプリケーションを再度起動します。
   * manager-gui を使用して AEM Web アプリケーションをインストールする場合は、アップロードファイルの最大サイズを増やす必要があります。デフォルトで許可されているアップロードサイズは 50 MB のみです。これに対して、マネージャー web アプリケーションの web.xml を開き、

      `webapps/manager/WEB-INF/web.xml`

      max-file-size と max-request-size を 500 MB 以上に増やします。そのような `web.xml` ファイルの例として、以下の `multipart-config` の例を参照してください。

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

      * WEB-INF/web.xml ファイルを解凍
      * sling.run.modes パラメーターを publish に変更
      * sling.home 初期パラメーターをコメント解除し、必要に応じてこのパスを設定
      * web.xml ファイルを再圧縮
   * AEM war ファイルは、ルート Web アプリケーションとしてデプロイする場合は ROOT.war に名前を変更し、aemauthor をコンテキストルートとする場合は aemauthor.war などに名前を変更します。
   * ファイルを Tomcat の webapps フォルダーにコピーします。
   * AEM がインストールされるまで待ちます。


## トラブルシューティング {#troubleshooting}

インストール中に発生する可能性のある問題の処理について詳しくは、以下を参照してください。

* [トラブルシューティング](/help/sites-deploying/troubleshooting.md)
