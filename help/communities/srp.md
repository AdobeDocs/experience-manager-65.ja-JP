---
title: ストレージリソースプロバイダーの概要
seo-title: Storage Resource Provider Overview
description: Communities 用の共通ストレージ
seo-description: Common storage for Communities
uuid: abdf4e5a-767b-428f-9aa4-0dc06819a26e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 63abeda4-6ea1-4b45-b188-f9c6b44ca0cd
exl-id: 5f313274-1a2a-4e83-9289-60a4729b99b4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1133'
ht-degree: 62%

---

# ストレージリソースプロバイダーの概要 {#storage-resource-provider-overview}

## はじめに {#introduction}

AEM Communities 6.1 以降、コミュニティコンテンツ（一般的にユーザー生成コンテンツ（UGC）と呼ばれる）は、[ストレージリソースプロバイダー](working-with-srp.md)（SRP）によって提供される単一の共通ストアに格納されます。

複数の SRP オプションがあり、それらはすべて、作成、読み取り、更新および削除（CRUD）操作がすべて含まれた、新しい AEM Communities インターフェイスである [SocialResourceProvider API](srp-and-ugc.md)（SRP API）によって UGC にアクセスします。

すべての SCF コンポーネントは SRP API を使用して実装されるので、[基になるトポロジ](topologies.md)または UGC の場所を知らなくてもコードを開発できます。

***SocialResourceProvider API は、AEM Communities の使用許諾を得たお客様のみが使用できます。***

>[!NOTE]
>
>**カスタムコンポーネント**：AEM Communities の使用許諾を得たお客様の場合、SRP API は、カスタムコンポーネントの開発者が、基になるトポロジに関係なく UGC にアクセスするために使用できます。詳しくは、 [SRP と UGC の基本事項](srp-and-ugc.md).

関連トピック：

* [SRP と UGC の基本事項](srp-and-ugc.md) - SRP ユーティリティメソッドと例。
* [SRP を使用した UGC へのアクセス](accessing-ugc-with-srp.md)  — コーディングのガイドライン。
* [SocialUtils リファクタリング](socialutils.md)  — 非推奨のユーティリティメソッドを現在の SRP ユーティリティメソッドにマッピングします。

## リポジトリについて {#about-the-repository}

SRP を理解するには、AEM コミュニティサイトにおける AEM リポジトリ（OAK）の役割を理解することが必要です。

**Java Content Repository（JCR）** この規格では、コンテンツリポジトリのデータモデルおよびアプリケーションプログラミングインターフェイス（[JCR API](https://jackrabbit.apache.org/jcr/jcr-api.html)）が定義されます。従来のファイル・システムの特性とリレーショナル・データベースの特性を組み合わせ、コンテンツ・アプリケーションが頻繁に必要とする機能を多数追加します。

JCR の 1 つの実装が AEM リポジトリである OAK です。

**Apache Jackrabbit Oak（OAK）**[ OAK](../../help/sites-deploying/platform.md) は、コンテンツ中心のアプリケーション向けに特別に設計されたデータストレージシステムである JCR 2.0 の実装です。これは、非構造化データと半構造化データ用に設計された階層データベースの一種です。 このリポジトリには、ユーザーに表示されるコンテンツだけでなく、アプリケーションで使用されるすべてのコード、テンプレートおよび内部データが格納されます。コンテンツにアクセスするための UI は次のとおりです。 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md).

JCR と OAK はどちらも、通常は AEM リポジトリを示すために使用されます。

