---
title: CustomToolbarsでのHTMLFormsのレンダリング
seo-title: CustomToolbarsでのHTMLFormsのレンダリング
description: 'null'
seo-description: 'null'
uuid: b9c9464e-ff19-4051-a39b-4ec71c512d10
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 7eb0e8a8-d76a-43f7-a012-c21157b14cd4
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '2304'
ht-degree: 1%

---


# CustomToolbars {#rendering-html-forms-with-customtoolbars}でHTMLFormsをレンダリング

## カスタムツールバーでのHTMLFormsのレンダリング{#rendering-html-forms-with-custom-toolbars}

Formsサービスでは、HTMLフォームでレンダリングされるツールバーをカスタマイズできます。 ツールバーは、初期設定のCSSスタイルを上書きして外観を変更するようカスタマイズしたり、Javaスクリプトを上書きして動的な動作を追加したりすることができます。 ツールバーは、fscmenu.xmlというXMLファイルを使用してカスタマイズします。 デフォルトでは、Formsサービスは内部的に指定されたURIの場所からこのファイルを取得します。

>[!NOTE]
>
>このURIの場所は、adobe-forms-core.jarファイルにあります。このファイルは、adobe-forms-dsc.jarファイル内にあります。 adobe-forms-dsc.jarファイルは、C:\Adobe\Adobe_Experience_Manager_forms\ folder (C:\ is the installation directory)にあります。 Win RARなどのファイル抽出ツールを使用して、アドビを開くことができます。

この場所からfscmenu.xmlをコピーし、必要に応じて変更して、カスタムURIの場所に配置できます。 次に、FormsサービスAPIを使用して、指定した場所にあるfscmenu.xmlファイルを使用してFormsサービスを開始するランタイムオプションを設定します。 これらのアクションにより、Formsサービスはカスタムツールバーを持つHTMLフォームをレンダリングします。

fscmenu.xmlファイルに加えて、次のファイルも取得する必要があります。

* fscmenu.js
* fscattachments.js
* fscmenu.css
* fscmenu-v.css
* fscmenu-ie.css
* fscdialog.css

fscJSは、各ノードに関連付けられているJavaスクリプトです。 `div#fscmenu`ノード用と`ul#fscmenuItem`ノード用に1つを指定する必要があります。 JSファイルは、コアツールバー機能を実装し、デフォルトファイルが機能します。

fscCSSは、特定のノードに関連付けられたスタイルシートです。 CSSファイル内のスタイルは、ツールバーの外観を指定します。 *fscVCSSは、レンダリングされたHTMLフォームの左側に表示される、垂直方向のツールバーのスタイルシートです。* *fscIECSSは、Internet ExplorerでレンダリングされるHTMLフォームに使用されるスタイルシートです。* 

上記のすべてのファイルがfscmenu.xmlファイルで参照されていることを確認します。 つまり、fscmenu.xmlファイルで、これらのファイルを指すURIの場所を指定します。これにより、Formsサービスでこれらのファイルを見つけられるようになります。 デフォルトでは、これらのファイルは、内部キーワード`FSWebRoot`または`ApplicationWebRoot`で始まるURIの場所で使用できます。

ツールバーをカスタマイズするには、外部キーワード`FSToolBarURI`を使用してキーワードを置き換えます。 このキーワードは、実行時にFormsサービスに渡されるURIを表します（この方法は後で示します）。

