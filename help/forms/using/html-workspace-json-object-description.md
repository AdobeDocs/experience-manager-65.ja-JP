---
title: AEM Forms Workspace JSON オブジェクトの詳細
seo-title: AEM Forms Workspace JSON オブジェクトの詳細
description: LiveCycle AEM Forms Workspace でカスタマイズ、拡張、変更、再利用のために使用された JSON JavaScript オブジェクトについての概念情報。
seo-description: LiveCycle AEM Forms Workspace でカスタマイズ、拡張、変更、再利用のために使用された JSON JavaScript オブジェクトについての概念情報。
uuid: 91c923c8-144a-4453-ba91-6a5193f1c4c4
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 61b7246d-ed28-4470-a0a2-a4aaf1a061a4
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# AEM Forms Workspace JSON オブジェクトの詳細 {#aem-forms-workspace-json-object-description}

AEM Forms Workspace で使用される JSON オブジェクトについて以下に説明します。

1. カテゴリ

   カテゴリは、Workspace の「開始プロセス」タブにあります。これらのカテゴリは、スタートポイントを分類するのに使用されます。

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ</strong></td>
   <td><strong>クライアントのみ</strong></td>
   <td><strong>コメント</strong></td>
  </tr>
  <tr>
   <td>名前</td>
   <td>F</td>
   <td>カテゴリ名</td>
  </tr>
  <tr>
   <td>id</td>
   <td>F</td>
   <td>カテゴリ ID<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>description<br type="_moz" /> </td>
   <td>F</td>
   <td>カテゴリの説明<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>parentOid<br type="_moz" /> </td>
   <td>F</td>
   <td>親カテゴリの oid が含まれます<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>startPointsList<br type="_moz" /> </td>
   <td>T</td>
   <td>カテゴリにあるすべてのスタートポイントのリストが含まれます</td>
  </tr>
  <tr>
   <td>categoryList</td>
   <td>T</td>
   <td>カテゴリの直接の子カテゴリのリストが含まれます<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>「すべてのスタートポイント」および「お気に入り」は、クライアント側で定義されるカテゴリです。「お気に入り」カテゴリには、ユーザーがお気に入りのマークを付けたすべてのスタートポイントが含まれます。「すべてのスタートポイント」カテゴリには、すべてのスタートポイントが含まれます。

1. スタートポイント

   スタートポイントは、呼び出された場合に Workspace からプロセスを開始するのに使用されます。

   | **プロパティ** | **クライアントのみ** | **コメント** |
   |---|---|---|
   | categoryId | F | スタートポイントが属するカテゴリの ID が含まれます。 |
   | description | F | スタートポイントの説明が含まれます。 |
   | 名前 | F | スタートポイントの名前が含まれます。 |
   | serializedImageTicket | F | スタートポイントに対応するイメージチケットが含まれます。このイメージチケットは、サーバーからスタートポイントのイメージを取得するために、スタートポイントのimageUrlフィールドで使用されます。 |
   | serviceName | F | スタートポイントのサービスの名前が含まれます。 |
   | startpointId | F | スタートポイントの ID が含まれます。 |
   | isFavorite | T | スタートポイントがお気に入りであるかどうかを示します。スタートポイントがお気に入りである場合は true、そうでない場合は false です。 |
   | isDefaultImage | T | プロセスに指定されたイメージがあるかどうかを示します。プロセスに関連付けられたイメージがない場合は true、ある場合は false です。 |
   | タスク | T | スタートポイントが呼び出される際に作成されたタスクが含まれます。 |
   | imageUrl | T | スタートポイントに対応するイメージの URL が含まれます。 |

1. タスク

   タスクはユーザー / グループに割り当てられ、データを入力できるフォームまたは Guide （推奨されていません）のユーザーインターフェイスが含まれます。ユーザーにタスクが割り当てられると、完了して送信するためのフォームまたは Guide が提供されます。

