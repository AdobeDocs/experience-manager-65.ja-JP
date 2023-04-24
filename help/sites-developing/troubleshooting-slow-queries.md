---
title: 処理に時間のかかるクエリのトラブルシューティング
seo-title: Troubleshooting Slow Queries
description: 処理に時間のかかるクエリのトラブルシューティング
seo-description: null
uuid: ad09546a-c049-44b2-99a3-cb74ee68f040
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: c01e42ff-e338-46e6-a961-131ef943ea91
exl-id: 3405cdd3-3d1b-414d-9931-b7d7b63f0a6f
source-git-commit: a296e459461973fc2dbd0641c6fdda1d89d8d524
workflow-type: tm+mt
source-wordcount: '2262'
ht-degree: 34%

---

# 処理に時間のかかるクエリのトラブルシューティング{#troubleshooting-slow-queries}

## 処理に時間のかかるクエリの分類 {#slow-query-classifications}

AEMでは、処理に時間のかかるクエリの 3 つの主な分類が重要度別に表示されます。

1. **インデックスなしクエリ**

   * 実行するクエリ **not** インデックスに解決し、JCR のコンテンツを走査して結果を収集する

1. **制限（範囲指定）が不十分なクエリ**

   * インデックスに解決されるが、結果を収集するには、すべてのインデックスエントリをトラバースする必要があるクエリ

1. **大きな結果セットクエリ**

   * 多数の結果を返すクエリ

最初の 2 つのクエリの分類（インデックスが少なく、制限が不十分）が遅くなる。 Oak クエリエンジンに対して各 **潜在的な** result （コンテンツノードまたはインデックスエントリ）: **実際** 結果セット。

各潜在的な結果を検査する行為は、トラバーシングと呼ばれるものです。

各潜在的な結果を検査する必要があるので、実際の結果セットを決定するコストは、電位結果の数に比例して増加します。

クエリ制限とチューニングインデックスを追加すると、インデックスデータを最適化された形式で保存し、結果を迅速に取得でき、潜在的な結果セットの線形検査の必要性を軽減または排除できます。

AEM 6.3 では、デフォルトで、100,000 件のトラバーサルに到達すると、クエリが失敗し、例外がスローされます。 この制限は、AEM 6.3 より前のAEMバージョンにはデフォルトで存在しませんが、Apache Jackrabbit Query Engine Settings OSGi 設定および QueryEngineSettings JMX bean（LimitReads プロパティ）で設定できます。

### インデックスレスクエリの検出 {#detecting-index-less-queries}

#### 開発中 {#during-development}

説明 **すべて** クエリを実行し、クエリプランに含まれていないことを確認します。 **/&amp;ast;traverse** 説明を含む。 トラバースするクエリプランの例は次のとおりです。

* **プラン：** `[nt:unstructured] as [a] /* traverse "/content//*" where ([a].[unindexedProperty] = 'some value') and (isdescendantnode([a], [/content])) */`

#### デプロイメント後 {#post-deployment}

* インデックスのないトラバーサルクエリについて、`error.log` を監視します。

   * `*INFO* org.apache.jackrabbit.oak.query.QueryImpl Traversal query (query without index) ... ; consider creating and index`
   * このメッセージは、使用可能なインデックスがなく、クエリが多数のノードを横断する可能性がある場合にのみ記録されます。 インデックスが使用可能な場合、メッセージはログに記録されませんが、トラバースする量が少ないので、処理が高速です。

