---
title: タスクのタブのカスタマイズ
seo-title: タスクのタブのカスタマイズ
description: LiveCycle AEM Forms Workspace でタスクのタブ名をカスタマイズする方法。
seo-description: LiveCycle AEM Forms Workspace でタスクのタブ名をカスタマイズする方法。
uuid: 77eabb63-f8ea-4ec0-8a41-b51c65cdecc0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: ac0a281f-f589-4a70-9bc7-1a23e054b02f
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# タスクのタブのカスタマイズ {#customizing-tabs-for-a-task}

Uber表示のコンポーネントと `Start Process` Uber表示のコンポ `Start Process` ーネントのタブ名を `Task Details` カスタマイズ `ToDo` できます。

1. 「[AEM Forms Workspace のカスタマイズの一般的な手順](/help/forms/using/generic-steps-html-workspace-customization.md)」に従います。
1. Change the value of `tabname`in the `translation.json` file.

   For example, change `/apps/ws/locales/en-US/translation.json` for English to the following.

   * For tasks initiated in the start process, use the following snippet from the `"startprocess" : {}` block.

   ```
   "tabname" : {
               "form" : "Application",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Helper Notes"
           }
   ```

   * For tasks in To-do, use the following snippet from the `"todo" : {}` block.

   ```
   "tabname" : {
               "summary" : "Bird's-eye view",
               "history" : "Past",
               "form" : "Form",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Notes"
   }
   ```

   >[!NOTE]
   >
   >対応するキーと値のペアをすべてのサポートされている言語に追加します。
