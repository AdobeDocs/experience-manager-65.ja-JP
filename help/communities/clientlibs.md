---
title: コミュニティコンポーネントの clientlib
description: ページにクライアントサイドライブラリ（clientlib）を追加して、使用状況の詳細を収集し、Communities コンポーネントのデバッグツールを使用できるようにする方法を説明します。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 94415926-a273-4f03-b7b6-57fdac12c741
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 3%

---

# コミュニティコンポーネントの clientlib {#clientlibs-for-communities-components}

## はじめに {#introduction}

ドキュメントのこの節では、Communities コンポーネントのページにクライアントサイドライブラリ（clientlibs）を追加する方法について説明します。

基本的な情報については、次を参照してください。

* 使用の詳細とデバッグツールを提供する [&#x200B; クライアントサイドライブラリの使用 &#x200B;](/help/sites-developing/clientlibs.md)
* [SCF の clientlibs](/help/communities/client-customize.md#clientlibs):SCF コンポーネントをカスタマイズする際に役立つ情報を提供します


## Clientlibs が必要な理由 {#why-clientlibs-are-required}

clientlib は、コンポーネントが適切に機能（JavaScript）し、スタイル設定（CSS）するために必要です。

機能に [&#x200B; コミュニティ機能 &#x200B;](/help/communities/functions.md) がある場合、必要なすべてのコンポーネントおよび設定（必要な clientlib を含む）がコミュニティサイトに存在します。 作成者が追加のコンポーネントを使用できるようにする場合にのみ、clientlib を追加する必要があります。

必要な clientlibs が見つからない場合、[Communities コンポーネントをページに追加する &#x200B;](/help/communities/author-communities.md)、JavaScript エラーが発生し、予期しない外観が発生する場合があります。

### 例：Clientlibs を使用せずに配置したレビュー {#example-placed-reviews-without-clientlibs}

![placed-reviews](assets/placed-reviews.png)

### 例：Clientlibs を使用して配置されたレビュー {#example-placed-reviews-with-clientlibs}

![reviews-clientlibs](assets/reviews-clientlibs.png)

## 必要な Clientlibs の識別 {#identifying-required-clientlibs}

デベロッパーにとって不可欠な機能情報は、必要な clientlib を特定します。

さらに、AEM インスタンスから [&#x200B; コミュニティコンポーネントガイド &#x200B;](/help/communities/components-guide.md) を参照すると、コンポーネントに必要な clientlib カテゴリのリストにアクセスできます。

例えば、[&#x200B; レビューページの上部に &#x200B;](https://localhost:4502/content/community-components/en/reviews.html) 必須の clientlib が一覧表示されます

* cq.ckeditor
* cq.social.hbs.reviews

![clientlibs-reviews](assets/clientlibs-reviews.png)

## 必要な Clientlibs の追加 {#adding-required-clientlibs}

Communities コンポーネントをページに追加する場合、コンポーネントに必要な clientlib がまだ存在しない場合は追加する必要があります。

[CRXDE|Lite](#using-crxde-lite) を使用して、コミュニティサイトページの既存の clientlibslist を変更します。

[CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md) を使用してコミュニティサイトのクライアントライブラリを追加するには：

* [https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de) を参照します。
* コンポーネントを追加するページの `clientlibslist` ノードを見つけます。

   * `/content/sites/sample/en/page/jcr:content/clientlibslist`

* ノード `clientlibslist` 選択した状態：

   * String[] プロパティの `scg:requiredClientLibs` を見つけます。
   * その `Value` を選択して、「文字列配列」ダイアログボックスにアクセスします。

      * 必要に応じて下にスクロールします。
      * 「+」を選択して、新しいクライアントライブラリを入力します。

         * 繰り返して、さらにクライアントライブラリを追加します。

         * 「**OK**」を選択します。

   * 「**すべて保存**」を選択します。

>[!NOTE]
>
>サイトがコミュニティサイトでない場合は、サイトで使用されているクライアントライブラリの存在または場所を検出する必要があります。

[AEM Communities使用の手引き &#x200B;](/help/communities/getting-started.md) の例を使用します。`site-name` は *engage* です。レビューコンポーネントを追加する場合、clientliblist は次のように表示されます。

![review-component](assets/review-component.png)
