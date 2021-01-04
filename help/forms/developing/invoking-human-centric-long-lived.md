---
title: 人間中心の長期間有効なプロセスの呼び出し
seo-title: 人間中心の長期間有効なプロセスの呼び出し
description: 呼び出しAPIを使用するJava Webベースのクライアントアプリケーション、Webサービスを使用するASP.NETアプリケーション、およびRemotingを使用して構築されたFlexで作成されたクライアントアプリケーションを使用して、Workbenchで作成された人間中心の長期間有効なプロセスをプログラムから呼び出します。
seo-description: 呼び出しAPIを使用するJava Webベースのクライアントアプリケーション、Webサービスを使用するASP.NETアプリケーション、およびRemotingを使用して構築されたFlexで作成されたクライアントアプリケーションを使用して、Workbenchで作成された人間中心の長期間有効なプロセスをプログラムから呼び出します。
uuid: 42269d41-a90f-4ea1-aeb9-d61337bcfa54
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: 18a320b4-dce6-4c50-8864-644b0b2d6644
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '3739'
ht-degree: 4%

---


# 人間中心の長期間有効なプロセスの呼び出し {#invoking-human-centric-long-lived-processes}

次のクライアントアプリケーションを使用して、Workbenchで作成された人間中心の長期間有効なプロセスをプログラムで呼び出すことができます。

* 呼び出しAPIを使用するJava Webベースのクライアントアプリケーション。 ([Java APIを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-java.md)(/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)を参照)。
* Webサービスを使用するASP.NETアプリケーション。 (「[Webサービスを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)」を参照)。
* Remotingを使用する、Flexで構築されたクライアントアプリケーション。 (「[AEM Formsリモートを使用したAEM Formsの呼び出し(AEM formsでは廃止)](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)」を参照)。

呼び出される長期間有効なプロセスは、*FirstAppSolution/PreLoanProcess*&#x200B;という名前です。 このプロセスは、[最初のAEM Formsアプリケーションの作成](https://www.adobe.com/go/learn_aemforms_firstapp_ds_63)で指定したチュートリアルに従って作成できます。

人間中心のプロセスには、ユーザーがWorkspaceを使用して応答できるタスクが含まれます。 例えば、Workbenchを使用する場合、銀行の管理者がローンの申し込みを承認または拒否できるプロセスを作成できます。 次の図に、プロセス&#x200B;*FirstAppSolution/PreLoanProcess*&#x200B;を示します。

*FirstAppSolution/PreLoanProcess*&#x200B;プロセスは、*formData*&#x200B;という名前の、データタイプがXMLの入力パラメーターを受け取ります。 このXMLデータは、*PreLoanForm.xdp*&#x200B;という名前のフォームデザインとマージされます。 次の図に示すフォームは、ローンの申し込みを承認または拒否するためにユーザーに割り当てられたタスクを表しています。 ユーザーがWorkspaceを使用してアプリケーションを承認または拒否します。 Workspaceユーザーは、次の図に示す「Approve」ボタンをクリックして、ローン要求を承認できます。 同様に、ユーザーは「拒否」ボタンをクリックしてローンの要求を拒否できます。

長期間有効なプロセスは、非同期で呼び出され、次の要因により、同期的に呼び出すことはできません。

* プロセスは、かなりの期間に及ぶことがあります。
* プロセスは、組織の境界をまたぐことができます。
* プロセスを終了するには、外部入力が必要です。 例えば、不在の管理者にフォームが送信される場合を考えてみます。 この場合、マネージャーがフォームを返して入力するまで、プロセスは完了しません。

長期間有効なプロセスが呼び出されると、AEM Formsは、レコードの作成の一環として呼び出し識別子の値を作成します。 このレコードは、長期間有効なプロセスのステータスを追跡し、AEM Formsデータベースに保存されます。 呼び出し識別子の値を使用して、長期間有効なプロセスのステータスを追跡できます。 また、プロセス呼び出し識別子の値を使用して、実行中のプロセスインスタンスの終了など、Process Manager操作を実行できます。

>[!NOTE]
>
>短時間のみ有効なプロセスが呼び出された場合、AEM Formsは呼び出し識別子の値やレコードを作成しません。

`FirstAppSolution/PreLoanProcess`プロセスは、XMLデータで表される申込書を申込者が送信すると呼び出されます。 入力プロセス変数の名前は`formData`で、そのデータ型はXMLです。 この説明の目的で、次のXMLデータが`FirstAppSolution/PreLoanProcess`プロセスへの入力として使用されているとします。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <LoanApp>
 <Name>Sam White</Name>
 <LoanAmount>250000</LoanAmount>
 <PhoneOrEmail>(555)555-5555</PhoneOrEmail>
 <ApprovalStatus>PENDING APPROVAL</ApprovalStatus>
 </LoanApp>
