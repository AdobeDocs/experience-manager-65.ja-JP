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
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# コミュニティサイト {#communities-sites}

本節は AEM Communities の管理担当者向けであり、AEM Communities の機能に詳しいユーザーを想定しています。

## 概要 {#overview}

概要および使用の手引きのチュートリアルについては、以下を参照してください。

* [AEM Communities の概要](overview.md)
* [AEM Communities 使用の手引き](getting-started.md)
* [イネーブルメントのための AEM Communities 使用の手引き](getting-started-enablement.md)

## 管理と設定に関するトピック {#administration-and-configuration-topics}

### コミュニティサイトの作成と管理 {#communities-site-creation-and-management}

* コミュニティ[コンソール](consoles.md)

   * [サイト](sites-console.md)

      * [グループ（サブコミュニティ）](groups.md)
   * [モデレート](moderation.md)
   * [メンバーおよびグループの管理](members.md)
   * [イネーブルメントリソース](resources.md)
   * [レポート](reports.md)


* Communities [*tools *](tools.md):

   * [サイトテンプレート](sites.md)
   * [グループテンプレート](tools-groups.md)
   * [コミュニティ機能](functions.md)
   * [ストレージ設定](srp-config.md)
   * [コンポーネントガイド](components-guide.md)
   * [バッジ](badges.md)


### ユーザー生成コンテンツ {#user-generated-content}

AEM Communities の主な機能の 1 つは、サインインしたサイト訪問者（メンバー）によるユーザー生成コンテンツ（UGC）の生成です。UGC の使用について詳しくは、以下を参照してください。

* [共通UGCストア](working-with-srp.md):UGCの共有ストレージ用のSRPの選択
* [UGCのモデレート](moderate-ugc.md):信頼できる会員は、UGCを一括または文脈内でモデレートする可能性がある
* [UGCタグ付け](tag-ugc.md):メンバーがコンテンツにタグを付けられるように機能を設定できます。
* [UGCの翻訳](translate-ugc.md):機能は、すべてのUGCを翻訳するように設定したり、メンバーが選択した投稿を翻訳できるように設定したりできます
* [Analytics設定](analytics.md):会員活動に関する様々な指標に関するレポートをAdobe Analyticsで有効にする

### コミュニティメンバー {#community-members}

* [ユーザーとユーザーグループの管理](users.md):特権を持つメンバーを含む、コミュニティメンバーおよびメンバーグループの詳細
* [貢献度の制限](limits.md)：新しいメンバーによる投稿を制約する機能
* [トンネルサービス](deploy-communities.md#tunnel-service-on-author):パブリッシュ側のメンバーとメンバーグループをオーサー環境からアクセスできるようにします。
* [メンバーとグループコンソール](members.md):発行側のメンバーとメンバーグループを作成者環境から作成および管理できます。
* [ユーザー同期](sync.md):複数の発行インスタンスでメンバーとメンバーグループを同期する場合
* [FacebookおよびTwitterでのソーシャルログイン](social-login.md):サイト訪問者がFacebookやTwitterの資格情報を使用してコミュニティのメンバーになれる機能
* [スコアとバッジ](implementing-scoring.md):会員の役割を識別するために割り当てられるバッジと、その会員がコミュニティに参加してバッジを得るための能力
* [通知](notifications.md):会員が従う活動を通知する能力
* [購読](subscriptions.md)：メンバーが外部の電子メールを使用してコミュニティと対話する機能
* [メッセージ](messaging.md):会員が内部メッセージを使ってコミュニティと対話する能力

### イネーブルメント機能 {#enablement-features}

* [イネーブルメント設定](enablement.md)：イネーブルメント機能を正しくセットアップするために必要な情報
* [Analytics設定](analytics.md):adobe Analytics for Communities機能を有効にするために必要な情報
* [イネーブルメントリソースのタグ付け](tag-resources.md)：イネーブルメントカタログの作成に必要

### デプロイメント {#deployment}

「デプロイメント」セクションには、AEM Communities 固有の情報が含まれています。

コミュニティコンテンツの使用用途は、デプロイメントの構造に影響します。

* [Communities 用の推奨トポロジ](topologies.md)

AEM プラットフォームに最新の Communities リリースをインストールすることが重要です。

* [最新の Communities 機能パック](deploy-communities.md#latestfeaturepack)

See the deployment page for other Communities specific information, such as for [Upgrading](upgrade.md), [Dispatcher](dispatcher.md) and [Replication](deploy-communities.md#replication-agents-on-author).

## 関連するコミュニティドキュメント {#related-communities-documentation}

* Visit [Deploying Communities](deploy-communities.md) to learn about recommended deployments.

* Visit [Developing Communities](communities.md) to learn about the social component framework (SCF) and customizing Communities components and features.

* Visit [Authoring Communities Components](author-communities.md) to learn how to author with and configure Communities components.
