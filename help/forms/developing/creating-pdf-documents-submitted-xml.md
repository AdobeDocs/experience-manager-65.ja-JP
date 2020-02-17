---
title: 送信済みXMLデータを使用したPDFドキュメントの作成
seo-title: 送信済みXMLデータを使用したPDFドキュメントの作成
description: 'null'
seo-description: 'null'
uuid: 2676c614-8988-451b-ac7c-bd07731a3f5f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 62490230-a24e-419d-95bb-c0bb04a03f96
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 送信済みXMLデータを使用したPDFドキュメントの作成 {#creating-pdf-documents-with-submittedxml-data}

## 送信済みXMLデータを使用したPDFドキュメントの作成 {#creating-pdf-documents-with-submitted-xml-data}

ユーザーがインタラクティブフォームに入力できるWebベースのアプリケーションでは、データをサーバーに送信し直す必要があります。 Formsサービスを使用すると、ユーザーがインタラクティブフォームに入力したフォームデータを取得できます。 その後、フォームデータを別のAEM Formsサービス操作に渡し、そのデータを使用してPDFドキュメントを作成できます。

>[!NOTE]
>
>この内容を読む前に、送信されたフォームの処理に関する十分な理解を得ることをお勧めします。 フォームデザインと送信済みXMLデータとの関係などの概念については、「送信済みのフォームの処理」を参照してください。

次の3つのAEM Formsサービスを含むワークフローについて考えてみましょう。

* ユーザーがWebベースのアプリケーションからFormsサービスにXMLデータを送信します。
* Formsサービスは、送信済みのフォームを処理し、フォームフィールドを抽出するために使用します。 フォームデータは処理できます。 例えば、データをエンタープライズデータベースに送信できます。
* フォームデータは、非インタラクティブPDFドキュメントを作成するためにOutputサービスに送信されます。
* 非インタラクティブPDFドキュメントは、Content Services（非推奨）に保存されます。

次の図に、このワークフローを視覚的に示します。

![cd_cd_finsrv_architecture_xml_pdf1](assets/cd_cd_finsrv_architecture_xml_pdf1.png)

ユーザーがクライアントWebブラウザーからフォームを送信した後、非インタラクティブPDFドキュメントはContent Services（非推奨）に保存されます。 次の図に、Content Services（非推奨）に保存されているPDFドキュメントを示します。

![cd_cd_cs_gui](assets/cd_cd_cs_gui.png)

### 手順の概要 {#summary-of-steps}

送信されたXMLデータを含む非インタラクティブPDFドキュメントを作成し、Content Services（非推奨）のPDFドキュメントに保存するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Forms、OutputおよびDocument Managementオブジェクトを作成します。
1. Formsサービスを使用してフォームデータを取得します。
1. Outputサービスを使用して、非インタラクティブPDFドキュメントを作成します。
1. Document Managementサービスを使用して、PDFフォームをContent Services（非推奨）に保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

**Forms、OutputおよびDocument Managementオブジェクトの作成**

プログラムでFormsサービスAPI操作を実行する前に、フォームクライアントAPIオブジェクトを作成します。 同様に、このワークフローはOutputおよびDocument Managementサービスを呼び出すので、Output Client APIオブジェクトとDocument Management Client APIオブジェクトの両方を作成します。

**Formsサービスを使用したフォームデータの取得**

Formsサービスに送信されたフォームデータを取得します。 送信されたデータは、ビジネス要件に合わせて処理できます。 例えば、フォームデータをエンタープライズデータベースに格納できます。 ただし、非インタラクティブPDFドキュメントを作成する場合は、フォームデータがOutputサービスに渡されます。

**Outputサービスを使用して、非インタラクティブPDFドキュメントを作成します。**

Outputサービスを使用して、フォームデザインとXMLフォームデータに基づく非インタラクティブPDFドキュメントを作成します。 ワークフローでは、フォームデータはFormsサービスから取得されます。

**Document Managementサービスを使用してPDFフォームをContent Services（非推奨）に保存する**

Document ManagementサービスAPIを使用して、PDFドキュメントをContent Services（非推奨）に保存します。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[FormsサービスAPIのクイックスタート](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

### Java APIを使用した送信済みXMLデータを使用したPDFドキュメントの作成 {#create-a-pdf-document-with-submitted-xml-data-using-the-java-api}

Forms、Output、およびDocument Management API(Java)を使用して、送信されたXMLデータを使用してPDFドキュメントを作成します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-forms-client.jar、adobe-output-client.jar、adobe-contentservices-client.jarなどのクライアントJARファイルを含めます。

1. Forms、OutputおよびDocument Managementオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `FormsServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。
   * Create an `OutputClient` object by using its constructor and passing the `ServiceClientFactory` object.
   * コンストラクタを使用して `DocumentManagementServiceClientImpl` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. Formsサービスを使用したフォームデータの取得

   * オブジェクト `FormsServiceClient` のメソッドを `processFormSubmission` 呼び出し、次の値を渡します。

      * フォーム `com.adobe.idp.Document` データを含むオブジェクトです。
      * すべての関連するHTTPヘッダーを含む環境変数を指定するstring値。 環境変数に1つ以上の値を指定して、処理するコンテンツタイプを `CONTENT_TYPE` 指定します。 例えば、XMLデータを処理するには、このパラメーターに次の文字列値を指定します。 `CONTENT_TYPE=text/xml`.
      * ヘッダー値を指定す `HTTP_USER_AGENT` るstring値(例： `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`)。
      * 実行時 `RenderOptionsSpec` のオプションを格納するオブジェクトです。
      このメ `processFormSubmission` ソッドは、フォー `FormsResult` ム送信の結果を含むオブジェクトを返します。

   * オブジェクトのメソッドを呼び出して、Formsサービスがフォームデータの処理を完了し `FormsResult` たかどうかを確認 `getAction` します。 このメソッドが値を返す場 `0`合、データは処理可能です。
   * オブジェクトのメソッドを呼び出して、オ `com.adobe.idp.Document` ブジェクトを作成し、フォ `FormsResult` ームデータを取得 `getOutputContent` します。 （このオブジェクトには、Outputサービスに送信できるフォームデータが含まれています）。
   * コンストラクターを `java.io.InputStream` 呼び出し、オブジェクトを `java.io.DataInputStream` 渡すことで、オブジェクトを作成 `com.adobe.idp.Document` します。
   * スタティックオ `org.w3c.dom.DocumentBuilderFactory` ブジェクトのメソッドを呼び出して、オ `org.w3c.dom.DocumentBuilderFactory` ブジェクトを作成 `newInstance` します。
   * オブジェクトの `org.w3c.dom.DocumentBuilder` メソッドを呼び出して、オ `org.w3c.dom.DocumentBuilderFactory` ブジェクトを作成 `newDocumentBuilder` します。
   * Create an `org.w3c.dom.Document` object by invoking the `org.w3c.dom.DocumentBuilder` object’s `parse` method and passing the `java.io.InputStream` object.
   * XMLドキュメント内の各ノードの値を取得します。 このタスクを実行する1つの方法は、2つのパラメーターを受け入れるカスタムメソッドを作成することです。オブ `org.w3c.dom.Document` ジェクトと、値を取得するノードの名前。 このメソッドは、ノードの値を表すstring値を返します。 このプロセスの後のコード例では、このカスタムメソッドが呼び出されま `getNodeText`す。 このメソッドの本体が表示されます。


1. Outputサービスを使用して、非インタラクティブPDFドキュメントを作成します。

   Create a PDF document by invoking the `OutputClient` object’s `generatePDFOutput` method and passing the following values:

   * 列 `TransformationFormat` 挙値。 PDFドキュメントを生成するには、を指定しま `TransformationFormat.PDF`す。
   * フォームデザイン名を指定する string 値。フォームデザインが、Formsサービスから取得したフォームデータと互換性があることを確認します。
   * フォームデザインが存在するコンテンツルートを指定するstring値。
   * PDF実行 `PDFOutputOptionsSpec` 時オプションを含むオブジェクトです。
   * レンダリ `RenderOptionsSpec` ングの実行時オプションを含むオブジェクトです。
   * フォー `com.adobe.idp.Document` ムデザインとマージするデータを含むXMLデータソースを含むオブジェクトです。 このオブジェクトがオブジェクトのメソッドによって返され `FormsResult` たことを確認して `getOutputContent` ください。
   * The `generatePDFOutput` method returns an `OutputResult` object that contains the results of the operation.
   * オブジェクトのメソッドを呼び出して、非インタラクティブPDF `OutputResult` ドキュメントを取得 `getGeneratedDoc` します。 このメソッドは、非イン `com.adobe.idp.Document` タラクティブPDFドキュメントを表すインスタンスを返します。

1. Document Managementサービスを使用してPDFフォームをContent Services（非推奨）に保存する

   オブジェクトのメソッドを呼び出し、次 `DocumentManagementServiceClientImpl` の値を渡 `storeContent` して、コンテンツを追加します。

   * コンテンツが追加されるストアを指定するstring値。 The default store is `SpacesStore`. この値は必須パラメーターです。
   * コンテンツを追加するスペースの完全修飾パスを指定するstring値(例 `/Company Home/Test Directory`:)。 この値は必須パラメーターです。
   * 新しいコンテンツを表すノード名(例： `MortgageForm.pdf`)。 この値は必須パラメーターです。
   * ノードタイプを指定するstring値。 PDFファイルなどの新しいコンテンツを追加するには、を指定しま `{https://www.alfresco.org/model/content/1.0}content`す。 この値は必須パラメーターです。
   * コンテンツ `com.adobe.idp.Document` を表すオブジェクトです。 この値は必須パラメーターです。
   * エンコード値(例えば、 `UTF-8`)を指定するstring値。 この値は必須パラメーターです。
   * バージ `UpdateVersionType` ョン情報の処理方法を指定する列挙値(例えば、コンテンツバージョン `UpdateVersionType.INCREMENT_MAJOR_VERSION` を増分する場合)。 )この値は必須パラメータです。
   * コンテ `java.util.List` ンツに関連するアスペクトを指定するインスタンス。 この値はオプションのパラメーターで、指定できま `null`す。
   * コンテンツ `java.util.Map` 属性を格納するオブジェクトです。
   このメソ `storeContent` ッドは、内容を表 `CRCResult` すオブジェクトを返します。 オブジェクト `CRCResult` を使用して、例えば、コンテンツの一意の識別子の値を取得することができます。 このタスクを実行するには、オブジェクトの `CRCResult` メソッドを呼び出 `getNodeUuid` します。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
