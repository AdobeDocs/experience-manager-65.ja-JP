---
title: Oak インデックスのトラブルシューティング
seo-title: Troubleshooting Oak Indexes
description: インデックス再作成の遅延を検出して修正する方法。
uuid: 6567ddae-128c-4302-b7e8-8befa66b1f43
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: ea70758f-6726-4634-bfb4-a957187baef0
exl-id: 85981463-189c-4f50-9d21-1d2f734b960a
source-git-commit: 9defa6d1843007e9375d839f72f6993c691a37c0
workflow-type: tm+mt
source-wordcount: '1474'
ht-degree: 38%

---

# Oak インデックスのトラブルシューティング{#troubleshooting-oak-indexes}

## インデックス再作成が遅い  {#slow-re-indexing}

AEMの内部インデックス再作成プロセスは、リポジトリデータを収集し、Oak インデックスに保存して、コンテンツに対するパフォーマンスの高いクエリをサポートします。 例外的な状況では、プロセスが遅くなったり、動かなくなったりする場合があります。 このページは、インデックス作成が遅いかどうかの識別、原因の特定、問題の解決に役立つトラブルシューティングガイドとして機能します。

不適切に長い時間を要するインデックス再作成と、大量のコンテンツのインデックス作成になるので、長い時間を要するインデックス再作成とを区別することが重要です。 例えば、コンテンツのインデックス作成に要する時間はコンテンツの量に応じて増えるので、大規模な実稼動リポジトリのインデックス作成には、小規模な開発リポジトリよりも時間がかかります。

詳しくは、 [クエリとインデックスに関するベストプラクティス](/help/sites-deploying/best-practices-for-queries-and-indexing.md) コンテンツのインデックス再作成のタイミングと方法に関する追加情報を参照してください。

## 初期検出 {#initial-detection}

時間がかかっているインデックス作成を最初に検出するには、`IndexStats` JMX MBean を確認する必要があります。影響を受ける AEM インスタンスで、次の手順を実行します。

1. Web コンソールを開いて「JMX」タブをクリックするか、https://&lt;ホスト>:&lt;ポート>/system/console/jmx（例：[http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx)）に移動します。
1. `IndexStats` Mbean に移動します。
1. 「`async`」および「`fulltext-async`」の `IndexStats` MBean を開きます。

1. 両方の MBean で、**Done** タイムスタンプおよび **LastIndexTime** タイムスタンプが現在の時刻から 45 分以内であるかどうかを確認します。

1. いずれかの MBean で、時間値（**Done** または **LastIndexedTime**）が現在の時間から 45 分より大きい場合は、インデックスジョブが失敗しているか、時間がかかりすぎています。この問題により、非同期インデックスが古くなります。

## 強制シャットダウン後、インデックス作成は一時停止しました {#indexing-is-paused-after-a-forced-shutdown}

