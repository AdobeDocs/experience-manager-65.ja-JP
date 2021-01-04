---
title: FormsをレンダリングするWeb アプリケーションの作成
seo-title: FormsをレンダリングするWeb アプリケーションの作成
description: Javaサーブレットを使用してFormsサービスを呼び出し、フォームをレンダリングするWebベースのアプリケーションを作成します。 Javaサーブレットは、フォームを返すFormsサービスとクライアントWebブラウザーの間のリンクとして機能します。
seo-description: Javaサーブレットを使用してFormsサービスを呼び出し、フォームをレンダリングするWebベースのアプリケーションを作成します。 Javaサーブレットは、フォームを返すFormsサービスとクライアントWebブラウザーの間のリンクとして機能します。
uuid: 00de10c5-79bd-4d8a-ae18-32f1fd2623bf
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: f29b089e-8902-4744-81c5-15ee41ba8069
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '1901'
ht-degree: 1%

---


# FormsをレンダリングするWeb アプリケーションの作成{#creating-web-applications-thatrenders-forms}

## FormsをレンダリングするWeb アプリケーションの作成{#creating-web-applications-that-renders-forms}

Javaサーブレットを使用してFormsサービスを呼び出し、フォームをレンダリングするWebベースのアプリケーションを作成できます。 Java™サーブレットを使用する利点の1つは、プロセスの戻り値をクライアントWebブラウザーに書き込めることです。 つまり、フォームを返すFormsサービスとクライアントWebブラウザーの間のリンクとして、Javaサーブレットを使用できます。

>[!NOTE]
>
>この節では、Formsサービスを呼び出し、フラグメントに基づいてフォームをレンダリングするJavaサーブレットを使用するWebベースのアプリケーションを作成する方法について説明します。 (「[フラグメントに基づくFormsのレンダリング](/help/forms/developing/rendering-forms-based-fragments.md)」を参照)。

Javaサーブレットを使用してフォームをクライアントWebブラウザーに書き込み、顧客が表示してフォームにデータを入力できるようにします。 データをフォームに入力した後、Webユーザーはフォーム上の送信ボタンをクリックして情報をJavaサーブレットに送信し、Javaサーブレットでデータの取得と処理を行うことができます。 例えば、データを別のプロセスに送信できます。

次の図に示すように、米国ベースのフォームデータまたはカナダベースのフォームデータを選択できるWebベースのアプリケーションの作成方法について説明します。

![cw_cw_fragmentwebclient](assets/cw_cw_fragmentwebclient.png)

レンダリングされるフォームは、フラグメントに基づくフォームです。 つまり、ユーザーがアメリカのデータを選択した場合、返されるフォームでは、アメリカのデータに基づくフラグメントが使用されます。 例えば、次の図に示すように、フォームのフッターに米国の住所が含まれています。

![cw_cw_fragmentformfooter](assets/cw_cw_fragementformfooter.png)

同様に、ユーザーがカナダのデータを選択した場合、次の図に示すように、返されたフォームにはカナダの住所が含まれます。

![cw_cw_fragmentformfootercnd](assets/cw_cw_fragementformfootercnd.png)

