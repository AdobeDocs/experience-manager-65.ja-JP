---
title: コミュニティコンポーネントの clientlib
description: コミュニティ用のクライアント側ライブラリ
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 94415926-a273-4f03-b7b6-57fdac12c741
source-git-commit: b9c164321baa3ed82ae87a97a325fcf0ad2f6ca0
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 4%

---

# コミュニティコンポーネントの clientlib {#clientlibs-for-communities-components}

## はじめに {#introduction}

この節では、コミュニティコンポーネント用のページにクライアント側ライブラリ (clientlibs) を追加する方法について説明します。

基本情報については、以下を参照してください。

* [クライアント側ライブラリの使用](/help/sites-developing/clientlibs.md) 使用状況の詳細とデバッグツールを提供します。
* [SCF の clientlibs](/help/communities/client-customize.md#clientlibs) SCF コンポーネントをカスタマイズする際に役立つ情報を提供します。


## clientlibs が必要な理由 {#why-clientlibs-are-required}

コンポーネントが適切に機能し (JavaScript)、スタイル設定 (CSS) されるには、clientlibs が必要です。

が存在する場合、 [コミュニティ機能](/help/communities/functions.md) 機能の場合、必要な clientlib を含む必要なすべてのコンポーネントと設定がコミュニティサイトに存在します。 作成者が追加のコンポーネントを使用できる場合にのみ、追加の clientlib を追加する必要があります。

必要な clientlib が見つからない場合、 [ページへのコミュニティコンポーネントの追加](/help/communities/author-communities.md) JavaScript エラーが発生し、予期しない外観が発生する場合がありました。

### 例：Clientlibs を使用しない場合のレビューの配置 {#example-placed-reviews-without-clientlibs}

![placed-reviews](assets/placed-reviews.png)

### 例：Clientlibs でのレビューの配置 {#example-placed-reviews-with-clientlibs}

![reviews-clientlibs](assets/reviews-clientlibs.png)

## 必要な clientlib の識別 {#identifying-required-clientlibs}

開発者向けの基本的な機能情報は、必要な clientlib を特定します。

さらに、AEMインスタンスから [コミュニティコンポーネントガイド](/help/communities/components-guide.md) では、コンポーネントに必要な clientlib カテゴリのリストにアクセスできます。

例えば、が [レビューページ](https://localhost:4502/content/community-components/en/reviews.html) 以下に、必要な clientlib を示します。

* cq.ckeditor
* cq.social.hbs.reviews

![clientlibs-reviews](assets/clientlibs-reviews.png)

## 必要な clientlib の追加 {#adding-required-clientlibs}

コミュニティコンポーネントをページに追加する場合は、そのコンポーネントに必要な clientlib を追加する必要があります（まだ追加していない場合）。

用途 [CRXDE|Lite](#using-crxde-lite) コミュニティサイトページの既存の clientlibslist を変更する場合。

を使用してコミュニティサイトに clientlib を追加するには [CRXDE Lite](/help/sites-developing/developing-with-crxde-lite.md):

* 参照先 [https://&lt;server>:&lt;port>/crx/de](https://localhost:4502/crx/de).
* を `clientlibslist` コンポーネントを追加するページのノード：

   * `/content/sites/sample/en/page/jcr:content/clientlibslist`

* を使用 `clientlibslist` 選択されたノード：

   * 文字列[] プロパティ `scg:requiredClientLibs`.
   * 選択 `Value` をクリックして、「文字列配列」ダイアログにアクセスします。

      * 必要に応じて下にスクロールします。
      * 「 + 」を選択して、新しいクライアントライブラリを入力します。

         * さらにクライアントライブラリを追加するには、この手順を繰り返します。

         * 「**OK**」を選択します。

   * **すべて保存** を選択します。

>[!NOTE]
>
>サイトがコミュニティサイトでない場合は、そのサイトで使用されているクライアントライブラリの存在または場所を検出する必要があります。

の使用 [AEM Communitiesの概要](/help/communities/getting-started.md) 例： `site-name` が *エンゲージ*&#x200B;レビューコンポーネントを追加すると、clientliblist は次のように表示されます。

![review-component](assets/review-component.png)
