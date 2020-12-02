---
title: 送信されたXMLデータを使用したPDFドキュメントの作成
seo-title: 送信されたXMLデータを使用したPDFドキュメントの作成
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
workflow-type: tm+mt
source-wordcount: '1279'
ht-degree: 5%

---


# 送信されたXMLデータを使用したPDFドキュメントの作成{#creating-pdf-documents-with-submittedxml-data}

## 送信されたXMLデータを使用したPDFドキュメントの作成{#creating-pdf-documents-with-submitted-xml-data}

ユーザーがインタラクティブフォームに入力できるWebベースのアプリケーションでは、データをサーバーに送信し直す必要があります。 Formsサービスを使用すると、ユーザーがインタラクティブフォームに入力したフォームデータを取得できます。 次に、フォームデータを別のAEM Formsサービス操作に渡し、そのデータを使用してPDFドキュメントを作成できます。

>[!NOTE]
>
>この内容を読む前に、送信済みフォームの処理に関する十分な理解を得ることをお勧めします。 フォームデザインと送信されたXMLデータの関係などの概念については、「送信されたFormsの処理」を参照してください。

3つのAEM Formsサービスを含む次のワークフローについて考えてみましょう。

* ユーザーは、XMLデータをWebベースのアプリケーションからFormsサービスに送信します。
* Formsサービスは、送信されたフォームの処理とフォームフィールドの抽出に使用されます。 フォームデータを処理できます。 例えば、データをエンタープライズデータベースに送信できます。
* フォームデータは、非インタラクティブPDFドキュメントを作成するためにOutputサービスに送信されます。
* 非インタラクティブPDFドキュメントは、Content Services（非推奨）に保存されます。

次の図に、このワークフローを視覚的に示します。

![cd_cd_finsrv_architecture_xml_pdf1](assets/cd_cd_finsrv_architecture_xml_pdf1.png)

ユーザーがクライアントWebブラウザーからフォームを送信した後、非インタラクティブPDFドキュメントがContent Services（非推奨）に保存されます。 次の図に、Content Services（非推奨）に保存されているPDFドキュメントを示します。

![cd_cd_cs_gui](assets/cd_cd_cs_gui.png)

### 手順{#summary-of-steps}の概要

送信されたXMLデータを含む非インタラクティブPDFドキュメントを作成し、Content Services（非推奨）のPDFドキュメントに保存するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Forms、出力、ドキュメント管理の各オブジェクトを作成します。
1. Formsサービスを使用してフォームデータを取得します。
1. Outputサービスを使用して、非インタラクティブPDFドキュメントを作成します。
1. ドキュメント管理サービスを使用して、PDFフォームをContent Services（非推奨）に格納します。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めてください。

**Forms、出力、ドキュメント管理の各オブジェクトの作成**

プログラムでFormsサービスAPI操作を実行する前に、FormsクライアントAPIオブジェクトを作成します。 同様に、このワークフローはOutputおよびドキュメント管理サービスを呼び出すので、Output Client APIオブジェクトとドキュメント管理クライアントAPIオブジェクトの両方を作成します。

**Formsサービスを使用したフォームデータの取得**

Formsサービスに送信されたフォームデータを取得します。 送信されたデータを処理して、ビジネス要件に合わせることができます。 例えば、フォームデータをエンタープライズデータベースに格納できます。 ただし、非インタラクティブPDFドキュメントを作成する場合は、フォームデータがOutputサービスに渡されます。

**Outputサービスを使用して、非インタラクティブPDFドキュメントを作成します。**

Outputサービスを使用して、フォームデザインとXMLフォームデータに基づく非インタラクティブPDFドキュメントを作成します。 ワークフローでは、フォームデータがFormsサービスから取得されます。

**ドキュメント管理サービスを使用して、PDFフォームをContent Services（非推奨）に格納する**

