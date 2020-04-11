---
title: インターフェイスのフォントの変更
seo-title: インターフェイスのフォントの変更
description: ユーザーインタフェイス上でフォントを選択して変更する方法。
seo-description: ユーザーインタフェイス上でフォントを選択して変更する方法。
uuid: 421fdd24-441a-4092-8c52-f3ed3d5d5671
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 9fcb80b4-cbc2-48a5-afd1-4f3bc50bc503
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# インターフェイスのフォントの変更{#changing-the-font-on-the-interface}

AEM Forms Workspace に表示されているフォントを変更することができます。ユーザーインターフェイスの特定のセクションで使用されているフォントは、スタイルシートの対応するセクションに定義されています。フォントは選択的にユーザーインタフェイス上で変更することができます。

Follow the [Generic steps for AEM Forms workspace customization](../../forms/using/generic-steps-html-workspace-customization.md) and depending on your requirements, follow the steps for customizing CSS, HTML, or both.

1. 既存のスタイルのフォントファミリを変更または追加します。
1. HTML 要素でフォントファミリインラインを変更または追加します。
1. スタイルを追加して HTML 要素で使用します。

例えば、トップナビゲーションバーのアンカーテキストのフォントを「Courier New」に変更するには、次の手順に従います。

1. にアクセスしてCRXDE Liteにログインしま `https://'[server]:[port]'/lc/crx/de/index.jsp`す。
1. 次のいずれかの操作をおこないます。

   1. 既存のスタイルでフォントファミリーを変更するには、/apps/ws/css にある newStyle.css ファイルに以下を追加します。

      ```css
      #topnav a {
         font-family: "Courier New";
      }
      ```

   1. To add the font-family inline for the HTML element, copy the `/libs/ws/js/runtime/templates/appnavigation.html` file to `/apps/ws/js/runtime/templates/appnavigation.html`.

      /apps/ws/js/runtime/templates/appnavigation.html ファイルを次のようにして更新します。

      ```
      <li class="process"><a href="#" title="<%= $.t('index.header.topnav.startprocess.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.startprocess.name')%></a></li>
      <li class="todo"><a href="#/todo" title="<%= $.t('index.header.topnav.todo.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.todo.name')%></a></li>
      <li class="track"><a href="#/tracking" title="<%= $.t('index.header.topnav.tracking.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.tracking.name')%></a></li>
      <li class="preference"><a href="#/preferences" title="<%= $.t('index.header.topnav.preferences.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.preferences.name')%></a></li>
      ```

      Open the /apps/ws/js/registry.js file for editing and replace `text!/lc/libs/ws/js/runtime/templates/appnavigation.html` with `text!/lc/apps/ws/js/runtime/templates/appnavigation.html`.

   1. フォントファミリを定義するスタイルを追加するには、/apps/ws/css にある newStyle.css ファイルに以下を追加します。

      ```css
      .myNewFontStyle a {
         font-family: "Courier New";
      }
      ```

      フォントファミリインラインを HTML 要素に追加するには、/apps/ws/js/runtime/templates にある appnavigation.html ファイルに以下を追加します。

      ```css
      <div id="topnav" class="myNewFontStyle">
          <ul>
              <li class="process"><a href="#" title="<%= $.t('index.header.topnav.startprocess.detail')%>" ><%= $.t('index.header.topnav.startprocess.name')%></a></li>
              <li class="todo"><a href="#/todo" title="<%= $.t('index.header.topnav.todo.detail')%>"><%= $.t('index.header.topnav.todo.name')%></a></li>
              <li class="track"><a href="#/tracking" title="<%= $.t('index.header.topnav.tracking.detail')%>" ><%= $.t('index.header.topnav.tracking.name')%></a></li>
              <li class="preference"><a href="#/preferences" title="<%= $.t('index.header.topnav.preferences.detail')%>" ><%= $.t('index.header.topnav.preferences.name')%></a></li>
          </ul>
      </div>
      ```

1. Workspace を再起動して変更が表示されるようにブラウザのキャッシュをクリアします。

![change_font_before](assets/change_font_before.png)

フォントをカスタマイズする前のトップナビゲーションバー

![change_font_after](assets/change_font_after.png)

最初のタブのフォントをカスタマイズした後のトップナビゲーションバー
