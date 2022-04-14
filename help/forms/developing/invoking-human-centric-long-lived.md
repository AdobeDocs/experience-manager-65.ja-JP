---
title: 人間中心の長期間有効なプロセスの呼び出し
seo-title: Invoking Human-Centric Long-Lived Processes
description: 'Invocation API を使用する Java Webベースのクライアントアプリケーション、Web サービスを使用する ASP.NET アプリケーション、および Remoting を使用する Flex で構築されたクライアントアプリケーションを使用して、Workbench で作成された人間中心の長期プロセスをプログラムで呼び出します。 '
seo-description: Programmatically invoke human-centric long-lived processes created in Workbench using a Java web-based client application that uses the Invocation API, an ASP.NET application that uses web services, and a client application built with Flex that uses Remoting.
uuid: 42269d41-a90f-4ea1-aeb9-d61337bcfa54
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: 18a320b4-dce6-4c50-8864-644b0b2d6644
role: Developer
exl-id: c9ebad8b-b631-492d-99a3-094e892b2ddb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '3699'
ht-degree: 100%

---

# 人間中心の長期間有効なプロセスの呼び出し {#invoking-human-centric-long-lived-processes}

Workbench で作成された人間中心の長期間有効なプロセスを、以下のクライアントアプリケーションを使用して、プログラムで呼び出すことができます。

* 呼び出し API を使用する Java Web ベースのクライアントアプリケーション。 （[Java API を使用した AEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-java.md)(/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-ap)を参照してください。）
* Web サービスを使用する ASP.NET アプリケーションです。 （[Web サービスを使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)を参照してください。）
* Remoting を使用する Flex で構築されたクライアントアプリケーション。 （[AEM forms では非推奨の AEM Forms Remoting を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)。）

呼び出される長期間有効なプロセスの名前は&#x200B;*FirstAppSolution/PreLoanProcess*&#x200B;です。このプロセスは、 [最初の AEM Forms アプリケーションの作成](https://www.adobe.com/go/learn_aemforms_firstapp_ds_63)に規定されたチュートリアルに従って作成できます。

人間中心のプロセスには、Workspace を使用してユーザーが応答できるタスクが含まれます。 例えば、Workbench を使用して、銀行の担当者がローン申し込みを承認または拒否できるプロセスを作成できます。 次の図に、プロセスを示します *FirstAppSolution/PreLoanProcess*。

この *FirstAppSolution/PreLoanProcess* プロセスには、データタイプが XML の、*formData* という名前の入力パラメターを入力できます。 この XML データは、*PreLoanForm.xdp*&#x200B;という名前のフォームデザインとマージされます。. 次の図に、ユーザーに割り当てられた、ローン申し込みを承認または拒否するタスクを表すフォームを示します。 ユーザーは Workspace を使用して、アプリケーションを承認または拒否します。 Workspace ユーザーは、次の図に示す「承認」ボタンをクリックして、ローン申し込みを承認できます。 同様に、ユーザーは「拒否」ボタンをクリックして、ローンの申し込みを拒否できます。

長期間有効なプロセスは非同期で呼び出され、次の要因により、同期で呼び出すことができません。

* プロセスが長い時間を要する。
* プロセスが、複数の組織にまたがっている。
* プロセスを完了するには、他人による入力が必要。例えば、不在の管理者にフォームが送信された場合を考えてみましょう。 この場合、上司が帰社しフォームを入力するまで、プロセスは完了しません。

長期間有効なプロセスが呼び出されると、AEM Forms はレコードの作成の一環として、呼び出し識別子の値を作成します。 このレコードは、長期間有効なプロセスのステータスを追跡し、AEM Forms データベースに保存されます。 呼び出し識別子の値を使用して、長期間有効なプロセスのステータスを追跡できます。さらにはプロセス呼び出し識別子の値を使用して、実行中のプロセスインスタンスの終了など、Process Manager の操作を実行できます。

>[!NOTE]
>
>短時間のみ有効なプロセスが呼び出された場合、AEM Forms は呼び出し識別子の値やレコードを作成しません。

この `FirstAppSolution/PreLoanProcess` プロセスは、XML データで表されたアプリケーションを申請者が送信すると呼び出されます。 入力プロセス変数の名前は`formData`であり、データタイプは XML です。 この説明の目的上、次のXMLデータが`FirstAppSolution/PreLoanProcess`プロセスへの入力として使用されると想定します。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <LoanApp>
 <Name>Sam White</Name>
 <LoanAmount>250000</LoanAmount>
 <PhoneOrEmail>(555)555-5555</PhoneOrEmail>
 <ApprovalStatus>PENDING APPROVAL</ApprovalStatus>
 </LoanApp>
