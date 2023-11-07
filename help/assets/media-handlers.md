---
title: メディアハンドラーとワークフローを使用したアセットの処理
description: メディアハンドラーと、ワークフローを使用してデジタルアセットに対してタスクを実行する方法について説明します。
mini-toc-levels: 1
contentOwner: AG
role: User
feature: Workflow,Renditions
exl-id: cfd6c981-1a35-4327-82d7-cf373d842cc3
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2156'
ht-degree: 83%

---

# メディアハンドラーとワークフローを使用したアセットの処理 {#processing-assets-using-media-handlers-and-workflows}

[!DNL Adobe Experience Manager Assets] には、アセットの処理に使用するデフォルトのワークフローとメディアハンドラーのセットが付属しています。ワークフローでは、アセットに対して実行するタスクを定義し、特定のタスクをメディアハンドラーに委任します。例えば、サムネールの生成やメタデータの抽出などです。

特定の MIME タイプのアセットがアップロードされた際に自動的に実行されるように、ワークフローを設定できます。処理手順は、一連の [!DNL Assets] メディアハンドラーに基づいて定義されます。[!DNL Experience Manager] には、[組み込みのハンドラー](#default-media-handlers)がいくつか用意されています。さらに、追加のハンドラーを[カスタムで開発](#creating-a-new-media-handler)したり、処理を[コマンドラインツール](#command-line-based-media-handler)に委任して定義したりできます。

メディアハンドラーは、アセットに対して特定のアクションを実行する [!DNL Assets] 内のサービスです。例えば、MP3 オーディオファイルを [!DNL Experience Manager] にアップロードすると、ワークフローは MP3 ハンドラーをトリガーし、MP3 ハンドラーはメタデータを抽出してサムネイルを生成します。通常、メディアハンドラーはワークフローと組み合わせて使用されます。[!DNL Experience Manager] 内では、よく使用される MIME タイプがサポートされています。アセットに対して特定のタスクを実行するには、ワークフローを拡張または作成するか、メディアハンドラーを拡張または作成するか、メディアハンドラーを無効または有効にします。

>[!NOTE]
>
>詳しくは、 [Assets でサポートされる形式](assets-formats.md) ページを参照し、 [!DNL Assets] および各形式でサポートされる機能。

## デフォルトのメディアハンドラー {#default-media-handlers}

[!DNL Assets] 内では以下のメディアハンドラーを使用できます。また、これらのメディアハンドラーはよく使用される MIME タイプを処理できます。

<!-- TBD: Java versions shouldn't be set to 1.5. Must be updated.
-->

| ハンドラー名 | サービス名（システムコンソールでの名称） | サポートされる MIME タイプ |
|--------------|--------------------------------------|----------------------|
| [!UICONTROL TextHandler] | com.day.cq.dam.core.impl.handler.TextHandler | text/plain |
| [!UICONTROL PdfHandler] | com.day.cq.dam.handler.standard.pdf.PdfHandler | <ul><li>application/pdf</li><li>application/illustrator</li></ul> |
| [!UICONTROL JpegHandler] | com.day.cq.dam.core.impl.handler.JpegHandler | image/jpeg |
| [!UICONTROL Mp3Handler] | com.day.cq.dam.handler.standard.mp3.Mp3Handler | audio/mpeg<br><b>重要</b> - MP3 ファイルをアップロードすると、 [サードパーティのライブラリを使用して処理](https://www.zxdr.it/programmi/SistEvolBDD/LibJava/doc/de/vdheide/mp3/MP3File.html). MP3 に可変ビットレート（VBR）がある場合、ライブラリは不正確なおおよその長さを計算します。 |
| [!UICONTROL ZipHandler] | com.day.cq.dam.handler.standard.zip.ZipHandler | <ul><li>application/java-archive </li><li> application/zip</li></ul> |
| [!UICONTROL PictHandler] | com.day.cq.dam.handler.standard.pict.PictHandler | image/pict |
| [!UICONTROL StandardImageHandler] | com.day.cq.dam.core.impl.handler.StandardImageHandler | <ul><li>image/gif </li><li> image/png </li> <li>application/photoshop </li> <li>image/jpeg </li><li> image/tiff </li> <li>image/x-ms-bmp </li><li> image/bmp</li></ul> |
| [!UICONTROL MSOfficeHandler] | com.day.cq.dam.handler.standard.msoffice.MSOfficeHandler | application/msword |
| [!UICONTROL MSPowerPointHandler] | com.day.cq.dam.handler.standard.msoffice.MSPowerPointHandler | application/vnd.ms-powerpoint |
| [!UICONTROL OpenOfficeHandler] | com.day.cq.dam.handler.standard.ooxml.OpenOfficeHandler | <ul><li>application/vnd.openxmlformats-officedocument.wordprocessingml.document</li><li> application/vnd.openxmlformats-officedocument.spreadsheetml.sheet</li><li> application/vnd.openxmlformats-officedocument.presentationml.presentation</li></ul> |
| [!UICONTROL EPubHandler] | com.day.cq.dam.handler.standard.epub.EPubHandler | application/epub+zip |
| [!UICONTROL GenericAssetHandler] | com.day.cq.dam.core.impl.handler.GenericAssetHandler | アセットからデータを抽出する他のハンドラーが見つからなかった場合のフォールバック |

{style="table-layout:auto"}

すべてのハンドラーは、次のタスクを実行します。

* アセットから使用可能なすべてのメタデータを抽出しています。
* アセットのサムネイル画像を作成します。

アクティブなメディアハンドラーを表示するには：

1. ブラウザーで、`https://localhost:4502/system/console/components` に移動します。
1. 「`com.day.cq.dam.core.impl.store.AssetStoreImpl`」をクリックします。
1. すべてのアクティブなメディアハンドラーリストが表示されます。次に例を示します。

![chlimage_1-437](assets/chlimage_1-437.png)

## ワークフローでメディアハンドラーを使用したアセットに対するタスクの実行 {#using-media-handlers-in-workflows-to-perform-tasks-on-assets}

通常、メディアハンドラーはワークフローと組み合わせて使用されるサービスです。

[!DNL Experience Manager] には、アセットを処理するデフォルトのワークフローがいくつかあります。ワークフローを表示するには、ワークフローコンソールを開き、**[!UICONTROL モデル]**&#x200B;タブをクリックしてください。[!DNL Assets] から始まるワークフロータイトルは、アセット固有のタイトルです。

特定の要件に従って、既存のワークフローを拡張し、新しいワークフローを作成してアセットを処理できます。

以下の例は、**[!UICONTROL AEM Assets 同期]**&#x200B;ワークフローを拡張して、PDF ドキュメント以外のすべてのアセットについてサブアセットを生成するための方法を示しています。

### メディアハンドラーを無効または有効にする {#disabling-enabling-a-media-handler}

メディアハンドラーは、Apache Felix Web Management Console を使用して無効または有効にできます。 メディアハンドラーが無効になっている場合、アセットに対してタスクは実行されません。

メディアハンドラーを有効/無効にするには：

1. ブラウザーで、`https://<host>:<port>/system/console/components` に移動します。
1. メディアハンドラーの名前の横にある「**[!UICONTROL Disable]**」をクリックします。例：`com.day.cq.dam.handler.standard.mp3.Mp3Handler`
1. ページを更新します。メディアハンドラーの横に、無効であることを示すアイコンが表示されます。
1. メディアハンドラーを有効にするには、メディアハンドラーの名前の横にある「**[!UICONTROL Enable]**」をクリックします。

### メディアハンドラーの作成 {#creating-a-new-media-handler}

新しいメディアタイプをサポートしたり、アセットに対して特定のタスクを実行したりするには、メディアハンドラーを作成する必要があります。 この節では、作業の進め方を説明します。

#### 重要なクラスおよびインターフェイス {#important-classes-and-interfaces}

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
   * その他すべてのアセットハンドラー実装の基礎として機能し、よく使用される機能を提供します。さらに、サブアセットの抽出についてよく使用される機能も提供します。
   * 実装を開始するための最適な方法は、最も多くの点について対応し、適切なデフォルト動作を提供している付属の抽象実装から継承することです。それが com.day.cq.dam.core.AbstractAssetHandler クラスです。
   * このクラスには、抽象的なサービス記述子が用意されています。したがって、このクラスから継承し、maven-sling-plugin を使用する場合、inherit フラグを true に設定する必要があります。

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

#### 例：特定のテキストハンドラーの作成 {#example-create-a-specific-text-handler}

この節では、透かし付きのサムネールを生成する特定のテキストハンドラを作成します。

以下の手順を実行します。

Eclipse に [!DNL Maven] プラグインをインストールして設定する方法、および [!DNL Maven] プロジェクトに必要な依存関係を設定する方法は、[開発ツール](../sites-developing/dev-tools.md) を参照してください。

以下の手順を実行した後、TXTファイルを [!DNL Experience Manager] にアップロードすると、ファイルのメタデータが抽出され、透かしありの 2 つのサムネールが生成されます。

1. Eclipse で、`myBundle` [!DNL Maven] プロジェクトを作成します。

   1. メニューバーで、**[!UICONTROL ファイル]**／**[!UICONTROL 新規]**／**[!UICONTROL その他]**&#x200B;をクリックします。
   1. ダイアログで、[!DNL Maven] フォルダーを展開し、[!DNL Maven] プロジェクトを選択して、**[!UICONTROL 次へ]**&#x200B;をクリックします。
   1. 「簡単なプロジェクトを作成する」と「デフォルトのワークスペースの場所を使用する」の各チェックボックスをオンにして、**[!UICONTROL 次へ]**&#x200B;をクリックしてください。
   1. [!DNL Maven] プロジェクトを定義します。

      * グループ Id：`com.day.cq5.myhandler`。
      * アーティファクト Id：myBundle.
      * 名前：My [!DNL Experience Manager] バンドル。
      * 説明：これは [!DNL Experience Manager] バンドルです。

   1. 「**[!UICONTROL 終了]**」をクリックします。

1. [!DNL Java] コンパイラーをバージョン 1.5 に設定します。

   1. `myBundle` プロジェクトを右クリックし、[!UICONTROL プロパティ]を選択してください。
   1. [!UICONTROL Java コンパイラー]を選択して、次のプロパティを 1.5 に設定してください。

      * コンパイラのコンプライアンスレベル
      * 生成された.class ファイルの互換性
      * ソースの互換性

   1. 「**[!UICONTROL OK]**」をクリックします。ダイアログウィンドウで、「**[!UICONTROL はい]**」をクリックします。

1.  `pom.xml` ファイルのコードを以下のコードで書き換えます。

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

1. `myBundle/src/main/java` の下に [!DNL Java] クラスを含むパッケージ `com.day.cq5.myhandler` を作成します。

   1. myBundle の下の `src/main/java` を右クリックし、「新規」、「パッケージ」の順に選択してください。
   1. `com.day.cq5.myhandler` という名前を付け、「終了」をクリックしてください。

1. [!DNL Java] クラス `MyHandler` を作成します。

   1. [!DNL Eclipse] で `myBundle/src/main/java` の下の、`com.day.cq5.myhandler` パッケージを右クリックします。[!UICONTROL 新規]、[!UICONTROL クラス]の順に選択します。
   1. ダイアログウィンドウで、[!DNL Java] クラスに `MyHandler` という名前を付け、「[!UICONTROL 終了]」をクリックしてください。[!DNL Eclipse] がファイル `MyHandler.java` を作成し、開きます。
   1. `MyHandler.java` で、既存のコードを以下のコードに置き換えてから、変更内容を保存してください。

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
      watermarkLayer = ImageHelper.createLayer(session, "/content/dam/we-retail/en/products/apparel/gloves/Gloves.jpg");
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
     // We need to keep track of the last character, if we have two whitespaces in a row we don't want to double count.
     // The starting of the document is always a whitespace.
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
     // If we do not end with a whitespace then we need to add one extra word.
     if (!currentWhiteSpace) { numwords++; }
     return numwords;
    }
   }
   ```

1. [!DNL Java] クラスをコンパイルして、バンドルを作成してください。

   1. `myBundle` プロジェクトを右クリックしてから、**[!UICONTROL 次として実行]**、**[!UICONTROL Maven インストール]**&#x200B;の順に選択してください。
   1. バンドル `myBundle-0.0.1-SNAPSHOT.jar`（コンパイル済みのクラスが含まれる）が `myBundle/target` の下に作成されます。

1. CRX エクスプローラーで、以下にノードを作成します。 `/apps/myApp`. 名前 = `install`、タイプ = `nt:folder`。
1. バンドルをコピーします。 `myBundle-0.0.1-SNAPSHOT.jar` そして下に保存し `/apps/myApp/install` （例えば、WebDAV を使用）。 新しいテキストハンドラーが [!DNL Experience Manager] でアクティブになります。
1. ブラウザーで、[!UICONTROL Apache Felix Web Management Console] を開きます。[!UICONTROL コンポーネント]タブを選択し、デフォルトのテキストハンドラー `com.day.cq.dam.core.impl.handler.TextHandler` を無効にしてください。

## コマンドラインベースのメディアハンドラー {#command-line-based-media-handler}

[!DNL Experience Manager] を使用すると、ワークフロー内で任意のコマンドラインツールを実行して、アセットを変換し（[!DNL ImageMagick] など）、新しいレンディションをアセットに追加できます。必要な操作は、[!DNL Experience Manager] サーバーをホストするディスクにコマンドラインツールをインストールして、ワークフローにプロセスのステップを追加し、設定することのみです。また、`CommandLineProcess` という起動プロセスによって、特定の MIME タイプに従ってフィルター処理を実行し、新しいレンディションに基づいて複数のサムネールを作成することもできます。

以下の変換を自動的に実行し、[!DNL Assets] 内に保存することができます。

* [ImageMagick](https://www.imagemagick.org/script/index.php) および [Ghostscript](https://www.ghostscript.com/) を使用した EPS および AI 変換。
* [FFmpeg](https://ffmpeg.org/) を使用した FLV ビデオのトランスコーディング。
* [LAME](https://lame.sourceforge.io/) を使用した MP3 エンコーディング。
* [SOX](https://sox.sourceforge.io/) を使用したオーディオ処理。

>[!NOTE]
>
>Windows 以外のシステムでは、ファイル名に一重引用符（&#39;）を含むビデオアセットのレンディションの生成中に FFMpeg ツールがエラーを返します。ビデオファイル名に一重引用符が含まれている場合は、[!DNL Experience Manager] にアップロードする前に削除してください。

`CommandLineProcess` プロセスは、リストに表示されている順序で以下の操作を実行します。

* MIME タイプを指定した場合、そのタイプに従ってファイルをフィルターします。
* [!DNL Experience Manager] サーバーをホストするディスクに一時ディレクトリを作成します。
* 元のファイルを一時ディレクトリにストリーミングします。
* ステップの引数で定義されたコマンドを実行します。[!DNL Experience Manager] を実行しているユーザーの権限を使用して、一時ディレクトリ内でコマンドが実行されます。
* 結果を [!DNL Experience Manager] サーバーのレンディションフォルダーにストリーミングします。
* 一時ディレクトリを削除します。
* 指定した場合、これらのレンディションに基づいてサムネールを作成します。 サムネールの数とサイズは、ステップの引数で定義します。

### [!DNL ImageMagick] を使用した例 {#an-example-using-imagemagick}

以下の例は、MIME タイプが GIF または TIFF のアセットが [!DNL Experience Manager] サーバーの `/content/dam` に追加されるたびに、元の画像の反転画像と 3 つの追加サムネール（140 x 100、48 x 48、10 x 250）が作成されるように、コマンドラインプロセスのステップを設定する方法を示します。

そのためには [!DNL ImageMagick] を使用します。[!DNL ImageMagick] は、ビットマップ画像の作成、編集、合成に使用される無料のコマンドラインソフトウェアです。

[!DNL Experience Manager] サーバーをホストするディスクに [!DNL ImageMagick] をインストールします。

1. [!DNL ImageMagick] のインストール：[ImageMagick のドキュメント](https://www.imagemagick.org/script/download.php)を参照してください。
1. コマンドラインで convert を実行できるようにツールを設定します。
1. ツールが適切にインストールされているかどうかを確認するには、コマンド `convert -h` をコマンドラインで実行します。

   convert ツールの使用できるすべてのオプションが記載されたヘルプ画面が表示されます。

   >[!NOTE]
   >
   >Windows のバージョンによっては、「convert」コマンドを実行できない場合があります。このコマンドは、[!DNL Windows] インストールの一部であるネイティブな変換ユーティリティと競合するためです。このような場合は、画像ファイルをサムネールに変換するために使用する [!DNL ImageMagick] ソフトウェアの完全パスを指定します。（例：`"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`）。

