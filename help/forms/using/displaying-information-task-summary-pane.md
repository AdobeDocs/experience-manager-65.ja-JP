---
title: タスクの概要ペインでの情報の表示
seo-title: タスクの概要ペインでの情報の表示
description: AEM Forms ワークスペースでは、タスクの概要ペインを設定して、タスクのサマリを表示したりその他の任意の Web ページを表示したりできます。
seo-description: AEM Forms ワークスペースでは、タスクの概要ペインを設定して、タスクのサマリを表示したりその他の任意の Web ページを表示したりできます。
uuid: 2fcc3d9f-0ec2-4250-8dc1-9746fd72ea60
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 90d0f584-b598-4b21-85d7-31da5f13d404
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 68%

---


# タスクの概要ペインでの情報の表示 {#displaying-information-in-the-task-summary-pane}

AEM Forms ワークスペースでタスクを開くと、タスクの概要ペインはタスクのサマリーを表示できます。タスクに対するこの追加の関連情報は、AEM Forms ワークスペースのエンドユーザーにとってより価値のあるものになります。

AEM Formsワークスペースを使用すると、タスクの概要ペインで選択したWebページを表示できます。 Workbench を使用してタスクの概要ペインを表示するためのプロセスを作成することができます。

1. Workbench で「Assign Task」処理を作成します。「Assign Task」操作についての詳細は、[Workbench ヘルプ](https://help.adobe.com/en_US/AEMForms/6.1/WorkbenchHelp/)のサービスリファレンストピックを参照してください。

   >[!NOTE]
   >
   >タスクの概要 URL がある場合は、タスクの概要の表示がデフォルトでフォーム表示の代わりに開きます。この場合は、ユーザーが「Assign Task」で「Open the form in maximized mode」オプションを有効にしている場合でも、フォームは最大化モードで開きません。

1. タスクの概要 URL フィールドを設定します。リテラル値、テンプレート、変数、または XPath 式を指定できます。
1. タスクの概要ページに関する情報を表示する例を以下に示します。

   * でCRXDE Lite環境にログインし `https://'[server]:[port]'/lc/crx/de`ます。
   * `Create a node`**SampleSummary **` under `/` with type `contentnt:`. In the properties of this node, add `unstructuredsling:` of type String and value ``. In the Access Control List of this node, add an entry for `resourceTypeSampleSummaryPERM_WORKSPACE_` allowing `USERjcr:read` privileges.`
   * `Create a folder`**SampleSummary **」を参照して`/apps`ください。 のアクセス制御リストで、許可するエントリ`/apps/SampleSummary`を追加`PERM_WORKSPACE_USER`し`jcr:readprivileges`ます。
   * `Create a file `html.esp` at `/apps/`. For example, add the following lines in `SampleSummaryhtml.esp`.`

   ```html
   <html>
       <body>
           <h1>Sample Summary</h1>
           <br/>
           <p>Hello Sir!
               <br/>
               This is sample summary page for this task.
           </p>
       </body>
   </html>
   ```

   * Set the value of task summary url as `/lc/content/SampleSummary.html` in Assign Task step.
   * When the task associated with this Assign Task step is opened in AEM Forms workspace, the `html.esp` at `/apps/SampleSummary` is rendered in task summary pane.
