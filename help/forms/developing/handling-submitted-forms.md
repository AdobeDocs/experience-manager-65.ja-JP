---
title: 送信済みFormsの処理
seo-title: 送信済みFormsの処理
description: Formsサービスを使用して、インタラクティブフォームに入力された送信済みデータを取得します。 ユーザーは、XML、PDF、URL UTF-16形式でフォームデータを送信できます。
seo-description: Formsサービスを使用して、インタラクティブフォームに入力された送信済みデータを取得します。 ユーザーは、XML、PDF、URL UTF-16形式でフォームデータを送信できます。
uuid: 673b28f1-f023-4da8-a6a0-c5ff921c5f5d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 3d838027-6bde-4a71-a428-4d5102f7d799
role: Developer
exl-id: 419335b2-2aae-4e83-98ff-18e61b7efa9c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2935'
ht-degree: 2%

---

# 送信されたForms {#handling-submitted-forms}の処理

**このドキュメントのサンプルと例は、JEE上のAEM Forms環境に限られています。**

ユーザーがインタラクティブフォームに入力できるWebベースのアプリケーションでは、データをサーバーに送り返す必要があります。 Formsサービスを使用すると、ユーザーがインタラクティブフォームに入力したデータを取得できます。 データを取得したら、ビジネス要件に合わせてデータを処理できます。 例えば、データをデータベースに格納し、データを別のアプリケーションに送信し、データを別のサービスに送信し、データをフォームデザインに結合して、Webブラウザーに表示するなどの操作を実行できます。

フォームデータは、XMLまたはPDFデータとしてFormsサービスに送信されます。これは、Designerで設定されるオプションです。 XMLとして送信されるフォームを使用して、個々のフィールドデータ値を抽出できます。 つまり、ユーザーがフォームに入力した各フォームフィールドの値を抽出できます。 PDFデータとして送信されるフォームは、XMLデータではなくバイナリデータです。 フォームをPDFファイルとして保存するか、別のサービスにフォームを送信することができます。 XMLとして送信されたフォームからデータを抽出し、そのフォームデータを使用してPDFドキュメントを作成する場合は、別のAEM Forms操作を呼び出します。 （[送信済みXMLデータを使用したPDFドキュメントの作成](/help/forms/developing/creating-pdf-documents-submitted-xml.md)を参照）。

次の図は、Webブラウザーに表示されるインタラクティブフォームから`HandleData`という名前のJavaサーブレットに送信されるデータを示しています。

![hs_hs_handlesubmit](assets/hs_hs_handlesubmit.png)

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
   <td><p>ユーザーがインタラクティブフォームに入力し、フォームの「送信」ボタンをクリックします。</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>データはXMLデータとして<code>HandleData</code> Javaサーブレットに送信されます。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p><code>HandleData</code> Javaサーブレットには、データを取得するアプリケーションロジックが含まれています。</p></td>
  </tr>
 </tbody>
</table>

## 送信されたXMLデータ{#handling-submitted-xml-data}の処理

フォームデータがXMLとして送信されると、送信されたデータを表すXMLデータを取得できます。 すべてのフォームフィールドは、XMLスキーマ内のノードとして表示されます。 ノード値は、ユーザーが入力した値に対応します。 ローンフォームでは、フォームの各フィールドがXMLデータ内のノードとして表示されます。 各ノードの値は、ユーザーが入力する値に対応します。 ユーザーが次のフォームに示すデータを使用してローンフォームに記入するとします。

![hs_hs_loanformdata](assets/hs_hs_loanformdata.png)

次の図に、FormsサービスクライアントAPIを使用して取得される、対応するXMLデータを示します。

![hs_hs_loandata](assets/hs_hs_loandata.png)

ローンフォームのフィールド。 これらの値は、
Java XMLクラスを使用する。

>[!NOTE]
>
>データをXMLデータとして送信するには、Designerでフォームデザインを正しく設定する必要があります。 XMLデータを送信するようにフォームデザインを適切に設定するには、フォームデザイン上にある「送信」ボタンがXMLデータを送信するように設定されていることを確認します。 XMLデータを送信するための「送信」ボタンの設定について詳しくは、[AEM Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)を参照してください。

