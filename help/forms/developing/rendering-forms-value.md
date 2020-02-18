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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 値によるフォームのレンダリング {#rendering-forms-by-value}

通常、Designerで作成されたフォームデザインは、Formsサービスへの参照によって渡されます。 フォームデザインは大きくなる場合があり、その結果、フォームデザインのバイトを値ごとにマーシャリングする必要がなくなるので、参照によって渡す方が効率的です。 また、Formsサービスは、フォームデザインをキャッシュして、キャッシュ時にフォームデザインを継続的に読み取る必要がないようにすることもできます。

フォームデザインにUUID属性が含まれる場合は、キャッシュされます。 UUID値は、すべてのフォームデザインで一意で、フォームを一意に識別するために使用されます。 値を指定してフォームをレンダリングする場合、フォームを繰り返し使用する場合にのみキャッシュする必要があります。 ただし、繰り返し使用されず一意である必要がある場合は、AEM Forms APIを使用して設定されたキャッシュオプションを使用してフォームをキャッシュするのを避けることができます。

また、Formsサービスは、フォームデザイン内のリンクされたコンテンツの場所を解決することもできます。 例えば、フォームデザイン内から参照されるリンク画像は、相対URLです。 リンクされたコンテンツは、常にフォームデザインの場所に対する相対コンテンツと見なされます。 したがって、リンクされたコンテンツを解決するには、フォームデザインの絶対位置に相対パスを適用して位置を決定する必要があります。

フォームデザインを参照渡しにする代わりに、値でフォームデザインを渡すことができます。 フォームデザインを動的に作成する場合、値を使用してフォームデザインを渡す方法が効率的です。つまり、クライアントアプリケーションが実行時にフォームデザインを作成するXMLを生成する場合です。 この場合、フォームデザインはメモリに保存されるので、物理リポジトリに保存されません。 実行時にフォームデザインを動的に作成し、値で渡す場合は、フォームをキャッシュして、Formsサービスのパフォーマンスを向上させることができます。

**値によるフォームの受け渡しの制限**

フォームデザインが値によって渡される場合、次の制限が適用されます。

* フォームデザイン内に相対リンクコンテンツを含めることはできません。 すべての画像とフラグメントは、フォームデザイン内に埋め込むか、絶対に参照する必要があります。
* フォームのレンダリング後は、サーバー側の計算を実行できません。 フォームがFormsサービスに返送されると、データは抽出され、サーバー側の計算なしで返されます。
* HTMLは実行時にリンクされた画像のみを使用できるので、埋め込まれた画像を含むHTMLを生成することはできません。 これは、Formsサービスが、参照先のフォームデザインから画像を取得することによって、HTMLに埋め込まれた画像をサポートするからです。 値によって渡されるフォームデザインに参照先がないので、HTMLページが表示されている場合は埋め込み画像を抽出できません。 したがって、画像参照は、HTMLでレンダリングする絶対パスである必要があります。

>[!NOTE]
>
>様々な種類のフォームを値でレンダリングできますが（例えば、HTMLフォームや使用権限を含むフォーム）、この節ではインタラクティブPDFフォームのレンダリングについて説明します。

>[!NOTE]
>
>For more information about the Forms service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## 手順の概要 {#summary-of-steps}

フォームを値でレンダリングするには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. フォームクライアントAPIオブジェクトを作成します。
1. フォームデザインを参照します。
1. 値でフォームをレンダリングします。
1. クライアントのWebブラウザーにフォームデータストリームを書き込みます。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

**フォームクライアントAPIオブジェクトの作成**

プログラムでデータをPDFフォームのクライアントAPIに読み込む前に、Data Integrationサービスクライアントを作成する必要があります。 サービスクライアントを作成する場合は、サービスの呼び出しに必要な接続設定を定義します。

**フォームデザインの参照**

値を指定してフォームをレンダリングする場合は、レンダリングするフォームデザ `com.adobe.idp.Document` インを含むオブジェクトを作成する必要があります。 既存のXDPファイルを参照することも、実行時にフォームデザインを動的に作成して、そのデータをに埋め込むこ `com.adobe.idp.Document` ともできます。

>[!NOTE]
>
>この節と対応するクイックスタートは、既存のXDPファイルを参照します。

**値によるフォームのレンダリング**

フォームを値でレンダリングするには、フォームデザインを含むインスタンスを `com.adobe.idp.Document` renderメソッドのパラメーターに渡します(オブジェクトのレンダリングメソッド( `inDataDoc` 、 `FormsServiceClient` など `renderPDFForm``(Deprecated) renderHTMLForm`)。 このパラメーター値は通常、フォームにマージされるデータ用に予約されます。 同様に、パラメーターに空の文字列値を渡し `formQuery` ます。 通常、このパラメーターには、フォームデザインの名前を指定する文字列値が必要です。

>[!NOTE]
>
>フォーム内にデータを表示する場合は、要素内でデータを指定する必要があり `xfa:datasets` ます。 XFAアーキテクチャについて詳しくは、https://partners.adobe.com/public/developer/xml/index_arch.htmlを参照して [ください](https://partners.adobe.com/public/developer/xml/index_arch.html)。

**クライアントのWebブラウザーにフォームデータストリームを書き込みます**

Formsサービスは、値に基づいてフォームをレンダリングする場合、クライアントのWebブラウザーに書き込む必要があるフォームデータストリームを返します。 クライアントのWebブラウザーに書き込むと、フォームがユーザーに表示されます。

**関連トピック**

[Java APIを使用した値によるフォームのレンダリング](#render-a-form-by-value-using-the-java-api)

[WebサービスAPIを使用して値でフォームをレンダリングする](#render-a-form-by-value-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[FormsサービスAPIのクイックスタート](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Formsサービスへのドキュメントの引き渡し](/help/forms/developing/passing-documents-forms-service.md)

[フォームをレンダリングするWebアプリケーションの作成](/help/forms/developing/creating-web-applications-renders-forms.md)

## Java APIを使用した値によるフォームのレンダリング {#render-a-form-by-value-using-the-java-api}

Forms API(Java)を使用して値でフォームをレンダリングします。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-forms-client.jarなどのクライアントJARファイルを含めます。

1. フォームクライアントAPIオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `FormsServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. フォームデザインの参照

   * コンストラ `java.io.FileInputStream` クターを使用し、XDPファイルの場所を指定するstring値を渡して、レンダリングするフォームデザインを表すオブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 値によるフォームのレンダリング

   オブジェクト `FormsServiceClient` のメソッドを `renderPDFForm` 呼び出し、次の値を渡します。

   * 空の文字列値。 （通常、このパラメーターにはフォームデザインの名前を指定するstring値が必要です）。
   * フォーム `com.adobe.idp.Document` デザインを含むオブジェクトです。 通常、このパラメーター値はフォームにマージされるデータ用に予約されます。
   * 実行時 `PDFFormRenderSpec` のオプションを格納するオブジェクトです。 これはオプションのパラメーターで、実行時 `null` のオプションを指定しないかどうかを指定できます。
   * Formsサ `URLSpec` ービスに必要なURI値を含むオブジェクトです。
   * 添付フ `java.util.HashMap` ァイルを格納するオブジェクト。 これはオプションのパラメーターで、フォームにフ `null` ァイルを添付しないかどうかを指定できます。
   このメソ `renderPDFForm` ッドは、クライア `FormsResult` ントのWebブラウザーに書き込み可能なフォームデータストリームを含むオブジェクトを返します。

1. クライアントのWebブラウザーにフォームデータストリームを書き込みます

   * オブジェクトの `com.adobe.idp.Document` メソッドを呼び出して、オ `FormsResult` ブジェクトを作成 `getOutputContent` します。
   * メソッドを呼び出して、オブジェ `com.adobe.idp.Document` クトのコンテンツタイプを取得 `getContentType` します。
   * メソッドを呼 `javax.servlet.http.HttpServletResponse` び出し、オブジェクトのコンテンツタ `setContentType` イプを渡すことで、オブジェクトのコンテンツタイプを設定 `com.adobe.idp.Document` します。
   * オブジェクトの `javax.servlet.ServletOutputStream` メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに書き込むために使用する `javax.servlet.http.HttpServletResponse` オブジェクトを作 `getOutputStream` 成します。
   * オブジェクト `java.io.InputStream` のメソッドを呼び出して、オ `com.adobe.idp.Document` ブジェクトを作成 `getInputStream` します。
   * バイト配列を作成し、オブジェクトのサイズを割り当て `InputStream` ます。 オブジェクト `InputStream` のメソッドを呼 `available` び出して、オブジェクトのサイズを取得 `InputStream` します。
   * オブジェクトのメソッドを呼び出し、バイト配列を引数として渡すこ `InputStream` とで、バイ `read`ト配列にフォームデータストリームを設定します。
   * オブジェクト `javax.servlet.ServletOutputStream` のメソッドを呼び `write` 出して、フォームデータストリームをクライアントWebブラウザーに送信します。 バイト配列をメソッドに渡し `write` ます。

**関連トピック**

[フォームの値別レンダリング](/help/forms/developing/rendering-forms-rendering-forms rendering-forms-value-rendering-forms.md#rendering-forms-by-value)

[クイックスタート（SOAPモード）:Java APIを使用した値によるレンダリング](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-by-value-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## WebサービスAPIを使用して値でフォームをレンダリングする {#render-a-form-by-value-using-the-web-service-api}

Forms API（Webサービス）を使用して値でフォームをレンダリングします。

1. プロジェクトファイルを含める

   * FormsサービスWSDLを使用するJavaプロキシクラスを作成します。
   * クラスパスにJavaプロキシクラスを含めます。

1. フォームクライアントAPIオブジェクトの作成

   オブジェクト `FormsService` を作成し、認証値を設定します。

1. フォームデザインの参照

   * コンストラクタを使用して `java.io.FileInputStream` オブジェクトを作成します。XDPファイルの場所を指定するstring値を渡します。
   * コンストラクタを使用して `BLOB` オブジェクトを作成します。このオ `BLOB` ブジェクトは、パスワードで暗号化されたPDFドキュメントを保存するために使用されます。
   * オブジェクトのコンテンツを格納するバイト配列を作成 `java.io.FileInputStream` します。 バイト配列のサイズは、そのメソッドを使用してオブジェクトのサ `java.io.FileInputStream` イズを取得することで決定で `available` きます。
   * オブジェクトのメソッドを呼び出し、バイト配列を渡すこ `java.io.FileInputStream` とで、バイト配列 `read` にストリームデータを設定します。
   * メソッドを呼び `BLOB` 出し、バイト配列を渡すこ `setBinaryData` とで、オブジェクトを設定します。

1. 値によるフォームのレンダリング

   オブジェクト `FormsService` のメソッドを `renderPDFForm` 呼び出し、次の値を渡します。

   * 空の文字列値。 （通常、このパラメーターにはフォームデザインの名前を指定するstring値が必要です）。
   * フォーム `BLOB` デザインを含むオブジェクトです。 通常、このパラメーター値はフォームにマージされるデータ用に予約されます。
   * 実行時 `PDFFormRenderSpec` のオプションを格納するオブジェクトです。 これはオプションのパラメーターで、実行時 `null` のオプションを指定しないかどうかを指定できます。
   * Formsサ `URLSpec` ービスに必要なURI値を含むオブジェクトです。
   * 添付フ `java.util.HashMap` ァイルを格納するオブジェクト。 これはオプションのパラメーターで、フォームにフ `null` ァイルを添付しないかどうかを指定できます。
   * メソッドに `com.adobe.idp.services.holders.BLOBHolder` よって入力される空のオブジェクトです。 これは、レンダリングされたPDFフォームを保存するために使用します。
   * メソッドに `javax.xml.rpc.holders.LongHolder` よって入力される空のオブジェクトです。 （この引数は、フォーム内のページ数を格納します）。
   * メソッドに `javax.xml.rpc.holders.StringHolder` よって入力される空のオブジェクトです。 （この引数はロケールの値を格納します）。
   * この操作 `com.adobe.idp.services.holders.FormsResultHolder` の結果を含む空のオブジェクトです。
   メソッド `renderPDFForm` は、最後の引 `com.adobe.idp.services.holders.FormsResultHolder` 数値として渡されたオブジェクトに、クライアントWebブラウザーに書き込む必要があるフォームデータストリームを入力します。

1. クライアントのWebブラウザーにフォームデータストリームを書き込みます

   * オブジェクト `FormResult` のデータメンバーの値を取得して、オ `com.adobe.idp.services.holders.FormsResultHolder` ブジェクトを `value` 作成します。
   * オブジェクトの `BLOB` メソッドを呼び出して、フォームデータを含むオ `FormsResult` ブジェクトを作成 `getOutputContent` します。
   * メソッドを呼び出して、オブジェ `BLOB` クトのコンテンツタイプを取得 `getContentType` します。
   * メソッドを呼 `javax.servlet.http.HttpServletResponse` び出し、オブジェクトのコンテンツタ `setContentType` イプを渡すことで、オブジェクトのコンテンツタイプを設定 `BLOB` します。
   * オブジェクトの `javax.servlet.ServletOutputStream` メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに書き込むために使用する `javax.servlet.http.HttpServletResponse` オブジェクトを作 `getOutputStream` 成します。
   * バイト配列を作成し、オブジェクトのメソッドを呼び出 `BLOB` して値を設定 `getBinaryData` します。 このタスクは、オブジェクトの内容をバ `FormsResult` イト配列に割り当てます。
   * オブジェクト `javax.servlet.http.HttpServletResponse` のメソッドを呼び `write` 出して、フォームデータストリームをクライアントWebブラウザーに送信します。 バイト配列をメソッドに渡し `write` ます。

**関連トピック**

[値によるフォームのレンダリング](#rendering-forms-by-value)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
