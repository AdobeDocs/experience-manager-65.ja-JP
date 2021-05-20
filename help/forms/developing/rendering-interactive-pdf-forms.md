---
title: インタラクティブPDF formsのレンダリング
seo-title: インタラクティブPDF formsのレンダリング
description: Formsサービスを使用して、インタラクティブPDF formsをクライアントデバイス（通常はWebブラウザー）にレンダリングし、ユーザーから情報を収集します。 Formsサービスを使用して、Java APIとWebサービスAPIを使用してインタラクティブフォームをレンダリングできます。
seo-description: Formsサービスを使用して、インタラクティブPDF formsをクライアントデバイス（通常はWebブラウザー）にレンダリングし、ユーザーから情報を収集します。 Formsサービスを使用して、Java APIとWebサービスAPIを使用してインタラクティブフォームをレンダリングできます。
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
source-wordcount: '2528'
ht-degree: 0%

---

# インタラクティブPDF formsのレンダリング{#rendering-interactive-pdf-forms}

**このドキュメントのサンプルと例は、JEE上のAEM Forms環境に限られています。**

Formsサービスは、ユーザーから情報を収集するために、インタラクティブPDF formsをクライアントデバイス（通常はWebブラウザー）にレンダリングします。 インタラクティブフォームがレンダリングされたら、ユーザーはフォームフィールドにデータを入力し、フォーム上の送信ボタンをクリックして、情報をFormsサービスに送り返すことができます。 インタラクティブPDFフォームを表示するには、クライアントWebブラウザーをホストしているコンピューターにAdobe ReaderまたはAcrobatをインストールする必要があります。

>[!NOTE]
>
>Formsサービスを使用してフォームをレンダリングする前に、フォームデザインを作成します。 通常、フォームデザインはDesignerで作成され、XDPファイルとして保存されます。 フォームデザインの作成について詳しくは、[Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)を参照してください。

**サンプルのローン申し込み**

Formsサービスがインタラクティブフォームを使用してユーザーから情報を収集する方法を示す、サンプルのローン申し込みフォームが導入されています。 このアプリケーションを使用すると、ユーザーは、ローンの保護に必要なデータをフォームに入力し、データをFormsサービスに送信できます。 次の図に、ローン申し込みのロジックフローを示します。

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
   <td><p><code>GetLoanForm</code> JavaサーブレットがHTMLページから呼び出されます。 </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p><code>GetLoanForm</code> Javaサーブレットは、FormsサービスクライアントAPIを使用して、ローンフォームをクライアントWebブラウザーにレンダリングします。 （<a href="#render-an-interactive-pdf-form-using-the-java-api">Java API</a>を使用してインタラクティブPDFフォームをレンダリングするを参照）。</p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>ユーザーがローンフォームに入力して「送信」ボタンをクリックすると、データが<code>HandleData</code> Javaサーブレットに送信されます。 （<i>"Loan form"</i>を参照）。</p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p><code>HandleData</code> Javaサーブレットは、FormsサービスクライアントAPIを使用してフォーム送信を処理し、フォームデータを取得します。 その後、データはエンタープライズデータベースに保存されます。 (<a href="/help/forms/developing/handling-submitted-forms.md#handling-submitted-forms">送信されたForms</a>の処理を参照)。</p></td>
  </tr>
  <tr>
   <td><p>5</p></td>
   <td><p>確認フォームがWebブラウザーにレンダリングされます。 ユーザーの姓と名などのデータは、レンダリング前にフォームにマージされます。 (<a href="/help/forms/developing/prepopulating-forms-flowable-layouts.md">編集可能なレイアウトを使用したFormsの事前入力</a>を参照)。</p></td>
  </tr>
 </tbody>
</table>

**ローンフォーム**

このインタラクティブなローンフォームは、サンプルのローンアプリケーションの`GetLoanForm` Java Servletによってレンダリングされます。

![ri_ri_loanform](assets/ri_ri_loanform.png)

**確認フォーム**

このフォームは、サンプルのローンアプリケーションの`HandleData` Java Servletによってレンダリングされます。

![ri_ri_confirm](assets/ri_ri_confirm.png)

`HandleData` Javaサーブレットは、このフォームにユーザーの姓名と金額を事前入力します。 フォームが事前入力された後、クライアントのWebブラウザーに送信されます。 ([編集可能なレイアウトを使用したFormsの事前入力](/help/forms/developing/prepopulating-forms-flowable-layouts.md)を参照)。

**Javaサーブレット**

サンプルのローン申し込みは、Javaサーブレットとして存在するFormsサービスアプリケーションの例です。 Javaサーブレットは、WebSphereなどのJ2EEアプリケーションサーバー上で実行されるJavaプログラムで、FormsサービスのクライアントAPIコードを含みます。

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

