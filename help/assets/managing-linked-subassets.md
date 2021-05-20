---
title: 参照と複数のページを含む複合アセットの管理
description: ' [!DNL Adobe InDesign], [!DNL Adobe Illustrator], and [!DNL Adobe Photoshop]内からデジタルアセットへの参照を作成する方法を説明します。 ページビューア機能を使用して、PDF、INDD、PPT、PPTX、AIファイルなど、複数ページのファイルの個々のサブアセットページを表示します。'
contentOwner: AG
role: Business Practitioner, Administrator
feature: アセット管理
exl-id: 1ea9d8fe-602c-452b-9a24-4125b705aedf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1380'
ht-degree: 18%

---

# 複合アセットと複数ページアセットの管理{#managing-compound-assets}

[!DNL Adobe Experience Manager Assets] は、アップロードされたファイルに、リポジトリ内に既に存在するアセットへの参照が含まれているかどうかを識別できます。この機能は、サポート対象のファイル形式でのみ使用できます。アップロードされたアセットに[!DNL Experience Manager]アセットへの参照が含まれている場合、アップロードされたアセットと参照先のアセットの間に双方向のリンクが作成されます。

冗長性を排除するだけでなく、[!DNL Adobe Creative Cloud]アプリケーションでアセットを参照することで、コラボレーションを強化し、ユーザーの効率と生産性を向上させます。

[!DNL Experience Manager Assets] は双方向の参照をサポートします。参照元のアセットは、アップロードされたファイルのアセットの詳細ページで確認できます。さらに、参照元のファイルは、参照元のアセットのアセットの詳細ページに表示できます。

参照は、参照元のアセットのパス、ドキュメント ID およびインスタンス ID に基づいて解決されます。

## [!DNL Adobe Illustrator]:デジタルアセットを参照として追加 {#refai}

[!DNL Adobe Illustrator]ファイル内から既存のデジタルアセットを参照できます。

1. [[!DNL Experience Manager] デスクトップアプリケーション](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=ja)を使用して、ローカルファイルシステムのデジタルアセットを取得します。 参照するアセットのファイルシステムの場所に移動します。
1. アセットをローカルフォルダーから[!DNL Illustrator]ファイルにドラッグします。

