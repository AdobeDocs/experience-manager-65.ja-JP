---
title: 再利用可能なコンポーネントの説明
description: AEM Forms Workspace コンポーネントを web アプリケーション内に統合するために役立つ、再利用可能なコンポーネントの完全リスト（ファイル名と依存関係）。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: b8cb7233-3d9e-41d4-85c5-8e8c2481f89c
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '1231'
ht-degree: 100%

---

# 再利用可能なコンポーネントの説明 {#description-of-reusable-components}

AEM Forms Workspace は、[再利用可能な](/help/forms/using/integrating-html-ws-components-web.md)コンポーネントで構成されており、これらのコンポーネントは CRX™ 内の固有の[フォルダー構造](/help/forms/using/folder-structure.md)内に整理されています。各コンポーネントには、フォルダー構造内の指定場所にあるモデル、表示、テンプレートファイル、他のコンポーネントファイルの JavaScript™ 依存関係、コンポーネントがリッスンするイベント、および AEM Forms Workspace 内でこれらのイベントをトリガーする JavaScript オブジェクトがあります。再利用可能なコンポーネントの完全なリストを、それらの構成ファイル名と依存関係と共に、以下に示します。

## TaskList {#tasklist}

<table>
 <tbody>
  <tr>
   <td><p>モデル</p></td>
   <td><p>tasklist.js</p></td>
  </tr>
  <tr>
   <td><p>表示</p></td>
   <td><p>tasklist.js</p></td>
  </tr>
  <tr>
   <td><p>テンプレート</p></td>
   <td><p>tasklist.html</p></td>
  </tr>
  <tr>
   <td><p>コンポーネントが必要</p></td>
   <td>
    <ul>
     <li><p>UserSearch</p></li>
     <li><p>タスク</p></li>
     <li><p>Teamtask</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>JS の依存関係</p></td>
   <td>
    <ul>
     <li><p>タスクモデル</p></li>
     <li><p>teamtask モデル</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>リスンされているイベント（イベント名 – トリガー）</p></td>
   <td>
    <ul>
     <li><p>filterSelected - tasklist モデル</p></li>
     <li><p>削除 - tasklist モデル</p></li>
     <li><p>updateQueue - tasklist モデル</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>カスタムアプリケーションからこのコンポーネントの filterSelected イベントをトリガーする場合、このコンポーネントは AEM Forms ワークスペースとは独立して使用できます。

## タスク {#task}

<table>
 <tbody>
  <tr>
   <td><p>モデル</p></td>
   <td><p>task.js</p></td>
  </tr>
  <tr>
   <td><p>表示</p></td>
   <td><p>task.js</p></td>
  </tr>
  <tr>
   <td><p>テンプレート</p></td>
   <td><p>task.html</p></td>
  </tr>
  <tr>
   <td><p>コンポーネントが必要</p></td>
   <td><p>該当なし</p></td>
  </tr>
  <tr>
   <td><p>JS の依存関係</p></td>
   <td>
    <ul>
     <li><p>tasklist モデル</p></li>
     <li><p>taskactions ユーティリティ</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>リスンされているイベント（イベント名 – トリガー）</p></td>
   <td>
    <ul>
     <li><p>submitComplete - タスクモデル</p></li>
     <li><p>却下 - タスクモデル</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Workspace は、TaskList モデルの fetchTask 関数を呼び出して、このコンポーネントのタスクモデルを作成します。

## FilterList {#filterlist}

<table>
 <tbody>
  <tr>
   <td><p>モデル</p></td>
   <td><p>tasklist.js</p></td>
  </tr>
  <tr>
   <td><p>表示</p></td>
   <td><p>filterlist.js</p></td>
  </tr>
  <tr>
   <td><p>テンプレート</p></td>
   <td><p>filterlist.html</p></td>
  </tr>
  <tr>
   <td><p>コンポーネントが必要</p></td>
   <td><p>該当なし</p></td>
  </tr>
  <tr>
   <td><p>JS の依存関係</p></td>
   <td><p>該当なし</p></td>
  </tr>
  <tr>
   <td><p>リスンされているイベント（イベント名 – トリガー）</p></td>
   <td>
    <ul>
     <li><p>取得済み - tasklist モデル </p></li>
     <li><p>削除 - tasklist モデル </p></li>
     <li><p>updateQueue - tasklist モデル </p></li>
     <li><p>refreshedQueue - tasklist モデル </p></li>
     <li><p>filterSelected - tasklist モデル</p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

