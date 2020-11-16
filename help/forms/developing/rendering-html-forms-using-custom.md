---
title: カスタムCSSファイルを使用したHTMLFormsのレンダリング
seo-title: カスタムCSSファイルを使用したHTMLFormsのレンダリング
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
source-git-commit: fcbe1d860410e215cb7c438f94579e0b14d262a5
workflow-type: tm+mt
source-wordcount: '1640'
ht-degree: 2%

---


# カスタムCSSファイルを使用したHTMLFormsのレンダリング {#rendering-html-forms-using-custom-css-files}

Formsサービスは、WebブラウザーからのHTTP要求に応じてHTMLフォームをレンダリングします。 HTMLフォームをレンダリングする場合、FormsサービスはカスタムCSSファイルを参照できます。 Formsサービスを使用してHTMLフォームをレンダリングする場合、ビジネス要件に合ったカスタムCSSファイルを作成し、そのCSSファイルを参照することができます。

Formsサービスは、カスタムCSSファイルをサイレントに解析します。 つまり、Formsサービスは、カスタムCSSファイルがCSS標準に準拠していない場合に発生する可能性があるエラーを報告しません。 この場合、Formsサービスはスタイルを無視し、CSSファイル内の残りのスタイルを使用し続けます。

次のリストは、カスタムCSSファイルでサポートされるスタイルを指定します。

* **クラスレベルのセレクタースタイルのペア**:カスタムCSSファイルに存在する場合、HTMLフォームでクラススタイルとして使用されるセレクターが使用されます。 未使用のクラススタイルは無視されます。
* **識別子レベルのセレクタースタイルのペア**:HTMLフォームで使用される場合は、すべての識別子スタイルが使用されます。
* **要素レベルのセレクタースタイルのペア**:HTMLフォームで使用される場合は、すべての要素スタイルが使用されます。
* **Style Priority**:スタイルの優先度（重要など）はサポートされ、カスタムCSSファイルで使用できます。
* **メディアの種類**:1つ以上のセレクタースタイルのペアを@mediaスタイルでラップして、メディアの種類を定義できます。 Formsサービスは、指定されたメディアの種類がサポートされているかどうかを確認しません。 カスタムCSSファイルで指定されたメディアタイプがHTMLフォームに結合されます。

FormsIVSアプリケーションを使用して、サンプルのCSSファイルを取得できます。 フォームをアップロードし、Test Form Designページでフォームを選択して、「GenerateCSS」をクリックします。 ボタンをクリックする前に、HTML変換タイプを設定する必要はありません。 次に、「保存」を選択します。 このCSSファイルは、ビジネス要件に合わせて編集できます。

>[!NOTE]
>
>カスタムCSSファイルを使用するHTMLフォームをレンダリングする前に、HTMLフォームのレンダリングについてしっかりと理解しておくことが重要です。 (「FormsをHTMLとして [レンダリング」を参照](/help/forms/developing/rendering-forms-html.md))。

>[!NOTE]
>
>For more information about the Forms service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## 手順の概要 {#summary-of-steps}

CSSファイルを使用するHTMLフォームをレンダリングするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. FormsJava APIオブジェクトを作成します。
1. CSSファイルを参照します。
1. HTMLフォームをレンダリングする。
1. フォームデータストリームをクライアントのWebブラウザーに書き込みます。

**プロジェクトファイルを含める**

開発プロジェクトに必要なファイルを含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めてください。

**FormsJava APIオブジェクトの作成**

Formsサービスがサポートする操作をプログラムで実行する前に、Formsクライアントオブジェクトを作成する必要があります。

**CSSファイルの参照**

カスタムCSSファイルを使用するHTMLフォームをレンダリングするには、既存のCSSファイルを必ず参照してください。

**HTMLフォームのレンダリング**

HTMLフォームをレンダリングするには、Designerで作成し、XDPファイルとして保存するフォームデザインを指定する必要があります。 また、HTML変換タイプを選択する必要もあります。 例えば、Internet Explorer 5.0以降用の動的HTMLをレンダリングするHTML変換タイプを指定できます。

HTMLフォームのレンダリングには、他のフォームタイプのレンダリングに必要なURI値などの値も必要です。

**フォームデータストリームをクライアントのWebブラウザーに書き込みます**

Formsサービスは、HTMLフォームをレンダリングするときにフォームデータストリームを返します。このストリームをクライアントのWebブラウザーに書き込み、HTMLフォームをユーザーに表示させる必要があります。

**関連トピック**

