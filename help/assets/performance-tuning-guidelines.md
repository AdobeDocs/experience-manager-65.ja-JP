---
title: パフォーマンスチューニング [!DNL Assets].
description: ' [!DNL Experience Manager] 構成、ハードウェア、ソフトウェア、ネットワークコンポーネントの変更により、ボトルネックを解消し、パフォーマンスを最適化 [!DNL Experience Manager Assets]に関する提案とガイダンス。'
contentOwner: AG
mini-toc-levels: 1
role: Architect, Admin
feature: Asset Management
exl-id: 1d9388de-f601-42bf-885b-6a7c3236b97e
source-git-commit: e3caa3e3067cf5e29cfcdf4286047eb346aefa23
workflow-type: tm+mt
source-wordcount: '2753'
ht-degree: 99%

---

<!-- TBD: Get reviewed by engineering. -->

# [!DNL Adobe Experience Manager Assets] パフォーマンスチューニングガイド {#assets-performance-tuning-guide}

[!DNL Experience Manager Assets] のセットアップには、数多くのハードウェア、ソフトウェアおよびネットワークコンポーネントが含まれています。導入のシナリオによっては、パフォーマンス上のボトルネックを排除するために、ハードウェア、ソフトウェアおよびネットワークコンポーネントに対して特殊な設定変更が必要になる場合があります。

また、特定のハードウェアおよびソフトウェアを最適化するガイドラインを識別してそれに従うことで優良な基盤を構築し、[!DNL Experience Manager Assets] の導入によりパフォーマンス、スケーラビリティおよび信頼性の面で期待通りの結果を得られます。

[!DNL Experience Manager Assets] のパフォーマンスが低下すると、インタラクティブパフォーマンス、アセット処理、ダウンロード速度などの領域におけるユーザーエクスペリエンスに影響します。

パフォーマンスの最適化は、すべてのプロジェクトでターゲット指標を確立する前に実行する、基本的なタスクです。

ユーザーに影響を及ぼす前にパフォーマンス上の問題を検出して修正する必要がある主な領域は次のとおりです。

## Platform {#platform}

Experience Manager は数々のプラットフォームでサポートされていますが、Linux や Windows ではパフォーマンスを最適化し実装を簡単にする優れたネイティブツールがサポートされています。[!DNL Experience Manager Assets] のデプロイメントでは、高いメモリ要件を満たすために 64 ビットのオペレーティングシステムを採用するのが理想です。あらゆる Experience Manager のデプロイメントにおいて、可能である場合は TarMK を実装してください。TarMK は単一のオーサーインスタンスを超えて拡張できませんが、パフォーマンスは MongoMK よりも優れています。TarMK オフロードインスタンスを追加すると、[!DNL Experience Manager Assets] のデプロイメントのワークフローの処理能力を高めることができます。

### 一時フォルダー {#temp-folder}

アセットのアップロード時間を短縮するには、Java 一時ディレクトリに高性能ストレージを使用します。Linux および Windows の場合は、RAM ドライブまたは SSD を使用できます。クラウドベースの環境では、同等の高速ストレージタイプを使用できます。例えば Amazon EC2 では、「[エフェメラルドライブ](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html)」を一時フォルダーに使用できます。

サーバーに十分なメモリがあるという前提で、RAM ドライブを設定します。Linux の場合、8GB RAM ドライブを作成するには、次のコマンドを実行します。

```shell
mkfs -q /dev/ram1 800000
 mkdir -p /mnt/aem-tmp
 mount /dev/ram1 /mnt/aem-tmp
 df -H | grep aem-tmp
```

Windows OS の場合、サードパーティ製ドライバーを使用して RAM ドライブを作成するか、SSD などの高性能ストレージを使用する必要があります。

高性能一時ボリュームの準備ができたら、JVM パラメーター `-Djava.io.tmpdir` を設定します。例えば、[!DNL Experience Manager] の `bin/start` スクリプト内の `CQ_JVM_OPTS` 変数の下に次の JVM パラメーターを追加できます。

`-Djava.io.tmpdir=/mnt/aem-tmp`

## Java の設定 {#java-configuration}

### Java バージョン {#java-version}

