---
title: JMX コンソールを使用したサービスの統合
seo-title: JMX コンソールを使用したサービスの統合
description: JMX コンソールを使用してサービスを管理する MBean を作成してデプロイすることで、管理タスクを実行できるようにサービス属性および操作を公開します
seo-description: JMX コンソールを使用してサービスを管理する MBean を作成してデプロイすることで、管理タスクを実行できるようにサービス属性および操作を公開します
uuid: 4a489a24-af10-4505-8333-aafc0c81dd3e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 83c590e0-2e6c-4499-a6ea-216e4c7bc43c
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5
workflow-type: tm+mt
source-wordcount: '1689'
ht-degree: 88%

---


# JMX コンソールを使用したサービスの統合{#integrating-services-with-the-jmx-console}

JMX コンソールを使用してサービスを管理する MBean を作成し、デプロイします。管理タスクを実行できるよう、サービス属性および操作を公開します。

JMX コンソールの使用については、[JMX コンソールを使用したサーバーリソースの監視](/help/sites-administering/jmx-console.md)を参照してください。

## Felix および CQ5 の JMX フレームワーク {#the-jmx-framework-in-felix-and-cq}

Apache Felix プラットフォーム上で、MBean を OSGi サービスとしてデプロイします。MBeanサービスがOSGi Service Registryに登録されると、Aries JMX WhiteboardモジュールはMBeanをMBeanサーバーに自動的に登録します。 すると、公開属性および操作を公開する JMX コンソールに MBean が表示されます。

![jmxwhiteboard](assets/jmxwhiteboard.png)

## CQ5 および CRX 向けの MBean の作成 {#creating-mbeans-for-cq-and-crx}

CQ5 または CRX リソースを管理するために作成する MBean は、javax.management.DynamicMBean インターフェイスをベースとしています。このような MBean を作成するには、JMX 仕様に明記されている通常のデザインパターンに従います。

* 属性を定義する get、set および is メソッドや、操作を定義するその他のメソッドを含む管理インターフェイスを作成します。
* 実装クラスを作成します。実装クラスは、DynamicMBean を実装するか、DynamicMBean の実装クラスを拡張する必要があります。
* 標準の命名規則に従って、実装クラスの名前は MBean をサフィックスに持つインターフェイス名になります。

管理インターフェイスの定義に加え、このインターフェイスで OSGi サービスインターフェイスも定義します。実装クラスによって OSGi サービスが実装されます。

### 注釈を使用した MBean 情報の提供 {#using-annotations-to-provide-mbean-information}

[com.adobe.granite.jmx.annotation](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/jmx/annotation/package-summary.html) パッケージには、MBean メタデータを JMX コンソールに簡単に提供するための注釈とクラスがいくつか用意されています。MBean の MBeanInfo オブジェクトに情報を直接追加する代わりに、これらの注釈とクラスを使用してください。

**注釈**

注釈を管理インターフェイスに追加して、MBean メタデータを指定します。この情報は、デプロイされている実装クラスごとに JMX コンソールに表示されます。以下の注釈を使用できます（詳しくは、[com.adobe.granite.jmx.annotation に関する JavaDoc](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/jmx/annotation/package-summary.html) を参照してください）。

* **Description：** MBean クラスまたはメソッドの説明を提供します。クラスの宣言に対して使用する場合、MBean の JMX コンソールページに説明が表示されます。メソッドに対して使用する場合、対応する属性または操作のテキストにマウスポインターを置くと、説明が表示されます。
* **Impact：**&#x200B;メソッドの影響。Valid parameter values are the fields defined by [javax.management.MBeanOperationInfo](https://docs.oracle.com/javase/1.5.0/docs/api/javax/management/MBeanOperationInfo.html).

* **Name：**&#x200B;操作パラメーターに対して表示する名前を指定します。この注釈を使用して、インターフェイスで使用されているメソッドパラメーターの実際の名前をオーバーライドします。
* **OpenTypeInfo：** JMX コンソールでの複合データまたは表形式データの表示に使用するクラスを指定します。Open MBean と併用します。
* **TabularTypeInfo：**&#x200B;表形式データの表示に使用するクラスに注釈を付けるために使用します。

**クラス**

クラスは、インターフェイスに追加した注釈を利用する Dynamic MBean を作成するために指定します。

