---
title: タスクまたはフォームをドラフトとして保存する
seo-title: タスクまたはフォームをドラフトとして保存する
description: AEM Forms アプリケーションでタスクまたはフォームのドラフトコピーを保存する手順
seo-description: AEM Forms アプリケーションでタスクまたはフォームのドラフトコピーを保存する手順
uuid: 1192d2c2-05a4-4a96-9015-e56111aa2646
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 9950288c-b5a2-4945-afad-be9ce2abc8e9
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# タスクまたはフォームをドラフトとして保存する {#saving-a-task-or-form-as-a-draft}

「ドラフトとして保存」オプションでは、関連フォームに記入済みのデータとともに、タスクまたはフォームのスナップショットが保存されます。テンプレートからドラフトを作成することもできます。ドラフトはモバイルデバイスに保存され、今後取得できるように Adobe Experience Manager Forms サーバーと同期されます。

You can [update the form](/help/forms/using/working-with-form.md), [annotate it](/help/forms/using/add-attachments.md) with photographs, and scribble notes. フォームの更新を続ける際は、ドラフトとして保存することをお勧めします。記入したフォームを後で送信する場合は、ドラフトとして保存しておくと便利です。

To enable save as draft feature for forms saved on forms portal, see [Saving an HTML5 form as a draft](/help/forms/using/saving-html5-form-draft.md).
To configure submission of adaptive forms, see [Drafts and submissions component](/help/forms/using/draft-submission-component.md). （AEM Forms JEEサーバーと同期されたフォームに対しては無効です）。

To create a draft, open the form and tap the **Save as Draft** ![save-as-draft](assets/save-as-draft.png). ドラフトの名前を入力して、「**保存**」をタップします。ドラフトは Drafts フォルダーに保存され、サーバーと同期されます。アプリケーションがオフラインの場合は、Outbox フォルダーに保存されます。

対応するフォームを後で更新した場合、変更内容はすぐに反映されます。AEM Forms アプリケーションを AEM Forms サーバーと同期すると、ドラフトが AEM Forms サーバーにアップロードされます。さらに、ドラフトは Outbox フォルダーから Tasks フォルダーか Drafts フォルダーに移動されます。その横には編集アイコンが表示されます。

複数のタスクやスタートポイントを使用しているときにタスクやスタートポイントを保存すると、ドラフトが保存されます。アプリケーションが AEM Forms サーバーと同期されるたびに、ドラフトがサーバー上に保存されます。これにより、最後に保存した日付と時刻のドラフトをいつでも回復できます。例えば、アプリケーションを再インストールするか、モバイルデバイスを変更する場合は、サーバーからドラフトをダウンロードできます。

## ドラフトの削除 {#delete-a-draft}

Drafts フォルダーにはすべてのドラフトが一覧表示されます。「ドラフトを削除」オプションを使用すると、ドラフトをモバイルデバイスとサーバーから完全に削除できます。

タスクから作成されたドラフトを削除するオプションは使用できません。タスクから作成されたドラフトを削除すると、タスクは中断されます。

ドラフトの破棄はオフラインモードとオンラインモードのいずれにおいても実行できます。オフラインモードでドラフトを破棄すると、サーバーとの接続が復元された後、ドラフトがサーバーから削除されます。

以下の手順を実行し、ドラフトを削除します。

1. In the AEM Forms app, navigate to **Forms.**
1. Select **Drafts** from the drop-down next to Search.
1. A form with the edit icon ![edit-draft-app](assets/edit-draft-app.png) denotes a draft. ドラフトの横にある水平省略記号をタップします。
1. 水平省略記号をタップして表示されたオプションの一覧から、「**ドラフトを削除**」をタップします。
