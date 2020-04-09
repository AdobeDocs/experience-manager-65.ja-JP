---
title: スタートポイントの使用
seo-title: スタートポイントの使用
description: Workbench で定義されたモバイルデバイスからAEM Forms プロセスを操作する手順。
seo-description: Workbench で定義されたモバイルデバイスからAEM Forms プロセスを操作する手順。
uuid: 1c4b4c86-cbdb-4e72-b0eb-7f8a2f5dcdde
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 1ea60fb2-cf9f-4a87-bd8e-98150e668456
docset: aem65
translation-type: tm+mt
source-git-commit: 72a582b7ac19322b81fd1a92de8fce34e55b9db1

---


# スタートポイントの使用{#working-with-startpoints}

スタートポイントは Workbench で作成されたプロセスを呼び出します。これはフォームの送信時にプロセスを呼び出すフォームに関連付けられています。プロセスについて理解するには、「[Geometrixx Finance リファレンスサイトのチュートリアル](../../forms/using/finance-reference-site-walkthrough.md)」を参照してください。

>[!NOTE]
>
>この概念について参照すると、スタートポイント、スタートプロセス、フォームという用語が区別なく使用される場合があります。

To initiate a process from the AEM Forms app, you need to have a startpoint of type **Workspace** in your process. また、スタートポイントに対して「**[!UICONTROL Mobile Workspace でスタートポイントを表示する]**」オプションをオンにする必要もあります。

![mws_startpoint_select_option](assets/mws_startpoint_select_option.png)

**Workbench で定義されたプロセスを開始するには**

1. AEM Forms アプリケーションで使用可能なスタートポイントを表示するには、[ホーム画面](../../forms/using/home-screen.md)に移動してください。
1. On the **[!UICONTROL Home]** screen, by default, the **[!UICONTROL All Forms]** list is displayed.

   スタートポイントはフォームに関連付けられています。スタートポイントに関連付けられたフォームをリストでタップして開きます。

   スタートポイントに関連付けられているフォームが開きます。

1. **[!UICONTROL スタートポイント]**&#x200B;フォームに、詳細情報を入力します。

   「[添付ファイル](../../forms/using/add-attachments.md)」ボタンを使用して、このタスクに注釈を追加できます。

1. After you fill the form, tap the **[!UICONTROL Submit]** button.

アプリケーションがオフラインの場合、フォームとそのデータは Outbox フォルダーに保存されます。

アプリケーションがオンラインの場合、タスクは AEM Forms Server と同期され、プロセスで指定されたユーザーに割り当てられます。

タスクリスト内のタスクを実行するには、「[タスクを開く](/help/forms/using/open-task.md)」を参照してください。

[サポートへのお問い合わせ](https://www.adobe.com/jp/account/sign-in.supportportal.html)