```

プロセスに渡される XML データは、プロセスで使用されるフォーム内のフィールドと一致する必要があります。 そうでなければ、データはフォーム内に表示されません。 `FirstAppSolution/PreLoanProcess`プロセスを呼び出すすべてのアプリケーション は、この XML データソースを渡す必要があります。 *人間中心の長期間有効なプロセスの呼び出し*&#x200B;で作成されたアプリケーションは、ユーザーが Web クライアントに入力した値から、XML データソースを動的に作成します。

クライアントアプリケーションを使用して、*FirstAppSolution/PreLoanProcess*&#x200B;は必要な XML データを処理します。 長期間有効なプロセスは、呼び出し識別子の値を戻り値として返します。 以下の図に、*FirstAppSolution/PreLoanProcess の長期間有効なプロセスを呼び出すクライアントアプリケーションを示します。 クライアントアプリケーションは XML データを送信し、呼び出し識別子の値を表す文字列値を取得します。

**関連トピック**

[人間中心の長期間有効なプロセスを呼び出す Java Web アプリケーションの作成](invoking-human-centric-long-lived.md#creating-a-java-web-application-that-invokes-a-human-centric-long-lived-process)

[人間中心の長期間有効なプロセスを呼び出す ASP.NET Web アプリケーションの作成](invoking-human-centric-long-lived.md#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process)

[人間中心の長期間有効なプロセスを呼び出す、Flex で構築されたクライアントアプリケーションの作成](invoking-human-centric-long-lived.md#creating-a-client-application-built-with-flex-that-invokes-a-human-centric-long-lived-process)

## 人間中心の長期間有効なプロセスを呼び出す Java Web アプリケーションの作成 {#creating-a-java-web-application-that-invokes-a-human-centric-long-lived-process}

Java サーブレットを使用してを`FirstAppSolution/PreLoanProcess`プロセス呼び出す Web ベースのアプリケーションを作成できます 。 Java サーブレットからこのプロセスを呼び出すには、Java サーブレット内で呼び出し API を使用します。 （[Java API を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)を参照してください。）

次の図に、名前、電話（またはメール）および値を投稿する Web ベースのクライアントアプリケーションを示します。 これらの値は、ユーザーが「アプリケーションを送信」ボタンをクリックすると、Java サーブレットに送信されます。

Java サーブレットは、以下のタスクを実行します。

* 「HTML」ページから Java サーブレットに投稿された値を取得します。
* *FirstAppSolution/PreLoanProcess* プロセスに渡す XML データソースを動的に作成します。名前、電話（またはメール）、金額の値は、XML データソースで指定されます。
* AEM Forms Invocation API を使用して *FirstAppSolution/PreLoanProcess* プロセスを呼び出します。
* クライアント web ブラウザーに呼び出し識別子の値を返します。

### 手順の概要 {#summary-of-steps}

`FirstAppSolution/PreLoanProcess` プロセスを呼び出す Java web ベースのアプリケーションを作成するには次の手順を実行します。

1. [Web プロジェクトを作成します](invoking-human-centric-long-lived.md#create-a-web-project)。
1. [サーブレット用の Java アプリケーションロジックの作成します](invoking-human-centric-long-lived.md#create-java-application-logic-for-the-servlet)。
1. [Web アプリケーション用の web ページの作成](invoking-human-centric-long-lived.md#create-the-web-page-for-the-web-application)
1. [Web アプリケーションを WAR ファイルにパッケージ化します](invoking-human-centric-long-lived.md#package-the-web-application-to-a-war-file)。
1. [AEM Forms をホストする J2EE アプリケーションサーバーに WAR ファイルをデプロイします](invoking-human-centric-long-lived.md#deploy-the-war-file-to-the-j2ee-application-server-hosting-aem-forms)。
1. [Web アプリケーションをテストします](invoking-human-centric-long-lived.md#test-your-web-application)。

>[!NOTE]
>
>これらの手順の一部は、AEM Forms がデプロイされている J2EE アプリケーションによって異なります。 例えば、WAR ファイルのデプロイ方法は、使用している J2EE アプリケーションサーバーによって異なります。 AEM Forms が JBoss® にデプロイされていることを前提としています。

### Web プロジェクトを作成 {#create-a-web-project}

Web アプリケーションを作成する最初の手順は、web プロジェクトを作成することです。このドキュメントの基になる Java IDE は Eclipse 3.3 です。Eclipse IDE を使用して、Web プロジェクトを作成し、必要な JAR ファイルをプロジェクトに追加します。*index.html* という名前の HTML ページと Java サーブレットをプロジェクトに追加します。

次のリストでは、web プロジェクトに含める JAR ファイルを指定します。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* J2EE.jar

これらの JAR ファイルの場所については、[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。

>[!NOTE]
>
>J2EE.jar ファイルは、Java サーブレットで使用されるデータタイプを定義します。この JAR ファイルは、AEM Forms がデプロイされている J2EE アプリケーションサーバーから取得できます。

**Web プロジェクトの作成**

1. Eclipse を起動し、**ファイル**／**新規プロジェクト**&#x200B;をクリックします。
1. **新規プロジェクト**&#x200B;ダイアログボックスで、**Web**／**ダイナミック Web プロジェクト**&#x200B;を選択します。
1. プロジェクト名として `InvokePreLoanProcess` と入力し、「**終了**」をクリックします。

**必要な JAR ファイルをプロジェクトに追加する**

1. プロジェクトエクスプローラーウィンドウで、`InvokePreLoanProcess` プロジェクトを右クリックして&#x200B;**プロパティ**&#x200B;を選択します。
1. 「**Java ビルドパス**」をクリックしてから「**ライブラリ**」タブをクリックします。
1. 「**外部 JAR を追加**」ボタンをクリックし、含める JAR ファイルを参照します。

**プロジェクトに Java サーブレットを追加**

1. プロジェクトエクスプローラーウィンドウで、`InvokePreLoanProcess` プロジェクトを右クリックして、**新規**／**その他**&#x200B;を選択します。
1. **Web** フォルダーを展開し、「**Servlet**」を選択してから「**次へ**」をクリックします。
1. サーブレットを作成ダイアログボックスで、サーブレット名として `SubmitXML` と入力してから「**終了**」をクリックします。

**プロジェクトに HTML ページを追加する**

1. プロジェクトエクスプローラーウィンドウで、`InvokePreLoanProcess` プロジェクトを右クリックして、**新規**／**その他**&#x200B;を選択します。
1. **Web** フォルダーを展開し 、「**HTML**」を選択してから「**次へ**」をクリックします。
1. 新規 HTML ダイアログボックスで、ファイル名として `index.html` と入力してから「**終了**」をクリックします。

>[!NOTE]
>
>SubmitXML Java サーブレットを呼び出す HTML コンテンツの作成について詳しくは、[Web アプリケーション用の Web ページの作成](invoking-human-centric-long-lived.md#create-the-web-page-for-the-web-application)を参照してください。

### サーブレット用の Java アプリケーションロジックの作成 {#create-java-application-logic-for-the-servlet}

Java サーブレット内から `FirstAppSolution/PreLoanProcess` プロセスを呼び出す Java アプリケーションロジックを作成します。次のコードは、 `SubmitXML` Java Servlet の構文を示しています。

```java
     public class SubmitXML extends HttpServlet implements Servlet {
         public void doGet(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {
         doPost(req,resp);
 
         }
         public void doPost(HttpServletRequest req, HttpServletResponse resp
         throws ServletException, IOException {
             //Add code here to invoke the FirstAppSolution/PreLoanProcess process
             }
```

通常、クライアントコードは Java サーブレットの `doGet` または `doPost` メソッドには配置しません。より優れたプログラミング方法は、このコードを別のクラスに配置することです。次に、`doPost` メソッド（または `doGet` メソッド）内からクラスをインスタンス化し、適切なメソッドを呼び出します。ただし、コードを簡潔にするために、コード例は最小限に抑えられ、`doPost` メソッドに配置されています。

Invocation API を使用して `FirstAppSolution/PreLoanProcess` プロセスを呼び出すには、次のタスクを実行します。

1. adobe-livecycle-client.jar などのクライアント JAR ファイルを Java プロジェクトのクラスパスに含めます。これらのファイルの場所については、[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。
1. HTML ページから送信された名前、電話、金額の値を取得します。これらの値を使用して、`FirstAppSolution/PreLoanProcess` プロセスに送信される XML データソースを動的に作成します。`org.w3c.dom` クラスを使用して XML データソースを作成できます（このアプリケーションロジックを次のコード例に示します）。
1. 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。（[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照。）
1. コンストラクターを使用して `ServiceClientFactory` オブジェクトを渡すことによって、`ServiceClient` オブジェクトを作成します。`ServiceClient` オブジェクトを使用すると、サービス操作を呼び出すことができます。呼び出し要求の検索、ディスパッチ、ルーティングなどのタスクを処理します。
1. コンストラクターを使用して `java.util.HashMap` オブジェクトを作成します。
1. 各入力パラメーターに対して `java.util.HashMap` オブジェクトの `put` メソッドを呼び出して、長期間有効なプロセスに渡します。プロセスの入力パラメーターの名前を必ず指定してください。`FirstAppSolution/PreLoanProcess` プロセスにはタイプ `XML`（`formData` という名前）の 1 つの入力パラメーターが必要なため、`put` メソッドを呼び出す必要があるのは 1 回だけです。

   ```java
    //Get the XML to pass to the FirstAppSolution/PreLoanProcess process
    org.w3c.dom.Document inXML = GetDataSource(name,phone,amount);
    
    //Create a Map object to store the parameter value
    Map params = new HashMap();
    params.put("formData", inXML);
   ```

1. `ServiceClientFactory` オブジェクトの `createInvocationRequest` メソッドを呼び出し、次の値を渡すことによって `InvocationRequest` オブジェクトを作成します。

   * 呼び出す長期間有効なプロセスの名前を指定する文字列値。`FirstAppSolution/PreLoanProcess` プロセスを呼び出すには、`FirstAppSolution/PreLoanProcess` を指定します。
   * プロセス操作名を表す文字列値。長期間有効なプロセス操作の名前は `invoke` です。
   * サービス操作に必要なパラメーター値を含む `java.util.HashMap` オブジェクト。
   * `false` を指定するブール値が同期リクエストを作成します（この値は、長時間有効なプロセスを呼び出すために適用されます）。

   >[!NOTE]
   >
   >*createInvocationRequest メソッドの 4 番目のパラメーターとして値 true を渡すことによって、短期間有効なプロセスを呼び出すことができます。値 true を渡すと、同期リクエストが作成されます。*

1. `ServiceClient` オブジェクトの `invoke` メソッドを呼び出し、`InvocationRequest` オブジェクトを渡すことによって、呼び出しリクエストを AEM Forms に送信します。`invoke` メソッドは、`InvocationReponse` オブジェクトを返します。
1. 長期間有効なプロセスは、呼び出し識別情報を表す文字列値を返します。`InvocationReponse` オブジェクトの `getInvocationId` メソッドを呼び出して、この値を取得します。

   ```java
    //Send the invocation request to the long-lived process and
    //get back an invocation response object
    InvocationResponse lcResponse = myServiceClient.invoke(lcRequest);
    String invocationId = lcResponse.getInvocationId();
   ```

1. 呼び出し ID 値をクライアント web ブラウザーに書き込みます。`java.io.PrintWriter` インスタンスを使用して、この値をクライアント web ブラウザーに書き込みます。

### クイックスタート：Invocation API を使用した長時間有効なプロセスの呼び出し {#quick-start-invoking-a-long-lived-process-using-the-invocation-api}

次の Java コード例は、`FirstAppSolution/PreLoanProcess` プロセスを呼び出す Java サーブレットを表しています。

```java
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-livecycle-client.jar
     * 2. adobe-usermanager-client.jar
     *
     * (Because this  quick start is implemented as a Java servlet, it is
     * not necessary to include J2EE specific JAR files - the Java project
     * that contains this quick start is exported as a WAR file which
     * is deployed to the J2EE application server)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * For complete details about the location of these JAR files,
     * see "Including AEM Forms library files" in Programming with AEM forms
     * */
 import java.io.ByteArrayOutputStream;
 import java.io.File;
 import java.io.IOException;
 import java.io.PrintWriter;
 
 import javax.servlet.ServletException;
 import javax.servlet.http.HttpServletRequest;
 import javax.servlet.http.HttpServletResponse;
 import java.util.*;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import javax.xml.parsers.DocumentBuilder;
 import javax.xml.parsers.DocumentBuilderFactory;
 import javax.xml.transform.Transformer;
 import javax.xml.transform.TransformerFactory;
 import javax.xml.transform.dom.DOMSource;
 import javax.xml.transform.stream.StreamResult;
 
 import com.adobe.idp.dsc.InvocationRequest;
 import com.adobe.idp.dsc.InvocationResponse;
 import com.adobe.idp.dsc.clientsdk.ServiceClient;
 import org.w3c.dom.Element;
 
     public class SubmitXML extends javax.servlet.http.HttpServlet implements javax.servlet.Servlet {
       static final long serialVersionUID = 1L;
 
        public SubmitXML() {
         super();
     }
 
 
     protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
         // TODO Auto-generated method stub
         doPost(request,response);
     }
 
     protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
 
         try{
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_EJB_ENDPOINT, "jnp://localhost:1099");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_EJB_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a ServiceClient object
             ServiceClient myServiceClient = myFactory.getServiceClient();
 
             //Get the values that are passed from the Loan HTML page
             String name = (String)request.getParameter("name");
             String phone = (String)request.getParameter("phone");
             String amount = (String)request.getParameter("amount");
 
             //Create XML to pass to the FirstAppSolution/PreLoanProcess process
             org.w3c.dom.Document inXML = GetDataSource(name,phone,amount);
 
             //Create a Map object to store the XML input parameter value
             Map params = new HashMap();
             params.put("formData", inXML);
 
             //Create an InvocationRequest object
             InvocationRequest lcRequest =  myFactory.createInvocationRequest(
                 "FirstAppSolution/PreLoanProcess", //Specify the long-lived process name
                     "invoke",           //Specify the operation name
                     params,               //Specify input values
                     false);               //Create an asynchronous request
 
             //Send the invocation request to the long-lived process and
             //get back an invocation response object
             InvocationResponse lcResponse = myServiceClient.invoke(lcRequest);
             String invocationId = lcResponse.getInvocationId();
 
             //Create a PrintWriter instance
             PrintWriter pp = response.getWriter();
 
             //Write the invocation identifier value back to the client web browser
             pp.println("The job status identifier value is: " +invocationId);
 
         }catch (Exception e) {
              System.out.println("The following exception occurred: "+e.getMessage());
       }
     }
 
 
      //Create XML data to pass to the long-lived process
      private static org.w3c.dom.Document GetDataSource(String name, String phone, String amount)
      {
             org.w3c.dom.Document document = null;
 
             try
             {
                 //Create DocumentBuilderFactory and DocumentBuilder objects
                 DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
                 DocumentBuilder builder = factory.newDocumentBuilder();
 
                 //Create a new Document object
                 document = builder.newDocument();
 
                 //Create MortgageApp - the root element in the XML
                 Element root = (Element)document.createElement("LoanApp");
                 document.appendChild(root);
 
                 //Create an XML element for Name
                 Element nameElement = (Element)document.createElement("Name");
                 nameElement.appendChild(document.createTextNode(name));
                 root.appendChild(nameElement);
 
                 //Create an XML element for Phone
                 Element phoneElement = (Element)document.createElement("PhoneOrEmail");
                 phoneElement.appendChild(document.createTextNode(phone));
                 root.appendChild(phoneElement);
 
                 //Create an XML element for amount
                 Element loanElement = (Element)document.createElement("LoanAmount");
                 loanElement.appendChild(document.createTextNode(amount));
                 root.appendChild(loanElement);
 
                 //Create an XML element for ApprovalStatus
                 Element approveElement = (Element)document.createElement("ApprovalStatus");
                 approveElement.appendChild(document.createTextNode("PENDING APPROVAL"));
                 root.appendChild(approveElement);
 
               }
          catch (Exception e) {
                   System.out.println("The following exception occurred: "+e.getMessage());
                }
         return document;
          }
         }
