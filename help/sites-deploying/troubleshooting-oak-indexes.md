---
title: Oak インデックスのトラブルシューティング
seo-title: Troubleshooting Oak Indexes
description: 時間のかかるインデックス再作成の検出および修正方法。
seo-description: How to detect and fix slow re-indexing.
uuid: 6567ddae-128c-4302-b7e8-8befa66b1f43
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: ea70758f-6726-4634-bfb4-a957187baef0
exl-id: 85981463-189c-4f50-9d21-1d2f734b960a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1476'
ht-degree: 100%

---

# Oak インデックスのトラブルシューティング{#troubleshooting-oak-indexes}

## インデックス再作成に時間がかかる  {#slow-re-indexing}

AEM の内部インデックス作成プロセスでは、コンテンツを効率的に検索できるように、リポジトリデータが収集され Oak インデックスに保存されます。例外的な状況で、このプロセスが遅くなったり、停止したりすることがあります。このページは、インデックス作成に時間がかかっているかどうかを識別し、原因を特定し、問題を解決するためのトラブルシューティングガイドの役割を果たします。

必要以上に長時間がかかっているインデックス再作成と、コンテンツの量が膨大であるために処理に時間がかかっているインデックス再作成を区別することが重要です。例えば、コンテンツのインデックス作成にかかる時間はコンテンツの量に比例するので、大規模な実稼動リポジトリのインデックスを再作成するには小規模な開発リポジトリよりも時間がかかります。

コンテンツのインデックス再作成のタイミングおよび方法について詳しくは、[クエリとインデックスに関するベストプラクティス](/help/sites-deploying/best-practices-for-queries-and-indexing.md)を参照してください。

## 最初の検出 {#initial-detection}

時間がかかっているインデックス作成を最初に検出するには、`IndexStats` JMX MBean を確認する必要があります。影響を受ける AEM インスタンスで、次の手順を実行します。

1. Web コンソールを開いて「JMX」タブをクリックするか、https://&lt;ホスト>:&lt;ポート>/system/console/jmx（例：[http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx)）に移動します。
1. `IndexStats` Mbean に移動します。
1. 「`async`」および「`fulltext-async`」の `IndexStats` MBean を開きます。

1. 両方の MBean で、**Done** タイムスタンプおよび **LastIndexTime** タイムスタンプが現在の時刻から 45 分以内であるかどうかを確認します。

1. いずれかの MBean で、時間値（**Done** または **LastIndexedTime**）が現在の時間から 45 分より大きい場合は、インデックスジョブが失敗しているか、時間がかかりすぎています。これにより、非同期インデックスが古い状態になります。

## 強制終了後にインデックス作成が一時停止する {#indexing-is-paused-after-a-forced-shutdown}

