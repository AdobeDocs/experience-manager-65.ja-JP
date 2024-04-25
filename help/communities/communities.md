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

の基盤 [コミュニティサイト](overview.md#communitiessites) が [ソーシャルコンポーネントフレームワーク](scf.md) （SCF）。 コミュニティサイトの作成は、 [コミュニティサイトテンプレート](sites-console.md) 構成する [コミュニティ機能](functions.md).

概要とはじめにのチュートリアルについては、次を参照してください。

* [AEM Communities の概要](overview.md)
* [AEM Communities 使用の手引き](getting-started.md)

>[!NOTE]
> 
>を最新の状態に保つことを強くお勧めします [最新リリース](deploy-communities.md#latest-releases).

## 推奨されるデプロイメント {#recommended-deployments}

* [コミュニティコンテンツストレージ](working-with-srp.md):UGC 共通ストアで使用可能なソーシャルリソースプロバイダー（SRP）の選択肢について説明します
* [Communities 用の推奨されるトポロジ](topologies.md)：ユースケースと SRP の選択に基づいたトポロジについて説明します

## ソーシャルコンポーネントフレームワーク {#social-component-framework}

* [ソーシャルコンポーネントフレームワーク](scf.md)：フレームワークと API の概要
* [SCF Handlebars ヘルパー](handlebars-helpers.md)：デフォルトのヘルパーとカスタムヘルパーの作成方法。
* [クライアントサイドのカスタマイズ](client-customize.md)：ブラウザーで実行されるコードのカスタマイズ。
* [サーバーサイドのカスタマイズ](server-customize.md)：サーバー上で実行されるコードのカスタマイズ。
* [ストレージリソースプロバイダー（SRP）](srp.md)：コミュニティコンテンツストレージの概要。
* [コーディングのガイドライン](code-guide.md)：ガイドライン、ヒントとテクニック。
* [コミュニティコンポーネントガイド](components-guide.md)：インタラクティブ開発ツール。

## コンポーネント、機能、機能の基本事項 {#component-function-and-feature-essentials}

AEM Communitiesのコンポーネント、関数および機能は、次の構成要素を提供します [コミュニティサイト](sites-console.md).

* [コンポーネントおよび機能の基本事項](essentials.md)
* [コミュニティコンポーネントの clientlib](clientlibs.md)
* [コミュニティ機能](functions.md)
* [コミュニティグループテンプレート](tools-groups.md)
* [コミュニティサイトテンプレート](sites.md)

## コミュニティメンバー {#community-members}

* [ユーザーとユーザーグループの管理](users.md)
* [ソーシャル FacebookとTwitterでのログイン](social-login.md)

## コミュニティグループ {#community-groups}

[コミュニティグループ](overview.md#communitygroups) は、コミュニティメンバーがコミュニティサイト内にサブコミュニティを形成できるようにする概念です。 コミュニティグループは、パブリッシュ環境またはオーサー環境で作成する場合があります。

* [コミュニティグループの基本事項](essentials-groups.md)
* [Groups 関数](functions.md#groups-function)
* [コミュニティグループテンプレート](tools-groups.md)
* [ユーザーとユーザーグループの管理](users.md)
* [作成者のコミュニティグループ](creating-groups.md)

## データの管理 {#managing-data}

* [SRP と UGC の基本事項](srp-and-ugc.md) - SRP API ユーティリティメソッドと例
* [タグの基本事項](tag.md) - コミュニティメンバーが UGC やカタログ化されたイネーブルメントリソースにタグを付ける機能

## チュートリアル {#tutorials}

* [クライアントサイドのチュートリアル](tutorials.md#client-side-customization)
* [サーバーサイドのチュートリアル](tutorials.md#server-side-customization)
* [ハウツーの説明](tutorials.md#how-to-instructions)

## トラブルシューティング {#troubleshooting}

* [トラブルシューティング](troubleshooting.md)
* [既知の問題](/help/release-notes/release-notes.md)

## 関連する Communities ドキュメント {#related-communities-documentation}

* 訪問 [Communities のデプロイ](deploy-communities.md) 推奨されるデプロイメントと Dispatcher 設定について説明します。

* 訪問 [コミュニティサイトの管理](administer-landing.md) コミュニティサイトの作成、コミュニティサイトテンプレートの設定、コミュニティコンテンツのモデレート、メンバーの管理およびメッセージングの設定について説明します。

* 訪問 [Communities コンポーネントのオーサリング](author-communities.md) でオーサリングし Communities コンポーネントを設定する方法について説明します。
