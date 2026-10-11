---
title: コミュニティコンポーネントの clientlib
description: クライアントサイドライブラリ（clientlibs）をページに追加して、使用状況の詳細を収集し、Communities コンポーネントのデバッグツールを使用できるようにする方法について説明します。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 94415926-a273-4f03-b7b6-57fdac12c741
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
source-wordcount: '406'
ht-degree: 4%
---
# コミュニティコンポーネントの clientlib {#clientlibs-for-communities-components}

## はじめに {#introduction}

ドキュメントのこの節では、クライアントサイドライブラリ（clientlibs）をコミュニティコンポーネントのページに追加する方法について説明します。

基本的な情報については、次を参照してください。

* [使用状況の詳細とデバッグツールを提供するクライアントサイドライブラリ ](/help/sites-developing/clientlibs.md)の使用
* SCF コンポーネントをカスタマイズする際に役立つ情報を提供するSCF](/help/communities/client-customize.md#clientlibs)の[Clientlibs


## Clientlibsが必要な理由 {#why-clientlibs-are-required}

コンポーネントの適切な機能（JavaScript）とスタイル設定（CSS）には、Clientlibが必要です。

機能に[ コミュニティ関数](/help/communities/functions.md)が存在する場合、必要なクライアントライブラリを含むすべての必要なコンポーネントと設定がコミュニティサイトに存在します。 追加のコンポーネントを作成者が使用できる場合にのみ、追加のクライアントライブラリを追加する必要があります。

必要なclientlibが見つからない場合、[Communities コンポーネントをページ ](/help/communities/author-communities.md)に追加すると、JavaScript エラーが発生し、予期しない外観になる可能性があります。

### 例：Clientlibsを使用しないレビューの配置 {#example-placed-reviews-without-clientlibs}

![配置済みレビュー](assets/placed-reviews.png)

### 例：Clientlibsを使用したレビューの配置 {#example-placed-reviews-with-clientlibs}

![reviews-clientlibs](assets/reviews-clientlibs.png)

## 必要なクライアントライブラリの特定 {#identifying-required-clientlibs}

開発者に必要な機能情報によって、必要なクライアントライブラリが特定されます。

また、AEM インスタンスから[ コミュニティコンポーネントガイド ](/help/communities/components-guide.md)を参照すると、コンポーネントに必要なclientlib カテゴリのリストにアクセスできます。

例えば、[ レビューページ ](https://localhost:4502/content/community-components/en/reviews.html)の上部に、リストされている必須のclientlibは次のとおりです

* cq.ckeditor
* cq.social.hbs.reviews

![clientlibs-reviews](assets/clientlibs-reviews.png)

## 必要なClientlibの追加 {#adding-required-clientlibs}

コミュニティ コンポーネントをページに追加する場合は、コンポーネントに必要なclientlibsを追加する必要があります（まだ存在しない場合）。

[CRXDE|Lite](#using-crxde-lite)を使用して、コミュニティサイトページの既存のclientlibslistを変更します。

[CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)を使用してコミュニティサイトのclientlibを追加するには：

* [https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de)を参照します。
* コンポーネントを追加するページの`clientlibslist` ノードを見つけます。

  * `/content/sites/sample/en/page/jcr:content/clientlibslist`

* `clientlibslist` ノードを選択しました：

  * 文字列[] プロパティ `scg:requiredClientLibs`を見つけます。
  * その`Value`を選択して、文字列配列ダイアログボックスにアクセスします。

    * 必要に応じて下にスクロールします。
    * 「+」を選択して、新しいクライアントライブラリを入力します。

      * この手順を繰り返して、クライアントライブラリをさらに追加します。

      * 「**OK**」を選択します。

  * 「**すべて保存**」を選択します。

>[!NOTE]
>
>サイトがコミュニティサイトでない場合は、サイトで使用されているクライアントライブラリの存在または場所を検出する必要があります。

[AEM Communitiesの使用開始](/help/communities/getting-started.md)の例（`site-name`は&#x200B;*engage*&#x200B;です）を使用すると、レビューコンポーネントを追加する場合にclientliblistが次のように表示されます。

![review-component](assets/review-component.png)
