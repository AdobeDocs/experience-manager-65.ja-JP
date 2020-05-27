---
title: Performance tuning for [!DNL Adobe Experience Manager Assets].
description: 構成、ハードウェア、ソフトウェア、ネットワーク・コンポーネントの変更に [!DNL Experience Manager] 関する提案とガイダンス。ボトルネックを解消し、パフォーマンスを最適化 [!DNL Experience Manager Assets]。
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '2723'
ht-degree: 53%

---


<!-- TBD: Get reviewed by engineering. -->

# [!DNL Adobe Experience Manager Assets] 性能調整ガイド {#assets-performance-tuning-guide}

An [!DNL Experience Manager Assets] setup contains a number of hardware, software, and network components. 導入のシナリオによっては、パフォーマンス上のボトルネックを排除するために、ハードウェア、ソフトウェアおよびネットワークコンポーネントに対して特殊な設定変更が必要になる場合があります。

In addition, identifying and adhering to certain hardware and software optimization guidelines helps build a sound foundation that enables your [!DNL Experience Manager Assets] deployment to meet expectations around performance, scalability, and reliability.

Poor performance in [!DNL Experience Manager Assets] can impact user experience around interactive performance, asset processing, download speed, and other areas.

パフォーマンスの最適化は、すべてのプロジェクトでターゲット指標を確立する前に実行する、基本的なタスクです。

ユーザーに影響を及ぼす前にパフォーマンス上の問題を検出して修正する必要がある主な領域は次のとおりです。

## プラットフォーム {#platform}

Experience Managerは様々なプラットフォームでサポートされていますが、LinuxおよびWindowsでのネイティブツールのサポートが最も多く行われ、パフォーマンスと導入の容易さの最適化に貢献しています。 Ideally, you should deploy a 64-bit operating system to meet the high memory requirements of an [!DNL Experience Manager Assets] deployment. Experience Manager導入の場合と同様、TarMKは可能な限り実装する必要があります。 TarMK は単一のオーサーインスタンスを超えて拡張できませんが、パフォーマンスは MongoMK よりも優れています。You can add TarMK offload instances to increase the workflow processing power of your [!DNL Experience Manager Assets] deployment.

### 一時フォルダー {#temp-folder}

アセットのアップロード時間を改善するには、Javaの一時ディレクトリに高いパフォーマンスのストレージを使用します。 Linux および Windows の場合は、RAM ドライブまたは SSD を使用できます。クラウドベースの環境では、同等の高速ストレージタイプを使用できます。For example in Amazon EC2, an [ephemeral drive](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html) drive can be used for the temporary folder.

サーバーに十分なメモリがあるという前提で、RAM ドライブを設定します。Linux の場合、8GB RAM ドライブを作成するには、次のコマンドを実行します。

```shell
mkfs -q /dev/ram1 800000
 mkdir -p /mnt/aem-tmp
 mount /dev/ram1 /mnt/aem-tmp
 df -H | grep aem-tmp
```

Windows OSでは、サードパーティ製のドライバを使用してRAMドライブを作成するか、SSDなどの高パフォーマンスストレージを使用します。

Once the high performance temporary volume is ready, set the JVM parameter `-Djava.io.tmpdir`. For example, you could add the JVM parameter below to the `CQ_JVM_OPTS` variable in the `bin/start` script of [!DNLExperience Manager]:

`-Djava.io.tmpdir=/mnt/aem-tmp`

## Java の設定 {#java-configuration}

### Java バージョン {#java-version}

最適なパフォーマンスを得るた [!DNL Experience Manager Assets] めに、Java 8にデプロイすることをお勧めします。

>[!NOTE]
>
>Oracleは、2015年4月にJava 7のアップデートのリリースを停止しました。

### JVM パラメーター {#jvm-parameters}

次のJVMパラメーターを設定します。

* `-XX:+UseConcMarkSweepGC`
* `-Doak.queryLimitInMemory`=500000
* `-Doak.queryLimitReads`=100000
* `-Dupdate.limit`=250000
* `-Doak.fastQuerySize`=true

## データストアとメモリの設定 {#data-store-and-memory-configuration}

### ファイルデータストアの設定 {#file-data-store-configuration}

