---
title: エージェント UI を使用してインタラクティブ通信の準備と送信を行う
seo-title: エージェント UI を使用してインタラクティブ通信の準備と送信を行う
description: エージェント UI を使用してインタラクティブ通信の準備を行い、後処理用として送信することができます。エージェントは、許可設定に基づいて必要な変更を行い、電子メールの送信や印刷出力などの後処理用としてインタラクティブ通信を送信します。
seo-description: エージェント UI を使用してインタラクティブ通信の準備と送信を行う
uuid: d1a19b83-f630-4648-9ad2-a22374e31aa9
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 110c86ea-9bd8-4018-bfcc-ca33e6b3f3ba
feature: インタラクティブコミュニケーション
exl-id: 4fb82e9b-f870-47db-ac92-2d7510acace8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2062'
ht-degree: 34%

---

# エージェント UI を使用してインタラクティブ通信の準備と送信を行う {#prepare-and-send-interactive-communication-using-the-agent-ui}

エージェント UI を使用してインタラクティブ通信の準備を行い、後処理用として送信することができます。エージェントは、許可設定に基づいて必要な変更を行い、電子メールの送信や印刷出力などの後処理用としてインタラクティブ通信を送信します。

## 概要 {#overview}

インタラクティブ通信を作成した後、エージェントは、エージェントUIでインタラクティブ通信を開き、データを入力し、コンテンツと添付ファイルを管理することで、受信者固有のコピーを準備できます。 最後に、エージェントはインタラクティブ通信を後処理に送信できます。

エージェントUIを使用してインタラクティブ通信を準備する際、エージェントは後処理に送信する前に、エージェントUIでインタラクティブ通信の次の側面を管理します。

* **データ**：エージェント UI の「データ」タブには、インタラクティブ通信内の変数とロックが解除されたフォームデータモデルプロパティが表示されます（エージェントを使用して編集できる変数とフォームデータモデルプロパティ）。これらの変数とプロパティは、インタラクティブ通信内のドキュメントフラグメントの編集時または作成時に生成されます。「データ」タブには、XDP テンプレートまたは印刷チャネルテンプレートに組み込まれているフィールドも表示されます。「データ」タブは、エージェントが編集可能な変数、フォームデータモデルのプロパティ、またはフィールドがインタラクティブ通信に存在する場合にのみ表示されます。
* **コンテンツ**：エージェントにより、「コンテンツ」タブに表示される各種コンテンツ（インタラクティブ通信内のドキュメントフラグメントやコンテンツ変数など）が管理されます。エージェントは、ドキュメントフラグメントのプロパティでインタラクティブ通信を作成する際に、許可されたとおりにドキュメントフラグメントに変更を加えることができます。 エージェントは、許可されている場合、ドキュメントフラグメントの並べ替え、追加/削除、改ページの追加も行えます。
* **添付ファイル**:「添付ファイル」タブは、インタラクティブ通信に添付ファイルがある場合、またはエージェントがライブラリにアクセスできる場合にのみ、エージェントUIに表示されます。エージェントは、添付ファイルの変更や編集を許可される場合とできない場合があります。

## エージェントUIを使用してインタラクティブ通信を準備する{#prepare-interactive-communication-using-the-agent-ui}

1. **[!UICONTROL フォーム]**／**[!UICONTROL フォームとドキュメント]**&#x200B;を選択します。
1. 適切なインタラクティブ通信を選択し、**[!UICONTROL エージェントUIを開く]**&#x200B;をタップします。

   >[!NOTE]
   >
   >エージェントUIは、選択したインタラクティブ通信に印刷チャネルがある場合にのみ機能します。

   ![openagentui](assets/openagentiui.png)

   インタラクティブ通信のコンテンツとプロパティに基づいて、エージェント UI に、「データ」タブ、「コンテンツ」タブ、「添付ファイル」タブという 3 つのタブが表示されます。

   ![無代性](assets/agentuitabs.png)

   次に、データの入力、コンテンツの管理、添付ファイルの管理を行います。

### データの入力 {#enter-data}

1. 「データ」タブで、変数のデータ、フォームデータモデルのプロパティ、印刷テンプレート（XDP）のフィールドを、必要に応じて入力します。アスタリスク(&amp;ast;)が付いた必須フィールドをすべて入力し、「**送信**」ボタンを有効にします。

   インタラクティブ通信のプレビューでデータフィールドの値をタップして、「データ」タブで対応するデータフィールドをハイライト表示するか、その逆を実行します。

