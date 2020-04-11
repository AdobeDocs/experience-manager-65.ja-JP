---
title: AEM Forms Workspace の操作
seo-title: AEM Forms Workspace の操作
description: AEM Forms Workspace のプロセスワークフローについて概要を簡単に説明する。
seo-description: AEM Forms Workspace のプロセスワークフローについて概要を簡単に説明する。
uuid: 36381e7b-1533-459c-80de-92e806a49cd5
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 866cd9cb-6661-4b0f-a3af-e39453e6e51b
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# AEM Forms Workspace の操作{#working-with-aem-forms-workspace}

## 概要 {#introduction}

AEM Forms Workspace は AEM Forms の一部です。Workspace は PDF フォームに加え、HTML フォームのレンダリングを容易にします。これで、モバイルインターフェイスや Web アプリケーションからビジネスプロセスに関わることができます。

また、AEM Forms Workspace は、標準的な HTML および JavaScript™ の展開方法を使用して高度にカスタマイズすることが可能です。これは、その他の Web アプリケーションと容易に統合するコンポーネントベースのソフトウェアです。

詳しくは、「[AEM Forms Workspace の概要](/help/forms/using/introduction-html-workspace.md)」を参照してください。

## はじめに {#getting-familiar}

Forms アプリケーションを作成してビジネスプロセスを自動化する全プロセスを理解するには、チュートリアルに従います。チュートリアルに従うと、Workbench、Designer、AEM Forms Workspace を使用して、アプリケーションを作成、管理、テストすることができます。実装について詳しくは、「[最初の AEM Forms アプリケーションの作成](https://help.adobe.com/en_US/livecycle/11.0/CreateFirstApp/index.html)」を参照してください。

## 機能の概要 {#functional-overview}

AEM Forms Workspace では、以下のタスクを実行できます。

**開始ビジネスプロセス：** AEM Forms Workspaceでは、カテゴリのプロセスを組織が設計および設定したとおりに実行します。 頻繁に使用するカテゴリをお気に入りに追加して、これらのカテゴリにすばやくアクセスできます。プロセスの開始時は通常、Forms ワークフローによってコントロールされるビジネスプロセスを開始するためのフォームに入力する必要があります。詳しくは、「[プロセスの開始](/help/forms/using/starting-processes.md)」を参照してください。

**表示と行動タスク:** TODOリストを表示すると、割り当てられているビジネスプロセスのタスク、または所属する任意のグループのタスク、または他のユーザーの共有ユーザーが表示されます。 必要に応じてタスクを開き、操作して完了することができます。タスクを完了するには通常、情報を入力し、フォームを承認するか拒否します。詳しくは、「[TODO リストの操作](/help/forms/using/todo-lists.md)」を参照してください。

**タスクの追跡**：タスクを追跡するには、AEM Forms Workspace の「追跡」タブを使用します。開始または参加したアクティブなプロセスおよび完了したプロセスを検索できます。プロセスに含まれていたタスク、割り当ておよびフォームを表示できます。また、既に開始したプロセスのフォームデータを使用して、新しいプロセスを開始することもできます。詳しくは、「[プロセスの追跡](/help/forms/using/tracking-processes.md)」を参照してください。

## AEM Forms Workspace の新しいサービス {#new-offering-of-aem-forms-workspace}

**タスクの一括承認サポート**

同じタイプのタスクを複数承認できます。承認用の1つのタスクを選択すると、同じプロセスを持ち、同じタスク名を持ち、同じルートオプションを持つタスクのみが有効なままになります。 See [Working with To-Do lists](/help/forms/using/todo-lists.md) for implementation details.

## Flex Workspace から AEM Forms Workspace への移行 {#migrating-from-flex-workspace-to-aem-forms-workspace}

Flex Workspace ユーザーが AEM Forms を使用することはできません。Flex Workspace を使用しているすべてのユーザーは AEM Forms Workspace に移行する必要があります。

AEM Forms Workspace では、デフォルトのアクションプロファイルで XDP フォームに関連付けられているデフォルトのレンダリング／送信サービスが変更され、新しいサービスが導入されました。詳しくは、「[新しいレンダリングと送信サービス](/help/forms/using/new-render-submit-service.md)」を参照してください。XDP フォームを使用する既存のプロセスを移行してこれらのサービスを使用するには、[この手順](/help/forms/using/new-render-submit-service.md#main-pars-faq)に従います。

**Flex Workspace カスタマイズと AEM Forms Workspace のマッピング**

両方の Workspace の各種タイプ間におけるカスタマイズのマッピングは次のとおりです。

<table>
 <tbody>
  <tr>
   <td><strong>カスタマイズのタイプ </strong></td>
   <td><strong>対象カスタマイズ </strong></td>
   <td><strong>対応する AEM Forms Workspace カスタマイズのシナリオ</strong></td>
  </tr>
  <tr>
   <td>ローカリゼーションのカスタマイズ</td>
   <td>
    <ol>
     <li>Workspace のロケールの変更</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/changing-locale-user-interface.md">AEM Forms Workspace ロケールの変更</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>テーマのカスタマイズ</td>
   <td>
    <ol>
     <li>画像の置換</li>
     <li>カラーの変更</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/changing-organization-logo-branding.md">組織ロゴの変更</a> </li>
     <li><a href="/help/forms/using/changing-color-scheme-interface.md">カラースキームの変更</a></li>
    </ol> </td>
  </tr>
  <tr>
   <td>レイアウトのカスタマイズ</td>
   <td>
    <ol>
     <li>Workspace ユーザーインターフェイスの簡素化<br /> </li>
     <li>新しいログイン画面の作成</li>
     <li>カスタム Approval Container の作成</li>
    </ol> </td>
   <td>
    <ol>
     <li><a href="/help/forms/using/description-reusable-components.md">再利用可能なコンポーネントの操作</a></li>
     <li><a href="/help/forms/using/creating-new-login-screen.md">新しいログイン画面の作成</a></li>
     <li>Approval Container は非推奨です。</li>
    </ol> </td>
  </tr>
 </tbody>
</table>

AEM Forms Workspace では利用できない Flex Workspace の機能には、メッセージと通知、ようこそページ、Approval Container、列見出しを管理するオプションなどがあります。完全なリストについては、「[AEM Forms Workspace では利用できない Flex Workspace の機能](/help/forms/using/features-flex-workspace-available-html.md)」を参照してください。

## AEM Forms Workspace を使用した開発 {#developing-with-aem-forms-workspace}

### アーキテクチャ {#architecture}

AEM Forms Workspace は、HTML および JavaScript™ ベースの、CRX™ にホスティングされている Web アプリケーションです。Workspace URL がブラウザーで開かれると、CRX™ リソースがアクセスされ、アプリケーションがブラウザー内で MTML ページとしてレンダリングされます。JavaScript ライブラリおよびカスタム JavaScript コードは、ユーザーインターフェイス、ユーザーインタラクション、AEM Forms サーバーとの通信など、アプリケーションの内外部の動作を管理します。詳しくは、「AEM Forms Workspace の[アーキテクチャ](/help/forms/using/html-workspace-architecture.md)」を参照してください。

### AEM Forms Workspace のカスタマイズ {#aem-forms-workspace-customization}

AEM Forms Workspace では、幅広く様々なカスタマイズをサポートしてユーザーインターフェイスのレイアウト、その表示方法、機能などを更新します。カスタマイズでは以下のうちの 1 つ以上を更新します。

* ユーザーインターフェイスの表示方法
* セマンティックのカスタマイズを使用した機能
* 他の Web アプリケーションでの HTML コンポーネントの再利用

「[カスタマイズ](/help/forms/using/introduction-customizing-html-workspace.md#main-pars-heading-0)」の記事では、このようなカスタマイズのタイプについて説明しています。

### 開発者環境の設定 {#set-up-the-developer-environment}

AEM Forms Workspace の成果物には、CRX にデプロイされる CRX パッケージ、完全なソースコードが含まれている SDK アーカイブ、サードパーティの JavaScript ライブラリ、AEM Forms Workspace のビルドスクリプトが含まれます。これらを使用して、上述したカスタマイズを実行するための開発者環境を設定します。詳しくは、「[AEM Forms Workspace コードの構築](/help/forms/using/introduction-customizing-html-workspace.md#main-pars-heading-3)」を参照してください。

主要なインターフェイスやコア機能をカスタマイズできます。これには、フォント、カラースキーム、ロゴ、ログイン画面、エラーダイアログ、サードパーティアプリケーションとの統合、サードパーティアプリケーションのコンポーネントの再利用などが含まれます。また、タスクの概要ページに表示するコンテンツの補正、タスクルートアクションのイメージの表示のほか、AEM Forms Workspace アプリケーションを作成する低レベルのバックポーンモデルやバックボーンビューの変更を行うこともできます。

### XDP フォームの HTML レンダリング {#html-rendering-of-xdp-forms}

新しいプロセスではデフォルトで、デスクトップ上では PDF 形式、タブレット上では HTML 形式で XDP フォームがレンダリングされます。XDP フォームはいつでも HTML 形式でレンダリングできます。詳しくは、「[新しいレンダリングと送信サービス](/help/forms/using/new-render-submit-service.md)」を参照してください。

[Mobile Forms機能は](https://helpx.adobe.com/livecycle/help/mobile-forms/introduction.html) 、 [プロファイルと連携し](https://helpx.adobe.com/livecycle/help/mobile-forms/creating-profile.html)、XDPフォームのHTMLレンダリングを有効にします。 「新規 HTML フォームのレンダリング」はデフォルトで `default.html` プロファイルを使用しますが、これは変更することができます。XDP フォームを HTML 形式でレンダリングする前に実行されたカスタム変更を追加することもできます。

## AEM Forms Workspace アプリケーション {#aem-forms-workspace-app}

モバイルデバイスでビジネスプロセスを操作するには、AEM Forms の AEM Forms Workspace アプリケーションサービスを使用します。詳しくは、「[AEM Forms Workspace アプリ：概要](https://helpx.adobe.com/livecycle/help/mobile-workspace/mobile-workspace-overview.html)」を参照してください。