通常、FormsサービスのクライアントAPIコードは、Javaサーブレットの`doGet`または`doPost`メソッド内に配置しません。 このコードを別のクラスに配置し、`doPost`メソッド（または`doGet`メソッド）内からクラスをインスタンス化して、適切なメソッドを呼び出す方が、プログラミングのベストプラクティスです。 ただし、コードを簡潔にするために、この節のコード例は最小限に抑え、コード例は`doPost`メソッドに配置します。

>[!NOTE]
>
>Formsサービスについて詳しくは、『 AEM Formsのサービスリファレンス[ 』を参照してください。](https://www.adobe.com/go/learn_aemforms_services_63)

**手順の概要**

インタラクティブPDFフォームをレンダリングするには、次のタスクを実行します。

1. プロジェクトファイルを含めます。
1. Forms Client APIオブジェクトを作成します。
1. URI値を指定します。
1. フォームにファイルを添付します（オプション）。
1. インタラクティブPDFフォームをレンダリングします。
1. フォームデータストリームをクライアントWebブラウザーに書き込みます。

**プロジェクトファイルを含める**

必要なファイルを開発プロジェクトに含めます。 Javaを使用してクライアントアプリケーションを作成する場合は、必要なJARファイルを含めます。 Webサービスを使用する場合は、プロキシファイルを必ず含めてください。

**Forms Client APIオブジェクトの作成**

プログラムでForms Service Client API操作を実行する前に、Forms Client APIオブジェクトを作成する必要があります。 Java APIを使用している場合は、`FormsServiceClient`オブジェクトを作成します。 Forms WebサービスAPIを使用している場合は、`FormsService`オブジェクトを作成します。

**URI値の指定**

Formsサービスでフォームをレンダリングするために必要なURI値を指定できます。 Formsアプリケーションの一部として保存されたフォームデザインは、コンテンツルートURI値`repository:///`を使用して参照できます。 例えば、*FormsApplication*&#x200B;という名前のFormsアプリケーション内にある&#x200B;*Loan.xdp*&#x200B;という名前のフォームデザインを考えてみましょう。

![ri_ri_formrepository](assets/ri_ri_formrepository.png)

このフォームデザインにアクセスするには、フォーム名（`renderPDFForm`メソッドに渡される最初のパラメーター）として`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`を指定し、コンテンツルートURI値として`repository:///`を指定します。

>[!NOTE]
>
>Workbenchを使用したFormsアプリケーションの作成について詳しくは、[Workbenchヘルプ](https://www.adobe.com/go/learn_aemforms_workbench_63)を参照してください。

Formsアプリケーション内のリソースへのパスは次のとおりです。

`Applications/Application-name/Application-version/Folder.../Filename`

次に、URI値の例を示します。

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

インタラクティブフォームをレンダリングする際に、フォームデータの投稿先となるターゲットURLなどのURI値を定義できます。 ターゲットURLは、次のいずれかの方法で定義できます。

* Designerでフォームデザインをデザインする際の「送信」ボタン
* FormsサービスクライアントAPIを使用する

ターゲットURLがフォームデザイン内で定義されている場合は、FormsサービスクライアントAPIを使用して上書きしないでください。 つまり、Forms APIを使用してターゲットURLを設定すると、フォームデザインで指定されたURLが、APIを使用して指定されたURLにリセットされます。 フォームデザインで指定されたターゲットURLにPDFフォームを送信する場合、プログラムによってターゲットURLを空の文字列に設定します。

送信ボタンと計算ボタン（サーバーで実行される対応するスクリプトを含む）を含むフォームがある場合、スクリプトを実行するためにフォームが送信されるURLをプログラムで定義できます。 フォームデザインの送信ボタンを使用して、フォームデータが投稿されるURLを指定します。 （[フォームデータの計算](/help/forms/developing/calculating-form-data.md)を参照）。

>[!NOTE]
>
>XDPファイルを参照するURL値を指定する代わりに、`com.adobe.idp.Document`インスタンスをFormsサービスに渡すこともできます。 `com.adobe.idp.Document`インスタンスにはフォームデザインが含まれています。 ([Formsサービスにドキュメントを渡す](/help/forms/developing/passing-documents-forms-service.md)を参照)。

**フォームにファイルを添付する**

フォームにファイルを添付できます。 添付ファイルを含むPDFフォームをレンダリングする場合、ユーザーは添付ファイルペインを使用してAcrobatで添付ファイルを取得できます。 フォームには、テキストファイルや、JPGファイルなどのバイナリファイルなど、様々なファイル形式を添付できます。

>[!NOTE]
>
>添付ファイルのフォームへの添付はオプションです。

**インタラクティブPDFフォームのレンダリング**

フォームをレンダリングするには、Designerで作成され、XDPまたはPDFファイルとして保存されたフォームデザインを使用します。 また、Acrobatを使用して作成され、PDFファイルとして保存されたフォームをレンダリングすることもできます。 インタラクティブPDFフォームをレンダリングするには、`FormsServiceClient`オブジェクトの`renderPDFForm`メソッドまたは`renderPDFForm2`メソッドを呼び出します。

`renderPDFForm`は`URLSpec`オブジェクトを使用します。 XDPファイルのコンテンツルートは、`URLSpec`オブジェクトの`setContentRootURI`メソッドを使用してFormsサービスに渡されます。 フォームデザイン名(`formQuery`)は、別のパラメーター値として渡されます。 2つの値が連結され、フォームデザインへの絶対参照が取得されます。

`renderPDFForm2`メソッドは、レンダリングするXDPまたはPDFドキュメントを含む`com.adobe.idp.Document`インスタンスを受け取ります。

>[!NOTE]
>
>入力ドキュメントがPDFドキュメントの場合、タグ付きPDFランタイムオプションは設定できません。 入力ファイルがXDPファイルの場合、タグ付きPDFオプションを設定できます。

## Java API {#render-an-interactive-pdf-form-using-the-java-api}を使用したインタラクティブPDFフォームのレンダリング

Forms API(Java)を使用してインタラクティブPDFフォームをレンダリングします。

1. プロジェクトファイルを含める

   Javaプロジェクトのクラスパスに、adobe-forms-client.jarなどのクライアントJARファイルを含めます。

1. Forms Client APIオブジェクトの作成

   * 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。
   * コンストラクターを使用して`FormsServiceClient`オブジェクトを渡し、`ServiceClientFactory`オブジェクトを作成します。

1. URI値の指定

   * コンストラクターを使用して、URI値を格納する`URLSpec`オブジェクトを作成します。
   * `URLSpec`オブジェクトの`setApplicationWebRoot`メソッドを呼び出して、アプリケーションのWebルートを表す文字列値を渡します。
   * `URLSpec`オブジェクトの`setContentRootURI`メソッドを呼び出し、コンテンツルートURI値を指定する文字列値を渡します。 フォームデザインがコンテンツルートURIに配置されていることを確認します。 そうでない場合、Formsサービスは例外をスローします。 リポジトリを参照するには、`repository:///`を指定します。
   * `URLSpec`オブジェクトの`setTargetURL`メソッドを呼び出し、フォームデータの投稿先となるターゲットURL値を指定する文字列値を渡します。 フォームデザインでターゲットURLを定義する場合は、空の文字列を渡すことができます。 演算を実行するためのフォームの送信先URLを指定することもできます。

1. フォームにファイルを添付する

   * コンストラクタを使用して、添付ファイルを格納する`java.util.HashMap`オブジェクトを作成します。
   * レンダリングされたフォームに添付する各ファイルに対して、 `java.util.HashMap`オブジェクトの`put`メソッドを呼び出します。 このメソッドに次の値を渡します。

      * 添付ファイルの名前（ファイル名拡張子を含む）を指定するstring値。
   * 添付ファイルを含む`com.adobe.idp.Document`オブジェクト。

   >[!NOTE]
   >
   >フォームに添付するファイルごとに、この手順を繰り返します。 この手順はオプションで、添付ファイルを送信しない場合は`null`を渡すことができます。

1. インタラクティブPDFフォームのレンダリング

   `FormsServiceClient`オブジェクトの`renderPDFForm`メソッドを呼び出し、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定するstring値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、必ず`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`のように完全なパスを指定してください。
   * フォームとマージするデータを含む`com.adobe.idp.Document`オブジェクト。 データを結合しない場合は、空の`com.adobe.idp.Document`オブジェクトを渡します。
   * 実行時オプションを格納する`PDFFormRenderSpec`オブジェクト。 これはオプションのパラメーターで、実行時オプションを指定しない場合は`null`を指定できます。
   * Formsサービスに必要なURI値を含む`URLSpec`オブジェクト。
   * 添付ファイルを格納する`java.util.HashMap`オブジェクト。 これはオプションのパラメーターで、フォームにファイルを添付しない場合は`null`を指定できます。

   `renderPDFForm`メソッドは、クライアントのWebブラウザーに書き込む必要があるフォームデータストリームを含む`FormsResult`オブジェクトを返します。

1. フォームデータストリームをクライアントWebブラウザーに書き込む

   * `FormsResult`オブジェクトの`getOutputContent`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトを作成します。
   * `getContentType`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトのコンテンツタイプを取得します。
   * `setContentType`メソッドを呼び出し、`com.adobe.idp.Document`オブジェクトのコンテンツタイプを渡すことで、`javax.servlet.http.HttpServletResponse`オブジェクトのコンテンツタイプを設定します。
   * `javax.servlet.http.HttpServletResponse`オブジェクトの`getOutputStream`メソッドを呼び出して、フォームデータストリームをクライアントWebブラウザーに書き込むための`javax.servlet.ServletOutputStream`オブジェクトを作成します。
   * `com.adobe.idp.Document`オブジェクトの`getInputStream`メソッドを呼び出して、`java.io.InputStream`オブジェクトを作成します。
   * `InputStream`オブジェクトの`read`メソッドを呼び出し、バイト配列を引数として渡すことで、バイト配列を作成し、フォームデータストリームに入力します。
   * `javax.servlet.ServletOutputStream`オブジェクトの`write`メソッドを呼び出して、フォームデータストリームをクライアントWebブラウザーに送信します。 `write`メソッドにバイト配列を渡します。

## WebサービスAPI {#render-an-interactive-pdf-form-using-the-web-service-api}を使用してインタラクティブPDFフォームをレンダリングする

Forms API（Webサービス）を使用してインタラクティブPDFフォームをレンダリングします。

1. プロジェクトファイルを含める

   * FormsサービスのWSDLを使用するJavaプロキシクラスを作成します。
   * Javaプロキシクラスをクラスパスに含めます。

1. Forms Client APIオブジェクトの作成

   `FormsService`オブジェクトを作成し、認証値を設定します。

1. URI値の指定

   * コンストラクターを使用して、URI値を格納する`URLSpec`オブジェクトを作成します。
   * `URLSpec`オブジェクトの`setApplicationWebRoot`メソッドを呼び出して、アプリケーションのWebルートを表す文字列値を渡します。
   * `URLSpec`オブジェクトの`setContentRootURI`メソッドを呼び出し、コンテンツルートURI値を指定する文字列値を渡します。 フォームデザインがコンテンツルートURIに配置されていることを確認します。 そうでない場合、Formsサービスは例外をスローします。 リポジトリを参照するには、`repository:///`を指定します。
   * `URLSpec`オブジェクトの`setTargetURL`メソッドを呼び出し、フォームデータの投稿先となるターゲットURL値を指定する文字列値を渡します。 フォームデザインでターゲットURLを定義する場合は、空の文字列を渡すことができます。 演算を実行するためのフォームの送信先URLを指定することもできます。

1. フォームにファイルを添付する

   * コンストラクタを使用して、添付ファイルを格納する`java.util.HashMap`オブジェクトを作成します。
   * レンダリングされたフォームに添付する各ファイルに対して、 `java.util.HashMap`オブジェクトの`put`メソッドを呼び出します。 このメソッドに次の値を渡します。

      * 添付ファイルの名前（ファイル名拡張子を含む）を指定するstring値
   * 添付ファイルを含む`BLOB`オブジェクト

   >[!NOTE]
   >
   >フォームに添付するファイルごとに、この手順を繰り返します。

1. インタラクティブPDFフォームのレンダリング

   `FormsService`オブジェクトの`renderPDFForm`メソッドを呼び出し、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定するstring値。 Formsアプリケーションの一部であるフォームデザインを参照する場合は、必ず`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`のように完全なパスを指定してください。
   * フォームとマージするデータを含む`BLOB`オブジェクト。 データを結合しない場合は、`null`を渡します。
   * 実行時オプションを格納する`PDFFormRenderSpec`オブジェクト。 これはオプションのパラメーターで、実行時オプションを指定しない場合は`null`を指定できます。
   * Formsサービスに必要なURI値を含む`URLSpec`オブジェクト。
   * 添付ファイルを格納する`java.util.HashMap`オブジェクト。 これはオプションのパラメーターで、フォームにファイルを添付しない場合は`null`を指定できます。
   * メソッドで設定される空の`com.adobe.idp.services.holders.BLOBHolder`オブジェクト。 これは、レンダリングされたPDFフォームを保存するために使用されます。
   * メソッドで設定される空の`javax.xml.rpc.holders.LongHolder`オブジェクト。 （この引数は、フォームのページ数を保存します。）
   * メソッドで設定される空の`javax.xml.rpc.holders.StringHolder`オブジェクト。 （この引数はロケール値を格納します。）
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

**フォームデータストリームをクライアントWebブラウザーに書き込む**

Formsサービスは、フォームをレンダリングする際に、クライアントのWebブラウザーに書き込む必要があるフォームデータストリームを返します。 クライアントのWebブラウザーに書き込まれると、フォームはユーザーに表示されます。
