---
title: コンポーネントのサイドローディング
description: コミュニティコンポーネントのサイドロードは、Web ページが単純な単一ページアプリとして設計され、サイト訪問者が選択した内容に応じて表示内容を動的に変更する場合に役立ちます
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 960e132c-b370-43d1-bd8f-e7d0ded7c0b3
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 1%

---

# コンポーネントのサイドローディング {#component-sideloading}

## 概要 {#overview}

コミュニティコンポーネントのサイドロードは、Web ページが単純な単一ページアプリとして設計され、サイト訪問者が選択した内容に応じて表示内容を動的に変更する場合に役立ちます。

これは、コミュニティコンポーネントがページテンプレートに存在せず、代わりにサイト訪問者の選択に従って動的に追加される場合に実行されます。

ソーシャルコンポーネントフレームワーク (SCF) は軽量な存在なので、最初のページ読み込み時に存在する SCF コンポーネントのみが登録されます。 ページの読み込み後に動的に追加された SCF コンポーネントを登録するには、SCF を呼び出してコンポーネントを「サイドロード」する必要があります。

Communities コンポーネントをサイドロードするように設計されているページでは、ページ全体をキャッシュできます。

SCF コンポーネントを動的に追加する手順は次のとおりです。

1. [DOM にコンポーネントを追加します。](#dynamically-add-component-to-dom)

1. [コンポーネントをサイドロード](#sideload-by-invoking-scf) 次の 2 つの方法のいずれかを使用します。

* [動的な追加](#dynamic-inclusion)
   * 動的に追加されたすべてのコンポーネントをブーストラップ
* [動的な読み込み](#dynamic-loading)
   * 特定のコンポーネントをオンデマンドで 1 つ追加

>[!NOTE]
>
>サイドローディング [存在しないリソース](scf.md#add-or-include-a-communities-component) はサポートされていません。

## DOM にコンポーネントを動的に追加 {#dynamically-add-component-to-dom}

コンポーネントが動的に含まれるか動的に読み込まれるかに関わらず、まず DOM に追加する必要があります。

SCF コンポーネントを追加する際に最も一般的なタグは DIV タグですが、他のタグも使用できます。 SCF はページが最初に読み込まれたときにのみ DOM を調べるので、SCF が明示的に呼び出されるまで、DOM へのこの追加は無視されます。

どのタグを使用する場合でも、少なくとも、その要素は、次の 2 つの属性を含めることで、通常の SCF ルート要素パターンに準拠している必要があります。

* **data-component-id**

  追加されたコンポーネントへの有効なパス。

* **data-scf-component**

  コンポーネントの resourceType です。

次に、追加されたコメントコンポーネントの例を示します。

```xml
<div
    class="scf-commentsystem scf translation-commentsystem"
    data-component-id="<%= currentPage.getPath()%>/jcr:content/content-left/comments"
    data-scf-component="social/commons/components/hbs/comments"
>
</div>
```

## SCF の呼び出しによるサイドロード {#sideload-by-invoking-scf}

### 動的な組み込み {#dynamic-inclusion}

動的インクルージョンは、ブーストラップリクエストを使用するので、SCF が DOM を調べて、ページ上のすべての SCF コンポーネントをブートスラップします。

ページの読み込み後に SCF コンポーネントを初期化するには、次のような JQuery イベントを発生させます。

`$(document).trigger(SCF.events.BOOTSTRAP_REQUEST);`

### 動的読み込み {#dynamic-loading}

動的な読み込みは、SCF コンポーネントの読み込みを制御します。

DOM 内のすべての SCF コンポーネントをブートストラップする代わりに、次の JavaScript メソッドを使用して、読み込む特定の SCF コンポーネントを指定することができます。

`SCF.addComponent(document.getElementById(*someId*));`

ここで、 `someId` は、 `data-component-id` 属性。
