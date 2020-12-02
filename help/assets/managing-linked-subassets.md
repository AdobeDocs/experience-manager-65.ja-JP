---
title: 参照と複数のページを持つ複合アセットの管理
description: ' [!DNL Adobe InDesign], [!DNL Adobe Illustrator], and [!DNL Adobe Photoshop]内からデジタルアセットへの参照を作成する方法を説明します。 ページビューア機能を使用して、PDF、INDD、PPT、PPTX、AIファイルなどの複数ページファイルの個々のサブアセットページを表示します。'
contentOwner: AG
translation-type: tm+mt
source-git-commit: 12c56c27c7f97f1029c757ec6d28f482516149d0
workflow-type: tm+mt
source-wordcount: '1348'
ht-degree: 17%

---


# 複合アセットと複数ページアセットの管理{#managing-compound-assets}

[!DNL Adobe Experience Manager Assets] アップロードしたファイルに、リポジトリ内に既に存在するアセットへの参照が含まれているかどうかを識別できます。この機能は、サポート対象のファイル形式でのみ使用できます。アップロードしたアセットに[!DNL Experience Manager]アセットへの参照が含まれている場合、アップロードされたアセットと参照されているアセットの間に双方向リンクが作成されます。

冗長性を排除するだけでなく、[!DNL Adobe Creative Cloud]アプリケーションでアセットを参照することで、コラボレーションを強化し、ユーザーの効率と生産性を向上させることができます。

[!DNL Experience Manager Assets] は、双方向参照をサポートします。参照元のアセットは、アップロードされたファイルのアセットの詳細ページで確認できます。また、参照元のアセットのアセットの詳細ページに、参照元のファイルを表示することもできます。

参照は、参照元のアセットのパス、ドキュメント ID およびインスタンス ID に基づいて解決されます。

## [!DNL Adobe Illustrator] {#refai}追加の参照としてのデジタルアセット

[!DNL Adobe Illustrator]ファイル内から既存のデジタルアセットを参照できます。

1. [[!DNL Experience Manager] デスクトップアプリ](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)を使用して、デジタルアセットをローカルファイルシステムに取得します。 参照するアセットのファイルシステムの場所に移動します。
1. アセットをローカルフォルダーから[!DNL Illustrator]ファイルにドラッグします。

