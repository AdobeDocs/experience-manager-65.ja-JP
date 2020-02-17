---
title: クライアントでのフォームのレンダリング
seo-title: クライアントでのフォームのレンダリング
description: 'null'
seo-description: 'null'
uuid: 09bcc23d-28b0-473a-87f1-bc17e87620f4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 08d36e9f-cafc-478e-9781-8fc29ac6262e
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# クライアントでのフォームのレンダリング {#rendering-forms-at-the-client}

## クライアントでのフォームのレンダリング {#rendering-forms-at-the-client-inner}

AcrobatまたはAdobe readerのクライアント側レンダリング機能を使用すると、PDFコンテンツの配信を最適化し、Formsサービスのネットワーク読み込み処理機能を向上できます。 このプロセスは、クライアントでのフォームのレンダリングと呼ばれます。 クライアントでフォームをレンダリングするには、クライアントデバイス（通常はWebブラウザー）でAcrobat 7.0またはAdobe Reader 7.0以降を使用する必要があります。

サーバーサイドのスクリプトの実行によって生じるフォームへの変更は、ルートサブフォームに設定された属性が含まれていない限り、クライアントでレンダリングされるフ `restoreState` ォームには反映されませ `auto`ん。 この属性について詳しくは、「 [Forms Designer」を参照してください。](https://www.adobe.com/go/learn_aemforms_designer_63)

>[!NOTE]
>
>For more information about the Forms service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary-of-steps}

クライアントでフォームをレンダリングするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. フォームクライアントAPIオブジェクトを作成します。
1. クライアントレンダリングの実行時オプションを設定します。
1. クライアントでフォームをレンダリングします。
1. クライアントのWebブラウザーにフォームを書き込みます。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

**フォームクライアントAPIオブジェクトの作成**

プログラムでFormsサービスのClient API操作を実行する前に、Formsサービスクライアントを作成する必要があります。 Java APIを使用している場合は、オブジェクトを作成し `FormsServiceClient` ます。 Forms webサービスAPIを使用している場合は、オブジェクトを作成し `FormsService` ます。

**クライアントレンダリングの実行時オプションの設定**

クライアントレンダリングの実行時オプションを設定し、実行時オプションをに設定して、クライアントでフォームをレンダリン `RenderAtClient` グする必要がありま `true`す。 これにより、フォームがレンダリングされるクライアントデバイスにフォームが配信されます。 が(デフ `RenderAtClient` ォルト値 `auto` の)場合、フォームデザインによって、フォームがクライアントでレンダリングされるかどうかが決まります。 フォームデザインは、編集可能なレイアウトを含むフォームデザインである必要があります。

オプションで設定できるランタイムオプションがあり `SeedPDF` ます。 このオ `SeedPDF` プションは、PDFコンテナ（シードPDFドキュメント）をフォームデザインとXMLデータと結合します。 フォームデザインとXMLデータの両方がAcrobatまたはAdobe Readerに配信され、フォームがレンダリングされます。 このオ `SeedPDF` プションは、クライアントコンピューターにフォームで使用されるフォントがない場合に使用できます。例えば、エンドユーザーが、フォームの所有者が使用のライセンスを受けているフォントを使用するライセンスを受けていない場合などです。

Designerを使用して、シードPDFファイルとして使用するシンプルなダイナミックPDFファイルを作成できます。 このタスクを実行するには、次の手順が必要です。

1. シードPDFファイル内にフォントを埋め込む必要があるかどうかを指定します。 シードPDFファイルには、レンダリングするフォームに必要な追加のフォントを含める必要があります。 シードPDFファイルにフォントを埋め込む場合は、フォントの使用許諾契約に違反していないことを確認してください。 Designerでは、フォントを法的に埋め込むことができるかどうかを指定できます。 保存時に、フォームに埋め込めないフォントが存在する場合は、埋め込めないフォントを示すメッセージがDesignerに表示されます。 このメッセージは、スタティックPDFドキュメントの場合はDesignerに表示されません。
1. DesignerでシードPDFファイルを作成する場合は、少なくともメッセージを含むテキストフィールドを追加することをお勧めします。 このメッセージは、Acrobat 7.0以降またはAdobe Reader 7.0以降を使用してドキュメントを表示する必要があることを伝える、Adobe Readerの以前のバージョンのユーザーを対象としています。
1. シードPDFファイルを、PDFファイル名拡張子が付いたダイナミックPDFファイルとして保存します。

