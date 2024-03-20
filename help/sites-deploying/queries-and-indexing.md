---
title: Oak クエリとインデックス作成
description: Adobe Experience Manager（AEM）6.5 でのインデックスの設定方法について説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/queries-and-indexing
feature: Configuring
exl-id: d9ec7728-84f7-42c8-9c80-e59e029840da
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '3034'
ht-degree: 99%

---

# Oak クエリとインデックス作成{#oak-queries-and-indexing}

>[!NOTE]
>
>この記事は、AEM 6 でのインデックス設定について説明しています。クエリおよびインデックス作成のパフォーマンスの最適化のベストプラクティスについては、[クエリとインデックスに関するベストプラクティス](/help/sites-deploying/best-practices-for-queries-and-indexing.md)を参照してください。

## はじめに {#introduction}

Jackrabbit 2 とは異なり、Oak はデフォルトでコンテンツのインデックスを作成しません。 カスタムインデックスは、従来のリレーショナルデータベースと同様に、必要に応じて作成する必要があります。特定のクエリのためのインデックスがない場合は、多数のノードが走査される可能性があります。クエリが機能しても非常に時間がかかる可能性があります。

Oak では、インデックスのないクエリが実行されると、WARN レベルのログメッセージが出力されます。

```xml
*WARN* Traversed 1000 nodes with filter Filter(query=select ...) consider creating an index or changing the query
```

## サポートされているクエリ言語 {#supported-query-languages}

Oak クエリエンジンでは、次の言語がサポートされています。

* XPath（推奨）
* SQL-2
* SQL（非推奨）
* JQOM

## インデクサーのタイプとコストの計算 {#indexer-types-and-cost-calculation}

Apache Oak ベースのバックエンドでは、様々なインデクサーをリポジトリにプラグインすることができます。

インデクサーの 1 つは、**プロパティインデックス**&#x200B;です。このインデクサーでは、インデックス定義がリポジトリ自体に格納されます。

デフォルトでは、**Apache Lucene** および **Solr** の実装も使用できます。どちらもフルテキストのインデックスをサポートしています。

使用できるインデクサーがない場合は、**トラバーサルインデックス**&#x200B;が使用されます。つまり、コンテンツにインデックスが作成されず、クエリに一致するものを見つけるために、コンテンツノードが走査されます。

あるクエリに対して複数のインデクサーを使用できる場合、使用できる各インデクサーによってクエリ実行コストが見積もられます。 次に、見積もりコストが最も低いインデクサーが Oak によって選択されます。

![chlimage_1-148](assets/chlimage_1-148.png)

この図は、Apache Oak のクエリ実行メカニズムに関する概要図です。

まず、クエリが抽象構文ツリーへと解析されます。次に、このクエリがチェックされ、Oak クエリのネイティブ言語である SQL-2 に変換されます。

次に、各インデックスを参照して、クエリのコストを見積もります。 完了すると、最も安いインデックスの結果が取得されます。 最後に、結果がフィルタリングされ、現在のユーザーが結果に対する読み取りアクセス権を持ち、結果が完全なクエリと一致するようにします。

## インデックスの設定 {#configuring-the-indexes}

