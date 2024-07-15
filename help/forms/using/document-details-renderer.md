---
title: レンダラーのドキュメントの詳細
description: サポートされる様々なフォームやファイルタイプをレンダリングする AEM Forms Workspace のレンダーの動作方法についての概念情報。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 946f0f6d-86af-41c1-98ef-98c8f5566e95
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms,Adaptive Forms,Mobile Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 100%

---

# レンダラーのドキュメントの詳細 {#document-details-for-renderer}

## はじめに {#introduction}

AEM Forms Workspace では、複数のフォームタイプをシームレスにサポートしています。次の機能が含まれます。

* PDF フォーム（XDP／Acroform／フラット PDF）
* 新規 HTML フォーム
* 画像
* サードパーティアプリケーション（Correspondence Management など）

このドキュメントでは、レンディションを中断することなく顧客の要件を満たすように、セマンティックカスタマイゼーションおよびコンポーネントの再利用の観点から、これらのレンダラーの動作を説明します。AEM Forms Workspace では、ユーザーインターフェイスおよびセマンティックの変更が可能ですが、異なるフォームタイプのレンダリングロジックは変更しないことをお勧めします。変更してしまうと、予測外の結果になる場合があります。このドキュメントは、別々のポータルで同じワークスペースコンポーネントを使用する、同じフォームのレンダリングをサポートするためのガイド／ナレッジであり、レンダリングロジック自体を変更するためのものではありません。

## PDF フォーム {#pdf-forms}

PDF フォームは `PdfTaskForm View` でレンダリングされます。

XDP フォームが PDF としてレンダリングされると、FormsAugmenter サービスは `FormBridge` JavaScript™ を追加します。この JavaScript™ （PDF フォーム内）が、フォーム送信、フォーム保存、またはフォームをオフラインにするなどのアクションを実行する手助けをします。

AEM Forms Workspace では、PDFTaskForm ビューは、`/lc/libs/ws/libs/ws/pdf.html` にある仲介としての役割を果たす HTML 経由で `FormBridge` JavaScript と通信します。フローを以下に示します。

**PDFTaskForm ビュー - pdf.html**

`window.postMessage`／`window.attachEvent('message')` を使用した通信

このメソッドは、親フレームと iframe 間の標準的な通信方法です。以前に開いた PDF フォームの既存のイベントリスナーは、新しく追加する前に削除されます。この削除では、タスクの詳細表示でフォームタブと履歴タブを切り替えることも考慮しています。

**pdf.html - `FormBridge`レンダリングされた PDF 内の JavaScript**

`pdfObject.postMessage`／`pdfObject.messageHandler` を使用した通信

このメソッドは、HTML からの PDF JavaScript との標準的な通信方法です。PdfTaskForm ビューは、フラット PDF にも対応していて、平面的にレンダリングします。

>[!NOTE]
>
>pdf.html や PdfTaskForm ビューの内容は変更しないことをお勧めします。

## 新規 HTML フォーム {#new-html-forms}

新規 HTML フォームは、NewHTMLTaskForm ビューによってレンダリングされます。

XDP フォームが、CRX にデプロイされたモバイルフォームのパッケージを使用して HTML としてレンダリングされる場合は、別の `FormBridge` JavaScript もフォームに追加されます。これは、フォームデータを保存したり送信したりするための異なるメソッドを示します。

この JavaScript は上記の PDF フォームで説明したものとは異なりますが、同じ用途に使用できます。

>[!NOTE]
>
>NewHTMLTaskForm ビューの内容は変更しないことをお勧めします。

## Flex フォームおよびガイド {#flex-forms-and-guides}

Flex フォームは SwfTaskForm ビューによってレンダリングされ、ガイドは HtmlTaskForm ビューによってレンダリングされます。

AEM Forms Workspace では、これらのビューは実際の SWF と通信します。これにより、`/lc/libs/ws/libs/ws/WSNextAdapter.swf` にある仲介としての役割を果たす SWF を使用して Flex フォーム／ガイドを作成します。

通信は `swfObject.postMessage`／`window.flexMessageHandler` を使用して行われます。

このプロトコルは `WsNextAdapter.swf` によって定義されています。ウィンドウオブジェクトの既存の `flexMessageHandlers` は、新しく追加される前に、以前に開いていた SWF フォームから削除されます。このロジックでは、タスクの詳細ビューでフォームタブと履歴タブを切り替えることも考慮しています。`WsNextAdapter.swf` は、保存や送信などの様々なフォームアクションの実行に使用されます。

>[!NOTE]
>
>`WSNextAdapter.swf` または SwfTaskForm / HtmlTaskForm 表示の内容を変更することはお勧めしません。

## サードパーティアプリケーション（Correspondence Management など） {#third-party-applications-for-example-correspondence-management}

サードパーティアプリケーションは、ExtAppTaskForm ビューを使用してレンダリングされます。

**サードパーティアプリケーションから AEM Forms Workspace への通信**

AEM Forms Workspace は `window.global.postMessage([Message],[Payload])` をリッスンします。

[Message] は、`runtimeMap` で `SubmitMessage`| `CancelMessage`| `ErrorMessage`| `actionEnabledMessage` として指定される文字列にすることができます。サードパーティアプリケーションが必要に応じて AEM Forms Workspace に通知するには、このインターフェイスを使用する必要があります。AEM Forms Workspace がタスクウィンドウをクリーンアップするには、タスクが送信されたことを知る必要があるため、このインターフェイスの使用は必須です。

**AEM Forms Workspace からサードパーティアプリケーションへの通信**

AEM Forms Workspace の直接アクションボタンが表示されている場合は、`window.[External-App-Name].getMessage([Action])` を呼び出します。この際、`[Action]` は `routeActionMap` から読み取られます。サードパーティアプリケーションは、このインターフェイスをリッスンして `postMessage ()` API 経由で AEM Forms Workspace に通知する必要があります。

例えば、Flex アプリケーションは、この通信をサポートするために `ExternalInterface.addCallback('getMessage', listener)` を定義することができます。サードパーティアプリケーションで独自のボタンを使用してフォーム送信を処理する場合は、`hideDirectActions = true() in the runtimeMap` を指定する必要があり、そうするとリスナーをスキップすることができます。従って、この構成はオプションです。

サードパーティアプリケーションの Correspondence Management との統合の詳細については、[AEM Forms Workspace での Correspondence Management の統合](/help/forms/using/integrating-correspondence-management-html-workspace.md)を参照してください。
