---
title: AEM Forms Workspace JSON オブジェクトの詳細
description: カスタマイズ、拡張、変更、再利用のためにLiveCycleAEM Forms Workspace で使用される JSON JavaScript オブジェクトに関する概念情報です。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: f837a2b3-4650-4261-84c6-291bb2a46dc7
source-git-commit: 970e0a97d531d4cbae76119960972e54ef65dda0
workflow-type: tm+mt
source-wordcount: '2144'
ht-degree: 18%

---

# AEM Forms Workspace JSON オブジェクトの詳細 {#aem-forms-workspace-json-object-description}

AEM Forms Workspace で使用される JSON オブジェクトを以下に示します。

1. カテゴリ

   カテゴリは、ワークスペースの「開始プロセス」タブに表示されます。 これらのカテゴリは、スタートポイントを分類するために使用されます。

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ</strong></td>
   <td><strong>クライアントのみ</strong></td>
   <td><strong>コメント</strong></td>
  </tr>
  <tr>
   <td>name</td>
   <td>F</td>
   <td>カテゴリ名</td>
  </tr>
  <tr>
   <td>id</td>
   <td>F</td>
   <td>カテゴリ ID<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>説明<br type="_moz" /> </td>
   <td>F</td>
   <td>カテゴリの説明<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>parentOid<br type="_moz" /> </td>
   <td>F</td>
   <td>親カテゴリの OID を含む<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>startPointsList<br type="_moz" /> </td>
   <td>T</td>
   <td>カテゴリに存在するすべての開始点のリストが含まれます</td>
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
>すべてのスタートポイントとお気に入りは、クライアント側で定義されるカテゴリです。 お気に入りのカテゴリには、ユーザーがお気に入りに登録したすべての開始点が含まれます。 すべての開始点カテゴリには、すべての開始点が含まれます。

1. Startpoint

   開始点は、起動時にワークスペースからプロセスを開始するために使用されます。

   | **プロパティ** | **クライアントのみ** | **コメント** |
   |---|---|---|
   | categoryId | F | スタートポイントが属するカテゴリの ID が含まれます。 |
   | description | F | スタートポイントの説明が含まれます。 |
   | name | F | 開始点の名前が含まれます。 |
   | serializedImageTicket | F | スタートポイントに対応するイメージチケットが含まれます。このイメージチケットは、サーバーからスタートポイントのイメージを取得するために、スタートポイントの imageUrl フィールドで使用されます。 |
   | serviceName | F | スタートポイントのサービスの名前が含まれます。 |
   | startpointId | F | 開始点の ID が含まれます。 |
   | isFavorite | T | 開始点をお気に入りにするかどうかを示します。 開始点がお気に入りの場合は true、それ以外の場合は false です。 |
   | isDefaultImage | T | プロセスに対してイメージが指定されているかどうかを示します。 プロセスに画像が関連付けられていない場合は true 、それ以外の場合は false です。 |
   | タスク | T | スタートポイントの呼び出し時に作成されたタスクが含まれます。 |
   | imageUrl | T | 開始点に対応する画像の URL が含まれます。 |

