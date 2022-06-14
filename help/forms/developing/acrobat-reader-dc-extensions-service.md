---
title: Acrobat Reader DC Extensions ServiceJava API クイックスタート (SOAP)
seo-title: Acrobat Reader DC extensions ServiceJava API Quick Start(SOAP)
description: Acrobat Reader DC Extensions サービスを使用して、PDF ドキュメントに使用権限を適用したり、PDF ドキュメントから使用権限を削除したり、LoanUsageRights.pdf という名前の権限を持つ PDF ドキュメントに使用権限を適用するために使用される秘密鍵証明書に関する情報を取得したりしてください。
seo-description: Use the  Acrobat Reader DC Extensions service to apply usage rights to a PDF document, remove usage rights from PDF documents, and retrieve  information about the credential that is used to apply usage-rights to a rights-enabled PDF document named LoanUsageRights.pdf.
uuid: 8e72ca94-a8c1-43aa-9845-a0da597051c5
contentOwner: admin
content-type: reference
topic-tags: develop
discoiquuid: 31a9bfc6-462d-4535-888f-31026b8fa674
role: Developer
exl-id: 82f0b6c1-ca0c-48c7-b7f6-b54704ac0830
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 100%

---

# Acrobat Reader DC Extensions ServiceJava API クイックスタート (SOAP) {#acrobat-reader-dc-extensions-servicejava-api-quick-start-soap}

Acrobat Reader DC Extensions サービスでは、次のクイックスタートを使用できます。

