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
source-git-commit: 70e6f2d8366456e5091b7b775dc40914948921ab

---


# SRP - コミュニティコンテンツストレージ{#srp-community-content-storage}

## 概要 {#introduction}

AEM Communities 6.1以降、ユーザー生成コンテンツ(UGC)は、ストレージリソースプロバイダー(SRP)が提供する単一の共通ストアに保存されます。 ASRP、MSRP、JSRPなど、選択できるSRPオプションがいくつかあります。

以前のリリースとは異なり、AEM インスタンス間の UGC のリバース／フォワードレプリケーションはありません。代わりに、JSRPを除き、UGCは、すべての作成者インスタンスとパブリッシュインスタンスから、作成、読み取り、更新、削除(CRUD)操作に直接アクセスできるようになります。

Following are the [characteristics of each SRP option](#characteristics-of-srp-options), which is crucial information for the decision process when choosing the appropriate SRP and [underlying deployment](/help/communities/topologies.md).

For details regarding the use of SRP for UGC, see [Storage Resource Provider Overview](/help/communities/srp.md).

>[!NOTE]
>
>SRP はコミュニティコンテンツにのみ適用されます。It does not affect where site content is stored ([node store](/help/sites-deploying/data-store-config.md)), and does not affect the secure handling of user registration, user profiles and user groups between AEM instances (see also [Managing User Data](#managing-user-data)).

>[!CAUTION]
>
>As of AEM 6.1, [UGC is never replicated](#ugc-never-replicated).
>
>デプロイメントに共通ストアが含まれていない場合（デフォルトの [JSRP](/help/communities/topologies.md#jsrp) トポロジなど）、UGC は、それが入力された AEM パブリッシュインスタンスまたはオーサーインスタンスでのみ表示可能になります。トポロジにパブリッシュクラスターが含まれる場合にのみ、UGCはパブリッシュインスタンスで表示されます。

## SRP オプションの特性 {#characteristics-of-srp-options}

[ASRP - Adobe ストレージリソースプロバイダー](/help/communities/asrp.md)このオプションを使用すると、UGC は、アドビがホストおよび管理するクラウドサービスで、リモートで保持されます。その場合は、追加のライセンスを取得し、アカウント担当者と協力して、その特定のライセンスのアカウントをプロビジョニングする必要があります。 ASRPには次のものが必要です。

* コミュニティコンテンツを保存するためにアドビが提供およびサポートする関連クラウドサービス。
* 特定の地域（米国、EMEA、APAC）のデータセンターを選択。

* UGCへのプログラムによるアクセスはすべてSRP APIを通じて行われます。

ASRPが適しています。

* TarMK発行ファーム用。
* ローカル・ストレージに投資する意図がない場合。

>[!NOTE]
>
>ASRPでの投稿（またはコメント）に添付ファイルをアップロードする場合、制限は50 MBです。

[MSRP - MongoDB ストレージリソースプロバイダー](/help/communities/msrp.md)このオプションを使用すると、UGC はローカルの MongoDB インスタンスに直接保持されます。

MSRPには次が必要です。

* コミュニティコンテンツを保存するMongoDBのローカルインストール。
* Apache Solrのローカルインストール。
* UGCへのプログラムによるアクセスはすべてSRP APIを通じて行われます。

ASRPが適しています。

* 既存のTarMK発行ファームの場合。
* MongoMKまたはRdbMKクラスターの場合。
* 大量のコミュニティコンテンツを期待する場合。

[DSRP - リレーショナルデータベースストレージリソースプロバイダー](/help/communities/dsrp.md)このオプションを使用すると、UGC はローカルの MySQL データベースインスタンスに直接保持されます。

DSRPには次が必要です。

* コミュニティコンテンツを保存するMySQLのローカルインストール。
* Apache Solrのローカルインストール。
* UGCへのプログラムによるアクセスはすべてSRP APIを通じて行われます。

DSRPが適しています。

* 既存のTarMK発行ファームの場合。
* MongoMKまたはRdbMKクラスターの場合。
* 大量のコミュニティコンテンツを期待する場合。

[JSRP - JCR ストレージリソースプロバイダー](/help/communities/jsrp.md)このデフォルトオプションを使用する場合は、共通ストアはありません。UGCは、入力されたAEMインスタンスと同じJCRリポジトリ内でのみ保持されます。

JSRP:

* コミュニティのコンテンツを、投稿先のAEM作成者または発行インスタンスのJCRリポジトリに保存します。
* UGCへのすべてのプログラムアクセスはSRP APIを通じて行う必要があります。
* 複数の発行インスタンスがデプロイされている場合（TarMKファーム内の発行インスタンス間に複製メカニズムがない場合）、発行クラスターが必要です。
* モデレートは、発行環境でのみ実行されます（作成者と発行の間に逆複製メカニズムはありません）。
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

作成者はオーサー環境でページコンテンツを作成し、パブリッシュ環境にレプリケートします。ページにコメント、レビュー、フォーラム、ブログ、QnAなどのインタラクティブなAEM Communities機能が含まれる場合、メンバー（サインインサイト訪問者）によるパブリッシュインスタンス上でのインタラクションによって、ユーザ生成コンテンツ(UGC)がパブリッシュ環境に入ります。

これまでは、このコミュニティコンテンツはオーサーインスタンスにリバースレプリケートされ、オーサーインスタンスからパブリッシュインスタンスにレプリケートされていました。逆複製と転送複製を使用してAEMインスタンス間の一貫性を維持すると問題が発生していました。

AEM Communities 6.1 以降では、前述のように、UGC 用の共有ストレージを使用することで UGC のレプリケーションが不要になりました。

サイトコンテンツはレプリケートされますが、UGC はレプリケートされません。

### ユーザーデータの管理 {#managing-user-data}

Also of interest to CommunitIes are [*users *,* user groups *, and* user profiles *](/help/communities/users.md). This user-related data, when created and updated in the publish environment, needs to be made available to other publish instances when the topology is a[publish farm](/help/sites-deploying/recommended-deploys.md#tarmk-farm).

AEM Communities 6.1 以降、ユーザー関連データは、レプリケーションではなく Sling ディストリビューションを使用して同期されます。For more information visit [User Synchronization](/help/communities/sync.md).

### AEM Communities 6.5 へのアップグレード {#upgrading-to-aem-communities}

AEM 6.5 Communitiesにアップグレードする場合、既存のUGCを維持する必要がある場合は、AEM 5.6.1またはAEM 6.0コミュニティでアドビのオンデマンドストレージとUGCのオンプレミスストレージのどちらを使用したかに応じて、手順を実行する必要があります。

詳しくは、[AEM Communities 6.5 へのアップグレード](/help/communities/upgrade.md)を参照してください。
