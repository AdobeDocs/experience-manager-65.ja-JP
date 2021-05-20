---
title: フォームデータの計算
seo-title: フォームデータの計算
description: Formsサービスを使用して、ユーザーがフォームに入力して結果を表示する値を計算します。 Formsサービスは、Java APIとWebサービスAPIを使用して値を計算します。
seo-description: Formsサービスを使用して、ユーザーがフォームに入力して結果を表示する値を計算します。 Formsサービスは、Java APIとWebサービスAPIを使用して値を計算します。
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
workflow-type: tm+mt
source-wordcount: '1916'
ht-degree: 2%

---

# フォームデータの計算{#calculating-form-data}

**このドキュメントのサンプルと例は、JEE上のAEM Forms環境に限られています。**

Formsサービスでは、ユーザーがフォームに入力した値を計算して結果を表示できます。 フォームデータを計算するには、2つのタスクを実行する必要があります。 まず、フォームデータを計算するフォームデザインスクリプトを作成します。 フォームデザインは、3種類のスクリプトをサポートします。 1つのスクリプトタイプはクライアントで実行され、もう1つはサーバーで実行され、3つ目はサーバーとクライアントの両方で実行されます。 このトピックで説明するスクリプトタイプは、サーバー上で実行されます。 HTML、PDF、フォームガイド（非推奨）の変換では、サーバー側の計算がサポートされています。

フォームデザインのプロセスの一環として、演算とスクリプトを使用し、より豊富なユーザーエクスペリエンスを提供できます。 演算とスクリプトは、ほとんどのフォームフィールドとオブジェクトに追加できます。 ユーザーがインタラクティブフォームに入力するデータに対して計算操作を実行するには、フォームデザインスクリプトを作成する必要があります。

ユーザーはフォームに値を入力し、「Calculate」ボタンをクリックして結果を表示します。 次のプロセスは、ユーザーがデータを計算できるサンプルアプリケーションを示しています。

