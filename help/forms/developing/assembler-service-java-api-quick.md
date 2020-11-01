---
title: Assembler Service Java API QuickStart(SOAP)
seo-title: Assembler Service Java API QuickStart(SOAP)
description: Assembler Service Java API QuickStart(SOAP)
uuid: 33ad5f7a-4f4c-4e72-937d-85891498a80e
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: b7b17cf8-def5-4a77-a872-c1f286814881
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 0%

---


# Assembler Service Java API QuickStart(SOAP) {#assembler-service-java-api-quickstart-soap}

AssemblerサービスでJava API Quick開始(SOAP)を使用できます

[クイック開始（SOAPモード）:Java APIを使用したPDFドキュメントのアセンブリ](assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-using-the-java-api)

[クイック開始（SOAPモード）:Java APIを使用したPDFドキュメントのディスアセンブリ](assembler-service-java-api-quick.md#quick-start-soap-mode-disassembling-a-pdf-document-using-the-java-api)

[クイック開始（SOAPモード）:Java APIを使用した暗号化PDFドキュメントのアセンブリ](assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-an-encrypted-pdf-document-using-the-java-api)

[クイック開始（SOAPモード）:Java APIを使用したベイトナンバリングによるPDFドキュメントのアセンブリ](assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-pdf-document-with-bates-numbering-using-the-java-api)

[クイック開始（SOAPモード）:Java APIを使用した非インタラクティブPDFドキュメントのアセンブリ](assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-a-non-interactive-pdf-document-using-the-java-api)

[クイック開始（SOAPモード）:Java APIを使用したドキュメントがPDF/Aに準拠しているかどうかの判定](assembler-service-java-api-quick.md#quick-start-soap-mode-determining-whether-a-document-is-pdf-a-compliant-using-the-java-api)

[クイック開始（SOAPモード）:Java APIを使用したDDXドキュメントの検証](assembler-service-java-api-quick.md#quick-start-soap-mode-validating-ddx-documents-using-the-java-api)

[クイック開始（SOAPモード）:Java APIを使用したブックマークによるPDFドキュメントのアセンブリ](assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-documents-with-bookmarks-using-the-java-api)

[クイック開始（SOAPモード）:Java APIを使用したDDXドキュメントの動的な作成](assembler-service-java-api-quick.md#quick-start-soap-mode-dynamically-creating-a-ddx-document-using-the-java-api)

[クイック開始（SOAPモード）:Java APIを使用したPDFPortfolioのアセンブリ](assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-portfolios-using-the-java-api)

[クイック開始（SOAPモード）:Java APIを使用した複数のXDPフラグメントのアセンブリ](assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-multiple-xdp-fragments-using-the-java-api)

AEM Formsの操作は、AEM Formsで厳密に型指定されたAPIを使用して実行できます。接続モードはSOAPに設定する必要があります。

>[!NOTE]
>
>「AEM Formsでのプログラミング」にあるクイック開始は、JBoss Application ServerおよびMicrosoft WindowsオペレーティングシステムにデプロイされるFormsサーバーに基づいています。 ただし、UNIXなど別のオペレーティングシステムを使用している場合は、Windows固有のパスを、該当するオペレーティングシステムでサポートされているパスに置き換えます。 同様に、別のJ2EEアプリケーションサーバーを使用する場合は、有効な接続プロパティを指定していることを確認してください。 See [Setting connection properties](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## クイック開始（SOAPモード）:Java APIを使用したPDFドキュメントのアセンブリ {#quick-start-soap-mode-assembling-a-pdf-document-using-the-java-api}

次のJavaコードの例は、 *map.pdf* と ** directions.pdfという2つのPDFソースドキュメントを1つのPDFドキュメントに結合します。 単一のPDFドキュメントの名前は *AssemblerResultPDF.pdfです*。 DDXドキュメントの名前は *shell.xmlです*。 (「 [プログラムによるPDFドキュメントのアセンブリ](/help/forms/developing/assembling-pdf-documents.md#programmatically-assembling-pdf-documents)」を参照)。

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-assembler-client.jar
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
     *
     * The following XML represents the DDX document used in this quick start:
     * <?xml version="1.0" encoding="UTF-8"?>
     * <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     * <PDF result="out.pdf">
     * <PDF source="map.pdf" />
     * <PDF source="directions.pdf" />
     * </PDF>
     *</DDX>
     */
 import com.adobe.livecycle.assembler.client.*;
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class InvokeAssemblerSOAP
 {
     public static void main(String[] args) {
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
 
             //Create an AssemblerServiceClient object
             AssemblerServiceClient assemblerClient = new AssemblerServiceClient(myFactory);
 
             //Create a FileInputStream object based on an existing DDX file
             FileInputStream myDDXFile = new FileInputStream("C:\\shell.xml");
 
             //Create a Document object based on the DDX file
             Document myDDX = new Document(myDDXFile);
 
             //Create a Map object to store PDF source documents
             Map inputs = new HashMap();
             FileInputStream mySourceMap = new FileInputStream("C:\\map.pdf");
             FileInputStream mySourceOptions = new FileInputStream("C:\\directions.pdf");
 
             //Create a Document object based on the map.pdf source file
             Document myPDFMapSource = new Document(mySourceMap);
 
             //Create a Document object based on the directions.pdf source file
             Document myPDFOptionsSource = new Document(mySourceOptions);
 
             //Place two entries into the Map object
             inputs.put("map.pdf",myPDFMapSource);
             inputs.put("directions.pdf",myPDFOptionsSource);
 
             //Create an AssemblerOptionsSpec object
             AssemblerOptionSpec assemblerSpec = new AssemblerOptionSpec();
             assemblerSpec.setFailOnError(false);
 
             //Submit the job to Assembler service
             AssemblerResult jobResult = assemblerClient.invokeDDX(myDDX,inputs,assemblerSpec);
             java.util.Map allDocs = jobResult.getDocuments();
 
             //Retrieve the result PDF document from the Map object
             Document outDoc = null;
 
             //Iterate through the map object to retrieve the result PDF document
             for (Iterator i = allDocs.entrySet().iterator(); i.hasNext();) {
                 // Retrieve the Map object’s value
                 Map.Entry e = (Map.Entry)i.next();
 
                 //Get the key name as specified in the
                 //DDX document
                 String keyName = (String)e.getKey();
                 if (keyName.equalsIgnoreCase("out.pdf"))
                 {
                     Object o = e.getValue();
                     outDoc = (Document)o;
 
                     //Save the result PDF file
                     File myOutFile = new File("C:\\AssemblerResultPDF.pdf");
                     outDoc.copyToFile(myOutFile);
                 }
             }
         }catch (Exception e) {
             e.printStackTrace();
         }
     }
 }
```

## クイック開始（SOAPモード）:Java APIを使用したPDFドキュメントのディスアセンブリ {#quick-start-soap-mode-disassembling-a-pdf-document-using-the-java-api}

次のJavaコードの例は、AssemblerResultPDF.pdfというPDFドキュメントを *分解します*。 DDXドキュメントの名前は *shell_disassemble.xmlです*。 アセンブル解除された各PDFドキュメントには名前が付けられ `ResultPDF[Number].pdf`ます。 つまり、最初にデアセンブリされたPDFドキュメントの名前は *ResultPDF1.pdfです。* このコードの例で使用される *shell_disassemble.xml* DDXドキュメントについて詳しくは、「PDFドキュメントの [プログラムによるディスアセンブリ」を参照してください](/help/forms/developing/assembling-pdf-documents.md#programmatically-disassembling-pdf-documents)。

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-assembler-client.jar
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
     *
     * The following XML represents the DDX document used in this quick start:
     * <?xml version="1.0" encoding="UTF-8"?>
     *<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     * <PDFsFromBookmarks prefix="stmt">
     * <PDF source="AssemblerResultPDF.pdf"/>
     *</PDFsFromBookmarks>
     *</DDX>
     */
 import com.adobe.livecycle.assembler.client.*;
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class DisassemblePDFSOAP
 {
     public static void main(String[] args) {
         try{
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory instance
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create an AssemblerServiceClient object
             AssemblerServiceClient assemblerClient = new AssemblerServiceClient(myFactory);
 
             //Create a FileInputStream object based on an existing DDX file
             FileInputStream myDDXFile = new FileInputStream("C:\\shell_disassemble.xml");
 
             //Create a Document object based on the DDX file
             Document myDDX = new Document(myDDXFile);
 
             //Create a Map object to store PDF source documents
             Map inputs = new HashMap();
             FileInputStream mySourceMap = new FileInputStream("C:\\AssemblerResultPDF.pdf");
 
             //Create a Document object based on the map.pdf source file
             Document myPDFSource = new Document(mySourceMap);
 
             //Place two entries into the Map object
             inputs.put("AssemblerResultPDF.pdf",myPDFSource);
 
             //Create an AssemblerOptionsSpec object
             AssemblerOptionSpec assemblerSpec = new AssemblerOptionSpec();
             assemblerSpec.setFailOnError(false);
 
             //Submit the job to the Assembler service
             AssemblerResult jobResult = assemblerClient.invokeDDX(myDDX,inputs,assemblerSpec);
             java.util.Map allDocs = jobResult.getDocuments();
 
             //Retrieve the result PDF documents from the Map object
             Document outDoc = null;
             int index = 0;
 
             //Iterate through the map object to retrieve the result PDF document
             for (Iterator i = allDocs.entrySet().iterator(); i.hasNext();) {
                 // Retrieve the Map object’s value
                 Map.Entry e = (Map.Entry)i.next();
                 Object o = e.getValue();
 
                 //Cast the Object to a Document
                 //and save to a file
                 outDoc = (Document)o;
                 File myOutFile = new File("C:\\ResultPDF"+index +".pdf");
                 outDoc.copyToFile(myOutFile);
                 index++;
             }
             if (index > 0)
                 System.out.println("The PDF document was disassembled into "+index+" PDF documents.");
             else
                 System.out.println("The PDF document was not disassembled.");
 
         }catch (Exception e) {
             System.out.println("Error OCCURRED: "+e.getMessage());
         }
     }
 }
```

## クイック開始（SOAPモード）:Java APIを使用した暗号化PDFドキュメントのアセンブリ {#quick-start-soap-mode-assembling-an-encrypted-pdf-document-using-the-java-api}

次のJavaコードの例は、パスワードで暗号化されたPDFドキュメントをアセンブリします。 保護されていないPDFドキュメントの名前は *Loan.pdfです*。 DDXドキュメントの名前は *shell_Encrypt.xmlです*。 暗号化されたPDFドキュメントの名前は *AssemblerEncryptedPDF.pdfです*。 (暗号化されたPDFドキュメントの [アセンブリを参照](/help/forms/developing/assembling-pdf-documents.md#assembling-encrypted-pdf-documents))。

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-assembler-client.jar
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
     *
     * The following XML represents the DDX document used in this quick start:
     *<?xml version="1.0" encoding="UTF-8"?>
     * <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     * <PDF result="EncryptLoan.pdf" encryption="userProtect">
     * <PDF source="inDoc" />
     * </PDF>
     * <PasswordEncryptionProfile name="userProtect" compatibilityLevel="Acrobat7">
     * <OpenPassword>AdobeOpen</OpenPassword>
     * </PasswordEncryptionProfile>
     * </DDX>
     */
 
 import com.adobe.livecycle.assembler.client.*;
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class AssembleEncryptedDocumentSOAP
 {
     public static void main(String[] args) {
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
 
             //Create an AssemblerServiceClient object
             AssemblerServiceClient assemblerClient = new AssemblerServiceClient(myFactory);
 
             /*
              * Create a FileInputStream object based on an existing DDX file
              * This DDX document contains instructions to encrypt the PDF document
              */
             FileInputStream myDDXFile = new FileInputStream("C:\\shell_Encrypt.xml");
 
             //Create a Document object based on the DDX file
             Document myDDX = new Document(myDDXFile);
 
             //Reference an unsecured PDF document
             FileInputStream mySourceLoan = new FileInputStream("C:\\Loan.pdf");
 
             //Create a Document object based on the Loan.pdf source file
             Document myPDFLoanSource = new Document(mySourceLoan);
 
             //Create an AssemblerOptionsSpec object
             AssemblerOptionSpec assemblerSpec = new AssemblerOptionSpec();
             assemblerSpec.setFailOnError(false);
 
             //Submit the job to Assembler service
             Document jobResult = assemblerClient.invokeOneDocument(myDDX,myPDFLoanSource,assemblerSpec);
 
             //Create the output file
             File myOutFile = new File("C:\\AssemblerEncryptedPDF.pdf");
             jobResult.copyToFile(myOutFile);
 
         }catch (Exception e) {
             e.printStackTrace();
         }
     }
 }
```

## クイック開始（SOAPモード）:Java APIを使用したベイトナンバリングによるPDFドキュメントのアセンブリ {#quick-start-soap-mode-assembling-a-pdf-document-with-bates-numbering-using-the-java-api}

以下のJavaコードの例は、一意のページ識別子（ベート番号）を使用してPDFドキュメントをアセンブリしています。 DDXドキュメントの名前は *shell_Bates.xmlです*。 Assemblerサービスから返されるPDFドキュメントは、AssemblerResultBatesPDF.pdfというPDFファイルとして保存され *ます*。 (ベイツナンバリングを使用したドキュメントの [アセンブリを参照](/help/forms/developing/assembling-pdf-documents.md#assembling-documents-using-bates-numbering))。

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-assembler-client.jar
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
     *
     * The following XML represents the DDX document used in this quick start:
     * <?xml version="1.0" encoding="UTF-8"?>
     * <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     * <PDF result="out.pdf">
     * <Header>
     * <Center>
     * <StyledText>
     * <p font-size="20pt"><BatesNumber/></p>
     * </StyledText>
     * </Center>
     * </Header>
     * <PDF source="map.pdf" />
     * <PDF source="directions.pdf" />
     * </PDF>
     * </DDX>
     */
 
 import com.adobe.livecycle.assembler.client.*;
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 
 public class AssembleBatesNumberDocumentSOAP
 {
     public static void main(String[] args) {
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
 
             //Create an AssemblerServiceClient object
             AssemblerServiceClient assemblerClient = new AssemblerServiceClient(myFactory);
 
             //Create a FileInputStream object based on an existing DDX file
             FileInputStream myDDXFile = new FileInputStream("C:\\shell_Bates.xml");
 
             //Create a Document object based on the DDX file
             Document myDDX = new Document(myDDXFile);
 
             //Create a Map object to store PDF source documents
             Map<String, Object> inputs = new HashMap<String, Object>();
             FileInputStream mySourceMap = new FileInputStream("C:\\Adobe\map.pdf");
             FileInputStream mySourceOptions = new FileInputStream("C:\\Adobe\directions.pdf");
 
             //Create a Document object based on the map.pdf source file
             Document myPDFMapSource = new Document(mySourceMap);
 
             //Create a Document object based on the directions.pdf source file
             Document myPDFOptionsSource = new Document(mySourceOptions);
 
             //Place two entries into the Map object
             inputs.put("map.pdf",myPDFMapSource);
             inputs.put("directions.pdf",myPDFOptionsSource);
 
             //Create an AssemblerOptionsSpec object
             AssemblerOptionSpec assemblerSpec = new AssemblerOptionSpec();
             assemblerSpec.setFailOnError(false);
 
             //Set the initial number to 100
             assemblerSpec.setFirstBatesNumber(100);
 
             //Submit the job to Assembler service
             AssemblerResult jobResult = assemblerClient.invokeDDX(myDDX,inputs,assemblerSpec);
             java.util.Map allDocs = jobResult.getDocuments();
 
             //Retrieve the result PDF document from the Map object
             Document outDoc = null;
 
             //Iterate through the map object to retrieve the result PDF document
             for (Iterator i = allDocs.entrySet().iterator(); i.hasNext();) {
                 // Retrieve the Map object’s value
                 Map.Entry e = (Map.Entry)i.next();
 
                 //Get the key name as specified in the
                 //DDX document
                 String keyName = (String)e.getKey();
                 if (keyName.equalsIgnoreCase("out.pdf"))
                 {
                     //Cast the Object to a Document
                     Object o = e.getValue();
                     outDoc = (Document)o;
 
                     //Create the output file
                     File myOutFile = new File("C:\\AssemblerResultBatesPDF.pdf");
                     outDoc.copyToFile(myOutFile);
                 }
             }
             System.out.println("The PDF that contains Bates numbering was assembled.");
         }catch (Exception e) {
             e.printStackTrace();
         }
     }
 }
```

## クイック開始（SOAPモード）:Java APIを使用した非インタラクティブPDFドキュメントのアセンブリ {#quick-start-soap-mode-assembling-a-non-interactive-pdf-document-using-the-java-api}

以下のJavaコードの例は、非インタラクティブPDFドキュメントをアセンブリしています。 Assemblerサービスに渡されるインタラクティブPDFドキュメントの名前は *Loan.pdfです*。 DDXドキュメントの名前は *shell_XFA.xmlです*。 非インタラクティブPDFドキュメントは、AssembleNonInteractivePDF.pdfというPDFファイル *として保存されます*。 (非インタラクティブPDFドキュメントの [アセンブリを参照](/help/forms/developing/assembling-pdf-documents.md#assembling-non-interactive-pdf-documents))。

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-assembler-client.jar
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
     *
     * The following XML represents the DDX document used in this quick start:
     * <?xml version="1.0" encoding="UTF-8"?>
     * <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     * <PDF result="out.pdf">
     * <PDF source="inDoc"/>
     * <NoXFA/>
     * </PDF>
     * </DDX>
     */
 import com.adobe.livecycle.assembler.client.*;
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class AssembleNonInteractiveSOAP
 {
     public static void main(String[] args) {
         try{
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory instance
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create an AssemblerServiceClient object
             AssemblerServiceClient assemblerClient = new AssemblerServiceClient(myFactory);
 
             /*
              * Create a FileInputStream object based on an existing DDX file
              * This DDX document contains instructions to create
              * a non-interactive PDF document
              */
             FileInputStream myDDXFile = new FileInputStream("C:\\shell_XFA.xml");
 
             //Create a Document object based on the DDX file
             Document myDDX = new Document(myDDXFile);
 
             //Reference an interactive PDF document
             FileInputStream mySourceLoan = new FileInputStream("C:\\Adobe\Loan.pdf");
 
             //Create a Document object based on the Loan.pdf source file
             Document myPDFLoanSource = new Document(mySourceLoan);
 
             //Create an AssemblerOptionsSpec object
             AssemblerOptionSpec assemblerSpec = new AssemblerOptionSpec();
             assemblerSpec.setFailOnError(false);
 
             //Submit the job to Assembler service and get back a
             //non-interactive PDF document
             Document outDoc = assemblerClient.invokeOneDocument(myDDX,myPDFLoanSource,assemblerSpec);
 
             //Save the non-interactive PDF document
             File myOutFile = new File("C:\\AssembleNonInteractivePDF.pdf");
             outDoc.copyToFile(myOutFile);
 
         }catch (Exception e) {
             e.printStackTrace();
         }
     }
 }
 
 
```

## クイック開始（SOAPモード）:Java APIを使用したドキュメントがPDF/Aに準拠しているかどうかの判定 {#quick-start-soap-mode-determining-whether-a-document-is-pdf-a-compliant-using-the-java-api}

以下のJavaコードの例は、入力PDFドキュメントがPDF/Aに準拠しているかどうかを判定します。 Assemblerサービスに渡される入力PDFドキュメントの名前は *Loan.pdfです*。 DDXドキュメントの名前はshell_PDFA.xmlです。 Assemblerサービスから返され、入力PDFドキュメントがPDF/Aに準拠しているかどうかを指定するXMLドキュメントを、result.xmlというXMLファイルとして保存します。 このコードの例で使用される *shell_PDFA.xml* DDXドキュメントについて詳しくは、「ドキュメントがPDF/Aに準拠しているかどうかを [確認する」を参照してください](/help/forms/developing/assembling-pdf-documents.md#determining-whether-documents-are-pdf-a-compliant)。

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-assembler-client.jar
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
     *
     * This quick start validates the following DDX document:
     *<?xml version="1.0" encoding="UTF-8"?>
     *<DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     * <DocumentInformation source="Loan.pdf" result="Loan_result.xml">
     * <PDFAValidation compliance="PDF/A-1b" resultLevel="Detailed" ignoreUnusedResources="true" allowCertificationSignatures="true" />
     * </DocumentInformation>
     *</DDX>
     */
 
 import com.adobe.livecycle.assembler.client.*;
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class AssembleDeterminePDFASOAP
 {
     public static void main(String[] args) {
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
 
             //Create an AssemblerServiceClient object
             AssemblerServiceClient assemblerClient = new AssemblerServiceClient(myFactory);
 
             //Create a FileInputStream object based on an existing DDX file
             FileInputStream myDDXFile = new FileInputStream("C:\\shell_PDFA.xml");
 
             //Create a Document object based on the DDX file
             Document myDDX = new Document(myDDXFile);
 
             //Create a Map object to store PDF source documents
             Map inputs = new HashMap();
             FileInputStream mySourceMap = new FileInputStream("C:\\Adobe\Loan.pdf");
 
             //Create a Document object based on the map.pdf source file
             Document myPDFMapSource = new Document(mySourceMap);
 
             //Place two entries into the Map object
             inputs.put("Loan.pdf",myPDFMapSource);
 
             //Create an AssemblerOptionsSpec object
             AssemblerOptionSpec assemblerSpec = new AssemblerOptionSpec();
             assemblerSpec.setFailOnError(false);
 
             //Submit the job to Assembler service
             AssemblerResult jobResult = assemblerClient.invokeDDX(myDDX,inputs,assemblerSpec);
             java.util.Map allDocs = jobResult.getDocuments();
 
             //Retrieve the result PDF document from the Map object
             Document outDoc = null;
 
             //Iterate through the map object to retrieve the result XML
             //document that specifies if the input document is
             //PDF/A compliant
             for (Iterator i = allDocs.entrySet().iterator(); i.hasNext();) {
                 // Retrieve the Map object’s value
                 Map.Entry e = (Map.Entry)i.next();
 
                 //Get the key name as specified in the
                 //DDX document
                 String keyName = (String)e.getKey();
                 if (keyName.equalsIgnoreCase("Loan_result.xml"))
                 {
                     //Get the element value
                     Object o = e.getValue();
 
                     //Cast the Object to a Document
                     outDoc = (Document)o;
 
                     //Save the XML file
                     File myMXLFile = new File("C:\\Adobe\result.xml");
                     outDoc.copyToFile(myMXLFile);
                      }
                 }
 
             System.out.println("The results are written to result.xml.");
         }catch (Exception e) {
             e.printStackTrace();
         }
     }
 }
```

## クイック開始（SOAPモード）:Java APIを使用したDDXドキュメントの検証 {#quick-start-soap-mode-validating-ddx-documents-using-the-java-api}

次のJavaコードの例は、bookmarkDDX.xmlという名前のファイルに基づいてDDXドキュメントを検証し *ます*。 (DDXドキュメントの [検証を参照](/help/forms/developing/assembling-pdf-documents.md#validating-ddx-documents))。

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-assembler-client.jar
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
     *
     * This quick start validates the following DDX document:
     *&<?xml version="1.0" encoding="UTF-8"?>
     * <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     * <PDF result="out.pdf">
     * <PDF source="map.pdf" />
     * <PDF source="directions.pdf" />
     * </PDF>
     * </DDX>
     */
 import com.adobe.livecycle.assembler.client.*;
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class ValidateDDXSOAP
 {
     public static void main(String[] args) {
 
         boolean isValid = false;
            Document outLog = null;
 
         try{
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory instance
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create an AssemblerServiceClient object
             AssemblerServiceClient assemblerClient = new AssemblerServiceClient(myFactory);
 
             //Create a FileInputStream object based on an existing DDX file
             FileInputStream myDDXFile = new FileInputStream("C:\\bookmarkDDX.xml");
 
             //Create a Document object based on the DDX file
             Document myDDX = new Document(myDDXFile);
 
             //Create an AssemblerOptionsSpec object
             AssemblerOptionSpec assemblerSpec = new AssemblerOptionSpec();
             assemblerSpec.setValidateOnly(true);
             assemblerSpec.setLogLevel("FINE");
             assemblerSpec.setFailOnError(false);
 
             //Validate the DDX document
             AssemblerResult jobResult = assemblerClient.invokeDDX(myDDX,null,assemblerSpec);
             outLog = jobResult.getJobLog();
             isValid = true;
 
         }catch (Exception e) {
              if (e instanceof OperationException) {
                     OperationException oe = (OperationException) e;
                     outLog = oe.getJobLog();
                     File myOutFile = new File("C:\\test.xml");
                     outLog.copyToFile(myOutFile);
                 }
              e.printStackTrace();
          } finally {
                if (outLog != null) {
                    File myOutFile = new File("C:\\test.xml");
                    outLog.copyToFile(myOutFile);
               }
           if (isValid) {
                 // do something
           } else {
                // do something else
              }
           }
     }
 }
```

## クイック開始（SOAPモード）:Java APIを使用したブックマークによるPDFドキュメントのアセンブリ {#quick-start-soap-mode-assembling-pdf-documents-with-bookmarks-using-the-java-api}

次のJavaコードの例は、しおりを含むPDFドキュメントをアセンブリしています。 DDXドキュメントの名前は *bookmarkDDX.xmlです*。 PDFドキュメントに追加するブックマークを示すブックマークXMLドキュメントの名前は、bookmarks.xmlです。 結果のPDFドキュメントは、AssemblerResultBookmarks.pdfというPDFファイルとして保存されます。 (「しおりを使用したPDFドキュメントの [アセンブリ](/help/forms/developing/assembling-pdf-documents.md#assembling-pdf-documents-with-bookmarks)」を参照)。

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-assembler-client.jar
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
     *
     * * This quick start uses the following DDX document:
     * <?xml version="1.0" encoding="UTF-8"?>
     * <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     * <PDF result="FinalDoc.pdf">
     * <PDF source="Loan.pdf">
     * <Bookmarks source="doc2" />
     * </PDF>
     * </PDF>
     * </DDX>
     *
     * This quick start also uses the following bookmarks XML
     * to assemble a PDF document containing bookmarks:
     * <?xml version="1.0" encoding="UTF-8"?>
     * <Bookmarks xmlns="https://ns.adobe.com/pdf/bookmarks" version="1.0">
     * <Bookmark>
     * <Action>
     * <Launch NewWindow="true">
     * <File Name="C:\Adobe\LoanDetails.pdf" />
     * </Launch>
     * </Action>
     * <Title>Open the Loan document</Title>
     * </Bookmark>
     * <Bookmark>
     * <Action>
     * <Launch>
     * <Win Name="C:\WINDOWS\notepad.exe" />
     * </Launch>
     * </Action>
     * <Title>Launch NotePad</Title>
     * </Bookmark>
     * </Bookmarks>
     *
     */
     import com.adobe.livecycle.assembler.client.*;
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class AssembleBookmarksSOAP
 {
     public static void main(String[] args) {
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
 
             //Create an AssemblerServiceClient object
             AssemblerServiceClient assemblerClient = new AssemblerServiceClient(myFactory);
 
             //Create a FileInputStream object based on an existing DDX file
             FileInputStream myDDXFile = new FileInputStream("C:\\bookmarkDDX.xml");
 
             //Create a Document object based on the DDX file
             Document myDDX = new Document(myDDXFile);
 
             //Create a Map object to store an input PDF document and a Bookmark
             //XML document
             Map inputs = new HashMap();
             FileInputStream mySourceMap = new FileInputStream("C:\\Loan.pdf");
             FileInputStream bookmarkInfo = new FileInputStream("C:\\bookmarks.xml");
 
             //Create a Document object based on the Loan.pdf source file
             Document myPDFMapSource = new Document(mySourceMap);
 
             //Create a Document object based on the bookmarks.xml file
             Document myBookmarkXML= new Document(bookmarkInfo);
 
             //Place two entries into the Map object
             inputs.put("Loan.pdf",myPDFMapSource);
             inputs.put("doc2",myBookmarkXML);
 
             //Create an AssemblerOptionsSpec object
             AssemblerOptionSpec assemblerSpec = new AssemblerOptionSpec();
             assemblerSpec.setFailOnError(false);
 
             //Submit the job to Assembler service
             AssemblerResult jobResult = assemblerClient.invokeDDX(myDDX,inputs,assemblerSpec);
             java.util.Map allDocs = jobResult.getDocuments();
 
             //Retrieve the result PDF document from the Map object
             Document outDoc = null;
 
             //Iterate through the map object to retrieve the result PDF document
             for (Iterator i = allDocs.entrySet().iterator(); i.hasNext();) {
                 // Retrieve the Map object’s value
                 Map.Entry e = (Map.Entry)i.next();
 
                 //Get the key name as specified in the
                 //DDX document
                 String keyName = (String)e.getKey();
                 if (keyName.equalsIgnoreCase("FinalDoc.pdf"))
                 {
                     Object o = e.getValue();
                     outDoc = (Document)o;
 
                     //Save the result PDF file
                     File myOutFile = new File("C:\\Adobe\Assembler\Output\AssemblerResultBookmarks.pdf");
                     outDoc.copyToFile(myOutFile);
                 }
             }
         }catch (Exception e) {
             e.printStackTrace();
         }
     }
 }
 
```

## クイック開始（SOAPモード）:Java APIを使用したDDXドキュメントの動的な作成 {#quick-start-soap-mode-dynamically-creating-a-ddx-document-using-the-java-api}

以下のJavaコードの例を使用すると、PDFドキュメントをディスアセンブリするDDXドキュメントを動的に作成できます。 入力PDFドキュメントのレベル1のブックマークごとに、新しいPDFドキュメントが作成されます。 次のコードの例には、2つのユーザー定義メソッドが含まれています。

* `createDDX`:Assemblerサービスに送信されるDDXドキュメントを表す `org.w3c.dom.Document` オブジェクトを作成します。 このユーザー定義メソッドは、 `org.w3c.dom.Document` オブジェクトを返します。
* `convertDDX`:オブジェクトを `org.w3c.dom.Document` オブジェクトに変換し `com.adobe.idp.Document` ます。 このメソッドは、 `org.w3c.dom.Document` オブジェクトを入力パラメーターとして受け取り、オブジェクトを返し `com.adobe.idp.Document` ます。

   このクイック開始では、これらの両方のメソッドが呼び出されます。 (DDXドキュメントの [動的な作成を参照](/help/forms/developing/assembling-pdf-documents.md#dynamically-creating-ddx-documents))。

```java
/*
 * This Java Quick Start uses the SOAP mode and contains the following JAR files
 * in the class path:
 * 1. adobe-assembler-client.jar
 * 2. adobe-livecycle-client.jar
 * 3. adobe-usermanager-client.jar
 * 4. adobe-utilities.jar
 * 5. jboss-client.jar (use a different JAR file if the forms server is not deployed
 * on JBoss)
 * 6. activation.jar (required for SOAP mode)
 * 7. axis.jar (required for SOAP mode)
 * 8. commons-codec-1.3.jar (required for SOAP mode)
 * 9. commons-collections-3.1.jar (required for SOAP mode)
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
 *
 * The following XML represents the DDX document created in this quick start:
 * <?xml version="1.0" encoding="UTF-8"?>
 * <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
 * <PDF result="out.pdf">
 * <PDF source="inDoc"/>
 * <NoXFA/>
 * </PDF>
 * </DDX>
 */
import com.adobe.livecycle.assembler.client.*;
import java.util.*;
import java.io.ByteArrayOutputStream;
import java.io.File;
import java.io.FileInputStream;
import javax.xml.parsers.DocumentBuilder;
import javax.xml.parsers.DocumentBuilderFactory;
import javax.xml.transform.Transformer;
import javax.xml.transform.TransformerFactory;
import javax.xml.transform.dom.DOMSource;
import javax.xml.transform.stream.StreamResult;
import org.w3c.dom.Element;
import com.adobe.idp.Document;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
public class AssemblePDFWithDynamicDDXSOAP {
 public static void main(String[] args) {
   try {
    //Set connection properties required to invoke AEM Forms using SOAP mode
    Properties connectionProps = new Properties();
    connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT,
     "https://'[server]:[port]'");
    connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL, ServiceCl ientFactoryProperties.DSC_SOAP_PROTOCOL);
    connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE,
     "JBoss");
    connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME,
     "administrator");
    connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD,
     "password");
    //Create a ServiceClientFactory instance
    ServiceClientFactory myFactory =
     ServiceClientFactory.createInstance(connectionProps);
    //Create an AssemblerServiceClient object
    AssemblerServiceClient assemblerClient = new AssemblerServiceClient(myFactory);
    //Dynamically create a DDX document
    org.w3c.dom.Document myDDX = createDDX();
    //Covert the DDX document to a com.adobe.idp.Document instance
    com.adobe.idp.Document ddx = convertDDX(myDDX);
    //Create a Map object to store PDF source documents
    Map inputs = new HashMap();
    FileInputStream mySourceMap = new FileInputStream("C:\\AssemblerResultPDF.pdf");
    //Create a Document object based on the map.pdf source file
    Document myPDFSource = new Document(mySourceMap);
    //Place the entry into the Map object
    inputs.put("AssemblerResultPDF.pdf", myPDFSource);
    //Create an AssemblerOptionsSpec object
    AssemblerOptionSpec assemblerSpec = new AssemblerOptionSpec();
    assemblerSpec.setFailOnError(false);
    //Submit the job to Assembler service and use the dynamically created DDX document
    AssemblerResult jobResult = assemblerClient.invokeDDX(ddx, inputs, assemblerSpec);
    java.util.Map allDocs = jobResult.getDocuments();
    //Retrieve the result PDF document from the Map object
    Document outDoc = null;
    int index = 1;
    //Iterate through the map object to retrieve the result PDF documents
    for (Iterator i = allDocs.entrySet().iterator(); i.hasNext();) {
     // Retrieve the Map object's value
     Map.Entry e = (Map.Entry) i.next();
     Object o = e.getValue();
     //Cast the Object to a Document
     //and save to a file
     outDoc = (Document) o;
     File myOutFile = new File("C:\\ResultPDF" + index + ".pdf");
     outDoc.copyToFile(myOutFile);
     index++;
    }
   } catch (Exception e) {
    e.printStackTrace();
   }
  }
  //Creates a DDX document using an org.w3c.dom.Document object
 private static org.w3c.dom.Document createDDX() {
   org.w3c.dom.Document document = null;
   try {
    //Create DocumentBuilderFactory and DocumentBuilder objects
    DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
    DocumentBuilder builder = factory.newDocumentBuilder();
    //Create a new Document object
    document = builder.newDocument();
    //Create the root element and append it to the XML DOM
    Element root = (Element) document.createElement("DDX");
    root.setAttribute("xmlns", "https://ns.adobe.com/DDX/1.0/");
    document.appendChild(root);
    //Create the PDFsFromBookmarks element
    Element PDFsFromBookmarks =
     (Element) document.createElement("PDFsFromBookmarks");
    PDFsFromBookmarks.setAttribute("prefix", "stmt");
    root.appendChild(PDFsFromBookmarks);
    //Create the PDF element
    Element PDF = (Element) document.createElement("PDF");
    PDF.setAttribute("source", "AssemblerResultPDF.pdf");
    PDFsFromBookmarks.appendChild(PDF);
   } catch (Exception e) {
    System.out.println("The following exception occurred: " + e.getMessage());
   }
   return document;
  }
  //Converts an org.w3c.dom.Document object to a
  //com.adobe.idp.Document object
 private static Document convertDDX(org.w3c.dom.Document myDOM) {
  byte[] mybytes = null;
  try {
   //Create a Java Transformer object
   TransformerFactory transFact = TransformerFactory.newInstance();
   Transformer transForm = transFact.newTransformer();
   //Create a Java ByteArrayOutputStream object
   ByteArrayOutputStream myOutStream = new ByteArrayOutputStream();
   //Create a Java Source object
   javax.xml.transform.dom.DOMSource myInput = new DOMSource(myDOM);
   //Create a Java Result object
   javax.xml.transform.stream.StreamResult myOutput = new StreamResult(myOutStream);
   //Populate the Java ByteArrayOutputStream object
   transForm.transform(myInput, myOutput);
   // Get the size of the ByteArrayOutputStream buffer
   int myByteSize = myOutStream.size();
   //Allocate myByteSize to the byte array
   mybytes = new byte[myByteSize];
   //Copy the content to the byte array
   mybytes = myOutStream.toByteArray();
  } catch (Exception e) {
   System.out.println("The following exception occurred: " + e.getMessage());
  }
  //Create a com.adobe.idp.Document object and copy the
  //contents of the byte array
  Document myDocument = new Document(mybytes);
  return myDocument;
 }
}
```

## クイック開始（SOAPモード）:Java APIを使用したPDFPortfolioのアセンブリ {#quick-start-soap-mode-assembling-pdf-portfolios-using-the-java-api}

以下のJavaコードの例を使用して、PDFポートフォリオを作成します。 PDFポートフォリオは、AssemblerResultPortfolio.pdfというPDFファイル *として保存されます*。 (PDFPortfolioの [アセンブリを参照](/help/forms/developing/assembling-pdf-documents.md#assembling-pdf-portfolios))。

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-assembler-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the forms server is not deployed
     * on JBoss)
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
     *
     * This is the DDX file used to create a PDF portfolio:
     * <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     * <PDF result="portfolio1.pdf">
     * <Portfolio>
     * <Navigator source="myNavigator">
     * <Resource name="navigator/image.xxx" source="myImage.png"/>
     * </Navigator>
     * </Portfolio>
     * <PackageFiles source="dog1"  >
     * <FieldData name="X">72</FieldData>
     * <FieldData name="Y">72</FieldData>
     * <File filename="saint_bernard.jpg" mimetype="image/jpeg"/>
     * </PackageFiles>
     * <PackageFiles source="dog2"  >
     * <FieldData name="X">120</FieldData>
     * <FieldData name="Y">216</FieldData>
     * <File filename="greyhound.pdf"/>
     * </PackageFiles>
     * </PDF>
     * </DDX>
     */
 import com.adobe.livecycle.assembler.client.*;
 
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class CreatePDFPortfolioSOAP {
     public static void main(String[] args) {
         try{
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory instance
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create an AssemblerServiceClient object
             AssemblerServiceClient assemblerClient = new AssemblerServiceClient(myFactory);
 
             //Create a FileInputStream object based on an existing DDX file
             FileInputStream myDDXFile = new FileInputStream("C:\\Adobe\portfolioAssembly.xml");
             FileInputStream myNavFile = new FileInputStream("C:\\Adobe\AdobeOnImage.nav");
 
             //Create a Document object based on the DDX file
             Document myDDX = new Document(myDDXFile);
             Document myNav = new Document(myNavFile);
 
             //Create a Map object to store PDF source documents
             Map<String,Object> input = new HashMap<String, Object>();
             FileInputStream mySourceNavImage = new FileInputStream("C:\\Adobe\myImage.png");
             FileInputStream mySourceDog1 = new FileInputStream("C:\\Adobe\saint_bernard.jpg");
             FileInputStream mySourceDog2 = new FileInputStream("C:\\Adobe\greyhound.pdf");
 
             //Create a Document object based on the myImage.png source file
             Document myPDFNavImageSource = new Document(mySourceNavImage);
 
             //Create a Document object based on the MyFirstFile.pdf source file
             Document myPDFDog1Source = new Document(mySourceDog1);
 
             //Create a Document object based on the MySecondFile.txt source file
             Document myPDFDog2Source = new Document(mySourceDog2);
 
             //Place two entries into the Map object
             input.put("myNavigator", myNav);
             input.put("myImage.png",myPDFNavImageSource);
             input.put("dog1",myPDFDog1Source);
             input.put("dog2",myPDFDog2Source);
 
             //Create an AssemblerOptionsSpec object
             AssemblerOptionSpec assemblerSpec = new AssemblerOptionSpec();
             assemblerSpec.setFailOnError(false);
 
             //Submit the job to Assembler service
             AssemblerResult jobResult = assemblerClient.invokeDDX(myDDX,input,assemblerSpec);
             Map<String,Document> allDocs = jobResult.getDocuments();
 
             //Retrieve the result PDF document from the Map object
             Document outDoc = null;
 
             //Iterate through the map object to retrieve the result PDF document
             for (Iterator<Map.Entry<String,Document>> i = allDocs.entrySet().iterator(); i.hasNext();) {
                 // Retrieve the Map object?s value
                 Map.Entry<String,Document> e = (Map.Entry<String,Document>)i.next();
 
                 //Get the key name as specified in the
                 //DDX document
                 String keyName = (String)e.getKey();
                 if (keyName.equalsIgnoreCase("portfolio1.pdf"))
                 {
                     Object o = e.getValue();
                     outDoc = (Document)o;
 
                     //Save the result PDF file
                     File myOutFile = new File("C:\\Adobe\AssemblerResultPortfolio.pdf");
                     outDoc.copyToFile(myOutFile);
                 }
             }
 
         }catch (Exception e) {
             e.printStackTrace();
         }
     }
 }
 
 
```

## クイック開始（SOAPモード）:Java APIを使用した複数のXDPフラグメントのアセンブリ {#quick-start-soap-mode-assembling-multiple-xdp-fragments-using-the-java-api}

以下のJavaコードの例を使用することで、次のXDPファイルに基づいてXDPフラグメントをアセンブルできます。 *tuc018_template_flowed.xdp*、 *tuc018_contact.xdp*、および* tuc018_patient.xdp*。 すべてのフラグメントを含むアセンブリ済みのXDPドキュメントは、AssemblerResultXDP.xdpという名前のXDPファイル *として保存されます*。 (複数のXDPフラグメントの [アセンブリを参照](/help/forms/developing/assembling-pdf-documents.md#assembling-multiple-xdp-fragments))。

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-assembler-client.jar
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
     *
     * The following XML represents the DDX document used in this quick start:
     * <?xml version="1.0" encoding="UTF-8"?>
     * <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     * <XDP result="tuc018result.xdp">
     * <XDP source="tuc018_template_flowed.xdp">
     * <XDPContent insertionPoint="ddx_fragment" source="tuc018_contact.xdp" fragment="subPatientContact" required="false"/>
     * <XDPContent insertionPoint="ddx_fragment" source="tuc018_patient.xdp" fragment="subPatientPhysical" required="false"/>
     * <XDPContent insertionPoint="ddx_fragment" source="tuc018_patient.xdp" fragment="subPatientHealth" required="false"/>
     * </XDP>
     * </XDP>
     * </DDX>
     */
 import com.adobe.livecycle.assembler.client.*;
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class AssembleFragmentsSOAP
 {
     public static void main(String[] args) {
         try{
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory instance
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create an AssemblerServiceClient object
             AssemblerServiceClient assemblerClient = new AssemblerServiceClient(myFactory);
 
             //Create a FileInputStream object based on an existing DDX file
             FileInputStream myDDXFile = new FileInputStream("C:\\Adobe\fragmentDDX.xml");
 
             //Create a Document object based on the DDX file
             Document myDDX = new Document(myDDXFile);
 
             //Create a Map object to store the input XDP files
             Map inputs = new HashMap();
             FileInputStream inSource = new FileInputStream("C:\\Adobe\tuc018_template_flowed.xdp");
             FileInputStream inFragment1 = new FileInputStream("C:\\Adobe\tuc018_contact.xdp");
             FileInputStream inFragment2 = new FileInputStream("C:\\Adobe\tuc018_patient.xdp");
 
             //Create a Document object
             Document myMapSource = new Document(inSource);
 
             //Create a Document object
             Document inFragment1Doc = new Document(inFragment1);
 
             //Create a Document object
             Document inFragment2Doc = new Document(inFragment2);
 
             //Place all of the XDP files into the MAP
             inputs.put("tuc018_template_flowed.xdp",myMapSource);
             inputs.put("tuc018_contact.xdp",inFragment1Doc);
             inputs.put("tuc018_patient.xdp",inFragment2Doc);
 
 
             //Create an AssemblerOptionsSpec object
             AssemblerOptionSpec assemblerSpec = new AssemblerOptionSpec();
             assemblerSpec.setFailOnError(false);
 
             //Submit the job to Assembler service
             AssemblerResult jobResult = assemblerClient.invokeDDX(myDDX,inputs,assemblerSpec);
             java.util.Map allDocs = jobResult.getDocuments();
 
             //Retrieve the result PDF document from the Map object
             Document outDoc = null;
 
             //Iterate through the map object to retrieve the result XDP document
             for (Iterator i = allDocs.entrySet().iterator(); i.hasNext();) {
                 // Retrieve the Map object’s value
                 Map.Entry e = (Map.Entry)i.next();
 
                 //Get the key name as specified in the
                 //DDX document
                 String keyName = (String)e.getKey();
                 if (keyName.equalsIgnoreCase("tuc018result.xdp"))
                 {
                     Object o = e.getValue();
                     outDoc = (Document)o;
 
                     //Save the result XDP file
                     File myOutFile = new File("C:\\AssemblerResultXDP.xdp");
                     outDoc.copyToFile(myOutFile);
                 }
             }
         }catch (Exception e) {
             e.printStackTrace();
         }
     }
 }
```

## クイック開始（SOAPモード）:Java APIを使用したPDFドキュメントの修正 {#quick-start-soap-mode-redacting-a-pdf-document-using-the-java-api}

次のコードの例は、を使用してPDFドキュメントを修正し `PDFUtility`ます。

>[!NOTE]
>
>`PDFUtility` acrobatを使用して修正対象としてマークされたPDFのみを修正できます。

```java
/*
 * This Java Quick Start uses the SOAP mode and contains the following JAR files
 * in the class path:
 * 1. adobe-pdfutility-client.jar
 * 2. adobe-livecycle-client.jar
 * 3. adobe-usermanager-client.jar
 * 4. adobe-utilities.jar
 * 5. jboss-client.jar (use a different JAR file if AEM Forms is not deployed
 * on JBoss)
 *
 * These JAR files are located in the following path:
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/common
 *
 * The adobe-utilities.jar file is located in the following path:
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/jboss
 *
 * The jboss-client.jar file is located in the following path:
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/jboss/bin/client
 *
 * If you want to invoke a remote AEM Forms instance and there is a
 * firewall between the client application and AEM Forms, then it is
 * recommended that you use the SOAP mode. When using the SOAP mode,
 * you have to include additional JAR files located in the following
 * path
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/thirdparty
 *
 * For information about the SOAP
 * mode and the additional JAR files that need to be included,
 * see "Setting connection properties" in Programming
 * with AEM Forms
 *
 * For complete details about the location of the AEM Forms JAR files,
 * see "Including AEM Forms library files" in Programming
 * with AEM Forms
 */

import java.util.*;
import com.adobe.livecycle.pdfutility.client.*;
import java.io.*;
import com.adobe.idp.Document;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;

public class RedactPDF
{
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

            // Create a ServiceClientFactory object
            ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);

            // Create a PDF Utility client
            PDFUtilityServiceClient pdfUt = new PDFUtilityServiceClient(myFactory);

            // Specify a PDF document to Redact
            FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\\RedactMarked.pdf");
            Document inDoc = new Document(fileInputStream);
            RedactionOptionSpec spec = new RedactionOptionSpec();

            // Convert the PDF document to redact
            RedactionResult redRes = pdfUt.redact(inDoc,spec);

            Document redactPDF = redRes.getDocument();

            //Save the returned Document object as an XDP file
            File redactedFile = new File("C:\\Adobe\\Redacted.pdf");
            redactPDF.copyToFile(redactedFile);
        }
        catch (Exception e)
        {
            e.printStackTrace();
        }
    }
}
```

