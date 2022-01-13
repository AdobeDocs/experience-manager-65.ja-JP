---
title: コミュニティの開発
seo-title: Developing Communities
description: フォーラム、ユーザーグループなどのコミュニティ機能を作成し、カスタマイズします
seo-description: Create and customize community features such as forums, user groups, and more
uuid: 51dc54da-9090-4d36-adf9-72d5479062a5
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: fbfe8097-3c3f-4a05-97ad-1ce526362a26
exl-id: 3ed3768a-1b3c-45a1-a34c-61694cd407d9
source-git-commit: d1b4cf87291f7e4a0670a21feca1ebf8dd5e0b5e
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 58%

---

# コミュニティの開発  {#developing-communities}

## 概要 {#overview}

AEM Communities により、フォーラム、ユーザーグループ、ブログ、Q&amp;A、カレンダー、コメント、レビュー、投票、評価、割り当てなどのコミュニティ機能の作成およびカスタマイズが簡素化されます。これらの機能を使用すると、パブリッシュ環境にユーザー生成コンテンツ (UGC) が入力されます。

の基盤 [コミュニティサイト](overview.md#communitiessites) が [ソーシャルコンポーネントフレームワーク](scf.md) (SCF)。 コミュニティサイトの作成は、 [コミュニティサイトテンプレート](sites-console.md) それは [コミュニティ機能](functions.md).

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

* [ソーシャルコンポーネントフレームワーク](scf.md):フレームワークと API の概要。
* [SCF Handlebars ヘルパー](handlebars-helpers.md):デフォルトのヘルパーとカスタムヘルパーの書き込み方法。
* [クライアント側のカスタマイズ](client-customize.md):ブラウザーで実行するコードのカスタマイズ。
* [サーバー側のカスタマイズ](server-customize.md):サーバー上で実行するコードのカスタマイズ。
* [ストレージリソースプロバイダー (SRP)](srp.md):コミュニティコンテンツストレージの概要。
* [コーディングのガイドライン](code-guide.md):ガイドライン、ヒント、テクニック。
* [コミュニティコンポーネントガイド](components-guide.md):インタラクティブ開発ツール。

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

[コミュニティグループ](overview.md#communitygroups)は、コミュニティメンバーがコミュニティサイト内でサブコミュニティを形成できるようにする概念です。コミュニティグループの作成は、パブリッシュ環境またはオーサー環境でおこなうことができます。

* [コミュニティグループの基本事項](essentials-groups.md)
* [グループ機能](functions.md#groups-function)
* [コミュニティグループテンプレート](tools-groups.md)
* [ユーザーとユーザーグループの管理](users.md)
* [作成者のコミュニティグループ](creating-groups.md)

## データの管理 {#managing-data}

* [SRP と UGC の基本事項](srp-and-ugc.md) - SRP API ユーティリティメソッドと例
* [タグの基本事項](tag.md)  — コミュニティメンバーが UGC やカタログ化されたイネーブルメントリソースにタグ付けする機能

## チュートリアル {#tutorials}

* [クライアント側チュートリアル](tutorials.md#client-side-customization)
* [サーバー側チュートリアル](tutorials.md#server-side-customization)
* [方法の説明](tutorials.md#how-to-instructions)

## トラブルシューティング {#troubleshooting}

* [トラブルシューティング](troubleshooting.md)
* [既知の問題](/help/release-notes/release-notes.md)

## 関連するコミュニティドキュメント {#related-communities-documentation}

* 訪問 [コミュニティのデプロイ](deploy-communities.md) を参照してください。

* コミュニティサイトの作成、コミュニティサイトテンプレートの設定、コミュニティコンテンツのモデレート、メンバーの管理およびメッセージングの設定については、[コミュニティサイトの管理](administer-landing.md)を参照してください。

* 訪問 [コミュニティコンポーネントのオーサリング](author-communities.md) コミュニティコンポーネントを使用して作成および設定する方法を学ぶには、以下を参照してください。