* **AnnotatedStandardMBean：** javax.management.StandardMBean クラスのサブクラスで、注釈メタデータを JMX コンソールに自動的に提供します。
* **OpenAnnotatedStandardMBean:** OpenTypeInfo注釈を使用するOpen Mbeanを作成するためのAnnotatedStandardMBeanクラスのサブクラス。

### MBean のデプロイ {#developing-mbeans}

一般的に、MBean は管理する OSGi サービスを表したものです。Felix プラットフォーム上で、他の Java サーバープラットフォームにデプロイする場合と同様に MBean を作成します。主な違いは、注釈を使用して以下の MBean 情報を指定できる点です。

* 管理インターフェイス：getter、setter および is メソッドを使用して属性を定義します。他のいずれかの公開メソッドを使用して操作を定義します。注釈を使用してBeanInfoオブジェクトのメタデータを提供します。
* MBean クラス：管理インターフェイスを実装します。インターフェイス上で注釈を処理できるように、AnnotatedStandardMBean クラスを拡張します。

次のサンプル MBean は、CRX リポジトリに関する情報を提供します。このインターフェイスは、Description 注釈を使用して JMX コンソールに情報を提供します。

#### 管理インターフェイス {#management-interface}

```java
package com.adobe.example.myapp;

import com.adobe.granite.jmx.annotation.Description;

@Description("Example MBean that exposes repository properties.")
public interface ExampleMBean {

    @Description("The name of the repository.")
    String getRepositoryName();

    @Description("The vendor of the repository.")
    String   getRepositoryVendor();

    @Description("The URL of repository vendor.")
    String getVendorUrl();
}
```

実装クラスは SlingRepository サービスを使用して、CRX リポジトリに関する情報を取得します。

#### MBean 実装クラス {#mbean-implementation-class}

```java
package com.adobe.example.myapp;

import org.apache.felix.scr.annotations.*;
import org.apache.sling.jcr.api.SlingRepository;

import com.adobe.granite.jmx.annotation.AnnotatedStandardMBean;

import javax.management.*;

public class ExampleMBeanImpl extends AnnotatedStandardMBean implements ExampleMBean {

    @Reference(cardinality = ReferenceCardinality.OPTIONAL_UNARY)
    private SlingRepository repository;

    public ExampleMBeanImpl() throws NotCompliantMBeanException {
        super(ExampleMBean.class);
    }

    public String getRepositoryName() {
        return repository.getDescriptor("jcr.repository.name");
    }

    public String getRepositoryVendor() {
        return repository.getDescriptor("jcr.repository.vendor");
    }

    public String getVendorUrl() {
        return repository.getDescriptor("jcr.repository.vendor.url");
    }
}
```

次の図は、JMX コンソールに表示されるこの MBean 用のページを示したものです。

![jmxdescription](assets/jmxdescription.png)

### MBean の登録 {#registering-mbeans}

MBean を OSGi サービスとして登録すると、MBean サーバーに自動的に登録されます。MBean を CQ5 にインストールするには、バンドルに含めて、他の OSGi サービスと同様に MBean サービスを書き出します。

OSGi 関連メタデータ以外にも、Aries JMX Whiteboard モジュールが MBean を MBean サーバーに登録するために必要な次のメタデータを提供する必要があります。

* **DynamicMBeanインターフェイスの名前：** MBeanサービスが `javax.management.DynamicMBea`nインターフェイスを実装することを宣言します。 この宣言によって、このサービスが MBean サービスであることが Aries JMX Whiteboard モジュールに通知されます。

* **MBeanドメインおよびキーのプロパティ：** Felixでは、この情報をMBeanのOSGiサービスのプロパティとして指定します。 This is the same information that you ordinarily provide to the MBean Server in a `javax.management.ObjectName` object.

MBean が単一のサービスを表している場合、必要な MBean サービスのインスタンスは 1 つだけです。この場合、Felix SCR Maven プラグインを使用していれば、MBean 実装クラスに Apache Felix Service Component Runtime（SCR）注釈を使用して、JMX 関連メタデータを指定できます。複数の MBean インスタンスをインスタンス化するために、MBean の OSGi サービスの登録を実行する別のクラスを作成できます。この場合、JMX 関連メタデータは実行時に生成されます。

**単一の MBean**

