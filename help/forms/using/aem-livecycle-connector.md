---
title: AEM Forms と Adobe LiveCycle の接続
seo-title: Connecting AEM Forms with Adobe LiveCycle
description: AEMLiveCycleコネクタを使用すると、AEMアプリとワークフロー内からLiveCycleES4 Document Services を開始できます。
seo-description: AEM LiveCycle connector lets you start LiveCycle ES4 Document Services from within AEM apps and workflows.
uuid: 7dc9d5ec-7b19-4d93-936d-81ceb45dfffa
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 7e404b45-1302-4dd1-b3c9-3f47fedb5f94
role: Admin
exl-id: 562f8a22-cbab-4915-bc0d-da9bea7d18fa
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1004'
ht-degree: 25%

---

# AEM Forms と Adobe LiveCycle の接続 {#connecting-aem-forms-with-adobe-livecycle}

Adobe Experience Manager(AEM)LiveCycleコネクタを使用すると、AEM Web アプリケーションおよびワークフロー内からAdobeLiveCycleES4 Document Services をシームレスに呼び出すことができます。 LiveCycleには、Java API を使用してクライアントアプリケーションがLiveCycleサービスを開始できる、リッチクライアント SDK が用意されています。 AEMLiveCycleコネクタは、OSGi 環境内でこれらの API の使用を簡単にします。

## AEM サーバーの Adobe LiveCycle への接続 {#connecting-aem-server-to-adobe-livecycle}

AEM LiveCycle Connector は「[AEM Forms アドオンパッケージ](/help/forms/using/installing-configuring-aem-forms-osgi.md)」の一部です。AEM Forms アドオンパッケージをインストールしたら、次の手順を実行して、LiveCycle サーバーの詳細を AEM Web Console に追加します。

1. AEM Web Console Configuration Manager で、AdobeLiveCycleClient SDK configuration Component を探します。
1. コンポーネントをクリックして、設定サーバーの URL、ユーザー名、パスワードを編集します。
1. 設定を確認し、「**保存**」をクリックします。

プロパティは説明なしですが、重要なプロパティは次のとおりです。

* **サーバー URL** - LiveCycle Server への URL を指定します。LiveCycle と AEM の間で HTTPS を経由して通信する場合、次の JVM で AEM を起動

  ```java
  argument
   -Djavax.net.ssl.trustStore=<<em>path to LC keystore</em>>
  ```

  option.

* **ユーザー名** - AEM と LiveCycle 間の通信を確立するのに使用するアカウントのユーザー名を指定します。アカウントは、Document Services の開始を許可されている LiveCycle ユーザーアカウントです。
* **パスワード** - パスワードを指定します。
* **サービス名** - 「ユーザー名」フィールドと「パスワード」フィールドに入力されたユーザー資格情報を使用して開始するサービスを指定します。 デフォルトでは、LiveCycleサービスの開始中に資格情報は渡されません。

## Document Services の開始 {#starting-document-services}

クライアントアプリケーションは、Java API、Web サービス、リモート、REST を使用してLiveCycleサービスをプログラムで開始できます。 Java クライアントの場合、アプリケーションはLiveCycleSDK を使用できます。 LiveCycleSDK は、これらのサービスをリモートで開始するための Java API を提供します。 例えば、Microsoft Word ドキュメントをPDFに変換する場合、クライアントは GeneratePDFService を開始します。 呼び出しフローは、次の手順で構成されます。

1. ServiceClientFactory インスタンスを作成します。
1. 各サービスはクライアントクラスを提供します。 サービスを開始するには、サービスのクライアントインスタンスを作成します。
1. サービスを開始し、結果を処理します。

AEMLiveCycleコネクタは、標準の OSGi の手段を使用してアクセスできる OSGi サービスとしてこれらのクライアントインスタンスを公開するので、フローを簡素化します。 LiveCycle コネクターには、以下の機能が用意されています。