```

プロセスに渡されるXMLデータは、プロセスで使用されるフォーム内のフィールドと一致する必要があります。 それ以外の場合、データはフォーム内に表示されません。 `FirstAppSolution/PreLoanProcess`プロセスを呼び出すすべてのアプリケーションは、このXMLデータソースを渡す必要があります。 *人間中心の長期間有効なプロセスの呼び出し*&#x200B;で作成されたアプリケーションは、ユーザーがWebクライアントに入力した値からXMLデータソースを動的に作成します。

クライアントアプリケーションを使用して、*FirstAppSolution/PreLoanProcess*&#x200B;プロセスに必要なXMLデータを送信できます。 長期間有効なプロセスは、呼び出し識別子の値を戻り値として返します。 次の図に、*FirstAppSolution/PreLoanProcessの長期間有効なプロセスを呼び出すクライアントアプリケーションを示します。 クライアントアプリケーションはXMLデータを送信し、呼び出し識別子の値を表すstring値を返します。

**関連トピック**

[人間中心の長期間有効なプロセスを呼び出す Java Web アプリケーションの作成](invoking-human-centric-long-lived.md#creating-a-java-web-application-that-invokes-a-human-centric-long-lived-process)

[人間中心の長期間有効なプロセスを呼び出すASP.NET Webアプリケーションの作成](invoking-human-centric-long-lived.md#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process)

[人間中心の長期間有効なプロセスを呼び出す、Flexで構築されたクライアントアプリケーションの作成](invoking-human-centric-long-lived.md#creating-a-client-application-built-with-flex-that-invokes-a-human-centric-long-lived-process)

## 人間中心の長期間有効なプロセスを呼び出す Java Web アプリケーションの作成 {#creating-a-java-web-application-that-invokes-a-human-centric-long-lived-process}

Javaサーブレットを使用して`FirstAppSolution/PreLoanProcess`プロセスを呼び出すWebベースのアプリケーションを作成できます。 Javaサーブレットからこのプロセスを呼び出すには、Javaサーブレット内でInvocation APIを使用します。 ([Java APIを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)を参照)。

次の図に、name、phone（またはemail）およびamountの値を投稿するWebベースのクライアントアプリケーションを示します。 これらの値は、ユーザーが「Submit Application」ボタンをクリックするとJavaサーブレットに送信されます。

Javaサーブレットは次のタスクを実行します。

* HTMLページからJavaサーブレットに投稿された値を取得します。
* *FirstAppSolution/PreLoanProcess*&#x200B;プロセスに渡すXMLデータソースを動的に作成します。 名前、電話（または電子メール）、金額の値は、XMLデータソースで指定されます。
* AEM Forms呼び出しAPIを使用して&#x200B;*FirstAppSolution/PreLoanProcess*&#x200B;プロセスを呼び出します。
* 呼び出し識別子の値をクライアントWebブラウザーに返します。

### 手順{#summary-of-steps}の概要

`FirstAppSolution/PreLoanProcess`プロセスを呼び出すJava Webベースのアプリケーションを作成するには、次の手順を実行します。

1. [Webプロジェクトを作成します](invoking-human-centric-long-lived.md#create-a-web-project)。
1. [サーブレット用のJavaアプリケーションロジックを作成します](invoking-human-centric-long-lived.md#create-java-application-logic-for-the-servlet)。
1. [Webアプリケーション用のWebページの作成](invoking-human-centric-long-lived.md#create-the-web-page-for-the-web-application)
1. [WebアプリケーションをWARファイルにパッケージ化します](invoking-human-centric-long-lived.md#package-the-web-application-to-a-war-file)。
1. [WARファイルを、AEM FormsをホストするJ2EEアプリケーションサーバーにデプロイします](invoking-human-centric-long-lived.md#deploy-the-war-file-to-the-j2ee-application-server-hosting-aem-forms)。
1. [Webアプリケーションをテストします](invoking-human-centric-long-lived.md#test-your-web-application)。

>[!NOTE]
>
>これらの手順の一部は、AEM FormsがデプロイされているJ2EEアプリケーションに依存しています。 例えば、WARファイルのデプロイに使用する方法は、使用しているJ2EEアプリケーションサーバーによって異なります。 AEM FormsはJBoss®にデプロイされていることを前提としています。

### Webプロジェクトの作成{#create-a-web-project}

Webアプリケーションを作成する最初の手順は、Webプロジェクトを作成することです。 このドキュメントが基盤とするJava IDEはEclipse 3.3です。Eclipse IDEを使用してWebプロジェクトを作成し、必要なJARファイルをプロジェクトに追加します。 &lt;a0追加/>index.html *という名前のHTMLページと、プロジェクトのJavaサーブレット。*

次のリストは、Webプロジェクトに含めるJARファイルを指定します。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* J2EE.jar

これらのJARファイルの場所については、[「AEM FormsJavaライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)」を参照してください。

>[!NOTE]
>
>J2EE.jarファイルは、Javaサーブレットで使用されるデータ型を定義します。 このJARファイルは、AEM FormsがデプロイされているJ2EEアプリケーションサーバーから取得できます。

**Webプロジェクトの作成**

1. 開始Eclipseを開き、**ファイル**/**新しいプロジェクト**&#x200B;をクリックします。
1. **新しいプロジェクト**&#x200B;ダイアログボックスで、**Web**/**ダイナミックWebプロジェクト**&#x200B;を選択します。
1. プロジェクト名に「`InvokePreLoanProcess`」と入力し、「**完了**」をクリックします。

**プロジェクトに追加必要なJARファイル**

1. 「プロジェクトエクスプローラ」ウィンドウで`InvokePreLoanProcess`プロジェクトを右クリックし、「**プロパティ**」を選択します。
1. 「**Javaビルドパス**」をクリックし、「**ライブラリ**」タブをクリックします。
1. 「**追加 External JARs**」ボタンをクリックし、含めるJARファイルを参照します。

**プロジ追加ェクトへのJavaサーブレット**

1. 「プロジェクトエクスプローラ」ウィンドウで、`InvokePreLoanProcess`プロジェクトを右クリックし、**新規**/**その他**&#x200B;を選択します。
1. **Web**&#x200B;フォルダーを展開し、「**サーブレット**」を選択して、「**次へ**」をクリックします。
1. [サーブレットを作成]ダイアログボックスで、サーブレットの名前に「`SubmitXML`」と入力し、「**完了**」をクリックします。

**プロジ追加ェクトのHTMLページ**

1. 「プロジェクトエクスプローラ」ウィンドウで、`InvokePreLoanProcess`プロジェクトを右クリックし、**新規**/**その他**&#x200B;を選択します。
1. **Web**&#x200B;フォルダーを展開し、「**HTML**」を選択して、「**次へ**」をクリックします。
1. 新規HTMLダイアログボックスで、ファイル名に「`index.html`」と入力し、「**完了**」をクリックします。

>[!NOTE]
>
>SubmitXML Javaサーブレットを呼び出すHTMLコンテンツの作成について詳しくは、[Webアプリケーション用のWebページの作成](invoking-human-centric-long-lived.md#create-the-web-page-for-the-web-application)を参照してください。

### サーブレット{#create-java-application-logic-for-the-servlet}用のJavaアプリケーションロジックの作成

Javaサーブレット内から`FirstAppSolution/PreLoanProcess`プロセスを呼び出すJavaアプリケーションロジックを作成します。 次のコードは、`SubmitXML` Javaサーブレットの構文を示しています。

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

通常、クライアントコードはJavaサーブレットの`doGet`メソッドまたは`doPost`メソッド内に配置しません。 このコードを別のクラスに配置する方が、より良いプログラミング方法です。 次に、`doPost`メソッド（または`doGet`メソッド）内からクラスをインスタンス化し、適切なメソッドを呼び出します。 ただし、コードを簡潔にするため、コード例は最小限に抑えられ、`doPost`メソッドに配置されます。

呼び出しAPIを使用して`FirstAppSolution/PreLoanProcess`プロセスを呼び出すには、次のタスクを実行します。

1. Javaプロジェクトのクラスパスに、adobe-livecycle-client.jarなどのクライアントJARファイルを含めます。 これらのファイルの場所については、[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。
1. HTMLページから送信された名前、電話番号、金額の値を取得します。 これらの値を使用して、`FirstAppSolution/PreLoanProcess`プロセスに送信するXMLデータソースを動的に作成します。 `org.w3c.dom`クラスを使用してXMLデータソースを作成できます（このアプリケーションロジックは次のコード例に示します）。
1. 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。（[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照。）
1. コンストラクタを使用して `ServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。`ServiceClient` オブジェクトを使用すると、サービス操作を呼び出すことができます。呼び出し要求の検索、ディスパッチ、ルーティングなどのタスクを処理します。
1. コンストラクタを使用して `java.util.HashMap` オブジェクトを作成します。
1. 各入力パラメーターに対して `java.util.HashMap` オブジェクトの `put` メソッドを呼び出して、長期間有効なプロセスに渡します。プロセスの入力パラメーターの名前を必ず指定してください。 `FirstAppSolution/PreLoanProcess`プロセスには`XML`型（`formData`という名前）の入力パラメーターが1つ必要なので、`put`メソッドを1回だけ呼び出す必要があります。

   ```java
    //Get the XML to pass to the FirstAppSolution/PreLoanProcess process
    org.w3c.dom.Document inXML = GetDataSource(name,phone,amount);
    
    //Create a Map object to store the parameter value
    Map params = new HashMap();
    params.put("formData", inXML);
   ```

