---
title: メディアハンドラーとワークフローを使用したアセットの処理
description: メディアハンドラーについて、およびワークフローを使用してデジタルアセットに対してタスクを実行する方法について説明します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: b14b377e52ab10c41355f069d97508b588d82216
workflow-type: tm+mt
source-wordcount: '2108'
ht-degree: 49%

---


# メディアハンドラーとワークフローを使用してアセットを処理{#processing-assets-using-media-handlers-and-workflows}

[!DNL Adobe Experience Manager Assets] には、アセットの処理に使用するデフォルトのワークフローとメディアハンドラーのセットが付属しています。ワークフローは、アセットに対して実行されるタスクを定義し、特定のタスク(サムネールの生成やメタデータ抽出など)をメディアハンドラーに委任します。

特定のMIMEタイプのアセットがアップロードされたときに、自動的に実行されるようにワークフローを設定できます。 処理手順は、一連の[!DNL Assets]メディアハンドラーに関して定義されます。 [!DNL Experience Manager] には、[組み込みのハンドラー](#default-media-handlers)がいくつか用意されています。さらに、追加のハンドラーを[カスタムで開発](#creating-a-new-media-handler)したり、処理を[コマンドラインツール](#command-line-based-media-handler)に委任して定義したりできます。

メディアハンドラーは、[!DNL Assets]内のサービスで、アセットに対して特定のアクションを実行します。 例えば、MP3オーディオファイルが[!DNL Experience Manager]にアップロードされると、ワークフローは、メタデータを抽出してサムネールを生成するMP3ハンドラをトリガします。 通常、メディアハンドラーはワークフローと組み合わせて使用されます。[!DNL Experience Manager]内では、一般的なMIMEタイプのほとんどがサポートされています。 アセットに対して特定のタスクを実行するには、ワークフローを拡張または作成するか、メディアハンドラーを拡張または作成するか、メディアハンドラーを無効または有効にします。

>[!NOTE]
>
>[サポートされるすべての形式](assets-formats.md)の説明と、各形式でサポートされる機能については、&lt;a0/>サポートされるアセットの形式&lt;a1/>のページを参照してください。[!DNL Assets]

## デフォルトのメディアハンドラー{#default-media-handlers}

[!DNL Assets]内では次のメディアハンドラを使用でき、最も一般的なMIME型を処理します。

<!-- TBD: Java versions shouldn't be set to 1.5. Must be updated.
-->

| ハンドラー名 | サービス名（システムコンソール内） | サポートされる MIME タイプ |
|--------------|--------------------------------------|----------------------|
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

1. ブラウザーで`http://localhost:4502/system/console/components`に移動します。
1. 「`com.day.cq.dam.core.impl.store.AssetStoreImpl`」をクリックします。
1. すべてのアクティブなメディアハンドラーリストが表示されます。次に例を示します。

![chlimage_1-437](assets/chlimage_1-437.png)

## ワークフロー内でメディアハンドラーを使用してアセット{#using-media-handlers-in-workflows-to-perform-tasks-on-assets}に対してタスクを実行する

通常、メディアハンドラーはワークフローと組み合わせて使用されるサービスです。

[!DNL Experience Manager] には、アセットを処理するデフォルトのワークフローがいくつかあります。ワークフローを表示するには、ワークフローコンソールを開き、「**[!UICONTROL モデル]**」タブをクリックします。「」から始まるワークフロータイトルは、アセット固有のタイトルです。[!DNL Assets]

特定の要件に従って、既存のワークフローを拡張し、新しいワークフローを作成してアセットを処理できます。

以下の例は、**[!UICONTROL AEM Assets 同期]**&#x200B;ワークフローを拡張して、PDF ドキュメント以外のすべてのアセットについてサブアセットを生成するための方法を示しています。

### メディアハンドラーを無効または有効にする{#disabling-enabling-a-media-handler}

メディアハンドラーを無効または有効にするには、Apache Felix Web Management Console を使用します。メディアハンドラーを無効にすると、そのアセットに対してメディアハンドラーのタスクは実行されません。

メディアハンドラーを有効または無効にするための手順

1. ブラウザーで、`https://<host>:<port>/system/console/components` です。
1. メディアハンドラーの名前の横にある「**[!UICONTROL Disable]**」をクリックします。例：`com.day.cq.dam.handler.standard.mp3.Mp3Handler`
1. ページを更新します。メディアハンドラーの横に、無効であることを示すアイコンが表示されます。
1. メディアハンドラーを有効にするには、メディアハンドラーの名前の横にある「**[!UICONTROL Enable]**」をクリックします。

### 新しいメディアハンドラーの作成{#creating-a-new-media-handler}

新しいメディアタイプをサポートしたり、アセットで特定のタスクを実行したりするには、新しいメディアハンドラーを作成する必要があります。ここでは、その進め方について説明します。

#### 重要なクラスとインターフェイス{#important-classes-and-interfaces}

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
   * 実装を開始する最善の方法は、ほとんどの処理を行い、適切なデフォルト動作を提供する、提供された抽象実装から継承することです。com.day.cq.dam.core.AbstractAssetHandlerクラス
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

#### 例：特定のテキストハンドラーを作成する{#example-create-a-specific-text-handler}

ここでは、透かしありのサムネールを生成する固有の Text Handler を作成します。

以下の手順を実行します。

[!DNL Maven]プラグインを使用してEclipseをインストールおよび設定し、[!DNL Maven]プロジェクトに必要な依存関係を設定する方法については、[開発ツール](../sites-developing/dev-tools.md)を参照してください。

次の手順を実行した後、TXTファイルを[!DNL Experience Manager]にアップロードすると、ファイルのメタデータが抽出され、透かし付きの2つのサムネールが生成されます。

1. Eclipseで、`myBundle` [!DNL Maven]プロジェクトを作成します。

   1. メニューバーで、**[!UICONTROL ファイル]**/**[!UICONTROL 新規]**/**[!UICONTROL その他]**&#x200B;をクリックします。
   1. ダイアログで、[!DNL Maven]フォルダーを展開し、[!DNL Maven]プロジェクトを選択して、**[!UICONTROL 次へ]**&#x200B;をクリックします。
   1. 「単純なプロジェクトを作成」ボックスと「デフォルトのワークスペースの場所を使用」ボックスをオンにし、「**[!UICONTROL 次へ]**」をクリックします。
   1. [!DNL Maven]プロジェクトの定義：

      * グループID:`com.day.cq5.myhandler`.
      * Artifact Id：myBundle.
      * 名前：[!DNL Experience Manager]バンドル。
      * 説明：これは私の[!DNL Experience Manager]バンドルです。
   1. 「**[!UICONTROL Finish]**」をクリックします。


1. [!DNL Java]コンパイラをバージョン1.5に設定します。

   1. `myBundle`プロジェクトを右クリックし、「[!UICONTROL プロパティ]」を選択します。
   1. 「[!UICONTROL Javaコンパイラー]」を選択し、次のプロパティを1.5に設定します。

      * Compiler compliance level
      * Generated .class files compatibility
      * Source compatibility
   1. 「**[!UICONTROL OK]**」をクリックします。ダイアログウィンドウで、「**[!UICONTROL はい]**」をクリックします。


1. `pom.xml`ファイル内のコードを次のコードに置き換えます。

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

1. `myBundle/src/main/java`の下に[!DNL Java]クラスを含むパッケージ`com.day.cq5.myhandler`を作成します。

   1. 「myBundle」で`src/main/java`を右クリックし、「新規」、「パッケージ」の順に選択します。
   1. `com.day.cq5.myhandler`という名前を付け、「完了」をクリックします。

1. [!DNL Java]クラス`MyHandler`を作成します。

   1. [!DNL Eclipse]の`myBundle/src/main/java`で、`com.day.cq5.myhandler`パッケージを右クリックします。 「[!UICONTROL 新規]」を選択し、「[!UICONTROL クラス]」を選択します。
   1. ダイアログウィンドウで、[!DNL Java]クラス`MyHandler`に名前を付け、[!UICONTROL 完了]をクリックします。 [!DNL Eclipse] ファイルを作成して開き `MyHandler.java`ます。
   1. `MyHandler.java`で既存のコードを次のコードに置き換え、変更を保存します。

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

1. [!DNL Java]クラスをコンパイルし、バンドルを作成します。

   1. `myBundle`プロジェクトを右クリックし、「**[!UICONTROL 実行]**」を選択してから、「**[!UICONTROL Mavenインストール]**」を選択します。
   1. バンドル`myBundle-0.0.1-SNAPSHOT.jar` （コンパイルされたクラスを含む）が`myBundle/target`の下に作成されます。

1. CRXエクスプローラーで、`/apps/myApp`の下に新しいノードを作成します。 名前= `install`、種類= `nt:folder`。
1. バンドル`myBundle-0.0.1-SNAPSHOT.jar`をコピーし、`/apps/myApp/install`の下に格納します（WebDAVなど）。 新しいテキストハンドラーが[!DNL Experience Manager]でアクティブになりました。
1. ブラウザーで、[!UICONTROL Apache Felix Web Management Console]を開きます。 「[!UICONTROL コンポーネント]」タブを選択し、デフォルトのテキストハンドラー`com.day.cq.dam.core.impl.handler.TextHandler`を無効にします。

## コマンドラインベースのメディアハンドラ{#command-line-based-media-handler}

[!DNL Experience Manager] を使用すると、ワークフロー内で任意のコマンドラインツールを実行して、アセットを変換し（ など）、新しいレンディションをアセットに追加できます。[!DNL ImageMagick][!DNL Experience Manager]サーバーをホストするディスクにコマンドラインツールをインストールし、ワークフローにプロセスステップを追加して設定するだけです。 また、`CommandLineProcess` という起動プロセスによって、特定の MIME タイプに従ってフィルター処理を実行し、新しいレンディションに基づいて複数のサムネールを作成することもできます。

次の変換は、[!DNL Assets]内で自動的に実行および保存できます。

* [ImageMagick](https://www.imagemagick.org/script/index.php)と[Ghostscript](https://www.ghostscript.com/)を使用したEPS変換とAI変換。
* [FFmpeg](https://ffmpeg.org/)を使用したFLVビデオトランスコード。
* [LAME](https://lame.sourceforge.io/)を使用したMP3エンコード。
* [SOX](https://sox.sourceforge.net/)を使用したオーディオ処理。

>[!NOTE]
>
>Windows以外のシステムでは、Fmpegツールは、ファイル名に一重引用符(&#39;)が含まれるビデオアセットのレンディションの生成中にエラーを返します。 ビデオファイルの名前に一重引用符が含まれている場合は、削除してから[!DNL Experience Manager]にアップロードしてください。

`CommandLineProcess` プロセスは、リストに表示されている順序で以下の操作を実行します。

* MIME タイプを指定した場合、そのタイプに従ってファイルをフィルターします。
* [!DNL Experience Manager]サーバーをホストするディスク上に一時ディレクトリを作成します。
* 元のファイルを一時ディレクトリにストリーミングします。
* ステップの引数で定義されたコマンドを実行します。[!DNL Experience Manager]を実行するユーザーの権限で、一時ディレクトリ内でコマンドを実行しています。
* 結果を[!DNL Experience Manager]サーバーのレンディションフォルダーにストリーミングして戻します。
* 一時ディレクトリを削除します。
* 指定した場合は、それらのレンディションに基づいてサムネールを作成します。サムネールの数とサイズは、ステップの引数で定義されます。

### [!DNL ImageMagick] {#an-example-using-imagemagick}の使用例

次の例は、miMIME eタイプGIFまたはTIFFを持つアセットが[!DNL Experience Manager]サーバーの`/content/dam`に追加されるたびに、元のアセットの反転画像が3つの追加のサムネール(140x100、48x48、10x25)と共に作成されるように、コマンドライン処理手順を設定する方法を示しています0)。

これを行うには、[!DNL ImageMagick]を使用します。 [!DNL ImageMagick] は、ビットマップ画像の作成、編集、構成に使用する無料のコマンドラインソフトウェアです。

[!DNL Experience Manager]サーバーをホストするディスクに[!DNL ImageMagick]をインストールします。

1. [!DNL ImageMagick]をインストール：[ImageMagickのドキュメント](https://www.imagemagick.org/script/download.php)を参照してください。
1. コマンドラインで convert を実行できるようにツールを設定します。
1. ツールが適切にインストールされているかどうかを確認するには、コマンド `convert -h` をコマンドラインで実行します。

   convert ツールの使用できるすべてのオプションが記載されたヘルプ画面が表示されます。

   >[!NOTE]
   >
   >Windowsの一部のバージョンでは、[!DNL Windows]のインストールに含まれるネイティブの変換ユーティリティと競合するので、convertコマンドの実行に失敗する場合があります。 この場合、画像ファイルをサムネールに変換するために使用する[!DNL ImageMagick]ソフトウェアの完全なパスに言及します。 例： `"C:\Program Files\ImageMagick-6.8.9-Q16\convert.exe" -define jpeg:size=319x319 ${filename} -thumbnail 319x319 cq5dam.thumbnail.319.319.png`

1. ツールが正しく実行されるかどうかを確認するには、作業ディレクトリにJPG画像を追加し、コマンドラインでconvert `<image-name>.jpg -flip <image-name>-flipped.jpg`コマンドを実行します。 反転画像がディレクトリに追加されます。次に、コマンドライン処理手順を&#x200B;**[!UICONTROL DAM Update Asset]**&#x200B;ワークフローに追加します。
1. **[!UICONTROL ワークフロー]**&#x200B;コンソールを開きます。
1. 「**[!UICONTROL モデル]**」タブで、**[!UICONTROL DAM アセット更新]**&#x200B;モデルを編集します。
1. **[!UICONTROL Web対応のレンディション]**&#x200B;の[!UICONTROL 引数]を次のように変更します。`mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`。
1. ワークフローを保存します。

変更したワークフローをテストするには、`/content/dam` にアセットを追加します。

1. ファイルシステムで、選択したTIFF画像を取得します。 名前を `myImage.tiff` に変更し、WebDAV などを使用して、`/content/dam` にコピーします。
1. **[!UICONTROL CQ5 DAM]** コンソール（例：`http://localhost:4502/libs/wcm/core/content/damadmin.html`）を開きます。
1. アセット **[!UICONTROL myImage.tiff]** を開き、反転画像と 3 つのサムネールが作成されたことを確認します。

#### CommandLineProcessプロセスステップ{#configuring-the-commandlineprocess-process-step}を設定

ここでは、[!UICONTROL CommandLineProcess] の[!UICONTROL プロセス引数]を設定する方法について説明します。

[!UICONTROL プロセスの引数]の値はコンマで区切り、空白で開始しないでください。

| 引数のフォーマット | 説明 |
|---|---|
| mime:&lt;mime-type> | オプション引数。アセットの MIME タイプが引数の MIME タイプと同じ場合にプロセスが適用されます。<br>いくつかのMIMEタイプを定義できます。 |
| tn:&lt;width>:&lt;height> | オプション引数。プロセスにより、引数で定義されたサイズのサムネールが作成されます。<br>複数のサムネールを定義できます。 |
| cmd: &lt;command> | 実行するコマンドを定義します。 この構文はコマンドラインツールによって異なります。1 つのコマンドのみを定義できます。<br>次の変数を使用して、コマンドを作成できます。<br>`${filename}`入力ファイルの名前（original.jpgなど）  <br> `${file}`:入力ファイルのフルパス名（例：）  `/tmp/cqdam0816.tmp/original.jpg` <br> `${directory}`:入力ファイルのディレクトリ。例 `/tmp/cqdam0816.tmp` <br>`${basename}`:入力ファイルの名前（拡張子なし）。例： original  <br>`${extension}`:入力ファイルの拡張子（JPGなど）。 |

例えば、[!DNL Experience Manager]サーバーをホストするディスクに[!DNL ImageMagick]がインストールされていて、[!UICONTROL CommandLineProcess]をImplementationとして使用し、次の値を[!UICONTROL Process Arguments]としてプロセス手順を作成する場合：

`mime:image/gif,mime:image/tiff,tn:140:100,tn:48:48,tn:10:250,cmd:convert ${directory}/${filename} -flip ${directory}/${basename}.flipped.jpg`

次に、ワークフローを実行すると、手順は`image/gif`または`mime:image/tiff`が`mime-types`であるアセットにのみ適用され、元の画像のフリップ画像が作成され、JPGに変換され、次の3つのサイズのサムネールが作成されます。140x100、48x48、10x250

次の[!UICONTROL プロセスの引数]を使用して、[!DNL ImageMagick]を使用して3つの標準サムネールを作成します。

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=319x319 -thumbnail "319x319>" -background transparent -gravity center -extent 319x319 -write png:cq5dam.thumbnail.319.319.png -thumbnail "140x100>" -background transparent -gravity center -extent 140x100 -write cq5dam.thumbnail.140.100.png -thumbnail "48x48>" -background transparent -gravity center -extent 48x48 cq5dam.thumbnail.48.48.png`

[!DNL ImageMagick]を使用してWeb対応のレンディションを作成するには、次の[!UICONTROL Process Arguments]を使用します。

`mime:image/tiff,mime:image/png,mime:image/bmp,mime:image/gif,mime:image/jpeg,cmd:convert ${filename} -define jpeg:size=1280x1280 -thumbnail "1280x1280>" cq5dam.web.1280.1280.jpeg`

>[!NOTE]
>
>[!UICONTROL CommandLineProcess]ステップは、アセット（タイプ`dam:Asset`のノード）またはアセットの子孫にのみ適用されます。

>[!MORELIKETHIS]
>
>* [アセットの処理](assets-workflow.md)

