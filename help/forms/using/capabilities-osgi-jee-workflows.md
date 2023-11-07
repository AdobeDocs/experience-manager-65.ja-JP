---
title: OSGi 上の Forms ベース AEM ワークフローおよび AEM Forms JEE ワークフローのアクションと機能
description: OSGi 上の Forms ベース AEM ワークフローおよび AEM Forms JEE ワークフローのアクションと機能
contentOwner: khsingh
exl-id: 505b8988-b2b3-4222-b3cb-9b3c6259fdd2
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '925'
ht-degree: 62%

---

# OSGi 上の Forms ベース AEM ワークフローおよび AEM Forms JEE ワークフローのアクションと機能 {#actions-and-capabilities-of-form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

## AEM Inbox とHTMLWorkspace {#aem-inbox-and-html-workspace}

AEM インボックスを使用して、OSGi 上で Forms ベースの AEM ワークフローを実行および監視できます。一方、HTMLワークスペースでは、AEM Forms JEE ワークフローを実行および監視できます。 以下の表に、OSGi 上の Forms ベース AEM ワークフローの AEM インボックスと、AEM Forms JEE ワークフローの HTML Workspace で使用できる重要なアクションを示します。

<table>
 <tbody>
  <tr>
   <td>アクション</td>
   <td>AEM インボックス</td>
   <td>HTMLワークスペース</td>
  </tr>
  <tr>
   <td>プロセス、タスクまたはフォームアプリケーションの開始<br /> </td>
   <td>サポート対象<br /> </td>
   <td>サポート対象<br /> </td>
  </tr>
  <tr>
   <td>タスクの送信</td>
   <td>サポート対象<br /> </td>
   <td>サポート対象<br /> </td>
  </tr>
  <tr>
   <td>グループへのタスクの割り当て</td>
   <td>サポート対象<br /> </td>
   <td>サポート対象<br /> </td>
  </tr>
  <tr>
   <td>複数のルートへの送信</td>
   <td>サポート対象<br /> </td>
   <td>サポート対象<br /> </td>
  </tr>
  <tr>
   <td>タスク履歴とタスクの概要の追跡</td>
   <td>サポート対象<br /> </td>
   <td>サポート対象<br /> </td>
  </tr>
  <tr>
   <td>電子メール通知</td>
   <td>サポート対象<br /> </td>
   <td>サポート対象<br /> </td>
  </tr>
  <tr>
   <td>タスクの再割り当て</td>
   <td>サポート対象</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>アダプティブフォームのフィールドレベルの添付ファイル</td>
   <td>サポート対象</td>
   <td>サポート対象外</td>
  </tr>
  <tr>
   <td>カレンダー表示</td>
   <td>サポート対象</td>
   <td>サポート対象外</td>
  </tr>
  <tr>
   <td>タスクレベルのコメント</td>
   <td>サポート対象</td>
   <td>サポート対象外</td>
  </tr>
  <tr>
   <td>キュー（共有個人キュー、キューからタスクを要求）</td>
   <td>サポート対象</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>不在通知</td>
   <td>サポート対象</td>
   <td>サポート対象</td>
  </tr>
    <tr>
   <td>UI 要素のカスタマイズ</td>
   <td>サポート対象</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>複数のユーザーへのタスクの割り当て</td>
   <td>サポート対象外</td>
   <td>サポート対象</td>
  </tr>
 </tbody>
</table>

## OSGi 上の Forms 中心のAEM Workflows とAEM Forms JEE ワークフロー {#form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

