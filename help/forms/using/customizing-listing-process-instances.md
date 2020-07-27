---
title: プロセスインスタンスのリストのカスタマイズ
seo-title: プロセスインスタンスのリストのカスタマイズ
description: AEM Forms Workspace のプロセスインスタンスで表示されるプロパティをカスタマイズする方法。
seo-description: AEM Forms Workspace のプロセスインスタンスで表示されるプロパティをカスタマイズする方法。
uuid: 3b55d9b9-7f73-46dd-9eb6-42be218440a1
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 40d7d43f-ee0a-4e34-ae93-20c9c940f76b
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '302'
ht-degree: 81%

---


# プロセスインスタンスのリストのカスタマイズ {#customizing-the-listing-of-process-instances}

プロセスインスタンスリストは、AEM Forms Workspace のトラッキングタブに表示されます。

プロセスインスタンスリストで、各プロセスインスタンスに対して AEM Forms Workspace はそのインスタンスのいくつかのプロパティを表示します。次のプロパティが各プロセスインスタンスで使用できます。これらのプロパティは、プロセスインスタンスコンポーネントモデルに属性として保存され、表示とテンプレートで使用できます。

<table>
 <tbody>
  <tr>
   <td><strong>Property</strong></td>
   <td><strong>コメント</strong></td>
  </tr>
  <tr>
   <td>description</td>
   <td>プロセスインスタンスの説明。</td>
  </tr>
  <tr>
   <td>initiator</td>
   <td>プロセスインスタンスのイニシエーターの名前。</td>
  </tr>
  <tr>
   <td>initiatorId</td>
   <td>プロセスインスタンスのイニシエーターの ID。</td>
  </tr>
  <tr>
   <td>processCompleteTime</td>
   <td>プロセスが完了したときのタイムスタンプ。</td>
  </tr>
  <tr>
   <td>processInstanceId</td>
   <td>プロセスインスタンスの ID。</td>
  </tr>
  <tr>
   <td>processInstanceStatus</td>
   <td>0 = 起動済み<br /> 1 = 実行中<br /> 2 = 完了<br /> 3 = 完了中<br /> 4 = 終了<br /> 5 = 終了中<br /> 6 = 休止<br /> 7 = 休止中<br /> 8 = 休止解除中</td>
  </tr>
  <tr>
   <td>processName</td>
   <td>プロセスの名前。</td>
  </tr>
  <tr>
   <td>processStartTime</td>
   <td>プロセスが開始したときのタイムスタンプ。</td>
  </tr>
  <tr>
   <td>processVariables</td>
   <td>プロセス変数のオブジェクトの配列。各プロセス変数オブジェクトは、<strong>名前</strong>（プロセス変数の名前）、<strong>値</strong>（プロセス変数の値）、および<strong>タイプ</strong>（プロセス変数のタイプ）を含みます。</td>
  </tr>
 </tbody>
</table>

**例:**

To display the `description` property of the process instance in the process instance card, perform the following steps.

1. [AEM Forms Workspace のカスタマイズの一般的な手順](/help/forms/using/generic-steps-html-workspace-customization.md)に従います。
1. 以下の操作を実行してください。

   1. 存在しない場合は、/libs/ws/js/runtime/templates/processinstance.html を /apps/ws/js/runtime/templates/ にコピーします。「**すべて保存**」をクリックします。
   1. processinstance.html内の追加class = &#39;processDescription&#39;を持つプロセス説明div。

   ```jsp
   <div class="processDescription" title="<%= description%>"><%= description%></div>
   ```

1. 以下の操作を実行してください。

   1. /apps/ws/js/registry.js を開いて編集します。
   1. 検索して、 `text!/lc/libs/ws/js/runtime/templates/processinstance.html`apps `text!/lc/`****/ws/js/runtime/templates/processinstance.htmlで置き換えます。

1. 上記の変更には、次のようにしてスタイルシート /apps/ws/css/newStyle.css にエントリを追加することによって、CSS ファイルを更新する必要があります。

   ```css
   .processinstance .processDescription {
    <!--Dummy values, need to be configured by user as per requirement as well as user can add or delete any property depending upon requirement-->
       width : 250px;
       font-size : 11pt;
       padding : 2px;
   }
   ```
