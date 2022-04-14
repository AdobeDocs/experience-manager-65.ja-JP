---
title: 権限付きフォームのレンダリング
seo-title: Rendering Rights-Enabled Forms
description: Forms サービスを使用して、使用権限が適用されているフォームをレンダリングします。Java API および web サービス API を使用して、権限付きフォームをレンダリングできます。
seo-description: Use the Forms service to render forms that have usage rights applied to them. You can render rights-enabled forms using the Java API and Web Service API.
uuid: ce5e4be6-d9b0-4989-a0e1-a8c3b98aed77
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d4c2b2f0-613a-409d-b39b-8e37fdb96eea
role: Developer
exl-id: 012a3a9f-542c-4ed1-a092-572bfccbdf21
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '1463'
ht-degree: 100%

---

# 権限付きフォームのレンダリング {#rendering-rights-enabled-forms}

Forms サービスでは、使用権限が適用されているフォームをレンダリングできます。使用権限は、Acrobat ではデフォルトで利用できるが Adobe Reader では利用できない機能（フォームにコメントを追加する機能や、フォームフィールドにデータを入力してフォームを保存する機能など）に関連しています。使用権限が適用されたフォームは、権限付きフォームと呼ばれます。ユーザーは、権限付きフォームを Adobe Reader で開くことで、そのフォームで有効になっている操作を実行できます。

