---
title: 呼び出しAPIクイック開始
seo-title: 呼び出しAPIクイック開始
description: 'null'
seo-description: 'null'
uuid: acf67177-98a4-4c99-95a5-3086907d7c2c
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: dcf83c9f-b818-44a2-9079-80a4fc357c4f
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1231'
ht-degree: 6%

---


# 呼び出しAPIクイック開始 {#invocation-api-quick-starts}

次のクイック開始は、AEM Formsサービスをプログラムで呼び出すときに使用できます。

<table>
 <thead>
  <tr>
   <th><p>説明</p></th>
   <th><p>Remoting API</p></th>
   <th><p>Java API</p></th>
   <th><p>WebサービスAPI</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p><a href="/help/forms/developing/invoking-human-centric-long-lived.md#invoking_human_centric_long_lived_processes">人間中心の長期間有効なプロセスの呼び出し</a></p></td>
   <td><p><a href="/help/forms/developing/invoking-human-centric-long-lived.md#invoking-a-long-lived-process-using-remoting">AEM Formsのリモート処理（AEM Formsでは廃止されています）を使用した長期間有効なプロセスの呼び出し</a></p></td>
   <td><p><a href="/help/forms/developing/invoking-human-centric-long-lived.md#quick_start_invoking_a_long_lived_process_using_the_invocation_api">クイック開始: 呼び出しAPIを使用した長期間有効なプロセスの呼び出し</a></p></td>
   <td><p><a href="/help/forms/developing/invoking-human-centric-long-lived.md#quick_start_invoking_a_long_lived_process_using_the_web_service_api">クイック開始: WebサービスAPIを使用した長期間有効なプロセスの呼び出し</a></p></td>
  </tr>
  <tr>
   <td><p><a href="/help/forms/developing/invoking-aem-forms-using-java.md#invoking_a_short_lived_process_using_the_invocation_api">呼び出し API を使用した短時間のみ有効なプロセスの呼び出し</a></p></td>
   <td><p>該当なし</p></td>
   <td><p><a href="invocation-api-quick-starts.md#quick_start_invoking_a_short_lived_process_using_the_invocation_api">クイックスタート：呼び出し API を使用した短時間のみ有効なプロセスの呼び出し</a></p></td>
   <td><p>該当なし</p></td>
  </tr>
  <tr>
   <td><p><a href="/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding">Base64エンコーディングを使用したAEM Formsの呼び出し</a> （Java Webサービスプロキシ）</p></td>
   <td><p>該当なし</p></td>
   <td><p>該当なし</p></td>
   <td><p><a href="invocation-api-quick-starts.md#quick_start_invoking_a_service_using_java_proxy_files_and_base64_encoding">クイック開始: JavaプロキシファイルとBase64エンコーディングを使用したサービスの呼び出し</a></p></td>
  </tr>
  <tr>
   <td><p><a href="/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding">Base64エンコーディング</a> （.NET Webサービスプロキシ）を使用してAEM Formsを呼び出す</p></td>
   <td><p>該当なし</p></td>
   <td><p>該当なし</p></td>
   <td><p><a href="invocation-api-quick-starts.md#quick_start_invoking_a_service_using_base64_in_a_microsoft_net_project">クイック開始: Microsoft .NETプロジェクトでbase64を使用してサービスを呼び出す</a></p></td>
  </tr>
  <tr>
   <td><p><a href="/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom">MTOM</a> （.NET Webサービスの例）を使用してAEM Formsを呼び出す</p></td>
   <td><p>該当なし</p></td>
   <td><p>該当なし</p></td>
   <td><p><a href="invocation-api-quick-starts.md#quick_start_invoking_a_service_using_mtom_in_a_net_project">クイック開始: .NETプロジェクトでMTOMを使用してサービスを呼び出す</a></p></td>
  </tr>
  <tr>
   <td><p><a href="/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref">SwaRef</a> （Java Webサービスの例）を使用したAEM Formsの呼び出し</p></td>
   <td><p>該当なし</p></td>
   <td><p>該当なし</p></td>
   <td><p><a href="invocation-api-quick-starts.md#quick_start_invoking_a_service_using_swaref_in_a_java_project">クイック開始: JavaプロジェクトでのSwaRefを使用したサービスの呼び出し</a></p></td>
  </tr>
  <tr>
   <td><p><a href="/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-blob-data-over-http">HTTP</a> （Java Webサービスの例）を使用したBLOBデータを使用したAEM Formsの呼び出し</p></td>
   <td><p>該当なし</p></td>
   <td><p>該当なし</p></td>
   <td><p><a href="invocation-api-quick-starts.md#quick_start_invoking_a_service_using_blob_data_over_http_in_a_net_project">クイック開始: .NETプロジェクトでHTTP経由のBLOBデータを使用してサービスを呼び出す</a></p></td>
  </tr>
  <tr>
   <td><p><a href="/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-blob-data-over-http">HTTP</a> （.NET Webサービスの例）を介したBLOBデータを使用したAEM Formsの呼び出し</p></td>
   <td><p>該当なし</p></td>
   <td><p>該当なし</p></td>
   <td><p><a href="invocation-api-quick-starts.md#quick_start_invoking_a_service_using_blob_data_over_http_in_a_java_project">クイック開始: JavaプロジェクトでHTTP経由のBLOBデータを使用してサービスを呼び出す</a></p></td>
  </tr>
  <tr>
   <td><p><a href="/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-dime">DIMEを使用したAEM Formsの呼び出し</a> （Java Webサービスの例）</p></td>
   <td><p>該当なし</p></td>
   <td><p>該当なし</p></td>
   <td><p><a href="invocation-api-quick-starts.md#quick_start_invoking_a_service_using_dime_in_a_java_project">クイック開始: JavaプロジェクトでのDIMEを使用したサービスの呼び出し</a></p></td>
  </tr>
  <tr>
   <td><p><a href="/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting">AEM Formsのリモート処理（AEM Formsでは廃止）を使用したAEM Formsの呼び出し</a></p></td>
   <td><p><a href="invocation-api-quick-starts.md#quick-start-invoking-a-short-lived-process-by-passing-an-unsecure-document-using-deprecated-for-aem-forms-aem-forms-remoting">クイック開始: AEM Formsのリモート処理（AEM Formsでは廃止されています）を使用して安全でないドキュメントを渡すことによる短時間のみ有効なプロセスの呼び出し</a></p></td>
   <td><p>該当なし</p></td>
   <td><p>該当なし</p></td>
  </tr>
  <tr>
   <td><p><a href="/help/forms/developing/invoking-aem-forms-using-remoting.md#passing_secure_documents_to_invoke_processes_using_remoting">Remotingを使用してプロセスを呼び出すための安全なドキュメントーの渡し</a></p></td>
   <td><p><a href="/help/forms/developing/invoking-aem-forms-using-remoting.md#quick-start-invoking-a-short-lived-process-by-passing-a-secure-document-using-remoting">クイック開始: AEM Formsのリモート処理（AEM Formsでは廃止されています）を使用して安全なドキュメントを渡すことによる短時間のみ有効なプロセスの呼び出し</a></p></td>
   <td><p>該当なし</p></td>
   <td><p>該当なし</p></td>
  </tr>
  <tr>
   <td><p><a href="/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking_custom_component_services_using_remoting">Remotingを使用したカスタムコンポーネントサービスの呼び出し</a></p></td>
   <td><p><a href="/help/forms/developing/invoking-aem-forms-using-remoting.md#quick-start-invoking-the-customer-custom-service-using-remoting">クイック開始: AEM Formsのリモート処理（AEM Formsでは廃止されています）を使用したCustomer Custom Serviceの呼び出し</a></p></td>
   <td><p>該当なし</p></td>
   <td><p>該当なし</p></td>
  </tr>
 </tbody>
