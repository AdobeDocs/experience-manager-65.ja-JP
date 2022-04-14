---
title: PDF サービス Java API クイックスタート（SOAP）を生成
seo-title: Generate PDF Service Java API QuickStart(SOAP)
description: Generate PDF サービスを使用して、Microsoft Word ドキュメントを PDF ドキュメントに変換し、HTML コンテンツを PDF ドキュメントに変換し、Java API を使用して PDF ドキュメントを RTF ファイルに変換します。
seo-description: Use the Generate PDF service to convert a Microsoft Word document to a PDF document, convert HTML content to a PDF document, convert a PDF document to an RTF file using the Java API.
uuid: f8c4a476-de5e-440a-b419-0bd1d7fde5ca
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: a7c0c4cf-7476-41e7-8d4e-564e6a21458d
role: Developer
exl-id: b856a93b-91fa-47a5-9e46-6a537218fd4e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '324'
ht-degree: 100%

---

# Generate PDF サービス Java API クイックスタート（SOAP） {#generate-pdf-service-java-api-quickstart-soap}

Java API クイックスタート（SOAP）は Generate PDF サービスで使用できます。

[クイックスタート（SOAP モード）：Java API を使用して Microsoft Word ドキュメントを PDF ドキュメントに変換](generate-pdf-service-java-api.md#quick-start-soap-mode-converting-a-microsoft-word-document-to-a-pdf-document-using-the-java-api)

[クイックスタート（SOAP モード）：Java API を使用して HTML コンテンツを PDF ドキュメントに変換](generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[クイックスタート（SOAP モード）：Java API（SOAP モード）を使用して PDF ドキュメントを RTF ファイルに変換](generate-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-an-rtf-file-using-the-java-api-soap-mode)

AEM Forms の操作は、AEM Forms の厳密に型指定された API を使用して実行できます。接続モードは、SOAP に設定する必要があります。

>[!NOTE]
>
>『AEM Forms によるプログラミング』にあるクイックスタートは、JBoss アプリケーションサーバーと Microsoft Windows オペレーティングシステムにデプロイされる Forms サーバーに基づいています。ただし、UNIX などの別のオペレーティングシステムを使用している場合は、Windows 固有のパスを、該当するオペレーティングシステムでサポートされているパスに置き換えます。 同様に、別の J2EE アプリケーションサーバーを使用している場合は、有効な接続プロパティを必ず指定してください。 （[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照）。

## クイックスタート（SOAP モード）：Java API を使用して Microsoft Word ドキュメントを PDF ドキュメントに変換 {#quick-start-soap-mode-converting-a-microsoft-word-document-to-a-pdf-document-using-the-java-api}

次のコードの例では、*Loan.doc* という名前の Word ファイルを *Loan.pdf* という名前の PDF ドキュメントに変換します（[Word ドキュメントを PDF ドキュメントへに変換](/help/forms/developing/converting-file-formats-pdf.md#converting-word-documents-to-pdf-documents)を参照してください）。

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-generatepdf-client.jar
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
 import java.io.File;
 import java.io.FileInputStream;
 import java.util.Properties;
 
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.generatepdf.client.CreatePDFResult;
 import com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient;
 
 public class ConvertWordDocumentSOAP {
 
     public static void main(String[] args)
     {
         try{
         //Set connection properties required to invoke AEM Forms using SOAP mode
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory instance
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create a GeneratePdfServiceClient object
         GeneratePdfServiceClient pdfGenClient = new GeneratePdfServiceClient(myFactory);
 
         //Get a Microsoft Word file document to convert to a PDF document
         String inputFileName = "C:\\Adobe\\Loan.doc";
         FileInputStream fileInputStream = new FileInputStream(inputFileName);
         Document inDoc = new Document(fileInputStream);
 
         //Set createPDF2 parameter values
         String adobePDFSettings = "Smallest_File_Size";
          String securitySettings = "No Security";
          String fileTypeSettings = "Filetype Settings";
 
          //Convert the Word document to a PDF document
          CreatePDFResult result = pdfGenClient.createPDF2(
             inDoc,
             inputFileName,
             fileTypeSettings,
             adobePDFSettings,
             securitySettings,
             null,
             null);
 
          //Get the newly created document
          Document createdDocument = result.getCreatedDocument();
 
          //Save the converted PDF document as a PDF file
         createdDocument.copyToFile(new File("C:\\Adobe\\Loan.pdf"));
     }
     catch (Exception e) {
         System.out.println("Error OCCURRED: " + e.getMessage());
         }
     }
 }
```

## クイックスタート（SOAP モード）：Java API を使用して HTML コンテンツを PDF ドキュメントに変換 {#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api}

次の Java コードの例では、https://www.adobe.com にある HTML コンテンツを、*AdobeHTML.pdf* という名前の PDF ドキュメントに変換します（[HTML ドキュメントを PDF ドキュメントに変換](/help/forms/developing/converting-file-formats-pdf.md#converting-html-documents-to-pdf-documents)を参照してください）。

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-generatepdf-client.jar
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
 import java.io.File;
 import java.util.Properties;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient;
 import com.adobe.livecycle.generatepdf.client.HtmlToPdfResult;
 
 public class ConvertHTMLSOAP {
 
     public static void main(String[] args)
     {
         try{
         //Set connection properties required to invoke AEM Forms using SOAP mode
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory instance
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create a GeneratePdfServiceClient object
         GeneratePdfServiceClient pdfGenClient = new GeneratePdfServiceClient(myFactory);
 
         //Get an HTML document to convert to a PDF document a
         String inputFileName = "https://www.adobe.com";
 
          String securitySettings = "No Security";
         String fileTypeSettings = "Standard";
 
          //Convert HTML content to a PDF document
          HtmlToPdfResult result = pdfGenClient.htmlToPDF2(
                  inputFileName,
                  fileTypeSettings,
                  securitySettings,
                  null,
                 null);
 
          //Get the newly created document
          Document createdDocument = result.getCreatedDocument();
 
          //Save the PDF document as a PDF file
         createdDocument.copyToFile(new File("C:\\AdobeHTML.pdf"));
     }
     catch (Exception e) {
         System.out.println("Error OCCURRED: " + e.getMessage());
     }
     }
 }
```

## クイックスタート（SOAP モード）：Java API（SOAP モード）を使用して PDF ドキュメントを RTF ファイルに変換 {#quick-start-soap-mode-converting-a-pdf-document-to-an-rtf-file-using-the-java-api-soap-mode}

次のコードの例では、*Loan.pdf* という名前の PDF ドキュメントを *Loan.rtf* という名前の RTF ドキュメントに変換します（[PDF ドキュメントを非画像形式に変換](/help/forms/developing/converting-file-formats-pdf.md#converting-pdf-documents-to-non-image-formats)を参照してください）。

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-generatepdf-client.jar
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
 import java.io.File;
 import java.io.FileInputStream;
 import java.util.Properties;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.generatepdf.client.ConvertPDFFormatType;
 import com.adobe.livecycle.generatepdf.client.ExportPDFResult;
 import com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient;
 
 
 public class GeneratePdf_ExportPDFSOAP {
 
     public static void main(String[] args)
     {
         try{
             //Set connection properties required to invoke AEM Forms using SOAP mode
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory instance
             ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a GeneratePdfServiceClient object
             GeneratePdfServiceClient pdfGenClient = new GeneratePdfServiceClient(factory);
 
             //Get a PDF document to convert to an RTF document
             String inputFileName = "C:\\Adobe\\Loan.pdf.pdf";
             FileInputStream fileInputStream = new FileInputStream(inputFileName);
             Document inDoc = new Document(fileInputStream);
 
             //Convert a PDF document to a RTF document
             ExportPDFResult result = pdfGenClient.exportPDF2(
                 inDoc,
                 inputFileName,
                 ConvertPDFFormatType.RTF,
                 null);
 
          //Get the newly created RTF document
          Document createdDocument = result.getConvertedDocument();
 
          //Save the RTF file
         createdDocument.copyToFile(new File("C:\\Adobe\\Loan.pdf.rtf"));
         }
         catch (Exception e) {
             System.out.println("Error OCCURRED: " + e.getMessage());
         }
     }
 }
```
