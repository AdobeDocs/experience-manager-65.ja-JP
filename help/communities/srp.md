---
title: ストレージリソースプロバイダーの概要
seo-title: ストレージリソースプロバイダーの概要
description: Communities 用の共通ストレージ
seo-description: Communities 用の共通ストレージ
uuid: abdf4e5a-767b-428f-9aa4-0dc06819a26e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 63abeda4-6ea1-4b45-b188-f9c6b44ca0cd
exl-id: 5f313274-1a2a-4e83-9289-60a4729b99b4
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1141'
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
>**カスタムコンポーネント**：AEM Communities の使用許諾を得たお客様の場合、SRP API は、カスタムコンポーネントの開発者が、基になるトポロジに関係なく UGC にアクセスするために使用できます。[SRPとUGCの基本事項](srp-and-ugc.md)を参照してください。

関連トピック：

* [SRPとUGCの基本事項](srp-and-ugc.md) - SRPユーティリティのメソッドと例。
* [SRPによるUGCへのアクセス](accessing-ugc-with-srp.md)  — コーディングのガイドライン
* [SocialUtilsのリファクタリング](socialutils.md)  — 非推奨のユーティリティメソッドを現在のSRPユーティリティメソッドにマッピングします。

## リポジトリについて {#about-the-repository}

SRP を理解するには、AEM コミュニティサイトにおける AEM リポジトリ（OAK）の役割を理解することが必要です。

