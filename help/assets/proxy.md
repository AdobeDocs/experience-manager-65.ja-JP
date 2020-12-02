---
title: '[!DNL Assets] 代理開発'
description: プロキシは、 [!DNL Experience Manager] instance that uses proxy workers to process jobs. Learn how to configure an [!DNL Experience Manager] プロキシ、サポートされている操作、プロキシコンポーネント、およびカスタムプロキシワーカーの開発方法です。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 59%

---


# [!DNL Assets] 代理開発  {#assets-proxy-development}

[!DNL Adobe Experience Manager Assets] では、特定のタスクの処理を配信するためにプロキシが使用されます。

プロキシは、ジョブの処理と結果の作成を担当するプロセッサーとしてプロキシワーカーを使用する、特定の（場合によっては別々の）Experience Managerインスタンスです。 プロキシワーカーは、幅広いタスクに使用できます。[!DNL Assets]プロキシの場合は、アセット内のレンダリング用にアセットを読み込むのに使用できます。 例えば、[IDS プロキシワーカー](indesign.md)は、 Server を使用して、 Assets 内で使用できるようにファイルを処理します。[!DNL Adobe InDesign]

プロキシが別の[!DNL Experience Manager]インスタンスの場合は、Experience Managerオーサリングインスタンスの負荷を軽減するのに役立ちます。 デフォルトでは、[!DNL Assets]は、同じJVM（Proxyを介して外部化）でアセット処理タスクを実行し、Experience Managerオーサリングインスタンスの負荷を軽減します。

## プロキシ（HTTPアクセス） {#proxy-http-access}

プロキシは、次の場所で処理ジョブを受け入れるように設定されている場合、HTTPサーブレットを介して使用できます。`/libs/dam/cloud/proxy`. このサーブレットは、POST されたパラメーターから Sling ジョブを作成します。作成されたジョブはプロキシのジョブキューに追加され、適切なプロキシワーカーに接続されます。

### サポートされている操作 {#supported-operations}

* `job`

   **要件**：パラメーター `jobevent` をシリアル化されたバリューマップとして設定する必要があります。これは、ジョブプロセッサ用の`Event`を作成するために使用されます。

   **結果**：新しいジョブが追加されます。成功した場合、一意のジョブ ID が返されます。

```shell
curl -u admin:admin -F":operation=job" -F"someproperty=xxxxxxxxxxxx"
    -F"jobevent=serialized value map" http://localhost:4502/libs/dam/cloud/proxy
```

* `result`

   **要件**:パラメーターを設定 `jobid` する必要があります。

   **結果**：ジョブプロセッサーによって作成されたノードの JSON 表現が返されます。

```shell
curl -u admin:admin -F":operation=result" -F"jobid=xxxxxxxxxxxx"
    http://localhost:4502   /libs/dam/cloud/proxy
```

* `resource`

   **要件**：パラメーター jobid を設定する必要があります。

   **結果**：指定されたジョブに関連付けられているリソースが返されます。

```shell
curl -u admin:admin -F":operation=resource" -F"jobid=xxxxxxxxxxxx"
    -F"resourcePath=something.pdf" http://localhost:4502/libs/dam/cloud/proxy
```

* `remove`

   **要件**：パラメーター jobid を設定する必要があります。

   **結果**：見つかった場合にジョブが削除されます。

```shell
curl -u admin:admin -F":operation=remove" -F"jobid=xxxxxxxxxxxx"
    http://localhost:4502/libs/dam/cloud/proxy
```

### プロキシワーカー {#proxy-worker}

