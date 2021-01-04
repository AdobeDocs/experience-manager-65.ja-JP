---
title: カスタムCSSファイルを使用したHTMLFormsのレンダリング
seo-title: カスタムCSSファイルを使用したHTMLFormsのレンダリング
description: Formsサービスを使用して、WebブラウザーからのHTTP要求に応答してHTMLフォームをレンダリングするカスタムCSSファイルを参照します。 Java APIとWeb Service APIを使用して、CSSファイルを使用するHTMLフォームをレンダリングできます。
seo-description: Formsサービスを使用して、WebブラウザーからのHTTP要求に応答してHTMLフォームをレンダリングするカスタムCSSファイルを参照します。 Java APIとWeb Service APIを使用して、CSSファイルを使用するHTMLフォームをレンダリングできます。
uuid: a44e96f1-001d-48a2-8c96-15cb9d0c71b3
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8fe7c072-7df0-44b7-92d0-bf39dc1e688a
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '1724'
ht-degree: 2%

---


# カスタムCSSファイルを使用したHTMLFormsのレンダリング{#rendering-html-forms-using-custom-css-files}

Formsサービスは、WebブラウザーからのHTTP要求に応じてHTMLフォームをレンダリングします。 HTMLフォームをレンダリングする場合、FormsサービスはカスタムCSSファイルを参照できます。 Formsサービスを使用してHTMLフォームをレンダリングする場合、ビジネス要件に合ったカスタムCSSファイルを作成し、そのCSSファイルを参照することができます。

Formsサービスは、カスタムCSSファイルをサイレントに解析します。 つまり、Formsサービスは、カスタムCSSファイルがCSS標準に準拠していない場合に発生する可能性があるエラーを報告しません。 この場合、Formsサービスはスタイルを無視し、CSSファイル内の残りのスタイルを使用し続けます。

次のリストは、カスタムCSSファイルでサポートされるスタイルを指定します。

* **クラスレベルのセレクタースタイルのペア**:カスタムCSSファイルに存在する場合、HTMLフォームでクラススタイルとして使用されるセレクターが使用されます。未使用のクラススタイルは無視されます。
* **識別子レベルのセレクタースタイルのペア**:HTMLフォームで使用される場合は、すべての識別子スタイルが使用されます。
* **要素レベルのセレクタースタイルのペア**:HTMLフォームで使用される場合は、すべての要素スタイルが使用されます。
* **Style Priority**:スタイルの優先度（重要など）はサポートされ、カスタムCSSファイルで使用できます。
* **メディアの種類**:1つ以上のセレクタースタイルのペアを@mediaスタイルでラップして、メディアの種類を定義できます。Formsサービスは、指定されたメディアの種類がサポートされているかどうかを確認しません。 カスタムCSSファイルで指定されたメディアタイプがHTMLフォームに結合されます。

FormsIVSアプリケーションを使用して、サンプルのCSSファイルを取得できます。 フォームをアップロードし、Test Form Designページでフォームを選択して、「GenerateCSS」をクリックします。 ボタンをクリックする前に、HTML変換タイプを設定する必要はありません。 次に、「保存」を選択します。 このCSSファイルは、ビジネス要件に合わせて編集できます。

>[!NOTE]
>
>カスタムCSSファイルを使用するHTMLフォームをレンダリングする前に、HTMLフォームのレンダリングについてしっかりと理解しておくことが重要です。 ([HTMLとしてのFormsのレンダリング](/help/forms/developing/rendering-forms-html.md)を参照)。

>[!NOTE]
>
>Formsサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

## 手順{#summary-of-steps}の概要

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

## Java API {#render-an-html-form-that-uses-a-css-file-using-the-java-api}を使用してCSSファイルを使用するHTMLフォームをレンダリングする

FormsAPI(Java)を使用して、カスタムCSSファイルを使用するHTMLフォームをレンダリングします。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-forms-client.jarなどのクライアントJARファイルを含めます。

