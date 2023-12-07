---
title: Communities 用の推奨トポロジ
description: ユーザー生成コンテンツ (UGC) の処理に近づく方法
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
exl-id: b6658330-d862-44e3-aac0-824fb91cd087
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 11%

---

# Communities 用の推奨トポロジ {#recommended-topologies-for-communities}

AEM Communities 6.1 以降では、サイト訪問者（メンバー）がパブリッシュ環境から送信したユーザー生成コンテンツ (UGC) を処理するための独自のアプローチが採用されています。

この方法は、通常オーサー環境から管理されるサイトコンテンツをAEMプラットフォームが処理する方法とは根本的に異なります。

AEMプラットフォームは、オーサーからパブリッシュにサイトコンテンツをレプリケートするノードストアを使用します。一方、AEM Communitiesは、レプリケートされない UGC に対して、単一の共通ストアを使用します。

共通の UGC ストアの場合は、 [ストレージリソースプロバイダー (SRP)](working-with-srp.md). 推奨される選択肢は次のとおりです。

* [DSRP - リレーショナルデータベースストレージリソースプロバイダー](dsrp.md)
* [MSRP - MongoDB ストレージリソースプロバイダー](msrp.md)
* [ASRP - Adobe ストレージリソースプロバイダー](asrp.md)

もう 1 つの SRP オプション [JSRP - JCR ストレージリソースプロバイダー](jsrp.md)は、オーサー環境とパブリッシュ環境の両方にアクセスするための共通の UGC ストアをサポートしていません。

共通のストアが必要な場合は、次の推奨トポロジが必要になります。

>[!NOTE]
>
>AEM Communitiesの場合、 [UGC はレプリケートされません](working-with-srp.md#ugc-never-replicated).
>
>デプロイメントに [共通店](working-with-srp.md)に設定されている場合、UGC は、入力されたAEMパブリッシュインスタンスまたはオーサーインスタンスでのみ表示されます。
>

>[!NOTE]
>
>AEMプラットフォームについて詳しくは、 [推奨されるデプロイメント](../../help/sites-deploying/recommended-deploys.md) および [AEM Platform の概要](../../help/sites-deploying/data-store-config.md).

## 実稼動用 {#for-production}

UGC の共通ストアの確立は不可欠です。したがって、基になるデプロイメントは、共通ストアをサポートする能力に依存します。

次の 2 つの例を示します。

1. 予想される UGC の量が多く、ローカルの MongoDB インスタンスが可能な場合は、次の選択肢が選択されます。 [MSRP](msrp.md).

1. ページコンテンツの最適なパフォーマンスを得るには、 [パブリッシュファーム](../../help/sites-deploying/recommended-deploys.md#tarmk-farm) および [ASRP](asrp.md) は、比較的簡単な操作で UGC の最適なスケーリングを提供します。

どちらの場合も、任意の OAK マイクロカーネルに基づいたデプロイメントを行うことができます。

適切な共通ストアを選択するには、固有の [特性](working-with-srp.md#characteristics-of-srp-options) それぞれの

Oak マイクロカーネルの詳細については、 [推奨されるデプロイメント](../../help/sites-deploying/recommended-deploys.md).

### TarMK パブリッシュファーム {#tarmk-publish-farm}

トポロジがパブリッシュファームの場合、重要なトピックは次のとおりです。

* [ユーザー同期](sync.md)
* [ユーザーとユーザーグループの管理](users.md)

### 推奨： DSRP、MSRP、ASRP {#recommended-dsrp-msrp-or-asrp}

| MicroKernel | サイト CONTENTREPOSITORY | ユーザー生成コンテンツリポジトリ | ストレージリソースプロバイダ | 共通ストア |
|-------------|------------------------|----------------------------------|---------------------------|---------------|
| いずれか | JCR | MySQL | DSRP | はい |
| いずれか | JCR | MongoDB | MSRP | はい |
| いずれか | JCR | Adobeのオンデマンドストレージ | ASRP | はい |

### JSRP {#jsrp}


| デプロイメント | サイト CONTENTREPOSITORY | ユーザー生成コンテンツリポジトリ | ストレージリソースプロバイダ | 共通ストア |
|----------------------|------------------------|----------------------------------|---------------------------|---------------------------------|
| TarMK ファーム（デフォルト） | JCR | JCR | JSRP | いいえ |
| Oak クラスタ | JCR | JCR | JSRP | 「はい（パブリッシュ環境のみ）」 |

## 開発用 {#for-development}

実稼動以外の環境の場合、 [JSRP](jsrp.md) は、1 つのオーサーインスタンスと 1 つのパブリッシュインスタンスを使用して開発環境を簡単に設定できるようにします。

を選択する場合 [ASRP](asrp.md), [DSRP](dsrp.md) または [MSRP](msrp.md) 実稼動環境では、Adobeオンデマンドストレージまたは MongoDB を使用して、同様の開発環境を設定することもできます。 例については、 [デモ用に MongoDB を設定する方法](demo-mongo.md).

## 参照 {#references}

* [ユーザー同期](sync.md)

  パブリッシュファームインスタンス間でのユーザーデータの同期について説明します。

* [ユーザーとユーザーグループの管理](users.md)

  オーサー環境とパブリッシュ環境におけるユーザーとユーザーグループの役割について説明します。

* UGC [共通店](working-with-srp.md)

  コミュニティコンテンツのストレージを、サイトコンテンツとは別に記述します。

* [ノードストアとデータストア](../../help/sites-deploying/data-store-config.md)

  基本的に、サイトのコンテンツはノードストアに格納されます。 Assets の場合は、バイナリデータを格納するようにデータストアを設定できます。 コミュニティの場合、SRP を選択するには、共通ストアを設定する必要があります。

* [ストレージ要素](../../help/sites-deploying/storage-elements-in-aem-6.md)

  Tar と MongoDB の 2 つのノードストレージ実装について説明します。