* AEM の[クエリパフォーマンス](/help/sites-administering/operations-dashboard.md#query-performance)操作コンソールに移動し、処理に時間がかかるクエリの[説明](/help/sites-administering/operations-dashboard.md#explain-query)を実行して、トラバーサルまたはインデックスのないクエリの説明を探します。

### 制限が不十分なクエリの検出 {#detecting-poorly-restricted-queries}

#### 開発中 {#during-development-1}

すべてのクエリについて説明し、クエリのプロパティ制限に合わせて調整されたインデックスに解決されることを確認します。

* 理想的なクエリプランの範囲では、すべてのプロパティ制限、および少なくともクエリで最も厳密なプロパティ制限に `indexRules` を持ちます。
* 結果を並べ替えるクエリは、Lucene プロパティインデックスに解決される必要があります。このインデックスには、`orderable=true.` を設定するプロパティによる並べ替えに関するインデックスルールがあります。

#### 例えば、デフォルトの `cqPageLucene` には `jcr:content/cq:tags` に対するインデックスルールがありません。 {#for-example-the-default-cqpagelucene-does-not-have-an-index-rule-for-jcr-content-cq-tags}

cq:tags インデックスルールを追加する前

* **cq:tags インデックスルール**

   * 標準では存在しません

* **Query Builder クエリ**

   ```js
   type=cq:Page
   property=jcr:content/cq:tags
   property.value=my:tag
   ```

* **クエリプラン**

   `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) *:* where [a].[jcr:content/cq:tags] = 'my:tag' */`

このクエリは `cqPageLucene` インデックスに解決されます。ただし、`jcr:content` または `cq:tags` のプロパティインデックスルールは存在しないので、この制限を評価する際に、`cqPageLucene` インデックス内のすべてのレコードが一致するかどうかを判断するためにチェックされます。したがって、インデックスに 100 万が含まれる場合 `cq:Page` ノードの後に 100 万件のレコードがチェックされ、結果セットが決定されます。

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

クエリの制限が増えると、対象となる結果セットが減り、クエリの最適化がさらに最適化されます。

同様に、 `cq:tags` プロパティ、制限付きのフルテキストクエリも含む `cq:tags` インデックスの結果はすべての全文一致を返すので、パフォーマンスが低下します。 その後、cq:tags の制限がフィルタリングされます。

インデックス後フィルタリングのもう 1 つの原因は、開発中に頻繁に見逃されるアクセス制御リストです。 ユーザーがアクセスできない可能性のあるパスがクエリによって返されないことを確認してください。 これは、コンテンツ構造を改善し、クエリに関連するパス制限を提供することで実行できます。

Lucene インデックスが多数の結果を返して小さなサブセットをクエリ結果として返しているかどうかを識別するのに便利な方法は、の DEBUG ログを有効にすることです。 `org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex`. これにより、インデックスから読み込まれているドキュメントの数を確認できます。 結果の数と読み込まれたドキュメントの数は不釣り合いになりません。 詳しくは、[ログ](/help/sites-deploying/configure-logging.md)を参照してください。

#### デプロイメント後 {#post-deployment-1}

* トラバーサルクエリについて、`error.log` を監視します。

   * `*WARN* org.apache.jackrabbit.oak.spi.query.Cursors$TraversingCursor Traversed ### nodes ... consider creating an index or changing the query`

* AEM の[クエリパフォーマンス](/help/sites-administering/operations-dashboard.md#query-performance)操作コンソールに移動し、処理に時間がかかるクエリの[説明](/help/sites-administering/operations-dashboard.md#explain-query)を実行して、クエリプロパティ制限がインデックスプロパティルールに解決されないクエリプランを探します。

### 大きな結果セットクエリの検出 {#detecting-large-result-set-queries}

#### 開発中 {#during-development-2}

oak.queryLimitInMemory ( 例：10000) と oak.queryLimitReads （例：5000）に低いしきい値を設定し、「The query read more than x nodes...」という UnsupportedOperationException をヒットする際に高価なクエリを最適化します。

しきい値を低く設定すると、リソースを大量に消費するクエリ（インデックスを使用しないクエリや、インデックスをカバーしないクエリ）を回避できます。 例えば、100 万個のノードを読み取るクエリは、大量の IO を引き起こし、アプリケーション全体のパフォーマンスに悪影響を与えます。 したがって、上記の制限によって失敗したクエリは、分析し、最適化する必要があります。

#### デプロイメント後 {#post-deployment-2}

* ログを監視して、大規模なノードの走査やヒープメモリの大量使用を引き起こしているクエリがないかどうかを調べます。

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * クエリを最適化して、横断するノードの数を減らします。

* 大量のヒープメモリ消費を引き起こすクエリについて、ログを監視します。

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * ヒープメモリの消費を減らすようにクエリを最適化します。

AEM 6.0 ～ 6.2 では、AEM 起動スクリプトで JVM パラメーターを使用してノードの走査のしきい値を調整することで、大規模なクエリによって環境に過度の負荷がかかるのを防ぐことができます。推奨される値は次のとおりです。

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

AEM 6.3 では、上記の 2 つのパラメーターはデフォルトで事前設定されており、OSGi QueryEngineSettings を使用して変更できます。

詳しくは、[https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits) を参照してください。

## クエリパフォーマンスの調整 {#query-performance-tuning}

AEMでのクエリパフォーマンス最適化のモットーは次のとおりです。

**「制限が多いほど、より良いものになる」**

次に、クエリのパフォーマンスを確保するための推奨される調整の概要を示します。 まず、クエリを調整し、目立たないアクティビティを調整し、必要に応じて、インデックス定義を調整します。

### クエリ文の調整 {#adjusting-the-query-statement}

AEMは、次のクエリ言語をサポートしています。

* Query Builder
* JCR-SQL2
* XPath

次の例では、AEM開発者が使用する最も一般的なクエリ言語として Query Builder を使用していますが、同じ原則が JCR-SQL2 および XPath にも当てはまります。

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

1. クエリが既存の Lucene プロパティインデックスに解決されるように、クエリのノードタイプ制限を調整します。

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

   `nt:hierarchyNode` は、 `cq:Page`. 仮定 `jcr:content/contentType=article-page` が適用されるのは次の場合のみです。 `cq:Page` ノードをAdobeのカスタムアプリケーションを介して、このクエリは `cq:Page` ノード `jcr:content/contentType=article-page`. ただし、次の理由から、このフローは亜最適な制限です。

   * 他のノードは次から継承 `nt:hierarchyNode` ( 例： `dam:Asset`) 結果のセットに不必要な追加を行う。
   * AEM で提供される、`nt:hierarchyNode` 用のインデックスは存在しませんが、`cq:Page` 用に提供されているインデックスはあります。
   `type=cq:Page` を設定すると、このクエリは `cq:Page` ノードのみに限定され、AEM の cqPageLucene に解決されます。これにより、結果は AEM のノードのサブセット（cq:Page ノードのみ）に限定されます。

1. または、クエリが既存のプロパティインデックスに解決されるようにプロパティの制限を調整します。

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

   プロパティ制限の変更元 `jcr:content/contentType` （カスタム値）を既知のプロパティに追加する `sling:resourceType` クエリをプロパティインデックスに解決できます。 `slingResourceType` を使用して、すべてのコンテンツを `sling:resourceType`.

   （Lucene プロパティインデックスとは異なる）プロパティインデックスは、クエリがノードタイプで認識されず、単一のプロパティ制限が結果セットに優先する場合に最も適しています。

1. クエリに可能な最も厳密なパス制限を追加します。 例：`/content/my-site`より`/content/my-site/us/en`が推奨され、また`/`より`/content/dam`が推奨されます。

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

   次のパス制限の範囲を設定 `path=/content`から `path=/content/my-site/us/en` を使用すると、検査する必要のあるインデックスエントリの数を減らすことができます。 クエリがパスを適切に制限できる場合、単なる `/content` または `/content/dam`を使用する場合、インデックスに `evaluatePathRestrictions=true`.

   `evaluatePathRestrictions` を使用すると、インデックスのサイズが大きくなります。

1. 可能な場合は、次のようなクエリ関数やクエリ操作を避けます。 `LIKE` および `fn:XXXX` コストは、制限に基づく結果の数に応じて拡大/縮小されます。

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

   LIKE 条件の評価には時間がかかります。これは、テキストがワイルドカードで始まる場合（「%...」）はインデックスを使用できないからです。jcr:contains 条件は、フルテキストのインデックスの使用を可能にするので、推奨されています。解決された Lucene プロパティインデックスに indexRule が必要です。 `jcr:content/contentType` と `analayzed=true`.

   `fn:lowercase(..)` などのクエリ関数の使用を最適化するのは、（より複雑で目立つインデックス分析設定の外部に）より高速な同等の手段がないので困難です。クエリ全体のパフォーマンスを向上させるには、他のスコーピング制限を特定することをお勧めします。この場合、関数は、可能な限り最小限の結果セットに対して動作する必要があります。

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

   `p.guessTotal=100` は、最初の 100 件の結果のみを収集するように Query Builder に指示します。 また、少なくとも 1 つの結果が存在するかどうかを示すブール値フラグを設定するには（この数をカウントすると遅くなるので、結果が何個以上あるかは示しません）。 この最適化は、ページネーションや無限読み込みの使用例に優れ、結果のサブセットのみが増分的に表示されます。

## 既存のインデックスの調整 {#existing-index-tuning}

1. 最適なクエリがプロパティインデックスに解決される場合、プロパティインデックスは最小限の調整可能なので、実行する必要はありません。
1. できることがある場合、クエリは Lucene プロパティインデックスに解決される必要があります。解決できるインデックスがない場合は、新しいインデックスの作成に進みます。
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

1. Oak Index Definition Generator( ) に XPath（または JCR-SQL2）を指定します。 `https://oakutils.appspot.com/generate/index` 最適化された Lucene プロパティインデックス定義を生成できます。 <!-- The above URL is 404 as of April 24, 2023 -->

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

1. 生成された定義を、追加する形で既存の Lucene プロパティインデックスに手動で結合します。既存の設定は、他のクエリを満たすために使用される場合があるので、削除しないように注意してください。

   1. cq:Page に対応する既存の Lucene プロパティインデックスを探します（インデックスマネージャを使用）。 この場合は、`/oak:index/cqPageLucene`です。
   1. 最適化されたインデックス定義 ( ステップ#4) と既存のインデックス (/oak:index/cqPageLucene) の間の設定差分を特定し、最適化されたインデックスの欠落している設定を既存のインデックス定義に追加します。
   1. AEMのインデックス再作成のベストプラクティスに従って、既存のコンテンツがこのインデックス設定の変更の影響を受ける可能性があるかどうかに基づいて、更新または再インデックスが順番におこなわれます。

## 新しいインデックスの作成 {#create-a-new-index}

1. クエリが既存の Lucene プロパティインデックスに解決されないことを確認します。 その場合は、上記の「チューニングと既存のインデックス」の節を参照してください。
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

1. Oak Index Definition Generator( ) に XPath（または JCR-SQL2）を指定します。 `https://oakutils.appspot.com/generate/index` 最適化された Lucene プロパティインデックス定義を生成できます。 <!-- The above URL is 404 as of April 24, 2023 -->

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

   Oak インデックス定義を管理するAEMプロジェクトに、新しいインデックス用の Oak Index Definition Generator が提供する XML 定義を追加します（コードはコードに依存するので、Oak インデックス定義をコードとして扱うことを忘れないでください）。

   通常のAEMソフトウェア開発ライフサイクルに従って新しいインデックスをデプロイおよびテストし、クエリがインデックスに解決され、クエリが実行されることを確認します。

   このインデックスの初期デプロイメント時に、AEMは必要なデータでインデックスを設定します。

## インデックスがないクエリおよびトラバーサルクエリに問題がない場合 {#when-index-less-and-traversal-queries-are-ok}

AEMの柔軟なコンテンツアーキテクチャにより、コンテンツ構造のトラバーサルが時間の経過と共に進化せず、容認できないほど大きくなるのを予測し確実にすることは困難です。

したがって、パス制限とノードタイプ制限の組み合わせによってクエリが確実に満たされる場合を除き、インデックスがクエリを確実に満たすようにします。 **20 個未満のノードがトラバースされます。**

## クエリ開発ツール {#query-development-tools}

### Adobe対応 {#adobe-supported}

* **Query Builder Debugger**

   * Query Builder クエリを実行するための web UI。対応する XPath（クエリの説明を実行または Oak Index Definition Generator で使用）を生成します。
   * AEMで [/libs/cq/search/content/querydebug.html](http://localhost:4502/libs/cq/search/content/querydebug.html)

* **CRXDE Lite — クエリツール**

   * XPath および JCR-SQL2 クエリを実行するための WebUI。
   * AEMで [/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp) /ツール/クエリ…

* **[クエリの説明を実行](/help/sites-administering/operations-dashboard.md#explain-query)**

   * 任意の XPATH または JCR-SQL2 クエリの詳細な説明（クエリ計画、クエリ時間、結果数）を提供する「AEM Operations」ダッシュボード。

* **[処理に時間のかかるクエリ／一般的なクエリ](/help/sites-administering/operations-dashboard.md#query-performance)**

   * AEMで実行された最近の遅いクエリと一般的なクエリの一覧を示すAEM操作ダッシュボード。

* **[インデックスマネージャ](/help/sites-administering/operations-dashboard.md#the-index-manager)**

   * AEMインスタンス上のインデックスを表示するAEM Operations WebUI;は、どのインデックスが存在するかを容易に理解できます。ターゲット設定または拡張が可能です。

* **[ログ](/help/sites-administering/operations-dashboard.md#log-messages)**

   * Query Builder のログ

      * `DEBUG @ com.day.cq.search.impl.builder.QueryImpl`
   * Oak クエリ実行のログ記録

      * `DEBUG @ org.apache.jackrabbit.oak.query`


* **Apache Jackrabbit Query Engine Settings OSGi Config**

   * トラバースクエリの失敗動作を設定する OSGi 設定。
   * AEMで [/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService](http://localhost:4502/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService)

* **NodeCounter JMX Mbean**

   * AEMのコンテンツツリー内のノード数の予測に使用される JMX MBean です。
   * AEMで [/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter)

### コミュニティによるサポート {#community-supported}

* **Oak Index Definition Generator( )`https://oakutils.appspot.com/generate/index`** <!-- The above URL is 404 as of April 24, 2023 -->

   * XPath または JCR-SQL2 クエリステートメントから最適な Lucence プロパティインデックスを生成します。

* **[AEM Chrome Plug-in](https://chrome.google.com/webstore/detail/aem-chrome-plug-in/ejdcnikffjleeffpigekhccpepplaode?hl=ja-JP)**

   * Google Chrome web ブラウザーの拡張機能で、実行されたクエリとそのクエリプランなど、リクエストごとのログデータをブラウザーの開発ツールコンソールに公開します。
   * [Sling Log Tracer 1.0.2 以上](https://sling.apache.org/downloads.cgi)がインストールされ、AEM で有効になっている必要があります。