1. このツールが正しく実行されていることを確認するには、JPG 画像を作業ディレクトリに追加して、コマンド convert `<image-name>.jpg -flip <image-name>-flipped.jpg` をコマンドラインで実行します。反転画像がディレクトリに追加されます。コマンドラインプロセスのステップを **[!UICONTROL DAM アセット更新]**&#x200B;ワークフローに追加します。
1. **[!UICONTROL ワークフロー]**&#x200B;コンソールを開きます。
1. 「**[!UICONTROL モデル]**」タブで、**[!UICONTROL DAM アセット更新]**&#x200B;モデルを編集します。
1. **[!UICONTROL Web 対応レンディション]**&#x200B;手順の[!UICONTROL 引数]を `mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg` に変更します。
1. ワークフローを保存します。

変更したワークフローをテストするには、`/content/dam` にアセットを追加します。

1. ファイルシステムで、任意の TIFF 画像を取得します。名前をに変更します。 `myImage.tiff` にコピーします。 `/content/dam`例えば、WebDAV を使用します。
1. 次に移動： **[!UICONTROL CQ5 DAM]** コンソール、例： `https://localhost:4502/libs/wcm/core/content/damadmin.html`.
1. アセット **[!UICONTROL myImage.tiff]** を開き、反転画像と 3 つのサムネールが作成されたことを確認します。

