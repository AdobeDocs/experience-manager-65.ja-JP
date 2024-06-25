---
title: AEM Forms ワークスペースで使用する API
description: カスタマイズと自動化のために開示された、公開 Java&trade; API、JavaScript API、および LiveCycle AEM Forms ワークスペースのメソッド。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 9034f73a-83f3-498e-b6a6-ad6577aa1a3a
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1059'
ht-degree: 100%

---

# AEM Forms ワークスペースで使用する API {#apis-used-in-aem-forms-workspace}

AEM Forms ワークスペースでは次の API が使用されています。

<table>
 <tbody>
  <tr>
   <td><strong>JavaScript メソッド</strong></td>
   <td><strong>サービス名</strong></td>
   <td><strong>API 名</strong></td>
   <td><strong>コメント</strong></td>
  </tr>
  <tr>
   <td>getGroups</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getGroups</td>
   <td>グループを検索します。何も指定しない場合はすべてのグループのリストを返します。名前を指定した場合はそれらのグループを返します。</td>
  </tr>
  <tr>
   <td>getUsersAndGroups</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getUsersAndGroups</td>
   <td>ユーザーおよびグループを検索します。何も指定しない場合はすべてのユーザーとグループのリストを返します。名前を指定した場合はそれらのユーザーとグループを返します。</td>
  </tr>
  <tr>
   <td>prepareForSubmit</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>prepareForSubmit</td>
   <td>フォームを DocumentSubmitServlet で送信する前に呼び出されます。実際の送信中に取得されるタスク ID をセッション変数（有効期限と共に）に設定します。</td>
  </tr>
  <tr>
   <td>submitTask</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>送信</td>
   <td>タスクに関連付けられたドキュメントオブジェクトを送信します（そして次にプロセスを送信します）。</td>
  </tr>
  <tr>
   <td>getRootEndpointCategories</td>
   <td>ProcessManagementStartpointService</td>
   <td>getRootEndpointCategories</td>
   <td>サーバーに存在するすべてのルートカテゴリを取得します。</td>
  </tr>
  <tr>
   <td>getDirectChildCategories</td>
   <td>ProcessManagementStartpointService</td>
   <td>getDirectChildCategories2</td>
   <td>カテゴリのすべての直接の子を取得します。</td>
  </tr>
  <tr>
   <td>getAllStartpoints</td>
   <td>ProcessManagementStartpointService</td>
   <td>getAllStartpoints</td>
   <td>サーバーに存在するすべてのカテゴリのすべてのスタートポイントを取得します。</td>
  </tr>
  <tr>
   <td>invokeStartpoint</td>
   <td>ProcessManagementStartpointService</td>
   <td>invokeStartpoint</td>
   <td>これにより、スタートポイントが呼びされてスタートポイントに対応する新しいタスクが作成されます。</td>
  </tr>
  <tr>
   <td>getAllTasks</td>
   <td>ProcessManagementTaskService</td>
   <td>getAllActionableTasks</td>
   <td>ログインユーザーに対して作成して転送または参照された、保存された、割り当てられた、割り当てて保存された、すべてのタスクを取得します。</td>
  </tr>
  <tr>
   <td>getTask</td>
   <td>ProcessManagementTaskService</td>
   <td>getTask</td>
   <td>特定のタスクを取得します。</td>
  </tr>
  <tr>
   <td>renderTask</td>
   <td>ProcessManagementTaskService</td>
   <td>render</td>
   <td>タスクをレンダリングして、フォーム URL、フォームタイプ、データ URL （必要な場合）などフォームのレンダリングに必要な情報を返します。</td>
  </tr>
  <tr>
   <td>submitWithPriorData</td>
   <td>ProcessManagementTaskService</td>
   <td>submitWithPriorData</td>
   <td>結果キーを使用して TaskManager の送信 API の結果を返します。</td>
  </tr>
  <tr>
   <td>submitWithData</td>
   <td>ProcessManagementTaskService</td>
   <td>submitWithData</td>
   <td>TaskManager の送信 API を使用してタスクに関連付けられたフォームデータ（文字列として渡された）を送信します。TaskManager の送信 API を呼び出さない Flex フォームに使用されます。</td>
  </tr>
  <tr>
   <td>save</td>
   <td>ProcessManagementTaskService</td>
   <td>save</td>
   <td>タスクをサーバーに保存します。</td>
  </tr>
  <tr>
   <td>complete</td>
   <td>ProcessManagementTaskService</td>
   <td>complete</td>
   <td>タスクを完了し、タスクはプロセス設計に従って次の手順に渡されます。</td>
  </tr>
  <tr>
   <td>getAttachment</td>
   <td>ProcessManagementTaskService</td>
   <td>getAttachment</td>
   <td>利用できる添付ファイルの URL を返します。</td>
  </tr>
  <tr>
   <td>getAllAttachments</td>
   <td>ProcessManagementTaskService</td>
   <td>getAllActionableAttachments</td>
   <td>タスクのすべての添付ファイルおよびメモを取得します。</td>
  </tr>
  <tr>
   <td>share</td>
   <td>ProcessManagementTaskService</td>
   <td>share</td>
   <td>別のユーザーとタスクを共有します。別のユーザーはタスクを要求してタスクの所有者になることができます。</td>
  </tr>
  <tr>
   <td>forward</td>
   <td>ProcessManagementTaskService</td>
   <td>forward</td>
   <td>別のユーザーにタスクを転送します。</td>
  </tr>
  <tr>
   <td>consult</td>
   <td>ProcessManagementTaskService</td>
   <td>consult</td>
   <td>別のユーザーにタスクについて問い合わせます。</td>
  </tr>
  <tr>
   <td>claim</td>
   <td>ProcessManagementTaskService</td>
   <td>claim</td>
   <td>共有キューで使用可能なタスクを要求します。</td>
  </tr>
  <tr>
   <td>unlock</td>
   <td>ProcessManagementTaskService</td>
   <td>unlock</td>
   <td>タスクのロックを解除します。</td>
  </tr>
  <tr>
   <td>lock</td>
   <td>ProcessManagementTaskService</td>
   <td>lock</td>
   <td>タスクをロックします。これにより、共有されている場合は別のユーザーが要求できなくなります。</td>
  </tr>
  <tr>
   <td>reject</td>
   <td>ProcessManagementTaskService</td>
   <td>reject</td>
   <td>タスクを前の所有者に返します。</td>
  </tr>
  <tr>
   <td>abandon</td>
   <td>ProcessManagementTaskService</td>
   <td>abandon</td>
   <td>タスクを削除します。</td>
  </tr>
  <tr>
   <td>setVisibility</td>
   <td>ProcessManagementTaskService</td>
   <td>setVisibility</td>
   <td>タスクの表示を設定します。表示が false に設定された場合は、それ以降ユーザーに表示されなくなります。</td>
  </tr>
  <tr>
   <td>getUsers</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getUsers</td>
   <td>ユーザーの検索に使用します。名前が指定されていない場合はすべてのユーザーを返しますが、そうでない場合は指定された名前のユーザーを返します。</td>
  </tr>
  <tr>
   <td>getUsersInGroup</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getUsersInGroupByName</td>
   <td>グループ内のすべてのユーザーを返します。</td>
  </tr>
  <tr>
   <td>grantQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>grantQueueAccess</td>
   <td>ログインユーザーのキューへのアクセス権を、指定したユーザーに付与します。基本的に固有のキューを別のユーザーと共有することになります。</td>
  </tr>
  <tr>
   <td>requestQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>requestQueueAccess</td>
   <td>ログインしたユーザーに対して指定したユーザーのキューへのアクセスをリクエストします。ユーザーがリクエストを承認した場合、ユーザーのキューはログインユーザーと共有されます。</td>
  </tr>
  <tr>
   <td>getGrantedUsers</td>
   <td>ProcessManagementQueueService</td>
   <td>getGrantedUsers</td>
   <td>ログインユーザーのキューへのアクセス権を持つすべてのユーザーを返します。</td>
  </tr>
  <tr>
   <td>getUsersForAccessibleQueues</td>
   <td>ProcessManagementQueueService</td>
   <td>getUsersForAccessibleQueues</td>
   <td>ユーザーにアクセス可能なキューを持つすべてのユーザーを返します。</td>
  </tr>
  <tr>
   <td>revokeQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>revokeQueueAccess</td>
   <td>ログインユーザーのキューへのアクセス権を持つユーザーのリストから、ユーザーを削除します。</td>
  </tr>
  <tr>
   <td>removeQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>removeQueueAccess</td>
   <td>ログインユーザーがアクセス可能なキューを持つユーザーのリストから、ユーザーを削除します。</td>
  </tr>
  <tr>
   <td>getAllQueues<br /> </td>
   <td>ProcessManagementQueueService<br /> </td>
   <td>getAllQueues<br /> </td>
   <td>ログインユーザーがアクセスできるすべてのキュー（自分のキュー、共有キュー、およびグループキュー）を取得します。<br /> </td>
  </tr>
  <tr>
   <td>getOutOfOfficeSettings</td>
   <td>ProcessManagementOutOfOfficeService</td>
   <td>getOutOfOfficeSettings</td>
   <td>ユーザーの不在設定を取得します。</td>
  </tr>
  <tr>
   <td>saveOutOfOfficeSettingsJson</td>
   <td>ProcessManagementOutOfOfficeService</td>
   <td>saveOutOfOfficeSettingsJson</td>
   <td>ユーザーの不在設定を保存します。</td>
  </tr>
  <tr>
   <td>getAllProcesses</td>
   <td>ProcessManagementProcessService</td>
   <td>getAllProcesses</td>
   <td>すべてのプロセスのリストを返します。</td>
  </tr>
  <tr>
   <td>getParticipatedProcesses</td>
   <td>ProcessManagementProcessService</td>
   <td>getParticipatedProcesses</td>
   <td>ログインユーザーが参加したすべてのプロセス名のリストを返します。</td>
  </tr>
  <tr>
   <td>getProcessInstance<br /> </td>
   <td>ProcessManagementProcessService<br /> </td>
   <td>getProcessInstance<br /> </td>
   <td>プロセスインスタンスの詳細を取得します。<br /> </td>
  </tr>
  <tr>
   <td>getProcessInstances</td>
   <td>ProcessManagementQueryService</td>
   <td>getProcessInstances</td>
   <td>プロセスのすべてのプロセスインスタンスを取得します。</td>
  </tr>
  <tr>
   <td>getPendingTasksForProcessInstance</td>
   <td>ProcessManagementQueryService</td>
   <td>getPendingTasksForProcessInstance</td>
   <td>プロセスインスタンスの保留中のタスクを取得します。</td>
  </tr>
  <tr>
   <td>getTasksForProcessInstance</td>
   <td>ProcessManagementQueryService</td>
   <td>getTasksForProcessInstance</td>
   <td>プロセスインスタンスのすべてのタスクを取得します。</td>
  </tr>
  <tr>
   <td>getAllSearchTemplates</td>
   <td>ProcessManagementQueryService</td>
   <td>getAllSearchTemplates</td>
   <td>すべての検索テンプレートのリストを返します。</td>
  </tr>
  <tr>
   <td>getTemplate</td>
   <td>ProcessManagementQueryService</td>
   <td>getTemplate</td>
   <td>検索テンプレートの内容を返します。</td>
  </tr>
  <tr>
   <td>findTasksJson<br /> </td>
   <td>ProcessManagementQueryService</td>
   <td>findTasksJson</td>
   <td>検索テンプレートのすべての条件を満たすすべてのタスクを検索して返します。</td>
  </tr>
  <tr>
   <td>getAssignmentsForTask</td>
   <td>ProcessManagementTaskService</td>
   <td>getAssignmentsForTask</td>
   <td>タスクのすべての割り当てを取得します。例えば、ユーザーがタスクを別のユーザーに転送または問い合わせする場合、それがタスクの割り当てになります。</td>
  </tr>
  <tr>
   <td>deleteAttachment </td>
   <td>TaskManagerService</td>
   <td>deleteAttachment</td>
   <td>添付ファイルを削除します。</td>
  </tr>
  <tr>
   <td>initialize</td>
   <td>ProcessManagementClientSessionService</td>
   <td>initialize</td>
   <td>必要に応じてアサーションを更新します。ユーザーを認証します。サーバー／クライアント情報のセッションパラメーターを設定します。ユーザー情報およびポーリング間隔を返します。</td>
  </tr>
  <tr>
   <td>getTasksForDirectReports</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>getTasksForDirectReports</td>
   <td>ログインしたマネージャーの直属の部下のすべてのタスクを返します。</td>
  </tr>
  <tr>
   <td>getTaskOfDirectReport<br /> </td>
   <td>ProcessManagementTeamTasksService</td>
   <td>getDirectReportTask</td>
   <td>ログインしたマネージャーの指定された直属の部下のタスクを返します。</td>
  </tr>
  <tr>
   <td>forwardTaskOfDirectReport</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>forwardTaskOfDirectReport</td>
   <td>別のユーザーに直属の部下のタスクを転送します。</td>
  </tr>
  <tr>
   <td>rejectTaskOfDirectReport</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>rejectTaskOfDirectReport</td>
   <td>前のユーザーに直属の部下のタスクを返します。</td>
  </tr>
  <tr>
   <td>getProperty</td>
   <td>WorkspacePropertyService</td>
   <td>getProperty</td>
   <td>ユーザーのワークスペースプロパティを取得します。</td>
  </tr>
  <tr>
   <td>removeProperty</td>
   <td>WorkspacePropertyService</td>
   <td>delete</td>
   <td>ユーザーのワークスペースプロパティを削除します。</td>
  </tr>
  <tr>
   <td>getProperties</td>
   <td>WorkspacePropertyService</td>
   <td>getPropertiesAsMap</td>
   <td>ユーザーのすべてのワークスペースプロパティを返します。</td>
  </tr>
  <tr>
   <td>setProperty</td>
   <td>WorkspacePropertyService</td>
   <td>setProperty</td>
   <td>ユーザーのワークスペースプロパティを設定します。</td>
  </tr>
  <tr>
   <td>getCurrentUserImageUrl</td>
   <td>ProcessManagementClientSessionService</td>
   <td>getCurrentUserImageUrl</td>
   <td>ログインユーザーのユーザーの画像 URL を取得します。</td>
  </tr>
  <tr>
   <td>getUserImageUrl</td>
   <td>ProcessManagementClientSessionService</td>
   <td>getUserImageUrl</td>
   <td>指定したユーザーのユーザーの画像 URL を取得します。</td>
  </tr>
  <tr>
   <td>uploadNote</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>uploadNote</td>
   <td>タスクのメモをサーバーにアップロードします。</td>
  </tr>
  <tr>
   <td>uploadRMAToServer（HTML テンプレートから直接呼び出すこともできます）<br /> </td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>uploadAttachment</td>
   <td>サーバーにタスクの添付ファイルをアップロードします。</td>
  </tr>
  <tr>
   <td>getImageURL（HTML テンプレートから直接呼び出すこともできます）</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>getImage</td>
   <td>プロセスの画像を取得します。</td>
  </tr>
 </tbody>
</table>
