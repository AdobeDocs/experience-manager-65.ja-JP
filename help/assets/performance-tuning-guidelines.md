---
title: パフォーマンス調整 [!DNL Assets]。
description: ' [!DNL Experience Manager] 構成、ハードウェア、ソフトウェア、ネットワーク・コンポーネントの変更に関する提案とガイダンス。ボトルネックを解消し、 [!DNL Experience Manager Assets]のパフォーマンスを最適化します。'
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 10dae6e9f49e93d2f4923cee754c1d23d9d4b25e
workflow-type: tm+mt
source-wordcount: '2744'
ht-degree: 52%

---


<!-- TBD: Get reviewed by engineering. -->

# [!DNL Adobe Experience Manager Assets] 性能調整ガイド  {#assets-performance-tuning-guide}

[!DNL Experience Manager Assets]セットアップには、多数のハードウェア、ソフトウェア、およびネットワークコンポーネントが含まれています。 導入のシナリオによっては、パフォーマンス上のボトルネックを排除するために、ハードウェア、ソフトウェアおよびネットワークコンポーネントに対して特殊な設定変更が必要になる場合があります。

さらに、特定のハードウェアおよびソフトウェアの最適化ガイドラインを特定し、遵守することで、[!DNL Experience Manager Assets]導入環境がパフォーマンス、拡張性、信頼性に関する期待に応える確実な基盤を構築できます。

[!DNL Experience Manager Assets]のパフォーマンスが低いと、インタラクティブパフォーマンス、アセット処理、ダウンロード速度、その他の領域でのユーザーエクスペリエンスに影響を与える可能性があります。

パフォーマンスの最適化は、すべてのプロジェクトでターゲット指標を確立する前に実行する、基本的なタスクです。

ユーザーに影響を及ぼす前にパフォーマンス上の問題を検出して修正する必要がある主な領域は次のとおりです。

## プラットフォーム {#platform}

Experience Managerは数多くのプラットフォームでサポートされていますが、AdobeはLinuxとWindowsでネイティブツールの最大のサポートを見つけ、最適なパフォーマンスと実装の容易さに貢献しています。 [!DNL Experience Manager Assets]導入の高メモリ要件を満たす64ビットオペレーティングシステムを導入するのが理想的です。 Experience Manager導入の場合と同様に、可能な限りTarMKを実装する必要があります。 TarMK は単一のオーサーインスタンスを超えて拡張できませんが、パフォーマンスは MongoMK よりも優れています。TarMKオフロードインスタンスを追加して、[!DNL Experience Manager Assets]導入のワークフロー処理能力を高めることができます。

### 一時フォルダー{#temp-folder}

アセットのアップロード時間を改善するには、Javaの一時ディレクトリに高いパフォーマンスのストレージを使用します。 Linux および Windows の場合は、RAM ドライブまたは SSD を使用できます。クラウドベースの環境では、同等の高速ストレージタイプを使用できます。例えば、AmazonEC2では、[Ephemeral Drive](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html)ドライブを一時フォルダーに使用できます。

サーバーに十分なメモリがあるという前提で、RAM ドライブを設定します。Linux の場合、8GB RAM ドライブを作成するには、次のコマンドを実行します。

```shell
mkfs -q /dev/ram1 800000
 mkdir -p /mnt/aem-tmp
 mount /dev/ram1 /mnt/aem-tmp
 df -H | grep aem-tmp
```

Windows OSでは、サードパーティ製のドライバを使用してRAMドライブを作成するか、SSDなどの高パフォーマンスストレージを使用します。

高パフォーマンスの一時ボリュームの準備が整ったら、JVMパラメーター`-Djava.io.tmpdir`を設定します。 例えば、[!DNL Experience Manager]の`bin/start`スクリプト内の`CQ_JVM_OPTS`変数に次のJVMパラメーターを追加できます。

`-Djava.io.tmpdir=/mnt/aem-tmp`

## Java の設定 {#java-configuration}

### Java バージョン {#java-version}

Adobeでは、最適なパフォーマンスを得るために、Java 8に[!DNL Experience Manager Assets]を導入することをお勧めします。

<!-- TBD: Link to the latest official word around Java.
-->

### JVM パラメーター {#jvm-parameters}

次のJVMパラメーターを設定します。