>[!NOTE]
>
>フラグメントを基にしたフォームデザインの作成について詳しくは、[Formsデザイナー](https://www.adobe.com/go/learn_aemforms_designer_63)を参照してください。

**サンプルファイル**

この節では、次の場所にあるサンプルファイルを使用します。

&lt;>Formsデザイナーのインストールディレクトリ&#x200B;*>/Samples/Forms/発注書/フォームフラグメント*

ここで、&lt;*install directory*>はインストールパスです。 クライアントアプリケーションの場合、Purchase Order Dynamic.xdpファイルはこのインストール場所からコピーされ、*Applications/FormsApplication*&#x200B;という名前のFormsアプリケーションにデプロイされます。 Purchase Order Dynamic.xdpファイルは、FormsFolderという名前のフォルダーに配置されます。 同様に、次の図に示すように、フラグメントはFragmentsという名前のフォルダーに配置されます。

![cw_cw_fragmentsrepository](assets/cw_cw_fragmentsrepository.png)

Purchase Order Dynamic.xdpのフォームデザインにアクセスするには、フォーム名（`renderPDFForm`メソッドに渡される最初のパラメーター）として`Applications/FormsApplication/1.0/FormsFolder/Purchase Order Dynamic.xdp`を指定し、コンテンツルートURI値として`repository:///`を指定します。

Webアプリケーションが使用するXMLデータファイルが、Dataフォルダーから`C:\Adobe`(AEM FormsをホストするJ2EEアプリケーションサーバーに属するファイルシステム)に移動されました。 ファイル名はPurchase Order *Canada.xml*&#x200B;およびPurchase Order *US.xml*&#x200B;です。

>[!NOTE]
>
>Workbenchを使用したFormsアプリケーションの作成について詳しくは、[workbenchヘルプ](https://www.adobe.com/go/learn_aemforms_workbench_63)を参照してください。

### 手順{#summary-of-steps}の概要

フラグメントに基づいてフォームをレンダリングするWebベースのアプリケーションを作成するには、次の手順を実行します。

1. 新しいWebプロジェクトを作成します。
1. Javaサーブレットを表すJavaアプリケーションロジックを作成します。
1. Webアプリケーション用のWebページを作成します。
1. WebアプリケーションをWARファイルにパッケージ化します。
1. WARファイルをJ2EEアプリケーションサーバーにデプロイします。
1. Webアプリケーションをテストします。

>[!NOTE]
>
>これらの手順の一部は、AEM FormsがデプロイされているJ2EEアプリケーションに依存しています。 例えば、WARファイルのデプロイに使用する方法は、使用しているJ2EEアプリケーションサーバーによって異なります。 この節では、AEM FormsがJBoss®にデプロイされていることを前提としています。

### Webプロジェクトの作成{#creating-a-web-project}

Formsサービスを呼び出すことのできるJavaサーブレットを含むWebアプリケーションを作成する最初の手順は、新しいWebプロジェクトを作成することです。 このドキュメントが基盤とするJava IDEはEclipse 3.3です。Eclipse IDEを使用してWebプロジェクトを作成し、必要なJARファイルをプロジェクトに追加します。 最後に、*index.html*&#x200B;という名前のHTMLページとJavaサーブレットをプロジェクトに追加します。

次のリストは、Webプロジェクトに追加する必要があるJARファイルを指定します。

* adobe-forms-client.jar
* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar

これらのJARファイルの場所については、[「AEM FormsJavaライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)」を参照してください。

**Webプロジェクトを作成するには：**

1. 開始Eclipseを開き、**ファイル**/**新しいプロジェクト**&#x200B;をクリックします。
1. **新しいプロジェクト**&#x200B;ダイアログボックスで、**Web**/**ダイナミックWebプロジェクト**&#x200B;を選択します。
1. プロジェクト名に「`FragmentsWebApplication`」と入力し、「**完了**」をクリックします。

**必要なJARファイルをプロジェクトに追加するには：**

1. 「プロジェクトエクスプローラ」ウィンドウで`FragmentsWebApplication`プロジェクトを右クリックし、「**プロパティ**」を選択します。
1. 「**Javaビルドパス**」をクリックし、「**ライブラリ**」タブをクリックします。
1. 「**追加 External JARs**」ボタンをクリックし、含めるJARファイルを参照します。

**プロジェクトにJavaサーブレットを追加するには：**

1. 「プロジェクトエクスプローラ」ウィンドウで、`FragmentsWebApplication`プロジェクトを右クリックし、**新規**/**その他**&#x200B;を選択します。
1. **Web**&#x200B;フォルダーを展開し、「**サーブレット**」を選択して、「**次へ**」をクリックします。
1. [サーブレットを作成]ダイアログボックスで、サーブレットの名前に「`RenderFormFragment`」と入力し、「**完了**」をクリックします。

**プロジェクトにHTMLページを追加するには：**

1. 「プロジェクトエクスプローラ」ウィンドウで、`FragmentsWebApplication`プロジェクトを右クリックし、**新規**/**その他**&#x200B;を選択します。
1. **Web**&#x200B;フォルダーを展開し、「**HTML**」を選択して、「**次へ**」をクリックします。
1. 新規HTMLダイアログボックスで、ファイル名に「`index.html`」と入力し、「**完了**」をクリックします。

>[!NOTE]
>
>`RenderFormFragment` Javaサーブレットを呼び出すHTMLページの作成について詳しくは、[Webページの作成](/help/forms/developing/rendering-forms.md#creating-the-web-page)を参照してください。

### サーブレット{#creating-java-application-logic-for-the-servlet}用のJavaアプリケーションロジックの作成

Javaサーブレット内からFormsサービスを呼び出すJavaアプリケーションロジックを作成します。 次のコードは、`RenderFormFragment` Javaサーブレットの構文を示しています。

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

通常、クライアントコードはJavaサーブレットの`doGet`メソッドまたは`doPost`メソッド内に配置しません。 このコードを別のクラスに配置し、`doPost`メソッド（または`doGet`メソッド）内からクラスをインスタンス化して、適切なメソッドを呼び出す方が、より良いプログラミング方法です。 ただし、コードを簡潔にするために、この節のコード例は最小限に抑え、コード例は`doPost`メソッドに配置します。

FormsサービスAPIを使用してフラグメントに基づいてフォームをレンダリングするには、次のタスクを実行します。

1. Javaプロジェクトのクラスパスに、adobe-forms-client.jarなどのクライアントJARファイルを含めます。 これらのファイルの場所については、[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。
1. HTMLフォームから送信されたラジオボタンの値を取得し、米国のデータを使用するか、カナダのデータを使用するかを指定します。 米国製が送信された場合は、*発注書US.xml*&#x200B;にあるデータを保存する`com.adobe.idp.Document`を作成します。 同様に、カナダの場合は、*Purchase Order Canada.xml*&#x200B;ファイルにデータを格納する`com.adobe.idp.Document`を作成します。
1. 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。（[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照。）
1. コンストラクターを使用し、`FormsServiceClient`オブジェクトを渡して、`ServiceClientFactory`オブジェクトを作成します。
1. コンストラクターを使用して、URI値を格納する`URLSpec`オブジェクトを作成します。
1. `URLSpec`オブジェクトの`setApplicationWebRoot`メソッドを呼び出し、アプリケーションのWebルートを表す文字列値を渡します。
1. `URLSpec`オブジェクトの`setContentRootURI`メソッドを呼び出し、コンテンツルートURI値を指定する文字列値を渡します。 フォームデザインとフラグメントがコンテンツルートURI内にあることを確認します。 そうでない場合、Formsサービスは例外をスローします。 AEM Formsリポジトリを参照するには、`repository://`を指定します。
1. `URLSpec`オブジェクトの`setTargetURL`メソッドを呼び出し、フォームデータのポスト先のターゲットURL値を指定する文字列値を渡します。 フォームデザインでターゲットURLを定義する場合は、空の文字列を渡すことができます。 演算を実行するために、フォームの送信先URLを指定することもできます。
1. `FormsServiceClient`オブジェクトの`renderPDFForm`メソッドを呼び出し、次の値を渡します。

   * ファイル名拡張子を含むフォームデザイン名を指定するstring値。
   * フォームとマージするデータを含む`com.adobe.idp.Document`オブジェクト（手順2で作成）。
   * 実行時オプションを格納する`PDFFormRenderSpec`オブジェクト。 詳しくは、[AEM FormsAPIリファレンス](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)を参照してください。
   * フラグメントに基づいてフォームをレンダリングするためにFormsサービスで必要なURI値を含む`URLSpec`オブジェクトです。
   * 添付ファイルを格納する`java.util.HashMap`オブジェクト。 これはオプションのパラメーターです。フォームにファイルを添付しない場合は、`null`を指定できます。

   `renderPDFForm`メソッドは、クライアントのWebブラウザーに書き込む必要があるフォームデータストリームを含む`FormsResult`オブジェクトを返します。

1. `FormsResult`オブジェクト&#39;s `getOutputContent`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトを作成します。
1. `getContentType`メソッドを呼び出して、`com.adobe.idp.Document`オブジェクトのコンテンツタイプを取得します。
1. `javax.servlet.http.HttpServletResponse`オブジェクトのコンテンツタイプを設定するには、`setContentType`メソッドを呼び出し、`com.adobe.idp.Document`オブジェクトのコンテンツタイプを渡します。
1. `javax.servlet.http.HttpServletResponse`オブジェクトの`getOutputStream`メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに書き込むために使用する`javax.servlet.ServletOutputStream`オブジェクトを作成します。
1. `com.adobe.idp.Document`オブジェクトの`getInputStream`メソッドを呼び出して、`java.io.InputStream`オブジェクトを作成します。
1. `InputStream`オブジェクトの`read`メソッドを呼び出し、バイト配列を引数として渡すことで、バイト配列を作成し、フォームデータストリームを入力します。
1. `javax.servlet.ServletOutputStream`オブジェクトの`write`メソッドを呼び出して、フォームデータストリームをクライアントのWebブラウザーに送信します。 バイト配列を`write`メソッドに渡します。

次のコード例は、Formsサービスを呼び出し、フラグメントに基づいてフォームをレンダリングするJavaサーブレットを表しています。

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

### Webページの作成{#creating-the-web-page}

index.html Webページは、Javaサーブレットへのエントリポイントを提供し、Formsサービスを呼び出します。 このWebページは、2つのラジオボタンと1つの送信ボタンを含む基本的なHTMLフォームです。 ラジオボタンの名前はradioです。 ユーザーが送信ボタンをクリックすると、フォームデータが`RenderFormFragment` Javaサーブレットにポストされます。

Javaサーブレットは、次のJavaコードを使用して、HTMLページから投稿されたデータを取得します。

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

次のHTMLコードは、開発環境のセットアップ時に作成されたindex.htmlファイルにあります。 （「[Webプロジェクトの作成](/help/forms/developing/rendering-forms.md#creating-a-web-project)」を参照）。

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

### Webアプリケーションのパッケージ化{#packaging-the-web-application}

Formsサービスを呼び出すJavaサーブレットをデプロイするには、WebアプリケーションをWARファイルにパッケージ化します。 コンポーネントのビジネスロジックが依存する外部JARファイル（adobe-livecycle-client.jarやadobe-forms-client.jarなど）もWARファイルに含めてください。

**WebアプリケーションをWARファイルにパッケージ化するには：**

1. **プロジェクトエクスプローラー**&#x200B;ウィンドウで`FragmentsWebApplication`プロジェクトを右クリックし、**エクスポート**/**WARファイル**&#x200B;を選択します。
1. 「**Web module**」テキストボックスに、Javaプロジェクトの名前として「`FragmentsWebApplication`」と入力します。
1. 「**宛先**」テキストボックスに、**ファイル名に`FragmentsWebApplication.war`**&#x200B;と入力し、WARファイルの場所を指定して、「完了」をクリックします。

### J2EEアプリケーションサーバーへのWARファイルのデプロイ{#deploying-the-war-file-to-the-j2ee-application-server}

WARファイルは、AEM FormsがデプロイされているJ2EEアプリケーションサーバーにデプロイできます。 WARファイルをデプロイすると、Webブラウザーを使用してHTML Webページにアクセスできます。

**WARファイルをJ2EEアプリケーションサーバーにデプロイするには：**

* エクスポートパスから`[Forms Install]\Adobe\Adobe Experience Manager Forms\jboss\server\all\deploy`にWARファイルをコピーします。

### Webアプリケーションのテスト{#testing-your-web-application}

Webアプリケーションをデプロイした後、Webブラウザーを使用してテストできます。 AEM Formsをホストしているコンピューターと同じコンピューターを使用している場合は、次のURLを指定できます。

* http://localhost:8080/FragmentsWebApplication/index.html

   ラジオボタンを選択し、「送信」ボタンをクリックします。 フラグメントに基づくフォームはWebブラウザーに表示されます。 問題が発生した場合は、J2EEアプリケーションサーバーのログファイルを参照してください。

