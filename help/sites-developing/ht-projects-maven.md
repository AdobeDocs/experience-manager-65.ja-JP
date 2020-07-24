---
title: Apache Maven を使用して AEM プロジェクトをビルドする方法
seo-title: Apache Maven を使用して AEM プロジェクトをビルドする方法
description: このドキュメントでは、Apache Maven に基づく AEM プロジェクトを設定する方法について説明します
seo-description: このドキュメントでは、Apache Maven に基づく AEM プロジェクトを設定する方法について説明します
uuid: 5db68639-7393-48b7-9d81-5b19b596ff21
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
discoiquuid: 3ebc1d22-a7a2-4375-9aa5-a18a7ceb446a
docset: aem65
translation-type: tm+mt
source-git-commit: 3b64b1fe5d47f115681608f38e7e53d078c4698e
workflow-type: tm+mt
source-wordcount: '2424'
ht-degree: 56%

---


# Apache Maven を使用して AEM プロジェクトをビルドする方法{#how-to-build-aem-projects-using-apache-maven}

## 概要 {#overview}

このドキュメントでは、[Apache Maven](https://maven.apache.org/) に基づく AEM プロジェクトを設定する方法について説明します。

Apache Maven は、ビルドを自動化し、質の高いプロジェクト情報を提供してソフトウェアプロジェクトを管理するためのオープンソースツールです。これは、AEM プロジェクト用に推奨されるビルド管理ツールです。

Maven に基づく AEM プロジェクトのビルドには以下のメリットがあります。

* IDE に依存しない開発環境
* アドビが提供する Maven のアーキタイプおよびアーティファクトの使用
* Maven ベースの開発の設定用の Apache Sling および Apache Felix ツールセットの使用
* IDE への読み込みが容易（Eclipse、IntelliJ など）
* 継続的インテグレーションシステムとの統合が容易

### Maven Project Archetypes {#maven-project-archetypes}

アドビでは、AEMプロジェクトのベースラインとして機能する2つのMavenアーキタイプを提供しています。 詳しくは、以下のリンクを参照してください。

* [AEMプロジェクトのアーキタイプ](https://github.com/adobe/aem-project-archetype)
* [単一ページアプリ用のMavenアーキタイプスターターキット](https://github.com/adobe/aem-spa-project-archetype)

## Adobe Experience Manager API の依存関係 {#experience-manager-api-dependencies}

### What is the UberJar? {#what-is-the-uberjar}

「UberJar」は、アドビから提供される特別なJavaアーカイブ(JAR)ファイルに付けられる非公式な名前です。 これらのJARファイルには、Adobe Experience Managerが公開するパブリックJava APIがすべて含まれています。 制限付き外部ライブラリに加えて、特にApache Sling、Apache Jackrabbit、Apache Lucene、Google Guavaから提供されるAEMで利用可能なすべてのパブリックAPIと、画像処理に使用される2つのライブラリ（Werner RandelshoferのCY JPEG ImageIOライブラリとLibrary）が含ます。 UberJarにはAPIインターフェイスとクラスのみが含まれます。つまり、AEMのOSGiバンドルによってエクスポートされたインターフェイスとクラスのみが含まれます。 They also contain a *MANIFEST.MF* file containing the correct package export versions for all of these exported packages, thus ensuring that projects built against the UberJar have the correct package import ranges.

### Why did Adobe create the UberJars? {#why-did-adobe-create-the-uberjars}

これまで、開発者は様々な AEM ライブラリに対する個別の依存関係を比較的多数管理し、新しい API が使用されるたびに、個別の依存関係を 1 つ以上プロジェクトに追加する必要がありました。1 つのプロジェクトに UberJar を導入すると、30 個の個別の依存関係がプロジェクトから削除されます。

AEM 6.5以降、アドビでは次の2つのUberJarを提供しています。 非推奨のインターフェイスと、その非推奨のインターフェイスを削除するインターフェイスを含むインターフェイス。 ビルド時に明示的に1つを参照することで、お客様は、廃止されたコードに依存しているかどうかを理解する必要があります。

2つ目のUber Jarは、非推奨のクラス、メソッド、プロパティを削除するので、ユーザーは、これらのクラス、メソッド、プロパティに対してコンパイルを行い、カスタムコードが将来の配達確認であるかを把握できます。

### 使用するUberJar {#which-uberjar-to-use}

AEM 6.5には、Uber Jarの2種類の味があります。

1. Uber Jar — 非推奨とマークされていないパブリックインターフェイスのみを含みます。 これは、将来の配達確認でコードベースが非推奨APIに依存しなくなるのを助けるため、 **UberJarを使用することを推奨します** 。
1. 非推奨のAPIを持つUber Jar — 今後のAEMのバージョンで非推奨とマークされているものを含め、すべてのパブリックインターフェイスが含まれます。

### UberJarsの使用方法 {#how-do-i-use-the-uberjars}

If you are using Apache Maven as a build system (which is the case for most AEM Java projects), you will need to add one or two elements to your *pom.xml* file. The first is a *dependency* element adding the actual dependency to your project:

**Uber Jar依存関係&#x200B;*（非推奨APIは除く）***

```xml
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.5.0</version>
    <classifier>apis</classifier>
    <scope>provided</scope>
</dependency>
```

**非推奨のAPIを含むUber Jar依存関係**

>[!CAUTION]
>
>アドビでは、今後のバージョンのAEMでアプリケーションが正しく動作するように、非推奨のAPIが**** *含まれていないUber Jarに対してデプロイすることをお勧めします。
>
>非推奨のAPIに依存するコードを変更して変更内容に合わせることができない場合にのみ、Uber Jarと非推奨のAPIのサポートを使用してください。

```xml
<dependency>
    <groupId>com.adobe.aem</groupId>
    <artifactId>uber-jar</artifactId>
    <version>6.5.0</version>
    <classifier>apis-with-deprecations</classifier>
    <scope>provided</scope>
</dependency>
```

Sonatype Nexus、Apache Archiva または JFrog Artifactory などの Maven Repository Manager を既に使用している場合は、このリポジトリマネージャーを参照するための適切な設定をプロジェクトに追加し、使用しているリポジトリマネージャーにアドビの Maven リポジトリ（[https://repo.adobe.com/nexus/content/groups/public/](https://repo.adobe.com/nexus/content/groups/public/)）を追加します。

If you are not using a repository manager, then you will need to add a *repository* element to your *pom.xml* file:

```xml
<repositories>
    <repository>
        <id>adobe-public-releases</id>
        <name>Adobe Public Repository</name>
        <url>https://repo.adobe.com/nexus/content/groups/public/</url>
        <layout>default</layout>
    </repository>
</repositories>
<pluginRepositories>
    <pluginRepository>
        <id>adobe-public-releases</id>
        <name>Adobe Public Repository</name>
        <url>https://repo.adobe.com/nexus/content/groups/public/</url>
        <layout>default</layout>
    </pluginRepository>
</pluginRepositories>
```

### What can I do with the UberJar? {#what-can-i-do-with-the-uberjar}

UberJar を使用して、AEM API（およびプロジェクトが使用する前述の API）に依存するプロジェクトコードをコンパイルできます。OSGi Service Component Runtime（SCR）および OSGi Metatype 情報も生成できます。いくつかの制限はありますが、単体テストを作成して実行することもできます。

### UberJar ではできないこと {#what-can-t-i-do-with-the-uberjar}

Because the UberJar contains **only** APIs, it is not executable and cannot be used to **run** Adobe Experience Manager. AEM を実行するには、スタンドアロンまたは Web Application Archive（WAR）形式の AEM Quickstart が必要です。

### 単体テストに関する制限について {#you-mentioned-limitations-on-unit-tests-please-explain-further}

一般的に、単体テストは 3 つの方法で製品 API とやり取りします。いずれの方法も、UberJar によって少しずつ異なる影響を受けます。

#### ユースケース 1 - API インターフェイスを呼び出すカスタムコード {#use-case-custom-code-which-calls-a-api-interface}

これは最も一般的なケースで、AEM API で定義されている Java インターフェイスのメソッドをカスタムコードで実行します。このインターフェイスの実装は、直接提供することも、依存関係挿入パターンを使用して挿入することもできます。**この使用例は、UberJarを使用して処理できます。**

前者の例を以下に示します。

```java
public class ClassWhichHasAEMInterfacePassedIn {
    /**
     * Get the first length characters of the page title.
     */
    public String getTrimmedTitle(Page page, int length) {
         String title = page.getTitle();
         return StringUtils.left(title, length);
    }
}
```

後者の例を以下に示します。

```java
@Component
@Service
public class ComponentWhichHasAEMInterfaceInjected implements TitleTrimmer {
    @Reference
    private PageManagerFactory pageManagerFactory;

    /**
     * Get the first length characters of the title of the page containing the provided Resource.
     */
    public String getTrimmedTitle(Resource resource, int length) {
        PageManager pageManager = pageManagerFactory.getPageManager(resource.getResourceResolver());
        Page page = pageManager.getContainingPage(resource);
        if (page == null) {
           return null;
        }
        String title = page.getTitle();
        return StringUtils.left(title, length);
    }
}
```

To unit test either of these methods, a developer would use a mocking framework such as [JMockit](http://jmockit.github.io), [Mockito](https://mockito.org/), [JMock](https://www.jmock.org/), or [Easymock](https://easymock.org/) to create a mock object for the AEM API referenced. この例では JMockit を使用していますが、特にこのユースケースでは、フレームワーク間の違いはあまりなく、構文的な相違に留まります。

```java
@RunWith(JMockit.class)
public class ClassWhichHasAEMInterfacePassedInTest {

    @Tested
    private ClassWhichHasAEMInterfacePassedIn instance;

    @Mocked
    private Page page;

    @Test
    public void test_that_long_string_is_trimmed() {
        new Expectations() {{
            page.getTitle();
            result = "a really really really really really long string";
        }};
        assertEquals("a really", instance.getTrimmedTitle(page, 8));
    }
}
```

```java
@RunWith(JMockit.class)
public class ComponentWhichHasAEMInterfaceInjectedTest {

    @Tested
    private ComponentWhichHasAEMInterfaceInjected instance;

    @Mocked
    private Page page;

    @Mocked
    private PageManager pageManager;

    @Injectable
    private PageManagerFactory pageManagerFactory;

    @Mocked
    private Resource resource;

    @Mocked
    private ResourceResolver resourceResolver;

    @Test
    public void test_that_long_string_is_trimmed() {
        new Expectations() {{
            resource.getResourceResolver();
            result = resourceResolver;
            pageManagerFactory.getPageManager(resourceResolver);
            result = pageManager;
            pageManager.getContainingPage(resource);
            result = page;
            page.getTitle();
            result = "a really really really really really long string";
        }};
        assertEquals("a really", instance.getTrimmedTitle(resource, 8));
    }
}
```

#### ユースケース 2 - API 実装クラスを呼び出すカスタムコード {#use-case-custom-code-which-calls-an-api-implementation-class}

このユースケースでは、AEM API のクラスの静的メソッドまたはインスタンスメソッドを呼び出します。つまり、ユースケース 1 のようにインターフェイスを参照するのではなく、具象クラスを参照します。

```java
public class ClassWhichUsesAStaticMethodFromAPI {

    /**
     * Get a map of asset titles to asset objects.
     *
     * @param resource either an asset resource or a folder containing assets.
     * @return an map of titles to assets. if an asset doesn't have a title, the name is used instead.
     */
    public Map<String, Asset> getAssetTitles(Resource resource) {
        Iterator<Asset> assets = DamUtil.getAssets(resource);
        Map<String, Asset> result = new HashMap<String, Asset>();
        while (assets.hasNext()) {
            Asset asset = assets.next();
            String title = asset.getMetadataValue(DamConstants.DC_TITLE);
            if (title == null) {
                title = asset.getName();
            }
            result.put(title, asset);
        }
        return result;
    }
}
```

```java
public class ClassWhichUsesAnInstanceMethodFromAPI {

    /**
     * Count the number of paragraphs in a parsys.
     *
     * @param resource the parsys resource
     * @return the count
     */
    public int countParagraphs(Resource resource) {
        return new ParagraphSystem(resource).paragraphs().size();
    }
}
```

**このユースケースは UberJar で処理できます。**&#x200B;ただし、性能テストについては、可能であればやはり API のモックを作成することをお勧めします。

```java
@RunWith(JMockit.class)
public class ClassWhichUsesAStaticMethodFromAPITest {

    @Tested
    private ClassWhichUsesAStaticMethodFromAPI instance;

    @Mocked(stubOutClassInitialization = true)
    private DamUtil unusedDamUtil = null;

    @Mocked
    private Resource resource;

    @Test
    public void test_that_empty_iterator_produces_empty_map() {
        new Expectations() {
            {
                DamUtil.getAssets(resource);
                result = Collections.<Asset> emptySet().iterator();
            }
        };
        Map<String, Asset> result = new ClassWhichUsesAStaticMethodFromAPI().getAssetTitles(resource);
        assertNotNull(result);
        assertEquals(0, result.size());
    }
    @Test
    public void test_with_reference_search() {
        assertTrue(true);
    }
}
```

```java
@RunWith(JMockit.class)
public class ClassWhichUsesAnInstanceMethodFromAPITest {

    @Tested
    private ClassWhichUsesAnInstanceMethodFromAPI instance;

    @Mocked
    private Resource parsys;

    @Mocked
    private Paragraph firstPar;

    @Mocked
    private Paragraph secondPar;

    @Test
    public void test_empty_parsys_returns_zero() {
        new MockUp<ParagraphSystem>() {
            @Mock
            public void $init(Resource resource) {
                assertEquals(parsys, resource);
            }
            @Mock
            public List<Paragraph> paragraphs() {
                return Collections.<Paragraph> emptyList();
            }
        };
        assertEquals(0, instance.countParagraphs(parsys));
    }
}
```

#### ユースケース 3 - API のベースクラスを拡張するカスタムコード {#use-case-custom-code-which-extends-a-base-class-from-the-api}

As with SCR Generation, if your code extends a base class (abstract or concrete) from the AEM API, you **must** use the UberJar in order to test it.

## Maven を使用した一般的な開発タスク {#common-development-tasks-with-maven}

### content モジュールにパスを追加する方法 {#how-to-add-paths-to-the-content-module}

content モジュールには、Maven でビルドされる AEM パッケージ用のフィルターを定義する src/main/content/META-INF/vault/filter.xml ファイルが格納されます。Maven アーキタイプによって作成されるこのファイルは次のようになります。

#### src/main/content/META-INF/vault/filter.xml {#src-main-content-meta-inf-vault-filter-xml}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/apps/myproject"/>
</workspaceFilter>
```

このファイルは様々な方法で使用されます。

* パッケージにインクルードするコンテンツを決定するために `content-package-maven-plugin` で使用します。
* 考慮するパスを決定するために VLT ツールで使用します。
* AEM パッケージマネージャーでパッケージが再ビルドされる場合は、インクルードするパスもこのファイルで定義されます。

アプリケーションの要件によっては、次のような他のコンテンツをインクルードするためにこれらのパスを追加する必要があります。

* ロールアウト設定
* ブループリント
* ワークフローモデル
* デザインページ
* サンプルコンテンツ

To add to the paths, add more `<filter>` elements:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/apps/myproject"/>
    <filter root="/content/myproject/sample-content"/>
</workspaceFilter>
```

#### 同期をおこなわずにパスをパッケージに追加する方法 {#adding-paths-to-the-package-without-syncing-them}

If you have files that should be added to the package that is built by the content-package-maven-plugin but that should not be synchronized between the file system and the repository, you can use `.vltignore` files. These files have the same syntax as [.gitignore](https://www.kernel.org/pub/software/scm/git/docs/gitignore.html) files.

For example, the archetype uses a `.vltignore` file to prevent the JAR file that is installed as part of the bundle from being synced back to the file system:

#### src/main/content/jcr_root/apps/myproject/install/.vltignore {#src-main-content-jcr-root-apps-myproject-install-vltignore}

```xml
*.jar
```

#### パッケージにパスを追加せずにパスを同期する方法 {#syncing-paths-without-adding-them-to-the-package}

ファイルシステムとリポジトリとの間で特定のパスの同期を維持し、AEM にインストールするためにビルドするパッケージにはそのパスをインクルードしない場合があります。

通常は `/libs/foundation` パスです。 開発のためには、このパスの内容をファイルシステムで使用できるようにし、例えば、IDEで、内のJSPを含むJSP挿入を解決できるようにし `/libs`ます。 ただし、カスタム実装で変更してはならない製品コードがパーツに含まれているので、構築するパッケージにその `/libs` パーツを含めたくありません。

To achieve this, you can provide a file `src/main/content/META-INF/vault/filter-vlt.xml`. If this file exists, it will be used by the VLT tool, e.g. when you perform `vlt up` and `vlt ci`, or when you have set `vlt sync` set up. The content-package-maven-plugin will continue to use the file `src/main/content/META-INF/vault/filter.xml` when creating the package.

For example, to make `/libs/foundation` available locally for development, but only include `/apps/myproject` in the package, use the following two files.

#### src/main/content/META-INF/vault/filter.xml {#src-main-content-meta-inf-vault-filter-xml-1}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/apps/myproject"/>
</workspaceFilter>
```

#### src/main/content/META-INF/vault/filter-vlt.xml {#src-main-content-meta-inf-vault-filter-vlt-xml}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<workspaceFilter version="1.0">
    <filter root="/libs/foundation"/>
    <filter root="/apps/myproject"/>
</workspaceFilter>
```

また、これらのファイルをパッケージにインクルードしないように maven-resources-plugin を再設定する必要があります。パッケージのインストール時に filter.xml ファイルは適用されません。パッケージマネージャーを使用してパッケージが再びビルドされる場合にのみ適用されます。

Change the `<resources>` section in the content pom accoringly:

#### src/main/content/pom.xml {#src-main-content-pom-xml}

```xml
<!-- ... -->
<resources>
 <resource>
  <directory>src/main/content/jcr_root</directory>
  <filtering>false</filtering>
  <excludes>
   <exclude>**/.vlt</exclude>
   <exclude>**/.vltignore</exclude>
   <exclude>libs/</exclude>
  </excludes>
 </resource>
</resources>
<!-- ... -->
```

### JSPの使用方法 {#how-to-work-with-jsps}

これまでに説明した Maven 設定では、コンポーネントと対応する JSP もインクルードできるコンテンツパッケージを作成します。ただし、Maven では JSP をコンテンツパッケージに含まれるその他のファイルとして扱い、JSP として認識しません。

AEM でのコンポーネントの動作はまったく同じですが、Maven に JSP を認識させる処理には 2 つの主なメリットがあります。

* JSP にエラーが含まれている場合に Maven を失敗させることができるので、JSP が最初に AEM にコンパイルされるときではなく、ビルド時にエラーを特定できます。
* Maven プロジェクトを読み込むことのできる IDE の場合、コード補完とタグライブラリのサポートが JSP で有効になります。

この設定を有効にするには、次の 2 つの処理が必要です。

1. タグライブラリの依存関係を追加する
1. Maven コンパイルプロセスの一環として JSP をコンパイルする

#### タグライブラリの依存関係の追加 {#adding-tag-library-dependencies}

以下に示す依存関係を `content` モジュールの POM に追加する必要があります。

>[!NOTE]
>
>Unless you are importing the product dependencies as described in [Importing AEM Product Dependencies](#importingaemproductdependencies) above, they also need to be added to the parent POM along with the version matching your AEM setup as described in [Adding Dependencies](#addingdependencies) above. The comments in each entry below show the package to search for in the Dependency Finder.

>[!NOTE]
>
>`com.adobe.granite.xssprotection` アーティファクトは cq-quickstart-product-dependencies POM にインクルードされません。このアーティファクトには、Dependency Finder から取得されるすべての Maven コーディネートが必要です。

#### Maven の compile フェーズの一環としての JSP のコンパイル {#compiling-jsps-as-part-of-the-maven-compile-phase}

To compile JSPs in Maven&#39;s `compile` phase, we use Apache Sling&#39;s [Maven JspC Plugin](https://sling.apache.org/documentation/development/jspc.html) as shown below:

* `jspc` ゴール（デフォルトで `compile` フェーズにバインドされるので、フェーズを明示的に指定する必要はありません）の実行を設定します。

* we tell it to compile any JSPs in `${project.build.directory}/jsps-to-compile`
* and output the result to `${project.build.directory}/ignoredjspc` (which translates to `myproject/content/target/ignoredjspc`)

* we set up maven-resources-plugin to copy the JSPs to `${project.build.directory}/jsps-to-compile` in the generate-sources phase and configure it to not copy the `libs/` folder (because that is AEM product code and we neither want to incur the dependencies for compilation for our project, nor do we need to validate that it compiles.

前述のとおり、第 1 の目的は JSP を検証し、JSP にエラーが含まれている場合にビルドプロセスを失敗させることです。そのため、無視される（実際には後ですぐに削除される）個別のディレクトリに対して JSP をコンパイルします。

また、Maven JspC Plugin の結果を OSGi バンドルの一部としてバンドルおよびデプロイすることもできますが、これにより他の影響や副作用が生じ、JSP の検証という目的を逸脱してしまいます。

JSPからコンパイルされたクラスを削除するために、Maven Clean Pluginを次のように設定しました。 Maven JspCプラグインの結果を調べたい場合は、を実行 `mvn compile` し `myproject/content` ます。その後、結果はに表示され `myproject/content/target/ignoredjspc`ます。

#### myproject/content/pom.xml {#myproject-content-pom-xml}

```xml
<build>
  <!-- ... -->
  <plugins>
    <!-- ... -->
    <plugin>
      <artifactId>maven-resources-plugin</artifactId>
      <executions>
        <execution>
          <id>copy-resources</id>
          <phase>generate-sources</phase>
          <goals>
            <goal>copy-resources</goal>
          </goals>
          <configuration>
            <outputDirectory>${project.build.directory}/jsps-to-compile</outputDirectory>
            <resources>
              <resource>
                <directory>src/main/content/jcr_root</directory>
                <excludes>
                  <exclude>libs/**</exclude>
                </excludes>
              </resource>
            </resources>
          </configuration>
        </execution>
      </executions>
    </plugin>
    <plugin>
      <groupId>org.apache.sling</groupId>
      <artifactId>maven-jspc-plugin</artifactId>
      <version>2.0.6</version>
      <executions>
        <execution>
          <id>compile-jsp</id>
          <goals>
            <goal>jspc</goal>
          </goals>
          <configuration>
            <jasperClassDebugInfo>false</jasperClassDebugInfo>
            <sourceDirectory>${project.build.directory}/jsps-to-compile</sourceDirectory>
            <outputDirectory>${project.build.directory}/ignoredjspc</outputDirectory>
          </configuration>
        </execution>
      </executions>
    </plugin>
    <plugin>
      <artifactId>maven-clean-plugin</artifactId>
      <executions>
        <execution>
          <id>remove-compiled-jsps</id>
          <goals>
            <goal>clean</goal>
          </goals>
          <phase>process-classes</phase>
          <configuration>
            <excludeDefaultDirectories>true</excludeDefaultDirectories>
            <filesets>
              <fileset>
                <directory>${project.build.directory}/jsps-to-compile</directory>
                <directory>${project.build.directory}/ignoredjspc</directory>
              </fileset>
            </filesets>
          </configuration>
        </execution>
      </executions>
    </plugin>
  </plugins>
</build>
```

>[!NOTE]
>
>Depending on whether you actually make use of JSP code in `/libs` (i.e. include JSPs from there), you will need to refine which JSPs are copied for compilation.
>
>E.g. if you include `/libs/foundation/global.jsp`, you can use the following configuration for the `maven-resources-plugin` instead of the configuration above which completely skips over `/libs`.
>
>
```
> <resource>  
>           <directory>src/main/content/jcr_root</directory>  
>           <includes>  
>                   <include>apps/**</include>  
>                   <include>libs/foundation/global.jsp</include>
>       </includes>  
>   </resource>  
>```

### SCM システムを使用する方法 {#how-to-work-with-scm-systems}

ソース設定管理（SCM）を使用する場合は、次のことを確認する必要があります。

* VCS がファイルシステム内のソース以外のアーティファクトを無視する
* VLT が VCS のアーティファクトを無視し、それらをリポジトリにチェックインしない

>[!NOTE]
>
>この説明には、SCM を使用するように Maven を設定する方法は含まれていません。この方法について詳しくは、[Maven の POM リファレンス](https://maven.apache.org/pom.html#SCM)および [Maven SCM Plugin のドキュメント](https://maven.apache.org/scm/)を参照してください。

#### SCM から除外するパターン {#patterns-to-exclude-from-scm}

次に、SCMから含めるパターンの一般的なリストを示します。 例えば、gitを使用している場合は、これらをプロジェクトの `.gitignore` ファイルに追加できます。

#### サンプルの .gitignore {#sample-gitignore}

```shell
# Ignore VLT files
.vlt
.vlt-sync.log
.vlt-sync-config.properties

# Ignore Quickstart launches in the source tree
license.properties
crx-quickstart

# Ignore compilation results
target

# Ignore IDE and Operating System artifacts
.idea
.classpath
.metadata
.project
.settings
maven-eclipse.xml
*.iml
*.ipr
*.iws
.DS_Store
```

#### VLT での SCM 制御ファイルの無視 {#ignoring-scm-control-files-in-vlt}

リポジトリにチェックインしたくないコンテンツのソースツリーに SCM 制御ファイルが含まれている場合があります。

次の状況について考えてみましょう。

インストールしたバンドルの jar ファイルがファイルシステムに同期されないようにするために、アーキタイプでは既に .vltignore ファイルを作成済みです。

#### src/main/content/jcr_root/apps/myproject/install/.vltignore {#src-main-content-jcr-root-apps-myproject-install-vltignore-1}

```shell
*.jar
```

当然、このファイルは SCM に追加したくないので、例えば git を使用する場合は、対応する `gitignore`.  ファイルを追加します。

#### src/main/content/jcr_root/apps/myproject/install/.gitignore {#src-main-content-jcr-root-apps-myproject-install-gitignore}

```shell
*.jar
```

を参照してください。 `gitignore` ファイルはリポジトリ(. `vltignore` ファイルを拡張して、を含める必要があります。 `gitignore` file:

#### src/main/content/jcr_root/apps/myproject/install/.vltignore {#src-main-content-jcr-root-apps-myproject-install-vltignore-2}

```shell
*.jar
.gitignore
```

### デプロイメントプロファイルを使用する方法 {#how-to-work-with-deployment-profiles}

ビルドプロセスが大規模な開発ライフサイクル管理の設定（継続的インテグレーションプロセスなど）に含まれている場合は、開発者のローカルインスタンスだけではなく、他のマシンへのデプロイが必要になることが多くなります。

このようなシナリオでは、プロジェクトの POM に新しい [Maven のビルドプロファイル](https://maven.apache.org/guides/introduction/introduction-to-profiles.html)を簡単に追加できます。

次に示す例では、`integrationServer` というプロファイルを追加します。このプロファイルでは、オーサーインスタンスとパブリッシュインスタンス用のホスト名とポートを再定義します。次に示すようにプロジェクトのルートから maven を実行して、これらのサーバーにデプロイできます。

```shell
# install on integration test author
$ mvn -PautoInstallPackage -PintegrationServer install

# install on integration test publisher
$ mvn -PautoInstallPackagePublish -PintegrationServer install
```

#### myproject/pom.xml {#myproject-pom-xml}

```xml
<profiles>

    <!-- ... -->

    <profile>
        <id>integrationServer</id>
        <properties>
            <crx.host>dev-author.intranet</crx.host>
            <crx.port>5502</crx.port>
            <publish.crx.host>dev-publish.intranet</publish.crx.host>
            <publish.crx.port>5503</publish.crx.port>
        </properties>
    </profile>
</profiles>
```

### AEM Communities と連携する方法 {#how-to-work-with-aem-communities}

AEM Communities 機能をライセンス許可するときは、追加の API jar が必要になります。

詳しくは、[コミュニティに Maven を使用](/help/communities/maven.md)を参照してください。
