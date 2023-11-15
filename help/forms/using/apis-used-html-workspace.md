---
title: AEM Forms ワークスペースで使用する各種 API
description: パブリック Java&trade、JavaScript API およびLiveCycleAEM Forms Workspace のメソッド、カスタマイズと自動化のために公開。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 9034f73a-83f3-498e-b6a6-ad6577aa1a3a
source-git-commit: 7f35fdee9dbca9dfd3992b56579d6d06633f8dec
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 3%

---

# AEM Forms ワークスペースで使用する各種 API {#apis-used-in-aem-forms-workspace}

AEM Forms Workspace では、次の API が使用されます。

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
   <td>グループを検索します。 何も指定しなかった場合は、すべてのグループのリストを返し、指定した名前のグループを返します。</td>
  </tr>
  <tr>
   <td>getUsersAndGroups</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getUsersAndGroups</td>
   <td>ユーザーとグループを検索します。 何も指定しなかった場合は、すべてのユーザーとグループのリストを返し、指定した名前のユーザーとグループを返します。</td>
  </tr>
  <tr>
   <td>prepareForSubmit</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>prepareForSubmit</td>
   <td>このメソッドは、DocumentSubmitServlet を介してフォームを送信する前に呼び出されます。 実際の送信中に取得されるタスク ID をセッション変数（有効期限と共に）に設定します。</td>
  </tr>
  <tr>
   <td>submitTask</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>送信</td>
   <td>タスクに関連付けられたドキュメントオブジェクトを送信します（そして、次にプロセスを送信します）。</td>
  </tr>
  <tr>
   <td>getRootEndpointCategories</td>
   <td>ProcessManagementStartpointService</td>
   <td>getRootEndpointCategories</td>
   <td>サーバー上に存在するすべてのルートカテゴリを取得します。</td>
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
   <td>すべてのカテゴリ下にサーバー上に存在するすべてのスタートポイントを取得します。</td>
  </tr>
  <tr>
   <td>invokeStartpoint</td>
   <td>ProcessManagementStartpointService</td>
   <td>invokeStartpoint</td>
   <td>これにより、スタートポイントが呼び出され、スタートポイントに対応するタスクが作成されます</td>
  </tr>
  <tr>
   <td>getAllTasks</td>
   <td>ProcessManagementTaskService</td>
   <td>getAllActionableTasks</td>
   <td>ログインしたユーザーに対して作成、転送、問い合わせ、保存、割り当て、割り当て、保存されたすべてのタスクを取得します。</td>
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
   <td>タスクをレンダリングし、必要に応じて、フォームのレンダリングに必要な情報を、フォームの URL、フォームの種類、データの URL などとして返します。</td>
  </tr>
  <tr>
   <td>submitWithPriorData</td>
   <td>ProcessManagementTaskService</td>
   <td>submitWithPriorData</td>
   <td>TaskManager の送信 API の結果を、結果キーを使用して返します。</td>
  </tr>
  <tr>
   <td>submitWithData</td>
   <td>ProcessManagementTaskService</td>
   <td>submitWithData</td>
   <td>TaskManager の送信 API を使用して、タスクに関連付けられた（文字列として渡された）フォームデータを送信します。 TaskManager の送信 API を呼び出さないFlexフォームに使用されます。</td>
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
   <td>タスクが完了し、プロセスデザインに従ってタスクが次のステップに渡されます。</td>
  </tr>
  <tr>
   <td>getAttachment</td>
   <td>ProcessManagementTaskService</td>
   <td>getAttachment</td>
   <td>添付ファイルが使用可能な添付ファイルの URL を返します。</td>
  </tr>
  <tr>
   <td>getAllAttachments</td>
   <td>ProcessManagementTaskService</td>
   <td>getAllActionableAttachments</td>
   <td>タスクのすべての添付ファイルとメモを取得します。</td>
  </tr>
  <tr>
   <td>share</td>
   <td>ProcessManagementTaskService</td>
   <td>share</td>
   <td>別のユーザーとタスクを共有します。 別のユーザーがタスクを要求して、タスクの所有者になることができます。</td>
  </tr>
  <tr>
   <td>送る</td>
   <td>ProcessManagementTaskService</td>
   <td>送る</td>
   <td>タスクを別のユーザーに転送します。</td>
  </tr>
  <tr>
   <td>consult</td>
   <td>ProcessManagementTaskService</td>
   <td>consult</td>
   <td>別のユーザーにタスクを問い合わせます。</td>
  </tr>
  <tr>
   <td>claim</td>
   <td>ProcessManagementTaskService</td>
   <td>claim</td>
   <td>共有キューで使用可能なタスクを要求します。</td>
  </tr>
  <tr>
   <td>ロック解除</td>
   <td>ProcessManagementTaskService</td>
   <td>ロック解除</td>
   <td>タスクのロックを解除します。</td>
  </tr>
  <tr>
   <td>ロック</td>
   <td>ProcessManagementTaskService</td>
   <td>ロック</td>
   <td>タスクをロックします。共有している場合は、別のユーザーがタスクを要求することはできません。</td>
  </tr>
  <tr>
   <td>reject</td>
   <td>ProcessManagementTaskService</td>
   <td>reject</td>
   <td>タスクの前の所有者にタスクを返します。</td>
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
   <td>タスクの表示を設定します。 visibility が false に設定されている場合、後でユーザーにはタスクが表示されません。</td>
  </tr>
  <tr>
   <td>getUsers</td>
   <td>ProcessManagementUserProxyService</td>
   <td>getUsers</td>
   <td>ユーザーの検索に使用されます。 名前が指定されていない場合はすべてのユーザーを返し、指定された名前を持つユーザーを返します。</td>
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
   <td>ログインしたユーザーのキューへのアクセスを指定したユーザーに許可します。 基本的に、自分のキューを別のユーザーと共有しています。</td>
  </tr>
  <tr>
   <td>requestQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>requestQueueAccess</td>
   <td>ログインしたユーザーに対して、指定したユーザーのキューのアクセス要求を行います。 ユーザーがリクエストを承認すると、そのユーザーのキューがログインしたユーザーと共有されます。</td>
  </tr>
  <tr>
   <td>getGrantedUsers</td>
   <td>ProcessManagementQueueService</td>
   <td>getGrantedUsers</td>
   <td>ログインしたユーザーのキューにアクセスできるすべてのユーザーを返します。</td>
  </tr>
  <tr>
   <td>getUsersForAccessibleQueues</td>
   <td>ProcessManagementQueueService</td>
   <td>getUsersForAccessibleQueues</td>
   <td>ユーザーがアクセス可能なキューを持つすべてのユーザーを返します。</td>
  </tr>
  <tr>
   <td>revokeQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>revokeQueueAccess</td>
   <td>ログインしたユーザーのキューにアクセスできるユーザーのリストから、ユーザーを削除します。</td>
  </tr>
  <tr>
   <td>removeQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>removeQueueAccess</td>
   <td>ログインしたユーザーがキューにアクセスできるユーザーのリストからユーザーを削除します。</td>
  </tr>
  <tr>
   <td>getAllQueues<br /> </td>
   <td>ProcessManagementQueueService<br /> </td>
   <td>getAllQueues<br /> </td>
   <td>ログインしたユーザーがアクセスできるすべてのキュー（独自、共有、グループのキュー）を取得します。<br /> </td>
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
   <td>getRenitedProcesses</td>
   <td>ProcessManagementProcessService</td>
   <td>getRenitedProcesses</td>
   <td>ログインしたユーザーが参加したすべてのプロセス名のリストを返します。</td>
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
   <td>すべての検索テンプレートのリストが返されます。</td>
  </tr>
  <tr>
   <td>getTemplate</td>
   <td>ProcessManagementQueryService</td>
   <td>getTemplate</td>
   <td>検索テンプレートのコンテンツを返します。</td>
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
   <td>タスクのすべての割り当てを取得します。 例えば、あるユーザーが別のユーザーにタスクを転送または問い合わせした場合、そのタスクはタスクの割り当てになります。</td>
  </tr>
  <tr>
   <td>deleteAttachment </td>
   <td>TaskManagerService</td>
   <td>deleteAttachment</td>
   <td>添付ファイルが削除されます。</td>
  </tr>
  <tr>
   <td>initialize</td>
   <td>ProcessManagementClientSessionService</td>
   <td>initialize</td>
   <td>必要に応じてアサーションを更新します。 ユーザーを認証します。 サーバー/クライアント情報のセッションパラメーターを設定します。 ユーザー情報とポーリング間隔を返します。</td>
  </tr>
  <tr>
   <td>getTasksForDirectReports</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>getTasksForDirectReports</td>
   <td>ログインしたマネージャーの直属の部下のタスクをすべて返します。</td>
  </tr>
  <tr>
   <td>getTaskOfDirectReport<br /> </td>
   <td>ProcessManagementTeamTasksService</td>
   <td>getDirectReportTask</td>
   <td>ログインしたマネージャーの指定した直属のレポートのタスクを返します。</td>
  </tr>
  <tr>
   <td>forwardTaskOfDirectReport</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>forwardTaskOfDirectReport</td>
   <td>直属のレポートのタスクを別のユーザーに転送します。</td>
  </tr>
  <tr>
   <td>rejectTaskOfDirectReport</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>rejectTaskOfDirectReport</td>
   <td>直属のレポートのタスクを前のユーザーに返します。</td>
  </tr>
  <tr>
   <td>getProperty</td>
   <td>WorkspacePropertyService</td>
   <td>getProperty</td>
   <td>ユーザーの Workspace プロパティを取得します。</td>
  </tr>
  <tr>
   <td>removeProperty</td>
   <td>WorkspacePropertyService</td>
   <td>delete</td>
   <td>ユーザーの Workspace プロパティを削除します。</td>
  </tr>
  <tr>
   <td>getProperties</td>
   <td>WorkspacePropertyService</td>
   <td>getPropertiesAsMap</td>
   <td>ユーザーのすべての Workspace プロパティを返します。</td>
  </tr>
  <tr>
   <td>setProperty</td>
   <td>WorkspacePropertyService</td>
   <td>setProperty</td>
   <td>ユーザーの Workspace プロパティを設定します。</td>
  </tr>
  <tr>
   <td>getCurrentUserImageUrl</td>
   <td>ProcessManagementClientSessionService</td>
   <td>getCurrentUserImageUrl</td>
   <td>ログインしたユーザーの画像 URL を取得します。</td>
  </tr>
  <tr>
   <td>getUserImageUrl</td>
   <td>ProcessManagementClientSessionService</td>
   <td>getUserImageUrl</td>
   <td>指定されたユーザーのユーザーの画像 URL を取得します。</td>
  </tr>
  <tr>
   <td>uploadNote</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>uploadNote</td>
   <td>タスクのメモをサーバーにアップロードします。</td>
  </tr>
  <tr>
   <td>uploadRMAToServer （html テンプレートから直接呼び出すこともできます）<br /> </td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>uploadAttachment</td>
   <td>タスクの添付ファイルをサーバーにアップロードします。</td>
  </tr>
  <tr>
   <td>getImageURL (HTMLテンプレートから直接呼び出されます )</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>getImage</td>
   <td>プロセスの画像を取得します。</td>
  </tr>
 </tbody>
</table>
