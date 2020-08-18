---
title: OSGi 上のフォームベース AEM ワークフローおよび AEM Forms JEE ワークフローのアクションと機能
description: OSGi 上のフォームベース AEM ワークフローおよび AEM Forms JEE ワークフローのアクションと機能
contentOwner: khsingh
translation-type: tm+mt
source-git-commit: dfa5a0dbfdd2c63ea0ec66d805e8b452baa3d0ac
workflow-type: tm+mt
source-wordcount: '929'
ht-degree: 70%

---


# OSGi 上のフォームベース AEM ワークフローおよび AEM Forms JEE ワークフローのアクションと機能 {#actions-and-capabilities-of-form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

## AEM インボックスと HTML ワークスペース {#aem-inbox-and-html-workspace}

AEM Inboxを使用して、OSGi上でForms中心のAEMワークフローを実行および監視できます。 一方、HTML Workspaceでは、AEM FormsJEEワークフローの実行と監視が可能です。 次の表は、OSGi上のForms中心のAEMワークフロー用AEMインボックスおよびAEM FormsJEEワークフロー用のHTML Workspaceで使用できる様々な重要なアクションを理解するうえで役立ちます。

<table>
 <tbody>
  <tr>
   <td>アクション</td>
   <td>AEM インボックス</td>
   <td>HTML Workspace</td>
  </tr>
  <tr>
   <td>プロセス、タスク、フォームアプリケーションを開始する<br /> </td>
   <td>サポート対象<br /> </td>
   <td>サポート対象<br /> </td>
  </tr>
  <tr>
   <td>タスクを送信する</td>
   <td>サポート対象<br /> </td>
   <td>サポート対象<br /> </td>
  </tr>
  <tr>
   <td>タスクをグループに割り当てる</td>
   <td>サポート対象<br /> </td>
   <td>サポート対象<br /> </td>
  </tr>
  <tr>
   <td>複数のルートに送信する</td>
   <td>サポート対象<br /> </td>
   <td>サポート対象<br /> </td>
  </tr>
  <tr>
   <td>タスクの履歴と概要を追跡する</td>
   <td>サポート対象<br /> </td>
   <td>サポート対象<br /> </td>
  </tr>
  <tr>
   <td>電子メール通知を送信する</td>
   <td>サポート対象<br /> </td>
   <td>サポート対象<br /> </td>
  </tr>
  <tr>
   <td>タスクの再割り当てを行う</td>
   <td>サポート対象</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>アダプティブフォームにフィールドレベルでファイルを添付する</td>
   <td>サポート対象</td>
   <td>サポートなし</td>
  </tr>
  <tr>
   <td>カレンダーを表示する</td>
   <td>サポート対象</td>
   <td>サポートなし</td>
  </tr>
  <tr>
   <td>タスクレベルでコメントを追加する</td>
   <td>サポート対象</td>
   <td>サポートなし</td>
  </tr>
  <tr>
   <td>キューを使用する（共有個人用キューの使用と、キュー内のタスクの要求）</td>
   <td>サポート対象</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>不在通知を送信する</td>
   <td>サポート対象</td>
   <td>サポート対象</td>
  </tr>
    <tr>
   <td>UI要素のカスタマイズ</td>
   <td>サポート対象</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>複数のユーザーにタスクを割り当てる</td>
   <td>サポートなし</td>
   <td>サポート</td>
  </tr>
 </tbody>
</table>

## OSGi 上のフォームベース AEM ワークフローと AEM Forms JEE ワークフロー {#form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

OSGi 上のフォームベース AEM ワークフローと AEM Forms JEE ワークフロー（JEE Process Management 上の AEM Forms）には、それぞれ異なる機能セットが付属しています。次の表は、OSGi上のフォーム中心のAEMワークフローおよびJEE上のAEM Formsワークフローで使用できる重要な機能を理解するうえで役立ちます。

