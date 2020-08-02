---
title: 処理に時間のかかるクエリのトラブルシューティング
seo-title: 処理に時間のかかるクエリのトラブルシューティング
description: 'null'
seo-description: 'null'
uuid: ad09546a-c049-44b2-99a3-cb74ee68f040
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: c01e42ff-e338-46e6-a961-131ef943ea91
translation-type: tm+mt
source-git-commit: 6d8680bcfb03197ac33bc7efb0e40796e38fef20
workflow-type: tm+mt
source-wordcount: '2267'
ht-degree: 69%

---


# 処理に時間のかかるクエリのトラブルシューティング{#troubleshooting-slow-queries}

## 処理に時間のかかるクエリの分類 {#slow-query-classifications}

AEM で処理に時間のかかるクエリは、主に 3 つに分類されます。以下に重大な順に示します。

1. **インデックスのないクエリ**

   * インデックスに解決&#x200B;**されず**、結果を収集するために JCR のコンテンツをトラバースするクエリ

1. **制限（範囲指定）が不十分なクエリ**

   * インデックスには解決されるが、結果を収集するためにすべてのインデックスエントリをトラバースする必要があるクエリ

1. **結果セットが大きいクエリ**

   * 非常に多くの結果を返すクエリ

The first 2 classifications of queries (index-less and poorly restricted) are slow, because they force the Oak query engine to inspect each **potential** result (content node or index entry) to identify which belong in the **actual** result set.

各結果候補を調査する動作をトラバースと呼びます。

結果候補をそれぞれ調査する必要があるので、実際の結果セットを特定するためのコストは、結果候補の数に比例して増大します。

クエリの制限を追加し、インデックスを調整すると、結果を迅速に取得できるように最適化された形式でインデックスデータを格納できます。また、結果候補セットを順次調査する必要性が低減するかなくなります。

AEM 6.3 では、デフォルトでトラバースの回数が 100,000 回に達すると、クエリが失敗し、例外がスローされます。この制限は、AEM 6.3より前のAEMバージョンではデフォルトで存在しませんが、Apache Jackrabbitクエリエンジン設定OSGi設定およびQueryEngineSettings JMX bean （プロパティLimitReads）を介して設定できます。

### インデックスのないクエリの検出 {#detecting-index-less-queries}

#### 開発時 {#during-development}

Explain **all** queries and ensure their query plans do not contain the **/&amp;ast; traverse** explanation in them. トラバースクエリ計画の例：

* **プラン：** `[nt:unstructured] as [a] /* traverse "/content//*" where ([a].[unindexedProperty] = 'some value') and (isdescendantnode([a], [/content])) */`

#### デプロイメント後 {#post-deployment}

* インデックスのないトラバーサルクエリについて、`error.log` を監視します。

   * `*INFO* org.apache.jackrabbit.oak.query.QueryImpl Traversal query (query without index) ... ; consider creating and index`
   * このメッセージがログに記録されるのは、使用できるインデックスがない場合とクエリが多数のノードをトラバースする可能性がある場合のみです。インデックスが使用可能な場合、メッセージはログに記録されませんが、トラバースの量が少ないので処理にかかる時間は短くなります。

