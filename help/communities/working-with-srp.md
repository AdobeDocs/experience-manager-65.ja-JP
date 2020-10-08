---
title: SRP - コミュニティコンテンツストレージ
seo-title: SRP - コミュニティコンテンツストレージ
description: AEM Communities 6.1 以降、ユーザー生成コンテンツ（UGC）は、ストレージリソースプロバイダー（SRP）により提供される単一の共通ストアに格納されます
seo-description: AEM Communities 6.1 以降、ユーザー生成コンテンツ（UGC）は、ストレージリソースプロバイダー（SRP）により提供される単一の共通ストアに格納されます
uuid: d45e03c4-378b-4510-a6a0-d48c8cb879d9
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 6f13b21a-f4ef-4889-9b8e-4da3f846fa35
docset: aem65
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '921'
ht-degree: 31%

---


# SRP - コミュニティコンテンツストレージ {#srp-community-content-storage}

## 概要 {#introduction}

AEM Communities6.1以降、ユーザ生成コンテンツ(UGC)は、ストレージリソースプロバイダ(SRP)が提供する単一の共通ストアに格納されます。 ASRP、MSRP、JSRPなど、選択できるSRPオプションがいくつかあります。

以前のリリースとは異なり、AEM インスタンス間の UGC のリバース／フォワードレプリケーションはありません。代わりに、JSRPを除き、UGCは作成、読み取り、更新、削除(CRUD)操作の作成、削除(JSRP)操作に直接アクセスできます。

