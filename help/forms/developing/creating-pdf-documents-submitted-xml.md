---
title: 送信された XML データを使用した PDF ドキュメントの作成
seo-title: Creating PDF Documents with SubmittedXML Data
description: Forms サービスを使用して、ユーザーがインタラクティブフォームに入力したフォームデータを取得します。フォームデータを別の AEM Forms サービス操作に渡し、そのデータを使用して PDF ドキュメントを作成します。
seo-description: Use the Forms service to retrieve the form data that the user entered into an interactive form. Pass the form data to another AEM Forms service operation and create a PDF document using the data.
uuid: 2676c614-8988-451b-ac7c-bd07731a3f5f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 62490230-a24e-419d-95bb-c0bb04a03f96
role: Developer
exl-id: d9d5b94a-9d10-4d90-9e10-5142f30ba4a3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '1320'
ht-degree: 100%

---

# 送信された XML データを使用した PDF ドキュメントの作成 {#creating-pdf-documents-with-submittedxml-data}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

## 送信された XML データを使用した PDF ドキュメントの作成 {#creating-pdf-documents-with-submitted-xml-data}

ユーザーがインタラクティブなフォームに入力できる web ベ ースのアプリケーションでは、データをサーバーに送信する必要があります。Forms サービスを使用すると、ユーザーがインタラクティブフォームに入力したフォームデータを取得できます。フォームデータを別の AEM Forms サービス操作に渡し、そのデータを使用して PDF ドキュメントを作成できます。

>[!NOTE]
>
>このコンテンツを読む前に、送信されたフォームの処理について十分に理解しておくことをお勧めします。フォームデザインと送信された XML データの関係などの概念については、「送信された Forms の処理」で説明しています。

3 つの AEM Forms サービスを含む次のワークフローについて考えてみます。

* ユーザーが、web ベースのアプリケーションから Forms サービスに XML データを送信します。
* Forms サービスは、送信されたフォームを処理し、フォームフィールドを抽出するために使用します。フォームデータは処理できます。たとえば、データをエンタープライズデータベースに送信できます。
* フォームデータは Output サービスに送信され、非インタラクティブ型の PDF ドキュメントが作成されます。
* 非インタラクティブ型の PDF ドキュメントが Content サービス（非推奨） に保存されます。

次の図は、このワークフローを視覚的に表したものです。

![cd_cd_finsrv_architecture_xml_pdf1](assets/cd_cd_finsrv_architecture_xml_pdf1.png)

ユーザーがクライアントの web ブラウザーからフォームを送信すると、非インタラクティブ型の PDF ドキュメントが Content サービス（非推奨）に保存されます。次の図は、Content サービス（非推奨）に保存されている PDF ドキュメントを示しています。

![cd_cd_cs_gui](assets/cd_cd_cs_gui.png)

### 手順の概要 {#summary-of-steps}

送信された XML データを使用して非インタラクティブ型の PDF ドキュメントを作成し、Content サービス（非推奨）で PDF ドキュメントに保存するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Forms、Output、Document Management のオブジェクトを作成します。
1. Forms サービスを使用してフォームデータを取得します。
1. Output サービスを使用して、非インタラクティブ型の PDF ドキュメントを作成します。
1. ドキュメント管理サービスを使用して、PDF フォームを Content サービス（非推奨）に保存します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**Forms、Output、Document Management のオブジェクトを作成する**

プログラムで Forms Service API 操作を実行する前に、Forms Client API オブジェクトを作成します。同様に、このワークフローは Output サービスと Document Management サービスを呼び出すため、Output クライアント API オブジェクトと Document Management クライアント API オブジェクトの両方を作成します。

**Forms サービスを使用してフォームデータを取得する**

Forms サービスに送信されたフォームデータを取得します。ビジネス要件を満たすように、送信されたデータを処理できます。例えば、フォームデータをエンタープライズデータベースに格納できます。ただし、非インタラクティブ型の PDF ドキュメントを作成するために、フォームデータを Output サービスに渡します。

**Output サービスを使用して、非インタラクティブ型の PDF ドキュメントを作成します。**

Output サービスを使用して、フォームデザインと XML フォームデータに基づく非インタラクティブ型 PDF ドキュメントを作成します。ワークフローでは、フォームデータは Forms サービスから取得されます。

**Document Management サービスを使用して、PDF フォームを Content サービス（非推奨）に格納する**

Document Management サービス API を使用して、PDF ドキュメントを Content サービス（非推奨）に格納します。

