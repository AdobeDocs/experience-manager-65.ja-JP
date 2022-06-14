---
title: SRP による UGC へのアクセス
seo-title: Accessing UGC with SRP
description: ASRP または MSRP を使用するようにサイトが設定されている場合、実際の UGC は AEM のノードストア（JCR）に格納されません。
seo-description: When a site is configured to use ASRP or MSRP, the actual UGC is not be stored in AEM's node store (JCR)
uuid: 30549f93-e370-4b8b-a35a-69e05884227e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 72d4022c-43ba-49e0-b94c-f2beabaef64d
docset: aem65
exl-id: 1157366f-2cc5-46e4-8ec6-e66fe5d0a0f6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 61%

---

# SRP による UGC へのアクセス {#accessing-ugc-with-srp}

## SRP について {#about-srp}

すべてのAEM Communitiesのコンポーネントと機能は、 [ソーシャルコンポーネントフレームワーク (SCF)](/help/communities/scf.md)を呼び出し、 SocialResourceProvider API を呼び出してユーザー生成コンテンツ (UGC) にアクセスします。

コミュニティサイトを作成する前に、 [ストレージリソースプロバイダー (SRP)](/help/communities/working-with-srp.md) は、基になる [トポロジ](/help/communities/topologies.md). SRP の実装は、次の 3 つのストレージオプションに基づいています。

1. [ASRP](/help/communities/asrp.md) - Adobe オンデマンドストレージ
1. [MSRP](/help/communities/msrp.md) - MongoDB
1. [JSRP](/help/communities/jsrp.md) - JCR

## UGC のストレージについて {#about-ugc-storage}

UGC のストレージに関して知っておくべき重要な点は、ASRP または MSRP を使用するようにサイトを設定する場合、実際の UGC はAEMに格納されないことです [ノードストア](/help/sites-deploying/data-store-config.md) (JCR)。

UGC をコピーして有用なメタデータを提供するノードが JCR 内に存在する場合がありますが、実際の UGC とこれらのノードを混同しないでください。

[ストレージリソースプロバイダーの概要](/help/communities/srp.md)を参照してください。

## ベストプラクティス {#best-practice}

カスタムコンポーネントを開発する際、開発者は、現在どのトポロジを選択しているかに関係なく、将来新しいトポロジに移行する柔軟性を保ちながら、慎重にコーディングする必要があります。

### JCR を使用できないことを想定する {#assume-jcr-not-available}

JCR に固有のメソッドの使用は避ける必要があります。

使用するメソッドは次のとおりです。

* Sling API（Sling リソース）

   * JCR ノードがあることを想定しないでください。

* OSGi イベント

   * JCR イベントがあることを想定しないでください。

* [SocialResourceUtilities](/help/communities/socialutils.md#socialresourceutilities-package)
* [SCFUtilities](/help/communities/socialutils.md#scfutilities-package)

使用を避けるメソッドは次のとおりです。

* Node API
* JCR イベント
* ワークフローランチャー（JCR イベントを使用する）

### 検索コレクションを使用する {#use-search-collections}

SRP ごとにネイティブなクエリー言語が異なる場合があります。メソッドは、 [com.adobe.cq.social.ugc.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) 適切なクエリ言語を実行するためのパッケージ。

詳しくは、[検索の基本事項](/help/communities/search-implementation.md)を参照してください。

## リソース {#resources}

* [コミュニティコンテンツストレージ](/help/communities/working-with-srp.md) - UGC 共通ストアに使用できる SRP の選択肢
* [ストレージリソースプロバイダーの概要](/help/communities/srp.md) - 序論とリポジトリの使用方法の概要
* [SRP と UGC の基本事項](/help/communities/srp-and-ugc.md) - SRP ユーティリティメソッドと例
* [検索の基本事項](/help/communities/search-implementation.md) - UGC の検索に関する基本情報
* [SocialUtils のリファクタリング](/help/communities/socialutils.md) - 廃止されたユーティリティメソッドと現在の SRP ユーティリティメソッドの対応関係