```

### Web アプリケーション用の web ページの作成 {#create-the-web-page-for-the-web-application}

*index.html* web ページは、`FirstAppSolution/PreLoanProcess` プロセスを呼び出す Java サーブレットへのエントリポイントを提供します。この web ページは、HTML フォームと送信ボタンを含む基本的な HTML フォームです。ユーザーが送信ボタンをクリックすると、フォームデータが `SubmitXML` Java サーブレットにポストされます。

Java サーブレットは、次の Java コードを使用して、HTML ページからポストされるデータをキャプチャします。

```java
 //Get the values that are passed from the Loan HTML page
 String name = request.getParameter("name");
 String phone = request.getParameter("phone");
 String amount = request.getParameter("amount");
```

次の HTML コードは、開発環境のセットアップ中に作成された index.html ファイルを表しています。（[Web プロジェクトの作成](invoking-human-centric-long-lived.md#create-a-web-project)を参照してください）。

```xml
 <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "https://www.w3.org/TR/html4/loose.dtd">
 <html>
 <head>
 <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
 <title>Insert title here</title>
 </head>
 <body>
 <table>
     <TBODY>
         <TR>
             <td><img src="financeCorpLogo.jpg" width="172" height="62"></TD>
             <td><FONT size="+2"><strong>Java Loan Application Page</strong></FONT></TD>
             <td> </TD>
             <td> </TD>
         </TR>
 
     </TBODY>
 </TABLE>
     <FORM action="https://hiro-xp:8080/PreLoanProcess/SubmitXML" method="post">
        <table>
          <TBODY>
                <TR>
                      <td><LABEL for="name">Name: </LABEL></TD>
                  <td><INPUT type="text" name="name"></TD>
                  <td><input type="submit" value="Submit Application"></TD>
                  </TR>
            <TR>
                  <td> <LABEL for="phone">Phone/Email: </LABEL></TD>
              <td><INPUT type="text" name="phone"></TD>
                  <td></TD>
              </TR>
 
            <TR>
                  <td><LABEL for="amount">Amount: </LABEL></TD>
              <td><INPUT type="text" name="amount"></TD>
                 <td></TD>
             </TR>
          </TBODY>
 </TABLE>
       </FORM>
 </body>
 </html>
