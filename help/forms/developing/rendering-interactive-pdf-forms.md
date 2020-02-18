---
title: インタラクティブPDFフォームのレンダリング
seo-title: インタラクティブPDFフォームのレンダリング
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
source-git-commit: 7cbe3e94eddb81925072f68388649befbb027e6d

---


# インタラクティブPDFフォームのレンダリング {#rendering-interactive-pdf-forms}

Formsサービスは、ユーザーから情報を収集するために、インタラクティブPDFフォームをクライアントデバイス（通常はWebブラウザー）にレンダリングします。 インタラクティブフォームがレンダリングされた後、ユーザーはフォームフィールドにデータを入力し、フォーム上の送信ボタンをクリックして、Formsサービスに情報を送り返すことができます。 インタラクティブPDFフォームを表示するには、クライアントWebブラウザーをホストするコンピューターにAdobe readerまたはAcrobatがインストールされている必要があります。

>[!NOTE]
>
>Formsサービスを使用してフォームをレンダリングする前に、フォームデザインを作成します。 通常、フォームデザインはDesignerで作成され、XDPファイルとして保存されます。 フォームデザインの作成について詳しくは、「 [Forms Designer」を参照してください](https://www.adobe.com/go/learn_aemforms_designer_63)。

**ローン申し込みの例**

Formsサービスがインタラクティブフォームを使用してユーザーから情報を収集する方法を示すローン申し込みのサンプルが紹介されています。 このアプリケーションを使用すると、ユーザーはローンのセキュリティ保護に必要なデータをフォームに入力し、データをFormsサービスに送信できます。 次の図に、ローン申し込みのロジックのフローを示します。

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
   <td><p>Javaサーブ <code>GetLoanForm</code> レットがHTMLページから呼び出されます。 </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Javaサーブ <code>GetLoanForm</code> レットは、FormsサービスクライアントAPIを使用して、ローンフォームをクライアントWebブラウザーにレンダリングします。 (Java APIを使 <a href="#render-an-interactive-pdf-form-using-the-java-api">用したインタラクティブPDFフォームのレンダリングを参照</a>)。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>ユーザーがローンフォームに入力し、「送信」ボタンをクリックすると、データが <code>HandleData</code> Javaサーブレットに送信されます。 (「ロ <i>ーンフォーム」を参照</i>)。</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Javaサーブ <code>HandleData</code> レットは、FormsサービスクライアントAPIを使用してフォーム送信を処理し、フォームデータを取得します。 その後、データはエンタープライズデータベースに保存されます。 (「送信済み <a href="/help/forms/developing/handling-submitted-forms.md#handling-submitted-forms">フォームの処理</a>」を参照)。</p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>確認フォームがWebブラウザーにレンダリングされます。 ユーザーの姓や名などのデータは、レンダリング前にフォームにマージされます。 (「編集可能な <a href="/help/forms/developing/prepopulating-forms-flowable-layouts.md">レイアウトでのフォームの自動埋め込み</a>」を参照)。</p></td>
  </tr>
 </tbody>
</table>

**ローンフォーム**

このインタラクティブローンフォームは、サンプルローンアプリケーションの `GetLoanForm` Javaサーブレットによってレンダリングされます。

![ri_ri_loanform](assets/ri_ri_loanform.png)

**確認フォーム**

このフォームは、サンプルローンアプリケーションの `HandleData` Javaサーブレットによってレンダリングされます。

![ri_ri_confirm](assets/ri_ri_confirm.png)

Javaサーブ `HandleData` レットは、このフォームにユーザーの姓と名と金額を事前設定します。 フォームにデータが事前入力されると、クライアントWebブラウザーに送信されます。 (編集可能なレ [イアウトでのフォームの自動埋め込みを参照](/help/forms/developing/prepopulating-forms-flowable-layouts.md))。

**Javaサーブレット**

サンプルのローン申込書は、Javaサーブレットとして存在するFormsサービスアプリケーションの例です。 Javaサーブレットは、WebSphereなどのJ2EEアプリケーションサーバー上で実行されるJavaプログラムで、FormsサービスクライアントAPIコードが含まれています。

次のコードは、GetLoanFormという名前のJavaサーブレットの構文を示しています。

```as3
     public class GetLoanForm extends HttpServlet implements Servlet {
         public void doGet(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {

         }
         public void doPost(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {

             }
```

通常は、FormsサービスのクライアントAPIコードをJavaサーブレットのメソッドまたはメソッド内に配置 `doGet` しま `doPost` せん。 このコードを別のクラスに配置し、メソッド（またはメソッド）内からクラスをインスタンス化し、適切なメソッドを呼び出す方 `doPost` 法が `doGet` 、より良いプログラミング方法です。 ただし、コードを簡潔にするために、この節のコード例は最小限に抑え、コード例はメソッドに配置し `doPost` ます。

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
1. クライアントのWebブラウザーにフォームデータストリームを書き込みます。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用している場合は、必ずプロキシファイルを含めてください。

**フォームクライアントAPIオブジェクトの作成**

プログラムでFormsサービスのClient API操作を実行する前に、Forms Client APIオブジェクトを作成する必要があります。 Java APIを使用している場合は、オブジェクトを作成し `FormsServiceClient` ます。 Forms webサービスAPIを使用している場合は、オブジェクトを作成し `FormsService` ます。

**URI値の指定**

Formsサービスでフォームをレンダリングするために必要なURI値を指定できます。 Formsアプリケーションの一部として保存されたフォームデザインは、コンテンツルートURI値を使用して参照できま `repository:///`す。 例えば、FormsApplicationというFormsアプリケーション内にある *Loan.xdp* という名前の次のフォームデザインを考えてみ *ます*。

![ri_ri_formrepository](assets/ri_ri_formrepository.png)

このフォームデザインにアクセスす `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp` るには、フォーム名（メソッドに渡される最初のパラメーター）と `renderPDFForm` コンテンツル `repository:///` ートURI値を指定します。

>[!NOTE]
>
>Workbenchを使用したFormsアプリケーションの作成について詳しくは、Workbenchヘルプを [参照してくださ](https://www.adobe.com/go/learn_aemforms_workbench_63)い。

Formsアプリケーション内のリソースへのパスは次のとおりです。

`Applications/Application-name/Application-version/Folder.../Filename`

次に、URI値の例を示します。

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

インタラクティブフォームをレンダリングする際に、フォームデータが投稿されるターゲットURLなどのURI値を定義できます。 ターゲットURLは、次のいずれかの方法で定義できます。

* Designerでフォームデザインをデザイン中の「送信」ボタン
* FormsサービスクライアントAPIを使用する

ターゲットURLがフォームデザイン内で定義されている場合は、FormsサービスクライアントAPIで上書きしないでください。 つまり、Forms APIを使用してターゲットURLを設定すると、フォームデザインで指定されたURLが、APIを使用して指定されたURLにリセットされます。 フォームデザインで指定されたターゲットURLにPDFフォームを送信する場合は、プログラムによってターゲットURLを空の文字列に設定します。

送信ボタンと計算ボタン（サーバーで実行される対応するスクリプトを含む）を含むフォームがある場合、フォームが送信されるスクリプトの実行先のURLをプログラムで定義できます。 フォームデザインの送信ボタンを使用して、フォームデータが投稿されるURLを指定します。 (フォーム [データの計算を参照](/help/forms/developing/calculating-form-data.md))。

>[!NOTE]
>
>XDPファイルを参照するURL値を指定する代わりに、Formsサービスにインスタンスを渡す `com.adobe.idp.Document` こともできます。 インスタ `com.adobe.idp.Document` ンスにフォームデザインが含まれます。 (「Formsサー [ビスへのドキュメントの引き渡し](/help/forms/developing/passing-documents-forms-service.md)」を参照)。

**フォームへのファイルの添付**

フォームにファイルを添付できます。 添付ファイルを含むPDFフォームをレンダリングする場合、ユーザーは添付ファイルパネルを使用してAcrobatで添付ファイルを取得できます。 テキストファイルや、JPGファイルなどのバイナリファイルに、様々な種類のファイルをフォームに添付できます。

>[!NOTE]
>
>添付ファイルのフォームへの添付はオプションです。

**インタラクティブPDFフォームのレンダリング**

フォームをレンダリングするには、Designerで作成され、XDPまたはPDFファイルとして保存されたフォームデザインを使用します。 また、Acrobatを使用して作成し、PDFファイルとして保存したフォームをレンダリングすることもできます。 インタラクティブPDFフォームをレンダリングするには、オブジェクト `FormsServiceClient` のメソッドまたはメソ `renderPDFForm` ッドを呼び出 `renderPDFForm2` します。

はオブジ `renderPDFForm` ェクトを使用 `URLSpec` します。 XDPファイルのコンテンツルートは、オブジェクトのメソッドを使用してFormsサー `URLSpec` ビスに渡さ `setContentRootURI` れます。 フォームデザイン名( `formQuery`)は、別のパラメーター値として渡されます。 2つの値が連結され、フォームデザインへの絶対参照が取得されます。

このメソ `renderPDFForm2` ッドは、レンダ `com.adobe.idp.Document` リングするXDPまたはPDFドキュメントを含むインスタンスを受け入れます。

>[!NOTE]
>
>入力ドキュメントがPDFドキュメントの場合、タグ付きPDFの実行時オプションを設定できません。 入力ファイルがXDPファイルの場合は、タグ付きPDFオプションを設定できます。

## Java APIを使用したインタラクティブPDFフォームのレンダリング {#render-an-interactive-pdf-form-using-the-java-api}

Forms API(Java)を使用してインタラクティブPDFフォームをレンダリングします。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-forms-client.jarなどのクライアントJARファイルを含めます。

1. フォームクライアントAPIオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * Create an `FormsServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. URI値の指定

   * コンストラク `URLSpec` ターを使用して、URI値を格納するオブジェクトを作成します。
   * オブジェクト `URLSpec` のメソッドを `setApplicationWebRoot` 呼び出し、アプリケーションのWebルートを表すstring値を渡します。
   * オブジェクト `URLSpec` のメソッドを `setContentRootURI` 呼び出し、コンテンツルートURI値を指定するstring値を渡します。 フォームデザインがコンテンツルートURI内にあることを確認します。 そうでない場合、Formsサービスは例外をスローします。 リポジトリを参照するには、を指定しま `repository:///`す。
   * オブジェクト `URLSpec` のメソッ `setTargetURL` ドを呼び出し、フォームデータの投稿先のターゲットURL値を指定するstring値を渡します。 フォームデザインでターゲットURLを定義する場合は、空の文字列を渡すことができます。 演算を実行するためにフォームの送信先URLを指定することもできます。

1. フォームへのファイルの添付

   * コンストラクタ `java.util.HashMap` ーを使用して、添付ファイルを格納するオブジェクトを作成します。
   * レンダリングさ `java.util.HashMap` れたフォームにア `put` タッチする各ファイルに対して、オブジェクトのメソッドを呼び出します。 このメソッドに次の値を渡します。

      * 添付ファイルの名前（ファイル名拡張子を含む）を指定するstring値。
   * 添付フ `com.adobe.idp.Document` ァイルを含むオブジェクトです。
   >[!NOTE]
   >
   >フォームに添付するファイルごとに、この手順を繰り返します。 この手順はオプションで、添付ファイルを送 `null` 信しない場合は渡すことができます。

1. インタラクティブPDFフォームのレンダリング

   オブジェクト `FormsServiceClient` のメソッドを `renderPDFForm` 呼び出し、次の値を渡します。

   * ファイル名の拡張子を含むフォームデザイン名を指定するstring値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、必ずなどの完全なパスを指定してくださ `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`い。
   * フォーム `com.adobe.idp.Document` とマージするデータを含むオブジェクトです。 データをマージしない場合は、空のオブジェクトを渡し `com.adobe.idp.Document` ます。
   * 実行時 `PDFFormRenderSpec` のオプションを格納するオブジェクトです。 これはオプションのパラメーターで、実行時 `null` のオプションを指定しないかどうかを指定できます。
   * Formsサ `URLSpec` ービスに必要なURI値を含むオブジェクトです。
   * 添付フ `java.util.HashMap` ァイルを格納するオブジェクト。 これはオプションのパラメーターで、フォームにフ `null` ァイルを添付しないかどうかを指定できます。
   このメソ `renderPDFForm` ッドは、クライア `FormsResult` ントのWebブラウザーに書き込む必要があるフォームデータストリームを含むオブジェクトを返します。

1. クライアントのWebブラウザーにフォームデータストリームを書き込みます

   * オブジェクトの `com.adobe.idp.Document` メソッドを呼び出して、オ `FormsResult` ブジェクトを作成 `getOutputContent` します。
   * メソッドを呼び出して、オブジェ `com.adobe.idp.Document` クトのコンテンツタイプを取得 `getContentType` します。
   * メソッドを呼 `javax.servlet.http.HttpServletResponse` び出し、オブジェクトのコンテンツタ `setContentType` イプを渡すことで、オブジェクトのコンテンツタイプを設定 `com.adobe.idp.Document` します。
   * オブジェクトの `javax.servlet.ServletOutputStream` メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに書き込むために使用する `javax.servlet.http.HttpServletResponse` オブジェクトを作 `getOutputStream` 成します。
   * オブジェクト `java.io.InputStream` のメソッドを呼び出して、オ `com.adobe.idp.Document` ブジェクトを作成 `getInputStream` します。
   * バイト配列を作成し、オブジェクトのメソッドを呼び出し、バイト配列を引数 `InputStream` として渡すこ `read` とで、フォームデータストリームを設定します。
   * オブジェクト `javax.servlet.ServletOutputStream` のメソッドを呼び `write` 出して、フォームデータストリームをクライアントWebブラウザーに送信します。 バイト配列をメソッドに渡し `write` ます。

## WebサービスAPIを使用してインタラクティブPDFフォームをレンダリングする {#render-an-interactive-pdf-form-using-the-web-service-api}

Forms API（Webサービス）を使用してインタラクティブPDFフォームをレンダリングします。

1. プロジェクトファイルを含める

   * FormsサービスWSDLを使用するJavaプロキシクラスを作成します。
   * クラスパスにJavaプロキシクラスを含めます。

1. フォームクライアントAPIオブジェクトの作成

   オブジェクト `FormsService` を作成し、認証値を設定します。

1. URI値の指定

   * コンストラク `URLSpec` ターを使用して、URI値を格納するオブジェクトを作成します。
   * オブジェクト `URLSpec` のメソッドを `setApplicationWebRoot` 呼び出し、アプリケーションのWebルートを表すstring値を渡します。
   * オブジェクト `URLSpec` のメソッドを `setContentRootURI` 呼び出し、コンテンツルートURI値を指定するstring値を渡します。 フォームデザインがコンテンツルートURI内にあることを確認します。 そうでない場合、Formsサービスは例外をスローします。 リポジトリを参照するには、を指定しま `repository:///`す。
   * オブジェクト `URLSpec` のメソッ `setTargetURL` ドを呼び出し、フォームデータの投稿先のターゲットURL値を指定するstring値を渡します。 フォームデザインでターゲットURLを定義する場合は、空の文字列を渡すことができます。 演算を実行するためにフォームの送信先URLを指定することもできます。

1. フォームへのファイルの添付

   * コンストラクタ `java.util.HashMap` ーを使用して、添付ファイルを格納するオブジェクトを作成します。
   * レンダリングさ `java.util.HashMap` れたフォームにア `put` タッチする各ファイルに対して、オブジェクトのメソッドを呼び出します。 このメソッドに次の値を渡します。

      * 添付ファイルの名前（ファイル名拡張子を含む）を指定するstring値
   * 添付フ `BLOB` ァイルを含むオブジェクト
   >[!NOTE]
   >
   >フォームに添付するファイルごとに、この手順を繰り返します。

1. インタラクティブPDFフォームのレンダリング

   オブジェクト `FormsService` のメソッドを `renderPDFForm` 呼び出し、次の値を渡します。

   * ファイル名の拡張子を含むフォームデザイン名を指定するstring値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、必ずなどの完全なパスを指定してくださ `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`い。
   * フォーム `BLOB` とマージするデータを含むオブジェクトです。 データを結合しない場合は、を渡します `null`。
   * 実行時 `PDFFormRenderSpec` のオプションを格納するオブジェクトです。 これはオプションのパラメーターで、実行時 `null` のオプションを指定しないかどうかを指定できます。
   * Formsサ `URLSpec` ービスに必要なURI値を含むオブジェクトです。
   * 添付フ `java.util.HashMap` ァイルを格納するオブジェクト。 これはオプションのパラメーターで、フォームにフ `null` ァイルを添付しないかどうかを指定できます。
   * メソッドに `com.adobe.idp.services.holders.BLOBHolder` よって入力される空のオブジェクトです。 これは、レンダリングされたPDFフォームを保存するために使用します。
   * メソッドに `javax.xml.rpc.holders.LongHolder` よって入力される空のオブジェクトです。 （この引数は、フォーム内のページ数を格納します。）
   * メソッドに `javax.xml.rpc.holders.StringHolder` よって入力される空のオブジェクトです。 （この引数はロケールの値を格納します。）
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

**クライアントのWebブラウザーにフォームデータストリームを書き込みます**

Formsサービスは、フォームをレンダリングすると、クライアントのWebブラウザーに書き込む必要があるフォームデータストリームを返します。 クライアントのWebブラウザーに書き込むと、フォームがユーザーに表示されます。
