---
title: コンポーネントおよび機能の基本事項
description: コミュニティサイト、テンプレート、グループの機能
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: a43c1c4d-a6c2-4ef9-9047-a945978e618b
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 24%
---
# コンポーネントおよび機能の基本事項  {#component-function-and-feature-essentials}

Adobe Experience Manager （AEM） Communitiesの機能では、コンテンツを投稿する前に、サイト訪問者がメンバーになり、[ コミュニティサイト ](overview.md#communitiessites)にログインする必要があります。 したがって、コミュニティサイトが[作成](sites-console.md)される[ コミュニティサイトテンプレート ](sites.md)は、ログイン機能とユーザープロファイル、メッセージ、検索、モデレーション、翻訳を含むように設計されています。

[ コミュニティグループ関数](functions.md#groups-function)が選択したコミュニティサイトテンプレートに含まれている場合、コミュニティサイトでは、メンバーによるコミュニティグループの作成がサポートされます。

次に、コミュニティのコンポーネント、機能、および機能に関する重要な情報へのリンクを示します。

## ベースコンポーネント {#base-components}

* [コメント](essentials-comments.md)
* [レビュー](reviews-basics.md)
* [集計](tally.md)

  * [「いいね!」の設定](essentials-liking.md)
  * [レーティング](rating-basics.md)
  * [投票](essentials-voting.md)
  * *調査（使用できなくなりました）*

## 関数を含むコンポーネント {#components-with-functions}

* [アクティビティストリーム](essentials-activities.md)
* [ ブログ ](blog-developer-basics.md) （`Journal`）

* [Calendar](calendar-basics-for-developers.md)
* [おすすめコンテンツ](essentials-featured.md)
* [ファイルライブラリ](essentials-file-library.md)
* [フォーラム](essentials-forum.md)
* [グループ](essentials-groups.md)
* [アイディエーション](ideation.md)
* [リーダーボード](leaderboard.md)
* [質問と回答](qna-essentials.md) `(QnA)`

## 機能 {#features}

* [クライアントライブラリ](clientlibs.md)
* [コミュニティサイト](sites-for-developers.md)
* [コンポーネント OSGi イベント](events.md)
* [コンポーネントのサイドローディング](sideloading.md)
* [メッセージ](essentials-messaging.md)
* [リッチテキストエディター](rte.md)
* [スコアリングとバッジ](configure-scoring.md)
* [検索](search-implementation.md)
* [ソーシャルグラフ](essentials-socialgraph.md)
* [ ストレージリソースプロバイダー](srp-and-ugc.md) `(SRP)`

* [タグ付け](tag.md)

## Javadocs {#javadocs}

[ オンライン javadocs](../../help/sites-developing/reference-materials.md)は、AEM 6.3 リリースで使用可能なAPIを反映しています。
Communities APIは`com.adobe.cq.social.*` パッケージに含まれています。

各[機能パック ](deploy-communities.md#latestfeaturepack)に対して、javadoc jarが使用可能になります。 詳しくは、[Maven for Communitiesの使用](maven.md#javadocs)を参照してください。

## 追加情報 {#additional-information}

* [ソーシャルコンポーネントフレームワーク（SCF）](scf.md)

  * [クライアントサイドのカスタマイズ](client-customize.md)
  * [サーバーサイドのカスタマイズ](server-customize.md)
  * [ストレージリソースプロバイダーの概要](srp.md)

* [コーディングのガイドライン](code-guide.md)
* [チュートリアル](tutorials.md)
* [トラブルシューティング](troubleshooting.md)
