---
title: Communities 用の推奨トポロジ
description: ユーザー生成コンテンツ（UGC）の処理へのアプローチ
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
exl-id: b6658330-d862-44e3-aac0-824fb91cd087
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 11%

---

# Communities 用の推奨トポロジ {#recommended-topologies-for-communities}

AEM Communities 6.1 以降、サイト訪問者（メンバー）がパブリッシュ環境から送信したユーザー生成コンテンツ（UGC）を処理する独自のアプローチが採用されています。

このアプローチは、通常オーサー環境から管理されるサイトコンテンツをAEM プラットフォームが処理する方法とは根本的に異なります。

AEM プラットフォームでは、オーサー環境からパブリッシュ環境にサイトコンテンツをレプリケートするノードストアを使用し、AEM Communitiesでは、UGC のために、レプリケートされない単一の共通ストアを使用します。

共通 UGC ストアの場合は、[&#x200B; ストレージリソースプロバイダー（SRP） &#x200B;](working-with-srp.md) を選択する必要があります。 推奨される選択肢は次のとおりです。

* [DSRP - リレーショナルデータベースストレージリソースプロバイダー](dsrp.md)
* [MSRP - MongoDB ストレージリソースプロバイダー](msrp.md)
* [ASRP - Adobe ストレージリソースプロバイダー](asrp.md)

もう 1 つの SRP オプション [JSRP - JCR ストレージリソースプロバイダー &#x200B;](jsrp.md) では、オーサー環境とパブリッシュ環境の両方のアクセス用に共通の UGC ストアがサポートされていません。

共通のストアを必要とすると、次の推奨トポロジになります。

>[!NOTE]
>
>AEM Communitiesの場合、[UGC はレプリケートされません &#x200B;](working-with-srp.md#ugc-never-replicated)。
>
>デプロイメントに [&#x200B; 共通ストア &#x200B;](working-with-srp.md) が含まれていない場合、UGC は、入力されたAEM パブリッシュインスタンスまたはオーサーインスタンスにのみ表示されます。
>

>[!NOTE]
>
>AEM Platform について詳しくは、[&#x200B; 推奨されるデプロイメント &#x200B;](../../help/sites-deploying/recommended-deploys.md) および [AEM Platform の概要 &#x200B;](../../help/sites-deploying/data-store-config.md) を参照してください。

## 実稼動用 {#for-production}

UGC の共通ストアの確立は不可欠です。したがって、基盤となるデプロイメントは、共通ストアをサポートできるかどうかに依存します。

2 つの例：

1. UGC の予想量が多く、ローカルの MongoDB インスタンスが可能な場合は、[MSRP](msrp.md) が選択されます。

1. ページコンテンツの最適なパフォーマンスを得るために、[&#x200B; パブリッシュファーム &#x200B;](../../help/sites-deploying/recommended-deploys.md#tarmk-farm) および [ASRP](asrp.md) を選択すると、比較的簡単な操作で UGC の最適なスケーリングが行われます。

どちらの場合も、デプロイメントは任意のOAK マイクロカーネルに基づいている可能性があります。

適切な共通店舗を選択するには、それぞれのユニークな [&#x200B; 特性 &#x200B;](working-with-srp.md#characteristics-of-srp-options) を慎重に検討してください。

Oak Microkernals について詳しくは、[&#x200B; 推奨されるデプロイメント &#x200B;](../../help/sites-deploying/recommended-deploys.md) を参照してください。

### TarMK パブリッシュファーム {#tarmk-publish-farm}

トポロジがパブリッシュファームであるとき、関連する重要なトピックは次のとおりです。

* [ユーザー同期](sync.md)
* [ユーザーとユーザーグループの管理](users.md)

### 推奨：DSRP、MSRP または ASRP {#recommended-dsrp-msrp-or-asrp}

| MicroKernel | サイト CONTENTREPOSITORY | ユーザー生成 CONTENTREPOSITORY | ストレージリソースプロバイダー | 共通ストア |
|-------------|------------------------|----------------------------------|---------------------------|---------------|
| いずれか | JCR | MySQL | DSRP | はい |
| いずれか | JCR | MongoDB | MSRP | はい |
| いずれか | JCR | Adobe on-demandstorage | ASRP | はい |

### JSRP {#jsrp}


| デプロイメント | サイト CONTENTREPOSITORY | ユーザー生成 CONTENTREPOSITORY | ストレージリソースプロバイダー | 共通ストア |
|----------------------|------------------------|----------------------------------|---------------------------|---------------------------------|
| TarMK ファーム（デフォルト） | JCR | JCR | JSRP | いいえ |
| Oak クラスター | JCR | JCR | JSRP | パブリッシュ環境でのみ使用 |

## 開発用 {#for-development}

実稼動以外の環境の場合、[JSRP](jsrp.md) を使用すると、1 つのオーサーインスタンスと 1 つのパブリッシュインスタンスを持つ開発環境のセットアップが簡単になります。

実稼動環境で [ASRP](asrp.md)、[DSRP](dsrp.md) または [MSRP](msrp.md) を選択した場合は、Adobeのオンデマンドストレージまたは MongoDB を使用して同様の開発環境をセットアップすることもできます。 例については、[&#x200B; デモ用に MongoDB をセットアップする方法 &#x200B;](demo-mongo.md) を参照してください。

## 参照 {#references}

* [ユーザー同期](sync.md)

  パブリッシュファームインスタンス間でのユーザーデータの同期について説明します。

* [ユーザーとユーザーグループの管理](users.md)

  オーサー環境とパブリッシュ環境におけるユーザーとユーザーグループの役割について説明します。

* UGC[&#x200B; 共通ストア &#x200B;](working-with-srp.md)

  サイトコンテンツとは別に、コミュニティコンテンツのストレージを表します。

* [ノードストアとデータストア](../../help/sites-deploying/data-store-config.md)

  基本的に、サイトコンテンツはノードストアに保存されます。 Assetsでは、バイナリデータを格納するようにデータストアを設定できます。 コミュニティの場合、SRP を選択するように共通ストアを設定する必要があります。

* [ストレージ要素](../../help/sites-deploying/storage-elements-in-aem-6.md)

  2 つのノードストレージ実装（Tar および MongoDB）について説明します。
