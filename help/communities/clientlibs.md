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
source-git-commit: 5b8b1544645465d10e7c2018364b6a74f1ad9a8e

---


# コミュニティコンポーネントの clientlib {#clientlibs-for-communities-components}

## 概要 {#introduction}

ドキュメントのこの節では、コミュニティコンポーネント用のクライアント側ライブラリ（clientlib）をページに追加する方法について説明します。

基本情報については、以下を参照してください。

* [使用状況の詳細とデバッグツールを提供する](/help/sites-developing/clientlibs.md) 、クライアント側ライブラリの使用
* [SCFコンポーネントのカスタマイズ時に役立つ情報を提供するSCF](/help/communities/client-customize.md#clientlibs) 用のClientlibs
* [ブログ：AEM Client Libraries explained by example](https://blogs.adobe.com/experiencedelivers/experience-management/clientlibs-explained-example/)

## clientlib が必要になる理由 {#why-clientlibs-are-required}

コンポーネントを正しく機能させ（JavaScript）、スタイル設定する（CSS）には、clientlib が必要です。

When there exists a [community function](/help/communities/functions.md) for a feature, all necessary components and configurations, including the required clientlibs, will be present in the community site. 作成者が追加のコンポーネントを使用できる場合にのみ、追加のclientlibを追加する必要があります。

必須の clientlib が欠落していると、[ページにコミュニティコンポーネントを追加](/help/communities/author-communities.md)したときに、JavaScript エラーが発生したり、予期しない外観が生じたりする可能性があります。

### 例：clientlib が欠落している場合のレビューの配置 {#example-placed-reviews-without-clientlibs}

![chlimage_1-132](assets/chlimage_1-132.png)

### 例：clientlib が存在する場合のレビューの配置 {#example-placed-reviews-with-clientlibs}

![chlimage_1-133](assets/chlimage_1-133.png)

## 必須の clientlib の識別 {#identifying-required-clientlibs}

開発者向けの基本機能情報の中で、必須の clientlib が識別されています。

また、AEM インスタンスから[コミュニティコンポーネントガイド](/help/communities/components-guide.md)を参照すると、コンポーネントに必須の clientlib カテゴリのリストにアクセスできます。

For example, at the very top of the [Reviews page](https://localhost:4502/content/community-components/en/reviews.html) the required clientlibs listed are

* cq.ckeditor
* cq.social.hbs.reviews

![chlimage_1-134](assets/chlimage_1-134.png)

## 必須の clientlib の追加 {#adding-required-clientlibs}

コミュニティコンポーネントをページに追加する場合、コンポーネントに必須の clientlib がまだ存在しなければ、追加する必要があります。

[CRXDE|Lite](#using-crxde-lite) を使用すると、コミュニティサイトページの既存の clientlibslist を変更できます。

To add a clientlib for a community site using [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) :

* Browse to [https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de)
* Locate the `clientlibslist` node for the page on which you wish to add the component

   * `/content/sites/sample/en/page/jcr:content/clientlibslist`

* With `clientlibslist` node selected

   * Stringプロパティの検索[]`scg:requiredClientLibs`
   * Select its `Value` to access the String array dialog

      * 必要に応じて下にスクロール
      * 「+」を選択して新しいクライアントライブラリを入力します。

         * 繰り返してクライアントライブラリを追加
      * 「**OK**」を選択します。
   * 「**すべて保存**」を選択します。



>[!NOTE]
>
>コミュニティサイト以外のサイトでは、使用されているクライアントライブラリの有無や場所を調べる必要があります。

ここでは、[AEM Communities 使用の手引き](/help/communities/getting-started.md)の例（`site-name` は *engage*）を引用し、レビューコンポーネントを追加する場合に clientliblist がどのように表示されるかを示しています。

![chlimage_1-135](assets/chlimage_1-135.png)

