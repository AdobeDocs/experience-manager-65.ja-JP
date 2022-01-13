---
title: パフォーマンスチューニング [!DNL Assets].
description: に関する提案とガイダンス [!DNL Experience Manager] 構成、ハードウェア、ソフトウェア、ネットワーク・コンポーネントの変更により、ボトルネックを解消し、パフォーマンスを最適化 [!DNL Experience Manager Assets].
contentOwner: AG
mini-toc-levels: 1
role: Architect, Admin
feature: Asset Management
exl-id: 1d9388de-f601-42bf-885b-6a7c3236b97e
source-git-commit: d1b4cf87291f7e4a0670a21feca1ebf8dd5e0b5e
workflow-type: tm+mt
source-wordcount: '2741'
ht-degree: 51%

---

<!-- TBD: Get reviewed by engineering. -->

# [!DNL Adobe Experience Manager Assets] パフォーマンスチューニングガイド {#assets-performance-tuning-guide}

An [!DNL Experience Manager Assets] セットアップには、多数のハードウェア、ソフトウェア、およびネットワークコンポーネントが含まれています。 導入のシナリオによっては、パフォーマンス上のボトルネックを排除するために、ハードウェア、ソフトウェアおよびネットワークコンポーネントに対して特殊な設定変更が必要になる場合があります。

また、特定のハードウェアおよびソフトウェア最適化ガイドラインを識別して遵守することで、お客様の [!DNL Experience Manager Assets] パフォーマンス、拡張性、信頼性に関する期待に応えるデプロイメント

でのパフォーマンスが低下 [!DNL Experience Manager Assets] は、インタラクティブなパフォーマンス、アセット処理、ダウンロード速度などの領域でのユーザーエクスペリエンスに影響を与える可能性があります。

パフォーマンスの最適化は、すべてのプロジェクトでターゲット指標を確立する前に実行する、基本的なタスクです。

ユーザーに影響を及ぼす前にパフォーマンス上の問題を検出して修正する必要がある主な領域は次のとおりです。

## Platform {#platform}

Experience Managerは多くのプラットフォームでサポートされていますが、Adobeは Linux と Windows で最も高いネイティブツールのサポートを見つけ、パフォーマンスを最適化し、実装を容易にします。 64 ビットオペレーティングシステムを導入して、 [!DNL Experience Manager Assets] デプロイメント。 任意のExperience Managerデプロイメントと同様に、可能な限り TarMK を実装する必要があります。 TarMK は単一のオーサーインスタンスを超えて拡張できませんが、パフォーマンスは MongoMK よりも優れています。TarMK オフロードインスタンスを追加して、 [!DNL Experience Manager Assets] デプロイメント。

### 一時フォルダー {#temp-folder}

アセットのアップロード時間を短縮するには、Java の一時ディレクトリに高パフォーマンスのストレージを使用します。 Linux および Windows の場合は、RAM ドライブまたは SSD を使用できます。クラウドベースの環境では、同等の高速ストレージタイプを使用できます。例えば、Amazon EC2 では、 [短命駆動](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html) ドライブは一時フォルダに使用できます。

サーバーに十分なメモリがあるという前提で、RAM ドライブを設定します。Linux の場合、8GB RAM ドライブを作成するには、次のコマンドを実行します。

```shell
mkfs -q /dev/ram1 800000
 mkdir -p /mnt/aem-tmp
 mount /dev/ram1 /mnt/aem-tmp
 df -H | grep aem-tmp
```

Windows OS では、サードパーティ製のドライバを使用して RAM ドライブを作成するか、SSD などの高性能ストレージを使用します。

高パフォーマンスの一時ボリュームの準備が整ったら、JVM パラメーターを設定します `-Djava.io.tmpdir`. 例えば、以下の JVM パラメーターを `CQ_JVM_OPTS` 変数の `bin/start` スクリプト [!DNL Experience Manager]:

`-Djava.io.tmpdir=/mnt/aem-tmp`

