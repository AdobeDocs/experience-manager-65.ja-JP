---
title: AEM Forms ワークスペースで使用する各種 API
seo-title: AEM Forms ワークスペースで使用する各種 API
description: Public Java API、JavaScript API、および LiveCycle AEM Forms ワークスペースのメソッド、カスタマイズとオートメーションのために開示。
seo-description: Public Java API、JavaScript API、および LiveCycle AEM Forms ワークスペースのメソッド、カスタマイズとオートメーションのために開示。
uuid: 9602990e-8ac7-42eb-b507-50b3594055ba
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 4a73a973-fccf-466b-b4a0-47652a14a080
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# AEM Forms ワークスペースで使用する 各種 API {#apis-used-in-aem-forms-workspace}

AEM Forms ワークスペースでは次の API が使用されています。

<table>
 <tbody>
  <tr>
   <td><strong>Javascript メソッド</strong></td>
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
   <td>これは、フォームを DocumentSubmitServlet 経由で送信する前に呼び出されます。実際の送信中に取得されるタスク ID をセッション変数（有効期限と共に）に設定します。</td>
  </tr>
  <tr>
   <td>submitTask</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>submit</td>
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
   <td>すべてのカテゴリ下にあるサーバーに存在するすべてのスタートポイントを取得します。</td>
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
   <td>ログインしたユーザーに対して作成されて転送または問い合わせ、保存、割り当てられた、あるいは割り当てられて保存されたすべてのタスクを取得します。</td>
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
   <td>TaskManager の送信 API を使用してタスクに関連付けられたフォームデータ（文字列として渡された）を送信します。TaskManager の送信 API を呼び出さないフレックスフォームに使用されます。</td>
  </tr>
  <tr>
   <td>保存</td>
   <td>ProcessManagementTaskService</td>
   <td>保存</td>
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
   <td>共有</td>
   <td>ProcessManagementTaskService</td>
   <td>共有</td>
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
   <td>タスクをロック解除します。</td>
  </tr>
  <tr>
   <td>lock</td>
   <td>ProcessManagementTaskService</td>
   <td>lock</td>
   <td>タスクをロックします。これにより、共有されている場合は別のユーザーが要求できなくなります。</td>
  </tr>
  <tr>
   <td>拒否</td>
   <td>ProcessManagementTaskService</td>
   <td>拒否</td>
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
   <td>ユーザーの検索に使用されます。名前が指定されていない場合はすべてのユーザーを返しますが、そうでない場合は指定された名前のユーザーを返します。</td>
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
   <td>ログインしたユーザーのキューへのアクセスを指定したユーザーに付与します。基本的に固有のキューを別のユーザーと共有することになります。</td>
  </tr>
  <tr>
   <td>requestQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>requestQueueAccess</td>
   <td>ログインしたユーザーに対して指定したユーザーのキューへのアクセスを要求します。ユーザーが要求を承認した場合、ユーザーのキューはログインユーザーと共有されます。</td>
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
   <td>ユーザーのリストから、ログインユーザーのキューへのアクセス権を持つユーザーを削除します。</td>
  </tr>
  <tr>
   <td>removeQueueAccess</td>
   <td>ProcessManagementQueueService</td>
   <td>removeQueueAccess</td>
   <td>ユーザーのリストからログインユーザーにアクセス可能なキューを持つユーザーを削除します。</td>
  </tr>
  <tr>
   <td>getAllQueues<br /> </td>
   <td>ProcessManagementQueueService<br /> </td>
   <td>getAllQueues<br /> </td>
   <td>ログインユーザーにアクセス可能なすべてのキュー（固有のキュー、共有キューおよびグループキュー）を取得します。<br /> </td>
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
   <td>タスクのすべてのアサインを取得します。例えば、ユーザーがタスクを別のユーザーに転送または問い合わせする場合、それがタスクのアサインになります。</td>
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
   <td>必要に応じてアサーションを更新します。ユーザーを認証します。サーバー / クライアント情報のセッションパラメータを設定します。ユーザー情報およびポーリング間隔を返します。</td>
  </tr>
  <tr>
   <td>getTasksForDirectReports</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>getTasksForDirectReports</td>
   <td>ログインしたマネージャーの直接レポートのすべてのタスクを返します。</td>
  </tr>
  <tr>
   <td>getTaskOfDirectReport<br /> </td>
   <td>ProcessManagementTeamTasksService</td>
   <td>getTaskOfDirectReport</td>
   <td>ログインしたマネージャーの指定された直接レポートのタスクを返します。</td>
  </tr>
  <tr>
   <td>forwardTaskOfDirectReport</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>forwardTaskOfDirectReport</td>
   <td>別のユーザーに直接レポートのタスクを転送します。</td>
  </tr>
  <tr>
   <td>rejectTaskOfDirectReport</td>
   <td>ProcessManagementTeamTasksService</td>
   <td>rejectTaskOfDirectReport</td>
   <td>前のユーザーに直接レポートのタスクを返します。</td>
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
   <td>ログインしたユーザーのユーザーの画像 URL を取得します。</td>
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
   <td>uploadRMAToServer （HTML テンプレートから直接呼び出すこともできます）<br /> </td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>uploadAttachment</td>
   <td>サーバーにタスクの添付ファイルをアップロードします。</td>
  </tr>
  <tr>
   <td>getImageURL （HTML テンプレートから直接呼び出すこともできます）</td>
   <td>ProcessManagementDocumentHandlingService</td>
   <td>getImage</td>
   <td>プロセスの画像を取得します。</td>
  </tr>
 </tbody>
</table>
