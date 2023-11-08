---
title: GraphQL クエリの最適化
description: ヘッドレスコンテンツ配信のためにAdobe Experience Manager as a Cloud Serviceでコンテンツフラグメントをフィルタリング、ページング、並べ替える際に、GraphQLクエリを最適化する方法について説明します。
exl-id: 47d0570b-224e-4109-b94e-ccc369d7ac5f
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '1964'
ht-degree: 61%

---

# GraphQLクエリの最適化 {#optimizing-graphql-queries}

>[!NOTE]
>
>これらの最適化レコメンデーションを適用する前に、以下を検討してください。 [GraphQLフィルタリングでのページングと並べ替えのためのコンテンツフラグメントの更新](/help/sites-developing/headless/graphql-api/graphql-optimized-filtering-content-update.md) 最高のパフォーマンスを実現するには：

これらのガイドラインは、GraphQLクエリでのパフォーマンスの問題を防ぐために提供されています。

## GraphQLチェックリスト {#graphql-checklist}

次のチェックリストは、Adobe Experience Manager(AEM)as a Cloud ServiceのGraphQLの設定と使用を最適化するためのものです。

### 第 1 原則 {#first-principles}

#### 永続的なGraphQLクエリを使用 {#use-persisted-graphql-queries}

**レコメンデーション**

永続化されたGraphQLクエリの使用を強くお勧めします。

永続的なGraphQLクエリは、コンテンツ配信ネットワーク (CDN) を利用して、クエリの実行パフォーマンスを低減するのに役立ちます。 クライアントアプリケーションは、高速なエッジ対応の実行を実現するために、GETリクエストを使用して永続化されたクエリをリクエストします。

**その他の参照**

以下を参照してください。

* [永続的な GraphQL クエリ](/help/sites-developing/headless/graphql-api/persisted-queries.md).
* [AEM での GraphQL の使用方法 - サンプルコンテンツとサンプルクエリ](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md)

#### GraphQL Index パッケージのインストール {#install-graphql-index-package}

**レコメンデーション**

GraphQLを使用するお客様 *必須* GraphQLインデックスパッケージを使用してExperience Managerコンテンツフラグメントをインストールします。 これにより、実際に使用する機能に基づいて、必要なインデックス定義を追加できます。このパッケージをインストールしないと、GraphQL クエリが遅くなったり失敗したりする場合があります。

