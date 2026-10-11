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
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 100%
---
# ドキュメントへのリンクの更新 {#updating-the-link-to-the-documentation}

AEM Forms Workspace のデフォルトのヘルプコンテンツにアクセスするには、**ヘルプ／Workspace ヘルプ**&#x200B;を選択します。 これは、アドビの web サイトのオンラインドキュメントを指しています。 ただし、それを更新して他の URL を指定するようにすることができます。

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
