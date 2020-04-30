---
title: '[!DNL Adobe Experience Manager Assets]のデプロイメントを監視するためのベストプラクティスです。'
description: '[!DNL Adobe Experience Manager]の展開後に、展開の環境とパフォーマンスを監視するためのベストプラクティスです。'
contentOwner: AG
translation-type: tm+mt
source-git-commit: 90f9c0b60d4b0878f56eefea838154bb7627066d

---


# 導入を監視するためのベストプラクテ [!DNL Adobe Experience Manager Assets] ィス {#assets-monitoring-best-practices}

監視には、 [!DNL Experience Manager Assets] 次のプロセスと技術の観察とレポートが含まれる必要があります。

* システム CPU
* システムメモリ使用量
* システムディスク IO および IO 待機時間
* システムネットワーク IO
* JMX MBeans。ヒープの使用と非同期プロセス(ワークフローなど)
* OSGi コンソールヘルスチェック

Typically, [!DNL Experience Manager Assets] can be monitored in two ways, live monitoring and long term monitoring.

## Live monitoring {#live-monitoring}

開発のパフォーマンステストの段階、または高負荷な状態になったときに、環境のパフォーマンス特性を把握するためにライブ監視を実行する必要があります。通常、ライブ監視はいくつかのツールを使用して実行します。以下にお勧めのツールを示します。

