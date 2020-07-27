---
title: インタラクティブPDF formsのレンダリング
seo-title: インタラクティブPDF formsのレンダリング
description: 'null'
seo-description: 'null'
uuid: df2a4dc8-f19e-49de-850f-85a204102631
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 3cb307ec-9b7b-4f03-b860-48553ccee746
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '2442'
ht-degree: 0%

---


# インタラクティブPDF formsのレンダリング {#rendering-interactive-pdf-forms}

Formsサービスは、ユーザーから情報を収集するために、インタラクティブなPDF formsをクライアントデバイス（通常はWebブラウザー）にレンダリングします。 インタラクティブフォームのレンダリング後、ユーザーはフォームフィールドにデータを入力し、フォーム上の送信ボタンをクリックして、情報をFormsサービスに送り返すことができます。 インタラクティブPDFフォームを表示するには、クライアントWebブラウザーをホストするコンピューターにAdobe ReaderまたはAcrobatをインストールする必要があります。

>[!NOTE]
>
>Formsサービスを使用してフォームをレンダリングする前に、フォームデザインを作成します。 通常、フォームデザインはDesignerで作成され、XDPファイルとして保存されます。 フォームデザインの作成について詳しくは、「 [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)」を参照してください。

**ローンの申し込み例**

Formsサービスがインタラクティブフォームを使用してユーザーから情報を収集する方法を示すローン申し込みのサンプルが紹介されています。 このアプリケーションを使用すると、ユーザーはローンのセキュリティ保護に必要なデータをフォームに入力し、データをFormsサービスに送信できます。 次の図に、ローン申込のロジックの流れを示します。

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
   <td><p>JavaサーブレットがHTMLページから呼び出され <code>GetLoanForm</code> ます。 </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Javaサーブレットは、FormsサービスクライアントAPIを使用してローンフォームをクライアントWebブラウザーにレンダリングします。 <code>GetLoanForm</code> (Java APIを使用したインタラクティブPDFフォームの <a href="#render-an-interactive-pdf-form-using-the-java-api">レンダリングを参照</a>)。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>ユーザーがローンフォームに入力し、「送信」ボタンをクリックすると、データが <code>HandleData</code> Javaサーブレットに送信されます。 (「ロ <i>ーンフォーム」を参照</i>)。</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Javaサーブレットは、FormsサービスクライアントAPIを使用してフォーム送信を処理し、フォームデータを取得します。 <code>HandleData</code> 次に、データをエンタープライズデータベースに格納します。 (送信済みのフォームの <a href="/help/forms/developing/handling-submitted-forms.md#handling-submitted-forms">処理を参照</a>)。</p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>確認フォームがWebブラウザーにレンダリングされて戻されます。 ユーザーの姓や名などのデータは、レンダリング前にフォームにマージされます。 (編集可能なレイアウト <a href="/help/forms/developing/prepopulating-forms-flowable-layouts.md">を含むフォームへの自動埋め込みを参照</a>)。</p></td>
  </tr>
 </tbody>
</table>

**ローンフォーム**

このインタラクティブローンフォームは、サンプルローンアプリケーションの `GetLoanForm` Javaサーブレットによってレンダリングされます。

![ri_ri_loanform](assets/ri_ri_loanform.png)

**確認フォーム**

このフォームは、サンプルローンアプリケーションの `HandleData` Javaサーブレットによってレンダリングされます。

![ri_ri_confirm](assets/ri_ri_confirm.png)

Javaサーブレットは、 `HandleData` このフォームにユーザーの姓と名と金額を事前入力します。 フォームに事前入力された後、フォームがクライアントのWebブラウザーに送信されます。 (編集可能なレイアウト [を含むフォームへの自動埋め込みを参照](/help/forms/developing/prepopulating-forms-flowable-layouts.md))。

**Javaサーブレット**

サンプルのローン申込書は、Javaサーブレットとして存在するFormsサービス申込書の例です。 Javaサーブレットは、WebSphereなどのJ2EEアプリケーションサーバー上で実行されるJavaプログラムで、FormsサービスクライアントAPIコードが含まれています。

次のコードは、GetLoanFormという名前のJavaサーブレットの構文を示しています。

```java
     public class GetLoanForm extends HttpServlet implements Servlet {
         public void doGet(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {

         }
         public void doPost(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {

             }
```

