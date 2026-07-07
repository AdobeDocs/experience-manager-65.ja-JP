---
title: ストレージリソースプロバイダーの概要
description: ユーザー生成コンテンツ（UGC）と呼ばれるコミュニティコンテンツが、ストレージリソースプロバイダー（SRP）が提供するシンプルで一般的なストアにどのように保存されるのかを説明します。
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
source-wordcount: '1154'
ht-degree: 3%

---

# ストレージリソースプロバイダーの概要 {#storage-resource-provider-overview}

## はじめに {#introduction}

Adobe Experience Manager （AEM） Communities 6.1では、一般的にユーザー生成コンテンツ （UGC）と呼ばれるコミュニティコンテンツが、[&#x200B; ストレージリソースプロバイダー](working-with-srp.md) （SRP）が提供する1つの共通ストアに保存されています。

新しいAEM Communities インターフェイス [SocialResourceProvider API](srp-and-ugc.md) （SRP API）を介してUGCにアクセスするSRP オプションがいくつかあり、これには、すべての作成、読み取り、更新、削除（CRUD）操作が含まれます。

すべてのSCF コンポーネントはSRP APIを使用して実装されているため、[基になるトポロジ &#x200B;](topologies.md)またはUGCの場所を知らずにコードを開発できます。

***SocialResourceProvider APIは、AEM Communitiesのライセンスを取得したお客様のみが利用できます。***

>[!NOTE]
>
>**カスタムコンポーネント**: AEM Communitiesのライセンスを取得したお客様の場合、SRP APIは、基礎となるトポロジに関係なく、カスタムコンポーネントの開発者がUGCにアクセスできるようにします。 [SRPおよびUGC Essentials](srp-and-ugc.md)を参照してください。

関連トピック：

* [SRPおよびUGC Essentials](srp-and-ugc.md) - SRP ユーティリティのメソッドと例。
* [SRPを使用したUGCへのアクセス &#x200B;](accessing-ugc-with-srp.md) - コーディング ガイドライン。
* [SocialUtils リファクタリング &#x200B;](socialutils.md) – 非推奨のユーティリティメソッドを現在のSRP ユーティリティメソッドにマッピングします。

## リポジトリについて {#about-the-repository}

SRPを理解するには、AEM コミュニティサイトでのAEM リポジトリ（Oak）の役割を理解することが役立ちます。

**Java™ コンテンツ リポジトリ （JCR）**
この標準は、コンテンツリポジトリのデータモデルとアプリケーションプログラミングインターフェイス（[JCR API](https://jackrabbit.apache.org/jcr/jcr-api.html)）を定義します。 従来のファイルシステムの特徴とリレーショナルデータベースの特徴を組み合わせ、コンテンツアプリケーションに必要な追加機能をいくつか追加します。

JCRの実装の1つは、AEM リポジトリであるOakです。

**Apache Jackrabbit Oak**
[Oak](../../help/sites-deploying/platform.md)は、コンテンツ中心のアプリケーション向けに設計されたデータ ストレージ システムであるJCR 2.0の実装です。 これは、非構造化データと半構造化データ用に設計された階層データベースの一種です。 リポジトリには、ユーザーに表示されるコンテンツだけでなく、アプリケーションで使用されるすべてのコード、テンプレート、内部データも保存されます。 コンテンツにアクセスするためのUIは[CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)です。

JCRとOakの両方は、通常、AEM リポジトリを参照するために使用されます。

プライベートオーサー環境でサイトコンテンツを開発した後、パブリックパブリッシュ環境にコピーする必要があります。 これは多くの場合、*[replication](deploy-communities.md#replication-agents-on-author)*&#x200B;という操作を通じて行われます。 これは作成者/開発者/管理者のコントロール下で行われます。

UGCの場合、コンテンツは登録されたサイト訪問者（コミュニティメンバー）によってパブリッシュ環境に入力されます。 ランダムに発生します。

管理とレポートの目的では、プライベート オーサー環境からUGCにアクセスできることが便利です。 SRPでは、オーサーからオーサーへのリバースレプリケーションは必要ないため、オーサーからのUGCへのアクセスがより一貫性があり、パフォーマンスも高くなります。

## SRPについて {#about-srp}

UGCを共有ストレージに保存すると、メンバーコンテンツのインスタンスが1つだけ存在します。ほとんどのデプロイメントでは、オーサー環境とパブリッシュ環境の両方からアクセスできます。 SRPの選択（MSRP、ASRP、JSRP）に関係なく、すべてはSRP APIを使用してプログラムでアクセスする必要があります。

>[!NOTE]
>
>サンプルコードとその他の詳細については、[SRPおよびUGC Essentials](srp-and-ugc.md)を参照してください。
>
>コーディングのベストプラクティスについては、[SRPを使用したUGCへのアクセス &#x200B;](accessing-ugc-with-srp.md)を参照してください。

### ASRP {#asrp}

ASRPがある場合、UGCはJCRに保存されず、Adobeでホストおよび管理されるクラウドサービスに保存されます。 ASRPに保存されたUGCは、CRXDE Liteで表示したり、JCR APIを使用してアクセスしたりすることはできません。

[ASRP - Adobe ストレージリソースプロバイダー](asrp.md)を参照してください。

開発者がUGCに直接アクセスすることはできません。

ASRPは、クエリにAdobe Cloudを使用しています。

### MSRP {#msrp}

MSRP、UGCがJCRに保存されていない場合は、MongoDBに保存されます。 MSRPに保存されたUGCは、CRXDE Liteで表示したり、JCR APIを使用してアクセスしたりすることはできません。

[MSRP - MongoDB ストレージリソースプロバイダー](msrp.md)を参照してください。

MSRPはASRPと同等ですが、すべてのAEM サーバーインスタンスが同じUGCにアクセスしているため、一般的なツールを使用してMongoDBに保存されているUGCに直接アクセスできます。

MSRPはクエリにSolrを使用します。

### JSRP {#jsrp}

JSRPは、1つのAEM インスタンス上のすべてのUGCにアクセスするためのデフォルトプロバイダーです。 MSRPやASRPを設定しなくても、AEM Communities 6.1をすばやく体験できます。

[JSRP - JCR ストレージリソースプロバイダー](jsrp.md)を参照してください。

UGCがJCRに保存されている間にJSRPがあり、CRXDE LiteおよびJCR APIでアクセスできる場合、AdobeではJCR APIを使用しないことをお勧めします。 変更を加えると、今後の変更がカスタムコードに影響を与える可能性があります。

さらに、オーサー環境とパブリッシュ環境のリポジトリは共有されません。 パブリッシュインスタンスのクラスターは共有パブリッシュリポジトリになりますが、パブリッシュで入力されたUGCはオーサーには表示されないため、オーサーからUGCを管理することはできません。 UGCは、そのUGCが入力されたインスタンスのAEM リポジトリ（JCR）にのみ保持されます。

JSRPは、クエリにOak インデックスを使用します。

## JCRのシャドウノードについて {#about-shadow-nodes-in-jcr}

UGCへのパスを模倣するシャドウノードは、次の2つの目的を果たすためにローカルリポジトリに存在します。

1. [アクセス制御（ACL）](#for-access-control-acls)
1. [非既存リソース（NER）](#for-non-existing-resources-ners)

SRPの実装に関係なく、実際のUGCはシャドウ ノードと同じ場所に&#x200B;*not*&#x200B;表示されます。

### ACL （アクセス制御） {#for-access-control-acls}

ASRPやMSRPなどの一部のSRP実装では、ACL検証を提供しないデータベースにコミュニティ コンテンツを保存します。 シャドウノードは、ACLを適用できるローカルリポジトリ内の場所を提供します。

SRP APIを使用すると、すべてのSRP オプションは、すべてのCRUD操作の前にシャドウの場所を同じようにチェックします。

ACL チェックでは、リソースのUGCに適用される権限のチェックに適したパスを返すユーティリティメソッドを使用します。

サンプルコードについては、[SRPおよびUGC Essentials](srp-and-ugc.md)を参照してください。

### 非既存リソース（NER） {#for-non-existing-resources-ners}

一部のCommunities コンポーネントはスクリプト内に含まれるため、Communities機能をサポートするにはSling Addressable ノードが必要です。 [含まれるコンポーネント &#x200B;](scf.md#add-or-include-a-communities-component)は、既存でないリソース （NER）と呼ばれます。

シャドウノードは、リポジトリ内のSling アドレス可能な場所を提供します。

>[!CAUTION]
>
>シャドウ ノードには複数の用途があるため、シャドウ ノードの存在は&#x200B;*not*&#x200B;は、コンポーネントがNERであることを意味します。

### 保存場所 {#storage-location}

次に、[&#x200B; コミュニティコンポーネントガイド &#x200B;](components-guide.md)の[&#x200B; コメント コンポーネント &#x200B;](http://localhost:4502/content/community-components/en/comments.html)を使用したシャドウノードの例を示します。

* コンポーネントは、次の場所のローカルリポジトリに存在します。

  `/content/community-components/en/comments/jcr:content/content/includable/comments`

* 対応するシャドウ ノードは、次の場所のローカル リポジトリに存在します。

  `/content/usergenerated/content/community-components/en/comments/jcr:content/content/includable/comments`

シャドウ ノードの下にUGCが見つかりません。

デフォルトの動作は、読み取りまたは書き込みのために関連するサブツリーが参照されるたびに、パブリッシュインスタンスにシャドウノードを設定することです。

例えば、デプロイメントがTarMK パブリッシュファームを持つ[MSRP](msrp.md)であるとします。

[&#x200B; メンバー](users.md)が（MongoDBに保存されている） pub1にUGCを投稿すると、pub1のJCRにシャドウノードが作成されます。

pub2でUGCを初めて読み取る場合、何も設定されていない場合、デフォルトの動作はシャドウノードを作成することです。

デフォルトのビヘイビアー以外のビヘイビアーが必要な場合は、オーサーインスタンスで設定し、すべてのパブリッシュインスタンスにロールフォワードする必要があります。これは通常、手動プロセスです。
