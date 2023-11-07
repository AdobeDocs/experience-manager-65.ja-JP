---
title: AEM Forms Workspace の操作
seo-title: Working with AEM Forms workspace
description: プロセスワークフローの概要を簡単に説明し、AEM Forms Workspace の概要を説明します。
seo-description: Get started with AEM Forms workspace with this quick overview of the process workflows.
uuid: 36381e7b-1533-459c-80de-92e806a49cd5
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 866cd9cb-6661-4b0f-a3af-e39453e6e51b
docset: aem65
exl-id: 0bedcbd9-2cf8-47da-9440-c773982e550c
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '1042'
ht-degree: 24%

---

# AEM Forms Workspace の操作{#working-with-aem-forms-workspace}

## はじめに {#introduction}

AEM Forms workspace はAEM Formsの一部です。 Workspace は、PDF formsに加えて、HTMLFormsのレンディションを容易にします。 これで、モバイルインターフェイスや Web アプリケーションからビジネスプロセスに取り組むことができます。

また、AEM Forms Workspace は、標準の開発方法と JavaScript™の開発方法を使用して、高度にカスタマイズできます。 これは、他の Web アプリケーションと容易に統合できる、コンポーネントベースのソフトウェアです。

詳しくは、 [AEM Forms Workspace の概要](/help/forms/using/introduction-html-workspace.md).

## 使い慣れ {#getting-familiar}

