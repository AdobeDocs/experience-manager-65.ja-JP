---
title: フォルダーのアセットとコレクションのレビュー
description: フォルダーまたはコレクション内のアセットに対してレビューワークフローを設定し、それをレビュー担当者またはクリエイティブパートナーと共有してフィードバックを得ることができます。
contentOwner: AG
translation-type: tm+mt
source-git-commit: e71b87b12d45bf12f29af917fddebeddedb18056

---


# フォルダーのアセットとコレクションのレビュー {#review-folder-assets-and-collections}

フォルダーまたはコレクション内のアセットに対してレビューワークフローを設定し、それをレビュー担当者またはクリエイティブパートナーと共有してフィードバックを得ることができます。

Adobe Experience Manager（AEM）Assets では、フォルダーまたはコレクション内のアセットに対してアドホックレビューワークフローを設定し、それをレビュー担当者またはクリエイティブパートナーと共有してフィードバックを得ることができます。

レビューワークフローをプロジェクトと関連付けることも、独立したレビュータスクを作成することもできます。

ユーザーがアセットを共有した後で、レビュー担当者がアセットを承認または拒否できます。ワークフローの様々なステージで、様々なタスクの完了に関する通知が対象の受信者に送られます。例えば、ユーザーがフォルダーまたはコレクションを共有すると、レビュー担当者は、フォルダーまたはコレクションがレビューのために共有されたという通知を受け取ります。

レビュー担当者がレビューを終了（アセットを承認または拒否）すると、ユーザーはレビューが完了したという通知を受け取ります。

## Create a review task for folders {#creating-a-review-task-for-folders}

1. Assets ユーザーインターフェイスで、レビュータスクを作成するフォルダーを選択します。
1. From the toolbar, tap **[!UICONTROL Create Review Task]** to open the **[!UICONTROL Review Task]** page. If you cannot see the option in the toolbar, tap/click **[!UICONTROL More]** and then select the option.

   ![chlimage_1-403](assets/chlimage_1-403.png)

1. (Optional) From the **[!UICONTROL Project]** list, select the project to which you want to associate the review task. By default, the **[!UICONTROL None]** option is selected. If you do not want to associate any project with the review task, retain this selection.

   >[!NOTE]
   >
   >エディターレベルの権限（またはそれ以上）のあるプロジェクトのみが「**[!UICONTROL プロジェクト]**」リストに表示されます。

1. レビュータスクの名前を入力し、「**[!UICONTROL 割り当て先]**」リストから承認者を選択します。

   >[!NOTE]
   >
   >選択されたプロジェクトのメンバーまたはグループが、承認者として「**[!UICONTROL 割り当て先]**」リストに表示されます。

1. レビュータスクの説明、タスクの優先順位および期限を入力します。

   ![task_details](assets/task_details.png)

1. 「詳細」タブで、URI の作成に使用されるラベルを入力します。

   ![review_name](assets/review_name.png)

1. 「**[!UICONTROL 送信]**」、「**[!UICONTROL 完了]**」の順にタップまたはクリックし、確認メッセージを閉じます。新しいタスクに関する通知が承認者に送信されます。
1. 承認者として AEM Assets にログインし、Assets UI に移動します。To approve assets, tap **[!UICONTROL Notifications]** and then select the review task from the list.

   ![アセットの通知](assets/aemAssetsNotification.png)

1. **[!UICONTROL レビュータスク]**&#x200B;ページでレビュータスクの詳細を確認し、「**[!UICONTROL レビュー]**」をタップまたはクリックします。
1. In the **[!UICONTROL Review Task]** page, select assets, and tap **[!UICONTROL Approve/Reject]** to approve or reject, as appropriate.

   ![review_task](assets/review_task.png)

1. ツールバー **[!UICONTROL から]** 「完了」をタップします。 In the dialog, enter a comment and tap/click  **[!UICONTROL Complete]** to confirm.
1. アセットユーザーインターフェイスに移動し、フォルダを開きます。 アセットの承認ステータスアイコンが、カード表示とリスト表示に表示されます。

   **カード表示**

   ![カード表示でのステータスの確認](assets/chlimage_1-404.png)

   **リスト表示**

   ![リスト表示でのステータスの確認](assets/review_status_listview.png)

## Create a review task for collections {#creating-a-review-task-for-collections}

1. コレクションページで、レビュータスクを作成するコレクションを選択します。
1. From the toolbar, tap **[!UICONTROL Create Review Task]** to open the **[!UICONTROL Review Task]** page. If you cannot see the option on the toolbar, tap **[!UICONTROL More]** and then select the option.

   ![chlimage_1-405](assets/chlimage_1-405.png)

1. (Optional) From the **[!UICONTROL Project]** list, select the project to which you want to associate the review task. By default, the **[!UICONTROL None]** option is selected. If you do not want to associate any project with the review task, retain this selection.

   >[!NOTE]
   >
   >エディターレベルの権限（またはそれ以上）のあるプロジェクトのみが「**[!UICONTROL プロジェクト]**」リストに表示されます。

1. レビュータスクの名前を入力し、「**[!UICONTROL 割り当て先]**」リストから承認者を選択します。

   >[!NOTE]
   >
   >選択されたプロジェクトのメンバーまたはグループが、承認者として「**[!UICONTROL 割り当て先]**」リストに表示されます。

1. レビュータスクの説明、タスクの優先順位および期限を入力します。

   ![task_details-collection](assets/task_details-collection.png)

1. 「**[!UICONTROL 送信]**」、「**[!UICONTROL 完了]**」の順にタップまたはクリックし、確認メッセージを閉じます。新しいタスクに関する通知が承認者に送信されます。
1. 承認者として AEM Assets にログインし、アセットコンソールに移動します。To approve assets, tap **[!UICONTROL Notifications]** and then select the review task from the list.
1. **[!UICONTROL レビュータスク]**&#x200B;ページでレビュータスクの詳細を確認し、「**[!UICONTROL レビュー]**」をタップまたはクリックします。
1. コレクションのすべてのアセットがレビューページに表示されます。Select the assets and tap **[!UICONTROL Approve/Reject]** to approve or reject assets, as appropriate.

   ![review_task_collection](assets/review_task_collection.png)

1. ツールバー **[!UICONTROL から]** 「完了」をタップします。 In the dialog, enter a comment and tap/click **[!UICONTROL Complete]** to confirm.
1. コレクションコンソールに移動して、コレクションを開きます。アセットの承認ステータスアイコンは、カード表示とリスト表示の両方に表示されます。

   ![collection_reviewstatuscardview](assets/collection_reviewstatuscardview.png)

   *図：カード表示*

   ![collection_reviewstatuslistview](assets/collection_reviewstatuslistview.png)

   *図：リスト表示*
