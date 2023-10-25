---
title: Oak クエリとインデックス作成
description: Adobe Experience Manager(AEM)6.5 でインデックスを設定する方法を説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/queries-and-indexing
feature: Configuring
exl-id: d9ec7728-84f7-42c8-9c80-e59e029840da
source-git-commit: c7c32130a3257c14c98b52f9db31d80587d7993a
workflow-type: tm+mt
source-wordcount: '3034'
ht-degree: 23%

---

# Oak クエリとインデックス作成{#oak-queries-and-indexing}

>[!NOTE]
>
>この記事では、AEM 6 でのインデックスの設定について説明します。 クエリおよびインデックス作成のパフォーマンスの最適化のベストプラクティスについては、[クエリとインデックスに関するベストプラクティス](/help/sites-deploying/best-practices-for-queries-and-indexing.md)を参照してください。

## はじめに {#introduction}

Jackrabbit 2 とは異なり、Oak はデフォルトでコンテンツのインデックスを作成しません。 カスタムインデックスは、従来のリレーショナルデータベースと同様に、必要に応じて作成する必要があります。 特定のクエリのインデックスがない場合、多くのノードがトラバースされる可能性があります。 クエリは引き続き動作する可能性がありますが、処理が遅い可能性があります。

Oak でインデックスのないクエリが検出された場合、WARN レベルのログメッセージが表示されます。

```xml
*WARN* Traversed 1000 nodes with filter Filter(query=select ...) consider creating an index or changing the query
```

## サポートされるクエリ言語 {#supported-query-languages}

Oak クエリエンジンは、次の言語をサポートしています。

* XPath （推奨）
* SQL-2
* SQL （非推奨）
* JQOM

## インデクサーのタイプとコストの計算 {#indexer-types-and-cost-calculation}

Apache Oak ベースのバックエンドを使用すると、様々なインデクサーをリポジトリにプラグインできます。

1 つのインデクサーは、 **プロパティインデックス**：インデックス定義をリポジトリ自体に格納します。

デフォルトでは、**Apache Lucene** および **Solr** の実装も使用できます。どちらもフルテキストのインデックスをサポートしています。

使用できるインデクサーがない場合は、**トラバーサルインデックス**&#x200B;が使用されます。つまり、コンテンツのインデックスが作成されず、クエリに一致するコンテンツノードが検索されます。

1 つのクエリに対して複数のインデクサーを使用できる場合、使用可能な各インデクサーは、クエリの実行にかかるコストを見積もります。 次に、Oak は推定コストが最も低いインデクサーを選択します。

![chlimage_1-148](assets/chlimage_1-148.png)

上の図は、Apache Oak のクエリ実行メカニズムの概要を示しています。

まず、クエリは抽象構文ツリーに解析されます。 次に、クエリがチェックされ、Oak クエリのネイティブ言語である SQL-2 に変換されます。

次に、各インデックスを参照して、クエリのコストを見積もります。 完了すると、最も安いインデックスの結果が取得されます。 最後に、結果がフィルタリングされ、現在のユーザーが結果に対する読み取りアクセス権を持ち、結果が完全なクエリと一致するようにします。

## インデックスの設定 {#configuring-the-indexes}

