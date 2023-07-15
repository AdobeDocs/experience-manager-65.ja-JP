---
title: コンポーネントおよび機能の基本事項
description: コミュニティサイト、テンプレート、グループの機能
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: a43c1c4d-a6c2-4ef9-9047-a945978e618b
source-git-commit: e161c37544c3391607cbe495644f3353b9f77fe3
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 26%

---

# コンポーネントおよび機能の基本事項  {#component-function-and-feature-essentials}

Adobe Experience Manager(AEM)Communities の機能を使用するには、サイトの訪問者がメンバーになり、 [コミュニティサイト](overview.md#communitiessites) コンテンツを投稿できるようになります。 このように [コミュニティサイトテンプレート](sites.md)（コミュニティサイトの場所） [作成済み](sites-console.md)は、ログイン機能とユーザープロファイル、メッセージング、検索、モデレート、翻訳を含むように設計されています。

コミュニティサイトでは、 [コミュニティグループ機能](functions.md#groups-function) 選択したコミュニティサイトテンプレートに含まれています。

コミュニティのコンポーネント、機能、機能に関する重要な情報へのリンクを次に示します。

## 基本コンポーネント {#base-components}

* [コメント](essentials-comments.md)
* [レビュー](reviews-basics.md)
* [集計](tally.md)

   * [「いいね!」の設定](essentials-liking.md)
   * [レーティング](rating-basics.md)
   * [投票](essentials-voting.md)
   * *投票（利用不可）*

## 関数を持つコンポーネント {#components-with-functions}

* [アクティビティストリーム](essentials-activities.md)
* [ブログ](blog-developer-basics.md) ( `Journal`)

* [Calendar](calendar-basics-for-developers.md)
* [おすすめコンテンツ](essentials-featured.md)
* [ファイルライブラリ](essentials-file-library.md)
* [フォーラム](essentials-forum.md)
* [グループ](essentials-groups.md)
* [アイディエーション](ideation.md)
* [リーダーボード](leaderboard.md)
* [質問と答え](qna-essentials.md) `(QnA)`

## 機能 {#features}

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

## Javadocs {#javadocs}

この [オンライン javadoc](../../help/sites-developing/reference-materials.md) AEM 6.3 リリースで使用可能な API を反映しています。
コミュニティ API は、 `com.adobe.cq.social.*` パッケージ。

各 [機能パック](deploy-communities.md#latestfeaturepack)の場合、javadoc jar が使用可能になります。 詳しくは、 [コミュニティでの Maven の使用](maven.md#javadocs).

## 追加情報 {#additional-information}

* [ソーシャルコンポーネントフレームワーク (SCF)](scf.md)

   * [クライアント側のカスタマイズ](client-customize.md)
   * [サーバー側のカスタマイズ](server-customize.md)
   * [ストレージリソースプロバイダーの概要](srp.md)

* [コーディングのガイドライン](code-guide.md)
* [チュートリアル](tutorials.md)
* [トラブルシューティング](troubleshooting.md)
