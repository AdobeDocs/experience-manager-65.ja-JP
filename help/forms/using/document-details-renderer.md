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
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 55%

---


# レンダラーのためのドキュメントの詳細 {#document-details-for-renderer}

## 概要 {#introduction}

AEM Forms Workspace では、複数のフォームタイプをシームレスにサポートしています。有効なタイプには以下が含まれます。

* PDF フォーム（XDP / Acroform / Flat PDF）
* 新規 HTML フォーム
* 画像
* サードパーティアプリケーション（たとえば、Correspondence Management など）

このドキュメントでは、表示を中断することなく顧客の要件を満たすように、セマンティックカスタマイゼーションおよびコンポーネントの再利用の観点からこれらのレンダラーの動作を説明します。AEM Formsワークスペースではユーザーインターフェイスやセマンティックの変更が可能ですが、様々なフォームタイプのレンダリングロジックは変更しないことをお勧めします。そうしないと、予測できない結果になる場合があります。 このドキュメントは、別々のポータルで同じワークスペースコンポーネントを使用する、同じフォームのレンダリングをサポートするためのガイド／ナレッジであり、レンダリングロジック自体を変更するためのものではありません。

## PDF フォーム {#pdf-forms}

PDF formsは、によってレンダリングされ `PdfTaskForm View`ます。

XDP フォームが PDF としてレンダリングされると、FormsAugmenter サービスは `FormBridge` JavaScript™ を追加します。この JavaScript™ （PDF フォーム内）が、フォーム送信、フォーム保存、またはフォームをオフラインにするなどのアクションを実行する手助けをします。

In AEM Forms workspace, PDFTaskForm view communicates with the `FormBridge`javascript, via an intermediary HTML present at `/lc/libs/ws/libs/ws/pdf.html`. フローを以下に示します。

**PDFTaskForm 表示 - pdf.html**

/を使用する通信 `window.postMessage` `window.attachEvent('message')`

このメソッドは、親フレームと I フレーム間の標準的な通信方法です。以前に開いていた PDF フォームからの既存のイベントリスナーは、新しく追加する前に削除されます。この削除では、タスクの詳細表示でフォームタブと履歴タブを切り替えることも考慮しています。

**レンダリングされた PDF 内の pdf.html -`FormBridge`javascript**

/を使用する通信 `pdfObject.postMessage` `pdfObject.messageHandler`

このメソッドは、HTMLからPDFJavaScriptと通信する標準的な方法です。 PdfTaskForm 表示は、フラット PDF にも対応していて、平面的にレンダリングします。

>[!NOTE]
>
>pdf.html / PdfTaskForm 表示の内容はを変更しないことをお勧めします。

## 新規 HTML フォーム {#new-html-forms}

新規 HTML フォームは、NewHTMLTaskForm 表示によってレンダリングされます。

When an XDP Form is rendered as HTML using the mobile forms package deployed on CRX, it also adds additional `FormBridge`JavaScript to the form, which exposes different methods for saving and submitting form data.

このJavaScriptは、上述のPDF formsで言及したものとは異なりますが、目的は同じです。

>[!NOTE]
>
>NewHTMLTaskForm表示の内容は変更しないことをお勧めします。

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

**AEM Forms・ワークスペース通信へのサード・パーティ・アプリケーション**

AEM Forms workspace listens on `window.global.postMessage([Message],[Payload])`

[Message] は、 `SubmitMessage`| `CancelMessage`| `ErrorMessage`| `actionEnabledMessage`が含まれ `runtimeMap`ます。 サードパーティアプリケーションは、必要に応じてAEM FormsWorkspaceに通知するには、このインターフェイスを使用する必要があります。 このインターフェイスの使用は必須です。これは、AEM Formsワークスペースがタスクーウィンドウをクリーンアップするためにタスクが送信されたことを知る必要があるからです。

**AEM Formsワークスペースからサードパーティアプリケーションへの通信**

AEM Formsワークスペースの直接アクションボタンが表示されている場合は、を呼び出し `window.[External-App-Name].getMessage([Action])`ます。ここで、は、から読み取 `[Action]` られ `routeActionMap`ます。 The third-party application must listen on this interface, and then notify AEM Forms workspace via the `postMessage ()` API.

For example, a Flex application can define `ExternalInterface.addCallback('getMessage', listener)` to support this communication. If the third-party application wants to handle form submission via its own buttons, then you should specify `hideDirectActions = true() in the runtimeMap` and you may skip this listener. 従って、この構築はオプションです。

サードパーティアプリケーションの Correspondence Management との統合の詳細については、「[AEM Forms Workspace での Correspondence Management の統合](/help/forms/using/integrating-correspondence-management-html-workspace.md)」を参照してください。