### コンテンツを管理 {#manage-content}

「コンテンツ」タブで、インタラクティブ通信内のドキュメントフラグメントやコンテンツ変数などのコンテンツを管理します。

1. 「**[!UICONTROL コンテンツ]**」を選択します。インタラクティブ通信の「コンテンツ」タブが表示されます。

   ![agentuicontenttab](assets/agentuicontenttab.png)

1. 必要に応じて、「コンテンツ」タブでドキュメントフラグメントを編集します。コンテンツ階層内の関連するフラグメントにフォーカスを移すには、インタラクティブ通信プレビューで関連する行または段落をタップするか、コンテンツ階層で直接フラグメントをタップします。

   例えば、以下のプレビュー画面で、「Make a payment online now ...」という行が含まれているドキュメントフラグメントを選択すると、「コンテンツ」タブでも同じドキュメントフラグメントが選択されます。

   ![contentmodulefocus](assets/contentmodulefocus.png)

   「コンテンツ」タブまたは「データ」タブで、プレビューの左上にある「コンテンツ内の選択済みモジュールをハイライト表示」(![highlightselectedmodulesincontentccr](assets/highlightselectedmodulesincontentccr.png))をタップして、プレビューで関連するテキスト、段落またはデータフィールドをタップ/選択したときにドキュメントフラグメントに移動する機能を無効または有効にします。

   インタラクティブ通信の作成時にエージェントが編集できるフラグメントには、「選択したコンテンツを編集」(![iconeditselectedcontent](assets/iconeditselectedcontent.png))アイコンが表示されます。 このアイコンをタップすると、フラグメントが編集モードで表示され、フラグメントを編集できるようになります。テキストの書式設定と管理を行うには、以下のオプションを使用します。

   * [書式設定オプション](#formattingtext)

      * [書式設定されたテキストを他のアプリケーションからコピーして貼り付け](#pasteformattedtext)
      * [テキストの一部をハイライト表示](#highlightemphasize)
   * [特殊文字](#specialcharacters)
   * [ショートカットキー](/help/forms/using/keyboard-shortcuts.md)

   エージェントユーザーインターフェイスの様々なドキュメントフラグメントで使用できるアクションの詳細については、「[エージェントユーザーインターフェイスで使用できるアクションと情報](#actionsagentui)」を参照してください。

1. インタラクティブ通信の印刷出力に改ページを追加するには、改ページを挿入する位置にカーソルを置き、「前の改ページ」または「後の改ページ」(![pagebreakbeforeafter](assets/pagebreakbeforeafter.png))を選択します。

   インタラクティブ通信に、改ページのプレースホルダーが明示的に挿入されます。この明示的な改ページによってインタラクティブ通信の外観がどのように変わるのかを確認するには、印刷出力をプレビュー表示します。

   ![explicitpagebreak](assets/explicitpagebreak.png)

   次に、インタラクティブ通信の添付ファイルの管理を行います。

### 添付ファイルの管理  {#manage-attachments}

1. **[!UICONTROL 添付ファイル]**&#x200B;を選択します。 エージェントUIには、インタラクティブ通信の作成時に設定された添付ファイルが表示されます。

   表示アイコンをタップして、インタラクティブ通信と一緒に添付ファイルを送信しないように選択し、添付ファイルのバツ印をタップして（エージェントが添付ファイルを削除または非表示にできる場合）、インタラクティブ通信から添付ファイルを削除できます。 インタラクティブ通信の作成時に必須ファイルとして指定された添付ファイルの場合、ビューアイコンと削除アイコンは無効になります。

   ![attachmentsagentui](assets/attachmentsagentui.png)

1. ライブラリアクセス（![ライブラリアクセス](assets/libraryaccess.png)）アイコンをタップしてコンテンツライブラリにアクセスし、添付ファイルとしてDAMアセットを挿入します。

   >[!NOTE]
   >
   >ライブラリアクセスアイコンは、（印刷チャネルのDocument Containerプロパティで）インタラクティブ通信の作成時にライブラリアクセスが有効になっている場合にのみ使用できます。

1. インタラクティブ通信の作成時に、添付ファイルの順序をロックしなかった場合は、添付ファイルを選択して上下の矢印をタップすると、添付ファイルの順序を変更することができます。
1. Web プレビューと印刷プレビューを使用して、2 つの出力が正しく作成されているかどうかを確認します。

   プレビューが十分な場合は、「**[!UICONTROL 送信]**」をタップして、インタラクティブ通信を後処理に送信または送信します。 または、変更を行うには、プレビューを終了して、変更を行う場所に戻ります。

## テキストの書式設定 {#formattingtext}

エージェント UI でテキストフラグメントを編集する場合、編集のタイプ（フォント、段落、リスト）に応じて、表示されるツールバーが異なります。

![](assets/typeofformattingtoolbar.png) ![typeofformattingtoolbarFontツールバー](do-not-localize/fonttoolbar.png)

フォントツールバー

![段落ツールバー](do-not-localize/paragraphtoolbar.png)

段落ツールバー

![リストツールバー](do-not-localize/listtoolbar.png)

リストツールバー

### テキストの一部をハイライト表示または強調表示する {#highlightemphasize}

編集可能なフラグメント内のテキストの一部をハイライト表示または強調表示するには、目的のテキストを選択して「ハイライト表示の色」をタップします。

![highlighttextagentui](assets/highlighttextagentui.png)

### 書式設定されたテキストの貼り付け {#pasteformattedtext}

![pastedtext](assets/pastedtext.png)

### テキスト内に特殊文字を挿入する {#specialcharacters}

エージェント UI では、210 個の特殊文字がサポートされています。管理者は、カスタマイズ](/help/forms/using/custom-special-characters.md)により、追加/カスタム特殊文字のサポートを[追加できます。

#### 添付ファイルの配信 {#attachmentdelivery}

* サーバー側のAPIを使用してインタラクティブ通信がインタラクティブPDFまたは非インタラクティブPDFとしてレンダリングされると、レンダリングされたPDFには添付ファイルがPDF添付ファイルとして含まれます。
* インタラクティブ通信に関連付けられた後処理がエージェントUIを使用して送信の一部として読み込まれると、添付ファイルはList&lt;com.adobe.idp.Document> inAttachmentDocsパラメーターとして渡されます。
* 配信メカニズムワークフロー（電子メールや印刷出力など）により、PDF 版のインタラクティブ通信と共に添付ファイルも配信されます。

## エージェント UI で使用できる操作と情報 {#actionsagentui}

### ドキュメントフラグメント {#document-fragments}

![](do-not-localize/contentoptionsdocfragments.png)

* **上矢印と下矢印**：上矢印と下矢印を使用して、インタラクティブ通信内のドキュメントフラグメントを上下に移動することができます。
* **削除**:可能な場合は、インタラクティブ通信からドキュメントフラグメントを削除します。
* **直前に改ページ**：（ターゲット領域の子フラグメントで使用可能）ドキュメントフラグメントの直前に改ページが挿入されます。
* **インデント**:ドキュメントフラグメントのインデントを増減します。
* **直後に改ページ** （ターゲット領域の子フラグメントに適用可能）:ドキュメントフラグメントの後に改ページを挿入します。

![docfragoptions](assets/docfragoptions.png)

* 編集：（テキストフラグメントの場合のみ）テキストドキュメントフラグメントを編集するためのリッチテキストエディターが起動します。詳しくは、[テキストのフォーマット](#formattingtext)を参照してください。

* 選択（目のアイコン）：インタラクティブ通信にドキュメントフラグメントを含めたり、インタラクティブ通信からドキュメントフラグメントを除外したりすることができます。
* 未入力値：ターゲット領域の未入力変数の数が表示されます。これは、表示専用情報です。

### リストドキュメントフラグメント  {#list-document-fragments}

![listoptions](assets/listoptions.png)

* 空白行を挿入： 空白行を挿入します。
* 選択（目のアイコン）：インタラクティブ通信にドキュメントフラグメントを含めたり、インタラクティブ通信からドキュメントフラグメントを除外したりすることができます。
* 箇条書き／番号付けをスキップ：リストドキュメントフラグ内で、箇条書きまたは番号付けをスキップすることができます。
* 未入力値：ターゲット領域の未入力変数の数が表示されます。これは、表示専用情報です。

## インタラクティブ通信を下書きとして保存{#save-as-draft}

エージェントUIを使用して、各インタラクティブ通信の1つ以上のドラフトを保存し、後でドラフトを取得して作業を続行できます。 ドラフトごとに異なる名前を指定して識別できます。

Adobeは、インタラクティブ通信をドラフトとして正常に保存するために、これらの手順を順に実行することをお勧めします。

### 「ドラフトとして保存」機能{#before-save-as-draft}を有効にします。

「ドラフトとして保存」機能は、デフォルトでは有効になっていません。 この機能を有効にするには、次の手順を実行します。

1. [ccrDocumentInstance](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/fd/ccm/ccr/ccrDocumentInstance/api/services/CCRDocumentInstanceService.html)サービスプロバイダーインターフェイス(SPI)を実装します。

   SPIを使用すると、インタラクティブ通信の下書きバージョンを、下書きIDを一意の識別子として使用してデータベースに保存できます。 これらの手順は、Mavenプロジェクトを使用してOSGiバンドルを構築する方法に関する事前の知識があることを前提としています。

   SPIの実装例については、[サンプルccrDocumentInstance SPIの実装](#sample-ccrDocumentInstance-spi)を参照してください。
1. `http://<hostname>:<port>/ system/console/bundles`を開き、**[!UICONTROL Install/Update]**&#x200B;をタップしてOSGiバンドルをアップロードします。 アップロードしたパッケージのステータスが「**アクティブ**」と表示されることを確認します。 パッケージのステータスが「**アクティブ**」と表示されない場合は、サーバーを再起動します。
1. `https://'[server]:[port]'/system/console/configMgr` にアクセスします。
1. 「**[!UICONTROL 通信設定を作成]**」をタップします。
1. 「**[!UICONTROL CCRDocumentInstanceServiceを使用して保存を有効にする]**」を選択して「**[!UICONTROL 保存]**」をタップします。

### インタラクティブ通信を下書きとして保存{#save-as-draft-agent-ui}

次の手順を実行して、インタラクティブ通信を下書きとして保存します。

1. Forms Managerでインタラクティブ通信を選択し、**[!UICONTROL エージェントUIを開く]**&#x200B;をタップします。

1. エージェントUIで適切な変更を行い、「**[!UICONTROL ドラフトとして保存]**」をタップします。

1. 「**[!UICONTROL 名前]**」フィールドにドラフトの名前を指定し、「**[!UICONTROL 完了]**」をタップします。

インタラクティブ通信を下書きとして保存したら、「**[!UICONTROL 変更を保存]**」をタップして、下書きに対する変更を保存します。

### インタラクティブ通信の下書きを取得する{#retrieve-draft}

インタラクティブ通信を下書きとして保存した後、引き続き作業を行うために取得できます。 次を使用してインタラクティブ通信を取得します。

`https://server:port/aem/forms/createcorrespondence.hmtl?draftid=[draftid]`

[] draftidrefersは、インタラクティブ通信をドラフトとして保存した後に生成されるドラフトバージョンの一意の識別子を指定します。

>[!NOTE]
>
>下書きとして保存した後にインタラクティブ通信に変更を加えた場合、下書きバージョンは開けません。

### ccrDocumentInstance SPI実装の例{#sample-ccrDocumentInstance-spi}

`ccrDocumentInstance` SPIを実装して、インタラクティブ通信を下書きとして保存します。 以下は、`ccrDocumentInstance` SPIの実装例です。

```javascript
package Implementation;

import com.adobe.fd.ccm.ccr.ccrDocumentInstance.api.exception.CCRDocumentException;
import com.adobe.fd.ccm.ccr.ccrDocumentInstance.api.model.CCRDocumentInstance;
import com.adobe.fd.ccm.ccr.ccrDocumentInstance.api.services.CCRDocumentInstanceService;
import org.apache.commons.lang3.StringUtils;
import org.osgi.service.component.annotations.Component;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import java.util.*;


@Component(service = CCRDocumentInstanceService.class, immediate = true)
public class CCRDraftService implements CCRDocumentInstanceService {

    private static final Logger logger = LoggerFactory.getLogger(CCRDraftService.class);

    private HashMap<String, Object> draftDataMap = new HashMap<>();

    @Override
    public String save(CCRDocumentInstance ccrDocumentInstance) throws CCRDocumentException {
        String documentInstanceName = ccrDocumentInstance.getName();
        if (StringUtils.isNotEmpty(documentInstanceName)) {
            logger.info("Saving ccrData with name : {}", ccrDocumentInstance.getName());
            if (!CCRDocumentInstance.Status.SUBMIT.equals(ccrDocumentInstance.getStatus())) {
                ccrDocumentInstance = mySQLDataBaseServiceCRUD(ccrDocumentInstance,null, "SAVE");
            }
        } else {
            logger.error("Could not save data as draft name is empty");
        }
        return ccrDocumentInstance.getId();
    }

    @Override
    public void update(CCRDocumentInstance ccrDocumentInstance) throws CCRDocumentException {
        String documentInstanceName = ccrDocumentInstance.getName();
        if (StringUtils.isNotEmpty(documentInstanceName)) {
            logger.info("Saving ccrData with name : {}", documentInstanceName);
            mySQLDataBaseServiceCRUD(ccrDocumentInstance, ccrDocumentInstance.getId(), "UPDATE");
        } else {
            logger.error("Could not save data as draft Name is empty");
        }
    }

    @Override
    public CCRDocumentInstance get(String id) throws CCRDocumentException {
        CCRDocumentInstance cCRDocumentInstance;
        if (StringUtils.isEmpty(id)) {
            logger.error("Could not retrieve data as draftId is empty");
            cCRDocumentInstance = null;
        } else {
            cCRDocumentInstance = mySQLDataBaseServiceCRUD(null, id,"GET");
        }
        return cCRDocumentInstance;
    }

    @Override
    public List<CCRDocumentInstance> getAll(String userId, Date creationTime, Date updateTime,
                                            Map<String, Object> optionsParams) throws CCRDocumentException {
        List<CCRDocumentInstance> ccrDocumentInstancesList = new ArrayList<>();

        HashMap<String, Object> allSavedDraft = mySQLGetALLData();
        for (String key : allSavedDraft.keySet()) {
            ccrDocumentInstancesList.add((CCRDocumentInstance) allSavedDraft.get(key));
        }
        return ccrDocumentInstancesList;
    }

    //The APIs call the service in the database using the following section.
    private CCRDocumentInstance mySQLDataBaseServiceCRUD(CCRDocumentInstance ccrDocumentInstance,String draftId, String method){
        if(method.equals("SAVE")){

            String autoGenerateId = draftDataMap.size() + 1 +"";
            ccrDocumentInstance.setId(autoGenerateId);
            draftDataMap.put(autoGenerateId, ccrDocumentInstance);
            return ccrDocumentInstance;

        }else if (method.equals("UPDATE")){

            draftDataMap.put(ccrDocumentInstance.getId(), ccrDocumentInstance);
            return ccrDocumentInstance;

        }else if(method.equals("GET")){

            return (CCRDocumentInstance) draftDataMap.get(draftId);

        }
        return null;
    }

    private HashMap<String, Object> mySQLGetALLData(){
        return draftDataMap;
    }
}
```

`save`、`update`、`get`および`getAll`操作は、データベースサービスを呼び出し、インタラクティブ通信を下書きとして保存し、インタラクティブ通信を更新し、データベースからデータを取得し、データベースで使用可能なすべてのインタラクティブ通信のデータを取得します。 このサンプルでは、データベースサービスの名前として`mySQLDataBaseServiceCRUD`を使用しています。

次の表は、SPIのサンプル`ccrDocumentInstance`の実装を示しています。 この例は、 `save` 、 `update` 、 `get`および`getAll`操作が、サンプル実装でデータベースサービスを呼び出す方法を示しています。

<table> 
 <tbody>
 <tr>
  <td><p><strong>操作</strong></p></td>
  <td><p><strong>データベースサービスの例</strong></p></td> 
   </tr>
  <tr>
   <td><p>インタラクティブ通信の下書きを作成するか、直接送信することができます。 保存操作用のAPIは、インタラクティブ通信がドラフトとして送信され、ドラフト名が含まれているかどうかを確認します。 次に、APIは、Saveを入力メソッドとしてmySQLDataBaseServiceCRUDサービスを呼び出します。</p></br><img src="assets/save-as-draft-save-operation.png"/></br>[#$sd1_sf1_dp9]</td>
   <td><p>mySQLDataBaseServiceCRUDサービスは、 Saveを入力メソッドとして検証し、自動生成されたドラフトIDを生成してAEMに返します。 ドラフトIDを生成するロジックは、データベースによって異なる場合があります。</p></br><img src="assets/save-operation-service.png"/></br>[#$sd1_sf1_dp13]</td>
   </tr>
  <tr>
   <td><p>更新操作のAPIは、インタラクティブ通信のドラフトの状態を取得し、インタラクティブ通信にドラフト名が含まれているかどうかを確認します。 APIはmySQLDataBaseServiceCRUDサービスを呼び出して、データベース内のその状態を更新します。</p></br><img src="assets/save-as-draft-update-operation.png"/></br>[#$sd1_sf1_dp17]</td>
   <td><p>mySQLDataBaseServiceCRUDサービスは、Updateを入力メソッドとして検証し、インタラクティブ通信の下書きの状態をデータベースに保存します。</br></p><img src="assets/update-operation-service.png"/></td>
   </tr>
   <tr>
   <td><p>get操作用のAPIは、インタラクティブ通信にドラフトIDが含まれているかどうかを確認します。 次に、APIは、Getを入力メソッドとしてmySQLDataBaseServiceCRUDサービスを呼び出し、インタラクティブ通信のデータを取得します。</br></p><img src="assets/save-as-draft-get-operation.png"/></td>
   <td><p>mySQLDataBaseServiceCRUDサービスは、Getを入力メソッドとして検証し、ドラフトIDに基づいてインタラクティブ通信のデータを取得します。</p></br><img src="assets/get-operation-service.png"/></br>[#$sd1_sf1_dp29]</td>
   </tr>
   <tr>
   <td><p>getAll操作のAPIは、mySQLGetALLDataサービスを呼び出して、データベースに保存されているすべてのインタラクティブ通信のデータを取得します。</br></p><img src="assets/save-as-draft-getall-operation.png"/></td>
   <td><p>mySQLGetALLDataサービスは、データベースに保存されているすべてのインタラクティブ通信のデータを取得します。</p></br><img src="assets/getall-operation-service.png"/></br>[#$sd1_sf1_dp37]</td>
   </tr>
  </tbody>
</table>

次に、実装に含まれる`pom.xml`ファイルの例を示します。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.adobe.livecycle</groupId>
    <artifactId>draft-sample</artifactId>
    <version>2.0.0-SNAPSHOT</version>

    <name>Interact</name>
    <packaging>bundle</packaging>

    <dependencies>
        <dependency>
            <groupId>com.adobe.aemfd</groupId>
            <artifactId>aemfd-client-sdk</artifactId>
            <version>6.0.160</version>
        </dependency>
    </dependencies>


    <!-- ====================================================================== -->
    <!-- B U I L D D E F I N I T I O N -->
    <!-- ====================================================================== -->
    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.felix</groupId>
                <artifactId>maven-bundle-plugin</artifactId>
                <version>3.3.0</version>
                <extensions>true</extensions>
                <executions>
                    <!--Configure extra execution of 'manifest' in process-classes phase to make sure SCR metadata is generated before unit test runs-->
                    <execution>
                        <id>scr-metadata</id>
                        <goals>
                            <goal>manifest</goal>
                        </goals>
                    </execution>
                </executions>
                <configuration>
                    <exportScr>true</exportScr>
                    <instructions>
                        <!-- Enable processing of OSGI DS component annotations -->
                        <_dsannotations>*</_dsannotations>
                        <!-- Enable processing of OSGI metatype annotations -->
                        <_metatypeannotations>*</_metatypeannotations>
                        <Bundle-SymbolicName>${project.groupId}-${project.artifactId}</Bundle-SymbolicName>
                    </instructions>
                </configuration>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-surefire-plugin</artifactId>
            </plugin>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <configuration>
                    <source>8</source>
                    <target>8</target>
                </configuration>
            </plugin>
        </plugins>
    </build>
    <profiles>
        <profile>
            <id>autoInstall</id>
            <build>
                <plugins>
                    <plugin>
                        <groupId>org.apache.sling</groupId>
                        <artifactId>maven-sling-plugin</artifactId>
                        <executions>
                            <execution>
                                <id>install-bundle</id>
                                <phase>install</phase>
                                <goals>
                                    <goal>install</goal>
                                </goals>
                            </execution>
                        </executions>
                    </plugin>
                </plugins>
            </build>
        </profile>
    </profiles>

</project>
```

>[!NOTE]
>
>`pom.xml`ファイルの`aemfd-client-sdk`依存関係を6.0.160に更新してください。
