---
title: ワークフローインスタンスの管理
seo-title: Administering Workflow Instances
description: ワークフローインスタンスの管理方法について説明します。
seo-description: Lear how to administer Workflow Instances.
uuid: 81e53ef5-fe62-4ed4-b2d4-132aa986d5aa
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: d9c96e7f-9416-48e1-a6af-47384f7bee92
exl-id: 90923d39-3ac5-4028-976c-d011f0404476
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 96%

---

# ワークフローインスタンスの管理{#administering-workflow-instances}

ワークフローコンソールには、ワークフローインスタンスを管理し、それらが想定どおりに実行されていることを確認するための複数のツールが用意されています。

>[!NOTE]
>
>[JMX コンソール](/help/sites-administering/jmx-console.md#workflow-maintenance)を使用すると、追加のワークフローメンテナンス操作を行うことができます。

ワークフローの管理用に、次の各種コンソールが用意されています。[グローバルナビゲーション](/help/sites-authoring/basic-handling.md#global-navigation)を使用して&#x200B;**ツール**&#x200B;パネルを開き、その後「**ワークフロー**」を選択します。

* **モデル**：ワークフロー定義を管理します
* **インスタンス**：実行中のワークフローインスタンスを表示および管理します
* **ランチャー**：ワークフローの起動方法を確認します
* **アーカイブ**：正常に完了したワークフローの履歴を表示します
* **エラー**：エラーで終了したワークフローの履歴を表示します
* **自動割り当て**：テンプレートへの自動割り当てワークフローを設定します

## ワークフローインスタンスのステータスの監視 {#monitoring-the-status-of-workflow-instances}

1. ナビゲーションを使用して、**ツール**／**ワークフロー**&#x200B;を選択します。
1. 「**インスタンス**」を選択して現在進行中のワークフローインスタンスのリストを表示します。

   ![wf-96](assets/wf-96.png)

<!--
## Search Workflow Instances {#search-workflow-instances}

1. Using Navigation select **Tools**, then **Workflow**.
1. Select **Instances** to display the list of workflow instances currently in progress. On the top rail, in the left corner, select **Filters**. Alternatively, you can use the keystrokes alt+1. The following dialog is displayed:

   ![wf-99-1](assets/wf-99-1.png)

1. In the Filter dialog, select the workflow search criteria. You can search based on these inputs:

   * Payload path: Select a specific path
   * Workflow model: Select a workflow model
   * Assignee: Select a workflow Assignee
   * Type: Task, Workflow item, or Workflow Failure
   * Task Status: Active, Complete, or Terminated
   * Where I Am: Owner AND Assignee, Owner only, Assignee only
   * Start Date: Start date before or after a specified date
   * End Date: End date before or after a specified date
   * Due Date: Due date before or after a specified date
   * Updated Date: Updated date before or after a specified date
-->

## ワークフローインスタンスの休止、再開および終了 {#suspending-resuming-and-terminating-a-workflow-instance}

1. ナビゲーションを使用して、**ツール**／**ワークフロー**&#x200B;を選択します。
1. 「**インスタンス**」を選択して現在進行中のワークフローインスタンスのリストを表示します。

   ![wf-96-1](assets/wf-96-1.png)

1. 特定の項目を選択してから、適宜「**終了**」、「**休止**」、または「**再開**」を使用します。この際、確認または詳細（あるいはその両方）を求められます。

   ![wf-97-1](assets/wf-97-1.png)

## アーカイブされたワークフローの表示 {#viewing-archived-workflows}

1. ナビゲーションを使用して、**ツール**／**ワークフロー**&#x200B;を選択します。
1. 「**アーカイブ**」を選択して正常に完了したワークフローインスタンスのリストを表示します。

   ![wf-98](assets/wf-98.png)

   >[!NOTE]
   >
   >中止ステータスはユーザーアクションの結果として発生するので、正常終了と見なされます。例えば、次のような場合が当てはまります。
   >
   >* 「**終了**」アクションが使用された場合
   >* ワークフローの対象となるページが（強制的に）削除されたことによって、ワークフローが終了した場合

1. 特定の項目を選択し、「**履歴を開く**」で詳細を確認します。

   ![wf-99](assets/wf-99.png)

## ワークフローインスタンスのエラーの修正 {#fixing-workflow-instance-failures}

ワークフローが失敗した場合、AEMは **失敗** コンソールを使用して、原因が処理された後に調査し、適切なアクションを取ることができます。

* **失敗の詳細**
ウィンドウを開き、 **失敗メッセージ**, **手順**、および **エラースタック**.

* **履歴を開く**&#x200B;ワークフローの履歴の詳細を表示します。

* **ステップを再試行**&#x200B;スクリプトステップコンポーネントのインスタンスをもう一度実行します。発生したエラーの原因を修正した後に「ステップを再試行」コマンドを使用します。例えば、プロセスステップが実行するスクリプトのバグを修正した後にステップを再試行します。
* **終了**&#x200B;エラーが原因で解決できない問題がワークフローに発生した場合にワークフローを終了します。例は、環境条件（リポジトリー内の情報がワークフローインスタンスで無効になったなど）にワークフローが依存している可能性がある場合です。
* **終了して再試行**&#x200B;元のペイロード、タイトルおよび説明を使用して新しいワークフローインスタンスが開始される点を除き、**終了**&#x200B;と同様です。

エラーを調査し、その後ワークフローを再開または停止するには、次のステップに従います。

1. ナビゲーションを使用して、**ツール**／**ワークフロー**&#x200B;を選択します。
1. 「**エラー**」を選択して正常に完了しなかったワークフローインスタンスのリストを表示します。
1. 特定の項目を選択し、その後適切なアクションを選択します。

   ![wf-47](assets/wf-47.png)

## ワークフローインスタンスの定期的なパージ {#regular-purging-of-workflow-instances}

ワークフローインスタンスの数を最小限に抑えるとワークフローエンジンのパフォーマンスが向上します。このため、完了したまたは実行中のワークフローインスタンスをリポジトリーから定期的に削除できます。

有効期間とステータスに応じてワークフローインスタンスをパージするように **Adobe Granite のワークフローのパージ設定**&#x200B;を設定します。また、すべてのモデルまたは特定のモデルのワークフローインスタンスをパージすることもできます。

また、様々な条件を満たすワークフローインスタンスをパージするために、サービスの設定を複数作成することもできます。例えば、予想していた時間よりも大幅に実行時間の長い特定のワークフローモデルのインスタンスをパージする設定を作成します。さらに、リポジトリーのサイズを最小限に抑えるために、特定の日数が経過した後に完了したワークフローをすべてパージするもう 1 つの設定を作成します。

 サービスを設定するには、[Web コンソール](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)を使用するか、[リポジトリに OSGi 設定を追加](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)します。次の表では、どちらの方法でも必要になるプロパティについて説明しています。

>[!NOTE]
>
>リポジトリーに設定を追加する場合のサービス PID は次のとおりです。
>
>`com.adobe.granite.workflow.purge.Scheduler`
>
>このサービスはファクトリサービスなので、`sling:OsgiConfig` ノードの名前には次のような ID サフィックスが必要です。
>
>`com.adobe.granite.workflow.purge.Scheduler-myidentifier`

<table>
 <tbody>
  <tr>
   <th>プロパティ名（web コンソール）</th>
   <th>OSGi のプロパティ名</th>
   <th>説明</th>
  </tr>
  <tr>
   <td>ジョブ名</td>
   <td>scheduledpurge.name</td>
   <td>スケジュール設定されたパージのわかりやすい名前。</td>
  </tr>
  <tr>
   <td>ワークフローのステータス</td>
   <td>scheduledpurge.workflowStatus</td>
   <td><p>パージするワークフローインスタンスのステータス。次の値を指定できます。</p>
    <ul>
     <li>COMPLETED：完了したワークフローインスタンスがパージされます。</li>
     <li>RUNNING：実行中のワークフローインスタンスがパージされます。</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Models To Purge</td>
   <td>scheduledpurge.modelIds</td>
   <td><p>パージするワークフローモデルの ID。この ID は model ノードのパスです（例：<br /> /var/workflow/models/dam/update_asset<br />）。 </p> <p>複数のモデルを指定するには、web コンソールの「 +」ボタンをクリックします。 </p> <p>すべてのワークフローモデルのインスタンスをパージする値を指定しないでください。</p> </td>
  </tr>
  <tr>
   <td>Workflow Age</td>
   <td>scheduledpurge.daysold</td>
   <td>パージするワークフローインスタンスの有効期間（日数）。</td>
  </tr>
 </tbody>
</table>

## インボックスの最大サイズの設定 {#setting-the-maximum-size-of-the-inbox}

インボックスの最大サイズは、[Web コンソール](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)を使用して **Adobe Granite Workflow Service** を設定する、または[リポジトリに OSGi 設定を追加](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)することで設定できます。次の表では、どちらの方法でも設定するプロパティについて説明しています。

>[!NOTE]
>
>リポジトリーに設定を追加する場合のサービス PID は次のとおりです。
>
>`com.adobe.granite.workflow.core.WorkflowSessionFactory`。

| プロパティ名（web コンソール） | OSGi のプロパティ名 |
|---|---|
| Max Inbox Query Size | granite.workflow.inboxQuerySize |

## 顧客所有のデータストアに対するワークフロー変数の使用 {#using-workflow-variables-customer-datastore}

ワークフローで処理されたデータは、アドビ提供のストレージ（JCR）に保存されます。このデータは、本来、機密性が高い可能性があります。ユーザー定義のメタデータ／データをすべて、アドビ提供のストレージではなく、ユーザー管理のストレージに保存することができます。以下の節では、これらの変数を外部ストレージ用に設定する方法について説明します。

### メタデータの外部ストレージを使用するようにモデルの設定 {#set-model-for-external-storage}

ワークフローモデルのレベルでは、モデル（およびそのランタイムインスタンス）にメタデータの外部ストレージが含まれていることを示すフラグが用意されています。外部ストレージ用にマークされたモデルのワークフローインスタンスに対するワークフロー変数は JCR に保持されません。

*userMetadataPersistenceEnabled* プロパティがワークフローモデルの *jcr:content* ノードに格納されます。このフラグは、ワークフローメタデータに *cq:userMetaDataCustomPersistenceEnabled* として保持されます。

以下の図は、ワークフローにフラグを設定する方法を示しています。

![workflow-externalize-config](assets/workflow-externalize-config.png)

### 外部ストレージ内のメタデータの API {#apis-for-metadata-external-storage}

変数を外部に保存するには、ワークフローで公開している API を実装する必要があります。

UserMetaDataPersistenceContext

次のサンプルは、API の使用方法を示しています。

```
@ProviderType
public interface UserMetaDataPersistenceContext {
 
    /**
     * Gets the workflow for persistence
     * @return workflow
     */
    Workflow getWorkflow();
 
    /**
     * Gets the workflow id for persistence
     * @return workflowId
     */
    String getWorkflowId();
 
    /**
     * Gets the user metadata persistence id
     * @return userDataId
     */
    String getUserDataId();
}
```

UserMetaDataPersistenceProvider

```
/**
 * This provider can be implemented to store the user defined workflow-data metadata in a custom storage location
 */
@ConsumerType
public interface UserMetaDataPersistenceProvider {
 
   /**
    * Retrieves the metadata using a unique identifier
    * @param userMetaDataPersistenceContext
    * @param metaDataMap of user defined workflow data metaData
    * @throws WorkflowException
    */
   void get(UserMetaDataPersistenceContext userMetaDataPersistenceContext, MetaDataMap metaDataMap) throws WorkflowException;
 
   /**
    * Stores the given metadata to the custom storage location
    * @param userMetaDataPersistenceContext
    * @param metaDataMap metadata map
    * @return the unique identifier that can be used to retrieve metadata. If null is returned, then workflowId is used.
    * @throws WorkflowException
    */
   String put(UserMetaDataPersistenceContext userMetaDataPersistenceContext, MetaDataMap metaDataMap) throws WorkflowException;
} 
```
