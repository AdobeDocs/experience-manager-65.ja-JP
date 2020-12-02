---
title: オフライン再インデックスを使用したアップグレード中のダウンタイムの短縮
description: AEMアップグレードの実行時にシステムのダウンタイムを短縮するために、オフライン再インデックス手法を使用する方法について説明します。
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
translation-type: tm+mt
source-git-commit: 9a4ae73c08657195da2741cccdb196bd7f7142c9
workflow-type: tm+mt
source-wordcount: '1343'
ht-degree: 1%

---


# オフライン再インデックスを使用したアップグレード中のダウンタイムの短縮{#offline-reindexing-to-reduce-downtime-during-upgrades}

## 概要 {#introduction}

Adobe Experience Managerのアップグレードにおける主な課題の1つは、インプレースアップグレードを実行する際の作成者環境に関連するダウンタイムです。 コンテンツ作成者は、アップグレード中に環境にアクセスできません。 したがって、アップグレードの実行に要する時間を最小限に抑えることが望ましいです。 大規模なリポジトリ、特にAEM Assetsプロジェクトでは、大量のデータストアと1時間あたりの高レベルのアセットのアップロードが行われるので、Oakインデックスの再インデックス作成は、アップグレード時間の大部分を占めます。

このセクションでは、Oak-runツールを使用して&#x200B;****&#x200B;のアップグレード前にリポジトリのインデックスを再作成し、実際のアップグレード中のダウンタイムを短縮する方法について説明します。 この手順は、AEM 6.4以降のバージョンの[Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html)インデックスに適用できます。

## 概要 {#overview}

AEMの新しいバージョンでは、機能セットが拡張されると、Oakインデックス定義に変更が加えられます。 Oakインデックスに変更を加えた場合、AEMインスタンスをアップグレードすると、強制的に再インデックスが作成されます。 アセットのテキスト（pdfファイルのテキストなど）を抽出してインデックスを作成する場合は、アセットのデプロイメントで再インデックスの作成は高価です。 MongoMKリポジトリでは、データはネットワーク上で保持され、再インデックス作成に要する時間がさらに長くなります。

アップグレード中に、ほとんどのお客様が直面する問題は、ダウンタイム時間を短縮することです。 解決策は、アップグレード中に再インデックスアクティビティを&#x200B;**スキップ**&#x200B;することです。 これは、アップグレードを実行する&#x200B;**以前の**&#x200B;インデックを新しく作成し、アップグレード中にインポートするだけで実現できます。

## アプローチ {#approach}

![offline-reindexing-upgrade-text-抽出](assets/offline-reindexing-upgrade-process.png)

[Oak-run](/help/sites-deploying/indexing-via-the-oak-run-jar.md)ツールを使用して、ターゲットAEMのバージョンのインデックス定義に対して、アップグレード前にインデックスを作成することをお勧めします。 上の図は、オフライン再インデックスのアプローチを示しています。

さらに、アプローチで説明されている手順の順序は次のとおりです。

1. バイナリからのテキストが最初に抽出される
2. ターゲットインデックス定義が作成されます
3. オフラインインデックスが作成されます
4. 次に、アップグレードプロセス中にインデックスがインポートされます

### テキスト抽出 {#text-extraction}

AEMで完全なインデックス付けを可能にするために、PDFなどのバイナリのテキストを抽出し、インデックスに追加する。 これは、インデックス作成プロセスでは通常、高コストな手順です。 テキスト抽出は、多数のバイナリを格納するアセットリポジトリの再インデックス付けを行う場合に特に提唱される最適化手順です。

![offline-reindexing-upgrade-text-抽出](assets/offline-reindexing-upgrade-text-extraction.png)

システムに保存されているバイナリのテキストは、tikaライブラリを使用して、oak-runツールを使用して抽出できます。 本番システムのクローンは、アップグレード前に取得でき、このテキスト抽出プロセスに使用できます。 次の手順に従って、このプロセスによってテキストストアが作成されます。

**1.リポジトリを通ってバイナリの詳細を収集**

この手順では、パスとBLOB IDを含むバイナリのタプルを含むCSVファイルを作成します。

インデックスの作成元のディレクトリから次のコマンドを実行します。 次の例では、リポジトリのホームディレクトリを想定しています。

