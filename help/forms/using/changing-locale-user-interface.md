---
title: AEM Forms Workspace ユーザーインターフェイスのロケールの変更
seo-title: AEM Forms Workspace ユーザーインターフェイスのロケールの変更
description: インターフェイス上で AEM Forms Workspace を変更してテキスト、折りたたまれているカテゴリ、キュー、プロセス、および日付選択をローカライズする方法。
seo-description: インターフェイス上で AEM Forms Workspace を変更してテキスト、折りたたまれているカテゴリ、キュー、プロセス、および日付選択をローカライズする方法。
uuid: c89ff150-a36e-45cc-99a6-8768dbe58eab
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 89f9d666-28e2-4201-8467-ae90693ca5d2
docset: aem65
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '587'
ht-degree: 61%

---


# AEM Forms Workspace ユーザーインターフェイスのロケールの変更{#changing-the-locale-of-aem-forms-workspace-user-interface}

AEM Formsのワークスペースでは、英語、フランス語、ドイツ語、日本語に対するサポートがすぐに利用できます。 また、AEM Formsワークスペースユーザーインターフェイスを他の言語にローカライズする機能も提供します。

AEM Formsワークスペースユーザーインターフェイスを任意の言語にローカライズするには：

* AEM Forms Workspace のテキストをローカライズします。
* 折りたたまれているカテゴリ、キュー、およびプロセスをローカライズする。
* 日付選択をローカライズする。

上記の手順を実行する前に、[AEM Formsワークスペースのカスタマイズの一般的な手順](../../forms/using/generic-steps-html-workspace-customization.md)に示されている手順に従っていることを確認してください。

>[!NOTE]
>
>AEM Forms Workspace のログイン画面の言語を変更するには、「[新しいログイン画面の作成](../../forms/using/creating-new-login-screen.md)」を参照してください。

## テキストのローカライズ  {#localizing-text}

次の手順を実行して、言語&#x200B;*新しい*&#x200B;とブラウザーのロケールコード&#x200B;*nw*&#x200B;のサポートを追加します。

1. CRXDE Lite にログインします。CRXDE LiteのデフォルトURLは`https://'[server]:[port]'/lc/crx/de/index.jsp`です。
1. 場所`apps/ws/locales`に移動し、新しいフォルダー`nw.`を作成します
1. ファイル`translation.json`を`/apps/ws/locales/en-US`から`/apps/ws/locales/nw`にコピーします。
1. `/apps/ws/locales/nw`に移動し、`translation.json`を開いて編集します。 translation.json ファイルにロケール固有の変更を行います。

   次の例では、AEM Forms Workspace の英語およびフランス語のロケールの translation.json ファイルを示します。

   ![translation_json_in_](assets/translation_json_in_en.png) ![entranslation_json_in_fr](assets/translation_json_in_fr.png)

## 折りたたまれているカテゴリ、キュー、およびプロセスのローカライズ {#localizing-collapsed-categories-queues-and-processes}

