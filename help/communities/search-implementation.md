---
title: 検索の基本事項
seo-title: 検索の基本事項
description: Communities での検索
seo-description: Communities での検索
uuid: 5f35a033-2069-499e-9cdb-db25781312f0
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 300aa9f3-596f-42bc-8d46-e535f2bc4379
exl-id: 8af5ee58-19d7-47b6-b45d-e88006703a5d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 40%

---

# 検索の基本事項 {#search-essentials}

## 概要 {#overview}

検索機能は AEM Communities の基本機能です。AEM Communitiesは、[AEMプラットフォーム検索](../../help/sites-deploying/queries-and-indexing.md)機能に加えて、ユーザー生成コンテンツ(UGC)を検索するための[UGC検索API](#ugc-search-api)を提供します。 UGCには、他のAEMコンテンツやユーザーデータとは別に入力および保存される一意のプロパティがあります。

Communitiesの場合、一般に検索される2つの項目は次のとおりです。

* コミュニティメンバーが投稿したコンテンツ

   * AEM CommunitiesのUGC検索APIを使用します。

* ユーザーとユーザーグループ（ユーザーデータ）

   * AEMプラットフォームの検索機能を使用します。

ドキュメントのこの節は、UGC を作成または管理するためのカスタムコンポーネントの作成を担当する開発者を対象としています。

## セキュリティおよびシャドウノード  {#security-and-shadow-nodes}

カスタムコンポーネントの場合は、[SocialResourceUtilities](socialutils.md#socialresourceutilities-package)メソッドを使用する必要があります。 UGCを作成および検索するユーティリティメソッドは、必要な[シャドウノード](srp.md#about-shadow-nodes-in-jcr)を確立し、メンバーにリクエストに対する正しい権限があることを確認します。

モデレート関連のプロパティについては、SRP ユーティリティでは管理しません。

UGCおよびACLシャドウノードへのアクセスに使用するユーティリティメソッドについては、[SRPとUGCの基本事項](srp-and-ugc.md)を参照してください。

## UGC Search API {#ugc-search-api}

[UGC 共通ストア](working-with-srp.md)は、それぞれ異なるネイティブクエリー言語を使用する様々なストレージリソースプロバイダー（SRP）の 1 社から提供されます。したがって、選択したSRPに関係なく、カスタムコードでは、[UGC APIパッケージ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html)(*com.adobe.cq.social.ugc.api*)のメソッドを使用し、選択したSRPに適したクエリ言語を呼び出す必要があります。

### ASRP 検索 {#asrp-searches}

[ASRP](asrp.md)の場合、UGCはAdobeクラウドに格納されます。 UGCはCRXでは表示されませんが、オーサー環境とパブリッシュ環境の両方で[モデレート](moderate-ugc.md)を使用できます。 [UGC検索API](#ugc-search-api)の使用は、ASRPでも他のSRPと同じように機能します。

ASRP 検索を管理するためのツールは現在存在しません。

検索可能なカスタムプロパティを作成する場合は、[命名要件](#naming-of-custom-properties)に従う必要があります。

### MSRP 検索 {#msrp-searches}

[MSRP](msrp.md)の場合、UGCはSolrを使用して検索するように設定されたMongoDBに格納されます。 UGCはCRXには表示されませんが、オーサー環境とパブリッシュ環境の両方で[モデレート](moderate-ugc.md)を使用できます。

MSRP および Solr については、次の点に留意してください。

* AEMプラットフォーム用の埋め込みSolrは、MSRPには使用されません。
* AEMプラットフォームにリモートSolrを使用している場合は、MSRPと共有できますが、異なるコレクションを使用する必要があります。
* Solrは、標準検索または多言語検索(MLS)用に設定できます。
* 設定について詳しくは、MSRPの[Solr設定](msrp.md#solr-configuration)を参照してください。

カスタム検索機能では、[UGC検索API](#ugc-search-api)を使用する必要があります。

検索可能なカスタムプロパティを作成する場合は、[命名要件](#naming-of-custom-properties)に従う必要があります。

### JSRP 検索 {#jsrp-searches}

[JSRP](jsrp.md)の場合、UGCは[Oak](../../help/sites-deploying/platform.md)に格納され、入力されたAEMオーサーインスタンスまたはパブリッシュインスタンスのリポジトリにのみ表示されます。

UGC は一般にパブリッシュ環境で入力されるので、複数の公開者が存在する実稼動システムでは、パブリッシュファームではなく、[パブリッシュクラスター](topologies.md)の設定を通して、入力されたコンテンツがすべての公開者から表示できるようにする必要があります。

JSRP の場合、パブリッシュ環境で入力された UGC はオーサー環境には表示されません。したがって、すべての[モデレート](moderate-ugc.md)タスクはパブリッシュ環境で実行されます。

カスタム検索機能では、[UGC検索API](#ugc-search-api)を使用する必要があります。

#### Oak インデックスの作成 {#oak-indexing}

AEMプラットフォーム検索用にOakインデックスは自動的には作成されませんが、AEM 6.2以降では、UGC検索結果を表示する際のパフォーマンスを向上し、ページ編集をサポートするためにAEM Communitiesに追加されました。

カスタムプロパティが使用中で、検索に時間がかかる場合は、カスタムプロパティのパフォーマンスを向上させるために、追加のインデックスを作成する必要があります。 ポータビリティを維持するために、検索可能なカスタムプロパティを作成する際には、[命名要件](#naming-of-custom-properties)に従ってください。

既存のインデックスの変更やカスタムインデックスの作成については、[Oakクエリとインデックス作成](../../help/sites-deploying/queries-and-indexing.md)を参照してください。

[Oak Index Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/oak-index-manager.html)は、ACS AEM Commonsから入手できます。 以下を提供します。

* 既存のインデックスのビュー。
* インデックス再作成を開始する機能。

[CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)内の既存のOakインデックスを表示するには、次の場所に移動します。

* `/oak:index/socialLucene`

![social-lucene](assets/social-lucene.png)

## インデックス付き検索のプロパティ {#indexed-search-properties}

### デフォルトの検索プロパティ {#default-search-properties}

様々なコミュニティ機能に使用される検索可能なプロパティの一部を次に示します。

| **プロパティ** | **データタイプ** |
|---|---|
| isFlagged | *ブール型* |
| isSpam | *ブール型* |
| 読み取り | *ブール型* |
| influence | *ブール型* |
| attachments | *ブール型* |
| sentiment | 長整数&#x200B;** |
| flagged | *ブール型* |
| added | *日付* |
| modifiedDate | *日付* |
| state | *String* |
| userIdentifier | *文字列* |
| replies | 長整数&#x200B;** |
| jcr:title | *文字列* |
| jcr:description | *文字列* |
| sling:resourceType | *文字列* |
| allowThreadedReply | *ブール型* |
| isDraft | *ブール型* |
| publishDate | *日付* |
| publishJobId | *文字列* |
| answered | *ブール型* |
| chosenanswered | *ブール型* |
| tag | *文字列* |
| cq:Tag | *文字列* |
| author_display_name | *文字列* |
| location_t | *文字列* |
| parentPath | *文字列* |
| parentTitle | 文字列&#x200B;** |

### カスタムプロパティの命名  {#naming-of-custom-properties}

カスタムプロパティを追加する場合、[UGC検索API](#ugc-search-api)で作成された並べ替えや検索でこれらのプロパティを表示するには、プロパティ名にサフィックスを追加する必要があります。**

サフィックスは、スキーマを使用するクエリ言語用です。

* プロパティが検索可能であることを示します。
* データタイプを識別します。

Solr は、スキーマを使用するクエリー言語の一例です。

| **サフィックス** | **データタイプ** |
|---|---|
| _b | *ブール型* |
| _dt | *Calendar* |
| _d | 倍精度浮動小数点&#x200B;** |
| _tl | 長整数&#x200B;** |
| _s | *文字列* |
| _t | *テキスト* |

**備考:**

* ** テキストはトークン化された文字列で ** す。文字列ではありません。あいまい検索には&#x200B;*テキスト*&#x200B;を使用します（このような検索）。

* 複数の値を持つタイプの場合、次のようにサフィックスに「s」を追加します。

   * `viewDate_dt`:単一の日付プロパティ
   * `viewDates_dts`:日付プロパティのリスト

## フィルター {#filters}

[コメントシステム](essentials-comments.md)を含むコンポーネントは、エンドポイントにフィルターパラメーターを追加できます。

AND および OR ロジックのフィルター構文は次のようになります（URL エンコード処理前）。

* OR を指定するには、1 つのフィルターパラメーターを使用し、値をカンマで区切って指定します。

   * `filter=name eq 'Jennifer',name eq 'Jen'`

* AND を指定するには、複数のフィルターパラメーターを使用します。

   * `filter = name eq 'Jackson'&filter=message eq 'testing'`

[コミュニティコンポーネントガイド](components-guide.md)で「検索結果」ページを開く際に使用される URL に見られるように、[検索コンポーネント](search.md)のデフォルト実装ではこの構文が使用されます。実験するには、[http://localhost:4503/content/community-components/en/search.html](http://localhost:4503/content/community-components/en/search.html)を参照します。

フィルター演算子は次のとおりです。

| EQ | 次と等しい |
|---|---|
| NE | 次と等しくない |
| LT | 次よりも小さい |
| LTE | 次よりも小さいか等しい |
| GE | 次よりも大きい |
| GTE | 次よりも大きいか等しい |
| LIKE | ファジーマッチ |

コンポーネントが配置されるページではなく、コミュニティコンポーネント（リソース）を URL で参照することが重要です。

* 正しい構文：フォーラムコンポーネント
   * `/content/community-components/en/forum/jcr:content/content/forum.social.json`
* 誤った構文：フォーラムページ
   * `/content/community-components/en/forum.social.json`

## SRP ツール {#srp-tools}

次のものをまとめた Adobe Marketing Cloud GitHub プロジェクトが公開されています。

[AEM Communities SRPツール](https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools)

このリポジトリには、SRP のデータを管理するためのツールが格納されています。

現在、任意の SRP からすべての UGC を削除できるサーブレットが 1 つ用意されています。

次に、ASRP からすべての UGC を削除する場合の例を示します。

```shell
curl -X POST http://localhost:4502/services/social/srp/cleanup?path=/content/usergenerated/asi/cloud -uadmin:admin
```

## トラブルシューティング {#troubleshooting}

### Solr クエリ  {#solr-query}

Solrクエリの問題のトラブルシューティングに役立つように、

`com.adobe.cq.social.srp.impl.SocialSolrConnector`

実際の Solr クエリが、デバッグログに URL エンコードされて表示されます。

Solrに対するクエリ：`sort=timestamp+desc&bl=en&pl=en&start=0&rows=10 &q=%2Btitle_t:(hello)+%2Bprovider_id:\/content/usergenerated/asi/mongo/content/+%2Bresource_type_s:&df=provider_id&trf=verbatim&fq={!cost%3D100}report_suite:mongo`

`q` パラメーターの値がクエリです。URLエンコーディングがデコードされたら、クエリをSolr Admin Queryツールに渡して、さらにデバッグできます。

## 関連リソース {#related-resources}

* [コミュニティコンテンツストレージ](working-with-srp.md)  - UGC共通ストアで使用可能なSRPの選択肢について説明します。
* [ストレージリソースプロバイダーの概要](srp.md)  — 概要とリポジトリの使用方法の概要。
* [SRPによるUGCへのアクセス](accessing-ugc-with-srp.md)  — コーディングのガイドライン
* [SocialUtilsのリファクタリング](socialutils.md)  - SocialUtilsに代わるSRPのユーティリティメソッド。
* [検索および検索結果コンポーネント](search.md)  — テンプレートにUGC検索機能を追加します。