```
java java -jar oak-run.jar tika <nodestore path> --fds-path <datastore path> --data-file text-extraction/oak-binary-stats.csv --generate
```

`nodestore path`は`mongo_ur`または`crx-quickstart/repository/segmentstore/`です

処理を高速化するには、`–fds-path`の代わりに`--fake-ds-path=temp`パラメーターを使用します。

**2.既存のインデックス**&#x200B;で使用可能なバイナリテキストストアを再利用します。

既存のシステムからインデックスデータをダンプし、テキストストアを抽出します。

次のコマンドを使用して、既存のインデックスデータをダンプできます。

```
java -jar oak-run.jar index <nodestore path> --fds-path=<datastore path> --index-dump
```

`nodestore path`は`mongo_ur`または`crx-quickstart/repository/segmentstore/`です

次に、上記のインデックスダンプを使用してストアを設定します。

```
java -jar oak-run.jar tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --index-dir ./indexing-result/index-dumps/<oak-index-name>/data populate
```

`oak-index-name`はフルテキストインデックスの名前です（例：&quot;lucene&quot;）。

**3.上記の手順**&#x200B;でミスしたバイナリのtikaライブラリを使用して、テキスト抽出プロセスを実行します。

```
java -cp oak-run.jar:tika-app-1.21.jar org.apache.jackrabbit.oak.run.Main tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --fds-path <datastore path> extract
```

`datastore path`はバイナリデータストアへのパスです。

作成したテキストストアは、将来のシナリオで再インデックスを作成する際に更新して再利用できます。

テキスト抽出プロセスに関する詳細は、[Oak-runドキュメント](https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html)を参照してください。

### オフライン再インデックス{#offline-reindexing}

![offline-reindexing-upgrade-offline-reindexing](assets/offline-reindexing-upgrade-offline-reindexing.png)

アップグレード前にLuceneインデックスをオフラインで作成します。 MongoMKを使用する場合は、ネットワークのオーバーヘッドを避けるため、MongoMkノードの1つで直接実行することをお勧めします。

インデックスをオフラインで作成するには、次の手順に従ってください。

**1.ターゲットAEMバージョン**&#x200B;のOak Luceneインデックス定義を生成します

既存のインデックス定義をダンプします。 ターゲットのAEMバージョンとoak-runのAdobeGraniteリポジトリバンドルを使用して、変更されたインデックス定義が生成されました。

**source** AEMインスタンスからインデックス定義をダンプするには、次のコマンドを実行します。