1. `ServiceClientFactory`オブジェクトの`createInvocationRequest`メソッドを呼び出し、次の値を渡して、`InvocationRequest`オブジェクトを作成します。

   * 長期間有効なプロセスを指定する文字列値。`FirstAppSolution/PreLoanProcess`プロセスを呼び出すには、`FirstAppSolution/PreLoanProcess`を指定します。
   * プロセス操作名を表す文字列値。長期間有効なプロセス操作の名前は`invoke`です。
   * サービス操作に必要なパラメーター値を含む `java.util.HashMap` オブジェクト。
   * 非同期リクエストを作成する`false`を指定するBoolean値（この値は長期間有効なプロセスを呼び出す場合に適用されます）。

   >[!NOTE]
   >
   >*短時間のみ有効なプロセスは、createInvocationRequestメソッドの4番目のパラメーターとして値trueを渡すことで呼び出すことができます。値trueを渡すと同期要求が作成されます。*

1. `ServiceClient`オブジェクトの`invoke`メソッドを呼び出し、`InvocationRequest`オブジェクトを渡して、呼び出し要求をAEM Formsに送信します。 `invoke`メソッドは`InvocationReponse`オブジェクトを返します。
1. 長期間有効なプロセスは、呼び出し識別値を表すstring値を返します。 `InvocationReponse`オブジェクトの`getInvocationId`メソッドを呼び出して、この値を取得します。

   ```java
    //Send the invocation request to the long-lived process and
    //get back an invocation response object
    InvocationResponse lcResponse = myServiceClient.invoke(lcRequest);
    String invocationId = lcResponse.getInvocationId();
   ```

