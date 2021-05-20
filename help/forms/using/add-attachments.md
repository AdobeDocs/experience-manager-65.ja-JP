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
exl-id: 82282e2d-63a1-47e9-b2ec-f50a4bd32bd3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 63%

---

# AEM Forms Workflow（JEE 上の AEM Forms）と同期されたフォーム内で、{#adding-attachments}

## AEM Forms Workflowサーバー(JEE上のAEM Forms)と同期されたフォームに添付ファイルを追加する{#adding-annotations}

AEM Forms アプリでは、AEM Forms JEE サーバーと同期されたフォームに対して、画像、手書きメモやテキストメモを添付することができます。フォームを AEM Forms Workflow サーバから読み込んだ場合は、添付ファイルがフォームに追加されます。添付ボタン![attachments-app](assets/attachments-app.png)をタップすると、フォーム内のすべての添付ファイルが一緒に表示されます。 赤色の通知は、フォームの添付ファイルの数を表示します。フォームに添付ファイルがない場合は、赤い通知ボタンは表示されません。 フォームに添付ファイルがない場合は、添付ファイルボタン![attch](assets/attch.png)をタップすると、写真や手書きメモを添付するオプションが表示されます。

以下のオプションがあります。

* **ギャラリー**：デバイス上に保存されたファイルの中から、画像を追加することができます。

* **カメラ**：写真を撮ってフォームに追加することができます。

* **メモ**：手書きメモやテキストメモを追加できます。手書きメモを追加するには![手書きメモ](assets/scribble.png)を、テキストメモを追加するには![キーボード](assets/keyboard.png)を使用します。

>[!NOTE]
>
>1人のユーザーが追加した添付ファイルは、他のAEM Forms Appユーザーに表示されます。 他のユーザーは、ユーザーが追加した添付ファイルを削除することはできません。


### 「添付ファイル」画面{#the-attachments-screen}

すべての添付ファイルを1か所に表示するには、![attachments-app](assets/attachments-app.png)をタップします。 ここで、添付ファイルの追加、名前変更、削除を行うことができます。

![すべての添付ファイルを集めた状態](assets/attachments-screen.png)

別の画像、手書きメモ、またはテキストを添付する場合は、「添付ファイル」画面の「**+**」ボタンを使用することができます。

### 写真を追加する {#adding-a-photograph}

フォームに画像を添付する際は、モバイルデバイスのカメラを使用するか、またはデバイスに保存された画像を使用することができます。

1. ウィンドウの下部にある添付ボタン![attch](assets/attch.png)をタップします。
1. 表示されるポップアップで「**Gallery**」または「**Camera**」をタップします。
1. 選択したオプションに応じて、次の操作を行います。

   1. 「**カメラ**」を選択した場合：

      写真を撮ります。次に、「****![use-pic](assets/use-pic.png)」ボタンをタップします。

      または、「**Retake** ![retake](assets/retake.png)」ボタンをタップして写真を撮り直します。

   1. 「**ギャラリー**」を選択した場合：

      デバイスの画像ブラウザがポップアップ表示されます。デバイスの画像ブラウザから、添付する画像をタップします。

### メモを追加する {#adding-a-note}

「**メモ**」オプションを使用すると、フォームに手書きメモとテキストの添付ファイルを追加できます。

1. ウィンドウの下部にある添付ボタン![attch](assets/attch.png)をタップします。
1. 表示されるポップアップで「**メモ**」をタップします。
1. 起動した「メモ」ユーザーインターフェイスで、フリーハンドの手書きメモをキャプチャします。

   ![「手書きメモ」インターフェイス](assets/scribble-ui.png)

   手書き

   「手書きメモ」インターフェイスでは、以下のオプションを使用できます。

   * **クリア**：スクリーンをクリアします。
   * **「完了」ボタン**：現在の手書きメモを添付します。
   * **キャンセルボタン**: 現在の手書きメモを破棄し、「手書きメモ」ユーザーインターフェイスを閉じます。
   * ![キーボード](assets/keyboard.png):手書きメモをクリアし、テキストメモを追加します。

   ![AEM Forms アプリの手書きメモ画面に表示されたキーボード](assets/keyboard-inapp.png)

## AEM Forms Workflowを使用せずにAEM Formsサーバーと同期されるフォームの添付ファイル(OSGi上のAEM Forms) {#attachments-in-forms-synced-with-the-aem-forms-servers-without-aem-forms-workflow-aem-forms-on-osgi}

AEM Forms OSGi サーバーと同期するモバイル向けフォームの添付ファイルは、AEM Forms JEE サーバーと同様の動作をします。

フォームレベルの添付ファイルは、アプリ上で AEM Forms OSGi サーバーから読み込んだアダプティブフォームではサポートされません。画像やテキストメモを添付するには、フォームの作成時に、フィールドレベルの添付ファイルを有効にします。ファイルの添付コンポーネントを、コンポーネントブラウザーからフィールド上にドラッグ＆ドロップします。

アダプティブフォームでは、添付されたファイルをレコードのドキュメント（DoR）に表示することができます。[XFA以外のアダプティブフォームのレコードのドキュメントの生成](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)を参照してください。
