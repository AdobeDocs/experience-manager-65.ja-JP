---
title: コミュニティサイト
seo-title: コミュニティサイト
description: AEM Communities のドキュメントの概要
seo-description: AEM Communities のドキュメントの概要
uuid: 9842ce6c-1af8-4b27-b199-07410e797ab2
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 8799386a-c3b8-43cf-9f71-580ff2a81abc
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 44%

---


# コミュニティサイト {#communities-sites}

本節は AEM Communities の管理担当者向けであり、AEM Communities の機能に詳しいユーザーを想定しています。

## 概要 {#overview}

概要および使用の手引きのチュートリアルについては、以下を参照してください。

* [AEM Communities の概要](overview.md)
* [AEM Communities 使用の手引き](getting-started.md)
* [イネーブルメントのための AEM Communities 使用の手引き](getting-started-enablement.md)

## 管理と設定に関するトピック  {#administration-and-configuration-topics}

### コミュニティサイトの作成と管理 {#communities-site-creation-and-management}

* コミュニティ[コンソール](consoles.md)

   * [Sites](sites-console.md)

      * [グループ（サブコミュニティ）](groups.md)
   * [モデレート](moderation.md)
   * [メンバーおよびグループの管理](members.md)
   * [イネーブルメントリソース](resources.md)
   * [レポート](reports.md)


* コミュニティ&#x200B;[*ツール*](tools.md):

   * [サイトテンプレート](sites.md)
   * [グループテンプレート](tools-groups.md)
   * [コミュニティ機能](functions.md)
   * [ストレージ設定](srp-config.md)
   * [コンポーネントガイド](components-guide.md)
   * [バッジ](badges.md)


### ユーザー生成コンテンツ {#user-generated-content}

AEM Communities の主な機能の 1 つは、サインインしたサイト訪問者（メンバー）によるユーザー生成コンテンツ（UGC）の生成です。UGC の使用について詳しくは、以下を参照してください。

* [共通UGCストア](working-with-srp.md):UGCの共有ストレージ用のSRPの選択
* [UGCのモデレート](moderate-ugc.md):信頼できるメンバーが一括またはコンテキスト内でUGCをモデレートする可能性がある
* [タグ付けUGC](tag-ugc.md):メンバーがコンテンツにタグを付けられるように機能を設定できます。
* [Translating UGC](translate-ugc.md):機能を設定して、すべてのUGCを翻訳したり、メンバーが選択した投稿を翻訳できるようにしたりできます。
* [Analytics設定](analytics.md):会員アクティビティに関する様々な指標に関するレポートをAdobe Analyticsに対して有効にする

### コミュニティメンバー {#community-members}

* [ユーザーとユーザーグループの管理](users.md):特権を持つメンバーを含む、コミュニティメンバーおよびメンバーグループの詳細。
* [貢献度の制限](limits.md)：新しいメンバーによる投稿を制約する機能.
* [トンネルサービス](deploy-communities.md#tunnel-service-on-author):発行側のメンバーとメンバーグループに対して、作成者環境からアクセスできます。
* [メンバーとグループコンソール](members.md):発行側のメンバーとメンバーグループを作成者環境から作成および管理できます。
* [ユーザー同期](sync.md):複数のパブリッシュインスタンス間でメンバーとメンバーグループを同期する場合。
* [FacebookおよびTwitterを使用したソーシャルログイン](social-login.md):サイト訪問者がFacebookやTwitterの資格情報を使用してコミュニティのメンバーになれる機能。
* [スコアリングとバッジ](implementing-scoring.md):会員の役割を識別するために割り当てられるバッジと、会員がコミュニティに参加してバッジを得るための能力。
* [通知](notifications.md):メンバーがフォローしているアクティビティを通知する機能。
* [購読](subscriptions.md)：メンバーが外部の電子メールを使用してコミュニティと対話する機能.
* [メッセージ](messaging.md):内部メッセージを使用してコミュニティとやり取りする機能。

### イネーブルメント機能 {#enablement-features}

* [イネーブルメント設定](enablement.md)：イネーブルメント機能を正しくセットアップするために必要な情報.
* [Analytics設定](analytics.md):コミュニティ機能でAdobe Analyticsを有効にするために必要な情報です。
* [イネーブルメントリソースのタグ付け](tag-resources.md)：イネーブルメントカタログの作成に必要.

### デプロイメント {#deployment}

「デプロイメント」セクションには、AEM Communities 固有の情報が含まれています。

コミュニティコンテンツの使用用途は、デプロイメントの構造に影響します。

* [Communities 用の推奨トポロジ](topologies.md)

AEM プラットフォームに最新の Communities リリースをインストールすることが重要です。

* [最新の Communities 機能パック](deploy-communities.md#latestfeaturepack)

[アップグレード](upgrade.md)、[ディスパッチャー](dispatcher.md)、[レプリケーション](deploy-communities.md#replication-agents-on-author)など、Communities固有のその他の情報については、デプロイメントページを参照してください。

## 関連するコミュニティドキュメント {#related-communities-documentation}

* 推奨される展開については、[Communitiesの展開](deploy-communities.md)を参照してください。

* Social Component Framework(SCF)とCommunitiesのコンポーネントと機能のカスタマイズについては、[Developing Communities](communities.md)を参照してください。

* Communitiesコンポーネントの作成方法と設定方法については、[Authoring Communities Components](author-communities.md)を参照してください。
