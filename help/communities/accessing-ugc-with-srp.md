---
title: SRP による UGC へのアクセス
description: サイトがASRPまたはMSRPを使用するように設定されている場合、実際のUGCはAEMのノードストア（JCR）に保存されません
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
source-wordcount: '342'
ht-degree: 3%

---

# SRP による UGC へのアクセス {#accessing-ugc-with-srp}

## SRPについて {#about-srp}

すべてのAEM Communities コンポーネントと機能は、[&#x200B; ソーシャルコンポーネントフレームワーク（SCF） &#x200B;](/help/communities/scf.md)上に構築されており、SocialResourceProvider APIを呼び出して、すべてのユーザー生成コンテンツ（UGC）にアクセスします。

コミュニティサイトを作成する前に、[&#x200B; ストレージリソースプロバイダー（SRP） &#x200B;](/help/communities/working-with-srp.md)を設定して、基になる[&#x200B; トポロジ &#x200B;](/help/communities/topologies.md)と一致する実装を選択する必要があります。 SRPの実装は、次の3つのストレージオプションに基づいています。

1. [ASRP](/help/communities/asrp.md) - Adobe オンデマンドストレージ
1. [MSRP](/help/communities/msrp.md) - MongoDB
1. [JSRP](/help/communities/jsrp.md) - JCR

## UGC ストレージについて {#about-ugc-storage}

UGCの保存について知っておくべき重要なことは、サイトがASRPまたはMSRPを使用するように設定されている場合、実際のUGCはAEMの[node store](/help/sites-deploying/data-store-config.md) （JCR）に保存されないことです。

JCRには、UGCをシャドウして有用なメタデータを提供するノードがありますが、これらのノードは実際のUGCと混同しないでください。

[&#x200B; ストレージリソースプロバイダーの概要を参照してください。](/help/communities/srp.md)

## ベストプラクティス {#best-practice}

カスタムコンポーネントを開発する場合、開発者は、現在選択されているトポロジとは独立してコードを作成するように注意する必要があります。これにより、将来的に新しいトポロジに移行する柔軟性を維持できます。

### JCRを使用できないと仮定 {#assume-jcr-not-available}

JCRに固有の方法は避けるべきです。

使用する方法：

* Sling API （Sling リソース）

   * jcr ノードがあると仮定しないでください

* OSGi イベント

   * jcr イベントが存在すると仮定しないでください

* [SocialResourceUtilities](/help/communities/socialutils.md#socialresourceutilities-package)
* [SCFUtilities](/help/communities/socialutils.md#scfutilities-package)

回避すべき方法：

* ノード API
* JCR イベント
* ワークフローランチャー（JCR イベントを使用）

### 検索コレクションを使用 {#use-search-collections}

SRPごとに、ネイティブクエリ言語を指定できます。 [com.adobe.cq.social.ugc.api](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) パッケージのメソッドを使用して、適切なクエリ言語を実行します。

詳しくは、[検索エッセンシャル &#x200B;](/help/communities/search-implementation.md)を参照してください。

## リソース {#resources}

* [&#x200B; コミュニティコンテンツストレージ &#x200B;](/help/communities/working-with-srp.md) - UGC共通ストアで利用可能なSRPの選択肢について説明します
* [&#x200B; ストレージリソースプロバイダーの概要](/help/communities/srp.md) – 概要とリポジトリの使用状況の概要
* [SRPおよびUGC Essentials](/help/communities/srp-and-ugc.md) - SRP ユーティリティのメソッドと例
* [Search Essentials](/help/communities/search-implementation.md) - UGCを検索するための必須情報
* [SocialUtils リファクタリング &#x200B;](/help/communities/socialutils.md) – 非推奨のユーティリティメソッドを現在のSRP ユーティリティメソッドにマッピング
