---
title: MongoDB を備えた AEM
seo-title: MongoDB を備えた AEM
description: MongoDB を備えた AEM を正常にデプロイするために必要なタスクと考慮事項について学習します。
seo-description: MongoDB を備えた AEM を正常にデプロイするために必要なタスクと考慮事項について学習します。
uuid: 8028832d-10de-4811-a769-fab699c162ec
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: cd3b979f-53d4-4274-b4eb-a9533329192a
docset: aem65
translation-type: tm+mt
source-git-commit: 56006a1f49e4d357cd7ee44a4a1dd1af7189e70a
workflow-type: tm+mt
source-wordcount: '6513'
ht-degree: 91%

---


# MongoDB を備えた AEM{#aem-with-mongodb}

この記事は、MongoDB を備えた Adobe Experience Manager を正常にデプロイするために必要なタスクと考慮事項に関する知識を深めることを目的としています。

デプロイメントについて詳しくは、このドキュメントの[デプロイとメンテナンス](/help/sites-deploying/deploy.md)の節を参照してください。

## AEM で MongoDB を使用する状況 {#when-to-use-mongodb-with-aem}

MongoDB は通常、次のいずれかの条件を満たす AEM オーサーのデプロイメントをサポートする場合に使用します。

* 1 日あたり 1,000 人を超える個別ユーザー
* 100 人を超える同時ユーザー
* 大量のページ編集
* 大規模なロールアウトまたはアクティベーション

上述の条件が適用されるのはオーサーインスタンスのみです。すべて TarMK ベースであることが必要なパブリッシュインスタンスには適用されません。オーサーインスタンスでは、未認証のアクセスは許可されないので、ユーザー数は認証済みのユーザーを表します。

条件が満たされない場合は、可用性に対応するために、TarMK アクティブ／スタンバイデプロイメントをお勧めします。通常、MongoDB は、1 台のハードウェアで実現できる性能よりも高い拡張要件が求められる場合に検討してください。

