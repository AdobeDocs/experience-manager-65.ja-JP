---
title: Forms JEE ワークフロー | ユーザーデータの処理
seo-title: Forms JEE ワークフロー | ユーザーデータの処理
description: Forms JEE ワークフロー | ユーザーデータの処理
uuid: 3b06ef19-d3c4-411e-9530-2c5d2159b559
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5632a8df-a827-4e38-beaa-18b61c2208a3
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '1371'
ht-degree: 70%

---


# Forms JEE ワークフロー | ユーザーデータの処理 {#forms-jee-workflows-handling-user-data}

AEM FormsのJEEワークフローは、ビジネスプロセスを設計、作成、管理するツールを提供します。 ワークフロープロセスは、特定の順序で実行される一連のステップで構成されます。各ステップで、ユーザーへのタスクの割り当てや電子メールメッセージの送信など、特定の処理が実行されます。プロセスは、アセット、ユーザーアカウントおよびサービスとインタラクティブに動作し、次のいずれかの方法でトリガーすることができます。

* AEM Forms Workspace からのプロセスの開始
* SOAP または RESTful サービスの使用
* アダプティブフォームの送信
* 監視フォルダーの使用
* 電子メールの使用

For more information about creating AEM Forms JEE workflow process, see [Workbench Help](http://www.adobe.com/go/learn_aemforms_workbench_65_jp).

## ユーザーデータとデータストア {#user-data-and-data-stores}

プロセスがトリガーされて進行すると、プロセスの参加者に関するデータ、プロセスに関連付られたフォームに参加者が入力したデータ、およびフォームに追加された添付ファイルが取得されます。これらのデータは AEM Forms JEE サーバーのデータベースに格納され、添付ファイルのような一部のデータは Global Document Storage（GDS）ディレクトリに格納されます（設定が行われている場合）。GDS ディレクトリは、共有ファイルシステムまたはデータベース上に構成できます。

## ユーザーデータへのアクセスと削除 {#access-and-delete-user-data}

プロセスがトリガーされると、一意のプロセスインスタンスIDと長期間有効な呼び出しIDが生成され、プロセスインスタンスに関連付けられます。 永続的呼び出し ID に基づいて、プロセスインスタンスのデータへアクセスしてデータを削除できます。プロセスインスタンスの長期間有効な呼び出しIDは、プロセスの開始者のユーザー名、またはタスクを送信したプロセス参加者のユーザー名を使用して推定できます。

ただし、以下のシナリオでは開始者のプロセスインスタンス ID を特定することはできません。

* **監視フォルダーを介してトリガーされたプロセス**：プロセスが監視フォルダーによりトリガーされた場合、そのプロセスの開始者を使用してプロセスインスタンスを特定することはできません。この場合、ユーザー情報は格納済みデータでエンコードされます。
* **AEM の発行インスタンスから開始されたプロセス**：AEM 発行インスタンスからトリガーされたすべてのプロセスインスタンスは、開始者に関する情報を取得しません。ただし、ユーザーデータは、ワークフロー変数に格納されているプロセスに関連付けられたフォームに取得される場合があります。
* **電子メールを使用して開始されたプロセス**:送信者の電子メールIDは、 `tb_job_instance` データベーステーブルの不透明なblob列のプロパティとして取得され、直接クエリーすることはできません。

### ワークフローの開始者または参加者が分かっている場合のプロセスインスタンス ID の特定 {#initiator-participant}

ワークフローの開始者または参加者のプロセスインスタンス ID を特定するには、次の手順を実行します。

1. Execute the following command in AEM Forms server database to retrieve the principal ID for workflow initiator or participant from the `edcprincipalentity` database table.

   ```sql
   select id from edcprincipalentity where canonicalname='user_ID'
   ```

   クエリを実行すると、指定された `user_ID` のプリンシパル ID が返されます。

1. （**ワークフロー開始者の場合**）次のコマンドを実行して、`tb_task` データベーステーブルから開始者のプリンシパル ID に関連付けられたすべてのタスクを取得します。

   ```sql
   select * from tb_task where start_task = 1 and create_user_id= 'initiator_principal_id'
   ```

   The query returns tasks initiated by the specified `initiator`_ `principal_id`. タスクには次の 2 つのタイプがあります。

   * **完了したタスク**:これらのタスクは送信済みで、フィールドに英数字の値が表示され `process_instance_id` ます。 送信済みタスクのすべてのプロセスインスタンス ID をメモして、手順を続行します。
   * **開始されたが完了していないタスク**：これらのタスクは開始されていますが、まだ送信されていません。The value in the `process_instance_id` field for these tasks is **0** (zero). この場合、対応するタスク ID をメモして、「[オーファンタスクの操作](#orphan)」を参照してください。

1. (**For workflow participants**) Execute the following command to retrieve process instance IDs associated with the principal ID of the process participant for the initiator from the `tb_assignment` database table.

   ```sql
   select distinct a.process_instance_id from tb_assignment a join tb_queue q on a.queue_id = q.id where q.workflow_user_id='participant_principal_id'
   ```

   クエリを実行すると、参加者がタスクを何も送信していない場合も含めて、参加者に関連付けられたすべてのプロセスのインスタンス ID が返されます。

   送信済みタスクのすべてのプロセスインスタンス ID をメモして、手順を続行します。

   For orphan tasks or tasks where the `process_instance_id` is 0 (zero), take note of the corresponding task IDs and see [Work with orphan tasks](#orphan).

1. Follow the instructions in [Purge user data from workflow instances based on process instance IDs](/help/forms/using/forms-workflow-jee-handling-user-data.md#purge) section to delete user data for identified process instance IDs.

### ユーザーデータがプリミティブ変数に格納されている場合のプロセスインスタンス ID の特定 {#primitive}

ワークフローは、ユーザーデータがデータベース内のBLOBとして格納される変数に取り込まれるように設計できます。 このような場合、次のプリミティブ型変数のいずれかに格納されている場合にのみ、ユーザーデータのクエリを実行できます。

* **文字列**：ユーザー ID は直接またはサブ文字列として含まれ、SQL を使用してクエリを実行できます。
* **数値**：ユーザー ID は直接含まれています。
* **XML**：ユーザー ID はデータベースにテキスト列として格納されたテキスト内のサブ文字列として含まれ、文字列と同じようにクエリを実行できます。

プリミティブ型変数にデータが格納されているワークフローにユーザーのデータが含まれるかどうかを確認するには、次の手順を実行します。

1. 次のデータベースコマンドを実行します。

   ```sql
   select database_table from omd_object_type where name='pt_<app_name>/<workflow_name>'
   ```

   The query returns a table name in `tb_<number>` format for the specified application ( `app_name`) and workflow ( `workflow_name`).

   >[!NOTE]
   >
   >ワークフローがアプリケーション内のサブフォルダーにネストされている場合、`name` プロパティの値は複合型にすることができます。ワークフローへの正確なフルパスを指定するようにしてください。これは、`omd_object_type` データベーステーブルから取得できます。

1. Review the `tb_<number>` table schema. テーブルには、指定されたワークフローのユーザーデータを格納する変数が含まれています。テーブルの変数はワークフローの変数に対応しています。

   ユーザー ID を含むワークフロー変数に対応する変数を特定してメモしておきます。特定された変数がプリミティブ型の場合は、クエリを実行して、ユーザー ID に関連付けられたワークフローインスタンスを確認できます。

1. 次のデータベースコマンドを実行します。このコマンドでは、`user_var` がユーザー ID を含むプリミティブ型の変数です。

   ```sql
   select process_instance_id from <tb_name> where <user_var>=<user_ID>
   ```

   クエリを実行すると、指定された `user_ID` に関連付けられたすべてのプロセスインスタンス ID が返されます。

1. Follow the instructions in [Purge user data from workflow instances based on process instance IDs](/help/forms/using/forms-workflow-jee-handling-user-data.md#purge) section to delete user data for identified process instance IDs.

### プロセスインスタンス ID に基づいてワークフローインスタンスからユーザーデータを削除する {#purge}

これでユーザーに関連付けられたプロセスインスタンス ID を特定できたので、次の手順を実行して個々のプロセスインスタンスからユーザーデータを削除します。

1. Execute the following command to retrieve long-lived invocation ID and status for a process instance from the `tb_process_instance` table.

   ```sql
   select long_lived_invocation_id, status from tb_process_instance where id='process_instance_id'
   ```

   The query returns the long-lived invocation ID and status for the specified `process_instance_id`.

1. Create an instance of the public `ProcessManager` client ( `com.adobe.idp.workflow.client.ProcessManager`) using a `ServiceClientFactory` instance with the correct connection settings.

   詳しくは、「[Class ProcessManager](https://helpx.adobe.com/jp/experience-manager/6-3/forms/ProgramLC/javadoc/com/adobe/idp/workflow/client/ProcessManager.html)」の Java API リファレンスを参照してください。

1. ワークフローインスタンスのステータスを確認します。ステータスが2(COMPLETE)または4(TERMINATED)以外の場合は、次のメソッドを呼び出して、最初にインスタンスを終了します。

   `ProcessManager.terminateProcess(<long_lived_invocation_id>)`.

1. 次のメソッドを呼び出して、ワークフローインスタンスを削除します。

   `ProcessManager.purgeProcessInstance(<long_lived_invocation_id>)`

   `purgeProcessInstance` メソッドを使用すると、AEM Forms サーバーデータベースおよび GDS から、指定された呼び出し ID のすべてのデータが完全に削除されます（設定が行われている場合）。

### オーファンタスクの操作 {#orphan}

オーファンタスクは、プロセスが開始されているがまだ送信されていないプロセスを含むタスクです。in this case, the `process_instance_id` is **0** (zero). したがって、プロセスインスタンス ID を使用してオーファンタスクに保存されたユーザーデータを追跡することはできません。ただし、オーファンタスクのタスク ID を使用してユーザーデータを追跡することができます。「`tb_task`ワークフローの開始者または参加者が分かっている場合のプロセスインスタンス ID の特定[」で説明されているように、ユーザーの ](/help/forms/using/forms-workflow-jee-handling-user-data.md#initiator-participant) テーブルからタスク ID を特定することができます。

タスク ID が特定されたら、次を実行して GDS およびデータベースからオーファンタスクに関連するファイルおよびデータを削除します。

1. AEM Forms サーバーデータベースで次のコマンドを実行して、特定されたタスク ID の ID を取得します。

   ```sql
   select id from tb_form_data where task_id=<task_id>
   ```

   クエリを実行すると、ID のリストが返されます。次のように、返された ID（`fd_id`）ごとにセッション ID 文字列のリストを作成します。

   * _ `wfattach<task_id>`
   * `_wftask<fd_id>`
   * `_wftaskformid<fd_id>`

1. GDS がファイルシステムまたはデータベースを指しているのかに応じて、次のいずれかの手順を実行します。

   1. **ファイルシステムの GDS**

      GDS ファイルシステムで次の手順を実行します。

      1. 次のセッションID文字列を拡張子として持つファイルを検索します。
      * `_wfattach<task_id>`
      * `_wftask<fd_id>`
      * `_wftaskformid<fd_id>`

      これらの拡張子を持つファイルはマーカーファイルです。これらのファイルは次の形式のファイル名で保存されます。

      `<file_name_guid>.session<session_id_string>`

      1. Delete all marker files and other files with the exact filename as `<file_name_guid>` from the file system.
   1. **データベースの GDS**

      セッション ID ごとに次のコマンドを実行します。

      ```sql
      delete from tb_dm_chunk where documentid in (select documentid from tb_dm_session_reference where sessionid=<session_id>)
      delete from tb_dm_session_reference where sessionid=<session_id>
      delete from tb_dm_deletion where sessionid=<session_id>
      ```




1. 次のコマンドを実行して、AEM Forms サーバーデータベースからタスク ID のデータを削除します。

   ```sql
   delete from tb_task_acl where task_id=<task_id>
   delete from tb_task_attachment where task_id=<task_id>
   delete from tb_form_data where task_id=<task_id>
   delete from tb_assignment where task_id=<task_id>
   delete from tb_task where id=<task_id>
   ```

