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
exl-id: 2a4297e4-2d88-4fa6-8fea-3fea06753605
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 39%

---

# アクティビティのトレンド {#activity-trends}

## はじめに {#introduction}

`Community Activity List`コンポーネントを使用すると、メンバーによる投稿および表示に関するトレンド情報や、コンテンツの投稿および表示を追加できます。

このドキュメントでは、次の内容について説明します。

* `Community Activity List`コンポーネントを[コミュニティサイト](/help/communities/overview.md#community-sites)に追加します。

* `Community Activity List`コンポーネントの設定。

### 要件 {#requirement}

`Community Activity List`のデータは、Adobe Analyticsがライセンスを受け、コミュニティサイトに対して設定されている場合にのみ使用できます。

[コミュニティ機能のための Analytics の設定](/help/communities/analytics.md)を参照してください。

### コミュニティのアクティビティリストをページに追加  {#adding-a-community-activity-list-to-a-page}

`Community Activity List`コンポーネントをオーサリングモードでページに追加するには、

* `Communities / Community Activity List`

コンポーネントを探し、ページ上の位置にドラッグします。

必要な情報については、[コミュニティコンポーネントの基本](/help/communities/basics.md)を参照してください。

コミュニティサイトのページに初めて配置されたとき、コンポーネントは次のように表示されます。

![community-activity](assets/community-activity.png)

### コミュニティのアクティビティリストの設定  {#configuring-community-activity-list}

配置済みの`Community Activity List`コンポーネントを選択し、`Configure`アイコンを選択すると、編集ダイアログが開きます。

![設定](assets/configure-new.png)

「**コメント**」タブでは、アップロードしたファイルに対するコメントを表示するかどうかと、その方法を指定します。

![プロパティ](assets/activity-list-properties.png)

* **型**

   コミュニティメンバーに関するデータを表示するか、ユーザー生成コンテンツ(UGC)を表示するかを指定します。

   次から選択：

   * `Members`
   * `Content`

   デフォルトは `Members` です。

* **表示タイトル**

   データの上に表示する説明的なタイトル（`Trending Content`など）。
初期設定では、タイトルはありません。

* **表示数**

   リストする項目の数。
初期設定は 10 です。

* **アクティビティタイプ**

   次のいずれかを選択します。

   * `Views`（訪問ページ数）
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

   特定のブログなど、サイトのサブセットに対するアクティビティの範囲を設定できます。
初期設定は、コミュニティサイト全体です。

* **メンバー数の集計**

   選択を解除（オフ）すると、最上位の投稿のみがカウントされます。 例えば、コンテキストがルートページ（デフォルト）の場合、`Posts`の`Activity Type`は、ルートページにコンテンツを投稿できないので、アクティビティを表示しません。 オンにすると、すべての下位のページがカウントに含まれます。初期設定はオンです。

### 4 つのコンポーネントがあるページの例 {#example-page-with-components}

**上位の訪問者**&#x200B;の設定：タイプ = メンバー、アクティビティタイプ = ビュー

**上位の** 投稿者の設定：タイプ=メンバー、アクティビティタイプ=投稿

**上位の** Contentconfig:タイプ=コンテンツ、アクティビティタイプ=ビュー

**Contentconfigのト** レンド分析：タイプ=コンテンツ、アクティビティタイプ=投稿

![コンポーネント](assets/activity-list-components.png)