アドビでは、最適なパフォーマンスを得られるよう、[!DNL Experience Manager Assets] を Java 8 にデプロイすることをお勧めします。

<!-- TBD: Link to the latest official word around Java.
-->

### JVM パラメーター {#jvm-parameters}

以下の JVM パラメーターを設定します。

* `-XX:+UseConcMarkSweepGC`
* `-Doak.queryLimitInMemory`=500000
* `-Doak.queryLimitReads`=100000
* `-Dupdate.limit`=250000
* `-Doak.fastQuerySize`=true

## データストアとメモリの設定 {#data-store-and-memory-configuration}

### ファイルデータストアの設定 {#file-data-store-configuration}

すべての [!DNL Experience Manager Assets] のユーザーに、データストアをセグメントストアから分離することをお勧めします。また、`maxCachedBinarySize` パラメーターと `cacheSizeInMB` パラメーターを設定することでパフォーマンスを最大化するのに役立ちます。キャッシュに含めることができるように、`maxCachedBinarySize` を最小のファイルサイズに設定します。`cacheSizeInMB` 内のデータストアで使用するインメモリキャッシュのサイズを指定します。この値は合計ヒープサイズの 2～10％に設定することをお勧めします。ただし、負荷テストやパフォーマンステストが理想的な設定を決定するのに役立ちます。

### バッファーされる画像キャッシュの最大サイズの設定 {#configure-the-maximum-size-of-the-buffered-image-cache}

多数のアセットを [!DNL Adobe Experience Manager] にアップロードするときは、メモリ消費の予期しないスパイクに対応するために、また OutOfMemoryErrors による JVM エラーを避けるために、バッファーされる画像キャッシュの最大サイズを減らしてください。例えば、最大ヒープ（-`Xmx` パラメーター）が 5 GB のシステムで、Oak BlobCache が 1 GB、文書キャッシュが 2 GB に設定されているとします。このときに、バッファーされるキャッシュが最大 1.25 GB のメモリを使用した場合、予期しないスパイクに使用できるメモリは 0.75 GB のみとなります。

バッファーされるキャッシュサイズは OSGi Web コンソールで設定します。`https://host:port/system/console/configMgr/com.day.cq.dam.core.impl.cache.CQBufferedImageCache` で、プロパティ `cq.dam.image.cache.max.memory` をバイト単位で指定します。例えば、1073741824 は 1 GB です（1024 x 1024 x 1024 = 1 GB）。

