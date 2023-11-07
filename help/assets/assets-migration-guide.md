---
title: アセットを一括で移行する
description: ' [!DNL Adobe Experience Manager] へのアセットの移行、メタデータの適用、レンディションの生成、パブリッシュインスタンスでのアクティベートをそれぞれ行う方法について説明します。'
contentOwner: AG
role: Architect, Admin
feature: Migration,Renditions,Asset Management
exl-id: 184f1645-894a-43c1-85f5-8e0d2d77aa73
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1795'
ht-degree: 58%

---

# アセットを一括で移行する方法 {#assets-migration-guide}

アセットを [!DNL Adobe Experience Manager] に移行する際には、いくつかの手順を考慮する必要があります。現在のホームからアセットやメタデータを抽出する方法は、実装環境により方法が大きく異なるのでこのドキュメントでは説明しません。本書では、抽出したアセットを [!DNL Experience Manager] に移行してメタデータを適用し、レンディションを生成してそれらをパブリッシュインスタンスでアクティベートする方法について説明します。

## 前提条件 {#prerequisites}

この方法に従って実際に手順を実行する前に、[Assets パフォーマンスチューニングに関するヒント](performance-tuning-guidelines.md)のガイダンスを確認して実践してください。最大同時ジョブ数の設定など、多くの手順では、負荷時のサーバーの安定性とパフォーマンスが大幅に向上します。 ファイルデータストアの設定など、他の手順は、システムがアセットを読み込んだ後は、実行するのがはるかに困難です。

