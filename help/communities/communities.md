---
title: コミュニティの開発
description: フォーラムやユーザーグループなどのコミュニティ機能を作成、カスタマイズできます。
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
source-wordcount: '399'
ht-degree: 15%
---
# コミュニティの開発  {#developing-communities}

## 概要 {#overview}

Adobe Experience Manager（AEM） Communitiesは、フォーラム、ユーザーグループ、ブログ、Q&amp;A、カレンダー、コメント、レビュー、投票、評価、割り当てなどのコミュニティ機能の作成とカスタマイズを簡素化します。 これらの機能により、UGC （ユーザー生成コンテンツ）がパブリッシュ環境に入力されます。

[&#x200B; コミュニティサイト &#x200B;](overview.md#communitiessites)の基盤は、[&#x200B; ソーシャルコンポーネントフレームワーク &#x200B;](scf.md) （SCF）です。 コミュニティサイトの作成は、[&#x200B; コミュニティ関数](functions.md)で構成される[&#x200B; コミュニティサイトテンプレート &#x200B;](sites-console.md)を選択することから始まります。

概要と基本チュートリアルについては、次のサイトを参照してください。

* [AEM Communities の概要](overview.md)
* [AEM Communities 使用の手引き](getting-started.md)

>[!NOTE]
> 
>最新のリリース [を最新の状態に保つことをお勧めします](deploy-communities.md#latest-releases)。

## 推奨されるデプロイメント {#recommended-deployments}

* [&#x200B; コミュニティコンテンツストレージ &#x200B;](working-with-srp.md):UGC共通ストアで利用可能なソーシャルリソースプロバイダー（SRP）の選択肢について説明します
* [&#x200B; コミュニティに推奨されるトポロジ &#x200B;](topologies.md)：ユースケースとSRPの選択に基づいてトポロジについて説明します

## ソーシャルコンポーネントフレームワーク {#social-component-framework}

* [&#x200B; ソーシャルコンポーネントフレームワーク &#x200B;](scf.md)：フレームワークとAPIの概要。
* [SCF ハンドルバーのヘルパー](handlebars-helpers.md)：既定のヘルパーとカスタムヘルパーの書き方。
* [&#x200B; クライアントサイドのカスタマイズ &#x200B;](client-customize.md): ブラウザーで実行されるコードをカスタマイズしています。
* [&#x200B; サーバーサイドのカスタマイズ &#x200B;](server-customize.md): サーバー上で実行されるコードをカスタマイズしています。
* [&#x200B; ストレージリソースプロバイダー（SRP） &#x200B;](srp.md)：コミュニティコンテンツストレージの概要。
* [&#x200B; コーディングガイドライン &#x200B;](code-guide.md)：ガイドライン、ヒント、テクニック。
* [&#x200B; コミュニティコンポーネントガイド &#x200B;](components-guide.md)：インタラクティブ開発ツール。

## コンポーネント、関数、および機能の基本 {#component-function-and-feature-essentials}

AEM Communitiesのコンポーネント、関数、機能は、[&#x200B; コミュニティサイト &#x200B;](sites-console.md)の構成要素を提供します。

* [コンポーネントおよび機能の基本事項](essentials.md)
* [コミュニティコンポーネントの clientlib](clientlibs.md)
* [コミュニティ機能](functions.md)
* [コミュニティグループテンプレート](tools-groups.md)
* [コミュニティサイトテンプレート](sites.md)

## コミュニティメンバー {#community-members}

* [ユーザーとユーザーグループの管理](users.md)
* [FacebookとTwitterでログイン](social-login.md)

## コミュニティグループ {#community-groups}

[&#x200B; コミュニティグループ &#x200B;](overview.md#communitygroups)は、コミュニティサイト内でコミュニティメンバーがサブコミュニティを形成できるようにするための概念です。 コミュニティグループの作成は、パブリッシュ環境またはオーサー環境で行うことができます。

* [コミュニティグループの基本事項](essentials-groups.md)
* [Groups関数](functions.md#groups-function)
* [コミュニティグループテンプレート](tools-groups.md)
* [ユーザーとユーザーグループの管理](users.md)
* [作成者のコミュニティグループ](creating-groups.md)

## データの管理 {#managing-data}

* [SRPおよびUGC Essentials](srp-and-ugc.md) - SRP API ユーティリティのメソッドと例
* [Essentials](tag.md)のタグ付け – コミュニティメンバーがUGCやカタログ化されたイネーブルメントリソースにタグ付けする機能

## チュートリアル {#tutorials}

* [クライアントサイドのチュートリアル](tutorials.md#client-side-customization)
* [サーバーサイドチュートリアル](tutorials.md#server-side-customization)
* [チュートリアルガイド](tutorials.md#how-to-instructions)

## トラブルシューティング {#troubleshooting}

* [トラブルシューティング](troubleshooting.md)
* [既知の問題](/help/release-notes/release-notes.md)

## 関連するCommunities ドキュメント {#related-communities-documentation}

* 推奨されるデプロイメントとDispatcher設定について詳しくは、[&#x200B; コミュニティのデプロイ &#x200B;](deploy-communities.md)を参照してください。

* コミュニティサイトの作成、コミュニティサイトテンプレートの設定、コミュニティコンテンツの管理、メンバーの管理、メッセージの設定について詳しくは、[&#x200B; コミュニティサイトの管理](administer-landing.md)にアクセスしてください。

* Communities コンポーネントを使用してオーサリングおよび設定する方法については、[Communities コンポーネントのオーサリング &#x200B;](author-communities.md)を参照してください。