## フィルター {#filter}

<table>
 <tbody>
  <tr>
   <td><p>表示</p> </td>
   <td><p>filter.js</p> </td>
  </tr>
  <tr>
   <td><p>テンプレート</p> </td>
   <td><p>filter.html</p> </td>
  </tr>
  <tr>
   <td><p>コンポーネントが必要</p> </td>
   <td><p>該当なし</p> </td>
  </tr>
  <tr>
   <td><p>JS の依存関係</p> </td>
   <td>
    <ul>
     <li><p>フィールド：キュー：{ name, qid, isDefault, type}</p> </li>
     <li><p>フィールド：クエリ：文字列</p> </li>
     <li><p>フィールド：parentView：filterlist ビュー</p> </li>
     <li><p>フィールド：parentModel：tasklist モデル</p> </li>
     <li><p>フィールド：ユーティリティ</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>リッスンされているイベント</p> </td>
   <td><p>該当なし</p> </td>
  </tr>
 </tbody>
</table>

## TeamQueues {#teamqueues}

<table>
 <tbody>
  <tr>
   <td><p>モデル</p></td>
   <td><p>tasklist.js</p></td>
  </tr>
  <tr>
   <td><p>表示</p></td>
   <td><p>teamqueues.js</p></td>
  </tr>
  <tr>
   <td><p>テンプレート</p></td>
   <td><p>teamqueues.html</p></td>
  </tr>
  <tr>
   <td><p>コンポーネントが必要</p></td>
   <td><p>該当なし</p></td>
  </tr>
  <tr>
   <td><p>JS の依存関係</p></td>
   <td><p>該当なし</p></td>
  </tr>
  <tr>
   <td><p>リスンされているイベント（イベント名 – トリガー）</p></td>
   <td>
    <ul>
     <li><p>取得済み - tasklist モデル </p></li>
     <li><p>削除 - tasklist モデル </p></li>
     <li><p>updateQueue - tasklist モデル </p></li>
     <li><p>teamQueuesFetched - tasklist モデル </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

## TeamFilter {#teamfilter}

<table>
 <tbody>
  <tr>
   <td><p>モデル</p> </td>
   <td><p>該当なし</p> </td>
  </tr>
  <tr>
   <td><p>表示</p> </td>
   <td><p>teamfilter.js</p> </td>
  </tr>
  <tr>
   <td><p>テンプレート</p> </td>
   <td><p>teamfilter.html</p> </td>
  </tr>
  <tr>
   <td><p>コンポーネントが必要</p> </td>
   <td><p>該当なし</p> </td>
  </tr>
  <tr>
   <td><p>JS の依存関係</p> </td>
   <td>
    <ul>
     <li><p>拡張：フィルタービュー</p> </li>
     <li><p>フィールド：キュー：{ name, qid, isDefault, type }</p> </li>
     <li><p>フィールド：クエリ：文字列</p> </li>
     <li><p>フィールド：parentView：filterlist ビュー</p> </li>
     <li><p>フィールド：parentModel：tasklist モデル</p> </li>
     <li><p>フィールド：ユーティリティ</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>リッスンされているイベント</p> </td>
   <td><p>該当なし</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>TeamFilter は、TaskList コンポーネントから選択されているタスクを示すイベントを取得します。これらのコンポーネントはモデルクラスを共有しますが、依存関係はありません。

## TaskDetails {#taskdetails}

