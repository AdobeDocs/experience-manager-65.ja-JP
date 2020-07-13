---
title: コンポーネントおよび機能の基本事項
seo-title: コンポーネントおよび機能の基本事項
description: コミュニティサイト、テンプレート、グループの機能
seo-description: コミュニティサイト、テンプレート、グループの機能
uuid: 6edfca2d-fe5b-4261-b033-51dc2f9dbfd7
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 2d308756-79d1-4d69-b51c-d4b6e692a137
translation-type: tm+mt
source-git-commit: c897f034edbdbeee74869165ed384c3408a857e0
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 71%

---


# コンポーネントおよび機能の基本事項  {#component-function-and-feature-essentials}

サイト訪問者が AEM Communities の機能を使用し、コンテンツを投稿するには、事前にメンバー登録し、[コミュニティサイト](overview.md#communitiessites)にログインする必要があります。Thus, [community site templates](sites.md), from which a community site is [created](sites-console.md), are designed to include a login feature as well as user profiles, messaging, search, moderation, and translation.

A community site will support members creating community groups when the [community groups function](functions.md#groups-function) is included in the selected community site template.

次のリンクをクリックすると、コミュニティのコンポーネントおよび機能に関する基本情報にアクセスできます。

## 基本コンポーネント {#base-components}

* [コメント](essentials-comments.md)
* [レビュー](reviews-basics.md)
* [集計](tally.md)

   * [「いいね!」の設定](essentials-liking.md)
   * [評価](rating-basics.md)
   * [投票](essentials-voting.md)
   * *投票（使用できなくなりました）*

## 機能のあるコンポーネント {#components-with-functions}

* [アクティビティストリーム](essentials-activities.md)
* [割り当て](essentials-assignments.md)
* [ブログ](blog-developer-basics.md) ( `Journal`)

* [カレンダー](calendar-basics-for-developers.md)
* [カタログ](catalog-developer-essentials.md)
* [おすすめコンテンツ](essentials-featured.md)
* [ファイルライブラリ](essentials-file-library.md)
* [フォーラム](essentials-forum.md)
* [グループ](essentials-groups.md)
* [アイディエーション](ideation.md)
* [リーダーボード](leaderboard.md)
* [質問と回答](qna-essentials.md) `(QnA)`

## 特長 {#features}

* [クライアントライブラリ](clientlibs.md)
* [コミュニティサイト](sites-for-developers.md)
* [コンポーネントの OSGi イベント](events.md)
* [コンポーネントのサイドローディング](sideloading.md)
* [メッセージ](essentials-messaging.md)
* [リッチテキストエディター](rte.md)
* [スコアとバッジ](configure-scoring.md)
* [検索](search-implementation.md)
* [ソーシャルグラフ](essentials-socialgraph.md)
* [ストレージリソースプロバイダ](srp-and-ugc.md) `(SRP)`

* [タグ付け](tag.md)

## Javadoc {#javadocs}

[オンライン javadoc](../../help/sites-developing/reference-materials.md) には、AEM 6.3 リリースで使用できる API が反映されています。Communities APIs are in `com.adobe.cq.social.*` packages.

各[機能パック](deploy-communities.md#latestfeaturepack)に対し、javadoc jar が提供されます。詳しくは、[Communities 用 Maven の使用](maven.md#javadocs)を参照してください。

## 追加情報 {#additional-information}

* [ソーシャルコンポーネントフレームワーク（SCF）](scf.md)

   * [クライアント側のカスタマイズ](client-customize.md)
   * [サーバー側のカスタマイズ](server-customize.md)
   * [ストレージリソースプロバイダーの概要](srp.md)

* [コーディングのガイドライン](code-guide.md)
* [チュートリアル](tutorials.md)
* [トラブルシューティング](troubleshooting.md)

