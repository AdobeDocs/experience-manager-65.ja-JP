---
title: 値によるフォームのレンダリング
seo-title: 値によるフォームのレンダリング
description: 'null'
seo-description: 'null'
uuid: b932cc54-662f-40ae-94e0-20ac82845f3b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: ddbb2b82-4c57-4845-a5be-2435902d312b
translation-type: tm+mt
source-git-commit: 66bfd6870b4c09dc2ca1b66058e0b9e040a71507

---


# 値によるフォームのレンダリング {#rendering-forms-by-value}

通常、Designerで作成されたフォームデザインは、Formsサービスへの参照によって渡されます。 フォームデザインは大きくなる場合があり、その結果、フォームデザインのバイトを値ごとにマーシャリングする必要がなくなるので、参照によって渡す方が効率的です。 また、Formsサービスは、フォームデザインをキャッシュして、キャッシュ時にフォームデザインを継続的に読み取る必要がないようにすることもできます。

フォームデザインにUUID属性が含まれている場合は、キャッシュされます。 UUID値は、すべてのフォームデザインで一意で、フォームを一意に識別するために使用されます。 値を使用してフォームをレンダリングする場合、フォームは繰り返し使用される場合にのみキャッシュされます。 ただし、フォームを繰り返し使用せず、一意である必要がある場合は、AEM Forms APIを使用して設定されたキャッシュオプションを使用してフォームをキャッシュしないようにすることができます。

また、Formsサービスは、フォームデザイン内のリンクされたコンテンツの場所を解決することもできます。 例えば、フォームデザイン内から参照されるリンク画像は、相対URLです。 リンクされたコンテンツは、常にフォームデザインの場所に対する相対コンテンツと見なされます。 したがって、リンクされたコンテンツを解決するには、フォームデザインの絶対パスを適用して、その場所を決定する必要があります。

参照によってフォームデザインを渡す代わりに、フォームデザインを値で渡すことができます。 フォームデザインを動的に作成する場合、値を使用してフォームデザインを渡す方法が効率的です。つまり、クライアントアプリケーションが実行時にフォームデザインを作成するXMLを生成する場合です。 この場合、フォームデザインはメモリに保存されるので、物理リポジトリに保存されません。 実行時に動的にフォームデザインを作成し、値を渡す場合、フォームをキャッシュして、Formsサービスのパフォーマンスを向上させることができます。

**値でフォームを渡す場合の制限**

フォームデザインが値によって渡される場合、次の制限が適用されます。

* フォームデザイン内に相対リンクコンテンツを含めることはできません。 すべての画像とフラグメントは、フォームデザイン内に埋め込むか、絶対参照する必要があります。
* フォームのレンダリング後は、サーバー側の計算を実行できません。 フォームがFormsサービスに送り返される場合、データは抽出され、サーバー側の計算なしで返されます。
* HTMLでは、リンクされた画像を実行時にのみ使用できるので、埋め込まれた画像を使用してHTMLを生成することはできません。 これは、Formsサービスで、参照先のフォームデザインから画像を取得することで、HTMLを使用した埋め込み画像がサポートされるためです。 値によって渡されるフォームデザインには参照先がないので、HTMLページが表示されている場合は埋め込み画像を抽出できません。 したがって、画像参照は、HTMLでレンダリングされる絶対パスである必要があります。

>[!NOTE]
>
>様々な種類のフォーム（HTMLフォームや使用権限を含むフォームなど）を値ごとにレンダリングできますが、この節ではインタラクティブPDFフォームのレンダリングについて説明します。

>[!NOTE]
>
>For more information about the Forms service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## 手順の概要 {#summary-of-steps}

フォームを値でレンダリングするには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. フォームクライアントAPIオブジェクトを作成します。
1. フォームデザインを参照します。
1. 値でフォームをレンダリングします。
1. フォームデータストリームをクライアントのWebブラウザーに書き込みます。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

**フォームクライアントAPIオブジェクトの作成**

プログラムによってデータをPDFフォームのクライアントAPIに読み込む前に、Data Integrationサービスクライアントを作成する必要があります。 サービスクライアントを作成する場合、サービスの呼び出しに必要な接続設定を定義します。

**フォームデザインの参照**

値を使用してフォームをレンダリングする場合、レンダリングするフォームデザ `com.adobe.idp.Document` インを含むオブジェクトを作成する必要があります。 既存のXDPファイルを参照するか、実行時にフォームデザインを動的に作成し、そのデータをに埋め込むこ `com.adobe.idp.Document` とができます。

>[!NOTE]
>
>この節と対応するクイック開始は、既存のXDPファイルを参照します。

**値によるフォームのレンダリング**

