---
title: タスクの操作
seo-title: Working with Tasks
description: タスクは、コンテンツで実行するべき作業項目を表し、プロジェクトで現在のタスクの完了レベルを判断するために使用されます。
seo-description: Tasks represent items of work to be done on content and are used in projects to determine the level of completeness of current tasks
uuid: df4efb3f-8298-4159-acfe-305ba6b46791
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
discoiquuid: 1b79d373-73f4-4228-b309-79e74d191f3e
exl-id: a0719745-8d67-44bc-92ba-9ab07f31f8d2
source-git-commit: 200b47070b7ead54ee54eea504bd960d4e0731d9
workflow-type: ht
source-wordcount: '597'
ht-degree: 100%

---


# タスクの操作 {#working-with-tasks}

タスクは、コンテンツに関して実行する作業項目を表します。タスクが割り当てられると、ワークフローインボックスに表示されます。タスク項目とワークフロー項目は、「**タイプ**」列の値によって区別することができます。

タスクは、プロジェクトの完了レベルを決定するために、プロジェクトでも使用されます。

## プロジェクトの進行状況の追跡 {#tracking-project-progress}

**タスク**&#x200B;タイルで表されるプロジェクト内部のアクティブなタスクまたは完了したタスクを監視することによって、プロジェクトの進行状況を追跡できます。プロジェクトの進行状況は、次のもので判断できます。

* **タスクタイル：**&#x200B;プロジェクトの全体的な進行状況は、プロジェクトの詳細ページに表示されるタスクタイルに表示されます。

* **タスクリスト：**&#x200B;タスクタイルをクリックすると、タスクのリストが表示されます。このリストには、プロジェクトに関連するすべてのタスクの詳細情報が含まれます。

どちらのオプションでもワークフロータスクと、タスクタイルで直接作成したタスクが表示されます。

### タスクタイル {#task-tile}

プロジェクトに関連タスクがある場合、プロジェクト内にタスクタイルが表示されます。タスクタイルは、プロジェクトの現在のステータスを示します。このステータスは、ワークフロー内の既存タスクに基づいています。ワークフローの進行に伴って今後作成されるタスクは含まれていません。タスクタイルには、次の情報が表示されます。

* 完了したタスクの割合
* アクティブなタスクの割合
* 期限切れのタスクの割合

![タスクタイル](assets/project-tile-tasks.png)

### プロジェクト内のタスクの表示または変更 {#viewing-or-modifying-the-tasks-in-a-project}

進行状況の追跡に加えて、プロジェクトに関する追加情報を表示または変更することもできます。

#### タスクリスト {#task-list}

タスクタイルの右下にある省略記号ボタンをクリックして、プロジェクトに関連するタスクでフィルターされたインボックスを表示します。期限、担当者、優先度、ステータスなどのメタデータと共に、タスクの詳細が表示されます。

![プロジェクトタスクインボックス](assets/project-tasks.png)

#### タスクの詳細 {#task-details}

特定のタスクの詳細を表示するには、インボックスで、タスクをタップまたはクリックして選択し、ツールバーの「**開く**」をタップまたはクリックします。

![タスクの詳細](assets/project-task-detail.png)

様々なタブで、タスクの詳細を表示、編集または追加できます。

* **タスク** - タスクの一般情報
* **プロジェクト情報** - タスクが関連付けられているプロジェクトの概要
* **ワークフロー情報** - タスクが関連付けられているワークフローの概要（該当する場合）
* **コメント** - タスク自体に対する一般的なコメント

### タスクの追加 {#adding-tasks}

新しいタスクをプロジェクトに追加できます。これらのタスクはタスクタイルに表示され、通知インボックスで使用できるので、未処理のタスクを把握できます。

タスクを追加するには：

1. プロジェクト内で、**タスク**&#x200B;タイルを探します。
1. タイルの右上にある下向きの山形をタップまたはクリックし、「**タスクを作成**」を選択します。
1. **タスクを追加**&#x200B;ウィンドウで、タスクの詳細（優先度、担当者、期限など）を指定します。

   ![タスクの追加](assets/project-add-task.png)

1. 「**送信**」をタップまたはクリックします。

## インボックス内でのタスクの使用 {#working-with-tasks-in-the-inbox}

プロジェクト自体からプロジェクトタスクにアクセスする代わりに、インボックスから直接アクセスできます。インボックスには、ワークフロー全体を理解できるよう、プロジェクト全体のタスクの概要が表示されます。

インボックスからタスクを開き、タスクのステータスを設定できます。所属するユーザーグループにタスクが割り当てられた場合も、そのタスクがインボックスに表示されます。この場合、グループのいずれかのメンバーが作業を実行し、タスクを完了することができます。

![インボックス](assets/project-inbox.png)

タスクを完了するには、タスクを選択して「**完了**」をクリックします。タスクに情報を追加して、「**完了**」をクリックします。詳しくは、[インボックス](/help/sites-authoring/inbox.md)を参照してください。