>[!NOTE]
>
>クライアント上でフォームをレンダリングする場合は、シードPDFランタイムオプションを定義する必要はありません。 シードPDFを指定しない場合、FormsサービスはCOSオブジェクトを含まず、実際のXDPコンテンツが内部に埋め込まれたPDFラッパーを含むシェルPDFを作成します。 この節の手順では、シードPDFの実行時オプションを設定しません。 COSオブジェクトについて詳しくは、『Adobe PDF Reference』ガイドを参照してください。

**クライアントでのフォームのレンダリング**

クライアントでフォームをレンダリングするには、フォームをレンダリングするアプリケーションロジックにクライアントレンダリングの実行時オプションが含まれていることを確認する必要があります。

**クライアントのWebブラウザーにフォームデータストリームを書き込みます**

Formsサービスは、クライアントWebブラウザーに書き込む必要があるフォームデータストリームを作成します。 クライアントのWebブラウザーに書き込むと、フォームはAcrobat 7.0またはAdobe Reader 7.0以降でレンダリングされ、ユーザーに表示されます。

**関連トピック**

[Java APIを使用してクライアントでフォームをレンダリングする](#render-a-form-at-the-client-using-the-java-api)

[WebサービスAPIを使用してクライアントでフォームをレンダリングする](#render-a-form-at-the-client-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[FormsサービスAPIのクイックスタート](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Formsサービスへのドキュメントの引き渡し](/help/forms/developing/passing-documents-forms-service.md)

[フォームをレンダリングするWebアプリケーションの作成](/help/forms/developing/creating-web-applications-renders-forms.md)

### Java APIを使用してクライアントでフォームをレンダリングする {#render-a-form-at-the-client-using-the-java-api}

Forms API(Java)を使用して、クライアントでフォームをレンダリングします。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-forms-client.jarなどのクライアントJARファイルを含めます。

1. フォームクライアントAPIオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `FormsServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. クライアントレンダリングの実行時オプションの設定

   * コンストラクタを使用して `PDFFormRenderSpec` オブジェクトを作成します。
   * オブジェクト `RenderAtClient` のメソッドを呼び出し、列挙値を渡 `PDFFormRenderSpec` して、実行時 `setRenderAtClient` のオプションを設定しま `RenderAtClient.Yes`す。

1. クライアントでのフォームのレンダリング

   オブジェクト `FormsServiceClient` のメソッドを `renderPDFForm` 呼び出し、次の値を渡します。

   * ファイル名の拡張子を含むフォームデザイン名を指定するstring値。 AEM Formsアプリケーションの一部であるフォームデザインを参照する場合は、必ずなどの完全なパスを指定してくださ `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`い。
   * フォーム `com.adobe.idp.Document` とマージするデータを含むオブジェクトです。 データをマージしない場合は、空のオブジェクトを渡し `com.adobe.idp.Document` ます。
   * クライア `PDFFormRenderSpec` ントでフォームをレンダリングするために必要な実行時オプションを格納するオブジェクトです。
   * Formsサ `URLSpec` ービスがフォームをレンダリングするために必要なURI値を含むオブジェクトです。
   * 添付フ `java.util.HashMap` ァイルを格納するオブジェクト。 これはオプションのパラメーターで、フォームにフ `null` ァイルを添付しないかどうかを指定できます。
   このメソ `renderPDFForm` ッドは、クライア `FormsResult` ントのWebブラウザーに書き込む必要があるフォームデータストリームを含むオブジェクトを返します。

1. クライアントのWebブラウザーにフォームデータストリームを書き込みます

   * オブジェクトの `com.adobe.idp.Document` メソッドを呼び出して、オ `FormsResult` ブジェクトを作成 `getOutputContent` します。
   * メソッドを呼び出して、オブジェ `com.adobe.idp.Document` クトのコンテンツタイプを取得 `getContentType` します。
   * メソッドを呼 `javax.servlet.http.HttpServletResponse` び出し、オブジェクトのコンテンツタ `setContentType` イプを渡すことで、オブジェクトのコンテンツタイプを設定 `com.adobe.idp.Document` します。
   * オブジェクトの `javax.servlet.ServletOutputStream` メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに書き込むために使用する `javax.servlet.http.HttpServletResponse` オブジェクトを作 `getOutputStream` 成します。
   * オブジェクト `java.io.InputStream` のメソッドを呼び出して、オ `com.adobe.idp.Document` ブジェクトを作成 `getInputStream` します。
   * バイト配列を作成し、オブジェクトのメソッドを呼び出し、バイト配列を引数 `InputStream` として渡すこ `read` とで、フォームデータストリームを設定します。
   * オブジェクト `javax.servlet.ServletOutputStream` のメソッドを呼び `write` 出して、フォームデータストリームをクライアントWebブラウザーに送信します。 バイト配列をメソッドに渡し `write` ます。

**関連トピック**

[クイックスタート（SOAPモード）:Java APIを使用したクライアントでのフォームのレンダリング](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-at-the-client-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用してクライアントでフォームをレンダリングする {#render-a-form-at-the-client-using-the-web-service-api}

Forms API（Webサービス）を使用して、クライアントでフォームをレンダリングします。

1. プロジェクトファイルを含める

   * FormsサービスWSDLを使用するJavaプロキシクラスを作成します。
   * クラスパスにJavaプロキシクラスを含めます。

1. フォームクライアントAPIオブジェクトの作成

   オブジェクト `FormsService` を作成し、認証値を設定します。

1. クライアントレンダリングの実行時オプションの設定

   * コンストラクタを使用して `PDFFormRenderSpec` オブジェクトを作成します。
   * オブジェクト `RenderAtClient` のメソッドを呼び出し、文字列値を `PDFFormRenderSpec` 渡して、実 `setRenderAtClient` 行時オプションを設定しま `RenderAtClient.Yes`す。

1. クライアントでのフォームのレンダリング

   オブジェクト `FormsService` のメソッドを `renderPDFForm` 呼び出し、次の値を渡します。

   * ファイル名の拡張子を含むフォームデザイン名を指定するstring値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、必ずなどの完全なパスを指定してくださ `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`い。
   * フォーム `BLOB` とマージするデータを含むオブジェクトです。 データを結合しない場合は、を渡します `null`。 ( [Prepulating Forms with Flowable Layouts](/help/forms/developing/rendering-forms-rendering-forms prepopulating-forms-flowable-layouts-prepogulating.md#prepopulating-forms-with-flowable-layouts)を参照)。
   * クライア `PDFFormRenderSpec` ントでフォームをレンダリングするために必要な実行時オプションを格納するオブジェクトです。
   * Formsサ `URLSpec` ービスに必要なURI値を含むオブジェクトです。
   * 添付フ `java.util.HashMap` ァイルを格納するオブジェクト。 これはオプションのパラメーターで、フォームにフ `null` ァイルを添付しないかどうかを指定できます。
   * メソッドに `com.adobe.idp.services.holders.BLOBHolder` よって入力される空のオブジェクトです。 このパラメーターは、レンダリングされたPDFフォームを保存するために使用されます。
   * メソッドに `javax.xml.rpc.holders.LongHolder` よって入力される空のオブジェクトです。 （この引数には、フォーム内のページ数が格納されます）。
   * メソッドに `javax.xml.rpc.holders.StringHolder` よって入力される空のオブジェクトです。 （この引数はロケールの値を格納します）。
   * この操作 `com.adobe.idp.services.holders.FormsResultHolder` の結果を含む空のオブジェクトです。
   メソッド `renderPDFForm` は、最後の引 `com.adobe.idp.services.holders.FormsResultHolder` 数値として渡されたオブジェクトに、クライアントWebブラウザーに書き込む必要があるフォームデータストリームを入力します。

1. クライアントのWebブラウザーにフォームデータストリームを書き込みます

   * オブジェクト `FormResult` のデータメンバーの値を取得して、オ `com.adobe.idp.services.holders.FormsResultHolder` ブジェクトを `value` 作成します。
   * オブジェクトの `BLOB` メソッドを呼び出して、フォームデータを含むオ `FormsResult` ブジェクトを作成 `getOutputContent` します。
   * メソッドを呼び出して、オブジェ `BLOB` クトのコンテンツタイプを取得 `getContentType` します。
   * メソッドを呼 `javax.servlet.http.HttpServletResponse` び出し、オブジェクトのコンテンツタ `setContentType` イプを渡すことで、オブジェクトのコンテンツタイプを設定 `BLOB` します。
   * オブジェクトの `javax.servlet.ServletOutputStream` メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに書き込むために使用する `javax.servlet.http.HttpServletResponse` オブジェクトを作 `getOutputStream` 成します。
   * バイト配列を作成し、オブジェクトのメソッドを呼び出 `BLOB` して値を設定 `getBinaryData` します。 このタスクは、オブジェクトの内容をバ `FormsResult` イト配列に割り当てます。
   * オブジェクト `javax.servlet.http.HttpServletResponse` のメソッドを呼び `write` 出して、フォームデータストリームをクライアントWebブラウザーに送信します。 バイト配列をメソッドに渡し `write` ます。

**関連トピック**

[クライアントでのフォームのレンダリング](#rendering-forms-at-the-client)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
