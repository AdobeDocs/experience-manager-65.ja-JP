---
title: 送信済みフォームの処理
seo-title: Handling Submitted Forms
description: Forms サービスを使用して、インタラクティブフォームに入力された送信済みデータを取得します。ユーザーは、XML 形式、PDF 形式、URL UTF-16 形式でフォームデータを送信できます。
seo-description: Use the Forms service to retrieve the submitted data entered in an interactive form. The user can submit the form data in XML, PDF, and URL UTF-16 formats.
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
source-wordcount: '2904'
ht-degree: 100%

---

# 送信済みフォームの処理 {#handling-submitted-forms}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

ユーザーがインタラクティブフォームに入力できる Web ベースのアプリケーションでは、データをサーバーに送り返す必要があります。Forms サービスを使用すると、ユーザーがインタラクティブフォームに入力したデータを取得できます。データを取得したら、ビジネス要件に合わせてそのデータを処理できます。例えば、そのデータをデータベースに格納したり、別のアプリケーションに送信したり、別のサービスに送信したり、フォームデザインで結合したり、Web ブラウザーに表示したりすることができます。

フォームデータは、XML データまたは PDF データとして Forms サービスに送信されます（その選択は Designer で設定します）。XML 形式で送信されたフォームを使用すると、個々のフィールドデータ値を抽出できます。つまり、ユーザーがフォームに入力した各フォームフィールドの値を抽出できます。PDF 形式で送信されたフォームは、XML データではなくバイナリデータです。そのフォームは、PDF ファイルとして保存するか、別のサービスに送信することができます。XML 形式で送信されたフォームからデータを抽出し、そのフォームデータを使用して PDF ドキュメントを作成する場合は、別の AEM Forms 操作を呼び出します。（[送信された XML データを使用して PDF ドキュメントを作成する](/help/forms/developing/creating-pdf-documents-submitted-xml.md)を参照してください）

次の図は、Web ブラウザーに表示されたインタラクティブフォームから `HandleData` という名前の Java サーブレットに送信されるデータを示しています。

![hs_hs_handlesubmit](assets/hs_hs_handlesubmit.png)

次の表で、図の手順を説明します。

<table>
 <thead>
  <tr>
   <th><p>手順</p></th>
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
   <td><p>データが XML データとして <code>HandleData</code> Java サーブレットに送信されます。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p><code>HandleData</code> Java サーブレットには、データを取得するアプリケーションロジックが含まれています。</p></td>
  </tr>
 </tbody>
</table>

## 送信された XML データの処理 {#handling-submitted-xml-data}

フォームデータを XML 形式で送信すると、送信データを表す XML データを取得できます。すべてのフォームフィールドは、XML スキーマのノードとして表示されます。ノードの値は、ユーザーが入力した値に対応します。フォーム内の各フィールドが XML データ内のノードとして表示されるローン申請書について考えてみましょう。各ノードの値は、ユーザーが入力する値に対応します。ユーザーが次のフォームに示すデータを使用してローン申請書に入力するとします。

![hs_hs_loanformdata](assets/hs_hs_loanformdata.png)

次の図に、Forms サービスクライアント API を使用して取得される、対応する XML データを示します。

![hs_hs_loandata](assets/hs_hs_loandata.png)

ローン申請書のフィールド。これらの値は、Java XML クラスを
使用して取得できます。

>[!NOTE]
>
>データを XML データとして送信するには、Designer でフォームデザインを正しく設定する必要があります。XML データを送信するようにフォームデザインを適切に設定するには、フォームデザイン上の「送信」ボタンが XML データを送信するように設定されていることを確認します。XML データを送信する「送信」ボタンの設定について詳しくは、[AEM Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63_jp) を参照してください。

## 送信された PDF データの処理 {#handling-submitted-pdf-data}

