---
title: スタートポイントの使用
description: Workbench で定義されたモバイルデバイスから Adobe Experience Manager Forms プロセスを操作する手順。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: d5970f90-2899-43a5-a3a0-61a2c844d919
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '235'
ht-degree: 100%

---

# スタートポイントの使用{#working-with-startpoints}

スタートポイントは Workbench で作成されたプロセスを呼び出します。これはフォームの送信時にプロセスを呼び出すフォームに関連付けられています。

>[!NOTE]
>
>この概念について参照すると、スタートポイント、スタートプロセス、フォームという用語が区別なく使用される場合があります。

Adobe Experience Manager（AEM）Forms アプリケーションからプロセスを開始するには、プロセスで&#x200B;**ワークスペース**&#x200B;タイプのスタートポイントが必要です。また、スタートポイントに対して「**[!UICONTROL Mobile Workspace でスタートポイントを表示する]**」オプションをオンにする必要もあります。

![mws_startpoint_select_option](assets/mws_startpoint_select_option.png)

**Workbench で定義されたプロセスを開始するには**

1. AEM Forms アプリケーションで使用可能なスタートポイントを表示するには、[ホーム画面](../../forms/using/home-screen.md)に移動してください。
1. デフォルトでは、**[!UICONTROL ホーム]**&#x200B;画面に「**[!UICONTROL すべてのフォーム]**」リストが表示されます。

   スタートポイントはフォームに関連付けられています。リストでスタートポイントに関連付けられているフォームを選択して開きます。

   スタートポイントに関連付けられているフォームが開きます。

1. **[!UICONTROL スタートポイント]**&#x200B;フォームに、詳細情報を入力します。

   「[添付ファイル](../../forms/using/add-attachments.md)」ボタンを使用して、このタスクに注釈を追加できます。

1. フォームを入力したら、「**[!UICONTROL 送信]**」ボタンを選択します。

アプリケーションがオフラインの場合、フォームとそのデータは Outbox フォルダーに保存されます。

アプリケーションがオンラインの場合、タスクは AEM Forms サーバーと同期され、プロセスで指定されたユーザーに割り当てられます。

タスクリスト内のタスクを実行するには、[タスクを開く](/help/forms/using/open-task.md)を参照してください。
