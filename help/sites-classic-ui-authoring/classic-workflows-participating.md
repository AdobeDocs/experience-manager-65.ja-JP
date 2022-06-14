---
title: 'ワークフローへの参加 '
seo-title: Participating in Workflows
description: ワークフローには通常、ページまたはアセットでユーザーがアクティビティを実行する必要があるステップが含まれています。ワークフローでアクティビティを実行するユーザーまたはグループを選択し、その人物やグループに作業項目を割り当てます。
seo-description: Workflows typically include steps that require a person to perform an activity on a page or asset. The workflow selects a user or group to perform the activity and assigns a work item to that person or group.
uuid: 04dcc8f2-dc11-430f-b0ae-47ef2cb069a2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 1d7a4889-82c5-4096-8567-8f66215a8458
exl-id: 2f1a3a73-7a20-48c7-8f3e-54252f5fb71c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 100%

---

# ワークフローへの参加 {#participating-in-workflows}

ワークフローには通常、ページまたはアセットでユーザーがアクティビティを実行する必要があるステップが含まれています。ワークフローでアクティビティを実行するユーザーまたはグループを選択し、その人物やグループに作業項目を割り当てます。

## 作業項目の処理 {#processing-your-work-items}

次のアクションを実行して作業項目を処理できます。

* **完了**

   項目を完了してワークフローを次のステップに進めることができます。

* **委任**

   ステップが割り当てられているが、何らかの理由によってアクションを実行できない場合、そのステップを別のユーザーまたはグループに委任できます。

   委任できるユーザーは、作業項目の割り当て先によって異なります。

   * 作業項目がグループに割り当てられた場合、グループメンバーに委任できます。
   * 作業項目がグループに割り当てられ、ユーザーに委任された場合、グループメンバーおよびグループに委任できます。
   * 作業項目が 1 人のユーザーに割り当てられた場合、作業項目を委任することはできません。

* **戻す**

   あるステップまたは一連のステップを繰り返す必要がある場合は、以前のステップに戻すことができます。これによって、ワークフロー内の以前に発生したステップを、再処理のために選択できます。ワークフローが指定したステップに戻り、そこから続行されます。

## ワークフローへの参加  {#participating-in-a-workflow}

### 割り当てられたワークフローアクションの通知 {#notifications-of-assigned-workflow-actions}

作業項目（**コンテンツを承認**&#x200B;など）が割り当てられると、様々なアラートや通知が表示されます。

* Web サイトコンソールの「**ステータス**」列は、ページがワークフローにあるときを示します。

   ![workflowstatus-1](assets/workflowstatus-1.png)

* ユーザーまたはユーザーが属するグループがワークフローの一部として作業項目に割り当てられていると、その作業項目が AEM ワークフローインボックスに表示されます。

   ![workflowinbox](assets/workflowinbox.png)

### 参加者ステップの完了 {#completing-a-participant-step}

指示されたアクションを実行すると、作業項目が完了します。これにより、ワークフローを続行できます。作業項目を完了するには、次の手順を使用します。

1. ワークフローステップを選択し、上部のナビゲーションバーの「**完了**」ボタンをクリックします。
1. 表示されたダイアログで、**次のステップ**（つまり、次に実行するステップ）を選択します。ドロップダウンリストには、すべての該当する移動先が示されます。**コメント**&#x200B;を入力することもできます。

   ![workflowcomplete](assets/workflowcomplete.png)

   列挙されるステップの数は、ワークフローモデルの設計によって異なります。

1. 「**OK**」をクリックして、アクションを確定します。

### 参加者ステップの委任 {#delegating-a-participant-step}

作業項目を委任するには、次の手順を使用します。

1. 上部のナビゲーションバーの「**委任**」ボタンをクリックします。
1. ダイアログで、ドロップダウンリストを使用して、作業項目を委任する「**ユーザー**」を選択します。「**コメント**」を追加することもできます。

   ![workflowdelegate](assets/workflowdelegate.png)

1. 「**OK**」をクリックして、アクションを確定します。

### 参加者ステップでの前のステップの実行 {#performing-step-back-on-a-participant-step}

前のステップを実行するには、次の手順を使用します。

1. 上部のナビゲーションバーの「戻す」ボタンをクリックします。
1. 表示されたダイアログで、「前のステップ」を選択します。つまり、次に実行するステップがワークフロー内の以前に発生したステップとなります。ドロップダウンリストには、すべての該当する移動先が示されます。

   ![screen_shot_2018-08-10at155325](assets/screen_shot_2018-08-10at155325.jpg)

1. 「OK」をクリックして、アクションを確定します。
