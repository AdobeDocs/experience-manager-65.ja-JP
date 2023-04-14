---
title: Adobe Experience Managerと MongoDB
description: MongoDB を使用したAdobe Experience Managerのデプロイメントを成功させるために必要なタスクと考慮事項について説明します。
uuid: 8028832d-10de-4811-a769-fab699c162ec
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: cd3b979f-53d4-4274-b4eb-a9533329192a
docset: aem65
exl-id: 70a39462-8584-4c76-a097-05ee436247b7
source-git-commit: af60428255fb883265ade7b2d9f363aacb84b9ad
workflow-type: tm+mt
source-wordcount: '6408'
ht-degree: 15%

---

# Adobe Experience Managerと MongoDB{#aem-with-mongodb}

この記事では、MongoDB を備えたAEM(Adobe Experience Manager) のデプロイを成功させるために必要な、タスクと考慮事項に関する知識の向上を目的としています。

デプロイメントに関する詳細については、 [デプロイと保守](/help/sites-deploying/deploy.md) の節を参照してください。

## MongoDB をAEMで使用する場合 {#when-to-use-mongodb-with-aem}

通常、MongoDB は、次の条件の 1 つを満たすAEMオーサーのデプロイメントをサポートするために使用されます。

* 1 日に 1,000 人を超えるユニークユーザー
* 100 人を超える同時ユーザー
* 大量のページ編集
* 大きなロールアウトまたはアクティベーション。

上記の条件は、オーサーインスタンスに対してのみ適用され、すべて TarMK ベースにする必要のあるパブリッシュインスタンスに対しては適用されません。 オーサーインスタンスは未認証のアクセスを許可しないので、ユーザー数は認証済みユーザーを指します。

条件が満たされない場合、可用性に対処するために TarMK のアクティブ/スタンバイデプロイメントをお勧めします。 一般に、MongoDB は、拡張要件が、単一のハードウェアアイテムで実現できる以上の条件を満たす場合に考慮する必要があります。

