---
title: コミュニティサイト
description: の管理者向けAdobe Experience Manager（AEM） Communities の基本事項について説明します。ユーザーは、その基本機能に精通しています。
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
source-wordcount: '449'
ht-degree: 8%

---

# コミュニティサイト {#communities-sites}

この節は、AEM Communitiesを管理するユーザーを対象としており、AEM Communitiesの機能に関する知識を前提としています。

## 概要 {#overview}

概要とはじめにのチュートリアルについては、次を参照してください。

* [AEM Communities の概要](overview.md)
* [AEM Communities 使用の手引き](getting-started.md)

## 管理および設定に関するトピック {#administration-and-configuration-topics}

### コミュニティサイトの作成と管理 {#communities-site-creation-and-management}

* コミュニティ [&#x200B; コンソール &#x200B;](consoles.md)

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

AEM Communitiesの主な機能は、ログインしたサイト訪問者（メンバー）がユーザー生成コンテンツ（UGC）を生成することです。 UGC の操作について詳しくは、次を参照してください。

* [Common UGC Store](working-with-srp.md):UGC の共有ストレージ用の SRP の選択
* [UGC のモデレート &#x200B;](moderate-ugc.md)：信頼されたメンバーは、一括またはコンテキスト内で UGC をモデレートできる場合があります
* [UGC のタグ付け &#x200B;](tag-ugc.md)：メンバーがコンテンツにタグ付けできるように機能を設定できます
* [UGC の翻訳 &#x200B;](translate-ugc.md)：機能は、すべての UGC を翻訳するように設定することも、メンバーが選択した投稿を翻訳できるようにすることもできます
* [Analytics 設定 &#x200B;](analytics.md)：メンバーアクティビティに関する様々な指標についてAdobe Analyticsがレポートできるようにします

### コミュニティメンバー {#community-members}

* [&#x200B; ユーザーとユーザーグループの管理 &#x200B;](users.md)：コミュニティメンバーとメンバーグループの詳細（権限のあるメンバーを含む）。
* [&#x200B; 貢献度制限 &#x200B;](limits.md)：新しいメンバーによる投稿を制限する機能。
* [&#x200B; トンネルサービス &#x200B;](deploy-communities.md#tunnel-service-on-author)：オーサー環境からパブリッシュ側のメンバーおよびメンバーグループにアクセスできるようにします。
* [&#x200B; メンバーコンソールとグループコンソール &#x200B;](members.md)：パブリッシュサイドのメンバーおよびメンバーグループを、オーサー環境で作成および管理できます。
* [&#x200B; ユーザー同期 &#x200B;](sync.md)：複数のパブリッシュインスタンス間でメンバーとメンバーグループを同期する場合。
* [FacebookおよびTwitterでのソーシャルログイン &#x200B;](social-login.md)：サイト訪問者がFacebookまたはTwitterの資格情報を使用してコミュニティメンバーになる機能。
* [&#x200B; スコアおよびバッジ &#x200B;](implementing-scoring.md)：バッジを割り当ててメンバーの役割を特定し、メンバーがコミュニティへの参加を通じてバッジを獲得する機能。
* [&#x200B; 通知 &#x200B;](notifications.md)：メンバーがフォローするアクティビティの通知を受け取る機能。
* [&#x200B; 購読 &#x200B;](subscriptions.md)：メンバーが外部メールを使用してコミュニティとやり取りする機能。
* [&#x200B; メッセージング &#x200B;](messaging.md)：メンバーが内部メッセージを使用してコミュニティとやり取りする機能。

### デプロイメント {#deployment}

「デプロイメント」セクションには、AEM Communitiesに固有の情報が含まれます。

コミュニティコンテンツの操作の性質は、デプロイメントの構造に影響します。

* [Communities 用の推奨トポロジ](topologies.md)

AEM プラットフォームには、最新の Communities リリースをインストールすることが重要です。

* [最新の Communities 機能パック](deploy-communities.md#latestfeaturepack)

[&#x200B; アップグレード &#x200B;](upgrade.md)、[Dispatcher](dispatcher.md)、&lbrace; レプリケーション [&#128279;](deploy-communities.md#replication-agents-on-author) など、Communities 固有のその他の情報については、デプロイメントページを参照し  ください。

## 関連する Communities ドキュメント {#related-communities-documentation}

* 推奨されるデプロイメントについて詳しくは、[Communities のデプロイ &#x200B;](deploy-communities.md) を参照してください。

* [&#x200B; コミュニティの開発 &#x200B;](communities.md) を参照して、ソーシャルコンポーネントフレームワーク（SCF）と、コミュニティのコンポーネントや機能のカスタマイズについて学ぶことができます。

* Communities コンポーネントを使用してオーサリングする方法と設定する方法については、[Communities コンポーネントのオーサリング &#x200B;](author-communities.md) を参照してください。