<table>
 <tbody>
  <tr>
   <td>機能</td>
   <td>OSGi 上のフォームベース AEM ワークフロー<br /> </td>
   <td>AEM Forms JEE ワークフロー</td>
  </tr>
  <tr>
   <td>アダプティブフォーム</td>
   <td>サポート対象</td>
   <td>サポート対象<br /> </td>
  </tr>
  <tr>
   <td>他の AEM ソリューションとの統合</td>
   <td>サポート対象</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>手書き署名</td>
   <td>サポート対象</td>
   <td>サポート対象<br /> </td>
  </tr>
  <tr>
   <td>カスタムの電子メールテンプレート</td>
   <td>サポート対象</td>
   <td>サポート対象<br /> </td>
  </tr>
  <tr>
   <td>タスク優先度の定義</td>
   <td>サポート対象</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>期限の経過後にタスクをタイムアウト</td>
   <td>サポート対象</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>ワークフロー内でのループ</td>
   <td>サポート対象</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>担当者の動的な選択 </td>
   <td>サポート対象</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>カスタムメタデータの使用</td>
   <td>サポート対象</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>電子署名（Adobe Sign）</td>
   <td>サポート <sup>[1]</sup></td>
   <td>サポート <sup>[5]</sup></td>
  </tr>
  <tr>
   <td>タスクとフォームアプリケーションの管理</td>
   <td>サポート <sup>[2]</sup><br /> </td>
   <td>サポート <sup>[2]</sup></td>
  </tr>
  <tr>
   <td>ドキュメントサービス</td>
   <td>サポート <sup>[3]</sup></td>
   <td>サポート <sup>[3]</sup></td>
  </tr>
  <tr>
   <td>完了したタスクをアダプティブフォームまたは PDF ドキュメントとしてレンダリング</td>
   <td>サポート対象</td>
   <td>サポート対象 [4]</td>
  </tr>
  <tr>
   <td>Correspondence Management との統合</td>
   <td>サポート対象</td>
   <td>サポート対象</td>
  </tr>
   <tr>
   <td>ゲートウェイ、NO WAIT </td>
   <td>サポート対象</td>
   <td>サポート対象</td>
  </tr>
   <tr>
   <td>データを格納する変数 </td>
   <td>サポート対象</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>OR、AND SPLIT</td>
   <td>サポート対象</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>ユーザーアバター</td>
   <td>サポート対象</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>ワークフロー終了時の電子メール送信</td>
   <td>Supported <sup>[7]</sup></td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>ワークフローからの Web サービスの呼び出し</td>
   <td>サポート対象</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>デジタル署名</td>
   <td>サポート対象<br /> </td>
   <td>サポート対象<br /> </td>
  </tr>
  <tr>
   <td>リセットボタン</td>
   <td>サポート対象</td>
   <td>サポートなし</td>
  </tr>
  <tr>
   <td>ワークフローステージ</td>
   <td>サポート対象</td>
   <td>サポートなし</td>
  </tr>
  <tr>
   <td>読み取り専用アダプティブフォーム</td>
   <td>サポート対象</td>
   <td>サポートなし</td>
  </tr>
  <tr>
   <td>デフォルトの保存ボタンを非表示</td>
   <td>サポート対象</td>
   <td>サポートなし</td>
  </tr>
  <tr>
   <td>ワークフローの詳細セクションの詳細な制御</td>
   <td>サポート対象</td>
   <td>サポートなし</td>
  </tr>
  <tr>
   <td>ポーリング/スケジュールサービス</td>
   <td>標準搭載</td>
   <td>必要なカスタム実装</td>
  </tr>
  <tr>
   <td>アダプティブFormsアプリ</td>
   <td>サポート対象</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>Assembler サービス</td>
   <td>サポート対象</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>PDF Generator サービス</td>
   <td>サポート対象</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>Forms サービス</td>
   <td>サポート対象</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>Output サービス</td>
   <td>サポート対象</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>ドキュメント保証</td>
   <td>サポート対象</td>
   <td>サポート対象 </td>
  </tr>
  <tr>
   <td>スクリプトの実行</td>
   <td>ECMAScriptのサポート</td>
   <td>Javaコードスニペットのサポート</td>
  </tr>
  <tr>
   <td>Assembler</td>
   <td>サポート対象</td>
   <td>サポート対象</td>
  </tr>  
  <tr>
   <td>HTML5 フォーム、インタラクティブ PDF フォーム、フォームセット</td>
   <td>サポートなし</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>プロセスレポート</td>
   <td>サポートなし</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>デジタル署名</td>
   <td>サポート対象</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>スタートポイントカテゴリ</td>
   <td>サポートなし </td>
   <td>サポート対象 </td>
  </tr>
  <tr>
   <td>一括タスクの承認 </td>
   <td>サポートなし </td>
   <td>サポート対象 </td>
  </tr>
  <tr>
   <td>ドラフトをカスタム名で保存</td>
   <td>サポートなし </td>
   <td>サポート対象 </td>
  </tr>
  <tr>
   <td>既存のプロセスデータによるプロセスの開始<br /> </td>
   <td>サポートなし</td>
   <td>サポート対象 </td>
  </tr>
  <tr>
   <td>スタートポイントをドラフトとして保存</td>
   <td>サポートなし</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>マネージャービュー</td>
   <td>サポートなし</td>
   <td>サポート対象<br /> </td>
  </tr>
  <tr>
   <td>検索テンプレート</td>
   <td>サポートなし</td>
   <td>サポート対象<br /> </td>
  </tr>
  <tr>
   <td>サードパーティアプリケーションとの統合</td>
   <td>サポートなし <sup>[6]</sup></td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>ワークフローアプリケーションまたはスタートポイントのタスクレベルの添付ファイル</td>
   <td>サポートなし</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>リマインダー電子メール</td>
   <td>サポートなし</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>タスクのタイムアウト時におけるタイトルの変更</td>
   <td>サポートなし</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>タスク委任時とタスク要求時の電子メール</td>
   <td>サポートなし</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>異なるグループ間での委任</td>
   <td>サポートなし</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>XSLT 変換</td>
   <td>サポートなし</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>動的タスクの優先度</td>
   <td>サポートなし</td>
   <td>サポートなし</td>
  </tr>
  <tr>
   <td>動的タイトル</td>
   <td>サポートなし</td>
   <td>サポートなし</td>
  </tr>
    <tr>
   <td>動的な説明</td>
   <td>サポートなし</td>
   <td>サポートなし</td>
  </tr>
 </tbody>
