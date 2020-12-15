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
source-git-commit: 6693baecb1345c30385eb04caeb03960925f46c3
workflow-type: tm+mt
source-wordcount: '1898'
ht-degree: 36%

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

**[AEM プラットフォーム](/help/sites-deploying/deploy.md#what-is-aem)**&#x200B;用

* 最新の[AEM 6.5アップデート](#aem64updates)のインストール

* デフォルトのポート(4502、4503)を使用しない場合は、[レプリケーションエージェント](#replication-agents-on-author)を構成します
* [暗号化キーを複製します](#replicate-the-crypto-key)
* グローバル化をサポートする場合、[自動変換](/help/sites-administering/translation.md)を設定
（開発用にサンプルを設定）

**[Communities 機能](/help/communities/overview.md)**&#x200B;用

* [発行ファーム](/help/sites-deploying/recommended-deploys.md#tarmk-farm)を展開する場合、[主な発行者](#primary-publisher)を特定します

* [トンネルサービスを有効にする](#tunnel-service-on-author)
* [ソーシャルログインを有効にする](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler)
* [Adobe Analytics の設定](/help/communities/analytics.md)
* [デフォルトの電子メールサービス](/help/communities/email.md)を設定
* [共有UGCストレージ](/help/communities/working-with-srp.md) (**SRP**)の選択肢を特定

   * MongoDB SRP [(MSRP)](/help/communities/msrp.md)の場合

      * [MongoDBのインストールと設定](/help/communities/msrp.md#mongodb-configuration)
      * [Solrの設定](/help/communities/solr.md)
      * [MSRP の選択](/help/communities/srp-config.md)
   * リレーショナルデータベースSRP [(DSRP)](/help/communities/dsrp.md)の場合

      * [MySQL用JDBCドライバーのインストール](#jdbc-driver-for-mysql)
      * [DSRP用のMySQLのインストールと設定](/help/communities/dsrp-mysql.md)
      * [Solrの設定](/help/communities/solr.md)
      * [DSRP の選択](/help/communities/srp-config.md)
   * AdobeSRP [(ASRP)](/help/communities/asrp.md)の場合

      * プロビジョニングについては、アカウント担当者にお問い合わせください。
      * [ASRP の選択](/help/communities/srp-config.md)
   * JCR SRP [(JSRP)](/help/communities/jsrp.md)の場合

      * 共有されたUGCストアではありません：

         * UGC のレプリケーションなし
         * UGC はそれが入力された AEM インスタンスまたはクラスターでのみ表示

         * デフォルトはJSRPです。
   イネーブルメント機能&#x200B;**[用](/help/communities/overview.md#enablement-community)**

   * [FFmpegのインストールと設定](/help/communities/ffmpeg.md)
   * [MySQL用JDBCドライバーのインストール](#jdbc-driver-for-mysql)
   * [AEM CommunitiesSCORM-Engineのインストール](#scorm-package)
   * [有効にするMySQLのインストールと設定](/help/communities/mysql.md)





## 最新リリース {#latest-releases}

AEM 6.5 Communities GAにはCommunitiesパッケージが含まれます。 AEM 6.5 [Communities](/help/release-notes/release-notes.md#experiencemanagercommunities) のアップデートについて詳しくは、[AEM 6.5 リリースノート](/help/release-notes/release-notes.md#communities-release-notes.html)を参照してください。

### AEM 6.5 のアップデート {#aem-updates}

AEM 6.4 以降、Communities のアップデートは、AEM 累積修正パックおよびサービスパックの一部として提供されています。

AEM 6.5の最新のアップデートについては、[Adobe Experience Manager6.4累積修正パックとサービスパック](https://helpx.adobe.com/jp/experience-manager/aem-releases-updates.html)を参照してください。

### バージョン履歴 {#version-history}

AEM 6.4 以降、AEM Communities 機能およびホットフィックスは、AEM Communities 累積修正パックおよびサービスパックの一部として提供されます。したがって、独立した機能パックは提供されません。

### MySQL 用 JDBC ドライバー {#jdbc-driver-for-mysql}

以下の 2 つの Communities 機能で MySQL データベースを使用しています。

* [有効化](/help/communities/enablement.md)の場合：SCORMアクティビティと学習者の記録
* [DSRP](/help/communities/dsrp.md)の場合：ユーザー生成コンテンツの保存(UGC)

MySQL コネクタを別途入手し、インストールする必要があります。

必要な手順は次のとおりです。

1. [https://dev.mysql.com/downloads/connector/j/](https://dev.mysql.com/downloads/connector/j/)からZIPアーカイブをダウンロードします。

   * バージョンは5.1.38以上である必要があります

1. アーカイブからmysql-connector-java-&lt;version>-bin.jar（バンドル）を抽出します。
1. Webコンソールを使用して、バンドルをインストールおよび開始します。

   * 例：https://localhost:4502/system/console/bundles
   *  **`Install/Update`**
   * ダウンロードした ZIP アーカイブから抽出したバンドルを参照し、選択します。
   * *Oracle社のMySQLcom.mysql.jdbc*&#x200B;用JDBCドライバーがアクティブであることを確認し、アクティブでない場合は開始します（またはログを確認します）

1. JDBCの設定後に既存のデプロイメントにインストールする場合は、WebコンソールからJDBC設定を再保存して、JDBCを新しいコネクタに再バインドします。
   * 例：https://localhost:4502/system/console/configMgr
   * `Day Commons JDBC Connections Pool`構成を検索
   * 選択して開きます
   *  `Save`

1. すべてのオーサーインスタンスとパブリッシュインスタンスで手順3と4を繰り返します。

バンドルのインストールに関する詳細は、[Webコンソール](/help/sites-deploying/web-console.md)ページを参照してください。

#### 例：インストール済みの MySQL コネクタバンドル {#example-installed-mysql-connector-bundle}

![connector-bundle](assets/connector-bundle.png)

### SCORM パッケージ {#scorm-package}

Shareable Content Object Reference Model（SCORM）は、e ラーニングの標準規格と仕様をまとめた参照モデルです。SCORM では、コンテンツを転送可能な ZIP ファイルにパッケージ化する方法も定義されています。

AEM Communities SCORM エンジンは[イネーブルメント](/help/communities/overview.md#enablement-community)機能で必要になります。AEM 6.5 CommunitiesでサポートされるScormパッケージ：

* [cq-social-scorm-package、バージョン2.3.7](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/social/scorm/cq-social-scorm-pkg) ( [SCORM 2017.1](https://rusticisoftware.com/blog/scorm-engine-2017-released/) エンジンを含む)。

**SCORMパッケージをインストールするには**

1. パッケージ共有から[cq-social-scorm-package、バージョン2.3.7](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq650/social/scorm/cq-social-scorm-pkg)をインストールします。
1. cqインスタンスから`/libs/social/config/scorm/database_scormengine_data.sql`をダウンロードし、mysqlサーバーで実行して、アップグレードされたscormEngineDBスキーマを作成します。
1. パブリッシャーの追加`https://<hostname>:<port>/system/console/configMgr`からCSRFフィルターの除外されたパスプロパティの`/content/communities/scorm/RecordResults`。


#### SCORM ロギング {#scorm-logging}

インストールすると、すべてのイネーブルメントアクティビティがシステムコンソールに詳細にロギングされます。

必要に応じて、`RusticiSoftware.*`パッケージのログレベルをWARNに設定できます。

ログの操作については、[監査レコードとログファイルの操作](/help/sites-deploying/monitoring-and-maintaining.md#working-with-audit-records-and-log-files)を参照してください。

### AEM の高度な MLS {#aem-advanced-mls}

SRP コレクション（MSRP または DSRP）で高度な多言語検索（MLS）をサポートするには、カスタムスキーマと Solr 設定に加えて、新しい Solr プラグインが必要です。必要な項目はすべて、ダウンロード可能なzipファイルにパッケージ化されます。

高度な MLS のダウンロード（「phasetwo」ともいう）は、アドビのリポジトリから入手できます。

* [AEM-SOLR-MLS-phasetwo](https://repo.adobe.com/nexus/content/repositories/releases/com/adobe/tat/AEM-SOLR-MLS-phasetwo/1.2.40/)

   * バージョン1.2.40、2016年4月7日
   * AEM-SOLR-MLS-phasetwo-1.2.40.zipをダウンロードします。

詳細とインストール情報については、SRPの[Solr Configuration](/help/communities/solr.md)を参照してください。

### パッケージ共有へのリンクについて {#about-links-to-package-share}

**Adobe AEM クラウドでのパッケージの表示**

このページのパッケージへのリンクには、`adobeaemcloud.com`上のパッケージ共有を行うので、AEMの実行中のインスタンスは必要ありません。 パッケージは表示可能ですが、「`Install`」ボタンはAdobeがホストするサイトにパッケージをインストールするためのものです。 ローカルのAEMインスタンスにインストールする場合は、`Install`を選択するとエラーが発生します。

**ローカルの AEM インスタンスにインストールする方法**

`adobeaemcloud.com`に表示されるパッケージをローカルのAEMインスタンスにインストールするには、まずパッケージをローカルディスクにダウンロードする必要があります。

* 「**アセット**」タブを選択します
* **ディスク**&#x200B;にダウンロードを選択

ローカルAEMインスタンスで、パッケージマネージャー(例：[https://localhost:4502/crx/packmgr/](https://localhost:4502/crx/packmgr/))を使用して、ローカルのAEMパッケージリポジトリにアップロードします。

または、ローカルAEMインスタンスからパッケージ共有を使用してパッケージにアクセスする場合(例えば、[https://localhost:4502/crx/packageshare/](https://localhost:4502/crx/packageshare/))、「`Download`」ボタンを押すと、ローカルAEMインスタンスのパッケージリポジトリにダウンロードされます。

ローカルAEMインスタンスのパッケージリポジトリに入ったら、パッケージマネージャーを使用してパッケージをインストールします。

詳しくは、[パッケージの使い方](/help/sites-administering/package-manager.md#package-share)を参照してください。

## 推奨されるデプロイメント {#recommended-deployments}

AEM Communitiesでは、共通のストアはユーザー生成コンテンツ(UGC)の格納に使用され、[ストレージリソースプロバイダー(SRP)](/help/communities/working-with-srp.md)と呼ばれることがよくあります。 推奨される展開は、共通ストアのSRPオプションの選択が中心です。

共通ストアは、公開環境でのUGCのモデレートと解析をサポートし、UGCの[レプリケーション](/help/communities/sync.md)を不要にします。

* [コミュニティコンテンツストア](/help/communities/working-with-srp.md)：AEM communities の SRP ストレージオプションについて説明します。

* [推奨されるトポロジ](/help/communities/topologies.md)：使用例や SRP オプションに応じて使用するトポロジについて説明します。

## アップグレード  {#upgrading}

以前のバージョンの AEM から AEM 6.5 プラットフォームにアップグレードするときは、[AEM 6.5 へのアップグレード](/help/sites-deploying/upgrade.md)をお読みください。

プラットフォームのアップグレードについてだけでなく、[AEM Communities 6.5 へのアップグレード](/help/communities/upgrade.md)もお読みいただき、Communities の変更について学習してください。

## 設定 {#configurations}

### プライマリパブリッシャー {#primary-publisher}

選択した展開が[発行ファーム](/help/communities/topologies.md#tarmk-publish-farm)の場合、1つのAEM発行インスタンスを&#x200B;**`primary publisher`**&#x200B;として識別する必要があります。これは、**通知**&#x200B;や&#x200B;**Adobe Analytics**&#x200B;に依存する機能など、すべてのインスタンスで発生しません。

デフォルトでは、`AEM Communities Publisher Configuration` OSGi設定は&#x200B;**`Primary Publisher`**&#x200B;チェックボックスをオンにして設定され、パブリッシュファーム内のすべてのパブリッシュインスタンスがプライマリとして自己識別されます。

したがって、すべてのセカンダリパブリッシュインスタンスの設定を編集して、「」チェックボックスをオフにする必要があります。******`Primary Publisher`**

![主版出版社](assets/primary-publisher.png)

パブリッシュファーム内の他のすべての（セカンダリ）パブリッシュインスタンスについて、以下をおこないます。

* 管理者権限を持つログイン
* [Webコンソール](/help/sites-deploying/configuring-osgi.md)にアクセス

   * 例：[https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* `AEM Communities Publisher Configuration`
* 編集アイコンを選択します
* 「**プライマリパブリッシャ**」ボックスのチェックを外します。
* **保存**&#x200B;を選択

### オーサー環境でのレプリケーションエージェント {#replication-agents-on-author}

レプリケーションは、コミュニティグループなどの発行環境で作成されるサイトコンテンツに使用され、[tunnel service](#tunnel-service-on-author)を使用して作成者環境からメンバーとメンバーグループを管理します。

プライマリパブリッシャーの場合は、[レプリケーションエージェント構成](/help/sites-deploying/replication.md)がパブリッシュサーバーと認証済みユーザーを正しく識別していることを確認します。 デフォルトの許可されたユーザー`admin,`は、既に適切な権限を持っています（`Communities Administrators`のメンバーです）。

他のユーザーが適切な権限を持つには、`administrators`ユーザーグループ（`Communities Administrators`のメンバーも含む）のメンバーとして追加する必要があります。

オーサー環境には 2 つのレプリケーションエージェントがあり、正しく設定するにはトランスポート設定が必要です。

* 作成者のレプリケーションコンソールにアクセスする

   * グローバルナビゲーションから、**[!UICONTROL ツール]**/**[!UICONTROL 導入]**/**[!UICONTROL レプリケーション]**/**[!UICONTROL 作成者]**&#x200B;のエージェントに移動します。

* 両方のエージェントに対して同じ手順を実行します。

   * **デフォルトエージェント（publish）**
   * **リバースレプリケーションエージェント（publish reverse）**

      1. エージェントの選択
      1. **編集**&#x200B;を選択
      1. 「**トランスポート**」タブを選択します
      1. ポート`4503`でない場合は、**URI**&#x200B;を編集して正しいポートを指定します

      1. ユーザー`admin`でない場合は、**ユーザー**&#x200B;と&#x200B;**パスワード**&#x200B;を編集して、`administrators`ユーザーグループのメンバーを指定します

以下の画像は、ポートを 4503 から 6103 に変更した結果を示しています。

#### デフォルトエージェント（発行） {#default-agent-publish}

![default-agent-publish](assets/default-agent-publish.png)

#### リバースレプリケーションエージェント（publish reverse）{#reverse-replication-agent-publish-reverse}

![逆複製エージェント](assets/reverse-replication-agent.png)

### オーサー環境のトンネルサービス {#tunnel-service-on-author}

作成者環境を使用してサイトの作成](/help/communities/sites-console.md)、[サイトのプロパティの変更](/help/communities/sites-console.md#modifying-site-properties)、または[コミュニティメンバーの管理](/help/communities/members.md)を行う場合は、作成者に登録された環境ではなく、公開ユーザーにアクセスする必要があります。[

トンネルサービスは、作成者の複製エージェントを使用してこのアクセスを提供します。

トンネルサービスを有効にするには：

* 作成者インスタンスに対する管理者権限でログインします。
* パブリッシャーがlocalhost:4503でない場合、またはトランスポートユーザーが`admin`でない場合、
[レプリケーションエージェントを構成](#replication-agents-on-author)

* [Webコンソール](/help/sites-deploying/configuring-osgi.md)にアクセス

   * 例：[https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

* `AEM Communities Publish Tunnel Service`
* 編集アイコンを選択します
* **enable**&#x200B;ボックスをチェック
* **保存**&#x200B;を選択

   ![トンネルサービス](assets/tunnel-service.png)

### 暗号鍵のレプリケーション {#replicate-the-crypto-key}

AEM Communities には、すべての AEM サーバーインスタンスで同じ暗号鍵を使用する必要がある機能が 2 つあります。これらは[Analytics](/help/communities/analytics.md)と[ASRP](/help/communities/asrp.md)です。

AEM 6.3以降、主要な資料はファイルシステムに保存され、リポジトリには保存されません。

オーサー環境から他のすべてのインスタンスに鍵の素材をコピーするには、以下の操作をおこなう必要があります。

* コピーする主要素材を含むAEMインスタンス（通常は作成者インスタンス）にアクセスします

   * ローカルファイルシステムの`com.adobe.granite.crypto.file`バンドルを探します。
例えば、

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`
      * `bundle.info`ファイルがバンドルを識別します
   * データフォルダーに移動し、
例えば、

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

      * hmacおよびプライマリ・ノード・ファイルのコピー


* 各ターゲットAEMインスタンスに対して

   * データフォルダーに移動し、
例えば、

      * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`
   * 以前にコピーした2つのファイルを貼り付けます
   * ターゲットAEMインスタンスが現在実行中の場合は、Granite Cryptoバンドル](#refresh-the-granite-crypto-bundle)を[更新する必要があります


>[!CAUTION]
>
>既に暗号鍵に基づいて別のセキュリティ機能が設定されている場合、暗号鍵のレプリケーションをおこなうと設定が破損する可能性があります。援助が必要な場合は、[カスタマーケア](https://helpx.adobe.com/jp/marketing-cloud/contact-support.html)にお問い合わせください。

#### リポジトリのレプリケーション {#repository-replication}

AEM 6.2以前と同様に、主要なマテリアルをリポジトリに保存する場合は、各AEMインスタンスの初回起動時に次のシステムプロパティを指定することで保存できます（初期リポジトリを作成します）。

* `-Dcom.adobe.granite.crypto.file.disable=true`

>[!NOTE]
>
>作成者](#replication-agents-on-author)の[レプリケーションエージェントが正しく構成されていることを確認することが重要です。

リポジトリに鍵の素材が格納されるので、オーサー環境から他のインスタンスへ暗号鍵をレプリケーションする方法は次のようになります。

[CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) を使用して、次の手順を実行します。

* [https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de)を参照します。
*  `/etc/key`
* `Replication`タブを開く
*  `Replicate`

* [Granite Cryptoバンドルの更新](#refresh-the-granite-crypto-bundle)

   ![replicare-repository](assets/replicare-repository.png)

#### Granite 暗号バンドルの更新 {#refresh-the-granite-crypto-bundle}

* 各発行インスタンスで、[Webコンソール](/help/sites-deploying/configuring-osgi.md)にアクセスします

   * 例：[https://&lt;server>:&lt;port>/system/console/bundles](https://localhost:4503/system/console/bundles)

* `Adobe Granite Crypto Support`バンドルを検索(com.adobe.granite.crypto)
* **更新**&#x200B;を選択

   ![花崗岩暗号の](assets/granite-crypto.png)

* しばらくすると、**成功**ダイアログが表示されます。
   `Operation completed successfully.`

### Apache HTTP サーバー {#apache-http-server}

Apache HTTP サーバーを使用する場合は、すべての関連エントリで正しいサーバー名を使用していることを確認してください。

特に、`RedirectMatch`内では`localhost`ではなく正しいサーバー名を使用するように注意してください。

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

* AEM [ディスパッチャー](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html)ドキュメント
* [Dispatcher のインストール](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher-install.html)
* [Communities 用の Dispatcher の設定](/help/communities/dispatcher.md)
* [既知の問題](/help/communities/troubleshooting.md#dispatcher-refetch-fails)

## 関連するコミュニティドキュメント  {#related-communities-documentation}

* コミュニティサイトの作成、コミュニティサイトテンプレートの設定、コミュニティコンテンツのモデレート、メンバーの管理およびメッセージングの設定については、[コミュニティサイトの管理](/help/communities/administer-landing.md)を参照してください。

* Social Component Framework(SCF)とCommunitiesのコンポーネントと機能のカスタマイズについては、[Developing Communities](/help/communities/communities.md)を参照してください。

* Communitiesコンポーネントの作成方法と設定方法については、[Authoring Communities Components](/help/communities/author-communities.md)を参照してください。

