---
title: SRP による UGC へのアクセス
seo-title: SRP による UGC へのアクセス
description: ASRP または MSRP を使用するようにサイトが設定されている場合、実際の UGC は AEM のノードストア（JCR）に格納されません。
seo-description: ASRP または MSRP を使用するようにサイトが設定されている場合、実際の UGC は AEM のノードストア（JCR）に格納されません。
uuid: 30549f93-e370-4b8b-a35a-69e05884227e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 72d4022c-43ba-49e0-b94c-f2beabaef64d
docset: aem65
translation-type: tm+mt
source-git-commit: 974d58efa560b90234d5121a11bdb445c7bf94cf
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 64%

---


# SRP による UGC へのアクセス {#accessing-ugc-with-srp}

## SRP について {#about-srp}

すべてのAEM Communitiesのコンポーネントと機能は、[ソーシャルコンポーネントフレームワーク(SCF)](/help/communities/scf.md)上に構築されています。このフレームワークは、SocialResourceProvider APIを呼び出してユーザー生成コンテンツ(UGC)にアクセスします。

コミュニティサイトを作成する前に、[ストレージリソースプロバイダー(SRP)](/help/communities/working-with-srp.md)を構成し、基になる[トポロジ](/help/communities/topologies.md)と一致する実装を選択する必要があります。 SRPの実装は、次の3つのストレージオプションに基づいています。

1. [ASRP](/help/communities/asrp.md) - Adobe オンデマンドストレージ
1. [MSRP](/help/communities/msrp.md) - MongoDB
1. [JSRP](/help/communities/jsrp.md) - JCR

## UGC のストレージについて  {#about-ugc-storage}

UGCのストレージに関して知っておくべき重要な点は、サイトがASRPまたはMSRPを使用するように設定されている場合、実際のUGCはAEM [node store](/help/sites-deploying/data-store-config.md)(JCR)に格納されないことです。

UGC をコピーして有用なメタデータを提供するノードが JCR 内に存在する場合がありますが、実際の UGC とこれらのノードを混同しないでください。

[ストレージリソースプロバイダーの概要](/help/communities/srp.md)を参照してください。

## ベストプラクティス  {#best-practice}

カスタムコンポーネントを開発する際、開発者は、現在どのトポロジを選択しているかに関係なく、将来新しいトポロジに移行する柔軟性を保ちながら、慎重にコーディングする必要があります。

### JCR を使用できないことを想定する  {#assume-jcr-not-available}

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

### 検索コレクションを使用する  {#use-search-collections}

SRP ごとにネイティブなクエリー言語が異なる場合があります。適切なクエリ言語を実行するには、[com.adobe.cq.sosical.ugc.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html)パッケージのメソッドを使用することをお勧めします。

詳しくは、[検索の基本事項](/help/communities/search-implementation.md)を参照してください。

## リソース {#resources}

* [コミュニティコンテンツストレージ](/help/communities/working-with-srp.md) - UGC 共通ストアに使用できる SRP の選択肢
* [ストレージリソースプロバイダーの概要](/help/communities/srp.md) - 序論とリポジトリの使用方法の概要
* [SRPとUGC Essentials](/help/communities/srp-and-ugc.md)  - SRPユーティリティのメソッドと例
* [検索の基本事項](/help/communities/search-implementation.md) - UGC の検索に関する基本情報
* [SocialUtils のリファクタリング](/help/communities/socialutils.md) - 廃止されたユーティリティメソッドと現在の SRP ユーティリティメソッドの対応関係

