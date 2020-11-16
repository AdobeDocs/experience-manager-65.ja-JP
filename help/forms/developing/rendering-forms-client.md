---
title: クライアントでのFormsのレンダリング
seo-title: クライアントでのFormsのレンダリング
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
source-git-commit: ab401a8007f6ea85c0e52169091ce7a38b3dbe5c
workflow-type: tm+mt
source-wordcount: '1664'
ht-degree: 2%

---


# クライアントでのFormsのレンダリング {#rendering-forms-at-the-client}

## クライアントでのFormsのレンダリング {#rendering-forms-at-the-client-inner}

AcrobatまたはAdobe Readerのクライアント側レンダリング機能を使用すると、PDFコンテンツの配信を最適化し、Formsサービスのネットワーク負荷を処理する機能を向上できます。 このプロセスは、クライアントでのフォームのレンダリングと呼ばれます。 クライアントでフォームをレンダリングするには、クライアントデバイス（通常はWebブラウザー）でAcrobat 7.0またはAdobe Reader7.0以降を使用する必要があります。

サーバーサイドのスクリプトの実行によって生じるフォームに対する変更は、ルートサブフォームに設定された `restoreState` 属性が含まれていない限り、クライアントでレンダリングされるフォームには反映されません `auto`。 この属性について詳しくは、「 [Formsデザイナ」を参照してください。](https://www.adobe.com/go/learn_aemforms_designer_63)

>[!NOTE]
>
>For more information about the Forms service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### 手順の概要 {#summary-of-steps}

クライアントでフォームをレンダリングするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. FormsクライアントAPIオブジェクトを作成します。
1. クライアントレンダリングの実行時オプションを設定します。
1. クライアントでフォームをレンダリングします。
1. クライアントのWebブラウザーにフォームを書き込みます。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めてください。

**FormsクライアントAPIオブジェクトの作成**

プログラムでFormsサービスのクライアントAPI操作を実行する前に、Formsサービスクライアントを作成する必要があります。 Java APIを使用している場合は、 `FormsServiceClient` オブジェクトを作成します。 FormsWebサービスAPIを使用している場合は、 `FormsService` オブジェクトを作成します。

**クライアントレンダリングの実行時オプションの設定**

実行時オプションをに設定して、クライアントでフォームをレンダリングする場合は、クライアントレンダリングの実行時オプションを設定する必要があり `RenderAtClient``true`ます。 これにより、フォームがレンダリングされるクライアントデバイスにフォームが配信されます。 が `RenderAtClient``auto` （デフォルト値）の場合、フォームデザインによって、フォームがクライアントでレンダリングされるかどうかが決まります。 フォームデザインは、編集可能なレイアウトを含むフォームデザインである必要があります。

オプションで設定できる実行時オプションは、 `SeedPDF` オプションです。 この `SeedPDF` オプションは、PDFコンテナ(シードPDFドキュメント)とフォームデザインおよびXMLデータを組み合わせます。 フォームデザインとXMLデータは共にAcrobatまたはAdobe Readerに配信され、そこでフォームがレンダリングされます。 この `SeedPDF` オプションは、クライアントコンピューターにフォームで使用されるフォントがない場合（フォームの所有者がライセンスを受けているフォントを使用するライセンスがエンドユーザーにない場合など）に使用できます。

Designerを使用すると、シードPDFファイルとして使用する単純な動的PDFファイルを作成できます。 このタスクを実行するには、次の手順を実行する必要があります。

1. シードPDFファイル内にフォントを埋め込む必要があるかどうかを指定します。 シードPDFファイルには、レンダリングするフォームに必要な追加のフォントを含める必要があります。 シードPDFファイルにフォントを埋め込む場合は、フォントの使用許諾契約に違反していないことを確認してください。 Designerでは、フォントを法的に埋め込めるかどうかを指定できます。 保存時に、フォームに埋め込むことができないフォントが存在する場合、Designerは埋め込めないフォントを一覧表示したメッセージを表示します。 スタティックPDFドキュメントの場合、このメッセージはDesignerには表示されません。
1. シードPDFファイルをDesignerで作成する場合は、少なくともメッセージを含むテキストフィールドを追加することをお勧めします。 このメッセージは、ドキュメントの表示にAcrobat 7.0以降またはAdobe Reader7.0以降が必要であるという内容の、Adobe Readerの以前のバージョンのユーザー向けに送信する必要があります。
1. シードPDFファイルを、PDFファイル名拡張子が付いた動的PDFファイルとして保存します。

>[!NOTE]
>
>クライアント上でフォームをレンダリングする場合、シードPDFランタイムオプションを定義する必要はありません。 シードPDFを指定しない場合、FormsサービスはCOSオブジェクトは含まず、実際のXDPコンテンツが内部に埋め込まれたPDFラッパーを含むシェルPDFを作成します。 この節の手順では、シードPDFの実行時オプションを設定しません。 COSオブジェクトの詳細については、『Adobe PDFリファレンス』マニュアルを参照してください。

**クライアントでフォームをレンダリングする**

クライアントでフォームをレンダリングするには、フォームをレンダリングするアプリケーションロジックにクライアントレンダリングの実行時オプションが含まれていることを確認する必要があります。

**フォームデータストリームをクライアントのWebブラウザーに書き込みます**

Formsサービスはフォームデータストリームを作成します。このデータストリームは、クライアントのWebブラウザーに書き込む必要があります。 クライアントWebブラウザーに書き込むと、フォームはAcrobat 7.0またはAdobe Reader7.0以降でレンダリングされ、ユーザーに表示されます。

**関連トピック**

[Java APIを使用してクライアントでフォームをレンダリングする](#render-a-form-at-the-client-using-the-java-api)

[WebサービスAPIを使用してクライアントでフォームをレンダリングする](#render-a-form-at-the-client-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[FormsサービスAPIクイック開始](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Formsサービスにドキュメントを渡す](/help/forms/developing/passing-documents-forms-service.md)

[FormsをレンダリングするWeb アプリケーションの作成](/help/forms/developing/creating-web-applications-renders-forms.md)

### Java APIを使用してクライアントでフォームをレンダリングする {#render-a-form-at-the-client-using-the-java-api}

FormsAPI(Java)を使用して、クライアントでフォームをレンダリングします。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-forms-client.jarなどのクライアントJARファイルを含めます。

1. FormsクライアントAPIオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `FormsServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. クライアントレンダリングの実行時オプションの設定

   * コンストラクタを使用して `PDFFormRenderSpec` オブジェクトを作成します。
   * オブジェクトの `RenderAtClient` メソッドを呼び出し、列挙値を渡して、 `PDFFormRenderSpec` 実行時オプションを設定 `setRenderAtClient``RenderAtClient.Yes`します。

1. クライアントでフォームをレンダリングする

   オブジェクトの `FormsServiceClient``renderPDFForm` メソッドを呼び出し、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定するstring値。 AEM Formsアプリケーションの一部であるフォームデザインを参照する場合は、完全なパスを必ず指定してください（例：） `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * フォームとマージするデータを含む `com.adobe.idp.Document` オブジェクト。 データをマージしない場合は、空の `com.adobe.idp.Document` オブジェクトを渡します。
   * クライアントでフォームをレンダリングするために必要な実行時オプションを格納する `PDFFormRenderSpec` オブジェクト。
   * フォームのレンダリングにFormsサービスが必要とするURI値を含む `URLSpec` オブジェクトです。
   * 添付ファイルを格納する `java.util.HashMap` オブジェクトです。 これはオプションのパラメーターで、フォームにファイルを添付しない `null` かどうかを指定できます。

   この `renderPDFForm``FormsResult` メソッドは、クライアントのWebブラウザーに書き込む必要があるフォームデータストリームを含むオブジェクトを返します。

1. フォームデータストリームをクライアントのWebブラウザーに書き込みます

   * オブジェクトの `com.adobe.idp.Document` メソッドを呼び出して、 `FormsResult` オブジェクトを作成し `getOutputContent` ます。
   * メソッドを呼び出して、 `com.adobe.idp.Document` オブジェクトのコンテンツタイプを取得し `getContentType` ます。
   * メソッドを呼び出し、オブジェクトの `javax.servlet.http.HttpServletResponse` コンテンツタイプを渡すことで、 `setContentType``com.adobe.idp.Document` オブジェクトのコンテンツタイプを設定します。
   * オブジェクトの `javax.servlet.ServletOutputStream` メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに書き込むために使用する `javax.servlet.http.HttpServletResponse``getOutputStream` オブジェクトを作成します。
   * オブジェクトの `java.io.InputStream` メソッドを呼び出して、 `com.adobe.idp.Document` オブジェクトを作成 `getInputStream` します。
   * バイト配列を作成し、 `InputStream` オブジェクトの `read` メソッドを呼び出して、バイト配列を引数として渡すことで、フォームデータストリームを設定します。
   * オブジェクトの `javax.servlet.ServletOutputStream``write` メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに送信します。 バイト配列を `write` メソッドに渡します。

**関連トピック**

[クイック開始（SOAPモード）:Java APIを使用したクライアントでのフォームのレンダリング](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-at-the-client-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用してクライアントでフォームをレンダリングする {#render-a-form-at-the-client-using-the-web-service-api}

FormsAPI（Webサービス）を使用して、クライアントでフォームをレンダリングします。

1. プロジェクトファイルを含める

   * FormsサービスのWSDLを使用するJavaプロキシクラスを作成します。
   * クラスパスにJavaプロキシクラスを含めます。

1. FormsクライアントAPIオブジェクトの作成

   オブジェクトを作成し、認証値を設定し `FormsService` ます。

1. クライアントレンダリングの実行時オプションの設定

   * コンストラクタを使用して `PDFFormRenderSpec` オブジェクトを作成します。
   * オブジェクトの `RenderAtClient` メソッドを呼び出し、文字列値を渡して、 `PDFFormRenderSpec` 実行時オプションを設定 `setRenderAtClient``RenderAtClient.Yes`します。

1. クライアントでフォームをレンダリングする

   オブジェクトの `FormsService``renderPDFForm` メソッドを呼び出し、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定するstring値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、完全なパスを必ず指定してください（例：） `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * フォームとマージするデータを含む `BLOB` オブジェクト。 データを結合したくない場合は、を渡し `null`ます。 (編集可能なレイアウト [をFormsに自動埋め込むを参照](/help/forms/developing/prepopulating-forms-flowable-layouts.md))。
   * クライアントでフォームをレンダリングするために必要な実行時オプションを格納する `PDFFormRenderSpec` オブジェクト。
   * Formsサービスに必要なURI値を含む `URLSpec` オブジェクトです。
   * 添付ファイルを格納する `java.util.HashMap` オブジェクトです。 これはオプションのパラメーターで、フォームにファイルを添付しない `null` かどうかを指定できます。
   * メソッドによって入力される空の `com.adobe.idp.services.holders.BLOBHolder` オブジェクトです。 このパラメーターは、レンダリングされたPDFフォームを保存するために使用されます。
   * メソッドによって入力される空の `javax.xml.rpc.holders.LongHolder` オブジェクトです。 （この引数は、フォームのページ数を格納します）。
   * メソッドによって入力される空の `javax.xml.rpc.holders.StringHolder` オブジェクトです。 （この引数はロケールの値を格納します）。
   * この操作の結果を含む空の `com.adobe.idp.services.holders.FormsResultHolder` オブジェクトです。

   この `renderPDFForm` メソッドは、最後の引数値として渡される `com.adobe.idp.services.holders.FormsResultHolder` オブジェクトに、クライアントWebブラウザーに書き込む必要があるフォームデータストリームを入力します。

1. フォームデータストリームをクライアントのWebブラウザーに書き込みます

   * オブジェクトの `FormResult` データメンバーの値を取得して `com.adobe.idp.services.holders.FormsResultHolder` オブジェクトを作成し `value` ます。
   * オブジェクトの `BLOB` メソッドを呼び出して、フォームデータを含む `FormsResult` オブジェクトを作成し `getOutputContent` ます。
   * メソッドを呼び出して、 `BLOB` オブジェクトのコンテンツタイプを取得し `getContentType` ます。
   * メソッドを呼び出し、オブジェクトの `javax.servlet.http.HttpServletResponse` コンテンツタイプを渡すことで、 `setContentType``BLOB` オブジェクトのコンテンツタイプを設定します。
   * オブジェクトの `javax.servlet.ServletOutputStream` メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに書き込むために使用する `javax.servlet.http.HttpServletResponse``getOutputStream` オブジェクトを作成します。
   * バイト配列を作成し、 `BLOB` オブジェクトの `getBinaryData` メソッドを呼び出して値を設定します。 このタスクは、 `FormsResult` オブジェクトの内容をバイト配列に割り当てます。
   * オブジェクトの `javax.servlet.http.HttpServletResponse``write` メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに送信します。 バイト配列を `write` メソッドに渡します。

**関連トピック**

[クライアントでのFormsのレンダリング](#rendering-forms-at-the-client)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
