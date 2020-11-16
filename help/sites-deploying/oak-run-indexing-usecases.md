---
title: oak-run.jar でのインデックス作成の使用例
seo-title: oak-run.jar でのインデックス作成の使用例
description: Oak-run ツールを使用してインデックスを作成する様々な使用例について説明します。
seo-description: Oak-run ツールを使用してインデックスを作成する様々な使用例について説明します。
uuid: 3c50080d-1e0d-4886-8d37-269f06881eb4
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 084075b8-826d-4f27-9342-35f33368f24f
noindex: true
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1392'
ht-degree: 88%

---


# oak-run.jar でのインデックス作成の使用例{#oak-run-jar-indexing-use-cases}

Oak-run は、コマンドラインで以下のようなインデックスに関する使用例をサポートします。AEM の JMX コンソールを使用する必要はありません。

Oakインデックスを管理するためのoak-run.jarインデックスコマンドを使用すると、次のようなメリットが得られます。

1. Oak-run indexコマンドは、AEM 6.4用の新しいインデックス作成ツールセットを提供します。
1. Oak-run を使用すると、インデックス再作成の時間を短縮でき、大規模なリポジトリでのインデックス再作成時間を削減できます。
1. Oak-run を使用すると、インデックス再作成中の AEM でのリソース消費を低減できるので、システム全体のパフォーマンスが向上します。
1. Oak-run は out-of-band のインデックス再作成機能を備えています。実稼動環境を利用したままインデックスを再作成する必要があり、インデックス再作成中のメンテナンスやダウンタイムが許容されない場合に使用できます。

以下の節では、コマンドの例を示します。oak-run インデックスコマンドは、すべての NodeStore および BlobStore 設定をサポートしています。以下では、FileDataStore および SegmentNodeStore を使用した設定の例を紹介します。

## 使用例 1 - インデックスの整合性チェック {#usercase1indexconsistencycheck}

これは、インデックスの破損に関連する使用例です。以前は、破損しているインデックスを特定できない場合もありました。このため、次の特長を持つツールが用意されています。

1. すべてのインデックスでインデックスの整合性チェックを実行し、有効なインデックスと無効なインデックスに関するレポートを提供します。
1. このツールは、AEM にアクセスできない場合でも使用可能です。
1. このツールは簡単に使用できます。

Checking for corrupt indexes can be performed via `--index-consistency-check` operation:

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-consistency-check
```

This will generate a report in `indexing-result/index-consistency-check-report.txt`. サンプルレポートについては、以下を参照してください。

```
Valid indexes :
        - /content/oak:index/enablementResourceName
        - /oak:index/cqProjectLucene
        - /oak:index/cqTagLucene
        - /oak:index/lucene
        - /oak:index/ntBaseLucene
        - /oak:index/socialLucene
    Invalid indexes :
        - /oak:index/atDamIndex
        - /oak:index/atIndex
        - /oak:index/cqPageLucene
        - /oak:index/damAssetLucene
        - /oak:index/groups
        - /oak:index/slingeventJob
        - /oak:index/users
        - /oak:index/workflowDataLucene
    Ignored indexes as these are not of type lucene:
        - /oak:index/acPrincipalName
        - /oak:index/active
```

### メリット {#uc1benefits}

このツールを使用することにより、サポートおよびシステム管理者は、破損しているインデックスをすばやく特定し、これらのインデックスを再作成できるようになりました。

## 使用例 2 - インデックス統計 {#usecase2indexstatistics}

以前は、クエリパフォーマンスに関して診断する場合、お客様のセットアップの既存のインデックス定義やインデックス関連統計が必要になることがありました。これらの情報は、これまで複数のリソースに散在していました。より簡単にトラブルシューティングできるように、次の特長を持つツールが用意されています。

1. システムに存在するすべてのインデックス定義を 1 つの JSON ファイルにダンプします。

1. 既存のインデックスの重要な統計をダンプします。

1. オフライン分析のためにインデックスコンテンツをダンプします。

1. AEM にアクセスできない場合でも使用可能です。

前述の操作は、次の操作用の index コマンドを使用して実行できるようになりました。

* `--index-info`  — インデックスに関連する各種統計を収集してダンプ

* `--index-definitions`  — インデックス定義を収集し、ダンプする

* `--index-dump`  — インデックス内容をダンプします

コマンドが実際にどのように機能するかについての例は、次を参照してください。

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-info --index-definitions --index-dump
```

