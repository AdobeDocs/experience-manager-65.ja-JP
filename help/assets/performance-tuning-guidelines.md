---
title: アセットパフォーマンス調整ガイド
description: AEMの設定、ハードウェア、ソフトウェア、およびネットワークコンポーネントに対する変更に関する提案とガイダンス。ボトルネックを解消し、AEM Assetsのパフォーマンスを最適化します。
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: c7d0bcbf39adfc7dfd01742651589efb72959603

---


<!-- TBD: Get reviewed by engineering. -->

# Assets performance tuning guide {#assets-performance-tuning-guide}

Adobe Experience Manager (AEM) Assets のセットアップには、数多くのハードウェア、ソフトウェアおよびネットワークコンポーネントが含まれています。導入のシナリオによっては、パフォーマンス上のボトルネックを排除するために、ハードウェア、ソフトウェアおよびネットワークコンポーネントに対して特殊な設定変更が必要になる場合があります。

また、特定のハードウェアおよびソフトウェアを最適化するガイドラインを識別してそれに従うことで優良な基盤を構築し、AEM Assets の導入によりパフォーマンス、スケーラビリティおよび信頼性の面で期待どおりの結果を得られます。

AEM Assets のパフォーマンスが低下すると、インタラクティブパフォーマンス、アセット処理、ダウンロード速度などの領域におけるユーザーエクスペリエンスに影響します。

パフォーマンスの最適化は、すべてのプロジェクトでターゲット指標を確立する前に実行する、基本的なタスクです。

ユーザーに影響を及ぼす前にパフォーマンス上の問題を検出して修正する必要がある主な領域は次のとおりです。

## プラットフォーム {#platform}

AEM は数々のプラットフォームでサポートされていますが、Linux や Windows ではパフォーマンスを最適化し実装を簡単にする優れたネイティブツールがサポートされています。AEM Assets のデプロイメントでは、高いメモリ要件を満たすために 64 ビットのオペレーティングシステムを採用するのが理想です。あらゆる AEM のデプロイメントにおいて、可能である場合は TarMK を実装してください。TarMK は単一のオーサーインスタンスを超えて拡張できませんが、パフォーマンスは MongoMK よりも優れています。TarMK オフロードインスタンスを追加すると、AEM Assets のデプロイメントのワークフローの処理能力を高めることができます。

### 一時フォルダ {#temp-folder}

アセットのアップロード時間を短縮するには、Javaの一時ディレクトリに高いストレージを使用してください。 Linux および Windows の場合は、RAM ドライブまたは SSD を使用できます。クラウドベースの環境では、同等の高速ストレージタイプを使用できます。For example in Amazon EC2, an [ephemeral drive](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html) drive can be used for the temporary folder.

サーバーに十分なメモリがあるという前提で、RAM ドライブを設定します。Linux の場合、8GB RAM ドライブを作成するには、次のコマンドを実行します。

```shell
mkfs -q /dev/ram1 800000
 mkdir -p /mnt/aem-tmp
 mount /dev/ram1 /mnt/aem-tmp
 df -H | grep aem-tmp
```

Windows OSでは、サードパーティ製のドライバを使用してRAMドライブを作成するか、SSDなどの高パフォーマンスのストレージを使用します。

Once the high performance temporary volume is ready, set the JVM parameter `-Djava.io.tmpdir`. For example, you could add the JVM parameter below to the `CQ_JVM_OPTS` variable in the `bin/start` script of AEM:

`-Djava.io.tmpdir=/mnt/aem-tmp`

## Java の設定 {#java-configuration}

### Java バージョン {#java-version}

パフォーマンスを最適化するために、AEM AssetsをJava 8にデプロイすることをお勧めします。

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

すべての AEM Assets のユーザーに、データストアをセグメントストアから分離することをお勧めします。また、`maxCachedBinarySize` パラメーターと `cacheSizeInMB` パラメーターを設定することでパフォーマンスを最大化するのに役立ちます。キャッシュに含めることができるように、`maxCachedBinarySize` を最小のファイルサイズに設定します。`cacheSizeInMB` 内のデータストアで使用するインメモリキャッシュのサイズを指定します。この値は合計ヒープサイズの 2～10％に設定することをお勧めします。ただし、負荷テストやパフォーマンステストが理想的な設定を決定するのに役立ちます。

### バッファーされる画像キャッシュの最大サイズの設定 {#configure-the-maximum-size-of-the-buffered-image-cache}

