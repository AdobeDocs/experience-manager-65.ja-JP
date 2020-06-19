---
title: AEM Forms と Adobe LiveCycle の接続
seo-title: AEM Forms と Adobe LiveCycle の接続
description: AEM LiveCycle コネクターを使用すると、AEM アプリケーションやワークフローからLiveCycle ES4 Document Services を呼び出すことができます。
seo-description: AEM LiveCycle コネクターを使用すると、AEM アプリケーションやワークフローからLiveCycle ES4 Document Services を呼び出すことができます。
uuid: 7dc9d5ec-7b19-4d93-936d-81ceb45dfffa
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 7e404b45-1302-4dd1-b3c9-3f47fedb5f94
translation-type: tm+mt
source-git-commit: b703c59d7d913fc890c713c6e49e7d89211fd998
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 93%

---


# AEM Forms と Adobe LiveCycle の接続 {#connecting-aem-forms-with-adobe-livecycle}

Adobe Experience Manager (AEM) LiveCycle Connector を使用し、AEM Web アプリとワークフローから Adobe LiveCycle ES4 Document Services を呼び出すことができます。LiveCycle はリッチクライアント SDK を提供します。これにより、クライアントアプリケーションは Java API を使用して LiveCycle サービスを開始します。AEM LiveCycle Connector は OSGi 環境でこれらの API の使用を簡素化します。

## AEM サーバーの Adobe LiveCycle への接続 {#connecting-aem-server-to-adobe-livecycle}

AEM LiveCycle Connector は「[AEM Forms アドオンパッケージ](/help/forms/using/installing-configuring-aem-forms-osgi.md)」の一部です。AEM Forms アドオンパッケージをインストールしたら、次の手順を実行して、LiveCycle サーバーの詳細を AEM Web Console に追加します。

1. AEM Web Console Configuration Manager で、Adobe LiveCycle Client SDK Configuration Component を見つけます。
1. コンポーネントをクリックして、構成サーバーの URL、ユーザー名、パスワードを編集します。
1. 設定を確認し、「**保存**」をクリックします。

プロパティは説明がなくても分かりますが、重要なプロパティは次のとおりです。

* **サーバー URL** - LiveCycle Server への URL を指定します。LiveCycleとAEM間でHTTPS経由で通信する場合は、AEMを次のJVMと開始します

   ```
   argument
    -Djavax.net.ssl.trustStore=<<em>path to LC keystore</em>>
   ```

   option.

* **ユーザー名** - AEM と LiveCycle 間の通信を確立するのに使用するアカウントのユーザー名を指定します。アカウントは、Document Services の開始を許可されている LiveCycle ユーザーアカウントです。
* **パスワード** - パスワードを指定します。
* **サービス名** - 「Username」と「Password」フィールドで入力するユーザー資格情報を使用して開始されるサービスを指定します。デフォルトでは、LiveCycle サービスを開始する間に資格情報は渡されません。

## Document Services の開始 {#starting-document-services}

クライアントアプリケーションは、Java API、 Web サービス、Remoting、REST を使用して LiveCycle サービスをプログラムで開始することができます。Java クライアントの場合、アプリケーションは LiveCycle SDK を使用できます。LiveCycle SDK は、これらのサービスをリモートで開始する Java API を提供します。例えば、Microsoft Word ドキュメントを PDF に変換するには、クライアントは GeneratePDFService を開始します。呼び出しのフローは次の手順から成ります。

1. ServiceClientFactory インスタンスを作成します。
1. 各サービスがクライアントクラスを提供します。サービスを開始するには、サービスのクライアントインスタンスを作成します。
1. サービスを開始し、結果を処理します。

AEM LiveCycle Connector は、標準的な OSGi の方法を使ってアクセスできる OSGi サービスとしてこれらのクライアントインスタンスを公開して、フローを簡素化します。LiveCycle Connectorには次の機能が用意されています。

