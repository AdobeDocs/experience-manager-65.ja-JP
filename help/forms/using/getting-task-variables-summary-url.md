---
title: サマリー URLでのタスク変数の取得
description: タスクに関する情報を再利用し、タスクを要約または説明するサマリ URL を生成する方法。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: b5e27b54-d141-48dd-a4ed-dd0a691319a5
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 20%

---

# サマリー URLでのタスク変数の取得 {#getting-task-variables-in-summary-url}

概要ページには、タスクに関する情報が表示されます。 この記事では、サマリーページでタスクに関する情報を再利用する方法について説明します。

このサンプルオーケストレーションでは、従業員は休暇申請フォームを送信します。 申込フォームは、従業員のマネージャーに承認を求めます。

1. resourceType のサンプルHTMLレンダラー (html.esp) を作成します。 **従業員/PtoApplication**.

   レンダラーは、次のプロパティがノードに設定されると仮定します。

   * 名前
   * empid
   * 理由
   * duration

   >[!NOTE]
   >
   >このレンダラーはサマリーページのテンプレートです。

   このレンダラーの以下のサンプルコードは、

   `apps/Employees/PtoApplication/html.esp`

   ```html
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

1. オーケストレーションを変更して、送信されたフォームデータから 4 つのプロパティを抽出します。 その後、CRX にタイプのノードを作成します。 **従業員/PtoApplication**&#x200B;に設定され、プロパティが設定されます。

   1. プロセスの作成 **PTO 概要を作成** を呼び出し、これをサブプロセスとして使用してから、 **タスクを割り当て** 操作をオーケストレーションで実行します。
   1. **employeeName**、**employeeID**、**ptoReason**、**totalDays** および **nodeName** を新しいプロセスで入力変数として定義します。これらの変数は送信されたフォームデータとして渡されます。

      出力変数も定義します。 **ptoNodePath** 概要 URL の設定時に使用される

   1. **create PTO summary** プロセスで、**set value** コンポーネントを使用して **nodeProperty**（**nodeProps**）マップに入力詳細を設定します。

      このマップのキーは、前の手順でHTMLレンダラーで定義したキーと同じである必要があります。

      また、 **sling:resourceType** 値を持つキー **従業員/PtoApplication** をマップに追加します。

   1. サブプロセスの使用 **storeContent** から **ContentRepositoryConnector** サービス **PTO 概要を作成** プロセス。 このサブプロセスは CRX ノードを作成します。

      次の 3 つの入力変数が必要です。

      * **フォルダーパス**：新しい CRX ノードが作成されるパス。 パスを次のように設定します。 **/content**.
      * **ノード名**：入力変数 nodeName をこのフィールドに割り当てます。 これは固有のノード名文字列です。
      * **ノードタイプ**：タイプを **nt:unstructured** として定義します。このプロセスの出力は nodePath です。 nodePath は、新しく作成されたノードの CRX パスです。 ndoePath は、 **PTO を作成** 要約プロセス。

   1. 送信されたフォームデータ (**employeeName**, **employeeID**, **ptoReason**、および **totalDays**) を新しいプロセスへの入力として使用する **PTO 概要を作成**. 出力を次のように取り込みます。 **ptoSummaryNodePath**.

1. 概要 URL を、サーバーの詳細と共に含まれる XPath 式として定義します。 **ptoSummaryNodePath**.

   XPath：`concat('https://[*server*]:[*port*]/lc',/process_data/@ptoSummaryNodePath,'.html')`。

AEM Forms Workspace で、タスクを開くと、概要 URL が CRX ノードにアクセスし、HTMLレンダラーに概要が表示されます。

概要レイアウトは、プロセスを変更せずに変更できます。 HTMLレンダラーは、サマリを適切に表示します。
