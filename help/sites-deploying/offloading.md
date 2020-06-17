---
title: ジョブのオフロード
seo-title: ジョブのオフロード
description: 特定のタイプの処理を実行するために、トポロジ内の AEM インスタンスを設定および使用する方法について説明します。
seo-description: 特定のタイプの処理を実行するために、トポロジ内の AEM インスタンスを設定および使用する方法について説明します。
uuid: e971d403-dfd2-471f-b23d-a67e35f1ed88
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 370151df-3b8e-41aa-b586-5c21ecb55ffe
translation-type: tm+mt
source-git-commit: c3e4b68c10496cac8f75d009fdd9ebd777826850
workflow-type: tm+mt
source-wordcount: '2771'
ht-degree: 68%

---


# ジョブのオフロード{#offloading-jobs}

## 概要 {#introduction}

オフロードは、トポロジ内のExperience Managerインスタンス間で処理タスクを分配します。 オフロードでは、特定の Experience Manager インスタンスを使用して、特定のタイプの処理を実行できます。処理を特化することによって、利用可能なサーバーリソースを最大限に使用できます。

Offloading is based on the [Apache Sling Discovery](https://sling.apache.org/documentation/bundles/discovery-api-and-impl.html) and Sling JobManager features. To use offloading, you add Experience Manager clusters to a topology and identify the job topics that the cluster process. Clusters are comprised of one or more Experience Manager instances, so that a single instance is considered to be a cluster.

トポロジへのインスタンスの追加について詳しくは、[トポロジの管理](/help/sites-deploying/offloading.md#administering-topologies)を参照してください。

### ジョブ配布 {#job-distribution}

Sling JobManager と JobConsumer を使用して、トポロジ内で処理されるジョブを作成できます。

* JobManager：特定のトピックのジョブを作成するサービス。
* JobConsumer：1 つ以上のトピックのジョブを実行するサービス。同じトピックに対して複数の JobConsumer サービスを登録できます。

JobManager でジョブが作成されると、オフロードフレームワークによって、ジョブを実行するトポロジ内の Experience Manager クラスターが選択されます。

* クラスターには、ジョブトピックに対して登録された JobConsumer を実行している 1 つ以上のインスタンスが含まれている必要があります。
* トピックは、クラスター内の少なくとも 1 つのインスタンスに対して有効化されている必要があります。

ジョブ配布の調整について詳しくは、[トピック使用の設定](/help/sites-deploying/offloading.md#configuring-topic-consumption)を参照してください。

![chlimage_1-109](assets/chlimage_1-109.png)

オフロードフレームワークでジョブを実行するクラスタが選択され、クラスタが複数のインスタンスで構成される場合、Sling Distributionは、クラスタ内のどのインスタンスがジョブを実行するかを決定します。

### ジョブペイロード {#job-payloads}

オフロードフレームワークでは、ジョブをリポジトリ内のリソースと関連付けるジョブペイロードがサポートされています。ジョブペイロードは、ジョブがリソースを処理するために作成されたり、別のコンピューターにオフロードされたりする場合に役立ちます。

ジョブの作成時に、ペイロードはそのジョブを作成するインスタンスにのみ配置されることが保証されます。ジョブのオフロード時に、レプリケーションエージェントによって、ペイロードが最終的にジョブを使用するインスタンスで作成されます。ジョブ実行が完了すると、リバースレプリケーションによって、ペイロードのコピーがジョブを作成したインスタンスに戻されます。

## トポロジの管理 {#administering-topologies}

トポロジは、オフロードに参加する疎結合された Experience Manager クラスターです。クラスターは 1 つ以上の Experience Manager サーバーインスタンスで構成されます（単一のインスタンスがクラスターと見なされます）。

各 Experience Manager インスタンスによって、以下のオフロード関連サービスが実行されます。

* Discovery Service：トポロジに参加するために Topology Connector に要求を送信します。
* Topology Connector：参加要求を受信し、各要求を承認または拒否します。

トポロジのすべてのメンバーの Discovery Service は、メンバーのうちの 1 つの Topology Connector を参照しています。以下の節では、このメンバーをルートメンバーと呼びます。

![chlimage_1-110](assets/chlimage_1-110.png)

トポロジ内の各クラスターには、リーダーと認識されるインスタンスが含まれています。クラスターリーダーは、クラスターの他のメンバーの代わりにトポロジとやり取りします。リーダーがクラスターから外れると、クラスターの新しいリーダーが自動的に選択されます。

### トポロジの表示 {#viewing-the-topology}

トポロジブラウザーを使用して、Experience Manager インスタンスが参加しているトポロジの状態を調べます。トポロジブラウザーには、トポロジのクラスターおよびインスタンスが表示されます。

各クラスターに対して、各メンバーがクラスターに参加した順序と、どのメンバーがリーダーかを示すリストが表示されます。 現在プロパティによって、現在管理しているインスタンスが示されます。

クラスターの各インスタンスについて、複数のトポロジ関連プロパティを確認できます。

* インスタンスのジョブ・コンシューマー用のトピックの許可リスト。
* トポロジとの接続用に公開されるエンドポイント
* インスタンスがどのジョブトピックについてオフロード用に登録されているか
* インスタンスによって処理されるジョブトピック

1. タッチ UI を使用して、「ツール」タブをクリックします（[http://localhost:4502/tools.html](http://localhost:4502/tools.html)）。
1. Granite の操作エリアで、「オフロードするブラウザー」をクリックします。
1. ナビゲーションパネルで、「トポロジブラウザー」をクリックします。

   トポロジに参加しているクラスターが表示されます。

   ![chlimage_1-111](assets/chlimage_1-111.png)

1. クラスターをクリックして、クラスターのインスタンスとそれらの ID、現在ステータスおよびリーダーステータスのリストを表示します。
1. インスタンス ID をクリックして、詳細なプロパティを表示します。

Web コンソールを使用してトポロジ情報を表示することもできます。コンソールには、トポロジのクラスターに関するその他の情報が表示されます。

* どのインスタンスがローカルインスタンスであるか
* このインスタンスがトポロジに接続するために使用する Topology Connector サービス（送信）と、このインスタンスに接続するサービス（受信）
* トポロジおよびインスタンスのプロパティの履歴を変更します。

以下の手順を使用して、Web コンソールのトポロジ管理ページを開きます。

1. ブラウザーで Web コンソールを開きます（[http://localhost:4502/system/console](http://localhost:4502/system/console)）。
1. Main／Topology Management をクリックします。

   ![chlimage_1-112](assets/chlimage_1-112.png)

### トポロジメンバーシップの設定 {#configuring-topology-membership}

Experience Manager インスタンスとトポロジとのインタラクション方法を制御するために、Apache Sling のリソースベースの Discovery Service が各インスタンスで実行されます。

Discovery Service によって、トポロジとの接続を確立および維持するために、定期的な POST 要求（ハートビート）が Topology Connector サービスに送信されます。Topology Connectorサービスは、トポロジに参加できるIPアドレスまたはホスト名の許可リストを維持します。

* インスタンスをトポロジに参加させるには、ルートメンバーの Topology Connector サービスの URL を指定します。
* インスタンスがトポロジを結合できるようにするには、ルートメンバーのTopology Connectorサービスの許可リストにそのインスタンスを追加します。

Web コンソールまたは sling:OsgiConfig ノードを使用して、org.apache.sling.discovery.impt.Config サービスの以下のプロパティを設定します。

<table>
 <tbody>
  <tr>
   <th>プロパティ名</th>
   <th>OSGi 名</th>
   <th>説明</th>
   <th>デフォルト値</th>
  </tr>
  <tr>
   <td>ハートビートタイムアウト（秒）</td>
   <td>heartbeatTimeout</td>
   <td>ターゲットのインスタンスを使用不可と見なすまでにハートビート応答を待機する時間（秒単位）。 </td>
   <td>20</td>
  </tr>
  <tr>
   <td>ハートビート間隔（秒）</td>
   <td>heartbeatInterval</td>
   <td>ハートビート間の時間（秒単位）。</td>
   <td>15</td>
  </tr>
  <tr>
   <td>最小イベント遅延（秒）</td>
   <td>minEventDelay</td>
   <td><p>トポロジに変更が発生した場合、状態の変更をTOPOLOGY_CHANGINGからTOPOLOGY_CHANGEDに遅延する時間。 状態がTOPOLOGY_CHANGINGの場合に発生する各変更は、この時間だけ遅延を増やします。</p> <p>この遅延によって、リスナーに大量のイベントが送られるのを防ぎます。 </p> <p>遅延を使用しない場合は、0 または負の数を指定します。</p> </td>
   <td>3</td>
  </tr>
  <tr>
   <td>Topology Connector URL</td>
   <td>topologyConnectorUrls</td>
   <td>ハートビートメッセージを送信する Topology Connector サービスの URL。</td>
   <td>http://localhost:4502/libs/sling/topology/connector</td>
  </tr>
  <tr>
   <td>トポロジコネクタ許可リスト</td>
   <td>topologyConnectorWhitelist</td>
   <td>ローカル Topology Connector サービスによってトポロジ内で許可される IP アドレスまたはホスト名のリスト。 </td>
   <td><p>localhost</p> <p>127.0.0.1</p> </td>
  </tr>
  <tr>
   <td>リポジトリ記述子名</td>
   <td>leaderElectionRepositoryDescriptor</td>
   <td> </td>
   <td>&lt;値なし&gt;</td>
  </tr>
 </tbody>
</table>

以下の手順を使用して、CQ インスタンスをトポロジのルートメンバーに接続します。この手順では、インスタンスがルートトポロジメンバーの Topology Connector URL を指すようにします。この手順をトポロジのすべてのメンバーで実行します。

1. ブラウザーで Web コンソールを開きます（[http://localhost:4502/system/console](http://localhost:4502/system/console)）。
1. Main／Topology Management をクリックします。
1. 「 Configure Discovery Service」をクリックします。
1. Topology Connector URL プロパティに項目を追加し、ルートトポロジメンバーの Topology Connector サービスの URL を指定します。URLは、https://rootservername:4502/libs/sling/topology/connectorの形式で指定します。

トポロジのルートメンバーで以下の手順を実行します。この手順では、他のトポロジメンバの名前がDiscovery Service許可リストに追加されます。

1. ブラウザーで Web コンソールを開きます（[http://localhost:4502/system/console](http://localhost:4502/system/console)）。
1. Main／Topology Management をクリックします。
1. 「 Configure Discovery Service」をクリックします。
1. トポロジの各メンバに対して、[トポロジコネクタ許可リスト]プロパティに項目を追加し、トポロジメンバのホスト名またはIPアドレスを指定します。

## トピック使用の設定 {#configuring-topic-consumption}

オフロードするブラウザーを使用して、トポロジ内の Experience Manager インスタンスのトピック使用を設定します。インスタンスごとに、使用するトピックを指定できます。例えば、1 つのインスタンスのみが特定のタイプのトピックを使用するようにトポロジを設定するには、その 1 つのインスタンスを除くすべてのインスタンスでそのトピックを無効にします。

ジョブは、関連するトピックがラウンドロビンロジックを使用して有効になっているインスタンス間で分散されます。

1. タッチ UI を使用して、「ツール」タブをクリックします（[http://localhost:4502/tools.html](http://localhost:4502/tools.html)）。
1. Granite の操作エリアで、「オフロードするブラウザー」をクリックします。
1. ナビゲーションパネルで、「オフロードするブラウザー」をクリックします。

   オフロードトピックと、トピックを使用できるサーバーインスタンスが表示されます。

   ![chlimage_1-113](assets/chlimage_1-113.png)

1. インスタンスに対するトピックの使用を無効にするには、トピック名の下のインスタンスの横にある「無効」をクリックします。
1. あるインスタンスのすべてのトピック使用を設定するには、トピックの下にあるインスタンス識別子をクリックします。

   ![chlimage_1-114](assets/chlimage_1-114.png)

1. トピックの横にある以下のボタンのいずれかをクリックし、インスタンスの使用動作を設定して、「保存」をクリックします。

   * 有効：このインスタンスはこのトピックのジョブを使用します。
   * 無効：このインスタンスはこのトピックのジョブを使用しません。
   * 排他：このインスタンスはこのトピックのみのジョブを使用します。
   **注意：**&#x200B;あるトピックに対して「排他」を選択すると、他のすべてのトピックは自動的に「無効」に設定されます。

### インストール済みの JobConsumer {#installed-job-consumers}

複数の JobConsumer 実装が Experience Manager とともにインストールされます。これらの JobConsumer が登録されているトピックが、オフロードするブラウザーに表示されます。表示されるその他のトピックは、カスタム JobConsumer で登録されたトピックです。以下の表に、デフォルトの JobConsumer を示します。

| ジョブトピック | サービス PID | 説明 |
|---|---|---|
| ／ | org.apache.sling.event.impl.jobs.deprecated.EventAdminBridge | Apache Sling とともにインストールされます。下位互換性のために、OSGi イベント管理によって生成されたジョブを処理します。 |
| com/day/cq/replication/job/&amp;ast; | com.day.cq.replication.impl.AgentManagerImpl | ジョブペイロードをレプリケートするレプリケーションエージェント。 |
| com/adobe/granite/workflow/offloading | com.adobe.granite.workflow.core.offloading.WorkflowOffloadingJobConsumer | DAM アセット更新オフローダーワークフローによって生成されたジョブを処理します。 |

### インスタンスのトピックの無効化と有効化 {#disabling-and-enabling-topics-for-an-instance}

Apache Sling Job Consumer Managerサービスには、トピックの許可リストおよびブロックリストのプロパティが用意されています。 これらのプロパティを設定して、Experience Manager インスタンスでの特定のトピックの処理を有効または無効にします。

**注意：**&#x200B;インスタンスがトポロジに属している場合は、トポロジ内の任意のコンピューターでオフロードするブラウザーを使用して、トピックを有効または無効にすることもできます。

有効なトピックのリストを作成するロジックでは、最初に許可リスト内のすべてのトピックが許可され、次にブロックリスト上のトピックが削除されます。 デフォルトでは、すべてのトピックが有効(許可リスト値は `*`)で、トピックは無効(ブロックリストに値がない)になっています。

Web コンソールまたは `sling:OsgiConfig` ノードを使用して、以下のプロパティを設定します。`sling:OsgiConfig` ノードの場合、JobConsumer Manager サービスの PID は、org.apache.sling.event.impl.jobs.JobConsumerManager です。

| Web コンソールでのプロパティ名 | OSGi ID | 説明 |
|---|---|---|
| トピック許可リスト | job.consumermanager.whitelist | ローカル JobManager サービスによって処理されるトピックのリスト。&amp;ast；のデフォルト値 を指定すると、すべてのトピックが登録済みのTopicConsumerサービスに送信されます。 |
| トピックブロックリスト | job.consumermanager.blacklist | ローカル JobManager サービスによって処理されないトピックのリスト。 |

## オフロードのレプリケーションエージェントの作成 {#creating-replication-agents-for-offloading}

オフロードフレームワークでは、作成者とワーカー間のリソースの転送にレプリケーションが使用されます。インスタンスがトポロジに参加すると、オフロードフレームワークによってレプリケーションエージェントが自動的に作成されます。エージェントはデフォルト値を使用して作成されます。エージェントが認証に使用するパスワードを手動で変更する必要があります。

>[!CAUTION]
>
>自動的に生成されるレプリケーションエージェントには既知の問題があるので、新しいレプリケーションエージェントを手動で作成する必要があります。オフロードのエージェントを作成する前に、[自動生成されたレプリケーションエージェントの使用に関する問題](/help/sites-deploying/offloading.md#problems-using-the-automatically-generated-replication-agents)の手順に従ってください。

オフロードのためにインスタンス間でジョブペイロードを転送するレプリケーションエージェントを作成します。以下の図に、作成者からワーカーインスタンスへのオフロードに必要なエージェントを示します。作成者のSling IDは1で、ワーカーインスタンスのSling IDは2です。

![chlimage_1-115](assets/chlimage_1-115.png)

この設定では、以下の 3 つのエージェントが必要です。

1. ワーカーインスタンスへレプリケートする、オーサーインスタンス上の送信エージェント
1. ワーカーインスタンス上のアウトボックスから引き出す、オーサーインスタンス上のリバースエージェント
1. ワーカーインスタンス上のアウトボックスエージェント

このレプリケーションスキームは、オーサーインスタンスとパブリッシュインスタンスの間で使用されるものと同様です。ただし、オフロードの場合は、関係するすべてのインスタンスはオーサーインスタンスです。

>[!NOTE]
>
>オフロードフレームワークでは、トポロジを使用してオフロードインスタンスの IP アドレスが取得されます。次に、これらの IP アドレスに基づいて、レプリケーションエージェントが自動的に作成されます。オフロード中のインスタンスのIPアドレスが後で変更された場合、その変更は、インスタンスの再起動後にトポロジに自動的に反映されます。 ただし、オフロードフレームワークでは、新しい IP アドレスを反映するようにレプリケーションエージェントが自動的に更新されることはありません。この状況を回避するには、トポロジ内のすべてのインスタンスに固定IPアドレスを使用します。

### オフロードのレプリケーションエージェントの命名 {#naming-the-replication-agents-for-offloading}

Use a specific format for the ***Name*** property of the replication agents so that the offloading framework automatically uses the correct agent for specific worker instances.

**オーサーインスタンスの送信エージェントの命名：**

`offloading_<slingid>`( `<slingid>` は、ワーカーインスタンスのSling IDです)。

例: `offloading_f5c8494a-4220-49b8-b079-360a72f71559`

**オーサーインスタンスのリバースエージェントの命名：**

`offloading_reverse_<slingid>`( `<slingid>` は、ワーカーインスタンスのSling IDです)。

例: `offloading_reverse_f5c8494a-4220-49b8-b079-360a72f71559`

**ワーカーインスタンスのアウトボックスの命名：**

`offloading_outbox`

### 送信エージェントの作成 {#creating-the-outgoing-agent}

1. 作成者で&#x200B;**レプリケーションエージェント**&#x200B;を作成します(レプリケーションエージェントの [ドキュメントを参照](/help/sites-deploying/replication.md))。 任意の **タイトルを指定します**。 「 **名前** 」は、命名規則に従う必要があります。
1. 以下のプロパティを使用してエージェントを作成します。

   | プロパティ | 値 |
   |---|---|
   | 設定／シリアル化の種類 | デフォルト |
   | トランスポート／トランスポート URI | https://*`<ip of target instance>`*:*`<port>`*`/bin/receive?sling:authRequestLogin=1` |
   | トランスポート／トランスポートユーザー | ターゲットインスタンスのレプリケーションユーザー |
   | Transport/Transport Password | ターゲットインスタンスのレプリケーションユーザーパスワード |
   | 拡張／HTTP メソッド | POST |
   | トリガー／デフォルトを無視 | True |

### リバースエージェントの作成 {#creating-the-reverse-agent}

1. Create a **Reverse Replication Agent** on author. (レプリケーションエージェントの [ドキュメントを参照](/help/sites-deploying/replication.md))。 任意の **タイトルを指定します**。 「 **名前** 」は、命名規則に従う必要があります。
1. 以下のプロパティを使用してエージェントを作成します。

   | プロパティ | 値 |
   |---|---|
   | 設定／シリアル化の種類 | デフォルト |
   | トランスポート／トランスポート URI | https://*`<ip of target instance>`*:*`<port>`*`/bin/receive?sling:authRequestLogin=1` |
   | トランスポート／トランスポートユーザー | ターゲットインスタンスのレプリケーションユーザー |
   | Transport/Transport Password | ターゲットインスタンスのレプリケーションユーザーパスワード |
   | 拡張／HTTP メソッド | GET |

### アウトボックスエージェントの作成 {#creating-the-outbox-agent}

1. ワーカーインスタンスに **複製エージェント** を作成します。 (レプリケーションエージェントの [ドキュメントを参照](/help/sites-deploying/replication.md))。 任意の **タイトルを指定します**。 「 **名前** 」は必須で `offloading_outbox`す。
1. 以下のプロパティを使用してエージェントを作成します。

   | プロパティ | 値 |
   |---|---|
   | 設定／シリアル化の種類 | デフォルト |
   | トランスポート／トランスポート URI | repo://var/replication/outbox |
   | トリガー／デフォルトを無視 | True |

### Sling ID の検索 {#finding-the-sling-id}

以下のいずれかの方法を使用して、Experience Manager インスタンスの Sling ID を取得します。

* Open the Web Console and, in the Sling Settings, find the value of the Sling ID property ([http://localhost:4502/system/console/status-slingsettings](http://localhost:4502/system/console/status-slingsettings)). このメソッドは、インスタンスがまだトポロジに含まれていない場合に役立ちます。
* インスタンスが既にトポロジの一部である場合は、トポロジブラウザーを使用します。

## DAM アセットの処理のオフロード {#offloading-the-processing-of-dam-assets}

DAM で追加または更新されたアセットのバックグラウンド処理が特定のインスタンスによって実行されるように、トポロジのインスタンスを設定します。

By default, Experience Manager executes the [!UICONTROL DAM Update Asset] workflow when a DAM asset changes or one is added to DAM. Change the default behavior so that Experience Manager instead executes the [!UICONTROL DAM Update Asset Offloader] workflow. This workflow generates a JobManager job that has a topic of `com/adobe/granite/workflow/offloading`. Then, configure the topology so that the job is offloaded to a dedicated worker.

>[!CAUTION]
>
>ワークフローのオフロードで使用する場合、ワークフローは一時的なものではありません。 For example, the [!UICONTROL DAM Update Asset] workflow must not be transient when used for asset offloading. To set/unset the transient flag on a workflow, see [Transient Workflows](/help/assets/performance-tuning-guidelines.md#workflows).

以下の手順では、次の特徴を持つオフロードトポロジを想定しています。

* 1 つ以上の Experience Manager インスタンスがオーサーインスタンスであり、ユーザーは DAM アセットの追加または更新のためにこのインスタンスとやり取りします。
* ユーザーは、DAM アセットを処理する 1 つ以上の Experience Manager インスタンスと直接的にはやり取りしません。これらのインスタンスは、DAM アセットのバックグラウンド処理専用です。

1. 各 Experience Manager インスタンスで、ルート Topology Connector を指すように Discovery Service を設定します（[トポロジメンバーシップの設定](#title4)を参照）。
1. 接続するインスタンスが許可リスト上に来るようにルートの地形コネクタを設定します。
1. Open Offloading Browser and disable the `com/adobe/granite/workflow/offloading` topic on the instances with which users interact to upload or change DAM assets.

   ![chlimage_1-116](assets/chlimage_1-116.png)

1. On each instance that users interact with to upload or change DAM assets, configure workflow launchers to use the [!UICONTROL DAM Update Asset Offloading] workflow:

   1. ワークフローコンソールを開きます。
   1. 「ランチャー」タブをクリックします。
   1. Locate the two Launcher configurations that execute the [!UICONTROL DAM Update Asset] workflow. One launcher configuration event type is Node Created, and the other type is Node Modified.
   1. Change both event types so that they execute the [!UICONTROL DAM Update Asset Offloading] workflow. (For information about launcher configurations, see [Starting Workflows When Nodes Change](/help/sites-administering/workflows-starting.md).)

1. On the instances that perform the background processing of DAM assets, disable the workflow launchers that execute the [!UICONTROL DAM Update Asset] workflow.

## 参考情報 {#further-reading}

このページで説明した詳細以外に、以下を参照することもできます。

* For information about using Java APIs to create jobs and job consumers, see [Creating and Consuming Jobs for Offloading](/help/sites-developing/dev-offloading.md).
