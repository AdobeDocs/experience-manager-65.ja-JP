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
source-git-commit: f30decf0e32a520dcda04b89c5c1f5b67ab6e028
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 4%

---

# コミュニティコンポーネントの基本 {#communities-components-basics}

## 概要 {#overview}

ドキュメントのオーサリングの節では、オーサーエディットモードでAEM サイトに Communities 機能を追加する方法と、コンポーネント設定について説明します。

コンポーネントは、AEM インスタンスおよびインタラクティブな [ コミュニティコンポーネントガイド ](components-guide.md) を使用して確認できます。

## Communities コンポーネントへのアクセス {#accessing-communities-components}

ページコンテンツのオーサリング時に、基になるテンプレートでページのデザインの変更が許可されている場合は、サイトデザインの一部としてコンポーネントブラウザーでまだ使用できないコンポーネントを有効にすることができます。

[ 使用可能なコミュニティコンポーネント ](author-communities.md#available-communities-components) のリストを参照してください。

>[!NOTE]
>
>一般的なオーサリング情報については、[ ページのオーサリングのクイックガイド ](../../help/sites-authoring/qg-page-authoring.md) を参照してください。
>
>AEMに詳しくない場合は、[ 基本操作 ](../../help/sites-authoring/basic-handling.md) に関するドキュメントを参照してください。

### デザインモードの開始 {#entering-design-mode}

**コミュニティ** コンポーネントがコンポーネントブラウザー（サイドキック）に見つからない場合は、他のコミュニティコンポーネントを追加するために `Design Mode` を入力する必要があります。 [ 必要なクライアントサイドライブラリ ](#required-clientlibs) （clientlibs）を追加する必要がある場合もあります。

詳しくは、[ デザインモードでのコンポーネントの設定 ](../../help/sites-authoring/default-components-designmode.md) を参照してください。

以下は、いくつかの Communities コンポーネントを選択して、コンポーネントブラウザーで表示している画像です。

![ コンポーネントデザイン ](assets/component-design.png)

選択したコンポーネントがコンポーネントブラウザーで使用できるようになりました。

![component-design1](assets/component-design1.png)

## 必須 Clientlibs {#required-clientlibs}

[ クライアントサイドライブラリ ](../../help/sites-developing/clientlibs.md) （clientlib）は、コンポーネントが適切に機能（JavaScript）し、スタイル設定（CSS）するために必要です。

Communities コンポーネントをページに追加するときに、結果がエラーや予期しない外観の場合、最初に試みるのは、Communities コンポーネントに必要な clientlib を追加することです。 詳しくは、[ コミュニティコンポーネントの Clientlibs](clientlibs.md) を参照してください。

### 例：最初に配置されたレビューにクライアントライブラリが含まれない {#example-initially-placed-reviews-without-client-libraries}

![clientlibs1](assets/clientlibs1.png)

### ...とクライアントライブラリ {#and-with-client-libraries}

![clientlibs2](assets/clientlibs2.png)

## タグ付け {#tagging}

多くの Communities 機能は、メンバーがパブリッシュ環境で入力（投稿）したコンテンツにタグ付けできるように設定できます。

タグ付けが許可されている場合、コミュニティサイトの設定は、パブリッシュ環境でメンバーに表示される名前空間を制限するように設定できます。 [ コミュニティサイトコンソール ](sites-console.md#tagging) を参照してください。

タグ付けを許可する機能：[blog](blog-feature.md)、[calendar](calendar.md)、[file library](file-library.md)、[forum](forum.md)

タグを使用する機能：[ 検索 ](search.md)、[ ソーシャルタグクラウド ](tagcloud.md)

オーサリング情報について：

* [タグの使用](../../help/sites-authoring/tags.md)

管理情報の場合：

* タグ名前空間の作成（分類）:[ タグの管理 ](../../help/sites-administering/tags.md)
* コミュニティサイト設定：[ タグ付け ](sites-console.md#tagging) を参照してください
* [ユーザー生成コンテンツのタグ付け](../../help/sites-authoring/tags.md)

開発者情報：

* [AEM タグ付けフレームワーク](../../help/sites-developing/framework.md)
* [タグ付けの基本事項](tag.md)
