---
title: テーマのカスタマイズ
description: AEM Formsアプリケーションのテーマをカスタマイズする方法を説明します。 HTMLコードと CSS ファイルをカスタマイズして、組織固有の外観と操作性を提供できます。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: 9b8c5933-b783-48f9-b463-15a01e06ee98
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 64%

---

# テーマのカスタマイズ {#theme-customization}

HTMLコードと CSS ファイルをカスタマイズして、AEM Formsアプリに組織固有の独自のルックアンドフィールを提供できます。 例えば、タスクや Startpoint の背景色や高さを変更できます。 次の例に、変更手順を示します。

* 説明の代わりに手順を表示
* 表示ルート数
* 背景のグラデーションの色

## 手順 {#steps}

1. プロジェクトを開きます。

   * iOS の場合、Xcode で `Capture.xcodeproj` を開きます。
   * Android の場合、Eclipse で Android プロジェクトを開きます。
   * Windows の場合、Visual Studio で `MWSWindows.sln` を開きます。

1. テンプレートフォルダーに移動します。

   * Xcode では、**Capture／www／wsmobile／js／runtime／templates** フォルダーに移動します。
   * Eclipse では、**assets／www／wsmobile／js／runtime／templates** フォルダーに移動します。
   * Visual Studio では、**MWSWindows／www／wsmobile／js／runtime／templates** フォルダーに移動します。

1. `template.html` ファイルを開いて編集します。
1. 次の文字列を探します。

   ```jsp
   <%if ( (task.description !== "") && (task.description !== null) && (typeof task.description !== null) && (typeof task.description !== 'undefined') ) {%>
                  <div class="description_details">
                    <%= task.description %>
                  </div>
                 <%} else
   ```

   `<%` に置き換えます。

1. `template.html` ファイル内の次のコードを探します。

   ```jsp
   <ul id="task_menu_list">
                                   <li class="approve" title="<%= task.availableCommands.directCommands[0]%>" data-routename="<%= task.availableCommands.directCommands[0]%>">
                                       <%= task.availableCommands.directCommands[0]%>
                                   </li>
                                   <li class="reject last" title="<%= task.availableCommands.directCommands[1]%>" data-routename="<%= task.availableCommands.directCommands[1]%>">
                                       <%= task.availableCommands.directCommands[1]%>
                                   </li>
   ```

1. 次の行にコメントをつけ、ファイルを保存します。

   ```jsp
   task.availableCommands.directCommands[1]%>">
   <%= task.availableCommands.directCommands[1]%>
   </li>
   ```

1. css フォルダーに移動します。

   * Xcode では、**Capture／www／wsmobile／css** に移動します。
   * Eclipse では、**assets／www／wsmobile／css** に移動します。
   * Visual Studio では、**MWSWindows／www／wsmobile／css** に移動します。

1. `_style.css` ファイルを開いて編集します。
1. 背景画像は、`#323232` を `#fff` に変更します。
1. 変更を保存し、`_style.css` ファイルを閉じます。
1. AEM Formsアプリを開きます。

   AEM Formsアプリに、説明ではなく手順が表示されるようになりました。