* ユーザーは、Webアプリケーションの開始ページとして機能するStartLoan.htmlというHTMLページにアクセスします。 このページは、`GetLoanForm`という名前のJavaサーブレットを呼び出します。
* `GetLoanForm`サーブレットがローンフォームをレンダリングします。 このフォームには、スクリプト、インタラクティブフィールド、計算ボタンおよび送信ボタンが含まれています。
* ユーザーがフォームのフィールドに値を入力し、「計算」ボタンをクリックします。 フォームが`CalculateData` Javaサーブレットに送信され、スクリプトが実行されます。 計算結果がフォームに表示された状態で、フォームがユーザーに送り返されます。
* 満足のいく結果が表示されるまで、ユーザーは引き続き値の入力と計算を行います。 問題が解決されたら、ユーザーは「送信」ボタンをクリックしてフォームを処理します。 フォームは、送信されたデータを取得する`ProcessForm`という名前の別のJavaサーブレットに送信されます。 ([送信されたForms](/help/forms/developing/rendering-forms.md#handling-submitted-forms)の処理を参照)。


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
   <td><p><code>GetLoanForm</code> JavaサーブレットがHTML開始ページから呼び出されます。 </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p><code>GetLoanForm</code> Javaサーブレットは、FormsサービスクライアントAPIを使用して、ローンフォームをクライアントWebブラウザーにレンダリングします。 サーバー上で実行するように設定されたスクリプトを含むフォームをレンダリングする場合と、スクリプトを含まないフォームをレンダリングする場合の違いは、スクリプトの実行に使用するターゲットの場所を指定する必要がある点です。 ターゲットの場所を指定しない場合、サーバー上で実行するように設定されたスクリプトは実行されません。 例えば、この節で紹介するアプリケーションについて考えてみましょう。 <code>CalculateData</code> Javaサーブレットは、スクリプトが実行されるターゲットの場所です。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>ユーザーがインタラクティブフィールドにデータを入力し、「計算」ボタンをクリックします。 フォームが<code>CalculateData</code> Javaサーブレットに送信され、スクリプトが実行されます。 </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>計算結果がフォームに表示された状態で、フォームがWebブラウザーにレンダリングされます。 </p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>値が十分な場合は、ユーザーが「送信」ボタンをクリックします。 フォームは、<code>ProcessForm</code>という名前の別のJavaサーブレットに送信されます。</p></td>
  </tr>
 </tbody>
</table>

通常、PDFコンテンツとして送信されるフォームには、クライアントで実行されるスクリプトが含まれます。 ただし、サーバー側の計算を実行することもできます。 「送信」ボタンを使用してスクリプトを計算することはできません。 この場合、Formsサービスでインタラクションが完了すると見なされるので、計算は実行されません。

フォームデザインスクリプトの使用方法を説明するために、この節では、サーバー上で実行するように設定されたスクリプトを含むシンプルなインタラクティブフォームを調べます。 次の図は、スクリプトを含むフォームデザインを示しています。このスクリプトを使用して、ユーザーが最初の2つのフィールドに入力し、その結果を3番目のフィールドに表示します。

![cf_cf_caldata](assets/cf_cf_caldata.png)

**A.** NumericField1 B. **NumericField2 Cという名前のフィール** ド **** NumericField3という名前のフィールド

このフォームデザインに含まれるスクリプトの構文は次のとおりです。

```javascript
     NumericField3 = NumericField2 + NumericField1
```

このフォームデザインでは、「計算」ボタンはコマンドボタンで、スクリプトはこのボタンの`Click`イベントに配置されます。 ユーザーが最初の2つのフィールド（NumericField1およびNumericField2）に値を入力し、「Calculate」ボタンをクリックすると、フォームがFormsサービスに送信され、スクリプトが実行されます。 Formsサービスは、計算の結果をNumericField3フィールドに表示して、フォームをクライアントデバイスにレンダリングし直します。

>[!NOTE]
>
>フォームデザインスクリプトの作成について詳しくは、「[Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)」を参照してください。

>[!NOTE]
>
>Formsサービスについて詳しくは、『 AEM Formsのサービスリファレンス[ 』を参照してください。](https://www.adobe.com/go/learn_aemforms_services_63)

## 手順の概要{#summary-of-steps}

フォームデータを計算するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Forms Client APIオブジェクトを作成します。
1. 計算スクリプトを含むフォームを取得します。
1. フォームデータストリームをクライアントWebブラウザーに書き戻す

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用する場合は、プロキシファイルを必ず含めてください。

**Forms Client APIオブジェクトの作成**

FormsサービスクライアントAPI操作をプログラムで実行する前に、Formsサービスクライアントを作成する必要があります。 Java APIを使用している場合は、`FormsServiceClient`オブジェクトを作成します。 Forms WebサービスAPIを使用している場合は、`FormsServiceService`オブジェクトを作成します。

**計算スクリプトを含むフォームの取得**

FormsサービスクライアントAPIを使用して、サーバー上で実行するように設定されたスクリプトを含むフォームを処理するアプリケーションロジックを作成します。 このプロセスは、送信されたフォームの処理に似ています。 ([送信されたForms](/help/forms/developing/handling-submitted-forms.md)の処理を参照)。

送信されたフォームに関連付けられている処理状態が`1` `(Calculate)`であることを確認します。つまり、Formsサービスがフォームデータに対して計算操作を実行し、結果をユーザーに書き戻す必要があります。 この場合、サーバー上で実行するように設定されたスクリプトが自動的に実行されます。

**フォームデータストリームをクライアントWebブラウザーに書き戻す**

送信されたフォームに関連付けられている処理状態が`1`であることを確認したら、結果をクライアントのWebブラウザーに書き戻す必要があります。 フォームが表示されると、計算された値が該当するフィールドに表示されます。

**関連項目**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files) 
[Java APICalculate form data using the Web service API ](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-java-api)
[APISetting connection ](/help/forms/developing/calculating-form-data.md#calculate-form-data-using-the-web-service-api)
[propertiesForms Service API Quick StartsRendering Interactive PDF ](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
[](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)
[](/help/forms/developing/rendering-interactive-pdf-forms.md)
[FormsForms Renders Webアプリケーションの作成](/help/forms/developing/creating-web-applications-renders-forms.md)

## Java APIを使用してフォームデータを計算する{#calculate-form-data-using-the-java-api}

Forms API(Java)を使用してフォームデータを計算します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-forms-client.jarなどのクライアントJARファイルを含めます。

1. Forms Client APIオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して`FormsServiceClient`オブジェクトを渡し、`ServiceClientFactory`オブジェクトを作成します。

1. 計算スクリプトを含むフォームの取得

   * 計算スクリプトを含むフォームデータを取得するには、コンストラクタを使用して`com.adobe.idp.Document`オブジェクトを作成し、コンストラクタ内から`javax.servlet.http.HttpServletResponse`オブジェクトの`getInputStream`メソッドを呼び出します。
   * `FormsServiceClient`オブジェクトの`processFormSubmission`メソッドを呼び出し、次の値を渡します。

      * フォームデータを格納する`com.adobe.idp.Document`オブジェクト。
      * 関連するすべてのHTTPヘッダーを含む環境変数を指定するstring値。 `CONTENT_TYPE`環境変数に1つ以上の値を指定して、処理するコンテンツタイプを指定する必要があります。 例えば、XMLデータとPDFデータを処理するには、このパラメーターに次の文字列値を指定します。`CONTENT_TYPE=application/xml&CONTENT_TYPE=application/pdf`
      * `HTTP_USER_AGENT`ヘッダー値を指定するstring値。例： `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`
      * 実行時オプションを格納する`RenderOptionsSpec`オブジェクト。

      `processFormSubmission`メソッドは、フォーム送信の結果を含む`FormsResult`オブジェクトを返します。

   * `FormsResult`オブジェクトの`getAction`メソッドを呼び出して、送信されたフォームに関連付けられている処理状態が`1`であることを確認します。 このメソッドが値`1`を返す場合、計算が実行され、データをクライアントWebブラウザーに書き戻すことができます。


1. フォームデータストリームをクライアントWebブラウザーに書き戻す

   * フォームデータストリームをクライアントのWebブラウザーに送信するために使用する`javax.servlet.ServletOutputStream`オブジェクトを作成します。
   * `FormsResult`オブジェクトの`getOutputContent`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトを作成します。
   * `com.adobe.idp.Document`オブジェクトの`getInputStream`メソッドを呼び出して、`java.io.InputStream`オブジェクトを作成します。
   * `InputStream`オブジェクトの`read`メソッドを呼び出し、バイト配列を引数として渡すことで、バイト配列を作成し、フォームデータストリームに入力します。
   * `javax.servlet.ServletOutputStream`オブジェクトの`write`メソッドを呼び出して、フォームデータストリームをクライアントWebブラウザーに送信します。 `write`メソッドにバイト配列を渡します。

**関連項目**


[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)
[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## WebサービスAPI {#calculate-form-data-using-the-web-service-api}を使用してフォームデータを計算する

Forms API（Webサービス）を使用してフォームデータを計算します。

1. プロジェクトファイルを含める

   * FormsサービスのWSDLを使用するJavaプロキシクラスを作成します。
   * Javaプロキシクラスをクラスパスに含めます。

1. Forms Client APIオブジェクトの作成

   `FormsService`オブジェクトを作成し、認証値を設定します。

1. 計算スクリプトを含むフォームの取得

   * Javaサーブレットに投稿されたフォームデータを取得するには、コンストラクタを使用して`BLOB`オブジェクトを作成します。
   * `javax.servlet.http.HttpServletResponse`オブジェクトの`getInputStream`メソッドを使用して、`java.io.InputStream`オブジェクトを作成します。
   * コンストラクターを使用して`java.io.ByteArrayOutputStream`オブジェクトの長さを渡し、`java.io.InputStream`オブジェクトを作成します。
   * `java.io.InputStream`オブジェクトの内容を`java.io.ByteArrayOutputStream`オブジェクトにコピーします。
   * `java.io.ByteArrayOutputStream`オブジェクトの`toByteArray`メソッドを呼び出して、バイト配列を作成します。
   * `setBinaryData`メソッドを呼び出し、バイト配列を引数として渡すことで、`BLOB`オブジェクトを設定します。
   * コンストラクタを使用して `RenderOptionsSpec` オブジェクトを作成します。`RenderOptionsSpec`オブジェクトの`setLocale`メソッドを呼び出し、ロケール値を指定する文字列値を渡すことによって、ロケール値を設定します。
   * `FormsServiceClient`オブジェクトの`processFormSubmission`メソッドを呼び出し、次の値を渡します。

      * フォームデータを格納する`BLOB`オブジェクト。
      * 環境変数を指定するstring値に、関連するすべてのHTTPヘッダーが含まれていました。 例えば、次の文字列値を指定できます。`HTTP_REFERER=referrer&HTTP_CONNECTION=keep-alive&CONTENT_TYPE=application/xml`
      * `HTTP_USER_AGENT`ヘッダー値を指定するstring値。例： `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`
      * 実行時オプションを格納する`RenderOptionsSpec`オブジェクト。 その他の情報, .
      * メソッドで設定される空の`BLOBHolder`オブジェクト。
      * メソッドで設定される空の`javax.xml.rpc.holders.StringHolder`オブジェクト。
      * メソッドで設定される空の`BLOBHolder`オブジェクト。
      * メソッドで設定される空の`BLOBHolder`オブジェクト。
      * メソッドで設定される空の`javax.xml.rpc.holders.ShortHolder`オブジェクト。
      * メソッドで設定される空の`MyArrayOf_xsd_anyTypeHolder`オブジェクト。 このパラメーターは、フォームと共に送信される添付ファイルを保存するために使用されます。
      * 送信されるフォームを使用してメソッドによって入力される、空の`FormsResultHolder`オブジェクト。

      `processFormSubmission`メソッドは、`FormsResultHolder`パラメーターにフォーム送信の結果を入力します。 `processFormSubmission`メソッドは、フォーム送信の結果を含む`FormsResult`オブジェクトを返します。

   * `FormsResult`オブジェクトの`getAction`メソッドを呼び出して、送信されたフォームに関連付けられている処理状態が`1`であることを確認します。 このメソッドが値`1`を返す場合、計算が実行され、データをクライアントWebブラウザーに書き戻すことができます。


1. フォームデータストリームをクライアントWebブラウザーに書き戻す

   * フォームデータストリームをクライアントのWebブラウザーに送信するために使用する`javax.servlet.ServletOutputStream`オブジェクトを作成します。
   * `FormsResult`オブジェクトの`getOutputContent`メソッドを呼び出して、フォームデータを含む`BLOB`オブジェクトを作成します。
   * バイト配列を作成し、`BLOB`オブジェクトの`getBinaryData`メソッドを呼び出してそれを設定します。 このタスクは、`FormsResult`オブジェクトの内容をバイト配列に割り当てます。
   * `javax.servlet.http.HttpServletResponse`オブジェクトの`write`メソッドを呼び出して、フォームデータストリームをクライアントWebブラウザーに送信します。 `write`メソッドにバイト配列を渡します。

**Base64エン**
[コーディングを使用したAEM Formsの呼び出しも参照してください。](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
