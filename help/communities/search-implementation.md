---
title: 検索の基本事項
seo-title: Search Essentials
description: Communities での検索
seo-description: Search in Communities
uuid: 5f35a033-2069-499e-9cdb-db25781312f0
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 300aa9f3-596f-42bc-8d46-e535f2bc4379
exl-id: 8af5ee58-19d7-47b6-b45d-e88006703a5d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1184'
ht-degree: 40%

---

# 検索の基本事項 {#search-essentials}

## 概要 {#overview}

検索機能は AEM Communities の基本機能です。また、 [AEM platform 検索](../../help/sites-deploying/queries-and-indexing.md) 機能、AEM Communities [UGC 検索 API](#ugc-search-api) ユーザー生成コンテンツ (UGC) を検索する目的で使用します。 UGC には、他のAEMコンテンツやユーザーデータとは別に入力および保存される固有のプロパティがあります。

Communities では、一般的に検索される 2 つの項目は次のとおりです。

* コミュニティメンバーが投稿したコンテンツ

   * AEM Communities の UGC 検索 API を使用します。

* ユーザーとユーザーグループ（ユーザーデータ）

   * AEMプラットフォーム検索機能を使用します。

ドキュメントのこの節は、UGC を作成または管理するためのカスタムコンポーネントの作成を担当する開発者を対象としています。

## セキュリティおよびシャドウノード {#security-and-shadow-nodes}

カスタムコンポーネントの場合、 [SocialResourceUtilities](socialutils.md#socialresourceutilities-package) メソッド。 UGC を作成および検索するユーティリティメソッドは、必要な [シャドウノード](srp.md#about-shadow-nodes-in-jcr) メンバーがリクエストに対する正しい権限を持っていることを確認します。

モデレート関連のプロパティについては、SRP ユーティリティでは管理しません。

詳しくは、 [SRP と UGC の基本事項](srp-and-ugc.md) UGC および ACL シャドウノードへのアクセスに使用するユーティリティメソッドに関する情報。

## UGC 検索 API {#ugc-search-api}

[UGC 共通ストア](working-with-srp.md)は、それぞれ異なるネイティブクエリー言語を使用する様々なストレージリソースプロバイダー（SRP）の 1 社から提供されます。したがって、選択した SRP に関係なく、カスタムコードでは [UGC API パッケージ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) (*com.adobe.cq.social.ugc.api*) を呼び出し、選択した SRP に適したクエリ言語を呼び出します。

### ASRP 検索 {#asrp-searches}

の場合 [ASRP](asrp.md)に設定した場合、UGC はAdobeクラウドに保存されます。 UGC は CRX には表示されませんが、 [モデレート](moderate-ugc.md) は、オーサー環境とパブリッシュ環境の両方から使用できます。 の使用 [UGC 検索 API](#ugc-search-api) ASRP では、他の SRP と同じように機能します。

ASRP 検索を管理するためのツールは現在存在しません。

検索可能なカスタムプロパティを作成する場合は、 [命名要件](#naming-of-custom-properties).

### MSRP 検索 {#msrp-searches}

の場合 [MSRP](msrp.md)を使用する場合、UGC は Solr を使用して検索するように設定された MongoDB に保存されます。 UGC は CRX には表示されませんが、 [モデレート](moderate-ugc.md) は、オーサー環境とパブリッシュ環境の両方から使用できます。

MSRP および Solr については、次の点に留意してください。

* AEMプラットフォームに埋め込まれた Solr は、MSRP には使用されません。
* AEMプラットフォームにリモート Solr を使用している場合、MSRP と共有できますが、異なるコレクションを使用する必要があります。
* Solr は、標準検索または多言語検索 (MLS) 用に設定できます。
* 設定の詳細については、 [Solr 設定](msrp.md#solr-configuration) （MSRP 用）

カスタム検索機能では、 [UGC 検索 API](#ugc-search-api).

検索可能なカスタムプロパティを作成する場合は、 [命名要件](#naming-of-custom-properties).

### JSRP 検索 {#jsrp-searches}

の場合 [JSRP](jsrp.md)に設定した場合、UGC は [Oak](../../help/sites-deploying/platform.md) とは、入力されたAEMオーサーインスタンスまたはパブリッシュインスタンスのリポジトリーにのみ表示されます。

UGC は一般にパブリッシュ環境で入力されるので、複数の公開者が存在する実稼動システムでは、パブリッシュファームではなく、[パブリッシュクラスター](topologies.md)の設定を通して、入力されたコンテンツがすべての公開者から表示できるようにする必要があります。

JSRP の場合、パブリッシュ環境で入力された UGC はオーサー環境には表示されません。したがって、すべて [モデレート](moderate-ugc.md) タスクはパブリッシュ環境で実行されます。

カスタム検索機能では、 [UGC 検索 API](#ugc-search-api).

#### Oak インデックスの作成 {#oak-indexing}

AEMプラットフォーム検索では Oak インデックスは自動的に作成されませんが、AEM 6.2 以降では、AEM Communitiesのパフォーマンスを向上させ、UGC 検索結果を表示する際のページネーションをサポートするために、Oak インデックスが追加されました。

カスタムプロパティが使用中で検索に時間がかかる場合は、カスタムプロパティのパフォーマンスを高めるために、追加のインデックスを作成する必要があります。 移植性を維持するには、 [命名要件](#naming-of-custom-properties) 検索可能なカスタムプロパティを作成する際。

既存のインデックスの変更やカスタムインデックスの作成については、 [Oak クエリとインデックス作成](../../help/sites-deploying/queries-and-indexing.md).

この [Oak インデックスマネージャ](https://adobe-consulting-services.github.io/acs-aem-commons/features/oak-index-manager.html) は、ACS AEM Commons から入手できます。 これには次の機能があります。

* 既存のインデックスのビュー。
* インデックス再作成を開始する機能。

で既存の Oak インデックスを表示するには、以下を実行します。 [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)の場所は次のようになります。

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
| sentiment | *Long* |
| flagged | *ブール型* |
| added | *日付* |
| modifiedDate | *日付* |
| ステート | *String* |
| userIdentifier | *文字列* |
| replies | *Long* |
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
| parentTitle | *文字列* |

### カスタムプロパティの命名 {#naming-of-custom-properties}

カスタムプロパティを追加する場合、これらのプロパティを、 [UGC 検索 API](#ugc-search-api)、 *必須* をクリックして、プロパティ名にサフィックスを追加します。

サフィックスは、スキーマを使用するクエリ言語用です。

* プロパティが検索可能であることを識別します。
* データタイプを識別します。

Solr は、スキーマを使用するクエリー言語の一例です。

| **サフィックス** | **データタイプ** |
|---|---|
| _b | *ブール型* |
| _dt | *Calendar* |
| _d | *倍精度浮動小数点* |
| _tl | *Long* |
| _秒 | *文字列* |
| _t | *テキスト* |

**メモ：**

* *テキスト* はトークン化された文字列です。 *文字列* がではありません。 用途 *テキスト* fuzy（より似た）検索用。

* 複数の値を持つタイプの場合、次のようにサフィックスに「s」を追加します。

   * `viewDate_dt`:単一の日付プロパティ
   * `viewDates_dts`:日付プロパティのリスト

## フィルター {#filters}

次を含むコンポーネント： [コメントシステム](essentials-comments.md) は、エンドポイントへのフィルターパラメーターの追加をサポートしています。

AND および OR ロジックのフィルター構文は次のようになります（URL エンコード処理前）。

* OR を指定するには、1 つのフィルターパラメーターを使用し、値をカンマで区切って指定します。

   * `filter=name eq 'Jennifer',name eq 'Jen'`

* AND を指定するには、複数のフィルターパラメーターを使用します。

   * `filter = name eq 'Jackson'&filter=message eq 'testing'`

[コミュニティコンポーネントガイド](components-guide.md)で「検索結果」ページを開く際に使用される URL に見られるように、[検索コンポーネント](search.md)のデフォルト実装ではこの構文が使用されます。実験するには、 [http://localhost:4503/content/community-components/en/search.html](http://localhost:4503/content/community-components/en/search.html).

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

[AEM Communities SRP ツール](https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools)

このリポジトリには、SRP のデータを管理するためのツールが格納されています。

現在、任意の SRP からすべての UGC を削除できるサーブレットが 1 つ用意されています。

次に、ASRP からすべての UGC を削除する場合の例を示します。

```shell
curl -X POST http://localhost:4502/services/social/srp/cleanup?path=/content/usergenerated/asi/cloud -uadmin:admin
```

## トラブルシューティング {#troubleshooting}

### Solr クエリ {#solr-query}

Solr クエリに関する問題のトラブルシューティングに役立つように、

`com.adobe.cq.social.srp.impl.SocialSolrConnector`

実際の Solr クエリが、デバッグログに URL エンコードされて表示されます。

solr に対するクエリ： `sort=timestamp+desc&bl=en&pl=en&start=0&rows=10 &q=%2Btitle_t:(hello)+%2Bprovider_id:\/content/usergenerated/asi/mongo/content/+%2Bresource_type_s:&df=provider_id&trf=verbatim&fq={!cost%3D100}report_suite:mongo`

`q` パラメーターの値がクエリです。URL エンコーディングがデコードされたら、クエリを Solr 管理クエリツールに渡して、さらにデバッグできます。

## 関連リソース {#related-resources}

* [コミュニティコンテンツストレージ](working-with-srp.md) - UGC 共通ストアで使用可能な SRP の選択肢について説明します。
* [ストレージリソースプロバイダの概要](srp.md)  — の概要とリポジトリの使用の概要。
* [SRP を使用した UGC へのアクセス](accessing-ugc-with-srp.md)  — コーディングのガイドライン。
* [SocialUtils リファクタリング](socialutils.md) - SocialUtils に代わる SRP のユーティリティメソッド。
* [検索および検索結果のコンポーネント](search.md)  — テンプレートに UGC 検索機能を追加します。