Forms サービスを呼び出す web アプリケーションについて考えます。Forms サービスがインタラクティブ PDF フォームをクライアント web ブラウザーにレンダリングしたら、ユーザーはフォームに入力し、フォームを PDF データとして送り返します。Forms サービスは PDF データを受け取ると、PDF データを別のサービスに送信したり、PDF ファイルとして保存したりできます。次の図に、アプリケーションのロジック・フローを示します。

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
   <td><p>Web ページには、Forms サービスを呼び出す Java サーブレットにアクセスするリンクが含まれています。</p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Forms サービスは、インタラクティブな PDF フォームをクライアント web ブラウザーにレンダリングします。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>ユーザーはインタラクティブフォームに入力し、「送信」ボタンをクリックします。 フォームは、PDF データとして Forms サービスに送り返されます。 このオプションは Designer で設定します。</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Forms サービスは、この PDF データを PDF ファイルとして保存します。 </p></td>
  </tr>
 </tbody>
</table>

## 送信された URL UTF-16 データの処理 {#handling-submitted-url-utf-16-data}

フォームデータが URL UTF-16 データとして送信される場合、クライアントコンピューターには Adobe Reader または Acrobat 8.1 以降が必要です。 また、フォームデザインに URL エンコードされたデータ (HTTP Post) を含む「送信」ボタンが含まれ、データエンコードオプションが UTF-16 の場合、フォームデザインはメモ帳などのテキストエディターで変更する必要があります。 エンコーディングオプションは、送信ボタン用に `UTF-16LE` または `UTF-16BE` のいずれかに設定できます。Designer はこの機能を提供していません。