使用権限をフォームに適用するには、Acrobat Reader DC Extensions サービスが AEM forms のインストール環境に含まれている必要があります。また、使用権限を PDF ドキュメントに適用できる有効な資格情報が必要です。つまり、権限付きフォームをレンダリングするには、Acrobat Reader DC Extensions サービスを適切に設定する必要があります。（[Acrobat Reader DC Extensions サービスについて](/help/forms/developing/assigning-usage-rights.md#about-the-acrobat-reader-dc-extensions-service)を参照してください）。

>[!NOTE]
>
>使用権限を含むフォームをレンダリングするには、PDF ファイルではなく XDP ファイルを入力として使用する必要があります。PDF ファイルを入力として使用した場合、フォームのレンダリングは可能ですが、権限付きフォームにはなりません。

>[!NOTE]
>
>`enableComments`、`enableCommentsOnline`、`enableEmbeddedFiles` または `enableDigitalSignatures` の使用権限を指定する場合、フォームに XML データを事前入力することはできません。（[編集可能なレイアウトを使用した Forms の事前入力](/help/forms/developing/prepopulating-forms-flowable-layouts.md)を参照してください）。

>[!NOTE]
>
>Forms サービスについて詳しくは、[AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

## 手順の概要 {#summary-of-steps}

権限付きフォームをレンダリングするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Forms Client API オブジェクトを作成します。
1. 使用権限の実行時オプションを設定します。
1. 権限付きフォームをレンダリングします。
1. 権限付きフォームをクライアント web ブラウザーに書き込みます。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**Forms Client API オブジェクトの作成**

Forms サービス Client API 操作をプログラムで実行には、事前に Forms サービスクライアントを作成しておく必要があります。

**使用権限の実行時オプションの設定**

権限付きフォームをレンダリングするには、使用権限の実行時オプションを設定する必要があります。また、使用権限をフォームに適用するために使用する資格情報のエイリアスも指定する必要があります。エイリアス値を指定したら、フォームに適用する各使用権限を指定します。

**権限付きフォームのレンダリング**

権限付きフォームをレンダリングするには、使用権限のないフォームをレンダリングする場合と同じアプリケーションロジックを使用します。唯一の違いは、使用権限の実行時オプションがアプリケーションロジックに含まれていることを確認する必要がある点です。

>[!NOTE]
>
>Forms web サービス API を使用して権限付きフォームをレンダリングする場合、フォームにファイルを添付することはできません。

**フォームデータストリームをクライアント web ブラウザーに書き込む**

Forms サービスが権限付きフォームをレンダリングすると、クライアント web ブラウザーに書き込む必要があるフォームデータストリームが返されます。クライアント web ブラウザーに書き込まれると、ユーザーはフォームを表示できます。Adobe Reader で権限付きフォームを表示しているユーザーは、そのフォームで有効になっている操作を実行できます。

**関連トピック**

[Java API を使用して権限付きフォームをレンダリングする](#render-rights-enabled-forms-using-the-java-api)

[Web サービス API を利用したライツ対応フォームのレンダリング](#render-rights-enabled-forms-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms サービス API のクイックスタート](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[インタラクティブ PDF Forms のレンダリング](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Forms をレンダリングする web アプリケーションの作成](/help/forms/developing/creating-web-applications-renders-forms.md)

### Java API を使用して権限付きフォームをレンダリングする {#render-rights-enabled-forms-using-the-java-api}

Forms API（Java）を使用して、権限付きフォームをレンダリングします。

1. プロジェクトファイルを含める

   adobe-forms-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. Forms Client API オブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用し、`ServiceClientFactory` オブジェクトを渡すことによって、`FormsServiceClient` オブジェクトを作成します。

1. 使用権限の実行時オプションを設定する

   * コンストラクタを使用して `ReaderExtensionSpec` オブジェクトを作成します。
   * `ReaderExtensionSpec` オブジェクトの `setReCredentialAlias` メソッドを呼び出し、エイリアス値を表す文字列値を指定することによって、資格情報のエイリアスを指定します。
   * `ReaderExtensionSpec` オブジェクトに属する対応するメソッドを呼び出して、各使用権限を設定します。ただし、使用権限を設定できるのは、参照する秘密鍵証明書でその権限が与えられている場合のみです。つまり、秘密鍵証明書で設定が許可されていない場合は、使用権限を設定できません。以下に例を示します。で、ユーザーがフォームのフィールドに入力して保存できる使用権を設定するには、`ReaderExtensionSpec` オブジェクトの `setReFillIn` メソッドを呼び出し、`true` を渡します。

   >[!NOTE]
   >
   >`ReaderExtensionSpec` オブジェクトの `setReCredentialPassword` メソッドを呼び出す必要はありません。このメソッドは、Forms サービスでは使用されません。

1. 権限設定されたフォームをレンダリングする

   `FormsServiceClient` オブジェクトの `renderPDFFormWithUsageRights` メソッドを呼び出して、次の値を渡します。

   * フォームデザイン名を指定する文字列値で、ファイル名の拡張子も含まれます。Forms アプリケーションの一部であるフォームデザインを参照する場合は、`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp` のように完全なパスを指定するようにしてください。
   * フォームと結合するデータを格納する `com.adobe.idp.Document` オブジェクト。データを結合しない場合は、空の `com.adobe.idp.Document` オブジェクトを渡します。
   * ランタイムオプションを格納する `PDFFormRenderSpec` オブジェクトです。
   * 使用権限の実行時オプションを格納する `ReaderExtensionSpec` オブジェクトです。
   * Forms サービスで必要な URI 値を格納する `URLSpec` オブジェクトです。

   `renderPDFFormWithUsageRights` メソッドは、クライアントの web ブラウザーに書き込まれなければならないフォームデータストリームを含む `FormsResult` オブジェクトを返します。

1. フォームデータストリームをクライアント web ブラウザーに書き込む

   * `FormsResult` オブジェクトの `getOutputContent` メソッドを呼び出して、`com.adobe.idp.Document` オブジェクトを作成します。
   * `com.adobe.idp.Document`オブジェクトの `getContentType` メソッドを呼び出して、そのコンテンツタイプを取得します。
   * `javax.servlet.http.HttpServletResponse`オブジェクトの `setContentType` メソッドを呼び出してコンテンツタイプを設定し、`com.adobe.idp.Document` オブジェクトのコンテンツタイプを渡します。
   * `javax.servlet.http.HttpServletResponse` オブジェクトの `getOutputStream` メソッドを呼び出して、クライアントの web ブラウザーにフォームデータストリームを書き込むために使用される `javax.servlet.ServletOutputStream` オブジェクトを作成します。
   * `com.adobe.idp.Document` オブジェクトの `getInputStream` メソッドを呼び出して、`java.io.InputStream` オブジェクトを作成します。
   * バイト配列を作成し、`InputStream` オブジェクトの `read` メソッドを呼び出して、引数としてバイト配列を渡すことで、フォームデータのストリームをその中に取り込みます。
   * `javax.servlet.ServletOutputStream` オブジェクトの `write` メソッドを呼び出して、フォームデータストリームをクライアント web ブラウザーに送信します。 バイト配列を `write` メソッドに渡します。

**関連トピック**

[クイックスタート（SOAP モード）：Java API を使用した権限が有効なフォームのレンダリング](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-rights-enabled-form-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Web サービス API を利用したライツ対応フォームのレンダリング {#render-rights-enabled-forms-using-the-web-service-api}

Forms API（web サービス）を使用して、権限が有効なフォームをレンダリングします。

1. プロジェクトファイルを含める

   * Forms Service WSDL を使用する Java プロキシクラスを作成します。
   * Java プロキシクラスをクラスパスに含めます。

1. Forms Client API オブジェクトの作成

   `FormsService` オブジェクトを作成し、認証値を設定します。

1. 使用権限の実行時オプションを設定する

   * コンストラクターを使用して `ReaderExtensionSpec` オブジェクトを作成します。
   * `ReaderExtensionSpec` オブジェクトの `setReCredentialAlias` メソッドを呼び出して、秘密鍵証明書のエイリアスを指定し、そのエイリアスの値を表す文字列値を指定します。
   * `ReaderExtensionSpec` オブジェクトに属する対応するメソッドを呼び出して、各使用権限を設定します。ただし、使用権限を設定できるのは、参照する秘密鍵証明書でその権限が与えられている場合のみです。つまり、秘密鍵証明書で設定が許可されていない場合は、使用権限を設定できません。ユーザーがフォームフィールドに入力し、フォームを保存できる使用権を設定するには、`ReaderExtensionSpec` オブジェクトの `setReFillIn` メソッドを呼び出し、`true` を渡します。

1. 権限設定されたフォームをレンダリングする

   `FormsService` オブジェクトの `renderPDFFormWithUsageRights` メソッドを呼び出して、次の値を渡します。

   * フォームデザイン名を指定する文字列値で、ファイル名の拡張子も含まれます。Forms アプリケーションの一部であるフォームデザインを参照する場合は、`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp` のように完全なパスを指定することを確認してください。
   * フォームで結合するデータを格納する `BLOB` オブジェクト。フォームでデータを結合しない場合は、空の XML データソースを基にした `BLOB` オブジェクトを渡す必要があります。null の `BLOB` オブジェクトを渡すことはできません。このようなオブジェクトを渡すと例外が発生します。
   * ランタイムオプションを格納する `PDFFormRenderSpec` オブジェクト。
   * 使用権のランタイムオプションを格納する `ReaderExtensionSpec` オブジェクト。
   * Forms サービスが必要とする URI 値を格納した `URLSpec` オブジェクト。

   `renderPDFFormWithUsageRights` メソッドは、クライアントの web ブラウザーに書き込まれなければならないフォームデータストリームを含む`FormsResult` オブジェクトを返します。

1. フォームデータストリームをクライアント web ブラウザーに書き込む

   * `FormsResult` オブジェクトの `getOutputContent` メソッドを呼び出して、フォームデータを格納する `BLOB` オブジェクトを作成します。
   * `BLOB` オ ブジェクトの `getContentType` メソッドを呼び出して、そのコンテンツタイプを取得します。
   * `javax.servlet.http.HttpServletResponse` オブジェクトの `setContentType` メソッドを呼び出して、そのコンテンツタイプを設定し、`BLOB` オブジェクトのコンテンツタイプを渡します。
   * `javax.servlet.http.HttpServletResponse` オブジェクトの `getOutputStream` メソッドを呼び出して、クライアントの web ブラウザーにフォームデータストリームを書き込むために使用される `javax.servlet.ServletOutputStream` オブジェクトを作成します。
   * バイト配列を作成し、`BLOB` オブジェクトの `getBinaryData` メソッドを呼び出して、バイト配列を投入します。このタスクは、`FormsResult` オブジェクトの内容をバイト配列に入力します。
   * `javax.servlet.http.HttpServletResponse` オブジェクトの `write` メソッドを呼び出して、フォームデータストリームをクライアント web ブラウザーに送信します。バイト配列を `write` メソッドに渡します。

**関連トピック**

[権限付きフォームのレンダリング](#rendering-rights-enabled-forms)

[Base64 エンコーディングを使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
