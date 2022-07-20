---
title: Forms をレンダリングする web アプリケーションの作成
seo-title: Creating Web Applications thatRenders Forms
description: Java サーブレットを使用して Forms サービスを呼び出し、フォームをレンダリングする web ベースのアプリケーションを作成します。Java サーブレットは、フォームを返す Forms サービスとクライアント Web ブラウザーの間のリンクとして機能します。
seo-description: Create a web-based application that uses Java servlets to invoke the Forms service and render forms. The Java servlet serves as the link between the Forms service that returns a form and a client web browser.
uuid: 00de10c5-79bd-4d8a-ae18-32f1fd2623bf
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: f29b089e-8902-4744-81c5-15ee41ba8069
role: Developer
exl-id: 85e00003-8c8b-463a-b728-66af174be295
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '1874'
ht-degree: 100%

---

# Forms をレンダリングする web アプリケーションの作成 {#creating-web-applications-thatrenders-forms}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

## Forms をレンダリングする web アプリケーションの作成 {#creating-web-applications-that-renders-forms}

Java サーブレットを使用して Forms サービスを呼び出し、フォームをレンダリングする web ベースのアプリケーションを作成できます。Java™ サーブレットを使用する利点の 1 つは、プロセスの戻り値をクライアント Web ブラウザーに書き込める点です。つまり、フォームを返す Forms サービスとクライアント Web ブラウザーの間のリンクとして Java サーブレットを使用できます。

>[!NOTE]
>
>ここでは、Forms サービスを呼び出し、フラグメントに基づいてフォームをレンダリングする Java サーブレットを使用する Web ベースのアプリケーションを作成する方法について説明します（[フラグメントに基づいた Forms のレンダリング](/help/forms/developing/rendering-forms-based-fragments.md)を参照してください）。

Java サーブレットを使用すると、顧客がフォームにデータを表示して入力できるように、フォームをクライアント Web ブラウザーに書き込むことができます。フォームにデータを入力した後、Web ユーザーはフォーム上の送信ボタンをクリックして、情報を Java サーブレットに送り返し、データを取得して処理できます。例えば、別のプロセスにデータを送信できます。

ここでは、次の図に示すように、米国ベースのフォームデータとカナダベースのフォームデータのいずれかを選択できる Web ベースのアプリケーションを作成する方法について説明します。

![cw_cw_fragmentwebclient](assets/cw_cw_fragmentwebclient.png)

レンダリングされるフォームは、フラグメントに基づくフォームです。つまり、ユーザーが米国のデータを選択した場合、返されるフォームは米国のデータに基づくフラグメントを使用します。例えば、次の図に示すように、フォームのフッターにはアメリカの住所が含まれています。

![cw_cw_fragmentformfooter](assets/cw_cw_fragementformfooter.png)

同様に、ユーザーがカナダのデータを選択した場合、返されるフォームには、次の図に示すように、カナダの住所が含まれます。

![cw_fragmentformfootercnd](assets/cw_cw_fragementformfootercnd.png)

>[!NOTE]
>
>フラグメントを基にしたフォームデザインの作成について詳しくは、[Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63_jp) を参照してください。

**サンプルファイル**

このセクションでは、次の場所にあるサンプルファイルを使用します。

&lt;*Forms Designer のインストールディレクトリ*>/Samples/Forms/Purchase Order/Form Fragments

ここで、&lt;*インストールディレクトリ*>はインストールパスです。クライアントアプリケーションの目的上、Purchase Order Dynamic.xdp ファイルはこのインストール場所からコピーされ、*Applications/FormsApplication* という名前の Forms アプリケーションにデプロイされました。Purchase Order Dynamic.xdp ファイルは、FormsFolder という名前のフォルダーに配置されます。同様に、フラグメントは、次の図に示すように、Fragments という名前のフォルダーに配置されます。

![cw_cw_fragmentsrepository](assets/cw_cw_fragmentsrepository.png)

Purchase Order Dynamic.xdp フォームデザインにアクセスするには、`Applications/FormsApplication/1.0/FormsFolder/Purchase Order Dynamic.xdp` をフォーム名（`renderPDFForm` メソッドに渡される 1 番目のパラメーター）として指定し、`repository:///` をコンテンツルート URI 値として設定します。