デザイン時にすべての属性と操作を定義できる MBean は、MBean 実装クラスの SCR 注釈を使用してデプロイできます。次の例では、`value` 注釈の `Service` 属性によって、サービスが `DynamicMBean` インターフェイスを実装することを宣言しています。`name` 注釈の `Property` 属性は、JMX ドメインおよびキーのプロパティを指定します。

#### SCR 注釈を使用した MBean 実装クラス {#mbean-implementation-class-with-scr-annotations}

```java
package com.adobe.example.myapp;

import org.apache.felix.scr.annotations.*;
import org.apache.sling.jcr.api.SlingRepository;

import com.adobe.granite.jmx.annotation.AnnotatedStandardMBean;

import javax.management.*;

@Component(immediate = true)
@Property(name = "jmx.objectname", value="com.adobe.example:type=CRX")
@Service(value = DynamicMBean.class)
public class ExampleMBeanImpl extends AnnotatedStandardMBean implements ExampleMBean {

    @Reference(cardinality = ReferenceCardinality.OPTIONAL_UNARY)
    private SlingRepository repository;

    public ExampleMBeanImpl() throws NotCompliantMBeanException {
        super(ExampleMBean.class);
    }

    public String getRepositoryName() {
        return repository.getDescriptor("jcr.repository.name");
    }

    public String getRepositoryVendor() {
        return repository.getDescriptor("jcr.repository.vendor");
    }

    public String getVendorUrl() {
        return repository.getDescriptor("jcr.repository.vendor.url");
    }
}
```

**複数の MBean サービスインスタンス**

1 つの管理対象サービスの複数インスタンスを管理するには、対応する MBean サービスのインスタンスを複数作成します。さらに、管理対象インスタンスの開始または終了時に、MBean サービスインスタンスを作成または削除する必要があります。MBean Managerクラスを作成して、実行時にMBeanサービスをインスタンス化し、サービスのライフサイクルを管理できます。

BundleContext を使用して、MBean を OSGi サービスとして登録します。JMX 関連情報を BundleContext.registerService メソッドの引数として使用する Dictionary オブジェクトに含めます。

次のコードサンプルでは、ExampleMBean サービスをプログラムによって登録しています。componentContext オブジェクトは ComponentContext で、BundleContext へのアクセスを提供します。

#### コードスニペット：プログラムによる MBean サービスの登録 {#code-snippet-programmatic-mbean-service-registration}

```java
Dictionary mbeanProps = new Hashtable();
mbeanProps.put("jmx.objectname", "com.adobe.example:type=CRX");
ExampleMBeanImpl mbean = new ExampleMBeanImpl();
ServiceRegistration serviceregistration =
            componentContext.getBundleContext().registerService(DynamicMBean.class.getName(), mbean, mbeanProps);
```

次の節のサンプル MBean でさらに詳しく説明します。

MBean サービスマネージャーは、サービス設定がリポジトリに保存されている場合に役立ちます。このマネージャーは、サービス情報を取得し、対応する MBean の設定と作成に使用できます。マネージャークラスは、リポジトリ変更イベントをリスンし、それに応じて MBean サービスを更新することもできます。

## 例：JMX を使用したワークフローモデルの監視 {#example-monitoring-workflow-models-using-jmx}

このサンプルの MBean は、リポジトリに保存されている CQ5 ワークフローモデルに関する情報を提供します。MBean マネージャークラスは、リポジトリに保存されているワークフローモデルに基づいて MBean を作成し、その OSGi サービスを実行時に登録します。このサンプルは、以下のメンバーを含む単一のバンドルで構成されています。

* WorkflowMBean：管理インターフェイス。
* WorkflowMBeanImpl：MBean 実装クラス。
* WorkflowMBeanManager：MBean マネージャークラスのインターフェイス。
* WorkflowMBeanManagerImpl：MBean マネージャーの実装クラス。

**注意：** 簡単にするために、この例のコードは、ログ記録やスローされた例外に対する反応を実行しません。

WorkflowMBeanManagerImpl には、コンポーネントアクティベーションメソッドが含まれています。コンポーネントをアクティベートすると、このメソッドによって以下のタスクが実行されます。

* バンドルの BundleContext を取得します。
* リポジトリをクエリして、既存のワークフローモデルのパスを取得します。
* ワークフローモデルごとにMBeanを作成します。
* MBean を OSGi サービスレジストリに登録します。

