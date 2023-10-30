---
title: Forms JEE ワークフロー | ユーザーデータの処理
description: AEM Forms JEE ワークフローを使用して、ビジネスプロセスを設計、作成、管理します。
uuid: 3b06ef19-d3c4-411e-9530-2c5d2159b559
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5632a8df-a827-4e38-beaa-18b61c2208a3
role: Admin
exl-id: 847fa303-8d1e-4a17-b90d-5f9da5ca2d77
source-git-commit: 0e5b89617d481c69882ec5d4658e76855aa9b691
workflow-type: tm+mt
source-wordcount: '1370'
ht-degree: 53%

---

# Forms JEE ワークフロー | ユーザーデータの処理 {#forms-jee-workflows-handling-user-data}

AEM Forms JEE ワークフローには、ビジネスプロセスを設計、作成および管理するためのツールが用意されています。ワークフロープロセスは、指定された順序で実行される一連のステップで構成されます。 各ステップでは、ユーザーへのタスクの割り当てやメールメッセージの送信など、特定のアクションを実行します。プロセスは、アセット、ユーザーアカウントおよびサービスとやり取りでき、次のいずれかの方法でトリガーできます。

* AEM Forms Workspace からのプロセスの開始
* SOAP または RESTful サービスの使用
* アダプティブフォームの送信
* 監視フォルダーの使用
* 電子メールの使用

