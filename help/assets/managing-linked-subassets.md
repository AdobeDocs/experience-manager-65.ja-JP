---
title: Experience Managerで、参照と複数ページのアセットを含む複合アセットを管理します。
description: InDesign、IllustratorおよびPhotoshopからAEMアセットへの参照を作成する方法を説明します。 ページビューア機能を使用して、PDF、INDD、PPT、PPTX、AIファイルなどの複数ページのファイルの個々のサブアセットページを表示します。
contentOwner: AG
translation-type: tm+mt
source-git-commit: d15273e9308926ca4745fc1045e2da9fe8ed91d4

---


# 複合アセットと複数ページアセットの管理 {#managing-compound-assets}

Adobe Experience Manager（AEM） Assets では、アップロードされたファイルに、リポジトリ内の既存のアセットへの参照が含まれているかどうかを確認できます。この機能は、サポート対象のファイル形式でのみ使用できます。アップロードされたアセットに AEM アセットへの参照が含まれている場合、アップロードされたアセットと参照先のアセットの間に双方向のリンクが作成されます。

Adobe Creative Cloud アプリケーションで AEM アセットを参照することで、冗長性を排除するだけでなく、コラボレーションを強化し、ユーザーの作業効率と生産性を高めることができます。

AEM Assetsでは、双方向の参照がサポートされています。 参照されたアセットは、アップロードされたファイルのアセットの詳細ページで検索できます。 さらに、AEM アセットの参照元のファイルは、参照先のアセットのアセットの詳細ページで確認できます。

参照は、参照先のアセットのパス、ドキュメント ID およびインスタンス ID に基づいて解決されます。

## Adobe Illustrator 内で AEM アセットを参照として追加 {#refai}

既存の AEM アセットを、Adobe Illustrator ファイル内から参照できます。

1. Using [AEM desktop app](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html), mount AEM Assets repository as a drive on your local machine. マウントしたドライブ内で、参照するアセットの場所に移動します。
1. マウントしたドライブから Illustrator ファイルにアセットをドラッグします。

