---
title: 追跡テーブルのカスタマイズ
seo-title: 追跡テーブルのカスタマイズ
description: AEM Forms Workspace の「追跡」タブに表示されるタスクテーブルのユーザープロセスの詳細表示をカスタマイズする方法。
seo-description: AEM Forms Workspace の「追跡」タブに表示されるタスクテーブルのユーザープロセスの詳細表示をカスタマイズする方法。
uuid: 13d6ebf2-99d5-434f-85f9-b0cba5f5751a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: bb7a6e9f-4f28-4d97-8a0c-949259fd6857
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 追跡テーブルのカスタマイズ{#customize-tracking-tables}

AEM Forms Workspaceの「追跡」タブは、ログインユーザーが関与するプロセスインスタンスの詳細を表示するために使用されます。 追跡テーブルを表示するには、最初に左ペインでプロセス名を選択して中央ペインでインスタンスのリストを表示します。プロセスインスタンスを選択すると、このインスタンスによって生成されたタスクのテーブルが右ペインに表示されます。デフォルトで、テーブル列に以下のタスク属性が表示されます（タスクモデルの対応する属性は括弧内に表示）。

* ID ( `taskId`)
* 名前 ( `stepName`)
* 説明 ( `instructions`)
* 選択されたアクション ( `selectedRoute`)
* 作成時刻( `createTime`)
* 完了時間( `completeTime`)
* 所有者 ( `currentAssignment.queueOwner`)

タスクテーブルに表示できるタスクモデルの残りの属性を以下に示します。

<table>
 <tbody>
  <tr>
   <td><p>actionInstanceId</p> </td>
   <td><p>isOpenFullScreen</p> </td>
   <td><p>reminderCount</p> </td>
  </tr>
  <tr>
   <td><p>classOfTask</p> </td>
   <td><p>isOwner</p> </td>
   <td><p>routeList</p> </td>
  </tr>
  <tr>
   <td><p>consultGroupId</p> </td>
   <td><p>isRouteSelectionRequired</p> </td>
   <td><p>savedFormCount</p> </td>
  </tr>
  <tr>
   <td><p>contentType</p> </td>
   <td><p>isShowAttachments</p> </td>
   <td><p>serializedImageTicket</p> </td>
  </tr>
  <tr>
   <td><p>createTime</p> </td>
   <td><p>isStartTask</p> </td>
   <td><p>serviceName</p> </td>
  </tr>
  <tr>
   <td><p>creationId</p> </td>
   <td><p>isVisible</p> </td>
   <td><p>serviceTitle</p> </td>
  </tr>
  <tr>
   <td><p>currentAssignment</p> </td>
   <td><p>nextReminder</p> </td>
   <td><p>showACLActions</p> </td>
  </tr>
  <tr>
   <td><p>deadline</p> </td>
   <td><p>numForms</p> </td>
   <td><p>showDirectActions</p> </td>
  </tr>
  <tr>
   <td><p>description</p> </td>
   <td><p>numFormsToBeSaved</p> </td>
   <td><p>status</p> </td>
  </tr>
  <tr>
   <td><p>displayName</p> </td>
   <td><p>outOfOfficeUserId</p> </td>
   <td><p>summaryUrl</p> </td>
  </tr>
  <tr>
   <td><p>forwardGroupId</p> </td>
   <td><p>outOfOfficeUserName</p> </td>
   <td><p>supportsSave</p> </td>
  </tr>
  <tr>
   <td><p>isApprovalUI</p> </td>
   <td><p>priority</p> </td>
   <td><p>taskACL</p> </td>
  </tr>
  <tr>
   <td><p>isCustomUI</p> </td>
   <td><p>processInstanceId</p> </td>
   <td><p>taskFormType</p> </td>
  </tr>
  <tr>
   <td><p>isDefaultImage</p> </td>
   <td><p>processInstanceStatus</p> </td>
   <td><p>taskUserInfo</p> </td>
  </tr>
  <tr>
   <td><p>isLocked</p> </td>
   <td><p>processVariables</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p>isMustOpenToComplete</p> </td>
   <td><p>readerSubmitOptions</p> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

以下のタスクテーブルのカスタマイズの場合は、ソースコードでセマンティックの変更を行う必要があります。See [Introduction to Customizing AEM Forms workspace](/help/forms/using/introduction-customizing-html-workspace.md) fo how you can make semantic changes using workspace SDK and build a minified package from the changed source.

## テーブル列と順序の変更 {#changing-table-columns-and-their-order}

1. テーブルに表示されたタスク属性とそれらの順序を変更するには、ファイル /ws/js/runtime/templates/processinstancehistory.html を設定します。

   ```as3
   <table>
       <thead>
           <tr>
               <!-- put the column headings in order here, for example-->
               <th><%= $.t('history.fixedTaskTableHeader.taskName')%></th>
               <th><%= $.t('history.fixedTaskTableHeader.taskInstructions')%></th>
               <th><%= $.t('history.fixedTaskTableHeader.taskRoute')%></th>
               <th><%= $.t('history.fixedTaskTableHeader.taskCreateTime')%></th>
               <th><%= $.t('history.fixedTaskTableHeader.taskCompleteTime')%></th>
           </tr>
       </thead>
   </table>
   ```

   ```as3
   <table>
       <tbody>
           <%_.each(obj, function(task){%>
           <tr>
               <!-- Put the task attributes in the order of headings, for example -->
               <td><%= task.stepName %></td>
               <td><%= task.instructions %></td>
               <td><%= !task.selectedRoute?'':(task.selectedRoute=='null'?'Default':task.selectedRoute) %></td>
               <td><%= task.createTime?task.formattedCreateTime:'' %></td>
               <td><%= task.completeTime? task.formattedCompleteTime:'' %></td>
           </tr>
           <%});%>
       </tbody>
   </table>
   ```

## 追跡テーブルの並べ替え {#sorting-a-tracking-table}

列の見出しをクリックするときにタスクリストテーブルを並べ替えるには：

1. Register a click handler for `.fixedTaskTableHeader th` in the file `js/runtime/views/processinstancehistory.js`.

   ```as3
   events: {
       //other handlers
       "click .fixedTaskTableHeader th": "onTaskTableHeaderClick",
       //other handlers
   }
   ```

   In the handler, invoke the `onTaskTableHeaderClick` function of `js/runtime/util/history.js`.

   ```as3
   onTaskTableHeaderClick: function (event) {
           history.onTaskTableHeaderClick(event);
   }
   ```

1. メソッドを `TaskTableHeaderClick` に公開しま `js/runtime/util/history.js`す。

   メソッドはクリックイベントからタスク属性を検索し、その属性のタスクリストを並べ替えて、並べ替えられたタスクリストでタスクテーブルをレンダリングします。

   並べ替えは、比較関数を指定することによって、タスクリストコレクションの Backbone 並べ替え関数を使用して行われます。

   ```as3
       return {
           //other methods
           onTaskTableHeaderClick  : onTaskTableHeaderClick,
           //other methods
       };
   ```

   ```as3
   onTaskTableHeaderClick = function (event) {
           var target = $(event.target),
            comparator,
               attribute;
           if(target.hasClass('taskName')){
            attribute = 'stepName';
           } else if(target.hasClass('taskInstructions')){
               attribute = 'instructions';
           } else if(target.hasClass('taskRoute')){
               attribute = 'selectedRoute';
           } else if(target.hasClass('taskCreateTime')){
               attribute = 'createTime';
           } else if(target.hasClass('taskCompleteTime')){
               attribute = 'completeTime';
           }
           taskList.comparator = function (task) {
            return task.get(attribute);
           };
           taskList.sort();
           render();
       };
   ```