お使いの Service Pack に適したバージョンについては、リリースノートを参照してください。 例えば、最新の Service Pack については、 [Experience Managerコンテンツフラグメント用のGraphQLインデックスパッケージのインストール](/help/release-notes/release-notes.md#install-aem-graphql-index-add-on-package) .

>[!NOTE]
>
>このパッケージは、インスタンスごとに 1 度だけインストールします。サービスパックごとに再インストールする必要はありません。

**その他の参照**
以下を参照してください。

* [Experience Manager コンテンツフラグメント用の GraphQL インデックスパッケージのインストール](/help/release-notes/release-notes.md#install-aem-graphql-index-add-on-package)

### キャッシュ方法 {#cache-strategy}

キャッシュの様々な方法を最適化に使用することもできます。

#### AEM Dispatcher のキャッシュの有効化 {#enable-aem-dispatcher-caching}

**レコメンデーション**

[AEM Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=ja) は、AEMサービス内の、CDN キャッシュの前の第 1 レベルのキャッシュです。

**その他の参照**

以下を参照してください。

* [GraphQLの永続クエリ — Dispatcher でのキャッシュの有効化](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#graphql-persisted-queries-enabling-caching-dispatcher)

#### コンテンツ配信ネットワーク (CDN) の使用 {#use-cdn}

**レコメンデーション**

GraphQLクエリとその JSON 応答は、をターゲット設定した場合はキャッシュできます `GET` リクエストを送信する必要があります。 これに対し、キャッシュされていないリクエストは、（リソース）非常に高コストで処理に時間がかかる場合があり、元のリソースにさらに悪影響を及ぼす可能性があります。

**その他の参照**

以下を参照してください。

* [AEMでの CDN の使用](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=ja#using-dispatcher-with-a-cdn)

#### HTTP キャッシュ制御ヘッダーの設定 {#set-http-cache-control-headers}

**レコメンデーション**

永続化されたGraphQLクエリを CDN で使用する場合は、適切な HTTP キャッシュ制御ヘッダーを設定することをお勧めします。

永続化された各クエリには、独自のキャッシュ制御ヘッダーのセットを設定できます。 ヘッダーは、 [GraphQL API](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md).

また、 **cURL** コマンドラインツールを使用します。 例えば、 `PUT` キャッシュコントロールを使用してラップされたプレーンクエリを作成するリクエストです。

```shell
$ curl -X PUT \
    -H 'authorization: Basic YWRtaW46YWRtaW4=' \
    -H "Content-Type: application/json" \
    "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
    -d \
'{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
```

<!-- or the [AEM GraphiQL IDE](/help/sites-developing/headless/graphql-api/graphiql-ide.md#managing-cache). 
-->

**その他の参照**

以下を参照してください。

* [永続クエリのキャッシュ](/help/sites-developing/headless/graphql-api/persisted-queries.md#caching-persisted-queries)
* [GraphQL クエリを永続化する方法](/help/sites-developing/headless/graphql-api/persisted-queries.md#how-to-persist-query)
<!--
* [Managing cache for your persisted queries](/help/sites-developing/headless/graphql-api/graphiql-ide.md#managing-cache)
-->

<!--
#### Use AEM GraphQL pre-caching {#use-aem-graphql-pre-caching}

**Recommendation**

This capability allows AEM to further cache content within the scope of GraphQL queries that can then be assembled as blocks in JSON output rather than line by line. 

**Further Reference**

Contact Adobe to enable this capability for your AEM Cloud Service program and environments. 
-->

### GraphQL Query optimization {#graphql-query-optimization}

同じモデルを共有するコンテンツフラグメントが多数ある AEM インスタンスでは、GraphQL のリストクエリに（リソースの点で）コストがかかる場合があります。

これは、GraphQL クエリ内で使用されているモデルを共有する&#x200B;*すべての*&#x200B;フラグメントを、メモリに読み込む必要があるためです。これは時間とメモリの両方を消費します。 結果セット全体をメモリに読み込んだ&#x200B;**後に**&#x200B;のみ、（最終的な）結果セット内の項目数を減らす可能性のあるフィルタリングを適用できます。

これにより、小さな結果セットでもパフォーマンスが低下するというインプレッションを与える可能性があります。ただし、実際には、フィルタリングを適用する前に内部で処理する必要があるので、初期結果セットのサイズが原因で速度が低下します。

パフォーマンスとメモリの問題を減らすには、この初期結果セットをできるだけ小さく保つ必要があります。

AEM には、GraphQL クエリを最適化する 2 つの方法があります。

* [ハイブリッドフィルタリング](#use-aem-graphql-hybrid-filtering)
* [ページング](#use-aem-graphql-pagination)（またはページネーション）

   * [並べ替え](#use-graphql-sorting)は、最適化に直接関連していませんが、ページングに関連しています

各アプローチには、独自のユースケースと制限があります。 この節では、ハイブリッドフィルターとページングに関する情報と、 [ベストプラクティス](#best-practices) GraphQLクエリの最適化に使用する

#### AEM GraphQLハイブリッドフィルタリングの使用 {#use-aem-graphql-hybrid-filtering}

**レコメンデーション**

ハイブリッドフィルタリングは、JCR フィルタリングと AEM フィルタリングを組み合わせます。

結果セットを AEM フィルタリング用のメモリに読み込む前に、（クエリ制約の形式で）JCR フィルターを適用します。 これは、JCR フィルターによって余分な結果が先に削除されるので、メモリに読み込まれる結果セットを減らすためです。

>[!NOTE]
>
>技術的な理由（柔軟性、フラグメントのネストなど）により、AEM はフィルタリング全体を JCR に委任できません。

この方法では、GraphQL フィルターが提供する柔軟性を維持しながら、可能な限り多くのフィルタリングを JCR に委任できます。

>[!NOTE]
>
>AEM Hybrid Filtering を使用するには、既存のコンテンツフラグメントを更新する必要があります

**その他の参照**

以下を参照してください。

* [GraphQLフィルタリングでのページングと並べ替えのためのコンテンツフラグメントの更新](/help/sites-developing/headless/graphql-api/graphql-optimized-filtering-content-update.md)
* [_tags ID でフィルタリングされた、バリエーションを含まないサンプルクエリ](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-filtering-tag-not-variations)

#### GraphQLのページネーションを使用 {#use-aem-graphql-pagination}

**レコメンデーション**

大きな結果セットを持つ複雑なクエリの応答時間は、GraphQL標準のページネーションを使用して応答をチャンクにセグメント化することで、改善できます。

AEMのGraphQLは、次の 2 種類のページネーションをサポートしています。

* [制限/オフセットベースのページネーション](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#list-offset-limit)
これはリストクエリに使用され、次で終わります。 `List`例： `articleList`.
これを使用するには、最初に返す項目（`offset`）と返す項目の数（`limit` またはページサイズ）を指定する必要があります。

* [カーソルベースのページネーション](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#paginated-first-after)（`first` および `after` で表される）
これにより、項目ごとに一意の ID が提供されます。「カーソル」とも呼ばれます。
クエリでは、前のページの最後の項目のカーソルとページサイズ（返される項目の最大数）を指定します。

  カーソルベースのページネーションはリストベースのクエリのデータ構造内に収まらないので、AEM では `Paginated` クエリタイプ（例： `articlePaginated`）を導入しました。 使用するデータ構造とパラメーターは、[GraphQL Cursor ConnectionSpecification](https://relay.dev/graphql/connections.htm) に準拠します。

  >[!NOTE]
  >
  >AEM は現在、前方ページングをサポートしています（`after`/`first` パラメーターを使用）。
  >
  >後方ページング（`before`/`last` パラメーターを使用）はサポートされていません。

**その他の参照**

以下を参照してください。

* [first と after を使用したサンプルページネーションクエリ](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-pagination-first-after)

#### GraphQLの並べ替えを使用 {#use-graphql-sorting}

**レコメンデーション**

また、GraphQL標準の並べ替え機能を使用すると、クライアントは JSON コンテンツを並べ替えられた順序で受け取ることができます。 これにより、クライアント上でさらに処理する必要が減少します。

並べ替えは、すべての並べ替え条件が最上位のフラグメントに関連している場合にのみ効率的です。

並べ替え順に、ネストされたフラグメントに配置された 1 つ以上のフィールドが含まれている場合、最上位モデルを共有するすべてのフラグメントをメモリに読み込む必要があります。 これにより、パフォーマンスが低下します。

>[!NOTE]
>
>最上位フィールドでの並べ替えも、（小さくても）パフォーマンスに影響を与えます。

**その他の参照**

以下を参照してください。

* [_tags ID でフィルタリングし、バリエーションを除外し、名前で並べ替えるクエリ例](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-filtering-tag-not-variations)

## ベストプラクティス {#best-practices}

すべての最適化レコメンデーションの主な目的は、初期結果セットを減らすことです。 ここに示すベストプラクティスで、その方法を説明します。 組み合わせることができます（推奨）。

### 最上位のプロパティのみをフィルター {#filter-top-level-properties-only}

現在、JCR レベルでのフィルタリングは、最上位のフラグメントに対してのみ機能します。

フィルターがネストされたフラグメントのフィールドに対応する場合、AEM はフォールバックして、基になるモデルを共有するすべてのフラグメントを（メモリに）読み込む必要があります。

最上位のフラグメントのフィールドとネストされたフラグメントのフィールドのフィルター式を、[AND 演算子](#logical-operations-in-filter-expressions)と組み合わせることで、このような GraphQL クエリを引き続き最適化できます。

### コンテンツ構造の使用 {#use-content-structure}

AEM では、通常、リポジトリ構造を使用して、処理するコンテンツの範囲を絞り込むことをお勧めします。

この方法は、GraphQL クエリにも適用する必要があります。

これを実行するには、最上位フラグメントの `_path` フィールドにフィルターを適用します。

```graphql
{
  someList(filter: {
    _path: {
      _expressions: [ 
        {
          value: "/content/dam/some/sub/path/",
          _operator: STARTS_WITH
        }
      ]
    }
  }) {
    items {
      # ...
    }
  }
}
```

>[!NOTE]
>
>最高のパフォーマンスを得るには、`value` の末尾に `/` を付ける必要があります。

### ページングの使用 {#use-paging}

ページングを使用して、初期の結果セットを減らすこともできます（特に、リクエストでフィルタリングと並べ替えを使用しない場合）。

ネストされたフラグメントをフィルターまたは並べ替える場合でも、AEM は大量のフラグメントをメモリに読み込む必要があるので、ページ分割されたクエリの処理に時間がかかる場合があります。 したがって、フィルタリングとページングを組み合わせる場合は、（前述のように）フィルタリングのルールを考慮してください。

ページングの場合、ページ分割された結果が常に明示的または暗黙的に並べ替えられるので、並べ替えも同様に重要です。

最初の数ページのみを取得したい場合、`...List` クエリと `...Paginated` クエリの使用に大きな違いはありません。 ただし、アプリケーションで 1～2 ページ以上のページを読みたい場合は、`...Paginated` クエリを使用することをお勧めします。後のページで、パフォーマンスが著しく向上します。

### フィルター式の論理演算 {#logical-operations-in-filter-expressions}

ネストされたフラグメントをフィルタリングする場合でも、`AND` 演算子を使用して組み合わされた最上位フィールドに付随するフィルターを提供して、JCR フィルタリングを適用できます。

一般的なユースケースは、最上位フラグメントの `_path` フィールドでフィルターを使用してクエリの範囲を制限し、最上位またはネストされたフラグメント上の追加フィールドでフィルタリングすることです。

この場合、様々なフィルター式が `AND` で組み合わされます。したがって、`_path` のフィルターにより、初期の結果セットが効果的に制限されます。 最上位フィールドのその他すべてのフィルターも、`AND` で組み合わせた場合を除き、初期結果セットを減らすのに役立ちます。

ネストされたフラグメントが含まれている場合、`OR` で組み合わされたフィルター式を最適化できません。`OR` 式は、ネストされたフラグメントが含まれて&#x200B;*いない*&#x200B;場合にのみ最適化できます。

### 複数行のテキストフィールドに対するフィルタリングの回避 {#avoid-filtering-multiline-textfields}

複数行のテキストフィールド（html、markdown、plaintext、json）のフィールドは、JCR クエリでフィルタリングできません。これらのフィールドの内容をその場で計算する必要があるからです。

それでも複数行のテキストフィールドに対してフィルタリングする必要がある場合は、フィルター式を追加して、初期の結果セットのサイズを制限し、`AND` と組み合わせることを検討してください。`_path` フィールドに対してフィルタリングして範囲を制限することも、適切なアプローチです。

### 仮想フィールドに対するフィルタリングの回避 {#avoid-filtering-virtual-fields}

仮想フィールド（`_` で始まるほとんどのフィールド）は、GraphQL クエリの実行中に計算されるので、JCR ベースのフィルタリングの範囲外です。

重要な例外は `_path` フィールです。コンテンツが適切に構造化されている場合は、初期結果セットのサイズを効果的に削減するために使用できます（[コンテンツ構造の使用](#use-content-structure)を参照）。

### ：フィルタリング除外 {#filtering-exclusions}

JCR レベルでフィルター式を評価できない場合が他にもいくつかあります（したがって、最高のパフォーマンスを実現するには回避する必要があります）。

* `_sensitiveness` フィルターオプションを使用し、`_sensitiveness` が `0.0` 以外に設定されている `Float` 値の式をフィルタリングします。

* `_ignoreCase` フィルターオプションを使用して、`String` 値の式をフィルタリングします。

* `null` 値のフィルタリング。

* `_apply: ALL_OR_EMPTY` を使用して配列をフィルタリングします。

* `_apply: INSTANCES`、`_instances: 0` を使用して配列をフィルタリングします。

* `CONTAINS_NOT` 演算子を使用して式をフィルタリングします。 

* `NOT_AT` 演算子を使用する `Calendar`、`Date` または `Time` 値の式をフィルタリングします。

### コンテンツフラグメントのネストを最小化 {#minimize-content-fragment-nesting}

コンテンツフラグメントのネストは、カスタムコンテンツ構造をモデル化する優れた方法です。 ネストされたフラグメントを持つフラグメント（ネストされたフラグメントを持つ、など）を持つこともできます。

ただし、レベルが多すぎる構造を作成すると、GraphQLはネストされたすべてのコンテンツフラグメントの階層全体をトラバースする必要があるので、GraphQLクエリの処理時間が長くなる可能性があります。

深いネストは、コンテンツガバナンスに悪影響を与える可能性もあります。 一般に、コンテンツフラグメントのネストは、5 レベルまたは 6 レベル未満に制限することをお勧めします。

### すべてのフォーマットを出力しない（複数行テキスト要素） {#do-not-output-all-formats}

AEM GraphQLは、 **[複数行テキスト](/help/assets/content-fragments/content-fragments-models.md#data-types)** 複数の形式のデータタイプ：リッチテキスト、シンプルテキスト、Markdown。

3 つの形式をすべて出力すると、JSON で出力されるテキストのサイズが約 3 倍になります。 これを、非常に広範なクエリからの一般的に大きな結果セットと組み合わせると、非常に大きな JSON 応答が生成されるので、計算に長い時間がかかる場合があります。 コンテンツのレンダリングに必要なテキスト形式のみに出力を制限することをお勧めします。

### コンテンツフラグメントの変更 {#modifying-content-fragments}

AEM UI または API を使用して、コンテンツフラグメントとそのリソースのみを変更します。 JCR で直接変更を行わないでください。

### クエリのテスト {#test-your-queries}

GraphQLクエリの処理は検索クエリの処理と似ており、単純なGETオールコンテンツ API リクエストよりも大幅に複雑です。

管理対象の非実稼動環境でクエリを慎重に計画、テスト、最適化することが、後で実稼動環境で使用する際に成功するための鍵となります。
