---
title: コミュニティコンポーネントの基本
seo-title: Communities Components Basics
description: 編集モードでの AEM Sites へのコミュニティ機能の付加とコンポーネントの設定
seo-description: Add Communities features to AEM sites in edit mode and configure components
uuid: c017a7c5-40d1-4592-9317-96fd727dac86
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 21714581-7645-4b47-a9b0-9f1424013240
exl-id: eb5ce76a-bf28-4540-bc2d-3b5ecb8286f2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 67%

---

# コミュニティコンポーネントの基本 {#communities-components-basics}

## 概要 {#overview}

このドキュメントのオーサリングセクションでは、オーサリング編集モードでの  AEM sites へのコミュニティ機能の付加や、コンポーネント設定の記述について説明します。

コンポーネントは、AEMインスタンスとインタラクティブを使用して確認できます [コミュニティコンポーネントガイド](components-guide.md).

## コミュニティコンポーネントへのアクセス {#accessing-communities-components}

ページコンテンツをオーサリングするときに、基になるテンプレートがページのデザイン変更を許可している場合は、コンポーネントブラウザーにまだ表示されていないコンポーネントをサイトデザインの一部として有効にできます。

使用可能なコミュニティコンポーネントは[こちら](author-communities.md#available-communities-components)を参照してください。

>[!NOTE]
>
>オーサリングに関する一般的な情報については、 [ページのオーサリングのクイックガイド](../../help/sites-authoring/qg-page-authoring.md).
>
>AEM に精通していない場合は、[基本操作](../../help/sites-authoring/basic-handling.md)に関するドキュメントを参照してください。

### デザインモードの開始 {#entering-design-mode}

次の場合、 **コミュニティ** コンポーネントがコンポーネントブラウザー（サイドキック）に見つからない場合は、 `Design Mode` をクリックして、他のコミュニティコンポーネントを追加します。 [必要なクライアント側ライブラリ](#required-clientlibs) (clientlibs) の追加も必要になる場合があります。

詳しくは、 [デザインモードでのコンポーネントの設定](../../help/sites-authoring/default-components-designmode.md).

次の図に、いくつかのコミュニティコンポーネントを選択して、コンポーネントブラウザーに表示する操作を示します。

![component-design](assets/component-design.png)

選択したコンポーネントがコンポーネントブラウザーに表示されるようになりました。

![component-design1](assets/component-design1.png)

## 必須の clientlibs {#required-clientlibs}

コンポーネントを正しく機能させ（JavaScript）、スタイル設定する（CSS）には、[クライアント側ライブラリ](../../help/sites-developing/clientlibs.md)（clientlibs）が必要です。

コミュニティコンポーネントをページに追加して、結果がエラーまたは予期せぬ表示になった場合は、まずコミュニティコンポーネントに必須の clientlibs の追加を試みてください。詳しくは、 [コミュニティコンポーネントの clientlib](clientlibs.md).

### 例：最初にクライアントライブラリのないレビューを配置… {#example-initially-placed-reviews-without-client-libraries}

![clientlibs1](assets/clientlibs1.png)

### ...およびクライアントライブラリ {#and-with-client-libraries}

![clientlibs2](assets/clientlibs2.png)

## タグ付け {#tagging}

パブリッシュ環境に入力（投稿）されたコンテンツへのタグ付けを許可するために、多くのコミュニティ機能を設定できます。

タグ付けが許可されている場合は、パブリッシュ環境でメンバーに表示する名前空間を制限するようにコミュニティサイトを設定できます。詳しくは、 [コミュニティサイトコンソール](sites-console.md#tagging).

タグ付けを許可する機能： [ブログ](blog-feature.md), [カレンダー](calendar.md), [ファイルライブラリ](file-library.md), [フォーラム](forum.md)

タグを使用する機能： [カタログ](catalog.md), [検索](search.md), [social タグクラウド](tagcloud.md)

オーサリングに関する情報：

* [タグの使用 ](../../help/sites-authoring/tags.md)

管理に関する情報：

* タグ名前空間（分類）の作成： [タグの管理](../../help/sites-administering/tags.md)
* コミュニティサイトの設定：参照 [タグ付け](sites-console.md#tagging)
* [ユーザー生成コンテンツのタグ付け](../../help/sites-authoring/tags.md)
* [イネーブルメントリソースのタグ付け](tag-resources.md)

開発者向けの情報：

* [AEM タグ付けフレームワーク](../../help/sites-developing/framework.md)
* [タグ付けの基本事項](tag.md)
