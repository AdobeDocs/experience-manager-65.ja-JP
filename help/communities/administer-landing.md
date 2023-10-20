---
title: コミュニティサイト
description: Adobe Experience Manager(AEM)Communities の基本を学び、既に基本機能に詳しい管理者向けの Communities を学びます。
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: e3ffc73e-2bc5-492d-b64b-750cc7d8ab9b
source-git-commit: f03d0ab9d0f491441378e16e1590d33651f064b5
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 8%

---

# コミュニティサイト {#communities-sites}

この節は、AEM Communitiesを管理し、AEM Communitiesの機能に精通しているユーザー向けです。

## 概要 {#overview}

概要と入門チュートリアルについては、次を参照してください。

* [AEM Communities の概要](overview.md)
* [AEM Communities 使用の手引き](getting-started.md)

## 管理および設定に関するトピック {#administration-and-configuration-topics}

### コミュニティサイトの作成と管理 {#communities-site-creation-and-management}

* Communities [コンソール](consoles.md)

   * [Sites](sites-console.md)

      * [グループ（サブコミュニティ）](groups.md)

   * [モデレート](moderation.md)
   * [メンバーおよびグループの管理](members.md)
   * [レポート](reports.md)

* Communities [*ツール*](tools.md):

   * [サイトテンプレート](sites.md)
   * [グループテンプレート](tools-groups.md)
   * [コミュニティ機能](functions.md)
   * [ストレージ設定](srp-config.md)
   * [コンポーネントガイド](components-guide.md)
   * [バッジ](badges.md)


### ユーザー生成コンテンツ {#user-generated-content}

AEM Communitiesの主な機能は、サインインしたサイト訪問者（メンバー）によるユーザー生成コンテンツ (UGC) の生成です。 UGC の使用に関する詳細は、次のとおりです。

* [共通 UGC ストア](working-with-srp.md):UGC の共有ストレージ用の SRP の選択
* [UGC のモデレート](moderate-ugc.md)：信頼されたメンバーは、UGC を一括またはコンテキスト内でモデレートできます
* [UGC のタグ付け](tag-ugc.md)：メンバーがコンテンツにタグ付けできるように機能を設定できます
* [UGC の翻訳](translate-ugc.md)：すべての UGC を翻訳する機能や、選択した投稿のメンバーによる翻訳を許可する機能を設定できます
* [Analytics 設定](analytics.md)：メンバーアクティビティに関する様々な指標に関するレポートをAdobe Analyticsで作成できます

### コミュニティメンバー {#community-members}

* [ユーザーとユーザーグループの管理](users.md)：権限を持つメンバーを含む、コミュニティメンバーとメンバーグループの詳細。
* [貢献度の制限](limits.md)：新しいメンバーによる投稿を制約する機能。
* [トンネルサービス](deploy-communities.md#tunnel-service-on-author)：オーサー環境から公開側のメンバーおよびメンバーグループにアクセスできます。
* [メンバーコンソールとグループコンソール](members.md)：オーサー環境からパブリッシュ側のメンバーおよびメンバーグループを作成および管理できます。
* [ユーザーの同期](sync.md)：複数のパブリッシュインスタンス間でメンバーとメンバーグループを同期する場合。
* [Social でのFacebookとTwitterのログイン](social-login.md)：サイト訪問者が、Facebookまたはコミュニティの資格情報を使用してコミュニティメンバーになれるTwitter機能。
* [スコアとバッジ](implementing-scoring.md)：メンバーの役割を識別するためにバッジを割り当てたり、メンバーがコミュニティに参加してバッジを獲得するための機能。
* [通知](notifications.md)：メンバーがフォローしているアクティビティを通知する機能。
* [購読](subscriptions.md)：メンバーが外部の電子メールを使用してコミュニティとやり取りする機能。
* [メッセージ](messaging.md)：メンバーが内部メッセージを使用してコミュニティとやり取りする機能。

### デプロイメント {#deployment}

デプロイメントセクションには、AEM Communitiesに固有の情報が含まれています。

コミュニティコンテンツを使用する性質は、デプロイメントの構造に影響します。

* [Communities 用の推奨トポロジ](topologies.md)

AEMプラットフォームに最新の Communities リリースをインストールすることが重要です。

* [最新の Communities 機能パック](deploy-communities.md#latestfeaturepack)

その他のコミュニティ固有の情報 ( 例： [アップグレード](upgrade.md), [Dispatcher](dispatcher.md)、および [レプリケーション](deploy-communities.md#replication-agents-on-author).

## 関連するコミュニティドキュメント {#related-communities-documentation}

* 訪問 [コミュニティのデプロイ](deploy-communities.md) ここで、推奨されるデプロイメントについて説明します。

* 訪問 [コミュニティの開発](communities.md) ここでは、ソーシャルコンポーネントフレームワーク (SCF) とコミュニティのコンポーネントおよび機能のカスタマイズについて学習できます。

* 訪問 [コミュニティコンポーネントのオーサリング](author-communities.md) ここでは、コミュニティコンポーネントを使用して作成および設定する方法について説明します。
