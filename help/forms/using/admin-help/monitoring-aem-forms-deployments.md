---
title: AEM Forms のデプロイメントの監視
seo-title: Monitoring AEM forms deployments
description: AEM forms のデプロイメントは、システムレベルと内部レベルの両方で監視できます。 このドキュメントでは、AEM forms のデプロイメントの監視について説明します。
seo-description: You can monitor AEM forms deployments from both a system level and an internal level. Learn more about monitoring AEM forms deployments from this document.
uuid: 032b7a93-3069-4ad5-a8c6-4c160f290669
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b3e7bca0-5aaf-4f28-bddb-fd7e8ed72ee8
exl-id: 931e8095-5c7c-4c1f-b95b-75ac2827d4f3
source-git-commit: c47b4dcfd2fbdcb0b98ad815f5b04d8f593e4f64
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 30%

---

# AEM Forms のデプロイメントの監視 {#monitoring-aem-forms-deployments}

AEM forms のデプロイメントは、システムレベルと内部レベルの両方で監視できます。 HP OpenView、IBM® Tivoli、CA UniCenter、および JMX と呼ばれるサード・パーティ製モニターなど、スペシャリスト管理ツールを使用できます。 *JConsole* を使用して、Java™アクティビティを特別に監視します。 監視戦略を実装すると、AEM Forms デプロイメントの可用性、信頼性、パフォーマンスが向上します。

<!-- For more information about monitoring AEM forms deployments, see [A technical guide for monitoring AEM forms deployments](https://www.adobe.com/devnet/livecycle/pdfs/lc_monitoring_wp_ue.pdf). This URL is 404. No suitable replacement URL was found after a search. Do not make this link live if it is dead! -->

## MBean を使用した監視 {#monitoring-using-mbeans}

AEM Formsには、ナビゲーションと統計の情報を提供する 2 つの登録済み MBean が用意されています。 次の部品は、統合と検査でサポートされる唯一の MBean です。

* **ServiceStatistic：**&#x200B;この MBean はサービス名とそのバージョンに関する情報を提供します。
* **OperationStatistic:** この MBean は、すべてのAEM Formsサーバーのサービスの統計を提供します。 この MBean では、管理者が呼び出し時間やエラー数など、特定のサービスに関する情報を取得できます。

### ServiceStatisticMbean パブリックインターフェイス {#servicestatisticmbean-public-interfaces}

ServiceStatistic MBean の次のパブリックインターフェイスには、テスト目的でアクセスできます。

```java
 public String getServiceId();
 public int getMajorVersion();
 public int getMinorVersion();
```

### OperationStatisticMbean パブリックインターフェイス {#operationstatisticmbean-public-interfaces}

OperationStatistic MBean の次のパブリックインターフェイスには、テスト目的でアクセスできます。

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

### MBean ツリーおよび操作の統計 {#mbean-tree-operation-statistics}

JMX コンソール (JConsole) を使用すると、OperationStatistic MBean の統計を使用できます。 これらの統計は MBean の属性で、次の階層ツリーの下で移動できます。

**MBean ツリー**

**アドビ ドメイン名：** アプリケーションサーバーに依存します。アプリケーションサーバーがドメインを定義していない場合、デフォルトは adobe.com です。

**ServiceType：** AdobeService は全サービスを表示するために使用される名前です。

**AdobeServiceName：**&#x200B;サービス名またはサービス ID。

**バージョン：**&#x200B;サービスのバージョン。

**運用の統計情報**

**呼び出し時間：**&#x200B;メソッドの実行にかかる時間。この呼び出しには、リクエストのシリアル化、クライアントからサーバーへの転送、シリアル化解除の時間は含まれません。

**呼び出し数：**&#x200B;サービスを呼び出した回数。

**平均呼び出し時間：**&#x200B;サーバーを起動した後に実行したすべての呼び出しにかかる平均時間。

**最大呼び出し時間：**&#x200B;サーバーを起動した後に実行した呼び出しのうち、最も長い呼び出し時間。

**最小呼び出し時間：**&#x200B;サーバーを起動した後に実行した呼び出しのうち、最も短い呼び出し時間。

**例外数：**&#x200B;エラーが発生した呼び出しの数。

**例外メッセージ：**&#x200B;発生した最後の例外のエラーメッセージ。

**最終サンプリング日時：**&#x200B;最後の呼び出しの日付。

**時間単位：** デフォルトはミリ秒です。

JMX 監視を有効にするには、通常、アプリケーションサーバーにいくつかの設定が必要です。 詳しくは、アプリケーションサーバーのドキュメントを参照してください。

### オープン JMX アクセスの設定方法の例 {#examples-of-how-to-set-up-open-jmx-access}

**JBoss® 4.0.3/4.2.0 - JVM スタートアップの設定**

JConsole から MBean を表示するには、JBoss アプリケーションサーバーの JVM 起動パラメーターを設定します。 JBoss が run.bat/sh ファイルから起動されていることを確認します。

1. InstallJBoss/bin にある run.bat ファイルを編集します。
1. JAVA_OPTS 行を検索し、次の行を追加します。

   ```shell
    -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=9088 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false
   ```

**WebLogic 9.2 /10 - JVM スタートアップの設定**

1. `[WebLogic home]/user_projects/domains/Adobe_Live_Cycle/bin` にある startWebLogic.bat ファイルを編集します。
1. JAVA_OPTS 行を検索し、次の行を追加します。

   ```shell
    -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.port=9088 -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false
   ```

1. WebLogic を再起動します。

>[!NOTE]
>
>WebLogic の場合は、リモートまたは IIOP を使用して MBean にアクセスできます。

**MBean へのリモートアクセス**

1. 新しい接続用に JConsole を起動し、リモートタブをクリックします。
1. ホスト名とポート（JVM の起動時に指定する番号 9088）を入力します。

**WebSphere® 6.1 - JVM スタートアップの設定**

1. Admin Console(Application server/server1/Process Definition/JVM) で、Generic JVM Argument のフィールドに次の行を追加します。

   ```shell
    -Djavax.management.builder.initial= -Dcom.sun.management.jmxremote
   ```

1. /opt/IBM/WebSphere/AppServer/java/jre/lib/management/management.propertiesファイルに次の 3 行を追加するか、コメントを解除します ( または &lt;your websphere=&quot;&quot; jre=&quot;&quot;>/ lib/management/management.properties):

   ```shell
    com.sun.management.jmxremote.port=9999 //any port you like, but make sure you use this port when you connect
    com.sun.management.jmxremote.authenticate=false
    com.sun.management.jmxremote.ssl=false
   ```

1. WebSphere を再起動します。
