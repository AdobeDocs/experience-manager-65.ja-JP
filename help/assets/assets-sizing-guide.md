---
title: '[!DNL Assets] サイジングガイド'
description: 導入に必要なインフラストラクチャとリソースを見積もるための効率的な指標を決定するためのベストプラクティス [!DNL Adobe Experience Manager Assets]。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '1614'
ht-degree: 60%

---


# [!DNL Assets] サイジングガイド {#assets-sizing-guide}

When sizing the environment for an [!DNL Adobe Experience Manager Assets] implementation, it is important to ensure that there are sufficient resources available in terms of disk, CPU, memory, IO, and network throughput. これらのリソースのサイジングには、システムに読み込まれたアセットの数を理解しておく必要があります。わかりやすい指標がない場合は、ライブラリの有効期間から既存のライブラリのサイズを分割し、アセットが作成されたときの割合を見つけることができます。

## ディスク {#disk}

### データストア {#datastore}

A common mistake made when sizing the required disk space for an [!DNL Assets] implementation is to base the calculations on the size of the raw images to be ingested into the system. By default, [!DNL Experience Manager] creates three renditions in addition to the original image for use in rendering the [!DNL Experience Manager] user interface elements. 以前の実装では、これらのレンディションは取り込まれるアセットのサイズの倍と想定されていました。

ほとんどのユーザーは、既製のレンディションに加えてカスタムレンディションを定義します。In addition to the renditions, [!DNL Assets] lets you extract sub-assets from common file types, such as [!DNL Adobe InDesign] and [!DNL Adobe Illustrator].

Finally, versioning capabilities of [!DNL Experience Manager] store duplicates of the assets in the version history. 頻繁に削除するバージョンを構成できます。 ただし、多くのユーザーはバージョンをシステムに長い間保持するので、ストレージ領域をさらに消費します。

これらの要素を考慮して、ユーザーのアセットを保存するための正確なストレージ領域を計算する手法が必要です。

1. システムに読み込まれるアセットのサイズと数を決定します。
1. Get a representative sample of the assets to be uploaded into [!DNL Experience Manager]. 例えば、システムに PSD、JPG、AI および PDF ファイルを読み込む場合、各ファイル形式の複数のサンプル画像が必要です。また、これらのサンプルは異なるファイルサイズや画像が混在する中で代表的なものである必要があります。
1. 使用するレンディションを定義します。
1. またはアプリケーションを使用して、レンディションを作成 [!DNL Experience Manager] し [!DNL ImageMagick][!DNL Adobe Creative Cloud] ます。 ユーザーが指定したレンディションに加えて、既製のレンディションを作成します。Scene7を実装するユーザーは、ICバイナリを使用してPTIFFレンディションを生成し、Experience Managerに保存することができます。
1. サブアセットを使用する場合は、適切なファイルタイプに合わせて生成します。
1. 出力された画像、レンディションおよびサブアセットのサイズを元の画像と比較します。これにより、システムが読み込まれたときに、期待される成長率を生成できます。 例えば、1 GB のアセットを処理した後に合計サイズが 3 GB のレンディションとサブアセットを生成した場合、レンディションの拡張係数は 3 です。
1. アセットのバージョンがシステムで管理される最大時間を決定します。
1. 既存のアセットがシステムで変更される頻度を決定します。If [!DNL Experience Manager] is used as a collaboration hub in creative workflows, the amount of changes are high. 完了したアセットのみがシステムにアップロードされる場合、この数はかなり少なくなります。
1. 毎月システムに読み込まれるアセットの数を決定します。正しい数字がわからない場合は、現在使用できるアセットの数を確認し、その数を最も古いアセットの年齢で除算して、おおよその数を計算します。

上記の手順を実行すると、次の項目を決定できます。