<table>
 <tbody>
  <tr>
   <td><p>モデル</p> </td>
   <td><p>tasklist.js</p> </td>
  </tr>
  <tr>
   <td><p>表示</p> </td>
   <td><p>taskdetails.js</p> </td>
  </tr>
  <tr>
   <td><p>テンプレート</p> </td>
   <td><p>taskdetails.html</p> </td>
  </tr>
  <tr>
   <td><p>コンポーネントが必要</p> </td>
   <td><p>ほとんどのユーティリティクラス</p> </td>
  </tr>
  <tr>
   <td><p>JS の依存関係</p> </td>
   <td>
    <ul>
     <li><p>processinstancehistory.html</p> </li>
     <li><p>formrendering ユーティリティ</p> </li>
     <li><p>ノートユーティリティ</p> </li>
     <li><p>添付ユーティリティ</p> </li>
     <li><p>taskactions ユーティリティ</p> </li>
     <li><p>履歴ユーティリティ</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>リスンされているイベント（イベント名 – トリガー）</p> </td>
   <td>
    <ul>
     <li><p>転送済み - タスクモデル</p> </li>
     <li><p>共有済み - タスクモデル</p> </li>
     <li><p>問い合わせ済み - タスクモデル</p> </li>
     <li><p>拒否済み - タスクモデル</p> </li>
     <li><p>中止済み - タスクモデル</p> </li>
     <li><p>ロック解除済み - タスクモデル</p> </li>
     <li><p>ロック済み - タスクモデル</p> </li>
     <li><p>要求済み - タスクモデル</p> </li>
     <li><p>change:taskselected - tasklist モデル</p> </li>
     <li><p>change:formUrl - タスクモデル</p> </li>
     <li>attachmentURLFetched - タスクモデル</li>
    </ul>
    <ul>
     <li>newAttachment - タスクモデル</li>
     <li><p>taskHistoryFetched - タスクモデル</p> </li>
     <li>prepareForSubmitComplete - タスクモデル</li>
     <li><p>submitComplete - タスクモデル</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## CategoryList {#categorylist}

<table>
 <tbody>
  <tr>
   <td><p>モデル</p></td>
   <td><p>categorylist.js</p></td>
  </tr>
  <tr>
   <td><p>表示</p></td>
   <td><p>categorylist.js</p></td>
  </tr>
  <tr>
   <td><p>テンプレート</p></td>
   <td><p>startprocess.html（ルートフォルダー内）</p></td>
  </tr>
  <tr>
   <td><p>コンポーネントが必要</p></td>
   <td><p>カテゴリ</p></td>
  </tr>
  <tr>
   <td><p>JS の依存関係</p></td>
   <td>
    <ul>
     <li><p>favoritecategoryfactory モデル</p></li>
     <li><p>allcategoryfactory モデル</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>リスンされているイベント（イベント名 – トリガー）</p></td>
   <td>
    <ul>
     <li><p>allStartpointsFetched - categorylist モデル </p></li>
     <li><p>追加 - categorylist モデル </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>このコンポーネントは、StartPointList、StartPoint、Task など、他の一部のコンポーネントのモデルクラスを使用します。この依存関係以外に、CategoryList を独立して使用することもできます。

## カテゴリ {#category}

<table>
 <tbody>
  <tr>
   <td><p>モデル</p></td>
   <td><p>category.js</p></td>
  </tr>
  <tr>
   <td><p>表示</p></td>
   <td><p>category.js</p></td>
  </tr>
  <tr>
   <td><p>テンプレート</p></td>
   <td><p>category.html</p></td>
  </tr>
  <tr>
   <td><p>コンポーネントが必要</p></td>
   <td><p>該当なし</p></td>
  </tr>
  <tr>
   <td><p>JS の依存関係</p></td>
   <td>
    <ul>
     <li><p>categorylist モデル</p></li>
     <li><p>startpointlist モデル</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>リスンされているイベント（イベント名 – トリガー）</p></td>
   <td>
    <ul>
     <li><p>変更済み - カテゴリモデル </p></li>
     <li><p>childrenFetched - カテゴリモデル </p></li>
     <li><p>category:selected - categorylist モデル </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

## StartPointList {#startpointlist}

