---
title: タスクの概要ペインでの情報の表示
description: AEM Forms Workspace では、タスクの概要ペインを設定して、タスクを要約したり、他の Web ページを表示したりできます。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 0b3087fe-a3fb-4eac-ad4b-c123526e8195
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 36%

---

# タスクの概要ペインでの情報の表示 {#displaying-information-in-the-task-summary-pane}

AEM Forms Workspace でタスクを開くと、タスクの概要ペインにタスクの概要が表示されます。 タスクに関するこの追加の関連情報により、AEM Forms Workspace のエンドユーザーにとってより多くの価値がもたらされます。

AEM Forms Workspace を使用すると、選択した Web ページを [ タスクの概要 ] ペインに表示できます。 Workbench を使用してタスクの概要ペインを表示するためのプロセスを作成することができます。

1. Workbench でタスクの割り当てプロセスを作成します。 「Assign Task」操作の詳細については、「Service Reference」( [Workbench ヘルプ](https://help.adobe.com/ja_JP/AEMForms/6.1/WorkbenchHelp/).

   >[!NOTE]
   >
   >TaskSummary URL が存在する場合は、デフォルトでは、フォームビューではなくタスクの概要ビューが開きます。 この場合、ユーザーが「タスクを割り当て」で「最大化モードでフォームを開く」オプションを有効にしても、フォームは最大化モードで開きません。

1. 「タスクの概要 URL 」フィールドを設定します。 リテラル値、テンプレート、変数または XPath 式を指定できます。
1. 「タスクの概要」ページに情報を表示する例を以下に示します。

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
