---
title: クライアントでのFormsのレンダリング
seo-title: クライアントでのFormsのレンダリング
description: AcrobatまたはAdobe Readerのクライアント側レンダリング機能を使用して、PDFコンテンツの配信を最適化し、Formsサービスのネットワーク読み込み処理機能を改善します
seo-description: AcrobatまたはAdobe Readerのクライアント側レンダリング機能を使用して、PDFコンテンツの配信を最適化し、Formsサービスのネットワーク読み込み処理機能を改善します
uuid: 09bcc23d-28b0-473a-87f1-bc17e87620f4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 08d36e9f-cafc-478e-9781-8fc29ac6262e
role: Developer
exl-id: e485980d-f200-46b7-9284-c9996003aa47
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1730'
ht-degree: 2%

---

# クライアントでのFormsのレンダリング{#rendering-forms-at-the-client}

**このドキュメントのサンプルと例は、JEE上のAEM Forms環境に限られています。**

## クライアントでのFormsのレンダリング{#rendering-forms-at-the-client-inner}

AcrobatまたはAdobe Readerのクライアント側レンダリング機能を使用すると、PDFコンテンツの配信を最適化し、Formsサービスのネットワーク読み込み処理機能を向上できます。 このプロセスは、クライアントでのフォームのレンダリングと呼ばれます。 クライアントでフォームをレンダリングするには、クライアントデバイス（通常はWebブラウザー）でAcrobat 7.0またはAdobe Reader 7.0以降を使用する必要があります。

