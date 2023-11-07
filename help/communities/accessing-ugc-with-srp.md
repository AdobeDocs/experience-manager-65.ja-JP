---
title: SRP による UGC へのアクセス
description: サイトが ASRP または MSRP を使用するように設定されている場合、実際の UGC はAEMノードストア (JCR) に格納されません
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
docset: aem65
exl-id: 1157366f-2cc5-46e4-8ec6-e66fe5d0a0f6
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 3%

---

# SRP による UGC へのアクセス {#accessing-ugc-with-srp}

## SRP について {#about-srp}

すべてのAEM Communitiesのコンポーネントと機能は、 [ソーシャルコンポーネントフレームワーク (SCF)](/help/communities/scf.md)を呼び出し、 SocialResourceProvider API を呼び出してユーザー生成コンテンツ (UGC) にアクセスします。

コミュニティサイトを作成する前に、 [ストレージリソースプロバイダー (SRP)](/help/communities/working-with-srp.md) は、基になる [トポロジ](/help/communities/topologies.md). SRP の実装は、次の 3 つのストレージオプションに基づいています。

1. [ASRP](/help/communities/asrp.md) -Adobeオンデマンドストレージ
1. [MSRP](/help/communities/msrp.md) - MongoDB
1. [JSRP](/help/communities/jsrp.md) - JCR

## UGC ストレージについて {#about-ugc-storage}

UGC のストレージに関して知っておくべき重要な点は、ASRP または MSRP を使用するようにサイトを設定する場合、実際の UGC はAEMに格納されないことです [ノードストア](/help/sites-deploying/data-store-config.md) (JCR)。

JCR には、UGC に影を付けて有用なメタデータを提供するノードが存在する場合がありますが、これらのノードを実際の UGC と混同しないでください。

詳しくは、 [ストレージリソースプロバイダの概要。](/help/communities/srp.md)

## ベストプラクティス {#best-practice}

カスタムコンポーネントを開発する場合、開発者は現在選択しているトポロジとは別にコーディングをおこなうように注意する必要があり、将来新しいトポロジに移行する柔軟性を維持する必要があります。

### JCR が使用できないと仮定 {#assume-jcr-not-available}

JCR に固有のメソッドは避ける必要があります。

使用するメソッド：

* Sling API（Sling リソース）

   * JCR ノードが存在するとは想定しないでください。

* OSGi イベント

   * JCR イベントがあるとは想定しないでください

* [SocialResourceUtilities](/help/communities/socialutils.md#socialresourceutilities-package)
* [SCFUtilities](/help/communities/socialutils.md#scfutilities-package)

回避する方法：

* ノード API
* JCR イベント
* ワークフローランチャー（JCR イベントを使用）

### コレクションを検索 {#use-search-collections}

異なる SRP は異なるネイティブクエリ言語を持つことができます。 のメソッドを使用します。 [com.adobe.cq.social.ugc.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) 適切なクエリ言語を実行するためのパッケージ。

詳しくは、 [検索の基本事項](/help/communities/search-implementation.md).

## リソース {#resources}

* [コミュニティコンテンツストレージ](/help/communities/working-with-srp.md) - UGC 共通ストアで使用可能な SRP の選択肢について説明します。
* [ストレージリソースプロバイダの概要](/help/communities/srp.md)  — 概要とリポジトリ使用の概要
* [SRP と UGC の基本事項](/help/communities/srp-and-ugc.md) - SRP ユーティリティメソッドと例
* [検索の基本事項](/help/communities/search-implementation.md) - UGC 検索に関する基本情報
* [SocialUtils のリファクタリング](/help/communities/socialutils.md)  — 非推奨のユーティリティメソッドを現在の SRP ユーティリティメソッドにマッピングします
