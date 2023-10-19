---
title: Communities のデプロイ
description: Adobe Experience Managerでコミュニティとコミュニティ機能をデプロイする方法を説明します。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
docset: aem65
exl-id: 5b3d572d-e73d-4626-b664-c985949469c9
source-git-commit: 62d4a8b3af5031ccc539d78f7d06a8cd1fec7af1
workflow-type: tm+mt
source-wordcount: '1712'
ht-degree: 4%

---

# Communities のデプロイ {#deploying-communities}

## 前提条件 {#prerequisites}

* [AEM 6.5 Platform](/help/sites-deploying/deploy.md)

* AEM Communitiesライセンス

* オプションのライセンス：

   * [Adobe Analytics for Communities の機能](/help/communities/analytics.md)
   * [MSRP 用 MongoDB](/help/communities/msrp.md)
   * [ASRP 用Adobeクラウド](/help/communities/asrp.md)

## インストールチェックリスト {#installation-checklist}

**の [AEM platform](/help/sites-deploying/deploy.md#what-is-aem)**

* 最新のインストール [AEM 6.5 の更新](#aem64updates)

* デフォルトのポート (4502、4503) を使用しない場合は、 [レプリケーションエージェントの設定](#replication-agents-on-author)
* [暗号鍵のレプリケート](#replicate-the-crypto-key)
* グローバル化を支援する場合、 [自動翻訳の設定](/help/sites-administering/translation.md)
（開発用のサンプル設定が用意されています）。

**の [コミュニティ機能](/help/communities/overview.md)**

* をデプロイする場合、 [パブリッシュファーム](/help/sites-deploying/recommended-deploys.md#tarmk-farm), [主なパブリッシャーの特定](#primary-publisher)

* [トンネルサービスを有効にする](#tunnel-service-on-author)
* [ソーシャルログインを有効にする](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler)
* [Adobe Analytics の設定](/help/communities/analytics.md)
* を設定します。 [デフォルトの電子メールサービス](/help/communities/email.md)
* 選択肢の特定 [共有 UGC ストレージ](/help/communities/working-with-srp.md) (**SRP**)

   * MongoDB SRP の場合 [(MSRP)](/help/communities/msrp.md)

      * [MongoDB のインストールと設定](/help/communities/msrp.md#mongodb-configuration)
      * [Solr を設定](/help/communities/solr.md)
      * [MSRP を選択](/help/communities/srp-config.md)

   * リレーショナルデータベース SRP の場合 [(DSRP)](/help/communities/dsrp.md)

      * [MySQL 用の JDBC ドライバーのインストール](#jdbc-driver-for-mysql)
      * [DSRP 用の MySQL のインストールと設定](/help/communities/dsrp-mysql.md)
      * [Solr を設定](/help/communities/solr.md)
      * [DSRP を選択](/help/communities/srp-config.md)

   * AdobeSRP の場合 [(ASRP)](/help/communities/asrp.md)

      * プロビジョニングについては、アカウント担当者にお問い合わせください。
      * [ASRP を選択](/help/communities/srp-config.md)

   * JCR SRP の場合 [(JSRP)](/help/communities/jsrp.md)

      * 共有 UGC（ユーザー生成コンテンツ）ストアではありません：

         * UGC はレプリケートされません
         * UGC は、UGC が入力されたAEMインスタンスまたはクラスター上でのみ表示されます

         * デフォルトは JSRP です。

## 最新リリース {#latest-releases}

AEM 6.5 Communities GA には Communities パッケージが含まれています。 AEM 6.5 の更新の詳細を知るには [Communities](/help/release-notes/release-notes.md#experiencemanagercommunities)を参照し、 [AEM 6.5 リリースノート](/help/release-notes/release-notes.md#communities-release-notes.html).

### AEM 6.5 の更新 {#aem-updates}

AEM 6.4 以降、Communities の更新はAEM Cumulative Fix Packs および Service Pack の一部として提供されます。

AEM 6.5 の最新の更新については、 [Adobe Experience Manager 6.4 累積修正パックおよびサービスパック](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates.html?lang=ja).

### バージョン履歴 {#version-history}

AEM 6.4 以降と同様に、AEM Communitiesの機能とホットフィックスは、AEM Communitiesの累積修正パックおよびサービスパックの一部です。 したがって、別の機能パックはありません。

### MySQL 用 JDBC ドライバー {#jdbc-driver-for-mysql}

1 つのコミュニティ機能で MySQL データベースを使用する：

* の場合 [DSRP](/help/communities/dsrp.md):UGC の格納

MySQL コネクタを取得し、別途インストールする必要があります。

必要な手順は次のとおりです。

1. から ZIP アーカイブをダウンロードします。 [https://dev.mysql.com/downloads/connector/j/](https://dev.mysql.com/downloads/connector/j/)

   * バージョンは 5.1.38 以降である必要があります

1. mysql-connector-java — を抽出します&lt;version>アーカイブから —bin.jar (bundle)
1. Web コンソールを使用して、バンドルをインストールして起動します。

   * 例： https://localhost:4502/system/console/bundles
   * **`Install/Update`** を選択します。
   * ダウンロードした ZIP アーカイブから抽出したバンドルを参照して選択
   * 確認する *Oracle社の MySQLcom.mysql.jdbc 用 JDBC ドライバ* がアクティブで、アクティブでない場合は開始（またはログを確認）

1. JDBC の設定後に既存のデプロイメントにインストールする場合は、Web コンソールから JDBC 設定を再保存して、JDBC を新しいコネクタに再バインドします。
   * 例： https://localhost:4502/system/console/configMgr
   * 場所 `Day Commons JDBC Connections Pool` 設定
   * 選択して開く
   * `Save` を選択します。

1. すべてのオーサーインスタンスとパブリッシュインスタンスで、手順 3 と 4 を繰り返します。

バンドルのインストールに関する詳細は、 [Web コンソール](/help/sites-deploying/web-console.md) ページに貼り付けます。

#### 例：MySQL Connector バンドルのインストール {#example-installed-mysql-connector-bundle}

![connector-bundle](assets/connector-bundle.png)



### 高度な MLS のAEM {#aem-advanced-mls}

高度な多言語検索 (MLS) をサポートする SRP コレクション（MSRP または DSRP）については、カスタムスキーマと Solr 設定に加えて、新しい Solr プラグインが必要です。 必要な項目はすべて、ダウンロード可能な zip ファイルにパッケージ化されます。

高度な MLS のダウンロード ( 別名 `phasetwo`) は次の場所からAdobeで使用できます。

* AEM-SOLR-MLS-phasetwo

  高度な MLS パッケージを入手するには、 [高度な MLS のAEM](deploy-communities.md#aem-advanced-mls) （ドキュメントのデプロイ節）を参照してください。

   * バージョン 1.2.40、2016 年 4 月 7 日
   * AEM-SOLR-MLS-phasetwo-1.2.40.zip をダウンロードします。

詳細およびインストール情報については、 [Solr 設定](/help/communities/solr.md) （SRP 用）

### パッケージ共有へのリンクについて {#about-links-to-package-share}

**パッケージはAdobeAEM Cloud で表示**

このページのパッケージへのリンクでは、パッケージ共有を次の場所で使用する場合と同様に、AEMの実行インスタンスは必要ありません。 `adobeaemcloud.com`. パッケージが表示可能な間は、 `Install` ボタンは、パッケージをAdobe・ホスト・サイトにインストールするためのものです。 ローカルのAEMインスタンスにインストールする場合は、「 」を選択します。 `Install` の場合、エラーが発生します。

**ローカルのAEMインスタンスにインストールする方法**

に表示されるパッケージをインストールするには `adobeaemcloud.com` ローカルのAEMインスタンス上で、まずパッケージをローカルディスクにダウンロードする必要があります。

* を選択します。 **Assets** タブ
* 選択 **ディスクにダウンロード**

ローカルのAEMインスタンスで、パッケージマネージャーを使用します ( 例： [https://localhost:4502/crx/packmgr/](https://localhost:4502/crx/packmgr/)) をクリックして、ローカルのAEMパッケージリポジトリにアップロードします。

または、ローカルのAEMインスタンスからパッケージ共有を使用してパッケージにアクセスします ( 例： [https://localhost:4502/crx/packageshare/](https://localhost:4502/crx/packageshare/))、 `Download` ボタンをクリックすると、ローカルのAEMインスタンスのパッケージリポジトリにダウンロードされます。

ローカルのAEMインスタンスのパッケージリポジトリで、パッケージマネージャーを使用してパッケージをインストールします。

詳しくは、 [パッケージの操作方法](/help/sites-administering/package-manager.md#package-share).

## 推奨されるデプロイメント {#recommended-deployments}

AEM Communitiesでは、共通ストアは UGC の格納に使用され、多くの場合、 [ストレージリソースプロバイダー (SRP)](/help/communities/working-with-srp.md). 推奨されるデプロイメントは、共通ストアに対する SRP オプションの選択を中心に行われます。

共通ストアは、パブリッシュ環境で UGC のモデレートと分析をサポートし、 [複製](/help/communities/sync.md) UGC の

* [コミュニティコンテンツストア](/help/communities/working-with-srp.md) : AEM Communitiesの SRP ストレージオプションについて説明します。

* [推奨されるトポロジ](/help/communities/topologies.md) ：使用例と SRP の選択に応じて使用するトポロジについて説明します。

## アップグレード {#upgrading}

以前のバージョンのAEMからAEM 6.5 プラットフォームにアップグレードする場合は、次を読むことが重要です。 [AEM 6.5 へのアップグレード](/help/sites-deploying/upgrade.md).

プラットフォームのアップグレードに加えて、 [AEM Communities 6.5 へのアップグレード](/help/communities/upgrade.md) コミュニティの変更について学ぶには

## 設定 {#configurations}

### プライマリ発行者 {#primary-publisher}

選択したデプロイメントが [パブリッシュファーム](/help/communities/topologies.md#tarmk-publish-farm)その場合、1 つのAEMパブリッシュインスタンスを **`primary publisher`** すべてのインスタンスで発生すべきでないアクティビティの場合。 例えば、に依存する機能などです。 **通知** または **Adobe Analytics**.

デフォルトでは、 `AEM Communities Publisher Configuration` OSGi 設定は、 **`Primary Publisher`** チェックボックスをオンにして、パブリッシュファーム内のすべてのパブリッシュインスタンスがプライマリとして自己識別されるようにします。

したがって、次の操作が必要となります。 **すべてのセカンダリパブリッシュインスタンスで設定を編集** チェックを外す **`Primary Publisher`** チェックボックス。

![primary-publisher](assets/primary-publisher.png)

パブリッシュファーム内のその他（セカンダリ）パブリッシュインスタンスの場合：

* 管理者権限でサインイン
* 次にアクセス： [web コンソール](/help/sites-deploying/configuring-osgi.md)

   * 例： [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* 次を見つけます。 `AEM Communities Publisher Configuration`
* 編集アイコンを選択します。
* をオフにします。 **プライマリ発行者** ボックス
* 「**保存**」を選択します

### オーサー環境のレプリケーションエージェント {#replication-agents-on-author}

レプリケーションは、パブリッシュ環境で作成されたサイトコンテンツ（コミュニティグループなど）に対して使用され、 [トンネルサービス](#tunnel-service-on-author).

プライマリパブリッシャーの場合、 [レプリケーションエージェントの設定](/help/sites-deploying/replication.md) は、パブリッシュサーバーと認証済みユーザーを正しく識別します。 デフォルトの許可されたユーザー `admin,` は既に適切な権限を持っています ( は `Communities Administrators`) をクリックします。

他のユーザーが適切な権限を持つには、メンバーとして `administrators` ユーザーグループ ( `Communities Administrators`) をクリックします。

オーサー環境には 2 つのレプリケーションエージェントがあり、トランスポート設定を正しく設定する必要があります。

* オーサー環境のレプリケーションコンソールにアクセスする

   * グローバルナビゲーションから、に移動します。 **[!UICONTROL ツール]** > **[!UICONTROL 導入]** > **[!UICONTROL レプリケーション]** > **[!UICONTROL 作成者のエージェント]**

* 両方のエージェントで同じ手順を実行します。

   * **デフォルトエージェント (publish)**
   * **リバースレプリケーションエージェント（パブリッシュリバース）**

      1. エージェントを選択
      1. 選択 **編集**
      1. を選択します。 **輸送** タブ
      1. ポートでない場合は `4503`、 **URI** 正しいポートを指定するには

      1. ユーザーでない場合は次のようにします。 `admin`、 **ユーザー** および **パスワード** メンバを指定するには、 `administrators` ユーザーグループ

次の図は、ポートを 4503 から 6103 に変更した結果を示しています。

#### デフォルトエージェント (publish) {#default-agent-publish}

![default-agent-publish](assets/default-agent-publish.png)

#### リバースレプリケーションエージェント（パブリッシュリバース） {#reverse-replication-agent-publish-reverse}

![reverse-replication-agent](assets/reverse-replication-agent.png)

### オーサー環境のトンネルサービス {#tunnel-service-on-author}

オーサー環境を使用して [サイトの作成](/help/communities/sites-console.md), [サイトのプロパティを変更する](/help/communities/sites-console.md#modifying-site-properties) または [コミュニティメンバーの管理](/help/communities/members.md)オーサー環境に登録されているユーザーではなく、パブリッシュ環境に登録されているメンバー（ユーザー）にアクセスする必要があります。

トンネルサービスは、オーサー環境のレプリケーションエージェントを使用してこのアクセスを提供します。

トンネルサービスを有効にするには：

* オーサーインスタンス上での管理者権限でログインします。
* パブリッシャーが localhost:4503 でない場合、またはトランスポートユーザーが `admin`を、 [レプリケーションエージェントの設定](#replication-agents-on-author)

* 次にアクセス： [Web コンソール](/help/sites-deploying/configuring-osgi.md)

   * 例： [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

* 次を見つけます。 `AEM Communities Publish Tunnel Service`
* 編集アイコンを選択します。
* 次を確認します。 **有効** ボックス
* 「**保存**」を選択します

  ![トンネルサービス](assets/tunnel-service.png)

### 暗号鍵のレプリケート {#replicate-the-crypto-key}

AEM Communitiesには 2 つの機能があり、すべてのAEMサーバーインスタンスで同じ暗号化キーを使用する必要があります。 以下が該当します。 [Analytics](/help/communities/analytics.md) および [ASRP](/help/communities/asrp.md).

AEM 6.3 以降では、キー資料はファイルシステムに保存され、リポジトリには保存されなくなります。

オーサーインスタンスから他のすべてのインスタンスに主要な資料をコピーするには、次の操作が必要です。

* コピーする主要な資料を含むAEMインスタンス（通常はオーサーインスタンス）にアクセスします。

   * 次を見つけます。 `com.adobe.granite.crypto.file` ローカル・ファイル・システム内のバンドル。例：

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`
      * The `bundle.info` ファイルはバンドルを識別します。

   * データフォルダーに移動します（例： ）。

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

      * hmac ファイルとプライマリノードファイルをコピーする

* 各ターゲットAEMインスタンス

   * データフォルダーに移動します（例： ）。

      * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

   * 前にコピーした 2 つのファイルを貼り付けます。
   * ～する必要がある。 [Granite Crypto バンドルを更新します。](#refresh-the-granite-crypto-bundle) target AEMインスタンスが実行中の場合

>[!CAUTION]
>
>暗号鍵に基づく別のセキュリティ機能が既に設定されている場合は、暗号鍵をレプリケートすると設定に損害が生じる可能性があります。 サポートが必要な場合は、 [カスタマーケアに問い合わせる](https://experienceleague.adobe.com/?support-solution=General&amp;lang=ja&amp;support-tab=home#support).

#### リポジトリレプリケーション {#repository-replication}

AEM 6.2 以前の場合と同様に、鍵の素材をリポジトリに保存しておくと、保存できます。 システムプロパティを指定します。 `-Dcom.adobe.granite.crypto.file.disable=true` 各AEMインスタンスの初回起動時（最初のリポジトリを作成）。

>[!NOTE]
>
>次を確認します。 [オーサー環境のレプリケーションエージェント](#replication-agents-on-author) が正しく設定されている。

リポジトリに保存されたキー材料を使用して、オーサーから他のインスタンスに暗号キーをレプリケートする方法は次のとおりです。

使用 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md):

* 参照先 [https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de)
* `/etc/key` を選択します。
* 開く `Replication` タブ
* `Replicate` を選択します。

* [Granite 暗号バンドルを更新します。](#refresh-the-granite-crypto-bundle)

  ![replicare-repository](assets/replicare-repository.png)

#### Granite 暗号バンドルを更新します。 {#refresh-the-granite-crypto-bundle}

* 各パブリッシュインスタンスで、 [Web コンソール](/help/sites-deploying/configuring-osgi.md)

   * 例： [https://&lt;server>:&lt;port>/system/console/bundles](https://localhost:4503/system/console/bundles)

* 場所 `Adobe Granite Crypto Support` バンドル (com.adobe.granite.crypto)
* 選択 **更新**

  ![granite-crypto](assets/granite-crypto.png)

* しばらくすると、 **成功** ダイアログが表示されます。
  `Operation completed successfully.`

### Apache HTTP サーバー {#apache-http-server}

Apache HTTP サーバーを使用している場合は、関連するすべてのエントリに対して正しいサーバー名を使用していることを確認します。

特に、正しいサーバー名を使用するように注意してください。 `localhost`、 `RedirectMatch`.

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

Dispatcher を使用する場合は、以下を参照してください。

* AEM [Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=ja) ドキュメント
* [Dispatcher のインストール](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/getting-started/dispatcher-install.html?lang=en)
* [Communities 用の Dispatcher の設定](/help/communities/dispatcher.md)
* [既知の問題](/help/communities/troubleshooting.md#dispatcher-refetch-fails)

## 関連するコミュニティドキュメント {#related-communities-documentation}

* 訪問 [コミュニティサイトの管理](/help/communities/administer-landing.md) コミュニティサイトの作成、コミュニティサイトテンプレートの設定、コミュニティコンテンツのモデレート、メンバーの管理、メッセージングの設定について説明します。

* 訪問 [コミュニティの開発](/help/communities/communities.md) ここでは、ソーシャルコンポーネントフレームワーク (SCF) とコミュニティのコンポーネントおよび機能のカスタマイズについて学習できます。

* 訪問 [コミュニティコンポーネントのオーサリング](/help/communities/author-communities.md) ここでは、コミュニティコンポーネントを使用して作成および設定する方法について説明します。
