---
title: HTML5 フォーム のデバッグ
description: このドキュメントでは、既知の問題をトラブルシューティングする手順を示します。
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
feature: Mobile Forms
exl-id: 7330c03f-7102-43c0-aac6-825cce8a113d
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 39%

---

# HTML5 フォーム のデバッグ {#debugging-html-forms}

このドキュメントでは、いくつかのトラブルシューティングシナリオを説明します。 各シナリオで、問題のトラブルシューティングにいくつかの手順を示します。 次の手順に従い、問題が解決しない場合は、ロガーを設定してエラーや警告のログを取得し、確認します。 HTML5 フォームのロギングについて詳しくは、[HTML5 フォームのログの生成](/help/forms/using/enable-logs.md)を参照してください。

## 問題：フォームをレンダリングすると、org.apache.sling.api.SlingException 例外ページが表示される {#problem-when-rendering-the-form-i-see-org-apache-sling-api-slingexception-exception-page}

例外詳細で、「**caused by**」という語句を検索します。

考えられる理由は、URL の 1 つ以上のパラメーターが正しくないことです。

次のパラメーターを確認します。

<table>
 <tbody>
  <tr>
   <td><strong>パラメーター</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td>テンプレート</td>
   <td>テンプレートのファイル名</td>
  </tr>
  <tr>
   <td>contentRoot</td>
   <td>テンプレートと関連リソースが存在するパス</td>
  </tr>
  <tr>
   <td>dataRef</td>
   <td>テンプレートと結合されているデータファイルの絶対パス。<br /> 注意：パスは、データファイルの絶対パスを定義します。</td>
  </tr>
  <tr>
   <td>データ</td>
   <td>テンプレートと結合される UTF-8 でエンコードされたデータバイト。</td>
  </tr>
 </tbody>
</table>

## 問題：フォームをレンダリングできない（エラーメッセージが表示される） {#problem-unable-to-render-form}