通常は、FormsサービスのクライアントAPIコードをJavaサーブレット `doGet` または `doPost` メソッド内に配置しません。 このコードを別のクラスに配置し、メソッド（またはメソッド）内からクラスをインスタンス化して、適切なメソッドを呼び出す方が、プログラミング `doPost` の `doGet` 方法が適切です。 ただし、コードを簡潔にするために、この節のコード例は最小限に抑え、コード例はこの `doPost` メソッドに配置します。

>[!NOTE]
>
>For more information about the Forms service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

**手順の概要**

インタラクティブPDFフォームをレンダリングするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. フォームクライアントAPIオブジェクトを作成します。
1. URI値を指定します。
1. フォームへのファイルの添付（オプション）
1. インタラクティブPDFフォームをレンダリングします。
1. フォームデータストリームをクライアントのWebブラウザーに書き込みます。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、プロキシファイルを必ず含めてください。

**フォームクライアントAPIオブジェクトの作成**

プログラムでFormsサービスのクライアントAPI操作を実行する前に、Forms Client APIオブジェクトを作成する必要があります。 Java APIを使用している場合は、 `FormsServiceClient` オブジェクトを作成します。 Forms WebサービスAPIを使用している場合は、 `FormsService` オブジェクトを作成します。

**URI値の指定**

Formsサービスでフォームをレンダリングするために必要なURI値を指定できます。 Formsアプリケーションの一部として保存されたフォームデザインは、コンテンツルートURI値を使用して参照でき `repository:///`ます。 例えば、FormsApplicationという名前のFormsアプリケーション内にある *Loan.xdp* という名前の次のフォームデザインを考えてみましょう **。

![ri_ri_formrepository](assets/ri_ri_formrepository.png)

このフォームデザインにアクセスするには、フォーム名( `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp` メソッドに渡される最初のパラメーター)とコンテンツルートURI `renderPDFForm``repository:///` の値を指定します。