**Java Content Repository（JCR）** この規格では、コンテンツリポジトリのデータモデルおよびアプリケーションプログラミングインターフェイス（[JCR API](https://jackrabbit.apache.org/jcr/jcr-api.html)）が定義されます。従来のファイル・システムの特性とリレーショナル・データベースの特性を組み合わせ、コンテンツ・アプリケーションで頻繁に必要とされる多くの機能を追加します。

JCR の 1 つの実装が AEM リポジトリである OAK です。

**Apache Jackrabbit Oak（OAK）**[ OAK](../../help/sites-deploying/platform.md) は、コンテンツ中心のアプリケーション向けに特別に設計されたデータストレージシステムである JCR 2.0 の実装です。これは、非構造化データと半構造化データ用に設計された階層データベースの一種です。 このリポジトリには、ユーザーに表示されるコンテンツだけでなく、アプリケーションで使用されるすべてのコード、テンプレートおよび内部データが格納されます。コンテンツにアクセスするUIは[CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)です。

JCR と OAK はどちらも、通常は AEM リポジトリを示すために使用されます。

非公開のオーサー環境でサイトコンテンツを開発した後、それを公開のパブリッシュ環境にコピーする必要があります。これは、多くの場合、*[レプリケーション](deploy-communities.md#replication-agents-on-author)*&#x200B;と呼ばれる操作を通じて実行されます。 これは、作成者、開発者、管理者の管理下で発生します。

UGC の場合、コンテンツは公開のパブリッシュ環境で登録済みサイト訪問者（コミュニティメンバー）によって生成されます。これはランダムに発生します。

管理およびレポートの目的では、非公開のオーサー環境から UGC にアクセスすることが有用です。SRPでは、パブリッシュからオーサーへのリバースレプリケーションは不要なので、オーサーからUGCへのアクセスの一貫性とパフォーマンスが向上します。

## SRP について {#about-srp}

UGC が共有ストレージに格納される場合、ほとんどのデプロイメントでオーサー環境とパブリッシュ環境の両方からアクセスできるメンバーコンテンツの単一インスタンスがあります。SRPの選択(MSRP、ASRP、JSRP)に関係なく、すべてのSRP APIを使用してプログラムでアクセスする必要があります。

>[!NOTE]
>
>サンプルコードとその他の詳細については、[SRPとUGCの基本事項](srp-and-ugc.md)を参照してください。
>
>コーディング時のベストプラクティスについては、[SRP による UGC へのアクセス](accessing-ugc-with-srp.md)を参照してください。

### ASRP {#asrp}

ASRP の場合、UGC は JCR には格納されず、Adobe がホストおよび管理するクラウドサービスに格納されます。ASRPに格納されたUGCは、JCR APIを使用してCRXDE Liteで表示したり、アクセスしたりすることはできません。

[ASRP - Adobe ストレージリソースプロバイダー](asrp.md)を参照してください。

開発者が UGC に直接アクセスすることはできません。

ASRP では検索に Adobe クラウドが使用されます。

### MSRP {#msrp}

MSRP の場合、UGC は JCR には格納されず、MongoDB に格納されます。MSRPに格納されたUGCは、JCR APIを使用してCRXDE Liteで表示したり、アクセスしたりすることはできません。

[MSRP - MongoDB ストレージリソースプロバイダー](msrp.md)を参照してください。

MSRP は ASRP と互換性がありますが、すべての AEM サーバーインスタンスは同じ UGC にアクセスするので、共通のツールを使用して MongoDB に格納された UGC に直接アクセスできます。

MSRP では検索に Solr が使用されます。

### JSRP {#jsrp}

JSRP は、単一 AEM インスタンス上のすべての UGC にアクセスするためのデフォルトのプロバイダーです。MSRPやASRPを設定しなくても、AEM Communities 6.1をすばやく体験できます。

[JSRP - JCRストレージリソースプロバイダー](jsrp.md)を参照してください。

JSRP の場合、UGC は JCR に格納され、CRXDE Lite と JCR API の両方でアクセスできますが、JCR API は使用しないことを強くお勧めします。使用すると、今後の変更によってカスタムコードが影響を受ける可能性があります。

さらに、オーサー環境とパブリッシュ環境のリポジトリは共有されません。パブリッシュインスタンスのクラスターは共有パブリッシュリポジトリになりますが、パブリッシュ時に入力されたUGCはオーサーで表示されないので、オーサーからUGCを管理することはできません。 UGCは、UGCが入力されたインスタンスのAEMリポジトリ(JCR)にのみ保持されます。

JSRPは、クエリにOakインデックスを使用します。

## JCR でのシャドウノードについて {#about-shadow-nodes-in-jcr}

UGC へのパスを模倣するシャドウノードは、以下の 2 つの目的のためにローカルリポジトリに存在します。

1. [アクセス制御(ACL)](#for-access-control-acls)
1. [存在しないリソース（NER）](#for-non-existing-resources-ners)

SRPの実装に関係なく、実際のUGCはシャドウノードと同じ場所に表示されません。

### For Access Control (ACLs) {#for-access-control-acls}

一部の SRP 実装（ASRP や MSRP など）では、コミュニティコンテンツは ACL 検証が提供されないデータベースに格納されます。シャドウノードは、ACLを適用できるローカルリポジトリ内の場所を提供します。

SRP API を使用すると、すべての SRP オプションによって、すべての CRUD 操作の前にシャドウの場所の同じチェックが実行されます。

ACL チェックでは、リソースの UGC に適用される権限のチェックに適したパスを返すユーティリティメソッドが使用されます。

サンプルコードについては、[SRPとUGCの基本事項](srp-and-ugc.md)を参照してください。

### For Non-Existing Resources (NERs) {#for-non-existing-resources-ners}

一部のコミュニティコンポーネントはスクリプトに含めることができ、したがってコミュニティ機能をサポートするために Sling アドレス可能ノードが必要です。[含ま](scf.md#add-or-include-a-communities-component) れるコンポーネントは、存在しないリソース(NER)と呼ばれます。

シャドウノードによって、リポジトリ内の Sling アドレス可能な場所が提供されます。

>[!CAUTION]
>
>シャドウノードには複数の用途があるので、シャドウノードの存在はコンポーネントが NER であることを意味しません。**

### 格納場所 {#storage-location}

以下に、[コミュニティコンポーネントガイド](components-guide.md)で[コメントコンポーネント](http://localhost:4502/content/community-components/en/comments.html)を使用したシャドウノードの例を示します。

* コンポーネントは、次の場所にあるローカルリポジトリに存在します。

   `/content/community-components/en/comments/jcr:content/content/includable/comments`

* 対応するシャドウノードは、次の場所にあるローカルリポジトリに存在します。

   `/content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments`

シャドウノードの下には UGC はありません。

デフォルトの動作では、読み取りまたは書き込み用に関連するサブツリーが参照されるたびに、パブリッシュインスタンスにシャドウノードを設定します。

例えば、TarMKパブリッシュファームを使用したデプロイメントが[MSRP](msrp.md)であるとします。

[メンバー](users.md)がpub1にUGCを投稿すると（MongoDBに格納）、シャドウノードがpub1のJCRに作成されます。

UGCがpub2で初めて読み取られる場合、何も設定されていないと、デフォルトの動作でシャドウノードが作成されます。

デフォルト以外の動作が必要な場合は、それをオーサーインスタンスで設定し、すべてのパブリッシュインスタンスにロールフォワードする必要があります。これは通常は手動プロセスです。
