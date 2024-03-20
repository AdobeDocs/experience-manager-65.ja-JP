---
title: 添付ファイルの追加
description: AEM Forms のアプリで、写真や手書きメモをタスクに注釈として追加
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: 82282e2d-63a1-47e9-b2ec-f50a4bd32bd3
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 100%

---

# 添付ファイルの追加{#adding-attachments}

## AEM Forms Workflow（JEE 上の AEM Forms）と同期されたフォーム内で、添付ファイルを追加する {#adding-annotations}

AEM Forms アプリでは、AEM Forms JEE サーバーと同期されたフォームに対して、画像、手書きメモやテキストメモを添付できます。フォームを AEM Forms Workflow サーバーから読み込んだ場合は、添付ファイルがフォームに追加されます。添付ファイルボタン ![attachments-app](assets/attachments-app.png) を選択すると、フォームに添付されたファイルを一括表示できます。赤色の通知は、フォームの添付ファイルの数を表示します。フォームに添付ファイルが存在しない場合、赤の通知ボタンは表示されません。フォームに添付ファイルが存在しない場合、添付ファイルボタン ![attch](assets/attch.png) を選択すると、写真や手書きメモを添付できるオプションが表示されます。

以下のオプションがあります。

* **ギャラリー**：デバイス上に保存された画像を追加することができます。

* **カメラ**：写真を撮ってフォームに追加できます。

* **メモ**：手書きメモやテキストメモを追加できます。手書きメモを追加するには![手書き](assets/scribble.png)を、テキストメモを追加するには![キーボード](assets/keyboard.png)を使用します。

>[!NOTE]
>
>単一ユーザーによって追加された添付ファイルは、他の AEM Forms アプリケーションのユーザーにも表示されます。他のユーザーは、ユーザーが追加した添付ファイルを削除することはできません。
>

### 添付ファイル画面 {#the-attachments-screen}

すべての添付ファイルを一括表示するには、![attachments-app](assets/attachments-app.png) を選択します。ここでは、添付ファイルの追加、名前変更、削除が可能です。

![すべての添付ファイルを集めた状態](assets/attachments-screen.png)

別の画像、手書きメモまたはテキストを添付する場合は、添付ファイル画面の「**+**」ボタンを使用することができます。

### 写真の追加 {#adding-a-photograph}

フォームに画像を添付する際は、モバイルデバイスのカメラを使用するか、またはデバイスに保存された画像を使用できます。

1. ウィンドウ下部にある添付ファイルボタン ![attch](assets/attch.png) を選択します。
1. 表示されるポップアップの中から、「**ギャラリー**」または「**カメラ**」を選択します。
1. 選択したオプションに応じて、次の操作を行います。

   1. 「**カメラ**」を選択した場合。

      写真を撮ります。次に「**使用**」![use-pic](assets/use-pic.png) ボタンを選択します。

      あるいは、「**撮り直し**」![retake](assets/retake.png) ボタンを選択して写真を撮り直します。

   1. 「**ギャラリー**」を選択した場合。

      デバイスの画像ブラウザーがポップアップ表示されます。デバイスの画像ブラウザーから、添付する画像を選択します。

### メモを追加する {#adding-a-note}

「**メモ**」オプションでは、フォームに手書きメモやテキストメモの添付ファイルを追加することができます。

1. ウィンドウ下部にある添付ファイルボタン ![attch](assets/attch.png) を選択します。
1. 表示されるポップアップで「**メモ**」を選択します。
1. 起動した「メモ」ユーザーインターフェイスで、フリーハンドの手書きメモをキャプチャします。

   ![手書きメモインターフェイス](assets/scribble-ui.png)

   手書き

   「手書きメモ」インターフェイスでは、次のオプションを使用できます。

   * **クリア**：スクリーンをクリアします。
   * **「完了」ボタン**：現在の手書きメモを添付します。
   * **「キャンセル」ボタン**：現在の手書きメモを破棄し、「手書きメモ」ユーザーインターフェイスを閉じます。
   * ![キーボード](assets/keyboard.png)：手書きメモをクリアし、テキストメモを追加します。

   ![AEM Forms アプリの手書きメモ画面に表示されたキーボード](assets/keyboard-inapp.png)

## AEM Forms Workflow（OSGi での AEM Forms）を使用しない AEM Forms サーバーと同期されるフォームの添付ファイル {#attachments-in-forms-synced-with-the-aem-forms-servers-without-aem-forms-workflow-aem-forms-on-osgi}

AEM Forms OSGi サーバーと同期するモバイル向けフォームの添付ファイルは、AEM Forms JEE サーバーと同様の動作をします。

フォームレベルの添付ファイルは、アプリ上で AEM Forms OSGi サーバーから読み込んだアダプティブフォームではサポートされません。画像やテキストメモを添付するには、フォームの作成時に、フィールドレベルの添付ファイルを有効にします。ファイルの添付コンポーネントを、コンポーネントブラウザーからフィールド上にドラッグ＆ドロップします。

アダプティブフォームでは、添付されたファイルをレコードのドキュメント（DoR）に表示できます。詳しくは、[XFA 以外のアダプティブフォームにおける、レコードのドキュメントの生成](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)を参照してください。
