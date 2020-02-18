---
title: 検索機能
seo-title: 検索機能
description: コミュニティサイトへの検索の追加と設定
seo-description: コミュニティサイトへの検索の追加と設定
uuid: ca633456-911f-447f-881e-653533125d5f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 3acac082-efbe-4995-b374-851cb9aaf62d
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 検索機能 {#search-feature}

検索機能は、フォーラムなど他の様々な機能と連携して、コンテンツを検索できるようにします。

When adding the ability to search posts entered by community members, referred to as user generated content (UGC), there are two components: [ `Search`](#search) and [ `Search Results`](#search-results).

The page that includes the `Search Results` component supports both searching and the display of results.

The page that includes the `Search`component provides a place to launch a search with results appearing on the `Search Results` page.

検索機能は、サイト訪問者やメンバーに向けてコンテンツを表示する他の機能と共に使用できます。

## 検索 {#search-features}

### 検索をページに追加 {#add-search-to-a-page}

作成者モードでペ `Search` ージにコンポーネントを追加するには、コンポーネントブラウザを使用してコンポーネントを `Communities / Search` 検索し、ページ上の所定の位置にドラッグします。 の使用に `Search` は、 `Search Results.`

For necessary information, visit [Communities Components Basics](basics.md).

When the required client-side library, `cq.social.hbs.search`, is included, this is how the `Search` component will appear.

![chlimage_1-373](assets/chlimage_1-373.png)

### 追加した検索を設定 {#configure-the-added-search}

Select the placed `Search` component to access and select the `Configure` icon which opens the edit dialog.

![chlimage_1-374](assets/chlimage_1-374.png)

Under the **[!UICONTROL Search Settings]** tab, specify how what paths are are search when a query is entered by a visitor.

![chlimage_1-375](assets/chlimage_1-375.png)

* **[!UICONTROL 検索パス]**「項目を追加」ボタンを使用して検索パスを追加すると、コンテンツの検索が限定されます。例えば、検索を特定のフォーラムに限定するには、ページ内に配置するフォーラムコンポーネントを選択します。

   * `/content/community-components/en/forum/jcr:content/content/forum`

* **[!UICONTROL 結果ページ]**：結果は、ブラウザーを使用してコンポーネントを含むページを選択することで指定された別のページに表示さ `Search Results` れます。

## 検索結果 {#search-results}

### 検索結果をページに追加 {#add-search-results-to-a-page}

To add a `Search Results` component to a page in author mode, use the component browser to locate

* `Communities / Search Results`

コンポーネントを探し、ページ上の位置にドラッグします。検索コンポーネントとは異なり、2番目のページは必要ありません。結果は同じページに表示されます。

If using Search elsewhere within the website, this one page with `Search Results` may be configured to be the `Result Page` for any or all instances of `Search`.

For necessary information, visit [Communities Components Basics](basics.md).

When the required client-side library, `cq.social.hbs.search`, is included, this is how the `Search Result` component will appear:

![chlimage_1-376](assets/chlimage_1-376.png)

### 追加した検索結果を設定 {#configure-the-added-search-result}

Select the placed `Search Results` component to access and select the `Configure` icon which opens the edit dialog.

![chlimage_1-377](assets/chlimage_1-377.png)

Under the **[!UICONTROL Search Result Settings]** tab, it is possible to specify what paths are included in the search when a query is entered by a visitor.

![chlimage_1-378](assets/chlimage_1-378.png)

* **[!UICONTROL 1 ページの検索結果数]** 1 ページに表示するトピック数または投稿数を定義します。初期設定は 10 です。

* **[!UICONTROL 検索パス]**「項目を追加」ボタンを使用して検索パスを追加すると、コンテンツの検索が限定されます。

## 追加情報 {#additional-information}

More information may be found on the [Search Essentials](search-implementation.md) page for developers.