JMX コンソールに、ドメインが com.adobe.example、タイプが workflow_model、プロパティがワークフローモデル設定ノードのパスである MBean メタデータが表示されます。

![jmxworkflowmbean](assets/jmxworkflowmbean.png)

### サンプル MBean {#the-example-mbean}

このサンプルには、MBean インターフェイスと、`com.day.cq.workflow.model.WorkflowModel` インターフェイスを表す実装が必要です。この例では、デザインの設定とデプロイメントの面に集中できるように、MBean は非常にシンプルになっています。この MBean は、単一の属性であるモデル名を公開します。

#### WorkflowMBean インターフェイス {#workflowmbean-interface}

```java
package com.adobe.example.myapp.api;

import com.adobe.granite.jmx.annotation.Description;

@Description("Example MBean that exposes Workflow model properties.")
public interface WorkflowMBean {

 @Description("The name of the Workflow model.")
 String getModelName();
}
```

#### WorkflowMBeanImpl {#workflowmbeanimpl}

```java
package com.adobe.example.myapp.impl;

import javax.management.NotCompliantMBeanException;

import com.day.cq.workflow.model.WorkflowModel;
import com.adobe.example.myapp.api.WorkflowMBean;
import com.adobe.granite.jmx.annotation.AnnotatedStandardMBean;

public class WorkflowMBeanImpl extends AnnotatedStandardMBean implements WorkflowMBean {

 WorkflowModel model;

 protected WorkflowMBeanImpl(WorkflowModel inmodel)
   throws NotCompliantMBeanException {
  super(WorkflowMBean.class);
  model=inmodel;
 }

 public String getModelName() {
  return model.getTitle();
 }
}
```

### サンプル MBean マネージャー {#the-example-mbean-manager}

WorkflowMBeanManager サービスには、WorkflowMBean サービスを作成するコンポーネントアクティベーションメソッドが含まれています。このサービス実装には、以下のメソッドがあります。

* activate：コンポーネントアクティベーター。WorkflowModel 設定ノードを読み取るための JCR セッションを作成します。モデル設定が保存されるルートノードは、静的フィールドで定義されます。設定ノードの名前も静的フィールドで定義されます。このメソッドは、モデルノードのパスを取得し、モデルの WorkflowMBean を作成する他のメソッドを呼び出します。
* getModelIds：ルートノードの下のリポジトリをたどって、各モデルノードのパスを取得します。
* makeMBean：モデルパスを使用して WorkflowModel オブジェクトを作成し、その WorkflowMBean を作成し、その OSGi サービスを登録します。

>[!NOTE]
>
>WorkflowMBeanManager 実装は、コンポーネントがアクティベートされたときに存在するモデル設定の MBean サービスのみを作成します。さらに堅牢な実装では、新しいモデル設定や、既存のモデル設定の変更または削除に関するリポジトリイベントをリスンします。変更が発生すると、マネージャーは対応する WorkflowMBean サービスを作成、変更または削除できます。


#### WorkflowMBeanManager インターフェイス {#workflowmbeanmanager-interface}

```java
package com.adobe.example.myapp.api;

public interface WorkflowMBeanManager {

}
```

#### WorkflowMBeanManagerImpl {#workflowmbeanmanagerimpl}

