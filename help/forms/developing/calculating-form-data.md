---
title: フォームデータの計算
seo-title: フォームデータの計算
description: 'null'
seo-description: 'null'
uuid: ccd85bc7-8ccc-44d9-9424-dfc1f603e688
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: b4f57e42-60a6-407d-9764-15a11615827d
translation-type: tm+mt
source-git-commit: 4b9e2ceafc301db9337868b78bcae87c0f07e14b

---


# フォームデータの計算 {#calculating-form-data}

Formsサービスでは、ユーザーがフォームに入力した値を計算し、結果を表示できます。 フォームデータを計算するには、2つのタスクを実行する必要があります。 まず、フォームデータを計算するフォームデザインスクリプトを作成します。 フォームデザインは3種類のスクリプトをサポートしています。 1つのスクリプトタイプはクライアントで実行し、もう1つはサーバーで実行し、3つ目はサーバーとクライアントの両方で実行します。 このトピックで説明するスクリプトタイプは、サーバー上で実行されます。 サーバー側の計算は、HTML、PDFおよびフォームガイド（非推奨）の変換でサポートされています。

フォームデザインプロセスの一環として、演算とスクリプトを使用し、より豊かなユーザーエクスペリエンスを提供できます。 演算とスクリプトは、フォームのほとんどのフィールドとオブジェクトに追加できます。 ユーザーがインタラクティブフォームに入力したデータに対して演算操作を実行するには、フォームデザインスクリプトを作成する必要があります。

ユーザーはフォームに値を入力し、「Calculate」ボタンをクリックして結果を表示します。 次のプロセスでは、ユーザーがデータを計算できるアプリケーションの例を説明します。

