---
title: コミュニティサイト
seo-title: Communities Sites
description: AEM Communities のドキュメントの概要
seo-description: Overview of the AEM Communities documentation
uuid: 9842ce6c-1af8-4b27-b199-07410e797ab2
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 8799386a-c3b8-43cf-9f71-580ff2a81abc
role: Admin
exl-id: e3ffc73e-2bc5-492d-b64b-750cc7d8ab9b
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '470'
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


* コミュニティ [*ツール*](tools.md):

   * [サイトテンプレート](sites.md)
   * [グループテンプレート](tools-groups.md)
   * [コミュニティ機能](functions.md)
   * [ストレージ設定](srp-config.md)
   * [コンポーネントガイド](components-guide.md)
   * [バッジ](badges.md)


### ユーザー生成コンテンツ {#user-generated-content}

AEM Communities の主な機能の 1 つは、サインインしたサイト訪問者（メンバー）によるユーザー生成コンテンツ（UGC）の生成です。UGC の使用について詳しくは、以下を参照してください。

* [共通 UGC ストア](working-with-srp.md):UGC の共有ストレージ用の SRP の選択
* [UGC のモデレート](moderate-ugc.md):信頼できるメンバーは、UGC を一括またはコンテキスト内でモデレートできます
* [UGC のタグ付け](tag-ugc.md):機能は、メンバーがコンテンツにタグを付けるのを許可するように設定できます
* [UGC の翻訳](translate-ugc.md):機能は、すべての UGC を翻訳するように設定したり、メンバーが選択した投稿を翻訳することを許可したりできます
* [Analytics 設定](analytics.md):Adobe Analyticsでのメンバーアクティビティに関する様々な指標のレポート作成

### コミュニティメンバー {#community-members}

* [ユーザーとユーザーグループの管理](users.md):権限を持つメンバーを含む、コミュニティメンバーおよびメンバーグループの詳細。
* [貢献度の制限](limits.md)：新しいメンバーによる投稿を制約する機能.
* [トンネルサービス](deploy-communities.md#tunnel-service-on-author):オーサー環境からパブリッシュ側のメンバーおよびメンバーグループにアクセスできます。
* [メンバーコンソールとグループコンソール](members.md):パブリッシュ側のメンバーとメンバーグループを、オーサー環境から作成および管理できます。
* [ユーザーの同期](sync.md):複数のパブリッシュインスタンス間でメンバーとメンバーグループを同期するため。
* [facebookとTwitterを使用したソーシャルログイン](social-login.md):サイト訪問者が、FacebookまたはTwitterの資格情報を使用してコミュニティメンバーになれる機能。
* [スコアとバッジ](implementing-scoring.md):メンバーの役割を識別するためにバッジを割り当てたり、メンバーがコミュニティに参加してバッジを獲得するための機能。
* [通知](notifications.md):メンバーがフォローしているアクティビティを通知する機能。
* [購読](subscriptions.md)：メンバーが外部の電子メールを使用してコミュニティと対話する機能.
* [メッセージ](messaging.md):メンバーが内部メッセージを使用してコミュニティとやり取りする機能。

### イネーブルメント機能 {#enablement-features}

* [イネーブルメント設定](enablement.md)：イネーブルメント機能を正しくセットアップするために必要な情報.
* [Analytics 設定](analytics.md):Communities 機能に対してAdobe Analyticsを有効にするために必要な情報です。
* [イネーブルメントリソースのタグ付け](tag-resources.md)：イネーブルメントカタログの作成に必要.

### デプロイメント {#deployment}

「デプロイメント」セクションには、AEM Communities 固有の情報が含まれています。

コミュニティコンテンツの使用用途は、デプロイメントの構造に影響します。

* [Communities 用の推奨トポロジ](topologies.md)

AEM プラットフォームに最新の Communities リリースをインストールすることが重要です。

* [最新の Communities 機能パック](deploy-communities.md#latestfeaturepack)

その他の Communities 固有の情報 ( 例： [アップグレード](upgrade.md), [Dispatcher](dispatcher.md) および [レプリケーション](deploy-communities.md#replication-agents-on-author).

## 関連するコミュニティドキュメント {#related-communities-documentation}

* 訪問 [コミュニティのデプロイ](deploy-communities.md) を参照して、推奨されるデプロイメントについて確認してください。

* 訪問 [コミュニティの開発](communities.md) ソーシャルコンポーネントフレームワーク (SCF) と、コミュニティのコンポーネントと機能のカスタマイズについて説明します。

* 訪問 [コミュニティコンポーネントのオーサリング](author-communities.md) コミュニティコンポーネントを使用して作成および設定する方法を学ぶには、以下を参照してください。