Separating the data store from the segment store is recommended for all [!DNL Experience Manager Assets] users. また、`maxCachedBinarySize` パラメーターと `cacheSizeInMB` パラメーターを設定することでパフォーマンスを最大化するのに役立ちます。キャッシュに含めることができるように、`maxCachedBinarySize` を最小のファイルサイズに設定します。`cacheSizeInMB` 内のデータストアで使用するインメモリキャッシュのサイズを指定します。この値は合計ヒープサイズの 2～10％に設定することをお勧めします。ただし、負荷テストやパフォーマンステストが理想的な設定を決定するのに役立ちます。

### バッファーされる画像キャッシュの最大サイズの設定 {#configure-the-maximum-size-of-the-buffered-image-cache}

When uploading large amounts of assets to [!DNLAdobe Experience Manager], to allow for unexpected spikes in memory consumption and to prevent JVM fails with OutOfMemoryErrors, reduce the configured maximum size of the buffered image cache. 例えば、最大ヒープ（-`Xmx` パラメーター）が 5 GB のシステムで、Oak BlobCache が 1 GB、文書キャッシュが 2 GB に設定されているとします。このときに、バッファーされるキャッシュが最大 1.25 GB のメモリを使用した場合、予期しないスパイクに使用できるメモリは 0.75 GB のみとなります。

バッファーされるキャッシュサイズは OSGi Web コンソールで設定します。`https://host:port/system/console/configMgr/com.day.cq.dam.core.impl.cache.CQBufferedImageCache` で、プロパティ `cq.dam.image.cache.max.memory` をバイト単位で指定します。例えば、1073741824 は 1 GB です（1024 x 1024 x 1024 = 1 GB）。

From Experience Manager 6.1 SP1, if you&#39;re using a `sling:osgiConfig` node for configuring this property, make sure to set the data type to Long. 詳しくは、[CQBufferedImageCache がアセットのアップロード中にヒープを消費する](https://helpx.adobe.com/jp/experience-manager/kb/cqbufferedimagecache-consumes-heap-during-asset-uploads.html)を参照してください。

### 共有データストア {#shared-data-stores}

S3 または共有ファイルデータストアの実装は、ディスク領域の節約と大規模な実装におけるネットワークスループットの向上に役立ちます。For more information on the pros and cons of using a shared datastore, see [Assets sizing guide](/help/assets/assets-sizing-guide.md).

### S3 データストア {#s-data-store}

次の S3 データストアの設定（`org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.cfg`）は、アドビが 12.8 TB のバイナリラージオブジェクト（BLOB）を既存のファイルデータストアから顧客サイトの S3 データストアに抽出するのに役立ちました。

```conf
accessKey=<snip>
 secretKey=<snip>
 s3Bucket=<snip>
 s3Region=us-standard
 s3EndPoint=<a href="https://s3.amazonaws.com/">s3.amazonaws.com</a>
 connectionTimeout=120000
 socketTimeout=120000
 maxConnections=80
 writeThreads=60
 concurrentUploadsThreads=30
 asyncUploadLimit=30
 maxErrorRetry=1000
 path=/opt/author/crx-quickstart/repository/datastore
 s3RenameKeys=false
 s3Encryption=SSE_S3
 proactiveCaching=true
 uploadRetries=1000
 migrateFailuresCount=400
```

## ネットワークの最適化 {#network-optimization}

多くの企業には HTTP トラフィックをスニッフィングするファイアウォールがあり、ファイルのアップロードに干渉しファイルを破損するので、HTTPS を有効にすることをお勧めします。サイズの大きなファイルのアップロードについては、Wi-Fi ネットワークでは簡単に飽和するおそれがあるので、必ず有線でネットワークに接続してください。For guidelines on identifying network bottlenecks, see [Assets sizing guide](/help/assets/assets-sizing-guide.md). To assess network performance by analyzing network topology, see [Assets network considerations](/help/assets/assets-network-considerations.md).

Primarily, your network optimization strategy depends upon the amount of bandwidth available and the load on your [!DNLExperience Manager] instance. ファイアウォールやプロキシなどの一般的な設定オプションは、ネットワークのパフォーマンスの改善に役立ちます。留意点は次のとおりです。

