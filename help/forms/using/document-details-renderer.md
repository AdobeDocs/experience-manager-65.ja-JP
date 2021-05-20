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
exl-id: 946f0f6d-86af-41c1-98ef-98c8f5566e95
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 55%

---

# レンダラーのためのドキュメントの詳細  {#document-details-for-renderer}

## はじめに {#introduction}

AEM Forms Workspace では、複数のフォームタイプをシームレスにサポートしています。有効なタイプには以下が含まれます。

* PDF フォーム（XDP / Acroform / Flat PDF）
* 新規 HTML フォーム
* 画像
* サードパーティアプリケーション（たとえば、Correspondence Management など）

このドキュメントでは、表示を中断することなく顧客の要件を満たすように、セマンティックカスタマイゼーションおよびコンポーネントの再利用の観点からこれらのレンダラーの動作を説明します。AEM Forms Workspaceではユーザーインターフェイスやセマンティックの変更が可能ですが、様々なフォームタイプのレンダリングロジックは変更しないことをお勧めします。そうしないと、予測できない結果が生じる場合があります。 このドキュメントは、別々のポータルで同じワークスペースコンポーネントを使用する、同じフォームのレンダリングをサポートするためのガイド／ナレッジであり、レンダリングロジック自体を変更するためのものではありません。

## PDF フォーム {#pdf-forms}

PDF formsは`PdfTaskForm View`によってレンダリングされます。

XDP フォームが PDF としてレンダリングされると、FormsAugmenter サービスは `FormBridge` JavaScript™ を追加します。この JavaScript™ （PDF フォーム内）が、フォーム送信、フォーム保存、またはフォームをオフラインにするなどのアクションを実行する手助けをします。

AEM Forms Workspaceでは、PDFTaskFormビューは、`/lc/libs/ws/libs/ws/pdf.html`にある中間のHTMLを介して`FormBridge`JavaScriptと通信します。 フローを以下に示します。

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

CRXにデプロイされたモバイルフォームパッケージを使用してXDPフォームがHTMLとしてレンダリングされると、フォームに`FormBridge`JavaScriptも追加されます。これにより、フォームデータの保存と送信にさまざまな方法が公開されます。

このJavaScriptは、上記のPDF formsとは異なりますが、同じ目的を果たします。

>[!NOTE]
>
>NewHTMLTaskForm表示の内容を変更することはお勧めしません。

## Flex フォームおよびガイド {#flex-forms-and-guides}

Flex フォームは SwfTaskForm によってレンダリングされ、ガイドは HtmlTaskForm 表示によってレンダリングされます。

AEM Forms Workspaceでは、これらのビューは実際のSWFと通信し、`/lc/libs/ws/libs/ws/WSNextAdapter.swf`にある中間のSWFを使用してFlexフォーム/ガイドを構成します

通信は`swfObject.postMessage` / `window.flexMessageHandler`を使用しておこなわれます。

このプロトコルは `WsNextAdapter.swf` によって定義されています。ウィンドウオブジェクトの既存の `flexMessageHandlers` は、新しく追加される前に、以前に開いていた SWF フォームから削除されます。このロジックでは、タスクの詳細表示でフォームタブと履歴タブを切り替えることも考慮しています。`WsNextAdapter.swf` は、保存や送信などの様々なフォームアクションの実行に使用されます。

>[!NOTE]
>
>`WSNextAdapter.swf` または SwfTaskForm / HtmlTaskForm 表示の内容を変更することはお勧めしません。

## サードパーティアプリケーション（Correspondence Managementなど）{#third-party-applications-for-example-correspondence-management}

サードパーティアプリケーションは、ExtAppTaskForm 表示を使用してレンダリングされます。

**AEM Forms Workspaceとの通信に対するサードパーティアプリケーション**

AEM Forms workspaceは`window.global.postMessage([Message],[Payload])`でリッスンします

[] Messagecanは、  `SubmitMessage`|  `CancelMessage`|  `ErrorMessage`|( `actionEnabledMessage`内)をクリックしま `runtimeMap`す。サードパーティアプリケーションは、必要に応じてAEM Forms Workspaceに通知するには、このインターフェイスを使用する必要があります。 AEM Forms Workspaceはタスクウィンドウをクリーンアップできるように、タスクが送信されたタイミングを知っている必要があるので、このインターフェイスの使用は必須です。

**AEM Forms workspaceからサードパーティアプリケーションへの通信**

AEM Forms Workspaceの直接アクションボタンが表示されている場合は、`window.[External-App-Name].getMessage([Action])`を呼び出します。ここで、`[Action]`は`routeActionMap`から読み取られます。 サードパーティアプリケーションは、このインターフェイスをリッスンし、`postMessage ()` APIを介してAEM Forms Workspaceに通知する必要があります。

例えば、Flexアプリケーションでは、この通信をサポートする`ExternalInterface.addCallback('getMessage', listener)`を定義できます。 サードパーティアプリケーションが独自のボタンを使用してフォーム送信を処理する場合は、`hideDirectActions = true() in the runtimeMap`を指定し、このリスナーをスキップできます。 従って、この構築はオプションです。

サードパーティアプリケーションの Correspondence Management との統合の詳細については、「[AEM Forms Workspace での Correspondence Management の統合](/help/forms/using/integrating-correspondence-management-html-workspace.md)」を参照してください。
