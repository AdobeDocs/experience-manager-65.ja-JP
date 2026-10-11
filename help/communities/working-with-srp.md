---
title: SRP - コミュニティコンテンツストレージ
description: AEM Communities 6.1では、ユーザー生成コンテンツ（UGC）は、ストレージリソースプロバイダー（SRP）が提供する1つの共通ストアに保存されます
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: e29aae44-67be-43d2-8004-c986412d9e63
solution: Experience Manager
feature: Communities
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
source-wordcount: '912'
ht-degree: 5%
---
# SRP - コミュニティコンテンツストレージ {#srp-community-content-storage}

## はじめに {#introduction}

AEM Communities 6.1では、UGCは、ストレージリソースプロバイダー（SRP）が提供する1つの共通ストアに保存されます。 ASRP、MSRP、JSRPなど、複数のSRP オプションを選択できます。

以前のリリースとは異なり、AEM インスタンス間でUGCのリバースレプリケーションやフォワードレプリケーションは行われません。 代わりに、SRPは、JSRPを除いて、すべてのオーサーインスタンスとパブリッシュインスタンスの作成、読み取り、更新、削除（CRUD）操作でUGCに直接アクセスできるようにします。

以下に、各SRP オプション ](#characteristics-of-srp-options)の[特性を示します。これは、適切なSRPと[基礎となるデプロイメント ](/help/communities/topologies.md)を選択する際の決定プロセスに関する重要な情報です。

UGCでのSRPの使用について詳しくは、[ ストレージリソースプロバイダーの概要](/help/communities/srp.md)を参照してください。

>[!NOTE]
>
>SRPはコミュニティコンテンツにのみ適用されます。 サイトコンテンツの保存場所（[node store](/help/sites-deploying/data-store-config.md)）には影響せず、AEM インスタンス間のユーザー登録、ユーザープロファイル、ユーザーグループの安全な取り扱いにも影響しません（[ ユーザーデータの管理](#managing-user-data)も参照）。

>[!CAUTION]
>
>AEM 6.1以降、[UGCはレプリケートされません](#ugc-never-replicated)。
>
>デプロイメントに、デフォルトの[JSRP](/help/communities/topologies.md#jsrp) トポロジなどの共通ストアが含まれていない場合、UGCは、そのトポロジが入力されたAEM パブリッシュインスタンスまたはオーサーインスタンスでのみ表示されます。 トポロジにパブリッシュクラスターが含まれている場合にのみ、UGCは任意のパブリッシュインスタンスに表示されます。

## SRP オプションの特徴 {#characteristics-of-srp-options}

[ASRP - Adobe ストレージリソースプロバイダー](/help/communities/asrp.md)

このオプションを使用すると、UGCは、Adobeでホストおよび管理されるクラウドサービスにリモートで保持されます。 追加のライセンスが必要で、アカウント担当者と協力して、その特定のライセンスのアカウントをプロビジョニングする必要があります。 ASRPには次が必要です。

* Adobeが提供し、サポートする関連クラウドサービスで、コミュニティコンテンツを保存します。
* 特定の地域（米国、EMEA、APAC）のデータセンターの選択。

* UGCへのあらゆるプログラムによるアクセスは、SRP APIを介しておこなわれます。

ASRPは適切です。

* TarMK パブリッシュファームの場合。
* ローカルストレージに投資する意図がない場合。

>[!NOTE]
>
>ASRPの投稿（またはコメント）に添付ファイルをアップロードするには、50 MBという制限があります。

[MSRP - MongoDB ストレージリソースプロバイダー](/help/communities/msrp.md)

このオプションを使用すると、UGCはローカルのMongoDB インスタンスに直接保持されます。

MSRPには次が必要です。

* コミュニティ コンテンツを保存するためのMongoDBのローカルのライセンス取得済みインストール。
* Apache Solrのローカルインストール。
* UGCへのあらゆるプログラムによるアクセスは、SRP APIを介しておこなわれます。

ASRPは適切です。

* 既存のTarMK パブリッシュファームの。
* MongoMKまたはRdbMK クラスターの場合。
* 非常に多くの時間を費やすことになると思います。

[DSRP - リレーショナルデータベースストレージリソースプロバイダー](/help/communities/dsrp.md)

このオプションを使用すると、UGCはローカルのMySQL データベースインスタンスに直接保持されます。

DSRPには次が必要です。

* コミュニティコンテンツを保存するためのMySQLのローカルインストール。
* Apache Solrのローカルインストール。
* UGCへのあらゆるプログラムによるアクセスは、SRP APIを介しておこなわれます。

DSRPは適切です。

* 既存のTarMK パブリッシュファームの。
* MongoMKまたはRdbMK クラスターの場合。
* 非常に多くの時間を費やすことになると思います。

[JSRP - JCR ストレージリソースプロバイダー](/help/communities/jsrp.md)

デフォルトのオプションでは、共通ストアはありません。 UGCは、入力されたAEM インスタンスと同じJCR リポジトリ内でのみ保持されます。

JSRP:

* AEM オーサーインスタンスまたはパブリッシュインスタンスのJCR リポジトリにコミュニティコンテンツを保存します。
* UGCへのすべてのプログラムによるアクセスは、SRP APIを介して行う必要があります。
* 複数のパブリッシュインスタンスがデプロイされている場合は、パブリッシュクラスターが必要です（TarMK ファーム内のパブリッシュインスタンス間にレプリケーションメカニズムはありません）。
* モデレーションはパブリッシュ環境でのみ実行されます（オーサーとパブリッシュの間には逆方向/順方向のレプリケーションメカニズムはありません）。
* 開発、デモ、トレーニングに最適です。

## SRPの設定 {#configuring-srp}

デフォルトストレージオプションの指定は、基礎となるデプロイメントに基づいて、[ ストレージ設定コンソール ](/help/communities/srp-config.md)を通じて行われます。

各オプションの設定の詳細については、次を参照してください。

* [ASRP - Adobe ストレージリソースプロバイダー](/help/communities/asrp.md)
* [MSRP - MongoDB ストレージリソースプロバイダー](/help/communities/msrp.md)
* [DSRP - リレーショナルデータベースストレージリソースプロバイダー](/help/communities/dsrp.md)
* [JSRP - JCR ストレージリソースプロバイダー](/help/communities/jsrp.md)

ストレージオプションがアクティブに選択されていない場合、JSRPはデフォルトで有効になっています。

## 追加情報 {#additional-information}

### UGCがレプリケートされない {#ugc-never-replicated}

オーサー環境では、オーサーはページコンテンツを作成し、パブリッシュ環境にレプリケートします。 ページにコメント、レビュー、フォーラム、ブログ、QnAなどのインタラクティブなAEM Communities機能が含まれている場合、パブリッシュインスタンス上のメンバー（サイト訪問者にログイン）によるインタラクションは、パブリッシュ環境に入力されたユーザー生成コンテンツ（UGC）になります。

以前は、このコミュニティコンテンツはオーサーインスタンスに、オーサーインスタンスからパブリッシュインスタンスにリバースレプリケートされていました。 リバースレプリケーションとフォワードレプリケーションを使用して、AEM インスタンス間の一貫性を維持するのが困難でした。

AEM Communities 6.1以降、UGCのレプリケーションの必要性は、前述のように、UGC用の共有ストレージを使用することで排除されました。

サイトコンテンツはレプリケートされますが、UGCはレプリケートされません。

### ユーザーデータの管理 {#managing-user-data}

CommunitIesにとっても興味深いのは、[*ユーザー*、*ユーザーグループ*、*ユーザープロファイル*](/help/communities/users.md)&#x200B;です。 このユーザー関連データは、パブリッシュ環境で作成および更新される際に、トポロジが[ パブリッシュファーム ](/help/sites-deploying/recommended-deploys.md#tarmk-farm)の場合に、他のパブリッシュインスタンスで利用できるようにする必要があります。

AEM Communities 6.1では、ユーザー関連のデータは、レプリケーションではなくSling ディストリビューションを使用して同期されます。 詳細については、[ ユーザー同期](/help/communities/sync.md)を参照してください。

### AEM Communities 6.5へのアップグレード {#upgrading-to-aem-communities}

AEM 6.5 Communitiesにアップグレードする際に、既存のUGCを保持する必要がある場合は、AEM 5.6.1またはAEM 6.0 コミュニティでAdobe オンデマンドストレージまたはUGCのオンプレミスストレージを使用しているかどうかに応じて、手順を実行する必要があります。

詳しくは、[AEM Communities 6.5](/help/communities/upgrade.md)へのアップグレードを参照してください。
