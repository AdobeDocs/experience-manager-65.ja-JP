---
title: フラグメントに基づいたフォームのレンダリング
seo-title: Rendering Forms Based on Fragments
description: Forms サービスを使用すると、Designer を使用して作成されたフラグメントに基づくフォームをレンダリングできます。
seo-description: Use the Forms service to render forms that are based on fragments created using Designer.
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
source-wordcount: '2209'
ht-degree: 100%

---

# フラグメントに基づいたフォームのレンダリング {#rendering-forms-based-on-fragments}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

## フラグメントに基づいたフォームのレンダリング {#rendering-forms-based-on-fragments-inner}

Forms サービスでは、 Designer を使用して作成したフラグメントに基づくフォームをレンダリングできます。*フラグメント*&#x200B;とは、フォームの再利用可能な部分のことで、複数のフォームデザインに挿入できる個別の XDP ファイルとして保存されます。例えば、フラグメントには住所ブロックや法律文を含めることができます。

フラグメントの使用により、大量のフォームの作成とメンテナンスを簡単に、短時間で実行できます。フォームを新規作成するときに、必要なフラグメントへの参照を挿入すると、そのフラグメントがフォームに表示されます。フラグメント参照には、物理 XDP ファイルを指すサブフォームが含まれます。フラグメントを基にしたフォームデザインの作成について詳しくは、[Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63_jp) を参照してください。

フラグメントには、選択サブフォームセットにラップされた複数のサブフォームを含めることができます。選択サブフォームセットは、データ接続からのデータのフローに基づいてサブフォームの表示を制御します。条件ステートメントを使用して、配信するフォームに表示するサブフォームをそのセットから指定します。例えば、セットにあるサブフォームごとに特定の地理的な場所に関する情報を指定しておき、ユーザーの場所に基づいて、表示するサブフォームを決定できます。

*スクリプトフラグメント*&#x200B;には、日付パーサーや web サービス呼び出しなど、特定のオブジェクトとは独立して保存されている再利用可能な JavaScript 関数や値が含まれています。このようなフラグメントには、階層パレットに変数の子として表示される単独のスクリプトオブジェクトがあります。フラグメントは、他のオブジェクトのプロパティとなっているスクリプトからは作成できません。このようなスクリプトとして、検証、計算、初期化などのイベントスクリプトがあります。

フラグメントを使用する利点は次のとおりです。

* **コンテンツの再利用**：フラグメントを使用して、複数のフォームデザインでコンテンツを再利用できます。複数のフォームで同じコンテンツの一部を使用する必要がある場合は、コンテンツをコピーまたは再作成するよりも、フラグメントを使用する方が速くて簡単です。フラグメントを使用し、それをフォームで参照することで、フォームデザインの中で頻繁に使用する部分を一貫性のあるコンテンツと外観ですべてのフォームに表示できます。
* **グローバルな更新**：フラグメントを使用すれば、1 つのファイルを一度変更するだけで、複数のフォームをグローバルに変更できます。フラグメントのコンテンツ、スクリプトオブジェクト、 データバインディング、レイアウトまたはスタイルを変更すると、そのフラグメントを参照しているすべての XDP フォームに変更が反映されます。
* 例えば、多くのフォームで共有される要素として、国名のドロップダウンリストオブジェクトを含んだ住所ブロックが考えられます。このドロップダウンリストオブジェクトの値を更新するには、多数のフォームを開いて変更する必要があります。フラグメントに住所ブロックを含めると、1 つのフラグメントファイルを開くだけで変更できます。
* PDF フォームでフラグメントを更新するには、Designer でそのフォームを再度保存します。
* **共有フォームの作成**：フラグメントを使用して、複数のリソースでフォームの作成を共有できます。スクリプトまたは Designer のその他の高度な機能に精通しているフォーム開発者は、スクリプトまたは動的プロパティを活用するフラグメントを作成、共有することができます。フォーム作成者がこれらのフラグメントを使用してフォームデザインをレイアウトすれば、複数の担当者が作成した複数のフォームの各部分で一貫性のある外観と機能を実現できます。

