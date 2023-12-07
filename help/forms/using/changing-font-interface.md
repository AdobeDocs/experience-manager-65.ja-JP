---
title: インターフェイスのフォントの変更
description: ユーザインターフェイス上のフォントを選択的に変更する方法。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: 226f70f0-8eb4-4724-b496-5801dc6b436f
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 47%

---

# インターフェイスのフォントの変更{#changing-the-font-on-the-interface}

AEM Forms Workspace に表示されるフォントを変更できます。 ユーザーインターフェイスの特定のセクションで使用されるフォントは、スタイルシートの対応するセクションで定義されます。 ユーザーインターフェイス上のフォントを選択的に変更できます。

[AEM Forms Workspace のカスタマイズの一般的な手順](../../forms/using/generic-steps-html-workspace-customization.md)に従います。要件に応じて、CSS、HTML、またはその両方をカスタマイズするための手順に従います。

1. 既存のスタイルのフォントファミリを変更または追加します。
1. フォント要素のフォントファミリインラインを変更またはHTMLします。
1. スタイルを追加し、それをHTML要素に使用します。

例えば、トップナビゲーションバーのアンカーテキストのフォントを「Courier New」に変更するには、次の手順に従います。

1. `https://'[server]:[port]'/lc/crx/de/index.jsp` にアクセスして CRXDE Lite にログインします。
1. 次のいずれかの操作を行います。

   1. 既存のスタイルのフォントファミリを変更するには、/apps/ws/css にある newStyle.css ファイルに次の内容を追加します。

      ```css
      #topnav a {
         font-family: "Courier New";
      }
      ```

   1. フォントファミリインラインを HTML 要素に追加するには、`/libs/ws/js/runtime/templates/appnavigation.html` ファイルを `/apps/ws/js/runtime/templates/appnavigation.html` にコピーします。

      /apps/ws/js/runtime/templates/appnavigation.html ファイルを次のようにして更新します。

      ```jsp
      <li class="process"><a href="#" title="<%= $.t('index.header.topnav.startprocess.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.startprocess.name')%></a></li>
      <li class="todo"><a href="#/todo" title="<%= $.t('index.header.topnav.todo.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.todo.name')%></a></li>
      <li class="track"><a href="#/tracking" title="<%= $.t('index.header.topnav.tracking.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.tracking.name')%></a></li>
      <li class="preference"><a href="#/preferences" title="<%= $.t('index.header.topnav.preferences.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.preferences.name')%></a></li>
      ```

      編集のため /apps/ws/js/registry.js ファイルを開き、`text!/lc/libs/ws/js/runtime/templates/appnavigation.html` を `text!/lc/apps/ws/js/runtime/templates/appnavigation.html` に置き換えます。

   1. フォントファミリを定義するスタイルを追加するには、 /apps/ws/css にある newStyle.css ファイルに次の内容を追加します。

      ```css
      .myNewFontStyle a {
         font-family: "Courier New";
      }
      ```

      HTML要素に font-family インラインを追加するには、/apps/ws/js/runtime/templates にある appnavigation.html ファイルに以下を追加します。

      ```jsp
      <div id="topnav" class="myNewFontStyle">
          <ul>
              <li class="process"><a href="#" title="<%= $.t('index.header.topnav.startprocess.detail')%>" ><%= $.t('index.header.topnav.startprocess.name')%></a></li>
              <li class="todo"><a href="#/todo" title="<%= $.t('index.header.topnav.todo.detail')%>"><%= $.t('index.header.topnav.todo.name')%></a></li>
              <li class="track"><a href="#/tracking" title="<%= $.t('index.header.topnav.tracking.detail')%>" ><%= $.t('index.header.topnav.tracking.name')%></a></li>
              <li class="preference"><a href="#/preferences" title="<%= $.t('index.header.topnav.preferences.detail')%>" ><%= $.t('index.header.topnav.preferences.name')%></a></li>
          </ul>
      </div>
      ```

1. ワークスペースを再起動し、変更を表示するためにブラウザーのキャッシュをクリアします。

![change_font_before](assets/change_font_before.png)

フォントをカスタマイズする前のトップナビゲーションバー

![change_font_after](assets/change_font_after.png)

最初のタブのフォントをカスタマイズした後のトップナビゲーションバー