<table>
 <tbody>
  <tr>
   <td><p>モデル</p></td>
   <td><p>categorylist.js</p></td>
  </tr>
  <tr>
   <td><p>表示</p></td>
   <td><p>startpointlist.js</p></td>
  </tr>
  <tr>
   <td><p>テンプレート</p></td>
   <td><p>startprocess.html（ルートフォルダー内）</p></td>
  </tr>
  <tr>
   <td><p>コンポーネントが必要</p></td>
   <td><p>該当なし</p></td>
  </tr>
  <tr>
   <td><p>JS の依存関係</p></td>
   <td>
    <ul>
     <li><p>カテゴリモデル</p></li>
     <li><p>favoritecategoryfactory モデル</p></li>
     <li><p>allcategoryfactory モデル</p></li>
     <li><p>startpoint ビュー</p></li>
     <li><p>startpointlist モデル</p></li>
     <li><p>startpoint モデル</p></li>
     <li><p>タスクモデル</p></li>
     <li><p>タスクモデル</p></li>
     <li><p>tasklist モデル</p></li>
     <li><p>teamtask モデル</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>リスンされているイベント（イベント名 – トリガー）</p></td>
   <td>
    <ul>
     <li><p>category:selected - categorylist モデル </p></li>
     <li><p>allStartpointsFetched - categorylist モデル </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>StartPointList と CategoryList コンポーネントはモデルクラスを共有するため、前者は後者に依存します。CategoryList は、どのカテゴリの開始ポイントが表示されるかについての情報にアクセスします。StartPointList を独立して使用するには、CategoryList からイベントトリガーをシミュレートします。

## StartPoint {#startpoint}

<table>
 <tbody>
  <tr>
   <td><p>モデル</p></td>
   <td><p>startpoint.js</p></td>
  </tr>
  <tr>
   <td><p>表示</p></td>
   <td><p>startpoint.js</p></td>
  </tr>
  <tr>
   <td><p>テンプレート</p></td>
   <td><p>startpoint.html</p></td>
  </tr>
  <tr>
   <td><p>コンポーネントが必要</p></td>
   <td><p>該当なし</p></td>
  </tr>
  <tr>
   <td><p>JS の依存関係</p></td>
   <td><p>タスクモデル</p></td>
  </tr>
  <tr>
   <td><p>リスンされているイベント（イベント名 – トリガー）</p></td>
   <td><p>変更 - startpoint モデル </p></td>
  </tr>
 </tbody>
</table>

## StartProcess {#startprocess}

<table>
 <tbody>
  <tr>
   <td><p>モデル</p> </td>
   <td><p>categorylist.js</p> </td>
  </tr>
  <tr>
   <td><p>表示</p> </td>
   <td><p>startprocess.js</p> </td>
  </tr>
  <tr>
   <td><p>テンプレート</p> </td>
   <td><p>startprocess.html</p> </td>
  </tr>
  <tr>
   <td><p>コンポーネントが必要</p> </td>
   <td>
    <ul>
     <li><p>ほとんどのユーティリティクラス</p> </li>
     <li><p>UserSearch</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>JS の依存関係</p> </td>
   <td>
    <ul>
     <li><p>カテゴリモデル</p> </li>
     <li><p>favoritecategoryfactory モデル</p> </li>
     <li><p>allcategoryfactory モデル</p> </li>
     <li><p>formrendering ユーティリティ</p> </li>
     <li><p>ノートユーティリティ</p> </li>
     <li><p>添付ユーティリティ</p> </li>
     <li><p>taskactions ユーティリティ</p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>リスンされているイベント（イベント名 – トリガー）</p> </td>
   <td>
    <ul>
     <li><p>category:selected - categorylist モデル</p> </li>
     <li><p>change:invokedTask - startpointlist モデル</p> </li>
     <li><p>change:formUrl - タスクモデル</p> </li>
     <li><p>startpoint:selected - startpointlist モデル</p> </li>
     <li><p>転送済み - タスクモデル</p> </li>
     <li><p>中止済み - タスクモデル</p> </li>
     <li><p>ロック解除済み - タスクモデル</p> </li>
     <li><p>ロック済み - タスクモデル</p> </li>
     <li>attachmentURLFetched - タスクモデル</li>
     <li>newAttachment - タスクモデル</li>
     <li>prepareForSubmitComplete - タスクモデル </li>
     <li><p>submitComplete - タスクモデル</p> </li>
     <li><p>allStartpointsFetched - categorylist モデル</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>StartProcess コンポーネントと StartPointList コンポーネントは、モデルクラスを共有します。このコンポーネントは、StartPointList から startpoint を選択すると関連が生じます。