1. [!DNL Illustrator]ファイルをマウントされたドライブに保存するか、[upload](/help/assets/manage-assets.md#uploading-assets)を[!DNL Experience Manager]リポジトリに保存します。

1. ワークフローが完了したら、そのアセットのアセットの詳細ページに移動します。既存のデジタルアセットへの参照は、**[!UICONTROL 参照]**&#x200B;列の&#x200B;**[!UICONTROL 依存関係]**&#x200B;の下に一覧表示されます。

   ![chlimage_1-84](assets/chlimage_1-258.png)

1. 「**[!UICONTROL 依存関係]**」に表示される参照元のアセットは、現在のファイルとは異なるファイルからも参照できます。参照先のファイルのリストを表示するには、「**[!UICONTROL 依存関係]**」にあるアセットをクリックします。

   ![chlimage_1-85](assets/chlimage_1-259.png)

1. ツールバーの&#x200B;**[!UICONTROL 表示のプロパティ]**&#x200B;をクリックします。 [!UICONTROL プロパティ]ページの現在のアセットを参照するファイルのリストは、**[!UICONTROL 基本]**&#x200B;タブの&#x200B;**[!UICONTROL 参照]**&#x200B;列に表示されます。

   ![アセットの詳細の「参照」列のExperience Managerアセットの参照を表示する](assets/asset-references.png)

   *図：アセットの詳細内のアセット参照。*

## [!DNL Adobe InDesign] {#add-aem-assets-as-references-in-adobe-indesign}追加の参照としてのデジタルアセット

[!DNL InDesign]ファイル内からデジタルアセットを参照するには、アセットを[!DNL InDesign]ファイルにドラッグするか、[!DNL InDesign]ファイルをZIPアーカイブとして書き出します。

参照されたアセットは既に[!DNL Experience Manager Assets]に存在します。 [InDesign Server](indesign.md)を設定すると、サブアセットを抽出できます。 [!DNL InDesign]ファイルに埋め込まれたアセットは、サブアセットとして抽出されます。

>[!NOTE]
>
>[!DNL InDesign Server]がプロキシになると、[!DNL InDesign]ファイルのプレビューがXMPメタデータに埋め込まれます。 この場合、サムネールの抽出は明示的には必要ありません。ただし、[!DNL InDesign Server]がプロキシ化されていない場合は、[!DNL InDesign]ファイルのサムネールを明示的に抽出する必要があります。

###  アセットをドラッグして参照を作成 {#create-references-by-dragging-aem-assets}

この手順は、[Adobe Illustrator](#refai)でデジタルアセットを参照として追加する手順と似ています。

### ZIP ファイルに書き出してアセットの参照を作成 {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. [ワークフローモデルの作成](/help/sites-developing/workflows-models.md)の手順を実行して、新しいワークフローを作成します。
1. [!DNL Adobe InDesign]のパッケージ機能を使用して、ドキュメントを書き出します。 [!DNL Adobe InDesign] ではドキュメントおよびリンクされたアセットを 1 つのパッケージとして書き出すことができます。この場合、書き出されたフォルダーには、[!DNL InDesign]ファイル内のサブアセットを含むLinksフォルダーが含まれます。
1. ZIPファイルを作成し、[!DNL Experience Manager]リポジトリにアップロードします。
1. `Unarchiver`ワークフローの開始。
1. ワークフローが完了すると、Linksフォルダー内の参照は自動的にサブアセットとして参照されます。 参照されるアセットのリストを表示するには、[!DNL InDesign]アセットのアセットの詳細ページに移動し、[パネル](/help/sites-authoring/basic-handling.md#rail-selector)を閉じます。

## [!DNL Adobe Photoshop] {#refps}追加の参照としてのデジタルアセット

1. [!DNL Experience Manager]デスクトップアプリを使用して[!DNL Experience Manager Assets]にアクセスします。 ローカルファイルシステム上のアセットをダウンロードして表示します。 [!UICONTROL リンクを配置]機能を[!DNL Adobe Photoshop]で使用します。 詳しくは、[デスクトップアプリにアセットを配置](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#place-assets-in-native-documents)を参照してください。

   ![chlimage_1-87](assets/chlimage_1-261.png)

1. [!DNL Photoshop]ファイルをマウントされたドライブに保存するか、[](/help/assets/manage-assets.md#uploading-assets)を[!DNL Experience Manager]リポジトリにアップロードします。
1. ワークフローが完了すると、既存の[!DNL Experience Manager]アセットへの参照がアセットの詳細ページに表示されます。

   参照元のアセットを表示するには、アセットの詳細ページで[パネル](/help/sites-authoring/basic-handling.md#rail-selector)を閉じます。

1. 参照元のアセットには、参照元のアセットのリストも含まれています。参照元のアセットのリストを表示するには、アセットの詳細ページに移動して、[パネル](/help/sites-authoring/basic-handling.md#rail-selector)を閉じます。

>[!NOTE]
>
>複合アセット内のアセットも、ドキュメント ID とインスタンス ID に基づいて参照できます。この機能は[!DNL Adobe Illustrator]および[!DNL Adobe Photoshop]バージョンでのみ利用できます。 その他の場合は、主複合アセット内のリンクされたアセットの相対パスに基づいて参照が行われます。これは、以前のバージョンの[!DNL Experience Manager]で行われた操作です。

## サブアセットを作成{#generate-subassets}

複数ページ形式のサポートされるアセット（PDFファイル、AIファイル、[!DNL Microsoft PowerPoint]ファイル、[!DNL Apple Keynote]ファイル、[!DNL Adobe InDesign]ファイル）の場合、[!DNL Experience Manager]は、元のアセットの個々のページに対応するサブアセットを生成できます。 これらのサブアセットは&#x200B;*親*&#x200B;アセットにリンクされ、複数ページの表示が容易になります。 その他の目的では、[!DNL Experience Manager]内のサブアセットは通常のアセットと同じように扱われます。

サブアセットの生成はデフォルトでは無効になっています。サブアセットの生成を有効にするには、次の手順に従います。

1. 管理者として[!DNL Experience Manager]にログインします。 **[!UICONTROL ツール]**/**[!UICONTROL ワークフロー]**/**[!UICONTROL モデル]**&#x200B;にアクセスします。
1. 「**[!UICONTROL DAM Update Asset]**&#x200B;ワークフロー」を選択し、「**[!UICONTROL 編集]**」をクリックします。
1. 「**[!UICONTROL サイドパネルを切り替え]**」をクリックし、**[!UICONTROL サブアセットを作成]**&#x200B;の手順を探します。 ワークフロー追加への手順です。 「**[!UICONTROL 同期]**」をクリックします。

サブアセットを生成するには、次のいずれかの操作を行います。

* 新しいアセット：[!UICONTROL DAM Update Assets]ワークフローは、[!DNL Experience Manager]にアップロードされた新しいアセットで実行されます。 サブアセットは、新しい複数ページのアセット用に自動生成されます。
* 既存の複数ページアセット：次のいずれかの手順に従って、[!UICONTROL DAM Update Assets]ワークフローを手動で実行します。

   * アセットを選択し、[!UICONTROL タイムライン]をクリックして、左側のパネルを開きます。 または、キーボードショートカット`alt + 3`を使用します。 「[!UICONTROL 開始ワークフロー]」をクリックし、「[!UICONTROL DAMアセットを更新]」を選択して「[!UICONTROL 開始]」をクリックし、「[!UICONTROL 続行]」をクリックします。
   * アセットを選択し、ツールバーの[!UICONTROL 作成]/[!UICONTROL ワークフロー]をクリックします。 ポップアップダイアログで、「[!UICONTROL DAMアセットを更新]ワークフロー」を選択し、「[!UICONTROL 開始]」をクリックし、「[!UICONTROL 続行]」をクリックします。

特にMicrosoft Wordドキュメントの場合は、**[!UICONTROL DAM Parse Wordドキュメント]**&#x200B;ワークフローを実行します。 Microsoft Wordドキュメントの内容から`cq:Page`コンポーネントを生成します。 このドキュメントから抽出された画像は `cq:Page` コンポーネントから参照されます。これらの画像は、サブアセットの生成が無効な場合も抽出されます。

## サブアセットの表示 {#viewing-subassets}

サブアセットは、サブアセットが生成され、選択した複数ページのアセットで使用できる場合にのみ表示されます。 生成されたサブアセットを表示するには、複数ページのアセットを開きます。 ページの左上の領域で、「![Option to open left rail](assets/do-not-localize/aem_leftrail_contentonly.png)」をクリックし、リストから「**[!UICONTROL Subassets]**」をクリックします。 リストから「**[!UICONTROL サブアセット]**」を選択した場合。 または、キーボードショートカット`alt + 5`を使用します。

![複数ページのアセットの表示サブアセット](assets/view_subassets_simulation.gif)

## 複数ページファイルのページの表示 {#view-pages-of-a-multi-page-file}

[!DNL Experience Manager Assets]のページビューア機能を使用して、PDF、INDD、PPT、PPTX、AIファイルなどの複数ページのファイルを表示できます。 複数ページのアセットを開き、ページの左上隅にある「**[!UICONTROL 表示ページ]**」をクリックします。 ページビューアが開き、アセットのページが表示されます。また、各ページを参照およびズームするためのコントロールが表示されます。

![複数ページのアセットの表示とページの確認](assets/view_multipage_asset_fmr.gif)

[!DNL InDesign]の場合は、[!DNL InDesign Server]を使用してページを抽出できます。 [!DNL InDesign]ファイルの作成中にページのプレビューが保存された場合、ページ抽出に[!DNL InDesign Server]は不要です。

次のオプションは、ツールバー、左側のナビゲーションバーおよびページビューアコントロールで使用できます。

* **[!UICONTROL デスクトップ]** アクションを使用して、デスクトッ [!DNL Experience Manager] プアプリを使用して特定のサブアセットを開いたり、表示したりします。[デスクトップアプリを使用する場合は、&lt;a0/>デスクトップアクション](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2)を設定する方法を参照してください。[!DNL Experience Manager]

* **[!UICONTROL 「]** プロパティ」オプションは、特定のサブアセットの  プロパティページを開きます。

* **[!UICONTROL 「]** 注釈」オプションを使用すると、特定のサブアセットに注釈を付けることができます。別のサブアセットで使用する注釈は、親アセットを表示用に開いたときに収集され、一緒に表示されます。

* **[!UICONTROL 「ページの]** 概要」オプションを選択すると、すべてのサブアセットが同時に表示されます。

* **[!UICONTROL 左側のレールを開くには、左側のレールの左側のレールで「]** Option」をクリックした後に、左側のレールのTimelineオプションにファイルのアクティビティストリーム ![](assets/do-not-localize/aem_leftrail_contentonly.png) が表示されます。

## ベストプラクティスと制限{#best-practice-limitation-tips}

* サブアセットの生成は、[!DNL Experience Manager]の展開ではリソースを大量に消費する可能性があります。 複雑なアセットがアップロードされたときにサブアセットを生成する場合は、DAMアセットの更新ワークフローで手順を追加します。 サブアセットをオンデマンドで生成する場合は、サブアセットを生成するための別のワークフローを作成します。 専用ワークフローを使用すると、DAM Update Assetワークフローの他の手順をスキップして、計算リソースを保存できます。

>[!MORELIKETHIS]
>
>* [Adobe Experience Manager デスクトップアプリケーションの使用](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)
>* [Adobe Experience ManagerでのDesktop Actionsの設定](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2)
>* [リンクされたスマートオブジェクトをAdobe Photoshopで作成](https://helpx.adobe.com/photoshop/using/create-smart-objects.html#create-linked-smart-objects)
>* [Adobe InDesignにグラフィックを配置](https://helpx.adobe.com/jp/indesign/using/placing-graphics.html)

