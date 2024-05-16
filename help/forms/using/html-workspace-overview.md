---
title: AEM Forms Workspace の操作
description: AEM Forms Workspace のプロセスワークフローについて概要を簡単に説明します。
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
docset: aem65
exl-id: 0bedcbd9-2cf8-47da-9440-c773982e550c
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '1019'
ht-degree: 100%

---

# AEM Forms Workspace の操作{#working-with-aem-forms-workspace}

## はじめに {#introduction}

AEM Forms Workspace は AEM Forms の一部です。Workspace は PDF フォームに加え、HTML フォームのレンダリングを容易にします。これで、モバイルインターフェイスや web アプリケーションからビジネスプロセスに関わることができます。

また、AEM Forms Workspace は、標準的な HTML および JavaScript™ の展開方法を使用して高度にカスタマイズすることが可能です。これは、その他の web アプリケーションと容易に統合するコンポーネントベースのソフトウェアです。

詳しくは、[AEM Forms Workspace の概要](/help/forms/using/introduction-html-workspace.md)を参照してください。

## はじめに {#getting-familiar}

Forms アプリケーションを作成してビジネスプロセスを自動化する全プロセスを理解するには、チュートリアルに従います。チュートリアルに従うと、Workbench、Designer、AEM Forms Workspace を使用して、アプリケーションを作成、管理、テストすることができます。実装について詳しくは、[最初の AEM Forms アプリケーションの作成](https://help.adobe.com/ja_JP/livecycle/11.0/CreateFirstApp/index.html)を参照してください。

## 機能の概要 {#functional-overview}

AEM Forms Workspace では、以下のタスクを実行できます。

**ビジネスプロセスの開始**：AEM Forms Workspace は組織で設計および設定されたとおりにプロセスを分類します。頻繁に使用するカテゴリをお気に入りに追加して、これらのカテゴリにすばやくアクセスできます。プロセスの開始時は通常、Forms Workflow によってコントロールされるビジネスプロセスを開始するためのフォームに入力する必要があります。詳しくは、[プロセスの開始](/help/forms/using/starting-processes.md)を参照してください。

**タスクの表示と操作**：TODO リストを表示すると、ビジネスプロセスから自分に割り当てられたタスク、自分が属するグループに割り当てられたタスク、または他のユーザーと共有しているタスクが表示されます。必要に応じてタスクを開き、操作して完了することができます。タスクを完了するには通常、情報を入力し、フォームを承認するか拒否します。詳しくは、[TODO リストの操作](/help/forms/using/todo-lists.md)を参照してください。

**タスクの追跡**：タスクを追跡するには、AEM Forms Workspace の「追跡」タブを使用します。開始または参加したアクティブなプロセスおよび完了したプロセスを検索できます。プロセスに含まれていたタスク、割り当ておよびフォームを表示できます。また、既に開始したプロセスのフォームデータを使用して、新しいプロセスを開始することもできます。詳しくは、[プロセスの追跡](/help/forms/using/tracking-processes.md)を参照してください。

## AEM Forms Workspace の新しいサービス {#new-offering-of-aem-forms-workspace}

**タスクの一括承認サポート**：

同じタイプのタスクを複数承認できます。承認するタスクを 1 つ選択すると、同じプロセス、同じタスク名、同じルートオプションのタスクのみが有効になります。実装について詳しくは、「[TODO リストの操作](/help/forms/using/todo-lists.md)」を参照してください。

## Flex Workspace から AEM Forms Workspace への移行 {#migrating-from-flex-workspace-to-aem-forms-workspace}

Flex Workspace ユーザーが AEM Forms を使用することはできません。Flex Workspace を使用しているすべてのユーザーは AEM Forms Workspace に移行する必要があります。

AEM Forms Workspace では、デフォルトのアクションプロファイルで XDP フォームに関連付けられているデフォルトのレンダリング／送信サービスが変更され、新しいサービスが導入されました。詳しくは、[新しいレンダリングと送信サービス](/help/forms/using/new-render-submit-service.md)を参照してください。XDP フォームを使用する既存のプロセスを移行してこれらのサービスを使用するには、[この手順](new-render-submit-service.md)に従います。

**Flex Workspace カスタマイズと AEM Forms Workspace のマッピング**

両ワークスペースの各種カスタマイズのマッピングは次のとおりです。

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
     <li><a href="/help/forms/using/changing-organization-logo-branding.md">組織のロゴの変更</a> </li>
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
     <li><a href="/help/forms/using/creating-new-login-screen.md">ログイン画面の作成</a></li>
     <li>Approval Container は非推奨です。</li>
    </ol> </td>
  </tr>
 </tbody>
</table>

AEM Forms Workspace では利用できない Flex Workspace の機能には、メッセージと通知、ようこそページ、Approval Container、列見出しを管理するオプションなどがあります。完全なリストについては、[AEM Forms Workspace では利用できない Flex Workspace の機能](/help/forms/using/features-flex-workspace-available-html.md)を参照してください。

## AEM Forms Workspace を使用した開発 {#developing-with-aem-forms-workspace}

### アーキテクチャ {#architecture}

AEM Forms Workspace は、HTML および JavaScript™ ベースの、CRX™ にホスティングされている web アプリケーションです。Workspace URL がブラウザーで開かれると、CRX™ リソースがアクセスされ、アプリケーションがブラウザー内で HTML ページとしてレンダリングされます。JavaScript ライブラリおよびカスタム JavaScript コードは、ユーザーインターフェイス、ユーザーインタラクション、AEM Forms サーバーとの通信など、アプリケーションの内外部の動作を管理します。詳しくは、AEM Forms Workspace の[アーキテクチャ](/help/forms/using/html-workspace-architecture.md)を参照してください。

### AEM Forms Workspace のカスタマイズ {#aem-forms-workspace-customization}

AEM Forms Workspace では、幅広く様々なカスタマイズをサポートしてユーザーインターフェイスのレイアウト、その表示方法、機能などを更新します。カスタマイズでは次の 1 つ以上を更新します。

* ユーザーインターフェイスの表示方法
* セマンティックのカスタマイズを使用した機能
* 他の web アプリケーションでの HTML コンポーネントの再利用

[カスタマイズ](introduction-customizing-html-workspace.md#types-of-customizations)の記事では、このようなカスタマイズのタイプについて説明しています。

### 開発者環境の設定 {#set-up-the-developer-environment}

AEM Forms Workspace の成果物には、CRX にデプロイされる CRX パッケージ、完全なソースコードが含まれている SDK アーカイブ、サードパーティの JavaScript ライブラリ、AEM Forms Workspace のビルドスクリプトが含まれます。これらを使用して、上述したカスタマイズを実行するための開発者環境を設定します。詳しくは、[AEM Forms Workspace コードの構築](introduction-customizing-html-workspace.md#building-html-workspace-code)を参照してください。

主要なインターフェイスやコア機能をカスタマイズできます。これには、フォント、カラースキーム、ロゴ、ログイン画面、エラーダイアログ、サードパーティアプリケーションとの統合、サードパーティアプリケーションのコンポーネントの再利用などが含まれます。また、タスクの概要ページに表示するコンテンツの補正、タスクルートアクションの画像の表示のほか、AEM Forms Workspace アプリケーションを作成する低レベルのバックポーンモデルやバックボーンビューの変更を行うこともできます。

### XDP フォームの HTML レンダリング {#html-rendering-of-xdp-forms}

新しいプロセスではデフォルトで、デスクトップ上では PDF 形式、タブレット上では HTML 形式で XDP フォームがレンダリングされます。XDP フォームはいつでも HTML 形式でレンダリングできます。詳しくは、[新しいレンダリングと送信サービス](/help/forms/using/new-render-submit-service.md)を参照してください。

[プロファイル](https://helpx.adobe.com/jp/livecycle/help/mobile-forms/creating-profile.html)を使用する [Mobile Forms](https://helpx.adobe.com/jp/livecycle/help/mobile-forms/introduction.html) 機能を使用すると、XDP フォームの HTML レンダリングを有効にできます。「新規 HTML フォームのレンダリング」はデフォルトで `default.html` プロファイルを使用しますが、これは変更することができます。XDP フォームを HTML 形式でレンダリングする前に実行されたカスタム変更を追加することもできます。

## AEM Forms Workspace アプリケーション {#aem-forms-workspace-app}

モバイルデバイスでビジネスプロセスを操作するには、AEM Forms の AEM Forms Workspace アプリケーションサービスを使用します。詳しくは、[AEM Forms Workspace アプリ：概要](https://helpx.adobe.com/jp/livecycle/help/mobile-workspace/mobile-workspace-overview.html)を参照してください。
