---
title: Communities のデプロイ
description: Adobe Experience Managerにコミュニティとコミュニティ機能をデプロイする方法について説明します。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
docset: aem65
exl-id: 5b3d572d-e73d-4626-b664-c985949469c9
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1658'
ht-degree: 2%

---

# Communities のデプロイ {#deploying-communities}

## 前提条件 {#prerequisites}

* [AEM 6.5 Platform](/help/sites-deploying/deploy.md)

* AEM Communities ライセンス

* オプション ライセンス：

   * [Adobe Analytics for Communities の機能](/help/communities/analytics.md)
   * [MongoDB for MSRP](/help/communities/msrp.md)
   * [ASRP のAdobeクラウド](/help/communities/asrp.md)

## インストールチェックリスト {#installation-checklist}

**の場合 [AEM platform](/help/sites-deploying/deploy.md#what-is-aem)**

* 最新のをインストール [AEM 6.5 のアップデート](#aem64updates)

* デフォルトポート（4502、4503）を使用していない場合は、 [レプリケーションエージェントの設定](#replication-agents-on-author)
* [暗号鍵をレプリケートします](#replicate-the-crypto-key)
* グローバル化をサポートする場合、 [自動翻訳の設定](/help/sites-administering/translation.md)
（サンプル設定は開発用に提供）

**の場合 [Communities 機能](/help/communities/overview.md)**

* をデプロイする場合 [パブリッシングファーム](/help/sites-deploying/recommended-deploys.md#tarmk-farm), [プライマリパブリッシャーの識別](#primary-publisher)

* [トンネルサービスを有効にする](#tunnel-service-on-author)
* [ソーシャルログインを有効にする](/help/communities/social-login.md#adobe-granite-oauth-authentication-handler)
* [Adobe Analytics の設定](/help/communities/analytics.md)
* を設定 [デフォルトのメールサービス](/help/communities/email.md)
* ～の選択肢を特定する [共有 UGC ストレージ](/help/communities/working-with-srp.md) （**SRP**）

   * Mongodb SRP の場合 [（MSRP）](/help/communities/msrp.md)

      * [MongoDB のインストールと設定](/help/communities/msrp.md#mongodb-configuration)
      * [Solr の設定](/help/communities/solr.md)
      * [MSRP を選択](/help/communities/srp-config.md)

   * リレーショナルデータベース SRP の場合 [（DSRP）](/help/communities/dsrp.md)

      * [MySQL 用の JDBC ドライバーのインストール](#jdbc-driver-for-mysql)
      * [DSRP 用の MySQL のインストールと設定](/help/communities/dsrp-mysql.md)
      * [Solr の設定](/help/communities/solr.md)
      * [DSRP を選択](/help/communities/srp-config.md)

   * AdobeSRP の場合 [（ASRP）](/help/communities/asrp.md)

      * プロビジョニングについてはアカウント担当者に相談してください
      * [ASRP の選択](/help/communities/srp-config.md)

   * JCR SRP の場合 [（JSRP）](/help/communities/jsrp.md)

      * 共有 UGC （ユーザー生成コンテンツ）ストアではありません：

         * UGC はレプリケートされない
         * UGC は、入力されたAEM インスタンスまたはクラスターでのみ表示されます

         * デフォルトは JSRP です

## 最新リリース {#latest-releases}

AEM 6.5 Communities GA には、Communities パッケージが含まれています。 AEM 6.5 の更新の詳細 [コミュニティ](/help/release-notes/release-notes.md#experiencemanagercommunities)を参照してください。 [AEM 6.5 リリースノート](/help/release-notes/release-notes.md#communities-release-notes.html).

### AEM 6.5 のアップデート {#aem-updates}

AEM 6.4 以降、Communities のアップデートは、AEM累積修正パックおよびサービスパックの一部として提供されます。

AEM 6.5 の最新の更新については、次を参照してください。 [Adobe Experience Manager 6.4 累積修正パックおよびサービスパック](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates).

### バージョン履歴 {#version-history}

AEM 6.4 以降と同様、AEM Communitiesの機能およびホットフィックスは、AEM Communities累積修正パックおよびサービスパックの一部です。 したがって、個別の機能パックはありません。

### MySQL 用 JDBC ドライバー {#jdbc-driver-for-mysql}

Communities の 1 つの機能は、MySQL データベースを使用します。

* の場合 [DSRP](/help/communities/dsrp.md):UGC の保存

MySQL コネクタを個別に取得してインストールする必要があります。

必要な手順は次のとおりです。

1. から ZIP アーカイブをダウンロードします。 [https://dev.mysql.com/downloads/connector/j/](https://dev.mysql.com/downloads/connector/j/)

   * バージョンは 5.1.38 以上である必要があります

1. mysql-connector-java – を抽出する&lt;version>アーカイブの – bin.jar （バンドル）
1. Web コンソールを使用して、バンドルをインストールして起動します。

   * 例：https://localhost:4502/system/console/bundles
   * **`Install/Update`** を選択します。
   * 参照…して、ダウンロードした ZIP アーカイブから抽出したバンドルを選択します
   * を確認します *Oracle社の MySQLcom.mysql.jdbc 用 JDBC ドライバー* アクティブであり、アクティブでない場合は開始する（またはログを確認する）

1. JDBC を設定した後で既存のデプロイメントにをインストールする場合は、Web コンソールで JDBC 設定を再度保存して、新しいコネクタに JDBC を再バインドします。
   * 例：https://localhost:4502/system/console/configMgr
   * を見つける `Day Commons JDBC Connections Pool` 設定
   * 選択して開く
   * `Save` を選択します。

1. 手順 3 と 4 を、すべてのオーサーインスタンスとパブリッシュインスタンスで繰り返します

バンドルのインストールについて詳しくは、を参照してください。 [Web コンソール](/help/sites-deploying/web-console.md) ページ。

#### 例：インストールされている MySQL コネクタバンドル {#example-installed-mysql-connector-bundle}

![connector-bundle](assets/connector-bundle.png)



### AEMの高度な MLS {#aem-advanced-mls}

SRP コレクション（MSRP または DSRP）が詳細多言語検索（MLS）をサポートするには、カスタムスキーマと Solr 設定に加えて、新しい Solr プラグインが必要です。 必要な項目はすべて、ダウンロード可能な zip ファイルにパッケージ化されます。

高度な MLS ダウンロード（別名） `phasetwo`）は、Adobeリポジトリから使用できます。

* AEM-SOLR-MLS-phasetwo

  高度な MLS パッケージを入手するには、を参照してください。 [AEMの高度な MLS](deploy-communities.md#aem-advanced-mls) ドキュメントの「デプロイ」セクションで説明します。

   * バージョン 1.2.40、2016 年 4 月 6 日（Pt）
   * AEM-SOLR-MLS-phasetwo-1.2.40.zip のダウンロード

詳細およびインストール情報については、次を参照してください： [Solr 設定](/help/communities/solr.md) （SRP の場合）

### Package Share へのリンクについて {#about-links-to-package-share}

**Adobe AEM Cloud に表示されるパッケージ**

このページのパッケージへのリンクは、Package Share の場合と同様に、AEMの実行中のインスタンスを必要としません `adobeaemcloud.com`. パッケージは表示可能ですが、 `Install` ボタンは、Adobeがホストするサイトにパッケージをインストールするためのものです。 ローカルのAEM インスタンスにをインストールする場合は、を選択します。 `Install` 結果としてエラーが発生します。

**ローカル AEM インスタンスにをインストールする方法**

に表示されているパッケージをインストールするには `adobeaemcloud.com` ローカル AEM インスタンスでは、まずパッケージをローカルディスクにダウンロードする必要があります。

* 「」を選択します **アセット** タブ
* を選択 **ディスクにダウンロード**

ローカルのAEM インスタンスで、パッケージマネージャー（など）を使用します。 [https://localhost:4502/crx/packmgr/](https://localhost:4502/crx/packmgr/)）、ローカルのAEM パッケージリポジトリにアップロードします。

または、ローカル AEM インスタンスからパッケージ共有を使用してパッケージにアクセスします（例：） [https://localhost:4502/crx/packageshare/](https://localhost:4502/crx/packageshare/)）、 `Download` ボタンが、ローカルのAEM インスタンスのパッケージリポジトリにダウンロードされます。

ローカル AEM インスタンスのパッケージリポジトリに移動したら、パッケージマネージャーを使用してパッケージをインストールします。

詳しくは、次を参照してください [パッケージの使用方法](/help/sites-administering/package-manager.md#package-share).

## 推奨されるデプロイメント {#recommended-deployments}

AEM Communitiesでは、UGC の格納に使用される共通ストアが、 [ストレージリソースプロバイダー（SRP）](/help/communities/working-with-srp.md). 推奨されるデプロイメントは、共通ストアの SRP オプションの選択に重点を置いています。

共通ストアは、パブリッシュ環境での UGC のモデレートおよび分析をサポートし、以下を不要にします [複製](/help/communities/sync.md) （UGC の）。

* [コミュニティコンテンツストア](/help/communities/working-with-srp.md) :AEM Communitiesの SRP ストレージオプションについて説明します

* [推奨されるトポロジ](/help/communities/topologies.md) ：ユースケースと SRP の選択に応じて、使用するトポロジについて説明します

## アップグレード {#upgrading}

以前のバージョンのAEMからAEM 6.5 プラットフォームにアップグレードする場合は、以下を参照することが重要です。 [AEM 6.5 へのアップグレード](/help/sites-deploying/upgrade.md).

プラットフォームのアップグレードに加えて、次をお読みください [AEM Communities 6.5 へのアップグレード](/help/communities/upgrade.md) コミュニティの変更点について説明します。

## 設定 {#configurations}

### プライマリ発行者 {#primary-publisher}

選択したデプロイメントが [パブリッシュファーム](/help/communities/topologies.md#tarmk-publish-farm)を選択した場合は、1 つのAEM パブリッシュインスタンスをとして識別する必要があります。 **`primary publisher`** （すべてのインスタンスで発生するわけではないアクティビティの場合）。 に依存する機能などがその例です **通知** または **Adobe Analytics**.

デフォルトでは、 `AEM Communities Publisher Configuration` OSGi の設定には以下が設定されます。 **`Primary Publisher`** チェックボックスをオンにして、パブリッシュファーム内のすべてのパブリッシュインスタンスがプライマリとして自己識別されるようにします。

そのため、以下の操作が必要になります。 **すべてのセカンダリパブリッシュインスタンスの設定を編集します。** 「」をオフにする **`Primary Publisher`** チェックボックス。

![primary-publisher](assets/primary-publisher.png)

パブリッシュファーム内のその他すべての（セカンダリ）パブリッシュインスタンスの場合：

* 管理者権限でログイン
* へのアクセス [web コンソール](/help/sites-deploying/configuring-osgi.md)

   * 例： [https://localhost:4503/system/console/configMgr](https://localhost:4503/system/console/configMgr)

* を見つけます。 `AEM Communities Publisher Configuration`
* 編集アイコンを選択します
* 「」をオフにします **プライマリ発行者** box
* 「**保存**」を選択します

### オーサー環境のレプリケーションエージェント {#replication-agents-on-author}

レプリケーションは、コミュニティグループなど、パブリッシュ環境で作成されたサイトコンテンツや、を使用したオーサー環境からのメンバーおよびメンバーグループの管理に使用されます [トンネル サービス](#tunnel-service-on-author).

プライマリパブリッシャーについては、 [レプリケーションエージェントの設定](/help/sites-deploying/replication.md) 公開サーバーと承認済みユーザーを正しく識別します。 デフォルトの認証済みユーザー `admin,` には既に適切な権限があります（は次のメンバーです： `Communities Administrators`）に設定します。

他のユーザーが適切な権限を持つには、それらのユーザーがのメンバーとして追加される必要があります。 `administrators` ユーザーグループ （のメンバーでもある） `Communities Administrators`）に設定します。

オーサー環境には 2 つのレプリケーションエージェントがあり、トランスポート設定を正しく設定する必要があります。

* 作成者のレプリケーションコンソールにアクセスします

   * グローバルナビゲーションから、に移動します。 **[!UICONTROL ツール]** > **[!UICONTROL デプロイメント]** > **[!UICONTROL 複製]** > **[!UICONTROL オーサー環境のエージェント]**

* 両方のエージェントに対して同じ手順に従います。

   * **デフォルトエージェント（公開）**
   * **リバースレプリケーションエージェント（リバースパブリッシュ）**

      1. エージェントを選択
      1. を選択 **編集**
      1. 「」を選択します **0.48181894** タブ
      1. ポートでない場合 `4503`、を編集します **URI** 正しいポートを指定するには

      1. ユーザーでない場合 `admin`、を編集します **ユーザー** および **パスワード** のメンバーを指定 `administrators` ユーザーグループ

次のイメージは、ポートを 4503 から 6103 に変更した結果を示しています。

#### デフォルトエージェント（公開） {#default-agent-publish}

![default-agent-publish](assets/default-agent-publish.png)

#### リバースレプリケーションエージェント（リバースパブリッシュ） {#reverse-replication-agent-publish-reverse}

![reverse-replication-agent](assets/reverse-replication-agent.png)

### オーサーのトンネルサービス {#tunnel-service-on-author}

オーサー環境を使用して以下を行う場合 [サイトの作成](/help/communities/sites-console.md), [サイトのプロパティの変更](/help/communities/sites-console.md#modifying-site-properties) または [コミュニティメンバーの管理](/help/communities/members.md)オーサー環境に登録されたユーザーではなく、パブリッシュ環境に登録されたメンバー（ユーザー）にアクセスする必要があります。

トンネルサービスは、作成者のレプリケーションエージェントを使用してこのアクセスを提供します。

トンネル サービスを有効にするには：

* オーサーインスタンスに管理者権限でログインします。
* パブリッシャーが localhost:4503 でない場合、またはトランスポートユーザーが `admin`、次に [レプリケーションエージェントの設定](#replication-agents-on-author)

* へのアクセス [Web コンソール](/help/sites-deploying/configuring-osgi.md)

   * 例： [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)

* を見つけます。 `AEM Communities Publish Tunnel Service`
* 編集アイコンを選択します
* を確認します **enable** box
* 「**保存**」を選択します

  ![tunnel-service](assets/tunnel-service.png)

### 暗号鍵をレプリケート {#replicate-the-crypto-key}

AEM Communitiesには、すべてのAEM サーバーインスタンスが同じ暗号化キーを使用する必要がある 2 つの機能があります。 次のとおりです [Analytics](/help/communities/analytics.md) および [ASRP](/help/communities/asrp.md).

AEM 6.3 以降では、主要なマテリアルはファイルシステムに保存され、リポジトリには存在しなくなります。

オーサー環境からその他すべてのインスタンスに主要なマテリアルをコピーするには、次の手順を実行する必要があります。

* コピーする鍵データが含まれているAEM インスタンス（通常はオーサーインスタンス）にアクセスします

   * を見つけます。 `com.adobe.granite.crypto.file` ローカルファイルシステム内のバンドル（例：）

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21`
      * この `bundle.info` ファイルはバンドルを識別します

   * データフォルダー（例：）に移動します。

      * `<author-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

      * hmac ファイルとプライマリノードファイルをコピーします。

* 各ターゲット AEM インスタンス用

   * データフォルダー（例：）に移動します。

      * `<publish-aem-install-dir>/crx-quickstart/launchpad/felix/bundle21/data`

   * 以前にコピーした 2 つのファイルを貼り付けます
   * ～する必要がある。 [granite Crypto バンドルを更新します](#refresh-the-granite-crypto-bundle) ターゲット AEM インスタンスが実行中である場合

>[!CAUTION]
>
>暗号鍵に基づく別のセキュリティ機能が既に設定されている場合、暗号鍵をレプリケートすると、設定が破損する可能性があります。 サポートが必要な場合、 [カスタマーケアへのお問い合わせ](https://experienceleague.adobe.com/?support-solution=General&amp;lang=ja&amp;support-tab=home#support).

#### リポジトリのレプリケーション {#repository-replication}

AEM 6.2 以前と同様に、重要な資料をリポジトリに保存しておくと、保持できます。 システムプロパティを指定 `-Dcom.adobe.granite.crypto.file.disable=true` 各AEM インスタンスの最初の起動時（初期リポジトリを作成します）。

>[!NOTE]
>
>を確認します [オーサー環境のレプリケーションエージェント](#replication-agents-on-author) が正しく設定されている。

リポジトリに格納された鍵要素を使用して、オーサーインスタンスから他のインスタンスに暗号鍵をレプリケートする方法は次のとおりです。

使用 [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md):

* を参照 [https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de)
* `/etc/key` を選択します。
* 開く `Replication` タブ
* `Replicate` を選択します。

* [Granite Crypto バンドルを更新します](#refresh-the-granite-crypto-bundle)

  ![replicare-repository](assets/replicare-repository.png)

#### Granite Crypto バンドルを更新します {#refresh-the-granite-crypto-bundle}

* 各パブリッシュインスタンスで、にアクセスします。 [Web コンソール](/help/sites-deploying/configuring-osgi.md)

   * 例： [https://&lt;server>:&lt;port>/system/console/bundles](https://localhost:4503/system/console/bundles)

* を見つける `Adobe Granite Crypto Support` バンドル（com.adobe.granite.crypto）
* を選択 **更新**

  ![granite-crypto](assets/granite-crypto.png)

* しばらくすると、 **成功** ダイアログが表示されます。
  `Operation completed successfully.`

### Apache HTTP サーバー {#apache-http-server}

Apache HTTP サーバーを使用する場合は、関連するすべてのエントリに正しいサーバー名を使用していることを確認します。

特に、正しいサーバー名を使用するように注意してください `localhost`、内 `RedirectMatch`.

#### httpd.conf サンプル {#httpd-conf-sample}

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

* AEM [Dispatcher](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/aem-releases-updates) 詳細を見る
* [Dispatcher のインストール](https://experienceleague.adobe.com/en/docs/experience-manager-dispatcher/using/getting-started/dispatcher-install)
* [Communities 用の Dispatcher の設定](/help/communities/dispatcher.md)
* [既知の問題](/help/communities/troubleshooting.md#dispatcher-refetch-fails)

## 関連する Communities ドキュメント {#related-communities-documentation}

* 訪問 [コミュニティサイトの管理](/help/communities/administer-landing.md) コミュニティサイトの作成、コミュニティサイトテンプレートの設定、コミュニティコンテンツのモデレート、メンバーの管理およびメッセージングの設定について説明します。

* 訪問 [コミュニティの開発](/help/communities/communities.md) ここでは、ソーシャルコンポーネントフレームワーク（SCF）と、Communities のコンポーネントや機能のカスタマイズについて説明します。

* 訪問 [Communities コンポーネントのオーサリング](/help/communities/author-communities.md) コミュニティのコンポーネントを使用してオーサリングおよび設定する方法について説明します。
