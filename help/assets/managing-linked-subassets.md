---
title: '[!DNL Adobe Experience Manager]で、参照と複数ページのアセットを含む複合アセットを管理します。'
description: '[!DNL Adobe InDesign]、[!DNL Adobe Illustrator]、[!DNL Adobe Photoshop]からデジタルアセットへの参照を作成する方法を説明します。 ページビューア機能を使用して、PDF、INDD、PPT、PPTX、AIファイルなどの複数ページファイルの個々のサブアセットページを表示します。'
contentOwner: AG
translation-type: tm+mt
source-git-commit: 90f9c0b60d4b0878f56eefea838154bb7627066d

---


# 複合アセットと複数ページアセットの管理 {#managing-compound-assets}

[!DNL Adobe Experience Manager Assets] は、アップロードされたファイルに、リポジトリ内に既に存在するアセットへの参照が含まれているかどうかを識別できます。 この機能は、サポート対象のファイル形式でのみ使用できます。If the uploaded asset contains any references to [!DNL Experience Manager] assets, a bidirectional link is created between the uploaded and referenced assets.

Besides eliminating redundancy, referencing the assets in [!DNL Adobe Creative Cloud] applications enhances collaboration and increases the efficiency and productivity of users.

[!DNL Experience Manager Assets] は、双方向参照をサポートします。 参照元のアセットは、アップロードされたファイルのアセットの詳細ページで確認できます。また、参照元のアセットの表示の詳細ページに、参照元のファイルを詳細に表示することもできます。

参照は、参照元のアセットのパス、ドキュメント ID およびインスタンス ID に基づいて解決されます。

## デジ追加タルアセット(参照元 [!DNL Adobe Illustrator] ) {#refai}

You can reference existing digital assets from within an [!DNL Adobe Illustrator] file.

