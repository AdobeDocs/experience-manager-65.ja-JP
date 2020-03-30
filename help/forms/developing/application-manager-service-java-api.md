---
title: Application ManagerサービスのJavaAPIクイック開始(SOAP)
seo-title: Application ManagerサービスのJavaAPIクイック開始(SOAP)
description: 'null'
seo-description: 'null'
uuid: 01a9bce3-868b-495b-bdee-bc60f029129e
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 12da2a9b-4009-496e-953f-c2ae0352f59f
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Application ManagerサービスのJavaAPIクイック開始(SOAP) {#application-manager-service-javaapi-quick-start-soap}

Application Managerサービスでは、Java APIクイック開始(SOAP)を使用できます。

[クイック開始:Java API(SOAP)を使用したアプリケーションのデプロイ](application-manager-service-java-api.md#quick-start-soap-mode-deploying-applications-using-the-java-api)

[クイック開始:Java API(SOAP)を使用したアプリケーションの削除](application-manager-service-java-api.md#quick-start-soap-mode-removing-an-application-using-the-java-api)

>[!NOTE]
>
>アプリケーションマネージャーAPIは、AEM Forms LCAファイルのみをサポートします。 LiveCycle ES2およびES4のLCAファイルはサポートされません。

AEM Formsの操作は、AEM Formsの厳密に型指定されたAPIを使用して実行できます。接続モードはSOAPに設定する必要があります。

* ***注意&#x200B;**:「AEM Formsでのプログラミング」にあるJava API(SOAP)クイック開始は、Unixなど別のオペレーティングシステムを使用している場合、Windows固有のパスを、該当するオペレーティングシステムでサポートされているパスに置き換えます。 同様に、別のJ2EEアプリケーションサーバーを使用する場合は、有効な接続プロパティを指定します。 （[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照。）*

## クイック開始（SOAPモード）:Java APIを使用したアプリケーションのデプロイ {#quick-start-soap-mode-deploying-applications-using-the-java-api}

次のJavaコードの例では、EncryptDocument.lcaという名前の既存のLCAファイルに基づいてアプリケーションを読み込 *みます*。

```as3
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-livecycle-client.jar
     * 2. adobe-usermanager-client.jar
     * 3. activation.jar (required for SOAP mode)
     * 4. axis.jar (required for SOAP mode)
     * 5. commons-codec-1.3.jar (required for SOAP mode)
     * 6. commons-collections-3.2.jar  (required for SOAP mode)
     * 7. commons-discovery.jar (required for SOAP mode)
     * 8. commons-logging.jar (required for SOAP mode)
     * 9. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 10. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 11. jaxrpc.jar (required for SOAP mode)
     * 12. log4j.jar (required for SOAP mode)
     * 13. mail.jar (required for SOAP mode)
     * 14. saaj.jar (required for SOAP mode)
     * 15. wsdl4j.jar (required for SOAP mode)
     * 16. xalan.jar (required for SOAP mode)
     * 17. xbean.jar (required for SOAP mode)
     * 18. xercesImpl.jar (required for SOAP mode)
     * 19. adobe-workflow-client-sdk.jar
     * 20. adobe-applicationmanager-client-sdk.jar
 
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
     */
 
 import java.io.FileInputStream;
 import java.util.*;
 
 import com.adobe.idp.Document;
 import com.adobe.idp.applicationmanager.application.ApplicationStatus;
 import com.adobe.idp.applicationmanager.client.ApplicationManager;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class DeployApplication {
 
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
 
             //Get the AEM Forms application to deploy
             FileInputStream fileApp = new FileInputStream("C:\\Adobe\EncryptDocument.lca");
             Document lcApp = new Document(fileApp);
 
             //Create an ApplicationManager object
             ApplicationManager appManager = new ApplicationManager(myFactory);
 
             //Import the application into the production server
             ApplicationStatus appStatus = appManager.importApplicationArchive(lcApp);
             int status = appStatus.getStatusCode();
 
             //Determine if the application was successfully deployed
             if (status==1)
                     System.out.println("The application was successfully deployed");
             else
                     System.out.println("The application was not successfully deployed. The status is "+status);
         }
         catch(Exception e)
         {
             e.printStackTrace();
         }
     }
 }
 
```

## クイック開始（SOAPモード）:Java APIを使用したアプリケーションの削除 {#quick-start-soap-mode-removing-an-application-using-the-java-api}

次のJavaコードの例は、EncryptDocumentという名前のアプリケーションを削 *除します*。

```as3
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-livecycle-client.jar
     * 2. adobe-usermanager-client.jar
     * 3. activation.jar (required for SOAP mode)
     * 4. axis.jar (required for SOAP mode)
     * 5. commons-codec-1.3.jar (required for SOAP mode)
     * 6. commons-collections-3.2.jar  (required for SOAP mode)
     * 7. commons-discovery.jar (required for SOAP mode)
     * 8. commons-logging.jar (required for SOAP mode)
     * 9. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 10. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 11. jaxrpc.jar (required for SOAP mode)
     * 12. log4j.jar (required for SOAP mode)
     * 13. mail.jar (required for SOAP mode)
     * 14. saaj.jar (required for SOAP mode)
     * 15. wsdl4j.jar (required for SOAP mode)
     * 16. xalan.jar (required for SOAP mode)
     * 17. xbean.jar (required for SOAP mode)
     * 18. xercesImpl.jar (required for SOAP mode)
     * 19. adobe-workflow-client-sdk.jar
     * 20. adobe-applicationmanager-client-sdk.jar
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
     */
 
 
 import java.util.*;
 
 import com.adobe.idp.applicationmanager.application.Application;
 import com.adobe.idp.applicationmanager.application.ApplicationId;
 
 import com.adobe.idp.applicationmanager.client.ApplicationManager;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class RemoveApplication {
 
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
 
             //Create a ComponentRegistryClient object
             ApplicationManager appManager = new ApplicationManager(myFactory);
 
             //Get all the deployed applications
             List allApps = appManager.getApplications();
 
             //Iterate through the applications
             Iterator iter= allApps.iterator();
             while (iter.hasNext()) {
 
              //Cast each element to an Application object
              Application myApplication  = (Application)iter.next();
              ApplicationId appID = myApplication.getApplicationId();
              String appName = appID.getApplicationName();
 
              System.out.println("The name of the AEM Forms application is "+ appID.getApplicationName());
              //Determine the name of the application
              if (appName.compareTo("EncryptDocument")==0)
              {
                  //Remove the application
                 appManager.removeApplication(appID);
                 System.out.println("The  "+ appID.getApplicationName() +" application was removed.");
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