## Java の設定 {#java-configuration}

### Java バージョン {#java-version}

Adobeは、 [!DNL Experience Manager Assets] を Java 8 に設定して、最適なパフォーマンスを実現します。

<!-- TBD: Link to the latest official word around Java.
-->

### JVM パラメーター {#jvm-parameters}

次の JVM パラメーターを設定します。

* `-XX:+UseConcMarkSweepGC`
* `-Doak.queryLimitInMemory`=500000
* `-Doak.queryLimitReads`=100000
* `-Dupdate.limit`=250000
* `-Doak.fastQuerySize`=true

## データストアとメモリの設定 {#data-store-and-memory-configuration}

### ファイルデータストアの設定 {#file-data-store-configuration}

すべての [!DNL Experience Manager Assets] ユーザー。 また、`maxCachedBinarySize` パラメーターと `cacheSizeInMB` パラメーターを設定することでパフォーマンスを最大化するのに役立ちます。キャッシュに含めることができるように、`maxCachedBinarySize` を最小のファイルサイズに設定します。`cacheSizeInMB` 内のデータストアで使用するインメモリキャッシュのサイズを指定します。この値は合計ヒープサイズの 2～10％に設定することをお勧めします。ただし、負荷テストやパフォーマンステストが理想的な設定を決定するのに役立ちます。

### バッファーされる画像キャッシュの最大サイズの設定 {#configure-the-maximum-size-of-the-buffered-image-cache}

大量のアセットをにアップロードする際 [!DNL Adobe Experience Manager]：メモリ消費の予期しないスパイクを許可し、OutOfMemoryErrors で JVM が失敗するのを防ぐには、バッファーされる画像キャッシュの最大サイズを減らします。 例えば、最大ヒープ（-`Xmx` パラメーター）が 5 GB のシステムで、Oak BlobCache が 1 GB、文書キャッシュが 2 GB に設定されているとします。このときに、バッファーされるキャッシュが最大 1.25 GB のメモリを使用した場合、予期しないスパイクに使用できるメモリは 0.75 GB のみとなります。

バッファーされるキャッシュサイズは OSGi Web コンソールで設定します。`https://host:port/system/console/configMgr/com.day.cq.dam.core.impl.cache.CQBufferedImageCache` で、プロパティ `cq.dam.image.cache.max.memory` をバイト単位で指定します。例えば、1073741824 は 1 GB です（1024 x 1024 x 1024 = 1 GB）。