多数のアセットを Adobe Experience Manager にアップロードするときは、メモリ消費の予期しないスパイクに対応するために、また OutOfMemoryErrors による JVM エラーを避けるために、バッファーされる画像キャッシュの最大サイズを減らしてください。例えば、最大ヒープ（-`Xmx` パラメーター）が 5 GB のシステムで、Oak BlobCache が 1 GB、文書キャッシュが 2 GB に設定されているとします。このときに、バッファーされるキャッシュが最大 1.25 GB のメモリを使用した場合、予期しないスパイクに使用できるメモリは 0.75 GB のみとなります。

バッファーされるキャッシュサイズは OSGi Web コンソールで設定します。`https://host:port/system/console/configMgr/com.day.cq.dam.core.impl.cache.CQBufferedImageCache` で、プロパティ `cq.dam.image.cache.max.memory` をバイト単位で指定します。例えば、1073741824 は 1 GB です（1024 x 1024 x 1024 = 1 GB）。

AEM 6.1 SP1 以降で `sling:osgiConfig` ノードを使用してこのプロパティを設定する場合は、データタイプを必ず Long にします。詳しくは、[CQBufferedImageCache がアセットのアップロード中にヒープを消費する](https://helpx.adobe.com/jp/experience-manager/kb/cqbufferedimagecache-consumes-heap-during-asset-uploads.html)を参照してください。

### 共有データストア {#shared-data-stores}

S3 または共有ファイルデータストアの実装は、ディスク領域の節約と大規模な実装におけるネットワークスループットの向上に役立ちます。For more information on the pros and cons of using a shared datastore, see [Assets Sizing Guide](/help/assets/assets-sizing-guide.md).

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

多くの企業には HTTP トラフィックをスニッフィングするファイアウォールがあり、ファイルのアップロードに干渉しファイルを破損するので、HTTPS を有効にすることをお勧めします。サイズの大きなファイルのアップロードについては、Wi-Fi ネットワークでは簡単に飽和するおそれがあるので、必ず有線でネットワークに接続してください。For guidelines on identifying network bottlenecks, see [Assets Sizing Guide](/help/assets/assets-sizing-guide.md). ネットワークトポロジを分析してネットワークのパフォーマンスを評価するには、[Assets のネットワークに関する考慮事項](/help/assets/assets-network-considerations.md)を参照してください。

第一に、ネットワークの最適化戦略は使用できる帯域幅や、AEM インスタンスに対する負荷によって変わります。ファイアウォールやプロキシなどの一般的な設定オプションは、ネットワークのパフォーマンスの改善に役立ちます。留意点は次のとおりです。

* インスタンスタイプ（小、中、大）によって、AEM インスタンスに十分なネットワーク帯域幅があることを確認します。AEM が AWS にホストされている場合、帯域幅が適切に分散されていることが特に重要です。
* AEM インスタンスが AWS にホストされている場合、広い用途に対応するスケールポリシーがあると便利です。高い負荷が予想される場合は、インスタンスのサイズを大きくします。負荷が標準的または低い場合は、インスタンスのサイズを小さくします。
* HTTPS：ユーザーの多くは HTTP トラフィックをスニッフィングするファイアウォールを装備しており、ファイルのアップロード操作に干渉しファイルを破損することもあります。
* サイズの大きなファイルのアップロード：必ず有線でネットワークに接続してください（Wi-Fi 接続は簡単に飽和するおそれがあります）。

## ワークフロー {#workflows}

### 一時的なワークフロー {#transient-workflows}

Wherever possible, set the [!UICONTROL DAM Update Asset] workflow to Transient. この設定にすると、ワークフローが通常のトラッキングやアーカイブ処理をパススルーする必要がなくなるので、ワークフローの処理に必要なオーバーヘッドが大幅に削減されます。

1. AEMインスタ `/miscadmin` ンス内のに移動しま `https://[aem_server]:[port]/miscadmin`す。

1. ツール/ワ **[!UICONTROL ークフ]** ロー **[!UICONTROL /モデル]** / **[!UICONTROL dam]** dam **** leversを展開します。

1. Open **[!UICONTROL DAM Update Asset]**. フローティングツールパネルで、「**[!UICONTROL ページ]**」タブに切り替えて「**[!UICONTROL ページプロパティ]**」をクリックします。

1. Select **[!UICONTROL Transient Workflow]** and click **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >一部の機能は一時的なワークフローをサポートしません。If your [!DNL Assets] deployment requires these features, do not configure transient workflows.

In cases where transient workflows cannot be used, run workflow purging regularly to delete archived [!UICONTROL DAM Update Asset] workflows to ensure system performance does not degrade.

通常、削除ワークフローを週単位で実行します。 ただし、大規模なアセットの取り込み中など、リソースを大量に消費するシナリオでは、より頻繁に実行できます。

ワークフローのパージを設定するには、OSGi コンソールで新しい Adobe Granite のワークフローのパージ設定を追加します。次に、ワークフローを週次メンテナンスウィンドウの一部としてスケジュールを設定します。

パージの実行時間が長すぎる場合、タイムアウトします。このため、ワークフローの数が多すぎることが原因でパージワークフローが終わらない状況を避けるために、パージジョブが確実に終わるようにする必要があります。

For example, after executing numerous non-transient workflows (that creates workflow instance nodes), you can execute [ACS AEM Commons Workflow Remover](https://adobe-consulting-services.github.io/acs-aem-commons/features/workflow-remover.html) on an ad-hoc basis. これにより、冗長および完了したワークフローのインスタンスが即座に削除されるので、Adobe Granite のワークフローのパージスケジューラーが実行されるのを待つ必要がありません。

### 並列ジョブの最大数 {#maximum-parallel-jobs}

デフォルトでは、AEM は最大でサーバー上のプロセッサーと同じ数の並列ジョブを実行できます。The problem with this setting is that during periods of heavy load, all of the processors are occupied by [!UICONTROL DAM Update Asset] workflows, slowing down UI responsiveness and preventing AEM from running other processes that safeguard server performance and stability. 次の手順を実行して、この値をサーバーで使用できるプロセッサーの半分の値にすることをお勧めします。

1. Experience Manager Authorで、に移動します `https://[aem_server]:[port]/system/console/slingevent`。

1. Click **[!UICONTROL Edit]** on each workflow queue that is relevant to your implementation, for example **[!UICONTROL Granite Transient Workflow Queue]**.

1. Update the value of **[!UICONTROL Maximum Parallel Jobs]** and click **[!UICONTROL Save]**.

まずは、キューを使用できるプロセッサーの半分に設定してください。ただし、場合によっては最大のスループットを得るためにこの値をお使いの環境に合わせて増減させる必要があります。一時的および一時的でないワークフローには別個のキューが用意されているほか、外部ワークフローなどその他の処理も存在します。プロセッサーの 50％に設定された複数のキューが同時にアクティブになると、システムはすぐにオーバーロードします。頻繁に使用されるキューは、ユーザーの実装により大きく異なります。このため、サーバーの安定性を損なうことなく効率を最大化するには、これらを慎重に設定する必要が生じる場合があります。

### DAM アセットの更新設定 {#dam-update-asset-configuration}

[!UICONTROL DAM Update Asset] Workflowには、Scene7 PTIFFの生成やInDesign Serverの統合など、タスク用に設定されたすべての手順が含まれています。 ただし、大多数のユーザーにとってこれらの手順のうちのいくつかは不要です。Adobe recommends you create a custom copy of the [!UICONTROL DAM Update Asset] workflow model, and remove any unnecessary steps. In this case, update the launchers for [!UICONTROL DAM Update Asset] to point to the new model.

Running the [!UICONTROL DAM Update Asset] workflow intensively can sharply increase the size of your file datatastore. アドビが実施した実験の結果によると、8 時間以内に約 5,500 のワークフローを実行した場合、データストアのサイズが約 400 GB 増加する可能性があります。

これは一時的な増加であり、データストアのガベージコレクションタスクを実行すると、データストアは元のサイズに戻ります。

通常、データストアのガベージコレクションタスクは、スケジュールされた他のメンテナンスタスクと共に毎週実行されます。

If you have a limited disk space and run [!UICONTROL DAM Update Asset] workflows intensively, consider scheduling the garbage collection task more frequently.

#### 実行時のレンディションの生成 {#runtime-rendition-generation}

お客様は Web サイトやビジネスパートナーへの配布に様々なサイズや形式の画像を使用します。各レンディションによりリポジトリ内のアセットの足跡が増加するので、この機能は適切なタイミングで使用することをお勧めします。画像の処理と保存に必要なリソースを減らすために、これらの画像を取り込み中にではなく実行時にレンディションとして生成できます。

多くの Sites のお客様はリクエストされた時点で画像のサイズを変更および切り抜く画像サーブレットを実装しています。これにより、パブリッシュインスタンスにさらに負荷がかけられます。ただし、これらの画像をキャッシュできる限り、問題を減らすことができます。

もう 1 つの方法では、Scene7 テクノロジーを使用して画像の操作をすべて引き渡します。さらに、Brand Portal もデプロイできます。Brand Portal は、AEM インフラストラクチャからレンディションを生成する責務だけでなく、パブリッシュ層全体も受け継ぎます。

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
>使用可能なすべてのディスク領域を ImageMagick で使用する場合、設定を誤るとサーバーの動作が不安定になるおそれがあります。
>
>ImageMagick を使用して大きなファイルを処理するために必要なポリシー変更をおこなうと、AEM のパフォーマンスに影響する可能性があります。詳しくは、[ImageMagick のインストールと設定](/help/assets/best-practices-for-imagemagick.md)を参照してください。

>[!NOTE]
>
>ImageMagickとファイルは、ではなく、で使用で `policy.xml` きます。 `configure.xml` 設定ファ `/usr/lib64/ImageMagick-&#42;/config/` イルの場所は `/etc/ImageMagick/`[](https://www.imagemagick.org/script/resources.php) 、ImageMagickのドキュメントを参照してください。

>[!TIP]
>
>Adobe Managed Services(AMS)でExperience Managerを使用している場合は、大量のPSDまたはPSBファイルを処理する予定の場合は、アドビのサポート窓口にご連絡ください。 AMS導入のためのこれらのベストプラクティスを実装し、アドビ独自の形式に最適なツールとモデルを選択するには、アドビカスタマーケアの担当者にご相談ください。

### XMP の書き戻し {#xmp-writeback}

XMP の書き戻しにより、AEM でメタデータが変更されたときは常に元のアセットが更新されます。これにより、次のような結果になります。

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

システムインデックスの更新が含まれている場合が多いので、最新のサービスパックやパフォーマンス関連のホットフィックスを実装してください。インデックス [の最適化については](https://helpx.adobe.com/jp/experience-manager/kb/performance-tuning-tips.html) 、パフォーマンス調整のヒントを参照してください。

頻繁に実行するクエリにカスタムインデックスを作成します。詳しくは、[スロークエリの分析手法（英語）](https://aemfaq.blogspot.com/2014/08/oak-query-log-file-analyzer-tool.html)と[カスタムインデックスの作成](/help/sites-deploying/queries-and-indexing.md)を参照してください。For additional insights around query and index best practices, see [Best Practices for Queries and Indexing](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

### Lucene Index の設定 {#lucene-index-configurations}

一部の最適化は、AEM Assetsのパフォーマンスを向上させるために、Oakインデックスの設定で行うことができます。 インデックス設定を更新して、再インデックス作成時間を改善します。

1. Open CRXDe `/crx/de/index.jsp` and log in as an administrative user
1. 参照先 `/oak:index/lucene`
1. 値、および追加を持つ文[] 字列プ `excludedPaths` ロ `/var`パテ `/etc/workflow/instances`ィで `/etc/replication`す。
1. 参照しま `/oak:index/damAssetLucene`す。 値を追加持つプ `String[]` ロパティ `includedPaths``/content/dam`。
1. 保存.

<!-- TBD: Review by engineering if required in 6.5 docs or not.

(AEM6.1 and 6.2 only) Update the `ntBaseLucene` index to improve asset delete and move performance:

1. Browse to `/oak:index/ntBaseLucene/indexRules/nt:base/properties`

1. Add two nt:unstructured nodes `slingResource` and `damResolvedPath` under `/oak:index/ntBaseLucene/indexRules/nt:base/properties`

1. Set the properties below on the nodes (where `ordered` and `propertyIndex` properties are of type `Boolean`:

   ```
   slingResource
   name="sling:resource"
   ordered=false
   propertyIndex= true
   type="String"
   damResolvedPath
   name="dam:resolvedPath"
   ordered=false
   propertyIndex=true
   type="String"
   ```

1. On the `/oak:index/ntBaseLucene` node, set the property `reindex=true`. Click **[!UICONTROL Save All]**.
1. Monitor the error.log to see when indexing is completed:
   Reindexing completed for indexes: [/oak:index/ntBaseLucene]
1. You can also see that indexing is completed by refreshing the /oak:index/ntBaseLucene node in CRXDe as the reindex property would go back to false
1. Once indexing is completed then go back to CRXDe and set the "type" property to disabled on these two indexes

    * */oak:index/slingResource*
    * */oak:index/damResolvedPath*

1. Click "Save All"
-->

Lucene テキスト抽出の無効化：

例えば、PDFドキュメント内のテキストを検索する場合など、アセットの全文検索を行う必要がない場合は、無効にします。 フルテキストインデックスを無効にすることで、インデックスのパフォーマンスを向上できます。

1. Go to the AEM package manager `/crx/packmgr/index.jsp`.
1. disable_indexingbinarytextraction-10.zipで入手可能なパッケ [ージをアップロードしてインストールします](assets/disable_indexingbinarytextextraction-10.zip)。

### guessTotal {#guess-total}

大きな結果セットを生成するクエリを作成するときは、クエリ実行時のメモリ消費を抑えるために `guessTotal` パラメーターを使用してください。

## 既知の問題 {#known-issues}

### サイズの大きなファイル {#large-files}

AEM では、サイズの大きなファイルに関連する既知の問題が主に 2 つあります。ファイルのサイズが 2 GB 以上に到達すると、コールドスタンバイの同期でメモリ不足のエラーが発生することがあります。場合によっては、スタンバイの同期が実行されなくなります。また、プライマリインスタンスのクラッシュを引き起こすこともあります。このシナリオは、コンテンツパッケージを含む、AEM 内の 2 GB を超えるすべてのファイルが該当します。

同様に、S3 共有データストアを使用している間にファイルのサイズが 2 GB に到達すると、キャッシュからファイルシステムにファイルが完全に保持されるまで、少し時間がかかることがあります。結果として、バイナリなしのレプリケーションを使用しているとき、レプリケーションが完了する前にバイナリデータが保持されていなかった可能性があります。この状況は、特にデータの可用性が重要な場合に問題を引き起こす可能性があります。

## パフォーマンスのテスト {#performance-testing}

すべての AEM のデプロイメントでボトルネックをすばやく特定し解決できるように、パフォーマンステストの体制を確立してください。留意点は次のとおりです。

### ネットワークのテスト {#network-testing}

お客様からのネットワークのパフォーマンスに関するすべての懸念については、次のタスクを実行してください。

* お客様のネットワーク内からネットワークのパフォーマンスをテストする
* アドビのネットワーク内からネットワークのパフォーマンスをテストする. AMS ユーザーの場合、CSE を使用してアドビのネットワーク内からテストしてください。
* 別のアクセスポイントからネットワークのパフォーマンスをテストする
* ネットワークのベンチマークツールを使用する
* ディスパッチャーに対してテストする

### AEM インスタンスのテスト {#aem-instance-testing}

CPUの効率的な使用とロードシェアリングを通じて、待ち時間を最小限に抑え、高いスループットを実現するには、AEMインスタンスのパフォーマンスを定期的に監視します。 具体的には、次のことを実行します。

* AEM インスタンスに対して負荷テストを実行する
* アップロードのパフォーマンスと UI の応答性を監視する

## AEM Assets のパフォーマンスチェックリストおよびアセット管理タスクの影響 {#checklist}

* HTTPS を有効化して企業の HTTP トラフィックスニッファーに対応する
* サイズの大きなアセットのアップロードには有線接続を使用する
* Java 8 にデプロイする
* 最適な JVM パラメーターを設定する
* ファイルシステムデータストアまたは S3 データストアを設定する
* 一時的なワークフローを有効化する
* Granite のワークフローキューを調整して同時に実行されるジョブ数を制限する
* ImageMagick を設定してリソースの消費を制限する
* Remove unnecessary steps from the [!UICONTROL DAM Update Asset] workflow
* ワークフローとバージョンのパージを設定する
* 最新のサービスパックとホットフィックスでインデックスを最適化する。その他のインデックスの最適化方法については、アドビサポートに問い合わせてください。
* guessTotal を使用してクエリのパフォーマンスを最適化する。
* （**[!UICONTROL AEM Web コンソール]**&#x200B;の **[!UICONTROL Day CQ DAM Mime Type サービス]**&#x200B;を有効にすることで）ファイルのコンテンツからファイルタイプを検出するように AEM を構成している場合、大量のファイルを一括アップロードする際はリソースを大量に消費するので、ピーク時以外の時間におこないます。