1. タスク

   タスクはユーザー/グループに割り当てられ、データを入力できるユーザーインターフェイス ( フォームまたはガイド（非推奨）) が含まれます。 ユーザーにタスクが割り当てられると、完了して送信するためのフォームまたはガイドが提供されます。

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
   <td>タスクが lc8 タスクの場合、タスクのクラスは「LC8」です。それ以外の場合、「標準」です。<br /> </td>
  </tr>
  <tr>
   <td>completeTime<br /> </td>
   <td>F</td>
   <td>タスクが完了したときのタイムスタンプが含まれます。<br /> </td>
  </tr>
  <tr>
   <td>consultGroupId<br /> </td>
   <td>F</td>
   <td>タスクの問い合わせ先となるグループの ID が含まれます。 これは、プロセスの設計時に設定されます。<br /> </td>
  </tr>
  <tr>
   <td>createTime<br /> </td>
   <td>F</td>
   <td>タスクが作成されたときのタイムスタンプが含まれます。<br /> </td>
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
   <td>タスクが期限に達したときのタイムスタンプが含まれます。<br /> </td>
  </tr>
  <tr>
   <td>説明<br /> </td>
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
   <td>タスクを転送できるグループの ID が含まれます。 これは、プロセスの設計時に設定されます。<br /> </td>
  </tr>
  <tr>
   <td>instructions<br /> </td>
   <td>F</td>
   <td>タスクの手順が含まれます。<br /> </td>
  </tr>
  <tr>
   <td>isLocked<br /> </td>
   <td>F</td>
   <td>タスクがロックされている場合は True です。<br /> </td>
  </tr>
  <tr>
   <td>isMustOpenToComplete<br /> </td>
   <td>F</td>
   <td>True を指定すると、タスクを完了するためにタスクフォームを開く必要があります。<br /> </td>
  </tr>
  <tr>
   <td>isOpenFullScreen<br /> </td>
   <td>F</td>
   <td>true の場合、タスクを開くと、フォームは初めて完全な画面を取ります。<br /> </td>
  </tr>
  <tr>
   <td>isRouteSelectionRequired<br /> </td>
   <td>F</td>
   <td>true の場合、タスクを完了するにはルートを選択する必要があります。<br /> </td>
  </tr>
  <tr>
   <td>isShowAttachments<br /> </td>
   <td>F</td>
   <td>true の場合は添付ファイルが表示されます。<br /> </td>
  </tr>
  <tr>
   <td>isStartTask<br /> </td>
   <td>F</td>
   <td>true の場合、タスクは開始点から作成されます。<br /> </td>
  </tr>
  <tr>
   <td>isVisible<br /> </td>
   <td>F</td>
   <td>True を指定すると、タスクが Workspace に表示されます。<br /> </td>
  </tr>
  <tr>
   <td>nextReminder<br /> </td>
   <td>F</td>
   <td>次のリマインダーのタイムスタンプ。<br /> </td>
  </tr>
  <tr>
   <td>優先度<br /> </td>
   <td>F</td>
   <td>タスクの優先度が含まれます。<br /> 1 =最も優先度が高い<br /> 2 =優先度（高）<br /> 3 =標準の優先度<br /> 4 =低い優先度<br /> 5 =最も低い優先度<br /> </td>
  </tr>
  <tr>
   <td>processInstanceId</td>
   <td>F</td>
   <td>タスクが含まれるプロセスインスタンスの ID。<br /> </td>
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
   <td>タスクに関連付けられたルートのリストが含まれます。 ユーザーは、ルートリストから任意のルートを選択することで、タスクを完了できます。<br /> </td>
  </tr>
  <tr>
   <td>selectedRoute<br /> </td>
   <td>F</td>
   <td>タスクが完了したときに選択したルートの名前が含まれます。<br /> </td>
  </tr>
  <tr>
   <td>serializedImageTicket<br /> </td>
   <td>F</td>
   <td>タスクに対応する画像チケットが含まれます。 この画像チケットは、サーバーからタスクの画像を取得するために、タスクの imageUrl フィールドで使用されます。<br /> <br /> </td>
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
   <td>1 =作成済み（タスクは開始点から作成されます。）<br /> 2 =作成して保存済み（タスクは開始点から作成されて保存されました。）<br /> 3 =割り当て済み（タスクはプロセスの開始後にユーザーに割り当てられます）<br /> 4 =割り当てて保存済み（タスクは割り当てられ、保存されました。）<br /> 100 =完了（タスクは完了しました。）<br /> 101 =期限切れ（タスクは期限切れになりました。）<br /> 102 =終了<br /> </td>
  </tr>
  <tr>
   <td>stepName<br /> </td>
   <td>F</td>
   <td>プロセスの設計中に設定されたタスクの名前が含まれます。<br /> </td>
  </tr>
  <tr>
   <td>summaryUrl<br /> </td>
   <td>F</td>
   <td>タスクの概要 URL が含まれます。<br /> </td>
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
   <td>タスクが最後に更新されたときのタイムスタンプ。<br /> </td>
  </tr>
  <tr>
   <td>formUrl<br /> </td>
   <td>T</td>
   <td>タスクのフォームの URL が含まれます。<br /> </td>
  </tr>
  <tr>
   <td>taskFormType<br /> </td>
   <td>T</td>
   <td>タスクフォームタイプが含まれます。 このフィールドを使用すると、タスクはクライアント上で pdf（SWF フォームなど）としてレンダリングされます。<br /> </td>
  </tr>
  <tr>
   <td>showDirectActions<br /> </td>
   <td>T</td>
   <td>true の場合、ルートアクションは Workspace に表示されます。<br /> </td>
  </tr>
  <tr>
   <td>showACLActions<br /> </td>
   <td>T</td>
   <td>true の場合、forward、consult、share などのアクションが Workspace に表示されます。<br /> </td>
  </tr>
  <tr>
   <td>supportsOffline<br /> </td>
   <td>T</td>
   <td>true の場合、フォームはオフラインにできます。 これは、PDF フォームに対してのみ使用されます。<br /> </td>
  </tr>
  <tr>
   <td>supportsSave<br /> </td>
   <td>T</td>
   <td>true の場合、ユーザーはタスクを保存できます。<br /> </td>
  </tr>
  <tr>
   <td>readerSubmitOptions<br /> </td>
   <td>T</td>
   <td>このオブジェクトには、PDF フォームに送信ボタンがない場合に Reader で PDF フォームを送信するためのオプションが含まれています。<br /> </td>
  </tr>
  <tr>
   <td>isDefaultImage<br /> </td>
   <td>T</td>
   <td>プロセスに対してイメージが指定されているかどうかを示します。 プロセスに画像が関連付けられていない場合は true 、それ以外の場合は false です。<br /> </td>
  </tr>
  <tr>
   <td>historyTaskList<br /> </td>
   <td>T</td>
   <td>タスクの詳細の「履歴」タブで使用されるタスクのリストが含まれます。<br /> </td>
  </tr>
  <tr>
   <td>isOwner<br /> </td>
   <td>T</td>
   <td>ログインしたユーザーがタスクの所有者である場合は True です。<br /> </td>
  </tr>
  <tr>
   <td>availableCommands<br /> </td>
   <td>T</td>
   <td>タスクに対して実行できるすべてのアクションが含まれます。<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.directCommands<br /> </td>
   <td>T</td>
   <td>タスクで使用可能なすべてのルートアクションが含まれます。<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.taskACLCommands<br /> </td>
   <td>T</td>
   <td>タスクに対して forward、share、consult などのコマンドが含まれます。<br /> </td>
  </tr>
  <tr>
   <td>availableCommands.otherCommands<br /> </td>
   <td>T</td>
   <td>ロック、ロック解除、放棄、返却、要求などのコマンドが使用可能になっています。<br /> </td>
  </tr>
  <tr>
   <td>processInstanceInfo<br /> </td>
   <td>T</td>
   <td>タスクのプロセスインスタンスに関する情報が含まれます。<br /> </td>
  </tr>
  <tr>
   <td>processVariables<br /> </td>
   <td>T<br /> </td>
   <td>プロセス変数（存在する場合）のオブジェクトの配列が含まれます。<br /> </td>
  </tr>
  <tr>
   <td>pendingTasks<br /> </td>
   <td>T</td>
   <td>タスクのプロセスインスタンスの保留中のタスクのリストが含まれます。<br /> </td>
  </tr>
  <tr>
   <td>userActions<br /> </td>
   <td>T</td>
   <td>これはオブジェクトの配列です。 各オブジェクトには、ルートに関する詳細と、対応する確認メッセージ（存在する場合）が含まれます。<br /> </td>
  </tr>
  <tr>
   <td>dataUrl<br /> </td>
   <td>T</td>
   <td>タスクのフォームのデータの URL です。<br /> </td>
  </tr>
  <tr>
   <td>externalAppConfig<br /> </td>
   <td>T</td>
   <td>これは、サードパーティのアプリケーションフォームの設定です。<br /> </td>
  </tr>
  <tr>
   <td>送信済み<br /> </td>
   <td>T</td>
   <td>タスクが送信された場合は True です。<br /> </td>
  </tr>
  <tr>
   <td>attachments<br /> </td>
   <td>T</td>
   <td>タスクの添付ファイルのリスト。<br /> </td>
  </tr>
  <tr>
   <td>割り当て<br /> </td>
   <td>T</td>
   <td>タスクの割り当てのリスト。<br /> </td>
  </tr>
 </tbody>
