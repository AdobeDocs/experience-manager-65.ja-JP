---
title: Forms サービスのパフォーマンスの最適化
seo-title: Optimizing the Performance of theForms Service
description: フォームのレンダリング時に実行時オプションを設定し、XDP ファイルをリポジトリに保存して、Formsサービスのパフォーマンスを最適化します。
seo-description: Set run-time options when rendering a form and store XDP files in the repository to optimize the performance of the Forms service.
uuid: 9040c09a-e5d0-432b-b1c5-ad46ab57c4fc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9f883483-b81e-42c6-a4a1-eb499dd112e7
role: Developer
exl-id: 5a746c6c-bf6e-4b25-ba7c-a35edb1f55f3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '1431'
ht-degree: 100%

---

# Forms サービスパフォーマンスの最適化 {#optimizing-the-performance-of-theforms-service}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

## Forms サービスパフォーマンスの最適化 {#optimizing-the-performance-of-the-forms-service}

フォームをレンダリングする際に、Forms サービスのパフォーマンスを最適化する実行時のオプションを設定できます。 Forms サービスのパフォーマンスを向上させるために実行できるもう 1 つのタスクは、XDP ファイルをリポジトリに格納することです。 ただし、この節では、このタスクの実行方法については説明しません。 （[Java クライアントライブラリを使用したサービスの呼び出し](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)を参照。）

>[!NOTE]
>
>AEM Forms サービスについて詳しくは、『[AEM Forms サービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)』を参照してください。

### 手順の概要 {#summary-of-steps}

フォームのレンダリング中に Forms サービスのパフォーマンスを最適化するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Forms Client API オブジェクトを作成します。
1. パフォーマンスの実行時オプションを設定します。
1. フォームをレンダリングします。
1. フォームデータストリームをクライアントの Web ブラウザーに書き込みます。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**Forms Client API オブジェクトの作成**

Forms Service Client API 操作をプログラムで実行する前に、Forms サービスクライアントを作成する必要があります。 Java API を使用している場合は、 `FormsServiceClient` オブジェクトを作成します。Forms Web サービス API を使用している場合は、 `FormsService` オブジェクトを作成します。

**パフォーマンスの実行時オプションを設定する**

次のパフォーマンス実行時オプションを設定して、Forms サービスのパフォーマンスを向上させることができます。

* **フォームのキャッシュ**：サーバーキャッシュ内で PDF としてレンダリングされるフォームをキャッシュできます。 各フォームは、初回生成後にキャッシュされます。それ以降のレンダリング時には、キャッシュされているフォームがフォームデザインのタイムスタンプよりも新しい場合、フォームはキャッシュから取得されます。フォームをキャッシュすると、リポジトリからフォームデザインを取得する必要がなくなるので、Forms サービスのパフォーマンスが向上します。
* フォームガイド（非推奨）は、他の変換タイプよりもレンダリングに時間がかかる場合があります。 パフォーマンスを向上させるために、フォームガイド（非推奨）をキャッシュすることをお勧めします。
* **スタンドアロンオプション**：Forms サービスでサーバーサイドの計算を実行する必要がない場合は、「スタンドアロン」オプションを `true` に設定すると、フォームは状態情報なしでレンダリングされます。 状態情報は、インタラクティブフォームをエンドユーザーにレンダリングし、そのユーザーがフォームに情報を入力して、そのフォームをFormsサービスに送り返す場合に必要です。 次に、Forms サービスは計算処理を実行し、フォームをレンダリングしてユーザーに戻し、結果がフォームに表示されます。フォームが状態情報なしで Forms サービスに送り返された場合、XML データのみが使用可能になり、サーバーサイドの計算は実行されません。
* **線形化された PDF**：線形化された PDF ドキュメントは、ネットワーク環境で効果的に増分アクセスできるよう整理されています。PDF ファイルは、あらゆる点で有効な PDF で、既存のすべてのビューアやその他の PDF アプリケーションと互換性があります。 つまり、線形化された PDF は、ダウンロード中に表示できます。
* このオプションを選択しても、クライアントで PDF フォームがレンダリングされる際のパフォーマンスは向上しません。
* **GuideRSL オプション**：実行時の共有ライブラリを使用して、フォームガイド（非推奨）の生成を有効にします。 つまり、最初のリクエストでは、小さい SWF ファイルと、ブラウザーのキャッシュに保存されている大きい共有ライブラリがダウンロードされます。 詳しくは、Flex ドキュメントの RSL を参照してください。
* また、クライアントでフォームをレンダリングして、Forms サービスのパフォーマンスを向上させることもできます。 （[クライアントでの Forms のレンダリング](/help/forms/developing/rendering-forms-client.md)を参照。）