#### CommandLineProcess プロセスステップの設定 {#configuring-the-commandlineprocess-process-step}

この節では、[!UICONTROL CommandLineProcess] の[!UICONTROL プロセス引数]を設定する方法について説明します。

[!UICONTROL プロセスの引数]の値をコンマを使用し、区切ります（空白で始めないでください）。

| 引数のフォーマット | 説明 |
|---|---|
| mime:&lt;mime-type> | オプション引数。アセットの MIME タイプが引数の MIME タイプと同じ場合にプロセスが適用されます。<br>複数の MIME タイプを定義できます。 |
| tn:&lt;width>:&lt;height> | オプション引数。プロセスにより、引数で定義されたサイズのサムネールが作成されます。<br>複数のサムネールを定義できます。 |
| cmd: &lt;command> | 実行するコマンドを定義します。この構文はコマンドラインツールによって異なります。1 つのコマンドのみを定義できます。<br>次の変数を使用して、コマンドを作成できます。<br>`${filename}`：入力ファイルの名前（例：original.jpg） <br> `${file}`：入力ファイルの完全パス名（例： ） `/tmp/cqdam0816.tmp/original.jpg` <br> `${directory}`：入力ファイルのディレクトリ（例： ） `/tmp/cqdam0816.tmp` <br>`${basename}`：拡張子なしの入力ファイル名（例：original） <br>`${extension}`：入力ファイルの拡張子 ( 例：JPG)。 |

