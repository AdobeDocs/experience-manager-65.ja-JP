---
title: 断片に基づくFormsのレンダリング
seo-title: 断片に基づくFormsのレンダリング
description: 'null'
seo-description: 'null'
uuid: 9c9a730d-f970-41f8-afed-4e6b6d3d393d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: a65c5303-0ebd-43a9-a777-401042d8fcad
translation-type: tm+mt
source-git-commit: 413af4ef9bc3652e05da78d622183bcf20a8bee7
workflow-type: tm+mt
source-wordcount: '2187'
ht-degree: 9%

---


# Rendering Forms Based on Fragments {#rendering-forms-based-on-fragments}

## Rendering Forms Based on Fragments {#rendering-forms-based-on-fragments-inner}

Formsサービスは、Designerを使用して作成したフラグメントに基づくフォームをレンダリングできます。 フ *ラグメント* はフォームの再利用可能な部分で、複数のフォームデザインに挿入できる独立したXDPファイルとして保存されます。 例えば、フラグメントには住所ブロックや法律文を含めることができます。

フラグメントの使用により、大量のフォームの作成とメンテナンスを簡単に、短時間で実行できます。新しいフォームを作成する場合は、必要なフラグメントへの参照を挿入すると、そのフラグメントがフォームに表示されます。 フラグメント参照には、物理 XDP ファイルを指すサブフォームが含まれます。フラグメントを基にしたフォームデザインの作成について詳しくは、 [Formsデザイナーを参照してください](https://www.adobe.com/go/learn_aemforms_designer_63)

フラグメントには、選択サブフォームセットに含めるサブフォームを複数含めることができます。 選択サブフォームセットは、データ接続からのデータのフローに基づいてサブフォームの表示を制御します。 条件ステートメントを使用して、配信するフォームに表示するサブフォームをそのセットから指定します。例えば、セット内の各サブフォームには特定の地理的な場所に関する情報を含めることができ、表示されるサブフォームはユーザーの場所に基づいて決定できます。

A *script fragment* contains reusable JavaScript functions or values that are stored separately from any particular object, such as a date parser or a web service invocation. このようなフラグメントには、階層パレットに変数の子として表示される単独のスクリプトオブジェクトがあります。フラグメントは、他のオブジェクトのプロパティとなっているスクリプトからは作成できません。このようなスクリプトとして、検証、計算、初期化などのイベントスクリプトがあります。

フラグメントを使用する利点は次のとおりです。

* **コンテンツの再利用**:フラグメントを使用すると、複数のフォームデザインでコンテンツを再利用できます。 複数のフォームで同じコンテンツの一部を使用する必要がある場合は、コンテンツをコピーまたは再作成するよりも、フラグメントを使用する方が高速で簡単です。 フラグメントを使用し、それをフォームで参照することで、フォームデザインの中で頻繁に使用する部分を一貫性のあるコンテンツと外観ですべてのフォームに表示できます。
* **グローバルな更新**:フラグメントを使用すると、1つのファイルで複数のフォームに1回だけグローバルな変更を行うことができます。 フラグメント内のコンテンツ、スクリプトオブジェクト、データ連結、レイアウトまたはスタイルを変更すると、そのフラグメントを参照するすべてのXDPフォームに変更が反映されます。
* 例えば、多くのフォームで共通する要素は、国のコンボボックスリストオブジェクトを含む住所ブロックなどです。 コンボボックスリストオブジェクトの値を更新する必要がある場合は、多数のフォームを開いて変更する必要があります。 フラグメントに住所ブロックを含める場合は、フラグメントファイルを1つ開くだけで変更できます。
* PDFフォーム内のフラグメントを更新するには、Designerでフォームを再度保存する必要があります。
* **共有フォームの作成**:フラグメントを使用すると、複数のリソースでフォームの作成を共有できます。 スクリプトまたは Designer のその他の高度な機能に精通しているフォーム開発者は、スクリプトまたは動的プロパティを活用するフラグメントを作成、共有することができます。フォーム作成者がこれらのフラグメントを使用してフォームデザインをレイアウトすれば、複数の担当者が作成した複数のフォームの各部分で一貫性のある外観と機能を実現できます。

### フラグメントを使用して組み立てたフォームデザインのアセンブリ {#assembling-a-form-design-assembled-using-fragments}

複数のフラグメントを基にしてFormsサービスに渡すフォームデザインをアセンブルできます。 複数のフラグメントをアセンブリするには、Assemblerサービスを使用します。 Assembleサービスを使用して、他のFormsサービス（Outputサービス）で使用されるフォームデザインを作成する例については、「フラグメントを使用したPDFドキュメントの [作成](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments)」を参照してください。 Outputサービスを使用する代わりに、Formsサービスを使用して同じワークフローを実行できます。

Assemblerサービスを使用する場合、フラグメントを使用してアセンブルされたフォームデザインを渡します。 作成されたフォームデザインは、他のフラグメントを参照していません。 これに対し、このトピックでは、他のフラグメントを参照するフォームデザインをFormsサービスに渡す方法について説明します。 ただし、フォームデザインはAssemblerでアセンブルされていません。 Designerで作成されました。

>[!NOTE]
>
>For more information about the Forms service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>フラグメントに基づいてフォームをレンダリングするWebベースのアプリケーションの作成について詳しくは、「FormsをレンダリングするWeb アプリケーションの [作成](/help/forms/developing/creating-web-applications-renders-forms.md)」を参照してください。

### 手順の概要 {#summary-of-steps}

フラグメントに基づいてフォームをレンダリングするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. FormsクライアントAPIオブジェクトを作成します。
1. URI値を指定します。
1. フォームをレンダリングします。
1. フォームデータストリームをクライアントのWebブラウザーに書き込みます。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めてください。

**FormsクライアントAPIオブジェクトの作成**

プログラムでFormsサービスのクライアントAPI操作を実行する前に、Formsサービスクライアントを作成する必要があります。

**URI値の指定**

フラグメントに基づいてフォームを正しくレンダリングするには、Formsサービスがフォームと、フォームデザインが参照するフラグメント（XDPファイル）の両方を見つけられることを確認する必要があります。 例えば、フォームの名前がPO.xdpで、このフォームでFooterUS.xdpとFooterCanada.xdpの2つのフラグメントを使用しているとします。 この場合、Formsサービスは3つのXDPファイルをすべて検索できる必要があります。

フォームとそのフラグメントを整理するには、フォームを1つの場所に配置し、別の場所に配置します。または、すべてのXDPファイルを同じ場所に配置します。 この節の目的上、すべてのXDPファイルがAEM Formsリポジトリにあると仮定します。 XDPファイルのAEM Formsリポジトリへの配置に関する詳細は、「リソースの [書き込み](/help/forms/developing/aem-forms-repository.md#writing-resources)」を参照してください。

フラグメントに基づいてフォームをレンダリングする場合は、フォーム自体のみを参照し、フラグメントは参照しません。 例えば、FooterUS.xdpやFooterCanada.xdpではなくPO.xdpを参照する必要があります。 フラグメントは、Formsサービスが見つけられる場所に配置してください。

**フォームのレンダリング**

フラグメントに基づくフォームは、フラグメント化されていないフォームと同じ方法でレンダリングできます。 つまり、フォームをPDF、HTML、またはフォームガイド（非推奨）としてレンダリングできます。 この節の例では、フラグメントに基づくフォームをインタラクティブPDFフォームとしてレンダリングします。 (インタラクティブPDF formsの [レンダリングを参照](/help/forms/developing/rendering-interactive-pdf-forms.md))。

**フォームデータストリームをクライアントのWebブラウザーに書き込みます**

Formsサービスはフォームをレンダリングすると、フォームデータストリームを返します。このストリームをクライアントのWebブラウザーに書き込む必要があります。 クライアントのWebブラウザーに書き込まれると、フォームはユーザーに表示されます。

**関連トピック**

[Java APIを使用したフラグメントに基づくフォームのレンダリング](#render-forms-based-on-fragments-using-the-java-api)

[WebサービスAPIを使用してフラグメントに基づいてフォームをレンダリングする](#render-forms-based-on-fragments-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[FormsサービスAPIクイック開始](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[インタラクティブPDF formsのレンダリング](/help/forms/developing/rendering-interactive-pdf-forms.md)

[FormsをレンダリングするWeb アプリケーションの作成](/help/forms/developing/creating-web-applications-renders-forms.md)

### Java APIを使用したフラグメントに基づくフォームのレンダリング {#render-forms-based-on-fragments-using-the-java-api}

FormsAPI(Java)を使用してフラグメントに基づいてフォームをレンダリングする：

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-forms-client.jarなどのクライアントJARファイルを含めます。

1. FormsクライアントAPIオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `FormsServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. URI値の指定

   * コンストラクターを使用して、URI値を格納する `URLSpec` オブジェクトを作成します。
   * オブジェクトの `URLSpec``setApplicationWebRoot` メソッドを呼び出し、アプリケーションのWebルートを表すstring値を渡します。
   * オブ `URLSpec` ジェクトの `setContentRootURI` メソッドを呼び出し、コンテンツルートURI値を指定するstring値を渡します。 フォームデザインとフラグメントがコンテンツルートURI内にあることを確認します。 そうでない場合、Formsサービスは例外をスローします。 リポジトリを参照するには、を指定し `repository://`ます。
   * オブジェクトの `URLSpec``setTargetURL` メソッドを呼び出し、フォームデータのポスト先のターゲットURL値を指定するstring値を渡します。 フォームデザインでターゲットURLを定義する場合は、空の文字列を渡すことができます。 演算を実行するために、フォームの送信先URLを指定することもできます。

1. フォームのレンダリング

   オブジェクトの `FormsServiceClient``renderPDFForm` メソッドを呼び出し、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定するstring値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、完全なパスを必ず指定してください（例：） `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * フォームとマージするデータを含む `com.adobe.idp.Document` オブジェクト。 データをマージしない場合は、空の `com.adobe.idp.Document` オブジェクトを渡します。
   * 実行時オプションを格納する `PDFFormRenderSpec` オブジェクト。
   * フラグメントに基づいてフォームをレンダリングするためにFormsサービスで必要なURI値を含む `URLSpec` オブジェクトです。
   * 添付ファイルを格納する `java.util.HashMap` オブジェクトです。 これはオプションのパラメーターで、フォームにファイルを添付しない `null` かどうかを指定できます。

   この `renderPDFForm``FormsResult` メソッドは、クライアントのWebブラウザーに書き込む必要があるフォームデータストリームを含むオブジェクトを返します。

1. フォームデータストリームをクライアントのWebブラウザーに書き込みます

   * オブジェクトの `com.adobe.idp.Document` メソッドを呼び出して、 `FormsResult` オブジェクトを作成し `getOutputContent` ます。
   * メソッドを呼び出して、 `com.adobe.idp.Document` オブジェクトのコンテンツタイプを取得し `getContentType` ます。
   * メソッドを呼び出し、オブジェクトの `javax.servlet.http.HttpServletResponse` コンテンツタイプを渡すことで、 `setContentType``com.adobe.idp.Document` オブジェクトのコンテンツタイプを設定します。
   * オブジェクトの `javax.servlet.ServletOutputStream` メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに書き込むために使用する `javax.servlet.http.HttpServletResponse``getOutputStream` オブジェクトを作成します。
   * オブジェクトの `java.io.InputStream` メソッドを呼び出して、 `com.adobe.idp.Document` オブジェクトを作成 `getInputStream` します。
   * オブジェクトの `InputStream``read`メソッドを呼び出し、バイト配列を引数として渡すことで、バイト配列を作成し、フォームデータストリームと共に値を入力します。
   * オブジェクトの `javax.servlet.ServletOutputStream``write` メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに送信します。 バイト配列を `write` メソッドに渡します。

**関連トピック**

[断片に基づくFormsのレンダリング](#rendering-forms-based-on-fragments)

[クイック開始（SOAPモード）:Java APIを使用したフラグメントに基づくフォームのレンダリング](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-based-on-fragments-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用してフラグメントに基づいてフォームをレンダリングする {#render-forms-based-on-fragments-using-the-web-service-api}

FormsAPI（Webサービス）を使用してフラグメントに基づいてフォームをレンダリングするには：

1. プロジェクトファイルを含める

   * FormsサービスのWSDLを使用するJavaプロキシクラスを作成します。
   * クラスパスにJavaプロキシクラスを含めます。

1. FormsクライアントAPIオブジェクトの作成

   オブジェクトを作成し、認証値を設定し `FormsService` ます。

1. URI値の指定

   * コンストラクターを使用して、URI値を格納する `URLSpec` オブジェクトを作成します。
   * オブジェクトの `URLSpec``setApplicationWebRoot` メソッドを呼び出し、アプリケーションのWebルートを表すstring値を渡します。
   * オブ `URLSpec` ジェクトの `setContentRootURI` メソッドを呼び出し、コンテンツルートURI値を指定するstring値を渡します。 フォームデザインがコンテンツルートURI内にあることを確認します。 そうでない場合、Formsサービスは例外をスローします。 リポジトリを参照するには、を指定し `repository://`ます。
   * オブジェクトの `URLSpec``setTargetURL` メソッドを呼び出し、フォームデータのポスト先のターゲットURL値を指定するstring値を渡します。 フォームデザインでターゲットURLを定義する場合は、空の文字列を渡すことができます。 演算を実行するために、フォームの送信先URLを指定することもできます。

1. フォームのレンダリング

   オブジェクトの `FormsService``renderPDFForm` メソッドを呼び出し、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定するstring値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、完全なパスを必ず指定してください（例：） `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * フォームとマージするデータを含む `BLOB` オブジェクト。 データを結合したくない場合は、を渡し `null`ます。
   * 実行時オプションを格納する `PDFFormRenderSpec` オブジェクト。 タグ付きPDFオプションは、入力ドキュメントがPDFドキュメントの場合は設定できません。 入力ファイルがXDPファイルの場合は、タグ付きPDFオプションを設定できます。
   * Formsサービスで必要なURI値を含む `URLSpec` オブジェクトです。
   * 添付ファイルを格納する `java.util.HashMap` オブジェクトです。 これはオプションのパラメーターで、フォームにファイルを添付しない `null` かどうかを指定できます。
   * メソッドによって入力される空の `com.adobe.idp.services.holders.BLOBHolder` オブジェクトです。 このパラメーターは、レンダリングされたフォームを保存するために使用します。
   * メソッドによって入力される空の `javax.xml.rpc.holders.LongHolder` オブジェクトです。 この引数は、フォームのページ数を格納します。
   * メソッドによって入力される空の `javax.xml.rpc.holders.StringHolder` オブジェクトです。 この引数はロケールの値を格納します。
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

[断片に基づくFormsのレンダリング](#rendering-forms-based-on-fragments)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
