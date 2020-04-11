---
title: アプリケーションの同期
seo-title: アプリケーションの同期
description: モバイルデバイス上の AEM Forms アプリケーションを AEM Forms サーバーと同期します。
seo-description: モバイルデバイス上の AEM Forms アプリケーションを AEM Forms サーバーと同期します。
uuid: 3a6fb2d5-2ec4-4f78-a42a-fc921b66238e
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 393e4332-a2cc-42c8-a18f-3035addbcfaa
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# アプリケーションの同期{#synchronizing-the-app}

## アプリケーションの同期 {#synchronizing-the-app-1}

アプリケーション内のフォームが AEM Forms サーバーからダウンロードされます。フォームは、「タスク」タブと「フォーム」タブにダウンロードされます。フォームから作成されたドラフトは「ドラフト」タブにダウンロードされ、タスクから作成されたドラフトは「タスク」タブにダウンロードされます。OSGi サーバー上のスタンドアロンフォームの場合、フォームとドラフトは、「フォーム」タブと「ドラフト」タブにそれぞれダウンロードされます。

アプリケーションがオンラインの場合、フォームを完了し送信すると、そのフォームはすぐに AEM Forms サーバーにアップロードされます。アプリケーションが同期されると、そのフォームはサーバーから取得されます。ただし、アプリケーションがオンラインの場合、ドラフトはただちにサーバーと同期されます。

AEM Forms サーバーがオンラインのときは、デフォルトでは、15 分間隔でアプリケーションが同期されます。ただし、この同期頻度を変更するオプションがあります。あるいは、任意の時点でアプリケーションを手動で同期することもできます。

**アプリケーションを手動で同期するには**

Tap the Synchronize button ![sync-app](assets/sync-app.png) at the lower-right corner of the home screen.

**同期頻度を変更するには**

1. 設定画面に移行するには、ホーム画面の左上角にあるメニューボタンをタップしてから、「**設定**」をタップします。
1. 設定画面で、「一般」タブをタップします。

   ![一般設定ウィンドウの「同期の頻度」設定](assets/gen-settings-2.png)

1. 「同期の頻度」オプションで、「同期の頻度」の右側の値をタップします。
1. ドロップダウンリストで、新しい同期頻度を選択します。

### 技術仕様 {#technical-specifications}

* AEM Forms サーバーへのオフラインアプリケーションデータの送信のメインロジックは runtime/offline/util/offline.js に含まれます。
* .js で、processOfflineSubmittedSavedTasks(...) 関数への呼び出しによって、保存済み／送信済みタスクをサーバーに送信します。 同期処理でのエラーや競合も処理されます。 タスクの送信に失敗すると、アプリケーションのタスクは失敗としてマークされます。 さらに、タスクは Outbox に残ります。
* syncSubmittedTask() および syncSavedTask() 関数は、個別のタスクに操作を実行します。
* ユーザーがサーバーへのオフライン状態の同期またはバックグラウンドスレッドによる自動同期を選択した後、タスクリストコンポーネントによって、processOfflineSubmittedSavedTasks() 関数への呼び出しが開始されます。
