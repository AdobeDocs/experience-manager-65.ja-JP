---
title: CustomToolbars を使用した HTML フォームのレンダリング
seo-title: Rendering HTML Forms with CustomToolbars
description: Forms サービスを使用して、HTML フォームでレンダリングされるツールバーをカスタマイズします。Java API と web サービス API を使用して、カスタムツールバーを含む HTML フォームをレンダリングできます。
seo-description: Use the Forms service to customize a toolbar that is rendered with an HTML form. You can render an HTML Form with a custom toolbar using the Java API and a Web Service API.
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
source-wordcount: '2345'
ht-degree: 100%

---

# CustomToolbars を使用した HTML フォームのレンダリング {#rendering-html-forms-with-customtoolbars}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

## カスタムツールバーを持つ HTML Forms のレンダリング {#rendering-html-forms-with-custom-toolbars}

Forms サービスを使用すると、HTML フォームでレンダリングされるツールバーをカスタマイズできます。ツールバーは、デフォルトの CSS スタイルをオーバーライドして外観を変更したり、Java スクリプトをオーバーライドして動的な動作を追加したりするようにカスタマイズできます。ツールバーは、fscmenu.xml という名前の XML ファイルを使用してカスタマイズされます。デフォルトでは、Forms サービスは内部で指定された URI の場所からこのファイルを取得します。

>[!NOTE]
>
>この URI の場所は、adobe-forms-core.jar ファイル（adobe-forms-dsc.jar ファイル内）にあります。adobe-forms-dsc.jar ファイルは、C:\Adobe\Adobe_Experience_Manager_forms\ folder にあります（C:\ はインストールディレクトリです）。Win RAR などのファイル抽出ツールを使用して、adobe を開くことができます。

この場所から fscmenu.xml をコピーして、必要に応じて変更し、カスタムの URI の場所に配置できます。次に、Forms Service API を使用して、指定された場所の fscmenu.xml ファイルを Forms サービスが使用するように、ランタイムオプションを設定します。これらのアクションにより、Forms サービスはカスタムツールバーを持つ HTML フォームをレンダリングします。

fscmenu.xml ファイルに加えて、次のファイルも取得する必要があります。

* fscmenu.js
* fscattachments.js
* fscmenu.css
* fscmenu-v.css
* fscmenu-ie.css
* fscdialog.css

fscJS は、各ノードに関連付けられる Java スクリプトです。`div#fscmenu` ノード用とオプションで `ul#fscmenuItem` ノード用を提供する必要があります。JS ファイルはツールバーのコア機能を実装し、デフォルトファイルが機能します。

fscCSS は、特定のノードに関連付けられているスタイルシートです。CSS ファイルのスタイルによって、ツールバーの外観が指定されます。*fscVCSS* は、レンダリングされた HTML フォームの左側に表示される、縦向きのツールバーのスタイルシートです。*fscIECSS* は、Internet Explorer でレンダリングされる HTML フォームに使用されるスタイルシートです。

上記のすべてのファイルが fscmenu.xml ファイルで参照されていることを確認します。つまり、fscmenu.xml ファイルで、これらのファイルを指す URI の場所を指定し、Forms サービスでそれらのファイルを検索できるようにします。デフォルトでは、これらのファイルは、内部キーワード `FSWebRoot` または `ApplicationWebRoot` で始まる URI の場所で利用できます。

ツールバーをカスタマイズするには、これらのキーワードを外部キーワード `FSToolBarURI` で置き換えます。このキーワードは、実行時に Forms サービスに渡される URI を表します（この方法については、この節で後述します）。

また、これらの JS ファイルと CSS ファイルの絶対的な場所（例：https://www.mycompany.com/scripts/misc/fscmenu.js）を指定することもできます。その場合、`FSToolBarURI` キーワードを使用する必要はありません。