* 読み込まれるアセットの Raw サイズ.
* 読み込まれるアセットの数.
* レンディションの拡張係数.
* 月ごとのアセットの変更回数.
* アセットのバージョンを管理する月数.
* 月ごとに読み込まれる新しいアセットの数.
* ストレージ領域の割り当ての増加年数。

これらの数を「ネットワークサイジング」スプレッドシートに指定してデータストアに必要な空き容量の合計を決定できます。It is also a useful tool to determine the impact of maintaining asset versions or modifying assets in [!DNL Experience Manager] on disk growth.

ツールに取り込まれているサンプルデータは、前述のステップを実行することの重要性を示しています。データストアのサイズを読み込まれる Raw 画像のみを基準に設定（1 TB）すると、係数が 15 になり、リポジトリサイズが少なく見積もられることがあります。

[ファイルを入手](assets/disk_sizing_tool.xlsx)

### Shared datastores {#shared-datastores}

大規模なデータストアの場合は、ネットワークに接続されたドライブ上の共有ファイルデータストアを介して、またはAmazonS3データストアを介して、共有データストアを実装できます。 この場合、個々のインスタンスでバイナリのコピーを管理する必要がありません。また、共有データストアは、バイナリレスのレプリケーションを容易にし、環境を発行するためにアセットをレプリケートするために使用される帯域幅を削減します。

#### ユースケース {#use-cases}

データストアはプライマリとスタンバイのオーサーインスタンス間で共有し、プライマリインスタンスで加えられた変更をスタンバイインスタンスで更新するのにかかる時間を最小化できます。また、オーサーインスタンスとパブリッシュインスタンス間でデータストアを共有し、レプリケーション中のトラフィックを最小化することもできます。

#### ドローバック {#drawbacks}

データストアの共有が常に推奨されるとは限りません。いくつかの落とし穴が存在します。

#### Single point of failure {#single-point-of-failure}

共有データストアは、インフラストラクチャに単一障害点をもたらすことがあります。次のシナリオを検討してみましょう。システムにオーサーインスタンスが 1 つ、パブリッシュインスタンスが 2 つあり、それぞれ独自のデータストアがあるとします。いずれか 1 つがクラッシュしても、残りの 2 つは引き続き稼動します。ただし、データストアが共有されている場合、1 つのディスクに障害が発生すると、インフラストラクチャ全体がダウンします。このため、データストアを簡単に復元できる場所に共有データストアのバックアップが必要です。

共有データストアには AWS S3 サービスをデプロイすることをお勧めします。これにより、通常のディスクアーキテクチャと比較して、障害が発生する確率を大幅に減らします。

#### Increased complexity {#increased-complexity}

共有データストアは、ガベージコレクションなどの操作を複雑にします。通常、スタンドアロンのデータストアのガベージコレクションは、1 つのクリックで開始できます。しかし、共有データストアの場合は、単一のノードで実際のコレクションを実行することに加えて、そのデータストアを使用する各メンバーでマークスイープ操作が必要になります。

AWSの運用では、EBSボリュームのRAIDアレイを構築する代わりに(AmazonS3を介して)1か所の中央サイトを実装することで、システムの複雑さと運用上のリスクを大幅に軽減できます。

#### Performance concerns {#performance-concerns}

共有データストアでは、すべてのインスタンス間で共有されるネットワークにマウントされたドライブにバイナリを保存する必要があります。これらのバイナリはネットワーク経由でアクセスされるので、システムのパフォーマンスに悪影響が出ます。 ネットワーク接続やディスクアレイを高速化することで、その影響を一部軽減できます。しかし、これにはコストがかかります。AWSの操作の場合、すべてのディスクはリモートで、ネットワーク接続が必要です。 エフェメラルボリュームでは、インスタンスが開始または停止するときにデータが失われます。

#### 待ち時間 {#latency}