1. 呼び出しID値をクライアントWebブラウザーに書き込みます。 `java.io.PrintWriter`インスタンスを使用して、この値をクライアントのWebブラウザーに書き込むことができます。

### クイック開始:呼び出しAPI {#quick-start-invoking-a-long-lived-process-using-the-invocation-api}を使用した長期間有効なプロセスの呼び出し

次のJavaコードの例は、`FirstAppSolution/PreLoanProcess`プロセスを呼び出すJavaサーブレットを表しています。

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

### Webアプリケーション用のWebページの作成{#create-the-web-page-for-the-web-application}

*index.html* Webページは、`FirstAppSolution/PreLoanProcess`プロセスを呼び出すJavaサーブレットへのエントリポイントを提供します。 このWebページは、HTMLフォームと送信ボタンを含む基本的なHTMLフォームです。 ユーザーが送信ボタンをクリックすると、フォームデータが`SubmitXML` Javaサーブレットにポストされます。

Javaサーブレットは、次のJavaコードを使用して、HTMLページから投稿されたデータを取得します。

```java
 //Get the values that are passed from the Loan HTML page
 String name = request.getParameter("name");
 String phone = request.getParameter("phone");
 String amount = request.getParameter("amount");
```

次のHTMLコードは、開発環境のセットアップ中に作成されたindex.htmlファイルを表しています。 （「[Webプロジェクトの作成](invoking-human-centric-long-lived.md#create-a-web-project)」を参照）。

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

### WebアプリケーションをWARファイルにパッケージ化{#package-the-web-application-to-a-war-file}

`FirstAppSolution/PreLoanProcess`プロセスを呼び出すJavaサーブレットをデプロイするには、WebアプリケーションをWARファイルにパッケージ化します。 コンポーネントのビジネスロジックが依存する外部JARファイル（adobe-livecycle-client.jarやadobe-usermanager-client.jarなど）もWARファイルに含めてください。

次の図に、WARファイルにパッケージ化されたEclipseプロジェクトのコンテンツを示します。

>[!NOTE]
>
>上の図では、JPGファイルは任意のJPG画像ファイルに置き換えることができます。

**WebアプリケーションのWARファイルへのパッケージ化：**

1. **プロジェクトエクスプローラー**&#x200B;ウィンドウで`InvokePreLoanProcess`プロジェクトを右クリックし、**エクスポート**/**WARファイル**&#x200B;を選択します。
1. 「**Web module**」テキストボックスに、Javaプロジェクトの名前として「`InvokePreLoanProcess`」と入力します。
1. 「**宛先**」テキストボックスに、**ファイル名に`PreLoanProcess.war`**&#x200B;と入力し、WARファイルの場所を指定して、「完了」をクリックします。

### WARファイルを、AEM FormsをホストするJ2EEアプリケーションサーバーにデプロイします{#deploy-the-war-file-to-the-j2ee-application-server-hosting-aem-forms}

WARファイルを、AEM FormsがデプロイされているJ2EEアプリケーションサーバーにデプロイします。 WARファイルをJ2EEアプリケーションサーバーにデプロイするには、WARファイルをエクスポートパスから`[AEM Forms Install]\Adobe\Adobe Experience Manager Forms\jboss\server\lc_turnkey\deploy`にコピーします。

>[!NOTE]
>
>aem formsがJBossにデプロイされていない場合は、AEM FormsをホストするJ2EEアプリケーションサーバーに準拠してWARファイルをデプロイする必要があります。

### Webアプリケーション{#test-your-web-application}をテストします。

Webアプリケーションをデプロイした後、Webブラウザーを使用してテストできます。 AEM Formsをホストしているコンピューターと同じコンピューターを使用している場合は、次のURLを指定できます。

* http://localhost:8080/PreLoanProcess/index.html

   HTMLフォームのフィールドに値を入力し、「Submit Application」ボタンをクリックします。 問題が発生した場合は、J2EEアプリケーションサーバーのログファイルを参照してください。

>[!NOTE]
>
>Javaアプリケーションがプロセスを呼び出したことを確認するために、開始ワークスペースでローンを受け入れます。

## 人間中心の長期間有効なプロセス{#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process}を呼び出すASP.NET Webアプリケーションの作成

`FirstAppSolution/PreLoanProcess`プロセスを呼び出すASP.NETアプリケーションを作成できます。 ASP.NETアプリケーションからこのプロセスを呼び出すには、Webサービスを使用します。 (「[Webサービスを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)」を参照)。

次の図に、エンドユーザーからデータを取得するASP.NETクライアントアプリケーションを示します。 データはXMLデータソースに配置され、ユーザーが「Submit Application」ボタンをクリックすると`FirstAppSolution/PreLoanProcess`プロセスに送信されます。

プロセスの呼び出し後に、呼び出し識別子の値が表示されます。 呼び出し識別子の値は、長期間有効なプロセスのステータスを追跡するレコードの一部として作成されます。

ASP.NETアプリケーションは、次のタスクを実行します。

* ユーザーがWebページに入力した値を取得します。
* * FirstAppSolution/PreLoanProcess *processに渡されるXMLデータソースを動的に作成します。 3つの値は、XMLデータソースで指定されます。
* Webサービスを使用して、* FirstAppSolution/PreLoanProcess *processを呼び出します。
* 呼び出し識別子の値と、長期間有効な操作のステータスをクライアントWebブラウザーに返します。

### 手順{#summary_of_steps-1}の概要

FirstAppSolution/PreLoanProcessプロセスを呼び出すことのできるASP.NETアプリケーションを作成するには、次の手順を実行します。

1. [ASP.NET Webアプリケーションを作成します](invoking-human-centric-long-lived.md#create-an-asp-net-web-application)。
1. [FirstAppSolution/PreLoanProcessを呼び出すASPページを作成します](invoking-human-centric-long-lived.md#create-an-asp-page-that-invokes-firstappsolution-preloanprocess)。
1. [ASP.NETアプリケーションを実行します](invoking-human-centric-long-lived.md#run-the-asp-net-application)。

### ASP.NET Webアプリケーションの作成{#create-an-asp-net-web-application}

Microsoft .NET C# ASP.NETWeb アプリケーションを作成します。 次の図は、*InvokePreLoanProcess*&#x200B;という名前のASP.NETプロジェクトの内容を示しています。

「Service References」の下に2つの項目があります。 最初のアイテムは* JobManager*という名前です。 この参照は、ASP.NETアプリケーションがJob Managerサービスを呼び出せるようにします。 このサービスは、長期間有効なプロセスのステータスに関する情報を返します。 例えば、プロセスが現在実行中である場合、このサービスは、プロセスが現在実行中であることを示す数値を返します。 2つ目の参照は&#x200B;*PreLoanProcess*&#x200B;という名前です。 このサービスリファレンスは、* FirstAppSolution/PreLoanProcess *processへの参照を表します。 サービス参照を作成すると、AEM Formsサービスに関連付けられたデータ型を.NETプロジェクト内で使用できるようになります。

**ASP.NETプロジェクトを作成する：**

1. 開始Microsoft Visual Studio 2008。
1. **ファイル**&#x200B;メニューから、**新規**、**Webサイト**&#x200B;を選択します。
1. **テンプレート**&#x200B;リストで、**ASP.NET Webサイト**&#x200B;を選択します。
1. 「**場所**」ボックスで、プロジェクトの場所を選択します。 プロジェクトに&#x200B;*InvokePreLoanProcess*&#x200B;という名前を付けます。
1. 「**言語**」ボックスで、「Visual C#」を選択します
1. 「OK」をクリックします。

**追加サービス参照：**

1. プロジェクトメニューで、「**追加サービス参照**」を選択します。
1. 「**アドレス**」ダイアログボックスで、Job ManagerサービスのWSDLを指定します。

   ```java
    https://hiro-xp:8080/soap/services/JobManager?WSDL&lc_version=9.0.1
   ```

1. 名前空間フィールドに`JobManager`と入力します。
1. 「**移動**」をクリックし、「**OK**」をクリックします。
1. **プロジェクト**&#x200B;メニューで、「**追加サービスリファレンス**」を選択します。
1. **アドレス**&#x200B;ダイアログボックスで、FirstAppSolution/PreLoanProcessプロセスのWSDLを指定します。

   ```java
    https://hiro-xp:8080/soap/services/FirstAppSolution/PreLoanProcess?WSDL&lc_version=9.0.1
   ```

1. 名前空間フィールドに`PreLoanProcess`と入力します。
1. 「**移動**」をクリックし、「**OK**」をクリックします。

>[!NOTE]
>
>`hiro-xp`を、AEM FormsをホストするJ2EEアプリケーションサーバーのIPアドレスに置き換えます。 `lc_version`オプションを使用すると、MTOMなどのAEM Forms機能を使用できます。 `lc_version`オプションを指定しないと、MTOMを使用してAEM Formsを呼び出すことはできません。 ([MTOMを使用したAEM Formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)を参照)。

### FirstAppSolution/PreLoanProcess {#create-an-asp-page-that-invokes-firstappsolution-preloanprocess}を呼び出すASPページを作成します

ASP.NETプロジェクト内に、HTMLページをローンの申込者に表示するWebフォーム（ASPXファイル）を追加します。 Webフォームは、`System.Web.UI.Page`から派生したクラスに基づいています。 `FirstAppSolution/PreLoanProcess`を呼び出すC#アプリケーションロジックは、`Button1_Click`メソッドにあります（このボタンは「アプリケーションを送信」ボタンを表します）。

次の図は、ASP.NETアプリケーションを示しています

次の表は、このASP.NETアプリケーションの一部であるコントロールをリストしたものです。

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
   <td><p>顧客の電話または電子メールアドレスを指定します。 </p></td>
  </tr>
  <tr>
   <td><p>TextBoxAmount</p></td>
   <td><p>ローン金額を指定します。</p></td>
  </tr>
  <tr>
   <td><p>Button1</p></td>
   <td><p>「申し込みの送信」ボタンを表します。</p></td>
  </tr>
  <tr>
   <td><p>LabelJobID</p></td>
   <td><p>呼び出し識別子の値を指定するLabelコントロール。</p></td>
  </tr>
  <tr>
   <td><p>LabelStatus</p></td>
   <td><p>ジョブステータスの値を指定するLabelコントロール。 この値は、Job Managerサービスを呼び出して取得されます。 </p></td>
  </tr>
 </tbody>
</table>

ASP.NETアプリケーションの一部であるアプリケーションロジックは、`FirstAppSolution/PreLoanProcess`プロセスに渡すXMLデータソースを動的に作成する必要があります。 申込者がHTMLページに入力した値は、XMLデータソース内で指定する必要があります。 これらのデータ値は、フォームがWorkspaceで表示されるときに、フォームにマージされます。 `System.Xml`名前空間ー内のクラスは、XMLデータソースの作成に使用されます。

ASP.NETアプリケーションからXMLデータを必要とするプロセスを呼び出す場合、XMLデータ型を使用できます。 つまり、`System.Xml.XmlDocument`インスタンスをプロセスに渡すことはできません。 プロセスに渡すこのXMLインスタンスの完全修飾名は`InvokePreLoanProcess.PreLoanProcess.XML`です。 `System.Xml.XmlDocument`インスタンスを`InvokePreLoanProcess.PreLoanProcess.XML`に変換します。 このタスクは、次のコードを使用して実行できます。

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

`FirstAppSolution/PreLoanProcess`プロセスを呼び出すASPページを作成するには、`Button1_Click`メソッドで次のタスクを実行します。

1. `FirstAppSolution_PreLoanProcessClient`オブジェクトを作成するには、そのデフォルトのコンストラクタを使用します。
1. `System.ServiceModel.EndpointAddress`コンストラクターを使用して`FirstAppSolution_PreLoanProcessClient.Endpoint.Address`オブジェクトを作成します。 WSDLをAEM Formsサービスに渡し、エンコードの種類を指定するstring値を渡します。

   ```java
    https://hiro-xp:8080/soap/services/FirstAppSolution/PreLoanProcess?blob=mtom
   ```

   `lc_version`属性を使用する必要はありません。 この属性は、サービス参照を作成する際に使用されます。 ただし、`?blob=mtom`を必ず指定してください。

   >[!NOTE]
   >
   >`hiro-xp`*を、AEM FormsをホストするJ2EEアプリケーションサーバーのIPアドレスに置き換えます。*

1. `FirstAppSolution_PreLoanProcessClient.Endpoint.Binding`データメンバの値を取得して`System.ServiceModel.BasicHttpBinding`オブジェクトを作成します。 戻り値を `BasicHttpBinding` にキャストします。
1. `System.ServiceModel.BasicHttpBinding`オブジェクトの`MessageEncoding`データメンバを`WSMessageEncoding.Mtom`に設定します。 この値により、MTOMが使用されます。
1. 次のタスクを実行して、基本的なHTTP認証を有効にします。

   * AEM formsユーザー名をデータメンバー`FirstAppSolution_PreLoanProcessClient.ClientCredentials.UserName.UserName`に割り当てます。
   * 対応するパスワード値をデータメンバ`FirstAppSolution_PreLoanProcessClient.ClientCredentials.UserName.Password`に割り当てます。
   * 定数値`HttpClientCredentialType.Basic`をデータメンバ`BasicHttpBindingSecurity.Transport.ClientCredentialType`に割り当てます。
   * 定数値`BasicHttpSecurityMode.TransportCredentialOnly`をデータメンバ`BasicHttpBindingSecurity.Security.Mode`に割り当てます。

   次のコードの例は、これらのタスクを示しています。

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

1. ユーザーがWebページに入力した名前、電話番号、金額の値を取得します。 これらの値を使用して、`FirstAppSolution/PreLoanProcess`プロセスに送信するXMLデータソースを動的に作成します。 プロセスに渡すXMLデータソースを表す`System.Xml.XmlDocument`を作成します（次のコード例には、このアプリケーションロジックが示されています）。
1. `System.Xml.XmlDocument`インスタンスを`InvokePreLoanProcess.PreLoanProcess.XML`に変換します（次のコードの例に、このアプリケーションロジックを示します）。
1. `FirstAppSolution_PreLoanProcessClient`オブジェクトの`invoke_Async`メソッドを呼び出して、`FirstAppSolution/PreLoanProcess`プロセスを呼び出します。 このメソッドは、長期間有効なプロセスの呼び出し識別子の値を表すstring値を返します。
1. isコンストラクタを使用して`JobManagerClient`を作成します。 （Job Managerサービスへのサービス参照が設定されていることを確認します）。
1. 手順1 ～ 5を繰り返します。 手順2では、次のURLを指定します。`https://hiro-xp:8080/soap/services/JobManager?blob=mtom`.
1. コンストラクタを使用して `JobId` オブジェクトを作成します。
1. `JobId`オブジェクトの`id`データメンバを、`FirstAppSolution_PreLoanProcessClient`オブジェクトの`invoke_Async`メソッドの戻り値で設定します。
1. `value` trueを`JobId`オブジェクトの`persistent`データメンバに割り当てます。
1. `JobManagerService`オブジェクトの`getStatus`メソッドを呼び出し、`JobId`オブジェクトを渡して、`JobStatus`オブジェクトを作成します。
1. `JobStatus`オブジェクトの`statusCode`データメンバの値を取得して、ステータス値を取得します。
1. 呼び出し識別子の値を`LabelJobID.Text`フィールドに割り当てます。
1. ステータス値を`LabelStatus.Text`フィールドに割り当てます。

### クイック開始:WebサービスAPI {#quick-start-invoking-a-long-lived-process-using-the-web-service-api}を使用して長期間有効なプロセスを呼び出す

以下のC#コードの例は`FirstAppSolution/PreLoanProcess`プロセスを呼び出します。

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
>getJobDescriptionユーザー定義メソッド内の値は、Job Managerサービスが返す値に対応しています。

### ASP.NETアプリケーション{#run-the-asp-net-application}を実行します

ASP.NETアプリケーションをコンパイルして展開した後は、Webブラウザーを使用してASP.NETアプリケーションを実行できます。 ASP.NETプロジェクトの名前が&#x200B;*InvokePreLoanProcess*&#x200B;の場合、Webブラウザー内で次のURLを指定します。

*http://localhost:1629/InvokePreLoanProcess/*Default.aspx

localhostは、ASP.NETプロジェクトをホストするwebサーバーの名前で、1629はポート番号です。 ASP.NETアプリケーションをコンパイルしてビルドすると、Microsoft Visual Studioによって自動的にデプロイされます。

>[!NOTE]
>
>ASP.NETアプリケーションがプロセスを呼び出したことを確認するには、開始ワークスペースを使用し、ローンを受け入れます。

## 人間中心の長期間有効なプロセスを呼び出す、Flexで構築されたクライアントアプリケーションの作成{#creating-a-client-application-built-with-flex-that-invokes-a-human-centric-long-lived-process}

*FirstAppSolution/PreLoanProcess*&#x200B;プロセスを呼び出すために、Flexで構築したクライアントアプリケーションを作成できます。 このアプリケーションは、Remotingを使用して&#x200B;*FirstAppSolution/PreLoanProcess*&#x200B;プロセスを呼び出します。 (「[AEM Formsリモートを使用したAEM Formsの呼び出し(AEM formsでは廃止)](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)」を参照)。

次の図に、エンドユーザーからデータを収集するFlexで構築されたクライアントアプリケーションを示します。 データはXMLデータソースに配置され、プロセスに送信されます。

プロセスの呼び出し後に、呼び出し識別子の値が表示されます。 呼び出し識別子の値は、長期間有効なプロセスのステータスを追跡するレコードの一部として作成されます。

Flexで構築されたクライアントアプリケーションは、次のタスクを実行します。

* ユーザーがWebページに入力した値を取得します。
* *FirstAppSolution/PreLoanProcess*&#x200B;プロセスに渡されるXMLデータソースを動的に作成します。 3つの値は、XMLデータソースで指定されます。
* Remotingを使用して&#x200B;*FirstAppSolution/PreLoanProcess*&#x200B;プロセスを呼び出します。
* 長期間有効なプロセスの呼び出し識別子の値を返します。

### 手順{#summary_of_steps-2}の概要

FirstAppSolution/PreLoanProcessプロセスを呼び出すことができるFlexで構築されたクライアントアプリケーションを作成するには、次の手順を実行します。

1. 新しいFlexプロジェクトを開始。
1. プロジェクトのクラスパスにadobe-remoting-provider.swcファイルを含めます。 ([AEM FormsFlexライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)を参照)。
1. ActionScriptまたはMXMLを使用して`mx:RemoteObject`インスタンスを作成します。 （「[mx:RemoteObjectインスタンスの作成](/help/forms/developing/invoking-aem-forms-using-remoting.md)」を参照）。
1. `ChannelSet`インスタンスを設定して、AEM Formsと通信し、`mx:RemoteObject`インスタンスに関連付けます。 (「[AEM Forms](/help/forms/developing/invoking-aem-forms-using-remoting.md)へのチャネルを作成する」を参照)。
1. ChannelSetの`login`メソッドまたはサービスの`setCredentials`メソッドを呼び出して、ユーザー識別子の値とパスワードを指定します。 （「[シングルサインオンの使用](/help/forms/developing/invoking-aem-forms-using-remoting.md#using-single-sign-on)」を参照）。
1. XMLインスタンスを作成して、`FirstAppSolution/PreLoanProcess`プロセスに渡すXMLデータソースを作成します。 （このアプリケーションロジックは次のコード例に示します）。
1. コンストラクターを使用して、Object型のオブジェクトを作成します。 次のコードに示すように、プロセスの入力パラメーターの名前を指定して、XMLをオブジェクトに割り当てます。

   ```csharp
    //Get the XML data to pass to the AEM Forms process
    var xml:XML = createXML();
    var params:Object = new Object();
    params["formData"]=xml;
   ```

1. `mx:RemoteObject`インスタンスの`invoke_Async`メソッドを呼び出して、`FirstAppSolution/PreLoanProcess`プロセスを呼び出します。 入力パラメーターを含む`Object`を渡します。 （[入力値](/help/forms/developing/invoking-aem-forms-using-remoting.md)を渡すを参照）。
1. 次のコードに示すように、長期間有効なプロセスから返される呼び出し識別値を取得します。

   ```csharp
    // Handles async call that invokes the long-lived process
    private function resultHandler(event:ResultEvent):void
    {
    ji = event.result as JobId;
    jobStatusDisplay.text = "Job Status ID: " + ji.jobId as String;
    }
   ```

### Remoting {#invoking-a-long-lived-process-using-remoting}を使用した長期間有効なプロセスの呼び出し

以下のFlexコードの例は、`FirstAppSolution/PreLoanProcess`プロセスを呼び出します。

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