>[!NOTE]
>
>これらのファイルの参照方法を混在させることはお勧めしません。つまり、すべての URI は、`FSToolBarURI` キーワードまたは絶対位置のいずれかを使用して、参照する必要があります。

JS ファイルと CSS ファイルを取得するには、adobe-forms-&lt;appserver>.ear ファイルを開きます。このファイル内で、adobe-forms-res.war を開きます。これらのファイルはすべて WAR ファイル内にあります。adobe-forms-&lt;appserver>.ear ファイルは、AEM Forms のインストールフォルダー内にあります（C:\ はインストールディレクトリです）。adobe-forms-&lt;appserver>.ear は、WinRAR などのファイル展開ツールを使用して開くことができます。

次の XML 構文は、サンプルの fscmenu.xml ファイルを示しています。

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
>太字のテキストは、参照する必要がある CSS ファイルおよび JS ファイルへの URI を表します。

次の項目では、ツールバーをカスタマイズする方法を説明します。

* `fscJS`、`fscCSS`、`fscVCSS`、`fscIECSS` 属性（fscmenu.xml ファイル内）の値を変更し、この節で説明するメソッドの 1 つ（例：`fscJS="FSToolBarURI/scripts/fscmenu.js"`）を使用して、参照されるファイルのカスタムの場所を反映させます。
* すべての CSS ファイルと JS ファイルを指定する必要があります。どのファイルも変更されない場合は、カスタムの場所にデフォルトのファイルを指定します。デフォルトのファイルを取得するには、この節で説明するように、様々なファイルを開きます。
* どのファイルに対しても、絶対参照（例えば、https://www.example.com/scripts/custom-vertical-fscmenu.css）を指定できます。
* `div#fscmenu` ノードが必要とする JS ファイルと CSS ファイルは、ツールバー機能に不可欠なものです。個々の `ul#fscmenuItem` ノードには、サポートする JS ファイルまたは CSS ファイルがある場合とない場合があります。

**ロケール値の変更**

ツールバーのカスタマイズの一環として、ツールバーのロケール値を変更できます。つまり、別の言語で表示できます。次の図は、フランス語で表示されたカスタムツールバーを示しています。

>[!NOTE]
>
>複数の言語でカスタムツールバーを作成することはできません。ツールバーは、ロケール設定に基づいて異なる XML ファイルを使用することはできません。

ツールバーのロケール値を変更するには、fscmenu.xml ファイルに表示する言語が含まれていることを確認します。次の XML 構文は、フランス語のツールバーを表示するために使用される fscmenu.xml ファイルを示しています。

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
>このセクションに関連付けられているクイックスタートは、前の図に示すように、この XML ファイルを使用してフランス語のカスタムツールバーを表示します。

また、`HTMLRenderSpec` オブジェクトの `setLocale` メソッドを呼び出してロケール値を指定する文字列値を渡すことによって、有効なロケール値を指定します。例えば、`fr_FR` を渡してフランス語を指定します。Forms サービスは、ローカライズされたツールバーにバンドルされています。

>[!NOTE]
>
>カスタムツールバーを使用する HTML フォームをレンダリングする前に、HTML フォームのレンダリング方法を知っておく必要があります（[フォームを HTML としてレンダリング](/help/forms/developing/rendering-forms-html.md)を参照）。

Forms サービスについて詳しくは、[AEM Forms サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary-of-steps}

カスタムツールバーを含む HTML フォームをレンダリングするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Forms Java API オブジェクトを作成します。
1. カスタム fscmenu XML ファイルを参照します。
1. HTML フォームをレンダリングします。
1. フォームデータストリームをクライアントの Web ブラウザーに書き込みます。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを含めます。

**Forms Java API オブジェクトの作成**

Forms サービスがサポートする操作をプログラムで実行する前に、Forms クライアントオブジェクトを作成する必要があります。

**カスタム fscmenu XML ファイルの参照**