1. Save the Illustrator file to the mounted drive, or [upload](/help/assets/managing-assets-touch-ui.md#uploading-assets) to the AEM repository.

1. ワークフローが完了したら、アセットのアセットの詳細ページに移動します。 既存の AEM アセットへの参照は、「**[!UICONTROL 参照]**」列の「**[!UICONTROL 依存関係]**」に一覧表示されます。

   ![chlimage_1-84](assets/chlimage_1-258.png)

1. The referenced assets that appear under **[!UICONTROL Dependencies]** can also be referenced by files other than the current one. 参照元のファイルのリストを表示するには、「**[!UICONTROL 依存関係]**」にあるアセットをクリックします。

   ![chlimage_1-85](assets/chlimage_1-259.png)

1. Click **[!UICONTROL View Properties]** from the toolbar. In the [!UICONTROL Properties] page, the list of files that reference the current asset appear under the **[!UICONTROL References]** column in the **[!UICONTROL Basic]** tab.

   ![アセットの詳細の「参照」列にExperience Managerアセットの参照を表示します。](assets/asset-references.png)

   *図：アセットの詳細のアセット参照*

## Adobe InDesign 内で AEM アセットを参照として追加 {#add-aem-assets-as-references-in-adobe-indesign}

InDesignファイル内からAEMアセットを参照するには、AEMアセットをInDesignファイルにドラッグするか、InDesignファイルをZIPファイルとして書き出します。

参照先のアセットは AEM Assets に既に存在します。サブアセットは、[InDesign サーバーを設定](/help/assets/indesign.md)することで抽出できます。InDesignファイルに埋め込まれたアセットは、サブアセットとして抽出されます。

>[!NOTE]
>
>InDesign サーバーにプロキシが設定されている場合、InDesign のファイルのプレビューが XMP メタデータ内に組み込まれています。この場合、サムネールの抽出は明示的には必要ありません。ただし、InDesign にプロキシが設定されていない場合、InDesign のファイルでサムネールを明示的に抽出する必要があります。

### Create references by dragging assets {#create-references-by-dragging-aem-assets}

This procedure is similar to [Add AEM assets as references in Adobe Illustrator](#refai).

### ZIP ファイルに書き出して アセットの参照を作成 {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. Perform the steps in [Create workflow models](/help/sites-developing/workflows-models.md) to create a new workflow.
1. Adobe InDesign のパッケージ機能を使用して、ドキュメントを書き出します。
Adobe InDesign ではドキュメントおよびリンクされたアセットを 1 つのパッケージとして書き出すことができます。この場合、書き出されたフォルダーには、InDesign ファイル内のサブアセットを格納するための Links フォルダーが含まれます。
1. ZIP ファイルを作成し、このファイルを AEM リポジトリにアップロードします。
1. Start the `Unarchiver` workflow.
1. When the workflow completes, the references in the Links folder are automatically referenced as subassets. To view a list of referred assets, navigate to the asset details page of the InDesign asset and close the [Rail](/help/sites-authoring/basic-handling.md#rail-selector).

## Adobe Photoshop 内で AEM アセットを参照として追加 {#refps}

1. WebDav クライアントを使用して、AEM Assets をドライブとしてマウントします。
1. Photoshop ファイルに AEM アセットへの参照を作成するには、Photoshop のリンクを配置機能を使用して、マウントしたドライブで対応するアセットに移動します。

   ![chlimage_1-87](assets/chlimage_1-261.png)

1. Save in Photoshop file to the mounted drive or or [upload](/help/assets/managing-assets-touch-ui.md#uploading-assets) to the AEM repository.
1. ワークフローが完了すると、既存のAEMアセットへの参照がアセットの詳細ページに表示されます。

   To view the referenced assets, close the [Rail](/help/sites-authoring/basic-handling.md#rail-selector) in the asset details page.

1. The referenced assets also contain the list of assets they are referenced from. To view a list of referenced assets, navigate to the asset details page and close the [Rail](/help/sites-authoring/basic-handling.md#rail-selector).

>[!NOTE]
>
>複合アセット内のアセットは、ドキュメントIDとインスタンスIDに基づいて参照することもできます。 この機能は、Adobe Illustrator と Adobe Photoshop のバージョンでのみ使用できます。その他の場合、AEM の以前のバージョンと同様に、メインの複合アセット内でリンクされたアセットの相対パスに基づいて参照が実行されます。

## サブアセットの作成 {#generate-subassets}

複数ページ形式のサポートされているアセットの場合 — PDFファイル、AIファイル、Microsoft PowerPointおよびApple Keynoteファイル、Adobe InDesignファイル — AEMは、元のアセットの個々のページに対応するサブアセットを生成できます。 これらのサブアセットは親アセットにリ *ンクされ* 、複数ページの表示が容易になります。 その他の目的では、サブアセットはAEMでは通常のアセットと同様に扱われます。

サブアセットの生成はデフォルトでは無効になっています。サブアセットの生成を有効にするには、次の手順に従います。

1. 管理者としてExperience Managerにログインします。 Access **[!UICONTROL Tools > Workflow > Models]**.
1. 「 **[!UICONTROL DAM Update Asset]** workflow」を選択し、「 **[!UICONTROL Edit」をクリックします]**。
1. 「サイドパ **[!UICONTROL ネルを切り替え]** 」をクリックし、「サブア **[!UICONTROL セットを作成」ステップを見つ]** けます。 ワークフローに手順を追加します。 「同期」をク **[!UICONTROL リックしま]**&#x200B;す。

サブアセットを生成するには、次のいずれかの操作を行います。

* 新しいアセット：DAMアセ [!UICONTROL ットの更新ワークフローは] 、AEMにアップロードされた新しいアセットに対して実行されます。 サブアセットは、新しい複数ページのアセット用に自動生成されます。
* 既存の複数ページアセット：次の手順に従って、 [!UICONTROL DAMアセットの更新ワークフロー] (DAM Update Assets)を手動で実行します。

   * アセットを選択し、「タイムラ [!UICONTROL イン] 」をクリックして左のパネルを開きます。 または、キーボードショートカットを使用しま `alt + 3`す。 「ワークフ [!UICONTROL ローを開始]」をクリックし、「 [!UICONTROL DAM Update Asset]」を選択し、「開始」をクリックして [!UICONTROL 、「続行」をク]リックします。
   * アセットを選択し、ツールバ [!UICONTROL ーで作成/ワークフロー] をクリックします。 ポップアップダイアログで、「 [!UICONTROL DAM Update Asset] workflow」を選択し、「 [!UICONTROL Start]」をクリックし、「 [!UICONTROL Proceed]」をクリックします。

特にMicrosoft Wordドキュメントの場合は、 **[!UICONTROL DAM Parse Wordドキュメントワークフローを実行します]** 。 Microsoft Word文書のコ `cq:Page` ンテンツからコンポーネントを生成します。 The images extracted from the document are referenced from the `cq:Page` component. これらの画像は、サブアセットの生成が無効な場合も抽出されます。

## View subassets {#viewing-subassets}

サブアセットは、サブアセットが生成され、選択した複数ページのアセットで使用できる場合にのみ表示されます。 生成されたサブアセットを表示するには、複数ページのアセットを開きます。 ページの左上の領域で、左側のパネルアイコンをクリックし ![、リストから](assets/do-not-localize/aem_leftrail_contentonly.png) 「サブアセ **[!UICONTROL ット]** 」をクリックします。 リストから「サブア **[!UICONTROL セット]** 」を選択した場合。 または、キーボードショートカットを使用しま `alt + 5`す。

![複数ページのアセットのサブアセットの表示](assets/view_subassets_simulation.gif)

## 複数ページファイルのページの表示 {#view-pages-of-a-multi-page-file}

AEM Assetsのページビューア機能を使用して、PDF、INDD、PPT、PPTX、AIファイルなどの複数ページのファイルを表示できます。 複数ページのアセットを開き、ペ **[!UICONTROL ージの左上隅]** 「ページを表示」をクリックします。 アセットのページが表示されるページビューアと、各ページを参照およびズームするコントロールです。

![複数ページのアセットのページの表示と表示](assets/view_multipage_asset_fmr.gif)

InDesign では、InDesign サーバーを使用してページを抽出できます。InDesign ファイルの作成中にページのプレビューが保存されている場合は、ページを抽出するために InDesign サーバーを使用する必要はありません。

ツールバー、左側のナビゲーションバーおよびページビューアのコントロールで、次のオプションを使用できます。

* **[!UICONTROL デスクトップアクション]** :AEMデスクトップアプリを使用して特定のサブアセットを開いたり、表示したりします。 AEMデスクトップアプリを使 [用する場合は](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#desktopactions-v2) 、Desktop Actionsを設定する方法を参照してください。

* **[!UICONTROL 「プロパティ]** 」オプションは、特定の [!UICONTROL サブアセットの] 「プロパティ」ページを開きます。

* **[!UICONTROL Annotate]** （注釈）オプションを使用すると、特定のサブアセットに注釈を付けることができます。 別のサブアセットで使用する注釈は、親アセットを表示用に開いたときに収集され、一緒に表示されます。

* **[!UICONTROL 「ページの概要]** 」オプションを選択すると、すべてのサブアセットが同時に表示されます。

* **[!UICONTROL 左側のパネル]** （左側のパネル）アイコンをクリックした後に、左側のパネル ![からタイムラインオプションを選択すると](assets/do-not-localize/aem_leftrail_contentonly.png) 、ファイルのアクティビティストリームが表示されます。