## ProcessNameList {#processnamelist}

<table>
 <tbody>
  <tr>
   <td><p>モデル</p></td>
   <td><p>processnamelist.js</p></td>
  </tr>
  <tr>
   <td><p>表示</p></td>
   <td><p>processnamelist.js</p></td>
  </tr>
  <tr>
   <td><p>テンプレート</p></td>
   <td><p>tracking.html（ルートフォルダー内）</p></td>
  </tr>
  <tr>
   <td><p>コンポーネントが必要</p></td>
   <td><p>該当なし</p></td>
  </tr>
  <tr>
   <td><p>JS の依存関係</p></td>
   <td><p>processname モデル</p></td>
  </tr>
  <tr>
   <td><p>リスンされているイベント（イベント名 – トリガー）</p></td>
   <td>
    <ul>
     <li><p>追加 - processnamelist モデル </p></li>
     <li><p>fetched:processnames - processnamelist モデル </p></li>
     <li><p>変更 - processnamelist モデル </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessNameList は、他のコンポーネントに依存しません。ただし、他のコンポーネントに依存する ProcessInstanceList モデルクラスに内部的に依存します。したがって、ProcessNameList は、ProcessInstanceList、ProcessInstance、TaskList、Teamtask、Task など、多くのモデルクラスを使用します。これらの依存関係に加えて、ProcessNameList を独立して使用することもできます。

## ProcessName {#processname}

<table>
 <tbody>
  <tr>
   <td><p>モデル</p></td>
   <td><p>processname.js</p></td>
  </tr>
  <tr>
   <td><p>表示</p></td>
   <td><p>processname（processnamelist.js 内）</p></td>
  </tr>
  <tr>
   <td><p>テンプレート</p></td>
   <td><p>processname.html</p></td>
  </tr>
  <tr>
   <td><p>コンポーネントが必要</p></td>
   <td><p>該当なし</p></td>
  </tr>
  <tr>
   <td><p>JS の依存関係</p></td>
   <td><p>processinstancelist モデル</p></td>
  </tr>
  <tr>
   <td><p>リスンされているイベント（イベント名 – トリガー）</p></td>
   <td><p>変更 - processname モデル </p></td>
  </tr>
 </tbody>
</table>

## ProcessInstanceList {#processinstancelist}

<table>
 <tbody>
  <tr>
   <td><p>モデル</p></td>
   <td><p>processnamelist.js</p></td>
  </tr>
  <tr>
   <td><p>表示</p></td>
   <td><p>processinstancelist.js</p></td>
  </tr>
  <tr>
   <td><p>テンプレート</p></td>
   <td><p>tracking.html（ルートフォルダー内）</p></td>
  </tr>
  <tr>
   <td><p>コンポーネントが必要</p></td>
   <td><p>該当なし</p></td>
  </tr>
  <tr>
   <td><p>JS の依存関係</p></td>
   <td><p>processname モデル</p></td>
  </tr>
  <tr>
   <td><p>リスンされているイベント（イベント名 – トリガー）</p></td>
   <td>
    <ul>
     <li><p>processname:selected - processnamelist モデル </p></li>
     <li><p>processname:instancesfetched - processnamelist モデル </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessInstanceList は、インスタンスを取得し表示するために、プロセス名を示す ProcessNameList からのイベントを期待します。ProcessInstanceList を独立して使用するには、イベントトリガーを個別にシミュレートします。

## ProcessInstance {#processinstance}