AEM Formsワークスペースは、画像を使用してカテゴリ、キューおよびプロセスのヘッダーを表示します。 これらのヘッダをローカライズするには、開発パッケージが必要です。開発パッケージの作成について詳しくは、「[AEM Formsワークスペースコードの構築」を参照してください。](introduction-customizing-html-workspace.md#building-html-workspace-code)

次の手順では、新しくローカライズされた画像ファイルは&#x200B;*Categories_nw.png*、*Queue_nw.png*、および *Processes_nw.png* であると想定しています。画像の推奨される幅は19pxです。

>[!NOTE]
>
>お使いのブラウザのブラウザ言語ロケールコードを検索するには、次のようにします。開く `https://'[server]:[port]'/lc/libs/ws/Locale.html`.

![collapsing_panels_image](assets/collapsing_panels_image.png)

次の手順を実行して画像をローカライズします。

1. WebDAV クライアントを使用して、画像ファイルを */apps/ws/images* フォルダーに配置します。
1. */apps/ws/css* に移動します。*newStyle.css* を開いて編集し、次のエントリを追加します。

   ```css
   #categoryListBar .content.nw {
        background: #3e3e3e url(../images/Categories_nw.png) no-repeat 10px 10px;
    }
   
   #filterListBar .content.nw {
       background: #3e3e3e url(../images/Queues_nw.png) no-repeat 10px 10px;
   }
   
   #processNameListBar .content.nw {
       background: #3e3e3e url(../images/Processes_nw.png) no-repeat 10px 10px;
   }
   ```

1. 「[Workspaceのカスタマイズ](../../forms/using/introduction-customizing-html-workspace.md)」記事に一覧表示されているすべてのセマンティックの変更を実行します。
1. */js/runtime/utility* フォルダーに移動し、*usersession.js* ファイルを開いて編集します。
1. 元のコードブロックに一覧表示されているコードを探して、if ステートメントに条件 *lang !== &#39;nw&#39;*&#x200B;をif文に追加します。

   ```javascript
   // Orignal code
   setLocale = function () {
           var lang = $.trim(i18n.lng());
           if (lang === null || lang === '' || (lang !== 'fr-FR' && lang !== 'de-DE' && lang !== 'ja-JP')) {
               window.lcWorkspace.locale = 'en-US';
           } else {
               window.lcWorkspace.locale = lang;
           }
       }
   ```

   ```javascript
   //new code
    setLocale = function () {
           var lang = $.trim(i18n.lng());
           if (lang === null || lang === '' || (lang !== 'fr-FR' && lang !== 'de-DE' && lang !== 'ja-JP' && lang !== 'nw')) {
               window.lcWorkspace.locale = 'en-US';
           } else {
               window.lcWorkspace.locale = lang;
           }
       }
   ```

## 日付選択のローカライズ {#localizing-date-picker}

*日付選択* API をローカライズするには、開発パッケージが必要です。開発パッケージの作成について詳しくは、「[AEM Formsワークスペースコード](introduction-customizing-html-workspace.md#building-html-workspace-code)の構築」を参照してください。

1. [jQuery UI パッケージ](https://jqueryui.com/download/all/)をダウンロードして抽出し、*&lt;抽出された jquery UI パッケージ>*\jquery-ui-1.10.2.zip\jquery-ui-1.10.2\ui\i18n に移動します。
1. ロケールコード nw の jquery.ui.datepicker-nw.js ファイルを apps/ws/js/libs/jqueryui にコピーして、ファイルにロケール固有の変更を行います。
1. `apps/ws/js`に移動し、`jquery.ui.datepicker-nw.js`ファイルを開いて編集します。
1. main.jsファイルで`jquery.ui.datepicker-nw.js.`のエイリアスを作成します。`jquery.ui.datepicker-nw.js`ファイルのエイリアスを作成するコードは次のとおりです。

   ```javascript
   jqueryuidatepickernw : pathprefix + 'libs/jqueryui/jquery.ui.datepicker-nw'
   ```

1. 日付選択を使用するすべてのファイルに`jqueryuidatepickernw`ファイルを含めるには、エイリアス&lt;a0/>を使用します。 `jquery.ui.datepicker-nw.js`日付選択は次のファイルで使用されます。

   * `js/runtime/views/outofoffice.js`
   * `js/runtime/views/searchtemplatedetails.js`

   以下のサンプルコードは、jquery.ui.datepicker-nw.js のエントリを追加する方法を示します。

   ```json
   //Original Code
   define([
       'jquery',
       'underscore',
       'backbone',
       'jqueryui',
       'jqueryuidatepickerja',
       'jqueryuidatepickerde',
       'jqueryuidatepickerfr',
       'slimscroll',
       'usersearchview',
       'logmanagerutil',
       'loggerutil'
   ], function ($, _, Backbone, jQueryUI, jQueryUIDatePickerJA, jQueryUIDatePickerDE, jQueryUIDatePickerFR, slimScroll, UserSearch, LogManager, Logger) {
   ```

   ```json
   // Code with Date Picker alias for new language
   define([
       'jquery',
       'underscore',
       'backbone',
       'jqueryui',
       'jqueryuidatepickerja',
       'jqueryuidatepickerde',
       'jqueryuidatepickerfr',
       'jqueryuidatepickernw', // Date Picker alias
       'slimscroll',
       'usersearchview',
       'logmanagerutil',
       'loggerutil'
   ], function ($, _, Backbone, jQueryUI, jQueryUIDatePickerJA, jQueryUIDatePickerDE, jQueryUIDatePickerFR, jQueryUIDatePickerNW, slimScroll, UserSearch, LogManager, Logger) {
   ```

1. 日付選択 API を使用するすべてのファイルで、デフォルトの日付選択 API の設定を変更します。日付選択 API は次のファイルで使用されます。

   * apps\ws\js\runtime\views\searchtemplatedetails.js
   * apps\ws\js\runtime\views\outofoffice.js

   次のコードを変更して新しいロケールを追加します。

   ```javascript
   if (locale === 'ja-JP') {
      $.datepicker.setDefaults($.datepicker.regional.ja);
   } else if (locale === 'de-DE') {
      $.datepicker.setDefaults($.datepicker.regional.de);
   } else if (locale === 'fr-FR') {
      $.datepicker.setDefaults($.datepicker.regional.fr);
   } else {
      $.datepicker.setDefaults($.datepicker.regional['']);
   }
   ```

   ```javascript
   if (locale === 'ja-JP') {
       $.datepicker.setDefaults($.datepicker.regional.ja);
   } else if (locale === 'de-DE') {
       $.datepicker.setDefaults($.datepicker.regional.de);
   } else if (locale === 'fr-FR') {
       $.datepicker.setDefaults($.datepicker.regional.fr);
   } else if (locale === 'nw') {
       $.datepicker.setDefaults($.datepicker.regional.nw);
   } else {
       $.datepicker.setDefaults($.datepicker.regional['']);
   }
   ```
