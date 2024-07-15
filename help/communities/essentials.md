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

Adobe Experience Manager（AEM） Communities の機能を使用するには、サイト訪問者がコンテンツを投稿する前に、メンバーになり、[ コミュニティサイト ](overview.md#communitiessites) にログインする必要があります。 したがって、コミュニティサイトを [ 作成 ](sites-console.md) する [ コミュニティサイトテンプレート ](sites.md) は、ログイン機能とユーザープロファイル、メッセージング、検索、モデレート、翻訳を含むように設計されています。

コミュニティ サイトは、選択したコミュニティ サイト テンプレートに [ コミュニティ グループ機能 ](functions.md#groups-function) が含まれている場合、コミュニティ グループを作成するメンバをサポートします。

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
* [ ブログ ](blog-developer-basics.md) （`Journal`）

* [Calendar](calendar-basics-for-developers.md)
* [おすすめコンテンツ](essentials-featured.md)
* [ファイルライブラリ](essentials-file-library.md)
* [フォーラム](essentials-forum.md)
* [グループ](essentials-groups.md)
* [アイディエーション](ideation.md)
* [リーダーボード](leaderboard.md)
* [ 質疑応答 ](qna-essentials.md)`(QnA)`

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
* [ ストレージリソースプロバイダー ](srp-and-ugc.md) `(SRP)`

* [タグ付け](tag.md)

## Javadocs {#javadocs}

[online javadocs](../../help/sites-developing/reference-materials.md) は、AEM 6.3 リリースで使用可能な API を反映しています。
Communities API は `com.adobe.cq.social.*` パッケージに含まれています。

[ 機能パック ](deploy-communities.md#latestfeaturepack) ごとに、Javadoc JAR が使用可能になります。 詳しくは、[ コミュニティでの Maven の使用 ](maven.md#javadocs) を参照してください。

## 追加情報 {#additional-information}

* [ソーシャルコンポーネントフレームワーク（SCF）](scf.md)

   * [クライアントサイドのカスタマイズ](client-customize.md)
   * [サーバーサイドのカスタマイズ](server-customize.md)
   * [ストレージリソースプロバイダーの概要](srp.md)

* [コーディングのガイドライン](code-guide.md)
* [チュートリアル](tutorials.md)
* [トラブルシューティング](troubleshooting.md)
