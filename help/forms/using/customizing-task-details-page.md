---
title: タスクの詳細ページのカスタマイズ
description: AEM Forms Workspace のタスクの詳細ページをカスタマイズして、タスクに関して表示されるデフォルト情報を変更する方法。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 48c24442-22d2-4d1a-9462-0aba78340281
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 30%

---

# タスクの詳細ページのカスタマイズ {#customizing-the-task-details-page}

タスクの詳細ページには、タスクとそのプロセスに関する情報が含まれます。 ただし、タスクの詳細ページをカスタマイズして、情報を追加または削除できます。

次の情報をタスクの詳細ページに追加できます。

* タスクの JSON オブジェクトで使用できる情報 ( [AEM Forms Workspace JSON オブジェクトの説明](/help/forms/using/html-workspace-json-object-description.md))
* プロセスインスタンスの JSON オブジェクトに含まれる情報 ( [AEM Forms Workspace JSON オブジェクトの説明](/help/forms/using/html-workspace-json-object-description.md))

タスクの詳細ページをカスタマイズするには：

1. フォロー [AEM Forms Workspace のカスタマイズの一般的な手順です。](/help/forms/using/generic-steps-html-workspace-customization.md)
1. 追加情報を表示するには、対応するキーと値のペアを `translation.json` ～にファイルを送る `todo`ブロック > `details`ブロック > `app`ブロック > [`required`ブロック].

   The [`required`ブロック] は、タスク情報のタスクブロック、プロセス情報のプロセスブロック、保留中のタスク情報の現在の保留中のタスクブロックなど、使用可能なブロックを指します。

   たとえば、タスクの詳細ページで Route Selection Required に関する情報を追加するには、次のキーと値のペアを task ブロックに追加します。

   ```json
   "todo" : {
       .
       .
       .
       "details" : {
           .
           .
           "task" : {
               .
               .
               "RouteSelectionRequired" : "Route Selection Required"
           }
       }
   }
   ```

   >[!NOTE]
   >
   >対応するキーと値のペアを、サポートされるすべての言語に追加します。

1. `/libs/ws/js/runtime/templates/taskdetails.html` を `/apps/ws/js/runtime/templates/taskdetails.html` にコピーします。

   新しい情報を `/apps/ws/js/runtime/templates/taskdetails.html` に追加します。次は例です。

   ```css
   <div class="detailsContainer">
       .
       .
       <ul>
           .
           .
           <li>
               <label for="routeSelectionRequired" title="<%= $.t('todo.details.task.RouteSelectionRequired')%>"><%= $.t('todo.details.task.RouteSelectionRequired')%></label>
               <div>
                   <span id="routeSelectionRequired"><%= isRouteSelectionRequired != null ? isRouteSelectionRequired : ''%></span>
               </div>
           </li>
           .
           .
       </ul>
   </div>
   ```

1. /apps/ws/js/registry.js を開いて編集します。

   `text!/lc/libs/ws/js/runtime/templates/taskdetails.html` を検索して `text!/lc/apps/ws/js/runtime/templates/taskdetails.html` で置き換えます。

>[!NOTE]
>
>タスクの詳細ページを AEM Forms Workspace の「**プロセスの開始**」タブで作成したタスクでカスタマイズするには、新しい情報を `/apps/ws/js/runtime/templates/startprocess.html` に追加します。
>
>詳細ページで追加した情報に新しいスタイルを追加するには、[ワークスペースのカスタマイズ](changing-locale-user-interface.md)にある&#x200B;*ユーザーインターフェイスの変更*&#x200B;セクションを使用して CSS ファイルを変更してください。
