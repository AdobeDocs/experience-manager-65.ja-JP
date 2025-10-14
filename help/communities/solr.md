---
title: SRP 用の Solr 設定
description: Apache Solr インストールは、異なるコレクションを使用することで、ノードストア（Oak）と共通ストア（SRP）間で共有されます
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: a9fc9c06-b9e6-4a5e-ab5e-0930ecd4b51b
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1423'
ht-degree: 3%

---

# SRP 用の Solr 設定 {#solr-configuration-for-srp}

## AEM Platform 用の Solr {#solr-for-aem-platform}

[Apache Solr](https://solr.apache.org/) インストールは、異なるコレクションを使用して、[&#x200B; ノードストア &#x200B;](../../help/sites-deploying/data-store-config.md) （Oak）と [&#x200B; 共通ストア &#x200B;](working-with-srp.md) （SRP）の間で共有される場合があります。

Oakと SRP の両方のコレクションを集中的に使用する場合は、パフォーマンス上の理由から、2 つ目の Solr をインストールすることがあります。

実稼動環境の場合、[SolrCloud モード &#x200B;](#solrcloud-mode) は、スタンドアロンモード（単一のローカル Solr セットアップ）よりもパフォーマンスが向上します。

### 要件 {#requirements}

Apache Solr をダウンロードしてインストールします。

* [&#x200B; バージョン 7.0](https://archive.apache.org/dist/lucene/solr/7.0.0/)

* Solr には Java™ 1.7 以降が必要です
* サービスは必要ありません
* 実行モードの選択：

   * スタンドアロンモード
   * [SolrCloud モード &#x200B;](#solrcloud-mode) （実稼動環境で推奨）

* 多言語検索（MLS）の選択

   * [標準 MLS のインストール](#installing-standard-mls)
   * [高度な MLS のインストール](#installing-advanced-mls)

## SolrCloud モード {#solrcloud-mode}

実稼動環境には、[SolrCloud](https://solr.apache.org/guide/6_6/solrcloud.html) モードをお勧めします。 SolrCloud モードで実行する場合は、多言語検索（MLS）をインストールする前に、SolrCloud をインストールして設定する必要があります。

SolrCloud の手順に従ってインストールすることをお勧めします。

* 同じサーバー上の 3 つの SolrCloud ノード。
* 外部 Apache ZooKeeper。

また、JVM を設定して、メモリ使用量とガベージコレクションを調整することをお勧めします。

### JVM の設定例 {#jvm-configuration-example}

```shell
JVM_OPTS="-server -Xmx2048m -XX:+UseConcMarkSweepGC -XX:+CMSClassUnloadingEnabled -Xloggc:../logs/gc.log -XX:+PrintGCDetails -XX:+PrintGCDateStamps -Djava.awt.headless=true"
```

### SolrCloud 設定コマンド {#solrcloud-setup-commands}

SolrCloud モードで実行する場合は、MLS をインストールする前に、次の SolrCloud 設定コマンドを使用し、知識を習得しておく必要があります。

#### 1. ZooKeeper に設定をアップロードする {#upload-a-configuration-to-zookeeper}

参照：
[https://solr.apache.org/guide/6_6/command-line-utilities.html](https://solr.apache.org/guide/6_6/command-line-utilities.html)

使用方法：
を押します。/scripts/cloud-scripts/zkcli.sh \
-cmd upconfig \
-zkhost *server:port* \
-confname *myconfig-name *\
-solrhome *solr-home-path* \
-confdir *config-dir*

#### 2. コレクションを作成する {#create-a-collection}

参照：
[https://solr.apache.org/guide/6_6/solr-control-script-reference.html#SolrControlScriptReference-Create](https://solr.apache.org/guide/6_6/solr-control-script-reference.html#SolrControlScriptReference-Create)

使用方法：
./bin/solr create \
-c *mycollection-name*\
-d *config-dir* \
-n *myconfig-name* \
-p *ポート*\
-s *シャードの数* \
-rf *レプリカの数*

#### 3. コレクションを設定セットにリンクする {#link-a-collection-to-a-configuration-set}

既に ZooKeeper にアップロードされている設定にコレクションをリンクします。

参照：
[https://solr.apache.org/guide/6_6/command-line-utilities.html](https://solr.apache.org/guide/6_6/command-line-utilities.html)

使用方法：
を押します。/scripts/cloud-scripts/zkcli.sh \
-cmd linkconfig \
-zkhost *server:port* \
-collection *mycollection-name* \
-confname *myconfig-name*

### 標準 MLS と高度な MLS の比較 {#comparison-of-standard-and-advanced-mls}

AEM Communitiesの多言語検索（MLS）は、Solr プラットフォームに対応するように構築されており、英語を含むすべてのサポート対象言語の検索を改善します。

AEM Communities用 MLS は、標準 MLS または高度な MLS として利用可能です。 標準 MLS には Solr 構成設定のみが含まれ、プラグインまたはリソースファイルは含まれません。 高度な MLS はより包括的なソリューションで、Solr 設定、プラグインおよび関連リソースが含まれます

標準の MLS には、次の言語のコンテンツ検索用の機能強化が含まれています。

* 英語：単語派生に一致させるための語幹改善。
* 日本語：半角文字の日本語トークン化を改善しました。

高度な MLS には、次の言語のコンテンツ検索用の機能強化が含まれています。

* 英語：stemmer を lemmatizer に置き換えます。
* ドイツ語：decompounder を追加。
* フランス語：省略処理を追加。
* 中国語（簡体字）：よりスマートな tokenizer を追加しました。
* 様々な言語：ステマー、ストップワードリスト、ノーマライザーを追加しました。

Advanced MLS では、以下の 33 種類の言語がサポートされています。

| アラビア語 | ドイツ語 | ノルウェー語 |
|---|---|---|
| ブルガリア語 | ギリシャ語 | ポーランド語 |
| 簡体字中国語 | ハイチ語 | ポルトガル語 |
| 中国語 (繁体字) | ヘブライ語 | ルーマニア語 |
| チェコ語 | ハンガリー語 | ロシア語 |
| デンマーク語 | インドネシア語 | スロバキア語 |
| オランダ語 | イタリア語 | スロベニア語 |
| 英語 | 日本語 | スペイン語 |
| エストニア語 | 韓国語 | スウェーデン語 |
| フィンランド語 | ラトビア語 | タイ語 |
| フランス語 | リトアニア語 | トルコ語 |

#### AEM 6.1 Solr 検索、標準 MLS、および詳細 MLS の比較 {#comparison-of-aem-solr-search-standard-mls-and-advanced-mls}

**メモ**:AEM 6.1 は、AEM 6.1 Communities FP3 以前を指します。

![compare-solr-mls](assets/compare-solr-mls.png)

### 標準 MLS のインストール {#installing-standard-mls}

SRP コレクション（MSRP または DSRP）で標準多言語検索（MLS）をサポートするには、Solr の 2 つの設定ファイルを変更する必要があります。

* **schema.xml**
* **solrconfig.xml**

Solr 4.10 の標準 MLS ファイル（schema.xml、solrconfig.xml）。

Solr 5.x の標準 MLS ファイル（schema.xml、solrconfig.xml）

標準の MLS ファイルはAEM リポジトリに格納されます。

**メモ**:Solr ファイルは msrp/ フォルダーに保存されますが、DSRP 用でもあります（変更は不要）。

**ダウンロード手順**:`solrX` を `solr4` または `solr5` （該当する場合）に置き換えます。

1. CRXDE|Lite を使用して、次を検索します。

   * `/libs/social/config/datastore/msrp/solrX/schema.xml`
   * `/libs/social/config/datastore/msrp/solrX/solrconfig.xml`

1. Solr がデプロイされているローカルサーバーにダウンロードします。

   * `jcr:content` ノードの `jcr:data` プロパティを見つけます。
   * ダウンロードを開始するには、「`view`」を選択します。
   * ファイルは必ず適切な名前とエンコーディング（UTF8）で保存してください。

1. スタンドアロンまたは SolrCloud モードのインストール手順に従います。

#### SolrCloud モード – 標準 MLS {#solrcloud-mode-standard-mls}

1. Solr を SolrCloud モードでインストールして設定します。
1. 新しい設定を準備します。

   1. `solr-install-dir*/myconfig/` のような new-config-dir*を作成します。

   1. 既存の Solr 設定ディレクトリの内容を *new-config-dir* にコピーします。

      * Solr4 の場合：`solr-install-dir/example/solr/collection1/conf/` をコピーします
      * Solr5 の場合：`solr-install-dir/server/solr/configsets/data_driven_schema_configs/` をコピーします

   1. 既存のファイルを上書きするには、ダウンロードした **schema.xml** と **solrconfig.xml** を *new-config-dir* にコピーします。

1. [&#x200B; 新しい設定をアップロード &#x200B;](#upload-a-configuration-to-zookeeper) して、ZooKeeper にアクセスします。
1. [&#x200B; コレクションを作成 &#x200B;](#create-a-collection) シャードの数、レプリカの数、設定名など、必要なパラメーターを指定します。
1. コレクションの作成時に設定名が指定されなかった場合は、新しく作成したコレクションに [&#x200B; リンク &#x200B;](#link-a-collection-to-a-configuration-set) し、ZooKeeper にアップロードされた設定を使用します。

1. MSRP の場合、新規インストールでない限り、[MSRP Reindex Tool](msrp.md#msrp-reindex-tool) を実行します。

#### スタンドアロンモード – 標準 MLS {#standalone-mode-standard-mls}

1. Solr をスタンドアロンモードでインストールします。
1. Solr5 を実行している場合は、collection1 を作成します（Solr4 と同様）。

   * `./bin/solr start`
   * `./bin/solr create_core -c collection1 -d sample_techproducts_configs`

1. Solr 設定ディレクトリの **schema.xml** と **solrconfig.xml** のバックアップ（例：）

   * Solr4 の場合：`solr-install-dir/example/solr/collection1/conf/`
   * Solr5 用に作成：`solr-install-dir/server/solr/collection1/conf/`

1. ダウンロードした **schema.xml** と **solrconfig.xml** を同じディレクトリにコピーします。

1. Solr を再起動します。
1. MSRP の場合、新規インストールでない限り、[MSRP Reindex Tool](#msrpreindextool) を実行します。

### 高度な MLS のインストール {#installing-advanced-mls}

SRP コレクション（MSRP または DSRP）が高度な MLS をサポートするには、カスタムスキーマと Solr 設定に加えて、新しい Solr プラグインが必要です。 必要な項目はすべて、ダウンロード可能な zip ファイルにパッケージ化されます。 さらに、Solr をスタンドアロンモードでデプロイする場合に使用するインストールスクリプトが含まれています。

高度な MLS パッケージを入手するには、ドキュメントの展開セクションの [AEM高度な MLS](deploy-communities.md#aem-advanced-mls) を参照してください。

SolrCloud またはスタンドアロンモードのインストールを開始するには：

* AEM-SOLR-MLS zip アーカイブを Solr をホストするサーバーにダウンロードします。
* アーカイブを解凍します。

#### SolrCloud モード – 高度な MLS {#solrcloud-mode-advanced-mls}

インストール手順 – Solr4 と Solr5 のいくつかの違いに注意してください。

1. Solr を SolrCloud モードでインストールして設定します。
1. アドバンスド MLS パッケージの内容をディスクに解凍します。 コンテンツには次の内容を含める必要があります。

   * **schema.xml**
   * **solrconfig.xml**
   * **stopwords/** フォルダー
   * **profiles/** フォルダー
   * **extra-libs/** フォルダー

1. 新しい設定を準備します。

   1. *new-config-dir* を作成

      * `solr-install-dir/myconfig/` など
      * サブフォルダー `stopwords/` および `lang/` の作成

   1. 既存の Solr 設定ディレクトリの内容を *new-config-dir* にコピーします。

      * Solr4 の場合：`solr-install-dir/example/solr/collection1/conf/` をコピーします
      * Solr5 の場合：`solr-install-dir/server/solr/configsets/data_driven_schema_configs/` をコピーします

   1. 抽出した **schema.xml** と **solrconfig.xml** を *new-config-dir* にコピーして、既存のファイルを上書きします。
   1. Solr5 の場合：`solr_install_dir/server/solr/configsets/sample_techproducts_configs/conf/lang/*.txt` を `new-config-dir/lang/` にコピーします
   1. 抽出した **stopwords/** フォルダーを *new-config-dir* にコピーすると、`new-config-dir/stopwords/*.txt` が発生します

1. [&#x200B; 新しい設定をアップロード &#x200B;](#upload-a-configuration-to-zookeeper) して ZooKeeper にアクセスする
1. 新しい **profiles/** フォルダーをコピー…

   * Solr4 の場合：各ノードのリソース/フォルダーにコピーします
   * Solr5 の場合：各 Solr インストールの server/resources/ フォルダーにコピーします。 すべてのノードが同じ Solr インストールディレクトリ内にある場合、この手順は 1 回だけ実行されます。

1. SolrCloud の各ノードの solr-home ディレクトリ（solr.xml が含まれる）に **lib/** フォルダーを作成します。 次の場所から各ノードの新しい lib/ フォルダーに jar をコピーします。

   * **extra-libs/** を拡張 MLS パッケージから抽出
   * *solr-install-dir/contrib/extraction/lib/*.jar
   * *solr-install-dir/dist/solr-cell*.jar
   * *solr-install-dir/contrib/clustering/lib/*.jar
   * *solr-install-dir/dist/solr-clustering*.jar
   * *solr-install-dir/contrib/langid/lib/*.jar
   * *solr-install-dir/dist/solr-langid*.jar
   * *solr-install-dir/contrib/velocity/lib/*.jar
   * *solr-install-dir/dist/solr-velocity*.jar
   * *solr-install-dir/contrib/analysis-extras/lib/*.jar
   * *solr-install-dir/contrib/analysis-extras/lucene-libs/*.jar

1. [&#x200B; コレクションを作成 &#x200B;](#create-a-collection) シャードの数、レプリカの数、設定名など、必要なパラメーターを指定します。
1. コレクションの作成時に設定名が指定されて *ない* 場合は、ZooKeeper にアップロードされた設定と共に、[&#x200B; 新しく作成したコレクションをリンク &#x200B;](#link-a-collection-to-a-configuration-set) します。

1. MSRP の場合、新規インストールでない限り、[MSRP Reindex Tool](#msrpreindextool) を実行します。

#### スタンドアロンモード – 高度な MLS {#standalone-mode-advanced-mls}

インストールスクリプトは詳細 MLS パッケージに含まれています。

パッケージの内容を、スタンドアロン Solr サーバーをホストするサーバーに抽出したら、インストールスクリプトを実行して、必要なリソースと設定ファイルをインストールします。

* Solr をスタンドアロンモードでインストールします。
* Solr5 を実行している場合は、collection1 を作成します（Solr4 と同様）。

   * `./bin/solr start`
   * `./bin/solr create_core -c collection1 -d sample_techproducts_configs`

* インストールスクリプトを実行します。[-v 4|5] [-d solrhome][-c collectionpath をインストール ]
ここで、

   * -d solrhome

     Solr インストールディレクトリ

   * -c collectionpath

     solr のコレクションパス

   * --help

     印刷コマンド ライン オプション

   * -v [4|5]

     solr のバージョンを設定

* Solr 4.10.4 の例：

   * Install.bat -v 4 -d c:/solr-4.10.4 -c:/solr-4.10.4/example/solr/collection1

* Solr 5.4.0 の例：

   * Install.sh -v 5 -d /tmp/solr-5.4.0 -c /tmp/solr-5.4.0/server/solr/collection1

**メモ**：

* インストールスクリプトは、「.orig」を付加して、新しいバージョンをインストールする前に schema.xml と solrconfig.xml をバックアップします

### solrconfig.xml について {#about-solrconfig-xml}

**solrconfig.xml** ファイルは、自動コミットの間隔と検索の可視性を制御するもので、テストとチューニングが必要です。

`<autoCommit>`: デフォルトでは、AutoCommit 間隔（安定したストレージに対するハードコミット）は 15 秒に設定されています。 検索がデフォルトで実行されるのは、事前コミット済みインデックスを使用する場合です。

コミットによる変更を反映するように更新されたインデックスを使用するように検索を変更するには、含まれる `openSearcher` を true に変更します。

`autoSoftCommit`: 「ソフト」コミットの場合は、変更が表示されます（インデックスが更新されます）。ただし、変更が安定したストレージに同期されるわけではありません（ハードコミット）。 その結果、パフォーマンスが向上した。 デフォルトでは、`autoSoftCommit` は無効になっており、含まれる `maxTime` は–1 に設定されています。
