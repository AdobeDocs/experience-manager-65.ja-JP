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

---


# Formsサービスのパフォーマンスの最適化 {#optimizing-the-performance-of-theforms-service}

## Formsサービスのパフォーマンスの最適化 {#optimizing-the-performance-of-the-forms-service}

フォームのレンダリング時に、Formsサービスのパフォーマンスを最適化する実行時のオプションを設定できます。 Formsサービスのパフォーマンスを向上させるために実行できる別のタスクは、XDPファイルをリポジトリに保存することです。 ただし、この作業の実行方法については説明しません。 (See [Invoking a service using a Java client library](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library).)

>[!NOTE]
>
>For more information about the Forms service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary-of-steps}

フォームのレンダリング中にFormsサービスのパフォーマンスを最適化するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. フォームクライアントAPIオブジェクトを作成します。
1. パフォーマンスの実行時オプションを設定します。
1. フォームをレンダリングします。
1. クライアントのWebブラウザーにフォームデータストリームを書き込みます。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

**フォームクライアントAPIオブジェクトの作成**

プログラムでFormsサービスのClient API操作を実行する前に、Formsサービスクライアントを作成する必要があります。 Java APIを使用している場合は、オブジェクトを作成し `FormsServiceClient` ます。 Forms webサービスAPIを使用している場合は、オブジェクトを作成し `FormsService` ます。

**パフォーマンスの実行時オプションの設定**

次のパフォーマンスランタイムオプションを設定して、Formsサービスのパフォーマンスを向上させることができます。

* **フォームのキャッシュ**:PDFとしてレンダリングされるフォームをサーバーキャッシュにキャッシュできます。 各フォームは、初回生成後にキャッシュされます。それ以降のレンダリング時には、キャッシュされているフォームがフォームデザインのタイムスタンプよりも新しい場合、フォームはキャッシュから取得されます。フォームをキャッシュすると、リポジトリからフォームデザインを取得する必要がないので、Formsサービスのパフォーマンスが向上します。
* フォームガイド（非推奨）のレンダリングには、他の変換タイプよりも時間がかかる場合があります。 パフォーマンスを向上させるために、フォームガイド（非推奨）をキャッシュすることをお勧めします。
* **スタンドアロンオプション**:Formsサービスでサーバー側の計算を実行する必要がない場合は、「スタンドアロン」オプションをに設定すると、状態情報なし `true`でフォームがレンダリングされます。 状態情報は、インタラクティブフォームをエンドユーザーに対してレンダリングし、そのユーザーがフォームに情報を入力して、フォームをFormsサービスに送り返す場合に必要です。 次に、Forms サービスは計算処理を実行し、フォームをレンダリングしてユーザーに戻し、結果がフォームに表示されます。状態情報のないフォームがFormsサービスに送り返されると、XMLデータのみが使用可能になり、サーバー側の計算は実行されません。
* **Linearized PDF**:線形化されたPDFファイルは、ネットワーク環境での効率的な増分アクセスを可能にするように編成されます。 このPDFファイルは、すべての点で有効なPDFで、既存のすべてのビューアおよび他のPDFアプリケーションと互換性があります。 つまり、線形化されたPDFは、ダウンロード中に表示できます。
* PDFフォームがクライアント上でレンダリングされる場合、このオプションを選択してもパフォーマンスは向上しません。
* **GuideRSLオプション**:実行時の共有ライブラリを使用するフォームガイド（非推奨）の生成を有効にします。 つまり、最初の要求では、より小さいSWFファイルと、ブラウザーのキャッシュに格納されるより大きな共有ライブラリがダウンロードされます。 詳しくは、FlexドキュメントのRSLを参照してください。
* また、クライアントでフォームをレンダリングすることで、Formsサービスのパフォーマンスを向上させることもできます。 (「クライアント [でのフォームのレンダリング](/help/forms/developing/rendering-forms-client.md)」を参照)。

**フォームのレンダリング**

パフォーマンスオプションを設定した後にフォームをレンダリングするには、パフォーマンスオプションを設定せずにフォームをレンダリングするのと同じアプリケーションロジックを使用します。

**クライアントのWebブラウザーにフォームデータストリームを書き込みます**

