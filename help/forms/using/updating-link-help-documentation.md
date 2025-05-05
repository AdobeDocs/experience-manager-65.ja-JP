---
title: ドキュメントへのリンクの更新
description: AEM Forms Workspace の Workspace Help のリンク先を更新して、カスタムドキュメントリンクに指定する方法。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: ca637bea-05c1-4920-9283-e782f07607de
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: Admin, User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 100%

---

# ドキュメントへのリンクの更新 {#updating-the-link-to-the-documentation}

AEM Forms Workspace のデフォルトのヘルプコンテンツにアクセスするには、**ヘルプ／Workspace ヘルプ**&#x200B;を選択します。これは、アドビの web サイトのオンラインドキュメントを指しています。ただし、それを更新して他の URL を指定するようにすることができます。

デフォルトのヘルプ URL を変更する場合は以下の使用事例を考慮してください。

* 選択した言語でローカライズされたヘルプを指定する場合。
* カスタマイズされた Workspace にカスタマイズされたヘルプコンテンツを指定する場合。

オンラインドキュメントの URL を更新するには、「[カスタマイズの一般的な手順](/help/forms/using/generic-steps-html-workspace-customization.md)」の後に以下の手順を実行します。

1. `userinfo.html` ファイルを `/libs/ws/js/runtime/templates` から `/apps/ws/js/runtime/templates` にコピーします。
1. 変更点：

   ```html
   <ul class="helpmenu">
     <li>
       <a href="https://www.adobe.com/go/learn_aemforms_documentation_63_jp" title="<%= $.t('index.header.dropdown.WorkspaceHelp')%>" target="_blank"><%= $.t('index.header.dropdown.WorkspaceHelp')%></a>
     </li>
   ```

   コピー先：

   ```html
   <ul class="helpmenu">
     <li>
       <a href="<!--place new help url here-->" title="<%= $.t('index.header.dropdown.WorkspaceHelp')%>" target="_blank"><%= $.t('index.header.dropdown.WorkspaceHelp')%></a>
     </li>
   ```

1. 以下の操作を実行します。

   1. /apps/ws/js/registry.js を開いて編集します。
   1. `text!/lc/libs/ws/js/runtime/templates/userinfo.html` を検索して `text!/lc/apps/ws/js/runtime/templates/userinfo.html` に置換します。
