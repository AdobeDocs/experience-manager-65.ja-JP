---
title: 一般設定の更新
seo-title: Updating general settings
description: ホーム画面などの AEM Forms アプリケーションの設定を更新し、Startpoints や添付ファイルのオプションを取得する
seo-description: Update AEM Forms app settings such as the Home screen and fetch Startpoints and attachments options
uuid: 650d677e-2b3c-498e-9e46-fa659af934ca
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 7fdb9fab-6bae-49b8-86b6-66138a2a6cd3
docset: aem65
exl-id: 3e74cda2-ba3e-4ee9-b7d0-76a804232199
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '388'
ht-degree: 100%

---

# 一般設定の更新{#updating-general-settings}

AEM Forms アプリの一般設定によって、添付ファイルの取得、オフラインモード、ランディング画面、デフォルトのカテゴリー、自動保存の頻度などの設定を行うことができます。

## アプリケーションの一般設定を更新する {#working-with-the-form}

アプリケーションを AEM Forms サーバーと同期すると、すべてのフォームと定義済みタスクがモバイルデバイス上にダウンロードされます。

アプリケーションが同期されたときに、デフォルトの EM Forms アプリケーションソリューションは、各フォームに関連付けられた添付ファイルをダウンロードすることはありません。

「一般」タブで、ダウンロードの添付ファイルや、オフラインモード、ランディング画面、自動保存、および同期設定変更してください。アプリケーションの[ホーム画面](../../forms/using/home-screen.md)を変更できます。

**設定画面で、「一般」タブに移動します。**

1. 設定画面に移動するには、ホーム画面の左上角にあるメニューボタンをタップしてから、「**設定**」をタップします。
1. 設定画面で、「一般」タブをタップします。

   ![AEM Forms アプリケーションの一般設定](assets/gen-settings-1.png)

   一般設定画面

   >[!NOTE]
   >
   >このオプションは、モバイルデバイスごとに表示が異なる場合があります。

### 一般設定 {#general-settings}

アプリの設定では、次の項目を変更することができます。

* **タスク添付ファイルを取得**： 各タスクがアプリケーションにダウンロードされたときに、関連の添付ファイルをダウンロードするかどうかを指定します。
* **オフラインモード**： AEM Forms アプリケーションのオフラインサービスを有効または無効にします。詳細については、「[オフラインモードの使用](/help/forms/using/work-offline-mode.md)」を参照してください。
* **ランディング画面**： アプリケーションの開始場所（[ホーム画面](../../forms/using/home-screen.md)）を設定します。選択可能なオプション：

   * フォーム
   * タスク
   * お気に入り

* **デフォルトカテゴリ**： ホーム画面に表示するフォームのカテゴリを選択できます。「すべて」を選択すると、すべてのフォームがホーム画面に表示されます。カテゴリは、アプリケーションにロードされるフォームに基づいて自動入力されます。フォームは、AEM Forms サーバーで指定したフォーム設定に基づいてアプリケーション内で使用できます。

* **自動保存頻度**： [モバイルアプリケーションがフォームデータをローカルに保存](../../forms/using/autosave-data-app.md)する頻度を設定します。
* **同期頻度**：オンラインモードで AEM Forms サーバーと[モバイルアプリケーションが同期される](../../forms/using/sync-app.md)頻度を設定します。
   **ローカルデータの消去**：デバイス上からデータベースを消去します。この中には、すべてのユーザやファイルストレージ用の設定とローカルデータが含まれます。 

>[!NOTE]
>
>キャッシュを消去すると、直後にアプリからログアウトされます。
>
>ただし、キャッシュ消去の操作を確認するプロンプトが表示されます。
