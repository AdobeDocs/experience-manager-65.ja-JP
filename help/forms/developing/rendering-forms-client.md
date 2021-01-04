---
title: クライアントでのFormsのレンダリング
seo-title: クライアントでのFormsのレンダリング
description: AcrobatまたはAdobe Readerのクライアント側レンダリング機能を使用して、PDFコンテンツの配信を最適化し、Formsサービスのネットワーク負荷を処理する機能を改善します。
seo-description: AcrobatまたはAdobe Readerのクライアント側レンダリング機能を使用して、PDFコンテンツの配信を最適化し、Formsサービスのネットワーク負荷を処理する機能を改善します。
uuid: 09bcc23d-28b0-473a-87f1-bc17e87620f4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 08d36e9f-cafc-478e-9781-8fc29ac6262e
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '1716'
ht-degree: 2%

---


# クライアントでのFormsのレンダリング{#rendering-forms-at-the-client}

## クライアントでのFormsのレンダリング{#rendering-forms-at-the-client-inner}

AcrobatまたはAdobe Readerのクライアント側レンダリング機能を使用すると、PDFコンテンツの配信を最適化し、Formsサービスのネットワーク負荷を処理する機能を向上できます。 このプロセスは、クライアントでのフォームのレンダリングと呼ばれます。 クライアントでフォームをレンダリングするには、クライアントデバイス（通常はWebブラウザー）でAcrobat 7.0またはAdobe Reader7.0以降を使用する必要があります。

