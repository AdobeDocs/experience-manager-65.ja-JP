---
title: HTML5 フォーム のデバッグ
seo-title: HTML5 フォーム のデバッグ
description: この文書では、既知の問題をトラブルシューティングするための手順をリストしています。
seo-description: この文書では、既知の問題をトラブルシューティングするための手順をリストしています。
uuid: df1835aa-6033-4ecb-97c8-4c3b7b96b943
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 5260d981-da40-40ab-834e-88e091840813
translation-type: tm+mt
source-git-commit: 998a127ce00c6cbb3db3a81d8a89d97ab9ef7469
workflow-type: tm+mt
source-wordcount: '830'
ht-degree: 67%

---


# HTML5 フォーム のデバッグ {#debugging-html-forms}

このドキュメントにはさまざまなトラブルシューティングのシナリオが含まれています。各シナリオにつき、問題をトラブルシューティングするためにいくつかの手順が提供されています。次の手順を実行し、引き続き問題が発生する場合は、ロガーを設定してエラーや警告のログを取得し、確認します。For more details about HTML5 forms logging, see [Generating Logs for HTML5 forms](/help/forms/using/enable-logs.md).

## 問題：フォームをレンダリングすると、org.apache.sling.api.SlingException 例外ページが表示される {#problem-when-rendering-the-form-i-see-org-apache-sling-api-slingexception-exception-page}

In the exception details, search for word **caused by**.

推定原因は、URL にある 1 つ以上のパラメーターが間違っていることです。

次のパラーメーターを確認します。

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
   <td>テンプレートと結合されるデータファイルの絶対パスです。<br />注意：パスはデータファイルの絶対パスを定義します。</td>
  </tr>
  <tr>
   <td>data</td>
   <td>テンプレートと結合されるUTF-8でエンコードされたデータバイトです。</td>
  </tr>
 </tbody>
</table>

## Problem: Unable to render a form (an error message is displayed) {#problem-unable-to-render-form}

