---
title: Batch API を使用して複数のインタラクティブ通信を生成する
description: Batch API を使用して複数のインタラクティブ通信を生成する
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communication
feature: Interactive Communication
exl-id: f65d8eb9-4d2c-4a6e-825f-45bcfaa7ca75
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '2228'
ht-degree: 99%

---

# Batch API を使用して複数のインタラクティブ通信を生成する {#use-batch-api-to-generate-multiple-ic}

Batch API を使用すると、テンプレートから複数のインタラクティブ通信を作成できます。テンプレートは、データのないインタラクティブ通信です。Batch API は、データとテンプレートを組み合わせて、インタラクティブな通信を作成します。この API は、インタラクティブ通信を大量に作成する際に役立ちます。例えば、複数の顧客に電話料金やクレジットカードの明細書を送信する場合です。

バッチ API は、フォームデータモデルから JSON 形式のレコード（データ）を受け取ります。生成されるインタラクティブ通信の数は、設定したフォームデータモデル内の入力 JSON ファイルで指定されたレコード数と等しくなります。API を使用して、印刷出力と Web 出力の両方を生成できます。「PRINT」オプションを選択すると PDF ドキュメントが生成され、「WEB」オプションを選択すると個々のレコードの JSON 形式のデータが生成されます。

## Batch API の使用 {#using-the-batch-api}

Batch API は、監視フォルダーと組み合わせて使用することも、スタンドアロンの Rest API として使用することもできます。Batch API を使用するには、生成されるインタラクティブ通信のテンプレート、出力タイプ （HTML、印刷、または両方）、ロケール、事前入力サービス、名前を設定します。

レコードとインタラクティブ通信テンプレートを組み合わせて、インタラクティブ通信を作成します。Batch API は、JSON ファイルから直接レコード（インタラクティブ通信テンプレートのデータ）を読み取ることも、フォームデータモデルを介してアクセスする外部データソースから読み取ることもできます。各レコードを別々の JSON ファイルに保持するか、JSON 配列を作成してすべてのレコードを 1 つのファイルに保持できます。

**JSON ファイル内の 1 つのレコード**

```json
{
   "employee": {
       "name": "Sara",
       "id": 3,
       "mobileNo": 9871996463,
       "age": 37
   }
}
```

**JSON ファイル内の複数のレコード**