<table>
 <tbody>
  <tr>
   <td><p>モデル</p></td>
   <td><p>processinstance.js</p></td>
  </tr>
  <tr>
   <td><p>表示</p></td>
   <td><p>processnamelist.js 内部の processname</p></td>
  </tr>
  <tr>
   <td><p>テンプレート</p></td>
   <td><p>processinstance.html</p></td>
  </tr>
  <tr>
   <td><p>コンポーネントが必要</p></td>
   <td><p>該当なし</p></td>
  </tr>
  <tr>
   <td><p>JS の依存関係</p></td>
   <td><p>tasklist モデル</p></td>
  </tr>
  <tr>
   <td><p>リスンされているイベント（イベント名 – トリガー）</p></td>
   <td><p>変更 - processinstance モデル </p></td>
  </tr>
 </tbody>
</table>

## ProcessInstanceHistory {#processinstancehistory}

<table>
 <tbody>
  <tr>
   <td><p>モデル</p></td>
   <td><p>processnamelist.js</p></td>
  </tr>
  <tr>
   <td><p>表示</p></td>
   <td><p>processinstancehistory.js</p></td>
  </tr>
  <tr>
   <td><p>テンプレート</p></td>
   <td><p>processinstancehistory.html</p></td>
  </tr>
  <tr>
   <td><p>コンポーネントが必要</p></td>
   <td><p>該当なし</p></td>
  </tr>
  <tr>
   <td><p>JS の依存関係</p></td>
   <td>
    <ul>
     <li><p>processname モデル</p></li>
     <li><p>履歴ユーティリティ</p></li>
    </ul></td>
  </tr>
  <tr>
   <td><p>リスンされているイベント（イベント名 – トリガー）</p></td>
   <td>
    <ul>
     <li><p>processname:selected - processnamelist モデル </p></li>
     <li><p>processinstance:selected - processinstancelist モデル </p></li>
     <li><p>tasksFetched - processinstance モデル </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ProcessInstanceHistory は、どのプロセスインスタンスの履歴を表示するかどうかを示す ProcessInstanceList からのイベントを期待します。この依存関係に加えて、コンポーネントを独立して使用することもできます。

## OutofOffice {#outofoffice}

<table>
 <tbody>
  <tr>
   <td><p>モデル</p> </td>
   <td><p>outofoffice.js</p> </td>
  </tr>
  <tr>
   <td><p>表示</p> </td>
   <td><p>outofoffice.js</p> </td>
  </tr>
  <tr>
   <td><p>テンプレート</p> </td>
   <td><p>outofoffice.html</p> </td>
  </tr>
  <tr>
   <td><p>コンポーネントが必要</p> </td>
   <td><p>UserSearch</p> </td>
  </tr>
  <tr>
   <td><p>JS の依存関係</p> </td>
   <td><p>usersearch ビュー</p> </td>
  </tr>
  <tr>
   <td><p>リスンされているイベント（イベント名 – トリガー）</p> </td>
   <td>
    <ul>
     <li><p>outOfOfficeSettingsFetched - outofoffice モデル</p> </li>
     <li><p>outOfOfficeSettingsSaved - outofoffice モデル</p> </li>
     <li><p>processesFetched - outofoffice モデル</p> </li>
     <li><p>principalSelected - principalsearch ビュー</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>OutofOffice は単独で使用可能です。

## ShareQueue {#sharequeue}

<table>
 <tbody>
  <tr>
   <td><p>モデル</p> </td>
   <td><p>sharequeue.js</p> </td>
  </tr>
  <tr>
   <td><p>表示</p> </td>
   <td><p>sharequeue.js</p> </td>
  </tr>
  <tr>
   <td><p>テンプレート</p> </td>
   <td><p>sharequeue.html</p> </td>
  </tr>
  <tr>
   <td><p>コンポーネントが必要</p> </td>
   <td><p>UserSearch</p> </td>
  </tr>
  <tr>
   <td><p>JS の依存関係</p> </td>
   <td><p>usersearch ビュー</p> </td>
  </tr>
  <tr>
   <td><p>リスンされているイベント（イベント名 – トリガー）</p> </td>
   <td>
    <ul>
     <li><p>queueAccessGranted - sharequeue モデル</p> </li>
     <li><p>queueAccessRequested - sharequeue モデル</p> </li>
     <li><p>grantedUsersFetched - sharequeue モデル</p> </li>
     <li>accessibleUsersFetched - sharequeue モデル</li>
     <li><p>queueAccessRevoked - sharequeue モデル</p> </li>
     <li><p>queueAccessRemoved - sharequeue モデル</p> </li>
     <li><p>principalSelected - principalsearch ビュー</p> </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>ShareQueue は独立して使用可能です。

