---
title: 検索機能
description: Communities サイトへの検索の追加と設定
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: e252b0e5-a2f8-468e-ac8c-951a5b0f2e32
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 2%

---

# 検索機能 {#search-feature}

検索機能は、フォーラムなどのその他の様々な機能と連携して、コンテンツを検索できるようにします。

ユーザー生成コンテンツ（UGC）と呼ばれる、コミュニティメンバーが入力した投稿を検索する機能を追加する場合、[&#x200B; 検索 &#x200B;](#search) と [&#x200B; 検索結果 &#x200B;](#search-results) の 2 つのコンポーネントがあります。

`Search Results` コンポーネントを含むページは、検索と結果の表示の両方をサポートしています。

`Search` コンポーネントを含むページには、検索を開始するための場所が用意されており、検索結果が `Search Results` のページに表示されます。

検索機能は、サイト訪問者やメンバーがコンテンツを表示できるようにする他の機能と併用できます。

## 検索 {#search-features}

### ページに検索を追加 {#add-search-to-a-page}

オーサーモードで `Search` コンポーネントをページに追加するには、コンポーネントブラウザーを使用して `Communities / Search` のコンポーネントを探し、ページ上にドラッグして配置します。 `Search` を使用するには、`Search Results.` に 2 ページ目が必要です

必要な情報については、[Communities コンポーネントの基本 &#x200B;](basics.md) を参照してください。

必要なクライアントサイドライブラリ `cq.social.hbs.search` が含まれている場合、`Search` コンポーネントはこの方法で表示されます。

![add-search](assets/add-search.png)

### 追加した検索を設定する {#configure-the-added-search}

配置した `Search` コンポーネントを選択してアクセスし、「`Configure`」アイコンを選択すると、編集ダイアログが開きます。

![&#x200B; 設定 &#x200B;](assets/configure-new.png)

「**[!UICONTROL 検索設定]**」タブで、訪問者がクエリを入力した際に検索するパスを指定します。

![search-settings](assets/search-settings.png)

* **[!UICONTROL 検索パス]**
「項目を追加」ボタンを使用して検索パスを追加すると、コンテンツの検索が制限されます。 例えば、検索を特定のフォーラムに制限するには、ページ内に配置したフォーラムコンポーネントを選択します。

   * `/content/community-components/en/forum/jcr:content/content/forum`

* **[!UICONTROL 結果ページ]**
結果は、`Search Results` コンポーネントを含むページをブラウザーで選択することにより指定された、別のページに表示されます。

## 検索結果 {#search-results}

### ページへの検索結果の追加 {#add-search-results-to-a-page}

オーサーモードで `Search Results` コンポーネントをページに追加するには、コンポーネントブラウザーを使用して以下を見つけます

* `Communities / Search Results`

ページ上にドラッグして配置します。 検索コンポーネントとは異なり、結果は同じページに表示されるので、2 番目のページは必要ありません。

Web サイト内の他の場所で検索を使用する場合、`Search Results` を含むこの 1 ページは、`Search` の任意またはすべてのインスタンスの `Result Page` として設定できます。

必要な情報については、[Communities コンポーネントの基本 &#x200B;](basics.md) を参照してください。

必要なクライアントサイドライブラリ `cq.social.hbs.search` が含まれている場合、`Search Result` のコンポーネントは次のように表示されます。

![search-result](assets/search-result1.png)

### 追加した検索結果の設定 {#configure-the-added-search-result}

配置した `Search Results` コンポーネントを選択してアクセスし、「`Configure`」アイコンを選択すると、編集ダイアログが開きます。

![&#x200B; 設定 &#x200B;](assets/configure-new.png)

「**[!UICONTROL 検索結果設定]**」タブでは、訪問者がクエリを入力したときに検索に含めるパスを指定できます。

![search-result-settings](assets/search-result-settings.png)

* **[!UICONTROL ページごとの検索結果]**

  ページごとに表示するトピック/投稿の数を定義します。 初期設定は 10 です。

* **[!UICONTROL 検索パス]**

  「項目を追加」ボタンを使用して検索パスを追加すると、コンテンツの検索が制限されます。

## 追加情報 {#additional-information}

詳しくは、開発者向けの [&#x200B; 検索の基本事項 &#x200B;](search-implementation.md) ページを参照してください。
