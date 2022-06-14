---
title: 検索機能
seo-title: Search Feature
description: コミュニティサイトへの検索の追加と設定
seo-description: Adding and configuring Search to a Communities site
uuid: ca633456-911f-447f-881e-653533125d5f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 3acac082-efbe-4995-b374-851cb9aaf62d
exl-id: e252b0e5-a2f8-468e-ac8c-951a5b0f2e32
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 29%

---

# 検索機能 {#search-feature}

検索機能は、フォーラムなど他の様々な機能と連携して、コンテンツを検索できるようにします。

コミュニティメンバーが入力した投稿（ユーザー生成コンテンツ（UGC））を検索する機能を追加するときは、[検索](#search)と[検索結果](#search-results)という 2 つのコンポーネントを使用します。

を含むページ `Search Results` コンポーネントは、検索と結果の表示の両方をサポートします。

を含むページ `Search` コンポーネントでは、検索を開始し、結果を `Search Results` ページ。

検索機能は、サイト訪問者やメンバーに向けてコンテンツを表示する他の機能と共に使用できます。

## 検索 {#search-features}

### 検索をページに追加 {#add-search-to-a-page}

を追加するには、以下を実行します。 `Search` コンポーネントをオーサリングモードでページに追加する場合は、コンポーネントブラウザーを使用して `Communities / Search` をクリックし、ページ上の適切な場所にドラッグします。 の使用 `Search` には 2 番目のページが必要です `Search Results.`

必要な情報については、 [コミュニティコンポーネントの基本](basics.md).

必要なクライアント側ライブラリの場合、 `cq.social.hbs.search`を含める場合は、次のようになります。 `Search` コンポーネントが表示されます。

![add-search](assets/add-search.png)

### 追加した検索を設定 {#configure-the-added-search}

配置された `Search` アクセスして選択するコンポーネント `Configure` 編集ダイアログを開くアイコン。

![confgure](assets/configure-new.png)

以下 **[!UICONTROL 検索設定]** タブでは、訪問者がクエリを入力した場合に検索するパスを指定します。

![search-settings](assets/search-settings.png)

* **[!UICONTROL 検索パス]**「項目を追加」ボタンを使用して検索パスを追加すると、コンテンツの検索が限定されます。例えば、検索を特定のフォーラムに限定するには、ページ内に配置されているフォーラムコンポーネントを選択します。

   * `/content/community-components/en/forum/jcr:content/content/forum`

* **[!UICONTROL 結果ページ]**
結果は、ブラウザーを使用して 
`Search Results` component.

## 検索結果 {#search-results}

### 検索結果をページに追加 {#add-search-results-to-a-page}

を追加するには、以下を実行します。 `Search Results` コンポーネントをオーサリングモードでページに追加する場合は、コンポーネントブラウザーを使用して

* `Communities / Search Results`

コンポーネントを探し、ページ上の位置にドラッグします。検索コンポーネントとは異なり、2 番目のページは不要です。同じページに結果が表示されるからです。

Web サイト内の別の場所で検索を使用する場合、この 1 つのページには `Search Results` は `Result Page` の任意の、またはすべてのインスタンスに対して `Search`.

必要な情報については、 [コミュニティコンポーネントの基本](basics.md).

必要なクライアント側ライブラリの場合、 `cq.social.hbs.search`を含める場合は、次のようになります。 `Search Result` コンポーネントが表示されます。

![search-result](assets/search-result1.png)

### 追加した検索結果を設定 {#configure-the-added-search-result}

配置された `Search Results` アクセスして選択するコンポーネント `Configure` 編集ダイアログを開くアイコン。

![設定](assets/configure-new.png)

以下 **[!UICONTROL 検索結果の設定]** 」タブで指定する場合、訪問者がクエリを入力したときに検索に含めるパスを指定できます。

![search-result-settings](assets/search-result-settings.png)

* **[!UICONTROL 1 ページの検索結果数]**

   1 ページに表示されるトピック/投稿の数を定義します。 初期設定は 10 です。

* **[!UICONTROL 検索パス]**

   「項目を追加」ボタンを使用して検索パスを追加すると、コンテンツの検索が制限されます。

## 追加情報 {#additional-information}

詳しくは、 [検索の基本事項](search-implementation.md) 開発者向けのページ