強制シャットダウンが発生すると、AEMは再起動後 30 分まで非同期インデックス作成を中断します。 また、最初のインデックス再作成パスを完了するには、通常、さらに 15 分かかり、合計 45 分間 ( [初期検出](/help/sites-deploying/troubleshooting-oak-indexes.md#initial-detection) （45 分の期間）。 強制シャットダウン後にインデックス作成が一時停止した場合：

1. まず、AEMインスタンスが強制的にシャットダウンされたか (AEMプロセスが強制的に強制的に強制終了されたか、電源障害が発生したか )、その後再起動されたかを確認します。

   * そのために、[AEM のログ](/help/sites-deploying/configure-logging.md)を参照してください。

1. 強制シャットダウンが発生した場合、再起動時に、AEMは自動的に最大 30 分間インデックス再作成を中断します。
1. AEMが通常の非同期インデックス作成操作を再開するまで、約 45 分待ちます。

## スレッドプールが過負荷 {#thread-pool-overloaded}

>[!NOTE]
>
>AEM 6.1 では、[AEM 6.1 CFP 11](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ja) がインストールされていることを確認してください。

例外的な状況では、非同期インデックス作成の管理に使用するスレッドプールが過負荷になる場合があります。 インデックス作成プロセスを分離するために、他のAEM作業が Oak のコンテンツをタイムリーにインデックス作成する機能に干渉するのを防ぐように、スレッドプールを設定できます。 その場合は、次の操作を行います。

1. 非同期インデックス作成に使用する Apache Sling Scheduler 用の新しい分離スレッドプールを定義します。

   * 影響を受ける AEM インスタンスで、AEM OSGi web コンソール／OSGi／設定／Apache Sling Scheduler に移動するか、https://&lt;ホスト>:&lt;ポート>/system/console/configMgr（例：[http://localhost:4502/system/console/configMgr](http://localhost:4502/system/console/configMgr)）に移動します。
   * 「許可されたスレッドプール」フィールドに、値が「oak」のエントリを追加します。
   * 変更を保存するには、 **保存** を右下に表示します。

   ![chlimage_1-119](assets/chlimage_1-119.png)

1. 新しい Apache Sling Scheduler スレッドプールが登録され、Apache Sling Scheduler Status Web コンソールに表示されることを確認します。

   * AEM OSGi web コンソール／ステータス／Sling Scheduler に移動するか、https://&lt;ホスト>:&lt;ポート>/system/console/status-slingscheduler（例：[http://localhost:4502/system/console/status-slingscheduler](http://localhost:4502/system/console/status-slingscheduler)）に移動します。
   * 次のプールエントリが存在することを確認します。

      * ApacheSlingoak
      * ApacheSlingdefault

   ![chlimage_1-120](assets/chlimage_1-120.png)

## 監視キューがいっぱいです {#observation-queue-is-full}

リポジトリに対する変更やコミットが短時間で多すぎると、監視キューがいっぱいになるので、インデックス作成が遅延する可能性があります。 まず、監視キューがいっぱいかどうかを確認します。

1. web コンソールに移動して「JMX」タブをクリックするか、https://&lt;ホスト>:&lt;ポート>/system/console/jmx（例：[http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx)）に移動します。
1. Oak リポジトリ統計 MBean を開き、いずれかの `ObservationQueueMaxLength` 値が 10,000 より大きいかどうかを確認します。

   * 通常の操作では、この最大値は（特に `per second` セクションでは）最終的に 0 になる必要があるので、`ObservationQueueMaxLength` の秒の指標が 0 であることを確認します。
   * 値が 10,000 以上で、徐々に増加する場合は、少なくとも 1 つの（場合によっては複数の）キューを新しい変更（コミット）が発生するほど速く処理できないことを示します。
   * 各監視キューには制限（デフォルトでは 10,000 個）があり、その制限に達すると処理が低下します。
   * MongoMK を使用している場合は、キューの長さが長くなるにつれて内部 Oak キャッシュのパフォーマンスが低下します。この相関関係は、`Consolidated Cache` 統計 MBean の `DocChildren` キャッシュの `missRate` が増加していることで確認できます。

1. 許容可能な監視キューの制限を超えないようにするには、次の操作をお勧めします。

   * コミットの一定率を下げます。 コミットの短いスパイクは許容できますが、一定の速度を下げる必要があります。
   * [Performance tuning tips／Mongo Storage Tuning／Document cache size](https://experienceleague.adobe.com/docs/experience-manager-64/deploying/configuring/configuring-performance.html?lang=en) の説明に従って、`DiffCache` のサイズを大きくします。

## スタックしたインデックス再作成プロセスの識別と修正 {#identifying-and-remediating-a-stuck-re-indexing-process}

インデックスの再作成は、次の 2 つの条件の下で「完全に停止している」と見なすことができます。

* インデックスの再作成が遅くなり、トラバースされたノード数に関する重要な進行がログファイルに報告されなくなります。

   * 例えば、1 時間の間にメッセージがなかった場合や、進行が遅すぎて完了するまでに 1 週間以上かかる場合などです。

* ログファイルに繰り返し例外が表示される場合 ( 例えば、 `OutOfMemoryException`) をインデックススレッド内に追加します。 ログ内の 1 つ以上の同じ例外を繰り返し実行した場合、Oak は同じものを繰り返しインデックス付けしようとしますが、同じ問題では失敗します。

スタックしたインデックス再作成プロセスを特定して修正するには、次の手順を実行します。

1. インデックス作成が停止した原因を特定するには、次の情報を収集する必要があります。

   * 5 分間のスレッドダンプを収集し、2 秒ごとに 1 つのスレッドダンプを収集します。
   * [アペンダーの DEBUG レベルとログの設定](/help/sites-deploying/configure-logging.md).

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

   * AEMを再起動すると、同時負荷が高い（監視キューのオーバーフローなど）場合に、問題が解決する場合があります。
   * 再起動しても問題が解決しない場合は、[アドビサポート](https://experienceleague.adobe.com/?support-solution=General&amp;lang=ja&amp;support-tab=home#support)に問題を提出し、手順 1 で収集したすべての情報を提供してください。

## 非同期インデックス再作成を安全に中止します {#safely-aborting-asynchronous-re-indexing}

インデックス再作成は、 `async, async-reindex`および f `ulltext-async` インデックス作成レーン ( `IndexStats` Mbean)。 詳しくは、Apache Oak ドキュメントの [How to Abort Reindexing](https://jackrabbit.apache.org/oak/docs/query/indexing.html#abort-reindex) も参照してください。また、次の点にも注意してください。

* Lucene と Lucene プロパティインデックスのインデックス再作成は、自然に非同期になるので、中止することができます。
* Oak プロパティインデックスの再インデックスは、 `PropertyIndexAsyncReindexMBean`.

インデックス再作成を安全に中止するには、次の手順に従います。

1. 停止する必要がある再インデックスレーンを制御する IndexStats MBean を識別します。

   * AEM OSGi web コンソール／メイン／JMX、または https://&lt;ホスト>:&lt;ポート>/system/console/jmx（例：[http://localhost:4502/system/console/jmx](http://localhost:4502/system/console/jmx)）に移動して、JMX コンソールから該当する IndexStats MBean に移動します。
   * 停止するインデックス再作成レーンに基づいて IndexStats MBean を開きます ( `async`, `async-reindex`または `fulltext-async`)

      * 該当するレーンを識別し、IndexStats MBean インスタンスを特定するには、Oak インデックスの「async」プロパティを確認します。「async」プロパティには、レーン名が含まれます。 `async`, `async-reindex`または `fulltext-async`.
      * レーンは、「Async」列のAEM Index Manager にアクセスしても使用できます。 インデックスマネージャにアクセスするには、操作/診断/インデックスマネージャに移動します。

   ![chlimage_1-121](assets/chlimage_1-121.png)

1. 適切な `IndexStats` MBean で `abortAndPause()` コマンドを呼び出します。
1. インデックス作成レーンの再開時にインデックス再作成が再開されないように、Oak インデックス定義を適切にマークします。

   * インデックスの再作成時 **既存** index、reindex プロパティを false に設定します。

      * `/oak:index/someExistingIndex@reindex=false`
   * または、 **新規** インデックス：

      * type プロパティを disabled に設定します。

         * `/oak:index/someNewIndex@type=disabled`
      * または、インデックス定義を完全に削除します。

   完了したら、変更をリポジトリにコミットします。

1. 最後に、中止されたインデックス作成レーンで非同期インデックス作成を再開します。

   * 手順 2 で `abortAndPause()` コマンドを発行した `IndexStats` MBean で、`resume()` コマンドを呼び出します。

## インデックス再作成の遅延を防ぐ {#preventing-slow-re-indexing}

静止時（例えば、大きなコンテンツの取り込み時ではなく）にインデックスを再作成することをお勧めします。また、AEMの読み込みが認識され、制御されるメンテナンスウィンドウでも、理想的にはインデックスを再作成します。 また、他のメンテナンスアクティビティ中にインデックス再作成がおこなわれないようにします。
