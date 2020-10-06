---
title: Communities のデプロイ
seo-title: Communities のデプロイ
description: AEM Communities のデプロイ方法
seo-description: AEM Communities のデプロイ方法
uuid: 18d9b424-004d-43b2-968a-318e27a93759
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: c8d7355f-5a70-40d1-bf22-62fab8002ea0
docset: aem65
translation-type: tm+mt
source-git-commit: 7c0834e9b70266e8b678771510fb1756c8091ea8
workflow-type: tm+mt
source-wordcount: '1891'
ht-degree: 35%

---


# Communities のデプロイ{#deploying-communities}

## 前提条件 {#prerequisites}

* [AEM 6.5 プラットフォーム](/help/sites-deploying/deploy.md)

* AEM Communities のライセンス

* オプションのライセンス：

   * [Adobe Analytics for Communities の機能](/help/communities/analytics.md)
   * [MongoDB for MSRP](/help/communities/msrp.md)
   * [Adobe Cloud for ASRP](/help/communities/asrp.md)

## インストールチェックリスト {#installation-checklist}

**AEMプラット[フォームの場合](/help/sites-deploying/deploy.md#what-is-aem)**:

* Install the latest [AEM 6.5 Updates](#aem64updates).

* If not using the default ports (4502, 4503), then [configure replication agents](#replication-agents-on-author).
* [暗号化キーの複製](#replicate-the-crypto-key)
* If supporting globalization, [setup automated translation](/help/sites-administering/translation.md)
(sample setup is provided for development).

**Communities機能[の場合](/help/communities/overview.md)**:

* [発行ファームを展開する場合](/help/sites-deploying/recommended-deploys.md#tarmk-farm)、主な発行者を [特定する](#primary-publisher)

* [トンネルサービスを有効にする](#tunnel-service-on-author)
* [ソーシャルログインを有効にする](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler)
* [Adobe Analytics の設定](/help/communities/analytics.md)
* [デフォルトの電子メールサービスの設定](/help/communities/email.md)
* [共有UGCストレージ](/help/communities/working-with-srp.md) (**SRP**)の選択肢の特定

   * If MongoDB SRP [(MSRP)](/help/communities/msrp.md)

      * [MongoDBのインストールと設定](/help/communities/msrp.md#mongodb-configuration)
      * [Solrの設定](/help/communities/solr.md)
      * [MSRP の選択](/help/communities/srp-config.md)
   * If relational database SRP [(DSRP)](/help/communities/dsrp.md)

      * [MySQL用JDBCドライバーのインストール](#jdbc-driver-for-mysql)
      * [DSRP用のMySQLのインストールと設定](/help/communities/dsrp-mysql.md)
      * [Solrの設定](/help/communities/solr.md)
      * [DSRP の選択](/help/communities/srp-config.md)
   * If Adobe SRP [(ASRP)](/help/communities/asrp.md)

      * プロビジョニングについては、アカウント担当者にお問い合わせください。
      * [ASRP の選択](/help/communities/srp-config.md)
   * If JCR SRP [(JSRP)](/help/communities/jsrp.md)

      * 共有されていないUGCストア：

         * UGC のレプリケーションなし.
         * UGCは、入力されたAEMインスタンスまたはクラスターでのみ表示されます。
      * デフォルトはJSRPです。

   イネーブルメント機能&#x200B;**[用](/help/communities/overview.md#enablement-community)**

   * [FFmpegのインストールと設定](/help/communities/ffmpeg.md)
   * [MySQL用JDBCドライバーのインストール](#jdbc-driver-for-mysql)
   * [AEM CommunitiesSCORM-Engineのインストール](#scorm-package)
   * [有効にするMySQLのインストールと設定](/help/communities/mysql.md)






## 最新リリース {#latest-releases}

AEM 6.5 Communities GA は、Communities パッケージと共に出荷されます。AEM 6.5 [Communities](/help/release-notes/release-notes.md#experiencemanagercommunities) のアップデートについて詳しくは、[AEM 6.5 リリースノート](/help/release-notes/release-notes.md#communities-release-notes.html)を参照してください。

### AEM 6.5 のアップデート {#aem-updates}

AEM 6.4 以降、Communities のアップデートは、AEM 累積修正パックおよびサービスパックの一部として提供されています。

For the latest updates to AEM 6.5, see [Adobe Experience Manager 6.4 Cumulative Fix Packs and Service Packs](https://helpx.adobe.com/jp/experience-manager/aem-releases-updates.html).

### バージョン履歴 {#version-history}

AEM 6.4 以降、AEM Communities 機能およびホットフィックスは、AEM Communities 累積修正パックおよびサービスパックの一部として提供されます。したがって、独立した機能パックは提供されません。

### MySQL 用 JDBC ドライバー {#jdbc-driver-for-mysql}

以下の 2 つの Communities 機能で MySQL データベースを使用しています。

* For [enablement](/help/communities/enablement.md): recording SCORM activities and learners
* For [DSRP](/help/communities/dsrp.md): storing user generated content (UGC)

MySQL コネクタを別途入手し、インストールする必要があります。

必要な手順は次のとおりです。

1. Download the ZIP archive from [https://dev.mysql.com/downloads/connector/j/](https://dev.mysql.com/downloads/connector/j/)

   * バージョンは5.1.38以上である必要があります

1. 抽出 `mysql-connector-java-&lt;version&gt;-bin.jar (bundle) from the archive`
1. Webコンソールを使用して、バンドルをインストールおよび開始します。

   * 例：https://localhost:4502/system/console/bundles
   *  **`Install/Update`**
   * ダウンロードした ZIP アーカイブから抽出したバンドルを参照し、選択します。
   * Check that *Oracle Corporation&#39;s JDBC Driver for MySQLcom.mysql.jdbc* is active, and start it if not (or check the logs)

1. JDBCの設定後に既存のデプロイメントにインストールする場合は、WebコンソールからJDBC設定を再保存して、JDBCを新しいコネクタに再バインドします。

   * 例：https://localhost:4502/system/console/configMgr
   * 設定を探し、 `Day Commons JDBC Connections Pool` 設定を開くよう選択します。
   *  `Save`.

1. すべてのオーサーインスタンスとパブリッシュインスタンスで手順3と4を繰り返します。

Further information on installing bundles is found on the [Web Console](/help/sites-deploying/web-console.md#bundles) page.

#### 例：インストール済みの MySQL コネクタバンドル {#example-installed-mysql-connector-bundle}

![](../assets/mysql-connector.png)

### SCORM パッケージ {#scorm-package}

Shareable Content Object Reference Model（SCORM）は、e ラーニングの標準規格と仕様をまとめた参照モデルです。SCORM では、コンテンツを転送可能な ZIP ファイルにパッケージ化する方法も定義されています。

AEM Communities SCORM エンジンは[イネーブルメント](/help/communities/overview.md#enablement-community)機能で必要になります。AEM 6.5 CommunitiesでサポートされるScormパッケージ：

* [cq-social-scorm-package、](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/social/scorm/cq-social-scorm-pkg) SCORM 2017.1 [](https://rusticisoftware.com/blog/scorm-engine-2017-released/) エンジンを含むバージョン2.3.7。

**SCORMパッケージをインストールするには**

1. パッケージ共有から [cq-social-scorm-package、バージョン2.3.7](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/social/scorm/cq-social-scorm-pkg) をインストールします。
1. Download `/libs/social/config/scorm/database_scormengine_data.sql` from cq instance and execute it in mysql server to create an upgraded scormEngineDB schema.
1. Add `/content/communities/scorm/RecordResults` in Excluded Paths property in CSRF filter from `https://<hostname>:<port>/system/console/configMgr` on publishers.

#### SCORM ロギング {#scorm-logging}

インストールすると、すべてのイネーブルメントアクティビティがシステムコンソールに詳細にロギングされます。

If desired, the log level can be set to WARN for the `RusticiSoftware.*` package.

For working with logs, see [Working with Audit Records and Log Files](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files).

### AEM の高度な MLS {#aem-advanced-mls}

SRP コレクション（MSRP または DSRP）で高度な多言語検索（MLS）をサポートするには、カスタムスキーマと Solr 設定に加えて、新しい Solr プラグインが必要です。必要な項目はすべて、ダウンロード可能なzipファイルにパッケージ化されます。

高度な MLS のダウンロード（「phasetwo」ともいう）は、アドビのリポジトリから入手できます。

* [AEM-SOLR-MLS-phasetwo](https://repo.adobe.com/nexus/content/repositories/releases/com/adobe/tat/AEM-SOLR-MLS-phasetwo/1.2.40/)

   * バージョン1.2.40、2016年4月7日
   * AEM-SOLR-MLS-phasetwo-1.2.40.zipをダウンロードします。

For details and installation information, visit [Solr Configuration](/help/communities/solr.md) for SRP.

### パッケージ共有へのリンクについて {#about-links-to-package-share}

**Adobe AEM クラウドでのパッケージの表示**

The links to packages on this page require no running instance of AEM as they are to package share on `adobeaemcloud.com`. While the packages are viewable, the `Install` button is for installing the packages into an Adobe hosted site. If intending to install on a local AEM instance, selecting `Install` will result in an error.

**ローカルの AEM インスタンスにインストールする方法**

To install the packages visible in `adobeaemcloud.com` on a local AEM instance, the package must first be downloaded to a local disk :

* Select the **Assets** tab
* Select **download to disk**

On the local AEM instance, use package manager (for example [https://localhost:4502/crx/packmgr/](https://localhost:4502/crx/packmgr/)), to upload to the local AEM&#39;s package repository.

Alternatively, accessing the package using package share from the local AEM instance (for example, [https://localhost:4502/crx/packageshare/](https://localhost:4502/crx/packageshare/)), the `Download` button will download to the local AEM instance&#39;s package repository.

ローカルAEMインスタンスのパッケージリポジトリに入ったら、パッケージマネージャーを使用してパッケージをインストールします。

For more information, visit [How to Work With Packages](/help/sites-administering/package-manager.md#package-share).

## 推奨されるデプロイメント {#recommended-deployments}

In AEM Communities, a common store is used to store user generated content (UGC) and is often referred to as the [storage resource provider (SRP)](/help/communities/working-with-srp.md). 推奨される展開は、共通ストアのSRPオプションの選択が中心です。

The common store supports moderation of, and analytics on, UGC in the publish environment while eliminating the need for [replication](/help/communities/sync.md) of UGC.

* [コミュニティコンテンツストア](/help/communities/working-with-srp.md)：AEM communities の SRP ストレージオプションについて説明します。

* [推奨されるトポロジ](/help/communities/topologies.md)：使用例や SRP オプションに応じて使用するトポロジについて説明します。

## アップグレード {#upgrading}

以前のバージョンの AEM から AEM 6.5 プラットフォームにアップグレードするときは、[AEM 6.5 へのアップグレード](/help/sites-deploying/upgrade.md)をお読みください。

プラットフォームのアップグレードについてだけでなく、[AEM Communities 6.5 へのアップグレード](/help/communities/upgrade.md)もお読みいただき、Communities の変更について学習してください。

## 設定 {#configurations}

### プライマリパブリッシャー {#primary-publisher}

When the deployment chosen is a [publish farm](/help/communities/topologies.md#tarmk-publish-farm), then one AEM publish instance must be identified as the **`primary publisher`** for activities which should not occur on all instances, such as features that rely on **notifications** or **Adobe Analytics**.

By default, the `AEM Communities Publisher Configuration` OSGi configuration is configured with the **`Primary Publisher`** check box checked, such that all publish instances in a publish farm would self-identify as the primary.

Therefore, it is necessary to **edit the configuration on all secondary publish instances** to uncheck the **`Primary Publisher`** check box.

![](../assets/primary-publisher.png)

パブリッシュファーム内の他のすべての（セカンダリ）パブリッシュインスタンスについて、以下をおこないます。

* 管理者権限でサインインする
* Access the [web console](/help/sites-deploying/configuring-osgi.md)

   * For example, [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* Folio Builder `AEM Communities Publisher Configuration`
* 編集アイコンを選択します
* Uncheck the **Primary Publisher** check box
* Select **Save**

### オーサー環境でのレプリケーションエージェント {#replication-agents-on-author}

Replication is used for site content created in the publish environment, such as community groups, as well as managing members and member groups from the author environment using the [tunnel service](#tunnel-service-on-author).

For the primary publisher, ensure the [Replication Agent Config](/help/sites-deploying/replication.md) correctly identifies the publish server and authorized user. The default authorized user, `admin` already has the appropriate permissions (is a member of `Communities Administrators`).

In order for some other user to have the appropriate permissions, they must be added as a member to the `administrators` user group (also a member of `Communities Administrators`).

オーサー環境には 2 つのレプリケーションエージェントがあり、正しく設定するにはトランスポート設定が必要です。

* 作成者のレプリケーションコンソールにアクセスする

   * From global navigation : **Tools, Deployment, Replication, Agents on author**

* 両方のエージェントに対して同じ手順を実行します。

   * **デフォルトエージェント（publish）**
   * **リバースレプリケーションエージェント（publish reverse）**

      1. エージェントを選択します。
      1. Select **edit**.
      1. Select the **Transport** tab
      1. If not port `4503`, edit the **URI** to specify the correct port.

      1. If not user `admin`, edit the **User** and **Password** to specify a member of the `administrators` user group.

以下の画像は、ポートを 4503 から 6103 に変更した結果を示しています。

#### デフォルトエージェント（publish） {#default-agent-publish}

![configure-limits](../assets/default-agent-publish.png)

#### リバースレプリケーションエージェント（publish reverse）{#reverse-replication-agent-publish-reverse}

![](../assets/reverse-replication-agent.png)

### オーサー環境のトンネルサービス {#tunnel-service-on-author}

When using the author environment to [create sites](/help/communities/sites-console.md), [modify site properties](/help/communities/sites-console.md#modifying-site-properties) or [manage community members](/help/communities/members.md), it is necessary to access members (users) registered in the publish environment, not users registered on author.

トンネルサービスは、作成者の複製エージェントを使用してこのアクセスを提供します。

トンネルサービスを有効にするには：

* On **author**, sign in with administrative privileges.
* If publisher is not localhost:4503 or transport user is not `admin`,
then [configure the replication agent](#replication-agents-on-author).

* Access the [Web Console](/help/sites-deploying/configuring-osgi.md)

   * For example, [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

* Folio Builder `AEM Communities Publish Tunnel Service`
* 編集アイコンを選択します
* Select the **enable** check box
* 「**Save**」を選択します。

![](../assets/tunnel-service.png)

### 暗号鍵のレプリケーション {#replicate-the-crypto-key}

AEM Communities には、すべての AEM サーバーインスタンスで同じ暗号鍵を使用する必要がある機能が 2 つあります。These are [Analytics](/help/communities/analytics.md) and [ASRP](/help/communities/asrp.md).

AEM 6.3以降、主要な資料はファイルシステムに保存され、リポジトリには保存されません。

オーサー環境から他のすべてのインスタンスに鍵の素材をコピーするには、以下の操作をおこなう必要があります。

* コピーする主要素材を含むAEMインスタンス（通常は作成者インスタンス）にアクセスします

   * Locate the `com.adobe.granite.crypto.file` bundle in the local file system

      例：

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`
      * The `bundle.info` file will identify the bundle
   * 例えば、データフォルダーに移動します。

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`
   * hmacおよびプライマリノードファイルをコピーします。



* 各ターゲットAEMインスタンスに対して

   * 例えば、データフォルダーに移動します。

      * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`
   * 以前にコピーした2つのファイルを貼り付けます
   * It is necessary to [refresh the Granite Crypto bundle](#refresh-the-granite-crypto-bundle) if the target AEM instance is currently running.


>[!CAUTION]
>
>既に暗号鍵に基づいて別のセキュリティ機能が設定されている場合、暗号鍵のレプリケーションをおこなうと設定が破損する可能性があります。For assistance, [contact customer care](https://helpx.adobe.com/jp/marketing-cloud/contact-support.html).


#### リポジトリのレプリケーション {#repository-replication}

AEM 6.2以前と同様に、主要なマテリアルをリポジトリに保存する場合は、各AEMインスタンスの初回起動時に次のシステムプロパティを指定することで保存できます（初期リポジトリを作成します）。

* `-Dcom.adobe.granite.crypto.file.disable=true`

>[!NOTE]
>
>It is important to verify that the [replication agent on author](#replication-agents-on-author) is correctly configured.


リポジトリに鍵の素材が格納されるので、オーサー環境から他のインスタンスへ暗号鍵をレプリケーションする方法は次のようになります。

[CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) を使用して、次の手順を実行します。

* Browse to [https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de)
*  `/etc/key`
* 「開く」 `Replication` タブ
*  `Replicate`

* [Granite 暗号バンドルを更新](#refresh-the-granite-crypto-bundle)します。

![](../assets/replicare-repository.png)

#### Granite 暗号バンドルの更新 {#refresh-the-granite-crypto-bundle}

* On each publish instance, access the [Web Console](/help/sites-deploying/configuring-osgi.md)

   * For example, [https://&lt;server>:&lt;port>/system/console/bundles](https://localhost:4503/system/console/bundles)

* バン `Adobe Granite Crypto Support` ドルの検索(com.adobe.granite.crypto)
* Select **Refresh**

![](../assets/refresh-granite-bundle.png)

* しばらくすると、 **成功** ダイアログが表示されます。
   `Operation completed successfully.`

### Apache HTTP サーバー {#apache-http-server}

Apache HTTP サーバーを使用する場合は、すべての関連エントリで正しいサーバー名を使用していることを確認してください。

In particular, be careful to use the correct server name, not `localhost`, in the `RedirectMatch`.

#### httpd.conf のサンプル {#httpd-conf-sample}

```shell
<IfModule alias_module>
     # XAMPP does not have a favicon; this prevents any 404 errors which may arise.
     Redirect 404 /favicon.ico
     <Location /favicon.ico>
         ErrorDocument 404 "No favicon"
     </Location>

    # Return from "Sign Out" generates response header directing you to "/", generating a 404 error
    # The RedirectMatch resolves it correctly when modified for the target Community Site :
    RedirectMatch ^/$ https://[server name]/content/sites/engage/en.html
 ...
 </IfModule>
```

### Dispatcher {#dispatcher}

Dispatcher を使用する場合は、次の説明を参照してください。

* AEM&#39;s [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html) documentation
* [Dispatcher のインストール](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-install.html)
* [Communities 用の Dispatcher の設定](/help/communities/dispatcher.md)
* [既知の問題](/help/communities/troubleshooting.md#dispatcher-refetch-fails)

## 関連するコミュニティドキュメント {#related-communities-documentation}

* コミュニティサイトの作成、コミュニティサイトテンプレートの設定、コミュニティコンテンツのモデレート、メンバーの管理およびメッセージングの設定については、[コミュニティサイトの管理](/help/communities/administer-landing.md)を参照してください。

* Visit [Developing Communities](/help/communities/communities.md) to learn about the social component framework (SCF) and customizing Communities components and features.

* Visit [Authoring Communities Components](/help/communities/author-communities.md) to learn how to author with and configure Communities components.

