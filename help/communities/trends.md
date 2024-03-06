---
title: アクティビティのトレンド
description: コミュニティアクティビティリストコンポーネントをページに追加する
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 2a4297e4-2d88-4fa6-8fea-3fea06753605
source-git-commit: 518207a0d8a95ef17b0972855a58f124fb215c85
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 5%

---

# アクティビティのトレンド {#activity-trends}

## はじめに {#introduction}

The `Community Activity List` コンポーネントを使用すると、メンバー別の投稿およびビューや、コンテンツの投稿およびビューに関するトレンド情報を追加できます。

このドキュメントでは、次の内容について説明します。

* の追加 `Community Activity List` コンポーネントを [コミュニティサイト](/help/communities/overview.md#community-sites).

* の設定 `Community Activity List` コンポーネント。

### 要件 {#requirement}

のデータ `Community Activity List` は、Adobe Analyticsがコミュニティサイトに対してライセンスを取得し、設定されている場合にのみ使用できます。

詳しくは、 [コミュニティ機能用の Analytics 設定](/help/communities/analytics.md).

### コミュニティアクティビティリストをページに追加する {#adding-a-community-activity-list-to-a-page}

を追加するには、以下を実行します。 `Community Activity List` コンポーネントをオーサリングモードでページに追加する場合は、 `Communities / Community Activity List` をクリックし、ページ上の適切な場所にドラッグします。

必要な情報については、 [コミュニティコンポーネントの基本](/help/communities/basics.md).

コミュニティサイトのページに最初に配置したとき、コンポーネントは次のように表示されます。

![community-activity](assets/community-activity.png)

### コミュニティアクティビティリストの設定  {#configuring-community-activity-list}

配置した `Community Activity List` コンポーネントを選択し、 `Configure` アイコンをクリックして、編集ダイアログボックスを開きます。

![設定](assets/configure-new.png)

の下 **コメント** タブで、アップロードされたファイルのコメントを表示するかどうかと表示する方法を指定します。

![プロパティ](assets/activity-list-properties.png)

* **タイプ**

  コミュニティメンバーに関するデータを表示するか、ユーザー生成コンテンツ (UGC) に関するデータを表示するかを指定します。

  次から選択します。

   * `Members`
   * `Content`

  デフォルトは `Members` です。

* **タイトルを表示**

  データの上に表示する説明的なタイトル（例： ） `Trending Content`.
初期設定ではタイトルはありません。

* **表示数**

  リストする項目の数。
デフォルトは 10 です。

* **アクティビティタイプ**

  次のいずれかを選択します。

   * `Views`（訪問ページ数）
   * `Posts`（UGC の作成）
   * `Follows`
   * `Likes`

  デフォルトは Views です。

* **期間**

  次のいずれかを選択します。

   * `Last 24 hours`
   * `Last 7 days`
   * `Last 30 days`
   * `Last 90 days`
   * `This year (since Jan 1)`
   * `Total`

  デフォルトは `Total` です。

* **コンテキストパス**

  これにより、特定のブログなど、サイトのサブセットに対するアクティビティの範囲を設定できます。
デフォルトはコミュニティサイト全体です。

* **メンバー数の集計**

  選択を解除（オフ）すると、最上位の投稿のみがカウントされます。 例えば、コンテキストがルートページ（デフォルト）の場合、 `Activity Type` / `Posts` ルートページにコンテンツを投稿できないので、「 」アクティビティは表示されません。 オンにすると、すべての下位のページのカウントが含まれます。
初期設定はオンです。

### 4 つのコンポーネントを持つページの例 {#example-page-with-components}

**上位の訪問者** config: Type = Members、Activity type = Views

**上位の寄稿者** config: Type = Members、Activity type = Posts

**上位のコンテンツ** config: Type = Content、Activity type = Views、

**コンテンツのトレンド** config: Type = Content、Activity type = Posts

![components](assets/activity-list-components.png)
