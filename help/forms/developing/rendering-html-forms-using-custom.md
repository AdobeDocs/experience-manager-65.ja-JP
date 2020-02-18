---
title: カスタムCSSファイルを使用したHTMLフォームのレンダリング
seo-title: カスタムCSSファイルを使用したHTMLフォームのレンダリング
description: 'null'
seo-description: 'null'
uuid: a44e96f1-001d-48a2-8c96-15cb9d0c71b3
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8fe7c072-7df0-44b7-92d0-bf39dc1e688a
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# カスタムCSSファイルを使用したHTMLフォームのレンダリング {#rendering-html-forms-using-custom-css-files}

Formsサービスは、WebブラウザーからのHTTP要求に応じてHTMLフォームをレンダリングします。 HTMLフォームをレンダリングする場合、FormsサービスはカスタムCSSファイルを参照できます。 Formsサービスを使用してHTMLフォームをレンダリングする場合、ビジネス要件に合わせてカスタムCSSファイルを作成し、そのCSSファイルを参照できます。

Formsサービスは、カスタムCSSファイルをサイレントに解析します。 つまり、カスタムCSSファイルがCSS標準に準拠していない場合に発生する可能性のあるエラーは、Formsサービスから報告されません。 この場合、Formsサービスはスタイルを無視し、CSSファイル内の残りのスタイルを使用し続けます。

次のリストは、カスタムCSSファイルでサポートされるスタイルを指定します。

* **クラスレベルのセレクタースタイルのペア**:カスタムCSSファイルに存在する場合は、HTMLフォームでクラススタイルとして使用されるセレクターが使用されます。 未使用のクラススタイルは無視されます。
* **識別子レベルのセレクタースタイルのペア**:HTMLフォームで使用される場合は、すべての識別子スタイルが使用されます。
* **要素レベルのセレクタースタイルのペア**:HTMLフォームで使用されている場合は、すべての要素スタイルが使用されます。
* **Style Priority**:スタイルの優先順位（重要な場合と同様）はサポートされ、カスタムCSSファイルで使用できます。
* **メディアの種類**:1つ以上のセレクタースタイルのペアを@mediaスタイルでラップして、メディアタイプを定義できます。 Formsサービスは、指定されたメディアの種類がサポートされているかどうかを確認しません。 カスタムCSSファイルで指定されたメディアタイプがHTMLフォームに結合されます。

サンプルのCSSファイルは、FormsIVSアプリケーションを使用して取得できます。 フォームをアップロードし、Test Form Designページでフォームを選択して、「GenerateCSS」をクリックします。 ボタンをクリックする前にHTML変換タイプを設定する必要はありません。 次に「保存」を選択します。 このCSSファイルは、ビジネス要件に合わせて編集できます。

>[!NOTE]
>
>カスタムCSSファイルを使用するHTMLフォームをレンダリングする前に、HTMLフォームのレンダリングについて十分に理解しておくことが重要です。 (「フォーム [のHTMLとしてのレンダリング](/help/forms/developing/rendering-forms-html.md)」を参照)。

>[!NOTE]
>
>For more information about the Forms service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## 手順の概要 {#summary-of-steps}

CSSファイルを使用するHTMLフォームをレンダリングするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Forms Java APIオブジェクトを作成します。
1. CSSファイルを参照します。
1. HTMLフォームをレンダリングします。
1. クライアントのWebブラウザーにフォームデータストリームを書き込みます。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

**フォームJava APIオブジェクトの作成**

Formsサービスでサポートされている操作をプログラムで実行する前に、Formsクライアントオブジェクトを作成する必要があります。

**CSSファイルの参照**

カスタムCSSファイルを使用するHTMLフォームをレンダリングするには、既存のCSSファイルを必ず参照してください。

**HTMLフォームのレンダリング**

HTMLフォームをレンダリングするには、Designerで作成し、XDPファイルとして保存するフォームデザインを指定する必要があります。 また、HTML変換タイプを選択する必要があります。 例えば、Internet Explorer 5.0以降用の動的HTMLをレンダリングするHTML変換タイプを指定できます。

HTMLフォームのレンダリングには、他のフォームタイプをレンダリングするために必要なURI値などの値も必要です。

**クライアントのWebブラウザーにフォームデータストリームを書き込みます**

Formsサービスは、HTMLフォームをレンダリングするときに、フォームデータストリームを返します。このストリームをクライアントのWebブラウザーに書き込み、HTMLフォームをユーザーに表示させる必要があります。

**関連トピック**

