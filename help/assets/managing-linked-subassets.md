---
title: 参照と複数のページを持つ複合アセットの管理
description: ' [!DNL Adobe InDesign]、 [!DNL Adobe Illustrator] および  [!DNL Adobe Photoshop] 内からデジタルアセットへの参照を作成する方法を説明します。ページビューア機能を使用して、PDF、INDD、PPT、PPTX、AI ファイルなど、複数ページのファイルの個々のサブアセットページを表示します。'
contentOwner: AG
role: User, Admin
feature: Asset Management
exl-id: 1ea9d8fe-602c-452b-9a24-4125b705aedf
source-git-commit: 79d8b5896f5f8eb7a22dccea81acf0656d435f2b
workflow-type: tm+mt
source-wordcount: '1424'
ht-degree: 100%

---

# 複合アセットと複数ページアセットの管理 {#managing-compound-assets}

[!DNL Adobe Experience Manager Assets] では、アップロードされたファイルに、リポジトリ内の既存のアセットへの参照が含まれているかどうかを確認できます。この機能は、サポート対象のファイル形式でのみ使用できます。アップロードされたアセットに [!DNL Experience Manager] アセットへの参照が含まれている場合、アップロードされたアセットと参照先のアセットの間に双方向のリンクが作成されます。

[!DNL Adobe Creative Cloud] アプリケーションでアセットを参照することで、冗長性を排除するだけでなく、コラボレーションを強化し、ユーザーの作業効率と生産性を高めることができます。

[!DNL Experience Manager Assets] では双方向の参照をサポートしています。参照元のアセットは、アップロードされたファイルのアセットの詳細ページで確認できます。さらに参照ファイルは、参照先のアセットのアセットの詳細ページで確認できます。

参照は、参照元のアセットのパス、ドキュメント ID およびインスタンス ID に基づいて解決されます。

## [!DNL Adobe Illustrator]：デジタルアセットを参照として追加 {#refai}

既存のデジタルアセットを、[!DNL Adobe Illustrator] ファイル内から参照できます。

1. [[!DNL Experience Manager] デスクトップアプリケーション](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=ja)を使用して、ローカルファイルシステム上のデジタルアセットを取得します。参照するアセットのファイルシステムの場所に移動します。
1. ローカルフォルダーから [!DNL Illustrator] ファイルにアセットをドラッグします。

