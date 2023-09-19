---
title: ホーム画面
description: AEM Formsアプリのホーム画面のコンポーネントの説明
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: 6c6fb516-1b11-4da4-b638-4388a070e397
source-git-commit: 65c5a4442f17e6bc52deaa1588f535a05698083f
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# ホーム画面{#home-screen}

AEM Formsアプリケーションにログインすると、ホーム画面にリダイレクトされます。

## デフォルトのホーム画面 {#default-home-screen}

デフォルトでは、ホーム画面には、スタートポイントとタスク ( 接続サーバーでAEM Forms Workflow が有効になっている場合 ) を含むすべてのフォームと、関連するサムネールが表示されます。 AEM Forms Server でサムネールを指定できます。

次の図では、デフォルトのホーム画面で基本的なコンポーネントに引き出し線の注釈が付けられています。

![フォームアプリケーションのホーム画面](assets/home-screen-1.png)

<!--Click to enlarge

![home-screen-1-1](assets/home-screen-1-1.png)-->

1. **メニューボタン**：「**メニュー**」ボタンをタップして、タスク、フォーム、アウトボックス、設定に移動します。AEM FormsアプリがAEM Forms JEE サーバーに接続されている場合は、「タスク」オプションが表示されます。 「タスク」オプションは、プロセス内のタスクから作成されたドラフトも保存します。 AEM Forms OSGi サーバーでは、「Tasks」オプションは非表示になっています。 Outbox は、サーバーと同期する前に、保存されたフォームとドラフトを保存します。 アプリの実行時に、Outbox に保存されているすべてのフォームとドラフトがAEM Forms Server にアップロードされます [サーバーと同期済み](../../forms/using/sync-app.md). 設定については、[一般設定の更新](../../forms/using/update-general-settings.md)を参照してください。
1. **タスクまたはフォーム**：作業対象のタスクまたはフォームがリストからタップされます。
1. **横省略記号**：フォームでアクションが使用可能であることを示します。 省略記号をタップすると、作成者が指定したアクションと説明が表示されます。 「**ドラフトを削除**」および「**完了**」オプションは、省略記号をタップすると表示されます。
1. **更新アイコン**：アプリをAEM Forms Server と同期できるように、更新アイコンをタップします。

### ホーム画面のカスタマイズ {#customizing-the-home-screen}

![一般設定](assets/gen-settings.png)

アプリケーションの「**[一般設定](../../forms/using/update-general-settings.md)**」か、または HTML Workspace の「**環境設定**」タブから、アプリケーションのデフォルトのホーム画面を変更できます。

アプリのホーム画面設定に加えた変更は、現在ログインしているユーザーまたは現在のモバイルデバイスのユーザーのホーム画面に影響します。

ただし、HTMLWorkspace での変更は、AEM Forms Server にログインしているすべてのAEM Formsアプリユーザーに影響します。
