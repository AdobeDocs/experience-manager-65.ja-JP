---
title: アクティビティのトレンド
description: ページへのコミュニティアクティビティリストコンポーネントの追加
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
docset: aem65
exl-id: 2a4297e4-2d88-4fa6-8fea-3fea06753605
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 4%

---

# アクティビティのトレンド {#activity-trends}

## はじめに {#introduction}

`Community Activity List` コンポーネントを使用すると、メンバー別の投稿とビュー、およびコンテンツの投稿とビューに関するトレンド情報を追加できます。

このドキュメントでは、次の内容について説明します。

* `Community Activity List` コンポーネントを [ コミュニティサイト ](/help/communities/overview.md#community-sites) に追加します。

* `Community Activity List` コンポーネントの設定。

### 要件 {#requirement}

`Community Activity List` のデータは、Adobe Analyticsがコミュニティサイトのライセンスを取得して設定されている場合にのみ使用できます。

[ コミュニティ機能のための Analytics 設定 ](/help/communities/analytics.md) を参照してください。

### ページへのコミュニティアクティビティリストの追加 {#adding-a-community-activity-list-to-a-page}

オーサーモードで `Community Activity List` コンポーネントをページに追加するには、コンポーネント `Communities / Community Activity List` を見つけてページ上にドラッグします。

必要な情報については、[Communities コンポーネントの基本 ](/help/communities/basics.md) を参照してください。

コミュニティサイトのページに初めて配置すると、コンポーネントは次のように表示されます。

![ コミュニティ アクティビティ ](assets/community-activity.png)

### コミュニティアクティビティリストの設定  {#configuring-community-activity-list}

配置した `Community Activity List` コンポーネントを選択し、「`Configure`」アイコンを選択して「編集」ダイアログボックスを開きます。

![ 設定 ](assets/configure-new.png)

「**コメント**」タブで、アップロードしたファイルのコメントを表示するかどうか、および表示方法を指定します。

![プロパティ](assets/activity-list-properties.png)

* **タイプ**

  コミュニティメンバーに関するデータと、ユーザー生成コンテンツ（UGC）に関するデータのどちらを表示するかを指定します。

  次から選択します。

   * `Members`
   * `Content`

  デフォルトは `Members` です。

* **タイトルを表示**

  データの上に表示する説明的なタイトル（`Trending Content` など）。
デフォルトはタイトルなし。

* **表示数**

  リストする項目の数。
デフォルトは 10 です。

* **アクティビティタイプ**

  次のいずれかを選択します。

   * `Views` （ページ訪問数）
   * `Posts` （UGC の作成）
   * `Follows`
   * `Likes`

  デフォルトはビューです。

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

  これにより、アクティビティを、特定のブログなど、サイトのサブセットに限定できます。
デフォルトはコミュニティサイト全体です。

* **メンバー数の集計**

  選択解除（オフ）すると、上位レベルの支柱のみがカウントされます。 例えば、コンテキストがルートページ（デフォルト）の場合は、コンテンツをルートページに投稿する機能がないので、`Posts` の `Activity Type` はアクティビティを表示しません。 オンにすると、すべての下位ページのカウントが含まれます。
デフォルトではオンになっています。

### 4 つのコンポーネントを持つページの例 {#example-page-with-components}

**上位訪問者** 設定：Type = Members、Activity type = Views

**上位の投稿者** 設定：Type = Members, Activity type = Posts

**上位のコンテンツ** 設定：Type = コンテンツ、Activity type = ビュー、

**コンテンツのトレンド** 設定：Type = コンテンツ、Activity type =投稿

![components](assets/activity-list-components.png)
