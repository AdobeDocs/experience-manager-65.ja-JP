---
title: タスクの詳細ページのカスタマイズ
description: AEM Forms Workspace のタスクの詳細ページをカスタマイズして、タスクに関して表示されるデフォルトの情報を変更する方法について説明します。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 48c24442-22d2-4d1a-9462-0aba78340281
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 100%
---
# タスクの詳細ページのカスタマイズ {#customizing-the-task-details-page}

タスクの詳細ページには、タスクおよびそのプロセスに関する情報が含まれています。 しかしながら、タスクの詳細ページをカスタマイズして情報を追加したり、削除したりすることができます。

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

   新しい情報を `/apps/ws/js/runtime/templates/taskdetails.html` に追加します。 次は例です。

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
