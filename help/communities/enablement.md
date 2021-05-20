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
role: Administrator
exl-id: b635e2ed-4637-4b2f-a746-ec8dc7541bab
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '447'
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

   イネーブルメントコミュニティの場合、`Community Enablement Managers`ユーザーグループのメンバーのみが`Community Site Enablement Manager`の役割を割り当てることができます。この役割には、パブリッシュ環境でのコンテンツの作成、割り当て、メンバー管理の権限が含まれます。

オプションで以下を設定します。

* **Adobe Analytics**

   Adobe Analytics と統合することで、包括的なレポート機能が追加され、また Analytics に Video Heartbeat を追加できます。

* **Dispatcher**

## 設定手順 {#configuration-steps}

イネーブルコミュニティに必要な手順を以下に示します。

各手順は、必要な詳細が記されたドキュメントにリンクしています。

**すべてのオーサー／パブリッシュインスタンスで、次の手順を実行します。**

1. **[MySQL用のJDBCドライバーのインストール](deploy-communities.md#jdbc-driver-for-mysql)**

   Webコンソール（バンドル）を使用します。*http://localhost:4502/system/console/bundles*

   SCORMパッケージをインストールする&#x200B;*前に*&#x200B;をインストールします。

1. **[SCORMパッケージのインストール](deploy-communities.md#scorm-package)**


   パッケージマネージャーを使用：*http://localhost:4502/crx/packmgr/*

**任意のサーバーで、次の手順を実行します。**

1. **[MySQL、MySQL Workbenchのインストール](mysql.md)**

1. **[MySQLデータベースのインストール](mysql.md#database-setup)**

   オーサーインスタンスからダウンロードしたSQLスクリプトの実行

   MySQL Workbenchの使用

**オーサーインスタンスをホストしている同じサーバーで、次の手順を実行します。**

1. **[FFmpeg のインストール](ffmpeg.md)**

**すべてのオーサー／パブリッシュインスタンスで、次の手順を実行します。**

1. **[JDBC接続プールの設定](mysql.md#configure-jdbc-connections)**

   Webコンソール(configMgr)を使用：*http://localhost:4502/system/console/configMgr*

1. **[SCORMエンジンサービスの設定](mysql.md#aem-communities-scormengine-service)**

   Webコンソール(configMgr)を使用：*http://localhost:4502/system/console/configMgr*

1. **[CSRFフィルターの設定](mysql.md#adobe-granite-csrf-filter)**

   Webコンソール(configMgr)を使用：*http://localhost:4502/system/console/configMgr*

**オーサーインスタンスで、次の手順を実行します。**

1. （*オプション*） **[Analyticsサービスの設定](analytics.md)**

   ツール/デプロイメント/Cloud Servicesコンソールを使用します。*http://localhost:4502/etc/cloudservices/sitecatalyst.html*

1. **[FFmpegの設定](ffmpeg.md#configure-ffmpeg-transcoding-service)**

   ワークフロー/モデルコンソールの使用

1. **[トンネルサービスの有効化](deploy-communities.md#tunnel-service-on-author)**

   Webコンソール(configMgr)を使用：*http://localhost:4502/system/console/configMgr*

1. **[コミュニティ管理者の作成](users.md#creating-community-members)**

   オーサー環境では、クラシックUIセキュリティコンソールを使用します。*http://localhost:4502/useradmin*

   パス= /home/users/communityを持つユーザーの作成

   * 次のグループにメンバーを追加します：

      * コミュニティイネーブルメントマネージャー
      * コミュニティ管理者

## Dispatcher {#dispatcher}

デプロイメントに[AEM Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html)が含まれている場合、イネーブルメント機能を正しく動作させるには、`clientheader`セクションと`filter`セクションを変更する必要があります。 [コミュニティのための Dispatcher の設定](dispatcher.md#enablement)を参照してください。
