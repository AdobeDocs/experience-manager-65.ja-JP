---
title: コミュニティの開発
description: フォーラム、ユーザーグループなどのコミュニティ機能を作成およびカスタマイズします。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 3ed3768a-1b3c-45a1-a34c-61694cd407d9
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 15%

---

# コミュニティの開発  {#developing-communities}

## 概要 {#overview}

Adobe Experience Manager（AEM） Communities を使用すると、フォーラム、ユーザーグループ、ブログ、Q&amp;A、カレンダー、コメント、レビュー、投票、評価、割り当てなどのコミュニティ機能を簡単に作成およびカスタマイズできます。 これらの機能により、ユーザー生成コンテンツ（UGC）がパブリッシュ環境に入力されます。

[&#x200B; コミュニティサイト &#x200B;](overview.md#communitiessites) の基盤となるのは、[&#x200B; ソーシャルコンポーネントフレームワーク &#x200B;](scf.md) （SCF）です。 コミュニティサイトの作成は、[&#x200B; コミュニティ機能 &#x200B;](functions.md) で構成された [&#128279;](sites-console.md) コミュニティサイトテンプレート  を選択することから始まります。

概要とはじめにのチュートリアルについては、次を参照してください。

* [AEM Communities の概要](overview.md)
* [AEM Communities 使用の手引き](getting-started.md)

>[!NOTE]
> 
>[&#x200B; 最新リリース &#x200B;](deploy-communities.md#latest-releases) を常に最新の状態にしておくことを強くお勧めします。

## 推奨されるデプロイメント {#recommended-deployments}

* [&#x200B; コミュニティコンテンツストレージ &#x200B;](working-with-srp.md):UGC 共通ストアで使用可能なソーシャルリソースプロバイダー（SRP）の選択肢について説明します
* [Communities 向けの推奨トポロジ &#x200B;](topologies.md)：ユースケースと SRP の選択に基づくトポロジについて説明します

## ソーシャルコンポーネントフレームワーク {#social-component-framework}

* [&#x200B; ソーシャルコンポーネントフレームワーク &#x200B;](scf.md)：フレームワークと API の概要
* [SCF Handlebars ヘルパー &#x200B;](handlebars-helpers.md)：デフォルトのヘルパーとカスタムヘルパーの記述方法。
* [&#x200B; クライアントサイドのカスタマイズ &#x200B;](client-customize.md)：ブラウザーで実行されるコードをカスタマイズする。
* [&#x200B; サーバーサイドのカスタマイズ &#x200B;](server-customize.md)：サーバー上で実行されるコードをカスタマイズする。
* [&#x200B; ストレージリソースプロバイダー（SRP） &#x200B;](srp.md)：コミュニティコンテンツストレージの概要。
* [&#x200B; コーディングガイドライン &#x200B;](code-guide.md)：ガイドライン、ヒントとテクニック。
* [&#x200B; コミュニティコンポーネントガイド &#x200B;](components-guide.md)：インタラクティブ開発ツール。

## コンポーネント、機能、機能の基本事項 {#component-function-and-feature-essentials}

AEM Communitiesのコンポーネント、機能および機能は、[&#x200B; コミュニティサイト &#x200B;](sites-console.md) の構築ブロックを提供します。

* [コンポーネントおよび機能の基本事項](essentials.md)
* [コミュニティコンポーネントの clientlib](clientlibs.md)
* [コミュニティ機能](functions.md)
* [コミュニティグループテンプレート](tools-groups.md)
* [コミュニティサイトテンプレート](sites.md)

## コミュニティメンバー {#community-members}

* [ユーザーとユーザーグループの管理](users.md)
* [ソーシャル FacebookとTwitterでのログイン](social-login.md)

## コミュニティグループ {#community-groups}

[&#x200B; コミュニティグループ &#x200B;](overview.md#communitygroups) は、コミュニティメンバーがコミュニティサイト内にサブコミュニティを形成できるようにするという概念です。 コミュニティグループは、パブリッシュ環境またはオーサー環境で作成する場合があります。

* [コミュニティグループの基本事項](essentials-groups.md)
* [Groups 関数](functions.md#groups-function)
* [コミュニティグループテンプレート](tools-groups.md)
* [ユーザーとユーザーグループの管理](users.md)
* [作成者のコミュニティグループ](creating-groups.md)

## データの管理 {#managing-data}

* [SRP と UGC の基本事項 &#x200B;](srp-and-ugc.md) - SRP API ユーティリティメソッドと例
* [&#x200B; タグの基本事項 &#x200B;](tag.md) - コミュニティメンバーが UGC やカタログ化されたイネーブルメントリソースにタグを付ける機能

## チュートリアル {#tutorials}

* [クライアントサイドのチュートリアル](tutorials.md#client-side-customization)
* [サーバーサイドのチュートリアル](tutorials.md#server-side-customization)
* [ハウツーの説明](tutorials.md#how-to-instructions)

## トラブルシューティング {#troubleshooting}

* [トラブルシューティング](troubleshooting.md)
* [既知の問題](/help/release-notes/release-notes.md)

## 関連する Communities ドキュメント {#related-communities-documentation}

* 推奨されるデプロイメントとDispatcher設定について詳しくは、[Communities のデプロイ &#x200B;](deploy-communities.md) を参照してください。

* コミュニティサイトの作成、コミュニティサイトテンプレートの設定、コミュニティコンテンツの管理、メンバーの管理、メッセージングの設定については、[&#x200B; コミュニティサイトの管理 &#x200B;](administer-landing.md) を参照してください。

* Communities コンポーネントを使用して作成および設定する方法については、[Communities コンポーネントのオーサリング &#x200B;](author-communities.md) を参照してください。