</table>

1. フィルター

   フィルターは基本的にユーザーまたはグループのキューです。 タスクがユーザーまたはグループに割り当てられると、対応するキューにタスクが追加されます。

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
   <td>キューがログインユーザーのデフォルトのキューの場合は true、そうでない場合は false です。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>name<br type="_moz" /> </td>
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
   <td>キューのタイプが含まれます。<br /> 0 — ユーザーキュー。<br />1.共有キュー.<br />2.グループキュー。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>query</td>
   <td>T</td>
   <td>フィルターに関連付けられたクエリが含まれます。 このクエリは、完全なタスクリストからタスクを検索するために使用されます。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>タスク</td>
   <td>T</td>
   <td>フィルターに属するすべてのタスクのリストが含まれます。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. 不在

   不在スケジュールを管理し、不在時に割り当てられたタスクのフローを制御できます。

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
   <td>ユーザーの不在スケジュールの配列オブジェクトが含まれます。 各スケジュールオブジェクトには、startDate フィールドにスケジュールの開始日、endDate フィールドにスケジュールの終了日が含まれます。スケジュールの endDate が null の場合は、ユーザーが不在スケジュールの終了日をスケジュールしていないことを意味します。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isNoPrimaryDesignate<br type="_moz" /> </td>
   <td>F</td>
   <td>ユーザーが不在の場合に主な指定がない場合は true です。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>isOutOfOffice<br type="_moz" /> </td>
   <td>F</td>
   <td>ユーザーが不在の場合は true です。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>outOfOfficeDesignate<br type="_moz" /> </td>
   <td>F</td>
   <td>ユーザーによってプライマリ指定として割り当てられたユーザーの詳細が含まれます。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processSpecificDesignates<br type="_moz" /> </td>
   <td>F</td>
   <td>プロセス固有の不在時の指定用のオブジェクトの配列が含まれます。 各プロセス固有の指定のオブジェクトには、processName （プロセスの名前）、 isNotDesignated （ユーザーが対応するプロセスに割り当てられていない場合は true）、および userDesignated （ユーザーが割り当てられていない場合はヌルで、割り当てられている場合は対応するプロセスに割り当てられたユーザーの詳細）が含まれます。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>プロセス<br type="_moz" /> </td>
   <td>T</td>
   <td>ユーザーが使用できるすべてのプロセスのリストが含まれます。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>initialOutOfOfficeSettings<br type="_moz" /> </td>
   <td>T</td>
   <td>最初に取得されたユーザーの不在時の初期設定が含まれます。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>outOfOfficeSettings<br type="_moz" /> </td>
   <td>T</td>
   <td>変更された不在時の設定が含まれます。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>userSearchHistory<br type="_moz" /> </td>
   <td>T</td>
   <td>ログインしたユーザーが日付まで検索したユーザーのリストが含まれます。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. プロセスインスタンス

   プロセスインスタンスは、プロセスが workspace または workbench を介して呼び出されると作成されます。

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ</strong></td>
   <td><strong>クライアントのみ</strong></td>
   <td><strong>コメント</strong></td>
  </tr>
  <tr>
   <td>説明<br type="_moz" /> </td>
   <td>F</td>
   <td>プロセスインスタンスの説明<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>イニシエーター</td>
   <td>F</td>
   <td>プロセスインスタンスのイニシエーターの名前。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>initiatorId</td>
   <td>F</td>
   <td>プロセスインスタンスのイニシエーターの ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processCompleteTime<br type="_moz" /> </td>
   <td>F</td>
   <td>処理が完了したときのタイムスタンプ。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceId<br type="_moz" /> </td>
   <td>F</td>
   <td>プロセスインスタンスの ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>processInstanceStatus<br type="_moz" /> </td>
   <td>F</td>
   <td>0 =開始済み<br /> 1 =実行中<br /> 2 =完了<br /> 3 =完了中<br /> 4 =終了<br /> 5 =終了中<br /> 6 =中断<br /> 7 =休止中<br /> 8 =休止解除中<br type="_moz" /> </td>
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
   <td>プロセス変数のオブジェクトの配列。 各プロセス変数オブジェクトは、name（プロセス変数の名前）、value（プロセス変数の値）、type（プロセス変数のタイプ）を含みます。<br type="_moz" /> </td>
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

