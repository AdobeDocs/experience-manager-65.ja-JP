---
title: 検索の基本事項
description: AEM Communitiesの重要な機能である検索機能について説明します。 Communities には、ユーザー作成コンテンツ用の検索 API も用意されています。
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 8af5ee58-19d7-47b6-b45d-e88006703a5d
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 5%

---

# 検索の基本事項 {#search-essentials}

## 概要 {#overview}

検索機能は、Adobe Experience Manager（AEM） Communities の重要な機能です。 に加えて [AEM platform 検索](../../help/sites-deploying/queries-and-indexing.md) AEM Communitiesが提供する機能 [UGC 検索 API](#ugc-search-api) ユーザー生成コンテンツ（UGC）を検索します。 UGC には、他のAEM コンテンツやユーザーデータとは別に入力および保存される一意のプロパティがあります。

Communities の場合、一般的に検索される 2 つの項目は次のとおりです。

* コミュニティメンバーが投稿したコンテンツ

   * AEM Communitiesの UGC 検索 API を使用します。

* ユーザーとユーザーグループ（ユーザーデータ）

   * AEM プラットフォームの検索機能を使用します。

この節のドキュメントは、UGC を作成または管理するカスタムコンポーネントを作成する開発者が関心を持つものです。

## セキュリティ・ノードとシャドウ・ノード {#security-and-shadow-nodes}

カスタムコンポーネントでは、 [SocialResourceUtilities](socialutils.md#socialresourceutilities-package) メソッド。 UGC を作成して検索するユーティリティメソッドによって、必要な [シャドウ ノード](srp.md#about-shadow-nodes-in-jcr) メンバーがリクエストに対する正しい権限を持っていることを確認します。

SRP ユーティリティで管理されないものは、モデレートに関連するプロパティです。

参照： [SRP と UGC の基本事項](srp-and-ugc.md) ugc および ACL シャドウノードへのアクセスに使用されるユーティリティメソッドについて説明します。

## UGC Search API {#ugc-search-api}

この [UGC 共通ストア](working-with-srp.md) は、様々なストレージリソースプロバイダー（SRP）の 1 つによって提供され、それぞれが異なるネイティブクエリ言語を持つ可能性があります。 したがって、選択した SRP に関係なく、カスタムコードは以下のメソッドを使用する必要があります。 [UGC API パッケージ](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/ugc/api/package-summary.html) （*com.adobe.cq.social.ugc.api*）に設定します。これにより、選択した SRP に適したクエリ言語が呼び出されます。

### ASRP 検索 {#asrp-searches}

の場合 [ASRP](asrp.md)を選択すると、UGC はAdobeクラウドに保存されます。 UGC は CRX には表示されませんが、 [中和](moderate-ugc.md) は、オーサー環境とパブリッシュ環境の両方から利用できます。 の使用 [UGC 検索 API](#ugc-search-api) asrp に対しては、他の SRP に対するのと同じように機能します。

ASRP 検索を管理するツールは現在存在しません。

検索可能なカスタムプロパティを作成する場合は、に従う必要があります。 [命名要件](#naming-of-custom-properties).

### MSRP 検索 {#msrp-searches}

の場合 [MSRP](msrp.md)を指定すると、UGC は Solr を使用して検索するように設定された MongoDB に保存されます。 UGC は CRX では表示されませんが、 [中和](moderate-ugc.md) は、オーサー環境とパブリッシュ環境の両方から利用できます。

MSRP および Solr について：

* AEM プラットフォーム用の埋め込み Solr は、MSRP には使用されません。
* AEM プラットフォームにリモート Solr を使用している場合、MSRP と共有される可能性がありますが、異なるコレクションを使用する必要があります。
* Solr は、標準検索または多言語検索（MLS）用に設定できます。
* 設定について詳しくは、を参照してください [Solr 設定](msrp.md#solr-configuration) （MSRP の場合）

カスタム検索機能では、 [UGC 検索 API](#ugc-search-api).

検索可能なカスタムプロパティを作成する場合は、に従う必要があります。 [命名要件](#naming-of-custom-properties).

### JSRP 検索 {#jsrp-searches}

の場合 [JSRP](jsrp.md)、UGC はに保存されます。 [Oak](../../help/sites-deploying/platform.md) およびは、入力されたAEM オーサーインスタンスまたはパブリッシュインスタンスのリポジトリでのみ表示されます。

UGC は通常パブリッシュ環境で入力されるので、マルチパブリッシャーの実稼働システムの場合は、を設定する必要があります [クラスターの公開](topologies.md)はパブリッシュファームではないので、入力したコンテンツはすべてのパブリッシャーから表示されます。

JSRP の場合、パブリッシュ環境で入力された UGC は、オーサー環境では表示されません。 したがって、すべて [中和](moderate-ugc.md) タスクは、パブリッシュ環境で実行されます。

カスタム検索機能では、 [UGC 検索 API](#ugc-search-api).

#### Oak インデックス作成 {#oak-indexing}

AEM 6.2 以降、AEM プラットフォームの検索用に Oak インデックスが自動的に作成されることはありませんが、UGC 検索結果を表示する際のパフォーマンスの向上やページネーションのサポートを目的として、AEM Communities用に追加されています。

カスタムプロパティが使用中で検索が遅い場合は、カスタムプロパティのパフォーマンスを高めるために、カスタムプロパティに追加のインデックスを作成する必要があります。 移植性を維持するには、 [命名要件](#naming-of-custom-properties) 検索可能なカスタムプロパティを作成する場合

既存のインデックスを変更する、またはカスタムインデックスを作成するには、を参照してください。 [Oak クエリとインデックス作成](../../help/sites-deploying/queries-and-indexing.md).

この [Oak インデックスマネージャー](https://adobe-consulting-services.github.io/acs-aem-commons/features/oak-index-manager.html) は、ACS AEM Commons から入手できます。 これには次の機能があります。

* 既存のインデックスのビュー。
* インデックス再作成機能。

で既存の Oak インデックスを表示するには、次の手順を実行します [CRXDE Lite](../../help/sites-developing/developing-with-crxde-lite.md)の場所はです。

* `/oak:index/socialLucene`

![社会的ルセン](assets/social-lucene.png)

## インデックス付き検索プロパティ {#indexed-search-properties}

### 既定の検索プロパティ {#default-search-properties}

様々な Communities 機能で使用される検索可能なプロパティの一部を次に示します。

| **プロパティ** | **データタイプ** |
|---|---|
| isFlaged | *ブーリアン* |
| isSpam | *ブーリアン* |
| 読み取り | *ブーリアン* |
| 影響力 | *ブーリアン* |
| attachments | *ブーリアン* |
| 感情 | *ロング* |
| フラグあり | *ブーリアン* |
| 追加済み | *日付* |
| modifiedDate | *日付* |
| ステート | *文字列* |
| userIdentifier | *文字列* |
| 返信 | *ロング* |
| jcr:title | *文字列* |
| jcr:description | *文字列* |
| sling:resourceType | *文字列* |
| allowThreadedReply | *ブーリアン* |
| isDraft | *ブーリアン* |
| publishDate | *日付* |
| publishJobId | *文字列* |
| 回答済み | *ブーリアン* |
| chosenanswered | *ブーリアン* |
| タグ | *文字列* |
| cq:Tag | *文字列* |
| author_display_name | *文字列* |
| location_t | *文字列* |
| parentPath | *文字列* |
| parentTitle | *文字列* |

### カスタムプロパティの命名 {#naming-of-custom-properties}

カスタムプロパティを追加する場合、で作成した並べ替えと検索でこれらのプロパティが表示されるようにするには [UGC 検索 API](#ugc-search-api)。です *必須* プロパティ名にサフィックスを追加する場合は、をクリックします。

サフィックスは、スキーマを使用するクエリ言語用です。

* プロパティが検索可能として識別されます。
* データタイプを識別します。

Solr は、スキーマを使用するクエリ言語の例です。

| **接尾辞** | **データタイプ** |
|---|---|
| _b | *ブーリアン* |
| _dt | *カレンダー* |
| _d | *ダブル* |
| _tl | *ロング* |
| _s | *文字列* |
| _t | *テキスト* |

**メモ：**

* *テキスト* はトークン化された文字列で、 *文字列* 等しくない。 使用方法 *テキスト* あいまい検索（これに近い）に使用します。

* 複数の値を持つ型の場合、サフィックスに「s」を追加します。次に例を示します。

   * `viewDate_dt`：単一の日付プロパティ
   * `viewDates_dts`：日付プロパティのリスト

## フィルター {#filters}

コンポーネント（を含む） [コメントシステム](essentials-comments.md)は、エンドポイントに加えてフィルターパラメーターもサポートしています。

AND および OR 論理のフィルター構文は、次のように表されます（URL エンコードされる前に示されます）。

* コンマ区切り値を持つ 1 つのフィルターパラメーターを指定または使用するには：

   * `filter=name eq 'Jennifer',name eq 'Jen'`

* 複数のフィルターパラメーターを指定して使用するには：

   * `filter = name eq 'Jackson'&filter=message eq 'testing'`

のデフォルトの実装 [検索コンポーネント](search.md) では、次の検索結果ページを開く URL に見られるように、この構文を使用します [コミュニティコンポーネントガイド](components-guide.md). 実験するには、を参照してください。 [http://localhost:4503/content/community-components/en/search.html](http://localhost:4503/content/community-components/en/search.html).

フィルター演算子は次のとおりです。

| EQ | が次の値と等しい |
|---|---|
| 新 | 次と等しくない |
| LT | より小さい |
| LTE | 次よりも小さいか等しい |
| GE | 次の値より大きい |
| GTE | 次よりも大きいか等しい |
| いいね！ | あいまい一致 |

コンポーネントが配置されているページではなく、URL が Communities コンポーネント（リソース）を参照することが重要です。

* 正しい形式：フォーラムコンポーネント
   * `/content/community-components/en/forum/jcr:content/content/forum.social.json`
* 間違った形式：フォーラムページ
   * `/content/community-components/en/forum.social.json`

## SRP ツール {#srp-tools}

次を含むAdobe Experience Cloud GitHub プロジェクトがあります。

[AEM Communities SRP ツール](https://github.com/Adobe-Marketing-Cloud/aem-communities-srp-tools)

このリポジトリには、SRP のデータを管理するためのツールが含まれています。

現在、任意の SRP からすべての UGC を削除できるサーブレットが 1 つあります。

例えば、ASRP のすべての UGC を削除するには、次のようにします。

```shell
curl -X POST http://localhost:4502/services/social/srp/cleanup?path=/content/usergenerated/asi/cloud -uadmin:admin
```

## トラブルシューティング {#troubleshooting}

### Solr クエリ {#solr-query}

Solr クエリの問題のトラブルシューティングに役立てるには、のデバッグログを有効にします。

`com.adobe.cq.social.srp.impl.SocialSolrConnector`。

実際の Solr クエリは、デバッグログにエンコードされた URL で表示されます。

solr に対するクエリは次のとおりです。 `sort=timestamp+desc&bl=en&pl=en&start=0&rows=10 &q=%2Btitle_t:(hello)+%2Bprovider_id:\/content/usergenerated/asi/mongo/content/+%2Bresource_type_s:&df=provider_id&trf=verbatim&fq={!cost%3D100}report_suite:mongo`

の値 `q` パラメーターはクエリです。 URL エンコーディングがデコードされると、クエリを Solr Admin Query ツールに渡して、さらにデバッグできるようになります。

## 関連リソース {#related-resources}

* [コミュニティコンテンツストレージ](working-with-srp.md) - UGC 共通ストアで使用可能な SRP の選択肢について説明します。
* [ストレージリソースプロバイダーの概要](srp.md)  – 概要とリポジトリ使用状況の概要。
* [SRP による UGC へのアクセス](accessing-ugc-with-srp.md) - コーディングガイドライン
* [SocialUtils のリファクタリング](socialutils.md) - SocialUtils に代わる SRP のユーティリティメソッド。
* [検索および検索結果のコンポーネント](search.md) - テンプレートへの UGC 検索機能の追加
