---
title: 外部 Web ページへのアダプティブフォームの埋め込み
seo-title: 外部 Web ページへのアダプティブフォームの埋め込み
description: 外部 Web ページにアダプティブフォームを埋め込む方法について学びましょう
seo-description: 外部 HTML Web ページにアダプティブフォームを埋め込む方法について学びましょう
uuid: d81032dd-af80-4f4b-a717-ee1b89fd3d3d
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: author
discoiquuid: d739c6da-3b41-4452-8728-d7cd1a3ae20b
docset: aem65
translation-type: tm+mt
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '979'
ht-degree: 65%

---


# 外部 Web ページへのアダプティブフォームの埋め込み{#embed-adaptive-form-in-external-web-page}

AEM の外側にホストされた Web ページか [AEM サイトページに、アダプティブフォームをシームレスに埋め込む](/help/forms/using/embed-adaptive-form-aem-sites.md)ことができます。埋め込まれたアダプティブフォームではすべての機能を使用できるため、ユーザーは、ページから移動することなくフォームを記入および送信できます。これにより、ユーザーは Web ページのその他のエレメントから離れることなく、同時にフォームの操作を行うことができます。。

## 前提条件 {#prerequisites}

外部 Web サイトにアダプティブフォームを埋め込む前に次の手順を実行します。

