---
title: CustomToolbarsでのHTMLフォームのレンダリング
seo-title: CustomToolbarsでのHTMLフォームのレンダリング
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


# CustomToolbarsでのHTMLフォームのレンダリング {#rendering-html-forms-with-customtoolbars}

## カスタムツールバーを含むHTMLフォームのレンダリング {#rendering-html-forms-with-custom-toolbars}

Formsサービスを使用すると、HTMLフォームでレンダリングされるツールバーをカスタマイズできます。 ツールバーは、初期設定のCSSスタイルを上書きして外観を変更するようカスタマイズしたり、Javaスクリプトを上書きして動的な動作を追加したりすることができます。 ツールバーは、fscmenu.xmlというXMLファイルを使用してカスタマイズします。 デフォルトでは、Formsサービスは内部的に指定されたURIの場所からこのファイルを取得します。

>[!NOTE]
>
>このURIの場所は、adobe-forms-core.jarファイルにあります。このファイルは、adobe-forms-dsc.jarファイル内にあります。 adobe-forms-dsc.jarファイルは、C:\Adobe\Adobe_Experience_Manager_forms\ folder (C:\ is the installation directory)にあります。 Win RARなどのファイル抽出ツールを使用して、アドビを開くことができます。

この場所からfscmenu.xmlをコピーし、必要に応じて変更して、カスタムURIの場所に配置できます。 次に、Forms Service APIを使用して、指定した場所からfscmenu.xmlファイルを使用してFormsサービスを実行するための実行時オプションを設定します。 これらのアクションにより、Formsサービスは、カスタムツールバーを持つHTMLフォームをレンダリングします。

fscmenu.xmlファイルに加えて、次のファイルも取得する必要があります。

* fscmenu.js
* fscattachments.js
* fscmenu.css
* fscmenu-v.css
* fscmenu-ie.css
* fscdialog.css

fscJSは、各ノードに関連付けられているJavaスクリプトです。 ノード用に1つを指定し、オプションで `div#fscmenu` ノード用に1つを指定する必要があり `ul#fscmenuItem` ます。 JSファイルは、コアツールバー機能を実装し、デフォルトファイルが機能します。

fscCSSは、特定のノードに関連付けられたスタイルシートです。 CSSファイル内のスタイルは、ツールバーの外観を指定します。 *fscVCSS* は、レンダリングされたHTMLフォームの左側に表示される、垂直方向のツールバーのスタイルシートです。 *fscIECSS* は、Internet ExplorerでレンダリングされるHTMLフォームに使用されるスタイルシートです。

上記のすべてのファイルがfscmenu.xmlファイルで参照されていることを確認します。 つまり、fscmenu.xmlファイルで、これらのファイルを指すURIの場所を指定します。これにより、Formsサービスでこれらのファイルを見つけることができます。 デフォルトでは、これらのファイルは、内部キーワード `FSWebRoot` またはで始まるURIの場所で使用でき `ApplicationWebRoot`ます。

ツールバーをカスタマイズするには、外部キーワードを使用してキーワードを置き換え `FSToolBarURI`ます。 このキーワードは、実行時にFormsサービスに渡されるURIを表します（この方法をこの節で後述します）。

