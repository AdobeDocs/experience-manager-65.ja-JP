---
title: Batch APIを使用して複数のインタラクティブな通信を生成する
description: Batch APIを使用して複数のインタラクティブな通信を生成する
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communication
translation-type: tm+mt
source-git-commit: 6a29cf13c89b71f851c67f85b01e8e648c0896b9

---


# Batch APIを使用して複数のインタラクティブな通信を生成する {#use-batch-api-to-generate-multiple-ic}

Batch APIを使用すると、テンプレートから複数のインタラクティブな通信を作成できます。 テンプレートは、データのないインタラクティブな通信です。 Batch APIは、データをテンプレートと組み合わせて、インタラクティブな通信を生成します。 このAPIは、インタラクティブ通信の大量生産に役立ちます。 例えば、電話料金、複数の顧客のクレジットカード明細などです。

Batch APIは、JSON形式のレコード（データ）とフォームデータモデルから受け取ります。 生成されるインタラクティブ通信の数は、設定されたフォームデータモデルの入力JSONファイルで指定されたレコード数と等しくなります。 APIを使用して、印刷出力とWeb出力の両方を生成できます。 「PRINT」オプションを選択するとPDFドキュメントが生成され、「WEB」オプションを選択すると個々のレコードのJSON形式のデータが生成されます。

## Batch APIの使用 {#using-the-batch-api}

Batch APIは、監視フォルダーと組み合わせて、またはスタンドアロンのRest APIとして使用できます。 Batch APIを使用するために、生成されるインタラクティブ通信のテンプレート、出力タイプ（HTML、PRINTまたはその両方）、ロケール、事前入力サービスおよび名前を設定します。

レコードをインタラクティブな通信テンプレートと組み合わせて、インタラクティブな通信を作成します。 Batch APIは、レコード（インタラクティブな通信テンプレートのデータ）をJSONファイルから直接読み取るか、フォームデータモデルを介してアクセスした外部データソースから読み取ることができます。 各レコードを個別のJSONファイルに保存するか、JSON配列を作成してすべてのレコードを1つのファイルに保存することができます。

**JSONファイル内の単一のレコード**

```JSON
{
   "employee": {
       "name": "Sara",
       "id": 3,
       "mobileNo": 9871996463,
       "age": 37
   }
}
```

**JSONファイル内の複数のレコード**

```JSON
[{
   "employee": {
       "name": "John",
       "id": 1,
       "mobileNo": 9871996461,
       "age": 39
   }
},{
   "employee": {
       "name": "Jacob",
       "id": 2,
       "mobileNo": 9871996462,
       "age": 38
   }
},{
   "employee": {
       "name": "Sara",
       "id": 3,
       "mobileNo": 9871996463,
       "age": 37
   }
}]
```

### Batch APIと監視フォルダーの使用 {#using-the-batch-api-watched-folders}

APIを簡単に体験できるように、AEM Formsでは、Batch APIを使用するように設定された監視フォルダーサービスをすぐに使用できます。 AEM Forms UIを介してサービスにアクセスし、複数のインタラクティブな通信を生成できます。 また、必要に応じてカスタムサービスを作成することもできます。 以下に示す方法を使用して、監視フォルダーでBatch APIを使用できます。

* インタラクティブな通信を生成するためのJSONファイル形式の入力データ（レコード）の指定
* 外部データソースに保存され、フォームデータモデルを介してアクセスされる入力データ（レコード）を使用して、インタラクティブな通信を作成する

#### インタラクティブな通信を生成するためのJSONファイル形式の入力データレコードの指定 {#specify-input-data-in-JSON-file-format}

レコードをインタラクティブな通信テンプレートと組み合わせて、インタラクティブな通信を作成します。 レコードごとに個別のJSONファイルを作成するか、JSON配列を作成してすべてのレコードを単一のファイルに保持することができます。

JSONファイルに保存されたレコードからインタラクティブな通信を作成するには：