### フラグメントを使用して作成されたフォームデザインの作成 {#assembling-a-form-design-assembled-using-fragments}

Forms サービスに渡すフォームデザインを、複数のフラグメントに基づいて作成することができます。複数のフラグメントを作成するには、Assembler サービスを使用します。別の Forms サービス（Output サービス）で使用するフォームデザインを作成するための Assemble サービスの使用例については、[フラグメントを使用した PDF ドキュメントの作成](/help/forms/developing/creating-document-output-streams.md#creating-pdf-documents-using-fragments)を参照してください。Output サービスを使用する代わりに、Forms サービスを使用して同じワークフローを実行できます。

Assembler サービスを使用する場合、フラグメントを使用して作成されたフォームデザインを渡します。作成されたフォームデザインは、他のフラグメントを参照しません。これに対し、このトピックでは、他のフラグメントを参照するフォームデザインを Forms サービスに渡す方法について説明します。ただし、このフォームデザインは Assembler によって作成されたものではありません。Designer で作成されています。

>[!NOTE]
>
>Forms サービスについて詳しくは、[AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

>[!NOTE]
>
>フラグメントに基づいてフォームをレンダリングする web ベースのアプリケーションの作成については、[フォームをレンダリングする web アプリケーションの作成](/help/forms/developing/creating-web-applications-renders-forms.md)を参照してください。

### 手順の概要 {#summary-of-steps}

フラグメントに基づいてフォームをレンダリングするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Forms Client API オブジェクトを作成します。
1. URI 値を指定します。
1. フォームをレンダリングします。
1. フォームデータストリームをクライアントの Web ブラウザーに書き込みます。

**プロジェクトファイルの組み込み**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**Forms Client API オブジェクトの作成**

Forms サービス Client API 操作をプログラムで実行には、事前に Forms サービスクライアントを作成しておく必要があります。

**URI 値の指定**

フラグメントに基づいてフォームを正常にレンダリングするには、フォームと、フォームデザインが参照するフラグメント（XDP ファイル）の両方を、Forms サービスが特定できるようにする必要があります。例えば、フォームの名前が PO.xdp で、このフォームが FooterUS.xdp および FooterCanada.xdp という 2 つのフラグメントを使用しているとします。このような場合、Forms サービスは 3 つの XDP ファイルをすべて特定できる必要があります。

フォームとフラグメントを別々の場所に配置して整理することができるほか、すべての XDP ファイルを同じ場所に配置することもできます。このセクションでは便宜上、すべての XDP ファイルが AEM Forms リポジトリ内にあると仮定します。AEM Forms リポジトリへの XDP ファイルの配置については、[リソースの書き込み](/help/forms/developing/aem-forms-repository.md#writing-resources)を参照してください。

フラグメントに基づいてフォームをレンダリングする場合は、フォーム自体のみを参照し、フラグメントは参照しないでください。例えば、FooterUS.xdp や FooterCanada.xdp ではなく、PO.xdp を参照する必要があります。フラグメントは、Forms サービスで見つけられる場所に配置してください。

**フォームのレンダリング**

フラグメントに基づくフォームは、フラグメント化されていないフォームと同じ方法でレンダリングできます。つまり、フォームを PDF、HTML またはフォームガイド（非推奨）としてレンダリングできます。この節の例では、フラグメントに基づいたフォームをインタラクティブな PDF フォームとしてレンダリングします。詳しくは、[インタラクティブ PDF フォームのレンダリング](/help/forms/developing/rendering-interactive-pdf-forms.md)を参照してください。

**クライアント web ブラウザーへのフォームデータストリームの書き込み**

Forms サービスがフォームをレンダリングすると、クライアントの web ブラウザーに書き込む必要があるフォームデータストリームが返されます。クライアント Web ブラウザーに書き込まれると、フォームはユーザーに対して表示されます。

**関連トピック**

[Java API を使用してフラグメントに基づいてフォームをレンダリング](#render-forms-based-on-fragments-using-the-java-api)

[Web サービス API を使用してフラグメントに基づいてフォームをレンダリング](#render-forms-based-on-fragments-using-the-web-service-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms サービス API のクイックスタート](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[インタラクティブ PDF Forms のレンダリング](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Forms をレンダリングする web アプリケーションの作成](/help/forms/developing/creating-web-applications-renders-forms.md)

### Java API を使用してフラグメントに基づいてフォームをレンダリング {#render-forms-based-on-fragments-using-the-java-api}

Forms API（Java）を使用して、フラグメントに基づいてフォームをレンダリングします。

1. プロジェクトファイルを含める

   adobe-forms-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. Forms Client API オブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して `ServiceClientFactory` オブジェクトを渡すことによって、`FormsServiceClient` オブジェクトを作成します。

1. URI 値を指定

   * コンストラクターを使用して、URI 値を格納する `URLSpec` オブジェクトを作成します。
   * `URLSpec` オブジェクトの `setApplicationWebRoot` メソッドを呼び出して、アプリケーションの web ルートを表す文字列値を渡します。
   * `URLSpec` オブジェクトの `setContentRootURI` メソッドを呼び出して、コンテンツルート URI 値を指定する文字列値を渡します。フォームデザインとフラグメントがコンテンツルート URI に配置されていることを確認します。そうでない場合、Forms サービスは例外をスローします。リポジトリを参照するには、`repository://` を指定します。
   * `URLSpec` オブジェクトの `setTargetURL` メソッドを呼び出して、フォームデータの送信先となるターゲット URL の値を指定する文字列を渡します。フォームデザインでターゲット URL を定義する場合、空の文字列を渡すことができます。また、計算を実行するためのフォームの送信先の URL を指定することもできます。

1. フォームのレンダリング

   `FormsServiceClient` オブジェクトの `renderPDFForm` メソッドを呼び出して、次の値を渡します。

   * フォームデザイン名を指定する文字列値で、ファイル名の拡張子も含まれます。Forms アプリケーションの一部であるフォームデザインを参照する場合は、必ず次のような完全なパスを指定してください。`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`
   * フォームに結合するデータを含む `com.adobe.idp.Document` オブジェクト。データを結合しない場合は、空の `com.adobe.idp.Document` オブジェクトを渡します。
   * 実行時オプションを保存する `PDFFormRenderSpec` オブジェクト。
   * フラグメントに基づいてフォームをレンダリングするために Forms サービスで必要な URI 値を含む `URLSpec` オブジェクト。
   * 添付ファイルを保存する `java.util.HashMap` オブジェクト。オプションのパラメーターです。フォームにファイルを添付しない場合は `null` を指定できます。

   `renderPDFForm` メソッドは、クライアントの Web ブラウザーに書き込む必要のあるフォームデータストリームを含む `FormsResult` オブジェクトを返します。

1. フォームデータストリームをクライアント web ブラウザーに書き込む

   * `FormsResult` オブジェクトの `getOutputContent` メソッドを呼び出して、`com.adobe.idp.Document` オブジェクトを作成します。
   * `getContentType` メソッドを呼び出して、`com.adobe.idp.Document` オブジェクトのコンテンツタイプを取得します。
   * `javax.servlet.http.HttpServletResponse` オブジェクトのコンテンツタイプを設定するには、`setContentType` メソッドを呼び出して、`com.adobe.idp.Document` オブジェクトのコンテンツタイプを渡します。
   * `javax.servlet.http.HttpServletResponse` オブジェクトの `getOutputStream` メソッドを呼び出して、フォームデータストリームをクライアント web ブラウザーに書き込むために使用される `javax.servlet.ServletOutputStream` オブジェクトを作成します。
   * `com.adobe.idp.Document` オブジェクトの `getInputStream` メソッドを呼び出して `java.io.InputStream` オブジェクトを作成します。
   * `InputStream` オブジェクトの `read` メソッドを呼び出して、引数としてバイト配列を渡すことで、バイト配列を作成し、フォームデータストリームを入力します。
   * `javax.servlet.ServletOutputStream` オブジェクトの `write` メソッドを呼び出して、クライアント web ブラウザーにフォームデータストリームを送信します。バイト配列を `write` メソッドに渡します。

**関連トピック**

[フラグメントに基づいたフォームのレンダリング](#rendering-forms-based-on-fragments)

[クイックスタート（SOAP モード）：Java API を使用したフラグメントベースのフォームのレンダリング](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-a-form-based-on-fragments-using-the-java-api)

[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Web サービス API を使用してフラグメントに基づいてフォームをレンダリング {#render-forms-based-on-fragments-using-the-web-service-api}

Forms API（web サービス）を使用して、フラグメントに基づいてフォームをレンダリングします。

1. プロジェクトファイルを含める

   * Forms Service WSDL を使用する Java プロキシクラスを作成します。
   * Java プロキシクラスをクラスパスに含めます。

1. Forms Client API オブジェクトの作成

   `FormsService` オブジェクトを作成し、認証値を設定します。

1. URI 値を指定

   * コンストラクターを使用して URI 値を格納する `URLSpec` オブジェクトを作成します。
   * `URLSpec` オブジェクトの `setApplicationWebRoot` メソッドを呼び出して、アプリケーションの web ルートを表す文字列値を渡します。
   * `URLSpec` オブジェクトの `setContentRootURI` メソッドを呼び出して、コンテンツルート URI 値を指定する文字列値を渡します。フォームデザインがコンテンツルート URI に配置されていることを確認します。そうでない場合、Forms サービスは例外をスローします。リポジトリを参照するには、`repository://` を指定します。
   * `URLSpec` オブジェクトの `setTargetURL` メソッドを呼び出して、フォームデータの送信先となるターゲット URL の値を指定する文字列を渡します。フォームデザインでターゲット URL を定義する場合、空の文字列を渡すことができます。また、計算を実行するためのフォームの送信先の URL を指定することもできます。

1. フォームのレンダリング

   `FormsService` オブジェクトの `renderPDFForm` メソッドを呼び出して、次の値を渡します。

   * フォームデザイン名を指定する文字列値で、ファイル名の拡張子も含まれます。Forms アプリケーションの一部であるフォームデザインを参照する場合は、必ず次のような完全なパスを指定してください。`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`
   * フォームに結合するデータを含む `BLOB` オブジェクト。データを結合しない場合は、空の `null` オブジェクトを渡します。
   * 実行時オプションを保存する `PDFFormRenderSpec` オブジェクト。入力ドキュメントが PDF ドキュメントの場合、「タグ付き PDF」オプションは設定できません。入力ファイルが XDP ファイルの場合は、「タグ付き PDF」オプションを設定できます。
   * Forms サービスで必要な URI 値を含む `URLSpec` オブジェクト。
   * 添付ファイルを保存する `java.util.HashMap` オブジェクト。これはオプションのパラメーターで、 フォームにファイルを添付しない場合に、`null`を指定します。
   * メソッドによって設定される空の `com.adobe.idp.services.holders.BLOBHolder` メソッド。このパラメーターは、レンダリングされたフォームを保存するために使用されます。
   * メソッドによって設定される空の `javax.xml.rpc.holders.LongHolder` オブジェクト。この引数は、フォームのページ数を保存します。
   * メソッドによって設定される空の `javax.xml.rpc.holders.StringHolder` オブジェクト。この引数はロケール値を格納します。
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

[フラグメントに基づいたフォームのレンダリング](#rendering-forms-based-on-fragments)

[Base64 エンコーディングを使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