## UISettings {#uisettings}

<table>
 <tbody>
  <tr>
   <td><p>モデル</p></td>
   <td><p>uisettings.js</p></td>
  </tr>
  <tr>
   <td><p>表示</p></td>
   <td><p>uisettings.js</p></td>
  </tr>
  <tr>
   <td><p>テンプレート</p></td>
   <td><p>uisettings.html</p></td>
  </tr>
  <tr>
   <td><p>コンポーネントが必要</p></td>
   <td><p>該当なし</p></td>
  </tr>
  <tr>
   <td><p>JS の依存関係</p></td>
   <td><p>該当なし</p></td>
  </tr>
  <tr>
   <td><p>リスンされているイベント（イベント名 – トリガー）</p></td>
   <td>
    <ul>
     <li><p>preferencesFetched - uisettings モデル </p></li>
     <li><p>settingUpdated - uisettings モデル </p></li>
    </ul></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>UISettings は独立して使用可能です。

## AppNavigation {#appnavigation}

<table>
 <tbody>
  <tr>
   <td><p>モデル</p></td>
   <td><p>appnavigation.js</p></td>
  </tr>
  <tr>
   <td><p>表示</p></td>
   <td><p>appnavigation.js</p></td>
  </tr>
  <tr>
   <td><p>テンプレート</p></td>
   <td><p>appnavigation.html</p></td>
  </tr>
  <tr>
   <td><p>コンポーネントが必要</p></td>
   <td><p>該当なし</p></td>
  </tr>
  <tr>
   <td><p>JS の依存関係</p></td>
   <td><p>該当なし</p></td>
  </tr>
  <tr>
   <td><p>リッスンされているイベント</p></td>
   <td><p>該当なし</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>AppNavigation は独立して使用可能です。

## UserInfo {#userinfo}

<table>
 <tbody>
  <tr>
   <td><p>モデル</p> </td>
   <td><p>userinfo.js</p> </td>
  </tr>
  <tr>
   <td><p>表示</p> </td>
   <td><p>userinfo.js</p> </td>
  </tr>
  <tr>
   <td><p>テンプレート</p> </td>
   <td><p>userinfo.html</p> </td>
  </tr>
  <tr>
   <td><p>コンポーネントが必要</p> </td>
   <td><p>該当なし</p> </td>
  </tr>
  <tr>
   <td><p>JS の依存関係</p> </td>
   <td><p>該当なし</p> </td>
  </tr>
  <tr>
   <td><p>リスンされているイベント（イベント名 – トリガー）</p> </td>
   <td>
    <ul>
     <li>userImageUrlFetched - userinfo モデル</li>
     <li>sessionRenewed - userinfo モデル <br /> </li>
     <li>sessionExpired - userinfo モデル </li>
    </ul> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>UserInfo は独立して使用可能です。

## WSError {#wserror}

<table>
 <tbody>
  <tr>
   <td><p>モデル</p></td>
   <td><p>wserror.js</p></td>
  </tr>
  <tr>
   <td><p>表示</p></td>
   <td><p>wserror.js</p></td>
  </tr>
  <tr>
   <td><p>テンプレート</p></td>
   <td><p>wserror.html</p></td>
  </tr>
  <tr>
   <td><p>コンポーネントが必要</p></td>
   <td><p>該当なし</p></td>
  </tr>
  <tr>
   <td><p>JS の依存関係</p></td>
   <td><p>該当なし</p></td>
  </tr>
  <tr>
   <td><p>リスンされているイベント（イベント名 – トリガー）</p></td>
   <td><p>newWsError - wserror モデル </p></td>
  </tr>
 </tbody>
