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
exl-id: b6658330-d862-44e3-aac0-824fb91cd087
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 42%

---

# Communities 用の推奨トポロジ {#recommended-topologies-for-communities}

AEM Communities 6.1以降では、サイト訪問者（メンバー）がパブリッシュ環境から送信したユーザー生成コンテンツ(UGC)を処理するための独自のアプローチが採用されています。

この手法は、一般的にオーサー環境から管理されるサイトコンテンツを AEM プラットフォームで処理する方法とは根本的に異なります。

AEM プラットフォームではオーサー環境からパブリッシュ環境にサイトコンテンツをレプリケートするノードストアを使用し、AEM Communities では UGC のために単一の共通ストアを使用します。UGC はレプリケートされません。

共通の UGC ストアの場合は、[ストレージリソースプロバイダー（SRP）](working-with-srp.md)を選択する必要があります。推奨される選択肢は次のとおりです。

* [DSRP - リレーショナルデータベースストレージリソースプロバイダー](dsrp.md)
* [MSRP - MongoDB ストレージリソースプロバイダー](msrp.md)
* [ASRP - Adobe ストレージリソースプロバイダー](asrp.md)

もう1つのSRPオプション[JSRP - JCRストレージリソースプロバイダー](jsrp.md)は、オーサー環境とパブリッシュ環境の両方がアクセスできる共通のUGCストアをサポートしていません。

共通ストアが必要な場合は、次のトポロジが推奨されます。

>[!NOTE]
>
>AEM Communitiesの場合、[UGCはレプリケートされません](working-with-srp.md#ugc-never-replicated)。
>
>デプロイメントに[共通ストア](working-with-srp.md)がない場合、UGC は入力された AEM パブリッシュインスタンスまたはオーサーインスタンスのいずれかにのみ表示されます。


>[!NOTE]
>
>AEM プラットフォームについて詳しくは、[推奨されるデプロイメント](../../help/sites-deploying/recommended-deploys.md)と[AEM プラットフォームの概要](../../help/sites-deploying/data-store-config.md)を参照してください。

## 実稼動について  {#for-production}

UGCの共通ストアの確立は不可欠です。したがって、基になるデプロイメントは、共通ストアをサポートする能力に依存しています。

2 つの例を示します。

1. 予想されるUGCのボリュームが大きく、ローカルのMongoDBインスタンスが可能な場合は、[MSRP](msrp.md)を選択します。

1. ページコンテンツの最適なパフォーマンスを得るために、[パブリッシュファーム](../../help/sites-deploying/recommended-deploys.md#tarmk-farm)と[ASRP](asrp.md)を選択すると、比較的簡単な操作でUGCの最適なスケーリングが可能になります。

どちらの場合も、任意の OAK マイクロカーネルを基にデプロイできます。

適切な共通ストアを選択するには、各ストアの固有の[特性](working-with-srp.md#characteristics-of-srp-options)を慎重に考慮します。

Oakマイクロカーネルの詳細については、[推奨されるデプロイメント](../../help/sites-deploying/recommended-deploys.md)を参照してください。

### TarMK パブリッシュファーム {#tarmk-publish-farm}

トポロジがパブリッシュファームの場合、重要なトピックは次のとおりです。

* [ユーザー同期](sync.md)
* [ユーザーとユーザーグループの管理](users.md)

### 推奨：DSRP、MSRP または ASRP {#recommended-dsrp-msrp-or-asrp}

| マイクロカーネル | サイトコンテンツリポジトリ | ユーザー生成CONTENTREPOSITORY | ストレージリソースプロバイダー | 共通ストア |
|-------------|------------------------|----------------------------------|---------------------------|---------------|
| 任意 | JCR | MySQL | DSRP | 可 |
| 任意 | JCR | MongoDB | MSRP | 可 |
| 任意 | JCR | Adobeのオンデマンドストレージ | ASRP | 可 |

### JSRP {#jsrp}


| デプロイメント | サイトコンテンツリポジトリ | ユーザー生成CONTENTREPOSITORY | ストレージリソースプロバイダー | 共通ストア |
|----------------------|------------------------|----------------------------------|---------------------------|---------------------------------|
| TarMK ファーム（デフォルト） | JCR | JCR | JSRP | 不可 |
| Oak クラスター | JCR | JCR | JSRP | 「発行環境専用」 |

## 開発について {#for-development}

非実稼動環境の場合、[JSRP](jsrp.md)は、1つのオーサーインスタンスと1つのパブリッシュインスタンスを使用した開発環境の設定を簡単にします。

実稼動用に[ASRP](asrp.md)、[DSRP](dsrp.md)または[MSRP](msrp.md)を選択した場合は、AdobeオンデマンドストレージまたはMongoDBを使用して、同様の開発環境を設定することもできます。 例えば、[Demo](demo-mongo.md)用にMongoDBを設定する方法を参照してください。

## 参照 {#references}

* [ユーザー同期](sync.md)

   パブリッシュファームインスタンス間でのユーザーデータの同期について説明します。

* [ユーザーとユーザーグループの管理](users.md)

   オーサー環境とパブリッシュ環境におけるユーザーとユーザーグループの役割について説明します。

* UGC [共通ストア](working-with-srp.md)

   サイトコンテンツとは別のコミュニティコンテンツのストレージを表します。

* [ノードストアとデータストア](../../help/sites-deploying/data-store-config.md)

   基本的に、サイトコンテンツはノードストアに格納されます。 Assetsの場合、データストアをバイナリデータを格納するように設定できます。 コミュニティの場合、SRPを選択するために共通ストアを設定する必要があります。

* [ストレージ要素](../../help/sites-deploying/storage-elements-in-aem-6.md)

   次の2つのノードストレージ実装について説明します。TarおよびMongoDB。
