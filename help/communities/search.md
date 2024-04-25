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

ユーザー生成コンテンツ（UGC）と呼ばれる、コミュニティメンバーが入力した投稿を検索する機能を追加する場合、次の 2 つのコンポーネントがあります。 [検索](#search) および [検索結果](#search-results).

を含むページ `Search Results` コンポーネントは、検索と結果の表示の両方をサポートしています。

を含むページ `Search` コンポーネントは、検索を開始するための場所を提供し、検索結果がに表示されます。 `Search Results` ページ。

検索機能は、サイト訪問者やメンバーがコンテンツを表示できるようにする他の機能と併用できます。

## 検索 {#search-features}

### ページに検索を追加 {#add-search-to-a-page}

を追加します `Search` オーサーモードのページにコンポーネントを追加する場合は、コンポーネントブラウザーを使用して次を見つけます `Communities / Search` ページ上にドラッグして配置します。 使用 `Search` には 2 番目のページが必要です `Search Results.`

詳細については、 [Communities コンポーネントの基本](basics.md).

必要なクライアントサイドライブラリが `cq.social.hbs.search`が含まれます。このようにして、 `Search` コンポーネントが表示されます。

![add-search](assets/add-search.png)

### 追加した検索を設定する {#configure-the-added-search}

配置されたを選択します。 `Search` にアクセスして選択するコンポーネント `Configure` アイコンをクリックします。このアイコンをクリックすると、編集ダイアログが開きます。

![設定](assets/configure-new.png)

の下 **[!UICONTROL 検索設定]** タブで、訪問者がクエリを入力した際のパスの検索方法を指定します。

![search-settings](assets/search-settings.png)

* **[!UICONTROL 検索パス]**
「項目を追加」ボタンを使用して検索パスを追加すると、コンテンツの検索が制限されます。 例えば、検索を特定のフォーラムに制限するには、ページ内に配置したフォーラムコンポーネントを選択します。

   * `/content/community-components/en/forum/jcr:content/content/forum`

* **[!UICONTROL 結果ページ]**
結果は、ブラウザーを使用してを含むページを選択することで指定された、別のページに表示されます。 `Search Results` コンポーネント。

## 検索結果 {#search-results}

### ページへの検索結果の追加 {#add-search-results-to-a-page}

を追加します `Search Results` オーサーモードのページにコンポーネントを追加する場合は、コンポーネントブラウザーを使用して次を見つけます

* `Communities / Search Results`

ページ上にドラッグして配置します。 検索コンポーネントとは異なり、結果は同じページに表示されるので、2 番目のページは必要ありません。

Web サイト内の他の場所で検索を使用する場合、この 1 ページには `Search Results` は、のように設定できます。 `Result Page` の一部またはすべてのインスタンス用 `Search`.

詳細については、 [Communities コンポーネントの基本](basics.md).

必要なクライアントサイドライブラリが `cq.social.hbs.search`が含まれます。このようにして、 `Search Result` コンポーネントが表示されます。

![search-result](assets/search-result1.png)

### 追加した検索結果の設定 {#configure-the-added-search-result}

配置されたを選択します。 `Search Results` にアクセスして選択するコンポーネント `Configure` アイコンをクリックします。このアイコンをクリックすると、編集ダイアログが開きます。

![設定](assets/configure-new.png)

の下 **[!UICONTROL 検索結果設定]** タブを使用すると、訪問者がクエリを入力した際に検索に含めるパスを指定できます。

![search-result-settings](assets/search-result-settings.png)

* **[!UICONTROL ページごとの検索結果]**

  ページごとに表示するトピック/投稿の数を定義します。 初期設定は 10 です。

* **[!UICONTROL 検索パス]**

  「項目を追加」ボタンを使用して検索パスを追加すると、コンテンツの検索が制限されます。

## 追加情報 {#additional-information}

詳しくは、 [検索の基本事項](search-implementation.md) 開発者向けのページです。
