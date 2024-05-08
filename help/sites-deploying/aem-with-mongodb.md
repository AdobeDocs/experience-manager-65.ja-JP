---
title: Adobe Experience Manager と MongoDB
description: MongoDB を備えた Adobe Experience Manager を正常にデプロイするために必要なタスクと考慮事項について説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
docset: aem65
exl-id: 70a39462-8584-4c76-a097-05ee436247b7
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '6185'
ht-degree: 100%

---

# Adobe Experience Manager と MongoDB{#aem-with-mongodb}

この記事では、MongoDB を備えた AEM（Adobe Experience Manager）を正常にデプロイするために必要なタスクと考慮事項に関する知識を深めることを目的としています。

デプロイメントについて詳しくは、このドキュメントの[デプロイとメンテナンス](/help/sites-deploying/deploy.md)の節を参照してください。

## AEM で MongoDB を使用すべき状況 {#when-to-use-mongodb-with-aem}

MongoDB は通常、次のいずれかの条件を満たす AEM オーサーデプロイメントをサポートするために使用します。

* 1 日あたり 1,000 人を超える個別ユーザー。
* 100 人を超える同時ユーザー。
* 大量のページ編集。
* 大規模なロールアウトまたはアクティベーション。

上記の条件が適用されるのはオーサーインスタンスのみです。すべて TarMK ベースであるパブリッシュインスタンスには適用されません。オーサーインスタンスでは、未認証のアクセスは許可されないので、ユーザー数は認証済みユーザーの数を表します。

条件が満たされない場合は、可用性に対応するために、TarMK アクティブ／スタンバイデプロイメントをお勧めします。通常は、スケーリング要件が 1 台のハードウェアで実現できる範囲を超える場合に MongoDB を検討してください。