>[!NOTE]
>
>インデックス定義のダンピングの詳細については、[Oakのドキュメント](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#async-index-data)を参照してください。

```
java -jar oak-run.jar index --fds-path <datastore path> <nodestore path> --index-definitions
```

`datastore path`と`nodestore path`は、**source** AEMインスタンスの値です。

次に、ターゲット版のGraniteリポジトリバンドルを使用して、**ターゲット版** AEM版からインデックス定義を生成します。

```
java -cp oak-run.jar:bundle-com.adobe.granite.repository.jar org.apache.jackrabbit.oak.index.IndexDefinitionUpdater --in indexing-definitions_source.json --out merge-index-definitions_target.json --initializer com.adobe.granite.repository.impl.GraniteContent
```

>[!NOTE]
>
> 上記のインデックス定義の作成プロセスは、`oak-run-1.12.0`以降のバージョンでのみサポートされます。 ターゲット設定は、Graniteリポジトリバンドル`com.adobe.granite.repository-x.x.xx.jar`を使用して行われます。

上記の手順では、`merge-index-definitions_target.json`という名前のJSONファイルを作成します。これはインデックス定義です。

**2.リポジトリでのチェックポイントの作成**

本番用&#x200B;**ソース** AEMインスタンスに長いライフタイムのチェックポイントを作成します。 これは、リポジトリをクローンする前に行う必要があります。

`http://serveraddress:serverport/system/console/jmx`にあるJMXコンソールを使用して、`CheckpointMBean`に移動し、十分な長い期間（200日など）のチェックポイントを作成します。 この場合、`CheckpointMBean#createCheckpoint`を`17280000000`と共に呼び出し、ライフタイム期間の引数としてミリ秒で指定します。

この処理が完了したら、新しく作成したチェックポイントIDをコピーし、JMX `CheckpointMBean#listCheckpoints`を使用して有効期間を検証します。

>[!NOTE]
>
> このチェックポイントは、インデックスが後でインポートされると削除されます。

詳細については、Oakのドキュメントの[チェックポイントの作成](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#out-of-band-create-checkpoint)を参照してください。

**生成されたインデックス定義に対してオフラインインデックス作成を実行します**

Luceneの再インデックスは、oak-runを使用してオフラインで実行できます。 このプロセスは、`indexing-result/indexes`の下のディスクにインデックスデータを作成します。 リポジトリに&#x200B;**書き込みを**&#x200B;行わないので、実行中のAEMインスタンスを停止する必要はありません。 作成したテキストストアは、次の処理に入力されます。

```
java -Doak.indexer.memLimitInMB=500 -jar oak-run.jar index <nodestore path> --reindex --doc-traversal-mode --checkpoint <checkpoint> --fds-path <datastore path> --index-definitions-file merge-index-definitions_target.json --pre-extracted-text-dir text-extraction/store

Sample <checkpoint> looks like r16c85700008-0-8
—fds-path: path to data store.
--pre-extracted-text-dir: Directory of pre-extracted text.
merge-index-definitions_target: JSON file having merged definitions for the target AEM instance. indexes in this file will be re-indexed.
```

`--doc-traversal-mode`パラメーターはMongoMKのインストールで使用すると便利です。リポジトリの内容をローカルフラットファイルにスプールすることで、再インデックス時間が大幅に短縮されます。 ただし、リポジトリのサイズと同じ重複領域が追加で必要になります。

MongoMKの場合、この手順がMongoDBインスタンスに近いインスタンスで実行されると、このプロセスが高速化されます。 同じマシン上で実行すると、ネットワークのオーバーヘッドが回避される場合があります。

技術的な詳細については、[oak-runのドキュメントの](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html)に記載されているインデックス作成に関するドキュメントを参照してください。

### インデックスのインポート{#importing-indexes}

AEM 6.4以降のバージョンでは、AEMには、起動シーケンスでディスクからインデックスをインポートする機能が組み込まれています。 フォルダ`<repository>/indexing-result/indexes`は、起動中にインデックスデータが存在するかどうかを監視します。 **ターゲット** AEM jarの新しいバージョンから開始する前に、[アップグレードプロセス](in-place-upgrade.md#performing-the-upgrade)の実行中に、事前に作成したインデックスを上記の場所にコピーできます。 AEMはそれをリポジトリにインポートし、対応するチェックポイントをシステムから削除します。 これにより、再インデックスを完全に回避する。

## その他のヒントとトラブルシューティング{#troubleshooting}

次に、役立つヒントとトラブルシューティングの手順を示します。

### 本番システムへの影響の軽減{#reduce-the-impact-on-the-live-production-system}

本番システムのクローンを作成し、そのクローンを使用してオフラインインデックスを作成することをお勧めします。 これにより、本番システムに与える潜在的な影響を排除できます。 ただし、インデックスのインポートに必要なチェックポイントは、実稼働システムに存在する必要があります。 したがって、クローンを作成する前にチェックポイントを作成することが重要です。

### Runbookと体験版の実行の準備{#prepare-a-runbook-and-trial-run}

[Runbook](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/upgrading/upgrade-planning.html#building-the-upgrade-and-rollback-runbook)を準備し、アップグレードを実稼動環境で実行する前に、いくつかの試用を行うことをお勧めします。

### オフラインインデックス付きのDoc Traversalモード{#doc-traversal-mode-with-offline-indexing}

オフラインインデックスの作成には、リポジトリ全体の複数のトランザクションが必要です。 MongoMKのインストールでは、インデックス作成プロセスのパフォーマンスに影響を与えるネットワークを介してリポジトリにアクセスします。 1つは、MongoDBレプリカ自体でオフラインインデックス作成処理を実行する方法です。これにより、ネットワークのオーバーヘッドが解消されます。 もう1つの方法は、doc traversalモードを使用する方法です。

Doc traversalモードは、オフラインインデックスを作成するoak-runコマンドにコマンドラインパラメータ`—doc-traversal`を追加することで適用できます。 このモードは、ローカルディスク内のリポジトリ全体のコピーをフラットファイルとしてスプールし、インデックス作成の実行に使用します。