```json
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

### 監視フォルダーでの Batch API の使用 {#using-the-batch-api-watched-folders}

API を簡単に操作できるように、AEM Forms には、Batch API を使用するように設定された監視フォルダーサービスが標準で用意されています。AEM Forms UI 経由でこのサービスにアクセスして、複数のインタラクティブ通信を生成できます。また、必要に応じて、カスタムサービスを作成することもできます。次に示すメソッドを使用して、監視フォルダーで Batch API を使用できます。

* インタラクティブ通信を作成するには、JSON ファイル形式で入力データ（レコード）を指定します
* インタラクティブ通信を作成するには、外部データソースに保存され、フォームデータモデルを介してアクセスされる入力データ（レコード）を使用します

#### インタラクティブ通信を作成するには、JSON ファイル形式の入力データレコードを指定します {#specify-input-data-in-JSON-file-format}

レコードとインタラクティブ通信テンプレートを組み合わせて、インタラクティブ通信を作成します。各レコードに対して個別の JSON ファイルを作成するか、すべてのレコードを 1 つのファイルに保持する JSON 配列を作成できます。

JSON ファイルに保存されたレコードからインタラクティブ通信を作成するには：

1. [監視フォルダー](https://experienceleague.adobe.com/docs/experience-manager-64/forms/publish-process-aem-forms/creating-configure-watched-folder.html)を作成して、Batch API を使用するように設定します。
   1. AEM Forms オーサーインスタンスにログインします。
   1. **[!UICONTROL ツール]**／**[!UICONTROL Forms]**／**[!UICONTROL 監視フォルダーを設定]**&#x200B;に移動します。「**[!UICONTROL 新規]**」をタップします。
   1. フォルダーの&#x200B;**[!UICONTROL 名前]**&#x200B;と物理的&#x200B;**[!UICONTROL パス]**&#x200B;を指定します。例えば、`c:\batchprocessing` のように指定します。
   1. **[!UICONTROL 次を使用してファイルを処理]**&#x200B;フィールドで「**[!UICONTROL サービス]**」オプションを選択します。
   1. **[!UICONTROL サービス名]**&#x200B;フィールドで、**[!UICONTROL com.adobe.fd.ccm.multichannel.batch.impl.service.InteractiveCommunicationBatchServiceImpl]** サービスを選択します。
   1. **[!UICONTROL 出力ファイルパターン]**&#x200B;を指定します。例：%F/ [pattern](https://experienceleague.adobe.com/docs/experience-manager-65/forms/administrator-help/manage-endpoints/configuring-watched-folder-endpoints.html?lang=ja) は、監視フォルダーが Watched Folder\input フォルダーのサブフォルダー内で入力ファイルを見つけることを指定します。
1. 以下の手順に従って、詳細設定パラメーターを設定します。
   1. 「**[!UICONTROL 詳細]**」タブを開いて、次のカスタムプロパティを追加します。

      | プロパティ | 型 | 説明 |
      |--- |--- |--- |
      | templatePath | 文字列 | 使用するインタラクティブ通信テンプレートのパスを指定します。例えば、 /content/dam/formsanddocuments/testsample/mediumic のように指定します。これは必須プロパティです。 |
      | recordPath | 文字列 | recordPath フィールドの値は、インタラクティブ通信の名前を設定するのに役立ちます。レコードのフィールドのパスは、recordPath フィールドの値として設定できます。例えば、 /employee/Id を指定した場合、id フィールドの値は、対応するインタラクティブ通信の名前になります。デフォルト値はランダムな[random UUID](https://docs.oracle.com/javase/7/docs/api/java/util/UUID.html#randomUUID()) です。 |
      | usePrefillService | Boolean | 値を False に設定します。usePrefillService パラメーターを使用すると、対応するインタラクティブ通信用に設定された事前入力サービスから取得したデータを、インタラクティブ通信に事前入力することができます。usePrefillService が true に設定されている場合、（レコードごとに）入力された JSON データは FDM 引数として扱われます。デフォルト値は false です。 |
      | batchType | 文字列 | 値を PRINT、WEB、または WEB_AND_PRINT に設定します。デフォルト値は WEB_AND_PRINT です。 |
      | locale | 文字列 | 出力インタラクティブ通信のロケールを指定します。そのまま使用できるサービスでは、ロケールオプションは使用されませんが、カスタムサービスを作成して、ローカライズされたインタラクティブ通信を生成することができます。デフォルト値は en_US です。 |

   1. 「**[!UICONTROL 作成]**」をタップすると、監視フォルダーが作成されます。
1. 監視フォルダーを使用してインタラクティブ通信を生成します。
   1. 監視フォルダーを開きます。入力フォルダーに移動します。
   1. 入力フォルダーにフォルダーを作成し、新しく作成したフォルダーに JSON ファイルを配置します。
   1. 監視フォルダーがファイルを処理するのを待ちます。処理が開始されると、入力ファイルと、そのファイルを含むサブフォルダーがステージングフォルダーに移動します。
   1. 出力フォルダーを開いて出力を表示します。
      * 監視フォルダー設定で PRINT オプションを指定すると、インタラクティブ PDF の通信出力が生成されます。
      * 監視フォルダー設定で WEB オプションを指定すると、レコードごとに JSON ファイルが生成されます。JSON ファイルを使用して [Web テンプレートに事前入力](#web-template)できます。
      * PRINT オプションと WEB オプションの両方を指定すると、レコードごとに PDF ドキュメントと JSON ファイルの両方が生成されます。

#### 外部データソースに保存され、フォームデータモデルを介してアクセスされる入力データを使用して、インタラクティブ通信を作成する {#use-fdm-as-data-source}

外部データソースに保存されたデータ（レコード）とインタラクティブ通信テンプレートを組み合わせて、インタラクティブ通信を作成できます。インタラクティブ通信を作成する場合は、フォームデータモデル（FDM）を介して外部データソースに接続し、データにアクセスします。外部データソースから同じフォームデータモデルを使用してデータを取得するように、監視フォルダーのバッチ処理サービスを設定できます。[外部データソースに保存されたレコードからインタラクティブ通信を作成する](https://experienceleague.adobe.com/docs/experience-manager-64/forms/form-data-model/work-with-form-data-model.html)には、次をおこないます。

1. テンプレートのフォームデータモデルを設定します。
   1. インタラクティブ通信テンプレートに関連付けたフォームデータモデルを開きます。
   1. トップレベルモデルオブジェクトを選択し、「プロパティを編集」をタップします。
   1. プロパティの編集ペインの「サービスの読み取り」フィールドから、サービス取得を選択します。
   1. 読み取りサービスの引数の鉛筆アイコンをタップして、引数をリクエスト属性にバインドし、バインド値を指定します。これにより、指定したバインド属性またはリテラル値にサービスの引数がバインドされ、それが引数としてサービスに渡され、指定した値に関連付けられている詳細情報がデータソースから取得されます。

      <br>
    この例では、id 引数を使用してユーザープロファイルの id 属性の値を取得し、それを引数として読み取りサービスに渡しています。指定された id について、employee データモデルオブジェクトから関連プロパティの値が読み取られ、その値がシステムに返されます。そのため、フォームの id フィールドに「00250」という値を入力すると、読み取りサービスは、従業員 ID に「00250」と設定されている従業員の詳細情報を読み取ります。
       <br>

      ![リクエスト属性の設定](assets/request-attribute.png)

   1. プロパティとフォームデータモデルを保存します。
1. リクエスト属性の値を設定：
   1. .json ファイルをファイルシステム上に作成し、編集用に開きます。
   1. JSON 配列を作成し、フォームデータモデルからデータを取得するためのプライマリ属性を指定します。例えば、次の JSON は FDM に対し、id が 27126 または 27127 のレコードのデータを送信するようにリクエストします。

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

   1. ファイルを保存して閉じます。

1. [監視フォルダー](https://experienceleague.adobe.com/docs/experience-manager-64/forms/publish-process-aem-forms/creating-configure-watched-folder.html)を作成して、Batch API サービスを使用するように設定します。
   1. AEM Forms オーサーインスタンスにログインします。
   1. **[!UICONTROL ツール]**／**[!UICONTROL Forms]**／**[!UICONTROL 監視フォルダーを設定]**&#x200B;に移動します。「**[!UICONTROL 新規]**」をタップします。
   1. フォルダーの&#x200B;**[!UICONTROL 名前]**&#x200B;と物理的&#x200B;**[!UICONTROL パス]**&#x200B;を指定します。例えば、`c:\batchprocessing` のように指定します。
   1. **[!UICONTROL 次を使用してファイルを処理]**&#x200B;フィールドで「**[!UICONTROL サービス]**」オプションを選択します。
   1. **[!UICONTROL サービス名]**&#x200B;フィールドで、**[!UICONTROL com.adobe.fd.ccm.multichannel.batch.impl.service.InteractiveCommunicationBatchServiceImpl]** サービスを選択します。
   1. **[!UICONTROL 出力ファイルパターン]**&#x200B;を指定します。例：%F/ [pattern](https://helpx.adobe.com/experience-manager/6-5/forms/using/admin-help/configuring-watched-folder-endpoints.html#about_file_patterns) は、監視フォルダーが Watched Folder\input フォルダーのサブフォルダー内で入力ファイルを見つけることを指定します。
1. 以下の手順に従って、詳細設定パラメーターを設定します。
   1. 「**[!UICONTROL 詳細]**」タブを開いて、次のカスタムプロパティを追加します。

      | プロパティ | 型 | 説明 |
      |--- |--- |--- |
      | templatePath | 文字列 | 使用するインタラクティブ通信テンプレートのパスを指定します。例えば、 /content/dam/formsanddocuments/testsample/mediumic のように指定します。これは必須プロパティです。 |
      | recordPath | 文字列 | recordPath フィールドの値は、インタラクティブ通信の名前を設定するのに役立ちます。レコードのフィールドのパスは、recordPath フィールドの値として設定できます。例えば、 /employee/Id を指定した場合、id フィールドの値は、対応するインタラクティブ通信の名前になります。デフォルト値はランダムな[random UUID](https://docs.oracle.com/javase/7/docs/api/java/util/UUID.html#randomUUID()) です。 |  |
      | usePrefillService | ブール値 | 値を True に設定します。デフォルト値は false です。値を true に設定すると、Batch API は設定されたフォームデータモデルからデータを読み取り、インタラクティブ通信に入力します。usePrefillService が true に設定されている場合、（レコードごとに）入力された JSON データは FDM 引数として扱われます。 |
      | batchType | 文字列 | 値を PRINT、WEB、または WEB_AND_PRINT に設定します。デフォルト値は WEB_AND_PRINT です。 |
      | ロケール | 文字列 | 出力インタラクティブ通信のロケールを指定します。そのまま使用できるサービスでは、ロケールオプションは使用されませんが、カスタムサービスを作成して、ローカライズされたインタラクティブ通信を生成することができます。デフォルト値は en_US です。 |

   1. 「**[!UICONTROL 作成]**」をタップすると、監視フォルダーが作成されます。
1. 監視フォルダーを使用してインタラクティブ通信を生成します。
   1. 監視フォルダーを開きます。入力フォルダーに移動します。
   1. 入力フォルダーにフォルダーを作成します。手順 2 で作成した JSON ファイルを、新しく作成したフォルダーに配置します。
   1. 監視フォルダーがファイルを処理するのを待ちます。処理が開始されると、入力ファイルと、そのファイルを含むサブフォルダーがステージングフォルダーに移動します。
   1. 出力フォルダーを開いて出力を表示します。
      * 監視フォルダー設定で PRINT オプションを指定すると、インタラクティブ PDF の通信出力が生成されます。
      * 監視フォルダー設定で WEB オプションを指定すると、レコードごとに JSON ファイルが生成されます。JSON ファイルを使用して [Web テンプレートに事前入力](#web-template)できます。
      * PRINT オプションと WEB オプションの両方を指定すると、レコードごとに PDF ドキュメントと JSON ファイルの両方が生成されます。

## REST リクエストを使用した Batch API の呼び出し

 [Batch API](https://helpx.adobe.com/jp/experience-manager/6-5/forms/javadocs/index.html) は Representational State Transfer（REST）リクエストを通じて呼び出すことができます。他のユーザーに REST エンドポイントを提供し、API へのアクセス、インタラクティブ通信の処理、保存とカスタマイズのための独自のメソッドを設定できるようにします。独自のカスタム Java サーブレットを開発して、AEM インスタンスに API をデプロイできます。

Java サーブレットをデプロイする前に、インタラクティブ通信があり、対応するデータファイルの準備が整っていることを確認します。次の手順を実行して、Java サーブレットの作成とデプロイをおこないます。

1. AEM インスタンスにログインし、インタラクティブ通信を作成します。以下のサンプルコードで説明するインタラクティブ通信を使用するには、[ここをクリック](assets/SimpleMediumIC.zip)してください。
1. AEM インスタンスで [Apache Maven を使用した AEM プロジェクトのビルドとデプロイ](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/aem-project-archetype.html?lang=ja)をおこないます。
1. AEM プロジェクトの POM ファイルの依存関係リストに [AEM Forms クライアント SDK バージョン 6.0.12](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=ja) 以降を追加します。例：

   ```xml
       <dependency>
           <groupId>com.adobe.aemfd</groupId>
           <artifactId>aemfd-client-sdk</artifactId>
           <version>6.0.122</version>
       </dependency>
   ```

1. Java プロジェクトを開き、.java ファイル（例：CCMBatchServlet.java）を作成します。次のコードをファイルに追加します。

   ```java
           package com.adobe.fd.ccm.multichannel.batch.integration;
   
           import java.io.File;
           import java.io.FileInputStream;
           import java.io.FileOutputStream;
           import java.io.IOException;
           import java.io.InputStream;
           import java.io.PrintWriter;
           import java.util.List;
           import javax.servlet.Servlet;
           import org.apache.commons.io.IOUtils;
           import org.apache.sling.api.SlingHttpServletRequest;
           import org.apache.sling.api.SlingHttpServletResponse;
           import org.apache.sling.api.servlets.SlingAllMethodsServlet;
           import org.json.JSONArray;
           import org.json.JSONObject;
           import org.osgi.service.component.annotations.Component;
           import org.osgi.service.component.annotations.Reference;
   
           import com.adobe.fd.ccm.multichannel.batch.api.builder.BatchConfigBuilder;
           import com.adobe.fd.ccm.multichannel.batch.api.factory.BatchComponentBuilderFactory;
           import com.adobe.fd.ccm.multichannel.batch.api.model.BatchConfig;
           import com.adobe.fd.ccm.multichannel.batch.api.model.BatchInput;
           import com.adobe.fd.ccm.multichannel.batch.api.model.BatchResult;
           import com.adobe.fd.ccm.multichannel.batch.api.model.BatchType;
           import com.adobe.fd.ccm.multichannel.batch.api.model.RecordResult;
           import com.adobe.fd.ccm.multichannel.batch.api.model.RenditionResult;
           import com.adobe.fd.ccm.multichannel.batch.api.service.BatchGeneratorService;
           import com.adobe.fd.ccm.multichannel.batch.util.BatchConstants;
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

