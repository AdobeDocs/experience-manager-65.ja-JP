---
title: フラグメントに基づくFormsのレンダリング
seo-title: フラグメントに基づくFormsのレンダリング
description: Formsサービスを使用して、Designerで作成されたフラグメントに基づくフォームをレンダリングします。
seo-description: Formsサービスを使用して、Designerで作成されたフラグメントに基づくフォームをレンダリングします。
uuid: 9c9a730d-f970-41f8-afed-4e6b6d3d393d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: a65c5303-0ebd-43a9-a777-401042d8fcad
role: Developer
exl-id: febf5350-3fc5-48c0-8bc5-198daff15936
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2229'
ht-degree: 9%

---

# フラグメントに基づくFormsのレンダリング{#rendering-forms-based-on-fragments}

**このドキュメントのサンプルと例は、JEE上のAEM Forms環境に限られています。**

## フラグメントに基づくFormsのレンダリング{#rendering-forms-based-on-fragments-inner}

Formsサービスは、Designerを使用して作成したフラグメントに基づくフォームをレンダリングできます。 *フラグメント*&#x200B;はフォームの再利用可能な部分で、複数のフォームデザインに挿入できる個別のXDPファイルとして保存されます。 例えば、フラグメントには住所ブロックや法律文を含めることができます。

フラグメントの使用により、大量のフォームの作成とメンテナンスを簡単に、短時間で実行できます。新しいフォームを作成する場合は、必要なフラグメントへの参照を挿入すると、フラグメントがフォームに表示されます。 フラグメント参照には、物理 XDP ファイルを指すサブフォームが含まれます。フラグメントに基づくフォームデザインの作成について詳しくは、[Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)を参照してください。

フラグメントには、選択サブフォームセットに含める複数のサブフォームを含めることができます。 選択サブフォームセットは、データ接続からのデータのフローに基づいてサブフォームの表示を制御します。 条件ステートメントを使用して、配信するフォームに表示するサブフォームをそのセットから指定します。例えば、セット内の各サブフォームには、特定の地理的位置に関する情報を含めることができ、表示されるサブフォームは、ユーザーの位置に基づいて決定できます。

*スクリプトフラグメント*&#x200B;には、日付パーサーやWebサービス呼び出しなど、特定のオブジェクトとは別に保存される再利用可能なJavaScript関数や値が含まれています。 このようなフラグメントには、階層パレットに変数の子として表示される単独のスクリプトオブジェクトがあります。フラグメントは、他のオブジェクトのプロパティとなっているスクリプトからは作成できません。このようなスクリプトとして、検証、計算、初期化などのイベントスクリプトがあります。

フラグメントを使用する利点は次のとおりです。

* **コンテンツの再利用**:フラグメントを使用すると、複数のフォームデザインでコンテンツを再利用できます。複数のフォームで同じコンテンツの一部を使用する必要がある場合は、コンテンツをコピーまたは再作成するよりも、フラグメントを使用するほうが高速で簡単です。 フラグメントを使用し、それをフォームで参照することで、フォームデザインの中で頻繁に使用する部分を一貫性のあるコンテンツと外観ですべてのフォームに表示できます。
* **グローバルな更新**:フラグメントを使用すると、1つのファイルで1回だけ複数のフォームに対してグローバルな変更を行うことができます。フラグメント内のコンテンツ、スクリプトオブジェクト、データ連結、レイアウト、スタイルを変更すると、そのフラグメントを参照するすべてのXDPフォームに変更が反映されます。
* 例えば、多くのフォームで共通する要素は、国のコンボボックスオブジェクトを含む住所ブロックです。 コンボボックスオブジェクトの値を更新する必要がある場合は、多数のフォームを開いて変更を加える必要があります。 フラグメントに住所ブロックを含める場合、変更を加えるには、1つのフラグメントファイルを開くだけで済みます。
* PDFフォーム内のフラグメントを更新するには、Designerでそのフォームを再保存する必要があります。
* **共有フォームの作成**:フラグメントを使用して、複数のリソースでフォームの作成を共有できます。スクリプトまたは Designer のその他の高度な機能に精通しているフォーム開発者は、スクリプトまたは動的プロパティを活用するフラグメントを作成、共有することができます。フォーム作成者がこれらのフラグメントを使用してフォームデザインをレイアウトすれば、複数の担当者が作成した複数のフォームの各部分で一貫性のある外観と機能を実現できます。