```

### Web アプリケーションを WAR ファイルにパッケージ化する {#package-the-web-application-to-a-war-file}

`FirstAppSolution/PreLoanProcess` プロセスを呼び出す Java サーブレットをデプロイするには、web アプリケーションを WAR ファイルにパッケージ化します。コンポーネントのビジネスロジックが依存する外部 JAR ファイル（ adobe-livecycle-client.jar や adobe-usermanager-client.jar など）も WAR ファイルに含めるようにします。

次のイラストは、WAR ファイルにパッケージ化された Eclipse プロジェクトのコンテンツを示しています。

>[!NOTE]
>
>前のイラストでは、JPG ファイルは任意の JPG 画像ファイルに置き換えることができます。

**Web アプリケーションを WAR ファイルにパッケージ化するには：**

1. **プロジェクトエクスプローラ**&#x200B;ウィンドウで、`InvokePreLoanProcess` プロジェクトを右クリックして、**エクスポート**／**WAR ファイル**&#x200B;を選択します。
1. **Web モジュール**&#x200B;テキストボックスで、Java プロジェクトの名前として `InvokePreLoanProcess` と入力します。
1. **宛先**&#x200B;テキストボックスで、**ファイル名として`PreLoanProcess.war`** と入力し、WAR ファイルの場所を指定してから「終了」をクリックします。

### AEM Forms をホストする J2EE アプリケーションサーバーに WAR ファイルをデプロイする {#deploy-the-war-file-to-the-j2ee-application-server-hosting-aem-forms}

WAR ファイルを、AEM Forms がデプロイされている J2EE アプリケーションサーバーにデプロイします。WAR ファイルを J2EE アプリケーションサーバーにデプロイするには、WAR ファイルをエクスポートパスから `[AEM Forms Install]\Adobe\Adobe Experience Manager Forms\jboss\server\lc_turnkey\deploy` にコピーします。

>[!NOTE]
>
>AEM Forms が JBoss にデプロイされていない場合は、AEM Forms をホストする J2EE アプリケーションサーバーに準拠して WAR ファイルをデプロイする必要があります。

### Web アプリケーションのテスト {#test-your-web-application}

Web アプリケーションをデプロイした後、Web ブラウザーを使用してテストできます。 AEM Forms をホストしているコンピューターを使用している場合は、次の URL を指定できます。

* http://localhost:8080/PreLoanProcess/index.html

   HTML フォームフィールドに値を入力し、「アプリケーションの送信」ボタンをクリックします。 問題が発生した場合は、J2EE アプリケーションサーバーのログファイルを参照してください。

>[!NOTE]
>
>Java アプリケーションがプロセスを呼び出したことを確認するには、Workspace を起動し、ローンを受け入れます。

## 人間中心の長期間有効なプロセスを呼び出す ASP.NET Web アプリケーションの作成 {#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process}

`FirstAppSolution/PreLoanProcess` プロセスを呼び出す ASP.NET アプリケーションを作成できます。ASP.NET アプリケーションからこのプロセスを呼び出すには、Web サービスを使用します。 （[Web サービスを使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)を参照してください）。

次のイラストは、エンドユーザーからデータを取得する ASP.NET クライアントアプリケーションを示しています。データは XML データソースに配置され、ユーザーが「アプリケーションを送信」ボタンをクリックした際に `FirstAppSolution/PreLoanProcess` プロセスに送信されます。

プロセスの呼び出し後に、呼び出し識別子の値が表示されることに注意してください。呼び出し識別子の値は、長期間有効なプロセスのステータスを追跡するレコードの一部として作成されます。

ASP.NET アプリケーションは、次のタスクを実行します。

* ユーザーが web ページに入力した値を取得します。
* FirstAppSolution/PreLoanProcess プロセス に渡される XML データソースを動的に作成します。3 つの値は、XML データソースで指定されます。
* Web サービスを使用して、FirstAppSolution/PreLoanProcess プロセスを呼び出します。
* 呼び出し識別子の値と、長時間有効な操作のステータスをクライアント web ブラウザーに返します。

### 手順の概要 {#summary_of_steps-1}

FirstAppSolution/PreLoanProcess プロセスを呼び出す ASP.NET アプリケーションを作成するには、次の手順を実行します。

1. [ASP.NET Web アプリケーションを作成します](invoking-human-centric-long-lived.md#create-an-asp-net-web-application)。
1. [FirstAppSolution/PreLoanProcess を呼び出す ASP ページを作成します](invoking-human-centric-long-lived.md#create-an-asp-page-that-invokes-firstappsolution-preloanprocess)。
1. [ASP.NET アプリケーションを実行します](invoking-human-centric-long-lived.md#run-the-asp-net-application)。

### ASP.NET Web アプリケーションの作成 {#create-an-asp-net-web-application}

Microsoft .NET C# ASP.NET Web アプリケーションを作成します。 次のイラストは、*InvokePreLoanProcess* という名前の ASP.NET プロジェクトのコンテンツを示します。

サービスリファレンスの下に、2 つの項目があることに注意してください。最初の項目の名前は JobManager です。 このリファレンスにより、ASP.NET アプリケーションは Job Manager サービスを呼び出すことができます。このサービスは、長期間有効なプロセスのステータスに関する情報を返します。例えば、プロセスが現在実行中の場合、このサービスは現在実行中のプロセスを示す数値を返します。 2 つ目のリファレンスは、*PreLoanProcess* という名前です。このサービスリファレンスは、FirstAppSolution/PreLoanProcess プロセスへの参照を表します。 サービスリファレンスを作成した後に、AEM Forms サービスに関連付けられているデータタイプを .NET プロジェクト内で使用できます。

**ASP.NET プロジェクトの作成：**

1. Microsoft Visual Studio 2008 を起動します。
1. **ファイル**&#x200B;メニューから、「**新規**」、「**Web サイト**」を選択します。
1. **テンプレート**&#x200B;リストから、「**ASP.NET Web サイト**」を選択します。
1. 「**場所**」ボックスで、プロジェクトの場所を選択します。 *InvokePreLoanProcess* とプロジェクトに名前を付けます。
1. 「**言語**」ボックスで、「ビジュアル C#」を選択します。
1. 「OK」をクリックします。

**サービスリファレンスの追加：**

1. プロジェクトメニューで、「**サービスリファレンスを追加**」を選択します。
1. **アドレス**&#x200B;ダイアログボックスで、Job Manager サービスに対する WSDL を指定します。

   ```java
    https://hiro-xp:8080/soap/services/JobManager?WSDL&lc_version=9.0.1
   ```

1. 「名前空間」フィールドに `JobManager` と入力します。
1. 「**Go**」をクリックし、「**OK**」をクリックします。
1. **プロジェクト**&#x200B;メニューから、「**サービスリファレンスを追加**」を選択します。
1. 「**アドレス**」ダイアログボックスで、FirstAppSolution/PreLoanProcess プロセスの WSDL を指定します。

   ```java
    https://hiro-xp:8080/soap/services/FirstAppSolution/PreLoanProcess?WSDL&lc_version=9.0.1
   ```

1. 「名前空間」フィールドに `PreLoanProcess` と入力します。
1. 「**Go**」をクリックし、「**OK**」をクリックします。

>[!NOTE]
>
>`hiro-xp` をAEM Forms をホストする J2EE アプリケーションサーバーの IP アドレスに置き換えます。`lc_version` オプションで、MTOM などの AEM Forms 機能が使用できます。 `lc_version` オプションを指定しない場合、MTOM を使用して AEM Forms を呼び出すことはできません。（[MTOM を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)を参照してください）。

### FirstAppSolution/PreLoanProcess を呼び出す ASP ページを作成する {#create-an-asp-page-that-invokes-firstappsolution-preloanprocess}

ASP.NET プロジェクト内に、ローン申請者に HTML ページを表示する web フォーム（ASPX ファイル）を追加します。Web フォームは、`System.Web.UI.Page` から派生したクラスに基づいています。`FirstAppSolution/PreLoanProcess` を呼び出す C# アプリケーションロジックは `Button1_Click` メソッドにあります（このボタンは、「アプリケーションの送信」ボタンを表します）。

次のイラストは、ASP.NET アプリケーションを示しています

次のテーブルは、この ASP.NET アプリケーションの一部であるコントロールの一覧です。

<table>
 <thead>
  <tr>
   <th><p>コントロール名</p></th>
   <th><p>説明</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>TextBoxName</p></td>
   <td><p>顧客の姓と名を指定します。 </p></td>
  </tr>
  <tr>
   <td><p>TextBoxPhone</p></td>
   <td><p>顧客の電話またはメールアドレスを指定します。 </p></td>
  </tr>
  <tr>
   <td><p>TextBoxAmount</p></td>
   <td><p>ローン金額を指定します。</p></td>
  </tr>
  <tr>
   <td><p>Button1</p></td>
   <td><p>「アプリケーションの送信」ボタンを表します。</p></td>
  </tr>
  <tr>
   <td><p>LabelJobID</p></td>
   <td><p>呼び出し識別子の値を指定するラベルコントロール。</p></td>
  </tr>
  <tr>
   <td><p>LabelStatus</p></td>
   <td><p>ジョブステータスの値を指定するラベルコントロール。この値は、Job Manager サービスを呼び出すことで取得されます。 </p></td>
  </tr>
 </tbody>
</table>

ASP.NET アプリケーションの一部であるアプリケーションロジックは、XML データソースを動的に作成し、`FirstAppSolution/PreLoanProcess` プロセスに渡します。申請者が HTML ページに入力した値は、XML データソース内で指定する必要があります。これらのデータ値は、フォームが Workspace で表示される際に、フォームに結合されます。`System.Xml` 名前空間にあるクラスは、XML データソースの作成に使用されます。

ASP.NET アプリケーションから XML データを必要とするプロセスを呼び出す場合、XML データタイプを使用できます。つまり、`System.Xml.XmlDocument` インスタンスをプロセスに渡すことはできません。プロセスに渡すこの XML インスタンスの完全修飾名は `InvokePreLoanProcess.PreLoanProcess.XML` です。 `System.Xml.XmlDocument` インスタンスを `InvokePreLoanProcess.PreLoanProcess.XML` に変換します。このタスクは、次のコードを使用して実行できます。

```java
 //Create the XML to pass to the FirstAppSolution/PreLoanProcess process
 XmlDocument myXML = CreateXML(userName, phone, amount);
 
 //Convert the XML to a InvokePreLoanProcess.PreLoanProcess.XML instance
 StringWriter sw = new StringWriter();
 XmlTextWriter xw = new XmlTextWriter(sw);
 myXML.WriteTo(xw);
 
 InvokePreLoanProcess.PreLoanProcess.XML inXML = new XML();
 inXML.document = sw.ToString();
