---
title: Backup and Restore サービス API のクイックスタート
seo-title: Backup and Restore Service APIQuick Starts
description: Backup and Restore サービス API のクイックスタート
uuid: c3992be2-ceb4-480d-9c8f-71eb0ea66dde
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 813162be-dbf5-4dc1-80ff-e37dbc25ef60
role: Developer
exl-id: ae17fd3a-0ba4-4a00-907b-811e500b0e14
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 100%

---

# Backup and Restore サービス API のクイックスタート {#backup-and-restore-service-apiquick-starts}

**このドキュメントのサンプルと例は、JEE 環境の AEM Forms のみを対象としています。**

Java API クイックスタート（SOAP）は、Backup and Restore サービス API で使用できます。

[クイックスタート：Java API（SOAP）を使用したバックアップモードの開始](backup-restore-service-api-quick.md#quick-start-soap-mode-entering-backup-mode-using-the-java-api)

[クイックスタート：Java API（SOAP）を使用したバックアップモードの終了](backup-restore-service-api-quick.md#quick-start-soap-mode-leaving-backup-mode-using-the-java-api)

AEM Forms の操作は、AEM Forms の厳密に型指定された API を使用して実行できます。接続モードは、SOAP に設定する必要があります。

>[!NOTE]
>
>AEM Forms によるプログラミングにあるクイックスタートは、Forms オペレーティングシステムに基づいています。ただし、UNIX などの別のオペレーティングシステムを使用している場合は、Windows 固有のパスを、該当するオペレーティングシステムでサポートされているパスに置き換えます。同様に、別の J2EE アプリケーションサーバーを使用している場合は、有効な接続プロパティを必ず指定してください。[接続プロパティの設定](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)を参照してください。

## クイックスタート（SOAP モード）：Java API を使用したバックアップモードの開始 {#quick-start-soap-mode-entering-backup-mode-using-the-java-api}

次の Java コード例では、2 時間にわたり、一意のラベルが指定されたバックアップモードになります。バックアップ時間の経過後、またはバックアップモードが明示的に終了された場合、Forms サーバーはグローバルドキュメントストレージからのファイルのパージを再開します。（[Forms サーバーでのバックアップモードの開始](/help/forms/developing/preparing-aem-forms-backup.md#entering-backup-mode-on-the-forms-server)を参照。）

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-backup-restore-client-sdk.jar
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
 import java.util.Properties;
 
 import com.adobe.idp.backup.dsc.client.BackupServiceClient;
 import com.adobe.idp.backup.dsc.service.BackupModeEntryResult;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class BackupRestoreEnter
 {
     public static void main(String[] args)
     {
         try
         {
             // Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL, ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME,"administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             // Create a ServiceClientFactory instance
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             // Create a BackupService client object
             BackupServiceClient backup = new BackupServiceClient(myFactory);
 
             // Specify a generic label, 120 minutes to perform the backup,
             // and not to provide continous backup mode coverage (used for snapshot backups)
             String backUpLabel = new String("Snapshot2008July01");
             int minsInBackupMode = 120;
             boolean continousCoverage = false;
 
 
             // Enter backup mode on the forms server server
             BackupModeEntryResult backupResult = backup.enterBackupMode(backUpLabel,minsInBackupMode, continousCoverage);
 
             // Get information from entering backup mode ontheforms server server.
             if (backupResult != null)
             {
                 System.out.println("Start time is: " + backupResult.getStartTime());
                 System.out.println("Backup Current ID is: " + backupResult.getId());
                 System.out.println("Backup Previous ID is: " + backupResult.getPreviousReservationId());
                 System.out.println("Backup Label is: " + backupResult.getLabel());
                 System.out.println("Backup Time to complete is: " + backupResult.getReservationTimeout());
             }
             else
             {
                 System.out.println("Could not enter backup mode.");
             }
 
         }
         catch (Exception e)
         {
             e.printStackTrace();
         }
         return;
     }
 }
 
```

## クイックスタート（SOAP モード）：Java API を使用したバックアップモードの終了 {#quick-start-soap-mode-leaving-backup-mode-using-the-java-api}

次の Java コード例では、Forms サーバーでバックアップモードが明示的に終了され、グローバルドキュメントストレージからのファイルのパージを再開します。（[Forms サーバーでのバックアップモードの終了](/help/forms/developing/preparing-aem-forms-backup.md#leaving-backup-mode-on-the-forms-server)を参照。）

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-backup-restore-client-sdk.jar
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
 import java.util.Properties;
 
 import com.adobe.idp.backup.dsc.client.BackupServiceClient;
 import com.adobe.idp.backup.dsc.service.BackupModeResult;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class BackupRestoreLeave
 {
 
     public static void main(String[] args)
     {
         try
         {
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'server':`port`");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL, ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME,"administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             // Create a ServiceClientFactory instance
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             // Create a BackupService object
             BackupServiceClient backup = new BackupServiceClient(myFactory);
 
             // Leave backup mode on the forms server
             BackupModeResult leaveBackupResult = backup.leaveBackupMode();
 
             //Get result information from leaving backup mode
             if (leaveBackupResult != null)
             {
                 System.out.println("Backup Mode ID is : " + leaveBackupResult.getId());
             }
             else
             {
                 System.out.println("Forms server is not in backup mode.");
             }
 
         }
         catch (Exception e)
         {
             e.printStackTrace();
         }
         return;
     }
 }
 
```