* [ビジュアルVM](https://visualvm.java.net/):Visual VMを使用すると、CPU使用率、Java表示使用率など、Java VMの詳細な情報をメモリに格納できます。 また、デプロイメントで実行するコードのサンプルと評価も可能です。
* [Top](https://man7.org/linux/man-pages/man1/top.1.html)：Top は、CPU、メモリ、IO 使用量などの使用量統計を表示するダッシュボードを開く Linux コマンドです。インスタンスの状況の概要を示します。
* [Htop](https://hisham.hm/htop/)：Htop は、インタラクティブなプロセスビューアです。Top が提供する情報に加えて、詳細な CPU およびメモリ使用状況が表示されます。Htop can be installed on most Linux systems using `yum install htop` or `apt-get install htop`.

* [Iotop](https://guichaz.free.fr/iotop/)：Iotop は、ディスク IO 使用量の詳細なダッシュボードです。ディスク IO を使用するプロセス、およびそのプロセスによる使用量を示すバーやメーターが表示されます。Iotop can be installed on most Linux systems using `yum install iotop` or `apt-get install iotop`.

* [Iftop](https://www.ex-parrot.com/pdw/iftop/)：Iftop は、イーサネット／ネットワークの使用量についての詳細情報を表示します。Iftop では、イーサネットを使用するエンティティについての通信チャネルごとの統計情報、および使用されている帯域幅の量が表示されます。Iftop can be installed on most Linux systems using `yum install iftop` or `apt-get install iftop`.

* Java Flight Recorder（JFR）：非実稼動環境で自由に使用できる、Oracle の市販ツールです。For more details, see [How to Use Java Flight Recorder to Diagnose CQ Runtime Problems](https://cq-ops.tumblr.com/post/73865704329/how-to-use-java-flight-recorder-to-diagnose-cq).
* [!DNL Experience Manager] `error.log` ファイル：ファイルを調べて、シ [!DNL Experience Manager] ステムに `error.log` 記録されたエラーの詳細を調べることができます。 調査するエラーを `tail -F quickstart/logs/error.log` 識別するには、コマンドを使用します。
* [ワークフローコンソール](/help/sites-administering/workflows.md)：ワークフローコンソールを使用して、遅れているワークフローや、停止しているワークフローを監視できます。

Typically, you use these tools together to obtain a comprehensive idea about the performance of your [!DNL Experience Manager] deployment.

>[!NOTE]
>
>これらのツールは標準的なツールです。アドビでは直接サポートしません。追加のライセンスは必要ありません。

![chlimage_1-33](assets/chlimage_1-143.png)

*図：Visual VMツールを使用したライブ監視。*

![chlimage_1-32](assets/chlimage_1-142.png)

## 長期監視 {#long-term-monitoring}

Long term monitoring of an [!DNL Experience Manager] deployment involves monitoring for a longer duration the same portions that are monitored live. また、環境に固有のアラートも定義します。

### ログの集約とレポート {#log-aggregation-and-reporting}

集計ログには、Splunk(TM)、Elastic Search、Logstash、Kabana(ELK)など、いくつかのツールが使用できます。 To evaluate the uptime of your [!DNL Experience Manager] deployment, it is important for you to understand log events specific to your system and create alerts based on them. 開発と運用の実践に関する十分な知識があれば、重要なアラートを生成するログ集計プロセスを調整する方法をより深く理解するのに役立ちます。

### 環境の監視 {#environment-monitoring}

環境の監視には、以下の監視が含まれます。

* ネットワークのスループット
* ディスク IO
* メモリ
* CPU 使用率
* JMX MBean
* 外部 Web サイト

それぞれの項目を監視するには、NewRelic（TM）や AppDynamics（TM）などの外部ツールが必要です。これらのツールを使用して、システム固有のアラート（システム利用率が高い、ワークフローのバックアップ、ヘルスチェック失敗、Web サイトへの不正なアクセスなど）を定義できます。アドビでは、特定のツールを推奨することはありません。ご自身に合ったツールを見つけ、説明した項目の監視に利用してください。

#### 内部アプリケーション監視 {#internal-application-monitoring}

Internal application monitoring includes monitoring the application components that make up the [!DNL Experience Manager] stack, including JVM, the content repository, and monitoring through custom application code built on the platform. 通常、SolarWinds（TM）、HP OpenView（TM）、Hyperic（TM）、Zabbix（TM）などの一般的な多くの監視ソリューションで直接監視できる JMX MBean を通して監視を実行します。JMX への直接接続をサポートしないシステムでは、JMX データを抽出して、それらのシステムがネイティブで理解できる形式で公開するシェルスクリプトを記述できます。

JMX MBean へのリモートアクセスは、デフォルトで無効になっています。For more information on monitoring through JMX, see [Monitoring and Management Using JMX Technology](https://docs.oracle.com/javase/7/docs/technotes/guides/management/agent.html).

多くの場合、統計情報を効果的に監視するにはベースラインが必要です。ベースラインを作成するには、通常の動作条件の下で一定期間システムを監視し、通常の指標を特定します。

**JVM 監視**

As with any Java-based application stack, [!DNL Experience Manager] depends on the resources that are provided to it through the underlying Java Virtual Machine. JVM により公開されているプラットフォーム MXBean によって、それらのリソースの多くの状態を監視できます。MXBean について詳しくは、[プラットフォーム MBean サーバーおよびプラットフォーム MXBean の使用](https://docs.oracle.com/javase/7/docs/technotes/guides/management/mxbeans.html)を参照してください。

JVMを監視できる基準パラメーターの一部を次に示します。

メモリ

* `MBean: lava.lang:type=Memory`
* URL: `/system/console/jmx/java.lang:type=Memory`
* インスタンス：すべてのサーバー
* アラームしきい値：ヒープまたは非ヒープメモリ使用率が、対応する最大メモリの 75％を超えた場合。
* アラーム定義：システムメモリが不十分である、またはコードにメモリリークがあります。スレッドダンプを分析して、定義を満たすかどうか判断します。

>[!Note]
>
>このBeanが提供する情報はバイト単位で表されます。

スレッド

* MBean: `java.lang:type=Threading`
* URL: `/system/console/jmx/java.lang:type=Threading`
* インスタンス：すべてのサーバー
* アラームしきい値：スレッド数がベースラインの 150％を超えた場合。
* アラーム定義：適切に停止できていないアクティブなプロセスがある、または非効率な操作で大量のリソースを消費しています。スレッドダンプを分析して、定義を満たすかどうか判断します。

**モニタ[!DNL Experience Manager]**

[!DNL Experience Manager] も、JMX を通して一連の統計情報および操作を公開しています。これにより、システムヘルスの評価をおこない、ユーザーに影響を与える前に問題を特定できます。詳しくは、 JMX MBean の[ドキュメント](/help/sites-administering/jmx-console.md)を参照してください。[!DNL Experience Manager]

Here are some baseline parameters that you can monitor for [!DNL Experience Manager]:

レプリケーションエージェント

* MBean: `com.adobe.granite.replication:type=agent,id=”<AGENT_NAME>”`
* URL: `/system/console/jmx/com.adobe.granite.replication:type=agent,id=”<AGENT_NAME>"`
* インスタンス：1 つのオーサーインスタンスおよびすべてのパブリッシュインスタンス（フラッシュエージェント）
* アラームしきい値：`QueueBlocked``true` の値が 、または `QueueNumEntries` の値がベースラインの 150％を超えた場合。

* アラーム定義：システムにブロックされたキューが存在しており、レプリケーションターゲットがダウンしているか、または到達不能であることを示しています。多くの場合、ネットワークまたはインフラストラクチャの問題により過剰なエントリがキューに登録されています。それによってシステムのパフォーマンスに悪影響が生じる可能性があります。

>[!Note]
>
>For the MBean and URL parameters, replace `<AGENT_NAME>` with the name of the replication agent you want to monitor.

セッションカウンター

* MBean: `org.apache.jackrabbit.oak:id=7,name="OakRepository Statistics",type="RepositoryStats"`
* URL：*/system/console/jmx/org.apache.jackrabbit.oak:id=7,name=&quot;OakRepository Statistics&quot;,type*=&quot;RepositoryStats&quot;
* インスタンス：すべてのサーバー
* アラームしきい値：開いているセッションの数がベースラインよりも 50％以上多い場合。
* アラーム定義：特定のコードによりセッションが開かれ、閉じられない状態になっています。この状態は徐々に進行し、最終的にはシステムでメモリリークの原因となります。システム上のセッション数は多少変動しますが、継続的に上昇してはいけません。

ヘルスチェック

[操作ダッシュボード](/help/sites-administering/operations-dashboard.md#health-reports)のヘルスチェックには、監視用の対応する JMX MBean があります。ただし、カスタムのヘルスチェックを記述して、追加のシステム統計情報を公開できます。

監視に役立つ、あらかじめ用意されたヘルスチェックをいくつか示します。

* システムチェック
   * MBean: `org.apache.sling.healthcheck:name=systemchecks,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=systemchecks,type=HealthCheck`
   * インスタンス：1 つのオーサーサーバー、およびすべてのパブリッシュサーバー
   * アラームしきい値：ステータスが OK ではない場合。
   * アラーム定義：いずれかの指標のステータスが警告または重要となっています。問題の原因について詳しくは、ログ属性を確認してください。

* レプリケーションキュー

   * MBean: `org.apache.sling.healthcheck:name=replicationQueue,type=HealthCheck `
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=replicationQueue,type=HealthCheck`
   * インスタンス：1 つのオーサーサーバー、およびすべてのパブリッシュサーバー
   * アラームしきい値：ステータスが OK ではない場合。
   * アラーム定義：いずれかの指標のステータスが警告または重要となっています。問題を発生させたキューについて詳しくは、ログ属性を確認してください。

* 応答パフォーマンス

   * MBean: `org.apache.sling.healthcheck:name=requestsStatus,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=requestsStatus,type=HealthCheck`
   * インスタンス：すべてのサーバー
   * アラーム期間：ステータスが OK ではない場合。
   * アラーム定義：いずれかの指標のステータスが警告または重要となっています。問題を発生させたキューについて詳しくは、ログ属性を確認してください。

* クエリパフォーマンス

   * MBean: `org.apache.sling.healthcheck:name=queriesStatus,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name= queriesStatus,type=HealthCheck`
   * インスタンス：1 つのオーサーサーバー、およびすべてのパブリッシュサーバー
   * アラームしきい値：ステータスが OK ではない場合。
   * アラーム定義：システムで 1 つ以上のクエリの実行速度が遅くなっています。問題を発生させたクエリについて詳しくは、ログ属性を確認してください。

* アクティブなバンドル

   * MBean: `org.apache.sling.healthcheck:name=inactiveBundles,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=inactiveBundles,type=HealthCheck`
   * インスタンス：すべてのサーバー
   * アラームしきい値：ステータスが OK ではない場合。
   * アラーム定義：システム上の非アクティブまたは未解決な OSGi バンドルの存在。問題を発生させたバンドルについて詳しくは、ログ属性を確認してください。

* ログエラー

   * MBean: `org.apache.sling.healthcheck:name=logErrorHealthCheck,type=HealthCheck`
   * URL: `/system/console/jmx/org.apache.sling.healthcheck:name=logErrorHealthCheck,type=HealthCheck`
   * インスタンス：すべてのサーバー
   * アラームしきい値：ステータスが OK ではない場合。
   * アラーム定義：ログファイルにエラーがあります。問題の原因について詳しくは、ログ属性を確認してください。

## Common issues and resolutions  {#common-issues-and-resolutions}

In the process of monitoring, if you encounter issues, here are some troubleshooting tasks that you can perform to resolve common issues with [!DNL Experience Manager] deployments:

* TarMK を使用している場合は、Tar 圧縮を頻繁に実行します。For more details, see [Maintain the repository](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository).
* ログを確 `OutOfMemoryError` 認します。 詳しくは、[メモリの問題の分析](https://helpx.adobe.com/experience-manager/kb/AnalyzeMemoryProblems.html)を参照してください。

* ログを確認し、インデックス化されていないクエリ、ツリートラバーサル、インデックストラバーサルへの参照がないかを確認します。これらは、インデックス化されていないクエリ、または不適切にインデックス化されたクエリを示しています。For For best practices on optimizing query and indexing performance, see [Best practices for queries and indexing](/help/sites-deploying/best-practices-for-queries-and-indexing.md).
* ワークフローが予期したとおりに動作していることを確認するには、ワークフローコンソールを使用します。可能な場合は、複数のワークフローを単一のワークフローにまとめます。
* ライブ監視を再確認し、他にボトルネックがないか、または特定のリソースを大量に使用している箇所がないかを確認します。
* Investigate the egress points from the client network and the ingress points to the [!DNL Experience Manager] deployment network, including the dispatcher. 多くの場合、これらがボトルネックが発生する領域となります。詳しくは、[Assets のネットワークにおける考慮事項](/help/assets/assets-network-considerations.md)を参照してください。
* サーバーのサイズを拡大 [!DNL Experience Manager] します。 You may have an inadequately sized your [!DNL Experience Manager] deployment. アドビカスタマーケアは、お使いのサーバーが小さすぎるかどうかを特定するのに役立ちます。
* `access.log` および `error.log` ファイルで、不具合の発生した時刻付近のエントリを調査します。カスタムコードの異常の兆候となるパターンを探します。それらを監視するイベントのリストに追加します。
