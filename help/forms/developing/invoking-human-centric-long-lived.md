---
title: 人間中心の長期間有効なプロセスの呼び出し
seo-title: 人間中心の長期間有効なプロセスの呼び出し
description: 'null'
seo-description: 'null'
uuid: 42269d41-a90f-4ea1-aeb9-d61337bcfa54
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: 18a320b4-dce6-4c50-8864-644b0b2d6644
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '3669'
ht-degree: 4%

---


# 人間中心の長期間有効なプロセスの呼び出し {#invoking-human-centric-long-lived-processes}

次のクライアントアプリケーションを使用して、Workbenchで作成された人間中心の長期間有効なプロセスをプログラムで呼び出すことができます。

* 呼び出しAPIを使用するJava Webベースのクライアントアプリケーション。 (Java APIを使用したAEM Formsの [呼び出し](/help/forms/developing/invoking-aem-forms-using-java.md)(/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api)を参照)。
* Webサービスを使用するASP.NETアプリケーション。 (See [Invoking AEM Forms Using Web Services](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)
* Flexで構築された、Remotingを使用するクライアントアプリケーション。 (「 [AEM Formsの呼び出し」（AEM Formsでは非推奨）AEM Formsのリモート処理を使用した呼び出し](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)」を参照)。

呼び出される長期間有効なプロセスは、FirstAppSolution/PreLoanProcessという名前 *です*。 このプロセスは、「最初のAEM Formsアプリケーションの [作成」で指定したチュートリアルに従って作成できます](https://www.adobe.com/go/learn_aemforms_firstapp_ds_63)。

人間中心のプロセスには、ユーザーがWorkspaceを使用して応答できるタスクが含まれます。 例えば、Workbenchを使用する場合、銀行の管理者がローンの申し込みを承認または拒否できるプロセスを作成できます。 次の図に、FirstAppSolution/PreLoanProcess *のプロセスを示します*。

FirstAppSolution/PreLoanProcess *プロセスは、データタイプがXMLである* formData ** という名前の入力パラメーターを受け取ります。 このXMLデータは、PreLoanForm.xdpという名前のフォームデザインとマージされ *ます*。 次の図に示すフォームは、ローンの申し込みを承認または拒否するためにユーザーに割り当てられたタスクを表しています。 ユーザーがWorkspaceを使用してアプリケーションを承認または拒否します。 Workspaceユーザーは、次の図に示す「Approve」ボタンをクリックして、ローン要求を承認できます。 同様に、ユーザーは「拒否」ボタンをクリックしてローンの要求を拒否できます。

長期間有効なプロセスは、非同期で呼び出され、次の要因により、同期的に呼び出すことはできません。

* プロセスは、かなりの期間に及ぶことがあります。
* プロセスは、組織の境界をまたぐことができます。
* プロセスを終了するには、外部入力が必要です。 例えば、不在の管理者にフォームが送信される場合を考えてみます。 この場合、マネージャーがフォームを返して入力するまで、プロセスは完了しません。

長期間有効なプロセスが呼び出されると、AEM Formsは、レコードの作成の一部として呼び出し識別子の値を作成します。 このレコードは、長期間有効なプロセスのステータスを追跡し、AEM Formsデータベースに保存されます。 呼び出し識別子の値を使用して、長期間有効なプロセスのステータスを追跡できます。 また、プロセス呼び出し識別子の値を使用して、実行中のプロセスインスタンスの終了など、Process Manager操作を実行できます。

>[!NOTE]
>
>短時間のみ有効なプロセスが呼び出された場合、AEM Formsは呼び出し識別子の値やレコードを作成しません。

この `FirstAppSolution/PreLoanProcess` プロセスは、XMLデータとして表される申込書が申込者から送信されたときに呼び出されます。 入力プロセス変数の名前 `formData` とデータ型はXMLです。 この説明の目的で、次のXMLデータがプロセスへの入力として使用されると仮定し `FirstAppSolution/PreLoanProcess` ます。

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <LoanApp>
 <Name>Sam White</Name>
 <LoanAmount>250000</LoanAmount>
 <PhoneOrEmail>(555)555-5555</PhoneOrEmail>
 <ApprovalStatus>PENDING APPROVAL</ApprovalStatus>
 </LoanApp>
```

プロセスに渡されるXMLデータは、プロセスで使用されるフォーム内のフィールドと一致する必要があります。 それ以外の場合、データはフォーム内に表示されません。 プロセスを呼び出すすべてのアプリケーションは、このXMLデータソースを渡す必要があり `FirstAppSolution/PreLoanProcess` ます。 「人間中心の長期間有効なプロセスの *呼び出し* 」で作成したアプリケーションは、ユーザーがWebクライアントに入力した値からXMLデータソースを動的に作成します。

クライアントアプリケーションを使用して、FirstAppSolution/PreLoanProcess ** プロセスに必要なXMLデータを送信できます。 長期間有効なプロセスは、呼び出し識別子の値を戻り値として返します。 次の図に、*FirstAppSolution/PreLoanProcessの長期間有効なプロセスを呼び出すクライアントアプリケーションを示します。 クライアントアプリケーションはXMLデータを送信し、呼び出し識別子の値を表すstring値を返します。

**関連トピック**

[人間中心の長期間有効なプロセスを呼び出す Java Web アプリケーションの作成](invoking-human-centric-long-lived.md#creating-a-java-web-application-that-invokes-a-human-centric-long-lived-process)

[人間中心の長期間有効なプロセスを呼び出すASP.NET Webアプリケーションの作成](invoking-human-centric-long-lived.md#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process)

[人間中心の長期間有効なプロセスを呼び出すFlexで構築されたクライアントアプリケーションの作成](invoking-human-centric-long-lived.md#creating-a-client-application-built-with-flex-that-invokes-a-human-centric-long-lived-process)

## 人間中心の長期間有効なプロセスを呼び出す Java Web アプリケーションの作成 {#creating-a-java-web-application-that-invokes-a-human-centric-long-lived-process}

Javaサーブレットを使用してプロセスを呼び出すWebベースのアプリケーションを作成でき `FirstAppSolution/PreLoanProcess` ます。 Javaサーブレットからこのプロセスを呼び出すには、Javaサーブレット内でInvocation APIを使用します。 (See [Invoking AEM Forms using the Java API](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api).)

次の図に、name、phone（またはemail）およびamountの値を投稿するWebベースのクライアントアプリケーションを示します。 これらの値は、ユーザーが「Submit Application」ボタンをクリックするとJavaサーブレットに送信されます。

Javaサーブレットは次のタスクを実行します。

* HTMLページからJavaサーブレットに投稿された値を取得します。
* FirstAppSolution/PreLoanProcess ** プロセスに渡すXMLデータソースを動的に作成します。 名前、電話（または電子メール）、金額の値は、XMLデータソースで指定されます。
* AEM Forms呼び出しAPIを使用して *FirstAppSolution/PreLoanProcess* プロセスを呼び出します。
* 呼び出し識別子の値をクライアントWebブラウザーに返します。

### 手順の概要 {#summary-of-steps}

プロセスを呼び出すJava Webベースのアプリケーションを作成するには、次の手順を実行し `FirstAppSolution/PreLoanProcess` ます。

1. [Webプロジェクトを作成します](invoking-human-centric-long-lived.md#create-a-web-project)。
1. [サーブレット用のJavaアプリケーションロジックを作成します](invoking-human-centric-long-lived.md#create-java-application-logic-for-the-servlet)。
1. [Webアプリケーション用のWebページの作成](invoking-human-centric-long-lived.md#create-the-web-page-for-the-web-application)
1. [WebアプリケーションをWARファイルにパッケージ化します](invoking-human-centric-long-lived.md#package-the-web-application-to-a-war-file)。
1. [WARファイルを、AEM FormsをホストするJ2EEアプリケーションサーバーにデプロイします](invoking-human-centric-long-lived.md#deploy-the-war-file-to-the-j2ee-application-server-hosting-aem-forms)。
1. [Webアプリケーションをテストします](invoking-human-centric-long-lived.md#test-your-web-application)。

>[!NOTE]
>
>これらの手順の一部は、AEM FormsがデプロイされるJ2EEアプリケーションに依存します。 例えば、WARファイルのデプロイに使用する方法は、使用しているJ2EEアプリケーションサーバーによって異なります。 AEM FormsがJBoss®にデプロイされていることを前提としています。

### Webプロジェクトの作成 {#create-a-web-project}

Webアプリケーションを作成する最初の手順は、Webプロジェクトを作成することです。 このドキュメントが基盤とするJava IDEはEclipse 3.3です。Eclipse IDEを使用してWebプロジェクトを作成し、必要なJARファイルをプロジェクトに追加します。 プロジ追加ェクトに対する *index.htmlというHTMLページ* 、およびJavaサーブレット。

次のリストは、Webプロジェクトに含めるJARファイルを指定します。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* J2EE.jar

For the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

>[!NOTE]
>
>J2EE.jarファイルは、Javaサーブレットで使用されるデータ型を定義します。 このJARファイルは、AEM FormsがデプロイされるJ2EEアプリケーションサーバーから取得できます。

**Webプロジェクトの作成**

1. 開始Eclipseを開き、 **File** / **New Project**&#x200B;をクリックします。
1. **新規プロジェクト** ダイアログボックスで、 **Web** / **ダイナミックWebプロジェクト**&#x200B;を選択します。
1. プロジェクト `InvokePreLoanProcess` の名前を入力し、「 **完了**」をクリックします。

**プロジェクトに追加必要なJARファイル**

1. 「プロジェクト・エクスプローラ」ウィンドウで、 `InvokePreLoanProcess` プロジェクトを右クリックし、「 **プロパティ**」を選択します。
1. 「 **Java build path** 」をクリックし、「 **Libraries** 」タブをクリックします。
1. 「 **External JARs** 」ボタンをクリックし、含めるJARファイルを参照します。

**プロジ追加ェクトへのJavaサーブレット**

1. 「プロジェクト・エクスプローラ」ウィンドウで、 `InvokePreLoanProcess` プロジェクトを右クリックし、「 **新規** 」>「 **その他**」を選択します。
1. [ **Web** ]フォルダを展開し、[ **サーブレット**]を選択して[ **次へ**]をクリックします。
1. 「サーブレットを作成」ダイアログで、サーブレットの名前 `SubmitXML` を入力し、「 **完了**」をクリックします。

**プロジ追加ェクトのHTMLページ**

1. 「プロジェクト・エクスプローラ」ウィンドウで、 `InvokePreLoanProcess` プロジェクトを右クリックし、「 **新規** 」>「 **その他**」を選択します。
1. 「 **Web** 」フォルダーを展開し、「 **HTML**」を選択して「 **次へ**」をクリックします。
1. 新規HTMLダイアログボックスで、ファイル名 `index.html` を入力し、「 **完了**」をクリックします。

>[!NOTE]
>
>SubmitXML Javaサーブレットを呼び出すHTMLコンテンツの作成について詳しくは、Webアプリケーション用のWebページの [作成を参照してください](invoking-human-centric-long-lived.md#create-the-web-page-for-the-web-application)。

### サーブレット用のJavaアプリケーションロジックの作成 {#create-java-application-logic-for-the-servlet}

Javaサーブレット内からプロセスを呼び出すJavaアプリケ `FirstAppSolution/PreLoanProcess` ーションロジックを作成します。 次のコードは、 `SubmitXML` Javaサーブレットの構文を示しています。

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

通常、クライアントコードはJavaサーブレット `doGet` または `doPost` メソッド内に配置しません。 このコードを別のクラスに配置する方が、より良いプログラミング方法です。 次に、メソッド（またはメソッド）内からクラスをインスタンス化し、適切な `doPost` メソッドを呼び出し `doGet` ます。 ただし、コードを簡潔にするために、コード例は最小限に抑えられ、 `doPost` メソッドに配置されます。

呼び出しAPIを使用して `FirstAppSolution/PreLoanProcess` プロセスを呼び出すには、次のタスクを実行します。

1. Javaプロジェクトのクラスパスに、adobe-livecycle-client.jarなどのクライアントJARファイルを含めます。 これらのファイルの場所については、[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。
1. HTMLページから送信された名前、電話番号、金額の値を取得します。 これらの値を使用して、プロセスに送信するXMLデータソースを動的に作成し `FirstAppSolution/PreLoanProcess` ます。 XMLデータソースの作成には、 `org.w3c.dom` クラスを使用できます（このアプリケーションロジックは次のコード例に示します）。
1. 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。（[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照。）
1. コンストラクタを使用して `ServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。`ServiceClient` オブジェクトを使用すると、サービス操作を呼び出すことができます。呼び出し要求の検索、ディスパッチ、ルーティングなどのタスクを処理します。
1. コンストラクタを使用して `java.util.HashMap` オブジェクトを作成します。
1. 各入力パラメーターに対して `java.util.HashMap` オブジェクトの `put` メソッドを呼び出して、長期間有効なプロセスに渡します。プロセスの入力パラメーターの名前を必ず指定してください。 この `FirstAppSolution/PreLoanProcess` プロセスには（名前付きの）型の入力パラメーターが1つ必要なので、この `XML``formData``put` メソッドを呼び出す必要があるのは1回だけです。

   ```java
    //Get the XML to pass to the FirstAppSolution/PreLoanProcess process
    org.w3c.dom.Document inXML = GetDataSource(name,phone,amount);
    
    //Create a Map object to store the parameter value
    Map params = new HashMap();
    params.put("formData", inXML);
   ```

1. Create an `InvocationRequest` object by invoking the `ServiceClientFactory` object’s `createInvocationRequest` method and passing the following values:

   * 長期間有効なプロセスを指定する文字列値。プロセスを呼び出すには、 `FirstAppSolution/PreLoanProcess` を指定し `FirstAppSolution/PreLoanProcess`ます。
   * プロセス操作名を表す文字列値。長期間有効なプロセス操作の名前はで `invoke`す。
   * サービス操作に必要なパラメーター値を含む `java.util.HashMap` オブジェクト。
   * A Boolean value that specifies `false`, which creates an asynchronous request (this value is applicable to invoke a long-lived process).

   >[!NOTE]
   >
   >*短時間のみ有効なプロセスは、createInvocationRequestメソッドの4番目のパラメーターとして値trueを渡すことで呼び出すことができます。 値trueを渡すと、同期要求が作成されます。*

1. Send the invocation request to AEM Forms by invoking the `ServiceClient` object’s `invoke` method and passing the `InvocationRequest` object. The `invoke` method returns an `InvocationReponse` object.
1. 長期間有効なプロセスは、呼び出し識別値を表すstring値を返します。 オブジェクトのメソッドを呼び出して、 `InvocationReponse` この値を取得し `getInvocationId` ます。

   ```java
    //Send the invocation request to the long-lived process and
    //get back an invocation response object
    InvocationResponse lcResponse = myServiceClient.invoke(lcRequest);
    String invocationId = lcResponse.getInvocationId();
   ```

1. 呼び出しID値をクライアントWebブラウザーに書き込みます。 インスタンスを使用して、この値をクライアントWebブラウザーに書き込むことができ `java.io.PrintWriter` ます。

### Quick Start: Invoking a long-lived process using the Invocation API {#quick-start-invoking-a-long-lived-process-using-the-invocation-api}

次のJavaコードの例は、 `FirstAppSolution/PreLoanProcess` プロセスを呼び出すJavaサーブレットを表しています。

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

### Webアプリケーション用のWebページの作成 {#create-the-web-page-for-the-web-application}

*index.html* Webページは、プロセスを呼び出すJavaサーブレットへのエントリポイントを提供し `FirstAppSolution/PreLoanProcess` ます。 このWebページは、HTMLフォームと送信ボタンを含む基本的なHTMLフォームです。 ユーザーが「送信」ボタンをクリックすると、フォームデータが `SubmitXML` Javaサーブレットに投稿されます。

Javaサーブレットは、次のJavaコードを使用して、HTMLページから投稿されたデータを取得します。

```java
 //Get the values that are passed from the Loan HTML page
 String name = request.getParameter("name");
 String phone = request.getParameter("phone");
 String amount = request.getParameter("amount");
```

次のHTMLコードは、開発環境のセットアップ中に作成されたindex.htmlファイルを表しています。 (Webプロジェクトの [作成を参照](invoking-human-centric-long-lived.md#create-a-web-project))。

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

### WebアプリケーションのWARファイルへのパッケージ化 {#package-the-web-application-to-a-war-file}

プロセスを呼び出すJavaサーブレットをデプロイするには、WebアプリケーションをWARファイルにパッケージ化します。 `FirstAppSolution/PreLoanProcess` コンポーネントのビジネスロジックが依存する外部JARファイル（adobe-livecycle-client.jarやadobe-usermanager-client.jarなど）もWARファイルに含めてください。

次の図に、WARファイルにパッケージ化されたEclipseプロジェクトのコンテンツを示します。

>[!NOTE]
>
>上の図では、JPGファイルは任意のJPG画像ファイルに置き換えることができます。

**WebアプリケーションのWARファイルへのパッケージ化：**

1. 「 **プロジェクトエクスプローラ** 」(Project Explorer)ウィンドウで、 `InvokePreLoanProcess` プロジェクトを右クリックし、「 **エクスポート** 」(Export) **/「** WARファイル」(WAR file)を選択します。
1. 「 **Webモジュール** 」テキストボックスに、Javaプロジェクト `InvokePreLoanProcess` の名前を入力します。
1. 「 **Destination** 」テキストボックス `PreLoanProcess.war`**に、**ファイル名を入力し、WARファイルの場所を指定して、「Finish」をクリックします。

### WARファイルを、AEM FormsをホストするJ2EEアプリケーションサーバーにデプロイします {#deploy-the-war-file-to-the-j2ee-application-server-hosting-aem-forms}

WARファイルを、AEM Formsのデプロイ先のJ2EEアプリケーションサーバーにデプロイします。 WARファイルをJ2EEアプリケーションサーバーにデプロイするには、WARファイルを書き出しパスからにコピーし `[AEM Forms Install]\Adobe\Adobe Experience Manager Forms\jboss\server\lc_turnkey\deploy`ます。

>[!NOTE]
>
>AEM FormsがJBossにデプロイされていない場合は、J2EE Application ServerのホスティングAEM Formsに準拠したWARファイルをデプロイする必要があります。

### Webアプリケーションのテスト {#test-your-web-application}

Webアプリケーションをデプロイした後、Webブラウザーを使用してテストできます。 AEM Formsをホストしているのと同じコンピューターを使用している場合は、次のURLを指定できます。

* http://localhost:8080/PreLoanProcess/index.html

   HTMLフォームのフィールドに値を入力し、「Submit Application」ボタンをクリックします。 問題が発生した場合は、J2EEアプリケーションサーバーのログファイルを参照してください。

>[!NOTE]
>
>Javaアプリケーションがプロセスを呼び出したことを確認するために、開始ワークスペースでローンを受け入れます。

## Creating an ASP.NET web application that invokes a human-centric long-lived process {#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process}

プロセスを呼び出すASP.NETアプリケーションを作成でき `FirstAppSolution/PreLoanProcess` ます。 ASP.NETアプリケーションからこのプロセスを呼び出すには、Webサービスを使用します。 (See [Invoking AEM Forms using Web Services](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)

次の図に、エンドユーザーからデータを取得するASP.NETクライアントアプリケーションを示します。 データはXMLデータソースに配置され、ユーザーが「Submit Application」ボタンをクリックするとプロセスに送信されます。 `FirstAppSolution/PreLoanProcess`

プロセスの呼び出し後に、呼び出し識別子の値が表示されます。 呼び出し識別子の値は、長期間有効なプロセスのステータスを追跡するレコードの一部として作成されます。

ASP.NETアプリケーションは、次のタスクを実行します。

* ユーザーがWebページに入力した値を取得します。
* * FirstAppSolution/PreLoanProcess *processに渡されるXMLデータソースを動的に作成します。 3つの値は、XMLデータソースで指定されます。
* Webサービスを使用して、* FirstAppSolution/PreLoanProcess *processを呼び出します。
* 呼び出し識別子の値と、長期間有効な操作のステータスをクライアントWebブラウザーに返します。

### 手順の概要 {#summary_of_steps-1}

FirstAppSolution/PreLoanProcessプロセスを呼び出すことのできるASP.NETアプリケーションを作成するには、次の手順を実行します。

1. [ASP.NET Webアプリケーションを作成します](invoking-human-centric-long-lived.md#create-an-asp-net-web-application)。
1. [FirstAppSolution/PreLoanProcessを呼び出すASPページを作成します](invoking-human-centric-long-lived.md#create-an-asp-page-that-invokes-firstappsolution-preloanprocess)。
1. [ASP.NETアプリケーションを実行します](invoking-human-centric-long-lived.md#run-the-asp-net-application)。

### ASP.NET Webアプリケーションの作成 {#create-an-asp-net-web-application}

Microsoft .NET C# ASP.NETWeb アプリケーションを作成します。 次の図は、InvokePreLoanProcessという名前のASP.NETプロジェクトの内容を示し *ています*。

「Service References」の下に2つの項目があります。 最初のアイテムは* JobManager*という名前です。 この参照は、ASP.NETアプリケーションがJob Managerサービスを呼び出せるようにします。 このサービスは、長期間有効なプロセスのステータスに関する情報を返します。 例えば、プロセスが現在実行中である場合、このサービスは、プロセスが現在実行中であることを示す数値を返します。 2番目の参照はPreLoanProcess *という名前です*。 このサービスリファレンスは、* FirstAppSolution/PreLoanProcess *processへの参照を表します。 サービス参照を作成すると、AEM Formsサービスに関連付けられたデータ型を.NETプロジェクト内で使用できるようになります。

**ASP.NETプロジェクトを作成する：**

1. 開始Microsoft Visual Studio 2008。
1. [ **ファイル** ]メニューから[ **新規**]、[ **Webサイト**]の順に選択します。
1. [ **テンプレート** ]リストで[ **ASP.NET Webサイト**]を選択します。
1. 「 **場所** 」ボックスで、プロジェクトの場所を選択します。 プロジェクトにInvokePreLoanProcessとい *う名前を付けます*。
1. 「 **言語** 」ボックスで、「Visual C#」を選択します。
1. 「OK」をクリックします。

**追加サービス参照：**

1. 「プロジェクト」メニューで、「 **追加サービス参照**」を選択します。
1. 「 **アドレス** 」ダイアログボックスで、Job ManagerサービスのWSDLを指定します。

   ```java
    https://hiro-xp:8080/soap/services/JobManager?WSDL&lc_version=9.0.1
   ```

1. 「名前空間」フィールドに、と入力し `JobManager`ます。
1. Click **Go** and then click **OK**.
1. 「 **プロジェクト****」メニューで、「**&#x200B;サービス参照」を選択します。
1. 「 **アドレス** 」ダイアログボックスで、FirstAppSolution/PreLoanProcessプロセスのWSDLを指定します。

   ```java
    https://hiro-xp:8080/soap/services/FirstAppSolution/PreLoanProcess?WSDL&lc_version=9.0.1
   ```

1. 「名前空間」フィールドに、と入力し `PreLoanProcess`ます。
1. Click **Go** and then click **OK**.

>[!NOTE]
>
>AEM Forms `hiro-xp` をホストするJ2EEアプリケーションサーバーのIPアドレスに置き換えます。 この `lc_version` オプションを使用すると、MTOMなどのAEM Forms機能を使用できるようになります。 この `lc_version`オプションを指定しないと、MTOMを使用してAEM Formsを呼び出すことはできません。 (MTOMを使用したAEM Formsの [呼び出しを参照](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom))。

### FirstAppSolution/PreLoanProcessを呼び出すASPページを作成します {#create-an-asp-page-that-invokes-firstappsolution-preloanprocess}

ASP.NETプロジェクト内に、HTMLページをローンの申込者に表示するWebフォーム（ASPXファイル）を追加します。 Webフォームは、から派生するクラスに基づいてい `System.Web.UI.Page`ます。 を呼び出すC#アプリケーションロジック `FirstAppSolution/PreLoanProcess` は、 `Button1_Click` メソッド内にあります（このボタンは「Submit Application」ボタンを表します）。

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

ASP.NETアプリケーションの一部であるアプリケーションロジックは、プロセスに渡すXMLデータソースを動的に作成する必要があり `FirstAppSolution/PreLoanProcess` ます。 申込者がHTMLページに入力した値は、XMLデータソース内で指定する必要があります。 これらのデータ値は、フォームがWorkspaceで表示されるときに、フォームにマージされます。 名前空間内のクラスは、XMLデータソースの作成に使用され `System.Xml` ます。

ASP.NETアプリケーションからXMLデータを必要とするプロセスを呼び出す場合、XMLデータ型を使用できます。 つまり、インスタンスをプロセスに渡すこ `System.Xml.XmlDocument` とはできません。 プロセスに渡すこのXMLインスタンスの完全修飾名はで `InvokePreLoanProcess.PreLoanProcess.XML`す。 インスタンスをに変換 `System.Xml.XmlDocument` し `InvokePreLoanProcess.PreLoanProcess.XML`ます。 このタスクは、次のコードを使用して実行できます。

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

プロセスを呼び出すASPページを作成するには、 `FirstAppSolution/PreLoanProcess` メソッドで次のタスクを実行し `Button1_Click` ます。

1. Create a `FirstAppSolution_PreLoanProcessClient` object by using its default constructor.
1. Create a `FirstAppSolution_PreLoanProcessClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLをAEM Formsサービスに渡し、エンコードの種類を指定するstring値を渡します。

   ```java
    https://hiro-xp:8080/soap/services/FirstAppSolution/PreLoanProcess?blob=mtom
   ```

   属性を使用する必要はありません `lc_version` 。 この属性は、サービス参照を作成する際に使用されます。 ただし、必ず指定を行ってください `?blob=mtom`。

   >[!NOTE]
   >
   >「 `hiro-xp`*」は、J2EEアプリケーションサーバーのホスティングAEM FormsのIPアドレスに置き換えます。 *

1. データメンバの値を取得して、 `System.ServiceModel.BasicHttpBinding` オブジェクトを作成し `FirstAppSolution_PreLoanProcessClient.Endpoint.Binding` ます。 戻り値を `BasicHttpBinding` にキャストします。
1. オブジェクトの `System.ServiceModel.BasicHttpBinding` デー `MessageEncoding` タメンバをに設定し `WSMessageEncoding.Mtom`ます。 この値により、MTOMが使用されます。
1. 次のタスクを実行して、基本的なHTTP認証を有効にします。

   * AEM Formsのユーザー名をデータメンバーに割り当て `FirstAppSolution_PreLoanProcessClient.ClientCredentials.UserName.UserName`ます。
   * 対応するパスワード値をデータメンバーに割り当て `FirstAppSolution_PreLoanProcessClient.ClientCredentials.UserName.Password`ます。
   * 定数値をデータメンバ `HttpClientCredentialType.Basic` ーに割り当て `BasicHttpBindingSecurity.Transport.ClientCredentialType`ます。
   * 定数値をデータメンバ `BasicHttpSecurityMode.TransportCredentialOnly` ーに割り当て `BasicHttpBindingSecurity.Security.Mode`ます。

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

1. ユーザーがWebページに入力した名前、電話番号、金額の値を取得します。 これらの値を使用して、プロセスに送信するXMLデータソースを動的に作成し `FirstAppSolution/PreLoanProcess` ます。 プロセス `System.Xml.XmlDocument` に渡すXMLデータソースを表すXMLを作成します（このアプリケーションロジックは次のコード例に示します）。
1. インスタンスを `System.Xml.XmlDocument` に変換し `InvokePreLoanProcess.PreLoanProcess.XML` ます（次のコードの例に、このアプリケーションロジックを示します）。
1. オブジェクトの `FirstAppSolution/PreLoanProcess` メソッドを呼び出して、 `FirstAppSolution_PreLoanProcessClient` プロセスを呼び出し `invoke_Async` ます。 このメソッドは、長期間有効なプロセスの呼び出し識別子の値を表すstring値を返します。
1. isコンストラクタ `JobManagerClient` を使用してを作成します。 （Job Managerサービスへのサービス参照が設定されていることを確認します）。
1. 手順1 ～ 5を繰り返します。 手順2では、次のURLを指定します。 `https://hiro-xp:8080/soap/services/JobManager?blob=mtom`.
1. コンストラクタを使用して `JobId` オブジェクトを作成します。
1. オブジェクトの `JobId` データメンバーを、オブジェクトのメ `id` ソッドの戻り値に設定し `FirstAppSolution_PreLoanProcessClient``invoke_Async` ます。
1. trueを `value` オブジェクトの `JobId``persistent` データメンバに割り当てます。
1. オブジェクトのメソッドを呼び出し、オブジェクトを渡して、オブジ `JobStatus` ェクトを作成し `JobManagerService``getStatus``JobId` ます。
1. オブジェクトの `JobStatus``statusCode` データメンバの値を取得して、ステータス値を取得します。
1. 呼び出し識別子の値をフィー `LabelJobID.Text` ルドに割り当てます。
1. フィールドにステータス値を割り当て `LabelStatus.Text` ます。

### クイック開始: WebサービスAPIを使用した長期間有効なプロセスの呼び出し {#quick-start-invoking-a-long-lived-process-using-the-web-service-api}

次のC#コードの例は、 `FirstAppSolution/PreLoanProcess`プロセスを呼び出します。

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

### ASP.NETアプリケーションの実行 {#run-the-asp-net-application}

ASP.NETアプリケーションをコンパイルして展開した後は、Webブラウザーを使用してASP.NETアプリケーションを実行できます。 ASP.NETプロジェクトの名前がInvokePreLoanProcessの場合は、Webブラウザー内で *次のURLを指定します*。

*http://localhost:1629/InvokePreLoanProcess/*Default.aspx

localhostは、ASP.NETプロジェクトをホストするwebサーバーの名前で、1629はポート番号です。 ASP.NETアプリケーションをコンパイルしてビルドすると、Microsoft Visual Studioによって自動的にデプロイされます。

>[!NOTE]
>
>ASP.NETアプリケーションがプロセスを呼び出したことを確認するには、開始ワークスペースを使用し、ローンを受け入れます。

## 人間中心の長期間有効なプロセスを呼び出すFlexで構築されたクライアントアプリケーションの作成 {#creating-a-client-application-built-with-flex-that-invokes-a-human-centric-long-lived-process}

Flexで構築されたクライアントアプリケーションを作成して、FirstAppSolution/PreLoanProcess ** プロセスを呼び出すことができます。 このアプリケーションは、Remotingを使用してFirstAppSolution/PreLoanProcess ** プロセスを呼び出します。 (「 [AEM Formsの呼び出し」（AEM Formsでは非推奨）AEM Formsのリモート処理を使用した呼び出し](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting)」を参照)。

次の図に、Flexで構築され、エンドユーザーからデータを収集するクライアントアプリケーションを示します。 データはXMLデータソースに配置され、プロセスに送信されます。

プロセスの呼び出し後に、呼び出し識別子の値が表示されます。 呼び出し識別子の値は、長期間有効なプロセスのステータスを追跡するレコードの一部として作成されます。

Flexで構築されたクライアントアプリケーションは、次のタスクを実行します。

* ユーザーがWebページに入力した値を取得します。
* FirstAppSolution/PreLoanProcess ** プロセスに渡されるXMLデータソースを動的に作成します。 3つの値は、XMLデータソースで指定されます。
* Remotingを使用して *FirstAppSolution/PreLoanProcess* プロセスを呼び出します。
* 長期間有効なプロセスの呼び出し識別子の値を返します。

### 手順の概要 {#summary_of_steps-2}

FirstAppSolution/PreLoanProcessプロセスを呼び出すことができるFlexで構築されたクライアントアプリケーションを作成するには、次の手順を実行します。

1. 新しいFlexプロジェクトの開始。
1. プロジェクトのクラスパスにadobe-remoting-provider.swcファイルを含めます。 (FlexライブラリファイルのAEM Forms [を含めるを参照](/help/forms/developing/invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file))。
1. ActionScriptまたはMXMLを使用して `mx:RemoteObject` インスタンスを作成します。 (mx:RemoteObjectインスタンスの [作成を参照](/help/forms/developing/invoking-aem-forms-using-remoting.md))。
1. AEM Formsと通信する `ChannelSet` インスタンスを設定し、そのインスタンスに関連付け `mx:RemoteObject` ます。 (AEM Formsへのチャネルの [作成を参照](/help/forms/developing/invoking-aem-forms-using-remoting.md))。
1. ChannelSetの `login``setCredentials` メソッドまたはサービスのメソッドを呼び出して、ユーザー識別子の値とパスワードを指定します。 (シングルサインオン [の使用を参照](/help/forms/developing/invoking-aem-forms-using-remoting.md#using-single-sign-on))。
1. XMLインスタンスを作成して、プロセスに渡すXMLデータソースを作成し `FirstAppSolution/PreLoanProcess` ます。 （このアプリケーションロジックは次のコード例に示します）。
1. コンストラクターを使用して、Object型のオブジェクトを作成します。 次のコードに示すように、プロセスの入力パラメーターの名前を指定して、XMLをオブジェクトに割り当てます。

   ```csharp
    //Get the XML data to pass to the AEM Forms process
    var xml:XML = createXML();
    var params:Object = new Object();
    params["formData"]=xml;
   ```

1. インスタンスの `FirstAppSolution/PreLoanProcess` メソッドを呼び出して、 `mx:RemoteObject``invoke_Async` プロセスを呼び出します。 入力パラメーター `Object` を含むを渡します。 ( [入力値の渡しを参照](/help/forms/developing/invoking-aem-forms-using-remoting.md))。
1. 次のコードに示すように、長期間有効なプロセスから返される呼び出し識別値を取得します。

   ```csharp
    // Handles async call that invokes the long-lived process
    private function resultHandler(event:ResultEvent):void
    {
    ji = event.result as JobId;
    jobStatusDisplay.text = "Job Status ID: " + ji.jobId as String;
    }
   ```

### Remotingを使用した長期間有効なプロセスの呼び出し {#invoking-a-long-lived-process-using-remoting}

次のFlexコードの例は、プロセスを呼び出し `FirstAppSolution/PreLoanProcess` ます。

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

