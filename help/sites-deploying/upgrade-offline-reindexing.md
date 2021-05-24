---
title: オフラインでのインデックス再作成を使用したアップグレード中のダウンタイムの削減
description: AEMのアップグレードを実行する際のシステムのダウンタイムを短縮するために、オフラインでのインデックス再作成手法を使用する方法を説明します。
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
feature: アップグレード
exl-id: 85bc041e-0ab1-42de-8bcc-c98a175d7494
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1344'
ht-degree: 1%

---

# オフラインでのインデックス再作成を使用したアップグレード中のダウンタイムの削減{#offline-reindexing-to-reduce-downtime-during-upgrades}

## はじめに {#introduction}

Adobe Experience Managerのアップグレードにおける主な課題の1つは、インプレースアップグレードの実行時にオーサー環境に関連するダウンタイムです。 コンテンツ作成者は、アップグレード中に環境にアクセスできません。 したがって、アップグレードの実行に要する時間を最小限に抑えることをお勧めします。 大規模なリポジトリ、特にAEM Assetsプロジェクトでは、通常、大規模なデータストアと1時間あたりの高レベルのアセットアップロードがあり、Oakインデックスの再インデックスは、アップグレード時間の大部分を占めます。

この節では、Oak-runツールを使用して、アップグレードを実行する前にリポジトリ&#x200B;**のインデックスを再作成し、実際のアップグレード中のダウンタイムを削減する方法について説明します。**&#x200B;上記の手順は、AEM 6.4以降のバージョンの[Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html)インデックスに適用できます。

## 概要 {#overview}

新しいバージョンのAEMでは、機能セットが拡張されると、Oakインデックス定義に変更が加えられます。 AEMインスタンスをアップグレードする際に、Oakインデックスを変更すると、インデックスが強制的に再作成されます。 アセットのテキスト（PDFファイルのテキストなど）が抽出され、インデックスが作成されるので、インデックス再作成はアセットのデプロイメントには高価です。 MongoMKリポジトリを使用すると、データはネットワークを介して保持され、インデックス再作成にかかる時間がさらに長くなります。

アップグレード中にほとんどのお客様が直面する問題は、ダウンタイム時間を短縮することです。 解決策は、アップグレード中にインデックス再作成アクティビティを&#x200B;**スキップ**&#x200B;することです。 これを実現するには、アップグレードを実行する&#x200B;**前の**&#x200B;インデックを新しく作成し、アップグレード中にインポートするだけです。

## アプローチ {#approach}

![offline-reindexing-upgrade-text-extraction](assets/offline-reindexing-upgrade-process.png)

アップグレードの前に、[Oak-run](/help/sites-deploying/indexing-via-the-oak-run-jar.md)ツールを使用して、ターゲットAEMバージョンのインデックス定義に対するインデックスを作成することをお勧めします。 上の図は、オフラインでのインデックス再作成のアプローチを示しています。

さらに、この手順は、アプローチで説明した手順の順序です。

1. 最初にバイナリのテキストが抽出されます
2. ターゲットインデックスの定義が作成される
3. オフラインインデックスが作成される
4. その後、アップグレードプロセス中にインデックスがインポートされます

### テキスト抽出 {#text-extraction}

AEMで完全なインデックスを有効にするには、PDFなどのバイナリのテキストを抽出し、インデックスに追加します。 これは通常、インデックス作成プロセスの高コストな手順です。 テキスト抽出は、多数のバイナリを格納するアセットリポジトリのインデックス再作成を目的とした最適化手順です。

![offline-reindexing-upgrade-text-extraction](assets/offline-reindexing-upgrade-text-extraction.png)

システムに保存されたバイナリのテキストは、 tikaライブラリを持つOak-runツールを使用して抽出できます。 本番システムのクローンは、アップグレードの前に取得でき、このテキスト抽出プロセスに使用できます。 次の手順を実行して、このプロセスによりテキストストアが作成されます。

**1.リポジトリをトラバースし、バイナリの詳細を収集します。**

この手順では、パスとBLOB IDを含むバイナリのタプルを含むCSVファイルを生成します。

インデックスを作成するディレクトリから次のコマンドを実行します。 次の例では、リポジトリのホームディレクトリを前提としています。

