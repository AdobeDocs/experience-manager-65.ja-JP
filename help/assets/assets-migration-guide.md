---
title: アセットの一括移行
description: アセットを [!DNL Adobe Experience Manager]に取り込み、メタデータを適用、レンディションを生成、パブリッシュインスタンスに対してアクティブ化する方法について説明します。
contentOwner: AG
role: Architect, Administrator
feature: 移行，レンディション，アセット管理
exl-id: 184f1645-894a-43c1-85f5-8e0d2d77aa73
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1803'
ht-degree: 67%

---

# アセットを一括で移行する方法{#assets-migration-guide}

アセットを[!DNL Adobe Experience Manager]に移行する際には、いくつかの手順を考慮する必要があります。 実装によって大きく異なるので、現在のホームからアセットとメタデータを抽出する方法は、このドキュメントの範囲外ですが、このドキュメントでは、これらのアセットを[!DNL Experience Manager]に取り込み、メタデータを適用し、レンディションを生成し、インスタンスを公開する方法について説明します。

## 前提条件 {#prerequisites}

この方法の手順を実際に実行する前に、[Assetsパフォーマンスチューニングのヒント](performance-tuning-guidelines.md)のガイダンスを確認し、実装してください。 ここで紹介する手順の多くは、同時に実行可能なジョブの最大数の設定など、負荷時のサーバーの安定性とパフォーマンスを大幅に改善します。システムにアセットが読み込まれた後だと、その他の手順（ファイルデータストアの設定など）を実行するのがより困難になります。

>[!NOTE]
>
>次のアセット移行ツールは、[!DNL Experience Manager]に含まれておらず、Adobeではサポートされていません。
>
>* ACS AEM ツールの Tag Maker
>* ACS AEM ツールの CSV Asset Importer
>* ACS Commons の Bulk Workflow Manager
>* ACS Commons の Fast Action Manager
>* 合成ワークフロー

