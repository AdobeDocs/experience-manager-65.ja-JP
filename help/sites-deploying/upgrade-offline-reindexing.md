---
title: オフラインでのインデックス再作成を使用したアップグレード中のダウンタイムの削減
description: AEM のアップグレードを実行する際に、オフラインのインデックス再作成手法を使用して、システムのダウンタイムを削減する方法を説明します。
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
feature: Upgrading
exl-id: 85bc041e-0ab1-42de-8bcc-c98a175d7494
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '1341'
ht-degree: 99%

---

# オフラインでのインデックス再作成を使用したアップグレード中のダウンタイムの削減 {#offline-reindexing-to-reduce-downtime-during-upgrades}

## はじめに {#introduction}

Adobe Experience Manager のアップグレードにおける主な課題の 1 つは、インプレースアップグレードの実行時にオーサー環境に関連するダウンタイムです。コンテンツ作成者は、アップグレード中に環境にアクセスできなくなります。このため、アップグレードの実行に要する時間を最小限に抑えることをお勧めします。大規模なリポジトリ、特に AEM Assets プロジェクトでは、大規模なデータストアと、1 時間あたりの高レベルのアセットアップロードがある場合、Oak インデックスのインデックス再作成は、アップグレード時間のかなりの割合を占めます。

ここでは、アップグレードを実行する&#x200B;**前**&#x200B;に、Oak-run ツールを使用してリポジトリを再インデックスする方法について説明します。実際のアップグレード中のダウンタイムを削減できます。AEM 6.4 以降のバージョンでは、次に示す手順を [Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html) に適用できます。

## 概要 {#overview}

新しいバージョンの AEM では、機能セットが拡張されると、Oak インデックス定義に変更が加えられます。AEM インスタンスのアップグレード時に、Oak インデックスを変更すると、インデックスが強制的に再作成されます。アセットのテキスト（pdf ファイルのテキストなど）が抽出されてインデックスが作成されるので、インデックス再作成はアセットのデプロイメントにはコストがかかります。MongoMK リポジトリを使用すると、データはネットワークを介して保持され、インデックス再作成に要する時間がさらに長くなります。

アップグレード中に多くのユーザーが直面する問題は、ダウンタイム時間の削減です。アップグレード中のインデックス再作成アクティビティを&#x200B;**スキップ**&#x200B;することが解決策となっています。これは、アップグレードを実行する&#x200B;**前**&#x200B;に、新しいインデックスを作成し、アップグレード中にインポートするだけで実現します。

## アプローチ {#approach}

![offline-reindexing-upgrade-text-extraction](assets/offline-reindexing-upgrade-process.png)

アップグレードの前に、[Oak-run](/help/sites-deploying/indexing-via-the-oak-run-jar.md) ツールを使用して、対象となる AEM バージョンのインデックス定義に対してインデックスを作成することです。上の図は、オフラインでのインデックス再作成のアプローチを示しています。

さらに、アプローチで説明した手順の順序は次のとおりです。

1. バイナリからのテキストが最初に抽出されます
2. ターゲットインデックス定義が作成されます
3. オフラインインデックスが作成されます
4. その後、アップグレードプロセス中にインデックスがインポートされます

### テキスト抽出 {#text-extraction}

AEM で完全なインデックス作成を有効にするには、PDF などのバイナリからテキストを抽出し、インデックスに追加します。これは通常、インデックス作成プロセスの高コストな手順です。テキスト抽出は、多数のバイナリを格納するので、特にアセットリポジトリのインデックス再作成に提案される最適化手順です。

![offline-reindexing-upgrade-text-extraction](assets/offline-reindexing-upgrade-text-extraction.png)

システムに保存されたバイナリのテキストは、tika ライブラリを持つ oak-run ツールを使用して抽出できます。実稼働システムのクローンは、アップグレードの前に取得でき、このテキスト抽出プロセスに使用できます。次の手順を実行すると、この処理によってテキストストアが作成されます。

**1.リポジトリをトラバースし、バイナリの詳細を収集します**

この手順では、パスと BLOB ID を含むバイナリのタプルを含む CSV ファイルを生成します。

インデックスを作成するディレクトリから次のコマンドを実行します。次の例では、リポジトリのホームディレクトリを想定しています。