* Visit the AEM [Query Performance](/help/sites-administering/operations-dashboard.md#query-performance) operations console and [Explain](/help/sites-administering/operations-dashboard.md#explain-query) slow queries looking for traversal or no index query explanations.

### 制限が不十分なクエリの検出 {#detecting-poorly-restricted-queries}

#### 開発時 {#during-development-1}

すべてのクエリの説明を実行し、クエリのプロパティ制限に一致するよう調整されたインデックスに解決されることを確認します。

* 理想的なクエリプランの範囲では、すべてのプロパティ制限、および少なくともクエリで最も厳密なプロパティ制限に `indexRules` を持ちます。
* 結果を並べ替えるクエリは、Lucene プロパティインデックスに解決される必要があります。このインデックスには、`orderable=true.` を設定するプロパティによる並べ替えに関するインデックスルールがあります。

#### For example, the default `cqPageLucene` does not have an index rule for `jcr:content/cq:tags` {#for-example-the-default-cqpagelucene-does-not-have-an-index-rule-for-jcr-content-cq-tags}

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

このクエリは `cqPageLucene` インデックスに解決されます。ただし、`jcr:content` または `cq:tags` のプロパティインデックスルールは存在しないので、この制限を評価する際に、`cqPageLucene` インデックス内のすべてのレコードが一致するかどうかを判断するためにチェックされます。つまり、インデックスに 100 万個の `cq:Page` ノードが含まれている場合は、結果セットを特定するために 100 万件のレコードがチェックされます。

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

The addition of the indexRule for `jcr:content/cq:tags` in the `cqPageLucene` index allows `cq:tags` data to be stored in an optimized way.

When a query with the `jcr:content/cq:tags` restriction is performed, the index can look up results by value. つまり、100 個の `cq:Page` ノードに値として `myTagNamespace:myTag` が設定されている場合は、この 100 件の結果だけが返され、他の 999,000 件は制限チェックから除外されるので、パフォーマンスは 10,000 倍向上します。

  当然ながら、さらにクエリを制限すると、対象となる結果セットが少なくなり、クエリはさらに最適化されます。

Similarly, without an additional index rule for the `cq:tags` property, even a fulltext query with a restriction on `cq:tags` would perform poorly as results from the index would return all fulltext matches. cq:tagsに対する制限は、その後フィルタリングされます。

インデックス後にフィルタリングされるもう 1 つの原因は、開発中に見落とされることがよくあるアクセス制御リストです。ユーザーがアクセスできない可能性のあるパスがクエリによって返されていないかどうかを確認してみます。これをおこなうには、通常、コンテキスト構造を改良すると共に、クエリに適切なパス制限を指定します。

A useful way to identify if the Lucene index is returning a lot of results to return a very small subset as query result is to enable DEBUG logs for `org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex` and see how many documents are being loaded from the index. 最終結果の数と読み込まれたドキュメントの数を比較すると釣り合うはずです。詳しくは、[ログ](/help/sites-deploying/configure-logging.md)を参照してください。

#### デプロイメント後 {#post-deployment-1}

* Monitor the `error.log` for traversal queries:

   * `*WARN* org.apache.jackrabbit.oak.spi.query.Cursors$TraversingCursor Traversed ### nodes ... consider creating an index or changing the query`

* Visit the AEM [Query Performance](/help/sites-administering/operations-dashboard.md#query-performance) operations console and [Explain](/help/sites-administering/operations-dashboard.md#explain-query) slow queries looking for query plans that do not resolve query property restrictions to index property rules.

### 結果セットが大きいクエリの検出 {#detecting-large-result-set-queries}

#### 開発時 {#during-development-2}

oak.queryLimitInMemory とoak.queryLimitReads のしきい値を低く設定し（例えば、それぞれ 10000 と 5000）、UnsupportedOperationException にヒットして「The query read more than x nodes...」と表示されたときに高負荷のクエリを最適化します。

これにより、リソースを集中的に使用するクエリ（つまり、インデックスのないクエリまたは対応するインデックスが少ないクエリ）を回避することができます。例えば、100 万個のノードを読み取るクエリでは、大量の IO が発生し、アプリケーション全体のパフォーマンスに悪影響を及ぼします。このため、上述の制限が原因で失敗するクエリは、分析して最適化する必要があります。

#### デプロイメント後 {#post-deployment-2}

* クエリが大きなノードトラバーサルまたは大きなヒープメモリの消費をトリガーしているかどうかログを監視します。 &quot;

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * クエリを最適化して、走査するノードの数を減らします。

* ログを監視して、ヒープメモリを大量に消費しているクエリがないかどうかを調べます。

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * クエリを最適化して、ヒープメモリの使用量を減らします。

AEM 6.0 - 6.2バージョンでは、AEM開始スクリプトのJVMパラメーターを使用してノードトラバーサルのしきい値を調整し、大きなクエリが環境をオーバーロードするのを防ぐことができます。 推奨される値は次のとおりです。

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

AEM 6.3 では、デフォルトで上述の 2 つのパラメーターが事前設定されており、OSGi QueryEngineSettings を使用して変更できます。

More information available under : [https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits)

## クエリパフォーマンスのチューニング {#query-performance-tuning}

AEM におけるクエリパフォーマンス最適化のモットーは次のとおりです。

**「制限は多いほどよい」**

以下に、クエリのパフォーマンスを確保するために推奨される調整の概要を示します。まずクエリ、次にあまり目立たないアクティビティ、その後必要に応じてインデックス定義をチューニングします。

### クエリステートメントの調整 {#adjusting-the-query-statement}

AEM では、以下のクエリ言語がサポートされています。

* Query Builder
* JCR-SQL2
* XPath

以下の例では、AEM 開発者が最もよく使用する Query Builder を使用していますが、JCR-SQL2 および XPath にも同じ原則が当てはまります。

1. クエリが既存の Lucene プロパティインデックスに解決されるようにノードタイプの制限を追加します。

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

   Setting `type=cq:Page` restricts this query to only `cq:Page` nodes, and resolves the query to AEM&#39;s cqPageLucene, limiting the results to a subset of nodes (only `cq:Page` nodes) in AEM.

1. クエリが既存の Lucene プロパティインデックスに解決されるようにクエリのノードタイプの制限を調整します。

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

   `nt:hierarchyNode` はの親ノードタイプ `cq:Page`で、カスタムアプリケーションを介してノードにのみ適用さ `jcr:content/contentType=article-page` れると仮定して、このクエリは、の `cq:Page` ノードのみを返 `cq:Page``jcr:content/contentType=article-page`します。 ただしこれは、以下の理由から、次善策としての制限となります。

   * Other node inherit from `nt:hierarchyNode` (eg. `dam:Asset`)を追加する際に、不必要に結果のセットに追加する必要があります。
   * No AEM-provided index exists for `nt:hierarchyNode`, however as there a provided index for `cq:Page`.
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

   Changing the property restriction from `jcr:content/contentType` (a custom value) to the well known property `sling:resourceType` lets the query to resolve to the property index `slingResourceType` which indexes all content by `sling:resourceType`.

   （Lucene プロパティインデックスではなく）プロパティインデックスの使用が最も適しているのは、クエリがノードタイプを認識せず、単一のプロパティ制限によって結果セットが決まる場合です。

1. クエリに可能な限り厳密なパス制限を追加します。例えば、「上」または「 `/content/my-site/us/en` 上」を選択し `/content/my-site`ま `/content/dam``/`す。

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

   Scoping the path restriction from `path=/content`to `path=/content/my-site/us/en` allows the indexes to reduce the number of index entries that need to be inspected. When the query can restrict the path very well, beyond just `/content` or `/content/dam`, ensure the index has `evaluatePathRestrictions=true`.

   Note using `evaluatePathRestrictions` increases the index size.

1. 可能な場合は、`LIKE` や `fn:XXXX` などのクエリの関数や操作を避けます。これらのコストは、制限に基づいた結果の数に伴って増減するからです。

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

   ワイルドカード(「%...」)を含むテキスト開始の場合は、インデックスを使用できないので、LIKE条件の評価は低速です。 jcr:contains 条件は、フルテキストのインデックスの使用を可能にするので、推奨されています。This requires the resolved Lucene Property Index to have indexRule for `jcr:content/contentType` with `analayzed=true`.

   Using query functions like `fn:lowercase(..)` may be harder to optimize as there are not faster equivalents (outside more complex and obtrusive index analyzer configurations). 他の範囲制限を指定し、クエリ全体のパフォーマンスを向上させることをお勧めします。これには、関数の操作対象となる結果候補のセットをできるだけ小さくする必要があります。

1. この調整は、Query Builder 固有であり、JCR-SQL2 または XPath には当てはまりません。******

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
   For cases where query execution is fast but the number of results are large, p. `guessTotal` is a critical optimization for Query Builder queries.

   `p.guessTotal=100` を指定すると、Query Builder は最初の 100 件の結果だけを収集し、さらに 1 つ以上の結果が存在するかどうかを示すブール値フラグを設定します（ただしカウントすると処理に時間がかかるので、残りの数は示されません）。この最適化は、ページネーションまたは無限ロードの使用例よりも優れており、結果のサブセットだけが増分的に表示されます。

## 既存のインデックスのチューニング {#existing-index-tuning}

1. 最適なクエリがプロパティインデックスに解決される場合、プロパティインデックスで可能なチューニングは最小限なので、できることはありません。
1. それ以外の場合は、クエリはLuceneプロパティインデックスに解決する必要があります。 解決できるインデックスがない場合は、「新しいインデックスの作成」に進んでください。
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

1. この XPath（または JCR-SQL2）を [Oak Index Definition Generator](https://oakutils.appspot.com/generate/index) に提供して、最適化された Lucene プロパティインデックス定義を生成します。

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

1. 生成された定義を既存のLuceneプロパティインデックスに追加方式で手動で結合します。 その他のクエリを満たすために使用される可能性があるので、既存の設定を削除しないよう注意してください。

   1. cq:Page を対象とする既存の Lucene プロパティインデックスを探します（インデックスマネージャーを使用）。In this case, `/oak:index/cqPageLucene`.
   1. 最適化したインデックス定義（手順 4）と既存のインデックス（/oak:index/cqPageLucene）の設定の差分を特定し、欠けている設定を最適化したインデックスから既存のインデックス定義に追加します。
   1. AEM のインデックス再作成のベストプラクティスにより、このインデックス設定の変更が既存コンテンツに影響するかどうかに基づいて、更新または再インデックス付けのいずれかが必要になります。

## Create a New Index {#create-a-new-index}

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

1. この XPath（または JCR-SQL2）を [Oak Index Definition Generator](https://oakutils.appspot.com/generate/index) に提供して、最適化された Lucene プロパティインデックス定義を生成します。

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

## インデックスを使用しないクエリとトラバーサル・システムが正常に動作するのはいつですか。 {#when-index-less-and-traversal-queries-are-ok}

AEM のコンテンツアーキテクチャは柔軟です。そのため、コンテンツ構造のトラバーサルが時間の経過と共に受け入れられないほど大きくならないことを予測したり保証したりすることは困難です。

Therefore, ensure an indexes satisfy queries, except if the combination of path restriction and nodetype restriction guarantees that **less than 20 nodes are ever traversed.**

## クエリ開発ツール {#query-development-tools}

### アドビでのサポート {#adobe-supported}

* **Query Builder Debugger**

   * Query Builder クエリを実行するための Web UI。対応する XPath（クエリの説明を実行または Oak Index Definition Generator で使用）を生成します。
   * Located on AEM at [/libs/cq/search/content/querydebug.html](http://localhost:4502/libs/cq/search/content/querydebug.html)

* **CRXDE Lite - クエリツール**

   * XPath および JCR-SQL2 クエリを実行するための Web UI。
   * Located on AEM at [/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp) > Tools > Query...

* **[クエリの説明を実行](/help/sites-administering/operations-dashboard.md#explain-query)**

   * 任意の XPATH または JCR-SQL2 クエリの詳しい説明（クエリプラン、クエリ時間、結果数）が表示される AEM 操作ダッシュボード。

* **[処理に時間のかかるクエリ／一般的なクエリ](/help/sites-administering/operations-dashboard.md#query-performance)**

   * AEM で最近実行された処理に時間のかかるクエリおよび一般的なクエリが一覧表示される AEM 操作ダッシュボード。

* **[インデックスマネージャー](/help/sites-administering/operations-dashboard.md#the-index-manager)**

   * AEM インスタンスのインデックスを表示する AEM 操作 Web UI。既存のインデックス、ターゲットにできるインデックス、または増強できるインデックスの把握に役立ちます。

* **[ログ](/help/sites-administering/operations-dashboard.md#log-messages)**

   * Query Builder のログ記録

      * `DEBUG @ com.day.cq.search.impl.builder.QueryImpl`
   * Oak クエリ実行のログ記録

      * `DEBUG @ org.apache.jackrabbit.oak.query`


* **Apache Jackrabbit クエリエンジンの OSGi 設定**

   * トラバースクエリの失敗動作を設定する OSGi 設定。
   * Located on AEM at [/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService](http://localhost:4502/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService)

* **NodeCounter JMX Mbean**

   * AEM のコンテンツツリーのノード数を推定するのに使用する JMX MBean。
   * Located on AEM at [/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter)

### コミュニティによるサポート {#community-supported}

* **[Oak Index Definition Generator](https://oakutils.appspot.com/generate/index)**

   * XPath または JCR-SQL2 クエリステートメントから最適な Lucence プロパティインデックスを生成します。

* **[AEM Chrome Plug-in](https://chrome.google.com/webstore/detail/aem-chrome-plug-in/ejdcnikffjleeffpigekhccpepplaode?hl=ja-JP)**

   * Google Chrome Web ブラウザーの拡張機能で、実行されたクエリとそのクエリプランなど、リクエストごとのログデータをブラウザーの開発ツールコンソールに公開します。
   * [Sling Log Tracer 1.0.2 以上](https://sling.apache.org/downloads.cgi)がインストールされ、AEM で有効になっている必要があります。
