---
title: スタートポイントの使用
description: Workbench で定義されたモバイルデバイスからAdobe Experience Manager Formsプロセスを操作する手順です。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: d5970f90-2899-43a5-a3a0-61a2c844d919
source-git-commit: 60924e7ee204e43a2ff833fbc394beca8db9c9d9
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 40%

---

# スタートポイントの使用{#working-with-startpoints}

スタートポイントは Workbench で作成されたプロセスを呼び出します。これはフォームの送信時にプロセスを呼び出すフォームに関連付けられています。

>[!NOTE]
>
>この概念を参照する場合、開始点、開始プロセス、フォームという用語は同じ意味で使用されます。

Adobe Experience Manager(AEM)Formsアプリからプロセスを開始するには、タイプのスタートポイントが必要です **Workspace** を設定します。 また、 **[!UICONTROL Mobile Workspace に表示]** オプションを使用します。

![mws_startpoint_select_option](assets/mws_startpoint_select_option.png)

**Workbench で定義されたプロセスを開始するには**

1. AEM Formsアプリで使用可能な Startpoint を表示するには、に移動します。 [ホーム画面](../../forms/using/home-screen.md).
1. デフォルトでは、**[!UICONTROL ホーム]**&#x200B;画面に「**[!UICONTROL すべてのフォーム]**」リストが表示されます。

   スタートポイントはフォームに関連付けられています。リストでスタートポイントに関連付けられているフォームをタップして開きます。

   スタートポイントに関連付けられているフォームが開きます。

1. **[!UICONTROL スタートポイント]**&#x200B;フォームに、詳細情報を入力します。

   「[添付ファイル](../../forms/using/add-attachments.md)」ボタンを使用して、このタスクに注釈を追加できます。

1. フォームを入力したら、「**[!UICONTROL 送信]**」ボタンをタップします。

アプリがオフラインの場合、フォームとそのデータは Outbox フォルダーに保存されます。

アプリがオンラインの場合、タスクはAEM Formsサーバーと同期され、プロセスで指定されたユーザーに割り当てられます。

タスクリスト内のタスクを操作するには、 [タスクを開く](/help/forms/using/open-task.md).
