---
title: 処理に時間のかかるクエリのトラブルシューティング
description: Adobe Experience Manager での処理に時間のかかるクエリのトラブルシューティング方法について説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 3405cdd3-3d1b-414d-9931-b7d7b63f0a6f
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '2237'
ht-degree: 94%

---

# 処理に時間のかかるクエリのトラブルシューティング{#troubleshooting-slow-queries}

## 処理に時間のかかるクエリの分類 {#slow-query-classifications}

AEM で処理に時間のかかるクエリは、主に以下の 3 つに分類されます（重要度の高い潤）。

1. **インデックスのないクエリ**

   * インデックスに解決&#x200B;**されず**、結果を収集するために JCR のコンテンツをトラバースするクエリ

1. **制限（範囲指定）が不十分なクエリ**

   * インデックスには解決されるが、結果を収集するためにすべてのインデックスエントリをトラバースする必要があるクエリ

1. **結果セットが大きいクエリ**

   * 多くの結果を返すクエリ

最初の 2 つの分類のクエリ（インデックスのないクエリと制限が不十分なクエリ）の処理に時間がかかります。時間がかかるのは、Oak クエリエンジンが強制的に結果&#x200B;**候補**（コンテンツノードやインデックスエントリ）それぞれを調査し、どれが&#x200B;**実際**&#x200B;の結果セットに属しているかを特定するからです。

各結果候補を調査する動作をトラバースと呼びます。

それぞれの結果候補を調査する必要があるため、実際の結果セットを決定するためのコストは、結果候補の数に比例して増加します。

クエリの制限を追加し、インデックスを調整すると、結果を迅速に取得できるように最適化された形式でインデックスデータを格納できます。また、結果候補セットを順次調査する必要性が低減するかなくなります。

AEM 6.3 では、デフォルトでトラバースの回数が 100,000 回に達すると、クエリが失敗し、例外がスローされます。この制限は、AEM 6.3 より前のバージョンの AEM ではデフォルトで存在しません。ただし、Apache Jackrabbit クエリエンジン設定の OSGi 設定および QueryEngineSettings JMX bean（LimitReads プロパティ）で設定できます。

### インデックスのないクエリの検出 {#detecting-index-less-queries}

#### 開発時 {#during-development}

**すべての**&#x200B;クエリの説明を実行し、それらのクエリプランに **/&amp;ast; traverse** が含まれていないことを確認します。トラバースするクエリプランの例は次のとおりです。

* **プラン：** `[nt:unstructured] as [a] /* traverse "/content//*" where ([a].[unindexedProperty] = 'some value') and (isdescendantnode([a], [/content])) */`

#### デプロイメント後 {#post-deployment}

* インデックスのないトラバーサルクエリについて、`error.log` を監視します。

   * `*INFO* org.apache.jackrabbit.oak.query.QueryImpl Traversal query (query without index) ... ; consider creating and index`
   * このメッセージがログに記録されるのは、使用できるインデックスがない場合とクエリが多数のノードをトラバースする可能性がある場合のみです。インデックスが使用可能な場合、メッセージはログに記録されませんが、トラバースの量が少ないので処理にかかる時間は短くなります。