* `-XX:+UseConcMarkSweepGC`
* `-Doak.queryLimitInMemory`=500000
* `-Doak.queryLimitReads`=100000
* `-Dupdate.limit`=250000
* `-Doak.fastQuerySize`=true

## データストアとメモリの設定 {#data-store-and-memory-configuration}

### ファイルデータストアの設定 {#file-data-store-configuration}

すべての[!DNL Experience Manager Assets]ユーザーには、データストアとセグメントストアを分けることをお勧めします。 また、`maxCachedBinarySize` パラメーターと `cacheSizeInMB` パラメーターを設定することでパフォーマンスを最大化するのに役立ちます。キャッシュに含めることができるように、`maxCachedBinarySize` を最小のファイルサイズに設定します。`cacheSizeInMB` 内のデータストアで使用するインメモリキャッシュのサイズを指定します。この値は合計ヒープサイズの 2～10％に設定することをお勧めします。ただし、負荷テストやパフォーマンステストが理想的な設定を決定するのに役立ちます。

### バッファーされる画像キャッシュの最大サイズの設定  {#configure-the-maximum-size-of-the-buffered-image-cache}

大量のアセットを[!DNL Adobe Experience Manager]にアップロードする場合、メモリ消費量が予期せぬ急増を生じさせ、OutOfMemoryErrorsでJVMが失敗するのを防ぐために、バッファされたイメージキャッシュの最大サイズを小さくします。 例えば、最大ヒープ（-`Xmx` パラメーター）が 5 GB のシステムで、Oak BlobCache が 1 GB、文書キャッシュが 2 GB に設定されているとします。このときに、バッファーされるキャッシュが最大 1.25 GB のメモリを使用した場合、予期しないスパイクに使用できるメモリは 0.75 GB のみとなります。

バッファーされるキャッシュサイズは OSGi Web コンソールで設定します。`https://host:port/system/console/configMgr/com.day.cq.dam.core.impl.cache.CQBufferedImageCache` で、プロパティ `cq.dam.image.cache.max.memory` をバイト単位で指定します。例えば、1073741824 は 1 GB です（1024 x 1024 x 1024 = 1 GB）。