```
java java -jar oak-run.jar tika <nodestore path> --fds-path <datastore path> --data-file text-extraction/oak-binary-stats.csv --generate
```

ここで、`nodestore path` は `mongo_ur` または `crx-quickstart/repository/segmentstore/` です。

`–fds-path` の代わりに `--fake-ds-path=temp` パラメーターを使用して、プロセスを高速化します。

**2.既存のインデックスで使用可能なバイナリテキストストアを再利用**

既存のシステムからインデックスデータをダンプし、テキストストアをエクストラクトします。

次のコマンドを使用して、既存のインデックスデータをダンプできます。

```
java -jar oak-run.jar index <nodestore path> --fds-path=<datastore path> --index-dump
```

ここで、`nodestore path` は `mongo_ur` または `crx-quickstart/repository/segmentstore/` です。

次に、上記のインデックスダンプを使用してストアに入力します。

```
java -jar oak-run.jar tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --index-dir ./indexing-result/index-dumps/<oak-index-name>/data populate
```

ここで、 `oak-index-name` はフルテキストインデックスの名前です（例：「lucene」）。

**3.上記の手順で除外したバイナリに対して、tika ライブラリを使用してテキスト抽出プロセスを実行します**

```
java -cp oak-run.jar:tika-app-1.21.jar org.apache.jackrabbit.oak.run.Main tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --fds-path <datastore path> extract
```

ここで、 `datastore path` はバイナリデータストアへのパスです。

作成したテキストストアは、将来のシナリオでインデックス再作成のために更新および再利用できます。

テキスト抽出プロセスの詳細に関しては、 [Oak-run ドキュメント](https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html)を参照してください。

### オフラインインデックス再作成 {#offline-reindexing}

![offline-reindexing-upgrade-offline-reindexing](assets/offline-reindexing-upgrade-offline-reindexing.png)

アップグレードの前に、Lucene インデックスをオフラインで作成します。MongoMK を使用する場合、MongoMk ノードの 1 つで直接実行することをお勧めします。これにより、ネットワークのオーバーヘッドが回避されます。

インデックスをオフラインで作成するには、以下の手順に従います。

**1.ターゲット AEM バージョンの Oak Lucene インデックス定義を生成します。**

既存のインデックス定義をダンプします。変更を受けたインデックス定義は、対象の AEM バージョンの Adobe Granite リポジトリーバンドルと oak-run を使用して生成されました。

インデックス定義を&#x200B;**ソース** AEM インスタンスからダンプするには、このコマンドを実行します。