[Java APIを使用したCSSファイルを使用したHTMLフォームのレンダリング](#render-an-html-form-that-uses-a-css-file-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[FormsサービスAPIのクイックスタート](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[インタラクティブPDFフォームのレンダリング](/help/forms/developing/rendering-interactive-pdf-forms.md)

[HTMLとしてのフォームのレンダリング](/help/forms/developing/rendering-forms-html.md)

[フォームをレンダリングするWebアプリケーションの作成](/help/forms/developing/creating-web-applications-renders-forms.md)

## Java APIを使用したCSSファイルを使用したHTMLフォームのレンダリング {#render-an-html-form-that-uses-a-css-file-using-the-java-api}

Forms API(Java)を使用して、カスタムCSSファイルを使用するHTMLフォームをレンダリングします。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-forms-client.jarなどのクライアントJARファイルを含めます。

1. フォームJava APIオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `FormsServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. CSSファイルの参照

   * Create an `HTMLRenderSpec` object by using its constructor.
   * カスタムCSSファイルを使用するHTMLフォームをレンダリングするには、オブジェクトのメソッ `HTMLRenderSpec` ドを呼び出 `setCustomCSSURI` し、CSSファイルの場所と名前を指定するstring値を渡します。

1. HTMLフォームのレンダリング

   オブジェクト `FormsServiceClient` のメソッドを `(Deprecated) (Deprecated) renderHTMLForm` 呼び出し、次の値を渡します。

   * ファイル名の拡張子を含むフォームデザイン名を指定するstring値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、必ずなどの完全なパスを指定してくださ `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`い。
   * HTMLプ `TransformTo` リファレンスタイプを指定するenum値。 例えば、Internet Explorer 5.0以降用の動的HTMLと互換性のあるHTMLフォームをレンダリングするには、を指定します `TransformTo.MSDHTML`。
   * フォーム `com.adobe.idp.Document` とマージするデータを含むオブジェクトです。 データをマージしない場合は、空のオブジェクトを渡し `com.adobe.idp.Document` ます。
   * HTML実行 `HTMLRenderSpec` 時オプションを格納するオブジェクトです。
   * ヘッダー値を指定す `HTTP_USER_AGENT` るstring値(例： `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`)。
   * HTMLフォ `URLSpec` ームのレンダリングに必要なURI値を格納するオブジェクトです。
   * 添付フ `java.util.HashMap` ァイルを格納するオブジェクト。 これはオプションのパラメーターで、フォームにフ `null` ァイルを添付しないかどうかを指定できます。
   このメソ `(Deprecated) renderHTMLForm` ッドは、クライア `FormsResult` ントのWebブラウザーに書き込む必要があるフォームデータストリームを含むオブジェクトを返します。

1. クライアントのWebブラウザーにフォームデータストリームを書き込みます

   * オブジェクトの `com.adobe.idp.Document` メソッドを呼び出して、オ `FormsResult` ブジェクトを作成 `getOutputContent` します。
   * メソッドを呼び出して、オブジェ `com.adobe.idp.Document` クトのコンテンツタイプを取得 `getContentType` します。
   * メソッドを呼 `javax.servlet.http.HttpServletResponse` び出し、オブジェクトのコンテンツタ `setContentType` イプを渡すことで、オブジェクトのコンテンツタイプを設定 `com.adobe.idp.Document` します。
   * オブジェクトの `javax.servlet.ServletOutputStream` メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに書き込むために使用する `javax.servlet.h\ttp.HttpServletResponse` オブジェクトを作 `getOutputStream` 成します。
   * オブジェクト `java.io.InputStream` のメソッドを呼び出して、オ `com.adobe.idp.Document` ブジェクトを作成 `getInputStream` します。
   * バイト配列を作成し、オブジェクトのメソッドを呼び出し、バイト配列を引数 `InputStream` として渡すこ `read` とで、フォームデータストリームを設定します。
   * オブジェクト `javax.servlet.ServletOutputStream` のメソッドを呼び `write` 出して、フォームデータストリームをクライアントWebブラウザーに送信します。 バイト配列をメソッドに渡し `write` ます。

**関連トピック**

[カスタムCSSファイルを使用したHTMLフォームのレンダリング](#rendering-html-forms-using-custom-css-files)

[クイックスタート（SOAPモード）:Java APIを使用したCSSファイルを使用したHTMLフォームのレンダリング](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-that-uses-a-css-file-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## WebサービスAPIを使用してCSSファイルを使用するHTMLフォームをレンダリングする {#render-an-html-form-that-uses-a-css-file-using-the-web-service-api}

Forms API（Webサービス）を使用して、カスタムCSSファイルを使用するHTMLフォームをレンダリングします。

1. プロジェクトファイルを含める

   * FormsサービスWSDLを使用するJavaプロキシクラスを作成します。
   * クラスパスにJavaプロキシクラスを含めます。

1. フォームJava APIオブジェクトの作成

   オブジェクト `FormsService` を作成し、認証値を設定します。

1. CSSファイルの参照

   * Create an `HTMLRenderSpec` object by using its constructor.
   * カスタムCSSファイルを使用するHTMLフォームをレンダリングするには、オブジェクトのメソッ `HTMLRenderSpec` ドを呼び出 `setCustomCSSURI` し、CSSファイルの場所と名前を指定するstring値を渡します。

1. HTMLフォームのレンダリング

   オブジェクト `FormsService` のメソッドを `(Deprecated) renderHTMLForm` 呼び出し、次の値を渡します。

   * ファイル名の拡張子を含むフォームデザイン名を指定するstring値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、必ずなどの完全なパスを指定してくださ `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`い。
   * HTMLプ `TransformTo` リファレンスタイプを指定するenum値。 例えば、Internet Explorer 5.0以降用の動的HTMLと互換性のあるHTMLフォームをレンダリングするには、を指定します `TransformTo.MSDHTML`。
   * フォーム `BLOB` とマージするデータを含むオブジェクトです。 データを結合しない場合は、を渡します `null`。 ( [Prepulating Forms with Flowable Layouts](/help/forms/developing/rendering-forms-rendering-forms prepopulating-forms-flowable-layouts-prepogulating.md#prepopulating-forms-with-flowable-layouts)を参照)。
   * HTML実行 `HTMLRenderSpec` 時オプションを格納するオブジェクトです。
   * ヘッダー値を指定す `HTTP_USER_AGENT` るstring値(例： `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`)。 この値を設定しない場合は、空の文字列を渡すことができます。
   * HTMLフォ `URLSpec` ームのレンダリングに必要なURI値を格納するオブジェクトです。
   * 添付フ `java.util.HashMap` ァイルを格納するオブジェクト。 これはオプションのパラメーターで、フォームにフ `null` ァイルを添付しないかどうかを指定できます。
   * メソッドに `com.adobe.idp.services.holders.BLOBHolder` よって入力される空のオブジェ `(Deprecated) renderHTMLForm` クト。 このパラメーター値は、レンダリングされたフォームを保存します。
   * メソッドに `com.adobe.idp.services.holders.BLOBHolder` よって入力される空のオブジェ `(Deprecated) renderHTMLForm` クト。 このパラメーターは、出力XMLデータを格納します。
   * メソッドに `javax.xml.rpc.holders.LongHolder` よって入力される空のオブジェ `(Deprecated) renderHTMLForm` クト。 この引数は、フォーム内のページ数を格納します。
   * メソッドに `javax.xml.rpc.holders.StringHolder` よって入力される空のオブジェ `(Deprecated) renderHTMLForm` クト。 この引数はロケールの値を格納します。
   * メソッドに `javax.xml.rpc.holders.StringHolder` よって入力される空のオブジェ `(Deprecated) renderHTMLForm` クト。 この引数は、使用されるHTMLレンダリング値を格納します。
   * この操作 `com.adobe.idp.services.holders.FormsResultHolder` の結果を含む空のオブジェクトです。
   メソッド `(Deprecated) renderHTMLForm` は、最後の引 `com.adobe.idp.services.holders.FormsResultHolder` 数値として渡されたオブジェクトに、クライアントWebブラウザーに書き込む必要があるフォームデータストリームを入力します。

1. クライアントのWebブラウザーにフォームデータストリームを書き込みます

   * オブジェクト `FormResult` のデータメンバーの値を取得して、オ `com.adobe.idp.services.holders.FormsResultHolder` ブジェクトを `value` 作成します。
   * オブジェクトの `BLOB` メソッドを呼び出して、フォームデータを含むオ `FormsResult` ブジェクトを作成 `getOutputContent` します。
   * メソッドを呼び出して、オブジェ `BLOB` クトのコンテンツタイプを取得 `getContentType` します。
   * メソッドを呼 `javax.servlet.http.HttpServletResponse` び出し、オブジェクトのコンテンツタ `setContentType` イプを渡すことで、オブジェクトのコンテンツタイプを設定 `BLOB` します。
   * オブジェクトの `javax.servlet.ServletOutputStream` メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに書き込むために使用する `javax.servlet.http.HttpServletResponse` オブジェクトを作 `getOutputStream` 成します。
   * バイト配列を作成し、オブジェクトのメソッドを呼び出 `BLOB` して値を設定 `getBinaryData` します。 このタスクは、オブジェクトの内容をバ `FormsResult` イト配列に割り当てます。
   * オブジェクト `javax.servlet.http.HttpServletResponse` のメソッドを呼び `write` 出して、フォームデータストリームをクライアントWebブラウザーに送信します。 バイト配列をメソッドに渡し `write` ます。

**関連トピック**

[カスタムCSSファイルを使用したHTMLフォームのレンダリング](#rendering-html-forms-using-custom-css-files)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
