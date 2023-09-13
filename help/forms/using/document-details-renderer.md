---
title: レンダラーのドキュメントの詳細
description: AEM Forms Workspace でのレンダリングがサポートされている様々なフォームやファイルタイプをレンダリングする方法に関する概念的情報です。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 946f0f6d-86af-41c1-98ef-98c8f5566e95
source-git-commit: 474a726058b141985f52a0faec6161a34be1e9dc
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 44%

---

# レンダラーのドキュメントの詳細 {#document-details-for-renderer}

## はじめに {#introduction}

AEM Forms Workspace では、複数のフォームタイプをシームレスにサポートします。 次の機能が含まれます。

* PDF forms(XDP、Acroform、フラットPDF)
* 新しいHTMLフォーム
* 画像
* サードパーティアプリケーション（Correspondence Management など）

このドキュメントでは、セマンティックのカスタマイズ/コンポーネントの再利用の観点から、これらのレンダラーの動作を説明し、レンディションを壊すことなく、顧客の要件を満たすようにします。 AEM Forms Workspace では、ユーザーインターフェイスおよびセマンティックの変更が可能ですが、異なるフォームタイプのレンダリングロジックは変更しないことをお勧めします。変更してしまうと、予測外の結果になる場合があります。このドキュメントは、異なるポータル内の同じワークスペースコンポーネントを使用して、同じフォームのレンダリングをサポートするガイダンス/知識を提供するためのもので、レンダリングロジック自体を変更するためのものではありません。

## PDF forms {#pdf-forms}

PDF フォームは `PdfTaskForm View` でレンダリングされます。

XDP フォームが PDF としてレンダリングされると、FormsAugmenter サービスは `FormBridge` JavaScript™ を追加します。この JavaScript™ （PDF フォーム内）が、フォーム送信、フォーム保存、またはフォームをオフラインにするなどのアクションを実行する手助けをします。

AEM Forms Workspace では、PDFTaskForm ビューは、 `FormBridge`JavaScript( `/lc/libs/ws/libs/ws/pdf.html`. フローは次のとおりです。

**PDFTaskForm 表示 — pdf.html**

`window.postMessage`／`window.attachEvent('message')` を使用した通信

この方法は、親フレームと iframe 間の標準的な通信方法です。 以前に開いたイベントの既存のPDF formsリスナーは、新しく追加する前に削除されます。 このパージでは、タスクの詳細ビューでのフォームタブと履歴タブの切り替えも考慮されます。

**pdf.html - `FormBridge`レンダリングされたPDF内の JavaScript**

`pdfObject.postMessage`／`pdfObject.messageHandler` を使用した通信

このメソッドは、HTML からの PDF JavaScript との標準的な通信方法です。PdfTaskForm ビューでは、フラットPDFも処理し、プレーンにレンダリングします。

>[!NOTE]
>
>PdfTaskForm ビューの pdf.html /コンテンツを編集することはお勧めしません。

## 新しいHTMLForms {#new-html-forms}

新しいHTMLフォームは、NewHTMLTaskForm ビューによってレンダリングされます。

XDP フォームが、CRX にデプロイされたモバイルフォームのパッケージを使用して HTML としてレンダリングされる場合は、別の `FormBridge` JavaScript もフォームに追加されます。これは、フォームデータを保存したり送信したりするための異なるメソッドを示します。

この JavaScript は、上記の JavaScript とは異なりますが、同じPDF formsを提供します。

>[!NOTE]
>
>Adobeは、NewHTMLTaskForm ビューのコンテンツを編集しないことをお勧めします。

## Flex Formsとガイド {#flex-forms-and-guides}

Flex Formsは SwfTaskForm でレンダリングされ、ガイドは HtmlTaskForm ビューでレンダリングされます。

AEM Forms Workspace では、これらの表示は実際のSWFと通信し、 Flex®のフォーム/ガイドを構成します。この情報は、 `/lc/libs/ws/libs/ws/WSNextAdapter.swf`

通信は `swfObject.postMessage`／`window.flexMessageHandler` を使用して行われます。

このプロトコルは `WsNextAdapter.swf` によって定義されています。ウィンドウオブジェクトの既存の `flexMessageHandlers` は、新しく追加される前に、以前に開いていた SWF フォームから削除されます。このロジックでは、タスクの詳細ビューで「フォーム」タブと「履歴」タブを切り替えることも考慮します。 The `WsNextAdapter.swf` は、保存や送信など、様々なフォームアクションを実行するために使用します。

>[!NOTE]
>
>`WSNextAdapter.swf` または SwfTaskForm / HtmlTaskForm 表示の内容を変更することはお勧めしません。

## サードパーティアプリケーション（Correspondence Management など） {#third-party-applications-for-example-correspondence-management}

サードパーティアプリケーションは、 ExtAppTaskForm ビューを使用してレンダリングされます。

**サードパーティアプリケーションから AEM Forms Workspace への通信**

AEM Forms Workspace は `window.global.postMessage([Message],[Payload])` をリッスンします。

[Message] は、`runtimeMap` で `SubmitMessage`| `CancelMessage`| `ErrorMessage`| `actionEnabledMessage` として指定される文字列にすることができます。サードパーティアプリケーションは、必要に応じてAEM Forms Workspace に通知するには、このインターフェイスを使用する必要があります。 AEM Forms Workspace がタスクウィンドウをクリーンアップするには、タスクが送信されたことを知る必要があるため、このインターフェイスの使用は必須です。

**AEM Forms Workspace からサードパーティアプリケーションへの通信**

AEM Forms Workspace の直接アクションボタンが表示されている場合は、`window.[External-App-Name].getMessage([Action])` を呼び出します。この際、`[Action]` は `routeActionMap` から読み取られます。サードパーティアプリケーションは、このインターフェイスをリッスンして `postMessage ()` API 経由で AEM Forms Workspace に通知する必要があります。

例えば、Flex アプリケーションは、この通信をサポートするために `ExternalInterface.addCallback('getMessage', listener)` を定義することができます。サードパーティアプリケーションで独自のボタンを使用してフォーム送信を処理する場合は、`hideDirectActions = true() in the runtimeMap` を指定する必要があり、そうするとリスナーをスキップすることができます。したがって、この構文はオプションです。

Correspondence Management に関するサードパーティアプリケーションの統合について詳しくは、 [AEM Forms Workspace での Correspondence Management の統合](/help/forms/using/integrating-correspondence-management-html-workspace.md).
