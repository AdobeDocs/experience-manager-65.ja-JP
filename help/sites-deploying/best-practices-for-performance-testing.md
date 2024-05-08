---
title: パフォーマンステストのベストプラクティス
description: パフォーマンステストに使用される全体的な戦略と方法論、およびプロセスの支援に役立ついくつかのツールについて説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: fcac75e1-15c1-4a37-8d43-93c95267b903
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '1790'
ht-degree: 100%

---

# パフォーマンステストのベストプラクティス{#best-practices-for-performance-testing}

## はじめに {#introduction}

パフォーマンステストは、AEM デプロイメントの重要な部分です。顧客の要件に応じて、パブリッシュインスタンス、オーサーインスタンス、またはその両方でパフォーマンステストを実行できます。

このドキュメントでは、パフォーマンステストを実行するための全体的な戦略と方法論、およびプロセスを支援するためにアドビが提供するいくつかのツールについて説明します。最後に、コード分析とシステム設定の両方の観点から、AEM 6 で使用可能なパフォーマンスの調整に役立つツールをいくつか取り上げます。

### 実際の環境に近いシミュレーション {#simulating-reality}

パフォーマンステストを実行する際は、できるだけ実稼動環境に近い環境を再現してください。多くの場合、これは難しい課題ですが、テストの精度を確保するためには不可欠です。パフォーマンステストを設計する際には、次の点を考慮することが重要です。

* 実稼動環境と同様のコンテンツ

クエリ応答時間など、AEM でのパフォーマンス測定の多くは、システム上のコンテンツのサイズの影響を受ける可能性があります。テスト環境では、実稼動データをできるだけ正確にコピーしたデータを使用することが重要です。

* 実稼動環境のコード

テスト環境にも、実稼動環境と同じ AEM のバージョンとホットフィックスをデプロイする必要があります。また、実稼動環境にデプロイするコードのバージョンでテストを実行することも重要です。

* 実稼動環境と同様のハードウェアとネットワーク設定

有意義なテストを実行するには、実稼動環境にできるだけ近い環境を用意する必要があります。テスト環境でも、実稼動環境と同一のハードウェア仕様、ネットワークインターフェイス、ロードバランサー、CDN を使用するのが理想的です。

* 実稼動環境の負荷

パフォーマンスに関する問題の多くは、システムの負荷が高くなってから判明します。パフォーマンステストの精度を上げるには、実稼動システムがピーク時に受ける負荷の死μレーションを行う必要があります。

### 目標の設定 {#setting-goals}

パフォーマンステストを開始する前に、機能以外の要件を設定して、負荷と応答時間を指定する必要があります。既存のシステムから移行する場合は、応答時間が現在の実稼動環境の値に近いことを確認します。負荷に関しては、現在のピーク時の負荷を 2 倍にするのが最適です。これにより、web サイトが拡大しても十分なパフォーマンスを維持できます。

### ツール {#tools}

市販のパフォーマンステストツールは数多く存在します。負荷発生ツールを実行するときは、テストを実行するコンピューターに十分なネットワーク帯域幅を用意することが重要です。2 倍の負荷を考慮しないと、テストマシンが接続の限界に達した場合に、テスト中の環境により大きな負荷をかけることができません。

#### テストツール {#testing-tools}

* アドビの **Tough Day** ツールを使用すると、AEM インスタンスで負荷を生成してパフォーマンスデータを収集できます。アドビの AEM エンジニアリングチームは実際にこのツールを使用して、AEM 製品の負荷テストを実施しています。Tough Day で実行するスクリプトは、プロパティファイルと JMX XML ファイルを使用して設定します。詳細情報は、[Tough Day のドキュメント](/help/sites-developing/tough-day.md)を参照してください。