```java
package com.adobe.example.myapp.impl;

import java.util.*;

import org.apache.felix.scr.annotations.*;

import javax.jcr.Session;
import javax.jcr.Node;
import javax.jcr.NodeIterator;
import javax.jcr.RepositoryException;
import javax.management.ObjectName;

import org.apache.sling.jcr.api.SlingRepository;
import org.osgi.framework.ServiceRegistration;
import org.osgi.service.component.ComponentContext;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.day.cq.workflow.WorkflowService;
import com.day.cq.workflow.WorkflowSession;
import com.adobe.example.myapp.api.WorkflowMBean;
import com.adobe.example.myapp.api.WorkflowMBeanManager;

/**Instantiates and registers WorkflowMBean services */
@Component(immediate=true)
@Service(value=WorkflowMBeanManager.class)
public class WorkflowMBeanManagerImpl implements WorkflowMBeanManager {
 //The ComponentContext provides access to the BundleContext
 private ComponentContext componentContext;

 //Use the SlingRepository service to read model nodes
 @Reference
        private SlingRepository repository = null;

 //Use the WorkflowService service to create WorkflowModel objects
 @Reference
 private WorkflowService workflowservice = null;

  private Session session;

         //Details about model nodes
  private static final String MODEL_ROOT ="/etc/workflow/models";
  private static final String MODEL_NODE = "model";

  private Set<String> modelIds = new HashSet<String>();

        //Storage for ServiceRegistrations for MBean services
  private Collection<ServiceRegistration> mbeanRegistrations= new Vector<ServiceRegistration>(0,1);

 @Activate
        protected void activate(ComponentContext ctx) {
             //Traverse the repository and load the model nodes
             try {
                   session = repository.loginAdministrative(null);
                   // load and store model node paths
                   if (session.nodeExists(MODEL_ROOT)) {
                          getModelIds(session.getNode(MODEL_ROOT));
                   }
                   //Create MBeans for each model
                   for(String modid: modelIds){
                    makeMBean(modid);
                    }
             }catch(Exception e){ }
          }

        /**
         * Add JMX domain and key properties to a collection
         * Instantiate a WorkflowModel and its WorkflowMBeanImpl object
         * Register the MBean OSGi service
         */
 private void makeMBean(String modelId) {
             // create MBean for the model
             try {
                 Dictionary<String, String> mbeanProps = new Hashtable<String, String>();
                 //These properties appear on the JMX Console home page
                 mbeanProps.put("jmx.objectname", "com.adobe.example:type=workflow_model,id=" + ObjectName.quote(modelId));
                 WorkflowSession wfsession = workflowservice.getWorkflowSession(session);
                 WorkflowMBeanImpl mbean = new WorkflowMBeanImpl(wfsession.getModel(modelId));

                ServiceRegistration serviceregistration = componentContext.getBundleContext().registerService(WorkflowMBean.class.getName(), mbean, mbeanProps);
                //Store the ServiceRegistration objects for deactivation
                mbeanRegistrations.add(serviceregistration);
             } catch (Throwable t) {}
         }

        /**
         * Traverses the repository branch below a given Node. Stores the path of each model node.
         */
 private void getModelIds(Node node) throws RepositoryException {
  try{
                     NodeIterator iter = node.getNodes();
                     while (iter.hasNext()) {
                           Node n = iter.nextNode();
                           //Look for "jcr:content" nodes
                           if (n.getName().equals("jcr:content")) {
                                //get the path of the model node and save it
                                if(n.hasNode(MODEL_NODE)){
                                      modelIds.add(n.getNode(MODEL_NODE).getPath());
                                 }
                           } else{
                                   //Scan child nodes
                                   getModelIds(n);
                           }
                       }
  }catch(Exception e){ }
       }

        /**
         * Log out of the JCR session and unregister WorkflowMBean services
         */
        @Deactivate
        protected void deactivate() {
          session.logout();
          session=null;
          for(ServiceRegistration sr:mbeanRegistrations){
         sr.unregister();
          }
        }
}
```

### サンプル MBean の POM ファイル {#the-pom-file-for-the-example-mbean}

以下の XML コードをコピーしてプロジェクトの pom.xml ファイルに貼り付け、コンポーネントバンドルを作成できます。POM は、必要な複数のプラグインおよび依存関係を参照します。

**プラグイン：**

* Apache Maven Compiler Plugin：ソースコードから Java クラスをコンパイルします。
* Apache Felix Maven Bundle Plugin：バンドルとマニフェストを作成します。
* Apache Felix Maven SCR Plugin：コンポーネント記述子ファイルを作成し、service-component マニフェストヘッダーを設定します。

**注意：**&#x200B;執筆時点では、Maven の scr プラグインは Eclipse の m2e プラグインと互換性がありません（[Felix bug 3170](https://issues.apache.org/jira/browse/FELIX-3170) を参照）。Eclipse IDE を使用するには、Maven をインストールして、コマンドラインインターフェイスでビルドを実行します。

#### サンプル POM ファイル {#example-pom-file}