>[!NOTE]
>
>大規模なリポジトリでインデックスを構築するには時間がかかります。これは、最初にインデックスを作成するときと、再インデックス（定義を変更した後にインデックスを再構築すること）を行うときの両方に当てはまります。[Oak インデックスのトラブルシューティング](/help/sites-deploying/troubleshooting-oak-indexes.md)と[時間のかかるインデックス再作成の防止](/help/sites-deploying/troubleshooting-oak-indexes.md#preventing-slow-re-indexing)も参照してください。

非常に大規模なリポジトリでインデックスを再作成する場合、特に MongoDB を使用してフルテキストのインデックスを作成する場合は、事前にテキストを抽出して、oak-run により初期インデックス構築し、インデックスを再作成する方法を検討してください。

インデックスは、リポジトリ内の **oak:index** ノードの下で、ノードとして設定されます。

インデックスノードのタイプは、**oak:QueryIndexDefinition** とする必要があります。各インデクサーでは、ノードプロパティとして複数の設定オプションを使用できます。 詳しくは、以下の各インデクサータイプに関する設定の詳細説明を参照してください。

### プロパティインデックス {#the-property-index}

プロパティインデックスは、プロパティの制約を持つが、フルテキストではないクエリに役立ちます。 これは、次の手順に従って実行できます。

1. `http://localhost:4502/crx/de/index.jsp` に移動して CRXDE を開きます。
1. **oak:index** の下に新しいノードを作成します。
1. このノードに **PropertyIndex** という名前を付け、ノードタイプを **oak:QueryIndexDefinition** に設定します。
1. 新しいノードに対して次のプロパティを設定します。

   * **タイプ：** `property` property（String タイプ）
   * **プロパティ名：** `jcr:uuid`（Name タイプ）

   この例では、`jcr:uuid` プロパティに対してインデックスを作成します。このプロパティの役割は、関連付けられたノードの Universally Unique Identifier（UUID）を公開することです。

1. 変更内容を保存します。

プロパティインデックスでは次の設定オプションを使用できます。

* **type** プロパティは、インデックスのタイプを指定するものであり、この例の場合は **property** に設定する必要があります。

* **propertyNames** プロパティは、インデックスに保存されるプロパティのリストを示します。欠落している場合は、プロパティ名の参照値としてノード名が使用されます。この例では、**jcr:uuid** プロパティの役割は、インデックスに追加されるノードの一意識別子（UUID）を公開することです。

* **unique** フラグは、**true** に設定されている場合、プロパティインデックスに対して一意性制約を付加します。

* **declaringNodeTypes** プロパティでは、インデックスが唯一適用される特定のノードタイプを指定できます。
* **reindex** フラグが **true** に設定されている場合、コンテンツ全体のインデックス再作成をトリガーします。

### 順序付きインデックス {#the-ordered-index}

順序付きインデックスはプロパティインデックスの拡張です。ただし、これは廃止されました。このタイプのインデックスは、[Lucene プロパティインデックス](#the-lucene-property-index)に置き換える必要があります。

### Lucene フルテキストインデックス {#the-lucene-full-text-index}

AEM 6 では、Apache Lucene に基づいたフルテキストインデクサーを使用できます。

フルテキストインデックスが設定されている場合、インデックス付けされる他の条件があるかどうか、およびパスの制約があるかどうかに関係なく、フルテキスト条件を持つすべてのクエリでフルテキストインデックスを使用します。

フルテキストインデックスを設定しない場合、フルテキスト条件が設定されたクエリは想定どおりに機能しません。

インデックスは、非同期のバックグラウンドスレッドによって更新されるので、一部のフルテキスト検索は、バックグラウンドプロセスが完了するまでの短い期間、使用できない場合があります。

次の手順に従って、Lucene フルテキストインデックスを設定できます。

1. CRXDE を開き、**oak:index** の下にノードを作成します。
1. このノードに **LuceneIndex** という名前を付け、ノードタイプを **oak:QueryIndexDefinition** に設定します。
1. ノードに次のプロパティを追加します。

   * **タイプ：** `lucene` （String タイプ）
   * **async：** `async`（String タイプ）

1. 変更内容を保存します。

Lucene インデックスでは次の設定オプションを使用できます。

* **type** プロパティ：インデックスのタイプを指定 - **lucene** に設定。
* **async** プロパティ：**async** に設定。この設定により、インデックス更新プロセスがバックグラウンドスレッドに送信されます。
* **includePropertyTypes** プロパティ：インデックスに含まれるプロパティタイプのサブセットを定義します。
* **excludePropertyNames** プロパティ：インデックスから除外する必要のあるプロパティの名前のリストを定義します。
* **reindex** フラグ：**true** に設定されている場合、コンテンツ全体のインデックス再作成をトリガーします。

### フルテキスト検索について {#understanding-fulltext-search}

この節のドキュメントは、Apache Lucene、Elasticsearch、PostgreSQL、SQLite、MySQL のフルテキストインデックスに適用されます。次の例は、AEM／Oak／Lucene の場合です。

<b>インデックスを作成するデータ</b>

開始点は、インデックスを作成する必要があるデータです。次のドキュメントを例として使用します。

| <b>ドキュメント ID</b> | <b>パス</b> | <b>フルテキスト</b> |
| --- | --- | --- |
| 100 | /content/rubik | 「Rubik はフィンランドのブランドだ」 |
| 200 | /content/rubiksCube | 「ルービックキューブは 1974 年に発明されました。」 |
| 300 | /content/cube | 「キューブは 3 次元の物体です。」 |


<b>転置インデックス</b>

インデックス作成のメカニズムでは、フルテキストを「トークン」と呼ばれる単語に分割し、「転置インデックス」と呼ばれるインデックスを作成します。このインデックスには、単語に対応するドキュメントのリストが含まれています。

短い、一般的な単語（「ストップワード」とも呼ばれる）はインデックスされません。すべてのトークンは小文字に変換され、ステミングが適用されます。

「*-*」などの特殊文字はインデックスされません。

| <b>トークン</b> | <b>ドキュメント ID</b> |
| --- | --- |
| 194 | ..., 200,... |
| ブランド | ..., 100,... |
| キューブ | ..., 200, 300,... |
| ディメンション | 300 |
| 完了 | ..., 100,... |
| インベント | 200 |
| オブジェクト | ..., 300,... |
| ルービック | ..., 100, 200,... |

ドキュメントのリストが並べ替えられます。これは、クエリを実行する際に便利です。

<b>検索中</b>

次に、クエリの例を示します。すべての特殊文字（*&#39;*&#x200B;など）がスペースに置き換えられました。

```
/jcr:root/content//element(\*; cq:Page)`[` jcr:contains('Rubik s Cube')`]`
```

単語はトークン化され、インデックス作成時と同じ方法でフィルタリングされます（例えば、単一文字の単語は削除されます）。この場合、検索対象は次のとおりです。

```
+:fulltext:rubik +:fulltext:cube
```

インデックスは、それらの単語のドキュメントのリストを調べます。ドキュメントが多い場合は、リストが大きくなる場合があります。例えば、次のようなものが含まれていると仮定します。


| <b>トークン</b> | <b>ドキュメント ID</b> |
| --- | --- |
| ルービック | 10, 100, 200, 1000 |
| キューブ | 30, 200, 300, 2000 |


Lucene は、2 つのリスト（または、`n` の単語を検索する場合は、ラウンドロビンの `n` リスト）を往復します。

* 「ルービック」で読み込むと、最初のエントリを取得し、10 とわかります。
* 「キューブ」で読み込むと、最初のエントリ `>` = 10 を取得します。10 が見つからない場合、次は 30 になります。
* 「ルービック」で読み込むと、最初のエントリ `>` = 30 を取得し、100 とわかります。
* 「キューブ」で読み込むと、最初のエントリ `>` = 100 を取得し、200 とわかります。
* 「ルービック」で読み込むと、最初のエントリ `>` = 200 を取得します。200 とわかります。つまり、ドキュメント 200 は両方の用語に一致します。これは記憶されます。
* 「ルービック」で読み込み、次のエントリ 1000 を取得します。
* 「キューブ」で読み込み、最初のエントリ `>` = 1000 を取得し、2000 とわかります。
* 「ルービック」で読み込み、最初のエントリ `>` = 2000 を取得し、リストの最後になります。
* 最後に、検索を停止します。

次の例に示すように、両方の用語を含むとわかったドキュメントは 200 です。

| 200 | /content/rubiksCube | 「ルービックキューブは 1974 年に発明されました。」 |
| --- | --- | --- |

複数のエントリが見つかった場合は、スコアで並べ替えられます。

### Lucene プロパティインデックス {#the-lucene-property-index}

**Oak 1.0.8** 以降では、Lucene を使用すると、フルテキスト以外のプロパティ制約を含むインデックスを作成することができます。

Lucene プロパティインデックスを作成するには、**fulltextEnabled** プロパティを常に false に設定する必要があります。

次のクエリの例について考えてみます。

```xml
select * from [nt:base] where [alias] = '/admin'
```

上記のクエリの Lucene プロパティインデックスを定義するには、以下の定義を追加します。それには、以下の下にノードを作成します。 **`oak:index`:**

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
>通常のプロパティインデックスと比較して、Lucene プロパティインデックスは常に非同期モードで設定されます。そのため、このインデックスから返される結果は、最新のリポジトリの状態を反映していない場合があります。

>[!NOTE]
>
>Lucene プロパティインデックスについて詳しくは、[Apache Jackrabbit Oak Lucene ドキュメントのページ](https://jackrabbit.apache.org/oak/docs/query/lucene.html)を参照してください。

### Lucene アナライザー {#lucene-analyzers}

Oak ではバージョン 1.2.0 以降、Lucene アナライザーをサポートしています。

アナライザーは、ドキュメントのインデックス作成時とクエリの実行時の両方に使用されます。アナライザーは、フィールドのテキストを調査して、トークンストリームを生成します。Lucene アナライザーは、一連のトークナイザークラスおよびフィルタークラスで構成されています。

このアナライザーは、`oak:index` 定義内の `analyzers` ノード（タイプ `nt:unstructured`）を介して定義できます。

インデックスのデフォルトのアナライザーは、analyzers ノードの子の `default` に設定されます。

![chlimage_1-149](assets/chlimage_1-149.png)

>[!NOTE]
>
>使用可能なアナライザーのリストについては、使用中の Lucene バージョンの API ドキュメントを参照してください。

#### アナライザークラスの直接指定 {#specifying-the-analyzer-class-directly}

標準のアナライザーを使用する場合は、次の手順に従って設定できます。

1. `oak:index` ノードの下で、アナライザーで使用するインデックスを見つけます。

1. このインデックスの下に `default` という子ノード（タイプ `nt:unstructured`）を作成します。

1. default ノードに次のプロパティを追加します。

   * **名前:** `class`
   * **タイプ：** `String`
   * **値：** `org.apache.lucene.analysis.standard.StandardAnalyzer`

   この値は、使用するアナライザークラスの名前です。

   また、特定の Lucene バージョンで使用するアナライザーを設定するには、オプションの `luceneMatchVersion` 文字列プロパティを使用することもできます。Lucene 4.7 で使用する場合の有効な構文は次のとおりです。

   * **名前：** `luceneMatchVersion`
   * **タイプ：** `String`
   * **値：** `LUCENE_47`

   `luceneMatchVersion` が指定されない場合、Oak では出荷時の Lucene のバージョンが使用されます。

1. アナライザー設定にストップワードファイルを追加する場合は、`default` ノードの下に新しいノードを作成し、次のプロパティを設定します。

   * **名前：** `stopwords`
   * **タイプ：** `nt:file`

#### 設定によるアナライザーの構成 {#creating-analyzers-via-composition}

アナライザーは、`Tokenizers`、`TokenFilters`、`CharFilters` に基づいて構成することもできます。そのためには、アナライザーを指定し、オプションのトークナイザーとフィルターの子ノードを作成します。これらはリストされた順序で適用されます。[https://wiki.apache.org/solr/AnalyzersTokenizersTokenFilters#Specifying_an_Analyzer_in_the_schema](https://cwiki.apache.org/confluence/display/solr/AnalyzersTokenizersTokenFilters#Specifying_an_Analyzer_in_the_schema) も参照してください。

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

フィルター、charFilters およびトークナイザーの名前は、ファクトリ設定のサフィックスを削除したものです。つまり、次のようになります。

* `org.apache.lucene.analysis.standard.StandardTokenizerFactory` が `standard` になります

* `org.apache.lucene.analysis.charfilter.MappingCharFilterFactory` が `Mapping` になります

* `org.apache.lucene.analysis.core.StopFilterFactory` が `Stop` になります

ファクトリに必要なすべての設定パラメーターは、対象ノードのプロパティとして指定します。

ストップワードの読み込みなど、外部ファイルのコンテンツを読み込む必要がある場合は、対象ファイル用の子ノード（タイプ `nt:file`）を作成することによってコンテンツを指定できます。

### Solr インデックス {#the-solr-index}

Solr インデックスの目的は主にフルテキスト検索ですが、パス、プロパティの制約および主タイプ制約による検索のインデックス作成にも使用できます。つまり、Oak の Solr インデックスは、あらゆる種類の JCR クエリに使用できます。

AEM での統合はリポジトリレベルで実行されるので、Solr は、Oak（AEM に付属する新しいリポジトリ実装）で使用できるインデックスの候補の 1 つです。

AEM インスタンスでリモートサーバーとして機能するように設定できます。

### AEM での単一リモート Solr サーバーの設定 {#configuring-aem-with-a-single-remote-solr-server}

AEM は、リモート Solr サーバーインスタンスと連動するように設定することもできます。

1. 最新バージョンの Solr をダウンロードして解凍します。この方法について詳しくは、[Apache Solr のインストールドキュメント](https://solr.apache.org/guide/6_6/installing-solr.html)を参照してください。
1. 2 つの Solr シャードを作成します。そのためには、Solr の展開先フォルダー内に、各シャード用のフォルダーを作成します。

   * 1 つ目のシャード用に、次のフォルダーを作成します。

   `<solrunpackdirectory>\aemsolr1\node1`

   * 2 つ目のシャード用に、次のフォルダーを作成します。

   `<solrunpackdirectory>\aemsolr2\node2`

1. Solr パッケージ内のサンプルインスタンスを探します。パッケージのルート内の「`example`」というフォルダーにあります。
1. サンプルインスタンスの次のフォルダーを、2 つのシャードフォルダー（`aemsolr1\node1` と `aemsolr2\node2`）にコピーします。

   * `contexts`
   * `etc`
   * `lib`
   * `resources`
   * `scripts`
   * `solr-webapp`
   * `webapps`
   * `start.jar`

1. 2 つのシャードフォルダーのそれぞれに、「`cfg`」というフォルダーを新しく作成します。
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

1. 「**Oak Solr**」サーバープロバイダー下のドロップダウンリストで「**Remote Solr**」を選択します。

1. CRXDE に移動し、管理者としてログインします。
1. **solrIndex** というノードを **oak:index** の下に作成し、次のプロパティを設定します。

   * **タイプ：** solr（文字列タイプ）
   * **async：** async（文字列型）
   * **reindex：** true（ブール値型）

1. 変更内容を保存します。

#### Solr の推奨設定 {#recommended-configuration-for-solr}

以下に、この記事で説明する 3 つの Solr デプロイメントすべてで使用できる基本設定の例を示します。AEM に既に存在する専用プロパティインデックスに対応しているため、他のアプリケーションでは使用しないでください。

この設定を適切に使用するには、アーカイブのコンテンツを直接 Solr ホームディレクトリに配置する必要があります。複数のノードから成るデプロイメントの場合は、各ノードの root フォルダー直下に配置してください。

Solr 推奨設定ファイル

[ファイルを入手](assets/recommended-conf.zip)

### AEM インデックス作成ツール {#aem-indexing-tools}

AEM 6.1 では、AEM 6.0 の次の 2 つのインデックス作成ツールが Adobe Consulting Services Commons ツールセットの一部として統合されています。

1. **クエリの説明**：管理者がクエリの実行方法を理解できるように設計されたツール。
1. **Oak インデックスマネージャー**：既存のインデックスを維持するための web ユーザーインターフェイス。

これらのツールには、AEM ようこそ画面から&#x200B;**ツール／操作／ダッシュボード／診断**&#x200B;を選択してアクセスできます。

これらのツールの使用方法について詳しくは、[操作ダッシュボードに関するドキュメント](/help/sites-administering/operations-dashboard.md)を参照してください。

#### OSGi を使用したプロパティインデックスの作成 {#creating-property-indexes-via-osgi}

ACS 共通パッケージでは、プロパティインデックスの作成に使用できる OSGi 設定も公開しています。

この設定には、web コンソールから「**Ensure Oak Property Index**」を検索してアクセスできます。

![chlimage_1-150](assets/chlimage_1-150.png)

### インデックス作成の問題のトラブルシューティング {#troubleshooting-indexing-issues}

クエリの実行に長くかかる場合や、一般的なシステムの応答が遅くなる場合があります。

この節では、そのような問題の原因を追跡するためにすべきことについての一連の推奨事項と、それらを解決する方法についてのアドバイスを示します。

#### 分析用のデバッグ情報の準備 {#preparing-debugging-info-for-analysis}

[クエリの説明ツール](/help/sites-administering/operations-dashboard.md#explain-query)を使用すると、実行中のクエリに必要な情報を簡単に取得できます。このツールは、ログレベル情報を参照しなくても、処理に時間のかかるクエリのデバッグに必要な正確な情報を収集できます。デバッグ対象となるクエリがわかっている場合は、このツールをお勧めします。

何らかの理由でこのツールを使用できない場合は、インデックスログを単一のファイルに収集し、そのファイルを使用して特定の問題をトラブルシューティングすることができます。

#### ログの有効化 {#enable-logging}

ログを有効にするには、Oak インデックスおよびクエリに関連するカテゴリで&#x200B;**デバッグ**&#x200B;レベルのログを有効にする必要があります。対象のカテゴリは以下の通りです。

* org.apache.jackrabbit.oak.plugins.index
* org.apache.jackrabbit.oak.query
* com.day.cq.search

**com.day.cq.search** カテゴリは、AEM が提供する QueryBuilder ユーティリティを使用している場合にのみ適用できます。

>[!NOTE]
>
>ログは、トラブルシューティングするクエリが実行中の間のみ、デバッグに設定されることが重要です。そうしないと、多くのイベントが時間の経過と共にログに生成されます。このため、必要なログが収集されたら、上記のカテゴリの情報レベルのログに戻ります。

以下の手順に従って、ログを有効にすることができます。

1. ブラウザーで `https://serveraddress:port/system/console/slinglog` を指定します。
1. コンソールの下部にある「**Add new Logger**」ボタンをクリックします。
1. 新しく作成された行で、前述のカテゴリを追加します。「**+**」記号を使用して、1 つのロガーに複数のカテゴリを追加できます。
1. **ログレベル**&#x200B;ドロップダウンリストから「**デバッグ**」を選択します。
1. 出力ファイルを `logs/queryDebug.log` に設定します。この設定によって、すべてのデバッグイベントが 1 つのログファイルに関連付けられます。
1. クエリを実行するか、デバッグ対象のクエリを使用しているページをレンダリングします。
1. クエリを実行したら、ログコンソールに戻り、新しく作成したロガーのログレベルを **INFO** に変更します。

#### インデックスの設定 {#index-configuration}

クエリの評価方法は、インデックスの設定に大きく影響されます。インデックス設定を分析するか、サポートに送信することが重要です。設定を、コンテンツパッケージとして取得することも、JSON レンディションを取得することもできます。

通常、インデックスの設定は CRXDE の `/oak:index` ノードに保存されており、JSON バージョンは次の場所で取得できます。

`https://serveraddress:port/oak:index.tidy.-1.json`

インデックスが別の場所で設定されている場合は、それに応じてパスを変更します。

#### MBean 出力 {#mbean-output}

デバッグ用にインデックス関連の MBean の出力を提供すると役立つ場合があります。手順は次のとおりです。

1. JMX コンソールに移動します。
   `https://serveraddress:port/system/console/jmx`

1. 以下の MBean を検索します。

   * Lucene インデックス統計
   * CopyOnRead サポート統計
   * Oak クエリ統計
   * IndexStats

1. それぞれの MBean をクリックして、パフォーマンス統計を取得します。サポートへの提出が必要な場合に備え、スクリーンショットを取得するか、記録しておきます。

また、これらの統計に関する JSON 形式の情報を、次の URL で取得できます。

* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`

`https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak.tidy.3.json` によっても統合された JMX 出力が提供されます。この出力には、Oak 関連のすべての MBean 詳細が JSON 形式で含まれています。

#### その他の詳細情報 {#other-details}

問題のトラブルシューティングのために、次のようなその他の情報を収集できます。

1. インスタンスが実行されている Oak のバージョン。この情報を確認するには、CRXDE を開き、ようこそページの右下隅にあるバージョンを参照するか、`org.apache.jackrabbit.oak-core` バンドルのバージョンをチェックします。
1. 問題が発生しているクエリの QueryBuilder デバッガーの出力。デバッガーには、`https://serveraddress:port/libs/cq/search/content/querydebug.html` からアクセスできます。
