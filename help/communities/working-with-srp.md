---
title: SRP - コミュニティコンテンツストレージ
description: AEM Communities 6.1 以降、ユーザー生成コンテンツ（UGC）は、ストレージリソースプロバイダー（SRP）が提供する 1 つの共通ストアに保存されます
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: e29aae44-67be-43d2-8004-c986412d9e63
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 5%

---

# SRP - コミュニティコンテンツストレージ {#srp-community-content-storage}

## はじめに {#introduction}

AEM Communities 6.1 以降、ユーザー作成コンテンツ（UGC）は、ストレージリソースプロバイダー（SRP）が提供する 1 つの共通ストアに保存されます。 ASRP、MSRP、JSRP など、いくつかの SRP オプションから選択できます。

以前のリリースとは異なり、AEM インスタンス間で UGC のリバースレプリケーション/フォワードレプリケーションを行うことはできません。 代わりに、SRP により、JSRP を除くすべてのオーサーインスタンスとパブリッシュインスタンスから、作成、読み取り、更新、削除（CRUD）操作のために UGC に直接アクセスできるようになります。

以下は以下のとおりです [各 SRP オプションの特性](#characteristics-of-srp-options)。これは、適切な SRP を選択する際の決定プロセスにとって重要な情報です。 [基盤となるデプロイメント](/help/communities/topologies.md).

UGC への SRP の使用について詳しくは、 [ストレージリソースプロバイダーの概要](/help/communities/srp.md).

>[!NOTE]
>
>SRP は、コミュニティコンテンツにのみ適用されます。 サイトコンテンツの保存場所（[ノードストア](/help/sites-deploying/data-store-config.md)）に設定し、AEM インスタンス間でのユーザー登録、ユーザープロファイルおよびユーザーグループの安全な処理に影響を与えません [ユーザーデータの管理](#managing-user-data)）に設定します。

>[!CAUTION]
>
>AEM 6.1 以降、 [UGC はレプリケートされない](#ugc-never-replicated).
>
>デプロイメントに共通ストアが含まれていない場合（デフォルトなど） [JSRP](/help/communities/topologies.md#jsrp) トポロジ、UGC は、入力されたAEM パブリッシュインスタンスまたはオーサーインスタンスでのみ表示されます。 トポロジにパブリッシュクラスターが含まれている場合にのみ、UGC はどのパブリッシュインスタンスにも表示されます。

## SRP オプションの特徴 {#characteristics-of-srp-options}

[ASRP - Adobe ストレージリソースプロバイダー](/help/communities/asrp.md)

このオプションを使用すると、UGC は、Adobeがホストおよび管理するクラウドサービスにリモートで保持されます。 追加のライセンスが必要で、特定のライセンスのアカウントをプロビジョニングするにはアカウント担当者と協力する必要があります。 ASRP には次が必要です。

* コミュニティコンテンツを格納するためにAdobeが提供およびサポートする、関連するクラウドサービス。
* 特定の地域（米国、EMEA、APAC）におけるデータセンターの選択。

* UGC へのプログラムによるアクセスはすべて、SRP API を介して行われます。

ASRP は次の場合に適しています。

* TarMK パブリッシュファームの場合。
* ローカルストレージに投資する意図がない場合。

>[!NOTE]
>
>ASRP では、投稿（コメント）への添付ファイルのアップロードに制限があります（50 MB）。

[MSRP - MongoDB ストレージリソースプロバイダー](/help/communities/msrp.md)

このオプションを使用すると、UGC はローカルの MongoDB インスタンスに直接保持されます。

MSRP には次が必要です。

* コミュニティコンテンツを保存するための、MongoDB のローカルのライセンスインストール。
* Apache Solr のローカルインストール。
* UGC へのプログラムによるアクセスはすべて、SRP API を介して行われます。

ASRP は次の場合に適しています。

* 既存の TarMK パブリッシュファームの場合。
* MongoMK または RdbMK クラスターの場合。
* 大量のコミュニティコンテンツを期待する場合。

[DSRP - リレーショナルデータベースストレージリソースプロバイダー](/help/communities/dsrp.md)

このオプションを使用すると、UGC はローカルの MySQL データベースインスタンスに直接保持されます。

DSRP には次が必要です。

* コミュニティコンテンツを保存するための MySQL のローカルインストール。
* Apache Solr のローカルインストール。
* UGC へのプログラムによるアクセスはすべて、SRP API を介して行われます。

DSRP は以下の場合に適しています。

* 既存の TarMK パブリッシュファームの場合。
* MongoMK または RdbMK クラスターの場合。
* 大量のコミュニティコンテンツを期待する場合。

[JSRP - JCR ストレージリソースプロバイダー](/help/communities/jsrp.md)

デフォルトのオプションでは、共通のストアはありません。 UGC は、入力されたAEM インスタンスと同じ JCR リポジトリにのみ保持されます。

JSRP:

* コミュニティコンテンツを、投稿先のAEM オーサーインスタンスまたはパブリッシュインスタンスの JCR リポジトリに格納します。
* SRP API を使用して、UGC に対するすべてのプログラムによるアクセスが必要です。
* 複数のパブリッシュインスタンスがデプロイされている（TarMK ファーム内のパブリッシュインスタンス間にレプリケーションメカニズムがない）場合は、パブリッシュクラスターが必要です。
* モデレートは、パブリッシュ環境でのみ実行されます（オーサーとパブリッシュの間にリバース/フォワードレプリケーションメカニズムはありません）。
* 開発、デモンストレーション、トレーニングに最適です。

## SRP の設定 {#configuring-srp}

基になるデプロイメントに基づいて、デフォルトのストレージオプションを指定するには、を使用します。 [ストレージ設定コンソール](/help/communities/srp-config.md).

各オプションの設定について詳しくは、以下を参照してください。

* [ASRP - Adobe ストレージリソースプロバイダー](/help/communities/asrp.md)
* [MSRP - MongoDB ストレージリソースプロバイダー](/help/communities/msrp.md)
* [DSRP - リレーショナルデータベースストレージリソースプロバイダー](/help/communities/dsrp.md)
* [JSRP - JCR ストレージリソースプロバイダー](/help/communities/jsrp.md)

ストレージオプションがアクティブに選択されていない場合、JSRP はデフォルトで有効になっています。

## 追加情報 {#additional-information}

### UGC はレプリケートされない {#ugc-never-replicated}

オーサー環境では、作成者がページコンテンツを作成し、それをパブリッシュ環境にレプリケートします。 ページにコメント、レビュー、フォーラム、ブログ、QnA などのインタラクティブなAEM Communities機能が含まれる場合、公開インスタンスでのメンバー（ログインしたサイトの訪問者）によるインタラクションの結果、公開環境に入力されたユーザー生成コンテンツ（UGC）が生成されます。

以前は、このコミュニティコンテンツはオーサーインスタンスにリバースレプリケーションされ、オーサーインスタンスからパブリッシュインスタンスにレプリケートされていました。 リバースレプリケーションとフォワードレプリケーションでAEM インスタンス間の一貫性を維持することが問題でした。

AEM Communities 6.1 以降、上述のように、UGC の共有ストレージを使用することで、UGC のレプリケーションの必要性がなくなりました。

サイトコンテンツがレプリケートされている間、UGC はレプリケートされません。

### ユーザーデータの管理 {#managing-user-data}

CommunitIes にとっても次のような利点があります [*ユーザー*, *ユーザーグループ*、および *ユーザープロファイル*](/help/communities/users.md). ユーザー関連のデータは、パブリッシュ環境で作成および更新されたときに、トポロジがの場合に他のパブリッシュインスタンスで使用できるようにする必要があります [パブリッシュファーム](/help/sites-deploying/recommended-deploys.md#tarmk-farm).

AEM Communities 6.1 では、ユーザー関連のデータはレプリケーションの代わりに Sling 配布を使用して同期されます。 詳しくは、を参照してください。 [ユーザーの同期](/help/communities/sync.md).

### AEM Communities 6.5 へのアップグレード {#upgrading-to-aem-communities}

AEM 6.5 Communities にアップグレードする際に、既存の UGC を保持する必要がある場合は、AEM 5.6.1 またはAEM 6.0 コミュニティでAdobeのオンデマンドストレージまたは UGC のオンプレミスストレージのどちらが使用されているかに応じて、手順を実行する必要があります。

詳しくは、次を参照してください： [AEM Communities 6.5 へのアップグレード](/help/communities/upgrade.md).
