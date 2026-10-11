---
title: 停止した操作および停止したブランチの使用
description: 停止した操作ページおよび停止したブランチページには、停止したプロセスが表示されます。
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: c96faae0-2b0f-4334-b61c-f13b2d1ec179
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
source-wordcount: '719'
ht-degree: 100%
---
# 停止した操作および停止したブランチの使用 {#working-with-stalled-operations-and-branches}

>[!NOTE]
> 
> ユーザーが管理者コンソールにアクセスする管理者権限を持っていることを確認します。

停止した操作ページおよび停止したブランチページには、停止したプロセスが表示されます。 操作の実行中または実行後にエラーが発生した場合、または、プロセス内での意図的な停止操作によって、プロセスは停止することがあります。

* 操作は、予期しないエラーが原因で停止することがあります。 プロセス内でのブランチ停止操作ではプロセスの実行が意図的に停止されますが、この場合は、管理者による介入が必要です。
* ブランチは、ルールの評価時に操作と操作の間で停止することがあります。

プロセスが停止した場合は、問題が修正され、操作またはブランチが再起動されるまで、操作は実行されません。

停止したアイテムごとに、リストには、以下の情報が表示されます。

**操作名またはブランチ名：**&#x200B;操作またはブランチの名前。

**ステータス：**&#x200B;停止した項目の場合は常に「停止」です。

**エラー：**&#x200B;問題に関する短い説明。

**プロセス ID：**&#x200B;プロセスがインスタンス化される（つまり、ユーザーまたは自動ステップによってプロセスが開始される）ときに、forms ワークフローによって割り当てられる正の整数。 この ID を使用して、プロセスインスタンスをライフサイクル全体にわたって追跡できます。

**プロセス名 - バージョン：**&#x200B;ワークベンチで割り当てられたプロセスの名前。

**停止日：**&#x200B;操作またはブランチが停止した日時。

停止した操作ページまたは停止したブランチページで、次のタスクを実行できます。

* エラーを選択して、その詳細情報を表示します。 エラーを選択すると、エラーの詳細ページが表示されます。
* 停止した操作を終了または再試行するか、停止したブランチを再試行します。

## 停止した操作またはブランチの終了または再試行 {#terminating-or-retrying-stalled-operations-or-branches}

停止した操作ページでは、表示されているプロセスインスタンスを終了できます。

プロセスインスタンスを終了すると、実行が停止し、以降の操作が行われません。 プロセスは、エラーによってブロックされたり、使用できなくなったりすることがあり、修正して再起動できない場合に限り、通常はプロセスを終了します。

停止した操作ページまたは停止したブランチページでは、操作またはブランチを再試行できます。

操作を再試行すると、操作を再開するリクエストが Forms Workflow に送信されます。 プロセスの停止を引き起こしたエラーが修正され、再試行リクエストが正常に行われると、プロセスの実行は停止した時点から再開され、そのステータスが RUNNING に変わります。 操作を再起動できない場合、ステータスは「停止」のままとなり、管理者による終了が必要になります。

### 停止した操作の終了 {#terminate-a-stalled-operation}

1. 管理コンソールで、サービス／Forms Workflow／停止した操作のエラーをクリックします。
1. 停止した操作ページで、終了するアイテムを選択し、「終了」をクリックします。

### 停止した操作またはブランチの再試行 {#retry-a-stalled-operation-or-branch}

1. 管理コンソールで、サービス／Forms Workflow をクリックし、「停止した操作のエラー」または「停止したブランチのエラー」をクリックします。
1. 停止した操作ページまたは停止したブランチページで、再試行するアイテムを選択し、「再試行」をクリックします。

## 停止した操作またはブランチのエラーの詳細の表示 {#viewing-error-details-about-stalled-operations-or-branches}

停止した操作ページまたは停止したブランチページで、停止したアイテムのリストからエラーを選択すると、エラーの詳細ページが表示され、問題のトラブルシューティングに役立つ、エラーに関する詳細情報が表示されます。

ページ下部のボックスには、エラー情報が表示されます。

エラーの詳細ページから、停止した操作の終了または再試行、および停止したブランチの再試行を行うこともできます。

## エスカレーションユーザーが存在しない場合にプロセスが停止しない {#process-does-not-stall-when-escalation-user-does-not-exist}

AEM Forms User サービスの Assign Task 操作が、特定の期間後に別のユーザーにタスクをエスカレーションするように設定されており、Assign Task 操作の終了後、エスカレーションが発生する前にエスカレーションユーザーが削除された場合、エラーが発生します。

これらの状況では、設定されたエスカレーション時にプロセスおよびタスクの状態が変更されず、エスカレーションが発生しませんが、プロセスは停止しません。 次のメッセージが、サーバーログに表示されます。

&quot;The principal specified for escalation is not valid, for taskID: *number*, queue specified: *number*.&quot;

タスクの生成前（Assign Task 操作の前）にエスカレーションユーザーが削除された場合、プロセスが停止するか、または InvalidPrincipal 例外イベントが発生します。

この問題を回避するには、ユーザーを削除するときに、そのユーザーに属するタスクを検索して適切に処理します （[タスクの使用](/help/forms/using/admin-help/tasks.md#working-with-tasks)を参照）。