サーバーサイドのスクリプトの実行によって生じるフォームへの変更は、ルートサブフォームに`auto`に設定された`restoreState`属性が含まれていない限り、クライアントでレンダリングされるフォームには反映されません。 この属性について詳しくは、「[Formsデザイナー](https://www.adobe.com/go/learn_aemforms_designer_63)」を参照してください。

>[!NOTE]
>
>Formsサービスの詳細については、『[AEM Formsのサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順{#summary-of-steps}の概要

クライアントでフォームをレンダリングするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. FormsクライアントAPIオブジェクトを作成します。
1. クライアントレンダリングの実行時オプションを設定します。
1. クライアントでフォームをレンダリングします。
1. クライアントのWebブラウザーにフォームを書き込みます。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めてください。

**FormsクライアントAPIオブジェクトの作成**

プログラムでFormsサービスのクライアントAPI操作を実行する前に、Formsサービスクライアントを作成する必要があります。 Java APIを使用している場合は、`FormsServiceClient`オブジェクトを作成します。 FormsのWebサービスAPIを使用している場合は、`FormsService`オブジェクトを作成します。

**クライアントレンダリングの実行時オプションの設定**

`RenderAtClient`実行時オプションを`true`に設定して、クライアントでフォームをレンダリングするようにクライアントレンダリングの実行時オプションを設定する必要があります。 これにより、フォームがレンダリングされるクライアントデバイスにフォームが配信されます。 `RenderAtClient`が`auto`（デフォルト値）の場合、フォームデザインによって、フォームがクライアントでレンダリングされるかどうかが決まります。 フォームデザインは、編集可能なレイアウトを含むフォームデザインである必要があります。

オプションで設定できるランタイムオプションは`SeedPDF`オプションです。 `SeedPDF`オプションは、PDFコンテナ(シードPDFドキュメント)とフォームデザインとXMLデータを組み合わせます。 フォームデザインとXMLデータは共にAcrobatまたはAdobe Readerに配信され、そこでフォームがレンダリングされます。 `SeedPDF`オプションは、クライアントコンピューターにフォームで使用されるフォントがない場合（フォームの所有者にライセンスされているフォントを使用するライセンスがエンドユーザーにない場合など）に使用できます。

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

### Java API {#render-a-form-at-the-client-using-the-java-api}を使用してクライアントでフォームをレンダリングする

FormsAPI(Java)を使用して、クライアントでフォームをレンダリングします。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-forms-client.jarなどのクライアントJARファイルを含めます。

1. FormsクライアントAPIオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用し、`FormsServiceClient`オブジェクトを渡して、`ServiceClientFactory`オブジェクトを作成します。

1. クライアントレンダリングの実行時オプションの設定

   * コンストラクタを使用して `PDFFormRenderSpec` オブジェクトを作成します。
   * `RenderAtClient`実行時オプションを設定するには、`PDFFormRenderSpec`オブジェクトの`setRenderAtClient`メソッドを呼び出し、列挙値`RenderAtClient.Yes`を渡します。

1. クライアントでフォームをレンダリングする

   `FormsServiceClient`オブジェクトの`renderPDFForm`メソッドを呼び出し、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定するstring値。 AEM Formsアプリケーションの一部であるフォームデザインを参照する場合は、`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`など、完全なパスを必ず指定してください。
   * フォームとマージするデータを含む`com.adobe.idp.Document`オブジェクト。 データをマージしない場合は、空の`com.adobe.idp.Document`オブジェクトを渡します。
   * クライアントでフォームをレンダリングするために必要な実行時オプションを格納する`PDFFormRenderSpec`オブジェクト。
   * フォームのレンダリングにFormsサービスが必要とするURI値を含む`URLSpec`オブジェクトです。
   * 添付ファイルを格納する`java.util.HashMap`オブジェクト。 これはオプションのパラメーターです。フォームにファイルを添付しない場合は、`null`を指定できます。

   `renderPDFForm`メソッドは、クライアントのWebブラウザーに書き込む必要があるフォームデータストリームを含む`FormsResult`オブジェクトを返します。

1. フォームデータストリームをクライアントのWebブラウザーに書き込みます

   * `FormsResult`オブジェクト&#39;s `getOutputContent`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトを作成します。
   * `getContentType`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトのコンテンツタイプを取得します。
   * `javax.servlet.http.HttpServletResponse`オブジェクトのコンテンツタイプを設定するには、`setContentType`メソッドを呼び出し、`com.adobe.idp.Document`オブジェクトのコンテンツタイプを渡します。
   * `javax.servlet.http.HttpServletResponse`オブジェクトの`getOutputStream`メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに書き込むために使用する`javax.servlet.ServletOutputStream`オブジェクトを作成します。
   * `com.adobe.idp.Document`オブジェクトの`getInputStream`メソッドを呼び出して、`java.io.InputStream`オブジェクトを作成します。
   * バイト配列を作成し、`InputStream`オブジェクトの`read`メソッドを呼び出して、バイト配列を引数として渡すことで、フォームデータストリームを設定します。
   * `javax.servlet.ServletOutputStream`オブジェクトの`write`メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに送信します。 バイト配列を`write`メソッドに渡します。

**関連トピック**

[クイック開始（SOAPモード）:Java APIを使用したクライアントでのフォームのレンダリング](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-at-the-client-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#render-a-form-at-the-client-using-the-web-service-api}を使用して、クライアントでフォームをレンダリングする

FormsAPI（Webサービス）を使用して、クライアントでフォームをレンダリングします。

1. プロジェクトファイルを含める

   * FormsサービスのWSDLを使用するJavaプロキシクラスを作成します。
   * クラスパスにJavaプロキシクラスを含めます。

1. FormsクライアントAPIオブジェクトの作成

   `FormsService`オブジェクトを作成し、認証値を設定します。

1. クライアントレンダリングの実行時オプションの設定

   * コンストラクタを使用して `PDFFormRenderSpec` オブジェクトを作成します。
   * `RenderAtClient`実行時オプションを設定するには、`PDFFormRenderSpec`オブジェクトの`setRenderAtClient`メソッドを呼び出し、文字列値`RenderAtClient.Yes`を渡します。

1. クライアントでフォームをレンダリングする

   `FormsService`オブジェクトの`renderPDFForm`メソッドを呼び出し、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定するstring値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`など、完全なパスを必ず指定してください。
   * フォームとマージするデータを含む`BLOB`オブジェクト。 データを結合したくない場合は、`null`を渡します。 (「[編集可能なレイアウトでFormsを自動埋め込む](/help/forms/developing/prepopulating-forms-flowable-layouts.md)」を参照)。
   * クライアントでフォームをレンダリングするために必要な実行時オプションを格納する`PDFFormRenderSpec`オブジェクト。
   * Formsサービスに必要なURI値を含む`URLSpec`オブジェクト。
   * 添付ファイルを格納する`java.util.HashMap`オブジェクト。 これはオプションのパラメーターです。フォームにファイルを添付しない場合は、`null`を指定できます。
   * メソッドによって入力される空の`com.adobe.idp.services.holders.BLOBHolder`オブジェクト。 このパラメーターは、レンダリングされたPDFフォームを保存するために使用されます。
   * メソッドによって入力される空の`javax.xml.rpc.holders.LongHolder`オブジェクト。 （この引数は、フォームのページ数を格納します）。
   * メソッドによって入力される空の`javax.xml.rpc.holders.StringHolder`オブジェクト。 （この引数はロケールの値を格納します）。
   * この操作の結果を含む空の`com.adobe.idp.services.holders.FormsResultHolder`オブジェクトです。

   `renderPDFForm`メソッドは、最後の引数値として渡される`com.adobe.idp.services.holders.FormsResultHolder`オブジェクトに、クライアントWebブラウザーに書き込む必要のあるフォームデータストリームを入力します。

1. フォームデータストリームをクライアントのWebブラウザーに書き込みます

   * `com.adobe.idp.services.holders.FormsResultHolder`オブジェクトの`value`データメンバの値を取得して、`FormResult`オブジェクトを作成します。
   * `FormsResult`オブジェクトの`getOutputContent`メソッドを呼び出して、フォームデータを含む`BLOB`オブジェクトを作成します。
   * `getContentType`メソッドを呼び出して、`BLOB`オブジェクトのコンテンツタイプを取得します。
   * `javax.servlet.http.HttpServletResponse`オブジェクトのコンテンツタイプを設定するには、`setContentType`メソッドを呼び出し、`BLOB`オブジェクトのコンテンツタイプを渡します。
   * `javax.servlet.http.HttpServletResponse`オブジェクトの`getOutputStream`メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに書き込むために使用する`javax.servlet.ServletOutputStream`オブジェクトを作成します。
   * バイト配列を作成し、`BLOB`オブジェクトの`getBinaryData`メソッドを呼び出して値を設定します。 このタスクは、`FormsResult`オブジェクトの内容をバイト配列に割り当てます。
   * `javax.servlet.http.HttpServletResponse`オブジェクトの`write`メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに送信します。 バイト配列を`write`メソッドに渡します。

**関連トピック**

[クライアントでのFormsのレンダリング](#rendering-forms-at-the-client)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
