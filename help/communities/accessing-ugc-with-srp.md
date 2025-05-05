---
title: SRP による UGC へのアクセス
description: ASRP または MSRP を使用するようにサイトが設定されている場合、実際の UGC はAEM Node Store （JCR）に格納されません
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 1157366f-2cc5-46e4-8ec6-e66fe5d0a0f6
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 3%

---

# SRP による UGC へのアクセス {#accessing-ugc-with-srp}

## SRP について {#about-srp}

AEM Communitiesのすべてのコンポーネントと機能は、[ ソーシャルコンポーネントフレームワーク（SCF） ](/help/communities/scf.md) に基づいて構築されています。これは、SocialResourceProvider API を呼び出して、すべてのユーザー生成コンテンツ（UGC）にアクセスします。

コミュニティサイトを作成する前に、基になる [ トポロジ ](/help/communities/topologies.md) と一致する実装を選択するように [&#128279;](/help/communities/working-with-srp.md) ストレージリソースプロバイダー（SRP を設定する必要があります。 SRP 実装は、次の 3 つのストレージオプションに基づいています。

1. [ASRP](/help/communities/asrp.md):Adobe・オン・デマンド・ストレージ
1. [MSRP](/help/communities/msrp.md) - MongoDB
1. [JSRP](/help/communities/jsrp.md) - JCR

## UGC ストレージについて {#about-ugc-storage}

UGC の格納について知っておくべき重要な点は、ASRP または MSRP を使用するようにサイトが設定されている場合、実際の UGC はAEM [node store](/help/sites-deploying/data-store-config.md) （JCR）に格納されないことです。

JCR には、有用なメタデータを提供するために UGC をシャドウイングするノードが含まれる場合がありますが、これらのノードを実際の UGC と混同しないでください。

[ ストレージリソースプロバイダーの概要 ](/help/communities/srp.md) を参照してください。

## ベストプラクティス {#best-practice}

カスタムコンポーネントを開発する場合、開発者は現在の選択したトポロジとは独立してコーディングするように注意する必要があります。これにより、今後は新しいトポロジに移行する柔軟性が保持されます。

### JCR が使用できないとします {#assume-jcr-not-available}

JCR に固有のメソッドは避ける必要があります。

使用するメソッド：

* Sling API （Sling リソース）

   * JCR ノードがあると想定しないでください

* OSGi イベント

   * JCR イベントがあると想定しないでください

* [SocialResourceUtilities](/help/communities/socialutils.md#socialresourceutilities-package)
* [SCFUtilities](/help/communities/socialutils.md#scfutilities-package)

回避方法：

* ノード API
* JCR イベント
* ワークフローランチャー（JCR イベントを使用）

### 検索コレクションの使用 {#use-search-collections}

SRP が異なると、異なるネイティブクエリ言語を持つことができます。 [com.adobe.cq.social.ugc.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) パッケージのメソッドを使用して、適切なクエリ言語を実行します。

詳しくは、[ 検索の基本事項 ](/help/communities/search-implementation.md) を参照してください。

## リソース {#resources}

* [ コミュニティコンテンツストレージ ](/help/communities/working-with-srp.md) - UGC 共通ストアで使用可能な SRP の選択肢について説明します
* [ ストレージリソースプロバイダーの概要 ](/help/communities/srp.md) – 概要とリポジトリの使用状況の概要
* [SRP と UGC の基本事項 ](/help/communities/srp-and-ugc.md) - SRP ユーティリティメソッドと例
* [ 検索の基本事項 ](/help/communities/search-implementation.md) - UGC 検索の基本情報
* [SocialUtils リファクタリング ](/help/communities/socialutils.md) – 非推奨のユーティリティメソッドを現在の SRP ユーティリティメソッドにマッピングする