```
java java -jar oak-run.jar tika <nodestore path> --fds-path <datastore path> --data-file text-extraction/oak-binary-stats.csv --generate
```

ここで、`nodestore path`は`mongo_ur`または`crx-quickstart/repository/segmentstore/`です。

処理を高速化するには、`–fds-path`の代わりに`--fake-ds-path=temp`パラメーターを使用します。

**2.既存のインデックス**&#x200B;で使用可能なバイナリテキストストアを再利用します。

既存のシステムからインデックスデータをダンプし、テキストストアを抽出します。

次のコマンドを使用して、既存のインデックスデータをダンプできます。

```
java -jar oak-run.jar index <nodestore path> --fds-path=<datastore path> --index-dump
```

ここで、`nodestore path`は`mongo_ur`または`crx-quickstart/repository/segmentstore/`です。

次に、上記のインデックスダンプを使用してストアを設定します。

```
java -jar oak-run.jar tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --index-dir ./indexing-result/index-dumps/<oak-index-name>/data populate
```

`oak-index-name`はフルテキストインデックスの名前です（例：「lucene」）。

**3.上記の手順**&#x200B;でミスされたバイナリのtikaライブラリを使用して、テキスト抽出プロセスを実行します。

```
java -cp oak-run.jar:tika-app-1.21.jar org.apache.jackrabbit.oak.run.Main tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --fds-path <datastore path> extract
```

`datastore path`はバイナリデータストアへのパスです。

作成したテキストストアは、今後のシナリオでインデックス再作成に使用できます。

テキスト抽出プロセスについて詳しくは、[Oak-runのドキュメント](https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html)を参照してください。

### オフラインでのインデックス再作成{#offline-reindexing}

![offline-reindexing-upgrade-offline-reindexing](assets/offline-reindexing-upgrade-offline-reindexing.png)

アップグレードの前に、Luceneインデックスをオフラインで作成します。 MongoMKを使用する場合は、ネットワークのオーバーヘッドを避けるため、いずれかのMongoMkノードで直接実行することをお勧めします。

インデックスをオフラインで作成するには、次の手順に従います。

**1.ターゲットAEMバージョン**&#x200B;のOak Luceneインデックス定義を生成します。

既存のインデックス定義をダンプします。 変更を受けたインデックス定義は、対象のAEMバージョンとoak-runのAdobeGraniteリポジトリバンドルを使用して生成されました。

**source** AEMインスタンスからインデックス定義をダンプするには、次のコマンドを実行します。

