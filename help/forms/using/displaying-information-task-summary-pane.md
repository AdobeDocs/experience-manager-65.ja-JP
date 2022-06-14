---
title: タスクの概要ペインでの情報の表示
seo-title: Displaying information in the Task Summary pane
description: AEM Forms ワークスペースでは、タスクの概要ペインを設定して、タスクのサマリを表示したりその他の任意の Web ページを表示したりできます。
seo-description: In AEM Forms workspace, a Task Summary pane can be configured to summarize the task or display any other web page.
uuid: 2fcc3d9f-0ec2-4250-8dc1-9746fd72ea60
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 90d0f584-b598-4b21-85d7-31da5f13d404
exl-id: 0b3087fe-a3fb-4eac-ad4b-c123526e8195
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 100%

---

# タスクの概要ペインでの情報の表示 {#displaying-information-in-the-task-summary-pane}

AEM Forms ワークスペースでタスクを開くと、タスクの概要ペインはタスクのサマリーを表示できます。タスクに対するこの追加の関連情報は、AEM Forms ワークスペースのエンドユーザーにとってより価値のあるものになります。

AEM Forms ワークスペースでは、タスクの概要ペインで選択した web ページを表示できます。Workbench を使用してタスクの概要ペインを表示するためのプロセスを作成することができます。

1. Workbench で「Assign Task」処理を作成します。「Assign Task」操作についての詳細は、[Workbench ヘルプ](https://help.adobe.com/ja_JP/AEMForms/6.1/WorkbenchHelp/)のサービスリファレンストピックを参照してください。

   >[!NOTE]
   >
   >タスクの概要 URL がある場合は、タスクの概要の表示がデフォルトでフォーム表示の代わりに開きます。この場合は、ユーザーが「Assign Task」で「Open the form in maximized mode」オプションを有効にしている場合でも、フォームは最大化モードで開きません。

1. タスクの概要 URL フィールドを設定します。リテラル値、テンプレート、変数、または XPath 式を指定できます。
1. タスクの概要ページに関する情報を表示する例を以下に示します。

   * `https://'[server]:[port]'/lc/crx/de` で CRXDE Lite 環境ログインします。
   * `Create a node`**SampleSummary** ` under `/content` with type `nt:unstructured`. In the properties of this node, add `sling:resourceType` of type String and value `SampleSummary`. In the Access Control List of this node, add an entry for `PERM_WORKSPACE_USER` allowing `jcr:read` privileges.`
   * `/apps` の下にある `Create a folder`**SampleSummary**。アクセス制御リスト `/apps/SampleSummary` に、`jcr:readprivileges` を許可する `PERM_WORKSPACE_USER` のエントリを追加します。
   * `Create a file `html.esp` at `/apps/SampleSummary`. For example, add the following lines in `html.esp`.`

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

   * タスクの割り当て手順で、タスクの概要 URL の値を `/lc/content/SampleSummary.html` に設定します。
   * このタスクの割り当て手順に関連付けられたタスクが AEM Forms ワークスペースで開かれると、`/apps/SampleSummary` の `html.esp` はタスクの概要ペインでレンダリングされます。
