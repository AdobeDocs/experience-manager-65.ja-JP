---
title: Batch APIを使用して複数のインタラクティブ通信を生成する
description: Batch APIを使用して複数のインタラクティブ通信を生成する
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communication
feature: インタラクティブコミュニケーション
exl-id: f65d8eb9-4d2c-4a6e-825f-45bcfaa7ca75
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2239'
ht-degree: 7%

---

# Batch API {#use-batch-api-to-generate-multiple-ic}を使用して複数のインタラクティブ通信を生成する

Batch APIを使用すると、テンプレートから複数のインタラクティブ通信を作成できます。 テンプレートは、データのないインタラクティブ通信です。 Batch APIは、データとテンプレートを組み合わせて、インタラクティブ通信を作成します。 このAPIは、インタラクティブ通信を大量に生産する際に役立ちます。 例えば、電話料金、複数の顧客のクレジットカード明細などです。

バッチAPIは、JSON形式のレコード（データ）とフォームデータモデルから受け取ります。 生成されるインタラクティブ通信の数は、設定済みのフォームデータモデル内の入力JSONファイルで指定されたレコード数と等しくなります。 APIを使用して、印刷出力とWeb出力の両方を生成できます。 「PRINT」オプションを選択するとPDFドキュメントが生成され、「WEB」オプションを選択すると個々のレコードのJSON形式のデータが生成されます。

## バッチAPIの使用{#using-the-batch-api}

バッチAPIは、監視フォルダーと組み合わせて、またはスタンドアロンのRest APIとして使用できます。 Batch APIを使用するには、生成されるインタラクティブ通信のテンプレート、出力タイプ（HTML、PRINTまたはその両方）、ロケール、事前入力サービス、名前を設定します。

レコードとインタラクティブ通信テンプレートを組み合わせて、インタラクティブ通信を作成できます。 バッチAPIは、JSONファイルから直接、またはフォームデータモデルを介してアクセスする外部データソースから、レコード（インタラクティブ通信テンプレートのデータ）を読み取ることができます。 各レコードを別々のJSONファイルに保持するか、JSON配列を作成してすべてのレコードを1つのファイルに保持できます。

**JSONファイル内の単一のレコード**

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

**JSONファイル内の複数のレコード**

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

### 監視フォルダーでのバッチAPIの使用{#using-the-batch-api-watched-folders}

APIを簡単に操作できるように、AEM Formsには、Batch APIを使用するように設定された監視フォルダーサービスが標準で用意されています。 AEM Forms UIを介してサービスにアクセスし、複数のインタラクティブ通信を生成できます。 また、必要に応じてカスタムサービスを作成することもできます。 次に示すメソッドを使用して、監視フォルダーでBatch APIを使用できます。

* インタラクティブ通信を生成するためのJSONファイル形式の入力データ（レコード）の指定
* 外部データソースに保存され、フォームデータモデルを介してアクセスされる入力データ（レコード）を使用して、インタラクティブ通信を作成する

#### JSONファイル形式の入力データレコードを指定して、インタラクティブ通信を生成します。{#specify-input-data-in-JSON-file-format}

レコードとインタラクティブ通信テンプレートを組み合わせて、インタラクティブ通信を作成できます。 各レコードに対して個別のJSONファイルを作成するか、JSON配列を作成してすべてのレコードを1つのファイルに保持できます。

JSONファイルに保存されたレコードからインタラクティブ通信を作成するには：

