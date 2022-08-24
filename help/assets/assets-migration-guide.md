---
title: アセットを一括で移行する
description: ' [!DNL Adobe Experience Manager] へのアセットの移行、メタデータの適用、レンディションの生成、パブリッシュインスタンスでのアクティベートをそれぞれ行う方法について説明します。'
contentOwner: AG
role: Architect, Admin
feature: Migration,Renditions,Asset Management
exl-id: 184f1645-894a-43c1-85f5-8e0d2d77aa73
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '1799'
ht-degree: 100%

---

# アセットを一括で移行する方法 {#assets-migration-guide}

アセットを [!DNL Adobe Experience Manager] に移行する際には、いくつかの手順を考慮する必要があります。現在のホームからアセットやメタデータを抽出する方法は、実装環境により方法が大きく異なるのでこのドキュメントでは説明しません。本書では、抽出したアセットを [!DNL Experience Manager] に移行してメタデータを適用し、レンディションを生成してそれらをパブリッシュインスタンスでアクティベートする方法について説明します。

## 前提条件 {#prerequisites}

この方法に従って実際に手順を実行する前に、[Assets パフォーマンスチューニングに関するヒント](performance-tuning-guidelines.md)のガイダンスを確認して実践してください。ここで紹介する手順の多くは、同時に実行可能なジョブの最大数の設定など、負荷時のサーバーの安定性とパフォーマンスを大幅に改善します。システムにアセットが読み込まれた後だと、その他の手順（ファイルデータストアの設定など）を実行するのがより困難になります。

