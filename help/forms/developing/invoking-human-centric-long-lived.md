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
source-git-commit: 67ea825215d1ca7cc2e350ed1c128c3146de45ec

---


# 人間中心の長期間有効なプロセスの呼び出し {#invoking-human-centric-long-lived-processes}

次のクライアントアプリケーションを使用して、Workbenchで作成された人間中心の長期間有効なプロセスをプログラムで呼び出すことができます。

* 呼び出しAPIを使用するJava webベースのクライアントアプリケーション。 (「Java API [を使用したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-java.md)」を参照)。
* Webサービスを使用するASP.NETアプリケーションです。 (See [Invoking AEM Forms Using Web Services](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)
* Remotingを使用するFlexで構築されたクライアントアプリケーション。 (『AEM Forms Remoting [を使用したAEM Formsの呼び出し(AEM Formsでは非推奨](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting))』を参照)。

呼び出される長期間有効なプロセスの名前は *FirstAppSolution/PreLoanProcessです*。 このプロセスは、「最初のAEM Formsアプリケーションの作成」で指定さ [れたチュートリアルに従って作成できます](https://www.adobe.com/go/learn_aemforms_firstapp_ds_63)。

人間中心のプロセスには、ユーザーがWorkspaceを使用して応答できるタスクが含まれます。 例えば、Workbenchを使用して、銀行管理者がローン申込を承認または拒否するプロセスを作成できます。 次の図に、プロセスFirstAppSolution/PreLoanProcessを示 *します*。

FirstAppSolution/PreLoanProcessプロ *セスは、データ型がXMLであるformData*** という名前の入力パラメーターを受け入れます。 XMLデータは、PreLoanForm.xdpという名前のフォームデザインとマ *ージされます*。 次の図は、ローン申込を承認または拒否するためにユーザーに割り当てられたタスクを表すフォームを示しています。 ユーザーがWorkspaceを使用してアプリケーションを承認または拒否します。 Workspaceユーザーは、次の図に示す「承認」ボタンをクリックして、ローン要求を承認できます。 同様に、ユーザーは「拒否」ボタンをクリックしてローンの要求を拒否できます。

長期間有効なプロセスは非同期で呼び出され、次の要因により同期的に呼び出すことはできません。

* プロセスは、かなりの期間に及ぶ場合があります。
* プロセスは組織の境界をまたぐことができます。
* プロセスを終了するには、外部入力が必要です。 例えば、不在の管理者にフォームが送信される場合を考えてみます。 この場合、マネージャーがフォームを返して入力するまで、プロセスは完了しません。

長時間有効なプロセスが呼び出されると、AEM Formsは、レコードの作成の一部として呼び出し識別子の値を作成します。 このレコードは、長期間有効なプロセスのステータスを追跡し、AEM Formsデータベースに保存されます。 呼び出し識別子の値を使用して、長期間有効なプロセスのステータスを追跡できます。 また、プロセス呼び出し識別子の値を使用して、実行中のプロセスインスタンスの終了など、Process Manager操作を実行できます。

>[!NOTE]
>
>短時間のみ有効なプロセスが呼び出された場合、AEM Formsは呼び出し識別子の値やレコードを作成しません。

申込者 `FirstAppSolution/PreLoanProcess` が申込書を送信すると、このプロセスが呼び出されます。この申込書はXMLデータで表されます。 入力プロセス変数の名前はXML `formData` で、データタイプはXMLです。 この説明の目的で、次のXMLデータがプロセスへの入力として使用されると仮定し `FirstAppSolution/PreLoanProcess` ます。

```as3
 <?xml version="1.0" encoding="UTF-8"?>
 <LoanApp>
 <Name>Sam White</Name>
 <LoanAmount>250000</LoanAmount>
 <PhoneOrEmail>(555)555-5555</PhoneOrEmail>
 <ApprovalStatus>PENDING APPROVAL</ApprovalStatus>
 </LoanApp>
```

プロセスに渡されるXMLデータは、プロセスで使用されるフォーム内のフィールドと一致する必要があります。 そうしないと、データはフォーム内に表示されません。 プロセスを呼び出すすべてのアプリケーシ `FirstAppSolution/PreLoanProcess` ョンは、このXMLデータソースを渡す必要があります。 「人間中心の長期間有効なプロ *セスの呼び出し」で作成されたアプリケーションは* 、ユーザーがWebクライアントに入力した値からXMLデータソースを動的に作成します。

クライアントアプリケーションを使用して、FirstAppSolution/PreLoanProcess *プロセスに必要な* XMLデータを送信できます。 長期間有効なプロセスは、呼び出し識別子の値を戻り値として返します。 次の図に、長期間有効なプロセスを呼び出すクライアントアプリケーションを示します。 クライアントアプリケーションはXMLデータを送信し、呼び出し識別子の値を表すstring値を取得します。

**関連トピック**

[人間中心の長期間有効なプロセスを呼び出す Java Web アプリケーションの作成](invoking-human-centric-long-lived.md#creating-a-java-web-application-that-invokes-a-human-centric-long-lived-process)

[人間中心の長期間有効なプロセスを呼び出すASP.NET webアプリケーションの作成](invoking-human-centric-long-lived.md#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process)

[人間中心の長期間有効なプロセスを呼び出すFlexで構築されたクライアントアプリケーションの作成](invoking-human-centric-long-lived.md#creating-a-client-application-built-with-flex-that-invokes-a-human-centric-long-lived-process)

## 人間中心の長期間有効なプロセスを呼び出す Java Web アプリケーションの作成 {#creating-a-java-web-application-that-invokes-a-human-centric-long-lived-process}

Javaサーブレットを使用してプロセスを呼び出すWebベースのアプリケーションを作成で `FirstAppSolution/PreLoanProcess` きます。 Javaサーブレットからこのプロセスを呼び出すには、Javaサーブレット内で呼び出しAPIを使用します。 (See [Invoking AEM Forms using the Java API](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-aem-forms-using-the-java-api).)

次の図は、名前、電話（または電子メール）および金額の値を投稿するWebベースのクライアントアプリケーションを示しています。 これらの値は、ユーザが「Submit Application」ボタンをクリックするとJavaサーブレットに送信されます。

Javaサーブレットは次のタスクを実行します。

* HTMLページからJavaサーブレットに投稿された値を取得します。
* FirstAppSolution/PreLoanProcessプロセスに渡すXMLデータソースを動的に *作成します* 。 名前、電話（または電子メール）、金額の値は、XMLデータソースで指定します。
* AEM Forms Invocation APIを使 *用して* 、FirstAppSolution/PreLoanProcessプロセスを呼び出します。
* 呼び出し識別子の値をクライアントWebブラウザーに返します。

### 手順の概要 {#summary-of-steps}

プロセスを呼び出すJava webベースのアプリケーションを作成す `FirstAppSolution/PreLoanProcess` るには、次の手順を実行します。

1. [Webプロジェクトを作成します](invoking-human-centric-long-lived.md#create-a-web-project)。
1. [サーブレット用のJavaアプリケーションロジックを作成します](invoking-human-centric-long-lived.md#create-java-application-logic-for-the-servlet)。
1. [Webアプリケーション用のWebページの作成](invoking-human-centric-long-lived.md#create-the-web-page-for-the-web-application)
1. [WebアプリケーションをWARファイルにパッケージ化します](invoking-human-centric-long-lived.md#package-the-web-application-to-a-war-file)。
1. [AEM FormsをホストするJ2EEアプリケーションサーバーにWARファイルをデプロイします](invoking-human-centric-long-lived.md#deploy-the-war-file-to-the-j2ee-application-server-hosting-aem-forms)。
1. [Webアプリケーションをテストします](invoking-human-centric-long-lived.md#test-your-web-application)。

>[!NOTE]
>
>これらの手順の一部は、AEM formsのデプロイ先のJ2EEアプリケーションに依存します。 例えば、WARファイルのデプロイ方法は、使用しているJ2EEアプリケーションサーバーに依存します。 AEM formsがJBoss®にデプロイされていることを前提としています。

### Webプロジェクトの作成 {#create-a-web-project}

Webアプリケーションを作成する最初の手順は、Webプロジェクトを作成することです。 このドキュメントが基にしているJava IDEはEclipse 3.3です。Eclipse IDEを使用して、Webプロジェクトを作成し、必要なJARファイルをプロジェクトに追加します。 プロジェクトに *index.htmlというHTMLページと* 、Javaサーブレットを追加します。

Webプロジェクトに含めるJARファイルを次に示します。

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* J2EE.jar

For the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

>[!NOTE]
>
>J2EE.jarファイルは、Javaサーブレットで使用するデータ型を定義します。 このJARファイルは、AEM FormsがデプロイされているJ2EEアプリケーションサーバーから取得できます。

**Webプロジェクトの作成**

1. Eclipseを起動し、 **File** / **New Projectをクリックします**。
1. 新規プロジ **ェクトダイアログ** で、 **Web** /ダイナミッ **クWebプロジェクトを選択します**。
1. プロジ `InvokePreLoanProcess` ェクトの名前を入力し、「完了」をクリック **します**。

**必要なJARファイルをプロジェクトに追加します**

1. 「プロジェクト・エクスプローラ」ウィンドウで、プロジェクトを右クリックし `InvokePreLoanProcess` 、「プロパティ」を **選択しま**&#x200B;す。
1. 「 **Javaビルドパス」をクリックし** 、「ライブラリ」タブをク **リックします** 。
1. 「 **Add External JARs** 」ボタンをクリックし、含めるJARファイルを参照します。

**プロジェクトへのJavaサーブレットの追加**

1. 「プロジェクト・エクスプローラ」ウィンドウで、プロジェクトを右クリ `InvokePreLoanProcess` ックし、「新規」>「その他」 **を選択** します ****。
1. 「 **Web** 」フォルダを展開し、「 **Servlet**」を選択して「 **Next」をクリックします**。
1. 「サーブレットを作成」ダイアログで、サーブ `SubmitXML` レットの名前を入力し、「完了」をクリック **します**。

**プロジェクトへのHTMLページの追加**

1. 「プロジェクト・エクスプローラ」ウィンドウで、プロジェクトを右クリ `InvokePreLoanProcess` ックし、「新規」>「その他」 **を選択** します ****。
1. 「 **Web** 」フォルダを展開し、「 **HTML**」を選択して「 **Next**」をクリックします。
1. 新規HTMLダイアログボックスで、ファイル名 `index.html` を入力し、「完了」をクリック **します**。

>[!NOTE]
>
>SubmitXML javaサーブレットを呼び出すHTMLコンテンツの作成について詳しくは、Webアプリケ [ーションのWebページの作成を参照してください](invoking-human-centric-long-lived.md#create-the-web-page-for-the-web-application)。

### サーブレット用のJavaアプリケーションロジックの作成 {#create-java-application-logic-for-the-servlet}

Javaサーブレット内からプロセスを呼び出すJava `FirstAppSolution/PreLoanProcess` アプリケーションロジックを作成します。 次のコードは、 `SubmitXML` Javaサーブレットの構文を示しています。

```as3
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

通常、クライアントコードはJavaサーブレットのメソッドまたはメソッド内に配置 `doGet` しま `doPost` せん。 より良いプログラミング方法は、このコードを別のクラスに配置することです。 次に、メソッド（またはメソッド）内からク `doPost` ラスをインスタ `doGet` ンス化し、適切なメソッドを呼び出します。 ただし、コードを簡潔にするために、コード例は最小限に抑えられ、メソッドに配置さ `doPost` れます。

呼び出しAPIを使用 `FirstAppSolution/PreLoanProcess` してプロセスを呼び出すには、次のタスクを実行します。

1. Javaプロジェクトのクラスパスに、adobe-livecycle-client.jarなどのクライアントJARファイルを含めます。 これらのファイルの場所については、[AEM Forms Java ライブラリファイルを含める](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)を参照してください。
1. HTMLページから送信された名前、電話番号、金額の値を取得します。 これらの値を使用して、プロセスに送信するXMLデータソースを動的に作成し `FirstAppSolution/PreLoanProcess` ます。 XMLデータソー `org.w3c.dom` スの作成にはクラスを使用できます（次のコードの例に、このアプリケーションロジックを示します）。
1. 接続プロパティを含む `ServiceClientFactory` オブジェクトを作成します。（[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照。）
1. コンストラクタを使用して `ServiceClient` オブジェクトを渡すことによって、`ServiceClientFactory` オブジェクトを作成します。`ServiceClient` オブジェクトを使用すると、サービス操作を呼び出すことができます。呼び出し要求の検索、ディスパッチ、ルーティングなどのタスクを処理します。
1. コンストラクタを使用して `java.util.HashMap` オブジェクトを作成します。
1. 各入力パラメーターに対して `java.util.HashMap` オブジェクトの `put` メソッドを呼び出して、長期間有効なプロセスに渡します。プロセスの入力パラメーターの名前を必ず指定してください。 プロセスに `FirstAppSolution/PreLoanProcess` は（名前付きの）型の入力パラメーターが1 `XML` つ必要 `formData`なので、メソッドを呼び出す必要があるのは1 `put` 回だけです。

   ```as3
    //Get the XML to pass to the FirstAppSolution/PreLoanProcess process
    org.w3c.dom.Document inXML = GetDataSource(name,phone,amount);
    
    //Create a Map object to store the parameter value
    Map params = new HashMap();
    params.put("formData", inXML);
   ```

1. Create an `InvocationRequest` object by invoking the `ServiceClientFactory` object’s `createInvocationRequest` method and passing the following values:

   * 長期間有効なプロセスを指定する文字列値。プロセスを呼び出すに `FirstAppSolution/PreLoanProcess` は、を指定しま `FirstAppSolution/PreLoanProcess`す。
   * プロセス操作名を表す文字列値。長期間有効なプロセス操作の名前はです `invoke`。
   * サービス操作に必要なパラメーター値を含む `java.util.HashMap` オブジェクト。
   * A Boolean value that specifies `false`, which creates an asynchronous request (this value is applicable to invoke a long-lived process).
   >[!NOTE]
   >
   >*短時間のみ有効なプロセスは、createInvocationRequestメソッドの4番目のパラメーターとして値trueを渡すことで呼び出すことができます。 値trueを渡すと、同期リクエストが作成されます。*

1. Send the invocation request to AEM Forms by invoking the `ServiceClient` object’s `invoke` method and passing the `InvocationRequest` object. The `invoke` method returns an `InvocationReponse` object.
1. 長期間有効なプロセスは、呼び出しID値を表すstring値を返します。 オブジェクトのメソッドを呼び出し `InvocationReponse` て、この値を取得 `getInvocationId` します。

   ```as3
    //Send the invocation request to the long-lived process and
    //get back an invocation response object
    InvocationResponse lcResponse = myServiceClient.invoke(lcRequest);
    String invocationId = lcResponse.getInvocationId();
   ```

1. 呼び出しID値をクライアントのWebブラウザーに書き込みます。 インスタンスを使用し `java.io.PrintWriter` て、この値をクライアントWebブラウザーに書き込むことができます。

### Quick Start: Invoking a long-lived process using the Invocation API {#quick-start-invoking-a-long-lived-process-using-the-invocation-api}

次のJavaコードの例は、プロセスを呼び出すJavaサーブレットを表して `FirstAppSolution/PreLoanProcess` います。

```as3
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

*index.html webページは* 、プロセスを呼び出すJavaサーブレットへのエントリポイントを提供 `FirstAppSolution/PreLoanProcess` します。 このWebページは、HTMLフォームと送信ボタンを含む基本HTMLフォームです。 ユーザーが送信ボタンをクリックすると、フォームデータが `SubmitXML` Javaサーブレットにポストされます。

Javaサーブレットは、次のJavaコードを使用して、HTMLページから投稿されたデータを取得します。

```as3
 //Get the values that are passed from the Loan HTML page
 String name = request.getParameter("name");
 String phone = request.getParameter("phone");
 String amount = request.getParameter("amount");
```

次のHTMLコードは、開発環境のセットアップ中に作成されたindex.htmlファイルを表しています。 (Webプロジ [ェクトの作成を参照](invoking-human-centric-long-lived.md#create-a-web-project))。

```as3
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

プロセスを呼び出すJavaサーブレットをデプロイす `FirstAppSolution/PreLoanProcess` るには、WebアプリケーションをWARファイルにパッケージ化します。 コンポーネントのビジネスロジックが依存する外部JARファイル（adobe-livecycle-client.jarやadobe-usermanager-client.jarなど）もWARファイルに含めてください。

次の図は、WARファイルにパッケージ化されたEclipseプロジェクトのコンテンツを示しています。

>[!NOTE]
>
>上の図では、JPGファイルを任意のJPG画像ファイルに置き換えることができます。

**WebアプリケーションのWARファイルへのパッケージ化：**

1. 「プロジェ **クトエクスプローラ** 」ウィンドウで、プロジェクトを右クリ `InvokePreLoanProcess` ックし、「エクスポー **ト** 」>「 **WARファイル」を選択します**。
1. 「 **Web module** 」テキストボッ `InvokePreLoanProcess` クスに、Javaプロジェクトの名前を入力します。
1. 「 **Destination** 」テキストボックスにフ `PreLoanProcess.war`**ァ&#x200B;**イル名を入力し、WARファイルの場所を指定して、「Finish」をクリックします。

### AEM FormsをホストするJ2EEアプリケーションサーバーにWARファイルをデプロイします {#deploy-the-war-file-to-the-j2ee-application-server-hosting-aem-forms}

AEM FormsがデプロイされているJ2EEアプリケーションサーバーにWARファイルをデプロイします。 WARファイルをJ2EEアプリケーションサーバーにデプロイするには、WARファイルをエクスポートパスからにコピーしま `[AEM Forms Install]\Adobe\Adobe Experience Manager Forms\jboss\server\lc_turnkey\deploy`す。

>[!NOTE]
>
>aem formsがJBossにデプロイされていない場合は、AEM formsをホストするJ2EEアプリケーションサーバーに準拠してWARファイルをデプロイする必要があります。

### Webアプリケーションのテスト {#test-your-web-application}

Webアプリケーションをデプロイした後、Webブラウザーを使用してテストできます。 AEM formsをホストするコンピューターと同じコンピューターを使用している場合は、次のURLを指定できます。

* http://localhost:8080/PreLoanProcess/index.html

   HTMLフォームフィールドに値を入力し、「Submit Application」ボタンをクリックします。 問題が発生した場合は、J2EEアプリケーションサーバーのログファイルを参照してください。

   ***注意&#x200B;**:Javaアプリケーションがプロセスを呼び出したことを確認するには、Workspaceを起動し、ローンを受け入れます。*

## Creating an ASP.NET web application that invokes a human-centric long-lived process {#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process}

プロセスを呼び出すASP.NETアプリケーションを作成でき `FirstAppSolution/PreLoanProcess` ます。 ASP.NETアプリケーションからこのプロセスを呼び出すには、Webサービスを使用します。 (See [Invoking AEM Forms using Web Services](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)

次の図は、エンドユーザーからデータを取得するASP.NETクライアントアプリケーションを示しています。 データはXMLデータソースに配置され、ユーザーが「Submit Application」ボタンをク `FirstAppSolution/PreLoanProcess` リックするとプロセスに送信されます。

プロセスの呼び出し後に、呼び出し識別子の値が表示されます。 呼び出し識別子の値は、長期間有効なプロセスのステータスを追跡するレコードの一部として作成されます。

ASP.NETアプリケーションは、次のタスクを実行します。

* ユーザーがWebページに入力した値を取得します。
* * firstAppSolution/PreLoanProcess *processに渡されるXMLデータソースを動的に作成します。 この3つの値は、XMLデータソースで指定されます。
* Webサービスを使用して、* FirstAppSolution/PreLoanProcess *processを呼び出します。
* 呼び出し識別子の値と長期間有効な操作のステータスをクライアントWebブラウザーに返します。

### 手順の概要 {#summary_of_steps-1}

FirstAppSolution/PreLoanProcessプロセスを呼び出すことができるASP.NETアプリケーションを作成するには、次の手順を実行します。

1. [ASP.NET webアプリケーションを作成します](invoking-human-centric-long-lived.md#create-an-asp-net-web-application)。
1. [FirstAppSolution/PreLoanProcessを呼び出すASPページを作成します](invoking-human-centric-long-lived.md#create-an-asp-page-that-invokes-firstappsolution-preloanprocess)。
1. [ASP.NETアプリケーションを実行します](invoking-human-centric-long-lived.md#run-the-asp-net-application)。

### ASP.NET webアプリケーションの作成 {#create-an-asp-net-web-application}

Microsoft .NET C# ASP.NET webアプリケーションを作成します。 次の図は、InvokePreLoanProcessというASP.NETプロジェクトの内容を示して *います*。

「Service References」の下に2つの項目が表示されます。 最初のアイテムは* jobManager*という名前です。 この参照により、ASP.NETアプリケーションからJob Managerサービスを呼び出すことができます。 このサービスは、長期間有効なプロセスのステータスに関する情報を返します。 例えば、プロセスが現在実行中の場合、このサービスはプロセスが現在実行中であることを示す数値を返します。 2つ目の参照はPreLoanProcessという名前&#x200B;*です*。 このサービス参照は、* firstAppSolution/PreLoanProcess *processへの参照を表します。 サービス参照を作成すると、AEM Formsサービスに関連付けられたデータ型を.NETプロジェクト内で使用できるようになります。

**ASP.NETプロジェクトを作成します。**

1. Microsoft Visual Studio 2008を起動します。
1. [ファイル **]メニューの[新規作** 成 **]、[** Webサイト]の順に選択します ****。
1. [テンプ **レート** ]ボックスの一覧で[ **ASP.NET Webサイト**]を選択します。
1. 「場所」ボ **ックスで** 、プロジェクトの場所を選択します。 プロジェクトに「InvokePreLoanProcess」という名 *前を付けます*。
1. 「言語」ボ **ックスで** 、「Visual C#」を選択します。
1. 「OK」をクリックします。

**サービス参照の追加：**

1. プロジェクトメニューで、「サービス参照 **を追加」を選択します**。
1. 「 **Address** 」ダイアログで、Job ManagerサービスのWSDLを指定します。

   ```as3
    https://hiro-xp:8080/soap/services/JobManager?WSDL&lc_version=9.0.1
   ```

1. 「名前空間」フィールドに、と入力しま `JobManager`す。
1. Click **Go** and then click **OK**.
1. 「プロジェク **ト** 」メニューで「サービス **参照の追加**」を選択します。
1. 「アドレス **」ダイアログ** で、FirstAppSolution/PreLoanProcessプロセスのWSDLを指定します。

   ```as3
    https://hiro-xp:8080/soap/services/FirstAppSolution/PreLoanProcess?WSDL&lc_version=9.0.1
   ```

1. 「名前空間」フィールドに、と入力しま `PreLoanProcess`す。
1. Click **Go** and then click **OK**.

>[!NOTE]
>
>AEM formsをホ `hiro-xp` ストするJ2EEアプリケーションサーバーのIPアドレスに置き換えます。 このオ `lc_version` プションを使用すると、MTOMなどのAEM Forms機能を使用できるようになります。 このオプションを指 `lc_version`定しないと、MTOMを使用してAEM Formsを呼び出すことはできません。 (「MTOMを使用 [したAEM formsの呼び出し](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)」を参照)。

### FirstAppSolution/PreLoanProcessを呼び出すASPページを作成します {#create-an-asp-page-that-invokes-firstappsolution-preloanprocess}

ASP.NETプロジェクト内で、HTMLページをローンの申込者に表示するWebフォーム（ASPXファイル）を追加します。 Webフォームは、から派生したクラスに基づいています `System.Web.UI.Page`。 を呼び出すC#アプリケーションロジック `FirstAppSolution/PreLoanProcess` は、メソッド内にあ `Button1_Click` ります（このボタンは「Submit Application」ボタンを表します）。

次の図に、ASP.NETアプリケーションを示します

次の表に、このASP.NETアプリケーションに含まれるコントロールを示します。

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
   <td><p>呼び出し識別子値の値を指定するLabelコントロールです。</p></td>
  </tr>
  <tr>
   <td><p>LabelStatus</p></td>
   <td><p>ジョブの状態の値を指定するLabelコントロールです。 この値は、Job Managerサービスを呼び出して取得されます。 </p></td>
  </tr>
 </tbody>
</table>

ASP.NETアプリケーションの一部であるアプリケーションロジックは、プロセスに渡すXMLデータソースを動的に作成する必要があ `FirstAppSolution/PreLoanProcess` ります。 申込者がHTMLページに入力した値は、XMLデータソース内で指定する必要があります。 これらのデータ値は、フォームがWorkspaceで表示されるときにフォームにマージされます。 名前空間にあるクラスは、XML `System.Xml` データソースの作成に使用されます。

ASP.NETアプリケーションからXMLデータを必要とするプロセスを呼び出す場合、XMLデータ型を使用できます。 つまり、インスタンスをプロセスに渡す `System.Xml.XmlDocument` ことはできません。 プロセスに渡すこのXMLインスタンスの完全修飾名はです `InvokePreLoanProcess.PreLoanProcess.XML`。 インスタンスを `System.Xml.XmlDocument` に変換しま `InvokePreLoanProcess.PreLoanProcess.XML`す。 このタスクは、次のコードを使用して実行できます。

```as3
 //Create the XML to pass to the FirstAppSolution/PreLoanProcess process
 XmlDocument myXML = CreateXML(userName, phone, amount);
 
 //Convert the XML to a InvokePreLoanProcess.PreLoanProcess.XML instance
 StringWriter sw = new StringWriter();
 XmlTextWriter xw = new XmlTextWriter(sw);
 myXML.WriteTo(xw);
 
 InvokePreLoanProcess.PreLoanProcess.XML inXML = new XML();
 inXML.document = sw.ToString();
```

プロセスを呼び出すASPページを作成す `FirstAppSolution/PreLoanProcess` るには、メソッドで次のタスクを実行し `Button1_Click` ます。

1. Create a `FirstAppSolution_PreLoanProcessClient` object by using its default constructor.
1. Create a `FirstAppSolution_PreLoanProcessClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. WSDLをAEM Formsサービスに渡し、エンコードの種類を指定するstring値を渡します。

   ```as3
    https://hiro-xp:8080/soap/services/FirstAppSolution/PreLoanProcess?blob=mtom
   ```

   属性を使用する必要はありま `lc_version` せん。 この属性は、サービス参照を作成する際に使用されます。 ただし、必ず、を指定してくださ `?blob=mtom`い。

   >[!NOTE]
   >
   >「 `hiro-xp`*」は、AEM formsをホストするJ2EEアプリケーションサーバーのIPアドレスに置き換えます。*

1. データメン `System.ServiceModel.BasicHttpBinding` バーの値を取得してオブジェクトを作 `FirstAppSolution_PreLoanProcessClient.Endpoint.Binding` 成します。 戻り値を `BasicHttpBinding` にキャストします。
1. オブジェクト `System.ServiceModel.BasicHttpBinding` のデータメンバ `MessageEncoding` ーをに設定しま `WSMessageEncoding.Mtom`す。 この値により、MTOMが使用されます。
1. 次のタスクを実行して、基本HTTP認証を有効にします。

   * AEM formsユーザー名をデータメンバーに割り当てま `FirstAppSolution_PreLoanProcessClient.ClientCredentials.UserName.UserName`す。
   * 対応するパスワード値をデータメンバーに割り当てま `FirstAppSolution_PreLoanProcessClient.ClientCredentials.UserName.Password`す。
   * 定数値をデータメン `HttpClientCredentialType.Basic` バーに割り当てま `BasicHttpBindingSecurity.Transport.ClientCredentialType`す。
   * 定数値をデータメン `BasicHttpSecurityMode.TransportCredentialOnly` バーに割り当てま `BasicHttpBindingSecurity.Security.Mode`す。
   次のコード例に、これらのタスクを示します。

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

1. ユーザーがWebページに入力した名前、電話番号、金額の値を取得します。 これらの値を使用して、プロセスに送信するXMLデータソースを動的に作成し `FirstAppSolution/PreLoanProcess` ます。 プロセス `System.Xml.XmlDocument` に渡すXMLデータソースを表すXMLを作成します（次のコードの例では、このアプリケーションロジックを示します）。
1. インスタンス `System.Xml.XmlDocument` をに変換しま `InvokePreLoanProcess.PreLoanProcess.XML` す（このアプリケーションロジックは次のコード例に示します）。
1. オブジェクトの `FirstAppSolution/PreLoanProcess` メソッドを呼び出して、 `FirstAppSolution_PreLoanProcessClient` プロセスを呼び出 `invoke_Async` します。 このメソッドは、長期間有効なプロセスの呼び出し識別子の値を表すstring値を返します。
1. isコンストラクタ `JobManagerClient` ーを使用してを作成します。 （Job Managerサービスへのサービス参照が設定されていることを確認します）。
1. 手順1 ～ 5を繰り返します。 手順2の次のURLを指定します。 `https://hiro-xp:8080/soap/services/JobManager?blob=mtom`.
1. コンストラクタを使用して `JobId` オブジェクトを作成します。
1. オブジェクト `JobId` のデータメ `id` ンバーに、オブジェクトのメソッドの戻り `FirstAppSolution_PreLoanProcessClient` 値を設定 `invoke_Async` します。
1. オブジェクト `value` のデータメンバ `JobId` ーにtrueを割り `persistent` 当てます。
1. オブジェクトの `JobStatus` メソッドを呼び出し、オ `JobManagerService` ブジェクトを渡すこ `getStatus` とで、オブジェクトを作成 `JobId` します。
1. オブジェクトのデータメンバの値を取得して、ステ `JobStatus` ータス値を取 `statusCode` 得します。
1. 呼び出し識別子の値をフィールドに割り当 `LabelJobID.Text` てます。
1. フィールドにステータス値を割り当 `LabelStatus.Text` てます。

### クイックスタート：WebサービスAPIを使用した長期間有効なプロセスの呼び出し {#quick-start-invoking-a-long-lived-process-using-the-web-service-api}

次のC#コードの例は、プロセスを呼び出 `FirstAppSolution/PreLoanProcess`します。

```as3
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
>getJobDescriptionユーザー定義メソッド内の値は、Job Managerサービスによって返される値に対応しています。

### ASP.NETアプリケーションを実行する {#run-the-asp-net-application}

ASP.NETアプリケーションをコンパイルして展開した後、Webブラウザーを使用して実行できます。 ASP.NETプロジェクトの名前がInvokePreLoanProcessの場合 *は*、Webブラウザー内で次のURLを指定します。

*http://localhost:1629/InvokePreLoanProcess/*Default.aspx

localhostはASP.NETプロジェクトをホストするWebサーバーの名前、1629はポート番号です。 ASP.NETアプリケーションをコンパイルして構築すると、Microsoft Visual studioによって自動的に展開されます。

>[!NOTE]
>
>ASP.NETアプリケーションがプロセスを呼び出したことを確認するには、Workspaceを起動し、ローンを受け入れます。

## 人間中心の長期間有効なプロセスを呼び出すFlexで構築されたクライアントアプリケーションの作成 {#creating-a-client-application-built-with-flex-that-invokes-a-human-centric-long-lived-process}

Flexで構築されたクライアントアプリケーションを作成して、FirstAppSolution/PreLoanProcess *プロセスを呼び出すことができます* 。 このアプリケーションは、Remotingを使用して *FirstAppSolution/PreLoanProcess* プロセスを呼び出します。 (『AEM Forms Remoting [を使用したAEM Formsの呼び出し(AEM Formsでは非推奨](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting))』を参照)。

次の図に、Flexで構築された、エンドユーザーからのデータ収集用のクライアントアプリケーションを示します。 データはXMLデータソースに配置され、プロセスに送信されます。

プロセスの呼び出し後に、呼び出し識別子の値が表示されます。 呼び出し識別子の値は、長期間有効なプロセスのステータスを追跡するレコードの一部として作成されます。

Flexで構築されたクライアントアプリケーションは、次のタスクを実行します。

* ユーザーがWebページに入力した値を取得します。
* FirstAppSolution/PreLoanProcessプロセスに渡されるXMLデータソースを動的に作 *成します* 。 この3つの値は、XMLデータソースで指定されます。
* Remotingを使用し *てFirstAppSolution/PreLoanProcess* プロセスを呼び出します。
* 長期間有効なプロセスの呼び出し識別子の値を返します。

### 手順の概要 {#summary_of_steps-2}

FirstAppSolution/PreLoanProcessプロセスを呼び出すことのできるFlexで構築されたクライアントアプリケーションを作成するには、次の手順を実行します。

1. 新しいFlexプロジェクトを開始します。
1. プロジェクトのクラスパスにadobe-remoting-provider.swcファイルを含めます。 (「AEM Forms flexラ [イブラリファイルのインクルード](/help/forms/developing/invoking-aem-forms-using-remoting.md#including-the-aem-forms-flex-library-file)」を参照)。
1. ActionScriptまたはMXMLを `mx:RemoteObject` 使用してインスタンスを作成します。 (mx:RemoteObjectイ [ンスタンスの作成を参照](/help/forms/developing/invoking-aem-forms-using-remoting.md))。
1. AEM Formsと通信す `ChannelSet` るインスタンスを設定し、そのインスタンスに関連付け `mx:RemoteObject` ます。 (「AEM formsへ [のチャネルの作成](/help/forms/developing/invoking-aem-forms-using-remoting.md)」を参照)。
1. ChannelSetのメソッドまたはサ `login` ービスのメソッドを呼び出して、ユ `setCredentials` ーザー識別子の値とパスワードを指定します。 (シングル [サインオンの使用を参照](/help/forms/developing/invoking-aem-forms-using-remoting.md#using-single-sign-on))。
1. XMLインスタンスを作成して、プロセスに渡すXML `FirstAppSolution/PreLoanProcess` データソースを作成します。 （このアプリケーションロジックは、次のコード例に示します）。
1. コンストラクターを使用して、Object型のオブジェクトを作成します。 次のコードに示すように、プロセスの入力パラメーターの名前を指定して、XMLをオブジェクトに割り当てます。

   ```as3
    //Get the XML data to pass to the AEM Forms process
    var xml:XML = createXML();
    var params:Object = new Object();
    params["formData"]=xml;
   ```

1. インスタンス `FirstAppSolution/PreLoanProcess` のメソッドを呼び出して、 `mx:RemoteObject` プロセスを呼び出 `invoke_Async` します。 入力パラメ `Object` ーターを含むを渡します。 (入力値 [の受け渡しを参照](/help/forms/developing/invoking-aem-forms-using-remoting.md))。
1. 次のコードに示すように、長期間有効なプロセスから返される呼び出しID値を取得します。

   ```as3
    // Handles async call that invokes the long-lived process
    private function resultHandler(event:ResultEvent):void
    {
    ji = event.result as JobId;
    jobStatusDisplay.text = "Job Status ID: " + ji.jobId as String;
    }
   ```

### Remotingを使用した長期間有効なプロセスの呼び出し {#invoking-a-long-lived-process-using-remoting}

次のFlexコードの例は、プロセスを呼び出 `FirstAppSolution/PreLoanProcess` します。

```as3
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