Formsサービスは、フォームをレンダリングした後、クライアントのWebブラウザーに書き込む必要があるフォームデータストリームを返します。 クライアントのWebブラウザーに書き込むと、フォームがユーザーに表示されます。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[FormsサービスAPIのクイックスタート](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[インタラクティブPDFフォームのレンダリング](/help/forms/developing/rendering-interactive-pdf-forms.md)

[HTMLとしてのフォームのレンダリング](/help/forms/developing/rendering-forms-html.md)

[フォームをレンダリングするWebアプリケーションの作成](/help/forms/developing/creating-web-applications-renders-forms.md)

### Java APIを使用したパフォーマンスの最適化 {#optimize-the-performance-using-the-java-api}

Forms API(Java)を使用して、最適なパフォーマンスでフォームをレンダリングします。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-forms-client.jarなどのクライアントJARファイルを含めます。

1. フォームクライアントAPIオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `FormsServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. パフォーマンスの実行時オプションの設定

   * コンストラクタを使用して `PDFFormRenderSpec` オブジェクトを作成します。
   * オブジェクトのメソッドを呼び出して渡すことで、フ `PDFFormRenderSpec` ォームキャッシュオプ `setCacheEnabled` ションを設定しま `true`す。
   * オブジェクトのメソッドを呼び出して渡すこ `PDFFormRenderSpec` とで、線形化オ `setLinearizedPDF` プションを設定 `true.`

1. フォームのレンダリング

   オブジェクト `FormsServiceClient` のメソッドを `renderPDFForm` 呼び出し、次の値を渡します。

   * ファイル名の拡張子を含むフォームデザイン名を指定するstring値。
   * フォーム `com.adobe.idp.Document` とマージするデータを含むオブジェクトです。 データをマージしない場合は、空のオブジェクトを渡し `com.adobe.idp.Document` ます。
   * パフォーマン `PDFFormRenderSpec` スを向上させるための実行時オプションを格納するオブジェクトです。
   * Formsサ `URLSpec` ービスに必要なURI値を含むオブジェクトです。
   * 添付フ `java.util.HashMap` ァイルを格納するオブジェクト。 これはオプションのパラメーターで、フォームにフ `null` ァイルを添付しないかどうかを指定できます。
   このメソ `renderPDFForm` ッドは、クライア `FormsResult` ントのWebブラウザーに書き込む必要があるフォームデータストリームを含むオブジェクトを返します。

1. クライアントのWebブラウザーにフォームデータストリームを書き込みます

   * フォームデー `javax.servlet.ServletOutputStream` タストリームをクライアントWebブラウザーに送信するために使用するオブジェクトを作成します。
   * オブジェクトの `com.adobe.idp.Document` メソッドを呼び出して、オ `FormsResult` ブジェクトを作成 `getOutputContent` します。
   * オブジェクト `java.io.InputStream` のメソッドを呼び出して、オ `com.adobe.idp.Document` ブジェクトを作成 `getInputStream` します。
   * バイト配列を作成し、オブジェクトのメソッドを呼び出し、バイト配列を引 `InputStream` 数として渡すこ `read`とで、フォームデータストリームを設定します。
   * オブジェクト `javax.servlet.ServletOutputStream` のメソッドを呼び `write` 出して、フォームデータストリームをクライアントWebブラウザーに送信します。 バイト配列をメソッドに渡し `write` ます。

**関連トピック**

[クイックスタート（SOAPモード）:Java APIを使用したパフォーマンスの最適化](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-optimizing-performance-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用したパフォーマンスの最適化 {#optimize-the-performance-using-the-web-service-api}

Forms API（Webサービス）を使用して、最適なパフォーマンスでフォームをレンダリングします。

1. プロジェクトファイルを含める

   * FormsサービスWSDLを使用するJavaプロキシクラスを作成します。
   * クラスパスにJavaプロキシクラスを含めます。

1. フォームクライアントAPIオブジェクトの作成

   オブジェクト `FormsService` を作成し、認証値を設定します。

1. パフォーマンスの実行時オプションの設定

   * コンストラクタを使用して `PDFFormRenderSpec` オブジェクトを作成します。
   * オブジェクトのメソッドを呼び出し、trueを渡して、 `PDFFormRenderSpec` フォームキャッシュ `setCacheEnabled` オプションを設定します。
   * オブジェクトのメソッドを呼び出し、true `PDFFormRenderSpec` を渡して、スタンドア `setStandAlone` ロンオプションを設定します。
   * オブジェクトのメソッドを呼び出し、true `PDFFormRenderSpec` を渡して線形 `setLinearizedPDF` 化オプションを設定します。

1. フォームのレンダリング

   オブジェクト `FormsService` のメソッドを `renderPDFForm` 呼び出し、次の値を渡します。

   * ファイル名の拡張子を含むフォームデザイン名を指定するstring値。
   * フォーム `BLOB` とマージするデータを含むオブジェクトです。 データを結合しない場合は、を渡します `null`。
   * 実行時 `PDFFormRenderSpecc` のオプションを格納するオブジェクトです。
   * Formsサ `URLSpec` ービスに必要なURI値を含むオブジェクトです。
   * 添付フ `java.util.HashMap` ァイルを格納するオブジェクト。 これはオプションのパラメーターで、フォームにフ `null` ァイルを添付しないかどうかを指定できます。
   * メソッドに `com.adobe.idp.services.holders.BLOBHolder` よって入力される空のオブジェクトです。 これは、レンダリングされたPDFフォームを保存するために使用します。
   * メソッドに `javax.xml.rpc.holders.LongHolder` よって入力される空のオブジェクトです。 （この引数には、フォーム内のページ数が格納されます）。
   * メソッドに `javax.xml.rpc.holders.StringHolder` よって入力される空のオブジェクトです。 （この引数はロケールの値を格納します）。
   * この操作 `com.adobe.idp.services.holders.FormsResultHolder` の結果を含む空のオブジェクトです。
   メソッド `renderPDFForm` は、最後の引 `com.adobe.idp.services.holders.FormsResultHolder` 数値として渡されたオブジェクトに、クライアントWebブラウザーに書き込む必要があるフォームデータストリームを入力します。

1. クライアントのWebブラウザーにフォームデータストリームを書き込みます

   * オブジェクト `FormResult` のデータメンバーの値を取得して、オ `com.adobe.idp.services.holders.FormsResultHolder` ブジェクトを `value` 作成します。
   * フォームデー `javax.servlet.ServletOutputStream` タストリームをクライアントWebブラウザーに送信するために使用するオブジェクトを作成します。
   * オブジェクトの `BLOB` メソッドを呼び出して、フォームデータを含むオ `FormsResult` ブジェクトを作成 `getOutputContent` します。
   * バイト配列を作成し、オブジェクトのメソッドを呼び出 `BLOB` して値を設定 `getBinaryData` します。 このタスクは、オブジェクトの内容をバ `FormsResult` イト配列に割り当てます。
   * オブジェクト `javax.servlet.http.HttpServletResponse` のメソッドを呼び `write` 出して、フォームデータストリームをクライアントWebブラウザーに送信します。 バイト配列をメソッドに渡し `write` ます。

**関連トピック**

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
