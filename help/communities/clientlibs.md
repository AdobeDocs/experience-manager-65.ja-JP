---
title: コミュニティコンポーネントの clientlib
seo-title: コミュニティコンポーネントの clientlib
description: Communities 用のクライアント側ライブラリ
seo-description: Communities 用のクライアント側ライブラリ
uuid: d2a9f986-96cf-4ee8-81e6-36a96f45ddcb
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 68ce47c8-a03f-40d6-a7f3-2cc64aee0594
docset: aem65
translation-type: tm+mt
source-git-commit: f6aa95514a266a042c9bd1165634e30e80479ae7
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 59%

---


# コミュニティコンポーネントの clientlib {#clientlibs-for-communities-components}

## 概要 {#introduction}

ドキュメントのこの節では、コミュニティコンポーネント用のクライアント側ライブラリ（clientlib）をページに追加する方法について説明します。

基本情報については、以下を参照してください。

* [使用状況の詳細とデバッグツールを提供するクライアント側ライブラリ](/help/sites-developing/clientlibs.md) (Using Client-Side Libraries)
* [SCFコンポーネントのカスタマイズ時に役立つ情報を提供する、SCF](/help/communities/client-customize.md#clientlibs) 用のClientlibs
* [ブログ：AEM Client Libraries explained by example](https://blogs.adobe.com/experiencedelivers/experience-management/clientlibs-explained-example/)

## clientlib が必要になる理由 {#why-clientlibs-are-required}

コンポーネントを正しく機能させ（JavaScript）、スタイル設定する（CSS）には、clientlib が必要です。

When there exists a [community function](/help/communities/functions.md) for a feature, all necessary components and configurations, including the required clientlibs, will be present in the community site. 作成者が追加のコンポーネントを使用できる場合にのみ、追加のclientlibを追加する必要があります。

必須の clientlib が欠落していると、[ページにコミュニティコンポーネントを追加](/help/communities/author-communities.md)したときに、JavaScript エラーが発生したり、予期しない外観が生じたりする可能性があります。

### 例：clientlib が欠落している場合のレビューの配置 {#example-placed-reviews-without-clientlibs}

![配置されたレビュー](assets/placed-reviews.png)

### 例：clientlib が存在する場合のレビューの配置 {#example-placed-reviews-with-clientlibs}

![reviews-clientlibs](assets/reviews-clientlibs.png)

## 必須の clientlib の識別 {#identifying-required-clientlibs}

開発者向けの基本機能情報の中で、必須の clientlib が識別されています。

また、AEM インスタンスから[コミュニティコンポーネントガイド](/help/communities/components-guide.md)を参照すると、コンポーネントに必須の clientlib カテゴリのリストにアクセスできます。

For example, at the very top of the [Reviews page](https://localhost:4502/content/community-components/en/reviews.html) the required clientlibs listed are

* cq.ckeditor
* cq.social.hbs.reviews

![clientlibs-reviews](assets/clientlibs-reviews.png)

## 必須の clientlib の追加 {#adding-required-clientlibs}

コミュニティコンポーネントをページに追加する場合、コンポーネントに必須の clientlib がまだ存在しなければ、追加する必要があります。

[CRXDE|Lite](#using-crxde-lite) を使用すると、コミュニティサイトページの既存の clientlibslist を変更できます。

[CRXDE Liteを使用してコミュニティサイトのclientlibを追加するには](/help/sites-developing/developing-with-crxde-lite.md):

* Browse to [https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de).
* Locate the `clientlibslist` node for the page on which you wish to add the component:

   * `/content/sites/sample/en/page/jcr:content/clientlibslist`

* With `clientlibslist` node selected:

   * String[] プロパティを探し `scg:requiredClientLibs`ます。
   * Select its `Value` to access the String array dialog.

      * 必要に応じて下にスクロールします。
      * 「+」を選択して、新しいクライアントライブラリを入力します。

         * さらにクライアントライブラリを追加する場合は、同じ手順を繰り返します。

         * 「**OK**」を選択します。
   * Select **Save All**.


>[!NOTE]
>
>コミュニティサイト以外のサイトでは、使用されているクライアントライブラリの有無や場所を調べる必要があります。


ここでは、[AEM Communities 使用の手引き](/help/communities/getting-started.md)の例（`site-name` は *engage*）を引用し、レビューコンポーネントを追加する場合に clientliblist がどのように表示されるかを示しています。

![レビューコンポーネント](assets/review-component.png)