S3 の実装では、バックグラウンドの書き込みスレッドにより待ち時間が発生します。バックアップ手順では、この遅延を考慮する必要があります。 また、バックアップを作成するときに Lucene のインデックスが未完成のままになることがあります。これには、S3 データストアに書き込まれ、別のインスタンスからアクセスされる、時間に左右されるすべてのファイルが該当します。

### Node store or document store {#node-store-document-store}

次の要素によってリソースが消費されるので、ノードストアやドキュメントストアの正確なサイジングを特定するのは困難です。

* アセットのメタデータ
* アセットのバージョン
* 監査ログ
* アーカイブされたワークフローとアクティブなワークフロー

バイナリはデータストアに保存されるので、各バイナリが空き容量を一部占有します。大部分のリポジトリのサイズは 100 GB を下回ります。ただし、1 TBまで大きなリポジトリが存在する場合もあります。 また、オフラインコンパクションを実行するには、コンパクション済みのリポジトリをコンパクション前のバージョンの横に書き直すための十分な空き容量がボリュームに必要です。経験則としては、ディスクのサイズをリポジトリの予想サイズの 1.5 倍にすることです。

リポジトリには、IOPSレベルが3000を超えるSSDまたはディスクを使用します。 IOPS がパフォーマンスのボトルネックとなる可能性を排除するために、CPU の入出力待機レベルを監視して問題の兆候を早めに把握するようにしてください。

[ファイルを入手](assets/aem_environment_sizingtool.xlsx)

## ネットワーク {#network}

[!DNL Assets] には、他の多くの プロジェクトよりネットワークのパフォーマンスが重要になる使用例がいくつかあります。[!DNL Experience Manager]お客様は高速なサーバーを使用できますが、ネットワーク接続の大きさが、システムからアセットをアップロードおよびダウンロードするユーザの負荷をサポートするのに十分でない場合、動作は遅くなります。 There is a good methodology for determining the choke point in a user&#39;s network connection to [!DNL Experience Manager] at [Assets considerations for user experience, instance sizing, workflow evaluation, and network topology](/help/assets/assets-network-considerations.md).

## 制限事項 {#limitations}

実装をサイジングするときは、システムの制限事項を頭に入れておくことが重要です。If the proposed implementation exceeds these limitations, employ creative strategies, such as partitioning the assets across multiple [!DNL Assets] implementations.

メモリ不足（OOM）の問題を起こす要因はファイルのサイズだけではありません。画像のサイズにも依存します。You can avoid OOM issues by providing a higher heap size when you start [!DNL Experience Manager].

In addition, you can edit the threshold size property of the `com.day.cq.dam.commons.handler.StandardImageHandler` component in Configuration Manager to use intermediate temporary file greater than zero.

## アセットの最大数 {#maximum-number-of-assets}

データストア内のファイル数は、ファイルシステムの制限により 21 億に制限されています。おそらくリポジトリについては、データストアの制限に到達するかなり前に、ノードが多すぎることによる問題に直面します。

レンディションが誤って生成される場合は、Camera Raw ライブラリを使用します。ただしこの場合、画像の長いほうのサイズが 65000 ピクセルを超えてはいけません。また、画像に含めるメモリのサイズは512 MP（512 x 1024 x 1024ピクセル）以下にする必要があります。 アセットのサイズは問題になりません。

It is difficult to accurately estimate the size of the TIFF file supported out-of-the-box with a specific heap for [!DNL Experience Manager] because additional factors, such as pixel size influence processing. It is possible that [!DNL Experience Manager] can process a file of size of 255 MB out-of-the-box, but cannot process a file size of 18 MB because the latter comprises of an unusually higher number pixels compared to the former.

## Size of assets {#size-of-assets}

初期設定では、 [!DNL Experience Manager] 最大2 GBのファイルサイズのアセットをアップロードできます。 で非常に大きなアセットをアップロードするには、非常に大きなアセット [!DNL Experience Manager]をアップロードする [ための設定を参照してください](managing-video-assets.md#configuration-to-upload-assets-that-are-larger-than-gb)。
