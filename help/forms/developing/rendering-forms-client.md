---
title: クライアント側でのフォームのレンダリング
seo-title: Rendering Forms at the Client
description: Acrobat や Adobe Reader のクライアントサイドレンダリング機能を使用して、PDF コンテンツの配信を最適化し、Forms サービスのネットワーク負荷への対応力を向上させます。
seo-description: Optimize the delivery of PDF content and improve the Forms service’s ability to handle network load by using the client-side rendering capability of Acrobat or Adobe Reader
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
source-wordcount: '1698'
ht-degree: 100%

---

# クライアント側でのフォームのレンダリング {#rendering-forms-at-the-client}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

## クライアント側でのフォームのレンダリング {#rendering-forms-at-the-client-inner}

Acrobat や Adobe Reader のクライアントサイドレンダリング機能を利用して、PDF コンテンツの配信を最適化し、Forms サービスのネットワーク負荷への対応力を向上させることができます。この処理をクライアントでのレンダリングといいます。クライアントでフォームをレンダリングするには、クライアントデバイス（通常は web ブラウザー）が Acrobat 7.0 または Adobe Reader 7.0 以降を使用している必要があります。

サーバーサイドのスクリプト実行によるフォームの変更は、ルートサブフォームに `restoreState` 属性が `auto` に設定されていない限り、クライアントで表示されるフォームには反映されません。この属性の詳細情報については、[Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63_jp) を参照してください。

