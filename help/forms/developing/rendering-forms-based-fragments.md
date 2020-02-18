---
title: フラグメントに基づくフォームのレンダリング
seo-title: フラグメントに基づくフォームのレンダリング
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

---


# Rendering Forms Based on Fragments {#rendering-forms-based-on-fragments}

## Rendering Forms Based on Fragments {#rendering-forms-based-on-fragments-inner}

Formsサービスは、Designerを使用して作成したフラグメントに基づくフォームをレンダリングできます。 フラ *グメントは* 、フォームの再利用可能な部分で、複数のフォームデザインに挿入できる個別のXDPファイルとして保存されます。 例えば、フラグメントには住所ブロックや法律文を含めることができます。

フラグメントの使用により、大量のフォームの作成とメンテナンスを簡単に、短時間で実行できます。新しいフォームを作成する場合は、必要なフラグメントへの参照を挿入すると、そのフラグメントがフォームに表示されます。 フラグメント参照には、物理 XDP ファイルを指すサブフォームが含まれます。フラグメントに基づくフォームデザインの作成について詳しくは、「 [Forms Designer」を参照してください](https://www.adobe.com/go/learn_aemforms_designer_63)

フラグメントには、選択サブフォームセットに含める複数のサブフォームを含めることができます。 選択サブフォームセットは、データ接続からのデータのフローに基づいてサブフォームの表示を制御します。 条件ステートメントを使用して、配信するフォームに表示するサブフォームをそのセットから指定します。例えば、セット内の各サブフォームに特定の地理的な場所に関する情報を含めることができ、表示されるサブフォームはユーザーの場所に基づいて決定できます。

A *script fragment* contains reusable JavaScript functions or values that are stored separately from any particular object, such as a date parser or a web service invocation. このようなフラグメントには、階層パレットに変数の子として表示される単独のスクリプトオブジェクトがあります。フラグメントは、他のオブジェクトのプロパティとなっているスクリプトからは作成できません。このようなスクリプトとして、検証、計算、初期化などのイベントスクリプトがあります。

フラグメントを使用する利点は次のとおりです。

* **コンテンツの再利用**:フラグメントを使用して、複数のフォームデザインでコンテンツを再利用できます。 同じコンテンツの一部を複数のフォームで使用する必要がある場合は、コンテンツをコピーまたは再作成するよりも、フラグメントを使用する方が高速で簡単です。 フラグメントを使用し、それをフォームで参照することで、フォームデザインの中で頻繁に使用する部分を一貫性のあるコンテンツと外観ですべてのフォームに表示できます。
* **グローバルな更新**:フラグメントを使用して、1つのファイルで複数のフォームに対してグローバルな変更を行うことができます。 フラグメント内のコンテンツ、スクリプトオブジェクト、データ連結、レイアウトまたはスタイルを変更でき、そのフラグメントを参照するすべてのXDPフォームに変更が反映されます。
* 例えば、多くのフォームで共通する要素は、国のコンボボックスオブジェクトを含む住所ブロックです。 コンボボックスオブジェクトの値を更新する必要がある場合は、多数のフォームを開いて変更を加える必要があります。 フラグメントに住所ブロックを含める場合は、変更を行うために必要なフラグメントファイルを1つだけ開く必要があります。
* PDFフォーム内のフラグメントを更新するには、Designerでフォームを再度保存する必要があります。
* **共有フォームの作成**:フラグメントを使用して、複数のリソース間でフォームの作成を共有できます。 スクリプトまたは Designer のその他の高度な機能に精通しているフォーム開発者は、スクリプトまたは動的プロパティを活用するフラグメントを作成、共有することができます。フォーム作成者がこれらのフラグメントを使用してフォームデザインをレイアウトすれば、複数の担当者が作成した複数のフォームの各部分で一貫性のある外観と機能を実現できます。

### フラグメントを使用してアセンブリされたフォームデザインのアセンブリ {#assembling-a-form-design-assembled-using-fragments}

フォームデザインをアセンブリして、複数のフラグメントに基づいてFormsサービスに渡すことができます。 複数のフラグメントをアセンブリするには、Assemblerサービスを使用します。 Assembleサービスを使用して、別のFormsサービス（Outputサービス）で使用されるフォームデザインを作成する例については、「フラグメントを使用したPDFドキュメントの作成」を [参照してください](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments)。 Outputサービスを使用する代わりに、Formsサービスを使用して同じワークフローを実行できます。

Assemblerサービスを使用する場合、フラグメントを使用してアセンブリされたフォームデザインを渡します。 作成されたフォームデザインは、他のフラグメントを参照しません。 これに対し、このトピックでは、他のフラグメントを参照するフォームデザインをFormsサービスに渡す方法について説明します。 ただし、フォームデザインはAssemblerによってアセンブルされませんでした。 Designerで作成されました。

>[!NOTE]
>
>For more information about the Forms service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>フラグメントに基づいてフォームをレンダリングするWebベースのアプリケーションの作成について詳しくは、「フォームをレンダリングするWebア [プリケーションの作成」を参照してくださ](/help/forms/developing/creating-web-applications-renders-forms.md)い。

### 手順の概要 {#summary-of-steps}

フラグメントに基づいてフォームをレンダリングするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. フォームクライアントAPIオブジェクトを作成します。
1. URI値を指定します。
1. フォームをレンダリングします。
1. クライアントのWebブラウザーにフォームデータストリームを書き込みます。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

**フォームクライアントAPIオブジェクトの作成**

プログラムでFormsサービスのClient API操作を実行する前に、Formsサービスクライアントを作成する必要があります。

**URI値の指定**

フラグメントに基づいてフォームを正しくレンダリングするには、Formsサービスで、フォームデザインが参照するフラグメントとフラグメント（XDPファイル）の両方を見つけられることを確認する必要があります。 例えば、フォームの名前がPO.xdpで、このフォームでFooterUS.xdpとFooterCanada.xdpという2つのフラグメントを使用しているとします。 この場合、Formsサービスは3つのXDPファイルをすべて検索できる必要があります。

フォームとそのフラグメントは、フォームを別の場所に配置して整理することも、すべてのXDPファイルを同じ場所に配置することもできます。 この節の目的では、すべてのXDPファイルがAEM Formsリポジトリ内にあると仮定します。 XDPファイルをAEM Formsリポジトリに配置する方法について詳しくは、「リソースの書き込み」を参 [照してくださ](/help/forms/developing/aem-forms-repository.md#writing-resources)い。

フラグメントに基づいてフォームをレンダリングする場合は、フォーム自体のみを参照し、フラグメントは参照しないでください。 例えば、FooterUS.xdpやFooterCanada.xdpではなくPO.xdpを参照する必要があります。 フラグメントは、Formsサービスが見つけられる場所に配置してください。

**フォームのレンダリング**

フラグメントに基づくフォームは、フラグメント化されていないフォームと同じ方法でレンダリングできます。 つまり、フォームをPDF、HTMLまたはフォームガイド（非推奨）としてレンダリングできます。 この節の例では、フラグメントに基づくフォームをインタラクティブPDFフォームとしてレンダリングします。 (インタラクティブPDF [フォームのレンダリングを参照](/help/forms/developing/rendering-interactive-pdf-forms.md))。

**クライアントのWebブラウザーにフォームデータストリームを書き込みます**

Formsサービスは、フォームをレンダリングすると、クライアントのWebブラウザーに書き込む必要があるフォームデータストリームを返します。 クライアントのWebブラウザーに書き込むと、フォームがユーザーに表示されます。

**関連トピック**

[Java APIを使用したフラグメントに基づくフォームのレンダリング](#render-forms-based-on-fragments-using-the-java-api)

[WebサービスAPIを使用してフラグメントに基づいてフォームをレンダリングする](#render-forms-based-on-fragments-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[FormsサービスAPIのクイックスタート](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[インタラクティブPDFフォームのレンダリング](/help/forms/developing/rendering-interactive-pdf-forms.md)

[フォームをレンダリングするWebアプリケーションの作成](/help/forms/developing/creating-web-applications-renders-forms.md)

### Java APIを使用したフラグメントに基づくフォームのレンダリング {#render-forms-based-on-fragments-using-the-java-api}

Forms API(Java)を使用して、フラグメントに基づいてフォームをレンダリングします。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-forms-client.jarなどのクライアントJARファイルを含めます。

1. フォームクライアントAPIオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `FormsServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. URI値の指定

   * コンストラク `URLSpec` ターを使用して、URI値を格納するオブジェクトを作成します。
   * オブジェクト `URLSpec` のメソッドを `setApplicationWebRoot` 呼び出し、アプリケーションのWebルートを表すstring値を渡します。
   * オブジェクト `URLSpec` のメソッドを `setContentRootURI` 呼び出し、コンテンツルートURI値を指定するstring値を渡します。 フォームデザインとフラグメントがコンテンツルートURIに配置されていることを確認します。 そうでない場合、Formsサービスは例外をスローします。 リポジトリを参照するには、を指定しま `repository://`す。
   * オブジェクト `URLSpec` のメソッ `setTargetURL` ドを呼び出し、フォームデータの投稿先のターゲットURL値を指定するstring値を渡します。 フォームデザインでターゲットURLを定義する場合は、空の文字列を渡すことができます。 演算を実行するためにフォームの送信先URLを指定することもできます。

1. フォームのレンダリング

   オブジェクト `FormsServiceClient` のメソッドを `renderPDFForm` 呼び出し、次の値を渡します。

   * ファイル名の拡張子を含むフォームデザイン名を指定するstring値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、必ずなどの完全なパスを指定してくださ `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`い。
   * フォーム `com.adobe.idp.Document` とマージするデータを含むオブジェクトです。 データをマージしない場合は、空のオブジェクトを渡し `com.adobe.idp.Document` ます。
   * 実行時 `PDFFormRenderSpec` のオプションを格納するオブジェクトです。
   * Formsサ `URLSpec` ービスがフラグメントに基づいてフォームをレンダリングするために必要なURI値を含むオブジェクトです。
   * 添付フ `java.util.HashMap` ァイルを格納するオブジェクト。 これはオプションのパラメーターで、フォームにフ `null` ァイルを添付しないかどうかを指定できます。
   このメソ `renderPDFForm` ッドは、クライア `FormsResult` ントのWebブラウザーに書き込む必要があるフォームデータストリームを含むオブジェクトを返します。

1. クライアントのWebブラウザーにフォームデータストリームを書き込みます

   * オブジェクトの `com.adobe.idp.Document` メソッドを呼び出して、オ `FormsResult` ブジェクトを作成 `getOutputContent` します。
   * メソッドを呼び出して、オブジェ `com.adobe.idp.Document` クトのコンテンツタイプを取得 `getContentType` します。
   * メソッドを呼 `javax.servlet.http.HttpServletResponse` び出し、オブジェクトのコンテンツタ `setContentType` イプを渡すことで、オブジェクトのコンテンツタイプを設定 `com.adobe.idp.Document` します。
   * オブジェクトの `javax.servlet.ServletOutputStream` メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに書き込むために使用する `javax.servlet.http.HttpServletResponse` オブジェクトを作 `getOutputStream` 成します。
   * オブジェクト `java.io.InputStream` のメソッドを呼び出して、オ `com.adobe.idp.Document` ブジェクトを作成 `getInputStream` します。
   * バイト配列を作成し、オブジェクトのメソッドを呼び出し、バイト配列を引 `InputStream` 数として渡すこ `read`とによって、フォームデータストリームを設定します。
   * オブジェクト `javax.servlet.ServletOutputStream` のメソッドを呼び `write` 出して、フォームデータストリームをクライアントWebブラウザーに送信します。 バイト配列をメソッドに渡し `write` ます。

**関連トピック**

[フラグメントに基づくフォームのレンダリング](#rendering-forms-based-on-fragments)

[クイックスタート（SOAPモード）:Java APIを使用したフラグメントに基づくフォームのレンダリング](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-based-on-fragments-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPIを使用してフラグメントに基づいてフォームをレンダリングする {#render-forms-based-on-fragments-using-the-web-service-api}

Forms API（Webサービス）を使用してフラグメントに基づいてフォームをレンダリングします。

1. プロジェクトファイルを含める

   * FormsサービスWSDLを使用するJavaプロキシクラスを作成します。
   * クラスパスにJavaプロキシクラスを含めます。

1. フォームクライアントAPIオブジェクトの作成

   オブジェクト `FormsService` を作成し、認証値を設定します。

1. URI値の指定

   * コンストラク `URLSpec` ターを使用して、URI値を格納するオブジェクトを作成します。
   * オブジェクト `URLSpec` のメソッドを `setApplicationWebRoot` 呼び出し、アプリケーションのWebルートを表すstring値を渡します。
   * オブジェクト `URLSpec` のメソッドを `setContentRootURI` 呼び出し、コンテンツルートURI値を指定するstring値を渡します。 フォームデザインがコンテンツルートURI内にあることを確認します。 そうでない場合、Formsサービスは例外をスローします。 リポジトリを参照するには、を指定しま `repository://`す。
   * オブジェクト `URLSpec` のメソッ `setTargetURL` ドを呼び出し、フォームデータの投稿先のターゲットURL値を指定するstring値を渡します。 フォームデザインでターゲットURLを定義する場合は、空の文字列を渡すことができます。 演算を実行するためにフォームの送信先URLを指定することもできます。

1. フォームのレンダリング

   オブジェクト `FormsService` のメソッドを `renderPDFForm` 呼び出し、次の値を渡します。

   * ファイル名の拡張子を含むフォームデザイン名を指定するstring値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、必ずなどの完全なパスを指定してくださ `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`い。
   * フォーム `BLOB` とマージするデータを含むオブジェクトです。 データを結合しない場合は、を渡します `null`。
   * 実行時 `PDFFormRenderSpec` のオプションを格納するオブジェクトです。 入力ドキュメントがPDFドキュメントの場合、タグ付きPDFオプションは設定できません。 入力ファイルがXDPファイルの場合は、タグ付きPDFオプションを設定できます。
   * Formsサ `URLSpec` ービスに必要なURI値を含むオブジェクトです。
   * 添付フ `java.util.HashMap` ァイルを格納するオブジェクト。 これはオプションのパラメーターで、フォームにフ `null` ァイルを添付しないかどうかを指定できます。
   * メソッドに `com.adobe.idp.services.holders.BLOBHolder` よって入力される空のオブジェクトです。 このパラメーターは、レンダリングされたフォームを保存するために使用されます。
   * メソッドに `javax.xml.rpc.holders.LongHolder` よって入力される空のオブジェクトです。 この引数は、フォーム内のページ数を格納します。
   * メソッドに `javax.xml.rpc.holders.StringHolder` よって入力される空のオブジェクトです。 この引数はロケールの値を格納します。
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

[フラグメントに基づくフォームのレンダリング](#rendering-forms-based-on-fragments)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