Experience Manager 6.1 SP1 以降で `sling:osgiConfig` ノードを使用してこのプロパティを設定する場合は、データタイプを必ず Long にします。詳しくは、[CQBufferedImageCache がアセットのアップロード中にヒープを消費する](https://helpx.adobe.com/jp/experience-manager/kb/cqbufferedimagecache-consumes-heap-during-asset-uploads.html)を参照してください。

### 共有データストア {#shared-data-stores}

S3 または共有ファイルデータストアの実装は、ディスク領域の節約と大規模な実装におけるネットワークスループットの向上に役立ちます。共有データベースの使用に関するメリットとデメリットについて詳しくは、[Assets サイジングガイド](/help/assets/assets-sizing-guide.md)を参照してください。

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

多くの企業には HTTP トラフィックをスニッフィングするファイアウォールがあり、ファイルのアップロードに干渉しファイルを破損するので、HTTPS を有効にすることをお勧めします。サイズの大きなファイルのアップロードについては、Wi-Fi ネットワークでは簡単に飽和するおそれがあるので、必ず有線でネットワークに接続してください。ネットワークのボトルネックを特定するガイドラインについては、[Assets サイジングガイド](/help/assets/assets-sizing-guide.md)を参照してください。ネットワークトポロジを分析してネットワークのパフォーマンスを評価するには、[Assets のネットワークに関する考慮事項](/help/assets/assets-network-considerations.md)を参照してください。

第一に、ネットワークの最適化戦略は使用できる帯域幅や、[!DNL Experience Manager] インスタンスに対する負荷によって変わります。ファイアウォールやプロキシなどの一般的な設定オプションは、ネットワークのパフォーマンスの改善に役立ちます。留意点は次のとおりです。

* インスタンスタイプ（小、中、大）によって、Experience Manager インスタンスに十分なネットワーク帯域幅があることを確認します。[!DNL Experience Manager] で AWS にホストされている場合、帯域幅が適切に分散されていることが特に重要です。
* [!DNL Experience Manager] インスタンスが AWS にホストされている場合、広い用途に対応するスケールポリシーがあると便利です。高い負荷が予想される場合は、インスタンスのサイズを大きくします。負荷が標準的または低い場合は、インスタンスのサイズを小さくします。
* HTTPS：ユーザーの多くは HTTP トラフィックをスニッフィングするファイアウォールを装備しており、ファイルのアップロード操作に干渉しファイルを破損することもあります。
* サイズの大きなファイルのアップロード：必ず有線でネットワークに接続してください（Wi-Fi 接続は簡単に飽和するおそれがあります）。

## ワークフロー {#workflows}

### 一時的なワークフロー {#transient-workflows}

可能な限り、「[!UICONTROL DAM アセットの更新]」ワークフローを「一時的」に設定します。この設定にすると、ワークフローが通常のトラッキングやアーカイブ処理をパススルーする必要がなくなるので、ワークフローの処理に必要なオーバーヘッドが大幅に削減されます。

1. `https://[aem_server]:[port]/miscadmin` の [!DNL Experience Manager] のデプロイメント内の `/miscadmin` に移動します。

1. **[!UICONTROL ツール]**／**[!UICONTROL ワークフロー]**／**[!UICONTROL モデル]**／**[!UICONTROL dam]** の順に展開します。

1. 「**[!UICONTROL DAM アセットの更新]**」を開きます。フローティングツールパネルで、「**[!UICONTROL ページ]**」タブに切り替えて「**[!UICONTROL ページプロパティ]**」をクリックします。

1. 「**[!UICONTROL 一時的なワークフロー]**」を選択し、「**[!UICONTROL OK]**」をクリックします。

   >[!NOTE]
   >
   >一部の機能は一時的なワークフローをサポートしません。[!DNL Assets] のデプロイメントにこれらの機能が必要な場合は、一時的なワークフローを設定しないでください。

一時的なワークフローを使用できない場合は、定期的にパージされるワークフローを実行してアーカイブされた「[!UICONTROL DAM アセットの更新]」ワークフローを削除し、システムのパフォーマンスが低下しないようにします。

通常、パージワークフローは毎週実行します。ただし、大規模なアセットの取り込み中など、多くのリソースを使用するシナリオではより頻繁に実行できます。

ワークフローのパージを設定するには、OSGi コンソールで新しい Adobe Granite のワークフローのパージ設定を追加します。次に、ワークフローを週次メンテナンスウィンドウの一部としてスケジュールを設定します。

パージの実行時間が長すぎる場合、タイムアウトします。このため、ワークフローの数が多すぎることが原因でパージワークフローが終わらない状況を避けるために、パージジョブが確実に終わるようにする必要があります。

例えば、一時的でない多数のワークフロー（ワークフローのインスタンスノードを作成する）を実行した後に、[ACS AEM Commons Workflow Remover](https://adobe-consulting-services.github.io/acs-aem-commons/features/workflow-remover.html) をアドホックベースで実行できます。これにより、冗長および完了したワークフローのインスタンスが即座に削除されるので、Adobe Granite のワークフローのパージスケジューラーが実行されるのを待つ必要がありません。

### 並列ジョブの最大数 {#maximum-parallel-jobs}

デフォルトでは、[!DNL Experience Manager] は最大でサーバー上のプロセッサーと同じ数の並列ジョブを実行できます。この設定の問題点は、多くの負荷がかかる期間にはすべてのプロセッサーが「[!UICONTROL DAM アセットの更新]」ワークフローに占有されるので、UI の応答が遅くなり、[!DNL Experience Manager] がサーバーのパフォーマンスや安定性を保護するその他の処理を実行できなくなる点です。次の手順を実行して、この値をサーバーで使用できるプロセッサーの半分の値にすることをお勧めします。

1. [!DNL Experience Manager] オーサー環境に移動し、`https://[aem_server]:[port]/system/console/slingevent` にアクセスします。

1. 実装に関連する各ワークフローキュー（**[!UICONTROL Granite の一時的なワークフローキュー]** など）で「**[!UICONTROL 編集]**」をクリックします。

1. **[!UICONTROL 並列ジョブの最大数]**&#x200B;の値を更新し、「**[!UICONTROL 保存]**」をクリックします。

まずは、キューを使用できるプロセッサーの半分に設定してください。ただし、場合によっては最大のスループットを得るためにこの値をお使いの環境に合わせて増減させる必要があります。一時的および一時的でないワークフローには別個のキューが用意されているほか、外部ワークフローなどその他の処理も存在します。プロセッサーの 50％に設定された複数のキューが同時にアクティブになると、システムはすぐにオーバーロードします。頻繁に使用されるキューは、ユーザーの実装により大きく異なります。このため、サーバーの安定性を損なうことなく効率を最大化するには、これらを慎重に設定する必要が生じる場合があります。

### DAM アセットの更新設定 {#dam-update-asset-configuration}

「[!UICONTROL DAM アセットの更新]」ワークフローには、 Dynamic Media PTIFF の生成や [!DNL Adobe InDesign Server] の統合など、タスク向けに設定された一連の手順がすべて含まれています。ただし、大多数のユーザーにとってこれらの手順のうちのいくつかは不要です。アドビでは「[!UICONTROL DAM アセットの更新]」ワークフローモデルのカスタムコピーを作成し、不要な手順はすべて削除することをお勧めします。この場合、[!UICONTROL DAM アセットの更新]のランチャーを更新して新しいモデルを参照するようにします。

[!UICONTROL DAM アセットの更新]ワークフローを集中的に実行すると、ファイルデータストアのサイズが急激に増加する可能性があります。アドビが実施した実験の結果によると、8 時間以内に約 5,500 のワークフローを実行した場合、データストアのサイズが約 400 GB 増加する可能性があります。

これは一時的な増加であり、データストアのガベージコレクションタスクを実行すると、データストアは元のサイズに戻ります。

通常、データストアのガベージコレクションタスクは、スケジュールされた他のメンテナンスタスクと共に毎週実行されます。

ディスク領域が限られている場合に、[!UICONTROL DAM アセットの更新]ワークフローを集中的に実行する際は、ガベージコレクションタスクの実行頻度を増やすことを検討してください。

#### 実行時のレンディションの生成 {#runtime-rendition-generation}

お客様は Web サイトやビジネスパートナーへの配布に様々なサイズや形式の画像を使用します。各レンディションによりリポジトリ内のアセットの足跡が増加するので、この機能は適切なタイミングで使用することをお勧めします。画像の処理と保存に必要なリソースを減らすために、これらの画像を取り込み中にではなく実行時にレンディションとして生成できます。

多くの Sites のお客様はリクエストされた時点で画像のサイズを変更および切り抜く画像サーブレットを実装しています。これにより、パブリッシュインスタンスにさらに負荷がかけられます。ただし、これらの画像をキャッシュできる限り、問題を減らすことができます。

別のアプローチは、 Dynamic Media テクノロジーを使用して画像の操作を完全にハンドオフすることです。さらに、Brand Portal もデプロイできます。Brand Portal は、[!DNL Experience Manager] インフラストラクチャからだけでなく、パブリッシュ層全体からのレンディション生成も受け継ぎます。

#### ImageMagick {#imagemagick}

「[!UICONTROL DAM アセットの更新]」ワークフローを ImageMagick を使用してレンディションを生成するようにカスタマイズした場合、`/etc/ImageMagick/` にある `policy.xml` ファイルを変更することをお勧めします。デフォルトでは、ImageMagick は OS ボリュームで使用できるディスク領域と空きメモリをすべて使用します。これらのリソースを制限するには、`policy.xml` の `policymap` セクション内で次のように設定を変更します。

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

さらに、`configure.xml` ファイルにある ImageMagick の一時フォルダーのパス（または環境変数 `MAGICK_TEMPORARY_PATH`）を、十分な空き領域と IOPS があるディスクパーティションに設定します。

>[!CAUTION]
>
>使用可能なすべてのディスク領域を ImageMagick で使用する場合、設定を誤るとサーバーの動作が不安定になるおそれがあります。大きなファイルを処理するために必要なポリシーを ImageMagick を使用して変更すると、[!DNL Experience Manager] のパフォーマンスに影響する可能性があります。詳しくは、[ImageMagick のインストールと設定](/help/assets/best-practices-for-imagemagick.md)を参照してください。

>[!NOTE]
>
>ImageMagick `policy.xml` および `configure.xml` ファイルは `/usr/lib64/ImageMagick-&#42;/config/` で `/etc/ImageMagick/` の代わりに利用できます。設定ファイルの場所については、[ImageMagick のドキュメント](https://www.imagemagick.org/script/resources.php) を参照してください。

Adobe Managed Services（AMS）で [!DNL Experience Manager] を使用しており、大きな PSD ファイルまたは PSB ファイルを大量に処理する予定がある場合は、アドビサポートにお問い合わせください。アドビカスタマーサポート担当者と協力して、AMS デプロイメントに関するこれらのベストプラクティスを実装し、アドビ独自の形式に対する最適なツールとモデルを選択します。[!DNL Experience Manager] では、30000 x 23000 ピクセルを超える高解像度の PSB ファイルを処理できない場合があります。

### XMP の書き戻し {#xmp-writeback}

XMP の書き戻しにより、[!DNL Experience Manager] でメタデータが変更されたときは常に元のアセットが更新されます。これにより、次のような結果になります。

* アセット自体が変更されます
* アセットのバージョンが作成されます
* [!UICONTROL 「DAM アセットの更新」がアセットに対して実行されます]

上記の結果により、大量のリソースが消費されます。したがって、Adobeでは、必要がない場合、XMPの書き戻しを無効にすることをお勧めします。 詳しくは、 [XMPの書き戻し](https://experienceleague.adobe.com/docs/experience-manager-64/assets/administer/xmp-writeback.html?lang=ja).

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

[最新のサービスパック](/help/release-notes/release-notes.md)およびパフォーマンス関連のホットフィックスをインストールしてください。多くの場合、これらはシステムインデックスの更新を含みます。一部のインデックスの最適化については、[パフォーマンスチューニングのヒント](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/performance-tuning-guidelines.html?lang=en)を参照してください。

頻繁に実行するクエリにカスタムインデックスを作成します。詳しくは、[スロークエリの分析手法（英語）](https://aemfaq.blogspot.com/2014/08/oak-query-log-file-analyzer-tool.html)と[カスタムインデックスの作成](/help/sites-deploying/queries-and-indexing.md)を参照してください。クエリやインデックスについての追加のインサイトやベストプラクティスについては、[クエリとインデックスに関するベストプラクティス](/help/sites-deploying/best-practices-for-queries-and-indexing.md) を参照してください。

### Lucene Index の設定 {#lucene-index-configurations}

Oak インデックス設定を最適化して、[!DNL Experience Manager Assets] のパフォーマンスを向上できる場合があります。インデックス設定を更新して、インデックス再作成時間を短縮します。

1. CRXDe `/crx/de/index.jsp` を開き、管理者ユーザーとしてログインします。
1. `/oak:index/lucene` を参照します。
1. `/var`、`/etc/workflow/instances`、`/etc/replication` の値を持つ `String[]` プロパティ `excludedPaths` を追加します。
1. `/oak:index/damAssetLucene` を参照します。値が `/content/dam` の `String[]` プロパティ `includedPaths` を追加します。変更を保存します。

PDF ドキュメント内のテキストを検索するなど、アセットの全文検索を行う必要がない場合は、無効にします。フルテキストインデックスを無効にすると、インデックスのパフォーマンスが向上します。[!DNL Apache Lucene] テキスト抽出を無効にするには、次の手順に従います。

1. [!DNL Experience Manager] インターフェイスで、[!UICONTROL パッケージマネージャー] にアクセスします。
1. [disable_indexingbinarytextraction-10.zip](assets/disable_indexingbinarytextextraction-10.zip) にあるパッケージをアップロードしてインストールします。

### guessTotal {#guess-total}

大きな結果セットを生成するクエリを作成するときは、クエリ実行時のメモリ消費を抑えるために `guessTotal` パラメーターを使用してください。

## 既知の問題 {#known-issues}

### サイズの大きなファイル {#large-files}

[!DNL Experience Manager] では、サイズの大きなファイルに関連する既知の問題が主に 2 つあります。ファイルのサイズが 2 GB 以上に到達すると、コールドスタンバイの同期でメモリ不足のエラーが発生することがあります。場合によっては、スタンバイの同期が実行されなくなります。また、プライマリインスタンスのクラッシュを引き起こすこともあります。このシナリオは、コンテンツパッケージを含む、[!DNL Experience Manager] 内の 2 GB を超えるすべてのファイルが該当します。

同様に、S3 共有データストアを使用している間にファイルのサイズが 2 GB に到達すると、キャッシュからファイルシステムにファイルが完全に保持されるまで、少し時間がかかることがあります。結果として、バイナリなしのレプリケーションを使用しているとき、レプリケーションが完了する前にバイナリデータが保持されていなかった可能性があります。この状況は、特にデータの可用性が重要な場合に問題を引き起こす可能性があります。

## パフォーマンスのテスト {#performance-testing}

すべての [!DNL Experience Manager] のデプロイメントでボトルネックをすばやく特定し解決できるように、パフォーマンステストの体制を確立してください。留意点は次のとおりです。

### ネットワークのテスト {#network-testing}

お客様からのネットワークのパフォーマンスに関するすべての懸念については、次のタスクを実行してください。

* お客様のネットワーク内からネットワークのパフォーマンスをテストする
* アドビのネットワーク内からネットワークのパフォーマンスをテストする。AMS ユーザーの場合、CSE を使用してアドビのネットワーク内からテストしてください。
* 別のアクセスポイントからネットワークのパフォーマンスをテストする
* ネットワークのベンチマークツールを使用する
* ディスパッチャーに対してテストする

### [!DNL Experience Manager] デプロイメントテスト {#aem-deployment-testing}

CPU を効率的に使用し、負荷を分割することで遅延を最小限に抑え、高いスループットを実現するには、[!DNL Experience Manager] のパフォーマンスを定期的に監視してください。具体的には、以下のようになります。

* [!DNL Experience Manager] デプロイメントに対して負荷テストを実行してください。
* アップロードのパフォーマンスと UI の応答性を監視する.

## [!DNL Experience Manager Assets] パフォーマンスチェックリストとアセット管理タスクの影響 {#checklist}

* HTTPS を有効化して企業の HTTP トラフィックスニッファーに対応する.
* サイズの大きなアセットのアップロードには有線接続を使用する.
* Java 8 にデプロイする
* 最適な JVM パラメーターを設定する。
* ファイルシステムデータストアまたは S3 データストアを設定します。
* サブアセットの生成を無効にします。有効にした場合、AEM ワークフローは複数ページのアセットの各ページに個別のアセットを作成します。これらのページはそれ自体がアセットであり、追加のディスク領域を消費するほか、バージョン管理や追加のワークフロー処理を必要とします。個別のページが必要ない場合は、サブアセットの生成とページの抽出のアクティビティを無効にしてください。
* 一時的なワークフローを有効化する.
* Granite のワークフローキューを調整して同時に実行されるジョブ数を制限する.
* [!DNL ImageMagick] を設定してリソースの消費を制限します。
* 「[!UICONTROL DAM アセットの更新]」ワークフローから不要な手順を削除します。
* ワークフローとバージョンのパージを設定する.
* 最新のサービスパックとホットフィックスでインデックスを最適化します。その他のインデックスの最適化方法については、アドビカスタマーサポートまでお問い合わせください。
* guessTotal を使用してクエリのパフォーマンスを最適化する。
* ファイルのコンテンツからファイルの種類を検出するように [!DNL Experience Manager] を設定すると（**[!UICONTROL AEM Web コンソール]** で **[!UICONTROL Day CQ DAM Mine タイプサービス]**&#x200B;を有効にする）リソースを大量に消費するので、ピーク外の時間帯に多くのファイルを一括アップロードします。
