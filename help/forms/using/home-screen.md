---
title: ホーム画面
description: AEM Forms アプリケーションのホーム画面のコンポーネントの説明
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: 6c6fb516-1b11-4da4-b638-4388a070e397
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 100%

---

# ホーム画面{#home-screen}

AEM Forms アプリケーションにログインすると、ホーム画面に誘導されます。

## デフォルトのホーム画面 {#default-home-screen}

デフォルトでは、ホーム画面にスタートポイントとタスク（接続したサーバーで AEM Forms Workflow が有効になっている場合）を含むすべてのフォームと、関連付けられたサムネールが表示されます。サムネールは、AEM Forms サーバーで指定できます。

次の図では、ホーム画面の基本的なコンポーネントに引き出し線で注釈を付けています。

![フォームアプリケーションのホーム画面](assets/home-screen-1.png)

<!--Click to enlarge

![home-screen-1-1](assets/home-screen-1-1.png)-->

1. **メニューボタン**：「**メニュー**」ボタンを選択して、タスク、フォーム、アウトボックス、設定に移動します。AEM Forms アプリケーションが AEM Forms JEE サーバーに接続されている場合は、タスクオプションが表示されます。タスクオプションでは、プロセス内のタスクから作成されたドラフトも保存されます。AEM Forms OSGi サーバーの場合は、タスクオプションは表示されません。アウトボックスには、サーバーと同期する前に保存されたフォームとタスクが格納されます。アウトボックスに保存されたすべてのフォームとドラフトは、アプリケーションが[サーバーと同期された](../../forms/using/sync-app.md)ときに AEM Forms サーバーにアップロードされます。設定については、[一般設定を更新](../../forms/using/update-general-settings.md)を参照してください。
1. **タスクまたはフォーム**：作業するタスクまたはフォームをリストから選択します。
1. **水平省略記号**：フォームに対してアクションが使用できることを示します。省略記号をタップすると、作成者が提供したアクションと説明が表示されます。「**ドラフトを削除**」および「**完了**」オプションは、省略記号を選択すると表示されます。
1. **更新アイコン**：アプリケーションと AEM Forms サーバーを同期させるには、「更新」アイコンを選択します。

### ホーム画面のカスタマイズ {#customizing-the-home-screen}

![一般設定](assets/gen-settings.png)

アプリケーションの「**[一般設定](../../forms/using/update-general-settings.md)**」か、または HTML Workspace の「**環境設定**」タブから、アプリケーションのデフォルトのホーム画面を変更できます。

アプリケーションのホーム画面の設定への変更は、現在のモバイルデバイスに現在ログオンしているユーザーのホーム画面に反映されます。

ただし、HTML Workspace で行われた変更は、AEM Forms サーバーにログオンしているすべての AEM Forms サーバーユーザーに反映されます。