>[!NOTE]
>
>オーサーインスタンスのサイジングと同時ユーザーの定義について詳しくは、[ハードウェアのサイジングのガイドライン](/help/managing/hardware-sizing-guidelines.md#authors-working-in-parallel)を参照してください。

### AEM における MongoDB の最小デプロイメント {#minimal-mongodb-deployment-for-aem}

MongoDB での AEM の最小デプロイメントは次のとおりです。簡潔にするために、SSL ターミネーションおよび HTTP プロキシコンポーネントは一般化されています。1つのMongoDBレプリカ・セットで構成され、1つのプライマリ・レプリカと2つのセカンダリ・レプリカがあります。

![chlimage_1-4](assets/chlimage_1-4.png)

最小デプロイメントには、レプリカセットとして設定された 3 つの `mongod` インスタンスが必要です。1 つのインスタンスはプライマリとして選択され、その他のインスタンスはセカンダリとして選択されます。この選択は、`mongod` によって管理されます。各インスタンスにローカルディスクが接続されています。クラスタが負荷をサポートするためには、最小12 MB/秒まで、1秒あたり3,000個を超えるI/O操作(IOPS)を持つことを推奨します。

AEM オーサーは `mongod` インスタンスに接続されます。各 AEM オーサーは 3 つの `mongod` インスタンスすべてに接続します。書き込みはプライマリに送信され、読み取りはいずれのインスタンスからもおこなうことができます。トラフィックは、Dispatcher によって、負荷に基づいてアクティブな AEM オーサーインスタンスのいずれかに分散されます。OAK データストアは `FileDataStore` であり、MongoDB の監視は、デプロイメントの場所に応じて、MMS または MongoDB Ops Manager によって提供されます。オペレーティングシステムレベルの監視とログの監視は、Splunk や Ganglia のようなサードパーティソリューションによって提供されます。

このデプロイメントでは、実装が正常に機能するには、すべてのコンポーネントが必要です。いずれかのコンポーネントが不足していると、実装は機能しません。

### オペレーティングシステム {#operating-systems}

AEM 6 でサポートされているオペレーティングシステムのリストについては、[技術要件のページ](/help/sites-deploying/technical-requirements.md)を参照してください。

### 環境 {#environments}

仮想化環境をサポートするには、プロジェクトを実行する様々な技術チームが適切にコミュニケーションを取る必要があります。これには、AEM を実行するチーム、オペレーティングシステムを所有するチームおよび仮想化インフラストラクチャを管理するチームが含まれます。

MongoDB インスタンスの I/O 処理能力については特殊な要件があり、この要件の管理は仮想化環境を管理するチームがおこなう必要があります。Amazon Web Services などのクラウドデプロイメントをプロジェクトで使用する場合、MongoDB インスタンスをサポートするための十分な I/O 処理能力と整合性が得られるようにインスタンスをプロビジョニングする必要があります。そうしないと、MongoDB プロセスと Oak リポジトリの動作が、信頼性が低く不安定なものになります。

仮想化環境では、VMWare のリソース割り当てポリシーによって MongoDB のストレージエンジンの機能が損なわれることがないように、MongoDB で特殊な I/O および VM の設定が必要になります。適切な実装では、個々のチーム間の障壁がなくなり、必要なパフォーマンスを実現するためにすべてのチームが連携して作業します。

## ハードウェアに関する考慮事項 {#hardware-considerations}

### ストレージ {#storage}

水平方向のスケーリングを早い段階でおこなうことなく、読み書きのスループットが最適なパフォーマンスになるようにするには、通常、SSD ストレージまたは SSD 相当のパフォーマンスを提供するストレージが MongoDB で必要となります。

### RAM {#ram}

MMAP ストレージエンジンを使用する MongoDB バージョン 2.6 および 3.0 では、データベースとそのインデックスの作業セットが RAM に収まる必要があります。

十分な RAM がないとパフォーマンスが大幅に低下します。作業セットとデータベースのサイズは、アプリケーションに大きく依存します。ある程度の概算をおこなうことはできますが、必要な RAM の容量を特定するための最も信頼できる方法は、AEM アプリケーションを構築して負荷テストを実施することです。

負荷テストを実施する場合は、データベースの合計サイズに対する作業セットの比率を次のように想定することができます。

* SSD ストレージの場合は 1:10
* ハードディスクストレージの場合は 1:3

つまり、SSD デプロイメントの場合、2 TB のデータベースには 200 GB の RAM が必要です。

MongoDB 3.0 の WiredTiger ストレージエンジンにも同じ制限が適用されますが、WiredTiger では MMAP ストレージエンジンと同様の方法でメモリマッピングを使用しないので、作業セット、RAM およびページフォールトの間の相関関係はそれほど強くありません。

>[!NOTE]
>
>MongoDB 3.0 を使用する AEM 6.1 のデプロイメントには、WiredTiger ストレージエンジンを使用することをお勧めします。

### データストア {#data-store}

MongoDB の作業セットに関する制限により、データストアを MongoDB から独立して保持することを強くお勧めします。ほとんどの環境では、すべての AEM インスタンスに対して使用可能な NAS を使用する `FileDataStore` を使用してください。For situations where the Amazon Web Services are used, there is also an `S3 DataStore`. 何らかの理由でデータストアを MongoDB 内に保持する場合は、データストアのサイズをデータベースの合計サイズに加算し、作業セットの計算を適切に調整する必要があります。これは、ページフォールトを発生させずにパフォーマンスを維持するには、はるかに多くの RAM をプロビジョニングすることを意味する場合があります。

## 監視 {#monitoring}

プロジェクトを正常に実装するには監視が不可欠です。十分な知識があれば、監視なしでも MongoDB 上で AEM を実行することは可能ですが、その知識を持っているのは通常、デプロイメントの各セクションを専門とするエンジニアです。

これは一般に、Apache Oak コアに取り組む R&amp;D エンジニアや MongoDB スペシャリストなどです。

すべてのレベルにおいて監視がない場合、問題を診断するためにコードベースの詳細な知識が必要になります。監視が実施されて、主要な統計に関する適切なガイダンスが提供されれば、実装チームは異常に対して的確に対応できます。

コマンドラインツールを使用してクラスターの動作のクイックスナップショットを取得することもできますが、多数のホストに対してリアルタイムでこれをおこなうのはほぼ不可能です。コマンドラインツールで数分間を超える履歴情報が提供されることはほとんどなく、様々なタイプの指標を相関させることもできません。`mongod` のバックグラウンド同期が短期間遅くなると、見かけ上は接続されていない仮想マシンからの共有ストレージリソースに対する I/O の待機や過剰な書き込みレベルの相関関係を見つけるために手動による多大な労力が必要になります。

### MongoDB Cloud Manager {#mongodb-cloud-manager}

MongoDB Cloud Manager は、MongoDB インスタンスを監視および管理できる、MongoDB で提供される無料のサービスです。これにより、MongoDB クラスターのパフォーマンスとヘルスをリアルタイムで把握できます。また、インスタンスが Cloud Manager 監視サーバーにアクセスできる場合は、クラウドでホストされているインスタンスとプライベートにホストされているインスタンスの両方を管理できます。

監視サーバーに接続するMongoDBインスタンスにインストールされたエージェントが必要です。 エージェントには次の 3 つのレベルがあります。

* MongoDB サーバー上のすべてのものを完全に自動化できる自動化エージェント
* `mongod` インスタンスを監視できる監視エージェント
* スケジュールされたデータバックアップを実行できるバックアップエージェント

Cloud Manager を使用して MongoDB クラスターのメンテナンスを自動化すると、定期的なタスクの多くが容易になりますが、これは必須ではありません。また、バックアップに Cloud Manager を使用することも必須ではありません。ただし、監視をおこなうために Cloud Manager を選択した場合、監視は必須です。

MongoDB Cloud Manager について詳しくは、[MongoDB のドキュメント](https://docs.cloud.mongodb.com/)を参照してください。

### MongoDB Ops Manager {#mongodb-ops-manager}

MongoDB Ops Manager は、MongoDB Cloud Manager と同じソフトウェアです。登録すると、Ops Manager をダウンロードして、プライベートデータセンターまたは他のラップトップマシンやデスクトップマシンにローカルにインストールできます。このソフトウェアは、ローカルの MongoDB データベースを使用してデータを格納し、Cloud Manager とまったく同様に管理対象サーバーと通信します。セキュリティポリシーで監視エージェントを禁止している場合は、MongoDB Ops Manager を使用してください。

### オペレーティングシステムの監視 {#operating-system-monitoring}

AEM MongoDB クラスターを実行するには、オペレーティングシステムレベルの監視が必要です。

そのようなシステムの良い例として Ganglia があります。Ganglia では、対象範囲の概要情報が提供され、CPU、負荷平均、空きディスク領域のようなヘルスに関する基本的な指標にとどまらず、必要な情報の詳細を表示できます。問題を診断するには、エントロピープールレベル、CPU I/O 待機、FIN_WAIT2 状態のソケットなど、下位レベルの情報が必要です。

### ログの集約 {#log-aggregation}

複数のサーバーで構成されるクラスターの場合、実稼動システムにはログの一元的な集約が必要となります。Splunk のようなソフトウェアではログの集約がサポートされており、チームは、ログを手動で収集しなくても、アプリケーションの動作のパターンを分析できます。

## チェックリスト {#checklists}

ここでは、プロジェクトを実装する前に、AEM と MongoDB のデプロイメントを適切に設定するために実行する必要がある様々な手順について説明します。

### ネットワーク {#network}

1. まず、すべてのホストに DNS エントリがあることを確認します。
1. ルーティング可能な他のすべてのホストから、すべてのホストがそれぞれの DNS エントリによって解決できる必要があります。
1. MongoDB ホストはすべて、同じクラスター内の他のすべての MongoDB ホストからルーティング可能です。
1. MongoDB ホストは、MongoDB Cloud Manager およびその他の監視サーバーにパケットをルーティングできます。
1. AEM サーバーは、すべての MongoDB サーバーにパケットをルーティングできます。
1. AEM サーバーと MongoDB サーバーの間のパケットの遅延は 2 ミリ秒未満であり、パケットの損失がなく、標準的な配信は 1 ミリ秒以下です。
1. AEM サーバーと MongoDB サーバーの間のホップは 2 つまでです。
1. 2 つの MongoDB サーバー間のホップは 2 つまでです。
1. 任意のコアサーバー（MongoDB、AEM または任意の組み合わせ）間のルーターは OSI レベル 3 以下です。
1. VLAN トランキングまたは何らかの形のネットワークトンネリングを使用している場合、パケット遅延チェックに適合している必要があります。

### AEM の設定 {#aem-configuration}

#### ノードストアの設定 {#node-store-configuration}

MongoMK を選択して AEM を使用するように AEM インスタンスを設定する必要があります。AEM における MongoMK 実装の基盤はドキュメントノードストアです。

ノードストアを設定する方法について詳しくは、[AEM でのノードストアとデータストアの設定](/help/sites-deploying/data-store-config.md)を参照してください。

次に、MongoDB の最小デプロイメントにおけるドキュメントノードストアの設定の例を示します。

```xml
# org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config
#MongoDB server details
mongodburi=mongodb://aem:aempassword@mongodbserver1.customer.com:27000,mongodbserver2.customer.com:27000

#Name of MongoDB database to use
db=aem

#Store binaries in custom BlobStore e.g. FileDataStore
customBlobStore=true

cache=2048
blobCacheSize=1024
```

ここで、

* `mongodburi` これは、AEM が接続する必要がある MongoDB サーバーです。接続は、デフォルトレプリカセットの既知のメンバーすべてに対して確立されます。MongoDB Cloud Manager を使用する場合は、サーバーセキュリティが有効になります。そのため、適切なユーザー名とパスワードが接続文字列に含まれている必要があります。エンタープライズ以外のバージョンの MongoDB では、ユーザー名およびパスワード認証のみがサポートされます。接続文字列の構文について詳しくは、こちらの[ドキュメント](https://docs.mongodb.org/manual/reference/connection-string/)を参照してください。

* `db`データベースの名前。AEMのデフォルトは 
`aem-author`.

* `customBlobStore` デプロイメントでバイナリがデータベースに格納される場合、バイナリは作業セットの一部になります。そのため、バイナリをMongoDBに格納しないよう推奨され、 
`FileSystem` データストアをNASに置く。

* `cache`
キャッシュサイズ（メガバイト）。 これは、 
`DocumentNodeStore`」を選択します。デフォルト値は 256 MB です。ただし、キャッシュが大きいほうが Oak の読み取りパフォーマンスは向上します。

* `blobCacheSize` 頻繁に使用される Blob は、データストアから再取得しなくて済むように、AEM にキャッシュできます。これは、Blob を MongoDB データベースに格納する場合は特に、パフォーマンスへの影響が大きくなります。オペレーティングシステムレベルのディスクキャッシュは、ファイルシステムベースのすべてのデータストアに効果的です。

#### データストアの設定 {#data-store-configuration}

データストアは、しきい値よりも大きいサイズのファイルを格納するために使用されます。そのしきい値以下のファイルは、ドキュメントノードストア内にプロパティとして格納されます。`MongoBlobStore` を使用する場合、Blob を格納するための専用のコレクションが MongoDB に作成されます。このコレクションは `mongod` インスタンスの作業セットに含まれ、パフォーマンスの問題を回避するには、より大きな RAM が `mongod` に必要になります。そのため、実稼動デプロイメントでは `MongoBlobStore` を使用せず、すべての AEM インスタンス間で共有される、NAS によって提供される `FileDataStore` を使用する設定をお勧めします。ファイルの管理にはオペレーティングシステムレベルのキャッシュが効率的なので、ディスク上のファイルの最小サイズをディスクのブロックサイズに近い値に設定して、ファイルシステムが効率的に使用され、`mongod` インスタンスの作業セットに多数の小さいドキュメントが過剰に含まれないようにします。

次に、MongoDB を使用した AEM の最小デプロイメントにおける一般的なデータストアの設定を示します。

```xml
# org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config
# The minimum size of an object that should be stored in this data store.
minRecordLength=4096
path=/datastore
maxCachedBinarySize=4096
cacheSizeInMB=128
```

ここで、

* `minRecordLength`
サイズ（バイト単位） このサイズ以下のバイナリは、ドキュメントノードストアに格納されます。Blob の ID を格納するのではなく、バイナリの内容が格納されます。このサイズより大きいバイナリの場合、バイナリのIDはnodesコレクションのドキュメントのプロパティとして格納され、バイナリの本体は 
`FileDataStore` ディスク上 一般的なファイルシステムのブロックサイズは 4,096 バイトです。

* `path` データストアのルートのパスです。MongoMK デプロイメントの場合、これはすべての AEM インスタンスで使用可能な共有ファイルシステムである必要があります。通常は、ネットワーク接続ストレージ（NAS）サーバーを使用します。AmazonWebサービスなどのクラウドデプロイメントの場合、 
`S3DataFileStore` も使用できます。

* `cacheSizeInMB` バイナリキャッシュの合計サイズ（メガバイト単位）です。これは、 
`maxCacheBinarySize` の設定に従います。

* `maxCachedBinarySize` バイナリキャッシュにキャッシュされるバイナリの最大サイズ（バイト単位）です。ファイルシステムベースのデータストアを使用する場合、バイナリはオペレーティングシステムによって既にキャッシュされているので、データストアのキャッシュに大きい値を使用することはお勧めしません。

#### クエリヒントの無効化 {#disabling-the-query-hint}

すべてのクエリと共に送信されるクエリヒントを無効にするには、プロパティ

`-Doak.mongo.disableIndexHint=true`

そのためには、AEM の起動時に上述のプロパティを追加します。これにより、MongoDB では、内部統計に基づいて最も適切なインデックスで計算がおこなわれます。

クエリヒントが無効でない場合は、インデックスのパフォーマンスをチューニングしても AEM のパフォーマンスには影響しません。

#### MongoMK の永続キャッシュの有効化 {#enable-persistent-cache-for-mongomk}

I/O の読み取りパフォーマンスを高くして環境での処理速度を最大化するには、MongoDB デプロイメントで永続キャッシュ設定を有効にすることをお勧めします。詳しくは、[Jackrabbit Oak のドキュメント](https://jackrabbit.apache.org/oak/docs/nodestore/persistent-cache.html)を参照してください。

## MongoDB オペレーティングシステムの最適化 {#mongodb-operating-system-optimizations}

### オペレーティングシステムのサポート {#operating-system-support}

MongoDB 2.6 では、メモリマップストレージエンジンを使用します。このストレージエンジンは、RAM とディスクに関するオペレーティングシステムレベルの管理でのいくつかの特性の影響を受けます。MongoDB インスタンスのクエリと読み取りのパフォーマンスを向上させるには、ページフォールトと呼ばれることもある、低速な I/O 操作を回避または排除する必要があります。これらは、特に `mongod` プロセスに適用されるページフォールトです。オペレーティングシステムレベルのページフォールトと混同しないでください。

高速な操作のためには、既に RAM に存在しているデータにのみ MongoDB データベースがアクセスする必要があります。アクセスする必要があるデータは、インデックスとデータで構成されています。インデックスとデータのこのコレクションは、作業セットと呼ばれます。使用可能な RAM よりも作業セットが大きい場合、MongoDB はディスクからそのデータをページインする必要があり（これにより、I/O コストが発生します）、既にメモリ内にある他のデータが消去されます。この消去が原因となってデータがディスクから再度読み込まれると、ページフォールトが増えてパフォーマンスが低下します。作業セットが動的で変動する場合は、操作をサポートするために、さらに多くのページフォールトが発生します。

MongoDB は、Linux の幅広いフレーバー、Windows、Mac OS を含む、数多くのオペレーティングシステムで動作します。詳しくは、[https://docs.mongodb.com/manual/installation/#supported-platforms](https://docs.mongodb.com/manual/installation/#supported-platforms) を参照してください。MongoDB には、選択したオペレーティングシステムによって、異なるオペレーティングシステムレベルの推奨事項があります。これらは [https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration](https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration) に掲載されていますが、ここでも簡単にまとめておきます。

#### Linux {#linux}

* Transparent Huge Page（THP）および defrag を無効にします。詳しくは、[Transparent Huge Page（THP）の設定についての説明](https://docs.mongodb.com/manual/tutorial/transparent-huge-pages/)を参照してください。
* 使用状況に応じてデータベースファイルを格納するデバイスの [readahead の設定を調整](https://docs.mongodb.com/manual/administration/production-notes/#readahead)します。

   * MMAPv1 ストレージエンジンでは、作業セットが利用可能な RAM よりも大きく、ドキュメントのアクセスパターンがランダムな場合、readahead を 32 または 16 に下げることを検討します。様々な設定を試し、使用するメモリの量を最大化でき、ページフォールトの回数を低減できる最適な値を見つけます。
   * WiredTiger ストレージエンジンでは、ストレージメディアタイプ（回転式のディスク、SSD など）にかかわらず、readahead を 0 に設定します。一般的に、readahead の値を高くすることで、測定可能、再現可能、かつ信頼性のあるメリットがあることをテストで確認できた場合を除き、この推奨 readahead 設定を使用します。[MongoDB のプロフェッショナルサポート](https://docs.mongodb.com/manual/administration/production-notes/#readahead)で、0 以外の readahead 設定を使用する場合のアドバイスとガイダンスを受けることができます。

* 仮想環境で RHEL 7／CentOS 7 を実行している場合は、Tuned ツールを無効にします。
* 仮想環境で RHEL 7／CentOS 7 を実行すると、Tuned ツールによって、パフォーマンスのスループットから得られたパフォーマンスプロファイルが自動的に呼び出され、これにより readahead 設定が自動的に 4 MB に設定されます。この設定は、パフォーマンスに悪影響を与えます。
* SSD ドライブでは、noop または deadline ディスクスケジューラーを使用します。
* ゲスト VM での仮想化ドライブでは、noop ディスクスケジューラーを使用します。
* NUMA を無効にするか、vm.zone_reclaim_mode を 0 に設定し、ノードインタリーブを指定して [mongod](https://docs.mongodb.com/manual/administration/production-notes/#readahead) インスタンスを実行します。詳しくは、[MongoDB and NUMA Hardware（MongoDB と NUMA ハードウェア）](https://docs.mongodb.com/manual/administration/production-notes/#readahead)を参照してください。

* 使用状況に応じてハードウェアの ulimit 値を調整します。同じユーザーで複数の [mongod](https://docs.mongodb.com/manual/reference/program/mongod/#bin.mongod) または [mongos](https://docs.mongodb.com/manual/reference/program/mongos/#bin.mongos) インスタンスを実行する場合、適宜 ulimit 値を拡張します。詳しくは、[UNIX ulimit Settings（UNIX の ulimit の設定）](https://docs.mongodb.com/manual/reference/ulimit/)を参照してください。

* [dbPath](https://docs.mongodb.com/manual/reference/configuration-options/#storage.dbPath) マウントポイントに noatime を使用します。
* デプロイメントにとって十分なファイルハンドル数（fs.file-max）、カーネルの pid の制限（kernel.pid_max）およびプロセスごとの最大スレッド数（kernel.threads-max）の設定にします。大規模なシステムでは、まず以下の設定から試すことをお勧めします。

   * fs.file-max の値：98000
   * kernel.pid_max の値：64000
   * andkernel.threads-max の値：64000

* システムに、スワップ領域が設定されていることを確認します。適切なサイジングについて詳しくは、オペレーティングシステムのドキュメントを参照してください。
* システムのデフォルトの TCP キープアライブが正しく設定されていることを確認します。レプリカセットおよびシャードクラスターでは、300 の値を設定すると、多くの場合パフォーマンスが良くなります。詳しくは、Frequently Asked Questions（よくある質問）の [Does TCP keepalive time affect MongoDB Deployments? （TCP キープアライブ時間は MongoDB のデプロイメントに影響がありますか）](https://docs.mongodb.com/manual/faq/diagnostics/#faq-keepalive)を参照してください。

#### Windows {#windows}

* NTFS の「最終アクセス時刻」の更新を無効にすることを検討します。これは、Unix 系システムで atime を無効にすることと似ています。

### WiredTiger {#wiredtiger}

MongoDB 3.2 以降、MongoDB のデフォルトのストレージエンジンは WiredTiger ストレージエンジンとなっています。このエンジンは、数多くの堅牢で拡張性のある機能を備えており、あらゆる一般的なデータベースワークロードに適したものとなっています。以下では、これらの機能について説明します。

#### ドキュメントレベルの同時実行性 {#document-level-concurrency}

WiredTiger では、書き込み操作に対して、ドキュメントレベルでの同時実行制御を使用しています。そのため、複数のクライアントが特定のコレクションの異なるドキュメントを同時に変更することができます。

ほとんどの読み取りおよび書き込み操作で、WiredTiger は楽観的同時実行制御を使用します。WiredTiger は、グローバル、データベースおよびコレクションのレベルで、インテントロックのみを使用します。ストレージエンジンが 2 つの操作の間で競合を検出すると、一方の操作で書き込みの競合が生じ、MongoDB は透過的にその操作を再試行します。一部のグローバルな操作（通常は複数のデータベースに関係する短時間の操作）では、引き続きグローバルな「インスタンス全体の」ロックが必要となります。

コレクションの削除などのその他の一部の操作では、引き続き排他的データベースロックが必要です。

#### スナップショットとチェックポイント {#snapshots-and-checkpoints}

WiredTiger はマルチバージョン同時実行制御（MVCC）を使用しています。WiredTiger は、操作の開始時にトランザクションに対してデータの特定の時点のスナップショットを提供します。スナップショットは、インメモリデータの整合性のあるビューです。

WiredTiger は、ディスクに書き込む際、すべてのデータファイルでの整合性が保たれるように、スナップショットのすべてのデータをディスクに書き込みます。この[永続化](https://docs.mongodb.com/manual/reference/glossary/#term-durable)されたデータは、データファイル内のチェックポイントとして機能します。チェックポイントでは、最後のチェックポイントに至るまでデータファイルの整合性が保たれることが保証されます。つまり、チェックポイントは復元ポイントとして機能します。

MongoDB では、60 秒間隔または 2 GB のジャーナルデータごとにチェックポイントを作成（スナップショットデータをディスクに書き込み）するよう WiredTiger が設定されます。

新しいチェックポイントの書き込み中は、以前のチェックポイントが引き続き有効となります。そのため、新しいチェックポイントの書き込み中に MongoDB が終了したり、エラーが発生した場合でも、再起動時には最後の有効なチェックポイントから MongoDB の復元が可能です。

WiredTiger のメタデータテーブルがアトミックに更新され、新しいチェックポイントを参照するようになると、新しいチェックポイントにアクセスできるようになるとともに、新しいチェックポイントが永続化されます。新しいチェックポイントにアクセス可能になると、WiredTiger は古いチェックポイントからページを解放します。

WiredTiger を使用すると、[ジャーナル処理](https://docs.mongodb.com/manual/reference/glossary/#term-durable)をおこなわなくても MongoDB は最後のチェックポイントから復元できます。ただし、最後のチェックポイントが作成された後の変更を復元するには、[ジャーナル処理](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal)を有効にして実行します。

#### ジャーナル {#journal}

WiredTiger では、トランザクションログの先行書き込みと[チェックポイント](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-checkpoints)を使用して、データの永続性を確保しています。

WiredTiger ジャーナルにより、チェックポイント間におこなわれたすべてのデータ変更が永続化されます。チェックポイント間に MongoDB が終了すると、最後のチェックポイント以降に変更されたすべてのデータがジャーナルを使用して再現されます。MongoDB がジャーナルデータをディスクに書き込む頻度について詳しくは、[Journaling Process（ジャーナル処理プロセス）](https://docs.mongodb.com/manual/core/journaling/#journal-process)を参照してください。

WiredTiger のジャーナルは、[snappy](https://docs.mongodb.com/manual/core/journaling/#journal-process) 圧縮ライブラリを使用して圧縮されます。別の圧縮アルゴリズムを指定する場合、または圧縮しない場合は、[storage.wiredTiger.engineConfig.journalCompressor](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.journalCompressor) 設定を使用します。

For more information see: [Journaling with WiredTiger](https://docs.mongodb.com/manual/core/journaling/#journaling-wiredtiger).

>[!NOTE]
>
>WiredTiger の最小ログレコードサイズは 128 バイトです。ログレコードが 128 バイト以下の場合、WiredTiger はそのレコードを圧縮しません。
>
>[storage.journal.enabled](https://docs.mongodb.com/manual/reference/configuration-options/#storage.journal.enabled) を false に設定すると、ジャーナル処理を無効にすることができ、ジャーナルを維持するためのオーバーヘッドを削減できます。
>
>[スタンドアロン](https://docs.mongodb.com/manual/reference/glossary/#term-standalone)インスタンスでは、ジャーナルを使用しないと、チェックポイント間で MongoDB が予期せず終了したときに一部のデータ変更が失われることになります。[レプリカセット](https://docs.mongodb.com/manual/reference/glossary/#term-replica-set)のメンバーでは、レプリケーションプロセスで十分な永続性が保証される可能性があります。

#### 圧縮 {#compression}

WiredTiger を使用する場合、MongoDB では、すべてのコレクションおよびインデックスで圧縮がサポートされます。圧縮を使用することで、必要なストレージ容量を最小限に抑えることができますが、その分 CPU の負荷が高くなります。

デフォルトで、WiredTiger は、すべてのコレクションで [snappy](https://docs.mongodb.com/manual/reference/glossary/#term-snappy) 圧縮ライブラリを使用したブロック圧縮を、すべてのインデックスで[プレフィックス圧縮](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression)を使用します。

コレクションでは、[zlib](https://docs.mongodb.com/manual/reference/glossary/#term-zlib) によるブロック圧縮も利用できます。別の圧縮アルゴリズムを指定する場合、または圧縮しない場合は、[storage.wiredTiger.collectionConfig.blockCompressor](https://docs.mongodb.com/manual/reference/glossary/#term-zlib) 設定を使用します。

インデックスで[プレフィックス圧縮](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression)を無効にするには、[storage.wiredTiger.indexConfig.prefixCompression](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.indexConfig.prefixCompression) 設定を使用します。

圧縮設定は、コレクションおよびインデックスの作成時に、コレクションごと、およびインデックスごとに設定することもできます。[Specify Storage Engine Options（ストレージエンジンのオプションの指定）](https://docs.mongodb.com/manual/reference/method/db.createCollection/#create-collection-storage-engine-options)および [db.collection.createIndex() の storageEngine オプション](https://docs.mongodb.com/manual/reference/method/db.collection.createIndex/#createindex-options)を参照してください。

ほとんどのワークロードでは、デフォルトの圧縮設定を使用すると、ストレージ利用の効率性と、処理速度の要件のバランスをとることができます。

デフォルトで、WiredTiger のジャーナルも圧縮されます。ジャーナルの圧縮について詳しくは、[Journal（ジャーナル）](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal)を参照してください。

#### メモリの使用 {#memory-use}

WiredTiger を使用する場合、MongoDB は WiredTiger の内部キャッシュとファイルシステムキャッシュの両方を利用します。

WiredTiger の内部キャッシュは、3.4 以降、デフォルトで、以下のいずれか大きい方を使用します。

* RAM の 50％から 1 GB を減算したサイズ
* 256 MB

WiredTiger は、デフォルトで、すべてのコレクションには Snappy ブロック圧縮を、すべてのインデックスにはプレフィックス圧縮を使用します。圧縮のデフォルトはグローバルレベルで設定できます。コレクションおよびインデックスの作成時に、コレクションごと、およびインデックスごとに設定することもできます。

WiredTiger の内部キャッシュのデータでは、ディスク上の形式とは異なるデータ表現が使用されます。

* ファイルシステムキャッシュのデータはディスク上の形式と同じで、データファイルの圧縮によるメリットも同等です。ファイルシステムキャッシュは、オペレーティングシステムがディスク I/O を低減するために使用します。

WiredTiger の内部キャッシュに読み込まれるインデックスでは、ディスク上の形式とは異なるデータ表現が使用されますが、インデックスのプレフィックス圧縮を使用して RAM の使用量を削減できます。

インデックスのプレフィックス圧縮は、インデックスが作成されたフィールドの共通のプレフィックスの重複を除去します。

WiredTiger の内部キャッシュのコレクションデータは圧縮されておらず、ディスク上の形式とは異なる表現が使用されます。ブロック圧縮をおこなうとディスクストレージ使用容量を大幅に削減できますが、サーバーがデータを操作する際にデータの展開が必要になります。

ファイルシステムキャッシュでは、MongoDB は、WiredTiger のキャッシュや他のプロセスで使用されていないすべての空きメモリを自動的に使用します。

WiredTiger の内部キャッシュのサイズを調整するには、[storage.wiredTiger.engineConfig.cacheSizeGB](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.cacheSizeGB) および [--wiredTigerCacheSizeGB](https://docs.mongodb.com/manual/reference/program/mongod/#cmdoption-wiredtigercachesizegb) を参照してください。WiredTiger の内部キャッシュのサイズは、デフォルト値よりも大きくしないでください。

### NUMA {#numa}

Non Uniform Memory Access（NUMA）を使用すると、プロセッサーコアにメモリをマップする方法をカーネルで管理できます。これにより、コアのメモリアクセスを高速化し、必要なデータに確実にアクセスできるようにする試みがおこなわれますが、NUMA は MMAP に干渉し、読み取りを予測できないのでさらに遅延が発生します。この理由から、NUMA に対応しているすべてのオペレーティングシステムの `mongod` プロセスでこの機能を無効にする必要があります。

基本的に、NUMA アーキテクチャでは、メモリは複数の CPU に接続され、複数の CPU はバスに接続されます。SMP または UMA アーキテクチャでは、メモリはバスに接続され、複数の CPU によって共有されます。スレッドが NUMA CPU のメモリを割り当てる際には、ポリシーに従って割り当てられます。デフォルトでは、スレッドのローカル CPU に接続されたメモリが割り当てられます。空きがない場合は、よりコストの高い空いている CPU のメモリが使用されます。一度割り当てられたメモリは CPU 間で移動しません。割り当ては、親スレッド（つまり、プロセスを開始したスレッド）から継承されたポリシーによって実行されます。

マシンをマルチコアの均一なメモリアーキテクチャと見なす多くのデータベースでは、これにより、最初の CPU が最初にいっぱいになり、次の CPU がその後にいっぱいになります。中核となるスレッドがメモリバッファを割り当てる場合は特にそうなります。これを解決するには、`mongod` プロセスを開始するために使用されるメインスレッドの NUMA ポリシーを変更します。

そのためには、次のコマンドを実行します。

```shell
numactl --interleaved=all <mongod> -f config
```

このポリシーでは、すべての CPU ノードでラウンドロビン方式でメモリが割り当てられるので、すべてのノードで配分が均等になります。CPU ハードウェアが複数あるシステムの場合のように、メモリに対する最も高速なアクセスが生成されるわけではありません。メモリ操作の約半分は速度が低下し、バスを経由しておこなわれますが、`mongod` は NUMA を目的として最適な方法で記述されているわけではないので、これは合理的な妥協策です。

### NUMA に関する問題 {#numa-issues}

If the `mongod` process is started from a location other than the `/etc/init.d` folder, it is probable that it will not be started with the correct NUMA policy. デフォルトポリシーによっては、問題が発生することがあります。This is because the various Linux package manager installers for MongoDB also install a service with configuration files located in `/etc/init.d` which perform the step outlined above. If you install and run MongoDB directly from an archive ( `.tar.gz`) then you will need to manually run mongod under the `numactl` process.

>[!NOTE]
>
>使用可能な NUMA ポリシーについて詳しくは、[numactl のドキュメント](https://linux.die.net/man/8/numactl)を参照してください。

MongoDB プロセスの動作は、個々の割り当てポリシーによって異なります。 

```

```

* `-membind=<nodes>`
一覧表示されたノードにのみ割り当てます。 mongod では、リストされているノードのメモリが割り当てられず、使用可能なメモリの一部が使用されない可能性があります。

* `-cpunodebind=<nodes>`
ノードでのみ実行します。 mongod は、指定されたノードのみで実行され、それらのノードで使用可能なメモリのみを使用します。

* `-physcpubind=<nodes>`
一覧に表示されたCPU（コア）でのみ実行します。 mongod は、リストされている CPU のみで実行され、それらの CPU で使用可能なメモリのみを使用します。

* `--localalloc`
常に現在のノードにメモリを割り当てますが、スレッドが実行するすべてのノードを使用します。 1 つのスレッドで割り当てが実行されている場合は、その CPU で使用可能なメモリのみが使用されます。

* `--preferred=<node>`
ノードに対する割り当てを優先しますが、優先ノードがいっぱいの場合は他のノードにフォールバックします。 ノードを定義するための相対注釈を使用できます。また、スレッドはすべてのノードで実行されます。

一部のポリシーでは、`mongod` プロセスに割り当てられるメモリが、使用可能なすべての RAM よりも少ない場合があります。MySQL とは異なり、MongoDB はオペレーティングシステムレベルのページングを積極的に回避します。その結果、使用可能であると思われるメモリよりも少ない量のメモリが `mongod` プロセスに割り当てられることがあります。

#### スワッピング {#swapping}

データベースはその性質上、大量のメモリを使用するので、オペレーティングシステムレベルのスワッピングを無効にする必要があります。MongoDB プロセスは、スワッピングしないように設計されています。

#### リモートファイルシステム {#remote-filesystems}

MongoDBの内部データファイル（mongodプロセスデータベースファイル）には、遅延が多すぎるので、NFSなどのリモートファイルシステムは推奨されません。 Oak Blob の格納に必要な共有ファイルシステム（FileDataStore）と混同しないでください。この場合は、NFS が推奨されます。

#### 先読み {#read-ahead}

ランダム読み取りを使用してページをページングする際に、不要なブロックがディスクから読み取られないように、読み取り先を調整する必要があります。これにより、I/O帯域幅が不要に消費されます。

### Linux に関する要件 {#linux-requirements}

#### カーネルの最小バージョン {#minimum-kernel-versions}

* **2.6.23** for `ext4` filesystems

* **2.6.25** for `xfs` filesystems

#### データベースディスクの推奨設定 {#recommended-settings-for-database-disks}

**atime の無効化**

データベースを格納するディスクについては `atime` を無効にすることをお勧めします。

**NOOP ディスクスケジューラーの設定**

手順は次のとおりです。

まず、現在設定されている I/O スケジューラーを確認します。そのためには、次のコマンドを実行します。

```shell
cat /sys/block/sdg/queue/scheduler
```

応答が `noop` である場合、さらに操作をおこなう必要はありません。

設定されている I/O スケジューラーが NOOP でない場合は、次のコマンドを実行して変更できます。

```shell
echo noop > /sys/block/sdg/queue/scheduler
```

**先読み値の調整**

MongoDB データベースが実行されるディスクでは、値を 32 にすることをお勧めします。これは 16 キロバイトに相当します。これを設定するには、次のコマンドを実行します。

```shell
sudo blockdev --setra <value> <device>
```

#### NTP の有効化 {#enable-ntp}

MongoDB データベースをホストしているマシンに NTP がインストールされ、実行されていることを確認します。例えば、CentOS マシンで yum パッケージマネージャーを使用してインストールできます。

```shell
sudo yum install ntp
```

NTP デーモンがインストールされ、正常に起動したら、ドリフトファイルでサーバーの時刻のずれを確認できます。

#### Transparent Huge Pages の無効化 {#disable-transparent-huge-pages}

Red Hat Linux では、Transparent Huge Pages（THP）と呼ばれるメモリ管理アルゴリズムが使用されます。このオペレーティングシステムをデータベースワークロードに使用している場合は、これを無効にすることをお勧めします。

無効にするには、次の手順に従います。

1. Open the `/etc/grub.conf` file in the text editor of your choice.
1. grub.conf ファイルに次の行を追加します。

   ```xml
   transparent_hugepage=never
   ```

1. 最後に、次のコマンドを実行して、設定が有効になっているかどうかを確認します。

   ```shell
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   THP が無効になっている場合、このコマンドの出力は次のようになります。

   ```xml
   always madvise [never]
   ```

>[!NOTE]
>
>Transparent Huge Pages について詳しくは、こちらの[記事](https://access.redhat.com/solutions/46111)を参照してください。

#### NUMA の無効化 {#disable-numa}

In most installations where NUMA is enabled, the MongoDB daemon will disable it automatically if it is run as a service from the `/etc/init.d` folder.

これに該当しない場合は、各プロセスレベルで NUMA を無効にすることができます。無効にするには、次のコマンドを実行します。

```shell
numactl --interleave=all <path_to_process>
```

Where `<path_to_process>` is the path to the mongod process.

続いて、次のコマンドを実行してゾーンの再利用を無効にします。

```shell
echo 0 > /proc/sys/vm/zone_reclaim_mode
```

#### mongod プロセスの ulimit 設定の調整 {#tweak-the-ulimit-settings-for-the-mongod-process}

Linux では、`ulimit` コマンドによるリソースの割り当てを設定で制御できます。これは、ユーザーごとにおこなうことも、プロセスごとにおこなうこともできます。

[MongoDB における ulimit の推奨設定](https://docs.mongodb.org/manual/reference/ulimit/#recommended-ulimit-settings)に従って、mongod プロセスの ulimit を設定することをお勧めします。

#### MongoDB の I/O パフォーマンスのテスト {#test-mongodb-i-o-performance}

MongoDB には、I/O パフォーマンスのテストを目的とした `mongoperf` というツールが用意されています。このツールを使用して、インフラストラクチャを構成しているすべての MongoDB インスタンスのパフォーマンスをテストすることをお勧めします。

`mongoperf` の使用方法については、[MongoDB のドキュメント](https://docs.mongodb.org/manual/reference/program/mongoperf/)を参照してください。

>[!NOTE]
>
>`mongoperf` は、MongoDB が実行されているプラットフォームにおける MongoDB のパフォーマンスの指標となるように設計されています。そのため、実稼動システムでのパフォーマンスを保証するものとして結果を捉えないでください。
>
>より正確なパフォーマンス結果を得るために、`fio` Linux ツールを使用して補完テストを実行できます。

**デプロイメントを構成している仮想マシンでの読み取りパフォーマンスのテスト**

ツールをインストールしたら、テストを実行するために MongoDB データベースディレクトリに切り替えます。続いて、次の設定で `mongoperf` を実行して、最初のテストを開始します。

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true}" | mongoperf
```

この出力がすべての MongoDB インスタンスの 32 のスレッドで最大 1 秒あたり 2 ギガバイト（2 GB/秒）、および 500,000 IOPS に達しているのが望ましい結果です。

`mmf:true` パラメーターを設定して、2 回目のテストを実行します。今回はメモリマップファイルを使用します。

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true,mmf:true}" | mongoperf
```

2 回目のテストの出力は最初のテストよりもかなり高くなり、メモリ転送のパフォーマンスが良くなったことを示します。

>[!NOTE]
>
>テストの実行時には、オペレーティングシステムの監視システムで対象の仮想マシンの I/O 使用率統計を確認してください。I/O 読み取りが 100 パーセント未満の値を示している場合は、仮想マシンに問題がある可能性があります。

**プライマリ MongoDB インスタンスの書き込みパフォーマンスのテスト**

次に、同じ設定で MongoDB データベースディレクトリから `mongoperf` を実行して、プライマリ MongoDB インスタンスの I/O 書き込みパフォーマンスを確認します。

```shell
echo "{nThreads:32,fileSizeMB:1000,w:true}" | mongoperf
```

この出力が 1 秒あたり 12 メガバイトで、約 3,000 IOPS に達していて、スレッド数による変動がほとんどないのが望ましい結果です。

## 仮想化環境に関する手順 {#steps-for-virtualised-environments}

### VMWare {#vmware}

VMWare ESX を使用して仮想化環境を管理およびデプロイする場合は必ず、MongoDB の操作に対応するように、ESX コンソールで次の設定を実行してください。

1. メモリバルーニングを無効にします。
1. MongoDB データベースをホストする仮想マシンのメモリを事前に割り当てて確保します。
1. Storage I/O Control を使用して、十分な I/O を `mongod` プロセスに割り当てます。
1. [CPU 予約](https://pubs.vmware.com/vsphere-4-esx-vcenter/index.jsp?topic=/com.vmware.vsphere.vmadmin.doc_41/vsp_vm_guide/configuring_virtual_machines/t_allocate_cpu_resources.html)を設定して、MongoDB をホストするマシンの CPU リソースを確保します。

1. 準仮想化 I/O ドライバーの使用を検討します。For more information on how to do this, check this [knowledgebase article](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&amp;cmd=displayKC&amp;externalId=1010398).

### Amazon Web Services {#amazon-web-services}

Amazon Web Services に MongoDB をセットアップする方法については、MongoDB Web サイトの [AWS 統合の設定](https://docs.cloud.mongodb.com/tutorial/configure-aws-settings/)に関する記事を参照してください。

## デプロイメントの前に MongoDB をセキュリティ保護する {#securing-mongodb-before-deployment}

デプロイメント前にデータベースの設定を保護する方法についてのアドバイスは、[MongoDB の安全なデプロイ](https://blogs.adobe.com/security/2015/07/securely-deploying-mongodb-3-0.html)に関する投稿を参照してください。

## Dispatcher {#dispatcher}

### Dispatcher のオペレーティングシステムの選択 {#choosing-the-operating-system-for-the-dispatcher}

MongoDB デプロイメントが適切に機能するには、Dispatcher をホストするオペレーティングシステムが **Apache httpd** **バージョン 2.4 以降**&#x200B;を実行している必要があります。

また、セキュリティへの影響を最小限に抑えるために、ビルドで使用されているすべてのライブラリが最新であることを確認してください。

### Dispatcher 設定 {#dispatcher-configuration}

一般的な Dispatcher 設定は、1 つの AEM インスタンスの 10 倍から 20 倍までの要求スループットに対応します。

Dispatcher は概してステートレスなので、水平方向に簡単にスケーリングできます。一部のデプロイメントでは、作成者が特定のリソースにアクセスできないように制限する必要があります。こうした理由から、オーサーインスタンスで Dispatcher を使用することを強くお勧めします。

Dispatcher を使用せずに AEM を実行するには、SSL ターミネーションとロードバランシングを別のアプリケーションで実行する必要があります。これが必要なのは、セッションには、セッションが作成された AEM インスタンスに対する親和性が必要であるからです。この概念は、スティッキー接続と呼ばれます。この目的は、コンテンツの更新が最小限の遅延でおこなわれるようにすることです。

設定方法について詳しくは、[Dispatcher のドキュメント](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html)を参照してください。

### その他の設定 {#additional-configuration}

#### スティッキー接続 {#sticky-connections}

スティッキー接続では、1 人のユーザーのパーソナライズされたページとセッションデータがすべて AEM の同じインスタンスで作成されます。このデータはインスタンスに格納されるので、同じユーザーからの後続の要求は同じインスタンスに戻ります。

AEM インスタンスに要求をルーティングするすべての内部レイヤーでスティッキー接続を有効にして、後続の要求が同じ AEM インスタンスに到達するようにすることをお勧めします。他の方法では、インスタンス間でコンテンツが更新される際に顕著な遅延が発生しますが、スティッキー接続を使用すると、遅延を最小限に抑えることができます。

#### 長い有効期限 {#long-expires}

デフォルトでは、AEM Dispatcher から送信されたコンテンツには Last-Modified および Etag ヘッダーが含まれていますが、コンテンツの有効期限を示すものはありません。これにより、ユーザーインターフェイスは常にリソースの最新バージョンを取得しますが、リソースが変更されているかどうかを確認するためにブラウザーで GET 操作が実行されることも意味します。その結果、ページの読み込みに応じて、複数の要求に対して 304（Not Modified）の HTTP 応答が返されることがあります。有効期限がないことがわかっているリソースについては、Expires ヘッダーを設定して Last-Modified および ETag ヘッダーを削除すると、コンテンツがキャッシュされ、Expires ヘッダーの日付になるまで、それ以上の更新要求はおこなわれなくなります。

ただし、この方法を使用すると、Expires ヘッダーの有効期限に達する前にブラウザーでリソースを期限切れにするための適当な方法がなくなります。この問題を緩和するために、クライアントライブラリに不変の URL を使用するように HtmlClientLibraryManager を設定できます。

これらの URL が変更されることはありません。URL に含まれているリソースの本文が変更された場合、変更内容が URL に自動的に反映され、ブラウザーから適切なバージョンのリソースが要求されます。

デフォルト設定では、HtmlClientLibraryManager にセレクターが追加されます。セレクターがある場合、セレクターはそのままの状態でリソースが Dispatcher にキャッシュされます。さらに、このセレクターを使用して、有効期限の動作が適切になるようにすることもできます。The default selector follows the `lc-.*?-lc` pattern. 次の Apache httpd 設定のディレクティブでは、このパターンと一致するすべての要求が、適切な有効期限を使用して処理されます。

```xml
Header set Expires "Tue, 20 Jan 2037 04:20:42 GMT" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header set Cache-Control "public, no-transform, max-age=267840000" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset ETag "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Last-Modified "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Pragma "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
```

#### スニッフィングなし {#no-sniff}

content-type がないコンテンツが送信された場合、多くのブラウザーでは、コンテンツの最初の数バイトを読み取って、コンテンツのタイプを推測しようとします。これは、「スニッフィング」と呼ばれます。リポジトリに書き込むことができるユーザーがコンテンツタイプを指定せずに悪意のあるコンテンツをアップロードする可能性があるので、スニッフィングによってセキュリティ上の脆弱性が生じます。

そのため、Dispatcher で処理されるリソースに `no-sniff` ヘッダーを追加することをお勧めします。ただし、Dispatcher ではヘッダーはキャッシュされません。これは、ローカルファイルシステムから提供されたコンテンツのコンテンツタイプが、生成元の AEM サーバーの元の content-type ヘッダーではなく、拡張子によって特定されることを意味します。

キャッシュされたリソースを Web アプリケーションがファイルタイプなしで提供することがないとわかっている場合は、スニッフィングなしを有効にしても問題ありません。

スニッフィングなしは包括的に有効にすることができます。

```xml
Header set X-Content-Type-Options "nosniff"
```

また、選択的に有効にすることもできます。

```xml
RewriteCond %{REQUEST_URI} \.(?:js|jsonp)$ [OR]
RewriteCond %{QUERY_STRING} (callback|jsonp|cb)=\w+
RewriteRule .* - [E=jsonp_request:1]
Header set X-Content-Type-Options "nosniff"  env=jsonp_request
Header setifempty Content-Type application/javascript env=jsonp_request
```

#### コンテンツセキュリティポリシー {#content-security-policy}

Dispatcher のデフォルト設定では、オープンなコンテンツセキュリティポリシー（CSP）が許可されます。これにより、ブラウザーサンドボックスのデフォルトポリシーが適用されるすべてのドメインからページにリソースを読み込むことができます。

信頼できない、または検証されていない外部サーバーから javascript エンジンにコードが読み込まれることを防ぐために、リソースの読み込み元を制限するようにしてください。

CSP では、ポリシーを微調整できます。ただし、複雑なアプリケーションでは、ポリシーの制限を厳格にしすぎると、ユーザーインターフェイスの一部が機能しなくなる可能性があるので、CSP ヘッダーを慎重に開発する必要があります。

>[!NOTE]
>
>この仕組みについて詳しくは、[コンテンツセキュリティポリシーに関する OWASP のページ](https://www.owasp.org/index.php/Content_Security_Policy)を参照してください。

### サイジング {#sizing}

サイジングについて詳しくは、[ハードウェアのサイジングのガイドライン](/help/managing/hardware-sizing-guidelines.md)を参照してください。

### MongoDB のパフォーマンスの最適化 {#mongodb-performance-optimization}

MongoDB のパフォーマンスについての一般的な情報は、[MongoDB のパフォーマンスの分析](https://docs.mongodb.org/manual/administration/analyzing-mongodb-performance/)に関するページを参照してください。

## 既知の制限事項 {#known-limitations}

### 同時インストール {#concurrent-installations}

MongoMK では、1 つのデータベースで複数の AEM インスタンスを同時に使用することがサポートされていますが、同時インストールはサポートされていません。

この制限を回避するには、まず 1 つのメンバーでインストールを実行し、最初のインストールが完了した後で、他のメンバーを追加します。

### ページ名の長さ {#page-name-length}

If AEM is running on a MongoMK persistence manager deployment, [page names are limited to 150 characters.](/help/sites-authoring/managing-pages.md)

>[!NOTE]
>
>[MongoDB自体の既知の制限としきい値についても詳しくは](https://docs.mongodb.com/manual/reference/limits/) 、MongoDBのドキュメントを参照してください。

