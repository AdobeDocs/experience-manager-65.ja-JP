---
title: メディアハンドラーとワークフローを使用したアセットの処理
description: メディアハンドラーについて、およびワークフローを使用してデジタルアセットに対してタスクを実行する方法について説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: 99ce6e0572797b7bccf755aede93623be6bd5698
workflow-type: tm+mt
source-wordcount: '2197'
ht-degree: 71%

---


# Process assets using media handlers and workflows {#processing-assets-using-media-handlers-and-workflows}

Adobe Experience Manager（AEM）Assets には、アセットを処理するためのデフォルトのワークフローとメディアハンドラーのセットが付属しています。ワークフローは、アセットに対して実行されるタスクを定義し、特定のタスク(サムネールの生成やメタデータ抽出など)をメディアハンドラーに委任します。

特定のMIMEタイプのアセットがアップロードされたときに、自動的に実行されるようにワークフローを設定できます。 処理手順は、一連のAEM Assetsメディアハンドラーに関して定義されます。 AEM には、[組み込みのハンドラー](#default-media-handlers)がいくつか用意されています。さらに、追加のハンドラーを[カスタムで開発](#creating-a-new-media-handler)したり、処理を[コマンドラインツール](#command-line-based-media-handler)に委任して定義したりできます。

メディアハンドラーは、アセットに対して特定の処理を実行する AEM Assets 内のサービスです。例えば、MP3 オーディオファイルを AEM にアップロードすると、ワークフローは MP3 ハンドラーを呼び出し、MP3 ハンドラーはメタデータを抽出してサムネールを生成します。通常、メディアハンドラーはワークフローと組み合わせて使用されます。AEM 内では、よく使用される MIME タイプがサポートされています。アセットに対して特定のタスクを実行するには、ワークフローを拡張または作成するか、メディアハンドラーを拡張または作成するか、メディアハンドラーを無効または有効にします。

>[!NOTE]
>
>AEM Assets でサポートされるすべての形式と、各形式でサポートされる機能の説明については、[Assets でサポートされる形式](assets-formats.md)を参照してください。

## Default media handlers {#default-media-handlers}

AEM Assets 内では以下のメディアハンドラーを使用できます。また、これらのメディアハンドラーはよく使用される MIME タイプを処理できます。

<!-- TBD: Apply correct formatting once table is moved to MD.
-->

| ハンドラー名 | サービス名（システムコンソールでの名称） | サポートされる MIME タイプ |
|---|---|---|
| [!UICONTROL TextHandler] | `com.day.cq.dam.core.impl.handler.TextHandler` | text/plain |
| [!UICONTROL PdfHandler] | `com.day.cq.dam.handler.standard.pdf.PdfHandler` | <ul><li>application/pdf</li><li>application/illustrator</li></ul> |
| [!UICONTROL JpegHandler] | `com.day.cq.dam.core.impl.handler.JpegHandler` | image/jpeg |
| [!UICONTROL Mp3Handler] | `com.day.cq.dam.handler.standard.mp3.Mp3Handler` | audio/mpeg |
| [!UICONTROL ZipHandler] | `com.day.cq.dam.handler.standard.zip.ZipHandler` | <ul><li>application/java-archive </li><li> application/zip</li></ul> |
| [!UICONTROL PictHandler] | `com.day.cq.dam.handler.standard.pict.PictHandler` | image/pict |
| [!UICONTROL StandardImageHandler] | `com.day.cq.dam.core.impl.handler.StandardImageHandler` | <ul><li>image/gif </li><li> image/png </li> <li>application/photoshop </li> <li>image/jpeg </li><li> image/tiff </li> <li>image/x-ms-bmp </li><li> image/bmp</li></ul> |
| [!UICONTROL MSOfficeHandler] | `com.day.cq.dam.handler.standard.msoffice.MSOfficeHandler` | application/msword |
| [!UICONTROL MSPowerPointHandler] | `com.day.cq.dam.handler.standard.msoffice.MSPowerPointHandler` | application/vnd.ms-powerpoint |
| [!UICONTROL OpenOfficeHandler] | `com.day.cq.dam.handler.standard.ooxml.OpenOfficeHandler` | <ul><li>application/vnd.openxmlformats-officedocument.wordprocessingml.document</li><li> application/vnd.openxmlformats-officedocument.spreadsheetml.sheet</li><li> application/vnd.openxmlformats-officedocument.presentationml.presentation</li></ul> |
| [!UICONTROL EPubHandler] | `com.day.cq.dam.handler.standard.epub.EPubHandler` | application/epub+zip |
| [!UICONTROL GenericAssetHandler] | `com.day.cq.dam.core.impl.handler.GenericAssetHandler` | アセットからデータを抽出するためのハンドラーが他に見つからなかった場合のフォールバック |

すべてのハンドラーは以下のタスクを実行できます。

* アセットから使用できるすべてのメタデータを抽出する
* アセットのサムネール画像の作成

アクティブなメディアハンドラを表示するには：

1. In your browser, navigate to `http://localhost:4502/system/console/components`.
1. 「`com.day.cq.dam.core.impl.store.AssetStoreImpl`」をクリックします。
1. すべてのアクティブなメディアハンドラーリストが表示されます。次に例を示します。

![chlimage_1-437](assets/chlimage_1-437.png)

## Use media handlers in workflows to perform tasks on assets {#using-media-handlers-in-workflows-to-perform-tasks-on-assets}

通常、メディアハンドラーはワークフローと組み合わせて使用されるサービスです。

AEM には、アセットを処理するデフォルトのワークフローがいくつかあります。ワークフローを表示するには、ワークフローコンソールを開き、「**[!UICONTROL モデル]**」タブをクリックします。「AEM Assets」から始まるワークフロータイトルは、アセット固有のタイトルです。

特定の要件に従って、既存のワークフローを拡張し、新しいワークフローを作成してアセットを処理できます。

以下の例は、**[!UICONTROL AEM Assets 同期]**&#x200B;ワークフローを拡張して、PDF ドキュメント以外のすべてのアセットについてサブアセットを生成するための方法を示しています。

### メディアハンドラーの無効化または有効化 {#disabling-enabling-a-media-handler}

メディアハンドラーを無効または有効にするには、Apache Felix Web Management Console を使用します。メディアハンドラーを無効にすると、そのアセットに対してメディアハンドラーのタスクは実行されません。

メディアハンドラーを有効または無効にするための手順

1. ブラウザーで、`https://<host>:<port>/system/console/components` です。
1. メディアハンドラーの名前の横にある「**[!UICONTROL Disable]**」をクリックします。例：`com.day.cq.dam.handler.standard.mp3.Mp3Handler`
1. ページを更新します。メディアハンドラーの横に、無効であることを示すアイコンが表示されます。
1. メディアハンドラーを有効にするには、メディアハンドラーの名前の横にある「**[!UICONTROL Enable]**」をクリックします。

### Create a new media handler {#creating-a-new-media-handler}

新しいメディアタイプをサポートしたり、アセットで特定のタスクを実行したりするには、新しいメディアハンドラーを作成する必要があります。ここでは、その進め方について説明します。

#### Important classes and interfaces {#important-classes-and-interfaces}

実装を開始するための最適な方法は、最も多くの点について対応し、適切なデフォルト動作を提供している付属の抽象実装から継承することです。それが `com.day.cq.dam.core.AbstractAssetHandler` クラスです。

このクラスには、抽象的なサービス記述子が用意されています。そのため、このクラスから継承し、maven-sling-plugin を使用する場合、inherit フラグを `true` に設定する必要があります。

次のメソッドを実装します。

* `extractMetadata()`：使用可能なすべてのメタデータを抽出します。
* `getThumbnailImage()`：渡されたアセットからサムネール画像を作成します。
* `getMimeTypes()`：アセットの MIME タイプを返します。

以下にテンプレートの例を示します。

```Java
package my.own.stuff; /** * @scr.component inherit="true" * @scr.service */ public class MyMediaHandler extends com.day.cq.dam.core.AbstractAssetHandler { // implement the relevant parts }
```

インターフェイスとクラスには以下が含まれます。

* `com.day.cq.dam.api.handler.AssetHandler` インターフェイス：特定の MIME タイプのサポートを追加するサービスを記述します。新しい MIME タイプを追加するには、このインターフェイスを実装する必要があります。このインターフェイスには、特定のドキュメントの読み込みと書き出し、サムネールの作成およびメタデータの抽出をおこなうメソッドがあります。
* `com.day.cq.dam.core.AbstractAssetHandler` クラス：その他すべてのアセットハンドラー実装の基礎として機能し、よく使用される機能を提供します。
* `com.day.cq.dam.core.AbstractSubAssetHandler` クラス：
   * このクラスは、他のすべてのアセットハンドラーの実装の基礎として機能し、共通の使用済み機能と、サブアセット抽出の共通の使用済み機能を提供します。
   * 実装を開始する最善の方法は、ほとんどの処理を行い、適切なデフォルト動作を提供する、提供された抽象実装から継承することです。 com.day.cq.dam.core.AbstractAssetHandlerクラス
   * このクラスには、抽象的なサービス記述子が用意されています。そのため、このクラスから継承し、maven-sling-plugin を使用する場合、inherit フラグを true に設定する必要があります。

以下のメソッドを実装する必要があります。

* `extractMetadata()`：使用できるすべてのメタデータを抽出します。
* `getThumbnailImage()`：渡されたアセットのサムネール画像を作成します。
* `getMimeTypes()`：アセットの MIME タイプを返します。

以下にテンプレートの例を示します。

package my.own.stuff; /&amp;ast;&amp;ast; &amp;ast; @scr.component inherit=&quot;true&quot; &amp;ast; @scr.service &amp;ast;/ public class MyMediaHandler extends com.day.cq.dam.core.AbstractAssetHandler { // 関係する部分を実装 }

インターフェイスとクラスには以下が含まれます。

* `com.day.cq.dam.api.handler.AssetHandler` インターフェイス：特定の MIME タイプのサポートを追加するサービスを記述します。新しい MIME タイプを追加するには、このインターフェイスを実装する必要があります。このインターフェイスには、特定のドキュメントの読み込みと書き出し、サムネールの作成およびメタデータの抽出をおこなうメソッドがあります。
* `com.day.cq.dam.core.AbstractAssetHandler` クラス：その他すべてのアセットハンドラー実装の基礎として機能し、よく使用される機能を提供します。
* `com.day.cq.dam.core.AbstractSubAssetHandler` クラス：その他すべてのアセットハンドラー実装の基礎として機能し、よく使用される機能を提供します。さらに、サブアセットの抽出についてよく使用される機能も提供します。

#### Example: create a specific text handler {#example-create-a-specific-text-handler}

ここでは、透かしありのサムネールを生成する固有の Text Handler を作成します。

以下の手順を実行します。

Mavenプラグインを使用してEclipseをインストールおよび設定し、Mavenプロジェクトに必要な依存関係を設定する方法については、 [開発ツール](../sites-developing/dev-tools.md) （英語）を参照してください。

以下の手順を実行した後、txt ファイルを AEM にアップロードすると、ファイルのメタデータが抽出され、透かしありの 2 つのサムネールが生成されます。

1. Eclipseで、Mavenプロジェクトを作成し `myBundle` ます。

   1. In the Menu bar, click **[!UICONTROL File > New > Other]**.
   1. In the dialog, expand the Maven folder, select Maven Project and click **[!UICONTROL Next]**.
   1. Check the Create a simple project box and the Use default Workspace locations box, then click **[!UICONTROL Next]**.
   1. Maven プロジェクトを定義します。

      * Group Id：com.day.cq5.myhandler
      * Artifact Id：myBundle
      * Name：My AEM バンドル
      * Description：これは AEM バンドルです
   1. 「**[!UICONTROL Finish]**」をクリックします。


1. Javaコンパイラをバージョン1.5に設定します。

   1. Right-click the `myBundle` project, select Properties.
   1. 「Java Compiler」を選択して、次のプロパティを 1.5 に設定します。

      * Compiler compliance level
      * Generated .class files compatibility
      * Source compatibility
   1. 「**[!UICONTROL OK]**」をクリックします。In the dialog window, click **[!UICONTROL Yes]**.


1. Replace the code in the `pom.xml` file with the following code:

   ```xml
   <project xmlns="https://maven.apache.org/POM/4.0.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="https://maven.apache.org/POM/4.0.0 https://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <!-- ====================================================================== -->
    <!-- P A R E N T P R O J E C T D E S C R I P T I O N -->
    <!-- ====================================================================== -->
    <parent>
     <groupId>com.day.cq.dam</groupId>
     <artifactId>dam</artifactId>
     <version>5.2.14</version>
     <relativePath>../parent</relativePath>
    </parent>
    <!-- ====================================================================== -->
    <!-- P R O J E C T D E S C R I P T I O N -->
    <!-- ====================================================================== -->
    <groupId>com.day.cq5.myhandler</groupId>
    <artifactId>myBundle</artifactId>
    <name>My CQ5 bundle</name>
    <version>0.0.1-SNAPSHOT</version>
    <description>This is my CQ5 bundle</description>
    <packaging>bundle</packaging>
    <!-- ====================================================================== -->
    <!-- B U I L D D E F I N I T I O N -->
    <!-- ====================================================================== -->
    <build>
     <plugins>
      <plugin>
       <groupId>org.apache.felix</groupId>
       <artifactId>maven-scr-plugin</artifactId>
      </plugin>
      <plugin>
       <groupId>org.apache.sling</groupId>
       <artifactId>maven-sling-plugin</artifactId>
       <configuration>
        <slingUrlSuffix>/libs/dam/install/</slingUrlSuffix>
       </configuration>
      </plugin>
      <plugin>
       <groupId>org.apache.felix</groupId>
       <artifactId>maven-bundle-plugin</artifactId>
       <extensions>true</extensions>
       <configuration>
        <instructions>
         <Bundle-Category>cq5</Bundle-Category>
         <Export-Package> com.day.cq5.myhandler </Export-Package>
        </instructions>
       </configuration>
      </plugin>
     </plugins>
    </build>
    <!-- ====================================================================== -->
    <!-- D E P E N D E N C I E S -->
    <!-- ====================================================================== -->
    <dependencies>
     <dependency>
      <groupId>com.day.cq.dam</groupId>
      <artifactId>cq-dam-api</artifactId>
      <version>5.2.10</version>
      <scope>provided</scope>
     </dependency>
     <dependency>
      <groupId>com.day.cq.dam</groupId>
      <artifactId>cq-dam-core</artifactId>
      <version>5.2.10</version>
      <scope>provided</scope>
     </dependency>
     <dependency>
      <groupId>com.day.cq</groupId>
      <artifactId>cq-commons</artifactId>
     </dependency>
     <dependency>
      <groupId>javax.jcr</groupId>
      <artifactId>jcr</artifactId>
     </dependency>
     <dependency>
      <groupId>org.apache.felix</groupId>
      <artifactId>org.osgi.compendium</artifactId>
     </dependency>
     <dependency>
      <groupId>org.slf4j</groupId>
      <artifactId>slf4j-api</artifactId>
     </dependency>
     <dependency>
      <groupId>commons-lang</groupId>
      <artifactId>commons-lang</artifactId>
     </dependency>
     <dependency>
      <groupId>commons-collections</groupId>
      <artifactId>commons-collections</artifactId>
     </dependency>
     <dependency>
      <groupId>commons-io</groupId>
      <artifactId>commons-io</artifactId>
     </dependency>
     <dependency>
      <groupId>com.day.commons</groupId>
      <artifactId>day-commons-gfx</artifactId>
     </dependency>
     <dependency>
      <groupId>com.day.commons</groupId>
      <artifactId>day-commons-text</artifactId>
     </dependency>
     <dependency>
      <groupId>com.day.cq.workflow</groupId>
      <artifactId>cq-workflow-api</artifactId>
     </dependency>
     <dependency>
      <groupId>com.day.cq.wcm</groupId>
      <artifactId>cq-wcm-foundation</artifactId>
      <version>5.2.22</version>
     </dependency>
    </dependencies>
   ```

1. 次の場所で、Javaクラス `com.day.cq5.myhandler` を含むパッケージを作成し `myBundle/src/main/java`ます。

   1. Under myBundle, right-click `src/main/java`, select New, then Package.
   1. Name it `com.day.cq5.myhandler` and click Finish.

1. Create the Java class `MyHandler`:

   1. Eclipseの下で、 `myBundle/src/main/java``com.day.cq5.myhandler` パッケージを右クリックし、「New」、「Class」の順に選択します。
   1. ダイアログウィンドウで、この Java クラスに MyHandler という名前を付け、「Finish」をクリックします。MyHandler.java ファイルが作成され、このファイルが開きます。
   1. In `MyHandler.java` replace the existing code with the following and then save the changes:

   ```java
   package com.day.cq5.myhandler;
   import java.awt.Color;
   import java.awt.Rectangle;
   import java.awt.image.BufferedImage;
   import java.io.IOException;
   import java.io.InputStream;
   import java.io.InputStreamReader;
   import javax.jcr.Node;
   import javax.jcr.RepositoryException;
   import javax.jcr.Session;
   import org.apache.commons.io.IOUtils;
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   import com.day.cq.dam.api.metadata.ExtractedMetadata;
   import com.day.cq.dam.core.AbstractAssetHandler;
   import com.day.image.Font;
   import com.day.image.Layer;
   import com.day.cq.wcm.foundation.ImageHelper;
   
   /**
    * The <code>MyHandler</code> can extract text files
    * @scr.component inherit="true" immediate="true" metatype="false"
    * @scr.service
    *
    **/
   
   public class MyHandler extends AbstractAssetHandler {
    /** * Logger instance for this class. */
    private static final Logger log = LoggerFactory.getLogger(MyHandler.class);
    /** * Music icon margin */
    private static final int MARGIN = 10;
    /** * @see com.day.cq.dam.api.handler.AssetHandler#getMimeTypes() */
    public String[] getMimeTypes() {
     return new String[] {"text/plain"};
    }
   
    public ExtractedMetadata extractMetadata(Node asset) {
     ExtractedMetadata extractedMetadata = new ExtractedMetadata();
     InputStream data = getInputStream(asset);
     try {
      // read text data
      InputStreamReader reader = new InputStreamReader(data);
      char[] buffer = new char[4096];
      String text = "";
      while (reader.read(buffer) != -1) {
       text += new String(buffer);
      }
      reader.close();
      long wordCount = this.wordCount(text);
      extractedMetadata.setProperty("text", text);
      extractedMetadata.setMetaDataProperty("Word Count",wordCount);
      setMimetype(extractedMetadata, asset);
     } catch (Throwable t) {
      log.error("handling error: " + t.toString(), t);
     } finally {
      IOUtils.closeQuietly(data);
     }
     return extractedMetadata; }
    // ----------------------< helpers >----------------------------------------
    protected BufferedImage getThumbnailImage(Node node) {
     ExtractedMetadata metadata = extractMetadata(node);
     final String text = (String) metadata.getProperty("text");
     // create text layer
     final Layer layer = new Layer(500, 600, Color.WHITE);
     layer.setPaint(Color.black);
     Font font = new Font("Arial", 12);
     String displayText = this.getDisplayText(text, 600, 12);
     if(displayText!=null && displayText.length() > 0) {
      // commons-gfx Font class would throw IllegalArgumentException on empty or null text
      layer.drawText(10, 10, 500, 600, displayText, font, Font.ALIGN_LEFT, 0, 0);
     }
     // create watermark and merge with text layer
     Layer watermarkLayer;
     try {
      final Session session = node.getSession();
      watermarkLayer = ImageHelper.createLayer(session, "/content/dam/geometrixx/icons/certificate.png");
      watermarkLayer.setX(MARGIN);
      watermarkLayer.setY(MARGIN);
      layer.merge(watermarkLayer);
     } catch (RepositoryException e) {
      // TODO Auto-generated catch block
      e.printStackTrace();
     } catch (IOException e) {
      // TODO Auto-generated catch block
      e.printStackTrace(); }
     layer.crop(new Rectangle(510, 600));
     return layer.getImage(); }
    // ---------------< private >-----------------------------------------------
    /**
     * This method cuts lines if the text file is too long..
     * * @param text
     * * text to check
     * * @param height
     * * text box height (px)
     * * @param fontheight
     * * font height (px)
     * * @return the text which will fit into the box
     */
    private String getDisplayText(String text, int height, int fontheight) {
     String trimmedText = text.trim();
     int numOfLines = height / fontheight;
     String lines[] = trimmedText.split("\n");
     if (lines.length <= numOfLines) {
      return trimmedText;
     } else {
      String cuttetText = "";
      for (int i = 0; i < numOfLines; i++) {
       cuttetText += lines[i] + "\n";
      }
      return cuttetText;
     }
    }
    /**
     * * This method counts the number of words in a string
     * * @param text the String whose words would like to be counted
     * * @return the number of words in the string
     * */
    private long wordCount(String text) {
     // We need to keep track of the last character, if we have two white spaces in a row we dont want to double count
     // The starting of the document is always a whitespace
     boolean prevWhiteSpace = true;
     boolean currentWhiteSpace = true;
     char c; long numwords = 0;
     int j = text.length();
     int i = 0;
     while (i < j) {
      c = text.charAt(i++);
      if (c == 0) { break; }
      currentWhiteSpace = Character.isWhitespace(c);
      if (currentWhiteSpace && !prevWhiteSpace) { numwords++; }
      prevWhiteSpace = currentWhiteSpace;
     }
     // If we do not end with a white space then we need to add one extra word
     if (!currentWhiteSpace) { numwords++; }
     return numwords;
    }
   }
   ```

1. Java クラスをコンパイルして、バンドルを作成します。

   1. Right-click the `myBundle` project, select **[!UICONTROL Run As]**, then **[!UICONTROL Maven Install]**.
   1. The bundle `myBundle-0.0.1-SNAPSHOT.jar` (containing the compiled class) is created under `myBundle/target`.

1. In CRX Explorer, create a new node under `/apps/myApp`. Name = `install`, Type = `nt:folder`.
1. Copy the bundle `myBundle-0.0.1-SNAPSHOT.jar` and store it under `/apps/myApp/install` (for example with WebDAV). 新しいテキストハンドラーが AEM でアクティブになります。
1. In your browser, open the [!UICONTROL Apache Felix Web Management Console]. Select the [!UICONTROL Components] tab and disable the default text handler `com.day.cq.dam.core.impl.handler.TextHandler`.

## Command Line based media handler {#command-line-based-media-handler}

AEM を使用すると、ワークフロー内で任意のコマンドラインツールを実行して、アセットを変換し（ImageMagick など）、新しいレンディションをアセットに追加できます。必要な操作は、AEM サーバーをホストするディスクにコマンドラインツールをインストールし、ワークフローにプロセスのステップを設定することのみです。また、`CommandLineProcess` という起動プロセスによって、特定の MIME タイプに従ってフィルター処理を実行し、新しいレンディションに基づいて複数のサムネールを作成することもできます。

以下の変換を自動的に実行し、AEM Assets 内に保存することができます。

* [ImageMagick](https://www.imagemagick.org/script/index.php) および [Ghostscript](https://www.ghostscript.com/) を使用した EPS および AI 変換。
* FLV video transcoding using [FFmpeg](https://ffmpeg.org/).
* MP3 encoding using [LAME](http://lame.sourceforge.net/).
* Audio processing using [SOX](http://sox.sourceforge.net/).

>[!NOTE]
>
>Windows以外のシステムでは、Fmpegツールは、ファイル名に一重引用符(&#39;)が含まれるビデオアセットのレンディションの生成中にエラーを返します。 ビデオファイル名に一重引用符が含まれている場合は、AEM にアップロードする前に削除してください。

`CommandLineProcess` プロセスは、リストに表示されている順序で以下の操作を実行します。

* MIME タイプを指定した場合、そのタイプに従ってファイルをフィルターします。
* AEM サーバーをホストするディスクに一時ディレクトリを作成します。
* 元のファイルを一時ディレクトリにストリーミングします。
* ステップの引数で定義されたコマンドを実行します。AEM を実行しているユーザーの権限を使用して、一時ディレクトリ内でコマンドが実行されます。
* 結果を AEM サーバーのレンディションフォルダーにストリーミングします。
* 一時ディレクトリを削除します。
* 指定した場合は、それらのレンディションに基づいてサムネールを作成します。サムネールの数とサイズは、ステップの引数で定義されます。

### An example using ImageMagick {#an-example-using-imagemagick}

次の例は、MIMEタイプgifまたはtiffを持つアセットがAEMサーバーの/content/damに追加されるたびに、元のアセットの反転画像が3つの追加のサムネール(140x100、48x48、10x250)と共に作成されるように、コマンドライン処理手順を設定する方法を示しています。

これを実現するには、ImageMagick を使用します。ImageMagick は無料のソフトウェアスイートです。ビットマップ画像の作成、編集および構成をおこなう機能があり、一般的にコマンドラインから使用されます。

まず、AEM サーバーをホストするディスクに ImageMagick をインストールします。

1. ImageMagick をインストールします。[ImageMagick のマニュアル](https://www.imagemagick.org/script/download.php)を参照してください。
1. コマンドラインで convert を実行できるようにツールを設定します。
1. ツールが適切にインストールされているかどうかを確認するには、コマンド `convert -h` をコマンドラインで実行します。

   convert ツールの使用できるすべてのオプションが記載されたヘルプ画面が表示されます。

   >[!NOTE]
   >
   >Windows のバージョン（Windows SE など）によっては、convert コマンドを実行できない場合があります。このコマンドは、Windows インストールの一部であるネイティブな変換ユーティリティと競合するからです。このような場合は、画像ファイルをサムネールに変換するために使用する ImageMagick ユーティリティの完全パスを指定します。例： `"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`

1. このツールが正しく実行されていることを確認するには、.jpg 画像を作業ディレクトリに追加して、コマンド convert `<image-name>.jpg -flip <image-name>-flipped.jpg` をコマンドラインで実行します。

   反転画像がディレクトリに追加されます。

コマンドラインプロセスのステップを **[!UICONTROL DAM アセット更新]**&#x200B;ワークフローに追加します。

1. **[!UICONTROL ワークフロー]**&#x200B;コンソールを開きます。
1. 「**[!UICONTROL モデル]**」タブで、**[!UICONTROL DAM アセット更新]**&#x200B;モデルを編集します。
1. 以下のように、**[!UICONTROL Web enabled rendition]** ステップの設定を変更します。

   **引数**：

   `mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`

1. ワークフローを保存します。

変更したワークフローをテストするには、`/content/dam` にアセットを追加します。

1. ファイルシステムで、選択したTIFF画像を取得します。 名前を `myImage.tiff` に変更し、WebDAV などを使用して、`/content/dam` にコピーします。
1. **[!UICONTROL CQ5 DAM]** コンソール（例：`http://localhost:4502/libs/wcm/core/content/damadmin.html`）を開きます。
1. アセット **[!UICONTROL myImage.tiff]** を開き、反転画像と 3 つのサムネールが作成されたことを確認します。

#### Configure the CommandLineProcess process step {#configuring-the-commandlineprocess-process-step}

ここでは、[!UICONTROL CommandLineProcess] の[!UICONTROL プロセス引数]を設定する方法について説明します。

「 [!UICONTROL Process Arguments] 」の値は、コンマで区切ります。空白で開始しないでください。

| 引数のフォーマット | 説明 |
|---|---|
| mime:&lt;mime-type> | オプション引数。アセットの MIME タイプが引数の MIME タイプと同じ場合にプロセスが適用されます。<br>複数の MIME タイプを定義できます。 |
| tn:&lt;width>:&lt;height> | オプション引数。プロセスにより、引数で定義されたサイズのサムネールが作成されます。<br>複数のサムネールを定義できます。 |
| cmd: &lt;command> | 実行されるコマンドを定義します。この構文はコマンドラインツールによって異なります。1 つのコマンドのみを定義できます。<br>次の変数を使用して、コマンドを作成できます。<br>`${filename}`入力ファイルの名前（original.jpgなど） <br> `${file}`: 入力ファイルのフルパス名(例：/tmp/cqdam0816.tmp/original.jpg) <br> `${directory}`: 入力ファイルのディレクトリ。例：/tmp/cqdam0816.tmp <br>`${basename}`: 入力ファイルの名前（拡張子なし）。例： original <br>`${extension}`: 入力ファイルの拡張子（jpgなど） |

例えば、AEM サーバーをホストするディスクに ImageMagick がインストールされており、[!UICONTROL CommandLineProcess] を実装として使用し、以下の値を[!UICONTROL プロセス引数]として使用してプロセスのステップを作成するとします。

`mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`

then, when the workflow runs, the step only applies to assets that have `image/gif` or `mime:image/tiff` as `mime-types`, it creates a flipped image of the original, converts it into JPG and creates three thumbnails that have the dimensions: 140x100, 48x48, and 10x250.

ImageMagick を使用して 3 つの標準のサムネールを作成するには、以下の[!UICONTROL プロセス引数]を使用します。

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=319x319 -thumbnail "319x319>" -background transparent -gravity center -extent 319x319 -write png:cq5dam.thumbnail.319.319.png -thumbnail "140x100>" -background transparent -gravity center -extent 140x100 -write cq5dam.thumbnail.140.100.png -thumbnail "48x48>" -background transparent -gravity center -extent 48x48 cq5dam.thumbnail.48.48.png`

ImageMagick を使用して Web 対応レンディションを作成するには、以下の[!UICONTROL プロセス引数]を使用します。

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=1280x1280 -thumbnail "1280x1280>" cq5dam.web.1280.1280.jpeg`

>[!NOTE]
>
>[!UICONTROL CommandLineProcess] ステップは、アセット（ノードタイプ `dam:Asset`）またはアセットの子孫にのみ適用されます。

>[!MORELIKETHIS]
>
>* [アセットの処理](assets-workflow.md)

