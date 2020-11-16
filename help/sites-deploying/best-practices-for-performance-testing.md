---
title: パフォーマンステストに関するベストプラクティス
seo-title: パフォーマンステストに関するベストプラクティス
description: この記事では、パフォーマンステストに関する全体的な戦略と使用する方法を概説するほか、そのプロセスのために使用できるいくつかのツールを紹介します。
seo-description: この記事では、パフォーマンステストに関する全体的な戦略と使用する方法を概説するほか、そのプロセスのために使用できるいくつかのツールを紹介します。
uuid: ab8720d6-b864-4d00-9e07-2e1699cfe7db
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 669018a0-f6ef-42b2-9c6f-83d7dd5a7095
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1925'
ht-degree: 91%

---


# パフォーマンステストに関するベストプラクティス{#best-practices-for-performance-testing}

## 概要 {#introduction}

パフォーマンステストは、AEM をデプロイするうえで重要な役割を担っています。顧客の要件に応じて、パブリッシュインスタンスかオーサーインスタンスのどちらか一方またはその両方でパフォーマンステストを実施します。

このドキュメントでは、全体的な戦略とパフォーマンステストの実行方法を概説するほか、アドビが提供するテスト支援ツールをいくつか紹介します。最後に、コード分析とシステム設定の両観点から、AEM 6 でのパフォーマンス調整に役立つツールをいくつか取り上げます。

### 実際の状況に近いシミュレーション {#simulating-reality}

パフォーマンステストを実行するときに最も重要なのは、可能な限り実稼動環境に近い状況を再現することです。これは簡単なことではありませんが、正確なパフォーマンステストをおこなうには不可欠です。パフォーマンステストを設計する際は、以下の点を考慮することが重要です。

* 実稼動環境と同様のコンテンツ

クエリ応答時間など、AEM でのパフォーマンス指標の多くは、システム上のコンテンツのサイズの影響を受けます。実稼動環境のデータにできるだけ近いコピーをテスト環境に用意することが重要です。

* 実稼動環境のコード

実稼動環境でデプロイする AEM のバージョンとホットフィックスは、テスト環境と同じである必要があります。実稼動環境にデプロイするコードのバージョンをテストすることも重要です。

* 実稼動環境と同様のハードウェアとネットワーク設定

意味のあるテストをおこなうには、実稼動環境にできる限り似せた環境を用意することが必要です。できれば、テスト環境と実稼動環境の両方で、同じハードウェア仕様、ネットワークインターフェイス、ロードバランサーおよび CDN を使用することが理想です。

* 実稼動環境の負荷

パフォーマンス問題の多くは、システムが高負荷状態になるまで認識されません。パフォーマンステストでは、実稼動システムのピーク時の負荷をシミュレートする必要があります。

### 目標の設定 {#setting-goals}

パフォーマンステストを開始する前に、負荷と応答時間を指定するための非機能要件を設定する必要があります。既存のシステムから移行する場合は、応答時間が現在の稼動時の値に近いかを確認します。負荷に関しては、現在のピーク負荷の 2 倍を想定します。こうしておけば、Web サイトが拡大しても十分なパフォーマンスが維持されることを保証できます。

### ツール {#tools}

市販のパフォーマンステストツールは数多く存在します。負荷生成ツールを実行する場合は、テストを実行するコンピューターに十分なネットワーク帯域幅があることを確認することが重要です。 そうしないと、テストマシンが接続の限界に達した場合に、テスト対象の環境にさらなる負荷をかけることができなくなります。

#### テストツール {#testing-tools}

* アドビの **Tough Day** ツールは、AEM インスタンスに負荷を発生させ、パフォーマンスデータを収集するために使用できます。AdobeのAEMエンジニアリングチームは、実際にこのツールを使用してAEM製品自体の読み込みテストを実行します。 Tough Day で実行されるスクリプトは、プロパティファイルと JMX XML ファイルによって設定されています。詳しくは、[Tough Day に関するドキュメント](/help/sites-developing/tough-day.md)を参照してください。