* OSGi サービスとしてのクライアントインスタンス：OSGI バンドルとしてパッケージ済みのクライアントは、「[ドキュメントサービスリスト](/help/forms/using/aem-livecycle-connector.md#p-document-services-list-p)」セクションに一覧表示されます。各クライアント jar は、OSGi Service Registry を使用して、クライアントインスタンスを OSGi サービスとして登録します。
* ユーザー資格情報の伝達：LiveCycleサーバーへの接続に必要な接続の詳細は、一元的に管理されます。
* ServiceClientFactory サービス：プロセスを開始するために、クライアントアプリケーションは ServiceClientFactory インスタンスにアクセスできます。

### OSGi Service Registry の Service References を介した開始 {#starting-via-service-references-from-osgi-service-registry}

AEM内から公開されたサービスを開始するには、次の手順に従います。

1. Maven の依存関係を特定します。 maven pom.xml ファイルの必要なクライアント jar に依存関係を追加します。 少なくとも、adobe-livecycle-client と adobe-usermanager-client jar に依存関係を追加します。

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

   サービスを開始するには、対応する Maven 依存関係をサービスに追加します。 依存関係のリストについては、 [Document Service リスト](/help/forms/using/aem-livecycle-connector.md#p-document-services-list-p). 例えば、Generate PDF サービスの場合は、次の依存関係を追加します。

   ```xml
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-generatepdf-client</artifactId>
     <version>11.0.0</version>
   </dependency>
   ```

1. サービス参照を取得します。 サービスインスタンスへのハンドルを取得します。 Java クラスを記述する場合は、Declarative Services 注釈を使用できます。

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

   上記のコードスニペットは、ドキュメントをPDFに変換するために、GeneratePdfServiceClient の createPDF API を開始します。 次のコードを使用して、JSP でも同様の呼び出しを実行できます。 主な違いは、次のコードでは Sling ScriptHelper を使用して GeneratePdfServiceClient にアクセスする点です。

   ```jsp
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

ServiceClientFactory クラスが必要になる場合もあります。 例えば、プロセスを呼び出すには ServiceClientFactory が必要です。

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

ほとんどの Document Service でLiveCycleを使用するには認証が必要です。 コードに明示的な資格情報を指定せずに、次のいずれかのオプションを使用して、これらのサービスを開始できます。

### 許可リスト設定 {#allowlist-configuration}

LiveCycleクライアント SDK 設定には、サービス名に関する設定が含まれています。 この設定は、呼び出しロジックが標準で管理者の資格情報を使用するサービスのリストです。 例えば、DirectoryManager サービス（User Management API の一部）をこのリストに追加した場合、任意のクライアントコードがサービスを直接使用でき、呼び出し層はLiveCycleサーバーに送信される要求の一環として、設定された資格情報を自動的に渡します

### RunAsManager {#runasmanager}

統合の一環として、新しいサービス RunAsManager が提供されます。 これにより、LiveCycleサーバーを呼び出す際に使用する秘密鍵証明書をプログラムで制御できます。

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

別の資格情報を渡す場合は、PasswordCredential インスタンスを取得するオーバーロードされたメソッドを使用できます。

```java
PasswordCredential credential = new PasswordCredential("administrator","password");
List<Component> components = runAsManager.doPrivileged(new PrivilegedAction<List<Component>>() {
    public List<Component> run() {
        return componentRegistry.getComponents();
    }
},credential);
```

### InvocationRequest プロパティ {#invocationrequest-property}

プロセスを呼び出す場合、または ServiceClientFactory クラスを直接使用して InvocationRequest を作成する場合は、設定された資格情報を呼び出しレイヤーが使用する必要があることを示すプロパティを指定できます。

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

### AdobeLiveCycleクライアント SDK API バンドル {#adobe-livecycle-client-sdk-api-bundle}

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

### AdobeLiveCycleクライアント SDK バンドル {#adobe-livecycle-client-sdk-bundle}

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

### AdobeLiveCycleTaskManager Client バンドル {#adobe-livecycle-taskmanager-client-bundle}

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

### AdobeLiveCycle Workflowクライアントバンドル {#adobe-livecycle-workflow-client-bundle}

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

### AdobeLiveCycleApplication Manager Client バンドル {#adobe-livecycle-application-manager-client-bundle}

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

### AdobeLiveCycleAssembler Client バンドル {#adobe-livecycle-assembler-client-bundle}

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

### AdobeLiveCycleフォームデータ統合クライアントバンドル {#adobe-livecycle-form-data-integration-client-bundle}

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

### AdobeLiveCycleRights Manager Client バンドル {#adobe-livecycle-rights-manager-client-bundle}

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

### AdobeLiveCycle署名クライアントバンドル {#adobe-livecycle-signatures-client-bundle}

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

### AdobeLiveCycleTruststore Client バンドル {#adobe-livecycle-truststore-client-bundle}

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

### AdobeLiveCycleリポジトリークライアントバンドル {#adobe-livecycle-repository-client-bundle}

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
