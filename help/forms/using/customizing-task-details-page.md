---
title: タスクの詳細ページのカスタマイズ
seo-title: タスクの詳細ページのカスタマイズ
description: AEM Forms Workspace のタスクの詳細ページをカスタマイズして、タスクについて表示されるデフォルトの情報を変更する方法。
seo-description: AEM Forms Workspace のタスクの詳細ページをカスタマイズして、タスクについて表示されるデフォルトの情報を変更する方法。
uuid: d85fae55-8e66-4595-8560-5485622b6841
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 16e57cf6-aaa1-406d-a6ad-71ec60b15386
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 63%

---


# タスクの詳細ページのカスタマイズ{#customizing-the-task-details-page}

タスクの詳細ページには、タスクおよびそのプロセスに関する情報が含まれています。しかしながら、タスクの詳細ページをカスタマイズして情報を追加したり、削除したりすることができます。

次の情報をタスクの詳細ページに追加することができます。

* タスクの JSON オブジェクトで入手できる情報（[AEM Forms Workspace JSON オブジェクトの説明の「タスク」セクション](/help/forms/using/html-workspace-json-object-description.md)）
* プロセスインスタンスの JSON オブジェクトで入手できる情報（[AEM Forms Workspace JSON オブジェクトの説明の「プロセスインスタンス」セクション](/help/forms/using/html-workspace-json-object-description.md)）

タスクの詳細ページをカスタマイズするには：

1. [AEM Forms Workspace のカスタマイズの一般的な手順](/help/forms/using/generic-steps-html-workspace-customization.md)に従います。
1. 追加の情報を表示するには、対応するキーと値のペアを`translation.json`ファイル(`todo`block > `details`block > `app`block > [ block `required` a6/>)に追加します。]

   [ `required`block]は、タスク情報のタスクブロック、プロセス情報のプロセスブロック、保留中のタスク情報のcurrentpendingtaskブロックなど、使用可能なブロックを参照します。

   たとえば、タスクの詳細ページに必要なルート選択に関する情報を追加するには、以下のキーと値のペアを task ブロックに追加することができます。

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

   追加`/apps/ws/js/runtime/templates/taskdetails.html`に対する新しい情報。 次に例を示します。

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

   `text!/lc/libs/ws/js/runtime/templates/taskdetails.html`を検索して`text!/lc/apps/ws/js/runtime/templates/taskdetails.html`に置き換えます。

>[!NOTE]
>
>AEM Formsワークスペースの&#x200B;**開始プロセス**&#x200B;タブで作成されたタスクでタスクの詳細ページをカスタマイズするには、`/apps/ws/js/runtime/templates/startprocess.html`に新しい情報を追加します。
>
>詳細ページに追加された情報に新しいスタイルを追加するには、[Workspaceのカスタマイズ](changing-locale-user-interface.md)の&#x200B;*ユーザーインターフェイスの変更*&#x200B;セクションを使用してCSSファイルを変更します。
