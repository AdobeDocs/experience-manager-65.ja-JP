---
title: 使用権限を付与されたFormsのレンダリング
seo-title: 使用権限を付与されたFormsのレンダリング
description: 使用権限が適用されたフォームをレンダリングするには、Formsサービスを使用します。 Java APIとWeb Service APIを使用して、使用権限を付与されたフォームをレンダリングできます。
seo-description: 使用権限が適用されたフォームをレンダリングするには、Formsサービスを使用します。 Java APIとWeb Service APIを使用して、使用権限を付与されたフォームをレンダリングできます。
uuid: ce5e4be6-d9b0-4989-a0e1-a8c3b98aed77
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d4c2b2f0-613a-409d-b39b-8e37fdb96eea
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '1493'
ht-degree: 5%

---


# 使用権限を有効にしたForms{#rendering-rights-enabled-forms}のレンダリング

Formsサービスは、使用権限が適用されたフォームをレンダリングできます。 使用権限は、Acrobat ではデフォルトで利用できるが Adobe Reader では利用できない機能（フォームにコメントを追加する機能や、フォームフィールドにデータを入力してフォームを保存する機能など）に関連しています。使用権限が適用されているFormsは、使用権限を付与されたフォームと呼ばれます。 使用権限を付与されたフォームをAdobe Readerで開いたユーザーは、そのフォームに対して有効になっている操作を実行できます。