**関連項目**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms サービス API のクイックスタート](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

### Java API を使用して、送信された XML データを使用した PDF ドキュメントを作成する {#create-a-pdf-document-with-submitted-xml-data-using-the-java-api}

Forms、Output、Document Management API（Java）を使用して、送信された XML データを使用した PDF ドキュメントを作成します。

1. プロジェクトファイルを含める

   Java プロジェクトのクラスパスに、adobe-forms-client.jar、adobe-output-client.jar、adobe-contentservices-client.jar などのクライアント JAR ファイルを含めます。

1. Forms、Output、Document Management オブジェクトを作成する

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して `ServiceClientFactory` オブジェクトを渡すことにより、`FormsServiceClient` オブジェクトを作成します。
   * コンストラクターを使用して `ServiceClientFactory` オブジェクトを渡すことにより、`OutputClient` オブジェクトを作成します。
   * `DocumentManagementServiceClientImpl` オブジェクトを作成するには、コンストラクターを使用して、`ServiceClientFactory` オブジェクトを渡します。

1. Forms サービスを使用したフォームデータの取得

   * `FormsServiceClient` オブジェクトの `processFormSubmission` メソッドを呼び出して、次の値を渡します。

      * フォームデータを含む `com.adobe.idp.Document` オブジェクト。
      * 関連するすべての HTTP ヘッダーを含む、環境変数を指定する文字列値。`CONTENT_TYPE` 環境変数に 1 つ以上の値を指定して、処理するコンテンツタイプを指定します。例えば、XML データを処理するには、このパラメーター `CONTENT_TYPE=text/xml` に次の文字列値を指定します。
      * `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)` などの `HTTP_USER_AGENT` ヘッダー値を指定する文字列値。
      * 実行時オプションを格納する `RenderOptionsSpec` オブジェクト。

      `processFormSubmission` メソッドは、フォーム送信の結果を含む `FormsResult` オブジェクトを返します。

   * Forms サービスがフォームデータの処理を終了したかどうかを確認するには、`FormsResult` オブジェクトの `getAction` メソッドを呼び出します。このメソッドが値 `0` を返した場合、処理するデータの準備が整っています。
   * フォームデータを取得するには、`FormsResult` オブジェクトの `getOutputContent` メソッドを呼び出して、`com.adobe.idp.Document` オブジェクトを作成します。（このオブジェクトには、Output サービスに送信できるフォームデータが含まれています。）
   * `java.io.InputStream` オブジェクトを作成するには、`java.io.DataInputStream` コントラクターを呼び出して、`com.adobe.idp.Document` オブジェクトを渡します。
   * 静的な `org.w3c.dom.DocumentBuilderFactory` オブジェクトの `newInstance` メソッドを呼び出して、`org.w3c.dom.DocumentBuilderFactory` オブジェクトを作成します。
   * `org.w3c.dom.DocumentBuilderFactory` オブジェクトの `newDocumentBuilder` メソッドを呼び出して、`org.w3c.dom.DocumentBuilder` オブジェクトを作成します。
   * `org.w3c.dom.Document` オブジェクトを作成するには、`org.w3c.dom.DocumentBuilder` オブジェクトの `parse` メソッドを呼び出して、`java.io.InputStream` オブジェクトを渡します。
   * XML ドキュメント内の各ノードの値を取得します。 このタスクを実行する 1 つの方法は、2 つのパラメーター（`org.w3c.dom.Document` オブジェクトと値を取得するノードの名前）を受け入れるカスタムメソッドを作成することです。このメソッドは、ノードの値を表す文字列値を返します。 このプロセスに続くコード例では、このカスタムメソッドは `getNodeText` と呼ばれます。このメソッドの本文を示します。


1. Output サービスを使用して、非インタラクティブ PDF ドキュメントを作成します。

   PDF ドキュメントを作成するには、`OutputClient` オブジェクトの `generatePDFOutput` メソッドを呼び出して、次の値を渡します。

   * `TransformationFormat` 列挙値。PDF ドキュメントを生成するには、`TransformationFormat.PDF` を指定します。
   * フォームデザイン名を指定する文字列値。フォームデザインが Forms サービスから取得したフォームデータと互換性があることを確認してください。
   * フォームデザインが配置されているコンテンツルートを指定する文字列の値です。
   * PDF 実行時オプションを含む `PDFOutputOptionsSpec` オブジェクト。
   * レンダリング実行時オプションを含む `RenderOptionsSpec` オブジェクト。
   * フォームデザインと結合するデータを含む XML データソースを含む `com.adobe.idp.Document` オブジェクト。`FormsResult` オブジェクトの `getOutputContent` メソッドによって、このオブジェクトが返されたことを確認してください。
   * `generatePDFOutput` メソッドは、操作の結果を含む `OutputResult` オブジェクトを返します。
   * `OutputResult` オブジェクトの `getGeneratedDoc` メソッドを呼び出して、非インタラクティブ PDF ドキュメントを取得します。このメソッドは、非インタラクティブ PDF ドキュメントを表す `com.adobe.idp.Document` インスタンスを返します。

1. Document Management サービスを使用した、PDF フォームのコンテンツサービスへの保存（非推奨）

   コンテンツを追加するには、`DocumentManagementServiceClientImpl` オブジェクトの `storeContent` メソッドを呼び出して、次の値を渡します。

   * コンテンツの追加先となるストアを指定する文字列値です。 デフォルトストアは `SpacesStore` です。この値は必須パラメーターです。
   * コンテンツが追加されるスペースの完全修飾パスを指定する文字列値（例えば、`/Company Home/Test Directory`）。この値は必須パラメーターです。
   * 新しいコンテンツを表すノード名（例えば、`MortgageForm.pdf`）。この値は必須パラメーターです。
   * ノードタイプを指定する文字列値です。PDF ファイルなどの新しいコンテンツを追加するには、`{https://www.alfresco.org/model/content/1.0}content` を指定します。この値は必須パラメーターです。
   * コンテンツを表す `com.adobe.idp.Document` オブジェクト。この値は必須パラメーターです。
   * エンコーディング値を指定する文字列値（例えば、`UTF-8`）。この値は必須パラメーターです。
   * バージョン情報の処理方法を指定する `UpdateVersionType` 列挙値（例えば、コンテンツバージョンを増分するための `UpdateVersionType.INCREMENT_MAJOR_VERSION`。）この値は必須パラメーターです。
   * コンテンツに関連する側面を指定する `java.util.List` インスタンス。この値はオプションのパラメーターで、`null` を指定できます。
   * コンテンツ属性を格納する `java.util.Map` オブジェクト。

   `storeContent` メソッドは、コンテンツを説明する `CRCResult` オブジェクトを返します。`CRCResult` オブジェクトを使用すると、例えば、コンテンツの一意の識別子の値を取得できます。このタスクを実行するには、`CRCResult` オブジェクトの `getNodeUuid` メソッドを呼び出します。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
