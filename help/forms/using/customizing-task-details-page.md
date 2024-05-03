---
title: タスクの詳細ページのカスタマイズ
description: AEM Forms Workspace のタスクの詳細ページをカスタマイズして、タスクに関して表示されるデフォルトの情報を変更する方法について説明します。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 48c24442-22d2-4d1a-9462-0aba78340281
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 100%

---

# タスクの詳細ページのカスタマイズ {#customizing-the-task-details-page}

タスクの詳細ページには、タスクおよびそのプロセスに関する情報が含まれています。しかしながら、タスクの詳細ページをカスタマイズして情報を追加したり、削除したりすることができます。

次の情報をタスクの詳細ページに追加することができます。

* タスクの JSON オブジェクトで入手できる情報（[AEM Forms Workspace JSON オブジェクトの説明](/help/forms/using/html-workspace-json-object-description.md)のタスクの節）
* プロセスインスタンスの JSON オブジェクトで入手できる情報（[AEM Forms Workspace JSON オブジェクトの説明](/help/forms/using/html-workspace-json-object-description.md)のプロセスインスタンスの節）

タスクの詳細ページをカスタマイズするには：

1. [AEM Forms Workspace のカスタマイズの一般的な手順](/help/forms/using/generic-steps-html-workspace-customization.md)に従います。
1. 追加の情報を表示するには、対応するキーと値のペアを `todo` ブロック／`details` ブロック／`app` ブロック／[`required` ブロック] にある `translation.json` ファイルに追加してください。

   [`required` ブロック] は、タスク情報の task ブロック、プロセス情報の process ブロック、および保留中のタスク情報の currentpendingtask ブロックなど、使用可能なブロックを指します。

   例えば、タスクの詳細ページに必要なルート選択に関する情報を追加するには、以下のキーと値のペアを task ブロックに追加することができます。

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
   >対応するキーと値のペアをすべてのサポートされている言語に追加します。

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
