---
title: Communities 用の推奨トポロジ
seo-title: Recommended Topologies for Communities
description: ユーザー生成コンテンツ（UGC）の処理への取り組み方
seo-description: How to approach the handling of user-generated content (UGC)
uuid: 4bc1c423-0ba9-4f2e-b11c-4d6824f45641
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: 46f135de-a0bf-451d-bdcc-fb29188250aa
exl-id: b6658330-d862-44e3-aac0-824fb91cd087
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 43%

---

# Communities 用の推奨トポロジ {#recommended-topologies-for-communities}

AEM Communities 6.1 以降では、サイト訪問者（メンバー）がパブリッシュ環境から送信したユーザー生成コンテンツ (UGC) を処理するための独自のアプローチが採用されています。

この手法は、一般的にオーサー環境から管理されるサイトコンテンツを AEM プラットフォームで処理する方法とは根本的に異なります。

AEM プラットフォームではオーサー環境からパブリッシュ環境にサイトコンテンツをレプリケートするノードストアを使用し、AEM Communities では UGC のために単一の共通ストアを使用します。UGC はレプリケートされません。

共通の UGC ストアの場合は、[ストレージリソースプロバイダー（SRP）](working-with-srp.md)を選択する必要があります。推奨される選択肢は次のとおりです。

* [DSRP - リレーショナルデータベースストレージリソースプロバイダー](dsrp.md)
* [MSRP - MongoDB ストレージリソースプロバイダー](msrp.md)
* [ASRP - Adobe ストレージリソースプロバイダー](asrp.md)

もう 1 つの SRP オプション [JSRP - JCR ストレージリソースプロバイダー](jsrp.md)は、オーサー環境とパブリッシュ環境の両方にアクセスするための共通の UGC ストアをサポートしていません。

共通ストアが必要な場合は、次のトポロジが推奨されます。

>[!NOTE]
>
>AEM Communities、 [UGC はレプリケートされません](working-with-srp.md#ugc-never-replicated).
>
>デプロイメントに[共通ストア](working-with-srp.md)がない場合、UGC は入力された AEM パブリッシュインスタンスまたはオーサーインスタンスのいずれかにのみ表示されます。

>[!NOTE]
>
>AEM プラットフォームについて詳しくは、[推奨されるデプロイメント](../../help/sites-deploying/recommended-deploys.md)と[AEM プラットフォームの概要](../../help/sites-deploying/data-store-config.md)を参照してください。

## 実稼動について {#for-production}

UGC の共通ストアの確立は不可欠です。したがって、基になるデプロイメントは、共通ストアをサポートする能力に依存します。

2 つの例を示します。

1. 予想される UGC の量が多く、ローカルの MongoDB インスタンスが可能な場合は、次の選択肢が選択されます [MSRP](msrp.md).

1. ページコンテンツの最適なパフォーマンスを得るには、 [パブリッシュファーム](../../help/sites-deploying/recommended-deploys.md#tarmk-farm) および [ASRP](asrp.md) は、比較的簡単な操作で UGC の最適なスケーリングを提供します。

どちらの場合も、任意の OAK マイクロカーネルを基にデプロイできます。

適切な共通ストアを選択するには、固有の [特性](working-with-srp.md#characteristics-of-srp-options) 各

Oak マイクロカーネルの詳細については、 [推奨されるデプロイメント](../../help/sites-deploying/recommended-deploys.md).

### TarMK パブリッシュファーム {#tarmk-publish-farm}

次に、トポロジがパブリッシュファームの場合に重要な関連トピックを示します。：

* [ユーザー同期](sync.md)
* [ユーザーとユーザーグループの管理](users.md)

### 推奨：DSRP、MSRP または ASRP {#recommended-dsrp-msrp-or-asrp}

| マイクロカーネル | サイト CONTENTREPOSITORY | ユーザー生成コンテンツリポジトリ | ストレージリソースプロバイダー | 共通ストア |
|-------------|------------------------|----------------------------------|---------------------------|---------------|
| 任意 | JCR | MySQL | DSRP | はい |
| 任意 | JCR | MongoDB | MSRP | はい |
| 任意 | JCR | Adobeオンデマンドストレージ | ASRP | はい |

### JSRP {#jsrp}


| デプロイメント | サイト CONTENTREPOSITORY | ユーザー生成コンテンツリポジトリ | ストレージリソースプロバイダー | 共通ストア |
|----------------------|------------------------|----------------------------------|---------------------------|---------------------------------|
| TarMK ファーム（デフォルト） | JCR | JCR | JSRP | いいえ |
| Oak クラスター | JCR | JCR | JSRP | 「はい（パブリッシュ環境のみ）」 |

## 開発について {#for-development}

非実稼動環境の場合、 [JSRP](jsrp.md) は、1 つのオーサーインスタンスと 1 つのパブリッシュインスタンスを使用して開発環境を簡単に設定できるようにします。

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

   次の 2 つのノードストレージ実装について説明します。Tar および MongoDB。