サーバー側スクリプトの実行によって生成されたフォームに対する変更は、ルートサブフォームに`auto`に設定された`restoreState`属性が含まれていない限り、クライアント側でレンダリングされるフォームに反映されません。 この属性について詳しくは、[Forms Designer.](https://www.adobe.com/go/learn_aemforms_designer_63)を参照してください。

>[!NOTE]
>
>Formsサービスについて詳しくは、『 AEM Formsのサービスリファレンス[ 』を参照してください。](https://www.adobe.com/go/learn_aemforms_services_63)

### 手順の概要{#summary-of-steps}

クライアントでフォームをレンダリングするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Forms Client APIオブジェクトを作成します。
1. クライアントレンダリングの実行時オプションを設定します。
1. クライアントでフォームをレンダリングします。
1. クライアントのWebブラウザーにフォームを書き込みます。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用する場合は、プロキシファイルを必ず含めてください。

**Forms Client APIオブジェクトの作成**

FormsサービスクライアントAPI操作をプログラムで実行する前に、Formsサービスクライアントを作成する必要があります。 Java APIを使用している場合は、`FormsServiceClient`オブジェクトを作成します。 Forms WebサービスAPIを使用している場合は、`FormsService`オブジェクトを作成します。

**クライアントレンダリングの実行時オプションの設定**

クライアントでフォームをレンダリングするランタイムオプションを設定するには、`RenderAtClient`ランタイムオプションを`true`に設定する必要があります。 これにより、フォームがレンダリングされるクライアントデバイスにフォームが配信されます。 `RenderAtClient`が`auto`（デフォルト値）の場合、フォームデザインによって、フォームがクライアントでレンダリングされるかどうかが決まります。 フォームデザインは、編集可能なレイアウトを含むフォームデザインにする必要があります。

設定できるオプションの実行時オプションは`SeedPDF`オプションです。 `SeedPDF`オプションは、PDFコンテナ（シードPDFドキュメント）とフォームデザインとXMLデータを組み合わせます。 フォームデザインとXMLデータの両方が、フォームがレンダリングされるAcrobatまたはAdobe Readerに配信されます。 `SeedPDF`オプションは、クライアントコンピューターにフォームで使用されるフォントがない場合に使用できます。例えば、エンドユーザーが、フォーム所有者が使用するライセンスを持つフォントを使用するライセンスを持っていない場合などです。

Designerを使用して、シードPDFファイルとして使用する簡単なダイナミックPDFファイルを作成できます。 このタスクを実行するには、次の手順が必要です。

1. シードPDFファイル内にフォントを埋め込む必要があるかどうかを指定します。 シードPDFファイルには、レンダリングされるフォームに必要な追加のフォントを含める必要があります。 シードPDFファイルにフォントを埋め込む場合は、フォント使用許諾契約に違反しないようにしてください。 Designerでは、フォントを法的に埋め込めるかどうかを指定できます。 保存時に、フォームに埋め込めないフォントがある場合、Designerは埋め込めないフォントの一覧を示すメッセージを表示します。 このメッセージは、スタティックPDFドキュメントの場合はDesignerには表示されません。
1. DesignerでシードPDFファイルを作成する場合は、少なくともメッセージを含むテキストフィールドを追加することをお勧めします。 このメッセージは、Adobe Readerの以前のバージョンのユーザーに対し、ドキュメントを表示するにはAcrobat 7.0以降またはAdobe Reader 7.0以降が必要であることを示すものにする必要があります。
1. シードPDFファイルを、PDFファイル名拡張子を持つダイナミックPDFファイルとして保存します。

>[!NOTE]
>
>クライアント上でフォームをレンダリングする場合、シードPDFの実行時オプションを定義する必要はありません。 シードPDFを指定しない場合、FormsサービスはシェルPDFを作成します。このPDFには、COSオブジェクトは含まれず、実際のXDPコンテンツが埋め込まれます。 この節の手順では、シードPDFの実行時オプションは設定しません。 COSオブジェクトについて詳しくは、『 Adobe PDFリファレンスガイド』を参照してください。

**クライアントでのフォームのレンダリング**

クライアントでフォームをレンダリングするには、フォームをレンダリングするクライアントレンダリングの実行時オプションがアプリケーションロジックに含まれている必要があります。

**フォームデータストリームをクライアントWebブラウザーに書き込む**

Formsサービスは、クライアントのWebブラウザーに書き込む必要があるフォームデータストリームを作成します。 クライアントのWebブラウザーに書き込まれると、フォームはAcrobat 7.0またはAdobe Reader 7.0以降でレンダリングされ、ユーザーに対して表示されます。

**関連トピック**

[Java APIを使用してクライアントでフォームをレンダリングする](#render-a-form-at-the-client-using-the-java-api)

[WebサービスAPIを使用してクライアントでフォームをレンダリングする](#render-a-form-at-the-client-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[FormsサービスAPIのクイックスタート](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Formsサービスにドキュメントを渡す](/help/forms/developing/passing-documents-forms-service.md)

[Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Java API {#render-a-form-at-the-client-using-the-java-api}を使用してクライアントでフォームをレンダリングする

Forms API(Java)を使用して、クライアントでフォームをレンダリングします。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-forms-client.jarなどのクライアントJARファイルを含めます。

1. Forms Client APIオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して`FormsServiceClient`オブジェクトを渡し、`ServiceClientFactory`オブジェクトを作成します。

1. クライアントレンダリングの実行時オプションの設定

   * コンストラクタを使用して `PDFFormRenderSpec` オブジェクトを作成します。
   * `PDFFormRenderSpec`オブジェクトの`setRenderAtClient`メソッドを呼び出し、列挙値`RenderAtClient.Yes`を渡すことで、`RenderAtClient`実行時オプションを設定します。

1. クライアントでのフォームのレンダリング

   `FormsServiceClient`オブジェクトの`renderPDFForm`メソッドを呼び出し、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定するstring値。 AEM Formsアプリケーションの一部であるフォームデザインを参照する場合は、必ず`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`のように完全なパスを指定してください。
   * フォームとマージするデータを含む`com.adobe.idp.Document`オブジェクト。 データを結合しない場合は、空の`com.adobe.idp.Document`オブジェクトを渡します。
   * クライアントでフォームをレンダリングするために必要な実行時オプションを格納する`PDFFormRenderSpec`オブジェクト。
   * フォームをレンダリングするためにFormsサービスで必要なURI値を含む`URLSpec`オブジェクト。
   * 添付ファイルを格納する`java.util.HashMap`オブジェクト。 これはオプションのパラメーターで、フォームにファイルを添付しない場合は`null`を指定できます。

   `renderPDFForm`メソッドは、クライアントのWebブラウザーに書き込む必要があるフォームデータストリームを含む`FormsResult`オブジェクトを返します。

1. フォームデータストリームをクライアントWebブラウザーに書き込む

   * `FormsResult`オブジェクトの`getOutputContent`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトを作成します。
   * `getContentType`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトのコンテンツタイプを取得します。
   * `setContentType`メソッドを呼び出し、`com.adobe.idp.Document`オブジェクトのコンテンツタイプを渡すことで、`javax.servlet.http.HttpServletResponse`オブジェクトのコンテンツタイプを設定します。
   * `javax.servlet.http.HttpServletResponse`オブジェクトの`getOutputStream`メソッドを呼び出して、フォームデータストリームをクライアントWebブラウザーに書き込むための`javax.servlet.ServletOutputStream`オブジェクトを作成します。
   * `com.adobe.idp.Document`オブジェクトの`getInputStream`メソッドを呼び出して、`java.io.InputStream`オブジェクトを作成します。
   * `InputStream`オブジェクトの`read`メソッドを呼び出し、バイト配列を引数として渡すことで、バイト配列を作成し、フォームデータストリームに入力します。
   * `javax.servlet.ServletOutputStream`オブジェクトの`write`メソッドを呼び出して、フォームデータストリームをクライアントWebブラウザーに送信します。 `write`メソッドにバイト配列を渡します。

**関連トピック**

[クイックスタート（SOAPモード）:Java APIを使用したクライアントでのフォームのレンダリング](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-at-the-client-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#render-a-form-at-the-client-using-the-web-service-api}を使用してクライアントでフォームをレンダリングする

Forms API（Webサービス）を使用して、クライアントでフォームをレンダリングします。

1. プロジェクトファイルを含める

   * FormsサービスのWSDLを使用するJavaプロキシクラスを作成します。
   * Javaプロキシクラスをクラスパスに含めます。

1. Forms Client APIオブジェクトの作成

   `FormsService`オブジェクトを作成し、認証値を設定します。

1. クライアントレンダリングの実行時オプションの設定

   * コンストラクタを使用して `PDFFormRenderSpec` オブジェクトを作成します。
   * `PDFFormRenderSpec`オブジェクトの`setRenderAtClient`メソッドを呼び出し、文字列値`RenderAtClient.Yes`を渡すことで、`RenderAtClient`ランタイムオプションを設定します。

1. クライアントでのフォームのレンダリング

   `FormsService`オブジェクトの`renderPDFForm`メソッドを呼び出し、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定するstring値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、必ず`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`のように完全なパスを指定してください。
   * フォームとマージするデータを含む`BLOB`オブジェクト。 データを結合しない場合は、`null`を渡します。 ([編集可能なレイアウトを使用したFormsの事前入力](/help/forms/developing/prepopulating-forms-flowable-layouts.md)を参照)。
   * クライアントでフォームをレンダリングするために必要な実行時オプションを格納する`PDFFormRenderSpec`オブジェクト。
   * Formsサービスに必要なURI値を含む`URLSpec`オブジェクト。
   * 添付ファイルを格納する`java.util.HashMap`オブジェクト。 これはオプションのパラメーターで、フォームにファイルを添付しない場合は`null`を指定できます。
   * メソッドで設定される空の`com.adobe.idp.services.holders.BLOBHolder`オブジェクト。 このパラメーターは、レンダリングされたPDFフォームを保存するために使用されます。
   * メソッドで設定される空の`javax.xml.rpc.holders.LongHolder`オブジェクト。 （この引数は、フォームのページ数を保存します）。
   * メソッドで設定される空の`javax.xml.rpc.holders.StringHolder`オブジェクト。 （この引数はロケール値を格納します）。
   * この操作の結果を格納する空の`com.adobe.idp.services.holders.FormsResultHolder`オブジェクト。

   `renderPDFForm`メソッドは、最後の引数値として渡される`com.adobe.idp.services.holders.FormsResultHolder`オブジェクトに、クライアントWebブラウザーに書き込む必要のあるフォームデータストリームを設定します。

1. フォームデータストリームをクライアントWebブラウザーに書き込む

   * `com.adobe.idp.services.holders.FormsResultHolder`オブジェクトの`value`データメンバーの値を取得して、`FormResult`オブジェクトを作成します。
   * `FormsResult`オブジェクトの`getOutputContent`メソッドを呼び出して、フォームデータを含む`BLOB`オブジェクトを作成します。
   * `getContentType`メソッドを呼び出して、`BLOB`オブジェクトのコンテンツタイプを取得します。
   * `setContentType`メソッドを呼び出し、`BLOB`オブジェクトのコンテンツタイプを渡すことで、`javax.servlet.http.HttpServletResponse`オブジェクトのコンテンツタイプを設定します。
   * `javax.servlet.http.HttpServletResponse`オブジェクトの`getOutputStream`メソッドを呼び出して、フォームデータストリームをクライアントWebブラウザーに書き込むための`javax.servlet.ServletOutputStream`オブジェクトを作成します。
   * バイト配列を作成し、`BLOB`オブジェクトの`getBinaryData`メソッドを呼び出してそれを設定します。 このタスクは、`FormsResult`オブジェクトの内容をバイト配列に割り当てます。
   * `javax.servlet.http.HttpServletResponse`オブジェクトの`write`メソッドを呼び出して、フォームデータストリームをクライアントWebブラウザーに送信します。 `write`メソッドにバイト配列を渡します。

**関連トピック**

[クライアントでのFormsのレンダリング](#rendering-forms-at-the-client)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