1. 指定したパラメーターが正しいことを確認します。パラメーター関する詳しい情報については、[パラメーターのレンダリング](#problem-when-rendering-the-form-i-see-org-apache-sling-api-slingexception-exception-page)を参照してください。
1. CRX Package Manager(https://&lt;server>:&lt;port>/crx/packmgr/index.jsp)にログインし、次のパッケージが正しくインストールされているかどうかを確認します。

   * adobe-lc-forms-content-pkg-&lt;version>.zip
   * adobe-lc-forms-runtime-pkg-&lt;version>.zip

1. https://&lt;server>:&lt;port>/system/console/bundlesにあるCQ Webコンソール（Felixコンソール）にログインします。

   次のバンドルのステータスが「アクティブ」であることを確認します。

   * scala-lang.bundle [osgi]

   (com.adobe.livecyclescala-lang.bundle)

   * AdobeXFAFormsレンダラ

   (com.adobe.livecycle.adobe-lc-forms-core)

   * Adobe XFA Forms LC Connector

   (com.adobe.livecycle.adobe-lc-forms-lc-connector)

## 問題：フォームがスタイルなしでレンダリングされる {#problem-form-renders-without-styles}

1. In your browser, open **Developer Tools**. Ensure that profile.css is available.
1. プロファイルのCSSファイルが使用できない場合は、https://&lt;server>:&lt;port>/crx/deでCRX DEにログインします。
1. 左のフォルダー階層で、/etc/clientlibs/fd/xfaforms/ に移動します。フォルダーにリストされている css.txt ファイルを開きます。

   * プロファイル
   * runtime
   * scrollnav
   * ツールバー
   * xfalib

1. css.txt 内に記載されているファイルが /libs/fd/xfaforms/clientlibs/xfalib/css の CRX DE lite 内に存在することを確認します。

   ```css
   #base=css
   application.css
   dialog.css
   datepicker.css
   scribble.css
   listboxwidget.css
   ```

1. これらのファイルがない場合、adobe-lc-forms-runtime-pkg-&lt;version>.zip パッケージを再びインストールします。

### 問題：予期しないエラーが発生した {#problem-unexpected-error-encountered}

1. フォームURLで、クエリパラメーターdebugClientLibsを追加し、その値をtrueに設定します(例： https://&lt;server>:&lt;port>/content/xfaforms/profiles/test.html?contentRoot=&lt;some path>&amp;template=&lt;name of xdp file>&amp;log=1-a9-b9-c9&amp;debugClientLibs=true)
1. Chrome のようなデスクトップブラウザーでデベロッパーツール／Console に移動します。
1. ログを開いて、エラーのタイプを特定します。ログの詳細については、「[HTML5 フォームのログ](/help/forms/using/enable-logs.md)」を参照してください。
1. デベロッパーツール／Console に移動します。スタックトレースを使用して、エラーを起こしているコードを探します。エラーをデバッグして問題を解決します。

   >[!NOTE]
   >
   >スクリプティングの失敗の場合は、フォームの PDF レンダリングでも問題が発生するかを確認します。「はい」の場合、フォームスクリプティングのロジックに問題があります。

## 問題：フォームを送信できない {#problem-unable-to-submit-the-form}

1. AEM サーバーにアクセスする権限を持っていること、およびサーバーに接続されていることを確認します。
1. パラメーター submitUrl が正しいことを確認します。
1. Enable the client side logs as mentioned at [Logs for the HTML5 forms](/help/forms/using/enable-logs.md) using debug option as **1-a5-b5-c5**. 次に、フォームをレンダリングし、送信を確認します。ブラウザーのデバッグコンソールを開き、エラーがあるかどうかを確認します。
1. 「[HTML5 フォームのログ](/help/forms/using/enable-logs.md)」に記載されている通りに、サーバーログを見つけます。サーバーログで送信の際にエラーが発生したかを確認します。

## 問題：ローカライズされたエラーメッセージが表示されない {#problem-localized-error-messages-do-not-display}

1. デスクトップブラウザーで、追加のクエリーパラメーター **debugClientLibs=true** でフォームをレンダリングしてから、デベロッパーツール／Resources に移動して、I18N.css のファイルの存在を確認します。
1. ファイルが使用できない場合は、https://&lt;server>:&lt;port>/crx/deでCRX DEにログインします。
1. 左のフォルダー階層で /libs/fd/xfaforms/clientlibs/I18N に移動し、次のファイルとフォルダーが存在することを確認します。

   * Namespace.js
   * LogMessages.js
   * 言語用のフォルダー

1. 上記のファイルまたはフォルダーで存在しないものがある場合は、**adobe-lc-forms-runtime-pkg-&lt;version>.zip** パッケージを再びインストールします。
1. ロケールの名前と同じ名前のフォルダ-に移動し、そのコンテンツを確認します。フォルダーには次のファイルが含まれている必要があります。

   * I18N.js
   * js.txt

1. js.txt のコンテンツを確認して、次のエントリがあることを確かめます。

   ```javascript
   ../Namespace.js
   I18N.js
   ../LogMessages.js
   ```

## 問題：画像が表示されない {#problem-image-not-showing-up}

1. 画像 URL が正しいことを確認します。
1. ブラウザーがこのタイプの画像をサポートしているかどうかを確認します。
1. In the exception details, search for word **caused by**.

   推定原因は、URL にある 1 つ以上のパラメーターが間違っていることです。

   次のパラーメーターを確認します。
ステップテキスト

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
   <td>テンプレートと結合されるデータファイルの絶対パスです。<br />注意：パスはデータファイルの絶対パスを定義します。</td>
  </tr>
  <tr>
   <td>data</td>
   <td>テンプレートと結合されるUTF-8でエンコードされたデータバイトです。</td>
  </tr>
 </tbody>
</table>

1. デスクトップブラウザーで、デベロッパーツール／Resources に移動します。

   画像が表示されるか、左側で「Frames」を確認します。