1. FormsJava APIオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `FormsServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. CSSファイルの参照

   * コンストラクターを使用して`HTMLRenderSpec`オブジェクトを作成します。
   * カスタムCSSファイルを使用するHTMLフォームをレンダリングするには、`HTMLRenderSpec`オブジェクトの`setCustomCSSURI`メソッドを呼び出し、CSSファイルの場所と名前を指定する文字列値を渡します。

1. HTMLフォームのレンダリング

   `FormsServiceClient`オブジェクトの`(Deprecated) (Deprecated) renderHTMLForm`メソッドを呼び出し、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定するstring値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`など、完全なパスを必ず指定してください。
   * HTML環境設定の種類を指定する`TransformTo`列挙値。 例えば、Internet Explorer 5.0以降用の動的HTMLと互換性のあるHTMLフォームをレンダリングするには、`TransformTo.MSDHTML`を指定します。
   * フォームとマージするデータを含む`com.adobe.idp.Document`オブジェクト。 データをマージしない場合は、空の`com.adobe.idp.Document`オブジェクトを渡します。
   * HTML実行時オプションを格納する`HTMLRenderSpec`オブジェクト。
   * `HTTP_USER_AGENT`ヘッダー値を指定するstring値（`Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`など）。
   * HTMLフォームのレンダリングに必要なURI値を格納する`URLSpec`オブジェクト。
   * 添付ファイルを格納する`java.util.HashMap`オブジェクト。 これはオプションのパラメーターです。フォームにファイルを添付しない場合は、`null`を指定できます。

   `(Deprecated) renderHTMLForm`メソッドは、クライアントのWebブラウザーに書き込む必要があるフォームデータストリームを含む`FormsResult`オブジェクトを返します。

1. フォームデータストリームをクライアントのWebブラウザーに書き込みます

   * `FormsResult`オブジェクト&#39;s `getOutputContent`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトを作成します。
   * `getContentType`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトのコンテンツタイプを取得します。
   * `javax.servlet.http.HttpServletResponse`オブジェクトのコンテンツタイプを設定するには、`setContentType`メソッドを呼び出し、`com.adobe.idp.Document`オブジェクトのコンテンツタイプを渡します。
   * `javax.servlet.h\ttp.HttpServletResponse`オブジェクトの`getOutputStream`メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに書き込むために使用する`javax.servlet.ServletOutputStream`オブジェクトを作成します。
   * `com.adobe.idp.Document`オブジェクトの`getInputStream`メソッドを呼び出して、`java.io.InputStream`オブジェクトを作成します。
   * バイト配列を作成し、`InputStream`オブジェクトの`read`メソッドを呼び出して、バイト配列を引数として渡すことで、フォームデータストリームを設定します。
   * `javax.servlet.ServletOutputStream`オブジェクトの`write`メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに送信します。 バイト配列を`write`メソッドに渡します。

**関連トピック**

