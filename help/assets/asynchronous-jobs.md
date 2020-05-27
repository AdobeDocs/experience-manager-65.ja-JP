---
title: 非同期操作
description: Experience Manager Assetsは、リソースを大量に消費する一部のタスクを非同期に完了することで、パフォーマンスを最適化します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 71%

---


# 非同期操作 {#asynchronous-operations}

Adobe Experience Manger Assetsでは、パフォーマンスへの悪影響を軽減するために、長時間かつリソースを大量に消費する特定のアセット操作を非同期的に処理します。

このような操作には以下のようなものがあります。

* 多数のアセットの削除
* 多数のアセットまたは多数の参照があるアセットの移動
* アセットメタデータの一括での書き出しまたは読み込み
* リモートのExperience Managerデプロイメントから、しきい値の制限を超えるアセットを取得しています。

非同期処理では複数のジョブがエンキューされ、システムリソースの可用性に応じた順序でジョブが実行されます。

非同期ジョブのステータスは、**[!UICONTROL 非同期ジョブステータス]**&#x200B;ページで確認できます。

>[!NOTE]
>
>デフォルトでは、 Assets でのジョブは並行して実行されます。N を CPU コアの数とすると、デフォルトでは N/2 のジョブを並行して実行できます。ジョブキューのカスタム設定を使用するには、Web コンソールで「**[!UICONTROL Async Operation Default Queue]**」設定を変更します。For more information, see [queue configurations](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#queue-configurations).

## Monitor the status of asynchronous operations {#monitoring-the-status-of-asynchronous-operations}

 Assets で非同期的に操作がおこなわれると、インボックスと電子メールに通知が届きます。

非同期操作のステータスの詳細を表示するには、**[!UICONTROL 非同期ジョブステータス]**&#x200B;ページに移動します。

1. Experience Managerインターフェイスで、 **[!UICONTROL 操作]** / **[!UICONTROL ジョブをクリックします]**。

1. **[!UICONTROL 非同期ジョブステータス]**&#x200B;ページで、操作の詳細をレビューします。

   ![非同期操作のステータスと詳細](assets/AsyncOperation-status.png)

   特定の操作の進行状況を確認するには、「**[!UICONTROL ステータス]**」列の値を参照します。進行状況に応じて、以下のいずれかのステータスが表示されます。

   * **[!UICONTROL アクティブ]**：操作は処理中です。

   * **[!UICONTROL 成功]**：操作は完了しました。

   * **[!UICONTROL 失敗]**&#x200B;または&#x200B;**[!UICONTROL エラー]**：操作を処理できませんでした。

   * **[!UICONTROL スケジュール済み]**：操作は後で処理するためにスケジュールされています。

1. To stop an active operation, select it from the list and click **[!UICONTROL Stop]** from the toolbar.

   ![stop_icon](assets/stop_icon.png)

1. To view extra details, for example description and logs, select the operation and click **[!UICONTROL Open]** from the toolbar.

   ![open_icon](assets/open_icon.png)

   ジョブの詳細ページが表示されます。

   ![job_details](assets/job_details.png)

1. リストから操作を削除するには、ツールバーの「**[!UICONTROL 削除]**」を選択します。To download the details in a CSV file, click **[!UICONTROL Download]**.

   >[!NOTE]
   >
   >ステータスがアクティブまたは待機中のジョブは削除できません。

## 完了したジョブの削除 {#purging-completed-jobs}

Experience Manager Assetsは毎日午前1時に削除ジョブを実行し、完了した非同期ジョブのうち1日以上経過しているジョブを削除します。

パージジョブのスケジュールと、完了済みジョブの詳細を削除するまでの保持期間を変更できます。また、任意の時点での詳細を保持する、完了済みジョブの最大数を設定することもできます。

1. Experience Managerインターフェイスで、 **[!UICONTROL ツール]** / **[!UICONTROL 操作]** / **[!UICONTROL Webコンソールをクリックします]**。
1. 「**[!UICONTROL Adobe CQ DAM Async Jobs Purge Scheduled]**」ジョブを開きます。
1. 完了済みジョブを削除するまでの日数のしきい値と、詳細を履歴に保持するジョブの最大数を指定します。

   ![非同期ジョブのパージをスケジュールするための設定](assets/configmgr_purge_asyncjobs.png)

1. 変更内容を保存します。

## Configure thresholds for asynchronous processing {#configuring-thresholds-for-asynchronous-processing}

 Assets が特定の操作を非同期的に処理する際の、アセットまたは参照の数のしきい値を設定できます。

### Configure thresholds for asynchronous delete operations {#configuring-thresholds-for-asynchronous-delete-operations}

削除するアセットまたはフォルダーの数がしきい値を超えると、削除操作が非同期的に実行されます。

1. Experience Managerインターフェイスで、 **[!UICONTROL ツール]** / **[!UICONTROL 操作]** / **[!UICONTROL Webコンソールをクリックします]**。
1. Web コンソールで、「**[!UICONTROL Async Delete Operation Job Processing]**」設定を開きます。
1. 「**[!UICONTROL Threshold number of assets]**」ボックスで、削除操作の非同期処理に関するアセットまたはフォルダー数のしきい値を指定します。

   ![delete_threshold](assets/delete_threshold.png)

1. 変更内容を保存します。

### Configure thresholds for asynchronous move operations {#configuring-thresholds-for-asynchronous-move-operations}

移動するアセットやフォルダーまたは参照の数がしきい値を超えると、移動操作が非同期的に実行されます。

1. Experience Managerインターフェイスで、 **[!UICONTROL ツール]** / **[!UICONTROL 操作]** / **[!UICONTROL Webコンソールをクリックします]**。
1. Web コンソールで、「**[!UICONTROL Async Move Operation Job Processing]**」設定を開きます。
1. 「**[!UICONTROL Threshold number of assets/references]**」ボックスで、移動操作の非同期処理に関するアセットやフォルダーまたは参照の数のしきい値を指定します。

   ![move_threshold](assets/move_threshold.png)

1. 変更内容を保存します。