The reports would be generated in `indexing-result/index-info.txt` and `indexing-result/index-definitions.json`

また、同じ詳細が Web コンソール経由でも提供され、設定のダンプ zip にも含まれます。この詳細には、次の場所からアクセスできます。

`https://serverhost:serverport/system/console/status-oak-index-defn`

### メリット {#uc2benefits}

このツールを使用すると、インデックス作成またはクエリの問題に関連するすべての必要な詳細をすばやく収集できるので、この情報の抽出にかかる時間を短縮できます。

## 使用例 3 - インデックス再作成 {#usecase3reindexing}

[シナリオ](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing)によっては、インデックス再作成の実行が必要な場合があります。Currently the reindexing is done by setting the `reindex` flag to `true` in the index definition node via CRXDE or via the Index Manager user interface. このフラグが設定されると、インデックス再作成が非同期的におこなわれます。

次に、インデックス再作成に関するいくつかの注意点を示します。

* インデックス再作成を `DocumentNodeStore` 設定でおこなう場合は、すべてのコンテンツがローカルである `SegmentNodeStore` 設定でおこなう場合より、時間がかなり長くかかります。

* 現在の設計では、インデックス再作成中に非同期インデクサーがブロックされます。他のすべての非同期インデックスが古くなり、インデックス作成中に更新が取得されません。このため、システムが使用中の場合は、最新の結果が表示されないことがあります。
* インデックス再作成には、リポジトリ全体のトラバーサルが伴います。これは、AEM 設定に大きな負荷がかかる可能性があり、エンドユーザーエクスペリエンスに影響する可能性があります。
* `DocumentNodeStore` インストールでは、インデックス再作成にかなりの時間がかかる可能性があります。操作中に Mongo データベースへの接続に失敗すると、インデックス作成を最初からやり直す必要があります。

* テキストを抽出するので、インデックス再作成に時間がかかる場合があります。これは、主に PDF ファイルが多く含まれる設定に当てはまります。テキスト抽出にかかる時間は、インデックス作成時間に影響する可能性があります。

これらの目的を満たすために、oak-run インデックスツールでは、必要に応じて使用できるインデックス再作成の様々なモードをサポートしています。oak-run インデックスコマンドには、次のメリットがあります。

* **out-of-band のインデックス再作成** - oak-run のインデックス再作成は、実行中の AEM 設定とは別に実行できるので、使用中の AEM インスタンスへの影響が最小限に抑えられます。

* **out-of-lane のインデックス再作成** - このインデックス再作成は、インデックス作成操作に影響を与えずにおこなわれます。つまり、非同期インデクサーは他のインデックス作成を続行できます。

* **インストールでの簡略化されたインデックス再作成** - `DocumentNodeStore`DocumentNodeStore インストールでは、インデックス再作成が単一のコマンドで実行できます。これにより、インデックス再作成が確実に最適な方法で実行されます。

* **インデックス定義の更新および新しいインデックス定義の導入のサポート**

### インデックス再作成 - DocumentNodeStore {#reindexdocumentnodestore}

`DocumentNodeStore` インストールでは、単一の oak-run コマンドを使用してインデックス再作成をおこなうことができます。

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore mongodb://server:port/aem
```

これには次のメリットがあります。

* 実行中の AEM インスタンスへの影響が少ない。ほとんどの読み取りはセカンダリサーバーから実行できます。実行中の AEM のキャッシュは、インデックス再作成に必要とされるトラバーサルをすべて考慮しても、悪影響は受けません。
* Users can also provide a JSON of a new or updated index via the `--index-definitions-file` option.

### インデックス再作成 - SegmentNodeStore {#reindexsegmentnodestore}

`SegmentNodeStore` インストールでは、次のいずれかの方法でインデックス再作成をおこなうことができます。

#### オンラインのインデックス再作成 - SegmentNodeStore {#onlinereindexsegmentnodestore}

既定の方法に従い、`reindex` フラグを設定してインデックス再作成をおこないます。

#### オンラインのインデックス再作成 - SegmentNodeStore - AEM インスタンス実行中 {#onlinereindexsegmentnodestoretheaeminstanceisrunning}

`SegmentNodeStore` インストールでは、セグメントファイルに読み取り／書き込みモードでアクセスできるのは 1 つのプロセスのみです。このため、oak-run のインデックス作成の一部の操作では、手動による追加の手順が必要です。

これには、次のものが含まれます。

1. ステップテキスト
1. AEM で使用される同じリポジトリに `oak-run` を読み取り専用モードで接続し、インデックスを作成します。これを実行する方法の例：

   ```shell
   java -jar oak-run-1.7.6.jar index --fds-path=/Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/datastore/ --checkpoint 26b7da38-a699-45b2-82fb-73aa2f9af0e2 --reindex --index-paths=/oak:index/lucene /Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/segmentstore/
   ```

1. 最後に、前述のコマンドを実行した後で、`IndexerMBean#importIndex` 操作を使用して、oak-run がインデックスファイルを保存したパスから、作成したインデックスファイルを読み込みます。

