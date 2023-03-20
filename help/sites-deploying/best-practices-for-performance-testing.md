---
title: パフォーマンステストのベストプラクティス
seo-title: Best Practices for Performance Testing
description: この記事では、パフォーマンステストに使用される全体的な戦略と方法論の概要と、プロセスを支援するツールの一部について説明します。
seo-description: This article outlines the overall strategies and methodologies used for performance testing as well as some of the tools that are available to assist in the process.
uuid: ab8720d6-b864-4d00-9e07-2e1699cfe7db
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 669018a0-f6ef-42b2-9c6f-83d7dd5a7095
exl-id: fcac75e1-15c1-4a37-8d43-93c95267b903
source-git-commit: 30327950779337ce869b6ca376120bc09826be21
workflow-type: tm+mt
source-wordcount: '1898'
ht-degree: 29%

---

# パフォーマンステストのベストプラクティス{#best-practices-for-performance-testing}

## はじめに {#introduction}

パフォーマンステストは、AEMのデプロイメントの重要な部分です。 お客様の要件に応じて、パブリッシュインスタンス、オーサーインスタンス、またはその両方でパフォーマンステストを実行できます。

このドキュメントでは、パフォーマンステストを実行する全体的な戦略と方法論の概要と、Adobeがプロセスを支援するために提供するツールの一部を説明します。 最後に、コード分析とシステム設定の両方の観点から、パフォーマンスチューニングに役立つAEM 6 で利用可能なツールの一部を分析します。

### 現実をシミュレートする {#simulating-reality}

パフォーマンステストを実行する際に最も重要なのは、実稼動環境をできるだけ模倣できるようにすることです。 これは困難な場合が多いですが、これらのテストの正確性を確認することが不可欠です。 パフォーマンステストの設計に取り組む際は、次の点を考慮に入れることが重要です。

* 実稼動用コンテンツ

AEMでの多くのパフォーマンス測定（クエリ応答時間など）は、システム上のコンテンツのサイズの影響を受ける場合があります。 テスト環境で、実稼動データのコピーをできるだけ近くに配置することが重要です。

* 実稼動コード

実稼動環境でデプロイするAEMのバージョンとホットフィックスは、テスト環境で同じにする必要があります。 また、実稼動環境にデプロイされるコードのバージョンをテストすることも重要です。

* 本番用のハードウェアとネットワーク構成

テストは、実稼働環境にできるだけ近い環境がないと意味をなします。 理想的には、ハードウェア仕様、ネットワークインターフェイス、ロードバランサー、CDN は、テスト環境の実稼動環境と同じにする必要があります。

* 実稼動負荷

システムの負荷が高くなるまで、パフォーマンスの問題は多く見られません。 優れたパフォーマンステストは、実稼動システムがピーク時に低下する負荷をシミュレートする必要があります。

### 目標の設定 {#setting-goals}

パフォーマンステストを開始する前に、負荷と応答時間を指定するために、機能しない要件を設定する必要があります。 既存のシステムから移行する場合は、応答時間が現在の実稼動時間と同じ値であることを確認します。 負荷の場合、現在のピーク負荷を 2 倍にするのが最適です。 これにより、Web サイトが成長しても、引き続き適切にパフォーマンスを維持できます。

### ツール {#tools}

市販のパフォーマンステストツールは数多く存在します。負荷発生ツールを実行するときは、テストを実行するコンピューターに十分なネットワーク帯域幅を用意することが重要です。そうしないと、テストマシンが接続の制限に達した後は、テスト中の環境に追加の負荷が生成されません。

#### テストツール {#testing-tools}

* Adobe **Tough Day** ツールを使用して、AEMインスタンスに負荷を生成し、パフォーマンスデータを収集できます。 AdobeのAEMエンジニアリングチームは、実際にはこのツールを使用してAEM製品自体の読み込みテストを実行します。 Tough Day で実行されるスクリプトは、プロパティファイルと JMX XML ファイルを介して設定されます。 詳しくは、 [Tough Day のドキュメント](/help/sites-developing/tough-day.md).

