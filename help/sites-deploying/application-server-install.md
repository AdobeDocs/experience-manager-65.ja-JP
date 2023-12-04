---
title: アプリケーションサーバーのインストール
description: アプリケーションサーバーと共にAdobe Experience Managerをインストールする方法を説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
exl-id: 3a90f1d2-e53f-4cc4-8122-024ad6500de0
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '1168'
ht-degree: 39%

---

# アプリケーションサーバーのインストール{#application-server-install}

>[!NOTE]
>
>`JAR` および `WAR` は、Adobe Experience Manager(AEM) がリリースされたファイルタイプです。 これらのフォーマットは、Adobeがコミットしたサポートレベルに対応するため、品質保証中です。
>

この節では、Adobe Experience Manager(AEM) をアプリケーションサーバーと共にインストールする方法について説明します。 詳しくは、 [サポートされるプラットフォーム](/help/sites-deploying/technical-requirements.md#servlet-engines-application-servers) 個々のアプリケーションサーバーに対して提供される特定のサポートレベルについては、の節を参照してください。

以下のアプリケーションサーバーのインストール手順について説明します。

* [WebSphere](#websphere)
* [JBoss](#jboss-eap)
* [Oracle WebLogic 12.1.3／12.2](#oracle-weblogic)
* [Tomcat 8／8.5](#tomcat)

Web アプリケーションのインストール、サーバーの設定、サーバーの起動および停止方法について詳しくは、該当するアプリケーションサーバーのドキュメントを参照してください。

>[!NOTE]
>
>WAR デプロイメントでDynamic Mediaを使用している場合は、 [Dynamic Mediaドキュメント](/help/assets/config-dynamic.md#enabling-dynamic-media).

## 概要 {#general-description}

### アプリケーションサーバーに AEM をインストールするときのデフォルトの動作 {#default-behaviour-when-installing-aem-in-an-application-server}

AEMは、デプロイする単一の war ファイルとして提供されます。

デプロイすると、デフォルトで次の処理がおこなわれます。

* 実行モードは `author`
* インスタンス（リポジトリ、Felix OSGi 環境、バンドルなど）が `${user.dir}/crx-quickstart`場所 `${user.dir}` は現在の作業ディレクトリで、crx-quickstart へのこのパスは `sling.home`

* コンテキストルートは、war ファイル名です。例：  `aem-6`

#### 設定 {#configuration}

デフォルトの動作は、次の方法で変更できます。

* 実行モード：デプロイメント前に、AEM war ファイルの `sling.run.modes` ファイルで `WEB-INF/web.xml` パラメーターを設定

* sling.home：デプロイメント前に、AEM war ファイルの `WEB-INF/web.xml` ファイルで `sling.home` パラメーターを設定

* コンテキストルート：AEM war ファイル名を変更

#### パブリッシュインストール {#publish-installation}

パブリッシュインスタンスをデプロイするには、実行モードを publish に設定する必要があります。

* AEM war ファイルからWEB-INF/web.xmlを解凍します。
* sling.run.modes パラメーターを publish に変更します。
* web.xml ファイルをAEM war ファイルに再パック
* AEM war ファイルをデプロイします。

#### インストールの確認 {#installation-check}

すべてがインストールされているかどうかを確認するには、次の操作を行います。

* `error.log` ファイルに対して「テール」を実行して、すべてのコンテンツがインストールされていることを確認
* `/system/console` を調べて、すべてのバンドルがインストールされていることを確認

#### 同じアプリケーションサーバー上の 2 つのインスタンス {#two-instances-on-the-same-application-server}

デモ用に、1 つのアプリケーションサーバーにオーサーインスタンスとパブリッシュインスタンスをインストールするのが適切な場合があります。 その場合は、次の手順を実行します。

1. パブリッシュインスタンスの sling.home 変数と sling.run.modes 変数を変更します。
1. AEM war ファイルから WEB-INF/web.xml ファイルを展開します。
1. sling.home パラメーターを別のパスに変更します（絶対パスと相対パスが可能です）。
1. sling.run.modes を、パブリッシュインスタンス用に publish に変更します。
1. web.xml ファイルを再圧縮します。
1. war ファイルの名前を変更し、異なる名前を付けます。 例えば、ある名前を aemauthor.war に、別の名前を aempublish.war に変更します。
1. メモリ設定を高くします。 例えば、デフォルトのAEMインスタンスは `-Xmx3072m`
1. 2 つの Web アプリケーションをデプロイします。
1. デプロイ後に、2 つの Web アプリケーションを停止します。
1. オーサーインスタンスとパブリッシュインスタンスの両方で、sling.properties ファイルで property felix.service.urlhandlers=false が false に設定されていると仮定します（デフォルトでは true に設定）。
1. 2 つの Web アプリケーションを再度起動します。

## アプリケーションサーバーのインストール手順 {#application-servers-installation-procedures}

### WebSphere® 8.5 {#websphere}

デプロイメントの前に、上記の[概要](#general-description)をお読みください。

**サーバーの準備**

* Basic Auth ヘッダーを通す：

   * AEMでユーザーを認証する方法の 1 つは、WebSphere®サーバーのグローバル管理セキュリティを無効にする方法です。無効にするには、「Security/Global Security」に移動し、「Enable administrative security」チェックボックスをオフにして、サーバーを保存して再起動します。

* `"JAVA_OPTS= -Xmx2048m"` を設定
* コンテキスト root = /を使用してAEMをインストールする場合は、既存のデフォルト Web アプリケーションのコンテキストルートを変更します。

**AEM web アプリケーションのデプロイ**

* AEM war ファイルをダウンロードします。
* 必要に応じて web.xml で設定します（上記の「一般的な説明」を参照）。

   * WEB-INF/web.xml ファイルを解凍
   * sling.run.modes パラメーターを publish に変更
   * sling.home 初期パラメーターをコメント解除し、必要に応じてこのパスを設定
   * web.xml ファイルを再圧縮

* AEM war ファイルをデプロイします。

   * コンテキストルートを選択します（Sling 実行モードを設定する場合は、デプロイウィザードの詳細な手順を選択し、ウィザードの手順 6 で指定する必要があります）。

* AEM Web アプリケーションを起動します。

#### JBoss® EAP 6.3.0/6.4.0 {#jboss-eap}

デプロイメントの前に、上記の[概要](#general-description)をお読みください。

**JBoss®サーバーの準備**

設定ファイルにメモリ引数を設定する ( 例： `standalone.conf`)

* JAVA_OPTS=&quot;-Xms64m -Xmx2048m&quot;

deployment-scanner を使用してAEM Web アプリケーションをインストールする場合は、 `deployment-timeout,` そういうわけで `deployment-timeout` インスタンスの xml ファイル内の属性 ( 例： `configuration/standalone.xml)`:

```xml
<subsystem xmlns="urn:jboss:domain:deployment-scanner:1.1">
            <deployment-scanner path="deployments" relative-to="jboss.server.base.dir" scan-interval="5000" deployment-timeout="1000"/>
</subsystem>
```

**AEM web アプリケーションのデプロイ**

* AEM Web アプリケーションを JBoss® Administration Console にアップロードします。

* AEM web アプリケーションを有効にします。

#### Oracle WebLogic 12.1.3／12.2 {#oracle-weblogic}

デプロイメントの前に、上記の[概要](#general-description)をお読みください。

これは、管理サーバーのみを使用するシンプルなサーバーレイアウトを使用します。

**WebLogic Server の準備**

* `${myDomain}/config/config.xml` で、security-configuration セクションに以下を追加します。

   * `<enforce-valid-basic-auth-credentials>false</enforce-valid-basic-auth-credentials>`正確な位置については、[https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd](https://xmlns.oracle.com/weblogic/domain/1.0/domain.xsd) を参照してください（デフォルトではセクションの最後に追加すれば問題ありません）。

* VM メモリ設定の値を増やします。

   * 開く `${myDomain}/bin/setDomainEnv.cmd` (resp .sh) WLS_MEM_ARGS を検索し、例えば set を検索します。 `WLS_MEM_ARGS_64BIT=-Xms256m -Xmx2048m`
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

* AEM war ファイルをアプリケーションとしてデプロイします（他の設定ではデフォルト設定を使用します）。
* インストールには時間がかかる場合があります…
* 「一般説明」で前述したようにインストールが完了したことを確認します（error.log の追跡など）。
* コンテキストルートは、WebLogic `/console` の web アプリケーションの「設定」タブで変更できます。

#### Tomcat 8／8.5 {#tomcat}

デプロイ前に、上記の[概要](#general-description)をお読みください。

* **Tomcat サーバーの準備**

   * VM メモリ設定の値を増やします。

      * In `bin/catalina.bat` (resp `catalina.sh` (UNIX®の場合 ) 次の設定を追加します。
      * `set "JAVA_OPTS= -Xmx2048m`

   * Tomcat では、インストール時に admin や manager のアクセス権を無効にします。 そのため、手動で編集する必要があります `tomcat-users.xml` 次のアカウントへのアクセスを許可するには：

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

   * コンテキストルート「/」を使用してAEMをデプロイする場合は、既存の ROOT Web アプリのコンテキストルートを変更する必要があります。

      * ROOT Web アプリの停止とデプロイ解除
      * Tomcat の webapps フォルダーの ROOT.war フォルダーの名前を変更します。
      * Web アプリを再起動

   * manager-gui を使用してAEM Web アプリケーションをインストールする場合は、アップロードされたファイルの最大サイズを増やす必要があります。これは、デフォルトで許可されるアップロードサイズが 50 MB のみであるためです。 これに対して、マネージャー web アプリケーションの web.xml を開き、

     `webapps/manager/WEB-INF/web.xml`

     max-file-size と max-request-size を少なくとも 500 MB に増やします。次を参照してください。 `multipart-config` 例 `web.xml` ファイル。

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
   * 必要に応じて web.xml で設定します（上記の「一般的な説明」を参照）。

      * WEB-INF/web.xml ファイルを解凍
      * sling.run.modes パラメーターを publish に変更
      * sling.home 初期パラメーターをコメント解除し、必要に応じてこのパスを設定
      * web.xml ファイルを再圧縮

   * AEM war ファイルをルート Web アプリとしてデプロイする場合は、名前を ROOT.war に変更します。aemauthor をコンテキストルートとして使用する場合は、名前を aemauthor.war に変更します。
   * tomcat の webapps フォルダーにコピーします。
   * AEMがインストールされるまで待つ

## トラブルシューティング {#troubleshooting}

インストール時に発生する可能性のある問題の対処方法については、以下を参照してください。

* [トラブルシューティング](/help/sites-deploying/troubleshooting.md)