[Java APIを使用してCSSファイルを使用するHTMLフォームをレンダリングする](#render-an-html-form-that-uses-a-css-file-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[FormsサービスAPIクイック開始](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[インタラクティブPDF formsのレンダリング](/help/forms/developing/rendering-interactive-pdf-forms.md)

[FormsをHTMLとしてレンダリング](/help/forms/developing/rendering-forms-html.md)

[FormsをレンダリングするWeb アプリケーションの作成](/help/forms/developing/creating-web-applications-renders-forms.md)

## Java APIを使用してCSSファイルを使用するHTMLフォームをレンダリングする {#render-an-html-form-that-uses-a-css-file-using-the-java-api}

FormsAPI(Java)を使用して、カスタムCSSファイルを使用するHTMLフォームをレンダリングします。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-forms-client.jarなどのクライアントJARファイルを含めます。

1. FormsJava APIオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `FormsServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. CSSファイルの参照

   * Create an `HTMLRenderSpec` object by using its constructor.
   * カスタムCSSファイルを使用するHTMLフォームをレンダリングするには、 `HTMLRenderSpec` オブジェクトの `setCustomCSSURI` メソッドを呼び出し、CSSファイルの場所と名前を指定する文字列値を渡します。

1. HTMLフォームのレンダリング

   オブジェクトの `FormsServiceClient``(Deprecated) (Deprecated) renderHTMLForm` メソッドを呼び出し、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定するstring値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、完全なパスを必ず指定してください（例：） `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * HTML環境設定タイプを指定する `TransformTo` enum値。 例えば、Internet Explorer 5.0以降用の動的HTMLと互換性のあるHTMLフォームをレンダリングするには、を指定し `TransformTo.MSDHTML`ます。
   * フォームとマージするデータを含む `com.adobe.idp.Document` オブジェクト。 データをマージしない場合は、空の `com.adobe.idp.Document` オブジェクトを渡します。
   * HTML実行時オプションを格納する `HTMLRenderSpec` オブジェクトです。
   * ヘッダー値を指定するstring値（例：） `HTTP_USER_AGENT``Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。
   * HTMLフォームのレンダリングに必要なURI値を格納する `URLSpec` オブジェクト。
   * 添付ファイルを格納する `java.util.HashMap` オブジェクトです。 これはオプションのパラメーターで、フォームにファイルを添付しない `null` かどうかを指定できます。

   この `(Deprecated) renderHTMLForm``FormsResult` メソッドは、クライアントのWebブラウザーに書き込む必要があるフォームデータストリームを含むオブジェクトを返します。

1. フォームデータストリームをクライアントのWebブラウザーに書き込みます

   * オブジェクトの `com.adobe.idp.Document` メソッドを呼び出して、 `FormsResult` オブジェクトを作成し `getOutputContent` ます。
   * メソッドを呼び出して、 `com.adobe.idp.Document` オブジェクトのコンテンツタイプを取得し `getContentType` ます。
   * メソッドを呼び出し、オブジェクトの `javax.servlet.http.HttpServletResponse` コンテンツタイプを渡すことで、 `setContentType``com.adobe.idp.Document` オブジェクトのコンテンツタイプを設定します。
   * オブジェクトの `javax.servlet.ServletOutputStream` メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに書き込むために使用する `javax.servlet.h\ttp.HttpServletResponse``getOutputStream` オブジェクトを作成します。
   * オブジェクトの `java.io.InputStream` メソッドを呼び出して、 `com.adobe.idp.Document` オブジェクトを作成 `getInputStream` します。
   * バイト配列を作成し、 `InputStream` オブジェクトの `read` メソッドを呼び出して、バイト配列を引数として渡すことで、フォームデータストリームを設定します。
   * オブジェクトの `javax.servlet.ServletOutputStream``write` メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに送信します。 バイト配列を `write` メソッドに渡します。

**関連トピック**

[カスタムCSSファイルを使用したHTMLFormsのレンダリング](#rendering-html-forms-using-custom-css-files)

[クイック開始（SOAPモード）:Java APIを使用したCSSファイルを使用したHTMLフォームのレンダリング](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-that-uses-a-css-file-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## WebサービスAPIを使用してCSSファイルを使用するHTMLフォームをレンダリングする {#render-an-html-form-that-uses-a-css-file-using-the-web-service-api}

FormsAPI（Webサービス）を使用して、カスタムCSSファイルを使用するHTMLフォームをレンダリングします。

1. プロジェクトファイルを含める

   * FormsサービスのWSDLを使用するJavaプロキシクラスを作成します。
   * クラスパスにJavaプロキシクラスを含めます。

1. FormsJava APIオブジェクトの作成

   オブジェクトを作成し、認証値を設定し `FormsService` ます。

1. CSSファイルの参照

   * Create an `HTMLRenderSpec` object by using its constructor.
   * カスタムCSSファイルを使用するHTMLフォームをレンダリングするには、 `HTMLRenderSpec` オブジェクトの `setCustomCSSURI` メソッドを呼び出し、CSSファイルの場所と名前を指定する文字列値を渡します。

1. HTMLフォームのレンダリング

   オブジェクトの `FormsService``(Deprecated) renderHTMLForm` メソッドを呼び出し、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定するstring値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、完全なパスを必ず指定してください（例：） `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * HTML環境設定タイプを指定する `TransformTo` enum値。 例えば、Internet Explorer 5.0以降用の動的HTMLと互換性のあるHTMLフォームをレンダリングするには、を指定し `TransformTo.MSDHTML`ます。
   * フォームとマージするデータを含む `BLOB` オブジェクト。 データを結合したくない場合は、を渡し `null`ます。 (編集可能なレイアウト [をFormsに自動埋め込むを参照](/help/forms/developing/prepopulating-forms-flowable-layouts.md))。
   * HTML実行時オプションを格納する `HTMLRenderSpec` オブジェクトです。
   * ヘッダー値を指定するstring値（例：） `HTTP_USER_AGENT``Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`。 この値を設定したくない場合は、空の文字列を渡すことができます。
   * HTMLフォームのレンダリングに必要なURI値を格納する `URLSpec` オブジェクト。
   * 添付ファイルを格納する `java.util.HashMap` オブジェクトです。 これはオプションのパラメーターで、フォームにファイルを添付しない `null` かどうかを指定できます。
   * メソッドによって入力される空の `com.adobe.idp.services.holders.BLOBHolder` オブジェクト `(Deprecated) renderHTMLForm` です。 このパラメーター値は、レンダリングされたフォームを保存します。
   * メソッドによって入力される空の `com.adobe.idp.services.holders.BLOBHolder` オブジェクト `(Deprecated) renderHTMLForm` です。 このパラメーターは、出力XMLデータを格納します。
   * メソッドによって入力される空の `javax.xml.rpc.holders.LongHolder` オブジェクト `(Deprecated) renderHTMLForm` です。 この引数は、フォームのページ数を格納します。
   * メソッドによって入力される空の `javax.xml.rpc.holders.StringHolder` オブジェクト `(Deprecated) renderHTMLForm` です。 この引数はロケールの値を格納します。
   * メソッドによって入力される空の `javax.xml.rpc.holders.StringHolder` オブジェクト `(Deprecated) renderHTMLForm` です。 この引数は、使用されるHTMLレンダリング値を格納します。
   * この操作の結果を含む空の `com.adobe.idp.services.holders.FormsResultHolder` オブジェクトです。

   この `(Deprecated) renderHTMLForm` メソッドは、最後の引数値として渡される `com.adobe.idp.services.holders.FormsResultHolder` オブジェクトに、クライアントWebブラウザーに書き込む必要があるフォームデータストリームを入力します。

1. フォームデータストリームをクライアントのWebブラウザーに書き込みます

   * オブジェクトの `FormResult` データメンバーの値を取得して `com.adobe.idp.services.holders.FormsResultHolder` オブジェクトを作成し `value` ます。
   * オブジェクトの `BLOB` メソッドを呼び出して、フォームデータを含む `FormsResult` オブジェクトを作成し `getOutputContent` ます。
   * メソッドを呼び出して、 `BLOB` オブジェクトのコンテンツタイプを取得し `getContentType` ます。
   * メソッドを呼び出し、オブジェクトの `javax.servlet.http.HttpServletResponse` コンテンツタイプを渡すことで、 `setContentType``BLOB` オブジェクトのコンテンツタイプを設定します。
   * オブジェクトの `javax.servlet.ServletOutputStream` メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに書き込むために使用する `javax.servlet.http.HttpServletResponse``getOutputStream` オブジェクトを作成します。
   * バイト配列を作成し、 `BLOB` オブジェクトの `getBinaryData` メソッドを呼び出して値を設定します。 このタスクは、 `FormsResult` オブジェクトの内容をバイト配列に割り当てます。
   * オブジェクトの `javax.servlet.http.HttpServletResponse``write` メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに送信します。 バイト配列を `write` メソッドに渡します。

**関連トピック**

[カスタムCSSファイルを使用したHTMLFormsのレンダリング](#rendering-html-forms-using-custom-css-files)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