Experience Manager6.1 SP1から、`sling:osgiConfig`ノードを使用してこのプロパティを設定する場合は、データタイプをLongに設定する必要があります。 詳しくは、[CQBufferedImageCache がアセットのアップロード中にヒープを消費する](https://helpx.adobe.com/jp/experience-manager/kb/cqbufferedimagecache-consumes-heap-during-asset-uploads.html)を参照してください。

### 共有データストア  {#shared-data-stores}

S3 または共有ファイルデータストアの実装は、ディスク領域の節約と大規模な実装におけるネットワークスループットの向上に役立ちます。共有データストアの使用の長所と短所について詳しくは、[アセットサイズ変更ガイド](/help/assets/assets-sizing-guide.md)を参照してください。

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

多くの企業には HTTP トラフィックをスニッフィングするファイアウォールがあり、ファイルのアップロードに干渉しファイルを破損するので、HTTPS を有効にすることをお勧めします。サイズの大きなファイルのアップロードについては、Wi-Fi ネットワークでは簡単に飽和するおそれがあるので、必ず有線でネットワークに接続してください。ネットワークのボトルネックの特定に関するガイドラインについては、[アセットサイズ設定ガイド](/help/assets/assets-sizing-guide.md)を参照してください。 ネットワークトポロジを分析してネットワークのパフォーマンスを評価する方法については、[アセットネットワークに関する考慮事項](/help/assets/assets-network-considerations.md)を参照してください。

主に、ネットワーク最適化戦略は、使用可能な帯域幅の量と[!DNL Experience Manager]インスタンスの負荷に依存します。 ファイアウォールやプロキシなどの一般的な設定オプションは、ネットワークのパフォーマンスの改善に役立ちます。留意点は次のとおりです。

* インスタンスのタイプ（小、中、大）に応じて、Experience Managerインスタンスに十分なネットワーク帯域幅があることを確認します。 [!DNL Experience Manager]がAWSでホストされている場合は、十分な帯域幅の割り当てが特に重要です。
* [!DNL Experience Manager]インスタンスがAWSでホストされている場合は、用途の広いスケーリングポリシーを利用できるのでメリットが得られます。 高い負荷が予想される場合は、インスタンスのサイズを大きくします。負荷が標準的または低い場合は、インスタンスのサイズを小さくします。
* HTTPS：ユーザーの多くは HTTP トラフィックをスニッフィングするファイアウォールを装備しており、ファイルのアップロード操作に干渉しファイルを破損することもあります。
* サイズの大きなファイルのアップロード：必ず有線でネットワークに接続してください（Wi-Fi 接続は簡単に飽和するおそれがあります）。

## ワークフロー {#workflows}

### 一時的なワークフロー {#transient-workflows}

可能であれば、[!UICONTROL DAM Update Asset]ワークフローを「一時的」に設定します。 この設定にすると、ワークフローが通常のトラッキングやアーカイブ処理をパススルーする必要がなくなるので、ワークフローの処理に必要なオーバーヘッドが大幅に削減されます。

1. `https://[aem_server]:[port]/miscadmin`の[!DNL Experience Manager]デプロイメントの`/miscadmin`に移動します。

1. **[!UICONTROL ツール]**/**[!UICONTROL ワークフロー]**/**[!UICONTROL モデル]**/**[!UICONTROL dam]**&#x200B;を展開します。

1. **[!UICONTROL DAM Update Asset]**&#x200B;を開きます。 フローティングツールパネルで、「**[!UICONTROL ページ]**」タブに切り替えて「**[!UICONTROL ページプロパティ]**」をクリックします。

1. 「一時的なワークフロー&#x200B;****」を選択し、「**[!UICONTROL OK]**」をクリックします。

   >[!NOTE]
   >
   >一部の機能は一時的なワークフローをサポートしません。[!DNL Assets]デプロイメントでこれらの機能が必要な場合は、一過性のワークフローを設定しないでください。

一過性のワークフローを使用できない場合は、定期的にワークフローの削除を実行して、アーカイブされた[!UICONTROL DAM Update Asset]ワークフローを削除し、システムのパフォーマンスが低下しないようにします。

通常、パージワークフローは週単位で実行します。 ただし、大規模なアセット取り込みの際など、リソースを大量に消費するシナリオでは、より頻繁にアセットを実行できます。

ワークフローのパージを設定するには、OSGi コンソールで新しい Adobe Granite のワークフローのパージ設定を追加します。次に、ワークフローを週次メンテナンスウィンドウの一部としてスケジュールを設定します。

パージの実行時間が長すぎる場合、タイムアウトします。このため、ワークフローの数が多すぎることが原因でパージワークフローが終わらない状況を避けるために、パージジョブが確実に終わるようにする必要があります。

例えば、多数の非一過性ワークフロー（ワークフローインスタンスノードを作成）を実行した後、[ACS AEM Commons Workflow Remover](https://adobe-consulting-services.github.io/acs-aem-commons/features/workflow-remover.html)をアドホックに実行できます。 これにより、冗長および完了したワークフローのインスタンスが即座に削除されるので、Adobe Granite のワークフローのパージスケジューラーが実行されるのを待つ必要がありません。

### 並列ジョブの最大数  {#maximum-parallel-jobs}

デフォルトでは、[!DNL Experience Manager]は、サーバー上のプロセッサ数と同じ数の並列ジョブを実行します。 この設定の問題は、負荷が大きい時間帯に、すべてのプロセッサーが[!UICONTROL DAM Update Asset]ワークフローに占有され、UIの応答性が低下し、[!DNL Experience Manager]がサーバーのパフォーマンスと安定性を保護する他のプロセスを実行できないことです。 次の手順を実行して、この値をサーバーで使用できるプロセッサーの半分の値にすることをお勧めします。

1. [!DNL Experience Manager]作成者で`https://[aem_server]:[port]/system/console/slingevent`にアクセスします。

1. **[!UICONTROL Granite Transient Workflow Queue]**&#x200B;のように、実装に関連する各ワークフローキューで「&lt;a0/>編集&#x200B;]**」をクリックします。**[!UICONTROL 

1. **[!UICONTROL Maximum Parallel Jobs]**&#x200B;の値を更新し、**[!UICONTROL Save]**&#x200B;をクリックします。

まずは、キューを使用できるプロセッサーの半分に設定してください。ただし、場合によっては最大のスループットを得るためにこの値をお使いの環境に合わせて増減させる必要があります。一時的および一時的でないワークフローには別個のキューが用意されているほか、外部ワークフローなどその他の処理も存在します。プロセッサーの 50％に設定された複数のキューが同時にアクティブになると、システムはすぐにオーバーロードします。頻繁に使用されるキューは、ユーザーの実装により大きく異なります。このため、サーバーの安定性を損なうことなく効率を最大化するには、これらを慎重に設定する必要が生じる場合があります。

### DAM アセットの更新設定 {#dam-update-asset-configuration}

[!UICONTROL DAM Update Asset]ワークフローには、Dynamic MediaPTIFFの生成や[!DNL Adobe InDesign Server]統合など、タスク用に構成されたすべての手順が含まれています。 ただし、大多数のユーザーにとってこれらの手順のうちのいくつかは不要です。Adobeでは、[!UICONTROL DAM Update Asset]ワークフローモデルのカスタムコピーを作成し、不要な手順を削除することをお勧めします。 この場合、[!UICONTROL DAM Update Asset]のランチャーを更新して、新しいモデルを指定します。

[!UICONTROL DAM Update Asset]ワークフローを大幅に実行すると、ファイルデータストアのサイズを大幅に拡大できます。 アドビが実施した実験の結果によると、8 時間以内に約 5,500 のワークフローを実行した場合、データストアのサイズが約 400 GB 増加する可能性があります。

これは一時的な増加であり、データストアのガベージコレクションタスクを実行すると、データストアは元のサイズに戻ります。

通常、データストアのガベージコレクションタスクは、スケジュールされた他のメンテナンスタスクと共に毎週実行されます。

ディスク領域が限られていて、[!UICONTROL DAM Update Asset]ワークフローを集中的に実行する場合は、ガベージコレクションタスクのスケジュールをより頻繁に設定することを検討してください。

#### 実行時のレンディションの生成 {#runtime-rendition-generation}

お客様は Web サイトやビジネスパートナーへの配布に様々なサイズや形式の画像を使用します。各レンディションによりリポジトリ内のアセットの足跡が増加するので、この機能は適切なタイミングで使用することをお勧めします。画像の処理と保存に必要なリソースを減らすために、これらの画像を取り込み中にではなく実行時にレンディションとして生成できます。

多くの Sites のお客様はリクエストされた時点で画像のサイズを変更および切り抜く画像サーブレットを実装しています。これにより、パブリッシュインスタンスにさらに負荷がかけられます。ただし、これらの画像をキャッシュできる限り、問題を減らすことができます。

別のアプローチは、Dynamic Mediaの技術を使って完全な画像操作を手渡すことです。 さらに、[!DNL Experience Manager]インフラストラクチャのレンディション生成の責任を引き継ぐだけでなく、公開層全体を引き継ぐBrand Portalを展開できます。

#### ImageMagick {#imagemagick}

[!UICONTROL DAM Update Asset]ワークフローをカスタマイズしてImageMagickを使用したレンディションを生成する場合、Adobeでは`/etc/ImageMagick/`の`policy.xml`ファイルを変更することを推奨します。 デフォルトでは、ImageMagick は OS ボリュームで使用できるディスク領域と空きメモリをすべて使用します。`policy.xml`の`policymap`セクション内で次の設定変更を行い、これらのリソースを制限します。

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

さらに、`configure.xml`ファイル内のImageMagickの一時フォルダーのパスを、十分な容量とIOPSを持つ環境パーティションに設定します（または、ディスク変数`MAGIC_TEMPORARY_PATH`を設定します）。

>[!CAUTION]
>
>使用可能なすべてのディスク領域を ImageMagick で使用する場合、設定を誤るとサーバーの動作が不安定になるおそれがあります。ImageMagickを使用して大きなファイルを処理するために必要なポリシーの変更は、[!DNL Experience Manager]のパフォーマンスに影響する場合があります。 詳しくは、[ImageMagick のインストールと設定](/help/assets/best-practices-for-imagemagick.md)を参照してください。

>[!NOTE]
>
>ImageMagick `policy.xml`ファイルと`configure.xml`ファイルは、`/etc/ImageMagick/`ではなく`/usr/lib64/ImageMagick-&#42;/config/`で入手できます。設定ファイルの場所については、[ImageMagickドキュメント](https://www.imagemagick.org/script/resources.php)を参照してください。

Adobe Managed Services(AMS)で[!DNL Experience Manager]を使用している場合は、大量のPSDファイルまたはPSBファイルを処理する予定の場合は、Adobeカスタマーケアにお問い合わせください。 AMS導入のためのこれらのベストプラクティスを実装し、Adobe独自の形式に対して可能な限り最適なツールとモデルを選択するには、Adobeカスタマーケアの担当者にご相談ください。 [!DNL Experience Manager] は、30000 x 23000ピクセルを超える高解像度PSBファイルを処理できない場合があります。

### XMP の書き戻し {#xmp-writeback}

XMPの書き戻しでは、メタデータが[!DNL Experience Manager]で変更されると元のアセットが更新され、次の結果になります。

* アセット自体が変更されます
* アセットのバージョンが作成されます
* [!UICONTROL 「DAM アセットの更新」がアセットに対して実行されます]

上記の結果により、大量のリソースが消費されます。このため、この機能が必要でない場合は、[XMP の書き戻しを無効化する](https://helpx.adobe.com/jp/experience-manager/kb/disable-xmp-writeback.html)ことをお勧めします。

ワークフロー実行フラグがチェックされている場合、大量のメタデータを読み込むと、リソースを集中的に使用する XMP 書き戻しアクティビティが発生するおそれがあります。このような読み込みは、他のユーザーのパフォーマンスに影響しないように、サーバー使用率が低いときに計画します。

## レプリケーション {#replication}

Sites の実装などで、アセットを多数のパブリッシュインスタンスにレプリケートするときは、チェーンレプリケーションを使用することをお勧めします。この場合、オーサーインスタンスが単一のパブリッシュインスタンスにレプリケートし、そのパブリッシュインスタンスが代わりに他のパブリッシュインスタンスにレプリケートすることで、オーサーインスタンスを解放します。

### チェーンレプリケーションの設定  {#configure-chain-replication}

1. レプリケーションのチェーン先に使用するパブリッシュインスタンスを選択します。
1. そのパブリッシュインスタンスで、他のパブリッシュインスタンスを指すレプリケーションエージェントを追加します。
1. 追加した各レプリケーションエージェントで、「トリガー」タブの「受信時」を有効にします。

>[!NOTE]
>
>アセットの自動アクティベートはお勧めしません。ただし、必要な場合は、ワークフローの最後の手順（通常は「DAM アセットの更新」）で実行することをお勧めします。

## 検索インデックス {#search-indexes}

システムインデックスの更新が含まれている場合が多いので、最新のサービスパックやパフォーマンス関連のホットフィックスを実装してください。インデックスの最適化については、[パフォーマンス調整のヒント](https://helpx.adobe.com/jp/experience-manager/kb/performance-tuning-tips.html)を参照してください。

頻繁に実行するクエリにカスタムインデックスを作成します。詳しくは、[スロークエリの分析手法（英語）](https://aemfaq.blogspot.com/2014/08/oak-query-log-file-analyzer-tool.html)と[カスタムインデックスの作成](/help/sites-deploying/queries-and-indexing.md)を参照してください。クエリとインデックスのベストプラクティスに関するその他の洞察については、[クエリとインデックスのベストプラクティス](/help/sites-deploying/best-practices-for-queries-and-indexing.md)を参照してください。

### Lucene Index の設定 {#lucene-index-configurations}

[!DNL Experience Manager Assets]のパフォーマンスを向上させるため、Oakインデックスの構成で最適化を行うことができます。 インデックス構成を更新して再インデックス作成時間を改善します。

1. CRXDe `/crx/de/index.jsp`を開き、管理ユーザーとしてログインします。
1. `/oak:index/lucene`を参照します。
1. 値追加`/var`、`/etc/workflow/instances`、および`/etc/replication`を持つ`String[]`プロパティ`excludedPaths`。
1. `/oak:index/damAssetLucene`を参照します。 値追加`/content/dam`の`String[]`プロパティ`includedPaths`。 変更を保存します。

例えば、PDFドキュメント内のテキストを検索する場合など、アセットをフルテキスト検索する必要がない場合は、これを無効にします。 フルテキストインデックスを無効にすると、インデックスのパフォーマンスが向上します。 [!DNL Apache Lucene]テキスト抽出を無効にするには、次の手順に従います。

1. [!DNL Experience Manager]インターフェイスで、[!UICONTROL パッケージマネージャー]にアクセスします。
1. [disable_indexingbinarytextraction-10.zip](assets/disable_indexingbinarytextextraction-10.zip)で入手可能なパッケージをアップロードしてインストールします。

### guessTotal {#guess-total}

大きな結果セットを生成するクエリを作成するときは、クエリ実行時のメモリ消費を抑えるために `guessTotal` パラメーターを使用してください。

## 既知の問題 {#known-issues}

### サイズの大きなファイル {#large-files}

[!DNL Experience Manager]には大きなファイルに関する2つの主な既知の問題があります。 ファイルのサイズが 2 GB 以上に到達すると、コールドスタンバイの同期でメモリ不足のエラーが発生することがあります。場合によっては、スタンバイの同期が実行されなくなります。また、プライマリインスタンスのクラッシュを引き起こすこともあります。このシナリオは、[!DNL Experience Manager]内の2 GBを超えるファイル（コンテンツパッケージを含む）に適用されます。

同様に、共有S3データストアを使用している間にファイルのサイズが2 GBに達した場合は、ファイルがキャッシュからファイルシステムに完全に保持されるまでに時間がかかる場合があります。 結果として、バイナリなしのレプリケーションを使用しているとき、レプリケーションが完了する前にバイナリデータが保持されていなかった可能性があります。この状況は、特にデータの可用性が重要な場合に問題を引き起こす可能性があります。

## パフォーマンスのテスト {#performance-testing}

[!DNL Experience Manager]導入のたびに、ボトルネックを迅速に特定し解決できるパフォーマンステスト体制を確立します。 留意点は次のとおりです。

### ネットワークのテスト  {#network-testing}

お客様からのネットワークのパフォーマンスに関するすべての懸念については、次のタスクを実行してください。

* お客様のネットワーク内からネットワークのパフォーマンスをテストする
* アドビのネットワーク内からネットワークのパフォーマンスをテストする：AMS ユーザーの場合、CSE を使用してアドビのネットワーク内からテストしてください。
* 別のアクセスポイントからネットワークのパフォーマンスをテストする
* ネットワークのベンチマークツールを使用する
* ディスパッチャーに対してテストする

### [!DNL Experience Manager] 導入テスト  {#aem-deployment-testing}

CPUの効率的な使用率と負荷分散により、待ち時間を最小限に抑え、高いスループットを実現するには、[!DNL Experience Manager]導入環境のパフォーマンスを定期的に監視します。 具体的には、次のことを実行します。

* [!DNL Experience Manager]展開に対してロードテストを実行します。
* アップロードのパフォーマンスと UI の応答性を監視する.

## [!DNL Experience Manager Assets] 資産管理タスクの性能チェックリストと影響  {#checklist}

* HTTPS を有効化して企業の HTTP トラフィックスニッファーに対応する.
* サイズの大きなアセットのアップロードには有線接続を使用する.
* Java 8 にデプロイする
* 最適な JVM パラメーターを設定する。
* ファイルシステムのDataStoreまたはS3データストアを構成します。
* サブアセットの生成を無効にします。 この機能が有効な場合、AEMワークフローは、複数ページのアセット内の各ページに対して個別のアセットを作成します。 これらの各ページは、追加のディスク領域を消費し、バージョン管理や追加のワークフロー処理が必要な個々のアセットです。 別々のページが必要ない場合は、サブアセットの生成とページ抽出のアクティビティを無効にします。
* 一時的なワークフローを有効化する.
* Granite のワークフローキューを調整して同時に実行されるジョブ数を制限する.
* [!DNL ImageMagick]を設定して、リソースの消費を制限します。
* [!UICONTROL DAM Update Asset]ワークフローから不要な手順を削除します。
* ワークフローとバージョンのパージを設定する.
* 最新のサービスパックとホットフィックスでインデックスを最適化する。利用可能なインデックスのその他の最適化については、Adobeカスタマーケアにお問い合わせください。
* guessTotal を使用してクエリのパフォーマンスを最適化する。
* ファイルの内容からファイルの種類を検出するように[!DNL Experience Manager]を設定した場合(**[!UICONTROL AEM Webコンソール]**&#x200B;で&#x200B;**[!UICONTROL Day CQ DAM MIME Type Service]**&#x200B;を有効にして)、リソースを大量に消費するため、多くのファイルを一括アップロードします。