<table>
 <tbody>
  <tr>
   <td>プロパティ<br /> </td>
   <td>クライアントのみ<br /> </td>
   <td>コメント<br /> </td>
  </tr>
  <tr>
   <td>classOfTask</td>
   <td>F</td>
   <td>タスクが lc8 タスクの場合、タスクのクラスは「LC8」ですが、それ以外の場合は「標準」です。<br /> </td>
  </tr>
  <tr>
   <td>completeTime<br /> </td>
   <td>F</td>
   <td>タスクが完了した時間のタイムスタンプが含まれます。<br /> </td>
  </tr>
  <tr>
   <td>consultGroupId<br /> </td>
   <td>F</td>
   <td>タスクを問い合わせることができるグループの ID が含まれます。これは、プロセスのデザイン中に設定されます。<br /> </td>
  </tr>
  <tr>
   <td>createTime<br /> </td>
   <td>F</td>
   <td>タスクが作成された時間のタイムスタンプが含まれます。<br /> </td>
  </tr>
  <tr>
   <td>creationId<br /> </td>
   <td>F</td>
   <td>タスクを作成したユーザーの ID が含まれます。<br /> </td>
  </tr>
  <tr>
   <td>currentAssignment<br /> </td>
   <td>F</td>
   <td>タスクの現在の割り当てに関する詳細が含まれます。<br /> </td>
  </tr>
  <tr>
   <td>deadline<br /> </td>
   <td>F</td>
   <td>タスクがデッドラインに達する時間のタイムスタンプが含まれます。<br /> </td>
  </tr>
  <tr>
   <td>description<br /> </td>
   <td>F</td>
   <td>タスクの説明が含まれます。<br /> </td>
  </tr>
  <tr>
   <td>displayName<br /> </td>
   <td>F</td>
   <td>タスクの表示名が含まれます。<br /> </td>
  </tr>
  <tr>
   <td>forwardGroupId<br /> </td>
   <td>F</td>
   <td>タスクを転送することができるグループの ID が含まれます。これは、プロセスのデザイン中に設定されます。<br /> </td>
  </tr>
  <tr>
   <td>instructions<br /> </td>
   <td>F</td>
   <td>タスクの手順が含まれます。<br /> </td>
  </tr>
  <tr>
   <td>isLocked<br /> </td>
   <td>F</td>
   <td>タスクがロックされている場合は true です。<br /> </td>
  </tr>
  <tr>
   <td>isMustOpenToComplete<br /> </td>
   <td>F</td>
   <td>タスクを完了するのにタスクフォームを開く必要がある場合は true です。<br /> </td>
  </tr>
  <tr>
   <td>isOpenFullScreen<br /> </td>
   <td>F</td>
   <td>true の場合は、タスクを開くと、フォームは最初に全スクリーンで表示されます。<br /> </td>
  </tr>
  <tr>
   <td>isRouteSelectionRequired<br /> </td>
   <td>F</td>
   <td>true の場合、タスクを完了するのにルートが選択されている必要があります。<br /> </td>
  </tr>
  <tr>
   <td>isShowAttachments<br /> </td>
   <td>F</td>
   <td>true の場合は添付ファイルが表示されます。<br /> </td>
  </tr>
  <tr>
   <td>isStartTask<br /> </td>
   <td>F</td>
   <td>true の場合、タスクはスタートポイントから作成されます。<br /> </td>
  </tr>
  <tr>
   <td>isVisible<br /> </td>
   <td>F</td>
   <td>タスクが Workspace に表示されている場合は true です。<br /> </td>
  </tr>
  <tr>
   <td>nextReminder<br /> </td>
   <td>F</td>
   <td>次のリマインダーのタイムスタンプです。<br /> </td>
  </tr>
  <tr>
   <td>priority<br /> </td>
   <td>F</td>
   <td>タスクの優先度が含まれます。<br /> 1 = 最高の優先度<br /> 2 = 高い優先度<br /> 3 = 標準の優先度<br /> 4 = 低い優先度<br /> 5 = 最低の優先度<br /> </td>
  </tr>
  <tr>
   <td>processInstanceId</td>
   <td>F</td>
   <td>タスクの一部であるプロセスインスタンスの ID。<br /> </td>
  </tr>
  <tr>
   <td>processInstanceStatus<br /> </td>
   <td>F</td>
   <td>タスクのプロセスインスタンスのステータス。<br /> </td>
  </tr>
  <tr>
   <td>reminderCount<br /> </td>
   <td>F</td>
   <td>タスクのリマインダーの数が含まれます。<br /> </td>
  </tr>
  <tr>
   <td>routeList<br /> </td>
   <td>F</td>
   <td>タスクに関連付けられたルートのリストが含まれます。ユーザーはルートリストからいずれかのルートを選択することによって、タスクを完了することができます。<br /> </td>
  </tr>
  <tr>
   <td>selectedRoute<br /> </td>
   <td>F</td>
   <td>タスクが完了した場合に選択したルートの名前が含まれます。<br /> </td>
  </tr>
  <tr>
   <td>serializedImageTicket<br /> </td>
   <td>F</td>
   <td>タスクに対応するイメージチケットが含まれます。このイメージチケットは、サーバーからタスクのイメージを取得するために、タスクの imageUrl フィールドで使用されます。<br /> <br /> </td>
  </tr>
  <tr>
   <td>serviceName<br /> </td>
   <td>F</td>
   <td>タスクのサービスの名前が含まれます。<br /> </td>
  </tr>
  <tr>
   <td>serviceTitle<br /> </td>
   <td>F</td>
   <td>タスクのサービスのタイトルが含まれます。<br /> </td>
  </tr>
  <tr>
   <td>status<br /> </td>
   <td>F</td>
   <td>1 = 作成済み（タスクはスタートポイントから作成されました。）<br />2 = 作成して保存済み（タスクはスタートポイントから作成されて保存されました。）<br />3 = 割り当て済み（タスクはプロセスが開始された後でユーザーに割り当てられました。）<br />4 = 割り当てて保存済み（タスクは割り当てられて保存されました。）<br />100 = 完了（タスクは完了しました。）<br />101 = 期限切れ（タスクはデッドラインに達しました。）<br /> 102 = 終了<br /> </td>
  </tr>
  <tr>
   <td>stepName<br /> </td>
   <td>F</td>
   <td>プロセスのデザイン中に設定されたタスクの名前が含まれます。<br /> </td>
  </tr>
  <tr>
   <td>summaryUrl<br /> </td>
   <td>F</td>
   <td>タスクのサマリー URL が含まれます。<br /> </td>
  </tr>
  <tr>
   <td>taskACL<br /> </td>
   <td>F</td>
   <td>タスクのアクセス制御リストです。<br /> </td>
  </tr>
  <tr>
   <td>taskId<br /> </td>
   <td>F</td>
   <td>タスクの ID。<br /> </td>
  </tr>
  <tr>
   <td>updateTime<br /> </td>
   <td>F</td>
   <td>タスクが最後に更新された時間のタイムスタンプ。<br /> </td>
  </tr>
  <tr>
   <td>formUrl<br /> </td>
   <td>T</td>
   <td>タスクのフォームの URL が含まれます。<br /> </td>
  </tr>
  <tr>
   <td>taskFormType<br /> </td>
   <td>T</td>
   <td>タスクのフォームタイプが含まれます。このフィールドを使用して、タスクはクライアントで PDF フォーム、SWF フォームなどにレンダリングされます。<br /> </td>
  </tr>
  <tr>
   <td>showDirectActions<br /> </td>
   <td>T</td>
   <td>true の場合、ルートアクションは Workspace に表示されます。<br /> </td>
  </tr>
  <tr>
   <td>showACLActions<br /> </td>
   <td>T</td>
   <td>true の場合、転送、問い合わせ、共有などのアクションは Workspace に表示されます。<br /> </td>
  </tr>
  <tr>
   <td>supportsOffline<br /> </td>
   <td>T</td>
   <td>true の場合、フォームはオフラインにすることができます。これは、PDF フォームのみです。<br /> </td>
  </tr>
  <tr>
   <td>supportsSave<br /> </td>
   <td>T</td>
   <td>true の場合、ユーザーはタスクを保存できます。<br /> </td>
  </tr>
  <tr>
   <td>readerSubmitOptions<br /> </td>
   <td>T</td>
   <td>このオブジェクトには、PDF フォームに送信ボタンがない場合はリーダー経由で PDF フォームを送信できるオプションが含まれます。<br /> </td>
  </tr>
  <tr>
   <td>isDefaultImage<br /> </td>
   <td>T</td>
   <td>プロセスに指定されたイメージがあるかどうかを示します。プロセスに関連付けられたイメージがない場合は true、ある場合は false です。<br /> </td>
  </tr>
  <tr>
   <td>historyTaskList<br /> </td>
   <td>T</td>
   <td>タスクの詳細の「履歴」タブに使用されるタスクのリストが含まれます。<br /> </td>
  </tr>
  <tr>
   <td>isOwner<br /> </td>
   <td>T</td>
   <td>ログインしたユーザーがタスクの所有者である場合は true です。<br /> </td>
  </tr>
  <tr>
   <td>availableCommands<br /> </td>
   <td>T</td>
   <td>タスクで実行することができるすべてのアクションが含まれます。<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.directCommands<br /> </td>
   <td>T</td>
   <td>タスクで利用可能なすべてのルートアクションが含まれます。<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.taskACLCommands<br /> </td>
   <td>T</td>
   <td>転送、共有、問い合わせなどのタスクで利用できるコマンドが含まれます。<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.otherCommands<br /> </td>
   <td>T</td>
   <td>ロック、ロック解除、中断、返信、要求などの利用可能なコマンドが含まれます。<br /> </td>
  </tr>
  <tr>
   <td>processInstanceInfo<br /> </td>
   <td>T</td>
   <td>タスクのプロセスインスタンスに関する情報が含まれます。<br /> </td>
  </tr>
  <tr>
   <td>processVariables<br /> </td>
   <td>T<br /> </td>
   <td>プロセス変数のオブジェクトの配列が含まれます（存在する場合）。<br /> </td>
  </tr>
  <tr>
   <td>pendingTasks<br /> </td>
   <td>T</td>
   <td>タスクのプロセスインスタンスの保留中のタスクのリストが含まれます。<br /> </td>
  </tr>
  <tr>
   <td>userActions<br /> </td>
   <td>T</td>
   <td>オブジェクトの配列です。各オブジェクトにはルートに関する詳細および対応する確認メッセージが含まれます（存在する場合）。<br /> </td>
  </tr>
  <tr>
   <td>dataUrl<br /> </td>
   <td>T</td>
   <td>タスクのフォームのデータの URL です。<br /> </td>
  </tr>
  <tr>
   <td>externalAppConfig<br /> </td>
   <td>T</td>
   <td>サードパーティアプリケーションフォームの設定です。<br /> </td>
  </tr>
  <tr>
   <td>submitted<br /> </td>
   <td>T</td>
   <td>タスクが送信された場合は true です。<br /> </td>
  </tr>
  <tr>
   <td>attachments<br /> </td>
   <td>T</td>
   <td>タスクの添付ファイルのリスト。<br /> </td>
  </tr>
  <tr>
   <td>assignments<br /> </td>
   <td>T</td>
   <td>タスクの割り当てのリスト。<br /> </td>
  </tr>
 </tbody>