>[!NOTE]
>
>AEM Forms サービスについて詳しくは、[AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

## 手順の概要 {#summary-of-steps}

送信されたフォームを処理するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Forms Client API オブジェクトを作成します。
1. フォームデータを取得します。
1. フォーム送信に添付ファイルが含まれているかどうかを確認します。
1. 送信されたデータを処理します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**Forms Client API オブジェクトの作成**

Forms Service Client API 操作をプログラムで実行する前に、Forms サービスクライアントを作成する必要があります。 Java API を使用している場合は、`FormsServiceClient` オブジェクトを作成します。Forms Web サービス API を使用している場合は、`FormsService` オブジェクトを作成します。

**フォームデータを取得**

送信されたフォームデータを取得するには、`FormsServiceClient` オブジェクトの `processFormSubmission` メソッドを呼び出します。このメソッドを呼び出す場合は、送信されたフォームのコンテンツタイプを指定する必要があります。 クライアントの Web ブラウザーから Forms サービスにデータが送信された場合、そのデータは XML または PDF データとして送信できます。 フォームフィールドに入力されたデータを取得するには、データを XML データとして送信します。

また、次の実行時オプションを設定して、PDF データとして送信されたフォームからフォームフィールドを取得することもできます。

* `CONTENT_TYPE=application/pdf` の値をコンテンツタイプパラメーターとして `processFormSubmission` メソッドに渡します。
* `RenderOptionsSpec` オブジェクトの `PDFToXDP` 値を `true` に設定します
* `RenderOptionsSpec` オブジェクトの `ExportDataFormat` 値を `XMLData` に設定します

`processFormSubmission` メソッドを呼び出すときに、送信されたフォームのコンテンツタイプを指定します。次のリストで、適用可能なコンテンツタイプの値を指定します。

* **text/xml**：PDF フォームがフォームデータを XML として送信するときに使用するコンテンツタイプを表します。
* **application/x-www-form-urlencoded**：HTML フォームがデータを XML として送信するときに使用するコンテンツタイプを表します。
* **application/pdf**：PDF フォームがデータを PDF として送信するときに使用するコンテンツタイプを表します。

>[!NOTE]
>
>送信済みフォームの処理のセクションに対応する 3 つのクイックスタートが関連付けられていることがわかるでしょう。 Java API クイックスタートを使用して PDF として送信された PDF フォームの処理には、送信済み PDF データの処理方法を示しています。このクイックスタートで指定されているコンテンツタイプは `application/pdf` です。Java API クイックスタートを使用して XML として送信された PDF フォームの処理は、PDF フォームから送信された送信済み XML データを処理する方法を示しています。 このクイックスタートで指定されているコンテンツタイプは `text/xml` です。同様に、Java API クイックスタートを使用して、XML 形式で送信されたHTMLフォームの処理で、HTMLフォームから送信された送信済み XML データを処理する方法を示します。 このクイックスタートで指定するコンテンツタイプは、 application/x-www-form-urlencoded です。

Forms サービスに投稿されたフォームデータを取得し、その処理状態を判断します。 つまり、データが Forms サービスに送信された場合、必ずしも Forms サービスによるデータの処理が完了し、データの処理準備が整ったとは限りません。 例えば、計算を実行できるよう、Forms サービスにデータを送信できます。計算が完了すると、フォームはレンダリングされてユーザーに返され、計算結果が表示されます。送信されたデータを処理する前に、Forms サービスがデータの処理を完了したかどうかを確認することをお勧めします。

Forms サービスは、データの処理が完了したかどうかを示す次の値を返します。

* **0（送信）：**&#x200B;送信したデータを処理する準備が整っています。
* **1（計算）：** Forms サービスがデータに対して計算操作を実行したので、結果をユーザーに返す必要があります。
* **2（検証）：** Forms サービスがフォームデータを検証したので、結果をユーザーに返す必要があります。
* **3（次へ）：**&#x200B;現在のページが変更されたので、その結果をクライアントアプリケーションに書き込む必要があります。
* **4（前へ**）：現在のページが変更されたので、その結果をクライアントアプリケーションに書き込む必要があります。

>[!NOTE]
>
>計算と検証の結果は、ユーザーに返す必要があります。（[フォームデータの計算](/help/forms/developing/calculating-form-data.md#calculating-form-data)を参照してください。

**送信フォームに添付ファイルが含まれているかどうかの確認**

Forms サービスに送信された Forms には、添付ファイルが含まれていることがあります。例えば、Acrobat に標準で備わっている添付ファイルウィンドウを使用すると、ユーザーは添付ファイルを選択して、フォームとともに送信できます。また、ユーザーは、HTML ファイルとともにレンダリングされる HTML ツールバーを使用して、添付ファイルを選択することもできます。

フォームに添付ファイルが含まれているかどうかを確認したら、そのデータを処理できます。例えば、添付ファイルをローカルファイルシステムに保存できます。

>[!NOTE]
>
>添付ファイルを取得するために、フォームは PDF データとして送信される必要があります。フォームが XML データとして送信された場合、添付ファイルは送信されません。

**送信されたデータの処理**

送信データのコンテンツタイプによって異なりますが、送信されたのが XML データであれば個々のフォームフィールドの値を抽出することができ、送信されたのが PDF データであれば PDF ファイルとして保存（または別のサービスに送信）することができます。個々のフォームフィールドを抽出するには、送信された XML データを XML データソースに変換し、`org.w3c.dom` クラスを使用して XML データソースの値を取得します。

**関連トピック**

[AEM Forms Java ライブラリファイルの組み込み](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms サービス API のクイックスタート](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Forms サービスにドキュメントを渡す](/help/forms/developing/passing-documents-forms-service.md)

[Forms をレンダリングする web アプリケーションの作成](/help/forms/developing/creating-web-applications-renders-forms.md)

## Java API を使用して送信フォームを処理する {#handle-submitted-forms-using-the-java-api}

Forms API（Java）を使用して、送信されたフォームを処理します。

1. プロジェクトファイルを含める

   adobe-forms-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. Forms Client API オブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用し、`ServiceClientFactory` オブジェクトを渡すことによって、`FormsServiceClient` オブジェクトを作成します。

1. フォームデータを取得

   * Java サーブレットに投稿されたフォームデータを取得するには、コンストラクタを使用し、そのコンストラクタ内から `javax.servlet.http.HttpServletResponse` オブジェクトの `getInputStream` メソッドを呼び出すことによって、`com.adobe.idp.Document` オブジェクトを作成します。
   * コンストラクタを使用して `RenderOptionsSpec` オブジェクトを作成します。`RenderOptionsSpec` オブジェクトの `setLocale` メソッドを呼び出し、ロケール値を指定する文字列値を渡すことによって、ロケール値を設定します。

   >[!NOTE]
   >
   >`RenderOptionsSpec` オブジェクトの `setPDF2XDP` メソッドを呼び出し `true` を渡すか、`setXMLData` を呼び出し `true` を渡すことによって、Forms サービスに対し、送信された PDF コンテンツから XDP データまたは XML データを作成するよう命令できます。その後、`FormsResult` オブジェクトの `getOutputXML` メソッドを呼び出して、XDP／XML データに対応する XML データを取得することができます。（`FormsResult` オブジェクトが `processFormSubmission` メソッドによって返されます。これについては、次の下位手順で説明します）。

   * `FormsServiceClient` オブジェクトの `processFormSubmission` メソッドを呼び出して、次の値を渡します。

      * フォームデータを含む `com.adobe.idp.Document` オブジェクト。
      * 関連するすべての HTTP ヘッダーを含む環境変数を指定する文字列値。 処理するコンテンツタイプを指定します。 XML データを処理するには、パラメーター `CONTENT_TYPE=text/xml` に次の文字列値を指定します。PDF データを処理するには、パラメーター `CONTENT_TYPE=application/pdf` に次の文字列値を指定します。
      * `HTTP_USER_AGENT` ヘッダー値を指定する文字列値（例：`Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`）。このパラメーター値はオプションです。
      * 実行時オプションを保存する `RenderOptionsSpec` オブジェクト。

      `processFormSubmission` メソッドは、フォーム送信の結果を含む `FormsResult` オブジェクトを返します。

   * `FormsResult` オブジェクトの `getAction` メソッドを呼び出して、Forms サービスがフォームデータの処理を完了したかどうかを判断します。このメソッドが値 `0` を返した場合、データを処理する準備が整っています。



1. フォーム送信に添付ファイルが含まれているかどうかを確認します

   *  `FormsResult` オブジェクトの `getAttachments` メソッドを呼び出します。このメソッドは、フォームと共に送信されたファイルを含む `java.util.List` オブジェクトを返します。
   * `java.util.List` オブジェクトを反復処理して、添付ファイルが存在するかどうかを確認します。 添付ファイルがある場合、各要素は `com.adobe.idp.Document` インスタンスです。`com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを呼び出して `java.io.File` オブジェクトを渡すことで、添付ファイルを保存できます。

   >[!NOTE]
   >
   >この手順は、フォームが PDF として送信された場合にのみ適用されます。

1. 送信されたデータを処理

   * データコンテンツタイプが `application/vnd.adobe.xdp+xml` または `text/xml` の場合、XML データ値を取得するアプリケーションロジックを作成します。

      * `FormsResult` オブジェクトの `getOutputContent` メソッドを呼び出すことによって `com.adobe.idp.Document` オブジェクトを作成します。
      * `java.io.DataInputStream` コンストラクターを呼び出して `com.adobe.idp.Document` オブジェクトを渡すことによって、`java.io.InputStream` オブジェクトを作成します。
      * 静的な `org.w3c.dom.DocumentBuilderFactory` オブジェクトの `newInstance` メソッドを呼び出して、`org.w3c.dom.DocumentBuilderFactory` オブジェクトを作成します。
      * `org.w3c.dom.DocumentBuilderFactory` オブジェクトの `newDocumentBuilder` メソッドを呼び出すことによって `org.w3c.dom.DocumentBuilder` オブジェクトを作成します。
      * `org.w3c.dom.DocumentBuilder` オブジェクトの `parse` メソッドを呼び出して `java.io.InputStream` オブジェクトを渡すことによって `org.w3c.dom.Document` オブジェクトを作成します。
      * XML ドキュメント内の各ノードの値を取得します。 このタスクを実行する 1 つの方法は、`org.w3c.dom.Document` オブジェクトおよび値を取得するノードの名前の 2 つのパラメーターを受け入れるカスタムメソッドを作成することです。このメソッドは、ノードの値を表す文字列値を返します。 このプロセスに続くコード例では、このカスタムメソッドは `getNodeText` と呼ばれています。このメソッドの本文を示します。
   * データコンテンツタイプが `application/pdf` の場合、アプリケーションロジックを作成して、送信された PDF データを PDF ファイルとして保存します。

      * `FormsResult` オブジェクトの `getOutputContent` メソッドを呼び出すことによって `com.adobe.idp.Document` オブジェクトを作成します。
      * パブリックコンストラクターを使用して `java.io.File` オブジェクトを作成します。ファイル名の拡張子には必ず PDF を指定してください。
      * `com.adobe.idp.Document` オブジェクトの `copyToFile` メソッドを呼び出して `java.io.File` オブジェクトを渡すことによって、PDFファイルに入力します。


**関連トピック**

[クイックスタート（SOAP モード）：Java API を使用して、XML として送信された PDF Forms の処理](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-xml-using-the-java-api)

[クイックスタート（SOAP モード）：Java API を使用して、XML として送信された HTML フォームの処理](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-html-forms-submitted-as-xml-using-the-java-api)

[クイックスタート（SOAP モード）：Java API を使用して、PDF として送信された PDF フォームの処理](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-handling-pdf-forms-submitted-as-pdf-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Web サービス API を使用して送信された PDF データを処理します {#handle-submitted-pdf-data-using-the-web-service-api}

Forms API（Web サービス）を使用して送信されたフォームを処理します。

1. プロジェクトファイルを含める

   * Forms Service WSDL を使用する Java プロキシクラスを作成します。
   * Java プロキシクラスをクラスパスに含めます。

1. Forms Client API オブジェクトの作成

   `FormsService` オブジェクトを作成し、認証値を設定します。

1. フォームデータを取得

   * Java サーブレットに投稿されたフォームデータを取得するには、コンストラクタ―を使用して `BLOB` オブジェクトを作成します。
   * `javax.servlet.http.HttpServletResponse` オブジェクトの `getInputStream` メソッドを呼び出すことによって `java.io.InputStream` オブジェクトを作成します。
   * コンストラクターを使用して `java.io.InputStream` オブジェクトの長さを渡すことによって、`java.io.ByteArrayOutputStream` オブジェクトを作成します。
   * `java.io.InputStream` オブジェクトの内容を `java.io.ByteArrayOutputStream` オブジェクトにコピーします。
   * `java.io.ByteArrayOutputStream` オブジェクトの `toByteArray` メソッドを呼び出してバイト配列を作成します。
   *  `setBinaryData` メソッドを呼び出してバイト配列を引数として渡すことによって、`BLOB` オブジェクトに入力します。
   * コンストラクターを使用して `RenderOptionsSpec` オブジェクトを作成します。 `RenderOptionsSpec` オブジェクトの `setLocale` メソッドを呼び出してロケール値を指定する文字列値を渡すことによって、ロケール値を設定します。
   * `FormsService` オブジェクトの `processFormSubmission` メソッドを呼び出して、次の値を渡します。

      * フォームデータを含む `BLOB` オブジェクト。
      * 関連するすべての HTTP ヘッダーを含む環境変数を指定する文字列値。 処理するコンテンツタイプを指定します。 XML データを処理するには、パラメーター `CONTENT_TYPE=text/xml` に次の文字列値を指定します。PDF データを処理するには、このパラメーターに文字列値 `CONTENT_TYPE=application/pdf` を指定します。
      * `HTTP_USER_AGENT` ヘッダー値を指定する文字列値（例： `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`）。
      * 実行時オプションを保存する `RenderOptionsSpec` オブジェクト。
      * メソッドによって設定される空の `BLOBHolder` オブジェクト。
      * メソッドによって設定される空の `javax.xml.rpc.holders.StringHolder` オブジェクト。
      * メソッドによって設定される空の `BLOBHolder` オブジェクト。
      * メソッドによって設定される空の `BLOBHolder` オブジェクト。
      * メソッドによって設定される空の `javax.xml.rpc.holders.ShortHolder` オブジェクト。
      * メソッドによって設定される空の `MyArrayOf_xsd_anyTypeHolder` オブジェクト。 このパラメーターは、フォームと共に送信される添付ファイルを保存するために使用されます。
      * 送信されるフォームを使用してメソッドによって設定される空の `FormsResultHolder` オブジェクト。

      `processFormSubmission` メソッドによって `FormsResultHolder` パラメーターにフォーム送信の結果が入力されます。

   * `FormsResult` オブジェクトの `getAction` メソッドを呼び出して、Forms サービスがフォームデータの処理を完了したかどうかを判断します。このメソッドが値 `0` を返す場合、フォームデータを処理する準備が整っています。`FormsResultHolder` オブジェクトの `value` データメンバーの値を取得することで、`FormsResult` オブジェクトを取得できます。


1. フォーム送信に添付ファイルが含まれているかどうかを確認します

   `MyArrayOf_xsd_anyTypeHolder` オブジェクトの `value` データメンバーの値を取得します（`MyArrayOf_xsd_anyTypeHolder` オブジェクトは `processFormSubmission`メソッドに渡されました）。このデータメンバーは `Objects` の配列を返します。`Object` 配列内の各要素は、フォームとともに送信されたファイルに対応する `Object` です。配列内の各要素を取得し、`BLOB` オブジェクトにキャストできます。

1. 送信されたデータを処理

   * データコンテンツタイプが `application/vnd.adobe.xdp+xml` または `text/xml` の場合、XML データ値を取得するアプリケーションロジックを作成します。

      * `FormsResult` オブジェクトの `getOutputContent` メソッドを呼び出すことによって `BLOB` オブジェクトを作成します。
      * `BLOB` オブジェクトの `getBinaryData` メソッドを呼び出してバイト配列を作成します。
      * `java.io.ByteArrayInputStream` コンストラクターを呼び出してバイト配列を渡すことにより、`java.io.InputStream` オブジェクトを作成します。
      * 静的な `org.w3c.dom.DocumentBuilderFactory` オブジェクトの `newInstance` メソッドを呼び出して、`org.w3c.dom.DocumentBuilderFactory` オブジェクトを作成します。
      * `org.w3c.dom.DocumentBuilderFactory` オブジェクトの `newDocumentBuilder` メソッドを呼び出すことによって `org.w3c.dom.DocumentBuilder` オブジェクトを作成します。
      * `org.w3c.dom.DocumentBuilder` オブジェクトの `parse` メソッドを呼び出して `java.io.InputStream` オブジェクトを渡すことによって `org.w3c.dom.Document` オブジェクトを作成します。
      * XML ドキュメント内の各ノードの値を取得します。 このタスクを実行する 1 つの方法は、`org.w3c.dom.Document` オブジェクトおよび値を取得するノードの名前の 2 つのパラメーターを受け入れるカスタムメソッドを作成することです。このメソッドは、ノードの値を表す文字列値を返します。 このプロセスに続くコード例では、このカスタムメソッドは `getNodeText` と呼ばれています。このメソッドの本文を示します。
   * データコンテンツタイプが `application/pdf` の場合、アプリケーションロジックを作成して、送信された PDF データを PDF ファイルとして保存します。

      *  `FormsResult` オブジェクトの `getOutputContent` メソッドを呼び出すことによって `BLOB` オブジェクトを作成します。
      * `BLOB` オブジェクトの `getBinaryData` メソッドを呼び出してバイト配列を作成します。
      * コンストラクターを使用して `java.io.File` オブジェクトを作成します。ファイル名の拡張子には必ず PDF を指定してください。
      * コンストラクターを使用して `java.io.FileOutputStream` オブジェクトを渡すことによって、`java.io.File` オブジェクトを作成します。
      * `java.io.FileOutputStream` オブジェクトの `write` メソッドを呼び出してバイト配列を渡すことによって、PDF ファイルを生成します。


**関連トピック**

[Base64 エンコーディングを使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