* AEM にはすぐに使用できるツールが備わっており、問題のあるクエリ、リクエスト、エラーメッセージを素早く確認できます。詳しくは、操作ダッシュボードのドキュメントの[診断ツール](/help/sites-administering/operations-dashboard.md#diagnosis-tools)の節を参照してください。
* Apache は **JMeter** という製品を提供しています。これは、パフォーマンスおよび負荷テストのほか、機能的性能の確認のために使用できます。オープンソースソフトウェアであり自由に使用できますが、エンタープライズ製品よりも機能セットが少なく、容易に習熟できます。JMeter can be found on Apache’s website at [https://jmeter.apache.org/](https://jmeter.apache.org/)

* **Load Runner** は、エンタープライズグレードの負荷テスト製品です。 無料の評価版が提供されています。 詳しくは、https://www.microfocus.com/en-us/products/loadrunner-load-testing/overviewを参照して [ください。](https://www.microfocus.com/en-us/products/loadrunner-load-testing/overview)

* [Neustar](https://www.neustar.biz/services/web-performance/load-testing) のようなクラウドベースの負荷テストツールも使用できます。
* モバイルまたはレスポンシブ Web サイトをテストする際は、また別のツールセットを使用する必要があります。こうしたツールでは、ネットワーク帯域幅の制限、3G や EDGE などの低速なモバイル接続のシミュレートをおこなえます。広く利用されているツールには以下のものがあります。

   * **[Network Link Conditioner](https://nshipster.com/network-link-conditioner/)** - 簡単に使用できる UI を備えており、またかなり低いレベルのネットワークスタックで動作します。OS X と iOS のバージョンがあります。[](https://nshipster.com/network-link-conditioner/)
   * [**Charles**](https://www.charlesproxy.com/) - ネットワーク制限を使用できる Web デバッグプロキシアプリケーションです。他にも用途がいくつかあります。提供されているバージョンは、Windows、OS X および Linux です。[](https://www.charlesproxy.com/)

#### 最適化ツール {#optimization-tools}

**監視**

[パフォーマンスの監視](/help/sites-deploying/monitoring-and-maintaining.md#monitoring-performance)では、問題の診断と調整すべき領域の特定に役立つツールと方法について説明しています。

**タッチ UI の開発者モード**

AEM 6 のタッチ操作向け UI の新機能の 1 つに、開発者モードがあります。作成者が編集モードとプレビューモードを切り替えられるのと同じように、開発者はオーサー UI で開発者モードに切り替えて、ページ上の各コンポーネントのレンダリング時間の確認と、エラーのスタックトレースの確認ができます。開発者モードについて詳しくは、こちらの [CQ Gems のプレゼンテーション](https://docs.adobe.com/content/ddc/en/gems/aem-6-0-developer-mode.html)を参照してください。

**rlog.jar を使用したリクエストログの解読**

AEM システムのリクエストログをより包括的に分析するには、`rlog.jar` を使用して、AEM で生成される `request.log` の検索および並べ替えをおこなうことができます。This jar file is included with an AEM installation in the `/crx-quickstart/opt/helpers` folder. rlog ツールとリクエストログ全般について詳しくは、[監視と保守](/help/sites-deploying/monitoring-and-maintaining.md)に関するドキュメントの参照してください。

**クエリーの説明を実行ツール**

ACS AEM ツールの[クエリの説明を実行ツール](/help/sites-administering/operations-dashboard.md#explain-query)を使用して、クエリ実行時に使用されるインデックスを表示できます。これは低速なクエリの実行を最適化する場合に非常に便利です。

**PageSpeed ツール**

Google の PageSpeed ツールは、ページパフォーマンスに関するベストプラクティスを実践するためのサイト分析や、さらなる最適化のために Apache インスタンスに Dispatcher と共にインストールできるプラグインを提供します。For more information, see the [PageSpeed Tools Website](https://developers.google.com/speed/pagespeed/).

## オーサー環境 {#author-environment}

### テストの実行 {#performing-tests}

オーサー環境でパフォーマンステストを実行するには、実稼動環境のオーサーインスタンスのエクスペリエンスをシミュレートしなければなりません。つまり、オーサーインスタンスの環境に、コンポーネント、OSGi バンドル、UI カスタマイズ、カスタムインデックスなど、実稼動環境のオーサーインスタンスに配置される様々な追加要素をすべて含めておく必要があります。

パフォーマンステストや負荷テスト用に設計された自動化フレームワークは数多くあります。これらのツールでカスタムのスクリプトを記録して再生することで、同様のコンテンツの作成とアクティベートアクティビティを同時に実行するピーク時のオーサーインスタンスの数をシミュレートすることが可能です。Tough Day ツールを使用し、数千個のアセットのアップロードや多数のページのアクティベートなどのアクティビティをシミュレートすることを推奨します。

高負荷のアセット読み込みやページオーサリングが必要になるような環境では、Tough Day のようなツールを使用して、ピーク時の負荷でも環境が効率的に動作するかを確認することが必要です。[WebDAV](/help/sites-administering/webdav-access.md) はスクリプトを必要としないツールで、大量のアセットを読み込むためにも使用できます。

#### MongoDB 固有の手順 {#mongodb-specific-steps}

バックエンドに MongoDB を使用しているシステムでは、負荷テストまたはパフォーマンステスト時に AEM の以下の [JMX](/help/sites-administering/jmx-console.md) MBean を監視する必要があります。

* **統合キャッシュ統計** MBean。次の場所に移動して、直接アクセスできます。

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D6%2Cname%3D%22Consolidated+Cache+statistics%22%2Ctype%3D%22ConsolidatedCacheStats%22`

For the cache named **Document-Diff**, the hit rate should be over `.90`. ヒット率が 90 ％を下回る場合は、`DocumentNodeStoreService` の設定を変更しなければならない可能性があります。お使いの環境に最適な設定はアドビの製品サポートからご案内できます。

* **Oak リポジトリ統計** Mbean。次の場所に移動して、直接アクセスできます。

`https://server:port/system/console/jmx/org.apache.jackrabbit.oak%3Aid%3D16%2Cname%3D%22Oak+Repository+Statistics%22%2Ctype%3D%22RepositoryStats%22`

**ObservationQueueMaxLength** のセクションには、直前の数時間、数分、数秒、数週間の Oak の観測キュー内のイベント数が表示されます。「per hour」のセクションでイベントの最大数を確認します。この数値を、`oak.observation.queue-length`OSGi コンソール&#x200B;**の** SlingRepositoryManager[ コンポーネントで確認できる](/help/sites-deploying/web-console.md) の設定と比較する必要があります。観測キューで表示される最大数が `queue-length` の設定を上回る場合は、設定の引き上げに関してアドビのサポートまでお問い合わせください。初期設定は 1,000 ですが、ほとんどの環境では、通常は 20,000 または 50,000 まで引き上げる必要があります。

## パブリッシュ環境 {#publish-environment}

### テストの実行 {#performing-tests-1}

負荷テストの対象となるデプロイメントで最も重要なのは、エンドユーザーに対面するパブリッシュ環境または Dispatcher 環境です。

このような Web サイトのパフォーマンスは、サードパーティの自動テストツールを使用してテストできます。こうしたツールを使用すると、ユーザーがサイト上でおこなう手順を記録したうえで、その手順を同時にいくつも実行し、実稼動 Web サイトと同様の負荷をシミュレートできます。

ほとんどの実稼動 Web サイトでは、Dispatcher キャッシュやコンテンツ配信ネットワークなどの最適化機能が導入されています。テスト時は、こうした最適化機能がテスト環境でも利用できるどうかを確認する必要があります。エンドユーザーの応答時間の監視に加えて、システムがハードウェアリソースによる制約を受けていないことを確認するために、パブリッシュサーバーと Dispatcher のシステム指標を監視する必要があります。

高度なパーソナライゼーションを必要としないシステムでは、Dispatcher がほとんどのリクエストをキャッシュする必要があります。これにより、パブリッシュインスタンスの負荷を比較的一定に保つことができます。高度なパーソナライゼーションが必要な場合は、可能な限り Dispatcher キャッシュを利用できるよう、パーソナライズされたコンテンツに iFrames や AJAX リクエストなどのテクノロジーを使用することを推奨します。

基本的なテストの場合は、Apache Bench を使用して Web サーバーの応答時間を測定し、メモリリークなどの問題を測定するための負荷を生成できます。詳しくは、[監視に関するドキュメント](/help/sites-deploying/monitoring-and-maintaining.md#apache-bench)の例を参照してください。

## パフォーマンス問題のトラブルシューティング {#troubleshooting-performance-issues}

オーサーインスタンスでパフォーマンステストを実行した後に、問題が発生した場合は、調査、診断および対応をおこなう必要があります。問題の分析と対応をおこなう際には、いくつかのツールと手法を使用できます。

* 操作ダッシュボードで[要求パフォーマンスログ](/help/sites-administering/operations-dashboard.md#request-performance)を確認できます。このツールを使用して低速なページリクエストを特定できます。
* [クエリパフォーマンスツール](/help/sites-administering/operations-dashboard.md#query-performance)で実行が遅いクエリを分析します。

* エラーログを見てエラーや警告を調べます。詳しくは、[ログ](/help/sites-deploying/configure-logging.md)を参照してください。
* メモリや CPU の使用状況のなどシステムのハードウェアリソースを監視します。これらのリソースが、パフォーマンスボトルネックの原因になっていることがよくあります。
* キャッシュを最大限に確保するために、ページのアーキテクチャと、URL パラメーターの使用を最小限に抑えるための仕組みを最適化します。
* [パフォーマンスの最適化](/help/sites-deploying/configuring-performance.md)と [Performance tuning tips ](https://helpx.adobe.com/jp/experience-manager/kb/performance-tuning-tips.html) のドキュメントに従ってください。

* オーサーインスタンスでの特定のページやコンポーネントの編集に問題がある場合は、タッチ UI の開発者モードを使用して、問題のあるページを調べてください。そうすることで、ページ上の各コンテンツ領域の内訳とそれぞれの読み込み時間がわかります。
* サイト上のすべての JS と CSS を最小限にします。具体的な方法については、こちらの[ブログ投稿](https://blogs.adobe.com/foxes/enable-js-and-css-minification/)を参照してください。
* コンポーネントに埋め込まれた CSS と JS を削除します。ページのレンダリングに必要な要求の数を最小限にするには、これらをクライアント側のライブラリに組み込んで最小化する必要があります。
* Chrome の「ネットワーク」タブなどのツールを使用してサーバーリクエストを調べることで、最も時間がかかるコンポーネントを確認します。

問題の領域を特定したら、パフォーマンスの最適化のためにアプリケーションコードを調べます。Adobeサポートでは、既製のAEM機能のうち、適切に動作しないものに対処できます。
