---
title: SRP 用の Solr 設定
description: 1 つの Apache Solr のインストールは、異なるコレクションを使用することで、ノードストア (Oak) と共通ストア (SRP) の間で共有できます
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: a9fc9c06-b9e6-4a5e-ab5e-0930ecd4b51b
source-git-commit: 1f1deb4f5d2033420aa1cece95666894b2f56aad
workflow-type: tm+mt
source-wordcount: '1423'
ht-degree: 3%

---

# SRP 用の Solr 設定 {#solr-configuration-for-srp}

## AEM Platform 用 Solr {#solr-for-aem-platform}

An [Apache Solr](https://solr.apache.org/) インストールは、 [ノードストア](../../help/sites-deploying/data-store-config.md) (Oak) および [共通店](working-with-srp.md) (SRP) 別のコレクションを使用。

Oak コレクションと SRP コレクションの両方を集中的に使用する場合は、パフォーマンス上の理由から 2 つ目の Solr をインストールすることができます。

実稼動環境の場合、 [SolrCloud モード](#solrcloud-mode) では、スタンドアロンモード（単一のローカル Solr 設定）よりも高いパフォーマンスを提供します。

### 要件 {#requirements}

Apache Solr をダウンロードしてインストールします。

* [バージョン 7.0](https://archive.apache.org/dist/lucene/solr/7.0.0/)

* Solr には Java™ 1.7 以降が必要です
* サービスは不要です
* 実行モードの選択：

   * スタンドアロンモード
   * [SolrCloud モード](#solrcloud-mode) （実稼動環境に推奨）

* 多言語検索 (MLS) の選択

   * [標準の MLS のインストール](#installing-standard-mls)
   * [高度な MLS のインストール](#installing-advanced-mls)

## SolrCloud モード {#solrcloud-mode}

[SolrCloud](https://solr.apache.org/guide/6_6/solrcloud.html) 実稼動環境では、モードをお勧めします。 SolrCloud モードで実行する場合は、多言語検索 (MLS) をインストールする前に、SolrCloud をインストールして設定する必要があります。

SolrCloud のインストール手順に従うことをお勧めします。

* 同じサーバー上の 3 つの SolrCloud ノード。
* 外部の Apache ZooKeeper。

メモリ使用量とガベージコレクションを調整する JVM を設定することもお勧めします。

### JVM 設定例 {#jvm-configuration-example}

```shell
JVM_OPTS="-server -Xmx2048m -XX:+UseConcMarkSweepGC -XX:+CMSClassUnloadingEnabled -Xloggc:../logs/gc.log -XX:+PrintGCDetails -XX:+PrintGCDateStamps -Djava.awt.headless=true"
```

### SolrCloud のコマンド設定 {#solrcloud-setup-commands}

SolrCloud モードで実行する場合は、MLS をインストールする前に、を使用し、次の SolrCloud 設定コマンドに関する知識が必要です。

#### 1. ZooKeeper に設定をアップロードする {#upload-a-configuration-to-zookeeper}

参照：
[https://solr.apache.org/guide/6_6/command-line-utilities.html](https://solr.apache.org/guide/6_6/command-line-utilities.html)

使用方法： sh ./scripts/cloud-scripts/zkcli.sh \
-cmd upconfig \
-zkhost *server:port* \
-confname *myconfig-name *\
-solrhome *solr-home-path* \
-confdir *config-dir*

#### 2.コレクションを作成する {#create-a-collection}

参照：
[https://solr.apache.org/guide/6_6/solr-control-script-reference.html#SolrControlScriptReference-Create](https://solr.apache.org/guide/6_6/solr-control-script-reference.html#SolrControlScriptReference-Create)

使用方法： 。/bin/solr create \
-c *mycollection-name*\
-d *config-dir* \
-n *myconfig-name* \
-p *ポート*\
-s *破片数* \
-rf *レプリカ数*

#### 3.コレクションを設定セットにリンクする {#link-a-collection-to-a-configuration-set}

既に ZooKeeper にアップロード済みの設定にコレクションをリンクします。

参照：
[https://solr.apache.org/guide/6_6/command-line-utilities.html](https://solr.apache.org/guide/6_6/command-line-utilities.html)

使用方法： sh ./scripts/cloud-scripts/zkcli.sh \
-cmd linkconfig \
-zkhost *server:port* \
-collection *mycollection-name* \
-confname *myconfig-name*

### 標準の MLS と高度な MLS の比較 {#comparison-of-standard-and-advanced-mls}

AEM Communitiesの多言語検索 (MLS) は、Solr プラットフォーム向けに構築されており、英語を含むすべてのサポート言語で検索を改善できます。

AEM Communities向けの MLS は、標準の MLS または高度な MLS として使用できます。 標準の MLS には Solr の設定のみが含まれ、プラグインやリソースファイルは除外されます。 高度な MLS はより包括的なソリューションで、Solr の設定、プラグイン、関連リソースが含まれます。

標準の MLS には、次の言語のコンテンツ検索の機能強化が含まれています。

* 英語：単語派生を一致させようとするステマーが改善されました。
* 日本語：半角文字の日本語トークン化を改善しました。

高度な MLS では、次の言語でのコンテンツ検索の機能が強化されています。

* 英語：ステマーを lemmatizer に置き換えました。
* ドイツ語：分解装置を追加しました。
* フランス語：配信処理を追加しました。
* 中国語（簡体字）：よりスマートなトークン化機能が追加されました。
* 各種言語：ステマー、ストップワードリストおよび標準化ツールが追加されました。

高度な MLS では、すべて以下の 33 言語がサポートされています。

| アラビア語 | ドイツ語 | ノルウェー語 |
|---|---|---|
| ブルガリア語 | ギリシャ語 | ポーランド語 |
| 簡体字中国語 | ハイチ語 | ポルトガル語 |
| 中国語 (繁体) | ヘブライ語 | ルーマニア語 |
| チェコ語 | ハンガリー語 | ロシア語 |
| デンマーク語 | インドネシア語 | スロバキア語 |
| オランダ語 | イタリア語 | スロベニア語 |
| 英語 | 日本語 | スペイン語 |
| エストニア語 | 韓国語 | スウェーデン語 |
| フィンランド語 | ラトビア語 | タイ語 |
| フランス語 | リトアニア語 | トルコ語 |

#### AEM 6.1 Solr 検索、標準の MLS、高度な MLS の比較 {#comparison-of-aem-solr-search-standard-mls-and-advanced-mls}

**注意**:AEM 6.1 は、AEM 6.1 Communities FP3 以前を指します。

![compare-solr-mls](assets/compare-solr-mls.png)

### 標準の MLS のインストール {#installing-standard-mls}

SRP コレクション（MSRP または DSRP）で標準多言語検索 (MLS) をサポートするには、Solr の設定ファイルを 2 つ変更する必要があります。

* **schema.xml**
* **solrconfig.xml**

Solr 4.10 用の標準の MLS ファイル (schema.xml、solrconfig.xml)。

Solr 5.x 用の標準の MLS ファイル (schema.xml、solrconfig.xml)

標準の MLS ファイルはAEMリポジトリに保存されます。

**注意**:Solr ファイルは msrp/フォルダーに格納されますが、DSRP 用にも格納されます（変更は必要ありません）。

**ダウンロード手順**：置換 `solrX` 次を使用 `solr4` または `solr5` 必要に応じて。

1. CRXDE|Lite を使用して、次の場所を特定します。

   * `/libs/social/config/datastore/msrp/solrX/schema.xml`
   * `/libs/social/config/datastore/msrp/solrX/solrconfig.xml`

1. Solr がデプロイされているローカルサーバーにダウンロードします。

   * 次を見つけます。 `jcr:content` ノードの `jcr:data` プロパティ。
   * ダウンロードを開始するには、「 `view`.
   * ファイルが適切な名前とエンコーディング (UTF8) で保存されていることを確認します。

1. スタンドアロンモードまたは SolrCloud モードのインストール手順に従います。

#### SolrCloud モード — 標準の MLS {#solrcloud-mode-standard-mls}

1. SolrCloud モードで Solr をインストールして設定します。
1. 新しい設定を準備します。

   1. new-config-dir*を作成します。例： `solr-install-dir*/myconfig/`

   1. 既存の Solr 設定ディレクトリの内容をにコピーします。 *new-config-dir*

      * Solr4 の場合：コピー `solr-install-dir/example/solr/collection1/conf/`
      * Solr5 の場合：コピー `solr-install-dir/server/solr/configsets/data_driven_schema_configs/`

   1. ダウンロードした **schema.xml** および **solrconfig.xml** から *new-config-dir* 既存のファイルを上書きします。

1. [新しい設定をアップロード](#upload-a-configuration-to-zookeeper) ZooKeeper へ。
1. [コレクションの作成](#create-a-collection) 必要なパラメータ（シャードの数、レプリカの数、構成名など）の指定
1. コレクションの作成時に設定名が指定されていなかった場合、 [この新しく作成したコレクションをリンク](#link-a-collection-to-a-configuration-set) 設定が ZooKeeper にアップロードされました。

1. MSRP の場合は、を実行します。 [MSRP インデックス再作成ツール](msrp.md#msrp-reindex-tool)（このインストールが新規の場合を除く）。

#### スタンドアロンモード — 標準の MLS {#standalone-mode-standard-mls}

1. スタンドアロンモードで Solr をインストールします。
1. Solr5 を実行する場合は、（Solr4 と同様に）collection1 を作成します。

   * `./bin/solr start`
   * `./bin/solr create_core -c collection1 -d sample_techproducts_configs`

1. バックアップ **schema.xml** および **solrconfig.xml** Solr の config ディレクトリに次のように入力します。

   * Solr4 の場合： `solr-install-dir/example/solr/collection1/conf/`
   * Solr5 用に作成： `solr-install-dir/server/solr/collection1/conf/`

1. ダウンロードした **schema.xml** および **solrconfig.xml** を同じディレクトリに追加します。

1. Solr を再起動します。
1. MSRP の場合は、を実行します。 [MSRP インデックス再作成ツール](#msrpreindextool)（このインストールが新規の場合を除く）。

### 高度な MLS のインストール {#installing-advanced-mls}

高度な MLS をサポートする SRP コレクション（MSRP または DSRP）の場合、カスタムスキーマと Solr 設定に加えて、新しい Solr プラグインが必要です。 必要な項目はすべて、ダウンロード可能な zip ファイルにパッケージ化されます。 また、Solr がスタンドアロンモードでデプロイされる場合に使用するインストールスクリプトも含まれています。

高度な MLS パッケージを入手するには、 [高度な MLS のAEM](deploy-communities.md#aem-advanced-mls) （ドキュメントのデプロイ節）を参照してください。

SolrCloud またはスタンドアロンモードでインストールを開始するには、次の手順を実行します。

* AEM-SOLR-MLS zip アーカイブを Solr をホストするサーバーにダウンロードします。
* アーカイブを解凍します。

#### SolrCloud モード — 高度な MLS {#solrcloud-mode-advanced-mls}

インストール手順 — Solr4 と Solr5 のいくつかの違いに注意してください。

1. SolrCloud モードで Solr をインストールして設定します。
1. 高度な MLS パッケージの内容をディスクに抽出します。 内容は次のとおりです。

   * **schema.xml**
   * **solrconfig.xml**
   * **ストップワード/** フォルダー
   * **プロファイル/** フォルダー
   * **extra-libs/** フォルダー

1. 新しい設定を準備します。

   1. の作成 *new-config-dir*

      * 例： `solr-install-dir/myconfig/`
      * サブフォルダーの作成 `stopwords/` および `lang/`

   1. 既存の Solr config dir の内容をにコピーします。 *new-config-dir*

      * Solr4 の場合：コピー `solr-install-dir/example/solr/collection1/conf/`
      * Solr5 の場合：コピー `solr-install-dir/server/solr/configsets/data_driven_schema_configs/`

   1. 抽出した **schema.xml** および **solrconfig.xml** から *new-config-dir* 既存のファイルを上書きします。
   1. Solr5 の場合：コピー `solr_install_dir/server/solr/configsets/sample_techproducts_configs/conf/lang/*.txt` から `new-config-dir/lang/`
   1. 抽出した **ストップワード/** フォルダー *new-config-dir* 結果として `new-config-dir/stopwords/*.txt`

1. [新しい設定をアップロード](#upload-a-configuration-to-zookeeper) ZooKeeper へ
1. 新しい **プロファイル/** フォルダー…

   * Solr4 の場合：各ノードの resources/フォルダーにコピーします。
   * Solr5 の場合：各 Solr インストールの server/resources/フォルダーにコピーします。 すべてのノードが同じ Solr インストールディレクトリにある場合、この手順は 1 回だけ実行されます。

1. の作成 **lib/** SolrCloud の各ノードの solr-home ディレクトリ（solr.xml を含む）内のフォルダー。 次の場所の jar を各ノードの新しい lib/フォルダーにコピーします。

   * **extra-libs/** 高度な MLS パッケージから抽出される
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

1. [コレクションの作成](#create-a-collection) 必要なパラメータ（シャードの数、レプリカの数、構成名など）の指定
1. 設定名が *not* コレクションの作成時に提供されます。 [この新しく作成したコレクションをリンク](#link-a-collection-to-a-configuration-set) 設定が ZooKeeper にアップロードされました。

1. MSRP の場合は、を実行します。 [MSRP インデックス再作成ツール](#msrpreindextool)（このインストールが新規の場合を除く）。

#### スタンドアロンモード — 高度な MLS {#standalone-mode-advanced-mls}

高度な MLS パッケージには、インストールスクリプトが含まれています。

パッケージの内容が、スタンドアロンの Solr サーバーをホストするサーバーに抽出されたら、インストールスクリプトを実行して、必要なリソースと設定ファイルをインストールします。

* スタンドアロンモードで Solr をインストールします。
* Solr5 を実行する場合は、（Solr4 と同様に）collection1 を作成します。

   * `./bin/solr start`
   * `./bin/solr create_core -c collection1 -d sample_techproducts_configs`

* インストールスクリプトの実行：インストール [-v 4|5] [-d solhome] [-c collectionpath]
場所：

   * -d solhome

     Solr インストールディレクトリ

   * -c collectionpath

     solr 内のコレクションパス

   * --help

     印刷コマンドラインオプション

   * -v [4|5]

     solr のバージョンを設定

* Solr 4.10.4の例：

   * Install.bat -v 4 -d c:/solr-4.10.4 -c:/solr-4.10.4/example/solr/collection1

* Solr 5.4.0 の場合の例：

   * Install.sh -v 5 -d /tmp/solr-5.4.0 -c /tmp/solr-5.4.0/server/solr/collection1

**メモ**：

* インストールスクリプトは、新しいバージョンをインストールする前に、&quot;.orig&quot;を追加して schema.xml と solrconfig.xml をバックアップします。

### solrconfig.xml について {#about-solrconfig-xml}

The **solrconfig.xml** ファイルは、自動コミット間隔と検索の表示を制御し、テストと調整が必要です。

`<autoCommit>`：デフォルトでは、安定したストレージへのハードコミットである自動コミット間隔は 15 秒に設定されています。 検索表示のデフォルト値は、コミット前のインデックスを使用する。

検索を変更して、コミットによる変更を反映するように更新されたインデックスを使用するには、含まれる `openSearcher` を true に設定します。

`autoSoftCommit`:「ソフト」コミットでは、変更が確実に表示されます（インデックスが更新されます）が、変更が安定したストレージ（ハードコミット）に同期されることは確認されません。 その結果、パフォーマンスが向上します。 デフォルトでは、 `autoSoftCommit` が含まれると無効になります `maxTime` -1 に設定します。
