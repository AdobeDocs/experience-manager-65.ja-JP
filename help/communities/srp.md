---
title: ストレージリソースプロバイダーの概要
description: ユーザー生成コンテンツ（UGC）と呼ばれるコミュニティコンテンツが、ストレージリソースプロバイダー（SRP）から提供されるシンプルで共通のストアにどのように保存されるかを説明します。
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 5f313274-1a2a-4e83-9289-60a4729b99b4
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1135'
ht-degree: 1%

---

# ストレージリソースプロバイダーの概要 {#storage-resource-provider-overview}

## はじめに {#introduction}

Adobe Experience Manager（AEM） Communities 6.1 では、コミュニティコンテンツ（一般的にユーザー生成コンテンツ（UGC）と呼ばれます）は、[ ストレージリソースプロバイダー ](working-with-srp.md) （SRP）から提供される単一の共通ストアに保存されます。

SRP オプションはいくつかあり、そのすべてが、新しいAEM Communities インターフェイスである [SocialResourceProvider API](srp-and-ugc.md) （SRP API）を通じて UGC にアクセスします。この API には、作成、読み取り、更新、削除（CRUD）のすべての操作が含まれています。

すべての SCF コンポーネントは SRP API を使用して実装されているため、[ 基盤となるトポロジ ](topologies.md) または UGC の場所に関する知識がなくてもコードを開発できます。

***SocialResourceProvider API は、AEM Communitiesのライセンスをお持ちのお客様のみが利用できます。***

>[!NOTE]
>
>**カスタムコンポーネント**:AEM Communitiesのライセンスをお持ちのお客様は、SRP API を、基盤となるトポロジに関係なく UGC にアクセスするカスタムコンポーネントの開発者が使用できます。 [SRP と UGC の初期設定 ](srp-and-ugc.md) を参照してください。

関連トピック：

* [SRP と UGC の基本事項 ](srp-and-ugc.md) - SRP ユーティリティメソッドと例。
* [SRP による UGC へのアクセス ](accessing-ugc-with-srp.md) - コーディングガイドライン。
* [SocialUtils リファクタリング ](socialutils.md) – 非推奨のユーティリティメソッドを現在の SRP ユーティリティメソッドにマッピングする

## リポジトリについて {#about-the-repository}

SRP を理解するには、AEM コミュニティサイトにおけるAEM リポジトリ（Oak）の役割を理解すると役に立ちます。

