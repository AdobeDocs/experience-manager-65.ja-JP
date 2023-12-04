---
title: アプリケーションの同期
seo-title: Synchronizing the app
description: モバイルデバイス上のAEM FormsアプリをAEM Formsサーバーと同期します。
seo-description: Synchronize the AEM Forms app on your mobile device with the AEM Forms server.
uuid: 3a6fb2d5-2ec4-4f78-a42a-fc921b66238e
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 393e4332-a2cc-42c8-a18f-3035addbcfaa
docset: aem65
exl-id: 6bb1d6df-b322-4112-bc25-6300877ee146
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 20%

---

# アプリケーションの同期{#synchronizing-the-app}

## アプリケーションの同期 {#synchronizing-the-app-1}

アプリケーション内のフォームが、AEM Formsサーバーからダウンロードされます。 フォームは、「タスク」タブと「Forms」タブにダウンロードされます。 フォームから作成されたドラフトは「ドラフト」タブにダウンロードされ、タスクから作成されたドラフトは「タスク」タブにダウンロードされます。 OSGi サーバー上のスタンドアロンフォームの場合、フォームとドラフトは、それぞれ「Forms」タブと「ドラフト」タブにダウンロードされます。

フォームを完了して送信すると、アプリがオンラインの場合、フォームはすぐにAEM Formsサーバーにアップロードされます。 アプリケーションが同期されると、フォームはサーバーから取得されます。 ただし、アプリケーションがオンラインの場合、ドラフトはただちにサーバーと同期されます。

AEM Formsサーバーがオンラインの場合、デフォルトでは、15 分ごとにアプリが同期されます。 ただし、同期頻度を変更するオプションがあります。 または、いつでも手動でアプリを同期できます。

**アプリを手動で同期するには**

「同期」ボタンを選択します。 ![sync-app](assets/sync-app.png) ホーム画面の右下隅に

**同期頻度を変更するには**

1. 設定画面に移動するには、ホーム画面の左上隅にあるメニューボタンを選択し、「 」を選択します。 **設定**.
1. 設定画面で、「一般」タブを選択します。

   ![一般設定ウィンドウの「同期の頻度」設定](assets/gen-settings-2.png)

1. 「同期の頻度」オプションで、「同期の頻度」の右側の値を選択します。
1. ドロップダウンリストで、新しい同期頻度を選択します。

### 技術仕様 {#technical-specifications}

* オフラインアプリデータをAEM Formsサーバーに送信する主なロジックは、 runtime/offline/util/offline.jsに含まれます。
* .js で、processOfflineSubmittedSavedTasks(...) 関数への呼び出しによって、保存済み／送信済みタスクをサーバーに送信します。同期処理でのエラーや競合も処理されます。タスクの送信に失敗すると、アプリケーションのタスクは失敗としてマークされます。さらに、タスクは Outbox に残ります。
* syncSubmittedTask() 関数と syncSavedTask() 関数は、個々のタスクに対して操作を実行します。
* ユーザーがサーバーとのオフライン状態の同期またはバックグラウンドスレッドによる自動同期を選択した後、タスクリストコンポーネントによって processOfflineSubmittedSavedTasks() 関数の呼び出しが開始されます。