1. [Experience Managerデスクトップアプリケーションを使用して](https://docs.adobe.com/content/help/ja-JP/experience-manager-desktop-app/using/using.html)、デジタルアセットをローカルファイルシステムに取り込みます。 参照するアセットのファイルシステムの場所に移動します。
1. Drag the asset from the local folder to the [!DNL Illustrator] file.

1. Save the [!DNL Illustrator] file to the mounted drive, or [upload](/help/assets/managing-assets-touch-ui.md#uploading-assets) to the [!DNL Experience Manager] repository.

1. ワークフローが完了したら、そのアセットのアセットの詳細ページに移動します。The references to existing digital assets are listed under **[!UICONTROL Dependencies]** in the **[!UICONTROL References]** column.

   ![chlimage_1-84](assets/chlimage_1-258.png)

1. 「**[!UICONTROL 依存関係]**」に表示される参照元のアセットは、現在のファイルとは異なるファイルからも参照できます。参照先のファイルのリストを表示するには、「**[!UICONTROL 依存関係]**」にあるアセットをクリックします。

   ![chlimage_1-85](assets/chlimage_1-259.png)

1. Click **[!UICONTROL View Properties]** from the toolbar. In the [!UICONTROL Properties] page, the list of files that reference the current asset appear under the **[!UICONTROL References]** column in the **[!UICONTROL Basic]** tab.

   ![表示の詳細の「参照」列にあるExperience Managerアセットの参照](assets/asset-references.png)

   *図：アセットの詳細のアセット参照。*

## デジ追加タルアセット(参照元 [!DNL Adobe InDesign] ) {#add-aem-assets-as-references-in-adobe-indesign}

To reference digital assets from within an [!DNL InDesign] file, either drag assets to the [!DNL InDesign] file or export the [!DNL InDesign] file as a ZIP archive.

Referenced assets already exist in [!DNL Experience Manager Assets]. You can extract subassets by [configuring InDesign Server](indesign.md). Embedded assets in an [!DNL InDesign] file are extracted as subassets.

>[!NOTE]
>
>If the [!DNL InDesign Server] is proxied, [!DNL InDesign] files have their preview embedded within their XMP metadata. この場合、サムネールの抽出は明示的には必要ありません。However, if the [!DNL InDesign Server] is not proxied, thumbnails must be explicitly extracted for [!DNL InDesign] files.

###  アセットをドラッグして参照を作成 {#create-references-by-dragging-aem-assets}

This procedure is similar to [add digital assets as references in Adobe Illustrator](#refai).

### ZIP ファイルに書き出してアセットの参照を作成 {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. Perform the steps in [Create workflow models](/help/sites-developing/workflows-models.md) to create a new workflow.
1. Use the Package feature of [!DNL Adobe InDesign] to export the document. [!DNL Adobe InDesign] ではドキュメントおよびリンクされたアセットを 1 つのパッケージとして書き出すことができます。In this case, the exported folder contains a Links folder that contains sub-assets in the [!DNL InDesign] file.
1. Create a ZIP file and upload it to the [!DNL Experience Manager] repository.
1. Start the `Unarchiver` workflow.
1. ワークフローが完了すると、Linksフォルダー内の参照が自動的にサブアセットとして参照されます。 To view a list of referred assets, navigate to the asset details page of the [!DNL InDesign] asset and close the [Rail](/help/sites-authoring/basic-handling.md#rail-selector).

## デジ追加タルアセット(参照元 [!DNL Adobe Photoshop] ) {#refps}

1. デスクトップ [!DNL Experience Manager] アプリを使用してアクセスしま [!DNL Experience Manager Assets]す。 ローカルファイルシステム上のアセットをダウンロードして表示します。 で[リンクを配 [!UICONTROL 置] ]機能を使用しま [!DNL Adobe Photoshop]す。 詳しくは、デス [クトップアプリへのアセットの配置を参照してくださ](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#place-assets-in-native-documents)い。

   ![chlimage_1-87](assets/chlimage_1-261.png)

1. Save in [!DNL Photoshop] file to the mounted drive or or [upload](/help/assets/managing-assets-touch-ui.md#uploading-assets) to the [!DNL Experience Manager] repository.
1. After the workflow completes, the references to existing [!DNL Experience Manager] assets are listed in the asset details page.

   参照元のアセットを表示するには、アセットの詳細ページで[パネル](/help/sites-authoring/basic-handling.md#rail-selector)を閉じます。

1. 参照元のアセットには、参照元のアセットのリストも含まれています。参照元のアセットのリストを表示するには、アセットの詳細ページに移動して、[パネル](/help/sites-authoring/basic-handling.md#rail-selector)を閉じます。

>[!NOTE]
>
>複合アセット内のアセットも、ドキュメント ID とインスタンス ID に基づいて参照できます。This functionality is available with [!DNL Adobe Illustrator] and [!DNL Adobe Photoshop] versions only. For others, referencing is done on the basis of relative path of linked assets in the main compound asset as done in earlier versions of [!DNL Experience Manager].

## サブアセットの作成 {#generate-subassets}

複数ページ形式のサポートされているアセットの場合 — PDFファイル、AIファイル、フ [!DNL Microsoft PowerPoint] ァイ [!DNL Apple Keynote] ル、ファ [!DNL Adobe InDesign] イル — 元のア [!DNL Experience Manager] セットの各ページに対応するサブアセットを生成できます。 これらのサブアセットは親アセットにリ *ンクされ* 、複数ページの表示が容易です。 その他の目的では、サブアセットは、では通常のアセットと同じように扱われま [!DNL Experience Manager]す。

サブアセットの生成はデフォルトでは無効になっています。サブアセットの生成を有効にするには、次の手順に従います。

1. Log into [!DNL Experience Manager] as an administrator. Access **[!UICONTROL Tools > Workflow > Models]**.
1. 「 **[!UICONTROL DAM Update Asset]** workflow」を選択し、「 **[!UICONTROL Edit」をクリックします]**。
1. 「サイドパ **[!UICONTROL ネルを切り替え]** 」をクリックし、「サブア **[!UICONTROL セットを作成」ステップを見つ]** けます。 ワークフロー追加へのステップです。 「同期」をク **[!UICONTROL リックしま]**&#x200B;す。

サブアセットを生成するには、次のいずれかの操作を行います。

* 新しいアセット：DAMアセ [!UICONTROL ットの更新ワークフローは] 、にアップロードされた新しいアセットに対して実行されま [!DNL Experience Manager]す。 サブアセットは、新しい複数ページのアセット用に自動生成されます。
* 既存の複数ページアセット：次の手順に従って、 [!UICONTROL DAMアセットの更新ワークフロー] (DAM Update Assets)を手動で実行します。

   * アセットを選択し、「タイムラ [!UICONTROL イン] 」をクリックして左のパネルを開きます。 Alternately, use the keyboard shortcut `alt + 3`. 「 [!UICONTROL 開始ワークフロー]」をクリックし、「 [!UICONTROL DAMアセットを更新」を選択して「]開始 [!UICONTROL 」をクリックし、「続行」をク]リックします。
   * アセットを選択し、ツールバ [!UICONTROL ーで作成/ワークフロー] をクリックします。 ポップアップダイアログで、「 [!UICONTROL DAM Update Asset] workflow」を選択し、「 [!UICONTROL 開始]」をクリックし、「 [!UICONTROL 続行]」をクリックします。

特にMicrosoft Wordドキュメントの場合は、 **[!UICONTROL DAM Parse Word Workflowを実行します]** 。 Microsoft Wordコンポーネ `cq:Page` ントのコンテンツからコンポーネントを生成します。ドキュメント このドキュメントから抽出された画像は `cq:Page` コンポーネントから参照されます。これらの画像は、サブアセットの生成が無効な場合も抽出されます。

## サブアセットの表示 {#viewing-subassets}

サブアセットは、サブアセットが生成され、選択した複数ページのアセットで使用できる場合にのみ表示されます。 生成されたサブ表示を作成するには、複数ページのアセットを開きます。 ページの左上の領域で、左側のパネルアイコンをクリックし ![、](assets/do-not-localize/aem_leftrail_contentonly.png) 「サブアセット」を **[!UICONTROL リストします]** 。 「サブアセット」を **[!UICONTROL リスト]** 。 Alternately, use the keyboard shortcut `alt + 5`.

![表示のサブアセット（複数ページのアセット用）](assets/view_subassets_simulation.gif)

## 複数ページファイルのページの表示 {#view-pages-of-a-multi-page-file}

のページビューア機能を使用して、PDF、INDD、PPT、PPTX、AIファイルなどの複数ページのファイルを表示できます [!DNL Experience Manager Assets]。 複数ページのアセットを開き、ページの **[!UICONTROL 表示]** 「ページ」をクリックします。 アセットのページが表示されるページビューアと、各ページを参照およびズームするコントロールです。

![表示と複数ページのアセットのページの確認](assets/view_multipage_asset_fmr.gif)

の場合、 [!DNL InDesign]を使用してページを抽出できま [!DNL InDesign Server]す。 If the previews of pages are saved during [!DNL InDesign] file creation, then [!DNL InDesign Server] is not required for page extraction.

ツールバー、左側のナビゲーションバーおよびページビューアのコントロールで、次のオプションを使用できます。

* **[!UICONTROL 「デスクトップアクション]** 」をクリックし、デスクトップアプリを使用して特定のサブアセットを開いたり、表 [!DNL Experience Manager] 示したりします。 Desktop Appを使用する場合 [は、Desktop Actions](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#desktopactions-v2) （デスクトップアクション）の設定方法を [!DNL Experience Manager] 参照してください。

* **[!UICONTROL 「プロパティ]** 」オプションは、特定の [!UICONTROL サブアセットの] 「プロパティ」ページを開きます。

* **[!UICONTROL Annotate]** （注釈）オプションを使用すると、特定のサブアセットに注釈を付けることができます。 別のサブアセットで使用する注釈は、親アセットを表示用に開いたときに収集され、一緒に表示されます。

* **[!UICONTROL 「ページの概要]** 」オプションを選択すると、すべてのサブアセットが同時に表示されます。

* **[!UICONTROL 左のパネル]** アイコンをクリックした後の左のパネルから ![のタイムラインオプションで](assets/do-not-localize/aem_leftrail_contentonly.png) 、ファイルのアクティビティストリームが表示されます。

>[!MORELIKETHIS]
>
>* [Adobe Experience Manager デスクトップアプリケーションの使用](https://docs.adobe.com/content/help/ja-JP/experience-manager-desktop-app/using/using.html)
>* [Adobe Experience Managerでのデスクトップアクションの設定](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#desktopactions-v2)
>* [Adobe Photoshopでのリンクされたスマートオブジェクトの作成](https://helpx.adobe.com/photoshop/using/create-smart-objects.html#create-linked-smart-objects)
>* [Adobe InDesignでのグラフィックの配置](https://helpx.adobe.com/jp/indesign/using/placing-graphics.html)