```

`FirstAppSolution/PreLoanProcess` プロセスを呼び出す ASP ページを作成するには、`Button1_Click` メソッドで次のタスクを実行します。

1. デフォルトのコンストラクターを使用し `FirstAppSolution_PreLoanProcessClient` オブジェクトを作成します。
1. `System.ServiceModel.EndpointAddress` コンストラクターを使用し `FirstAppSolution_PreLoanProcessClient.Endpoint.Address` オブジェクトを作成します。WSDL を指定する文字列値を AEM Forms サービスとエンコーディングタイプに渡します。

   ```java
    https://hiro-xp:8080/soap/services/FirstAppSolution/PreLoanProcess?blob=mtom
   ```

   `lc_version` 属性を使用する必要はありません。この属性は、サービス参照を作成する際に使用されます。ただし、`?blob=mtom` を指定する必要があります。

   >[!NOTE]
   >
   >`hiro-xp`* を AEM Forms をホストしている J2EE アプリケーションサーバーの IP アドレスに置き換えます。*

1. `FirstAppSolution_PreLoanProcessClient.Endpoint.Binding` データメンバーの値を取得して、`System.ServiceModel.BasicHttpBinding` オブジェクトを作成します。戻り値を `BasicHttpBinding` にキャストします。
1. `System.ServiceModel.BasicHttpBinding` オブジェクトの `MessageEncoding` データメンバーを `WSMessageEncoding.Mtom` に設定します。この値により、MTOM が確実に使用されます。
1. 次のタスクを実行して、HTTP 基本認証を有効にします。

   * AEM Forms ユーザー名をデータメンバー `FirstAppSolution_PreLoanProcessClient.ClientCredentials.UserName.UserName` に割り当てます。
   * 対応するパスワード値をデータメンバー `FirstAppSolution_PreLoanProcessClient.ClientCredentials.UserName.Password` に割り当てます。
   * 定数値 `HttpClientCredentialType.Basic` をデータメンバー `BasicHttpBindingSecurity.Transport.ClientCredentialType` に割り当てます。
   * 定数値 `BasicHttpSecurityMode.TransportCredentialOnly` をデータメンバー `BasicHttpBindingSecurity.Security.Mode` に割り当てます。

   次のコードの例に、これらのタスクを示します。

   ```as3
    //Enable BASIC HTTP authentication
    BasicHttpBinding b = (BasicHttpBinding)mortgageClient.Endpoint.Binding;
    b.MessageEncoding = WSMessageEncoding.Mtom;
    mortgageClient.ClientCredentials.UserName.UserName = "administrator";
    mortgageClient.ClientCredentials.UserName.Password = "password";
    b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
    b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
    b.MaxReceivedMessageSize = 2000000;
    b.MaxBufferSize = 2000000;
    b.ReaderQuotas.MaxArrayLength = 2000000;
   ```

1. ユーザーが web ページに入力した名前、電話、金額の値を取得します。これらの値を使用して、`FirstAppSolution/PreLoanProcess` プロセスに送信される XML データソースを動的に作成します。プロセスに渡す XML データソースを表す `System.Xml.XmlDocument` を作成します（次のコード例に、このアプリケーションロジックを示します）。
1. `System.Xml.XmlDocument` インスタンスを `InvokePreLoanProcess.PreLoanProcess.XML` に変換します（次のコード例に、このアプリケーションロジックを示します）。
1. `FirstAppSolution_PreLoanProcessClient` オブジェクトの `invoke_Async` メソッドを呼び出して、`FirstAppSolution/PreLoanProcess` プロセスを呼び出します。このメソッドは、長期間有効なプロセスの呼び出し識別子の値を表す文字列値を返します。
1. コンストラクターを使用して `JobManagerClient` を作成します。（Job Manager サービスへのサービス参照が設定されていることを確認してください）。
1. 手順 1 ～ 5 を繰り返します。手順 2 で URL `https://hiro-xp:8080/soap/services/JobManager?blob=mtom` を指定します。
1. コンストラクターを使用して `JobId` オブジェクトを作成します。
1. `JobId` オブジェクトの `id` データメンバーに `FirstAppSolution_PreLoanProcessClient` オブジェクトの `invoke_Async` メソッドの戻り値を設定します。
1. `value` true を `JobId` オブジェクトの `persistent` データメンバーに割り当てます。
1. `JobManagerService` オブジェクトの `getStatus` メソッドを呼び出し、`JobId` オブジェクトを渡すことにより、`JobStatus` オブジェクトを作成します。
1. `JobStatus` オブジェクトの `statusCode` データメンバーの値を取得して、ステータス値を取得します。
1. 呼び出し識別情報の値を `LabelJobID.Text` フィールドに割り当てます。
1. ステータス値を `LabelStatus.Text` フィールドに割り当てます。