例えば、[!DNL Experience Manager] サーバーをホストするディスクに [!DNL ImageMagick] がインストールされており、[!UICONTROL CommandLineProcess] を実装として使用し、以下の値を[!UICONTROL プロセス引数]として使用してプロセスのステップを作成するとします。

`mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`

この場合、ワークフローを実行すると、`mime-types` が `image/gif` または `mime:image/tiff` のアセットにのみ、このステップが適用され、元の画像の反転画像が作成され、JPG に変換され、140 x 100、48 x 48 および 10 x 250 というサイズの 3 つのサムネールが作成されます。

[!DNL ImageMagick] を使用して 3 つの標準のサムネールを作成するには、以下の[!UICONTROL プロセス引数]を使用します。

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=319x319 -thumbnail "319x319>" -background transparent -gravity center -extent 319x319 -write png:cq5dam.thumbnail.319.319.png -thumbnail "140x100>" -background transparent -gravity center -extent 140x100 -write cq5dam.thumbnail.140.100.png -thumbnail "48x48>" -background transparent -gravity center -extent 48x48 cq5dam.thumbnail.48.48.png`

[!DNL ImageMagick] を使用して web 対応レンディションを作成するには、以下の[!UICONTROL プロセス引数]を使用します。

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=1280x1280 -thumbnail "1280x1280>" cq5dam.web.1280.1280.jpeg`

>[!NOTE]
>
>[!UICONTROL CommandLineProcess] ステップは、アセット（ノードタイプ `dam:Asset`）またはアセットの子孫にのみ適用されます。

>[!MORELIKETHIS]
>
>* [アセットを処理](assets-workflow.md)
