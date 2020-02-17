---
title: カスタムツールバーを使用したHTMLフォームのレンダリング
seo-title: カスタムツールバーを使用したHTMLフォームのレンダリング
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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# カスタムツールバーを使用したHTMLフォームのレンダリング {#rendering-html-forms-with-customtoolbars}

## カスタムツールバーを使用したHTMLフォームのレンダリング {#rendering-html-forms-with-custom-toolbars}

Formsサービスを使用すると、HTMLフォームでレンダリングされるツールバーをカスタマイズできます。 ツールバーは、初期設定のCSSスタイルを上書きして外観を変更したり、Javaスクリプトを上書きして動的な動作を追加したりすることで、カスタマイズ可能です。 ツールバーは、fscmenu.xmlというXMLファイルを使用してカスタマイズします。 デフォルトでは、Formsサービスは内部的に指定されたURIの場所からこのファイルを取得します。

>[!NOTE]
>
>このURIの場所は、adobe-forms-core.jarファイル内にあります。このファイルは、adobe-forms-dsc.jarファイル内にあります。 adobe-forms-dsc.jarファイルは、C:\Adobe\Adobe_Experience_Manager_forms\ folder (C:\ is the installation directory)にあります。 Win RARなどのファイル抽出ツールを使用して、アドビを開くことができます。

この場所からfscmenu.xmlをコピーし、必要に応じて変更して、カスタムURIの場所に配置できます。 次に、Forms Service APIを使用して、指定した場所にあるfscmenu.xmlファイルを使用してFormsサービスを実行する実行時オプションを設定します。 これらのアクションにより、Formsサービスは、カスタムツールバーを持つHTMLフォームをレンダリングします。

fscmenu.xmlファイルに加えて、次のファイルも取得する必要があります。

* fscmenu.js
* fscattachments.js
* fscmenu.css
* fscmenu-v.css
* fscmenu-ie.css
* fscdialog.css

fscJSは、各ノードに関連付けられているJavaスクリプトです。 ノード用に1つを指定し、必要に応じてノ `div#fscmenu` ード用にも指定する必要があ `ul#fscmenuItem` ります。 JSファイルには、コアツールバー機能が実装され、デフォルトファイルが機能します。

fscCSSは、特定のノードに関連付けられたスタイルシートです。 CSSファイル内のスタイルは、ツールバーの外観を指定します。 *fscVCSSは* 、レンダリングされたHTMLフォームの左側に表示される、垂直方向のツールバーのスタイルシートです。 *fscIECSSは* 、Internet ExplorerでレンダリングされるHTMLフォームに使用されるスタイルシートです。

上記のすべてのファイルがfscmenu.xmlファイルで参照されていることを確認します。 つまり、fscmenu.xmlファイルで、Formsサービスがファイルを見つけられるように、これらのファイルを指すURIの場所を指定します。 デフォルトでは、これらのファイルは、内部キーワードまたはで始まるURIの場所で使用 `FSWebRoot` できま `ApplicationWebRoot`す。

ツールバーをカスタマイズするには、外部キーワードを使用してキーワードを置き換えま `FSToolBarURI`す。 このキーワードは、実行時にFormsサービスに渡されるURIを表します（この方法については、この節で後述します）。