非公開のオーサー環境でサイトコンテンツを開発した後、それを公開のパブリッシュ環境にコピーする必要があります。これは、多くの場合、 *[複製](deploy-communities.md#replication-agents-on-author)*. これは、作成者、開発者、管理者の管理下で発生します。

UGC の場合、コンテンツは公開のパブリッシュ環境で登録済みサイト訪問者（コミュニティメンバー）によって生成されます。これはランダムに発生します。

管理およびレポートの目的では、非公開のオーサー環境から UGC にアクセスすることが有用です。SRP では、パブリッシュからオーサーへのリバースレプリケーションは不要なので、オーサーから UGC にアクセスする方が一貫性が高く、パフォーマンスも向上します。

## SRP について {#about-srp}

UGC が共有ストレージに格納される場合、ほとんどのデプロイメントでオーサー環境とパブリッシュ環境の両方からアクセスできるメンバーコンテンツの単一インスタンスがあります。SRP の選択 (MSRP、ASRP、JSRP) に関係なく、すべての SRP API を使用してプログラムからアクセスする必要があります。

>[!NOTE]
>
>詳しくは、 [SRP と UGC の基本事項](srp-and-ugc.md) を参照してください。
>
>コーディング時のベストプラクティスについては、[SRP による UGC へのアクセス](accessing-ugc-with-srp.md)を参照してください。

### ASRP {#asrp}

ASRP の場合、UGC は JCR には格納されず、Adobe がホストおよび管理するクラウドサービスに格納されます。ASRP に保存された UGC は、CRXDE Liteで表示したり、JCR API を使用してアクセスしたりすることはできません。

[ASRP - Adobe ストレージリソースプロバイダー](asrp.md)を参照してください。

開発者が UGC に直接アクセスすることはできません。

ASRP では検索に Adobe クラウドが使用されます。

### MSRP {#msrp}

MSRP の場合、UGC は JCR には格納されず、MongoDB に格納されます。MSRP に格納された UGC は、CRXDE Liteで表示したり、JCR API を使用してアクセスしたりすることはできません。

[MSRP - MongoDB ストレージリソースプロバイダー](msrp.md)を参照してください。

MSRP は ASRP と互換性がありますが、すべての AEM サーバーインスタンスは同じ UGC にアクセスするので、共通のツールを使用して MongoDB に格納された UGC に直接アクセスできます。

MSRP では検索に Solr が使用されます。

### JSRP {#jsrp}

JSRP は、単一 AEM インスタンス上のすべての UGC にアクセスするためのデフォルトのプロバイダーです。MSRP や ASRP を設定しなくても、AEM Communities 6.1 をすばやく体験できます。

詳しくは、 [JSRP - JCR ストレージリソースプロバイダー](jsrp.md).

JSRP の場合、UGC は JCR に格納され、CRXDE Lite と JCR API の両方でアクセスできますが、JCR API は使用しないことを強くお勧めします。使用すると、今後の変更によってカスタムコードが影響を受ける可能性があります。

さらに、オーサー環境とパブリッシュ環境のリポジトリは共有されません。パブリッシュインスタンスのクラスターが共有パブリッシュリポジトリになりますが、パブリッシュ時に入力された UGC はオーサーに表示されないので、オーサーから UGC を管理することはできません。 UGC は、入力されたインスタンスのAEMリポジトリ (JCR) にのみ保持されます。

JSRP は、クエリに Oak インデックスを使用します。

## JCR でのシャドウノードについて {#about-shadow-nodes-in-jcr}

UGC へのパスを模倣するシャドウノードは、以下の 2 つの目的のためにローカルリポジトリに存在します。

1. [アクセス制御 (ACL)](#for-access-control-acls)
1. [存在しないリソース（NER）](#for-non-existing-resources-ners)

SRP の実装に関係なく、実際の UGC はシャドウノードと同じ場所に表示されません。

### アクセス制御（ACL）のため {#for-access-control-acls}

一部の SRP 実装（ASRP や MSRP など）では、コミュニティコンテンツは ACL 検証が提供されないデータベースに格納されます。シャドウノードは、ACL を適用できるローカルリポジトリ内の場所を提供します。

SRP API を使用すると、すべての SRP オプションによって、すべての CRUD 操作の前にシャドウの場所の同じチェックが実行されます。

ACL チェックでは、リソースの UGC に適用される権限のチェックに適したパスを返すユーティリティメソッドが使用されます。

詳しくは、 [SRP と UGC の基本事項](srp-and-ugc.md) を参照してください。

### 存在しないリソース（NER）のため {#for-non-existing-resources-ners}

一部のコミュニティコンポーネントはスクリプトに含めることができ、したがってコミュニティ機能をサポートするために Sling アドレス可能ノードが必要です。[含まれるコンポーネント](scf.md#add-or-include-a-communities-component) は、存在しないリソース (NER) と呼ばれます。

シャドウノードによって、リポジトリ内の Sling アドレス可能な場所が提供されます。

>[!CAUTION]
>
>シャドウノードには複数の用途があるので、シャドウノードの存在はコンポーネントが NER であることを意味しません。**

### 格納場所 {#storage-location}

次に、 [コメントコンポーネント](http://localhost:4502/content/community-components/en/comments.html) 内 [コミュニティコンポーネントガイド](components-guide.md):

* コンポーネントは次の場所にあるローカルリポジトリに存在します。

   `/content/community-components/en/comments/jcr:content/content/includable/comments`

* 対応するシャドウノードが、次の場所にあるローカルリポジトリに存在します。

   `/content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments`

シャドウノードの下には UGC はありません。

デフォルトの動作では、関連するサブツリーが読み取りまたは書き込み用に参照されるたびに、パブリッシュインスタンス上にシャドウノードを設定します。

例えば、デプロイメントが [MSRP](msrp.md) TarMK パブリッシュファームを使用します。

When a [メンバー](users.md) pub1（MongoDB に格納）に UGC を投稿し、pub1 の JCR にシャドウノードを作成します。

UGC が pub2 で初めて読み取られる場合、何も設定されていないと、デフォルトの動作ではシャドウノードが作成されます。

デフォルト以外の動作が必要な場合は、それをオーサーインスタンスで設定し、すべてのパブリッシュインスタンスにロールフォワードする必要があります。これは通常は手動プロセスです。
