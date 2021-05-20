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
role: Administrator
exl-id: e29aae44-67be-43d2-8004-c986412d9e63
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '921'
ht-degree: 31%

---

# SRP - コミュニティコンテンツストレージ  {#srp-community-content-storage}

## はじめに {#introduction}

AEM Communities 6.1以降、ユーザー生成コンテンツ(UGC)は、ストレージリソースプロバイダー(SRP)が提供する単一の共通ストアに保存されます。 ASRP、MSRP、JSRPなど、選択できるSRPオプションがいくつかあります。

以前のリリースとは異なり、AEM インスタンス間の UGC のリバース／フォワードレプリケーションはありません。代わりに、JSRPを除き、UGCに直接アクセスして、すべてのオーサーインスタンスとパブリッシュインスタンスから作成、読み取り、更新、削除(CRUD)操作を実行できます。

各SRPオプション](#characteristics-of-srp-options)の[特性を以下に示します。これは、適切なSRPおよび[基盤となるデプロイメント](/help/communities/topologies.md)を選択する際の判定プロセスにとって重要な情報です。

UGCでのSRPの使用に関する詳細は、「[ストレージリソースプロバイダーの概要](/help/communities/srp.md)」を参照してください。

>[!NOTE]
>
>SRP はコミュニティコンテンツにのみ適用されます。サイトコンテンツの格納先([node store](/help/sites-deploying/data-store-config.md))には影響せず、AEMインスタンス間のユーザー登録、ユーザープロファイル、ユーザーグループの安全な処理には影響しません（[ユーザーデータの管理](#managing-user-data)も参照）。

>[!CAUTION]
>
>AEM 6.1以降では、[UGCはレプリケートされません。](#ugc-never-replicated)
>
>デプロイメントに共通ストアが含まれていない場合（デフォルトの [JSRP](/help/communities/topologies.md#jsrp) トポロジなど）、UGC は、それが入力された AEM パブリッシュインスタンスまたはオーサーインスタンスでのみ表示可能になります。トポロジにパブリッシュクラスターが含まれる場合にのみ、UGCは任意のパブリッシュインスタンスで表示されます。

## SRP オプションの特性 {#characteristics-of-srp-options}

[ASRP - Adobe ストレージリソースプロバイダー](/help/communities/asrp.md)

このオプションを使用すると、UGCは、Adobeがホストおよび管理するクラウドサービスでリモートで保持されます。 追加のライセンスが必要です。また、アカウント担当者と協力して、その特定のライセンスのアカウントをプロビジョニングする必要があります。 ASRPには次が必要です。

* コミュニティコンテンツを保存するためにAdobeが提供およびサポートする関連クラウドサービス。
* 特定の地域（米国、EMEA、APAC）のデータセンターの選択

* UGCへのプログラムによるアクセスはすべて、SRP APIを通じて行います。

ASRPが適しています。

* TarMKパブリッシュファームの場合。
* ローカル・ストレージに投資する意図がない場合。

>[!NOTE]
>
>ASRPでの投稿（またはコメント）への添付ファイルのアップロードには、制限があります(50 MB)。

[MSRP - MongoDB ストレージリソースプロバイダー](/help/communities/msrp.md)

このオプションを使用すると、UGCはローカルのMongoDBインスタンスに直接保持されます。

MSRPには以下が必要です。

* コミュニティコンテンツを保存するための、MongoDBのローカルのライセンスインストール。
* Apache Solrのローカルインストール。
* UGCへのプログラムによるアクセスはすべて、SRP APIを通じて行います。

ASRPが適しています。

* 既存のTarMKパブリッシュファームの場合。
* MongoMKまたはRdbMKクラスターの場合。
* 大量のコミュニティコンテンツが必要な場合。

[DSRP - リレーショナルデータベースストレージリソースプロバイダー](/help/communities/dsrp.md)

このオプションを使用すると、UGCはローカルのMySQLデータベースインスタンスに直接保持されます。

DSRPには以下が必要です。

* コミュニティコンテンツを保存するためのMySQLのローカルインストール。
* Apache Solrのローカルインストール。
* UGCへのプログラムによるアクセスはすべて、SRP APIを通じて行います。

DSRPが適しています。

* 既存のTarMKパブリッシュファームの場合。
* MongoMKまたはRdbMKクラスターの場合。
* 大量のコミュニティコンテンツが必要な場合。

[JSRP - JCR ストレージリソースプロバイダー](/help/communities/jsrp.md)

デフォルトのオプションでは、共通ストアはありません。 UGCは、入力されたAEMインスタンスと同じJCRリポジトリにのみ保持されます。

JSRP:

* コミュニティコンテンツを、投稿先のAEMオーサーインスタンスまたはパブリッシュインスタンスのJCRリポジトリに格納します。
* SRP APIを介してUGCにプログラム的にアクセスする必要があります。
* 複数のパブリッシュインスタンスがデプロイされている場合は、パブリッシュクラスターが必要です（TarMKファーム内のパブリッシュインスタンス間にレプリケーションメカニズムはありません）。
* モデレートは、パブリッシュ環境でのみ実行されます（オーサー環境とパブリッシュ環境の間には、リバース/フォワードレプリケーションメカニズムはありません）。
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

作成者はオーサー環境でページコンテンツを作成し、パブリッシュ環境にレプリケートします。ページにコメント、レビュー、フォーラム、ブログ、Q&amp;AなどのインタラクティブなAEM Communities機能が含まれる場合、パブリッシュインスタンス上でのメンバー（サインインサイト訪問者）のインタラクションにより、パブリッシュ環境にユーザー生成コンテンツ(UGC)が入力されます。

これまでは、このコミュニティコンテンツはオーサーインスタンスにリバースレプリケートされ、オーサーインスタンスからパブリッシュインスタンスにレプリケートされていました。リバースおよびフォワードレプリケーションを使用してAEMインスタンス間の一貫性を維持することは問題でした。

AEM Communities 6.1 以降では、前述のように、UGC 用の共有ストレージを使用することで UGC のレプリケーションが不要になりました。

サイトコンテンツはレプリケートされますが、UGC はレプリケートされません。

### ユーザーデータの管理  {#managing-user-data}

また、CommunitIesには、[*ユーザー*、*ユーザーグループ*、*ユーザープロファイル*](/help/communities/users.md)&#x200B;が関心を持ちます。 このユーザー関連データは、パブリッシュ環境で作成および更新する際に、トポロジが[パブリッシュファーム](/help/sites-deploying/recommended-deploys.md#tarmk-farm)の場合に、他のパブリッシュインスタンスで使用可能にする必要があります。

AEM Communities 6.1 以降、ユーザー関連データは、レプリケーションではなく Sling ディストリビューションを使用して同期されます。詳しくは、[ユーザーの同期](/help/communities/sync.md)を参照してください。

### AEM Communities 6.5 へのアップグレード {#upgrading-to-aem-communities}

AEM 6.5 Communitiesにアップグレードする際に、既存のUGCを保持する必要がある場合は、AEM 5.6.1またはAEM 6.0コミュニティでAdobeオンデマンドストレージを使用したか、UGCのオンプレミスストレージを使用したかに応じて、手順を実行する必要があります。

詳しくは、[AEM Communities 6.5 へのアップグレード](/help/communities/upgrade.md)を参照してください。