フォームを値でレンダリングするには、フォームデザインを含むインスタンスをレンダリングメソッドのパラメーターに渡します( `com.adobe.idp.Document` 、などのオブジェクトのレンダリングメソッドの `inDataDoc` いずれかを指定で `FormsServiceClient``renderPDFForm``(Deprecated) renderHTMLForm`きます)。 このパラメーター値は、通常、フォームにマージされるデータ用に予約されます。 同様に、空の文字列値をパラメーターに渡し `formQuery` ます。 通常、このパラメーターには、フォームデザインの名前を指定する文字列値が必要です。

>[!NOTE]
>
>フォーム内にデータを表示する場合は、要素内でデータを指定する必要があり `xfa:datasets` ます。 XFAアーキテクチャについて詳しくは、https://partners.adobe.com/public/developer/xml/index_arch.htmlを参照して [ください](https://partners.adobe.com/public/developer/xml/index_arch.html)。

**フォームデータストリームをクライアントWebブラウザーに書き込む**

Formsサービスは、値を使用してフォームをレンダリングする場合、フォームデータストリームを返します。このストリームは、クライアントのWebブラウザーに書き込む必要があります。 クライアントのWebブラウザーに書き込むと、フォームはユーザーに表示されます。

**関連トピック**

[Java APIを使用した値によるフォームのレンダリング](#render-a-form-by-value-using-the-java-api)

[WebサービスAPIを使用した値によるフォームのレンダリング](#render-a-form-by-value-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[FormsサービスAPIのクイック開始](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Formsサービスへのドキュメントの引き渡し](/help/forms/developing/passing-documents-forms-service.md)

[フォームをレンダリングするWeb アプリケーションの作成](/help/forms/developing/creating-web-applications-renders-forms.md)

## Java APIを使用した値によるフォームのレンダリング {#render-a-form-by-value-using-the-java-api}

Forms API (Java)を使用して値でフォームをレンダリングする：

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-forms-client.jarなどのクライアントJARファイルを含めます。

1. フォームクライアントAPIオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `FormsServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. フォームデザインの参照

   * コンストラクター `java.io.FileInputStream` を使用し、XDPファイルの場所を指定するstring値を渡して、レンダリングするフォームデザインを表すオブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 値によるフォームのレンダリング

   オブジェクト `FormsServiceClient` のメソッドを `renderPDFForm` 呼び出し、次の値を渡します。

   * 空の文字列値。 （通常、このパラメーターには、フォームデザインの名前を指定する文字列値が必要です）。
   * フォーム `com.adobe.idp.Document` デザインを含むオブジェクトです。 通常、このパラメーター値は、フォームにマージされるデータ用に予約されます。
   * 実行時 `PDFFormRenderSpec` のオプションを格納するオブジェクト。 これはオプションのパラメーターで、実行時 `null` のオプションを指定しないかどうかを指定できます。
   * Formsサ `URLSpec` ービスで必要なURI値を含むオブジェクトです。
   * 添付ファ `java.util.HashMap` イルを格納するオブジェクト。 これはオプションのパラメーターで、フォームにフ `null` ァイルを添付しないかどうかを指定できます。
   このメソ `renderPDFForm` ッドは、クラ `FormsResult` イアントのWebブラウザーに書き込み可能なフォームデータストリームを含むオブジェクトを返します。

1. フォームデータストリームをクライアントWebブラウザーに書き込む

   * オブジェクトの `com.adobe.idp.Document` メソッドを呼び出して、オ `FormsResult` ブジェクトを作成 `getOutputContent` します。
   * メソッドを呼び出して、オブジェ `com.adobe.idp.Document` クトのコンテンツタイプを取 `getContentType` 得します。
   * メソッドを呼 `javax.servlet.http.HttpServletResponse` び出し、オブジェクトのコンテ `setContentType` ンツタイプを渡して、オブジェクトのコンテンツタイプを設定 `com.adobe.idp.Document` します。
   * オブジェクトの `javax.servlet.ServletOutputStream` メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに書き込むために使用す `javax.servlet.http.HttpServletResponse` るオブジェクトを作成 `getOutputStream` します。
   * オブジェクトの `java.io.InputStream` メソッドを呼び出して、オ `com.adobe.idp.Document` ブジェクトを作成 `getInputStream` します。
   * バイト配列を作成し、オブジェクトのサイズを割り当て `InputStream` ます。 オブジェクト `InputStream` のメソッドを `available` 呼び出して、オブジェクトのサイズを取得 `InputStream` します。
   * オブジェクトのメソッドを呼び出し、バイト配列を引数とし `InputStream` て渡すことによ `read`り、バイト配列にフォームデータストリームを設定します。
   * オブジェクト `javax.servlet.ServletOutputStream` のメソッドを呼 `write` び出して、フォームデータストリームをクライアントWebブラウザーに送信します。 バイト配列をメソッドに渡し `write` ます。

**関連トピック**

[値によるフォームのレンダリング](/help/forms/developing/rendering-forms.md)

[クイック開始（SOAPモード）:Java APIを使用した値によるレンダリング](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-by-value-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## WebサービスAPIを使用した値によるフォームのレンダリング {#render-a-form-by-value-using-the-web-service-api}

Forms API（Webサービス）を使用して値でフォームをレンダリングします。

1. プロジェクトファイルを含める

   * FormsサービスのWSDLを使用するJavaプロキシクラスを作成します。
   * クラスパスにJavaプロキシクラスを含めます。

1. フォームクライアントAPIオブジェクトの作成

   オブジェクトを `FormsService` 作成し、認証値を設定します。

1. フォームデザインの参照

   * コンストラクタを使用して `java.io.FileInputStream` オブジェクトを作成します。XDPファイルの場所を指定するstring値を渡します。
   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、パスワードで暗号化されたPDFドキュメントの保存に使用されます。
   * オブジェクトの内容を格納するバイト配列を作成 `java.io.FileInputStream` します。 バイト配列のサイズは、そのメソッドを使用してオブジェ `java.io.FileInputStream` クトのサイズを取得することで決定で `available` きます。
   * オブジェクトのメソッドを呼び出し、バイト配列を渡すこ `java.io.FileInputStream` とで、バイト配 `read` 列にストリームデータを入力します。
   * メソッドを呼び `BLOB` 出し、バイト配列を渡 `setBinaryData` すことで、オブジェクトを入力します。

1. 値によるフォームのレンダリング

   オブジェクト `FormsService` のメソッドを `renderPDFForm` 呼び出し、次の値を渡します。

   * 空の文字列値。 （通常、このパラメーターには、フォームデザインの名前を指定する文字列値が必要です）。
   * フォーム `BLOB` デザインを含むオブジェクトです。 通常、このパラメーター値は、フォームにマージされるデータ用に予約されます。
   * 実行時 `PDFFormRenderSpec` のオプションを格納するオブジェクト。 これはオプションのパラメーターで、実行時 `null` のオプションを指定しないかどうかを指定できます。
   * Formsサ `URLSpec` ービスで必要なURI値を含むオブジェクトです。
   * 添付ファ `java.util.HashMap` イルを格納するオブジェクト。 これはオプションのパラメーターで、フォームにフ `null` ァイルを添付しないかどうかを指定できます。
   * メソッドに `com.adobe.idp.services.holders.BLOBHolder` よって入力される空のオブジェクトです。 これは、レンダリングされたPDFフォームを保存するために使用されます。
   * メソッドに `javax.xml.rpc.holders.LongHolder` よって入力される空のオブジェクトです。 （この引数は、フォームのページ数を格納します）。
   * メソッドに `javax.xml.rpc.holders.StringHolder` よって入力される空のオブジェクトです。 （この引数はロケールの値を格納します）。
   * この操作の `com.adobe.idp.services.holders.FormsResultHolder` 結果を含む空のオブジェクトです。
   メソッド `renderPDFForm` は、最後の引 `com.adobe.idp.services.holders.FormsResultHolder` 数として渡されたオブジェクトに、クライアントWebブラウザーに書き込む必要のあるフォームデータストリームを設定します。

1. フォームデータストリームをクライアントWebブラウザーに書き込む

   * オブジェクト `FormResult` のデータメンバーの値を取得して、オ `com.adobe.idp.services.holders.FormsResultHolder` ブジェクトを `value` 作成します。
   * オブジェクトの `BLOB` メソッドを呼び出して、フォームデータを含む `FormsResult` オブジェクトを作成 `getOutputContent` します。
   * メソッドを呼び出して、オブジェ `BLOB` クトのコンテンツタイプを取 `getContentType` 得します。
   * メソッドを呼 `javax.servlet.http.HttpServletResponse` び出し、オブジェクトのコンテ `setContentType` ンツタイプを渡して、オブジェクトのコンテンツタイプを設定 `BLOB` します。
   * オブジェクトの `javax.servlet.ServletOutputStream` メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに書き込むために使用す `javax.servlet.http.HttpServletResponse` るオブジェクトを作成 `getOutputStream` します。
   * バイト配列を作成し、オブジェクトのメソッドを呼び出 `BLOB` して値を設定 `getBinaryData` します。 このタスクは、オブジェクトの内容をバ `FormsResult` イト配列に割り当てます。
   * オブジェクト `javax.servlet.http.HttpServletResponse` のメソッドを呼 `write` び出して、フォームデータストリームをクライアントWebブラウザーに送信します。 バイト配列をメソッドに渡し `write` ます。

**関連トピック**

[値によるフォームのレンダリング](#rendering-forms-by-value)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
