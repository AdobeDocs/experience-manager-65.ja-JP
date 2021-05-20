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
exl-id: 94415926-a273-4f03-b7b6-57fdac12c741
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 59%

---

# コミュニティコンポーネントの clientlib {#clientlibs-for-communities-components}

## はじめに {#introduction}

ドキュメントのこの節では、コミュニティコンポーネント用のクライアント側ライブラリ（clientlib）をページに追加する方法について説明します。

基本情報については、以下を参照してください。

* [使用方法の詳細とデバッ](/help/sites-developing/clientlibs.md) グツールを提供するクライアント側ライブラリの使用
* [SCF用clientlibs :SCFコン](/help/communities/client-customize.md#clientlibs) ポーネントをカスタマイズする際に役立つ情報を提供します。
* [ブログ：AEM Client Libraries explained by example](https://blogs.adobe.com/experiencedelivers/experience-management/clientlibs-explained-example/)

## clientlib が必要になる理由  {#why-clientlibs-are-required}

コンポーネントを正しく機能させ（JavaScript）、スタイル設定する（CSS）には、clientlib が必要です。

1つの機能に[コミュニティ機能](/help/communities/functions.md)が存在する場合、必要なclientlibを含む必要なコンポーネントと設定がすべてコミュニティサイトに表示されます。 作成者が追加のコンポーネントを使用できる場合にのみ、追加のclientlibを追加する必要があります。

必須の clientlib が欠落していると、[ページにコミュニティコンポーネントを追加](/help/communities/author-communities.md)したときに、JavaScript エラーが発生したり、予期しない外観が生じたりする可能性があります。

### 例：clientlib が欠落している場合のレビューの配置  {#example-placed-reviews-without-clientlibs}

![配置レビュー](assets/placed-reviews.png)

### 例：clientlib が存在する場合のレビューの配置 {#example-placed-reviews-with-clientlibs}

![reviews-clientlibs](assets/reviews-clientlibs.png)

## 必須の clientlib の識別 {#identifying-required-clientlibs}

開発者向けの基本機能情報の中で、必須の clientlib が識別されています。

また、AEM インスタンスから[コミュニティコンポーネントガイド](/help/communities/components-guide.md)を参照すると、コンポーネントに必須の clientlib カテゴリのリストにアクセスできます。

例えば、[「レビュー」ページの最上部に](https://localhost:4502/content/community-components/en/reviews.html)リストされている必要なclientlibは次のとおりです。

* cq.ckeditor
* cq.social.hbs.reviews

![clientlibs-reviews](assets/clientlibs-reviews.png)

## 必須の clientlib の追加 {#adding-required-clientlibs}

コミュニティコンポーネントをページに追加する場合、コンポーネントに必須の clientlib がまだ存在しなければ、追加する必要があります。

[CRXDE|Lite](#using-crxde-lite) を使用すると、コミュニティサイトページの既存の clientlibslist を変更できます。

[CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md)を使用してコミュニティサイトのclientlibを追加するには：

* [https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de)を参照します。
* コンポーネントを追加するページの`clientlibslist`ノードを探します。

   * `/content/sites/sample/en/page/jcr:content/clientlibslist`

* `clientlibslist`ノードを選択した状態：

   * 文字列[]プロパティ`scg:requiredClientLibs`を探します。
   * `Value`を選択して、「文字列配列」ダイアログにアクセスします。

      * 必要に応じて下にスクロールします。
      * +を選択して、新しいクライアントライブラリを入力します。

         * クライアントライブラリをさらに追加する場合に繰り返します。

         * 「**OK**」を選択します。
   * 「**すべて保存**」を選択します。


>[!NOTE]
>
>コミュニティサイト以外のサイトでは、使用されているクライアントライブラリの有無や場所を調べる必要があります。

ここでは、[AEM Communities 使用の手引き](/help/communities/getting-started.md)の例（`site-name` は *engage*）を引用し、レビューコンポーネントを追加する場合に clientliblist がどのように表示されるかを示しています。

![review-component](assets/review-component.png)
