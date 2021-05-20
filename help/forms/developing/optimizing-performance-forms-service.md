---
title: Formsサービスのパフォーマンスの最適化
seo-title: Formsサービスのパフォーマンスの最適化
description: フォームのレンダリング時にランタイムオプションを設定し、XDPファイルをリポジトリに格納して、Formsサービスのパフォーマンスを最適化します。
seo-description: フォームのレンダリング時にランタイムオプションを設定し、XDPファイルをリポジトリに格納して、Formsサービスのパフォーマンスを最適化します。
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
workflow-type: tm+mt
source-wordcount: '1459'
ht-degree: 6%

---

# Formsサービスのパフォーマンスの最適化{#optimizing-the-performance-of-theforms-service}

**このドキュメントのサンプルと例は、JEE上のAEM Forms環境に限られています。**

## Formsサービスのパフォーマンスの最適化{#optimizing-the-performance-of-the-forms-service}

フォームをレンダリングする際に、Formsサービスのパフォーマンスを最適化する実行時オプションを設定できます。 Formsサービスのパフォーマンスを向上させるために実行できるもう1つのタスクは、XDPファイルをリポジトリに保存することです。 ただし、この節では、このタスクの実行方法については説明しません。 （[Javaクライアントライブラリ](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-service-using-a-java-client-library)を使用したサービスの呼び出しを参照）。