</table>

1. フィルター

   フィルターは基本的にユーザーまたはグループのキューです。タスクがユーザー / グループに割り当てられた場合、タスクは対応するキューに追加されます。

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ</strong></td>
   <td><strong>クライアントのみ</strong></td>
   <td><strong>コメント</strong></td>
  </tr>
  <tr>
   <td>isDefault <br type="_moz" /> </td>
   <td>F</td>
   <td>キューがログインしたユーザーのデフォルトのキューである場合は true で、それ以外の場合は false です。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>名前<br type="_moz" /> </td>
   <td>F</td>
   <td>キューの所有者の名前。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>qid</td>
   <td>F</td>
   <td>キューの ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>type</td>
   <td>F</td>
   <td>キューのタイプが含まれます。<br />0 - ユーザーキュー<br />1.共有キュー<br />2.グループキュー<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>query</td>
   <td>T</td>
   <td>フィルターに関連付けられたキューが含まれます。このクエリーを使用して完全なタスクリストからタスクを検索します。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>tasks</td>
   <td>T</td>
   <td>フィルターに属するすべてのタスクのリストが含まれます。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 不在

   不在スケジュールを管理して不在時に割り当てられたタスクのフローを制御することができます。

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ</strong><br type="_moz" /> </td>
   <td><strong>クライアントのみ</strong><br type="_moz" /> </td>
   <td><strong>コメント</strong><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>dateRanges<br type="_moz" /> </td>
   <td>F</td>
   <td>ユーザーの不在スケジュールの配列オブジェクトが含まれます。各スケジュールオブジェクトでは、startDateフィールドにスケジュールの開始日が含まれ、endDateフィールドにはスケジュールの終了日が含まれます。 If endDate is null in schedule, it implies that user has not scheduled the end date of out-of-office schedule.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isNoPrimaryDesignate<br type="_moz" /> </td>
   <td>F</td>
   <td>ユーザーが不在の場合の主要連絡先が指定されていない場合は true です。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isOutOfOffice<br type="_moz" /> </td>
   <td>F</td>
   <td>ユーザーが不在の場合は true です。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>outOfOfficeDesignate<br type="_moz" /> </td>
   <td>F</td>
   <td>ユーザーによって主要連絡先として指定されたユーザーの詳細が含まれます。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processSpecificDesignates<br type="_moz" /> </td>
   <td>F</td>
   <td>プロセス固有の不在時の連絡先のオブジェクトの配列が含まれます。In each process-specific designate object, processName contains the name of the process, isNotDesignated is true if no user is assigned for corresponding process, and userDesignated is null if no user assigned else details of the user assigned for corresponding process.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processes<br type="_moz" /> </td>
   <td>T</td>
   <td>ユーザーが利用できるすべてのプロセスのリストが含まれます。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>initialOutOfOfficeSettings<br type="_moz" /> </td>
   <td>T</td>
   <td>最初に取得したユーザーの不在時の初期設定が含まれます。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>outOfOfficeSettings<br type="_moz" /> </td>
   <td>T</td>
   <td>変更された不在時の設定が含まれます。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>userSearchHistory<br type="_moz" /> </td>
   <td>T</td>
   <td>日付までにログインしたユーザーによって検索されたユーザーのリストが含まれます。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. プロセスインスタンス

   プロセスインスタンスは、プロセスが Workspace または Workbench 経由で呼び出された場合に作成されます。

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ</strong></td>
   <td><strong>クライアントのみ</strong></td>
   <td><strong>コメント</strong></td>
  </tr>
  <tr>
   <td>description<br type="_moz" /> </td>
   <td>F</td>
   <td>プロセスインスタンスの説明<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>initiator</td>
   <td>F</td>
   <td>プロセスインスタンスのイニシエーターの名前。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>initiatorId</td>
   <td>F</td>
   <td>プロセスインスタンスのイニシエーターの ID.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processCompleteTime<br type="_moz" /> </td>
   <td>F</td>
   <td>プロセスが完了したときのタイムスタンプ。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceId<br type="_moz" /> </td>
   <td>F</td>
   <td>プロセスインスタンスの ID.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceStatus<br type="_moz" /> </td>
   <td>F</td>
   <td>0 = 起動済み<br /> 1 = 実行中<br /> 2 = 完了<br /> 3 = 完了中<br /> 4 = 終了<br /> 5 = 終了中<br /> 6 = 休止<br /> 7 = 休止中<br /> 8 = 休止解除中<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processName<br type="_moz" /> </td>
   <td>F</td>
   <td>プロセスの名前。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processStartTime<br type="_moz" /> </td>
   <td>F</td>
   <td>プロセスが開始したときのタイムスタンプ。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processVariables<br type="_moz" /> </td>
   <td>F</td>
   <td>プロセス変数のオブジェクトの配列。Each process variable object contains name which is name of process variable, value which is value of process variable and type which is type of process variable.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>tasklist<br type="_moz" /> </td>
   <td>T</td>
   <td>このプロセスインスタンスによって生成されたタスク。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. プロセス名

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ</strong></td>
   <td><strong>クライアントのみ</strong></td>
   <td><strong>コメント</strong></td>
  </tr>
  <tr>
   <td>processMajorVersion<br type="_moz" /> </td>
   <td>F</td>
   <td>プロセスのメジャーバージョン。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processMinorVersion<br type="_moz" /> </td>
   <td>F</td>
   <td>プロセスのマイナーバージョン。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processName<br type="_moz" /> </td>
   <td>F</td>
   <td>プロセスの名前。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processTitle<br type="_moz" /> </td>
   <td>F</td>
   <td>プロセスのタイトル。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceList<br type="_moz" /> </td>
   <td>T</td>
   <td>このプロセスのプロセスインスタンスのリスト。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. タスクの割り当てオブジェクト

   タスクの割り当てオブジェクトには、タスクの割り当てに関する情報が含まれます。以下にタスクの割り当てのプロパティを示します。

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ</strong></td>
   <td><strong>クライアントのみ</strong></td>
   <td><strong>コメント</strong></td>
  </tr>
  <tr>
   <td>assignmentCreateTime<br type="_moz" /> </td>
   <td>F</td>
   <td>このタスクの割り当てが作成されたときのタイムスタンプ。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>assignmentType<br type="_moz" /> </td>
   <td>F</td>
   <td>0 = 初期割り当て<br /> 1 = 転送（タスクはタスクの現在の所有者に転送されました）<br />2 = 返信（タスクはタスクの以前の所有者によってタスクの現在の所有者に返信されました。）<br />3 = 要求済み（タスクは現在のタスクの所有者によって要求されました）<br />4 = エスカレーション（タスクはエスカレーション後に現在のタスクの所有者に割り当てられました。）<br />5 = 割り当てられている管理者（タスクは現在のタスクの所有者に管理者によって割り当てられました）<br />6 = 問い合わせ済み（タスクはタスクの現在の所有者に問い合わせされました）<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>assignmentUpdateTime<br type="_moz" /> </td>
   <td>F</td>
   <td>このタスクの割り当てが更新されたときのタイムスタンプ。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueId<br type="_moz" /> </td>
   <td>F</td>
   <td>タスクの現在の所有者のキューの ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueOwner<br type="_moz" /> </td>
   <td>F</td>
   <td>タスクの現在の所有者の名前。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>queueOwnerId<br type="_moz" /> </td>
   <td>F</td>
   <td>タスクの現在の所有者の ID。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. タスク ACL オブジェクト

   タスク ACL オブジェクトには、タスクの転送、共有、問い合わせなどの権限に関する情報が含まれます。以下にタスク ACL のプロパティを示します。

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ</strong></td>
   <td><strong>クライアントのみ</strong></td>
   <td><strong>コメント</strong></td>
  </tr>
  <tr>
   <td>canAddAttachments<br type="_moz" /> </td>
   <td>F</td>
   <td>true の場合はタスクに添付ファイルを追加することができます。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canAddNotes<br type="_moz" /> </td>
   <td>F</td>
   <td>true の場合はタスクにメモを追加することができます。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canClaim<br type="_moz" /> </td>
   <td>F</td>
   <td>true の場合はタスクを要求することができます。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canConsult<br type="_moz" /> </td>
   <td>F</td>
   <td>true の場合はタスクを問い合わせすることができます。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canForward<br type="_moz" /> </td>
   <td>F</td>
   <td>true の場合はタスクを転送することができます。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canShare<br type="_moz" /> </td>
   <td>F</td>
   <td>true の場合はタスクを共有することができます。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. タスクの添付ファイル

   添付ファイルをタスクに追加することができます。添付のタイプは添付ファイルおよびメモが可能です。以下に添付オブジェクトのプロパティを示します。

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ</strong></td>
   <td><strong>クライアントのみ</strong></td>
   <td><strong>コメント</strong></td>
  </tr>
  <tr>
   <td>creationDate<br type="_moz" /> </td>
   <td>F</td>
   <td>添付ファイルが作成されたときのタイムスタンプ。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>creatorId<br type="_moz" /> </td>
   <td>F</td>
   <td>添付ファイルに追加されたユーザーの ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>creatorName<br type="_moz" /> </td>
   <td>F</td>
   <td>添付ファイルを追加したユーザーの名前。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>description<br type="_moz" /> </td>
   <td>F</td>
   <td>添付ファイルの説明。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>fileName<br type="_moz" /> </td>
   <td>F</td>
   <td>添付ファイルの名前。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>id<br type="_moz" /> </td>
   <td>F</td>
   <td>添付ファイルの ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>lastModifiedDate<br type="_moz" /> </td>
   <td>F</td>
   <td>添付ファイルが最後に変更されたときのタイムスタンプ。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>noteExtended<br type="_moz" /> </td>
   <td>F</td>
   <td>true の場合はメモは拡張された（長い）メモです。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>権限<br type="_moz" /> </td>
   <td>F</td>
   <td>添付ファイルに関連付けられた権限。allowRead field is for read permission, allowWrite is for write permission, allowDelete is for delete permission.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>サイズ<br type="_moz" /> </td>
   <td>F</td>
   <td>添付ファイルのサイズ（バイト）。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>taskId<br type="_moz" /> </td>
   <td>F</td>
   <td>添付ファイルが追加されたタスクの ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>type<br type="_moz" /> </td>
   <td>F</td>
   <td>Type is attachment for files and Type is note for notes.<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedCreationDate<br type="_moz" /> </td>
   <td>T</td>
   <td>ユーザーの UI 設定に応じて添付ファイルの作成日が含まれます。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedDescription<br type="_moz" /> </td>
   <td>T</td>
   <td>書式設定された添付ファイルの説明。AEM Forms Workspace の添付ファイルの説明に存在する特殊文字を表示するのに使用されます。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedFileName<br type="_moz" /> </td>
   <td>T</td>
   <td>書式設定された添付ファイル名。AEM Forms Workspace の添付ファイルの名前に存在する特殊文字を表示するのに使用されます。これは、メモでのみ利用できます。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. ユーザー

   以下にユーザーオブジェクトのプロパティを示します。

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ</strong></td>
   <td><strong>クライアントのみ</strong></td>
   <td><strong>コメント</strong></td>
  </tr>
  <tr>
   <td>address<br type="_moz" /> </td>
   <td>F</td>
   <td>ユーザーのアドレス。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>commonName<br type="_moz" /> </td>
   <td>F</td>
   <td>ユーザーの共通名。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>description<br type="_moz" /> </td>
   <td>F</td>
   <td>ユーザーの説明。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>directGroupMemberships<br type="_moz" /> </td>
   <td>F</td>
   <td>ユーザーのグループのリスト。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>displayName<br type="_moz" /> </td>
   <td>F</td>
   <td>ユーザーの表示名。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>email<br type="_moz" /> </td>
   <td>F</td>
   <td>ユーザーの電子メール ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isOutOfOffice<br type="_moz" /> </td>
   <td>F</td>
   <td>ユーザーが不在の場合は true です。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>lastName<br type="_moz" /> </td>
   <td>F</td>
   <td>ユーザーの姓。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>firstName<br type="_moz" /> </td>
   <td>F</td>
   <td>ユーザーの名。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>oid<br type="_moz" /> </td>
   <td>F</td>
   <td>ユーザーの ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>org<br type="_moz" /> </td>
   <td>F</td>
   <td>ユーザーの組織の名前。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>postalAddress<br type="_moz" /> </td>
   <td>F</td>
   <td>ユーザーの住所。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>telephone<br type="_moz" /> </td>
   <td>F</td>
   <td>ユーザーの連絡先番号。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>telephoneNumber<br type="_moz" /> </td>
   <td>F</td>
   <td>ユーザーの連絡先番号。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>userid<br type="_moz" /> </td>
   <td>F</td>
   <td>ユーザーのログイン ID。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>
