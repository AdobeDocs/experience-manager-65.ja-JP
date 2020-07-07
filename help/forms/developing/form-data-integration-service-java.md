---
title: Form Data Integration Service JavaAPI Quick開始(SOAP)
seo-title: Form Data Integration Service JavaAPI Quick開始(SOAP)
description: 'null'
seo-description: 'null'
uuid: bde8e83d-56d3-4331-a025-82b327c219b7
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 91b738ec-aa00-4f05-bf42-2574ced8d993
translation-type: tm+mt
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 0%

---


# Form Data Integration Service Java API Quick開始(SOAP) {#form-data-integration-service-javaapi-quick-start-soap}

Form Data Integrationサービスでは、次のクイック開始を使用できます。

[クイック開始（SOAPモード）: Java APIを使用したフォームデータの読み込み](form-data-integration-service-java.md#quick-start-soap-mode-importing-form-data-using-the-java-api)

[クイック開始（SOAPモード）: Java APIを使用したフォームデータの書き出し](form-data-integration-service-java.md#quick-start-soap-mode-exporting-form-data-using-the-java-api)

AEM Forms操作は、厳密に型指定されたAPIをAEM Formsを使用して実行できます。接続モードはSOAPに設定する必要があります。

>[!NOTE]
>
>「AEM Formsによるプログラミング」にあるクイック開始は、JBoss Application ServerおよびMicrosoft WindowsオペレーティングシステムにデプロイされるForms Serverに基づいています。 ただし、UNIXなど別のオペレーティングシステムを使用している場合は、Windows固有のパスを、該当するオペレーティングシステムでサポートされているパスに置き換えます。 同様に、別のJ2EEアプリケーションサーバーを使用する場合は、有効な接続プロパティを指定していることを確認してください。 See [Setting connection properties](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).

## クイック開始（SOAPモード）: Java APIを使用したフォームデータの読み込み {#quick-start-soap-mode-importing-form-data-using-the-java-api}

以下のJavaコードの例を使用することで、データをPDFフォームに読み込むことができます。 データは *Loan_data.xmlというXMLファイルにあり* 、PDFフォームはResultLoanForm.pdfというPDFファイルとして保存され **&#x200B;ます。 (フォームデータの [読み込みを参照](/help/forms/developing/importing-exporting-data.md#importing-form-data))。

```as3
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-formdataintegration-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the forms server is not deployed
     * on JBoss)
     * 6. activation.jar (required for SOAP mode)
     * 7. axis.jar (required for SOAP mode)
     * 8. commons-codec-1.3.jar (required for SOAP mode)
     * 9.  commons-collections-3.1.jar  (required for SOAP mode)
     * 10. commons-discovery.jar (required for SOAP mode)
     * 11. commons-logging.jar (required for SOAP mode)
     * 12. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 13. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 14. jaxrpc.jar (required for SOAP mode)
     * 15. log4j.jar (required for SOAP mode)
     * 16. mail.jar (required for SOAP mode)
     * 17. saaj.jar (required for SOAP mode)
     * 18. wsdl4j.jar (required for SOAP mode)
     * 19. xalan.jar (required for SOAP mode)
     * 20. xbean.jar (required for SOAP mode)
     * 21. xercesImpl.jar (required for SOAP mode)
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
     * SOAP required JAR files are located in the following path:
     * <install directory>/sdk/client-libs/thirdparty
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include these additional JAR files
     *
     * For information about the SOAP
     * mode, see "Setting connection properties" in Programming
     * with AEM Forms
     */
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.formdataintegration.client.*;
 
 public class ImportDataSOAP {
 
     public static void main(String[] args) {
 
         try{
             //Set connection properties required to invoke AEM Forms using SOAP mode
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
              //Create a ServiceClientFactory object
              ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a FormDataIntegrationClient object
             FormDataIntegrationClient dataClient = new FormDataIntegrationClient(myFactory);
 
             //Import XDP XML data into an XFA PDF document
             //Reference an XFA PDF form
             FileInputStream inputStream = new FileInputStream("C:\\Adobe\Loan.pdf");
             Document inputPDF = new Document(inputStream);
 
             FileInputStream dataInput = new FileInputStream("C:\\Adobe\Loan_data.xml");
             Document inputDataFile = new Document(dataInput);
 
             //Import data into the form
             Document resultPDF = dataClient.importData(inputPDF,inputDataFile);
 
             //Save the PDF file
             File resultFile = new File("C:\\Adobe\ResultLoanForm.pdf");
             resultPDF.copyToFile(resultFile);
 
         }catch (Exception e) {
              e.printStackTrace();
         }
       }
     }
 
```

## クイック開始（SOAPモード）: Java APIを使用したフォームデータの書き出し {#quick-start-soap-mode-exporting-form-data-using-the-java-api}

以下のJavaコードの例は、PDFフォームからデータを書き出します。 フォームデータは、 *Loan_data.xmlというXMLファイルとして保存されます*。 (Exporting Form Data [](/help/forms/developing/importing-exporting-data.md#exporting-form-data))。

```as3
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-formdataintegration-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the forms server is not deployed
     * on JBoss)
     * 6. activation.jar (required for SOAP mode)
     * 7. axis.jar (required for SOAP mode)
     * 8. commons-codec-1.3.jar (required for SOAP mode)
     * 9.  commons-collections-3.1.jar  (required for SOAP mode)
     * 10. commons-discovery.jar (required for SOAP mode)
     * 11. commons-logging.jar (required for SOAP mode)
     * 12. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 13. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 14. jaxrpc.jar (required for SOAP mode)
     * 15. log4j.jar (required for SOAP mode)
     * 16. mail.jar (required for SOAP mode)
     * 17. saaj.jar (required for SOAP mode)
     * 18. wsdl4j.jar (required for SOAP mode)
     * 19. xalan.jar (required for SOAP mode)
     * 20. xbean.jar (required for SOAP mode)
     * 21. xercesImpl.jar (required for SOAP mode)
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
     * SOAP required JAR files are located in the following path:
     * <install directory>/sdk/client-libs/thirdparty
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include these additional JAR files
     *
     * For information about the SOAP
     * mode, see "Setting connection properties" in Programming
     * with AEM Forms
     */
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.formdataintegration.client.*;
 
 public class ExportDataSOAP {
 
     public static void main(String[] args) {
 
     try{
         //Set connection properties required to invoke AEM Forms using SOAP mode
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
          //Create a ServiceClientFactory object
          ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
          //Create a FormDataIntegrationClient object
          FormDataIntegrationClient dataClient = new FormDataIntegrationClient(myFactory);
 
          //Reference a PDF form from which to export data
          FileInputStream fileInputStream2 = new FileInputStream("C:\\Adobe\LoanForm.pdf");
          Document inputPDF = new Document(fileInputStream2);
 
          //Export data from the form
          Document resultPDF = dataClient.exportData(inputPDF);
 
          //Save the exported form data as an XML file
          File resultFile = new File("C:\\Adobe\Loan_data.xml");
          resultPDF.copyToFile(resultFile);
 
     }catch (Exception e) {
              e.printStackTrace();
         }
     }
 }
```

