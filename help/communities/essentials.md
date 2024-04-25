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
source-wordcount: '208'
ht-degree: 24%

---

# コンポーネントおよび機能の基本事項  {#component-function-and-feature-essentials}

Adobe Experience Manager（AEM） Communities の機能を使用するには、サイト訪問者がメンバーになり、 [コミュニティサイト](overview.md#communitiessites) コンテンツを投稿する前に。 したがって、 [コミュニティサイトテンプレート](sites.md)、コミュニティサイトがある [作成日](sites-console.md)には、ログイン機能とユーザープロファイル、メッセージング、検索、モデレート、翻訳が含まれるように設計されています。

コミュニティサイトは、次の場合、コミュニティグループを作成するメンバーをサポートします [コミュニティグループ機能](functions.md#groups-function) 選択したコミュニティサイトテンプレートに含まれます。

次に、Communities のコンポーネント、機能、機能に関する基本情報へのリンクを示します。

## 基本コンポーネント {#base-components}

* [コメント](essentials-comments.md)
* [レビュー](reviews-basics.md)
* [集計](tally.md)

   * [「いいね!」の設定](essentials-liking.md)
   * [レーティング](rating-basics.md)
   * [投票](essentials-voting.md)
   * *ポーリング （使用できなくなりました）*

## 関数を含むコンポーネント {#components-with-functions}

* [アクティビティストリーム](essentials-activities.md)
* [ブログ](blog-developer-basics.md) （ `Journal`）

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
* [コンポーネントの OSGi イベント](events.md)
* [コンポーネントのサイドローディング](sideloading.md)
* [メッセージ](essentials-messaging.md)
* [リッチテキストエディター](rte.md)
* [スコアおよびバッジ](configure-scoring.md)
* [検索](search-implementation.md)
* [ソーシャルグラフ](essentials-socialgraph.md)
* [記憶域リソース プロバイダー](srp-and-ugc.md) `(SRP)`

* [タグ付け](tag.md)

## Javadocs {#javadocs}

この [オンライン javadocs](../../help/sites-developing/reference-materials.md) AEM 6.3 リリースで使用可能な API を反映します。
Communities の API は次の場所にあります `com.adobe.cq.social.*` パッケージ。

それぞれに対して [機能パック](deploy-communities.md#latestfeaturepack)を選択すると、javadoc jar が使用可能になります。 詳しくは、次を参照してください [コミュニティでの Maven の使用](maven.md#javadocs).

## 追加情報 {#additional-information}

* [ソーシャルコンポーネントフレームワーク（SCF）](scf.md)

   * [クライアントサイドのカスタマイズ](client-customize.md)
   * [サーバーサイドのカスタマイズ](server-customize.md)
   * [ストレージリソースプロバイダーの概要](srp.md)

* [コーディングのガイドライン](code-guide.md)
* [チュートリアル](tutorials.md)
* [トラブルシューティング](troubleshooting.md)