* インスタンスのタイプ（小、モデレート、大）に応じて、Experience Managerインスタンスに十分なネットワーク帯域幅があることを確認します。 Adequate bandwidth allocation is especially important if [!DNLExperience Manager] is hosted on AWS.
* If your [!DNLExperience Manager] instance is hosted on AWS, you can benefit by having a versatile scaling policy. 高い負荷が予想される場合は、インスタンスのサイズを大きくします。負荷が標準的または低い場合は、インスタンスのサイズを小さくします。
* HTTPS：ユーザーの多くは HTTP トラフィックをスニッフィングするファイアウォールを装備しており、ファイルのアップロード操作に干渉しファイルを破損することもあります。
* サイズの大きなファイルのアップロード：必ず有線でネットワークに接続してください（Wi-Fi 接続は簡単に飽和するおそれがあります）。

## ワークフロー {#workflows}

### 一時的なワークフロー {#transient-workflows}

Wherever possible, set the [!UICONTROL DAM Update Asset] workflow to Transient. この設定にすると、ワークフローが通常のトラッキングやアーカイブ処理をパススルーする必要がなくなるので、ワークフローの処理に必要なオーバーヘッドが大幅に削減されます。

1. Experience Manager `/miscadmin` の [!DNLEインスタンス()に移動]`https://[aem_server]:[port]/miscadmin`します。

1. **[!UICONTROL ツール]** / **[!UICONTROL ワークフロー]** / **[!UICONTROL モデル/]****** damを展開します。

1. Open **[!UICONTROL DAM Update Asset]**. フローティングツールパネルで、「**[!UICONTROL ページ]**」タブに切り替えて「**[!UICONTROL ページプロパティ]**」をクリックします。

1. Select **[!UICONTROL Transient Workflow]** and click **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >一部の機能は一時的なワークフローをサポートしません。If your [!DNL Assets] deployment requires these features, do not configure transient workflows.

In cases where transient workflows cannot be used, run workflow purging regularly to delete archived [!UICONTROL DAM Update Asset] workflows to ensure system performance does not degrade.

通常、パージワークフローは週単位で実行します。 ただし、大規模なアセット取り込みの際など、リソースを大量に消費するシナリオでは、より頻繁にアセットを実行できます。

ワークフローのパージを設定するには、OSGi コンソールで新しい Adobe Granite のワークフローのパージ設定を追加します。次に、ワークフローを週次メンテナンスウィンドウの一部としてスケジュールを設定します。

パージの実行時間が長すぎる場合、タイムアウトします。このため、ワークフローの数が多すぎることが原因でパージワークフローが終わらない状況を避けるために、パージジョブが確実に終わるようにする必要があります。

