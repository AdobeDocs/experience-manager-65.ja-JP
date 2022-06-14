---
title: SRP 用の Solr 設定
seo-title: Solr Configuration for SRP
description: 別々のコレクションを使用することで、1 つの Apache Solr をノードストア（Oak）と共通ストア（SRP）の間で共有できます
seo-description: An Apache Solr installation may be shared between the node store (Oak) and common store (SRP) by using different collections
uuid: 7356343d-073c-4266-bdcb-c7e999281476
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e228f1db-91ea-4ec3-86da-06d89d74bc72
role: Admin
exl-id: a9fc9c06-b9e6-4a5e-ab5e-0930ecd4b51b
source-git-commit: 1d334c42088342954feb34f6179dc5b134f81bb8
workflow-type: tm+mt
source-wordcount: '1457'
ht-degree: 49%

---

# SRP 用の Solr 設定 {#solr-configuration-for-srp}

## AEM プラットフォーム用の Solr {#solr-for-aem-platform}

別々のコレクションを使用することで、1 つの [Apache Solr](https://lucene.apache.org/solr/) を[ノードストア](../../help/sites-deploying/data-store-config.md)（Oak）と[共通ストア](working-with-srp.md)（SRP）の間で共有できます。

Oak と SRP のコレクションがどちらも高頻度で使用される場合は、パフォーマンス上の理由から 2 つ目の Solr をインストールすることもできます。

実稼動環境の場合、 [SolrCloud モード](#solrcloud-mode) では、スタンドアロンモード（単一のローカル Solr 設定）よりも高いパフォーマンスを提供します。

### 要件 {#requirements}

Apache Solr のダウンロードとインストール：

* [バージョン 7.0](https://archive.apache.org/dist/lucene/solr/7.0.0/)

* Solr には Java 1.7 以降が必要です。
* サービスは不要
* 実行モードの選択：

   * スタンドアロンモード
   * [SolrCloud モード](#solrcloud-mode)（実稼動環境で推奨）

* 多言語検索 (MLS) の選択

   * [標準の MLS のインストール](#installing-standard-mls)
   * [高度な MLS のインストール](#installing-advanced-mls)

## SolrCloud モード {#solrcloud-mode}

[SolrCloud](https://solr.apache.org/guide/6_6/solrcloud.html) 実稼動環境では、モードをお勧めします。 SolrCloud モードで実行する場合は、多言語検索 (MLS) をインストールする前に、SolrCloud をインストールして設定する必要があります。

SolrCloud の手順に従い、以下をインストールすることを推奨します。

* 同じサーバー上の 3 つの SolrCloud ノード.
* 外部の Apache ZooKeeper。

また、メモリ使用量とガベージコレクションを調整するために、JVM を設定することを推奨します。

### JVM の設定例 {#jvm-configuration-example}

```shell
JVM_OPTS="-server -Xmx2048m -XX:MaxPermSize=768M -XX:+UseConcMarkSweepGC -XX:+CMSClassUnloadingEnabled -Xloggc:../logs/gc.log -XX:+PrintGCDetails -XX:+PrintGCDateStamps -Djava.awt.headless=true"
```

### SolrCloud セットアップコマンド {#solrcloud-setup-commands}

SolrCloud モードで実行する場合は、MLS をインストールする前に、以下の SolrCloud セットアップコマンドを理解して使用する必要があります。

#### 1. 設定を ZooKeeper にアップロード {#upload-a-configuration-to-zookeeper}

参照：
[https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities](https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities)

使用方法：sh./scripts/cloud-scripts/zkcli.sh \
-cmd upconfig \
-zkhost *server:port* \
-confname *myconfig-name *\
-solrhome *solr-home-path* \
-confdir *config-dir*

#### 2. コレクションを作成 {#create-a-collection}

参照：
[https://cwiki.apache.org/confluence/display/solr/Solr+Start+Script+Reference#SolrStartScriptReference-Create](https://cwiki.apache.org/confluence/display/solr/Solr+Start+Script+Reference#SolrStartScriptReference-Create)

使用方法:
./bin/solr create \
-c *mycollection-name*\
-d *config-dir* \
-n *myconfig-name* \
-p *ポート*\
-s *破片数* \
-rf *レプリカ数*

#### 3. コレクションを設定セットにリンク {#link-a-collection-to-a-configuration-set}

コレクションを ZooKeeper にアップロードした設定にリンクします。

参照：
[https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities](https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities)

使用方法：sh./scripts/cloud-scripts/zkcli.sh \
-cmd linkconfig \
-zkhost *server:port* \
-collection *mycollection-name* \
-confname *myconfig-name*

### 標準の MLS と高度な MLS の比較 {#comparison-of-standard-and-advanced-mls}

AEM Communities の多言語検索（MLS）は、英語を含め、サポートされるすべての言語にまたがる検索の質を向上させる目的で、Solr プラットフォーム用に構築された機能です。

AEM Communities の MLS は、標準の MLS と高度な MLS のどちらかを利用できます。標準の MLS には Solr 設定だけが含まれ、プラグインやリソースファイルは含まれていません。高度な MLS は、より包括的なソリューションであり、Solr 設定に加えてプラグインと関連リソースを含んでいます。

標準の MLS には、以下の言語のコンテンツ検索の機能強化が含まれています。

* 英語：単語の派生を一致させようとした場合のステマーが改善されました。
* 日本語：半角文字の日本語トークン化を改善しました。

高度な MLS には、下の言語のコンテンツ検索の機能強化が含まれています。

* 英語：ステマーを lemmatizer に置き換えました。
* ドイツ語：decompounder を追加しました。
* フランス語：配信処理を追加しました。
* 中国語（簡体字）:よりスマートなトークン化機能が追加されました。
* 各種言語：ステマー、ストップワードリスト、およびノーマライザを追加しました。

高度な MLS では、合計で以下の 33 の言語がサポートされます。

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

標準の多言語検索（MLS）をサポートするには、SRP コレクション（MSRP または DSRP）について、以下の 2 つの Solr の設定ファイルを変更する必要があります。

* **schema.xml**
* **solrconfig.xml**

Solr 4.10 用の標準の MLS ファイル (schema.xml、solrconfig.xml)。

Solr 5.x 用の標準の MLS ファイル (schema.xml、solrconfig.xml)

標準の MLS ファイルは AEM リポジトリに格納されます。

**注意**：Solr ファイルは msrp/ フォルダーに格納されていますが、DSRP にも対応します（変更不要）。

**ダウンロード手順**:置換 `solrX` と `solr4` または `solr5` 必要に応じて。

1. CRXDE|Lite を使用して、次の場所を特定します。

   * `/libs/social/config/datastore/msrp/solrX/schema.xml`
   * `/libs/social/config/datastore/msrp/solrX/solrconfig.xml`

1. Solr がデプロイされているローカルサーバーにダウンロードします。

   * を `jcr:content` ノードの `jcr:data` プロパティ。
   * 選択 `view` をクリックしてダウンロードを開始します。
   * ファイルが適切な名前とエンコーディング (UTF8) で保存されていることを確認します。

1. スタンドアロンモードまたは SolrCloud モードのインストール手順に従います。

#### SolrCloud モード - 標準の MLS {#solrcloud-mode-standard-mls}

1. SolrCloud モードの Solr をインストールして設定します。。
1. 以下の手順で新しい設定を用意します。

   1. new-config-dir*を作成します。例： `solr-install-dir*/myconfig/`

   1. 既存の Solr 設定ディレクトリの内容をにコピーします。 *new-config-dir*

      * Solr4 の場合：コピー `solr-install-dir/example/solr/collection1/conf/`
      * Solr5 の場合：コピー `solr-install-dir/server/solr/configsets/data_driven_schema_configs/`
   1. ダウンロードした **schema.xml** および **solrconfig.xml** から *new-config-dir* 既存のファイルを上書きします。


1. [新しい設定をアップロード](#upload-a-configuration-to-zookeeper) ZooKeeper へ。
1. シャードの数、レプリカ数および設定名など、必要なパラメーターを設定して[コレクションを作成](#create-a-collection)します。
1. コレクションの作成時に設定名が指定されていなかった場合、 [この新しく作成したコレクションをリンク](#link-a-collection-to-a-configuration-set) 設定が ZooKeeper にアップロードされました。

1. MSRP の場合は、を実行します。 [MSRP インデックス再作成ツール](msrp.md#msrp-reindex-tool)（これが新規インストールでない場合）

#### スタンドアロンモード - 標準の MLS {#standalone-mode-standard-mls}

1. スタンドアロンモードの Solr をインストールします。。
1. Solr5 を実行している場合、以下のコマンドで collection1 を作成します（Solr4 と同様）。

   * `./bin/solr start`
   * `./bin/solr create_core -c collection1 -d sample_techproducts_configs`

1. 例えば以下の Solr 設定ディレクトリに **schema.xml** と **solrconfig.xml** にバックアップします。

   * Solr4 の場合： `solr-install-dir/example/solr/collection1/conf/`
   * Solr5 用に作成： `solr-install-dir/server/solr/collection1/conf/`

1. ダウンロードした **schema.xml** および **solrconfig.xml** を同じディレクトリに追加します。

1. Solr を再起動します。
1. MSRP の場合は、を実行します。 [MSRP インデックス再作成ツール](#msrpreindextool)（これが新規インストールでない場合）

### 高度な MLS のインストール {#installing-advanced-mls}

高度な MLS をサポートするための SRP コレクション（MSRP または DSRP）については、カスタムスキーマと Solr 設定に加え、新しい Solr プラグインが必要です。必要な項目はすべて、ダウンロード可能な zip ファイルにパッケージ化されます。 また、Solr がスタンドアロンモードでデプロイされる場合に使用するインストールスクリプトも含まれています。

高度な MLS パッケージを入手するには、 [高度な MLS のAEM](deploy-communities.md#aem-advanced-mls) （ドキュメントのデプロイ節）を参照してください。

SolrCloud モードまたはスタンドアロンモードのどちらかのインストールを開始するには：

* AEM-SOLR-MLS zip アーカイブを Solr をホストするサーバーにダウンロードします。
* アーカイブを解凍します。

#### SolrCloud モード - 高度な MLS {#solrcloud-mode-advanced-mls}

インストール手順 - 以下のとおり、Solr4 と Solr5 で少し違いがある点に注意してください。

1. SolrCloud モードで Solr をインストールして設定します。
1. 高度な MLS パッケージの内容をディスクに抽出します。内容は次のとおりです。

   * **schema.xml**
   * **solrconfig.xml**
   * **stopwords/**&#x200B;フォルダー
   * **profiles/**&#x200B;フォルダー
   * **extra-libs/** フォルダー

1. 以下の手順で新しい設定を用意します。

   1. の作成 *new-config-dir*

      * 例： `solr-install-dir/myconfig/`
      * サブフォルダーの作成 `stopwords/` および `lang/`
   1. 既存の Solr config dir の内容をにコピーします。 *new-config-dir*

      * Solr4 の場合：コピー `solr-install-dir/example/solr/collection1/conf/`
      * Solr5 の場合：コピー `solr-install-dir/server/solr/configsets/data_driven_schema_configs/`
   1. 抽出した **schema.xml** および **solrconfig.xml** から *new-config-dir* 既存のファイルを上書きします。
   1. Solr5 の場合：コピー `solr_install_dir/server/solr/configsets/sample_techproducts_configs/conf/lang/*.txt` から `new-config-dir/lang/`
   1. 抽出した **ストップワード** フォルダー *new-config-dir* 結果として `new-config-dir/stopwords/*.txt`



1. [新しい設定をアップロード](#upload-a-configuration-to-zookeeper) ZooKeeper へ
1. 以下のとおり、新しい **profiles/** フォルダーをコピーします。

   * Solr4 の場合：各ノードの resources/フォルダーにコピーします。
   * Solr5 の場合：各 Solr インストールの server/resources/フォルダーにをコピーします。 すべてのノードが同じ Solr インストールディレクトリにある場合、この手順は 1 回だけ実行されます。

1. の作成 **lib/** SolrCloud の各ノードの solr-home ディレクトリ（solr.xml を含む）内のフォルダー。 次の場所の jar を各ノードの新しい lib/フォルダーにコピーします。

   * 高度な MLS のパッケージから抽出した **extra-libs/**
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

1. シャードの数、レプリカ数および設定名など、必要なパラメーターを設定して[コレクションを作成](#create-a-collection)します。
1. 設定の名前をコレクション作成中に指定しなかった&#x200B;**&#x200B;場合は、ZooKeeper にアップロードした設定に[新しく作成したこのコレクションをリンク](#link-a-collection-to-a-configuration-set)します。。

1. MSRP の場合は、を実行します。 [MSRP インデックス再作成ツール](#msrpreindextool)（これが新規インストールでない場合）

#### スタンドアロンモード - 高度な MLS {#standalone-mode-advanced-mls}

高度な MLS のパッケージには、インストールスクリプトが同梱されています。

スタンドアロンの Solr サーバーをホストしているサーバーにパッケージの内容を抽出したら、必要なリソースと設定ファイルをインストールするために、インストールスクリプトを実行します。

* スタンドアロンモードの Solr をインストールします。。
* Solr5 を実行している場合、以下のコマンドで collection1 を作成します（Solr4 と同様）。

   * `./bin/solr start`
   * `./bin/solr create_core -c collection1 -d sample_techproducts_configs`

* インストールスクリプトを実行します。インストール [-v 4|5] [-d solhome] [-c collectionpath]
場所：

   * -d solhome

      Solr インストールディレクトリ

   * -c collectionpath

      solr 内のコレクションパス

   * --help

      印刷コマンドラインオプション

   * -v [4|5]

      solr のバージョンを設定

* Solr 4.10.4 の場合の例：

   * Install.bat -v 4 -d c:/solr-4.10.4 -c c:/solr-4.10.4/example/solr/collection1

* Solr 5.4.0 の場合の例：

   * Install.sh -v 5 -d /tmp/solr-5.4.0 -c /tmp/solr-5.4.0/server/solr/collection1

**メモ**：

* インストールスクリプトは、新しいバージョンをインストールする前に、&quot;.orig&quot;を追加して schema.xml と solrconfig.xml をバックアップします。

### solrconfig.xml について {#about-solrconfig-xml}

**solrconfig.xml** は、自動コミットの間隔と検索表示を制御するファイルであり、テストと調整が必要です。

`<autoCommit>`:既定では、安定した記憶域に対するハードコミットである AutoCommit 間隔は 15 秒に設定されています。 検索表示のデフォルト値は、コミット前のインデックスを使用する。

検索を変更して、コミットによる変更を反映するように更新されたインデックスを使用するには、含まれる `openSearcher` を true に設定します。

`autoSoftCommit`:「ソフト」コミットでは、変更が表示される（インデックスが更新される）ことを確認しますが、変更が安定したストレージ（ハードコミット）に同期されることは確認されません。 その結果、パフォーマンスが向上します。 デフォルトでは、 `autoSoftCommit` が含まれると無効になります `maxTime` -1 に設定します。
