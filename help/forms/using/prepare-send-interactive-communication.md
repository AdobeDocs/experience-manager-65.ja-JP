---
title: エージェント UI を使用してインタラクティブ通信の準備と送信を行う
seo-title: エージェント UI を使用してインタラクティブ通信の準備と送信を行う
description: エージェント UI を使用してインタラクティブ通信の準備を行い、後処理用として送信することができます。エージェントは、許可設定に基づいて必要な変更を行い、電子メールの送信や印刷出力などの後処理用としてインタラクティブ通信を送信します。
seo-description: エージェント UI を使用してインタラクティブ通信の準備と送信を行う
uuid: d1a19b83-f630-4648-9ad2-a22374e31aa9
topic-tags: interactive-communications
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 110c86ea-9bd8-4018-bfcc-ca33e6b3f3ba
translation-type: tm+mt
source-git-commit: 06335b9a85414b6b1141dd19c863dfaad0812503

---


# エージェント UI を使用してインタラクティブ通信の準備と送信を行う {#prepare-and-send-interactive-communication-using-the-agent-ui}

エージェント UI を使用してインタラクティブ通信の準備を行い、後処理用として送信することができます。エージェントは、許可設定に基づいて必要な変更を行い、電子メールの送信や印刷出力などの後処理用としてインタラクティブ通信を送信します。

## 概要 {#overview}

インタラクティブ通信を作成した後、エージェントはエージェントUIでインタラクティブ通信を開き、データを入力し、コンテンツと添付ファイルを管理することで、受信者に固有のコピーを作成できます。 最後に、エージェントは後処理に対してインタラクティブ通信を送信できます。

エージェントUIを使用して対話型通信を準備する際、エージェントは、後処理に送信する前に、エージェントUIで対話型通信の次の側面を管理します。

* **データ**：エージェント UI の「データ」タブには、インタラクティブ通信内の変数とロックが解除されたフォームデータモデルプロパティが表示されます（エージェントを使用して編集できる変数とフォームデータモデルプロパティ）。これらの変数とプロパティは、インタラクティブ通信内のドキュメントフラグメントの編集時または作成時に生成されます。「データ」タブには、XDP テンプレートまたは印刷チャネルテンプレートに組み込まれているフィールドも表示されます。「データ」タブは、エージェントが編集可能な変数、フォームデータモデルのプロパティ、またはインタラクティブ通信内のフィールドがある場合にのみ表示されます。
* **コンテンツ**：エージェントにより、「コンテンツ」タブに表示される各種コンテンツ（インタラクティブ通信内のドキュメントフラグメントやコンテンツ変数など）が管理されます。エージェントは、ドキュメントフラグメントのプロパティでインタラクティブ通信を作成する際に、許可されているとおりにドキュメントフラグメントに変更を加えることができます。 エージェントでは、許可されている場合、ドキュメントフラグメントの順序の変更、追加/削除、改ページの追加を行うこともできます。
* **Attachments**:[添付ファイル]タブは、Interactive Communicationに添付ファイルがある場合、またはエージェントがライブラリにアクセスできる場合にのみ、エージェントUIに表示されます。 エージェントは添付ファイルの変更や編集を許可される場合とできない場合があります。

## Prepare Interactive Communication using the Agent UI {#prepare-interactive-communication-using-the-agent-ui}

1. **[!UICONTROL フォーム]**／**[!UICONTROL フォームとドキュメント]**&#x200B;を選択します。
1. Select the appropriate Interactive Communication and tap **[!UICONTROL Open Agent UI]**.

   >[!NOTE]
   >
   >エージェントUIは、選択したインタラクティブ通信に印刷チャネルがある場合にのみ機能します。

   ![openagentiui](assets/openagentiui.png)

   インタラクティブ通信のコンテンツとプロパティに基づいて、エージェント UI に、「データ」タブ、「コンテンツ」タブ、「添付ファイル」タブという 3 つのタブが表示されます。

   ![無代性](assets/agentuitabs.png)

   次に、データの入力、コンテンツの管理、添付ファイルの管理を行います。