>[!NOTE]
>
>大規模なリポジトリの場合、インデックスの構築は時間のかかる操作です。 これは、インデックスの初期作成とインデックスの再作成（定義を変更した後にインデックスを再構築）の両方に当てはまります。 関連トピック [Oak インデックスのトラブルシューティング](/help/sites-deploying/troubleshooting-oak-indexes.md) および [インデックス再作成の遅延を防ぐ](/help/sites-deploying/troubleshooting-oak-indexes.md#preventing-slow-re-indexing).

大規模なリポジトリでインデックス再作成が必要な場合、特に MongoDB を使用し、フルテキストインデックスの場合は、テキストの事前抽出を検討し、oak-run を使用して初期インデックスを作成し、インデックスを再作成します。

インデックスは、リポジトリ内のノードとして、 **Oak:index** ノード。

インデックスノードのタイプは、 **oak:QueryIndexDefinition** 各インデクサーでは、ノードプロパティとして複数の設定オプションを使用できます。 詳しくは、以下の各インデクサータイプの設定の詳細を参照してください。

### プロパティインデックス {#the-property-index}

プロパティインデックスは、プロパティの制約を持つが、フルテキストではないクエリに役立ちます。 次の手順に従って設定できます。

1. `http://localhost:4502/crx/de/index.jsp` に移動して CRXDE を開きます。
1. の下にノードを作成します。 **oak:index**
1. ノードに名前を付けます。 **PropertyIndex**&#x200B;をクリックし、ノードタイプをに設定します。 **oak:QueryIndexDefinition**
1. 新しいノードに対して次のプロパティを設定します。

   * **タイプ：** `property` property（String タイプ）
   * **プロパティ名：** `jcr:uuid`（Name タイプ）

   この例では、 `jcr:uuid` プロパティ。このプロパティの役割は、接続先のノードの UUID(Universally Unique Identifier) を公開することです。

1. 変更内容を保存します。

プロパティインデックスには次の設定オプションがあります。

* The **type** プロパティは、インデックスのタイプを指定します。この場合、をに設定する必要があります。 **プロパティ**

* The **propertyNames** プロパティは、インデックスに保存されるプロパティのリストを示します。 見つからない場合は、ノード名がプロパティ名の参照値として使用されます。 この例では、 **jcr:uuid** プロパティの名前を指定して、そのノードの一意の識別子 (UUID) をインデックスに追加します。

* **unique** フラグは、**true** に設定されている場合、プロパティインデックスに対して一意性制約を付加します。

* The **declaringNodeTypes** プロパティを使用すると、インデックスの適用先となる特定のノードタイプを指定できます。
* The **再インデックス** に設定されている場合はフラグを設定 **true**、コンテンツの完全なインデックス再作成をトリガーします。

### 順序付きインデックス {#the-ordered-index}

Ordered インデックスは、Property インデックスの拡張です。 ただし、非推奨（廃止予定）となりました。 このタイプのインデックスは、 [Lucene プロパティインデックス](#the-lucene-property-index).

### Lucene フルテキストインデックス {#the-lucene-full-text-index}

AEM 6 では、Apache Lucene に基づいたフルテキストインデクサーを使用できます。

全文インデックスを設定した場合、全文インデックス条件を持つすべてのクエリは全文インデックスを使用します。インデックスが設定されている他の条件がある場合でも、パス制限がある場合でも使用します。

全文インデックスが設定されていない場合、全文条件を持つクエリは期待どおりに動作しません。

インデックスは非同期のバックグラウンドスレッドによって更新されるので、一部のフルテキスト検索は、バックグラウンドプロセスが完了するまで、少しの時間枠で使用できません。

次の手順に従って、Lucene のフルテキストインデックスを設定できます。

1. CRXDE を開き、以下にノードを作成します。 **oak:index**.
1. ノードに名前を付けます。 **LuceneIndex** ノードタイプをに設定します。 **oak:QueryIndexDefinition**
1. ノードに次のプロパティを追加します。

   * **タイプ：** `lucene` （String タイプ）
   * **async：** `async`（String タイプ）

1. 変更内容を保存します。

Lucene Index には次の設定オプションがあります。

* The **type** インデックスのタイプを指定するプロパティは、次のように設定する必要があります。 **lucene**
* The **非同期** に設定する必要があるプロパティ **非同期**. これにより、インデックス更新プロセスがバックグラウンドスレッドに送られます。
* The **includePropertyTypes** プロパティ。インデックスに含めるプロパティタイプのサブセットを定義します。
* The **excludePropertyNames** プロパティ名のリストを定義する — インデックスから除外する必要のあるプロパティ。
* The **再インデックス** に設定するとフラグを設定する **true**、コンテンツの完全なインデックス再作成をトリガーします。

### フルテキスト検索について {#understanding-fulltext-search}

この節のドキュメントは、例えば、PostgreSQL、SQLite、MySQL の Apache Lucene、Elasticsearch、フルテキストインデックスに適用されます。 次の例は、AEM / Oak / Lucene 用です。

<b>インデックスを作成するデータ</b>

開始点は、インデックスを作成する必要があるデータです。 例として、次のドキュメントを使用します。

| <b>ドキュメント ID</b> | <b>パス</b> | <b>フルテキスト</b> |
| --- | --- | --- |
| 100 | /content/rubik | 「ルービックはフィンランドのブランドだ」 |
| 200 | /content/rubiksCube | 「ルービックキューブは 1974 年に発明されました」 |
| 300 | /content/cube | 「立方体は 3 次元の物体です」 |


<b>反転インデックス</b>

インデックス作成メカニズムは、フルテキストを「トークン」と呼ばれる単語に分割し、「逆インデックス」と呼ばれるインデックスを作成します。 このインデックスには、各単語に対して表示されるドキュメントのリストが含まれます。

短く、一般的な単語（「stopwords」とも呼ばれます）はインデックス付けされません。 すべてのトークンは小文字に変換され、ステミングが適用されます。

特殊文字（例： ） *&quot;-&quot;* インデックスが作成されていません。

| <b>トークン</b> | <b>ドキュメント ID</b> |
| --- | --- |
| 194 | ..., 200,... |
| ブランド | ..., 100,... |
| キューブ | ..., 200, 300,... |
| ディメンション | 300 |
| 終了 | ..., 100,... |
| 発明する | 200 |
| オブジェクト | ..., 300,... |
| ルービック | ..., 100, 200,... |

ドキュメントのリストが並べ替えられます。 これは、クエリを実行する際に便利です。

<b>検索中</b>

次に、クエリの例を示します。 すべての特殊文字 ( *&#39;*) は次のスペースに置き換えられました。

```
/jcr:root/content//element(\*; cq:Page)`[` jcr:contains('Rubik s Cube')`]`
```

単語はトークン化され、インデックス作成時と同じ方法でフィルタリングされます（例えば、単一文字の単語は削除されます）。 この場合、検索対象は次のとおりです。

```
+:fulltext:rubik +:fulltext:cube
```

インデックスは、それらの単語のドキュメントのリストを調べます。 ドキュメントが多い場合は、リストが大きくなる場合があります。 例えば、次のようなものが含まれていると仮定します。


| <b>トークン</b> | <b>ドキュメント ID</b> |
| --- | --- |
| ルービック | 10, 100, 200, 1000 |
| キューブ | 30, 200, 300, 2000 |


Lucene は、2 つのリスト（またはラウンドロビン）間をフリップします `n` リスト、検索時 `n` 単語 ):

* &quot;rubik&quot;で読み取る最初のエントリを取得：10 を見つけます
* 「キューブ」で読み取ると、最初のエントリが取得されます `>` = 10. 10 が見つからない場合、次の 1 は 30 です。
* 「ルービック」で読み取る最初のエントリ `>` = 30: 100 を見つけます。
* 「キューブ」で読み取ると、最初のエントリが取得されます `>` = 100: 200 を見つけます。
* 「ルービック」で読み取る最初のエントリ `>` = 200。 200 件見つかりました。 つまり、document 200 は両方の用語に一致します。 これは記憶されています。
* 「ルービック」の読み取りは次のエントリを取得： 1000。
* 「キューブ」で読み取ると、最初のエントリが取得されます `>` = 1000: 2000 を見つけます。
* 「ルービック」で読み取る最初のエントリ `>` = 2000：リストの末尾。
* 最後に、検索を停止できます。

次の例に示すように、両方の用語を含むドキュメントは 200 のみです。

| 200 | /content/rubiksCube | 「ルービックキューブは 1974 年に発明されました」 |
| --- | --- | --- |

複数のエントリが見つかった場合、それらはスコアで並べ替えられます。

### Lucene プロパティインデックス {#the-lucene-property-index}

次以降 **Oak 1.0.8**&#x200B;を使用すると、Lucene を使用して、フルテキストではないプロパティ制約を含むインデックスを作成できます。

Lucene プロパティインデックスを作成するには、 **fulltextEnabled** プロパティは常に false に設定する必要があります。

次のクエリの例について考えてみます。

```xml
select * from [nt:base] where [alias] = '/admin'
```

上記のクエリの Lucene プロパティインデックスを定義するには、以下の定義を追加します。それには、以下の下にノードを作成します。 **oak:index:**

* **名前：** `LucenePropertyIndex`
* **タイプ：** `oak:QueryIndexDefinition`

ノードを作成したら、次のプロパティを追加します。

* **type：**

  ```xml
  lucene (of type String)
  ```

* **async：**

  ```xml
  async (of type String)
  ```

* **fulltextEnabled：**

  ```xml
  false (of type Boolean)
  ```

* **includePropertyNames：** `["alias"] (of type String)`

>[!NOTE]
>
>通常のプロパティインデックスと比較して、Lucene プロパティインデックスは常に非同期モードで設定されます。 したがって、インデックスから返される結果は、常にリポジトリの最新の状態を反映していない場合があります。

>[!NOTE]
>
>Lucene プロパティインデックスについて詳しくは、[Apache Jackrabbit Oak Lucene ドキュメントのページ](https://jackrabbit.apache.org/oak/docs/query/lucene.html)を参照してください。

### Lucene アナライザー {#lucene-analyzers}

バージョン 1.2.0 以降、Oak は Lucene アナライザーをサポートします。

アナライザは、ドキュメントのインデックスが作成されるときと、クエリ時の両方で使用されます。 アナライザは、フィールドのテキストを調べ、トークンストリームを生成します。 Lucene アナライザーは、一連のトークン化クラスとフィルタークラスで構成されています。

アナライザーは、 `analyzers` ノード ( タイプ `nt:unstructured`) を `oak:index` 定義。

インデックスのデフォルトのアナライザーは、analyzers ノードの子の `default` に設定されます。

![chlimage_1-149](assets/chlimage_1-149.png)

>[!NOTE]
>
>使用可能なアナライザーのリストについては、使用している Lucene バージョンの API ドキュメントを参照してください。

#### Analyzer クラスの直接指定 {#specifying-the-analyzer-class-directly}

標準のアナライザを使用する場合は、次の手順に従って設定できます。

1. アナライザを使用するインデックスを、 `oak:index` ノード。

1. このインデックスの下に `default` という子ノード（タイプ `nt:unstructured`）を作成します。

1. default ノードに次のプロパティを追加します。

   * **名前:** `class`
   * **タイプ：** `String`
   * **値：** `org.apache.lucene.analysis.standard.StandardAnalyzer`

   値は、使用するアナライザ・クラスの名前です。

   また、特定の Lucene バージョンで使用するアナライザを設定するには、オプションの `luceneMatchVersion` 文字列プロパティ。 Lucene 4.7 で使用する場合の有効な構文は次のとおりです。

   * **名前：** `luceneMatchVersion`
   * **タイプ：** `String`
   * **値：** `LUCENE_47`

   次の場合 `luceneMatchVersion` が指定されていない場合、Oak は付属の Lucene のバージョンを使用します。

1. Analyzer 構成にストップワードファイルを追加する場合は、 `default` 1 つは次のプロパティを持ちます。

   * **名前：** `stopwords`
   * **タイプ：** `nt:file`

#### 構成を使用したアナライザの作成 {#creating-analyzers-via-composition}

アナライザーは、 `Tokenizers`, `TokenFilters`、および `CharFilters`. これを行うには、アナライザを指定し、オプションの tokenizer と filter の子ノードをリスト順に作成します。 関連トピック [https://cwiki.apache.org/confluence/display/solr/AnalyzersTokenizersTokenFilters#Specifying_an_Analyzer_in_the_schema](https://cwiki.apache.org/confluence/display/solr/AnalyzersTokenizersTokenFilters#Specifying_an_Analyzer_in_the_schema)

例えば、次のノード構造について考えてみます。

* **名前:** `analyzers`

   * **名前:** `default`

      * **名前:** `charFilters`
      * **タイプ:** `nt:unstructured`

         * **名前:** `HTMLStrip`
         * **名前:** `Mapping`

      * **名前:** `tokenizer`

         * **プロパティ名:** `name`

            * **タイプ:** `String`
            * **値：** `Standard`

      * **名前：** `filters`
      * **タイプ:** `nt:unstructured`

         * **名前:** `LowerCase`
         * **名前:** `Stop`

            * **プロパティ名:** `words`

               * **タイプ:** `String`
               * **値：** `stop1.txt, stop2.txt`

            * **名前：** `stop1.txt`

               * **タイプ:** `nt:file`

            * **名前:** `stop2.txt`

               * **タイプ：** `nt:file`

フィルタ、charFilters、および tokenizers の名前は、ファクトリのサフィックスを削除することで形成されます。 したがって、

* `org.apache.lucene.analysis.standard.StandardTokenizerFactory` が `standard` になります

* `org.apache.lucene.analysis.charfilter.MappingCharFilterFactory` が `Mapping` になります

* `org.apache.lucene.analysis.core.StopFilterFactory` が `Stop` になります

ファクトリに必要な設定パラメーターは、該当するノードのプロパティとして指定されます。

ストップワードの読み込みなど、外部ファイルからのコンテンツを読み込む必要がある場合、コンテンツは、 `nt:file` 問題のファイルのタイプ。

### Solr インデックス {#the-solr-index}

Solr インデックスの目的はフルテキスト検索ですが、パス、プロパティ制限、プライマリタイプ制限で検索をインデックス化する場合にも使用できます。 つまり、Oak 内の Solr インデックスは、任意の種類の JCR クエリに使用できます。

AEMでの統合はリポジトリレベルでおこなわれるので、Solr は Oak で使用できるインデックスの 1 つです。Oak はAEMに付属の新しいリポジトリ実装です。

AEM インスタンスでリモートサーバーとして機能するように設定できます。

### AEM での単一リモート Solr サーバーの設定 {#configuring-aem-with-a-single-remote-solr-server}

AEM は、リモート Solr サーバーインスタンスと連動するように設定することもできます。

1. 最新バージョンの Solr をダウンロードして抽出します。 この方法について詳しくは、 [Apache Solr のインストールドキュメント](https://solr.apache.org/guide/6_6/installing-solr.html).
1. 次に、2 つの Solr シャードを作成します。 そのためには、Solr の展開先フォルダー内に、各シャード用のフォルダーを作成します。

   * 1 つ目のシャード用に、次のフォルダーを作成します。

   `<solrunpackdirectory>\aemsolr1\node1`

   * 2 つ目のシャード用に、次のフォルダーを作成します。

   `<solrunpackdirectory>\aemsolr2\node2`

1. Solr パッケージ内のサンプルインスタンスを探します。これは、「 `example`」が含まれています。
1. サンプルインスタンスの次のフォルダーを、2 つのシャードフォルダー（`aemsolr1\node1` と `aemsolr2\node2`）にコピーします。

   * `contexts`
   * `etc`
   * `lib`
   * `resources`
   * `scripts`
   * `solr-webapp`
   * `webapps`
   * `start.jar`

1. 「 」という名前のフォルダーを作成します。 `cfg`」という名前が付けられます。
1. 新規作成した `cfg` フォルダーに、Solr および Zookeeper 設定ファイルを配置します。

   >[!NOTE]
   >
   >Solr および ZooKeeper 設定について詳しくは、[Solr の設定に関するドキュメント](https://cwiki.apache.org/confluence/display/solr/ConfiguringSolr)および [ZooKeeper 入門ガイド](https://zookeeper.apache.org/doc/r3.1.2/zookeeperStarted.html)を参照してください。

1. 1 つ目のシャードを ZooKeeper サポート付きで起動するために、`aemsolr1\node1` に移動し、次のコマンドを実行します。

   ```xml
   java -Xmx2g -Dbootstrap_confdir=./cfg/oak/conf -Dcollection.configName=myconf -DzkRun -DnumShards=2 -jar start.jar
   ```

1. 2 つ目のシャードを起動するために、`aemsolr2\node2` に移動し、次のコマンドを実行します。

   ```xml
   java -Xmx2g -Djetty.port=7574 -DzkHost=localhost:9983 -jar start.jar
   ```

1. 両方のシャードが起動したら、Solr インターフェイスに接続し（`http://localhost:8983/solr/#/`）、すべてが稼働していることをテストします。
1. AEM を起動し、次の Web コンソール（`http://localhost:4502/system/console/configMgr`）にアクセスします
1. 「**Oak Solr remote server configuration**」で次の設定を行います。

   * Solr HTTP URL：`http://localhost:8983/solr/`

1. 選択 **リモート Solr** を選択します。 **Oak Solr** サーバープロバイダー。

1. CRXDE に移動し、管理者としてログインします。
1. という名前のノードを作成します。 **solrIndex** under **oak:index**&#x200B;をクリックし、次のプロパティを設定します。

   * **タイプ：** solr（文字列タイプ）
   * **async：** async（文字列型）
   * **reindex：** true（ブール値型）

1. 変更内容を保存します。

#### Solr の推奨設定 {#recommended-configuration-for-solr}

以下に、この記事で説明する 3 つの Solr デプロイメントすべてで使用できる基本設定の例を示します。AEM に既に存在する専用プロパティインデックスに対応しているため、他のアプリケーションでは使用しないでください。

これを適切に使用するには、アーカイブの内容を Solr ホームディレクトリに直接配置する必要があります。 複数ノードのデプロイメントがある場合は、各ノードのルートフォルダーの直下に配置する必要があります。

Solr 推奨設定ファイル

[ファイルを入手](assets/recommended-conf.zip)

### AEM インデックス作成ツール {#aem-indexing-tools}

AEM 6.1 では、AEM 6.0 の次の 2 つのインデックス作成ツールが Adobe Consulting Services Commons ツールセットの一部として統合されています。

1. **クエリの説明を実行**&#x200B;は、管理者がクエリの実行方法を理解できるように設計されたツールです。
1. **Oak インデックスマネージャ**：既存のインデックスを維持するための Web ユーザーインターフェイス。

これで、 **ツール/運営/ダッシュボード/診断** をAEMのようこそ画面から開きます。

使用方法について詳しくは、 [運用ダッシュボードのドキュメント](/help/sites-administering/operations-dashboard.md).

#### OSGi を使用したプロパティインデックスの作成 {#creating-property-indexes-via-osgi}

ACS Commons パッケージは、プロパティインデックスの作成に使用できる OSGi 設定も公開します。

Web コンソールからアクセスするには、「**Oak プロパティインデックスを確認します。**&quot;.

![chlimage_1-150](assets/chlimage_1-150.png)

### インデックス作成の問題のトラブルシューティング {#troubleshooting-indexing-issues}

クエリの実行に時間がかかり、一般的なシステム応答時間が長くなる場合があります。

この節では、こうした問題の原因を追跡するために何をおこなう必要があるかに関する推奨事項と、その解決方法に関するアドバイスを示します。

#### 分析のデバッグ情報を準備中 {#preparing-debugging-info-for-analysis}

実行中のクエリに必要な情報を取得する最も簡単な方法は、 [クエリの説明を実行ツール](/help/sites-administering/operations-dashboard.md#explain-query). これにより、ログレベルの情報を調べる必要なく、処理の遅いクエリのデバッグに必要な正確な情報を収集できます。 デバッグ対象となるクエリがわかっている場合は、このツールをお勧めします。

何らかの理由でこれが不可能な場合は、インデックス作成ログを単一のファイルで収集し、それを使用して特定の問題のトラブルシューティングを行うことができます。

#### ログを有効にする {#enable-logging}

ログを有効にするには、 **デバッグ** Oak のインデックス作成とクエリに関するカテゴリのレベルログ。 次のカテゴリがあります。

* org.apache.jackrabbit.oak.plugins.index
* org.apache.jackrabbit.oak.query
* com.day.cq.search

The **com.day.cq.search** カテゴリは、AEMが提供する QueryBuilder ユーティリティを使用している場合にのみ適用できます。

>[!NOTE]
>
>ログは、トラブルシューティングするクエリが実行中の間のみ、DEBUG に設定されることが重要です。 そうしないと、多くのイベントが時間の経過と共にログに生成されます。 このため、必要なログが収集されたら、前述のカテゴリの情報レベルのログに戻します。

次の手順に従って、ログを有効にすることができます。

1. ブラウザーで `https://serveraddress:port/system/console/slinglog` を指定します。
1. コンソールの下部にある「**Add new Logger**」ボタンをクリックします。
1. 新しく作成された行で、前述のカテゴリを追加します。**+** 記号を使用して、1 つのロガーに複数のカテゴリを追加できます。
1. 選択 **デバッグ** から **ログレベル** 」ドロップダウンリストから選択できます。
1. 出力ファイルをに設定します。 `logs/queryDebug.log`. これにより、すべての DEBUG イベントが 1 つのログファイルに関連付けられます。
1. クエリを実行するか、デバッグ対象のクエリを使用しているページをレンダリングします。
1. クエリを実行したら、ログコンソールに戻り、新しく作成したロガーのログレベルを **INFO** に変更します。

#### インデックス設定 {#index-configuration}

クエリの評価方法は、インデックス設定の影響を大きく受けます。 インデックス設定を分析またはサポートに送信することが重要です。 設定は、コンテンツパッケージとして取得するか、JSON レンディションを取得できます。

通常、インデックス設定は `/oak:index` CRXDE のノードでは、次の場所で JSON のバージョンを取得できます。

`https://serveraddress:port/oak:index.tidy.-1.json`

インデックスが別の場所で設定されている場合は、それに応じてパスを変更します。

#### MBean 出力 {#mbean-output}

デバッグにインデックス関連の MBean の出力を提供すると役立つ場合があります。 手順は次のとおりです。

1. JMX コンソールに移動します。
   `https://serveraddress:port/system/console/jmx`

1. 次の MBean を検索します。

   * Lucene Index 統計
   * CopyOnRead のサポート統計
   * Oak クエリ統計
   * IndexStats

1. 各 MBean をクリックして、パフォーマンス統計を取得できます。 サポートの送信が必要な場合に備えて、スクリーンショットを作成するか、メモしておきます。

また、これらの統計に関する JSON 形式の情報を、次の URL で取得できます。

* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`

統合された JMX 出力は、 `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak.tidy.3.json`. これには、Oak 関連のすべての MBean の詳細が JSON 形式で含まれます。

#### その他の詳細 {#other-details}

問題のトラブルシューティングに役立つ次のような詳細を収集できます。

1. インスタンスが実行されている Oak のバージョン。 この情報を確認するには、CRXDE を開き、ようこそページの右下隅にあるバージョンを参照するか、`org.apache.jackrabbit.oak-core` バンドルのバージョンをチェックします。
1. 問題が発生しているクエリの QueryBuilder デバッガーの出力。デバッガーには、`https://serveraddress:port/libs/cq/search/content/querydebug.html` からアクセスできます。
