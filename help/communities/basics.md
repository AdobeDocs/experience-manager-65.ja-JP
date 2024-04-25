---
title: コミュニティコンポーネントの基本
description: 編集モードでのAEM Sites への Communities 機能の追加とコンポーネントの設定
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: eb5ce76a-bf28-4540-bc2d-3b5ecb8286f2
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 4%

---

# コミュニティコンポーネントの基本 {#communities-components-basics}

## 概要 {#overview}

ドキュメントのオーサリングの節では、オーサーエディットモードでAEM サイトに Communities 機能を追加する方法と、コンポーネント設定について説明します。

コンポーネントは、AEM インスタンスとインタラクティブを使用して確認できます [コミュニティコンポーネントガイド](components-guide.md).

## Communities コンポーネントへのアクセス {#accessing-communities-components}

ページコンテンツのオーサリング時に、基になるテンプレートでページのデザインの変更が許可されている場合は、サイトデザインの一部としてコンポーネントブラウザーでまだ使用できないコンポーネントを有効にすることができます。

使用可能な Communities コンポーネントが一覧表示されます [こちら](author-communities.md#available-communities-components).

>[!NOTE]
>
>オーサリングに関する一般的な情報については、 [ページのオーサリングのクイックガイド](../../help/sites-authoring/qg-page-authoring.md).
>
>AEMに詳しくない場合は、次のドキュメントを参照してください [基本操作](../../help/sites-authoring/basic-handling.md).

### デザインモードの開始 {#entering-design-mode}

If a **コミュニティ** コンポーネントがコンポーネントブラウザー（サイドキック）に見つかりません。入力する必要があります `Design Mode` をクリックして、他の Communities コンポーネントを追加します。 [必要なクライアントサイドライブラリ](#required-clientlibs) （clientlibs）を追加する必要がある場合もあります。

詳しくは、を参照してください [デザインモードでのコンポーネントの設定](../../help/sites-authoring/default-components-designmode.md).

以下は、いくつかの Communities コンポーネントを選択して、コンポーネントブラウザーで表示している画像です。

![component-design](assets/component-design.png)

選択したコンポーネントがコンポーネントブラウザーで使用できるようになりました。

![component-design1](assets/component-design1.png)

## 必須 Clientlibs {#required-clientlibs}

[クライアントサイドライブラリ](../../help/sites-developing/clientlibs.md) （clientlib）は、コンポーネントが適切に機能（JavaScript）され、スタイル設定（CSS）されている必要があります。

Communities コンポーネントをページに追加するときに、結果がエラーや予期しない外観の場合、最初に試みるのは、Communities コンポーネントに必要な clientlib を追加することです。 詳しくは、を参照してください [コミュニティコンポーネントの clientlib](clientlibs.md).

### 例：最初に配置されたレビューにクライアントライブラリが含まれない {#example-initially-placed-reviews-without-client-libraries}

![clientlibs1](assets/clientlibs1.png)

### ...とクライアントライブラリ {#and-with-client-libraries}

![clientlibs2](assets/clientlibs2.png)

## タグ付け {#tagging}

多くの Communities 機能は、メンバーがパブリッシュ環境で入力（投稿）したコンテンツにタグ付けできるように設定できます。

タグ付けが許可されている場合、コミュニティサイトの設定は、パブリッシュ環境でメンバーに表示される名前空間を制限するように設定できます。 を参照してください。 [コミュニティサイトコンソール](sites-console.md#tagging).

タグ付けが可能な機能： [ブログ](blog-feature.md), [カレンダー](calendar.md), [ファイルライブラリ](file-library.md), [フォーラム](forum.md)

タグを使用する機能： [検索](search.md), [ソーシャルタグクラウド](tagcloud.md)

オーサリング情報について：

* [タグの使用](../../help/sites-authoring/tags.md)

管理情報の場合：

* タグ名前空間の作成（分類）: [タグの管理](../../help/sites-administering/tags.md)
* コミュニティサイト設定：を参照してください [タグ設定](sites-console.md#tagging)
* [ユーザー生成コンテンツのタグ付け](../../help/sites-authoring/tags.md)

開発者情報：

* [AEM タグ付けフレームワーク](../../help/sites-developing/framework.md)
* [タグ付けの基本事項](tag.md)
