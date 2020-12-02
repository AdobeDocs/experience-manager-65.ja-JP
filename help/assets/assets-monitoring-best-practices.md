---
title: ' [!DNL Assets] 導入を監視するためのベストプラクティス'
description: 展開後の [!DNL Adobe Experience Manager] 展開の環境とパフォーマンスを監視するためのベストプラクティスです。
contentOwner: AG
translation-type: tm+mt
source-git-commit: b14b377e52ab10c41355f069d97508b588d82216
workflow-type: tm+mt
source-wordcount: '1668'
ht-degree: 67%

---


# [!DNL Adobe Experience Manager Assets]導入{#assets-monitoring-best-practices}を監視するためのベストプラクティス

[!DNL Experience Manager Assets]の観点から見ると、監視には以下のプロセスとテクノロジーの観察とレポートが含まれるはずです。

* システム CPU
* システムメモリ使用量
* システムディスク IO および IO 待機時間
* システムネットワーク IO
* ヒープの使用率と非同期プロセス(ワークフローなど)のためのJMX MBean
* OSGi コンソールヘルスチェック

通常、[!DNL Experience Manager Assets]は、ライブモニタと長期モニタの2つの方法で監視できます。

## ライブモニタリング{#live-monitoring}

開発のパフォーマンステストの段階、または高負荷な状態になったときに、環境のパフォーマンス特性を把握するためにライブ監視を実行する必要があります。通常、ライブ監視はいくつかのツールを使用して実行します。以下にお勧めのツールを示します。