1. [監視フォルダー](https://docs.adobe.com/content/help/en/experience-manager-64/forms/publish-process-aem-forms/creating-configure-watched-folder.html)を作成し、バッチAPIを使用するように設定します。
   1. AEM Formsオーサーインスタンスにログインします。
   1. **[!UICONTROL ツール]** / **[!UICONTROL Forms]** / **[!UICONTROL 監視フォルダーの設定]**&#x200B;に移動します。 「**[!UICONTROL 新規]**」をタップします。
   1. フォルダーの&#x200B;**[!UICONTROL 名前]**&#x200B;と物理的な&#x200B;**[!UICONTROL パス]**&#x200B;を指定します。 （例：`c:\batchprocessing`）。
   1. 「**[!UICONTROL 次を使用してファイルを処理]**」フィールドで「**[!UICONTROL サービス]**」オプションを選択します。
   1. **[!UICONTROL 「サービス名]**」フィールドで、**[!UICONTROL com.adobe.fd.ccm.multichannel.batch.impl.service.InteractiveCommunicationBatchServiceImpl]**&#x200B;サービスを選択します。
   1. **[!UICONTROL 出力ファイルパターン]**&#x200B;を指定します。 例えば、%F/ [pattern](https://helpx.adobe.com/experience-manager/6-5/forms/using/admin-help/configuring-watched-folder-endpoints.html#about_file_patterns)は、監視フォルダーがWatched Folder\inputフォルダーのサブフォルダー内に入力ファイルを見つけることを指定します。
1. 詳細設定パラメーターの設定：
   1. 「**[!UICONTROL 詳細]**」タブを開き、次のカスタムプロパティを追加します。

      | プロパティ | 型 | 説明 |
      |--- |--- |--- |
      | templatePath | 文字列 | 使用するインタラクティブ通信テンプレートのパスを指定します。 例えば、 /content/dam/formsanddocuments/testsample/mediumicのように指定します。 これは必須プロパティです。 |
      | recordPath | 文字列 | recordPathフィールドの値は、インタラクティブ通信の名前を設定するのに役立ちます。 レコードのフィールドのパスは、 recordPathフィールドの値として設定できます。 例えば、 /employee/Idを指定した場合、idフィールドの値は、対応するインタラクティブ通信の名前になります。 デフォルト値は、ランダムな[ランダムなUUID](https://docs.oracle.com/javase/7/docs/api/java/util/UUID.html#randomUUID())です。 |
      | usePrefillService | ブール値 | 値をFalseに設定します。 usePrefillServiceパラメーターを使用すると、対応するインタラクティブ通信用に設定された事前入力サービスから取得したデータで、インタラクティブ通信を事前入力できます。 usePrefillServiceがtrueに設定されている場合、（レコードごとの）入力JSONデータはFDM引数として扱われます。 デフォルト値は false です。 |
      | batchType | 文字列 | 値をPRINT、WEB、またはWEB_AND_PRINTに設定します。 デフォルト値はWEB_AND_PRINTです。 |
      | locale | 文字列 | 出力インタラクティブ通信のロケールを指定します。 標準のサービスでは、ロケールオプションは使用されませんが、カスタムサービスを作成して、ローカライズされたインタラクティブ通信を生成することができます。 デフォルト値はen_USです。 |

   1. 「**[!UICONTROL 作成]**」をタップします。監視フォルダーが作成されます。
1. インタラクティブ通信を生成するには、監視フォルダーを使用します。
   1. 監視フォルダーを開きます。 入力フォルダーに移動します。
   1. 入力フォルダーにフォルダーを作成し、新しく作成したフォルダーにJSONファイルを配置します。
   1. 監視フォルダーがファイルを処理するのを待ちます。 処理が開始されると、入力ファイルと、そのファイルを含むサブフォルダーがステージングフォルダーに移動されます。
   1. outputフォルダーを開いて出力を表示します。
      * 「監視フォルダーの設定」でPRINTオプションを指定すると、インタラクティブ通信のPDF出力が生成されます。
      * 「監視フォルダーの設定」でWEBオプションを指定すると、レコードごとにJSONファイルが生成されます。 JSONファイルを使用して、Webテンプレート](#web-template)に事前に[入力できます。
      * PRINTオプションとWEBオプションの両方を指定すると、レコードごとにPDFドキュメントとJSONファイルの両方が生成されます。

#### 外部データソースに保存され、フォームデータモデルを介してアクセスされる入力データを使用して、インタラクティブ通信を作成します。{#use-fdm-as-data-source}

外部データソースに保存されたデータ（レコード）とインタラクティブ通信テンプレートを組み合わせて、インタラクティブ通信を作成できます。 インタラクティブ通信を作成する場合は、フォームデータモデル(FDM)を使用して外部データソースに接続し、データにアクセスします。 外部データソースから同じフォームデータモデルを使用してデータを取得するように、監視フォルダーバッチ処理サービスを設定できます。 [外部データソース](https://docs.adobe.com/content/help/en/experience-manager-64/forms/form-data-model/work-with-form-data-model.html)に保存されたレコードからインタラクティブ通信を作成するには、次の手順を実行します。

1. テンプレートのフォームデータモデルを設定します。
   1. インタラクティブ通信テンプレートに関連付けられたフォームデータモデルを開きます。
   1. トップレベルモデルオブジェクトを選択し、「プロパティを編集」をタップします。
   1. 「プロパティの編集」ペインの「読み取りサービス」フィールドから、取得サービスまたは取得サービスを選択します。
   1. 読み取りサービス引数の鉛筆アイコンをタップして、引数をリクエスト属性にバインドし、バインド値を指定します。 これにより、指定したバインド属性またはリテラル値にサービスの引数がバインドされ、それが引数としてサービスに渡され、指定した値に関連付けられている詳細情報がデータソースから取得されます。

      <br>
        この例では、 id引数はユーザープロファイルのid属性の値を取り、それを引数として読み取りサービスに渡します。指定したIDの従業員データモデルオブジェクトから、関連するプロパティの値を読み取り、返します。 したがって、フォームのidフィールドに00250と指定すると、読み取りサービスは従業員IDが00250の従業員の詳細を読み取ります。
        <br>

      ![リクエスト属性の設定](assets/request-attribute.png)

   1. プロパティとフォームデータモデルを保存します。
1. 要求属性の値の設定：
   1. .jsonファイルをファイルシステム上に作成し、編集用に開きます。
   1. JSON配列を作成し、フォームデータモデルからデータを取得するためのプライマリ属性を指定します。 例えば、次のJSONは、FDMに対し、idが27126または27127のレコードのデータを送信するよう要求します。

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

1. [監視フォルダー](https://docs.adobe.com/content/help/en/experience-manager-64/forms/publish-process-aem-forms/creating-configure-watched-folder.html)を作成し、Batch APIサービスを使用するように設定します。
   1. AEM Formsオーサーインスタンスにログインします。
   1. **[!UICONTROL ツール]** / **[!UICONTROL Forms]** / **[!UICONTROL 監視フォルダーの設定]**&#x200B;に移動します。 「**[!UICONTROL 新規]**」をタップします。
   1. フォルダーの&#x200B;**[!UICONTROL 名前]**&#x200B;と物理的な&#x200B;**[!UICONTROL パス]**&#x200B;を指定します。 （例：`c:\batchprocessing`）。
   1. 「**[!UICONTROL 次を使用してファイルを処理]**」フィールドで「**[!UICONTROL サービス]**」オプションを選択します。
   1. **[!UICONTROL 「サービス名]**」フィールドで、**[!UICONTROL com.adobe.fd.ccm.multichannel.batch.impl.service.InteractiveCommunicationBatchServiceImpl]**&#x200B;サービスを選択します。
   1. **[!UICONTROL 出力ファイルパターン]**&#x200B;を指定します。 例えば、%F/ [pattern](https://helpx.adobe.com/experience-manager/6-5/forms/using/admin-help/configuring-watched-folder-endpoints.html#about_file_patterns)は、監視フォルダーがWatched Folder\inputフォルダーのサブフォルダー内に入力ファイルを見つけることを指定します。
1. 詳細設定パラメーターの設定：
   1. 「**[!UICONTROL 詳細]**」タブを開き、次のカスタムプロパティを追加します。

      | プロパティ | 型 | 説明 |
      |--- |--- |--- |
      | templatePath | 文字列 | 使用するインタラクティブ通信テンプレートのパスを指定します。 例えば、 /content/dam/formsanddocuments/testsample/mediumicのように指定します。 これは必須プロパティです。 |
      | recordPath | 文字列 | recordPathフィールドの値は、インタラクティブ通信の名前を設定するのに役立ちます。 レコードのフィールドのパスは、 recordPathフィールドの値として設定できます。 例えば、 /employee/Idを指定した場合、idフィールドの値は、対応するインタラクティブ通信の名前になります。 デフォルト値は、ランダムな[ランダムなUUID](https://docs.oracle.com/javase/7/docs/api/java/util/UUID.html#randomUUID())です。 |  |
      | usePrefillService | ブール値 | 値をTrueに設定します。 デフォルト値は false です。値がtrueに設定されている場合、バッチAPIは設定されたフォームデータモデルからデータを読み取り、インタラクティブ通信に入力します。 usePrefillServiceがtrueに設定されている場合、（レコードごとの）入力JSONデータはFDM引数として扱われます。 |
      | batchType | 文字列 | 値をPRINT、WEB、またはWEB_AND_PRINTに設定します。 デフォルト値はWEB_AND_PRINTです。 |
      | locale | 文字列 | 出力インタラクティブ通信のロケールを指定します。 標準のサービスでは、ロケールオプションは使用されませんが、カスタムサービスを作成して、ローカライズされたインタラクティブ通信を生成することができます。 デフォルト値はen_USです。 |

   1. 「**[!UICONTROL 作成]**」をタップします。監視フォルダーが作成されます。
1. インタラクティブ通信を生成するには、監視フォルダーを使用します。
   1. 監視フォルダーを開きます。 入力フォルダーに移動します。
   1. 入力フォルダーにフォルダーを作成します。 手順2で作成したJSONファイルを、新しく作成したフォルダーに配置します。
   1. 監視フォルダーがファイルを処理するのを待ちます。 処理が開始されると、入力ファイルと、そのファイルを含むサブフォルダーがステージングフォルダーに移動されます。
   1. outputフォルダーを開いて出力を表示します。
      * 「監視フォルダーの設定」でPRINTオプションを指定すると、インタラクティブ通信のPDF出力が生成されます。
      * 「監視フォルダーの設定」でWEBオプションを指定すると、レコードごとにJSONファイルが生成されます。 JSONファイルを使用して、Webテンプレート](#web-template)に事前に[入力できます。
      * PRINTオプションとWEBオプションの両方を指定すると、レコードごとにPDFドキュメントとJSONファイルの両方が生成されます。

## RESTリクエストを使用したバッチAPIの呼び出し

Representational State Transfer(REST)リクエストを使用して、[Batch API](https://helpx.adobe.com/jp/experience-manager/6-5/forms/javadocs/index.html)を呼び出すことができます。 RESTエンドポイントを他のユーザーに提供してAPIにアクセスし、インタラクティブ通信を処理、保存およびカスタマイズするための独自のメソッドを設定できます。 独自のカスタムJavaサーブレットを開発して、AEMインスタンスにAPIをデプロイできます。

Javaサーブレットをデプロイする前に、インタラクティブ通信があり、対応するデータファイルが準備できていることを確認します。 次の手順を実行して、Javaサーブレットを作成およびデプロイします。

1. AEMインスタンスにログインし、インタラクティブ通信を作成します。 以下のサンプルコードに記載されているインタラクティブ通信を使用するには、[ここ](assets/SimpleMediumIC.zip)をクリックしてください。
1. [AEMインスタンス上でApache Mavenを使用してAEMプロジェ](https://helpx.adobe.com/experience-manager/using/maven_arch13.html) クトを構築し、デプロイします。
1. AEMプロジェクトのPOMファイルの依存関係リストに[AEM Forms Client SDKバージョン6.0.12](https://repo.adobe.com/nexus/content/repositories/public/com/adobe/aemfd/aemfd-client-sdk/)以降を追加します。 例：

   ```xml
       <dependency>
           <groupId>com.adobe.aemfd</groupId>
           <artifactId>aemfd-client-sdk</artifactId>
           <version>6.0.122</version>
       </dependency>
   ```

1. Javaプロジェクトを開き、.javaファイル（例：CCMBatchServlet.java）を作成します。 次のコードをファイルに追加しました。

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

1. 上記のコードで、テンプレートパス(setTemplatePath)をテンプレートのパスに置き換え、setBatchType APIの値を設定します。
   * PRINTオプションを指定すると、インタラクティブ通信のPDF出力が生成されます。
   * WEBオプションを指定すると、レコードごとにJSONファイルが生成されます。 JSONファイルを使用して、Webテンプレート](#web-template)に事前に[入力できます。
   * PRINTオプションとWEBオプションの両方を指定すると、レコードごとにPDFドキュメントとJSONファイルの両方が生成されます。

1. [Mavenを使用して、更新されたコードをAEMインスタンスにデプロイします](https://helpx.adobe.com/experience-manager/using/maven_arch13.html#BuildtheOSGibundleusingMaven)。
1. バッチAPIを呼び出して、インタラクティブ通信を生成します。 バッチAPIを印刷すると、レコード数に応じてPDFファイルと.jsonファイルのストリームが返されます。 JSONファイルを使用して、Webテンプレート](#web-template)に事前に[入力できます。 上記のコードを使用する場合、APIは`http://localhost:4502/bin/batchServlet`にデプロイされます。 このコードは、PDFとJSONファイルのストリームを印刷して返します。

### Webテンプレート{#web-template}の事前入力

batchTypeを設定してWebチャネルをレンダリングすると、APIはすべてのデータレコードに対してJSONファイルを生成します。 次の構文を使用して、JSONファイルを対応するWebチャネルとマージしてインタラクティブ通信を生成できます。

**構文**
`http://host:port/<template-path>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=<guide-merged-json-path>`

****
例：JSONファイルがにあり、次のイン `C:\batch\mergedJsonPath.json` タラクティブ通信テンプレートを使用する場合：  `http://host:port/content/dam/formsanddocuments/testsample/mediumic/jcr:content?channel=web`

次に、パブリッシュノード上の次のURLは、インタラクティブ通信のWebチャネルを表示します
`http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=file:///C:/batch/mergedJsonData.json`

ファイルシステムにデータを保存する以外に、JSONファイルをCRXリポジトリ、ファイルシステム、Webサーバーに保存するか、OSGI事前入力サービスを介してデータにアクセスできます。 様々なプロトコルを使用してデータを結合する構文は次のとおりです。

* **CRXプロトコル**

   `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=crx:///tmp/fd/af/mergedJsonData.json`

* **ファイルプロトコル**

   `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=file:///C:/Users/af/mergedJsonData.json`

* **事前入力サービスプロトコル**

   `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=service://[SERVICE_NAME]/[IDENTIFIER]`

   SERVICE_NAME は OSGI 事前入力サービスの名前を参照します。事前入力サービスの作成と実行を参照してください。

   IDENTIFIER は、事前入力データを取得するために OSGI 事前入力サービスが必要とするメタデータを参照します。ログイン済みユーザーの識別子は、使用できるメタデータの一例です。

* **HTTPプロトコル**

   `http://host:port/<path-to-ic>/jcr:content?channel=web&mode=preview&guideMergedJsonPath=http://localhost:8000/somesamplexmlfile.xml`

>[!NOTE]
>
>デフォルトでは、CRXプロトコルのみが有効になっています。 その他のサポートされているプロトコルを有効にするには、「[Configuration Managerを使用した事前入力サービスの設定](https://helpx.adobe.com/experience-manager/6-5/forms/using/prepopulate-adaptive-form-fields.html#ConfiguringprefillserviceusingConfigurationManager)」を参照してください。
