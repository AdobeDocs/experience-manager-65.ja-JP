---
title: タスクのタブのカスタマイズ
description: LiveCycle AEM Forms Workspace でタスクのタブ名をカスタマイズする方法について説明します。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 8412cfec-bcab-40b7-9e5b-fcc211d43c0b
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
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
