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
translation-type: tm+mt
source-git-commit: 4090b1641467c6fb02b2fcce4df97b9fd5da4e2f
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
>WAR導入でDynamic Mediaを使用している場合は、[Dynamic Mediaのドキュメント](/help/assets/config-dynamic.md#enabling-dynamic-media)を参照してください。

## General Description {#general-description}

### アプリケーションサーバー{#default-behaviour-when-installing-aem-in-an-application-server}にAEMをインストールする際のデフォルトの動作

AEM は、単一の war ファイルとしてデプロイされます。

デプロイすると、デフォルトで次のようになります。

* 実行モードは`author`です
* インスタンス(Repository、Felix OSGI環境、バンドルなど) が`${user.dir}/crx-quickstart`にインストールされています。`${user.dir}`は現在の作業ディレクトリです。このcrx-quickstartへのパスは`sling.home`と呼ばれます

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
* `/system/console`を見ると、すべてのバンドルがインストールされています

#### 同じアプリケーションサーバーに 2 つのインスタンス {#two-instances-on-the-same-application-server}

デモンストレーション目的で、オーサーインスタンスとパブリッシュインスタンスを 1 つのアプリケーションサーバーにインストールすることが適切な場合があります。そのためには、次の手順を実行します。

1. 発行インスタンスのsling.home変数とsling.run.modes変数を変更します。
1. AEM warファイルからWEB-INF/web.xmlファイルを解凍します。
1. sling.home パラメーターを別のパス（絶対パスと相対パスが指定可能）に変更します。
1. sling.run.modesを発行インスタンス用に発行に変更します。
1. web.xmlファイルを再パックします。
1. warファイルの名前を変更し、異なる名前にします。例えば、aemauthor.warに名前が変更され、aempublish.warに名前が変更されます。
1. より大きいメモリ設定を使用します。例えば、デフォルトのAEMインスタンスでは次のように使用します。-Xmx3072m
1. 2 つの Web アプリケーションをデプロイします。
1. デプロイ後に、2 つの Web アプリケーションを停止します。
1. 作成者インスタンスと発行インスタンスの両方で、sling.propertiesファイル内のプロパティfelix.service.urlhandlers=falseがfalseに設定されていることを保証します（デフォルトではtrueに設定されています）。
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

   * Unpack WEB-INF/web.xmlファイル
   * sling.run.modesパラメーターを発行に変更
   * sling.homeの初期パラメータのコメントを解除し、このパスを必要に応じて設定します。
   * web.xmlファイルの再パック

* AEM war ファイルをデプロイします。

   * コンテキストルートを選択します（sling 実行モードを設定する場合は、デプロイウィザードの詳細な手順を選択し、ウィザードの手順 6 でコンテキストルートを指定する必要があります）。

* AEM Web アプリケーションを起動します。

#### JBoss EAP 6.3.0／6.4.0  {#jboss-eap}

デプロイ前に、上記の[概要](#general-description)を読んでください。

**JBoss サーバーの準備**

confファイルにメモリ引数を設定します(例：`standalone.conf`)

* JAVA_OPTS=&quot;-Xms64m -Xmx2048m&quot;

deployment-scanner forを使用してAEM webアプリケーションをインストールする場合は、インスタンスのxmlファイルに`deployment-timeout`属性を設定する`deployment-timeout,`の値を増やすとよいでしょう(例： `configuration/standalone.xml)`:

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

* `${myDomain}/config/config.xml`security-configurationセクションに次を追加します。

   * `<enforce-valid-basic-auth-credentials>false</enforce-valid-basic-auth-credentials>` https://xmlns.oracle.com/weblogic/domain/1.0/domain. [](https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd) xsdで、正しい位置を確認します（初期設定では、セクションの最後に配置するのにok）。

* VM メモリ設定の値を増やします。

   * `${myDomain}/bin/setDomainEnv.cmd` (resp .sh)search for WLS_MEM_ARGSを開きます。例：`WLS_MEM_ARGS_64BIT=-Xms256m -Xmx2048m`
   * WebLogic Serverの再起動

* `${myDomain}`にパッケージフォルダーとcqフォルダー内、その中にPlanフォルダーを作成

**AEM Web アプリケーションのデプロイ**

* AEM war ファイルをダウンロードします。
* AEM warファイルを${myDomain}/packages/cqフォルダーに配置します
* 必要に応じて`WEB-INF/web.xml`に設定を行います（上記の「一般的な説明」を参照）

   * `WEB-INF/web.xml`ファイルを解凍
   * sling.run.modesパラメーターを発行に変更
   * sling.homeの最初のパラメーターのコメントを解除し、必要に応じてこのパスを設定します（一般的な説明を参照）。
   * web.xmlファイルの再パック

* AEM war ファイルをアプリケーションとしてデプロイします（他の設定にはデフォルト設定を使用）。
* インストールには時間がかかる場合があります。
* 上記の「概要」で説明した方法で、インストールが完了したことを確認します（error.log を追跡するなど）。
* コンテキストルートは、Webアプリケーションの「Configuration」タブのWebLogic `/console`で変更できます

#### Tomcat 8／8.5 {#tomcat}

デプロイ前に、上記の[概要](#general-description)を読んでください。

* **Tomcat サーバーの準備**

   * VM メモリ設定の値を増やします。

      * `bin/catalina.bat`（UNIXの場合はresp `catalina.sh`）に次の設定を追加します。
      * `set "JAVA_OPTS= -Xmx2048m`
   * Tomcatでは、インストール時に管理者とマネージャの両方のアクセスが有効になっていません。 したがって、`tomcat-users.xml`を手動で編集し、次のアカウントへのアクセスを許可する必要があります。

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
   * manager-gui を使用して AEM Web アプリケーションをインストールする場合は、アップロードファイルの最大サイズを増やす必要があります。デフォルトで許可されているアップロードサイズは 50 MB のみです。その場合は、マネージャーWebアプリケーションのweb.xmlを開き、

      `webapps/manager/WEB-INF/web.xml`

      max-file-sizeとmax-request-sizeを少なくとも500 MBに増やします。次の`multipart-config`例を参照してください。`web.xml`

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

      * Unpack WEB-INF/web.xmlファイル
      * sling.run.modesパラメーターを発行に変更
      * sling.homeの初期パラメータのコメントを解除し、このパスを必要に応じて設定します。
      * web.xmlファイルの再パック
   * AEM war ファイルは、ルート Web アプリケーションとしてデプロイする場合は ROOT.war に名前を変更し、aemauthor をコンテキストルートとする場合は aemauthor.war などに名前を変更します。
   * ファイルを Tomcat の webapps フォルダーにコピーします。
   * AEM がインストールされるまで待ちます。


## トラブルシューティング {#troubleshooting}

インストール中に発生する可能性のある問題の処理について詳しくは、以下を参照してください。

* [トラブルシューティング](/help/sites-deploying/troubleshooting.md)