</table>

AEM Forms操作は、厳密に型指定されたAPIをAEM Formsを使用して実行できます。接続モードはSOAPに設定する必要があります。

>[!NOTE]
>
>「AEM Formsによるプログラミング」にあるクイック開始は、JBoss Application ServerおよびMicrosoft WindowsオペレーティングシステムにデプロイされるFormsサーバーに基づいています。 ただし、UNIXなど別のオペレーティングシステムを使用している場合は、Windows固有のパスを、該当するオペレーティングシステムでサポートされているパスに置き換えます。 同様に、別のJ2EEアプリケーションサーバーを使用する場合は、有効な接続プロパティを指定していることを確認してください。 See [Setting connection properties](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

## クイックスタート：呼び出し API を使用した短時間のみ有効なプロセスの呼び出し {#quick-start-invoking-a-short-lived-process-using-the-invocation-api}

以下のJavaコードの例は、という名前の短時間のみ有効なプロセスを呼び出し `MyApplication/EncryptDocument`ます。 このプロセスは同期的に呼び出されます。 このプロセスの入力パラメーターに名前が付けられ `inDoc`ます。 このプロセスの出力パラメーターには名前が付けられ `outDoc`ます。 パスワードで暗号化されたPDFドキュメントは、というPDFファイルとして保存され `EncryptLoan.pdf`ます。 (See [Invoking a short-lived process using the Invocation API](/help/forms/developing/invoking-aem-forms-using-java.md#invoking-a-short-lived-process-using-the-invocation-api).)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-convertpdf-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the forms server is not deployed
     * on JBoss)
     * 6. jacorb.jar (use a different JAR file if the forms server is not deployed on JBoss)
     * 7. jnp-client.jar (use a different JAR file if the forms server is not deployed on JBoss)
     *
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * The adobe-utilities.jar file is located in the following path:
     * <install directory>/sdk/client-libs/jboss
     *
     * The jboss-client.jar file is located in the following path:
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
     * path
     * <install directory>/sdk/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms Java library files" in Programming
     * with AEM Forms
     */
 import java.io.File;
 import java.io.FileInputStream;
 import java.io.InputStream;
 import java.util.HashMap;
 import java.util.Map;
 import java.util.Properties;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.InvocationRequest;
 import com.adobe.idp.dsc.InvocationResponse;
 import com.adobe.idp.dsc.clientsdk.ServiceClient;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 
     public class InvokeDocumentEncryptLooselyTypedAPI {
 
         public static void main(String[] args)
         {
         try
         {
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             // Create a ServiceClientFactory instance
             ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a ServiceClient object
             ServiceClient myServiceClient = factory.getServiceClient();
 
             //Create a Map object to store the parameter value
             Map params = new HashMap();
 
             InputStream inFile = new FileInputStream("C:\\Adobe\Loan.pdf");
             Document inDoc = new Document(inFile);
 
             //Populate the Map object with a parameter value
             //required to invoke the MyApplication/EncryptDocument short-lived process
             //inDoc refers to the name of the input parameter for the process
             params.put("inDoc", inDoc);
 
             //Create an InvocationRequest object
             InvocationRequest request =  factory.createInvocationRequest(
                     "MyApplication/EncryptDocument",        //Specify the short-lived process name
                     "invoke",           //Specify the operation name
                     params,               //Specify input values
                     true);               //Create a synchronous request
 
             //Send the invocation request to the short-lived process and
             //get back an invocation response -- outDoc refers to the output parameter for the
             //MyApplication/EncryptDocument process
             InvocationResponse response = myServiceClient.invoke(request);
             Document encryptDoc = (Document) response.getOutputParameter("outDoc");
 
             //Save the encrypted PDF document returned by the process
             //Save the password-encrypted PDF document
             File outFile = new File("C:\\Adobe\EncryptLoan.pdf");
             encryptDoc.copyToFile (outFile);
             }catch (Exception e) {
                 e.printStackTrace();
             }
         }
 }
```

## クイック開始: Microsoft .NETプロジェクトでbase64を使用してサービスを呼び出す {#quick-start-invoking-a-service-using-base64-in-a-microsoft-net-project}

次のC#コードの例は、Base64エンコーディングを使用してMicrosoft .NETプロジェクト `MyApplication/EncryptDocument` から名前付きのプロセスを呼び出します。 (Base64エンコーディングを使用したAEM Formsの [呼び出しを参照](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding))。

Loan.pdfというPDFファイルに基づく保護されていないPDFドキュメント *が、AEM Formsプロセスに渡されます* 。 プロセスは、パスワードで暗号化されたPDFドキュメントを返します。この画像は、EncryptedPDF.pdfというPDFファイル *として保存されます*。

```java
 /*
     * Ensure that you create a .NET client assembly that uses
     * base64 encoding. This is required to populate a BLOB
     * object with data or retrieve data from a BLOB object.
     *
     * For information, see "Invoking AEM Forms using Base64 Encoding" in
     * Programming with AEM forms
     */
 using System;
 using System.Collections;
 using System.ComponentModel;
 using System.Data;
 using System.IO;
 
 namespace InvokeEncryptDocumentBase64
 {
 
        class InvokeEncryptDocumentUsingBase64
        {
 
            const int BUFFER_SIZE = 4096;
            [STAThread]
            static void Main(string[] args)
            {
 
                try
                {
                    String pdfFile = "C:\\Adobe\Loan.pdf";
                    String encryptedPDF = "C:\\Adobe\EncryptedPDF.pdf";
 
 
                    //Create an MyApplication_EncryptDocumentService object and set authentication values
                    MyApplication2_EncryptDocumentService encryptClient = new MyApplication2_EncryptDocumentService();
                    encryptClient.Credentials = new System.Net.NetworkCredential("administrator", "password");
 
                    //Reference the PDF file to send to the EncryptDocument process
                    FileStream fs = new FileStream(pdfFile, FileMode.Open);
 
                    //Create a BLOB object
                    BLOB inDoc = new BLOB();
 
                    //Get the length of the file stream
                    int len = (int)fs.Length;
                    byte[] ByteArray = new byte[len];
 
                    //Populate the byte array with the contents of the FileStream object
                    fs.Read(ByteArray, 0, len);
                    inDoc.binaryData = ByteArray;
 
                    //Invoke the EncryptDocument process
                    BLOB outDoc = encryptClient.invoke(inDoc);
 
                    //Populate a byte array with BLOB data
                    byte[] outByteArray = outDoc.binaryData;
 
                    //Create a new file named UsageRightsLoan.pdf
                    FileStream fs2 = new FileStream(encryptedPDF, FileMode.OpenOrCreate);
 
                    //Create a BinaryWriter object
                    BinaryWriter w = new BinaryWriter(fs2);
                    w.Write(outByteArray);
                    w.Close();
                    fs2.Close();
                 }
                catch (Exception ee)
                {
                    Console.WriteLine(ee.Message);
                }
            }
        }
 }
 
```

## クイック開始: JavaプロキシファイルとBase64エンコーディングを使用したサービスの呼び出し {#quick-start-invoking-a-service-using-java-proxy-files-and-base64-encoding}

次のJavaコードの例は、JAX-WSおよびBase64エンコーディングを使用して作成されたJavaプロキシファイルを使用して、という名前のプロセスを呼び出します。 `MyApplication/EncryptDocument` (Base64エンコーディングを使用したAEM Formsの [呼び出しを参照](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding))。

Loan.pdfというPDFファイルに基づく保護されていないPDFドキュメント *が、AEM Formsプロセスに渡されます* 。 プロセスは、パスワードで暗号化されたPDFドキュメントを返します。この画像は、EncryptedDocument.pdfというPDFファイル *として保存されます*。

```java
 /**
     * Ensure that you create Java proxy files that consume
     *theAEM Forms service WSDL. You can use JAX-WS to create
     * the Java proxy files.
     *
     * This Java quick start uses Base64 to invoke a short-lived process named
     * EncryptDocument. For information, see
     * "Invoking AEM Forms using Base64" in Programming with AEM forms.
     */
 
 import java.io.*;
 
 import javax.xml.ws.BindingProvider;
 import com.adobe.idp.services.*;
 
 public class InvokeEncryptDocumentBase64 {
     public static void main(String[] args){
 
         try{
             //Create a MyApplicationEncryptDocument object
             MyApplicationEncryptDocumentService encClient = new MyApplicationEncryptDocumentService();
             MyApplicationEncryptDocument encryptDocClient = encClient.getEncryptDocument();
 
             //Set connection values required to invoke AEM Forms
             String url = "'[server]:[port]'/soap/services/MyApplication/EncryptDocument?blob=base64";
             String username = "administrator";
             String password = "password";
             ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
             ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
             ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
 
                // Get the input PDF document to send to the EncryptDocument process
                BLOB inDoc = new BLOB();
 
             // Get the input DDX document and input PDF sources
             File fileName = new File("C:\\Adobe\Loan.pdf");
             FileInputStream inFs = new FileInputStream(fileName);
 
             // Get the length of the file stream and create a byte array
             int inLen = (int)fileName.length();
             byte[] inByteArray = new byte[inLen];
 
                // Populate the byte array with the content of the file stream
             inFs.read(inByteArray, 0, inLen);
 
                // Populate the BLOB objects
             inDoc.setBinaryData(inByteArray);
 
                //invoke the short-lived process named MyApplication/EncryptDocument
             BLOB outDoc = encryptDocClient.invoke(inDoc);
 
             //Save the encrypted file as a PDF file
             byte[] encryptedDocument = outDoc.getBinaryData();
 
             //Create a File object
             File outFile = new File("C:\\Adobe\EncryptedDocument.pdf");
 
             //Create a FileOutputStream object.
             FileOutputStream myFileW = new FileOutputStream(outFile);
 
             //Call the FileOutputStream object's write method and pass the pdf data
             myFileW.write(encryptedDocument);
 
             //Close the FileOutputStream object
             myFileW.close();
                System.out.println("The short-lived process named MyApplication/EncryptDocument was successfully invoked.");
         }
         catch(Exception e)
         {
             e.printStackTrace();
         }
 
     }
 
 }
 
 
```

## クイック開始: AEM Formsのリモート処理（AEM Formsでは廃止されています）を使用して安全でないドキュメントを渡すことによる短時間のみ有効なプロセスの呼び出し {#quick-start-invoking-a-short-lived-process-by-passing-an-unsecure-document-using-deprecated-for-aem-forms-aem-forms-remoting}

次のFlexコードの例は、という名前の短時間のみ有効なプロセスを呼び出し `MyApplication/EncryptDocument`ます。 （『AEM formsでは非推奨）AEM Formsのリモートを使用したAEM Formsの [呼び出し』を参照](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting))。

>[!NOTE]
>
>このクイック開始は、AEM Formsプロセスを呼び出し、セキュリティで保護されていないドキュメントをアップロードします。 このクイック開始を実行するには、セキュリティで保護されていないドキュメントをアップロードするようにAEM Formsを設定する必要があります。 セキュリティで保護されていないドキュメントを受け入れるようにAEM Formsを設定する方法について詳しくは、セキュリティで保護されているドキュメントとセキュリティで保護されていないを受け入れるようにAEM Formsを [設定する方法を参照してください](/help/forms/developing/invoking-aem-forms-using-remoting.md#configuring-aem-forms-to-accept-secure-and-unsecure-documents)。

```java
 <?xml version="1.0" encoding="utf-8"?>
 <mx:Application  xmlns="*"
      creationComplete="initializeChannelSet();">
      <mx:Script>
        <![CDATA[
 
      import mx.rpc.AEM Forms.DocumentReference;
      import flash.net.FileReference;
      import flash.net.URLRequest;
      import flash.events.Event;
      import flash.events.DataEvent;
      import mx.messaging.ChannelSet;
      import mx.messaging.channels.AMFChannel;
      import mx.rpc.events.ResultEvent;
      import mx.collections.ArrayCollection;
      import mx.rpc.AsyncToken;
 
       // Classes used in file retrieval
      private var fileRef:FileReference = new FileReference();
      private var docRef:DocumentReference = new DocumentReference();
      private var parentResourcePath:String = "/";
      private var serverPort:String = "'[server]:[port]'";
      private var now1:Date;
      private  var cs:ChannelSet
 
      // Holds information returned from AEM Forms
      [Bindable]
      public var progressList:ArrayCollection = new ArrayCollection();
 
      // Set up channel set to invoke AEM Forms.
      // This must be done before calling any service or process, but only
      // once for the entire application.
       private function initializeChannelSet():void {
        cs = new ChannelSet();
        cs.addChannel(new AMFChannel("remoting-amf", "https://" + serverPort + "/remoting/messagebroker/amf"));
        EncryptDocument.setCredentials("administrator", "password");
        EncryptDocument.channelSet = cs;
      }
 
      // Call this method to upload the file.
      // This creates a file picker and lets the user select a PDF file to pass to the EncryptDocument process.
      private function uploadFile():void {
        fileRef.addEventListener(Event.SELECT, selectHandler);
        fileRef.browse();
      }
 
       private function selectHandler(event:Event):void
             {
             var authTokenService:RemoteObject = new RemoteObject("LC.FileUploadAuthenticator");
             authTokenService.addEventListener("result", authTokenReceived);
             authTokenService.channelSet = cs;
             authTokenService.getFileUploadToken();
             }
 
     private function authTokenReceived(event:ResultEvent):void
             {
             var token:String = event.result as String;
             var request:URLRequest = DocumentReference.constructRequestForUpload("https://'[server]:[port]'", token);
 
             try
             {
           fileRef.upload(request);
             }
             catch (error:Error)
             {
             trace("Unable to upload file.");
             }
             }
 
 
      // Called once the file is completely uploaded.
      private function completeHandler(event:DataEvent):void {
        now1 = new Date();
 
        // Set the docRefs url and referenceType parameters
        docRef.url = event.data as String;
        docRef.referenceType=DocumentReference.REF_TYPE_URL;
        executeInvokeProcess();
      }
 
      //This method invokes the EncryptDocument process
      public function executeInvokeProcess():void {
 
         //Create an Object to store the input value for the EncryptDocument process
         var params:Object = new Object();
         params["inDoc"]=docRef;
 
         // Invoke the EncryptDocument process
         var token:AsyncToken;
         token = EncryptDocument.invoke(params);
         token.name = name;
      }
 
      // This method handles a successful conversion invocation
      public function handleResult(event:ResultEvent):void
      {
            //Retrieve information returned from the service invocation
          var token:AsyncToken = event.token;
          var res:Object = event.result;
          var dr:DocumentReference = res["outDoc"] as DocumentReference;
          var now2:Date = new Date();
 
          // These fields map to columns in the DataGrid
          var progObject:Object = new Object();
          progObject.filename = token.name;
          progObject.timing = (now2.time - now1.time).toString();
          progObject.state = "Success";
          progObject.link = "<a href=" + dr.url + "> open </a>";
          progressList.addItem(progObject);
      }
 
      private function resultHandler(event:ResultEvent):void {
        // Do anything else here.
      }
 
        ]]>
      </mx:Script>
      <mx:RemoteObject id="EncryptDocument" destination="MyApplication/EncryptDocument" result="resultHandler(event);">
          <mx:method name="invoke" result="handleResult(event)"/>
      </mx:RemoteObject>
 
      <!--//This consists of what is displayed on the webpage-->
      <mx:Panel id="lcPanel" title="EncryptDocument  (Deprecated for AEM forms) AEM Forms Remoting Example"
           height="25%" width="25%" paddingTop="10" paddingLeft="10" paddingRight="10"
           paddingBottom="10">
         <mx:Label width="100%" color="blue"
                text="Select a PDF file to pass to the EncryptDocument process"/>
        <mx:DataGrid x="10" y="0" width="500" id="idProgress" editable="false"
           dataProvider="{progressList}" height="231" selectable="false" >
          <mx:columns>
            <mx:DataGridColumn headerText="Filename" width="200" dataField="filename" editable="false"/>
            <mx:DataGridColumn headerText="State" width="75" dataField="state" editable="false"/>
            <mx:DataGridColumn headerText="Timing" width="75" dataField="timing" editable="false"/>
            <mx:DataGridColumn headerText="Click to Open" dataField="link" editable="false" >
             <mx:itemRenderer>
                <mx:Component>
                   <mx:Text x="0" y="0" width="100%" htmlText="{data.link}"/>
                </mx:Component>
             </mx:itemRenderer>
            </mx:DataGridColumn>
          </mx:columns>
        </mx:DataGrid>
        <mx:Button label="Select File" click="uploadFile()" />
      </mx:Panel>
 </mx:Application>
 
```

## クイック開始: .NETプロジェクトでDIMEを使用してサービスを呼び出す {#quick-start-invoking-a-service-using-dime-in-a-net-project}

次のC#コードの例は、Dimeを使用してMicrosoft .NETプロジェクト `MyApplication/EncryptDocument` から名前が付けられたプロセスを呼び出します。 (Base64エンコーディングを使用したAEM Formsの [呼び出しを参照](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding))。

DIMEを使用して、 *map.pdfというPDFファイルに基づく保護されていないPDFドキュメントがAEM Formsプロセスに渡されます* 。 パスワードで暗号化されたPDFドキュメントが返され、 *mapEncrypt.pdfというPDFファイルとして保存されます*。

```java
 /**
     *
     * Ensure that you create a .NET project that uses
     * Web Services Enhancements 2.0. This is required to send a
     * AEM Forms process an attachment using DIME.
     *
     * For information, see "Invoking AEM Forms using DIME" in Programming with AEM forms.
     */
 
 using System;
 using System.Collections;
 using System.ComponentModel;
 using System.Data;
 using System.IO;
 using Microsoft.Web.Services2.Dime;
 using Microsoft.Web.Services2.Attachments;
 using Microsoft.Web.Services2.Configuration;
 using Microsoft.Web.Services2;
 
 //The following statement represents a web reference to
 //the forms server that contains the process that
 //is invoked
 using ConsoleApplication1.LC_Host;
 
 namespace ConsoleApplication1
 {
 
      class InvokeEncryptDocumentUsingDime
        {
 
            const int BUFFER_SIZE = 4096;
            [STAThread]
            static void Main(string[] args)
            {
 
            try
               {
                   String pdfFile = "C:\\Adobe\map.pdf";
                   String encryptedPDF = "C:\\Adobe\mapEncrypt.pdf";
 
                   //Create an EncryptDocumentServiceWse object and set authentication values
                   EncryptDocumentServiceWse encryptClient = new EncryptDocumentServiceWse();
                   encryptClient.Credentials = new System.Net.NetworkCredential("administrator", "password");
 
                   // Create the DIME attachment representing a PDF document
                   DimeAttachment inputDocAttachment = new DimeAttachment(
                       System.Guid.NewGuid().ToString(),
                       "application/pdf",
                       TypeFormat.MediaType,
                       pdfFile);
 
                    //Create a BLOB object
                    BLOB inDoc = new BLOB();
 
                    //Set the DIME attachment ID
                    inDoc.attachmentID = inputDocAttachment.Id;
                    encryptClient.RequestSoapContext.Attachments.Add(inputDocAttachment);
 
                    //Invoke the EncryptDocument process
                    BLOB outDoc = encryptClient.invoke(inDoc);
 
                    //Get the returned attachment identifier value
                    String encryptedDocId = outDoc.attachmentID;
                    FileStream myStream = new FileStream(encryptedPDF, FileMode.Create, FileAccess.Write);
 
                    //Iterate through the attachments
                    foreach (Attachment attachment in encryptClient.ResponseSoapContext.Attachments)
                      {
                        if (attachment.Id.Equals(encryptedDocId))
                          {
                            //Create a byte array that contains the encrypted PDF document
                            System.IO.Stream mySteam2 = attachment.Stream;
                            byte[] myBytes = new byte[mySteam2.Length];
                            int size = (int)mySteam2.Length;
                            mySteam2.Read(myBytes, 0, size);
 
                            //Save the encrypted PDF document as a PDF file
                            FileStream fs2 = new FileStream(encryptedPDF, FileMode.OpenOrCreate);
 
                            //Create a BinaryWriter object
                            BinaryWriter w = new BinaryWriter(fs2);
                            w.Write(myBytes);
                            w.Close();
                            fs2.Close();
                            Console.Out.WriteLine("Saved converted document at:" + encryptedPDF);
                        }
                   }
                }
                catch (Exception ee)
               {
                   Console.WriteLine(ee.Message);
                }
            }
        }
 }
 
```

## クイック開始: JavaプロジェクトでのDIMEを使用したサービスの呼び出し {#quick-start-invoking-a-service-using-dime-in-a-java-project}

次のJavaコードの例は、DIMEを使用してという名前のプロセスを呼び出し `MyApplication/EncryptDocument` ます。 (DIMEを使用したAEM Formsの [呼び出しを参照](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-dime))。

Loan.pdfというPDFファイルに基づく保護されていないPDFドキュメント *が、DIMEを使用してAEM Formsプロセスに渡されます* 。 パスワードで暗号化されたPDFドキュメントが返され、EncryptLoan.pdfというPDFファイルとして *保存されます*。

```java
 /**
     * Ensure that you create Java Axis files that
     * are required to send a AEM Forms process
     * an attachment using DIME.
     *
     * For information, see "Invoking AEM Forms using DIME" in Programming with AEM forms.
     */
 import com.adobe.idp.services.*;
 import java.io.File;
 import java.io.FileOutputStream;
 import java.io.InputStream;
 import java.net.URL;
 import javax.activation.DataHandler;
 import javax.activation.FileDataSource;
 
 import org.apache.axis.attachments.AttachmentPart;
 
 public class InvokeDocumentEncryptDime {
     public static void main(String[] args) {
 
     try{
 
         //Create a MyApplicationEncryptDocumentServiceLocator object
         MyApplicationEncryptDocumentServiceLocator locate = new MyApplicationEncryptDocumentServiceLocator ();
 
         //specify the service target URL and object type
         URL serviceURL = new URL("https://'[server]:[port]'/soap/services/MyApplication/EncryptDocument?blob=dime");
 
         //Use the binding stub with the locator
         EncryptDocumentSoapBindingStub encryptionClientStub = new EncryptDocumentSoapBindingStub(serviceURL,locate);
         encryptionClientStub.setUsername("administrator");
         encryptionClientStub.setPassword("password");
 
          //Get the DIME Attachments - which is the PDF document to encrypt
          java.io.File file = new java.io.File("C:\\Adobe\Loan.pdf");
 
          //Create a DataHandler object
          DataHandler buildFile = new DataHandler(new FileDataSource(file));
 
          //Use the DataHandler object to create an AttachmentPart object
          AttachmentPart part = new AttachmentPart(buildFile);
         //get the attachment ID
         String attachmentID = part.getContentId();
 
         //Add the attachment to the encryption service stub
         encryptionClientStub.addAttachment(part);
 
         //Inform ES where the attachment is stored by providing the attachment id
         BLOB inDoc = new BLOB();
         inDoc.setAttachmentID(attachmentID);
 
         BLOB outDoc = encryptionClientStub.invoke(inDoc);
 
         //Go through the returned attachments and get the encrypted PDF document
         byte[] resultByte = null;
         attachmentID = outDoc.getAttachmentID();
 
         //Find the proper attachment
         Object[] parts = encryptionClientStub.getAttachments();
         for (int i=0;i<parts.length;i++){
             AttachmentPart attPart = (AttachmentPart)  parts[i];
             if (attPart.getContentId().equals(attachmentID)) {
                 //DataHandler
                 buildFile = attPart.getDataHandler();
                 InputStream stream = buildFile.getInputStream();
 
                 byte[] pdfStream = new byte[stream.available()];
                 stream.read(pdfStream);
 
                 //Create a File object
                 File outFile = new File("C:\\Adobe\EncryptLoan.pdf");
 
                 //Create a FileOutputStream object.
                 FileOutputStream myFileW = new FileOutputStream(outFile);
 
                 //Call the FileOutputStream object?s write method and pass the pdf data
                 myFileW.write(pdfStream);
 
                 //Close the FileOutputStream object
                 myFileW.close();
 
             }
         }
     }
     catch(Exception e)
     {
         e.printStackTrace();
     }
     }
 
 }
 
```

## クイック開始: JavaプロジェクトでHTTP経由のBLOBデータを使用してサービスを呼び出す {#quick-start-invoking-a-service-using-blob-data-over-http-in-a-java-project}

以下のJavaコードの例は、HTTP経由のデータを `MyApplication/EncryptDocument` 使用してという名前のプロセスを呼び出します。 (HTTP経由のBLOBデータを使用したAEM Formsの [呼び出しを参照](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-blob-data-over-http))。

Loan.pdfというPDFファイルに基づく保護されていないPDFドキュメント ** が、SOAP over HTTPを使用してAEM Formsプロセスに渡されます。 PDFファイルは次のURLにあります。 `https://'[server]:[port]'/FormsQS`. プロセスは、パスワードで暗号化されたPDFドキュメントを返します。この画像は、EncryptedDocument.pdfというPDFファイル *として保存されます*。

```java
 /**
     * Ensure that you create Java proxy files that consume
     *theAEM Forms service WSDL. You can use JAX-WS to create
     * the Java proxy files.
     *
     * This Java quick start uses BLOB over HTTP to invoke a short-lived process named
     * EncryptDocument. For information, see
     * "Invoking AEM Forms using BLOB over HTTP" in Programming with AEM forms.
     */
 import java.io.*;
 import java.net.URL;
 
 import javax.xml.ws.BindingProvider;
 import com.adobe.idp.services.*;
 
 public class InvokeEncryptDocumentHTTP {
     public static void main(String[] args){
 
         try{
             //Create a MyApplicationEncryptDocument object
             MyApplicationEncryptDocumentService encClient = new MyApplicationEncryptDocumentService();
             MyApplicationEncryptDocument encryptDocClient = encClient.getEncryptDocument();
 
             //Set connection values required to invoke AEM Forms using BLOB over HTTP
             String url = "https://'[server]:[port]'/soap/services/MyApplication/EncryptDocument?blob=http";
             String username = "administrator";
             String password = "password";
             ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
             ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
             ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
 
             //Create a BLOB object and populate it by invoking the setRemoteURL method
             BLOB inDoc = new BLOB();
             inDoc.setRemoteURL("https://'[server]:[port]'/FormsQS/Loan.pdf");
 
                //invoke the short-lived process named MyApplication/EncryptDocument
             BLOB outDoc = encryptDocClient.invoke(inDoc);
 
             //Retrieve an InputStream from the returned BLOB instance
             URL myURL = new URL(outDoc.getRemoteURL());
             InputStream inputStream = myURL.openStream();
 
             //Create a new file containing the returned PDF document
             File f = new File("C:\\Adobe\EncryptedDocument.pdf");
             OutputStream out = new FileOutputStream(f);
 
             //Iterate through the buffer
             byte buf[] = new byte[1024];
             int len;
             while ((len = inputStream.read(buf)) > 0)
                 out.write(buf, 0, len);
             out.close();
             inputStream.close();
 
              System.out.println("The short-lived process named EncryptDocument was successfully invoked.");
         }
         catch(Exception e)
         {
             e.printStackTrace();
         }
 
     }
 
 }
 
 
```

## クイック開始: .NETプロジェクトでHTTP経由のBLOBデータを使用してサービスを呼び出す {#quick-start-invoking-a-service-using-blob-data-over-http-in-a-net-project}

次のC#コードの例は、HTTP経由のデータを使用して、Microsoft .NETプロジェクト `MyApplication/EncryptDocument` からという名前のプロセスを呼び出します。 (HTTP経由のBLOBデータを使用したAEM Formsの [呼び出しを参照](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-blob-data-over-http))。

Loan.pdfというPDFファイルに基づく保護されていないPDFドキュメント ** が、HTTP経由のBLOBを使用してAEM Formsプロセスに渡されます。 プロセスは、パスワードで暗号化されたPDFドキュメントを返します。この画像は、EncryptedPDF.pdfというPDFファイル *として保存されます*。

```java
 /*
     * Ensure that you create a .NET client assembly that uses
     * SOAP over HTTP. This is required to populate a BLOB
     * object’s remote URL data memeber.
     *
     * For information, see "Invoking AEM Forms using BLOB data over HTTP" in
     * Programming with AEM forms
     */
 using System;
 using System.Collections;
 using System.ComponentModel;
 using System.Data;
 using System.IO;
 using System.Security.Policy;
 
 namespace InvokeEncryptDocumentHTTP
 {
 
        class InvokeEncryptDocumentUsingHTTP
        {
 
            const int BUFFER_SIZE = 4096;
            [STAThread]
            static void Main(string[] args)
            {
 
                try
                {
                    String urlData = "https://'[server]:[port]'/FormsQS/Loan.pdf";
 
                    //Create a MyApplication_EncryptDocumentService object and set authentication values
                    MyApplication_EncryptDocumentService encryptClient = new MyApplication_EncryptDocumentService();
                    encryptClient.Credentials = new System.Net.NetworkCredential("administrator", "password");
 
                    //Create a BLOB object
                    BLOB inDoc = new BLOB();
 
                    //Populate the BLOB object’s remoteURL data member
                    inDoc.remoteURL = urlData;
 
                    //Invoke the EncryptDocument process
                    BLOB outDoc = encryptClient.invoke(inDoc);
 
                    //Create a UriBuilder object using the
                    //BLOB object’s remoteURL data member field
                    UriBuilder uri = new UriBuilder(outDoc.remoteURL);
 
                   //Convert the UriBuilder to a Stream object
                    System.Net.WebRequest wr = System.Net.WebRequest.Create(uri.Uri);
                    System.Net.WebResponse response = wr.GetResponse();
                    System.IO.StreamReader sr = new System.IO.StreamReader(response.GetResponseStream());
                    Stream mySteam = sr.BaseStream;
 
                    //Create a byte array
                    byte[] myData = new byte[BUFFER_SIZE];
 
                   //Populate the byte array
                   PopulateArray(mySteam, myData);
 
                   //Create a new file named UsageRightsLoan.pdf
                   FileStream fs2 = new FileStream("C:\\Adobe\EncryptedPDF.pdf", FileMode.OpenOrCreate);
 
                   //Create a BinaryWriter object
                   BinaryWriter w = new BinaryWriter(fs2);
                   w.Write(myData);
                   w.Close();
                   fs2.Close();
                }
                catch (Exception ee)
                {
                    Console.WriteLine(ee.Message);
                }
            }
 
            public static void PopulateArray(Stream stream, byte[] data)
            {
                int offset = 0;
                int remaining = data.Length;
                while (remaining > 0)
                {
                    int read = stream.Read(data, offset, remaining);
                    if (read <= 0)
                        throw new EndOfStreamException();
                    remaining -= read;
                    offset += read;
                }
            }
 
        }
 }
 
```

## クイック開始: .NETプロジェクトでMTOMを使用してサービスを呼び出す {#quick-start-invoking-a-service-using-mtom-in-a-net-project}

次のC#コードの例は、MTOMを使用してMicrosoft .NETプロジェクト `MyApplication/EncryptDocument` からという名前のプロセスを呼び出します。 (MTOMを使用したAEM Formsの [呼び出しを参照](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom))。

MTOMを使用して、 *loan.pdfというPDFファイルに基づく保護されていないPDFドキュメントがAEM Formsプロセスに渡されます* 。 プロセスは、パスワードで暗号化されたPDFドキュメントを返します。この画像は、EncryptedDocument.pdfというPDFファイル *として保存されます*。

```java
 ???/**
     * Ensure that you create a .NET project that uses
     * MS Visual Studio 2008 and version 3.5 of the .NET
     * framework. This is required to invoke a
     * AEM Forms service using MTOM.
     *
     * For information, see "Invoking AEM Forms using MTOM" in Programming with AEM forms
     */
 using System;
 using System.Collections.Generic;
 using System.Linq;
 using System.Text;
 using System.ServiceModel;
 using EncryptDocumentMTOM.ServiceReference1;
 using System.IO;
 
 //Invoke the EncryptDocument process using MTOM
 namespace EncryptDocumentUsingMTOM
 {
        class Program
        {
            static void Main(string[] args)
            {
                try
                {
                    //Specify the name of the PDF file to encrypt
                    String pdfFile = "C:\\Adobe\loan.pdf";
 
                    //Create an EncryptDocumentClient object
                    MyApplication_EncryptDocumentClient encryptProcess = new MyApplication_EncryptDocumentClient();
                    encryptProcess.Endpoint.Address = new System.ServiceModel.EndpointAddress("https://'[server]:[port]'/soap/services/MyApplication/EncryptDocument?blob=mtom");
                    BasicHttpBinding b = (BasicHttpBinding)encryptProcess.Endpoint.Binding;
                    b.MessageEncoding = WSMessageEncoding.Mtom;
 
                    //Enable BASIC HTTP authentication
                    encryptProcess.ClientCredentials.UserName.UserName = "administrator";
                    encryptProcess.ClientCredentials.UserName.Password = "password";
                    b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
                    b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
                    b.MaxReceivedMessageSize = 4000000;
                    b.MaxBufferSize = 4000000;
                    b.ReaderQuotas.MaxArrayLength = 4000000;
 
                    //Reference the PDF file to send to the EncryptDocument process
                    FileStream fs = new FileStream(pdfFile, FileMode.Open);
 
                    //Create a BLOB object
                    BLOB inDoc = new BLOB();
 
                    //Get the length of the file stream
                    int len = (int)fs.Length;
                    byte[] ByteArray = new byte[len];
 
                    //Populate the byte array with the contents of the FileStream object
                    fs.Read(ByteArray, 0, len);
                    inDoc.MTOM = ByteArray;
 
                    //Invoke the EncryptDocument short-lived process
                    BLOB outDoc = encryptProcess.invoke(inDoc);
                    byte[] encryptDoc = outDoc.MTOM;
 
                    //Create a new file containing the encrypted PDF document
                    string FILE_NAME = "C:\\Adobe\EncryptedDocument.pdf";
                    FileStream fs2 = new FileStream(FILE_NAME, FileMode.OpenOrCreate);
                    BinaryWriter w = new BinaryWriter(fs2);
                    w.Write(encryptDoc);
                    w.Close();
                    fs2.Close();
                }
                catch (Exception ee)
                {
                    Console.WriteLine(ee.Message);
                }
            }
        }
 }
 
```

>[!NOTE]
>
>AEM Formsサービス操作の実行方法を示すクイック開始の多くには、MTOMコードの例が含まれています。

## クイック開始: JavaプロジェクトでのSwaRefを使用したサービスの呼び出し {#quick-start-invoking-a-service-using-swaref-in-a-java-project}

以下のJavaコードの例は、Javaプロジェクト `MyApplication/EncryptDocument` から名前のプロセスを呼び出します。 このJavaプロジェクトでは、JAX-WSとSwaRefをエンコーディングタイプとして使用して作成したプロキシクラスを使用します。 (SwaRefを使用したAEM Formsの [呼び出しを参照](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref))。

Loan.pdfというPDFファイルに基づく保護されていないPDFドキュメント ** が、SwaRefを使用してAEM Formsプロセスに渡されます。 暗号化されたPDFドキュメントは、EncryptedDocument.pdfというPDFファイル *として保存されます*。

```java
 /**
     * Ensure that you create Java proxy files that consume
     *theAEM Forms service WSDL. You can use JAX-WS to create
     * the Java proxy files.
     *
     * This Java quick start uses SwaRef to invoke a short-lived process named
     * EncryptDocument. For information, see
     * "Invoking AEM Forms using SwaRef" in Programming with AEM forms.
     */
 
 import javax.xml.ws.BindingProvider;
 import javax.activation.DataHandler;
 import javax.activation.DataSource;
 import javax.activation.FileDataSource;
 import java.io.*;
 
 import com.adobe.idp.services.*;
 
 public class InvokeEncryptDocumentSwaRef {
 
 public static void main(String[] args) {
 
         try{
 
         //Specify connection values required to invoke the MyApplication/EncryptDocument process
         //using SwaRef
         String url = "https://'[server]:[port]'/soap/services/MyApplication/EncryptDocument?blob=swaref";
         String username = "administrator";
         String password = "password";
         String pdfFile = "C:\\Adobe\Loan.pdf";
 
         //Create a MyApplicationEncryptDocument object
         MyApplicationEncryptDocumentService encClient = new MyApplicationEncryptDocumentService();
         MyApplicationEncryptDocument encryptDocClient = encClient.getEncryptDocument();
 
         ((BindingProvider)encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
         ((BindingProvider)encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
         ((BindingProvider)encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
 
          //Create a file object
          File pdf = new File(pdfFile);
 
          //Create a DataSource object
          DataSource myDS = new FileDataSource(pdf);
 
          //Create a DataHandler object
          DataHandler dataHandler = new DataHandler(myDS);
 
         //Create a BLOB object and populate it with the DataHandler
         BLOB inDoc = new BLOB();
         inDoc.setSwaRef(dataHandler);
 
         //Invoke the EncryptDocument process
         BLOB outDoc = encryptDocClient.invoke(inDoc);
 
         //Save the encrypted file as a PDF file
         DataHandler handler = outDoc.getSwaRef();
 
         //Create a new file containing the returned PDF document
         File f = new File("C:\\Adobe\EncryptedDocument.pdf");
         InputStream inputStream = handler.getInputStream();
         OutputStream out = new FileOutputStream(f);
 
         //Iterate through the buffer
         byte buf[] = new byte[1024];
         int len;
         while ((len = inputStream.read(buf)) > 0)
             out.write(buf, 0, len);
         out.close();
         inputStream.close();
 
          System.out.println("The short-lived process named MyApplication/EncryptDocument was successfully invoked.");
 
         }catch (Exception e) {
              e.printStackTrace();
             }
         }
 }
 
 
```

>[!NOTE]
>
>サービス操作の実行方法を示すクイック開始の多くには、SwaRefコード例が含まれています。