このシナリオでは、AEM サーバーを停止したり、新しいインスタンスをプロビジョニングしたりする必要はありません。ただし、インデックス作成にはリポジトリ全体のトラバーサルが伴うので、インストールへの I/O 負荷が増加し、実行時のパフォーマンスに悪影響があります。

#### オンラインのインデックス再作成 - SegmentNodeStore - AEM インスタンスのシャットダウン {#onlinereindexsegmentnodestoreaeminstanceisdown}

`SegmentNodeStore` インストールでは、単一の oak-run コマンドを使用してインデックス再作成をおこなうことができます。ただし、AEM インスタンスをシャットダウンする必要があります。

次のコマンドを使用して、インデックス再作成を開始できます。

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore  /path/to/segmentstore/
```

この方法と前述の方法の違いは、チェックポイントの作成とインデックスの読み込みが自動的におこなわれることです。欠点は、処理中に AEM を終了する必要があることです。

#### Out of Band のインデックス再作成 - SegmentNodeStore {#outofbandreindexsegmentnodestore}

この使用例では、クローン作成された設定でインデックスを再作成して、実行中の AEM インスタンスへの影響を最小限に抑えることができます。

1. JMX 操作でチェックポイントを作成します。これをおこなうには、[JMX コンソール](/help/sites-administering/jmx-console.md)に移動して、`CheckpointManager` を検索します。Then, click on the **createCheckpoint(long p1)** operation using a high value for expiration in seconds (for example, **2592000**).
1. Copy the `crx-quickstart` folder to a new machine
1. oak-run の index コマンドを使用してインデックスを再作成します。

1. 生成されたインデックスファイルを AEM サーバーにコピーします。

1. JMX を使用してインデックスファイルを読み込みます。

この使用例では、別のインスタンスのデータストアにアクセスできることを前提としています。`FileDataStore` が EBS などのクラウドベースのストレージソリューションに配置されている場合は、このデータストアにアクセスできないことがあります。This excludes the scenario where `FileDataStore` is also cloned. インデックス定義でフルテキストのインデックス作成が実行されない場合は、`DataStore` へのアクセスは必要ありません。

## 使用例 4 - インデックス定義の更新 {#usecase4updatingindexdefinitions}

現在、インデックス定義の変更は、[ACS Ensure Index](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) パッケージ経由で送信できます。これにより、コンテンツパッケージ経由でインデックス定義の送信が可能になります。コンテンツパッケージは後で、`reindex` フラグを `true` に設定してインデックスを再作成する必要があります。

これは、インデックス再作成に時間がかからない小規模なインストールに適しています。ただし、非常に大きいリポジトリでは、インデックス再作成にかなりの時間がかかります。このような場合は、oak-run インデックスツールを使用できます。

oak-run では、インデックス定義を JSON 形式で提供したり、out-of-band モードでインデックスを作成したりすることができます。out-of-band モードの場合、ライブインスタンスでは変更がおこなわれません。

この使用例を検討する必要があるプロセスは次のとおりです。

1. A developer would update the index definitions on a local instance and then generate an index definition JSON file via the `--index-definitions` option

1. 更新された JSON がシステム管理者に提供されます。
1. システム管理者は out-of-band 方式に従って、別のインストールでインデックスを準備します。
1. これが完了すると、生成されたインデックスファイルが、実行中の AEM インストールに読み込まれます。