* AEM Forms サーバーのパブリッシュインスタンスに埋め込むアダプティブフォームを発行します。
* Web サイト上で、アダプティブフォームをホストする Web ページを決定するか、新規に作成します。Ensure that the webpage can [read jQuery files from a CDN](https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js) or has a local copy of the jQuery embeded. アダプティブフォームをレンダリングするには、jQueryが必要です。
* When AEM server and the web page are on different domains, perform the steps listed in sectiion, [enable AEM Forms to serve adaptive forms to a cross domain site](#cross-site).

## アダプティブフォームの埋め込み {#embed-adaptive-form}

WebページにJavaScriptの数行を挿入することで、アダプティブフォームを埋め込むことができます。 コードの API は AEM サーバーにアダプティブフォームのリソースを求める HTTP リクエストを送信し、指定したフォームコンテナにアダプティブフォームを挿入します。

アダプティブフォームを埋め込むには：

1. 次のコードを使用して、Webサイト上にWebページを作成します。

   ```html
   <!doctype html>
   <html>
     <head>
       <title>This is the title of the webpage!</title>
       <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
     </head>
     <body>
     <div class="customafsection"/>
       <p>This section is replaced with the adaptive form.</p>
   
    <script>
    var options = {path:"/content/forms/af/locbasic.html", dataRef:"", themepath:"", CSS_Selector:".customafsection"};
    alert(options.path);
    var loadAdaptiveForm = function(options){
    //alert(options.path);
       if(options.path) {
           // options.path refers to the publish URL of the adaptive form
           // For Example: https:myserver:4503/content/forms/af/ABC, where ABC is the adaptive form
           // Note: If AEM server is running on a context path, the adaptive form URL must contain the context path
           var path = options.path;
           path += "/jcr:content/guideContainer.html";
           $.ajax({
               url  : path ,
               type : "GET",
               data : {
                   // Set the wcmmode to be disabled
                   wcmmode : "disabled"
                   // Set the data reference, if any
                  // "dataRef": options.dataRef
                   // Specify a different theme for the form object
                 //  "themeOverride" : options.themepath
               },
               async: false,
               success: function (data) {
                   // If jquery is loaded, set the inner html of the container
                   // If jquery is not loaded, use APIs provided by document to set the inner HTML but these APIs would not evaluate the script tag in HTML as per the HTML5 spec
                   // For example: document.getElementById().innerHTML
                   if(window.$ && options.CSS_Selector){
                       // HTML API of jquery extracts the tags, updates the DOM, and evaluates the code embedded in the script tag.
                       $(options.CSS_Selector).html(data);
                   }
               },
               error: function (data) {
                   // any error handler
               }
           });
       } else {
           if (typeof(console) !== "undefined") {
               console.log("Path of Adaptive Form not specified to loadAdaptiveForm");
           }
       }
    }(options);
   
    </script>
     </body>
   </html>
   ```

1. 埋め込まれたコードで：

   * Change value of the *options.path* variable with the path of the publish URL of the adaptive form. AEM サーバーがコンテキストパス上で実行されている場合は、その URL にコンテキストパスが含まれるようにします。例えば、上記のコードとアダプティブフォームは同じaem formsサーバー上に存在するので、例ではアダプティブフォーム/content/forms/af/locbasic.htmlのコンテキストパスを使用しています。
   * *options.dataRef* を URL を渡す属性と置き換えます。You can use the dataref variable to [prefill an adaptive form](/help/forms/using/prepopulate-adaptive-form-fields.md).
   * *options.themePath* をアダプティブフォームで設定されたテーマ以外のテーマへのパスと置き換えます。また、リクエストの属性を使用してテーマのパスを指定することができます。
   * CSS_Selector は、アダプティブフォームが埋め込まれているフォームコンテナの CSS セレクターです。例えば、.customafsection cssクラスは、上記の例のCSSセレクターです。

アダプティブフォームが Web ページに埋め込まれました。埋め込まれたアダプティブフォームで次を確認します。

* 元のアダプティブフォームにあったヘッダーとフッターは、埋め込まれたフォームには含まれません。
* ドラフトおよび送信済みフォームは、フォームポータル上の「ドラフト」タブと「送信」タブで使用できます。
* 元のアダプティブフォームに構築された送信アクションは、埋め込まれたフォームでも保持されます。
* アダプティブフォームのルールは保持され、埋め込みフォームでも完全に機能します。
* 元のフォームに構築されたのエクスペリエンスのターゲット設定と A/B テストは、埋め込まれたアダプティブフォームでは動作しません。
* 元のフォームに Adobe Analytics が構築されている場合、分析データは Adobe Analytics サーバーで取得されます。ただし、フォームの分析レポートでは使用できません。

## サンプルトポロジー {#sample-topology}

アダプティブフォームを埋め込む外部 Web ページは、プライベートネットワークのファイアウォールの中にある AEM サーバーにリクエストを送信します。リクエストを安全に AEM サーバーに向けるようにするには、リバースプロキシサーバーを設定することをお勧めします。

ディスパッチャーなしで Apache 2.4 リバースプロキシサーバーをセットアップする方法について説明します。In this example, you will host the AEM server with `/forms` context path and map `/forms` for the reverse proxy. It ensures that any request for `/forms` on Apache server are directed to the AEM instance. This topology helps reduces the number of rules at the dispatcher layer as all request prefixed with `/forms` route to the AEM server.

1. `httpd.conf` 設定ファイルを開き、次のコードの行をコメント解除します。または、これらのコードの行をファイルに追加することができます。

   ```text
   LoadModule proxy_html_module modules/mod_proxy_html.so
   LoadModule proxy_http_module modules/mod_proxy_http.so
   ```

1. Set up proxy rules by adding the following lines of code in the `httpd-proxy.conf` configuration file.

   ```text
   ProxyPass /forms https://[AEM_Instance]/forms
   ProxyPassReverse /forms https://[AEM_Instance]/forms
   ```

   Replace `[AEM_Instance]` with the AEM server publish URL in the rules.

コンテキストパスにAEMサーバーをマウントしない場合、Apacheレイヤーのプロキシルールは次のようになります。

```text
ProxyPass /content https://<AEM_Instance>/content
ProxyPass /etc https://<AEM_Instance>/etc
ProxyPass /etc.clientlibs https://<AEM_Instance>/etc.clientlibs
# CSRF Filter
ProxyPass /libs/granite/csrf/token.json https://<AEM_Instance>/libs/granite/csrf/token.json

ProxyPassReverse /etc https://<AEM_Instance>/etc
ProxyPassReverse /etc.clientlibs https://<AEM_Instance>/etc.clientlibs
# written for thank you page and other URL present in AF during redirect
ProxyPassReverse /content https://<AEM_Instance>/content
```

>[!NOTE]
>
>その他のトポロジを設定する場合は、送信、事前入力およびその他のURLをディスパッチャーレイヤーの許可リストに追加します。

## ベストプラクティス {#best-practices}

Web ページにアダプティブフォームを埋め込む場合、次のベストプラクティスを検討します。

* Web ページの CSS に定義されたスタイルルールが、フォームオブジェクト CSS と衝突しないようにしてください。衝突を避けるため、アダプティブフォームテーマの Web ページ CSS を AEM クライアントライブラリを使用して再利用できます。アダプティブフォームテーマのクライアントライブラリの使用について詳しくは、「[AEM Forms のテーマ](../../forms/using/themes.md)」を参照してください。
* Web ページのフォームコンテナがウィンドウの幅全体を使用するようにしてください。これにより、モバイルデバイスに設定された CSS ルールが確実に変更なしで動作するようになります。フォームコンテナがウィンドウの幅全体に表示されない場合は、さまざまなモバイルデバイスに適合するようにカスタムの CSS を記述する必要があります。
* Use `[getData](https://helpx.adobe.com/experience-manager/6-3/forms/javascript-api/GuideBridge.html)` API to get the XML or JSON representation of form data in client.
* Use `[unloadAdaptiveForm](https://helpx.adobe.com/experience-manager/6-3/forms/javascript-api/GuideBridge.html)` API to unload the adaptive form from HTML DOM.
* AEMサーバーから応答を送信する際に、アクセス制御接触チャネルのヘッダーを設定します。

## AEM Forms がクロスドメインサイトに対してアダプティブフォームをサーブできるようにする {#cross-site}

1. On AEM author instance, go to AEM Web Console Configuration Manager at `https://'[server]:[port]'/system/console/configMgr`.
1. **Apache Sling Referrer Filter** 構成を探して開きます。
1. 「許可済みホスト」フィールドで、Web ページが存在するドメインを指定します。これにより、ホストは AEM サーバーに POST リクエストをできるようになります。正規式を使用して、一連の外部アプリケーションドメインを指定することもできます。

