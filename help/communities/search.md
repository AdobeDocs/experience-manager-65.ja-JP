---
title: 検索機能
description: コミュニティサイトへの検索の追加と設定
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: e252b0e5-a2f8-468e-ac8c-951a5b0f2e32
source-git-commit: 5bdf42d1ce7b2126bfb2670049deec4b6eaedba2
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 3%

---

# 検索機能 {#search-feature}

検索機能は、フォーラムなどの他の様々な機能と連携して、コンテンツを検索する機能を提供します。

コミュニティメンバーが入力した投稿 ( ユーザー生成コンテンツ (UGC) と呼ばれる ) を検索する機能を追加する場合、次の 2 つの要素があります。 [検索](#search) および [検索結果](#search-results).

を含むページ `Search Results` コンポーネントは、検索と結果の表示の両方をサポートします。

を含むページ `Search` コンポーネントでは、検索を開始し、結果を `Search Results` ページに貼り付けます。

検索機能は、サイトの訪問者やメンバーがコンテンツを表示できるその他の機能と共に使用できます。

## 検索 {#search-features}

### ページに検索を追加 {#add-search-to-a-page}

を追加するには、以下を実行します。 `Search` コンポーネントをオーサリングモードでページに追加する場合は、コンポーネントブラウザーを使用して `Communities / Search` をクリックし、ページ上の適切な場所にドラッグします。 の使用 `Search` には 2 番目のページが必要です `Search Results.`

必要な情報については、 [コミュニティコンポーネントの基本](basics.md).

必要なクライアント側ライブラリの場合、 `cq.social.hbs.search`を含める場合は、次のようになります。 `Search` コンポーネントが表示されます。

![add-search](assets/add-search.png)

### 追加した検索の設定 {#configure-the-added-search}

配置した `Search` アクセスして選択するコンポーネント `Configure` 編集ダイアログを開くアイコン。

![confgure](assets/configure-new.png)

の下 **[!UICONTROL 検索設定]** タブでは、訪問者がクエリを入力した場合に検索するパスを指定します。

![search-settings](assets/search-settings.png)

* **[!UICONTROL 検索パス]**
「項目を追加」ボタンを使用して検索パスを追加すると、コンテンツの検索が制限されます。 例えば、検索を特定のフォーラムに限定するには、ページ内に配置されているフォーラムコンポーネントを選択します。

   * `/content/community-components/en/forum/jcr:content/content/forum`

* **[!UICONTROL 結果ページ]**
結果は、ブラウザーを使用して `Search Results` コンポーネント。

## 検索結果 {#search-results}

### 検索結果をページに追加 {#add-search-results-to-a-page}

を追加するには、以下を実行します。 `Search Results` コンポーネントをオーサリングモードでページに追加する場合は、コンポーネントブラウザーを使用して

* `Communities / Search Results`

をクリックし、ページ上の適切な場所にドラッグします。 検索コンポーネントとは異なり、2 番目のページは不要です。同じページに結果が表示されるからです。

Web サイト内の別の場所で検索を使用する場合、この 1 つのページには `Search Results` は、 `Result Page` の任意の、またはすべてのインスタンスに対して `Search`.

必要な情報については、 [コミュニティコンポーネントの基本](basics.md).

必要なクライアント側ライブラリの場合、 `cq.social.hbs.search`を含める場合は、次のようになります。 `Search Result` コンポーネントが表示されます。

![search-result](assets/search-result1.png)

### 追加された検索結果の設定 {#configure-the-added-search-result}

配置した `Search Results` アクセスして選択するコンポーネント `Configure` 編集ダイアログを開くアイコン。

![設定](assets/configure-new.png)

の下 **[!UICONTROL 検索結果の設定]** 」タブで指定する場合、訪問者がクエリを入力したときに検索に含めるパスを指定できます。

![search-result-settings](assets/search-result-settings.png)

* **[!UICONTROL 1 ページの検索結果数]**

  1 ページに表示されるトピック/投稿の数を定義します。 初期設定は 10 です。

* **[!UICONTROL 検索パス]**

  「項目を追加」ボタンを使用して検索パスを追加すると、コンテンツの検索が制限されます。

## 追加情報 {#additional-information}

詳しくは、 [検索の基本事項](search-implementation.md) 開発者向けのページ