1. 指定したパラメーターが正しいことを確認します。 パラメーターについて詳しくは、 [レンダリングパラメーター](#problem-when-rendering-the-form-i-see-org-apache-sling-api-slingexception-exception-page).
1. https://&lt;server>:&lt;port>/crx/packmgr/index.jsp で CRX パッケージマネージャーにログインし、以下のパッケージが正しくインストールされているかどうか確認します。

   * adobe-lc-forms-content-pkg-&lt;version>.zip
   * adobe-lc-forms-runtime-pkg-&lt;version>.zip

1. https://&lt;server>:&lt;port>/system/console/bundles で CQ web コンソール（Felix コンソール）にログインします。

   次のバンドルのステータスが「アクティブ」であることを確認します。

   * scala-lang.bundle [osgi]

   （com.adobe.livecyclescala-lang.bundle）

   * Adobe XFA Forms Renderer

   （com.adobe.livecycle.adobe-lc-forms-core）

   * Adobe XFA Forms LC Connector

   （com.adobe.livecycle.adobe-lc-forms-lc-connector）

## 問題：フォームがスタイルなしでレンダリングされる {#problem-form-renders-without-styles}

1. お使いのブラウザーで、**開発ツール**&#x200B;を開きます。profile.css が存在することを確認します。
1. profile.css ファイルが存在しない場合は、https://&lt;server>:&lt;port>/crx/de で CRX DE にログインします。
1. 左側のフォルダー階層で、 /etc/clientlibs/fd/xfaforms/に移動します。 フォルダーに一覧表示されている css.txt ファイルを開きます。

   * プロファイル
   * runtime
   * scrollnav
   * ツールバー
   * xfalib

1. css.txt 内に記載されているファイルが、/libs/fd/xfaforms/clientlibs/xfalib/css の CRX DE lite に存在することを確認します。

   ```css
   #base=css
   application.css
   dialog.css
   datepicker.css
   scribble.css
   listboxwidget.css
   ```

1. 上記のファイルが使用できない場合は、 adobe-lc-forms-runtime-pkg-&lt;version>.zip パッケージを再度作成します。

### 問題：予期しないエラーが発生しました {#problem-unexpected-error-encountered}

1. フォームの URL にクエリーパラメーター「debugClientLibs」を追加し、その値を「true」に設定します（例：https://&lt;サーバー>:&lt;ポート>/content/xfaforms/profiles/test.html?contentRoot=&lt;パス>&amp;template=&lt;xdp ファイル名>&amp;log=1-a9-b9-c9&amp;debugClientLibs=true）
1. Chrome などのデスクトップブラウザーで、デベロッパーツール/コンソールに移動します。
1. ログを開いて、エラーのタイプを特定します。 ログについて詳しくは、 [HTML5 フォームのログ](/help/forms/using/enable-logs.md).
1. 開発者ツール/コンソールに移動します。 スタックトレースを使用して、エラーの原因となっているコードを見つけます。 エラーをデバッグして問題を解決します。

   >[!NOTE]
   >
   >スクリプティングの失敗の場合は、フォームのPDFレンディション中にも同じ問題が発生するかどうかを確認します。 発生する場合は、フォームスクリプティングのロジックに問題があります。

## 問題：フォームを送信できません {#problem-unable-to-submit-the-form}

1. AEMサーバーにアクセスする権限があり、サーバーに接続していることを確認します。
1. パラメーター submitUrl が正しいことを確認します。
1. **1-a5-b5-c5** をデバッグオプションとして使用し、[HTML5 フォームのログ](/help/forms/using/enable-logs.md)に記載されている通りにクライアントサイドログを有効にします。次に、フォームをレンダリングし、送信をクリックします。ブラウザーのデバッグコンソールを開き、エラーがあるかどうかを確認します。
1. サーバーログを見つけます ( [HTML5 フォームのログ](/help/forms/using/enable-logs.md). 送信中にサーバーログにエラーが発生したかどうかを確認します。

## 問題：ローカライズされたエラーメッセージが表示されない {#problem-localized-error-messages-do-not-display}

1. 追加のクエリパラメーターでフォームをレンダリングする **debugClientLibs=true** デスクトップブラウザーで、デベロッパーツール/リソースに移動し、I18N.css ファイルの有無を確認します。
1. ファイルが存在しない場合は、https://&lt;サーバー>:&lt;ポート>/crx/de で CRX DE にログインします。
1. 左側のフォルダー階層で、/libs/fd/xfaforms/clientlibs/I18Nに移動し、次のファイルとフォルダーが存在することを確認します。

   * Namespace.js
   * LogMessages.js
   * 言語用のフォルダー

1. 上記のファイルまたはフォルダーのいずれかが存在しない場合は、 **adobe-lc-forms-runtime-pkg-&lt;version>.zip** もう一度パッケージ化します。
1. ロケール名と同じ名前のフォルダーに移動し、その内容を確認します。 フォルダーには次のファイルが含まれている必要があります。

   * I18N.js
   * js.txt

1. js.txt の内容を確認し、次のエントリが含まれていることを確認します。

   ```javascript
   ../Namespace.js
   I18N.js
   ../LogMessages.js
   ```

## 問題：画像が表示されない {#problem-image-not-showing-up}

1. 画像の URL が正しいことを確認します。
1. ブラウザーがこのタイプの画像をサポートしているかどうかを確認します。
1. 例外詳細で、「**caused by**」という語句を検索します。

   考えられる理由は、URL の 1 つ以上のパラメーターが正しくないことです。

   次のパラメーターを確認します。ステップテキスト

<table>
 <tbody>
  <tr>
   <td><strong>パラメーター</strong></td>
   <td><strong>説明</strong></td>
  </tr>
  <tr>
   <td>テンプレート</td>
   <td>テンプレートのファイル名</td>
  </tr>
  <tr>
   <td>contentRoot</td>
   <td>テンプレートと関連リソースが存在するパス</td>
  </tr>
  <tr>
   <td>dataRef</td>
   <td>テンプレートと結合されているデータファイルの絶対パス。<br /> 注意：パスは、データファイルの絶対パスを定義します。</td>
  </tr>
  <tr>
   <td>データ</td>
   <td>テンプレートと結合される UTF-8 でエンコードされたデータバイト。</td>
  </tr>
 </tbody>
</table>

1. デスクトップブラウザーで、デベロッパーツール/リソースに移動します。

   画像が表示される場合は、Frames の左側でチェックします。
