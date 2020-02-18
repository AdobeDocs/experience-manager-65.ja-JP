---
title: イネーブルメント機能の設定
seo-title: イネーブルメント機能の設定
description: Communities でイネーブルメント機能を設定します
seo-description: Communities でイネーブルメント機能を設定します
uuid: 27be3128-1a7d-412e-99a9-6e3b3b0aec1c
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 765a3d9b-4552-403e-872c-fdf684ac271d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# イネーブルメント機能の設定 {#configuring-enablement-features}

## 概要 {#overview}

イネーブルメント機能では、[イネーブルメントコミュニティ](overview.md#enablement-community)を作成できます。

* この機能を実稼働環境で使用するには、追加のライセンスが必要です。

イネーブルメント機能を使用するには、次の必要があります。

以下をインストールします。

* **SCORM** Sharable Content Object Reference Model（SCORM）は、e ラーニングの規格と仕様を集めたものです。SCORM では、コンテンツを転送可能な ZIP ファイルにパッケージ化する方法も定義されています。

* **MySQL** MySQL は、主に、イネーブルメントリソースの SCORM 追跡データおよびレポートデータや、ビデオの再生状況の追跡用テーブルを格納するために使用されるリレーショナルデータベースです。イネーブルメント機能パックで SCORM を使用するには、MySQL JDBC ドライバが必要です。

* **FFmpeg** FFmpeg はオーディオとビデオの変換およびストリーミングのためのソリューションです。インストールすると、[ビデオアセット](../../help/sites-authoring/default-components-foundation.md#video)の適切なトランスコーディングに使用できます。イネーブルメントコミュニティでは、オーサー環境で、アップロードしたリソースのメタデータを取得したり、リソースの一覧に表示するサムネイルを生成するときに FFmpeg を使用します。

以下をセットアップします。

* **コミュニティマ**&#x200B;ネージャーコミュニティを有効にする場合、ユーザーグループのメンバーのみにロールを割り当てることができます。権限には、公開環境でのコンテンツの作成、割り当て、メンバ `Community Enablement Managers``*Community Site* Enablement Manager`ー管理が含まれます。

オプションで以下を設定します。

* **Adobe Analytics** Adobe Analytics と統合することで、包括的なレポート機能が追加され、また Analytics に Video Heartbeat を追加できます。

* **Dispatcher**

## 設定手順 {#configuration-steps}

イネーブルコミュニティに必要な手順を以下に示します。

各手順は、必要な詳細が記されたドキュメントにリンクしています。

**すべてのオーサー／パブリッシュインスタンスで、次の手順を実行します。**

1. **[mysqlを使用Webコンソール用JDBCドライ](deploy-communities.md#jdbc-driver-for-mysql)**バーのインストール（バンドル）:*http://localhost:4502/system/console/bundles*Install *before install*before installing SCORM package

1. **[scormパッケージをインストール](deploy-communities.md#scorm-package)**Package Managerを使用します。http://localhost:4502/crx/packmgr/**

**任意のサーバーで、次の手順を実行します。**

1. **[MySQL、MySQL Workbench をインストール](mysql.md)**

1. **[mysqlデータベースのインストール](mysql.md#database-setup)**作成者インスタンスからダウンロードしたSQLスクリプトの実行MySQL Workbenchの使用

**オーサーインスタンスをホストしている同じサーバーで、次の手順を実行します。**

1. **[FFmpeg をインストール](ffmpeg.md)**

**すべてのオーサー／パブリッシュインスタンスで、次の手順を実行します。**

1. **[jdbc接続プールの設定](mysql.md#configure-jdbc-connections)**Webコンソールを使用(configMgr):http://localhost:4502/system/console/configMgr **

1. **[scormエンジンサービスの設定](mysql.md#aem-communities-scormengine-service)**Webコンソールを使用する(configMgr):http://localhost:4502/system/console/configMgr **

1. **[csrfフィルタの設定](mysql.md#adobe-granite-csrf-filter)**Webコンソールを使用(configMgr):http://localhost:4502/system/console/configMgr **

**オーサーインスタンスで、次の手順を実行します。**

1. (*optional*) **[configure Analytics service](analytics.md)**Use Tools, Deployment, Cloud Services console:*http://localhost:4502/etc/cloudservices/sitecatalyst.html*

1. **[fmpegUse Workflow](ffmpeg.md#configure-ffmpeg-transcoding-service)**/Modelsコンソールの設定

1. **[トンネルサービス](deploy-communities.md#tunnel-service-on-author)**Webコンソールを使用(configMgr)を有効にします。http://localhost:4502/system/console/configMgr **

1. **[コミュニティ管理者の作成](users.md#creating-community-members)**作成者環境では、クラシックUIセキュリティコンソールを使用します。*http://localhost:4502/useradmin*パス= /home/users/communityを使用してユーザーを作成

   * 次のグループにメンバーを追加します。

      * コミュニティイネーブルメントマネージャー
      * コミュニティ管理者

## Dispatcher {#dispatcher}

When the deployment includes [AEM&#39;s Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html), in order for the enablement features to work properly, the `clientheader`and `filter`sections need modification. [コミュニティのための Dispatcher の設定](dispatcher.md#enablement)を参照してください。
