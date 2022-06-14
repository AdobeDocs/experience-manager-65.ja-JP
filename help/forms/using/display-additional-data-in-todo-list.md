---
title: TODO リストでの追加のデータの表示
seo-title: Displaying additional data in ToDo list
description: LiveCycle AEM Forms Workspace の TODO リストの表示をカスタマイズして、デフォルト以外の情報を表示する方法。
seo-description: How-to customize the display of the To-do list of LiveCycle AEM Forms workspace to show more information besides the default.
uuid: 9467c655-dce2-43ce-8e8f-54542fe81279
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: fed3b562-bcc2-4fb7-8fd2-35b1ac621e16
docset: aem65
exl-id: f8b84f13-02d3-4787-95e1-25fd684e6d3b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 100%

---

# TODO リストでの追加のデータの表示{#displaying-additional-data-in-todo-list}

デフォルトで、AEM Forms Workspace TODO リストにタスクの表示名および説明が表示されます。しかしながら、作成日や締切日などのその他の情報を追加することができます。また、アイコンを追加したり、表示のスタイルを変更することもできます。

![デフォルト設定を表示する HTML Workspace の「TODO」タブ](assets/html-todo-list.png)

この記事では、TODO リストの各タスクに情報を追加する手順について説明します。

## 追加できる情報 {#what-can-be-added}

サーバーによって送信された `task.json` にある情報を追加することができます。情報は、平文テキストとして追加することも、スタイルを使用して情報をフォーマットすることもできます。

JSON オブジェクトの説明についての詳細は、[この](/help/forms/using/html-workspace-json-object-description.md)記事を参照してください。

## タスクでの情報の表示 {#displaying-information-on-a-task}

1. 「[AEM Forms Workspace のカスタマイズの一般的な手順](../../forms/using/generic-steps-html-workspace-customization.md)」に従います。
1. タスクに追加の情報を表示するには、対応するキーと値のペアを `translation.json` のタスクブロック内に追加する必要があります。

   例えば、`/apps/ws/locales/en-US/translation.json` （英語）に変更します。

   ```json
   "task" : {
           "reminder" : {
               "value" : "Reminder",
               "tooltip" : "This is reminder __reminderCount__, for this task."
           },
           "deadlined" : {
               "value" : "Deadlined",
               "tooltip" : "This task has deadlined"
           },
           "save" : {
               "message" : "Task has been saved successfully"
           },
           "status" : {
               "deadlined" : "Deadlined",
               "created" : "Created",
               "assignedsaved" : "Draft from assigned task",
               "terminated" : "Terminated",
               "assigned" : "Assigned",
               "unknown" : "Unknown",
               "createdsaved" : "Draft from created task",
               "completed" : "Completed"
           },
           "draft" : {
               "value" : "Saved",
               "tooltip" : "This task is marked as a draft"
           },
           "escalated" : {
               "value" : "Escalated",
               "tooltip" : "This task has been escalated"
           },
           "forward" : {
               "value" : "Forwarded",
               "tooltip" : "This task was forwarded"
           },
           "priority" : {
               "highest" : "Highest priority",
               "normal" : "Normal priority",
               "high" : "High priority",
               "low" : "Low priority",
               "lowest" : "Lowest priority"
           },
           "claimed" : {
               "value" : "Claimed",
               "tooltip" : "This task has been claimed"
           },
           "locked" : {
               "value" : "Locked",
               "tooltip" : "This task is locked"
           },
           "consulted" : {
               "value" : "Consulted",
               "tooltip" : "This task has been consulted"
           },
           "returned" : {
               "value" : "Returned",
               "tooltip" : "This task was returned back"
           },
           "multiplesubmitbuttons" : {
               "message" : "The form associated with this task has multiple submit buttons so the Workspace Complete button will be disabled. Click the appropriate button on the form to submit it."
           },
           "nosubmitbutton" : {
               "message" : "The form associated with this task does not appear to have submit buttons. You may need to upgrade your Adobe Reader version to 9.1 or greater and enable the Reader Submit option in your process."
           },
           "icon" : {
               "tooltip" : "open the task __taskName__"
           }
       }
   ```

   >[!NOTE]
   >
   >対応するキーと値のペアをすべてのサポートされている言語に追加します。

1. たとえば、次のようにしてタスクブロック内に情報を追加します。

   ```json
   "stepname" : {
               "value" : "Step Name",
               "tooltip" : "This task belongs to __stepName__ step"
   }
   ```

## 新規プロパティでの CSS の定義 {#defining-css-for-the-new-property}

1. タスクに追加された情報（プロパティ）にスタイルを適用できます。これを行うには、`/apps/ws/css/newStyle.css` に追加された新規プロパティにスタイル情報を追加する必要があります。

   たとえば、以下を追加します。

   ```css
   .task .taskProperties .stepname{
       width: 25px;
       background: url(../images/stepname.png) no-repeat; /*-------- Or just reuse background image / image-sprite defined .task .taskProperties span of style.css---------------------*/
       background-position: 0px 0px; /*-------- Dummy values, need to be configured as per user background image / image-sprite ---------------------*/
   }
   ```

## HTML テンプレートへのエントリの追加 {#adding-entry-in-the-html-template}

最後に、タスクに追加する各プロパティの開発パッケージにエントリを含める必要があります。作成する方法については、「AEM Forms Workspace コードの構築」を参照してください。

1. `task.html` をコピーします：

   * コピー元：`/libs/ws/js/runtime/templates/`
   * コピー先：`/apps/ws/js/runtime/templates/`

1. 新しい情報を `/apps/ws/js/runtime/templates/task.html` に追加します。

   例えば、`div class="taskProperties"` の下に追加します。

   ```jsp
   <span class="stepname" alt="<%= $.t('task.stepname.value')%>" title = '<%= $.t("task.stepname.tooltip",{stepName:stepName})%>'/>
   ```
