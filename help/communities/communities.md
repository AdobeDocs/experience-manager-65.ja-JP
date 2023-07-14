---
title: コミュニティの開発
description: フォーラムやユーザーグループなどのコミュニティ機能を作成し、カスタマイズします。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 3ed3768a-1b3c-45a1-a34c-61694cd407d9
source-git-commit: 260f71acd330167572d817fdf145a018b09cbc65
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 15%

---

# コミュニティの開発  {#developing-communities}

## 概要 {#overview}

Adobe Experience Manager(AEM)Communities を使用すると、フォーラム、ユーザーグループ、ブログ、Q&amp;A、カレンダー、コメント、レビュー、投票、評価、割り当てなどのコミュニティ機能の作成とカスタマイズが簡単に行えます。 これらの機能を使用すると、パブリッシュ環境にユーザー生成コンテンツ (UGC) が入力されます。

の基盤 [コミュニティサイト](overview.md#communitiessites) が [ソーシャルコンポーネントフレームワーク](scf.md) (SCF)。 コミュニティサイトの作成は、 [コミュニティサイトテンプレート](sites-console.md) それは [コミュニティ機能](functions.md).

概要と入門チュートリアルについては、次を参照してください。

* [AEM Communities の概要](overview.md)
* [AEM Communities 使用の手引き](getting-started.md)

>[!NOTE]
> 
>を常に最新の状態に保つことを強くお勧めします。 [最新リリース](deploy-communities.md#latest-releases).

## 推奨されるデプロイメント {#recommended-deployments}

* [コミュニティコンテンツストレージ](working-with-srp.md):UGC 共通ストアで使用可能なソーシャルリソースプロバイダー (SRP) の選択肢について説明します。
* [コミュニティ用の推奨トポロジ](topologies.md):使用例と SRP の選択に基づくトポロジについて説明します。

## ソーシャルコンポーネントフレームワーク {#social-component-framework}

* [ソーシャルコンポーネントフレームワーク](scf.md):フレームワークと API の概要。
* [SCF Handlebars ヘルパー](handlebars-helpers.md):デフォルトのヘルパーとカスタムヘルパーの書き込み方法。
* [クライアント側のカスタマイズ](client-customize.md):ブラウザーで実行するコードのカスタマイズ。
* [サーバー側のカスタマイズ](server-customize.md):サーバー上で実行するコードのカスタマイズ。
* [ストレージリソースプロバイダー (SRP)](srp.md):コミュニティコンテンツストレージの概要。
* [コーディングのガイドライン](code-guide.md):ガイドライン、ヒント、テクニック。
* [コミュニティコンポーネントガイド](components-guide.md):インタラクティブ開発ツール。

## コンポーネント、機能、機能の基本事項 {#component-function-and-feature-essentials}

AEM Communitiesのコンポーネント、機能および機能は、 [コミュニティサイト](sites-console.md).

* [コンポーネントおよび機能の基本事項](essentials.md)
* [コミュニティコンポーネントの clientlib](clientlibs.md)
* [コミュニティ機能](functions.md)
* [コミュニティグループテンプレート](tools-groups.md)
* [コミュニティサイトテンプレート](sites.md)

## コミュニティメンバー {#community-members}

* [ユーザーとユーザーグループの管理](users.md)
* [Social でのFacebookおよびTwitterのログイン](social-login.md)

## コミュニティグループ {#community-groups}

[コミュニティグループ](overview.md#communitygroups) は、コミュニティメンバーがコミュニティサイト内でサブコミュニティを形成できるようにする概念です。 コミュニティグループの作成は、パブリッシュ環境またはオーサー環境でおこなうことができます。

* [コミュニティグループの基本事項](essentials-groups.md)
* [グループ機能](functions.md#groups-function)
* [コミュニティグループテンプレート](tools-groups.md)
* [ユーザーとユーザーグループの管理](users.md)
* [作成者向けコミュニティグループ](creating-groups.md)

## データの管理 {#managing-data}

* [SRP と UGC の基本事項](srp-and-ugc.md) - SRP API ユーティリティメソッドと例
* [タグの基本事項](tag.md)  — コミュニティメンバーが UGC やカタログ化されたイネーブルメントリソースにタグ付けする機能

## チュートリアル {#tutorials}

* [クライアント側チュートリアル](tutorials.md#client-side-customization)
* [サーバー側チュートリアル](tutorials.md#server-side-customization)
* [ハウツーインストラクション](tutorials.md#how-to-instructions)

## トラブルシューティング {#troubleshooting}

* [トラブルシューティング](troubleshooting.md)
* [既知の問題](/help/release-notes/release-notes.md)

## 関連するコミュニティドキュメント {#related-communities-documentation}

* 訪問 [コミュニティのデプロイ](deploy-communities.md) を参照して、推奨されるデプロイメントと Dispatcher 設定について確認してください。

* 訪問 [コミュニティサイトの管理](administer-landing.md) コミュニティサイトの作成、コミュニティサイトテンプレートの設定、コミュニティコンテンツのモデレート、メンバーの管理、メッセージングの設定について説明します。

* 訪問 [コミュニティコンポーネントのオーサリング](author-communities.md) コミュニティコンポーネントを使用して作成および設定する方法を学ぶには、以下を参照してください。
