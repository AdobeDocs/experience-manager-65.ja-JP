---
title: 監視のベストプラクティス [!DNL Assets] デプロイメント
description: ' [!DNL Adobe Experience Manager]  インスタンスをデプロイした後の環境およびパフォーマンスの監視に関するベストプラクティス。'
contentOwner: AG
role: Admin, Architect
feature: Asset Management
exl-id: a9e1bd6b-c768-4faa-99a3-7110693998dc
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1639'
ht-degree: 42%

---

# 監視のベストプラクティス [!DNL Adobe Experience Manager Assets] デプロイメント {#assets-monitoring-best-practices}

[!DNL Experience Manager Assets] の観点から見ると、監視には、次のプロセスおよびテクノロジーの観察とレポートを含める必要があります。

* システム CPU
* システムメモリ使用量
* システムディスクの IO と IO の待機時間
* システムネットワーク IO
* ヒープ使用率およびワークフローなどの非同期プロセス用の JMX MBean
* OSGi コンソールヘルスチェック

通常、[!DNL Experience Manager Assets] の監視には、ライブ監視と長期的監視の 2 種類があります。

## ライブ監視 {#live-monitoring}

開発環境のパフォーマンステストフェーズ中または高負荷の状況でライブ監視を実行して、環境のパフォーマンス特性を把握する必要があります。 通常、ライブ監視は、一連のツールを使用して実行する必要があります。 次に推奨事項を示します。