**フォームをレンダリング**

パフォーマンスオプションを設定した後にフォームをレンダリングするには、パフォーマンスオプションを指定せずにフォームをレンダリングする場合と同じアプリケーションロジックを使用します。

**フォームデータストリームをクライアント web ブラウザーに書き込む**

Forms サービスがフォームをレンダリングすると、クライアントの Web ブラウザーに書き込む必要があるフォームデータストリームが返されます。 クライアント Web ブラウザーに書き込まれると、フォームはユーザーに対して表示されます。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms サービス API のクイックスタート](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[インタラクティブ PDF Forms のレンダリング](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Forms を HTML としてレンダリング](/help/forms/developing/rendering-forms-html.md)

[Forms をレンダリングする web アプリケーションの作成](/help/forms/developing/creating-web-applications-renders-forms.md)

### Java API を使用したパフォーマンスの最適化 {#optimize-the-performance-using-the-java-api}

Forms API（Java）を使用して、最適化されたパフォーマンスでフォームをレンダリングします。

1. プロジェクトファイルを含める

   adobe-forms-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. Forms Client API オブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * `FormsServiceClient` オブジェクトを作成するには、コンストラクターを使用して `ServiceClientFactory` オブジェクトを渡します。

1. パフォーマンスの実行時オプションの設定

   * コンストラクターを使用して `PDFFormRenderSpec` オブジェクトを作成します。
   * フォームキャッシュオプションを設定するには、`PDFFormRenderSpec` オブジェクトの `setCacheEnabled` メソッドを呼び出して、`true` を渡します。
   * 線形化オプションを設定するには、`PDFFormRenderSpec` オブジェクトの `setLinearizedPDF` メソッドを呼び出して、`true.` を渡します。

1. フォームのレンダリング

   `FormsServiceClient` オブジェクトの `renderPDFForm` メソッドを呼び出して、次の値を渡します。

   * ファイル名拡張子を含んだフォームデザイン名を指定する文字列値。
   * フォームに結合するデータを含む `com.adobe.idp.Document` オブジェクト。 データを結合しない場合は、空の `com.adobe.idp.Document` オブジェクトを渡します。
   * パフォーマンスを向上させるための実行時オプションを保存する `PDFFormRenderSpec` オブジェクト。
   * Forms サービスで必要な URI 値を格納する `URLSpec` オブジェクト。
   * 添付ファイルを保存する `java.util.HashMap` オブジェクト。 これはオプションのパラメーターで、フォームにファイルを添付しない場合 `null` を指定できます。

   この `renderPDFForm` メソッドは、クライアントの web ブラウザーに書き込む必要があるフォームデータストリームを含む `FormsResult` オブジェクトを返します。

1. フォームデータストリームをクライアント web ブラウザーに書き込む

   * フォームデータストリームをクライアントの web ブラウザーに送信するために使用する `javax.servlet.ServletOutputStream` オブジェクトを作成します。
   * `FormsResult` オブジェクトの `getOutputContent` メソッド呼び出して、`com.adobe.idp.Document` オブジェクトを作成します。
   * `com.adobe.idp.Document` オブジェクトの `getInputStream` メソッドを呼び出して、`java.io.InputStream` オブジェクトを作成します。
   * バイト配列を作成し、フォームデータストリームを入力するには、`InputStream` オブジェクトの `read` メソッドを呼び出して、バイト配列を引数として渡します。
   * `javax.servlet.ServletOutputStream` オブジェクトの `write` メソッドを呼び出して、フォームデータストリームをクライアント web ブラウザーに送信します。 バイト配列を `write` メソッドに渡します。

**関連トピック**

[クイックスタート（SOAP モード）：Java API を使用したパフォーマンスの最適化](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-optimizing-performance-using-the-java-api)

[AEM Forms Java ライブラリファイルの組み込み](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用したパフォーマンスの最適化 {#optimize-the-performance-using-the-web-service-api}

Forms API（web サービス）を使用して、最適化されたパフォーマンスでフォームをレンダリングします。

1. プロジェクトファイルを含める

   * Forms Service WSDL を使用する Java プロキシクラスを作成します。
   * Java プロキシクラスをクラスパスに含めます。

1. Forms Client API オブジェクトの作成

   `FormsService` オブジェクトを作成し、認証値を設定します。

1. パフォーマンスの実行時オプションの設定

   * コンストラクターを使用して `PDFFormRenderSpec` オブジェクトを作成します。
   * フォームキャッシュオプションを設定するには、`PDFFormRenderSpec` オブジェクトの `setCacheEnabled` メソッドを呼び出して、true を渡します。
   * スタンドアロンオプションを設定するには、`PDFFormRenderSpec` オブジェクトの `setStandAlone` メソッドを呼び出して、true を渡します。
   * 線形化オプションを設定するには、`PDFFormRenderSpec` オブジェクトの `setLinearizedPDF` メソッドを呼び出して、true を渡します。

1. フォームのレンダリング

   `FormsService` オブジェクトの `renderPDFForm` メソッドを呼び出し、次の値を渡します。

   * ファイル名拡張子を含んだフォームデザイン名を指定する文字列値。
   * フォームに結合するデータを含む `BLOB` オブジェクト。 データを結合しない場合は、`null` を渡します。
   * 実行時オプションを保存する `PDFFormRenderSpecc` オブジェクト。
   * Forms サービスで必要な URI 値を格納する `URLSpec` オブジェクト。
   * 添付ファイルを保存する `java.util.HashMap` オブジェクト。 これはオプションのパラメーターで、フォームにファイルを添付しない場合 `null` を指定できます。
   * メソッドによって設定される空の `com.adobe.idp.services.holders.BLOBHolder` オブジェクト。 これは、レンダリングされた PDF フォームを保存するために使用されます。
   * メソッドによって生成される空の `javax.xml.rpc.holders.LongHolder` オブジェクト。 （この引数は、フォームのページ数を保存します）。
   * メソッドによって設定される空の `javax.xml.rpc.holders.StringHolder` オブジェクト。 （この引数はロケール値を格納します）。
   * この操作の結果を格納する空の `com.adobe.idp.services.holders.FormsResultHolder` オブジェクト。

   この `renderPDFForm` メソッドによって、最後の引数値として渡される `com.adobe.idp.services.holders.FormsResultHolder` オブジェクトに、クライアント web ブラウザーに書き込む必要のあるフォームデータストリームが設定されます。

1. フォームデータストリームをクライアント web ブラウザーに書き込む

   * `com.adobe.idp.services.holders.FormsResultHolder` オブジェクトの `value` データメンバーの値を取得して、`FormResult` オブジェクトを作成します。
   * フォームデータストリームをクライアントの web ブラウザーに送信するために使用する `javax.servlet.ServletOutputStream` オブジェクトを作成します。
   * `FormsResult` オブジェクトの `getOutputContent` メソッドを呼び出して、フォームデータを含む `BLOB` オブジェクトを作成します。
   * `BLOB` オブジェクトの `getBinaryData` メソッドを呼び出すことによって、バイト配列を作成して設定します。このタスクは、`FormsResult` オブジェクトのコンテンツをバイト配列に変換します。
   *  `javax.servlet.http.HttpServletResponse` オブジェクトの `write` メソッドを呼び出して、フォームデータストリームをクライアント Web ブラウザーに送信します。 バイト配列を `write` メソッドに渡します。

**関連トピック**

[Base64 エンコーディングを使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