AEM Forms JEE ワークフロープロセスの作成について詳しくは、[Workbench ヘルプ](https://www.adobe.com/go/learn_aemforms_workbench_65_jp)を参照してください。

## ユーザーデータとデータストア {#user-data-and-data-stores}

プロセスがトリガーされ、進行するにつれて、プロセス参加者に関するデータ、プロセスに関連付けられたフォームに参加者が入力したデータ、およびフォームに追加された添付ファイルが取り込まれます。 データはAEM Forms JEE サーバーのデータベースに保存され、設定に応じて、添付ファイルなどの一部のデータがグローバルドキュメントストレージ (GDS) ディレクトリに保存されます。 GDS ディレクトリは、共有ファイルシステムまたはデータベース上で設定できます。

## ユーザーデータへのアクセスと削除 {#access-and-delete-user-data}

プロセスがトリガーされると、一意のプロセスインスタンス ID と永続的呼び出し ID が生成され、プロセスインスタンスに関連付けられます。永続的呼び出し ID に基づいて、プロセスインスタンスのデータへアクセスして、データを削除できます。プロセスイニシエーターのユーザー名またはタスクを送信したプロセス参加者のユーザー名を使用して、プロセスインスタンスの永続的呼び出し ID を推測することができます。

ただし、次のシナリオでは、イニシエーターのプロセスインスタンス ID を特定できません。

* **監視フォルダーを介してトリガーされたプロセス**：プロセスが監視フォルダーによってトリガーされた場合、そのプロセスの開始者を使用してプロセスインスタンスを識別することはできません。 この場合、ユーザー情報は格納済みデータにエンコードされています。
* **プロセスは、パブリッシュAEMインスタンスから開始されました**:AEMパブリッシュインスタンスからトリガーされるすべてのプロセスインスタンスは、イニシエーターに関する情報を取り込みません。 ただし、ユーザーデータは、プロセスに関連付けられたフォームに取り込まれ、ワークフロー変数に保存される場合があります。
* **メールを介して開始されたプロセス**：送信者のメール ID は、直接クエリを実行することができない `tb_job_instance` データベーステーブルの Opaque Blob 列にプロパティとして取得されます。

### ワークフローの開始者または参加者が既知の場合のプロセスインスタンス ID の識別 {#initiator-participant}

ワークフロー開始者または参加者のプロセスインスタンス ID を識別するには、次の手順を実行します。

1. AEM Forms サーバーデータベースで次のコマンドを実行して、`edcprincipalentity` データベーステーブルからワークフローイニシエーターまたは参加者のプリンシパル ID を取得します。

   ```sql
   select id from edcprincipalentity where canonicalname='user_ID'
   ```

   クエリを実行すると、指定された `user_ID` のプリンシパル ID が返されます。

1. （**ワークフローイニシエーターの場合**）次のコマンドを実行して、`tb_task` データベーステーブルからイニシエーターのプリンシパル ID に関連付けられたすべてのタスクを取得します。

   ```sql
   select * from tb_task where start_task = 1 and create_user_id= 'initiator_principal_id'
   ```

   クエリを実行すると、指定された `initiator`_`principal_id` により開始されたタスクが返されます。タスクには次の 2 つのタイプがあります。

   * **完了したタスク**：これらのタスクは既に送信されており、`process_instance_id` フィールドには英数字の値が表示されます。送信済みタスクのすべてのプロセスインスタンス ID をメモして、手順を続行します。
   * **開始されたが完了していないタスク**：これらのタスクは開始されていますが、まだ送信されていません。これらのタスクの `process_instance_id` フィールドの値は、**0**（ゼロ）になります。この場合、対応するタスク ID をメモして、[オーファンタスクの操作](#orphan)を参照してください。

1. （**ワークフロー参加者の場合**）次のコマンドを実行して、`tb_assignment` データベーステーブルからイニシエーター用のプロセス参加者のプリンシパル ID に関連付けられたプロセスインスタンス ID を取得します。

   ```sql
   select distinct a.process_instance_id from tb_assignment a join tb_queue q on a.queue_id = q.id where q.workflow_user_id='participant_principal_id'
   ```

   クエリは、参加者がタスクを送信しなかったプロセスも含め、参加者に関連付けられたすべてのプロセスのインスタンス ID を返します。

   送信済みタスクのすべてのプロセスインスタンス ID をメモして、手順を続行します。

   オーファンタスクまたは `process_instance_id` が 0（ゼロ）であるタスクの場合、該当するタスク ID をメモして、[オーファンタスクの操作](#orphan)を参照してください。

1. [プロセスインスタンス ID に基づいてワークフローインスタンスからユーザーデータを削除する](/help/forms/using/forms-workflow-jee-handling-user-data.md#purge)節の手順に従って、特定されたプロセスインスタンス ID のユーザーデータを削除します。

### ユーザーデータがプリミティブ変数に格納されている場合のプロセスインスタンス ID の特定 {#primitive}

ワークフローは、ユーザーデータがデータベース内の Blob として格納される変数に取得されるように設計できます。このような場合、ユーザーデータを次のプリミティブ型変数のいずれかに格納されている場合にのみ、クエリを実行できます。

* **文字列**：ユーザー ID が直接または部分文字列として含まれ、SQL を使用してクエリできます。
* **数値**：ユーザー ID が直接含まれます。
* **XML**：ユーザー ID を、データベース内のテキスト列として保存されたテキスト内のサブ文字列として含み、文字列と同様にクエリできます。

以下の手順を実行して、プリミティブ型変数にデータを格納するワークフローに、そのユーザーのデータが含まれているかどうかを判断します。

1. 次のデータベースコマンドを実行します。

   ```sql
   select database_table from omd_object_type where name='pt_<app_name>/<workflow_name>'
   ```

   クエリを実行すると、指定されたアプリケーション（`app_name`）およびワークフロー（`workflow_name`）に `tb_<number>` 形式でテーブル名が返されます。

   >[!NOTE]
   >
   >ワークフローがアプリケーション内のサブフォルダーにネストされている場合、`name` プロパティの値は複合型にすることができます。ワークフローへの正確なフルパスを指定するようにしてください。これは、`omd_object_type` データベーステーブルから取得できます。

1. `tb_<number>` テーブルスキーマを確認します。このテーブルには、指定したワークフローのユーザーデータを格納する変数が含まれています。 テーブル内の変数は、ワークフロー内の変数に対応しています。

   ユーザー ID を含むワークフロー変数に対応する変数を特定し、メモします。 識別された変数がプリミティブ型の場合は、クエリを実行して、ユーザー ID に関連付けられたワークフローインスタンスを特定できます。

1. 次のデータベースコマンドを実行します。このコマンドでは、`user_var` がユーザー ID を含むプリミティブ型の変数です。

   ```sql
   select process_instance_id from <tb_name> where <user_var>=<user_ID>
   ```

   クエリを実行すると、指定された `user_ID` に関連付けられたすべてのプロセスインスタンス ID が返されます。

1. [プロセスインスタンス ID に基づいてワークフローインスタンスからユーザーデータを削除する](/help/forms/using/forms-workflow-jee-handling-user-data.md#purge)節の手順に従って、特定されたプロセスインスタンス ID のユーザーデータを削除します。

### プロセスインスタンス ID に基づいて、ワークフローインスタンスからユーザーデータをパージします {#purge}

ユーザーに関連付けられたプロセスインスタンス ID を識別したら、以下の手順を実行して、各プロセスインスタンスからユーザーデータを削除します。

1. 次のコマンドを実行して、`tb_process_instance` テーブルからプロセスインスタンスの永続的呼び出し ID およびステータスを取得します。

   ```sql
   select long_lived_invocation_id, status from tb_process_instance where id='process_instance_id'
   ```

   クエリを実行すると、指定された `process_instance_id` の永続的呼び出し ID およびステータスが返されます。

1. パブリック `ProcessManager` クライアント（`com.adobe.idp.workflow.client.ProcessManager`）のインスタンスを、適切に接続設定された `ServiceClientFactory` インスタンスを使用して作成します。

   詳しくは、 Java API リファレンス ( [クラス ProcessManager](https://helpx.adobe.com/jp/experience-manager/6-3/forms/ProgramLC/javadoc/com/adobe/idp/workflow/client/ProcessManager.html).

1. ワークフローインスタンスのステータスを確認します。 ステータスが 2（COMPLETE）または 4（TERMINATED）以外の場合、次のメソッドを呼び出して最初にインスタンスを停止します。

   `ProcessManager.terminateProcess(<long_lived_invocation_id>)`。

1. 次のメソッドを呼び出して、ワークフローインスタンスを削除します。

   `ProcessManager.purgeProcessInstance(<long_lived_invocation_id>)`

   `purgeProcessInstance` メソッドを使用すると、AEM Forms サーバーデータベースおよび GDS から、指定された呼び出し ID のすべてのデータが完全に削除されます（設定が行われている場合）。

### オーファンタスクの操作 {#orphan}

オーファンタスクとは、プロセスが開始されたがまだ送信されていないタスクを指します。 この場合、`process_instance_id` は **0**（ゼロ）になります。したがって、プロセスインスタンス ID を使用してオーファンタスク用に保存されたユーザーデータをトレースすることはできません。 ただし、オーファンタスクのタスク ID を使用してトレースできます。 [ワークフローイニシエーターまたは参加者が分かっている場合のプロセスインスタンス ID の特定](/help/forms/using/forms-workflow-jee-handling-user-data.md#initiator-participant)で説明されているように、ユーザーの `tb_task` テーブルからタスク ID を特定することができます。

タスク ID を取得したら、次の手順を実行して、GDS およびデータベースからオーファンタスクを含む関連ファイルとデータをパージします。

1. AEM Formsサーバーデータベースで次のコマンドを実行して、識別されたタスク ID の ID を取得します。

   ```sql
   select id from tb_form_data where task_id=<task_id>
   ```

   クエリを実行すると、ID のリストが返されます。 次のように、返された ID（`fd_id`）ごとにセッション ID 文字列のリストを作成します。

   * _ `wfattach<task_id>`
   * `_wftask<fd_id>`
   * `_wftaskformid<fd_id>`

1. GDS がファイルシステムを指すかデータベースを指すかに応じて、次のいずれかの手順を実行します。

   1. **ファイルシステム内の GDS**

      GDS ファイルシステムでは、次の手順に従います。

      1. 以下のセッション ID 文字列を拡張子として持つファイルを検索します。

      * `_wfattach<task_id>`
      * `_wftask<fd_id>`
      * `_wftaskformid<fd_id>`

      これらの拡張子を持つファイルはマーカーファイルです。 ファイル名と共に次の形式で保存されます。

      `<file_name_guid>.session<session_id_string>`

      1. すべてのマーカーファイルおよび `<file_name_guid>` と同じファイル名を持つファイルをファイルシステムから削除します。

   1. **データベース内の GDS**

      各セッション ID に対して次のコマンドを実行します。

      ```sql
      delete from tb_dm_chunk where documentid in (select documentid from tb_dm_session_reference where sessionid=<session_id>)
      delete from tb_dm_session_reference where sessionid=<session_id>
      delete from tb_dm_deletion where sessionid=<session_id>
      ```

1. 次のコマンドを実行して、AEM Formsサーバーデータベースからタスク ID のデータを削除します。

   ```sql
   delete from tb_task_acl where task_id=<task_id>
   delete from tb_task_attachment where task_id=<task_id>
   delete from tb_form_data where task_id=<task_id>
   delete from tb_assignment where task_id=<task_id>
   delete from tb_task where id=<task_id>
   ```
