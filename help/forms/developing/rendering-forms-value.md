---
title: 値別に Forms をレンダリング
seo-title: Rendering Forms By Value
description: Forms API（Java）を使用して、Java API および web サービス API を使用して値でフォームをレンダリングします。
seo-description: Use the Forms API (Java) to render a form by value using the Java API and Web Service API.
uuid: b932cc54-662f-40ae-94e0-20ac82845f3b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: ddbb2b82-4c57-4845-a5be-2435902d312b
role: Developer
exl-id: a3a6a06d-ec90-4147-a5f0-e776a086ee12
source-git-commit: 0c7dba43dad8608b4a5de271e1e44942c950fb16
workflow-type: ht
source-wordcount: '1835'
ht-degree: 100%

---

# 値別に Forms をレンダリング {#rendering-forms-by-value}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

通常、Designer で作成されたフォームデザインは、参照によって Forms サービスに渡されます。 フォームデザインは大きくなる可能性があり、その結果、フォームデザインのバイトを値でマーシャリングする必要がなくなるよう、参照で渡す方がより効率的です。 また、Forms サービスは、キャッシュ時にフォームデザインを継続的に読み取る必要がないように、フォームデザインをキャッシュすることもできます。

フォームデザインに UUID 属性が含まれている場合は、キャッシュされます。 UUID 値は、すべてのフォームデザインで一意であり、フォームを一意に識別するために使用されます。 値でフォームをレンダリングする場合、繰り返し使用する場合にのみフォームをキャッシュする必要があります。 ただし、フォームを繰り返し使用せず、一意にする必要がある場合は、AEM Forms API で設定されたキャッシュオプションを使用して、フォームをキャッシュするのを避けることができます。

Forms サービスは、フォームデザイン内のリンクされたコンテンツの場所を解決することもできます。 例えば、フォームデザイン内で参照されるリンク画像は、相対 URL です。 リンクされたコンテンツは、常にフォームデザインの場所を基準とした相対コンテンツと見なされます。 したがって、リンクされたコンテンツを解決するには、フォームデザインの絶対パスを適用して、その場所を決定する必要があります。

参照によってフォームデザインを渡す代わりに、値でフォームデザインを渡すことができます。 フォームデザインを動的に作成する場合、値でフォームデザインを渡すと効率的です。つまり、クライアントアプリケーションが実行時にフォームデザインを作成する XML を生成する場合です。 この場合、フォームデザインはメモリに保存されるので、物理リポジトリに保存されません。 実行時に動的にフォームデザインを作成し、値で渡す場合は、フォームをキャッシュして、Forms サービスのパフォーマンスを向上させることができます。

**値によるフォームの受け渡しの制限**

フォームデザインが値で渡される場合は、次の制限が適用されます。

* フォームデザイン内に相対的にリンクされたコンテンツを含めることはできません。 すべての画像とフラグメントは、フォームデザイン内に埋め込むか、絶対に参照する必要があります。
* フォームのレンダリング後は、サーバーサイドの計算を実行できません。 フォームが Forms サービスに送り返されると、データが抽出され、サーバーサイドの計算なしで返されます。
* HTML は実行時にのみリンク画像を使用できるので、埋め込まれた画像を使用して HTML を生成することはできません。 これは、Forms サービスが参照先のフォームデザインから画像を取得することで、HTML での埋め込み画像をサポートしているためです。 値で渡されたフォームデザインには参照先がないので、HTML ページが表示されているときに埋め込み画像を抽出することはできません。 したがって、画像参照は、HTML でレンダリングする絶対パスにする必要があります。

>[!NOTE]
>
>異なる種類のフォームを値でレンダリングすることもできます（例えば、HTML フォームや、使用権限を含むフォーム）がありますが、このセクションでは、インタラクティブ PDF forms のレンダリングについて説明します。

