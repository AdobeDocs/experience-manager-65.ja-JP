---
title: Communities 用の推奨トポロジ
seo-title: Communities 用の推奨トポロジ
description: ユーザー生成コンテンツ（UGC）の処理への取り組み方
seo-description: ユーザー生成コンテンツ（UGC）の処理への取り組み方
uuid: 4bc1c423-0ba9-4f2e-b11c-4d6824f45641
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: 46f135de-a0bf-451d-bdcc-fb29188250aa
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 43%

---


# Communities 用の推奨トポロジ {#recommended-topologies-for-communities}

AEM Communities6.1以降、サイト訪問者（会員）が発行環境から提出したユーザ生成コンテンツ(UGC)の処理には、独自のアプローチが採用されています。

この手法は、一般的にオーサー環境から管理されるサイトコンテンツを AEM プラットフォームで処理する方法とは根本的に異なります。

AEM プラットフォームではオーサー環境からパブリッシュ環境にサイトコンテンツをレプリケートするノードストアを使用し、AEM Communities では UGC のために単一の共通ストアを使用します。UGC はレプリケートされません。

共通の UGC ストアの場合は、[ストレージリソースプロバイダー（SRP）](working-with-srp.md)を選択する必要があります。推奨される選択肢は次のとおりです。

* [DSRP - リレーショナルデータベースストレージリソースプロバイダー](dsrp.md)
* [MSRP - MongoDB ストレージリソースプロバイダー](msrp.md)
* [ASRP - Adobe ストレージリソースプロバイダー](asrp.md)

もう1つのSRPオプション[JSRP - JCRストレージリソースプロバイダー](jsrp.md)は、両方のアクセスに対して、作成者と発行環境の共通のUGCストアをサポートしていません。

共通ストアが必要な場合は、次のトポロジが推奨されます。

>[!NOTE]
>
>AEM Communitiesの場合、[UGCは](working-with-srp.md#ugc-never-replicated)複製されません。
>
>デプロイメントに[共通ストア](working-with-srp.md)がない場合、UGC は入力された AEM パブリッシュインスタンスまたはオーサーインスタンスのいずれかにのみ表示されます。


>[!NOTE]
>
>AEM プラットフォームについて詳しくは、[推奨されるデプロイメント](../../help/sites-deploying/recommended-deploys.md)と[AEM プラットフォームの概要](../../help/sites-deploying/data-store-config.md)を参照してください。

## 実稼動について  {#for-production}

UGCに共通のストアを確立することは不可欠です。したがって、基盤となるデプロイメントは、共通のストアをサポートする能力に左右されます。

2 つの例を示します。

1. 予想されるUGCの量が多く、ローカルのMongoDBインスタンスが可能な場合は、[MSRP](msrp.md)を選択します。

1. ページコンテンツの最適なパフォーマンスを得るために、[パブリッシュファーム](../../help/sites-deploying/recommended-deploys.md#tarmk-farm)と[ASRP](asrp.md)を選択すると、比較的単純な操作でUGCの最適な拡大・縮小が行われます。

どちらの場合も、任意の OAK マイクロカーネルを基にデプロイできます。

適切な共通ストアを選択するには、それぞれの[特性](working-with-srp.md#characteristics-of-srp-options)を慎重に検討します。

Oakマイクロカーナルの詳細については、[推奨されるデプロイメント](../../help/sites-deploying/recommended-deploys.md)を参照してください。

### TarMK パブリッシュファーム {#tarmk-publish-farm}

トポロジが発行ファームの場合、重要な関連トピックは次のとおりです。

* [ユーザーの同期](sync.md)
* [ユーザーとユーザーグループの管理](users.md)

### 推奨：DSRP、MSRP または ASRP {#recommended-dsrp-msrp-or-asrp}

| マイクロカーネル | サイトコンテンツリポジトリ | ユーザー生成CONTENTREPOSITORY | ストレージリソースプロバイダー | 共通店 |
|-------------|------------------------|----------------------------------|---------------------------|---------------|
| 任意 | JCR | MySQL | DSRP | 可 |
| 任意 | JCR | MongoDB | MSRP | 可 |
| 任意 | JCR | Adobeのオンデマンドストレージ | ASRP | はい |

### JSRP  {#jsrp}


| デプロイメント | サイトコンテンツリポジトリ | ユーザー生成CONTENTREPOSITORY | ストレージリソースプロバイダー | 共通店 |
|----------------------|------------------------|----------------------------------|---------------------------|---------------------------------|
| TarMK ファーム（デフォルト） | JCR | JCR | JSRP | 不可 |
| Oak クラスター | JCR | JCR | JSRP | 公開環境のみ |

## 開発について {#for-development}

実稼働以外の環境では、[JSRP](jsrp.md)を使用すると、1つの作成者インスタンスと1つの発行インスタンスを持つ開発環境を簡単に設定できます。

実稼働用に[ASRP](asrp.md)、[DSRP](dsrp.md)、[MSRP](msrp.md)を選択した場合、AdobeオンデマンドストレージまたはMongoDBを使用して、同様の開発環境を設定することもできます。 例については、[HowTo Setup MongoDB for Demo](demo-mongo.md)を参照してください。

## 参照 {#references}

* [ユーザーの同期](sync.md)

   発行ファームインスタンス間でのユーザーデータの同期について説明します。

* [ユーザーとユーザーグループの管理](users.md)

   作成者および公開環境におけるユーザーとユーザーグループの役割について説明します。

* UGC [共通ストア](working-with-srp.md)

   コミュニティコンテンツのストレージを、サイトコンテンツとは別に説明します。

* [ノードストアとデータストア](../../help/sites-deploying/data-store-config.md)

   基本的に、サイトのコンテンツはノードストアに保存されます。 アセットの場合、データストアはバイナリデータを格納するように設定できます。 Communitiesの場合、SRPを選択するように共通ストアを設定する必要があります。

* [AEM 6.3 のストレージ要素](../../help/sites-deploying/storage-elements-in-aem-6.md)

   2つのノードストレージの実装について説明します。TarおよびMongoDB。
