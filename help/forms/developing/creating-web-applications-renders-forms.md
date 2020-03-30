---
title: フォームをレンダリングするWeb アプリケーションの作成
seo-title: フォームをレンダリングするWeb アプリケーションの作成
description: 'null'
seo-description: 'null'
uuid: 00de10c5-79bd-4d8a-ae18-32f1fd2623bf
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: f29b089e-8902-4744-81c5-15ee41ba8069
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# フォームをレンダリングするWeb アプリケーションの作成 {#creating-web-applications-thatrenders-forms}

## フォームをレンダリングするWeb アプリケーションの作成 {#creating-web-applications-that-renders-forms}

Javaサーブレットを使用してFormsサービスを呼び出し、フォームをレンダリングするWebベースのアプリケーションを作成できます。 Java™サーブレットを使用する利点の1つは、プロセスの戻り値をクライアントWebブラウザに書き込めることです。 つまり、Javaサーブレットは、フォームを返すFormsサービスとクライアントWebブラウザーの間のリンクとして使用できます。

>[!NOTE]
>
>この節では、Formsサービスを呼び出し、フラグメントに基づいてフォームをレンダリングするJavaサーブレットを使用するWebベースのアプリケーションを作成する方法について説明します。 (See [Rendering Forms Based on Fragments](/help/forms/developing/rendering-forms-based-fragments.md).)

Javaサーブレットを使用して、顧客がフォームに表示してデータを入力できるように、フォームをクライアントWebブラウザーに書き込むことができます。 フォームにデータを入力した後、Webユーザーはフォーム上の送信ボタンをクリックして情報をJavaサーブレットに送り返し、データの取得と処理を行います。 例えば、データを別のプロセスに送信できます。

ここでは、次の図に示すように、米国ベースのフォームデータまたはカナダベースのフォームデータをユーザーが選択できるWebベースのアプリケーションの作成方法を説明します。

![cw_cw_fragmentwebclient](assets/cw_cw_fragmentwebclient.png)

レンダリングされるフォームは、フラグメントに基づくフォームです。 つまり、ユーザーが米国のデータを選択した場合、返されるフォームでは、米国のデータに基づくフラグメントが使用されます。 例えば、次の図に示すように、フォームのフッターに米国の住所が含まれています。

![cw_cw_fragmentformfooter](assets/cw_cw_fragementformfooter.png)

同様に、ユーザーがカナダのデータを選択した場合、返されるフォームには、次の図に示すように、カナダの住所が含まれます。

![cw_cw_fragmentformfootercnd](assets/cw_cw_fragementformfootercnd.png)

>[!NOTE]
>
>フラグメントに基づくフォームデザインの作成について詳しくは、「 [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63)」を参照してください。

**サンプルファイル**

この節では、次の場所にあるサンプルファイルを使用します。

&lt;*Forms Designer install directory*>/Samples/Forms/Purchase Order/Form Fragments

&lt;*install directory*>は、インストールパスです。 クライアントアプリケーションの目的で、Purchase Order Dynamic.xdpファイルがこのインストール場所からコピーされ、 *Applications/FormsApplicationという名前のFormsアプリケーションにデプロイされました*。 Purchase Order Dynamic.xdpファイルは、FormsFolderという名前のフォルダーに配置されます。 同様に、次の図に示すように、フラグメントはFragmentsという名前のフォルダーに配置されます。

![cw_cw_fragmentsrepository](assets/cw_cw_fragmentsrepository.png)

Purchase Order Dynamic.xdpフォームデザインにアクセスするには、フォーム名(メソッドに渡される最初のパラメ `Applications/FormsApplication/1.0/FormsFolder/Purchase Order Dynamic.xdp` ーター)として `renderPDFForm` 、コンテンツル `repository:///` ートURI値として指定します。