* [Visual VM](https://visualvm.github.io/)：Visual VM を使用すると、CPU 使用率や、Java によるメモリ使用量などの詳細な Java VM 情報を表示できます。また、デプロイメント上で実行されるコードのサンプリングと評価をすることができます。
* [上](https://man7.org/linux/man-pages/man1/top.1.html):Top は、ダッシュボードを開く Linux コマンドで、CPU、メモリ、I/O 使用量などの使用状況の統計を表示します。 インスタンスで発生している処理の概要を示します。
* [Htop](https://hisham.hm/htop/):Htop は、インタラクティブなプロセスビューアです。 Top が提供する機能に加えて、CPU とメモリの使用量が詳細に表示されます。 Htop は、`yum install htop` または `apt-get install htop` を使用してほとんどの Linux システムにインストールできます。

* Iotop：Iotop は、ディスク IO 使用量の詳細なダッシュボードです。ディスク IO を使用するプロセス、およびそのプロセスによる使用量を示すバーやメーターが表示されます。Iotop は、`yum install iotop` または `apt-get install iotop` を使用してほとんどの Linux システムにインストールできます。

* [Iftop](https://www.ex-parrot.com/pdw/iftop/):Iftop は、イーサネット/ネットワーク使用状況に関する詳細情報を表示します。 Iftop は、イーサネットを使用するエンティティと、使用する帯域幅の量に関する通信チャネルごとの統計を表示します。 Iftop は、`yum install iftop` または `apt-get install iftop` を使用してほとんどの Linux システムにインストールできます。

* Java Flight Recorder（JFR）：非実稼動環境で自由に使用できる、Oracle の市販ツールです。詳しくは、[Java Flight Recorder を使用した CQ ランタイムの問題の診断方法](https://cq-ops.tumblr.com/post/73865704329/how-to-use-java-flight-recorder-to-diagnose-cq)を参照してください。
* [!DNL Experience Manager] `error.log` ファイル：システムでログに記録されたエラーの詳細を [!DNL Experience Manager] `error.log` ファイルで調査できます。コマンド `tail -F quickstart/logs/error.log` を使用して、調査するエラーを特定します。
* [ワークフローコンソール](/help/sites-administering/workflows.md)：ワークフローコンソールを使用して、遅れているワークフローや、停止しているワークフローを監視できます。

通常は、これらのツールを組み合わせて使用し、[!DNL Experience Manager] デプロイメントのパフォーマンスについて包括的に把握します。

>[!NOTE]
>
>これらのツールは標準のツールで、Adobeで直接サポートされていません。 追加のライセンスは必要ありません。

![chlimage_1-33](assets/chlimage_1-143.png)

*図：Visual VM ツールを使用したライブ監視。*

![chlimage_1-32](assets/chlimage_1-142.png)

## 長期的な監視 {#long-term-monitoring}

[!DNL Experience Manager] デプロイメントの長期的監視では、ライブで監視されるのと同じ部分の長期にわたる監視を行います。また、環境に固有のアラートの定義も含まれます。

### ログの集計とレポート {#log-aggregation-and-reporting}

ログを集計するツールがいくつかあります。例えば、Splunk(TM) や Elastic Search、Logstash、Kabana(ELK) などです。 [!DNL Experience Manager] デプロイメントの稼動時間を評価するには、システムに固有のログイベントを理解し、それに基づきアラートを作成することが重要です。開発および運用手法をよく理解しておくと、ログ集約プロセスを適切に調整して、重要なアラートを生成するのに役立ちます。

### 環境の監視 {#environment-monitoring}

環境の監視には、次の監視が含まれます。

* ネットワークスループット
* ディスク IO
* メモリ
* CPU 使用率
* JMX MBeans
* 外部 Web サイト

各項目を監視するには、NewRelic(TM) や AppDynamics(TM) などの外部ツールが必要です。 これらのツールを使用して、システムの使用率が高い、ワークフローのバックアップ、ヘルスチェックの失敗、Web サイトへの未認証アクセスなど、システムに固有のアラートを定義できます。 Adobeは、他のユーザーよりも特定のツールを推奨しません。 ユーザーに適したツールを見つけ、それを使用して、説明した項目を監視します。

#### 内部アプリケーションの監視 {#internal-application-monitoring}

内部アプリケーション監視には、JVM などの [!DNL Experience Manager] スタックを構成するアプリケーションコンポーネントの監視、コンテンツリポジトリの監視、およびプラットフォーム上に構築されたカスタムアプリケーションコードによる監視が含まれます。一般に、SolarWinds(TM)、HP OpenView(TM)、Hyperic(TM)、Zabbix(TM) など、多くの一般的な監視ソリューションで直接監視できる JMX Mbeans を通じて実行されます。 JMX への直接接続をサポートしていないシステムの場合は、シェルスクリプトを記述して JMX データを抽出し、ネイティブに理解できる形式でこれらのシステムに公開できます。

JMX MBean へのリモートアクセスは、デフォルトで無効になっています。JMX を通した監視について詳しくは、[JMX テクノロジを使用した監視と管理](https://docs.oracle.com/javase/7/docs/technotes/guides/management/agent.html)を参照してください。

多くの場合、統計を効果的に監視するには、ベースラインが必要です。 ベースラインを作成するには、システムを所定の期間通常の稼働状態で観察し、その後、通常の指標を特定します。

**JVM 監視**

他の Java ベースのアプリケーションスタックと同様に、[!DNL Experience Manager] は基盤となる Java Virtual Machine から提供されたリソースを利用します。JVM によって公開される Platform MXBean を使用して、これらのリソースの多くの状態を監視できます。 MXBean について詳しくは、 [Platform MBean サーバーと Platform MXBean の使用](https://docs.oracle.com/javase/7/docs/technotes/guides/management/mxbeans.html).

JVM で監視できるベースラインパラメーターをいくつか示します。

メモリ

* `MBean: lava.lang:type=Memory`
* URL：`/system/console/jmx/java.lang:type=Memory`
* インスタンス：すべてのサーバー
* アラームしきい値：ヒープまたは非ヒープメモリの使用率が、対応する最大メモリの 75%を超えた場合。
* アラーム定義：システムメモリが不足しているか、コードにメモリリークがあります。 スレッドダンプを分析して定義に到達します。

>[!NOTE]
>
>注意：この Bean から提供される情報の単位はバイトです。

スレッド

* MBean：`java.lang:type=Threading`
* URL：`/system/console/jmx/java.lang:type=Threading`
* インスタンス：すべてのサーバー
* アラームしきい値：スレッド数がベースラインの 150%を超える場合。
* アラーム定義：アクティブな暴走プロセスがあるか、非効率な操作が大量のリソースを消費しています。 スレッドダンプを分析して定義に到達します。

**監視[!DNL Experience Manager]**

また、[!DNL Experience Manager] は、JMX を通して一連の統計情報および操作を公開しています。これにより、システムヘルスを評価し、ユーザーに影響を与える前に問題を特定できます。詳しくは、[!DNL Experience Manager] JMX MBean の[ドキュメント](/help/sites-administering/jmx-console.md)を参照してください。

[!DNL Experience Manager] で監視できるベースラインパラメーターをいくつか示します。

レプリケーションエージェント

* MBean：`com.adobe.granite.replication:type=agent,id="<AGENT_NAME>"`
* URL：`/system/console/jmx/com.adobe.granite.replication:type=agent,id="<AGENT_NAME>"`
* インスタンス：1 つのオーサーインスタンスおよびすべてのパブリッシュインスタンス（フラッシュエージェント）
* アラームしきい値：`QueueBlocked``true` の値が 、または `QueueNumEntries` の値がベースラインの 150％を超えた場合。

* アラーム定義：システム内にブロックされたキューが存在し、レプリケーションターゲットがダウンしているか、到達できないことを示す。 多くの場合、ネットワークまたはインフラストラクチャの問題により、過剰なエントリがキューに入れられ、システムのパフォーマンスに悪影響を与える可能性があります。

>[!NOTE]
>
>注意：MBean および URL パラメーターでは、`<AGENT_NAME>` を監視するレプリケーションエージェントの名前に置き換えます。

セッションカウンター

* MBean：`org.apache.jackrabbit.oak:id=7,name="OakRepository Statistics",type="RepositoryStats"`
* URL: */system/console/jmx/org.apache.jackrabbit.oak:id=7,name=&quot;OakRepository Statistics&quot;,type*=&quot;RepositoryStats&quot;
* インスタンス：すべてのサーバー
* アラームしきい値：開いているセッションがベースラインを 50%以上超えた場合。
* アラーム定義：セッションは、コードの一部を通じて開かれ、閉じることはありません。 この問題は時間の経過と共にゆっくり発生し、最終的にシステムでメモリリークが発生する可能性があります。 システム上でセッション数が変動する場合は、継続的に増加しないでください。

ヘルスチェック

で使用可能なヘルスチェック [操作ダッシュボード](/help/sites-administering/operations-dashboard.md#health-reports) 対応する JMX MBean が監視用に用意されている。 ただし、カスタムヘルスチェックを記述して、追加のシステム統計を公開することができます。

監視に役立つ、あらかじめ用意されているヘルスチェックを次に示します。

* システムチェック
   * MBean：`org.apache.sling.healthcheck:name=systemchecks,type=HealthCheck`
   * URL：`/system/console/jmx/org.apache.sling.healthcheck:name=systemchecks,type=HealthCheck`
   * インスタンス：1 人の作成者、すべてのパブリッシュサーバー
   * アラームしきい値：ステータスが OK でない場合
   * アラーム定義：いずれかの指標のステータスは、WARN または CRITICAL です。 問題の原因について詳しくは、ログ属性を確認してください。

* レプリケーションキュー

   * MBean：`org.apache.sling.healthcheck:name=replicationQueue,type=HealthCheck`
   * URL：`/system/console/jmx/org.apache.sling.healthcheck:name=replicationQueue,type=HealthCheck`
   * インスタンス：1 人の作成者、すべてのパブリッシュサーバー
   * アラームしきい値：ステータスが OK でない場合
   * アラーム定義：いずれかの指標のステータスは、WARN または CRITICAL です。 問題の原因となったキューについて詳しくは、ログ属性を確認してください。

* 応答パフォーマンス

   * MBean：`org.apache.sling.healthcheck:name=requestsStatus,type=HealthCheck`
   * URL：`/system/console/jmx/org.apache.sling.healthcheck:name=requestsStatus,type=HealthCheck`
   * インスタンス：すべてのサーバー
   * アラームの時間：ステータスが OK でない場合
   * アラーム定義：いずれかの指標のステータスは、WARN または CRITICAL のどちらかです。 問題の原因となったキューについて詳しくは、ログ属性を確認してください。

* クエリーパフォーマンス

   * MBean：`org.apache.sling.healthcheck:name=queriesStatus,type=HealthCheck`
   * URL：`/system/console/jmx/org.apache.sling.healthcheck:name= queriesStatus,type=HealthCheck`
   * インスタンス：1 人の作成者、すべてのパブリッシュサーバー
   * アラームしきい値：ステータスが OK でない場合
   * アラーム定義：システムで 1 つ以上のクエリが低速で実行されています。 問題の原因となったクエリについて詳しくは、ログ属性を確認してください。

* アクティブなバンドル

   * MBean：`org.apache.sling.healthcheck:name=inactiveBundles,type=HealthCheck`
   * URL：`/system/console/jmx/org.apache.sling.healthcheck:name=inactiveBundles,type=HealthCheck`
   * インスタンス：すべてのサーバー
   * アラームしきい値：ステータスが OK でない場合
   * アラーム定義：システム上に非アクティブな OSGi バンドルまたは未解決の OSGi バンドルが存在する。 問題の原因となったバンドルについて詳しくは、ログ属性を確認してください。

* ログエラー

   * MBean：`org.apache.sling.healthcheck:name=logErrorHealthCheck,type=HealthCheck`
   * URL：`/system/console/jmx/org.apache.sling.healthcheck:name=logErrorHealthCheck,type=HealthCheck`
   * インスタンス：すべてのサーバー
   * アラームしきい値：ステータスが OK でない場合
   * アラーム定義：ログファイルにエラーがあります。 問題の原因について詳しくは、ログ属性を確認してください。

## よくある問題と解決策  {#common-issues-and-resolutions}

監視中に問題が発生した場合は、以下のトラブルシューティングを実行して、[!DNL Experience Manager] デプロイメントでよくある問題を解決できます。

* TarMK を使用している場合は、Tar 圧縮を頻繁に実行します。詳しくは、[リポジトリのメンテナンス](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)を参照してください。
* `OutOfMemoryError` ログを確認します。詳しくは、[メモリの問題の分析](https://experienceleague.adobe.com/docs/experience-cloud-kcs/kbarticles/KA-17482.html?lang=ja)を参照してください。

* ログで、インデックスが作成されていないクエリ、ツリートラバーサル、またはインデックストラバーサルへの参照がないかを確認します。 これらは、インデックスが作成されていないクエリや、インデックスが不適切なクエリを示します。 クエリおよびインデックス作成のパフォーマンスを最適化するためのベストプラクティスについては、[クエリとインデックスに関するベストプラクティス](/help/sites-deploying/best-practices-for-queries-and-indexing.md)を参照してください。
* ワークフローコンソールを使用して、ワークフローが期待どおりに実行されることを確認します。 可能な場合は、複数のワークフローを 1 つのワークフローにまとめます。
* ライブ監視を再確認し、他にボトルネックがないか、または特定のリソースを大量に使用している箇所がないかを確認します。
* Dispatcher を含むクライアントネットワークからの出口ポイントおよび [!DNL Experience Manager] デプロイメントネットワークへの入り口ポイントを調査します。多くの場合、これらはボトルネック領域です。 詳しくは、 [Assets のネットワークに関する考慮事項](/help/assets/assets-network-considerations.md).
* [!DNL Experience Manager] サーバーのサイズを大きくします。[!DNL Experience Manager] デプロイメントのサイズが不適切な可能性があります。アドビカスタマーサポートは、サーバーのサイズが適切かどうかを判断するお手伝いをします。
* `access.log` および `error.log` ファイルで、不具合の発生した時刻付近のエントリを調査します。カスタムコードの異常を示す可能性のあるパターンを探します。 監視するイベントのリストに追加します。
