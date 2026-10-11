---
title: Communities 用の推奨トポロジ
description: UGCの取り扱いに対するアプローチ
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
exl-id: b6658330-d862-44e3-aac0-824fb91cd087
solution: Experience Manager
feature: Communities
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 11%
---
# Communities 用の推奨トポロジ {#recommended-topologies-for-communities}

AEM Communities 6.1では、サイト訪問者（メンバー）がパブリッシュ環境から送信したユーザー生成コンテンツ（UGC）を処理するための独自のアプローチが採用されています。

このアプローチは、一般的にオーサー環境から管理されるサイトコンテンツを、AEMの基盤が処理する方法とは根本的に異なります。

AEMでは、サイトコンテンツをオーサーからパブリッシュまでレプリケートするノードストアを使用します。一方、AEM Communitiesでは、レプリケートされないUGCに対して、単一の一般的なストアを使用します。

共通のUGC ストアの場合、[ ストレージリソースプロバイダー（SRP） ](working-with-srp.md)を選択する必要があります。 推奨される選択肢は次のとおりです。

* [DSRP - リレーショナルデータベースストレージリソースプロバイダー](dsrp.md)
* [MSRP - MongoDB ストレージリソースプロバイダー](msrp.md)
* [ASRP - Adobe ストレージリソースプロバイダー](asrp.md)

もう1つのSRP オプション [JSRP - JCR ストレージリソースプロバイダー](jsrp.md)は、オーサー環境とパブリッシュ環境の両方にアクセスするための共通のUGC ストアをサポートしていません。

共通のストアを必要とすると、次の推奨トポロジになります。

>[!NOTE]
>
>AEM Communitiesの場合、[UGCはレプリケートされません](working-with-srp.md#ugc-never-replicated)。
>
>デプロイメントに[common store](working-with-srp.md)が含まれていない場合、UGCは、そのUGCが入力されたAEM パブリッシュインスタンスまたはオーサーインスタンスでのみ表示されます。
>

>[!NOTE]
>
>AEM Platformについて詳しくは、[推奨されるデプロイメント ](../../help/sites-deploying/recommended-deploys.md)および[AEM Platformの概要](../../help/sites-deploying/data-store-config.md)を参照してください。

## 本番用 {#for-production}

UGC用の共通ストアを確立することは不可欠です。そのため、共通ストアをサポートできるかどうかは、基盤となるデプロイメントによって異なります。

2つの例：

1. 予想されるUGCのボリュームが多く、ローカル MongoDB インスタンスが可能な場合は、[MSRP](msrp.md)を選択します。

1. ページコンテンツの最適なパフォーマンスを実現するには、[ パブリッシュファーム ](../../help/sites-deploying/recommended-deploys.md#tarmk-farm)と[ASRP](asrp.md)を選択すると、比較的簡単な操作でUGCを最適に拡張できます。

どちらの場合も、デプロイメントは任意のOAK マイクロカーネルに基づいている可能性があります。

適切な共通ストアを選択するには、それぞれの一意の[特性](working-with-srp.md#characteristics-of-srp-options)を慎重に検討します。

Oak マイクロカーナルについて詳しくは、[おすすめのデプロイメント ](../../help/sites-deploying/recommended-deploys.md)を参照してください。

### TarMK パブリッシュファーム {#tarmk-publish-farm}

トポロジがパブリッシュファームの場合、重要な関連トピックは次のとおりです。

* [ユーザー同期](sync.md)
* [ユーザーとユーザーグループの管理](users.md)

### 推奨：DSRP、MSRPまたはASRP {#recommended-dsrp-msrp-or-asrp}

| MicroKernel | サイトコンテンツリポジトリ | ユーザー生成コンテンツリポジトリ | ストレージリソースプロバイダー | 共通ストア |
|-------------|------------------------|----------------------------------|---------------------------|---------------|
| いずれか | JCR | MySQL | DSRP | はい |
| いずれか | JCR | MongoDB | MSRP | はい |
| いずれか | JCR | Adobe オンデマンドストレージ | ASRP | はい |

### JSRP {#jsrp}


| デプロイメント | サイトコンテンツリポジトリ | ユーザー生成コンテンツリポジトリ | ストレージリソースプロバイダー | 共通ストア |
|----------------------|------------------------|----------------------------------|---------------------------|---------------------------------|
| TarMK ファーム （デフォルト） | JCR | JCR | JSRP | いいえ |
| Oak クラスター | JCR | JCR | JSRP | Yesfor パブリッシュ環境のみ |

## 開発用 {#for-development}

実稼動以外の環境の場合、[JSRP](jsrp.md)は、1つのオーサーインスタンスと1つのパブリッシュインスタンスで開発環境を簡単に設定できます。

実稼動用に[ASRP](asrp.md)、[DSRP](dsrp.md)または[MSRP](msrp.md)を選択した場合は、Adobe オンデマンドストレージまたはMongoDBを使用して、同様の開発環境をセットアップすることもできます。 例については、[HowTo Setup MongoDB for Demo](demo-mongo.md)を参照してください。

## 参照 {#references}

* [ユーザー同期](sync.md)

  パブリッシュファームインスタンス間でのユーザーデータの同期化について説明します。

* [ユーザーとユーザーグループの管理](users.md)

  オーサー環境とパブリッシュ環境でのユーザーとユーザーグループの役割について説明します。

* UGC [共通ストア ](working-with-srp.md)

  サイトコンテンツとは別に、コミュニティコンテンツのストレージについて説明します。

* [ノードストアとデータストア](../../help/sites-deploying/data-store-config.md)

  基本的に、サイトコンテンツはノードストアに保存されます。 Assetsの場合、バイナリデータを格納するようにデータストアを設定できます。 Communitiesの場合は、SRPを選択するように共通ストアを設定する必要があります。

* [ストレージ要素](../../help/sites-deploying/storage-elements-in-aem-6.md)

  2つのノードストレージ実装（TarとMongoDB）について説明します。
