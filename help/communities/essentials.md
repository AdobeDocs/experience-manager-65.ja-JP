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
exl-id: a43c1c4d-a6c2-4ef9-9047-a945978e618b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 71%

---

# コンポーネントおよび機能の基本事項   {#component-function-and-feature-essentials}

サイト訪問者が AEM Communities の機能を使用し、コンテンツを投稿するには、事前にメンバー登録し、[コミュニティサイト](overview.md#communitiessites)にログインする必要があります。したがって、コミュニティサイトが[作成](sites-console.md)される[コミュニティサイトテンプレート](sites.md)には、ログイン機能と、ユーザープロファイル、メッセージング、検索、モデレート、翻訳が含まれます。

選択したコミュニティサイトテンプレートに[コミュニティグループ機能](functions.md#groups-function)が含まれると、コミュニティサイトでコミュニティグループの作成がサポートされます。

次のリンクをクリックすると、コミュニティのコンポーネントおよび機能に関する基本情報にアクセスできます。

## 基本コンポーネント  {#base-components}

* [コメント](essentials-comments.md)
* [レビュー](reviews-basics.md)
* [集計](tally.md)

   * [「いいね!」の設定](essentials-liking.md)
   * [評価](rating-basics.md)
   * [投票](essentials-voting.md)
   * *投票（利用不可）*

## 機能のあるコンポーネント {#components-with-functions}

* [アクティビティストリーム](essentials-activities.md)
* [割り当て](essentials-assignments.md)
* [ブログ](blog-developer-basics.md) ( `Journal`)

* [Calendar](calendar-basics-for-developers.md)
* [カタログ](catalog-developer-essentials.md)
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
* [スコアとバッジ](configure-scoring.md)
* [検索](search-implementation.md)
* [ソーシャルグラフ](essentials-socialgraph.md)
* [ストレージリソースプロバイダ](srp-and-ugc.md) `(SRP)`

* [タグ付け](tag.md)

## Javadoc {#javadocs}

[オンライン javadoc](../../help/sites-developing/reference-materials.md) には、AEM 6.3 リリースで使用できる API が反映されています。コミュニティAPIは`com.adobe.cq.social.*`パッケージに含まれています。

各[機能パック](deploy-communities.md#latestfeaturepack)に対し、javadoc jar が提供されます。詳しくは、[Communities 用 Maven の使用](maven.md#javadocs)を参照してください。

## 追加情報 {#additional-information}

* [ソーシャルコンポーネントフレームワーク（SCF）](scf.md)

   * [クライアント側のカスタマイズ](client-customize.md)
   * [サーバー側のカスタマイズ](server-customize.md)
   * [ストレージリソースプロバイダーの概要](srp.md)

* [コーディングのガイドライン](code-guide.md)
* [チュートリアル](tutorials.md)
* [トラブルシューティング](troubleshooting.md)