* Client instances as OSGi Service: The clients packaged as OSGI bundles are listed in the [Document Services list](/help/forms/using/aem-livecycle-connector.md#p-document-services-list-p) section. 各クライアント jar は、OSGi Service Registry を使用する OSGi サービスとしてクライアントインスタンスを登録します。
* ユーザー資格情報の伝播：LiveCycle サーバーに接続するために必要な接続の詳細情報は、一元的に管理されます。
* ServiceClientFactory サービス：プロセスを開始するために、クライアントアプリケーションは ServiceClientFactory インスタンスにアクセスできます。

### Service References を介した OSGi Service Registry からの開始 {#starting-via-service-references-from-osgi-service-registry}

公開されたサービスを AEM の中から開始するには、次の手順を実行します。

1. Maven 依存性を判定します。maven pom.xml ファイルで、必要なクライアント jar に依存性を追加します。少なくとも adobe-livecycle-client jar および adobe-usermanager-client jar に依存性を追加する必要があります。

   ```xml
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-livecycle-client</artifactId>
     <version>11.0.0</version>
   </dependency>
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-usermanager-client</artifactId>
     <version>11.0.0</version>
   </dependency>
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-cq-integration-api</artifactId>
     <version>11.0.0</version>
   </dependency>
   ```

   サービスを開始するには、サービスに対応する Maven 依存性を追加します。依存性のリストについて詳しくは、「[Document Service リスト](/help/forms/using/aem-livecycle-connector.md#p-document-services-list-p)」を参照してください。例えば、Generate PDFサービスの場合、次の依存関係を追加します。

   ```xml
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-generatepdf-client</artifactId>
     <version>11.0.0</version>
   </dependency>
   ```

1. サービス参照を取得します。サービスインスタンスへのハンドルを取得します。Java クラスを作成している場合、Declarative Services の注釈を使用できます。

   ```java
   import com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient;
   import com.adobe.livecycle.generatepdf.client.CreatePDFResult;
   import com.adobe.idp.Document;
   
   @Reference
   GeneratePdfServiceClient generatePDF;
   ...
   
   Resource r = resourceResolver.getResource("/path/tp/docx");
   Document sourceDoc = new Document(r.adaptTo(InputStream.class));
   CreatePDFResult result = generatePDF.createPDF2(
                       sourceDoc,
                       extension, //inputFileExtension
                       null, //fileTypeSettings
                       null, //pdfSettings
                       null, //securitySettings
                       settingsDoc, //settingsDoc
                       null //xmpDoc
               );
   ```

   上記のコードスニペットでは、ドキュメントを PDF に変換するために GeneratePdfServiceClient の createPDF API を開始します。次のコードを使用し、JSP で同じ呼び出しを実行できます。主な違いは、次のコードではSling ScriptHelperを使用してGeneratePdfServiceClientにアクセスする点です。

   ```java
   <%@ page import="com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient" %>
   <%@ page import="com.adobe.livecycle.generatepdf.client.CreatePDFResult" %>
   <%@ page import="com.adobe.idp.Document" %>
   
   GeneratePdfServiceClient generatePDF = sling.getService(GeneratePdfServiceClient.class);
   Document sourceDoc = ...
   CreatePDFResult result = generatePDF.createPDF2(
                       sourceDoc,
                       extension, //inputFileExtension
                       null, //fileTypeSettings
                       null, //pdfSettings
                       null, //securitySettings
                       settingsDoc, //settingsDoc
                       null //xmpDoc
               );
   ```

### ServiceClientFactory を介した開始 {#starting-via-serviceclientfactory}

ServiceClientFactory クラスが必要になる場合があります。例えば、プロセスを呼び出すには ServiceClientFactory が必要です。

```java
import com.adobe.livecycle.dsc.clientsdk.ServiceClientFactoryProvider;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;

@Reference
ServiceClientFactoryProvider scfProvider;

...
ServiceClientFactory scf = scfProvider.getDefaultServiceClientFactory();
...
```

## RunAs サポート {#runas-support}

LiveCycle のほとんどの Document Service には認証が必要です。次のオプションのいずれかを使用すると、コードに資格情報を明示的に指定せずにこれらのサービスを開始できます。

### 許可リスト設定 {#allowlist-configuration}

LiveCycle Client SDK 設定には、サービス名についての設定が含まれています。この設定は、呼び出しロジックが追加設定なしに管理者資格情報を使用するサービスのリストです。例えば、DirectoryManager サービス（User Management API の一部）をこのリストに追加する場合、すべてのクライアントコードはこのサービスを直接使用することが可能で、呼び出しレイヤーは LiveCycle サーバーに送信された要求の一部として、設定された資格情報を自動的に渡します。

### RunAsManager {#runasmanager}

統合の一部として、新しいサービス RunAsManager を提供しています。このサービスにより、LiveCycle サーバーへの呼び出しをする際に、資格情報をプログラムで制御できます。

```java
import com.adobe.livecycle.dsc.clientsdk.security.PasswordCredential;
import com.adobe.livecycle.dsc.clientsdk.security.PrivilegedAction;
import com.adobe.livecycle.dsc.clientsdk.security.RunAsManager;
import com.adobe.idp.dsc.registry.component.ComponentRegistry;

@Reference
private RunAsManager runAsManager;

List<Component> components = runAsManager.doPrivileged(new PrivilegedAction<List<Component>>() {
            public List<Component> run() {
                return componentRegistry.getComponents();
            }
        });
assertNotNull(components);
```

異なる資格情報を渡す場合は、PasswordCredential インスタンスが必要となる、過度に負荷がかかる方法を使用できます。

```java
PasswordCredential credential = new PasswordCredential("administrator","password");
List<Component> components = runAsManager.doPrivileged(new PrivilegedAction<List<Component>>() {
    public List<Component> run() {
        return componentRegistry.getComponents();
    }
},credential);
```

### InvocationRequest プロパティ {#invocationrequest-property}

プロセスを呼び出す場合、または ServiceClientFactory を直接使用して InvocationRequest を作成する場合は、設定済みの資格情報を呼び出しレイヤーが使用する必要があることをプロパティが示すように指定できます。

```java
import com.adobe.idp.dsc.InvocationResponse
import com.adobe.idp.dsc.InvocationRequest
import com.adobe.livecycle.dsc.clientsdk.ServiceClientFactoryProvider
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory
import com.adobe.livecycle.dsc.clientsdk.InvocationProperties

ServiceClientFactoryProvider scfp = sling.getService(ServiceClientFactoryProvider.class)
ServiceClientFactory serviceClientFactory = scfp.getDefaultServiceClientFactory()
InvocationRequest ir = serviceClientFactory.createInvocationRequest("sample/LetterSubmissionProcess", "invoke", new HashMap(), true);

//Here we are invoking the request with system user
ir.setProperty(InvocationProperties.INVOKER_TYPE,InvocationProperties.INVOKER_TYPE_SYSTEM)

InvocationResponse response = serviceClientFactory.getServiceClient().invoke(ir);
```

## Document Services リスト {#document-services-list}

### Adobe LiveCycle Client SDK API バンドル {#adobe-livecycle-client-sdk-api-bundle}

次のサービスを使用できます。

* com.adobe.idp.um.api.AuthenticationManager
* com.adobe.idp.um.api.DirectoryManager
* com.adobe.idp.um.api.AuthorizationManager
* com.adobe.idp.dsc.registry.service.ServiceRegistry
* com.adobe.idp.dsc.registry.component.ComponentRegistry

#### Maven の依存関係 {#maven-dependencies}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-livecycle-client</artifactId>
  <version>11.0.0</version>
</dependency>
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-usermanager-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Client SDK バンドル {#adobe-livecycle-client-sdk-bundle}

次のサービスを使用できます。

* com.adobe.livecycle.dsc.clientsdk.security.RunAsManager
* com.adobe.livecycle.dsc.clientsdk.ServiceClientFactoryProvider

#### Maven の依存関係 {#maven-dependencies-1}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-livecycle-cq-integration-api</artifactId>
  <version>1.1.10</version>
</dependency>
```

### Adobe Livecycle TaskManager Client バンドル {#adobe-livecycle-taskmanager-client-bundle}

次のサービスを使用できます。

* com.adobe.idp.taskmanager.dsc.client.task.TaskManager
* com.adobe.idp.taskmanager.dsc.client.TaskManagerQueryService
* com.adobe.idp.taskmanager.dsc.client.queuemanager.QueueManager
* com.adobe.idp.taskmanager.dsc.client.emailsettings.EmailSettingService
* com.adobe.idp.taskmanager.dsc.client.endpoint.TaskManagerEndpointClient
* com.adobe.idp.taskmanager.dsc.client.userlist.UserlistService

#### Maven の依存関係 {#maven-dependencies-2}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-taskmanager-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Workflow Client バンドル {#adobe-livecycle-workflow-client-bundle}

次のサービスを使用できます。

* com.adobe.idp.workflow.client.WorkflowServiceClient

#### Maven の依存関係 {#maven-dependencies-3}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-workflow-client-sdk</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle PDF Generator Client バンドル {#adobe-livecycle-pdf-generator-client-bundle}

次のサービスを使用できます。

* com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient

#### Maven の依存関係 {#maven-dependencies-4}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-generatepdf-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Application Manager Client バンドル {#adobe-livecycle-application-manager-client-bundle}

次のサービスを使用できます。

* com.adobe.idp.applicationmanager.service.ApplicationManager
* com.adobe.livecycle.applicationmanager.client.ApplicationManager
* com.adobe.livecycle.design.service.DesigntimeService

#### Maven の依存関係 {#maven-dependencies-5}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-applicationmanager-client-sdk</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Assembler Client バンドル {#adobe-livecycle-assembler-client-bundle}

次のサービスを使用できます。

* com.adobe.livecycle.assembler.client.AssemblerServiceClient

#### Maven の依存関係 {#maven-dependencies-6}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-assembler-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Form Data Integration Client バンドル {#adobe-livecycle-form-data-integration-client-bundle}

次のサービスを使用できます。

* com.adobe.livecycle.formdataintegration.client.FormDataIntegrationClient

#### Maven の依存関係 {#maven-dependencies-7}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-formdataintegration-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Forms Client バンドル {#adobe-livecycle-forms-client-bundle}

次のサービスを使用できます。

* com.adobe.livecycle.formsservice.client.FormsServiceClient

#### Maven の依存関係 {#maven-dependencies-8}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-forms-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Output Client バンドル {#adobe-livecycle-output-client-bundle}

次のサービスを使用できます。

* com.adobe.livecycle.output.client.OutputClient

#### Maven の依存関係 {#maven-dependencies-9}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-output-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Reader Extensions Client バンドル {#adobe-livecycle-reader-extensions-client-bundle}

次のサービスを使用できます。

* com.adobe.livecycle.readerextensions.client.ReaderExtensionsServiceClient

#### Maven の依存関係 {#maven-dependencies-10}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-reader-extensions-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Rights Manager Client バンドル {#adobe-livecycle-rights-manager-client-bundle}

次のサービスを使用できます。

* com.adobe.livecycle.rightsmanagement.client.DocumentManager
* com.adobe.livecycle.rightsmanagement.client.EventManager
* com.adobe.livecycle.rightsmanagement.client.ExternalUserManager
* com.adobe.livecycle.rightsmanagement.client.LicenseManager
* com.adobe.livecycle.rightsmanagement.client.WatermarkManager
* com.adobe.livecycle.rightsmanagement.client.PolicyManager
* com.adobe.livecycle.rightsmanagement.client.AbstractPolicyManager

#### Maven の依存関係 {#maven-dependencies-11}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-rightsmanagement-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Signatures Client バンドル {#adobe-livecycle-signatures-client-bundle}

次のサービスを使用できます。

* com.adobe.livecycle.signatures.client.SignatureServiceClientInterface

#### Maven の依存関係 {#maven-dependencies-12}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-signatures-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Truststore Client バンドル {#adobe-livecycle-truststore-client-bundle}

次のサービスを使用できます。

* com.adobe.truststore.dsc.TrustConfigurationService
* com.adobe.truststore.dsc.CRLService
* com.adobe.truststore.dsc.CredentialService
* com.adobe.truststore.dsc.CertificateService

#### Maven の依存関係 {#maven-dependencies-13}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-truststore-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Repository Client バンドル {#adobe-livecycle-repository-client-bundle}

次のサービスを使用できます。

* com.adobe.repository.bindings.ResourceRepository
* com.adobe.repository.bindings.ResourceSynchronizer

#### Maven の依存関係 {#maven-dependencies-14}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-repository-client</artifactId>
  <version>11.0.0</version>
</dependency>
```