```xml
<project xmlns="https://maven.apache.org/POM/4.0.0"
  xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.adobe.example.myapp</groupId>
  <artifactId>workflow-mbean</artifactId>
  <version>0.0.2-SNAPSHOT</version>
  <name>mbean-simple</name>
  <url>www.adobe.com</url>
  <description>A simple MBean</description>
  <packaging>bundle</packaging>
    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>
    <build>
        <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-compiler-plugin</artifactId>
            <configuration>
                <source>1.5</source>
                <target>1.5</target>
            </configuration>
        </plugin>
            <plugin>
                <groupId>org.apache.felix</groupId>
                <artifactId>maven-scr-plugin</artifactId>
                <version>1.7.2</version>
                <executions>
                    <execution>
                        <id>generate-scr-scrdescriptor</id>
              <goals>
                 <goal>scr</goal>
              </goals>
            </execution>
         </executions>
            </plugin>
             <plugin>
            <groupId>org.apache.felix</groupId>
            <artifactId>maven-bundle-plugin</artifactId>
            <version>1.4.3</version>
            <extensions>true</extensions>
            <configuration>
                <instructions>
                    <Export-Package>com.adobe.example.myapp.*;version=${project.version}</Export-Package>
                </instructions>
            </configuration>
        </plugin>
        </plugins>
    </build>
    <dependencies>
        <dependency>
            <groupId>org.apache.felix</groupId>
            <artifactId>org.apache.felix.scr.annotations</artifactId>
            <version>1.6.0</version>
            <scope>provided</scope>
        </dependency>
         <dependency>
            <groupId>org.apache.sling</groupId>
            <artifactId>org.apache.sling.api</artifactId>
            <version>2.0.8</version>
            <scope>provided</scope>
        </dependency>
         <dependency>
            <groupId>org.apache.felix</groupId>
            <artifactId>org.apache.felix.scr</artifactId>
            <version>1.6.1-R1236132</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>org.apache.sling</groupId>
            <artifactId>org.apache.sling.jcr.api</artifactId>
            <version>2.0.4</version>
        </dependency>
        <dependency>
            <groupId>com.adobe.granite</groupId>
            <artifactId>com.adobe.granite.jmx</artifactId>
            <version>0.1.6</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
       <groupId>com.day.cq.wcm</groupId>
       <artifactId>cq-wcm-mobile-api</artifactId>
       <version>5.5.2</version>
       <scope>provided</scope>
      </dependency>
      <dependency>
       <groupId>com.day.cq.workflow</groupId>
       <artifactId>cq-workflow-api</artifactId>
       <version>5.5.0</version>
       <scope>provided</scope>
      </dependency>
      <dependency>
       <groupId>javax.jcr</groupId>
       <artifactId>jcr</artifactId>
       <version>2.0</version>
       <scope>provided</scope>
      </dependency>
      <dependency>
                <groupId>org.slf4j</groupId>
  <artifactId>slf4j-api</artifactId>
  <version>1.6.4</version>
  <scope>provided</scope>
 </dependency>
    </dependencies>
</project>
```

公開されているアドビリポジトリを使用するには、以下のプロファイルを Maven 設定ファイルに追加します。

#### Maven プロファイル {#maven-profile}

```xml
<profile>
    <id>adobe-public</id>
    <activation>
         <activeByDefault>false</activeByDefault>
    </activation>
    <properties>
         <releaseRepository-Id>adobe-public-releases</releaseRepository-Id>
         <releaseRepository-Name>Adobe Public Releases</releaseRepository-Name>
         <releaseRepository-URL>https://repo.adobe.com/nexus/content/groups/public</releaseRepository-URL>
    </properties>
    <repositories>
         <repository>
             <id>adobe-public-releases</id>
             <name>Adobe Basel Public Repository</name>
             <url>https://repo.adobe.com/nexus/content/groups/public</url>
             <releases>
                 <enabled>true</enabled>
                 <updatePolicy>never</updatePolicy>
             </releases>
             <snapshots>
                 <enabled>false</enabled>
             </snapshots>
         </repository>
     </repositories>
     <pluginRepositories>
         <pluginRepository>
             <id>adobe-public-releases</id>
             <name>Adobe Basel Public Repository</name>
             <url>https://repo.adobe.com/nexus/content/groups/public</url>
             <releases>
                 <enabled>true</enabled>
                 <updatePolicy>never</updatePolicy>
             </releases>
             <snapshots>
                 <enabled>false</enabled>
             </snapshots>
         </pluginRepository>
     </pluginRepositories>
</profile>
```