* AEM の[クエリパフォーマンス](/help/sites-administering/operations-dashboard.md#query-performance)操作コンソールに移動し、処理に時間がかかるクエリの[説明](/help/sites-administering/operations-dashboard.md#explain-query)を実行して、トラバーサルまたはインデックスのないクエリの説明を探します。

### 制限が不十分なクエリの検出 {#detecting-poorly-restricted-queries}

#### 開発時 {#during-development-1}

すべてのクエリの説明を実行し、クエリのプロパティ制限に一致するよう調整されたインデックスに解決されることを確認します。

* 理想的なクエリプランの範囲では、すべてのプロパティ制限、および少なくともクエリで最も厳密なプロパティ制限に `indexRules` を持ちます。
* 結果を並べ替えるクエリは、Lucene プロパティインデックスに解決される必要があります。このインデックスには、`orderable=true.` を設定するプロパティによる並べ替えに関するインデックスルールがあります。

#### 例えば、デフォルトの `cqPageLucene` には `jcr:content/cq:tags` に対するインデックスルールがありません。 {#for-example-the-default-cqpagelucene-does-not-have-an-index-rule-for-jcr-content-cq-tags}

cq:tags インデックスルールを追加する前

* **cq:tags インデックスルール**

   * デフォルトでは存在しません。

* **Query Builder クエリ**

  ```js
  type=cq:Page
  property=jcr:content/cq:tags
  property.value=my:tag
  ```

* **クエリプラン**

  `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) *:* where [a].[jcr:content/cq:tags] = 'my:tag' */`

このクエリは `cqPageLucene` インデックスに解決されます。ただし、`jcr:content` または `cq:tags` のプロパティインデックスルールは存在しないので、この制限を評価する際に、`cqPageLucene` インデックス内のすべてのレコードが一致するかどうかを判断するためにチェックされます。つまり、インデックスに 100 万個の `cq:Page` ノードが含まれている場合は、結果セットを特定するために 100 万件のレコードをチェックします。

cq:tags インデックスルールを追加した後

* **cq:tags インデックスルール**

  ```js
  /oak:index/cqPageLucene/indexRules/cq:Page/properties/cqTags
  @name=jcr:content/cq:tags
  @propertyIndex=true
  ```

* **Query Builder クエリ**

  ```js
  type=cq:Page
  property=jcr:content/cq:tags
  property.value=myTagNamespace:myTag
  ```

* **クエリプラン**

  `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) jcr:content/cq:tags:my:tag where [a].[jcr:content/cq:tags] = 'my:tag' */`

`cqPageLucene` インデックスに `jcr:content/cq:tags` のインデックスルールを追加したので、`cq:tags` のデータは最適な方法で格納することができます。

`jcr:content/cq:tags` 制限を持つクエリを実行すると、インデックスは値に従って結果を検索できます。つまり、100 個の `cq:Page` ノードに値として `myTagNamespace:myTag` が設定されている場合は、この 100 件の結果だけが返され、他の 999,000 件は制限チェックから除外されるので、パフォーマンスは 10,000 倍向上します。

さらにクエリを制限すると、対象となる結果セットが少なくなり、クエリはさらに最適化されます。

同様に、`cq:tags` プロパティのインデックスルールを追加しない場合は、`cq:tags` に対する制限を持つフルテキストクエリであっても、インデックスからの結果ではフルテキスト一致がすべて返されるので、パフォーマンスは低下します。その後、cq:tags の制限がフィルタリングされます。

インデックス後にフィルタリングされるもう 1 つの原因は、開発中に見落とされることがよくあるアクセス制御リストです。ユーザーがアクセスできない可能性のあるパスがクエリで返されないようにしてください。これは、より良いコンテンツ構造を実現し、クエリに関連するパス制限を提供することで行うことができます。

`org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex` の DEBUG ログを有効にすると、Lucene インデックスが多数の結果を返して小さなサブセットをクエリ結果として返しているかどうかを識別するのに便利です。これにより、インデックスから読み込まれているドキュメントの数を確認できます。読み込まれるドキュメントの数に対する最終結果の数は、不釣り合いではありません。 詳しくは、[ログ](/help/sites-deploying/configure-logging.md)を参照してください。

#### デプロイメント後 {#post-deployment-1}

* トラバーサルクエリについて、`error.log` を監視します。

   * `*WARN* org.apache.jackrabbit.oak.spi.query.Cursors$TraversingCursor Traversed ### nodes ... consider creating an index or changing the query`

* AEM の[クエリパフォーマンス](/help/sites-administering/operations-dashboard.md#query-performance)操作コンソールに移動し、処理に時間がかかるクエリの[説明](/help/sites-administering/operations-dashboard.md#explain-query)を実行して、クエリプロパティ制限がインデックスプロパティルールに解決されないクエリプランを探します。

### 結果セットが大きいクエリの検出 {#detecting-large-result-set-queries}

#### 開発時 {#during-development-2}

「クエリは x 個を超えるノードを読み取った...」という UnsupportedOperationException が発生する場合は、oak.queryLimitInMemory と oak.queryLimitReads に低いしきい値（例えば、それぞれ 10000 と 5000）を設定して高負荷のクエリを最適化します。

低いしきい値を設定すると、リソースを大量に消費するクエリ（インデックスを使用しないクエリや、対応するインデックスが少ないクエリ）を回避できます。例えば、100 万個のノードを読み取るクエリは大量の IO を引き起こし、アプリケーション全体のパフォーマンスに悪影響を及ぼします。したがって、上記の制限によって失敗したクエリを分析し、最適化する必要があります。

#### デプロイメント後 {#post-deployment-2}

* ログを監視して、大規模なノードの走査やヒープメモリの大量使用を引き起こしているクエリがないかどうかを調べます。

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * クエリを最適化して、走査されるノードの数を減らします。

* 大量のヒープメモリの消費を引き起こすクエリについてログを監視します。

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * クエリを最適化して、ヒープメモリの使用量を減らします。

AEM 6.0 ～ 6.2 では、AEM 起動スクリプトで JVM パラメーターを使用してノードの走査のしきい値を調整することで、大規模なクエリによって環境に過度の負荷がかかるのを防ぐことができます。推奨される値は次のとおりです。

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

AEM 6.3 では、デフォルトで上述の 2 つのパラメーターが事前設定されており、OSGi QueryEngineSettings を使用して変更できます。

詳しくは、[https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits) を参照してください。

## クエリパフォーマンスの調整 {#query-performance-tuning}

AEM でのクエリパフォーマンス最適化のモットーは次のとおりです。

**「制限が多いほどよい。」**

以下に、クエリのパフォーマンスを確保するために推奨される調整の概要を示します。まずクエリ、あまり目立たないアクティビティを調整し、その後必要に応じてインデックス定義を調整します。

### クエリステートメントの調整 {#adjusting-the-query-statement}

AEM では、以下のクエリ言語をサポートしています。

* Query Builder
* JCR-SQL2
* XPath

次の例では、AEM開発者が使用する最も一般的なクエリ言語であるため Query Builder を使用していますが、JCR-SQL2 と XPath にも同じ原則が適用されます。

1. クエリが既存の Lucene プロパティインデックスに解決されるように、ノードタイプの制限を追加します。

* **最適化されていないクエリ**

  ```js
  property=jcr:content/contentType
  property.value=article-page
  ```

* **最適化されたクエリ**

  ```js
  type=cq:Page
  property=jcr:content/contentType
  property.value=article-page
  ```

  ノードタイプの制限がないクエリにより、AEM では `nt:base` ノードタイプが想定されます。これは、AEM のすべてのノードのサブタイプなので、実質上ノードタイプの制限は存在しません。

  `type=cq:Page` を設定すると、このクエリは `cq:Page` ノードのみに限定され、AEM の cqPageLucene に解決されます。これにより、結果は AEM のノードのサブセット（ `cq:Page`ノードのみ）に限定されます。

1. クエリが既存の Lucene プロパティインデックスに解決されるように、クエリのノードタイプの制限を調整します。

* **最適化されていないクエリ**

  ```js
  type=nt:hierarchyNode
  property=jcr:content/contentType
  property.value=article-page
  ```

* **最適化されたクエリ**

  ```js
  type=cq:Page
  property=jcr:content/contentType
  property.value=article-page
  ```

  `nt:hierarchyNode` は、`cq:Page` の親ノードタイプです。アドビのカスタムアプリケーションを通じて `jcr:content/contentType=article-page` が `cq:Page` ノードのみに適用されるとすると、このクエリは、`jcr:content/contentType=article-page` である `cq:Page` ノードのみを返します。これは、以下の理由から、次善策としての制限となります。

   * `nt:hierarchyNode` から継承された他のノード（`dam:Asset` など）が、結果候補のセットに不必要に追加されます。
   * AEM で提供される、`nt:hierarchyNode` 用のインデックスは存在しませんが、`cq:Page` 用に提供されているインデックスはあります。

  `type=cq:Page` を設定すると、このクエリは `cq:Page` ノードのみに限定され、AEM の cqPageLucene に解決されます。これにより、結果は AEM のノードのサブセット（cq:Page ノードのみ）に限定されます。

1. または、クエリが既存のプロパティインデックスに解決されるように、プロパティの制限を調整します。

* **最適化されていないクエリ**

  ```js
  property=jcr:content/contentType
  property.value=article-page
  ```

* **最適化されたクエリ**

  ```js
  property=jcr:content/sling:resourceType
  property.value=my-site/components/structure/article-page
  ```

  プロパティの制限を `jcr:content/contentType`（カスタム値）から既知のプロパティ `sling:resourceType` に変更すると、クエリはプロパティインデックス `slingResourceType` に解決され、`sling:resourceType` によってすべてのコンテンツにインデックスを作成します。

  （Lucene プロパティインデックスではなく）プロパティインデックスの使用が最も適しているのは、クエリがノードタイプを認識せず、単一のプロパティ制限によって結果セットが決まる場合です。

1. クエリに可能な限り厳密なパス制限を追加します。例：`/content/my-site`より`/content/my-site/us/en`が推奨され、また`/`より`/content/dam`が推奨されます。

* **最適化されていないクエリ**

  ```js
  type=cq:Page
  path=/content
  property=jcr:content/contentType
  property.value=article-page
  ```

* **最適化されたクエリ**

  ```js
  type=cq:Page
  path=/content/my-site/us/en
  property=jcr:content/contentType
  property.value=article-page
  ```

  パス制限の範囲を `path=/content` から `path=/content/my-site/us/en` に指定すると、点検が必要なインデックスエントリの数を減らすことができます。単に `/content` や `/content/dam` ではなく、クエリでパスを効果的に制限できる場合は、インデックスに `evaluatePathRestrictions=true` があることを確認します。

  `evaluatePathRestrictions` を使用すると、インデックスのサイズが大きくなります。

1. 可能な場合は、`LIKE` や `fn:XXXX` などのクエリの関数やクエリの操作を避けます（これらのコストは、制限に基づいた結果の数に伴って増減するため）。

* **最適化されていないクエリ**

  ```js
  type=cq:Page
  property=jcr:content/contentType
  property.operation=like
  property.value=%article%
  ```

* **最適化されたクエリ**

  ```js
  type=cq:Page
  fulltext=article
  fulltext.relPath=jcr:content/contentType
  ```

  LIKE 条件の評価には時間がかかります。これは、テキストがワイルドカードで始まる場合（「%...」）はインデックスを使用できないからです。jcr:contains 条件は、フルテキストのインデックスの使用を可能にするので、推奨されています。これには、解決された Lucene プロパティインデックスに、`analayzed=true` に設定した `jcr:content/contentType` のインデックスルールが必要です。

  `fn:lowercase(..)` などのクエリ関数の使用を最適化するのは、（より複雑で目立つインデックス分析設定の外部に）より高速な同等の手段がないので困難です。他の範囲制限を指定し、クエリ全体のパフォーマンスを向上させることをお勧めします。これには、関数の操作対象となる結果候補のセットをできるだけ小さくする必要があります。

1. この調整は、Query Builder 固有であり、JCR-SQL2 または XPath には当てはまりません&#x200B;***。***

   完全な結果セットがすぐに必要で&#x200B;**ない**&#x200B;場合は、[Query Builder の guessTotal](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results) を使用します。

   * **最適化されていないクエリ**

     ```js
     type=cq:Page
     path=/content
     ```

   * **最適化されたクエリ**

     ```js
     type=cq:Page
     path=/content
     p.guessTotal=100
     ```

   クエリの実行時間が短くても結果の数が多い場合、p.`guessTotal` は、Query Builder のクエリにとって必要不可欠な最適化です。

   `p.guessTotal=100` を指定すると、Query Builder は最初の 100 件の結果だけを収集します。さらに、1 つ以上の結果が存在するかどうかを示すブール値フラグを設定します（ただしカウントすると処理に時間がかかるので、残りの数は示されません）。この最適化は、ページネーションまたは無限読み込みのユースケースよりも優れており、結果のサブセットだけが増分的に表示されます。

## 既存のインデックスのチューニング {#existing-index-tuning}

1. 最適なクエリがプロパティインデックスに解決される場合、プロパティインデックスでは最小限のチューニングのみが可能なので、他にすることはありません。
1. できることがある場合、クエリは Lucene プロパティインデックスに解決される必要があります。解決できるインデックスがない場合は、「インデックスの作成」に進んでください。
1. 必要に応じて、クエリを XPath または JCR-SQL2 に変換します。

   * **Query Builder クエリ**

     ```js
     query type=cq:Page
     path=/content/my-site/us/en
     property=jcr:content/contentType
     property.value=article-page
     orderby=@jcr:content/publishDate
     orderby.sort=desc
     ```

   * **Query Builder クエリから生成された XPath**

     ```js
     /jcr:root/content/my-site/us/en//element(*, cq:Page)[jcr:content/@contentType = 'article-page'] order by jcr:content/@publishDate descending
     ```

1. この XPath（または JCR-SQL2）を `https://oakutils.appspot.com/generate/index` で Oak Index Definition Generator に提供して、最適化された Lucene プロパティインデックス定義を生成します。<!-- The above URL is 404 as of April 24, 2023 -->

   **生成された Lucene プロパティインデックス定義**

   ```xml
   - evaluatePathRestrictions = true
   - compatVersion = 2
   - type = "lucene"
   - async = "async"
   - jcr:primaryType = oak:QueryIndexDefinition
       + indexRules
       + cq:Page
           + properties
           + contentType
               - name = "jcr:content/contentType"
               - propertyIndex = true
           + publishDate
               - ordered = true
               - name = "jcr:content/publishDate"
   ```

1. 生成された定義を、追加する形で既存の Lucene プロパティインデックスに手動で結合します。その他のクエリを満たすために使用される可能性があるので、既存の設定を削除しないよう注意してください。

   1. cq:Page を対象とする既存の Lucene プロパティインデックスを探します（インデックスマネージャーを使用）。この場合は、`/oak:index/cqPageLucene`です。
   1. 最適化したインデックス定義（手順 4）と既存のインデックス（/oak:index/cqPageLucene）の設定の差分を特定し、欠けている設定を最適化したインデックスから既存のインデックス定義に追加します。
   1. AEM のインデックス再作成のベストプラクティスにより、このインデックス設定の変更が既存コンテンツに影響するかどうかに基づいて、更新または再インデックス付けのいずれかが必要になります。

## 新しいインデックスを作成 {#create-a-new-index}

1. クエリが既存の Lucene プロパティインデックスに解決されないことを確認します。解決される場合は、前述の既存インデックスのチューニングに関する節を参照してください。
1. 必要に応じて、クエリを XPath または JCR-SQL2 に変換します。

   * **Query Builder クエリ**

     ```js
     type=myApp:Author
     property=firstName
     property.value=ira
     ```

   * **Query Builder クエリから生成された XPath**

     ```js
     //element(*, myApp:Page)[@firstName = 'ira']
     ```

1. この XPath（または JCR-SQL2）を `https://oakutils.appspot.com/generate/index` で Oak Index Definition Generator に提供して、最適化された Lucene プロパティインデックス定義を生成します。<!-- The above URL is 404 as of April 24, 2023 -->

   **生成された Lucene プロパティインデックス定義**

   ```xml
   - compatVersion = 2
   - type = "lucene"
   - async = "async"
   - jcr:primaryType = oak:QueryIndexDefinition
       + indexRules
       + myApp:AuthorModel
           + properties
           + firstName
               - name = "firstName"
               - propertyIndex = true
   ```

1. 生成された Lucene プロパティインデックス定義をデプロイします。

   Oak Index Definition Generator によって新しいインデックスに提供された XML 定義を、Oak インデックス定義を管理する AEM プロジェクトに追加します（コードは Oak インデックス定義に依存するので、これらの定義はコードとして扱うことを忘れないでください）。

   通常の AEM ソフトウェア開発ライフサイクルに従って新しいインデックスをデプロイしてテストし、クエリがインデックスに解決され、効率よく実行されることを確認します。

   このインデックスを初めてデプロイしたときに、AEM によってインデックスに必要なデータが追加されます。

## インデックスがないクエリおよびトラバーサルクエリに問題がない場合 {#when-index-less-and-traversal-queries-are-ok}

AEM のコンテンツアーキテクチャは柔軟です。そのため、コンテンツ構造のトラバーサルが時間の経過と共に受け入れられないほど大きくならないことを予測したり保証したりすることは困難です。

こうした理由から、パス制限とノードタイプ制限の組み合わせによって&#x200B;**トラバースされるノードが 20 個未満**&#x200B;であることが保証される場合を除いて、インデックスがクエリを確実に満たすようにします。

## クエリ開発ツール {#query-development-tools}

### アドビによるサポート {#adobe-supported}

* **Query Builder Debugger**

   * Query Builder クエリを実行するための web UI。対応する XPath（クエリの説明を実行または Oak Index Definition Generator で使用）を生成します。
   * AEM の [/libs/cq/search/content/querydebug.html](http://localhost:4502/libs/cq/search/content/querydebug.html) にあります。

* **CRXDE Lite - クエリツール**

   * XPath および JCR-SQL2 クエリを実行するための web UI。
   * AEM の [/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp)／ツール／クエリにあります。

* **[クエリの説明を実行](/help/sites-administering/operations-dashboard.md#explain-query)**

   * 任意の XPATH または JCR-SQL2 クエリの詳しい説明（クエリプラン、クエリ時間、結果数）が表示される AEM 操作ダッシュボード。

* **[処理に時間のかかるクエリ／一般的なクエリ](/help/sites-administering/operations-dashboard.md#query-performance)**

   * AEM で最近実行された処理に時間のかかるクエリおよび一般的なクエリが一覧表示される AEM 操作ダッシュボード。

* **[インデックスマネージャー](/help/sites-administering/operations-dashboard.md#the-index-manager)**

   * AEM インスタンスのインデックスを表示する AEM 操作 web UI。既存のインデックス、ターゲットにできるインデックス、または増強できるインデックスの把握に役立ちます。

* **[ログ](/help/sites-administering/operations-dashboard.md#log-messages)**

   * Query Builder のログ記録

      * `DEBUG @ com.day.cq.search.impl.builder.QueryImpl`

   * Oak クエリ実行のログ記録

      * `DEBUG @ org.apache.jackrabbit.oak.query`

* **Apache Jackrabbit クエリエンジンの OSGi 設定**

   * トラバースクエリの失敗動作を設定する OSGi 設定。
   * AEM の [/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService](http://localhost:4502/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService) にあります。

* **NodeCounter JMX Mbean**

   * AEM のコンテンツツリーのノード数を推定するのに使用する JMX MBean。
   * AEM の [/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter) にあります。

### コミュニティによるサポート {#community-supported}

* **`https://oakutils.appspot.com/generate/index`** の Oak Index Definition Generator<!-- The above URL is 404 as of April 24, 2023 -->

   * XPath または JCR-SQL2 クエリステートメントから最適な Lucence プロパティインデックスを生成します。

* **_AEM Chrome プラグイン_** <!-- For whatever reason, the URL to this extension was causing too many redirects when doing the request so it was removed entirely to get rid of the error; users can easily look up the extension in Google instead. DO NOT ADD THE URL AGAIN!-->

   * この _AEM Chrome プラグイン_ は、Google Chrome web ブラウザー拡張機能で、実行クエリとそのクエリプランなど、リクエストごとのログデータをブラウザーの開発ツールコンソールに公開します。
   * をインストールして有効にする必要があります [Sling ログトレーサー 1.0.2 以降](https://sling.apache.org/downloads.cgi) （AEM上）。
