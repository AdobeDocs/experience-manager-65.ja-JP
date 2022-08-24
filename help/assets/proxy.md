---
title: '"[!DNL Assets] プロキシ開発"'
description: プロキシは、プロキシワーカーを使用してジョブを処理する  [!DNL Experience Manager]  インスタンスです。 [!DNL Experience Manager] プロキシ、サポートされている操作、プロキシコンポーネントを設定する方法、カスタムプロキシワーカーを開発する方法について説明します。
contentOwner: AG
role: Admin, Architect
exl-id: 42fff236-b4e1-4f42-922c-97da32a933cf
source-git-commit: e24316cb9495a552960ae0620e4198f10a08b691
workflow-type: tm+mt
source-wordcount: '844'
ht-degree: 100%

---

# [!DNL Assets] プロキシ開発 {#assets-proxy-development}

[!DNL Adobe Experience Manager Assets] では、特定のタスクの処理を配信するためにプロキシが使用されます。

プロキシは、ジョブの処理と結果の作成を担うプロセッサーとしてプロキシワーカーを使用する、特定の（場合によっては個別の）Experience Manager インスタンスです。プロキシワーカーは、幅広いタスクに使用できます。[!DNL Assets] プロキシの場合、これを使用して、Assets 内にレンダリングするアセットを読み込むことができます。例えば、[IDS プロキシワーカー](indesign.md)は、 Server を使用して、 Assets 内で使用できるようにファイルを処理します。[!DNL Adobe InDesign]

プロキシが個別の [!DNL Experience Manager] インスタンスである場合は、[!DNL Experience Manager] オーサリングインスタンスの負荷の軽減に役立ちます。デフォルトでは、[!DNL Assets] は同じ JVM 内（プロキシによって外部化）でアセット処理タスクを実行し、[!DNL Experience Manager] オーサリングインスタンスへの負荷を軽減させます。

## プロキシ（HTTP アクセス） {#proxy-http-access}

プロキシは、次の場所でのジョブの処理を受け入れるよう設定されている場合に、HTTP Servlet を介して使用できます。`/libs/dam/cloud/proxy`.このサーブレットは、POST されたパラメーターから Sling ジョブを作成します。作成されたジョブはプロキシのジョブキューに追加され、適切なプロキシワーカーに接続されます。

### サポートされている操作 {#supported-operations}

* `job`

   **要件**：パラメーター `jobevent` をシリアル化されたバリューマップとして設定する必要があります。ジョブプロセッサー用の `Event` の作成に使用します。

   **結果**：新しいジョブが追加されます。成功した場合、一意のジョブ ID が返されます。

```shell
curl -u admin:admin -F":operation=job" -F"someproperty=xxxxxxxxxxxx"
    -F"jobevent=serialized value map" http://localhost:4502/libs/dam/cloud/proxy
```

* `result`

   **要件**：パラメーター `jobid` を設定する必要があります。

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

### クライアント API {#client-api}

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

### クラウドサービスの設定 {#cloud-service-configurations}

<!-- TBD: Cannot find com.day.cq.dam.api.proxy at https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html which were generated in May 2020. Hiding this broken link for now.
>[!NOTE]
>
>Reference documentation for the proxy API is available under [`com.day.cq.dam.api.proxy`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/dam/api/proxy/package-summary.html).
-->

プロキシ設定とプロキシワーカー設定は、どちらもクラウドサービス設定を介して使用でき、[!DNL Assets] から&#x200B;**ツール**&#x200B;コンソールまたは `/etc/cloudservices/proxy` 以下からアクセスできます。各プロキシワーカーは、 ワーカーに固有の設定の詳細 （例： `/etc/cloudservices/proxy/workername`）で、`/etc/cloudservices/proxy` にノードを追加するように想定されています。

>[!NOTE]
>
>詳しくは、[InDesign Server プロキシワーカーの設定](indesign.md#configuring-the-proxy-worker-for-indesign-server)および[クラウドサービスの設定](../sites-developing/extending-cloud-config.md)を参照してください。

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

[IDS プロキシワーカー](indesign.md)は、InDesign アセットの処理をアウトソースするために既にデフォルトで提供されている、[!DNL Assets] プロキシワーカーの一例です。

独自の [!DNL Assets] プロキシワーカーを開発および設定して、[!DNL Assets] 処理タスクをディスパッチおよびアウトソースする専用のワーカーを作成することもできます。

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
>次の手順では、参照例として InDesign に相当するものを示しています。

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
>プールメカニズムは、[!DNL Assets] プロキシフレームワークに標準提供されているものではありません。
>
>[!DNL InDesign] 統合によって、[!DNL InDesign] Server のプール（IDSPool）にアクセスできるようになります。このプーリングは [!DNL InDesign] 統合に固有のものであり、[!DNL Assets] プロキシフレームワークの一部ではありません。

>[!NOTE]
>
>結果の同期：
>
>同じプロキシを使用するインスタンスが n 個ある場合、処理結果はプロキシに保持されます。クライアント（Experience Manager 作成者）の役目は、ジョブ作成時にクライアントに指定されるものと同じ一意のジョブ ID を使用して、結果をリクエストすることです。プロキシでは、単にジョブを実行し、リクエストに備えて結果を準備しておくだけです。
