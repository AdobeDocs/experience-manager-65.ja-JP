---
title: コミュニティサイト
description: 管理者がAdobe Experience Manager（AEM）の基本機能に精通している場合は、その基本について説明します。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: e3ffc73e-2bc5-492d-b64b-750cc7d8ab9b
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 8%

---

# コミュニティサイト {#communities-sites}

このセクションは、AEM Communitiesを管理し、AEM Communitiesの機能に精通しているユーザーを対象としています。

## 概要 {#overview}

概要と基本チュートリアルについては、次のサイトを参照してください。

* [AEM Communities の概要](overview.md)
* [AEM Communities 使用の手引き](getting-started.md)

## 管理と設定のトピック {#administration-and-configuration-topics}

### Communities サイトの作成と管理 {#communities-site-creation-and-management}

* コミュニティ [ コンソール ](consoles.md)

   * [Sites](sites-console.md)

      * [グループ（サブコミュニティ）](groups.md)

   * [モデレート](moderation.md)
   * [メンバーとグループの管理](members.md)
   * [レポート](reports.md)

* コミュニティ [*ツール*](tools.md):

   * [サイトテンプレート](sites.md)
   * [グループテンプレート](tools-groups.md)
   * [コミュニティ機能](functions.md)
   * [ストレージ設定](srp-config.md)
   * [コンポーネントガイド](components-guide.md)
   * [バッジ](badges.md)


### ユーザー生成コンテンツ {#user-generated-content}

AEM Communitiesの主な機能は、サインインサイト訪問者（メンバー）がUGCを生成することです。 UGCの利用方法について詳しくは、次のサイトをご覧ください。

* [共通UGC ストア ](working-with-srp.md):UGCの共有ストレージ用のSRPの選択
* [UGCの管理](moderate-ugc.md)：信頼できるメンバーは、一括またはコンテキスト内でUGCを管理できます
* [UGC](tag-ugc.md)のタグ付け：メンバーがコンテンツをタグ付けできるように機能を設定できます
* [UGCの翻訳](translate-ugc.md)：すべてのUGCを翻訳するように機能を設定するか、メンバーが選択した投稿を翻訳できるように設定できます
* [Analytics Configuration](analytics.md): Adobe Analyticsでメンバーのアクティビティに関する様々な指標をレポートできるようにしています

### コミュニティメンバー {#community-members}

* [ ユーザーとユーザーグループの管理](users.md)：権限のあるメンバーを含む、コミュニティメンバーとメンバーグループの詳細。
* [貢献度制限](limits.md)：新しいメンバーによる投稿を制限する機能。
* [ トンネルサービス ](deploy-communities.md#tunnel-service-on-author)：パブリッシュサイドのメンバーとメンバーグループにオーサー環境からアクセスできるようにします。
* [ メンバーとグループ コンソール ](members.md)：パブリッシュサイドのメンバーとメンバーグループを作成し、オーサー環境から管理できます。
* [ ユーザー同期](sync.md)：複数のパブリッシュインスタンス間でメンバーとメンバーグループを同期します。
* [FacebookおよびTwitterでログイン ](social-login.md)：サイト訪問者がFacebookまたはTwitterの資格情報を使用してコミュニティ メンバーになる機能。
* [ スコアリングとバッジ ](implementing-scoring.md): バッジを割り当ててメンバーの役割を特定し、メンバーがコミュニティへの参加を通じてバッジを獲得できるようにする機能。
* [通知](notifications.md)：メンバーがフォローしているアクティビティを通知する機能。
* [ サブスクリプション ](subscriptions.md)：メンバーが外部メールを使用してコミュニティと対話する機能。
* [ メッセージ ](messaging.md)：メンバーが内部メッセージを使用してコミュニティと対話する機能。

### デプロイメント {#deployment}

「デプロイメント」セクションには、AEM Communitiesに固有の情報が含まれています。

コミュニティコンテンツを扱う性質は、デプロイメントの構造に影響します。

* [Communities 用の推奨トポロジ](topologies.md)

AEM プラットフォームに最新のCommunities リリースをインストールすることが重要です。

* [最新のコミュニティ機能パック](deploy-communities.md#latestfeaturepack)

[ アップグレード ](upgrade.md)、[Dispatcher](dispatcher.md)、[ レプリケーション ](deploy-communities.md#replication-agents-on-author)など、その他のコミュニティ固有の情報については、デプロイメントページを参照してください。

## 関連するCommunities ドキュメント {#related-communities-documentation}

* [ コミュニティのデプロイ ](deploy-communities.md)にアクセスすると、推奨されるデプロイメントについて確認できます。

* [ コミュニティの開発](communities.md)にアクセスして、ソーシャルコンポーネントフレームワーク（SCF）とコミュニティのコンポーネントと機能のカスタマイズについて学ぶことができます。

* [Communities コンポーネントのオーサリング ](author-communities.md)にアクセスして、Communities コンポーネントのオーサリングと設定方法を学ぶことができます。
