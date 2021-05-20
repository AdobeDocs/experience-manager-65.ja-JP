---
title: コンポーネントのサイドローディング
seo-title: コンポーネントのサイドローディング
description: コミュニティコンポーネントのサイドローディングは、Web ページが、サイト訪問者の選択に応じて表示内容が動的に変わる単純なシングルページアプリケーションとして設計されている場合に便利です
seo-description: コミュニティコンポーネントのサイドローディングは、Web ページが、サイト訪問者の選択に応じて表示内容が動的に変わる単純なシングルページアプリケーションとして設計されている場合に便利です
uuid: 8c9a5fde-26a3-4610-bc14-f8b665059015
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a9cb5294-e5ab-445b-b7c2-ffeecda91c50
exl-id: 960e132c-b370-43d1-bd8f-e7d0ded7c0b3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 78%

---

# コンポーネントのサイドローディング {#component-sideloading}

## 概要 {#overview}

コミュニティコンポーネントのサイドローディングは、Web ページが、サイト訪問者の選択に応じて表示内容が動的に変わる単純なシングルページアプリケーションとして設計されている場合に便利です.

これは、コミュニティコンポーネントがページテンプレートに存在せず、サイト訪問者の選択後に動的に追加される場合に実現されます。

ソーシャルコンポーネントフレームワーク（SCF）は軽量なので、初期ページロード時に存在する SCF コンポーネントのみが登録されます。ページの読み込み後に動的に追加されるSCFコンポーネントを登録するには、SCFを呼び出してコンポーネントを「サイドロード」する必要があります。

コミュニティコンポーネントをサイドローディングするようページが設計されている場合、ページ全体をキャッシュすることができます。

SCF コンポーネントを動的に追加する手順は、次のとおりです。

1. [DOMにコンポーネントを追加する](#dynamically-add-component-to-dom)

1. [次の2つの方法のい](#sideload-by-invoking-scf) ずれかを使用して、コンポーネントをサイドロードします。

* [動的な組み込み](#dynamic-inclusion)
   * 動的に追加されるすべてのコンポーネントをブーストラップする
* [動的な読み込み](#dynamic-loading)
   * 特定のコンポーネントをオンデマンドで追加

>[!NOTE]
>
>[存在しないリソース](scf.md#add-or-include-a-communities-component)のサイドローディングはサポートされていません。

## DOM に対するコンポーネントの動的な追加  {#dynamically-add-component-to-dom}

動的なインクルードの場合も動的なロードの場合も、最初にコンポーネントを DOM に追加する必要があります。

SCF コンポーネントを追加する際に最もよく使用されるタグは DIV タグですが、他のタグを使用することもできます。SCFはページが最初に読み込まれるときにのみDOMを調べるので、SCFが明示的に呼び出されるまで、DOMへのこの追加は無視されます。

どのタグを使用する場合も、最低限、要素が通常の SCF ルート要素パターンに準拠している必要があります。そのためには、次の 2 つの属性を含めます。

* **data-component-id**

   追加されたコンポーネントへの有効なパス。

* **data-scf-component**

   コンポーネントのresourceType。

以下に示すのは、追加されるコメントコンポーネントの例です。

```xml
<div
    class="scf-commentsystem scf translation-commentsystem"
    data-component-id="<%= currentPage.getPath()%>/jcr:content/content-left/comments"
    data-scf-component="social/commons/components/hbs/comments"
>
</div>
```

## SCF の呼び出しによるサイドローディング {#sideload-by-invoking-scf}

### 動的なインクルード {#dynamic-inclusion}

動的なインクルードでは、ブートストラップ要求を使用します。これにより、SCF によって DOM が確認され、ページ上で見つかったすべての SCF コンポーネントがブートストラップされます。

ページロード後にいつでも次のような JQuery イベントを実行して、SCF コンポーネントを初期化できます。

`$(document).trigger(SCF.events.BOOTSTRAP_REQUEST);`

### 動的なロード {#dynamic-loading}

動的なロードでは、ロードする SCF コンポーネントを制御できます。

次の JavaScript メソッドを使用すると、DOM にあるすべての SCF コンポーネントをブートストラップする代わりに、ロードする特定の SCF コンポーネントを指定できます。

`SCF.addComponent(document.getElementById(*someId*));`

`someId`は`data-component-id`属性の値です。
