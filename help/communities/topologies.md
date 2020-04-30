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
source-git-commit: 77d00c1d6e94b257aa0533ca88b5f9a12dba0054

---


# Communities 用の推奨トポロジ {#recommended-topologies-for-communities}

AEM Communities 6.1では、サイト訪問者（メンバー）が発行環境から送信したユーザ生成コンテンツ(UGC)を処理するための独自のアプローチが採用されています。

この手法は、一般的にオーサー環境から管理されるサイトコンテンツを AEM プラットフォームで処理する方法とは根本的に異なります。

AEM プラットフォームではオーサー環境からパブリッシュ環境にサイトコンテンツをレプリケートするノードストアを使用し、AEM Communities では UGC のために単一の共通ストアを使用します。UGC はレプリケートされません。

共通の UGC ストアの場合は、[ストレージリソースプロバイダー（SRP）](working-with-srp.md)を選択する必要があります。推奨される選択肢は次のとおりです。

* [DSRP - リレーショナルデータベースストレージリソースプロバイダー](dsrp.md)
* [MSRP - MongoDB ストレージリソースプロバイダー](msrp.md)
* [ASRP - Adobe ストレージリソースプロバイダー](asrp.md)

One other SRP option, [JSRP - JCR Storage Resource Provider](jsrp.md), does not support a common UGC store for the author and publish environments to both access.

共通ストアが必要な場合は、次のトポロジが推奨されます。

>[!NOTE]
>
>For AEM Communities, [UGC is never replicated](working-with-srp.md#ugc-never-replicated).
>
>デプロイメントに[共通ストア](working-with-srp.md)がない場合、UGC は入力された AEM パブリッシュインスタンスまたはオーサーインスタンスのいずれかにのみ表示されます。


>[!NOTE]
>
>AEM プラットフォームについて詳しくは、[推奨されるデプロイメント](../../help/sites-deploying/recommended-deploys.md)と[AEM プラットフォームの概要](../../help/sites-deploying/data-store-config.md)を参照してください。


## 実稼動について {#for-production}

UGC用の共通ストアを確立することは重要なので、基盤となるデプロイメントは共通ストアをサポートする能力に左右されます。

2 つの例を示します。

1. If the expected volume of UGC is high and a local MongoDB instance is possible, then the choice would be [MSRP](msrp.md).

1. For optimal performance for page content, the choice of a [publish farm](../../help/sites-deploying/recommended-deploys.md#tarmk-farm) and [ASRP](asrp.md) would provide optimal scaling of UGC with relatively straightforward operations.

どちらの場合も、任意の OAK マイクロカーネルを基にデプロイできます。

To choose the appropriate common store, carefully consider the unique [characteristics](working-with-srp.md#characteristics-of-srp-options) of each.

For more details on Oak microkernals, visit [Recommended Deployments](../../help/sites-deploying/recommended-deploys.md).

### TarMK パブリッシュファーム {#tarmk-publish-farm}

トポロジがパブリッシュファームの場合、重要な関連トピックは次のとおりです。

* [ユーザーの同期](sync.md)
* [ユーザーとユーザーグループの管理](users.md)

### 推奨：DSRP、MSRP または ASRP {#recommended-dsrp-msrp-or-asrp}

| マイクロカーネル | サイトコンテンツリポジトリ | ユーザー生成CONTENTREPOSITORY | ストレージリソースプロバイダー | 共通店 |
|-------------|------------------------|----------------------------------|---------------------------|---------------|
| 任意 | JCR | MySQL | DSRP | 可 |
| 任意 | JCR | MongoDB | MSRP | 可 |
| 任意 | JCR | アドビのオンデマンドストレージ | ASRP | Yes |

### JSRP {#jsrp}


| デプロイメント | サイトコンテンツリポジトリ | ユーザー生成CONTENTREPOSITORY | ストレージリソースプロバイダー | 共通店 |
|----------------------|------------------------|----------------------------------|---------------------------|---------------------------------|
| TarMK ファーム（デフォルト） | JCR | JCR | JSRP | 不可 |
| Oak クラスター | JCR | JCR | JSRP | はい公開環境のみ |

## 開発について {#for-development}

For non-production environments, [JSRP](jsrp.md) provides simplicity in setting up a development environment with one author instance and one publish instance.

If choosing [ASRP](asrp.md), [DSRP](dsrp.md) or [MSRP](msrp.md) for production, it is also possible to setup a similar development environment using Adobe on-demand storage or MongoDB. For an example, see [HowTo Setup MongoDB for Demo](demo-mongo.md).

## 参照 {#references}

* [ユーザーの同期](sync.md)

   発行ファームインスタンス間でのユーザーデータの同期化を説明します。

* [ユーザーとユーザーグループの管理](users.md)

   作成者および発行ユーザーのユーザーおよびユーザーグループの役割について説明します。環境

* UGC共 [通店](working-with-srp.md)

   コミュニティコンテンツのストレージを、サイトコンテンツとは別に説明します。

* [ノードストアとデータストア](../../help/sites-deploying/data-store-config.md)

   基本的に、サイトのコンテンツはノードストアに保存されます。 アセットの場合、データストアはバイナリデータを格納するように設定できます。 コミュニティの場合、SRPを選択するように共通ストアを設定する必要があります。

* [AEM 6.3 のストレージ要素](../../help/sites-deploying/storage-elements-in-aem-6.md)

   2つのノードの実装についてストレージします。TarおよびMongoDB。