[クイックスタート（SOAP モード）：Java API を使用した使用権限の適用](#quick-start-soap-mode-applying-usage-rights-using-the-java-api)

[PDF ドキュメントから使用権限を削除](#quick-start-soap-mode-removing-usage-rights-from-a-pdf-document-using-the-java-api)

[クイックスタート（SOAP モード）：Java API を使用した秘密鍵証明書情報の取得](acrobat-reader-dc-extensions-service.md#quick-start-soap-mode-retrieving-credential-information-using-the-java-api)

AEM Forms の操作は、AEM Forms の厳密に型指定された API を使用して実行できます。接続モードは、SOAP に設定する必要があります。

>[!NOTE]
>
>『AEM Forms によるプログラミング』にあるクイックスタートは、Forms サーバーのオペレーティングシステムに基づいています。ただし、UNIX などの別のオペレーティングシステムを使用している場合は、Windows 固有のパスを、該当するオペレーティングシステムでサポートされているパスに置き換えます。 同様に、別の J2EE アプリケーションサーバーを使用している場合は、有効な接続プロパティを必ず指定してください。 （[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照）。

## クイックスタート（SOAP モード）：Java API を使用した使用権限の適用 {#quick-start-soap-mode-applying-usage-rights-using-the-java-api}

次の Java コードの例では、 使用権限を *Loan.pdf* という名前の PDF ドキュメントに適用します。権限を持つ PDF ドキュメントは、*LoanUsageRights.pdf* という名前の PDF ファイルとして保存されます。 この PDF ドキュメントには、`enabledComments`、`enabledFormFillIn`、および `enabledDigitalSignatures` の使用権限が適用されます。（[PDF ドキュメントへの使用権限の適用](/help/forms/developing/assigning-usage-rights.md)）。


```java
 /* 
     * This Java Quick Start uses the SOAP mode and contains the following JAR files 
     * in the class path: 
     * 1. adobe-reader-extensions-client.jar 
     * 2. adobe-livecycle-client.jar 
     * 3. adobe-usermanager-client.jar 
     * 4. activation.jar (required for SOAP mode) 
     * 5. axis.jar (required for SOAP mode) 
     * 6. commons-codec-1.3.jar (required for SOAP mode) 
     * 7. commons-collections-3.2.jar  (required for SOAP mode) 
     * 8. commons-discovery.jar (required for SOAP mode) 
     * 9. commons-logging.jar (required for SOAP mode) 
     * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode) 
     * 11. jaxen-1.1-beta-9.jar (required for SOAP mode) 
     * 12. jaxrpc.jar (required for SOAP mode) 
     * 13. log4j.jar (required for SOAP mode) 
     * 14. mail.jar (required for SOAP mode) 
     * 15. saaj.jar (required for SOAP mode) 
     * 16. wsdl4j.jar (required for SOAP mode) 
     * 17. xalan.jar (required for SOAP mode) 
     * 18. xbean.jar (required for SOAP mode) 
     * 19. xercesImpl.jar (required for SOAP mode) 
     * 
     * These JAR files are located in the following path: 
     * <install directory>/sdk/client-libs/common 
     * 
     * 
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
 import com.adobe.livecycle.readerextensions.client.*; 
 import java.util.*; 
 import java.io.File; 
 import java.io.FileInputStream; 
 import com.adobe.idp.Document; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
  
 public class ApplyUsageRightsSOAP{ 
  
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
          
           //Create a ReaderExtensionsServiceClient object 
           ReaderExtensionsServiceClient reClient = new ReaderExtensionsServiceClient(myFactory);  
          
           //Retrieve the PDF document to which to apply usage rights 
           FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\Loan.pdf");  
           Document inputPDF = new Document(fileInputStream); 
                   
           //Create a UsageRight object and specify specific usage rights 
           UsageRights useRight = new UsageRights();  
           useRight.setEnabledDynamicFormFields(true); 
           useRight.setEnabledComments(true); 
           useRight.setEnabledFormFillIn(true); 
           useRight.setEnabledDigitalSignatures(true); 
          
           //Create a ReaderExtensionsOptions object 
           ReaderExtensionsOptionSpec reOptions = new ReaderExtensionsOptionSpec();  
                   
           //Set the usage rights  
           reOptions.setUsageRights(useRight);  
           reOptions.setMessage("This is a Rights-Enabled PDF Document"); 
          
           //Apply usage rights to a PDF document 
           Document rightsEnabledPDF = reClient.applyUsageRights( 
              inputPDF, 
              "RE2", 
             null, 
             reOptions);  
          
           //Create a new PDF file that represents the rights-enabled PDF document 
           File resultFile = new File("C:\\Adobe\LoanUsageRights.pdf");  
           rightsEnabledPDF.copyToFile(resultFile); 
                          
         }catch (Exception e) { 
              e.printStackTrace(); 
         }     
     } 
 } 
  
  
```

## クイックスタート（SOAP モード）：Java API を使用した PDF ドキュメントからの使用権限の削除 {#quick-start-soap-mode-removing-usage-rights-from-a-pdf-document-using-the-java-api}

次の Java コードの例では、*LoanUsageRights.pdf* という名前の権限を持つ PDF ドキュメントから使用権限を削除します。 （[PDF ドキュメントから使用権限の削除](/help/forms/developing/assigning-usage-rights.md)を参照してください）。

```java
 /* 
     * This Java Quick Start uses the SOAP mode and contains the following JAR files 
     * in the class path: 
     * 1. adobe-reader-extensions-client.jar 
     * 2. adobe-livecycle-client.jar 
     * 3. adobe-usermanager-client.jar 
     * 4. activation.jar (required for SOAP mode) 
     * 5. axis.jar (required for SOAP mode) 
     * 6. commons-codec-1.3.jar (required for SOAP mode) 
     * 7. commons-collections-3.2.jar  (required for SOAP mode) 
     * 8. commons-discovery.jar (required for SOAP mode) 
     * 9. commons-logging.jar (required for SOAP mode) 
     * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode) 
     * 11. jaxen-1.1-beta-9.jar (required for SOAP mode) 
     * 12. jaxrpc.jar (required for SOAP mode) 
     * 13. log4j.jar (required for SOAP mode) 
     * 14. mail.jar (required for SOAP mode) 
     * 15. saaj.jar (required for SOAP mode) 
     * 16. wsdl4j.jar (required for SOAP mode) 
     * 17. xalan.jar (required for SOAP mode) 
     * 18. xbean.jar (required for SOAP mode) 
     * 19. xercesImpl.jar (required for SOAP mode) 
     * 
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to  
     * your local development environment and then include the 3 JBoss JAR files in your class path 
     * 
     * These JAR files are located in the following path: 
     * <install directory>/sdk/client-libs/common 
     * 
     * 
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
 import com.adobe.livecycle.readerextensions.client.*; 
 import java.util.*; 
 import java.io.File; 
 import java.io.FileInputStream; 
 import com.adobe.idp.Document; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
  
 public class RemoveUsageRights{ 
  
     public static void main(String[] args) { 
       try{ 
           //Set connection properties required to invoke AEM Forms                                 
           Properties connectionProps = new Properties(); 
           connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'"); 
          connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);           
           connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss"); 
           connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator"); 
           connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
          
           //Create a ServiceClientFactory object 
           ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps); 
                  
           //Create a ReaderExtensionsServiceClient object 
           ReaderExtensionsServiceClient reClient = new ReaderExtensionsServiceClient(myFactory);  
          
                //Retrieve a rights-enabled PDF document from 
                //which to remove usage rights 
           FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\LoanUsageRights.pdf");  
           Document inputPDF = new Document(fileInputStream); 
                   
           //Remove usage rights from the PDF document 
           Document rightsEnabledPDF = reClient.removeUsageRights(inputPDF);  
          
           //Save the PDF document as a PDF file 
           File resultFile = new File("C:\\Adobe\noUsageRightsLoan.pdf");  
           rightsEnabledPDF.copyToFile(resultFile); 
           System.out.println("Usage rights were removed from the document");  
                          
         }catch (Exception e) { 
              e.printStackTrace(); 
         }     
     } 
 } 
 
```

## クイックスタート（SOAP モード）：Java API を使用した秘密鍵証明書情報の取得 {#quick-start-soap-mode-retrieving-credential-information-using-the-java-api}

次の Java コードの例では、*LoanUsageRights.pdf* という名前の権限を与えられた PDF ドキュメントに使用権原を適用するために使用される秘密鍵証明書に関する情報を取得します。 （[認証情報の取得](/help/forms/developing/assigning-usage-rights.md)を参照してください）。

```java
 /* 
     * This Java Quick Start uses the SOAP mode and contains the following JAR files 
     * in the class path: 
     * 1. adobe-reader-extensions-client.jar 
     * 2. adobe-livecycle-client.jar 
     * 3. adobe-usermanager-client.jar 
     * 4. activation.jar (required for SOAP mode) 
     * 5. axis.jar (required for SOAP mode) 
     * 6. commons-codec-1.3.jar (required for SOAP mode) 
     * 7. commons-collections-3.2.jar  (required for SOAP mode) 
     * 8. commons-discovery.jar (required for SOAP mode) 
     * 9. commons-logging.jar (required for SOAP mode) 
     * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode) 
     * 11. jaxen-1.1-beta-9.jar (required for SOAP mode) 
     * 12. jaxrpc.jar (required for SOAP mode) 
     * 13. log4j.jar (required for SOAP mode) 
     * 14. mail.jar (required for SOAP mode) 
     * 15. saaj.jar (required for SOAP mode) 
     * 16. wsdl4j.jar (required for SOAP mode) 
     * 17. xalan.jar (required for SOAP mode) 
     * 18. xbean.jar (required for SOAP mode) 
     * 19. xercesImpl.jar (required for SOAP mode) 
     * 
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to  
     * your local development environment and then include the 3 JBoss JAR files in your class path 
     * 
     * These JAR files are located in the following path: 
     * <install directory>/sdk/client-libs/common 
     * 
     * 
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
 import com.adobe.livecycle.readerextensions.client.*; 
 import java.util.*; 
 import java.io.FileInputStream; 
 import com.adobe.idp.Document; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
  
 public class RetrieveCredentialInformation { 
  
     public static void main(String[] args) { 
       try{ 
                   
           //Set connection properties required to invoke AEM Forms                             
           Properties connectionProps = new Properties(); 
           connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'"); 
          connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);           
           connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss"); 
           connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator"); 
           connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
          
           //Create a ServiceClientFactory object 
           ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps); 
                  
           //Create a ReaderExtensionsServiceClient object 
           ReaderExtensionsServiceClient reClient = new ReaderExtensionsServiceClient(myFactory);  
          
           //Retrieve a rights-enabled PDF document 
           FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\LoanUsageRights.pdf");  
           Document inputPDF = new Document(fileInputStream); 
                   
           //Retrieve credential information 
           GetUsageRightsResult usageRightsResult = reClient.getDocumentUsageRights(inputPDF);  
          
           //Get the date after which the credential is no longer valid 
           Date endDate = usageRightsResult.getNotAfter(); 
          
           //Get the message displayed in Adobe Reader when the rights-enabled 
           //document is opened 
           String message = usageRightsResult.getMessage(); 
          
           //Get usage rights to see if the enableFormFillIn is enabled 
           UsageRights myRights = usageRightsResult.getRights(); 
           boolean ans = myRights.isEnabledFormFillIn(); 
          
           if (ans==true) 
              System.out.println("The enableFormFillIn usage right is enabled"); 
           else 
             System.out.println("The enableFormFillIn usage right is not enabled"); 
                                                   
         }catch (Exception e) { 
              e.printStackTrace(); 
         }     
                  
     } 
 } 
 
```