>
>
このソフトウェアはオープンソースで、[Apache v2 License](https://adobe-consulting-services.github.io/pages/license.html) が適用されます。質問や問題を報告するには、それぞれ [ACS AEM ツール](https://github.com/Adobe-Consulting-Services/acs-aem-commons/issues)と [ACS AEM Commons に関する GitHub の問題](https://github.com/Adobe-Consulting-Services/acs-aem-tools/issues)を利用してください。

## [!DNL Experience Manager] {#migrating-to-aem}に移行

[!DNL Experience Manager]へのアセットの移行にはいくつかの手順が必要で、段階的なプロセスと見なす必要があります。 移行のフェーズは次のとおりです。

1. ワークフローを無効化する。
1. タグを読み込む。
1. アセットを取り込む。
1. レンディションを処理する。
1. アセットをアクティベートする。
1. ワークフローを有効化する。

![chlimage_1-223](assets/chlimage_1-223.png)

### ワークフローを無効にする{#disabling-workflows}

移行を開始する前に、[!UICONTROL DAMアセットの更新]ワークフローのランチャーを無効にします。 すべてのアセットを取り込んでからワークフローをバッチで実行する方法が最適です。移行が実行されるときに既にライブである場合は、これらのアクティビティを営業時間外に実行するようにスケジュールを設定できます。

### タグの読み込み{#loading-tags}

画像に適用するタグ分類は既に用意されていることがあります。CSVアセットインポーターやメタデータプロファイルの[!DNL Experience Manager]サポートなどのツールは、アセットにタグを適用するプロセスを自動化できますが、タグはシステムに読み込む必要があります。 [ACS AEM ツールの Tag Maker](https://adobe-consulting-services.github.io/acs-aem-tools/features/tag-maker/index.html) 機能を使用すると、システムに読み込まれた Microsoft Excel のスプレッドシートを使用してタグを入力できます。

### アセットの取り込み{#ingesting-assets}

アセットをシステムに取り込む際に重要なのは、パフォーマンスと安定性です。システムに大量のデータを読み込むので、特に既に実稼動環境にあるシステムでは、システムがパフォーマンスを可能な限り発揮できるようにする一方で、処理に必要な時間を短縮し、システムのオーバーロードによりシステムがクラッシュしないように注意する必要があります。

システムにアセットを読み込むには、HTTP を使用したプッシュベースのアプローチと JCR の API を使用したプルベースのアプローチがあります。

#### HTTP {#pushing-through-http}を介して送信

アドビの Managed Services チームは Glutton というツールを使用してお客様の環境にデータを読み込みます。Gluttonは、[!DNL Experience Manager]デプロイメント上の1つのディレクトリから別のディレクトリにすべてのアセットを読み込む、小さなJavaアプリケーションです。 Glutton の代わりに、Perl スクリプトなどのツールを使用してアセットをリポジトリに投稿することもできます。

HTTPS を通じたプッシュのアプローチには、主に次の 2 つの欠点があります。

1. アセットは HTTP を介してサーバーに送信する必要がある。これには大量のオーバーヘッドが発生し、時間もかかるので、移行に要する時間が長くなります。
1. アセットに適用する必要があるタグやカスタムメタデータがある場合、このアプローチでは、アセットを取り込んだ後にこのメタデータを適用するという、2 段階のカスタムプロセスを実行する必要がある。

アセットを取り込むもう一方のアプローチでは、ローカルファイルシステムからアセットを引っ張ってきます。ただし、プルベースのアプローチを実行する外部ドライブやネットワーク共有がサーバーにマウントされていない場合は、HTTP を通じたアセットの投稿が最適なオプションです。

#### ローカルファイルシステム{#pulling-from-the-local-filesystem}からフェッチ

[ACS AEM ツールの CSV Asset Importer](https://adobe-consulting-services.github.io/acs-aem-tools/features/csv-asset-importer/index.html) は、アセットをファイルシステムから、アセットメタデータをアセット読み込みの CSV ファイルから、それぞれ取り込みます。Experience ManagerAsset Manager APIは、アセットをシステムに読み込み、設定済みのメタデータプロパティを適用するために使用します。 アセットはネットワークファイルマウントまたは外部ドライブを介してサーバーにマウントされているのが理想です。

アセットをネットワーク上で送信する必要がないので、全体的なパフォーマンスが劇的に向上します。このため、一般的にはこの方法がアセットをリポジトリに読み込む最も効率的な方法と見なされています。さらに、ツールがメタデータの取り込みをサポートし、すべてのアセットとメタデータを 1 つの手順で取り込むことができるので、別のツールを使用してメタデータを適用する 2 つ目の手順が不要になります。

### レンディションの処理{#processing-renditions}

アセットをシステムに読み込んだ後、[!UICONTROL DAMアセットの更新]ワークフローを通じてアセットを処理し、メタデータを抽出してレンディションを生成する必要があります。 この手順を実行する前に、必要に応じて[!UICONTROL DAMアセットの更新]ワークフローを複製および変更する必要があります。 標準のワークフローには、Dynamic Media PTIFFの生成や[!DNL InDesign Server]統合など、ユーザーにとって不要な手順が多数含まれています。

ニーズに合わせてワークフローを設定したら、次の 2 つの方法のいずれかで実行できます。

1. 最も簡単なアプローチは、[ACS Commons の Bulk Workflow Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/bulk-workflow-manager.html) です。このツールを使用すると、クエリを実行し、クエリの結果をワークフローを通じて処理します。バッチサイズを設定するオプションも用意されています。
1. [ACS Commons の Fast Action Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html) は[合成ワークフロー](https://adobe-consulting-services.github.io/acs-aem-commons/features/synthetic-workflow.html)と組み合わせて使用できます。このアプローチはより複雑ですが、サーバーリソースの使用を最適化しながら、[!DNL Experience Manager]ワークフローエンジンのオーバーヘッドを削除できます。 さらに、Fast Action Manager はサーバーリソースを動的に監視し、システムに配置された読み込みをスロットリングすることでパフォーマンスを大幅に向上します。サンプルスクリプトは ACS Commons の機能ページに記載されています。

### アセットのアクティベート{#activating-assets}

パブリッシュ層のあるデプロイメントでは、アセットをパブリッシュファームにアクティベートする必要があります。アドビは 1 つ以上のパブリッシュインスタンスを実行することを推奨していますが、すべてのアセットを 1 つのパブリッシュインスタンスにレプリケートして、そのインスタンスをクローンする方法が最も効率的です。多数のアセットをアクティベートするときは、ツリーのアクティベートを実行した後に、干渉する必要が生じる場合があります。理由は次のとおりです。アクティベーションを実行すると、項目がSlingジョブ/イベントキューに追加されます。 このキューのサイズがだいたい 40,000 項目を超えると、処理速度が劇的に低下します。このキューのサイズが 100,000 項目を超えると、システムの安定性に影響を及ぼします。

この問題を回避するには、[Fast Action Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html) を使用してアセットのレプリケートを管理します。これは Sling キューを使用することなく動作し、オーバーヘッドを減らすほか、ワークロードをスロットルしてサーバーのオーバーロードを防ぎます。レプリケーションの管理に FAM を使用する例は、この機能のドキュメントページに記載しています。

アセットをパブリッシュファームに移行するその他のオプションは、[vlt-rcp](https://jackrabbit.apache.org/filevault/rcp.html) または [oak-run](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run) を使用する方法です。これらは Jackrabbit の一部のツールとして提供されます。[Grabbit](https://github.com/TWCable/grabbit)と呼ばれる、[!DNL Experience Manager]インフラストラクチャのオープンソースツールを使用する方法もあります。vitよりも高いパフォーマンスを発揮すると言われています。

これらのアプローチで注意すべき点は、オーサーインスタンス上でアセットがアクティベートされていると表示されないことです。アセットのアクティベート状態を正しくフラグ設定するには、アセットをアクティベート済みとマークする別のスクリプトも実行する必要があります。

>[!NOTE]
>
>アドビは Grabbit を管理およびサポートしません。

### 公開のクローン{#cloning-publish}

アセットがアクティベートされたら、パブリッシュインスタンスをクローンしてデプロイメントに必要なコピーを必要な分だけ作成できます。サーバーのクローンは比較的簡単ですが、いくつか重要な手順があります。パブリッシュをクローンするには：

1. ソースインスタンスとデータストアをバックアップします。
1. インスタンスとデータストアのバックアップを対象の場所に復元します。続く手順はすべてこの新しいインスタンスを参照します。
1. `crx-quickstart/launchpad/felix` でファイルシステムの検索を実行し、`sling.id` を探します。このファイルを削除します。
1. データストアのルートパスで、`repository-XXX` ファイルを探してすべて削除します。
1. `crx-quickstart/install/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config` と `crx-quickstart/launchpad/config/org/apache/jackrabbit/oak/plugins/blob/datastore/FileDataStore.config` を編集し、新しい環境のデータストアの場所を指すようにします。
1. 環境を開始します。
1. オーサー環境にあるすべてのレプリケーションエージェントが正しいパブリッシュインスタンスを指す、または新しいインスタンスの Dispatcher のフラッシュエージェントが新しい環境の正しい Dispatcher を参照するように設定を更新します。

### ワークフローを有効にする{#enabling-workflows}

移行が完了したら、レンディションの生成とメタデータの抽出をサポートして継続的なシステム使用を実現するために、[!UICONTROL DAMアセットの更新]ワークフローのランチャーを再度有効にする必要があります。

## [!DNL Experience Manager]デプロイメント間の移行{#migrating-between-aem-instances}

ごく一般的ではありませんが、場合によっては、[!DNL Experience Manager]デプロイメント間で大量のデータを移行する必要があります。例えば、[!DNL Experience Manager]アップグレードを実行する場合、ハードウェアをアップグレードする場合、またはAMS移行を使用する場合など、新しいデータセンターに移行する場合などです。

このケースでは、移行するアセットには既にメタデータが入力されており、レンディションは既に生成されています。インスタンス間の移動に集中することができます。[!DNL Experience Manager]デプロイメント間で移行する場合は、次の手順を実行します。

1. ワークフローを無効にする：アセットと共にレンディションを移行するので、[!UICONTROL DAMアセットの更新]ワークフローのワークフローランチャーを無効にする必要があります。

1. タグの移行：ソース[!DNL Experience Manager]デプロイメントには既にタグが読み込まれているので、それらをコンテンツパッケージにビルドして、ターゲットインスタンスにパッケージをインストールできます。

1. アセットの移行：ある[!DNL Experience Manager]デプロイメントから別のデプロイメントにアセットを移動する場合に推奨されるツールは2つあります。

   * **Vaultリモートコ** ピーまたはvlt rcpを使用すると、ネットワークを介してvltを使用できます。移動元と移動先のディレクトリを指定すると、vit がすべてのリポジトリデータを一方のインスタンスからダウンロードし、もう一方に読み込みます。vt rcp については、[https://jackrabbit.apache.org/filevault/rcp.html](https://jackrabbit.apache.org/filevault/rcp.html) に記載されています。
   * **Grabbit**[!DNL Experience Manager]。Time Warner Cable が の実装のために開発した、オープンソースのコンテンツ同期ツールです。継続的なデータストリームを使用するので、vlt rcp と比較して待ち時間が少なく、vlt rcp の 2 倍から 10 倍高速であると言われています。また、Grabbit はデルタコンテンツのみの同期をサポートし、最初の移行パスが完了した後に加えられた変更を同期できます。

1. アセットのアクティベート：[!DNL Experience Manager]への最初の移行については、[アセット](#activating-assets)のアクティベートの手順に従って進めてください。

1. 公開のクローン：新しい移行と同様に、1つのパブリッシュインスタンスを読み込み、クローンを作成する方が、両方のノードでコンテンツをアクティブ化するよりも効率的です。 [パブリッシュインスタンスのクローン](#cloning-publish)を参照してください。

1. ワークフローの有効化：移行が完了したら、 [!UICONTROL DAMアセットの更新]ワークフローのランチャーを再度有効にして、レンディションの生成とメタデータの抽出をサポートし、稼動中のシステムで日常的に使用できるようにします。
