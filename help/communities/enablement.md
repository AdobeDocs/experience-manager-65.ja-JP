---
title: イネーブルメント機能の設定
seo-title: Configuring Enablement Features
description: Communities でイネーブルメント機能を設定します
seo-description: Configure enablement features in Communities
uuid: 27be3128-1a7d-412e-99a9-6e3b3b0aec1c
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 765a3d9b-4552-403e-872c-fdf684ac271d
role: Admin
exl-id: b635e2ed-4637-4b2f-a746-ec8dc7541bab
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 53%

---

# イネーブルメント機能の設定 {#configuring-enablement-features}

## 概要 {#overview}

イネーブルメント機能では、[イネーブルメントコミュニティ](overview.md#enablement-community)を作成できます。

* この機能を実稼動環境で使用するには、追加のライセンスが必要です。

イネーブルメント機能を使用するには、次の必要があります。

以下をインストールします。

* **SCORM**

   Sharable Content Object Reference Model（SCORM）とは、e ラーニングの標準規格および仕様です。コンテンツを転送可能な ZIP ファイルにパッケージ化する方法も定義しています。

* **MySQL**

    MySQL は、主に、イネーブルメントリソースの SCORM 追跡データおよびレポートデータや、ビデオの再生状況の追跡用テーブルを格納するために使用されるリレーショナルデータベースです。イネーブルメント機能パックで SCORM を使用するには、MySQL JDBC ドライバが必要です。

* **FFmpeg**

   FFmpeg はオーディオとビデオの変換およびストリーミングのためのソリューションです。インストールすると、[ビデオアセット](../../help/sites-authoring/default-components-foundation.md#video)の適切なトランスコーディングに使用できます。イネーブルメントコミュニティでは、オーサー環境で、アップロードしたリソースのメタデータを取得したり、リソースの一覧に表示するサムネイルを生成するときに FFmpeg を使用します。

以下をセットアップします。

* **コミュニティマネージャー**

   イネーブルメントコミュニティの場合、 `Community Enablement Managers` ユーザーグループには、 `Community Site Enablement Manager`（権限には、コンテンツの作成、割り当て、パブリッシュ環境でのメンバー管理などが含まれます）

オプションで以下を設定します。

* **Adobe Analytics**

   Adobe Analytics と統合することで、包括的なレポート機能が追加され、また Analytics に Video Heartbeat を追加できます。

* **Dispatcher**

## 設定手順 {#configuration-steps}

イネーブルコミュニティに必要な手順を以下に示します。

各手順は、必要な詳細が記されたドキュメントにリンクしています。

**すべてのオーサー／パブリッシュインスタンスで、次の手順を実行します。**

1. **[MySQL 用の JDBC ドライバーのインストール](deploy-communities.md#jdbc-driver-for-mysql)**

   Web コンソール（バンドル）を使用： *http://localhost:4502/system/console/bundles*

   インストール *前* SCORM パッケージのインストール

1. **[SCORM パッケージをインストール](deploy-communities.md#scorm-package)**


   パッケージマネージャを使用： *http://localhost:4502/crx/packmgr/*

**任意のサーバーで、次の手順を実行します。**

1. **[MySQL、MySQL Workbench のインストール](mysql.md)**

1. **[MySQL データベースのインストール](mysql.md#database-setup)**

   オーサーインスタンスからダウンロードした SQL スクリプトを実行

   MySQL Workbench の使用

**オーサーインスタンスをホストしている同じサーバーで、次の手順を実行します。**

1. **[FFmpeg のインストール](ffmpeg.md)**

**すべてのオーサー／パブリッシュインスタンスで、次の手順を実行します。**

1. **[JDBC 接続プールの設定](mysql.md#configure-jdbc-connections)**

   Web コンソール (configMgr) を使用： *http://localhost:4502/system/console/configMgr*

1. **[SCORM エンジンサービスの設定](mysql.md#aem-communities-scormengine-service)**

   Web コンソール (configMgr) を使用： *http://localhost:4502/system/console/configMgr*

1. **[CSRF フィルターの設定](mysql.md#adobe-granite-csrf-filter)**

   Web コンソール (configMgr) を使用： *http://localhost:4502/system/console/configMgr*

**オーサーインスタンスで、次の手順を実行します。**

1. (*オプション*) **[Analytics サービスを設定する](analytics.md)**

   ツール/デプロイメント/Cloud Servicesコンソールを使用します。 *http://localhost:4502/etc/cloudservices/sitecatalyst.html*

1. **[FFmpeg を設定](ffmpeg.md#configure-ffmpeg-transcoding-service)**

   ワークフロー/モデルコンソールの使用

1. **[トンネルサービスの有効化](deploy-communities.md#tunnel-service-on-author)**

   Web コンソール (configMgr) を使用： *http://localhost:4502/system/console/configMgr*

1. **[コミュニティ管理者を作成](users.md#creating-community-members)**

   オーサー環境の場合は、クラシック UI セキュリティコンソールを使用します。 *http://localhost:4502/useradmin*

   パス= /home/users/community を持つユーザーを作成

   * 次のグループにメンバーを追加します：

      * コミュニティイネーブルメントマネージャー
      * コミュニティ管理者

## Dispatcher {#dispatcher}

デプロイメントに次の条件が含まれる場合 [AEM Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=ja)イネーブルメント機能を正しく動作させるには、 `clientheader` および `filter` セクションは変更が必要です。 [コミュニティのための Dispatcher の設定](dispatcher.md#enablement)を参照してください。