これらのJSファイルとCSSファイルの絶対位置を指定することもできます(例：https://www.mycompany.com/scripts/misc/fscmenu.js)。 この場合、`FSToolBarURI`キーワードを使用する必要はありません。

>[!NOTE]
>
>これらのファイルの参照方法を混在させないことをお勧めします。 つまり、すべてのURIは`FSToolBarURI`キーワードまたは絶対位置を使用して参照する必要があります。

JSファイルとCSSファイルは、adobe-forms-&lt;appserver>.earファイルを開いて取得できます。 このファイル内で、adobe-forms-res.warを開きます。 これらのファイルはすべてWARファイル内にあります。 adobe-forms-&lt;appserver>.earファイルは、AEM formsのインストールフォルダー(C:\ is the installation directory)にあります。 WinRARなどのファイル抽出ツールを使用して、adobe-forms-&lt;appserver>.earを開くことができます。

次のXML構文は、fscmenu.xmlファイルの例を示しています。

```html
 <div id="fscmenu" fscJS="FSToolBarURI/scripts/fscmenu.js" fscCSS="FSToolBarURI/fscmenu.css" fscVCSS="FSToolBarURI/fscmenu-v.css" fscIECSS="FSToolBarURI/fscmenu-ie.css">
         <ul class="fscmenuItem" id="Home">
             <li>
                 <a href="#" fscTarget="_top" tabindex="1">Home</a>
             </li>
         </ul>
         <ul class="fscmenuItem" id="Upload" fscJS="FSToolBarURI/scripts/fscattachments.js" fscCSS="FSToolBarURI/fscdialog.css">
             <li>
                 <a tabindex="2">Upload Attachments</a>
                 <ul class="fscmenuPopup" id="fscUploadAttachments">
                     <li>
                         <a href="javascript:doUploadDialog();" tabindex="3">Add ...</a>
                     </li>
                     <li>
                         <a href="javascript:doDeleteDialog();" tabindex="4">Delete ...</a>
                     </li>
                 </ul>
             </li>
         </ul>
         <ul class="fscmenuItem" id="Download">
             <li>
                 <a tabindex="100">Download Attachments</a>
                 <ul class="fscmenuPopup">
                     <li>
                         <a tabindex="101">None available</a>
                     </li>
                 </ul>
             </li>
         </ul>
     </div>
```

>[!NOTE]
>
>太字のテキストは、参照する必要があるCSSファイルとJSファイルのURIを表しています。

次の項目では、ツールバーのカスタマイズ方法を説明します。

* `fscJS`、`fscCSS`、`fscVCSS`、`fscIECSS`の各属性（fscmenu.xmlファイル内）の値を変更し、参照ファイルのカスタムの場所を反映します。これには、この節で説明する方法（例：`fscJS="FSToolBarURI/scripts/fscmenu.js"`）を使用します。
* すべてのCSSファイルとJSファイルを指定する必要があります。 どのファイルも変更されない場合は、カスタムの場所にデフォルトのファイルを指定します。 この節で説明する様々なファイルを開いて、デフォルトのファイルを取得できます。
* 任意のファイルに絶対参照(例えば、https://www.example.com/scripts/custom-vertical-fscmenu.css)を指定できます。
* `div#fscmenu`ノードが必要とするJSファイルとCSSファイルは、ツールバー機能に不可欠です。 個々の`ul#fscmenuItem`ノードには、サポートするJSファイルまたはCSSファイルがある場合とない場合があります。

**ローカル値の変更**

ツールバーのカスタマイズの一環として、ツールバーのロケール値を変更できます。 つまり、別の言語で表示できます。 次の図に、フランス語で表示されるカスタムツールバーを示します。

>[!NOTE]
>
>複数の言語でカスタムツールバーを作成することはできません。 ツールバーでは、ロケールの設定に基づいて異なるXMLファイルを使用できません。

ツールバーのロケール値を変更するには、fscmenu.xmlファイルに表示する言語が含まれていることを確認します。 次のXML構文は、フランス語のツールバーの表示に使用されるfscmenu.xmlファイルを示しています。

```html
 <div id="fscmenu" fscJS="FSToolBarURI/scripts/fscmenu.js" fscCSS="FSToolBarURI/fscmenu.css" fscVCSS="FSToolBarURI/fscmenu-v.css" fscIECSS="FSToolBarURI/fscmenu-ie.css">
         <ul class="fscmenuItem" id="Home">
             <li>
                 <a href="#" fscTarget="_top" tabindex="1">Accueil</a>
             </li>
         </ul>
         <ul class="fscmenuItem" id="Upload" fscJS="FSToolBarURI/scripts/fscattachments.js" fscCSS="FSToolBarURI/fscdialog.css">
             <li>
                 <a tabindex="2">Télécharger les pièces jointes</a>
                 <ul class="fscmenuPopup" id="fscUploadAttachments">
                     <li>
                         <a href="javascript:doUploadDialog();" tabindex="3">Ajouter...</a>
                     </li>
                     <li>
                         <a href="javascript:doDeleteDialog();" tabindex="4">Supprimer...</a>
                     </li>
                 </ul>
             </li>
         </ul>
         <ul class="fscmenuItem" id="Download">
             <li>
                 <a tabindex="100">Télécharger les pièces jointes</a>
                 <ul class="fscmenuPopup">
                     <li>
                         <a tabindex="101">Aucune disponible</a>
                     </li>
                 </ul>
             </li>
         </ul>
     </div>
```

>[!NOTE]
>
>このセクションに関連付けられているクイック開始は、前の図のように、このXMLファイルを使用してフランス語のカスタムツールバーを表示します。

また、`HTMLRenderSpec`オブジェクトの`setLocale`メソッドを呼び出し、ロケール値を指定する文字列値を渡すことで、有効なロケール値を指定します。 例えば、`fr_FR`を渡してフランス語を指定します。 Formsサービスはローカライズされたツールバーにバンドルされています。

>[!NOTE]
>
>カスタムツールバーを使用するHTMLフォームをレンダリングする前に、HTMLフォームのレンダリング方法を知っておく必要があります。 ([HTMLとしてのFormsのレンダリング](/help/forms/developing/rendering-forms-html.md)を参照)。

Formsサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順{#summary-of-steps}の概要

カスタムツールバーを含むHTMLフォームをレンダリングするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. FormsJava APIオブジェクトを作成します。
1. カスタムfscmenu XMLファイルを参照します。
1. HTMLフォームをレンダリングする。
1. フォームデータストリームをクライアントのWebブラウザーに書き込みます。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを含めます。

**FormsJava APIオブジェクトの作成**

Formsサービスがサポートする操作をプログラムで実行する前に、Formsクライアントオブジェクトを作成する必要があります。

**カスタムfscmenu XMLファイルの参照**

カスタムツールバーを含むHTMLフォームをレンダリングするには、ツールバーを説明するfscmenu XMLファイルを参照します。 （この節では、fscmenu XMLファイルの2つの例を示します）。 また、fscmenu.xmlファイルで、すべての参照ファイルの場所が正しく指定されていることを確認してください。 この節で前述したように、すべてのファイルが`FSToolBarURI`キーワードか、絶対位置で参照されていることを確認してください。

**HTMLフォームのレンダリング**

HTMLフォームをレンダリングするには、Designerで作成し、XDPファイルとして保存したフォームデザインを指定します。 HTML変換タイプも選択します。 例えば、Internet Explorer 5.0以降用の動的HTMLをレンダリングするHTML変換タイプを指定できます。

HTMLフォームのレンダリングには、他のフォームタイプをレンダリングするためのURI値などの値も必要です。

**フォームデータストリームをクライアントのWebブラウザーに書き込みます**

Formsサービスは、HTMLフォームをレンダリングするときに、フォームデータストリームを返します。このストリームをユーザーに表示するには、クライアントのWebブラウザーに書き込む必要があります。

**関連トピック**

[Java APIを使用してカスタムツールバーでHTMLフォームをレンダリングする](#render-an-html-form-with-a-custom-toolbar-using-the-java-api)

[WebサービスAPIを使用したカスタムツールバーを使用したHTMLフォームのレンダリング](#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[FormsサービスAPIクイック開始](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[インタラクティブPDF formsのレンダリング](/help/forms/developing/rendering-interactive-pdf-forms.md)

[FormsをHTMLとしてレンダリング](/help/forms/developing/rendering-forms-html.md)

[FormsをレンダリングするWeb アプリケーションの作成](/help/forms/developing/creating-web-applications-renders-forms.md)

### Java API {#render-an-html-form-with-a-custom-toolbar-using-the-java-api}を使用してカスタムツールバーでHTMLフォームをレンダリングする

FormsサービスAPI(Java)を使用して、カスタムツールバーを含むHTMLフォームをレンダリングします。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-forms-client.jarなどのクライアントJARファイルを含めます。

1. FormsJava APIオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `FormsServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. カスタムfscmenu XMLファイルの参照

   * コンストラクターを使用して`HTMLRenderSpec`オブジェクトを作成します。
   * ツールバーを含むHTMLフォームをレンダリングするには、`HTMLRenderSpec`オブジェクトの`setHTMLToolbar`メソッドを呼び出し、`HTMLToolbar`列挙値を渡します。 例えば、垂直方向のHTMLツールバーを表示するには、`HTMLToolbar.Vertical`を渡します。
   * `HTMLRenderSpec`オブジェクトの`setToolbarURI`メソッドを呼び出し、XMLファイルのURIの場所を指定する文字列値を渡して、fscmenu XMLファイルの場所を指定します。
   * 該当する場合は、`HTMLRenderSpec`オブジェクトの`setLocale`メソッドを呼び出し、ロケール値を指定する文字列値を渡して、ロケール値を設定します。 デフォルト値は英語です。

   >[!NOTE]
   >
   >このセクションに関連付けられているクイック開始では、この値を&#x200B;`fr_FR`*.*&#x200B;に設定します。

1. HTMLフォームのレンダリング

   `FormsServiceClient`オブジェクトの`renderHTMLForm`メソッドを呼び出し、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定するstring値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`など、完全なパスを必ず指定してください。
   * HTML環境設定の種類を指定する`TransformTo`列挙値。 例えば、Internet Explorer 5.0以降用の動的HTMLと互換性のあるHTMLフォームをレンダリングするには、`TransformTo.MSDHTML`を指定します。
   * フォームとマージするデータを含む`com.adobe.idp.Document`オブジェクト。 データをマージしない場合は、空の`com.adobe.idp.Document`オブジェクトを渡します。
   * HTML実行時オプションを格納する`HTMLRenderSpec`オブジェクト。
   * `HTTP_USER_AGENT`ヘッダー値を指定するstring値（`Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`など）。
   * HTMLフォームのレンダリングに必要なURI値を格納する`URLSpec`オブジェクト。
   * 添付ファイルを格納する`java.util.HashMap`オブジェクト。 これはオプションのパラメーターです。フォームにファイルを添付しない場合は、`null`を指定できます。

   `renderHTMLForm`メソッドは、クライアントのWebブラウザーに書き込む必要があるフォームデータストリームを含む`FormsResult`オブジェクトを返します。

1. フォームデータストリームをクライアントのWebブラウザーに書き込みます

   * `FormsResult`オブジェクト&#39;s `getOutputContent`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトを作成します。
   * `getContentType`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトのコンテンツタイプを取得します。
   * `javax.servlet.http.HttpServletResponse`オブジェクトのコンテンツタイプを設定するには、`setContentType`メソッドを呼び出し、`com.adobe.idp.Document`オブジェクトのコンテンツタイプを渡します。
   * `javax.servlet.http.HttpServletResponse`オブジェクトの`getOutputStream`メソッドを呼び出して、フォームデータストリームをクライアントWebブラウザーに書き込むために使用する`javax.servlet.ServletOutputStream`オブジェクトを作成します。
   * `com.adobe.idp.Document`オブジェクトの`getInputStream`メソッドを呼び出して、`java.io.InputStream`オブジェクトを作成します。
   * バイト配列を作成し、`InputStream`オブジェクトの`read`メソッドを呼び出して、バイト配列を引数として渡すことで、フォームデータストリームを設定します。
   * `javax.servlet.ServletOutputStream`オブジェクトの`write`メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに送信します。 バイト配列を`write`メソッドに渡します。

**関連トピック**

[クイック開始（SOAPモード）:Java APIを使用したカスタムツールバーによるHTMLフォームのレンダリング](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-with-a-custom-toolbar-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api}を使用したカスタムツールバーを使用したHTMLフォームのレンダリング

FormsサービスAPI（Webサービス）を使用して、カスタムツールバーを含むHTMLフォームをレンダリングします。

1. プロジェクトファイルを含める

   * FormsサービスのWSDLを使用するJavaプロキシクラスを作成します。
   * クラスパスにJavaプロキシクラスを含めます。

1. FormsJava APIオブジェクトの作成

   `FormsService`オブジェクトを作成し、認証値を設定します。

1. カスタムfscmenu XMLファイルの参照

   * コンストラクターを使用して`HTMLRenderSpec`オブジェクトを作成します。
   * ツールバーを含むHTMLフォームをレンダリングするには、`HTMLRenderSpec`オブジェクトの`setHTMLToolbar`メソッドを呼び出し、`HTMLToolbar`列挙値を渡します。 例えば、垂直方向のHTMLツールバーを表示するには、`HTMLToolbar.Vertical`を渡します。
   * `HTMLRenderSpec`オブジェクトの`setToolbarURI`メソッドを呼び出し、XMLファイルのURIの場所を指定する文字列値を渡して、fscmenu XMLファイルの場所を指定します。
   * 該当する場合は、`HTMLRenderSpec`オブジェクトの`setLocale`メソッドを呼び出し、ロケール値を指定する文字列値を渡して、ロケール値を設定します。 デフォルト値は英語です。

   >[!NOTE]
   >
   >このセクションに関連付けられているクイック開始では、この値を&#x200B;`fr_FR`*.*&#x200B;に設定します。

1. HTMLフォームのレンダリング

   `FormsService`オブジェクトの`renderHTMLForm`メソッドを呼び出し、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定するstring値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`など、完全なパスを必ず指定してください。
   * HTML環境設定の種類を指定する`TransformTo`列挙値。 例えば、Internet Explorer 5.0以降用の動的HTMLと互換性のあるHTMLフォームをレンダリングするには、`TransformTo.MSDHTML`を指定します。
   * フォームとマージするデータを含む`BLOB`オブジェクト。 データを結合したくない場合は、`null`を渡します。
   * HTML実行時オプションを格納する`HTMLRenderSpec`オブジェクト。
   * `HTTP_USER_AGENT`ヘッダー値を指定するstring値（`Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322`など）。 この値を設定したくない場合は、空の文字列を渡すことができます。
   * HTMLフォームのレンダリングに必要なURI値を格納する`URLSpec`オブジェクト。
   * 添付ファイルを格納する`java.util.HashMap`オブジェクト。 このパラメーターはオプションです。フォームにファイルを添付しない場合は、`null`を指定できます。
   * `renderHTMLForm`メソッドによって入力される空の`com.adobe.idp.services.holders.BLOBHolder`オブジェクト。 このパラメーター値は、レンダリングされたフォームを保存します。
   * `renderHTMLForm`メソッドによって入力される空の`com.adobe.idp.services.holders.BLOBHolder`オブジェクト。 このパラメーターは、出力XMLデータを格納します。
   * `renderHTMLForm`メソッドによって入力される空の`javax.xml.rpc.holders.LongHolder`オブジェクト。 この引数は、フォームのページ数を格納します。
   * `renderHTMLForm`メソッドによって入力される空の`javax.xml.rpc.holders.StringHolder`オブジェクト。 この引数はロケールの値を格納します。
   * `renderHTMLForm`メソッドによって入力される空の`javax.xml.rpc.holders.StringHolder`オブジェクト。 この引数は、使用されるHTMLレンダリング値を格納します。
   * この操作の結果を含む空の`com.adobe.idp.services.holders.FormsResultHolder`オブジェクトです。

   `renderHTMLForm`メソッドは、最後の引数値として渡される`com.adobe.idp.services.holders.FormsResultHolder`オブジェクトに、クライアントWebブラウザーに書き込む必要のあるフォームデータストリームを入力します。

1. フォームデータストリームをクライアントのWebブラウザーに書き込みます

   * `com.adobe.idp.services.holders.FormsResultHolder`オブジェクトの`value`データメンバの値を取得して、`FormResult`オブジェクトを作成します。
   * `FormsResult`オブジェクトの`getOutputContent`メソッドを呼び出して、フォームデータを含む`BLOB`オブジェクトを作成します。
   * `getContentType`メソッドを呼び出して、`BLOB`オブジェクトのコンテンツタイプを取得します。
   * `javax.servlet.http.HttpServletResponse`オブジェクトのコンテンツタイプを設定するには、`setContentType`メソッドを呼び出し、`BLOB`オブジェクトのコンテンツタイプを渡します。
   * `javax.servlet.http.HttpServletResponse`オブジェクトの`getOutputStream`メソッドを呼び出して、フォームデータストリームをクライアントWebブラウザーに書き込むために使用する`javax.servlet.ServletOutputStream`オブジェクトを作成します。
   * バイト配列を作成し、`BLOB`オブジェクトの`getBinaryData`メソッドを呼び出して値を設定します。 このタスクは、`FormsResult`オブジェクトの内容をバイト配列に割り当てます。
   * `javax.servlet.http.HttpServletResponse`オブジェクトの`write`メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに送信します。 バイト配列を`write`メソッドに渡します。

**関連トピック**

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
