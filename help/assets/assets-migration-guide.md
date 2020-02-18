---
title: アセットのAdobe Experience Managerアセットへの一括移行
description: アセットを AEM に移行してメタデータを適用し、レンディションを生成してそれらをパブリッシュインスタンスでアクティベートする方法について説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0ff23556444fcb161b0adf744bb72fdc50322d92

---


# アセットを一括で移行する方法 {#assets-migration-guide}

アセットを AEM に移行する際には、いくつかの手順を考慮する必要があります。現在のホームからアセットやメタデータを抽出する方法は、実装によりやり方が異なるのでこのドキュメントでは説明しません。本書では、抽出したアセットを AEM に移行してメタデータを適用し、レンディションを生成してそれらをパブリッシュインスタンスでアクティベートする方法について説明します。

## 前提条件 {#prerequisites}

Before actually performing any of the steps in this methodology, please review and implement the guidance in [Assets performance tuning tips](performance-tuning-guidelines.md). ここで紹介する手順の多くは、同時に実行可能なジョブの最大数の設定など、負荷時のサーバーの安定性とパフォーマンスを大幅に改善します。システムにアセットが読み込まれた後だと、その他の手順（ファイルデータストアの設定など）を実行するのがより困難になります。

>[!NOTE]
>
>次のアセット移行ツールはAEMに含まれておらず、アドビではサポートされていません。
>
>* ACS AEM ツールの Tag Maker
>* ACS AEM ツールの CSV Asset Importer
>* ACS Commons の Bulk Workflow Manager
>* ACS Commons の Fast Action Manager
>* 合成ワークフロー
>
>
このソフトウェアはオープンソースで、[Apache v2 License](https://adobe-consulting-services.github.io/pages/license.html) が適用されます。質問や問題を報告するには、それぞれ [GitHub の ACS AEM ツール](https://github.com/Adobe-Consulting-Services/acs-aem-commons/issues)と [ACS AEM Commons に関する Issues](https://github.com/Adobe-Consulting-Services/acs-aem-tools/issues) を利用してください。

## AEMへの移行 {#migrating-to-aem}

AEM にアセットを移行するにはいくつかの手順を経る必要があるので、フェーズ別に処理することをお勧めします。移行のフェーズは次のとおりです。

1. ワークフローを無効化する。
1. タグを読み込む。
1. アセットを取り込む。
1. レンディションを処理する。
1. アセットをアクティベートする。
1. ワークフローを有効化する。

![chlimage_1-223](assets/chlimage_1-223.png)

### Disable workflows {#disabling-workflows}

移行を開始する前に、DAM アセットの更新ワークフローのランチャーを無効化します。すべてのアセットを取り込んでからワークフローをバッチで実行する方法が最適です。移行が実行されるときに既にライブである場合は、これらのアクティビティを営業時間外に実行するようにスケジュールを設定できます。

### Load tags {#loading-tags}

画像に適用するタグ分類は既に用意されていることがあります。CSV Asset Importer などのツールや AEM のメタデータプロファイルのサポートにより、タグをアセットに適用する処理は自動化できますが、タグをシステムに読み込む必要があります。The [ACS AEM Tools Tag Maker](https://adobe-consulting-services.github.io/acs-aem-tools/features/tag-maker/index.html) feature lets you populate tags by using a Microsoft Excel spreadsheet that is loaded into the system.

### Ingest assets {#ingesting-assets}

アセットをシステムに取り込む際に重要なのは、パフォーマンスと安定性です。システムに大量のデータを読み込むので、特に既に実稼動環境にあるシステムでは、システムがパフォーマンスを可能な限り発揮できるようにする一方で、処理に必要な時間を短縮し、システムのオーバーロードによりシステムがクラッシュしないように注意する必要があります。

システムにアセットを読み込むには、HTTP を使用したプッシュベースのアプローチと JCR の API を使用したプルベースのアプローチがあります。

#### HTTP経由で送信 {#pushing-through-http}

アドビの Managed Services チームは Glutton というツールを使用してお客様の環境にデータを読み込みます。Glutton は小さな Java アプリケーションで、AEM インスタンスのあるディレクトリから別のディレクトリにすべてのアセットを読み込みます。Glutton の代わりに、Perl スクリプトなどのツールを使用してアセットをリポジトリに投稿することもできます。

httpsをプッシュするアプローチを使用する場合は、主に2つの方法があります。

1. アセットは HTTP を介してサーバーに送信する必要がある。これには大量のオーバーヘッドが発生し、時間もかかるので、移行に要する時間が長くなります。
1. アセットに適用する必要があるタグやカスタムメタデータがある場合、このアプローチでは、アセットを取り込んだ後にこのメタデータを適用するという、2 段階のカスタムプロセスを実行する必要がある。

アセットを取り込むもう一方のアプローチでは、ローカルファイルシステムからアセットを引っ張ってきます。ただし、プルベースのアプローチを実行する外部ドライブやネットワーク共有がサーバーにマウントされていない場合は、HTTP を通じたアセットの投稿が最適なオプションです。

#### Fetch from the local filesystem {#pulling-from-the-local-filesystem}

[ACS AEM Tools CSV Asset Importerは](https://adobe-consulting-services.github.io/acs-aem-tools/features/csv-asset-importer/index.html) 、アセットをファイルシステムから取り込み、アセットを読み込むためのCSVファイルからアセットメタデータを取り込みます。 AEM Asset Manager API はアセットをシステムに取り込み、設定したメタデータプロパティを適用します。アセットはネットワークファイルマウントまたは外部ドライブを介してサーバーにマウントされているのが理想です。

アセットをネットワーク上で送信する必要がないので、全体的なパフォーマンスが劇的に向上します。このため、一般的にはこの方法がアセットをリポジトリに読み込む最も効率的な方法と見なされています。さらに、ツールがメタデータの取り込みをサポートし、すべてのアセットとメタデータを 1 つの手順で取り込むことができるので、別のツールを使用してメタデータを適用する 2 つ目の手順が不要になります。

### Process renditions {#processing-renditions}

アセットをシステムに読み込んだ後、メタデータを抽出してレンディションを生成するには、DAM アセットの更新ワークフローを通じてアセットを処理する必要があります。この手順を実行する前に、DAM アセットの更新ワークフローをニーズに合わせて複製および変更する必要があります。既製のワークフローには、Scene7 PTIFF の生成や InDesign サーバーの統合など、ユーザーによっては必要でない手順が多く含まれています。

ニーズに合わせてワークフローを設定したら、次の 2 つの方法のいずれかで実行できます。

1. The simplest approach is [ACS Commons’ Bulk Workflow Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/bulk-workflow-manager.html). このツールを使用すると、クエリを実行し、クエリの結果をワークフローを通じて処理します。バッチサイズを設定するオプションも用意されています。
1. You can use the [ACS Commons Fast Action Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html) in concert with [Synthetic Workflows](https://adobe-consulting-services.github.io/acs-aem-commons/features/synthetic-workflow.html). このアプローチはより複雑ですが、AEM ワークフローエンジンのオーバーヘッドを削除し、サーバーリソースの使用を最適化します。さらに、Fast Action Manager はサーバーリソースを動的に監視し、システムに配置された読み込みをスロットルすることでパフォーマンスを大幅にブーストします。サンプルスクリプトは ACS Commons の機能ページに用意されています。

### Activate assets {#activating-assets}

パブリッシュ層のあるデプロイメントでは、アセットをパブリッシュファームにアクティベートする必要があります。アドビは 1 つ以上のパブリッシュインスタンスを実行することを推奨していますが、すべてのアセットを 1 つのパブリッシュインスタンスにレプリケートして、そのインスタンスをクローンする方法が最も効率的です。多数のアセットをアクティベートするときは、ツリーのアクティベートを実行した後に、干渉する必要がある場合があります。理由は次のとおりです。アクティブ化をオフにすると、アイテムがSlingジョブ/イベントキューに追加されます。 このキューのサイズがだいたい 40,000 項目を超えると、処理速度が劇的に低下します。このキューのサイズが 100,000 項目を超えると、システムの安定性に影響を及ぼします。

この問題を回避するには、[Fast Action Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html) を使用してアセットのレプリケートを管理します。これは Sling キューを使用することなく動作し、オーバーヘッドを減らすほか、ワークロードをスロットルしてサーバーのオーバーロードを防ぎます。レプリケーションの管理に FAM を使用する例は、この機能のドキュメントページに記載しています。

Other options for getting assets to the publish farm include using [vlt-rcp](https://jackrabbit.apache.org/filevault/rcp.html) or [oak-run](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run), which are provided as tools as part of Jackrabbit. Another option is to use an open-sourced tool for your AEM infrastructure called [Grabbit](https://github.com/TWCable/grabbit), which claims to have faster performance than vlt.

これらのアプローチで注意すべき点は、オーサリングインスタンス上でアセットがアクティベートされていると表示されないことです。アセットのアクティベート状態を正しくフラグするには、アセットをアクティベート済みとマークする別のスクリプトも実行する必要があります。

>[!NOTE]
>
>アドビは Grabbit を管理およびサポートしません。

### Clone Publish {#cloning-publish}

アセットがアクティベートされたら、パブリッシュインスタンスをクローンしてデプロイメントに必要なコピーを必要な分だけ作成できます。サーバーのクローンは比較的簡単ですが、いくつか重要な手順があります。パブリッシュをクローンするには：

1. ソースインスタンスとデータストアをバックアップします。
1. インスタンスとデータストアのバックアップを対象の場所に復元します。続く手順はすべてこの新しいインスタンスを参照します。
1. Perform a filesystem search under `crx-quickstart/launchpad/felix` for `sling.id`. このファイルを削除します。
1. データストアのルートパスで、`repository-XXX` ファイルを探してすべて削除します。
1. 新しい `crx-quickstart/install/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config` 環境上 `crx-quickstart/launchpad/config/org/apache/jackrabbit/oak/plugins/blob/datastore/FileDataStore.config` のデータストアの場所を編集し、その場所を指すようにします。
1. 環境を開始します。
1. オーサー環境にあるすべてのレプリケーションエージェントが正しいパブリッシュインスタンスを指す、または新しいインスタンスのディスパッチャーのフラッシュエージェントが新しい環境の正しいディスパッチャーを参照するように設定を更新します。

### Enable workflows {#enabling-workflows}

移行が完了したら、レンディションの生成とメタデータの抽出をサポートするように DAM の更新アセットワークフローのランチャーを再度有効化し、稼動中のシステムが日常的に使用できるようにします。

## AEMデプロイメント間の移行 {#migrating-between-aem-instances}

それほど一般的ではありませんが、ある AEM インスタンスからもう一方のインスタンスに大量のデータを移行する必要があることもあります。例えば、AEM やお使いのハードウェアをアップグレードする場合や、AMS の移行などに伴い新しいデータセンターに移行する場合などです。

このケースでは、移行するアセットには既にメタデータが入力されており、レンディションは既に生成されています。インスタンス間の移動に集中することができます。AEM インスタンス間で移行するには、次の手順を実行します。

1. ワークフローを無効にする：レンディションをアセットと共に移行するので、DAM Update Assetのワークフローランチャーを無効にする必要があります。

1. タグの移行：ソースAEMインスタンスに既にタグが読み込まれているので、コンテンツパッケージ内にタグを作成し、ターゲットインスタンスにパッケージをインストールできます。

1. アセットの移行：AEMインスタンス間でアセットを移動する場合に推奨されるツールは2つあります。

   * **Vault Remote Copy** (vlt rcp)を使用すると、ネットワーク全体でvltを使用できます。 移動元と移動先のディレクトリを指定すると、vit がすべてのリポジトリデータを一方のインスタンスからダウンロードし、もう一方に読み込みます。Vlt rcp is documented at [https://jackrabbit.apache.org/filevault/rcp.html](https://jackrabbit.apache.org/filevault/rcp.html)
   * **Grabbit**。Time Warner Cable が AEM の実装のために開発した、オープンソースのコンテンツ同期ツールです。継続的なデータストリームを使用するので、vlt rcp と比較して待ち時間が少なく、vlt rcp の 2 倍から 10 倍高速であると言われています。また、Grabbit はデルタコンテンツのみの同期をサポートし、最初の移行パスが完了した後に加えられた変更を同期できます。

1. Activate assets: Follow the instructions for [activating assets](#activating-assets) documented for the initial migration to AEM.

1. 公開のコピー：新しい移行と同様に、単一の発行インスタンスを読み込んでコピーする方が、両方のノードでコンテンツをアクティブ化するよりも効率的です。 [パブリッシュインスタンスのクローン](#cloning-publish)を参照してください。

1. ワークフローの有効化：移行が完了したら、DAMアセットの更新ワークフローのランチャーを再度有効にして、日常的なシステム使用のためのレンディションの生成とメタデータの抽出をサポートします。