プロキシワーカーは、ジョブの処理および結果の作成を担当するプロセッサーです。ワーカーはプロキシインスタンスにあり、プロキシワーカーとして認識されるには、[sling JobProcessor](https://sling.apache.org/site/eventing-and-jobs.html) を実装する必要があります。

>[!NOTE]
>
>ワーカーがプロキシワーカーとして認識されるには、[sling JobProcessor](https://sling.apache.org/site/eventing-and-jobs.html) を実装する必要があります。

### クライアント API  {#client-api}

[`JobService`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html) は、ジョブを作成および削除し、ジョブの結果を取得するためのメソッドを提供する OSGi サービスとして使用できます。このサービスのデフォルトの実装（`JobServiceImpl`）は、HTTP クライアントを使用して、リモートプロキシサーブレットと通信します。

API の使用例を以下に示します。

```java
@Reference
 JobService proxyJobService;

 // to create a new job
 final Hashtable props = new Hashtable();
 props.put("someproperty", "some value");
 props.put(JobUtil.PROPERTY_JOB_TOPIC, "myworker/job"); // this is an identifier of the worker
 final String jobId = proxyJobService.addJob(props, new Asset[]{asset});

 // to check status (returns JobService.STATUS_FINISHED or JobService.STATUS_INPROGRESS)
 int status = proxyJobService.getStatus(jobId)

 // to get the result
 final String jsonString = proxyJobService.getResult(jobId);

 // to remove job and cleanup
 proxyJobService.removeJob(jobId);
```

### クラウドサービス設定 {#cloud-service-configurations}

>[!NOTE]
>
>プロキシ API の参考ドキュメントは、[`com.day.cq.dam.api.proxy`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/proxy/package-summary.html) にあります。

プロキシとプロキシの両方のワーカー設定は、クラウドサービスの設定を介して、[!DNL Assets] **ツール**&#x200B;コンソールまたは`/etc/cloudservices/proxy`からアクセスできるように設定できます。 各プロキシワーカーは、`/etc/cloudservices/proxy`の下にノードを追加して、ワーカー固有の構成の詳細（例：`/etc/cloudservices/proxy/workername`）を確認する必要があります。

>[!NOTE]
>
>詳細については、[InDesign Serverプロキシワーカーの構成](indesign.md#configuring-the-proxy-worker-for-indesign-server)と[Cloud Servicesの構成](../sites-developing/extending-cloud-config.md)を参照してください。

API の使用例を以下に示します。

```java
@Reference(policy = ReferencePolicy.STATIC)
 ProxyConfig proxyConfig;

 // to get proxy config
 Configuration cloudConfig = proxyConfig.getConfiguration();
 final String value = cloudConfig.get("someProperty", "defaultValue");

 // to get worker config
 Configuration cloudConfig = proxyConfig.getConfiguration("workername");
 final String value = cloudConfig.get("someProperty", "defaultValue");
```

### カスタマイズしたプロキシワーカーの開発 {#developing-a-customized-proxy-worker}

[IDSプロキシワーカー](indesign.md)は、既にあらかじめ用意されている[!DNL Assets]プロキシワーカーの例です。この例では、InDesignアセットの処理をアウトソースします。

独自の[!DNL Assets]プロキシワーカーを開発および設定して、[!DNL Assets]処理タスクをディスパッチし、アウトソースする専門的なワーカーを作成することもできます。

独自のカスタムプロキシワーカーを設定するには、以下を実行する必要があります。

* 以下を設定および実装します（Sling イベントを使用）。

   * カスタムジョブトピック
   * カスタムジョブイベントハンドラー

* 次に、JobService API を使用して以下を実行します。

   * プロキシへのカスタムジョブのディスパッチ
   * ジョブの管理

* ワークフローからプロキシを使用する場合は、WorkflowExternalProcess API および JobService API を使用して、カスタム外部手順を実装する必要があります。

以下の図および手順に、実行方法の詳細を示します。

![chlimage_1-249](assets/chlimage_1-249.png)

>[!NOTE]
>
>次の手順では、InDesignの等価性を参照例として示します。

1. [Sling ジョブ](https://sling.apache.org/site/eventing-and-jobs.html)が使用されるので、ユーザーの使用例向けにジョブトピックを定義する必要があります。

   例として、IDS プロキシワーカーの `IDSJob.IDS_EXTENDSCRIPT_JOB` を参照してください。

1. 外部手順を使用してイベントを呼び出し、それが終了するまで待機します。これは、ID をポーリングすることによって実行されます。新機能を実装する独自の手順を開発する必要があります。

   `WorkflowExternalProcess` を実装してから、JobService API およびジョブトピックを使用してジョブイベントを準備し、JobService（OSGi サービス）にディスパッチします。

   例として、IDS プロキシワーカーの `INDDMediaExtractProcess`.java を参照してください。

1. トピックのジョブハンドラーを実装します。特定のアクションを実行し、ワーカー実装と見なされるように、このハンドラーを開発する必要があります。

   例として、IDS プロキシワーカーの `IDSJobProcessor.java` を参照してください。

1. dam-commons の `ProxyUtil.java` を使用します。これにより、DAM プロキシを使用してジョブをワーカーにディスパッチできます。

>[!NOTE]
>
>[!DNL Assets]プロキシフレームワークがすぐに使えるのはプールのメカニズムです。
>
>[!DNL InDesign]統合により、[!DNL InDesign]サーバーのプール(IDSPool)にアクセスできます。 このプーリングは[!DNL InDesign]統合に固有のものであり、[!DNL Assets]プロキシフレームワークの一部ではありません。

>[!NOTE]
>
>結果の同期：
>
>同じプロキシを使用するインスタンスが n 個ある場合、処理結果はプロキシに保持されます。ジョブの作成時にクライアントに与えられたのと同じ一意のジョブIDを使用して結果をリクエストするのは、クライアント(Experience Manager作成者)のジョブです。 プロキシでは、単にジョブを実行し、リクエストに備えて結果を準備しておくだけです。