### データの入力 {#enter-data}

1. 「データ」タブで、変数のデータ、フォームデータモデルのプロパティ、印刷テンプレート（XDP）のフィールドを、必要に応じて入力します。Fill up all the mandatory fields marked with an asterisk (&amp;ast;) to enable the **Submit** button.

   インタラクティブ通信プレビューでデータフィールドの値をタップして、「データ」タブで対応するデータフィールドをハイライト表示するか、逆の場合も同様に表示します。

### コンテンツを管理 {#manage-content}

「コンテンツ」タブで、インタラクティブ通信内のドキュメントフラグメントやコンテンツ変数などのコンテンツを管理します。

1. 「**[!UICONTROL コンテンツ]**」を選択します。[インタラクティブコミュニケーション]の[コンテンツ]タブが表示されます。

   ![agentuicontenttab](assets/agentuicontenttab.png)

1. 必要に応じて、「コンテンツ」タブでドキュメントフラグメントを編集します。コンテンツ階層の関連するフラグメントにフォーカスするには、インタラクティブ通信プレビューで関連する行または段落をタップするか、コンテンツ階層で直接フラグメントをタップします。

   例えば、以下のプレビュー画面で、「Make a payment online now ...」という行が含まれているドキュメントフラグメントを選択すると、「コンテンツ」タブでも同じドキュメントフラグメントが選択されます。

   ![contentmodulefocus](assets/contentmodulefocus.png)

   In the Content or Data tab, by tapping Highlight Selected Modules In Content ( ![highlightselectedmodulesincontentccr](assets/highlightselectedmodulesincontentccr.png)) on upper left of the preview, you can disable or enable functionality to go to the document fragment when the relevant text, paragraph, or data field is tapped/selected in the preview.

   The fragments that are allowed to be edited by the agent while creating the Interactive Communication have the Edit Selected Content ( ![iconeditselectedcontent](assets/iconeditselectedcontent.png)) icon. このアイコンをタップすると、フラグメントが編集モードで表示され、フラグメントを編集できるようになります。テキストの書式設定と管理を行うには、以下のオプションを使用します。

   * [書式設定オプション](#formattingtext)

      * [書式設定されたテキストを他のアプリケーションからコピーして貼り付け](#pasteformattedtext)
      * [テキストの一部をハイライト表示](#highlightemphasize)
   * [特殊文字](#specialcharacters)
   * [ショートカットキー](/help/forms/using/keyboard-shortcuts.md)
   For more information on the actions available for various document fragments in the Agent user interface, see [Actions and info available in the Agent user interface](#actionsagentui).

1. To add a page break to the print output of the Interactive Communication, place the cursor where you want to insert a page break and select Page Break Before or Page Break After ( ![pagebreakbeforeafter](assets/pagebreakbeforeafter.png)).

   インタラクティブ通信に、改ページのプレースホルダーが明示的に挿入されます。この明示的な改ページによってインタラクティブ通信の外観がどのように変わるのかを確認するには、印刷出力をプレビュー表示します。

   ![explicitpagebreak](assets/explicitpagebreak.png)

   次に、インタラクティブ通信の添付ファイルの管理を行います。

### 添付ファイルの管理 {#manage-attachments}

1. Select **[!UICONTROL Attachment]**. エージェントUIには、インタラクティブ通信の作成時に設定したとおりに、利用可能な添付ファイルが表示されます。

   表示アイコンをタップして、添付ファイルをインタラクティブ通信と共に送信しないように選択し、添付ファイルの×印をタップして（エージェントが添付ファイルを削除または非表示にできる場合）、Interactive Communicationから添付ファイルを削除できます。 インタラクティブ通信の作成時に必須ファイルとして指定された添付ファイルの場合、ビューアイコンと削除アイコンは無効になります。

   ![attachmentsagentuis](assets/attachmentsagentui.png)

1. Tap the Library Access ( ![libraryaccess](assets/libraryaccess.png)) icon to access Content Library to insert DAM assets as attachments.

   >[!NOTE]
   >
   >ライブラリアクセスアイコンは、（印刷チャネルのDocument Containerプロパティで）インタラクティブ通信の作成中にライブラリアクセスが有効になっている場合にのみ使用できます。

1. インタラクティブ通信の作成時に、添付ファイルの順序をロックしなかった場合は、添付ファイルを選択して上下の矢印をタップすると、添付ファイルの順序を変更することができます。
1. Web プレビューと印刷プレビューを使用して、2 つの出力が正しく作成されているかどうかを確認します。

   If you find the previews to be satisfactory, tap **[!UICONTROL Submit]** to submit/send the Interactive Communication to a post process. または、変更を行うには、プレビューを終了して、変更を行う場所に戻ります。

## テキストの書式設定 {#formattingtext}

エージェント UI でテキストフラグメントを編集する場合、編集のタイプ（フォント、段落、リスト）に応じて、表示されるツールバーが異なります。

![typeofformattingtoolbarフォント](assets/typeofformattingtoolbar.png)![ツールバー](do-not-localize/fonttoolbar.png)

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

エージェント UI では、210 個の特殊文字がサポートされています。The admin can [add support for more/custom special characters by customization](/help/forms/using/custom-special-characters.md).

#### 添付ファイルの配信 {#attachmentdelivery}

* サーバー側APIを使用してインタラクティブPDFまたは非インタラクティブPDFとしてインタラクティブ通信がレンダリングされる場合、レンダリングされるPDFには添付ファイルがPDF添付ファイルとして含まれます。
* インタラクティブ通信に関連付けられた後処理がエージェントUIを使用して送信の一部として読み込まれると、添付ファイルはList&lt;com.adobe.idp.Document> inAttachmentDocsパラメーターとして渡されます。
* 配信メカニズムワークフロー（電子メールや印刷出力など）により、PDF 版のインタラクティブ通信と共に添付ファイルも配信されます。

## エージェント UI で使用できる操作と情報 {#actionsagentui}

### ドキュメントフラグメント {#document-fragments}

![](do-not-localize/contentoptionsdocfragments.png)

* **上矢印と下矢印**：上矢印と下矢印を使用して、インタラクティブ通信内のドキュメントフラグメントを上下に移動することができます。
* **削除**:許可されている場合は、ドキュメントフラグメントをインタラクティブ通信から削除します。
* **直前に改ページ**：（ターゲット領域の子フラグメントで使用可能）ドキュメントフラグメントの直前に改ページが挿入されます。
* **インデント**:ドキュメントフラグメントのインデントを増減します。
* **後で改ページ** （ターゲット領域の子フラグメントに適用）:ドキュメントフラグメントの後に改ページを挿入します。

![docfragoptions](assets/docfragoptions.png)

* 編集：（テキストフラグメントの場合のみ）テキストドキュメントフラグメントを編集するためのリッチテキストエディターが起動します。詳しくは、[テキストのフォーマット](#formattingtext)を参照してください。

* 選択（目のアイコン）：インタラクティブ通信にドキュメントフラグメントを含めたり、インタラクティブ通信からドキュメントフラグメントを除外したりすることができます。
* 未入力値：ターゲット領域の未入力変数の数が表示されます。これは、表示専用情報です。

### リストドキュメントフラグメント {#list-document-fragments}

![listoptions](assets/listoptions.png)

* 空白行を挿入： 空白行を挿入します。
* 選択（目のアイコン）：インタラクティブ通信にドキュメントフラグメントを含めたり、インタラクティブ通信からドキュメントフラグメントを除外したりすることができます。
* 箇条書き／番号付けをスキップ：リストドキュメントフラグ内で、箇条書きまたは番号付けをスキップすることができます。
* 未入力値：ターゲット領域の未入力変数の数が表示されます。これは、表示専用情報です。