1. 上記のコードで、テンプレートのパス（setTemplatePath）をテンプレートのパスに置き換え、setBatchType API の値を設定します。
   * プリントオプションを指定すると、インタラクティブ通信の PDF 出力が生成されます。
   * Web オプションを指定すると、レコードごとに JSON ファイルが生成されます。JSON ファイルを使用すると、[Web テンプレートの事前入力](#web-template)ができます。
   * PRINT オプションと WEB オプションの両方を指定すると、レコードごとに PDF ドキュメントと JSON ファイルの両方が生成されます。

1. [Maven を使用して、更新されたコードを AEM インスタンスにデプロイする](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/developing/aem-project-archetype.html?lang=ja)。
1. バッチ API を呼び出して、インタラクティブ通信を生成します。バッチ API では、レコード数に応じて、PDFと.json ファイルのストリームを出力して返します。JSON ファイルを使用すると、[Web テンプレートの事前入力](#web-template)ができます。上記のコードを使用する場合、API は `http://localhost:4502/bin/batchServlet` にデプロイされます。このコードは、PDF ファイルと JSON ファイルのストリームを出力して返します。

### Web テンプレートの事前入力 {#web-template}

Web チャネルをレンダリングする batchType を設定すると、API はデータレコードごとに JSON ファイルを生成します。次の構文を使用して、JSON ファイルを対応する Web チャネルに結合して、インタラクティブ通信を生成できます。

**構文**
`http://host:port/<template-path>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=<guide-merged-json-path>`

**例**
JSON ファイルが `C:\batch\mergedJsonPath.json` にあり、次のインタラクティブ通信テンプレートを使用する場合：`http://host:port/content/dam/formsanddocuments/testsample/mediumic/jcr:content?channel=web`

次に、パブリッシュノード上の次の URL は、インタラクティブ通信の Web チャネルを表示します
`http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=file:///C:/batch/mergedJsonData.json`

ファイルシステムにデータを保存する以外に、JSON ファイルを CRX リポジトリ、ファイルシステム、Web サーバーに保存するか、OSGI 事前入力サービスを介してデータにアクセスできます。様々なプロトコルを使用してデータを結合する構文は次のとおりです。

* **CRX プロトコル**

   `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=crx:///tmp/fd/af/mergedJsonData.json`

* **ファイルプロトコル**

   `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=file:///C:/Users/af/mergedJsonData.json`

* **事前入力サービスプロトコル**

   `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=service://[SERVICE_NAME]/[IDENTIFIER]`

   SERVICE_NAME とは OSGI 事前入力サービスの名前を指します。「事前入力サービスの作成と実行」を参照してください。

   識別情報とは、OSGI 事前入力サービスが事前入力データを取得するために必要なメタデータを指します。ログイン済みユーザーの識別子は、使用できるメタデータの一例です。

* **HTTP プロトコル**

   `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=http://localhost:8000/somesamplexmlfile.xml`

>[!NOTE]
>
>デフォルトでは、CRX プロトコルのみが有効になっています。その他のサポートされているプロトコルを有効にするには、[Configuration Manager を使用した事前入力サービスの設定](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/prepopulate-adaptive-form-fields.html?lang=ja)を参照してください。