Following are the [characteristics of each SRP option](#characteristics-of-srp-options), which is crucial information for the decision process when choosing the appropriate SRP and [underlying deployment](/help/communities/topologies.md).

For details regarding the use of SRP for UGC, see [Storage Resource Provider Overview](/help/communities/srp.md).

>[!NOTE]
>
>SRP はコミュニティコンテンツにのみ適用されます。It does not affect where site content is stored ([node store](/help/sites-deploying/data-store-config.md)), and does not affect the secure handling of user registration, user profiles and user groups between AEM instances (see also [Managing User Data](#managing-user-data)).

>[!CAUTION]
>
>As of AEM 6.1, [UGC is never replicated](#ugc-never-replicated).
>
>デプロイメントに共通ストアが含まれていない場合（デフォルトの [JSRP](/help/communities/topologies.md#jsrp) トポロジなど）、UGC は、それが入力された AEM パブリッシュインスタンスまたはオーサーインスタンスでのみ表示可能になります。トポロジにパブリッシュクラスタが含まれる場合にのみ、UGCは任意のパブリッシュインスタンスで表示されます。

## SRP オプションの特性 {#characteristics-of-srp-options}

[ASRP - Adobe ストレージリソースプロバイダー](/help/communities/asrp.md)

このオプションを使用すると、Adobeがホストし管理するクラウドサービスでUGCがリモートで保持されます。 その場合は、追加のライセンスが必要です。また、アカウントを特定のライセンス用にプロビジョニングするには、アカウント担当者と連携する必要があります。 ASRPには次の要件があります。

* Adobeが提供およびサポートし、コミュニティコンテンツを保存するための関連クラウドサービス。
* 特定の地域（米国、EMEA、APAC）のデータセンターを選択。

* UGCへのプログラムによるアクセスはすべてSRP APIを通じて行われます。

ASRPが適しています。

* TarMK発行ファームの場合。
* 現地ストレージに投資する意図がない場合。

>[!NOTE]
>
>ASRPでの投稿（またはコメント）に添付ファイルをアップロードする場合、制限はあります(50 MB)。

[MSRP - MongoDB ストレージリソースプロバイダー](/help/communities/msrp.md)

このオプションを使用すると、UGCはローカルのMongoDBインスタンスで直接保持されます。

MSRPには次が必要です。

* コミュニティコンテンツを保存するMongoDBのローカルインストール。
* Apache Solrのローカルインストール。
* UGCへのプログラムによるアクセスはすべてSRP APIを通じて行われます。

ASRPが適しています。

* 既存のTarMK発行ファームの場合。
* MongoMKまたはRdbMKクラスターの場合。
* 大量のコミュニティコンテンツを期待する場合。

[DSRP - リレーショナルデータベースストレージリソースプロバイダー](/help/communities/dsrp.md)

このオプションを使用すると、UGCはローカルのMySQLデータベースインスタンスに直接保持されます。

DSRPには次が必要です。

* コミュニティコンテンツを保存するMySQLのローカルインストール。
* Apache Solrのローカルインストール。
* UGCへのプログラムによるアクセスはすべてSRP APIを通じて行われます。

DSRPが適しています。

* 既存のTarMK発行ファームの場合。
* MongoMKまたはRdbMKクラスターの場合。
* 大量のコミュニティコンテンツを期待する場合。

[JSRP - JCR ストレージリソースプロバイダー](/help/communities/jsrp.md)

デフォルトのオプションでは、共通ストアはありません。 UGCは、入力されたAEMインスタンスと同じJCRリポジトリにのみ保持されます。

JSRP:

* コミュニティコンテンツは、投稿先のAEM作成者または発行インスタンスのJCRリポジトリに保存されます。
* UGCへのすべてのプログラムによるアクセスは、SRP APIを通じて行う必要があります。
* 複数の発行インスタンスがデプロイされている場合（TarMKファーム内の発行インスタンス間に複製メカニズムがない場合）、発行クラスターが必要です。
* モデレートは、発行環境でのみ実行されます（作成者と発行の間に逆/転送のレプリケーションメカニズムはありません）。
* 開発、デモ、トレーニングに最適です。

## SRP の設定 {#configuring-srp}

デフォルトのストレージオプションの指定は、基礎となるデプロイメントに基づき、[ストレージ設定コンソール](/help/communities/srp-config.md)でおこないます。

各オプションの設定について詳しくは、以下を参照してください。

* [ASRP - Adobe ストレージリソースプロバイダー](/help/communities/asrp.md)
* [MSRP - MongoDB ストレージリソースプロバイダー](/help/communities/msrp.md)
* [DSRP - リレーショナルデータベースストレージリソースプロバイダー](/help/communities/dsrp.md)
* [JSRP - JCR ストレージリソースプロバイダー](/help/communities/jsrp.md)

ストレージオプションが選択されていない場合は、JSRP がデフォルトで有効になります。

## 追加情報 {#additional-information}

### UGC のレプリケーションの廃止 {#ugc-never-replicated}

作成者はオーサー環境でページコンテンツを作成し、パブリッシュ環境にレプリケートします。ページにコメント、レビュー、フォーラム、ブログ、QnAなどのインタラクティブなAEM Communities機能が含まれる場合、メンバーによる(サイト訪問者でサインインした)発行インスタンス上でのインタラクションは、発行環境にユーザ生成コンテンツ(UGC)を入力します。

これまでは、このコミュニティコンテンツはオーサーインスタンスにリバースレプリケートされ、オーサーインスタンスからパブリッシュインスタンスにレプリケートされていました。逆複製と転送複製のAEMインスタンス間で一貫性を維持するのに問題がありました。

AEM Communities 6.1 以降では、前述のように、UGC 用の共有ストレージを使用することで UGC のレプリケーションが不要になりました。

サイトコンテンツはレプリケートされますが、UGC はレプリケートされません。

### ユーザーデータの管理 {#managing-user-data}

Also of interest to CommunitIes are [*users*, *user groups*, and *user profiles*](/help/communities/users.md). This user-related data, when created and updated in the publish environment, needs to be made available to other publish instances when the topology is a [publish farm](/help/sites-deploying/recommended-deploys.md#tarmk-farm).

AEM Communities 6.1 以降、ユーザー関連データは、レプリケーションではなく Sling ディストリビューションを使用して同期されます。For more information visit [User Synchronization](/help/communities/sync.md).

### AEM Communities 6.5 へのアップグレード {#upgrading-to-aem-communities}

AEM 6.5 Communitiesにアップグレードする場合、既存のUGCを保持する必要がある場合は、AEM 5.6.1またはAEM 6.0コミュニティでAdobeのオンデマンドストレージまたはオンプレミスストレージのUGCを使用したかに応じて、手順を実行する必要があります。

詳しくは、[AEM Communities 6.5 へのアップグレード](/help/communities/upgrade.md)を参照してください。