</table>

## UserSearch {#usersearch}

<table>
 <tbody>
  <tr>
   <td><p>モデル</p> </td>
   <td><p>usersearch.js</p> </td>
  </tr>
  <tr>
   <td><p>表示</p> </td>
   <td><p>usersearch.js</p> </td>
  </tr>
  <tr>
   <td><p>テンプレート</p> </td>
   <td><p>usersearch.html</p> </td>
  </tr>
  <tr>
   <td><p>コンポーネントが必要</p> </td>
   <td><p>該当なし</p> </td>
  </tr>
  <tr>
   <td><p>JS の依存関係</p> </td>
   <td><p>該当なし</p> </td>
  </tr>
  <tr>
   <td><p>リスンされているイベント（イベント名 – トリガー）</p> </td>
   <td>
    <ul>
     <li>principalSearched - principalsearch モデル</li>
     <li>outOfOfficeInfoFetched - usersearch モデル</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

## SearchTemplate {#searchtemplate}

<table>
 <tbody>
  <tr>
   <td><p>モデル</p> </td>
   <td><p>searchtemplate.js</p> </td>
  </tr>
  <tr>
   <td><p>表示</p> </td>
   <td><p>searchtemplate (in searchtemplatelist.js) </p> </td>
  </tr>
  <tr>
   <td><p>テンプレート</p> </td>
   <td><p>searchtemplate.html</p> </td>
  </tr>
  <tr>
   <td><p>コンポーネントが必要</p> </td>
   <td><p>該当なし</p> </td>
  </tr>
  <tr>
   <td><p>JS の依存関係</p> </td>
   <td><p>該当なし</p> </td>
  </tr>
  <tr>
   <td><p>リスンされているイベント（イベント名 – トリガー）</p> </td>
   <td><p>templateFetched- searchtemplate モデル</p> </td>
  </tr>
 </tbody>
</table>

## SearchTemplateList {#searchtemplatelist}

<table>
 <tbody>
  <tr>
   <td><p>モデル</p> </td>
   <td><p>searchtemplatelist.js</p> </td>
  </tr>
  <tr>
   <td><p>表示</p> </td>
   <td><p>searchtemplatelist.js</p> </td>
  </tr>
  <tr>
   <td><p>テンプレート</p> </td>
   <td><p>tracking.html（ルートフォルダー内）</p> </td>
  </tr>
  <tr>
   <td><p>コンポーネントが必要</p> </td>
   <td><p>該当なし</p> </td>
  </tr>
  <tr>
   <td><p>JS の依存関係</p> </td>
   <td><p>searchtemplate モデル</p> </td>
  </tr>
  <tr>
   <td><p>リスンされているイベント（イベント名 – トリガー）</p> </td>
   <td><p>change - searchtemplatelist モデル</p> </td>
  </tr>
 </tbody>
</table>

## SearchTemplateDetails {#searchtemplatedetails}

<table>
 <tbody>
  <tr>
   <td><p>モデル</p> </td>
   <td><p>searchtemplatelist.js</p> </td>
  </tr>
  <tr>
   <td><p>表示</p> </td>
   <td><p>searchtemplatedetails.js</p> </td>
  </tr>
  <tr>
   <td><p>テンプレート</p> </td>
   <td><p>searchtemplatedetails.html</p> </td>
  </tr>
  <tr>
   <td><p>コンポーネントが必要</p> </td>
   <td><p>該当なし</p> </td>
  </tr>
  <tr>
   <td><p>JS の依存関係</p> </td>
   <td>該当なし<br /> </td>
  </tr>
  <tr>
   <td><p>リスンされているイベント（イベント名 – トリガー）</p> </td>
   <td><p>searchTemplate:selected - searchtemplate モデル</p> </td>
  </tr>
 </tbody>
</table>