>[!NOTE]
>
>インデックス定義のダンプについて詳しくは、[Oakのドキュメント](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#async-index-data)を参照してください。

```
java -jar oak-run.jar index --fds-path <datastore path> <nodestore path> --index-definitions
```

ここで、`datastore path`と`nodestore path`は、**ソース** AEMインスタンスからのものです。

次に、ターゲットバージョンのGraniteリポジトリバンドルを使用して、**ターゲット** AEMバージョンからインデックス定義を生成します。

```
java -cp oak-run.jar:bundle-com.adobe.granite.repository.jar org.apache.jackrabbit.oak.index.IndexDefinitionUpdater --in indexing-definitions_source.json --out merge-index-definitions_target.json --initializer com.adobe.granite.repository.impl.GraniteContent
```

>[!NOTE]
>
> 上記のインデックス定義の作成プロセスは、`oak-run-1.12.0`バージョン以降でのみサポートされます。 ターゲティングはGraniteリポジトリバンドル`com.adobe.granite.repository-x.x.xx.jar`を使用しておこないます。

上記の手順では、インデックス定義である`merge-index-definitions_target.json`というJSONファイルを作成します。

**2.リポジトリ内にチェックポイントを作成します。**

本番用の&#x200B;**ソース** AEMインスタンスに長い有効期間のチェックポイントを作成します。 これは、リポジトリのクローンを作成する前におこなう必要があります。

`http://serveraddress:serverport/system/console/jmx`にあるJMXコンソールを使用して、`CheckpointMBean`に移動し、有効期間が十分に長いチェックポイントを作成します（例：200日）。 この場合は、 `CheckpointMBean#createCheckpoint`を呼び出し、全期間（ミリ秒）の引数として`17280000000`を指定します。

これが完了したら、新しく作成したチェックポイントIDをコピーし、JMX `CheckpointMBean#listCheckpoints`を使用して有効期間を検証します。

>[!NOTE]
>
> このチェックポイントは、後でインデックスがインポートされると削除されます。

詳しくは、Oakのドキュメントの[チェックポイントの作成](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#out-of-band-create-checkpoint)を参照してください。

**生成されたインデックス定義に対してオフラインインデックス作成を実行する**

Luceneのインデックス再作成は、oak-runを使用してオフラインで実行できます。 このプロセスは、`indexing-result/indexes`の下のディスクにインデックスデータを作成します。 リポジトリに&#x200B;**書き込みを行わない**&#x200B;ので、実行中のAEMインスタンスを停止する必要はありません。 作成したテキストストアは、次の処理に入ります。

```
java -Doak.indexer.memLimitInMB=500 -jar oak-run.jar index <nodestore path> --reindex --doc-traversal-mode --checkpoint <checkpoint> --fds-path <datastore path> --index-definitions-file merge-index-definitions_target.json --pre-extracted-text-dir text-extraction/store

Sample <checkpoint> looks like r16c85700008-0-8
—fds-path: path to data store.
--pre-extracted-text-dir: Directory of pre-extracted text.
merge-index-definitions_target: JSON file having merged definitions for the target AEM instance. indexes in this file will be re-indexed.
```

`--doc-traversal-mode`パラメーターは、リポジトリコンテンツをローカルフラットファイルにスプールすることでインデックス再作成時間が大幅に向上するので、MongoMKインストールで便利です。 ただし、リポジトリの2倍のサイズの追加のディスク領域が必要です。

MongoMKの場合、この手順をMongoDBインスタンスに近いインスタンスで実行すると、このプロセスを高速化できます。 同じマシン上で実行する場合、ネットワークのオーバーヘッドを回避できます。

技術的な詳細については、[oak-runのインデックス作成に関するドキュメント](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html)を参照してください。

### インデックスのインポート{#importing-indexes}

AEM 6.4以降のバージョンでは、AEMには、起動シーケンスでディスクからインデックスをインポートする機能が組み込まれています。 フォルダー`<repository>/indexing-result/indexes`は、起動中にインデックスデータが存在するのを監視します。 **target** AEM jarの新しいバージョンを開始する前に、[アップグレードプロセス](in-place-upgrade.md#performing-the-upgrade)で、事前に作成したインデックスを上記の場所にコピーできます。 AEMはリポジトリに読み込み、対応するチェックポイントをシステムから削除します。 したがって、再インデックスは完全に回避される。

## その他のヒントとトラブルシューティング {#troubleshooting}

以下に、役立つヒントとトラブルシューティングの手順を示します。

### 実稼動システムへの影響の軽減{#reduce-the-impact-on-the-live-production-system}

本番システムのクローンを作成し、そのクローンを使用してオフラインインデックスを作成することをお勧めします。 これにより、本番システムに与える潜在的な影響を排除できます。 ただし、インデックスのインポートに必要なチェックポイントは、実稼動システムに存在する必要があります。 したがって、クローンを作成する前にチェックポイントを作成することが重要です。

### Runbookと試用版の実行の準備{#prepare-a-runbook-and-trial-run}

[Runbook](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/upgrading/upgrade-planning.html#building-the-upgrade-and-rollback-runbook)を準備し、本番環境でアップグレードを実行する前に、いくつかの試用を実行することをお勧めします。

### オフラインインデックス付きドキュメントトラバーサルモード{#doc-traversal-mode-with-offline-indexing}

オフラインインデックス作成には、リポジトリ全体の複数のトラバーサルが必要です。 MongoMKインストールでは、インデックス作成プロセスのパフォーマンスに影響を与えるネットワークを介してリポジトリにアクセスします。 1つの選択肢は、MongoDBレプリカ自体でオフラインのインデックス作成プロセスを実行することで、ネットワークのオーバーヘッドをなくすことです。 もう1つのオプションは、ドキュメントトラバーサルモードの使用です。

Doc traversalモードは、オフラインインデックス作成用のoak-runコマンドにコマンドラインパラメーター`—doc-traversal`を追加することで適用できます。 このモードは、ローカルディスク内のリポジトリ全体のコピーをフラットファイルとしてスプールし、それを使用してインデックス作成を実行します。
