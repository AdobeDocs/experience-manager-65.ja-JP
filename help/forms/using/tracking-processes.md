---
title: プロセスの追跡
description: プロセスを検索してそれらの詳細を表示することによって、プロセスを追跡する方法。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 381a46c6-c73c-476a-a1a0-20d921069c37
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
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
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 100%
---
# プロセスの追跡 {#tracking-processes}

追跡ページでは、開始または参加したアクティブなプロセスや完了したプロセスを検索し、そのプロセスの詳細を表示することができます。 プロセスの詳細には、プロセスに含まれていたタスク、割り当ておよびフォームが表示されます。 また、既に開始したプロセスのフォームデータを使用して、新しいプロセスを開始することもできます。

## プロセスとタスクを検索する {#search-for-processes-and-tasks}

プロセスインスタンスおよび関連付けられているタスクは、プロセス名に基づいて、または AEM Forms Workspace の管理者によって設定された検索テンプレートを使用して検索できます。

検索結果に表示する列を設定することができます。

>[!NOTE]
>
>実際にタスクに参加していない限り、検索結果には、アクセス権限を持つグループタスクリストまたは共有タスクリストに表示されたタスクは含まれません。 管理者によって削除された完了済みプロセスインスタンスも含まれません。

### プロセス名で検索する {#search-by-process-name}

1. 追跡ページの左側のパネルで、プロセス名を選択します。 開始または完了したタスクを含むプロセスのすべてのインスタンスがメインパネルに表示されます。
1. プロセスインスタンスをクリックして、詳細情報を表示します。

### 検索テンプレートを使用してタスクを検索する {#search-for-a-task-using-a-search-template}

1. 追跡ページの左側のリストから、「**検索テンプレート**」を選択して、検索テンプレートを選択します。
1. テンプレートが検索パラメーターをサポートしている場合は、検索パラメーターを絞り込むため、テンプレートフィールドに記入して「**検索**」をクリックします。 検索条件に一致する、参加したすべてのタスクのリストが表示されます。

## プロセスの詳細を表示する {#view-process-details}

追跡ページで、プロセスを選択してその詳細を表示することができます。 様々なパラメーターに基づいてプロセスを検索し、タスクの詳細を表示することができます。 また、複数のユーザーが同時にタスクを受信できるプロセスに関する「ステータス」タブも表示できます。ここでは、ドキュメントを確認するためのツールを使用できます。

**ステータス：**&#x200B;あるプロセスのタスクのステータスは、タスクをクリックすると「選択したアクション」列に表示されます。 ただし、プロセスのステータスは使用できません。

1. プロセスインスタンスの一部であるタスクの詳細を表示するには、検索結果リストからプロセスインスタンスを選択します。
1. タスクの詳細情報を表示するには、以下のアクションを 1 つ以上実行します。

   * タスクのメモと添付ファイルを表示するには、「添付ファイル」タブをクリックします。
   * タスクの割り当ての詳細を表示するには、「割り当て」タブをクリックします。
   * 関連付けられているフォームを表示するには、フォームボタンをクリックします。
