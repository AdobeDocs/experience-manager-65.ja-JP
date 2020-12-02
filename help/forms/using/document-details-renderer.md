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


# レンダラーのためのドキュメントの詳細  {#document-details-for-renderer}

## 概要 {#introduction}

AEM Forms Workspace では、複数のフォームタイプをシームレスにサポートしています。有効なタイプには以下が含まれます。

* PDF フォーム（XDP / Acroform / Flat PDF）
* 新規 HTML フォーム
* 画像
* サードパーティアプリケーション（たとえば、Correspondence Management など）

このドキュメントでは、表示を中断することなく顧客の要件を満たすように、セマンティックカスタマイゼーションおよびコンポーネントの再利用の観点からこれらのレンダラーの動作を説明します。AEM Formsワークスペースではユーザーインターフェイスやセマンティックの変更が可能ですが、様々なフォームタイプのレンダリングロジックは変更しないことをお勧めします。そうしないと、予測できない結果になる場合があります。 このドキュメントは、別々のポータルで同じワークスペースコンポーネントを使用する、同じフォームのレンダリングをサポートするためのガイド／ナレッジであり、レンダリングロジック自体を変更するためのものではありません。

## PDF フォーム {#pdf-forms}

PDF formsは`PdfTaskForm View`によってレンダリングされます。

XDP フォームが PDF としてレンダリングされると、FormsAugmenter サービスは `FormBridge` JavaScript™ を追加します。この JavaScript™ （PDF フォーム内）が、フォーム送信、フォーム保存、またはフォームをオフラインにするなどのアクションを実行する手助けをします。

AEM Formsのワークスペースでは、PDFTaskForm表示は`/lc/libs/ws/libs/ws/pdf.html`にある仲介者のHTMLを介して`FormBridge`javascriptと通信します。 フローを以下に示します。

**PDFTaskForm 表示 - pdf.html**

`window.postMessage` / `window.attachEvent('message')`を使用する通信

このメソッドは、親フレームと I フレーム間の標準的な通信方法です。以前に開いていた PDF フォームからの既存のイベントリスナーは、新しく追加する前に削除されます。この削除では、タスクの詳細表示でフォームタブと履歴タブを切り替えることも考慮しています。

**レンダリングされた PDF 内の pdf.html - `FormBridge` javascript**

`pdfObject.postMessage` / `pdfObject.messageHandler`を使用する通信

このメソッドは、HTMLからPDFJavaScriptと通信する標準的な方法です。 PdfTaskForm 表示は、フラット PDF にも対応していて、平面的にレンダリングします。

>[!NOTE]
>
>pdf.html / PdfTaskForm 表示の内容はを変更しないことをお勧めします。

## 新規 HTML フォーム  {#new-html-forms}

新規 HTML フォームは、NewHTMLTaskForm 表示によってレンダリングされます。

CRXにデプロイされたモバイルフォームパッケージを使用してXDPフォームがHTMLとしてレンダリングされると、フォームにも`FormBridge`JavaScriptが追加され、フォームデータの保存と送信のための様々な方法が公開されます。

このJavaScriptは、上述のPDF formsで言及したものとは異なりますが、目的は同じです。

>[!NOTE]
>
>NewHTMLTaskForm表示の内容は変更しないことをお勧めします。

## Flex フォームおよびガイド {#flex-forms-and-guides}

Flex フォームは SwfTaskForm によってレンダリングされ、ガイドは HtmlTaskForm 表示によってレンダリングされます。

AEM Formsのワークスペースでは、これらの表示は実際のSWFと通信します。これにより、`/lc/libs/ws/libs/ws/WSNextAdapter.swf`にある中間のSWFを使用してFlexフォーム/ガイドを構成します

通信は`swfObject.postMessage` / `window.flexMessageHandler`を使用して行われます。

このプロトコルは `WsNextAdapter.swf` によって定義されています。ウィンドウオブジェクトの既存の `flexMessageHandlers` は、新しく追加される前に、以前に開いていた SWF フォームから削除されます。このロジックでは、タスクの詳細表示でフォームタブと履歴タブを切り替えることも考慮しています。`WsNextAdapter.swf` は、保存や送信などの様々なフォームアクションの実行に使用されます。

>[!NOTE]
>
>`WSNextAdapter.swf` または SwfTaskForm / HtmlTaskForm 表示の内容を変更することはお勧めしません。

## サードパーティアプリケーション（Correspondence Managementなど） {#third-party-applications-for-example-correspondence-management}

サードパーティアプリケーションは、ExtAppTaskForm 表示を使用してレンダリングされます。

**AEM Forms・ワークスペース通信へのサード・パーティ・アプリケーション**

AEM Formsワークスペースは`window.global.postMessage([Message],[Payload])`をリッスンします

[] Messagecは次のように指定された文字列にすることができます。  `SubmitMessage`|  `CancelMessage`|  `ErrorMessage`| `actionEnabledMessage`が含まれ `runtimeMap`ます。サードパーティアプリケーションは、必要に応じてAEM FormsWorkspaceに通知するには、このインターフェイスを使用する必要があります。 このインターフェイスの使用は必須です。これは、AEM Formsワークスペースがタスクーウィンドウをクリーンアップするためにタスクが送信されたことを知る必要があるからです。

**AEM Formsワークスペースからサードパーティアプリケーションへの通信**

AEM Formsワークスペースの直接アクションボタンが表示されている場合は、`window.[External-App-Name].getMessage([Action])`を呼び出します。`[Action]`は`routeActionMap`から読み取られます。 サードパーティアプリケーションは、このインターフェイスをリッスンし、`postMessage ()` APIを介してAEM Formsのワークスペースに通知する必要があります。

例えば、Flexのアプリケーションでは、この通信をサポートする`ExternalInterface.addCallback('getMessage', listener)`を定義できます。 サードパーティアプリケーションが独自のボタンを使用してフォームの送信を処理する場合は、`hideDirectActions = true() in the runtimeMap`を指定し、このリスナーをスキップできます。 従って、この構築はオプションです。

サードパーティアプリケーションの Correspondence Management との統合の詳細については、「[AEM Forms Workspace での Correspondence Management の統合](/help/forms/using/integrating-correspondence-management-html-workspace.md)」を参照してください。
