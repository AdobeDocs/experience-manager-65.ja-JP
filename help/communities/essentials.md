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
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 24%
---
# コンポーネントおよび機能の基本事項  {#component-function-and-feature-essentials}

Adobe Experience Manager （AEM） Communitiesの機能では、コンテンツを投稿する前に、サイト訪問者がメンバーになり、[&#x200B; コミュニティサイト &#x200B;](overview.md#communitiessites)にログインする必要があります。 したがって、コミュニティサイトが[作成](sites-console.md)される[&#x200B; コミュニティサイトテンプレート &#x200B;](sites.md)は、ログイン機能とユーザープロファイル、メッセージ、検索、モデレーション、翻訳を含むように設計されています。

[&#x200B; コミュニティグループ関数](functions.md#groups-function)が選択したコミュニティサイトテンプレートに含まれている場合、コミュニティサイトでは、メンバーによるコミュニティグループの作成がサポートされます。

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
* [&#x200B; ブログ &#x200B;](blog-developer-basics.md) （`Journal`）

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
* [&#x200B; ストレージリソースプロバイダー](srp-and-ugc.md) `(SRP)`

* [タグ付け](tag.md)

## Javadocs {#javadocs}

[&#x200B; オンライン javadocs](../../help/sites-developing/reference-materials.md)は、AEM 6.3 リリースで使用可能なAPIを反映しています。
Communities APIは`com.adobe.cq.social.*` パッケージに含まれています。

各[機能パック &#x200B;](deploy-communities.md#latestfeaturepack)に対して、javadoc jarが使用可能になります。 詳しくは、[Maven for Communitiesの使用](maven.md#javadocs)を参照してください。

## 追加情報 {#additional-information}

* [ソーシャルコンポーネントフレームワーク（SCF）](scf.md)

  * [クライアントサイドのカスタマイズ](client-customize.md)
  * [サーバーサイドのカスタマイズ](server-customize.md)
  * [ストレージリソースプロバイダーの概要](srp.md)

* [コーディングのガイドライン](code-guide.md)
* [チュートリアル](tutorials.md)
* [トラブルシューティング](troubleshooting.md)
