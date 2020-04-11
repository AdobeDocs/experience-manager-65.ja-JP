---
title: サマリー URL でのタスク変数の取得
seo-title: サマリー URL でのタスク変数の取得
description: タスクについての情報を再利用し、サマリー URL を生成してタスクを要約および説明する方法。
seo-description: タスクについての情報を再利用し、サマリー URL を生成してタスクを要約および説明する方法。
uuid: 9eab3a6a-a99a-40ae-b483-33ec7d21c5b6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6dc31bec-b02d-47db-a4f4-be8c14c5619e
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# サマリー URL でのタスク変数の取得 {#getting-task-variables-in-summary-url}

要約ページには、タスクに関連する情報が表示されます。この記事では、要約ページでタスクに関連する情報を再利用する方法について説明します。

このサンプルオーケストレーションでは、従業員は休暇申請書を送信します。申請書は許可を受けるために従業員のマネージャーに渡されます。

1. resourseType **Employees/PtoApplication** のサンプル HTML レンダラー（html.esp）を作成します。

   レンダラーは次のプロパティがノードに設定されているものとみなします。

   * ename
   * empid
   * reason
   * duration
   **注意**：このレンダラーは要約ページのテンプレートです。

   このレンダラーの以下のサンプルコードは、

   `apps/Employees/PtoApplication/html.esp`

   ```
   <html>
     <body>
       <table>
       <tbody>
       <tr>
           <td>
               <h3>Employee Name: <%= currentNode.ename %></h3>
               <h3>Employee ID: <%= currentNode.eid %></h3>
               <h3>Leave duration: <%= currentNode.duration %> days</h3>
               <h3>Reason: <%= currentNode.reason %></h3>
           </td>
       </tr>
       </tbody>
       </table>
     </body>
   </html>
   ```

1. オーケストレーションを変更して送信されたフォームデータから 4 つのプロパティを抽出します。その後、プロパティを入力してタイプ **Employees/PtoApplication** の CRX にノードを作成します。

   1. プロセス **create PTO summary** を作成し、これをオーケストレーションで **Assign Task** 操作の前のサブプロセスとして使用します。
   1. **employeeName**、**employeeID**、**ptoReason**、**totalDays**、および **nodeName**&#x200B;を新しいプロセスで入力変数として定義します。これらの変数は送信されたフォームデータとして渡されます。

      サマリー URL を設定する際に使用される出力変数 **ptoNodePath**&#x200B;も指定します。

   1. **create PTO summary** プロセスで、**set value** コンポーネントを使用して **nodeProperty**（**nodeProps**）マップに入力詳細を設定します。

      このマップのキーは、前の手順の HTML レンダラーで定義したキーと同じである必要があります。

      また、マップに **sling:resourceType** キーを値 **Employees/PtoApplication** と共に追加します。

   1. **create PTO summary** プロセスの **ContentRepositoryConnector** サービスからサブプロセス **storeContent** を使用します。このサブプロセスで CRX ノードを作成します。

      これには 3 つの入力変数が必要です。

      * **フォルダパス**：新しい CRX ノードが作成されるパスです。パスを **/content** に設定します。
      * **ノード名**：入力変数 nodeName をこのフィールドに割り当てます。これは一意のノード名文字列です。
      * **ノードタイプ**:タイプを **nt:unstructuredと定義します**。 このプロセスの出力は nodePath です。nodePath は、新しく作成されたノードの CRX パスです。ndoePath は、**create PTO** 要約プロセスの最後の出力になります。
   1. 送信されたフォームデータ（**employeeName**、**employeeID**、**ptoReason**、および **totalDays**）を新しいプロセス **create PTO summary** への入力として渡します。**ptoSummaryNodePath** として出力を取得します。


1. サマリー URL を **ptoSummaryNodePath** と共にサーバー詳細が含まれた XPath 式として定義します。

   XPath: `concat('https://[*server*]:[*port*]/lc',/process_data/@ptoSummaryNodePath,'.html')`.

AEM Forms Workspace で、タスクを開くと、サマリー URL は CRX ノードにアクセスし、HTML レンダラーはサマリーを表示します。

サマリーのレイアウトはプロセスを変更することなく変更することができます。HTML レンダラーはサマリーを適宜表示します。