### フラグメント{#assembling-a-form-design-assembled-using-fragments}を使用してアセンブリされたフォームデザインのアセンブリ

複数のフラグメントに基づいてFormsサービスに渡すフォームデザインを組み立てることができます。 複数のフラグメントをアセンブリするには、Assemblerサービスを使用します。 Assembleサービスを使用して別のFormsサービス（Outputサービス）で使用されるフォームデザインを作成する例については、「[フラグメントを使用したPDFドキュメントの作成](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments)」を参照してください。 Outputサービスを使用する代わりに、Formsサービスを使用して同じワークフローを実行できます。

Assemblerサービスを使用する場合、フラグメントを使用してアセンブルされたフォームデザインを渡します。 作成されたフォームデザインは、他のフラグメントを参照していません。 これに対し、このトピックでは、他のフラグメントを参照するフォームデザインをFormsサービスに渡す方法について説明します。 ただし、フォームデザインはAssemblerによってアセンブルされていません。 Designerで作成されました。

>[!NOTE]
>
>Formsサービスについて詳しくは、『 AEM Formsのサービスリファレンス[ 』を参照してください。](https://www.adobe.com/go/learn_aemforms_services_63)

>[!NOTE]
>
>フラグメントに基づいてフォームをレンダリングするWebベースのアプリケーションの作成について詳しくは、[Forms](/help/forms/developing/creating-web-applications-renders-forms.md)をレンダリングするWebアプリケーションの作成を参照してください。

### 手順の概要{#summary-of-steps}

フラグメントに基づいてフォームをレンダリングするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Forms Client APIオブジェクトを作成します。
1. URI値を指定します。
1. フォームをレンダリングします。
1. フォームデータストリームをクライアントWebブラウザーに書き込みます。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用する場合は、プロキシファイルを必ず含めてください。

**Forms Client APIオブジェクトの作成**

FormsサービスクライアントAPI操作をプログラムで実行する前に、Formsサービスクライアントを作成する必要があります。

**URI値の指定**

フラグメントに基づいてフォームを正常にレンダリングするには、Formsサービスで、フォームデザインが参照するフォームとフラグメント（XDPファイル）の両方を検索できるようにする必要があります。 例えば、フォームの名前がPO.xdpで、このフォームがFooterUS.xdpおよびFooterCanada.xdpという2つのフラグメントを使用するとします。 この場合、Formsサービスは3つのXDPファイルをすべて見つけることができます。

フォームを別の場所に配置してフォームとそのフラグメントを整理することも、すべてのXDPファイルを同じ場所に配置することもできます。 この節の目的では、すべてのXDPファイルがAEM Formsリポジトリ内にあると仮定します。 AEM FormsリポジトリへのXDPファイルの配置について詳しくは、[リソース](/help/forms/developing/aem-forms-repository.md#writing-resources)の書き込みを参照してください。

フラグメントに基づいてフォームをレンダリングする場合は、フォーム自体のみを参照し、フラグメントは参照しないでください。 例えば、FooterUS.xdpやFooterCanada.xdpではなく、PO.xdpを参照する必要があります。 フラグメントは、Formsサービスで見つけられる場所に配置する必要があります。

**フォームのレンダリング**

フラグメントに基づくフォームは、フラグメント化されていないフォームと同じ方法でレンダリングできます。 つまり、フォームをPDF、HTML、またはフォームガイド（非推奨）としてレンダリングできます。 この節の例では、フラグメントに基づいたフォームをインタラクティブPDFフォームとしてレンダリングします。 ([インタラクティブPDF formsのレンダリング](/help/forms/developing/rendering-interactive-pdf-forms.md)を参照)。

**フォームデータストリームをクライアントWebブラウザーに書き込む**

Formsサービスは、フォームをレンダリングする際に、クライアントのWebブラウザーに書き込む必要があるフォームデータストリームを返します。 クライアントのWebブラウザーに書き込まれると、フォームはユーザーに表示されます。

**関連トピック**

[Java APIを使用してフラグメントに基づいてフォームをレンダリングする](#render-forms-based-on-fragments-using-the-java-api)

[WebサービスAPIを使用してフラグメントに基づいてフォームをレンダリングする](#render-forms-based-on-fragments-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[FormsサービスAPIのクイックスタート](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[インタラクティブPDF formsのレンダリング](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Forms](/help/forms/developing/creating-web-applications-renders-forms.md)

### Java API {#render-forms-based-on-fragments-using-the-java-api}を使用してフラグメントに基づいてフォームをレンダリングする

Forms API(Java)を使用して、フラグメントに基づいてフォームをレンダリングします。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-forms-client.jarなどのクライアントJARファイルを含めます。

1. Forms Client APIオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して`FormsServiceClient`オブジェクトを渡し、`ServiceClientFactory`オブジェクトを作成します。

1. URI値の指定

   * コンストラクターを使用して、URI値を格納する`URLSpec`オブジェクトを作成します。
   * `URLSpec`オブジェクトの`setApplicationWebRoot`メソッドを呼び出して、アプリケーションのWebルートを表す文字列値を渡します。
   * `URLSpec`オブジェクトの`setContentRootURI`メソッドを呼び出し、コンテンツルートURI値を指定する文字列値を渡します。 フォームデザインとフラグメントがコンテンツルートURIに配置されていることを確認します。 そうでない場合、Formsサービスは例外をスローします。 リポジトリを参照するには、`repository://`を指定します。
   * `URLSpec`オブジェクトの`setTargetURL`メソッドを呼び出し、フォームデータの投稿先となるターゲットURL値を指定する文字列値を渡します。 フォームデザインでターゲットURLを定義する場合は、空の文字列を渡すことができます。 演算を実行するためのフォームの送信先URLを指定することもできます。

1. フォームのレンダリング

   `FormsServiceClient`オブジェクトの`renderPDFForm`メソッドを呼び出し、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定するstring値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、必ず`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`のように完全なパスを指定してください。
   * フォームとマージするデータを含む`com.adobe.idp.Document`オブジェクト。 データを結合しない場合は、空の`com.adobe.idp.Document`オブジェクトを渡します。
   * 実行時オプションを格納する`PDFFormRenderSpec`オブジェクト。
   * フラグメントに基づいてフォームをレンダリングするためにFormsサービスで必要なURI値を含む`URLSpec`オブジェクト。
   * 添付ファイルを格納する`java.util.HashMap`オブジェクト。 これはオプションのパラメーターで、フォームにファイルを添付しない場合は`null`を指定できます。

   `renderPDFForm`メソッドは、クライアントのWebブラウザーに書き込む必要があるフォームデータストリームを含む`FormsResult`オブジェクトを返します。

1. フォームデータストリームをクライアントWebブラウザーに書き込む

   * `FormsResult`オブジェクトの`getOutputContent`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトを作成します。
   * `getContentType`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトのコンテンツタイプを取得します。
   * `setContentType`メソッドを呼び出し、`com.adobe.idp.Document`オブジェクトのコンテンツタイプを渡すことで、`javax.servlet.http.HttpServletResponse`オブジェクトのコンテンツタイプを設定します。
   * `javax.servlet.http.HttpServletResponse`オブジェクトの`getOutputStream`メソッドを呼び出して、フォームデータストリームをクライアントWebブラウザーに書き込むための`javax.servlet.ServletOutputStream`オブジェクトを作成します。
   * `com.adobe.idp.Document`オブジェクトの`getInputStream`メソッドを呼び出して、`java.io.InputStream`オブジェクトを作成します。
   * `InputStream`オブジェクトの`read`メソッドを呼び出し、バイト配列を引数として渡すことで、バイト配列にフォームデータストリームを入力します。
   * `javax.servlet.ServletOutputStream`オブジェクトの`write`メソッドを呼び出して、フォームデータストリームをクライアントWebブラウザーに送信します。 `write`メソッドにバイト配列を渡します。

**関連トピック**

[フラグメントに基づくFormsのレンダリング](#rendering-forms-based-on-fragments)

[クイックスタート（SOAPモード）:Java APIを使用したフラグメントに基づくフォームのレンダリング](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-based-on-fragments-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### WebサービスAPI {#render-forms-based-on-fragments-using-the-web-service-api}を使用してフラグメントに基づいてフォームをレンダリングする

Forms API（Webサービス）を使用して、フラグメントに基づいてフォームをレンダリングします。

1. プロジェクトファイルを含める

   * FormsサービスのWSDLを使用するJavaプロキシクラスを作成します。
   * Javaプロキシクラスをクラスパスに含めます。

1. Forms Client APIオブジェクトの作成

   `FormsService`オブジェクトを作成し、認証値を設定します。

1. URI値の指定

   * コンストラクターを使用して、URI値を格納する`URLSpec`オブジェクトを作成します。
   * `URLSpec`オブジェクトの`setApplicationWebRoot`メソッドを呼び出して、アプリケーションのWebルートを表す文字列値を渡します。
   * `URLSpec`オブジェクトの`setContentRootURI`メソッドを呼び出し、コンテンツルートURI値を指定する文字列値を渡します。 フォームデザインがコンテンツルートURIに配置されていることを確認します。 そうでない場合、Formsサービスは例外をスローします。 リポジトリを参照するには、`repository://`を指定します。
   * `URLSpec`オブジェクトの`setTargetURL`メソッドを呼び出し、フォームデータの投稿先となるターゲットURL値を指定する文字列値を渡します。 フォームデザインでターゲットURLを定義する場合は、空の文字列を渡すことができます。 演算を実行するためのフォームの送信先URLを指定することもできます。

1. フォームのレンダリング

   `FormsService`オブジェクトの`renderPDFForm`メソッドを呼び出し、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定するstring値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、必ず`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`のように完全なパスを指定してください。
   * フォームとマージするデータを含む`BLOB`オブジェクト。 データを結合しない場合は、`null`を渡します。
   * 実行時オプションを格納する`PDFFormRenderSpec`オブジェクト。 入力ドキュメントがPDFドキュメントの場合、タグ付きPDFオプションは設定できません。 入力ファイルがXDPファイルの場合、タグ付きPDFオプションを設定できます。
   * Formsサービスに必要なURI値を含む`URLSpec`オブジェクト。
   * 添付ファイルを格納する`java.util.HashMap`オブジェクト。 これはオプションのパラメーターで、フォームにファイルを添付しない場合は`null`を指定できます。
   * メソッドで設定される空の`com.adobe.idp.services.holders.BLOBHolder`オブジェクト。 このパラメーターは、レンダリングされたフォームを保存するために使用されます。
   * メソッドで設定される空の`javax.xml.rpc.holders.LongHolder`オブジェクト。 この引数は、フォームのページ数を保存します。
   * メソッドで設定される空の`javax.xml.rpc.holders.StringHolder`オブジェクト。 この引数はロケール値を格納します。
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

[フラグメントに基づくFormsのレンダリング](#rendering-forms-based-on-fragments)

[Base64エンコーディングを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
