---
title: AEM Forms のデプロイメントの監視
description: AEM Forms のデプロイメントは、システムレベルおよび内部レベルの両方で監視できます。このドキュメントでは、AEM Forms のデプロイメントの監視について説明します。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 931e8095-5c7c-4c1f-b95b-75ac2827d4f3
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 100%

---

# AEM Forms のデプロイメントの監視 {#monitoring-aem-forms-deployments}

AEM Forms のデプロイメントは、システムレベルおよび内部レベルの両方で監視できます。スペシャリスト管理ツール（HP OpenView、IBM® Tivoli、CA UniCenter およびサードパーティ JMX モニターである *JConsole* など）を使用することで、Java™ アクティビティを詳細に監視できます。監視方法の導入により、AEM Forms デプロイメントの可用性、信頼性およびパフォーマンスが向上します。

<!-- For more information about monitoring AEM forms deployments, see [A technical guide for monitoring AEM forms deployments](https://www.adobe.com/devnet/livecycle/pdfs/lc_monitoring_wp_ue.pdf). This URL is 404. No suitable replacement URL was found after a search. Do not make this link live if it is dead! -->

## MBean を使用した監視 {#monitoring-using-mbeans}

AEM Forms には、ナビゲーションおよび統計情報を提供する 2 つの MBean が登録されています。統合とインスペクションのためにサポートされている MBean はこれらのみです。

* **ServiceStatistic：**&#x200B;この MBean はサービス名とそのバージョンに関する情報を提供します。
* **OperationStatistic：**&#x200B;この MBean は AEM Forms サーバーのすべてのサービスに関する統計情報を提供します。この MBean で管理者は、呼び出し時間やエラー数など、特定のサービスに関する情報を取得できます。

### ServiceStatisticMbean 公開インターフェイス {#servicestatisticmbean-public-interfaces}

次の ServiceStatistic MBean の公開インターフェイスには、テスト目的でアクセスできます。

```java
 public String getServiceId();
 public int getMajorVersion();
 public int getMinorVersion();
```

### OperationStatisticMbean 公開インターフェイス {#operationstatisticmbean-public-interfaces}

次の OperationStatistic MBean の公開インターフェイスには、テスト目的でアクセスできます。

```java
 // InvocationCount: The number of times the method is invoked.
 public long getInvocationCount();
 // InvocationStartTime: The time at which the method started to execute.
 public long getInvocationStartTime();
 // InvocationEndTime: The time at which the method finished execution.
 public long getInvocationEndTime();
 // InvocationTime: The time taken for the execution of the method.
 public long getInvocationTime();
 // LastSamplingDateTime: Convert InvocationStartTime to a formatted string
 public String getLastSamplingDateTime();
 // MaxInvocationTime: The maximum time taken for the execution of the method.
 public long getMaxInvocationTime();
 // MinInvocationTime: The minimum time taken for the execution of the method.
 public long getMinInvocationTime();
 // AverageInvocationTime: the averege execution time taken for the execution of the method.
 public double getAverageInvocationTime();
 // ExceptionCount: The number of times the method has thrown an Exception.
 public long getExceptionCount();
 // ExceptionMessage: The message of the last exception occurred.
 public String getExeptionMessage();
 public void setExceptionMessage(String errorMessage);
```

### MBean ツリーおよび運用の統計情報 {#mbean-tree-operation-statistics}

JMX コンソール（JConsole）を使用すると、OperationStatistic MBean の統計情報を使用できます。この統計情報は MBean の属性です。次の階層ツリーで移動できます。

**MBean ツリー**

**アドビ ドメイン名：** アプリケーションサーバーに依存します。アプリケーションサーバーがドメインを定義していない場合、デフォルトは adobe.com です。

**ServiceType：** AdobeService は全サービスを表示するために使用される名前です。

**AdobeServiceName：**&#x200B;サービス名またはサービス ID。

**バージョン：**&#x200B;サービスのバージョン。

**運用の統計情報**

**呼び出し時間：**&#x200B;メソッドの実行にかかる時間。この呼び出しには、リクエストのシリアライズ、クライアントからサーバーへの転送およびデシリアライズにかかる時間は含まれません。

**呼び出し数：**&#x200B;サービスを呼び出した回数。

**平均呼び出し時間：**&#x200B;サーバーを起動した後に実行したすべての呼び出しにかかる平均時間。

**最大呼び出し時間：**&#x200B;サーバーを起動した後に実行した呼び出しのうち、最も長い呼び出し時間。

**最小呼び出し時間：**&#x200B;サーバーを起動した後に実行した呼び出しのうち、最も短い呼び出し時間。

**例外数：**&#x200B;エラーが発生した呼び出しの数。

**例外メッセージ：**&#x200B;発生した最後の例外のエラーメッセージ。

**最終サンプリング日時：**&#x200B;最後の呼び出しの日付。

**時間単位：** デフォルトはミリ秒です。

JMX 監視を有効にするには、通常、アプリケーションサーバーに何らかの設定が必要です。詳しくは、アプリケーションサーバーのドキュメントを参照してください。

### オープン JMX アクセスをセットアップする方法の例 {#examples-of-how-to-set-up-open-jmx-access}

**JBoss® 4.0.3/4.2.0 - JVM スタートアップの設定**

JConsole から MBean を表示するには、JBoss アプリケーションサーバーの JVM スタートアップパラメーターを設定する必要があります。JBoss は必ず run.bat／run.sh ファイルから起動します。

1. InstallJBoss/bin にある run.bat ファイルを編集します。
1. JAVA_OPTS 行を見つけ、次の内容を追加します。

   ```shell
    -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=9088 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false
   ```

**WebLogic 9.2／10 - JVM スタートアップの設定**

1. `[WebLogic home]/user_projects/domains/Adobe_Live_Cycle/bin` にある startWebLogic.bat ファイルを編集します。
1. JAVA_OPTS 行を見つけ、次の内容を追加します。

   ```shell
    -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=9088 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false
   ```

1. WebLogic を再起動します。

>[!NOTE]
>
>WebLogic の場合、リモートまたは IIOP を使用して MBean にアクセスできます。

**MBean へのリモートからのアクセス**

1. 新しい接続用に JConsole を起動し、リモートタブをクリックします。
1. ホスト名とポート（9088、JVM のスタートアップオプションで指定した番号）を入力します。

**Websphere® 6.1 - JVM スタートアップの設定**

1. Admin Console（アプリケーションサーバー／サーバー 1／プロセスの定義／JVM）で、Generic JVM Argument のフィールドに次の行を追加します。

   ```shell
    -Djavax.management.builder.initial= -Dcom.sun.management.jmxremote
   ```

1. /opt/IBM/WebSphere/AppServer/java/jre/lib/management/management.properties ファイル（または &lt;Your Websphere JRE>/ lib/management/management.properties）に次の 3 行を追加するか、コメントを解除します。

   ```shell
    com.sun.management.jmxremote.port=9999 //any port you like, but make sure you use this port when you connect
    com.sun.management.jmxremote.authenticate=false
    com.sun.management.jmxremote.ssl=false
   ```

1. WebSphere を再起動します。