### クイックスタート：Web サービス API を使用した長期間有効なプロセスの呼び出し {#quick-start-invoking-a-long-lived-process-using-the-web-service-api}

次の C# コードの例では `FirstAppSolution/PreLoanProcess` プロセスを呼び出します。

```csharp
 ???/**
     * Ensure that you create a .NET project that uses
     * MS Visual Studio 2008 and version 3.5 of the .NET
     * framework. This is required to invoke a
     * AEM Forms service using MTOM.
 
 
 using System;
 using System.Collections;
 using System.Configuration;
 using System.Data;
 using System.Linq;
 using System.Web;
 using System.ServiceModel;
 using System.Web.Security;
 using System.Web.UI;
 using System.Web.UI.HtmlControls;
 using System.Web.UI.WebControls;
 using System.Web.UI.WebControls.WebParts;
 using System.Xml.Linq;
 using System.Xml;
 using System.IO;
 
 //A reference to FirstAppSolution/PreLoanProcess
 using InvokePreLoanProcess.PreLoanProcess;
 
 //A reference to JobManager service
 using InvokePreLoanProcess.JobManager;
 
 
 namespace InvokePreLoanProcess
 {
        public partial class _Default : System.Web.UI.Page
        {
            //This method is called when the Submit Application button is
            //Clicked
            protected void Button1_Click(object sender, EventArgs e)
            {
                //Create a FirstAppSolution_PreLoanProcessClient object
                FirstAppSolution_PreLoanProcessClient mortgageClient = new FirstAppSolution_PreLoanProcessClient();
                mortgageClient.Endpoint.Address = new System.ServiceModel.EndpointAddress("https://hiro-xp:8080/soap/services/FirstAppSolution/PreLoanProcess?blob=mtom");
 
                //Enable BASIC HTTP authentication
                BasicHttpBinding b = (BasicHttpBinding)mortgageClient.Endpoint.Binding;
                b.MessageEncoding = WSMessageEncoding.Mtom;
                mortgageClient.ClientCredentials.UserName.UserName = "administrator";
                mortgageClient.ClientCredentials.UserName.Password = "password";
                b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
                b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
                b.MaxReceivedMessageSize = 2000000;
                b.MaxBufferSize = 2000000;
                b.ReaderQuotas.MaxArrayLength = 2000000;
 
                //Retrieve values that user entered into the web page
                String userName = TextBoxName.Text;
                String phone = TextBoxPhone.Text;
                String amount = TextBoxAmount.Text;
 
                //Create the XML to pass to the FirstAppSolution/PreLoanProcess process
                XmlDocument myXML = CreateXML(userName, phone, amount);
 
                StringWriter sw = new StringWriter();
                XmlTextWriter xw = new XmlTextWriter(sw);
                myXML.WriteTo(xw);
 
                InvokePreLoanProcess.PreLoanProcess.XML inXML = new XML();
                inXML.document = sw.ToString();
 
                //INvoke the FirstAppSolution/PreLoanProcess process
                String invocationID =  mortgageClient.invoke_Async(inXML);
 
                //Create a JobManagerClient object to obtain the status of the long-lived operation
                JobManagerClient jobManager = new JobManagerClient();
                jobManager.Endpoint.Address = new System.ServiceModel.EndpointAddress("https://hiro-xp:8080/soap/services/JobManager?blob=mtom");
 
                //Enable BASIC HTTP authentication
                BasicHttpBinding b1 = (BasicHttpBinding)jobManager.Endpoint.Binding;
                b1.MessageEncoding = WSMessageEncoding.Mtom;
                jobManager.ClientCredentials.UserName.UserName = "administrator";
                jobManager.ClientCredentials.UserName.Password = "password";
                b1.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
                b1.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
                b1.MaxReceivedMessageSize = 2000000;
                b1.MaxBufferSize = 2000000;
                b1.ReaderQuotas.MaxArrayLength = 2000000;
 
 
                //Create a JobID object that represents the status of the
                //long-lived operation
                JobId jobId = new JobId();
                jobId.id = invocationID;
                jobId.persistent = true;
                JobStatus jobStatus = jobManager.getStatus(jobId);
                System.Int16 val2 = jobStatus.statusCode;
                LabelJobID.Text = "The job status identifier value is " + invocationID;
                LabelStatus.Text = "The status of the long-lived operation is " + getJobDescription(val2);
 
            }
 
            private static XmlDocument CreateXML(String name, String phone, String amount)
            {
                //This method dynamically creates a DDX document
                //to pass to the FirstAppSolution/PreLoanProcess process
                XmlDocument xmlDoc = new XmlDocument();
 
                //Create the root element and append it to the XML DOM
                System.Xml.XmlElement root = xmlDoc.CreateElement("LoanApp");
                xmlDoc.AppendChild(root);
 
                //Create the Name element
                XmlElement nameElement = xmlDoc.CreateElement("Name");
                nameElement.AppendChild(xmlDoc.CreateTextNode(name));
                root.AppendChild(nameElement);
 
                //Create the LoanAmount element
                XmlElement LoanAmount = xmlDoc.CreateElement("LoanAmount");
                LoanAmount.AppendChild(xmlDoc.CreateTextNode(amount));
                root.AppendChild(LoanAmount);
 
                //Create the PhoneOrEmail element
                XmlElement PhoneOrEmail = xmlDoc.CreateElement("PhoneOrEmail");
                PhoneOrEmail.AppendChild(xmlDoc.CreateTextNode(phone));
                root.AppendChild(PhoneOrEmail);
 
                //Create the ApprovalStatus element
                XmlElement ApprovalStatus = xmlDoc.CreateElement("ApprovalStatus");
                ApprovalStatus.AppendChild(xmlDoc.CreateTextNode("PENDING APPROVAL"));
                root.AppendChild(ApprovalStatus);
 
                //Return the XmlElement instance
                return xmlDoc;
            }
 
 
            //Returns the String value of the Job Manager status code
            private String getJobDescription(int val)
            {
                switch(val)
                {
                    case 0:
                        return "JOB_STATUS_UNKNOWN";
 
                    case 1:
                        return "JOB_STATUS_QUEUED";
 
                    case 2:
                        return "JOB_STATUS_RUNNING";
 
                    case 3:
                        return "JOB_STATUS_COMPLETED";
 
                    case 4:
                        return "JOB_STATUS_FAILED";
 
                     case 5:
                        return "JOB_STATUS_COMPLETED";
 
                    case 6:
                        return "JOB_STATUS_SUSPENDED";
 
                    case 7:
                        return "JOB_STATUS_COMPLETE_REQUESTED";
 
                    case 8:
                        return "JOB_STATUS_TERMINATE_REQUESTED";
 
                     case 9:
                        return "JOB_STATUS_SUSPEND_REQUESTED";
 
                       case 10:
                        return "JOB_STATUS_RESUME_REQUESTED";
                }
 
                return "";
            }
       }
 }
 
```

