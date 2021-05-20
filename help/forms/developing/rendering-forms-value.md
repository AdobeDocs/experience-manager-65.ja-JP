---
title: 値によるFormsのレンダリング
seo-title: 値によるFormsのレンダリング
description: Forms API(Java)を使用して、Java APIとWebサービスAPIを使用して値でフォームをレンダリングします。
seo-description: Forms API(Java)を使用して、Java APIとWebサービスAPIを使用して値でフォームをレンダリングします。
uuid: b932cc54-662f-40ae-94e0-20ac82845f3b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: ddbb2b82-4c57-4845-a5be-2435902d312b
role: Developer
exl-id: a3a6a06d-ec90-4147-a5f0-e776a086ee12
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1862'
ht-degree: 3%

---

# 値{#rendering-forms-by-value}によるFormsのレンダリング

**このドキュメントのサンプルと例は、JEE上のAEM Forms環境に限られています。**

通常、Designerで作成されたフォームデザインは、Formsサービスへの参照によって渡されます。 フォームデザインは大きくなる可能性があり、その結果、フォームデザインのバイトを値でマーシャリングする必要がなく、参照で渡す方が効率的になります。 また、Formsサービスは、フォームデザインをキャッシュして、キャッシュ時にフォームデザインを継続的に読み取る必要がないようにすることもできます。

フォームデザインにUUID属性が含まれている場合は、その属性がキャッシュされます。 UUID値は、すべてのフォームデザインで一意で、フォームを一意に識別するために使用されます。 値でフォームをレンダリングする場合は、繰り返し使用する場合にのみフォームをキャッシュする必要があります。 ただし、フォームを繰り返し使用せずに一意にする必要がある場合は、AEM Forms APIを使用して設定されたキャッシュオプションを使用して、フォームをキャッシュするのを避けることができます。

Formsサービスは、フォームデザイン内のリンクされたコンテンツの場所を解決することもできます。 例えば、フォームデザイン内から参照されるリンク画像は、相対URLです。 リンクされたコンテンツは、常にフォームデザインの場所に対する相対コンテンツと見なされます。 したがって、リンクされたコンテンツを解決するには、フォームデザインの絶対位置に相対パスを適用して、場所を決定する必要があります。

参照によってフォームデザインを渡す代わりに、値でフォームデザインを渡すことができます。 フォームデザインを動的に作成する場合は、フォームデザインを値で渡すと効率的です。つまり、クライアントアプリケーションが実行時にフォームデザインを作成するXMLを生成する場合です。 この場合、フォームデザインはメモリに保存されるので、物理リポジトリに保存されません。 実行時に動的にフォームデザインを作成し、値を渡す場合は、フォームをキャッシュして、Formsサービスのパフォーマンスを向上させることができます。

**フォームを値で渡す際の制限**

フォームデザインが値で渡される場合は、次の制限が適用されます。

* フォームデザイン内には、相対的にリンクされたコンテンツを含めることはできません。 すべての画像とフラグメントは、フォームデザイン内に埋め込むか、絶対に参照する必要があります。
* フォームのレンダリング後にサーバー側の計算を実行することはできません。 フォームがFormsサービスに送り返されると、データが抽出され、サーバー側の計算なしで返されます。
* HTMLでは、実行時にのみリンクされた画像を使用できるので、埋め込まれた画像を含むHTMLを生成することはできません。 これは、Formsサービスが参照先のフォームデザインから画像を取得することで、HTMLを含んだ埋め込み画像をサポートするためです。 値で渡されるフォームデザインには参照先の場所がないので、HTMLページを表示する際に埋め込み画像を抽出することはできません。 したがって、画像参照は、HTMLでレンダリングされる絶対パスにする必要があります。

>[!NOTE]
>
>値ごとに異なる種類のフォームをレンダリングできますが（例えば、HTMLフォームや使用権限を含むフォームなど）、この節ではインタラクティブPDF formsのレンダリングについて説明します。

