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
translation-type: tm+mt
source-git-commit: 7acd89d830b9e758eec1b5a4beb18c22e4d12dcf
workflow-type: tm+mt
source-wordcount: '1141'
ht-degree: 63%

---


# ストレージリソースプロバイダーの概要 {#storage-resource-provider-overview}

## 概要 {#introduction}

AEM Communities 6.1 以降、コミュニティコンテンツ（一般的にユーザー生成コンテンツ（UGC）と呼ばれる）は、[ストレージリソースプロバイダー](working-with-srp.md)（SRP）によって提供される単一の共通ストアに格納されます。

複数の SRP オプションがあり、それらはすべて、作成、読み取り、更新および削除（CRUD）操作がすべて含まれた、新しい AEM Communities インターフェイスである [SocialResourceProvider API](srp-and-ugc.md)（SRP API）によって UGC にアクセスします。

すべての SCF コンポーネントは SRP API を使用して実装されるので、[基になるトポロジ](topologies.md)または UGC の場所を知らなくてもコードを開発できます。

***SocialResourceProvider API は、AEM Communities の使用許諾を得たお客様のみが使用できます。***

>[!NOTE]
>
>**カスタムコンポーネント**：AEM Communities の使用許諾を得たお客様の場合、SRP API は、カスタムコンポーネントの開発者が、基になるトポロジに関係なく UGC にアクセスするために使用できます。See [SRP and UGC Essentials](srp-and-ugc.md).


関連トピック：

* [SRPとUGC Essentials](srp-and-ugc.md) - SRPユーティリティのメソッドと例。
* [SRP](accessing-ugc-with-srp.md) - Codingガイドラインを使用したUGCへのアクセス
* [SocialUtilsリファクタリング](socialutils.md) — 非推奨のユーティリティメソッドを現在のSRPユーティリティメソッドにマッピングします。

## リポジトリについて {#about-the-repository}

SRP を理解するには、AEM コミュニティサイトにおける AEM リポジトリ（OAK）の役割を理解することが必要です。

