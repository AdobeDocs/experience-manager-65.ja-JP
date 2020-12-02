---
title: 値によるFormsのレンダリング
seo-title: 値によるFormsのレンダリング
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
workflow-type: tm+mt
source-wordcount: '1812'
ht-degree: 3%

---


# 値{#rendering-forms-by-value}でFormsをレンダリング

通常、Designerで作成されたフォームデザインは、Formsサービスへの参照によって渡されます。 フォームデザインは大きくなる場合があり、その結果、フォームデザインのバイトを値でマーシャリングする必要がなくなるように、参照によって渡す方が効率的になります。 また、Formsサービスはフォームデザインをキャッシュできるので、キャッシュしたときにフォームデザインを継続的に読み取る必要がありません。

フォームデザインにUUID属性が含まれる場合は、キャッシュされます。 UUID値は、すべてのフォームデザインで一意で、フォームを一意に識別するために使用します。 値を指定してフォームをレンダリングする場合、フォームを繰り返し使用する場合にのみキャッシュする必要があります。 ただし、フォームを繰り返し使用せず、一意である必要がある場合は、AEM FormsAPIで設定されたキャッシュオプションを使用してフォームをキャッシュしないでください。

また、Formsサービスは、フォームデザイン内のリンクされたコンテンツの場所を解決することもできます。 例えば、フォームデザイン内から参照されるリンク画像は、相対URLです。 リンクされたコンテンツは、常にフォームデザインの場所に対する相対コンテンツであると見なされます。 したがって、リンクされたコンテンツを解決するには、フォームデザインの絶対位置に相対パスを適用して位置を決定する必要があります。

フォームデザインを参照で渡す代わりに、値でフォームデザインを渡すことができます。 フォームデザインを動的に作成する場合、値を使用してフォームデザインを渡す方法が効率的です。つまり、クライアントアプリケーションが実行時にフォームデザインを作成するXMLを生成する場合です。 この場合、フォームデザインはメモリに保存されるので、物理リポジトリには保存されません。 実行時に動的にフォームデザインを作成し、値を渡す場合は、フォームをキャッシュして、Formsサービスのパフォーマンスを向上させることができます。

**値によるフォームの渡しの制限**

フォームデザインが値によって渡される場合、次の制限が適用されます。

* 相対的なリンクコンテンツをフォームデザイン内に置くことはできません。 すべての画像とフラグメントは、フォームデザイン内に埋め込むか、絶対に参照する必要があります。
* フォームのレンダリング後は、サーバー側の計算を実行できません。 フォームがFormsサービスに送信され戻されると、データは抽出され、サーバー側で計算されることなく返されます。
* HTMLでは、リンクされた画像を実行時にのみ使用できるので、埋め込み画像を使用してHTMLを生成することはできません。 これは、Formsサービスが参照先のフォームデザインから画像を取得することで、HTMLを使用した埋め込み画像をサポートするからです。 値によって渡されるフォームデザインは参照先を持たないので、HTMLページが表示されている場合、埋め込み画像を抽出することはできません。 したがって、画像参照は、HTMLでレンダリングする絶対パスである必要があります。

>[!NOTE]
>
>値ごとに異なる種類のフォーム（HTMLフォームや使用権限を含むフォームなど）をレンダリングできますが、この節ではインタラクティブPDF formsのレンダリングについて説明します。

>[!NOTE]
>
>Formsサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

## 手順{#summary-of-steps}の概要

値を指定してフォームをレンダリングするには、次の手順を実行します。

1. プロジェクトファイルを含めます。
1. FormsクライアントAPIオブジェクトを作成します。
1. フォームデザインを参照します。
1. 値でフォームをレンダリングする。
1. フォームデータストリームをクライアントのWebブラウザーに書き込みます。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めます。

**FormsクライアントAPIオブジェクトの作成**

プログラムでデータをPDFフォームのクライアントAPIに読み込む前に、Data Integrationサービスクライアントを作成する必要があります。 サービスクライアントを作成する場合、サービスの呼び出しに必要な接続設定を定義します。

**フォームデザインの参照**

値を指定してフォームをレンダリングする場合は、レンダリングするフォームデザインを含む`com.adobe.idp.Document`オブジェクトを作成する必要があります。 既存のXDPファイルを参照することも、実行時に動的にフォームデザインを作成して、`com.adobe.idp.Document`にそのデータを埋め込むこともできます。

>[!NOTE]
>
>この節と対応するクイック開始では、既存のXDPファイルを参照します。

**値によるフォームのレンダリング**