>[!NOTE]
>
>Formsサービスについて詳しくは、『 AEM Formsのサービスリファレンス[ 』を参照してください。](https://www.adobe.com/go/learn_aemforms_services_63)

### 手順の概要{#summary-of-steps}

フォームのレンダリング中にFormsサービスのパフォーマンスを最適化するには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Forms Client APIオブジェクトを作成します。
1. パフォーマンスの実行時オプションを設定します。
1. フォームをレンダリングします。
1. フォームデータストリームをクライアントWebブラウザーに書き込みます。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用する場合は、プロキシファイルを必ず含めてください。

**Forms Client APIオブジェクトの作成**

FormsサービスクライアントAPI操作をプログラムで実行する前に、Formsサービスクライアントを作成する必要があります。 Java APIを使用している場合は、`FormsServiceClient`オブジェクトを作成します。 Forms WebサービスAPIを使用している場合は、`FormsService`オブジェクトを作成します。

**パフォーマンスの実行時オプションの設定**

次のパフォーマンスランタイムオプションを設定して、Formsサービスのパフォーマンスを向上させることができます。

* **フォームキャッシュ**:PDFとしてサーバーキャッシュにレンダリングされるフォームをキャッシュできます。各フォームは、初回生成後にキャッシュされます。それ以降のレンダリング時には、キャッシュされているフォームがフォームデザインのタイムスタンプよりも新しい場合、フォームはキャッシュから取得されます。フォームをキャッシュすると、リポジトリからフォームデザインを取得する必要がなくなるので、Formsサービスのパフォーマンスが向上します。
* フォームガイド（非推奨）は、他の変換タイプよりもレンダリングに時間がかかる場合があります。 パフォーマンスを向上させるために、フォームガイド（非推奨）をキャッシュすることをお勧めします。
* **スタンドアロンオプション**:Formsサービスでサーバー側の計算を実行する必要がない場合は、「スタンドアロン」オプションをに設定すると、フォームが状態情報なしでレンダリングされま `true`す。状態情報は、インタラクティブフォームをエンドユーザーにレンダリングし、そのユーザーがフォームに情報を入力してフォームをFormsサービスに送り返す場合に必要です。 次に、Forms サービスは計算処理を実行し、フォームをレンダリングしてユーザーに戻し、結果がフォームに表示されます。状態情報のないフォームがFormsサービスに送信されると、XMLデータのみが使用可能になり、サーバー側の計算は実行されません。
* **線形化PDF**:線形化されたPDFファイルは、ネットワーク環境での効率的な増分アクセスを可能にするように編成されます。PDFファイルは、あらゆる点で有効なPDFで、既存のすべてのビューアやその他のPDFアプリケーションと互換性があります。 つまり、線形化されたPDFは、ダウンロード中に表示できます。
* このオプションを選択しても、PDFフォームがクライアントでレンダリングされる際のパフォーマンスは向上しません。
* **GuideRSLオプション**:実行時の共有ライブラリを使用して、フォームガイド（非推奨）の生成を有効にします。つまり、最初のリクエストでは、小さなSWFファイルと、ブラウザーのキャッシュに保存される大きな共有ライブラリがダウンロードされます。 詳しくは、 FlexのドキュメントのRSLを参照してください。
* また、クライアントでフォームをレンダリングすることで、Formsサービスのパフォーマンスを向上させることもできます。 ([クライアントでのFormsのレンダリング](/help/forms/developing/rendering-forms-client.md)を参照)。

**フォームのレンダリング**

パフォーマンスオプションを設定した後にフォームをレンダリングするには、パフォーマンスオプションを指定せずにフォームをレンダリングする場合と同じアプリケーションロジックを使用します。

**フォームデータストリームをクライアントWebブラウザーに書き込む**

Formsサービスは、フォームをレンダリングした後、クライアントのWebブラウザーに書き込む必要があるフォームデータストリームを返します。 クライアントのWebブラウザーに書き込まれると、フォームはユーザーに表示されます。

**関連トピック**

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[FormsサービスAPIのクイックスタート](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[インタラクティブPDF formsのレンダリング](/help/forms/developing/rendering-interactive-pdf-forms.md)

[FormsをHTMLとしてレンダリング](/help/forms/developing/rendering-forms-html.md)

[Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Java API {#optimize-the-performance-using-the-java-api}を使用してパフォーマンスを最適化します。

Forms API(Java)を使用して、最適化されたパフォーマンスでフォームをレンダリングします。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-forms-client.jarなどのクライアントJARファイルを含めます。

1. Forms Client APIオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して`FormsServiceClient`オブジェクトを渡し、`ServiceClientFactory`オブジェクトを作成します。

1. パフォーマンスの実行時オプションの設定

   * コンストラクタを使用して `PDFFormRenderSpec` オブジェクトを作成します。
   * `PDFFormRenderSpec`オブジェクトの`setCacheEnabled`メソッドを呼び出して`true`を渡すことで、フォームキャッシュオプションを設定します。
   * `PDFFormRenderSpec`オブジェクトの`setLinearizedPDF`メソッドを呼び出し、`true.`を渡すことによって線形化オプションを設定します

1. フォームのレンダリング

   `FormsServiceClient`オブジェクトの`renderPDFForm`メソッドを呼び出し、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定するstring値。
   * フォームとマージするデータを含む`com.adobe.idp.Document`オブジェクト。 データを結合しない場合は、空の`com.adobe.idp.Document`オブジェクトを渡します。
   * パフォーマンスを向上させるために実行時オプションを格納する`PDFFormRenderSpec`オブジェクト。
   * Formsサービスに必要なURI値を含む`URLSpec`オブジェクト。
   * 添付ファイルを格納する`java.util.HashMap`オブジェクト。 これはオプションのパラメーターで、フォームにファイルを添付しない場合は`null`を指定できます。

   `renderPDFForm`メソッドは、クライアントのWebブラウザーに書き込む必要があるフォームデータストリームを含む`FormsResult`オブジェクトを返します。

1. フォームデータストリームをクライアントWebブラウザーに書き込む

   * フォームデータストリームをクライアントのWebブラウザーに送信するために使用する`javax.servlet.ServletOutputStream`オブジェクトを作成します。
   * `FormsResult`オブジェクトの`getOutputContent`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトを作成します。
   * `com.adobe.idp.Document`オブジェクトの`getInputStream`メソッドを呼び出して、`java.io.InputStream`オブジェクトを作成します。
   * `InputStream`オブジェクトの`read`メソッドを呼び出し、バイト配列を引数として渡すことで、バイト配列を作成し、フォームデータストリームに入力します。
   * `javax.servlet.ServletOutputStream`オブジェクトの`write`メソッドを呼び出して、フォームデータストリームをクライアントWebブラウザーに送信します。 `write`メソッドにバイト配列を渡します。

**関連トピック**

[クイックスタート（SOAPモード）:Java APIを使用したパフォーマンスの最適化](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-optimizing-performance-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#optimize-the-performance-using-the-web-service-api}を使用してパフォーマンスを最適化する

Forms API（Webサービス）を使用して、最適化されたパフォーマンスでフォームをレンダリングします。

1. プロジェクトファイルを含める

   * FormsサービスのWSDLを使用するJavaプロキシクラスを作成します。
   * Javaプロキシクラスをクラスパスに含めます。

1. Forms Client APIオブジェクトの作成

   `FormsService`オブジェクトを作成し、認証値を設定します。

1. パフォーマンスの実行時オプションの設定

   * コンストラクタを使用して `PDFFormRenderSpec` オブジェクトを作成します。
   * `PDFFormRenderSpec`オブジェクトの`setCacheEnabled`メソッドを呼び出し、trueを渡すことで、フォームキャッシュオプションを設定します。
   * `PDFFormRenderSpec`オブジェクトの`setStandAlone`メソッドを呼び出し、trueを渡すことで、スタンドアロンオプションを設定します。
   * `PDFFormRenderSpec`オブジェクトの`setLinearizedPDF`メソッドを呼び出し、trueを渡すことで、線形化オプションを設定します。

1. フォームのレンダリング

   `FormsService`オブジェクトの`renderPDFForm`メソッドを呼び出し、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定するstring値。
   * フォームとマージするデータを含む`BLOB`オブジェクト。 データを結合しない場合は、`null`を渡します。
   * 実行時オプションを格納する`PDFFormRenderSpecc`オブジェクト。
   * Formsサービスに必要なURI値を含む`URLSpec`オブジェクト。
   * 添付ファイルを格納する`java.util.HashMap`オブジェクト。 これはオプションのパラメーターで、フォームにファイルを添付しない場合は`null`を指定できます。
   * メソッドで設定される空の`com.adobe.idp.services.holders.BLOBHolder`オブジェクト。 これは、レンダリングされたPDFフォームを保存するために使用されます。
   * メソッドで設定される空の`javax.xml.rpc.holders.LongHolder`オブジェクト。 （この引数は、フォームのページ数を保存します）。
   * メソッドで設定される空の`javax.xml.rpc.holders.StringHolder`オブジェクト。 （この引数はロケール値を格納します）。
   * この操作の結果を格納する空の`com.adobe.idp.services.holders.FormsResultHolder`オブジェクト。

   `renderPDFForm`メソッドは、最後の引数値として渡される`com.adobe.idp.services.holders.FormsResultHolder`オブジェクトに、クライアントWebブラウザーに書き込む必要のあるフォームデータストリームを設定します。

1. フォームデータストリームをクライアントWebブラウザーに書き込む

   * `com.adobe.idp.services.holders.FormsResultHolder`オブジェクトの`value`データメンバーの値を取得して、`FormResult`オブジェクトを作成します。
   * フォームデータストリームをクライアントのWebブラウザーに送信するために使用する`javax.servlet.ServletOutputStream`オブジェクトを作成します。
   * `FormsResult`オブジェクトの`getOutputContent`メソッドを呼び出して、フォームデータを含む`BLOB`オブジェクトを作成します。
   * バイト配列を作成し、`BLOB`オブジェクトの`getBinaryData`メソッドを呼び出してそれを設定します。 このタスクは、`FormsResult`オブジェクトの内容をバイト配列に割り当てます。
   * `javax.servlet.http.HttpServletResponse`オブジェクトの`write`メソッドを呼び出して、フォームデータストリームをクライアントWebブラウザーに送信します。 `write`メソッドにバイト配列を渡します。

**関連トピック**

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