>[!NOTE]
>
>getJobDescription ユーザー定義メソッド内の値は、Job Manager サービスが返す値に対応しています。

### ASP.NET アプリケーションを実行します。 {#run-the-asp-net-application}

ASP.NET アプリケーションをコンパイルしてデプロイした後、web ブラウザーを使用して実行できます。ASP.NET プロジェクトの名前が *InvokePreLoanProcess* である場合、web ブラウザー内で次の URL を指定します。

*http://localhost:1629/InvokePreLoanProcess/*Default.aspx

localhost は ASP.NET プロジェクトをホストする web サーバーの名前で、1629 はポート番号です。ASP.NET アプリケーションをコンパイルしてビルドすると、Microsoft Visual Studio によって自動的にデプロイされます。

>[!NOTE]
>
>ASP.NET アプリケーションがこのプロセスを呼び出したことを確認するには、Workspace を起動し、ローンを受け入れます。

## 人間中心の長期間有効なプロセスを呼び出す、Flexで構築されたクライアントアプリケーションの作成 {#creating-a-client-application-built-with-flex-that-invokes-a-human-centric-long-lived-process}

Flex で構築した *FirstAppSolution/PreLoanProcess* プロセスを呼び出すためのクライアントアプリケーションを作成できます。このアプリケーションは、Remoting を使用して *FirstAppSolution/PreLoanProcess* プロセスを呼び出します。（[ AEM Forms では廃止となった AEM Forms Remoting を使用した AEM Forms の呼び出し](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)を参照。）

次のイラストに、Flex で構築したクライアントアプリケーションでエンドユーザーからデータを収集する様子を示します。データは XML データソースに配置され、プロセスに送信されます。

プロセスの呼び出し後に、呼び出し識別子の値が表示されることに注意してください。呼び出し識別子の値は、長期間有効なプロセスのステータスを追跡するレコードの一部として作成されます。

Flex で構築されたクライアントアプリケーションは、次のタスクを実行します。

* ユーザーが web ページに入力した値を取得します。
* *FirstAppSolution/PreLoanProcess* プロセスに渡される XML データソースを動的に作成します。3 つの値は、XML データソースで指定されます。
* Remoting を使用して *FirstAppSolution/PreLoanProcess* プロセスをを呼び出します。
* 長期間有効なプロセスの呼び出し識別子の値を返します。

### 手順の概要 {#summary_of_steps-2}

FirstAppSolution/PreLoanProcess プロセスを呼び出すことができる Flex で構築されたクライアントアプリケーションを作成するには、次の手順を実行します。

