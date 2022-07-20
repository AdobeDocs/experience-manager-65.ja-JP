---
title: フォームデータの計算
seo-title: Calculating Form Data
description: Forms サービスを使用して、ユーザーがフォームに入力した値を計算し、結果を表示します。Forms サービスは、Java API および Web サービス API を使用して値を計算します。
seo-description: Use the Forms service to calculate values that a user enters into a form and display the results. Forms service calculates the values using the Java API and Web Service API.
uuid: ccd85bc7-8ccc-44d9-9424-dfc1f603e688
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: operations
discoiquuid: b4f57e42-60a6-407d-9764-15a11615827d
role: Developer
exl-id: 28abf044-6c8e-4578-ae2e-54cdbd694c5f
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '1882'
ht-degree: 100%

---

# フォームデータの計算 {#calculating-form-data}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

Forms サービスでは、ユーザーがフォームに入力した値を計算し、結果を表示できます。フォームデータを計算するには、2 つのタスクを実行する必要があります。まず、フォームデータを計算するフォームデザインスクリプトを作成します。フォームデザインは、3 つのタイプのスクリプトをサポートしています。1 つのスクリプトタイプはクライアントで実行され、もう 1 つはサーバーで実行され、3 つ目のタイプはサーバーとクライアントの両方で実行されます。このトピックで説明するスクリプトタイプは、サーバー上で実行されます。HTML、PDF、Form Guide（非推奨）の変換では、サーバーサイドの計算がサポートされます。

フォームデザインプロセスの一環として、演算とスクリプトを活用して、よりリッチなユーザーエクスペリエンスを提供できます。演算とスクリプトは、ほとんどのフォームフィールドとオブジェクトに追加できます。ユーザーがインタラクティブフォームに入力したデータに対して計算操作を実行するには、フォームデザインスクリプトを作成する必要があります。

ユーザーがフォームに値を入力して「計算」ボタンをクリックし、結果を表示します。次のプロセスは、ユーザーがデータを計算できるサンプルアプリケーションを示しています。

