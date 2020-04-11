---
title: 添付ファイルの追加
seo-title: 添付ファイルの追加
description: AEM Forms のアプリで、写真や手書きメモをタスクに注釈として追加する
seo-description: AEM Forms のアプリで、写真や手書きメモをタスクに注釈として追加する
uuid: 3d2738b4-fd43-44ec-8eaf-a2ad4b7e5af5
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: d5976ed2-4482-495c-bf77-6d192379cfef
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# AEM Forms Workflow（JEE 上の AEM Forms）と同期されたフォーム内で、{#adding-attachments}

## Adding attachments in forms synced with AEM Forms Workflow server (AEM Forms on JEE) {#adding-annotations}

AEM Forms アプリでは、AEM Forms JEE サーバーと同期されたフォームに対して、画像、手書きメモやテキストメモを添付することができます。フォームを AEM Forms Workflow サーバから読み込んだ場合は、添付ファイルがフォームに追加されます。You can tap the attachment button ![attachments-app](assets/attachments-app.png) to see all the attachments in a form together. 赤色の通知は、フォームの添付ファイルの数を表示します。フォームに添付ファイルがない場合は、赤い通知ボタンは表示されません。 If there are no attachments in the form, when you tap the attachments button ![attch](assets/attch.png), you get options to attach photos or scribbles.

次のオプションがあります。

* **ギャラリー**：デバイス上に保存されたファイルの中から、画像を追加することができます。

* **カメラ**：写真を撮ってフォームに追加することができます。

* **メモ**：手書きメモやテキストメモを追加できます。Use ![scribble](assets/scribble.png) to add a scribble, and ![keyboard](assets/keyboard.png) to add a text note.

>[!NOTE]
>
>1人のユーザーが追加した添付ファイルは、他のAEM Formsアプリケーションのユーザーに表示されます。 他のユーザーは、ユーザーが追加した添付ファイルを削除することはできません。


### 「添付ファイル」画面{#the-attachments-screen}

To see all the attachments in a place, tap ![attachments-app](assets/attachments-app.png). ここでは、添付ファイルの追加、名前の変更および削除が可能です。

![すべての添付ファイルを集めた状態](assets/attachments-screen.png)

別の画像、手書きメモ、またはテキストを添付する場合は、「添付ファイル」画面の「**+**」ボタンを使用することができます。

### 写真を追加する {#adding-a-photograph}

フォームに画像を添付する際は、モバイルデバイスのカメラを使用するか、またはデバイスに保存された画像を使用することができます。

1. Tap the attachment button ![attch](assets/attch.png) at the bottom of the window.
1. Tap **Gallery** or **Camera** in the pop-up that appears.
1. 選択したオプションに応じて、次の操作を行います。

   1. 「**カメラ**」を選択した場合：

      写真を撮ります。Then tap the **Use** ![use-pic](assets/use-pic.png) button.

      Or tap the **Retake** ![retake](assets/retake.png) button to retake the photograph.

   1. 「**ギャラリー**」を選択した場合：

      デバイスの画像ブラウザがポップアップ表示されます。デバイスの画像ブラウザから、添付する画像をタップします。

### メモを追加する {#adding-a-note}

The **Notes** option lets you add freehand scribbles and text attachments in your form.

1. Tap the attachment button ![attch](assets/attch.png) at the bottom of the window.
1. 表示されるポップアップで「**メモ**」をタップします。
1. 起動した「メモ」ユーザーインターフェイスで、フリーハンドの手書きメモをキャプチャします。

   ![「手書きメモ」インターフェイス](assets/scribble-ui.png)

   手書き

   「手書きメモ」インターフェイスでは、以下のオプションを使用できます。

   * **クリア**：スクリーンをクリアします。
   * **「完了」ボタン**：現在の手書きメモを添付します。
   * **キャンセルボタン**: 現在の手書きメモを破棄し、「手書きメモ」ユーザーインターフェイスを閉じます。
   * ![キーボード](assets/keyboard.png):手書きメモをクリアし、テキストメモを追加できるようにします。
   ![AEM Forms アプリの手書きメモ画面に表示されたキーボード](assets/keyboard-inapp.png)

## Attachments in forms synced with the AEM Forms servers without AEM Forms Workflow (AEM Forms on OSGi) {#attachments-in-forms-synced-with-the-aem-forms-servers-without-aem-forms-workflow-aem-forms-on-osgi}

AEM Forms OSGi サーバーと同期するモバイル向けフォームの添付ファイルは、AEM Forms JEE サーバーと同様の動作をします。

フォームレベルの添付ファイルは、アプリ上で AEM Forms OSGi サーバーから読み込んだアダプティブフォームではサポートされません。画像やテキストメモを添付するには、フォームの作成時に、フィールドレベルの添付ファイルを有効にします。ファイルの添付コンポーネントを、コンポーネントブラウザーからフィールド上にドラッグ＆ドロップします。

アダプティブフォームでは、添付されたファイルをレコードのドキュメント（DoR）に表示することができます。See, [Generate Document of Record for non-XFA adaptive forms](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md).