Content Services（非推奨）にPDFドキュメントを格納するには、ドキュメント管理サービスAPIを使用します。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[FormsサービスAPIクイック開始](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

### Java API {#create-a-pdf-document-with-submitted-xml-data-using-the-java-api}を使用して、送信されたXMLデータを使用してPDFドキュメントを作成します。

Forms、出力、ドキュメント管理API(Java)を使用して、送信されたXMLデータを使用してPDFドキュメントを作成します。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-forms-client.jar、adobe-output-client.jar、adobe-contentservices-client.jarなどのクライアントJARファイルを含めます。

1. Forms、出力、ドキュメント管理の各オブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクタを使用して `FormsServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用し、`OutputClient`オブジェクトを渡して、`ServiceClientFactory`オブジェクトを作成します。
   * コンストラクタを使用して `DocumentManagementServiceClientImpl` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。

1. Formsサービスを使用したフォームデータの取得

   * `FormsServiceClient`オブジェクトの`processFormSubmission`メソッドを呼び出し、次の値を渡します。

      * フォームデータを含む`com.adobe.idp.Document`オブジェクト。
      * 関連するすべてのHTTPヘッダーを含む環境変数を指定するstring値。 環境変数`CONTENT_TYPE`に1つ以上の値を指定して、処理するコンテンツタイプを指定します。 例えば、XMLデータを処理するには、このパラメーターに次の文字列値を指定します。`CONTENT_TYPE=text/xml`.
      * `HTTP_USER_AGENT`ヘッダー値を指定するstring値（`Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`など）。
      * 実行時オプションを格納する`RenderOptionsSpec`オブジェクト。

      `processFormSubmission`メソッドは、フォーム送信の結果を含む`FormsResult`オブジェクトを返します。

   * `FormsResult`オブジェクトの`getAction`メソッドを呼び出して、Formsサービスがフォームデータの処理を完了したかどうかを判断します。 このメソッドが値`0`を返す場合、データは処理の準備ができています。
   * `FormsResult`オブジェクトの`getOutputContent`メソッドを呼び出して`com.adobe.idp.Document`オブジェクトを作成し、フォームデータを取得します。 （このオブジェクトには、Outputサービスに送信できるフォームデータが含まれます）。
   * `java.io.DataInputStream`コンストラクターを呼び出し、`com.adobe.idp.Document`オブジェクトを渡して、`java.io.InputStream`オブジェクトを作成します。
   * 静的`org.w3c.dom.DocumentBuilderFactory`オブジェクトの`newInstance`メソッドを呼び出して、`org.w3c.dom.DocumentBuilderFactory`オブジェクトを作成します。
   * `org.w3c.dom.DocumentBuilderFactory`オブジェクトの`newDocumentBuilder`メソッドを呼び出して、`org.w3c.dom.DocumentBuilder`オブジェクトを作成します。
   * `org.w3c.dom.DocumentBuilder`オブジェクトの`parse`メソッドを呼び出し、`java.io.InputStream`オブジェクトを渡して、`org.w3c.dom.Document`オブジェクトを作成します。
   * XMLドキュメント内の各ノードの値を取得します。 このタスクを実行する1つの方法は、2つのパラメーターを受け取るカスタムメソッドを作成することです。`org.w3c.dom.Document`オブジェクトと、値を取得するノードの名前。 このメソッドは、ノードの値を表すstring値を返します。 このプロセスの後のコード例では、このカスタムメソッドは`getNodeText`と呼ばれます。 このメソッドの本文が表示されます。


1. Outputサービスを使用して、非インタラクティブPDFドキュメントを作成します。

   `OutputClient`オブジェクトの`generatePDFOutput`メソッドを呼び出し、次の値を渡してPDFドキュメントを作成します。

   * `TransformationFormat`列挙値。 PDFドキュメントを生成するには、`TransformationFormat.PDF`を指定します。
   * フォームデザイン名を指定する string 値。フォームデザインが、Formsサービスから取得したフォームデータと互換性があることを確認します。
   * フォームデザインが配置されているコンテンツルートを指定するstring値。
   * PDFランタイムオプションを含む`PDFOutputOptionsSpec`オブジェクト。
   * レンダリングの実行時オプションを含む`RenderOptionsSpec`オブジェクト。
   * フォームデザインとマージするデータを含むXMLデータソースが含まれる`com.adobe.idp.Document`オブジェクトです。 このオブジェクトが`FormsResult`オブジェクトの`getOutputContent`メソッドによって返されたことを確認します。
   * `generatePDFOutput`メソッドは、操作の結果を含む`OutputResult`オブジェクトを返します。
   * `OutputResult`オブジェクトの`getGeneratedDoc`メソッドを呼び出して、非インタラクティブPDFドキュメントを取得します。 このメソッドは、非インタラクティブPDFドキュメントを表す`com.adobe.idp.Document`インスタンスを返します。

1. ドキュメント管理サービスを使用したContent Services（非推奨）へのPDFフォームの保存

   `DocumentManagementServiceClientImpl`追加オブジェクトの`storeContent`メソッドを呼び出し、次の値を渡すことで、内容を指定します。

   * コンテンツが追加されるストアを指定するstring値です。 デフォルトのストアは`SpacesStore`です。 この値は必須のパラメータです。
   * コンテンツが追加されるスペースの完全修飾パスを指定するstring値（例：`/Company Home/Test Directory`）。 この値は必須のパラメータです。
   * 新しいコンテンツを表すノード名（例：`MortgageForm.pdf`）。 この値は必須のパラメータです。
   * ノードタイプを指定するstring値。 PDFファイルなど、新しいコンテンツを追加するには、`{https://www.alfresco.org/model/content/1.0}content`を指定します。 この値は必須のパラメータです。
   * コンテンツを表す`com.adobe.idp.Document`オブジェクト。 この値は必須のパラメータです。
   * エンコード値を指定するstring値（例：`UTF-8`）。 この値は必須のパラメータです。
   * バージョン情報の処理方法を指定する`UpdateVersionType`定義済みリスト値（例えば、`UpdateVersionType.INCREMENT_MAJOR_VERSION`でコンテンツバージョンを増やします）。 )この値は必須パラメータです。
   * コンテンツに関連する要素を指定する`java.util.List`インスタンス。 この値はオプションのパラメーターで、`null`を指定できます。
   * コンテンツ属性を格納する`java.util.Map`オブジェクト。

   `storeContent`メソッドは、内容を記述する`CRCResult`オブジェクトを返します。 `CRCResult`オブジェクトを使用して、例えば、コンテンツの固有な識別子の値を取得できます。 このタスクを実行するには、`CRCResult`オブジェクトの`getNodeUuid`メソッドを呼び出します。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
