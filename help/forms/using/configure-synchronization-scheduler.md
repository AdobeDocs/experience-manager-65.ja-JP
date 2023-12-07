---
title: 同期スケジューラの設定
description: アセットの移行と同期、同期スケジューラーの設定、フォルダーを使用したアセットの整理方法について説明します。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
docset: aem65
role: Admin
exl-id: 34db1f76-ee40-4612-85da-22041e7560fb
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 57%

---

# 同期スケジューラの設定 {#configuring-the-synchronization-scheduler}

デフォルトでは、同期スケジューラーは 3 分ごとに実行され、LiveCycleWorkbench 11 を介してリポジトリ内で変更および更新されたすべてのアセットを同期します。 同期プロセスが完了すると、フォームとリソースを含むアプリケーションがAEM Formsユーザーインターフェイスに表示されます。

## 同期スケジューラーの間隔の変更 {#change-interval-of-the-synchronization-scheduler}

次の手順を実行して、同期スケジューラの間隔を変更します。

1. AEM Configuration Manager にログインします。 Configuration Manager の URL ：`https://'[server]:[port]'/lc/system/console/configMgr`

1. **FormsManagerConfiguration** バンドルを探して開きます。 

1. 「**同期スケジューラー頻度**」オプションに対して新しい値を指定します。

   頻度の単位は分です。例えば、スケジューラーを 60 分ごとに実行するように設定するには、60 と指定します。

## アセットの同期 {#synchronizing-assets}

「**リポジトリからアセットを同期**」オプションを使用すると、アセットを手動で同期できます。次の手順を実行して、アセットを手動で同期します。

1. AEM Formsにログインします。 デフォルトの URL は `https://'[server]:[port]'/lc/aem/forms/` です。

   ![AEM Forms ユーザーインターフェイス](assets/aem_forms_ui.png)

   **図：** *AEM Forms ユーザーインターフェイス*

1. ツールバーの ![aem6forms_sync](assets/aem6forms_sync.png) アイコンをクリックします。最後に設定したパスにアセットが存在しない場合は、下の図に示すダイアログボックスが表示されます。「**開始**」をクリックして同期を開始します。

   ![同期ダイアログボックス](assets/migrate-and-syncronize.png)

   **図：** *同期ダイアログボックス*

## 同期エラーのトラブルシューティング {#troubleshooting-synchronization-error}

ワークフローデザイナー (Workbench Workbench) で新しいLiveCycleを作成できます。

新しく作成したアプリケーションと /content/dam/formsanddocuments にあるフォルダーの名前が同一の場合、エラー「*このアプリケーションと同じ名前のアセットがすでにルートレベルで存在します。*」がログに記録されます。

競合を解決するには、アプリケーションの名前を変更し、アセットを手動で同期します。

![アセット同期の競合ダイアログボックス](assets/sync-conflict.png)

**図：** *アセット同期ダイアログボックスの競合*