>[!NOTE]
>
>AEM Forms サービスについて詳しくは、[AEM Forms サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

## 手順の概要 {#summary-of-steps}

値でフォームをレンダリングするには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Forms Client API オブジェクトを作成します。
1. フォームデザインを保存します。
1. 値でフォームをレンダリングします。
1. フォームデータストリームをクライアントの Web ブラウザーに書き込みます。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めるようにします。

**Forms Client API オブジェクトの作成**

プログラムによってデータを PDF form クライアント API に読み込む前に、Data Integration Service クライアントを作成する必要があります。 サービスクライアントを作成する場合、サービスを呼び出すために必要な接続設定を定義します。

**フォームデザインの参照**

値でフォームをレンダリングする場合は、レンダリングするフォームデザインを含む `com.adobe.idp.Document` オブジェクトを作成する必要があります。既存の XDP ファイルを参照することも、実行時にフォームデザインを動的に作成してそのデータを `com.adobe.idp.Document` に入力することもできます。

>[!NOTE]
>
>このセクションと対応するクイックスタートでは、既存の XDP ファイルを参照します。

**値でフォームをレンダリング**

値でフォームをレンダリングするには、フォームデザインを含む `com.adobe.idp.Document` インスタンスをレンダリングメソッドの `inDataDoc` パラメーターに渡します（`renderPDFForm`、`(Deprecated) renderHTMLForm` など、`FormsServiceClient` オブジェクトのレンダリングメソッドのいずれでもかまいません）。このパラメーター値は、通常、フォームと結合されるデータ用に予約されます。同様に、空の文字列値を `formQuery` パラメーターに渡します。通常、このパラメーターにはフォームデザインの名前を指定する文字列値が必要です。

>[!NOTE]
>
>フォーム内にデータを表示する場合は、データは `xfa:datasets` 要素内で指定する必要があります。XFA アーキテクチャについて詳しくは、[https://www.pdfa.org/norm-refs/XFA-3_3.pdf](https://www.pdfa.org/norm-refs/XFA-3_3.pdf)を参照してください。

**フォームデータストリームをクライアントの web ブラウザーに書き込む**

Forms サービスがフォームを値でレンダリングすると、クライアントの web ブラウザーに書き込む必要のあるフォームデータストリームが返されます。クライアント Web ブラウザーに書き込まれると、フォームはユーザーに対して表示されます。

**関連トピック**

[Java API を使用して値でフォームをレンダリング](#render-a-form-by-value-using-the-java-api)

[Web サービス API を使用して値でフォームをレンダリング](#render-a-form-by-value-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms サービス API のクイックスタート](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Forms サービスにドキュメントを渡す](/help/forms/developing/passing-documents-forms-service.md)

[Forms をレンダリングする web アプリケーションの作成](/help/forms/developing/creating-web-applications-renders-forms.md)

## Java API を使用して値でフォームをレンダリング {#render-a-form-by-value-using-the-java-api}

Forms API（Java）を使用して値でフォームをレンダリング：

1. プロジェクトファイルを含める

   adobe-forms-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. Forms Client API オブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して `ServiceClientFactory` オブジェクトを渡し、`FormsServiceClient` オブジェクトを作成します。

1. フォームデザインの参照

   * コンストラクターを使用して、XDP ファイルの場所を指定する文字列の値を渡すことにより、レンダリングするフォームデザインを表す `java.io.FileInputStream` オブジェクトを作成します。
   * コンストラクターを使用して `java.io.FileInputStream` オブジェクトを渡すことにり、`com.adobe.idp.Document` オブジェクトを作成します。

1. 値でフォームをレンダリング

   `FormsServiceClient` オブジェクトの `renderPDFForm` メソッドを呼び出して、次の値を渡します。

   * 空の文字列の値（通常、このパラメーターにはフォームデザインの名前を指定する文字列の値が必要です）。
   * フォームデザインを含む `com.adobe.idp.Document` オブジェクト。通常、このパラメーター値はフォームにマージするデータ用に予約されています。
   * 実行時オプションを保存する `PDFFormRenderSpec` オブジェクト。このパラメーターはオプションであり、実行時のオプションを指定しない場合、`null` を指定できます。
   * Forms サービスで必要とされる URI 値を格納する `URLSpec` オブジェクト。
   * 添付ファイルを保存する `java.util.HashMap` オブジェクト。このパラメーターはオプションであり、フォームにファイルを添付しない場合、`null` を指定できます。

   `renderPDFForm` メソッドは、クライアントの web ブラウザーに書き込まれるフォームデータストリームを格納する `FormsResult` オブジェクトを返します。

1. フォームデータストリームをクライアント web ブラウザーに書き込む

   * `FormsResult` オブジェクトの `getOutputContent` メソッドを呼び出すことにより、`com.adobe.idp.Document` オブジェクトを作成します。
   * `getContentType` メソッドを呼び出すことにより、`com.adobe.idp.Document` オブジェクトのコンテンツタイプを取得します。
   * `setContentType` メソッドを呼び出して、`com.adobe.idp.Document` オブジェクトのコンテンツタイプ 渡すことにより、`javax.servlet.http.HttpServletResponse` オブジェクトのコンテンツタイプを設定します。
   * `javax.servlet.http.HttpServletResponse` オブジェクトの `getOutputStream` メソッドを呼び出すことにより、クライアントの web ブラウザーにフォームデータストリームを書き込むために使用する `javax.servlet.ServletOutputStream` オブジェクトを作成します。
   * `com.adobe.idp.Document` オブジェクトの `getInputStream` メソッドを呼び出すことにより、`java.io.InputStream` オブジェクトを作成します。
   * バイト配列を作成し、`InputStream` オブジェクトのサイズを割り当てます。`InputStream` オブジェクトの `available` メソッドを呼び出して、`InputStream` オブジェクトのサイズを取得します。
   * `InputStream` オブジェクトの `read` メソッドを呼び出して、バイト配列を引数として渡すことにより、バイト配列にフォームデータストリームを格納します。
   * `javax.servlet.ServletOutputStream` オブジェクトの `write` メソッドを呼び出して、フォームデータストリームをクライアント web ブラウザーに送信します。バイト配列を `write` メソッドに渡します。

**関連項目**

[値別に Forms をレンダリング](/help/forms/developing/rendering-forms.md)

[クイックスタート（SOAP モード）：Java API を使用した値によるレンダリング](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-by-value-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Web サービス API を使用して値でフォームをレンダリング {#render-a-form-by-value-using-the-web-service-api}

Forms API（web サービス）を使用して値でフォームをレンダリングします。

1. プロジェクトファイルを含める

   * Forms Service WSDL を使用する Java プロキシクラスを作成します。
   * Java プロキシクラスをクラスパスに含めます。

1. Forms Client API オブジェクトの作成

   `FormsService` オブジェクトを作成し、認証情報を設定します。

1. フォームデザインの参照

   * コンストラクターを使用して `java.io.FileInputStream` オブジェクトを作成します。XDP ファイルの場所を指定する文字列の値を渡します。
   * コンストラクターを使用して `BLOB` オブジェクトを作成します。`BLOB` オブジェクトは、パスワードで暗号化された PDF ドキュメントを保存するために使用されます。
   * `java.io.FileInputStream` オブジェクトのコンテンツを格納するバイト配列を作成します。`available` メソッドを使用して `java.io.FileInputStream` オブジェクトのサイズを取得することにより、バイト配列のサイズを指定できます。
   * `java.io.FileInputStream` オブジェクトの `read` メソッドを呼び出してバイト配列を渡すことにより、バイト配列にストリームデータを格納します。
   * `setBinaryData` メソッドを呼び出してバイト配列を渡すことにより、`BLOB` オブジェクトに入力します。

1. 値でフォームをレンダリング

   `FormsService` オブジェクトの `renderPDFForm` メソッドを呼び出して、次の値を渡します。

   * 空の文字列の値（通常、このパラメーターにはフォームデザインの名前を指定する文字列の値が必要です）。
   * フォームデザインを含む `BLOB` オブジェクト。通常、このパラメーター値はフォームにマージするデータ用に予約されています。
   * 実行時オプションを保存する `PDFFormRenderSpec` オブジェクト。これはオプションのパラメーターであり、実行時オプションを指定したくない場合は `null` を指定できます。
   * Forms サービスで必要な URI 値を格納する `URLSpec` オブジェクト。
   * 添付ファイルを格納する `java.util.HashMap` オブジェクト。これはオプションのパラメーターであり、フォームにファイルを添付しない場合は `null` を指定できます。
   * メソッドによって設定される空の `com.adobe.idp.services.holders.BLOBHolder` オブジェクト。これは、レンダリングされた PDF フォームを保存するために使用されます。
   * メソッドによって設定される空の `javax.xml.rpc.holders.LongHolder` オブジェクト。（この引数は、フォームのページ数を保存します）。
   * メソッドによって設定される空の `javax.xml.rpc.holders.StringHolder` オブジェクト。（この引数はロケール値を格納します。）
   * この操作の結果を格納する 空の `com.adobe.idp.services.holders.FormsResultHolder` オブジェクト。

   `renderPDFForm` メソッドは、最後の引数値として渡される `com.adobe.idp.services.holders.FormsResultHolder` オブジェクトに、クライアント web ブラウザーに書き込む必要のあるフォームデータストリームを入力します。

1. フォームデータストリームをクライアント web ブラウザーに書き込む

   * `com.adobe.idp.services.holders.FormsResultHolder` オブジェクトの `value` データメンバーの値を取得して、`FormResult` オブジェクトを作成します。
   * `FormsResult` オブジェクトの `getOutputContent` メソッドを呼び出して、フォームデータを含む `BLOB` オブジェクトを作成します。
   * `BLOB` オブジェクトの `getContentType` メソッドを呼び出して、コンテンツタイプを取得します。
   * `javax.servlet.http.HttpServletResponse` オブジェクトのコンテンツタイプを設定するには、その `setContentType` メソッドを呼び出して `BLOB` オブジェクトのコンテンツタイプを渡します。
   * `javax.servlet.http.HttpServletResponse` オブジェクトの `getOutputStream` メソッドを呼び出して、フォームデータストリームをクライアント web ブラウザーに書き込むために使用される `javax.servlet.ServletOutputStream` オブジェクトを作成します。
   * バイト配列を作成し、`BLOB` オブジェクトの `getBinaryData` メソッドを呼び出して設定します。このタスクは、`FormsResult` オブジェクトのコンテンツをバイト配列に割り当てます。
   * `javax.servlet.http.HttpServletResponse` オブジェクトの `write` メソッドを呼び出して、フォームデータストリームをクライアント web ブラウザーに送信します。バイト配列を `write` メソッドに渡します。

**関連項目**

[値別に Forms をレンダリング](#rendering-forms-by-value)

[Base64 エンコーディングを使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
