---
title: アクティビティのトレンド
seo-title: アクティビティのトレンド
description: コミュニティのアクティビティリストコンポーネントをページに追加
seo-description: コミュニティのアクティビティリストコンポーネントをページに追加
uuid: 316aabf7-01a5-46da-be59-70c206eb6a3d
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 4a0debdd-acb9-4646-80bb-fec66fae4088
docset: aem65
translation-type: tm+mt
source-git-commit: 77d00c1d6e94b257aa0533ca88b5f9a12dba0054

---


# アクティビティのトレンド {#activity-trends}

## 概要 {#introduction}

The `Community Activity List` component provides the ability to add trending information regarding posts and views by members as well as posts and views of content.

このドキュメントでは、次の内容を説明します。

* Adding the `Community Activity List` component to a [community site](/help/communities/overview.md#community-sites).

* Configuration settings for the `Community Activity List` component.

### 要件 {#requirement}

Data for the `Community Activity List` is only available when Adobe Analytics is licensed and configured for the community site.

[コミュニティ機能のための Analytics の設定](/help/communities/analytics.md)を参照してください。

### コミュニティのアクティビティリストをページに追加 {#adding-a-community-activity-list-to-a-page}

To add a `Community Activity List` component to a page in author mode, locate the component

* `Communities / Community Activity List`

コンポーネントを探し、ページ上の位置にドラッグします。

For necessary information, visit [Communities Components Basics](/help/communities/basics.md).

コミュニティサイトのページに初めて配置されたとき、コンポーネントは次のように表示されます。

![chlimage_1-54](assets/chlimage_1-54.png)

### コミュニティのアクティビティリストの設定  {#configuring-community-activity-list}

Select the placed `Community Activity List` component to access and select the `Configure` icon which opens the edit dialog.

![chlimage_1-55](assets/chlimage_1-55.png)

「**コメント**」タブでは、アップロードしたファイルに対するコメントを表示するかどうかと、その方法を指定します。

![chlimage_1-56](assets/chlimage_1-56.png)

* **タイプ**

   コミュニティメンバーに関するデータを表示するか、ユーザー生成コンテンツ(UGC)を表示するかを指定します。

   次から選択：

   * `Members`
   * `Content`
   デフォルトは `Members` です。

* **表示タイトル**

   データの上に表示する説明的なタイトル（など） `Trending Content`。
初期設定では、タイトルはありません。

* **表示数**

   アイテムのリスト数。
初期設定は 10 です。

* **アクティビティタイプ**

   次のいずれかを選択します。

   * `Views`（ページ訪問数）
   * `Posts`（UGCの作成）
   * `Follows`
   * `Likes`
   初期設定は「ビュー」です。

* **期間**

   次のいずれかを選択します。

   * `Last 24 hours`
   * `Last 7 days`
   * `Last 30 days`
   * `Last 90 days`
   * `This year (since Jan 1st)`
   * `Total`
   デフォルトは `Total` です。

* **コンテキストパス**

   特定のブログなど、アクティビティをサイトのサブセットに対してスコープできます。
初期設定は、コミュニティサイト全体です。

* **メンバー数の集計**

   選択を解除（オフ）すると、最上位の投稿のみがカウントされます。 For example, if the context is the root page (the default), then an `Activity Type` of `Posts` will never show any activity as there is no ability to post content to the root page. オンにすると、すべての下位のページがカウントに含まれます。初期設定はオンです。

### 4 つのコンポーネントがあるページの例 {#example-page-with-components}

**上位の訪問者**&#x200B;の設定：タイプ = メンバー、アクティビティタイプ = ビュー

**上位の寄稿者** の設定：タイプ=メンバー、アクティビティタイプ=投稿

**Top Content** config:タイプ=コンテンツ、アクティビティタイプ=表示、

**Trending Content** config:タイプ=コンテンツ、アクティビティタイプ=投稿

![chlimage_1-57](assets/chlimage_1-57.png)