強制終了によって、再起動後に AEM で非同期インデックス作成が最大 30 分停止し、通常は最初のインデックス再作成が完了するまでさらに 15 分かかり、合計で約 45 分が必要となります（[最初の検出](/help/sites-deploying/troubleshooting-oak-indexes.md#initial-detection) の 45 分の時間枠を思い出してください）。強制終了後にインデックス作成が一時停止していることが疑われる場合は、次のことをおこなってください。

1. 最初に、AEM インスタンスが強制的に終了した（AEM プロセスが強制的に kill された、または電源障害が発生した）後に再起動したかどうかを確認します。

   * そのために、[AEM のログ](/help/sites-deploying/configure-logging.md)を参照してください。

1. 強制終了が発生した場合、再起動後 AEM ではインデックス再作成が自動的に最大 30 分停止します。
1. AEM で通常の非同期インデックス作成操作が再開されるまで約 45 分待ってください。

## スレッドプールが過負荷になる {#thread-pool-overloaded}

>[!NOTE]
>
>AEM 6.1 では、[AEM 6.1 CFP 11](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ja) がインストールされていることを確認してください。

例外的な状況で、非同期インデックス作成の管理に使用されるスレッドプールが過負荷になることがあります。インデックス作成プロセスを分離するために、適当な時間でコンテンツにインデックス作成する Oak の機能に他の AEM の処理が干渉しないように、スレッドプールを設定できます。そのためには、次の手順を実行します。

1. Apache Sling Scheduler が非同期インデックス作成に使用する、分離された新しいスレッドプールを定義します。

   * 影響を受ける AEM インスタンスで、AEM OSGi web コンソール／OSGi／設定／Apache Sling Scheduler に移動するか、https://&lt;ホスト>:&lt;ポート>/system/console/configMgr（例：[http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)）に移動します。
   * 「Allowed Thread Pools」フィールドに「oak」という値でエントリを追加します。
   * 右下の「Save」をクリックして変更内容を保存します。

   ![chlimage_1-119](assets/chlimage_1-119.png)

1. Apache Sling Scheduler の新しいスレッドプールが登録され、Apache Sling Scheduler のステータス web コンソールに表示されていることを確認します。

   * AEM OSGi web コンソール／ステータス／Sling Scheduler に移動するか、https://&lt;ホスト>:&lt;ポート>/system/console/status-slingscheduler（例：[http://localhost:4502/system/console/status-slingscheduler](http://localhost:4502/system/console/status-slingscheduler)）に移動します。
   * 次のプールエントリが存在することを確認します。

      * ApacheSlingoak
      * ApacheSlingdefault

   ![chlimage_1-120](assets/chlimage_1-120.png)

## 監視キューがいっぱいである {#observation-queue-is-full}

リポジトリに非常に多くの変更とコミットが短時間におこなわれた場合、監視キューがいっぱいになることによってインデックス作成が遅延することがあります。まず、監視キューがいっぱいかどうかを確認します。

1. web コンソールに移動して「JMX」タブをクリックするか、https://&lt;ホスト>:&lt;ポート>/system/console/jmx（例：[http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx)）に移動します。
1. Oak リポジトリ統計 MBean を開き、いずれかの `ObservationQueueMaxLength` 値が 10,000 より大きいかどうかを確認します。

   * 通常の操作では、この最大値は（特に `per second` セクションでは）最終的に 0 になる必要があるので、`ObservationQueueMaxLength` の秒の指標が 0 であることを確認します。
   * 値が 10,000 以上で、徐々に増加する場合は、少なくとも 1 つ（あるいはそれ以上）のキューを新しい変更（コミット）が発生するのと同じ速さで処理できないことを示しています。
   * 各監視キューには制限（デフォルトは 10,000）があり、キューがこの制限に達すると処理能力が低下します。
   * MongoMK を使用している場合は、キューの長さが長くなるにつれて内部 Oak キャッシュのパフォーマンスが低下します。この相関関係は、`Consolidated Cache` 統計 MBean の `DocChildren` キャッシュの `missRate` が増加していることで確認できます。

1. 許容可能な監視キュー制限を超えないようにするには、次のことをお勧めします。

   * 通常時のコミット数を低く抑える。コミットの短時間の急増は許容できますが、通常時のコミット数は低く抑える必要があります。
   * [Performance tuning tips／Mongo Storage Tuning／Document cache size](https://helpx.adobe.com/experience-manager/kb/performance-tuning-tips.html#main-pars_text_3) の説明に従って、`DiffCache` のサイズを大きくします。

## 動きがないインデックス再作成プロセスの識別および修正 {#identifying-and-remediating-a-stuck-re-indexing-process}

次の 2 つの状況下において、インデックス再作成は、「完全に動きがない」と見なすことができます。

* インデックス再作成の速度が遅く、走査されたノード数に関する大きな進捗がログファイルで報告されない。

   * 例えば、1 時間以上メッセージが出力されない場合、または進捗が非常に遅く、終了まで 1 週間以上かかる場合。

* インデックス作成スレッドでログファイルに例外（`OutOfMemoryException` など）が繰り返し出力されている場合に、インデックス再作成が無限ループで動かなくなっている。ログに同じ例外が繰り返し表示される場合は、Oak が同じコンテンツのインデックスを繰り返し作成しようとして、同じ問題で失敗していることを示しています。

動きがないインデックス再作成プロセスを識別および修正するには、次の手順を実行します。

1. インデックス作成が動かない原因を識別するためには、次の情報を収集する必要があります。

   * 2 秒ごとにスレッドダンプを取得し、5 分間収集します。
   * [アペンダーの DEBUG レベルおよびログを設定します](/help/sites-deploying/configure-logging.md)。

      * *org.apache.jackrabbit.oak.plugins.index.AsyncIndexUpdate*
      * *org.apache.jackrabbit.oak.plugins.index.IndexUpdate*
   * 非同期 `IndexStats` MBean からデータを収集します。

      * AEM OSGi web コンソール／メイン／JMX／IndexStat／async に移動します。

         または、[http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DIndexStats) に移動します。
   * [oak-run.jar のコンソールモード](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run)を使用して、`/:async` ノードに存在する内容の詳細を収集します。
   * `CheckpointManager` MBean を使用して、リポジトリチェックポイントのリストを収集します。

      * AEM OSGi web コンソール／メイン／JMX／CheckpointManager／listCheckpoints()

         または、[http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DSegment+node+store+checkpoint+management%2Ctype%3DCheckpointManager) に移動します。



1. 手順 1 に示されているすべての情報を収集した後、AEM を再起動します。

   * 同時負荷が高い場合（監視キューのオーバーフローなど）は、AEM を再起動すると問題が解決することがあります。
   * 再起動しても問題が解決しない場合は、[アドビサポート](https://helpx.adobe.com/jp/marketing-cloud/contact-support.html)に問題を提出し、手順 1 で収集したすべての情報を提供してください。

## 非同期のインデックス再作成の安全な中止 {#safely-aborting-asynchronous-re-indexing}

インデックス再作成は、`async, async-reindex` および f `ulltext-async` インデックス作成レーン（`IndexStats` Mbean）を使用して安全に中止（完了する前に停止）できます。詳しくは、Apache Oak ドキュメントの [How to Abort Reindexing](https://jackrabbit.apache.org/oak/docs/query/indexing.html#abort-reindex) も参照してください。また、以下の点にご留意ください。

* Lucene および Lucene プロパティインデックスのインデックス再作成は、そもそも非同期なので、中止できます。
* Oak プロパティインデックスのインデックス再作成は、インデックス再作成が `PropertyIndexAsyncReindexMBean` で開始された場合にのみ、中止できます。

インデックス再作成を安全に中止するには、次の手順に従います。

1. 停止する必要があるインデックス再作成レーンを制御する IndexStats MBean を識別します。

   * AEM OSGi web コンソール／メイン／JMX、または https://&lt;ホスト>:&lt;ポート>/system/console/jmx（例：[http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx)）に移動して、JMX コンソールから該当する IndexStats MBean に移動します。
   * 停止するインデックス再作成レーン（`async`、`async-reindex`、 `fulltext-async`）にもとづいて IndexStats MBean を開きます。

      * 該当するレーンを識別し、IndexStats MBean インスタンスを特定するには、Oak インデックスの「async」プロパティを確認します。「async」プロパティにはレーン名が示されています（`async`、`async-reindex`、`fulltext-async` のいずれか）。
      * レーンは、AEM のインデックスマネージャにアクセスして、「非同期」列で識別することもできます。インデックスマネージャにアクセスするには、運営／診断／インデックスマネージャに移動します。

   ![chlimage_1-121](assets/chlimage_1-121.png)

1. 適切な `IndexStats` MBean で `abortAndPause()` コマンドを呼び出します。
1. インデックス作成レーンの再開時にインデックス再作成が再開されないように、Oak インデックス定義を適切にマークします。

   * **既存の**&#x200B;インデックスを再作成する場合は、reindex プロパティを false に設定します。

      * `/oak:index/someExistingIndex@reindex=false`
   * あるいは、**新規**&#x200B;インデックスの場合は次のようにします。

      * type プロパティを無効に設定します。

         * `/oak:index/someNewIndex@type=disabled`
      * または、インデックス定義を完全に削除します。

   完了したら、変更をリポジトリにコミットします。

1. 最後に、中止したインデックス作成レーンで非同期インデックス作成を再開します。

   * 手順 2 で `abortAndPause()` コマンドを発行した `IndexStats` MBean で、`resume()` コマンドを呼び出します。

## 時間のかかるインデックス再作成の回避 {#preventing-slow-re-indexing}

インデックス再作成は、処理の少ない時間（例えば、大量のコンテンツの取り込みを行っていない時間帯）、理想的には AEM の負荷を把握および制御できるメンテナンスウィンドウで行うことをお勧めします。また、インデックス再作成が他のメンテナンスアクティビティ中に実行されないようにしてください。
