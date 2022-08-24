---
title: インタラクティブ PDF Forms のレンダリング
seo-title: Rendering Interactive PDF Forms
description: Forms サービスを使用して、インタラクティブ PDF forms をクライアントデバイス（通常は web ブラウザー）にレンダリングして、ユーザーから情報を収集します。Forms サービスを使用して、Java API および web サービス API を使いインタラクティブフォームをレンダリングできます。
seo-description: Use the Forms service to render interactive PDF forms to client devices, typically web browsers, to collect information from users. You can use Forms service to render interactive forms using the Java API and Web Service API.
uuid: df2a4dc8-f19e-49de-850f-85a204102631
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 3cb307ec-9b7b-4f03-b860-48553ccee746
role: Developer
exl-id: d9f32939-c2c0-4531-b15e-f63941c289e3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2487'
ht-degree: 100%

---

# インタラクティブ PDF Forms のレンダリング {#rendering-interactive-pdf-forms}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

Forms サービスは、ユーザーから情報を収集するために、インタラクティブ PDF forms をクライアントデバイス（通常は web ブラウザー）にレンダリングします。インタラクティブフォームがレンダリングされると、ユーザーはフォームフィールドにデータを入力し、フォーム上の送信ボタンをクリックして、情報を Forms サービスに送り返すことができます。インタラクティブな PDF フォームを表示するには、クライアント Web ブラウザーをホストするコンピューターに Adobe Reader または Acrobat をインストールする必要があります。

>[!NOTE]
>
>Forms サービスを使用してフォームをレンダリングする前に、フォームデザインを作成します。通常、フォームデザインは Designer で作成され、XDP ファイルとして保存されます。フォームデザインの作成について詳しくは、[Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63_jp) を参照してください。

**ローン申し込みのサンプル**

Forms サービスが、どのようにしてインタラクティブフォームを使用してユーザーから情報を収集するかを示すために、サンプルのローン申し込みフォームが紹介されています。このアプリケーションを使用すると、ユーザーはローンのセキュリティ保護に必須のデータをフォームに入力し、データを Forms サービスに送信できます。次の図に、ローン申し込みのロジックフローを示します。

![ri_ri_finsrv_loanapp_v1](assets/ri_ri_finsrv_loanapp_v1.png)

次の表に、この図の手順を示します。

<table>
 <thead>
  <tr>
   <th><p>ステップ</p></th>
   <th><p>説明</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>この <code>GetLoanForm</code> Java サーブレットは、「HTML」ページから呼び出されます。 </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>この <code>GetLoanForm</code> Java サーブレットは、Forms Service Client API を使用して、ローン申し込みフォームをクライアント web ブラウザーにレンダリングします。（ <a href="#render-an-interactive-pdf-form-using-the-java-api">Java API を使用したインタラクティブ PDF フォームのレンダリング</a>を参照してください。）</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>ユーザーがローン申し込みフォームに入力し、送信ボタンをクリックすると、データが <code>HandleData</code> Java サーブレットに送信されます。（<i>「ローン申し込みフォーム」</i>を参照してください。）</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>この <code>HandleData</code> Java サーブレットは、Forms Service Client API を使用してフォーム送信を処理し、フォームデータを取得します。次に、データはエンタープライズデータベースに保存されます。（<a href="/help/forms/developing/handling-submitted-forms.md#handling-submitted-forms">送信済みフォームの処理</a>を参照してください。）</p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>確認フォームが web ブラウザーにレンダリングされます。ユーザーの姓や名などのデータは、レンダリング前にフォームと結合されます。（<a href="/help/forms/developing/prepopulating-forms-flowable-layouts.md">編集可能なレイアウトを使用した Forms の事前入力</a>を参照してください。）</p></td>
  </tr>
 </tbody>
</table>

**ローン申し込みフォーム**

このインタラクティブなローン申し込みフォームは、サンプルのローン申請の `GetLoanForm` Java サーブレットによってレンダリングされます。

![ri_ri_loanform](assets/ri_ri_loanform.png)

**確認フォーム**

このフォームは、サンプルのローン申請の `HandleData` Java サーブレットにレンダリングされます。

![ri_ri_confirm](assets/ri_ri_confirm.png)