>[!NOTE]
>
>Workbenchを使用したFormsアプリケーションの作成に関する詳細は、『 [Workbenchヘルプ](https://www.adobe.com/go/learn_aemforms_workbench_63)』を参照してください。

Formsアプリケーション内のリソースへのパスは次のとおりです。

`Applications/Application-name/Application-version/Folder.../Filename`

次に、URI値の例を示します。

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

インタラクティブフォームをレンダリングする場合、フォームデータの投稿先となるターゲットURLなどのURI値を定義できます。 ターゲットURLは、次のいずれかの方法で定義できます。

* Designerでフォームデザインをデザインする際の「Submit」ボタン
* FormsサービスクライアントAPIを使用する

ターゲットURLがフォームデザイン内で定義されている場合は、FormsサービスクライアントAPIで上書きしないでください。 つまり、Forms APIを使用してターゲットURLを設定すると、フォームデザインで指定されたURLが、APIを使用して指定されたURLにリセットされます。 PDFフォームをフォームデザインで指定されたターゲットURLに送信する場合は、プログラムでターゲットURLを空の文字列に設定します。

送信ボタンと計算ボタン（サーバーで実行される対応するスクリプトを含む）を含むフォームがある場合、スクリプトを実行するためにフォームを送信する先のURLをプログラムで定義できます。 フォームデザインの送信ボタンを使用して、フォームデータが投稿されるURLを指定します。 (フォームデータの [計算を参照](/help/forms/developing/calculating-form-data.md))。

>[!NOTE]
>
>XDPファイルを参照するURL値を指定する代わりに、Formsサービスに `com.adobe.idp.Document` インスタンスを渡すこともできます。 この `com.adobe.idp.Document` インスタンスにはフォームデザインが含まれています。 (「Formsサービスに [ドキュメントを渡す](/help/forms/developing/passing-documents-forms-service.md)」を参照)。

**フォームへのファイルの添付**

フォームにファイルを添付できます。 添付ファイルを含むPDFフォームをレンダリングする場合、ユーザーは添付ファイルペインを使用して、Acrobatで添付ファイルを取得できます。 テキストファイルなどのフォームや、JPGファイルなどのバイナリファイルに、様々なファイル形式を添付できます。

>[!NOTE]
>
>添付ファイルのフォームへの添付は任意です。

**インタラクティブPDFフォームのレンダリング**

フォームをレンダリングするには、Designerで作成され、XDPまたはPDFファイルとして保存されたフォームデザインを使用します。 また、Acrobatを使用して作成し、PDFファイルとして保存したフォームをレンダリングすることもできます。 インタラクティブPDFフォームをレンダリングするには、 `FormsServiceClient` オブジェクトの `renderPDFForm` メソッドまたは `renderPDFForm2` メソッドを呼び出します。

はオブジェクト `renderPDFForm` を使用 `URLSpec` します。 XDPファイルに対するコンテンツルートは、 `URLSpec` オブジェクトの `setContentRootURI` メソッドを使用してFormsサービスに渡されます。 フォームデザイン名( `formQuery`)は、別のパラメーター値として渡されます。 2つの値が連結され、フォームデザインの絶対参照が取得されます。

この `renderPDFForm2` メソッドは、レンダリングするXDPまたはPDFドキュメントを含む `com.adobe.idp.Document` インスタンスを受け取ります。

>[!NOTE]
>
>入力ドキュメントがPDFドキュメントの場合、タグ付きPDFランタイムオプションは設定できません。 入力ファイルがXDPファイルの場合は、タグ付きPDFオプションを設定できます。

## Java APIを使用してインタラクティブPDFフォームをレンダリングする {#render-an-interactive-pdf-form-using-the-java-api}

Forms API(Java)を使用してインタラクティブPDFフォームをレンダリングします。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-forms-client.jarなどのクライアントJARファイルを含めます。

1. フォームクライアントAPIオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `FormsServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. URI値の指定

   * コンストラクターを使用して、URI値を格納する `URLSpec` オブジェクトを作成します。
   * オブジェクトの `URLSpec``setApplicationWebRoot` メソッドを呼び出し、アプリケーションのWebルートを表すstring値を渡します。
   * オブ `URLSpec` ジェクトの `setContentRootURI` メソッドを呼び出し、コンテンツルートURI値を指定するstring値を渡します。 フォームデザインがコンテンツルートURI内にあることを確認します。 そうでない場合、Formsサービスは例外をスローします。 リポジトリを参照するには、を指定し `repository:///`ます。
   * オブジェクトの `URLSpec``setTargetURL` メソッドを呼び出し、フォームデータのポスト先のターゲットURL値を指定するstring値を渡します。 フォームデザインでターゲットURLを定義する場合は、空の文字列を渡すことができます。 演算を実行するために、フォームの送信先URLを指定することもできます。

1. フォームへのファイルの添付

   * コンストラクターを使用して、添付ファイルを格納する `java.util.HashMap` オブジェクトを作成します。
   * レンダリングされたフォームにアタッチする各ファイルに対して `java.util.HashMap` オブジェクトの `put` メソッドを呼び出します。 このメソッドに次の値を渡します。

      * 添付ファイルの名前（ファイル名拡張子を含む）を指定するstring値。
   * 添付ファイルを含む `com.adobe.idp.Document` オブジェクトです。

   >[!NOTE]
   >
   >フォームに添付するファイルごとに、この手順を繰り返します。 この手順はオプションです。添付ファイルを送信したくない `null` 場合は、この手順を渡すことができます。

1. インタラクティブPDFフォームのレンダリング

   オブジェクトの `FormsServiceClient``renderPDFForm` メソッドを呼び出し、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定するstring値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、完全なパス（など）を必ず指定してください `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * フォームとマージするデータを含む `com.adobe.idp.Document` オブジェクト。 データをマージしない場合は、空の `com.adobe.idp.Document` オブジェクトを渡します。
   * 実行時オプションを格納する `PDFFormRenderSpec` オブジェクト。 これはオプションのパラメーターで、実行時のオプションを指定しない `null` かどうかを指定できます。
   * Formsサービスに必要なURI値を含む `URLSpec` オブジェクトです。
   * 添付ファイルを格納する `java.util.HashMap` オブジェクトです。 これはオプションのパラメーターで、フォームにファイルを添付しない `null` かどうかを指定できます。

   この `renderPDFForm``FormsResult` メソッドは、クライアントのWebブラウザーに書き込む必要があるフォームデータストリームを含むオブジェクトを返します。

1. フォームデータストリームをクライアントのWebブラウザーに書き込みます

   * オブジェクトの `com.adobe.idp.Document` メソッドを呼び出して、 `FormsResult` オブジェクトを作成し `getOutputContent` ます。
   * メソッドを呼び出して、 `com.adobe.idp.Document` オブジェクトのコンテンツタイプを取得し `getContentType` ます。
   * メソッドを呼び出し、オブジェクトの `javax.servlet.http.HttpServletResponse` コンテンツタイプを渡すことで、 `setContentType``com.adobe.idp.Document` オブジェクトのコンテンツタイプを設定します。
   * オブジェクトの `javax.servlet.ServletOutputStream` メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに書き込むために使用する `javax.servlet.http.HttpServletResponse``getOutputStream` オブジェクトを作成します。
   * オブジェクトの `java.io.InputStream` メソッドを呼び出して、 `com.adobe.idp.Document` オブジェクトを作成 `getInputStream` します。
   * バイト配列を作成し、 `InputStream` オブジェクトの `read` メソッドを呼び出して、バイト配列を引数として渡すことで、フォームデータストリームを設定します。
   * オブジェクトの `javax.servlet.ServletOutputStream``write` メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに送信します。 バイト配列を `write` メソッドに渡します。

## WebサービスAPIを使用してインタラクティブPDFフォームをレンダリングする {#render-an-interactive-pdf-form-using-the-web-service-api}

Forms API（Webサービス）を使用してインタラクティブPDFフォームをレンダリングします。

1. プロジェクトファイルを含める

   * FormsサービスのWSDLを使用するJavaプロキシクラスを作成します。
   * クラスパスにJavaプロキシクラスを含めます。

1. フォームクライアントAPIオブジェクトの作成

   オブジェクトを作成し、認証値を設定し `FormsService` ます。

1. URI値の指定

   * コンストラクターを使用して、URI値を格納する `URLSpec` オブジェクトを作成します。
   * オブジェクトの `URLSpec``setApplicationWebRoot` メソッドを呼び出し、アプリケーションのWebルートを表すstring値を渡します。
   * オブ `URLSpec` ジェクトの `setContentRootURI` メソッドを呼び出し、コンテンツルートURI値を指定するstring値を渡します。 フォームデザインがコンテンツルートURI内にあることを確認します。 そうでない場合、Formsサービスは例外をスローします。 リポジトリを参照するには、を指定し `repository:///`ます。
   * オブジェクトの `URLSpec``setTargetURL` メソッドを呼び出し、フォームデータのポスト先のターゲットURL値を指定するstring値を渡します。 フォームデザインでターゲットURLを定義する場合は、空の文字列を渡すことができます。 演算を実行するために、フォームの送信先URLを指定することもできます。

1. フォームへのファイルの添付

   * コンストラクターを使用して、添付ファイルを格納する `java.util.HashMap` オブジェクトを作成します。
   * レンダリングされたフォームにアタッチする各ファイルに対して `java.util.HashMap` オブジェクトの `put` メソッドを呼び出します。 このメソッドに次の値を渡します。

      * 添付ファイルの名前（ファイル名拡張子を含む）を指定するstring値
   * 添付ファイルを含む `BLOB` オブジェクト

   >[!NOTE]
   >
   >フォームに添付するファイルごとに、この手順を繰り返します。

1. インタラクティブPDFフォームのレンダリング

   オブジェクトの `FormsService``renderPDFForm` メソッドを呼び出し、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定するstring値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、完全なパス（など）を必ず指定してください `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`。
   * フォームとマージするデータを含む `BLOB` オブジェクト。 データを結合したくない場合は、を渡し `null`ます。
   * 実行時オプションを格納する `PDFFormRenderSpec` オブジェクト。 これはオプションのパラメーターで、実行時のオプションを指定しない `null` かどうかを指定できます。
   * Formsサービスに必要なURI値を含む `URLSpec` オブジェクトです。
   * 添付ファイルを格納する `java.util.HashMap` オブジェクトです。 これはオプションのパラメーターで、フォームにファイルを添付しない `null` かどうかを指定できます。
   * メソッドによって入力される空の `com.adobe.idp.services.holders.BLOBHolder` オブジェクトです。 これは、レンダリングされたPDFフォームを保存するために使用します。
   * メソッドによって入力される空の `javax.xml.rpc.holders.LongHolder` オブジェクトです。 （この引数は、フォームのページ数を格納します。）
   * メソッドによって入力される空の `javax.xml.rpc.holders.StringHolder` オブジェクトです。 （この引数はロケールの値を格納します）。
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

**フォームデータストリームをクライアントのWebブラウザーに書き込みます**

Formsサービスは、フォームをレンダリングするときに、フォームデータストリームを返します。このデータストリームは、クライアントのWebブラウザーに書き込む必要があります。 クライアントのWebブラウザーに書き込まれると、フォームはユーザーに表示されます。