また、これらのJSファイルとCSSファイルの絶対位置を指定することもできます(例：https://www.mycompany.com/scripts/misc/fscmenu.js)。 この場合、キーワードを使用する必要はありま `FSToolBarURI` せん。

>[!NOTE]
>
>これらのファイルの参照方法を混在させないことをお勧めします。 つまり、すべてのURIは、キーワードまたは絶対位置を使用して `FSToolBarURI` 参照する必要があります。

JSファイルとCSSファイルを取得するには、adobe-forms-&lt;appserver>.earファイルを開きます。 このファイル内で、adobe-forms-res.warを開きます。 これらのファイルはすべてWARファイル内にあります。 adobe-forms-&lt;appserver>.earファイルは、AEM formsのインストールフォルダー(C:\ is the installation directory)にあります。 WinRARなどのファイル抽出ツールを使用して、adobe-forms-&lt;appserver>.earを開くことができます。

次のXML構文は、fscmenu.xmlファイルの例を示しています。

```as3
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
>太字のテキストは、参照する必要があるCSSファイルとJSファイルのURIを表します。

次の項目では、ツールバーのカスタマイズ方法を説明します。

* （fscmenu.xmlファイル内の） `fscJS`、、 `fscCSS`、 `fscVCSS``fscIECSS` 、の属性の値を変更して、参照ファイルのカスタムの場所を反映します。そのためには、この節で説明する方法のいずれかを使用します(例 `fscJS="FSToolBarURI/scripts/fscmenu.js"`)。
* すべてのCSSファイルとJSファイルを指定する必要があります。 ファイルが変更されない場合は、カスタムの場所にデフォルトのファイルを指定します。 この節で説明する様々なファイルを開いて、デフォルトのファイルを取得できます。
* 任意のファイルに対して絶対参照(例えば、https://www.example.com/scripts/custom-vertical-fscmenu.css)を指定できます。
* ノードで必要なJSファイルとCSSファイルは、ツ `div#fscmenu` ールバー機能に不可欠です。 個々のノ `ul#fscmenuItem` ードには、サポートするJSまたはCSSファイルが含まれている場合と含まれない場合があります。

**ローカル値の変更**

ツールバーのカスタマイズの一環として、ツールバーのロケール値を変更できます。 つまり、別の言語で表示できます。 次の図に、フランス語で表示されるカスタムツールバーを示します。

>[!NOTE]
>
>複数の言語でカスタムツールバーを作成することはできません。 ツールバーは、ロケールの設定に基づいて異なるXMLファイルを使用できません。

ツールバーのロケール値を変更するには、fscmenu.xmlファイルに表示する言語が含まれていることを確認します。 次のXML構文は、フランス語のツールバーの表示に使用するfscmenu.xmlファイルを示しています。

```as3
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
>この節に関連付けられているクイックスタートでは、このXMLファイルを使用して、前の図に示すようにフランス語のカスタムツールバーを表示します。

また、オブジェクトのメソッドを呼び出し、ロケ `HTMLRenderSpec` ール値を指 `setLocale` 定する文字列値を渡して、有効なロケール値を指定します。 例えば、フランス語を `fr_FR` 指定するにはを渡します。 Formsサービスは、ローカライズされたツールバーにバンドルされています。

>[!NOTE]
>
>カスタムツールバーを使用するHTMLフォームをレンダリングする前に、HTMLフォームのレンダリング方法を理解しておく必要があります。 (「フォーム [のHTMLとしてのレンダリング](/help/forms/developing/rendering-forms-html.md)」を参照)。

For more information about the Forms service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary-of-steps}

カスタムツールバーを含むHTMLフォームをレンダリングするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Forms Java APIオブジェクトを作成します。
1. カスタムfscmenu XMLファイルを参照します。
1. HTMLフォームをレンダリングします。
1. クライアントのWebブラウザーにフォームデータストリームを書き込みます。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを含めます。

**フォームJava APIオブジェクトの作成**

Formsサービスがサポートする操作をプログラムで実行する前に、Formsクライアントオブジェクトを作成する必要があります。

**カスタムfscmenu XMLファイルの参照**

カスタムツールバーを含むHTMLフォームをレンダリングするには、ツールバーを説明するfscmenu XMLファイルを参照します。 （この節では、fscmenu XMLファイルの2つの例を示します）。また、fscmenu.xmlファイルで、すべての参照ファイルの場所が正しく指定されていることを確認してください。 この節で前述したように、すべてのファイルがキーワードまたはその絶対位置で参照さ `FSToolBarURI` れていることを確認します。

**HTMLフォームのレンダリング**

HTMLフォームをレンダリングするには、Designerで作成され、XDPファイルとして保存されたフォームデザインを指定します。 HTML変換タイプも選択します。 例えば、Internet Explorer 5.0以降用の動的HTMLをレンダリングするHTML変換タイプを指定できます。

HTMLフォームのレンダリングには、他のフォームタイプのレンダリング用のURI値などの値も必要です。

**クライアントのWebブラウザーにフォームデータストリームを書き込みます**

Formsサービスは、HTMLフォームをレンダリングするときに、フォームデータストリームを返します。このストリームをクライアントのWebブラウザーに書き込み、HTMLフォームをユーザーに表示させる必要があります。

**関連トピック**

[Java APIを使用してカスタムツールバーでHTMLフォームをレンダリングする](#render-an-html-form-with-a-custom-toolbar-using-the-java-api)

[WebサービスAPIを使用したカスタムツールバーによるHTMLフォームのレンダリング](#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[FormsサービスAPIのクイックスタート](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[インタラクティブPDFフォームのレンダリング](/help/forms/developing/rendering-interactive-pdf-forms.md)

[HTMLとしてのフォームのレンダリング](/help/forms/developing/rendering-forms-html.md)

[フォームをレンダリングするWebアプリケーションの作成](/help/forms/developing/creating-web-applications-renders-forms.md)

### Java APIを使用してカスタムツールバーでHTMLフォームをレンダリングする {#render-an-html-form-with-a-custom-toolbar-using-the-java-api}

Forms Service API(Java)を使用して、カスタムツールバーを含むHTMLフォームをレンダリングします。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-forms-client.jarなどのクライアントJARファイルを含めます。

1. フォームJava APIオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `FormsServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. カスタムfscmenu XMLファイルの参照

   * Create an `HTMLRenderSpec` object by using its constructor.
   * ツールバーを使用してHTMLフォームをレンダリングするには、オブ `HTMLRenderSpec` ジェクトのメソッドを `setHTMLToolbar` 呼び出し、列挙値を渡 `HTMLToolbar` します。 例えば、垂直方向のHTMLツールバーを表示するには、を渡しま `HTMLToolbar.Vertical`す。
   * オブジェクトのメソッドを呼び出し、XMLファイルのURI `HTMLRenderSpec` の場所を指 `setToolbarURI` 定するstring値を渡して、fscmenu XMLファイルの場所を指定します。
   * 該当する場合は、オブジェクトのメソッドを呼び出し、ロケ `HTMLRenderSpec` ール値を指 `setLocale` 定する文字列値を渡して、ロケール値を設定します。 デフォルト値は英語です。
   >[!NOTE]
   >
   >このセクションに関連付けられているクイックスタートでは、この値をに設定しま `fr_FR`*す。*

1. HTMLフォームのレンダリング

   オブジェクト `FormsServiceClient` のメソッドを `renderHTMLForm` 呼び出し、次の値を渡します。

   * ファイル名の拡張子を含むフォームデザイン名を指定するstring値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、必ずなどの完全なパスを指定してくださ `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`い。
   * HTMLプ `TransformTo` リファレンスタイプを指定するenum値。 例えば、Internet Explorer 5.0以降用の動的HTMLと互換性のあるHTMLフォームをレンダリングするには、を指定します `TransformTo.MSDHTML`。
   * フォーム `com.adobe.idp.Document` とマージするデータを含むオブジェクトです。 データをマージしない場合は、空のオブジェクトを渡し `com.adobe.idp.Document` ます。
   * HTML実行 `HTMLRenderSpec` 時オプションを格納するオブジェクトです。
   * ヘッダー値を指定す `HTTP_USER_AGENT` るstring値(例： `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`)。
   * HTMLフォ `URLSpec` ームのレンダリングに必要なURI値を格納するオブジェクトです。
   * 添付フ `java.util.HashMap` ァイルを格納するオブジェクト。 これはオプションのパラメーターで、フォームにフ `null` ァイルを添付しないかどうかを指定できます。
   このメソ `renderHTMLForm` ッドは、クライア `FormsResult` ントのWebブラウザーに書き込む必要があるフォームデータストリームを含むオブジェクトを返します。

1. クライアントのWebブラウザーにフォームデータストリームを書き込みます

   * オブジェクトの `com.adobe.idp.Document` メソッドを呼び出して、オ `FormsResult` ブジェクトを作成 `getOutputContent` します。
   * メソッドを呼び出して、オブジェ `com.adobe.idp.Document` クトのコンテンツタイプを取得 `getContentType` します。
   * メソッドを呼 `javax.servlet.http.HttpServletResponse` び出し、オブジェクトのコンテンツタ `setContentType` イプを渡すことで、オブジェクトのコンテンツタイプを設定 `com.adobe.idp.Document` します。
   * オブジェクト `javax.servlet.ServletOutputStream` のメソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに書き込むために使用するオ `javax.servlet.http.HttpServletResponse` ブジェクトを作成 `getOutputStream` します。
   * オブジェクト `java.io.InputStream` のメソッドを呼び出して、オ `com.adobe.idp.Document` ブジェクトを作成 `getInputStream` します。
   * バイト配列を作成し、オブジェクトのメソッドを呼び出し、バイト配列を引数 `InputStream` として渡すこ `read` とで、フォームデータストリームを設定します。
   * オブジェクト `javax.servlet.ServletOutputStream` のメソッドを呼び `write` 出して、フォームデータストリームをクライアントWebブラウザーに送信します。 バイト配列をメソッドに渡し `write` ます。

**関連トピック**

[クイックスタート（SOAPモード）:Java APIを使用したカスタムツールバーによるHTMLフォームのレンダリング](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-with-a-custom-toolbar-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したカスタムツールバーによるHTMLフォームのレンダリング {#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api}

Forms Service API（Webサービス）を使用して、カスタムツールバーを含むHTMLフォームをレンダリングします。

1. プロジェクトファイルを含める

   * FormsサービスWSDLを使用するJavaプロキシクラスを作成します。
   * クラスパスにJavaプロキシクラスを含めます。

1. フォームJava APIオブジェクトの作成

   オブジェクト `FormsService` を作成し、認証値を設定します。

1. カスタムfscmenu XMLファイルの参照

   * Create an `HTMLRenderSpec` object by using its constructor.
   * ツールバーを使用してHTMLフォームをレンダリングするには、オブ `HTMLRenderSpec` ジェクトのメソッドを `setHTMLToolbar` 呼び出し、列挙値を渡 `HTMLToolbar` します。 例えば、垂直方向のHTMLツールバーを表示するには、を渡しま `HTMLToolbar.Vertical`す。
   * オブジェクトのメソッドを呼び出し、XMLファイルのURI `HTMLRenderSpec` の場所を指 `setToolbarURI` 定するstring値を渡して、fscmenu XMLファイルの場所を指定します。
   * 該当する場合は、オブジェクトのメソッドを呼び出し、ロケ `HTMLRenderSpec` ール値を指 `setLocale` 定する文字列値を渡して、ロケール値を設定します。 デフォルト値は英語です。
   >[!NOTE]
   >
   >このセクションに関連付けられているクイックスタートでは、この値をに設定しま `fr_FR`*す。*

1. HTMLフォームのレンダリング

   オブジェクト `FormsService` のメソッドを `renderHTMLForm` 呼び出し、次の値を渡します。

   * ファイル名の拡張子を含むフォームデザイン名を指定するstring値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、必ずなどの完全なパスを指定してくださ `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`い。
   * HTMLプ `TransformTo` リファレンスタイプを指定するenum値。 例えば、Internet Explorer 5.0以降用の動的HTMLと互換性のあるHTMLフォームをレンダリングするには、を指定します `TransformTo.MSDHTML`。
   * フォーム `BLOB` とマージするデータを含むオブジェクトです。 データを結合しない場合は、を渡します `null`。
   * HTML実行 `HTMLRenderSpec` 時オプションを格納するオブジェクトです。
   * ヘッダー値( `HTTP_USER_AGENT` など)を指定するstring `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322`値。 この値を設定しない場合は、空の文字列を渡すことができます。
   * HTMLフォ `URLSpec` ームのレンダリングに必要なURI値を格納するオブジェクトです。
   * 添付フ `java.util.HashMap` ァイルを格納するオブジェクト。 このパラメーターはオプションで、フォームにフ `null` ァイルを添付しないかどうかを指定できます。
   * メソッドに `com.adobe.idp.services.holders.BLOBHolder` よって入力される空のオブジェ `renderHTMLForm` クト。 このパラメーター値は、レンダリングされたフォームを保存します。
   * メソッドに `com.adobe.idp.services.holders.BLOBHolder` よって入力される空のオブジェ `renderHTMLForm` クト。 このパラメーターは、出力XMLデータを格納します。
   * メソッドに `javax.xml.rpc.holders.LongHolder` よって入力される空のオブジェ `renderHTMLForm` クト。 この引数は、フォーム内のページ数を格納します。
   * メソッドに `javax.xml.rpc.holders.StringHolder` よって入力される空のオブジェ `renderHTMLForm` クト。 この引数はロケールの値を格納します。
   * メソッドに `javax.xml.rpc.holders.StringHolder` よって入力される空のオブジェ `renderHTMLForm` クト。 この引数は、使用されるHTMLレンダリング値を格納します。
   * この操作 `com.adobe.idp.services.holders.FormsResultHolder` の結果を含む空のオブジェクトです。
   メソッド `renderHTMLForm` は、最後の引 `com.adobe.idp.services.holders.FormsResultHolder` 数値として渡されたオブジェクトに、クライアントWebブラウザーに書き込む必要があるフォームデータストリームを入力します。

1. クライアントのWebブラウザーにフォームデータストリームを書き込みます

   * オブジェクト `FormResult` のデータメンバーの値を取得して、オ `com.adobe.idp.services.holders.FormsResultHolder` ブジェクトを `value` 作成します。
   * オブジェクトの `BLOB` メソッドを呼び出して、フォームデータを含むオ `FormsResult` ブジェクトを作成 `getOutputContent` します。
   * メソッドを呼び出して、オブジェ `BLOB` クトのコンテンツタイプを取得 `getContentType` します。
   * メソッドを呼 `javax.servlet.http.HttpServletResponse` び出し、オブジェクトのコンテンツタ `setContentType` イプを渡すことで、オブジェクトのコンテンツタイプを設定 `BLOB` します。
   * オブジェクト `javax.servlet.ServletOutputStream` のメソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに書き込むために使用するオ `javax.servlet.http.HttpServletResponse` ブジェクトを作成 `getOutputStream` します。
   * バイト配列を作成し、オブジェクトのメソッドを呼び出 `BLOB` して値を設定 `getBinaryData` します。 このタスクは、オブジェクトの内容をバ `FormsResult` イト配列に割り当てます。
   * オブジェクト `javax.servlet.http.HttpServletResponse` のメソッドを呼び `write` 出して、フォームデータストリームをクライアントWebブラウザーに送信します。 バイト配列をメソッドに渡し `write` ます。

**関連トピック**

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
