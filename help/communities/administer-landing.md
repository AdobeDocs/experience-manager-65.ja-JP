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
exl-id: e3ffc73e-2bc5-492d-b64b-750cc7d8ab9b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 44%

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
* [UGCのモデレート](moderate-ugc.md):信頼されているメンバーは、UGCを一括またはコンテキスト内でモデレートできます
* [UGCのタグ付け](tag-ugc.md):機能は、メンバーがコンテンツにタグを付けるのを許可するように設定できます
* [UGCの翻訳](translate-ugc.md):機能は、すべてのUGCを翻訳するように設定したり、選択した投稿の翻訳をメンバーに許可したりできます
* [Analyticsの設定](analytics.md):Adobe Analyticsでのメンバーアクティビティに関する様々な指標のレポートの有効化

### コミュニティメンバー {#community-members}

* [ユーザーとユーザーグループの管理](users.md):権限を持つメンバーを含む、コミュニティメンバーおよびメンバーグループの詳細。
* [貢献度の制限](limits.md)：新しいメンバーによる投稿を制約する機能.
* [トンネルサービス](deploy-communities.md#tunnel-service-on-author):オーサー環境からパブリッシュ側のメンバーとメンバーグループにアクセスできます。
* [メンバーコンソールとグループコンソール](members.md):オーサー環境からパブリッシュ側のメンバーとメンバーグループを作成および管理できます。
* [ユーザーの同期](sync.md):複数のパブリッシュインスタンス間でメンバーとメンバーグループを同期する場合。
* [facebookとTwitterを使用したソーシャルログイン](social-login.md):サイト訪問者が、FacebookまたはTwitterの資格情報を使用してコミュニティメンバーになれる機能。
* [スコアとバッジ](implementing-scoring.md):メンバーの役割を識別するためにバッジを割り当てたり、メンバーがコミュニティに参加してバッジを獲得する機能。
* [通知](notifications.md):メンバーがフォローしているアクティビティを通知する機能。
* [購読](subscriptions.md)：メンバーが外部の電子メールを使用してコミュニティと対話する機能.
* [メッセージ](messaging.md):メンバーが内部メッセージを使用してコミュニティとやり取りする機能。

### イネーブルメント機能 {#enablement-features}

* [イネーブルメント設定](enablement.md)：イネーブルメント機能を正しくセットアップするために必要な情報.
* [Analyticsの設定](analytics.md):コミュニティ機能に対してAdobe Analyticsを有効にするために必要な情報です。
* [イネーブルメントリソースのタグ付け](tag-resources.md)：イネーブルメントカタログの作成に必要.

### デプロイメント {#deployment}

「デプロイメント」セクションには、AEM Communities 固有の情報が含まれています。

コミュニティコンテンツの使用用途は、デプロイメントの構造に影響します。

* [Communities 用の推奨トポロジ](topologies.md)

AEM プラットフォームに最新の Communities リリースをインストールすることが重要です。

* [最新の Communities 機能パック](deploy-communities.md#latestfeaturepack)

[アップグレード](upgrade.md)、[Dispatcher](dispatcher.md)、[レプリケーション](deploy-communities.md#replication-agents-on-author)など、その他のCommunities固有の情報については、デプロイメントページを参照してください。

## 関連するコミュニティドキュメント {#related-communities-documentation}

* 推奨されるデプロイメントについては、[Communitiesのデプロイ](deploy-communities.md)を参照してください。

* ソーシャルコンポーネントフレームワーク(SCF)とコミュニティのコンポーネントと機能のカスタマイズについては、 [コミュニティの開発](communities.md)を参照してください。

* コミュニティコンポーネントを使用してオーサリングおよび設定する方法については、 [コミュニティコンポーネントのオーサリング](author-communities.md)を参照してください。