## 送信されたPDFデータの処理{#handling-submitted-pdf-data}

Formsサービスを呼び出すWebアプリケーションを検討します。 FormsサービスがインタラクティブPDFフォームをクライアントWebブラウザーにレンダリングした後、ユーザーはフォームに入力し、PDFデータとして送り返します。 Formsサービスは、PDFデータを受け取ると、そのPDFデータを別のサービスに送信したり、PDFファイルとして保存したりできます。 次の図に、アプリケーションのロジック・フローを示します。

![hs_hs_savingforms](assets/hs_hs_savingforms.png)

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
   <td><p>Webページには、Formsサービスを呼び出すJavaサーブレットにアクセスするリンクが含まれています。</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Formsサービスは、インタラクティブPDFフォームをクライアントのWebブラウザーにレンダリングします。</p></td>
  </tr>
  <tr>
   <td><p>1</p></td>
   <td><p>ユーザーはインタラクティブフォームに入力し、送信ボタンをクリックします。 フォームがPDFデータとしてFormsサービスに送信されます。 このオプションはDesignerで設定されます。</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Formsサービスは、PDFデータをPDFファイルとして保存します。 </p></td>
  </tr>
 </tbody>
</table>

## 送信されたURL UTF-16データの処理{#handling-submitted-url-utf-16-data}

フォームデータがURL UTF-16データとして送信される場合、クライアントコンピューターにはAdobe ReaderまたはAcrobat 8.1以降が必要です。 また、フォームデザインにURLエンコードデータ(HTTP Post)を含む送信ボタンが含まれ、データエンコードオプションがUTF-16の場合は、フォームデザインをメモ帳などのテキストエディターで変更する必要があります。 送信ボタンのエンコーディングオプションを`UTF-16LE`または`UTF-16BE`に設定できます。 Designerはこの機能を提供しません。

