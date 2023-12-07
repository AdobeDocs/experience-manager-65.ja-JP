---
title: ドキュメントへのリンクの更新
description: AEM Forms Workspace の Workspace ヘルプリンクの宛先を更新して、カスタムドキュメントリンクを指すようにする方法。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: ca637bea-05c1-4920-9283-e782f07607de
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 43%

---

# ドキュメントへのリンクの更新 {#updating-the-link-to-the-documentation}

AEM Forms Workspace のデフォルトのヘルプコンテンツにアクセスするには、 **ヘルプ/Workspace ヘルプ**. Adobeの Web サイト上のオンラインドキュメントを指しています。 ただし、他の URL を指すように更新することもできます。

デフォルトのヘルプ URL を変更する場合は、次の使用例を検討してください。

* 選択した言語でローカライズされたヘルプを提供する場合。
* カスタマイズされた Workspace にカスタマイズされたヘルプコンテンツを指定する場合。

オンラインドキュメントの URL を更新するには、「[カスタマイズの一般的な手順](/help/forms/using/generic-steps-html-workspace-customization.md)」の後に以下の手順を実行します。

1. `userinfo.html` ファイルを `/libs/ws/js/runtime/templates` から `/apps/ws/js/runtime/templates` にコピーします。
1. 変更点：

   ```html
   <ul class="helpmenu">
     <li>
       <a href="https://www.adobe.com/go/learn_aemforms_documentation_63" title="<%= $.t('index.header.dropdown.WorkspaceHelp')%>" target="_blank"><%= $.t('index.header.dropdown.WorkspaceHelp')%></a>
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