</table>

1. OSGiでフォーム中心のAEMワークフローを使用して、入力済みのアダプティブフォームに署名できます。 OSGi上のフォーム中心のAEMワークフローは、フォームの署名をサポートしています。 The [in-form signing](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience) experience is not supported.

1. AEM FormsJEEワークフローを実行および監視するには、AEM FormsOSGiおよびHTML Workspaceでフォーム中心のワークフローを実行および監視するには、AEMインボックスへのアクセスが必要です。
1. ネイティブの AEM Forms Document Services は、OSGi 上のフォームベース AEM ワークフローと AEM Forms JEE ワークフローの両方で使用することができます。AEMワークフローは、OSGiおよびAEM FormsJEE(Process Management)ワークフロー上のフォーム中心のAEMワークフローにネイティブドキュメントサービスを使用します。
1. AEM Forms JEE ワークフローでレンダリングできるのは、アダプティブフォームだけです。アダプティブフォームを PDF ドキュメントとしてレンダリングすることはできません。
1. AEM Forms JEE ワークフローには、Adobe Sign 用の独立したステップは存在しません。AEM Forms JEE ワークフローに対して、Adobe Sign が有効になっているアダプティブフォームを使用する必要があります。詳しくは、[Adobe Sign のドキュメント](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component)を参照してください。
1. 「 [Invoke Form Data Model Service](../../forms/using/aem-forms-workflow-step-reference.md#p-invoke-form-data-model-service-step-p) 」手順を使用すると、Webサービスサービスを呼び出し、サードパーティのアプリケーションからデータを投稿または取得できます。
1. 「電子メールの [送信](../../forms/using/aem-forms-workflow-step-reference.md#send-email-step) 」手順を使用して、電子メールを送信できます。

## AEM インボックスの機能と AEM Forms アプリケーションの機能との違い {#differences-between-aem-inbox-and-aem-forms-app-features}

Two of the prominent ways to launch a Forms-centric workflow are using [AEM Inbox](../../forms/using/manage-applications-inbox.md) and AEM Forms app. ただし、AEM インボックスの機能と AEM Forms アプリケーションの機能は異なっています。AEM Inbox works only with [Forms-centric workflows](../../forms/using/aem-forms-workflow.md) while the AEM Forms app works with both Forms-centric workflows as well as process management.

以下の表に、AEM インボックスの機能と AEM Forms アプリケーションの機能を示します。

<table>
 <tbody>
  <tr>
   <td><p><strong>アクション</strong></p> </td>
   <td><p><strong>AEM インボックス</strong></p> </td>
   <td><p><strong>AEM Forms アプリケーション</strong></p> </td>
  </tr>
  <tr>
   <td><p>フォームアプリケーションを起動する</p> </td>
   <td><p>サポート対象</p> </td>
   <td><p>サポート対象</p> </td>
  </tr>
  <tr>
   <td><p>タスクを送信する</p> </td>
   <td><p>サポート対象</p> </td>
   <td><p>サポート対象</p> </td>
  </tr>
  <tr>
   <td><p>タスクを委任する</p> </td>
   <td><p>サポート対象</p> </td>
   <td><p>サポートなし</p> </td>
  </tr>
  <tr>
   <td><p>タスクの履歴と概要を追跡する</p> </td>
   <td><p>サポート対象</p> </td>
   <td><p>サポートなし</p> </td>
  </tr>
  <tr>
   <td><p>タスクレベルの添付ファイルを追加する</p> </td>
   <td><p>サポート対象</p> </td>
   <td><p>サポート対象</p> </td>
  </tr>
  <tr>
   <td><p>タスクレベルの添付ファイルを表示する</p> </td>
   <td><p>サポート対象</p> </td>
   <td><p>サポート対象</p> </td>
  </tr>
  <tr>
   <td><p>フール度レベルの添付ファイルを追加する</p> </td>
   <td><p>サポート対象</p> </td>
   <td><p>サポート対象</p> </td>
  </tr>
  <tr>
   <td><p>カレンダービューを表示する</p> </td>
   <td><p>サポート対象</p> </td>
   <td><p>サポートなし</p> </td>
  </tr>
  <tr>
   <td><p>コメントを追加する</p> </td>
   <td><p>サポート対象</p> </td>
   <td><p>サポート対象</p> </td>
  </tr>
 </tbody>
</table>