1. [!DNL Illustrator]ファイルをマウントしたドライブに保存するか、[](/help/assets/manage-assets.md#uploading-assets)を[!DNL Experience Manager]リポジトリにアップロードします。

1. ワークフローが完了したら、そのアセットのアセットの詳細ページに移動します。既存のデジタルアセットへの参照は、**[!UICONTROL 参照]**&#x200B;列の&#x200B;**[!UICONTROL 依存関係]**&#x200B;に一覧表示されます。

   ![chlimage_1-84](assets/chlimage_1-258.png)

1. 「**[!UICONTROL 依存関係]**」に表示される参照元のアセットは、現在のファイルとは異なるファイルからも参照できます。参照先のファイルのリストを表示するには、「**[!UICONTROL 依存関係]**」にあるアセットをクリックします。

   ![chlimage_1-85](assets/chlimage_1-259.png)

1. ツールバーの「**[!UICONTROL プロパティを表示]**」をクリックします。 [!UICONTROL プロパティ]ページで、現在のアセットを参照しているファイルのリストが「**[!UICONTROL 基本]**」タブの「**[!UICONTROL 参照]**」列に表示されます。

   ![アセットの詳細の「Experience Manager内のアセットの参照」列の表示](assets/asset-references.png)

   *図：アセットの詳細でのアセット参照。*

## [!DNL Adobe InDesign]:デジタルアセットを参照として追加  {#add-aem-assets-as-references-in-adobe-indesign}

[!DNL InDesign]ファイル内からデジタルアセットを参照するには、アセットを[!DNL InDesign]ファイルにドラッグするか、[!DNL InDesign]ファイルをZIPアーカイブとして書き出します。

参照元のアセットは[!DNL Experience Manager Assets]に既に存在します。 InDesign Server](indesign.md)を設定して、サブアセットを抽出できます。 [[!DNL InDesign]ファイル内の埋め込みアセットは、サブアセットとして抽出されます。

>[!NOTE]
>
>[!DNL InDesign Server]がプロキシ化されている場合、[!DNL InDesign]ファイルのプレビューがXMPメタデータに埋め込まれます。 この場合、サムネールの抽出は明示的には必要ありません。ただし、[!DNL InDesign Server]がプロキシ化されていない場合は、[!DNL InDesign]ファイルに対してサムネールを明示的に抽出する必要があります。

INDDファイルがアップロードされると、リポジトリ内に`xmpMM:InstanceID`プロパティと`xmpMM:DocumentID`プロパティを持つアセットに対するクエリを実行することで、参照が取得されます。

###  アセットをドラッグして参照を作成 {#create-references-by-dragging-aem-assets}

この手順は、Adobe Illustrator](#refai)でデジタルアセットを参照として追加する[の場合と同様です。

### ZIP ファイルに書き出してアセットの参照を作成 {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. [ワークフローモデルの作成](/help/sites-developing/workflows-models.md)の手順を実行して、新しいワークフローを作成します。
1. [!DNL Adobe InDesign]の[パッケージ機能](https://helpx.adobe.com/indesign/how-to/indesign-package-files-for-handoff.html)を使用して、ドキュメントを書き出します。 [!DNL Adobe InDesign] ではドキュメントおよびリンクされたアセットを 1 つのパッケージとして書き出すことができます。この場合、書き出されたフォルダーには、[!DNL InDesign]ファイル内のサブアセットを格納する`Links`フォルダーが含まれます。 `Links`フォルダーは、INDDファイルと同じフォルダーに存在します。
1. ZIPファイルを作成し、[!DNL Experience Manager]リポジトリにアップロードします。
1. `Unarchiver`ワークフローを開始します。
1. ワークフローが完了すると、リンクフォルダー内の参照がサブアセットとして自動的に参照されます。 参照元のアセットのリストを表示するには、[!DNL InDesign]アセットのアセットの詳細ページに移動し、[レール](/help/sites-authoring/basic-handling.md#rail-selector)を閉じます。

## [!DNL Adobe Photoshop]:デジタルアセットを参照として追加 {#refps}

1. [!DNL Experience Manager]デスクトップアプリケーションを使用して[!DNL Experience Manager Assets]にアクセスします。 ローカルファイルシステムでアセットをダウンロードして表示します。 [!UICONTROL リンクされた]を[!DNL Adobe Photoshop]に配置する機能を使用します。 [デスクトップアプリケーションへのアセットの配置](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#place-assets-in-native-documents)を参照してください。

   ![chlimage_1-87](assets/chlimage_1-261.png)

1. [!DNL Photoshop]ファイルをマウントしたドライブに保存するか、[](/help/assets/manage-assets.md#uploading-assets)を[!DNL Experience Manager]リポジトリにアップロードします。
1. ワークフローが完了すると、既存の[!DNL Experience Manager]アセットへの参照がアセットの詳細ページに表示されます。

   参照元のアセットを表示するには、アセットの詳細ページで[パネル](/help/sites-authoring/basic-handling.md#rail-selector)を閉じます。

1. 参照元のアセットには、参照元のアセットのリストも含まれています。参照元のアセットのリストを表示するには、アセットの詳細ページに移動して、[パネル](/help/sites-authoring/basic-handling.md#rail-selector)を閉じます。

>[!NOTE]
>
>複合アセット内のアセットも、ドキュメント ID とインスタンス ID に基づいて参照できます。この機能は、[!DNL Adobe Illustrator]と[!DNL Adobe Photoshop]のバージョンでのみ使用できます。 その他の場合は、以前のバージョンの[!DNL Experience Manager]と同様に、メイン複合アセット内のリンクされたアセットの相対パスに基づいて参照がおこなわれます。

## サブアセット{#generate-subassets}を作成します。

複数ページ形式のアセット（PDFファイル、AIファイル、[!DNL Microsoft PowerPoint]ファイル、[!DNL Apple Keynote]ファイル、[!DNL Adobe InDesign]ファイル）をサポートしている場合、元のアセットの各ページに対応するサブアセットを[!DNL Experience Manager]で生成できます。 これらのサブアセットは&#x200B;*親*&#x200B;アセットにリンクされ、複数ページ表示が容易になります。 その他の目的では、サブアセットは[!DNL Experience Manager]では通常のアセットと同じように扱われます。

サブアセットの生成はデフォルトでは無効になっています。サブアセットの生成を有効にするには、次の手順に従います。

1. [!DNL Experience Manager]に管理者としてログインします。 **[!UICONTROL ツール]** / **[!UICONTROL ワークフロー]** / **[!UICONTROL モデル]**&#x200B;にアクセスします。
1. 「**[!UICONTROL DAMアセットの更新]**」ワークフローを選択し、「**[!UICONTROL 編集]**」をクリックします。
1. **[!UICONTROL サイドパネルを切り替え]**&#x200B;をクリックし、**[!UICONTROL サブアセットを作成]**&#x200B;の手順を見つけます。 ワークフローにステップを追加します。 「**[!UICONTROL 同期]**」をクリックします。

サブアセットを生成するには、次のいずれかの操作を行います。

* 新しいアセット：[!UICONTROL DAMアセットの更新]ワークフローは、[!DNL Experience Manager]にアップロードされた新しいアセットで実行されます。 新しい複数ページアセット用にサブアセットが自動生成されます。
* 既存の複数ページアセット：次のいずれかの手順に従って、[!UICONTROL DAMアセットの更新]ワークフローを手動で実行します。

   * アセットを選択し、「[!UICONTROL タイムライン]」をクリックして左のパネルを開きます。 または、キーボードショートカット`alt + 3`を使用します。 「[!UICONTROL ワークフローを開始]」をクリックし、「[!UICONTROL DAMアセットの更新]」を選択して、「[!UICONTROL 開始]」をクリックし、「[!UICONTROL 続行]」をクリックします。
   * アセットを選択し、ツールバーの[!UICONTROL 作成] / [!UICONTROL ワークフロー]をクリックします。 ポップアップダイアログで、「[!UICONTROL DAMアセットの更新]」ワークフローを選択し、「[!UICONTROL 開始]」をクリックして、「[!UICONTROL 続行]」をクリックします。

特にMicrosoft Wordドキュメントの場合は、**[!UICONTROL DAM Wordドキュメントの解析]**&#x200B;ワークフローを実行します。 Microsoft Wordドキュメントの内容から`cq:Page`コンポーネントが生成されます。 このドキュメントから抽出された画像は `cq:Page` コンポーネントから参照されます。これらの画像は、サブアセットの生成が無効な場合も抽出されます。

## サブアセットの表示 {#viewing-subassets}

サブアセットは、サブアセットが生成され、選択した複数ページのアセットで使用できる場合にのみ表示されます。 生成されたサブアセットを表示するには、複数ページのアセットを開きます。 ページの左上の領域で、「![オプション](assets/do-not-localize/aem_leftrail_contentonly.png)」をクリックして左側のレールを開き、リストから「**[!UICONTROL サブアセット]**」をクリックします。 リストから「**[!UICONTROL サブアセット]**」を選択します。 または、キーボードショートカット`alt + 5`を使用します。

![複数ページアセットのサブアセットの表示](assets/view_subassets_simulation.gif)

## 複数ページファイルのページの表示 {#view-pages-of-a-multi-page-file}

[!DNL Experience Manager Assets]のページビューア機能を使用して、PDF、INDD、PPT、PPTX、AIファイルなどの複数ページファイルを表示できます。 複数ページのアセットを開き、ページの左上隅にある「**[!UICONTROL ページを表示]**」をクリックします。 アセットのページと、各ページを参照およびズームするためのコントロールが表示されるページビューア。

![複数ページアセットのページの表示と表示](assets/view_multipage_asset_fmr.gif)

[!DNL InDesign]の場合は、[!DNL InDesign Server]を使用してページを抽出できます。 [!DNL InDesign]ファイルの作成中にページのプレビューを保存する場合、ページを抽出する際に[!DNL InDesign Server]は必要ありません。

ツールバー、左側のレールおよびページビューアコントロールで、次のオプションを使用できます。

* **[!UICONTROL デスクト]** ップアクションを使用して特定のサブアセットを開く、または表 [!DNL Experience Manager] 示する。[!DNL Experience Manager]デスクトップアプリケーションを使用している場合は、[デスクトップアクションの設定](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=ja#desktopactions-v2)方法を参照してください。

* **[!UICONTROL 「]** プロパティ」オプションは、特  定のサブアセットのプロパティページを開きます。

* **** 「注釈」オプションを使用すると、特定のサブアセットに注釈を付けることができます。別のサブアセットで使用する注釈は、親アセットを表示用に開く際に収集され、一緒に表示されます。

* **[!UICONTROL 「ページの]** 概要」オプションでは、すべてのサブアセットが同時に表示されます。

* **** 左側のレールを開くには、「オプション」をクリックした後 ![の左側のレールのタイムラインオ](assets/do-not-localize/aem_leftrail_contentonly.png) プションに、ファイルのアクティビティストリームが表示されます。

## ベストプラクティスと制限事項{#best-practice-limitation-tips}

* サブアセットの生成は、あらゆる[!DNL Experience Manager]デプロイメントでリソースを大量に消費する可能性があります。 複雑なアセットがアップロードされたときにサブアセットを生成する場合は、 DAMアセットの更新ワークフローにステップを追加します。 オンデマンドでサブアセットを生成する場合は、サブアセットを生成する別のワークフローを作成します。 専用のワークフローを使用すると、 DAMアセットの更新ワークフローの他の手順をスキップして、計算リソースを保存できます。

>[!MORELIKETHIS]
>
>* [Adobe Experience Manager デスクトップアプリケーションの使用](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)
>* [Adobe Experience Managerでのデスクトップアクションの設定](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2)
>* [Adobe Photoshopでのリンクされたスマートオブジェクトの作成](https://helpx.adobe.com/photoshop/using/create-smart-objects.html#create-linked-smart-objects)
>* [Adobe InDesignへのグラフィックの配置](https://helpx.adobe.com/jp/indesign/using/placing-graphics.html)