Web アプリケーションで使用される XML データファイルが Data フォルダーから `C:\Adobe`（AEM Forms をホストする J2EE アプリケーションサーバーに属するファイルシステム）に移動されました。ファイル名は「Purchase Order *Canada.xml*」および「Purchase Order *US.xml*」です。

>[!NOTE]
>
>Workbench を使用した Forms アプリケーションの作成について詳しくは、[Workbench ヘルプ](https://www.adobe.com/go/learn_aemforms_workbench_63_jp)を参照してください。

### 手順の概要 {#summary-of-steps}

フラグメントに基づいて Forms をレンダリングする Web ベースのアプリケーションを作成するには、次の手順を実行します。

1. 新規 web プロジェクトを作成します。
1. Java サーブレットを表す Java アプリケーションロジックを作成します。
1. Web アプリケーション用の Web ページを作成します。
1. Web アプリケーションを WAR ファイルにパッケージ化します。
1. J2EE アプリケーションサーバーに WAR ファイルをデプロイします。
1. Web アプリケーションをテストします。

>[!NOTE]
>
>これらの手順の一部は、AEM Forms がデプロイされている J2EE アプリケーションによって異なります。例えば、WAR ファイルのデプロイ方法は、使用している J2EE アプリケーションサーバーによって異なります。この節では、AEM Forms が JBoss® にデプロイされていることを前提としています。

### Web プロジェクトの作成 {#creating-a-web-project}

Forms サービスを呼び出す Java サーブレットを含む Web アプリケーションを作成する最初の手順は、新しい Web プロジェクトを作成することです。このドキュメントの基になる Java IDE は Eclipse 3.3 です。Eclipse IDE を使用して、Web プロジェクトを作成し、必要な JAR ファイルをプロジェクトに追加します。最後に、*index.html* という名前の HTML ページと Java サーブレットをプロジェクトに追加します。

次のリストは、Web プロジェクトに追加する必要がある JAR ファイルを指定します。

* adobe-forms-client.jar
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar

これらのファイルの場所については、[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。

**新しい web プロジェクトを作成するには、次の手順を実行します。**

1. Eclipse を起動し、**ファイル**／**新規プロジェクト**&#x200B;をクリックします。
1. **新規プロジェクト**&#x200B;ダイアログボックスで、**Web**／**ダイナミック Web プロジェクト**&#x200B;を選択します。
1. `FragmentsWebApplication` をプロジェクト名を入力し、「**完了**」をクリックします。

**必要な JAR ファイルをプロジェクトに追加するには、次の手順に従います。**

1. プロジェクトエクスプローラウィンドウで、`FragmentsWebApplication` プロジェクトを右クリックして&#x200B;**プロパティ**&#x200B;を選択します。
1. 「**Java ビルドパス**」をクリックしてから「**ライブラリ**」タブをクリックします。
1. 「**外部 JAR を追加**」ボタンをクリックし、含める JAR ファイルを参照します。

**Java サーブレットをプロジェクトに追加するには、次の手順を実行します。**

1. プロジェクトエクスプローラウィンドウで、`FragmentsWebApplication` プロジェクトを右クリックして、**新規**／**その他**&#x200B;を選択します。
1. **Web** フォルダーを展開し、「**Servlet**」を選択してから「**次へ**」をクリックします。
1. サーブレットを作成ダイアログボックスで、`RenderFormFragment` をサーブレット名として入力してから「**完了**」をクリックします。

**プロジェクトに HTML ページを追加するには、次の手順を実行します。**

1. プロジェクトエクスプローラウィンドウで、`FragmentsWebApplication` プロジェクトを右クリックして、**新規**／**その他**&#x200B;を選択します。
1. **Web** フォルダーを展開して、**HTML** を選択し、**次へ**&#x200B;をクリックします。
1. 新しい HTML ダイアログボックスで、ファイル名に `index.html` と入力してから「**完了**」をクリックします。 

>[!NOTE]
>
>`RenderFormFragment` Java サーブレットを呼び出す HTML ページの作成に関する情報については、[Web ページの作成](/help/forms/developing/rendering-forms.md#creating-the-web-page)を参照してください。

### サーブレットの Java アプリケーションロジックの作成 {#creating-java-application-logic-for-the-servlet}

Java サーブレット内から Forms サービスを呼び出す Java アプリケーションロジックを作成します。次のコードは、`RenderFormFragment` Java サーブレットの構文を示します。

```java
     public class RenderFormFragment extends HttpServlet implements Servlet {
         public void doGet(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {
         doPost(req,resp);
 
         }
         public void doPost(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {
             //Add code here to invoke the Forms service
             }
```

通常、Java サーブレットの `doGet` または `doPost` メソッドにはクライアントコードを配置しません。より優れたプログラミング方法は、このコードを別のクラスに配置し、`doPost` メソッド（または `doGet` メソッド）内からクラスをインスタンス化し、適切なメソッドを呼び出すことです。ただし、コードを簡潔にするため、このセクションのコード例は最低限に抑えられており、コード例は `doPost` メソッドに配置されています。

Forms サービス API を使用してフラグメントに基づいてフォームをレンダリングするには、次のタスクを実行します。

1. adobe-livecycle-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。これらのファイルの場所については、[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。
1. HTML フォームから送信されたラジオボタンの値を取得し、米国データとカナダデータのどちらを使用するかを指定します。米国データが送信された場合、*Purchase Order US.xml* のデータを格納する `com.adobe.idp.Document` を作成します。同様に、カナダの場合は、*Purchase Order Canada.xml* ファイルのデータを格納する `com.adobe.idp.Document` を作成します。
1. 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します（[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照）
1. コンストラクターを使用して `ServiceClientFactory` オブジェクトを渡すことによって、`FormsServiceClient` オブジェクトを作成します。
1. コンストラクターを使用して、URI 値を格納する `URLSpec` オブジェクトを作成します。
1. `URLSpec` オブジェクトの `setApplicationWebRoot` メソッドを呼び出して、アプリケーションの web ルートを表す文字列値を渡します。
1. `URLSpec` オブジェクトの `setContentRootURI` メソッドを呼び出して、コンテンツルート URI 値を指定する文字列値を渡します。フォームデザインとフラグメントがコンテンツルート URI に配置されていることを確認します。そうでない場合、Forms サービスは例外をスローします。AEM Forms リポジトリを参照するには、`repository://` を指定してください。
1. `URLSpec` オブジェクトの `setTargetURL` メソッドを呼び出して、フォームデータの送信先となるターゲット URL 値を指定する文字列値を渡します。フォームデザインでターゲット URL を定義する場合、空の文字列を渡すことができます。また、計算を実行するためのフォームの送信先の URL を指定することもできます。
1. `FormsServiceClient` オブジェクトの `renderPDFForm` メソッドを呼び出して次の値を渡します。

   * ファイル名拡張子を含んだフォームデザイン名を指定する文字列値。
   * フォームに結合するデータを含む `com.adobe.idp.Document` オブジェクト（手順 2 で作成）。
   * 実行時オプションを保存する `PDFFormRenderSpec` オブジェクト。詳細情報については、「[AEM Forms API リフェレンス](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=ja)」を参照してください。
   * `URLSpec` フラグメントに基づいてフォームをレンダリングするために Forms サービスで必要な URI 値を含むオブジェクト。
   * 添付ファイルを保存する `java.util.HashMap` オブジェクト。オプションのパラメーターです。フォームにファイルを添付しない場合は `null` を指定できます。

   `renderPDFForm` メソッドは、クライアントの Web ブラウザーに書き込む必要があるフォームデータストリームを含む `FormsResult` オブジェクトを返します。

1. `FormsResult` オブジェクトの `getOutputContent` メソッドを呼び出して、`com.adobe.idp.Document` オブジェクトを作成します。
1. `getContentType` メソッドを呼び出して、`com.adobe.idp.Document` オブジェクトのコンテンツタイプを取得します。
1. `javax.servlet.http.HttpServletResponse` オブジェクトのコンテンツタイプを設定するには、`setContentType` メソッドを呼び出して、`com.adobe.idp.Document` オブジェクトのコンテンツタイプを渡します。
1. `javax.servlet.http.HttpServletResponse` オブジェクトの `getOutputStream` メソッドを呼び出して、フォームデータストリームをクライアント web ブラウザーに書き込むために使用される `javax.servlet.ServletOutputStream` オブジェクトを作成します。
1. `com.adobe.idp.Document` オブジェクトの `getInputStream` メソッドを呼び出して `java.io.InputStream` オブジェクトを作成します。
1. `InputStream` オブジェクトの `read` メソッドを呼び出して、引数としてバイト配列を渡すことで、バイト配列を作成し、フォームデータストリームを入力します。
1. `javax.servlet.ServletOutputStream` オブジェクトの `write` メソッドを呼び出して、クライアント web ブラウザーにフォームデータストリームを送信します。バイト配列を `write` メソッドに渡します。

次のコード例は、Formsサービスを呼び出し、フラグメントに基づいてフォームをレンダリングする Java サーブレットを表しています。

```java
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-forms-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     *
     * (Because Forms quick starts are implemented as Java servlets, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     */
 import java.io.File;
 import java.io.FileInputStream;
 import java.io.IOException;
 import java.io.PrintWriter;
 
 import javax.servlet.Servlet;
 import javax.servlet.ServletException;
 import javax.servlet.ServletOutputStream;
 import javax.servlet.http.HttpServlet;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import com.adobe.livecycle.formsservice.client.*;
 import java.util.*;
 import java.io.InputStream;
 import java.net.URL;
 
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class RenderFormFragment extends HttpServlet implements Servlet {
 
     public void doGet(HttpServletRequest req, HttpServletResponse resp)
         throws ServletException, IOException {
             doPost(req,resp);
 
     }
     public void doPost(HttpServletRequest req, HttpServletResponse resp)
     throws ServletException, IOException {
 
 
 
         try{
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Get the value of selected radio button
             String radioValue = req.getParameter("radio");
 
             //Create an Document object to store form data
             Document oInputData = null;
 
             //The value of the radio button determines the form data to use
             //which determines which fragments used in the form
             if (radioValue.compareTo("AMERICAN") == 0)            {
                 FileInputStream myData = new FileInputStream("C:\\Adobe\Purchase Order US.xml");
                 oInputData = new Document(myData);
             }
             else if (radioValue.compareTo("CANADIAN") == 0)            {
                 FileInputStream myData = new FileInputStream("C:\\Adobe\Purchase Order Canada.xml");
                 oInputData = new Document(myData);
             }
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a FormsServiceClient object
             FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
             //Set the parameter values for the renderPDFForm method
             String formName = "Applications/FormsApplication/1.0/FormsFolder/Purchase Order Dynamic.xdp";
 
             //Cache the PDF form
             PDFFormRenderSpec pdfFormRenderSpec = new PDFFormRenderSpec();
             pdfFormRenderSpec.setCacheEnabled(new Boolean(true));
 
             //Specify URI values that are required to render a form
             //design based on fragments
             URLSpec uriValues = new URLSpec();
             uriValues.setApplicationWebRoot("https://'[server]:[port]'/RenderFormFragment");
             uriValues.setContentRootURI("repository:///");
             uriValues.setTargetURL("https://'[server]:[port]'/FormsServiceClientApp/HandleData");
 
             //Invoke the renderPDFForm method and write the
             //results to a client web browser
             FormsResult formOut = formsClient.renderPDFForm(
                         formName,               //formQuery
                         oInputData,             //inDataDoc
                         pdfFormRenderSpec,      //PDFFormRenderSpec
                         uriValues,                //urlSpec
                         null                    //attachments
                         );
 
             //Create a Document object that stores form data
             Document myData = formOut.getOutputContent();
 
             //Get the content type of the response and
             //set the HttpServletResponse object’s content type
             String contentType = myData.getContentType();
             resp.setContentType(contentType);
 
             //Create a ServletOutputStream object
             ServletOutputStream oOutput = resp.getOutputStream();
 
             //Create an InputStream object
             InputStream inputStream = myData.getInputStream();
 
             //Write the data stream to the web browser
             byte[] data = new byte[4096];
             int bytesRead = 0;
             while ((bytesRead = inputStream.read(data)) > 0)
             {
                 oOutput.write(data, 0, bytesRead);
             }
 
         }catch (Exception e) {
              System.out.println("The following exception occurred: "+e.getMessage());
       }
     }
 }
```

### Web ページの作成 {#creating-the-web-page}

index.html の Web ページは、Java サーブレットへのエントリポイントを提供し、Forms サービスを呼び出します。この Web ページは、2 つのラジオボタンと 1 つの送信ボタンを含む基本的な HTML フォームです。ラジオボタンの名前は radio です。ユーザーが送信ボタンをクリックすると、フォームデータが `RenderFormFragment` Java サーブレットに投稿されます。

Java サーブレットは、次の Java コードを使用して、HTML ページからポストされるデータをキャプチャします。

```java
             Document oInputData = null;
 
             //Get the value of selected radio button
             String radioValue = req.getParameter("radio");
 
             //The value of the radio button determines the form data to use
             //which determines which fragments used in the form
             if (radioValue.compareTo("AMERICAN") == 0)            {
                 FileInputStream myData = new FileInputStream("C:\\Adobe\Purchase Order US.xml");
                 oInputData = new Document(myData);
             }
             else if (radioValue.compareTo("CANADIAN") == 0)            {
                 FileInputStream myData = new FileInputStream("C:\\Adobe\Purchase Order Canada.xml");
                 oInputData = new Document(myData);
             }
```

次の HTML コードは、開発環境のセットアップ中に作成された index.html ファイルにあります（[Web プロジェクトの作成](/help/forms/developing/rendering-forms.md#creating-a-web-project)を参照）。

```xml
 <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "https://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
 <html xmlns="https://www.w3.org/1999/xhtml">
 <head>
 <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
 <title>Untitled Document</title>
 </head>
 
 <body>
 <form name="myform" action="https://'[server]:[port]'/FragmentsWebApplication/RenderFormFragment" method="post">
      <table>
      <tr>
        <th>Forms Fragment Web Client</th>
      </tr>
      <tr>
        <td>
          <label>
          <input type="radio" name="radio" id="radio_Data" value="CANADIAN" />
          Canadian data<br />
          </label>
          <p>
            <label>
            <input type="radio" name="radio" id="radio_Data" value="AMERICAN" checked/>
            American data</label>
          </p>
        </td>
      </tr>
      <tr>
      <td>
        <label>
          <input type="submit" name="button_Submit" id="button_Submit" value="Submit" />
            </label>
            </td>
         </tr>
        </table>
      </form>
 </body>
 </html>
```

### Web アプリケーションのパッケージ化 {#packaging-the-web-application}

Forms サービスを呼び出す Java サーブレットをデプロイするには、web アプリケーションを WAR ファイルにパッケージ化します。コンポーネントのビジネスロジックが依存する外部 JAR ファイル（adobe-livecycle-client.jar や adobe-forms-client.jar など）も WAR ファイルに含めるようにします。

**Web アプリケーションを WAR ファイルにパッケージ化するには、次の手順に従います。**

1. **プロジェクトエクスプローラ**&#x200B;ウィンドウで、`FragmentsWebApplication` プロジェクトを右クリックして、 **書き出し**／**WAR ファイル**&#x200B;を選択します。
1. 「**Web モジュール**」テキストボックスで、Java プロジェクトの名前として `FragmentsWebApplication` と入力します。
1. **宛先**&#x200B;テキストボックスで、**ファイル名に`FragmentsWebApplication.war`** と入力し、WAR ファイルの場所を指定して「完了」をクリックします。

### J2EE アプリケーションサーバーへの WAR ファイルのデプロイ {#deploying-the-war-file-to-the-j2ee-application-server}

WAR ファイルは、AEM Forms がデプロイされている J2EE アプリケーションサーバーにデプロイできます。WAR ファイルをデプロイした後は、Web ブラウザーを使用して HTML Web ページにアクセスできます。

**J2EE アプリケーションサーバーに WAR ファイルをデプロイするには、次の手順に従います。**

* WAR ファイルをエクスポートパスから `[Forms Install]\Adobe\Adobe Experience Manager Forms\jboss\server\all\deploy` にコピーします。

### Web アプリケーションのテスト {#testing-your-web-application}

Web アプリケーションをデプロイした後、Web ブラウザーを使用してテストできます。AEM Forms をホストしているコンピューターを使用している場合は、次の URL を指定できます。

* http://localhost:8080/FragmentsWebApplication/index.html

   「ラジオ」ボタンを選択し、「送信」ボタンをクリックしてください。フラグメントに基づくフォームが Web ブラウザーに表示されます。問題が発生した場合は、J2EE アプリケーションサーバーのログファイルを参照してください。