>[!NOTE]
>
>次のアセット移行ツールは [!DNL Experience Manager] の一部ではないので、Adobe ではサポートしていません。
>
>* ACS AEM ツールの Tag Maker
>* ACS AEM Tools CSV Asset Importer
>* ACS Commons Bulk Workflow Manager
>* ACS Commons Fast Action Manager
>* 合成ワークフロー
>
>このソフトウェアはオープンソースで、[Apache v2 License](https://adobe-consulting-services.github.io/pages/license.html) が適用されます。質問や問題を報告するには、それぞれ [ACS AEM ツール](https://github.com/Adobe-Consulting-Services/acs-aem-commons/issues)と [ACS AEM Commons に関する GitHub の問題](https://github.com/Adobe-Consulting-Services/acs-aem-tools/issues)を利用してください。

## [!DNL Experience Manager] への移行 {#migrating-to-aem}

[!DNL Experience Manager] にアセットを移行するにはいくつかの手順を経る必要があるので、フェーズ別に処理することをお勧めします。移行の段階は次のとおりです。

1. ワークフローの無効化.
1. タグの読み込み.
1. アセットの取り込み.
1. レンディションの処理.
1. アセットのアクティベート.
1. ワークフローを有効化する.

![chlimage_1-223](assets/chlimage_1-223.png)

### ワークフローの無効化 {#disabling-workflows}

移行を開始する前に、[!UICONTROL DAM アセットの更新]ワークフローのランチャーを無効化します。すべてのアセットをシステムに取り込んでから、ワークフローをバッチで実行することをお勧めします。 移行中に既にライブ状態になっている場合は、これらのアクティビティを非稼働時に実行するようにスケジュールできます。

### タグの読み込み {#loading-tags}

画像に適用するタグ分類は既に用意されていることがあります。CSV Asset Importer などのツールや [!DNL Experience Manager] のメタデータプロファイルのサポートにより、タグをアセットに適用する処理は自動化できますが、タグをシステムに読み込む必要があります。[ACS AEM ツールの Tag Maker](https://adobe-consulting-services.github.io/acs-aem-tools/features/tag-maker/index.html) 機能を使用すると、システムに読み込まれた Microsoft Excel のスプレッドシートを使用してタグを入力できます。

### アセットの取り込み {#ingesting-assets}

アセットをシステムに取り込む際には、パフォーマンスと安定性が重要です。 大量のデータをシステムに読み込むので、システムのパフォーマンスを確保し、必要な時間を最小限に抑え、システムの過負荷を回避する必要があります。これは、特に、実稼動環境にあるシステムで発生する可能性があります。

アセットをシステムに読み込む方法には、HTTP を使用したプッシュベースのアプローチと、JCR API を使用したプルベースのアプローチの 2 つがあります。

#### HTTP 経由で送信 {#pushing-through-http}

AdobeのManaged Servicesチームは、Glutton と呼ばれるツールを使用して、顧客環境にデータを読み込みます。 Glutton は小さな Java アプリケーションであり、[!DNL Experience Manager] のデプロイメントでディレクトリから別のディレクトリにすべてのアセットを読み込みます。Glutton の代わりに、Perl スクリプトなどのツールを使用してアセットをリポジトリに投稿することもできます。

HTTPS を通じたプッシュのアプローチには、主に次の 2 つの欠点があります。

1. アセットは HTTP 経由でサーバーに送信する必要があります。 これにはかなりのオーバーヘッドが必要で、時間がかかるので、移行の実行に要する時間が長くなります。
1. アセットに適用する必要があるタグとカスタムメタデータがある場合、このアプローチでは 2 つ目のカスタムプロセスが必要です。読み込んだメタデータをアセットに適用するには、次の手順を実行する必要があります。

アセットを取り込むもう 1 つの方法は、ローカルファイルシステムからアセットを取り込むことです。 ただし、プルベースのアプローチを実行するために外部ドライブやネットワーク共有をサーバーにマウントできない場合は、HTTP 経由でアセットを投稿するのが最適なオプションです。

#### ローカルファイルシステムからの取得 {#pulling-from-the-local-filesystem}

[ACS AEM ツールの CSV Asset Importer](https://adobe-consulting-services.github.io/acs-aem-tools/features/csv-asset-importer/index.html) は、アセットをファイルシステムから、アセットメタデータをアセット読み込み用の CSV ファイルから、それぞれ取り込みます。Experience Manager の Asset Manager API を使用して、アセットをシステムに取り込み、設定したメタデータプロパティを適用します。アセットは、ネットワークファイルマウント経由または外部ドライブ経由でサーバーにマウントするのが理想的です。

アセットをネットワーク経由で転送する必要がないので、全体的なパフォーマンスが大幅に向上します。通常、この方法は、アセットをリポジトリに読み込む最も効率的な方法と見なされます。 また、このツールはメタデータの取り込みをサポートしているので、すべてのアセットとメタデータを 1 つの手順で読み込むことができます。別のツールを使用してメタデータを適用する 2 つ目の手順を作成する必要もあります。

### レンディションの処理 {#processing-renditions}

アセットをシステムに読み込んだ後、メタデータを抽出してレンディションを生成するには、[!UICONTROL DAM アセットの更新]ワークフローを通じてアセットを処理する必要があります。この手順を実行する前に、[!UICONTROL DAM アセットの更新]ワークフローをニーズに合わせて複製および変更する必要があります。既製のワークフローには、Dynamic Media PTIFF の生成や [!DNL InDesign Server] の統合など、ユーザーによっては必要でない手順が多く含まれています。

ニーズに合わせてワークフローを設定したら、次の 2 つの方法のいずれかで実行できます。

1. 最も簡単な方法は次のとおりです。 [ACS Commons の Bulk Workflow Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/bulk-workflow-manager.html). このツールを使用すると、クエリを実行し、ワークフローを通じてクエリの結果を処理できます。 バッチサイズを設定するオプションもあります。
1. [ACS Commons の Fast Action Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html) は[合成ワークフロー](https://adobe-consulting-services.github.io/acs-aem-commons/features/synthetic-workflow.html)と組み合わせて使用できます。このアプローチはより複雑ですが、[!DNL Experience Manager] ワークフローエンジンのオーバーヘッドを削除し、サーバーリソースの使用を最適化します。さらに、Fast Action Manager はサーバーリソースを動的に監視し、システムに配置された読み込みをスロットリングすることでパフォーマンスを大幅に向上します。サンプルスクリプトは ACS Commons の機能ページに記載されています。

### アセットのアクティベート {#activating-assets}

パブリッシュ層を持つデプロイメントの場合は、パブリッシュファームに対してアセットをアクティベートする必要があります。 Adobeでは、複数のパブリッシュインスタンスを実行することをお勧めしますが、すべてのアセットを 1 つのパブリッシュインスタンスにレプリケートし、そのインスタンスをクローンする方が最も効率的です。 多数のアセットをアクティベートするときは、ツリーのアクティベートを実行した後に、干渉する必要が生じる場合があります。理由は、アクティベートをトリガーするときに、Sling のジョブやイベントキューに項目が追加されるからです。このキューのサイズが約 40,000 項目を超え始めると、処理が大幅に遅くなります。 このキューのサイズが 100,000 項目を超えると、システムの安定性に影響が出始めます。

この問題を回避するには、 [Fast Action Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html) アセットのレプリケーションを管理します。 これは、Sling キューを使用せずに動作し、オーバーヘッドを削減しながら、ワークロードを調整してサーバーが過負荷になるのを防ぎます。 FAM を使用してレプリケーションを管理する例は、機能のドキュメントページに示されています。

アセットをパブリッシュファームに移行するその他のオプションは、[vlt-rcp](https://jackrabbit.apache.org/filevault/rcp.html) または [oak-run](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run) を使用する方法です。これらは Jackrabbit の一部のツールとして提供されます。[!DNL Experience Manager] インフラストラクチャにオープンソースツール [Grabbit](https://github.com/TWCable/grabbit) を使用する方法もあります。vlt よりも高いパフォーマンスを発揮すると言われています。

これらのアプローチで注意すべき点は、オーサーインスタンス上でアセットがアクティベートされていると表示されないことです。アセットのアクティベート状態を正しくフラグ設定するには、アセットをアクティベート済みとマークする別のスクリプトも実行する必要があります。

>[!NOTE]
>
>Adobeは Grabbit を維持またはサポートしていません。

### パブリッシュをクローン化する {#cloning-publish}

アセットがアクティベートされたら、パブリッシュインスタンスを複製して、デプロイメントに必要な数のコピーを作成できます。 サーバーのクローン作成は非常に簡単ですが、覚えておくべき重要な手順がいくつかあります。 公開を複製するには：

1. ソースインスタンスとデータストアをバックアップします。
1. インスタンスとデータストアのバックアップをターゲットの場所に復元します。 以下の手順はすべて、この新しいインスタンスを参照します。
1. `crx-quickstart/launchpad/felix` でファイルシステムの検索を実行し、`sling.id` を探します。このファイルを削除します。
1. データストアのルートパスで、`repository-XXX` ファイルを探してすべて削除します。
1. `crx-quickstart/install/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config` と `crx-quickstart/launchpad/config/org/apache/jackrabbit/oak/plugins/blob/datastore/FileDataStore.config` を編集し、新しい環境のデータストアの場所を指すようにします。
1. 環境を起動します。
1. オーサー環境にあるすべてのレプリケーションエージェントが正しいパブリッシュインスタンスを指す、または新しいインスタンスの Dispatcher のフラッシュエージェントが新しい環境の正しい Dispatcher を参照するように設定を更新します。

### ワークフローを有効化する {#enabling-workflows}

移行が完了したら、レンディションの生成とメタデータの抽出をサポートするために [!UICONTROL DAM の更新アセット]ワークフローのランチャーを再度有効化し、稼働中のシステムが日常的に使用できるようにします。

## [!DNL Experience Manager] デプロイメントを超えた移行 {#migrating-between-aem-instances}

それほど一般的ではないものの、ある [!DNL Experience Manager] デプロイメントから別のデプロイメントに大量のデータを移行する必要があります。例えば、[!DNL Experience Manager] のアップグレードを実行したり、ハードウェアをアップグレードをしたり、新しいデータセンターへの移行（AMS の移行）を実行する場合です。

この場合、アセットには既にメタデータが入力されており、レンディションは既に生成されています。 あるインスタンスから別のインスタンスへのアセットの移動に集中するだけで済みます。 [!DNL Experience Manager] デプロイメント間で移行を行うには、次の手順を実行します。

1. ワークフローランチャーを無効化する：他のアセットとともに共にレンディションを移行するするため、[!UICONTROL DAM の更新アセット]ワークフローのランチャーを無効にする必要があります。

1. タグを移行する：タグは既にソースの [!DNL Experience Manager] デプロイメントに読み込まれているため、コンテンツパッケージでタグをビルドした後、パッケージ自体をターゲットデプロイメントにインストールできます。

1. アセット移行する：[!DNL Experience Manager]デプロイメントから別のデプロイメントにアセットを移行する場合に推奨されるツールは次の 2 つです。

   * **Vault リモートコピー** vlt rcp を使用すると、ネットワーク全体で vlt を使用できます。 移動元と移動先のディレクトリを指定すると、vit がすべてのリポジトリデータを一方のインスタンスからダウンロードし、もう一方に読み込みます。vt rcp については、[https://jackrabbit.apache.org/filevault/rcp.html](https://jackrabbit.apache.org/filevault/rcp.html) に記載されています。
   * **Grabbit**：Time Warner Cable が自社の [!DNL Experience Manager] 実装のために開発したオープンソースのコンテンツ同期ツールです。連続したデータストリームを使用するので、vlt rcp と比べて待ち時間が短く、vlt rcp の 2～10 倍の速さで速度が向上します。 また、Grabbit では、差分コンテンツの同期のみがサポートされ、最初の移行パスが完了した後に変更を同期できます。

1. アセットを有効にする：[アセットの有効化](#activating-assets)については、[!DNL Experience Manager] に初めて移行する際の手順について記載された説明に従ってください。

1. パブリッシュをクローン化する：新規の移行の場合と同様に、1 つのパブリッシュインスタンスを読み込んでクローン化する方が、両方のノードでコンテンツを有効にするよりも効率的です。[パブリッシュインスタンスのクローン](#cloning-publish)を参照してください。

1. ワークフローを有効にする：移行が完了したら、[!UICONTROL DAM の更新アセット]ワークフローのランチャーを再び有効にして、レンディションの生成とメタデータの抽出をサポートし、日常的なシステムの利用を継続できるようにします。