>[!NOTE]
>
>Formsサービスについて詳しくは、『 AEM Formsのサービスリファレンス[ 』を参照してください。](https://www.adobe.com/go/learn_aemforms_services_63)

## 手順の概要{#summary-of-steps}

値でフォームをレンダリングするには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. Forms Client APIオブジェクトを作成します。
1. フォームデザインを参照します。
1. 値でフォームをレンダリングします。
1. フォームデータストリームをクライアントWebブラウザーに書き込みます。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用する場合は、プロキシファイルを必ず含めてください。

**Forms Client APIオブジェクトの作成**

プログラムによってデータをPDFフォームのクライアントAPIに読み込む前に、データ統合サービスクライアントを作成する必要があります。 サービスクライアントを作成する場合、サービスを呼び出すために必要な接続設定を定義します。

**フォームデザインの参照**

値でフォームをレンダリングする場合は、レンダリングするフォームデザインを格納する`com.adobe.idp.Document`オブジェクトを作成する必要があります。 既存のXDPファイルを参照することも、実行時に動的にフォームデザインを作成して、`com.adobe.idp.Document`にそのデータを入力することもできます。

>[!NOTE]
>
>このセクションと対応するクイックスタートは、既存のXDPファイルを参照します。

**値によるフォームのレンダリング**

フォームを値でレンダリングするには、フォームデザインを含む`com.adobe.idp.Document`インスタンスをレンダリングメソッドの`inDataDoc`パラメーターに渡します（`renderPDFForm`、`(Deprecated) renderHTMLForm`など、`FormsServiceClient`オブジェクトのレンダリングメソッドのいずれかを指定できます）。 このパラメーター値は、通常、フォームとマージされるデータ用に予約されます。 同様に、空の文字列値を`formQuery`パラメーターに渡します。 通常、このパラメーターにはフォームデザインの名前を指定する文字列値が必要です。

>[!NOTE]
>
>フォーム内にデータを表示する場合は、`xfa:datasets`要素内でデータを指定する必要があります。 XFAアーキテクチャについて詳しくは、[https://partners.adobe.com/public/developer/xml/index_arch.html](https://partners.adobe.com/public/developer/xml/index_arch.html)を参照してください。

**フォームデータストリームをクライアントWebブラウザーに書き込む**

Formsサービスは、値でフォームをレンダリングする場合、フォームデータストリームを返します。このストリームは、クライアントのWebブラウザーに書き込む必要があります。 クライアントのWebブラウザーに書き込まれると、フォームはユーザーに表示されます。

**関連トピック**

[Java APIを使用した値によるフォームのレンダリング](#render-a-form-by-value-using-the-java-api)

[WebサービスAPIを使用して値でフォームをレンダリングする](#render-a-form-by-value-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[FormsサービスAPIのクイックスタート](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Formsサービスにドキュメントを渡す](/help/forms/developing/passing-documents-forms-service.md)

[Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Java API {#render-a-form-by-value-using-the-java-api}を使用して値でフォームをレンダリングする

Forms API(Java)を使用して値でフォームをレンダリングする：

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-forms-client.jarなどのクライアントJARファイルを含めます。

1. Forms Client APIオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して`FormsServiceClient`オブジェクトを渡し、`ServiceClientFactory`オブジェクトを作成します。

1. フォームデザインの参照

   * レンダリングするフォームデザインを表す`java.io.FileInputStream`オブジェクトを作成します。そのためには、コンストラクターを使用し、XDPファイルの場所を指定する文字列値を渡します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 値によるフォームのレンダリング

   `FormsServiceClient`オブジェクトの`renderPDFForm`メソッドを呼び出し、次の値を渡します。

   * 空の文字列値。 （通常、このパラメーターにはフォームデザインの名前を指定する文字列値が必要です）。
   * フォームデザインを含む`com.adobe.idp.Document`オブジェクト。 通常、このパラメーター値はフォームとマージされるデータ用に予約されます。
   * 実行時オプションを格納する`PDFFormRenderSpec`オブジェクト。 これはオプションのパラメーターで、実行時オプションを指定しない場合は`null`を指定できます。
   * Formsサービスに必要なURI値を含む`URLSpec`オブジェクト。
   * 添付ファイルを格納する`java.util.HashMap`オブジェクト。 これはオプションのパラメーターで、フォームにファイルを添付しない場合は`null`を指定できます。

   `renderPDFForm`メソッドは、クライアントのWebブラウザーに書き込み可能なフォームデータストリームを含む`FormsResult`オブジェクトを返します。

1. フォームデータストリームをクライアントWebブラウザーに書き込む

   * `FormsResult`オブジェクトの`getOutputContent`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトを作成します。
   * `getContentType`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトのコンテンツタイプを取得します。
   * `setContentType`メソッドを呼び出し、`com.adobe.idp.Document`オブジェクトのコンテンツタイプを渡すことで、`javax.servlet.http.HttpServletResponse`オブジェクトのコンテンツタイプを設定します。
   * `javax.servlet.http.HttpServletResponse`オブジェクトの`getOutputStream`メソッドを呼び出して、フォームデータストリームをクライアントWebブラウザーに書き込むための`javax.servlet.ServletOutputStream`オブジェクトを作成します。
   * `com.adobe.idp.Document`オブジェクトの`getInputStream`メソッドを呼び出して、`java.io.InputStream`オブジェクトを作成します。
   * バイト配列を作成し、`InputStream`オブジェクトのサイズを割り当てます。 `InputStream`オブジェクトの`available`メソッドを呼び出して、`InputStream`オブジェクトのサイズを取得します。
   * `InputStream`オブジェクトの`read`メソッドを呼び出し、バイト配列を引数として渡すことで、フォームデータストリームをバイト配列に入力します。
   * `javax.servlet.ServletOutputStream`オブジェクトの`write`メソッドを呼び出して、フォームデータストリームをクライアントWebブラウザーに送信します。 `write`メソッドにバイト配列を渡します。

**関連トピック**

[値によるFormsのレンダリング](/help/forms/developing/rendering-forms.md)

[クイックスタート（SOAPモード）:Java APIを使用した値によるレンダリング](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-by-value-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## WebサービスAPI {#render-a-form-by-value-using-the-web-service-api}を使用して値でフォームをレンダリングする

Forms API（Webサービス）を使用して値でフォームをレンダリングする：

1. プロジェクトファイルを含める

   * FormsサービスのWSDLを使用するJavaプロキシクラスを作成します。
   * Javaプロキシクラスをクラスパスに含めます。

1. Forms Client APIオブジェクトの作成

   `FormsService`オブジェクトを作成し、認証値を設定します。

1. フォームデザインの参照

   * コンストラクタを使用して `java.io.FileInputStream` オブジェクトを作成します。XDPファイルの場所を指定するstring値を渡します。
   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、パスワードで暗号化されたPDFドキュメントを保存するために使用します。
   * `java.io.FileInputStream`オブジェクトの内容を格納するバイト配列を作成します。 `available`メソッドを使用して`java.io.FileInputStream`オブジェクトのサイズを取得することで、バイト配列のサイズを決定できます。
   * `java.io.FileInputStream`オブジェクトの`read`メソッドを呼び出し、バイト配列を渡すことにより、ストリームデータをバイト配列に入力します。
   * `setBinaryData`メソッドを呼び出し、バイト配列を渡すことで、`BLOB`オブジェクトを設定します。

1. 値によるフォームのレンダリング

   `FormsService`オブジェクトの`renderPDFForm`メソッドを呼び出し、次の値を渡します。

   * 空の文字列値。 （通常、このパラメーターにはフォームデザインの名前を指定する文字列値が必要です）。
   * フォームデザインを含む`BLOB`オブジェクト。 通常、このパラメーター値はフォームとマージされるデータ用に予約されます。
   * 実行時オプションを格納する`PDFFormRenderSpec`オブジェクト。 これはオプションのパラメーターで、実行時オプションを指定しない場合は`null`を指定できます。
   * Formsサービスに必要なURI値を含む`URLSpec`オブジェクト。
   * 添付ファイルを格納する`java.util.HashMap`オブジェクト。 これはオプションのパラメーターで、フォームにファイルを添付しない場合は`null`を指定できます。
   * メソッドで設定される空の`com.adobe.idp.services.holders.BLOBHolder`オブジェクト。 これは、レンダリングされたPDFフォームを保存するために使用されます。
   * メソッドで設定される空の`javax.xml.rpc.holders.LongHolder`オブジェクト。 （この引数は、フォームのページ数を格納します）。
   * メソッドで設定される空の`javax.xml.rpc.holders.StringHolder`オブジェクト。 （この引数はロケール値を格納します。）
   * この操作の結果を格納する空の`com.adobe.idp.services.holders.FormsResultHolder`オブジェクト。

   `renderPDFForm`メソッドは、最後の引数値として渡される`com.adobe.idp.services.holders.FormsResultHolder`オブジェクトに、クライアントWebブラウザーに書き込む必要のあるフォームデータストリームを設定します。

1. フォームデータストリームをクライアントWebブラウザーに書き込む

   * `com.adobe.idp.services.holders.FormsResultHolder`オブジェクトの`value`データメンバーの値を取得して、`FormResult`オブジェクトを作成します。
   * `FormsResult`オブジェクトの`getOutputContent`メソッドを呼び出して、フォームデータを含む`BLOB`オブジェクトを作成します。
   * `getContentType`メソッドを呼び出して、`BLOB`オブジェクトのコンテンツタイプを取得します。
   * `setContentType`メソッドを呼び出し、`BLOB`オブジェクトのコンテンツタイプを渡すことで、`javax.servlet.http.HttpServletResponse`オブジェクトのコンテンツタイプを設定します。
   * `javax.servlet.http.HttpServletResponse`オブジェクトの`getOutputStream`メソッドを呼び出して、フォームデータストリームをクライアントWebブラウザーに書き込むための`javax.servlet.ServletOutputStream`オブジェクトを作成します。
   * バイト配列を作成し、`BLOB`オブジェクトの`getBinaryData`メソッドを呼び出してそれを設定します。 このタスクは、`FormsResult`オブジェクトの内容をバイト配列に割り当てます。
   * `javax.servlet.http.HttpServletResponse`オブジェクトの`write`メソッドを呼び出して、フォームデータストリームをクライアントWebブラウザーに送信します。 `write`メソッドにバイト配列を渡します。

**関連トピック**

[値によるFormsのレンダリング](#rendering-forms-by-value)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
