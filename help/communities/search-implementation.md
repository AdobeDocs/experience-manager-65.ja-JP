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
translation-type: tm+mt
source-git-commit: 9a4ae73c08657195da2741cccdb196bd7f7142c9
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 40%

---


# 検索の基本事項 {#search-essentials}

## 概要 {#overview}

検索機能は AEM Communities の基本機能です。[AEM platform search](../../help/sites-deploying/queries-and-indexing.md)機能に加えて、AEM Communitiesはユーザ生成コンテンツ(UGC)を検索する目的で[UGC search API](#ugc-search-api)を提供しています。 UGCには、他のAEMコンテンツやユーザーデータとは別に入力および保存されるので、固有のプロパティがあります。

Communitiesでは、一般に検索される2つの項目は次のとおりです。

* コミュニティメンバーが投稿したコンテンツ

   * AEM CommunitiesのUGC検索APIを使用します。

* ユーザーとユーザーグループ（ユーザーデータ）

   * AEMプラットフォーム検索機能を使用します。

ドキュメントのこの節は、UGC を作成または管理するためのカスタムコンポーネントの作成を担当する開発者を対象としています。

## セキュリティおよびシャドウノード  {#security-and-shadow-nodes}

カスタムコンポーネントの場合は、[SocialResourceUtilities](socialutils.md#socialresourceutilities-package)メソッドを使用する必要があります。 UGCを作成および検索するユーティリティメソッドは、必要な[シャドウノード](srp.md#about-shadow-nodes-in-jcr)を確立し、メンバーに要求に対する正しい権限があることを確認します。

モデレート関連のプロパティについては、SRP ユーティリティでは管理しません。

UGCおよびACLシャドウノードへのアクセスに使用するユーティリティメソッドの詳細については、[SRPとUGC Essentials](srp-and-ugc.md)を参照してください。

## UGC Search API {#ugc-search-api}

[UGC 共通ストア](working-with-srp.md)は、それぞれ異なるネイティブクエリー言語を使用する様々なストレージリソースプロバイダー（SRP）の 1 社から提供されます。したがって、選択したSRPに関係なく、カスタムコードは[UGC APIパッケージ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html)(*com.adobe.cq.sosical.ugc.api*)からのメソッドを使用し、選択したSRPに適したクエリ言語を呼び出す必要があります。

### ASRP 検索 {#asrp-searches}

[ASRP](asrp.md)の場合、UGCはAdobeクラウドに保存されます。 UGCはCRXに表示されませんが、[モデレート](moderate-ugc.md)は作成者と発行の両方の環境から利用できます。 [UGC検索API](#ugc-search-api)の使用は、ASRPでは他のSRPと同じように機能します。

ASRP 検索を管理するためのツールは現在存在しません。

検索可能なカスタムプロパティを作成する場合は、[命名規則](#naming-of-custom-properties)に従う必要があります。

### MSRP 検索 {#msrp-searches}

[MSRP](msrp.md)の場合、UGCはSolrを使用して検索するように設定されたMongoDBに保存されます。 UGCはCRXには表示されませんが、[モデレート](moderate-ugc.md)は作成者と発行の両方の環境から利用できます。

MSRP および Solr については、次の点に留意してください。

* AEMプラットフォーム用の埋め込みSolrは、MSRPには使用されません。
* AEMプラットフォームにリモートSolrを使用する場合、MSRPと共有できますが、異なるコレクションを使用する必要があります。
* Solrは、標準検索または多言語検索(MLS)用に設定できます。
* 設定の詳細については、「MSRPの[Solr設定](msrp.md#solr-configuration)」を参照してください。

カスタム検索機能では、[UGC検索API](#ugc-search-api)を使用する必要があります。

検索可能なカスタムプロパティを作成する場合は、[命名規則](#naming-of-custom-properties)に従う必要があります。

### JSRP 検索 {#jsrp-searches}

[JSRP](jsrp.md)の場合、UGCは[Oak](../../help/sites-deploying/platform.md)に保存され、入力されたAEM作成者インスタンスまたは発行インスタンスのリポジトリにのみ表示されます。

UGC は一般にパブリッシュ環境で入力されるので、複数の公開者が存在する実稼動システムでは、パブリッシュファームではなく、[パブリッシュクラスター](topologies.md)の設定を通して、入力されたコンテンツがすべての公開者から表示できるようにする必要があります。

JSRP の場合、パブリッシュ環境で入力された UGC はオーサー環境には表示されません。したがって、すべての[モデレート](moderate-ugc.md)タスクは発行環境で行われます。

カスタム検索機能では、[UGC検索API](#ugc-search-api)を使用する必要があります。

#### Oak インデックスの作成 {#oak-indexing}

AEMプラットフォーム検索では、Oakインデックスは自動的には作成されませんが、AEM 6.2以降では、パフォーマンスを向上させ、UGC検索結果を表示する際のページネーションをサポートするため、AEM Communities向けに追加されています。

カスタムプロパティが使用中で検索が遅い場合は、カスタムプロパティのパフォーマンスを高めるために、カスタムプロパティ用に追加のインデックスを作成する必要があります。 携帯性を維持するために、検索可能なカスタムプロパティを作成する際は、[命名規則](#naming-of-custom-properties)に従ってください。

既存のインデックスの変更やカスタムインデックスの作成については、[Oakクエリとインデックス作成](../../help/sites-deploying/queries-and-indexing.md)を参照してください。

[Oak Index Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/oak-index-manager.html)は、ACS AEM Commonsから入手できます。 次の機能が提供されます。

* 既存のインデックスの表示。
* 再インデックスを開始する機能。

[CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)内の既存のOakインデックスを表示するには、次の場所に移動します。

* `/oak:index/socialLucene`

![社会的利益](assets/social-lucene.png)

## インデックス付き検索のプロパティ {#indexed-search-properties}

### デフォルトの検索プロパティ {#default-search-properties}

様々なコミュニティ機能に使用される検索可能なプロパティの一部を次に示します。

| **プロパティ** | **データタイプ** |
|---|---|
| isFlagged | *Boolean* |
| isSpam | *ブール値* |
| 読み取り | *ブール値* |
| influence | *ブール値* |
| attachments | *ブール値* |
| sentiment | 長整数&#x200B;** |
| flagged | *ブール値* |
| added | *日付* |
| modifiedDate | *日付* |
| state | *String* |
| userIdentifier | *文字列* |
| replies | 長整数&#x200B;** |
| jcr:title | *文字列* |
| jcr:description | *文字列* |
| sling:resourceType | *文字列* |
| allowThreadedReply | *ブール値* |
| isDraft | *ブール値* |
| publishDate | *日付* |
| publishJobId | *文字列* |
| answered | *ブール値* |
| chosenanswered | *ブール値* |
| tag | *文字列* |
| cq:Tag | *文字列* |
| author_display_name | *文字列* |
| location_t | *文字列* |
| parentPath | *文字列* |
| parentTitle | 文字列&#x200B;** |

### カスタムプロパティの命名  {#naming-of-custom-properties}

カスタムプロパティを追加する場合、[UGC検索API](#ugc-search-api)で作成された並べ替えや検索でこれらのプロパティを表示するには、プロパティ名にサフィックスを追加する&#x200B;*必要な*&#x200B;があります。

サフィックスは、スキーマを使用するクエリ言語用です。

* プロパティは検索可能であることを示します。
* データタイプを識別します。

Solr は、スキーマを使用するクエリー言語の一例です。

| **サフィックス** | **データタイプ** |
|---|---|
| _b | *ブール値* |
| _dt | カレンダー&#x200B;** |
| _d | 倍精度浮動小数点&#x200B;** |
| _tl | 長整数&#x200B;** |
| _s | *文字列* |
| _t | *テキスト* |

**備考:**

* ** テキストはトークン化された文字列で、 ** 文字列は含まれません。*テキスト*&#x200B;を使用して、あいまい検索を行います（このように）。

* 複数の値を持つタイプの場合、次のようにサフィックスに「s」を追加します。

   * `viewDate_dt`:単一の日付プロパティ
   * `viewDates_dts`:datesプロパティのリスト

## フィルター {#filters}

[コメントシステム](essentials-comments.md)を含むコンポーネントは、そのエンドポイントにフィルターパラメーターを追加できます。

AND および OR ロジックのフィルター構文は次のようになります（URL エンコード処理前）。

* OR を指定するには、1 つのフィルターパラメーターを使用し、値をカンマで区切って指定します。

   * `filter=name eq 'Jennifer',name eq 'Jen'`

* AND を指定するには、複数のフィルターパラメーターを使用します。

   * `filter = name eq 'Jackson'&filter=message eq 'testing'`

[コミュニティコンポーネントガイド](components-guide.md)で「検索結果」ページを開く際に使用される URL に見られるように、[検索コンポーネント](search.md)のデフォルト実装ではこの構文が使用されます。テストするには、[http://localhost:4503/content/community-components/en/search.html](http://localhost:4503/content/community-components/en/search.html)を参照します。

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

* 正しい構文：フォーラム要素
   * `/content/community-components/en/forum/jcr:content/content/forum.social.json`
* 誤った例：フォーラムページ
   * `/content/community-components/en/forum.social.json`

## SRP ツール {#srp-tools}

次のものをまとめた Adobe Marketing Cloud GitHub プロジェクトが公開されています。

[AEM CommunitiesSRPツール](https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools)

このリポジトリには、SRP のデータを管理するためのツールが格納されています。

現在、任意の SRP からすべての UGC を削除できるサーブレットが 1 つ用意されています。

次に、ASRP からすべての UGC を削除する場合の例を示します。

```shell
curl -X POST http://localhost:4502/services/social/srp/cleanup?path=/content/usergenerated/asi/cloud -uadmin:admin
```

## トラブルシューティング {#troubleshooting}

### Solr クエリ {#solr-query}

Solrクエリの問題のトラブルシューティングに役立つには、

`com.adobe.cq.social.srp.impl.SocialSolrConnector`.

実際の Solr クエリが、デバッグログに URL エンコードされて表示されます。

solrへのクエリ:`sort=timestamp+desc&bl=en&pl=en&start=0&rows=10 &q=%2Btitle_t:(hello)+%2Bprovider_id:\/content/usergenerated/asi/mongo/content/+%2Bresource_type_s:&df=provider_id&trf=verbatim&fq={!cost%3D100}report_suite:mongo`

`q` パラメーターの値がクエリです。URLエンコーディングがデコードされると、クエリをSolr管理者クエリツールに渡して、さらに詳細なデバッグを行うことができます。

## 関連リソース {#related-resources}

* [コミュニティコンテンツストレージ](working-with-srp.md) - UGC共通ストアで使用できるSRPの選択肢について説明します。
* [ストレージリソースプロバイダの概要](srp.md)  — 概要とリポジトリ使用の概要
* [SRP](accessing-ugc-with-srp.md) - Codingガイドラインを使用したUGCへのアクセス
* [SocialUtilsリファクタリング](socialutils.md) - SocialUtilsを置き換えるSRPのユーティリティメソッド。
* [検索と検索結果のコンポーネント](search.md)  — テンプレートへのUGC検索機能の追加

