---
title: アプリケーションサーバーのインストール
seo-title: アプリケーションサーバーのインストール
description: AEM をアプリケーションサーバーと共にインストールする方法を学習します。
seo-description: AEM をアプリケーションサーバーと共にインストールする方法を学習します。
uuid: c9571f80-6ed1-46fe-b7c3-946658dfc3f4
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 6fdce35d-2709-41cc-87fb-27a4b867e960
exl-id: 3a90f1d2-e53f-4cc4-8122-024ad6500de0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1175'
ht-degree: 61%

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
>WARデプロイメントでDynamic Mediaを使用している場合は、[Dynamic Mediaのドキュメント](/help/assets/config-dynamic.md#enabling-dynamic-media)を参照してください。

## General Description {#general-description}

### アプリケーションサーバーにAEMをインストールする際のデフォルトの動作{#default-behaviour-when-installing-aem-in-an-application-server}

AEM は、単一の war ファイルとしてデプロイされます。

デプロイすると、デフォルトで次のようになります。

* 実行モードは`author`です。
* インスタンス（リポジトリ、Felix OSGI環境、バンドルなど） が`${user.dir}/crx-quickstart`（`${user.dir}`は現在の作業ディレクトリ）にインストールされている場合、crx-quickstartへのこのパスは`sling.home`と呼ばれます。

* コンテキストルートは、warファイル名です。例：`aem-6`

#### 設定 {#configuration}

デフォルトの動作は次のように変更できます。

* 実行モード：デプロイメント前に、AEM war ファイルの `sling.run.modes` ファイルで `WEB-INF/web.xml` パラメーターを設定

* ：デプロイメント前に、AEM war ファイルの `sling.home` ファイルで `WEB-INF/web.xml`sling.home パラメーターを設定

* コンテキストルート：AEM war ファイル名を変更

#### パブリッシュインストール {#publish-installation}

パブリッシュインスタンスをデプロイするには、実行モードを publish に設定する必要があります。

* AEM war ファイルから WEB-INF/web.xml を展開
* sling.run.modes パラメーターを publish に変更
* web.xml ファイルを AEM war ファイルに再圧縮
* AEM war ファイルをデプロイします。

#### インストールの確認 {#installation-check}

すべてがインストールされているかどうかは、次の手順で確認します。

* `error.log` ファイルを追跡して、すべてのコンテンツがインストールされていることを確認
* `/system/console`を見て、すべてのバンドルがインストールされていることを確認します。

#### 同じアプリケーションサーバーに 2 つのインスタンス {#two-instances-on-the-same-application-server}

デモンストレーション目的で、オーサーインスタンスとパブリッシュインスタンスを 1 つのアプリケーションサーバーにインストールすることが適切な場合があります。そのためには、次の手順を実行します。

1. パブリッシュインスタンスのsling.home変数とsling.run.modes変数を変更します。
1. AEM warファイルからWEB-INF/web.xmlファイルを解凍します。
1. sling.home パラメーターを別のパス（絶対パスと相対パスが指定可能）に変更します。
1. パブリッシュインスタンスに対して、 sling.run.modesをpublishに変更します。
1. web.xmlファイルを再パックします。
1. warファイルの名前を変更します。例えば、1つはaemauthor.warに、もう1つはaempublish.warに名前を変更します。
1. より大きいメモリ設定を使用します。例えば、デフォルトのAEMインスタンスの場合は、次のように使用します。-Xmx3072m
1. 2 つの Web アプリケーションをデプロイします。
1. デプロイ後に、2 つの Web アプリケーションを停止します。
1. オーサーインスタンスとパブリッシュインスタンスの両方で、 sling.propertiesファイルで、プロパティfelix.service.urlhandlers=falseがfalseに設定されていることを確認します（デフォルトではtrueに設定されています）。
1. 2 つの Web アプリケーションを再度起動します。

## アプリケーションサーバーのインストール手順  {#application-servers-installation-procedures}

### WebSphere 8.5 {#websphere}

デプロイ前に、上記の[概要](#general-description)を読んでください。

**サーバーの準備**

* Basic 認証ヘッダーを無効にします。

   * AEM でユーザーを認証する方法の 1 つは、WebSphere サーバーのグローバル管理セキュリティを無効にすることです。これを行うには、Security／Global Security で「Enable administrative security」チェックボックスを解除し、保存して、サーバーを再起動します。

* set `"JAVA_OPTS= -Xmx2048m"`
* コンテキストルート = / を使用して AEM をインストールする場合は、まず既存のデフォルト Web アプリケーションのコンテキストルートを変更する必要があります。

**AEM Web アプリケーションのデプロイ**

* AEM war ファイルをダウンロードします。
* 必要に応じて、web.xml で設定します（上記の「概要」を参照）。

   * WEB-INF/web.xmlファイルを解凍します。
   * sling.run.modesパラメーターをpublishに変更
   * sling.homeの初期パラメーターのコメントを解除し、必要に応じてこのパスを設定します。
   * web.xmlファイルの再パック

* AEM war ファイルをデプロイします。

   * コンテキストルートを選択します（sling 実行モードを設定する場合は、デプロイウィザードの詳細な手順を選択し、ウィザードの手順 6 でコンテキストルートを指定する必要があります）。

* AEM Web アプリケーションを起動します。

#### JBoss EAP 6.3.0／6.4.0  {#jboss-eap}

デプロイ前に、上記の[概要](#general-description)を読んでください。

**JBoss サーバーの準備**

設定ファイル(例：`standalone.conf`)

* JAVA_OPTS=&quot;-Xms64m -Xmx2048m&quot;

deployment-scanner forを使用してAEM webアプリケーションをインストールする場合は、インスタンスのxmlファイルに`deployment-timeout`属性を設定する`deployment-timeout,`を増やすとよいでしょう(例：`configuration/standalone.xml)`:

```xml
<subsystem xmlns="urn:jboss:domain:deployment-scanner:1.1">
            <deployment-scanner path="deployments" relative-to="jboss.server.base.dir" scan-interval="5000" deployment-timeout="1000"/>
</subsystem>
```

**AEM Web アプリケーションのデプロイ**

* AEM WebアプリケーションをJBoss管理コンソールにアップロードします。

* AEM Webアプリケーションを有効にします。

#### Oracle WebLogic 12.1.3／12.2 {#oracle-weblogic}

デプロイ前に、上記の[概要](#general-description)を読んでください。

管理サーバーが 1 つだけのシンプルなサーバーレイアウトを使用します。

**WebLogic Server の準備**

* `${myDomain}/config/config.xml`で、security-configurationセクションに次を追加します。

   * `<enforce-valid-basic-auth-credentials>false</enforce-valid-basic-auth-credentials>` 正しい位置 [については、 https://xmlns.oracle.com/weblogic/domain/1.0/domain.](https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd) xsdを参照してください（デフォルトでは、セクションの最後に位置付けるのはokです）。

* VM メモリ設定の値を増やします。

   * `${myDomain}/bin/setDomainEnv.cmd` (resp .sh)を開き、WLS_MEM_ARGSを検索し、例えば`WLS_MEM_ARGS_64BIT=-Xms256m -Xmx2048m`を設定します。
   * WebLogic Serverの再起動

* `${myDomain}`内にパッケージフォルダーとcqフォルダー内にPlanフォルダーを作成します

**AEM Web アプリケーションのデプロイ**

* AEM war ファイルをダウンロードします。
* AEM warファイルを${myDomain}/packages/cqフォルダーに配置します。
* 必要に応じて`WEB-INF/web.xml`で設定します（上記の「一般説明」を参照）。

   * `WEB-INF/web.xml`ファイルを解凍します
   * sling.run.modesパラメーターをpublishに変更
   * sling.home初期パラメーターのコメントを解除し、必要に応じてこのパスを設定します（一般的な説明を参照）。
   * web.xmlファイルの再パック

* AEM war ファイルをアプリケーションとしてデプロイします（他の設定にはデフォルト設定を使用）。
* インストールには時間がかかる場合があります。
* 上記の「概要」で説明した方法で、インストールが完了したことを確認します（error.log を追跡するなど）。
* コンテキストルートは、WebLogicのWebアプリケーションの「Configuration」タブで変更できます。 `/console`

#### Tomcat 8／8.5 {#tomcat}

デプロイ前に、上記の[概要](#general-description)を読んでください。

* **Tomcat サーバーの準備**

   * VM メモリ設定の値を増やします。

      * `bin/catalina.bat`（UNIXの場合はresp `catalina.sh`）に次の設定を追加します。
      * `set "JAVA_OPTS= -Xmx2048m`
   * Tomcatでは、インストール時にadminアクセスもmanagerアクセスも使用できません。 したがって、これらのアカウントへのアクセスを許可するには、`tomcat-users.xml`を手動で編集する必要があります。

      * `tomcat-users.xml` を編集して、admin および manager のアクセスを含めます。設定は次の例のようになります。

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
   * manager-gui を使用して AEM Web アプリケーションをインストールする場合は、アップロードファイルの最大サイズを増やす必要があります。デフォルトで許可されているアップロードサイズは 50 MB のみです。これに対して、マネージャーWebアプリケーションのweb.xmlを開きます。

      `webapps/manager/WEB-INF/web.xml`

      max-file-sizeとmax-request-sizeを少なくとも500 MBに増やします。次の`multipart-config`の例を参照してください。 `web.xml`ファイルの例。

      ```xml
      <multipart-config>
      <!-- 500MB max -->
      <max-file-size>524288000</max-file-size>
      <max-request-size>524288000</max-request-size>
      <file-size-threshold>0</file-size-threshold>
      </multipart-config>
      ```




* **AEM Web アプリケーションのデプロイ**

   * AEM war ファイルをダウンロードします。
   * 必要に応じて、web.xml で設定します（上記の「概要」を参照）。

      * WEB-INF/web.xmlファイルを解凍します。
      * sling.run.modesパラメーターをpublishに変更
      * sling.homeの初期パラメーターのコメントを解除し、必要に応じてこのパスを設定します。
      * web.xmlファイルの再パック
   * AEM war ファイルは、ルート Web アプリケーションとしてデプロイする場合は ROOT.war に名前を変更し、aemauthor をコンテキストルートとする場合は aemauthor.war などに名前を変更します。
   * ファイルを Tomcat の webapps フォルダーにコピーします。
   * AEM がインストールされるまで待ちます。


## トラブルシューティング {#troubleshooting}

インストール中に発生する可能性のある問題の処理について詳しくは、以下を参照してください。

* [トラブルシューティング](/help/sites-deploying/troubleshooting.md)
