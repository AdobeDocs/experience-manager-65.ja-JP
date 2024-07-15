---
title: コンポーネントのサイドローディング
description: Communities コンポーネントのサイドローディングは、web ページが単純な単一ページアプリとしてデザインされた場合に役立ちます。このアプリでは、サイト訪問者が選択した項目に応じて表示内容が動的に変更されます
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 960e132c-b370-43d1-bd8f-e7d0ded7c0b3
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 1%

---

# コンポーネントのサイドローディング {#component-sideloading}

## 概要 {#overview}

Communities コンポーネントのサイドローディングは、web ページが単純な単一ページアプリとしてデザインされた場合に役立ちます。このアプリでは、サイト訪問者が選択した項目に応じて表示内容が動的に変更されます。

これは、Communities コンポーネントがページテンプレートに存在せず、サイト訪問者の選択に従って動的に追加された場合に実現されます。

ソーシャルコンポーネントフレームワーク（SCF）は軽量なプレゼンスを有するので、最初のページ読み込み時に存在する SCF コンポーネントのみが登録される。 動的に追加される SCF コンポーネントをページ読み込み後に登録するには、SCF を呼び出してコンポーネントを「サイドロード」する必要があります。

Communities コンポーネントをサイドロードするようにページをデザインすると、ページ全体をキャッシュすることができます。

SCF コンポーネントを動的に追加する手順は次のとおりです。

1. [DOM にコンポーネントを追加します](#dynamically-add-component-to-dom)

1. [ コンポーネントをサイドロード ](#sideload-by-invoking-scf) し、次の 2 つの方法のいずれかを使用します。

* [動的インクルージョン](#dynamic-inclusion)
   * 動的に追加されたすべてのコンポーネントをブートストラップする
* [動的読み込み](#dynamic-loading)
   * オンデマンドで 1 つの特定のコンポーネントを追加

>[!NOTE]
>
>[ 既存のリソースではない ](scf.md#add-or-include-a-communities-component) のサイドローディングはサポートされていません。

## DOM へのコンポーネントの動的な追加 {#dynamically-add-component-to-dom}

コンポーネントが動的に含まれているか動的に読み込まれているかに関わらず、まず DOM に追加する必要があります。

SCF コンポーネントを追加する場合、最も一般的に使用されるタグは DIV タグですが、他のタグも使用できます。 SCF はページの初回読み込み時にのみ DOM を調べるので、SCF が明示的に呼び出されるまで、DOM へのこの追加は気付かれません。

使用されるタグが何であれ、少なくとも、次の 2 つの属性を含めることで、要素が通常の SCF ルート要素パターンに準拠する必要があります。

* **data-component-id**

  追加されたコンポーネントへの有効なパス。

* **data-scf-component**

  コンポーネントの resourceType。

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

### 動的インクルージョン {#dynamic-inclusion}

動的インクルージョンでは、SCF が DOM を調べ、ページ上で見つかったすべての SCF コンポーネントをブートストラップするブーストリクエストを使用します。

ページの読み込み後に SCF コンポーネントを初期化するには、次のような JQuery イベントを発生させるだけです。

`$(document).trigger(SCF.events.BOOTSTRAP_REQUEST);`

### 動的読み込み {#dynamic-loading}

動的読み込みでは、SCF コンポーネントの読み込みを制御できます。

DOM 内のすべての SCF コンポーネントをブートストラップする代わりに、このJavaScript メソッドを使用して、読み込む特定の SCF コンポーネントを指定することができます。

`SCF.addComponent(document.getElementById(*someId*));`

ここで、`someId` は `data-component-id` 属性の値です。