* AEM には、問題のあるクエリ、リクエスト、エラーメッセージを迅速に確認するための、すぐに使用できるツールが用意されています。詳細情報は、操作ダッシュボードのドキュメントの[診断ツール](/help/sites-administering/operations-dashboard.md#diagnosis-tools)セクションを参照してください。
* Apache では、パフォーマンスと負荷のテスト、機能動作に使用できる **JMeter** という製品を提供しています。オープンソースソフトウェアであり無料で使用できますが、エンタープライズ製品よりも機能セットが少なく、使い方を覚えるのが簡単です。JMeter は Apache の web サイト（[https://jmeter.apache.org/](https://jmeter.apache.org/)）で入手できます。

* **Load Runner** はエンタープライズレベルの負荷テスト製品です。無償の評価版も提供されています。詳しくは、[https://www.microfocus.com/ja-jp/portfolio/performance-engineering/overview](https://www.microfocus.com/en-us/portfolio/performance-engineering/overview) を参照してください。

* また、[Vercara](https://vercara.com/website-performance-management) などの web サイト負荷テストツールも使用できます。
* モバイル web サイトやレスポンシブ web サイトをテストする際は、別のツールセットを使用する必要があります。こうしたツールでは、ネットワーク帯域幅の制限、3G や EDGE などの低速なモバイル接続のシミュレーションを行えます。広く利用されているツールには以下のものがあります。

   * **[Network Link Conditioner](https://nshipster.com/network-link-conditioner/)** - 簡単に使用できる UI を備えており、またかなり低いレベルのネットワークスタックで動作します。OS X と iOS のバージョンがあります。
   * [**Charles**](https://www.charlesproxy.com/) - ネットワーク制限を使用できる Web デバッグプロキシアプリケーションです。他にも用途がいくつかあります。Windows、OS X および Linux® に対応したバージョンが提供されています。

#### 最適化ツール {#optimization-tools}

**監視**

[パフォーマンスの監視](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance)では、問題の診断と調整すべき領域の特定に役立つツールと方法について説明しています。

**タッチ UI の開発者モード**

AEM 6 のタッチ操作対応 UI の新機能の 1 つに、開発者モードがあります。作成者が編集モードとプレビューモードを切り替えるのと同様に、開発者はオーサー UI でデベロッパーモードに切り替えることができます。これにより、ページ上の各コンポーネントのレンダリング時間を確認し、エラーのスタックトレースを確認できます。デベロッパーモードについて詳しくは、[CQ Gems のプレゼンテーション](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2014/aem-developer-mode.html?lang=ja)を参照してください。

**rlog.jar を使用したリクエストログの解読**

AEM システムのリクエストログをより包括的に分析するには、`rlog.jar` を使用して、AEM で生成される `request.log` の検索および並べ替えをおこなうことができます。この jar ファイルは、AEM インストールの `/crx-quickstart/opt/helpers` フォルダーにあります。rlog ツールとリクエストログ全般について詳しくは、[モニタリングと保守](/help/sites-deploying/monitoring-and-maintaining.md)に関するドキュメントを参照してください。

**クエリの説明を実行ツール**

ACS AEM ツールの[クエリの説明を実行ツール](/help/sites-administering/operations-dashboard.md#explain-query)を使用して、クエリ実行時に使用されるインデックスを表示できます。これは低速なクエリの実行を最適化する場合に便利です。

**PageSpeed ツール**

Google の PageSpeed ツールは、ページパフォーマンスに関するベストプラクティスを実践するためのサイト分析や、さらなる最適化のために Apache インスタンスに Dispatcher と共にインストールできるプラグインを提供します。
詳しくは、[PageSpeed ツールの web サイト](https://developers.google.com/speed)を参照してください。

## オーサー環境 {#author-environment}

### テストの実行 {#performing-tests}

オーサー環境でパフォーマンステストを実行するには、実稼動のオーサーのエクスペリエンスをシミュレートする必要があります。つまり、オーサーインストールには、コンポーネント、OSGi バンドル、UI カスタマイズ、カスタムインデックスなど、実稼動環境のオーサーインスタンスに配置される様々な追加要素をすべて含めておく必要があります。

パフォーマンスと負荷のテスト用に設計された、様々な自動化フレームワークを利用できます。これらのツールでカスタムのスクリプトを記録してから再生することで、類似コンテンツの作成とアクティベートアクティビティを同時に実行する、ピーク時の数でオーサーをのシミュレーションを行うことが可能です。Tough Day ツールを使用し、数千個のアセットのアップロードや、多数のページのアクティベートなどのアクティビティのシミュレーションを行うことを推奨します。

アセットの読み込みやページのオーサリングを頻繁に行う必要がある環境では、Tough Day などのツールを使用することが不可欠です。これにより、負荷のピーク時に環境を効率的に運用できます。[WebDAV](/help/sites-administering/webdav-access.md) はスクリプトを必要としないツールで、大量のアセットを読み込むためにも使用できます。

#### MongoDB 固有の手順 {#mongodb-specific-steps}

バックエンドに MongoDB を使用しているシステムでは、負荷テストまたはパフォーマンステスト時に AEM の以下の [JMX](/help/sites-administering/jmx-console.md) MBean を監視する必要があります。

* **統合キャッシュ統計** MBean。次の場所から直接アクセスできます。

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D6%2Cname%3D%22Consolidated+Cache+statistics%22%2Ctype%3D%22ConsolidatedCacheStats%22`

**Document-Diff** という名前のキャッシュは、ヒット率を `.90` 以上にする必要があります。ヒット率が 90 ％を下回る場合は、`DocumentNodeStoreService` の設定を変更しなければならない可能性があります。お使いの環境に最適な設定はアドビの製品サポートからご案内できます。

* **Oak リポジトリ統計** Mbean。次の場所から直接アクセスできます。

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D16%2Cname%3D%22Oak+Repository+Statistics%22%2Ctype%3D%22RepositoryStats%22`

**ObservationQueueMaxLength** のセクションには、直前の数時間、数分、数秒、数週間の Oak の観測キュー内のイベント数が表示されます。「1 時間あたり」セクションで最も多いイベント数を見つけます。この数を `oak.observation.queue-length` の設定値と比較します。監視キューに表示される最大数が `queue-length` 設定を超える場合：

1. パラメーター `oak.observation.queue‐length=50000` を含む `com.adobe.granite.repository.impl.SlingRepositoryManager.cfg` という名前のファイルを作成します。
1. /crx-quickstart/install フォルダーの下に配置します。

>[!NOTE]
>詳しくは、[AEM 6.x |パフォーマンスチューニングのヒント](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-performance.html?lang=ja)を参照してください

デフォルト設定は 10,000 ですが、ほとんどのデプロイメントでは 20,000 または 50,000 に引き上げる必要があります。

## パブリッシュ環境 {#publish-environment}

### テストの実行 {#performing-tests-1}

負荷テストを行うべきデプロイメントの最も重要な部分は、エンドユーザーが直面するパブリッシュ環境または Dispatcher 環境です。

サードパーティの自動テストツールを使用すると、web サイトのパフォーマンスをテストできます。それらのツールは、ユーザーがサイト上で実行する手順を記録し、そのセッションを同時に多数実行することで、実稼動 web サイトの典型的な負荷をシミュレートできます。

ほとんどの実稼動 web サイトでは、Dispatcher のキャッシュやコンテンツ配信ネットワークなどの最適化が行われています。テスト時には、これらの最適化がテスト環境でも利用できることを確認します。エンドユーザーの応答時間を監視するだけでなく、パブリッシュサーバーと Dispatcher のシステム指標を監視し、システムがハードウェアリソースによる制約を受けていないことを確認します。

高度なパーソナライゼーションを必要としないシステムでは、Dispatcher がほとんどの要求をキャッシュする必要があります。その結果、パブリッシュインスタンスの負荷は比較的平坦に保たれるはずです。高度なパーソナライゼーションが必要な場合は、可能な限り多くの Dispatcher キャッシュを利用できるように、パーソナライズされたコンテンツに iFrames や AJAX リクエストなどのテクノロジーを使用することをお勧めします。

基本的なテストでは、Apache Bench を使用すると web サーバーの応答時間を測定することができ、メモリリークなどの測定に必要な負荷を作成できます。例については、[監視に関するドキュメント](/help/sites-deploying/monitoring-and-maintaining.md#apache-bench)を参照してください。

## パフォーマンスの問題のトラブルシューティング {#troubleshooting-performance-issues}

オーサーインスタンスでパフォーマンステストを実行した後、問題があれば調査、診断、対処するが必要があります。分析を行い、問題に対処する際には、次のようなツールと手法を使用できます。

* 操作ダッシュボードで、[リクエストパフォーマンスログ](/help/sites-administering/operations-dashboard.md#request-performance)を確認できます。このツールを使用すると、低速なページリクエストを特定できます。
* [クエリパフォーマンスツール](/help/sites-administering/operations-dashboard.md#query-performance)で実行が遅いクエリを分析します。

* エラーログで、エラーや警告を確認します。詳しくは、[ログ](/help/sites-deploying/configure-logging.md)を参照してください。
* メモリと CPU の使用率、ディスク I/O、ネットワーク I/O などのシステムハードウェアリソースを監視します。これらのリソースが、パフォーマンスのボトルネックの原因になっていることがよくあります。
* ページのアーキテクチャとページの処理方法を最適化して、URL パラメーターの使用を最小限に抑え、できるだけ多くのキャッシュを可能にします。
* [パフォーマンスの最適化](/help/sites-deploying/configuring-performance.md)と[パフォーマンスチューニングのヒント](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-performance.html?lang=ja)のドキュメントに従ってください。

* オーサーインスタンス上の特定のページやコンポーネントの編集に問題がある場合は、タッチ UI 開発者モードを使用して、該当するページを調べます。これにより、ページ上の各コンテンツ領域の内訳とそれぞれの読み込み時間がわかります。
* サイト上のすべての JS と CSS を最小限にします。この[ブログ投稿](https://blogs.adobe.com/foxes/enable-js-and-css-minification/)を参照してください。
* 埋め込まれた CSS および JS を、コンポーネントから削除します。ページのレンダリングに必要な要求の数を最小限に抑えるには、ページをクライアント側ライブラリに含めて最小化する必要があります。
* サーバーリクエストを調べ、最も長くかかっているリクエストを確認するには、Chrome の「ネットワーク」タブなどのブラウザーツールを使用します。

問題の領域を特定したら、パフォーマンスの最適化のためにアプリケーションコードを調べます。AEM の組み込みの機能が適切に実行されない場合は、アドビのサポートが対応します。