1. [!DNL Illustrator] ファイルをマウントしたドライブに保存するか、[!DNL Experience Manager] リポジトリに[アップロード](/help/assets/manage-assets.md#uploading-assets)します。

1. ワークフローが完了したら、そのアセットのアセットの詳細ページに移動します。既存のデジタルアセットへの参照は、**[!UICONTROL 参照]**&#x200B;列の&#x200B;**[!UICONTROL 依存関係]**&#x200B;に一覧表示されます。

   ![chlimage_1-84](assets/chlimage_1-258.png)

1. 「**[!UICONTROL 依存関係]**」に表示される参照元のアセットは、現在のファイルとは異なるファイルからも参照できます。参照先のファイルのリストを表示するには、「**[!UICONTROL 依存関係]**」にあるアセットをクリックします。

   ![chlimage_1-85](assets/chlimage_1-259.png)

1. ツールバーの&#x200B;**[!UICONTROL プロパティを表示]**&#x200B;をクリックします。[!UICONTROL プロパティ]ページで、現在のアセットを参照しているファイルのリストが「**[!UICONTROL 基本]**」タブの&#x200B;**[!UICONTROL 参照]**&#x200B;列に表示されます。

   ![アセットの詳細の参照列に Experience Manager Assets の参照が表示されます](assets/asset-references.png)

   *図：アセットの詳細内のアセット参照。*

## [!DNL Adobe InDesign]：デジタルアセットを参照として追加 {#add-aem-assets-as-references-in-adobe-indesign}

[!DNL InDesign] ファイル内からデジタルアセットを参照するには、アセットを [!DNL InDesign] ファイルにドラッグするか、[!DNL InDesign] ファイルを ZIP アーカイブとしてエクスポートします。

参照元のアセットは [!DNL Experience Manager Assets] に既に存在します。サブアセットは、[InDesign Server を設定](indesign.md)することで抽出できます。[!DNL InDesign] ファイルに組み込まれたアセットがサブアセットとして抽出されます。

>[!NOTE]
>
>[!DNL InDesign Server] にプロキシが設定されている場合、[!DNL InDesign] のファイルのプレビューが XMP メタデータ内に組み込まれます。この場合、サムネールの抽出は明示的には必要ありません。ただし、[!DNL InDesign Server] にプロキシが設定されていない場合、[!DNL InDesign] のファイルでサムネールを明示的に抽出する必要があります。

INDD ファイルがアップロードされると、`xmpMM:InstanceID` および `xmpMM:DocumentID` プロパティがリポジトリにあるアセットにクエリを実行することで、参照が取得されます。

### アセットをドラッグして参照を作成  {#create-references-by-dragging-aem-assets}

この手順は、[Adobe Illustrator でデジタルアセットを参照として追加する](#refai)場合の手順と同様です。

### ZIP ファイルに書き出してアセットの参照を作成 {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. [ワークフローモデルの作成](/help/sites-developing/workflows-models.md)の手順を実行し、新しいワークフローを作成します。
1. [!DNL Adobe InDesign] の[パッケージ機能](https://helpx.adobe.com/indesign/how-to/indesign-package-files-for-handoff.html)を使用して、ドキュメントをエクスポートします。[!DNL Adobe InDesign] ではドキュメントおよびリンクされたアセットを 1 つのパッケージとして書き出すことができます。この場合、エクスポートされたフォルダーには、[!DNL InDesign] ファイル内のサブアセットを格納するための `Links` フォルダーが含まれます。この `Links` フォルダーが INDD ファイルと同じフォルダーに存在する。
1. ZIP ファイルを作成し、このファイルを [!DNL Experience Manager] リポジトリにアップロードします。
1. `Unarchiver` ワークフローを開始します。
1. ワークフローが完了すると、Links フォルダー内の参照がサブアセットとして自動的に参照されます。参照されているアセットのリストを表示するには、[!DNL InDesign] アセットのアセットの詳細ページに移動して、[パネル](/help/sites-authoring/basic-handling.md#rail-selector)を閉じます。

## [!DNL Adobe Photoshop]：デジタルアセットを参照として追加 {#refps}

1. [!DNL Experience Manager] デスクトップアプリケーションを使用して [!DNL Experience Manager Assets] にアクセスします。ローカルファイルシステムのアセットをダウンロードして表示します。[!DNL Adobe Photoshop] の[!UICONTROL リンク場所]の機能を使用します。詳しくは、[デスクトップアプリケーションへのアセットの配置](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=ja#place-assets-in-native-documents)を参照してください。

1. [!DNL Photoshop] ファイルをマウントしたドライブに保存するか、[!DNL Experience Manager] リポジトリに[アップロード](/help/assets/manage-assets.md#uploading-assets)します。
1. ワークフローが完了したら、既存の [!DNL Experience Manager] アセットへの参照がアセットの詳細ページに一覧表示されます。

   参照元のアセットを表示するには、アセットの詳細ページで[パネル](/help/sites-authoring/basic-handling.md#rail-selector)を閉じます。

1. 参照元のアセットには、参照元のアセットのリストも含まれています。参照元のアセットのリストを表示するには、アセットの詳細ページに移動して、[パネル](/help/sites-authoring/basic-handling.md#rail-selector)を閉じます。

>[!NOTE]
>
>複合アセット内のアセットも、ドキュメント ID とインスタンス ID に基づいて参照できます。この機能は、[!DNL Adobe Illustrator] と [!DNL Adobe Photoshop] のバージョンでのみ使用できます。その以外の場合、[!DNL Experience Manager] の以前のバージョンと同様に、メインの複合アセット内でリンクされたアセットの相対パスに基づいて参照が実行されます。

## サブアセットの作成 {#generate-subassets}

複数ページ形式のサポート対象のアセット（PDF ファイル、AI ファイル、[!DNL Microsoft PowerPoint] および [!DNL Apple Keynote] ファイル、[!DNL Adobe InDesign] ファイル）では、[!DNL Experience Manager] は元のアセットの個々のページに対応するサブアセットを生成できます。これらのサブアセットは&#x200B;*親*&#x200B;アセットにリンクされ、複数ページ表示を容易にします。その他の目的では、サブアセットは [!DNL Experience Manager] での標準アセットのように扱われます。

サブアセットの生成はデフォルトでは無効になっています。サブアセットの生成を有効にするには、次の手順に従います。

1. [!DNL Experience Manager] に管理者としてログインします。**[!UICONTROL ツール]**／**[!UICONTROL ワークフロー]**／**[!UICONTROL モデル]**&#x200B;にアクセスします。
1. **[!UICONTROL DAM アセットの更新]**&#x200B;ワークフローを選択し、**[!UICONTROL 編集]**&#x200B;をクリックしてください。
1. **[!UICONTROL サイドパネルを切り替え]**&#x200B;をクリックし、**[!UICONTROL サブアセットを作成]**&#x200B;のステップを探してください。ワークフローにステップを追加します。 **[!UICONTROL 同期]**&#x200B;をクリックします。

サブアセットを生成するには、以下のいずれかの操作を行います。

* 新しいアセット：この [!UICONTROL DAM アセットの更新]ワークフローは、[!DNL Experience Manager] にアップロードされた新しいアセットで実行されます。複数ページの新しいアセットに対してサブアセットが自動生成されます。
* 既存の複数ページアセット：手動で [!UICONTROL DAM アセットの更新]ワークフローを次のいずれかのステップに従って実行します。

   * アセットを選択し、[!UICONTROL タイムライン]をクリックして、左側のパネルを開きます。または、キーボードショートカット `alt + 3` を使用します。[!UICONTROL ワークフローを開始]をクリックし、[!UICONTROL DAM アセットの更新]を選択して、[!UICONTROL 開始]をクリックしてから、[!UICONTROL 続行]をクリックしてください。
   * アセットを選択し、ツールバーから[!UICONTROL 作成]／[!UICONTROL ワークフロー]をクリックしてください。ポップアップダイアログで、[!UICONTROL DAM アセットの更新]ワークフローを選択して、[!UICONTROL 開始]をクリックしてから、[!UICONTROL 続行]をクリックしてください。

特に Microsoft Word ドキュメントの場合は、**[!UICONTROL DAM Word ドキュメントの解析]**&#x200B;ワークフローを実行します。これにより、`cq:Page`コンポーネントを Microsoft Word ドキュメントのコンテンツから生成します。このドキュメントから抽出された画像は `cq:Page` コンポーネントから参照されます。これらの画像は、サブアセットの生成が無効な場合も抽出されます。

>[!NOTE]
>
>[!UICONTROL プロセスの引数]の[!UICONTROL サブアセットの作成プロセス - ステップのプロパティ]で、[!DNL Experience Manager] が生成するサブアセットの数を指定できます。デフォルト値は 5 です。すべてのサブアセットを生成するには、フィールドを空のままにします。フィールドに負の値が設定されている場合、サブアセットは生成されません。

## サブアセットの表示 {#viewing-subassets}

サブアセットが生成され、選択した複数ページのアセットで使用できる場合にのみ、サブアセットが表示されます。生成されたサブアセットを表示するには、複数ページのアセットを開きます。 ページの左上の領域で、![左側のパネルを開くオプション](assets/do-not-localize/aem_leftrail_contentonly.png)をクリックしてから、リストの&#x200B;**[!UICONTROL サブアセット]**&#x200B;をクリックしてください。 リストから&#x200B;**[!UICONTROL サブアセット]**&#x200B;を選択した場合。または、キーボードショートカット `alt + 5` を使用します。

![複数ページアセットのサブアセットの表示](assets/view_subassets_simulation.gif)

## 複数ページファイルのページの表示 {#view-pages-of-a-multi-page-file}

[!DNL Experience Manager Assets] のページビューア機能を使用して、PDF、INDD、PPT、PPTX および AI ファイルなどの複数ページファイルを表示することができます。複数ページのアセットを開き、ページの左上隅にある&#x200B;**[!UICONTROL ページを表示]**&#x200B;をクリックしてください。開いたページビューアにはアセットのページと、各ページを参照およびズームするためのコントロールが表示されます。

![複数ページアセットのページの表示](assets/view_multipage_asset_fmr.gif)

[!DNL InDesign] の場合、[!DNL InDesign Server] を使用してページを抽出することができます。ページのプレビューが [!DNL InDesign] ファイルの作成中に保存された場合、ページの抽出に [!DNL InDesign Server] は必要ありません。

ツールバー、左側のレールおよびページビューアコントロールで、次のオプションを使用できます。

* [!DNL Experience Manager] デスクトップアプリケーションを使用して、特定のサブアセットを開くまたは表示する&#x200B;**[!UICONTROL デスクトップアクション]**。[!DNL Experience Manager] デスクトップアプリケーションを使用している場合は、[デスクトップアクションの設定](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=ja#desktopactions-v2)を参照してください。

* **[!UICONTROL プロパティ]**&#x200B;オプションを選択すると、特定のサブアセットの[!UICONTROL プロパティ]ページが開きます。

* **[!UICONTROL 注釈]**&#x200B;オプションを使用すると、特定のサブアセットに注釈を付けることができます。 別のサブアセットで使用する注釈は、親アセットを表示用に開いたときに収集および表示されます。

* 「**[!UICONTROL ページ概要]**」オプションを選択すると、すべてのサブアセットが同時に表示されます。

* ![左側のパネルを開くオプション](assets/do-not-localize/aem_leftrail_contentonly.png)をクリックした後、左側のパネルの&#x200B;**[!UICONTROL タイムライン]**&#x200B;オプションをクリックすると、ファイルのアクティビティストリームが表示されます。

## ベストプラクティスと制限事項 {#best-practice-limitation-tips}

* サブアセットの生成は、あらゆる [!DNL Experience Manager] デプロイメントでリソースに負荷がかかる可能性があります。複雑なアセットがアップロードされたときにサブアセットを生成する場合は、DAM アセットの更新ワークフローにこのステップを追加してください。 オンデマンドでサブアセットを生成する場合は、別のワークフローを作成してサブアセットを生成します。 専用のワークフローを使用すると、DAM アセットの更新ワークフローの他の手順をスキップし、計算リソースを節約することができます。

>[!MORELIKETHIS]
>
>* [Adobe Experience Manager デスクトップアプリケーションの使用](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)
>* [Adobe Experience Manager でのデスクトップアクションの設定](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2)
>* [Adobe Photoshop でのリンクされたスマートオブジェクトの作成](https://helpx.adobe.com/jp/photoshop/using/create-smart-objects.html#create-linked-smart-objects)
>* [Adobe InDesign へのグラフィックの配置](https://helpx.adobe.com/jp/indesign/using/placing-graphics.html)