* [ビジュアルVM](https://visualvm.github.io/):Visual VMを使用すると、CPU使用率、Javaメモリ使用量など、Java VMの詳細な情報を表示できます。また、デプロイメントで実行するコードのサンプリングや評価を行うこともできます。
* [Top](https://man7.org/linux/man-pages/man1/top.1.html)：Top は、CPU、メモリ、IO 使用量などの使用量統計を表示するダッシュボードを開く Linux コマンドです。インスタンスの状況の概要を示します。
* [Htop](https://hisham.hm/htop/)：Htop は、インタラクティブなプロセスビューアです。Top が提供する情報に加えて、詳細な CPU およびメモリ使用状況が表示されます。Htopは、`yum install htop`または`apt-get install htop`を使用して、ほとんどのLinuxシステムにインストールできます。

* Iotop：Iotop は、ディスク IO 使用量の詳細なダッシュボードです。ディスク IO を使用するプロセス、およびそのプロセスによる使用量を示すバーやメーターが表示されます。iotopは、`yum install iotop`または`apt-get install iotop`を使って、ほとんどのLinuxシステムにインストールできます。

* [Iftop](https://www.ex-parrot.com/pdw/iftop/)：Iftop は、イーサネット／ネットワークの使用量についての詳細情報を表示します。Iftop では、イーサネットを使用するエンティティについての通信チャネルごとの統計情報、および使用されている帯域幅の量が表示されます。iftopは、`yum install iftop`や`apt-get install iftop`を使って、ほとんどのLinuxシステムにインストールできます。

* Java Flight Recorder（JFR）：非実稼動環境で自由に使用できる、Oracle の市販ツールです。詳しくは、[Java Flight Recorderを使用してCQランタイムの問題を診断する方法](https://cq-ops.tumblr.com/post/73865704329/how-to-use-java-flight-recorder-to-diagnose-cq)を参照してください。
* [!DNL Experience Manager] `error.log` ファイル：この [!DNL Experience Manager] `error.log` ファイルを調べて、システムにログインしたエラーの詳細を調べることができます。`tail -F quickstart/logs/error.log`コマンドを使用して、調査するエラーを識別します。
* [ワークフローコンソール](/help/sites-administering/workflows.md)：ワークフローコンソールを使用して、遅れているワークフローや、停止しているワークフローを監視できます。

通常は、[!DNL Experience Manager]展開のパフォーマンスに関する包括的な概念を得るために、これらのツールを一緒に使用します。

>[!NOTE]
>
>これらのツールは標準的なツールです。アドビでは直接サポートしません。追加のライセンスは必要ありません。

![chlimage_1-33](assets/chlimage_1-143.png)

*図：Visual VMツールを使用したライブ監視*

![chlimage_1-32](assets/chlimage_1-142.png)

## 長期監視{#long-term-monitoring}

[!DNL Experience Manager]デプロイメントの長期的な監視には、ライブで監視されるのと同じ部分を長期間監視する必要があります。 また、環境に固有のアラートも定義します。

### ログの集約とレポート  {#log-aggregation-and-reporting}

集計ログには、Splunk(TM)やElastic Search、Logstash、Kabana(ELK)などのツールが使用できます。 [!DNL Experience Manager]導入環境の稼働時間を評価するには、システムに固有のログイベントを理解し、それに基づいてアラートを作成することが重要です。 開発と運用に関する慣習を十分に理解しておくと、重要なアラートを生成するログ集計プロセスを調整する方法をより深く理解できます。

### 環境の監視 {#environment-monitoring}

環境の監視には、以下の監視が含まれます。

* ネットワークのスループット
* ディスク IO
* メモリ
* CPU 使用率
* JMX MBean
* 外部 Web サイト

それぞれの項目を監視するには、NewRelic（TM）や AppDynamics（TM）などの外部ツールが必要です。これらのツールを使用して、システム固有のアラート（システム利用率が高い、ワークフローのバックアップ、ヘルスチェック失敗、Web サイトへの不正なアクセスなど）を定義できます。アドビでは、特定のツールを推奨することはありません。ご自身に合ったツールを見つけ、説明した項目の監視に利用してください。

#### 内部アプリケーション監視  {#internal-application-monitoring}

内部アプリケーションの監視には、JVM、コンテンツリポジトリ、プラットフォーム上に構築されたカスタムアプリケーションコードによる監視など、[!DNL Experience Manager]スタックを構成するアプリケーションコンポーネントの監視が含まれます。 通常、SolarWinds（TM）、HP OpenView（TM）、Hyperic（TM）、Zabbix（TM）などの一般的な多くの監視ソリューションで直接監視できる JMX MBean を通して監視を実行します。JMX への直接接続をサポートしないシステムでは、JMX データを抽出して、それらのシステムがネイティブで理解できる形式で公開するシェルスクリプトを記述できます。

JMX MBean へのリモートアクセスは、デフォルトで無効になっています。JMXによる監視の詳細については、[Monitoring and Management Using JMX Technology](https://docs.oracle.com/javase/7/docs/technotes/guides/management/agent.html)を参照してください。

多くの場合、統計情報を効果的に監視するにはベースラインが必要です。ベースラインを作成するには、通常の動作条件の下で一定期間システムを監視し、通常の指標を特定します。

**JVM 監視**

[!DNL Experience Manager]は、Javaベースのアプリケーションスタックと同様、基盤となるJava仮想マシンを通じて提供されるリソースに依存します。 JVM により公開されているプラットフォーム MXBean によって、それらのリソースの多くの状態を監視できます。MXBean について詳しくは、[プラットフォーム MBean サーバーおよびプラットフォーム MXBean の使用](https://docs.oracle.com/javase/7/docs/technotes/guides/management/mxbeans.html)を参照してください。

JVMの基準パラメーターの一部を以下に示します。

メモリ

* `MBean: lava.lang:type=Memory`
* URL: `/system/console/jmx/java.lang:type=Memory`
* インスタンス：すべてのサーバー
* アラームしきい値：ヒープまたは非ヒープメモリ使用率が、対応する最大メモリの 75％を超えた場合。
* アラーム定義：システムメモリが不十分である、またはコードにメモリリークがあります。スレッドダンプを分析して、定義を満たすかどうか判断します。

>[!NOTE]
>
>このBeanが提供する情報は、バイト単位で表されます。

スレッド

* MBean:`java.lang:type=Threading`
* URL:`/system/console/jmx/java.lang:type=Threading`
* インスタンス：すべてのサーバー
* アラームしきい値：スレッド数がベースラインの 150％を超えた場合。
* アラーム定義：適切に停止できていないアクティブなプロセスがある、または非効率な操作で大量のリソースを消費しています。スレッドダンプを分析して、定義を満たすかどうか判断します。

**モニタ[!DNL Experience Manager]**

[!DNL Experience Manager] も、JMX を通して一連の統計情報および操作を公開しています。これにより、システムヘルスの評価をおこない、ユーザーに影響を与える前に問題を特定できます。詳しくは、 JMX MBean の[ドキュメント](/help/sites-administering/jmx-console.md)を参照してください。[!DNL Experience Manager]

以下に、[!DNL Experience Manager]の監視が可能な基準パラメータの一部を示します。

レプリケーションエージェント

* MBean:`com.adobe.granite.replication:type=agent,id=”<AGENT_NAME>”`
* URL:`/system/console/jmx/com.adobe.granite.replication:type=agent,id=”<AGENT_NAME>"`
* インスタンス：1 つのオーサーインスタンスおよびすべてのパブリッシュインスタンス（フラッシュエージェント）
* アラームしきい値：`QueueBlocked``true` の値が 、または `QueueNumEntries` の値がベースラインの 150％を超えた場合。

* アラーム定義：システムにブロックされたキューが存在しており、レプリケーションターゲットがダウンしているか、または到達不能であることを示しています。多くの場合、ネットワークまたはインフラストラクチャの問題により過剰なエントリがキューに登録されています。それによってシステムのパフォーマンスに悪影響が生じる可能性があります。

>[!NOTE]
>
>MBeanおよびURLパラメーターの場合は、`<AGENT_NAME>`を監視する複製エージェントの名前に置き換えます。

セッションカウンター

* MBean:`org.apache.jackrabbit.oak:id=7,name="OakRepository Statistics",type="RepositoryStats"`
* URL：*/system/console/jmx/org.apache.jackrabbit.oak:id=7,name=&quot;OakRepository Statistics&quot;,type*=&quot;RepositoryStats&quot;
* インスタンス：すべてのサーバー
* アラームしきい値：開いているセッションの数がベースラインよりも 50％以上多い場合。
* アラーム定義：特定のコードによりセッションが開かれ、閉じられない状態になっています。この状態は徐々に進行し、最終的にはシステムでメモリリークの原因となります。システム上のセッション数は多少変動しますが、継続的に上昇してはいけません。

ヘルスチェック

[操作ダッシュボード](/help/sites-administering/operations-dashboard.md#health-reports)のヘルスチェックには、監視用の対応する JMX MBean があります。ただし、カスタムのヘルスチェックを記述して、追加のシステム統計情報を公開できます。

監視に役立つ、あらかじめ用意されたヘルスチェックをいくつか示します。

* システムチェック
   * MBean:`org.apache.sling.healthcheck:name=systemchecks,type=HealthCheck`
   * URL:`/system/console/jmx/org.apache.sling.healthcheck:name=systemchecks,type=HealthCheck`
   * インスタンス：1 つのオーサーサーバー、およびすべてのパブリッシュサーバー
   * アラームしきい値：ステータスが OK ではない場合。
   * アラーム定義：いずれかの指標のステータスが警告または重要となっています。問題の原因について詳しくは、ログ属性を確認してください。

* レプリケーションキュー

   * MBean:`org.apache.sling.healthcheck:name=replicationQueue,type=HealthCheck`
   * URL:`/system/console/jmx/org.apache.sling.healthcheck:name=replicationQueue,type=HealthCheck`
   * インスタンス：1 つのオーサーサーバー、およびすべてのパブリッシュサーバー
   * アラームしきい値：ステータスが OK ではない場合。
   * アラーム定義：いずれかの指標のステータスが警告または重要となっています。問題を発生させたキューについて詳しくは、ログ属性を確認してください。

* 応答パフォーマンス

   * MBean:`org.apache.sling.healthcheck:name=requestsStatus,type=HealthCheck`
   * URL:`/system/console/jmx/org.apache.sling.healthcheck:name=requestsStatus,type=HealthCheck`
   * インスタンス：すべてのサーバー
   * アラーム期間：ステータスが OK ではない場合。
   * アラーム定義：いずれかの指標のステータスが警告または重要となっています。問題を発生させたキューについて詳しくは、ログ属性を確認してください。

* クエリパフォーマンス

   * MBean:`org.apache.sling.healthcheck:name=queriesStatus,type=HealthCheck`
   * URL:`/system/console/jmx/org.apache.sling.healthcheck:name= queriesStatus,type=HealthCheck`
   * インスタンス：1 つのオーサーサーバー、およびすべてのパブリッシュサーバー
   * アラームしきい値：ステータスが OK ではない場合。
   * アラーム定義：システムで 1 つ以上のクエリの実行速度が遅くなっています。問題を発生させたクエリについて詳しくは、ログ属性を確認してください。

* アクティブなバンドル

   * MBean:`org.apache.sling.healthcheck:name=inactiveBundles,type=HealthCheck`
   * URL:`/system/console/jmx/org.apache.sling.healthcheck:name=inactiveBundles,type=HealthCheck`
   * インスタンス：すべてのサーバー
   * アラームしきい値：ステータスが OK ではない場合。
   * アラーム定義：システム上の非アクティブまたは未解決な OSGi バンドルの存在。問題を発生させたバンドルについて詳しくは、ログ属性を確認してください。

* ログエラー

   * MBean:`org.apache.sling.healthcheck:name=logErrorHealthCheck,type=HealthCheck`
   * URL:`/system/console/jmx/org.apache.sling.healthcheck:name=logErrorHealthCheck,type=HealthCheck`
   * インスタンス：すべてのサーバー
   * アラームしきい値：ステータスが OK ではない場合。
   * アラーム定義：ログファイルにエラーがあります。問題の原因について詳しくは、ログ属性を確認してください。

## 一般的な問題と解決{#common-issues-and-resolutions}

監視の過程で問題が発生した場合は、次に示すトラブルシューティングタスクを実行して、[!DNL Experience Manager]デプロイメントで発生する一般的な問題を解決できます。

* TarMK を使用している場合は、Tar 圧縮を頻繁に実行します。詳しくは、[リポジトリの管理](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)を参照してください。
* `OutOfMemoryError`ログを確認します。 詳しくは、[メモリの問題の分析](https://helpx.adobe.com/experience-manager/kb/AnalyzeMemoryProblems.html)を参照してください。

* ログを確認し、インデックス化されていないクエリ、ツリートラバーサル、インデックストラバーサルへの参照がないかを確認します。これらは、インデックス化されていないクエリ、または不適切にインデックス化されたクエリを示しています。クエリとインデックス作成のパフォーマンスを最適化するベストプラクティスについては、[クエリとインデックス作成のベストプラクティス](/help/sites-deploying/best-practices-for-queries-and-indexing.md)を参照してください。
* ワークフローが予期したとおりに動作していることを確認するには、ワークフローコンソールを使用します。可能な場合は、複数のワークフローを単一のワークフローにまとめます。
* ライブ監視を再確認し、他にボトルネックがないか、または特定のリソースを大量に使用している箇所がないかを確認します。
* クライアントネットワークからの出力ポイントと、ディスパッチャーを含む[!DNL Experience Manager]デプロイメントネットワークへの入力ポイントを調べます。 多くの場合、これらがボトルネックが発生する領域となります。詳しくは、[Assets のネットワークにおける考慮事項](/help/assets/assets-network-considerations.md)を参照してください。
* [!DNL Experience Manager]サーバをアップサイズにします。 [!DNL Experience Manager]の展開のサイズが不十分である可能性があります。 Adobeカスタマーケアは、サーバーのサイズが小さいかどうかを特定するのに役立ちます。
* `access.log` および `error.log` ファイルで、不具合の発生した時刻付近のエントリを調査します。カスタムコードの異常の兆候となるパターンを探します。それらを監視するイベントのリストに追加します。
