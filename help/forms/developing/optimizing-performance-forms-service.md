---
title: Formsサービスのパフォーマンスの最適化
seo-title: Formsサービスのパフォーマンスの最適化
description: 'null'
seo-description: 'null'
uuid: 9040c09a-e5d0-432b-b1c5-ad46ab57c4fc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9f883483-b81e-42c6-a4a1-eb499dd112e7
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1403'
ht-degree: 7%

---


# Formsサービスのパフォーマンスの最適化 {#optimizing-the-performance-of-theforms-service}

## Formsサービスのパフォーマンスの最適化 {#optimizing-the-performance-of-the-forms-service}

フォームのレンダリング時に、Formsサービスのパフォーマンスを最適化する実行時オプションを設定できます。 Formsサービスのパフォーマンスを向上させるために実行できるもう1つのタスクは、XDPファイルをリポジトリに保存することです。 ただし、このタスクの実行方法は説明しません。 (See [Invoking a service using a Java client library](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library).)

>[!NOTE]
>
>For more information about the Forms service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary-of-steps}

フォームのレンダリング中にFormsサービスのパフォーマンスを最適化するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. FormsクライアントAPIオブジェクトを作成します。
1. パフォーマンスの実行時オプションを設定します。
1. フォームをレンダリングします。
1. フォームデータストリームをクライアントのWebブラウザーに書き込みます。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めてください。

**FormsクライアントAPIオブジェクトの作成**

プログラムでFormsサービスのクライアントAPI操作を実行する前に、Formsサービスクライアントを作成する必要があります。 Java APIを使用している場合は、 `FormsServiceClient` オブジェクトを作成します。 FormsWebサービスAPIを使用している場合は、 `FormsService` オブジェクトを作成します。

**パフォーマンスの実行時オプションの設定**

次のパフォーマンスランタイムオプションを設定して、Formsサービスのパフォーマンスを向上させることができます。

* **フォームキャッシング**:PDFとしてレンダリングされるフォームをサーバーキャッシュにキャッシュできます。 各フォームは、初回生成後にキャッシュされます。それ以降のレンダリング時には、キャッシュされているフォームがフォームデザインのタイムスタンプよりも新しい場合、フォームはキャッシュから取得されます。フォームをキャッシュすると、リポジトリからフォームデザインを取得する必要がなくなるので、Formsサービスのパフォーマンスが向上します。
* フォームガイド（非推奨）は、他の変換タイプよりもレンダリングに時間がかかる場合があります。 パフォーマンスを向上させるために、フォームガイド（非推奨）をキャッシュすることをお勧めします。
* **スタンドアロンオプション**:サーバー側の計算を実行するのにFormsサービスが必要ない場合は、スタンドアロンオプションをに設定すると、フォームが状態情報なしでレンダリングさ `true`れます。 状態情報は、インタラクティブフォームをレンダリングしてエンドユーザーがフォームに情報を入力し、そのフォームをFormsサービスに送り返す場合に必要です。 次に、Forms サービスは計算処理を実行し、フォームをレンダリングしてユーザーに戻し、結果がフォームに表示されます。状態情報のないフォームがFormsサービスに送り返されると、XMLデータのみが使用可能になり、サーバー側の計算は実行されません。
* **Linearized PDF**:線形化されたPDFファイルは、ネットワーク環境での効率的な増分アクセスを可能にするように編成されています。 このPDFファイルは、あらゆる点で有効なPDFであり、既存のすべてのビューアおよび他のPDFアプリケーションと互換性があります。 つまり、線形化されたPDFは、ダウンロード中に表示できます。
* PDFフォームがクライアント上でレンダリングされる場合、このオプションを選択してもパフォーマンスは向上しません。
* **GuideRSLオプション**:ランタイム共有ライブラリを使用して、フォームガイド（非推奨）の生成を有効にします。 つまり、最初の要求では、より小さなSWFファイルと、ブラウザーのキャッシュに格納されるより大きな共有ライブラリがダウンロードされます。 詳しくは、FlexのドキュメントのRSLを参照してください。
* また、クライアントでフォームをレンダリングすることで、Formsサービスのパフォーマンスを向上させることもできます。 (クライアントでの [Formsのレンダリングを参照](/help/forms/developing/rendering-forms-client.md))。

**フォームのレンダリング**

パフォーマンスオプションを設定した後にフォームをレンダリングするには、パフォーマンスオプションを設定せずにフォームをレンダリングするのと同じアプリケーションロジックを使用します。

**フォームデータストリームをクライアントのWebブラウザーに書き込みます**