* AEMには、すぐに使用できるツールが用意されており、問題のあるクエリ、リクエスト、エラーメッセージをすばやく確認できます。 詳しくは、 [診断ツール](/help/sites-administering/operations-dashboard.md#diagnosis-tools) 操作ダッシュボードのドキュメントの節を参照してください。
* Apache は、 **JMeter** これは、機能的な動作だけでなく、パフォーマンスや負荷のテストにも使用できます。 オープンソースのソフトウェアであり、自由に使用できますが、エンタープライズ製品よりも機能セットが小さく、学習曲線が急激です。 JMeter は Apache の Web サイト ( [https://jmeter.apache.org/](https://jmeter.apache.org/)

* **Load Runner** はエンタープライズレベルの負荷テスト製品です。無償の評価版も提供されています。詳しくは、 [https://www.microfocus.com/en-us/products/loadrunner-load-testing/overview](https://www.microfocus.com/en-us/products/loadrunner-load-testing/overview) を参照してください。

* クラウドベースの負荷テストツール ( [Neustar](https://www.neustar.biz/services/web-performance/load-testing) また、を使用することもできます。
* モバイル Web サイトやレスポンシブ Web サイトをテストする場合は、別のツールセットを使用する必要があります。 ネットワーク帯域幅を制限し、3G や EDGE などの低速なモバイル接続をシミュレートすることで機能します。 広く利用されているツールには以下のものがあります。

   * **[Network Link Conditioner](https://nshipster.com/network-link-conditioner/)** - 簡単に使用できる UI を備えており、またかなり低いレベルのネットワークスタックで動作します。OS X と iOS のバージョンがあります。
   * [**Charles**](https://www.charlesproxy.com/) - ネットワーク制限を使用できる Web デバッグプロキシアプリケーションです。他にも用途がいくつかあります。提供されているバージョンは、Windows、OS X および Linux です。

#### 最適化ツール {#optimization-tools}

**監視**

[パフォーマンスの監視](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance)では、問題の診断と調整すべき領域の特定に役立つツールと方法について説明しています。

**タッチ UI の開発者モード**

AEM 6 のタッチ操作対応 UI の新機能の 1 つに、開発者モードがあります。 作成者が編集モードとプレビューモードを切り替える場合と同様に、開発者はオーサー UI で開発者モードに切り替えて、ページ上の各コンポーネントのレンダリング時間を確認したり、エラーのスタックトレースを確認したりできます。 デベロッパーモードについて詳しくは、次を参照してください。 [CQ Gems プレゼンテーション](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2014/aem-developer-mode.html?lang=en).

**rlog.jar を使用した要求ログの読み取り**

AEM システムのリクエストログをより包括的に分析するには、`rlog.jar` を使用して、AEM で生成される `request.log` の検索および並べ替えをおこなうことができます。この jar ファイルは、AEM インストールの `/crx-quickstart/opt/helpers` フォルダーにあります。rlog ツールとリクエストログ全般について詳しくは、 [監視と保守](/help/sites-deploying/monitoring-and-maintaining.md) ドキュメント。

**クエリの説明を実行ツール**

この [クエリの説明を実行ツール](/help/sites-administering/operations-dashboard.md#explain-query) の ACS AEMツールは、クエリの実行時に使用されるインデックスを表示するために使用できます。 これは、低速で実行するクエリを最適化する場合に非常に役立ちます。

**PageSpeed ツール**

Googleの PageSpeed ツールは、ページパフォーマンスのベストプラクティスに準拠したサイト分析と、Apache インスタンス上の Dispatcher と一緒にインストールして、さらに最適化をおこなうためのプラグインを提供します。 詳しくは、[PageSpeed ツールの web サイト](https://developers.google.com/speed/pagespeed/)を参照してください。

## オーサー環境 {#author-environment}

### テストの実行 {#performing-tests}

オーサー環境でパフォーマンステストを実行するには、実稼働の作成者のエクスペリエンスをシミュレートする必要があります。つまり、オーサーインスタンスの環境に、コンポーネント、OSGi バンドル、UI カスタマイズ、カスタムインデックスなど、実稼動環境のオーサーインスタンスに配置される様々な追加要素をすべて含めておく必要があります。

パフォーマンスおよび負荷テスト用に設計された、多くの自動化フレームワークを使用できます。 カスタムスクリプトをこれらのツールに記録し、再生して、同様のコンテンツ作成とアクティベーションアクティビティを同時に実行する、最も多くの作成者をシミュレートできます。 Tough Day ツールを使用して、数千のアセットのアップロードや大量のページのアクティベートなどのアクティビティをシミュレートすることをお勧めします。

高負荷のアセット読み込みやページオーサリングが必要になるような環境では、Tough Day のようなツールを使用して、ピーク時の負荷でも環境が効率的に動作するかを確認することが必要です。[WebDAV](/help/sites-administering/webdav-access.md) はスクリプトを必要としないツールで、大量のアセットを読み込むためにも使用できます。

#### MongoDB 固有の手順 {#mongodb-specific-steps}

MongoDB バックエンドを備えたシステムでは、AEMは、次の機能を提供します。 [JMX](/help/sites-administering/jmx-console.md) 読み込みテストまたはパフォーマンステストを実行する際に監視する必要がある MBean:

* この **統合キャッシュ統計** MBean。 次の場所から直接アクセスできます。

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D6%2Cname%3D%22Consolidated+Cache+statistics%22%2Ctype%3D%22ConsolidatedCacheStats%22`

**Document-Diff** という名前のキャッシュは、ヒット率を `.90` 以上にする必要があります。ヒット率が 90 ％を下回る場合は、`DocumentNodeStoreService` の設定を変更しなければならない可能性があります。Adobeの製品サポートでは、環境に最適な設定をレコメンデーションできます。

* この **Oak リポジトリ統計** Mbean。 次の場所から直接アクセスできます。

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D16%2Cname%3D%22Oak+Repository+Statistics%22%2Ctype%3D%22RepositoryStats%22`

この **ObservationQueueMaxLength** セクションには、過去数時間、分、秒、週にわたる Oak の監視キュー内のイベント数が表示されます。 「per hour」セクションで最も多くのイベントを見つけます。 この数は、`oak.observation.queue-length` 設定と比較する必要があります。監視キューに表示される最大数が `queue-length` 設定を超える場合：

1. パラメーター `oak.observation.queue‐length=50000` を含む `com.adobe.granite.repository.impl.SlingRepositoryManager.cfg` という名前のファイルを作成します。
1. /crx-quickstart/install フォルダーの下に配置します。

>[!NOTE]
>[AEM 6.x | パフォーマンスチューニングのヒント](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html)の KB 記事も参照してください。 

初期設定は 10,000 ですが、ほとんどの環境では、通常は 20,000 または 50,000 まで引き上げる必要があります。

## パブリッシュ環境 {#publish-environment}

### テストの実行 {#performing-tests-1}

読み込みテストをおこなう必要があるデプロイメントの最も重要な部分は、パブリッシュ環境または Dispatcher 環境に面しているエンドユーザーです。

サードパーティの自動テストツールを使用して、Web サイトのパフォーマンスをテストできます。 こうしたツールを使用すると、ユーザーがサイト上でおこなう手順を記録したうえで、その手順を同時にいくつも実行し、実稼動 Web サイトと同様の負荷をシミュレートできます。

ほとんどの実稼動 Web サイトでは、Dispatcher のキャッシュやコンテンツ配信ネットワークなどの最適化がおこなわれています。 テスト時に、これらの最適化がテスト環境でも利用できることを確認する必要があります。 エンドユーザーの応答時間の監視に加えて、パブリッシュサーバーと Dispatcher のシステム指標を監視して、システムがハードウェアリソースに制限されないようにする必要があります。

高度なパーソナライゼーションを必要としないシステムでは、Dispatcher がほとんどの要求をキャッシュする必要があります。 その結果、パブリッシュインスタンスの負荷は比較的平坦なままにする必要があります。 高度なパーソナライゼーションが必要な場合は、可能な限り多くの Dispatcher のキャッシュを可能にするよう、パーソナライズされたコンテンツに iFrames やAJAXリクエストなどのテクノロジーを使用することをお勧めします。

基本的なテストでは、Apache Bench を使用して Web サーバーの応答時間を測定し、メモリリークなどの測定に必要な負荷を作成できます。 詳しくは、 [監視に関するドキュメント](/help/sites-deploying/monitoring-and-maintaining.md#apache-bench).

## パフォーマンスの問題のトラブルシューティング {#troubleshooting-performance-issues}

オーサーインスタンスでパフォーマンステストを実行した後、問題を調査、診断および対処する必要があります。 分析を実行し、問題に対処する際に、次のいくつかのツールと手法を使用できます。

* 以下を調べることができます。 [リクエストパフォーマンスログ](/help/sites-administering/operations-dashboard.md#request-performance) 」をクリックします。 このツールは、低速なページリクエストを識別するために使用できます
* [クエリパフォーマンスツール](/help/sites-administering/operations-dashboard.md#query-performance)で実行が遅いクエリを分析します。

* エラーや警告のエラー行を確認します。 詳しくは、 [ログ](/help/sites-deploying/configure-logging.md)
* メモリと CPU の使用率、ディスク I/O、ネットワーク I/O などのシステムハードウェアリソースを監視します。多くの場合、これらのリソースはパフォーマンスのボトルネックの原因となります
* 可能な限りキャッシュを許可するように、ページのアーキテクチャと、URL パラメーターの使用を最小限に抑える方法を最適化します
* [パフォーマンスの最適化](/help/sites-deploying/configuring-performance.md)と [Performance tuning tips](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html) のドキュメントに従ってください。

* オーサーインスタンス上の特定のページやコンポーネントの編集に問題がある場合は、タッチ UI 開発者モードを使用して、該当するページを調べます。 これにより、ページ上の各コンテンツ領域の分類と読み込み時間が提供されます
* サイト上のすべての JS と CSS を縮小します。 この方法について詳しくは、 [ブログ投稿](https://blogs.adobe.com/foxes/enable-js-and-css-minification/).
* 埋め込まれた CSS および JS をコンポーネントから削除します。 ページのレンダリングに必要な要求の数を最小限に抑えるために、ページをクライアント側ライブラリに含めて縮小する必要があります
* Chrome の「ネットワーク」タブなどのブラウザーツールを使用して、サーバーリクエストを調べ、最も長くかかっているサーバーを確認します。

問題の領域を特定したら、パフォーマンスの最適化のためにアプリケーションコードを調べます。AEM の組み込みの機能が適切に実行されない場合は、アドビのサポートが対応します。
