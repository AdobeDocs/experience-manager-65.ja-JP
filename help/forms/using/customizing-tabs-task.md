---
title: タスクのタブのカスタマイズ
seo-title: Customizing tabs for a task
description: LiveCycle AEM Forms Workspace でタスクのタブ名をカスタマイズする方法。
seo-description: How-to customize the names of the tabs for your tasks, in LiveCycle AEM Forms workspace.
uuid: 77eabb63-f8ea-4ec0-8a41-b51c65cdecc0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: ac0a281f-f589-4a70-9bc7-1a23e054b02f
exl-id: 8412cfec-bcab-40b7-9e5b-fcc211d43c0b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '101'
ht-degree: 100%

---

# タスクのタブのカスタマイズ {#customizing-tabs-for-a-task}

`Start Process` Uber ビューの `Start Process` コンポーネントと `ToDo` Uber ビューの `Task Details` コンポーネントのタブ名をカスタマイズできます。

1. 「[AEM Forms Workspace のカスタマイズの一般的な手順](/help/forms/using/generic-steps-html-workspace-customization.md)」に従います。
1. `translation.json` ファイルにある `tabname` の値を変更します。

   たとえば、英語の場合は `/apps/ws/locales/en-US/translation.json` を次のように変更します。

   * 開始プロセスで開始したタスクの場合は、`"startprocess" : {}` ブロックから次のスニペットを使用します。

   ```json
   "tabname" : {
               "form" : "Application",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Helper Notes"
           }
   ```

   * To-do のタスクの場合は、`"todo" : {}` ブロックから次のスニペットを使用します。

   ```json
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