OSGi 上の Forms 中心のAEM Workflows とAEM Forms JEE Workflows(JEE 上のAEM Forms Process Management) には、異なる機能セットがあります。 以下の表は、OSGi 上の Forms ベース AEM ワークフローと JEE 上の AEM Forms ワークフローで利用できる、重要な機能を理解するのに役立ちます。

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
   <td>他のAEMソリューションとの統合</td>
   <td>サポート対象</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>手書き署名</td>
   <td>サポート対象</td>
   <td>サポート対象<br /> </td>
  </tr>
  <tr>
   <td>カスタム電子メールテンプレート</td>
   <td>サポート対象</td>
   <td>サポート対象<br /> </td>
  </tr>
  <tr>
   <td>タスクの優先度の定義</td>
   <td>サポート対象</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>期限後にタスクをタイムアウトします</td>
   <td>サポート対象</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>ワークフロー内のループ</td>
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
   <td>E 署名 (Adobe Sign)</td>
   <td>サポート対象 <sup>[1]</sup></td>
   <td>サポート対象 <sup>[5]</sup></td>
  </tr>
  <tr>
   <td>タスクとフォームのアプリケーションを管理</td>
   <td>サポート対象 <sup>[2]</sup><br /> </td>
   <td>サポート対象 <sup>[2]</sup></td>
  </tr>
  <tr>
   <td>ドキュメントサービス</td>
   <td>サポート対象 <sup>[3]</sup></td>
   <td>サポート対象 <sup>[3]</sup></td>
  </tr>
  <tr>
   <td>完了したタスクをアダプティブフォームまたはPDFドキュメントとしてレンダリング</td>
   <td>サポート対象</td>
   <td>サポート対象[4]</td>
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
   <td>OR、AND 分岐</td>
   <td>サポート対象</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>ユーザーアバター</td>
   <td>サポート対象</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>ワークフローの最後に E メールを送信</td>
   <td>サポート対象 <sup>[7]</sup></td>
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
   <td>サポート対象外</td>
  </tr>
  <tr>
   <td>ワークフローステージ</td>
   <td>サポート対象</td>
   <td>サポート対象外</td>
  </tr>
  <tr>
   <td>読み取り専用のアダプティブフォーム</td>
   <td>サポート対象</td>
   <td>サポート対象外</td>
  </tr>
  <tr>
   <td>デフォルトの保存ボタンを非表示にする</td>
   <td>サポート対象</td>
   <td>サポート対象外</td>
  </tr>
  <tr>
   <td>ワークフローの詳細セクションの詳細なコントロール</td>
   <td>サポート対象</td>
   <td>サポート対象外</td>
  </tr>
  <tr>
   <td>ポーリング／スケジュール設定サービス</td>
   <td>すぐに利用可能</td>
   <td>カスタム実装が必要</td>
  </tr>
  <tr>
   <td>アダプティブフォームのアプリケーション</td>
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
   <td>Execute Script</td>
   <td>ECMAScript をサポート</td>
   <td>Java コードスニペットをサポート</td>
  </tr>
  <tr>
   <td>Assembler</td>
   <td>サポート対象</td>
   <td>サポート対象</td>
  </tr>  
  <tr>
   <td>HTML5 フォーム、インタラクティブ PDF フォーム、フォームセット</td>
   <td>サポート対象外</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>プロセスレポート</td>
   <td>サポート対象外</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>デジタル署名</td>
   <td>サポート対象</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>スタートポイントカテゴリ</td>
   <td>サポート対象外 </td>
   <td>サポート対象 </td>
  </tr>
  <tr>
   <td>タスクの一括承認 </td>
   <td>サポート対象外 </td>
   <td>サポート対象 </td>
  </tr>
  <tr>
   <td>ドラフトをカスタム名で保存</td>
   <td>サポート対象外 </td>
   <td>サポート対象 </td>
  </tr>
  <tr>
   <td>既存のプロセスデータを使用したプロセスの開始<br /> </td>
   <td>サポート対象外</td>
   <td>サポート対象 </td>
  </tr>
  <tr>
   <td>スタートポイントをドラフトとして保存中</td>
   <td>サポート対象外</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>マネージャビュー</td>
   <td>サポート対象外</td>
   <td>サポート対象<br /> </td>
  </tr>
  <tr>
   <td>テンプレートを検索</td>
   <td>サポート対象外</td>
   <td>サポート対象<br /> </td>
  </tr>
  <tr>
   <td>サードパーティアプリケーションとの統合</td>
   <td>サポート対象外 <sup>[6]</sup></td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>ワークフローアプリケーションまたはスタートポイント用のタスクレベルの添付ファイル</td>
   <td>サポート対象外</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>リマインダーの電子メール</td>
   <td>サポート対象外</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>タスクタイムアウト時にタイトルを変更</td>
   <td>サポート対象外</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>タスクの委任とタスクの要求に関するメール</td>
   <td>サポート対象外</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>異なるグループ間で委任</td>
   <td>サポート対象外</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>XSLT 変換</td>
   <td>サポート対象外</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>動的タスクの優先度</td>
   <td>サポート対象外</td>
   <td>サポート対象外</td>
  </tr>
  <tr>
   <td>動的タイトル</td>
   <td>サポート対象外</td>
   <td>サポート対象外</td>
  </tr>
    <tr>
   <td>動的な説明</td>
   <td>サポート対象外</td>
   <td>サポート対象外</td>
  </tr>
 </tbody>