1. タスク割り当てオブジェクト

   タスクの割り当てオブジェクトには、タスクの割り当てに関する情報が含まれます。 次に、タスクの割り当てのプロパティを示します。

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
   <td>タスクのこの割り当てが作成されたときのタイムスタンプ。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>assignmentType<br type="_moz" /> </td>
   <td>F</td>
   <td>0 =初期割り当て<br /> 1 =転送（タスクはタスクの現在の所有者に転送されました。）<br /> 2 =返されました（タスクは、タスクの前の所有者によってタスクの現在の所有者に返されました。）<br /> 3 =要求済み（タスクは現在のタスクの所有者によって要求されました。）<br /> 4 =エスカレーション（タスクはエスカレーション後に現在のタスクの所有者に割り当てられました。）<br /> 5 =管理者の割り当て（タスクは管理者によって現在のタスク所有者に割り当てられました。）<br /> 6 =問い合わせ済み（タスクは現在のタスク所有者に問い合わせ済みです。）<br type="_moz" /> </td>
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

   タスク ACL オブジェクトには、タスクの転送、共有、問い合わせなどの権限に関する情報が含まれます。 次に、タスクの ACL のプロパティを示します。

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
   <td>true の場合、タスクに添付ファイルを追加できます。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canAddNotes<br type="_moz" /> </td>
   <td>F</td>
   <td>true の場合は、タスクにメモを追加できます。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canClaim<br type="_moz" /> </td>
   <td>F</td>
   <td>true の場合は、タスクを要求できます。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canConsult<br type="_moz" /> </td>
   <td>F</td>
   <td>true の場合は、タスクを問い合わせることができます。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canForward<br type="_moz" /> </td>
   <td>F</td>
   <td>true の場合は、タスクを転送できます。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>canShare<br type="_moz" /> </td>
   <td>F</td>
   <td>true の場合は、タスクを共有できます。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. タスクの添付ファイル

   タスクに添付ファイルを追加できます。 添付ファイルのタイプは添付ファイルとメモにすることができます。 次に、attachment オブジェクトのプロパティを示します。

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
   <td>添付ファイルを追加したユーザーの ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>creatorName<br type="_moz" /> </td>
   <td>F</td>
   <td>添付ファイルを追加したユーザーの名前。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>説明<br type="_moz" /> </td>
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
   <td>true の場合、メモは拡張（長い）メモです。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>権限<br type="_moz" /> </td>
   <td>F</td>
   <td>添付ファイルに関連付けられた権限。allowRead フィールドは読み取り権限、allowWrite は書き込み権限、allowDelete は削除権限用です。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>サイズ<br type="_moz" /> </td>
   <td>F</td>
   <td>添付ファイルのサイズ（バイト単位）。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>taskId<br type="_moz" /> </td>
   <td>F</td>
   <td>添付ファイルを追加するタスクの ID。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>type<br type="_moz" /> </td>
   <td>F</td>
   <td>タイプは、ファイルの場合は attachment で、メモの場合は note です。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedCreationDate<br type="_moz" /> </td>
   <td>T</td>
   <td>ユーザーの UI 設定に応じて添付ファイルの作成日が含まれます。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedDescription<br type="_moz" /> </td>
   <td>T</td>
   <td>書式付き添付ファイルの説明。 AEM Forms Workspace の添付ファイルの説明に存在する特殊文字を表示するために使用します。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>formattedFileName<br type="_moz" /> </td>
   <td>T</td>
   <td>書式付き添付ファイル名。 AEM Forms Workspace の添付ファイル名に存在する特殊文字を表示するために使用されます。 これはメモ用です。<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

1. User

   次に、user オブジェクトのプロパティを示します。

<table>
 <tbody>
  <tr>
   <td><strong>プロパティ</strong></td>
   <td><strong>クライアントのみ</strong></td>
   <td><strong>コメント</strong></td>
  </tr>
  <tr>
   <td>住所<br type="_moz" /> </td>
   <td>F</td>
   <td>ユーザーのアドレス。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>commonName<br type="_moz" /> </td>
   <td>F</td>
   <td>ユーザーの共通名。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>説明<br type="_moz" /> </td>
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
   <td>ユーザーの郵送先住所。<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>電話<br type="_moz" /> </td>
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
