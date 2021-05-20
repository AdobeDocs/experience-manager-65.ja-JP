---
title: カスタムツールバーを使用したHTML Formsのレンダリング
seo-title: カスタムツールバーを使用したHTML Formsのレンダリング
description: Formsサービスを使用して、HTMLフォームでレンダリングされるツールバーをカスタマイズします。 Java APIとWebサービスAPIを使用して、カスタムツールバーでHTMLフォームをレンダリングできます。
seo-description: Formsサービスを使用して、HTMLフォームでレンダリングされるツールバーをカスタマイズします。 Java APIとWebサービスAPIを使用して、カスタムツールバーでHTMLフォームをレンダリングできます。
uuid: b9c9464e-ff19-4051-a39b-4ec71c512d10
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 7eb0e8a8-d76a-43f7-a012-c21157b14cd4
role: Developer
exl-id: 0b992b1c-3878-447a-bccc-7034aa3e98bc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2384'
ht-degree: 1%

---

# カスタムツールバーを使用したHTML Formsのレンダリング{#rendering-html-forms-with-customtoolbars}

**このドキュメントのサンプルと例は、JEE上のAEM Forms環境に限られています。**

## カスタムツールバーを使用したHTML Formsのレンダリング{#rendering-html-forms-with-custom-toolbars}

Formsサービスを使用すると、HTMLフォームでレンダリングされるツールバーをカスタマイズできます。 デフォルトのCSSスタイルを上書きすることでツールバーの外観を変更したり、Javaスクリプトを上書きして動的な動作を追加したりするように、ツールバーをカスタマイズできます。 ツールバーは、 fscmenu.xmlという名前のXMLファイルを使用してカスタマイズされます。 デフォルトでは、Formsサービスは内部で指定されたURIの場所からこのファイルを取得します。

>[!NOTE]
>
>このURIの場所は、adobe-forms-core.jarファイル（ adobe-forms-dsc.jarファイル）にあります。 adobe-forms-dsc.jarファイルは、C:\Adobe\Adobe_Experience_Manager_forms\ folder (C:\ is the installation directory)にあります。 Win RARなどのファイル抽出ツールを使用して、アドビを開くことができます。

この場所からfscmenu.xmlをコピーし、必要に応じて変更して、カスタムURIの場所に配置できます。 次に、FormsサービスAPIを使用して、指定した場所のfscmenu.xmlファイルを使用してFormsサービスを実行する実行時オプションを設定します。 これらのアクションにより、Formsサービスは、カスタムツールバーを含むHTMLフォームをレンダリングします。

fscmenu.xmlファイルに加えて、次のファイルも取得する必要があります。

* fscmenu.js
* fscattachments.js
* fscmenu.css
* fscmenu-v.css
* fscmenu-ie.css
* fscdialog.css

fscJSは、各ノードに関連付けられているJavaスクリプトです。 `div#fscmenu`ノード用と`ul#fscmenuItem`ノード用にそれぞれ1つを指定する必要があります。 JSファイルは、コアツールバー機能を実装し、デフォルトファイルが機能します。

fscCSSは、特定のノードに関連付けられているスタイルシートです。 CSSファイル内のスタイルによって、ツールバーの外観が指定されます。 ** fscVCSSは、レンダリングされたHTMLフォームの左側に表示される、垂直方向のツールバー用のスタイルシートです。** fscIECSSは、Internet ExplorerでレンダリングされるHTMLフォームに使用されるスタイルシートです。

上記のすべてのファイルがfscmenu.xmlファイルで参照されていることを確認します。 つまり、 fscmenu.xmlファイルで、これらのファイルを指すURIの場所を指定して、Formsサービスがそれらのファイルを見つけられるようにします。 デフォルトでは、これらのファイルは、内部キーワード`FSWebRoot`または`ApplicationWebRoot`で始まるURIの場所で使用できます。