>[!NOTE]
>
>AEM Forms サービスについて詳しくは、[Forms 用サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

### 手順の概要 {#summary-of-steps}

クライアントでフォームをレンダリングするには、以下の作タスクを実行します。

1. プロジェクトファイルを含めます。
1. Forms Client API オブジェクトを作成します。
1. クライアントレンダリングの実行時オプションを設定します。
1. クライアントでフォームをレンダリングします。
1. クライアントの web ブラウザーにフォームを書き込みます。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**Forms Client API オブジェクトの作成**

Forms Service Client API 操作をプログラムで実行する前に、Forms サービスクライアントを作成する必要があります。 Java API を使用している場合は、`FormsServiceClient` オブジェクトを作成します。Forms web サービス API を使用している場合は、`FormsService`オブジェクトを作成してください。

**クライアントレンダリングの実行時オプションを設定**

クライアントでフォームをレンダリングするには、`RenderAtClient` 実行時オプションを `true` に設定することにより、クライアントレンダリングの実行時オプションを設定する必要があります。この結果、フォームがレンダリングされたクライアントデバイスに配信されます。`RenderAtClient` が `auto`（デフォルト値）の場合、フォームデザインがクライアントでレンダリングされるかどうかを決定します。編集可能なレイアウトを持つフォームデザインが要求されます。

設定可能な実行時オプションとして、`SeedPDF` オプションがあります。`SeedPDF` オプションは、PDF コンテナ（シード PDF ドキュメント）を、フォームデザインと XML データとに組み合わせます。フォームのデザインと XML データの両方が Acrobat または Adobe Reader に配信され、そこでフォームがレンダリングされます。`SeedPDF` オプションは、フォームで使用されているフォントをクライアントコンピュータが持っていない場合に使用できます。例えば、フォームの所有者が使用ライセンスを持っているフォントに対して、エンドユーザーが使用ライセンスを持っていない場合などです。

Designer を使用して、シード PDF ファイルとして使用するための、シンプルなダイナミック PDF ファイルを作成することができます。このタスクを行うには、以下の手順が必要です。

1. シード PDF ファイル内にフォントを埋め込む必要があるかどうかを判断します。シード PDF ファイルには、レンダリングするフォームに必要なフォントを追加する必要があります。シード PDF ファイルにフォントを埋め込む場合、フォントのライセンス契約に違反していないことを確認してください。Designer では、合法的にフォントを埋め込むことができるかどうかを判断することができます。保存時に、フォームに埋め込めないフォントがある場合、Designer は埋め込めないフォントのリストをメッセージで表示します。このメッセージは、静的な PDF ドキュメントの場合は Designer に表示されません。
1. Designer でシード PDF ファイルを作成する場合、最低限、メッセージを含むテキストフィールドを追加することを推奨します。Adobe Reader の旧バージョンを使用するユーザーに対しては、ドキュメントを表示するには Acrobat 7.0 以降、または Adobe Reader 7.0 以降が必要であることを示すメッセージが表示されます。
1. シード PDF ファイルを、PDF ファイル名の拡張子をつけてダイナミック PDF ファイルとして保存します。

>[!NOTE]
>
>クライアントでフォームをレンダリングするために、シード PDF 実行時オプションを定義する必要はありません。シード PDF を指定しない場合、Forms サービスは、COS オブジェクトを含まないシェル PDF を作成しますが、これは実際の XDP のコンテンツを内部に埋め込んだ PDF ラッパーを含んでいます。この節の手順では、シード PDF 実行時オプションは設定しません。COS オブジェクトについては、Adobe PDF リファレンスガイドを参照してください。

**クライアントでフォームをレンダリング**

クライアントでフォームをレンダリングするには、クライアントレンダリングの実行時オプションが、フォームをレンダリングするアプリケーションロジックに含まれていることを確認する必要があります。

**フォームデータストリームをクライアントの web ブラウザーに書き込む**

Forms サービスは、クライアントの web ブラウザーに書き込むフォームデータストリームを作成します。クライアントの web ブラウザーに書き込まれると、フォームは Acrobat 7.0 または Adobe Reader 7.0 以降でレンダリングされ、ユーザーに対して表示されます。

**関連トピック**

[Java API を使用したクライアントでのフォームのレンダリング](#render-a-form-at-the-client-using-the-java-api)

[Web サービス API を使用したクライアントでのフォームのレンダリング](#render-a-form-at-the-client-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms サービス API のクイックスタート](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Forms サービスにドキュメントを渡す](/help/forms/developing/passing-documents-forms-service.md)

[Forms をレンダリングする web アプリケーションの作成](/help/forms/developing/creating-web-applications-renders-forms.md)

### Java API を使用したクライアントでのフォームのレンダリング {#render-a-form-at-the-client-using-the-java-api}

Forms API (Java) を使用して、クライアントでフォームをレンダリングするには、以下の手順に従います。

1. プロジェクトファイルを含める

   adobe-forms-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. Forms Client API オブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して `ServiceClientFactory` オブジェクトを渡し、`FormsServiceClient` オブジェクトを作成します。

1. クライアントレンダリング実行時オプションを設定する

   * コンストラクタを使用して `PDFFormRenderSpec` オブジェクトを作成します。
   * `RenderAtClient` 実行時オプションを設定するには、`PDFFormRenderSpec` オブジェクトの `setRenderAtClient` メソッドを呼び出し、列挙値 `RenderAtClient.Yes` を渡します。

1. クライアントでフォームをレンダリングする

   `FormsServiceClient` オブジェクトの `renderPDFForm` メソッドを呼び出し、次の値を渡します。

   * フォームデザイン名を指定する文字列値で、ファイル名の拡張子も含まれます。AEM Forms アプリケーションの一部であるフォームデザインを参照する場合は、`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp` のように完全なパスを指定します。
   * フォームと統合するデータを含む `com.adobe.idp.Document` オブジェクトです。データを統合しない場合、空の `com.adobe.idp.Document` オブジェクトを渡します。
   * クライアントでフォームをレンダリングするために必要な実行時オプションを格納する `PDFFormRenderSpec` オブジェクトです。
   * フォームを表示するために Forms サービスが必要とする URI の値を含む `URLSpec` オブジェクトです。
   * 添付ファイルを保存する `java.util.HashMap` オブジェクトです。オプションのパラメーターです。フォームにファイルを添付しない場合は `null` を指定できます。

   `renderPDFForm` メソッドは、クライアントの Web ブラウザーに書き込む必要のあるフォームデータストリームを含む `FormsResult` オブジェクトを返します。

1. フォームデータストリームをクライアント web ブラウザーに書き込む

   * `FormsResult` オブジェクトの `getOutputContent` メソッドを呼び出して、`com.adobe.idp.Document` オブジェクトを作成します。
   * `getContentType` メソッドを呼び出して、`com.adobe.idp.Document` オブジェクトのコンテンツタイプを取得します。
   * `javax.servlet.http.HttpServletResponse` オブジェクトのコンテンツタイプを設定するには、`setContentType` メソッドを呼び出して、`com.adobe.idp.Document` オブジェクトのコンテンツタイプを渡します。
   * `javax.servlet.http.HttpServletResponse` オブジェクトの `getOutputStream` メソッドを呼び出して、フォームデータストリームをクライアント web ブラウザーに書き込むために使用される `javax.servlet.ServletOutputStream` オブジェクトを作成します。
   * `com.adobe.idp.Document` オブジェクトの `getInputStream` メソッドを呼び出すことによって `java.io.InputStream` オブジェクトを作成します。
   * `InputStream` オブジェクトの `read` メソッドを呼び出してバイト配列を引数として渡すことによって、バイト配列を作成してフォームデータストリームを入力します。
   * `javax.servlet.ServletOutputStream` オブジェクトの `write` メソッドを呼び出して、フォームデータストリームをクライアント web ブラウザーに送信します。バイト配列を `write` メソッドに渡します。

**関連トピック**

[クイックスタート（SOAP モード）：Java API を使ったクライアントでのフォームのレンダリング](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-at-the-client-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用したクライアントでのフォームのレンダリング {#render-a-form-at-the-client-using-the-web-service-api}

Forms API（Webサービス）を使用して、クライアントでフォームをレンダリングするには：

1. プロジェクトファイルを含める

   * Forms Service WSDL を使用する Java プロキシクラスを作成します。
   * Java プロキシクラスをクラスパスに含めます。

1. Forms Client API オブジェクトの作成

   `FormsService` オブジェクトを作成して、認証値を設定します。

1. クライアントレンダリング実行時オプションを設定する

   * コンストラクタを使用して `PDFFormRenderSpec` オブジェクトを作成します。
   * `RenderAtClient` 実行時オプションを設定するには、`PDFFormRenderSpec` オブジェクトの `setRenderAtClient` メソッドを呼び出し、文字列値 `RenderAtClient.Yes` を渡します。

1. クライアントでフォームをレンダリングする

   `FormsService` オブジェクトの `renderPDFForm` メソッドを呼び出し、次の値を渡します。

   * フォームデザイン名を指定する文字列値で、ファイル名の拡張子も含まれます。Forms アプリケーションの一部であるフォームデザインを参照する場合は、必ず次のような完全なパスを指定してください。`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`
   * フォームと結合するデータを含む `BLOB` オブジェクトです。データを結合しない場合は、`null` を渡します。（[流動レイアウトによるフォームの事前入力](/help/forms/developing/prepopulating-forms-flowable-layouts.md)を参照してください）。
   * クライアントでフォームのレンダリングに必要な実行時オプションを格納する `PDFFormRenderSpec` オブジェクトです。
   * Forms サービスで必要とされる URI 値を含む `URLSpec` オブジェクトです。
   * 添付ファイルを保存する `java.util.HashMap` オブジェクト。 これはオプションのパラメーターで、 フォームにファイルを添付しない場合に、`null`を指定します。
   * メソッドによって入力される空の `com.adobe.idp.services.holders.BLOBHolder` オブジェクトです。このパラメーターは、レンダリングされた PDF フォームを格納するために使用されます。
   * メソッドによって入力される空の `javax.xml.rpc.holders.LongHolder` オブジェクトです。（この引数は、フォームのページ数を保存します）。
   * メソッドによって設定される空の `javax.xml.rpc.holders.StringHolder` オブジェクト。（この引数はロケール値を格納します）。
   * この操作の結果を格納する空の `com.adobe.idp.services.holders.FormsResultHolder` オブジェクト。

   `renderPDFForm` メソッドは、最後の引数値として渡される `com.adobe.idp.services.holders.FormsResultHolder` オブジェクトに、クライアント web ブラウザーに書き込む必要のあるフォームデータストリームを入力します。

1. フォームデータストリームをクライアント web ブラウザーに書き込む

   * `com.adobe.idp.services.holders.FormsResultHolder` オブジェクトの `value` データメンバーの値を取得して、`FormResult` オブジェクトを作成します。
   * `FormsResult` オブジェクトの `getOutputContent` メソッドを呼び出して、フォームデータを含む `BLOB` オブジェクトを作成します。
   * `getContentType` メソッドを呼び出して、`BLOB` オブジェクトのコンテンツタイプを取得します。
   * `javax.servlet.http.HttpServletResponse` オブジェクトのコンテンツタイプを設定するには、`setContentType` メソッドを呼び出して、`BLOB` オブジェクトのコンテンツタイプを渡します。
   * `javax.servlet.http.HttpServletResponse` オブジェクトの `getOutputStream` メソッドを呼び出して、フォームデータストリームをクライアント web ブラウザーに書き込むために使用される `javax.servlet.ServletOutputStream` オブジェクトを作成します。
   * バイト配列を作成し、`BLOB` オブジェクトの `getBinaryData` メソッドを呼び出して入力します。このタスクは、`FormsResult` オブジェクトのコンテンツをバイト配列に割り当てます。
   * `javax.servlet.http.HttpServletResponse` オブジェクトの `write` メソッドを呼び出して、フォームデータストリームをクライアント web ブラウザーに送信します。バイト配列を `write` メソッドに渡します。

**関連トピック**

[クライアント側でのフォームのレンダリング](#rendering-forms-at-the-client)

[Base64 エンコーディングを使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