>[!NOTE]
>
>インデックス定義のダンプに関する詳細は、[Oak ドキュメント](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#async-index-data) を参照してください。

```
java -jar oak-run.jar index --fds-path <datastore path> <nodestore path> --index-definitions
```

ここで、`datastore path` および `nodestore path` は、**ソース** AEMインスタンスです。

次に、**ターゲット** AEM バージョンから、ターゲットバージョンの Granite リポジトリーバンドルを使用して、インデックスの定義を生成します。

```
java -cp oak-run.jar:bundle-com.adobe.granite.repository.jar org.apache.jackrabbit.oak.index.IndexDefinitionUpdater --in indexing-definitions_source.json --out merge-index-definitions_target.json --initializer com.adobe.granite.repository.impl.GraniteContent
```

>[!NOTE]
>
>上記のインデックス定義の作成プロセスは、 `oak-run-1.12.0` バージョン以降のみでサポートされています。ターゲティングは、Granite リポジトリーバンドル `com.adobe.granite.repository-x.x.xx.jar` を使用して行われます。

上記の手順では、`merge-index-definitions_target.json` という名前の JSON ファイルを作成します。これはインデックス定義です。

**2.リポジトリー** でチェックポイントを作成

実稼動環境用 **source** AEMインスタンスに、有効期間が長いチェックポイントを作成します。これは、リポジトリーのクローンを作成する前に行う必要があります。

`http://serveraddress:serverport/system/console/jmx` にある JMX コンソールを経由して、`CheckpointMBean` に移動し、有効期間が十分に長いチェックポイントを作成します（例：200 日）。これには、`CheckpointMBean#createCheckpoint` を、有効期間（ミリ秒）の引数としての `17280000000` と併せて呼び出します。

その後、新しく作成したチェックポイント ID をコピーし、JMX `CheckpointMBean#listCheckpoints` を使用して有効期間を検証します.

>[!NOTE]
>
>このチェックポイントは、後でインデックスが読み込まれた際に削除されます。

詳細に関しては、Oak ドキュメントの[チェックポイントの作成](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#out-of-band-create-checkpoint)を参照してください。

**生成されたインデックス定義に対してオフラインでのインデックス作成を実行**

Lucene のインデックス再作成は、oak-run を使用してオフラインで実行できます。このプロセスは、`indexing-result/indexes` の下のディスクにインデックスデータを作成します。リポジトリへの書き込みは&#x200B;**行われない**&#x200B;ので、実行中の AEM インスタンスを停止する必要はありません。作成したテキストストアがこのプロセスに入力されます。

```
java -Doak.indexer.memLimitInMB=500 -jar oak-run.jar index <nodestore path> --reindex --doc-traversal-mode --checkpoint <checkpoint> --fds-path <datastore path> --index-definitions-file merge-index-definitions_target.json --pre-extracted-text-dir text-extraction/store

Sample <checkpoint> looks like r16c85700008-0-8
—fds-path: path to data store.
--pre-extracted-text-dir: Directory of pre-extracted text.
merge-index-definitions_target: JSON file having merged definitions for the target AEM instance. indexes in this file will be re-indexed.
```

`--doc-traversal-mode` パラメーターの使用方法は、リポジトリコンテンツをローカルフラットファイルにスプールすることにより、再インデックス時間を大幅に改善するので、MongoMK のインストールで便利です。ただし、リポジトリの 2 倍のサイズのディスク空き容量が必要です。

MongoMK の場合、MongoDB インスタンスに近いインスタンスでこの手順を実行すると、このプロセスを高速化できます。同じマシン上で実行すると、ネットワークのオーバーヘッドを回避できます。

技術的な詳細については、[インデックス作成用の oak-run ドキュメント](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html)を参照してください。

### インデックスの読み込み {#importing-indexes}

AEM 6.4 以降のバージョンでは、AEM には、起動シーケンス時にディスクからインデックスを読み込む機能が組み込まれています。起動時、フォルダー `<repository>/indexing-result/indexes` にインデックスデータが存在するか確認されます。新しいバージョンの&#x200B;**ターゲット** AEM jarで起動する前の[アップグレード処理](in-place-upgrade.md#performing-the-upgrade)中に、事前に作成したインデックスを上記の場所にコピーすることができます。AEM はそのインデックスをリポジトリに読み込み、対応するチェックポイントをシステムから削除します。したがって、再インデックスは完全に回避されます。

## その他のヒントとトラブルシューティング {#troubleshooting}

以下に、役立つヒントとトラブルシューティング手順を示します。

### 実稼動システムへの影響の軽減 {#reduce-the-impact-on-the-live-production-system}

実稼働システムのクローンを作成し、そのクローンを使用して、オフラインインデックスを作成することをお勧めします。これにより、実稼動システムに与える影響を排除できます。ただし、実稼動システムには、インデックスの読み込みに必要なチェックポイントが必要です。したがって、クローンを作成する前にチェックポイントを作成することが重要です。

### Runbook と体験版の実行を準備する {#prepare-a-runbook-and-trial-run}

実稼動環境でアップグレードを実行する前に、[Runbook](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/upgrading/upgrade-planning.html#building-the-upgrade-and-rollback-runbook) を準備し、トライアルを何回か実行することをお勧めします。

### オフラインインデックス付きドキュメントトラバーサルモード {#doc-traversal-mode-with-offline-indexing}

オフラインのインデックス作成では、リポジトリ全体で複数のトラバーサルを実行する必要グアあります。MongoMK のインストールでは、インデックス作成プロセスのパフォーマンスに影響を与えるネットワークを介してリポジトリにアクセスします。選択肢のひとつは、MongoDB レプリカ自体でオフラインインデックス作成プロセスを実行することで、ネットワークのオーバーヘッドをなくすことです。もうひとつの選択肢は、ドキュメントトラバーサルモードの使用です。

コマンドラインパラメーター `—doc-traversal` を oak-run コマンドに追加することで、ドキュメントトラバーサルモードを適用し、オフラインでのインデックス作成を実行します。このモードでは、ローカルディスク内のリポジトリ全体のコピーがフラットファイルとしてスプールされ、インデックス作成の実行に使用されます。
