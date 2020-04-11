---
title: レンダラーのためのドキュメントの詳細
seo-title: レンダラーのためのドキュメントの詳細
description: サポートされる様々なフォームやファイルタイプをレンダリングする AEM Forms Workspace のレンダーの動作方法についての概念情報。
seo-description: サポートされる様々なフォームやファイルタイプをレンダリングする AEM Forms Workspace のレンダーの動作方法についての概念情報。
uuid: ae3f0585-9105-4ca7-a490-ffdefd3ac8cd
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: b6e88080-6ffc-4796-98c7-d7462bca454e
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# レンダラーのためのドキュメントの詳細 {#document-details-for-renderer}

## 概要 {#introduction}

AEM Forms Workspace では、複数のフォームタイプをシームレスにサポートしています。有効なタイプには以下が含まれます。

* PDF フォーム（XDP / Acroform / Flat PDF）
* 新規 HTML フォーム
* 画像
* サードパーティアプリケーション（たとえば、Correspondence Management など）

このドキュメントでは、表示を中断することなく顧客の要件を満たすように、セマンティックカスタマイゼーションおよびコンポーネントの再利用の観点からこれらのレンダラーの動作を説明します。AEM Forms Workspaceではユーザーインターフェイスやセマンティックの変更が許可されますが、様々なフォームタイプのレンダリングロジックを変更しないことをお勧めします。変更しないと、予期しない結果が生じる場合があります。 このドキュメントは、別々のポータルで同じワークスペースコンポーネントを使用する、同じフォームのレンダリングをサポートするためのガイド／ナレッジであり、レンダリングロジック自体を変更するためのものではありません。

## PDF フォーム {#pdf-forms}

PDFフォームは、によってレンダリングされま `PdfTaskForm View`す。

XDP フォームが PDF としてレンダリングされると、FormsAugmenter サービスは `FormBridge` JavaScript™ を追加します。この JavaScript™ （PDF フォーム内）が、フォーム送信、フォーム保存、またはフォームをオフラインにするなどのアクションを実行する手助けをします。

In AEM Forms workspace, PDFTaskForm view communicates with the `FormBridge`javascript, via an intermediary HTML present at `/lc/libs/ws/libs/ws/pdf.html`. フローを以下に示します。

**PDFTaskForm 表示 - pdf.html**

/を使用した通 `window.postMessage` 信 `window.attachEvent('message')`

このメソッドは、親フレームと I フレーム間の標準的な通信方法です。以前に開いていた PDF フォームからの既存のイベントリスナーは、新しく追加する前に削除されます。この削除では、タスクの詳細表示でフォームタブと履歴タブを切り替えることも考慮しています。

**レンダリングされた PDF 内の pdf.html -`FormBridge`javascript**

/を使用した通 `pdfObject.postMessage` 信 `pdfObject.messageHandler`

このメソッドは、HTML からの PDF javascript との標準的な通信方法です。PdfTaskForm 表示は、フラット PDF にも対応していて、平面的にレンダリングします。

>[!NOTE]
>
>pdf.html / PdfTaskForm 表示の内容はを変更しないことをお勧めします。

## 新規 HTML フォーム {#new-html-forms}

新規 HTML フォームは、NewHTMLTaskForm 表示によってレンダリングされます。

XDP フォームが CRX にデプロイされたモバイルフォームのパッケージを使用して HTML としてレンダリングされた場合は、追加の `FormBridge` javascript もフォームに追加します。これは、フォームデータを保存して送信するのに異なるメソッドを示します。

この javascript は上記の PDF フォームで言及したものとは異なりますが、同じ用途に使用できます。

>[!NOTE]
>
>NewHTMLTaskFormフォルダーの内容は変更しないことをお勧めします。表示

## Flex フォームおよびガイド {#flex-forms-and-guides}

Flex フォームは SwfTaskForm によってレンダリングされ、ガイドは HtmlTaskForm 表示によってレンダリングされます。

In AEM Forms workspace, these views communicate with the actual SWF which makes up the flex form/guide using an intermediary SWF present at `/lc/libs/ws/libs/ws/WSNextAdapter.swf`

The communication happens using `swfObject.postMessage` / `window.flexMessageHandler`.

このプロトコルは `WsNextAdapter.swf` によって定義されています。ウィンドウオブジェクトの既存の `flexMessageHandlers` は、新しく追加される前に、以前に開いていた SWF フォームから削除されます。このロジックでは、タスクの詳細表示でフォームタブと履歴タブを切り替えることも考慮しています。`WsNextAdapter.swf` は、保存や送信などの様々なフォームアクションの実行に使用されます。

>[!NOTE]
>
>`WSNextAdapter.swf` または SwfTaskForm / HtmlTaskForm 表示の内容を変更することはお勧めしません。

## Third-party applications (for example, Correspondence Management) {#third-party-applications-for-example-correspondence-management}

サードパーティアプリケーションは、ExtAppTaskForm 表示を使用してレンダリングされます。

**AEM Forms Workspaceとのサードパーティアプリケーションの通信**

AEM Forms workspace listens on `window.global.postMessage([Message],[Payload])`

[Messageは] 、 `SubmitMessage`| `CancelMessage`| `ErrorMessage`| `actionEnabledMessage`を含めま `runtimeMap`す。 サードパーティアプリケーションは、必要に応じてAEM Forms Workspaceに通知するために、このインターフェイスを使用する必要があります。 AEM Forms Workspaceは、タスクウィンドウをクリーンアップできるように、タスクが送信されたことを知る必要があるので、このインターフェイスの使用は必須です。

**AEM Forms Workspaceからサードパーティアプリケーションへの通信**

AEM Forms Workspaceの直接アクションボタンが表示されている場合は、[が呼び出 `window.[External-App-Name].getMessage([Action])`されます。こ `Action]``routeActionMap`の[は、 The third-party application must listen on this interface, and then notify AEM Forms workspace via the `postMessage ()` API.

For example, a Flex application can define `ExternalInterface.addCallback('getMessage', listener)` to support this communication. If the third-party application wants to handle form submission via its own buttons, then you should specify `hideDirectActions = true() in the runtimeMap` and you may skip this listener. 従って、この構築はオプションです。

サードパーティアプリケーションの Correspondence Management との統合の詳細については、「[AEM Forms Workspace での Correspondence Management の統合](/help/forms/using/integrating-correspondence-management-html-workspace.md)」を参照してください。