フォームに使用権限を適用するには、Acrobat Reader DC拡張サービスがAEM formsのインストールに含まれている必要があります。 また、PDFドキュメントに使用権限を適用できる有効な秘密鍵証明書が必要です。 つまり、使用権限を付与されたフォームをレンダリングする前に、Acrobat Reader DC拡張サービスを適切に設定する必要があります。 ([Acrobat Reader DC拡張サービス](/help/forms/developing/assigning-usage-rights.md#about-the-acrobat-reader-dc-extensions-service)についてを参照)。

>[!NOTE]
>
>使用権限を含むフォームをレンダリングするには、PDFファイルではなく、入力としてXDPファイルを使用する必要があります。 PDFファイルを入力として使用する場合、フォームは引き続きレンダリングされます。ただし、このフォームは使用権限を付与されたフォームではありません。

>[!NOTE]
>
>次の使用権限を指定する場合は、XMLデータを使用してフォームを自動埋め込むことはできません。`enableComments`、`enableCommentsOnline`、`enableEmbeddedFiles`、または`enableDigitalSignatures`。 (「[編集可能なレイアウトでFormsを自動埋め込む](/help/forms/developing/prepopulating-forms-flowable-layouts.md)」を参照)。

>[!NOTE]
>
>Formsサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

## 手順{#summary-of-steps}の概要

使用権限を付与されたフォームをレンダリングするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. FormsクライアントAPIオブジェクトを作成します。
1. 使用権限の実行時オプションを設定します。
1. 使用権限を付与されたフォームをレンダリングする。
1. 使用権限を付与されたフォームをクライアントWebブラウザーに書き込みます。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めてください。

**FormsクライアントAPIオブジェクトの作成**

プログラムでFormsサービスのクライアントAPI操作を実行する前に、Formsサービスクライアントを作成する必要があります。

**使用権限の実行時オプションの設定**

使用権限を付与されたフォームをレンダリングするには、使用権限の実行時オプションを設定する必要があります。 また、使用権限をフォームに適用するために使用する秘密鍵証明書のエイリアスも指定する必要があります。 エイリアス値を指定した後、フォームに適用する各使用権限を指定します。

**使用権限を付与されたフォームのレンダリング**

使用権限を付与されたフォームをレンダリングするには、使用権限のないフォームをレンダリングするのと同じアプリケーションロジックを使用します。 唯一の違いは、使用権限の実行時オプションがアプリケーションロジックに確実に含まれていることです。

>[!NOTE]
>
>FormsWebサービスAPIを使用して使用権限を付与されたフォームをレンダリングする場合、フォームにファイルを添付することはできません。

**フォームデータストリームをクライアントのWebブラウザーに書き込みます**

使用権限を付与されたフォームをレンダリングすると、Formsサービスはフォームデータストリームを返し、クライアントのWebブラウザーに書き込む必要があります。 クライアントのWebブラウザーに書き込まれると、フォームはユーザーに表示されます。 Adobe Readerで使用権限を付与されたフォームを表示しているユーザーは、そのフォームに対して有効になっている操作を実行できます。

**関連トピック**

[Java APIを使用して権限を付与されたフォームをレンダリングする](#render-rights-enabled-forms-using-the-java-api)

[WebサービスAPIを使用して権限を付与されたフォームをレンダリングする](#render-rights-enabled-forms-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[FormsサービスAPIクイック開始](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[インタラクティブPDF formsのレンダリング](/help/forms/developing/rendering-interactive-pdf-forms.md)

[FormsをレンダリングするWeb アプリケーションの作成](/help/forms/developing/creating-web-applications-renders-forms.md)

### Java API {#render-rights-enabled-forms-using-the-java-api}を使用して権限を付与されたフォームをレンダリングする

FormsAPI(Java)を使用して、使用権限を付与されたフォームをレンダリングします。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-forms-client.jarなどのクライアントJARファイルを含めます。

1. FormsクライアントAPIオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用し、`FormsServiceClient`オブジェクトを渡して、`ServiceClientFactory`オブジェクトを作成します。

1. 使用権限の実行時オプションの設定

   * コンストラクタを使用して `ReaderExtensionSpec` オブジェクトを作成します。
   * `ReaderExtensionSpec`オブジェクトの`setReCredentialAlias`メソッドを呼び出して秘密鍵証明書のエイリアスを指定し、エイリアス値を表すstring値を指定します。
   * `ReaderExtensionSpec`オブジェクトに属する対応するメソッドを呼び出して、各使用権限を設定します。 ただし、使用権限を設定できるのは、参照する秘密鍵証明書で許可されている場合のみです。 つまり、秘密鍵証明書で設定が許可されていない場合は、使用権限を設定できません。 例：. ユーザーがフォームフィールドに入力してフォームを保存できる使用権限を設定するには、`ReaderExtensionSpec`オブジェクトの`setReFillIn`メソッドを呼び出して、`true`を渡します。

   >[!NOTE]
   >
   >`ReaderExtensionSpec`オブジェクトの`setReCredentialPassword`メソッドを呼び出す必要はありません。 このメソッドは、Formsサービスでは使用されません。

1. 使用権限を付与されたフォームのレンダリング

   `FormsServiceClient`オブジェクトの`renderPDFFormWithUsageRights`メソッドを呼び出し、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定するstring値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`など、完全なパスを必ず指定してください。
   * フォームとマージするデータを含む`com.adobe.idp.Document`オブジェクト。 データをマージしない場合は、空の`com.adobe.idp.Document`オブジェクトを渡します。
   * 実行時オプションを格納する`PDFFormRenderSpec`オブジェクト。
   * 使用権限の実行時オプションを格納する`ReaderExtensionSpec`オブジェクト。
   * Formsサービスに必要なURI値を含む`URLSpec`オブジェクト。

   `renderPDFFormWithUsageRights`メソッドは、クライアントのWebブラウザーに書き込む必要があるフォームデータストリームを含む`FormsResult`オブジェクトを返します。

1. フォームデータストリームをクライアントのWebブラウザーに書き込みます

   * `FormsResult`オブジェクト&#39;s `getOutputContent`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトを作成します。
   * `getContentType`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトのコンテンツタイプを取得します。
   * `javax.servlet.http.HttpServletResponse`オブジェクトのコンテンツタイプを設定するには、`setContentType`メソッドを呼び出し、`com.adobe.idp.Document`オブジェクトのコンテンツタイプを渡します。
   * `javax.servlet.http.HttpServletResponse`オブジェクトの`getOutputStream`メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに書き込むために使用する`javax.servlet.ServletOutputStream`オブジェクトを作成します。
   * `com.adobe.idp.Document`オブジェクトの`getInputStream`メソッドを呼び出して、`java.io.InputStream`オブジェクトを作成します。
   * `InputStream`オブジェクトの`read`メソッドを呼び出し、バイト配列を引数として渡すことで、バイト配列を作成し、フォームデータストリームを入力します。
   * `javax.servlet.ServletOutputStream`オブジェクトの`write`メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに送信します。 バイト配列を`write`メソッドに渡します。

**関連トピック**

[クイック開始（SOAPモード）:Java APIを使用した使用権限付きフォームのレンダリング](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-rights-enabled-form-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## WebサービスAPI {#render-rights-enabled-forms-using-the-web-service-api}を使用して、権限を付与されたフォームをレンダリングする

FormsAPI（Webサービス）を使用して、使用権限を付与されたフォームをレンダリングします。

1. プロジェクトファイルを含める

   * FormsサービスのWSDLを使用するJavaプロキシクラスを作成します。
   * クラスパスにJavaプロキシクラスを含めます。

1. FormsクライアントAPIオブジェクトの作成

   `FormsService`オブジェクトを作成し、認証値を設定します。

1. 使用権限の実行時オプションの設定

   * コンストラクタを使用して `ReaderExtensionSpec` オブジェクトを作成します。
   * `ReaderExtensionSpec`オブジェクトの`setReCredentialAlias`メソッドを呼び出して秘密鍵証明書のエイリアスを指定し、エイリアス値を表すstring値を指定します。
   * `ReaderExtensionSpec`オブジェクトに属する対応するメソッドを呼び出して、各使用権限を設定します。 ただし、使用権限を設定できるのは、参照する秘密鍵証明書で許可されている場合のみです。 つまり、秘密鍵証明書で設定が許可されていない場合は、使用権限を設定できません。 ユーザーがフォームフィールドに入力してフォームを保存できる使用権限を設定するには、`ReaderExtensionSpec`オブジェクトの`setReFillIn`メソッドを呼び出して`true`を渡します。

1. 使用権限を付与されたフォームのレンダリング

   `FormsService`オブジェクトの`renderPDFFormWithUsageRights`メソッドを呼び出し、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定するstring値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`など、完全なパスを必ず指定してください。
   * フォームとマージするデータを含む`BLOB`オブジェクト。 データをフォームとマージしない場合は、空のXMLデータソースに基づく`BLOB`オブジェクトを渡す必要があります。 nullの`BLOB`オブジェクトを渡すことはできません。それ以外の場合は、例外が発生します。
   * 実行時オプションを格納する`PDFFormRenderSpec`オブジェクト。
   * 使用権限の実行時オプションを格納する`ReaderExtensionSpec`オブジェクト。
   * Formsサービスに必要なURI値を含む`URLSpec`オブジェクト。

   `renderPDFFormWithUsageRights`メソッドは、クライアントのWebブラウザーに書き込む必要があるフォームデータストリームを含む`FormsResult`オブジェクトを返します。

1. フォームデータストリームをクライアントのWebブラウザーに書き込みます

   * `FormsResult`オブジェクトの`getOutputContent`メソッドを呼び出して、フォームデータを含む`BLOB`オブジェクトを作成します。
   * `getContentType`メソッドを呼び出して、`BLOB`オブジェクトのコンテンツタイプを取得します。
   * `javax.servlet.http.HttpServletResponse`オブジェクトのコンテンツタイプを設定するには、`setContentType`メソッドを呼び出し、`BLOB`オブジェクトのコンテンツタイプを渡します。
   * `javax.servlet.http.HttpServletResponse`オブジェクトの`getOutputStream`メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに書き込むために使用する`javax.servlet.ServletOutputStream`オブジェクトを作成します。
   * バイト配列を作成し、`BLOB`オブジェクトの`getBinaryData`メソッドを呼び出して値を設定します。 このタスクは、`FormsResult`オブジェクトの内容をバイト配列に割り当てます。
   * `javax.servlet.http.HttpServletResponse`オブジェクトの`write`メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに送信します。 バイト配列を`write`メソッドに渡します。

**関連トピック**

[使用権限を付与されたFormsのレンダリング](#rendering-rights-enabled-forms)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