ツールバーをカスタマイズするには、外部キーワード`FSToolBarURI`を使用してキーワードを置き換えます。 このキーワードは、実行時にFormsサービスに渡されるURIを表します（このアプローチについては、この節で後述します）。

また、これらのJSファイルとCSSファイルの絶対的な場所(例： https://www.mycompany.com/scripts/misc/fscmenu.js )を指定することもできます。 この場合、`FSToolBarURI`キーワードを使用する必要はありません。

>[!NOTE]
>
>これらのファイルの参照方法を混在させることはお勧めしません。 つまり、すべてのURIは`FSToolBarURI`キーワードまたは絶対位置を使用して参照する必要があります。

JSファイルとCSSファイルは、 adobe-forms-&lt;appserver>.earファイルを開いて取得できます。 このファイル内で、 adobe-forms-res.warを開きます。 これらのファイルはすべてWARファイルに格納されています。 adobe-forms-&lt;appserver>.earファイルは、AEM formsのインストールフォルダー(C:\ is the installation directory)にあります。 WinRARなどのファイル抽出ツールを使用して、 adobe-forms-&lt;appserver>.earを開くことができます。

次のXML構文は、 fscmenu.xmlファイルの例を示しています。

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

次の項目では、ツールバーをカスタマイズする方法を説明します。

* `fscJS`、`fscCSS`、`fscVCSS`、`fscIECSS`の各属性の値を（fscmenu.xmlファイル内で）変更し、この節で説明する方法（例えば`fscJS="FSToolBarURI/scripts/fscmenu.js"`）の1つを使用して、参照ファイルのカスタムの場所を反映します。
* すべてのCSSファイルとJSファイルを指定する必要があります。 どのファイルも変更されない場合は、カスタムの場所にデフォルトのファイルを指定します。 この節で説明するように、様々なファイルを開くことで、デフォルトのファイルを取得できます。
* 任意のファイルに絶対参照(例えば、https://www.example.com/scripts/custom-vertical-fscmenu.css)を指定することはできます。
* `div#fscmenu`ノードで必要となるJSファイルとCSSファイルは、ツールバー機能に不可欠です。 個々の`ul#fscmenuItem`ノードには、サポートするJSまたはCSSファイルが含まれている場合と含まれない場合があります。

**ローカル値の変更**

ツールバーのカスタマイズの一環として、ツールバーのロケール値を変更できます。 つまり、別の言語で表示できます。 次の図は、フランス語で表示されるカスタムツールバーを示しています。

>[!NOTE]
>
>複数の言語でカスタムツールバーを作成することはできません。 ツールバーは、ロケール設定に基づいて異なるXMLファイルを使用できません。

ツールバーのロケール値を変更するには、表示する言語がfscmenu.xmlファイルに含まれていることを確認します。 次のXML構文は、フランス語のツールバーを表示するために使用されるfscmenu.xmlファイルを示しています。

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
>このセクションに関連付けられているクイックスタートは、前の図に示すように、このXMLファイルを使用してフランス語のカスタムツールバーを表示します。

また、`HTMLRenderSpec`オブジェクトの`setLocale`メソッドを呼び出し、ロケール値を指定する文字列値を渡すことで、有効なロケール値を指定します。 例えば、`fr_FR`を渡してフランス語を指定します。 Formsサービスは、ローカライズされたツールバーにバンドルされています。

>[!NOTE]
>
>カスタムツールバーを使用するHTMLフォームをレンダリングする前に、HTMLフォームのレンダリング方法を理解しておく必要があります。 ([FormsをHTMLとしてレンダリングする](/help/forms/developing/rendering-forms-html.md)を参照)。

Formsサービスについて詳しくは、『 AEM Formsのサービスリファレンス[ 』を参照してください。](https://www.adobe.com/go/learn_aemforms_services_63)

### 手順の概要{#summary-of-steps}

カスタムツールバーを含むHTMLフォームをレンダリングするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Forms Java APIオブジェクトを作成します。
1. カスタムfscmenu XMLファイルを参照します。
1. HTMLフォームをレンダリングします。
1. フォームデータストリームをクライアントWebブラウザーに書き込みます。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを含めます。

**Forms Java APIオブジェクトの作成**

Formsサービスがサポートする操作をプログラムで実行する前に、Formsクライアントオブジェクトを作成する必要があります。

**カスタムfscmenu XMLファイルの参照**

カスタムツールバーを含むHTMLフォームをレンダリングするには、ツールバーを記述するfscmenu XMLファイルを参照します。 （この節では、fscmenu XMLファイルの2つの例を示します）。 また、 fscmenu.xmlファイルで、すべての参照ファイルの場所が正しく指定されていることを確認してください。 この節で前述したように、すべてのファイルが`FSToolBarURI`キーワードまたは絶対位置で参照されていることを確認します。

**HTMLフォームのレンダリング**

HTMLフォームをレンダリングするには、Designerで作成されXDPファイルとして保存されたフォームデザインを指定します。 また、HTML変換タイプを選択します。 例えば、Internet Explorer 5.0以降用の動的HTMLをレンダリングするHTML変換タイプを指定できます。

HTMLフォームのレンダリングには、他のフォームタイプをレンダリングするためのURI値などの値も必要です。

**フォームデータストリームをクライアントWebブラウザーに書き込む**

Formsサービスは、HTMLフォームをレンダリングする際に、フォームデータストリームを返します。このストリームをクライアントWebブラウザーに書き込んで、HTMLフォームをユーザーに表示させる必要があります。

**関連トピック**

[Java APIを使用したカスタムツールバーでのHTMLフォームのレンダリング](#render-an-html-form-with-a-custom-toolbar-using-the-java-api)

[WebサービスAPIを使用したカスタムツールバーでのHTMLフォームのレンダリング](#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[FormsサービスAPIのクイックスタート](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[インタラクティブPDF formsのレンダリング](/help/forms/developing/rendering-interactive-pdf-forms.md)

[FormsをHTMLとしてレンダリング](/help/forms/developing/rendering-forms-html.md)

[Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Java API {#render-an-html-form-with-a-custom-toolbar-using-the-java-api}を使用して、カスタムツールバーでHTMLフォームをレンダリングする

FormsサービスAPI(Java)を使用して、カスタムツールバーを含むHTMLフォームをレンダリングします。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-forms-client.jarなどのクライアントJARファイルを含めます。

1. Forms Java APIオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `FormsServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. カスタムfscmenu XMLファイルの参照

   * `HTMLRenderSpec`オブジェクトを作成するには、コンストラクタを使用します。
   * ツールバーでHTMLフォームをレンダリングするには、`HTMLRenderSpec`オブジェクトの`setHTMLToolbar`メソッドを呼び出して、`HTMLToolbar`列挙値を渡します。 例えば、垂直方向のHTMLツールバーを表示するには、`HTMLToolbar.Vertical`を渡します。
   * `HTMLRenderSpec`オブジェクトの`setToolbarURI`メソッドを呼び出し、XMLファイルのURI位置を指定する文字列値を渡して、fscmenu XMLファイルの場所を指定します。
   * 該当する場合は、`HTMLRenderSpec`オブジェクトの`setLocale`メソッドを呼び出し、ロケール値を指定する文字列値を渡してロケール値を設定します。 デフォルト値は英語です。

   >[!NOTE]
   >
   >このセクションに関連付けられているクイックスタートは、この値を&#x200B;`fr_FR`*.*&#x200B;に設定します。

1. HTMLフォームのレンダリング

   `FormsServiceClient`オブジェクトの`renderHTMLForm`メソッドを呼び出し、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定するstring値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、必ず`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`のように完全なパスを指定してください。
   * HTML環境設定タイプを指定する`TransformTo`列挙値。 例えば、Internet Explorer 5.0以降の動的HTMLと互換性のあるHTMLフォームをレンダリングするには、`TransformTo.MSDHTML`と指定します。
   * フォームとマージするデータを含む`com.adobe.idp.Document`オブジェクト。 データを結合しない場合は、空の`com.adobe.idp.Document`オブジェクトを渡します。
   * HTML実行時オプションを格納する`HTMLRenderSpec`オブジェクト。
   * `HTTP_USER_AGENT`ヘッダー値を指定するstring値（`Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`など）。
   * HTMLフォームのレンダリングに必要なURI値を格納する`URLSpec`オブジェクト。
   * 添付ファイルを格納する`java.util.HashMap`オブジェクト。 これはオプションのパラメーターで、フォームにファイルを添付しない場合は`null`を指定できます。

   `renderHTMLForm`メソッドは、クライアントのWebブラウザーに書き込む必要があるフォームデータストリームを含む`FormsResult`オブジェクトを返します。

1. フォームデータストリームをクライアントWebブラウザーに書き込む

   * `FormsResult`オブジェクトの`getOutputContent`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトを作成します。
   * `getContentType`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトのコンテンツタイプを取得します。
   * `setContentType`メソッドを呼び出し、`com.adobe.idp.Document`オブジェクトのコンテンツタイプを渡すことで、`javax.servlet.http.HttpServletResponse`オブジェクトのコンテンツタイプを設定します。
   * `javax.servlet.http.HttpServletResponse`オブジェクトの`getOutputStream`メソッドを呼び出して、フォームデータストリームをクライアントWebブラウザーに書き込むために使用する`javax.servlet.ServletOutputStream`オブジェクトを作成します。
   * `com.adobe.idp.Document`オブジェクトの`getInputStream`メソッドを呼び出して、`java.io.InputStream`オブジェクトを作成します。
   * `InputStream`オブジェクトの`read`メソッドを呼び出し、バイト配列を引数として渡すことで、バイト配列を作成し、フォームデータストリームに入力します。
   * `javax.servlet.ServletOutputStream`オブジェクトの`write`メソッドを呼び出して、フォームデータストリームをクライアントWebブラウザーに送信します。 `write`メソッドにバイト配列を渡します。

**関連トピック**

[クイックスタート（SOAPモード）:Java APIを使用した、カスタムツールバーでのHTMLフォームのレンダリング](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-with-a-custom-toolbar-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api}を使用したカスタムツールバーでのHTMLフォームのレンダリング

FormsサービスAPI（Webサービス）を使用して、カスタムツールバーを含むHTMLフォームをレンダリングします。

1. プロジェクトファイルを含める

   * FormsサービスのWSDLを使用するJavaプロキシクラスを作成します。
   * クラスパスにJavaプロキシクラスを含めます。

1. Forms Java APIオブジェクトの作成

   `FormsService`オブジェクトを作成し、認証値を設定します。

1. カスタムfscmenu XMLファイルの参照

   * `HTMLRenderSpec`オブジェクトを作成するには、コンストラクタを使用します。
   * ツールバーでHTMLフォームをレンダリングするには、`HTMLRenderSpec`オブジェクトの`setHTMLToolbar`メソッドを呼び出して、`HTMLToolbar`列挙値を渡します。 例えば、垂直方向のHTMLツールバーを表示するには、`HTMLToolbar.Vertical`を渡します。
   * `HTMLRenderSpec`オブジェクトの`setToolbarURI`メソッドを呼び出し、XMLファイルのURI位置を指定する文字列値を渡して、fscmenu XMLファイルの場所を指定します。
   * 該当する場合は、`HTMLRenderSpec`オブジェクトの`setLocale`メソッドを呼び出し、ロケール値を指定する文字列値を渡してロケール値を設定します。 デフォルト値は英語です。

   >[!NOTE]
   >
   >このセクションに関連付けられているクイックスタートは、この値を&#x200B;`fr_FR`*.*&#x200B;に設定します。

1. HTMLフォームのレンダリング

   `FormsService`オブジェクトの`renderHTMLForm`メソッドを呼び出し、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定するstring値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、必ず`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`のように完全なパスを指定してください。
   * HTML環境設定タイプを指定する`TransformTo`列挙値。 例えば、Internet Explorer 5.0以降の動的HTMLと互換性のあるHTMLフォームをレンダリングするには、`TransformTo.MSDHTML`と指定します。
   * フォームとマージするデータを含む`BLOB`オブジェクト。 データを結合しない場合は、`null`を渡します。
   * HTML実行時オプションを格納する`HTMLRenderSpec`オブジェクト。
   * `HTTP_USER_AGENT`ヘッダー値を指定するstring値（`Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322`など）。 この値を設定しない場合は、空の文字列を渡すことができます。
   * HTMLフォームのレンダリングに必要なURI値を格納する`URLSpec`オブジェクト。
   * 添付ファイルを格納する`java.util.HashMap`オブジェクト。 このパラメーターはオプションです。フォームにファイルを添付しない場合は、`null`を指定できます。
   * `renderHTMLForm`メソッドで設定される空の`com.adobe.idp.services.holders.BLOBHolder`オブジェクト。 このパラメーター値は、レンダリングされたフォームを保存します。
   * `renderHTMLForm`メソッドで設定される空の`com.adobe.idp.services.holders.BLOBHolder`オブジェクト。 このパラメーターは、出力XMLデータを格納します。
   * `renderHTMLForm`メソッドで設定される空の`javax.xml.rpc.holders.LongHolder`オブジェクト。 この引数は、フォームのページ数を保存します。
   * `renderHTMLForm`メソッドで設定される空の`javax.xml.rpc.holders.StringHolder`オブジェクト。 この引数はロケール値を格納します。
   * `renderHTMLForm`メソッドで設定される空の`javax.xml.rpc.holders.StringHolder`オブジェクト。 この引数は、使用されるHTMLレンダリング値を格納します。
   * この操作の結果を格納する空の`com.adobe.idp.services.holders.FormsResultHolder`オブジェクト。

   `renderHTMLForm`メソッドは、最後の引数値として渡される`com.adobe.idp.services.holders.FormsResultHolder`オブジェクトに、クライアントWebブラウザーに書き込む必要のあるフォームデータストリームを設定します。

1. フォームデータストリームをクライアントWebブラウザーに書き込む

   * `com.adobe.idp.services.holders.FormsResultHolder`オブジェクトの`value`データメンバーの値を取得して、`FormResult`オブジェクトを作成します。
   * `FormsResult`オブジェクトの`getOutputContent`メソッドを呼び出して、フォームデータを含む`BLOB`オブジェクトを作成します。
   * `getContentType`メソッドを呼び出して、`BLOB`オブジェクトのコンテンツタイプを取得します。
   * `setContentType`メソッドを呼び出し、`BLOB`オブジェクトのコンテンツタイプを渡すことで、`javax.servlet.http.HttpServletResponse`オブジェクトのコンテンツタイプを設定します。
   * `javax.servlet.http.HttpServletResponse`オブジェクトの`getOutputStream`メソッドを呼び出して、フォームデータストリームをクライアントWebブラウザーに書き込むために使用する`javax.servlet.ServletOutputStream`オブジェクトを作成します。
   * バイト配列を作成し、`BLOB`オブジェクトの`getBinaryData`メソッドを呼び出してそれを設定します。 このタスクは、`FormsResult`オブジェクトの内容をバイト配列に割り当てます。
   * `javax.servlet.http.HttpServletResponse`オブジェクトの`write`メソッドを呼び出して、フォームデータストリームをクライアントWebブラウザーに送信します。 `write`メソッドにバイト配列を渡します。

**関連トピック**

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