ビジネスプロセスを自動化するフォームアプリケーションを作成するエンドツーエンドのプロセスを理解するには、このチュートリアルに従ってください。 チュートリアルに従って操作を行うと、Workbench、Designer、AEM Formsの各ワークスペースを使用して、アプリケーションの作成、管理、テストを行うことができます。 実装の詳細については、 [最初のAEM Formsアプリケーションの作成](https://help.adobe.com/ja_JP/livecycle/11.0/CreateFirstApp/index.html).

## 機能の概要 {#functional-overview}

AEM Forms Workspace を使用して、次のタスクを実行できます。

**ビジネスプロセスの開始**：AEM Forms Workspace は組織で設計および設定されたとおりにプロセスを分類します。頻繁に使用するカテゴリをお気に入りに登録して、そのカテゴリにすばやくアクセスできます。 プロセスを開始する際は、通常、フォームに入力して、フォームワークフローが制御するビジネスプロセスを開始します。 詳しくは、 [プロセスの開始](/help/forms/using/starting-processes.md).

**タスクの表示と操作**：TODO リストを表示すると、ビジネスプロセスから自分に割り当てられたタスク、自分が属するグループに割り当てられたタスク、または他のユーザーと共有しているタスクが表示されます。必要に応じて、タスクを開いて操作し、完了することができます。 通常、タスクを完了するには、情報の提供、フォームの承認、またはフォームの拒否が必要です。 詳しくは、 [TODO リストの操作](/help/forms/using/todo-lists.md).

**タスクの追跡**：タスクを追跡するには、AEM Forms Workspace の「追跡」タブを使用します。 開始または参加したアクティブなプロセスや完了したプロセスを検索できます。 プロセスの一部であったタスク、割り当て、フォームを表示できます。 また、以前に開始したプロセスのフォームデータを使用して、新しいプロセスを開始することもできます。 詳しくは、 [プロセスの追跡](/help/forms/using/tracking-processes.md).

## AEM Forms Workspace の新機能 {#new-offering-of-aem-forms-workspace}

**タスクの一括承認のサポート**:

同じタイプの複数のタスクを承認できます。 承認するタスクを 1 つ選択すると、同じプロセス、同じタスク名、同じルートオプションのタスクのみが有効になります。実装について詳しくは、「[TODO リストの操作](/help/forms/using/todo-lists.md)」を参照してください。

## Flex Workspace から AEM Forms Workspace への移行 {#migrating-from-flex-workspace-to-aem-forms-workspace}

Flex Workspace は、AEM Formsのお客様には対応していません。 Flex Workspace を使用しているすべてのお客様は、AEM Forms Workspace に移行する必要があります。

AEM Forms Workspace では、XDP フォームに関連付けられているデフォルトのアクションプロファイルで、デフォルトのレンダリングサービスと送信サービスが変更され、新しいサービスが導入されています。 詳しくは、 [新しいレンダリングと送信サービス](/help/forms/using/new-render-submit-service.md). XDP フォームを使用する既存のプロセスを移行してこれらのサービスを使用するには、[この手順](new-render-submit-service.md)に従います。

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
     <li>色の修正</li>
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
     <li>カスタム Approval コンテナの作成</li>
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

AEM Forms Workspace では使用できないFlex Workspace の機能には、メッセージと通知、ようこそページ、承認コンテナ、列見出しを管理するオプションなどがあります。 完全なリストについては、 [Flex Workspace の機能は、AEM Forms Workspace では使用できません](/help/forms/using/features-flex-workspace-available-html.md).

## AEM Forms Workspace を使用した開発 {#developing-with-aem-forms-workspace}

### アーキテクチャ {#architecture}

AEM Forms workspace は、CRX™でホストされるHTMLおよび JavaScript™ベースの Web アプリケーションです。 Workspace URL がブラウザーで開かれると、CRX™ リソースがアクセスされ、アプリケーションがブラウザー内で HTML ページとしてレンダリングされます。JavaScript ライブラリおよびカスタム JavaScript コードは、ユーザーインターフェイス、ユーザーインタラクション、AEM Formsサーバーとの通信など、アプリケーションの内部および外部の動作を管理します。 詳しくは、 AEM Forms Workspace を参照してください。 [アーキテクチャ](/help/forms/using/html-workspace-architecture.md).

### AEM Forms workspace のカスタマイズ {#aem-forms-workspace-customization}

AEM Forms workspace は、様々なカスタマイズをサポートし、ユーザーインターフェイスのレイアウト、外観、機能などを更新します。 カスタマイズには、次の 1 つ以上を更新する必要があります。

* ユーザーインターフェイスの外観
* セマンティックのカスタマイズを使用する機能
* 他の Web アプリケーションでのHTMLコンポーネントの再利用

The [カスタマイズ](introduction-customizing-html-workspace.md#types-of-customizations) この記事では、このようなカスタマイズのタイプについて説明します。

### 開発環境の設定 {#set-up-the-developer-environment}

AEM Forms Workspace の成果物には、CRX にデプロイされた CRX パッケージ、完全なソースコードを含む SDK アーカイブ、サードパーティ JavaScript ライブラリ、AEM Forms Workspace のビルドスクリプトが含まれます。 これらを使用して、上記のカスタマイズを実行する開発環境を設定します。 詳しくは、 [AEM Forms Workspace コードの構築](introduction-customizing-html-workspace.md#building-html-workspace-code).

インターフェイスとコア機能の主要な部分（フォント、カラースキーム、ロゴ、ログイン画面、エラーダイアログ、サードパーティアプリケーションとの統合、サードパーティアプリケーションでのコンポーネントの再利用など）をカスタマイズできます。 また、[ タスクの概要 ] ページに表示される内容を拡張し、タスクのルートアクションのイメージを表示し、AEM Forms Workspace アプリケーションを作成する下位レベルの Backbone モデルとビューを変更することもできます。

### XDP FormsのHTMLレンダリング {#html-rendering-of-xdp-forms}

新しいプロセスの場合、デフォルトでは、XDP フォームはデスクトップ上ではPDF形式、タブレット上ではHTML形式でレンダリングされます。 XDP フォームは常にレンダリング形式でHTMLできます。 詳しくは、 [新しいレンダリングと送信サービス](/help/forms/using/new-render-submit-service.md).

[プロファイル](https://helpx.adobe.com/jp/livecycle/help/mobile-forms/creating-profile.html)を使用する [Mobile Forms](https://helpx.adobe.com/jp/livecycle/help/mobile-forms/introduction.html) 機能を使用すると、XDP フォームの HTML レンダリングを有効にできます。「新規 HTML フォームのレンダリング」はデフォルトで `default.html` プロファイルを使用しますが、これは変更することができます。また、XDP フォームをHTML形式でレンダリングする前に発生するカスタム変更を追加することもできます。

## AEM Forms workspace アプリ {#aem-forms-workspace-app}

モバイルデバイスでビジネスプロセスを操作するには、AEM FormsのAEM Forms workspace アプリ機能を使用できます。 詳しくは、 [AEM Forms workspace アプリの概要](https://helpx.adobe.com/jp/livecycle/help/mobile-workspace/mobile-workspace-overview.html).