[カスタムCSSファイルを使用したHTMLFormsのレンダリング](#rendering-html-forms-using-custom-css-files)

[クイック開始（SOAPモード）:Java APIを使用したCSSファイルを使用したHTMLフォームのレンダリング](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-that-uses-a-css-file-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## WebサービスAPI {#render-an-html-form-that-uses-a-css-file-using-the-web-service-api}を使用してCSSファイルを使用するHTMLフォームをレンダリングする

FormsAPI（Webサービス）を使用して、カスタムCSSファイルを使用するHTMLフォームをレンダリングします。

1. プロジェクトファイルを含める

   * FormsサービスのWSDLを使用するJavaプロキシクラスを作成します。
   * クラスパスにJavaプロキシクラスを含めます。

1. FormsJava APIオブジェクトの作成

   `FormsService`オブジェクトを作成し、認証値を設定します。

1. CSSファイルの参照

   * コンストラクターを使用して`HTMLRenderSpec`オブジェクトを作成します。
   * カスタムCSSファイルを使用するHTMLフォームをレンダリングするには、`HTMLRenderSpec`オブジェクトの`setCustomCSSURI`メソッドを呼び出し、CSSファイルの場所と名前を指定する文字列値を渡します。

1. HTMLフォームのレンダリング

   `FormsService`オブジェクトの`(Deprecated) renderHTMLForm`メソッドを呼び出し、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定するstring値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`など、完全なパスを必ず指定してください。
   * HTML環境設定の種類を指定する`TransformTo`列挙値。 例えば、Internet Explorer 5.0以降用の動的HTMLと互換性のあるHTMLフォームをレンダリングするには、`TransformTo.MSDHTML`を指定します。
   * フォームとマージするデータを含む`BLOB`オブジェクト。 データを結合したくない場合は、`null`を渡します。 (「[編集可能なレイアウトでFormsを自動埋め込む](/help/forms/developing/prepopulating-forms-flowable-layouts.md)」を参照)。
   * HTML実行時オプションを格納する`HTMLRenderSpec`オブジェクト。
   * `HTTP_USER_AGENT`ヘッダー値を指定するstring値（`Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`など）。 この値を設定したくない場合は、空の文字列を渡すことができます。
   * HTMLフォームのレンダリングに必要なURI値を格納する`URLSpec`オブジェクト。
   * 添付ファイルを格納する`java.util.HashMap`オブジェクト。 これはオプションのパラメーターです。フォームにファイルを添付しない場合は、`null`を指定できます。
   * `(Deprecated) renderHTMLForm`メソッドによって入力される空の`com.adobe.idp.services.holders.BLOBHolder`オブジェクト。 このパラメーター値は、レンダリングされたフォームを保存します。
   * `(Deprecated) renderHTMLForm`メソッドによって入力される空の`com.adobe.idp.services.holders.BLOBHolder`オブジェクト。 このパラメーターは、出力XMLデータを格納します。
   * `(Deprecated) renderHTMLForm`メソッドによって入力される空の`javax.xml.rpc.holders.LongHolder`オブジェクト。 この引数は、フォームのページ数を格納します。
   * `(Deprecated) renderHTMLForm`メソッドによって入力される空の`javax.xml.rpc.holders.StringHolder`オブジェクト。 この引数はロケールの値を格納します。
   * `(Deprecated) renderHTMLForm`メソッドによって入力される空の`javax.xml.rpc.holders.StringHolder`オブジェクト。 この引数は、使用されるHTMLレンダリング値を格納します。
   * この操作の結果を含む空の`com.adobe.idp.services.holders.FormsResultHolder`オブジェクトです。

   `(Deprecated) renderHTMLForm`メソッドは、最後の引数値として渡される`com.adobe.idp.services.holders.FormsResultHolder`オブジェクトに、クライアントWebブラウザーに書き込む必要のあるフォームデータストリームを入力します。

1. フォームデータストリームをクライアントのWebブラウザーに書き込みます

   * `com.adobe.idp.services.holders.FormsResultHolder`オブジェクトの`value`データメンバの値を取得して、`FormResult`オブジェクトを作成します。
   * `FormsResult`オブジェクトの`getOutputContent`メソッドを呼び出して、フォームデータを含む`BLOB`オブジェクトを作成します。
   * `getContentType`メソッドを呼び出して、`BLOB`オブジェクトのコンテンツタイプを取得します。
   * `javax.servlet.http.HttpServletResponse`オブジェクトのコンテンツタイプを設定するには、`setContentType`メソッドを呼び出し、`BLOB`オブジェクトのコンテンツタイプを渡します。
   * `javax.servlet.http.HttpServletResponse`オブジェクトの`getOutputStream`メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに書き込むために使用する`javax.servlet.ServletOutputStream`オブジェクトを作成します。
   * バイト配列を作成し、`BLOB`オブジェクトの`getBinaryData`メソッドを呼び出して値を設定します。 このタスクは、`FormsResult`オブジェクトの内容をバイト配列に割り当てます。
   * `javax.servlet.http.HttpServletResponse`オブジェクトの`write`メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに送信します。 バイト配列を`write`メソッドに渡します。

**関連トピック**

[カスタムCSSファイルを使用したHTMLFormsのレンダリング](#rendering-html-forms-using-custom-css-files)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