</table>

1. OSGi 上の Forms 中心の AEM ワークフローを使用して、入力済みアダプティブフォームに署名することができます。OSGi 上の Forms 中心の AEM ワークフローでは、フォーム外署名機能がサポートされています。[フォーム内署名](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience)エクスペリエンスはサポートされていません。

1. AEM Forms JEE ワークフローを実行および監視するには、AEM Forms OSGi および HTML ワークスペースで Forms 中心のワークフローを実行および監視するために AEM インボックスにアクセスする必要があります。
1. ネイティブの AEM Forms ドキュメントサービスは、OSGi 上のフォーム中心の AEM ワークフローと AEM Forms JEE ワークフローの両方で使用することができます。AEM ワークフローでは、OSGi 上のフォーム中心の AEM ワークフローと AEM Forms JEE ワークフローに対して、ネイティブのドキュメントサービスが使用されます。
1. AEM Forms JEE ワークフローは、アダプティブフォームのみをレンダリングできます。 アダプティブフォームをPDFドキュメントとしてレンダリングすることはできません。
1. AEM forms JEE ワークフローには、Adobe Sign用の個別の手順はありません。 AEM forms JEE ワークフローに対して、Adobe Sign対応のアダプティブフォームが必要です。 詳しくは、 [Adobe Signドキュメント](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component).
1. [フォームデータモデルサービスを呼び出し](../../forms/using/aem-forms-workflow-step-reference.md#p-invoke-form-data-model-service-step-p)する手順を使用して、Web サービスのサービスを呼び出し、サードパーティアプリケーションからデータを投稿または取得できます。
1. [メールの送信](../../forms/using/aem-forms-workflow-step-reference.md#send-email-step)手順を使用して、メールを送信できます。

## AEM インボックスの機能と AEM Forms アプリケーションの機能との違い {#differences-between-aem-inbox-and-aem-forms-app-features}

Forms 中心のワークフローを起動するには、[AEM インボックス](../../forms/using/manage-applications-inbox.md)と AEM Forms アプリケーションの 2 つの方法があります。ただし、AEM インボックスの機能と AEM Forms アプリケーションの機能は異なっています。AEM Inbox は、 [Forms中心のワークフロー](../../forms/using/aem-forms-workflow.md) 一方、AEM Formsアプリは、Forms中心のワークフローとプロセス管理の両方で動作します。

以下の表に、AEM インボックスの機能と AEM Forms アプリケーションの機能を示します。

<table>
 <tbody>
  <tr>
   <td><p><strong>アクション</strong></p> </td>
   <td><p><strong>AEM インボックス</strong></p> </td>
   <td><p><strong>AEM Forms アプリケーション</strong></p> </td>
  </tr>
  <tr>
   <td><p>フォームアプリケーションの開始</p> </td>
   <td><p>サポート対象</p> </td>
   <td><p>サポート対象</p> </td>
  </tr>
  <tr>
   <td><p>タスクの送信</p> </td>
   <td><p>サポート対象</p> </td>
   <td><p>サポート対象</p> </td>
  </tr>
  <tr>
   <td><p>タスクの委任</p> </td>
   <td><p>サポート対象</p> </td>
   <td><p>サポート対象外</p> </td>
  </tr>
  <tr>
   <td><p>タスク履歴とタスクの概要の追跡</p> </td>
   <td><p>サポート対象</p> </td>
   <td><p>サポート対象外</p> </td>
  </tr>
  <tr>
   <td><p>タスクレベルの添付ファイルの追加</p> </td>
   <td><p>サポート対象</p> </td>
   <td><p>サポート対象</p> </td>
  </tr>
  <tr>
   <td><p>タスクレベルの添付ファイルの表示</p> </td>
   <td><p>サポート対象</p> </td>
   <td><p>サポート対象</p> </td>
  </tr>
  <tr>
   <td><p>フィールドレベルの添付ファイルの追加</p> </td>
   <td><p>サポート対象</p> </td>
   <td><p>サポート対象</p> </td>
  </tr>
  <tr>
   <td><p>カレンダービューの表示</p> </td>
   <td><p>サポート対象</p> </td>
   <td><p>サポート対象外</p> </td>
  </tr>
  <tr>
   <td><p>コメントの追加</p> </td>
   <td><p>サポート対象</p> </td>
   <td><p>サポート対象</p> </td>
  </tr>
 </tbody>
</table>