For example, after executing numerous non-transient workflows (that creates workflow instance nodes), you can execute [ACS AEM Commons Workflow Remover](https://adobe-consulting-services.github.io/acs-aem-commons/features/workflow-remover.html) on an ad-hoc basis. これにより、冗長および完了したワークフローのインスタンスが即座に削除されるので、Adobe Granite のワークフローのパージスケジューラーが実行されるのを待つ必要がありません。

### 並列ジョブの最大数 {#maximum-parallel-jobs}

By default, [!DNLExperience Manager] runs a maximum number of parallel jobs equal to the number of processors on the server. The problem with this setting is that during periods of heavy load, all of the processors are occupied by [!UICONTROL DAM Update Asset] workflows, slowing down UI responsiveness and preventing [!DNLExperience Manager] from running other processes that safeguard server performance and stability. 次の手順を実行して、この値をサーバーで使用できるプロセッサーの半分の値にすることをお勧めします。

1. Experience Manager [!DNLEAuthorで、にアクセス]`https://[aem_server]:[port]/system/console/slingevent`します。

1. Click **[!UICONTROL Edit]** on each workflow queue that is relevant to your implementation, for example **[!UICONTROL Granite Transient Workflow Queue]**.

1. Update the value of **[!UICONTROL Maximum Parallel Jobs]** and click **[!UICONTROL Save]**.

まずは、キューを使用できるプロセッサーの半分に設定してください。ただし、場合によっては最大のスループットを得るためにこの値をお使いの環境に合わせて増減させる必要があります。一時的および一時的でないワークフローには別個のキューが用意されているほか、外部ワークフローなどその他の処理も存在します。プロセッサーの 50％に設定された複数のキューが同時にアクティブになると、システムはすぐにオーバーロードします。頻繁に使用されるキューは、ユーザーの実装により大きく異なります。このため、サーバーの安定性を損なうことなく効率を最大化するには、これらを慎重に設定する必要が生じる場合があります。

### DAM アセットの更新設定 {#dam-update-asset-configuration}

[!UICONTROL DAM Update Asset] Workflowには、Scene7 PTIFFの生成や [!DNL Adobe InDesign Server] 統合など、タスクに対して設定されたすべての手順が含まれます。 ただし、大多数のユーザーにとってこれらの手順のうちのいくつかは不要です。Adobe recommends you create a custom copy of the [!UICONTROL DAM Update Asset] workflow model, and remove any unnecessary steps. In this case, update the launchers for [!UICONTROL DAM Update Asset] to point to the new model.

Running the [!UICONTROL DAM Update Asset] workflow intensively can sharply increase the size of your file datatastore. アドビが実施した実験の結果によると、8 時間以内に約 5,500 のワークフローを実行した場合、データストアのサイズが約 400 GB 増加する可能性があります。

これは一時的な増加であり、データストアのガベージコレクションタスクを実行すると、データストアは元のサイズに戻ります。

通常、データストアのガベージコレクションタスクは、スケジュールされた他のメンテナンスタスクと共に毎週実行されます。

If you have a limited disk space and run [!UICONTROL DAM Update Asset] workflows intensively, consider scheduling the garbage collection task more frequently.

#### 実行時のレンディションの生成 {#runtime-rendition-generation}

お客様は Web サイトやビジネスパートナーへの配布に様々なサイズや形式の画像を使用します。各レンディションによりリポジトリ内のアセットの足跡が増加するので、この機能は適切なタイミングで使用することをお勧めします。画像の処理と保存に必要なリソースを減らすために、これらの画像を取り込み中にではなく実行時にレンディションとして生成できます。

多くの Sites のお客様はリクエストされた時点で画像のサイズを変更および切り抜く画像サーブレットを実装しています。これにより、パブリッシュインスタンスにさらに負荷がかけられます。ただし、これらの画像をキャッシュできる限り、問題を減らすことができます。

もう 1 つの方法では、Scene7 テクノロジーを使用して画像の操作をすべて引き渡します。Additionally, you can deploy Brand Portal that not only takes over rendition generation responsibilities from the [!DNLExperience Manager] infrastructure, but also the entire publish tier.

#### ImageMagick {#imagemagick}

If you customize the [!UICONTROL DAM Update Asset] workflow to generate renditions using ImageMagick, Adobe recommends you modify the `policy.xml` file at `/etc/ImageMagick/`. デフォルトでは、ImageMagick は OS ボリュームで使用できるディスク領域と空きメモリをすべて使用します。Make the following configuration changes within the `policymap` section of `policy.xml` to limit these resources.

```xml
<policymap>
  <!-- <policy domain="system" name="precision" value="6"/> -->
  <policy domain="resource" name="temporary-path" value="/ephemeral0/imagemagick_tmp"/>
  <policy domain="resource" name="memory" value="1000MiB"/>
  <policy domain="resource" name="map" value="1000MiB"/>
  <!-- <policy domain="resource" name="area" value="1gb"/> -->
  <policy domain="resource" name="disk" value="10000MiB"/>
  <!-- <policy domain="resource" name="file" value="768"/> -->
  <policy domain="resource" name="thread" value="1"/>
  <policy domain="resource" name="throttle" value="50"/>
  <!-- <policy domain="resource" name="time" value="3600"/> -->
</policymap>
```

In addition, set the path of ImageMagick&#39;s temporary folder in the `configure.xml` file (or by setting the environment variable `MAGIC_TEMPORARY_PATH`) to a disk partition that has sufficient space and IOPS.

>[!CAUTION]
>
>使用可能なすべてのディスク領域を ImageMagick で使用する場合、設定を誤るとサーバーの動作が不安定になるおそれがあります。The policy changes required to process large files using ImageMagick may impact the [!DNLExperience Manager] performance. 詳しくは、[ImageMagick のインストールと設定](/help/assets/best-practices-for-imagemagick.md)を参照してください。

>[!NOTE]
>
>ImageMagick `policy.xml` と `configure.xml` ファイルは、ではなく、で入手できます `/usr/lib64/ImageMagick-&#42;/config/` 。設定ファイルの場所については、ImageMagickのドキュメント `/etc/ImageMagick/`[](https://www.imagemagick.org/script/resources.php) を参照してください。

If you are using [!DNL Experience Manager] on Adobe Managed Services (AMS), reach out to Adobe Customer Care if you plan to process lots of large PSD or PSB files. AMSデプロイメントに関するこれらのベストプラクティスを実装し、アドビ独自の形式に関する最良のツールとモデルを選択するには、アドビカスタマーケアの担当者にご相談ください。 [!DNL Experience Manager] は、30000 x 23000ピクセルを超える高解像度PSBファイルを処理できない場合があります。

### XMP の書き戻し {#xmp-writeback}

XMP writeback updates the original asset whenever metadata is modified in [!DNL Experience Manager], which results in the following:

* アセット自体が変更されます
* アセットのバージョンが作成されます
* [!UICONTROL 「DAM アセットの更新」がアセットに対して実行されます]

上記の結果により、大量のリソースが消費されます。このため、この機能が必要でない場合は、[XMP の書き戻しを無効化する](https://helpx.adobe.com/jp/experience-manager/kb/disable-xmp-writeback.html)ことをお勧めします。

ワークフロー実行フラグがチェックされている場合、大量のメタデータを読み込むと、リソースを集中的に使用する XMP 書き戻しアクティビティが発生するおそれがあります。このような読み込みは、他のユーザーのパフォーマンスに影響しないように、サーバー使用率が低いときに計画します。

## レプリケーション {#replication}

Sites の実装などで、アセットを多数のパブリッシュインスタンスにレプリケートするときは、チェーンレプリケーションを使用することをお勧めします。この場合、オーサーインスタンスが単一のパブリッシュインスタンスにレプリケートし、そのパブリッシュインスタンスが代わりに他のパブリッシュインスタンスにレプリケートすることで、オーサーインスタンスを解放します。

### チェーンレプリケーションの設定 {#configure-chain-replication}

1. レプリケーションのチェーン先に使用するパブリッシュインスタンスを選択します。
1. そのパブリッシュインスタンスで、他のパブリッシュインスタンスを指すレプリケーションエージェントを追加します。
1. 追加した各レプリケーションエージェントで、「トリガー」タブの「受信時」を有効にします。

>[!NOTE]
>
>アセットの自動アクティベートはお勧めしません。ただし、必要な場合は、ワークフローの最後の手順（通常は「DAM アセットの更新」）で実行することをお勧めします。

## 検索インデックス {#search-indexes}

システムインデックスの更新が含まれている場合が多いので、最新のサービスパックやパフォーマンス関連のホットフィックスを実装してください。一部のインデックスの最適化については、 [パフォーマンス調整のヒント](https://helpx.adobe.com/jp/experience-manager/kb/performance-tuning-tips.html) （英語）を参照してください。

頻繁に実行するクエリにカスタムインデックスを作成します。詳しくは、[スロークエリの分析手法（英語）](https://aemfaq.blogspot.com/2014/08/oak-query-log-file-analyzer-tool.html)と[カスタムインデックスの作成](/help/sites-deploying/queries-and-indexing.md)を参照してください。For additional insights around query and index best practices, see [Best Practices for Queries and Indexing](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

### Lucene Index の設定 {#lucene-index-configurations}

Some optimizations can be done on the Oak index configurations that can help improve [!DNL Experience Manager Assets] performance. インデックス構成を更新して再インデックス作成時間を改善します。

1. Open CRXDe `/crx/de/index.jsp` and log in as an administrative user.
1. を参照し `/oak:index/lucene`ます。
1. 値、お `String[]` よびを持つ追加プロパティ `excludedPaths``/var`で `/etc/workflow/instances``/etc/replication`す。
1. を参照し `/oak:index/damAssetLucene`ます。 値を追加持つ `String[]` プロパテ `includedPaths` ィ `/content/dam`。 変更を保存します。

例えば、PDFドキュメント内のテキストを検索する場合など、アセットをフルテキスト検索する必要がない場合は、これを無効にします。 フルテキストインデックスを無効にすると、インデックスのパフォーマンスが向上します。 テキスト [!DNL Apache Lucene] 抽出を無効にするには、次の手順に従います。

1. インター [!DNL Experience Manager] フェイスで、 [!UICONTROL パッケージマネージャーにアクセスします]。
1. disable_indexingbinarytextraction-10.zipで入手可能なパッケージをアップロードしてインスト [ールします](assets/disable_indexingbinarytextextraction-10.zip)。

### guessTotal {#guess-total}

大きな結果セットを生成するクエリを作成するときは、クエリ実行時のメモリ消費を抑えるために `guessTotal` パラメーターを使用してください。

## 既知の問題 {#known-issues}

### サイズの大きなファイル {#large-files}

There are two major known issues related to large files in [!DNL Experience Manager]. ファイルのサイズが 2 GB 以上に到達すると、コールドスタンバイの同期でメモリ不足のエラーが発生することがあります。場合によっては、スタンバイの同期が実行されなくなります。また、プライマリインスタンスのクラッシュを引き起こすこともあります。This scenario applies to any file in [!DNL Experience Manager] that is larger than 2GB, including content packages.

同様に、共有S3データストアを使用している間にファイルのサイズが2 GBに達した場合は、ファイルがキャッシュからファイルシステムに完全に保持されるまでに時間がかかる場合があります。 結果として、バイナリなしのレプリケーションを使用しているとき、レプリケーションが完了する前にバイナリデータが保持されていなかった可能性があります。この状況は、特にデータの可用性が重要な場合に問題を引き起こす可能性があります。

## パフォーマンスのテスト {#performance-testing}

For every [!DNL Experience Manager] deployment, establish a performance testing regime that can identify and resolve bottlenecks quickly. 留意点は次のとおりです。

### ネットワークのテスト {#network-testing}

お客様からのネットワークのパフォーマンスに関するすべての懸念については、次のタスクを実行してください。

* お客様のネットワーク内からネットワークのパフォーマンスをテストする
* アドビのネットワーク内からネットワークのパフォーマンスをテストする. AMS ユーザーの場合、CSE を使用してアドビのネットワーク内からテストしてください。
* 別のアクセスポイントからネットワークのパフォーマンスをテストする
* ネットワークのベンチマークツールを使用する
* ディスパッチャーに対してテストする

### [!DNL Experience Manager] インスタンス試験 {#aem-instance-testing}

To minimize latency and achieve high throughput through efficient CPU utilization and load-sharing, monitor the performance of your [!DNL Experience Manager] instance regularly. 具体的には、次のことを実行します。

* Run load tests against the [!DNL Experience Manager] instance.
* アップロードのパフォーマンスと UI の応答性を監視する.

## [!DNL Experience Manager Assets] 資産管理タスクの性能チェックリストと影響 {#checklist}

* HTTPS を有効化して企業の HTTP トラフィックスニッファーに対応する.
* サイズの大きなアセットのアップロードには有線接続を使用する.
* Java 8 にデプロイする
* 最適な JVM パラメーターを設定する。
* ファイルシステムのDataStoreまたはS3データストアを構成します。
* 一時的なワークフローを有効化する.
* Granite のワークフローキューを調整して同時に実行されるジョブ数を制限する.
* Configure [!DNL ImageMagick] to limit resource consumption.
* Remove unnecessary steps from the [!UICONTROL DAM Update Asset] workflow.
* ワークフローとバージョンのパージを設定する.
* 最新のサービスパックとホットフィックスでインデックスを最適化する。利用可能なインデックスのその他の最適化については、アドビカスタマーケアにお問い合わせください。
* guessTotal を使用してクエリのパフォーマンスを最適化する。
* If you configure [!DNL Experience Manager] to detect file types from the content of the files (by enabling **[!UICONTROL Day CQ DAM Mime Type Service]** in the **[!UICONTROL AEM Web Console]**), upload many files in bulk during non-peak hours as it is resource-intensive.
