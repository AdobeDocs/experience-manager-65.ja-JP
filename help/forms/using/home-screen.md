---
title: ホーム画面
seo-title: Home screen
description: AEM Forms アプリケーションのホーム画面のコンポーネントの説明
seo-description: Description of the components of the AEM Forms app Home screen
uuid: abc95e58-a685-42a9-82ab-4990155945d3
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: ba79479b-4159-4a39-95eb-2285e7ece9d4
docset: aem65
exl-id: 6c6fb516-1b11-4da4-b638-4388a070e397
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '331'
ht-degree: 100%

---

# ホーム画面{#home-screen}

AEM Forms アプリケーションにログインすると、ホーム画面に誘導されます。

## デフォルトのホーム画面 {#default-home-screen}

デフォルトでは、ホーム画面にスタートポイントとタスク（接続したサーバーで AEM Forms Workflow が有効になっている場合）を含むすべてのフォームと、関連付けられたサムネイルが表示されます。サムネイルは、AEM Forms サーバーで指定できます。

次の図では、ホーム画面の基本的なコンポーネントに引き出し線で注釈を付けています。

![フォームアプリケーションのホーム画面](assets/home-screen-1.png)

<!--Click to enlarge

![home-screen-1-1](assets/home-screen-1-1.png)-->

1. **メニューボタン**：「**メニュー**」ボタンをタップして、タスク、フォーム、アウトボックス、設定に移動します。AEM Forms アプリケーションが AEM Forms JEE サーバーに接続されている場合は、タスクオプションが表示されます。タスクオプションでは、プロセス内のタスクから作成されたドラフトも保存されます。AEM Forms OSGi サーバーの場合は、タスクオプションは表示されません。アウトボックスには、サーバーと同期する前に保存されたフォームとタスクが格納されます。アウトボックスに保存されたすべてのフォームとドラフトは、アプリケーションが[サーバーと同期された](../../forms/using/sync-app.md)ときに AEM Forms サーバーにアップロードされます。設定については、[一般設定の更新](../../forms/using/update-general-settings.md)を参照してください。
1. **タスクまたはフォーム**： 作業するタスクまたはフォームを一覧からタップします。
1. **水平省略記号**： フォームに対してアクションが使用できることを示します。省略記号をタップすると、作成者が提供したアクションと説明が表示されます。「**ドラフトを削除**」および「**完了**」オプションは、省略記号をタップすると表示されます。
1. **更新アイコン**：アプリケーションと AEM Forms サーバーを同期させるには、更新アイコンをタップします。

### ホーム画面のカスタマイズ {#customizing-the-home-screen}

![一般設定](assets/gen-settings.png)

アプリケーションの「**[一般設定](../../forms/using/update-general-settings.md)**」か、または HTML Workspace の「**環境設定**」タブから、アプリケーションのデフォルトのホーム画面を変更できます。

アプリケーションのホーム画面の設定への変更は、現在のモバイルデバイスに現在ログオンしているユーザーのホーム画面に反映されます。

ただし、HTML Workspace で行われた変更は、AEM Forms サーバーにログオンしているすべての AEM Forms サーバーユーザーに反映されます。
