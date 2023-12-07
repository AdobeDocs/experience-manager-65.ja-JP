---
title: SRP - コミュニティコンテンツストレージ
description: AEM Communities 6.1 以降、ユーザー生成コンテンツ (UGC) は、ストレージリソースプロバイダー (SRP) が提供する単一の共通ストアに保存されます
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: e29aae44-67be-43d2-8004-c986412d9e63
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 5%

---

# SRP - コミュニティコンテンツストレージ {#srp-community-content-storage}

## はじめに {#introduction}

AEM Communities 6.1 以降では、ユーザー生成コンテンツ (UGC) は、ストレージリソースプロバイダー (SRP) が提供する単一の共通ストアに保存されます。 ASRP、MSRP、JSRP など、選択できる SRP オプションが複数あります。

以前のリリースとは異なり、AEMインスタンス間での UGC のリバース/フォワードレプリケーションはありません。 代わりに、JSRP の場合を除き、UGC に直接アクセスして、すべてのオーサーインスタンスとパブリッシュインスタンスから作成、読み取り、更新、削除 (CRUD) 操作を行うことができます。

次に、 [各 SRP オプションの特性](#characteristics-of-srp-options)：適切な SRP と [基盤となる展開](/help/communities/topologies.md).

UGC での SRP の使用について詳しくは、 [ストレージリソースプロバイダの概要](/help/communities/srp.md).

>[!NOTE]
>
>SRP はコミュニティコンテンツにのみ適用されます。 サイトコンテンツが保存される場所 ([ノードストア](/help/sites-deploying/data-store-config.md)) や、AEMインスタンス間でのユーザー登録、ユーザープロファイルおよびユーザーグループの安全な処理に影響を与えません ( [ユーザーデータの管理](#managing-user-data)) をクリックします。

>[!CAUTION]
>
>AEM 6.1 以降、 [UGC はレプリケートされません](#ugc-never-replicated).
>
>デプロイメントに共通ストア（デフォルトなど）が含まれていない場合 [JSRP](/help/communities/topologies.md#jsrp) トポロジの場合、UGC は、その UGC が入力されたAEMパブリッシュインスタンスまたはオーサーインスタンス上でのみ表示されます。 トポロジにパブリッシュクラスターが含まれている場合にのみ、UGC は任意のパブリッシュインスタンスで表示されます。

## SRP オプションの特性 {#characteristics-of-srp-options}

[ASRP - Adobe ストレージリソースプロバイダー](/help/communities/asrp.md)

このオプションを使用すると、UGC は、Adobeがホストおよび管理するクラウドサービスにリモートで保持されます。 追加のライセンスが必要です。また、アカウント担当者と協力して、その特定のライセンスのアカウントをプロビジョニングする必要があります。 ASRP には次が必要です。

* コミュニティコンテンツを保存するためにAdobeが提供およびサポートする関連クラウドサービス。
* 特定の地域（米国、EMEA、APAC）のデータセンターの選択。

* UGC に対するプログラムによるアクセスはすべて、SRP API を通じて実行できます。

ASRP が適しています。

* TarMK パブリッシュファームの場合。
* ローカル・ストレージに投資する意図がない場合。

>[!NOTE]
>
>ASRP 内の投稿（またはコメント）に添付ファイルをアップロードする場合は、制限があります (50 MB)。

[MSRP - MongoDB ストレージリソースプロバイダー](/help/communities/msrp.md)

このオプションを使用すると、UGC はローカルの MongoDB インスタンスに直接保持されます。

MSRP には以下が必要です。

* コミュニティコンテンツを保存するための MongoDB のローカルのライセンスインストール。
* Apache Solr のローカルインストール。
* UGC に対するプログラムによるアクセスはすべて、SRP API を通じて実行できます。

ASRP が適しています。

* 既存の TarMK パブリッシュファームの場合。
* MongoMK または RdbMK クラスターの場合。
* 大量のコミュニティコンテンツを期待する場合。

[DSRP - リレーショナルデータベースストレージリソースプロバイダー](/help/communities/dsrp.md)

このオプションを使用すると、UGC はローカルの MySQL データベースインスタンスに直接保持されます。

DSRP には以下が必要です。

* コミュニティコンテンツを保存するための MySQL のローカルインストール。
* Apache Solr のローカルインストール。
* UGC に対するプログラムによるアクセスはすべて、SRP API を通じて実行できます。

DSRP が適しています。

* 既存の TarMK パブリッシュファームの場合。
* MongoMK または RdbMK クラスターの場合。
* 大量のコミュニティコンテンツを期待する場合。

[JSRP - JCR ストレージリソースプロバイダー](/help/communities/jsrp.md)

デフォルトのオプションでは、共通ストアはありません。 UGC は、入力されたAEMインスタンスと同じ JCR リポジトリにのみ保持されます。

JSRP:

* コミュニティコンテンツを、投稿先のAEMオーサーインスタンスまたはパブリッシュインスタンスの JCR リポジトリに格納します。
* SRP API を介して UGC にプログラムによるすべてのアクセスを必要とします。
* 複数のパブリッシュインスタンスがデプロイされている場合は、パブリッシュクラスターが必要です（TarMK ファーム内のパブリッシュインスタンス間にレプリケーションメカニズムが存在しません）。
* モデレートは、パブリッシュ環境でのみ実行されます（オーサーとパブリッシュの間には、リバース/フォワードのレプリケーションメカニズムはありません）。
* 開発、デモ、トレーニングに最適です。

## SRP の設定 {#configuring-srp}

デフォルトのストレージオプションを指定するには、基になるデプロイメントに基づいて、 [ストレージ設定コンソール](/help/communities/srp-config.md).

各オプションの設定について詳しくは、次を参照してください。

* [ASRP - Adobe ストレージリソースプロバイダー](/help/communities/asrp.md)
* [MSRP - MongoDB ストレージリソースプロバイダー](/help/communities/msrp.md)
* [DSRP - リレーショナルデータベースストレージリソースプロバイダー](/help/communities/dsrp.md)
* [JSRP - JCR ストレージリソースプロバイダー](/help/communities/jsrp.md)

ストレージオプションがアクティブに選択されていない場合、JSRP はデフォルトで有効になっています。

## 追加情報 {#additional-information}

### UGC がレプリケートされていません {#ugc-never-replicated}

オーサー環境では、オーサーがページコンテンツを作成し、パブリッシュ環境にレプリケートします。 ページにコメント、レビュー、フォーラム、ブログ、Q&amp;A などのインタラクティブなAEM Communities機能が含まれる場合、パブリッシュインスタンス上でのメンバー（サインインしたサイト訪問者）のインタラクションにより、パブリッシュ環境にユーザー生成コンテンツ (UGC) が入力されます。

以前は、このコミュニティコンテンツは、オーサーインスタンスにリバースレプリケートされ、オーサーインスタンスからパブリッシュインスタンスにレプリケートされていました。 リバースレプリケーションとフォワードレプリケーションを使用して、AEMインスタンス間の一貫性を維持することに問題が発生していました。

AEM Communities 6.1 以降、前述のように、UGC 用の共有ストレージを使用することで、UGC のレプリケーションの必要性がなくなりました。

サイトコンテンツはレプリケートされますが、UGC はレプリケートされません。

### ユーザーデータの管理 {#managing-user-data}

CommunitIes に対する関心も [*ユーザー*, *ユーザーグループ*、および *ユーザープロファイル*](/help/communities/users.md). このユーザー関連データは、パブリッシュ環境で作成および更新されたときに、トポロジが [パブリッシュファーム](/help/sites-deploying/recommended-deploys.md#tarmk-farm).

AEM Communities 6.1 以降では、ユーザー関連のデータは、レプリケーションではなく Sling 配布を使用して同期されます。 詳しくは、 [ユーザーの同期](/help/communities/sync.md).

### AEM Communities 6.5 へのアップグレード {#upgrading-to-aem-communities}

AEM 6.5 Communities にアップグレードする際に、既存の UGC を保持する必要がある場合は、AEM 5.6.1 またはAEM 6.0 コミュニティでAdobeのオンデマンドストレージを使用したか、オンプレミスストレージを使用したかに応じて、手順を実行する必要があります。

詳しくは、 [AEM Communities 6.5 へのアップグレード](/help/communities/upgrade.md).