* ユーザーは、Webアプリケーションの開始ページとして機能するStartLoan.htmlというHTMLページにアクセスします。 このページは、という名前のJavaサーブレットを呼び出しま `GetLoanForm`す。
* サーブレット `GetLoanForm` はローンフォームをレンダリングします。 このフォームには、スクリプト、インタラクティブフィールド、計算ボタン、送信ボタンが含まれています。
* ユーザーがフォームのフィールドに値を入力し、「計算」ボタンをクリックします。 フォームがJavaサーブレットに送信さ `CalculateData` れ、スクリプトが実行されます。 計算結果がフォームに表示された状態で、フォームがユーザーに返されます。
* ユーザは、満足のいく結果が表示されるまで値の入力と計算を続けます。 ユーザーは、問題がない場合に「送信」ボタンをクリックしてフォームを処理します。 送信されたデータを取得する別のJavaサーブレット `ProcessForm` に、フォームが送信されます。 (「送信済み [フォームの処理](/help/forms/developing/rendering-forms.md#handling-submitted-forms)」を参照)。


次の図に、アプリケーションのロジックフローを示します。

![cf_cf_finsrv_loancalcapp_v1](assets/cf_cf_finsrv_loancalcapp_v1.png)

次の表に、この図の手順を示します。

<table>
 <thead>
  <tr>
   <th><p>ステップ</p></th>
   <th><p>説明</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>HTMLの開 <code>GetLoanForm</code> 始ページからJavaサーブレットが呼び出されます。 </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Javaサーブ <code>GetLoanForm</code> レットは、FormsサービスクライアントAPIを使用して、ローンフォームをクライアントWebブラウザーにレンダリングします。 サーバーで実行するように設定されたスクリプトを含むフォームをレンダリングする場合と、スクリプトを含まないフォームをレンダリングする場合の違いは、スクリプトの実行に使用するターゲットの場所を指定する必要がある点です。 ターゲットの場所を指定しない場合、サーバー上で実行するように設定されたスクリプトは実行されません。 例えば、この節で紹介したアプリケーションについて考えてみましょう。 Javaサーブ <code>CalculateData</code> レットは、スクリプトが実行されるターゲットの場所です。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>ユーザーがインタラクティブフィールドにデータを入力し、「計算」ボタンをクリックします。 フォームが <code>CalculateData</code> Javaサーブレットに送信され、スクリプトが実行されます。 </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>フォームがWebブラウザーにレンダリングされ、計算結果がフォームに表示されます。 </p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>値が満足できる場合は、ユーザーが「送信」ボタンをクリックします。 フォームは、という名前の別のJavaサーブレットに送信されま <code>ProcessForm</code>す。</p></td>
  </tr>
 </tbody>
</table>

通常、PDFコンテンツとして送信されるフォームには、クライアント上で実行されるスクリプトが含まれます。 ただし、サーバー側の計算も実行できます。 「送信」ボタンは、スクリプトの計算には使用できません。 この場合、Formsサービスはインタラクションが完了したと見なすので、計算は実行されません。

フォームデザインスクリプトの使用を説明するために、この節では、サーバー上で実行するように設定されたスクリプトを含むシンプルなインタラクティブフォームについて調べます。 次の図は、ユーザーが最初の2つのフィールドに入力した値を加算し、その結果を3つ目のフィールドに表示するスクリプトを含むフォームデザインを示しています。

![cf_cf_caldata](assets/cf_cf_caldata.png)

******A.NumericField1** Bという名前のフィールド。NumericField2 **C.** numericField3という名前のフィールド

このフォームデザインにあるスクリプトの構文は次のとおりです。

```as3
     NumericField3 = NumericField2 + NumericField1
```

このフォームデザインでは、「計算」ボタンはコマンドボタンで、スクリプトはこのボタンのイベント内にあ `Click` ります。 ユーザーが最初の2つのフィールド（NumericField1とNumericField2）に値を入力し、「Calculate」ボタンをクリックすると、フォームがFormsサービスに送信され、スクリプトが実行されます。 Formsサービスは、計算の結果をNumericField3フィールドに表示して、フォームをクライアントデバイスにレンダリングし直します。

>[!NOTE]
>
>フォームデザインスクリプトの作成について詳しくは、「 [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)」を参照してください。

>[!NOTE]
>
>For more information about the Forms service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## 手順の概要 {#summary-of-steps}

フォームデータを計算するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. フォームクライアントAPIオブジェクトを作成します。
1. 演算スクリプトを含むフォームを取得します。
1. フォームデータストリームをクライアントWebブラウザーに書き戻します

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

**フォームクライアントAPIオブジェクトの作成**

プログラムでFormsサービスのClient API操作を実行する前に、Formsサービスクライアントを作成する必要があります。 Java APIを使用している場合は、オブジェクトを作成し `FormsServiceClient` ます。 Forms webサービスAPIを使用している場合は、オブジェクトを作成し `FormsServiceService` ます。

**演算スクリプトを含むフォームの取得**

FormsサービスクライアントAPIを使用して、サーバー上で実行するように設定されたスクリプトを含むフォームを処理するアプリケーションロジックを作成します。 このプロセスは、送信されたフォームの処理と似ています。 (送信済 [みのフォームの処理](/help/forms/developing/rendering-forms-rendering-forms handling-submitted-forms-handling-submitted.md#handling-submitted-forms)を参照)。

送信されたフォームに関連付けられている処理状態が、 `1``(Calculate)`Formsサービスがフォームデータに対して計算操作を実行し、結果をユーザーに書き戻す必要があることを確認します。 この場合、サーバー上で実行するように設定されたスクリプトが自動的に実行されます。

**フォームデータストリームをクライアントWebブラウザーに書き戻します**

送信されたフォームに関連付けられている処理状態が確認され `1`たら、結果をクライアントのWebブラウザーに書き戻す必要があります。 フォームが表示されると、計算された値が適切なフィールドに表示されます。

**関連項目**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
Java APIを使用した[Calculateフォームデータの計算WebサービスAPI](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-java-api)[](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-web-service-api)Connection Propertiesの設定接続プロパティの設定Forms Service API Starts apiインタラクティブ[](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)[](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)[](/help/forms/developing/rendering-interactive-pdf-forms.md)[Rendering Interactive Forms Applications Web Forms Renders](/help/forms/developing/creating-web-applications-renders-forms.md)

## Java APIを使用してフォームデータを計算する {#calculate-form-data-using-the-java-api}

Forms API(Java)を使用してフォームデータを計算します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-forms-client.jarなどのクライアントJARファイルを含めます。

1. フォームクライアントAPIオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `FormsServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. 演算スクリプトを含むフォームの取得

   * 演算スクリプトを含むフォームデータを取得するには、コンストラクターを使用し `com.adobe.idp.Document` てオブジェクトを作成し、コンストラクター内からオ `javax.servlet.http.HttpServletResponse` ブジェクトの `getInputStream` メソッドを呼び出します。
   * オブジェクト `FormsServiceClient` のメソッドを `processFormSubmission` 呼び出し、次の値を渡します。

      * フォーム `com.adobe.idp.Document` データを含むオブジェクトです。
      * すべての関連するHTTPヘッダーを含む環境変数を指定するstring値。 環境変数に1つ以上の値を指定して、処理するコンテンツタイプを指定する必要 `CONTENT_TYPE` があります。 例えば、XMLおよびPDFデータを処理するには、このパラメーターに次の文字列値を指定します。 `CONTENT_TYPE=application/xml&CONTENT_TYPE=application/pdf`
      * ヘッダー値を指定す `HTTP_USER_AGENT` るstring値。例えば、 `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * 実行時 `RenderOptionsSpec` のオプションを格納するオブジェクトです。
      このメ `processFormSubmission` ソッドは、フォー `FormsResult` ム送信の結果を含むオブジェクトを返します。

   * 送信されたフォームに関連付けられた処理状態が、オブジェクトのメ `1` ソッドを呼び出して `FormsResult` いることを確認 `getAction` します。 このメソッドが値を返す場合、 `1`計算が実行され、データをクライアントWebブラウザーに書き戻すことができます。


1. フォームデータストリームをクライアントWebブラウザーに書き戻します

   * フォームデー `javax.servlet.ServletOutputStream` タストリームをクライアントWebブラウザーに送信するために使用するオブジェクトを作成します。
   * オブジェクトの `com.adobe.idp.Document` メソッドを呼び出して、オ `FormsResult` ブジェクトを作成 `getOutputContent` します。
   * オブジェクト `java.io.InputStream` のメソッドを呼び出して、オ `com.adobe.idp.Document` ブジェクトを作成 `getInputStream` します。
   * バイト配列を作成し、オブジェクトのメソッドを呼び出し、バイト配列を引数 `InputStream` として渡すこ `read` とで、フォームデータストリームを設定します。
   * オブジェクト `javax.servlet.ServletOutputStream` のメソッドを呼び `write` 出して、フォームデータストリームをクライアントWebブラウザーに送信します。 バイト配列をメソッドに渡し `write` ます。

**関連項目**


[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## WebサービスAPIを使用してフォームデータを計算する {#calculate-form-data-using-the-web-service-api}

Forms API（Webサービス）を使用してフォームデータを計算します。

1. プロジェクトファイルを含める

   * FormsサービスWSDLを使用するJavaプロキシクラスを作成します。
   * クラスパスにJavaプロキシクラスを含めます。

1. フォームクライアントAPIオブジェクトの作成

   オブジェクト `FormsService` を作成し、認証値を設定します。

1. 演算スクリプトを含むフォームの取得

   * Javaサーブレットにポストされたフォームデータを取得するには、コンストラクタを使 `BLOB` 用してオブジェクトを作成します。
   * オブジェクト `java.io.InputStream` のメソッドを使用して、オ `javax.servlet.http.HttpServletResponse` ブジェクトを作成 `getInputStream` します。
   * Create a `java.io.ByteArrayOutputStream` object by using its constructor and passing the length of the `java.io.InputStream` object.
   * オブジェクトの内容をオ `java.io.InputStream` ブジェクトにコピ `java.io.ByteArrayOutputStream` ーします。
   * オブジェクトのメソッドを呼び出して、バ `java.io.ByteArrayOutputStream` イト配列を作成 `toByteArray` します。
   * メソッドを呼 `BLOB` び出し、バイト配列を `setBinaryData` 引数として渡すことで、オブジェクトを設定します。
   * コンストラクタを使用して `RenderOptionsSpec` オブジェクトを作成します。オブジェクトのメソッドを呼び出し、ロ `RenderOptionsSpec` ケール値を指 `setLocale` 定する文字列値を渡して、ロケール値を設定します。
   * オブジェクト `FormsServiceClient` のメソッドを `processFormSubmission` 呼び出し、次の値を渡します。

      * フォーム `BLOB` データを含むオブジェクトです。
      * 関連するすべてのHTTPヘッダーが含まれる環境変数を指定するstring値。 例えば、次の文字列値を指定できます。 `HTTP_REFERER=referrer&HTTP_CONNECTION=keep-alive&CONTENT_TYPE=application/xml`
      * ヘッダー値を指定す `HTTP_USER_AGENT` るstring値。例えば、 `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * 実行時 `RenderOptionsSpec` のオプションを格納するオブジェクトです。 その他の情報, .
      * メソッドに `BLOBHolder` よって入力される空のオブジェクトです。
      * メソッドに `javax.xml.rpc.holders.StringHolder` よって入力される空のオブジェクトです。
      * メソッドに `BLOBHolder` よって入力される空のオブジェクトです。
      * メソッドに `BLOBHolder` よって入力される空のオブジェクトです。
      * メソッドに `javax.xml.rpc.holders.ShortHolder` よって入力される空のオブジェクトです。
      * メソッドに `MyArrayOf_xsd_anyTypeHolder` よって入力される空のオブジェクトです。 このパラメーターは、フォームと共に送信される添付ファイルを保存するために使用されます。
      * 送信され `FormsResultHolder` たフォームを含む、メソッドによって入力される空のオブジェクト。
      メソッ `processFormSubmission` ドは、フォー `FormsResultHolder` ム送信の結果をパラメーターに入力します。 このメ `processFormSubmission` ソッドは、フォー `FormsResult` ム送信の結果を含むオブジェクトを返します。

   * 送信されたフォームに関連付けられた処理状態が、オブジェクトのメ `1` ソッドを呼び出して `FormsResult` いることを確認 `getAction` します。 このメソッドが値を返す場合、 `1`計算が実行され、データをクライアントWebブラウザーに書き戻すことができます。


1. フォームデータストリームをクライアントWebブラウザーに書き戻します

   * フォームデー `javax.servlet.ServletOutputStream` タストリームをクライアントWebブラウザーに送信するために使用するオブジェクトを作成します。
   * オブジェクトの `BLOB` メソッドを呼び出して、フォームデータを含むオ `FormsResult` ブジェクトを作成 `getOutputContent` します。
   * バイト配列を作成し、オブジェクトのメソッドを呼び出 `BLOB` して値を設定 `getBinaryData` します。 このタスクは、オブジェクトの内容をバ `FormsResult` イト配列に割り当てます。
   * オブジェクト `javax.servlet.http.HttpServletResponse` のメソッドを呼び `write` 出して、フォームデータストリームをクライアントWebブラウザーに送信します。 バイト配列をメソッドに渡し `write` ます。

**「Base64エンコーデ**[ィングを使用したAEM Formsの呼び出し」も参照してください。](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
