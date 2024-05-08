---
title: ジョブのオフロード
description: 特定のタイプの処理を実行するために、トポロジ内の AEM インスタンスを設定および使用する方法について説明します。
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Configuring
exl-id: 429c96ff-4185-4215-97e8-9bd2c130a9b1
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '2318'
ht-degree: 99%

---

# ジョブのオフロード{#offloading-jobs}

## はじめに {#introduction}

オフロードによって、トポロジ内の Experience Manager インスタンス間で処理タスクが配布されます。オフロードを使用すると、特定の Experience Manager インスタンスを使用して特定のタイプの処理を実行できます。特殊化した処理により、使用可能なサーバーリソースの使用を最大限に活用できます。

オフロードは、[Apache Sling Discovery](https://sling.apache.org/documentation/bundles/discovery-api-and-impl.html) および Sling JobManager の機能に基づきます。オフロードを使用するには、Experience Manager クラスターをトポロジに追加し、クラスターで処理するジョブトピックを特定します。クラスターは 1 つ以上の Experience Manager インスタンスで構成され、単一のインスタンスがクラスターと見なされます。

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

オフロードフレームワークによってジョブを実行するクラスターが選択される際に、そのクラスターが複数のインスタンスで構成されていると、Sling 配布によってクラスター内のどのインスタンスがジョブを実行するかが決定されます。

### ジョブペイロード {#job-payloads}

オフロードフレームワークでは、ジョブをリポジトリ内のリソースと関連付けるジョブペイロードがサポートされています。ジョブペイロードは、ジョブがリソースを処理するために作成されたり、別のコンピューターにオフロードされたりする場合に役立ちます。

ジョブの作成時に、ペイロードはそのジョブを作成するインスタンスにのみ配置されることが保証されます。ジョブのオフロード時に、レプリケーションエージェントによって、ペイロードが最終的にジョブを使用するインスタンスで作成されます。ジョブ実行が完了すると、リバースレプリケーションによって、ペイロードのコピーがジョブを作成したインスタンスに戻されます。

## トポロジの管理 {#administering-topologies}

トポロジは、オフロードに使用される疎結合の Experience Manager クラスターです。クラスターは 1 つ以上の Experience Manager サーバーインスタンスで構成されます（単一のインスタンスがクラスターと見なされます）。

各 Experience Manager インスタンスによって、以下のオフロード関連サービスが実行されます。

* Discovery Service：トポロジに参加するために Topology Connector にリクエストを送信します。
* Topology Connector：参加リクエストを受信し、各リクエストを承認または拒否します。

トポロジのすべてのメンバーの Discovery Service は、メンバーのうちの 1 つの Topology Connector を参照しています。以下の節では、このメンバーをルートメンバーと呼びます。

![chlimage_1-110](assets/chlimage_1-110.png)

トポロジ内の各クラスターには、リーダーと認識されるインスタンスが含まれています。クラスターリーダーは、クラスターの他のメンバーの代わりにトポロジとやり取りします。リーダーがクラスターから外れると、クラスターの新しいリーダーが自動的に選択されます。

### トポロジの表示 {#viewing-the-topology}

トポロジブラウザーを使用して、Experience Manager インスタンスが参加しているトポロジの状態を調べます。トポロジブラウザーには、トポロジのクラスターおよびインスタンスが表示されます。

クラスターごとに、クラスターメンバーのリストが表示されます。このリストには、各メンバーがクラスターに参加した順序と、どのメンバーがリーダーかが示されています。現在プロパティによって、現在管理しているインスタンスが示されます。

クラスターの各インスタンスについて、複数のトポロジ関連プロパティを確認できます。

* インスタンスのジョブコンシューマーが担当するトピックの許可リスト。
* トポロジとの接続用に公開されるエンドポイント
* インスタンスがどのジョブトピックについてオフロード用に登録されているか
* インスタンスによって処理されるジョブトピック

1. タッチ UI を使用して、「ツール」タブをクリックします。([http://localhost:4502/tools.html](http://localhost:4502/tools.html))
1. Granite の操作エリアで、「オフロードするブラウザー」をクリックします。
1. ナビゲーションパネルで、「トポロジブラウザー」をクリックします。

   トポロジに参加しているクラスターが表示されます。

   ![chlimage_1-111](assets/chlimage_1-111.png)

1. クラスターをクリックして、クラスターのインスタンスとそれらの ID、現在ステータスおよびリーダーステータスのリストを表示します。
1. インスタンス ID をクリックして、詳細なプロパティを表示します。

Web コンソールを使用してトポロジ情報を表示することもできます。コンソールには、トポロジのクラスターに関するその他の情報が表示されます。

* どのインスタンスがローカルインスタンスであるか
* このインスタンスがトポロジに接続するために使用する Topology Connector サービス（送信）と、このインスタンスに接続するサービス（受信）
* トポロジおよびインスタンスのプロパティの変更履歴

以下の手順を使用して、web コンソールの Topology Management ページを開きます。

1. ブラウザーで web コンソールを開きます。([http://localhost:4502/system/console](http://localhost:4502/system/console))
1. Main／Topology Management をクリックします。

   ![chlimage_1-112](assets/chlimage_1-112.png)

### トポロジメンバーシップの設定 {#configuring-topology-membership}

Experience Manager インスタンスとトポロジとのインタラクション方法を制御するために、Apache Sling のリソースベースの Discovery Service が各インスタンスで実行されます。

Discovery Service によって、トポロジとの接続を確立および維持するために、定期的な POST リクエスト（ハートビート）が Topology Connector サービスに送信されます。Topology Connector サービスでは、トポロジへの参加が許可される IP アドレスまたはホスト名の許可リストを維持管理します。

* インスタンスをトポロジに参加させるには、ルートメンバーの Topology Connector サービスの URL を指定します。
* インスタンスがトポロジに参加できるようにするには、ルートメンバーの Topology Connector サービスの許可リストにインスタンスを追加します。

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
   <td><p>トポロジに対して変更が発生したときに、TOPOLOGY_CHANGING から TOPOLOGY_CHANGED への状態の変更を遅延させる時間。状態が TOPOLOGY_CHANGING のときに発生する変更につき、この時間だけ遅延が大きくなります。</p> <p>この遅延によって、リスナーに大量のイベントが送られるのを防ぎます。 </p> <p>遅延を使用しない場合は、0 または負の数を指定します。</p> </td>
   <td>3</td>
  </tr>
  <tr>
   <td>Topology Connector URL</td>
   <td>topologyConnectorUrls</td>
   <td>ハートビートメッセージを送信する Topology Connector サービスの URL。</td>
   <td>http://localhost:4502/libs/sling/topology/connector</td>
  </tr>
  <tr>
   <td>Topology Connector 許可リスト</td>
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

1. ブラウザーで web コンソールを開きます。([http://localhost:4502/system/console](http://localhost:4502/system/console))
1. Main／Topology Management をクリックします。
1. 「Configure Discovery Service」をクリックします。
1. Topology Connector URL プロパティに項目を追加し、ルートトポロジメンバーの Topology Connector サービスの URL を指定します。URL の形式は、https://rootservername:4502/libs/sling/topology/connector です。

トポロジのルートメンバーで以下の手順を実行します。この手順では、ルートメンバーの Discovery Service 許可リストに他のトポロジメンバーの名前を追加します。

1. ブラウザーで web コンソールを開きます。([http://localhost:4502/system/console](http://localhost:4502/system/console))
1. Main／Topology Management をクリックします。
1. 「Configure Discovery Service」をクリックします。
1. トポロジの各メンバーについて、Topology Connector の許可リストプロパティに項目を追加し、トポロジメンバーのホスト名または IP アドレスを指定します。

## トピック使用の設定 {#configuring-topic-consumption}

オフロードするブラウザーを使用して、トポロジ内の Experience Manager インスタンスのトピック使用を設定します。インスタンスごとに、使用するトピックを指定できます。例えば、1 つのインスタンスのみが特定のタイプのトピックを使用するようにトポロジを設定するには、その 1 つのインスタンスを除くすべてのインスタンスでそのトピックを無効にします。

ジョブは、ラウンドロビンロジックを使用して、関連するトピックが有効なインスタンス間で配布されます。

1. タッチ UI を使用して、「ツール」タブをクリックします。([http://localhost:4502/tools.html](http://localhost:4502/tools.html))
1. Granite の操作エリアで、「オフロードするブラウザー」をクリックします。
1. ナビゲーションパネルで、「オフロードするブラウザー」をクリックします。

   オフロードトピックと、トピックを使用できるサーバーインスタンスが表示されます。

   ![chlimage_1-113](assets/chlimage_1-113.png)

1. インスタンスのトピック使用を無効にするには、トピック名の下で、インスタンスの横の「無効にする」をクリックします。
1. あるインスタンスのすべてのトピック使用を設定するには、トピックの下にあるインスタンス識別子をクリックします。

   ![chlimage_1-114](assets/chlimage_1-114.png)

1. トピックの横にある以下のボタンのいずれかをクリックし、インスタンスの使用動作を設定して、「保存」をクリックします。

   * 有効：このインスタンスはこのトピックのジョブを使用します。
   * 無効：このインスタンスはこのトピックのジョブを使用しません。
   * 排他：このインスタンスはこのトピックのみのジョブを使用します。

   **メモ：**&#x200B;あるトピックに対して「排他」を選択すると、他のすべてのトピックは自動的に「無効」に設定されます。

### インストール済みの JobConsumer {#installed-job-consumers}

複数の JobConsumer 実装が Experience Manager と共にインストールされます。これらの JobConsumer が登録されているトピックが、オフロードするブラウザーに表示されます。表示されるその他のトピックは、カスタム JobConsumer で登録されたトピックです。以下の表に、デフォルトの JobConsumer を示します。

| ジョブトピック | サービス PID | 説明 |
|---|---|---|
| ／ | org.apache.sling.event.impl.jobs.deprecated.EventAdminBridge | Apache Sling と共にインストールされます。後方互換性のために、OSGi イベント管理によって生成されたジョブを処理します。 |
| com/day/cq/replication/job/&amp;ast; | com.day.cq.replication.impl.AgentManagerImpl | ジョブペイロードをレプリケートするレプリケーションエージェント。 |

<!--
| com/adobe/granite/workflow/offloading |com.adobe.granite.workflow.core.offloading.WorkflowOffloadingJobConsumer |Processes jobs that the DAM Update Asset Offloader workflow generates. |
-->

### インスタンスのトピックの無効化と有効化 {#disabling-and-enabling-topics-for-an-instance}

Apache Sling JobConsumer Manager サービスによって、トピックの許可リストプロパティとブロックリストプロパティが提供されます。これらのプロパティを設定して、Experience Manager インスタンスでの特定のトピックの処理を有効または無効にします。

**注意：**&#x200B;インスタンスがトポロジに属している場合は、トポロジ内の任意のコンピューターでオフロードするブラウザーを使用して、トピックを有効または無効にすることもできます。

有効化されたトピックのリストを作成するロジックでは、まず許可リスト内のすべてのトピックを許可した後、ブロックリスト内のトピックを削除します。デフォルトでは、すべてのトピックが有効になり（許可リストの値は `*`）、無効になるトピックはありません（ブロックリストの値がありません）。

Web コンソールまたは `sling:OsgiConfig` ノードを使用して、以下のプロパティを設定します。`sling:OsgiConfig` ノードの場合、JobConsumer Manager サービスの PID は、org.apache.sling.event.impl.jobs.JobConsumerManager です。

| Web コンソールでのプロパティ名 | OSGi ID | 説明 |
|---|---|---|
| トピック許可リスト | job.consumermanager.whitelist | ローカル JobManager サービスによって処理されるトピックのリスト。デフォルト値の &amp;ast; では、すべてのトピックが登録済み TopicConsumer サービスに送信されます。 |
| トピックブロックリスト | job.consumermanager.blacklist | ローカル JobManager サービスによって処理されないトピックのリスト。 |

## オフロードのレプリケーションエージェントの作成 {#creating-replication-agents-for-offloading}

オフロードフレームワークでは、作成者とワーカー間のリソースの転送にレプリケーションが使用されます。インスタンスがトポロジに参加すると、オフロードフレームワークによってレプリケーションエージェントが自動的に作成されます。エージェントはデフォルト値を使用して作成されます。エージェントが認証に使用するパスワードを手動で変更します。

>[!CAUTION]
>
>自動生成されたレプリケーションエージェントには既知の問題があるので、新しいレプリケーションエージェントを手動で作成する必要があります。

オフロードのためにインスタンス間でジョブペイロードを転送するレプリケーションエージェントを作成します。以下の図に、作成者からワーカーインスタンスへのオフロードに必要なエージェントを示します。オーサーの Sling ID は 1、ワーカーインスタンスの Sling ID は 2 です。

![chlimage_1-115](assets/chlimage_1-115.png)

この設定では、以下の 3 つのエージェントが必要です。

1. ワーカーインスタンスへレプリケートする、オーサーインスタンス上の送信エージェント
1. ワーカーインスタンス上のアウトボックスから引き出す、オーサーインスタンス上のリバースエージェント
1. ワーカーインスタンス上のアウトボックスエージェント

このレプリケーションスキームは、オーサーインスタンスとパブリッシュインスタンスの間で使用されるものと同様です。ただし、オフロードの場合は、関係するすべてのインスタンスはオーサーインスタンスです。

>[!NOTE]
>
>オフロードフレームワークでは、トポロジを使用してオフロードインスタンスの IP アドレスが取得されます。次に、これらの IP アドレスに基づいて、レプリケーションエージェントが自動的に作成されます。オフロードインスタンスの IP アドレスが後で変更された場合、変更はインスタンスの再起動後にトポロジ上で自動的に伝搬されます。ただし、オフロードフレームワークでは、新しい IP アドレスを反映するようにレプリケーションエージェントが自動的に更新されることはありません。この状況を回避するには、トポロジ内のすべてのインスタンスに固定 IP アドレスを使用します。

### オフロードのレプリケーションエージェントの命名 {#naming-the-replication-agents-for-offloading}

オフロードフレームワークによって特定のワーカーインスタンスに対して適切なエージェントが自動的に使用されるように、レプリケーションエージェントの「***名前***」プロパティに特定のフォーマットを使用します。

**オーサーインスタンスの送信エージェントの命名：**

`offloading_<slingid>`、ここで `<slingid>` は、ワーカーインスタンスの Sling ID です。

例：`offloading_f5c8494a-4220-49b8-b079-360a72f71559`

**オーサーインスタンスのリバースエージェントの命名：**

`offloading_reverse_<slingid>`、ここで `<slingid>` は、ワーカーインスタンスの Sling ID です。

例：`offloading_reverse_f5c8494a-4220-49b8-b079-360a72f71559`

**ワーカーインスタンスのアウトボックスの命名：**

`offloading_outbox`

### 送信エージェントの作成 {#creating-the-outgoing-agent}

1. 作成者で&#x200B;**レプリケーションエージェント**&#x200B;を作成します（[レプリケーションエージェントのドキュメント](/help/sites-deploying/replication.md)を参照してください）。任意の&#x200B;**タイトル**&#x200B;を指定します。**名前**&#x200B;は命名規則に従う必要があります。
1. 以下のプロパティを使用してエージェントを作成します。

   | プロパティ | 値 |
   |---|---|
   | 設定／シリアル化の種類 | デフォルト |
   | トランスポート／トランスポート URI | https://*`<ip of target instance>`*:*`<port>`*`/bin/receive?sling:authRequestLogin=1` |
   | トランスポート／トランスポートユーザー | ターゲットインスタンスのレプリケーションユーザー |
   | トランスポート／トランスポートパスワード | ターゲットインスタンスのレプリケーションユーザーパスワード |
   | 拡張／HTTP メソッド | POST |
   | トリガー／デフォルトを無視 | True |

### リバースエージェントの作成 {#creating-the-reverse-agent}

1. 作成者に&#x200B;**リバースレプリケーションエージェント**&#x200B;を作成します。（[レプリケーションエージェントのドキュメント](/help/sites-deploying/replication.md)を参照してください）。任意の&#x200B;**タイトル**&#x200B;を指定します。**名前**&#x200B;は命名規則に従う必要があります。
1. 以下のプロパティを使用してエージェントを作成します。

   | プロパティ | 値 |
   |---|---|
   | 設定／シリアル化の種類 | デフォルト |
   | トランスポート／トランスポート URI | https://*`<ip of target instance>`*:*`<port>`*`/bin/receive?sling:authRequestLogin=1` |
   | トランスポート／トランスポートユーザー | ターゲットインスタンスのレプリケーションユーザー |
   | トランスポート／トランスポートパスワード | ターゲットインスタンスのレプリケーションユーザーパスワード |
   | 拡張／HTTP メソッド | GET |

### アウトボックスエージェントの作成 {#creating-the-outbox-agent}

1. ワーカーインスタンス上に&#x200B;**レプリケーションエージェント**&#x200B;を作成します。（[レプリケーションエージェントのドキュメント](/help/sites-deploying/replication.md)を参照してください）。任意の&#x200B;**タイトル**&#x200B;を指定します。**名前**&#x200B;は `offloading_outbox` にする必要があります。
1. 以下のプロパティを使用してエージェントを作成します。

   | プロパティ | 値 |
   |---|---|
   | 設定／シリアル化の種類 | デフォルト |
   | トランスポート／トランスポート URI | repo://var/replication/outbox |
   | トリガー／デフォルトを無視 | True |

### Sling ID の検索 {#finding-the-sling-id}

以下のいずれかの方法を使用して、Experience Manager インスタンスの Sling ID を取得します。

* Web コンソールを開き、Sling 設定で、Sling ID プロパティの値を検索します（[http://localhost:4502/system/console/status-slingsettings](http://localhost:4502/system/console/status-slingsettings)）。この方法は、インスタンスがまだトポロジの一部ではない場合に役立ちます。
* インスタンスが既にトポロジの一部である場合は、トポロジブラウザーを使用します。

<!--
## Offloading the Processing of DAM Assets {#offloading-the-processing-of-dam-assets}

Configure the instances of a topology so that specific instances perform the background processing of assets that are added or updated in DAM.

By default, Experience Manager executes the [!UICONTROL DAM Update Asset] workflow when a DAM asset changes or one is added to DAM. Change the default behavior so that Experience Manager instead executes the [!UICONTROL DAM Update Asset Offloader] workflow. This workflow generates a JobManager job that has a topic of `com/adobe/granite/workflow/offloading`. Then, configure the topology so that the job is offloaded to a dedicated worker.

>[!CAUTION]
>
>No workflow should be transient when used with workflow offloading. For example, the [!UICONTROL DAM Update Asset] workflow must not be transient when used for asset offloading. To set/unset the transient flag on a workflow, see [Transient Workflows](/help/assets/performance-tuning-guidelines.md#workflows).

The following procedure assumes the following characteristics for the offloading topology:

* One or more Experience Manager instance are authoring instances that users interact with for adding or updating DAM assets.
* Users to do not directly interact with one or more Experience Manager instances that process the DAM assets. These instances are dedicated to the background processing of DAM assets.

1. On each Experience Manager instance, configure the Discovery Service so that it points to the root Topography Connector. (See [Configuring Topology Membership](#title4).)
1. Configure the root Topography Connector so that the connecting instances are on the allow list.
1. Open Offloading Browser and disable the `com/adobe/granite/workflow/offloading` topic on the instances with which users interact to upload or change DAM assets.

   ![chlimage_1-116](assets/chlimage_1-116.png)

1. On each instance that users interact with to upload or change DAM assets, configure workflow launchers to use the [!UICONTROL DAM Update Asset Offloading] workflow:

    1. Open the Workflow console.
    1. Click the Launcher tab.
    1. Locate the two Launcher configurations that execute the [!UICONTROL DAM Update Asset] workflow. One launcher configuration event type is Node Created, and the other type is Node Modified.
    1. Change both event types so that they execute the [!UICONTROL DAM Update Asset Offloading] workflow. (For information about launcher configurations, see [Starting Workflows When Nodes Change](/help/sites-administering/workflows-starting.md).)

1. On the instances that perform the background processing of DAM assets, disable the workflow launchers that execute the [!UICONTROL DAM Update Asset] workflow.
-->

## 参考情報 {#further-reading}

このページで説明した詳細以外に、以下を参照することもできます。

* Java API を使用したジョブおよびジョブコンシューマーの作成について詳しくは、[オフロードのためのジョブの作成と使用](/help/sites-developing/dev-offloading.md)を参照してください。