これらのJSファイルとCSSファイルの絶対位置を指定することもできます(例：https://www.mycompany.com/scripts/misc/fscmenu.js)。 この場合、キー `FSToolBarURI` ワードを使用する必要はありません。

>[!NOTE]
>
>これらのファイルの参照方法を混在させないことをお勧めします。 つまり、すべてのURIは、キーワードまたは絶対位置を使用して参照する必要があり `FSToolBarURI` ます。

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
>太字のテキストは、参照する必要があるCSSおよびJSファイルへのURIを表します。

次の項目では、ツールバーのカスタマイズ方法を説明します。

* （fscmenu.xmlファイル内の） `fscJS`、、、の `fscCSS`属性の値を変更し、参照ファイルのカスタムの場所を反映します。この節で説明する方法のいずれかを使用します(例： `fscVCSS``fscIECSS``fscJS="FSToolBarURI/scripts/fscmenu.js"`)。
* すべてのCSSファイルとJSファイルを指定する必要があります。 どのファイルも変更されない場合は、カスタムの場所にデフォルトのファイルを指定します。 この節で説明する様々なファイルを開いて、デフォルトのファイルを取得できます。
* 任意のファイルに絶対参照(例えば、https://www.example.com/scripts/custom-vertical-fscmenu.css)を指定できます。
* ノードが必要とするJSファイルとCSSファイルは、ツールバー機能にとって `div#fscmenu` 必須です。 個々の `ul#fscmenuItem` ノードには、サポートするJSまたはCSSファイルがある場合とない場合があります。

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

また、 `HTMLRenderSpec` オブジェクトの `setLocale` メソッドを呼び出し、ロケール値を指定する文字列値を渡すことで、有効なロケール値を指定します。 例えば、フランス語 `fr_FR` を指定するにはを渡します。 Formsサービスは、ローカライズされたツールバーにバンドルされています。

>[!NOTE]
>
>カスタムツールバーを使用するHTMLフォームをレンダリングする前に、HTMLフォームのレンダリング方法を知っておく必要があります。 (「フォームをHTMLとして [レンダリングする」を参照](/help/forms/developing/rendering-forms-html.md))。

For more information about the Forms service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary-of-steps}

カスタムツールバーを含むHTMLフォームをレンダリングするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. フォームJava APIオブジェクトを作成します。
1. カスタムfscmenu XMLファイルを参照します。
1. HTMLフォームをレンダリングする。
1. フォームデータストリームをクライアントのWebブラウザーに書き込みます。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを含めます。

**フォームJava APIオブジェクトの作成**

Formsサービスがサポートする操作をプログラムで実行する前に、Formsクライアントオブジェクトを作成する必要があります。

**カスタムfscmenu XMLファイルの参照**

カスタムツールバーを含むHTMLフォームをレンダリングするには、ツールバーを説明するfscmenu XMLファイルを参照します。 （この節では、fscmenu XMLファイルの2つの例を示します）。 また、fscmenu.xmlファイルで、すべての参照ファイルの場所が正しく指定されていることを確認してください。 この節で前述したように、すべてのファイルがキーワードまたは絶対位置で参照されているこ `FSToolBarURI` とを確認します。

**HTMLフォームのレンダリング**

HTMLフォームをレンダリングするには、Designerで作成し、XDPファイルとして保存したフォームデザインを指定します。 HTML変換タイプも選択します。 例えば、Internet Explorer 5.0以降用の動的HTMLをレンダリングするHTML変換タイプを指定できます。

HTMLフォームのレンダリングには、他のフォームタイプをレンダリングするためのURI値などの値も必要です。

**フォームデータストリームをクライアントのWebブラウザーに書き込みます**

Formsサービスは、HTMLフォームをレンダリングするときに、フォームデータストリームを返します。このストリームをユーザーに表示させるには、クライアントWebブラウザーに書き込む必要があります。

**関連トピック**

[Java APIを使用してカスタムツールバーでHTMLフォームをレンダリングする](#render-an-html-form-with-a-custom-toolbar-using-the-java-api)

[WebサービスAPIを使用したカスタムツールバーを使用したHTMLフォームのレンダリング](#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[FormsサービスAPIのクイック開始](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[インタラクティブPDF formsのレンダリング](/help/forms/developing/rendering-interactive-pdf-forms.md)

[HTML形式でのフォームのレンダリング](/help/forms/developing/rendering-forms-html.md)

[フォームをレンダリングするWeb アプリケーションの作成](/help/forms/developing/creating-web-applications-renders-forms.md)

### Java APIを使用してカスタムツールバーでHTMLフォームをレンダリングする {#render-an-html-form-with-a-custom-toolbar-using-the-java-api}

Forms Service API(Java)を使用して、カスタムツールバーを含むHTMLフォームをレンダリングします。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-forms-client.jarなどのクライアントJARファイルを含めます。

1. フォームJava APIオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `FormsServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. カスタムfscmenu XMLファイルの参照

   * Create an `HTMLRenderSpec` object by using its constructor.
   * ツールバーを含むHTMLフォームをレンダリングするには、 `HTMLRenderSpec` オブジェクトの `setHTMLToolbar``HTMLToolbar` メソッドを呼び出し、列挙値を渡します。 例えば、垂直方向のHTMLツールバーを表示するには、を渡し `HTMLToolbar.Vertical`ます。
   * オブジェクトのメソッドを呼び出し、XMLファイルのURIの場所を指定するstring値を渡して、fscmenu XMLファイルの場所を指定し `HTMLRenderSpec``setToolbarURI` ます。
   * 該当する場合は、 `HTMLRenderSpec` オブジェクトの `setLocale` メソッドを呼び出し、ロケール値を指定する文字列値を渡して、ロケール値を設定します。 デフォルト値は英語です。

   >[!NOTE]
   >
   >このセクションに関連付けられているクイック開始では、この値がに設定され `fr_FR`*ます。*

1. HTMLフォームのレンダリング

   オブジェクトの `FormsServiceClient``renderHTMLForm` メソッドを呼び出し、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定するstring値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、完全なパス（など）を必ず指定してください `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * HTML環境設定タイプを指定する `TransformTo` enum値。 例えば、Internet Explorer 5.0以降用の動的HTMLと互換性のあるHTMLフォームをレンダリングするには、を指定し `TransformTo.MSDHTML`ます。
   * フォームとマージするデータを含む `com.adobe.idp.Document` オブジェクト。 データをマージしない場合は、空の `com.adobe.idp.Document` オブジェクトを渡します。
   * HTML実行時オプションを格納する `HTMLRenderSpec` オブジェクトです。
   * ヘッダー値を指定するstring値（例：） `HTTP_USER_AGENT``Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。
   * HTMLフォームのレンダリングに必要なURI値を格納する `URLSpec` オブジェクト。
   * 添付ファイルを格納する `java.util.HashMap` オブジェクトです。 これはオプションのパラメーターで、フォームにファイルを添付しない `null` かどうかを指定できます。

   この `renderHTMLForm``FormsResult` メソッドは、クライアントのWebブラウザーに書き込む必要があるフォームデータストリームを含むオブジェクトを返します。

1. フォームデータストリームをクライアントのWebブラウザーに書き込みます

   * オブジェクトの `com.adobe.idp.Document` メソッドを呼び出して、 `FormsResult` オブジェクトを作成し `getOutputContent` ます。
   * メソッドを呼び出して、 `com.adobe.idp.Document` オブジェクトのコンテンツタイプを取得し `getContentType` ます。
   * メソッドを呼び出し、オブジェクトの `javax.servlet.http.HttpServletResponse` コンテンツタイプを渡すことで、 `setContentType``com.adobe.idp.Document` オブジェクトのコンテンツタイプを設定します。
   * オブジェクトの `javax.servlet.ServletOutputStream` メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに書き込むために使用する `javax.servlet.http.HttpServletResponse``getOutputStream` オブジェクトを作成します。
   * オブジェクトの `java.io.InputStream` メソッドを呼び出して、 `com.adobe.idp.Document` オブジェクトを作成 `getInputStream` します。
   * バイト配列を作成し、 `InputStream` オブジェクトの `read` メソッドを呼び出して、バイト配列を引数として渡すことで、フォームデータストリームを設定します。
   * オブジェクトの `javax.servlet.ServletOutputStream``write` メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに送信します。 バイト配列を `write` メソッドに渡します。

**関連トピック**

[クイック開始（SOAPモード）: Java APIを使用したカスタムツールバーによるHTMLフォームのレンダリング](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-with-a-custom-toolbar-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したカスタムツールバーを使用したHTMLフォームのレンダリング {#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api}

Forms Service API（Webサービス）を使用して、カスタムツールバーを含むHTMLフォームをレンダリングします。

1. プロジェクトファイルを含める

   * FormsサービスのWSDLを使用するJavaプロキシクラスを作成します。
   * クラスパスにJavaプロキシクラスを含めます。

1. フォームJava APIオブジェクトの作成

   オブジェクトを作成し、認証値を設定し `FormsService` ます。

1. カスタムfscmenu XMLファイルの参照

   * Create an `HTMLRenderSpec` object by using its constructor.
   * ツールバーを含むHTMLフォームをレンダリングするには、 `HTMLRenderSpec` オブジェクトの `setHTMLToolbar``HTMLToolbar` メソッドを呼び出し、列挙値を渡します。 例えば、垂直方向のHTMLツールバーを表示するには、を渡し `HTMLToolbar.Vertical`ます。
   * オブジェクトのメソッドを呼び出し、XMLファイルのURIの場所を指定するstring値を渡して、fscmenu XMLファイルの場所を指定し `HTMLRenderSpec``setToolbarURI` ます。
   * 該当する場合は、 `HTMLRenderSpec` オブジェクトの `setLocale` メソッドを呼び出し、ロケール値を指定する文字列値を渡して、ロケール値を設定します。 デフォルト値は英語です。

   >[!NOTE]
   >
   >このセクションに関連付けられているクイック開始では、この値がに設定され `fr_FR`*ます。*

1. HTMLフォームのレンダリング

   オブジェクトの `FormsService``renderHTMLForm` メソッドを呼び出し、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定するstring値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、完全なパス（など）を必ず指定してください `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * HTML環境設定タイプを指定する `TransformTo` enum値。 例えば、Internet Explorer 5.0以降用の動的HTMLと互換性のあるHTMLフォームをレンダリングするには、を指定し `TransformTo.MSDHTML`ます。
   * フォームとマージするデータを含む `BLOB` オブジェクト。 データを結合したくない場合は、を渡し `null`ます。
   * HTML実行時オプションを格納する `HTMLRenderSpec` オブジェクトです。
   * ヘッダー値(例： `HTTP_USER_AGENT` )を指定するstring値 `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322`。 この値を設定したくない場合は、空の文字列を渡すことができます。
   * HTMLフォームのレンダリングに必要なURI値を格納する `URLSpec` オブジェクト。
   * 添付ファイルを格納する `java.util.HashMap` オブジェクトです。 このパラメーターはオプションです。フォームにファイルを添付しない `null` かどうかを指定できます。
   * メソッドによって入力される空の `com.adobe.idp.services.holders.BLOBHolder` オブジェクト `renderHTMLForm` です。 このパラメーター値は、レンダリングされたフォームを保存します。
   * メソッドによって入力される空の `com.adobe.idp.services.holders.BLOBHolder` オブジェクト `renderHTMLForm` です。 このパラメーターは、出力XMLデータを格納します。
   * メソッドによって入力される空の `javax.xml.rpc.holders.LongHolder` オブジェクト `renderHTMLForm` です。 この引数は、フォームのページ数を格納します。
   * メソッドによって入力される空の `javax.xml.rpc.holders.StringHolder` オブジェクト `renderHTMLForm` です。 この引数はロケールの値を格納します。
   * メソッドによって入力される空の `javax.xml.rpc.holders.StringHolder` オブジェクト `renderHTMLForm` です。 この引数は、使用されるHTMLレンダリング値を格納します。
   * この操作の結果を含む空の `com.adobe.idp.services.holders.FormsResultHolder` オブジェクトです。

   この `renderHTMLForm` メソッドは、最後の引数値として渡される `com.adobe.idp.services.holders.FormsResultHolder` オブジェクトに、クライアントWebブラウザーに書き込む必要があるフォームデータストリームを入力します。

1. フォームデータストリームをクライアントのWebブラウザーに書き込みます

   * オブジェクトの `FormResult` データメンバーの値を取得して `com.adobe.idp.services.holders.FormsResultHolder` オブジェクトを作成し `value` ます。
   * オブジェクトの `BLOB` メソッドを呼び出して、フォームデータを含む `FormsResult` オブジェクトを作成し `getOutputContent` ます。
   * メソッドを呼び出して、 `BLOB` オブジェクトのコンテンツタイプを取得し `getContentType` ます。
   * メソッドを呼び出し、オブジェクトの `javax.servlet.http.HttpServletResponse` コンテンツタイプを渡すことで、 `setContentType``BLOB` オブジェクトのコンテンツタイプを設定します。
   * オブジェクトの `javax.servlet.ServletOutputStream` メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに書き込むために使用する `javax.servlet.http.HttpServletResponse``getOutputStream` オブジェクトを作成します。
   * バイト配列を作成し、 `BLOB` オブジェクトの `getBinaryData` メソッドを呼び出して値を設定します。 このタスクは、 `FormsResult` オブジェクトの内容をバイト配列に割り当てます。
   * オブジェクトの `javax.servlet.http.HttpServletResponse``write` メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに送信します。 バイト配列を `write` メソッドに渡します。

**関連トピック**

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