>[!NOTE]
>
>オーサーインスタンスのサイズ設定と同時ユーザーの定義に関する追加情報については、 [ハードウェアのサイズ設定のガイドライン](/help/managing/hardware-sizing-guidelines.md#authors-working-in-parallel).

### AEM向けの MongoDB の最小デプロイメント {#minimal-mongodb-deployment-for-aem}

以下は、MongoDB 上のAEMの最小限のデプロイメントです。 簡単にするために、SSL 終了と HTTP プロキシコンポーネントが一般化されました。 これは、1 つのプライマリと 2 つのセカンダリを含む単一の MongoDB レプリカセットで構成されています。

![chlimage_1-4](assets/chlimage_1-4.png)

最小限のデプロイメントには 3 つの `mongod` レプリカセットとして構成されたインスタンス。 1 つのインスタンスがプライマリに選択され、他のインスタンスがセカンダリに選択されます。選択はが管理します。 `mongod`. 各インスタンスにローカルディスクが接続されています。このため、クラスタは負荷をサポートでき、1 秒あたり 3,000 個を超える I/O 操作 (IOPS) を持つ 1 秒あたり 12 MB の最小スループットを推奨します。

AEM オーサーは `mongod` インスタンスに接続されます。各 AEM オーサーは 3 つの `mongod` インスタンスすべてに接続します。書き込みはプライマリに送信され、読み取りはどのインスタンスからも読み取ることができます。 トラフィックは、Dispatcher による読み込みに基づいて、アクティブなAEMオーサーインスタンスのいずれかに分散されます。 Oak データストアは、 `FileDataStore`、および MongoDB の監視は、デプロイメントの場所に応じて、MMS または MongoDB Ops Manager によって提供されます。 オペレーティングシステムレベルとログの監視は、Splunk や Ganglia などのサードパーティソリューションによって提供されます。

このデプロイメントでは、実装を成功させるには、すべてのコンポーネントが必要です。 見つからないコンポーネントは、実装が機能しないままです。

### オペレーティングシステム {#operating-systems}

AEM 6 でサポートされているオペレーティングシステムのリストについては、[技術要件のページ](/help/sites-deploying/technical-requirements.md)を参照してください。

### 環境 {#environments}

プロジェクトを実行する異なる技術チーム間で良好な通信が可能な場合、仮想化環境がサポートされます。 このサポートには、AEMを実行しているチーム、オペレーティングシステムを所有しているチーム、仮想化インフラストラクチャを管理しているチームが含まれます。

仮想化環境を管理するチームが管理する必要がある、MongoDB インスタンスの I/O 容量に関する特定の要件があります。 プロジェクトでAmazon Web Servicesなどのクラウドデプロイメントを使用する場合は、MongoDB インスタンスをサポートするために、十分な I/O 容量と一貫性を持つインスタンスをプロビジョニングする必要があります。 そうでない場合、MongoDB プロセスと Oak リポジトリは、信頼性が低く不安定に実行されます。

仮想化環境では、MongoDB のストレージエンジンが VMWare のリソース割り当てポリシーによって機能しなくなるように、MongoDB は特定の I/O および VM 設定を必要とします。 実装が成功すれば、様々なチーム間に障壁がなくなり、すべてが必要なパフォーマンスを提供するためにサインアップされます。

## ハードウェアに関する考慮事項 {#hardware-considerations}

### ストレージ {#storage}

MongoDB は、早期の水平スケーリングを必要とせずに、最高のパフォーマンスを得るために読み取りと書き込みのスループットを実現するために、通常、SSD と同等のパフォーマンスを持つ SSD ストレージまたはストレージが必要です。

### RAM {#ram}

MMAP ストレージエンジンを使用する MongoDB バージョン 2.6 および 3.0 では、データベースの作業セットとそのインデックスが RAM に適合している必要があります。

RAM が不足すると、パフォーマンスが大幅に低下します。 作業セットとデータベースのサイズは、アプリケーションに大きく依存します。 一部の予測は可能ですが、必要な RAM の量を判断する最も信頼性の高い方法は、AEMアプリケーションを構築し、負荷テストを行うことです。

負荷テストプロセスを支援するために、作業セットの合計データベースサイズに対する次の比率を想定できます。

* 1:10 （SSD ストレージ用）
* ハードディスクストレージの場合は 1:3

この比率は、SSD の導入時に 2 TB のデータベースに 200 GB の RAM が必要となることを意味します。

MongoDB 3.0 の WiredTiger ストレージエンジンにも同じ制限がありますが、作業セット、RAM、およびページの障害の間の相関関係はそれほど強くありません。 WiredTiger は、MMAP ストレージエンジンと同じ方法でメモリマッピングを使用しません。

>[!NOTE]
>
>Adobeは、MongoDB 3.0 を使用するAEM 6.1 のデプロイメントには、WiredTiger ストレージエンジンを使用することをお勧めします。

### データストア {#data-store}

MongoDB の作業セットの制限により、データストアは MongoDB とは独立した状態に維持することをお勧めします。 ほとんどの環境では、 `FileDataStore` すべてのAEMインスタンスで利用可能な NAS を使用する必要があります。 Amazon Web Services を使用する場合は、`S3 DataStore` もあります。何らかの理由で、データストアが MongoDB 内に保持され、データストアのサイズを合計データベースサイズに追加し、作業セットの計算を適切に調整する必要があります。 このサイズ設定は、ページ障害が発生しないパフォーマンスを維持するために、より多くの RAM をプロビジョニングすることを意味する場合があります。

## モニタリング {#monitoring}

プロジェクトを正しく実装するには、監視が不可欠です。 十分な知識があれば、監視を行わずにAEMを MongoDB 上で実行できます。 ただし、この知識は、通常、デプロイメントの各セクションに特化したエンジニアで見られます。

この専門知識には、通常、Apache Oak Core で作業する R&amp;D エンジニアと MongoDB スペシャリストが関与します。

すべてのレベルで監視をおこなわない場合、問題を診断するには、コードベースに関する詳細な知識が必要です。 監視を実施し、主要な統計に関する適切なガイダンスを提供することで、実装チームは異常値に適切に対応できます。

コマンドラインツールを使用してクラスタの動作のスナップショットを簡単に得ることは可能ですが、多くのホストでリアルタイムで実行することはほとんど不可能です。 コマンドラインツールでは、数分を超える履歴情報を提供することはほとんどなく、様々なタイプの指標を相互に関連付けることはできません。 `mongod` のバックグラウンド同期が短期間遅くなると、見かけ上は接続されていない仮想マシンからの共有ストレージリソースに対する I/O の待機や過剰な書き込みレベルの相関関係を見つけるために手動による多大な労力が必要になります。

### MongoDB Cloud Manager {#mongodb-cloud-manager}

MongoDB Cloud Manager は、MongoDB インスタンスの監視と管理を可能にする、MongoDB が提供する無料のサービスです。 MongoDB クラスターのパフォーマンスとヘルスをリアルタイムで確認できます。 インスタンスが Cloud Manager 監視サーバーに到達できる場合、クラウドと非公開でホストされるインスタンスの両方を管理します。

このサービスを使用するには、監視サーバーに接続する MongoDB インスタンスにエージェントがインストールされている必要があります。エージェントには次の 3 つのレベルがあります。

* MongoDB サーバー上のすべての処理を完全に自動化できる自動化エージェント
* `mongod` インスタンスを監視できる監視エージェント
* データのスケジュールバックアップを実行できるバックアップエージェント。

MongoDB クラスターのメンテナンスを自動化するために Cloud Manager を使用すると、多くの日常的なタスクが容易になりますが、必須ではなく、バックアップに Cloud Manager を使用する必要もありません。 ただし、監視する Cloud Manager を選択する場合は、監視が必要です。

MongoDB Cloud Manager について詳しくは、[MongoDB のドキュメント](https://docs.cloud.mongodb.com/)を参照してください。

### MongoDB Ops Manager {#mongodb-ops-manager}

MongoDB Ops Manager は、MongoDB Cloud Manager と同じソフトウェアです。 登録が完了すると、Ops Manager は、プライベートデータセンターや他のノート PC やデスクトップマシンにローカルでダウンロードしてインストールできます。 ローカルの MongoDB データベースを使用してデータを保存し、Cloud Manager と同じ方法で管理対象サーバーと通信します。 監視エージェントを禁止するセキュリティポリシーがある場合は、MongoDB Ops Manager を使用する必要があります。

### オペレーティングシステムの監視 {#operating-system-monitoring}

AEM MongoDB クラスターを実行するには、オペレーティングシステムレベルの監視が必要です。

Ganglia はこのようなシステムの良い例であり、CPU、負荷平均、空きディスク容量などの基本的なヘルス指標を超えて、必要な情報の範囲と詳細を示します。 問題を診断するには、エントロピープールレベル、CPU I/O 待機、FIN_WAIT2 状態のソケットなどの下位レベルの情報が必要です。

### ログの集計 {#log-aggregation}

複数のサーバのクラスタを使用する場合、本番システムでは中央ログの集約が必要です。 Splunk のようなソフトウェアは、ログの集計をサポートし、チームがログを手動で収集することなく、アプリケーションの動作パターンを分析できるようにします。

## チェックリスト {#checklists}

この節では、プロジェクトを実装する前に、AEMおよび MongoDB のデプロイメントが適切に設定されていることを確認するために必要な様々な手順について説明します。

### ネットワーク {#network}

1. まず、すべてのホストに DNS エントリがあることを確認します。
1. すべてのホストは、他のすべてのルーティング可能なホストからの DNS エントリで解決可能である必要があります
1. すべての MongoDB ホストは、同じクラスタ内の他のすべての MongoDB ホストからルーティング可能です
1. MongoDB ホストは、MongoDB Cloud Manager およびその他の監視サーバーにパケットをルーティングできます
1. AEMサーバは、すべての MongoDB サーバにパケットをルーティングできます
1. 任意のAEMサーバーと MongoDB サーバーとの間のパケット遅延は 2 ミリ秒未満で、パケット損失がなく、1 ミリ秒以下の標準配布が可能です。
1. AEMと MongoDB サーバー間のホップが 2 つ以下であることを確認します。
1. 2 台の MongoDB サーバー間のホップは 2 つまでです
1. 任意のコアサーバ (MongoDB、AEM、または任意の組み合わせ ) 間に OSI レベル 3 より高いルータは存在しません。
1. VLAN トランキングまたは任意の形式のネットワークトンネリングを使用する場合は、パケットレイテンシチェックに従う必要があります。

### AEM設定 {#aem-configuration}

#### ノードストアの設定 {#node-store-configuration}

AEMインスタンスは、MongoMK でAEMを使用するように設定する必要があります。 AEMでの MongoMK 実装の基礎は、ドキュメントノードストアです。

ノードストアの設定方法について詳しくは、 [AEMでのノードストアとデータストアの設定](/help/sites-deploying/data-store-config.md).

最小限の MongoDB デプロイメントに対するドキュメントノードストアの設定例を以下に示します。

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

* `mongodburi`
MongoDB サーバーAEMがに接続する必要があります。 既定のレプリカセットの既知のすべてのメンバに対して接続が行われます。 MongoDB Cloud Manager を使用すると、サーバーセキュリティが有効になります。 したがって、接続文字列には適切なユーザー名とパスワードを含める必要があります。 MongoDB の非エンタープライズバージョンでは、ユーザー名とパスワードの認証のみがサポートされます。 接続文字列の構文について詳しくは、 [ドキュメント](https://docs.mongodb.org/manual/reference/connection-string/).

* `db`データベースの名前。AEM のデフォルトは  
`aem-author` です。

* `customBlobStore`
デプロイメントでデータベースにバイナリが格納されている場合、バイナリは作業セットの一部となります。 そのため、MongoDB 内にバイナリを格納しないようにし、 
NAS 上の `FileSystem` データストア。

* `cache`
キャッシュサイズ (MB)。 このスペースは、 
`DocumentNodeStore` を使用して作成します。デフォルトは 256MB です。ただし、Oak の読み取りパフォーマンスは大きなキャッシュのメリットがあります。

* `blobCacheSize`
頻繁に使用される Blob は、データストアから再取得しなくて済むように、AEM にキャッシュできます。これは、特に MongoDB データベースに BLOB を保存する場合に、パフォーマンスに大きな影響を与えます。 すべてのファイル・システム・ベースのデータ・ストアは、オペレーティング・システム・レベルのディスク・キャッシュのメリットを受けます。

#### データストアの設定 {#data-store-configuration}

データストアは、しきい値より大きいサイズのファイルを保存するために使用します。 このしきい値の下では、ファイルはドキュメントノードストア内のプロパティとして保存されます。 `MongoBlobStore` を使用する場合、Blob を格納するための専用のコレクションが MongoDB に作成されます。このコレクションは、 `mongod` インスタンスを作成し、必要とする `mongod` パフォーマンスの問題を回避するために、より多くの RAM を使用できます。 そのため、推奨される設定は、 `MongoBlobStore` 実稼動デプロイメント用と使用 `FileDataStore` すべてのAEMインスタンス間で共有される NAS によってバックアップされます。 オペレーティングシステムレベルのキャッシュはファイルの管理に効率的なので、ディスク上のファイルの最小サイズはディスクのブロックサイズに近いサイズに設定する必要があります。 これにより、ファイルシステムが効率的に使用され、多くの小さなドキュメントが `mongod` インスタンス。

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
サイズ（バイト単位）。このサイズ以下のバイナリは、ドキュメントノードストアと共に保存されます。 BLOB の ID を保存するのではなく、バイナリのコンテンツが保存されます。 このサイズを超えるバイナリの場合、バイナリの ID は Document のプロパティとして nodes コレクションに格納されます。 また、バイナリの本文は 
ディスク上の `FileDataStore` に。一般的なファイルシステムのブロックサイズは 4,096 バイトです。

* `path`
データストアのルートのパスです。MongoMK デプロイメントの場合、このパスは、すべてのAEMインスタンスで使用可能な共有ファイルシステムである必要があります。 通常は、NAS(Network Attached Storage) サーバが使用されます。 Amazon Web Services などのクラウドデプロイメントの場合、 
`S3DataFileStore` も利用できます。

* `cacheSizeInMB`
バイナリキャッシュの合計サイズ（メガバイト単位）です。これは、以下のものより小さいバイナリをキャッシュするために使用されます： 
`maxCacheBinarySize` の設定値。

* `maxCachedBinarySize`
バイナリキャッシュにキャッシュされるバイナリの最大サイズ（バイト単位）です。ファイルシステムベースのデータストアを使用する場合、バイナリはオペレーティングシステムによって既にキャッシュされているので、データストアのキャッシュに大きな値を使用することはお勧めしません。

#### クエリヒントの無効化 {#disabling-the-query-hint}

すべてのクエリと共に送信されるクエリヒントを無効にすることをお勧めします。 `-Doak.mongo.disableIndexHint=true` AEMを起動したとき。 これにより、MongoDB は、内部統計に基づいて、使用する最も適切なインデックスに基づいて計算を行います。

クエリヒントが無効になっていない場合、インデックスのパフォーマンス調整はAEMのパフォーマンスに影響しません。

#### MongoMK の永続キャッシュの有効化 {#enable-persistent-cache-for-mongomk}

高い I/O 読み取りパフォーマンスを持つ環境の速度を最大化するために、MongoDB デプロイメントに対して永続的なキャッシュ設定を有効にすることをお勧めします。 詳しくは、 [Jackrabbit Oak ドキュメント](https://jackrabbit.apache.org/oak/docs/nodestore/persistent-cache.html).

## MongoDB オペレーティングシステムの最適化 {#mongodb-operating-system-optimizations}

### オペレーティングシステムのサポート {#operating-system-support}

MongoDB 2.6 は、RAM とディスク間のオペレーティングシステムレベル管理の一部の側面に敏感なメモリマップストレージエンジンを使用します。 MongoDB インスタンスのクエリと読み取りパフォーマンスは、ページフォルトと呼ばれる、低速な I/O 操作を回避または排除することに依存しています。 これらの問題は、 `mongod` 特にプロセス。 オペレーティングシステムレベルのページ障害と混同しないでください。

高速な操作を行うには、MongoDB データベースは既に RAM にあるデータにのみアクセスする必要があります。 アクセスする必要があるデータは、インデックスとデータで構成されます。 このインデックスとデータのコレクションを作業セットと呼びます。 作業セットが使用可能な RAM より大きい場合、MongoDB は、I/O コストが発生するディスクからそのデータをページに格納する必要があり、既にメモリ内にある他のデータを削除する必要があります。 削除によってデータがディスクから再読み込みされると、ページの障害が支配し、パフォーマンスが低下します。 作業セットが動的で変数の場合、操作をサポートするために、より多くのページフォルトが発生します。

MongoDB は、Linux®の各種フレーバー、Windows、macOSなど、複数のオペレーティングシステムで動作します。 詳しくは、 [https://docs.mongodb.com/manual/installation/#supported-platforms](https://docs.mongodb.com/manual/installation/#supported-platforms) を参照してください。 MongoDB は、お使いのオペレーティングシステムに応じて、オペレーティングシステムレベルの推奨事項が異なります。 次のドキュメントが記載されています： [https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration](https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration) 便宜上、ここに要約した

#### Linux® {#linux}

* 透明なハグページとデフラグをオフにします。 詳しくは、 [Transparent Huge Pages 設定](https://docs.mongodb.com/manual/tutorial/transparent-huge-pages/) を参照してください。
* [読み込み先の設定を調整する](https://docs.mongodb.com/manual/administration/production-notes/#readahead) を設定します。

   * MMAPv1 ストレージエンジンの場合、作業セットのサイズが使用可能な RAM より大きく、ドキュメントのアクセスパターンがランダムな場合は、読み上げを 32 または 16 に減らすことを検討してください。 様々な設定を評価し、常駐メモリを最大限にし、ページフォルトの数を減らす最適な値を見つけることができます。
   * WiredTiger ストレージエンジンの場合は、ストレージメディアのタイプ（回転、SSD など）に関係なく、readahead を 0 に設定します。 一般に、readahead 設定は、より高い readahead 値を使用する場合に測定可能で繰り返し可能で信頼性の高いメリットが得られる場合を除き、推奨されます。 [MongoDB Professional サポート](https://docs.mongodb.com/manual/administration/production-notes/#readahead) は、ゼロ以外の readahead 設定に関するアドバイスとガイダンスを提供できます。

* 仮想環境で RHEL 7/CentOS 7 を実行している場合は、Tuned ツールを無効にします。
* RHEL 7/CentOS 7 を仮想環境で実行する場合、調整されたツールは、パフォーマンススループットから派生したパフォーマンスプロファイルを自動的に呼び出し、readahead 設定を 4 MB に自動的に設定します。 この設定は、パフォーマンスに悪影響を与える可能性があります。
* SSD ドライブの noop または deadline ディスクスケジューラを使用します。
* ゲスト VM の仮想化ドライブに対して noop ディスクスケジューラを使用します。
* NUMA を無効にするか、設定します `vm.zone_reclaim_mode` を 0 に設定してを実行します。 [モンゴ](https://docs.mongodb.com/manual/administration/production-notes/#readahead) インターリービングノードを持つインスタンス 詳しくは、 [MongoDB と NUMA ハードウェア](https://docs.mongodb.com/manual/administration/production-notes/#readahead) を参照してください。

* 使用事例に合わせてハードウェアの上限値を調整します。 複数の [モンゴ](https://docs.mongodb.com/manual/reference/program/mongod/#bin.mongod) または [モンゴ](https://docs.mongodb.com/manual/reference/program/mongos/#bin.mongos) インスタンスが同じユーザーの下で実行されている場合は、それに応じて ulimit 値を調整します。 詳しくは、 [UNIX® ulimit 設定](https://docs.mongodb.com/manual/reference/ulimit/) を参照してください。

* 次に対して noatime を使用 [dbPath](https://docs.mongodb.com/manual/reference/configuration-options/#storage.dbPath) マウントポイント。
* デプロイメントに十分なファイルハンドル (fs.file-max)、カーネルの pid 制限 (kernel.pid_max)、プロセスごとの最大スレッド数 (kernel.threads-max) を設定します。 大規模なシステムでは、次の値が出発点として適しています。

   * fs.file-max 値：98000,
   * kernel.pid_max の値は64000,
   * andkernel.threads-max の値は64000です。

* システムにスワップ領域が設定されていることを確認します。 適切なサイズ設定について詳しくは、オペレーティングシステムのドキュメントを参照してください。
* システムのデフォルトの TCP キープアライブが正しく設定されていることを確認します。 値が 300 の場合は、多くの場合、レプリカセットとシャード化されたクラスタのパフォーマンスが向上します。 詳しくは、 [TCP キープアライブ時間は MongoDB デプロイメントに影響を与えますか？](https://docs.mongodb.com/manual/faq/diagnostics/#faq-keepalive) （よくある質問）を参照してください。

#### Windows {#windows}

* NTFS の「最終アクセス時刻」の更新を無効にすることを検討します。この設定は、Unix 系のシステムで atime を無効にする場合と似ています。

### WiredTiger {#wiredtiger}

MongoDB 3.2 以降、MongoDB のデフォルトのストレージエンジンは WiredTiger ストレージエンジンです。 このエンジンは、堅牢で拡張性の高い機能をいくつか提供し、あらゆる一般的なデータベースの負荷に対して非常に適しています。 次のセクションでは、これらの機能について説明します。

#### ドキュメントレベルの同時実行 {#document-level-concurrency}

WiredTiger は、書き込み操作にドキュメントレベルの同時実行制御を使用します。 その結果、複数のクライアントが 1 つのコレクションの異なるドキュメントを同時に変更できます。

ほとんどの読み取りおよび書き込み操作で、WiredTiger は楽観的な同時実行制御を使用します。 WiredTiger は、グローバル、データベース、コレクションレベルでのインテントロックのみを使用します。 ストレージエンジンが 2 つの操作間の競合を検出すると、書き込みの競合が発生し、MongoDB がその操作を透過的に再試行します。 一部のグローバル操作（通常、複数のデータベースに関する短時間のみ有効な操作）では、引き続きグローバルな「インスタンス全体」ロックが必要です。

コレクションの削除など、その他の操作では、排他的なデータベースロックが必要です。

#### スナップショットとチェックポイント {#snapshots-and-checkpoints}

WiredTiger は、MultiVersion Concurrency Control(MVCC) を使用します。 操作の開始時に、WiredTiger はトランザクションに対するデータのポイントインタイムスナップショットを提供します。 スナップショットは、メモリ内データの一貫した表示を示します。

WiredTiger は、ディスクに書き込む際、すべてのデータファイルでの整合性が保たれるように、スナップショットのすべてのデータをディスクに書き込みます。この[永続化](https://docs.mongodb.com/manual/reference/glossary/#term-durable)されたデータは、データファイル内のチェックポイントとして機能します。チェックポイントを使用すると、最後のチェックポイントに至るまで、および最後のチェックポイントを含めて、データファイルの整合性が確保されます。 つまり、チェックポイントは回復ポイントとして機能する場合があります。

MongoDB は、60 秒または 2 GB のジャーナルデータの間隔でチェックポイント（つまり、スナップショットデータをディスクに書き込む）を作成するように WiredTiger を設定します。

新しいチェックポイントの書き込み中、以前のチェックポイントは引き続き有効です。 したがって、新しいチェックポイントの書き込み中に MongoDB が終了したりエラーが発生した場合でも、再起動時に MongoDB は最後の有効なチェックポイントから回復できます。

新しいチェックポイントは、WiredTiger のメタデータテーブルが自動的に更新され、新しいチェックポイントを参照する際に、アクセス可能で永続的になります。 新しいチェックポイントにアクセスできるようになると、WiredTiger は古いチェックポイントからページを解放します。

WiredTiger を使用 ( [ジャーナル](https://docs.mongodb.com/manual/reference/glossary/#term-durable)を使用すると、MongoDB は最後のチェックポイントから回復できます。ただし、最後のチェックポイントの後に行った変更を復元するには、を使用してを実行します。 [ジャーナル](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal).

#### ジャーナル {#journal}

WiredTiger は、 [checkpoints](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-checkpoints) データの耐久性を確保する。

WiredTiger ジャーナルは、チェックポイント間のすべてのデータ変更を保持します。 チェックポイント間で MongoDB が終了した場合は、ジャーナルを使用して、最後のチェックポイント以降に変更されたすべてのデータを再生します。 MongoDB がジャーナルデータをディスクに書き込む頻度について詳しくは、 [ジャーナリングプロセス](https://docs.mongodb.com/manual/core/journaling/#journal-process).

WiredTiger ジャーナルは、 [素早い](https://docs.mongodb.com/manual/core/journaling/#journal-process) 圧縮ライブラリ。 別の圧縮アルゴリズムを指定する場合、または圧縮を使用しない場合は、 [storage.wiredTiger.engineConfig.journalCompressor](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.journalCompressor) 設定。

詳しくは、 [WiredTiger を使用したジャーナリング](https://docs.mongodb.com/manual/core/journaling/#journaling-wiredtiger).

>[!NOTE]
>
>WiredTiger の最小ログレコードサイズは 128 バイトです。 ログレコードが 128 バイト以下の場合、WiredTiger はそのレコードを圧縮しません。
>
>[storage.journal.enabled](https://docs.mongodb.com/manual/reference/configuration-options/#storage.journal.enabled) を false に設定すると、ジャーナル処理を無効にすることができ、ジャーナルを維持するためのオーバーヘッドを削減できます。
>
>の場合 [スタンドアロン](https://docs.mongodb.com/manual/reference/glossary/#term-standalone) インスタンスでは、ジャーナルを使用しない場合、チェックポイント間で MongoDB が予期せず終了すると、一部のデータ変更が失われます。 のメンバーの場合 [レプリカセット](https://docs.mongodb.com/manual/reference/glossary/#term-replica-set)を使用すると、レプリケーションプロセスで十分な耐久性が保証される場合があります。

#### 圧縮 {#compression}

WiredTiger を使用すると、MongoDB はすべてのコレクションとインデックスの圧縮をサポートします。 圧縮により、CPU の追加コストをかけてストレージの使用を最小限に抑えます。

デフォルトで、WiredTiger は、すべてのコレクションで [snappy](https://docs.mongodb.com/manual/reference/glossary/#term-snappy) 圧縮ライブラリを使用したブロック圧縮を、すべてのインデックスで[プレフィックス圧縮](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression)を使用します。

コレクションの場合、 [zlib](https://docs.mongodb.com/manual/reference/glossary/#term-zlib) はも利用できます。 別の圧縮アルゴリズムを指定する場合、または圧縮を使用しない場合は、 [storage.wiredTiger.collectionConfig.blockCompressor](https://docs.mongodb.com/manual/reference/glossary/#term-zlib) 設定。

インデックスで[プレフィックス圧縮](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression)を無効にするには、[storage.wiredTiger.indexConfig.prefixCompression](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.indexConfig.prefixCompression)設定を使用します。

また、圧縮設定は、コレクションおよびインデックスの作成時に、コレクションごとおよびインデックスごとに設定できます。 詳しくは、 [ストレージエンジンのオプションを指定](https://docs.mongodb.com/manual/reference/method/db.createCollection/#create-collection-storage-engine-options) および [db.collection.createIndex() storageEngine](https://docs.mongodb.com/manual/reference/method/db.collection.createIndex/#createindex-options) オプション。

ほとんどのワークロードでは、デフォルトの圧縮設定により、ストレージ効率と処理要件のバランスが取れます。

WiredTiger ジャーナルもデフォルトで圧縮されています。 ジャーナルの圧縮について詳しくは、 [ジャーナル](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal).

#### メモリ使用量 {#memory-use}

WiredTiger を使用する場合、MongoDB は WiredTiger の内部キャッシュとファイルシステムのキャッシュの両方を使用します。

3.4 以降、WiredTiger の内部キャッシュは、デフォルトで、次のいずれか大きい方を使用します。

* RAM の 50%から 1 GB を引いた、または
* 256 MB

既定では、WiredTiger はすべてのコレクションに対して Snappy ブロック圧縮を使用し、すべてのインデックスに対してプレフィックス圧縮を使用します。 圧縮のデフォルトはグローバルレベルで設定でき、コレクションおよびインデックスの作成時に、コレクションごとおよびインデックスごとに設定することもできます。

WiredTiger の内部キャッシュのデータには、ディスク上の形式とは異なる表現が使用されます。

* ファイル・システム・キャッシュ内のデータは、ディスク上のフォーマットと同じです。データ・ファイルの圧縮のメリットも含まれます。 ファイルシステムのキャッシュは、ディスクの I/O を減らすためにオペレーティングシステムによって使用されます。

WiredTiger の内部キャッシュに読み込まれたインデックスは、ディスク上の形式とは異なるデータ表現を持ちますが、インデックスのプレフィックス圧縮を利用して、RAM の使用量を減らすことができます。

インデックスプレフィックス圧縮は、インデックス付きのフィールドから共通のプレフィックスの重複を排除します。

WiredTiger の内部キャッシュ内の収集データは非圧縮で、ディスク上の形式とは異なる表現を使用します。 ブロック圧縮は、ディスク上のストレージを大幅に節約できますが、サーバがデータを操作するには、データを圧縮解除する必要があります。

MongoDB は、ファイルシステムのキャッシュを介して、WiredTiger のキャッシュや他のプロセスで使用されないすべての空きメモリを自動的に使用します。

WiredTiger の内部キャッシュのサイズを調整するには、 [storage.wiredTiger.engineConfig.cacheSizeGB](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.cacheSizeGB) および [—wiredTigerCacheSizeGB](https://docs.mongodb.com/manual/reference/program/mongod/#cmdoption-wiredtigercachesizegb). WiredTiger の内部キャッシュサイズをデフォルト値より大きくしないでください。

### NUMA {#numa}

NUMA(Non-Uniform Memory Access) を使用すると、カーネルはプロセッサーコアにメモリをマッピングする方法を管理できます。 このプロセスは、コアが必要なデータに確実にアクセスできるように、メモリアクセスを高速化しようと試みますが、NUMA は MMAP に干渉し、読み取りを予測できないので、追加の待ち時間が発生します。 その結果、NUMA は `mongod` すべての対応オペレーティングシステムで処理を実行します。

要するに、NUMA アーキテクチャのメモリは CPU に接続され、CPU はバスに接続されます。 SMP または UMA アーキテクチャでは、メモリはバスに接続され、CPU によって共有されます。 スレッドが NUMA CPU にメモリを割り当てると、ポリシーに従って割り当てられます。 デフォルトでは、スレッドのローカル CPU に接続されたメモリを割り当てます（空きがない場合を除く）。空き CPU のメモリをより高いコストで使用します。 割り当て後は、メモリは CPU 間を移動しません。 割り当ては、親スレッドから継承されたポリシーによって実行されます。最終的には、プロセスを開始したスレッドになります。

多くのデータベースでは、コンピュータをマルチコアの均一メモリアーキテクチャと見なす場合、このシナリオは、最初に CPU がフルになり、後でセカンダリ CPU が満杯になる原因となります。 特に、中央のスレッドがメモリバッファの割り当てを担当する場合には真です。 解決策は、NUMA ポリシーを変更し、 `mongod` 次のコマンドを実行してプロセスを実行します。

```shell
numactl --interleaved=all <mongod> -f config
```

このポリシーは、すべての CPU ノードに対してラウンドロビン方式でメモリを割り当て、すべてのノードに対して均等に分配します。 複数の CPU ハードウェアを搭載したシステムとは異なり、メモリに対する最高のパフォーマンスアクセスは生成されません。 メモリの動作の約半分が遅く、バスを経由しますが、 `mongod` は、ターゲット NUMA に最適な方法で書き込まれていないので、妥当な妥協点となります。

### NUMA に関する問題 {#numa-issues}

この `mongod` プロセスは `/etc/init.d` フォルダーに保存されている場合、正しい NUMA ポリシーで開始されていない可能性があります。 デフォルトポリシーによっては、問題が発生することがあります。これは、MongoDB 用の様々な Linux® Package Manager インストーラーが、 `/etc/init.d` 上記の手順を実行する アーカイブ ( `.tar.gz`) の場合は、 `numactl` プロセス。

>[!NOTE]
>
>使用可能な NUMA ポリシーについて詳しくは、[numactl のドキュメント](https://linux.die.net/man/8/numactl)を参照してください。

MongoDB プロセスの動作は、次のように、割り当てポリシーの違いによって異なります。

```

```

* `-membind=<nodes>`
リストされているノードのみで割り当てをおこないます。Mongod は、リストされたノードにメモリを割り当てず、使用可能なすべてのメモリを使用するわけではありません。

* `-cpunodebind=<nodes>`
ノードでのみ実行します。 Mongod は、指定されたノード上でのみ動作し、それらのノードで使用可能なメモリのみを使用します。

* `-physcpubind=<nodes>`
リストに表示されている CPU（コア）でのみ実行します。 Mongod は、リストされた CPU 上でのみ動作し、それらの CPU で使用可能なメモリのみを使用します。

* `--localalloc`
常に現在のノードのメモリを割り当てますが、スレッドを実行しているすべてのノードを使用します。1 つのスレッドが割り当てを実行した場合は、その CPU で使用可能なメモリのみが使用されます。

* `--preferred=<node>`
指定されたノードへの割り当てを優先しますが、優先されるノードがいっぱいである場合は他のノードにフォールバックします。ノードを定義する相対表記を使用できます。 また、スレッドはすべてのノードで実行されます。

一部のポリシーでは、`mongod` プロセスに割り当てられるメモリが、使用可能なすべての RAM よりも少ない場合があります。MySQL とは異なり、MongoDB はオペレーティングシステムレベルのページングを積極的に回避し、その結果、 `mongod` プロセスで使用可能なメモリが少なくなる場合があります。

#### スワップ {#swapping}

データベースのメモリを大量に消費する性質上、オペレーティングシステムレベルのスワップを無効にする必要があります。 MongoDB プロセスは、設計によるスワップを回避します。

#### リモートファイルシステム {#remote-filesystems}

NFS などのリモートファイルシステムでは、非常に多くの遅延が発生します。そのため、MongoDB の内部データファイル（mongod プロセスデータベースファイル）にはお勧めしません。NFS が推奨される Oak Blob(FileDataStore) のストレージに必要な共有ファイルシステムと混同しないでください。

#### 先読み {#read-ahead}

読み取りを先に調整して、ページがランダム読み取りを使用してページ化された場合に、不要なブロックがディスクから読み取られないようにします。 この結果、I/O 帯域幅が不要に消費されることを意味します。

### Linux®の要件 {#linux-requirements}

#### カーネルの最小バージョン {#minimum-kernel-versions}

* `ext4` ファイルシステムの場合 **2.6.23**

* `xfs` ファイルシステムの場合 **2.6.25**

#### データベースディスクの推奨設定 {#recommended-settings-for-database-disks}

**atime をオフにする**

を推奨します。 `atime` データベースを含むディスクの場合は、がオフになっています。

**NOOP ディスクスケジューラを設定する**

次の手順を実行します。

まず、次のコマンドを実行して、設定されている I/O スケジューラを確認します。

```shell
cat /sys/block/sdg/queue/scheduler
```

応答が `noop`ですから、これ以上何もする必要はありません。

設定されている I/O スケジューラーが NOOP でない場合は、次のコマンドを実行して変更できます。

```shell
echo noop > /sys/block/sdg/queue/scheduler
```

**先読み値を調整する**

MongoDB データベースが実行されるディスクには、値 32 を使用することをお勧めします。 この値は 16 KB になります。 次のコマンドを実行して設定できます。

```shell
sudo blockdev --setra <value> <device>
```

#### NTP を有効にする {#enable-ntp}

MongoDB データベースをホストするマシンに NTP がインストールされ、実行されていることを確認します。 例えば、CentOS マシンで yum Package Manager を使用してインストールできます。

```shell
sudo yum install ntp
```

NTP デーモンがインストールされ、正常に起動したら、drift ファイルでサーバの時間オフセットを確認できます。

#### 透明な巨大ページを無効にする {#disable-transparent-huge-pages}

Red Hat® Linux®は、Transparent Huge Pages(THP) と呼ばれるメモリ管理アルゴリズムを使用します。 データベースのワークロードにオペレーティングシステムを使用している場合は、無効にすることをお勧めします。

無効にするには、次の手順に従います。

1. `/etc/grub.conf` ファイルを任意のテキストエディターで開きます。
1. grub.conf ファイルに次の行を追加します。

   ```xml
   transparent_hugepage=never
   ```

1. 最後に、次のコマンドを実行して、設定が有効になったかどうかを確認します。

   ```shell
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   THP が無効の場合、上記のコマンドの出力は次のようになります。

   ```xml
   always madvise [never]
   ```

>[!NOTE]
>
>Transparent Huge Pages について詳しくは、こちらの[記事](https://access.redhat.com/solutions/46111)を参照してください。

#### NUMA の無効化 {#disable-numa}

NUMA が有効になっているほとんどのインストールでは、MongoDB デーモンは、 `/etc/init.d` フォルダー。

そうでない場合は、プロセスレベルで NUMA を無効にできます。 無効にするには、次のコマンドを実行します。

```shell
numactl --interleave=all <path_to_process>
```

`<path_to_process>` は、mongod プロセスへのパスです。

続いて、次のコマンドを実行してゾーンの再利用を無効にします。

```shell
echo 0 > /proc/sys/vm/zone_reclaim_mode
```

#### mongod プロセスの ulimit 設定の微調整 {#tweak-the-ulimit-settings-for-the-mongod-process}

Linux®では、 `ulimit` コマンドを使用します。 この設定は、ユーザーに対して実行することも、プロセスごとに実行することもできます。

mongod プロセスの ulimit は、 [MongoDB 推奨 ulimit 設定](https://docs.mongodb.org/manual/reference/ulimit/#recommended-ulimit-settings).

#### MongoDB I/O パフォーマンスのテスト {#test-mongodb-i-o-performance}

MongoDB には、I/O パフォーマンスのテストを目的とした `mongoperf` というツールが用意されています。このツールを使用して、インフラストラクチャを構成しているすべての MongoDB インスタンスのパフォーマンスをテストすることをお勧めします。

`mongoperf` の使用方法について詳しくは、[MongoDB のドキュメント](https://docs.mongodb.org/manual/reference/program/mongoperf/)を参照してください。

>[!NOTE]
>
>この `mongoperf` は、実行されているプラットフォーム上の MongoDB のパフォーマンスを示す指標です。 その結果は、実稼動システムのパフォーマンスに対して確定的な結果として扱われるべきではありません。
>
>より正確なパフォーマンス結果を得るには、 `fio` Linux®ツール。

**デプロイメントを構成している仮想マシンでの読み取りパフォーマンスのテスト**

ツールをインストールしたら、MongoDB データベースディレクトリに切り替えてテストを実行します。 続いて、次の設定で `mongoperf` を実行して、最初のテストを開始します。

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
テストを実施するときは、オペレーティングシステムのモニタリングシステムで対象の仮想マシンの I/O 使用率の状況を確認してください。I/O 読み取りが 100 パーセントに満たない値を示している場合は、仮想マシンに問題がある可能性があります。

**プライマリ MongoDB インスタンスの書き込みパフォーマンステスト**

次に、同じ設定で MongoDB データベースディレクトリから `mongoperf` を実行して、プライマリ MongoDB インスタンスの I/O 書き込みパフォーマンスを確認します。

```shell
echo "{nThreads:32,fileSizeMB:1000,w:true}" | mongoperf
```

必要な出力は、1 秒あたり 12 メガバイトで、約 3,000 IOPS に達し、スレッド数の差はほとんどありません。

## 仮想化環境の手順 {#steps-for-virtualised-environments}

### VMWare {#vmware}

WMWare ESX を使用して仮想化環境を管理および展開する場合は、MongoDB の操作に対応するために、ESX コンソールから次の設定を実行してください。

1. メモリバルーンを無効にします。
1. MongoDB データベースをホストする仮想マシンのメモリを事前に割り当てて予約する
1. Storage I/O Control を使用して、十分な I/O を `mongod` プロセスに割り当てます。
1. [CPU 予約](https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.vsphere.hostclient.doc/GUID-6C9023B2-3A8F-48EB-8A36-44E3D14958F6.html?hWord=N4IghgNiBc4RB7AxmALgUwAQGEAKBVTAJ3QGcEBXIpMkAXyA)を設定して、MongoDB をホストするマシンの CPU リソースを確保します。

1. 準仮想化 I/O ドライバーの使用を検討します。詳しくは、 [ナレッジベース記事](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&amp;cmd=displayKC&amp;externalId=1010398).

### Amazon Web Services {#amazon-web-services}

Amazon Web Services に MongoDB をセットアップする方法については、MongoDB web サイトの [AWS 統合の設定](https://docs.cloud.mongodb.com/tutorial/configure-aws-settings/)に関する記事を参照してください。

## デプロイ前に MongoDB をセキュリティで保護する {#securing-mongodb-before-deployment}

次の投稿を参照： [MongoDB の安全なデプロイ](https://blogs.adobe.com/security/2015/07/securely-deploying-mongodb-3-0.html) を参照してください。

## Dispatcher {#dispatcher}

### Dispatcher 用のオペレーティングシステムの選択 {#choosing-the-operating-system-for-the-dispatcher}

MongoDB デプロイメントを適切に機能させるには、Dispatcher をホストするオペレーティングシステムが実行されている必要があります **Apache httpd** **バージョン 2.4 以降。**

また、セキュリティ上の影響を最小限に抑えるために、ビルドで使用されるすべてのライブラリが最新であることを確認してください。

### Dispatcher 設定 {#dispatcher-configuration}

一般的な Dispatcher 設定は、1 つのAEMインスタンスの要求スループットの 10～20 倍の値を提供します。

Dispatcher はステートレスなので、水平方向に簡単に拡大できます。 一部のデプロイメントでは、作成者が特定のリソースにアクセスできるように制限する必要があります。 オーサーインスタンスで Dispatcher を使用することをお勧めします。

AEMを Dispatcher なしで実行する場合は、SSL を終了し、別のアプリケーションでロードバランシングを実行する必要があります。 セッションは、作成先のAEMインスタンス（スティッキー接続と呼ばれる概念）に対するアフィニティを持つ必要があるので、これが必要です。 その理由は、コンテンツの更新の待ち時間が最小限に抑えられるようにするためです。

設定方法について詳しくは、[Dispatcher のドキュメント](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=ja)を参照してください。

### 追加設定 {#additional-configuration}

#### スティッキー接続 {#sticky-connections}

スティッキー接続により、1 人のユーザーのパーソナライズされたページとセッションデータを、すべてAEMの同じインスタンスで構成することができます。 このデータはインスタンスに保存されるので、以降の同じユーザーからの要求は同じインスタンスに戻ります。

すべての内部レイヤーでスティッキー接続を有効にして、AEMインスタンスにリクエストをルーティングし、以降のリクエストが同じAEMインスタンスに到達するようにすることをお勧めします。 これにより、インスタンス間でコンテンツが更新された場合に目に見える遅延を最小限に抑えることができます。

#### 長い有効期限 {#long-expires}

デフォルトでは、AEM Dispatcher から送信されるコンテンツには、 Last-Modified ヘッダーと Etag ヘッダーがあり、コンテンツの有効期限を示すものはありません。 このフローにより、ユーザーインターフェイスは常にリソースの最新バージョンを取得します。 また、ブラウザーは、リソースが変更されたかどうかを確認するGET操作を実行します。 その結果、ページの読み込みに応じて、HTTP 応答が 304（未変更）の複数のリクエストが発生する場合があります。 期限切れにならないリソースの場合、 Expires ヘッダーを設定し、 Last-Modified ヘッダーと ETag ヘッダーを削除すると、コンテンツがキャッシュされます。 また、 Expires ヘッダーの日付を満たすまで、それ以上の更新リクエストはおこなわれません。

ただし、この方法を使用すると、Expires ヘッダーの有効期限が切れる前にブラウザーでリソースの有効期限が切れる妥当な方法がなくなります。 このワークフローを軽減するために、クライアントライブラリに不変 URL を使用するように HtmlClientLibraryManager を設定できます。

これらの URL は必ず変更されません。 URL に含まれるリソースの本文が変更されると、変更内容が URL に反映され、ブラウザーで正しいバージョンのリソースがリクエストされるようになります。

デフォルトの設定では、HtmlClientLibraryManager にセレクターが追加されます。 セレクターの場合、リソースは Dispatcher にキャッシュされ、セレクターはそのまま残ります。 また、このセレクターを使用して、正しい有効期限動作を確実にすることもできます。 デフォルトのセレクターでは、`lc-.*?-lc` というパターンが使用されます。次の Apache httpd 設定ディレクティブでは、そのパターンに一致するすべての要求が適切な有効期限で提供されます。

```xml
Header set Expires "Tue, 20 Jan 2037 04:20:42 GMT" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header set Cache-Control "public, no-transform, max-age=267840000" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset ETag "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Last-Modified "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Pragma "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
```

#### スニフなし {#no-sniff}

content-type を指定せずにコンテンツを送信する場合、多くのブラウザーでは、コンテンツの最初の数バイトを読み取ることで、コンテンツのタイプを推測しようとします。 この方法は「スニフィング」と呼ばれます。 スニフィングを行うと、リポジトリに書き込むことのできるユーザーが、コンテンツタイプのない悪意のあるコンテンツをアップロードする可能性があるので、セキュリティの脆弱性が生じます。

このため、 `no-sniff` ヘッダーから Dispatcher が提供するリソースへ。 ただし、Dispatcher はヘッダーをキャッシュしません。 したがって、ローカルファイルシステムから提供されるコンテンツのコンテンツタイプは、元のAEMサーバーの元の content-type ヘッダーを使用するのではなく、拡張子によって決まるという意味です。

Web アプリケーションがファイルタイプなしでキャッシュされたリソースを提供しないことがわかっている場合は、スニフを安全に有効にできません。

スニフなし (No Sniff) は、次のように含めて有効にできます。

```xml
Header set X-Content-Type-Options "nosniff"
```

また、次のように選択的に有効にすることもできます。

```xml
RewriteCond %{REQUEST_URI} \.(?:js|jsonp)$ [OR]
RewriteCond %{QUERY_STRING} (callback|jsonp|cb)=\w+
RewriteRule .* - [E=jsonp_request:1]
Header set X-Content-Type-Options "nosniff"  env=jsonp_request
Header setifempty Content-Type application/javascript env=jsonp_request
```

#### コンテンツセキュリティポリシー {#content-security-policy}

デフォルトの Dispatcher 設定では、CSP とも呼ばれる、開いたコンテンツセキュリティポリシーを許可します。 これらの設定を使用すると、ページはブラウザーサンドボックスのデフォルトポリシーに従うすべてのドメインからリソースを読み込むことができます。

信頼できない外部サーバーや検証されていない外部サーバーから JavaScript エンジンにコードが読み込まれるのを防ぐには、リソースの読み込み元を制限することをお勧めします。

CSP を使用すると、ポリシーを微調整できます。 ただし、複雑なアプリケーションでは、CSP ヘッダーを慎重に開発する必要があります。制限が厳しすぎると、ユーザーインターフェイスの一部が壊れる可能性があるので、このヘッダーを作成する必要があります。

>[!NOTE]
この機能について詳しくは、 [コンテンツセキュリティポリシーの OWASP ページ](https://owasp.deteact.com/cheat/cheatsheets/Content_Security_Policy_Cheat_Sheet.html).

### サイズ調整 {#sizing}

サイズ設定について詳しくは、 [ハードウェアのサイズ設定のガイドライン](/help/managing/hardware-sizing-guidelines.md).

### MongoDB パフォーマンスの最適化 {#mongodb-performance-optimization}

MongoDB のパフォーマンスに関する一般的な情報については、 [MongoDB のパフォーマンスの分析](https://docs.mongodb.org/manual/administration/analyzing-mongodb-performance/).

## 既知の制限事項 {#known-limitations}

### 同時インストール {#concurrent-installations}

単一のデータベースを持つ複数のAEMインスタンスの同時使用は MongoMK でサポートされますが、同時インストールはサポートされません。

この問題を回避するには、まず 1 人のメンバーでインストールを実行し、最初のインストールが完了した後に他のメンバーを追加します。

### ページ名の長さ {#page-name-length}

AEM が MongoMK 永続性マネージャーのデプロイメントで実行されている場合、[ページ名は 150 文字に制限されます。](/help/sites-authoring/managing-pages.md)

>[!NOTE]
詳しくは、 [MongoDB ドキュメント](https://docs.mongodb.com/manual/reference/limits/) そのため、MongoDB の既知の制限としきい値について把握することができます。
