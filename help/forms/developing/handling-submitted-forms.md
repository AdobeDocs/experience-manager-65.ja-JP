---
title: 提出されたFormsの処理
seo-title: 提出されたFormsの処理
description: インタラクティブフォームに入力された送信済みデータを取得するには、Formsサービスを使用します。 フォームデータは、XML、PDFおよびURL UTF-16形式で送信できます。
seo-description: インタラクティブフォームに入力された送信済みデータを取得するには、Formsサービスを使用します。 フォームデータは、XML、PDFおよびURL UTF-16形式で送信できます。
uuid: 673b28f1-f023-4da8-a6a0-c5ff921c5f5d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 3d838027-6bde-4a71-a428-4d5102f7d799
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '2921'
ht-degree: 2%

---


# 送信されたFormsの処理{#handling-submitted-forms}

ユーザーがインタラクティブフォームに入力できるWebベースのアプリケーションでは、データをサーバーに送信し直す必要があります。 Formsサービスを使用すると、ユーザーがインタラクティブフォームに入力したデータを取得できます。 データを取得したら、ビジネス要件に合わせてデータを処理できます。 例えば、データをデータベースに格納し、データを別のアプリケーションに送信し、データを別のサービスに送信し、データをフォームデザインに結合し、Webブラウザーにデータを表示するなどの操作を実行できます。

フォームデータは、XMLまたはPDFデータとしてFormsサービスに送信されます。これは、Designerで設定されるオプションです。 XML形式で送信されるフォームを使用すると、個々のフィールドデータ値を抽出できます。 つまり、ユーザーがフォームに入力した各フォームフィールドの値を抽出できます。 PDFデータとして送信されるフォームは、XMLデータではなくバイナリデータです。 フォームをPDFファイルとして保存したり、別のサービスにフォームを送信したりできます。 XMLとして送信されたフォームからデータを抽出し、フォームデータを使用してPDFドキュメントを作成する場合は、別のAEM Forms操作を呼び出します。 (「[送信されたXMLデータを使用したPDFドキュメントの作成](/help/forms/developing/creating-pdf-documents-submitted-xml.md)」を参照)。

次の図は、Webブラウザーに表示されるインタラクティブフォームから`HandleData`という名前のJavaサーブレットに送信されるデータを示しています。

![hs_hs_handlessubmit](assets/hs_hs_handlesubmit.png)

次の表で、この図の手順を説明します。

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
   <td><p><code>HandleData</code> Javaサーブレットには、データを取得するためのアプリケーションロジックが含まれています。</p></td>
  </tr>
 </tbody>
</table>

## 送信されたXMLデータの処理{#handling-submitted-xml-data}

フォームデータがXMLとして送信されると、送信されたデータを表すXMLデータを取得できます。 すべてのフォームフィールドは、XMLスキーマでノードとして表示されます。 ノードの値は、ユーザーが入力した値に対応します。 フォームの各フィールドがXMLデータ内のノードとして表示されるローンフォームを考えてみましょう。 各ノードの値は、ユーザーが入力する値に対応します。 ユーザーがローンフォームに次のフォームに表示されるデータを入力するとします。

![hs_hs_loanformdata](assets/hs_hs_loanformdata.png)

次の図に、FormsサービスクライアントAPIを使用して取得された、対応するXMLデータを示します。

![hs_hs_loandata](assets/hs_hs_loandata.png)

ローンフォームのフィールド。 これらの値は取得できます
Java XMLクラスの使用」を参照してください。