**Java Content Repository（JCR）** この規格では、コンテンツリポジトリのデータモデルおよびアプリケーションプログラミングインターフェイス（[JCR API](https://jackrabbit.apache.org/jcr/jcr-api.html)）が定義されます。従来のファイル・システムの特性とリレーショナル・データベースの特性を組み合わせ、コンテンツ・アプリケーションが頻繁に必要とする機能を多数追加します。

JCR の 1 つの実装が AEM リポジトリである OAK です。

**Apache Jackrabbit Oak（OAK）**[ OAK](../../help/sites-deploying/platform.md) は、コンテンツ中心のアプリケーション向けに特別に設計されたデータストレージシステムである JCR 2.0 の実装です。これは、非構造化データや半構造化データを対象に設計された階層型データベースの一種です。 このリポジトリには、ユーザーに表示されるコンテンツだけでなく、アプリケーションで使用されるすべてのコード、テンプレートおよび内部データが格納されます。The UI for accessing content is [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md).

JCR と OAK はどちらも、通常は AEM リポジトリを示すために使用されます。

非公開のオーサー環境でサイトコンテンツを開発した後、それを公開のパブリッシュ環境にコピーする必要があります。This is often done through an operation called *[replication](deploy-communities.md#replication-agents-on-author)*. これは、作成者、開発者、管理者の管理下で発生します。

UGC の場合、コンテンツは公開のパブリッシュ環境で登録済みサイト訪問者（コミュニティメンバー）によって生成されます。これはランダムに発生します。

管理およびレポートの目的では、非公開のオーサー環境から UGC にアクセスすることが有用です。SRPを使用すると、作成者からのUGCへのアクセスはより一貫性が高く、発行から作成者への逆複製は不要です。

## SRP について {#about-srp}

UGC が共有ストレージに格納される場合、ほとんどのデプロイメントでオーサー環境とパブリッシュ環境の両方からアクセスできるメンバーコンテンツの単一インスタンスがあります。SRPの選択(MSRP、ASRP、JSRP)に関係なく、すべてSRP APIを使用してプログラムからアクセスする必要があります。

>[!NOTE]
>
>See [SRP and UGC Essentials](srp-and-ugc.md) for sample code and additional details.
>
>コーディング時のベストプラクティスについては、[SRP による UGC へのアクセス](accessing-ugc-with-srp.md)を参照してください。


### ASRP {#asrp}

ASRP の場合、UGC は JCR には格納されず、Adobe がホストおよび管理するクラウドサービスに格納されます。ASRPに保存されたUGCは、CRXDE Liteで表示したり、JCR APIを使用してアクセスしたりすることはできません。

[ASRP - Adobe ストレージリソースプロバイダー](asrp.md)を参照してください。

開発者が UGC に直接アクセスすることはできません。

ASRP では検索に Adobe クラウドが使用されます。

### MSRP {#msrp}

MSRP の場合、UGC は JCR には格納されず、MongoDB に格納されます。MSRPに保存されたUGCは、CRXDE Liteで表示したり、JCR APIを使用してアクセスしたりすることはできません。

[MSRP - MongoDB ストレージリソースプロバイダー](msrp.md)を参照してください。

MSRP は ASRP と互換性がありますが、すべての AEM サーバーインスタンスは同じ UGC にアクセスするので、共通のツールを使用して MongoDB に格納された UGC に直接アクセスできます。

MSRP では検索に Solr が使用されます。

### JSRP {#jsrp}

JSRP は、単一 AEM インスタンス上のすべての UGC にアクセスするためのデフォルトのプロバイダーです。MSRPやASRPを設定しなくても、AEM Communities6.1を素早く体験できます。

See [JSRP - JCR Storage Resource Provider](jsrp.md).

JSRP の場合、UGC は JCR に格納され、CRXDE Lite と JCR API の両方でアクセスできますが、JCR API は使用しないことを強くお勧めします。使用すると、今後の変更によってカスタムコードが影響を受ける可能性があります。

さらに、オーサー環境とパブリッシュ環境のリポジトリは共有されません。発行インスタンスのクラスターは共有発行リポジトリになりますが、発行時に入力されたUGCは作成者に表示されないので、作成者からUGCを管理することはできません。 UGCは、そのUGCが入力されたインスタンスのAEMリポジトリ(JCR)でのみ持続します。

JSRP では検索に Oak インデックスが使用されます。

## JCR でのシャドウノードについて {#about-shadow-nodes-in-jcr}

UGC へのパスを模倣するシャドウノードは、以下の 2 つの目的のためにローカルリポジトリに存在します。

1. [アクセス制御(ACL)](#for-access-control-acls)
1. [存在しないリソース（NER）](#for-non-existing-resources-ners)

SRPの実装に関係なく、実際のUGCはシャドウノードと同じ場所に*表示されません。

### For Access Control (ACLs) {#for-access-control-acls}

一部の SRP 実装（ASRP や MSRP など）では、コミュニティコンテンツは ACL 検証が提供されないデータベースに格納されます。シャドウノードは、ACLを適用できるローカルリポジトリ内の場所を提供します。

SRP API を使用すると、すべての SRP オプションによって、すべての CRUD 操作の前にシャドウの場所の同じチェックが実行されます。

ACL チェックでは、リソースの UGC に適用される権限のチェックに適したパスを返すユーティリティメソッドが使用されます。

See [SRP and UGC Essentials](srp-and-ugc.md) for sample code.

### For Non-Existing Resources (NERs) {#for-non-existing-resources-ners}

一部のコミュニティコンポーネントはスクリプトに含めることができ、したがってコミュニティ機能をサポートするために Sling アドレス可能ノードが必要です。[含まれるコンポーネント](scf.md#add-or-include-a-communities-component) は、「既存以外のリソース(NER)」と呼ばれます。

シャドウノードによって、リポジトリ内の Sling アドレス可能な場所が提供されます。

>[!CAUTION]
>
>シャドウノードには複数の用途があるので、シャドウノードの存在はコンポーネントが NER であることを意味しません。**


### 格納場所 {#storage-location}

Following is an example of a shadow node, using the [Comments component](http://localhost:4502/content/community-components/en/comments.html) in the [Community Components Guide](components-guide.md):

* コンポーネントは次の場所にあるローカルリポジトリに存在します。

   `/content/community-components/en/comments/jcr:content/content/includable/comments`

* 対応するシャドウノードは、次の場所にあるローカルリポジトリに存在します。

   `/content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments`

シャドウノードの下には UGC はありません。

デフォルトの動作では、関連するサブツリーが読み取りまたは書き込み用に参照されるたびに、発行インスタンスにシャドウノードを設定します。

As an example, suppose the deployment is [MSRP](msrp.md) with a TarMK publish farm.

When a [member](users.md) posts UGC on pub1 (stored in MongoDB), shadow nodes are created in JCR on pub1.

pub2でUGCを初めて読み取るとき、何も設定されていない場合は、デフォルトの動作でシャドウノードが作成されます。

デフォルト以外の動作が必要な場合は、それをオーサーインスタンスで設定し、すべてのパブリッシュインスタンスにロールフォワードする必要があります。これは通常は手動プロセスです。
