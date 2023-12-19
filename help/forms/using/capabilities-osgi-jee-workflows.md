---
title: OSGi 上の Forms ベース AEM ワークフローおよび AEM Forms JEE ワークフローのアクションと機能
description: OSGi 上の Forms ベース AEM ワークフローおよび AEM Forms JEE ワークフローのアクションと機能
contentOwner: khsingh
exl-id: 505b8988-b2b3-4222-b3cb-9b3c6259fdd2
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 97%

---

# OSGi 上の Forms ベース AEM ワークフローおよび AEM Forms JEE ワークフローのアクションと機能 {#actions-and-capabilities-of-form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

## AEM インボックスと HTML ワークスペース {#aem-inbox-and-html-workspace}

AEM インボックスを使用して、OSGi 上で Forms ベースの AEM ワークフローを実行および監視できます。また、HTML ワークスペースにより、AEM Forms JEE ワークフローを実行および監視することもできます。以下の表に、OSGi 上の Forms ベース AEM ワークフローの AEM インボックスと、AEM Forms JEE ワークフローの HTML Workspace で使用できる重要なアクションを示します。

<table>
 <tbody>
  <tr>
   <td>アクション</td>
   <td>AEM インボックス</td>
   <td>HTML ワークスペース</td>
  </tr>
  <tr>
   <td>プロセス、タスク、フォームアプリケーションの開始<br /> </td>
   <td>サポート対象<br /> </td>
   <td>サポート対象<br /> </td>
  </tr>
  <tr>
   <td>タスクの送信</td>
   <td>サポート対象<br /> </td>
   <td>サポート対象<br /> </td>
  </tr>
  <tr>
   <td>タスクをグループに割り当て</td>
   <td>サポート対象<br /> </td>
   <td>サポート対象<br /> </td>
  </tr>
  <tr>
   <td>複数のルートに送信</td>
   <td>サポート対象<br /> </td>
   <td>サポート対象<br /> </td>
  </tr>
  <tr>
   <td>タスクの履歴と概要を追跡</td>
   <td>サポート対象<br /> </td>
   <td>サポート対象<br /> </td>
  </tr>
  <tr>
   <td>メール通知</td>
   <td>サポート対象<br /> </td>
   <td>サポート対象<br /> </td>
  </tr>
  <tr>
   <td>タスクの再割り当て</td>
   <td>サポート対象</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>アダプティブフォームにフィールドレベルでファイルを添付</td>
   <td>サポート対象</td>
   <td>サポート対象外</td>
  </tr>
  <tr>
   <td>カレンダービュー</td>
   <td>サポート対象</td>
   <td>サポート対象外</td>
  </tr>
  <tr>
   <td>タスクレベルのコメント</td>
   <td>サポート対象</td>
   <td>サポート対象外</td>
  </tr>
  <tr>
   <td>キュー（個人のキューの共有、キュー内のタスクの要求）</td>
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
   <td>複数のユーザーにタスクを割り当て</td>
   <td>サポート対象外</td>
   <td>サポート対象</td>
  </tr>
 </tbody>
</table>

## OSGi 上のフォームベース AEM ワークフローと AEM Forms JEE ワークフロー {#form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

OSGi 上のフォームベース AEM ワークフローと AEM Forms JEE ワークフロー（JEE 上の AEM Forms のプロセス管理）には、それぞれ異なる機能セットが付属しています。以下の表は、OSGi 上の Forms ベース AEM ワークフローと JEE 上の AEM Forms ワークフローで利用できる、重要な機能を理解するのに役立ちます。

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
   <td>カスタムのメールテンプレート</td>
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
   <td>電子サイン（Adobe Sign）</td>
   <td>サポート対象 <sup>[1]</sup></td>
   <td>サポート対象 <sup>[5]</sup></td>
  </tr>
  <tr>
   <td>タスクとフォームアプリケーションの管理</td>
   <td>サポート対象 <sup>[2]</sup><br /> </td>
   <td>サポート対象 <sup>[2]</sup></td>
  </tr>
  <tr>
   <td>ドキュメントサービス</td>
   <td>サポート対象 <sup>[3]</sup></td>
   <td>サポート対象 <sup>[3]</sup></td>
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
   <td>ワークフロー終了時のメール送信</td>
   <td>サポート対象 <sup>[7]</sup></td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>ワークフローからの web サービスの呼び出し</td>
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
   <td>読み取り専用アダプティブフォーム</td>
   <td>サポート対象</td>
   <td>サポート対象外</td>
  </tr>
  <tr>
   <td>デフォルトの保存ボタンを非表示</td>
   <td>サポート対象</td>
   <td>サポート対象外</td>
  </tr>
  <tr>
   <td>ワークフローの詳細セクションの細かな制御</td>
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
   <td>既存のプロセスデータによるプロセスの開始<br /> </td>
   <td>サポート対象外</td>
   <td>サポート対象 </td>
  </tr>
  <tr>
   <td>スタートポイントをドラフトとして保存</td>
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
   <td>ワークフローアプリケーションまたはスタートポイントのタスクレベルの添付ファイル</td>
   <td>サポート対象外</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>リマインダーメール</td>
   <td>サポート対象外</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>タスクのタイムアウト時におけるタイトルの変更</td>
   <td>サポート対象外</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>タスク委任時とタスク要求時のメール</td>
   <td>サポート対象外</td>
   <td>サポート対象</td>
  </tr>
  <tr>
   <td>異なるグループ間での委任</td>
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
1. AEM Forms JEE ワークフローでレンダリングできるのは、アダプティブフォームだけです。アダプティブフォームを PDF ドキュメントとしてレンダリングすることはできません。
1. AEM Forms JEE ワークフローには、Adobe Sign 用の独立したステップは存在しません。AEM Forms JEE ワークフローに対して、Adobe Sign が有効になっているアダプティブフォームを使用する必要があります。詳しくは、[Adobe Sign のドキュメント](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component)を参照してください。
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
   <td><p>タスクの履歴と概要を追跡</p> </td>
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