1. 監視フォル [ダーを作成](https://docs.adobe.com/content/help/en/experience-manager-64/forms/publish-process-aem-forms/creating-configure-watched-folder.html) 、Batch APIを使用するように設定します。
   1. AEM Forms作成者インスタンスにログインします。
   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Forms]** > **[!UICONTROL Configure Watched Folder]**. 「**[!UICONTROL 新規]**」をタップします。
   1. フォルダ **[!UICONTROL ーの名前]** と物 **[!UICONTROL 理パス]** を指定します。 例： `c:\batchprocessing`
   1. 「次を使用し **[!UICONTROL てファイルを処]** 理」フィールドで「サービス **** 」オプションを選択します。
   1. 「サービ **[!UICONTROL ス名」フィールドで、com.adobe.fd.ccm.multichannel.batch.impl.service.InteractiveCommunicationBatchServiceImpl]** サービスを **[!UICONTROL 選択します]** 。
   1. 出力ファイル **[!UICONTROL パターンを指定]**。 例えば、%F/パターンは [](https://helpx.adobe.com/experience-manager/6-5/forms/using/admin-help/configuring-watched-folder-endpoints.html#about_file_patterns) 、監視フォルダーがWatched Folder\inputフォルダーのサブフォルダー内の入力ファイルを検索できるように指定します。
1. 詳細パラメータの設定：
   1. 「詳細」タブ **[!UICONTROL を開き]** 、次のカスタムプロパティを追加します。

      | プロパティ | タイプ | 説明 |
      |--- |--- |--- |
      | templatePath | String | 使用するインタラクティブ通信テンプレートのパスを指定します。 例えば、/content/dam/formsanddocuments/testsample/mediumicのように指定します。 これは必須プロパティです。 |
      | recordPath | String | recordPathフィールドの値は、インタラクティブ通信の名前を設定するのに役立ちます。 レコードのフィールドのパスをrecordPathフィールドの値として設定できます。 例えば、/employee/Idを指定した場合、idフィールドの値は、対応する対話型通信の名前になります。 デフォルト値はランダムなランダ [ムUUIDです](https://docs.oracle.com/javase/7/docs/api/java/util/UUID.html#randomUUID())。 |
      | usePrefillService | Boolean | 値をFalseに設定します。 usePrefillServiceパラメーターを使用すると、対応するインタラクティブ通信用に設定された事前入力サービスから取得したデータを、インタラクティブ通信に事前入力できます。 usePrefillServiceがtrueに設定されている場合、（各レコードの）入力JSONデータはFDM引数として扱われます。 デフォルト値は false です。 |
      | batchType | String | 値をPRINT、WEBまたはWEB_AND_PRINTに設定します。 デフォルト値はWEB_AND_PRINTです。 |
      | locale | String | 出力インタラクティブ通信のロケールを指定します。 標準搭載のサービスではロケールオプションは使用されませんが、カスタムサービスを作成して、ローカライズされたインタラクティブ通信を生成することができます。 デフォルト値はen_USです。 |

   1. 「作成」 **[!UICONTROL をタップし]** 、監視フォルダーが作成されます。
1. 監視フォルダーを使用してインタラクティブな通信を生成します。
   1. 監視フォルダーを開きます。 入力フォルダーに移動します。
   1. 入力フォルダーにフォルダーを作成し、新しく作成したフォルダーにJSONファイルを配置します。
   1. 監視フォルダーがファイルを処理するのを待ちます。 処理開始ーの場合、入力ファイルとそのファイルを含むサブフォルダーがステージングフォルダーに移動されます。
   1. 出力フォルダーを開き、出力表示ーを指定します。
      * 「監視フォルダーの設定」でPRINTオプションを指定すると、インタラクティブ通信のPDF出力が生成されます。
      * 監視フォルダーの設定でWEBオプションを指定すると、レコードごとのJSONファイルが生成されます。 このJSONファイルを使用して、Webテンプ [レートに事前入力できます](#web-template)。
      * PRINTとWEBの両方のオプションを指定すると、PDFドキュメントとレコードあたりのJSONファイルの両方が生成されます。

#### 外部データソースに保存され、フォームデータモデルを介してアクセスされる入力データを使用して、インタラクティブな通信を生成する {#use-fdm-as-data-source}

外部データソースに保存されたデータ（レコード）をインタラクティブな通信テンプレートと組み合わせて、インタラクティブな通信を作成します。 インタラクティブな通信を作成する場合、フォームデータモデル(FDM)を介して外部データソースに接続し、データにアクセスします。 外部データソースから同じフォームデータモデルを使用してデータを取得するように、監視フォルダーのバッチ処理サービスを設定できます。 外部デ [ータ・ソースに保存されたレコードからインタラクティブな通信を作成するには](https://docs.adobe.com/content/help/en/experience-manager-64/forms/form-data-model/work-with-form-data-model.html):

1. テンプレートのフォームデータモデルの設定：
   1. インタラクティブ通信テンプレートに関連付けられたフォームデータモデルを開きます。
   1. 最上位モデルオブジェクトを選択し、「プロパティを編集」をタップします。
   1. 「プロパティの編集」ペインの「サービスの読み取り」フィールドから、取得または取得サービスを選択します。
   1. 読み取りサービスの引数の鉛筆アイコンをタップして、引数をリクエスト属性に連結し、連結値を指定します。 これにより、指定したバインド属性またはリテラル値にサービスの引数がバインドされ、それが引数としてサービスに渡され、指定した値に関連付けられている詳細情報がデータソースから取得されます。

      <br>
        この例では、id引数はユーザープロファイルのid属性の値を受け取り、読み取りサービスに引数として渡します。 指定したIDの従業員データモデルオブジェクトから関連するプロパティの値を読み取り、返します。 So, if you specify 00250 in the id field in the form, the read service will read details of the employee with 00250 employee id.
        <br>

      ![リクエスト属性の設定](assets/request-attribute.png)

   1. プロパティとフォームデータモデルを保存します。
1. リクエスト属性の値の設定：
   1. ファイルシステム上に.jsonファイルを作成し、編集用に開きます。
   1. JSON配列を作成し、フォームデータモデルからデータを取得するためのプライマリ属性を指定します。 例えば、次のJSONは、FDMにIDが27126または27127のレコードのデータを送信するよう要求します。

      ```json
          [
              {
                  "id": 27126
              },
              {
                  "id": 27127
              }
          ]
      ```

   1.  ファイルを保存して閉じます。

1. 監視フォル [ダーを作成し](https://docs.adobe.com/content/help/en/experience-manager-64/forms/publish-process-aem-forms/creating-configure-watched-folder.html) 、Batch APIサービスを使用するように設定します。
   1. AEM Forms作成者インスタンスにログインします。
   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Forms]** > **[!UICONTROL Configure Watched Folder]**. 「**[!UICONTROL 新規]**」をタップします。
   1. フォルダ **[!UICONTROL ーの名前]** と物 **[!UICONTROL 理パス]** を指定します。 例： `c:\batchprocessing`
   1. 「次を使用し **[!UICONTROL てファイルを処]** 理」フィールドで「サービス **** 」オプションを選択します。
   1. 「サービ **[!UICONTROL ス名」フィールドで、com.adobe.fd.ccm.multichannel.batch.impl.service.InteractiveCommunicationBatchServiceImpl]** サービスを **[!UICONTROL 選択します]** 。
   1. 出力ファイル **[!UICONTROL パターンを指定]**。 例えば、%F/パターンは [](https://helpx.adobe.com/experience-manager/6-5/forms/using/admin-help/configuring-watched-folder-endpoints.html#about_file_patterns) 、監視フォルダーがWatched Folder\inputフォルダーのサブフォルダー内の入力ファイルを検索できるように指定します。
1. 詳細パラメータの設定：
   1. 「詳細」タブ **[!UICONTROL を開き]** 、次のカスタムプロパティを追加します。

      | プロパティ | タイプ | 説明 |
      |--- |--- |--- |
      | templatePath | String | 使用するインタラクティブ通信テンプレートのパスを指定します。 例えば、/content/dam/formsanddocuments/testsample/mediumicのように指定します。 これは必須プロパティです。 |
      | recordPath | String | recordPathフィールドの値は、インタラクティブ通信の名前を設定するのに役立ちます。 レコードのフィールドのパスをrecordPathフィールドの値として設定できます。 例えば、/employee/Idを指定した場合、idフィールドの値は、対応する対話型通信の名前になります。 デフォルト値はランダムなランダ [ムUUIDです](https://docs.oracle.com/javase/7/docs/api/java/util/UUID.html#randomUUID())。 |  |
      | usePrefillService | Boolean | 値をTrueに設定します。 デフォルト値は false です。この値をtrueに設定すると、Batch APIは設定されたフォームデータモデルからデータを読み取り、インタラクティブ通信に入力します。 usePrefillServiceがtrueに設定されている場合、（各レコードの）入力JSONデータはFDM引数として扱われます。 |
      | batchType | String | 値をPRINT、WEBまたはWEB_AND_PRINTに設定します。 デフォルト値はWEB_AND_PRINTです。 |
      | locale | String | 出力インタラクティブ通信のロケールを指定します。 標準搭載のサービスではロケールオプションは使用されませんが、カスタムサービスを作成して、ローカライズされたインタラクティブ通信を生成することができます。 デフォルト値はen_USです。 |

   1. 「作成」 **[!UICONTROL をタップし]** 、監視フォルダーが作成されます。
1. 監視フォルダーを使用してインタラクティブな通信を生成します。
   1. 監視フォルダーを開きます。 入力フォルダーに移動します。
   1. 入力フォルダーにフォルダーを作成します。 手順2で作成したJSONファイルを新しく作成したフォルダーに配置します。
   1. 監視フォルダーがファイルを処理するのを待ちます。 処理開始ーの場合、入力ファイルとそのファイルを含むサブフォルダーがステージングフォルダーに移動されます。
   1. 出力フォルダーを開き、出力表示ーを指定します。
      * 「監視フォルダーの設定」でPRINTオプションを指定すると、インタラクティブ通信のPDF出力が生成されます。
      * 監視フォルダーの設定でWEBオプションを指定すると、レコードごとのJSONファイルが生成されます。 このJSONファイルを使用して、Webテンプ [レートに事前入力できます](#web-template)。
      * PRINTとWEBの両方のオプションを指定すると、PDFドキュメントとレコードあたりのJSONファイルの両方が生成されます。

## REST要求を使用したBatch APIの呼び出し

Representational State Transfer(REST [)リクエストを使用して](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/index.html) 、Batch APIを呼び出すことができます。 RESTエンドポイントを他のユーザーに提供して、APIにアクセスし、インタラクティブ通信を処理、保存、カスタマイズするための独自のメソッドを設定できます。 独自のカスタムJavaサーブレットを開発し、AEMインスタンスにAPIをデプロイできます。

Javaサーブレットをデプロイする前に、インタラクティブな通信を行い、対応するデータファイルの準備が整っていることを確認します。 次の手順を実行して、Javaサーブレットを作成し、デプロイします。

1. AEMインスタンスにログインし、インタラクティブ通信を作成します。 以下のサンプルコードで説明したインタラクティブな通信を使用するには、ここをク [リックしま](assets/SimpleMediumIC.zip)す。
1. [AEMインスタンスでApache Mavenを使用してAEMプロジェクトを構築](https://helpx.adobe.com/experience-manager/using/maven_arch13.html) 、デプロイします。
1. AEM追加プロジェクトのPOmファイルの依存リストにある [AEM Forms Client SDKバージョン6.0.12以降および最新の](https://repo.adobe.com/nexus/content/repositories/public/com/adobe/aemfd/aemfd-client-sdk/) AEM Uber [](https://docs.adobe.com/content/help/en/experience-manager-65/release-notes/service-pack/sp-release-notes.html#uber-jar) Jar。 以下に例を示します。

   ```XML
       <dependency>
           <groupId>com.adobe.aemfd</groupId>
           <artifactId>aemfd-client-sdk</artifactId>
           <version>6.0.122</version>
       </dependency>
       <dependency>
          <groupId>com.adobe.aem</groupId>
          <artifactId>uber-jar</artifactId>
          <version>6.5.0</version>
          <classifier>apis</classifier>
          <scope>provided</scope>
       </dependency>
   ```

1. Javaプロジェクトを開き、CCMBatchServlet.javaなどの.javaファイルを作成します。 次のコードを ファイルに追加します。

   ```java
           package com.adobe.fd.ccm.multichannel.batch.integration;
   
           import java.io.File;
           import java.io.FileInputStream;
           import java.io.FileOutputStream;
           import java.io.IOException;
           import java.io.InputStream;
           import java.io.OutputStream;
           import java.io.PrintWriter;
           import java.util.List;
           import java.util.logging.FileHandler;
           import java.util.logging.Logger;
           import java.util.logging.SimpleFormatter;
   
           import javax.servlet.Servlet;
           import javax.servlet.ServletContext;
   
           import com.adobe.aemfd.watchfolder.service.api.ContentProcessor;
   
           import org.apache.commons.io.IOUtils;
           import org.apache.sling.api.SlingHttpServletRequest;
           import org.apache.sling.api.SlingHttpServletResponse;
           import org.apache.sling.api.servlets.SlingAllMethodsServlet;
           import org.json.JSONArray;
           import org.json.JSONObject;
           import org.osgi.service.component.annotations.Component;
           import org.osgi.service.component.annotations.Reference;
   
           import com.adobe.aemfd.docmanager.Document;
           import com.adobe.aemfd.docmanager.passivation.DocumentPassivationHandler;
           import com.adobe.fd.ccm.multichannel.batch.api.factory.BatchComponentBuilderFactory;
           import com.adobe.fd.ccm.multichannel.batch.api.model.BatchConfig;
           import com.adobe.fd.ccm.multichannel.batch.api.model.BatchInput;
           import com.adobe.fd.ccm.multichannel.batch.api.model.BatchResult;
           import com.adobe.fd.ccm.multichannel.batch.api.model.BatchType;
           import com.adobe.fd.ccm.multichannel.batch.api.model.RecordResult;
           import com.adobe.fd.ccm.multichannel.batch.api.model.RenditionResult;
           import com.adobe.fd.ccm.multichannel.batch.api.service.BatchGeneratorService;
           import com.adobe.fd.ccm.multichannel.batch.util.BatchConstants;
           import com.adobe.icc.render.obj.Content;
   
           import javax.annotation.PostConstruct;
           import javax.inject.Inject;
           import javax.inject.Named;
   
           import org.apache.sling.api.resource.Resource;
           import org.apache.sling.models.annotations.Default;
           import org.apache.sling.models.annotations.Model;
           import org.apache.sling.settings.SlingSettingsService;
           import org.apache.sling.api.resource.ResourceUtil;
   
   
           import org.slf4j.*;
           import java.util.Date;
   
           @Component(service=Servlet.class,
           property={
                   "sling.servlet.methods=GET",
                   "sling.servlet.paths="+ "/bin/batchServlet"
           })
           public class CCMBatchServlet extends SlingAllMethodsServlet {
   
               @Reference
               private BatchGeneratorService batchGeneratorService;
               @Reference
               private BatchComponentBuilderFactory batchBuilderFactory;
               public void doGet(SlingHttpServletRequest req, SlingHttpServletResponse resp) {
                   try {
                       executeBatch(req,resp);
                   } catch (Exception e) {
                       e.printStackTrace();
                   }
               }
               private void executeBatch(SlingHttpServletRequest req, SlingHttpServletResponse resp) throws Exception {
                   int count = 0;
                   JSONArray inputJSONArray = new JSONArray();
                   String filePath = req.getParameter("filePath");
                   InputStream is = new FileInputStream(filePath);
                   String data = IOUtils.toString(is);
                   try {
                       // If input file is json object, then create json object and add in json array, if not then try for json array
                       JSONObject inputJSON = new JSONObject(data);
                       inputJSONArray.put(inputJSON);
                   } catch (Exception e) {
                       try {
                           // If input file is json array, then iterate and add all objects into inputJsonArray otherwise throw exception
                           JSONArray inputArray = new JSONArray(data);
                           for(int i=0;i<inputArray.length();i++) {
                               inputJSONArray.put(inputArray.getJSONObject(i));
                           }
                       } catch (Exception ex) {
                           throw new Exception("Invalid JSON Data. File name : " + filePath, ex);
                       }
                   }
                   BatchInput batchInput = batchBuilderFactory.getBatchInputBuilder().setData(inputJSONArray).setTemplatePath("/content/dam/formsanddocuments/[path of the interactive communcation]").build();
                   BatchConfig batchConfig = batchBuilderFactory.getBatchConfigBuilder().setBatchType(BatchType.WEB_AND_PRINT).build();
                   BatchResult batchResult = batchGeneratorService.generateBatch(batchInput, batchConfig);
                   List<RecordResult> recordList = batchResult.getRecordResults();
                   JSONObject result = new JSONObject();
                   for (RecordResult recordResult : recordList) {
                       String recordId = recordResult.getRecordID();
                       for (RenditionResult renditionResult : recordResult.getRenditionResults()) {
                           if (renditionResult.isRecordPassed()) {
                               InputStream output = renditionResult.getDocumentStream().getInputStream();
                               result.put(recordId +"_"+renditionResult.getContentType(), output);
   
                               Date date= new Date();
                               long time = date.getTime();
   
                               // Print output
                               if(getFileExtension(renditionResult.getContentType()).equalsIgnoreCase(".json")) {
                                   File file = new File(time + getFileExtension(renditionResult.getContentType()));
                                   copyInputStreamToFile(output, file);
                               } else
                               {
                                   File file = new File(time + getFileExtension(renditionResult.getContentType()));
                                   copyInputStreamToFile(output, file);
                               }
                           }
                       }
                   }
                   PrintWriter writer = resp.getWriter();
                   JSONObject resultObj = new JSONObject();
                   resultObj.put("result", result);
                   writer.write(resultObj.toString());
               }
   
   
               private static void copyInputStreamToFile(InputStream inputStream, File file)
                       throws IOException {
   
                       try (FileOutputStream outputStream = new FileOutputStream(file)) {
   
                           int read;
                           byte[] bytes = new byte[1024];
   
                           while ((read = inputStream.read(bytes)) != -1) {
                               outputStream.write(bytes, 0, read);
                           }
   
                       }
   
                   }
   
   
               private String getFileExtension(String contentType) {
                   if (contentType.endsWith(BatchConstants.JSON)) {
                       return ".json";
                   } else return ".pdf";
               }
   
   
           }
   ```

1. 上記のコードで、テンプレートパス(setTemplatePath)をテンプレートのパスに置き換え、setBatchType APIの設定値を次のように指定します。
   * PRINTオプションを指定すると、インタラクティブ通信のPDF出力が生成されます。
   * WEBオプションを指定すると、レコードごとにJSONファイルが生成されます。 このJSONファイルを使用して、Webテンプ [レートに事前入力できます](#web-template)。
   * PRINTとWEBの両方のオプションを指定すると、PDFドキュメントとレコードあたりのJSONファイルの両方が生成されます。

1. [mavenを使用して、更新したコードをAEMインスタンスにデプロイします](https://helpx.adobe.com/experience-manager/using/maven_arch13.html#BuildtheOSGibundleusingMaven)。
1. バッチAPIを呼び出して、インタラクティブ通信を生成します。 バッチAPIは、レコード数に応じてPDFファイルと.jsonファイルのストリームを印刷します。 このJSONファイルを使用して、Webテンプ [レートに事前入力できます](#web-template)。 上記のコードを使用する場合、APIはにデプロイされま `http://localhost:4502/bin/batchServlet`す。 このコードは、PDFファイルとJSONファイルのストリームを印刷して返します。

### Webテンプレートの事前入力 {#web-template}

batchTypeを設定してWebチャネルをレンダリングすると、APIはすべてのデータレコードに対してJSONファイルを生成します。 次の構文を使用して、JSONファイルと対応するWebチャネルを結合し、インタラクティブな通信を生成できます。

**構文**`http://host:port/<template-path>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=<guide-merged-json-path>`

**例** JSONファイルがにあり、次のインタラクティブ通 `C:\batch\mergedJsonPath.json` 信テンプレートを使用する場合： `http://host:port/content/dam/formsanddocuments/testsample/mediumic/jcr:content?channel=web`

次に、パブリッシュノード上の次のURLは、インタラクティブ通信のWfcチャネルを表示する`http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=file:///C:/batch/mergedJsonData.json`

データをファイルシステムに保存する以外に、JSONファイルをCRX-repository、ファイルシステム、Webサーバーに保存するか、OSGI事前入力サービスを介してデータにアクセスできます。 様々なプロトコルを使用してデータを結合する構文を次に示します。

* **CRXプロトコル**
   `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=crx:///tmp/fd/af/mergedJsonData.json`

* **ファイルプロトコル**
   `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=file:///C:/Users/af/mergedJsonData.json`

* **事前入力サービスプロトコル**
   `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=service://[SERVICE_NAME]/[IDENTIFIER]`

   SERVICE_NAME は OSGI 事前入力サービスの名前を参照します。「事前入力サービスの作成と実行」を参照してください。

   IDENTIFIER は、事前入力データを取得するために OSGI 事前入力サービスが必要とするメタデータを参照します。ログイン済みユーザーの識別子は、使用できるメタデータの一例です。

* **HTTPプロトコル**
   `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=http://localhost:8000/somesamplexmlfile.xml`

>[!NOTE]
> CRXプロトコルのみがデフォルトで有効になっています。 その他のサポートされているプロトコルを有効にするには、Configuration Managerを使 [用した事前入力サービスの設定を参照してくださ](https://helpx.adobe.com/experience-manager/6-5/forms/using/prepopulate-adaptive-form-fields.html#ConfiguringprefillserviceusingConfigurationManager)い。
