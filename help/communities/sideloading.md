---
title: コンポーネントのサイドローディング
description: Communities コンポーネントのサイドローディングは、web ページが、サイト訪問者が選択した内容に応じて表示される内容を動的に変更するシンプルな単一ページアプリとして設計されている場合に便利です
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 960e132c-b370-43d1-bd8f-e7d0ded7c0b3
solution: Experience Manager
feature: Communities
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 1%
---
# コンポーネントのサイドローディング {#component-sideloading}

## 概要 {#overview}

Communities コンポーネントのサイドローディングは、web ページが、サイト訪問者が選択した内容に応じて表示される内容を動的に変更するシンプルな単一ページアプリとして設計されている場合に便利です。

これは、コミュニティコンポーネントがページテンプレートに存在せず、代わりにサイト訪問者の選択後に動的に追加される場合に実行されます。

ソーシャルコンポーネントフレームワーク（SCF）は軽量な存在であるため、最初のページ読み込み時に存在するSCF コンポーネントのみが登録されます。 ページ読み込み後に動的に追加されたSCF コンポーネントを登録するには、SCFを呼び出してコンポーネントを「サイドロード」する必要があります。

ページがCommunities コンポーネントをサイドロードするように設計されている場合は、ページ全体をキャッシュできます。

SCF コンポーネントを動的に追加する手順は次のとおりです。

1. [コンポーネントをDOMに追加する](#dynamically-add-component-to-dom)

1. [次の2つの方法のいずれかを使用してコンポーネント ](#sideload-by-invoking-scf)を読み込みます。

* [動的インクルージョン](#dynamic-inclusion)
  * 動的に追加されたすべてのコンポーネントをブーストラップする
* [動的な読み込み](#dynamic-loading)
  * 特定のコンポーネントを1つオンデマンドで追加

>[!NOTE]
>
>[既存でないリソース ](scf.md#add-or-include-a-communities-component)のサイドロードはサポートされていません。

## DOMにコンポーネントを動的に追加 {#dynamically-add-component-to-dom}

コンポーネントが動的に組み込まれるか、動的に読み込まれるかにかかわらず、最初にDOMに追加する必要があります。

SCF コンポーネントを追加する場合、最も一般的なタグはDIV タグですが、他のタグも使用できます。 SCFは、ページが最初に読み込まれたときにのみDOMを調べるので、SCFが明示的に呼び出されるまで、DOMへのこの追加は無視されます。

どのタグを使用しても、少なくとも、要素は次の2つの属性を含むことで、通常のSCF ルート要素パターンに準拠している必要があります。

* **data-component-id**

  追加されたコンポーネントへの効果的なパス。

* **data-scf-component**

  コンポーネントのresourceType。

追加されたコメントコンポーネントの例を次に示します。

```xml
<div
    class="scf-commentsystem scf translation-commentsystem"
    data-component-id="<%= currentPage.getPath()%>/jcr:content/content-left/comments"
    data-scf-component="social/commons/components/hbs/comments"
>
</div>
```

## SCFの呼び出しによるサイドロード {#sideload-by-invoking-scf}

### 動的インクルージョン {#dynamic-inclusion}

動的インクルージョンでは、ブートストラップリクエストを使用します。この結果、SCFはDOMを調べ、ページに見つかったすべてのSCF コンポーネントをブートストラップします。

ページ読み込み後にいつでもSCF コンポーネントを初期化するには、次のようなJQuery イベントを起動するだけです。

`$(document).trigger(SCF.events.BOOTSTRAP_REQUEST);`

### 動的ロード {#dynamic-loading}

動的な読み込みでは、SCF コンポーネントの読み込みを制御できます。

DOM内にあるすべてのSCF コンポーネントをブートストラップする代わりに、次のJavaScript メソッドを使用して読み込む特定のSCF コンポーネントを指定できます。

`SCF.addComponent(document.getElementById(*someId*));`

ここで、`someId`は`data-component-id`属性の値です。
