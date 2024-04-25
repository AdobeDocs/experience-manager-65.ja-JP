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

この `Community Activity List` コンポーネントを使用すると、メンバー別の投稿とビュー、およびコンテンツの投稿とビューに関するトレンド情報を追加できます。

このドキュメントでは、次の内容について説明します。

* の追加 `Community Activity List` コンポーネントからへ [コミュニティサイト](/help/communities/overview.md#community-sites).

* の設定 `Community Activity List` コンポーネント。

### 要件 {#requirement}

のデータ `Community Activity List` は、Adobe Analyticsがコミュニティサイトのライセンスを取得して設定されている場合にのみ使用できます。

参照： [コミュニティ機能のための Analytics 設定](/help/communities/analytics.md).

### ページへのコミュニティアクティビティリストの追加 {#adding-a-community-activity-list-to-a-page}

を追加します `Community Activity List` オーサーモードのページへのコンポーネントの移動 `Communities / Community Activity List` ページ上にドラッグして配置します。

詳細については、 [Communities コンポーネントの基本](/help/communities/basics.md).

コミュニティサイトのページに初めて配置すると、コンポーネントは次のように表示されます。

![地域活動](assets/community-activity.png)

### コミュニティアクティビティリストの設定  {#configuring-community-activity-list}

配置されたを選択します。 `Community Activity List` コンポーネントを選択してから、 `Configure` アイコンをクリックして、編集ダイアログボックスを開きます。

![設定](assets/configure-new.png)

の下 **コメント** タブで、アップロードしたファイルのコメントを表示するかどうかと、どのように表示するかを指定します。

![プロパティ](assets/activity-list-properties.png)

* **タイプ**

  コミュニティメンバーに関するデータと、ユーザー生成コンテンツ（UGC）に関するデータのどちらを表示するかを指定します。

  次から選択します。

   * `Members`
   * `Content`

  デフォルトは `Members` です。

* **タイトルを表示**

  データの上に表示する説明的なタイトル（例：） `Trending Content`.
デフォルトはタイトルなし。

* **表示数**

  リストする項目の数。
デフォルトは 10 です。

* **アクティビティタイプ**

  次のいずれかを選択します。

   * `Views`（ページ訪問）
   * `Posts`（UGC の作成）
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

  選択解除（オフ）すると、上位レベルの支柱のみがカウントされます。 例えば、コンテキストがルートページ（デフォルト）の場合、 `Activity Type` 件中 `Posts` ルートページにコンテンツを投稿する機能がないので、はアクティビティを表示しません。 オンにすると、すべての下位ページのカウントが含まれます。
デフォルトではオンになっています。

### 4 つのコンポーネントを持つページの例 {#example-page-with-components}

**上位の訪問者** 設定：Type = Members、Activity type = Views

**トップの貢献者** config: Type = Members, Activity type = Posts

**トップ コンテンツ** config: Type = Content, Activity type = Views,

**コンテンツのトレンド** 設定：タイプ = コンテンツ、アクティビティタイプ =投稿

![components](assets/activity-list-components.png)
