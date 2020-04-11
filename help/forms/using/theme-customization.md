---
title: テーマのカスタマイズ
seo-title: テーマのカスタマイズ
description: AEM Forms アプリケーションのテーマのカスタマイズ方法
seo-description: AEM Forms アプリケーションのテーマのカスタマイズ方法
uuid: 36632e67-1cc6-416d-ae80-d84bbabab4bd
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: c72f608e-052a-4bf9-b7bc-ddf57483af35
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# テーマのカスタマイズ {#theme-customization}

HTML コードおよび CSS ファイルをカスタマイズし、AEM Forms アプリケーションに組織固有の明確なルック＆フィールを提供することができます。たとえば、タスクまたはスタートポイントの背景色や高さを変更できます。次のことを変更する手順を、以下に例で示します。

* 説明の代わりに手順を表示する
* 表示ルート数
* 背景諧調色

## 手順 {#steps}

1. プロジェクトを開きます。

   * For iOS, open `Capture.xcodeproj` in Xcode
   * Android の場合、Eclipse で Android プロジェクトを開きます。
   * For Windows, open `MWSWindows.sln` in Visual Studio.

1. テンプレートフォルダーに移動します。

   * In Xcode, navigate to the **Capture > www > wsmobile > js > runtime > templates** folder.
   * In Eclipse, navigate to the **assets > www > wsmobile > js > runtime > templates** folder.
   * In Visual Studio, navigate to the **MWSWindows > www > wsmobile > js > runtime > templates** folder.

1. Open the `template.html` file for editing.
1. 次の文字列を探します。

   ```
   <%if ( (task.description !== "") && (task.description !== null) && (typeof task.description !== null) && (typeof task.description !== 'undefined') ) {%>
                  <div class="description_details">
                    <%= task.description %>
                  </div>
                 <%} else
   ```

   Replace it with `<%`.

1. `template.html` ファイル内の次のコードを探します。

   ```
   <ul id="task_menu_list">
                                   <li class="approve" title="<%= task.availableCommands.directCommands[0]%>" data-routename="<%= task.availableCommands.directCommands[0]%>">
                                       <%= task.availableCommands.directCommands[0]%>
                                   </li>
                                   <li class="reject last" title="<%= task.availableCommands.directCommands[1]%>" data-routename="<%= task.availableCommands.directCommands[1]%>">
                                       <%= task.availableCommands.directCommands[1]%>
                                   </li>
   ```

1. 次の行にコメントをつけ、ファイルを保存します。

   ```
   task.availableCommands.directCommands[1]%>">
   <%= task.availableCommands.directCommands[1]%>
   </li>
   ```

1. css フォルダーに移動します。

   * In Xcode, navigate to **Capture > www > wsmobile > css**.
   * In Eclipse, navigate to **assets > www > wsmobile > css**.
   * In Visual Studio, navigate to **MWSWindows > www > wsmobile > css**.

1. Open the `_style.css` file for editing.
1. For Background image, change `#323232` to `#fff`.
1. Save the changes and close `_style.css` file.
1. AEM Forms アプリケーションを開きます。

   AEM Forms アプリケーションには、説明の代わりに手順が表示されるようになっています。