値を指定してフォームをレンダリングするには、フォームデザインを含む`com.adobe.idp.Document`インスタンスをレンダリングメソッドの`inDataDoc`パラメーターに渡します（`renderPDFForm`、`(Deprecated) renderHTMLForm`など、`FormsServiceClient`オブジェクトのレンダリングメソッドのいずれか）。 このパラメーターの値は通常、フォームにマージされるデータ用に予約されています。 同様に、`formQuery`パラメーターに空の文字列値を渡します。 通常、このパラメーターにはフォームデザインの名前を指定する文字列値が必要です。

>[!NOTE]
>
>フォーム内にデータを表示する場合は、`xfa:datasets`要素内にデータを指定する必要があります。 XFAアーキテクチャについて詳しくは、[https://partners.adobe.com/public/developer/xml/index_arch.html](https://partners.adobe.com/public/developer/xml/index_arch.html)を参照してください。

**フォームデータストリームをクライアントのWebブラウザーに書き込みます**

Formsサービスは、値別にフォームをレンダリングする場合、フォームデータストリームを返します。このストリームをクライアントのWebブラウザーに書き込む必要があります。 クライアントのWebブラウザーに書き込まれると、フォームはユーザーに表示されます。

**関連トピック**

[Java APIを使用した値によるフォームのレンダリング](#render-a-form-by-value-using-the-java-api)

[WebサービスAPIを使用して値でフォームをレンダリングする](#render-a-form-by-value-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[FormsサービスAPIクイック開始](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Formsサービスにドキュメントを渡す](/help/forms/developing/passing-documents-forms-service.md)

[FormsをレンダリングするWeb アプリケーションの作成](/help/forms/developing/creating-web-applications-renders-forms.md)

## Java API {#render-a-form-by-value-using-the-java-api}を使用して値でフォームをレンダリングする

FormsAPI(Java)を使用して値でフォームをレンダリングする：

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-forms-client.jarなどのクライアントJARファイルを含めます。

1. FormsクライアントAPIオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用し、`FormsServiceClient`オブジェクトを渡して、`ServiceClientFactory`オブジェクトを作成します。

1. フォームデザインの参照

   * コンストラクターを使用し、XDPファイルの場所を指定する文字列値を渡して、レンダリングするフォームデザインを表す`java.io.FileInputStream`オブジェクトを作成します。
   * コンストラクタを使用して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.FileInputStream` オブジェクトを作成します。

1. 値によるフォームのレンダリング

   `FormsServiceClient`オブジェクトの`renderPDFForm`メソッドを呼び出し、次の値を渡します。

   * 空の文字列値です。 （通常、このパラメーターにはフォームデザインの名前を指定する文字列値が必要です）。
   * フォームデザインを含む`com.adobe.idp.Document`オブジェクト。 通常、このパラメーターの値はフォームにマージされるデータ用に予約されています。
   * 実行時オプションを格納する`PDFFormRenderSpec`オブジェクト。 これはオプションのパラメーターです。実行時のオプションを指定しない場合は、`null`を指定できます。
   * Formsサービスに必要なURI値を含む`URLSpec`オブジェクト。
   * 添付ファイルを格納する`java.util.HashMap`オブジェクト。 これはオプションのパラメーターです。フォームにファイルを添付しない場合は、`null`を指定できます。

   `renderPDFForm`メソッドは、クライアントのWebブラウザーに書き込み可能なフォームデータストリームを含む`FormsResult`オブジェクトを返します。

1. フォームデータストリームをクライアントのWebブラウザーに書き込みます

   * `FormsResult`オブジェクト&#39;s `getOutputContent`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトを作成します。
   * `getContentType`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトのコンテンツタイプを取得します。
   * `javax.servlet.http.HttpServletResponse`オブジェクトのコンテンツタイプを設定するには、`setContentType`メソッドを呼び出し、`com.adobe.idp.Document`オブジェクトのコンテンツタイプを渡します。
   * `javax.servlet.http.HttpServletResponse`オブジェクトの`getOutputStream`メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに書き込むために使用する`javax.servlet.ServletOutputStream`オブジェクトを作成します。
   * `com.adobe.idp.Document`オブジェクトの`getInputStream`メソッドを呼び出して、`java.io.InputStream`オブジェクトを作成します。
   * バイト配列を作成し、`InputStream`オブジェクトのサイズを割り当てます。 `InputStream`オブジェクトの`available`メソッドを呼び出して、`InputStream`オブジェクトのサイズを取得します。
   * `InputStream`オブジェクトの`read`メソッドを呼び出し、バイト配列を引数として渡すことで、フォームデータストリームをバイト配列に入力します。
   * `javax.servlet.ServletOutputStream`オブジェクトの`write`メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに送信します。 バイト配列を`write`メソッドに渡します。

**関連トピック**

[値によるFormsのレンダリング](/help/forms/developing/rendering-forms.md)

[クイック開始（SOAPモード）:Java APIを使用した値によるレンダリング](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-by-value-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## WebサービスAPI {#render-a-form-by-value-using-the-web-service-api}を使用して値でフォームをレンダリングする

FormsAPI（Webサービス）を使用して値でフォームをレンダリングする：

1. プロジェクトファイルを含める

   * FormsサービスのWSDLを使用するJavaプロキシクラスを作成します。
   * クラスパスにJavaプロキシクラスを含めます。

1. FormsクライアントAPIオブジェクトの作成

   `FormsService`オブジェクトを作成し、認証値を設定します。

1. フォームデザインの参照

   * コンストラクタを使用して `java.io.FileInputStream` オブジェクトを作成します。XDPファイルの場所を指定するstring値を渡します。
   * コンストラクタを使用して `BLOB` オブジェクトを作成します。`BLOB`オブジェクトは、パスワードで暗号化されたPDFドキュメントを保存するために使用します。
   * `java.io.FileInputStream`オブジェクトの内容を格納するバイト配列を作成します。 `java.io.FileInputStream`オブジェクトのサイズを取得するには、`available`メソッドを使用します。
   * `java.io.FileInputStream`オブジェクトの`read`メソッドを呼び出し、バイト配列を渡すことで、ストリームデータをバイト配列に入力します。
   * `BLOB`オブジェクトを入力するには、`setBinaryData`メソッドを呼び出し、バイト配列を渡します。

1. 値によるフォームのレンダリング

   `FormsService`オブジェクトの`renderPDFForm`メソッドを呼び出し、次の値を渡します。

   * 空の文字列値です。 （通常、このパラメーターにはフォームデザインの名前を指定する文字列値が必要です）。
   * フォームデザインを含む`BLOB`オブジェクト。 通常、このパラメーターの値はフォームにマージされるデータ用に予約されています。
   * 実行時オプションを格納する`PDFFormRenderSpec`オブジェクト。 これはオプションのパラメーターです。実行時のオプションを指定しない場合は、`null`を指定できます。
   * Formsサービスに必要なURI値を含む`URLSpec`オブジェクト。
   * 添付ファイルを格納する`java.util.HashMap`オブジェクト。 これはオプションのパラメーターです。フォームにファイルを添付しない場合は、`null`を指定できます。
   * メソッドによって入力される空の`com.adobe.idp.services.holders.BLOBHolder`オブジェクト。 これは、レンダリングされたPDFフォームを保存するために使用します。
   * メソッドによって入力される空の`javax.xml.rpc.holders.LongHolder`オブジェクト。 （この引数は、フォームのページ数を格納します）。
   * メソッドによって入力される空の`javax.xml.rpc.holders.StringHolder`オブジェクト。 （この引数はロケールの値を格納します）。
   * この操作の結果を含む空の`com.adobe.idp.services.holders.FormsResultHolder`オブジェクトです。

   `renderPDFForm`メソッドは、最後の引数値として渡される`com.adobe.idp.services.holders.FormsResultHolder`オブジェクトに、クライアントWebブラウザーに書き込む必要のあるフォームデータストリームを入力します。

1. フォームデータストリームをクライアントのWebブラウザーに書き込みます

   * `com.adobe.idp.services.holders.FormsResultHolder`オブジェクトの`value`データメンバの値を取得して、`FormResult`オブジェクトを作成します。
   * `FormsResult`オブジェクトの`getOutputContent`メソッドを呼び出して、フォームデータを含む`BLOB`オブジェクトを作成します。
   * `getContentType`メソッドを呼び出して、`BLOB`オブジェクトのコンテンツタイプを取得します。
   * `javax.servlet.http.HttpServletResponse`オブジェクトのコンテンツタイプを設定するには、`setContentType`メソッドを呼び出し、`BLOB`オブジェクトのコンテンツタイプを渡します。
   * `javax.servlet.http.HttpServletResponse`オブジェクトの`getOutputStream`メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに書き込むために使用する`javax.servlet.ServletOutputStream`オブジェクトを作成します。
   * バイト配列を作成し、`BLOB`オブジェクトの`getBinaryData`メソッドを呼び出して値を設定します。 このタスクは、`FormsResult`オブジェクトの内容をバイト配列に割り当てます。
   * `javax.servlet.http.HttpServletResponse`オブジェクトの`write`メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに送信します。 バイト配列を`write`メソッドに渡します。

**関連トピック**

[値によるFormsのレンダリング](#rendering-forms-by-value)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