この `HandleData` Java サーブレットは、このフォームにユーザーの姓と名および金額を事前入力します。フォームが事前入力された後、クライアントの web ブラウザーに送信されます。（[編集可能なレイアウトを使用した Forms の事前入力](/help/forms/developing/prepopulating-forms-flowable-layouts.md)）

**Java サーブレット**

サンプルのローン申し込みフォームは、Java サーブレットとして存在する Forms サービスアプリケーションの一例です。Java サーブレットは、WebSphere などの J2EE アプリケーションサーバー上で実行される Java プログラムで、Forms Service Client API コードを含みます。

次のコードは、GetLoanForm という名前の Java サーブレットの構文を示します。

```java
     public class GetLoanForm extends HttpServlet implements Servlet {
         public void doGet(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {

         }
         public void doPost(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {

             }
```

通常、 Java サーブレットの `doGet` または `doPost` メソッドには Forms Service Client API コードを配置しません。より優れたプログラミング方法としては、このコードを別のクラスに配置し、そのクラスを、`doPost` メソッド（または `doGet` メソッド）でインスタンス化し、適切なメソッドを呼び出します。ただし、コードを簡潔にするため、このセクションでのコードの例は最小限に抑えられ、コード例は `doPost` メソッドで配置されています。

>[!NOTE]
>
>Forms サービスについて詳しくは、[AEM Forms のサービスリファレンス](https://www.adobe.com/go/learn_aemforms_services_63)を参照してください。

**手順の概要**

インタラクティブ PDF フォームをレンダリングするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Forms Client API オブジェクトを作成します。
1. URI 値を指定します。
1. フォームにファイルを添付します（オプション）。
1. インタラクティブ PDF フォームをレンダリングします。
1. フォームデータストリームをクライアントの Web ブラウザーに書き込みます。

**プロジェクトファイルの組み込み**

必要なファイルを開発プロジェクトに含めます。Java を使用してクライアントアプリケーションを作成する場合は、必要な JAR ファイルを含めます。Web サービスを使用している場合は、プロキシファイルを必ず含めてください。

**Forms Client API オブジェクトの作成**

Forms Service Client API 操作をプログラムで実行する前に、Forms Client API オブジェクトを作成する必要があります。Java API を使用している場合は、`FormsServiceClient` オブジェクトを作成します。Forms web サービス API を使用している場合は、`FormsService` オブジェクトを作成します。

**URI 値の指定**

Forms サービスでフォームをレンダリングするために必要な URI 値を指定できます。Forms アプリケーションの一部として保存されたフォームデザインは、コンテンツルート URI 値 `repository:///` を使用して参照できます。例えば、*FormsApplication* という Forms アプリケーション内にある *Loan.xdp* という次のフォームデザインを考えます。

![ri_ri_formrepository](assets/ri_ri_formrepository.png)

このフォームデザインにアクセスするには、フォーム名（`renderPDFForm` メソッドに渡される最初のパラメーター）として `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp` を指定し、コンテンツルート URI 値として `repository:///` を指定します。

>[!NOTE]
>
>Workbench を使用した Forms アプリケーションの作成について詳しくは、[Workbench ヘルプ](https://www.adobe.com/go/learn_aemforms_workbench_63_jp)を参照してください。

Forms アプリケーション内のリソースへのパスは次のとおりです。

`Applications/Application-name/Application-version/Folder.../Filename`

URI 値の一例を以下に示します。

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

インタラクティブフォームをレンダリングする際に、フォームデータの送信先となるターゲット URL などの URI 値を定義できます。ターゲット URL は、次のいずれかの方法で定義できます。

* Designer でフォームデザインを設計する際の「送信」ボタン
* Forms サービス Client API を使用

ターゲット URL がフォームデザイン内で定義されている場合は、Forms サービス Client API を使用して上書きしないでください。Forms API を使用してターゲット URL を設定すると、フォームデザインで指定された URL が、API を使用して指定された URL にリセットされます。フォームデザインで指定されたターゲット URL に PDF フォームを送信する場合は、プログラムによってターゲット URL を空の文字列に設定します。

「送信」ボタンと「計算」ボタン（サーバーで実行される対応するスクリプト）を含むフォームがある場合、フォームが送信されるスクリプトの URL をプログラムで定義してスクリプトを実行できます。フォームデザインの送信ボタンを使用して、フォームデータが投稿される URL を指定します（[フォームデータの計算](/help/forms/developing/calculating-form-data.md)を参照）。

>[!NOTE]
>
>XDP ファイルを参照する URL 値を指定する代わりに、Forms サービスに `com.adobe.idp.Document` インスタンスを渡すこともできます。`com.adobe.idp.Document` インスタンスにはフォームデザインが含まれています（[Forms サービスにドキュメントを渡す](/help/forms/developing/passing-documents-forms-service.md)を参照）。

**フォームにファイルを添付する**

フォームにファイルを添付できます。添付ファイルを含む PDF フォームをレンダリングすると、ユーザーは添付ファイルペインを使用して Acrobat で添付ファイルを取得できます。フォームには、テキストファイルなどの様々なファイルタイプを添付したり、バイナリファイル（JPG ファイルなど ）に添付したりできます。

>[!NOTE]
>
>フォームへのファイルの添付はオプションです。

**インタラクティブ PDF フォームのレンダリング**

フォームをレンダリングするには、Designer で作成され、XDP ファイルまたは PDF ファイルとして保存されたフォームデザインを使用します。また、Acrobat を使用して作成され、PDF ファイルとして保存されたフォームをレンダリングすることもできます。インタラクティブな PDF フォームをレンダリングするには、`FormsServiceClient` オブジェクトの `renderPDFForm` メソッドまたは `renderPDFForm2` メソッドを呼び出します。

`renderPDFForm` は `URLSpec` オブジェクトを使用します。XDP ファイルへのコンテンツルートは、`URLSpec` オブジェクトの `setContentRootURI` メソッドを使用して Forms サービスに渡されます。フォームデザイン名（`formQuery`）は別のパラメーター値として渡されます。2 つの値が連結され、フォームデザインへの絶対参照が取得されます。

`renderPDFForm2` メソッドはレンダリングする XDP ドキュメントまたは PDF ドキュメントを含む `com.adobe.idp.Document` インスタンスを受け取ります。

>[!NOTE]
>
>入力ドキュメントが PDF ドキュメントの場合、タグ付き PDF の実行時オプションは設定できません。入力ファイルが XDP ファイルの場合は、「タグ付き PDF」オプションを設定できます。

## Java API を使用したインタラクティブ PDF フォームのレンダリング {#render-an-interactive-pdf-form-using-the-java-api}

Forms API（Java）を使用してインタラクティブ PDF フォームをレンダリングします。

1. プロジェクトファイルを含める

   adobe-forms-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。

1. Forms Client API オブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して `ServiceClientFactory` オブジェクトを渡すことによって、`FormsServiceClient` オブジェクトを作成します。

1. URI 値を指定

   * コンストラクターを使用して、URI 値を格納する `URLSpec` オブジェクトを作成します。
   * `URLSpec` オブジェクトの `setApplicationWebRoot` メソッドを呼び出して、アプリケーションの web ルートを表す文字列値を渡します。
   * `URLSpec` オブジェクトの `setContentRootURI` メソッドを呼び出して、コンテンツルート URI 値を指定する文字列値を渡します。フォームデザインがコンテンツルート URI に配置されていることを確認します。そうでない場合、Forms サービスは例外をスローします。リポジトリを参照するには、`repository:///` を指定します。
   * `URLSpec` オブジェクトの `setTargetURL` メソッドを呼び出して、フォームデータの送信先となるターゲット URL の値を指定する文字列を渡します。フォームデザインでターゲット URL を定義する場合、空の文字列を渡すことができます。また、計算を実行するためのフォームの送信先の URL を指定することもできます。

1. フォームにファイルを添付する

   * コンストラクターを使用して、添付ファイルを格納する `java.util.HashMap` オブジェクトを作成します。
   * レンダリングされたフォームに添付するファイルごとに `java.util.HashMap` オブジェクトの `put` メソッドを呼び出します。このメソッドに次の値を渡します。

      * ファイル名の拡張子を含む、添付ファイルの名前を指定する文字列値
   * 添付ファイルを含む `com.adobe.idp.Document` オブジェクト

   >[!NOTE]
   >
   >フォームに添付するファイルごとに、この手順を繰り返します。この手順はオプションです。添付ファイルを送信しない場合は、`null` を渡すことができます。

1. インタラクティブ PDF フォームのレンダリング

   `FormsServiceClient` オブジェクトの `renderPDFForm` メソッドを呼び出して、次の値を渡します。

   * フォームデザイン名を指定する文字列値で、ファイル名の拡張子も含まれます。Forms アプリケーションの一部であるフォームデザインを参照する場合は、必ず次のような完全なパスを指定してください。`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`
   * フォームに結合するデータを含む `com.adobe.idp.Document` オブジェクト。データを結合しない場合は、空の `com.adobe.idp.Document` オブジェクトを渡します。
   * 実行時オプションを格納する `PDFFormRenderSpec` オブジェクト。これはオプションのパラメーターで、実行時オプションを指定しない場合は、`null` を指定できます。
   * Forms サービスで必要となる URI 値が含まれる `URLSpec` オブジェクト。
   * 添付ファイルを保存する `java.util.HashMap` オブジェクト。オプションのパラメーターです。フォームにファイルを添付しない場合は `null` を指定できます。

   `renderPDFForm` メソッドは、クライアントの Web ブラウザーに書き込む必要のあるフォームデータストリームを含む `FormsResult` オブジェクトを返します。

1. フォームデータストリームをクライアント web ブラウザーに書き込む

   * `FormsResult` オブジェクトの `getOutputContent` メソッドを呼び出して、`com.adobe.idp.Document` オブジェクトを作成します。
   * `getContentType` メソッドを呼び出して、`com.adobe.idp.Document` オブジェクトのコンテンツタイプを取得します。
   * `javax.servlet.http.HttpServletResponse` オブジェクトのコンテンツタイプを設定するには、`setContentType` メソッドを呼び出して、`com.adobe.idp.Document` オブジェクトのコンテンツタイプを渡します。
   * `javax.servlet.http.HttpServletResponse` オブジェクトの `getOutputStream` メソッドを呼び出して、フォームデータストリームをクライアント web ブラウザーに書き込むために使用される `javax.servlet.ServletOutputStream` オブジェクトを作成します。
   * `com.adobe.idp.Document` オブジェクトの `getInputStream` メソッドを呼び出すことによって `java.io.InputStream` オブジェクトを作成します。
   * `InputStream` オブジェクトの `read` メソッドを呼び出してバイト配列を引数として渡すことによって、バイト配列を作成してフォームデータストリームを入力します。
   * `javax.servlet.ServletOutputStream` オブジェクトの `write` メソッドを呼び出して、フォームデータストリームをクライアント web ブラウザーに送信します。`write` メソッドにバイト配列を渡します。

## Web サービス API を使用したインタラクティブ PDF フォームのレンダリング {#render-an-interactive-pdf-form-using-the-web-service-api}

Forms API（web サービス）を使用してインタラクティブ PDF フォームをレンダリングします。

1. プロジェクトファイルを含める

   * Forms Service WSDL を使用する Java プロキシクラスを作成します。
   * Java プロキシクラスをクラスパスに含めます。

1. Forms Client API オブジェクトの作成

   `FormsService` オブジェクトを作成し、認証値を設定します。

1. URI 値を指定

   * コンストラクターを使用して、URI 値を格納する `URLSpec` オブジェクトを作成します。
   * `URLSpec` オブジェクトの `setApplicationWebRoot` メソッドを呼び出して、アプリケーションの web ルートを表す文字列値を渡します。
   * `URLSpec` オブジェクトの `setContentRootURI` メソッドを呼び出して、コンテンツルート URI 値を指定する文字列値を渡します。フォームデザインがコンテンツルート URI に配置されていることを確認します。そうでない場合、Forms サービスは例外をスローします。リポジトリを参照するには、`repository:///` を指定します。
   * `URLSpec` オブジェクトの `setTargetURL` メソッドを呼び出して、フォームデータの送信先となるターゲット URL の値を指定する文字列を渡します。フォームデザインでターゲット URL を定義する場合、空の文字列を渡すことができます。また、計算を実行するためのフォームの送信先の URL を指定することもできます。

1. フォームにファイルを添付する

   * コンストラクターを使用して、添付ファイルを格納する `java.util.HashMap` オブジェクトを作成します。
   * レンダリングされたフォームに添付するファイルごとに `java.util.HashMap` オブジェクトの `put` メソッドを呼び出します。このメソッドに次の値を渡します。

      * ファイル名の拡張子を含む添付ファイルの名前を指定する文字列値
   * 添付ファイルを含む `BLOB` オブジェクト

   >[!NOTE]
   >
   >フォームに添付するファイルごとに、この手順を繰り返します。

1. インタラクティブ PDF フォームのレンダリング

   `FormsService` オブジェクトの `renderPDFForm` メソッドを呼び出して、次の値を渡します。

   * フォームデザイン名を指定する文字列値で、ファイル名の拡張子も含まれます。Forms アプリケーションの一部であるフォームデザインを参照する場合は、必ず次のような完全なパスを指定してください。`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`
   * フォームに結合するデータを含む `BLOB` オブジェクト。データを結合しない場合は、空の `null` オブジェクトを渡します。
   * 実行時オプションを格納する `PDFFormRenderSpec` オブジェクト。これはオプションのパラメーターで、実行時オプションを指定しない場合は、`null` を指定できます。
   * Forms サービスで必要となる URI 値が含まれる `URLSpec` オブジェクト。
   * 添付ファイルを保存する `java.util.HashMap` オブジェクト。これはオプションのパラメーターで、 フォームにファイルを添付しない場合に、`null`を指定します。
   * メソッドによって設定される空の `com.adobe.idp.services.holders.BLOBHolder` オブジェクト。これは、レンダリングされた PDF フォームを保存するために使用されます。
   * メソッドによって設定される空の `javax.xml.rpc.holders.LongHolder` オブジェクト。（この引数は、フォームのページ数を格納します。）
   * メソッドによって設定される空の `javax.xml.rpc.holders.StringHolder` オブジェクト。（この引数はロケール値を格納します。）
   * この操作の結果を含むことになる空の `com.adobe.idp.services.holders.FormsResultHolder` オブジェクト。

   `renderPDFForm` メソッドは、最後の引数値として渡される `com.adobe.idp.services.holders.FormsResultHolder` オブジェクトに、クライアント web ブラウザーに書き込む必要のあるフォームデータストリームを入力します。

1. フォームデータストリームをクライアント web ブラウザーに書き込む

   * `com.adobe.idp.services.holders.FormsResultHolder` オブジェクトの `value` データメンバーの値を取得して、`FormResult` オブジェクトを作成します。
   * `FormsResult` オブジェクトの `getOutputContent` メソッドを呼び出して、フォームデータを含む `BLOB` オブジェクトを作成します。
   * `getContentType` メソッドを呼び出して、`BLOB` オブジェクトのコンテンツタイプを取得します。
   * `javax.servlet.http.HttpServletResponse` オブジェクトのコンテンツタイプを設定するには、`setContentType` メソッドを呼び出して、`BLOB` オブジェクトのコンテンツタイプを渡します。
   * `javax.servlet.http.HttpServletResponse` オブジェクトの `getOutputStream` メソッドを呼び出して、フォームデータストリームをクライアント web ブラウザーに書き込むために使用される `javax.servlet.ServletOutputStream` オブジェクトを作成します。
   * バイト配列を作成し、`BLOB` オブジェクトの `getBinaryData` メソッドを呼び出して入力します。このタスクは、`FormsResult` オブジェクトのコンテンツをバイト配列に割り当てます。
   * `javax.servlet.http.HttpServletResponse` オブジェクトの `write` メソッドを呼び出して、フォームデータストリームをクライアント web ブラウザーに送信します。バイト配列を `write` メソッドに渡します。

**フォームデータストリームをクライアント web ブラウザーに書き込む**

Forms サービスがフォームをレンダリングすると、クライアントの web ブラウザーに書き込む必要があるフォームデータストリームが返されます。クライアント Web ブラウザーに書き込まれると、フォームはユーザーに対して表示されます。