**Java™ コンテンツリポジトリ（JCR）**
この標準は、コンテンツリポジトリのデータモデルとアプリケーションプログラミングインターフェイス（[JCR API](https://jackrabbit.apache.org/jcr/jcr-api.html)）を定義します。 従来のファイルシステムの特性とリレーショナルデータベースの特性を組み合わせ、コンテンツアプリケーションでしばしば必要とされる機能をいくつか追加しています。

JCR の実装の 1 つにAEM リポジトリーであるOakがあります。

**Apache Jackrabbit Oak**
[Oak](../../help/sites-deploying/platform.md) は、コンテンツ中心のアプリケーション向けに設計されたデータストレージシステムである JCR 2.0 の実装です。 非構造化データと半構造化データ用に設計された階層データベースの一種です。 リポジトリには、ユーザーに表示されるコンテンツだけでなく、アプリケーションで使用されるすべてのコード、テンプレート、内部データも保存されます。 コンテンツにアクセスするための UI は、[CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md) です。

通常、JCR とOakは両方ともAEM リポジトリを参照するために使用されます。

非公開のオーサー環境でサイトコンテンツを開発した後、それを公開パブリッシュ環境にコピーする必要があります。 この操作は、多くの場合、*[レプリケーション](deploy-communities.md#replication-agents-on-author)* と呼ばれる操作を通じて行われます。 これは、作成者、開発者、管理者の管理下で行われます。

UGC の場合、コンテンツは、登録されたサイト訪問者（コミュニティメンバー）によって、公開パブリッシュ環境に入力されます。 これはランダムに発生します。

管理やレポートの目的では、非公開のオーサー環境から UGC にアクセスできると便利です。 Publishからオーサーへのリバースレプリケーションが必要ないので、SRP を使用すると、オーサーからの UGC へのアクセスの一貫性とパフォーマンスが向上します。

## SRP について {#about-srp}

UGC を共有ストレージに保存すると、メンバーコンテンツのインスタンスが 1 つになり、ほとんどのデプロイメントで、オーサー環境とパブリッシュ環境の両方からアクセスできます。 SRP の選択（MSRP、ASRP、JSRP）に関係なく、SRP API を使用してすべてにプログラムでアクセスする必要があります。

>[!NOTE]
>
>サンプルコードとその他の詳細については、[SRP と UGC の初期設定 ](srp-and-ugc.md) を参照してください。
>
>コーディング時のベストプラクティスについては、[SRP による UGC へのアクセス ](accessing-ugc-with-srp.md) を参照してください。

### ASRP {#asrp}

ASRP がある場合、UGC は JCR に格納されず、Adobeがホストおよび管理するクラウドサービスに格納されます。 ASRP に保存された UGC は、CRXDE Liteで閲覧したり、JCR API を使用してアクセスしたりすることはできません。

[ASRP - Adobeストレージリソースプロバイダー ](asrp.md) を参照してください。

開発者が UGC に直接アクセスすることはできません。

ASRP は、クエリにAdobeクラウドを使用します。

### MSRP {#msrp}

存在する場合、MSRP、UGC は JCR には格納されず、MongoDB に格納されます。 MSRP に保存された UGC には、CRXDE Liteで表示したり、JCR API を使用してアクセスしたりすることはできません。

[MSRP - MongoDB ストレージリソースプロバイダー ](msrp.md) を参照してください。

MSRP は ASRP に相当しますが、すべてのAEM サーバーインスタンスが同じ UGC にアクセスしているので、共通のツールを使用して MongoDB に保存された UGC に直接アクセスすることができます。

MSRP は、クエリに Solr を使用します。

### JSRP {#jsrp}

JSRP は、1 つのAEM インスタンス上のすべての UGC にアクセスするためのデフォルトのプロバイダーです。 これにより、MSRP や ASRP を設定しなくても、AEM Communities 6.1 をすばやく体験できます。

[JSRP - JCR ストレージリソースプロバイダー ](jsrp.md) を参照してください。

UGC が JCR に格納されていて、CRXDE Liteおよび JCR API でアクセスできる場合、Adobeは JCR API を使用しないことをお勧めします。 その場合、今後の変更により、カスタムコードに影響が出る可能性があります。

また、オーサー環境とPublish環境用のリポジトリは共有されません。 パブリッシュインスタンスのクラスターは共有パブリッシュリポジトリーになりますが、Publishに入力された UGC はオーサー環境には表示されないので、オーサー環境から UGC を管理することはできません。 UGC は、入力されたインスタンスのAEM リポジトリ（JCR）にのみ保持されます。

JSRP は、クエリにOak インデックスを使用します。

## JCR のシャドウノードについて {#about-shadow-nodes-in-jcr}

UGC のパスを模したシャドウノードがローカルリポジトリに存在し、次の 2 つの目的を果たします。

1. [アクセス制御（ACL）](#for-access-control-acls)
1. [存在しないリソース（NER）](#for-non-existing-resources-ners)

SRP の実装に関係なく、実際の UGC はシャドウノードと同じ場所に表示 *されません*。

### アクセス制御（ACL） {#for-access-control-acls}

ASRP や MSRP など、一部の SRP 実装では、ACL 検証を提供しないデータベースにコミュニティコンテンツを保存します。 シャドウノードは、ACL を適用できるローカルリポジトリ内の場所を提供します。

SRP API を使用すると、すべての SRP オプションは、すべての CRUD 操作の前にシャドウの場所の同じチェックを実行します。

ACL チェックでは、ユーティリティメソッドを使用して、リソースの UGC に適用される権限を確認するのに適したパスを返します。

サンプルコードについては、「[SRP と UGC の初期設定 ](srp-and-ugc.md)」を参照してください。

### 既存のリソース以外（NER） {#for-non-existing-resources-ners}

一部の Communities コンポーネントはスクリプト内に含まれるので、Communities の機能をサポートするには Sling アドレス可能なノードが必要です。 [ 含まれるコンポーネント ](scf.md#add-or-include-a-communities-component) は、存在しないリソース（NER）と呼ばれます。

シャドウノードは、リポジトリ内の Sling のアドレス指定可能な場所を提供します。

>[!CAUTION]
>
>シャドウノードには複数の用途があるので、シャドウノードが存在するということは、コンポーネントが NER であるということを意味 *しません*。

### 保存場所 {#storage-location}

[ コミュニティコンポーネントガイド ](components-guide.md) の [ コメントコンポーネント ](http://localhost:4502/content/community-components/en/comments.html) を使用した、シャドウノードの例を次に示します。

* コンポーネントは、次の場所にあるローカルリポジトリに存在します。

  `/content/community-components/en/comments/jcr:content/content/includable/comments`

* 対応するシャドウノードは、次の場所にあるローカルリポジトリに存在します。

  `/content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments`

シャドウノードの下に UGC が見つかりません。

デフォルトの動作では、関連するサブツリーが読み取りまたは書き込みに参照されるたびに、パブリッシュインスタンスにシャドウノードが設定されます。

例えば、デプロイメントが TarMK パブリッシュファームを使用する [MSRP](msrp.md) であるとします。

[ メンバー ](users.md) が UGC を pub1 に投稿すると（MongoDB に保存されます）、シャドーノードが pub1 の JCR に作成されます。

UGC が pub2 で初めて読み取られるときに、何も設定されていない場合、デフォルトの動作はシャドウノードを作成することです。

デフォルトの動作以外が必要な場合は、オーサーインスタンスで設定し、すべてのパブリッシュインスタンスにロールフォワードする必要があります。通常、これは手動のプロセスです。