>[!NOTE]
>
>オーサーインスタンスのサイズ設定と同時ユーザーの定義について詳しくは、[ハードウェアのサイジングのガイドライン](/help/managing/hardware-sizing-guidelines.md#authors-working-in-parallel)を参照してください。

### AEM 向けの MongoDB の最小デプロイメント {#minimal-mongodb-deployment-for-aem}

AEM 向けの MongoDB の最小デプロイメントを以下に示します。説明を簡単にするために、SSL ターミネーションコンポーネントと HTTP プロキシコンポーネントは一般化されています。これは、1 つのプライマリと 2 つのセカンダリを含む単一の MongoDB レプリカセットで構成されています。

![chlimage_1-4](assets/chlimage_1-4.png)

最小デプロイメントには、レプリカセットとして設定された 3 つの `mongod` インスタンスが必要です。1 つのインスタンスはプライマリとして選択され、その他のインスタンスはセカンダリとして選択されます。この選択は、`mongod` によって管理されます。各インスタンスにローカルディスクが接続されています。クラスターで負荷に対応できるように、1 秒あたりの I/O 操作回数（IOPS）が 3,000 を超える毎秒 12 MB以上のスループットが推奨されます。

AEM オーサーは `mongod` インスタンスに接続されます。各 AEM オーサーは 3 つの `mongod` インスタンスすべてに接続します。書き込みはプライマリに送信され、読み取りはどのインスタンスからも行うことができます。トラフィックは、Dispatcher によって、負荷に基づいてアクティブな AEM オーサーインスタンスのいずれかに分散されます。OAK データストアは `FileDataStore` であり、MongoDB の監視は、デプロイメントの場所に応じて、MMS または MongoDB Ops Manager によって提供されます。オペレーティングシステムレベルの監視とログの監視は、Splunk や Ganglia などのサードパーティソリューションによって提供されます。

このデプロイメントでは、実装が正常に機能するには、すべてのコンポーネントが必要です。コンポーネントが不足していると、実装は機能しません。

### オペレーティングシステム {#operating-systems}

AEM 6 でサポートされているオペレーティングシステムのリストについては、[技術要件のページ](/help/sites-deploying/technical-requirements.md)を参照してください。

### 環境 {#environments}

プロジェクトを実行する様々な技術チーム間で良好なコミュニケーションが取れている場合に、仮想化環境がサポートされます。このサポートには、AEM を実行しているチーム、オペレーティングシステムを所有しているチームおよび仮想化インフラストラクチャを管理しているチームが含まれます。

MongoDB インスタンスの I/O 処理能力については特定の要件があり、この要件の管理は仮想化環境を管理するチームが行う必要があります。Amazon Web Services などのクラウドデプロイメントをプロジェクトで使用する場合は、MongoDB インスタンスをサポートするための十分な I/O 処理能力と一貫性を確保できるようにインスタンスをプロビジョニングする必要があります。そうでない場合は、MongoDB プロセスと Oak リポジトリの動作が、信頼性が低い不安定なものになります。

仮想化環境では、VMWare のリソース割り当てポリシーによって MongoDB のストレージエンジンの機能が損なわれることがないように、MongoDB で特定の I/O 設定と VM 設定が必要になります。実装に成功すれば、様々なチーム間の障壁がなくなり、必要なパフォーマンスを実現するために全員が協力して取り組みます。

## ハードウェアに関する考慮事項 {#hardware-considerations}

### ストレージ {#storage}

水平方向のスケーリングを早い段階で行わなくても、読み書きのスループットが最適なパフォーマンスになるようにするには、通常、SSD ストレージまたは SSD 相当のパフォーマンスを提供するストレージが MongoDB で必要になります。

### RAM {#ram}

MMAP ストレージエンジンを使用する MongoDB バージョン 2.6 および 3.0 では、データベースの作業セットとそのインデックスが RAM に収まる必要があります。

十分な RAM がないと、パフォーマンスが大幅に低下します。作業セットとデータベースのサイズは、アプリケーションに大きく依存します。ある程度の推定は可能ですが、必要な RAM の量を判断するための最も信頼できる方法は、AEM アプリケーションを構築して負荷テストを実施することです。

負荷テストを実施する場合は、テストプロセスを支援するために、データベースの合計サイズに対する作業セットの比率を次のように想定することができます。

* SSD ストレージの場合は 1:10
* ハードディスクストレージの場合は 1:3

つまり、SSD デプロイメントの場合は、2 TB のデータベースに 200 GB の RAM が必要になります。

MongoDB 3.0 の WiredTiger ストレージエンジンにも同じ制限が適用されますが、作業セット、RAM およびページフォールトの間の相関関係はそれほど強くありません。WiredTiger は、MMAP ストレージエンジンとは異なり、メモリマッピングを使用しません。

>[!NOTE]
>
>MongoDB 3.0 を使用する AEM 6.1 のデプロイメントには、WiredTiger ストレージエンジンを使用することをお勧めします。

### データストア {#data-store}

MongoDB の作業セットの制限により、データストアを MongoDB とは独立に維持管理することをお勧めします。ほとんどの環境では、すべての AEM インスタンスに対して使用可能な NAS を使用する `FileDataStore` を使用してください。Amazon Web Services を使用する場合は、`S3 DataStore` もあります。何らかの理由でデータストアを MongoDB 内で維持管理する場合は、データストアのサイズをデータベースの合計サイズに加算し、作業セットの計算を適切に調整する必要があります。このサイズ設定では、ページフォールトを発生させずにパフォーマンスを維持するために、より多くの RAM をプロビジョニングする可能性があります。

## モニタリング {#monitoring}

プロジェクトを正常に実装するには、監視が不可欠です。十分な知識があれば、監視を行わずに AEM を MongoDB 上で実行することも可能です。しかし、その知識は、通常、デプロイメントの各セクションを専門とするエンジニアが持っているものです。

この専門知識には、通常、Apache Oak Core に取り組んでいる研究開発エンジニアや MongoDB スペシャリストが関与します。

すべてのレベルで監視を行わない場合、問題の診断には、コードベースの詳細な知識が必要になります。監視が実施され、主要な統計情報に関する適切なガイダンスが提供されれば、実装チームは異常値に的確に対応できます。

コマンドラインツールを使用してクラスターの動作のスナップショットを即座に取得することもできますが、多数のホストに対してこれをリアルタイムで行うのはほぼ不可能です。数分を超える履歴情報がコマンドラインツールで提供されることはほとんどなく、様々なタイプの指標を相互に関連付けることもできません。`mongod` のバックグラウンド同期が短期間遅くなると、見かけ上は接続されていない仮想マシンからの共有ストレージリソースに対する I/O の待機や過剰な書き込みレベルの相関関係を見つけるために手動による多大な労力が必要になります。

### MongoDB Cloud Manager {#mongodb-cloud-manager}

MongoDB Cloud Manager は、MongoDB インスタンスの監視と管理を可能にする MongoDB 提供の無料サービスです。これを使用することで、MongoDB クラスターのパフォーマンスとヘルスをリアルタイムで把握できます。また、インスタンスが Cloud Manager 監視サーバーにアクセスできる場合は、クラウドでホストされているインスタンスとプライベートにホストされているインスタンスの両方を管理できます。

このサービスを使用するには、監視サーバーに接続する MongoDB インスタンスにエージェントがインストールされている必要があります。エージェントには次の 3 つのレベルがあります。

* MongoDB サーバー上のすべての処理を完全に自動化できる自動化エージェント
* `mongod` インスタンスを監視できる監視エージェント
* スケジュールされたデータバックアップを実行できるバックアップエージェント

Cloud Manager を使用して MongoDB クラスターのメンテナンスを自動化すると、日常的なタスクの多くが容易になりますが、それは必須ではありません。また、バックアップに Cloud Manager を使用することも必須ではありません。ただし、監視を行うために Cloud Manager を選択した場合、監視は必須です。

MongoDB Cloud Manager について詳しくは、[MongoDB のドキュメント](https://docs.cloud.mongodb.com/)を参照してください。

### MongoDB Ops Manager {#mongodb-ops-manager}

MongoDB Ops Manager は、MongoDB Cloud Manager と同じソフトウェアです。登録すると、Ops Manager をダウンロードして、プライベートデータセンターまたは他のノート PC やデスクトップ PC にローカルにインストールできます。このソフトウェアは、ローカルの MongoDB データベースを使用してデータを保存し、Cloud Manager と同様に管理対象サーバーと通信します。セキュリティポリシーで監視エージェントを禁止している場合は、MongoDB Ops Manager を使用してください。

### オペレーティングシステムの監視 {#operating-system-monitoring}

AEM MongoDB クラスターを実行するには、オペレーティングシステムレベルの監視が必要です。

そのようなシステムの良い例として Ganglia があります。Ganglia は、対象範囲の状況を報告し、CPU、負荷平均、空きディスク領域などの基本的なヘルス指標にとどまらず、必要な情報の詳細を表示します。問題を診断するには、エントロピープールレベル、CPU I/O 待機、FIN_WAIT2 状態のソケットなど、下位レベルの情報が必要です。

### ログの集約 {#log-aggregation}

複数のサーバーで構成されるクラスターの場合、実稼動システムでは、ログの一元的な集約が必要になります。Splunk のようなソフトウェアでは、ログの集約をサポートしており、チームは、ログを手動で収集しなくても、アプリケーションの動作のパターンを分析できます。

## チェックリスト {#checklists}

ここでは、プロジェクトを実装する前に、AEM と MongoDB のデプロイメントを適切にセットアップするために必要な様々な手順について説明します。

### ネットワーク {#network}

1. まず、すべてのホストに DNS エントリがあることを確認します。
1. ルーティング可能な他のすべてのホストから、すべてのホストがそれぞれの DNS エントリによって解決できる必要があります。
1. すべての MongoDB ホストは、同じクラスター内の他のすべての MongoDB ホストからルーティング可能です。
1. MongoDB ホストは、MongoDB Cloud Manager およびその他の監視サーバーにパケットをルーティングできます。
1. AEM サーバーは、すべての MongoDB サーバーにパケットをルーティングできます。
1. 任意の AEM サーバーと MongoDB サーバーの間のパケット遅延は 2 ミリ秒未満であり、パケット損失がなく、標準的な配信は 1 ミリ秒以下です。
1. AEM サーバーと MongoDB サーバーの間のホップは 2 つまでです。
1. 2 つの MongoDB サーバー間のホップは 2 つまでです。
1. 任意のコアサーバー（MongoDB、AEM または任意の組み合わせ）間には、OSI レベル 3 を超えるルーターは存在しません。
1. VLAN トランキングまたは何らかの形のネットワークトンネリングを使用している場合は、パケット遅延チェックに適合している必要があります。

### AEM の設定 {#aem-configuration}

#### ノードストアの設定 {#node-store-configuration}

AEM を MongoMK と連携させて使用するように AEM インスタンスを設定する必要があります。AEM における MongoMK 実装の基盤はドキュメントノードストアです。

ノードストアの設定方法について詳しくは、[AEM でのノードストアとデータストアの設定](/help/sites-deploying/data-store-config.md)を参照してください。

MongoDB の最小デプロイメントに対応するドキュメントノードストアの設定例を以下に示します。

```xml
# org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config
#MongoDB server details
mongodburi=mongodb://aem:aempassword@mongodbserver1.customer.com:27000,mongodbserver2.customer.com:27000

#Name of MongoDB database to use
db=aem

#Store binaries in custom BlobStore for example, FileDataStore
customBlobStore=true

cache=2048
blobCacheSize=1024
```

ここで、

* `mongodburi`
AEM が接続する必要がある MongoDB サーバー。接続は、デフォルトレプリカセットの既知のすべてのメンバーに対して確立されます。MongoDB Cloud Manager を使用する場合は、サーバーセキュリティが有効になります。そのため、適切なユーザー名とパスワードが接続文字列に含まれている必要があります。エンタープライズ以外のバージョンの MongoDB では、ユーザー名とパスワードによる認証のみがサポートされています。接続文字列の構文について詳しくは、こちらの[ドキュメント](https://docs.mongodb.org/manual/reference/connection-string/)を参照してください。

* `db`データベースの名前。AEM のデフォルトは `aem-author` です。

* `customBlobStore`
デプロイメントでバイナリがデータベースに保存される場合、バイナリは作業セットの一部になります。そのため、バイナリを MongoDB 内に格納せず、できれば、NAS 上の `FileSystem` データストアのような代替データストアに格納することをお勧めします。

* `cache`
キャッシュサイズ（MB 単位）。この領域は `DocumentNodeStore` で使用される様々なキャッシュに配分されます。デフォルトは 256 MB です。ただし、キャッシュが大きい方が Oak の読み取りパフォーマンスは向上します。

* `blobCacheSize`
頻繁に使用される BLOB は、データストアから再取得しなくて済むように、AEM にキャッシュできます。これは、特に MongoDB データベースに BLOB を格納する場合に、パフォーマンスへの影響が大きくなります。オペレーティングシステムレベルのディスクキャッシュは、ファイルシステムベースのすべてのデータストアに効果的です。

#### データストアの設定 {#data-store-configuration}

データストアは、しきい値より大きいサイズのファイルを格納するために使用されます。そのしきい値以下のファイルは、ドキュメントノードストア内にプロパティとして格納されます。`MongoBlobStore` を使用する場合、Blob を格納するための専用のコレクションが MongoDB に作成されます。このコレクションは `mongod` インスタンスの作業セットに含まれ、パフォーマンス上の問題を回避するには、より大きな RAM が `mongod` に必要になります。そのため、実稼動デプロイメントでは `MongoBlobStore` を使用せず、すべての AEM インスタンス間で共有される NAS 提供の `FileDataStore` を使用する設定をお勧めします。オペレーティングシステムレベルのキャッシュはファイルの管理に効率的なので、ディスク上のファイルの最小サイズは、ディスクのブロックサイズに近い値に設定してください。これにより、ファイルシステムが効率的に使用され、多くの小さなドキュメントが `mongod` インスタンスのワーキングセットに過度な影響を与えることがありません。

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
サイズ（バイト単位）。このサイズ以下のバイナリは、ドキュメントノードストアに格納されます。BLOB の ID を格納するのではなく、バイナリの内容が格納されます。このサイズを超えるバイナリについては、バイナリの ID がドキュメントのプロパティとしてノードのコレクションに格納されます。また、バイナリの本文はディスク上の `FileDataStore` に格納されます。一般的なファイルシステムのブロックサイズは 4,096 バイトです。

* `path`
データストアのルートのパスです。MongoMK デプロイメントの場合、このパスは、すべての AEM インスタンスで使用可能な共有ファイルシステムである必要があります。通常は、NAS（ネットワーク接続ストレージ）サーバーが使用されます。Amazon Web Services のようなクラウドデプロイメントの場合は、`S3DataFileStore` を使用することもできます。

* `cacheSizeInMB`
バイナリキャッシュの合計サイズ（メガバイト単位）です。`maxCacheBinarySize` 設定より小さいバイナリのキャッシュに使用されます。

* `maxCachedBinarySize`
バイナリキャッシュにキャッシュされるバイナリの最大サイズ（バイト単位）です。ファイルシステムベースのデータストアを使用する場合、バイナリはオペレーティングシステムによって既にキャッシュされているので、データストアのキャッシュに大きい値を使用することはお勧めしません。

#### クエリヒントの無効化 {#disabling-the-query-hint}

すべてのクエリと共に送信されるクエリヒントを無効にすることをお勧めします。それには、AEM の起動時にプロパティ `-Doak.mongo.disableIndexHint=true` を付加します。これにより、MongoDB では、内部統計に基づいて最も適切なインデックスで計算が行われます。

クエリヒントが無効でない場合は、インデックスのパフォーマンスをチューニングしても AEM のパフォーマンスには影響しません。

#### MongoMK の永続キャッシュの有効化 {#enable-persistent-cache-for-mongomk}

I/O の読み取りパフォーマンスを高くして環境での処理速度を最大化するには、MongoDB デプロイメントで永続キャッシュ設定を有効にすることをお勧めします。詳しくは、[Jackrabbit Oak のドキュメント](https://jackrabbit.apache.org/oak/docs/nodestore/persistent-cache.html)を参照してください。

## MongoDB オペレーティングシステムの最適化 {#mongodb-operating-system-optimizations}

### オペレーティングシステムのサポート {#operating-system-support}

MongoDB 2.6 で使用しているメモリマップストレージエンジンは、RAM とディスク間のオペレーティングシステムレベル管理のいくつかの側面に影響されます。MongoDB インスタンスのクエリと読み取りのパフォーマンスを向上させるには、ページフォールトと呼ばれることが多い低速な I/O 操作を回避または排除する必要があります。これらの問題は、特に `mongod` プロセスに適用されるページフォールトです。オペレーティングシステムレベルのページフォールトと混同しないでください。

高速な操作のためには、既に RAM に存在しているデータにのみ MongoDB データベースがアクセスする必要があります。アクセスする必要があるデータは、インデックスとデータで構成されています。インデックスとデータのこのコレクションは、作業セットと呼ばれます。使用可能な RAM よりも作業セットが大きい場合、MongoDB はディスクからそのデータをページインする必要があり（これにより、I/O コストが発生します）、既にメモリ内にある他のデータが消去されます。この消去が原因となってデータがディスクから再度読み込まれると、ページフォールトが増えてパフォーマンスが低下します。作業セットが動的で変動する場合は、操作をサポートするために、さらに多くのページフォールトが発生します。

MongoDB は、Linux® の様々なフレーバー、Windows、Mac OS を含む、いくつかのオペレーティングシステムで動作します。詳しくは、[https://docs.mongodb.com/manual/installation/#supported-platforms](https://docs.mongodb.com/manual/installation/#supported-platforms) を参照してください。MongoDB のオペレーティングシステムレベルのレコメンデーションは、選択したオペレーティングシステムによって異なります。これらは [https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration](https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration) に掲載されていますが、ここでも簡単にまとめておきます。

#### Linux® {#linux}

* Transparent Huge Page（THP）および defrag を無効にします。詳しくは、[Transparent Huge Page（THP）の設定についての説明](https://docs.mongodb.com/manual/tutorial/transparent-huge-pages/)を参照してください。
* 使用状況に合わせて、データベースファイルを格納するデバイスの [readahead 設定を調整](https://docs.mongodb.com/manual/administration/production-notes/#readahead)します。

   * MMAPv1 ストレージエンジンでは、作業セットが利用可能な RAM よりも大きく、ドキュメントのアクセスパターンがランダムな場合、readahead を 32 または 16 に下げることを検討します。様々な設定を評価して、常駐メモリを最大化しページフォールト回数を低減できる最適な値を見つけます。
   * WiredTiger ストレージエンジンでは、ストレージメディアタイプ（回転式のディスク、SSD など）にかかわらず、readahead を 0 に設定します。一般に、readahead の値を大きくすることで測定可能、再現可能かつ信頼性の高いメリットがあることがテストの結果わかる場合を除き、readahead の推奨設定を使用します。[MongoDB のプロフェッショナルサポート](https://docs.mongodb.com/manual/administration/production-notes/#readahead)で、0 以外の readahead 設定を使用する場合のアドバイスとガイダンスを受けることができます。

* 仮想環境で RHEL 7／CentOS 7 を実行している場合は、Tuned ツールを無効にします。
* 仮想環境で RHEL 7／CentOS 7 を実行すると、パフォーマンスのスループットから得られたパフォーマンスプロファイルが Tuned ツールによって自動的に呼び出され、その結果、readahead 設定が自動的に 4 MB に設定されます。この設定は、パフォーマンスに悪影響を及ぼす可能性があります。
* SSD ドライブでは、noop または deadline ディスクスケジューラーを使用します。
* ゲスト VM での仮想化ドライブでは、noop ディスクスケジューラーを使用します。
* NUMA を無効にするか、`vm.zone_reclaim_mode` を 0 に設定し、ノードインタリーブを指定して [mongod](https://docs.mongodb.com/manual/administration/production-notes/#readahead) インスタンスを実行します。詳しくは、[MongoDB and NUMA Hardware](https://docs.mongodb.com/manual/administration/production-notes/#readahead)（英語）を参照してください。

* 使用状況に合わせて、ハードウェアの ulimit 値を調整します。同じユーザーで複数の [mongod](https://docs.mongodb.com/manual/reference/program/mongod/#bin.mongod) または [mongos](https://docs.mongodb.com/manual/reference/program/mongos/#bin.mongos) インスタンスを実行する場合は、適宜 ulimit 値を拡張します。詳しくは、[UNIX® ulimit Settings](https://docs.mongodb.com/manual/reference/ulimit/)（英語）を参照してください。

* [dbPath](https://docs.mongodb.com/manual/reference/configuration-options/#storage.dbPath) マウントポイントに noatime を使用します。
* デプロイメントにとって十分なファイルハンドル数（fs.file-max）、カーネルの pid の制限（kernel.pid_max）およびプロセスごとの最大スレッド数（kernel.threads-max）を設定します。大規模なシステムでは、まず以下の設定から試すことをお勧めします。

   * fs.file-max の値：98000
   * kernel.pid_max の値：64000
   * andkernel.threads-max の値：64000

* システムに、スワップ領域が設定されていることを確認します。適切なサイジングについて詳しくは、オペレーティングシステムのドキュメントを参照してください。
* システムのデフォルト TCP キープアライブが正しく設定されていることを確認します。レプリカセットおよびシャードクラスターでは、300 の値を設定すると、多くの場合、パフォーマンスが向上します。詳しくは、Frequently Asked Questions（よくある質問）の [Does TCP keepalive time affect MongoDB Deployments?](https://docs.mongodb.com/manual/faq/diagnostics/#faq-keepalive) を参照してください。

#### Windows {#windows}

* NTFS の「最終アクセス時刻」の更新を無効にすることを検討します。この設定は、Unix 系システムで atime を無効にする場合と似ています。

### WiredTiger {#wiredtiger}

MongoDB 3.2 以降、MongoDB のデフォルトのストレージエンジンは WiredTiger ストレージエンジンとなっています。このエンジンは、堅牢で拡張性の高い機能を備えており、あらゆる一般的なデータベースワークロードにはるかに適しています。以下では、これらの機能について説明します。

#### ドキュメントレベルの同時実行性 {#document-level-concurrency}

WiredTiger では、書き込み操作にドキュメントレベルの同時実行制御を使用します。そのため、複数のクライアントが特定のコレクションの異なるドキュメントを同時に変更できます。

ほとんどの読み取り操作と書き込み操作で、WiredTiger は楽観的同時実行制御を使用します。WiredTiger は、グローバルレベル、データベースレベルおよびコレクションレベルでのインテントロックのみを使用します。ストレージエンジンが 2 つの操作間の競合を検出すると、一方の操作で書き込みの競合が発生するので、MongoDB がその操作を透過的に再試行します。一部のグローバル操作（通常、複数のデータベースが関与する短時間の操作）では、グローバルな「インスタンス全体」のロックが引き続き必要です。

コレクションの削除など、その他の一部の操作では、排他的データベースロックが引き続き必要です。

#### スナップショットとチェックポイント {#snapshots-and-checkpoints}

WiredTiger では、マルチバージョン同時実行制御（MVCC）を使用しています。操作の開始時に、WiredTiger はトランザクションにデータの特定の時点のスナップショットを提供します。スナップショットは、メモリ内データの一貫性のあるビューを提供します。

WiredTiger は、ディスクに書き込む際、すべてのデータファイルでの整合性が保たれるように、スナップショットのすべてのデータをディスクに書き込みます。この[永続化](https://docs.mongodb.com/manual/reference/glossary/#term-durable)されたデータは、データファイル内のチェックポイントとして機能します。チェックポイントにより、最後のチェックポイントに至るまで、データファイルの一貫性が確保されます。つまり、チェックポイントは回復ポイントとして機能することができます。

MongoDB では、60 秒間隔または 2 GB のジャーナルデータごとにチェックポイントを作成する（スナップショットデータをディスクに書き込む）ように、WiredTiger を設定します。

新しいチェックポイントの書き込み中は、以前のチェックポイントが引き続き有効となります。そのため、新しいチェックポイントの書き込み中に MongoDB が終了したり、エラーが発生した場合でも、再起動時には最後の有効なチェックポイントから MongoDB を復元できます。

WiredTiger のメタデータテーブルがアトミックに更新されて、新しいチェックポイントを参照するようになると、新しいチェックポイントにアクセスできるようになると共に、新しいチェックポイントが永続化されます。新しいチェックポイントにアクセスできるようになると、WiredTiger は古いチェックポイントからページを解放します。

WiredTiger を使用すると、[ジャーナル処理](https://docs.mongodb.com/manual/reference/glossary/#term-durable)さえ行わずに、MongoDB を最後のチェックポイントから復元できます。ただし、最後のチェックポイントが作成された後の変更を復元するには、[ジャーナル処理](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal)を有効にして実行します。

#### ジャーナル {#journal}

WiredTiger では、トランザクションログの先行書き込みと[チェックポイント](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-checkpoints)を組み合わせて、データの永続性を確保しています。

WiredTiger ジャーナルにより、チェックポイント間に行われたすべてのデータ変更が永続化されます。チェックポイント間で MongoDB が終了した場合、MongoDB はジャーナルを使用して、最後のチェックポイント以降に変更されたすべてのデータを再現します。MongoDB がジャーナルデータをディスクに書き込む頻度について詳しくは、[Journaling Process](https://docs.mongodb.com/manual/core/journaling/#journal-process)（英語）を参照してください。

WiredTiger のジャーナルは、[snappy](https://docs.mongodb.com/manual/core/journaling/#journal-process) 圧縮ライブラリを使用して圧縮されます。別の圧縮アルゴリズムを指定する場合や、圧縮しない場合は、[storage.wiredTiger.engineConfig.journalCompressor](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.journalCompressor) 設定を使用します。

詳しくは、[Journaling with WiredTiger](https://docs.mongodb.com/manual/core/journaling/#journaling-wiredtiger)（英語）を参照してください。

>[!NOTE]
>
>WiredTiger の最小ログレコードサイズは 128 バイトです。ログレコードが 128 バイト以下の場合、WiredTiger はそのレコードを圧縮しません。
>
>[storage.journal.enabled](https://docs.mongodb.com/manual/reference/configuration-options/#storage.journal.enabled) を false に設定すると、ジャーナル処理を無効にすることができ、ジャーナルを維持するためのオーバーヘッドを削減できます。
>
>[スタンドアロン](https://docs.mongodb.com/manual/reference/glossary/#term-standalone)インスタンスについては、ジャーナルを使用しないと、チェックポイント間で MongoDB が予期せず終了したときに一部のデータ変更が失われることになります。[レプリカセット](https://docs.mongodb.com/manual/reference/glossary/#term-replica-set)のメンバーについては、レプリケーションプロセスで持続性が十分に保証される可能性があります。

#### 圧縮 {#compression}

WiredTiger を使用する場合、MongoDB では、すべてのコレクションおよびインデックスで圧縮がサポートされます。圧縮を使用すると、必要なストレージ容量を最小限に抑えることができますが、その分 CPU の負荷が高くなります。

デフォルトで、WiredTiger は、すべてのコレクションで [snappy](https://docs.mongodb.com/manual/reference/glossary/#term-snappy) 圧縮ライブラリを使用したブロック圧縮を、すべてのインデックスで[プレフィックス圧縮](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression)を使用します。

コレクションでは、[zlib](https://docs.mongodb.com/manual/reference/glossary/#term-zlib) によるブロック圧縮も利用できます。別の圧縮アルゴリズムを指定する場合や、圧縮しない場合は、[storage.wiredTiger.collectionConfig.blockCompressor](https://docs.mongodb.com/manual/reference/glossary/#term-zlib) 設定を使用します。

インデックスで[プレフィックス圧縮](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression)を無効にするには、[storage.wiredTiger.indexConfig.prefixCompression](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.indexConfig.prefixCompression)設定を使用します。

圧縮設定は、コレクションおよびインデックスの作成時に、コレクションごとおよびインデックスごとに設定することもできます。[ストレージエンジンオプションの指定方法](https://docs.mongodb.com/manual/reference/method/db.createCollection/#create-collection-storage-engine-options)および [db.collection.createIndex() の storageEngine](https://docs.mongodb.com/manual/reference/method/db.collection.createIndex/#createindex-options) オプションを参照してください。

ほとんどのワークロードでは、デフォルトの圧縮設定を使用すると、ストレージの効率性の要件と処理速度の要件のバランスをとることができます。

デフォルトで、WiredTiger のジャーナルも圧縮されます。ジャーナルの圧縮について詳しくは、[Journal](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal)（英語）を参照してください。

#### メモリの使用 {#memory-use}

WiredTiger を使用する場合、MongoDB は WiredTiger の内部キャッシュとファイルシステムキャッシュの両方を使用します。

WiredTiger の内部キャッシュは、3.4 以降、デフォルトで、以下のいずれか大きい方を使用します。

* RAM の 50％から 1 GB を減算したサイズ
* 256 MB

WiredTiger は、デフォルトで、すべてのコレクションには Snappy ブロック圧縮を使用し、すべてのインデックスにはプレフィックス圧縮を使用します。圧縮のデフォルトはグローバルレベルで設定できます。コレクションおよびインデックスの作成時に、コレクションごとおよびインデックスごとに設定することもできます。

WiredTiger の内部キャッシュのデータでは、ディスク上の形式とは異なるデータ表現が使用されます。

* ファイルシステムキャッシュのデータはディスク上の形式と同じで、データファイルの圧縮によるメリットも同等です。ファイルシステムキャッシュは、オペレーティングシステムがディスク I/O を低減するために使用します。

WiredTiger の内部キャッシュに読み込まれるインデックスでは、ディスク上の形式とは異なるデータ表現が使用されますが、インデックスのプレフィックス圧縮を使用して RAM の使用量を削減できます。

インデックスのプレフィックス圧縮は、インデックスが作成されたフィールドの共通のプレフィックスの重複を除去します。

WiredTiger の内部キャッシュのコレクションデータは圧縮されておらず、ディスク上の形式とは異なる表現が使用されます。ブロック圧縮を行うとディスクストレージ使用容量を大幅に削減できますが、サーバーがデータを操作する際にデータの圧縮解除が必要になります。

ファイルシステムキャッシュでは、MongoDB は、WiredTiger のキャッシュや他のプロセスで使用されていないすべての空きメモリを自動的に使用します。

WiredTiger の内部キャッシュのサイズを調整するには、[storage.wiredTiger.engineConfig.cacheSizeGB](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.cacheSizeGB) および [--wiredTigerCacheSizeGB](https://docs.mongodb.com/manual/reference/program/mongod/#cmdoption-wiredtigercachesizegb) を参照してください。WiredTiger の内部キャッシュのサイズは、デフォルト値よりも大きくしないでください。

### NUMA {#numa}

NUMA（Non Uniform Memory Access）を使用すると、プロセッサーコアにメモリをマップする方法をカーネルで管理できます。このプロセスでは、コアのメモリアクセスを高速化し、必要なデータに確実にアクセスできるように試みますが、NUMA が MMAP に干渉し、読み取りを予測できないのでさらに遅延が発生します。そのため、対応できるすべてのオペレーティングシステムで、`mongod` プロセスの NUMA を無効にする必要があります。

基本的に、NUMA アーキテクチャでは、メモリは複数の CPU に接続され、複数の CPU はバスに接続されます。SMP または UMA アーキテクチャでは、メモリはバスに接続され、複数の CPU によって共有されます。スレッドが NUMA CPU のメモリを割り当てる際には、ポリシーに従って割り当てられます。デフォルトでは、空きがない場合を除いて、スレッドのローカル CPU に接続されたメモリが割り当てられます。空きがない場合は、よりコストの高い空き CPU のメモリが使用されます。一度割り当てられたメモリは CPU 間で移動しません。割り当ては、親スレッド（最終的にはプロセスを開始したスレッド）から継承されたポリシーに従って実行されます。

コンピューターをマルチコアの均一なメモリアーキテクチャと見なす多くのデータベースでは、このシナリオの結果、初めの CPU がまずいっぱいになり、サブ CPU がその後にいっぱいになります。中核となるスレッドがメモリバッファの割り当てを担当する場合は、特にそうなります。これを解決するには、次のコマンドを実行して、`mongod` プロセスを開始するために使用されるメインスレッドの NUMA ポリシーを変更します。

```shell
numactl --interleaved=all <mongod> -f config
```

このポリシーでは、すべての CPU ノードでラウンドロビン方式でメモリが割り当てられるので、すべてのノードで配分が均等になります。CPU ハードウェアが複数あるシステムの場合のように、メモリに対する最も高速なアクセスが生成されるわけではありません。メモリ操作の約半分は速度が低下し、バスを経由して行われますが、`mongod` は NUMA を目的として最適な方法で記述されているわけではないので、これは合理的な妥協策になります。

### NUMA に関する問題 {#numa-issues}

`/etc/init.d` フォルダー以外の場所から `mongod` プロセスが開始された場合、適切な NUMA ポリシーで開始されなかった可能性があります。デフォルトポリシーによっては、問題が発生することがあります。その理由は、MongoDB 用の様々な Linux® パッケージマネージャーインストーラーが、`/etc/init.d` に設定ファイルと共にサービスをインストールし、それにより上記の手順が実行されるからです。アーカイブ（`.tar.gz`）から直接 MongoDB をインストールして実行する場合は、mongod を `numactl` プロセスで手動で実行する必要があります。

>[!NOTE]
>
>使用可能な NUMA ポリシーについて詳しくは、[numactl のドキュメント](https://linux.die.net/man/8/numactl)を参照してください。

MongoDB プロセスの動作は、個々の割り当てポリシーによって異なります。

```

```

* `-membind=<nodes>`
リストされているノードのみで割り当てを行います。mongod では、リストされているノードのメモリが割り当てられず、使用可能なメモリの一部が使用されない可能性があります。

* `-cpunodebind=<nodes>`
ノードのみで実行します。mongod は、指定されたノードのみで実行され、それらのノードで使用可能なメモリのみを使用します。

* `-physcpubind=<nodes>`
リストされている CPU（コア）のみで実行します。mongod は、リストされている CPU のみで実行され、それらの CPU で使用可能なメモリのみを使用します。

* `--localalloc`
常に現在のノードのメモリを割り当てますが、スレッドを実行しているすべてのノードを使用します。1 つのスレッドで割り当てが実行されている場合は、その CPU で使用可能なメモリのみが使用されます。

* `--preferred=<node>`
指定されたノードへの割り当てを優先しますが、優先されるノードがいっぱいである場合は他のノードにフォールバックします。ノードを定義するための相対注釈を使用できます。また、スレッドはすべてのノードで実行されます。

一部のポリシーでは、`mongod` プロセスに割り当てられるメモリが、使用可能なすべての RAM よりも少ない場合があります。MySQL とは異なり、MongoDB はオペレーティングシステムレベルのページングを積極的に回避します。そのため、使用可能であると思われるメモリよりも少ない量のメモリが `mongod` プロセスに割り当てられることがあります。

#### スワッピング {#swapping}

データベースはその性質上、大量のメモリを使用するので、オペレーティングシステムレベルのスワッピングを無効にする必要があります。MongoDB プロセスは、スワッピングしないように設計されています。

#### リモートファイルシステム {#remote-filesystems}

NFS などのリモートファイルシステムでは、非常に多くの遅延が発生します。そのため、MongoDB の内部データファイル（mongod プロセスデータベースファイル）にはお勧めしません。なお、Oak Blob の格納に必要な共有ファイルシステム（FileDataStore）の場合と混同しないでください。この場合は、NFS が推奨されます。

#### 先読み {#read-ahead}

ランダム読み取りを使用してページがページインされるときに、不要なブロックがディスクから読み取られないように、先読みを調整します。そうしないと、I/O 帯域幅が不必要に消費されることになります。

### Linux® に関する要件 {#linux-requirements}

#### カーネルの最小バージョン {#minimum-kernel-versions}

* `ext4` ファイルシステムの場合 **2.6.23**

* `xfs` ファイルシステムの場合 **2.6.25**

#### データベースディスクの推奨設定 {#recommended-settings-for-database-disks}

**atime の無効化**

データベースを格納するディスクについては、`atime` を無効にすることをお勧めします。

**NOOP ディスクスケジューラーの設定**

次の手順を実行します。

まず、次のコマンドを実行して、設定されている I/O スケジューラーを確認します。

```shell
cat /sys/block/sdg/queue/scheduler
```

応答が `noop` の場合は、これ以上何もする必要はありません。

設定されている I/O スケジューラーが NOOP でない場合は、次のコマンドを実行して変更できます。

```shell
echo noop > /sys/block/sdg/queue/scheduler
```

**先読み値の調整**

MongoDB データベースが実行されるディスクには、値を 32 にすることをお勧めします。この値は 16 KB になります。これを設定するには、次のコマンドを実行します。

```shell
sudo blockdev --setra <value> <device>
```

#### NTP を有効にする {#enable-ntp}

MongoDB データベースをホストしているマシンに NTP がインストールされ、実行されていることを確認します。例えば、CentOS マシンで yum パッケージマネージャーを使用してインストールできます。

```shell
sudo yum install ntp
```

NTP デーモンがインストールされ、正常に起動したら、ドリフトファイルでサーバーの時間オフセットを確認できます。

#### Transparent Huge Pages を無効にする {#disable-transparent-huge-pages}

Red Hat Linux では、Transparent Huge Pages（THP）と呼ばれるメモリ管理アルゴリズムが使用されます。このオペレーティングシステムをデータベースワークロードに使用している場合は、これを無効にすることをお勧めします。

無効にするには、次の手順に従います。

1. `/etc/grub.conf` ファイルを任意のテキストエディターで開きます。
1. grub.conf ファイルに次の行を追加します。

   ```xml
   transparent_hugepage=never
   ```

1. 最後に、次のコマンドを実行して、設定が反映されていることを確認します。

   ```shell
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   THP が無効になっている場合、上記のコマンドの出力は次のようになります。

   ```xml
   always madvise [never]
   ```

>[!NOTE]
>
>Transparent Huge Pages について詳しくは、こちらの[記事](https://access.redhat.com/solutions/46111)を参照してください。

#### NUMA の無効化 {#disable-numa}

NUMA が有効になっているほとんどのインストール環境では、NUMA が `/etc/init.d` フォルダーからサービスとして実行されると、MongoDB デーモンによって自動的に無効になります。

これに該当しない場合は、各プロセスレベルで NUMA を無効にできます。無効にするには、次のコマンドを実行します。

```shell
numactl --interleave=all <path_to_process>
```

`<path_to_process>` は、mongod プロセスへのパスです。

続いて、次のコマンドを実行してゾーンの再利用を無効にします。

```shell
echo 0 > /proc/sys/vm/zone_reclaim_mode
```

#### mongod プロセスの ulimit 設定の微調整 {#tweak-the-ulimit-settings-for-the-mongod-process}

Linux® では、`ulimit` コマンドを使用してリソースの割り当ての制限を設定できます。この設定は、ユーザーごとまたはプロセスごとに実行できます。

[MongoDB における ulimit の推奨設定](https://docs.mongodb.org/manual/reference/ulimit/#recommended-ulimit-settings)に従って、mongod プロセスの ulimit を設定することをお勧めします。

#### MongoDB の I/O パフォーマンスのテスト {#test-mongodb-i-o-performance}

MongoDB には、I/O パフォーマンスのテストを目的とした `mongoperf` というツールが用意されています。このツールを使用して、インフラストラクチャを構成しているすべての MongoDB インスタンスのパフォーマンスをテストすることをお勧めします。

`mongoperf` の使用方法について詳しくは、[MongoDB のドキュメント](https://docs.mongodb.org/manual/reference/program/mongoperf/)を参照してください。

>[!NOTE]
>
>`mongoperf` は、MongoDB が実行されているプラットフォームにおけるパフォーマンスの指標です。したがって、この結果が実稼働システムのパフォーマンスを決定すると捉えないようにしてください。
>
>`fio` Linux® ツールを使用して補完的なテストを実行すると、より正確なパフォーマンス結果を得ることができます。

**デプロイメントを構成している仮想マシンでの読み取りパフォーマンスのテスト**

ツールをインストールしたら、MongoDB データベースディレクトリに切り替えてテストを実行します。続いて、次の設定で `mongoperf` を実行して、最初のテストを開始します。

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true}" | mongoperf
```

すべての MongoDB インスタンスで、最大 1 秒あたり 2 ギガバイト（2 GB/秒）および 500,000 IOPS を 32 スレッドで実行しているのが望ましい結果です。

2 回目のテストを実行します。今回は `mmf:true` パラメーターを設定して、メモリマップファイルを使用します。

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true,mmf:true}" | mongoperf
```

2 回目のテストの結果は最初のテストよりもかなり高くなり、メモリ転送のパフォーマンスが良くなったことを示しています。

>[!NOTE]
>
>テストを実施するときは、オペレーティングシステムのモニタリングシステムで対象の仮想マシンの I/O 使用率の状況を確認してください。I/O 読み取りが 100 パーセントに満たない値を示している場合は、仮想マシンに問題がある可能性があります。

**プライマリ MongoDB インスタンスの書き込みパフォーマンステスト**

次に、同じ設定で MongoDB データベースディレクトリから `mongoperf` を実行して、プライマリ MongoDB インスタンスの I/O 書き込みパフォーマンスを確認します。

```shell
echo "{nThreads:32,fileSizeMB:1000,w:true}" | mongoperf
```

理想的な出力は 1 秒あたり 12 メガバイトで、スレッド数による変動がほとんどなく、約 3000 IOPS に達している必要があります。

## 仮想化環境に関する手順 {#steps-for-virtualised-environments}

### VMWare {#vmware}

WMWare ESX を使用して仮想化環境を管理およびデプロイしている場合は、MongoDB の操作に対応するように、必ず ESX コンソールから次の設定を実行してください。

1. メモリバルーンを無効にします。
1. MongoDB データベースをホストする仮想マシンにメモリを事前に割り当てて確保します。
1. Storage I/O Control を使用して、十分な I/O を `mongod` プロセスに割り当てます。
1. [CPU 予約](https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.vsphere.hostclient.doc/GUID-6C9023B2-3A8F-48EB-8A36-44E3D14958F6.html?hWord=N4IghgNiBc4RB7AxmALgUwAQGEAKBVTAJ3QGcEBXIpMkAXyA)を設定して、MongoDB をホストするマシンの CPU リソースを確保します。

1. 準仮想化 I/O ドライバーの使用を検討します。[ナレッジベースの記事](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&amp;cmd=displayKC&amp;externalId=1010398)を参照してください。

### Amazon Web Services {#amazon-web-services}

Amazon Web Services に MongoDB をセットアップする方法については、MongoDB web サイトの [AWS 統合の設定](https://docs.cloud.mongodb.com/tutorial/configure-aws-settings/)に関する記事を参照してください。

## デプロイ前に MongoDB をセキュリティで保護する {#securing-mongodb-before-deployment}

デプロイメント前にデータベースの設定を保護する方法についてのアドバイスは、[MongoDB の安全なデプロイメント](https://blogs.adobe.com/security/2015/07/securely-deploying-mongodb-3-0.html)に関する投稿を参照してください。

## Dispatcher {#dispatcher}

### Dispatcher のオペレーティングシステムの選択 {#choosing-the-operating-system-for-the-dispatcher}

MongoDB デプロイメントを適切に機能させるには、Dispatcher をホストするオペレーティングシステムで **Apache httpd** **バージョン 2.4 以降**&#x200B;を実行している必要があります。

また、セキュリティへの影響を最小化するために、ビルドで使用されるすべてのライブラリが最新であることを確認してください。

### Dispatcher 設定 {#dispatcher-configuration}

一般的な Dispatcher 設定では、1 つの AEM インスタンスの 10 倍から 20 倍のリクエストスループットが提供されます。

Dispatcher はステートレスなので、水平方向に簡単に拡大・縮小できます。一部のデプロイメントでは、作成者が特定のリソースにアクセスできないように制限する必要があります。作成者インスタンスでは Dispatcher を使用することをお勧めします。

Dispatcher を使用せずに AEM を実行する場合は、SSL 停止とロードバランシングを別のアプリケーションで実行する必要があります。セッションが作成された AEM インスタンスに対するアフィニティ（スティッキー接続と呼ばれる概念）を備えるために、この設定を行う必要があります。これにより、コンテンツを更新する際の待ち時間を最小限に抑えることができます。

設定方法について詳しくは、[Dispatcher のドキュメント](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=ja)を参照してください。

### その他の設定 {#additional-configuration}

#### スティッキー接続 {#sticky-connections}

スティッキー接続を使用すると、1 人のユーザーのパーソナライズされたページとセッションデータをすべて、AEM の同じインスタンスで作成できます。このデータはインスタンスに格納されるため、同じユーザーからの後続のリクエストは同じインスタンスに返されます。

AEM インスタンスにリクエストをルーティングするすべての内部レイヤーでスティッキー接続を有効にし、後続のリクエストが同じ AEM インスタンスに到達するようにしておくことをお勧めします。これにより、インスタンス間でコンテンツを更新する際に発生する長い待ち時間を最短化できます。

#### 長い有効期限 {#long-expires}

デフォルトでは、AEM Dispatcher から送信されるコンテンツには Last-Modified ヘッダーと Etag ヘッダーが含まれており、コンテンツの有効期限を示すものはありません。このフローにより、ユーザーインターフェイスで常に最新バージョンのリソースを取得できるようになります。また、ブラウザーで GET 操作が実行されて、リソースが変更されたかどうかが確認されることも意味します。その結果、ページの読み込みに応じて、HTTP 応答が 304（未変更）となる複数のリクエストが発生する可能性があります。リソースに有効期限がない場合、Expires ヘッダーを設定し、Last-Modified ヘッダーと ETag ヘッダーを削除すると、コンテンツがキャッシュされます。また、Expires ヘッダーの日付になるまで、それ以上の更新リクエストは行われません。

ただし、この方法を使用すると、Expires ヘッダーの有効期限が切れる前に、ブラウザーでリソースの有効期限が切れるようにする妥当な方法がなくなります。このワークフローの問題を軽減するには、クライアントライブラリに不変 URL を使用するように HtmlClientLibraryManager を設定することができます。

これらの URL が変更されることはありません。URL に含まれているリソースの本文が変更されると、その変更内容が URL に反映されて、ブラウザーから適切なバージョンのリソースが要求されるようになります。

デフォルトの設定では、HtmlClientLibraryManager にセレクターが追加されます。セレクターがある場合、セレクターはそのままの状態でリソースが Dispatcher にキャッシュされます。また、このセレクターを使用して、有効期限切れに関する正しい動作を保証することもできます。デフォルトのセレクターでは、`lc-.*?-lc` というパターンが使用されます。次の Apache httpd 設定ディレクティブでは、そのパターンに一致するすべてのリクエストが適切な有効期限で処理されます。

```xml
Header set Expires "Tue, 20 Jan 2037 04:20:42 GMT" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header set Cache-Control "public, no-transform, max-age=267840000" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset ETag "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Last-Modified "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Pragma "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
```

#### スニッフィングなし {#no-sniff}

content-type がないコンテンツが送信された場合、多くのブラウザーでは、コンテンツの最初の数バイトを読み取って、コンテンツのタイプを推測しようとします。この手法は「スニッフィング」と呼ばれます。リポジトリに書き込むことができるユーザーが、コンテンツタイプを指定せずに悪意のあるコンテンツをアップロードする可能性があるので、スニッフィングによってセキュリティ上の脆弱性が生じます。

そのため、Dispatcher で処理されるリソースに `no-sniff` ヘッダーを追加することをお勧めします。ただし、Dispatcher ではヘッダーはキャッシュされません。そのため、ローカルファイルシステムから提供されるコンテンツのコンテンツタイプは、元の AEM サーバーのオリジナルの content-type ヘッダーを使用するのではなく、コンテンツの拡張子で判別されることになります。

キャッシュされたリソースを web アプリケーションがファイルタイプなしで提供することがないとわかっている場合は、スニッフィングなしを有効にしても問題ありません。

スニッフィングなしは、次のようにして、包括的に有効にすることができます。

```xml
Header set X-Content-Type-Options "nosniff"
```

また、次のようにして、選択的に有効にすることもできます。

```xml
RewriteCond %{REQUEST_URI} \.(?:js|jsonp)$ [OR]
RewriteCond %{QUERY_STRING} (callback|jsonp|cb)=\w+
RewriteRule .* - [E=jsonp_request:1]
Header set X-Content-Type-Options "nosniff"  env=jsonp_request
Header setifempty Content-Type application/javascript env=jsonp_request
```

#### コンテンツセキュリティポリシー {#content-security-policy}

Dispatcher のデフォルト設定では、オープンなコンテンツセキュリティポリシー（CSP）が許可されます。これらの設定により、ブラウザーサンドボックスのデフォルトポリシーが適用されるすべてのドメインからページにリソースを読み込むことができます。

信頼できない外部サーバーや検証されていない外部サーバーから JavaScript エンジンにコードが読み込まれないようにするために、リソースの読み込み元を制限することをお勧めします。

CSP では、ポリシーを微調整できます。ただし、複雑なアプリケーションでは、ポリシーによる制限が厳しすぎると、ユーザーインターフェイスの一部が機能しなくなる可能性があるので、CSP ヘッダーを慎重に開発する必要があります。

>[!NOTE]
>
>この仕組みについて詳しくは、[コンテンツセキュリティポリシーに関する OWASP のページ](https://owasp.deteact.com/cheat/cheatsheets/Content_Security_Policy_Cheat_Sheet.html)を参照してください。

### サイジング {#sizing}

サイジングについて詳しくは、[ハードウェアのサイジングのガイドライン](/help/managing/hardware-sizing-guidelines.md)を参照してください。

### MongoDB のパフォーマンスの最適化 {#mongodb-performance-optimization}

MongoDB のパフォーマンスに関する一般的な情報については、[MongoDB のパフォーマンスの分析に関するページ](https://docs.mongodb.org/manual/administration/analyzing-mongodb-performance/)を参照してください。

## 既知の制限事項 {#known-limitations}

### 同時インストール {#concurrent-installations}

MongoMK では、1 つのデータベースで複数の AEM インスタンスを同時に使用することがサポートされていますが、同時インストールはサポートされていません。

この問題を回避するには、まず 1 つのメンバーでインストールを実行し、最初のインストールが完了した後で、他のメンバーを追加します。

### ページ名の長さ {#page-name-length}

AEM が MongoMK 永続性マネージャーのデプロイメントで実行されている場合、[ページ名は 150 文字に制限されます。](/help/sites-authoring/managing-pages.md)

>[!NOTE]
>
>MongoDB の既知の制限やしきい値を把握しておくために、[MongoDB ドキュメント](https://docs.mongodb.com/manual/reference/limits/)を参照してください。