Experience Manager6.1 SP1( `sling:osgiConfig` ノードでこのプロパティを設定する場合は、データ型を必ず Long に設定してください。 詳しくは、[CQBufferedImageCache がアセットのアップロード中にヒープを消費する](https://helpx.adobe.com/jp/experience-manager/kb/cqbufferedimagecache-consumes-heap-during-asset-uploads.html)を参照してください。

### 共有データストア {#shared-data-stores}

S3 または共有ファイルデータストアの実装は、ディスク領域の節約と大規模な実装におけるネットワークスループットの向上に役立ちます。共有データストアの使用に関する長所と短所について詳しくは、 [Assets サイズ設定ガイド](/help/assets/assets-sizing-guide.md).

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

多くの企業には HTTP トラフィックをスニッフィングするファイアウォールがあり、ファイルのアップロードに干渉しファイルを破損するので、HTTPS を有効にすることをお勧めします。サイズの大きなファイルのアップロードについては、Wi-Fi ネットワークでは簡単に飽和するおそれがあるので、必ず有線でネットワークに接続してください。ネットワークのボトルネックの特定に関するガイドラインについては、 [Assets サイズ設定ガイド](/help/assets/assets-sizing-guide.md). ネットワークトポロジを分析してネットワークのパフォーマンスを評価するには、 [Assets のネットワークに関する考慮事項](/help/assets/assets-network-considerations.md).

主に、ネットワーク最適化戦略は、使用可能な帯域幅の量と、 [!DNL Experience Manager] インスタンス。 ファイアウォールやプロキシなどの一般的な設定オプションは、ネットワークのパフォーマンスの改善に役立ちます。留意点は次のとおりです。

* インスタンスのタイプ（小、中、大）に応じて、Experience Managerインスタンスに十分なネットワーク帯域幅があることを確認します。 特に次の場合、十分な帯域幅の割り当てが重要です。 [!DNL Experience Manager] はAWSでホストされています。
* 次に、 [!DNL Experience Manager] インスタンスはAWSでホストされており、多用途なスケーリングポリシーを採用することでメリットを得ることができます。 高い負荷が予想される場合は、インスタンスのサイズを大きくします。負荷が標準的または低い場合は、インスタンスのサイズを小さくします。
* HTTPS：ユーザーの多くは HTTP トラフィックをスニッフィングするファイアウォールを装備しており、ファイルのアップロード操作に干渉しファイルを破損することもあります。
* サイズの大きなファイルのアップロード：必ず有線でネットワークに接続してください（Wi-Fi 接続は簡単に飽和するおそれがあります）。

## ワークフロー {#workflows}

### 一時的なワークフロー {#transient-workflows}

可能な限り、 [!UICONTROL DAM アセットの更新] ワークフローを一時的なものにします。 この設定にすると、ワークフローが通常のトラッキングやアーカイブ処理をパススルーする必要がなくなるので、ワークフローの処理に必要なオーバーヘッドが大幅に削減されます。

1. に移動します。 `/miscadmin` 内 [!DNL Experience Manager] のデプロイメント `https://[aem_server]:[port]/miscadmin`.

1. 展開 **[!UICONTROL ツール]** > **[!UICONTROL ワークフロー]** > **[!UICONTROL モデル]** > **[!UICONTROL dam]**.

1. 開く **[!UICONTROL DAM アセットの更新]**. フローティングツールパネルで、「**[!UICONTROL ページ]**」タブに切り替えて「**[!UICONTROL ページプロパティ]**」をクリックします。

1. 選択 **[!UICONTROL 一時的なワークフロー]** をクリックし、 **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >一部の機能は一時的なワークフローをサポートしません。次に、 [!DNL Assets] デプロイメントには、これらの機能が必要です。一時的なワークフローは設定しないでください。

一時的なワークフローを使用できない場合は、定期的にワークフローのパージを実行して、アーカイブ済みを削除します [!UICONTROL DAM アセットの更新] ワークフローを使用して、システムのパフォーマンスが低下しないようにします。

通常、パージワークフローは毎週実行します。 ただし、大規模なアセットの取り込み中など、リソースを大量に消費するシナリオでは、より頻繁にアセットを実行できます。

ワークフローのパージを設定するには、OSGi コンソールで新しい Adobe Granite のワークフローのパージ設定を追加します。次に、ワークフローを週次メンテナンスウィンドウの一部としてスケジュールを設定します。

パージの実行時間が長すぎる場合、タイムアウトします。このため、ワークフローの数が多すぎることが原因でパージワークフローが終わらない状況を避けるために、パージジョブが確実に終わるようにする必要があります。

例えば、一時的でない多数のワークフロー（ワークフローインスタンスノードを作成する）を実行した後に、を実行できます [ACS AEM Commons Workflow Remover](https://adobe-consulting-services.github.io/acs-aem-commons/features/workflow-remover.html) アドホックベースで これにより、冗長および完了したワークフローのインスタンスが即座に削除されるので、Adobe Granite のワークフローのパージスケジューラーが実行されるのを待つ必要がありません。

### 並列ジョブの最大数 {#maximum-parallel-jobs}

デフォルトでは、 [!DNL Experience Manager] は、サーバー上のプロセッサの数と同じ並列ジョブの最大数を実行します。 この設定の問題は、負荷が大きい時間帯に、すべてのプロセッサが [!UICONTROL DAM アセットの更新] ワークフロー、UI の応答性の低下と回避 [!DNL Experience Manager] サーバのパフォーマンスと安定性を保護する他のプロセスの実行から 次の手順を実行して、この値をサーバーで使用できるプロセッサーの半分の値にすることをお勧めします。

1. オン [!DNL Experience Manager] 作成者、アクセス `https://[aem_server]:[port]/system/console/slingevent`.

1. クリック **[!UICONTROL 編集]** 実装に関連する各ワークフローキュー（例： ）に対して、 **[!UICONTROL Granite 一時的なワークフローキュー]**.

1. の値を更新 **[!UICONTROL 並列ジョブの最大数]** をクリックし、 **[!UICONTROL 保存]**.

まずは、キューを使用できるプロセッサーの半分に設定してください。ただし、場合によっては最大のスループットを得るためにこの値をお使いの環境に合わせて増減させる必要があります。一時的および一時的でないワークフローには別個のキューが用意されているほか、外部ワークフローなどその他の処理も存在します。プロセッサーの 50％に設定された複数のキューが同時にアクティブになると、システムはすぐにオーバーロードします。頻繁に使用されるキューは、ユーザーの実装により大きく異なります。このため、サーバーの安定性を損なうことなく効率を最大化するには、これらを慎重に設定する必要が生じる場合があります。

### DAM アセットの更新設定 {#dam-update-asset-configuration}

この [!UICONTROL DAM アセットの更新] ワークフローには、Dynamic Media PTIFF 生成や [!DNL Adobe InDesign Server] 統合とも呼ばれます。 ただし、大多数のユーザーにとってこれらの手順のうちのいくつかは不要です。Adobeでは、 [!UICONTROL DAM アセットの更新] ワークフローモデルを作成し、不要なステップを削除します。 この場合、のランチャーを更新します。 [!UICONTROL DAM アセットの更新] をクリックして、新しいモデルを指定します。

の実行 [!UICONTROL DAM アセットの更新] ワークフローでは、ファイルデータストアのサイズを集中的に大幅に増やすことができます。 アドビが実施した実験の結果によると、8 時間以内に約 5,500 のワークフローを実行した場合、データストアのサイズが約 400 GB 増加する可能性があります。

これは一時的な増加であり、データストアのガベージコレクションタスクを実行すると、データストアは元のサイズに戻ります。

通常、データストアのガベージコレクションタスクは、スケジュールされた他のメンテナンスタスクと共に毎週実行されます。

ディスク容量が限られている場合は、次のコマンドを実行します。 [!UICONTROL DAM アセットの更新] ワークフローの集中的な作業では、ガベージコレクションタスクのスケジュールをより頻繁に設定することを検討してください。

#### 実行時のレンディションの生成 {#runtime-rendition-generation}

お客様は Web サイトやビジネスパートナーへの配布に様々なサイズや形式の画像を使用します。各レンディションによりリポジトリ内のアセットの足跡が増加するので、この機能は適切なタイミングで使用することをお勧めします。画像の処理と保存に必要なリソースを減らすために、これらの画像を取り込み中にではなく実行時にレンディションとして生成できます。

多くの Sites のお客様はリクエストされた時点で画像のサイズを変更および切り抜く画像サーブレットを実装しています。これにより、パブリッシュインスタンスにさらに負荷がかけられます。ただし、これらの画像をキャッシュできる限り、問題を減らすことができます。

別のアプローチは、 Dynamic Mediaテクノロジーを使用して画像の操作を完全にハンドオフすることです。 さらに、レンディション生成の責任を [!DNL Experience Manager] インフラストラクチャのみでなく、パブリッシュ層全体にも影響を与えます。

#### ImageMagick {#imagemagick}

次をカスタマイズした場合： [!UICONTROL DAM アセットの更新] ImageMagick を使用してレンディションを生成するワークフローでは、Adobeは、 `policy.xml` ～にファイルを送る `/etc/ImageMagick/`. デフォルトでは、ImageMagick は OS ボリュームで使用できるディスク領域と空きメモリをすべて使用します。次の設定変更を `policymap` セクション `policy.xml` を使用して、これらのリソースを制限します。

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

さらに、 `configure.xml` ファイル（または環境変数を設定して） `MAGIC_TEMPORARY_PATH`) を、十分な容量と IOPS を持つディスクパーティションに割り当てます。

>[!CAUTION]
>
>使用可能なすべてのディスク領域を ImageMagick で使用する場合、設定を誤るとサーバーの動作が不安定になるおそれがあります。ImageMagick を使用して大きなファイルを処理するために必要なポリシーの変更は、 [!DNL Experience Manager] パフォーマンス。 詳しくは、[ImageMagick のインストールと設定](/help/assets/best-practices-for-imagemagick.md)を参照してください。

>[!NOTE]
>
>ImageMagick `policy.xml` および `configure.xml` ファイルは次の場所で利用できます： `/usr/lib64/ImageMagick-&#42;/config/` の代わりに `/etc/ImageMagick/`参照： [ImageMagick のドキュメント](https://www.imagemagick.org/script/resources.php) （設定ファイルの場所）。

次を使用する場合： [!DNL Experience Manager] 大きなPSDや PSB ファイルを大量に処理する予定がある場合は、Adobe Managed Services(AMS) でAdobeカスタマーサポートにお問い合わせください。 Adobeカスタマーサポート担当者と協力して、AMS の導入に関するこれらのベストプラクティスを実装し、Adobe独自の形式に関する最適なツールとモデルを選択します。 [!DNL Experience Manager] では、30000 x 23000ピクセルを超える高解像度の PSB ファイルを処理できない場合があります。

### XMP の書き戻し {#xmp-writeback}

メタデータが [!DNL Experience Manager]を呼び出すと、次のようになります。

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

インストール [最新のサービスパック](/help/release-notes/release-notes.md) およびパフォーマンス関連のホットフィックスは、多くの場合、システムインデックスの更新を含みます。 詳しくは、 [パフォーマンスチューニングのヒント](https://helpx.adobe.com/jp/experience-manager/kb/performance-tuning-tips.html) 一部のインデックスの最適化。

頻繁に実行するクエリにカスタムインデックスを作成します。詳しくは、[スロークエリの分析手法（英語）](https://aemfaq.blogspot.com/2014/08/oak-query-log-file-analyzer-tool.html)と[カスタムインデックスの作成](/help/sites-deploying/queries-and-indexing.md)を参照してください。クエリとインデックスのベストプラクティスに関する追加のインサイトについては、 [クエリとインデックスに関するベストプラクティス](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

### Lucene Index の設定 {#lucene-index-configurations}

Oak インデックス設定で最適化を行うと、改善に役立ちます。 [!DNL Experience Manager Assets] パフォーマンス。 インデックス設定を更新して、インデックス再作成時間を短縮します。

1. CRXDe を開く `/crx/de/index.jsp` 管理者ユーザーとしてログインします。
1. 参照先 `/oak:index/lucene`.
1. を追加します。 `String[]` プロパティ `excludedPaths` 値あり `/var`, `/etc/workflow/instances`、および `/etc/replication`.
1. 参照先 `/oak:index/damAssetLucene`. を追加します。 `String[]` プロパティ `includedPaths` 値と共に `/content/dam`. 変更を保存します。

PDFドキュメント内のテキストを検索するなど、アセットの全文検索を行う必要がない場合は、無効にします。 フルテキストインデックスを無効にすると、インデックスのパフォーマンスが向上します。 無効にするには [!DNL Apache Lucene] テキスト抽出：次の手順に従います。

1. In [!DNL Experience Manager] インターフェイス、アクセス [!UICONTROL パッケージマネージャー].
1. 次の場所にあるパッケージをアップロードしてインストールします。 [disable_indexingbinarytextraction-10.zip](assets/disable_indexingbinarytextextraction-10.zip).

### guessTotal {#guess-total}

大きな結果セットを生成するクエリを作成するときは、クエリ実行時のメモリ消費を抑えるために `guessTotal` パラメーターを使用してください。

## 既知の問題 {#known-issues}

### サイズの大きなファイル {#large-files}

サイズの大きいファイルに関する既知の問題は、 [!DNL Experience Manager]. ファイルのサイズが 2 GB 以上に到達すると、コールドスタンバイの同期でメモリ不足のエラーが発生することがあります。場合によっては、スタンバイの同期が実行されなくなります。また、プライマリインスタンスのクラッシュを引き起こすこともあります。このシナリオは、 [!DNL Experience Manager] は 2 GB を超え、コンテンツパッケージを含みます。

同様に、共有 S3 データストアを使用している間にファイルのサイズが 2 GB に達した場合、ファイルがキャッシュからファイルシステムに完全に保持されるまでに時間がかかる場合があります。 結果として、バイナリなしのレプリケーションを使用しているとき、レプリケーションが完了する前にバイナリデータが保持されていなかった可能性があります。この状況は、特にデータの可用性が重要な場合に問題を引き起こす可能性があります。

## パフォーマンスのテスト {#performance-testing}

期間 [!DNL Experience Manager] 導入、ボトルネックを迅速に特定して解決できるパフォーマンステスト体制を確立します。 留意点は次のとおりです。

### ネットワークのテスト {#network-testing}

お客様からのネットワークのパフォーマンスに関するすべての懸念については、次のタスクを実行してください。

* お客様のネットワーク内からネットワークのパフォーマンスをテストする
* アドビのネットワーク内からネットワークのパフォーマンスをテストする。AMS ユーザーの場合、CSE を使用してアドビのネットワーク内からテストしてください。
* 別のアクセスポイントからネットワークのパフォーマンスをテストする
* ネットワークのベンチマークツールを使用する
* ディスパッチャーに対してテストする

### [!DNL Experience Manager] デプロイメントテスト {#aem-deployment-testing}

CPU の効率的な使用率と負荷分散により、待ち時間を最小限に抑え、高いスループットを実現するには、 [!DNL Experience Manager] 定期的にデプロイします。 具体的には、以下のようになります。

* に対して負荷テストを実行 [!DNL Experience Manager] デプロイメント。
* アップロードのパフォーマンスと UI の応答性を監視する.

## [!DNL Experience Manager Assets] パフォーマンスチェックリストとアセット管理タスクの影響 {#checklist}

* HTTPS を有効化して企業の HTTP トラフィックスニッファーに対応する.
* サイズの大きなアセットのアップロードには有線接続を使用する.
* Java 8 にデプロイする
* 最適な JVM パラメーターを設定する。
* ファイルシステムのデータストアまたは S3 データストアを設定します。
* サブアセットの生成を無効にします。 有効にした場合、AEMワークフローは複数ページのアセットの各ページに個別のアセットを作成します。 これらの各ページは、追加のディスク領域を消費し、バージョン管理と追加のワークフロー処理が必要な個々のアセットです。 別々のページが必要ない場合は、サブアセットの生成およびページの抽出アクティビティを無効にします。
* 一時的なワークフローを有効化する.
* Granite のワークフローキューを調整して同時に実行されるジョブ数を制限する.
* 設定 [!DNL ImageMagick] リソースの消費を制限する。
* 不要な手順を [!UICONTROL DAM アセットの更新] ワークフロー。
* ワークフローとバージョンのパージを設定する.
* 最新のサービスパックとホットフィックスでインデックスを最適化します。 その他のインデックスの最適化方法については、Adobeカスタマーサポートにお問い合わせください。
* guessTotal を使用してクエリのパフォーマンスを最適化する。
* 次を設定する場合： [!DNL Experience Manager] ファイルの内容からファイルの種類を検出するには、 **[!UICONTROL Day CQ DAM Mime Type Service]** 内 **[!UICONTROL AEM Web コンソール]**)、リソースを大量に消費するので、ピーク時以外の時間帯に多数のファイルを一括アップロードします。