* ユーザーが、web アプリケーションの開始ページとして機能する StartLoan.html という名前の HTML ページにアクセスします。このページは、`GetLoanForm` という名前の Java サーブレットを呼び出します。
* `GetLoanForm` サーブレットは、ローンフォームをレンダリングします。このフォームには、スクリプト、インタラクティブフィールド、計算ボタン、送信ボタンが含まれています。
* ユーザーがフォームのフィールドに値を入力し、「計算」ボタンをクリックします。フォームは、スクリプトが実行される `CalculateData` Java サーブレットに送信されます。計算結果がフォームに表示された状態で、フォームがユーザーに送り返されます。
* ユーザーは、満足のいく結果が表示されるまで、値の入力と計算を続行します。満足したら、ユーザーは「送信」ボタンをクリックして、フォームを処理します。フォームは、送信されたデータの取得を担当する `ProcessForm` という名前の別の Java サーブレットに送信されます（[送信済みフォームの処理](/help/forms/developing/rendering-forms.md#handling-submitted-forms)を参照）。


次の図に、アプリケーションのロジック・フローを示します。

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
   <td><p><code>GetLoanForm</code> Java サーブレットは、HTML 開始ページから呼び出されます。 </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p><code>GetLoanForm</code> Java サーブレットは、Forms Service Client API を使用して、クライアント web ブラウザーにローンフォームをレンダリングします。サーバー上で実行するように設定されたスクリプトを含むフォームのレンダリングと、スクリプトを含まないフォームのレンダリングの違いは、スクリプトの実行に使用されるターゲットの場所を指定する必要があることです。ターゲットの場所が指定されていない場合、サーバー上で実行するように設定されたスクリプトは実行されません。例えば、この節で紹介するアプリケーションについて考えてみましょう。<code>CalculateData</code> Java サーブレットは、スクリプトが実行されるターゲットの場所です。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>ユーザーがインタラクティブフィールドにデータを入力して、「計算」ボタンをクリックします。フォームが <code>CalculateData</code> Java サーブレットに送信され、スクリプトがそこで実行されます。 </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>計算結果がフォームに表示された状態で、フォームが web ブラウザーにレンダリングされます。 </p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>ユーザーは、値に満足したら、「送信」ボタンをクリックします。フォームは、<code>ProcessForm</code> という名前の別の Java サーブレットに送信されます。</p></td>
  </tr>
 </tbody>
</table>

通常、PDF コンテンツとして送信されるフォームには、クライアント上で実行されるスクリプトが含まれます。ただし、サーバーサイドの計算を実行することもできます。「送信」ボタンは、スクリプトの計算には使用できません。この場合、Forms サービスはインタラクションが完了すると見なすので、計算は実行されません。

フォームデザインスクリプトの使用方法を説明するために、この節では、サーバー上で実行するように設定されたスクリプトを含むシンプルなインタラクティブフォームについて見ていきます。次の図は、ユーザーが最初の 2 つのフィールドに入力した値を加算し、その結果を 3 番目のフィールドに表示するスクリプトを含むフォームデザインを示しています。

![cf_cf_caldata](assets/cf_cf_caldata.png)

**A.** NumericField1 という名前のフィールド **B.** NumericField2 という名前のフィールド **C.** NumericField3 という名前のフィールド

このフォームデザインに配置されるスクリプトの構文は次のとおりです。

```javascript
     NumericField3 = NumericField2 + NumericField1
```

このフォームデザインでは、「計算」ボタンはコマンドボタンであり、スクリプトはこのボタンの `Click` イベントに配置されています。ユーザーが最初の 2 つのフィールド（NumericField1 および NumericField2）に値を入力して「計算」ボタンをクリックすると、フォームが Forms サービスに送信され、スクリプトが実行されます。Forms サービスは、NumericField3 フィールドに表示された計算結果を使用して、フォームをクライアントデバイスにレンダリングし直します。

>[!NOTE]
>
>フォームデザインスクリプトの作成について詳しくは、[Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63_jp)を参照してください。

>[!NOTE]
>
>Forms サービスについて詳しくは、[AEM Forms サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

## 手順の概要 {#summary-of-steps}

フォームデータを計算するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Forms Client API オブジェクトを作成します。
1. 計算スクリプトを含むフォームを取得します。
1. フォームデータストリームをクライアントの web ブラウザーに書き戻します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**Forms Client API オブジェクトの作成**

Forms Service Client API 操作をプログラムで実行する前に、Forms サービスクライアントを作成する必要があります。Java API を使用している場合は、`FormsServiceClient` オブジェクトを作成します。Forms web サービス API を使用している場合は、`FormsServiceService` オブジェクトを作成します。

**計算スクリプトを含むフォームの取得**

Forms サービスのクライアント API を使用して、サーバー上で実行するように設定されたスクリプトを含むフォームを処理するアプリケーションロジックを作成します。このプロセスは、送信されたフォームの処理に似ています。（[送信済みフォームの処理](/help/forms/developing/handling-submitted-forms.md)を参照。）

送信されたフォームに関連付けられた処理状態が `1` `(Calculate)` であることを確認します。これは、Forms サービスがフォームデータに対して計算操作を実行しており、結果をユーザーに書き戻す必要があることを意味します。この場合、サーバー上で実行するように設定されたスクリプトが自動的に実行されます。

**フォームデータストリームをクライアントの web ブラウザーに書き戻す**

送信されたフォームに関連付けられている処理状態が `1` の場合は、結果をクライアント web ブラウザーに書き戻す必要があります。フォームが表示されると、計算された値が適切なフィールドに表示されます。

**関連項目**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[Java API を使用してフォームデータを計算する](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-java-api)
[Web サービス API を使用してフォームデータを計算する](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-web-service-api)
[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
[Forms サービス API クイックスタート](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)
[インタラクティブ PDF Forms のレンダリング](/help/forms/developing/rendering-interactive-pdf-forms.md)
[Forms をレンダリングする Web アプリケーションの作成](/help/forms/developing/creating-web-applications-renders-forms.md)

## Java API を使用してフォームデータを計算する {#calculate-form-data-using-the-java-api}

Forms API（Java）を使用してフォームデータを計算します。

1. プロジェクトファイルを含める

   クライアント JAR ファイル（adobe-forms-client.jar など）を Java プロジェクトのクラスパスに含めます。

1. Forms Client API オブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して `ServiceClientFactory` オブジェクトを渡すことにより、`FormsServiceClient` オブジェクトを作成します。

1. 計算スクリプトを含むフォームの取得

   * 計算スクリプトを含むフォームデータを取得するには、コンストラクターを使用して、コンストラクター内から `javax.servlet.http.HttpServletResponse` オブジェクトの `getInputStream` メソッドを呼び出すことによって、`com.adobe.idp.Document` オブジェクトを作成します。
   *  `FormsServiceClient` オブジェクトの `processFormSubmission` メソッドを呼び出して、次の値を渡します。

      * フォームデータを含む `com.adobe.idp.Document` オブジェクト。
      * 関連するすべての HTTP ヘッダーを含む環境変数を指定する文字列値。`CONTENT_TYPE` 環境変数に 1 つまたは複数の値を指定して、処理するコンテンツタイプを指定する必要があります。例えば、XML データと PDF データを処理するには、このパラメーターに文字列値「`CONTENT_TYPE=application/xml&CONTENT_TYPE=application/pdf`」を指定します。
      * `HTTP_USER_AGENT` ヘッダー値を指定する文字列値（例： `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`）。
      * 実行時オプションを格納する `RenderOptionsSpec` オブジェクト。

      `processFormSubmission` メソッドは、フォーム送信の結果を含む `FormsResult` オブジェクトを返します。

   * `FormsResult` オブジェクトの `getAction` メソッドを呼び出すことによって、送信されたフォームに関連付けられている処理状態が `1` であることを確認します。このメソッドが値 `1` を返した場合、計算は実行されており、データをクライアントの web ブラウザーに書き戻すことができます。


1. フォームデータストリームをクライアントの web ブラウザーに書き戻します。

   * フォームデータストリームをクライアント web ブラウザーに送信するために使用される `javax.servlet.ServletOutputStream` オブジェクトを作成します。
   * `FormsResult` オブジェクトの `getOutputContent` メソッドを呼び出すことによって、`com.adobe.idp.Document` オブジェクトを作成します。
   * `com.adobe.idp.Document` オブジェクトの `getInputStream` メソッドを呼び出すことによって `java.io.InputStream` オブジェクトを作成します。
   * `InputStream` オブジェクトの `read` メソッドを呼び出してバイト配列を引数として渡すことによって、バイト配列を作成してフォームデータストリームを入力します。
   * `javax.servlet.ServletOutputStream` オブジェクトの `write` メソッドを呼び出して、フォームデータストリームをクライアント web ブラウザーに送信します。バイト配列を `write` メソッドに渡します。

**関連項目**


[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Web サービス API を使用したフォームデータの計算 {#calculate-form-data-using-the-web-service-api}

Forms API（web サービス）を使用してフォームデータを計算します。

1. プロジェクトファイルを含める

   * Forms Service WSDL を使用する Java プロキシクラスを作成します。
   * Java プロキシクラスをクラスパスに含めます。

1. Forms Client API オブジェクトの作成

   `FormsService` オブジェクトを作成して、認証情報を設定します。

1. 計算スクリプトを含むフォームの取得

   * Java サーブレットにポストされたフォームデータを取得するには、コンストラクターを使用して `BLOB` オブジェクトを作成します。
   * `javax.servlet.http.HttpServletResponse` オブジェクトの `getInputStream` メソッドを使用して、`java.io.InputStream` オブジェクトを 作成します。
   * コンストラクターを使用して、`java.io.InputStream` オブジェクトの長さを渡すことにより、`java.io.ByteArrayOutputStream` オブジェクトを作成します。
   * `java.io.InputStream` オブジェクトの内容を `java.io.ByteArrayOutputStream` オブジェクトにコピーします。
   * `java.io.ByteArrayOutputStream` オブジェクトの `toByteArray` メソッドを呼び出してバイト配列を作成します。
   *  `setBinaryData` メソッドを呼び出してバイト配列を引数として渡すことによって、`BLOB` オブジェクトに入力します。
   * コンストラクターを使用して `RenderOptionsSpec` オブジェクトを作成します。`RenderOptionsSpec` オブジェクトの `setLocale` メソッドを呼び出してロケール値を指定する文字列値を渡すことによって、ロケール値を設定します。
   * `FormsServiceClient` オブジェクトの `processFormSubmission` メソッドを呼び出して、次の値を渡します。

      * フォームデータを格納する `BLOB` オブジェクト。
      * 関連するすべての HTTP ヘッダーが含まれる環境変数を指定する文字列の値。例えば、次の文字列の値を指定できます。`HTTP_REFERER=referrer&HTTP_CONNECTION=keep-alive&CONTENT_TYPE=application/xml`
      * `HTTP_USER_AGENT` ヘッダーの値を指定する文字列の値。例えば、`Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)` などです。
      * 実行時オプションを保存する `RenderOptionsSpec` オブジェクト。その他の情報。
      * このメソッドで入力される空の `BLOBHolder` オブジェクト。
      * メソッドによって設定される空の `javax.xml.rpc.holders.StringHolder` オブジェクト。
      * メソッドによって設定される空の `BLOBHolder` オブジェクト。
      * メソッドによって設定される空の `BLOBHolder` オブジェクト。
      * メソッドによって設定される空の `javax.xml.rpc.holders.ShortHolder` オブジェクト。
      * メソッドによって設定される空の `MyArrayOf_xsd_anyTypeHolder` オブジェクト。このパラメーターは、フォームと共に送信される添付ファイルを保存するために使用されます。
      * 送信したフォームを使用して、このメソッドで入力される空の `FormsResultHolder` オブジェクト。

      `processFormSubmission` メソッドで、フォーム送信の結果を `FormsResultHolder` パラメーターに入力します。`processFormSubmission` メソッドは、フォーム送信の結果を含む `FormsResult` オブジェクトを返します。

   * `FormsResult` オブジェクトの `getAction` メソッドを呼び出すことによって、送信されたフォームに関連付けられている処理状態が `1` であることを確認します。このメソッドが値 `1` を返した場合、計算は実行されており、データをクライアントの web ブラウザーに書き戻すことができます。


1. フォームデータストリームをクライアントの web ブラウザーに書き戻します。

   * フォームデータストリームをクライアントの web ブラウザーに送信するために使用する `javax.servlet.ServletOutputStream` オブジェクトを作成します。
   * `FormsResult` オブジェクトの `getOutputContent` メソッドを呼び出して、フォームデータを含む `BLOB` オブジェクトを作成します。
   * バイト配列を作成し、`BLOB` オブジェクトの `getBinaryData` メソッドを呼び出して、入力します。このタスクは、`FormsResult` オブジェクトのコンテンツをバイト配列に割り当てます。
   * `javax.servlet.http.HttpServletResponse` オブジェクトの `write` メソッドを呼び出して、フォームデータストリームをクライアント web ブラウザーに送信します。バイト配列を `write` メソッドに渡します。

**関連項目**
[Base64 エンコーディングを使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