>[!NOTE]
>
>データをXMLデータとして送信するには、Designerでフォームデザインを正しく設定する必要があります。 XMLデータを送信するようにフォームデザインを適切に設定するには、フォームデザイン上にある「送信」ボタンがXMLデータを送信するように設定します。 XMLデータを送信するための「送信」ボタンの設定について詳しくは、[AEM Formsデザイナ](https://www.adobe.com/go/learn_aemforms_designer_63)を参照してください。

## 送信されたPDFデータの処理{#handling-submitted-pdf-data}

Formsサービスを呼び出すWebアプリケーションを考えてみましょう。 FormsサービスがインタラクティブPDFフォームをクライアントのWebブラウザーにレンダリングした後、ユーザーはフォームに入力し、PDFデータとして送信し返します。 Formsサービスは、PDFデータを受け取ると、そのPDFデータを別のサービスに送信したり、PDFファイルとして保存したりできます。 次の図に、アプリケーションのロジックのフローを示します。

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
   <td><p>ユーザーがインタラクティブフォームに入力し、送信ボタンをクリックします。 フォームがPDFデータとしてFormsサービスに送信されます。 このオプションはDesignerで設定されます。</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Formsサービスは、PDFデータをPDFファイルとして保存します。 </p></td>
  </tr>
 </tbody>
</table>

## 送信されたURL UTF-16データの処理{#handling-submitted-url-utf-16-data}

フォームデータがURL UTF-16データとして送信される場合、クライアントコンピューターはAdobe ReaderまたはAcrobat 8.1以降を必要とします。 また、フォームデザインにURLエンコードデータ(HTTP Post)を持つ送信ボタンが含まれ、データエンコードオプションがUTF-16の場合は、フォームデザインをメモ帳などのテキストエディターで変更する必要があります。 送信ボタンのエンコーディングオプションを`UTF-16LE`または`UTF-16BE`に設定できます。 Designerでは、この機能は提供されていません。

>[!NOTE]
>
>Formsサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

## 手順{#summary-of-steps}の概要

送信済みのフォームを処理するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. FormsクライアントAPIオブジェクトを作成します。
1. フォームデータを取得します。
1. フォーム送信に添付ファイルが含まれているかどうかを確認します。
1. 送信されたデータを処理します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めてください。

**FormsクライアントAPIオブジェクトの作成**

プログラムでFormsサービスのクライアントAPI操作を実行する前に、Formsサービスクライアントを作成する必要があります。 Java APIを使用している場合は、`FormsServiceClient`オブジェクトを作成します。 FormsのWebサービスAPIを使用している場合は、`FormsService`オブジェクトを作成します。

**フォームデータの取得**

送信されたフォームデータを取得するには、`FormsServiceClient`オブジェクトの`processFormSubmission`メソッドを呼び出します。 このメソッドを呼び出す場合は、送信済みフォームのコンテンツタイプを指定する必要があります。 クライアントのWebブラウザーからFormsサービスにデータが送信されると、XMLまたはPDFデータとして送信できます。 フォームフィールドに入力されたデータを取得するには、データをXMLデータとして送信します。

次の実行時オプションを設定して、PDFデータとして送信されたフォームからフォームフィールドを取得することもできます。

* 次の値を`processFormSubmission`メソッドにcontent typeパラメーターとして渡します。`CONTENT_TYPE=application/pdf`.
* `RenderOptionsSpec`オブジェクトの`PDFToXDP`値を`true`に設定します
* `RenderOptionsSpec`オブジェクトの`ExportDataFormat`値を`XMLData`に設定します

`processFormSubmission`メソッドを呼び出すときに、送信済みフォームのコンテンツタイプを指定します。 次のリストは、適用可能なコンテンツタイプの値を指定します。

* **text/xml**:PDFフォームがフォームデータをXMLとして送信する場合に使用するコンテンツタイプを表します。
* **application/x-www-form-urlencoded**:HTMLフォームがデータをXMLとして送信する場合に使用するコンテンツタイプを表します。
* **application/pdf**:PDFフォームがデータをPDFとして送信する場合に使用するコンテンツタイプを表します。

>[!NOTE]
>
>「送信されたFormsの処理」セクションに関連するクイック開始が3つあります。 Java APIクイック開始を使用してPDFとして送信された処理PDF formsでは、送信されたPDFデータの処理方法を示します。 このクイック開始で指定されているコンテンツタイプは`application/pdf`です。 Java APIクイック開始を使用してXMLとして送信されたPDF formsの処理では、PDFフォームから送信された送信済みXMLデータの処理方法を示します。 このクイック開始で指定されているコンテンツタイプは`text/xml`です。 同様に、Java APIクイック開始を使用したXML形式で送信されたHTMLフォームの処理では、HTMLフォームから送信された送信済みXMLデータの処理方法を示します。 このクイック開始で指定するコンテンツタイプは、application/x-www-form-urlencodedです。

Formsサービスに投稿されたフォームデータを取得し、その処理状態を判断します。 つまり、Formsサービスにデータを送信する場合、必ずしもFormsサービスがデータの処理を完了し、データを処理する準備ができているとは限りません。 例えば、計算を実行するために、データをFormsサービスに送信できます。 計算が完了すると、フォームがレンダリングされてユーザーに戻され、計算結果が表示されます。 送信されたデータを処理する前に、Formsサービスがデータの処理を完了したかどうかを確認することをお勧めします。

Formsサービスは、データの処理が完了したかどうかを示す次の値を返します。

* **0（送信）:** 送信されたデータを処理する準備ができました。
* **1（計算）:** Formsサービスはデータに対して計算操作を実行し、結果をユーザーにレンダリングして戻す必要があります。
* **2（検証）:Forms** サービスが検証したフォームデータと結果をユーザーにレンダリングして戻す必要があります。
* **3（次へ）:** 現在のページが、クライアントアプリケーションに書き込む必要のある結果と共に変更されました。
* **4(前**):現在のページが変更され、クライアントアプリケーションに書き込む必要のある結果が反映されています。

>[!NOTE]
>
>計算と検証は、ユーザーにレンダリングして戻す必要があります。 （「[フォームデータの計算](/help/forms/developing/calculating-form-data.md#calculating-form-data)」を参照）。

**フォーム送信に添付ファイルが含まれているかどうかを確認する**

Formsサービスに送信されたFormsには添付ファイルを含めることができます。 例えば、Acrobatの組み込みの添付ファイルペインを使用して、フォームと共に送信する添付ファイルを選択できます。 また、HTMLファイルと共にレンダリングされるHTMLツールバーを使用して、添付ファイルを選択することもできます。

フォームに添付ファイルが含まれているかどうかを確認したら、データを処理できます。 例えば、添付ファイルをローカルファイルシステムに保存できます。

>[!NOTE]
>
>添付ファイルを取得するには、フォームをPDFデータとして送信する必要があります。 フォームがXMLデータとして送信される場合、添付ファイルは送信されません。

**送信されたデータを処理する**

送信データのコンテンツタイプに応じて、送信されたXMLデータから個々のフォームフィールド値を抽出したり、送信されたPDFデータをPDFファイルとして保存したり（または別のサービスに送信したり）できます。 個々のフォームフィールドを抽出するには、送信されたXMLデータをXMLデータソースに変換し、`org.w3c.dom`クラスを使用してXMLデータソースの値を取得します。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[FormsサービスAPIクイック開始](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Formsサービスにドキュメントを渡す](/help/forms/developing/passing-documents-forms-service.md)

[FormsをレンダリングするWeb アプリケーションの作成](/help/forms/developing/creating-web-applications-renders-forms.md)

## Java API {#handle-submitted-forms-using-the-java-api}を使用して送信済みのフォームを処理する

FormsAPI(Java)を使用して、送信済みフォームを処理します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-forms-client.jarなどのクライアントJARファイルを含めます。

1. FormsクライアントAPIオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用し、`FormsServiceClient`オブジェクトを渡して、`ServiceClientFactory`オブジェクトを作成します。

1. フォームデータの取得

   * Javaサーブレットに投稿されたフォームデータを取得するには、コンストラクターを使用して`com.adobe.idp.Document`オブジェクトを作成し、コンストラクター内から`javax.servlet.http.HttpServletResponse`オブジェクトの`getInputStream`メソッドを呼び出します。
   * コンストラクタを使用して `RenderOptionsSpec` オブジェクトを作成します。`RenderOptionsSpec`オブジェクトの`setLocale`メソッドを呼び出し、ロケール値を指定する文字列値を渡して、ロケール値を設定します。

   >[!NOTE]
   >
   >`RenderOptionsSpec`オブジェクトの`setPDF2XDP`メソッドを呼び出して`true`を渡し、`setXMLData`を呼び出して`true`を渡すことで、送信されたPDFコンテンツからXDPまたはXMLデータを作成するようFormsサービスに指示できます。 その後、`FormsResult`オブジェクトの`getOutputXML`メソッドを呼び出して、XDP/XMLデータに対応するXMLデータを取得できます。 （`FormsResult`オブジェクトは`processFormSubmission`メソッドによって返されます。これについては、次のサブステップで説明します）。

   * `FormsServiceClient`オブジェクトの`processFormSubmission`メソッドを呼び出し、次の値を渡します。

      * フォームデータを含む`com.adobe.idp.Document`オブジェクト。
      * 関連するすべてのHTTPヘッダーを含む環境変数を指定するstring値。 処理するコンテンツタイプを指定します。 XMLデータを処理するには、このパラメーターに次の文字列値を指定します。`CONTENT_TYPE=text/xml`. PDFデータを処理するには、このパラメーターに次の文字列値を指定します。`CONTENT_TYPE=application/pdf`.
      * `HTTP_USER_AGENT`ヘッダー値を指定するstring値（例：）。 `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`」を選択します。このパラメーターの値はオプションです。
      * 実行時オプションを格納する`RenderOptionsSpec`オブジェクト。

      `processFormSubmission`メソッドは、フォーム送信の結果を含む`FormsResult`オブジェクトを返します。

   * `FormsResult`オブジェクトの`getAction`メソッドを呼び出して、Formsサービスがフォームデータの処理を完了したかどうかを判断します。 このメソッドが値`0`を返す場合、データは処理の準備ができています。



1. フォーム送信に添付ファイルが含まれているかどうかを確認する

   * `FormsResult`オブジェクトの`getAttachments`メソッドを呼び出します。 このメソッドは、フォームと共に送信されたファイルを含む`java.util.List`オブジェクトを返します。
   * `java.util.List`オブジェクトを繰り返し処理して、添付ファイルが存在するかどうかを確認します。 添付ファイルがある場合、各要素は`com.adobe.idp.Document`インスタンスになります。 `com.adobe.idp.Document`オブジェクトの`copyToFile`メソッドを呼び出し、`java.io.File`オブジェクトを渡すことで、添付ファイルを保存できます。

   >[!NOTE]
   >
   >この手順は、フォームがPDFとして送信される場合にのみ適用されます。

1. 送信されたデータを処理する

   * データコンテンツタイプが`application/vnd.adobe.xdp+xml`または`text/xml`の場合は、XMLデータ値を取得するためのアプリケーションロジックを作成します。

      * `FormsResult`オブジェクトの`getOutputContent`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトを作成します。
      * `java.io.DataInputStream`コンストラクターを呼び出し、`com.adobe.idp.Document`オブジェクトを渡して、`java.io.InputStream`オブジェクトを作成します。
      * 静的`org.w3c.dom.DocumentBuilderFactory`オブジェクトの`newInstance`メソッドを呼び出して、`org.w3c.dom.DocumentBuilderFactory`オブジェクトを作成します。
      * `org.w3c.dom.DocumentBuilderFactory`オブジェクトの`newDocumentBuilder`メソッドを呼び出して、`org.w3c.dom.DocumentBuilder`オブジェクトを作成します。
      * `org.w3c.dom.DocumentBuilder`オブジェクトの`parse`メソッドを呼び出し、`java.io.InputStream`オブジェクトを渡して、`org.w3c.dom.Document`オブジェクトを作成します。
      * XMLドキュメント内の各ノードの値を取得します。 このタスクを実行する1つの方法は、2つのパラメーターを受け取るカスタムメソッドを作成することです。`org.w3c.dom.Document`オブジェクトと、値を取得するノードの名前。 このメソッドは、ノードの値を表すstring値を返します。 このプロセスの後のコード例では、このカスタムメソッドは`getNodeText`と呼ばれます。 このメソッドの本文が表示されます。
   * データコンテンツタイプが`application/pdf`の場合は、送信されたPDFデータをPDFファイルとして保存するためのアプリケーションロジックを作成します。

      * `FormsResult`オブジェクトの`getOutputContent`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトを作成します。
      * パブリックコンストラクタを使用して`java.io.File`オブジェクトを作成します。 ファイル名の拡張子としてPDFを必ず指定してください。
      * `com.adobe.idp.Document`オブジェクトの`copyToFile`メソッドを呼び出し、`java.io.File`オブジェクトを渡して、PDFファイルを入力します。


**関連トピック**

[クイック開始（SOAPモード）:Java APIを使用してXMLとして送信されたPDF formsの処理](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-xml-using-the-java-api)

[クイック開始（SOAPモード）:Java APIを使用したXML形式で送信されたHTMLフォームの処理](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-html-forms-submitted-as-xml-using-the-java-api)

[クイック開始（SOAPモード）:Java APIを使用してPDFとして送信されたPDF formsの処理](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-pdf-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## WebサービスAPI {#handle-submitted-pdf-data-using-the-web-service-api}を使用して送信されたPDFデータを処理する

FormsAPI（Webサービス）を使用して、送信済みフォームを処理します。

1. プロジェクトファイルを含める

   * FormsサービスのWSDLを使用するJavaプロキシクラスを作成します。
   * クラスパスにJavaプロキシクラスを含めます。

1. FormsクライアントAPIオブジェクトの作成

   `FormsService`オブジェクトを作成し、認証値を設定します。

1. フォームデータの取得

   * Javaサーブレットに投稿されたフォームデータを取得するには、コンストラクタを使用して`BLOB`オブジェクトを作成します。
   * `javax.servlet.http.HttpServletResponse`オブジェクトの`getInputStream`メソッドを呼び出して、`java.io.InputStream`オブジェクトを作成します。
   * コンストラクターを使用し、`java.io.InputStream`オブジェクトの長さを渡して、`java.io.ByteArrayOutputStream`オブジェクトを作成します。
   * `java.io.InputStream`オブジェクトの内容を`java.io.ByteArrayOutputStream`オブジェクトにコピーします。
   * `java.io.ByteArrayOutputStream`オブジェクトの`toByteArray`メソッドを呼び出して、バイト配列を作成します。
   * `BLOB`オブジェクトを入力するには、`setBinaryData`メソッドを呼び出し、バイト配列を引数として渡します。
   * コンストラクタを使用して `RenderOptionsSpec` オブジェクトを作成します。`RenderOptionsSpec`オブジェクトの`setLocale`メソッドを呼び出し、ロケール値を指定する文字列値を渡して、ロケール値を設定します。
   * `FormsService`オブジェクトの`processFormSubmission`メソッドを呼び出し、次の値を渡します。

      * フォームデータを含む`BLOB`オブジェクト。
      * 関連するすべてのHTTPヘッダーを含む環境変数を指定するstring値。 処理するコンテンツタイプを指定します。 XMLデータを処理するには、このパラメーターに次の文字列値を指定します。`CONTENT_TYPE=text/xml`. PDFデータを処理するには、このパラメーターに次の文字列値を指定します。`CONTENT_TYPE=application/pdf`.
      * `HTTP_USER_AGENT`ヘッダー値を指定するstring値。例：`Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`
      * 実行時オプションを格納する`RenderOptionsSpec`オブジェクト。
      * メソッドによって入力される空の`BLOBHolder`オブジェクト。
      * メソッドによって入力される空の`javax.xml.rpc.holders.StringHolder`オブジェクト。
      * メソッドによって入力される空の`BLOBHolder`オブジェクト。
      * メソッドによって入力される空の`BLOBHolder`オブジェクト。
      * メソッドによって入力される空の`javax.xml.rpc.holders.ShortHolder`オブジェクト。
      * メソッドによって入力される空の`MyArrayOf_xsd_anyTypeHolder`オブジェクト。 このパラメーターは、フォームと共に送信された添付ファイルを保存するために使用されます。
      * 送信されたフォームと共にメソッドによって入力される、空の`FormsResultHolder`オブジェクト。

      `processFormSubmission`メソッドは、フォーム送信の結果を`FormsResultHolder`パラメーターに入力します。

   * `FormsResult`オブジェクトの`getAction`メソッドを呼び出して、Formsサービスがフォームデータの処理を完了したかどうかを判断します。 このメソッドが値`0`を返す場合、フォームデータは処理の準備ができています。 `FormsResultHolder`オブジェクトの`value`データメンバの値を取得することで、`FormsResult`オブジェクトを取得できます。


1. フォーム送信に添付ファイルが含まれているかどうかを確認する

   `MyArrayOf_xsd_anyTypeHolder`オブジェクトの`value`データメンバの値を取得します（`MyArrayOf_xsd_anyTypeHolder`オブジェクトが`processFormSubmission`メソッドに渡されました）。 このデータメンバは`Objects`の配列を返します。 `Object`配列内の各要素は`Object`で、フォームと共に送信されたファイルに対応します。 配列内の各要素を取得し、`BLOB`オブジェクトにキャストできます。

1. 送信されたデータを処理する

   * データコンテンツタイプが`application/vnd.adobe.xdp+xml`または`text/xml`の場合は、XMLデータ値を取得するためのアプリケーションロジックを作成します。

      * `FormsResult`オブジェクトの`getOutputContent`メソッドを呼び出して、`BLOB`オブジェクトを作成します。
      * `BLOB`オブジェクトの`getBinaryData`メソッドを呼び出して、バイト配列を作成します。
      * `java.io.ByteArrayInputStream`コンストラクターを呼び出し、バイト配列を渡して、`java.io.InputStream`オブジェクトを作成します。
      * 静的`org.w3c.dom.DocumentBuilderFactory`オブジェクトの`newInstance`メソッドを呼び出して、`org.w3c.dom.DocumentBuilderFactory`オブジェクトを作成します。
      * `org.w3c.dom.DocumentBuilderFactory`オブジェクトの`newDocumentBuilder`メソッドを呼び出して、`org.w3c.dom.DocumentBuilder`オブジェクトを作成します。
      * `org.w3c.dom.DocumentBuilder`オブジェクトの`parse`メソッドを呼び出し、`java.io.InputStream`オブジェクトを渡して、`org.w3c.dom.Document`オブジェクトを作成します。
      * XMLドキュメント内の各ノードの値を取得します。 このタスクを実行する1つの方法は、2つのパラメーターを受け取るカスタムメソッドを作成することです。`org.w3c.dom.Document`オブジェクトと、値を取得するノードの名前。 このメソッドは、ノードの値を表すstring値を返します。 このプロセスの後のコード例では、このカスタムメソッドは`getNodeText`と呼ばれます。 このメソッドの本文が表示されます。
   * データコンテンツタイプが`application/pdf`の場合は、送信されたPDFデータをPDFファイルとして保存するためのアプリケーションロジックを作成します。

      * `FormsResult`オブジェクトの`getOutputContent`メソッドを呼び出して、`BLOB`オブジェクトを作成します。
      * `BLOB`オブジェクトの`getBinaryData`メソッドを呼び出して、バイト配列を作成します。
      * パブリックコンストラクタを使用して`java.io.File`オブジェクトを作成します。 ファイル名の拡張子としてPDFを必ず指定してください。
      * コンストラクタを使用して `java.io.FileOutputStream` オブジェクトを渡すことによって、`java.io.File` オブジェクトを作成します。
      * `java.io.FileOutputStream`オブジェクトの`write`メソッドを呼び出し、バイト配列を渡して、PDFファイルを入力します。


**関連トピック**

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)