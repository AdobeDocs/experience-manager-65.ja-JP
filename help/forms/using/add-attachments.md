---
title: 添付ファイルの追加
description: 写真や手書きメモを注釈としてAEM Formsアプリのタスクに追加する
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
docset: aem65
exl-id: 82282e2d-63a1-47e9-b2ec-f50a4bd32bd3
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 54%

---

# 添付ファイルの追加{#adding-attachments}

## AEM Forms Workflow（JEE 上の AEM Forms）と同期されたフォーム内で、添付ファイルを追加する {#adding-annotations}

AEM Formsアプリを使用すると、AEM Forms JEE サーバーと同期されたフォームに、画像、手書きメモ、テキストメモを添付できます。 フォームがAEM Forms Workflow サーバーから読み込まれると、添付ファイルがフォームに追加されます。 添付ボタン ![attachments-app](assets/attachments-app.png) をタップすると、フォームに添付されたファイルを一括表示することができます。赤色の通知は、フォームの添付ファイルの数を表示します。フォームに添付ファイルが存在しない場合、赤の通知ボタンは表示されません。フォームに添付ファイルが存在しない場合に添付ファイルボタン ![attch](assets/attch.png) をタップすると、写真や手書きメモを添付できるオプションが表示されます。

以下のオプションがあります。

* **ギャラリー**：デバイス上に保存された画像を追加することができます。

* **カメラ**：写真を撮ってフォームに追加できます。

* **メモ**：手書きメモやテキストメモを追加できます。手書きメモを追加するには![手書き](assets/scribble.png)を、テキストメモを追加するには![キーボード](assets/keyboard.png)を使用します。

>[!NOTE]
>
>単一ユーザーによって追加された添付ファイルは、他の AEM Forms アプリケーションのユーザーにも表示されます。他のユーザーは、ユーザーが追加した添付ファイルを削除することはできません。
>

### 添付ファイル画面 {#the-attachments-screen}

すべての添付ファイルを一括表示するには、![attachments-app](assets/attachments-app.png) をタップします。ここでは、添付ファイルの追加、名前変更、削除が可能です。

![すべての添付ファイルを集めた状態](assets/attachments-screen.png)

別の画像、手書きメモまたはテキストを添付する場合は、添付ファイル画面の「**+**」ボタンを使用することができます。

### 写真の追加 {#adding-a-photograph}

モバイルデバイスのカメラを使用したり、デバイスに保存した画像を使用して、フォームに画像を添付したりできます。

1. ウィンドウ下部にある添付ファイルボタン ![attch](assets/attch.png) をクリックします。
1. 表示されるポップアップの中から、「**ギャラリー**」または「**カメラ**」をタップします。
1. 選択したオプションに基づいて、次の操作を実行します。

   1. 次を選択した場合、 **カメラ**.

      写真を撮りなさい。 次に&#x200B;**使用** ![use-pic](assets/use-pic.png)ボタンをタップします。

      あるいは、**撮り直し** ![retake](assets/retake.png) ボタンをタップして写真を撮り直します。

   1. 次を選択した場合、 **ギャラリー**.

      デバイスの画像ブラウザーがポップアップ表示されます。 デバイスの画像ブラウザーから、添付する画像をタップします。

### メモを追加する {#adding-a-note}

「**メモ**」オプションでは、フォームに手書きメモやテキストメモの添付ファイルを追加することができます。

1. ウィンドウ下部にある添付ファイルボタン ![attch](assets/attch.png) をクリックします。
1. タップ **メモ** が表示されるポップアップに表示されます。
1. 起動した Notes ユーザーインターフェイスで、フリーハンドの手書きメモをキャプチャします。

   ![手書きメモインターフェイス](assets/scribble-ui.png)

   手書き

   手書きメモインターフェイスでは、次のオプションを使用できます。

   * **クリア**：画面をクリアします。
   * **「完了」ボタン**：現在の手書きメモを添付します。
   * **キャンセルボタン**：現在の手書きメモを破棄し、手書きメモユーザーインターフェイスを閉じます。
   * ![キーボード](assets/keyboard.png)：手書きメモをクリアし、テキストメモを追加します。

   ![AEM Forms アプリの手書きメモ画面に表示されたキーボード](assets/keyboard-inapp.png)

## AEM Forms Workflow を使用せずにAEM Formsサーバーと同期されたフォームの添付ファイル (OSGi 上のAEM Forms) {#attachments-in-forms-synced-with-the-aem-forms-servers-without-aem-forms-workflow-aem-forms-on-osgi}

AEM Forms OSGi サーバーと同期されたモバイルフォームの添付ファイルは、AEM Forms JEE サーバーと同様に機能します。

フォームレベルの添付ファイルは、AEM Forms OSGi サーバーからアプリ内で読み込まれたアダプティブフォームではサポートされていません。 画像やテキストメモを添付するには、フォームの作成時にフィールドレベルの添付ファイルを有効にします。 ファイル添付コンポーネントを、コンポーネントブラウザーからフィールドにドラッグ&amp;ドロップします。

アダプティブフォームがある場合は、レコードのドキュメント (DoR) 内の添付ファイルを表示することができます。 [非 XFA アダプティブフォームにおける、レコードのドキュメントの生成](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)を参照してください。