>[!NOTE]
>
>Formsサービスについて詳しくは、『 AEM Formsのサービスリファレンス[ 』を参照してください。](https://www.adobe.com/go/learn_aemforms_services_63)

## 手順の概要{#summary-of-steps}

送信済みのフォームを処理するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Forms Client APIオブジェクトを作成します。
1. フォームデータを取得します。
1. フォーム送信に添付ファイルが含まれているかどうかを確認します。
1. 送信されたデータを処理します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用する場合は、プロキシファイルを必ず含めてください。

**Forms Client APIオブジェクトの作成**

FormsサービスクライアントAPI操作をプログラムで実行する前に、Formsサービスクライアントを作成する必要があります。 Java APIを使用している場合は、`FormsServiceClient`オブジェクトを作成します。 Forms WebサービスAPIを使用している場合は、`FormsService`オブジェクトを作成します。

**フォームデータの取得**

送信されたフォームデータを取得するには、`FormsServiceClient`オブジェクトの`processFormSubmission`メソッドを呼び出します。 このメソッドを呼び出す場合は、送信済みフォームのコンテンツタイプを指定する必要があります。 クライアントのWebブラウザーからFormsサービスにデータを送信する場合、XMLまたはPDFデータとして送信できます。 フォームフィールドに入力されたデータを取得するには、データをXMLデータとして送信します。

また、次の実行時オプションを設定して、PDFデータとして送信されたフォームからフォームフィールドを取得することもできます。

* 次の値を`processFormSubmission`メソッドにコンテンツタイプパラメーターとして渡します。`CONTENT_TYPE=application/pdf`.
* `RenderOptionsSpec`オブジェクトの`PDFToXDP`値を`true`に設定します。
* `RenderOptionsSpec`オブジェクトの`ExportDataFormat`値を`XMLData`に設定します。

`processFormSubmission`メソッドを呼び出すときに、送信されたフォームのコンテンツタイプを指定します。 次のリストで、適用可能なコンテンツタイプ値を指定します。

* **text/xml**:PDFフォームでフォームデータをXMLとして送信する際に使用するコンテンツタイプを表します。
* **application/x-www-form-urlencoded**:HTMLフォームでデータをXMLとして送信する際に使用するコンテンツタイプを表します。
* **application/pdf**:PDFフォームでデータをPDFとして送信する際に使用するコンテンツタイプを表します。

>[!NOTE]
>
>「送信済みFormsの処理」セクションには、対応する3つのクイックスタートが関連付けられています。 Java APIクイックスタートを使用したPDFとして送信されたPDF formsの処理では、送信されたPDFデータの処理方法を示します。 このクイックスタートで指定されているコンテンツタイプは`application/pdf`です。 Java APIクイックスタートを使用したXMLとして送信されたPDF formsの処理では、PDFフォームから送信された送信済みXMLデータを処理する方法を示します。 このクイックスタートで指定されているコンテンツタイプは`text/xml`です。 同様に、Java APIクイックスタートを使用したXML形式でのHTMLフォームの処理で、HTMLフォームから送信された送信済みXMLデータの処理方法を示します。 このクイックスタートで指定するコンテンツタイプは、application/x-www-form-urlencodedです。

Formsサービスに投稿されたフォームデータを取得し、その処理状態を判断します。 つまり、データがFormsサービスに送信される場合、必ずしもFormsサービスによるデータの処理が完了し、データの処理準備ができたとは限りません。 例えば、計算を実行するためにFormsサービスにデータを送信できます。 計算が完了すると、フォームはユーザーにレンダリングされ、計算結果が表示されます。 送信されたデータを処理する前に、Formsサービスがデータの処理を完了したかどうかを確認することをお勧めします。

Formsサービスは、データの処理が完了したかどうかを示す次の値を返します。

* **0（送信）:** 送信されたデータは処理の準備ができました。
* **1（計算）:** Formsサービスがデータに対して計算操作を実行したので、結果をユーザーにレンダリングする必要があります。
* **2（検証）:** Formsサービスが検証したフォームデータと、その結果をユーザーに返す必要があります。
* **3（次へ）:** 現在のページが変更され、クライアントアプリケーションに書き込む必要がある結果が反映されました。
* **4(前**):現在のページは、クライアントアプリケーションに書き込む必要がある結果と共に変更されます。

>[!NOTE]
>
>計算と検証は、ユーザーにレンダリングし直す必要があります。 （[フォームデータ](/help/forms/developing/calculating-form-data.md#calculating-form-data)の計算を参照）。

**フォーム送信に添付ファイルが含まれているかどうかを確認します**

Formsサービスに送信されるFormsには、添付ファイルを含めることができます。 例えば、Acrobatに組み込まれている添付ファイルウィンドウを使用すると、ユーザーは添付ファイルを選択してフォームと共に送信できます。 また、HTMLファイルと共にレンダリングされるHTMLツールバーを使用して、添付ファイルを選択することもできます。

フォームに添付ファイルが含まれているかどうかを確認したら、データを処理できます。 例えば、添付ファイルをローカルファイルシステムに保存できます。

>[!NOTE]
>
>添付ファイルを取得するには、フォームをPDFデータとして送信する必要があります。 フォームがXMLデータとして送信された場合、添付ファイルは送信されません。

**送信されたデータの処理**

送信データのコンテンツタイプに応じて、個々のフォームフィールドの値を送信済みXMLデータから抽出するか、送信済みPDFデータをPDFファイルとして保存する（または別のサービスに送信する）ことができます。 個々のフォームフィールドを抽出するには、送信されたXMLデータをXMLデータソースに変換し、`org.w3c.dom`クラスを使用してXMLデータソースの値を取得します。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[FormsサービスAPIのクイックスタート](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Formsサービスにドキュメントを渡す](/help/forms/developing/passing-documents-forms-service.md)

[Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

## Java APIを使用して送信されたフォームを処理する{#handle-submitted-forms-using-the-java-api}

Forms API(Java)を使用して、送信されたフォームを処理します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-forms-client.jarなどのクライアントJARファイルを含めます。

1. Forms Client APIオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して`FormsServiceClient`オブジェクトを渡し、`ServiceClientFactory`オブジェクトを作成します。

1. フォームデータの取得

   * Javaサーブレットに投稿されたフォームデータを取得するには、コンストラクターを使用して`com.adobe.idp.Document`オブジェクトを作成し、コンストラクター内から`javax.servlet.http.HttpServletResponse`オブジェクトの`getInputStream`メソッドを呼び出します。
   * コンストラクタを使用して `RenderOptionsSpec` オブジェクトを作成します。`RenderOptionsSpec`オブジェクトの`setLocale`メソッドを呼び出し、ロケール値を指定する文字列値を渡すことによって、ロケール値を設定します。

   >[!NOTE]
   >
   >`RenderOptionsSpec`オブジェクトの`setPDF2XDP`メソッドを呼び出して`true`を渡し、`setXMLData`を呼び出して`true`を渡すことで、送信されたPDFコンテンツからXDPまたはXMLデータを作成するようFormsサービスに指示できます。 その後、`FormsResult`オブジェクトの`getOutputXML`メソッドを呼び出して、XDP/XMLデータに対応するXMLデータを取得できます。 （`FormsResult`オブジェクトは、次のサブステップで説明する`processFormSubmission`メソッドで返されます）。

   * `FormsServiceClient`オブジェクトの`processFormSubmission`メソッドを呼び出し、次の値を渡します。

      * フォームデータを格納する`com.adobe.idp.Document`オブジェクト。
      * 関連するすべてのHTTPヘッダーを含む環境変数を指定するstring値。 処理するコンテンツタイプを指定します。 XMLデータを処理するには、このパラメーターに次の文字列値を指定します。`CONTENT_TYPE=text/xml`. PDFデータを処理するには、このパラメーターに次の文字列値を指定します。`CONTENT_TYPE=application/pdf`.
      * `HTTP_USER_AGENT`ヘッダー値を指定するstring値（例： ）。 `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`」を選択します。このパラメーター値はオプションです。
      * 実行時オプションを格納する`RenderOptionsSpec`オブジェクト。

      `processFormSubmission`メソッドは、フォーム送信の結果を含む`FormsResult`オブジェクトを返します。

   * `FormsResult`オブジェクトの`getAction`メソッドを呼び出して、Formsサービスがフォームデータの処理を完了したかどうかを判断します。 このメソッドが値`0`を返す場合、データは処理できる状態になります。



1. フォーム送信に添付ファイルが含まれているかどうかを確認します

   * `FormsResult`オブジェクトの`getAttachments`メソッドを呼び出します。 このメソッドは、フォームと共に送信されたファイルを含む`java.util.List`オブジェクトを返します。
   * `java.util.List`オブジェクトを繰り返し処理して、添付ファイルが存在するかどうかを判断します。 添付ファイルがある場合、各要素は`com.adobe.idp.Document`インスタンスになります。 `com.adobe.idp.Document`オブジェクトの`copyToFile`メソッドを呼び出し、`java.io.File`オブジェクトを渡すことで、添付ファイルを保存できます。

   >[!NOTE]
   >
   >この手順は、フォームがPDFとして送信された場合にのみ適用されます。

1. 送信されたデータの処理

   * データコンテンツタイプが`application/vnd.adobe.xdp+xml`または`text/xml`の場合、XMLデータ値を取得するアプリケーションロジックを作成します。

      * `FormsResult`オブジェクトの`getOutputContent`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトを作成します。
      * `java.io.DataInputStream`コンストラクターを呼び出し、`com.adobe.idp.Document`オブジェクトを渡して、`java.io.InputStream`オブジェクトを作成します。
      * 静的な`org.w3c.dom.DocumentBuilderFactory`オブジェクトの`newInstance`メソッドを呼び出して、`org.w3c.dom.DocumentBuilderFactory`オブジェクトを作成します。
      * `org.w3c.dom.DocumentBuilderFactory`オブジェクトの`newDocumentBuilder`メソッドを呼び出して、`org.w3c.dom.DocumentBuilder`オブジェクトを作成します。
      * `org.w3c.dom.DocumentBuilder`オブジェクトの`parse`メソッドを呼び出し、`java.io.InputStream`オブジェクトを渡して、`org.w3c.dom.Document`オブジェクトを作成します。
      * XMLドキュメント内の各ノードの値を取得します。 このタスクを実行する1つの方法は、次の2つのパラメーターを受け入れるカスタムメソッドを作成することです。`org.w3c.dom.Document`オブジェクトと、値を取得するノードの名前。 このメソッドは、ノードの値を表す文字列値を返します。 このプロセスに続くコード例では、このカスタムメソッドを`getNodeText`と呼びます。 このメソッドの本文が表示されます。
   * データコンテンツタイプが`application/pdf`の場合は、送信されたPDFデータをPDFファイルとして保存するアプリケーションロジックを作成します。

      * `FormsResult`オブジェクトの`getOutputContent`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトを作成します。
      * `java.io.File`オブジェクトを作成するには、そのパブリックコンストラクターを使用します。 ファイル名の拡張子としてPDFを必ず指定してください。
      * `com.adobe.idp.Document`オブジェクトの`copyToFile`メソッドを呼び出して`java.io.File`オブジェクトを渡すことによって、PDFファイルを生成します。


**関連トピック**

[クイックスタート（SOAPモード）:Java APIを使用してXMLとして送信されたPDF formsの処理](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-xml-using-the-java-api)

[クイックスタート（SOAPモード）:Java APIを使用して、XMLとして送信されたHTMLフォームの処理](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-html-forms-submitted-as-xml-using-the-java-api)

[クイックスタート（SOAPモード）:Java APIを使用してPDFとして送信されたPDF formsの処理](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-pdf-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## WebサービスAPI {#handle-submitted-pdf-data-using-the-web-service-api}を使用して送信されたPDFデータを処理します

Forms API（Webサービス）を使用して、送信されたフォームを処理します。

1. プロジェクトファイルを含める

   * FormsサービスのWSDLを使用するJavaプロキシクラスを作成します。
   * Javaプロキシクラスをクラスパスに含めます。

1. Forms Client APIオブジェクトの作成

   `FormsService`オブジェクトを作成し、認証値を設定します。

1. フォームデータの取得

   * Javaサーブレットに投稿されたフォームデータを取得するには、コンストラクタを使用して`BLOB`オブジェクトを作成します。
   * `javax.servlet.http.HttpServletResponse`オブジェクトの`getInputStream`メソッドを呼び出して、`java.io.InputStream`オブジェクトを作成します。
   * コンストラクターを使用して`java.io.ByteArrayOutputStream`オブジェクトの長さを渡し、`java.io.InputStream`オブジェクトを作成します。
   * `java.io.InputStream`オブジェクトの内容を`java.io.ByteArrayOutputStream`オブジェクトにコピーします。
   * `java.io.ByteArrayOutputStream`オブジェクトの`toByteArray`メソッドを呼び出して、バイト配列を作成します。
   * `setBinaryData`メソッドを呼び出し、バイト配列を引数として渡すことで、`BLOB`オブジェクトを設定します。
   * コンストラクタを使用して `RenderOptionsSpec` オブジェクトを作成します。`RenderOptionsSpec`オブジェクトの`setLocale`メソッドを呼び出し、ロケール値を指定する文字列値を渡すことによって、ロケール値を設定します。
   * `FormsService`オブジェクトの`processFormSubmission`メソッドを呼び出し、次の値を渡します。

      * フォームデータを格納する`BLOB`オブジェクト。
      * 関連するすべてのHTTPヘッダーを含む環境変数を指定するstring値。 処理するコンテンツタイプを指定します。 XMLデータを処理するには、このパラメーターに次の文字列値を指定します。`CONTENT_TYPE=text/xml`. PDFデータを処理するには、このパラメーターに次の文字列値を指定します。`CONTENT_TYPE=application/pdf`.
      * `HTTP_USER_AGENT`ヘッダー値を指定するstring値。例： `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`
      * 実行時オプションを格納する`RenderOptionsSpec`オブジェクト。
      * メソッドで設定される空の`BLOBHolder`オブジェクト。
      * メソッドで設定される空の`javax.xml.rpc.holders.StringHolder`オブジェクト。
      * メソッドで設定される空の`BLOBHolder`オブジェクト。
      * メソッドで設定される空の`BLOBHolder`オブジェクト。
      * メソッドで設定される空の`javax.xml.rpc.holders.ShortHolder`オブジェクト。
      * メソッドで設定される空の`MyArrayOf_xsd_anyTypeHolder`オブジェクト。 このパラメーターは、フォームと共に送信される添付ファイルを保存するために使用されます。
      * 送信されるフォームを使用してメソッドによって入力される、空の`FormsResultHolder`オブジェクト。

      `processFormSubmission`メソッドは、`FormsResultHolder`パラメーターにフォーム送信の結果を入力します。

   * `FormsResult`オブジェクトの`getAction`メソッドを呼び出して、Formsサービスがフォームデータの処理を完了したかどうかを判断します。 このメソッドが値`0`を返す場合、フォームデータは処理できる状態になります。 `FormsResult`オブジェクトは、`FormsResultHolder`オブジェクトの`value`データメンバーの値を取得することで取得できます。


1. フォーム送信に添付ファイルが含まれているかどうかを確認します

   `MyArrayOf_xsd_anyTypeHolder`オブジェクトの`value`データメンバーの値を取得します（`MyArrayOf_xsd_anyTypeHolder`オブジェクトが`processFormSubmission`メソッドに渡されました）。 このデータメンバは`Objects`の配列を返します。 `Object`配列内の各要素は、フォームと共に送信されたファイルに対応する`Object`です。 配列内の各要素を取得し、`BLOB`オブジェクトにキャストできます。

1. 送信されたデータの処理

   * データコンテンツタイプが`application/vnd.adobe.xdp+xml`または`text/xml`の場合、XMLデータ値を取得するアプリケーションロジックを作成します。

      * `FormsResult`オブジェクトの`getOutputContent`メソッドを呼び出して、`BLOB`オブジェクトを作成します。
      * `BLOB`オブジェクトの`getBinaryData`メソッドを呼び出して、バイト配列を作成します。
      * `java.io.ByteArrayInputStream`コンストラクターを呼び出してバイト配列を渡すことで、`java.io.InputStream`オブジェクトを作成します。
      * 静的な`org.w3c.dom.DocumentBuilderFactory`オブジェクトの`newInstance`メソッドを呼び出して、`org.w3c.dom.DocumentBuilderFactory`オブジェクトを作成します。
      * `org.w3c.dom.DocumentBuilderFactory`オブジェクトの`newDocumentBuilder`メソッドを呼び出して、`org.w3c.dom.DocumentBuilder`オブジェクトを作成します。
      * `org.w3c.dom.DocumentBuilder`オブジェクトの`parse`メソッドを呼び出し、`java.io.InputStream`オブジェクトを渡して、`org.w3c.dom.Document`オブジェクトを作成します。
      * XMLドキュメント内の各ノードの値を取得します。 このタスクを実行する1つの方法は、次の2つのパラメーターを受け入れるカスタムメソッドを作成することです。`org.w3c.dom.Document`オブジェクトと、値を取得するノードの名前。 このメソッドは、ノードの値を表す文字列値を返します。 このプロセスに続くコード例では、このカスタムメソッドを`getNodeText`と呼びます。 このメソッドの本文が表示されます。
   * データコンテンツタイプが`application/pdf`の場合は、送信されたPDFデータをPDFファイルとして保存するアプリケーションロジックを作成します。

      * `FormsResult`オブジェクトの`getOutputContent`メソッドを呼び出して、`BLOB`オブジェクトを作成します。
      * `BLOB`オブジェクトの`getBinaryData`メソッドを呼び出して、バイト配列を作成します。
      * `java.io.File`オブジェクトを作成するには、そのパブリックコンストラクターを使用します。 ファイル名の拡張子としてPDFを必ず指定してください。
      * コンストラクタを使用して `java.io.FileOutputStream` オブジェクトを渡すことによって、`java.io.File` オブジェクトを作成します。
      * `java.io.FileOutputStream`オブジェクトの`write`メソッドを呼び出し、バイト配列を渡すことによって、PDFファイルを生成します。


**関連トピック**

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