カスタムツールバーを含む HTML フォームをレンダリングするには、ツールバーを記述する fscmenu XML ファイルを参照します（この節では、fscmenu XML ファイルの 2 つの例を示します）。また、fscmenu.xml ファイルで、参照されるすべてのファイルの場所が正しく指定されていることを確認します。この節で前述したように、すべてのファイルが `FSToolBarURI` キーワードまたはそれらの絶対位置のいずれかによって参照されていることを確認してください。

**HTMLフォームのレンダリング**

HTML フォームをレンダリングするには、Designer で作成され XDP ファイルとして保存されたフォームデザインを指定します。また、変換タイプとして HTML を選択します。たとえば、Internet Explorer 5.0 以降のダイナミック HTML をレンダリングする HTML 変換タイプを指定できます。

また、HTML フォームのレンダリングには、他のフォームタイプをレンダリングするための URI 値などの値も必要です。

**クライアント web ブラウザーへのフォームデータストリームの書き込み**

Forms サービスが HTML フォームをレンダリングすると、フォームデータストリームが返されます。このデータストリームは、HTML フォームをユーザーに表示するためにクライアントの web ブラウザーに書き込む必要があります。

**関連トピック**

[Java API を使用してカスタムツールバーを含む HTML フォームをレンダリングする](#render-an-html-form-with-a-custom-toolbar-using-the-java-api)

[Web サービス API を使用してカスタムツールバーを含む HTML フォームをレンダリングする](#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms サービス API のクイックスタート](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[インタラクティブ PDF Forms のレンダリング](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Forms を HTML としてレンダリング](/help/forms/developing/rendering-forms-html.md)

[Forms をレンダリングする web アプリケーションの作成](/help/forms/developing/creating-web-applications-renders-forms.md)

### Java API を使用してカスタムツールバーを含む HTML フォームをレンダリングする {#render-an-html-form-with-a-custom-toolbar-using-the-java-api}

Forms Service API（Java）を使用して、カスタムツールバーを含む HTML フォームをレンダリングします。

1. プロジェクトファイルを含める

   adobe-forms-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. Forms Java API オブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `FormsServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. カスタム fscmenu XML ファイルの参照

   * コンストラクターを使用して `HTMLRenderSpec` オブジェクトを作成します。
   * ツールバーを使用して HTML フォームをレンダリングするには、`HTMLRenderSpec` オブジェクトの `setHTMLToolbar` メソッドを呼び出して、`HTMLToolbar` enum 値を渡します。例えば、縦の HTML ツールバーを表示するには、`HTMLToolbar.Vertical` を渡します。
   * `HTMLRenderSpec` オブジェクトの `setToolbarURI` メソッドを呼び出して XML ファイルの URI の場所を指定する文字列値を渡すことによって、fscmenuXML ファイルの場所を指定します。
   * 該当する場合は、`HTMLRenderSpec` オブジェクトの `setLocale` メソッドを呼び出してロケール値を指定する文字列値を渡すことによって、ロケール値を設定します。デフォルト値は英語です。

   >[!NOTE]
   >
   >この節に関連するクイックスタートでは、この値を `fr_FR`*に設定します。*

1. HTML フォームのレンダリング

   `FormsServiceClient` オブジェクトの `renderHTMLForm` メソッドを呼び出して、次の値を渡します。

   * フォームデザイン名を指定する文字列値で、ファイル名の拡張子も含まれます。Forms アプリケーションの一部であるフォームデザインを参照する場合は、必ず次のような完全なパスを指定します。`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`
   * HTML の環境設定タイプを指定する `TransformTo` enum 値。例えば、Internet Explorer 5.0 以降の動的 HTML と互換性のある HTML フォームをレンダリングするには、`TransformTo.MSDHTML` を指定します。
   * フォームに結合するデータを含む `com.adobe.idp.Document` オブジェクト。データを結合しない場合は、空の `com.adobe.idp.Document` オブジェクトを渡します。
   * HTML の実行時オプションが格納された `HTMLRenderSpec` オブジェクト。
   * `HTTP_USER_AGENT` ヘッダー値（例：`Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`）を指定する文字列値。
   * HTML フォームのレンダリングに必要な URI 値が格納された `URLSpec` オブジェクト。
   * 添付ファイルを格納する `java.util.HashMap` オブジェクト。 これはオプションのパラメーターで、 フォームにファイルを添付しない場合は `null` を指定できます。

   `renderHTMLForm` メソッドは、 クライアント web ブラウザーに書き込む必要があるフォームデータストリームを含んだ `FormsResult` オブジェクトを返します。

1. フォームデータストリームをクライアント web ブラウザーに書き込む

   * `FormsResult` オブジェクトの `getOutputContent` メソッドを呼び出して、`com.adobe.idp.Document` オブジェクトを作成します。
   * `getContentType` メソッドを呼び出して、`com.adobe.idp.Document` オブジェクトのコンテンツタイプを取得します。
   * `setContentType` メソッドを呼び出し、`com.adobe.idp.Document` オブジェクトのコンテンツタイプを渡すことで、`javax.servlet.http.HttpServletResponse` オブジェクトのコンテンツタイプを設定します。
   * `javax.servlet.http.HttpServletResponse` オブジェクトの `getOutputStream` メソッドを呼び出して、フォームデータストリームをクライアント web ブラウザーに書き出すのに使用される `javax.servlet.ServletOutputStream` オブジェクトを作成します。
   * `com.adobe.idp.Document` オブジェクトの `getInputStream` メソッドを呼び出して、`java.io.InputStream` オブジェクトを作成します。
   * `InputStream` オブジェクトの `read` メソッドを呼び出してバイト配列を引数として渡すことによって、バイト配列を作成してフォームデータストリームを入力します。
   * `javax.servlet.ServletOutputStream` オブジェクトの `write` メソッドを呼び出して、フォームデータストリームをクライアント web ブラウザーに送信します。バイト配列を `write` メソッドに渡します。

**関連トピック**

[クイックスタート（SOAP モード）：Java API を使用した、カスタムツールバーでの HTML フォームのレンダリング](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-with-a-custom-toolbar-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用してカスタムツールバーを含む HTML フォームをレンダリングする {#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api}

Forms サービス API（web サービス）を使用して、カスタムツールバーを含んだ HTML フォームをレンダリングします。

1. プロジェクトファイルを含める

   * Forms Service WSDL を使用する Java プロキシクラスを作成します。
   * クラスパスに Java プロキシクラスを含めます。

1. Forms Java API オブジェクトの作成

   `FormsService` オブジェクトを作成し、認証値を設定します。

1. カスタム fscmenu XML ファイルの参照

   * コンストラクターを使用して `HTMLRenderSpec` オブジェクトを作成します。
   * ツールバーを使用して HTML フォームをレンダリングするには、`HTMLRenderSpec` オブジェクトの `setHTMLToolbar` メソッドを呼び出して、`HTMLToolbar` enum 値を渡します。例えば、縦の HTML ツールバーを表示するには、`HTMLToolbar.Vertical` を渡します。
   * `HTMLRenderSpec` オブジェクトの `setToolbarURI` メソッドを呼び出して XML ファイルの URI の場所を指定する文字列値を渡すことによって、fscmenuXML ファイルの場所を指定します。
   * 該当する場合は、`HTMLRenderSpec` オブジェクトの `setLocale` メソッドを呼び出してロケール値を指定する文字列値を渡すことによって、ロケール値を設定します。デフォルト値は英語です。

   >[!NOTE]
   >
   >この節に関連するクイックスタートでは、この値を `fr_FR`*に設定します。*

1. HTML フォームのレンダリング

   `FormsService` オブジェクトの `renderHTMLForm` メソッドを呼び出して、次の値を渡します。

   * フォームデザイン名を指定する文字列値で、ファイル名の拡張子も含まれます。Forms アプリケーションの一部であるフォームデザインを参照する場合は、必ず次のような完全なパスを指定します。`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`
   * HTML の環境設定タイプを指定する `TransformTo` enum 値。例えば、Internet Explorer 5.0 以降の動的 HTML と互換性のある HTML フォームをレンダリングするには、`TransformTo.MSDHTML` を指定します。
   * フォームと結合するデータを含んだ `BLOB` オブジェクト。 データを結合しない場合は、 `null` を渡します。
   * HTML の実行時オプションが格納されている `HTMLRenderSpec` オブジェクト。
   * `HTTP_USER_AGENT` ヘッダー値を指定する文字列値（例：`Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322`)）。この値を設定しない場合は、空の文字列を渡します。
   * HTML フォームのレンダリングに必要な URI 値を格納する `URLSpec` オブジェクト。
   * 添付ファイルを格納する `java.util.HashMap` オブジェクト。このパラメーターはオプションで、フォームにファイルを添付しない場合は `null` を指定できます。
   * `renderHTMLForm` メソッドでデータが入力される空の `com.adobe.idp.services.holders.BLOBHolder` オブジェクト。このパラメーター値には、レンダリングされたフォームが格納されます。
   * `renderHTMLForm` メソッドで入力される空の `com.adobe.idp.services.holders.BLOBHolder` オブジェクト。このパラメーターには、出力 XML データが格納されます。
   * `renderHTMLForm` メソッドでデータが入力される空の `javax.xml.rpc.holders.LongHolder` オブジェクト。この引数には、フォームのページ数が格納されます。
   * `renderHTMLForm` メソッドでデータが入力される空の `javax.xml.rpc.holders.StringHolder` オブジェクト。 この引数には、ロケール値が格納されます。
   * `renderHTMLForm` メソッドでデータが入力される空の `javax.xml.rpc.holders.StringHolder` オブジェクト。この引数には、使用する HTML レンダリング値が格納されます。
   * この操作の結果を格納する空の `com.adobe.idp.services.holders.FormsResultHolder` オブジェクト。

   `renderHTMLForm` メソッドは、最後の引数値として渡される `com.adobe.idp.services.holders.FormsResultHolder` オブジェクトに、クライアント web ブラウザーに書き込む必要のあるフォームデータストリームを入力します。

1. フォームデータストリームをクライアント web ブラウザーに書き込む

   * `com.adobe.idp.services.holders.FormsResultHolder` オブジェクトの `value` データメンバーの値を取得して、`FormResult` オブジェクトを作成します。
   * `FormsResult` オブジェクトの `getOutputContent` メソッドを呼び出して、フォームデータを含む `BLOB` オブジェクトを作成します。
   * `getContentType` メソッドを呼び出して、`BLOB` オブジェクトのコンテンツタイプを取得します。
   * `setContentType` メソッドを呼び出し、`BLOB` オブジェクトのコンテンツタイプを渡すことで、`javax.servlet.http.HttpServletResponse` オブジェクトのコンテンツタイプを設定します。
   * フォームデータストリームをクライアント web ブラウザーに書き出すのに使用される `javax.servlet.ServletOutputStream` オブジェクトを、`javax.servlet.http.HttpServletResponse` オブジェクトの `getOutputStream` メソッドを呼び出して作成します。
   * バイト配列を作成し、`BLOB` オブジェクトの `getBinaryData` メソッドを呼び出して値を入力します。このタスクは、`FormsResult` オブジェクトのコンテンツをバイト配列に割り当てます。
   * `javax.servlet.http.HttpServletResponse` オブジェクトの `write` メソッドを呼び出して、フォームデータストリームをクライアント web ブラウザーに送信します。バイト配列を `write` メソッドに渡します。

**関連トピック**

[Base64 エンコーディングを使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
