---
title: 使用権限を付与されたフォームのレンダリング
seo-title: 使用権限を付与されたフォームのレンダリング
description: 'null'
seo-description: 'null'
uuid: ce5e4be6-d9b0-4989-a0e1-a8c3b98aed77
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d4c2b2f0-613a-409d-b39b-8e37fdb96eea
translation-type: tm+mt
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d

---


# 使用権限を付与されたフォームのレンダリング {#rendering-rights-enabled-forms}

Formsサービスは、使用権限が適用されたフォームをレンダリングできます。 使用権限は、Acrobat ではデフォルトで利用できるが Adobe Reader では利用できない機能（フォームにコメントを追加する機能や、フォームフィールドにデータを入力してフォームを保存する機能など）に関連しています。使用権限が適用されているフォームは、使用権限を付与されたフォームと呼ばれます。 使用権限を付与されたフォームをAdobe readerで開いたユーザーは、そのフォームに対して有効になっている操作を実行できます。

フォームに使用権限を適用するには、Acrobat Reader DCエクステンションサービスがAEM formsのインストールに含まれている必要があります。 また、PDFドキュメントに使用権限を適用できる有効な秘密鍵証明書が必要です。 つまり、使用権限を付与されたフォームをレンダリングする前に、Acrobat Reader DCエクステンションサービスを適切に設定する必要があります。 (Acrobat Reader DCエ [クステンションサービスについてを参照](/help/forms/developing/assigning-usage-rights.md#about-the-acrobat-reader-dc-extensions-service))。

>[!NOTE]
>
>使用権限を含むフォームをレンダリングするには、PDFファイルではなく、入力としてXDPファイルを使用する必要があります。 PDFファイルを入力として使用する場合、フォームはレンダリングされます。ただし、このフォームは使用権限を付与されたフォームではありません。

>[!NOTE]
>
>次の使用権限を指定する場合は、XMLデータを使用してフォームを自動埋め込むことはできません。 `enableComments`、 `enableCommentsOnline`、ま `enableEmbeddedFiles`たは `enableDigitalSignatures`、 (「編集可能な [レイアウトでのフォームの自動埋め込み](/help/forms/developing/prepopulating-forms-flowable-layouts.md)」を参照)。

>[!NOTE]
>
>For more information about the Forms service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## 手順の概要 {#summary-of-steps}

使用権限を付与されたフォームをレンダリングするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. フォームクライアントAPIオブジェクトを作成します。
1. 使用権限の実行時オプションを設定します。
1. 使用権限を付与されたフォームをレンダリングします。
1. 使用権限を付与されたフォームをクライアントWebブラウザーに書き込みます。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

**フォームクライアントAPIオブジェクトの作成**

プログラムでFormsサービスのClient API操作を実行する前に、Formsサービスクライアントを作成する必要があります。

**使用権限の実行時オプションの設定**

使用権限を付与されたフォームをレンダリングするには、使用権限の実行時オプションを設定する必要があります。 また、フォームに使用権限を適用するために使用する秘密鍵証明書のエイリアスも指定する必要があります。 エイリアス値を指定した後、フォームに適用する各使用権限を指定します。

**使用権限を付与されたフォームのレンダリング**

使用権限を付与されたフォームをレンダリングするには、使用権限のないフォームをレンダリングするのと同じアプリケーションロジックを使用します。 唯一の違いは、使用権限の実行時オプションがアプリケーションロジックに含まれていることを確認する必要がある点です。

>[!NOTE]
>
>Forms webサービスAPIを使用して使用権限を付与されたフォームをレンダリングする場合、フォームにファイルを添付することはできません。

**クライアントのWebブラウザーにフォームデータストリームを書き込みます**

Formsサービスは、使用権限を付与されたフォームをレンダリングすると、クライアントWebブラウザーに書き込む必要があるフォームデータストリームを返します。 クライアントのWebブラウザーに書き込まれると、フォームはユーザーに表示されます。 使用権限を付与されたフォームをAdobe readerで表示しているユーザーは、そのフォームに対して有効になっている操作を実行できます。

**関連トピック**

[Java APIを使用して権限を付与されたフォームをレンダリングする](#render-rights-enabled-forms-using-the-java-api)

[WebサービスAPIを使用して権限を付与されたフォームをレンダリングする](#render-rights-enabled-forms-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[FormsサービスAPIのクイックスタート](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[インタラクティブPDFフォームのレンダリング](/help/forms/developing/rendering-interactive-pdf-forms.md)

[フォームをレンダリングするWebアプリケーションの作成](/help/forms/developing/creating-web-applications-renders-forms.md)

### Java APIを使用して権限を付与されたフォームをレンダリングする {#render-rights-enabled-forms-using-the-java-api}

Forms API(Java)を使用して、使用権限を付与されたフォームをレンダリングします。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-forms-client.jarなどのクライアントJARファイルを含めます。

1. フォームクライアントAPIオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `FormsServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. 使用権限の実行時オプションの設定

   * コンストラクタを使用して `ReaderExtensionSpec` オブジェクトを作成します。
   * オブジェクトのメソッドを呼び出して秘密鍵証 `ReaderExtensionSpec` 明書のエイリアスを `setReCredentialAlias` 指定し、エイリアス値を表すstring値を指定します。
   * オブジェクトに属する対応するメソッドを呼び出して、各使用権限を設定 `ReaderExtensionSpec` します。 ただし、参照する秘密鍵証明書で許可されている場合にのみ、使用権限を設定できます。 つまり、秘密鍵証明書で設定が許可されていない場合は、使用権限を設定できません。 例えば、 ユーザーがフォームフィールドに入力してフォームを保存できる使用権限を設定するには、オブジェクトのメソッドを呼び出 `ReaderExtensionSpec` して、 `setReFillIn` 渡してくださ `true`い。
   >[!NOTE]
   >
   >オブジェクトのメソッドを呼び出す `ReaderExtensionSpec` 必要はあり `setReCredentialPassword` ません。 このメソッドは、Formsサービスでは使用されません。

1. 使用権限を付与されたフォームのレンダリング

   オブジェクト `FormsServiceClient` のメソッドを `renderPDFFormWithUsageRights` 呼び出し、次の値を渡します。

   * ファイル名の拡張子を含むフォームデザイン名を指定するstring値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、必ずなどの完全なパスを指定してくださ `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`い。
   * フォーム `com.adobe.idp.Document` とマージするデータを含むオブジェクトです。 データをマージしない場合は、空のオブジェクトを渡し `com.adobe.idp.Document` ます。
   * 実行時 `PDFFormRenderSpec` のオプションを格納するオブジェクトです。
   * 使用権 `ReaderExtensionSpec` 限の実行時オプションを格納するオブジェクトです。
   * Formsサ `URLSpec` ービスに必要なURI値を含むオブジェクトです。
   このメソ `renderPDFFormWithUsageRights` ッドは、クライア `FormsResult` ントのWebブラウザーに書き込む必要があるフォームデータストリームを含むオブジェクトを返します。

1. クライアントのWebブラウザーにフォームデータストリームを書き込みます

   * オブジェクトの `com.adobe.idp.Document` メソッドを呼び出して、オ `FormsResult` ブジェクトを作成 `getOutputContent` します。
   * メソッドを呼び出して、オブジェ `com.adobe.idp.Document` クトのコンテンツタイプを取得 `getContentType` します。
   * メソッドを呼 `javax.servlet.http.HttpServletResponse` び出し、オブジェクトのコンテンツタ `setContentType` イプを渡すことで、オブジェクトのコンテンツタイプを設定 `com.adobe.idp.Document` します。
   * オブジェクトの `javax.servlet.ServletOutputStream` メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに書き込むために使用する `javax.servlet.http.HttpServletResponse` オブジェクトを作 `getOutputStream` 成します。
   * オブジェクト `java.io.InputStream` のメソッドを呼び出して、オ `com.adobe.idp.Document` ブジェクトを作成 `getInputStream` します。
   * バイト配列を作成し、オブジェクトのメソッドを呼び出し、バイト配列を引 `InputStream` 数として渡すこ `read` とによって、フォームデータストリームを設定します。
   * オブジェクト `javax.servlet.ServletOutputStream` のメソッドを呼び `write` 出して、フォームデータストリームをクライアントWebブラウザーに送信します。 バイト配列をメソッドに渡し `write` ます。

**関連トピック**

[クイックスタート（SOAPモード）:Java APIを使用した権限付きフォームのレンダリング](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-rights-enabled-form-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## WebサービスAPIを使用して権限を付与されたフォームをレンダリングする {#render-rights-enabled-forms-using-the-web-service-api}

Forms API（Webサービス）を使用して、使用権限を付与されたフォームをレンダリングします。

1. プロジェクトファイルを含める

   * FormsサービスWSDLを使用するJavaプロキシクラスを作成します。
   * クラスパスにJavaプロキシクラスを含めます。

1. フォームクライアントAPIオブジェクトの作成

   オブジェクト `FormsService` を作成し、認証値を設定します。

1. 使用権限の実行時オプションの設定

   * コンストラクタを使用して `ReaderExtensionSpec` オブジェクトを作成します。
   * オブジェクトのメソッドを呼び出して秘密鍵証 `ReaderExtensionSpec` 明書のエイリアスを `setReCredentialAlias` 指定し、エイリアス値を表すstring値を指定します。
   * オブジェクトに属する対応するメソッドを呼び出して、各使用権限を設定 `ReaderExtensionSpec` します。 ただし、参照する秘密鍵証明書で許可されている場合にのみ、使用権限を設定できます。 つまり、秘密鍵証明書で設定が許可されていない場合は、使用権限を設定できません。 ユーザーがフォームフィールドに入力してフォームを保存できる使用権限を設定するには、オブジェクトのメソッド `ReaderExtensionSpec` を呼び出して `setReFillIn` 渡しま `true`す。

1. 使用権限を付与されたフォームのレンダリング

   オブジェクト `FormsService` のメソッドを `renderPDFFormWithUsageRights` 呼び出し、次の値を渡します。

   * ファイル名の拡張子を含むフォームデザイン名を指定するstring値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、必ずなどの完全なパスを指定してくださ `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`い。
   * フォーム `BLOB` とマージするデータを含むオブジェクトです。 データをフォームとマージしない場合は、空のXMLデータソースに基づ `BLOB` くオブジェクトを渡す必要があります。 nullのオブジェクトを渡すこ `BLOB` とはできません。それ以外の場合は、例外がスローされます。
   * 実行時 `PDFFormRenderSpec` のオプションを格納するオブジェクトです。
   * 使用権 `ReaderExtensionSpec` 限の実行時オプションを格納するオブジェクトです。
   * Formsサ `URLSpec` ービスに必要なURI値を含むオブジェクトです。
   このメソ `renderPDFFormWithUsageRights` ッドは、クライア `FormsResult` ントのWebブラウザーに書き込む必要があるフォームデータストリームを含むオブジェクトを返します。

1. クライアントのWebブラウザーにフォームデータストリームを書き込みます

   * オブジェクトの `BLOB` メソッドを呼び出して、フォームデータを含むオ `FormsResult` ブジェクトを作成 `getOutputContent` します。
   * メソッドを呼び出して、オブジェ `BLOB` クトのコンテンツタイプを取得 `getContentType` します。
   * メソッドを呼 `javax.servlet.http.HttpServletResponse` び出し、オブジェクトのコンテンツタ `setContentType` イプを渡すことで、オブジェクトのコンテンツタイプを設定 `BLOB` します。
   * オブジェクトの `javax.servlet.ServletOutputStream` メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに書き込むために使用する `javax.servlet.http.HttpServletResponse` オブジェクトを作 `getOutputStream` 成します。
   * バイト配列を作成し、オブジェクトのメソッドを呼び出 `BLOB` して値を設定 `getBinaryData` します。 このタスクは、オブジェクトの内容をバ `FormsResult` イト配列に割り当てます。
   * オブジェクト `javax.servlet.http.HttpServletResponse` のメソッドを呼び `write` 出して、フォームデータストリームをクライアントWebブラウザーに送信します。 バイト配列をメソッドに渡し `write` ます。

**関連トピック**

[使用権限を付与されたフォームのレンダリング](#rendering-rights-enabled-forms)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
