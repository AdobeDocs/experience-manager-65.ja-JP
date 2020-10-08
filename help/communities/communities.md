---
title: コミュニティの開発
seo-title: コミュニティの開発
description: フォーラム、ユーザーグループなどのコミュニティ機能を作成し、カスタマイズします
seo-description: フォーラム、ユーザーグループなどのコミュニティ機能を作成し、カスタマイズします
uuid: 51dc54da-9090-4d36-adf9-72d5479062a5
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: fbfe8097-3c3f-4a05-97ad-1ce526362a26
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 59%

---


# コミュニティの開発  {#developing-communities}

## 概要 {#overview}

AEM Communities により、フォーラム、ユーザーグループ、ブログ、Q&amp;A、カレンダー、コメント、レビュー、投票、評価、割り当てなどのコミュニティ機能の作成およびカスタマイズが簡素化されます。これらの機能により、ユーザ生成コンテンツ(UGC)が公開環境に入力されます。

The foundation of a [community site](overview.md#communitiessites) is the [social component framework](scf.md) (SCF). Creation of a community site begins with the selection of a [community site template](sites-console.md) that is composed of [community functions](functions.md).

概要および使用の手引きのチュートリアルについては、以下を参照してください。

* [AEM Communities の概要](overview.md)
* [AEM Communities 使用の手引き](getting-started.md)
* [イネーブルメントのための AEM Communities 使用の手引き](getting-started-enablement.md)

>[!NOTE]
> 
>[最新リリース](deploy-communities.md#latest-releases)によって常に最新状態にしておくことをお勧めします。

## 推奨されるデプロイメント {#recommended-deployments}

* [コミュニティコンテンツストレージ](working-with-srp.md)：UGC 共通ストアの使用可能な SRP 選択肢について説明します。
* [コミュニティに推奨されるトポロジ](topologies.md)：使用例および SRP 選択肢に基づいてトポロジについて説明します。

## ソーシャルコンポーネントフレームワーク {#social-component-framework}

* [Social Component Framework](scf.md):フレームワークとAPIの概要を説明します。
* [SCFハンドルヘルパー](handlebars-helpers.md):デフォルトのヘルパーおよびカスタムヘルパーの作成方法。
* [クライアント側のカスタマイズ](client-customize.md):ブラウザーで実行するコードのカスタマイズ
* [サーバー側のカスタマイズ](server-customize.md):サーバーで実行するコードのカスタマイズ
* [ストレージリソースプロバイダ(SRP)](srp.md):コミュニティコンテンツのストレージの概要を示します。
* [コーディングのガイドライン](code-guide.md):ガイドライン、ヒント、テクニックを参照してください。
* [コミュニティコンポーネントガイド](components-guide.md):インタラクティブ開発ツール

## コンポーネントおよび機能の基本事項 {#component-function-and-feature-essentials}

AEM Communities のコンポーネントおよび機能によって、[コミュニティサイト](sites-console.md)に構成要素が提供されます。

* [コンポーネントおよび機能の基本事項](essentials.md)
* [コミュニティコンポーネントの clientlib](clientlibs.md)
* [コミュニティ機能](functions.md)
* [コミュニティグループテンプレート](tools-groups.md)
* [コミュニティサイトテンプレート](sites.md)

## コミュニティメンバー {#community-members}

* [ユーザーとユーザーグループの管理](users.md)
* [Facebook と Twitter を使用したソーシャルログイン](social-login.md)

## コミュニティグループ {#community-groups}

[コミュニティグループ](overview.md#communitygroups)は、コミュニティメンバーがコミュニティサイト内でサブコミュニティを形成できるようにする概念です。コミュニティグループの作成は、発行環境または作成者フォルダーで行うことができます。

* [コミュニティグループの基本事項](essentials-groups.md)
* [グループ機能](functions.md#groups-function)
* [コミュニティグループテンプレート](tools-groups.md)
* [ユーザーとユーザーグループの管理](users.md)
* [作成者のコミュニティグループ](creating-groups.md)

## データの管理 {#managing-data}

* [SRPとUGC Essentials](srp-and-ugc.md) - SRP APIユーティリティのメソッドと例
* [Tag Essentials](tag.md) — コミュニティメンバーがUGCやカタログ化された有効化リソースにタグ付けする機能

## チュートリアル {#tutorials}

* [クライアント側チュートリアル](tutorials.md#client-side-customization)
* [サーバー側チュートリアル](tutorials.md#server-side-customization)
* [方法の説明](tutorials.md#how-to-instructions)

## トラブルシューティング {#troubleshooting}

* [トラブルシューティング](troubleshooting.md)
* [既知の問題](/help/release-notes/known-issues.md)

## 関連するコミュニティドキュメント {#related-communities-documentation}

* Visit [Deploying Communities](deploy-communities.md) to learn about recommended deployments and dispatcher configuration.

* コミュニティサイトの作成、コミュニティサイトテンプレートの設定、コミュニティコンテンツのモデレート、メンバーの管理およびメッセージングの設定については、[コミュニティサイトの管理](administer-landing.md)を参照してください。

* Visit [Authoring Communities Components](author-communities.md) to learn how to author with and configure Communities components.