Formsサービスはフォームをレンダリングした後、フォームデータストリームを返します。このデータストリームは、クライアントのWebブラウザーに書き込む必要があります。 クライアントのWebブラウザーに書き込まれると、フォームはユーザーに表示されます。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[FormsサービスAPIクイック開始](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[インタラクティブPDF formsのレンダリング](/help/forms/developing/rendering-interactive-pdf-forms.md)

[FormsをHTMLとしてレンダリング](/help/forms/developing/rendering-forms-html.md)

[FormsをレンダリングするWeb アプリケーションの作成](/help/forms/developing/creating-web-applications-renders-forms.md)

### Java APIを使用したパフォーマンスの最適化 {#optimize-the-performance-using-the-java-api}

FormsAPI(Java)を使用して、パフォーマンスを最適化したフォームをレンダリングします。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-forms-client.jarなどのクライアントJARファイルを含めます。

1. FormsクライアントAPIオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `FormsServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. パフォーマンスの実行時オプションの設定

   * コンストラクタを使用して `PDFFormRenderSpec` オブジェクトを作成します。
   * オブジェクトの `PDFFormRenderSpec` メソッドを呼び出して渡すことで、フォームキャッシュオプションを設定 `setCacheEnabled``true`します。
   * 線形化オプションを設定するには、 `PDFFormRenderSpec` オブジェクトの `setLinearizedPDF` メソッドを呼び出して、 `true.`

1. フォームのレンダリング

   オブジェクトの `FormsServiceClient``renderPDFForm` メソッドを呼び出し、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定するstring値。
   * フォームとマージするデータを含む `com.adobe.idp.Document` オブジェクト。 データをマージしない場合は、空の `com.adobe.idp.Document` オブジェクトを渡します。
   * パフォーマンスを向上させるための実行時オプションを格納する `PDFFormRenderSpec` オブジェクトです。
   * Formsサービスに必要なURI値を含む `URLSpec` オブジェクトです。
   * 添付ファイルを格納する `java.util.HashMap` オブジェクトです。 これはオプションのパラメーターで、フォームにファイルを添付しない `null` かどうかを指定できます。

   この `renderPDFForm``FormsResult` メソッドは、クライアントのWebブラウザーに書き込む必要があるフォームデータストリームを含むオブジェクトを返します。

1. フォームデータストリームをクライアントのWebブラウザーに書き込みます

   * フォームデータストリームをクライアントのWebブラウザーに送信するために使用する `javax.servlet.ServletOutputStream` オブジェクトを作成します。
   * オブジェクトの `com.adobe.idp.Document` メソッドを呼び出して、 `FormsResult` オブジェクトを作成し `getOutputContent` ます。
   * オブジェクトの `java.io.InputStream` メソッドを呼び出して、 `com.adobe.idp.Document` オブジェクトを作成 `getInputStream` します。
   * バイト配列を作成し、 `InputStream` オブジェクトの `read`メソッドを呼び出して、バイト配列を引数として渡すことで、フォームデータストリームを設定します。
   * オブジェクトの `javax.servlet.ServletOutputStream``write` メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに送信します。 バイト配列を `write` メソッドに渡します。

**関連トピック**

[クイック開始（SOAPモード）:Java APIを使用したパフォーマンスの最適化](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-optimizing-performance-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用してパフォーマンスを最適化する {#optimize-the-performance-using-the-web-service-api}

FormsAPI（Webサービス）を使用して、パフォーマンスを最適化したフォームをレンダリングします。

1. プロジェクトファイルを含める

   * FormsサービスのWSDLを使用するJavaプロキシクラスを作成します。
   * クラスパスにJavaプロキシクラスを含めます。

1. FormsクライアントAPIオブジェクトの作成

   オブジェクトを作成し、認証値を設定し `FormsService` ます。

1. パフォーマンスの実行時オプションの設定

   * コンストラクタを使用して `PDFFormRenderSpec` オブジェクトを作成します。
   * オブジェクトのメソッドを呼び出し、trueを渡して、フォ `PDFFormRenderSpec` ームキャッシュオプションを設定し `setCacheEnabled` ます。
   * オブジェクトのメソッドを呼び出し、trueを渡して、スタンドアロ `PDFFormRenderSpec` ンのオプションを設定し `setStandAlone` ます。
   * 線形化オプションを設定するには、 `PDFFormRenderSpec` オブジェクトの `setLinearizedPDF` メソッドを呼び出し、trueを渡します。

1. フォームのレンダリング

   オブジェクトの `FormsService``renderPDFForm` メソッドを呼び出し、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定するstring値。
   * フォームとマージするデータを含む `BLOB` オブジェクト。 データを結合したくない場合は、を渡し `null`ます。
   * 実行時オプションを格納する `PDFFormRenderSpecc` オブジェクト。
   * Formsサービスに必要なURI値を含む `URLSpec` オブジェクトです。
   * 添付ファイルを格納する `java.util.HashMap` オブジェクトです。 これはオプションのパラメーターで、フォームにファイルを添付しない `null` かどうかを指定できます。
   * メソッドによって入力される空の `com.adobe.idp.services.holders.BLOBHolder` オブジェクトです。 これは、レンダリングされたPDFフォームを保存するために使用します。
   * メソッドによって入力される空の `javax.xml.rpc.holders.LongHolder` オブジェクトです。 （この引数は、フォームのページ数を格納します）。
   * メソッドによって入力される空の `javax.xml.rpc.holders.StringHolder` オブジェクトです。 （この引数はロケールの値を格納します）。
   * この操作の結果を含む空の `com.adobe.idp.services.holders.FormsResultHolder` オブジェクトです。

   この `renderPDFForm` メソッドは、最後の引数値として渡される `com.adobe.idp.services.holders.FormsResultHolder` オブジェクトに、クライアントWebブラウザーに書き込む必要があるフォームデータストリームを入力します。

1. フォームデータストリームをクライアントのWebブラウザーに書き込みます

   * オブジェクトの `FormResult` データメンバーの値を取得して `com.adobe.idp.services.holders.FormsResultHolder` オブジェクトを作成し `value` ます。
   * フォームデータストリームをクライアントのWebブラウザーに送信するために使用する `javax.servlet.ServletOutputStream` オブジェクトを作成します。
   * オブジェクトの `BLOB` メソッドを呼び出して、フォームデータを含む `FormsResult` オブジェクトを作成し `getOutputContent` ます。
   * バイト配列を作成し、 `BLOB` オブジェクトの `getBinaryData` メソッドを呼び出して値を設定します。 このタスクは、 `FormsResult` オブジェクトの内容をバイト配列に割り当てます。
   * オブジェクトの `javax.servlet.http.HttpServletResponse``write` メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに送信します。 バイト配列を `write` メソッドに渡します。

**関連トピック**

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