>[!NOTE]
>
>次のアセット移行ツールは [!DNL Experience Manager] の一部ではないので、Adobe ではサポートしていません。
>
>* ACS AEM ツールの Tag Maker
>* ACS AEM ツールの CSV Asset Importer
>* ACS Commons の Bulk Workflow Manager
>* ACS Commons の Fast Action Manager
>* 合成ワークフロー
>
>このソフトウェアはオープンソースで、[Apache v2 License](https://adobe-consulting-services.github.io/pages/license.html) が適用されます。質問や問題を報告するには、それぞれ [ACS AEM ツール](https://github.com/Adobe-Consulting-Services/acs-aem-commons/issues)と [ACS AEM Commons に関する GitHub の問題](https://github.com/Adobe-Consulting-Services/acs-aem-tools/issues)を利用してください。

## [!DNL Experience Manager] への移行 {#migrating-to-aem}

[!DNL Experience Manager] にアセットを移行するにはいくつかの手順を経る必要があるので、フェーズ別に処理することをお勧めします。移行のフェーズは次のとおりです。

1. ワークフローの無効化.
1. タグの読み込み.
1. アセットの取り込み.
1. レンディションの処理.
1. アセットのアクティベート.
1. ワークフローを有効化する.

![chlimage_1-223](assets/chlimage_1-223.png)

### ワークフローの無効化 {#disabling-workflows}

移行を開始する前に、[!UICONTROL DAM アセットの更新]ワークフローのランチャーを無効化します。すべてのアセットを取り込んでからワークフローをバッチで実行する方法が最適です。移行が実行されるときに既にライブである場合は、これらのアクティビティを営業時間外に実行するようにスケジュールを設定できます。

### タグの読み込み {#loading-tags}

画像に適用するタグ分類は既に用意されていることがあります。CSV Asset Importer などのツールや [!DNL Experience Manager] のメタデータプロファイルのサポートにより、タグをアセットに適用する処理は自動化できますが、タグをシステムに読み込む必要があります。[ACS AEM ツールの Tag Maker](https://adobe-consulting-services.github.io/acs-aem-tools/features/tag-maker/index.html) 機能を使用すると、システムに読み込まれた Microsoft Excel のスプレッドシートを使用してタグを入力できます。

### アセットの取り込み {#ingesting-assets}

アセットをシステムに取り込む際に重要なのは、パフォーマンスと安定性です。システムに大量のデータを読み込むので、特に既に実稼動環境にあるシステムでは、システムがパフォーマンスを可能な限り発揮できるようにする一方で、処理に必要な時間を短縮し、システムのオーバーロードによりシステムがクラッシュしないように注意する必要があります。

システムにアセットを読み込むには、HTTP を使用したプッシュベースのアプローチと JCR の API を使用したプルベースのアプローチがあります。

#### HTTP 経由で送信 {#pushing-through-http}

アドビの Managed Services チームは Glutton というツールを使用してお客様の環境にデータを読み込みます。Glutton は小さな Java アプリケーションであり、[!DNL Experience Manager] のデプロイメントでディレクトリから別のディレクトリにすべてのアセットを読み込みます。Glutton の代わりに、Perl スクリプトなどのツールを使用してアセットをリポジトリに投稿することもできます。

HTTPS を通じたプッシュのアプローチには、主に次の 2 つの欠点があります。

1. アセットは HTTP を介してサーバーに送信する必要がある。これには大量のオーバーヘッドが発生し、時間もかかるので、移行に要する時間が長くなります。
1. アセットに適用する必要があるタグやカスタムメタデータがある場合、このアプローチでは、アセットを取り込んだ後にこのメタデータを適用するという、2 段階のカスタムプロセスを実行する必要がある。

アセットを取り込むもう一方のアプローチでは、ローカルファイルシステムからアセットを引っ張ってきます。ただし、プルベースのアプローチを実行する外部ドライブやネットワーク共有がサーバーにマウントされていない場合は、HTTP を通じたアセットの投稿が最適なオプションです。

#### ローカルファイルシステムからの取得 {#pulling-from-the-local-filesystem}

[ACS AEM ツールの CSV Asset Importer](https://adobe-consulting-services.github.io/acs-aem-tools/features/csv-asset-importer/index.html) は、アセットをファイルシステムから、アセットメタデータをアセット読み込み用の CSV ファイルから、それぞれ取り込みます。Experience Manager の Asset Manager API を使用して、アセットをシステムに取り込み、設定したメタデータプロパティを適用します。アセットはネットワークファイルマウントまたは外部ドライブを介してサーバーにマウントされているのが理想です。

アセットをネットワーク上で送信する必要がないので、全体的なパフォーマンスが劇的に向上します。このため、一般的にはこの方法がアセットをリポジトリに読み込む最も効率的な方法と見なされています。さらに、ツールがメタデータの取り込みをサポートし、すべてのアセットとメタデータを 1 つの手順で取り込むことができるので、別のツールを使用してメタデータを適用する 2 つ目の手順が不要になります。

### レンディションの処理 {#processing-renditions}

アセットをシステムに読み込んだ後、メタデータを抽出してレンディションを生成するには、[!UICONTROL DAM アセットの更新]ワークフローを通じてアセットを処理する必要があります。この手順を実行する前に、[!UICONTROL DAM アセットの更新]ワークフローをニーズに合わせて複製および変更する必要があります。既製のワークフローには、Dynamic Media PTIFF の生成や [!DNL InDesign Server] の統合など、ユーザーによっては必要でない手順が多く含まれています。

ニーズに合わせてワークフローを設定したら、次の 2 つの方法のいずれかで実行できます。

1. 最も簡単なアプローチは、[ACS Commons の Bulk Workflow Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/bulk-workflow-manager.html) です。このツールを使用すると、クエリを実行し、クエリの結果をワークフローを通じて処理します。バッチサイズを設定するオプションも用意されています。
1. [ACS Commons の Fast Action Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html) は[合成ワークフロー](https://adobe-consulting-services.github.io/acs-aem-commons/features/synthetic-workflow.html)と組み合わせて使用できます。このアプローチはより複雑ですが、[!DNL Experience Manager] ワークフローエンジンのオーバーヘッドを削除し、サーバーリソースの使用を最適化します。さらに、Fast Action Manager はサーバーリソースを動的に監視し、システムに配置された読み込みをスロットリングすることでパフォーマンスを大幅に向上します。サンプルスクリプトは ACS Commons の機能ページに記載されています。

### アセットのアクティベート {#activating-assets}

パブリッシュ層のあるデプロイメントでは、アセットをパブリッシュファームにアクティベートする必要があります。アドビは 1 つ以上のパブリッシュインスタンスを実行することを推奨していますが、すべてのアセットを 1 つのパブリッシュインスタンスにレプリケートして、そのインスタンスをクローンする方法が最も効率的です。多数のアセットをアクティベートするときは、ツリーのアクティベートを実行した後に、干渉する必要が生じる場合があります。理由は、アクティベートをトリガーするときに、Sling のジョブやイベントキューに項目が追加されるからです。このキューのサイズがだいたい 40,000 項目を超えると、処理速度が劇的に低下します。このキューのサイズが 100,000 項目を超えると、システムの安定性に影響を及ぼします。

この問題を回避するには、[Fast Action Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html) を使用してアセットのレプリケートを管理します。これは Sling キューを使用することなく動作し、オーバーヘッドを減らすほか、ワークロードをスロットルしてサーバーのオーバーロードを防ぎます。レプリケーションの管理に FAM を使用する例は、この機能のドキュメントページに記載しています。

アセットをパブリッシュファームに移行するその他のオプションは、[vlt-rcp](https://jackrabbit.apache.org/filevault/rcp.html) または [oak-run](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run) を使用する方法です。これらは Jackrabbit の一部のツールとして提供されます。[!DNL Experience Manager] インフラストラクチャにオープンソースツール [Grabbit](https://github.com/TWCable/grabbit) を使用する方法もあります。vlt よりも高いパフォーマンスを発揮すると言われています。

これらのアプローチで注意すべき点は、オーサーインスタンス上でアセットがアクティベートされていると表示されないことです。アセットのアクティベート状態を正しくフラグ設定するには、アセットをアクティベート済みとマークする別のスクリプトも実行する必要があります。

>[!NOTE]
>
>アドビは Grabbit を管理およびサポートしません。

### パブリッシュをクローン化する {#cloning-publish}

アセットがアクティベートされたら、パブリッシュインスタンスをクローンしてデプロイメントに必要なコピーを必要な分だけ作成できます。サーバーのクローンは比較的簡単ですが、いくつか重要な手順があります。パブリッシュをクローンするには：

1. ソースインスタンスとデータストアをバックアップします。
1. インスタンスとデータストアのバックアップを対象の場所に復元します。続く手順はすべてこの新しいインスタンスを参照します。
1. `crx-quickstart/launchpad/felix` でファイルシステムの検索を実行し、`sling.id` を探します。このファイルを削除します。
1. データストアのルートパスで、`repository-XXX` ファイルを探してすべて削除します。
1. `crx-quickstart/install/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config` と `crx-quickstart/launchpad/config/org/apache/jackrabbit/oak/plugins/blob/datastore/FileDataStore.config` を編集し、新しい環境のデータストアの場所を指すようにします。
1. 環境を開始します。
1. オーサー環境にあるすべてのレプリケーションエージェントが正しいパブリッシュインスタンスを指す、または新しいインスタンスの Dispatcher のフラッシュエージェントが新しい環境の正しい Dispatcher を参照するように設定を更新します。

### ワークフローを有効化する {#enabling-workflows}

移行が完了したら、レンディションの生成とメタデータの抽出をサポートするために [!UICONTROL DAM の更新アセット]ワークフローのランチャーを再度有効化し、稼働中のシステムが日常的に使用できるようにします。

## [!DNL Experience Manager] デプロイメントを超えた移行 {#migrating-between-aem-instances}

それほど一般的ではないものの、ある [!DNL Experience Manager] デプロイメントから別のデプロイメントに大量のデータを移行する必要があります。例えば、[!DNL Experience Manager] のアップグレードを実行したり、ハードウェアをアップグレードをしたり、新しいデータセンターへの移行（AMS の移行）を実行する場合です。

このケースでは、移行するアセットには既にメタデータが入力されており、レンディションは既に生成されています。インスタンス間の移動に集中することができます。[!DNL Experience Manager] デプロイメント間で移行を行うには、次の手順を実行します。

1. ワークフローランチャーを無効化する：他のアセットとともに共にレンディションを移行するするため、[!UICONTROL DAM の更新アセット]ワークフローのランチャーを無効にする必要があります。

1. タグを移行する：タグは既にソースの [!DNL Experience Manager] デプロイメントに読み込まれているため、コンテンツパッケージでタグをビルドした後、パッケージ自体をターゲットデプロイメントにインストールできます。

1. アセット移行する：[!DNL Experience Manager]デプロイメントから別のデプロイメントにアセットを移行する場合に推奨されるツールは次の 2 つです。

   * **Vault Remote Copy**（vlt rcp）：ネットワーク全体で vlt が使用できるようになります。移動元と移動先のディレクトリを指定すると、vit がすべてのリポジトリデータを一方のインスタンスからダウンロードし、もう一方に読み込みます。vt rcp については、[https://jackrabbit.apache.org/filevault/rcp.html](https://jackrabbit.apache.org/filevault/rcp.html) に記載されています。
   * **Grabbit**：Time Warner Cable が自社の [!DNL Experience Manager] 実装のために開発したオープンソースのコンテンツ同期ツールです。継続的なデータストリームを使用するので、vlt rcp と比較して待ち時間が少なく、vlt rcp の 2 倍から 10 倍高速であると言われています。また、Grabbit はデルタコンテンツのみの同期をサポートし、最初の移行パスが完了した後に加えられた変更を同期できます。

1. アセットを有効にする：[アセットの有効化](#activating-assets)については、[!DNL Experience Manager] に初めて移行する際の手順について記載された説明に従ってください。

1. パブリッシュをクローン化する：新規の移行の場合と同様に、1 つのパブリッシュインスタンスを読み込んでクローン化する方が、両方のノードでコンテンツを有効にするよりも効率的です。[パブリッシュインスタンスのクローン](#cloning-publish)を参照してください。

1. ワークフローを有効にする：移行が完了したら、[!UICONTROL DAM の更新アセット]ワークフローのランチャーを再び有効にして、レンディションの生成とメタデータの抽出をサポートし、日常的なシステムの利用を継続できるようにします。