1. 新しい Flex プロジェクトを開始します。
1. プロジェクトのクラスパスに adobe-remoting-provider.swc ファイルを含めます。 （[AEM Forms Flex ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)を参照。）
1. ActionScript または MXML 経由で`mx:RemoteObject`インスタンスを作成します。（[mx:RemoteObject インスタンスの作成](/help/forms/developing/invoking-aem-forms-using-remoting.md)を参照。）
1. AEM Forms と通信するための `ChannelSet` インスタンスを設定し、それを `mx:RemoteObject` インスタンスに関連付けます。（[AEM Forms へのチャンネルの作成](/help/forms/developing/invoking-aem-forms-using-remoting.md)を参照。）
1. ChannelSet の`login`メソッドまたはサービスの`setCredentials`メソッドを使用して、ユーザー識別情報の値とパスワードを指定します。 （ [シングルサインオンの使用](/help/forms/developing/invoking-aem-forms-using-remoting.md#using-single-sign-on)を参照。）
1. XML インスタンスを作成して、`FirstAppSolution/PreLoanProcess` プロセスに渡す XML データソースを作成します。（このアプリケーションロジックを次のコード例に示します）。
1. コンストラクターを使用して、Object タイプのオブジェクトを作成します。 次のコードに示すように、プロセスの入力パラメーターの名前を指定して、XML をオブジェクトに割り当てます。

   ```csharp
    //Get the XML data to pass to the AEM Forms process
    var xml:XML = createXML();
    var params:Object = new Object();
    params["formData"]=xml;
   ```

1. `mx:RemoteObject`インスタンスの`invoke_Async`メソッドを呼び出すことによって、`FirstAppSolution/PreLoanProcess`プロセスを呼び出します。入力パラメーターを含む`Object`を渡します。（[入力値を渡す](/help/forms/developing/invoking-aem-forms-using-remoting.md)を参照してください）。
1. 次のコードに示すように、長期間有効なプロセスから返される呼び出し識別値を取得します。

   ```csharp
    // Handles async call that invokes the long-lived process
    private function resultHandler(event:ResultEvent):void
    {
    ji = event.result as JobId;
    jobStatusDisplay.text = "Job Status ID: " + ji.jobId as String;
    }
   ```

### Remoting を使用した長期間有効なプロセスの呼び出し {#invoking-a-long-lived-process-using-remoting}

次の Flex コードの例では、`FirstAppSolution/PreLoanProcess`プロセスを呼び出します。

```java
 <?xml version="1.0" encoding="utf-8"?>
 
 <mx:Application  xmlns="*" backgroundColor="#FFFFFF"
      creationComplete="initializeChannelSet();">
 
 <mx:Script>
          <![CDATA[
 
             import mx.controls.Alert;
             import mx.rpc.events.FaultEvent;
             import mx.rpc.events.ResultEvent;
             import flash.net.navigateToURL;
             import mx.messaging.ChannelSet;
             import mx.messaging.channels.AMFChannel;
             import mx.collections.ArrayCollection;
             import mx.rpc.livecycle.JobId;
             import mx.rpc.livecycle.JobStatus;
             import mx.rpc.livecycle.DocumentReference;
             import mx.formatters.NumberFormatter;
 
             // Holds the job ID returned by LC.JobManager
             private var ji:JobId;
 
             private function initializeChannelSet():void
              {
              var cs:ChannelSet= new ChannelSet();
         cs.addChannel(new AMFChannel("remoting-amf", "https://hiro-xp:8080/remoting/messagebroker/amf"));
         LC_MortgageApp.setCredentials("tblue", "password");
         LC_MortgageApp.channelSet = cs;
              }
 
            private function submitApplication():void
             {
             //Get the XML data to pass to the AEM Forms process
             var xml:XML = createXML();
             var params:Object = new Object();
             params["formData"]=xml;
             LC_MortgageApp.invoke_Async(params);
             }
 
             // Handles async call that invokes the long-lived process
             private function resultHandler(event:ResultEvent):void
             {
                ji = event.result as JobId;
                jobStatusDisplay.text = "Job Status ID: " + ji.jobId as String;
             }
 
             private function createXML():XML
             {
                //Calculate the Mortgage value to place in the XML data
                var propertyPrice:String = txtAmount.text ;
                var name:String = txtName.text ;
                var phone:String = txtPhone.text ;;
 
                var model:XML =
 
                  <LoanApp>
                           <Name>{name}</Name>
                           <LoanAmount>{propertyPrice}</LoanAmount>
                           <PhoneOrEmail>{phone}</PhoneOrEmail>
                           <ApprovalStatus>PENDING APPROVAL</ApprovalStatus>
                  </LoanApp>
 
              return model;
             }
 
 
          ]]>
       </mx:Script>
 
       <!-- Declare the RemoteObject and set its destination to the mortgage-app remoting endpoint defined in AEM Forms. -->
       <mx:RemoteObject id="LC_MortgageApp" destination="FirstAppSolution/PreLoanProcess" result="resultHandler(event);">
          <mx:method name="invoke_Async" result="resultHandler(event)"/>
      </mx:RemoteObject>
 
 
     <mx:Grid x="229" y="186">
         <mx:GridRow width="100%" height="100%">
             <mx:GridItem width="100%" height="100%">
                 <mx:Image>
                     <mx:source>file:///D|/LiveCycle_9/FirstApp/financeCorpLogo.jpg</mx:source>
                 </mx:Image>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
                 <mx:Label text="Flex Loan Application Page" fontSize="20"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
             </mx:GridItem>
         </mx:GridRow>
         <mx:GridRow width="100%" height="100%">
             <mx:GridItem width="100%" height="100%">
                 <mx:Label text="Name:" fontSize="12" fontWeight="bold"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
                 <mx:TextInput id="txtName"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
                 <mx:Button label="Submit Application" click="submitApplication()"/>
             </mx:GridItem>
         </mx:GridRow>
         <mx:GridRow width="100%" height="100%">
             <mx:GridItem width="100%" height="100%">
                 <mx:Label text="Phone/Email:" fontSize="12" fontWeight="bold"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
                 <mx:TextInput id="txtPhone"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
             </mx:GridItem>
         </mx:GridRow>
         <mx:GridRow width="100%" height="100%">
             <mx:GridItem width="100%" height="100%">
                 <mx:Label text="Amount:" fontSize="12" fontWeight="bold"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
                 <mx:TextInput id="txtAmount"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
             </mx:GridItem>
         </mx:GridRow>
         <mx:GridRow width="100%" height="100%">
             <mx:GridItem width="100%" height="100%">
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
                 <mx:Label text="Label" id="jobStatusDisplay" enabled="true" fontSize="12" fontWeight="bold"/>
             </mx:GridItem>
             <mx:GridItem width="100%" height="100%">
             </mx:GridItem>
         </mx:GridRow>
     </mx:Grid>
 
 </mx:Application>
 
```
