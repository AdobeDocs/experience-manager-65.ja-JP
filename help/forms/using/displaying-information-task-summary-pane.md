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


# タスクの概要ペインでの情報の表示  {#displaying-information-in-the-task-summary-pane}

AEM Forms ワークスペースでタスクを開くと、タスクの概要ペインはタスクのサマリーを表示できます。タスクに対するこの追加の関連情報は、AEM Forms ワークスペースのエンドユーザーにとってより価値のあるものになります。

AEM Formsワークスペースでは、タスクの概要ペインで選択したWebページを表示できます。 Workbench を使用してタスクの概要ペインを表示するためのプロセスを作成することができます。

1. Workbench で「Assign Task」処理を作成します。「Assign Task」操作についての詳細は、[Workbench ヘルプ](https://help.adobe.com/en_US/AEMForms/6.1/WorkbenchHelp/)のサービスリファレンストピックを参照してください。

   >[!NOTE]
   >
   >タスクの概要 URL がある場合は、タスクの概要の表示がデフォルトでフォーム表示の代わりに開きます。この場合は、ユーザーが「Assign Task」で「Open the form in maximized mode」オプションを有効にしている場合でも、フォームは最大化モードで開きません。

1. タスクの概要 URL フィールドを設定します。リテラル値、テンプレート、変数、または XPath 式を指定できます。
1. タスクの概要ページに関する情報を表示する例を以下に示します。

   * `https://'[server]:[port]'/lc/crx/de`のCRXDE Lite環境にログインします。
   * `Create a node`**SampleSummary** ` under `/` with type `content:`. In the properties of this node, add `unstructuredsling:` of type String and value ``. In the Access Control List of this node, add an entry for `resourceTypeSampleSummaryPERM_WORKSPACE_` allowing `USERjcr:read` privileges.`
   * `Create a folder`**SampleSummary** の下 `/apps`に表示されます。`/apps/SampleSummary`のアクセス制御リストで、`jcr:readprivileges`を許可する`PERM_WORKSPACE_USER`のエントリを追加します。
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

   * タスクの割り当て手順で、タスクの概要urlの値を`/lc/content/SampleSummary.html`に設定します。
   * このタスクの割り当て手順に関連付けられたタスクがAEM Formsのワークスペースで開かれると、`/apps/SampleSummary`の`html.esp`がタスクの概要ペインに表示されます。
