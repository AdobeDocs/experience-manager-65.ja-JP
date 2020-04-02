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
source-git-commit: ab401a8007f6ea85c0e52169091ce7a38b3dbe5c

---


# クライアントでのフォームのレンダリング {#rendering-forms-at-the-client}

## クライアントでのフォームのレンダリング {#rendering-forms-at-the-client-inner}

AcrobatまたはAdobe Readerのクライアント側のレンダリング機能を使用すると、PDFコンテンツの配信を最適化し、Formsサービスのネットワーク読み込み処理機能を向上できます。 このプロセスは、クライアントでのフォームのレンダリングと呼ばれます。 クライアントでフォームをレンダリングするには、クライアントデバイス（通常はWebブラウザー）でAcrobat 7.0またはAdobe Reader 7.0以降を使用する必要があります。

サーバーサイドのスクリプトの実行によるフォームへの変更は、ルートサブフォームに設定された属性が含まれていない限り、クライアントでレンダリングされるフ `restoreState` ォームには反映されませ `auto`ん。 この属性について詳しくは、「 [Forms Designer」を参照してください。](https://www.adobe.com/go/learn_aemforms_designer_63)

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

プログラムによってFormsサービスのクライアントAPI操作を実行する前に、Formsサービスクライアントを作成する必要があります。 Java APIを使用している場合は、オブジェクトを作成し `FormsServiceClient` ます。 Forms WebサービスAPIを使用している場合は、オブジェクトを作成 `FormsService` します。

**クライアントレンダリングの実行時オプションの設定**

クライアントレンダリングの実行時オプションを設定し、実行時オプションをに設定して、クライアントでフォームをレンダリング `RenderAtClient` する必要がありま `true`す。 この結果、フォームがレンダリングされるクライアントデバイスにフォームが配信されます。 が(デフ `RenderAtClient` ォル `auto` ト値)の場合、フォームデザインによって、フォームがクライアントでレンダリングされるかどうかが決まります。 フォームデザインは、編集可能なレイアウトを含むフォームデザインである必要があります。

オプションで設定できる実行時オプションがこのオプシ `SeedPDF` ョンです。 このオ `SeedPDF` プションは、PDFコンテナ(シードPDFドキュメント)とフォームデザインおよびXMLデータを組み合わせます。 フォームデザインとXMLデータの両方がAcrobatまたはAdobe Readerに配信され、フォームがレンダリングされます。 このオ `SeedPDF` プションは、クライアントコンピューターにフォームで使用されているフォントがない場合（フォームの所有者が使用を許可されているフォントを使用するライセンスがエンドユーザーにない場合など）に使用できます。

Designerを使用して、シードPDFファイルとして使用するシンプルなダイナミックPDFファイルを作成できます。 この操作を実行するには、次の手順が必要です。タスク

1. シードPDFファイル内にフォントを埋め込む必要があるかどうかを指定します。 シードPDFファイルには、レンダリングするフォームに必要な追加のフォントを含める必要があります。 シードPDFファイルにフォントを埋め込む場合は、フォントの使用許諾契約に違反していないことを確認してください。 Designerでは、フォントを法的に埋め込むことができるかどうかを指定できます。 保存時に、フォームに埋め込めないフォントが存在する場合、Designerは埋め込めないフォントの一覧を示すメッセージを表示します。 このメッセージは、スタティックPDFメッセージに対してはDesignerでは表示されません。ドキュメント
1. DesignerでシードPDFファイルを作成する場合は、少なくともメッセージを含むテキストフィールドを追加することをお勧めします。 ドキュメントの表示にAcrobat 7.0以降またはAdobe Reader 7.0以降が必要であることを伝えるメッセージが、以前のバージョンのAdobe Readerのユーザーに表示されます。
1. シードPDFファイルを、PDFファイル名拡張子が付いたダイナミックPDFファイルとして保存します。

>[!NOTE]
>
>クライアント上でフォームをレンダリングする場合、シードPDFの実行時オプションを定義する必要はありません。 シードPDFを指定しない場合、FormsサービスはCOSオブジェクトは含まれず、実際のXDPコンテンツが内部に埋め込まれたPDFラッパーを含むシェルPDFを作成します。 この節の手順では、シードPDFの実行時オプションは設定しません。 COSオブジェクトについて詳しくは、『Adobe PDF Reference』ガイドを参照してください。

**クライアントでのフォームのレンダリング**

クライアントでフォームをレンダリングするには、フォームをレンダリングするクライアントレンダリングの実行時オプションがアプリケーションロジックに含まれていることを確認する必要があります。

**フォームデータストリームをクライアントWebブラウザーに書き込む**

Formsサービスは、クライアントWebブラウザーに書き込む必要のあるフォームデータストリームを作成します。 クライアントWebブラウザーに書き込むと、フォームはAcrobat 7.0またはAdobe Reader 7.0以降でレンダリングされ、ユーザーに表示されます。

**関連トピック**

[Java APIを使用してクライアントでフォームをレンダリングする](#render-a-form-at-the-client-using-the-java-api)

[WebサービスAPIを使用してクライアントでフォームをレンダリングする](#render-a-form-at-the-client-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[FormsサービスAPIのクイック開始](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Formsサービスへのドキュメントの引き渡し](/help/forms/developing/passing-documents-forms-service.md)

[フォームをレンダリングするWeb アプリケーションの作成](/help/forms/developing/creating-web-applications-renders-forms.md)

### Java APIを使用してクライアントでフォームをレンダリングする {#render-a-form-at-the-client-using-the-java-api}

Forms API (Java)を使用して、クライアントでフォームをレンダリングします。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-forms-client.jarなどのクライアントJARファイルを含めます。

1. フォームクライアントAPIオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `FormsServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. クライアントレンダリングの実行時オプションの設定

   * コンストラクタを使用して `PDFFormRenderSpec` オブジェクトを作成します。
   * オブジェクト `RenderAtClient` のメソッドを呼び出し、列挙 `PDFFormRenderSpec` 値を渡して、 `setRenderAtClient` 実行時のオプションを設定しま `RenderAtClient.Yes`す。

1. クライアントでのフォームのレンダリング

   オブジェクト `FormsServiceClient` のメソッドを `renderPDFForm` 呼び出し、次の値を渡します。

   * ファイル名の拡張子を含む、フォームデザイン名を指定するstring値。 AEM Formsアプリケーションの一部であるフォームデザインを参照する場合は、次のような完全なパスを必ず指定してくださ `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`い。
   * フォーム `com.adobe.idp.Document` とマージするデータを含むオブジェクトです。 データを結合しない場合は、空のオブジェクトを渡し `com.adobe.idp.Document` ます。
   * クライア `PDFFormRenderSpec` ントでフォームをレンダリングするために必要な実行時オプションを格納するオブジェクト。
   * Formsサ `URLSpec` ービスでフォームをレンダリングするために必要なURI値を含むオブジェクトです。
   * 添付ファ `java.util.HashMap` イルを格納するオブジェクト。 これはオプションのパラメーターで、フォームにフ `null` ァイルを添付しないかどうかを指定できます。
   このメソ `renderPDFForm` ッドは、クラ `FormsResult` イアントWebブラウザーに書き込む必要があるフォームデータストリームを含むオブジェクトを返します。

1. フォームデータストリームをクライアントWebブラウザーに書き込む

   * オブジェクトの `com.adobe.idp.Document` メソッドを呼び出して、オ `FormsResult` ブジェクトを作成 `getOutputContent` します。
   * メソッドを呼び出して、オブジェ `com.adobe.idp.Document` クトのコンテンツタイプを取 `getContentType` 得します。
   * メソッドを呼 `javax.servlet.http.HttpServletResponse` び出し、オブジェクトのコンテ `setContentType` ンツタイプを渡して、オブジェクトのコンテンツタイプを設定 `com.adobe.idp.Document` します。
   * オブジェクトの `javax.servlet.ServletOutputStream` メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに書き込むために使用す `javax.servlet.http.HttpServletResponse` るオブジェクトを作成 `getOutputStream` します。
   * オブジェクトの `java.io.InputStream` メソッドを呼び出して、オ `com.adobe.idp.Document` ブジェクトを作成 `getInputStream` します。
   * バイト配列を作成し、オブジェクトのメソッドを呼び出し、バイト配列を引 `InputStream` 数として渡すこ `read` とで、フォームデータストリームを設定します。
   * オブジェクト `javax.servlet.ServletOutputStream` のメソッドを呼 `write` び出して、フォームデータストリームをクライアントWebブラウザーに送信します。 バイト配列をメソッドに渡し `write` ます。

**関連トピック**

[クイック開始（SOAPモード）:Java APIを使用したクライアントでのフォームのレンダリング](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-at-the-client-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用してクライアントでフォームをレンダリングする {#render-a-form-at-the-client-using-the-web-service-api}

Forms API（Webサービス）を使用して、クライアントでフォームをレンダリングします。

1. プロジェクトファイルを含める

   * FormsサービスのWSDLを使用するJavaプロキシクラスを作成します。
   * クラスパスにJavaプロキシクラスを含めます。

1. フォームクライアントAPIオブジェクトの作成

   オブジェクトを `FormsService` 作成し、認証値を設定します。

1. クライアントレンダリングの実行時オプションの設定

   * コンストラクタを使用して `PDFFormRenderSpec` オブジェクトを作成します。
   * オブジェクト `RenderAtClient` のメソッドを呼び出し、文字 `PDFFormRenderSpec` 列値を渡すこ `setRenderAtClient` とで、実行時オプションを設定しま `RenderAtClient.Yes`す。

1. クライアントでのフォームのレンダリング

   オブジェクト `FormsService` のメソッドを `renderPDFForm` 呼び出し、次の値を渡します。

   * ファイル名の拡張子を含む、フォームデザイン名を指定するstring値。 Formsアプリケーションの一部であるフォームデザインを参照する場合、などの完全なパスを必ず指定してくださ `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`い。
   * フォーム `BLOB` とマージするデータを含むオブジェクトです。 データを結合しない場合は、を渡します `null`。 (編集可能な [レイアウトでのフォームの自動埋め込みを参照](/help/forms/developing/prepopulating-forms-flowable-layouts.md))。
   * クライア `PDFFormRenderSpec` ントでフォームをレンダリングするために必要な実行時オプションを格納するオブジェクト。
   * Formsサ `URLSpec` ービスで必要なURI値を含むオブジェクトです。
   * 添付ファ `java.util.HashMap` イルを格納するオブジェクト。 これはオプションのパラメーターで、フォームにフ `null` ァイルを添付しないかどうかを指定できます。
   * メソッドに `com.adobe.idp.services.holders.BLOBHolder` よって入力される空のオブジェクトです。 このパラメーターは、レンダリングされたPDFフォームを保存するために使用されます。
   * メソッドに `javax.xml.rpc.holders.LongHolder` よって入力される空のオブジェクトです。 （この引数は、フォームのページ数を格納します）。
   * メソッドに `javax.xml.rpc.holders.StringHolder` よって入力される空のオブジェクトです。 （この引数にはロケールの値が格納されます）。
   * この操作の `com.adobe.idp.services.holders.FormsResultHolder` 結果を含む空のオブジェクトです。
   メソッド `renderPDFForm` は、最後の引 `com.adobe.idp.services.holders.FormsResultHolder` 数として渡されたオブジェクトに、クライアントWebブラウザーに書き込む必要のあるフォームデータストリームを設定します。

1. フォームデータストリームをクライアントWebブラウザーに書き込む

   * オブジェクト `FormResult` のデータメンバーの値を取得して、オ `com.adobe.idp.services.holders.FormsResultHolder` ブジェクトを `value` 作成します。
   * オブジェクトの `BLOB` メソッドを呼び出して、フォームデータを含む `FormsResult` オブジェクトを作成 `getOutputContent` します。
   * メソッドを呼び出して、オブジェ `BLOB` クトのコンテンツタイプを取 `getContentType` 得します。
   * メソッドを呼 `javax.servlet.http.HttpServletResponse` び出し、オブジェクトのコンテ `setContentType` ンツタイプを渡して、オブジェクトのコンテンツタイプを設定 `BLOB` します。
   * オブジェクトの `javax.servlet.ServletOutputStream` メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに書き込むために使用す `javax.servlet.http.HttpServletResponse` るオブジェクトを作成 `getOutputStream` します。
   * バイト配列を作成し、オブジェクトのメソッドを呼び出 `BLOB` して値を設定 `getBinaryData` します。 このタスクは、オブジェクトの内容をバ `FormsResult` イト配列に割り当てます。
   * オブジェクト `javax.servlet.http.HttpServletResponse` のメソッドを呼 `write` び出して、フォームデータストリームをクライアントWebブラウザーに送信します。 バイト配列をメソッドに渡し `write` ます。

**関連トピック**

[クライアントでのフォームのレンダリング](#rendering-forms-at-the-client)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
