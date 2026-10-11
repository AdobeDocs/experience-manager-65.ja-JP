---
title: サマリー URLでのタスク変数の取得
description: タスクについての情報を再利用し、サマリー URL を生成してタスクを要約および説明する方法。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: b5e27b54-d141-48dd-a4ed-dd0a691319a5
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
source-wordcount: '432'
ht-degree: 95%
---
# サマリー URLでのタスク変数の取得 {#getting-task-variables-in-summary-url}

概要ページには、タスクに関連する情報が表示されます。 この記事では、サマリーページでタスクに関連する情報を再利用する方法について説明します。

このサンプルオーケストレーションでは、従業員は休暇申請書を提出します。 申請書は許可を受けるために従業員のマネージャーに渡されます。

1. resourseType **Employees/PtoApplication** のサンプル HTML レンダラー（html.esp）を作成します。

   レンダラーは、次のプロパティがノードに設定されているものとみなします。

   * ename
   * empid
   * reason
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

1. オーケストレーションを変更して送信されたフォームデータから 4 つのプロパティを抽出します。 その後、プロパティを入力してタイプ **Employees/PtoApplication** の CRX にノードを作成します。

   1. プロセス **create PTO summary** を作成し、これをオーケストレーションで **Assign Task** 操作の前のサブプロセスとして使用します。
   1. **employeeName**、**employeeID**、**ptoReason**、**totalDays** および **nodeName** を新しいプロセスで入力変数として定義します。 これらの変数は送信されたフォームデータとして渡されます。

      サマリー URL を設定する際に使用される出力変数 **ptoNodePath** も指定します。

   1. **create PTO summary** プロセスで、**set value** コンポーネントを使用して **nodeProperty**（**nodeProps**）マップに入力詳細を設定します。

      このマップのキーは、前の手順の HTML レンダラーで定義したキーと同じである必要があります。

      また、値&#x200B;**Employees/PtoApplication**&#x200B;の&#x200B;**sling:resourceType** キーをマップに追加します。

   1. **create PTO summary** プロセスの **ContentRepositoryConnector** サービスからサブプロセス **storeContent** を使用します。 このサブプロセスで CRX ノードを作成します。

      これには 3 つの入力変数が必要です。

      * **フォルダーパス**：新しい CRX ノードが作成されるパスです。 パスを **/content** に設定します。
      * **ノード名**：入力変数 nodeName をこのフィールドに割り当てます。 これは固有のノード名文字列です。
      * **ノードタイプ**：タイプを&#x200B;**nt:unstructured**&#x200B;として定義します。 このプロセスの出力は nodePath です。 nodePath は、新しく作成されたノードの CRX パスです。 nodePath は、**create PTO** サマリープロセスの最後の出力になります。

   1. 送信されたフォームデータ（**employeeName**、**employeeID**、**ptoReason** および **totalDays**）を新しいプロセス **create PTO summary** への入力として渡します。 **ptoSummaryNodePath** として出力を取得します。

1. サマリー URL を **ptoSummaryNodePath** と共にサーバー詳細が含まれた XPath 式として定義します。

   XPath：`concat('https://[*server*]:[*port*]/lc',/process_data/@ptoSummaryNodePath,'.html')`。

AEM Forms Workspace で、タスクを開くと、サマリー URL は CRX ノードにアクセスし、HTML レンダラーはサマリーを表示します。

サマリーのレイアウトはプロセスを変更することなく変更できます。 HTML レンダラーはサマリーを適宜表示します。