Webアプリケーションで使用されるXMLデータファイルが、Dataフォルダーから `C:\Adobe`（AEM FormsをホストするJ2EEアプリケーションサーバーに属するファイルシステム）に移動されました。 ファイル名はPurchase Order *Canada.xml* 、Purchase Order *US.xmlです*。

>[!NOTE]
>
>Workbenchを使用したFormsアプリケーションの作成について詳しくは、Workbenchヘルプを参 [照してくださ](https://www.adobe.com/go/learn_aemforms_workbench_63)い。

### 手順の概要 {#summary-of-steps}

フラグメントに基づいてフォームをレンダリングするWebベースのアプリケーションを作成するには、次の手順を実行します。

1. 新しいWebプロジェクトを作成します。
1. Javaサーブレットを表すJavaアプリケーションロジックを作成します。
1. WebアプリケーションのWebページを作成します。
1. WebアプリケーションをWARファイルにパッケージ化します。
1. WARファイルをJ2EEアプリケーションサーバーにデプロイします。
1. Webアプリケーションをテストします。

>[!NOTE]
>
>これらの手順の一部は、AEM Formsのデプロイ先のJ2EEアプリケーションに依存します。 例えば、WARファイルのデプロイ方法は、使用しているJ2EEアプリケーションサーバーによって異なります。 この節では、AEM FormsがJBoss®にデプロイされていることを前提としています。

### Creating a web project {#creating-a-web-project}

Formsサービスを呼び出すJavaサーブレットを含むWebアプリケーションを作成する最初の手順は、新しいWebプロジェクトを作成することです。 このドキュメントの基盤となるJava IDEはEclipse 3.3です。Eclipse IDEを使用して、Webプロジェクトを作成し、必要なJARファイルをプロジェクトに追加します。 最後に、 *index.htmlというHTMLページと* 、Javaサーブレットをプロジェクトに追加します。

次のリストでは、Webプロジェクトに追加する必要のあるJARファイルを指定します。

* adobe-forms-client.jar
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar

For the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Webプロジェクトを作成するには：**

1. 開始Eclipseで、 **File** / **New Projectをクリックします**。
1. 新規プロジェ **クトダイアログ** ボックスで、 **Web** /ダイナミッ **クWebプロジェクトを選択します**。
1. プロジェクト `FragmentsWebApplication` の名前を入力し、「完了」をクリック **します**。

**必要なJARファイルをプロジェクトに追加するには：**

1. 「プロジェクト・エクスプローラ」ウィンドウで、プロジェクトを右クリッ `FragmentsWebApplication` クし、「プロパティ」を **選択しま**&#x200B;す。
1. 「 **Javaビルドパス」をクリックし** 、「ライブラリ」タブをク **リックします** 。
1. 「 **追加External JARs** 」ボタンをクリックし、含めるJARファイルを参照します。

**プロジェクトにJavaサーブレットを追加するには：**

1. 「プロジェクトエクスプローラ」ウィンドウで、プロジェクトを右クリ `FragmentsWebApplication` ックし、「新規」>「そ **の他** 」を選 **択します**。
1. 「 **Web** 」フォルダを展開し、「 **Servlet**」を選択して「 **Next」をクリックします**。
1. 「サーブレットを作成」ダイアログで、サ `RenderFormFragment` ーブレットの名前を入力し、「完了」をクリッ **クします**。

**HTMLページをプロジェクトに追加するには：**

1. 「プロジェクトエクスプローラ」ウィンドウで、プロジェクトを右クリ `FragmentsWebApplication` ックし、「新規」>「そ **の他** 」を選 **択します**。
1. 「 **Web** 」フォルダを展開し、「 **HTML**」を選択して「 **Next**」をクリックします。
1. 新規HTMLダイアログボックスで、ファイル名 `index.html` を入力し、「完了」をクリック **します**。

>[!NOTE]
>
>Javaサーブレットを呼び出すHTMLページの作成について詳しくは、 `RenderFormFragment` Webページの作成[を参照してください](/help/forms/developing/rendering-forms.md#creating-the-web-page)。

### サーブレット用のJavaアプリケーションロジックの作成 {#creating-java-application-logic-for-the-servlet}

Formsサービスを呼び出すJavaアプリケーションロジックは、Javaサーブレット内から作成します。 次のコードは、 `RenderFormFragment` Javaサーブレットの構文を示しています。

```as3
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

通常、クライアントコードはJavaサーブレットのメソッドやメソッド内に配置 `doGet` しま `doPost` せん。 より良いプログラミング方法は、このコードを別のクラスに配置し、メソッド（またはメソッド）内からクラスをインスタンス化し、適 `doPost` 切なメソッ `doGet` ドを呼び出すことです。 ただし、コードを簡潔にするため、この節のコード例は最小限に抑えられ、コード例がメソッドに配置され `doPost` ます。

FormsサービスAPIを使用してフラグメントに基づいてフォームをレンダリングするには、次のタスクを実行します。

1. Javaプロジェクトのクラスパスに、adobe-forms-client.jarなどのクライアントJARファイルを含めます。 これらのファイルの場所については、[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。
1. HTMLフォームから送信されたラジオボタンの値を取得し、米国のデータを使用するか、カナダのデータを使用するかを指定します。 米国の場合は、Purchase Order US.xmlに `com.adobe.idp.Document` あるデータを保存する *データを作成します*。 同様に、カナダの場合は、Purchase Order Canada.xml `com.adobe.idp.Document` ファイル内のデータを格納 *するを作成します* 。
1. 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。（[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照。）
1. Create an `FormsServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.
1. コンストラク `URLSpec` ターを使用して、URI値を格納するオブジェクトを作成します。
1. オブジェクト `URLSpec` のメソッ `setApplicationWebRoot` ドを呼び出し、アプリケーションのWebルートを表すstring値を渡します。
1. オブジェクト `URLSpec` のメソッド `setContentRootURI` を呼び出し、コンテンツルートURI値を指定するstring値を渡します。 フォームデザインとフラグメントがコンテンツルートURIに配置されていることを確認します。 そうでない場合、Formsサービスは例外をスローします。 AEM Formsリポジトリを参照するには、を指定しま `repository://`す。
1. オブジェクト `URLSpec` のメソッ `setTargetURL` ドを呼び出し、フォームデータのポスト先のターゲットURL値を指定するstring値を渡します。 フォームデザインでターゲットURLを定義する場合は、空の文字列を渡すことができます。 また、計算を実行するためにフォームの送信先URLを指定することもできます。
1. オブジェクト `FormsServiceClient` のメソッドを `renderPDFForm` 呼び出し、次の値を渡します。

   * ファイル名の拡張子を含む、フォームデザイン名を指定するstring値。
   * フォーム `com.adobe.idp.Document` とマージするデータを含むオブジェクト（手順2で作成）。
   * 実行時 `PDFFormRenderSpec` のオプションを格納するオブジェクト。 For more information, see [AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * フラグ `URLSpec` メントに基づいてフォームをレンダリングするためにFormsサービスで必要なURI値を含むオブジェクトです。
   * 添付ファ `java.util.HashMap` イルを格納するオブジェクト。 これはオプションのパラメーターで、フォームにフ `null` ァイルを添付しないかどうかを指定できます。
   このメソ `renderPDFForm` ッドは、クラ `FormsResult` イアントWebブラウザーに書き込む必要があるフォームデータストリームを含むオブジェクトを返します。

1. オブジェクトの `com.adobe.idp.Document` メソッドを呼び出して、オ `FormsResult` ブジェクトを作成 `getOutputContent` します。
1. メソッドを呼び出して、オブジェ `com.adobe.idp.Document` クトのコンテンツタイプを取 `getContentType` 得します。
1. メソッドを呼 `javax.servlet.http.HttpServletResponse` び出し、オブジェクトのコンテ `setContentType` ンツタイプを渡して、オブジェクトのコンテンツタイプを設定 `com.adobe.idp.Document` します。
1. オブジェクトの `javax.servlet.ServletOutputStream` メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに書き込むために使用す `javax.servlet.http.HttpServletResponse` るオブジェクトを作成 `getOutputStream` します。
1. オブジェクトの `java.io.InputStream` メソッドを呼び出して、オ `com.adobe.idp.Document` ブジェクトを作成 `getInputStream` します。
1. オブジェクトのメソッドを呼び出し、バイト配列を引数として渡すことで、バ `InputStream` イト配列を作成 `read`し、フォームデータストリームを埋め込みます。
1. オブジェクト `javax.servlet.ServletOutputStream` のメソッドを呼 `write` び出して、フォームデータストリームをクライアントWebブラウザーに送信します。 バイト配列をメソッドに渡し `write` ます。

次のコード例は、Formsサービスを呼び出し、フラグメントに基づいてフォームをレンダリングするJavaサーブレットを表しています。

```as3
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

### Webページの作成 {#creating-the-web-page}

index.html Webページは、Javaサーブレットへのエントリポイントを提供し、Formsサービスを呼び出します。 このWebページは、2つのラジオボタンと1つの送信ボタンを含む基本的なHTMLフォームです。 ラジオボタンの名前は「radio」です。 ユーザーが送信ボタンをクリックすると、フォームデータが `RenderFormFragment` Javaサーブレットにポストされます。

Javaサーブレットは、次のJavaコードを使用して、HTMLページから投稿されたデータを取得します。

```as3
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

次のHTMLコードは、開発環境のセットアップ時に作成されたindex.htmlファイル内にあります。 (See [Creating a web project](/help/forms/developing/rendering-forms.md#creating-a-web-project).)

```as3
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

### Webアプリケーションのパッケージ化 {#packaging-the-web-application}

Formsサービスを呼び出すJavaサーブレットをデプロイするには、WebアプリケーションをWARファイルにパッケージ化します。 コンポーネントのビジネスロジックが依存する外部JARファイル（adobe-livecycle-client.jarやadobe-forms-client.jarなど）もWARファイルに含めてください。

**WebアプリケーションをWARファイルにパッケージ化するには：**

1. 「プロジェ **クトエクスプローラ** 」ウィンドウで、プロジェクトを右ク `FragmentsWebApplication` リックし、「エクス **ポート** / **WARファイル」を選択します**。
1. 「 **Web module** 」テキストボッ `FragmentsWebApplication` クスに、Javaプロジェクトの名前を入力します。
1. 「 **Destination** 」テキストボッ `FragmentsWebApplication.war`**クス&#x200B;**に、ファイル名を入力し、WARファイルの場所を指定して、「Finish」をクリックします。

### J2EEアプリケーションサーバーへのWARファイルのデプロイ {#deploying-the-war-file-to-the-j2ee-application-server}

WARファイルは、AEM Formsのデプロイ先のJ2EEアプリケーションサーバーにデプロイできます。 WARファイルをデプロイした後、Webブラウザーを使用してHTML Webページにアクセスできます。

**WARファイルをJ2EEアプリケーションサーバーにデプロイするには：**

* エクスポートパスからにWARファイルをコピーしま `[Forms Install]\Adobe\Adobe Experience Manager Forms\jboss\server\all\deploy`す。

### Webアプリケーションのテスト {#testing-your-web-application}

Webアプリケーションをデプロイした後、Webブラウザーを使用してテストできます。 AEM Formsをホストするコンピューターと同じコンピューターを使用している場合は、次のURLを指定できます。

* http://localhost:8080/FragmentsWebApplication/index.html

   ラジオボタンを選択し、「送信」ボタンをクリックします。 フラグメントに基づくフォームがWebブラウザーに表示されます。 問題が発生した場合は、J2EEアプリケーションサーバーのログファイルを参照してください。

